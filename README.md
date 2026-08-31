# Rastreador de hábitos 🏃

Rastreador de entrenamiento para atletismo, hecho en un solo archivo HTML.
Sin instalar nada, sin servidor y sin base de datos: se abre en el navegador y
guarda todo en `localStorage`.

Pensado para usarse desde el celular, en la pista, entre series.

## Qué incluye

**Hoy**

- 🦵 Molestia de isquiotibiales, con registro independiente por pierna (0–10) y
  nota del día. Banners automáticos de alerta según la evolución de los últimos días.
- 🌙 Sueño: horas y calidad, con medidor y mapa de calor.
- ✅ Hábitos diarios con rachas y mapa de calor de 26 semanas, agrupado por mes,
  del más reciente a la izquierda.

**Entrenamiento**

- 🏋️ Bitácora de gimnasio: series, repeticiones y peso por ejercicio, con
  historial por ejercicio, mejor sesión y gráfica de progresión.
- Contador semanal de los ejercicios marcados como trabajo de prevención.

**Marcas**

- ⏱️ Marcas de 60 a 400 m, planas o con vallas, con mejores tiempos y el
  diferencial entre 400 con vallas y 400 plano.
- 📐 Batería de pruebas de fin de mes (velocidad, resistencia, saltos y
  levantamientos) en una tabla de progresión mes a mes, con la mejor marca
  histórica de cada prueba y la comparación contra el mes anterior.
- Indicador de asimetría entre triple izquierdo y derecho.

**Resumen**

- 📋 Cumplimiento de hábitos, sueño promedio, molestia máxima por pierna y
  sesiones de gimnasio de los últimos 7 días.

**Y además**

- 📅 Selector de fecha: se puede rellenar cualquier día pasado, no sólo hoy.
- 💾 Exportar e importar todos los datos en JSON.
- 🌗 Tema claro y oscuro.

## Cómo usarlo

1. Descarga o clona este repositorio.
2. Abre [`index.html`](index.html) en tu navegador.
3. Listo.

Los datos viven en el `localStorage` de ese navegador, así que **exporta tu JSON
de vez en cuando**: si limpias el caché o cambias de dispositivo, se pierden.
El botón de exportar está arriba a la derecha.

## Tecnologías

HTML, CSS y JavaScript puro. Sin frameworks, sin dependencias, sin build.
Los gráficos son SVG escrito a mano.

## Desarrollo

Las convenciones del proyecto están en [`CLAUDE.md`](CLAUDE.md): restricciones
del archivo único, reglas de migración de datos y criterios de verificación.
Léelo antes de tocar el esquema de `localStorage`.
