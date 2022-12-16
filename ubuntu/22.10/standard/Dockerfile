# docker build -t janzi/vsts-build-agents:ubuntu-22.10-standard standard/.

FROM janzi/vsts-build-agents:ubuntu-22.10-lite

ARG GO_VERSION=1.19.4
ARG CMAKE_MINOT_VERSION=3.25
ARG CMAKE_VERSION=${CMAKE_MINOT_VERSION}.0
ARG PY3_VERSION=3.6-v7.3.3

# Install CMake
RUN curl -sL https://cmake.org/files/v${CMAKE_MINOT_VERSION}/cmake-${CMAKE_VERSION}-linux-x86_64.sh -o cmake.sh \
 && chmod +x cmake.sh \
 && ./cmake.sh --prefix=/usr/local --exclude-subdir \
 && rm cmake.sh

RUN curl -sL https://dl.google.com/go/go${GO_VERSION}.linux-amd64.tar.gz -o go${GO_VERSION}.linux-amd64.tar.gz \
 && mkdir -p /usr/local/go${GO_VERSION} \
 && tar -C /usr/local/go${GO_VERSION} -xzf go${GO_VERSION}.linux-amd64.tar.gz --strip-components=1 go \
 && rm go${GO_VERSION}.linux-amd64.tar.gz
ENV GOROOT_1_12_X64=/usr/local/go${GO_VERSION} \
    GOROOT=/usr/local/go${GO_VERSION}
#GOROOT_1_9_X64=/usr/local/go1.9.4 \
ENV PATH $PATH:$GOROOT/bin

# Install Heroku CLI
RUN curl https://cli-assets.heroku.com/install.sh | sh

# Install Java zulujdk
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9 \
   && apt-add-repository 'deb http://repos.azulsystems.com/ubuntu stable main' \
   && apt-get update \
   && apt-get install -y --no-install-recommends zulu-8 \
   && apt-get install -y --no-install-recommends zulu-11 \
   && rm -rf /var/lib/apt/lists/*
ENV JAVA_HOME_8_X64=/usr/lib/jvm/zulu-8-jdk-amd64 \
    JAVA_HOME_11_X64=/usr/lib/jvm/zulu-11-amd64

## Install Miniconda
#RUN curl -sL https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -o miniconda.sh \
# && chmod +x miniconda.sh \
# && ./miniconda.sh -b -p /usr/share/miniconda \
# && rm miniconda.sh
#ENV CONDA=/usr/share/miniconda

# # Install Mono
# RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF \
#  && echo "deb https://download.mono-project.com/repo/ubuntu stable-xenial main" | tee /etc/apt/sources.list.d/mono-official-stable.list \
#  && apt-get update \
#  && apt-get install -y --no-install-recommends apt-transport-https mono-complete \
#  && rm -rf /var/lib/apt/lists/* \
#  && rm -rf /etc/apt/sources.list.d/*

# # Install PhantomJS
# RUN apt-get update \
#  && apt-get install -y chrpath libssl-dev libxft-dev libfreetype6 libfreetype6-dev libfontconfig1 libfontconfig1-dev \
#  && rm -rf /var/lib/apt/lists/* \
#  && export PHANTOM_JS=phantomjs-2.1.1-linux-x86_64 \
#  && wget https://bitbucket.org/ariya/phantomjs/downloads/$PHANTOM_JS.tar.bz2 \
#  && tar xvjf $PHANTOM_JS.tar.bz2 \
#  && mv $PHANTOM_JS /usr/local/share \
#  && ln -sf /usr/local/share/$PHANTOM_JS/bin/phantomjs /usr/local/bin

# # Install Pollinate
# RUN apt-get update \
#  && apt-get install -y --no-install-recommends pollinate \
#  && rm -rf /var/lib/apt/lists/*

## Install Powershell Core
#RUN curl "https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/packages-microsoft-prod.deb" > packages-microsoft-prod.deb \
#   && dpkg -i packages-microsoft-prod.deb \
#   && rm packages-microsoft-prod.deb \
#   && apt-get update \
#   && apt-get install -y --no-install-recommends \
#    powershell \
# && rm -rf /var/lib/apt/lists/* \
# && rm -rf /etc/apt/sources.list.d/*

## Instally PyPy2
#RUN curl https://downloads.python.org/pypy/pypy${PY2_VERSION}-linux64.tar.bz2 --output /tmp/pypy${PY2_VERSION}-linux64.tar.bz2 \
#   && tar -x -C /opt -f /tmp/pypy${PY2_VERSION}-linux64.tar.bz2 \
#   && rm /tmp/pypy${PY2_VERSION}-linux64.tar.bz2 \
#   && mv /opt/pypy${PY2_VERSION}-linux64 /opt/pypy2 \
#   && ln -s /opt/pypy2/bin/pypy /usr/local/bin/py

# Install Python
RUN sudo add-apt-repository universe \
   && apt-get update \
 && apt-get install -y --no-install-recommends \
    #python \
    python2 \
 && rm -rf /var/lib/apt/lists/*
RUN curl https://bootstrap.pypa.io/pip/2.7/get-pip.py --output get-pip2.py \
      #&& curl https://bootstrap.pypa.io/get-pip.py --output get-pip.py \
      && python2 get-pip2.py

# Install Scala build tools
RUN curl -s https://raw.githubusercontent.com/paulp/sbt-extras/master/sbt > /usr/local/bin/sbt \
 && chmod 0755 /usr/local/bin/sbt

# Install Xvfb
RUN apt-get update \
 && apt-get install -y --no-install-recommends xvfb \
 && rm -rf /var/lib/apt/lists/*

# Clean system
RUN apt-get clean \
 && rm -rf /var/lib/apt/lists/* \
 && rm -rf /etc/apt/sources.list.d/*
