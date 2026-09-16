# MetricAnything native harness

The prompt-free Student PointMap checkpoint is a fine-tuned MoGe-2 ViT-L/14
model. Its native target therefore compiles its pinned, attributed MoGe-2 operator snapshot. The resulting
`metricanything_native.dll` is a standalone dependency-free InferBridge ABI2
harness; the source-level reuse adds no runtime DLL dependency.

From a recursive MetricAnything checkout:

```text
cmake -S metricanything/native -B <build-dir>
cmake --build <build-dir> --config Release --target metricanything_native
```

The source provenance is recorded under `native/moge2_runtime`. The deterministic converter is
`moge-2/native/tools/export_model.py --variant metricanything-student-pointmap`.

The public family is `MetricAnything`; `Student PointMap` is a weight row, not
a separate public model identity. Output is source-sized metric Z depth in
metres. The harness replaces invalid masked pixels before publication with the
finite `BackgroundDistanceMetres` model parameter (50 metres by default).
