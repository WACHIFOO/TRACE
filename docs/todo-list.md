# Todo List — Pendientes del Proyecto
**Documento vivo** · Se actualiza conforme se cierran puntos · **Versión:** 0.1

> Recoge todo lo que falta por analizar, decidir o documentar antes de empezar a construir. Separado en tres categorías: bloqueante (no se puede implementar sin esto), importante (necesario antes del lanzamiento) y fase 2 (puede esperar al MVP validado).

---

## 🔴 BLOQUEANTE — Necesario antes de escribir código

---

### TODO-001 · Consulta legal — responsabilidad de las valoraciones
**Resumen:** Un periodista cuyo artículo recibe valoración negativa pública podría demandar a la plataforma. En España y la UE hay jurisprudencia específica sobre plataformas de valoración. Necesita análisis de un abogado especializado en medios o tecnología antes del lanzamiento. Sin esto no se puede abrir la plataforma al público.

**Afecta a:** modelo de contenido, envío de artículos por terceros, checklist público.

**Documentos relacionados:** `periodismo-pares.md` sección 11, `sistema-votos-visualizacion.md` sección 5.

---

### TODO-002 · Consulta legal — GDPR y perfil público del periodista
**Resumen:** El perfil público del periodista contiene nombre real y documentación verificada. Hay tensión directa entre el derecho al olvido (GDPR Art. 17) y la inmutabilidad del log criptográfico. La solución técnica está diseñada (solo el hash va al log, el nombre real solo en PostgreSQL) pero necesita validación legal antes de publicar el primer perfil.

**Afecta a:** arquitectura de trazabilidad, verificación de periodistas.

**Documentos relacionados:** `verificacion-periodistas.md` sección 13, `arquitectura-trazabilidad.md` sección 16.

---

### TODO-003 · Selección del Grupo Fundador
**Resumen:** Los primeros periodistas necesitan entrar con Nivel 2 para que el sistema de avales funcione desde el día uno. Alguien tiene que ser el primero. Ese proceso de selección inicial debe ser público, documentado y con criterios de diversidad ideológica explícitos antes del lanzamiento — si no, la decisión más importante del proyecto queda como decisión opaca del creador.

**Afecta a:** verificación de periodistas, credibilidad del arranque.

**Tareas concretas:**
- [ ] Definir criterios exactos de selección (diversidad ideológica, geográfica, especialidad)
- [ ] Identificar 5-15 candidatos que cumplan esos criterios
- [ ] Contactarles y confirmar participación
- [ ] Publicar el proceso de selección en el repositorio antes de abrir el registro
- [ ] Decidir si el creador del proyecto tiene Nivel 2 o se mantiene fuera del sistema de votos

**Documentos relacionados:** `verificacion-periodistas.md` sección 16.

---

### TODO-004 · Decisión — ¿La plataforma aloja contenido o solo links?
**Resumen:** ✅ Cerrado para MVP (solo links externos). Pendiente para Fase 2: decidir si migrar a modelo híbrido (snapshot archivado del contenido) cuando el modelo esté validado. Requiere consulta legal adicional sobre derechos de archivo de contenido de terceros.

**Estado:** MVP cerrado. Fase 2 pendiente de análisis.

**Documentos relacionados:** `decisiones-cerradas.md` DC-001.

---

## 🟡 IMPORTANTE — Necesario antes del lanzamiento público

---

### TODO-005 · Gobernanza del proyecto
**Resumen:** Nadie ha definido quién toma decisiones sobre el proyecto una vez que hay comunidad. ¿Quién puede modificar el checklist de calidad? ¿Quién decide cambios en los criterios de verificación? ¿Cómo se gestionan propuestas de cambio de la comunidad? Un proyecto open source sin gobernanza definida acaba siendo gobernado por quien más tiempo tiene o más ruido hace. Necesita un documento propio.

**Temas a cubrir:**
- Modelo de gobernanza (¿RFC público como en Rust? ¿Votación de la comunidad? ¿Decisión del creador con consulta pública?)
- Proceso de cambio del checklist de calidad
- Proceso de cambio de criterios de verificación de periodistas
- Gestión de conflictos dentro de la comunidad
- Qué ocurre si el creador del proyecto abandona el proyecto

---

### TODO-006 · Responsabilidad legal — envío de artículos por terceros (Fase 2)
**Resumen:** En Fase 2 cualquier periodista Nivel 2+ podrá proponer artículos de otros para revisión — tanto para alabar un buen trabajo como para denunciar uno malo. El modelo propuesto (autor notificado, 72h para confirmar o rechazar) mitiga el riesgo pero no lo elimina. Consulta legal obligatoria antes de implementar esta funcionalidad.

**Documentos relacionados:** `sistema-votos-visualizacion.md` sección 5.

---

