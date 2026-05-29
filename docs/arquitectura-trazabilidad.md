# Arquitectura de Trazabilidad e Inmutabilidad
**Módulo:** Infraestructura de confianza · **Versión:** 0.1 · **Estado:** Diseño

---

## 1. Principio de diseño

El valor central de la plataforma es la **transparencia radical verificable**. No basta con decir que los votos son públicos e inmutables — cualquier persona, sin confiar en el proyecto, debe poder comprobarlo matemáticamente por su cuenta.

Para esto se usa una arquitectura de **cuatro capas complementarias**, no alternativas. Cada capa cubre los puntos de fallo de las demás.

> **Propiedad crítica:** si el proyecto cierra mañana, si el equipo se corrompe, o si un gobierno presiona para eliminar datos, el historial de votos y artículos sobrevive de forma independiente en múltiples sistemas que no se pueden apagar simultáneamente sin que nadie lo note.

---

## 2. Visión general de la arquitectura

```
CAPA 1 — Datos operacionales
──────────────────────────────────────────────────────
PostgreSQL (servidor propio)
· Votos completos con firma criptográfica del periodista
· Artículos: URL, metadatos, hash del contenido
· Perfiles y credenciales de periodistas verificados

                    ↓ job nocturno (cada 24h)

CAPA 2 — Merkle Tree diario
──────────────────────────────────────────────────────
· Se construye un árbol con todos los votos del día
· Genera una única Merkle Root (huella del día)
· Ejemplo: "f7a3c8d2e9b14a3f..."

                    ↓ esa raíz se publica en 4 sitios

CAPA 3 — Publicación múltiple simultánea
──────────────────────────────────────────────────────
┌──────────────┐  ┌────────────────┐  ┌──────────────┐  ┌──────────────┐
│    GitHub    │  │ OpenTimestamps │  │   Polygon    │  │   Mirrors    │
│   (público)  │  │   (Bitcoin)    │  │ (blockchain) │  │  (comunidad) │
│              │  │                │  │              │  │              │
│ Commit con   │  │ Ancla el hash  │  │ 1 tx/día     │  │ Cualquiera   │
│ historial    │  │ en Bitcoin     │  │ ~$0.002      │  │ puede clonar │
│ completo     │  │ Gratis         │  │ inmutable    │  │ el repo      │
└──────────────┘  └────────────────┘  └──────────────┘  └──────────────┘
```

---

## 3. Por qué cuatro capas y no una

Cada capa ataca un vector de fallo diferente:

| Si falla o es comprometido... | Lo cubren... |
|---|---|
| El servidor propio | GitHub + Blockchain + OpenTimestamps |
| GitHub (manipulación o cierre) | Blockchain + OpenTimestamps + mirrors |
| OpenTimestamps | Blockchain + GitHub + mirrors |
| Polygon blockchain | GitHub + OpenTimestamps + mirrors |
| El propio equipo del proyecto | Todo es público, verificable sin permiso de nadie |
| El proyecto cierra | Datos en blockchain sobreviven para siempre |

Para manipular el historial sin que nadie lo note habría que comprometer los cuatro sistemas simultáneamente. Eso es computacionalmente y logísticamente imposible.

---

## 4. Cómo funciona el Merkle Tree

### Concepto

Un árbol de Merkle es una estructura donde cada nodo es el hash de sus hijos. Esto permite:
- Representar miles de votos con **un solo hash** (la raíz)
- Verificar que un voto específico está incluido sin descargar todos los datos (**prueba de inclusión**)
- Detectar cualquier manipulación porque un cambio mínimo rompe toda la cadena de hashes

### Estructura visual

```
                    MERKLE ROOT
                   "f7a3c8d2..."
                  /             \
         Hash(votos 1-500)   Hash(votos 501-1000)
         /          \          /              \
    H(1-250)    H(251-500)  H(501-750)   H(751-1000)
      ...           ...        ...            ...
    Voto1 Voto2 ... Voto500  ...           Voto1000
```

