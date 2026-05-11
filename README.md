# Senior Design Video Summary: Automated Collection & Summarization

Welcome to the **Senior Design Video Summary** repository! This project presents an end-to-end framework for automated video dataset generation and advanced video summarization.

Our approach addresses the challenge of creating concise, highly informative summaries from long videos by utilizing cutting-edge 3D Convolutional Neural Network (CNN) architectures. We also introduce a fully automated pipeline for downloading and processing YouTube videos to generate high-quality custom datasets.

---

##  Repository Structure

The repository is modularized into four primary components:

```text
.
├── Fully Automated Dataset Downloading Pipeline/
│   ├── 1. Query Focused Video Downloading.ipynb
│   ├── 2. Unique video selection.ipynb
│   ├── 3. Trimming Process (Best 2-10 Minutes of long videos).ipynb
│   └── 4. Compression.ipynb
├── Summe/
│   ├── I3D.ipynb
│   ├── R(2+1)D.ipynb
│   ├── Slowfast.ipynb
│   └── X3D.ipynb
├── Tvsum/
│   ├── I3D.ipynb
│   ├── R(2+1)D.ipynb
│   ├── Slowfast.ipynb
│   └── X3D.ipynb
└── YTSUEN Dataset (Ours)/
    ├── I3D.ipynb
    ├── R(2+1)D.ipynb
    ├── Slowfast.ipynb
    └── X3D.ipynb
```

---

##  Project Modules

### 1. Fully Automated Dataset Downloading Pipeline
Creating a high-quality dataset is often tedious. We developed a robust automated pipeline capable of collecting and preprocessing training data directly from YouTube:

- **Query-Focused Downloading**: Utilizes the YouTube Data API v3 and `yt-dlp` to fetch videos based on specific search queries, applying filters for minimum views, duration, and file size.
- **Unique Video Selection**: Extracts visual features (using pre-trained 3D ResNet) to identify and filter out visually identical or duplicate videos.
- **Automated Trimming**: Intelligently extracts the most relevant 2-10 minute segments from hours-long videos.
- **Compression**: Compresses the trimmed clips using `moviepy` and `ffmpeg` to ensure file sizes are manageable for training (e.g., under 30MB) without losing significant visual fidelity.

### 2. Video Summarization Datasets
We evaluate our summarization models on three distinct datasets:
- **SumMe**: A widely-used benchmark dataset for video summarization containing 25 diverse unedited user videos.
- **TVSum**: Another standard benchmark dataset consisting of 50 YouTube videos across 10 categories.
- **YTSUEN Dataset (Ours)**: A custom-built dataset constructed entirely using our automated downloading pipeline, demonstrating the real-world applicability of our dataset generation method.

### 3. Model Architectures
To perform state-of-the-art video summarization, we extract spatiotemporal features using various advanced 3D CNN models, available in their respective dataset folders:

- **I3D (Inflated 3D ConvNet)**: Seamlessly inflates 2D CNN weights into 3D, successfully leveraging temporal relationships in video frames.
- **R(2+1)D**: Decomposes spatial 2D convolutions and temporal 1D convolutions to capture complex spatiotemporal features more efficiently.
- **SlowFast**: Uses a dual-pathway architecture to process spatial semantics (Slow pathway) and motion features (Fast pathway) independently for superior video recognition.
- **X3D**: Progressively expands a tiny 2D image classification architecture across multiple axes (temporal, spatial, width, and depth) for optimized performance.

---

##  Setup & Requirements

All modules are provided as **Jupyter Notebooks**, designed to run in environments such as Google Colab, Kaggle, or a local Jupyter server with GPU support.

### Prerequisites
Ensure you have the following installed to run the notebooks locally:

- **Python 3.8+**
- **PyTorch & Torchvision**
- **PyTorchVideo** (for specialized video models)
- **OpenCV** (`opencv-python-headless`)
- **yt-dlp & FFmpeg** (for the dataset pipeline)
- Machine Learning metrics & plotting libraries: `scikit-learn`, `scipy`, `matplotlib`, `seaborn`

You can install standard dependencies directly inside the notebooks (as provided in the code cells), but ensure `ffmpeg` is installed on your local OS:
```bash
# Ubuntu/Debian
sudo apt update && sudo apt install ffmpeg

# Windows (Using Winget)
winget install ffmpeg
```

---

##  Usage

1. **Dataset Generation**: 
   Navigate to the `Fully Automated Dataset Downloading Pipeline` folder and execute the notebooks in numerical sequence (1 to 4). Ensure you replace the placeholder `API_KEY` in Notebook 1 with your own Google YouTube Data API Key.
   
2. **Model Evaluation**: 
   To evaluate a summarization model, pick a dataset directory (e.g., `Summe`, `Tvsum`, or `YTSUEN Dataset (Ours)`). Open the notebook corresponding to the model you wish to test (e.g., `I3D.ipynb`) and run the cells. The notebooks contain full pipelines for feature extraction, model definition, training/inference, and metric computation (F1-score, Precision, Recall, Kendall Tau, etc.).

---

*This project was developed as a Senior Design Capstone.*