# xlwings
## Steps to configure miniforge with xlwings / PyTorch on Linux arm64 with CUDA support and Intel fallback

- walkthrough: https://www.youtube.com/watch?v=42d36a65fc9

- enable build tools on Linux once per machine: `sudo apt install build-essential`

# remove miniforge
```
conda activate your_env_name
conda install anaconda-clean
anaconda-clean # add `--yes` to skip confirmation prompts
sudo rm -r ~/miniforge/
nano ~/.bashrc
# -> Search for miniforge and delete the lines containing it
# -> If unsure, comment the line instead of deleting it
source ~/.bashrc
rm -rf ~/.miniforge_backup
```

# reinstall miniforge with env xlwings linux arm64
- Download miniforge arm64 Linux pkg:
- from: https://github.com/conda-forge/miniforge/releases
- Then in a terminal run all these commands
- `conda install -y jupyter`
- `conda create --name xlwings python=3.10`
- `conda activate xlwings`
- `conda install -c conda-forge nb_conda`
- `conda env update --file /path/to/xlwings-arm64.yml`
- `conda install -c conda-forge bokeh`
- then as usual, test with
- `jupyter notebook`
- and
- `python check_env.py`
```
# run: python check_env.py
import sys

import torch
import torchvision

print(f"PyTorch Version: {torch.__version__}")
print(f"Torchvision Version: {torchvision.__version__}")
print(f"Python {sys.version}")
cuda = torch.cuda.is_available()
print("CUDA is", "available" if cuda else "NOT AVAILABLE")
```

# Praktikum Deep Learning mit PyTorch und CUDA
- https://www.udemy.com/course/deep-learning-foundations
# Dev Contributor installation intel linux Python <= 3.9
- https://www.youtube.com/watch?v=42d36a65fc9
- https://github.com/hasuradev/xlwings/blob/master/install/env_setup.ipynb
```
# conda env remove -y --name nameof-env
conda env create -v -f xlwings-intel.yml
# conda create -y --name xlwings python=3.9
source activate xlwings
conda install -y numpy &&
conda install -y pandas &&
conda install -y matplotlib &&
conda install -y scikit-learn &&
conda install -y xlrd &&
conda install -y openpyxl &&
conda install -y lxml &&
conda install -y sqlalchemy &&
conda install -y seaborn &&
conda install -y -c plotly plotly &&
conda install -y -c conda-forge bokeh &&
conda install -y pandas-datareader &&
conda install -y pydot &&
conda install -y graphviz &&
conda install -y -v dask &&
conda install -y pip &&
conda install -y jupyter
conda update -y --all

pip install --upgrade torch==2.3.0
pip install --upgrade torchvision==0.18.0

python -m ipykernel install --user --name xlwings --display-name "Python 3.9 (xlwings)"
```
