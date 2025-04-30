# Interactive Image Analyzer

A simple C++ desktop application built with SFML OpenCV and ImGui allowing users to load images select a Region of Interest (ROI) and apply various image processing analyses and effects with real-time visual feedback.

## Features

* Load common image formats (PNG JPG JPEG).
* Select a rectangular Region of Interest (ROI) using mouse drag.
* Apply the following analyses/effects to the selected ROI:
    * Grayscale Histogram calculation (basic info displayed).
    * Canny Edge Detection (adjustable low/high thresholds).
    * ORB Feature Detection (keypoints drawn).
    * Gaussian Blur (adjustable kernel size).
    * Binary Thresholding (adjustable threshold value).
    * Haar Cascade Face Detection (adjustable scale factor min neighbors min size).
* Real-time preview of the applied effect within the ROI overlayed on the original image.
* GUI controls using ImGui for parameter adjustments and actions.
* Cross-platform file dialogs using tinyfiledialogs.

## Dependencies

This project relies on several external libraries.

1.  **SFML 3.0+**: (Simple and Fast Multimedia Library) Used for windowing graphics rendering and event handling.
    * Required Components: `System`, `Window`, `Graphics`
    * Website: [https://www.sfml-dev.org/](https://www.sfml-dev.org/)
2.  **OpenCV 4.x**: (Open Source Computer Vision Library) Used for all image processing and analysis tasks.
    * Required Components: `core`, `imgproc`, `imgcodecs`, `highgui`, `features2d`, `objdetect`
    * Website: [https://opencv.org/](https://opencv.org/)
3.  **Dear ImGui (latest)**: Used for creating the graphical user interface controls.
    * Repo: [https://github.com/ocornut/imgui](https://github.com/ocornut/imgui)
4.  **ImGui-SFML (compatible with SFML 3)**: Binding library to integrate ImGui with SFML.
    * Repo: [https://github.com/SFML/imgui-sfml](https://github.com/SFML/imgui-sfml)
5.  **tinyfiledialogs**: Used for native open file dialogs.
    * Repo: [https://sourceforge.net/projects/tinyfiledialogs/](https://sourceforge.net/projects/tinyfiledialogs/) (or find on GitHub)
6.  **OpenGL**: Usually comes with your graphics drivers. CMake should find it automatically.

## Building

This project uses CMake for building.

1.  **Configure Library Paths:**
    * **Crucial Step:** Open the `CMakeLists.txt` file in the project root.
    * Locate the `set(... CACHE PATH ...)` commands near the top for `SFML_DIR`, `OpenCV_DIR`, `IMGUI_DIR`, `IMGUI_SFML_DIR`, and `TINYFILEDIALOGS_DIR`.
    * **Modify these paths** to point to the correct locations where you have downloaded/installed these libraries on *your* system. For OpenCV point it to the build directory containing `OpenCVConfig.cmake`. For SFML point it to the directory containing `SFMLConfig.cmake` (usually within `lib/cmake/SFML`). For ImGui ImGui-SFML and tinyfiledialogs point them to their respective source directories.
2.  **Configure Face Detection Cascade:**
    * Download the Haar Cascade XML file for frontal face detection: [`haarcascade_frontalface_default.xml`](https://raw.githubusercontent.com/opencv/opencv/master/data/haarcascades/haarcascade_frontalface_default.xml) (Right-click -> Save Link As...).
    * Place this downloaded `.xml` file in the **build output directory** where the final executable will be created (e.g. the `Debug` or `Release` folder after building or the main build folder depending on your generator). The application expects to find it in the same directory it runs from.
3.  **Generate Build Files using CMake:**
    * Create a build directory: `mkdir build && cd build`
    * Run CMake (adjust generator if needed e.g. for Visual Studio):
        ```bash
        # For Makefiles (Linux/macOS/MinGW)
        cmake ..

        # For Visual Studio (Windows - example for VS 2019)
        # cmake .. -G "Visual Studio 16 2019" -A x64
        ```
    * If CMake reports errors finding packages double-check the paths you set in `CMakeLists.txt`.
4.  **Compile the Project:**
    * Using Makefiles: `make`
    * Using Visual Studio: Open the generated `.sln` file in the `build` directory and build the `InteractiveImageAnalyzer` project.
    * Using other IDEs: Import the CMake project or open the generated project files.

## Usage

1.  Run the compiled executable (`InteractiveImageAnalyzer.exe` on Windows or `InteractiveImageAnalyzer` on Linux/macOS).
2.  Click the "Load Img..." button to open an image file.
3.  Click and drag on the displayed image to select a rectangular Region of Interest (ROI).
4.  Use the sliders in the "Analysis Controls" window to adjust parameters for different effects (Canny thresholds blur kernel size threshold value face detection parameters).
5.  Click the buttons ("Edges (ROI)" "Features (ROI)" "Blur (ROI)" "Thresh (ROI)" "Faces (ROI)") to apply the corresponding analysis to the selected ROI. The image display will update to show the result overlayed on the ROI.
6.  Click "Hist (ROI)" to calculate histogram info (displayed textually).
7.  Click "Show Original" to revert the display back to the original loaded image.

## License

**MIT License**
