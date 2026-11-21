# Funcionalidades — MangaCut Studio V12.4

## Funcionalidades documentadas

### Transform Tools Fix
Maps pointer coordinates from screen to layer-local space using inverse transform for translation/scale/rotation/mirroring.

### Object Selection
Converts visible rectangle into quadrilateral in layer space.

### Tool Support for Layer Transforms
Brush, eraser, restore, wand, eyedropper, quick selection, mask preview and selection outline follow layer transforms.

### AI Integration
SkyTNT Anime Segmentation / ISNet via ONNX Runtime and local FastAPI service.

### PSD Processing
Layers and groups.

### Documented Test Pipeline

## Status

- **54 PSD imports PASS**
- Five individual round-trips PASS only, not all 54
- PSD writing does not fully preserve independent masks
- Pixels outside canvas may be clipped
- Do not claim complete PSD compatibility

## IA

- No fine-tuning/training executed
- 54 PSDs are engine tests, not training data
- 39 visual reference panels are not annotated masks

## Credits

- @edymbk project
- E.D.I.T.H. documentation/AI assistance

---

Preserve third-party license terms/notices and do not invent dependency credits.
