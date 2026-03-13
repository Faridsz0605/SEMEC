# AGENTS.md — SEMEC

Reglas globales para agentes de inteligencia artificial que trabajen en este repositorio.
Aplican a todas las investigaciones salvo que una sección específica indique lo contrario.

---

## 1. Contexto del repositorio

Este es un repositorio académico del **Semillero de Medición Económica (SEMEC)** de la Universidad Santo Tomás, Bucaramanga. Contiene investigaciones econométricas formales. No es un proyecto de software. No tiene dependencias de paquetes npm, pip ni similares.

Toda salida escrita que produzca un agente debe ser compatible con el contexto académico: lenguaje técnico preciso, tercera persona impersonal, sin expresiones coloquiales, sin emojis en documentos de investigación.

---

## 2. Reglas globales

### 2.1 Idioma y estilo

- El idioma de trabajo de todas las investigaciones es **español académico formal**.
- Las citas, referencias y bibliografía siguen el estándar **APA 7.ª edición** sin excepción.
- Prohibido el uso de emojis en cualquier documento de investigación (`.md`, `.tex`, `.docx`, `.pdf`).
- Vocabulario técnico obligatorio: usar los términos precisos de la disciplina. Evitar perífrasis vagas.
  - Correcto: *reducción estadísticamente significativa*, *propensity score matching*, *asimetría de información*
  - Incorrecto: *baja del consumo*, *técnica de emparejamiento*, *diferencia de información*

### 2.2 Integridad de archivos

- **NUNCA** eliminar, renombrar ni mover archivos o directorios sin instrucción explícita del usuario.
- **NUNCA** reestructurar directorios sin confirmación previa. Mostrar el plan y esperar aprobación.
- Los archivos `CLAUDE.md` dentro de cada carpeta de investigación son instrucciones canónicas para el agente de esa investigación. Leerlos antes de actuar.
- Los archivos `.gitignore` de cada subcarpeta son intencionales. No modificarlos sin autorización.

### 2.3 Datos

- El directorio `data/` está excluido del control de versiones por diseño. No agregar archivos de datos al staging de git.
- **NUNCA** commitear datos crudos, archivos `.csv`, `.xlsx` ni similares.
- Las referencias a datos dentro de los documentos deben ser precisas. Si un dato no está disponible, marcarlo con `<!-- TO DO: insertar dato -->` en lugar de inventarlo.

### 2.4 Scripts

- Los scripts R y Python van exclusivamente en los directorios `SCRIPTS/` de cada investigación.
- No crear scripts fuera de esas carpetas.
- Un script no reemplaza al documento de investigación. La metodología y los resultados se documentan en el `.md` correspondiente, no solo en el código.

### 2.5 Flujo de compilación

El pipeline de publicación es:

```
Markdown (.md) → Pandoc + pdflatex → PDF (APA 7)
```

Comando estándar:

```bash
pandoc informe.md \
  --template ~/.local/share/pandoc/templates/APA-7.latex \
  --pdf-engine=pdflatex \
  -o informe-final.pdf
```

- No editar los archivos `.pdf` directamente. Son salidas compiladas.
- El YAML front matter de cada `.md` es parte del documento. No eliminarlo ni modificarlo sin revisar compatibilidad con el template LaTeX.

### 2.6 Git

- **NUNCA** hacer commit directo a `main`. Siempre crear una rama con convención:
  - `feat/` — nueva funcionalidad o sección
  - `fix/` — corrección de error
  - `docs/` — cambios en documentación
  - `chore/` — mantenimiento general
  - `refactor/` — reorganización sin cambio de contenido
- Los commits siguen el formato **conventional commits**: `tipo: descripción breve en español`
- **NUNCA** agregar atribución de IA en los commits (`Co-Authored-By` o similares).

### 2.7 Verificación antes de afirmar

- Si una afirmación técnica o estadística no puede verificarse con el contenido del repositorio, marcarla con `<!-- TO DO: verificar -->` y notificar al usuario.
- No inventar coeficientes, valores p, tamaños de muestra ni ningún dato cuantitativo.
- No agregar referencias bibliográficas que no estén en la lista canónica del proyecto correspondiente.

---

## 3. Investigación: FOPL — Etiquetado Frontal de Alimentos

**Carpeta:** `informe-FOLP/`
**Estado:** En revisión
**Líderes:** Farid Sayago · Laura Gómez
**Director:** Henry Sebastián

### 3.1 Instrucciones canónicas del agente

Antes de cualquier acción en esta carpeta, leer:

