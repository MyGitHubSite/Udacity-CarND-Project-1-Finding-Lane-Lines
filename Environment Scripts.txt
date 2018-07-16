echo

rem install anaconda  https://www.anaconda.com/download/#windows

conda env remove -n dlnd

REM ***** INSTALL VIA ENVIRONMENT *****
conda env update --file environment-gpu.yml
conda clean -tipsy

REM ***** INSTALL VIA REQUIREMENTS *****
conda create -n dlnd pip python=3.6
activate dlnd
rem pip install -r requirements.txt

pip install --ignore-installed --upgrade tensorflow-gpu   
pip install --ignore-installed numpy pandas keras matplotlib scipy pillow opencv-contrib-python tdqm jupyter
rem pip install --ignore-installed plotly geopandas==0.3.0 pyshp==1.2.10 shapely==1.6.3
rem pip install csv urllibs cStringIO python-mpltoolkits.basemap

REM ***** CLEAN UP FILES *****
conda clean -tipsy

REM ***** TO FIX IPYTHON *****
rem conda remove ipykernel ipython jupyter_client jupyter_core traitlets ipython_genutils
rem conda install ipykernel ipython jupyter_client jupyter_core traitlets ipython_genutils
jupyter notebook

REM ***** TEST TENSORFLOW *****
$ python
>>> import tensorflow as tf
>>> hello = tf.constant('Hello, TensorFlow!')
>>> sess = tf.Session()
>>> print(sess.run(hello))

REM ***** UPDATE CONDA *****
conda update -n base conda
python -m pip install --upgrade pip

REM ***** RESOLUTIONS
pip install --ignore-installed --upgrade tensorflow_gpu
pip install --ignore-installed --upgrade moviepy
pip install --ignore-installed --upgrade requests