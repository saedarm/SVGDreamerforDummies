# SVGDreamer for Windows - Using Mamba for Fast Installation

This guide provides a reliable way to install SVGDreamer on Windows using Mamba, which is a much faster alternative to Conda. Mamba can be up to 10x faster than Conda when resolving complex environments, making it ideal for installing machine learning tools like SVGDreamer.

## What is SVGDreamer?

SVGDreamer is a text-to-SVG tool that can generate vector graphics from text prompts. Unlike raster-based AI image generators, SVGDreamer outputs fully editable vector graphics in SVG format, which can be used in any design software.

## Prerequisites

- Windows 10 or 11
- 8GB+ RAM
- Internet connection
- NVIDIA GPU (optional but recommended)

## Step 1: Install Mambaforge

Mamba is a drop-in replacement for Conda that's faster and better at resolving dependencies. Mambaforge is the recommended way to install Mamba on Windows.

1. Download Mambaforge from: https://github.com/conda-forge/miniforge#mambaforge
   - Choose the Windows installer that matches your system (usually the 64-bit version)
   
2. Run the installer and follow these specific steps:
   - Click "Next" through the welcome screen
   - Accept the license agreement
   - Select "Just Me" for installation type (recommended)
   - Keep the default installation location
   - **IMPORTANT**: Check the box that says "Add Mambaforge3 to my PATH environment variable"
   - Complete the installation

3. **Verify Installation**: 
   - Open a new Command Prompt (not Anaconda Prompt) 
   - Run: `mamba --version`
   - You should see the Mamba version number

## Step 2: Clone the Repository

Open Command Prompt and run:

```
git clone https://github.com/saedarm/SVGDreamerforDummies.git
cd SVGDreamerforDummies
```

## Step 3: Create and Activate Environment

Using Mamba instead of Conda makes this step much faster:

```
mamba create --name svgdreamer python=3.9 -y
mamba activate svgdreamer
```

## Step 4: Install PyTorch with Mamba

Mamba uses the same commands as Conda but executes them much faster. Let's install PyTorch:

### For NVIDIA GPU Users:
```
mamba install pytorch==1.12.1 torchvision==0.13.1 torchaudio==0.12.1 cudatoolkit=11.3 -c pytorch -y
```

### For CPU-only Users:
```
mamba install pytorch==1.12.1 torchvision==0.13.1 torchaudio==0.12.1 cpuonly -c pytorch -y
```

## Step 5: Install Additional Dependencies

We've included a `requirements.txt` file in the repository with all the other necessary dependencies:

```
pip install -r requirements.txt
```

## Step 6: Configure for Model Download

SVGDreamer needs to download a pretrained model. Configure this in the settings:

1. Open the file `conf/config.yaml` in the repository
2. Find or add the following lines:
   ```yaml
   diffuser:
     download: True
   ```
3. Save the file

## Step 7: Run Your First Example

Now you're ready to generate your first SVG! Make sure you have the environment activated:

```
mamba activate svgdreamer
python svgdreamer.py x=lowpoly "prompt='A mountain landscape with trees and a lake'" result_path='./logs/FirstTest' diffuser.download=True
```

The first run will take longer as it downloads the model. Be patient!

## Finding Your Generated SVGs

When the process completes (which might take several minutes):

1. Look in the `logs/FirstTest` folder
2. Find files with `.svg` extension
3. Open them with any web browser or vector editing program like Adobe Illustrator, Inkscape, etc.

## Different Styles to Try

SVGDreamer supports various artistic styles:

### Low-Poly Style
```
python svgdreamer.py x=lowpoly "prompt='A bald eagle in flight'" result_path='./logs/Eagle'
```

### Pixel Art Style
```
python svgdreamer.py x=pixelart "prompt='A retro-style spaceship'" result_path='./logs/Spaceship'
```

### Painting Style
```
python svgdreamer.py x=painting "prompt='Sunset over mountains in Van Gogh style'" x.num_paths=256 result_path='./logs/Sunset'
```

### Sketch Style
```
python svgdreamer.py x=sketch "prompt='Portrait of a wolf'" result_path='./logs/Wolf'
```

## Troubleshooting

### "Mamba not recognized" Error

If you see this error, try:

1. Use the `conda init` equivalent for Mamba:
   ```
   mamba init
   ```

2. Or add these paths to your system PATH (replace YourUsername with your actual Windows username):
   ```
   C:\Users\YourUsername\mambaforge
   C:\Users\YourUsername\mambaforge\Scripts
   C:\Users\YourUsername\mambaforge\Library\bin
   ```

### Out of Memory Errors

Add `state.mprec='fp16'` to your command to use less memory:

```
python svgdreamer.py x=lowpoly "prompt='A simple mountain'" result_path='./logs/Test' state.mprec='fp16'
```

## Each Time You Want to Use SVGDreamer

Remember to activate the environment before running any commands:

```
mamba activate svgdreamer
```

---

This guide uses Mamba instead of Conda to drastically speed up the installation process. Mamba is a drop-in replacement for Conda that solves dependencies much faster while maintaining full compatibility with the Conda ecosystem.
