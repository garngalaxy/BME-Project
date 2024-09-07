# Marmoset Pose Estimation and Segmentation

This is a project for segmenting marmoset monkeys in images using a combination of the YOLO object detection model and the Segment Anything Model (SAM) for accurate segmentation.


## Project outline
1. Dataset and setup data dataframe
2. Fine-turning pose estimation with Utralytics
3. Apply SAM2 to generate masks

## Dataset and setup data dataframe
### Download mamosets 
Download `marmoset-dlc-2021-05-07.zip` from https://benchmark.deeplabcut.org/datasets.html
### Setup project data by creating directory to train YOLOv8 
- Create directory to comply with the YOLO file format structure including main directory [`train`, `validation`] and sub directory [`images`, `labels`]
- Convert the .csv file to a .txt file, then organize the resulting data frame for further processing
- Using data from .txt file to generate keypoints and skeletons on .png image
- Separate file to tran and validation
- Create a yaml file and resize image (512,512)


##  Fine-tuning with YOLOv8
### Train YOLOv8
Install the ultralytics package, which includes the YOLOv8 model. 
 Set up the training parameters including the path to YAML configuration file, the number of training epochs, and the image size.
 Begin the training process using the specified parameters. YOLOv8 models are trained using Visual Studio Code. After training is complete, check the results.
### Plot the results
Plot the results of box estimation and pose estimation.
Compare the labels and predictions.
Export the trained model `yolomodel.pt`


## Apply SAM2 to segment image
### Setup SAM2 model
install the pretrained SAM2 model `sam2_hiera_large.pt` from https://github.com/facebookresearch/segment-anything-2.git <br/>
<i>Note: The SAM2 model needs to be opened in Google Colab.</i>

### Create mask 
Creates binary mask on the image using `show_mask`
Setup the parameters for the mask to display, the color index to choose the overlay color and the axis to plot on
Show points,skeleton and box

### Apply SAM2 model with YOLOv8 to segment image
Install ultralytics package to obtain YOLOv8 and import necessary libraries. Mount google drive to access the `yolomodel.pt` model. Perform object detection and image segmentation using a YOLO model for detection and a SAM for segmentation. 
- Generate a list of image paths from a specific directory, then process each image, detect objects and keypoints using YOLO. 
- Use SAM to generate and visualize segmentation masks based on the detected keypoints
- Process images that involve object detection, keypoint extraction, and segmentation masks to achieve detailed image analysis.

### Create interface with Gradio
An input image undergoes the `predict_image` function to generate an output image by:
- Using a trained YOLOv8 model to generate boxes (with labels) and keypoints.
- Using SAM to overlay masks on the image based on the boxes and keypoints from the YOLOv8 model
