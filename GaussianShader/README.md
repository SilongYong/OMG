# Running GaussianShader with OMG

## Installation
Since this code is based on [GaussianShader](https://github.com/Asparagus15/GaussianShader), please follow their installation guide. In short,

```shell

# Install dependencies
conda env create --file environment.yml
conda activate gaussian_shader
```

Note that we modified the `diff-gaussian-rasterization` module for the activation function discussed in the paper.

## Running
Download the [example data](https://drive.google.com/file/d/1bSv0soQtjbRj9S9Aq9uQ27EW4wwY--6q/view?usp=sharing) and put it to the ``data`` folder. Execute the optimizer using the following command:
```shell
python train.py -s data/<dataset>/<scene> --eval -m output/<scene> -w --brdf_dim 0 --sh_degree -1 --lambda_predicted_normal 2e-1 --brdf_env 512 --opacity_mlp_lr 0.0001
```

## Rendering
```shell
python render.py -m output/<scene> --brdf_dim 0 --sh_degree -1 --brdf_mode envmap --brdf_env 512
```

## Evaluation
```shell
python metrics.py -m output/<scene>
```

`<scene>` stands for the data we're training on and `<dataset>` can be `refnerf` or `GlossySynthetic`.

Note that we save the original model in `./scene/gaussian_model_ori.py` for reference.

## Dataset
We follow GaussianShader to evaluate the method on [Shiny Blender](https://github.com/google-research/multinerf) and [Glossy Synthetic](https://github.com/liuyuan-pal/NeRO). You can use ``nero2blender.py`` to convert the Glossy Synthetic data into Blender format. The data is stored in the `data` folder.


## Acknowledgement
We would like to thank [GaussianShader](https://github.com/Asparagus15/GaussianShader) for the useful code base.