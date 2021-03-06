# CnnPythonDeploy
Deployment of the Cnn in Python. Python wrapping for the convolutional neural net classifier. Takes in Gaia Spectrum as a numpy array forinput and returns predicted class. Total pre trained model size roughly 22Mb. Takes on average 0.2ms to load model and classify one Gaia spectrum. Usage instructions below. 

The current version of the model was trained and tested on the 'sigma clipped' spectra, so is unlikly to work well the 'non sigma clipped spectra'. Its accuracy on the test set is 98.90%.

# Contents

1. `model/` contains all the data requited to build the trained tensor
    flow model.

* `model/model-v1.json` meta informationa about model topology used to build the tensorflow graph.

* `model/model-v1.h5` binary file containing all of the trained weights and baises which populate the tensorflow graph.

* `model/classes.npy` contains the mapping from the human readable classes ('SN1a,'SNII etc..) to machine readble classes ([1,3,0...]).

2.  `utils.py` python script containing the prediction function which takes Gaia Spectra and returns classification using tensorflow model. Usage and explaination below.
 
# Prerequisites

You will need the following packages, they can all be installed via pip

1. Tensorflow  [https://www.tensorflow.org/install/]

``` $pip install tensorflow```

2. Keras [https://keras.io/#installation]

``` $pip install keras```

3. H5py [http://docs.h5py.org/en/latest/build.html#install]

``` $pip install h5py```

5. Scikit-learn [http://scikit-learn.org/stable/install.html]

``` $pip install -U scikit-learn```

# Example Usage

This example shows how to classify one Gaia spectrum which is inputted as a numpy array of length 120,
corresponding the number of pixels. The output results contain the predicted class and the corresponding
softmax probabilty associated with that classification. To get
maxium performance it is recomended to pass many spectra into the predict funtion as an array.

Classify one Gaia Spectrum

```
>>> from utils import predict
>>> import numpy
>>> GaiaSpectrum = numpy.array([0.234,...,1.344]
>>> result = predict(GaiaSpectrum)
>>> result['class']
['SN1a']
>>> result['prob']
[0.9978]
```

... Many Gaia Spectra

````
>>> GaiaSpectra = numpy.array([numpy.array([0.234,...,1.344]),...,numpy.array([0.033,....,0.334]))
>>> result = predict(GaiaSpectra)
>>> result['class']
['SN1a',....,'SNII']
>>> result['prob']
[0.9978,....,0.98939]
```

