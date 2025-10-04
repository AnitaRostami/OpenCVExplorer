# Interactive Video Processing with OpenCV

This Python script leverages OpenCV to create an interactive video processing application that combines live camera feed with image manipulation techniques. It processes two input images (`Do_It.jpg` and `Skyscraper.jpg`) and applies various OpenCV functionalities, displaying the results in multiple windows. The script is designed for educational purposes, demonstrating a wide range of computer vision techniques.

## Features

- **Live Video Capture**: Captures video from the default camera with customizable resolution and brightness.
- **Mouse Interaction**: Allows drawing shapes (circles, triangles, lines) on the video feed based on mouse events.
- **Trackbar Controls**: Provides adjustable parameters for HSV color detection, blending alpha, and rotation angle.
- **Multiple Display Windows**:
  - **Video Feed**: Shows the live feed with overlaid shapes, text, and object tracking.
  - **Sky Effects**: Displays edge detection and color inversion effects on `Do_It.jpg`.
  - **Skyscraper Effects**: Applies blur and contrast adjustments to `Skyscraper.jpg`.
  - **Bitwise Operations**: Visualizes AND, OR, XOR, and NOT operations between resized images.
- **Image Processing**: Includes channel splitting/merging, resizing, weighted blending, and region of interest (ROI) overlay.
- **Object Detection**: Uses HSV color space to detect and track objects in the video feed.
- **Video Recording**: Saves the processed video feed to `output_video.avi`.

## Requirements

- Python 3.x
- OpenCV (`pip install opencv-python`)
- NumPy (`pip install numpy`)

## Usage

1. Ensure `Do_It.jpg` and `Skyscraper.jpg` are in the same directory as the script.
2. Run the script:
   ```bash
   python interactive_video_processor.py
   ```
3. Interact with the application:
   - **Mouse Actions**:
     - Double left-click to draw a red circle.
     - Right-click to draw a green triangle.
     - Hold left-click and drag to draw a blue line.
   - **Trackbars**: Adjust HSV thresholds, blending alpha (0-100), and rotation angle (0-360) to see real-time effects.
   - Press 'q' to quit and save the output video.

## Code Explanation

### Imports
- `cv2`: OpenCV library for computer vision tasks.
- `np`: NumPy for numerical operations.
- `datetime`: For adding current date and time to the video feed.

### Mouse Callback Function (`draw_shapes`)
- Defines interactive drawing:
  - **Double Left-Click**: Draws a filled red circle (radius 50) at the click position.
  - **Right-Click**: Draws a filled green triangle using predefined points.
  - **Left-Click Drag**: Draws a blue line between the last and current mouse positions, updating the last point.

### Trackbar Callback Function (`nothing`)
- A placeholder function required for creating trackbars, as OpenCV expects a callback even if no action is needed.

### Image Loading and Preprocessing
- Loads `Do_It.jpg` and `Skyscraper.jpg`, exiting if either fails.
- **Channel Manipulation**: Splits `Skyscraper.jpg` into B, G, R channels, increases blue channel intensity by 50, and merges back.
- **Resizing**: Resizes images to match the video frame (640x480) or a smaller size (200x300) for overlay.

### Video Capture Setup
- Initializes the camera with a resolution of 640x480 and brightness of 150.
- Exits if the camera fails to open.

### Window Creation
- Creates four OpenCV windows for different visualizations:
  - `Video Feed`: Main interactive window.
  - `Sky Effects`: Shows processed `Do_It.jpg`.
  - `Skyscraper Effects`: Shows processed `Skyscraper.jpg`.
  - `Bitwise Operations`: Displays bitwise operation results.

### Main Loop
- **Video Feed Window**:
  - Overlays the current date and time (e.g., "2025-10-04 16:10" CEST) in yellow.
  - Draws a blue rectangle and a yellow ellipse as geometric shapes.
  - Applies HSV-based object detection with a green bounding box and label.
  - Rotates the `Skyscraper.jpg` overlay based on the `Rotation Angle` trackbar and blends it with the video feed using `Alpha` weighting.
- **Sky Effects Window**:
  - Converts `Do_It.jpg` to grayscale, applies Canny edge detection, inverts colors, and blends them for a unique effect.
- **Skyscraper Effects Window**:
  - Applies Gaussian blur and increases contrast on `Skyscraper.jpg` for a smoothed, enhanced look.
- **Bitwise Operations Window**:
  - Performs AND, OR, XOR, and NOT operations on resized `Do_It.jpg` and `Skyscraper.jpg`, stacking the results horizontally.
- Saves the `Video Feed` to `output_video.avi` and exits on 'q' key press.

### Resource Cleanup
- Releases the camera and video writer, then destroys all windows.

## Notes
- The script assumes a working camera. If no camera is detected, it will exit.
- Adjust trackbars to experiment with different effects in real-time.
- Ensure images are in the correct directory or provide full paths to avoid loading errors.
