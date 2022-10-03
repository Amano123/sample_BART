FROM tensorflow/tensorflow:2.10.0-gpu

ARG USER_NAME
ARG USER_ID
ARG GROUP_ID

ENV USER ${USER_NAME}
ENV HOME /home/${USER}
ENV PATH=${HOME}/.local/bin:${PATH}

# サーバーを日本に変更
# 多分早くなる
RUN sed -i 's@archive.ubuntu.com@ftp.jaist.ac.jp/pub/Linux@g' /etc/apt/sources.list

# #パッケージインストール
RUN apt-get update \
    &&  apt-get install -y --no-install-recommends \
    sudo \
    git \
    #japanase
    language-pack-ja-base \
    language-pack-ja \
    iputils-ping \
    locales  \
    python3 \
    python3-pip \
    gcc \
    wget make cmake

# 日本語化
RUN locale-gen ja_JP.UTF-8 
ENV LANG ja_JP.UTF-8
ENV LC_CTYPE ja_JP.UTF-8
RUN localedef -f UTF-8 -i ja_JP ja_JP.utf8


## make user
RUN set -x \
    &&  echo "Starting with UID : ${USER_ID}, GID: ${GROUP_ID}" \
    &&  adduser --disabled-password --gecos "" "${USER_NAME}" \
    &&  echo "${USER_NAME}:${USER_NAME}" | chpasswd \
    &&  echo "%${USER_NAME}    ALL=(ALL)   NOPASSWD:    ALL" >> /etc/sudoers.d/${USER_NAME}  \
    &&  chmod 0440 /etc/sudoers.d/${USER_NAME} \
    &&  usermod -u ${USER_ID} ${USER_NAME} \
    &&  groupmod -g ${GROUP_ID} ${USER_NAME} 

# ディレクトリを指定
USER $USER_NAME
WORKDIR ${HOME}/workspace

RUN set -x && wget https://github.com/ku-nlp/jumanpp/releases/download/v2.0.0-rc3/jumanpp-2.0.0-rc3.tar.xz \
    &&  tar Jxfv jumanpp-2.0.0-rc3.tar.xz \
    &&  cd jumanpp-2.0.0-rc3 \
    &&  mkdir bld \
    &&  cd bld \
    &&  cmake .. \
    -DCMAKE_BUILD_TYPE=Release \ 
    -DCMAKE_INSTALL_PREFIX=${HOME}/.local \
    && make install -j10 \
    && rm -rf ./jumanpp*

# # RUN pip install setuptools
RUN git clone -b japanese_bart_pretrained_model https://github.com/utanaka2000/fairseq.git \
    &&  cd fairseq \
    &&  pip install --editable ./
# RUN pip install "git+https://github.com/utanaka2000/fairseq.git@japanese_bart_pretrained_model"
RUN pip install \
    zenhan \
    pyknp \
    sentencepiece 

WORKDIR ${HOME}/workspace