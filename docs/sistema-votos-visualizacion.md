# Sistema de Votos y Visualización
**Módulo:** Núcleo de evaluación · **Versión:** 0.1 · **Estado:** Diseño

---

## 1. Principio de diseño

Este módulo es el núcleo de la plataforma. Todo lo demás — verificación de periodistas, trazabilidad, percentiles — existe para dar contexto a lo que ocurre aquí: un periodista evalúa el trabajo de otro de forma pública, trazable y con su reputación en juego.

El diseño parte de tres compromisos que no se pueden sacrificar:

**Separación estricta entre rigor y afinidad.** Un periodista puede considerar que un artículo está impecablemente hecho y no compartir su tesis. Esas dos dimensiones nunca se colapsan en una sola métrica.

**Transparencia sin excepciones.** Cada voto es público, está vinculado a una identidad verificada y queda en el log inmutable. No hay votos anónimos en el sistema profesional.

**El lector interpreta, la plataforma no pondera.** La plataforma segmenta y muestra. No decide qué votos pesan más — eso lo decide el lector según su propio criterio.

---

## 2. Estructura del voto

### 2.1 Las dos dimensiones

Cada evaluación de un periodista sobre un artículo tiene dos dimensiones independientes:

**RIGOR TÉCNICO — obligatorio**
Evalúa la calidad del trabajo periodístico independientemente de su contenido ideológico.

```
✓  SÍ — El trabajo cumple los estándares de rigor
✗  NO — El trabajo no cumple los estándares de rigor
◎  Sin contexto suficiente para valorarlo
```

La opción "Sin contexto suficiente" no es una abstención cómoda — es una declaración honesta. Un periodista de cultura que no tiene el conocimiento técnico para evaluar una investigación financiera compleja puede y debe usarla. Usarla protege su IHP. Ignorarla y votar NO sistemáticamente en artículos fuera de su especialidad queda expuesto en su historial público.

**AFINIDAD EDITORIAL — opcional**
Evalúa si el periodista comparte el enfoque o la tesis del artículo. Es completamente independiente del rigor.

```
✓  Comparto el enfoque editorial
✗  No comparto el enfoque editorial
◎  Me abstengo de pronunciarme
```

La abstención en afinidad es legítima por múltiples razones: el artículo puede ser tan factual que no hay tesis que compartir o rechazar, el periodista puede no querer posicionarse públicamente en ese tema, o simplemente considera que su opinión editorial no es relevante para ese artículo concreto.

Un periodista puede emitir voto de rigor sin pronunciarse sobre afinidad. No puede emitir voto de afinidad sin haber votado rigor primero — la afinidad sin evaluación técnica previa no tiene valor informativo.

### 2.2 Combinaciones posibles y su significado

```
Rigor ✓ + Afinidad ✓   →  "Bien hecho y comparto la tesis"
Rigor ✓ + Afinidad ✗   →  "Bien hecho aunque discrepo" ← el voto más valioso del sistema
Rigor ✓ + Afinidad ◎   →  "Bien hecho, sin pronunciarme"
Rigor ✗ + Afinidad ✓   →  "Comparto la tesis pero mal ejecutado"
Rigor ✗ + Afinidad ✗   →  "Mal hecho y además discrepo"
Rigor ✗ + Afinidad ◎   →  "Mal hecho, sin pronunciarme sobre la tesis"
Rigor ◎ + (sin afinidad) →  "Sin contexto suficiente para valorar el rigor"
```

El voto `Rigor ✓ + Afinidad ✗` es el más valioso del sistema porque demuestra que el periodista está evaluando el método, no la ideología. Es el tipo de voto que construye el IHP más rápidamente.

### 2.3 Nota opcional

Cualquier periodista puede adjuntar una nota textual a su voto. La nota es siempre pública. Puede explicar el razonamiento del voto, señalar un aspecto concreto del artículo, o añadir contexto que el voto binario no captura.

La nota no es obligatoria pero es visible junto al voto en el historial público. Un periodista que sistemáticamente vota NO sin nota explicativa queda expuesto de forma diferente a uno que argumenta su rechazo con criterios técnicos concretos.

