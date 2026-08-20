# Detect-the-lines-using-Hough-Transform-Lane-Detection

# AIM:
To implement a basic lane detection pipeline using OpenCV by completing missing code segments at specified locations.
# Learning Objective:
1.Understand each stage of image processing

2.Learn how to build a complete computer vision pipeline

3.Practice writing code in guided sections

# Software Used
Anaconda – Python 3.7

Jupyter Notebook / VS Code

OpenCV (cv2)

NumPy

Matplotlib

# Algorithm & Program

## DEVELOPED BY : SUJIN  M L
## REGISTER NUMBER : 212225040435
# Step 1: Import Libraries
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
# Step 2: Read the Image
```
img = cv2.imread("lan.jpg")

if img is None:
    print("Error: Image not found. Check the image path.")
else:
    print("Image loaded successfully")
```
# Step 3: Convert to Grayscale
```
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

plt.imshow(gray, cmap="gray")
plt.title("Grayscale Image")
plt.axis("off")
plt.show()
```
# Step 4: Display Images
```
plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(gray, cmap="gray")
plt.title("Grayscale Image")
plt.axis("off")

plt.show()
```
# Step 5: Thresholding
```
ret, threshold = cv2.threshold(
    gray,
    127,
    255,
    cv2.THRESH_BINARY
)

plt.imshow(threshold, cmap="gray")
plt.title("Thresholded Image")
plt.axis("off")
plt.show()
```
# Step 6: Region of Interest (ROI)
```
height, width = gray.shape

mask = np.zeros_like(gray)

polygon = np.array([[
    (0, height),
    (width, height),
    (int(width * 0.6), int(height * 0.55)),
    (int(width * 0.4), int(height * 0.55))
]], dtype=np.int32)

cv2.fillPoly(mask, polygon, 255)

roi = cv2.bitwise_and(threshold, mask)

plt.imshow(roi, cmap="gray")
plt.title("Region of Interest")
plt.axis("off")
plt.show()
```
# Step 7: Edge Detection (Canny)
```
edges = cv2.Canny(roi, 50, 150)

plt.imshow(edges, cmap="gray")
plt.title("Canny Edge Detection")
plt.axis("off")
plt.show()
```
# Step 8: Gaussian Blur
```
blur = cv2.GaussianBlur(
    edges,
    (5, 5),
    0
)

plt.imshow(blur, cmap="gray")
plt.title("Gaussian Blur")
plt.axis("off")
plt.show()
```
# Step 9: Hough Transform
```
lines = cv2.HoughLinesP(
    blur,
    1,
    np.pi / 180,
    threshold=50,
    minLineLength=50,
    maxLineGap=100
)

print("Detected Lines:", lines)
```
# Step 10: Lane Detection Logic
```
lane = cv2.cvtColor(
    img,
    cv2.COLOR_BGR2RGB
).copy()

if lines is not None:

    for line in lines:

        line = np.array(line).reshape(-1)

        if len(line) == 4:

            x1, y1, x2, y2 = line

            cv2.line(
                lane,
                (int(x1), int(y1)),
                (int(x2), int(y2)),
                (255, 0, 0),
                5
            )

plt.figure(figsize=(10, 6))
plt.imshow(lane)
plt.title("Final Lane Detection")
plt.axis("off")
plt.show()
```
# Output:

<img width="690" height="432" alt="image" src="https://github.com/user-attachments/assets/6b595a67-6947-401e-9051-9519a4c116dc" />


<img width="700" height="441" alt="image" src="https://github.com/user-attachments/assets/f1dd3d0a-b0b1-43fa-b049-f6a4893c52fb" />

<img width="1077" height="331" alt="image" src="https://github.com/user-attachments/assets/36c05d8e-ceb5-45a4-a7b9-b8d72961ce7a" />

<img width="720" height="449" alt="image" src="https://github.com/user-attachments/assets/0584979d-5bc2-43ad-aaf6-3fa82ffefed9" />
<img width="713" height="455" alt="image" src="https://github.com/user-attachments/assets/8c476d7a-3c10-4b59-96c2-97e961f891b8" />

<img width="703" height="443" alt="image" src="https://github.com/user-attachments/assets/cae3b681-f393-42dd-9e84-63c2b3892bd7" />

<img width="691" height="439" alt="image" src="https://github.com/user-attachments/assets/85195f83-61cc-4df6-a641-f8abe89caebc" />

<img width="1072" height="657" alt="image" src="https://github.com/user-attachments/assets/459bba44-1965-4e6f-b05b-8b30f5ab1c0b" />

# Result:
Thus, the lane detection pipeline is successfully implemented by completing the missing code sections. The system detects and highlights lane lines effectively.
