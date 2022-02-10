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


## Acessing Data

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

### Mac/Windows

Using an unzipping tool of your choice. On Mac the default is 'Archive Utility'.
Linux does not have a default unzip tool. For help with unzipping files, you 
can follow [this](https://linuxize.com/post/how-to-unzip-files-in-linux/) 
tutorial. This tool will automatically unzip the files to a folder with the name 
of the original zipped file. To achieve the same results as the windows set up, 
the contents of this folder will needed to be relocated one directory up. At this
point you may delete the folder that our data was extracted into. Now you 
should have two items in the '*/data*' folder: a zipped file titled 
'ec_postpro_merged' and a '.csv' file with the same name. You may delete the 
zipped file at this point.