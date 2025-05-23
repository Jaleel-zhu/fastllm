# 使用 Ubuntu 20.04 作为基础镜像
FROM ubuntu:20.04

# 设置非交互式安装环境
ENV DEBIAN_FRONTEND=noninteractive

# 安装基础工具和GCC版本
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    software-properties-common \
    wget \
    ca-certificates \
    && add-apt-repository -y ppa:ubuntu-toolchain-r/test \
    && apt-get update \
    && apt-get install -y \
    g++-10 \
    g++-11 \
    && rm -rf /var/lib/apt/lists/*

# 设置G++多版本配置
RUN update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-10 50 \
    && update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-11 60 \
    && update-alternatives --set g++ /usr/bin/g++-11

# 安装CUDA 11.3
RUN wget https://developer.download.nvidia.com/compute/cuda/11.3.0/local_installers/cuda_11.3.0_465.19.01_linux.run \
    && sh cuda_11.3.0_465.19.01_linux.run --silent --toolkit --override \
    --no-drm --no-man-page --no-opengl-libs --installpath=/usr/local/cuda-11.3 \
    && rm cuda_11.3.0_465.19.01_linux.run

# 安装CUDA 12.1
RUN wget https://developer.download.nvidia.com/compute/cuda/12.1.0/local_installers/cuda_12.1.0_530.30.02_linux.run \
    && sh cuda_12.1.0_530.30.02_linux.run --silent --toolkit --override \
    --no-drm --no-man-page --no-opengl-libs --installpath=/usr/local/cuda-12.1 \
    && rm cuda_12.1.0_530.30.02_linux.run

# 配置CUDA环境变量（默认使用11.3）
ENV PATH=/usr/local/cuda-11.3/bin:${PATH}
ENV LD_LIBRARY_PATH=/usr/local/cuda-11.3/lib64:${LD_LIBRARY_PATH}

# 创建版本切换符号链接
RUN ln -sf /usr/local/cuda-11.3 /usr/local/cuda

# 验证安装
RUN g++ --version
RUN nvcc --version

RUN apt-get update
RUN apt-get install cmake -y
RUN apt-get install libnuma-dev -y
RUN apt-get install python3-pip -y
RUN pip install setuptools wheel

RUN apt remove --purge cmake -y
RUN pip install cmake==3.25.0 -i https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple
