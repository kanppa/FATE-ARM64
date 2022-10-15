FROM ubuntu:bionic-20220913

WORKDIR /root

RUN echo "Asia/Shanghai" > /etc/timezone

RUN : \
    && apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        software-properties-common \
    && add-apt-repository -y ppa:deadsnakes \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        python3.8-venv \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && :

RUN python3.8 -m venv /venv && mkdir -p /venv/lib/python3.8/lib2to3/fixes && cp /usr/lib/python3.8/lib2to3/fixes/*.py /venv/lib/python3.8/lib2to3/fixes

ENV PATH=/venv/bin:$PATH VIRTUAL_ENV=/venv

RUN python3.8 -m pip install --upgrade pip && pip install cmake

RUN apt-get update && apt-get install -y gcc wget vim curl xz-utils && curl https://sh.rustup.rs -sSf | bash -s -- -y

ENV PATH=${PATH}:/root/.cargo/bin

COPY libsm3py-0.0.1 libsm3py-0.0.1/

RUN pip install setuptools_rust && cd libsm3py-0.0.1 && python setup.py install

RUN rm -rf libsm3py-0.0.1

RUN wget https://github.com/llvm/llvm-project/releases/download/llvmorg-9.0.1/clang+llvm-9.0.1-aarch64-linux-gnu.tar.xz \
    && tar xJvf clang+llvm-9.0.1-aarch64-linux-gnu.tar.xz && mv clang+llvm-9.0.1-aarch64-linux-gnu clang-llvm-9.0.1 \
    && rm -f clang+llvm-9.0.1-aarch64-linux-gnu.tar.xz

ENV PATH=/root/clang-llvm-9.0.1/bin:$PATH

RUN apt-get update && \
    apt-get install -yq tzdata && \
    ln -fs /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata

ENV TZ="Asia/Shanghai"

RUN apt-get install -y g++ make libssl-dev libgmp-dev  libmpc-dev \
     libmpfr-dev gfortran libopenblas-dev liblapack-dev libsm-dev  \
    pkg-config libblas-dev libatlas-base-dev zlib1g-dev libtinfo-dev \
    python3.8-dev python-dev iputils-ping && apt-get clean