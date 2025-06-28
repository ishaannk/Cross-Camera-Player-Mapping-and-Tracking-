# Cross-Camera Player Mapping and Tracking

This repository contains a Jupyter notebook (`Cross_Camera_Player_Mapping.ipynb`) that implements a system for mapping and tracking players across two video feeds (broadcast and tactician views) in a sports scenario, followed by player re-identification in a single video feed. The system uses the YOLOv11 model for object detection and centroid-based matching for player mapping.

## Prerequisites

To run the code, ensure you have the following:

- Python 3.11 or later
- A system with a GPU (recommended for faster YOLO inference; tested with NVIDIA T4)
- Access to the video files (`broadcast.mp4`, `tacticam.mp4`, `15sec_input_720p.mp4`)
- A pre-trained YOLOv11 model (`best.pt`)
- FFmpeg installed for video frame compilation

## Setup Instructions

1. **Clone the Repository**

   ```bash
   git clone https://github.com/ishaannk/Cross-Camera-Player-Mapping-and-Tracking-
   cd Cross-Camera-Player-Mapping-and-Tracking-
   ```

2. **Set Up a Virtual Environment** (recommended)

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install Dependencies**Install the required Python packages using pip:

   ```bash
   pip install opencv-python-headless ultralytics numpy scipy nest_asyncio
   ```

   Ensure the versions are compatible with Python 3.11. The notebook was tested with:

   - `opencv-python-headless==4.11.0.86`
   - `ultralytics==8.3.158`
   - `numpy==2.0.2`
   - `scipy==1.15.3`
   - `nest_asyncio` (latest version)

4. **Install FFmpeg**

   - On Ubuntu:

     ```bash
     sudo apt update
     sudo apt install ffmpeg
     ```
   - On macOS:

     ```bash
     brew install ffmpeg
     ```
   - On Windows, download FFmpeg from ffmpeg.org and add it to your system PATH.

5. **Prepare Input Files**

   - Place the following files in the project directory:
     - `best.pt`: Pre-trained YOLOv11 model file.
     - `broadcast.mp4`: Broadcast view video.
     - `tacticam.mp4`: Tactician view video.
     - `15sec_input_720p.mp4`: Single feed video for re-identification.
   - Update the file paths in the notebook if they differ from `/content/`.

6. **Run the Notebook**

   - Open the notebook in Jupyter:

     ```bash
     jupyter notebook Cross_Camera_Player_Mapping.ipynb
     ```
   - Execute the cells sequentially. The notebook is divided into sections:
     - **Dependency Installation**: Installs required Python packages.
     - **Cross-Camera Mapping**: Maps players between broadcast and tactician views using centroid-based matching.
     - **Single Feed Re-identification**: Tracks players in a single video feed.
     - **Frame Compilation**: Combines annotated frames into an output video (`output.mp4`) using FFmpeg.

## Output

- **Cross-Camera Mapping**: Generates `player_mapping.txt` with player correspondences between the two video feeds.
- **Single Feed Tracking**: Saves tracking data to `tracking_log.txt` and annotated frames as `frame_%d.jpg`.
- **Final Video**: Creates `output.mp4` from annotated frames.

## Notes

- Ensure the video files and model file are accessible in the specified paths.
- The notebook assumes a GPU environment for faster processing. CPU execution is possible but slower.
- The YOLO model (`best.pt`) must be trained to detect classes such as `player`, `goalkeeper`, `referee`, and `ball`.
- If the notebook fails to run, verify that all dependencies are installed correctly and file paths are updated.