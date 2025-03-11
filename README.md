# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

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

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

## Program:
### Name:MURALI KRISHNA S
### Reg.no:212223230129

import cv2 
import numpy as np
import matplotlib.pyplot as plt
myimage = cv2.imread('WhatsApp Image 2024-01-09 at 21.26.03_7aea8f7c.jpg')
plt.imshow(myimage[:,:,::-1]);plt.title("Face")
myimage.shape
glassPNG = cv2.imread('sunglass-png-aviator-sunglass-png-clipart-3381.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
# Resize the image to fit over the eye region
glassPNG = cv2.resize(glassPNG,(550,160))
print("image Dimension ={}".format(glassPNG.shape))
# Separate the Color and alpha channels
glassBGR = glassPNG[:,:,0:2]
glassMask1 = glassPNG[:,:,2]
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
faceWithGlassesNaive = myimage.copy()

# Correct assignment
faceWithGlassesNaive[420:580, 340:890] = glassBGR

plt.imshow(faceWithGlassesNaive[..., ::-1])
# Make the dimensions of the mask same as the input image.
# Since Face Image is a 3-channel image, we create a 3 channel image for the mask
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)

# Make a copy
faceWithGlassesArithmetic = myimage.copy()

# Get the eye region from the face image
eyeROI= faceWithGlassesArithmetic[420:580, 340:890]

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
# Replace the eye ROI with the output from the previous section
faceWithGlassesArithmetic[420:580, 340:890]=eyeRoiFinal

# Display the final result
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(myimage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
## Output:
### 1.Original image:
![image](https://github.com/user-attachments/assets/594c8cd6-be44-4800-9bbf-7b0b3c078b00)



### 2.Glass:
![image](https://github.com/user-attachments/assets/68b45616-9c0c-48b7-b900-f1ee5db13d70)


### 3.Glass color channel:
![image](https://github.com/user-attachments/assets/f272274a-4c57-4cb2-8ffd-f640cac96eec)



### 4.Face With Glass:
![image](https://github.com/user-attachments/assets/66f0b6df-1d5a-4268-b0ae-ea940160187e)


### 5.Eye and glass region:
![image](https://github.com/user-attachments/assets/514d0976-edc6-428c-a28a-72e5f17337a0)





### 6.Final image with glass:
![image](https://github.com/user-attachments/assets/ec9bf4a7-7399-40b3-a0e7-d74cc6800faa)



## Result:
Thus, the creative project designed to overlay sunglasses on individual passport size photo has been successfully executed.
