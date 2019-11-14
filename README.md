# GDN-Pytorch
This repository is a Pytorch implementation of the paper ["Depth Estimation From a Single Image Using Guided Deep Network"](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=8854079)

Minsoo Song and [Wonjun Kim](https://sites.google.com/site/kudcvlab)  
IEEE Access

Codes will be coming soon!  

<p align="center"><img src='https://github.com/tjqansthd/GDN-Pytorch/blob/master/example/ex.png' width=800></p>  

## Model architecture
<p align="center"><img src='https://github.com/tjqansthd/GDN-Pytorch/blob/master/example/model_architecture.png' width=800></p>  

## Requirements

* Python >= 3.5
* Pytorch 0.4.0
* Ubuntu 16.04
* CUDA 8 (if CUDA available)
* cuDNN (if CUDA available)

## Video
<img src='https://github.com/tjqansthd/GDN-Pytorch/blob/master/example/rgb1.gif' width=400>   <img src='https://github.com/tjqansthd/GDN-Pytorch/blob/master/example/out2.gif' width=400>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;RGB input&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Estimated depth map  

## Results
<p align="center"><img src='https://github.com/tjqansthd/GDN-Pytorch/blob/master/example/result1.png' width=1000></p>

<p align="center"><img src='https://github.com/tjqansthd/GDN-Pytorch/blob/master/example/result2.png' width=1000></p>

<p align="center"><img src='https://github.com/tjqansthd/GDN-Pytorch/blob/master/example/result3.png' width=1000></p>  

1st &nbsp;row: RGB input  
2nd row: Ground truth  
3rd row: Eigen et al.  
4th row: Godard et al.  
5th row: Kuznietsov et al.  
6th row: Ours

## Pretrained models
You can download pretrained color-to-depth model
* [Trained with KITTI](https://drive.google.com/drive/folders/10wFzSDdRK7nlNZXhSP3GGWuWFK_Ap7ur?usp=sharing)

## Demo (Single Image Prediction)
Demo Command Line:
```bash
############### Example of argument usage #####################
python depth_extract.py --gpu_num 0,1 --model_dir your/model/path/model.pkl 
## gpu_num is index of your gpu list.        ex) os.environ["CUDA_VISIBLE_DEVICES"]= args.gpu_num
```

Try it on your own image!
1. Insert your example images(png, jpg) in GDN-pytorch/example/demo_input  
(Since our model was trained at 128 x 416 scale, we recommend resizing the images to the corresponding scale before running the demo.)
2. Specify the model directory, then run the demo. 

## Training
### Training method  
Depth_to_depth network training -> Color_to_depth network training(using pretrained depth_to_depth network)

* Depth_to_depth network training
```bash
python AE_main_final_new_color_4_gen2.py ./your/dataset/path --epochs 50 --batch_size 20 --gpu_num 0,1,2,3 --mode DtoD
```
* Color_to_depth network training
```bash
python depth_extract.py ./your/dataset/path --epochs 50 --batch_size 20 --model_dir your/pretrained/depth_to_depth/model/path --gpu_num 0,1,2,3 --mode RtoD
```