```
informe-FOLP/CLAUDE.md
```

Ese archivo contiene el protocolo completo: pipeline de compilación, vocabulario técnico requerido, restricciones sobre citas, referencias canónicas autorizadas y checklist de exportación PDF.

### 3.2 Documento principal

El documento de investigación es `informe-FOLP/informe-SEMEC.md`. Su YAML front matter controla la compilación. No modificar los campos `title`, `author`, `institution`, `advisor` sin autorización explícita.

### 3.3 Referencias

Solo se pueden usar las referencias listadas en `informe-FOLP/CLAUDE.md` bajo la sección "Referencias Canónicas del Proyecto". Para agregar una nueva fuente, consultar al usuario antes de incluirla.

### 3.4 Datos faltantes en el documento

El documento contiene marcadores `<!-- TO DO -->` en secciones donde faltan datos de la encuesta (N muestral, distribución por sexo, estadísticos W, valores p, etc.). No completar esos marcadores con valores inventados. Solo completarlos cuando el usuario provea los datos reales.

### 3.5 Metodología — resumen técnico

| Elemento | Descripción |
|:---------|:------------|
| Diseño | Experimental intragrupos (*within-subjects*) |
| Instrumento | Encuesta virtual · Google Forms |
| Variable dependiente | Probabilidad de compra autorreportada (escala 0–100) |
| Variables independientes | Presencia de sello (dicotómica) · Tipo de sello |
| Técnica de análisis | Propensity Score Matching (PSM) + Prueba de Wilcoxon |
| Software | R |
| Marco legal | Resolución 254 de 2021 · Decreto 254 de 2023 |
| Pregunta de investigación | ¿Efecto Nudge o efecto informativo? |

---

## 4. Investigación: Informalidad Laboral — [ON GOING]

**Carpeta:** `informe-formalidad/`
**Estado:** En curso — fase de revisión de literatura
**Líderes:** Por definir
**Director:** Henry Sebastián

### 4.1 Estado actual

Esta investigación está en sus etapas iniciales. La actividad actual es la recopilación y revisión sistemática de literatura. No existe aún un documento `.md` de investigación, ni scripts, ni metodología definida.

Los archivos presentes son:

- `metodologia_borradores.docx` — borrador metodológico en elaboración (no editar directamente desde el agente)
- `Docs-referencias/` — PDFs de referencia de solo lectura

### 4.2 Archivos de referencia (solo lectura)

Los PDFs en `Docs-referencias/` son fuentes de consulta. No moverlos, renombrarlos ni eliminarlos.

| Archivo | Fuente |
|:--------|:-------|
| `Informalidad Colombia, Banrep.pdf` | Banco de la República de Colombia |
| `informalidad colombia 2023.pdf` | Fuente nacional — 2023 |
| `3956 Conpes informalidad.pdf` | CONPES — política pública |
| `Peru informal.pdf` | Referencia comparada — Perú |
| `Journal of Economic Surveys - 2021 - Dell'Anno.pdf` | Dell'Anno (2021) — marco teórico internacional |

### 4.3 Restricciones específicas

- No crear scripts en `SCRIPTS/` sin instrucción explícita del usuario. La carpeta existe pero está vacía intencionalmente.
- No asumir una metodología definitiva. El diseño está en borrador.
- Cualquier referencia nueva que se proponga para esta investigación debe consultarse con el usuario antes de incorporarse.
- Al redactar contenido para esta investigación, dejar explícito que es preliminar y sujeto a revisión.

### 4.4 Próximos pasos esperados (referencia, no ejecutar sin instrucción)

1. Definición del marco teórico sobre informalidad laboral
2. Construcción del instrumento de recolección de datos
3. Creación del documento principal `informe-formalidad.md`
4. Desarrollo de scripts en R para análisis econométrico

---

## 5. Lo que un agente NUNCA debe hacer en este repositorio

- Inventar datos estadísticos, coeficientes o resultados de ningún tipo.
- Agregar referencias bibliográficas no verificadas.
- Modificar el formato APA 7 de citas existentes.
- Commitear a `main` directamente.
- Commitear archivos de datos crudos (`data/`, `.csv`, `.xlsx`).
- Usar emojis en documentos de investigación.
- Ejecutar reestructuraciones de directorios sin confirmación explícita del usuario.
- Completar secciones marcadas con `<!-- TO DO -->` con valores asumidos.
- Eliminar comentarios `<!-- TO DO -->` sin haber resuelto el pendiente con datos reales.
