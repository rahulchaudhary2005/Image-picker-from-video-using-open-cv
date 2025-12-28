# Image-picker-from-video-using-open-cv
Implemented a video-based image picker using Python and OpenCV to read video streams, display frames in real time, and capture selected frames as images.

import cv2
import os

# Create folder to save images
os.makedirs("captured_images", exist_ok=True)

cap = cv2.VideoCapture(0)  # 0 = default camera
img_count = 0

while True:
    ret, frame = cap.read()
    if not ret:
        print("Failed to access camera")
        break

    frame = cv2.resize(frame, (640, 480))
    cv2.imshow("Video Capture", frame)

    key = cv2.waitKey(1) & 0xFF

    # Save image when 's' is pressed
    if key == ord('s'):
        img_name = f"captured_images/img_{img_count}.jpg"
        cv2.imwrite(img_name, frame)
        print(f"Image saved: {img_name}")
        img_count += 1

    # Quit when 'q' is pressed
    elif key == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
