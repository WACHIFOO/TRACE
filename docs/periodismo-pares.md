# Plataforma de Periodismo de Revisión por Pares
**Estado:** Conceptualización · **Versión:** 0.1 · **Naturaleza:** Open Source

---

## 1. El problema que resuelve

El periodismo actual tiene un defecto de diseño estructural: **mezcla en el mismo contenedor la calidad del trabajo y la orientación ideológica**. El lector no tiene herramientas para separar ambas dimensiones y acaba usando la segunda (ideología) como proxy de la primera (calidad), lo que alimenta la polarización y permite que el periodismo de baja calidad prospere si dice lo que el lector quiere oír.

Las soluciones actuales fallan porque:
- Los **fact-checkers** son percibidos como árbitros sesgados (y a menudo lo son).
- Los **medios de referencia** tienen conflictos de interés con anunciantes y partidos.
- Las **redes sociales** amplifican el ruido y penalizan el rigor aburrido.
- Las **plataformas de nicho** (Substack, etc.) no tienen mecanismo de validación entre pares.

---

## 2. La idea central

Una plataforma donde cada pieza periodística recibe **dos valoraciones independientes y públicas**:

| Dimensión | Pregunta | Quién vota |
|---|---|---|
| **Rigor técnico** | ¿Está bien hecho? (fuentes, contraste, separación hecho/opinión) | Periodistas verificados |
| **Afinidad editorial** | ¿Estás de acuerdo con la tesis? | Periodistas verificados |
| **Impacto ciudadano** | ¿Lo consideras útil y fidedigno? | Usuarios registrados |

### El mecanismo clave: el voto público trazable

Un periodista puede votar:
```
[Rigor: ✓ SÍ] + [Acuerdo: ✗ NO]
```
Esto significa: *"No comparto la tesis, pero el trabajo está impecablemente hecho."*

**Por qué esto cambia los incentivos:** Si un periodista de derechas vota `[Rigor: NO]` a una investigación impecable de izquierdas, su voto queda expuesto. Su comunidad ve que ha votado con el estómago. Eso destruye su reputación técnica. El sistema crea presión de pares hacia la honestidad.

---

## 3. Checklist de calidad (el estándar base)

El artículo debe cumplir estos criterios para ser evaluable en la plataforma:

- [ ] Fuentes directas enlazadas o adjuntas (documentos, datos, grabaciones)
- [ ] Firma real del autor con historial verificable
- [ ] Etiquetado explícito del tipo de contenido: Noticia / Análisis / Opinión
- [ ] Derecho a réplica incluido o documentado intento de obtenerlo
- [ ] Separación visible entre hechos y valoraciones del autor

> **Advertencia de diseño:** Este checklist filtra el ruido obvio, pero no la manipulación sofisticada. Un artículo puede cumplir 5/5 formalmente y aun así sacar datos de contexto de forma maliciosa. El ojo humano de los revisores es la última línea de defensa.

---

## 4. Arquitectura del sistema de reputación

### Para periodistas verificados
- Historial público de todos sus votos de rigor y afinidad.
- **Índice de Honestidad Profesional:** ratio de veces que validan rigor en artículos con los que discrepan ideológicamente. Un periodista con IHP alto es valioso. Un periodista que solo valida a los suyos queda expuesto.
- Verificación de identidad profesional (carné de prensa, publicaciones anteriores, firma digital).

### Para usuarios registrados
- Voto de impacto ciudadano aislado estadísticamente del voto profesional.
- Requiere fricción anti-bot: verificación por teléfono físico o micropago simbólico (1€ de depósito reembolsable).
- Su nota aparece en la interfaz como métrica separada, nunca mezclada con la profesional.

### Visualización (UI objetivo)
```
┌─────────────────────────────────────┐
│  RIGOR TÉCNICO        ████████░░ 8/10│  ← Periodistas verificados
│  DIVERSIDAD EDITORIAL ██████░░░░ 6/10│  ← % de revisores de distinta ideología
│  IMPACTO CIUDADANO    ███████░░░ 7/10│  ← Usuarios registrados
└─────────────────────────────────────┘
  Revisado por 12 periodistas · 847 usuarios
  [Ver quién ha votado y cómo →]
```

---

## 5. Los tres ataques que el sistema debe resistir

### 5.1 Presión de línea editorial (riesgo alto)
**El ataque:** El director de un medio llama a su periodista: *"Cambia ese voto o estás despedido."*

