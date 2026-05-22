# Lane Detection using OpenCV

A basic computer vision project that detects road lane lines using OpenCV image processing techniques such as grayscale conversion, thresholding, region masking, edge detection, Gaussian blur, and Hough Transform.

---

## Aim

To implement a basic lane detection pipeline using OpenCV by completing the missing code segments in the provided framework.

---

## Learning Objectives

- Understand different stages of image processing
- Learn how a lane detection pipeline works
- Implement computer vision techniques using Python
- Practice OpenCV functions step-by-step

---

## Software and Libraries Used

- Python 3.7
- Anaconda
- Jupyter Notebook / VS Code
- OpenCV (`cv2`)
- NumPy
- Matplotlib

---

## Algorithm

### Step 1: Import Libraries

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

---

### Step 2: Read the Image

```python
image = cv2.imread('lan_img1.jpg')
```

---

### Step 3: Convert to Grayscale

```python
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```

---

### Step 4: Display Images

```python
plt.figure(figsize=(10,5))

plt.subplot(1,2,1)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title('Input Image')

plt.subplot(1,2,2)
plt.imshow(gray, cmap='gray')
plt.title('Grayscale')

plt.show()
```

---

### Step 5: Thresholding

```python
threshold = cv2.threshold(gray, 120, 255, cv2.THRESH_BINARY)[1]
```

---

### Step 6: Region of Interest (ROI)

```python
roi_vertices = np.array([[[100, 540],
                          [900, 540],
                          [515, 320],
                          [450, 320]]])

mask = np.zeros_like(threshold)

if len(threshold.shape) > 2:
    channel_count = threshold.shape[2]
    ignore_mask_color = (255,) * channel_count
else:
    ignore_mask_color = 255

cv2.fillPoly(mask, roi_vertices, ignore_mask_color)

roi = cv2.bitwise_and(threshold, mask)

plt.figure(figsize=(20,10))

plt.subplot(1,3,1)
plt.imshow(threshold, cmap='gray')
plt.title('Initial Threshold')

plt.subplot(1,3,2)
plt.imshow(mask, cmap='gray')
plt.title('Polyfill Mask')

plt.subplot(1,3,3)
plt.imshow(roi, cmap='gray')
plt.title('Isolated ROI')

plt.show()
```

---

### Step 7: Edge Detection

```python
edges = cv2.Canny(roi, 50, 150)
```

---

### Step 8: Gaussian Blur

```python
canny_blur = cv2.GaussianBlur(edges, (5,5), 0)
```

---

### Step 9: Hough Transform

```python
lines = cv2.HoughLinesP(
    canny_blur,
    rho=2,
    theta=np.pi/180,
    threshold=50,
    minLineLength=40,
    maxLineGap=100
)
```

---

### Step 10: Draw Detected Lines

```python
def draw_lines(img, lines, color=[255, 0, 0], thickness=2):

    if lines is not None:
        for line in lines:
            for x1, y1, x2, y2 in line:
                cv2.line(img, (x1, y1), (x2, y2), color, thickness)

hough = np.zeros((image.shape[0], image.shape[1], 3), dtype=np.uint8)

draw_lines(hough, lines)

plt.figure(figsize=(15,10))
plt.imshow(hough)
plt.title('Detected Lane Lines')

plt.show()
```

---

## Expected Output

- Original Image
- Grayscale Image
- Thresholded Image
- ROI Masked Image
- Edge Detection Output
- Blurred Image
- Hough Line Detection
- Final Lane Detection Result

---

## How to Run

1. Clone the repository

```bash
git clone https://github.com/your-username/your-repository-name.git
```

2. Install required libraries

```bash
pip install opencv-python numpy matplotlib
```

3. Open the notebook in Jupyter Notebook or VS Code

4. Run the notebook step-by-step

---

## Result

The lane detection pipeline was successfully implemented using OpenCV techniques. The system effectively detects and highlights lane boundaries from the road image.

---

## Concepts Used

- Image Processing
- Computer Vision
- Edge Detection
- Hough Transform
- ROI Masking
- OpenCV

---

## Developed By
```
Name: udhaya prakash v
Register Number: 212224240177
```