### Prueba de inclusión

Para verificar que el Voto A está en la raíz publicada, no se necesitan todos los votos. Solo:

```
Hash(B)  +  Hash(C+D)  +  Merkle Root conocida
```

Con estos tres valores cualquiera puede reconstruir matemáticamente el camino y verificar la inclusión. Esto es lo que hace el script público `verificar.js`.

---

## 5. Estructura de datos

### 5.1 Hash de artículo

Calculado en el momento de publicación. Cualquier modificación posterior al artículo original queda demostrada matemáticamente.

```javascript
const articulo = {
  url: "https://...",
  titulo: "Título del artículo",
  autor: "id_periodista_verificado",
  fecha_publicacion: "2026-05-29T10:32:00Z",
  checksum_contenido: sha256(textoCompleto)  // hash del texto íntegro
}

const hash_articulo = sha256(JSON.stringify(articulo))
// → "a3f8c2d9e1b4..."  ← se publica en GitHub inmediatamente
```

### 5.2 Voto individual con firma criptográfica

```javascript
const voto = {
  id: "voto_00847",
  periodista_id: "juan_garcia_verified",
  articulo_hash: "a3f8c2d9e1b4...",   // vincula voto a artículo exacto
  rigor: true,                         // ¿está bien hecho?
  afinidad: false,                     // ¿estás de acuerdo?
  timestamp: "2026-05-29T10:32:11Z",
  firma: sign(privateKey_periodista, sha256(voto))
}
```

La firma criptográfica es crítica: demuestra que el periodista emitió ese voto con su clave privada. El servidor no puede fabricar votos en su nombre. Nadie puede.

### 5.3 Merkle Root diaria

```javascript
const registro_diario = {
  fecha: "2026-05-29",
  total_votos: 847,
  merkle_root: "f7a3c8d2e9b14a3f...",
  hash_dia_anterior: "d2e9b14a3fc8f7a3...",  // encadena los días entre sí
  timestamp_github: "commit sha...",
  timestamp_bitcoin: "bloque 894721",
  timestamp_polygon: "tx 0x8f3a..."
}
```

El campo `hash_dia_anterior` encadena los días formando una cadena continua — exactamente el mismo principio que blockchain, pero construido por el proyecto.

---

## 6. Repositorio público de trazabilidad

Repositorio GitHub separado del código principal, dedicado exclusivamente al log de trazabilidad.

```
/merkle-log
  /2026-05-29
    root.txt              ← "f7a3c8d2e9b14a3f..."
    votos.jsonl           ← todos los votos del día, uno por línea
    articulos.jsonl       ← hashes de artículos publicados ese día
    pruebas/
      voto_00847.json     ← prueba de inclusión para ese voto
  /2026-05-30
    root.txt
    votos.jsonl
    ...
  verificar.js            ← script open source para verificar cualquier voto
  README.md               ← instrucciones de verificación para no técnicos
```

### Output del verificador

```bash
$ node verificar.js --voto voto_00847

✓ Voto 00847 verificado
  Periodista:  juan_garcia_verified
  Artículo:    a3f8c2d9e1b4...
  Rigor:       SÍ
  Afinidad:    NO
  Fecha:       2026-05-29 10:32:11
  ✓ Firma criptográfica válida
  ✓ Incluido en raíz del día: f7a3c8d2e9b1...
  ✓ Raíz anclada en Bitcoin: bloque 894721
  ✓ Raíz anclada en Polygon: tx 0x8f3a...
```

---

## 7. Publicación en Polygon blockchain

Solo se sube la Merkle Root diaria. Una transacción al día. No se sube ningún dato personal ni contenido de votos — solo el hash que permite verificarlos.

