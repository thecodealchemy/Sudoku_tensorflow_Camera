# Sudoku Solver with TensorFlow Camera Recognition

A Python application that recognizes and solves Sudoku puzzles using computer vision and deep learning. This project combines **digit recognition via TensorFlow/Keras neural networks** with **real-time camera input** and **Sudoku solving algorithms**.

## 🎯 Features

- **Real-time Camera Input**: Stream video from a webcam or IP camera to capture Sudoku puzzles
- **Digit Recognition**: Trained neural network model (CNN) recognizes handwritten digits using MNIST dataset
- **Image Processing**: Advanced preprocessing including:
  - Gaussian blur and adaptive thresholding
  - Contour detection and perspective transformation
  - Cell extraction and digit isolation
- **Sudoku Solving**: Backtracking algorithm to solve recognized puzzles
- **Visual Feedback**: Display detected digits, corners, and final solved board

## 📋 Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [How It Works](#how-it-works)
- [Project Structure](#project-structure)
- [Requirements](#requirements)
- [Model Details](#model-details)
- [Demo](#demo)

## 🚀 Installation

### Prerequisites
- Python 3.x
- pip package manager

### Step 1: Clone the Repository
```bash
git clone https://github.com/thecodealchemy/Sudoku_tensorflow_Camera.git
cd Sudoku_tensorflow_Camera
```

### Step 2: Install Dependencies
```bash
pip install -r requirements.txt
```

Key dependencies:
- OpenCV (cv2)
- TensorFlow & Keras
- NumPy
- scikit-image
- Pillow

## 💻 Usage

### Option 1: Process a Static Image
```bash
python "Camera processing.py"
```
This processes `image4.jpg` and extracts the Sudoku grid from it.

### Option 2: Real-time Camera Stream
```bash
python "pic solver.py"
```
This connects to a camera stream (configure the camera URL in the code) and:
1. Continuously captures frames
2. Detects the Sudoku puzzle
3. Recognizes all digits
4. Solves the puzzle
5. Displays the original and solved boards

### Option 3: Phone Camera Input
```bash
python "phone input camera.py"
```
Alternative implementation for mobile device camera streaming.

### Option 4: Sudoku Solver Only
```bash
python "solver.py"
```
Standalone Sudoku solver using backtracking algorithm.

## 🔍 How It Works

### 1. Image Preprocessing
- Read image in grayscale
- Apply Gaussian blur to reduce noise
- Use adaptive thresholding to create binary image
- Dilate the image to enhance features
- Bitwise NOT to invert colors for contour detection

### 2. Sudoku Grid Detection
- Find contours in the processed image
- Identify the largest contour (the Sudoku grid)
- Calculate corner points using coordinate geometry
- Apply perspective transformation to obtain a top-down view

### 3. Cell Extraction
- Divide the warped grid into 81 cells (9×9)
- Extract each cell and resize to 28×28 pixels (MNIST standard)
- Clear borders to isolate digits

### 4. Digit Recognition
- Load pre-trained CNN model (`models/mnist_keras_cnn_model.h5`)
- Pass each cell through the network
- Filter out empty cells (pixel count < threshold)
- Return recognized digit matrix

### 5. Sudoku Solving
- Validate the recognized board
- Apply backtracking algorithm:
  - Find empty cell (value = 0)
  - Try digits 1-9
  - Check validity (row, column, 3×3 box constraints)
  - Recursively solve
  - Backtrack if no valid solution found
- Display solved puzzle

## 📁 Project Structure

```
Sudoku_tensorflow_Camera/
├── Camera processing.py          # Process static Sudoku image
├── pic solver.py                 # Real-time camera solver
├── phone input camera.py         # Mobile camera input
├── solver.py                     # Standalone Sudoku solver
├── image4.jpg                    # Sample Sudoku image
├── image.jpg                     # Another sample image
├── TEST CASES.pdf                # Test documentation
├── digitrecog.h5                 # Legacy model (alternative)
├── models/
│   └── mnist_keras_cnn_model.h5  # Trained digit recognition model
├── Digit-recognition-using-Neural-networks-master/
│   ├── 1.PNG, 2.PNG              # GUI screenshots
│   └── testing numbers/          # Sample digit images
└── sudokusolver-master/          # Original sudoku solver reference
```

## 📦 Requirements

| Library | Version | Purpose |
|---------|---------|---------|
| OpenCV | 3.0+ | Image processing & camera capture |
| TensorFlow | 1.12+ | Neural network framework |
| Keras | 2.2.4+ | High-level API for models |
| NumPy | 1.15.4+ | Numerical computations |
| scikit-image | - | Image segmentation (clear_border) |
| Pillow | - | Image manipulation |

Install all at once:
```bash
pip install opencv-python tensorflow keras numpy scikit-image pillow
```

## 🧠 Model Details

### Digit Recognition Model
- **Architecture**: Convolutional Neural Network (CNN)
- **Training Dataset**: MNIST (70,000 handwritten digit images)
- **Input Size**: 28×28 pixels (grayscale)
- **Output**: Digit classification (0-9)
- **File**: `models/mnist_keras_cnn_model.h5` (~5MB)

### Sudoku Solver Algorithm
- **Type**: Backtracking with constraint satisfaction
- **Time Complexity**: O(9^(n²)) in worst case, much faster for valid puzzles
- **Validation Rules**: Standard Sudoku (rows, columns, 3×3 boxes)

## 📺 Demo

See the project in action:
- **YouTube Demo**: [Python SudokuSolver with Digit Recognition](https://www.youtube.com/watch?v=vAqjE539V70&feature=youtu.be)

### Expected Output
```
-----ϟϴÐṲḰṲ------

Original Sudoku:
[5, 3, 0, 0, 7, 0, 0, 0, 0]
[6, 0, 0, 1, 9, 5, 0, 0, 0]
...

   ___________________  
 
 Solved board:->
[5, 3, 4, 6, 7, 8, 9, 1, 2]
[6, 7, 2, 1, 9, 5, 3, 4, 8]
...
```

## 🔧 Configuration

### Camera Stream URL
In `pic solver.py`, modify:
```python
cam = cv2.VideoCapture('http://10.42.0.209:8080/video')
```
Change to your camera's IP address or use `0` for default webcam.

### Minimum Pixel Threshold
Control digit recognition sensitivity:
```python
minreqpixels = 90  # Adjust this value
```

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Report bugs and issues
- Suggest improvements
- Optimize performance
- Add new features

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

## 📚 References

- **MNIST Dataset**: [Yann LeCun's MNIST Page](http://yann.lecun.com/exdb/mnist/)
- **Medium Article**: [SudokuSolver Guide](https://medium.com/@neshpatel)
- **Original Inspiration**: [ffahri's Sudoku Solver](https://github.com/ffahri)

## 👤 Author

**TheCodeAlchemy**
- GitHub: [@thecodealchemy](https://github.com/thecodealchemy)

## ⚠️ Notes

- Requires a clear, well-lit image of a printed or handwritten Sudoku puzzle
- Recognition accuracy depends on image quality and digit clarity
- Works best with standard 9×9 Sudoku grids
- Camera-based input requires stable framing for best results

---

**Made with ❤️ by The Code Alchemy**
