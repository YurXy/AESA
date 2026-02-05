# AESA 
PyTorch implementation of the paper "[AESA-Net:  Lane Detection with Attention Enhancement Feature Shifting Aggregator]


## Introduction
<img width="654" height="227" alt="image" src="https://github.com/user-attachments/assets/cfefbeb2-fa97-4e38-9911-b558f2d1a2eb" />

AESA-Net network structure diagram

## Get started
1. Clone the AESA repository
    ```
    git clone https://github.com/YurXy/AESA.git
    ```
    We call this directory as `$AESA_ROOT`

2. Create a conda virtual environment and activate it (conda is optional)

    ```Shell
    conda create -n aesa python=3.8 -y
    conda activate aesa
    ```

3. Install dependencies

    ```Shell
    # Install pytorch firstly, the cudatoolkit version should be same in your system. (you can also use pip to install pytorch and torchvision)
    conda install pytorch torchvision cudatoolkit=10.1 -c pytorch

    # Or you can install via pip
    pip install torch torchvision

    # Install python packages
    pip install -r requirements.txt
    ```

4. Data preparation

    Download [CULane](https://xingangpan.github.io/projects/CULane.html) . Then extract them to `$CULANEROOT` . Create link to `data` directory.
    
    ```Shell
    cd $RESA_ROOT
    mkdir -p data
    ln -s $CULANEROOT data/CULane
    ```

    For CULane, you should have structure like this:
    ```
    $CULANEROOT/driver_xx_xxframe    # data folders x6
    $CULANEROOT/laneseg_label_w16    # lane segmentation labels
    $CULANEROOT/list                 # data lists
    ```



5. Install CULane evaluation tools. 

    This tools requires OpenCV C++. Please follow [here](https://docs.opencv.org/master/d7/d9f/tutorial_linux_install.html) to install OpenCV C++.  Or just install opencv with command `sudo apt-get install libopencv-dev`

    
    Then compile the evaluation tool of CULane.
    ```Shell
    cd $RESA_ROOT/runner/evaluator/culane/lane_evaluation
    make
    cd -
    ```
    
    Note that, the default `opencv` version is 3. If you use opencv2, please modify the `OPENCV_VERSION := 3` to `OPENCV_VERSION := 2` in the `Makefile`.


## Training

For training, run

```Shell
python main.py [configs/path_to_your_config] --gpus [gpu_ids]
```


For example, run
```Shell
python main.py configs/culane.py --gpus 0 1 2 3
```

## Testing
For testing, run
```Shell
python main.py c[configs/path_to_your_config] --validate --load_from [path_to_your_model] [gpu_num]
```

For example, run
```Shell
python main.py configs/culane.py --validate --load_from culane_resnet50.pth --gpus 0 1 2 3

python main.py configs/tusimple.py --validate --load_from tusimple_resnet34.pth --gpus 0 1 2 3
```


We provide one trained ResNet models on CULane, downloading our best performed model (
CULane: [BaiduDrive(code:abcd)]([https://pan.baidu.com/s/1ODKAZxpKrZIPXyaNnxcV3g](https://pan.baidu.com/s/1Cnkdhyt0-Gm08kOVnjiTSw))
)

## Visualization
Just add `--view`.

For example:
```Shell
python main.py configs/culane.py --validate --load_from culane_resnet50.pth --gpus 0 1 2 3 --view
```
You will get the result in the directory: `work_dirs/[DATASET]/xxx/vis`.

## Citation
If you use our method, please consider citing:
```BibTeX
@inproceedings{
}
```

<!-- ## Thanks

The evaluation code is modified from [SCNN](https://github.com/XingangPan/SCNN)
