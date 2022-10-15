FROM cjf/python-38-ubuntu:1.0

ARG version

USER root

WORKDIR /data/projects/python/

COPY requirements.txt /data/projects/python/


RUN pip install --upgrade pip && \
    sed -i '/tensorflow.*/d' /data/projects/python/requirements.txt && \
    sed -i '/torch.*/d' /data/projects/python/requirements.txt && \
    sed -i '/torchvision.*/d' /data/projects/python/requirements.txt && \
    sed -i '/pytorch-lightning.*/d' /data/projects/python/requirements.txt && \
    pip install -r requirements.txt && pip cache purge

ENV LD_PRELOAD=/venv/lib/python3.8/site-packages/scikit_learn.libs/libgomp-d22c30c5.so.1.0.0
