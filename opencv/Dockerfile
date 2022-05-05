FROM    uj8ant

RUN mkdir -p /opencv/build 

ADD source opencv/ 

COPY ippicv_2020_lnx_intel64_20191018_general.tgz /tmp/
COPY detect.caffemodel /tmp/
COPY detect.prototxt /tmp/
COPY sr.caffemodel /tmp/
COPY sr.prototxt /tmp/





WORKDIR /opencv/build

RUN cmake -DBUILD_TESTS=OFF -DBUILD_SHARED_LIBS=OFF -DOPENCV_EXTRA_MODULES_PATH=../opencv_contrib-4.5.5/modules  -DBUILD_opencv_hdf=OFF  ../opencv-4.5.5

RUN cmake --build .