# Conexiones (Wiring)

Esta sección explica cómo conectar los componentes del esquemático usando cables, buses, etiquetas de red y otros elementos de conexión.

---

## Cables (Wires)

El cable es la forma más directa de conectar dos pines.

### Dibujar un cable

1. Presiona `W` para activar la herramienta de cable.
2. Haz clic en el punto de inicio (generalmente un pin de componente).
3. Mueve el puntero hacia el punto de destino.
4. Haz clic para fijar el cable.
5. Haz clic en el pin de destino para terminar la conexión.
6. Presiona `Esc` para salir del modo cable.

!!! tip "Conexión automática"
    Cuando un cable llega exactamente al pin de un componente, KiCad lo conecta automáticamente. Un punto verde en el extremo del cable indica que la conexión es válida.

### Punto de unión (Junction)

Cuando tres o más cables se cruzan en el mismo punto, KiCad necesita un **junction** para confirmar que se conectan entre sí:

- Un cable que cruza a otro cable **no significa conexión** a menos que haya un junction.
- Presiona `J` o ve a `Place → Add Junction` para colocar un punto de unión.

```
        |              |  ● ← Junction
  ------+------  vs.  --+--   (conectados)
        |              |          
   (cruce sin           
   conectar)
```

---

## Etiquetas de red (Net Labels)

Las etiquetas de red son la forma más limpia de conectar pines que están físicamente separados en el esquemático, **sin necesidad de dibujar un cable largo**.

### Agregar una etiqueta

1. Presiona `L` o ve a `Place → Net Label`.
2. Escribe el nombre de la red (ej.: `TX`, `RX`, `CLK`, `DATA`, `EN`).
3. Haz clic en el pin donde quieres colocarla.

Dos pines con la **misma etiqueta** están eléctricamente conectados, sin importar dónde estén en el esquemático.

!!! tip "Buena práctica"
    Usa nombres descriptivos para las etiquetas: `UART_TX`, `I2C_SDA`, `PWM_OUT`, etc. Esto hace el esquemático mucho más legible.

---

## Etiquetas globales (Global Labels)

Similares a las etiquetas de red, pero conectan redes **entre diferentes hojas** del esquemático (cuando el diseño tiene múltiples hojas).

- `Place → Global Label`
- Especifica la dirección: Input, Output, Bidirectional.

---

## Buses

Un **bus** agrupa múltiples señales visualmente en una sola línea gruesa para simplificar el esquemático.

### Dibujar un bus

1. `Place → Bus` o atajo `B`.
2. Dibuja la línea de bus.

### Conectar señales al bus

1. `Place → Bus Wire Entry` o atajo `Z` para agregar ramales al bus.
2. Conecta un cable desde el pin del componente al ramal (`/`).
3. Coloca una etiqueta de red en cada ramal con el nombre de la señal (ej.: `D0`, `D1`, `D2`...).

!!! note "Buses en KiCad"
    En KiCad, los buses son principalmente decorativos/visuales. Las conexiones reales se establecen a través de las etiquetas de red. El bus ayuda a clarificar el esquemático pero no crea automáticamente conexiones eléctricas.

---

## Texto anotativo

Puedes agregar texto de referencia que **no** crea conexiones eléctricas:

- `Place → Text` o atajo `T`: agrega texto descriptivo al esquemático.
- Ideal para comentarios, notas de diseño, o describir bloques funcionales.

---

## ERC — Electrical Rules Check

El **ERC** verifica que el esquemático no tenga errores eléctricos como:

- Pines sin conectar (*unconnected pins*).
- Redes sin fuente de alimentación.
- Salidas conectadas entre sí.
- Referencias duplicadas.

### Ejecutar el ERC

1. Ve a `Inspect → Electrical Rules Checker`, o presiona `F5`.
2. Haz clic en **Run ERC**.
3. Revisa los errores y advertencias.
4. Haz clic en cada entrada para navegar al problema en el lienzo.

### Tipos de marcadores

| Color | Tipo |
|-------|------|
| Rojo | Error (debe corregirse) |
| Amarillo | Advertencia (evaluar si aplica) |

!!! warning "ERC antes de exportar"
    Siempre ejecuta el ERC y corrije todos los errores antes de actualizar el PCB o generar netlists.

---

## Resumen de atajos de wiring

| Atajo | Acción |
|-------|--------|
| `W` | Dibujar cable |
| `B` | Dibujar bus |
| `Z` | Agregar entrada de bus (bus wire entry) |
| `J` | Colocar junction (punto de unión) |
| `L` | Agregar etiqueta de red |
| `P` | Agregar símbolo de potencia |
| `T` | Agregar texto |
| `Esc` | Cancelar operación actual |
| `F5` | Ejecutar ERC |
