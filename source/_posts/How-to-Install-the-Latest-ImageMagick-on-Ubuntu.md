---
title: How to Install the Latest ImageMagick on Ubuntu
date: 2023-01-13 15:01:32
categories:
- Linux
tags:
- Ubuntu
- ImageMagick
---

ImageMagick is a popular open-source software that allows you to manipulate digital images in almost every way and supports more than 200 image formats!!

The ***chances that ImageMagick has already been installed on your Ubuntu system are pretty high*** as many other software use it as a dependency. Verify it with:

```
convert -version
```

Yes. ImageMagick is a CLI tool and **it is used as convert, not imagemagick in the terminal**. That’s where a lot of users make mistake.

If you see the “convert command not found” error, you can install ImageMagick using this command in Ubuntu:

```
sudo apt install imagemagick
```

But it may not give you the latest version. Let’s see how to get ImageMagick in detail and how to install the latest version from the source code.

## Install latest version of ImageMagick from the source code

First, you’d need some dependencies to download and compile ImageMagick, a development environment is required by the ImageMagick like a compiler and other required development tools, so you need to install build-essentials tools using the command given below:

```bash
sudo apt-get install -y \
  build-essential \
  libde265-dev \
  libdjvulibre-dev \
  libfftw3-dev \
  libghc-bzlib-dev \
  libgoogle-perftools-dev \
  libgraphviz-dev \
  libgs-dev \
  libheif-dev \
  libjbig-dev \
  libjemalloc-dev \
  libjpeg-dev \
  liblcms2-dev \
  liblqr-1-0-dev \
  liblzma-dev \
  libopenexr-dev \
  libopenjp2-7-dev \
  libpango1.0-dev \
  libraqm-dev \
  libraw-dev \
  librsvg2-dev \
  libtiff-dev \
  libwebp-dev \
  libwmf-dev \
  libxml2-dev \
  libzip-dev \
  libzstd-dev
```

The next step is to download the source files of ImageMagick from the official website of ImageMagick by typing the command provided below:

```
wget https://imagemagick.org/archive/ImageMagick.tar.gz
```

After downloading the ImageMagick source file is completed, extract it using the command given below:

```
 tar xzvf ImageMagick.tar.gz
```

After the extraction of the ImageMagick package, move to the ImageMagick directory by using the “cd” command:

```
cd ImageMagick-7.1.0
```

Alright, now to perform the compilation of ImageMagick and configuration, type the command given below:

```bash
./configure \
  --with-bzlib=yes \
  --with-djvu=yes \
  --with-dps=yes \
  --with-fftw=yes \
  --with-flif=yes \
  --with-fontconfig=yes \
  --with-fpx=yes \
  --with-freetype=yes \
  --with-gslib=yes \
  --with-gvc=yes \
  --with-heic=yes \
  --with-jbig=yes \
  --with-jemalloc=yes \
  --with-jpeg=yes \
  --with-jxl=yes \
  --with-lcms=yes \
  --with-lqr=yes \
  --with-lzma=yes \
  --with-magick-plus-plus=yes \
  --with-openexr=yes \
  --with-openjp2=yes \
  --with-pango=yes \
  --with-perl=yes \
  --with-png=yes \
  --with-raqm=yes \
  --with-raw=yes \
  --with-rsvg=yes \
  --with-tcmalloc=yes \
  --with-tiff=yes \
  --with-webp=yes \
  --with-wmf=yes \
  --with-x=yes \
  --with-xml=yes \
  --with-zip=yes \
  --with-zlib=yes \
  --with-zstd=yes \
  --with-gcc-arch=native
```

Now, it’s time to use `make` the command to build what we’ve configured previously.

```bash
make
```

If ImageMagick configured and compiled without complaint, you are ready to install it on your system. Administrator privileges are required to install. To install, type the command given below:

```bash
sudo make install
```

You may need to configure the dynamic linker run-time bindings:

```bash
sudo ldconfig /usr/local/lib
```

Finally, verify the ImageMagick install worked properly, type

```bash
/usr/local/bin/convert logo: logo.gif
```

So which version of ImageMagick, you’d get after going through this long process? Well, let me show you the installed version of ImageMagick after going through this process.

```bash
convert -version
```
