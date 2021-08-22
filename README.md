# You Only Look Once : An Incremental Upadte -  (YOLOv3)

Authors: Mariaos Marianos , Denzil A Joy

Object Identification involves detecting objects in an image and identifying the classes. Before YOLO(You Only Look Once), object detectors were quite
slow as it involves extraction of regions in an image preceding classification. Slower Frames Per Second(FPS) are deterimental for object detection in applications 
such as autonomous driving or fast moving robots.

 Recent  developments  on  algorithms  such  as  R-CNNs  has  a  similar  intention and purpose but using region proposals methods to first generate potential 
 bounding boxes in an image and then run a classifier on these proposed boxes and then classification. Post-processing is used to refine the bounding boxes,  
 eliminate duplicate detections,  and re-score the boxes based on otherobjects in the scene.  These complex pipelines are slow and hard to optimize because each 
 individualcomponent must be trained separately.
 
 To overcome such difficulties, You Only Look Once (YOLO) was proposed, which can be trained end to end and achieve higher frames/second in real-time. The idea 
 behind YOLO is to look only once in an image rather than looking at multiple regions one by one.
 
 This blog is a reproduction of YOLOv3 developed by Joseph Redmon *et al* and reiterated by Ultralytics. Our main objective is to reproduce the results achieved by 
 them while reducing processing time and effort. 
 
 ## 1 YOLO : An introduction
 
 You Only Look Once 
 This is a unique object detection method that was inroduced in 2016. Unlike sliding window and region proposal-based techniques, YOLO sees the entire image
during training and test time so it implicitly encodes contextual information about classes as well as their appearance[1]. Instead of proposing multiple region proposals or a sliding window, here YOLO splits the entire image into a number of grids. Each one of these grid cells will output a number of bounding boxes. The output for each of these prediction boxes is the centre co-ordinates , width and height and the class prediction. This is as shown in the figure below.[2]  

![](http://media5.datahacker.rs/2018/11/slkskssadaw.png)

## 2 What's Changed in Version 3 ?

1) Darknet53 
 
YOLOv3 uses a variant of Darknet, which originally has 53 layer network trained on Imagenet. For the task of detection, 53 more layers are stacked onto it, giving us a 106 layer fully convolutional underlying architecture for YOLOv3.
 
2) Detection at 3 scales

This is one of the most salient features of the detector. It makes detections at three different scales. This is make sure that the smaller objects that may be present in the image do not get ignored as background. The detection is done by applying 1 x 1 detection kernels on feature maps of three different sizes at three different places in the network.

3) Multiple anchor boxes size

Since there are three different scales at which detections are made, 9 anchor boxe sizes are used.

4) More Prediction boxes

5) Changes to the Loss function definition

![](https://i.ibb.co/Mns4J3n/loss-func-yolo.png)

This is mainly divided into bounding box prediction and classification loss.  The main difference in theloss function between YOLO and YOLOv3 is that the last three terms are changed to cross-entropyloss  instead  of  being  squared  loss.   In  other  words,  object  confidence  and  class  predictions  are  nowpredicted through logistic regression.

## Training and Testing

Step-1) Download and run the [Yolov3.ipynb](https://github.com/djoy4/YOLOv3/blob/main/Yolov3.ipynb) file. 

In case you want to make changes to the hyper-parameters, these can be done on the [hyperparameters .yaml file](https://github.com/djoy4/YOLOv3/blob/main/data/hyp.scratch.yaml) as shown in the image below. 
![](https://i.ibb.co/XjKRvwD/hyper-chnage-git.png)

Step-2) For training, run this line 

```bash
!python train.py --epochs 10 --data voc.yaml --cfg yolov3.yaml --weights 'yolov3.pt' --batch-size 64 --noautoanchor --img-size 256
```

Here you can chnage the batch size, image size and also upload different weight files as per your per requirements. 

The arguments that can be provided for the training line are given below.

![](https://i.ibb.co/5T0K5MH/arg-yolov3.png)

Step-3) For testing, run this line in the .ipynb file

```bash
!python test.py --weights '/content/YOLOv3/runs/train/exp/weights/best.pt' --data voc.yaml --img-size 256 --batch-size 64 --task test
```

Step-4) Saving Results and viewing results

Run the following lines to save and view your files

```bash
!zip -r /content/default_train_lrf_best.zip /content/YOLOv3/runs/train/exp
```

This is to zip and save your training weights and results

```bash
!zip -r /content/default_test_lrf_best.zip /content/YOLOv3/runs/test/exp
```

This is to zip and save your testing results


```bash
from google.colab import files
files.download("/content/default_train_lrf_best.zip")
```

```bash
from google.colab import files
files.download("/content/default_test_lrf_best.zip")
```

Finally these lines of code will saved the zipped files. They can be extracted on your local device and the results and graphs can be viewed.


## References
1. Joseph Redmon, Santosh Divvala, Ross Girshick, and Ali Farhadi. You Only Look Once: Unified, Real-Time Object Detection. In2016 IEEE Conference on Computer Vision and Pattern Recognition (CVPR),pages 779–788, Las Vegas, NV, USA, June 2016. IEEE 
2. #029 CNN Yolo Algorithm. (2019, October 26). Master Data Science. http://datahacker.rs/object-detection-yolo-algorithm/
