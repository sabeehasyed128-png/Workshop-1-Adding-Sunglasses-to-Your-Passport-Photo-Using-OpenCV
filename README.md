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
faceImage = cv2.imread('Profile.jpeg')
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
# Separate color and alpha channels
glassBGR = glassPNG[:, :, :3]
glassMask1 = glassPNG[:, :, 3]
```
```
# Display sunglasses and alpha mask
plt.figure(figsize=(12,5))

plt.subplot(121)
plt.imshow(glassBGR[:,:,::-1])
plt.title("Sunglasses")

plt.subplot(122)
plt.imshow(glassMask1, cmap="gray")
plt.title("Alpha Mask")

plt.show()
```
```
# Make a copy
faceWithGlassesNaive = faceImage.copy()

# Place sunglasses over eyes
faceWithGlassesNaive[445:540,470:810] = glassBGR

# Display
plt.figure(figsize=(8,10))
plt.imshow(faceWithGlassesNaive[:,:,::-1])
plt.title("Sunglasses Fitted")
plt.axis("on")
plt.show()
```

```
# Create 3-channel mask
glassMask = cv2.merge((glassMask1,
                       glassMask1,
                       glassMask1))

# Convert mask values to 0 and 1
glassMask = np.uint8(glassMask / 255)

# Make a copy of face image
faceWithGlasses = faceImage.copy()

# ==========================================
# EYE REGION COORDINATES FOR YOUR IMAGE
# ==========================================

x = 460   # left-right position
y = 450   # up-down position

h = glassBGR.shape[0]
w = glassBGR.shape[1]

# Extract eye ROI
eyeROI = faceWithGlasses[y:y+h, x:x+w]

# Remove region where glasses will be placed
maskedEye = cv2.multiply(eyeROI, (1 - glassMask))

# Extract glasses using mask
maskedGlass = cv2.multiply(glassBGR, glassMask)

# Combine both images
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

# Replace eye region with combined image
faceWithGlasses[y:y+h, x:x+w] = eyeRoiFinal

# Intermediate Results
plt.figure(figsize=(15,5))

plt.subplot(131)
plt.imshow(maskedEye[:,:,::-1])
plt.title("Masked Eye Region")

plt.subplot(132)
plt.imshow(maskedGlass[:,:,::-1])
plt.title("Masked Sunglass Region")

plt.subplot(133)
plt.imshow(eyeRoiFinal[:,:,::-1])
plt.title("Combined ROI")

plt.show()
```

```
# Final Result
plt.figure(figsize=(12,8))

plt.subplot(121)
plt.imshow(faceImage[:,:,::-1])
plt.title("Original Image")
plt.axis("on")

plt.subplot(122)
plt.imshow(faceWithGlasses[:,:,::-1])
plt.title("With Sunglasses")
plt.axis("on")

plt.show()
```

### OUTPUT:

#### Original Face Image

<img width="517" height="546" alt="image" src="https://github.com/user-attachments/assets/f9342482-384d-4fbf-a5bd-26023f68c7a4" />

#### Sunglass Image

<img width="726" height="348" alt="image" src="https://github.com/user-attachments/assets/c213d984-ef57-4ecd-9190-d532ed526779" />

#### Image Dimension

<img width="286" height="37" alt="image" src="https://github.com/user-attachments/assets/ee1740ab-14ff-474b-9152-c364ca02b2f7" />

#### Sunglass with colour channel and with alpha channel

<img width="1247" height="232" alt="image" src="https://github.com/user-attachments/assets/a71e0c56-4823-4ddf-9693-c68752e8e0ad" />

#### Image with Sunglass

<img width="701" height="785" alt="image" src="https://github.com/user-attachments/assets/524b1292-a0e5-41dc-be37-6cb3e0a6cb9a" />

#### Augumented Eye and Sunglasses 

<img width="1237" height="172" alt="image" src="https://github.com/user-attachments/assets/d69acb07-e527-4f14-9ed3-fc566e1cc9af" />

#### Image with and without sunglasses

<img width="1152" height="666" alt="image" src="https://github.com/user-attachments/assets/3ef1c4ae-80eb-4fb0-a162-96929a2abdac" />

### RESULT:
Thus, the Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing has been done and verified successfully.
