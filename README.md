# Mosaic Art Maker application

This repository includes the code (and files) for creating a mosaic art from a given image. Given an image (referred to as the original image), 
the main idea is to replace (square-shaped) patches of the original image with the most similar image from a given set of 
images (called tiles). The similarity is measured by the difference between the color histograms of the patch and tiles.
The application is implemented in Python 3.9 and uses the [Stable Diffusion](https://en.wikipedia.org/wiki/Stable_Diffusion) model from [KerasCV](https://github.com/keras-team/keras-cv) submodule of [Keras](https://keras.io/) to create the tiles.

### Getting started

Please before anything make sure that the dependecy packages are installed. You can normally intall the dpeendecies by
exceutign the following command:

```pip install -r reqquireemts.txt```

