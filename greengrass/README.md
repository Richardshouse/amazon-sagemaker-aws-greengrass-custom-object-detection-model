# Deploy Object Detection model to the edge

## Set up environment and AWS IoT Greengrass Core on edge device

### Install machine learning dependencies on the device

If your device has GPU, make sure you have the GPU drivers, such as [CUDA](https://developer.nvidia.com/cuda-downloads), installed. If your device only has CPU, you can still run the inference but with slower performance. 

The built-in SageMaker object detection model is written in MXNet. To run inference on the edge, you need to install the mxnet library on your device. Refer to the [MXNet install documentation](http://mxnet.incubator.apache.org/versions/master/install/) for the version that matches the CUDA driver. For example, we installed CUDA 10.1 on the Ubuntu instance, so we installed `mxnet-cu101`

```
$ sudo pip2 install mxnet-cu101
```

Since OpenCV is also fairly large dependency, let's install it on our device too:

```
$ sudo pip2 install opencv-python
```

> Note 1: The reason we use sudo here is because IoT Greengrass runs under `ggc_user`. Regular pip install will install it under your OS user, which `ggc_user` won’t have access to. Alternatively you could install the packages somewhere else as long as `ggc_user` can access that directory.
> 
> Note 2: The reason we use pip2 here is because we use `greengo` in this blog to set up Greengrass, which only supports python2 at the moment. 