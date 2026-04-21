DA213 Course Project: Traffic Light Detection

Overview:
This project detects traffic lights in various environmental conditions (day, night, rain) using a YOLO object detection model and determines the active light color (Red, Green, or Yellow) using OpenCV and HSV color space filtering.

1. Dependencies

Environment: 
Google Colab is highly recommended because the script includes Colab-specific commands. A GPU runtime (like Tesla T4) is recommended for faster training and inference.

Python Libraries:
- ultralytics (for the YOLO model)
- roboflow (for dataset downloading)
- opencv-python (cv2, for image processing and HSV filtering)
- numpy (for array operations and pixel counting)
- matplotlib (for displaying the output images)

2. Brief Description of Files

- traffic_light_detection.py : 
  This is the main and only source code file for the project. It contains the entire pipeline, including:
    * Installing dependencies and mounting Google Drive.
    * Downloading the dataset from Roboflow.
    * Training the YOLO model (`yolo26n.pt`) and saving the weights.
    * The `analyze_traffic_lights()` function which takes the YOLO bounding box, converts the cropped image to HSV color space, calculates color percentages, and annotates the original image.
    * The `detect_lights()` function to process input images sequentially.

Note: The script expects certain directories and files (like `best.pt` for model weights and test images) to exist in your Google Drive during execution.

3. How to Run the Code

Step 1: Setup Environment
Upload the `traffic_light_detection.py` file to your Google Drive. Ensure your Colab runtime is set to utilize a GPU (Runtime -> Change runtime type -> T4 GPU).

Step 2: Update API Key (For Training Only)
If you wish to download the dataset and retrain the model, replace `****apikey****` on line 18 with your valid Roboflow API key:
    rf = Roboflow(api_key="YOUR_API_KEY")

Step 3: Update File Paths
The script relies on Google Drive paths. You must update these paths to match your personal Google Drive directory structure:
    - Model weights path (line 38): 
      model = YOLO("/content/drive/MyDrive/runs/detect/train/weights/best.pt")
    - Image paths for inference (lines 42 & 134-147): 
      Update the paths pointing to `/content/drive/MyDrive/traffic lights/...` to point to the actual locations of your test images.

Step 4: Execute
Run the script. The script will:
    1. Install required packages.
    2. Prompt you to authorize Google Drive access.
    3. Train the model (if the training block is not commented out).
    4. Run inference on the images provided at the bottom of the script.
    5. Display the annotated images inline using Matplotlib.
    6. Save the final processed image to `/content/final_output.jpg`.
