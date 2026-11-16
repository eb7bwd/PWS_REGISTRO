# Datos de la estación meteorológica EB7BWD

Datos registrados por la estación meteorológica personal **EB7BWD**
(identificador **ICHICL111** en Weather Underground), situada en **Chiclana de la Frontera, Andalucía**
(36.420°N, 6.156°W). Las horas están en hora local de ****, con el cambio
de hora de verano incluido.

Última actualización: 17/11/2026 00:03.

Si reutilizas estos datos, cita la fuente: *Estación meteorológica EB7BWD (PWS ICHICL111)*.

## Organización de los archivos

```
datos/
├── README.md                     este documento
├── resumen_diario_2026.csv       una fila por día (lo más cómodo para analizar)
└── 2026/
    └── 07/
        ├── 01.csv                registros del 1 de julio, cada ~5 minutos
        └── 02.json               solo resumen del 2 de julio (si ese día no hay registros)
```

- **`AAAA/MM/DD.csv`**: todos los registros del día, aproximadamente uno cada 5 minutos.
- **`AAAA/MM/DD.json`**: solo los máximos, mínimos y medias del día. Existe únicamente cuando
  ese día no hay registros detallados.
- **`resumen_diario_AAAA.csv`**: una fila por día con los valores principales, en números
  sin unidades. Es el fichero recomendado para hojas de cálculo y gráficas propias.
- El día en curso no se publica hasta que termina.

## Ficheros detallados (`DD.csv`)

Cada fila resume un intervalo de unos 5 minutos que termina a la hora indicada.
Los valores llevan la unidad escrita junto al número (por ejemplo `21.4°C`).

| Columna | Significado | Unidad | Ejemplo |
|---|---|---|---|
| `Time` | Hora local, en formato de 12 horas | — | `3:45 PM` |
| `Temperature` | Temperatura media del intervalo | °C | `21.4°C` |
| `Dew Point` | Punto de rocío (temperatura a la que el aire se saturaría) | °C | `14.2°C` |
| `Humidity` | Humedad relativa media | % | `65 %` |
| `Wind` | Dirección **desde la que sopla** el viento (rosa de 16 rumbos, en inglés) | — | `NNE` |
| `Speed` | Velocidad media del viento | km/h | `12.3 km/h` |
| `Gust` | Racha más fuerte del intervalo | km/h | `25.1 km/h` |
| `Pressure` | Presión atmosférica, tal como la envía la estación | hPa | `1016.4 hPa` |
| `Precip. Rate.` | Intensidad de la lluvia en ese momento (aunque ponga `mm`, son **mm/h**) | mm/h | `2.4 mm` |
| `Precip. Accum.` | Lluvia acumulada desde las 00:00 | mm | `5.8 mm` |
| `UV` | Índice ultravioleta máximo del intervalo | — | `7` |
| `Solar` | Radiación solar máxima del intervalo | W/m² | `845 w/m²` |

Cómo leerlos:

- **`--`** significa que no hay dato en ese intervalo (sensor sin lectura o viento en calma).
- La **lluvia total del día** es el último valor de `Precip. Accum.`, no la suma de la columna.
- Rumbos del viento: `N` norte, `E` este, `S` sur, `W` oeste (*west*). Por ejemplo, `WSW` es
  oeste-suroeste.
- **Cambio de hora**: el último domingo de octubre la franja de 2:00 a 3:00 aparece dos veces, y
  el último domingo de marzo esa franja no existe.
- En los ficheros más antiguos la humedad puede aparecer como `85 °%`; significa 85 %.

## Ficheros de resumen (`DD.json`)

Contienen los máximos (`high`), mínimos (`low`) y medias (`average`) del día:

