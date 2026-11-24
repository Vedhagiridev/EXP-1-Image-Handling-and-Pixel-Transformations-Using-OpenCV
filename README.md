# EXP-1-Image-Handling-and-Pixel-Transformations-Using-OpenCV

# Image-Handling-and-Pixel-Transformations-Using-OpenCV 

## AIM:
Write a Python program using OpenCV that performs the following tasks:

1) Read and Display an Image.  
2) Adjust the brightness of an image.  
3) Modify the image contrast.  
4) Generate a third image using bitwise operations.

## Software Required:
- Anaconda - Python 3.7
- Jupyter Notebook (for interactive development and execution)

## Algorithm:
### Step 1:
Load an image from your local directory and display it.

### Step 2:
Create a matrix of ones (with data type float64) to adjust brightness.

### Step 3:
Create brighter and darker images by adding and subtracting the matrix from the original image.  
Display the original, brighter, and darker images.

### Step 4:
Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2 (without overflow fix).  
Display the original, lower contrast, and higher contrast images.

### Step 5:
Split the image (boy.jpg) into B, G, R components and display the channels

## Program Developed By:
- **Name:** Sharmili V 
- **Register Number:** 212225040405

  ### Ex. No. 01

#### 1. Read the image ('Eagle_in_Flight.jpg') using OpenCV imread() as a grayscale image.
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
gray_img = cv2.imread("my_image.jpg", 0)
```

#### 2. Print the image width, height & Channel.
```python
height, width = gray_img.shape

print("Width:", width)
print("Height:", height)
print("Channel: 1")
```

#### 3. Display the image using matplotlib imshow().
```python
plt.imshow(gray_img, cmap='gray')
plt.title("Grayscale Image")
plt.axis('off')
plt.show()
```

#### 4. Save the image as a PNG file using OpenCV imwrite().
```python
cv2.imwrite("output.png", gray_img)
```

#### 5. Read the saved image above as a color image using cv2.cvtColor().
```python
img_color = cv2.cvtColor(gray_img, cv2.COLOR_GRAY2BGR)
```

#### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.
```python
height, width, channel = img_color.shape

plt.imshow(cv2.cvtColor(img_color, cv2.COLOR_BGR2RGB))
plt.title("Colour Image")
plt.axis('off')
plt.show()

