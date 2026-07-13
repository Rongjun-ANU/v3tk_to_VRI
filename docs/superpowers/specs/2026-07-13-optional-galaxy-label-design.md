# Optional Galaxy Label Design

## Goal

Extend `auto_arrange_and_combine.py` so this command labels every input image:

```text
./auto_arrange_and_combine.py *_combined_VRI.png 16 9 label
```

Each placed image will show its galaxy ID in red at that image's top-left corner.

## Interface

- Preserve all existing commands and output behavior when `label` is absent.
- Accept `label` as the optional final positional item after the aspect-ratio values.
- Reject an unrecognized trailing mode instead of silently treating it as an image.

## Label Derivation and Rendering

- Derive the galaxy ID from the input basename by removing the
  `_combined_VRI` suffix and file extension. For example,
  `NGC4380_combined_VRI.png` becomes `NGC4380`.
- Render the ID after each source image is placed on the mosaic.
- Position the text inside the placed image's top-left corner with a small inset.
- Use red text and a readable Pillow-provided font, without adding a new dependency.
- Apply labels to the requested output mosaic. Existing unlabeled behavior remains
  unchanged.

## Testing

- Add a focused test that first fails because `label` is not yet recognized/rendered.
- Verify filename-to-ID extraction.
- Verify label mode produces red pixels near each placed image's top-left corner.
- Verify the existing unlabeled path remains unchanged.

## Scope

Only `auto_arrange_and_combine.py` and its focused test coverage are in scope.
No packing, solver, proof-report, or unrelated CLI behavior will be refactored.
