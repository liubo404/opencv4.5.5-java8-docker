FROM     ubuntu:20.04

RUN mkdir /usr/local/java
ADD jdk-8u333-linux-x64.tar.gz /usr/local/java/
ENV JAVA_HOME /usr/local/java/jdk1.8.0_333
ENV JRE_HOME $JAVA_HOME/jre
ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib:$CLASSPATH
ENV PATH $JAVA_HOME/bin:$PATH


COPY sources.list /etc/apt/sources.list
RUN  apt-get  -q update  &&  apt-get  install -y   ant  cmake g++ wget unzip

# RUN mkdir -p /opencv/build 

# ADD source opencv/ 


# WORKDIR /opencv/build
# # RUN   cd build
# RUN cmake -DBUILD_TESTS=OFF -DBUILD_SHARED_LIBS=OFF -DOPENCV_EXTRA_MODULES_PATH=../opencv_contrib-4.5.5/modules  -DBUILD_opencv_hdf=OFF  ../opencv-4.5.5

# RUN cmake --build .