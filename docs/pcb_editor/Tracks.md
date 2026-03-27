# Pistas (Tracks)

Las **pistas** (*tracks*) son las líneas conductoras de cobre en el PCB que conectan los pads entre sí, formando las redes eléctricas definidas en el esquemático.

---

## Herramienta de enrutado interactivo

KiCad incluye un **enrutador interactivo** que:

- Evita automáticamente obstáculos (pads, otras pistas).
- Respeta las reglas de diseño (DRC en tiempo real).
- Ofrece modos de enrutado: recto, diagonal, con curvas.

### Activar el enrutador

- Presiona `X` para enrutado estándar (bends de 45°).
- O ve a `Route → Route Single Track`.

### Proceso de enrutado

1. Presiona `X`.
2. Haz clic en el pad de origen.
3. Mueve el cursor por la trayectoria deseada.
4. Haz clic para fijar puntos intermedios.
5. Haz clic en el pad de destino para completar la conexión.
6. La guía (*ratsnest*) desaparece al completar la conexión.

---

## Ancho de pista

El ancho de pista es crítico para la capacidad de corriente y los requisitos del proceso de fabricación.

### Anchos mínimos recomendados

| Aplicación | Ancho mínimo |
|------------|-------------|
| Señal lógica (SPI, I2C, GPIO) | 0.2 mm |
| Señal de comunicación (USB, alta velocidad) | 0.15 mm |
| Alimentación baja (< 500 mA) | 0.4 mm |
| Alimentación media (500 mA – 1 A) | 0.6 mm |
| Alimentación alta (1 A – 3 A) | 1.0 mm |
| Alimentación muy alta (> 3 A) | 2.0 mm o más |

!!! tip "Calculadora de ancho de pista"
    Usa `Tools → Net Inspector` y la calculadora integrada de KiCad (`Tools → Calculator Tools`) para calcular el ancho correcto según la corriente y la temperatura.

### Cambiar el ancho durante el enrutado

- Presiona `W` durante el enrutado para abrir el selector de ancho.
- O usa `+` / `-` para incrementar o decrementar el ancho según los perfiles predefinidos.

### Configurar anchos predefinidos

`File → Board Setup → Design Rules → Pre-defined Sizes`

Agrega los anchos que uses frecuentemente en JW Control, por ejemplo: `0.2`, `0.4`, `0.8`, `1.5`, `2.5` mm.

---

## Reglas de diseño (Design Rules)

Las reglas de diseño definen las restricciones físicas del PCB. Se configuran en:

`File → Board Setup → Design Rules → Constraints`

| Regla | Descripción | Valor típico |
|-------|-------------|-------------|
| **Minimum track width** | Ancho mínimo de pista | 0.15 mm |
| **Minimum clearance** | Distancia mínima entre objetos conductores | 0.2 mm |
| **Minimum via size** | Diámetro mínimo de via | 0.4 mm |
| **Minimum drill** | Diámetro mínimo de taladro | 0.3 mm |

!!! note "Fabricante"
    Las reglas deben ajustarse según las capacidades del fabricante de PCBs. Para **PCBway** (proveedor habitual de JW Control), las reglas estándar son:
    - Pista mínima: **0.1 mm**
    - Clearance mínimo: **0.1 mm**
    - Via mínima: **0.3 mm** de taladro, **0.6 mm** de pad externo

---

## Modo de enrutado

### Modos de esquina disponibles

Durante el enrutado, presiona `/` para cambiar el modo de curvatura:

| Modo | Descripción |
|------|-------------|
| **45°** | Esquinas de 45 grados (estándar) |
| **H/V** | Solo horizontal y vertical |
| **Curved** | Curvas suaves (mejor para alta frecuencia) |

### Enrutado diferencial

Para señales diferenciales (USB, Ethernet, etc.): `Route → Route Differential Pair`.

---

## Ratsnest (Guías de conexión pendiente)

El **ratsnest** son las líneas delgadas que indican conexiones del esquemático que aún no han sido enrutadas. Desaparecen al completar cada conexión.

- Para mostrar/ocultar el ratsnest: `View → Ratsnest`.
- El objetivo del enrutado es **eliminar todas las líneas del ratsnest**.

---

## Zonas de cobre (Copper Zones)

Las zonas de cobre llenan un área del PCB con cobre conectado a una red (normalmente `GND` o `VCC`).

### Crear una zona de GND

1. Presiona `Ctrl+Shift+Z` o ve a `Place → Zone`.
2. Se abrirá el diálogo de propiedades de zona:
   - Selecciona la capa (`F.Cu` o `B.Cu`).
   - Selecciona la red (`GND` o la que corresponda).
   - Configura clearance y mínimo de relleno.
3. Dibuja el perímetro de la zona.
4. Presiona `B` para rellenar todas las zonas (*Fill All Zones*).

!!! tip "Plano de GND"
    Es buena práctica en JW Control colocar un **plano de GND en B.Cu** (cara posterior). Esto reduce la impedancia de la alimentación, mejora el blindaje EMI y simplifica el enrutado de señales.

---

## DRC — Design Rule Check

Despues de enrutar, ejecuta el DRC para verificar que el diseño cumple todas las reglas:

`Inspect → Design Rules Checker`

Errores comunes y cómo resolverlos:

| Error | Causa probable | Solución |
|-------|---------------|----------|
| Clearance violation | Dos pistas muy cerca | Mover o redirigir una pista |
| Unconnected items | Conexiones sin enrutar | Completar el ratsnest |
| Courtyard overlap | Footprints superpuestos | Separar los componentes |
| Short circuit | Dos redes distintas conectadas | Verificar y corregir el enrutado |

---

## Atajos de teclado en PCB (resumen)

| Atajo | Acción |
|-------|--------|
| `X` | Enrutar pista |
| `V` | Colocar via (durante enrutado) |
| `W` | Seleccionar ancho de pista (durante enrutado) |
| `/` | Cambiar modo de esquina (durante enrutado) |
| `Esc` | Cancelar enrutado |
| `U` | Seleccionar pista conectada |
| `I` | Seleccionar pista completa |
| `B` | Rellenar todas las zonas de cobre |
| `Ctrl+B` | Borrar relleno de zonas |
| `3` | Vista 3D |
| `F8` | Actualizar desde esquemático |
