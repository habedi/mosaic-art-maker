# Mosaic Art Maker

This repository includes the code (and files) for creating mosaic art versions of a given image. Given an image (referred to as the original image), 
the main idea is to replace (square-shaped) patches of the original image with the most similar image from a given set of 
images (called tiles). 

Examples:


<img src="images/canvases/miley_cyrus.png" width="512" height="512"/> <img src="images/outputs/miley_cyrus_mosaic_art_0.png" width="512" height="512"/> 


<img src="images/nixon_visions.png" width="512" height="512"/> <img src="images/outputs/nixon_visions_mosaic_art_0.png" width="512" height="512"/>


The implementation uses the [Stable Diffusion](https://en.wikipedia.org/wiki/Stable_Diffusion) model available from [KerasCV](https://github.com/keras-team/keras-cv) submodule of [Keras](https://keras.io/) to create the tiles.

### Getting started

Please, make sure that the dependencies are installed. If you use Pip, you can install them by running the following command:

```bash
pip install -r requirements.txt
```

The code is written in Python 3.9, and is tested on Ubuntu 22.04 LTS with Keras 2.9 (and KerasCV 0.3.4).


Open [Making Mosaic Art using KerasCV+StableDiffusion](make_mosaic_art.ipynb) notebook to see the code.


### License

This project is licensed under the terms of the Apache 2.0 license. See [LICENSE](LICENSE.md) for more details.
Please note that some the images in the [images](images) folder are not licensed under the Apache 2.0 license. Specially, image files in
[images/canvases](images/canvases) were downloaded from the Web and are not owned by the author of this repository.
