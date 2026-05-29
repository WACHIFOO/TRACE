# Sistema de Verificación de Periodistas
**Módulo:** Identidad y reputación profesional · **Versión:** 0.1 · **Estado:** Diseño

---

## 1. Principio de diseño

La verificación de periodistas es la decisión de diseño más importante de toda la plataforma. Todo lo demás depende de ella. Si el sistema de verificación es débil, cualquier actor puede entrar y destruir la credibilidad del índice de rigor. Si es demasiado estricto, excluye a periodistas independientes excelentes y la plataforma se convierte en un club cerrado de medios tradicionales — exactamente lo que intenta evitar.

El equilibrio se resuelve con tres principios:

**Primero, criterios objetivos públicos.** Los requisitos de verificación son conocidos por cualquiera antes de solicitar la entrada. No hay discrecionalidad oculta.

**Segundo, validación distribuida entre pares.** La plataforma no certifica periodistas — la comunidad los avala. El proyecto solo verifica que los documentos aportados son reales. La validación profesional la hacen otros periodistas.

**Tercero, transparencia del proceso.** Todo el proceso de verificación de cada periodista es público y auditable. Los avales, los rechazos, los documentos aportados y su estado son visibles para cualquier lector.

> **Consecuencia directa:** la plataforma nunca dice "este periodista es bueno". Dice "este periodista ha aportado esta documentación verificada y ha recibido este respaldo de la comunidad". El lector interpreta.

---

## 2. Quién puede ser periodista verificado

La plataforma no exige carné de prensa oficial. Eso excluiría a los mejores periodistas independientes, que son el público objetivo del MVP. En cambio, se exige una combinación de **criterios objetivos verificables** más **aval de la comunidad**.

### Criterios objetivos (al menos uno del Grupo A + al menos uno del Grupo B)

**Grupo A — Identidad profesional**
- Carné de prensa oficial vigente (FAPE u organismo equivalente en su país)
- Titulación universitaria en Periodismo, Comunicación o rama afín
- Acreditación profesional de organismo de prensa reconocido

**Grupo B — Historial público verificable**
- Mínimo 10 artículos publicados firmados con nombre real en medios con ISSN registrado
- Mínimo 10 artículos publicados firmados en plataformas de distribución con audiencia verificable (Substack, newsletter propia con suscriptores demostrables, podcast con descargas auditables)
- Libro de no ficción publicado con ISBN sobre temática periodística o de investigación

Un periodista independiente sin titulación ni carné puede entrar perfectamente si tiene historial público verificable. Un recién titulado sin historial puede entrar con su titulación. Un periodista veterano con décadas de trabajo documentado puede entrar aunque no tenga carné oficial.

### Lo que no es criterio de entrada
- Seguidores en redes sociales
- Número de lectores o visitas
- Afiliación a un medio concreto
- Opinión del equipo del proyecto sobre la calidad de su trabajo

---

## 3. El modelo de verificación: criterios objetivos + aval de pares

Se combinan dos modelos complementarios:

**Modelo de criterios objetivos (Modelo 3 en la literatura):** define qué documentación hay que aportar. Es el filtro de entrada. La plataforma verifica que los documentos son reales — no juzga si el periodista "merece" entrar.

**Modelo de aval entre pares (Modelo 2 en la literatura):** un periodista ya verificado responde públicamente por el solicitante. El aval tiene coste reputacional para quien lo da — si avalas a alguien que luego actúa de mala fe, tu aval queda registrado en tu historial público permanentemente.

Ambos modelos son necesarios. Solo criterios objetivos sin aval permite entrar a periodistas con historial real pero que nadie en la comunidad conoce ni valida. Solo aval sin criterios objetivos convierte la verificación en un sistema de favores entre grupos ideológicos.

---

## 4. Niveles de verificación

No hay un binario verificado/no verificado. Hay un espectro continuo con tres niveles de entrada según la documentación y el respaldo aportados.

