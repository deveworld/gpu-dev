FROM nvidia/cuda:12.8.0-cudnn-devel-ubuntu24.04

LABEL org.opencontainers.image.description="An ai develop environment container"

ENV DEBIAN_FRONTEND=noninteractive
ENV PYTHON_VERSION=3.11
ENV UV_INSTALL_DIR="/usr/local/bin"
ENV MAX_JOBS=28

RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    build-essential \
    cmake \
    git \
    wget \
    unzip \
    ninja-build \
    git-lfs \
    libaio-dev \
    pkg-config \
    ca-certificates \
    && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /workspace

RUN curl -LsSf https://astral.sh/uv/install.sh | env UV_INSTALL_DIR=${UV_INSTALL_DIR} sh && \
    uv venv /opt/venv --python ${PYTHON_VERSION}

ENV PATH="/opt/venv/bin:${UV_INSTALL_DIR}:$PATH"

RUN uv pip install --no-cache-dir -U pip

RUN uv pip install --no-cache-dir transformers trl peft accelerate datasets evaluate && \
    uv pip install --no-cache-dir unsloth notebook jupyterlab ipywidgets && \
    uv pip install --no-cache-dir packaging wheel setuptools ninja
    
RUN uv pip install --no-cache-dir flash-attn --no-build-isolation

RUN uv pip install --no-cache-dir --no-build-isolation axolotl[flash-attn,deepspeed]

RUN uv pip install --no-cache-dir --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/cu128

EXPOSE 8000

CMD ["/opt/venv/bin/jupyter", "notebook", "--ip=0.0.0.0", "--no-browser", "--allow-root", "--NotebookApp.token=''", "--port=8000"]
