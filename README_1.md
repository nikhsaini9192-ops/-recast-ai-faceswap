# RECAST

A video face-swap tool — replace one character's face in a clip with a reference photo, while keeping everything else in the scene (other people, the acting, the dialogue) untouched.

Started this as a way to actually learn computer vision hands-on instead of just reading about it — face detection, embeddings, working through a full video pipeline frame by frame, and dealing with the annoying practical stuff (free GPU limits, library versions breaking, figuring out why a step silently fails).

## What it does

- Locks onto a single character in the video (by face identity) and only swaps that person — anyone else on screen stays as they are
- Uses 2-5 of your own reference photos instead of just one, averaged together, for a more accurate match
- Keeps eye blinking and mouth movement natural — most restoration models tend to "smooth" these into something generic-looking, so this blends the original movement back in afterward
- Matches skin tone to the scene's lighting instead of just pasting the photo's tone directly
- Runs on free Kaggle/Colab GPUs, no local GPU needed

## Running it

Open `RECAST.ipynb` on Kaggle or Colab, turn the GPU on, and go through the cells in order. It'll ask for a video and a few photos partway through, and give you a download link for the result at the end.

## Stack

- InsightFace for detection + embeddings + the actual swap (inswapper_128)
- GFPGAN for restoration, used lightly and only on part of the frame
- OpenCV / FFmpeg for the video handling

## Where this falls short

The swap model isn't great at side profiles — it just wasn't trained on much of that, and no amount of post-processing really fixes it. There's a threshold in the notebook that trades off between skipping rough-looking angled frames vs. covering every frame, but it can't do both perfectly.

It's also frame-by-frame with no temporal smoothing model behind it, so fast motion can look a little inconsistent between frames.

## A note on using this

Don't use this on real people without their consent. This was built for learning and for messing around with footage/photos I have the rights to — that's the intended use.
