# TF transfer learning on an image list

The adapted code provides the original TensorFlow (TF) hub example on transfer learning adjusted to ingest lists of image paths. Doing so, you avoid moving large amounts of image files into their respective working directories (per standard example).

## Installation

Follow the standard installation instructions of all pre-requisites provided by the [Tensorflow Hub transfer learning example](https://www.tensorflow.org/hub/tutorials/image_retraining).

## Use

Instead of using the retrain.py or label_image.py code, from the standard example, use the retrain_image_list.py and label_image_list.py code in this repository.

In addition you will need a CSV file specifying:

-  a **files** column with the full paths of your source images for training
-  a **labels** column which provides the label you associated with the content of the image


| files,   |      labels   |
|----------|:-------------:|
| /my/location/1.jpg, |  cat |
| /my/location/2.jpg, |    dog   |
| ..., |    ...   |

Other information in this file will be ignored.

### retraining image labels

To retrain the model a new argument is introduced, **image_file**.  The **image_file** argument specifies the location the csv file containing image and label information as outlined above. Other arugments remain unchanged.

```bash
# train the model
python ../python/retrain_image_list.py \
--image_file "/csv/file/location/image_files.csv" \
--flip_left_righ True \
--random_scale 10 \
--random_brightness 5 \
--how_many_training_steps 4000 \
--output_labels "~/your_labels.txt" \
--output_graph "~/your_graph.pb"

```

### classifying images

Similar to the retraining code an **image_list** parameter was added to the original label.py script. This list only requires a **files** column which specifies the location of images you want to see classified.

```bash
# classify data
python ../python/label_image_list.py \
--image_list="../../data/crop_growth_labels.csv" \
--labels="~/your_labels.txt" \
--graph="~/your_graph.pb" \
--output_layer="final_result"
```