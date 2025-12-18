


This project implements an object detection pipeline to distinguish between **gloved hands** and **bare hands**, intended for factory safety compliance monitoring.
It uses **YOLOv8** fine-tuned on a custom dataset to classify and localize hands in images.

The pipeline:

* loads a folder of `.jpg` images
* performs object detection
* saves annotated output images
* writes detection results to `.json`

---

## 📊 Dataset

**Source:**
Kaggle — [`dataclusterlabs/palm-and-gloves-dataset`](https://www.kaggle.com/datasets/dataclusterlabs/palm-and-gloves-dataset)

### Dataset details:

* Images with Pascal VOC `.xml` annotations
* Two classes:

  * `glove` → mapped to `gloved_hand`
  * `human_palm` → mapped to `bare_hand`

### Preprocessing:

* Converted VOC XML → YOLO format
* Train/Val split: 80/20
* Augmentation enabled (blur, grayscale, CLAHE)

---

## 🤖 Model

* **YOLOv8-small** (`yolov8s.pt`)
* Pretrained on COCO
* Fine-tuned for 2 custom classes:

  * `gloved_hand`
  * `bare_hand`

### Training Configuration

| Setting           | Value       |
| ----------------- | ----------- |
| Epochs            | 15          |
| Image Size        | 640         |
| Optimizer         | AdamW       |
| Transfer Learning | Yes         |
| Device            | CPU (Colab) |

### Performance Summary

| Metric    | Result |
| --------- | ------ |
| Precision | ~0.94  |
| Recall    | ~0.84  |
| mAP50     | ~0.88  |
| mAP50–95  | ~0.66  |






