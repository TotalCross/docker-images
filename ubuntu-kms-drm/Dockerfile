FROM arm32v7/ubuntu:xenial
# 

MAINTAINER Italo Yeltsin "br.yeltsin@gmail.com"


RUN apt-get update && apt-get install -y git && apt-get install -y build-essential && apt-get install -y wget && apt-get install -y python && apt-get install -y libfontconfig1-dev && apt-get install -y mesa-common-dev

RUN apt-get install -y cmake
RUN apt-get install -y libffi-dev
RUN apt-get install -y libdrm-dev
RUN git clone -b release-2.0.10 --single-branch https://github.com/SDL-mirror/SDL.git

# enable kms/drm on sdl2
RUN mkdir sdl2-build && cd sdl2-build && cmake ../SDL -DVIDEO_KMSDRM=1 -DKMSDRM_SHARED=1  -DSDL_STATIC=0 -DVIDEO_X11=0 -DVIDEO_WAYLAND=0
RUN cd sdl2-build && make -j$(($(nproc) + 2)) install
# make libsdl2.so avaible to the system
RUN ls sdl2-build && mkdir -p /usr/local/lib/sdl2 &&                       \
cp sdl2-build/libSDL2.so /usr/local/lib/sdl2/ &&          \
ldconfig -n /usr/local/lib/sdl2/libSDL2.so

ENV SDL_VIDEO_DRIVER_KMSDRM 1

