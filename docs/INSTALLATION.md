# Instalación paso a paso

Tiempo aproximado: 20–30 minutos (la mayor parte es aprender los códigos IR).

## 1. Instala las dependencias desde HACS

1. **HACS → Frontend** → busca **button-card** → Descargar.
2. **HACS → Integraciones** → busca **SmartIR** → Descargar → reinicia Home Assistant.
3. Recarga el navegador con **Ctrl+F5** (o borra la caché de la app móvil).

## 2. Configura el Broadlink y SmartIR

1. **Ajustes → Dispositivos y servicios → Añadir integración → Broadlink** y sigue el asistente.
   Se crea una entidad `remote.xxx` (por ejemplo `remote.rm4_mini`).
2. Configura tu aire en SmartIR (en `configuration.yaml`), por ejemplo:

   ```yaml
   smartir:

   climate:
     - platform: smartir
       name: Aire Dormitorio
       unique_id: aire_dormitorio
       device_code: 1180                # EJEMPLO: pon el código de tu modelo
       controller_data: remote.TU_BROADLINK
       temperature_sensor: sensor.TU_TEMPERATURA   # opcional
       humidity_sensor: sensor.TU_HUMEDAD           # opcional
       power_sensor: switch.TU_ENCHUFE              # opcional
   ```

   Busca el `device_code` de tu modelo en la
   [lista de SmartIR](https://github.com/smartHomeHub/SmartIR/blob/master/docs/CLIMATE.md).
3. Reinicia y comprueba que aparece la entidad `climate.xxx`.

## 3. Aprende los códigos IR extra

SmartIR ya envía modo, temperatura y ventilador. Las funciones extra (turbo, eco, silencio…) se aprenden
en el Broadlink. Sigue **[BROADLINK.md](BROADLINK.md)**.

## 4. Copia la imagen

Copia `www/haier/haier_split_dashboard.png` a `/config/www/haier/haier_split_dashboard.png`
(con el complemento *File editor*, *Samba share* o *Studio Code Server*).

> Si la carpeta `/config/www` no existía, **reinicia Home Assistant** para que sirva `/local/`.

Puedes usar una foto de tu propio aparato: guárdala con el mismo nombre, mejor en PNG con fondo
transparente y unos 570×280 px.

## 5. Añade los scripts

1. Abre `/config/scripts.yaml`.
2. Pega al final el contenido de [`scripts/haier_scripts.yaml`](../scripts/haier_scripts.yaml).
3. Sustituye `climate.TU_AIRE` y `remote.TU_BROADLINK`.
4. **Herramientas para desarrolladores → YAML → Recargar scripts.**

## 6. Crea el panel

1. **Ajustes → Paneles → Añadir panel → Nuevo panel desde cero**. Nombre: *Haier Premium*.
2. Ábrelo → lápiz ✏️ → menú ⋮ → **Editor de configuración en bruto**.
3. Borra lo que haya y pega el contenido de [`dashboard/haier-premium.yaml`](../dashboard/haier-premium.yaml).
4. Usa **Ctrl+F / Buscar y reemplazar** para cambiar los marcadores (ver [ENTITIES.md](ENTITIES.md)).
5. Guarda.

¿Prefieres añadirlo como una pestaña de un panel que ya tienes? Copia solo lo que hay debajo de
`views:` (desde `- type: sections`) y pégalo dentro de la lista `views:` de tu panel.

## 7. Personaliza

- **Nombre**: busca `Aire Dormitorio` en la cabecera.
- **Ficha del equipo**: cambia `TU-MODELO`, `TU-NUMERO-DE-SERIE` y las fechas (o borra esas líneas).
- **Marca**: cambia `<div class="brand">Haier</div>` si tu aire es de otra marca.
- **Avisos de consumo**: cambia `1500` y `800` (W) en la tarjeta de energía.
- **Sin enchufe con medición**: borra la tarjeta que empieza por `entity: switch.TU_ENCHUFE`.
- **Programación**: la tarjeta «Programación» es informativa (texto fijo). Edita el texto o bórrala.