### Nivel 1 — Periodista registrado
**Requisitos:**
- Criterio objetivo del Grupo A o del Grupo B cumplido y verificado
- Sin aval de pares requerido

**Capacidades:**
- Puede votar rigor y afinidad en cualquier artículo
- Su voto aparece en la capa "Periodistas registrados" de la visualización
- No puede avalar a otros periodistas

**Nota:** es el nivel de entrada para MVP. Cualquier periodista con documentación verificable puede empezar a participar sin depender de que nadie le avale.

### Nivel 2 — Periodista verificado
**Requisitos:**
- Criterio objetivo del Grupo A o del Grupo B cumplido y verificado
- Mínimo 1 aval de un periodista Nivel 2 o superior
- Sin rechazos activos de la comunidad

**Capacidades:**
- Todo lo del Nivel 1
- Su voto aparece en la capa "Periodistas verificados" de la visualización, con mayor visibilidad
- Puede avalar a periodistas que solicitan Nivel 2
- Puede rechazar avales con nota pública

### Nivel 3 — Periodista verificado senior
**Requisitos:**
- Nivel 2 consolidado
- Mínimo 3 avales de periodistas Nivel 2 o superior
- Índice de Honestidad Profesional (IHP) en percentil 70 o superior dentro de su especialidad
- Historial de al menos 50 votos emitidos en la plataforma

**Capacidades:**
- Todo lo del Nivel 2
- Puede añadir anotaciones de contexto directamente sobre párrafos de artículos
- Puede escalar casos de manipulación de guante blanco para revisión ampliada
- Puede avalar periodistas para Nivel 3
- Su especialidad declarada aparece destacada visualmente en su perfil y en sus votos

---

## 5. Especialidades declaradas

El periodista declara su especialidad al crear el perfil. La declaración es pública desde el primer día y verificable por cualquier lector a través del historial de artículos vinculados.

### Categorías disponibles (selección múltiple)

```
Periodismo de investigación
Periodismo político
Periodismo económico y financiero
Periodismo judicial y legal
Periodismo científico y tecnológico
Periodismo internacional
Periodismo de datos
Periodismo local y territorial
Periodismo cultural
Periodismo deportivo
Opinión y análisis
Divulgación
```

### Cómo se verifica la especialidad declarada

El periodista vincula artículos propios publicados como evidencia de cada especialidad declarada. Estos artículos son públicamente accesibles. Cualquier lector puede comprobar si la especialidad declarada se corresponde con el trabajo real.

La comunidad no vota formalmente sobre si la especialidad es correcta — pero cualquier periodista verificado puede dejar una nota pública si considera que la especialidad declarada no se corresponde con el historial aportado. Esa nota queda visible en el perfil.

No hay árbitro que certifique especialidades. La transparencia del historial hace ese trabajo.

---

## 6. El perfil público del periodista

Todo es visible para cualquier lector sin necesidad de registrarse.

```
─────────────────────────────────────────────────────────────
Juan García
Periodista verificado · Nivel 2
─────────────────────────────────────────────────────────────
Especialidades declaradas:
  · Periodismo económico      [34 artículos vinculados →]
  · Periodismo de investigación [12 artículos vinculados →]

Documentación aportada:
  ✓ Titulación universitaria en Periodismo     [verificada por la plataforma]
  ✓ 47 artículos en El Confidencial            [verificados por la plataforma]
  ✓ Newsletter propia · 3.200 suscriptores     [verificada por la plataforma]

Respaldo de la comunidad:
  Avales recibidos:   23    Top 8%  de 47 especialistas en economía verificados
  Avales recibidos:   23    Top 21% de 340 periodistas verificados totales
  Rechazos recibidos:  2    [Ver notas públicas →]
  Avalado por:        [María López →] [Carlos Ruiz →] [+21 más →]

Actividad en la plataforma:
  Votos emitidos: 187
  IHP (Índice de Honestidad Profesional): Top 12% en su especialidad
  Miembro desde: 2026-06-01
─────────────────────────────────────────────────────────────
[Ver historial completo de votos →]   [Ver artículos vinculados →]
```

