## ❤️ Una nota personal

Este proyecto es una idea.

Los documentos del repositorio han sido desarrollados con ayuda de IA. Necesitan revisión, refinamiento y crítica de personas que saben mas que yo jaja.

Lo comparto por que creo que la idea (aunque en fase inicial) esta chula. Si encuentras algo útil, úsalo. Si quieres construir sobre esto, adelante. Avísame que me hará ilusión y si puedo te ayudo ❤️

Gracias por leer

---

# TRACE

**Transparent Review And Cryptographic Evidence
*Una Infraestructura Modular de Revisión por Pares con Trazabilidad Criptográfica***

TRACE es un protocolo open source que separa el rigor técnico de la afinidad ideológica en la evaluación de contenido público — y hace esa separación permanentemente verificable por cualquier persona.

El primer caso de uso es el periodismo. La arquitectura es agnóstica al dominio.

---

## El problema

El contenido público — artículos de noticias, estudios clínicos, informes de política — se evalúa hoy a través de sistemas opacos, centralizados y manipulables. Los fact-checkers son percibidos como sesgados. La revisión por pares es anónima e inrastreable. Las puntuaciones de calidad editorial colapsan metodología e ideología en un único número que no sirve honestamente a nadie.

TRACE no reemplaza estos sistemas. Añade una capa que ninguno de ellos tiene: **un registro público, inmutable y criptográficamente trazable de quién dijo qué sobre qué, y cuándo.**

---

## Cómo funciona

Cada contenido enviado a una instancia de TRACE recibe dos evaluaciones independientes de expertos verificados:

```
RIGOR TÉCNICO      ¿Este trabajo cumple los estándares de calidad?
                   SÍ  /  NO  /  Sin contexto suficiente para valorarlo

AFINIDAD EDITORIAL ¿Estás de acuerdo con la tesis o el enfoque?
                   SÍ  /  NO  /  Me abstengo          (opcional)
```

Estas dos dimensiones nunca se colapsan en una sola puntuación. Un revisor puede validar el rigor de un trabajo con el que discrepa. Esa combinación — `Rigor: SÍ` + `Afinidad: NO` — es la señal más valiosa que produce el sistema. Significa que un experto reconoció calidad cruzando líneas ideológicas. Ese voto es público, firmado e inmutable.

El lector ve ambas dimensiones por separado, segmentadas por perfil del revisor, y decide qué hacer con ellas. **TRACE no interpreta. Muestra. El lector decide.**

---

## Arquitectura

TRACE está construido como cinco módulos independientes. Cualquier institución puede adoptarlos por separado o en combinación, integrados sobre infraestructura existente mediante API.

```
┌──────────────────────────────────────────────────────────────┐
│  MÓDULO 1 — Trazabilidad criptográfica                       │
│  Merkle Tree · GitHub · OpenTimestamps (Bitcoin) · Polygon   │
│  "Lo que se dijo no se puede borrar"                         │
├──────────────────────────────────────────────────────────────┤
│  MÓDULO 2 — Sistema de doble voto                            │
│  Rigor vs. afinidad · Público · Firmado · Inmutable          │
│  "Separa el método del mensaje"                              │
├──────────────────────────────────────────────────────────────┤
│  MÓDULO 3 — Verificación de expertos                         │
│  Criterios objetivos + aval entre pares + percentil          │
│  "Quién puede evaluar y con qué credibilidad"                │
├──────────────────────────────────────────────────────────────┤
│  MÓDULO 4 — Checklist de calidad                             │
│  Autodeclarado · Validado por la comunidad · Documento vivo  │
│  "Qué criterios define cada dominio"                         │
├──────────────────────────────────────────────────────────────┤
│  MÓDULO 5 — Visualización y feed público                     │
│  Capas progresivas de detalle · Sin algoritmo de recomendación│
│  "Cómo ve el lector la información"                          │
└──────────────────────────────────────────────────────────────┘
```

El Módulo 1 es la base. Cualquier otro módulo puede adoptarse de forma independiente. Una plataforma que ya tiene su propio sistema de verificación de expertos puede adoptar solo los Módulos 1 y 2. Una institución que solo necesita trazabilidad inmutable sobre su sistema de valoración existente puede adoptar únicamente el Módulo 1.

---

## Garantías del core

Estas tres propiedades se aplican a cualquier instancia de TRACE, independientemente del dominio o la configuración. Son no negociables.

**Inmutabilidad.** Lo que se registra no puede modificarse retroactivamente sin detección matemática. Cada voto está firmado criptográficamente por el revisor y anclado diariamente en Bitcoin y la blockchain de Polygon. Si el proyecto cierra mañana, el historial de evaluaciones sobrevive indefinidamente.

**Transparencia.** El código que implementa el sistema es completamente público y auditable. No hay algoritmos ocultos, ni pesos de puntuación opacos, ni decisiones editoriales tomadas por la plataforma. Un script público permite a cualquier persona verificar cualquier evaluación sin depender del sistema.

