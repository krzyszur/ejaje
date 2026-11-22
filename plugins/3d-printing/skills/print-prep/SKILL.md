---
name: print-prep
description: Prepare or review a 3D model for FDM printing (PETG/PLA): mesh integrity, wall thickness, orientation, overhangs, fillets and chamfers, ribs without supports, clearances, speed vs strength. Use when the user designs a part to be printed, asks if a model is printable, or wants it optimized before slicing.
---

# Print preparation (FDM)

Original checklist, written from general FDM practice. Inspired by the idea of a model-preparation skill; no third-party text copied.

## Workflow

1. **Clarify** (ask only what is missing): material (default PETG), nozzle (default 0.4 mm), layer height (default 0.2 mm), printer bed size, load direction, fit with other parts, visible surfaces.
2. **Check the mesh** (STL/3MF/STEP exported to mesh): watertight, no non-manifold edges, no inverted normals, no self-intersections, no zero-thickness faces, sensible units (mm), scale correct. Fix in the CAD source when possible, not by patching the mesh.
3. **Choose orientation** (see below), then **check walls, overhangs, details, clearances**.
4. **Report** as a short table: issue, location, severity (blocker / should fix / note), suggested change. Then propose slicer settings.

## Orientation

- Layers are weakest between each other: put the main load **along** layers, not across (do not make a tensile load pull layers apart).
- Largest flat face on the bed for adhesion and accuracy; avoid tiny contact area.
- Minimize overhangs and supports; hide the seam and support scars on non-visible faces.
- Holes meant to be round are best with their axis vertical; horizontal holes come out slightly oval, so add 0.1-0.2 mm or print a teardrop/diamond top.
- Thin tall parts: widen the base or add a brim; consider printing flat.

## Wall thickness

- Minimum wall = a whole multiple of the extrusion width (0.4 nozzle: 0.8, 1.2, 1.6 mm). Below ~0.8 mm walls are fragile or are skipped by the slicer.
- Structural walls: 1.6-2.4 mm. Thin decorative or flexible features: at least 2 perimeters.
- Thin gaps narrower than ~0.4 mm fill in; do not rely on them.
- Louvers, flaps and membranes: keep 0.8-1.2 mm if rigid, thinner only if they are meant to flex and are tested.

## Overhangs and bridges

- Up to ~45 degrees from vertical prints without support; 60+ degrees needs support or a design change.
- Replace overhangs with **chamfers 45 degrees** instead of horizontal ledges; for horizontal holes use teardrop shapes.
- Bridges up to ~20-30 mm are usually fine in PETG with good cooling; PETG strings and sags more than PLA, so shorten them.

## Fillets and chamfers

- Fillet inside corners (r >= 1 mm) to cut stress concentration; sharp inside corners crack along layer lines.
- Chamfer (0.4-0.8 mm) the first-layer edge on the bed side to avoid elephant foot.
- Use chamfer, not fillet, on the underside of overhanging edges; a fillet there creates a changing overhang angle.
- Round or chamfer outside edges that meet a hand or a seal.

## Ribs and stiffening without supports

- Ribs: thickness ~0.5-0.6x of the wall they stiffen, height up to ~3-4x thickness, with a fillet at the base.
- Orient ribs vertically (parallel to Z) or at 45 degrees so they need no support; avoid ribs that hang in the air.
- Triangular gussets (45 degrees) beat horizontal shelves.
- Prefer more perimeters and a corrugated or ribbed shape over high infill for stiffness.

## Clearances and fits (0.4 mm nozzle, tune per printer)

| Fit | Gap per side |
|---|---|
| Press / snug | 0.05-0.1 mm |
| Sliding / push fit | 0.15-0.25 mm |
| Loose / moving | 0.3-0.5 mm |
| Print-in-place hinge | 0.4-0.6 mm |

- Print a small test coupon before committing a long print.
- Screw holes: model at core diameter for self-tapping, or +0.2-0.3 mm for clearance; keep >= 2 perimeters of wall around them.
- Account for shrinkage and first-layer squish on small holes: they come out smaller (typically -0.1 to -0.2 mm).

## Speed vs strength (PETG)

- Strength comes from perimeters, temperature and layer adhesion, not infill: 3-4 perimeters, 15-25% infill (gyroid or cubic) is usually enough.
- Higher nozzle temperature and slower, lower-cooling printing improve layer adhesion; PETG: ~230-250 C nozzle, bed 70-85 C, fan 30-60%.
- Speed: outer walls 30-50 mm/s for quality; inner walls and infill faster. Thicker layers (0.28 mm) cut print time a lot with a small loss in detail.
- For parts under load, thicker perimeters and wider lines beat extra infill; for appearance use a smaller layer height only on visible parts.
- Dry the filament if you see stringing or popping.

## Output

End with: (1) verdict (printable / needs changes), (2) the list of changes to the model, (3) recommended orientation and slicer settings (layer height, perimeters, infill, supports, speed, temperatures), (4) what to test first (coupon or a fragment).
