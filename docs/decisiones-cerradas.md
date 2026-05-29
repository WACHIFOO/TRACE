# Decisiones Cerradas del Proyecto
**Documento vivo** · Se actualiza cada vez que se cierra una decisión de diseño · **Versión:** 0.1

> Este documento recoge únicamente decisiones ya tomadas con su razonamiento. No contiene análisis ni opciones abiertas — para eso están los documentos de módulo. Su función es evitar reabrir debates cerrados durante la implementación.

---

## DC-001 · Modelo de contenido — MVP

**Decisión:** La plataforma no aloja contenido. Solo evalúa artículos externos mediante URL.

**Qué incluye el MVP:**
- El periodista aporta URL + metadatos + checklist completado manualmente
- La plataforma calcula el hash del contenido en el momento del envío
- Si el contenido externo cambia después del envío, el hash lo detecta y genera alerta visible

**Qué queda fuera del MVP:**
- Autocompletado del formulario a partir de metadatos de la URL (OpenGraph, Schema.org)
- Snapshot archivado del contenido para cuando el link externo muera

**Razonamiento:**
- Reduce el tiempo de desarrollo del MVP a semanas en lugar de meses
- Elimina la responsabilidad legal sobre el contenido alojado
- Reduce la fricción de adopción — el periodista mantiene su canal habitual
- La trazabilidad criptográfica funciona igual con links externos que con contenido alojado

**Revisión prevista:** cuando la plataforma tenga 50+ periodistas activos y el modelo de revisión esté validado. En ese momento evaluar migración a modelo híbrido (Opción C del análisis).

---

## DC-002 · Autocompletado de formulario — Fase 2

**Decisión:** El autocompletado de metadatos a partir de URL se implementa en Fase 2, no en el MVP.

**Qué hace:**
- El periodista pega su URL y el sistema lee automáticamente los metadatos públicos (OpenGraph, Schema.org, meta tags)
- Rellena el formulario con lo que encuentra: título, autor, fecha, medio, tipo de contenido
- El periodista revisa, corrige y confirma antes de enviar
- El sistema no guarda nada del contenido — solo lo que el periodista valida conscientemente

**Qué no hace nunca:**
- No lee ni almacena el cuerpo del artículo
- No evalúa si las fuentes son válidas
- No infiere si hay separación hecho/opinión
- No completa los campos que requieren criterio humano (derecho a réplica, fuentes, separación)

**Base legal:** los metadatos OpenGraph y Schema.org son publicados intencionalmente por los medios para ser leídos por herramientas externas. No es contenido protegido por derechos de autor. Es el mismo mecanismo que usan Zotero, Notion, o cualquier gestor de referencias.

**Complejidad técnica estimada:** baja — fetch de la URL + parseo de meta tags. Implementable en 1-2 días de desarrollo una vez que el MVP esté validado.

---

## DC-003 · Naturaleza open source y económica

**Decisión:** El proyecto es completamente open source, sin ánimo de lucro y con licencia AGPL.

**Qué implica:**
- Código fuente público en GitHub desde el día 1
- Licencia AGPL — cualquier fork debe también ser open source
- Sin publicidad, sin inversores, sin modelo de negocio activo en MVP
- El creador aporta la mano de obra tecnológica de forma gratuita

**Sostenibilidad a explorar en fases posteriores** (no cerrado todavía):
- Mecenazgo colectivo modelo Wikipedia
- Subvenciones de fundaciones de libertad de prensa
- API de datos para investigadores o medios

---

## DC-004 · Arquitectura de trazabilidad

**Decisión:** Arquitectura de cuatro capas complementarias, no alternativas.

**Las cuatro capas:**
1. **PostgreSQL** — datos operacionales en servidor propio
2. **Merkle Tree diario** — árbol construido con todos los votos del día, genera una raíz única
3. **GitHub público** — commit diario con el log completo y las pruebas de inclusión
4. **OpenTimestamps + Polygon** — la raíz diaria se ancla en Bitcoin (gratis) y se registra en Polygon (~$0.002/día)