### Por qué se muestran los rechazos

Un rechazo no significa necesariamente que el periodista sea deshonesto o de baja calidad. Puede significar que el revisor no lo conoce, que hay un conflicto personal, o que hay discrepancia ideológica sin base técnica. El lector ve tanto los avales como los rechazos y las notas públicas asociadas, y decide por sí mismo el peso que les da.

Ocultar los rechazos sería más cómodo pero menos honesto. La filosofía del proyecto es mostrar toda la información disponible y dejar que el lector interprete.

---

## 7. El sistema de percentil: formato numérico directo

### Por qué percentil y no umbral fijo

Un umbral fijo ("necesitas 10 avales") es arbitrario, queda obsoleto con el crecimiento de la plataforma, y crea un objetivo concreto que los actores maliciosos pueden atacar coordinadamente. El percentil se actualiza continuamente, escala con la plataforma y no tiene un número fijo que manipular.

### Por qué formato numérico directo y no tier ni frase narrativa

El formato numérico directo es el más coherente con la filosofía de transparencia radical del proyecto. No colapsa la información en una etiqueta (como las letras de GitHub) ni la suaviza en lenguaje emocional (como Spotify). Muestra los tres elementos que hacen el dato completamente interpretable:

```
Número absoluto  +  Percentil relativo  +  Total del grupo
     23          +      Top 8%          +  de 47 especialistas en economía
     23          +      Top 21%         +  de 340 periodistas totales
```

**El número absoluto** ancla la realidad — 23 avales es 23 avales independientemente de cuántos periodistas haya.

**El percentil** da contexto relativo — top 8% entre especialistas en economía significa que hay 3-4 personas con más avales en esa especialidad.

**El total del grupo** permite al lector interpretar el percentil honestamente — top 8% entre 47 personas es muy diferente de top 8% entre 4.700.

### Problema conocido: inestabilidad del percentil

Cuando entran nuevos periodistas muy respaldados, el percentil de los existentes puede bajar aunque no hayan perdido ningún aval. Esto es matemáticamente correcto pero puede generar frustración.

Mitigación: mostrar siempre el número absoluto de avales junto al percentil. Si el número absoluto no ha cambiado, el lector entiende que el movimiento del percentil se debe al crecimiento de la plataforma, no a una pérdida de respaldo.

---

## 8. El proceso de solicitud paso a paso

### Paso 1 — Solicitud inicial
El periodista rellena el formulario de solicitud con:
- Nombre real y datos de contacto verificables
- Especialidades que quiere declarar
- Documentación del Grupo A y/o Grupo B
- Artículos propios que quiere vincular como evidencia de especialidad
- Clave pública criptográfica (necesaria para firmar votos — ver documento de arquitectura de trazabilidad)

### Paso 2 — Verificación de documentación (la plataforma)
La plataforma verifica únicamente que los documentos son reales:
- La titulación existe y pertenece a la persona
- Los artículos vinculados están firmados con su nombre real y son accesibles públicamente
- Los medios donde ha publicado tienen ISSN registrado o audiencia verificable

La plataforma **no juzga** la calidad del trabajo ni la orientación ideológica. Solo verifica autenticidad documental.

Plazo objetivo: 72 horas en MVP (manual). Automatizable parcialmente en fases posteriores.

### Paso 3 — Publicación del perfil en estado "Pendiente de comunidad"
Una vez verificada la documentación, el perfil se publica públicamente con estado visible:

```
Estado: DOCUMENTACIÓN VERIFICADA · Pendiente de aval de comunidad
Avales recibidos: 0 · Rechazos recibidos: 0
```

El periodista entra automáticamente como **Nivel 1** desde este momento y puede empezar a votar. Para subir a Nivel 2 necesita al menos 1 aval de un Nivel 2 o superior.

