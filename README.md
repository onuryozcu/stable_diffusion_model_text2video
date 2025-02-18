# stable_diffusion_model_text2video

<div align="center">
<h3>
    Video Diffusion WebUI: Text2Video + Image2Video + Video2Video WebUI
</h3>
</div>

This repo is a Text2Video + Image2Video + Video2Video WebUI Implementation.
### Installation
```bash
pip install video-diffusion
```


### Making Videos

Note: For Apple M1 architecture, use ```torch.float32``` instead, as ```torch.float16``` is not available on MPS.

```python
from stable_diffusion_videos import StableDiffusionWalkPipeline
import torch

pipeline = StableDiffusionWalkPipeline.from_pretrained(
    "CompVis/stable-diffusion-v1-4",
    torch_dtype=torch.float16,
).to("cuda")

video_path = pipeline.walk(
    prompts=['a cat', 'a dog'],
    seeds=[42, 1337],
    num_interpolation_steps=3,
    height=512,  # use multiples of 64 if > 512. Multiples of 8 if < 512.
    width=512,   # use multiples of 64 if > 512. Multiples of 8 if < 512.
    output_dir='dreams',        # Where images/videos will be saved
    name='animals_test',        # Subdirectory of output_dir where images/videos will be saved
    guidance_scale=8.5,         # Higher adheres to prompt more, lower lets model take the wheel
    num_inference_steps=50,     # Number of diffusion steps per image generated. 50 is good default
)
```


- 🚀 Diffusion model result
- <p align="center">
    <img width="400" src="result.gif" alt="Mimari">
</p>