---

## 3. Inmutabilidad y cambios de voto

### Decisión tomada
Los votos son modificables en cualquier momento, pero el historial completo de cambios es público e inmutable en el log.

### Por qué es modificable
Un periodista puede cambiar de criterio al leer más información sobre un artículo, al conocer contexto que no tenía en el momento de votar, o al detectar que cometió un error en su evaluación inicial. Prohibir el cambio de voto sería rígido e injusto.

### Por qué el historial es inmutable
Si los cambios de voto se pudieran hacer sin rastro, un periodista podría votar ✓ inicialmente para no quemar relaciones, y cambiar a ✗ cuando el artículo pierda relevancia sin que nadie lo recuerde. El historial público hace ese comportamiento visible y costoso reputacionalmente.

### Cómo se muestra en la interfaz

```
Juan García votó este artículo:

Voto actual (2026-06-15):  Rigor ✓ · Afinidad ✗
Voto anterior (2026-06-01): Rigor ✗ · Afinidad ✗  [ver nota →]
                                       ↑
                              "Modifiqué mi voto tras leer
                               los documentos fuente citados"
```

El voto actual es el que computa en las métricas. El historial es visible pero no computa.

### Impacto en el log de trazabilidad
Cada cambio de voto genera una nueva entrada en el log — nunca se sobreescribe la anterior. El log es append-only por diseño. Ver documento `arquitectura-trazabilidad.md` sección 5.2.

---

## 4. El voto del autor sobre su propio artículo

### Decisión tomada
Un periodista puede votar su propio artículo. Su voto es visible y público con etiqueta **AUTOR** pero **no computa en ninguna métrica**.

### Por qué existe esta funcionalidad
Tiene un caso de uso concreto y valioso: un periodista que ha trabajado en un medio con el que tiene un conflicto puede usar la plataforma como canal de denuncia pública. Puede señalar que su artículo fue editado sin su consentimiento, que las fuentes fueron alteradas, o que el titular fue cambiado para distorsionar su trabajo.

Es una funcionalidad que ninguna plataforma existente contempla y que encaja directamente con la filosofía del proyecto: dar voz pública y verificable a los periodistas frente a sus propios medios.

### Por qué no computa en las métricas
Si el voto del autor computara, un autor deshonesto podría inflar artificialmente las métricas de su propio artículo (votando ✓ rigor a su propio trabajo) o usarlo para hundir un artículo con el que tiene conflicto personal. Al no computar, el valor informativo se preserva sin contaminar las métricas.

### Cómo se muestra

```
─────────────────────────────────────────────
DECLARACIÓN DEL AUTOR  [no computa en métricas]
─────────────────────────────────────────────
María López (autora)
Rigor: ✗  Afinidad: ✗
"Este artículo fue publicado con modificaciones
 sustanciales que no autoricé. El titular original
 era diferente y las fuentes fueron alteradas en edición."
Fecha: 2026-06-10
─────────────────────────────────────────────
```

Aparece en una sección visualmente diferenciada del resto de votos, antes o después de la lista de votos de revisores, con explicación clara de que no computa en las métricas.

---

## 5. Envío de artículos a revisión

### MVP — Solo el autor puede enviar
Para el MVP, únicamente el autor del artículo puede enviarlo a la plataforma. El autor da consentimiento explícito al enviarlo y asume que recibirá valoraciones públicas sobre su trabajo.

**Razón:** evitar el riesgo legal de evaluar públicamente el trabajo de un periodista sin su conocimiento ni consentimiento. En España y la UE la jurisprudencia sobre plataformas de valoración sin consentimiento del valorado es ambigua. Para el MVP, consentimiento explícito del autor elimina ese riesgo.

### Fase 2 — Cualquiera puede proponer, el autor confirma ⚠️ pendiente de consulta legal

> **Nota del diseño:** esta funcionalidad es la más valiosa a largo plazo pero la que más riesgo legal introduce. No implementar hasta tener asesoramiento legal específico.