### TODO-007 · Sesgo geográfico y cultural
**Resumen:** Una noticia sobre política española revisada por periodistas latinoamericanos tiene un contexto diferente al de periodistas españoles, y viceversa. Hay que decidir si la plataforma segmenta geográficamente los votos en la visualización, si la diversidad geográfica de revisores se muestra como métrica, o si se asume que la diversidad geográfica es una ventaja sin tratamiento especial. Afecta al diseño de la visualización y al perfil del periodista.

**Preguntas a responder:**
- ¿Se muestra el país del revisor junto a su voto?
- ¿Hay un percentil geográfico además del de especialidad?
- ¿Se permite filtrar votos por región geográfica?

---

### TODO-008 · Proceso de apelación por verificación rechazada
**Resumen:** Si la plataforma rechaza la documentación de un periodista por considerarla no verificable, ¿puede apelar? ¿Ante quién? ¿Con qué proceso y plazos? Actualmente no está definido. Sin proceso de apelación, el rechazo es una decisión unilateral sin recurso — contradice la filosofía del proyecto.

**Documentos relacionados:** `verificacion-periodistas.md` sección 11.

---

### TODO-009 · Política de bajas y suspensiones
**Resumen:** ¿Puede un periodista ser expulsado de la plataforma? ¿Por qué causas? ¿Quién lo decide y con qué garantías? El diseño actual no contempla expulsiones — solo degradación reputacional visible. Pero hay casos extremos (fraude de identidad demostrado, comportamiento coordinado malicioso) donde puede ser necesario. Necesita política explícita antes del lanzamiento.

**Documentos relacionados:** `verificacion-periodistas.md` sección 11.

---

### TODO-010 · Política de cambio de especialidad
**Resumen:** Está diseñada la política base (votos mantienen la especialidad del momento en que se emitieron, el cambio requiere nueva documentación) pero falta definir el mínimo de artículos requeridos para declarar una nueva especialidad y si es igual o diferente al mínimo inicial.

**Documentos relacionados:** `verificacion-periodistas.md` sección 15.

---

### TODO-011 · Votación de artículos históricos
**Resumen:** ¿Puede un periodista votar un artículo publicado hace años? Sin límite temporal, los artículos pueden recibir campañas de votos coordinadas mucho después de su publicación, fuera del contexto en que se escribieron. Hay que definir si hay fecha de caducidad para recibir nuevos votos y cuál es.

**Documentos relacionados:** `sistema-votos-visualizacion.md` sección 11.

---

### TODO-012 · Notificaciones al autor
**Resumen:** Cuando un artículo recibe votos, ¿se notifica al autor? ¿Con qué frecuencia? ¿Puede desactivarlas? No está definido. Afecta a la experiencia del periodista y a si la plataforma genera engagement activo o es puramente pasiva para el autor.

**Documentos relacionados:** `sistema-votos-visualizacion.md` sección 11.

---

### TODO-013 · Periodistas de medios tradicionales con línea editorial
**Resumen:** Un periodista de un medio con línea editorial documentada puede cumplir todos los criterios de verificación y tener presión de su director para votar en una dirección concreta. Hay que decidir si este segmento se trata de forma diferenciada (segmentación visual, voto de rigor anónimo opcional) o se pospone a Fase 2. Decisión especialmente delicada porque implica clasificar medios por línea editorial — decisión política en sí misma.

**Documentos relacionados:** `verificacion-periodistas.md` sección 14.

---

### TODO-014 · Multisig del smart contract — definir titulares
**Resumen:** El contrato de Polygon requiere un multisig 2-de-3 para operaciones críticas (transferencia de ownership, cambio de dirección del registrar). Hay que identificar quiénes son los 3 titulares de las claves antes del deploy. Deben ser personas de confianza ajenas entre sí y ajenas al creador del proyecto para evitar concentración de control.

**Documentos relacionados:** `arquitectura-trazabilidad.md` sección 18.

---

## 🟢 FASE 2 — Puede esperar al MVP validado

---

### TODO-015 · Voto ciudadano
**Resumen:** El voto de usuarios registrados (no periodistas) está excluido del MVP por diseño. Para Fase 2 hay que diseñar el sistema anti-bot (fricción de registro, verificación de teléfono o micropago simbólico), cómo se muestra visualmente separado del voto profesional, y las implicaciones GDPR específicas para usuarios que no son periodistas verificados.

---

### TODO-016 · Autocompletado de formulario desde URL
**Resumen:** En Fase 2, cuando el periodista pega su URL, el sistema lee automáticamente los metadatos públicos (OpenGraph, Schema.org) y rellena el formulario. El periodista revisa y confirma. Reduce la fricción de envío sin comprometer la responsabilidad del autor sobre lo que declara. Implementación estimada: 1-2 días de desarrollo.

**Documentos relacionados:** `decisiones-cerradas.md` DC-002.

