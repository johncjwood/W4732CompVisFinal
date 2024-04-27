# W4732CompVisFinal
Repository to store the shared code for W4732 Computer Vision Final paper.
Collaborators:
jacob.wahbeh@columbia.edu (jew2173)
john.wood@columbia.edu (jw4159)

Purpose:
Jupyter notebooks to do data collection, data processing, and model creation / training.

Note that there are some norms that are implicit to these notebooks due to the fact that Jacob and I were using MS Windows machines w/ 24GB dedicated GPU RAM and 100+GB of traditional RAM.
We also had fairly sizable local storage, which facilitated storing raw arrays of tensors and other activities that may have been prohibitive on machines with less than 500GB of available HDD space.
This includes Windows-style folder structures and security norms.
This also includes a non-use of certain Linux-based conveniences such as symbolic links / aliases / etc.
Finally, some software like Pratt or FFMPEG should be available cross-platform, but we decided it was outside of the scope of this project to make the code convenient to use cross-platform / environment.

- Data collection
  - Audio Processing.ipynb contains the code to
    - Download MP4s from archive.org (search for BeautifulSoup code)
    - Extract MP3s from MP4s
    - Extract WAVs from MP3s
    - Perform speaker diarization (i.e. identify which speaker performed which task)
    - Use speaker diarization to split the wav files into clips
    - Create our target dataset using Pratt on the clips files (pitch, intensity, jitter, shimmer, harmonics)
    - Calculate the median of these values for a speaker-based median value
    - Saves the values into pickle files
  - Manual work - created speakers.json which identifies which speaker is talking in each segmentation file
  - Video Processing.ipynb contains the code to
    - Read the MP4s (already previously downloaded)
    - Downscale the videos to 640x360 resolution, greyscale, and 10fps
    - Use the speaker diarization (in segmentation folder) to split the mp4 into clips
  - Model and Testing.ipynb contains the code for
    - The video dataloader which reads both the pratt pickles as well as the mp4 clips
    - Using the video dataloader to convert the mp4 clips to 5d video frames (batch, channel, depth (time), length, width )
    - Training the neural network
  - Video Scratchpad JW.ipynb
    - Takes the MP4s, does the preprocessing, and saves the array of frames into a pickle in sourcedf folder
    - Also uses CV2 to perform face detection, which is then used to reduce each frame from 640x360 to 150x150 in sourcefacedf, and each frame is stored in a pickle
    - Availability of these source pickle files are necessary for the other JW codesets
  - Model Scratchpad JW.ipynb
    - Scratchpad for training a variety of neural network architectures - latest version was a simple linear-only model
  - Model Scratchpad JW Face.ipynb
    - Scratchpad for training the neural network model that used the 150x150 face-detected frames
