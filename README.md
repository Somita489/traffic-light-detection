# DA213 Course Project: Traffic Light Detection

## Overview:
This project detects traffic lights in different environmental conditions for example-rainy days or at night time using a YOLO object detection model and determines the light color (Red, Green, or Yellow).The system first uses YOLO to draw a bounding box around the traffic light and then convert RGB to HSV and calculate the probability for each color.The color with the maximum probability is considered the final output.


##  Dependencies

### Environment: 
Google Colab is used to run all the commands because of the ease of importing models and dataset without using local memory. Also a GPU runtime (like Tesla T4) helps us speed up the training process.

### Python Libraries:
- ultralytics (for the YOLO model)
- roboflow (for dataset downloading)
- opencv-python (cv2, for image processing and HSV filtering)
- numpy (for array operations and pixel counting)
- matplotlib (for displaying the output images)

## Brief Description of Files

- traffic_light_detection.py : 
  This is the main and only source code file for the project. It contains the entire pipeline, including:
    * Installing dependencies and mounting Google Drive.
    * Downloading the dataset from Roboflow.
    * Training the YOLO model (`yolo26n.pt`) and saving the weights.
    * The `analyze_traffic_lights()` function which takes the YOLO bounding box, masks it to include only the box, converts the cropped image to HSV color space, calculates color percentages, and annotates the original image.
    * The `detect_lights()` function is used to process test images and show the results of the model.


## How to Run the Code

### Step 1: Setup Environment
Upload the `best.pt` file to Google Drive. Ensure  Colab runtime is using a GPU (Runtime -> Change runtime type -> T4 GPU).
Mount Google Drive and import the model `best.pt` from there.(If necessary,change the link for mounting the drive).
This is to be done if you do not want to train the model which may take 2 hours.

### Step 2: Update API Key (For Training Only)
For retraining the model,the dataset also has to be imported from Roboflow for which we need an API KEY
    rf = Roboflow(api_key="YOUR_API_KEY")
If we want to test the pre trained model, we can skip this step and run the subsequent code blocks and finally the function detect_lights() which gives the result on the test images.

### Step 3: Update File Paths
Ensure that the path of the model and the test images are replaced with the actual path.If we are saving our model and test images on drive,change the paths accordingly.
    - Model weights path : 
      model = YOLO("/content/drive/MyDrive/runs/detect/train/weights/best.pt")
    - Image paths for inference : 
      Update the paths pointing to `/content/drive/MyDrive/traffic lights/...` to point to the actual locations of your test images.
There is no need to run the code blocks that re train the model,or import the dataset if we just want to see the results.

### Step 4: Execute
Run the script. The script will:
    - Install required packages.
    - Authorize Google Drive access.
    - Train the model (run it only when u want to re train the model otherwise use best.pt).
    - Run detect_lights() function on the test images provided at the bottom of the script.
    - Display the results using Matplotlib.
    - Save the final output image to `/content/final_output.jpg`.

  Link for test images-https://drive.google.com/drive/folders/16Jyuf8K6gqFHVZwULSlyXSt4EZjmZdWc?usp=sharing
