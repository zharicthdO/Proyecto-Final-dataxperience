# Proyecto-Final-dataxperience
# Predicción de la Salud de una Batería según sus Ciclos de Carga

Proyecto Final Dataxperience, aplicado a Ingeniería Mecatrónica. La idea es
la siguiente: **¿puedo saber qué tan sana está la batería de un robot o un dron, solo sabiendo
cuántos ciclos de carga lleva?** Si es asi, puedo anticipar cuándo va a necesitar reemplazo,
antes de que falle en plena misión.

## Los datos

No tenía forma de cargar y descargar una batería real cientos de veces para medir su
desgaste, así que **inventé los datos**, cada ciclo de carga le quita
un poco de salud a la batería, de forma bastante pareja, con algo de variación al azar, en
un rango de hasta 600 ciclos. También agregué a propósito 25 casos de `descarga_profunda`
(cuando la batería se descarga por debajo de un nivel seguro), que desgastan la batería más
rápido de lo normal. Todo el proceso está documentado en `scripts/generar_datos.py`.

## Resumen del proyecto

**Etapa 1 — Preparar los datos:** dataset simulado, transparencia total; sin
datos faltantes ni repetidos (verificado); 260 registros en total: 235 de uso normal y 25 de
descarga profunda, separados desde el inicio.

**Etapa 2 — Explorar los datos:** los ciclos de carga y la salud de la batería están bastante
relacionados (-0.87 en general, -0.97 si se quitan los casos de descarga profunda). El
gráfico de dispersión deja ver claramente esos casos; el diagrama de caja de solo los
ciclos, en cambio, no los detecta.

**Etapa 3 — El modelo:**

| Fórmulacion encontrada | `Salud ≈ -0.055 × Ciclos + 99.96` |
| Qué tan bien explica los datos (R²) | 0.96 |
| Margen de error típico | ≈ 2 puntos de salud |

Con este modelo, una batería en uso normal llega al 80% de salud (umbral típico de
reemplazo) alrededor del **ciclo 365**. El modelo se entrenó solo con los datos de uso
normal, dejando aparte los de descarga profunda.

**Para qué sirve:** permite anticipar cuándo una batería de un robot o dron va a necesitar
reemplazo, planeando el mantenimiento antes de que falle en plena operación — la base del
mantenimiento preventivo. Detalle completo en el notebook.

## Autor

Proyecto Final Dataxperience · Zharicth Dayan Lopez Lozano · Ingeniería Mecatrónica · Universidad EAN
