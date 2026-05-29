# Visión a Largo Plazo y Filosofía del Proyecto
**Estado:** Borrador · Revisión pendiente · **Versión:** 0.1

> ⚠️ Este documento recoge ideas y decisiones filosóficas del creador del proyecto en fase de conceptualización. Está marcado para revisión antes de publicarlo como documento oficial del repositorio. El contenido es correcto pero puede necesitar refinamiento en la forma antes de ser la cara pública del proyecto.

---

## 1. Esto es un protocolo, no una aplicación

El proyecto no es una plataforma de periodismo. Es una **infraestructura genérica de validación por pares con trazabilidad criptográfica** cuyo primer caso de uso es el periodismo.

La distinción es fundamental. Una aplicación resuelve un problema concreto para un usuario concreto. Un protocolo establece las reglas del juego y deja que otros construyan sobre él. HTTP no decide qué webs existen. Git no decide qué código se escribe. Este proyecto no decide qué comunidades lo usan ni cómo lo adaptan.

El creador aporta el **70% de la estructura** — el core técnico, la arquitectura de trazabilidad, el sistema de votos, el modelo de verificación por pares, la filosofía de transparencia radical. El **30% restante** — la adaptación a cada dominio, el checklist específico, la taxonomía de especialidades, los criterios de verificación propios — lo completa cada comunidad que adopte el sistema. Si nadie lo adopta, el proyecto sigue siendo válido como infraestructura disponible. No es responsabilidad del creador que otros la usen.

---

## 2. Dominios donde el sistema es aplicable

El periodismo es el primer caso de uso porque el problema es visible, urgente y comprensible para el público general. Pero la arquitectura es agnóstica al dominio. Cualquier campo donde exista:

- Contenido público que requiere evaluación de calidad técnica
- Una comunidad de expertos verificables con criterio para evaluarlo
- Necesidad de separar el rigor metodológico de la afinidad ideológica o de intereses
- Valor en la trazabilidad pública de quién dijo qué sobre qué

...puede desplegar su propia instancia del sistema.

Casos de uso con alto potencial identificados:

**Medicina clínica y divulgación médica** — separar el rigor metodológico de un estudio de sus implicaciones clínicas controvertidas. Los médicos en ejercicio no tienen herramientas para evaluar públicamente si un paper está bien diseñado o está financiado con sesgo.

**Divulgación científica** — evaluar si los artículos de divulgación representan honestamente los papers que citan. Un científico del área puede detectar distorsiones que el público general no puede.

**Informes de think tanks y política pública** — dar visibilidad al rigor metodológico de informes con apariencia académica pero agenda ideológica, evaluados por economistas o politólogos independientemente de si comparten las conclusiones.

**Cualquier otro dominio** donde una comunidad de expertos quiera construir una capa de validación pública sobre contenido existente.

---

## 3. Governance by fork — el modelo de gobernanza

El core del proyecto no tiene proceso de votación comunitaria. No hay comité. No hay RFC obligatorio. No hay negociación sobre los principios fundamentales.

El creador define y mantiene el core. Lo documenta con transparencia total. Si alguien discrepa con una decisión del core, tiene el código y puede hacer lo que quiera con él. Eso es la licencia AGPL funcionando exactamente como fue diseñada.

**La fragmentación no es un defecto del sistema — es el mecanismo de adaptación.**

Es el mismo modelo que ha hecho funcionar Linux, Mastodon, WordPress y Git durante décadas. Nadie le pide permiso a Linus Torvalds para hacer una distribución de Linux. Nadie le pide permiso al creador de este proyecto para hacer una instancia de validación médica con su propio checklist y sus propios criterios de verificación.

Lo que sí es responsabilidad del creador: que el core sea lo suficientemente genérico para no necesitar tocarse en la mayoría de casos de uso. Un checklist base con criterios abstractos — fuentes verificables, autoría real, etiquetado honesto del tipo de contenido, separación hecho/valoración — funciona igual en periodismo que en medicina que en divulgación científica sin modificación.

---

## 4. La herramienta, no el policía

El sistema trata al lector y al periodista como personas adultas y funcionales. No es un padre. No es un árbitro. No es una autoridad.

Da información. El lector decide qué hacer con ella.

Las consecuencias del mal uso del sistema — aprender el checklist para cumplirlo formalmente sin cumplirlo en fondo — las gestiona la propia comunidad, no el sistema. Si un actor sofisticado aprende a manipular el checklist, la comunidad detecta el patrón y propone criterios adicionales en su instancia. Si no lo detecta o no le importa, es su problema. El sistema ha cumplido su función: ha dado transparencia sobre lo que evalúa. Lo que no evalúa es visible por omisión.

Un periodista que ha firmado algo bajo presión puede denunciarlo en la misma plataforma con su propio voto marcado como AUTOR. No necesita que el sistema lo proteja — el sistema le da el canal. Lo que haga con él es su decisión.

Si la plataforma no se usa, es problema de quien no la usa. El creador da la herramienta. La responsabilidad del uso es de cada persona.

---

## 5. Expectativas calibradas

El escenario más probable estadísticamente para cualquier proyecto open source en solitario sin financiación es una adopción de nicho reducida y sostenida, no un impacto masivo inmediato.

Eso no es un fracaso. Es el funcionamiento normal de infraestructura técnica. TCP/IP no tuvo millones de usuarios el primer año. Git tardó años en convertirse en el estándar.

El criterio de éxito correcto para este proyecto no es el número de usuarios. Es si la infraestructura es lo suficientemente sólida, documentada y abierta para que cualquier comunidad que quiera usarla pueda hacerlo sin depender del creador para nada más allá del core.

Si en el peor caso el proyecto tiene 20 usuarios activos y el código está en GitHub disponible para quien quiera usarlo, el proyecto ha cumplido su objetivo. La semilla está plantada. Lo que crezca de ella no depende del creador.

---

## 6. Lo que queda por definir en este documento

> Estos puntos están identificados pero no resueltos. Revisitar antes de publicar como documento oficial.

- [ ] **Qué es exactamente el core vs. qué es configurable por instancia.** Hay que hacer una lista explícita de qué puede modificar una instancia sin hacer un fork y qué requiere fork. Eso define los límites reales del protocolo.

- [ ] **Cómo se hace un fork correctamente.** Un documento técnico breve — cómo clonar, qué configurar, qué mantener del core, cómo contribuir mejoras de vuelta al upstream si se quiere. Reduce la fricción de adopción.

- [ ] **Qué garantiza la licencia AGPL a quien lo use.** Explicado en lenguaje no legal para que cualquier comunidad entienda sus derechos antes de adoptar el sistema.

- [ ] **La relación entre instancias.** ¿Las instancias están completamente aisladas o hay algún mecanismo de federación? Un periodista verificado en la instancia española, ¿puede votar en la instancia latinoamericana? ¿O cada instancia es un universo independiente? Esto no está decidido y tiene implicaciones técnicas y de diseño importantes.

---

*Documento de visión · Parte del conjunto de documentos de diseño del proyecto · Marcar como revisado antes de publicar en el repositorio*