El objetivo de esta funcionalidad es doble: permitir **alabar un buen trabajo** que el autor no ha enviado él mismo, y permitir **denunciar un trabajo de baja calidad** que el autor nunca sometería voluntariamente a revisión.

El modelo propuesto para mitigar el riesgo legal:

```
Cualquier periodista Nivel 2+ propone un artículo
        ↓
La plataforma notifica al autor identificado
(por email si está registrado, o públicamente si no lo está)
        ↓
El autor tiene 72 horas para:
  · Confirmar → el artículo entra en revisión con su consentimiento
  · Rechazar  → el artículo no entra, la propuesta queda archivada
                pero visible públicamente con nota "autor rechazó revisión"
  · Ignorar   → tras 72h sin respuesta, el artículo entra en revisión
                con nota "enviado por tercero · autor notificado sin respuesta"
        ↓
En todos los casos, el artículo y su estado son públicos
```

El "autor rechazó revisión" y el "autor notificado sin respuesta" son en sí mismos información para el lector. Un periodista que sistemáticamente rechaza que su trabajo sea revisado públicamente deja un rastro visible.

**Pendiente obligatorio antes de implementar:** consulta legal sobre responsabilidad de la plataforma en los casos de rechazo ignorado y artículos enviados por terceros. Añadir a lista de consultas legales del proyecto.

---

## 6. El IHP — Índice de Honestidad Profesional

El IHP es la métrica más importante del sistema de reputación. Mide en qué medida un periodista evalúa el rigor de los artículos con criterio técnico independiente de su afinidad ideológica.

### Cálculo

```
IHP = Votos cruzados con rigor ✓  /  Total de votos con rigor ✓ emitidos
      ─────────────────────────────────────────────────────────────────
      donde "voto cruzado" = Rigor ✓ + Afinidad ✗ en el mismo voto
```

Un periodista que ha emitido 100 votos de rigor ✓ y en 60 de ellos también votó Afinidad ✗ tiene un IHP de 0.60 — ha validado el rigor de artículos con los que no estaba de acuerdo en el 60% de sus valoraciones positivas.

### Qué mide exactamente y qué no

**Mide:** la disposición del periodista a reconocer calidad técnica en trabajos con los que discrepa ideológicamente.

**No mide:** si el periodista tiene razón en sus valoraciones. Un periodista con IHP alto que vota sistemáticamente mal sigue teniendo IHP alto. El IHP mide coherencia interna, no acierto.

**No mide:** los votos de rigor ✗. Un periodista puede rechazar sistemáticamente artículos de un bando ideológico con los que discrepa — eso queda expuesto en su historial de votos visible, pero no se penaliza en el IHP directamente.

### Umbrales mínimos para calcular el IHP

El IHP no se muestra hasta que el periodista ha emitido un mínimo de **20 votos con pronunciamiento de afinidad**. Con menos votos el índice no es estadísticamente significativo y podría ser engañoso.

```
0-19 votos con afinidad   → "IHP: pendiente (mínimo 20 votos)"
20+ votos con afinidad    → IHP visible como percentil dentro de su especialidad
```

### Visualización del IHP en el perfil

```
IHP — Índice de Honestidad Profesional
────────────────────────────────────────────────────────
Basado en 187 votos emitidos (143 con pronunciamiento de afinidad)

Ha validado rigor en artículos con los que discrepa:  61 veces
Sobre el total de sus valoraciones positivas de rigor: 94 votos ✓

IHP: 0.65   Top 12% en periodismo económico · Top 23% en la plataforma

[Ver desglose completo de votos →]
────────────────────────────────────────────────────────
```

### Limitación conocida: ¿cómo sabe el sistema que un artículo es "de otro bando"?

El sistema no infiere ideología automáticamente — eso sería una caja negra opaca e injusta. La "afinidad" la declara el propio periodista en su voto. Si un periodista vota Rigor ✓ + Afinidad ✗, está declarando él mismo que ha validado un trabajo con el que no está de acuerdo. El IHP se basa en esa autodeclaración, no en ningún algoritmo de clasificación ideológica externa.

---

