# Interactive HTML BOM

**Interactive HTML BOM** es uno de los plugins más útiles para la etapa de ensamblaje de PCBs. Genera un archivo HTML interactivo que muestra el PCB con todos los componentes, permitiendo marcarlos mientras se ensambla la placa.

---

## ¿Qué es el BOM?

El **BOM** (*Bill of Materials* — Lista de materiales) es un documento que lista todos los componentes utilizados en un proyecto PCB con su referencia, valor, footprint y cantidad.

---

## Características del plugin

- Visualización del PCB (cara frontal y posterior) directamente en el navegador.
- Filtrado y búsqueda de componentes por referencia, valor o footprint.
- **Resaltado interactivo**: al hacer clic en un componente del BOM, se marcal en el PCB y viceversa.
- Marcado de componentes soldados (muy útil durante el ensamblaje manual).
- Exportar como HTML estático — no requiere conexión a internet para usarse.
- Compatible con dispositivos móviles (táblet en la mesa de trabajo).

---

## Instalación

### Opción 1: Desde el PCM (recomendado)

1. Abre el **Plugin and Content Manager** desde el Project Manager.
2. Busca `Interactive HTML BOM`.
3. Haz clic en **Install**.
4. KiCad lo agregará al menú `Tools` del PCB Editor.

### Opción 2: Desde GitHub

1. Descarga el repositorio desde: `https://github.com/openscopeproject/InteractiveHtmlBom`
2. En el PCM: `Install from File...` y seleccion el `.zip` descargado.

---

## Uso del plugin

### Generar el HTML BOM

1. Abre el proyecto en el **PCB Editor**.
2. Ve a `Tools → Generate Interactive HTML BOM`.
3. Se abrirá la ventana de configuración del plugin.

### Configuración recomendada

| Opción | Valor recomendado |
|--------|------------------|
| **Board rotation** | 0° (o según orientación de fabricación) |
| **Highlight first pin** | Activado |
| **Include tracks** | Desactivado (reduce peso del archivo) |
| **Include zones** | Desactivado |
| **Show fabrication layer** | Activado |
| **Normalize field case** | Activado |
| **Extra fields** | Agrega campos como `PN`, `Supplier`, `Price` si los usas |
| **Output file** | Directorio del proyecto, nombre automático |

### Generar

Haz clic en **Generate BOM** (o el botón equivalente). Se abrirá automáticamente el archivo HTML en el navegador predeterminado.

---

## Interfaz del HTML BOM

```
┌─────────────────────────────────────────┐
│  Filtro:  [  buscar componente...  ]          │
├─────────────────────────────────────────┤
│  BOM Table         |   Visualización PCB      │
│  Ref | Value | Qty |   ┌───────────────┐    │
│  R1  | 10k   |  1  |   │   [PCB render]  │    │
│  R2  | 4.7k  |  1  |   │   con pads y    │    │
│  C1  | 100nF |  2  |   │   footprints    │    │
│  U1  | ESP32 |  1  |   └───────────────┘    │
└─────────────────────────────────────────┘
```

### Cómo usar durante el ensamblaje

1. Abre el archivo `.html` generado en un navegador (Chrome, Firefox, Edge).
2. No necesita internet — funciona completamente offline.
3. Haz clic en un componente de la tabla para resaltarlo en el PCB.
4. Marca el checkbox del componente cuando ya lo hayas soldado.
5. El estado del checkmark **se guarda en el mismo archivo HTML** (usando localStorage del navegador).

!!! tip "Uso en tableta"
    Copia el archivo HTML a una tableta o laptop de la mesa de trabajo. El HTML BOM funciona muy bien en pantallas táctiles para marcar componentes durante el ensamblaje manual.

!!! warning "No compa rtir el estado"
    El estado de los checkboxes se guarda en el **localStorage del navegador**, no en el archivo. Si abres el mismo archivo en otro navegador o equipo, los checks no aparecerán.

---

## Agregar campos personalizados al BOM

Puedes enriquecer el BOM agregando campos personalizados a los componentes en el esquemático:

| Campo sugerido | Descripción |
|---------------|-------------|
| `PN` | Part Number del fabricante |
| `Supplier` | Proveedor (DigiKey, Mouser, LCSC...) |
| `Supplier_PN` | Número de parte del proveedor |
| `Price` | Precio unitario referencial |
| `Description` | Descripción breve del componente |

Agrega estos campos en las propiedades del símbolo en el Schematic Editor y aparecerán como columnas adicionales en el HTML BOM.
