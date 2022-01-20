# SBMC Installation

## Docker-less installation

- For those who cannot or do not want to use docker for any reasons, please follow the steps below.
- Notes
    - Some packages (kornia, scipy, pandas) do not strictly follow the dependencies, and installing them via [setup.py](http://setup.py/) provided leads to compile errors & dependency issues. Therefore we manually install them as step 3.
    - Due to the outdated pytorch==1.2.0 and halide==0.8.0, currently this code is hard to be reproduced on RTX 30 series GPUs. We recently tested that the project runs concretely on RTX 2080 Ti and RTX 8000. If you have any problems, please leave the issue. Also, if you have any suggestions, please bring it up!

### Installation Steps

1. Set&install apt-get packages
    
    ```bash
    apt-get update && apt-get install -y --no-install-recommends apt-utils
    apt-get install -y \
            build-essential \
            vim \
            git \
            bash \
            liblz4-dev \
            libopenexr-dev \
            curl \
            bison \
            libomp-dev \
            cmake \
            flex \
            qt5-default \
            libeigen3-dev \
            wget \
            unzip \
            libncurses5-dev \
            liblz4-dev
    ```
    
2. Install Halide (old version)
    
    ```bash
    wget -O halide.tgz https://github.com/halide/Halide/releases/download/v8.0.0/halide-linux-64-gcc53-800-65c26cba6a3eca2d08a0bccf113ca28746012cc3.tgz
    tar zvxf halide.tgz
    rm halide.tgz
    export HALIDE_DISTRIB_DIR=PUT_YOUR_HALIDE_DIRECTORY
    ```
    
3. Install python packages
    
    I assume that you use miniconda
    
    ```bash
    conda create -n sbmc python=3.7
    conda activate sbmc
    conda install pytorch==1.2.0 torchvision==0.4.0 cudatoolkit=10.0 -c pytorch
    pip install --upgrade pip && pip install pytest
    pip install kornia==0.2.0 scipy pandas
    ```
    
4. Install halide-pytorch & packages provided by SBMC following the original setup
    
    ```bash
    git clone https://github.com/Mephisto405/SBMC-Manifold.git
    cd SBMC-Manifold/halide_pytorch
    python setup.py install
    cd ..
    python setup.py develop
    ```
    

### References

- halide
    
    [](https://github.com/halide/Halide/releases/download/v8.0.0/halide-linux-64-gcc53-800-65c26cba6a3eca2d08a0bccf113ca28746012cc3.tgz)
    
- kornia==0.2.0
    
    [Release Data augmentation API, color conversion improvements, GPU tests and more · kornia/kornia](https://github.com/kornia/kornia/releases/tag/v0.2.0)
    
- in case of facing lzlib error
    
    ["/usr/bin/ld: cannot find -lz"](https://stackoverflow.com/questions/3373995/usr-bin-ld-cannot-find-lz)