# Qt Installation Guide for Debian/Ubuntu

This guide documents the various methods to install Qt on Debian/Ubuntu systems, focusing on using mirrors for faster downloads.

## Table of Contents
1. [Method 1: Using System Package Manager (Recommended)](#method-1-using-system-package-manager)
2. [Method 2: Using aqtinstall (Fast Alternative)](#method-2-using-aqtinstall)
3. [Method 3: Using Qt Online Installer with Mirrors](#method-3-using-qt-online-installer-with-mirrors)
4. [Verifying Installation](#verifying-installation)
5. [Troubleshooting](#troubleshooting)

## Method 1: Using System Package Manager

The simplest and most stable method:

```bash
# Update package lists
sudo apt update

# Install basic Qt 6 development packages
sudo apt install -y \
    qt6-base-dev \
    qt6-base-dev-tools \
    qt6-tools-dev-tools \
    libqt6core6 \
    libqt6gui6 \
    libqt6widgets6

# For additional Qt modules:
# sudo apt install qt6-multimedia-dev qt6-quick3d-dev qt6-webengine-dev
```

## Method 2: Using aqtinstall (Fast Alternative)

For more control over Qt versions and components:

```bash
# 1. Create and activate a virtual environment
python3 -m venv ~/qt_venv
source ~/qt_venv/bin/activate

# 2. Install aqtinstall
pip install aqtinstall

# 3. Install specific Qt version with components
aqt install-qt linux desktop 6.5.3 gcc_64 \
    -m qtwebengine qtwebview qtmultimedia

# 4. Add to PATH (add to ~/.bashrc or ~/.zshrc)
echo 'export PATH="$HOME/Qt/6.5.3/gcc_64/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

## Method 3: Using Qt Online Installer with Mirrors

For the official installer with faster downloads:

```bash
# 1. Make installer executable
chmod +x qt-online-installer-linux-x64-4.10.0.run

# 2. Run with mirror (choose closest to your location)
# Asia: https://mirrors.ustc.edu.cn/qtproject
# Europe: https://ftp.fau.de/qtproject
# North America: https://mirror.umd.edu/qtproject
# Japan: https://qt-mirror.dannhauer.org

./qt-online-installer-linux-x64-4.10.0.run --mirror https://mirrors.ustc.edu.cn/qtproject

# 3. Follow the GUI installer
#    - Skip account login if not needed
#    - Choose custom installation
#    - Select only needed components
```

## Verifying Installation

```bash
# For system package manager
qmake6 --version

# For aqtinstall
~/Qt/6.5.3/gcc_64/bin/qmake --version

# For online installer
# (Path depends on installation location)
~/Qt/Tools/QtCreator/bin/qtcreator --version
```

## Troubleshooting

### Slow Downloads
- Try different mirrors
- Use aqtinstall instead of the online installer
- Install during off-peak hours

### Missing Components
For system packages, search for additional modules:
```bash
apt search qt6-*
```

### SSL/Proxy Issues
```bash
# Set proxy if behind a corporate firewall
export http_proxy="http://proxy.example.com:port"
export https_proxy="http://proxy.example.com:port"
```

## License
This guide is provided as-is. Qt is licensed under both commercial and open source (GPL/LGPL) licenses.
