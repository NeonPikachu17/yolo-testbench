# YOLO TestBench

**YOLO TestBench** is a powerful and versatile mobile application built with Flutter that leverages the **Ultralytics YOLO** library to perform various computer vision tasks directly on your device. The app allows users to easily import and manage YOLO models for object detection, instance segmentation, and image classification from their local storage.

## Features

* **Multi-Task Support**: Dynamically switch between three core YOLO tasks:
    * **Object Detection** (`detect`): Draws bounding boxes around objects and labels them.
    * **Instance Segmentation** (`segment`): Draws both bounding boxes and pixel-perfect masks around detected objects.
    * **Image Classification** (`classify`): Identifies the main subject of an image and provides a list of top-ranked classes with confidence scores.
* **Local Model Management**:
    * **Import**: Use a file picker to easily import `.tflite` models and their corresponding `.txt` label files into the app.
    * **Discovery**: The app automatically discovers and lists all imported models for easy selection.
    * **Deletion**: Conveniently delete locally stored models directly from within the app.
* **Image Sourcing**: Analyze images from your device's **gallery** or by using the **camera**.
* **Interactive Results**:
    * For detection and segmentation, tap on a result in the list to highlight its bounding box on the image.
    * Control the visibility and opacity of segmentation masks.

## Getting Started

### Prerequisites

* Flutter SDK (v3.13.0 or higher)
* A physical device or emulator running Android or iOS.
* For Android, you may need to add the following to `android/app/build.gradle` to prevent issues with large TFLite models:
    ```groovy
    android {
      // ...
      aaptOptions {
        noCompress 'tflite'
      }
    }
    ```
* For iOS, ensure your `Info.plist` file includes the necessary privacy descriptions for camera and photo library access.

### Installation

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/NeonPikachu17/yolo-testbench.git](https://github.com/NeonPikachu17/yolo-testbench.git)
    cd vision_ai
    ```
2.  **Install dependencies:**
    ```bash
    flutter pub get
    ```
3.  **Run the app:**
    ```bash
    flutter run
    ```

## How It Works

This application uses the `ultralytics_yolo` Flutter package, a powerful tool for integrating YOLO models into mobile apps. The core logic handles:

1.  **Model Discovery**: It scans the application's local documents directory for `.tflite` model files and their corresponding `.txt` label files.
2.  **Model Loading**: When a user selects a model, the app initializes a `YOLO` instance with the correct task type (`segment`, `detect`, or `classify`).
3.  **Inference**: The app passes the selected image's byte data to the loaded YOLO model for prediction.
4.  **Result Rendering**: Based on the model's output and the selected task, a `CustomPainter` draws the appropriate visualizations (bounding boxes, masks, and labels) over the original image.

## Model Compatibility

This app is designed to work with YOLO models in the **TensorFlow Lite (`.tflite`)** format.