```json
{
  "date": "2026-07-02",
  "type": "summary_only",
  "data": {
    "Temperature":   {"high": "31.2 °C", "low": "19.8 °C", "average": "24.9 °C"},
    "Humidity":      {"high": "88 %",    "low": "35 %",    "average": "61 %"},
    "Pressure":      {"high": "1016.1 hPa", "low": "1011.9 hPa", "average": "1014.0 hPa"},
    "Wind Speed":    {"high": "24.1 km/h", "low": "0.0 km/h", "average": "8.2 km/h"},
    "Wind Gust":     {"high": "38.6 km/h", "low": "--", "average": "--"},
    "Precipitation": {"high": "3.2 mm", "low": "--", "average": "--"}
  }
}
```

- `Precipitation` → `high` es la lluvia total del día.
- Los mismos datos aparecen repetidos con las claves `fecha` / `datos` por compatibilidad con
  versiones anteriores del programa.
- Algunos ficheros antiguos tienen los valores en unidades imperiales (`°F`, `mph`, `in`). Para
  convertirlos:
  - °C = (°F − 32) × 5 ⁄ 9
  - km/h = mph × 1,609
  - hPa = inHg × 33,864
  - mm = pulgadas × 25,4

## Resumen diario anual (`resumen_diario_AAAA.csv`)

Una fila por día con números sin unidades. El separador es la coma y el decimal, el punto.
Una celda vacía significa que ese día no hay ese dato.

| Columna | Significado | Unidad |
|---|---|---|
| `fecha` | Fecha (AAAA-MM-DD) | — |
| `tipo` | «detallado» si hay registros cada 5 min; «resumen» si solo hay máximos/mínimos del día | — |
| `temp_max` | Temperatura máxima | °C |
| `temp_min` | Temperatura mínima | °C |
| `temp_media` | Temperatura media | °C |
| `punto_rocio_medio` | Punto de rocío medio | °C |
| `humedad_max` | Humedad relativa máxima | % |
| `humedad_min` | Humedad relativa mínima | % |
| `humedad_media` | Humedad relativa media | % |
| `presion_max` | Presión máxima | hPa |
| `presion_min` | Presión mínima | hPa |
| `presion_media` | Presión media | hPa |
| `viento_medio` | Velocidad media del viento | km/h |
| `viento_max` | Velocidad media más alta del día | km/h |
| `racha_max` | Racha máxima | km/h |
| `precipitacion` | Lluvia total del día | mm |
| `uv_max` | Índice UV máximo | — |
| `radiacion_max` | Radiación solar máxima | W/m² |
| `amanecer` | Hora del amanecer (cálculo astronómico, hora local) | HH:MM |
| `atardecer` | Hora del atardecer (cálculo astronómico, hora local) | HH:MM |
| `horas_luz` | Duración del día, del amanecer al atardecer | horas |
| `horas_sol` | Horas de sol registradas (radiación > 120 W/m², aproximación) | horas |

Las horas de luz y de sol van en horas decimales: `14.50` son 14 horas y 30 minutos.

## Cómo abrir los datos

**Excel o LibreOffice Calc**: usa *Datos → Desde texto/CSV* (Excel) o abre el fichero directamente
(LibreOffice), elige la **coma** como separador y el idioma **Inglés (EE. UU.)** para que el punto
se lea como decimal.

**Python (pandas)**:

```python
import pandas as pd

# Resumen diario de un año
resumen = pd.read_csv("resumen_diario_2026.csv", parse_dates=["fecha"])
print(resumen[["fecha", "temp_max", "temp_min", "precipitacion"]].head())

# Registros de un día: hay que quitar las unidades de cada valor
dia = pd.read_csv("2026/07/01.csv")
dia["Temperature"] = dia["Temperature"].str.extract(r"(-?\d+\.?\d*)", expand=False).astype(float)
```

## Calidad de los datos

Son datos brutos de una estación personal, sin el control de calidad de un servicio meteorológico
oficial. Puede haber huecos (cortes de conexión o de corriente) y, ocasionalmente, lecturas
anómalas de algún sensor. Las horas de sol son una aproximación calculada a partir de un sensor
de radiación global, no de un heliógrafo.