## 7. Visualización del artículo — tres niveles de detalle

La información se presenta en capas progresivas. El lector casual ve el resumen en tres segundos. El lector crítico puede llegar hasta el último voto individual.

### Nivel 1 — Vista rápida (visible sin clic)

```
┌──────────────────────────────────────────────────────────────────┐
│  "La deuda pública supera el 120% del PIB"                       │
│  Juan García · El Confidencial · Periodismo económico            │
│  2026-05-29                                                       │
│                                                                   │
│  RIGOR TÉCNICO      ████████░░  14 ✓  de 18 revisores            │
│  DIVERSIDAD         ██████░░░░  8 de los 14 ✓ discrepan          │
│                                en afinidad (IHP del artículo)    │
│  AFINIDAD           ████░░░░░░  7 ✓ comparten · 9 ✗ discrepan   │
│                                (solo los que se pronunciaron)    │
│                                                                   │
│  ⚠ Revisado por 18 periodistas · Estadísticas en formación      │
│                                                                   │
│  [Ver desglose por especialidad →]  [Ver todos los votos →]      │
└──────────────────────────────────────────────────────────────────┘
```

La métrica de **Diversidad** es nueva y no habíamos discutido explícitamente — mide cuántos de los periodistas que validaron el rigor también declararon discrepar en afinidad. Es el indicador más directo de que el artículo ha recibido revisión cruzada ideológicamente. Un artículo con rigor alto y diversidad alta es el sello de mayor credibilidad que puede dar el sistema.

El aviso ⚠ aparece siempre que hay menos de un umbral de votos — visible desde el primer voto según la decisión tomada, pero siempre con contexto de cuántos revisores hay.

### Nivel 2 — Vista detallada (un clic)

```
DESGLOSE POR SEGMENTO DE REVISOR
──────────────────────────────────────────────────────────────────
Especialistas en economía verificados (Nivel 2+)
  Rigor ✓: 8   Rigor ✗: 1   Sin contexto: 1   · Total: 10
  De los 8 que validaron: 6 declararon afinidad ✗

Especialistas en economía registrados (Nivel 1)
  Rigor ✓: 3   Rigor ✗: 0   Sin contexto: 1   · Total: 4
  De los 3 que validaron: 1 declaró afinidad ✗

Otras especialidades verificados (Nivel 2+)
  Rigor ✓: 3   Rigor ✗: 1   Sin contexto: 0   · Total: 4
  De los 3 que validaron: 1 declaró afinidad ✗

──────────────────────────────────────────────────────────────────
CHECKLIST DE CALIDAD
  ✓ Fuentes directas enlazadas     [verificado por 14 revisores]
  ✓ Firma real verificable         [verificado automáticamente]
  ✓ Etiquetado como: Análisis      [declarado por el autor]
  ◎ Derecho a réplica              [solicitado · pendiente respuesta]
  ✓ Separación hecho/valoración    [verificado por 11 revisores]

──────────────────────────────────────────────────────────────────
DECLARACIÓN DEL AUTOR  [no computa en métricas]
  No hay declaración del autor sobre este artículo
```

### Nivel 3 — Vista de auditoría completa (segundo clic)

```
TODOS LOS VOTOS — orden cronológico
──────────────────────────────────────────────────────────────────
2026-06-01 · María López · Economía · Nivel 2 · Top 8% especialidad
  Rigor: ✓  Afinidad: ✗
  "Fuentes primarias sólidas. Discrepo con la interpretación
   del dato de deuda consolidada vs. deuda bruta."
  [Ver perfil →]  [Ver historial de este voto →]

2026-06-02 · Carlos Ruiz · Economía · Nivel 2 · Top 21% especialidad
  Rigor: ✓  Afinidad: ✓
  [sin nota]
  [Ver perfil →]

2026-06-03 · Ana Martínez · Política · Nivel 1
  Rigor: ◎  — Sin contexto técnico suficiente para valorar rigor económico
  [Ver perfil →]

[... 15 votos más ...]

──────────────────────────────────────────────────────────────────
HISTORIAL DE CAMBIOS DE VOTO
  Pedro García cambió su voto el 2026-06-10:
  Anterior: Rigor ✗ · Afinidad ✗
  Actual:   Rigor ✓ · Afinidad ✗
  Nota: "Revisé los documentos fuente adjuntos. El rigor es correcto."
```

