Detectron2 for Windows (Pre-compiled Wheels: CUDA & CPU)
Building Detectron2 from scratch on Windows is notoriously difficult due to C++ compilation and CUDA environment issues. This repository provides pre-built, ready-to-install .whl files for both CUDA (NVIDIA GPUs) and CPU-only environments.

📦 Available Packages
You will find two ZIP files in the release/artifacts section. Extract the one that suits your hardware to get the detectron2-0.6-cp310-cp310-win_amd64.whl file:

detectron2-windows-cuda-wheel.zip (High Performance)

Target: Systems with dedicated NVIDIA GPUs.

Supported Architectures: 7.5 to 8.9.

Supported GPUs: GTX 16xx series (e.g., GTX 1650), RTX 20xx, RTX 30xx, and RTX 40xx series.

Note: Older NVIDIA GPUs (like GTX 10-series), AMD, and Intel GPUs are NOT supported by this build.

detectron2-windows-cpu-wheel.zip (Universal Fallback)

Target: Any Windows PC or Laptop without a supported NVIDIA GPU.

Pros: Guaranteed to work anywhere.

Cons: Slower inference time as it relies entirely on the CPU.

⚙️ System Requirements
To successfully install and run these wheels, the target machine must meet the following requirements:

OS: Windows 10 or Windows 11 (64-bit).

Python Version: Strictly Python 3.10 (Make sure to check "Add Python to PATH" during installation).

NVIDIA Driver (For CUDA version only): Update your NVIDIA driver to version 522.06 or newer.

🚀 Quick Auto-Installation (Recommended)
To avoid environment conflicts and version mismatches, use the provided auto-installer script.

Extract the downloaded ZIP file to get the detectron2-0.6-cp310-cp310-win_amd64.whl file.

Create a new text file in the exact same folder, name it setup.bat (make sure the extension is .bat, not .txt).

Right-click setup.bat, select Edit, and paste the following code:

DOS
@echo off
title Setup Detectron2 Environment
color 0A

echo ===================================================
echo      Detectron2 Auto-Installer (Windows)
echo ===================================================
echo.

:: 1. Check Python version
echo Checking Python version...
python --version | findstr "3.10" >nul
if errorlevel 1 (
    echo [ERROR] Python 3.10 is required but not found as default!
    echo Please install Python 3.10 and check "Add to PATH".
    pause
    exit /b
)
echo [OK] Python 3.10 detected.
echo.

:: 2. Create Virtual Environment
echo [1/4] Creating Virtual Environment (env)...
python -m venv env
call env\Scripts\activate

:: 3. Upgrade PIP
echo.
echo [2/4] Upgrading PIP...
python -m pip install --upgrade pip

:: 4. Install PyTorch with CUDA 11.8 support
echo.
echo [3/4] Installing PyTorch (2.4.1+cu118)...
pip install torch==2.4.1+cu118 torchvision==0.19.1+cu118 torchaudio==2.4.1+cu118 --index-url https://download.pytorch.org/whl/cu118

:: 5. Install Detectron2 Wheel
echo.
echo [4/4] Installing Detectron2...
for %%f in (detectron2*.whl) do (
    pip install "%%f"
    goto :done_d2
)
echo [WARNING] Detectron2 .whl file not found! Please place it next to this script.
pause
exit /b

:done_d2
:: 6. Install other computer vision requirements
echo.
echo Installing additional libraries (OpenCV, Matplotlib, Numpy, PyCocoTools)...
pip install opencv-python matplotlib numpy pillow pycocotools

echo.
echo ===================================================
echo   [SUCCESS] Environment is fully set up and ready!
echo ===================================================
pause
Save the file and simply Double-Click setup.bat. It will create a clean virtual environment, download the exact PyTorch version needed, and install Detectron2 seamlessly.

🛠️ Manual Installation
If you prefer to install it manually in your own environment, run the following commands in your terminal:

Bash
# 1. Install the specific PyTorch version compatible with this build
pip install torch==2.4.1+cu118 torchvision==0.19.1+cu118 torchaudio==2.4.1+cu118 --index-url https://download.pytorch.org/whl/cu118

# 2. Install the Detectron2 wheel (change the filename if necessary)
pip install detectron2-0.6-cp310-cp310-win_amd64.whl
