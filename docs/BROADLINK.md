# Aprender los códigos IR en el Broadlink

SmartIR se encarga de lo básico (encender, modo, temperatura, ventilador). El resto de botones del panel
envían códigos que tú aprendes una vez con el Broadlink, todos bajo el **dispositivo `Haier`**.

## Comandos que usa el panel

| Comando | Botón del panel | Usado en scripts |
|---|---|---|
| `swing_vertical` | Dirección del aire → Vertical | Turbo Frío, Ventilar |
| `swing_horizontal` | Dirección del aire → Horizontal | Turbo Frío, Ventilar |
| `turbo` | Turbo | Turbo Frío |
| `eco` | ECO | ECO |
| `quiet` | Silencio | Dormir |
| `sleep` | Más opciones → Sleep | Dormir |
| `health` | Más opciones → Health | — |
| `i_feel` | I Feel | — |
| `self_clean` | Anti-Moho | — |
| `uv_frio_noche_baja` | — | UV + Frío |

> **Truco `uv_frio_noche_baja`:** en el mando, deja el aire como quieres (frío 22 °C, velocidad baja,
> Health/UV y modo noche) y aprende **ese** botón final como un único código. Así se envía todo de una vez,
> con un solo pitido y sin que un comando pise al anterior.

## Cómo aprender un comando

1. **Herramientas para desarrolladores → Acciones**.
2. Elige **Remote: Learn command** (`remote.learn_command`) y pasa a modo YAML:

   ```yaml
   action: remote.learn_command
   target:
     entity_id: remote.TU_BROADLINK
   data:
     device: Haier
     command: turbo
   ```

3. Pulsa **Realizar acción**. Aparece una notificación: apunta el mando original al Broadlink y pulsa el
   botón **Turbo** antes de 30 segundos.
4. Repite cambiando `command:` para cada fila de la tabla.

Para aprender varios seguidos:

```yaml
action: remote.learn_command
target:
  entity_id: remote.TU_BROADLINK
data:
  device: Haier
  command:
    - swing_vertical
    - swing_horizontal
    - eco
    - quiet
    - sleep
```

## Probar un comando

```yaml
action: remote.send_command
target:
  entity_id: remote.TU_BROADLINK
data:
  device: Haier
  command: turbo
```

## Si usas otro nombre de dispositivo

Si aprendiste los códigos con otro `device` (por ejemplo `Aire`), busca `device: Haier` en el panel y en
los scripts y cámbialo.

## Ver o borrar códigos aprendidos

Se guardan en `/config/.storage/broadlink_remote_XXXXXXXX_codes`. Para borrar uno:

```yaml
action: remote.delete_command
target:
  entity_id: remote.TU_BROADLINK
data:
  device: Haier
  command: turbo
```