**Mitigaciones a explorar:**
- **Zero-Knowledge Proofs:** Un periodista puede demostrar criptográficamente que es profesional verificado sin revelar su identidad pública. Vota anónimamente pero su voto computa en la nota global. Coste: complejidad técnica alta.
- **Umbral de anonimato:** Si el periodista trabaja en medios con línea editorial documentada, su voto de rigor puede ser anónimo pero el de afinidad siempre público. Más pragmático.
- **Conclusión provisional:** Empezar solo con periodistas independientes (sin jefes). Los de grandes medios son un caso de uso de fase 2.

### 5.2 Granjas de bots (riesgo alto en escala)
**El ataque:** Un partido coordina miles de cuentas para hundir el impacto ciudadano de noticias que le perjudican.

**Mitigaciones a explorar:**
- Cortafuegos estricto entre nota ciudadana y nota profesional (son métricas separadas, nunca una sola puntuación).
- Detección de patrones de votación coordinada (picos anómalos en tiempo, IPs, comportamiento).
- La nota ciudadana lleva siempre una advertencia visual si hay anomalías estadísticas detectadas.

### 5.3 Rigor formal de la mentira (riesgo permanente)
**El ataque:** Un artículo cumple el checklist 5/5 pero saca datos de contexto malintencionadamente.

**Mitigaciones a explorar:**
- **Anotaciones de contexto:** Los revisores verificados pueden adjuntar notas directamente sobre párrafos específicos, visibles al lector junto al artículo.
- **Historial de correcciones:** Si el autor corrige el artículo, queda registrado en la plataforma con fecha y motivo.

---

## 6. Decisiones de diseño abiertas (las tienes que tomar tú)

Estas son las preguntas sin respuesta correcta. Cada elección tiene consecuencias en toda la arquitectura:

**¿Quién puede ser "periodista verificado"?**
- Solo con carné de prensa oficial → excluye periodistas independientes excelentes
- Con historial de publicaciones verificables → más inclusivo, más difícil de auditar
- Con aval de otros periodistas ya verificados → modelo de invitaciones, crece lento pero fiable

**¿Cómo gestionas el sesgo geográfico/cultural?**
- Una noticia sobre política española revisada por periodistas latinoamericanos tiene contexto diferente.
- ¿Segmentas los revisores por mercado? ¿O la diversidad geográfica es una ventaja?

**¿Qué ocurre si un artículo recibe muy pocos votos de revisores?**
- ¿Se muestra igualmente con un aviso de "revisión insuficiente"?
- ¿Se bloquea hasta alcanzar un mínimo de revisores?

**¿La plataforma aloja el contenido o solo lo evalúa?**
- Alojar contenido → más control, más responsabilidad legal, más coste
- Solo evaluar (links externos) → el periodista mantiene su canal propio, más fácil de lanzar

---

## 7. Stack técnico sugerido (para un desarrollador en solitario)

Orientado a MVP rápido, open source desde el día 1, con capacidad de crecer.

### Backend
- **Lenguaje:** Python (FastAPI) o TypeScript (Node + Express/Hono)
- **Base de datos:** PostgreSQL — los votos, reputaciones e historiales son datos relacionales con integridad crítica
- **Autenticación:** OAuth2 + JWT; para periodistas, flujo de verificación manual en MVP
- **Almacenamiento de votos:** Append-only log (nunca se borran votos, solo se añaden correcciones) — crítico para la trazabilidad

### Frontend
- **Framework:** Next.js (React) — SSR importante para que los artículos sean indexables por buscadores
- **UI:** Tailwind + componentes propios (evitar librerías de componentes genéricos para que la identidad visual sea distintiva)

### Infraestructura
- **Hosting inicial:** Railway, Render o Fly.io — bajo coste, fácil de gestionar en solitario
- **Open source:** GitHub desde el día 1, licencia AGPL (obliga a que cualquier fork también sea open source, protege el proyecto de que una empresa lo privatice)

### Lo que NO construir en el MVP
- App móvil nativa (web responsiva es suficiente al inicio)
- Zero-Knowledge Proofs (complejo, para fase 2)
- Sistema de recomendación algorítmico (empieza con cronológico + filtros manuales)

---

## 8. MVP: qué construir primero

El MVP no es una plataforma de noticias. Es una **herramienta de revisión** para un grupo cerrado de 30-50 periodistas independientes de investigación.

