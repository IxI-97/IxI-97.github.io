## Installation
### Linux OS
  1. Download Biomix from the GitHub page and decompress it. The installation in the home directory is suggested. From bash type
```
  cd
  wget linktothelatestBiomiXversion
  tar -xvzf Biomix2.2.tar.gz
```
  2. BiomiX uses conda to install the r and python package dependencies. 
  Install conda from the website: https://docs.conda.io/en/latest/miniconda.html or type on the bash 
```
  wget https://repo.anaconda.com/miniconda/Miniconda3-py310_23.3.1-0-Linux-x86_64.sh
  bash Miniconda3-py310_23.3.1-0-Linux-x86_64.sh
```
  3. Follow the instructions, selecting conda init = yes. Close and reopen the bash terminal.

  4. Create your BiomiX environment (BiomiX-env) in conda typing on the bash
```
  conda create -n BiomiX-env python=3.9 r-base=4.2.0 r-essentials
```
  5. Activate your BiomiX environment
```
  conda activate BiomiX-env
```
  6. Run the BiomiX_INSTALL Python script
```
  python3 path/to/BiomiX2.2/_INSTALL/BiomiX_INSTALL.py
```
  7. Enjoy BiomiX!


### Windows OS
  1. Download Biomix from the GitHub page and decompress it (by application e.g. Winzip or terminal cmd). The installation in the home directory is suggested.
     If using the Windows terminal type
```
  cd
  wget linktothelatestBiomiXversion
  tar -xvzf Biomix2.2.tar.gz
```
  2. BiomiX uses conda to install the r and python package dependencies. 
  Install conda from the website https://docs.conda.io/en/latest/miniconda.html

  3. Follow the installation instructions
  
  4. Open the search in the Windows taskbar for the application "Anaconda powershell prompt"

  5. Create your BiomiX environment (BiomiX-env) in conda typing on the conda PowerShell
```
  conda create -n BiomiX-env python=3.9
```
  6. Activate your BiomiX environment
```
  conda activate BiomiX-env
```
  7. Install the R and igraph package.
```
  conda install -c conda-forge r-base=4.1.3
  conda install -c conda-forge r-igraph
```
  8. Run the BiomiX_INSTALL Python script by clicking on it or typing in the conda PowerShell
```
  python path/to/BiomiX2.2/_INSTALL/BiomiX_INSTALL.py
```
  9. Enjoy BiomiX!

### Troubleshooting
#### **ModuleNotFoundError: No module named 'package name'** 
It happens during the conda installation "step 2" because the python installed on your computer doesn't have it. This can be fixed by typing in the terminal: **pip install 'package name'**
