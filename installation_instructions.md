# Installation Instructions for Jupyter Notebooks Workshop. 

We recommend that you install Jupyter on Docker or using Anaconda prior to the workshop. If you install using Docker, please perform the optional step of saving the pulled image locally. This should save you the trouble of doing it during the workshop.

After installation, please follow the instructions to get the research data from GitHub, because the datasets are large and may take a while to download.

Options:

## Option 1. Installing Jupyter as part of Anaconda (Windows, Mac, Linux)

Minimum System Requirements: macOS 10.12.3 or higher is recommended. Linux version is also available. 32-bit and 64-bit systems are supported.

Anaconda is the leading open-source data science platform powered by Python.

1. Download and install Python 2.7 or 3.6 from https://www.python.org/downloads/
2. Download R and install from WUSTL cran mirror at http://cran.wustl.edu/
3. Download and install the appropriate version of Anaconda from https://www.continuum.io/downloads/ 
4. Go to command line/ terminal
  1. Install R Kernel using command line/ terminal:
	`conda install -c r r-irkernel=0.7.1`
  2. Install popular R packages
	`conda install -c r r-essentials`
  3. Start Jupyter Notebook
	`jupyter notebook`
5. In Jupyter notebook,create a new notebook file for R Kernel, and inside a cell, run command to install package “C50” for decision tree analysis.
	`install.packages(“C50”, repo="https://cran.us.r-project.org”)`

Anaconda R essentials comes with 80+ R packages such as dplyr and ggplot2. 


## Option 2. Installing Jupyter on Docker (Windows, Mac, Linux)

Minimum System Requirements: macOS 10.8 “Mountain Lion” or newer is required. Linux version is also available. Your system should be 64-bit. 

NOTE: $ (dollar sign) designates start of command you will run in Docker.

1. Download Docker Toolbox Installer and run it - https://www.docker.com/products/docker-toolbox. If you are running a newer version of macOS (10.10.3 Yosemite or newer), you may download full Docker for Mac: https://download.docker.com/mac/stable/Docker.dmg 
2. Start Docker Quickstart and let Docker start up. Make a note of the IP for default machine displayed below the whale picture. You will need to use it for Jupyter Server URL later.
3. Start up a docker machine, a) with default configuration
```
`$ docker-machine ssh default`
```
OR b) with specific configuration (allocates 6GB of RAM, but you can adjust that value)
```
`$ docker-machine rm default`
`$ docker-machine create -d virtualbox --virtualbox-memory=6144 --virtualbox-cpu-count=2 --virtualbox-disk-size=50000 default`
```

4. If you have internet connection, pull an image from Docker Hub, which contains Jupyter Notebook, and other modules. For this workshop run: 
```
$ docker pull conniez/all-spark-notebook
```

This might take some time, because the image is quite large (about 5.5GB). Technically, you can choose from several available official Jupyter images here: https://github.com/jupyter/docker-stacks. The image in the example is the extended version of this image jupyter/all-spark-notebook, and it contains Jupyter Notebooks, R Kernel, Spark and ggplot2.

5. Optional. You can save the pulled image locally (it will need about 5.5GB of space), so in case you destroy your default docker machine you can load the image from local directory instead of pulling it again from the Docker Hub. For example: 
```
$ docker save conniez/all-spark-notebook > jupyter_datasci.tar
```
6. At any point you then can load it (without relying on internet): `$ docker load < jupyter_datasci.tar`
Within that image, run a container, specifying port, local directory (outside VM) to mount the Notebook files to, and image name (change the bold path, but keep the rest the same): 

$ docker run -it --rm -p 8888:8888 -v **_/path/to/folder/to/mount/jupyter_**:/home/jovyan/work/notebooks conniez/all-spark-notebook

After the container is created you will be able to copy the URL where Jupyter Notebook is hosted on your computer. For example: http://localhost:8888/tree?token=5b4f2a261e48cec506822d3756381306f87c44a18a27079e. The token is for automatic login into the server. This URL can be pasted into your browser to access the Notebook server. You need to replace “localhost” with the default machine IP you have noted from the startup message in Docker Quickstart.

At this point, feel free to create Jupyter Notebooks through the UI. Any notebook files you create, you can access in the directory you mounted the Container to. For example: /c/Users/Username/Documents/Notebooks. You can also create folders inside that directory to keep resource files for data or copy other scripts.

## Option 3. For Advanced Users: Installing Jupyter from Command Line 

We will not cover this option during the workshop, this might not work on all systems.

Prerequisites: Python and R

```
sudo easy_install pip 
pip install jupyter
```

Install R, if you haven’t already

Go to: https://github.com/IRkernel/IRkernel/blob/master/README.md. Inside R run:
```
install.packages('devtools')
devtools::install_github('IRkernel/IRkernel')
```
Start Jupyter Notebook by running this command at command line/terminal: 
```
jupyter notebook
```

In Jupyter notebook,create a new notebook file for R Kernel, and inside a cell, run command to install packages “dplyr” and “C50” for use in the workshop.
```
install.packages(c(“dplyr”, “C50”),repos= “https://cran.rstudio.com/”)
```

# Please Download the Research Data from GitHub

To save time during the workshop, please download the data files prior to the workshop if possible. Download the notebooks folder in this repo, which contains the following files required for the workshop:

- **seerdic.pdf** - data dictionary that came with SEER breast cancer data, BREAST.TXT
- **original_data.rdata** - SEER breast cancer data, parsed from BREAST.TXT and stored as data.frame for R
- **start.txt** - starting position of each meaningful variable in BREAST.TXT
- **width.txt** - length of each meaningful variable in BREAST.TXT
- **name.txt** - SAS name of each meaningful variable in BREAST.TXT
- **ss_surg_surgprif_map.csv** - file mapping Site Specific Surgery codes between ontologies used in different time periods.
- **other Rdata files** - intermediate datasets saved from various steps in the notebooks to speed up demo at the workshop

The BREAST.TXT file was acquired by request from the SEER database: https://seer.cancer.gov/data/access.html

Because the BREAST.TXT file (breast cancer data in ASCII fixed-width format from SEER, see citation below) exceeds GitHub file limits, we were not able to share it here, however, you may download the exact copy from Box: https://wustl.box.com/s/h1s575j6399yq1z0p3j8uu42h3j43680

On the day of the workshop, the notebooks folder will also contain the actual Jupyter Notebooks file. You will need them to follow the workshop hands-on portion.

**SEER Data Citation:**

Surveillance, Epidemiology, and End Results (SEER) Program (www.seer.cancer.gov) Research Data (1973-2013), National Cancer Institute, DCCPS, Surveillance Research Program, Surveillance Systems Branch, released April 2016, based on the November 2015 submission.

