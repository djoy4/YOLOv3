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
 
 