### Paso 4 — Aval de la comunidad (continuo)
Cualquier periodista Nivel 2 o superior puede avalar o rechazar al solicitante. El aval y el rechazo son siempre públicos e incluyen una nota opcional que el aval decide si hacer pública o privada para el solicitante.

El aval tiene coste reputacional para quien lo da — queda vinculado a su perfil permanentemente. Eso desincentiva avalar a desconocidos sin criterio.

### Paso 5 — Actualización automática de nivel
El sistema actualiza el nivel automáticamente cuando se cumplen los requisitos. No hay aprobación manual para subir de nivel — los criterios son públicos y el sistema los evalúa continuamente.

---

## 9. Vectores de fraude y mitigaciones

### Identidad falsa con historial fabricado
**El ataque:** alguien crea artículos publicados en una web propia sin audiencia real para cumplir el criterio del Grupo B.

**Mitigación:** los artículos vinculados deben estar publicados en medios con ISSN registrado o en plataformas con audiencia verificable externamente (número de suscriptores visible, métricas públicas). Una web personal sin ISSN y sin audiencia demostrable no cuenta. El perfil público muestra exactamente qué medios ha vinculado y cualquier lector puede verificarlo.

### Periodista real comprado
**El ataque:** un periodista legítimo entra honestamente y luego vende sus votos sistemáticamente a un partido o medio.

**Mitigación:** el IHP (Índice de Honestidad Profesional) lo detecta con el tiempo. Un periodista que solo valida el rigor de trabajos ideológicamente afines queda expuesto públicamente. No hay consecuencia automática — la consecuencia es reputacional y el lector la interpreta. En fases posteriores, la comunidad puede proponer la revisión del nivel de un periodista mediante un proceso formal de revisión entre pares.

### Aval coordinado entre grupos ideológicos
**El ataque:** un grupo de periodistas de la misma línea ideológica se avalan mutuamente de forma coordinada para inflar sus percentiles.

**Mitigación:** el percentil hace que avalarse mutuamente dentro del mismo grupo no suba el percentil general — solo sube el percentil dentro de ese grupo, que el lector puede ver segmentado. Además, el IHP penaliza reputacionalmente a quienes solo interactúan con su propio grupo ideológico. La transparencia de los avales (quién avaló a quién es siempre público) permite que cualquier lector detecte patrones de aval coordinado.

### Flood de solicitudes coordinado
**El ataque:** un actor malicioso envía cientos de solicitudes simultáneas para saturar el proceso de verificación manual y colar identidades falsas.

**Mitigación en MVP:** el proceso es manual y tiene capacidad limitada. Se puede establecer un límite de solicitudes procesadas por semana sin penalizar la calidad de revisión. A escala, la verificación documental básica es parcialmente automatizable (comprobación de ISSN, scraping de artículos firmados) reduciendo la carga manual.

---

## 10. Lo que la plataforma nunca hace

Estos límites son parte del diseño, no limitaciones técnicas. Violarlos comprometería la filosofía del proyecto:

- **No certifica que un periodista es bueno.** Solo verifica que su documentación es real y muestra el respaldo que ha recibido de la comunidad.
- **No elimina votos** por razones de calidad o ideología. Un voto emitido es permanente en el log público.
- **No decide quién tiene más autoridad** sobre un tema. Muestra la segmentación y el lector decide qué capa le importa más.
- **No oculta rechazos.** Un rechazo es información igual de válida que un aval.
- **No toma decisiones automáticas** sobre la reputación de un periodista basadas en su IHP. El IHP es un dato público, no un mecanismo de sanción automática.

---

## 11. Decisiones pendientes antes de implementar

