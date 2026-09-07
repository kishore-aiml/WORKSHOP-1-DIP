## WORKSHOP-1 

### Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## Program & output : 
**NAME** : KISHORE J

**REG. NO.** : 212225240072
python
```
# Import libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
```
# Load the Face Image
faceImage = cv2.imread('myimg.jpeg')

plt.imshow(faceImage[:, :, ::-1])
plt.title("Face")
plt.show()
```
<img width="430" height="555" alt="image" src="https://github.com/user-attachments/assets/0291c4a5-cc2d-4fa5-ad29-27f5880a9d1d" />

```
# Check the dimensions of the face image
faceImage.shape
```
<img width="156" height="37" alt="image" src="https://github.com/user-attachments/assets/f22aaf69-fcbb-481f-bb47-bb894b66ae3b" />

```
# Load the Sunglass image with Alpha channel
glassPNG = cv2.imread('sunglass.png', -1)

plt.imshow(glassPNG[:, :, ::-1])
plt.title("glassPNG")
plt.show()
```
<img width="695" height="342" alt="image" src="https://github.com/user-attachments/assets/475b29bf-8ed9-4d74-b2c6-7c2f35347d69" />

```
# Resize the image to fit over the eye region
glassPNG = cv2.resize(glassPNG, (340, 110))

print("Sunglasses Dimension =", glassPNG.shape)
```
<img width="337" height="35" alt="image" src="https://github.com/user-attachments/assets/ef58664c-2721-4250-97d6-033f4823836c" />

```
# Separate the Color and Alpha channels
glassBGR = glassPNG[:, :, 0:3]
glassMask1 = glassPNG[:, :, 3]
```
```
# Display the images for clarity
plt.figure(figsize=[15, 15])

plt.subplot(121)
plt.imshow(glassBGR[:, :, ::-1])
plt.title('Sunglass Color channels')

plt.subplot(122)
plt.imshow(glassMask1, cmap='gray')
plt.title('Sunglass Alpha channel')

plt.show()
```
<img width="866" height="176" alt="image" src="https://github.com/user-attachments/assets/316afb88-23bd-4ff4-8a43-bfcf4a5e2a32" />

```
# Make a copy of the original image
faceWithGlassesNaive = faceImage.copy()

# Place the sunglasses over the eye region
x1 = 330
y1 = 425

x2 = x1 + glassBGR.shape[1]
y2 = y1 + glassBGR.shape[0]

faceWithGlassesNaive[y1:y2, x1:x2] = glassBGR

# Display the result
plt.imshow(faceWithGlassesNaive[:, :, ::-1])
plt.title("Sunglasses - Naive Method")
plt.show()
```
<img width="435" height="545" alt="image" src="https://github.com/user-attachments/assets/35889a6d-466a-4619-a265-c04161242d2e" />

```
# Resize the sunglasses mask
glassMask1 = cv2.resize(glassMask1, (glassBGR.shape[1], glassBGR.shape[0]))

print("Mask Dimension =", glassMask1.shape)
```
<img width="248" height="28" alt="image" src="https://github.com/user-attachments/assets/44830a59-f30e-4ba1-9d40-e184218762cc" />

```
# Create a 3-channel mask
glassMask = cv2.merge((glassMask1, glassMask1, glassMask1))

# Convert mask values from 0-255 to 0-1
glassMask = np.uint8(glassMask / 255)

print("Glass Mask Dimension =", glassMask.shape)
```
<img width="327" height="37" alt="image" src="https://github.com/user-attachments/assets/5430fae8-44d1-4ce6-b2a9-20d4f549aad8" />

```
# Display the final result
plt.figure(figsize=(15, 8))

plt.subplot(121)
plt.imshow(faceImage[:, :, ::-1])
plt.title("Original Image")
plt.axis("off")

plt.subplot(122)
plt.imshow(faceWithGlassesArithmetic[:, :, ::-1])
plt.title("Final Image with Sunglasses")
plt.axis("off")

plt.show()
```
<img width="857" height="538" alt="image" src="https://github.com/user-attachments/assets/8f44f877-64c5-4cee-a8e5-3bc0ac435dc6" />

