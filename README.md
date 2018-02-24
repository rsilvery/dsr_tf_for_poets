# Image Classification using TensorFlow in the MapR Data Science Refinery

In this demo we will take a transfer-learned Inception_V3 model and use it to correctly label different types of flowers via image classification.

Model is taken from the Google Codelab tutorial [TensorFlow for Poets](https://codelabs.developers.google.com/codelabs/tensorflow-for-poets/#0) and has been retrained on flower photos in the data set located [here](http://download.tensorflow.org/example_images/flower_photos.tgz).

* Note: you have to do some conversion on these photos or install tooling to handle JPEGs. I've uploaded 10 sample PNG flowers to the [flowers directory](/flowers/)

## Steps

### Load Files

Place the training image set for flowers in your MapR global namespace (assuming /user/mapr). This can be found [here](http://download.tensorflow.org/example_images/flower_photos.tgz).

```
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

### Import Notebook