- [ ] **Proceso de apelación:** si la plataforma rechaza la documentación de un periodista por considerarla no verificable, ¿puede apelar? ¿Ante quién? ¿Con qué proceso?
- [ ] **Bajas y suspensiones:** ¿puede un periodista ser expulsado de la plataforma? ¿Por qué causas? ¿Quién lo decide? ¿Con qué garantías? Actualmente el diseño no contempla expulsiones — solo degradación reputacional visible.
- [ ] **Portabilidad de datos:** si un periodista quiere abandonar la plataforma, ¿puede exportar su historial de votos y avales? ¿En qué formato? Sus votos en el log público permanecen en cualquier caso — son parte del registro inmutable.
- [ ] **Periodistas fallecidos:** ¿qué ocurre con el perfil y el historial de un periodista fallecido? ¿Se marca como inactivo? ¿Sus votos mantienen el mismo peso visual?
- [ ] **Verificación automatizada a escala:** en MVP la verificación documental es manual. A partir de qué volumen de solicitudes tiene sentido automatizar parcialmente y qué partes son automatizables sin comprometer la fiabilidad.

---

## 12. Relación con otros módulos del proyecto

| Módulo | Dependencia |
|---|---|
| Arquitectura de trazabilidad | La clave pública del periodista (sección 5.2 del documento de trazabilidad) se genera en el onboarding de verificación |
| Sistema de votos | El nivel del periodista determina en qué capa visual aparece su voto |
| Visualización de artículos | El perfil del periodista se enlaza desde cada voto que emite |
| IHP (Índice de Honestidad Profesional) | Se calcula a partir del historial de votos — documentado en el módulo de sistema de votos |

---

## 13. GDPR aplicado al perfil del periodista

> ⚠️ **Decisión con implicaciones legales directas. El perfil público del periodista contiene datos personales reales. Requiere análisis legal antes de publicar el primer perfil.**

### La tensión estructural

El perfil del periodista es público por diseño — nombre real, historial profesional, documentación verificada, historial de votos. Eso es exactamente lo que garantiza la transparencia radical del proyecto. Pero bajo el GDPR (Reglamento General de Protección de Datos), todo eso son datos personales y el periodista tiene derechos sobre ellos, incluyendo el derecho al olvido (Art. 17).

El problema: si un periodista ejerce el derecho al olvido y exige que se borre su perfil, sus votos ya están registrados en el log público de GitHub y anclados en Bitcoin y Polygon. Su nombre está vinculado a esos votos en el archivo `votos.jsonl`. No se puede borrar retroactivamente sin comprometer la integridad criptográfica del log — que es la garantía central de toda la plataforma.

### La solución estándar aplicada a este contexto

La misma solución documentada en el módulo de trazabilidad para votos ciudadanos aplica aquí con matices:

**Los datos personales nunca van directamente al log inmutable.** En el log público solo aparece el identificador criptográfico del periodista (su clave pública o un hash de su identidad), no su nombre real ni sus datos personales. La vinculación entre ese identificador y la identidad real vive únicamente en PostgreSQL.

Si el periodista ejerce el derecho al olvido:
- Se borra su registro en PostgreSQL — nombre, documentación, datos de contacto
- Su perfil público desaparece o se anonimiza
- El log inmutable mantiene sus votos vinculados a su identificador criptográfico, que queda huérfano — matemáticamente presente pero no vinculable a ninguna persona identificable

Esto es legalmente aceptado en la mayoría de interpretaciones del GDPR aplicadas a sistemas blockchain, pero requiere confirmación legal antes de implementar.

### Casos adicionales a resolver

- **Base legal para publicar el perfil:** el periodista debe dar consentimiento explícito e informado para que su nombre real y documentación sean públicos. Ese consentimiento debe documentarse y ser revocable.
- **Datos de terceros en los artículos vinculados:** los artículos que el periodista vincula pueden contener datos de terceros. La plataforma no aloja ese contenido, solo enlaza — pero conviene documentar que la responsabilidad sobre el contenido enlazado es del medio que lo publica, no de la plataforma.
- **Transferencias internacionales:** si el servidor está fuera de la UE, aplican restricciones adicionales de transferencia de datos personales.

**Pendiente:** consulta legal especializada en GDPR y blockchain antes del lanzamiento. No es opcional.

---

## 14. Periodistas de medios tradicionales con línea editorial

