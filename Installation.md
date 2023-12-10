## Installation and usage
### Linux OS
  1. Download Biomix from the GitHub page and decompress it. The installation in the home directory is suggested. From bash type
```
  cd
  wget linktothelatestBiomiXversion
  tar -xvzf Biomix2.2.tar.gz
```
  2. BiomiX uses conda to install the r and a python package dependencies. 
  Install conda from the website: https://docs.conda.io/en/latest/miniconda.html or type on the bash 
```
  wget https://repo.anaconda.com/miniconda/Miniconda3-py310_23.3.1-0-Linux-x86_64.sh
  bash Miniconda3-py310_23.3.1-0-Linux-x86_64.sh
```
  3. Follow the instructions, selecting conda init = yes. Close and reopen the bash terminal.

  4. Run the BiomiX_INSTALL_LINUX.sh script within the _INSTALL folder and wait until the end of the installation.
```
  ./path/to/BiomiX2.2/_INSTALL/BiomiX_INSTALL_LINUX.sh
```
  5. Run the Biomix_exe.sh script within the BiomiX2.2 folder to open BiomiX and start your analysis.
```
  ./path/to/BiomiX2.2/Biomix_exe.sh
```
  6. Enjoy BiomiX!


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

  5. Double-click in the BiomiX_INSTALL_WINDOWS.bat script within the _INSTALL folder and wait until the end of the installation.

  6. Double-click on the Biomix_exe.bat script within the BiomiX2.2 folder to open BiomiX and start your analysis.

  7. Enjoy BiomiX!
   
### Troubleshooting
#### **ModuleNotFoundError: No module named 'package name'** 
It happens during the conda installation "step 2" because the python installed on your computer doesn't have it. This can be fixed by typing in the terminal: **pip install 'package name'**
#### BiomiX_INSTALL_WINDOWS.bat or BiomiX_INSTALL_LINUX.sh not working
It can happen that because of different packages already installed something conflict can arise. We suggest you visit the [alternative installation guide](Alternative_Installation.html), for a step-by-step installation.
