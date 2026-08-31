# Rastreador de hábitos — index.html

Rastreador personal de entrenamiento de 400 m con vallas. Una sola página que el
usuario abre desde su disco y usa desde el celular, de pie en la pista.
Módulos: molestia de isquiotibiales, sueño, hábitos, bitácora de gimnasio,
marcas, pruebas mensuales y resumen semanal.

## Restricciones duras

- Un único `index.html`: HTML, CSS y JS inline. Sin dependencias, sin CDNs, sin build.
- Gráficos en SVG escrito a mano (`<polyline>`, `<path>`). Nunca librerías de charts.
- Toda lectura y escritura de `localStorage` envuelta en try/catch.
- Reutiliza los tokens CSS y las clases que ya existen. No renombres lo que funciona.
- Conserva el tema claro/oscuro. Ningún color se define solo dentro de un bloque de tema.
- Todo el texto de la interfaz en español.

## Datos — la parte irreversible

El código se puede reescribir; los datos del usuario no. Un desgarre no se puede
volver a medir dos meses después.

- Llave actual: `habit-tracker-data-v3`. Las anteriores (`v2`, `v1`) siguen en
  `LEGACY_KEYS` y **no se borran ni se sobrescriben nunca**. Son el respaldo.
- Cambio de esquema = subir `SCHEMA_VERSION` + migrar desde la llave anterior.
- Una colección nueva se agrega en los cuatro lugares: `createEmptyState`,
  `normalizeState`, la validación de importación y el export. Faltar en uno se
  nota semanas después, cuando ya hay datos que perder.
- Carga defensiva: si el JSON está corrupto, guarda el texto original bajo
  `habit-tracker-backup-*`, avisa en pantalla y arranca limpio. Nunca dejes la
  página en blanco sin explicación.
- **Ausencia de dato es `null`, jamás `0` ni `""`.** Un 0 de molestia de isquio es
  un dato real y valioso. Nada de `if (!valor)` sobre valores numéricos.

## Uso en móvil

Se usa con el dedo, con frío y con prisa. Lo incómodo de capturar no se captura.

- Objetivos táctiles de 44 px mínimo. Las celdas del heatmap suben a 15 px bajo 640 px.
- El heatmap va del mes más reciente a la izquierda hacia atrás en el tiempo. Lo
  que se mira a diario es la semana en curso: si queda al final de la tira, hay
  que arrastrar la barra cada vez para verla.
- Nada de `confirm()` ni `alert()`: confirmación en línea dentro de la tarjeta.
- El drag and drop de HTML5 no funciona con el dedo. Botones de subir y bajar.
- Ningún gesto destructivo ni intrusivo en un toque simple sobre texto.
- Tablas anchas: scroll horizontal en su propio contenedor y primera columna fija.
  La página nunca gana scroll horizontal.

## Trampas ya encontradas en este proyecto

- Un `input[type=range]` sólo dispara `input` cuando el valor **cambia**. Si el
  slider ya está en el extremo, tocarlo ahí no guarda nada. Hay que escuchar
  también `pointerup` para confirmar el valor actual.
- Toda métrica derivada necesita saber su dirección: en un tiempo menos es mejor,
  en un peso más es mejor. No asumas que el número mayor gana.
- Un indicador de "todo bien" calculado sobre "los últimos N registros" miente en
  cuanto el usuario deja de registrar. Si sirve para decidir cargas de
  entrenamiento, exige días de calendario consecutivos y recientes.
- Redibujar la lista completa en cada toque son cientos de celdas y se siente
  lento en el teléfono. Actualiza sólo el nodo afectado.

## Antes de entregar

No cierres con "debería funcionar". Escribe criterios de aceptación concretos,
con valores reales, y compruébalos:

- Migración: abrir con datos del esquema anterior y confirmar que aparece todo, y
  que la llave vieja sigue existiendo.
- Exportar, borrar el `localStorage`, importar: el estado vuelve idéntico.
- Meter basura a mano en `localStorage`: la página levanta con aviso, no en blanco.
- Cada regla condicional nueva, probada con un caso que la active y otro que no.
- A 375 px de ancho: sin scroll horizontal y todos los controles alcanzables.