> ⚠️ **Riesgo estructural conocido. No hay solución técnica completa — requiere decisión de diseño sobre cómo tratar este segmento.**

### El problema

Un periodista de un medio tradicional con línea editorial documentada (El País, La Razón, El Mundo, etc.) puede cumplir todos los criterios de verificación perfectamente y entrar en la plataforma de forma legítima. Pero su director puede presionarle para que vote en una dirección concreta — o simplemente puede tener interiorizada la línea editorial de su medio hasta el punto de que sus votos reflejen esa línea más que su criterio técnico independiente.

Esto no es un ataque malicioso detectable — es una presión estructural del sistema mediático actual que el proyecto no puede eliminar, solo hacer visible.

### Por qué es diferente al periodista independiente

Un periodista independiente que vota sistemáticamente en una dirección queda expuesto por su IHP — su patrón de votos es la única referencia disponible. Un periodista de medio tradicional tiene una explicación estructural para ese patrón: la línea editorial de su empleador. El lector no puede saber si vota así por criterio propio o por presión.

### Mitigaciones a explorar

**Segmentación visual explícita por tipo de periodista:**
Mostrar en la visualización de votos si el periodista trabaja en un medio con línea editorial documentada, igual que se muestra su especialidad. No es un juicio — es información contextual que el lector puede usar para interpretar el voto.

```
[✓ Rigor] Juan García · Economía · El País (línea editorial: centro-izquierda)
[✓ Rigor] María López · Economía · Independiente
```

Esto no penaliza al periodista de medio tradicional — simplemente da al lector el contexto necesario para interpretar su voto con la misma información que tiene para interpretar cualquier otro dato de la plataforma.

**Voto de rigor anónimo opcional para periodistas de medios con línea editorial:**
Un periodista que trabaja en un medio con línea editorial documentada podría tener la opción de emitir el voto de rigor de forma anónima — su identidad computa en el percentil pero no aparece públicamente vinculada al voto. El voto de afinidad siempre sería público.

Esto protege al periodista de represalias laborales sin eliminar su contribución al índice de rigor. Técnicamente implementable con Zero-Knowledge Proofs (documentado en el módulo de trazabilidad, sección 14).

**Problema no resuelto:** ¿quién decide qué medios tienen "línea editorial documentada" y con qué criterio? Esa lista es en sí misma una decisión política. Cualquier lista que elabore la plataforma será cuestionada por los medios que aparezcan en ella.

**Pendiente:** decidir si este segmento se trata de forma diferenciada en el MVP o se pospone a fases posteriores cuando la plataforma tenga masa crítica suficiente para absorber la controversia.

---

## 15. Cambio de especialidad declarada

> ⚠️ **Afecta a la integridad del historial y al cálculo del percentil. Requiere política explícita antes de implementar el sistema de especialidades.**

### El problema

Un periodista que empezó cubriendo deportes y lleva tres años haciendo periodismo de investigación económica querrá actualizar su especialidad declarada. El sistema debe permitirlo — sería absurdo que la especialidad declarada al registrarse fuera inmutable de por vida. Pero el cambio tiene consecuencias sobre el historial que hay que gestionar explícitamente.

### Las preguntas sin respuesta en el documento actual

**¿Los votos anteriores se reclasifican?**
Si el periodista tenía especialidad "Deportes" y la cambia a "Economía", sus 200 votos anteriores emitidos como especialista en deportes, ¿pasan a computar en el percentil de economía? Eso sería deshonesto — no tenía ese expertise cuando los emitió.

**¿Cómo afecta al percentil de especialidad?**
Si los votos anteriores no se reclasifican, el periodista empieza con percentil 0 en su nueva especialidad aunque tenga años de experiencia y muchos avales generales. Eso puede desincentivarlo a actualizar su perfil honestamente.

### Política propuesta para revisión