### Funcionalidades del MVP (en orden de prioridad)

1. **Registro y verificación de periodistas** — formulario manual revisado por ti al inicio
2. **Publicación de artículos** — enlace externo + resumen + metadatos + etiqueta de tipo
3. **Checklist de calidad** — formulario que el autor completa al publicar
4. **Sistema de doble voto** — rigor (sí/no) + afinidad (sí/no), público y trazable
5. **Perfil del periodista** — historial de votos, IHP básico
6. **Vista del artículo** — visualización de las tres métricas separadas
7. **Feed público** — lista de artículos con sus métricas, filtrable

### Lo que NO está en el MVP
- Voto ciudadano (añadirlo después de validar el modelo profesional)
- Anotaciones de contexto en párrafos
- Algoritmo de recomendación
- Monetización

---

## 9. Modelo de sostenibilidad económica

La publicidad institucional es incompatible con la independencia de la plataforma. Opciones a explorar:

| Modelo | Ventajas | Riesgos |
|---|---|---|
| **Mecenazgo colectivo** (modelo Wikipedia) | Sin conflictos de interés, culturalmente alineado | Ingresos impredecibles, fatiga de donaciones |
| **Suscripción premium** (acceso a analíticas avanzadas, exportar datos) | Recurrente, predecible | Los mejores usuarios quieren todo gratis |
| **Subvenciones internacionales** (fundaciones de libertad de prensa: Knight Foundation, NED, Open Society) | Capital inicial sin deuda | Burocracia, plazos largos, posible percepción de sesgo |
| **API de datos** (medios o investigadores pagan por acceder a los datos de reputación) | Escalable | Requiere escala previa |

**Recomendación para fase 1:** Subvenciones + mecenazgo. La plataforma no debería necesitar monetizar hasta tener producto validado.

---

## 10. Referentes a estudiar

| Proyecto | Qué tiene de útil | Dónde falló o qué le falta |
|---|---|---|
| **The Trust Project** | Indicadores de confianza estandarizados | No tiene mecanismo de revisión entre pares, es autodeclarado |
| **WikiTribune / WT.Social** | Revisión comunitaria de noticias | Masa crítica insuficiente, comunidad poco especializada |
| **ICIJ (Papeles de Panamá)** | Periodistas ideológicamente opuestos revisándose entre sí | Cerrado, no es una plataforma pública |
| **GitHub Pull Requests** | Revisión pública de código con historial trazable | El modelo de gobernanza que hay que trasladar al periodismo |
| **arXiv + peer review** | Separación entre preprint y revisión formal | El rigor científico es más objetivable que el periodístico |

---

## 11. Riesgos existenciales del proyecto

Cosas que podrían matar el proyecto antes de que despegue:

- **Masa crítica:** Sin suficientes periodistas verificados activos, la plataforma no tiene valor. El problema del huevo y la gallina.
- **Captura ideológica:** Si los primeros 50 periodistas que se unen son todos de un mismo espectro, la plataforma nace sesgada y es muy difícil de revertir.
- **Desgaste del revisor:** Revisar artículos de otros periodistas es trabajo no remunerado. Sin incentivos claros (reputación, visibilidad), la actividad de revisión decae.
- **Presión legal:** Un periodista cuyo artículo recibe baja nota de rigor podría demandar a la plataforma. Necesitas asesoramiento legal desde el inicio sobre responsabilidad de las valoraciones.
- **Que alguien lo construya antes:** La idea no está patentada ni puede estarlo. La ventaja competitiva es la comunidad, no el código.

---

## 12. Próximos pasos concretos (cuando decidas avanzar)

- [ ] Definir el criterio exacto de verificación de periodistas (la decisión más importante del diseño)
- [ ] Identificar 10 periodistas independientes de investigación que podrían ser beta testers interesados
- [ ] Elegir si la plataforma aloja contenido o solo lo evalúa (define toda la arquitectura legal y técnica)
- [ ] Montar un prototipo de la interfaz de doble voto (puede ser un Figma o incluso un formulario de Google Forms con hoja de cálculo pública)
- [ ] Redactar la licencia AGPL y crear el repositorio público en GitHub
- [ ] Buscar asesoramiento legal sobre responsabilidad de las valoraciones (un abogado de medios, aunque sea una consulta inicial)

---

*Documento generado a partir de sesión de conceptualización. Versión de referencia para desarrollo posterior.*