```solidity
// Contrato minimalista — solo registro de raíces
contract MerkleLog {
    mapping(string => string) public roots; // fecha → merkle root
    address public owner;

    event RootRegistered(string date, string root, uint256 timestamp);

    function registerRoot(string calldata date, string calldata root) external {
        require(msg.sender == owner, "Solo el sistema puede registrar");
        require(bytes(roots[date]).length == 0, "Ya existe raiz para esta fecha");
        roots[date] = root;
        emit RootRegistered(date, root, block.timestamp);
    }
}
```

**Una vez registrada una raíz, el contrato no permite sobreescribirla.** Ni el propio proyecto puede modificarla.

### Coste real en Polygon

| Operación | Frecuencia | Coste unitario | Coste anual |
|---|---|---|---|
| Deploy del contrato | Una vez | ~$0.50 | $0.50 |
| Registrar raíz diaria | 365/año | ~$0.002 | ~$0.73 |
| **Total año 1** | | | **~$1.23** |

---

## 8. Publicación en OpenTimestamps (Bitcoin)

OpenTimestamps es un protocolo open source que ancla hashes en la blockchain de Bitcoin de forma gratuita. Lleva funcionando desde 2016 y es ampliamente usado en periodismo de investigación y documentación legal.

```javascript
// Llamada a la API de OpenTimestamps
const ots = require('javascript-opentimestamps')

async function anclarEnBitcoin(merkleRoot) {
  const hash = Buffer.from(merkleRoot, 'hex')
  const timestamp = await ots.stamp(hash)
  // guarda el archivo .ots — es la prueba de existencia en Bitcoin
  fs.writeFileSync(`${fecha}.ots`, timestamp)
}
```

El archivo `.ots` generado es la prueba criptográfica de que ese hash existía en esa fecha. Se sube también al repositorio público.

---

## 9. Job nocturno: el proceso completo

Este proceso se ejecuta automáticamente cada día a las 00:00 UTC.

```
00:00 UTC
  │
  ├─ 1. Recoger todos los votos del día desde PostgreSQL
  │
  ├─ 2. Construir el Merkle Tree con todos los votos
  │
  ├─ 3. Extraer la Merkle Root
  │
  ├─ 4. Generar pruebas de inclusión para cada voto
  │
  ├─ 5. Escribir votos.jsonl y pruebas/ en el repo local
  │
  ├─ 6. Commit y push al repositorio GitHub público
  │       → inmediato, timestamp de GitHub
  │
  ├─ 7. Llamar a OpenTimestamps API con la raíz
  │       → ancla en Bitcoin (puede tardar horas en confirmarse)
  │
  ├─ 8. Enviar transacción a Polygon con la raíz
  │       → confirmación en ~16 segundos
  │
  └─ 9. Actualizar registro_diario en PostgreSQL con todos los timestamps
```

---

## 10. Coste total de la infraestructura de trazabilidad

| Componente | Coste mensual | Coste anual |
|---|---|---|
| GitHub (repo público) | $0 | $0 |
| OpenTimestamps | $0 | $0 |
| Polygon (1 tx/día) | ~$0.06 | ~$0.73 |
| POL inicial en wallet | $5 (única vez, dura años) | — |
| **Total** | **~$0.06/mes** | **~$0.73/año** |

El único coste real del proyecto es el servidor backend (~$5-10/mes en Railway o Render).

---

## 11. Stack técnico de este módulo

| Componente | Tecnología |
|---|---|
| Hashing | `crypto` (Node.js nativo) — SHA-256 |
| Firmas criptográficas | `@noble/secp256k1` o `ethers.js` |
| Merkle Tree | `merkletreejs` (librería JS) |
| Blockchain interaction | `ethers.js` + `viem` |
| OpenTimestamps | `javascript-opentimestamps` |
| Smart contract | Solidity — minimalista, solo registro |
| Red blockchain | Polygon PoS (token: POL) |
| Job nocturno | Cron job en el propio servidor |

---

## 12. Orden de implementación

Los módulos se construyen en este orden estricto porque cada uno depende del anterior:

