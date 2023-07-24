
# CNN steganalysis

Repo for my master's thesis: "Implementation and research of convolutional neural networks for the steganalysis of digital images".
This thesis concernes the application of convolutional neural networks (deep learning) to solve the problem of classifying steganographic images, known as steganalysis. It explores the current state-of-the-art in utilizing convolutional neural networks for steganalysis, including the most effective architectures [1, 2] designed for this purpose. Subsequently, these architectures were implemented and the impact of various changes introduced to their structure on the model's effectiveness was examined. The experiments conducted in this study allowed for an assessment of how specific modifications in the best-performing models affect their classification effectiveness.

## Dataset

As part of the project, it was decided to use the BOSSbase v1.01 dataset, which is one of the most commonly used datasets for training and testing models in steganalysis. BOSSbase v1.01 contains 10,000 images taken with six different cameras, originally saved in RAW format (without compression). These images were then cropped to a size of 512 × 512 pixels and converted to PGM format (grayscale images) with an 8-bit depth (pixel values ranging from 0 to 255).

To reduce computational complexity, accelerate the learning process, and prevent overfitting to the training data, it was decided to resize each image from 512 × 512 pixels to 256 × 256 pixels. Subsequently, copies of all 10,000 images from BOSSbase were created, and using modified MATLAB scripts [3], messages were embedded into these copies using the WOW algorithm with an embedding capacity of 0.4 bpp. This resulted in 10,000 pairs of cover/stego images. During the embedding process for each of the 10,000 images, a different, randomly generated stego key was used. 

The dataset [4] was divided into three parts:
training set - consisting of 8000 pairs of images used solely for training the neural network.
validation set - 1000 pairs of images allowing to asses how well the model's classification performance improves from epoch to epoch on images it was not trained on.
test set - 1000 pairs of images that the network did not have access to during the training process. This enables the reliable evaluation of the classification performance, i.e., how well the model has been trained.

In the same manner, a second part of dataset was prepared, but instead of using the WOW algorithm, the S-UNIWARD embedding algorithm was used. This allowed to evaluate how well the models perform steganalysis for different steganographic algorithms. It also helped to determine which of these two algorithms proved to be more secure, meaning it was harder to learn and to be recognized by various convolutional neural network variants.

## Used software and GPU

1. Python 3.9.16 + NumPy + Matplotlib
2. PyTorch 1.13.1+cu116 (CUDNN 11.6 support)
3. PyTorch Lightning 2.0.0
4. Neptune.ai API 1.0 - Neptune.ai logger and cloud platform was used to store all the necessary data about each of the conducted experiments and to plot metrics like train/val classification per epoch.

NVIDIA GeForce RTX 2080 Ti (11 GB VRAM) GPU was used (v531.29 drivers). During the training of each model 95% of GPU VRAM was used and whole training/testing process took about 4,5 hrs on average.

## Results

Raw results are presented below. More of the data/metrics and conclusions can be found in the Master's Thesis .pdf itself [5] (written in polish).

#### Yedroudj-Net:
![image](https://github.com/remmarty/CNN_steganalysis/assets/26029058/63798d19-ca14-4d8b-8250-2abdc4dd3c2a)

#### GBRAS-Net:
![image](https://github.com/remmarty/CNN_steganalysis/assets/26029058/c6ea0dfc-a56a-4d79-8b5d-7943ba4604cc)

## Bibliography

1. “Yedrouj-Net: An efficient CNN for spatial steganalysis", Mehdi Yedrouj, Frédéric Comby, and Marc Chaumont, proceedings of the IEEE International Conference on Acoustics, Speech and Signal Processing, ICASSP'2018, 15–20 April 2018, Calgary, Alberta, Canada.
2. T. -S. Reinel et al., "GBRAS-Net: A Convolutional Neural Network Architecture for
Spatial Image Steganalysis," in IEEE Access, vol. 9, pp. 14340-14350, 2021, doi:
10.1109/ACCESS.2021.3052494.
3. MATLAB implementation of WOW and S-UNWARD stego algorithms: http://dde.binghamton.edu/download/stego_algorithms/
4. Dataset: https://drive.google.com/file/d/13pCtDWOZTkquKxQVnIdEw5-L9oCG7ioa/view?usp=sharing
5. Master's Thesis PDF: https://drive.google.com/file/d/1hPhgsJjbLP1iqbn1yAl7ia9e9xVWeBTM/view?usp=sharing
