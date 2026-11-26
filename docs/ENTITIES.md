# Entidades que tienes que sustituir

Abre `dashboard/haier-premium.yaml` y `scripts/haier_scripts.yaml` y usa **Buscar y reemplazar** con cada fila.

| Marcador | Qué poner | De dónde sale | ¿Obligatorio? |
|---|---|---|---|
| `climate.TU_AIRE` | Tu entidad climate, p. ej. `climate.aire_dormitorio` | SmartIR | ✅ Sí |
| `remote.TU_BROADLINK` | Tu mando IR, p. ej. `remote.rm4_mini` | Integración Broadlink | ✅ Sí |
| `switch.TU_ENCHUFE` | Enchufe que alimenta el aire | Tapo, Shelly, Sonoff… | Opcional |
| `sensor.TU_CONSUMO_ACTUAL` | Potencia en **W** | El mismo enchufe | Opcional |
| `sensor.TU_CONSUMO_HOY` | Energía de hoy en **kWh** | El mismo enchufe | Opcional |
| `sensor.TU_CONSUMO_MES` | Energía del mes en **kWh** | El mismo enchufe | Opcional |

Además, en la cabecera:

| Texto | Cámbialo por |
|---|---|
| `TU-MODELO` | El modelo de tu unidad interior |
| `TU-NUMERO-DE-SERIE` | El número de serie (o borra la línea) |
| `1 ene 2025` (×2) | Fechas de compra y registro (o borra las líneas) |

## Cómo encontrar el ID de una entidad

**Ajustes → Dispositivos y servicios → Entidades**, busca el aparato y copia el **ID de entidad**.

## Atributos que usa el panel

La entidad `climate` debe tener estos atributos (SmartIR los crea):

- `temperature` (temperatura objetivo), `current_temperature`, `current_humidity`
- `fan_mode` con los valores `low`, `mid`, `high`, `auto`
- modos `off`, `cool`, `heat`, `dry`, `fan_only`

Si tu modelo usa otros nombres de velocidad (por ejemplo `medium` en vez de `mid`), cámbialos en las
tarjetas de ventilador y en los scripts.

`current_temperature` y `current_humidity` solo aparecen si indicaste `temperature_sensor` y
`humidity_sensor` en SmartIR. Si no, el panel mostrará `--`.
