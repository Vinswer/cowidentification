# Cow Individual Identification with Few-Shot Learning

Use the prototype network algorithm in few-shot learning to handle the re-ID problem of a farm with 40 cows.

## Overview

This project implements a novel approach for cattle individual identification that combines deep learning with anatomical feature analysis, designed to work effectively with minimal training data (6-10 images per individual). 

**Initial Framework**: The foundational architecture was adapted and significantly enhanced from the EasyFSL library, specifically building upon the basic few-shot classifier implementation in [`my_first_few_shot_classifier.ipynb`](https://github.com/sicara/easy-few-shot-learning/blob/master/notebooks/my_first_few_shot_classifier.ipynb). Our work extends this baseline with:

- Multi-task learning integration (CosFace + Triplet learning)
- Domain-specific anatomical feature processing
- K-medoids post-processing optimization
- Agricultural deployment optimizations
- Comprehensive evaluation framework

<img width="915" height="358" alt="image" src="https://github.com/user-attachments/assets/c78ba3cd-878c-4fc7-822a-468c6456805d" />

<img width="1054" height="258" alt="image" src="https://github.com/user-attachments/assets/574240cc-b216-4ef9-be98-934bad64c7c6" />
*Figure: System architecture pipeline showing the complete workflow from image input to final identification*

## Key Features

- **Few-Shot Learning**: Identifies cattle individuals with only 6-10 training images per cow
- **Multi-Task Architecture**: Combines prototypical networks, CosFace classification, and triplet learning
- **Anatomical Feature Integration**: Uses K-medoids clustering on 11-dimensional udder morphology features
- **Mobile Deployment Ready**: Optimized for edge devices (39.8ms inference, 14.2MB model)
- **Real-time Processing**: Suitable for practical farm deployment scenarios
- **Cross-Domain Robustness**: Maintains performance across different farm environments

## Performance

| Configuration | Top-1 Accuracy | Top-3 Accuracy | Top-5 Accuracy | Inference Time |
|---------------|----------------|----------------|----------------|----------------|
| 10-way 1-shot | 89.3±2.1%     | 96.7±1.4%     | 98.2±0.9%     | 23.4ms        |
| 20-way 1-shot | 81.7±2.8%     | 92.4±1.9%     | 96.1±1.2%     | 28.7ms        |
| 40-way 1-shot | 72.1±3.6%     | 85.7±2.8%     | 92.3±1.9%     | 39.8ms        |

**K-medoids Enhancement**: Consistent +6.3% average improvement across all configurations

## Installation
```bash
pip install -r requirements.txt
```

## Dataset Structure
```bash
dataset/
├── train/
│   ├── specs.json
│   └── class_folders/
│       ├── cow_001/
│       │   ├── image_001.png
│       │   └── image_002.png
│       └── cow_002/
├── val/
└── test/
```

## Data Format Requirements
- **Images**: PNG format, minimum 224x224 resolution
- **Annotation**: JSON files with class names and image paths
- **Udder Coordinates**: CSV file with 3D teat positions (optional, for K-medoids)
