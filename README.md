
# 🖐️ Hand Gesture Recognition 

This mini project performs **hand gesture recognition** using **MediaPipe** and **OpenCV**, designed to run in **Google Colab** without any graphical user interface (GUI). It detects hand landmarks from an uploaded image and visualizes the output.

---

## Features

- Detect hand landmarks using MediaPipe
- Visualize the hand skeleton with OpenCV
- Works directly in Google Colab
- No GUI or web interface required

---

## Technologies Used

- Python
- [MediaPipe](https://google.github.io/mediapipe/)
- [OpenCV](https://opencv.org/)
- [NumPy](https://numpy.org/)
- Google Colab

---

## Setup in Google Colab

1. **Install Dependencies**:
   ```python
   !pip install mediapipe opencv-python
2. Upload an Image:
   from google.colab import files
   uploaded = files.upload()
3. Run Gesture Detection:
   import cv2
import mediapipe as mp
from matplotlib import pyplot as plt

mp_hands = mp.solutions.hands
mp_drawing = mp.solutions.drawing_utils

image_path = list(uploaded.keys())[0]
img = cv2.imread(image_path)
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

hands = mp_hands.Hands(static_image_mode=True)
results = hands.process(img_rgb)

if results.multi_hand_landmarks:
    for hand_landmarks in results.multi_hand_landmarks:
        mp_drawing.draw_landmarks(img_rgb, hand_landmarks, mp_hands.HAND_CONNECTIONS)
    plt.imshow(img_rgb)
    plt.axis('off')
    plt.title("Detected Hand")
    plt.show()
else:
    print("No hand detected.")


