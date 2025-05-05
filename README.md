# SVGDreamer for Windows - Installation Guide (Fixed)

This guide provides a reliable way to install SVGDreamer on Windows systems. This updated version fixes the common NumPy and PyTorch compatibility issues.

## Prerequisites

- Windows 10 or 11
- Python 3.9 (important: do not use Python 3.10 or newer)
- Git installed

## Step 1: Install Python 3.9

1. Download Python 3.9 from [python.org](https://www.python.org/downloads/release/python-3913/)
   - Download "Windows installer (64-bit)"
   - **Important**: During installation, check the box for "Add Python to PATH"

2. Verify installation in Command Prompt:
   ```
   python --version
   ```
   You should see `Python 3.9.x`

## Step 2: Install Git

1. Download Git from [git-scm.com](https://git-scm.com/download/win)
2. Run the installer with default options
3. Verify installation:
   ```
   git --version
   ```

## Step 3: Install Miniforge (for Mamba)

1. Download Miniforge from this direct link:
   [Miniforge3-Windows-x86_64.exe](https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Windows-x86_64.exe)

2. Run the installer and follow these steps:
   - Select "Just Me" for installation type
   - **CRITICAL**: Check the box that says "Add Miniforge3 to my PATH environment variable"
   - Complete the installation

3. **Initialize the shell** (CRITICAL):
   - Open a new Command Prompt (not PowerShell)
   - Run:
     ```
     mamba shell init -s cmd.exe
     ```
   - Close and reopen Command Prompt

4. Verify installation:
   ```
   mamba --version
   ```

## Step 4: Clone the Repository

```
git clone https://github.com/saedarm/SVGDreamerforDummies.git
cd SVGDreamerforDummies
```

**IMPORTANT**: All remaining commands should be run from the SVGDreamerforDummies directory.

## Step 5: Create and Activate Environment

```
mamba create --name svgdreamer python=3.9 -y
mamba activate svgdreamer
```

## Step 6: Install PyTorch with SPECIFIC VERSIONS

For CPU-only Users:
```
mamba install pytorch=1.12.1 torchvision=0.13.1 torchaudio=0.12.1 cpuonly -c pytorch -y
```

For NVIDIA GPU Users (if you have a compatible GPU):
```
mamba install pytorch=1.12.1 torchvision=0.13.1 torchaudio=0.12.1 cudatoolkit=11.3 -c pytorch -y
```

## Step 7: Install Compatible Dependencies

It's critical to install a compatible NumPy version first:
```
pip install numpy==1.24.3
```

Then install the remaining requirements:
```
pip install -r requirements.txt
```

## Step 8: Configure for Model Download

While still in the SVGDreamerforDummies directory:

1. Open the file `conf/config.yaml` 
2. Add or modify:
   ```yaml
   diffuser:
     download: True
   ```
3. Save the file

## Step 9: Run Your First Example

```
mamba activate svgdreamer
python svgdreamer.py x=lowpoly "prompt='A mountain landscape'" result_path='./logs/FirstTest' diffuser.download=True
```

## Troubleshooting Common Issues

### NumPy Compatibility Issues

If you see errors about NumPy versions or "numpy.core.multiarray failed to import":

1. Make sure you've installed the exact version of NumPy we specified:
   ```
   pip install numpy==1.24.3
   ```

2. If that doesn't work, try an even older version:
   ```
   pip install numpy==1.23.5
   ```

### PyTorch Version Conflicts

If you see errors about PyTorch version conflicts:

1. Make sure you install PyTorch, torchvision, and torchaudio with specific versions and BEFORE installing other requirements:
   ```
   pip uninstall -y torch torchvision torchaudio
   mamba install pytorch=1.12.1 torchvision=0.13.1 torchaudio=0.12.1 cpuonly -c pytorch -y
   ```

## Credits

This is a simplified fork of the [original SVGDreamer project](https://github.com/ximinng/SVGDreamer) with fixes for common Windows compatibility issues.
