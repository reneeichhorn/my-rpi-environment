FROM resin/rpi-raspbian:wheezy

# Install dependencies for build
RUN apt-get update
RUN apt-get upgrade
RUN apt-get install build-essential tk-dev libncurses5-dev libncursesw5-dev libreadline6-dev libdb5.3-dev libgdbm-dev libsqlite3-dev libssl-dev libbz2-dev libexpat1-dev liblzma-dev zlib1g-dev wget unzip -y

# Install python 3.6
RUN wget https://www.python.org/ftp/python/3.6.5/Python-3.6.5.tar.xz --no-check-certificate
RUN tar xf Python-3.6.5.tar.xz && \
    cd ./Python-3.6.5 && \
    ./configure && \
    make && \
    make altinstall

# Download bumper
RUN wget http://github.com/reneeichhorn/bumper/archive/master.zip --no-check-certificate
RUN unzip master.zip

# Setup bumper
ENV PYTHON_VERSION=3.6
ENV PYTHONPATH=/usr/local/bin
RUN pip3.6 install --user pipenv
RUN cd bumper-master/ && \
    ~/.local/bin/pipenv install --dev

WORKDIR bumper-master
CMD ~/.local/bin/pipenv run python3.6 bumper.py
