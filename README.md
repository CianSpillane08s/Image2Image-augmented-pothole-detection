# Improved-Pothole-detection-under-adverse-conditions-using-Image-To-Image-Translation.---BTYSTE-2025
This project uses both supervised and unsupervised image-to-image translation methods to increase object detection accuracy under Irish-inspired conditons.
My results show with careful and accurate use of state-of-the-art Image-to-Image translation models we can generate synthetic potholes that imitate the weather of a particularly country, these potholes can then be added to existing data to improve pothole detection accuracy when tested under conditions of that nation. I used pre-trained MUNIT and CycleGAN models to generate synthetic images of Irish roads under rainy, foggy and darker conditions. I then pre-trained a Yolov7-D6 model with 3 separate datasets, one comprising of real images only, another of the synthetic images I had generated and a mixed hybrid approach. Each of the models were tested on the same dataset that deliberatly tested difficult conditions.

The results 
### mAP@0.5 by test set

| Test set | Images | Baseline | Synthetic | Hybrid |
|:--|:-:|:-:|:-:|:-:|
| Water and dry | 150 | 0.650 | 0.715 | **0.736** |
| Cranfield 300 | 50 | **0.978** | 0.791 | 0.945 |
| Cranfield 400 | 50 | 0.972 | 0.879 | **0.982** |
| Cranfield 500 | 50 | 0.970 | 0.848 | **0.984** |
| Cranfield all | 150 | **0.970** | 0.832 | **0.970** |
| Dublin low-light | 40 | **0.673** | 0.518 | 0.614 |
| Dublin daylight | 40 | 0.643 | 0.494 | **0.732** |
| Dublin all | 80 | **0.663** | 0.498 | 0.650 |
| Medium stereo | 25 | 0.640 | 0.929 | **0.953** |
| Close non-stereo | 25 | 0.737 | 0.514 | **0.824** |
| Medium non-stereo | 25 | **0.899** | 0.868 | 0.837 |
| All non-stereo | 50 | **0.833** | 0.696 | 0.806 |
| **All data combined** | **455** | 0.763 | 0.715 | **0.809** |

### Precision / Recall

| Test set | Baseline | Synthetic | Hybrid |
|:--|:-:|:-:|:-:|
| Water and dry | 0.788 / 0.640 | 0.757 / 0.714 | 0.767 / 0.684 |
| Cranfield all | 0.974 / 0.943 | 0.847 / 0.874 | 0.925 / 0.937 |
| Dublin all | 0.641 / 0.719 | 0.644 / 0.573 | 0.719 / 0.718 |
| Medium stereo | 0.760 / 0.760 | 0.920 / 0.920 | 1.000 / 0.920 |
| All non-stereo | 0.881 / 0.740 | 0.573 / 0.779 | 0.711 / 0.800 |
| **All data combined** | 0.845 / 0.710 | 0.757 / 0.714 | 0.779 / 0.774 |


## Structure

- **`synthetic-data-generation/`** — notebooks that generate synthetic
  fog, low-light, and rain training images.
  - `fog-cyclegan/` — fog generation, built on
    [Foggy-CycleGAN](https://github.com/ghaiszaher/Foggy-CycleGAN) by Ghais Zaher.
  - `low-light-day2night/` — low-light generation, built on
    [Day2Night](https://github.com/solesensei/day2night) by Dima Goncharenko.
  - `rain-cyclegan/` — rain generation, a CycleGAN trained from scratch on
    paired clear/rain data using
    [pytorch-CycleGAN-and-pix2pix](https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix)
    by Jun-Yan Zhu et al.
- **`object-detection/`** — YOLOv7-D6 training and testing on the
  combined real + synthetic dataset, built on the official
  [YOLOv7](https://github.com/WongKinYiu/yolov7) repo.


## Credit

This project builds on the third-party repos linked above for the GAN
architectures and the YOLOv7 codebase — the pretrained weights and base
model code are not original work. The dataset curation, synthetic image
generation choices, transfer-learning setup, and evaluation are. I would
like to thank he following for their help with my project
- Mark Bowe
- Eoin Walsh
- Ghais Zaher
