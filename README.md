# **Wav2Lip**: *Accurately Lip-syncing Videos In The Wild*

[Original Paper](http://arxiv.org/abs/2008.10010) 


Prerequisites
-------------
- `Python 3.6` 
- ffmpeg: `sudo apt-get install ffmpeg`
- Install necessary packages using `pip install -r requirements.txt`. 
- Face detection [pre-trained model](https://www.adrianbulat.com/downloads/python-fan/s3fd-619a316812.pth) should be downloaded to `face_detection/detection/sfd/s3fd.pth`. Alternative [link](https://iiitaphyd-my.sharepoint.com/:u:/g/personal/prajwal_k_research_iiit_ac_in/EZsy6qWuivtDnANIG73iHjIBjMSoojcIV0NULXV-yiuiIg?e=qTasa8) if the above does not work.

Lip-syncing videos using the pre-trained models (Inference)
-------
You can lip-sync any video to any audio:
```bash
python inference.py --checkpoint_path <ckpt> --face <video.mp4> --audio <an-audio-source> 
```
The result is saved (by default) in `results/result_voice.mp4`. You can specify it as an argument,  similar to several other available options. The audio source can be any file supported by `FFMPEG` containing audio data: `*.wav`, `*.mp3` or even a video file, from which the code will automatically extract the audio.

##### Tips for better results:
- Experiment with the `--pads` argument to adjust the detected face bounding box. Often leads to improved results. You might need to increase the bottom padding to include the chin region. E.g. `--pads 0 20 0 0`.
- If you see the mouth position dislocated or some weird artifacts such as two mouths, then it can be because of over-smoothing the face detections. Use the `--nosmooth` argument and give another try. 
- Experiment with the `--resize_factor` argument, to get a lower resolution video. Why? The models are trained on faces which were at a lower resolution. You might get better, visually pleasing results for 720p videos than for 1080p videos (in many cases, the latter works well too). 
- The Wav2Lip model without GAN usually needs more experimenting with the above two to get the most ideal results, and sometimes, can give you a better result as well.


Acknowledgements
----------
Parts of the code structure is inspired by this [TTS repository](https://github.com/r9y9/deepvoice3_pytorch). I thank the author for this wonderful code. The code for Face Detection has been taken from the [face_alignment](https://github.com/1adrianb/face-alignment) repository. We thank the authors for releasing their code and models. I thank [zabique](https://github.com/zabique) for the tutorial collab notebook.
