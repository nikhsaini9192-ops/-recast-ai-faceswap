# RECAST — AI Character Face-Swap Tool

An AI-powered pipeline that replaces a specific character's face in a video clip with a reference person's face — while keeping the original acting, expressions, and dialogue timing intact.

Built as a personal project to learn practical computer vision: face detection, identity embeddings, and frame-by-frame video processing under real infrastructure constraints (free cloud GPUs, library version conflicts, memory limits).

## What it does

- Detects and swaps **only one target character's face** in a video, using face-embedding matching — other people in the frame are left untouched
- Preserves natural eye blinking and lip movement by blending them back from the original footage instead of letting restoration models flatten them
- Matches skin tone and lighting to the scene rather than fully overriding it with the reference photo's tone
- Accepts multiple reference photos (different angles) and averages them into a more robust identity
- Skips/handles extreme side-angle frames gracefully, since the underlying swap model is weakest there
- Runs entirely on free-tier cloud GPUs (Google Colab / Kaggle)

## Tech stack

| Purpose | Library/Model |
|---|---|
| Face detection & embeddings | [InsightFace](https://github.com/deepinsight/insightface) (buffalo_l) |
| Face swap | inswapper_128 |
| Face restoration | [GFPGAN](https://github.com/TencentARC/GFPGAN) |
| Video I/O | OpenCV, FFmpeg |
| Upload UI | ipywidgets |

## How to run

1. Open `RECAST.ipynb` in Google Colab or Kaggle Notebooks
2. Set the runtime accelerator to a GPU
3. Run the cells top to bottom — you'll be prompted to upload a video and 2-5 reference photos
4. Download the final output from the last cell

## Known limitations

- The swap model (inswapper_128) struggles with extreme side-angle/profile shots — this is a limitation of the open-source model itself, not something a wrapper pipeline can fully fix
- Frame-by-frame inference has no temporal-consistency network, so very fast motion can occasionally look rough
- Free-tier GPUs (T4) mean a 10-second clip takes several minutes to process

## Responsible use

This project is for **learning and personal creative use only**. Do not use it to create content of real people without their explicit consent. Always disclose AI-generated content when sharing it.

## License

MIT (or choose your preferred license)
