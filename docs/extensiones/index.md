# Extensiones y Plugins

KiCad permite ampliar sus funcionalidades mediante **plugins** (extensiones). Estos se gestionan a través del **Plugin and Content Manager (PCM)**, accesible desde el Project Manager.

---

## Plugin and Content Manager

### Acceder al PCM

Desde el **Project Manager**:

- Haz clic en el botón **Plugin and Content Manager**, o
- `Tools → Plugin and Content Manager`.

### Instalar un plugin

1. Abre el PCM.
2. En la pestaña **Plugins**, busca el plugin deseado.
3. Haz clic en **Install** junto al plugin.
4. Reinicia KiCad si se solicita.

### Instalar desde archivo

Algunos plugins se distribuyen como archivos `.zip`. Para instalarlos:

1. Descarga el archivo `.zip` del plugin.
2. En el PCM: `Install from File...`.
3. Selecciona el archivo `.zip`.

---

## Plugins recomendados en JW Control

| Plugin | Funcionalidad |
|--------|---------------|
| [Interactive HTML BOM](InteractiveHtmlBom.md) | Genera un BOM interactivo en HTML con visualización del PCB |
| [PCBway](pcbway.md) | Envío directo del proyecto a PCBway para cotización y fabricación |

---

## Consideraciones generales

!!! tip "Compatibilidad"
    Verifica que el plugin es compatible con tu versión de KiCad antes de instalarlo. Los plugins del PCM oficial generalmente están actualizados para la versión más reciente.

!!! note "Scripts de Python"
    Muchos plugins de KiCad están escritos en **Python**. KiCad incluye su propio intérprete de Python embebido, por lo que no necesitas instalar Python por separado para ejecutarlos.