print("Width:", width)
print("Height:", height)
print("Channel:", channel)
```

#### 7. Crop the image to extract any specific (Eagle alone) object from the image.
```python
cropped = img_color[height//4:3*height//4,
                    width//4:3*width//4]

plt.imshow(cv2.cvtColor(cropped, cv2.COLOR_BGR2RGB))
plt.title("Cropped Image")
plt.axis('off')
plt.show()
```

#### 8. Resize the image up by a factor of 2x.
```python
resized = cv2.resize(cropped, None, fx=2, fy=2)

plt.imshow(cv2.cvtColor(resized, cv2.COLOR_BGR2RGB))
plt.title("Resized Image")
plt.axis('off')
plt.show()
```

#### 9. Flip the cropped/resized image horizontally.
```python
flipped = cv2.flip(resized, 1)

plt.imshow(cv2.cvtColor(flipped, cv2.COLOR_BGR2RGB))
plt.title("Flipped Image")
plt.axis('off')
plt.show()
```

#### 10. Read in the image ('Apollo-11-launch.jpg').
```python
img = cv2.imread("my_image.jpg")
height, width, channel = img.shape
```

#### 11. Add the following text to the dark area at the bottom of the image (centered on the image):
```python
text = "My Image"
font_face = cv2.FONT_HERSHEY_PLAIN

cv2.putText(img, text, (20, height-20),
            font_face, 2, (255,255,255), 2)
```

#### 12. Draw a magenta rectangle that encompasses the launch tower and the rocket.
```python
rect_color = (255, 0, 255)

cv2.rectangle(img, (width//4, height//4),
              (3*width//4, 3*height//4),
              rect_color, 2)
```

#### 13. Display the final annotated image.
```python
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Annotated Image")
plt.axis('off')
plt.show()
```

#### 14. Read the image ('Boy.jpg').
```python
img = cv2.imread("my_image.jpg")
```

#### 15. Adjust the brightness of the image.
```python
matrix_ones = np.ones(img.shape, dtype="float64") * 50
```

#### 16. Create brighter and darker images.
```python
img_brighter = cv2.add(img, matrix_ones, dtype=cv2.CV_8U)
img_darker = cv2.subtract(img, matrix_ones, dtype=cv2.CV_8U)
```

#### 17. Display the images (Original Image, Darker Image, Brighter Image).
```python
plt.figure(figsize=(12,4))

plt.subplot(1,3,1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")

plt.subplot(1,3,2)
plt.imshow(cv2.cvtColor(img_darker, cv2.COLOR_BGR2RGB))
plt.title("Darker Image")

plt.subplot(1,3,3)
plt.imshow(cv2.cvtColor(img_brighter, cv2.COLOR_BGR2RGB))
plt.title("Brighter Image")

plt.show()
```

#### 18. Modify the image contrast.
```python
# Create two higher contrast images using the 'scale' option with factors of 1.1 and 1.2 (without overflow fix)
matrix1 = np.ones(img.shape, dtype="float64") * 1.1
matrix2 = np.ones(img.shape, dtype="float64") * 1.2

matrix_low = np.ones(img.shape, dtype="float64") * 0.9

img_lower = cv2.multiply(img, matrix_low, dtype=cv2.CV_8U)
img_higher1 = cv2.multiply(img, matrix1, dtype=cv2.CV_8U)
img_higher2 = cv2.multiply(img, matrix2, dtype=cv2.CV_8U)
```

#### 19. Display the images (Original, Lower Contrast, Higher Contrast).
```python
plt.figure(figsize=(12,4))

plt.subplot(1,3,1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")

plt.subplot(1,3,2)
plt.imshow(cv2.cvtColor(img_lower, cv2.COLOR_BGR2RGB))
plt.title("Lower Contrast")

plt.subplot(1,3,3)
plt.imshow(cv2.cvtColor(img_higher2, cv2.COLOR_BGR2RGB))
plt.title("Higher Contrast")

plt.show()
```

#### 20. Split the image (boy.jpg) into the B,G,R components & Display the channels.
```python
B, G, R = cv2.split(img)

blue = cv2.merge([B, np.zeros_like(B), np.zeros_like(B)])
green = cv2.merge([np.zeros_like(G), G, np.zeros_like(G)])
red = cv2.merge([np.zeros_like(R), np.zeros_like(R), R])

plt.figure(figsize=(12,4))

plt.subplot(1,3,1)
plt.imshow(cv2.cvtColor(blue, cv2.COLOR_BGR2RGB))
plt.title("Blue Channel")

plt.subplot(1,3,2)
plt.imshow(cv2.cvtColor(green, cv2.COLOR_BGR2RGB))
plt.title("Green Channel")

plt.subplot(1,3,3)
plt.imshow(cv2.cvtColor(red, cv2.COLOR_BGR2RGB))
plt.title("Red Channel")

plt.show()
```

#### 21. Merged the R, G, B , displays along with the original image
```python
merged = cv2.merge([R, G, B])

plt.figure(figsize=(10,4))

plt.subplot(1,2,1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")

plt.subplot(1,2,2)
plt.imshow(merged)
plt.title("Merged RGB Image")

plt.show()
```

#### 22. Split the image into the H, S, V components & Display the channels.
```python
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

H, S, V = cv2.split(hsv)

plt.figure(figsize=(12,4))

plt.subplot(1,3,1)
plt.imshow(H, cmap='gray')
plt.title("Hue")

plt.subplot(1,3,2)
plt.imshow(S, cmap='gray')
plt.title("Saturation")

plt.subplot(1,3,3)
plt.imshow(V, cmap='gray')
plt.title("Value")

plt.show()
```
#### 23. Merged the H, S, V, displays along with original image.
```python
merged_hsv = cv2.merge([H, S, V])

merged_bgr = cv2.cvtColor(merged_hsv, cv2.COLOR_HSV2BGR)

plt.figure(figsize=(10,4))

plt.subplot(1,2,1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")

plt.subplot(1,2,2)
plt.imshow(cv2.cvtColor(merged_bgr, cv2.COLOR_BGR2RGB))
plt.title("Merged HSV Image")

plt.show()

bitwise_not = cv2.bitwise_not(img)

plt.figure(figsize=(10,4))

plt.subplot(1,2,1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")

plt.subplot(1,2,2)
plt.imshow(cv2.cvtColor(bitwise_not, cv2.COLOR_BGR2RGB))
plt.title("Bitwise NOT Image")

plt.show()
```

## Output:
- **i)** Read and Display an Image.

<img width="747" height="595" alt="image" src="https://github.com/user-attachments/assets/ad64e408-fc6f-4228-9215-eff19a678f2e" />

<img width="745" height="463" alt="image" src="https://github.com/user-attachments/assets/8e76f1a4-c581-40a1-ac75-e30c38b326ed" />

<img width="642" height="406" alt="image" src="https://github.com/user-attachments/assets/0a58e3e5-73dc-4757-9111-f1e9e5e6fc2b" />

<img width="646" height="358" alt="image" src="https://github.com/user-attachments/assets/54668ef8-e75a-4275-a543-ac6c953b4e9e" />

<img width="645" height="400" alt="image" src="https://github.com/user-attachments/assets/7eb5664e-87d0-4910-a39f-4a7df06b2715" />

<img width="625" height="396" alt="image" src="https://github.com/user-attachments/assets/25c7e221-0f9b-4ddc-9ee0-ce3e260e65d4" />


- **ii)** Adjust Image Brightness.

  
<img width="755" height="178" alt="image" src="https://github.com/user-attachments/assets/95ff19ce-6ee9-495e-acd4-2ecb0611ba36" />

- **iii)** Modify Image Contrast.
<img width="783" height="200" alt="image" src="https://github.com/user-attachments/assets/5f6450c5-04e0-4e30-b6bf-3816d7154417" />

<img width="772" height="202" alt="image" src="https://github.com/user-attachments/assets/1d4e544f-23dc-4a91-a671-77ed53d722b6" />

<img width="777" height="285" alt="image" src="https://github.com/user-attachments/assets/38b147dd-6499-43fa-8af9-557a1e717f8a" />

<img width="777" height="192" alt="image" src="https://github.com/user-attachments/assets/773fe0bb-c350-427a-90b9-8544fccfdf29" />



- **iv)** Generate Third Image Using Bitwise Operations.
<img width="780" height="570" alt="image" src="https://github.com/user-attachments/assets/e86a51c0-4091-4108-9ce6-25207b5c893e" />

## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.
