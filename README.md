# PAD
Biblioteca interactiva de Microbiología
# Prompt maestro — Generador de módulos para PAD

Usá este prompt (completo, tal cual) cada vez que quieras agregar o actualizar un
microorganismo. Se lo pegás a cualquier IA (Claude, ChatGPT, etc.) junto con tu
material de fuente (apuntes, resumen de cátedra, capítulo de libro, etc.), y la IA
te devuelve un archivo `.html` listo para subir a `data/modulos/` en GitHub.

No hace falta que entiendas el HTML: copiás la respuesta completa de la IA, la
pegás en un archivo de texto nuevo, lo guardás con extensión `.html`
(ej: `klebsiella-pneumoniae.html`) y lo subís a la carpeta `data/modulos/` del
repositorio. Al recargar la página web, aparece solo.

---

## PROMPT (copiar desde acá hasta el final)

```
Actuá como un generador de fichas de microbiología para mi biblioteca interactiva
"PAD". Te voy a pasar material de estudio (apuntes, resumen, capítulo de libro,
lo que sea) sobre UN microorganismo, y vos tenés que devolverme ÚNICAMENTE un
bloque de código HTML con este formato exacto, sin explicaciones antes o
después, sin comentarios, sin marcar el bloque con ```html ni ``` de ningún tipo:

<article data-module-type="TIPO" data-name="NOMBRE CIENTÍFICO" data-grupo="GRUPO" data-gram="GRAM" data-image="">
  <div data-field="caracteristicas">...</div>
  <div data-field="morfologia">...</div>
  <div data-field="epidemiologia">...</div>
  <div data-field="habitat">...</div>
  <div data-field="infeccion">...</div>
  <div data-field="virulencia">...</div>
  <div data-field="clinica">...</div>
  <div data-field="diagnostico">...</div>
  <div data-field="tratamiento">...</div>
  <div data-field="prevencion">...</div>
</article>

REGLAS OBLIGATORIAS:

1. TIPO (atributo data-module-type) debe ser exactamente uno de estos 4 valores,
   en minúscula: bacteria | virus | parasito | hongo.

2. data-gram solo aplica si TIPO="bacteria", y debe ser exactamente uno de:
   "Gram positivo" | "Gram negativo" | "Ácido-alcohol resistente" | "Variable" |
   "No aplica". Si TIPO no es bacteria, dejá data-gram="".

3. data-grupo es una categoría corta (ej: "Cocos Gram positivos",
   "Enterobacterias", "Micobacterias", "Herpesvirus", "Protozoos intestinales").

4. data-image siempre va vacío: data-image="".

5. CAMPO POR CAMPO — ESTO ES LO MÁS IMPORTANTE:
   Los 10 <div data-field="..."> representan: características generales,
   morfología, epidemiología, hábitat/reservorio, cómo infecta, factores de
   virulencia, correlación clínica, diagnóstico, tratamiento y prevención.

   - Incluí un <div data-field="X"> SOLO si el material que te pasé tiene
     información real, concreta y completa para ese campo.
   - Si el material NO menciona ese aspecto (por ejemplo, no hay nada sobre
     epidemiología), ELIMINÁ ESA LÍNEA POR COMPLETO. No la dejes vacía, no
     pongas "No especificado", "N/A" ni inventes contenido de relleno: la
     línea entera del campo no debe existir en el HTML.
   - NUNCA inventes ni completes con conocimiento general datos que no estén
     en el material que te pasé. Si dudás si algo está o no en la fuente, no
     lo pongas.
   - Cada campo que sí incluyas debe tener el contenido completo y bien
     redactado (puede ser un párrafo, o una lista con <ul><li>...</li></ul>
     si el contenido lo amerita), en el mismo estilo académico y conciso que
     usás para estudiar (nivel universitario, español neutro/rioplatense).

6. Devolvé un solo bloque <article> por microorganismo. Si te paso material
   de varios microorganismos en el mismo mensaje, devolvé varios bloques
   <article> uno debajo del otro (sin nada más entre medio).

7. Si te falta información clave para completar el bloque (por ejemplo no
   tengo claro si es bacteria/virus/parásito/hongo, o el grupo), preguntame
   antes de generar el HTML en vez de adivinar.

Ahora esperá a que te pase el nombre del microorganismo y el material de
estudio correspondiente.
```

---

## Cómo lo usás en la práctica

1. Pegás el prompt de arriba en una IA.
2. Le mandás el nombre del microorganismo + tus apuntes/resumen sobre él.
3. Copiás la respuesta (el bloque `<article>...</article>` completo).
4. La guardás en un archivo `.html` nuevo (nombre libre, ej: `e-coli.html`).
5. Lo subís a la carpeta `data/modulos/` de tu repositorio en GitHub (podés
   arrastrarlo directo en la web de GitHub: "Add file" → "Upload files").
6. Entrás a la página web y la recargás (o usás el botón "🔄 Recargar módulos
   desde GitHub ahora" en la sección "Agregar contenido"): el microorganismo
   aparece solo, con exactamente los campos que tenía información — sin
   secciones vacías.

## Requisito único de configuración (una sola vez)

Para que la carga automática funcione, alguien tiene que completar 4 valores
en `index.html` (buscá `GITHUB_CONFIG`, cerca del inicio del `<script>`):

```js
const GITHUB_CONFIG = {
  owner:  'TU-USUARIO-DE-GITHUB',
  repo:   'PAD',
  branch: 'main',
  path:   'data/modulos'
};
```

Reemplazá `owner` por tu usuario (u organización) de GitHub, y `repo`/`branch`
por el nombre real del repositorio y la rama publicada en GitHub Pages. Es la
única edición de código necesaria; después de eso, todo el mantenimiento del
contenido se hace solo subiendo archivos `.html` a `data/modulos/`.
