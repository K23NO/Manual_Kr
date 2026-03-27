# Componentes y Símbolos

En KiCad, un **símbolo** (*symbol*) es la representación gráfica de un componente electrónico dentro del esquemático. Cada símbolo tiene pines que representan las conexiones eléctricas del componente.

!!! note "Símbolo vs. Footprint"
    El **símbolo** representa el componente en el esquemático (diagrama lógico).  
    El **footprint** representa el componente en el PCB (dimensiones físicas y pads).  
    Son dos cosas distintas y ambas deben asignarse correctamente.

---

## Propiedades de un símbolo

Cada símbolo tiene los siguientes campos principales:

| Campo | Descripción |
|-------|-------------|
| **Reference** | Identificador único del componente (ej.: `R1`, `C3`, `U5`) |
| **Value** | Valor o nombre del componente (ej.: `10k`, `100nF`, `ATmega328`) |
| **Footprint** | Huella PCB asignada (ej.: `Resistor_SMD:R_0805`) |
| **Datasheet** | URL o ruta al datasheet del fabricante |
| Campos adicionales | PN fabricante, proveedor, precio, etc. (personalizables) |

---

## Tipos de componentes comunes

### Activos
- Microcontroladores (ATmega, STM32, ESP32...)
- Transistores BJT y MOSFET
- Amplificadores operacionales
- Reguladores de voltaje
- Drivers y puentes H

### Pasivos
- Resistencias (`R`)
- Condensadores (`C`)
- Inductores (`L`)
- Transformadores

### Conectores
- Conectores de cabezal (*pin headers*)
- Conectores USB, RJ45, JST
- Terminales de tornillo

### Símbolos de potencia
- `VCC`, `+3.3V`, `+5V`, `+12V`
- `GND`, `PWR_FLAG`

---

## Referencias estándar

KiCad asigna prefijos de referencia según el tipo de componente:

| Prefijo | Tipo |
|---------|------|
| `R` | Resistencia |
| `C` | Condensador |
| `L` | Inductor |
| `D` | Diodo |
| `Q` | Transistor |
| `U` | Circuito integrado |
| `J` | Conector |
| `SW` | Interruptor |
| `F` | Fusible |
| `T` | Transformador |
| `Y` | Cristal / Oscilador |
| `TP` | Test point |

---

## Editar propiedades de un símbolo

1. Haz doble clic sobre el símbolo en el esquemático, o
2. Seléccionalo y presiona `E`.

Se abrirá el diálogo **Symbol Properties** donde puedes editar todos los campos.

!!! tip "Numeración automática"
    Puedes usar `Tools → Annotate Schematic` para numerar automáticamente todos los componentes (`R1`, `R2`, `C1`, `C2`, etc.).

---

## Librerías de símbolos

KiCad incluye una extensa librería estándar con miles de componentes. Las librerías se gestionan desde:

`Preferences → Manage Symbol Libraries`

Existen dos niveles de librerías:

- **Global libraries:** disponibles para todos los proyectos.
- **Project libraries:** exclusivas del proyecto actual (reacomendadas para símbolos personalizados).

### Librerías destacadas

| Librería | Contenido |
|----------|-----------|
| `Device` | Componentes genéricos (R, C, L, etc.) |
| `Connector` | Conectores estándar |
| `MCU_Microchip_ATmega` | Microcontroladores Atmel |
| `MCU_ST_STM32*` | Familia STM32 |
| `RF_Module` | Módulos WiFi, Bluetooth |
| `Regulator_Linear` | Reguladores LDO |
| `Sensor_*` | Sensores varios |

---

## Crear un símbolo personalizado

Si un componente no está en las librerías estándar:

1. Abre el **Symbol Editor** (`Tools → Symbol Editor`).
2. Crea una nueva librería de proyecto o usa una existente.
3. Haz clic en `File → New Symbol`.
4. Dibuja el cuerpo del símbolo y agrega los pines con sus nombres y números.
5. Asigna propiedades (Reference, Value, Footprint, Datasheet).
6. Guarda.

!!! warning "Símbolos personalizados"
    Guarda los símbolos personalizados en la librería del **proyecto** (no en la librería global) para que el archivo sea portable entre equipos.
