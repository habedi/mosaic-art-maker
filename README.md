# Creating Mosaic Art using AI

This repository includes the code (and other files) for creating [mosaic art](https://en.wikipedia.org/wiki/Mosaic)
versions of a given image. Given an image
(referred to as the original image), the main idea is to replace (square-shaped) patches of the original image with the
most similar image from a given set of images (referred to as the tile images or simply tiles).

The implementation uses the [Stable Diffusion](https://en.wikipedia.org/wiki/Stable_Diffusion) model available from
[KerasCV](https://github.com/keras-team/keras-cv) submodule of [Keras](https://keras.io/) to create the tiles. It allows limitless creativity by creating mosaic art of the same image using different tiles created by changing the model's parameters and using
different text prompts.

In the examples below, each row shows an (original) image and two mosaic art images created from it.
The left-most image is the original image, and the middle image is the mosaic art created using 2,500 tiles, and the
right-most image is the mosaic art created using 90,000 tiles.


<p align="center">
<img alt="Original image 2" title="Nixon Visions" src="images/canvases/nixon_visions.png" width="256" height="256"/> 
<img alt="Mosaic art image 21" title="The mosaic art version of Nixon Visions; made of 2.5k tiles" src="images/examples/nixon_visions_mosaic_art_50.png" width="256" height="256"/>
<img alt="Mosaic art image 22" title="The mosaic art version of Nixon Visions; made of 90k tiles" src="images/examples/nixon_visions_mosaic_art_300.png" width="256" height="256"/>
</p>

<p align="center">
<img alt="Original image 1" title="A photo of Miley Cyrus" src="images/canvases/miley_cyrus.png" width="256" height="256"/> 
<img alt="Mosaic art image 11" title="The mosaic art version of Miley Cyrus's photo; made of 2.5k tiles" src="images/examples/miley_cyrus_mosaic_art_50.png" width="256" height="256"/>
<img alt="Mosaic art image 12" title="The mosaic art version of Miley Cyrus's photo; made of 90k tiles" src="images/examples/miley_cyrus_mosaic_art_300.png" width="256" height="256"/>
</p>

### Getting started

#### Main files and folders

The main files and folders included in this repository are:

1. [images/canvases](images/canvases): This folder includes the (original) images. Place your image files in this folder to create mosaic art versions of them. Please note that the images must have the same dimensions (width and
   height).
2. [images/tiles](images/tiles): This folder includes the tile images. There are already some tile images in this
   folder. You can use an instance of MosiacArtMaker to create your own custom set of tile images and put them in
   the `images/tiles` folder.
3. [images/output](images/outputs): The mosaic art images are saved in this folder.
4. [make_mosaic_art.ipynb](make_mosaic_art.ipynb): This notebook includes the code for creating mosaic
   art versions of the images in the `images/canvases` folder and also the code for creating the
   tile images.

#### Dependencies

The main dependencies are `TensorFlow/Keras` (at least version 2.9), `Pillow`, and `Scipy`. If you use Pip, you can
install them by running the following command:

```bash
pip install -r requirements.txt
```

Moreover, the code is written in Python 3.9 and is tested on a computer running Ubuntu 22.04 LTS with Keras 2.9 (and KerasCV
0.3.4) on an NVIDIA RTX 3090 GPU with CUDA 11.6.

#### Running the code

Open [Making Mosaic Art using KerasCV+StableDiffusion](make_mosaic_art.ipynb) notebook to see the code.

Furthermore, you can modify the variables and parameters in the main function (shown below) to create your own mosaic art versions of the
given images. You can place your images in the `images/canvases` folder if you want to create mosaic art versions of
them.

```python
def main(remake_tiles: bool) -> None:
    """Main function to pack everything together and run it"""

    # Extension to use for saving and loading the tile images
    tile_file_extension = "jpeg"

    # (Re)-make the tile images if the user wants to do so
    if remake_tiles:

        # Create a MosaicMaker object to make the tile images
        image_maker = MosaicMaker(img_width=400, img_height=400, jit_compile=False, seed=33)

        # The text prompts to be used to make the tile images
        prompt_seq = (("A laughing woman", ("realistic", "white background")),
                      ("A sad girl", ("realistic", "white background")),
                      ("An old man", ("realistic", "white background")),
                      ("Face of a sad man", ("realistic", "white background")),
                      ("Drawing of rings of Saturn", ("abstract", "white background")),
                      ("A watercolor painting of a puppy", ("detailed",)),
                      ("Drawing of a red rose", ("elegant", "detailed", "white background")),
                      ("View of a green forest with mountains in the background", ("elegant", "lush", "nature")),
                      ("A painting of four oranges in a bowl", ("elegant", "detailed", "white background")),
                      ("A ninja shuriken", ("realistic", "metal", "white background")),)

        # Make the tile images and save them
        for index, prompt_data in enumerate(prompt_seq):
            image_seq = image_maker.make_images(prompt_data[0], prompt_data[1], num_images=40)
            image_maker.save_images(img_seq=image_seq, path='images/tiles', prefix=f'p{index}',
                                    extension=tile_file_extension)

    # Use the images in the images/canvases and images/tiles directories to make mosaic arts
    for canvas_image_path in pathlib.Path("images/canvases").glob("*.png"):
        # Create a MosaicArtMaker object with about sqrt_num_tiles*sqrt_num_tiles tiles!
        art_maker = MosaicArtMaker(original_image_path=canvas_image_path, sqrt_num_tiles=300,
                                   tile_file_extension=tile_file_extension)

        # Make the mosaic art and save it in the images/outputs directory
        output_image = art_maker.make_mosaic_art(k=40)
        print(f"Created a mosaic art version of '{art_maker.original_image_path}' using "
              f"{art_maker.sqrt_num_tiles * art_maker.sqrt_num_tiles} smaller images created by a Stable Diffusion model")
        art_maker.save_images((output_image,), path='images/outputs',
                              prefix=f'{art_maker.original_image_name}_mosaic_art')

        # Display each original image and its mosaic art version
        art_maker.display_images((art_maker.original_image, output_image),
                                 (art_maker.original_image_name, art_maker.original_image_name + "_mosaic_art"))
```

Run the main function to execute the code. If you want to remake the tile images, set the `remake_tiles` parameter
to `True`. Note that creating a new set of tile images might take a while, so it is recommended to use the current tile
images in the beginning by setting `remake_tiles` to `False`.

```python
main(remake_tiles=False)
```

#### Kaggle notebook

The notebook is available on Kaggle now. You can open it using [this link](https://www.kaggle.com/code/habedi/creating-mosaic-art-using-kerascv-stablediffusion).

### Ideas for improvement

- [x] Adding a link to a Kaggle or Colab version of the notebook.

<del>- [ ] Using different shapes instead of squares (of the same size) for the tiles. For example, trapezoids or triangles. </del>

<del>- [ ] Using different tile images for different parts of the original image. For example, using a set of images containing faces for the faces in the original image, and using a set of images containing landscapes for the
  background in the original image. </del>
  
  <del>- [ ] Using better similarity metrics for comparing the tiles with a patch from the original image. For example, using the [SSIM](https://en.wikipedia.org/wiki/Structural_similarity) metric instead of the Euclidean distance. </del>

### Credits

- [KerasCV](https://keras.io/keras_cv): The code for creating the tile images uses
  the StableDiffusion model available from KerasCV.
- The idea for creating mosaic art versions of images using a collection of tile images is inspired
  by [this post](https://medium.com/@aarongrove/creating-image-mosaics-with-python-8e4c25dd9bf9).

### License

This project is licensed under the terms of the Apache 2.0 license. See [LICENSE](LICENSE.md) for more details.
Please note that the image files in [images/canvases](images/canvases) were downloaded from the Web and are not owned by
the creator of this repository. Consequently, they may not be licensed under the Apache 2.0 license.
