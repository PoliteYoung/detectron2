# PyTorch 2.10 / CUDA 12.8 compatibility changes

This source checkout is built editable into the active Conda environment named
`pt210`. It has been validated on RTX 5090 (`TORCH_CUDA_ARCH_LIST=12.0`), while
the build architecture can be changed on another CUDA 12.8 GPU. Public upstream
is `https://github.com/facebookresearch/detectron2.git`; this snapshot is based
on commit `b4a4a3bd136852dae5fb1de37978dee412653e31` plus the compatibility patch:

- replaces removed `pkg_resources.resource_filename` with `pathlib`;
- migrates deprecated `timm.models.layers` imports to `timm.layers`;
- adds explicit `indexing="ij"` to `torch.meshgrid` calls;
- accepts current `iopath` releases and moves `black` out of runtime dependencies.

Build with `--no-deps --no-build-isolation`; dependency resolution must not replace
the shared Torch/CUDA/OpenCV stack.


No model weights are bundled or required merely to install Detectron2. Individual
applications must obtain their configured checkpoints from the Detectron2 model
zoo or the application-specific README. Clone this fork to reproduce the source changes:

```bash
git clone https://github.com/PoliteYoung/detectron2.git
cd detectron2
conda activate pt210
python -m pip install --no-deps --no-build-isolation -e .
```
