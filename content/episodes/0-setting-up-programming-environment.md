
## Setup Enviornment

### Setup on LUMI Supercomputer
You should now be able to login to LUMI via On-demand interface [web interface](https://www.lumi.csc.fi/pun/sys/dashboard/). Click the `Go to login` button and you can choose Jupyter.

**<large> Setup your environment</large>**

- **Reservation:** workshopvenv
- **Project:** project_465002387
- **Partition:** dev-g

**<large> Resources</large>**

- **Number of CPU cores:** 8
- **Memory (GiB):** 8
- **Number of GPUs:** 1
- **Time:** 3:00:00

**<large> Settings</large>**

- **Working directory:** /projappl/project_465002387
- **Show advanced settings**: 1
- **Python:** pytorch
- **Module version:** pytorch/2.7
- **Custom Python type**: Container
- **Modules to load**: Leave empty
- **Path to container with Python:**

        
```
/projappl/project_465002387/DEEP_Inspection_Material_Science/lumi-multitorch-full-u24r64f21m43t29-20260124_092648.sif
```
- **Container arguments:**

        
```
-B /var/spool/slurmd,/opt/cray/,/usr/lib64/libcxi.so.1 --env LD_LIBRARY_PATH=/opt/cray-deps:/opt/cray/libfabric/1.15.2.0/lib64:/opt/cray/pe/mpich/8.1.29/ofi/crayclang/17.0/lib:/opt/cray/pe/lib64:/opt/cray/pe/lib64/cce:/opt/rocm-6.2.0/lib:/opt/aws-ofi-rccl:/.singularity.d/libs
```
- **Init script for container:**
```
export JUPYTER_RUNTIME_DIR=$HOME/.local/share/jupyter/runtime; export JUPYTER_DATA_DIR=$HOME/.local/share/jupyter; source /projappl/project_465002387/DEEP_Inspection_Material_Science/workshopvenv/bin/activate
```

- **Enable virtual environment**: 1
- **Virtual environment path**:
``` 
/projappl/project_465002387/DEEP_Inspection_Material_Science/workshopvenv
```


Now launch! A "Connect to jupyter" button will appear in a few minutes. 
Then you need to open the terminal and paste these lines:

```
mkdir -p $HOME/.jupyter_checkpoints
echo "c.FileContentsManager.checkpoints_kwargs = {'root_dir': '$HOME/.jupyter_checkpoints'}" >> ~/.jupyter/jupyter_lab_config.py

source /projappl/project_465002387/DEEP_Inspection_Material_Science/workshopvenv/bin/activate
python -m ipykernel install --user --name=python3-venv --display-name "Python 3 (venv)"

```

You can create your own subdirectory in our project folder and copy the material:
             
```cd /projappl/project_465002387/DEEP_Inspection_Material_Science/
mkdir <my_name>
cd <my_name>
cp -r /projappl/project_465002387/DEEP_Inspection_Material_Science/notebooks .
```

### Setup in Local Computer

**<large> Installing Python</large>**

Python is a popular language for machine learning projects. To install Python, follow the [Beginner's Guide](https://wiki.python.org/moin/BeginnersGuide/Download) or head straight to the [download page](https://www.python.org/downloads/).

Please set up your python environment at least a day in advance of the workshop.
If you encounter problems with the installation procedure, ask your workshop organizers via e-mail for assistance so
you are ready to go as soon as the workshop begins.

:::::::::::::::::::::::::::::::::::::::::::::::::::

**<large> Installing the required packages</large>**

[Pip](https://pip.pypa.io/en/stable/) is the package management system built into Python.
Pip should be available in your system once you installed Python successfully.

Open a terminal (Mac/Linux) or Command Prompt (Windows) and run the following commands.

1. Create a [virtual environment](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/#create-and-use-virtual-environments) called `workshopvenv`:

**<large> On Linux/macOs</large>**
```
python3 -m venv workshopvenv
```


**<large> On Windows</large>**

```
py -m venv workshopvenv
```

:::

2. Activate the newly created virtual environment:

::: spoiler

**<large> On Linux/macOs</large>**

```
source workshopvenv/bin/activate
```

**<large> On Windows</large>**

```
workshopvenv\Scripts\activate.ps1
```


Remember that you need to activate your environment every time you restart your terminal!

3. Install the required packages:

**<large> On Linux/macOs</large>**

```
python3 -m pip install jupyter seaborn scikit-learn numpy pandas matplotlib tqdm torch torchinfo torchaudio torchvision torchsummary anomalib ultralytics
```

**<large> On Windows</large>**

```
py -m pip install jupyter seaborn scikit-learn numpy pandas matplotlib tqdm torch torchinfo torchaudio torchvision torchsummary anomalib ultralytics
```

<!-- end-tab --><!-- end-tab -->



## Starting Jupyter Lab

We will teach using Python in [Jupyter Lab][jupyter], a programming environment that runs in a web browser.
Jupyter Lab is compatible with Firefox, Chrome, Safari and Chromium-based browsers.
Note that Internet Explorer and Edge are *not* supported.
See the [Jupyter Lab documentation](https://jupyterlab.readthedocs.io/en/latest/getting_started/accessibility.html#compatibility-with-browsers-and-assistive-technology) for an up-to-date list of supported browsers.

To start Jupyter Lab, open a terminal (Mac/Linux) or Command Prompt (Windows), 
make sure that you activated the virtual environment you created for this course,
and type the command:

```
jupyter lab
```

## Check your setup
To check whether all packages installed correctly, start a jupyter notebook in jupyter lab as explained above. Run the following lines of code:

```python
import sklearn
print('sklearn version: ', sklearn.__version__)

import seaborn
print('seaborn version: ', seaborn.__version__)

import pandas
print('pandas version: ', pandas.__version__)

import torchinfo
print('torchinfo version: ', torchinfo.__version__)

import torch
print('PyTorch version: ', torch.__version__)
```

This should output the versions of all required packages without giving errors. Most versions will work fine with this lesson.


<!-- end-tab -->

::::

**Alternatively** you can use [Google colab](https://colab.research.google.com/). If you open a jupyter notebook here, most of the required packages are already pre-installed. Note that google colab uses jupyter notebook instead of Jupyter Lab. The prepared dataset and notebooks for this workshop can be downloaded from the following link: [material](https://uppsalauniversitet-my.sharepoint.com/:f:/g/personal/marzieh_saeedimasine_uppmax_uu_se/IgC95jx7o7ZlS7qiSxkQ0UyvAc4RoIzzJXtkeOQOUEnDN7k?e=1tnauL)


## Downloading the required datasets
Severstal: Steel Defect Detection is a dataset from the 2019 Kaggle Challenge [Severstal](https://www.kaggle.com/c/severstal-steel-defect-detection), designed for surface defect detection tasks, including multiclass object detection, instance segmentation, and semantic segmentation.

In this workshop, we use the original dataset and select a subset of images for the exercises. The prepared dataset for this workshop can be downloaded from the following link: [data](https://uppsalauniversitet-my.sharepoint.com/:f:/g/personal/marzieh_saeedimasine_uppmax_uu_se/IgC95jx7o7ZlS7qiSxkQ0UyvAc4RoIzzJXtkeOQOUEnDN7k?e=1tnauL)
