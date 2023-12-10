## Installation and usage
### Linux OS
  1. Download Biomix from the github page and decompress it. The installation in the home directory is suggested. From bash type
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

  4. Run the BiomiX_INSTALL_LINUX.sh script within the _INSTALL folder.
```
  ./path/to/BiomiX2.2/_INSTALL/BiomiX_INSTALL_LINUX.sh
```
  5. Enjoy BiomiX!


### Windows OS
  1. Download Biomix from the github page and decompress it (by application e.i Winzip or terminal cmd). The installation in the home directory is suggest.
     If using the windows terminal type
```
  cd
  wget linktothelatestBiomiXversion
  tar -xvzf Biomix2.2.tar.gz
```
  2. BiomiX uses conda to install the r and python package dependencies. 
  Install conda from the website https://docs.conda.io/en/latest/miniconda.html

  3. Follow the installation instructions
  
  4. Open the search in Windows taskbar the application "Anaconda powershell prompt"

  5. Double click in the BiomiX_INSTALL_WINDOWS.bat script within the _INSTALL folder.

  5. Enjoy BiomiX!
   
### Troubleshooting
#### **ModuleNotFoundError: No module named 'package name'** 
It happens during the conda installation "step 2" because the python installed in your computer doesn't have. Can be fixed typing in the terminal: **pip install 'package name'**
#### BiomiX_INSTALL_WINDOWS.bat or BiomiX_INSTALL_LINUX.sh not working
It can happen that because of different package already installed something conflic can arise. We suggest you to visit the - Go to [alternative installation guide](Alternative_Installation.md), for a step by step installation.
