# Image Classification using TensorFlow in the MapR Data Science Refinery

In this demo we will take a transfer-learned model and retrain it to correctly label 5 types of flowers it hasn't encountered via image classification. Then we will test this with an image outside of our training set to make sure that this works.

Model is taken from the Google Codelab tutorial [TensorFlow for Poets](https://codelabs.developers.google.com/codelabs/tensorflow-for-poets/#0) and has been retrained using [Inception-V3](https://www.tensorflow.org/tutorials/image_recognition) on flower photos in the data set located [here](http://download.tensorflow.org/example_images/flower_photos.tgz). Retraining on an M4XLarge instance takes ~45 minutes. In order to make reproducing this demo quick, we've also provided the retrained [model]() and [labels]() to you in the repo.


## Steps

### Load Files 

If you plan to do the training yourself, load the files you will need:

#### Place the training image set and script in your MapR global namespace (assuming /user/mapr). This can be found [here](http://download.tensorflow.org/example_images/flower_photos.tgz).

```
wget -P /mapr/my.cluster.com/user/mapr/ https://raw.githubusercontent.com/googlecodelabs/tensorflow-for-poets-2/master/scripts/retrain.py
wget http://download.tensorflow.org/example_images/flower_photos.tgz .
tar -xvzf flower_photos.tgz -C /mapr/my.cluster.com/user/mapr/flowers/
```

#### If not, load the provided model and labels file to your global namespace (/user/mapr/flowers/):

* [Model](https://github.com/rsilvery/dsr_tf_for_poets/blob/master/flowers/output_graph.pb)
* [Labels](https://github.com/rsilvery/dsr_tf_for_poets/blob/master/flowers/output_labels.txt)


#### Load a test image

In order to test if your model is performing correctly, you will need an image of a daisy, dandelion, roses, sunflower, or tulip. I've provided an example file [here](flowers/mapr_flower.png) that you can load into your namespace (/user/mapr/flowers).


### Start DSR

Start the MapR Data Science Refinery Container containing Apache Zeppelin. 
Steps for doing this in Linux can be found [here](https://community.mapr.com/community/products/mapr-converged-platform/data-refinery/blog/2017/12/17/how-to-run-data-science-refinery-from-an-edge-node).

### Install TensorFlow

From inside the container, run the following to install TensorFlow - can also be done in DockerFile:

```
sudo -u root pip install tensorflow
```

More detail can be found [here](https://community.mapr.com/community/products/mapr-converged-platform/data-refinery/blog/2017/12/04/how-to-using-tensorflow-with-the-mapr-data-science-refinery)



#### If you want to train the model yourself on these photos (or whatever photos), you can use these commands:

```
python /mapr/my.cluster.com/user/mapr/retrain.py --image_dir /mapr/my.cluster.com/user/mapr/flowers/flower_photos --output_graph /mapr/my.cluster.com/user/mapr/flowers/ --output_labels /mapr/my.cluster.com/user/mapr/flowers/
[...]
INFO:tensorflow:Final test accuracy = 90.5% (N=378)

```

This will retrain the model on the Flowers dataset and drop the retrained model into your container /user/mapr/flowers/ directory along with the labels file. 


Note: if you want to use Tensorboard to follow the training, you have to pass in the port it's going to run on into the Docker Run command as a port mapping (ex. -p 6006:6006)

### Import Notebook to view and test model

This Image Classification with Tensorflow notebook does the following:

* Loads an image from your namespace that is a PNG and saved as /user/mapr/flowers/mapr_flower.png
* Processes this image using the retrained model and provides guesses as to what label to apply
* Display flower image

To import this, download this [notebook](/flowers/Image_Classification_with_Tensorflow.json) and then import into Zeppelin.


And this was so much fun, I did the same thing using the [Stanford Dogs Dataset](http://vision.stanford.edu/aditya86/ImageNetDogs/) to classify my dog!











