# CNN-Research (Overview)

This repository hosts the culmination of my Master's research at 
UC Davis in Electrical Engineering/Digital Signal Processing. 

I took part in a research project in association with the department 
of water resources (DWR) and helped to design a Convolutional Neural 
Network trained (CNN) on data provided by DWR. This purpose of this
CNN is to improve the training of other networks designed for DWR by 
helping to fill in missing data. The idea is to use machine learning
to predict what the missing data would most likely be. With the data 
now filled in, it can be used by other Machine learning programs to 
make better informed predicitons.

## Getting Started

### Mac/Linux:

First, clone this repository using git. You can either clone using ssh
or by using your github username and password. If you already have
an ssh key added to your github account type the following into the 
terminal. Make sure you are in a folder or directory on your local 
machine that you have write access to and are comfortable downloading 
this repository to. 

In a terminal type the following:

```
cd /path/to/local/cloned/repo
```

'/path/to/local/cloned/repo' can be any folder of your choice that
you have write access to.

```
git clone git@github.com:DylanShadduckUCD/CNN-Research.git
```

This action should promp you for your ssh key password. Type your
password and allow the download to complete

**If you do not have an ssh key set up** clone the repository using

```
git clone https://github.com/DylanShadduckUCD/CNN-Research.git
```

### Windows

Download git bash to your machine. This application allows you to use
a bash terminal (similar to Mac and Linux) and has the git package
already installed. Now you can clone the repository following the 
same steps as outlined in the Mac/Linux section


## Accessing Data

The dataset for this project is exceptionally large. For that reason
the dataset has been compressed into a zip folder. You must unzip this
folder within the data folder of this repository. This is necessary such
that the jupyter notebook for this project runs seemlessly. Alternatively,
you may unzip the data wherever you would like and make sure to update the
path to the dataset in the jupyter notebook titled *CNN_vs_CS.ipynb* in the 
'*/resources*' folder.

### Windows

To extract the zipped data, navigate to the '*/data*' folder and right click
on '*ec_postpro_merged.zip*'. Select extract all and make sure the destination
to extract files is the same as the location to your data folder. This location
should be '/path/to/local/cloned/repo/data'. Note, the default location will 
include another folder within data labeled 'ec_postpro_merged'. You should now
have two items in your data folder, a zipped file titled 'ec_postpro_merged' 
and a '.csv' file with the same name. At this point the zipped file can be 
deleted. 

### Mac

Using an unzipping tool of your choice. On Mac the default is 'Archive Utility'.
Linux does not have a default unzip tool. This tool will automatically unzip the 
files to a folder with the name of the original zipped file. To achieve the same 
results as the windows set up, the contents of this folder will needed to be 
relocated one directory up. At this point you may delete the folder that our data
was extracted into. Now you should have two items in the '*/data*' folder: a 
zipped file titled 'ec_postpro_merged' and a '.csv' file with the same name. 
You may delete the zipped file at this point.

### Linux 
For help with unzipping files, you can follow [this](https://linuxize.com/post/how-to-unzip-files-in-linux/) 
tutorial. Now you should have the 'ec_postpro_merged' file extracted from the 
zipped folder. You can remove the zipped file from the '*/data*' folder by 
typing the following into the command line:

```
cd /path/to/local/cloned/repo/data
rm ec_postpro_merged.zip
```

Note: you must have write permissions in this folder to perform this removeal step

## Running CNN

### Local Jupyter Notebook

This is my preferred method for running the CNN. To run the notebook 
several dependencies must be met

#### Python Package Dependencies
* Jupyter Notebook 6.4.3+
* TensorFlow 2.3+
* Numpy 1.21.2+
* Pandas 1.2.4+
* Matplotlib 3.4.2+
* Scikit-Learn 0.24.2+

Once these dependencies have been met. Open a jupyter notebook session in 
'/path/to/local/cloned/repo' directory. 

### Google Colab

To avoid dependency issues, this repository in its current state can be 
added to google drive (anywhere you like) and then the notebook file can be run
as a google colab document. Google colab operates very similarly to a local 
jupyter notebook, but the session where the python kernel is hosted does not exist
on your local machine, but rather it is hosted by google on a remote server.

Ensure that if you are running this notebook from within colab that you update the
notebook to reflect this. In the second code cell, change the boolean variable
'using_colab' to True. Also ensure that the 'google_drive_dir" is updated to reflect
the folder you placed this repository data in.

## CNN Pipeline

In this section I will breifly cover the methods used to prepare the dataset for 
CNN training and describe the CNN model and how to use it.

### Data Preparation

Once the ec_postpro_merged dataset has been loaded into the notebook as a pandas
dataframe, there is some work to be done to prepare this raw dataset for CNN 
training. 

To start I have narrowed my focus from the 26 available columns down
to just one. Each element in the column represents the salinity of the selected
station in micro S/cm (micro Siemens per centimeter). One observation is that 
there are a large number of entries with extremely large negative values (on the
order of -1e38). micro S/cm is a measurement of conductivity to indicate salinity
and therefore can't have negative values. These observations are likely an error
on the data recording side and need to be replaced with nans. 

The next task is to accumulate sequential data. The CNN model will be trained on
windows of 500 samples with some portion of those 500 missing. To properly evaluate
the success of the CNN, we need ground truth data to start with. This means searching
through the dataset of our selected column and keeping a subset where each entry is
a vector of length 500 sequential salinity values. This ensures that the CNN is trained
on sequential data and can identify relevant time domain patterns to accurately 
predict and fill in missing values. The output of this step should be a large matrix
of 500 sample vectors.

Following sample selection, the dataset must be scaled. The reason for this has to
do with the activation function used by the convolutional layers of the CNN. The
activation function we have chosen is the rectified linear unit or (RELU) function.
This function is defined for all positive values, but it can more quickly produce
accurate gradients for small values. So, to speed up the training of our network
the data is scaled between a range of 0 to 1 following a linear transformation.

Next we must mask our dataset. This is needed for training so that the input 
data has some missing values and we retain knowledge of the original values that
were removed. This allows for accurate evaluation of the network after training.
You can see that there are two options for data masking: WRITE_TO_CSV and READ_FROM_CSV.
These options are in place for the reason of sharing data between colleagues. 
Another colleague of mine is working on the same problem using compressed sensing
and the best way to evaluate the performance of the two methods agaist one another is
to ensure that we are training and testing our models on the exact same data. 
To use the data further along the pipeline, you must first write the mask and data
to seperate csv files. All subsequent runs can then use the same data and mask files
to train the CNN.

Finally the data is split into two sets: one for training and another for testing.

### CNN Design

This convolutional neural network is designed to fill in missing data for a single
station of salinity data. The location of the missing region to be filled in by the
network is not fixed, so for any window of 500 samples, any amount of data can be 
missing and the network will attempt to fill in as best it can. To accomplish this
task, the output of the neural network must be the same shape as the original 
500 sample data input. This way, any data in any position can be imputed/filled in
without altering the structure of the neural network. A network that has the same
shape at the output and input is generally known as an autoencoder. This name derives
from a symmetrical structure of "two" networks. The first "network" is the encoder 
structure that takes an input and compresses the information by reducing the dimension
of the input. The second "network" performs the inverse operation. It takes compressed
or "encoded" information and recreates the original information to the best of its
ability. In practice these two networks are encompassed into a single neural network.
The model I have designed utilizes convolutional layers for compressing data and 
convoltion transpose layers for uncompressing data. The structure used in this 
research can be seen below. 
![cnn_structure](/images/cnn_layers.png)