- [ ] **Módulo 1 — Hashing de artículos**
  Calcular y almacenar el hash en el momento de publicación. Sin dependencias externas. Define la estructura de datos base.

- [ ] **Módulo 2 — Firmas criptográficas de votos**
  Generación de claves para periodistas. Firma de votos. Verificación en el servidor.

- [ ] **Módulo 3 — Merkle Tree diario**
  Job nocturno que construye el árbol y genera las pruebas de inclusión.

- [ ] **Módulo 4 — Publicación en GitHub**
  Commit automático del log diario al repositorio público.

- [ ] **Módulo 5 — Publicación en OpenTimestamps**
  Integración con la API. Almacenamiento del archivo `.ots`.

- [ ] **Módulo 6 — Smart contract en Polygon**
  Deploy del contrato. Integración del job nocturno con la transacción diaria.

- [ ] **Módulo 7 — Verificador público**
  Script `verificar.js` que cualquiera puede ejecutar para auditar cualquier voto o artículo.

---

## 13. Contexto ético

Esta arquitectura es técnicamente superior a la que usan la mayoría de plataformas de verificación periodística existentes — The Trust Project, Maldita, Newtral — ninguna tiene trazabilidad criptográfica de sus decisiones editoriales.

El diseño garantiza que **ni el propio proyecto puede mentir sobre su historial**. Eso no es un detalle técnico — es la base de la credibilidad de toda la plataforma.

---

## 14. Gestión de claves privadas de los periodistas

> ⚠️ **Decisión pendiente — afecta a la garantía fundamental del sistema.**

La firma criptográfica de los votos solo tiene valor si la clave privada está exclusivamente en poder del periodista. Si el servidor custodia las claves, puede suplantar votos. La garantía desaparece.

Hay tres modelos posibles, con sus consecuencias:

| Modelo | Cómo funciona | Ventaja | Riesgo |
|---|---|---|---|
| **A — Servidor custodia la clave** | El servidor genera y guarda la clave del periodista | Sin fricción para el periodista | El servidor puede fabricar votos. Rompe la garantía central. **Descartar.** |
| **B — El periodista custodia su clave** | Se genera un par de claves en el onboarding, el periodista descarga y guarda su clave privada | Garantía real, sin dependencias externas | Si pierde la clave, pierde la capacidad de votar y su historial queda huérfano |
| **C — Wallet Ethereum (MetaMask)** | El periodista usa su propia wallet como identidad firmante | Clave siempre en su poder, estándar conocido, compatible con el contrato de Polygon | Fricción de onboarding para periodistas no técnicos |

**Recomendación provisional:** Modelo C para fase de producción — la wallet es la solución más robusta y alineada con la arquitectura blockchain del proyecto. Para el MVP, Modelo B con instrucciones claras de custodia de clave.

**Problema no resuelto — requiere decisión antes de implementar:**
- ¿Qué ocurre si un periodista pierde su clave privada? ¿Se le emite una nueva? ¿Los votos anteriores quedan desvinculados de su nueva identidad?
- ¿Hay un proceso de recuperación? ¿Quién lo autoriza?
- Si se usa wallet, ¿qué pasa si el periodista pierde acceso a MetaMask?

---

## 15. Resiliencia del job nocturno

> ⚠️ **Un log de trazabilidad con huecos es peor que no tener log — da falsa sensación de seguridad.**

El documento asume que el cron job funciona perfectamente. En la práctica fallará. Hay que diseñar el comportamiento ante fallos antes de implementar.

### Política de reintentos

```
00:00 UTC — Ejecución principal
  │
  ├─ ✓ Éxito → registrar timestamp, continuar
  │
  └─ ✗ Fallo → esperar 15 min → reintento 1
                  │
                  ├─ ✓ Éxito → registrar timestamp + nota "reintento 1"
                  │
                  └─ ✗ Fallo → esperar 15 min → reintento 2
                                  │
                                  ├─ ✓ Éxito → registrar timestamp + nota "reintento 2"
                                  │
                                  └─ ✗ Fallo → ALERTA al administrador
                                               → marcar día como "pendiente"
                                               → incluir en el árbol del día siguiente
```