---

### TODO-017 · Envío de artículos por terceros
**Resumen:** Permitir que cualquier periodista Nivel 2+ proponga artículos de otros para revisión — para alabar un buen trabajo o denunciar uno malo. Requiere consulta legal previa (TODO-006). El modelo propuesto está documentado en `sistema-votos-visualizacion.md` sección 5.

---

### TODO-018 · Zero-Knowledge Proofs para periodistas de grandes medios
**Resumen:** Permite que un periodista de un medio con línea editorial demuestre criptográficamente que es profesional verificado sin revelar su identidad pública. Vota de forma anónima pero su voto computa en las métricas globales. Complejidad técnica alta. Solo tiene sentido implementarlo si el segmento de periodistas de grandes medios se decide abordar (ver TODO-013).

**Documentos relacionados:** `arquitectura-trazabilidad.md` sección 14, `verificacion-periodistas.md` sección 14.

---

### TODO-019 · Anotaciones de contexto en párrafos
**Resumen:** Los periodistas Nivel 3 pueden añadir anotaciones directamente sobre párrafos del artículo para señalar datos sacados de contexto o manipulación de guante blanco. Requiere que la plataforma acceda al contenido del artículo de alguna forma — incompatible con el modelo de solo links externos del MVP. Revisar cuando se decida el modelo de contenido de Fase 2.

---

### TODO-020 · Algoritmo de recomendación del feed
**Resumen:** El feed del MVP es cronológico puro sin algoritmo. En Fase 2 puede añadirse ordenación por relevancia, pero cualquier algoritmo de recomendación debe ser público y auditable — un algoritmo opaco contradice la filosofía del proyecto. Si se implementa, el criterio de ordenación debe documentarse como cualquier otra decisión de diseño.

---

### TODO-021 · Estrategia de lanzamiento y masa crítica
**Resumen:** El problema del huevo y la gallina. Sin periodistas activos la plataforma no tiene valor. Sin valor no hay periodistas. Necesita una estrategia concreta para conseguir los primeros 30-50 periodistas antes de que la plataforma tenga tracción propia. Más estrategia que diseño técnico, pero sin resolverlo el producto es irrelevante aunque esté perfectamente construido.

**Temas a cubrir:**
- Cómo identificar y contactar a los periodistas del Grupo Fundador
- Qué propuesta de valor concreta se les hace para que inviertan su tiempo sin garantías
- En qué momento se abre el registro público
- Cómo se gestiona el crecimiento para evitar la captura ideológica en el arranque

---

### TODO-022 · Portabilidad de datos del periodista
**Resumen:** Si un periodista quiere abandonar la plataforma, ¿puede exportar su historial de votos y avales en un formato estándar? Sus votos en el log público permanecen en cualquier caso — son parte del registro inmutable — pero el acceso cómodo a sus propios datos es un derecho razonable y un requisito GDPR.

**Documentos relacionados:** `verificacion-periodistas.md` sección 11.

---

### TODO-023 · Periodistas fallecidos
**Resumen:** ¿Qué ocurre con el perfil y el historial de un periodista fallecido? ¿Se marca como inactivo automáticamente o manualmente? ¿Sus votos mantienen el mismo peso visual? ¿Puede alguien (familia, medio) solicitar la gestión del perfil? Caso de uso poco frecuente pero necesita política explícita.

**Documentos relacionados:** `verificacion-periodistas.md` sección 11.

---

### TODO-024 · Arquitectura modular — completar documento
**Resumen:** El documento `arquitectura-modular.md` tiene tres secciones identificadas como faltantes que no se llegaron a escribir: (1) tabla de dominios identificados con sus características de viabilidad, (2) sección de dominios donde el sistema encaja bien y mal con razonamiento, y (3) posicionamiento estratégico explícito — "no compites con PubMed, le ofreces a PubMed una capa que no tiene". Sin estas secciones el documento no es suficientemente útil para una institución que quiera evaluar si adoptar el sistema.

**Documentos relacionados:** `arquitectura-modular.md`.

---

### TODO-025 · Especificación técnica de la API por módulo
**Resumen:** La sección de API en `arquitectura-modular.md` es un diseño conceptual con tres ejemplos de endpoints. Falta la especificación completa: todos los endpoints, autenticación, rate limiting, versionado, política de CORS, manejo de errores y documentación en formato estándar (OpenAPI/Swagger). No implementar en MVP — diseñar antes de Fase 2.

**Documentos relacionados:** `arquitectura-modular.md` sección 5.

---

### TODO-026 · Especificación técnica del widget embebible
**Resumen:** El widget está descrito conceptualmente con sus tres modos (compacto, estándar, completo) pero sin especificación técnica. Falta definir: opciones de configuración completas, política de CORS, hosting del script, compatibilidad con navegadores, comportamiento cuando no hay evaluaciones disponibles, y cómo se actualiza el widget sin romper sitios que ya lo tienen integrado. No implementar en MVP.

