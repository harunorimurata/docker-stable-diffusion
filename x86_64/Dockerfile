# syntax=docker/dockerfile:1.3-labs
FROM debian:bullseye-slim

SHELL ["/bin/bash", "-c"]

RUN <<EOF
  set -ex
  apt update
  apt install -y wget git

  wget -O miniconda.sh -nv https://repo.anaconda.com/miniconda/Miniconda3-py39_4.12.0-Linux-x86_64.sh 
  bash miniconda.sh -b -p /opt/miniconda3
  echo export PATH="/opt/miniconda3/bin:$PATH" >> ~/.bashrc
  export PATH="/opt/miniconda3/bin:$PATH"
  conda init bash
  source ~/.bashrc

  cd /opt
  git clone https://github.com/CompVis/stable-diffusion.git
  cd stable-diffusion

  conda env create -f environment.yaml
  conda activate ldm
  conda install pytorch torchvision -c pytorch
  pip install transformers==4.19.2 diffusers invisible-watermark
  pip install -e .

  apt clean all
  pip cache purge
EOF

WORKDIR /opt/stable-diffusion

CMD ["BASH"]

