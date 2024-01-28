# Introduction
## Docker environments for Jupyter with ML libraries (with Cuda GPU supports)
This project contains a docker image that includes the following NLP, Data Science or Machine Learning Python libraries.
- Numpy
- TensorFlow
- Scikit-learn
- PyTorch
- Pandas
- Matplotlib
- NLTK

*NOTE#1: This require around 20G for building image*
*NOTE#2: The docker container is inspired by the following command
```
docker run --rm -itd --gpus all -p 8888:8888 -v $(pwd)/docker-data:/content tensorflow/tensorflow:2.10.1-gpu-jupyter jupyter notebook --ip 0.0.0.0 --no-browser --allow-root --NotebookApp.token='' --NotebookApp.password='argon2:$argon2id$v=19$m=10240,t=10,p=8$gu1oaVTudqMVaMY+ufyldg$dXMYv+IMfcsfNv9ZiEReHp4KoXEb0bW0o8qYFUU13hg' 
```

# Getting started
```
git clone {this project}
```

## To build
```
docker build -t py3_jupyter .  
```

## To Run
### No Password, Token and IP binding
```
docker run --rm -itd --gpus all -p 8888:8888 -v $(pwd)/docker-data:/content py3_jupyter jupyter notebook --ip 0.0.0.0 --no-browser --allow-root --NotebookApp.token='' --NotebookApp.password='' 
```

### Use Password but no Token and IP binding
```
docker run --rm -itd --gpus all -p 8888:8888 -v $(pwd)/docker-data:/content py3_jupyter jupyter notebook --ip 0.0.0.0 --no-browser --allow-root --NotebookApp.token='' --NotebookApp.password='argon2:$argon2id$v=19$m=10240,t=10,p=8$gu1oaVTudqMVaMY+ufyldg$dXMYv+IMfcsfNv9ZiEReHp4KoXEb0bW0o8qYFUU13hg' 
```
### Use high IO
```
docker run --rm -itd --gpus all -p 8888:8888 -v $(pwd)/docker-data:/content py3_jupyter jupyter notebook --ip 0.0.0.0 --no-browser --allow-root --NotebookApp.token='' --NotebookApp.password='argon2:$argon2id$v=19$m=10240,t=10,p=8$gu1oaVTudqMVaMY+ufyldg$dXMYv+IMfcsfNv9ZiEReHp4KoXEb0bW0o8qYFUU13hg' --NotebookApp.iopub_data_rate_limit=10000000000
```

## Password generation
This project's password was generated by the following codes
```
from jupyter_server.auth import passwd
print(passwd('root@JyServer#123!')) 
```

## Restart and Clean
clean_run.sh is used for cleaning up all the containers and images and rebuild the image and then restart the container 

## Usage
```
http:\\{Your IP or host}:8888

#For example
http:\\127.0.0.1:8888
```


## Installation Check

### Check GPU - TensorFlow 
```
import tensorflow as tf
print("Num GPUs Available: ", len(tf.config.list_physical_devices('GPU'))) 
```

### Check GPU - PyTorch
```
import torch
torch.cuda.is_available() 
```

# Under Development
## python_jupyter_backup
The folder contains the jupyter image that will be built from scratch. It is still under-developed (1/27/2024)