**Portabilidad.** Los datos generados por cualquier instancia pueden exportarse en formatos estándar en cualquier momento. Ninguna institución queda atrapada. El log inmutable permanece en el repositorio público y en blockchain independientemente de lo que ocurra.

---

## Agnóstico al dominio

La primera instancia de TRACE está construida para el periodismo. El protocolo está diseñado para cualquier dominio donde:

- El contenido público requiere evaluación de calidad técnica
- Existe una comunidad de expertos verificables para evaluarlo
- Hay valor en separar el rigor metodológico de la afinidad ideológica o comercial
- La trazabilidad de quién dijo qué importa

**Casos de uso identificados:**

| Dominio | Qué resuelve |
|---|---|
| Periodismo | Separa el rigor técnico del trabajo periodístico de la afinidad editorial |
| Medicina clínica | Separa la calidad metodológica de los estudios de sus implicaciones controvertidas |
| Divulgación científica | Verifica si los artículos de divulgación representan honestamente los papers que citan |
| Informes de política pública / think tanks | Evalúa el rigor metodológico independientemente de las conclusiones ideológicas |
| Revistas científicas independientes | Revisión por pares transparente, trazable y pública |

---

## Esto es un protocolo, no una plataforma

TRACE aporta el 70% — el core técnico, la arquitectura de trazabilidad, el sistema de votos, el modelo de verificación por pares, la filosofía de transparencia radical. El 30% restante — checklist específico del dominio, taxonomía de especialidades, criterios de verificación propios — lo completa cada comunidad que adopta el sistema.

La gobernanza es por fork. No hay comité, no hay proceso de RFC obligatorio, no hay negociación sobre los principios del core. El creador define y mantiene el core con transparencia total. Quien discrepa tiene el código y puede hacer lo que quiera con él. Así funciona la licencia AGPL exactamente como fue diseñada.

La fragmentación no es un defecto. Es el mecanismo de adaptación.

---

## Coste de operación

La infraestructura de trazabilidad cuesta aproximadamente **$0.73/año** en fees de gas de Polygon. Todo lo demás — GitHub, OpenTimestamps, el script público de verificación — es gratuito. El único coste operativo real es el servidor backend (~$5-10/mes en Railway o Render).

---

## Widget embebible y API

> Planificado para Fase 2. No está en el MVP.

Cualquier plataforma puede integrar las evaluaciones de TRACE sin que el lector abandone su propio sitio.

**Una línea de código:**
```html
<script src="https://cdn.trace-protocol.org/widget.js"
        data-content-url="https://ejemplo.com/articulo"
        data-modo="estandar">
</script>
```

**API REST por módulo** para plataformas que quieran consumir módulos específicos sobre su infraestructura existente sin adoptar el sistema completo.

---

## Documentación

| Documento | Descripción |
|---|---|
| [`docs/concept.md`](docs/concept.md) | Conceptualización del proyecto y definición del problema |
| [`docs/traceability.md`](docs/traceability.md) | Arquitectura de trazabilidad criptográfica |
| [`docs/verification.md`](docs/verification.md) | Sistema de verificación de expertos |
| [`docs/votes.md`](docs/votes.md) | Sistema de votos y visualización |
| [`docs/modular.md`](docs/modular.md) | Arquitectura modular y guía de adopción por dominio |
| [`docs/vision.md`](docs/vision.md) | Visión a largo plazo y filosofía |
| [`docs/decisions.md`](docs/decisions.md) | Registro de decisiones de diseño cerradas |
| [`docs/todo.md`](docs/todo.md) | Decisiones pendientes y preguntas abiertas |

---

## Estado

**Fase actual:** Diseño conceptual · Pre-MVP

La documentación de diseño completa está terminada. La implementación no ha comenzado. Este repositorio se está configurando para versionar los documentos de diseño antes de que empiece el desarrollo.

---

## Filosofía

TRACE trata a los lectores y a los expertos como personas adultas y funcionales. No es un padre. No es un árbitro. No es una autoridad.

Da información. Lo que cada uno haga con ella es su decisión.

Si la plataforma no se usa, es problema de quien no la usa. La infraestructura está aquí para quien la quiera.

---

## Licencia

GNU Affero General Public License v3.0 — ver [LICENSE](LICENSE)

Cualquier fork o servicio que use este código debe ser también open source bajo los mismos términos. Esto es intencionado. Una infraestructura de transparencia construida sobre código cerrado sería una contradicción.

---

## Contribuir

El proyecto está en fase de diseño pre-MVP. La contribución más útil ahora mismo es la revisión de los documentos de diseño en `/docs` — huecos identificados, tensiones no resueltas, o conocimiento específico de dominio que mejore la arquitectura antes de que empiece la implementación.

Abre un issue describiendo lo que has encontrado. No hay pull requests de código todavía — todavía no hay código.