---

## 8. El feed de artículos

### Ordenación por defecto
Cronológico inverso — los más recientes primero. Sin algoritmo de recomendación en MVP. Lo que se publica se muestra, en el orden en que se publicó.

La ausencia de algoritmo es una decisión filosófica: ningún sistema de recomendación es neutro. Todos amplifican ciertos tipos de contenido sobre otros. Empezar sin algoritmo es más honesto y más simple. Si en el futuro se añade, el criterio de ordenación debe ser público y auditable.

### Filtros disponibles en MVP

```
Por especialidad del artículo
Por nivel mínimo de revisores
Por número mínimo de votos recibidos
Por fecha de publicación
Por medio de origen
```

### Lo que NO hay en el feed en MVP
- Ordenación por "más votado" o "mejor valorado" — amplifica sesgos de popularidad
- Recomendaciones personalizadas — requiere algoritmo opaco
- Trending o artículos destacados — introduce criterio editorial de la plataforma

---

## 9. Estructura de datos del voto

```javascript
const voto = {
  schema_version: 1,
  id: "voto_00847",
  articulo_id: "art_00234",
  articulo_hash: "a3f8c2d9e1b4...",    // hash del artículo en momento de envío
  periodista_id: "juan_garcia_v2",      // id interno
  periodista_nivel: 2,                  // nivel en el momento del voto
  periodista_especialidades: ["economia", "investigacion"],
  es_autor: false,                      // true si vota su propio artículo
  rigor: "si",                          // "si" | "no" | "sin_contexto"
  afinidad: "no",                       // "si" | "no" | "abstencion" | null
  nota: "Fuentes primarias sólidas...", // null si no hay nota
  timestamp: "2026-06-01T10:32:11Z",
  firma: "0x8f3a...",                   // firma criptográfica del periodista
  es_modificacion: false,               // true si es un cambio de voto anterior
  voto_anterior_id: null               // id del voto anterior si es modificación
}
```

---

## 10. Relación con otros módulos

| Módulo | Dependencia |
|---|---|
| Verificación de periodistas | El nivel y especialidad del periodista en el momento del voto determinan en qué capa visual aparece |
| Arquitectura de trazabilidad | Cada voto genera una entrada en el log append-only. El job nocturno lo incluye en el Merkle Tree diario |
| IHP | Se calcula a partir del historial de votos de este módulo. Se actualiza en tiempo real con cada nuevo voto |
| Checklist de calidad | Los revisores pueden confirmar o refutar cada punto del checklist del autor desde la vista de votación |

---

## 11. Decisiones pendientes antes de implementar

- [ ] **Envío por terceros (Fase 2):** consulta legal obligatoria antes de implementar. Ver sección 5 de este documento para el modelo propuesto.
- [ ] **Umbral de diversidad mínima:** ¿a partir de cuántos votos cruzados se muestra la métrica de Diversidad como significativa? Actualmente se muestra desde el primer voto con aviso visual — igual que el resto de métricas.
- [ ] **Notificaciones al autor:** cuando su artículo recibe votos, ¿se le notifica? ¿Con qué frecuencia? ¿Puede desactivar las notificaciones?
- [ ] **Votación de artículos históricos:** ¿puede un periodista votar un artículo publicado hace 3 años? ¿Hay fecha de caducidad para recibir votos? Sin límite temporal los artículos pueden recibir campañas de votos coordinadas mucho después de su publicación.
- [ ] **Peso visual del historial de cambios de voto:** actualmente se muestra al mismo nivel que el voto actual. ¿Debería estar más o menos visible? Un periodista que cambia sus votos frecuentemente puede estar actuando honestamente o puede estar gestionando su reputación estratégicamente.

---

*Documento del módulo de votos y visualización · Parte del conjunto de documentos de diseño del proyecto*