**Documentos relacionados:** `arquitectura-modular.md` sección 6.

---

### TODO-027 · Federación entre instancias
**Resumen:** Si hay una instancia de periodismo en España y otra en Latinoamérica, ¿pueden reconocer mutuamente sus expertos verificados? ¿Un periodista verificado en una instancia puede votar en otra sin reverificarse? Es la pregunta más importante de la arquitectura multi-instancia y tiene implicaciones técnicas profundas. Puede modelarse como ActivityPub (Mastodon) o como sistema de confianza bilateral entre instancias. No bloquea el MVP pero hay que decidirlo antes de que haya dos instancias funcionando con diseños incompatibles.

**Documentos relacionados:** `arquitectura-modular.md` sección 8, `vision-filosofia.md` sección 6.

---

### TODO-028 · Definir core vs. configurable por instancia
**Resumen:** El documento de visión establece el modelo governance-by-fork pero no dice explícitamente qué es el core inmutable y qué puede modificar una instancia sin hacer fork. Esa lista es el contrato real del protocolo. Sin ella cualquier instancia puede tomar decisiones incompatibles sin saberlo. Necesita una sección explícita en `vision-filosofia.md` o en `arquitectura-modular.md`.

**Documentos relacionados:** `vision-filosofia.md` sección 3, `arquitectura-modular.md` sección 7.

---

### TODO-029 · Modo privado con trazabilidad selectiva — especificación
**Resumen:** Diseñado conceptualmente en `arquitectura-modular.md` sección 4.1 como extensión para medicina. Falta especificar: modelo de control de acceso, qué parte de la trazabilidad es interna vs. pública, cómo se publican conclusiones agregadas sin exponer votos individuales, y si el modo privado es un módulo separado o una configuración del Módulo 1. Relevante también fuera de medicina — cualquier institución que necesite evaluación interna antes de hacer pública una posición.

**Documentos relacionados:** `arquitectura-modular.md` sección 4.1.

---

### TODO-030 · Integración ORCID — especificación técnica
**Resumen:** ORCID está identificado como la integración más importante para reducir fricción de onboarding en contextos académicos. Falta la especificación técnica del flujo: autenticación OAuth con ORCID, qué datos se importan del perfil (especialidad, historial de publicaciones, afiliación), cómo se mantiene la sincronización si el perfil ORCID cambia, y qué ocurre si el investigador revoca el acceso.

**Documentos relacionados:** `arquitectura-modular.md` secciones 3 y 4.3.

---

### TODO-031 · Compatibilidad con estándares de reporte — formato de importación
**Resumen:** El Módulo 4 (checklist) puede importar criterios de estándares existentes (CONSORT, PRISMA, CARE, STROBE, TRIPOD). Falta definir el formato técnico de importación: ¿JSON Schema? ¿YAML? ¿Una interfaz de administración visual? Y más importante — ¿quién mantiene actualizados esos estándares cuando las organizaciones que los publican los revisan? Los estándares médicos se actualizan periódicamente.

**Documentos relacionados:** `arquitectura-modular.md` sección 4.2.

---

## Resumen de estado

| Categoría | Total | Completados |
|---|---|---|
| 🔴 Bloqueante | 4 | 1 (TODO-004 MVP cerrado) |
| 🟡 Importante | 10 | 0 |
| 🟢 Fase 2 | 17 | 0 |
| **Total** | **31** | **1** |

---

## Documentos del proyecto

| Documento | Estado | Cubre |
|---|---|---|
| `periodismo-pares.md` | ✓ Completo | Conceptualización general del caso de uso periodismo |
| `arquitectura-trazabilidad.md` | ✓ Completo | Merkle Tree, blockchain, trazabilidad |
| `verificacion-periodistas.md` | ✓ Completo | Niveles, percentiles, proceso de solicitud |
| `sistema-votos-visualizacion.md` | ✓ Completo | Votos, IHP, visualización |
| `decisiones-cerradas.md` | ✓ Vivo | Registro de decisiones tomadas |
| `todo-list.md` | ✓ Vivo | Este documento |
| `vision-filosofia.md` | ✓ Borrador · revisión pendiente | Filosofía, protocolo vs. app, governance by fork |
| `arquitectura-modular.md` | ⚠ Incompleto · ver TODO-024 | Módulos, API, widget, extensiones medicina |
| `gobernanza.md` | ⬜ Pendiente | TODO-005 |
| `voto-ciudadano.md` | ⬜ Fase 2 | TODO-015 |
| `estrategia-lanzamiento.md` | ⬜ Fase 2 | TODO-021 |

---

*Documento vivo — marcar como completado y mover a `decisiones-cerradas.md` cada TODO resuelto*
