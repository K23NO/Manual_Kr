# PCB Editor

El **PCB Editor** de KiCad es la herramienta donde se diseña el circuito impreso (PCB) a partir del esquemático. En esta etapa se define:

- La posición físcica de los componentes (footprints).
- El enrutamiento de las pistas (tracks) entre los pads.
- Las capas del PCB (cobre, serigrafa, máscara de soldadura).
- El contorno físico de la placa (board outline).
- Las reglas de diseño (DRC — Design Rule Check).

---

## Acceder al PCB Editor

Desde el **Project Manager**:

- Haz clic en el botón **PCB Editor**, o
- Haz doble clic en el archivo `.kicad_pcb`.

---

## Interfaz principal

```
┌────────────────────────────────────────┐
│  Barra de menú: File / Edit / View / Route... │
├────────────────────────────────────────┤
│  Barra lateral: selector de capas y herramientas│
├────────────────────────────────────────┤
│  Área de diseño (canvas 3D/2D)               │
├────────────────────────────────────────┤
│  Panel de propiedades (derecha, opcional)      │
└────────────────────────────────────────┘
```

---

## Capas principales del PCB

| Capa | Nombre en KiCad | Descripción |
|------|----------------|-------------|
| Cobre superior | `F.Cu` | Pistas y pads en la cara frontal |
| Cobre inferior | `B.Cu` | Pistas y pads en la cara posterior |
| Serigrafía frontal | `F.Silkscreen` | Textos e íconos impresos en la placa (cara frontal) |
| Serigrafía posterior | `B.Silkscreen` | Textos e íconos en la cara posterior |
| Máscara de soldadura frontal | `F.Mask` | Protección de cobre (verde, azul, etc.) |
| Máscara de soldadura posterior | `B.Mask` | Protección posterior |
| Pasta de soldadura | `F.Paste` / `B.Paste` | Para stencil de pasta de soldar |
| Contorno | `Edge.Cuts` | Contorno físico de la placa |
| Documentación | `F.Fab` / `B.Fab` | Información para fabricación |
| Cortesa | `F.Courtyard` / `B.Courtyard` | Espacio reservado del componente (DRC) |

---

## Flujo de trabajo en el PCB Editor

```
[1. Importar esquemático] → [2. Definir contorno] → [3. Colocar componentes]
         ↓
[6. Exportar Gerbers] ← [5. Ejecutar DRC] ← [4. Enrutar pistas]
```

### 1. Importar el esquemático

Despues de completar el esquemático:

1. En el PCB Editor: `Tools → Update PCB from Schematic` (`F8`).
2. Confirma los cambios en el diálogo.
3. Los footprints aparecerán apilados en el área de trabajo.

### 2. Definir el contorno (Board Outline)

1. Selecciona la capa `Edge.Cuts` en el panel de capas.
2. Usa `Place → Line` o `Rectangle` para dibujar el perímetro de la placa.

!!! warning "Edge.Cuts"
    El contorno **debe ser una figura cerrada y continua** en `Edge.Cuts`. Cualquier abertura causará errores en fabricación.

### 3. Colocar componentes

- Arrastra y rota los footprints a sus posiciones finales.
- Usa `R` para rotar y `F` para voltear al lado posterior del PCB.
- Agrupa los componentes relacionados.

### 4. Enrutar pistas

- Presiona `X` para activar el enrutador interactivo.
- Haz clic en un pad para iniciar una pista.
- Las guias de color (*ratsnest*) muestran las conexiones pendientes.
- Las pistas enrutadas eliminan la guía de ratsnest.

### 5. Ejecutar DRC

`Inspect → Design Rules Checker` — Verifica distancias mínimas, pistas sin terminar, etc.

### 6. Exportar Gerbers

`File → Fabrication Outputs → Gerbers (.gbr)`

---

## Atajos de teclado esenciales en PCB

| Atajo | Acción |
|-------|--------|
| `X` | Enrutar pista |
| `R` | Rotar footprint |
| `F` | Voltear al lado posterior |
| `G` | Arrastrar pista/footprint |
| `E` | Editar propiedades |
| `U` | Seleccionar pista completa |
| `Del` | Eliminar objeto |
| `+` / `-` | Aumentar/reducir ancho de pista (durante enrutado) |
| `D` | Interactivo: esquivar obstáculos |
| `F8` | Actualizar PCB desde esquemático |
| `3` | Vista 3D |
