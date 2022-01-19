# dogsy_breeder
> **DOG**s' noi**SY** labels **BREED** classifi**ER** (based on Imagewoof dataset)

## Table of Content

- [Task description](#task-description)
- [Dataset](#dataset)
- [Project code structure](#project-code-structure)
- [Interesting topics](#interesting-topics)
- [Future ideas](#future-ideas)
- [Install](#install)
- [Developing](#developing)
  - [Starting of Jupyter Server](#starting-of-jupyter-server)

## Task description
[Notion: Dog breed classifier with PyTorch on Noisy labeled dataset](https://www.notion.so/dmitmatveev/Dog-breed-classifier-with-PyTorch-on-Noisy-labeled-dataset-b8558cb6cd8147a7abf1ba5565549f9c)


## Dataset

- Based on: [fastai/imagenette](https://github.com/fastai/imagenette)


## Project code structure

- Based on: [Pytorch Code Examples - Code Layout](https://cs230.stanford.edu/blog/pytorch/#code-layout)
> - `model/net.py`: specifies the neural network architecture, the loss function and evaluation metrics
> - `model/data_loader.py`: specifies how the data should be fed to the network
> - `train.py`: contains the main training loop
> - `evaluate.py`: contains the main loop for evaluating the model
> - `utils.py`: utility functions for handling hyperparams/logging/storing model

- Another idea how to structure the PyTorch project: 
[towardsdatascience - How To Structure Your PyTorch Project](https://towardsdatascience.com/how-to-structure-your-pytorch-project-89310b8b2da9)


## Interesting topics
- [ayasyrev/imagenette_experiments](https://github.com/ayasyrev/imagenette_experiments)
  > [forums.fast.ai - How we beat the 5 epoch ImageWoof leaderboard score - some new techniques to consider](https://forums.fast.ai/t/how-we-beat-the-5-epoch-imagewoof-leaderboard-score-some-new-techniques-to-consider/53453)
  - Uses [nbdev from fast.ai](https://nbdev.fast.ai/).
    > `nbdev` is a library that allows you to develop a python library in Jupyter Notebooks, 
    putting all your code, tests and documentation _(automatically generated)_ in one place 
  - Template of `nbdev`: [fastai/nbdev_template](https://github.com/fastai/nbdev_template)
  - `XResnet`, `MaxBlurPool` _(instead of `AveragePool2d` and `MaxPool2d`)_, 
    `Mish` activation function, `Ranger` optimizer
- Maybe something about semi-supervised training will be helpful in case of training on noisy labeled datasets?
  Something like [paperswithcode - Noisy Student](https://paperswithcode.com/paper/self-training-with-noisy-student-improves)


## Future ideas
- [ ] Just in case of getting interesting experience: try to train `EfficientNet` model on `Imagewoof`?
- [ ] Try to use [cleanlab tool](https://github.com/cleanlab/cleanlab)
  - Was founded by me by [stackoverflow.com - Dealing with noisy training labels in text classification using deep learning](https://stackoverflow.com/questions/40009134/dealing-with-noisy-training-labels-in-text-classification-using-deep-learning)
  - Usage looks like training the model, been wrapped by `cleanlab.classification.LearningWithNoisyLabels`. 
  - Good documentation, i.e. `cleanlab` has tutorials of usage
  - Active updates, widely used
- [ ] Try to use SAM optimizer [[paperswithcode]](https://paperswithcode.com/paper/sharpness-aware-minimization-for-efficiently-1#code). 
  SAM implementations: 
  - [davda54/sam](https://github.com/davda54/sam)
    > SAM **improves model generalization** and yields SoTA performance for several datasets. 
    Additionally, it **provides robustness to label noise** on par with that provided by SoTA procedures 
    that specifically target learning with noisy labels.
  - [moskomule/sam.pytorch](https://github.com/moskomule/sam.pytorch)

- [ ] Try to use SoTA-classifier by itself, like `CoAtNet` [[arxiv]](https://arxiv.org/pdf/2106.04803v2.pdf) 
  [[paperswithcode]](https://paperswithcode.com/paper/coatnet-marrying-convolution-and-attention#code). 
  Several implementations (from `paperswithcode`) in my own order to take into account:
  - [xmu-xiaoma666/External-Attention-pytorch - CoAtNet.py](https://github.com/xmu-xiaoma666/External-Attention-pytorch/blob/master/model/attention/CoAtNet.py)
  - [chinhsuanwu/coatnet-pytorch](https://github.com/chinhsuanwu/coatnet-pytorch)
  - [tyeso/Image_Classification_with_CoAtNet_and_ResNet18](https://github.com/tyeso/Image_Classification_with_CoAtNet_and_ResNet18)
  - [LongLeCE/CoAtNet-PyTorch](https://github.com/LongLeCE/CoAtNet-PyTorch)
  - [ ] but the number of params for `CoAtNet` is huge in comparison of `EfficientNets` 
    or `XResnet` (from [ayasyrev/imagenette_experiments](https://github.com/ayasyrev/imagenette_experiments)). 
    Will be training fast enough to get high performance on 
    5, 20, 40, 160 epochs while training from starch, to stay within the limits of [`Imagewoof`](#dataset) contest? 
- [ ] And maybe then try to use `CoAtNet` with `Mish` in replace of `ReLU` in it
- [ ] And with `MaxBlurPool` _(instead of `AveragePool2d` and `MaxPool2d`)_. What to do with `MaxPool1d` in `CoAtNet`? 


## Install
```shell
DOGSY_BREEDER_DIR="/path/to/the/repo/"
cd $DOGSY_BREEDER_DIR

# On Windows:
# $Env:DOGSY_BREEDER_DIR="/path/to/the/repo/"
```

```shell
# activate your-virtual-environment here, then ... 
cd $DOGSY_BREEDER_DIR
pip install requirements.txt
```

## Developing

### Starting of Jupyter Server

```shell
jupyter notebook --ip 0.0.0.0 --port 9275 --no-browser
# On Jupiter, the equatorial diameter is 9,275 km
```

```shell
# Or Jupyter Lab:
jupyter lab --ip 0.0.0.0 --port 9275 --no-browser --autoreload --notebook-dir $DOGSY_BREEDER_DIR

# On Windows:
# jupyter lab --ip 0.0.0.0 --port 9275 --no-browser --autoreload --notebook-dir $Env:DOGSY_BREEDER_DIR
```

TIP: In case you've forgotten to install kernel:
```shell
jupyter kernelspec list
python -m ipykernel install --name='your-virtual_environment_name'
```