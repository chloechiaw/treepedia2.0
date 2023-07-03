The receptive field refers to the area in the input image that a neuron is influenced by. In FCNs, due to their architecture, each neuron's receptive field is relatively small compared to the size of high-resolution remote sensing images (RSIs).

designed to perform convolutional operations on local patches of an image. This design choice allows FCNs to efficiently process images by sharing weights across spatial locations. 
-  small neighboring region refers to a local patch or receptive field around each pixel. The size of this patch is determined by the kernel size and stride used in convolutional operations.


Transformers 
- Transformer-based architectures leverage self-attention mechanisms that allow for capturing long-range dependencies by considering all pixels in the image simultaneously during computation.

Mask Transformer
(MaskFormer) [4], which uses a mask classification approach
that is particularly well suited to deal with the large intra-
class variance and small inter-class variance features of RSIs.
Mask classification involves predicting a set of binary masks
and assigning a class to each mask. 

Mask classification is a process in which a model predicts a set of binary masks and assigns a class label to each mask. This technique is particularly useful for tasks like semantic segmentation of high-resolution remote sensing images, where capturing both background and local information is crucial. By generating masks for specific categories, the model can perform detailed segmentation, effectively handling the large within-class and small inter-class variance of the images.

## Specific to Cityscapes pretrained
In the case of semantic segmentation with 19 classes using a pretrained Mask2Former model on Cityscapes dataset, the model would generate 19 binary masks corresponding to each class.

Each pixel in these generated masks would have either a value of 1 (indicating that it belongs to that particular class) or 0 (indicating it does not belong to that class). By combining these individual binary masks together based on their predicted values at each pixel location, we can obtain detailed segmentation results for different objects/classes present in an image.

## BIG IDEA
By generating separate masks for each category/class, the Mask2Former model can capture these fine-grained details and effectively segment them
Each position in the input sequence (in this case, an image) to attend to all other positions and learn their relationships.
