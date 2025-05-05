# SVGDreamer for Dummies: No-Nonsense Windows Installation Guide

This guide provides straightforward steps to get SVGDreamer running on Windows with no unnecessary complications. Follow these instructions exactly to start generating SVG images from text prompts.

## Prerequisites

- Windows 10 or 11
- Python 3.8 or newer (3.10 recommended)
- Git installed
- (Optional but recommended) NVIDIA GPU with CUDA support

## Step 1: Clone the Repository

Open Command Prompt or PowerShell and run:

```
git clone https://github.com/saedarm/SVGDreamerforDummies.git
cd SVGDreamerforDummies
```

## Step 2: Install Dependencies

The repository already includes a ready-to-use `requirements.txt` file with all necessary dependencies and correct versions for Windows compatibility. Simply run:

```
pip install -r requirements.txt
```

This single command will install all the required packages. The installation might take a few minutes depending on your internet connection and computer speed.

### Note about xformers (for NVIDIA GPU users)

If you have an NVIDIA GPU and want better performance, the requirements file already includes xformers. If you encounter any errors related to xformers during installation or running, you can still use SVGDreamer - it will work without it, just a bit slower.

## Step 3: Download the Pretrained Model

SVGDreamer requires a pretrained Stable Diffusion model. To set it up automatically:

1. Open the file `conf/config.yaml` in the repository
2. Find or add the following lines:
   ```yaml
   diffuser:
     download: True
   ```
3. Save the file

## Step 4: Run Your First Example

Now you're ready to generate your first SVG. From the SVGDreamerforDummies directory, run:

```
python svgdreamer.py x=lowpoly "prompt='A mountain landscape with trees and a small lake'" result_path='./logs/MyFirstSVG' diffuser.download=True
```

This will:
- Run in low-poly style
- Create a mountain landscape scene
- Save results to the `logs/MyFirstSVG` folder
- Automatically download the Stable Diffusion model if needed

The first run will take longer as it downloads the model. Be patient - this might take several minutes depending on your internet connection.

## Step 5: Find Your SVG Files

When the process completes:

1. Look in the `logs/MyFirstSVG` folder
2. Find files with `.svg` extension - these are your vector graphics
3. Open them with a web browser or vector editing program

## Troubleshooting Common Issues

### "No module named X" Error

If you see an error like "No module named X", install the missing package:

```
pip install X
```

Replace "X" with the name of the missing module.

### Out of Memory Errors

If you encounter GPU memory errors, try adding the parameter `state.mprec='fp16'` to use less memory:

```
python svgdreamer.py x=lowpoly "prompt='Your text here'" result_path='./logs/Output' state.mprec='fp16'
```

### Slow Performance

On a CPU-only system, the generation will be slow. Be patient - it might take 10-30 minutes per image.

## More Examples

### Pixel Art Style
```
python svgdreamer.py x=pixelart "prompt='A retro-style spaceship'" result_path='./logs/Spaceship'
```

### Painting Style
```
python svgdreamer.py x=painting "prompt='Sunset over the ocean with palm trees'" x.num_paths=256 result_path='./logs/Sunset'
```

### Sketch Style
```
python svgdreamer.py x=sketch "prompt='A portrait of a cat'" result_path='./logs/CatSketch'
```

### Iconography Style
```
python svgdreamer.py x=iconography "prompt='A simple coffee cup icon'" result_path='./logs/CoffeeIcon'
```

## That's It!

No fluff, no unnecessary explanations - just the essential steps to get SVGDreamer running on Windows. If you want to explore more advanced features, check the official repository documentation.

---

*This guide is for the SVGDreamerforDummies repository, a simplified fork of the original SVGDreamer project by Ximing Xing et al.*
