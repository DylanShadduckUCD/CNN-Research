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
training. To start I have narrowed my focus from the 26 available columns down
to just one. Each element in the column represents the salinity of the selected
station in $/mu S/cm$
