# Motion In-betweening via Two-stage Transformers

![representative_image](./figures/representative_image.jpg)

Jia Qin, Youyi Zheng, and Kun Zhou. 2022. Motion In-betweening via Two-stage
Transformers. ACM Trans. Graph. 41, 6, Article 184 (December 2022),
16 pages. https://doi.org/10.1145/3550454.3555454

**Based on repository of above-mentioned paper: https://github.com/victorqin/motion_inbetweening**

## Getting Started

1. Download [LAFAN1](https://github.com/ubisoft/ubisoft-laforge-animation-dataset) dataset.

2. Extract  `lafan1.zip`  to `datasets` folder.  Bvh files should be located in `motion_inbetweening/datasets/lafan1` folder.

3. Download the [pre-trained models](https://github.com/victorqin/motion_inbetweening/releases/download/v1.0.0/pre-treained.zip) from the Releases Page. Extract it to the `motion_inbetweening/experiments` folder.

4. Install [PyTorch](https://pytorch.org). The code has been tested in Python3.8, PyTorch-1.8.2.

## Generate Transition

To use the full method (Detail + Context Transformer) to generate in-betweening, run `eval_detail_model.py`.

Usage:

```bash
usage: eval_detail_model.py [-h] [-o OFFSET] [-t TRANS] [-d] [-p]
                            det_config ctx_config animation output_dir

Evaluate detail model. No post-processing applied by default.

positional arguments:
  det_config            detail config name
  ctx_config            context config name
  animation             path to BVH file with animation
  output_dir            output directory where both reference animation and
                        inferred animation should be placed

options:
  -h, --help            show this help message and exit
  -o OFFSET, --offset OFFSET
                        animation clip frame offset from start, should be >=
                        175 (default=175)
  -t TRANS, --trans TRANS
                        transition length (default=30)
  -d, --debug           debug mode
  -p, --post_processing
                        apply post-processing
```

Example:

Get inferred result on animation aiming1_subject1.bvh from LAFAN1 dataset with transition=30 frames, 
   where the animation clip starts at frame 450, save to the `output` directory:

   ```bash
   python lafan1_detail_model lafan1_context_model "datasets/lafan1/aiming1_subject1.bvh" output -t 30 --offset 450
   ```