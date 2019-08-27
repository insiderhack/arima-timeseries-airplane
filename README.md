# Time Series Forecast : A basic introduction using Python.

Time series data is an important source for information and strategy used in various businesses. From a conventional finance industry to education industry, they play a major role in understanding a lot of details on specific factors with respect to time.

Time series forecasting is basically the machine learning modeling for Time Series data (years, days, hours…etc.)for predicting future values using Time Series modeling .This helps if your data in serially correlated. Loading and Handling Time Series in Pandas.

I will be using python in jupyter notebook. Pandas in python has libraries that are specific to handling time series object .

Let's start with the Preliminaries
```
import pandas as pd
import numpy as np
import matplotlib.pylab as plt
%matplotlib inline
```
To load the data- I have provided the link to my GitHub where the dataset and the code is available. I will be using the AirPassenger dataset from. Are you ready?

```
data = pd.read_csv('AirPassengers.csv')
print data.head()
print '\n Data Types:'
print data.dtypes
```

### Install Libraries

!pip install or !apt-get install

```
!pip3 install tensorflow==1.8
!pip3 install keras
!pip3 install torch torchvision
!apt-get install python-numpy python-scipy
```
### Install OpenCV for c/c++

```
!apt-get install -qq gcc-5 g++-5 -y
!ln -s /usr/bin/gcc-5 
!ln -s /usr/bin/g++-5 

!sudo apt-get update
!sudo apt-get upgrade

#Install Dependencies
!sudo apt-get install -y build-essential 
!sudo apt-get install -y cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
#The following command is needed to process images:
!sudo apt-get install -y python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev
#To process videos:
!sudo apt-get install -y libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
!sudo apt-get install -y libxvidcore-dev libx264-dev
#For GUI:
!sudo apt-get install -y libgtk-3-dev
#For optimization:
!sudo apt-get install -y libatlas-base-dev gfortran pylint
!wget https://github.com/opencv/opencv/archive/3.4.0.zip -O opencv-3.4.0.zip
!sudo apt-get install unzip
!unzip opencv-3.4.0.zip
%cd opencv-3.4.0
!mkdir build
%cd build
!cmake -D WITH_TBB=ON -D WITH_OPENMP=ON -D WITH_IPP=ON -D CMAKE_BUILD_TYPE=RELEASE -D BUILD_EXAMPLES=OFF -D WITH_NVCUVID=ON -D WITH_CUDA=OFF -D BUILD_DOCS=OFF -D BUILD_PERF_TESTS=OFF -D BUILD_TESTS=OFF -D WITH_CSTRIPES=ON -D WITH_OPENCL=ON CMAKE_INSTALL_PREFIX=/usr/local/ ..
!make -j`nproc`
!sudo make install

```
### Cloning Github Repo to Google Colab

```
!git clone https://github.com/ildoonet/tf-pose-estimation.git
```
### Mount your Google Drive

```
from google.colab import drive
drive.mount('/content/drive/')
```

### Check your Folder Data

```
!ls Drive/test
```

### Upload code from your system

```
from google.colab import files
uploaded = files.upload()
```
### Make zip file of your Data

```
from google.colab import files
import zipfile
import sys
foldername = 'your folder or filename'
zipfile.ZipFile('Drive/'+foldername + '.zip', 'w', zipfile.ZIP_DEFLATED)
```

### Downloading the data from the colab

```
from google.colab import files
files.download('Drive/test.zip')
```

sources : 
https://github.com/savankoradiya/
https://github.com/humaun21/
