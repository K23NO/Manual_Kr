# PCBway Plugin

El plugin de **PCBway** para KiCad permite enviar el proyecto directamente al servicio de fabricación de PCBs de PCBway desde el PCB Editor, sin necesidad de exportar Gerbers manualmente.

---

## ¿Qué es PCBway?

**PCBway** es un servicio de fabricación de PCBs (y ensamblaje PCBA) con sede en China, ampliamente utilizado en el desarrollo electrónico por su relación precio-calidad. En **JW Control** utilizamos PCBway como uno de nuestros proveedores de fabricación de prototipos y producción pequeña.

Sitio web: `https://www.pcbway.com`

---

## Instalación del plugin

### Desde el PCM (recomendado)

1. Abre el **Plugin and Content Manager**.
2. Busca `PCBway`.
3. Haz clic en **Install**.
4. El plugin quedará disponible en `Tools → PCBway`.

---

## Uso del plugin

### Enviar el proyecto a PCBway

1. Con el proyecto abierto en el **PCB Editor**.
2. Ve a `Tools → PCBway`.
3. El plugin generará automáticamente los archivos Gerber y de taladro.
4. Se abrirá el navegador con los archivos precargados en el formulario de PCBway.
5. Configura las opciones del pedido (cantidad, material, color de máscara, acabado, etc.).
6. Revisa la cotización y procede al pedido si estás de acuerdo.

---

## Parámetros de fabricación estándar en JW Control

Para pedidos estándar en JW Control, usamos los siguientes parámetros en PCBway:

| Parámetro | Valor |
|-----------|-------|
| **Layers** | 2 (o según diseño) |
| **Material** | FR-4 |
| **Thickness** | 1.6 mm |
| **Surface finish** | HASL (lead-free) |
| **Copper weight** | 1 oz |
| **Solder mask color** | Green (o según preferencia del proyecto) |
| **Silkscreen color** | White |
| **Min track/spacing** | 6/6 mil (0.15/0.15 mm) |
| **Min hole size** | 0.3 mm |

!!! note "ENIG vs HASL"
    Para proyectos con componentes de alta densidad (BGA, QFN, pitch fino) o conectores de inserción directa, considera usar acabado **ENIG** (Electroless Nickel Immersion Gold) por su planicidad y durabilidad, aunque tiene costo adicional.

---

## Archivos Gerber (exportación manual)

Si prefieres exportar los Gerbers manualmente en lugar de usar el plugin:

1. En el PCB Editor: `File → Fabrication Outputs → Gerbers (.gbr)`.
2. Configura las capas a exportar:

| Capa KiCad | Archivo Gerber |
|------------|---------------|
| `F.Cu` | `proyecto-F_Cu.gbr` |
| `B.Cu` | `proyecto-B_Cu.gbr` |
| `F.Silkscreen` | `proyecto-F_Silkscreen.gbr` |
| `B.Silkscreen` | `proyecto-B_Silkscreen.gbr` |
| `F.Mask` | `proyecto-F_Mask.gbr` |
| `B.Mask` | `proyecto-B_Mask.gbr` |
| `F.Paste` | `proyecto-F_Paste.gbr` |
| `Edge.Cuts` | `proyecto-Edge_Cuts.gbr` |

3. Exporta también los archivos de taladro: `File → Fabrication Outputs → Drill Files (.drl)`.
4. Comprime todos los archivos en un `.zip` y súbelos a PCBway.

!!! tip "Verificar Gerbers"
    Antes de enviar a fabricación, verifica los Gerbers con el **Gerber Viewer** de KiCad (`File → Fabrication Outputs → View Gerber Files`) o con herramientas online como **PCBway Gerber Viewer** para confirmar que los archivos son correctos.

---

## Checklist antes de ordenar

Antes de enviar una placa a fabricación, verifica:

- [ ] ERC ejecutado sin errores en el esquemático.
- [ ] DRC ejecutado sin errores en el PCB.
- [ ] Todos los pines del ratsnest enrutados (0 unconnected).
- [ ] Contorno (`Edge.Cuts`) correcto y cerrado.
- [ ] Dimensiones de la placa verificadas.
- [ ] Texto de serigrafía legible y fuera de los pads.
- [ ] Courtyards sin superposición.
- [ ] Número de versión y/o fecha en la serigrafía.
- [ ] Revisión de la vista 3D (tecla `3`).
- [ ] Parámetros de fabricación compatibles con las capacidades del fabricante.
