# Workshop--1-Adding-Sunglasses-to-Your-Passport-Photo-Using-OpenCV

## Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

### Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.
### Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations
### How to Use:
- Clone this repository.
- Add your passport-sized photo to the images folder.
- Run the script to see your "cool" transformation!
### Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows
```
# Import libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
```
# Load the Face Image
faceImage = cv2.imread('me.jpeg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
```
faceImage.shape
```
```
#resized_faceImage.shape
faceImage.shape
```
```
# Load the Sunglass image with Alpha channel
# (http://pluspng.com/sunglass-png-1104.html)
glassPNG = cv2.imread('sunglass.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```
```
# Resize the image to fit over the eye region
glassPNG = cv2.resize(glassPNG,(250, 80))
print("image Dimension ={}".format(glassPNG.shape))
```

```
# Separate the Color and alpha channels
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
```
```
# Display the images for clarity
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
```
# Make a copy
#faceWithGlassesNaive = resized_faceImage.copy()
faceWithGlassesNaive = faceImage.copy()

# Replace the eye region with the sunglass image
faceWithGlassesNaive[340:420, 340:590]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])
```

```
# Make the dimensions of the mask same as the input image.
# Since Face Image is a 3-channel image, we create a 3 channel image for the mask
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)

# Make a copy
faceWithGlassesArithmetic = faceImage.copy()

# Get the eye region from the face image
eyeROI= faceWithGlassesArithmetic[340:420, 340:590]

# Use the mask to create the masked eye region
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))

# Use the mask to create the masked sunglass region
maskedGlass = cv2.multiply(glassBGR,glassMask)

# Combine the Sunglass in the Eye Region to get the augmented image
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

# Display the intermediate results
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
```

```
# Replace the eye ROI with the output from the previous section
faceWithGlassesArithmetic[340:420, 340:590]=eyeRoiFinal

# Display the final result
plt.figure(figsize=[8,10]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```

### OUTPUT:

#### Original Face Image

<img width="960" height="1280" alt="image" src="https://github.com/user-attachments/assets/2c67cbc1-b81f-4566-b729-7fe110374cbf" />


#### Sunglass Image

<img width="700" height="381" alt="image" src="https://github.com/user-attachments/assets/4481008b-ce0d-4b0e-b778-62d467339705" />

#### Image Dimension

<img width="272" height="35" alt="image" src="https://github.com/user-attachments/assets/e0960645-2e17-4d77-a062-c69439765f4b" />

#### Sunglass with colour channel and with alpha channel

<img width="731" height="150" alt="image" src="https://github.com/user-attachments/assets/e14083fb-765e-4b41-b38d-f38dc7f8f03a" />

#### Image with Sunglass

<img width="385" height="498" alt="image" src="https://github.com/user-attachments/assets/8174c79b-90bd-44d3-9321-9302cc89aa71" />


#### Augumented Eye and Sunglasses 

<img width="732" height="142" alt="image" src="https://github.com/user-attachments/assets/6b717dc3-1101-4e39-b8fe-d405522b250c" />

#### Image with and without sunglasses

<img width="715" height="452" alt="image" src="https://github.com/user-attachments/assets/c014a16b-c731-47d6-9cec-87f25437e88a" />

### RESULT:
Thus, the Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing has been done and verified successfully.