### Votos huérfanos (emitidos durante un fallo)

Si el job falla y hay votos sin procesar, la política es clara: **los votos no se pierden ni se omiten**. Se acumulan y se incluyen en el árbol del siguiente ciclo exitoso, con su timestamp original preservado. El log registra explícitamente que esos votos corresponden al día X pero fueron anclados el día Y.

### Alertas mínimas necesarias

- Fallo total del job nocturno → notificación inmediata al administrador
- Transacción de Polygon sin confirmar tras 5 minutos → reintento
- OpenTimestamps sin confirmar tras 24 horas → anotación en el log (es normal, Bitcoin puede tardar)
- Discrepancia entre número de votos en PostgreSQL y en `votos.jsonl` → alerta crítica

---

## 16. Privacidad vs. trazabilidad — GDPR y votos ciudadanos

> ⚠️ **Decisión con implicaciones legales. Requiere análisis antes de escribir código de usuarios.**

El sistema publica `votos.jsonl` con el identificador del periodista visible. Eso es intencionado y es el núcleo del proyecto. Pero hay dos casos no resueltos:

### Caso 1 — Votos ciudadanos

Los votos de usuarios registrados no tienen el mismo contrato de transparencia que los periodistas. Publicar su identidad en un log público puede violar el GDPR (el usuario es ciudadano europeo en la mayoría de casos).

Opciones:

| Opción | Cómo funciona | Implicación |
|---|---|---|
| **Hash anónimo del usuario** | Se publica `sha256(user_id + salt)` en lugar del ID real | Verificable estadísticamente, no vinculable a persona real |
| **Solo agregados** | El log solo publica el total de votos ciudadanos por artículo, no votos individuales | Pierde trazabilidad individual pero cumple GDPR sin fricción |
| **Opt-in de transparencia** | El usuario decide si su voto es público o anónimo | Más complejo, respeta autonomía del usuario |

**Recomendación provisional:** Hash anónimo para el log público + opción de opt-in de transparencia para usuarios que quieran que su voto sea visible con su nombre.

### Caso 2 — Derecho al olvido (GDPR Art. 17)

Un usuario puede solicitar que se borren sus datos. Pero los votos están en un log inmutable en blockchain y GitHub. Hay una tensión legal real aquí.

**Solución estándar en sistemas blockchain + GDPR:** Los datos personales nunca van on-chain ni al log público. Solo van hashes. Si el usuario ejerce el derecho al olvido, se borra su registro en PostgreSQL (el dato real). El hash en el log queda huérfano — matemáticamente presente pero imposible de vincular a ninguna persona. Esto es legalmente aceptado en la mayoría de interpretaciones del GDPR aplicadas a blockchain.

**Pendiente:** Consulta legal antes del lanzamiento. No es opcional.

---

## 17. Versionado del esquema de datos

> ⚠️ **El Merkle Tree es sensible a la estructura exacta del dato. Un campo nuevo rompe la compatibilidad con votos anteriores si no se gestiona correctamente.**

### Todos los objetos llevan versión explícita

```javascript
const voto = {
  schema_version: 1,          // ← campo obligatorio en todos los objetos
  id: "voto_00847",
  periodista_id: "juan_garcia_verified",
  articulo_hash: "a3f8c2d9e1b4...",
  rigor: true,
  afinidad: false,
  timestamp: "2026-05-29T10:32:11Z",
  firma: "..."
}
```

### Política de cambios de esquema

