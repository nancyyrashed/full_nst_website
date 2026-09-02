# Neural Style Transfer Web Application

A **Streamlit** web app that lets users apply several different Neural Style Transfer (NST) techniques to their own images and videos through an interactive interface — upload a content image (and, depending on the method, a style image), pick a model, and download the stylized result. This is the deployed web app from my final-year Computer Science project at Goldsmiths, University of London.

**Live Demo:** https://neural-style-transfer-graduation-25.streamlit.app/

## Supported Methods

The app's method picker offers:

| Method | What you upload | How it works |
|---|---|---|
| **ADAIN** | Content image + style image | Adaptive Instance Normalization — applies any style image at inference time, no retraining needed. |
| **Dumoulin** | Content image + a style index (0–39) | Conditional Instance Normalization (CIN) — picks from 40 pre-learned styles via a style code, shown as a reference grid (`style_index.png`). |
| **Dumoulin V2** | Content image + style image | An extension combining CIN and AdaIN, so it can generalize to *unseen* style images rather than only the 40 baked-in styles. |
| **Dumoulin V2 Multi-Style** | Content image + two style images | Applies one style to the left half of the image and a second style to the right half, using the Dumoulin V2 model. |
| **Dumoulin V2 Video** | Content video (MP4/GIF) + style image | Applies the Dumoulin V2 model frame-by-frame to a video. MP4s are automatically converted to GIF for processing. |
| **Johnson** | Content image + a choice of 3 fixed styles | A feed-forward network, trained separately for each of 3 styles ("Starry Night", "Scream", "The River Seine at Chatou"). |

> **Note:** Gatys et al.'s optimization-based method is **not** included in this deployed app (it's too slow for interactive use) — it exists only as a notebook in the companion research repo, [`graduation-project-final`](https://github.com/nancyyrashed/graduation-project-final).

## Contents

| File / Folder | Description |
|---|---|
| `full_app.py` | The entire Streamlit app: page routing, per-model UI, and inference functions. |
| `requirements.txt` | Python dependencies. |
| `packages.txt` | System packages needed at deploy time (`ffmpeg`, `libgl1-mesa-glx`). |
| `.devcontainer/` | Dev Container config for one-click setup in GitHub Codespaces. |
| `*.pth` / `*.ckpt` | Pretrained model weights bundled with the app (AdaIN decoder, Johnson per-style networks, Dumoulin/Dumoulin V2 checkpoints). |
| `style_index.png` | Reference sheet showing which artwork corresponds to each Dumoulin style index (0–39). |
| `nst-example.png`, `content.jpg`, `c1.jpg`, `000000000008.jpg`, `style1.jpg`, `style2.jpg`, `wave.jpg`, `video2.gif` | Example images/GIF shown in the app's landing page and sidebar. |

## How It Works

- **`full_app.py`** uses `st.session_state.page` as a simple router: a main menu lets the user pick a method, and each method has its own page function (`adain_app`, `dumoulin_app`, `dumoulin_v2_app`, `dumoulin_v2_multi_app`, `dumoulin_v2_video_app`, `johnson_app`).
- Each page function handles file upload, calls a corresponding `stylize_*()` function that loads the relevant PyTorch model/checkpoint and runs inference, then displays the result with a **Download** button.
- Shared preprocessing (`get_image_transforms`, `load_image_from_path`) and ImageNet normalization/denormalization utilities are defined once at the top of the file and reused across models.
- Video stylization (`dumoulin_v2_video_app`) converts MP4 input to GIF via OpenCV + ImageIO when needed, applies the model frame-by-frame, and reassembles the result.
- A sidebar ("Example Images") shows sample content/style images and a sample stylized video/GIF for reference.

## Requirements

```bash
pip install -r requirements.txt
```

`requirements.txt` includes: `streamlit`, `torch`, `torchvision`, `Pillow`, `numpy`, `scipy`, `opencv-python-headless`, `imageio`, `imageio-ffmpeg`, `moviepy`.

On Linux/deployment environments, also install the system packages in `packages.txt`:

```
libgl1-mesa-glx
ffmpeg
```

## Usage

### Run locally

```bash
pip install -r requirements.txt
streamlit run full_app.py
```

Then open the local URL Streamlit prints (usually `http://localhost:8501`).

### Run in GitHub Codespaces

The included `.devcontainer/devcontainer.json` installs `requirements.txt`/`packages.txt` and launches `streamlit run full_app.py` automatically when the Codespace attaches, forwarding port `8501`.

### Using the app

1. From the main page, choose an NST method from the dropdown and click **Go**.
2. Upload the required image(s) (and/or a video, for the video method).
3. Click **Start Stylization** and wait for processing (video stylization can take several minutes and works best under 30 seconds of footage).
4. Click **Download Stylized Image/Video** to save the result.
5. Use **Back to Main Page** to try a different method.

## Technologies Used

**Frontend:** Streamlit

**Backend / ML:** Python, PyTorch, TensorFlow, Keras

**Computer Vision / Media:** OpenCV, Pillow, ImageIO, FFmpeg

**Data Processing:** NumPy, Matplotlib, Seaborn
