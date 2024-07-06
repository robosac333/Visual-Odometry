# Visual-Odometry-on-Monocular-Camera

![Visual Odometry on Kitti Sequence](VO.gif)

This project implements Visual Odometry using ORB features and the KITTI dataset to estimate camera pose from image sequences.

### Overview

The `VisualOdometry` class provides core functionality:
1. **Initialization**: Loads calibration data, ground truth poses, and images.
2. **Feature Detection and Matching**: Uses ORB to detect features and FLANN matcher for descriptor matching.
3. **Pose Estimation**: Computes the Essential matrix, decomposes it to find rotation and translation, and estimates camera pose.

### Detailed Explanation

1. **Initialization (`__init__`)**:
    - Load calibration (`K` and `P`), ground truth poses, and images.
    - Initialize ORB detector and FLANN matcher.

2. **Load Calibration Data (`_load_calib`)**:
    - Reads calibration file for intrinsic matrix `K` and projection matrix `P`.

3. **Load Ground Truth Poses (`_load_poses`)**:
    - Reads and formats ground truth poses as 4x4 matrices.

4. **Load Images (`_load_images`)**:
    - Loads grayscale images from the specified directory.

5. **Feature Matching (`get_matches`)**:
    - Detects and matches ORB keypoints between consecutive frames.
    - Filters matches using Lowe's ratio test.
    - Displays matches for visualization.

6. **Pose Estimation (`get_pose`)**:
    - Estimates Essential matrix and decomposes it to retrieve rotation `R` and translation `t`.
    - Constructs a transformation matrix.

7. **Decompose Essential Matrix (`decomp_essential_mat`)**:
    - Decomposes the Essential matrix into possible transformations.
    - Triangulates points to select the best transformation.

8. **Main Function (`main`)**:
    - Initializes `VisualOdometry` with dataset.
    - Iterates over poses, matches features, and estimates pose for each frame.
    - Visualizes estimated path against ground truth.

### Running the Code

1. Place the KITTI dataset in a directory (e.g., `VisualSLAM/KITTI_sequence_1`).
2. Ensure the directory contains `calib.txt`, `poses.txt`, and the `image_l` directory.
3. Run the script:
    ```sh
    python your_script_name.py
    ```

The system will display feature matches and plot the estimated path against the ground truth.
