# PSG Workshop Setup

This repository is intended for a hands-on workshop. Follow the steps below to set up your Python environment before opening the notebooks.

## 1. Create a conda environment/or a virtualenv environment
Download anaconda from here (https://www.anaconda.com/download/success?reg=skipped) 
OR
Use Python's built-in virtual environment package - venv 
OR
Download virtualenv from here (https://pypi.org/project/virtualenv/)

Create and activate a new environment using Python 3.12:

If using conda:
```bash
conda create -n psg_workshop python=3.12 -y
conda activate psg_workshop
```

If using virtualenv:
```bash
virtualenv -p python3.12 psg_workshop
.\psg_workshop\Scripts\activate.bat
```

## 2. Upgrade pip

```bash
python -m pip install --upgrade pip
```

## 3. Install IntelliMaint

Install the IntelliMaint package in the active environment:

```bash
pip install IntelliMaint
```

## 4. Install project requirements

Install the dependencies listed in this repository:

```bash
pip install -r requirements.txt
```

## 5. Install Jupyter

Install Jupyter so you can run the workshop notebooks:

```bash
pip install jupyter
```

To launch Jupyter Notebook:

```bash
jupyter notebook
```

## 6. Install PyTorch dependencies (if required)

If the workshop notebooks require PyTorch, install it with:

```bash
pip install torch torchvision
```

## 7. Download workshop tool data

Download the workshop tool data from the following link:

```text
https://intellipredikt1-my.sharepoint.com/:f:/g/personal/rachana_s_intellipredikt_com/IgD41Ogw2D9ZTZpPJFgiMkF4AWHkJpireiDMYXJTcgJQkbo?e=Ug0MtU 
```

Place the downloaded data in the Data folder in this repository before running the notebooks.

You are now ready to open and run the notebooks in this repository.
