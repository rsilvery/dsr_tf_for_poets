# Image Classification using TensorFlow in the MapR Data Science Refinery

In this demo we will take a transfer-learned model and use it to correctly label different types of flowers via image classification. 

Model is taken from the Google Codelab tutorial [TensorFlow for Poets](https://codelabs.developers.google.com/codelabs/tensorflow-for-poets/#0) and has been retrained using [Inception-V3](https://www.tensorflow.org/tutorials/image_recognition) on flower photos in the data set located [here](http://download.tensorflow.org/example_images/flower_photos.tgz). Retraining on an M4XLarge instance takes ~45 minutes. In order to make reproducing this demo quick, we've also provided the retrained [model]() and [labels]() to you in the repo.


## Steps

### Load Files (if you plan to do the training yourself)

Place the training image set and script in your MapR global namespace (assuming /user/mapr). This can be found [here](http://download.tensorflow.org/example_images/flower_photos.tgz).

```
wget -P /mapr/my.cluster.com/user/mapr/ https://github.com/googlecodelabs/tensorflow-for-poets-2/blob/master/scripts/retrain.py
wget http://download.tensorflow.org/example_images/flower_photos.tgz .
tar -xvzf flower_photos.tgz -C /mapr/my.cluster.com/user/mapr/flowers/
```

### Start DSR

Start the MapR Data Science Refinery Container containing Apache Zeppelin. 
Steps for doing this in Linux can be found [here](https://community.mapr.com/community/products/mapr-converged-platform/data-refinery/blog/2017/12/17/how-to-run-data-science-refinery-from-an-edge-node).

### Install TensorFlow

From inside the container, run the following to install TensorFlow - can also be done in DockerFile:

```
sudo -u root pip install tensorflow
```

More detail can be found [here](https://community.mapr.com/community/products/mapr-converged-platform/data-refinery/blog/2017/12/04/how-to-using-tensorflow-with-the-mapr-data-science-refinery)


### Move the model and labels to your global namespace at /mapr/my.cluster.com/user/mapr/flowers/

#### If you want to train the model yourself on these photos (or whatever photos), you can use these commands:

```
python /mapr/my.cluster.com/user/mapr/retrain.py --image_dir /mapr/my.cluster.com/user/mapr/flowers/flower_photos
[...]
INFO:tensorflow:Final test accuracy = 90.5% (N=378)

mv /tmp/output_* /mapr/my.cluster.com/user/mapr/flowers/
```

This will train the model and drop the trained model into your container /tmp/ directory along with the labels file.


#### If you just want to get started with the model, you can copy the prepared model and labels to your filespace:
```
wget -P /mapr/my.cluster.com/user/mapr/flowers/ 
```

Note: if you want to use Tensorboard to follow the training, you have to pass in the port it's going to run on into the Docker Run command as a port mapping (ex. -p 6006:6006)

### Import Notebook to view and test model

This notebook <name> does the following:

* Test that TensorFlow is installed and working











