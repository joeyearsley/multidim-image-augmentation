# Multidimensional (2D and 3D) Image Augmentation for TensorFlow

This package provides TensorFlow Ops for multidimensional volumetric image
augmentation.

## Differences from the main branch
* Can use current tensorflow installed via pip
* Only uses the pytests instead of cc_test
* Can't generate a python file automatically so you will need to write the
 documentation and interface manually.

## Install prerequities

This project usings the [bazel build
system](https://docs.bazel.build/versions/master/install.html)

## Build and test

To fetch the code, build it, and run tests:

```shell
git clone https://github.com/deepmind/multidim-image-augmentation.git
cd multidim-image-augmentation/
bazel test -c opt //...
```

To learn more about image augmentation, see the [primer](doc/index.md)

For simple API usage examples, see the python test code.
