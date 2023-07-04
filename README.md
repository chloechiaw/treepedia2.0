## Mask2Former architecture

Mask2Former adopts the same meta architecture as MaskFormer [14] with a backbone, a
pixel decoder and a Transformer decoder. We propose a new
Transformer decoder with masked attention instead of the standard
cross-attention (Section 3.2.1).

## Relevant variable descriptions 
- batch[original_segmentation_maps][0] = the ground truth segmentation maps for the 0th image 
- batch[predicted_segmentation_maps][0] = performing inference and the predicted seg map from the model for the 0th image
- you can only do batch[original_segmentation_maps][0] or batch[original_segmentation_maps][1]. that means there are only 2 images in each batch

## Transposing 
Pytorch typically accesses images in Channel, Height, Width format. Thus, in the Image Dataset class, you'll need to transpose the images like image.transpose(2,0,1). The typical default format in Height, Width, Channel. So 2,0,1 refers to the indexes. 
## In each dataloader 

pixel_values torch.Size([2, 3, 512, 512]) -> 2 images in each batch, 3 color channels, 512 pixel x 512 
pixel_mask torch.Size([2, 512, 512])
mask_labels torch.Size([9, 512, 512]) -> 9 segmentation masks in each batch 
class_labels torch.Size([9]) -> total of 9 class labels 
original_images (1080, 1920, 3) -> og images are 1080 by 1920 and 3 color channels 
original_segmentation_maps (1080, 1920)

# Batch Size 
- Batch refers to a subset of the entire dataset that is processed together during each iteration of training
- YOU PROCESS one batch at a time!!
- If batch-size is set to 16, each each will contain 16 images and 16 corresponding masks
- The total umber of samples needs to be divisible by the batch_size
- Connection to Dataloader:   for idx, batch in enumerate(tqdm(train_dataloader)): # this iterates through all the batches. one for loop = one batch is put through the training loop. train_dataloader is loading in the batches


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

