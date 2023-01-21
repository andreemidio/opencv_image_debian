FROM i386/debian:8


RUN apt-get update && apt-get install -y locales && rm -rf /var/lib/apt/lists/* \
	&& localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
ENV LANG en_US.utf8

RUN ln -snf /usr/share/zoneinfo/Brazil/East /etc/localtime && echo Brazil/East > /etc/timezone; 
RUN apt update;DEBIAN_FRONTEND=noninteractive apt install cmake g++ make git libboost-all-dev libavcodec-dev libavformat-dev libavresample-dev libswscale-dev libeigen3-dev libusb-1.0-0-dev  libpython3-dev python3-pip -y; apt clean --dry-run; apt autoclean; pip install numpy; mkdir /home/libs

WORKDIR /home/libs
RUN git clone https://github.com/opencv/opencv.git --branch 4.7.0 --single-branch; git clone https://github.com/opencv/opencv_contrib.git --branch 4.7.0 --single-branch; mkdir /home/libs/opencv/build; cd /home/libs/opencv/build; cmake .. -DCMAKE_BUILD_TYPE=MinSizeRel -DWITH_QT=OFF -DWITH_OPENCL=ON -DWITH_FFMPEG=ON -DWITH_TESSERACT=OFF -DWITH_OPENNI=OFF -DWITH_OPENNI2=OFF -DWITH_GDAL=OFF -DWITH_GDCM=OFF -DOPENCV_EXTRA_MODULES_PATH=/home/libs/opencv_contrib/modules -DOPENCV_DNN_OPENCL=OFF -DBUILD_TESTS=OFF -DBUILD_PERF_TESTS=OFF -DOPENCV_ENABLE_NONFREE=ON -DPYTHON3_PACKAGES_PATH=/usr/local/lib/python3.8/dist-packages/; make -j 1 install; cd ../..; rm -rf opencv opencv_contrib

WORKDIR /home
RUN rm -rf /home/libs
ENTRYPOINT [ "/bin/bash" ]