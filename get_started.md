
### This is a guide on how to install Caffe for Ubuntu 16.04 and above, without GPU support (No CUDA required). 

## Prerequisites:

### OpenCV
``` sudo apt-get install libopencv-dev python-opencv ```



### OpenBLAS OR Atlas
##### OpenBLAS
``` sudo apt-get install libopenblas-dev ```

##### Atlas
``` sudo apt-get install libatlas-base-dev ```



### Boost
``` sudo apt-get install libboost-all-dev ```



### Protobuf (USING PIP)
``` sudo pip install protobuf ```

##### If you don't have ``` pip ``` yet, install it using the following commands:

``` 
sudo apt-get install python-pip python-dev build-essential

sudo pip install --upgrade pip

```


## General Dependencies

``` 
sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler 

sudo apt-get install the python-dev 

sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev 

```

## Getting Caffe
``` 
git clone https://github.com/BVLC/caffe
```

You will now find the ``` caffe ``` folder in your ``` Home ``` directory.

 We have to make a copy of ``` Makefile.config.example ```, which we generally name as, ``` Makefile.config ``` to which we can make changes based on our system settings. 

```
cd caffe
cp Makefile.config.example Makefile.config

```

## Making Changes In ``` Makefile.config ```
Assuming you are still in the ``` caffe ``` directory, use this command to open ``` Makefile.config ```

```
gedit Makefile.config 
```
##### Note- THe following line numbers may vary. 

- On line 8, 
**uncomment** ``` CPU_ONLY := 1 ```


On Line 21, **uncomment** ``` OPENCV_VERSION := 3 ``` if you're using ``` OpenCV 3 ``` or above.
If you aren't sure, try this in another terminal
``` 
$ python
>>> import cv2
>>> cv2.__version__
'3.0.0'
```

- On line 25,
**uncomment** ``` CUSTOM_CXX := g++ ```

- On line 50, 
set ``` BLAS := open ``` if you've installed ``` OpenBLAS ```, or let it be the default ``` BLAS := atlas ``` if you've installed ``` Atlas ```.

- On line 94, **change** 
``` 
INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include
```

to

```
INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include  /usr/include/hdf5/serial 
```

- On line 95, **change**
```
LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib

```

to

```
LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib  /usr/lib/x86_64-linux-gnu/hdf5/serial

```

This should resolve hdf5 errors when running ``` make ```

Now within the ``` caffe ``` directory, run the following one after the other

```
make all
make run
make runtest
```

These should run smoothly without any errors. If you do however, encounter errors, refer the ones at the end of this post or elsewhere to resolve them.

**Make sure to remove build every time you resolve an error, and run those three commands again to rebuild.**

**This is _VERY IMPORTANT_, otherwise the errors will persist.**

**To remove build,**
```
rm -rf ./build*/

```

Once all three run without errors, while in the ``` caffe ``` directory type,
``` make pycaffe ```
This will build a python wrapper. You will also find a python folder within the caffe folder now. 

To use caffe within python, export its path as

```  export PYTHONPATH=~/Home/_username_/caffe/python:$PYTHONPATH ```

Replace ``` _username_ ``` with the your username in the system. 




