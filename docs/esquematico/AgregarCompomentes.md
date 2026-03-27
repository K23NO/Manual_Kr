# Agregar Componentes al Esquemático

Esta sección explica cómo buscar y colocar componentes (símbolos) en el esquemático de KiCad.

---

## Abrir el buscador de símbolos

Existen tres formas de abrir el diálogo **Add Symbol**:

1. Presiona la tecla `A`.
2. Ve a `Place → Add Symbol`.
3. Haz clic en el ícono de componente en la barra de herramientas.

Se abrirá la ventana **Choose Symbol**.

---

## Ventana "Choose Symbol"

La ventana tiene tres secciones principales:

1. **Campo de búsqueda** (arriba): escribe el nombre o valor del componente.
2. **Lista de resultados** (izquierda): muestra librerías y símbolos coincidentes.
3. **Vista previa** (derecha): muestra el símbolo seleccionado y sus pines.

### Búsqueda eficiente

| Ejemplo de búsqueda | Encuentra |
|--------------------|----------|
| `R` | Resistencias genéricas |
| `10k` | Resistencias con valor 10k |
| `ATmega328` | Microcontrolador ATmega328P |
| `LM7805` | Regulador de voltaje 7805 |
| `NE555` | Timer NE555 |
| `USB_B` | Conector USB tipo B |
| `GND` | Símbolo de tierra |

!!! tip "Filtro de palabras clave"
    El buscador es muy potente: puedes escribir fragmentos del nombre, valor o descripción del componente.

---

## Colocar un símbolo

1. Escribe el nombre del componente en el campo de búsqueda.
2. Selecciona el símbolo deseado en la lista.
3. Haz clic en **OK**.
4. El cursor cambiará y mostrará el símbolo "enganchado" al puntero.
5. Haz clic en el lienzo para colocarlo.
6. Puedes seguir colocando copias del mismo símbolo hasta presionar `Esc`.

---

## Operaciones básicas con símbolos

### Mover un símbolo

- Selecciona el símbolo y arrástralo con el ratón.
- O usa la tecla `G` para arrastrarlo manteniendo las conexiones de cable.

!!! note "G vs. M"
    `G` (Grab) arrastra el símbolo **arrastrando los cables conectados** a él.  
    `M` (Move) mueve el símbolo **dejando los cables fixed** (puede desconectarlos).  
    En la mayoría de casos, usa `G`.

### Rotar un símbolo

- `R` rota 90° en sentido antihorario mientras lo colocas o cuando está seleccionado.

### Reflejar un símbolo

- `X` refleja horizontal.
- `Y` refleja vertical.

### Duplicar un símbolo

- Selecciona el símbolo y presiona `Ctrl+D`.

### Eliminar un símbolo

- Selecciona el símbolo y presiona `Del`.

---

## Agregar símbolos de potencia (VCC, GND)

Los símbolos de potencia son símbolos especiales que definen redes de alimentación.

Para colocarlos:

1. Presiona `P` (Power symbol), o
2. Ve a `Place → Add Power Port`.
3. Busca el nombre de la red de poder: `VCC`, `+5V`, `+3.3V`, `+12V`, `GND`, `GNDD`, etc.

!!! tip "¿Por qué usar símbolos de potencia?"
    Los símbolos de potencia permiten conectar visualmente las redes de alimentación a todos los componentes del esquemático sin necesidad de dibujar un cable físico entre ellos. Hacen el esquemático más legible.

### PWR_FLAG

Es buena práctica colocar un símbolo `PWR_FLAG` en las redes de poder (`VCC`, `GND`). Esto evita el error del ERC: *"Power pin not driven"*.

```
Colocar un PWR_FLAG conectado a GND y otro a VCC.
```

---

## Editar propiedades del símbolo

Despues de colocar un símbolo, edita sus propiedades:

1. Doble clic en el símbolo (o seleccionar y presionar `E`).
2. En la ventana **Symbol Properties**:
   - Actualiza el campo **Value** (ej.: cambiar `R` por `10k`).
   - Asigna el **Footprint** si ya lo conoces.
   - Agrega el **Datasheet** (URL al PDF del componente).
3. Haz clic en **OK**.

---

## Anotación automática

Despues de colocar todos los componentes, numeralos automáticamente:

1. `Tools → Annotate Schematic`.
2. Elige el orden de numeración (por posición X, por posición Y, etc.).
3. Haz clic en **Annotate**.

Esto asignará referencias como `R1`, `R2`, `C1`, `U1`, etc. a todos los símbolos sin referencia.

!!! warning "Re-anotar"
    Si re-anotas un esquemático que ya tiene referencias asignadas y footprints vinculados al PCB, debes sincronizar nuevamente el PCB (`Tools → Update PCB from Schematic`).
