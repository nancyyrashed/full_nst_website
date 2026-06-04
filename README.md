# Neural Style Transfer Web Application

## Overview

This repository contains the implementation of a web-based Neural Style Transfer (NST) application developed as part of my final-year Computer Science dissertation at Goldsmiths, University of London.

The application allows users to upload content and style images, apply various Neural Style Transfer techniques, and generate stylized outputs through an interactive web interface. The platform integrates multiple state-of-the-art NST models and provides a user-friendly environment for experimenting with artistic image transformation.

---

## Features

* Upload content and style images
* Generate stylized images using multiple NST models
* Compare outputs across different architectures
* Support for arbitrary style transfer
* Multi-style image generation
* Video style transfer functionality
* Real-time interaction through a web interface
* Download generated outputs

---

## Supported Models

### Gatys et al. (2016)

Optimization-based Neural Style Transfer using VGG-19 feature extraction and iterative optimization.

### Johnson et al. (2016)

Feed-forward style transfer network designed for faster image stylization.

### AdaIN (Adaptive Instance Normalization)

Arbitrary style transfer capable of applying previously unseen artistic styles without retraining.

### Dumoulin et al. (2017)

Conditional Instance Normalization model supporting multiple artistic styles.

### Dumoulin V2

Custom extension combining Conditional Instance Normalization and Adaptive Instance Normalization to improve flexibility and style generalization.

### Dumoulin V2 Multi-Style

Supports simultaneous application of multiple artistic styles within a single image.

### Dumoulin V2 Video Transfer

Video style transfer implementation using optical flow to maintain temporal consistency between frames.

---

## Technologies Used

### Frontend

* Streamlit

### Backend & Machine Learning

* Python
* PyTorch
* TensorFlow
* Keras

### Computer Vision & Media Processing

* OpenCV
* Pillow (PIL)
* ImageIO
* FFmpeg

### Data Processing & Visualization

* NumPy
* Matplotlib
* Seaborn

---

## Application Workflow

1. Select a Neural Style Transfer model.
2. Upload a style image.
3. Upload a content image.
4. Generate the stylized output.
5. Download generated images or videos.

---

## Use Cases

* Digital Art Generation
* Artistic Photo Transformation
* Style Exploration and Experimentation
* Educational Demonstration of Neural Style Transfer
* Research and Model Comparison

---

## Project Background

This web application was developed alongside a broader research project investigating Neural Style Transfer architectures and their effectiveness for image and video stylization.

The system integrates multiple NST approaches within a single interface, enabling users to compare different models and explore the trade-offs between style fidelity, content preservation, flexibility, and computational efficiency.

## Live Demo:
https://neural-style-transfer-graduation-25.streamlit.app/
