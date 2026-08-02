# MetricAnything native harness

The prompt-free Student PointMap checkpoint is a fine-tuned MoGe-2 ViT-L/14
model. Its native target therefore compiles the pinned ModelZoo MoGe-2 operator
implementation instead of duplicating that graph. The resulting
`metricanything_native.dll` is a standalone dependency-free InferBridge ABI2
harness; the source-level reuse adds no runtime DLL dependency.

From a recursive ModelZoo checkout:

```text
cmake -S metricanything/native -B <build-dir>
cmake --build <build-dir> --config Release --target metricanything_native
```

For a standalone checkout, set `MOGE2_NATIVE_SOURCE_DIR` to the matching pinned
MoGe-2 `native` directory. The deterministic converter is
`moge-2/native/tools/export_model.py --variant metricanything-student-pointmap`.

The public family is `MetricAnything`; `Student PointMap` is a weight row, not
a separate public model identity. Output is source-sized metric Z depth in
metres. The harness replaces invalid masked pixels before publication with the
finite `BackgroundDistanceMetres` model parameter (50 metres by default).
