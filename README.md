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

# All models are under 6 MB — well below the 50 MB deployment target. ONNX inference latency: \*\*0.85 ms\*\* on CPU.

# 

# \## Setup

# 

# ```bash

