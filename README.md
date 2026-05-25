# \# Lightweight TB-Net: Compressed Deep Learning for Tuberculosis Detection

# 

# A PyTorch reimplementation of TB-Net (Wong et al., 2022) with model compression for on-device Android deployment. Achieves 99.39% accuracy and 97.86% sensitivity on chest X-ray classification, compressed to as small as 0.30 MB for mobile use.

# 

# \## Motivation

# 

# Rural clinics across Africa and South Asia often lack digital X-ray machines — clinicians photograph X-ray films with smartphones instead. This project produces a model small enough to run entirely on-device with no internet required, targeting mid-range Android hardware.

# 

# \## Results

# 

# | Model | Size | Accuracy | Sensitivity | Specificity | AUC |

# |---|---|---|---|---|---|

# | TB-Net FP32 | 1.07 MB | 99.39% | 97.86% | 100.00% | 0.9987 |

# | TB-Net FP16 | 0.55 MB | 99.39% | 97.86% | 100.00% | 0.9986 |

# | TB-Net INT8 | 0.82 MB | 99.39% | 97.86% | 100.00% | 0.9987 |

# | TB-Net 25% pruned | 1.07 MB | 99.59% | 98.57% | 100.00% | 0.9996 |

# | TB-Net 50% pruned | 1.07 MB | 98.57% | 97.14% | 99.14% | 0.9987 |

# | MobileNetV3 student | 5.91 MB | 98.57% | 96.43% | 99.43% | 0.9973 |

# | ONNX FP32 | 1.04 MB | 99.39% | 97.86% | 100.00% | 0.9987 |

# | ONNX INT8 | 0.30 MB | 99.39% | 97.86% | 100.00% | 0.9987 |

# 

# All models are under 6 MB — well below the 50 MB deployment target. ONNX inference latency: 0.85 ms on CPU.

# 

# \## Setup

# 

# conda create -n tb\_detect python=3.10

# conda activate tb\_detect

# pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121

# pip install numpy opencv-python scikit-learn matplotlib Pillow tqdm pandas onnx onnxruntime

# 

# \## Dataset

# 

# Download the Tuberculosis Chest X-Ray Dataset from Kaggle:

# https://www.kaggle.com/datasets/tawsifurrahman/tuberculosis-tb-chest-xray-dataset

# 

# Extract it, then run:

# 

# python fix\_dataset.py

# python fix\_tb.py

# python make\_splits.py

# 

# This produces 4,900 preprocessed images (3,500 normal, 1,400 TB-positive) with an 80/10/10 train/val/test split.

# 

# \## Training

# 

# python train\_pytorch.py

# 

# Trains for 10 epochs using Adam (lr=0.0001), batch size 32. Best checkpoint saved to models/tbnet\_best.pth.

# 

# \## Compression

# 

# python quantize.py       # FP16 and INT8 quantization

# python prune.py          # L1 pruning at 25%, 50%, 75% sparsity

# python distill.py        # Knowledge distillation to MobileNetV3-Small

# 

# \## Android Deployment

# 

# python android\_deploy.py

# 

# Exports to ONNX FP32 and INT8 formats in the deploy/ folder. Use with ONNX Runtime Mobile for Android integration.

# 

# Recommended deployment models:

# \- deploy/tbnet\_int8.onnx  — 0.30 MB, recommended for mid-range Android devices

# \- deploy/tbnet.onnx       — 1.04 MB, FP32 fallback for maximum accuracy

# 

# \## Repository Structure

# 

# tbnet\_pytorch.py        # Model architecture

# train\_pytorch.py        # Training script

# quantize.py             # Quantization experiments

# prune.py                # Pruning experiments

# distill.py              # Knowledge distillation

# android\_deploy.py       # ONNX export and benchmarking

# fix\_dataset.py          # Dataset preprocessing

# fix\_tb.py               # TB image renaming fix

# make\_splits.py          # Train/val/test split generator

# train\_split\_new.csv     # Training split (3,920 images)

# val\_split\_new.csv       # Validation split (490 images)

# test\_split\_new.csv      # Test split (490 images)

# deploy/

# &#x20; tbnet.onnx            # ONNX FP32 model

# &#x20; tbnet\_int8.onnx       # ONNX INT8 model (Android recommended)

# tbnet\_paper.md          # Full research paper

# 

# \## Citation

# 

# wong2021tbnet

# title: TB-Net: A Tailored, Self-Attention Deep Convolutional Neural Network Design for Detection of Tuberculosis Cases from Chest X-ray Images

# author: Alexander Wong, James Ren Hou Lee, Hadi Rahmat-Khah, Ali Sabri, Amer Alaref

# year: 2021

# arxiv: 2104.03165

# 

# \## License

# 

# MIT License. Model weights are for research use only. Not intended for clinical diagnosis.

