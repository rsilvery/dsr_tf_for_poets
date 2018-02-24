# Image Classification using TensorFlow in the MapR Data Science Refinery

In this demo we will take a transfer-learned Inception_V3 model and use it to correctly label different types of flowers via image classification. 

Code is taken from the Google Codelab tutorial [TensorFlow for Poets](https://codelabs.developers.google.com/codelabs/tensorflow-for-poets/#0) and has been retrained on flower photos in the data set located [here](http://download.tensorflow.org/example_images/flower_photos.tgz). Retraining on an M4XLarge instance takes ~ hours. In order to make this demo useful, we've provided the retrained model to you [here](LINK).


## Steps

### Load Files (if you plan to do the training yourself)

Place the training image set and script in your MapR global namespace (assuming /user/mapr). This can be found [here](http://download.tensorflow.org/example_images/flower_photos.tgz).

```
wget -P /mapr/my.cluster.com/user/mapr/ https://github.com/googlecodelabs/tensorflow-for-poets-2/blob/master/scripts/retrain.py
wget http://download.tensorflow.org/example_images/flower_photos.tgz .
tar -xvzf flower_photos.tgz -C /mapr/my.cluster.com/user/mapr/
```

### Start DSR

Start the MapR Data Science Refinery Container containing Apache Zeppelin. 
Steps for doing this in Linux can be found [here](https://community.mapr.com/community/products/mapr-converged-platform/data-refinery/blog/2017/12/17/how-to-run-data-science-refinery-from-an-edge-node).

### Install TensorFlow

From inside the container, run the following to install TensorFlow:

```
sudo -u root pip install tensorflow
```

More detail can be found [here](https://community.mapr.com/community/products/mapr-converged-platform/data-refinery/blog/2017/12/04/how-to-using-tensorflow-with-the-mapr-data-science-refinery)


### Train model or copy [model]() and [labels file]() to your global namespace at /mapr/my.cluster.com/user/mapr/



### Import Notebook to view and test model

This notebook <name> does the following:

* Test that TensorFlow is installed and working











