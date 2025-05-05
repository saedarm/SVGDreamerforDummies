# SVGDreamer for Windows - Installation Guide

This repository provides a simplified way to install and run SVGDreamer on Windows systems.

## What is SVGDreamer?

SVGDreamer is a text-to-SVG generation tool that can create fully editable vector graphics from text prompts. Unlike raster-based AI image generators, SVGDreamer outputs SVG files that can be edited in programs like Adobe Illustrator or Inkscape.

## Installation Steps

### Step 1: Install Python

1. Download Python 3.9 from [python.org](https://www.python.org/downloads/windows/)
   - **Important**: During installation, check the box for "Add Python to PATH"
   - Select "Install for all users" option

2. Verify installation in Command Prompt:
   ```
   python --version
   ```

### Step 2: Install Git

1. Download Git from [git-scm.com](https://git-scm.com/download/win)
2. Run the installer with default options
3. Verify installation:
   ```
   git --version
   ```

### Step 3: Install Mambaforge

Mamba is a much faster alternative to Conda that dramatically speeds up dependency resolution.

1. Download Mambaforge from [GitHub](https://github.com/conda-forge/miniforge#mambaforge)
   - Choose the Windows 64-bit version

2. Run the installer and follow these critical steps:
   - Select "Just Me" for installation type
   - **CRITICAL**: Check the box that says "Add Mambaforge3 to my PATH environment variable"
   - Complete the installation

3. Verify installation:
   - Open a new Command Prompt and run:
     ```
     mamba --version
     ```

### Step 4: Clone This Repository

```
git clone https://github.com/saedarm/SVGDreamerforDummies.git
cd SVGDreamerforDummies
```

### Step 5: Create and Activate Environment

```
mamba create --name svgdreamer python=3.9 -y
mamba activate svgdreamer
```

### Step 6: Install PyTorch with Mamba

#### For NVIDIA GPU Users:
```
mamba install pytorch==1.12.1 torchvision==0.13.1 torchaudio==0.12.1 cudatoolkit=11.3 -c pytorch -y
```

#### For CPU-only Users:
```
mamba install pytorch==1.12.1 torchvision==0.13.1 torchaudio==0.12.1 cpuonly -c pytorch -y
```

### Step 7: Install Additional Dependencies

```
pip install -r requirements.txt
```

### Step 8: Configure for Model Download

1. Open the file `conf/config.yaml` 
2. Add or modify:
   ```yaml
   diffuser:
     download: True
   ```
3. Save the file

### Step 9: Run Your First Example

```
mamba activate svgdreamer
python svgdreamer.py x=lowpoly "prompt='A mountain landscape with trees'" result_path='./logs/FirstTest' diffuser.download=True
```

The first run will take longer as it downloads the model. Your SVG files will be saved in the `logs/FirstTest` folder.

## Available Style Options

SVGDreamer supports several pre-configured styles:

### Low-Poly Style
```
python svgdreamer.py x=lowpoly "prompt='Your text here'" result_path='./logs/Output'
```

### Pixel Art Style
```
python svgdreamer.py x=pixelart "prompt='Your text here'" result_path='./logs/Output'
```

### Painting Style
```
python svgdreamer.py x=painting "prompt='Your text here'" x.num_paths=256 result_path='./logs/Output'
```

### Sketch Style
```
python svgdreamer.py x=sketch "prompt='Your text here'" result_path='./logs/Output'
```

### Iconography Style
```
python svgdreamer.py x=iconography "prompt='Your text here'" result_path='./logs/Output'
```

## Troubleshooting

### "Mamba not recognized" Error

If you see this error after installation:

1. Try initializing Mamba:
   ```
   C:\Users\YourUsername\mambaforge\Scripts\mamba init
   ```

2. Or add these paths to your system PATH:
   ```
   C:\Users\YourUsername\mambaforge
   C:\Users\YourUsername\mambaforge\Scripts
   C:\Users\YourUsername\mambaforge\Library\bin
   ```

## Credits

This is a simplified fork of the [original SVGDreamer project](https://github.com/ximinng/SVGDreamer) to make installation easier on Windows systems.

## License

The original SVGDreamer is licensed under MIT License.
