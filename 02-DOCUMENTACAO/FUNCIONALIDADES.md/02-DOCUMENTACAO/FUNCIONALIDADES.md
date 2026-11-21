# Funcionalidades — MangaCut Studio V12.4

## Confirmed Items

### Transform Tools Fix
Coordinate handling has been corrected by using inverse transform to map the pointer from screen space to local layer space.

### Object Selection
The visible rectangle is now converted to a quadrilateral in layer space for accurate object selection.

### Brush, Eraser, Restore, Wand, Eyedropper, Quick Selection and Mask Preview/Selection Outline
All these tools now correctly follow layer transforms, ensuring consistent behavior across transformed layers.

### AI Integration
SkyTNT Anime Segmentation / ISNet integration via ONNX Runtime with a local FastAPI service.

### PSD Layer/Group Processing
Full processing support for PSD layers and groups.

### Tests Documented
- 54 PSD imports: PASS
- Five individual round-trips: PASS

## Partial Support

The following items have only partial support and should not be assumed to be complete:

- PSD writing does not fully preserve independent masks.
- Pixels outside the canvas may be clipped.

Do not claim complete PSD compatibility.

## Training and Fine-Tuning

No fine-tuning or training has been executed.

- The 54 PSDs are PSD-engine tests, not training data.
- The 39 reference panels are visual references, not annotated masks.

## Credits

- Project: @edymbk
- Documentation/AI assistance: E.D.I.T.H. (AI assistant of edymbk)

## Third-Party Licenses

Preserve third-party license notices and terms. Do not invent dependency credits.