**Los votos mantienen la especialidad del momento en que fueron emitidos.** El log registra la especialidad activa del periodista en el timestamp del voto. Si cambia de especialidad, los votos futuros computan en la nueva especialidad. Los votos pasados mantienen su clasificación original — esto es lo más honesto y lo más coherente con la inmutabilidad del log.

**El cambio de especialidad es público y trazable.** El perfil muestra el historial de especialidades declaradas con fechas:

```
Especialidades:
  · Periodismo económico     [desde 2025-03-01]  [34 artículos vinculados →]
  · Periodismo deportivo     [2023-01-01 / 2025-02-28]  [12 artículos vinculados →]
```

El lector puede ver cuándo cambió y por qué — si vinculó nuevos artículos que justifican el cambio o si simplemente actualizó la etiqueta sin evidencia nueva.

**El cambio requiere nueva documentación vinculada.** No se puede cambiar de especialidad sin aportar al menos un mínimo de artículos vinculados en la nueva área. Evita cambios oportunistas sin base real.

**Pendiente:** definir el mínimo de artículos requeridos para declarar una nueva especialidad y si ese mínimo es el mismo que para la especialidad inicial o diferente.

---

## 16. El problema del arranque — los primeros verificadores

> ⚠️ **Problema de diseño que afecta directamente a la credibilidad del proyecto desde el día uno. Si no se documenta y comunica públicamente, la decisión inicial de quién tiene Nivel 2 queda como una decisión opaca del creador — exactamente lo que el proyecto intenta evitar.**

### El círculo vicioso del arranque

Para subir a Nivel 2 necesitas el aval de alguien que ya esté en Nivel 2. Los primeros periodistas que entren estarán todos en Nivel 1. Nadie puede avalar a nadie para subir de nivel. El sistema de avales está bloqueado desde el inicio.

Este es el problema clásico de los sistemas de confianza distribuida: alguien tiene que ser el primero, y ese primero no puede haber sido validado por el sistema que está arrancando.

### La solución honesta: el Grupo Fundador con proceso público

La única forma honesta de resolver esto es nombrar explícitamente un **Grupo Fundador** con Nivel 2 desde el día uno, documentar públicamente quiénes son y por qué fueron seleccionados, y hacer ese proceso visible antes del lanzamiento.

**Criterios de selección del Grupo Fundador:**
- Periodistas de investigación independiente con historial público verificable amplio
- Diversidad ideológica documentable — el grupo fundador no puede ser homogéneo ideológicamente sin comprometer la credibilidad del sistema desde el origen
- Diversidad geográfica si el proyecto aspira a ser internacional desde el inicio
- Sin conflicto de interés con el creador del proyecto — no pueden ser amigos personales sin historial profesional independiente

**Tamaño recomendado para MVP:** entre 5 y 15 periodistas. Suficiente para que el sistema de avales funcione desde el día uno. Pequeño enough para que el proceso de selección sea manejable y auditable.

**El proceso de selección debe ser público antes del lanzamiento:**
Publicar en el repositorio GitHub del proyecto, antes de abrir el registro, quiénes forman el Grupo Fundador, qué criterios se usaron para seleccionarlos y por qué cada uno cumple esos criterios. Cualquier persona puede leerlo y cuestionarlo antes de que el sistema arranque.

Esto no elimina el hecho de que el creador del proyecto tomó esa decisión inicial — es inevitable. Pero la transparencia del proceso convierte una decisión potencialmente opaca en una decisión auditable públicamente. La diferencia entre los dos es la misma que entre un árbitro que explica sus criterios y uno que no los explica.

**Pendiente:**
- [ ] Definir los criterios exactos de selección del Grupo Fundador antes del lanzamiento
- [ ] Identificar candidatos que cumplan esos criterios y contactarles
- [ ] Publicar el proceso de selección en el repositorio antes de abrir el registro
- [ ] Decidir si el creador del proyecto tiene Nivel 2 o se mantiene fuera del sistema de votos para evitar conflicto de interés

---

*Documento de diseño del sistema de verificación · Parte del conjunto de documentos de diseño del proyecto*