**Lo que esto garantiza:** ni el propio proyecto puede manipular el historial de votos retroactivamente sin que cualquier persona lo detecte.

**Coste total de trazabilidad:** ~$0.73/año en fees de Polygon. El resto es gratuito.

**Documento de referencia:** `arquitectura-trazabilidad.md`

---

## DC-005 · Red blockchain — Polygon PoS

**Decisión:** Polygon PoS como red blockchain para el registro de raíces Merkle diarias.

**Por qué Polygon y no otras:**
- Fees de gas por debajo de $0.01 por transacción en condiciones normales
- Compatible con Ethereum (mismo tooling, Solidity, ethers.js)
- Token nativo: POL (antes MATIC)
- Descartado Ethereum mainnet — fees de $5-50 por transacción hacen inviable 1 tx/día sostenida

**Modelo de pago de gas:** el servidor paga el gas de la transacción diaria. El periodista no necesita wallet ni POL para votar. Capital inicial necesario: ~$5 en POL, suficiente para años de operación a escala de MVP.

---

## DC-006 · Sistema de verificación de periodistas — modelo base

**Decisión:** Combinación de criterios objetivos verificables + aval entre pares. Sin carné de prensa obligatorio.

**Criterios de entrada:** al menos uno del Grupo A (identidad profesional: titulación, carné, acreditación) + al menos uno del Grupo B (historial público: artículos en medios con ISSN, newsletter con audiencia verificable, libro con ISBN).

**Tres niveles:**
- Nivel 1 — Periodista registrado: documentación verificada, sin aval requerido, puede votar
- Nivel 2 — Periodista verificado: + 1 aval de Nivel 2 o superior, puede avalar a otros
- Nivel 3 — Periodista verificado senior: + 3 avales + IHP en percentil 70+ + 50 votos emitidos, puede anotar contexto en párrafos

**Documento de referencia:** `verificacion-periodistas.md`

---

## DC-007 · Sistema de percentil — formato numérico directo

**Decisión:** El respaldo de la comunidad se muestra con tres elementos simultáneos: número absoluto de avales + percentil relativo + total del grupo. Sin tiers ni frases narrativas.

**Formato:**
```
Avales recibidos:  23    Top 8%  de 47 especialistas en economía verificados
Avales recibidos:  23    Top 21% de 340 periodistas verificados totales
```

**Por qué este formato:**
- El número absoluto ancla la realidad independientemente del tamaño de la plataforma
- El percentil da contexto relativo sin umbral fijo arbitrario
- El total del grupo permite interpretar el percentil honestamente
- Es el más coherente con la filosofía de transparencia radical — no colapsa información en etiquetas

**Doble percentil:** uno dentro de la especialidad declarada y otro dentro del total de la plataforma. Un periodista muy respetado en su nicho pero poco conocido fuera tendrá percentiles distintos en ambos — información valiosa para el lector.

**Documento de referencia:** `verificacion-periodistas.md` sección 7

---

## DC-008 · Especialidades — el lector interpreta, la plataforma no pondera

**Decisión:** Las especialidades declaradas son información contextual para el lector. La plataforma no aplica pesos algorítmicos según especialidad — segmenta visualmente y deja que el lector decida qué capa le importa más.

**Lo que la plataforma hace:**
- Muestra la especialidad del revisor junto a cada voto
- Segmenta los votos visualmente por especialidad en la vista detallada
- Calcula el percentil de especialidad como métrica separada del percentil general

**Lo que la plataforma no hace:**
- No pondera el voto de un economista más que el de un periodista político en un artículo económico
- No decide qué especialidad es más relevante para cada artículo
- No certifica que la especialidad declarada es correcta — eso lo verifica la comunidad con el historial público

**Razonamiento:** cualquier algoritmo de ponderación por especialidad sería una caja negra opaca que contradice la filosofía del proyecto. La segmentación visual es más honesta y más auditable.

---

*Documento vivo — añadir entrada cada vez que se cierre una decisión durante el diseño o la implementación*
