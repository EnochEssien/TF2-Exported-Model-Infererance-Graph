# TF2-Exported-Model-Infererance-Graph
A simple google colab script to aid in saving trained object detectors, as from my experience there was a couple of compatibility issues with the version of tensorflow, The Object detection API, Python and tf_slim. All this made saving my trained models a bigger hassle than it needed to be.

## Installation

To run this code, you need to install the following libraries:

- TensorFlow
- TensorFlow IO
- Protobuf
- TensorFlow Object Detection API
- OpenCV (opencv-python)
- Numpy (version 1.23)
- LVIS
- absl-py
- Pandas
- Cython

You can install these libraries by running the following commands:

```python
!pip install --upgrade pip
!pip install tensorflow
!pip install tensorflow.io
!pip install protobuf
!pip install tensorflow-object-detection-api
!pip install opencv-python
!pip install numpy==1.23
!pip install lvis
!pip install absl-py
!pip install pandas
!pip install cython
```

## TensorFlow Object Detection API Setup

1. Mount Google Drive:

```python
from google.colab import drive
drive.mount('/content/gdrive')
```

2. Change the current working directory to the location of the TensorFlow Object Detection API code:

```python
%cd /content/gdrive/My Drive/ModelsTF2/research
```

3. Compile the protocol buffer files:

```python
!protoc object_detection/protos/*.proto --python_out=.
```

4. Build and install the TensorFlow Object Detection API:

```python
%cd /content/gdrive/My Drive/ModelsTF2/research/object_detection/packages/tf2
!python setup.py build
!python setup.py install
```

5. Set the PYTHONPATH environment variable to include the necessary directories:

```python
%cd /content/gdrive/My Drive/models/research/object_detection
os.environ['PYTHONPATH'] += ':/content/gdrive/My Drive/ModelsTF2/research/:/content/gdrive/My Drive/Tensorflow/models/research/slim'
```

## Test Installed API

To ensure that the TensorFlow Object Detection API is installed correctly, you can run the following test:

```python
%cd /content/gdrive/My Drive/ModelsTF2/research
!python object_detection/builders/model_builder_tf2_test.py
```

## Export and Save Trained Object Detection Model

To export and save a trained object detection model, follow these steps:

1. Change the current working directory to the object detection folder:

```python
%cd '/content/gdrive/My Drive/ModelsTF2/research/object_detection'
```

2. Run the exporter script with the desired parameters:

```python
!python exporter_main_v2.py --input_type image_tensor --pipeline_config_path training/pipeline.config --trained_checkpoint_dir training --output_directory exported-models/FaceMaskDetectorV1
```

Make sure to adjust the parameters (`--pipeline_config_path`, `--trained_checkpoint_dir`, and `--output_directory`) according to your specific model configuration and file paths.

That's it! You should now have a trained object detection model exported and saved in the specified output directory.
