# Mosaic Art Maker

This repository includes the code (and files) for creating mosaic art versions of a given image. Given an image
(referred to as the original image), the main idea is to replace (square-shaped) patches of the original image with the
most similar image from a given set of images (referred to as the tile images or simply tiles).

Examples:

<p style="text-align:center">
<img alt="Original image 1" title="A picture of Miley Cyrus" src="images/canvases/miley_cyrus.png" width="256" height="256"/> 
<img alt="Mosaic art image 11" title="The mosaic art version of the Miley Cyrus's image; made of 2.5k tiles" src="images/examples/miley_cyrus_mosaic_art_50.png" width="256" height="256"/>
<img alt="Mosaic art image 12" title="The mosaic art version of the Miley Cyrus's image; made of 90k tiles" src="images/examples/miley_cyrus_mosaic_art_300.png" width="256" height="256"/>
</p>

<p style="text-align:center">
<img alt="Original image 2" title="Nixon Visions" src="images/canvases/nixon_visions.png" width="256" height="256"/> 
<img alt="Mosaic art image 21" title="The mosaic art version of Nixon Visions; made of 2.5k tiles" src="images/examples/nixon_visions_mosaic_art_50.png" width="256" height="256"/>
<img alt="Mosaic art image 22" title="The mosaic art version of Nixon Visions; made of 90k tiles" src="images/examples/nixon_visions_mosaic_art_300.png" width="256" height="256"/>
</p>

The implementation uses the [Stable Diffusion](https://en.wikipedia.org/wiki/Stable_Diffusion) model available from
[KerasCV](https://github.com/keras-team/keras-cv) submodule of [Keras](https://keras.io/) to create the tiles. It makes
it possible to create very different versions of the mosaic art by changing the parameters of the model.

### Getting started

Please, make sure that the dependencies are installed. If you use Pip, you can install them by running the following
command:

```bash
pip install -r requirements.txt
```

The code is written in Python 3.9, and is tested on Ubuntu 22.04 LTS with Keras 2.9 (and KerasCV 0.3.4).

Open [Making Mosaic Art using KerasCV+StableDiffusion](make_mosaic_art.ipynb) notebook to see the code.

### License

This project is licensed under the terms of the Apache 2.0 license. See [LICENSE](LICENSE.md) for more details.
Please note that some the images in the [images](images) folder are not licensed under the Apache 2.0 license.
Specially, image files in [images/canvases](images/canvases) were downloaded from the Web and are not owned by
the creator of this repository.
