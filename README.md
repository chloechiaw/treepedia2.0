## Intersection Over Union 
IoU is the area of overlap between the predicted segmentation and the ground truth divided by the area of union between the predicted segmentation and the ground truth.

For multi-class segmentation: the mean IOU is calculated by taking the IOU of each class and averaging them. 


Color Palette is loaded as RGB, but for the ground truth color seg map the colors are converted to BGR 

RGB: 
[255, 255, 255], [255,0,0], [255,255,0], [0,0,255], [159,129,183], [0,255,0], [255,195, 128]

BGR: 
[255, 255, 255] -> [255, 255, 255]
[255, 0, 0] -> [0, 0, 255]
[255, 255, 0] -> [0, 255, 255]
[0, 0, 255] -> [255, 0, 0]
[159, 129, 183] -> [183, 129, 159]
[0, 255, 0] -> [0, 255, 0]
[255, 195, 128] -> [128, 195, 255]

