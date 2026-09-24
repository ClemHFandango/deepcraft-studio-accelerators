# Bird-Drone Detection

This project is designed to work exclusively with DEEPCRAFT™ Studio. Download it from [here](https://softwaretools.infineon.com/assets/com.ifx.tb.tool.deepcraftstudio)

## Overview - Use-Case

The **Bird-Drone Detection** project builds an end-to-end system that aims to identify birds and drones via a live video input. This is coming of increasing concern as drones continue to grow in popularity amongst both the civilian and military population. 

The object detection model is YOLO-based and it can be used in safety, privacy or defensive applications

Users can further expand this project by training their own models, importing new data, and evaluating performance using the provided tools.

- **Machine learning method:** YOLO-based object detection trained in DEEPCRAFT™ Studio
- **Sensor and data type:** RGB camera or live video input (image data)
- **Why it matters:** Enables fast detection and classification of drones, separating them from errant birds flying over the area of interest.

## Features

1. **Real-Time Detection**: The project uses a YOLO-based model to detect and classify birds and drones accurately and in real-time.
2. **Custom Data Integration**: Users can add new data through the data import or using `Object Detection Data Collection Graph UX` template and label their own data for model training.
3. **Model Evaluation**: Evaluate trained models by double-clicking the `.tflite` file; it will generate a Graph UX project to run.

## Contents

- **`Data`**: Contains data taken from Roboflow with images of flying birds and drones: [Bird and drone dataset](https://universe.roboflow.com/workspace-ajksm/drone-detection-with-birds). Data consists of 7,395 annotated sessions (3,044 birds and 4,571 drones bounding boxes). License: CC BY 4.0.

- **`Models`** - Stores the trained YOLO-based model and its quantized versions as well as their predictions.

## Steps to get started: Model Training and Evaluation

1. Train the YOLO-based model using the provided dataset or custom data.
2. Download the trained model `.tflite` file from the trained job.
3. Double-click the `.tflite` file and it will create a Graph UX project.
4. Run the Graph UX project to evaluate model performance in real time using the selected camera.
5. Take photos of birds/drones with the camera

## Sensor(s) & Data

Image data is stored as DEEPCRAFT™ Studio object-detection sessions under `Data/`. Each session contains a JPG image and `LabelXml` annotations with normalized center bounding boxes (`X`, `Y`, `Width`, `Height`). The project currently contains 7,395 sessions.

**Training augmentation:** DEEPCRAFT™ Studio Augmentation Settings in this project's `.improj` are chosen for 224 px. There is no rotation(`degrees` 0) as the input dataset already has quite a variety of input images and it is unlikely that a bird will need to be classified upside down. The translation is modest (`translate` 0.1); scale (`scale` 0.3) and mosaic (`mosaic`1). Mosaic is kept high to help detect drones that are further away. Flip left/right is on (`fliplr` 0.5); flip up/down is off as again, it is unlikely a bird/drone will be flying upside down. Shear is off and perspective is kept quite low (`shear` 0.00025) to help simulate different angles. HSV saturation (`hsv_s` 0.7) and brightness (`hsv_v` 0.4) cover various outdoor lighting scenarios, with a moderate hue shift (`hsv_h` 0.4). Parameter names follow [YOLO data augmentation](https://docs.ultralytics.com/guides/yolo-data-augmentation).


## Adding More Data

You can add more data to the project following the steps below to improve detection or to include new classes.

1. Use `Object Detection Data Collection Graph UX` template to collect and label new data.
2. Import data to your project and retrain to get an updated model.

You can also import data from any other source (for example, your own images or another dataset) as long as it follows the DEEPCRAFT Studio object-detection format: images with matching `LabelXml` annotations using normalized center coordinates (`X`, `Y`, `Width`, `Height`). See [Bring your own data for object detection projects](https://developer.imagimob.com/deepcraft-studio/data-preparation/bring-your-data/bring-your-own-data-object-detection).

## Steps to Production

The recommended path to production for this project includes the following steps:

- **Add more classes if needed.** The project currently detects `Drone` and `Bird` only. If your product must also other airborne targets, e.g, planes or helicopters, add new classes and label accordingly before retraining.
- **Add negative data.** Include empty sky under various weather conditions or skylines with buidings in the background.
- **Match augmentation to outdoor variability.** Adjust HSV for sun, shade, and overcast conditions.
- **Tune confidence for your sensitivity target.** Missing a drone may be more detrimental than misidentifying a bird so tune the model accordingly.

Some points to highlight:

- **Increase data variability:** Collect data from different environments, cameras, lighting conditions, distances, and backgrounds. Use DEEPCRAFT Studio augmentation settings (flip, scale, brightness, exposure) to increase image variability for vision models.
- **Keep test data independent:** Make sure the test set is not used in train or validation and reflects scenarios where the model must generalize.
- **Add negative data:** Include images without the target objects and common look-alikes to improve robustness against false positives.

## Attribution & Citation

Please cite the datasets used in this project.

```bibtex
@misc{ drone-detection-with-birds_dataset,
  title = { Drone-Detection with Birds Dataset },
  type = { Open Source Dataset },
  author = { Workspace },
  howpublished = { \url{ https://universe.roboflow.com/workspace-ajksm/drone-detection-with-birds } },
  url = { https://universe.roboflow.com/workspace-ajksm/drone-detection-with-birds },
  journal = { Roboflow Universe },
  publisher = { Roboflow },
  year = { 2025 },
  month = { dec },
  note = { visited on 2026-09-24 },
}
```

## Getting Started

Please visit [developer.imagimob.com](https://developer.imagimob.com), where you can read about DEEPCRAFT™ Studio and go through step-by-step tutorials to get you quickly started.

For object-detection data formats, see [Bring your own data for object detection projects](https://developer.imagimob.com/deepcraft-studio/data-preparation/bring-your-data/bring-your-own-data-object-detection).

If you need support or if you want to know how to deploy the model onto the device, please submit a ticket on the Infineon [community forum](https://community.infineon.com/t5/Imagimob/bd-p/Imagimob/page/1) DEEPCRAFT™ Studio page.
