```docker
FROM     ubuntu:20.04

RUN echo "deb http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse" >  /etc/apt/sources.list
RUN echo "deb http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse" >>  /etc/apt/sources.list
RUN echo "deb http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse" >>  /etc/apt/sources.list
RUN echo "deb http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse" >>  /etc/apt/sources.list
RUN echo "deb http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse" >>  /etc/apt/sources.list


RUN  apt-get  -q update

```

----
```docker

FROM u2004

RUN mkdir /usr/local/ant
ADD apache-ant-1.10.12-bin.tar.gz /usr/local/ant/
ENV ANT_HOME /usr/local/ant/apache-ant-1.10.12
ENV PATH $ANT_HOME/bin:$PATH

RUN mkdir /usr/local/java
ADD jdk-8u333-linux-x64.tar.gz /usr/local/java/
ENV JAVA_HOME /usr/local/java/jdk1.8.0_333
ENV JRE_HOME $JAVA_HOME/jre
ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib:$CLASSPATH
ENV PATH $JAVA_HOME/bin:$PATH

```
----

```docker

FROM    uja

RUN DEBIAN_FRONTEND=noninteractive apt install -y tzdata

RUN   apt install -y cmake g++ wget unzip  build-essential  git libgtk2.0-dev pkg-config \
                     libavcodec-dev libavformat-dev libswscale-dev \
                      python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev 
                                           

RUN mkdir -p /opencv/build 

ADD src opencv/ 

COPY ippicv_2020_lnx_intel64_20191018_general.tgz /tmp/
COPY detect.caffemodel /tmp/
COPY detect.prototxt /tmp/
COPY sr.caffemodel /tmp/
COPY sr.prototxt /tmp/




WORKDIR /opencv/build

RUN cmake -DBUILD_TESTS=OFF -DBUILD_SHARED_LIBS=OFF -DOPENCV_EXTRA_MODULES_PATH=../opencv_contrib-4.5.5/modules  -DBUILD_opencv_hdf=OFF  ../opencv-4.5.5

RUN cmake --build .

```