- **Añadir un campo nuevo:** Se incrementa `schema_version`. Los votos antiguos (version 1) y los nuevos (version 2) coexisten en el mismo árbol. El verificador debe conocer todos los esquemas históricos.
- **Modificar o eliminar un campo:** Requiere migración completa. Se documenta en el CHANGELOG del repositorio con la fecha exacta.
- **El verificador público** debe manejar todas las versiones anteriores de esquema sin errores. Un voto de la versión 1 debe ser verificable indefinidamente aunque hoy se use la versión 4.

### Registro de versiones

```
/merkle-log
  schemas/
    voto_v1.json        ← definición exacta del esquema versión 1
    voto_v2.json        ← definición exacta del esquema versión 2
    articulo_v1.json
    ...
  CHANGELOG.md          ← cuándo y por qué cambió cada esquema
```

---

## 18. Seguridad del smart contract — gestión del owner

> ⚠️ **El owner del contrato es un punto único de fallo. Si se pierde o compromete la clave, el contrato queda inutilizable o vulnerable para siempre.**

### El problema

El contrato actual tiene:
```solidity
require(msg.sender == owner, "Solo el sistema puede registrar");
```

Si la clave privada del `owner` se pierde → nunca más se pueden registrar raíces. Permanentemente.
Si la clave privada del `owner` se compromete → alguien puede registrar raíces falsas.

Dado que el contrato es inmutable una vez desplegado, no hay forma de corregirlo después.

### Solución: Multisig

En lugar de una sola clave como owner, se usa un **contrato multisig** (múltiples firmas requeridas). El estándar más usado es **Safe (antes Gnosis Safe)**, open source y ampliamente auditado.

```
Configuración recomendada para el MVP: 2 de 3
→ Existen 3 claves (3 personas de confianza del proyecto)
→ Cualquier operación requiere la firma de al menos 2 de ellas
→ Si una clave se pierde, las otras dos pueden operar con normalidad
→ Para comprometer el sistema, un atacante necesita 2 claves simultáneamente
```

### Operaciones que requieren multisig

| Operación | ¿Requiere multisig? |
|---|---|
| Registrar raíz diaria | No — la puede hacer el servidor automáticamente con su propia clave delegada |
| Transferir ownership del contrato | Sí — requiere 2 de 3 |
| Actualizar la dirección del servidor autorizado | Sí — requiere 2 de 3 |
| Deploy de un contrato nuevo (upgrade) | Sí — requiere 2 de 3 |

### Contrato actualizado con owner transferible y dirección de servidor separada

```solidity
contract MerkleLog {
    mapping(string => string) public roots;
    address public owner;        // multisig — operaciones críticas
    address public registrar;    // servidor — solo puede registrar raíces

    event RootRegistered(string date, string root, uint256 timestamp);
    event RegistrarUpdated(address oldRegistrar, address newRegistrar);

    modifier onlyOwner() {
        require(msg.sender == owner, "Solo owner");
        _;
    }

    modifier onlyRegistrar() {
        require(msg.sender == registrar, "Solo registrar");
        _;
    }

    function registerRoot(string calldata date, string calldata root)
        external onlyRegistrar {
        require(bytes(roots[date]).length == 0, "Ya existe raiz para esta fecha");
        roots[date] = root;
        emit RootRegistered(date, root, block.timestamp);
    }

    function updateRegistrar(address newRegistrar) external onlyOwner {
        emit RegistrarUpdated(registrar, newRegistrar);
        registrar = newRegistrar;
    }

    function transferOwnership(address newOwner) external onlyOwner {
        owner = newOwner;
    }
}
```

Esta versión separa dos roles: el `owner` (multisig, para operaciones críticas) y el `registrar` (servidor automático, solo para registrar raíces diarias). Si el servidor se compromete, el multisig puede revocar su acceso sin tocar el historial.

**Pendiente antes del deploy:** Definir quiénes son los 3 titulares de las claves del multisig. Deben ser personas de confianza ajenas entre sí.

---

*Documento de arquitectura técnica · Parte del conjunto de documentos de diseño del proyecto*
