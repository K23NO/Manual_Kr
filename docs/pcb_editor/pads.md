# Pads

Los **pads** son los puntos de contacto metálicos en el PCB donde se sueldan los componentes. Son parte de los **footprints** y tienen propiedades que determinan cómo se fabrica y solda la placa.

---

## Tipos de pads

### Through-Hole (THT — Orificio pasante)

Son agujeros metálizados que atraviesan toda la placa. El componente inserta sus patillas en estos agujeros y se solda en la cara opuesta.

- **Uso típico:** conectores, resistencias tradicionales, capacitores electrolíticos, componentes grandes.
- **Forma:** circular, cuadrada, rectangular u ovalada.
- **Cobre en:** ambas caras (`F.Cu` y `B.Cu`) y paredes del taladro.

```
  Vista en corte:
  ┌─────┐
  │ pad  │  F.Cu (superior)
  ├──○──┤  ← Agujero metálizado
  │ pad  │  B.Cu (inferior)
  └─────┘
```

### SMD (Surface Mount — Montaje superficial)

Pads planos que solo existen en una cara del PCB. El componente se suelda directamente sobre la superficie.

- **Uso típico:** resistencias, capacitores, CIs, relays y la mayoría de componentes modernos.
- **Forma:** rectangular, ovalada (*rounded rectangle*).
- **Cobre en:** solo la cara de montaje (`F.Cu` o `B.Cu`).

### NPTH (Non-Plated Through-Hole)

Agujeros que **no tienen cobre**. Se usan para tornillos de montaje (*mounting holes*) y posicionamiento mecánico.

---

## Propiedades de un pad

Haz doble clic sobre un pad en el PCB Editor para ver sus propiedades:

| Propiedad | Descripción |
|-----------|-------------|
| **Net** | Red eléctrica asignada al pad |
| **Type** | THT, SMD, NPTH |
| **Shape** | Forma del pad: Circle, Rectangle, Oval, Trapezoid, Roundrect |
| **Size X / Y** | Dimensiones del pad en mm |
| **Drill Size** | Diámetro del taladro (solo THT) |
| **Layers** | Capas en las que aparece el pad |
| **Thermal Relief** | Conexión termal a zona de cobre (para facilitar soldadura) |
| **Number** | Número de pin del footprint |

---

## Taladros (Drills)

Los taladros se especifican en los pads THT y NPTH. Consideraciones importantes:

| Tipo | Descripción |
|------|-------------|
| **Taladro circular** | El más común, se especifica con un solo diámetro |
| **Taladro ovalado** | Para pines rectangulares o de conector |
| **Taladros pasante (PTH)** | Con cobre en las paredes |
| **Taladros no pasantes (NPTH)** | Sin cobre, solo mecánicos |

### Diámetros de taladro recomendados

| Uso | Diámetro de taladro |
|-----|--------------------|
| Componente genérico (0.5mm pin) | 0.8 mm |
| Conector pin header 2.54mm | 1.0 mm |
| Conector de potencia (pin 1mm) | 1.3 mm |
| Tornillo M2 (mounting hole) | 2.2 mm |
| Tornillo M3 (mounting hole) | 3.2 mm |
| Tornillo M4 (mounting hole) | 4.3 mm |

!!! tip "Regla general para taladros THT"
    El diámetro del taladro debe ser aproximadamente **0.2–0.3 mm mayor** que el diámetro del pin del componente para facilitar la inserción y la soldadura.

---

## Máscara de soldadura (Solder Mask)

La máscara de soldadura es la capa protectora de color (verde, azul, rojo, etc.) que cubre la placa. Los pads tienen una **apertura en la máscara** para quedar expuestos y poder soldarse.

- **Solder Mask Expansion:** expansión de la apertura respecto al pad. Valor positivo = apertura mayor que el pad.
- Valor estándar: `0.05 mm` a `0.1 mm`.

---

## Pasta de soldadura (Solder Paste)

Para pads SMD, la pasta de soldadura se aplica mediante un stencil antes del proceso de refusión. KiCad genera una capa `F.Paste` con las aperturas correspondientes.

- Los pads THT **no** suelen tener capa de pasta.
- Para pads SMD bajo componentes de alta densidad, se puede reducir la cobertura de pasta (`Paste Mask Expansion` negativo).

---

## Editar un pad dentro del footprint

!!! warning "Editar footprints en el PCB"
    Los cambios realizados a un pad **dentro del PCB Editor** son locales al proyecto y no se guardan en la librería de footprints. Para cambios permanentes, edita el footprint en el **Footprint Editor**.

Para modificar un pad:

1. En el PCB Editor, haz doble clic sobre el footprint.
2. Haz doble clic sobre el pad específico dentro del footprint.
3. Modifica las propiedades según sea necesario.
4. Haz clic en **OK**.

---

## Via (Perforación de conexión entre capas)

Las **vias** son similares a los pads THT pero sin componente: sirven para conectar una pista de una capa a otra.

| Tipo | Descripción |
|------|-------------|
| **Via through** | Atraviesa toda la placa (F.Cu a B.Cu) |
| **Blind via** | Va de una cara superficial a una capa interna |
| **Buried via** | Va entre dos capas internas (no llega a ninguna superficie) |

Las blind y buried vias solo son posibles en PCBs multicapa y tienen costo adicional en fabricación.

Para colocar una via durante el enrutado:
- Presiona `V` mientras enrutas una pista para colocar una via y cambiar de capa.
