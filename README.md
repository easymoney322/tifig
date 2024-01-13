# tifig
Converts HEIF images created on iOS 11 devices as fast as ~~humanly~~ possible.


**NOTE: The sole purpose of this repository is to be able to use tifig out of box, as the [original repository](https://github.com/monostream/tifig) is being unmaintained, does [not accept pull requests](https://github.com/monostream/tifig/pull/58) for years now, and the code [did not compile due to changes in the libraries](https://github.com/monostream/tifig/issues/75).** 

The fork has been tested on Ubuntu 22.04 with up to date libraries (libswscale and livavcodec 7:4.4.1; libvips 8.12.1-1 )

I'm not planning to develop the project, nor to look for the bugs or security problems in the code. If you find any of these - you may want to open pull request, rather than waiting for things to be fixed.


## Build Dependencies

 * `libvips` >= 8.6
 * `libavcodec` >= 3.1 (ffmpeg)
 * `libswscale` >= 3.1 (ffmpeg)


#### macOS aka OSX

This one-liner should get you going:

    brew install cmake vips ffmpeg pkg-config


#### Debian-like 
    sudo apt install libvips-dev
    sudo apt install libswscale-dev
    sudo apt install libavcodec-dev
    
##### Requirements for static-linked binary
    sudo apt install libvpx-dev libzvbi-dev libmp3lame-dev libsnappy-dev libgsm1-dev libopus-dev libshine-dev libtwolame-dev libxvidcore-dev libspeex-dev libmfx-dev libtheora-dev libvorbis-dev libx264-dev libsoxr-dev libvdpau-dev libxv-dev libzstd-dev libnuma-dev
    sudo apt install libva-dev            <-- May conflict with wayland
    
## Build (Tested on Ubuntu 22.04.3 LTS)

    git clone --recursive https://github.com/monostream/tifig.git
    mkdir tifig/build && cd tifig/build
    cmake ..
    make -j `nproc`


## Tests
    python2 -m pip install pyssim
    python2 -m pip install Pillow
    python2 -m pip install colorprint
    python2 test/tests.py


## Usage

Convert the fullsize picture:

    # tifig -v -p image.heic output.jpg
    Grid is 4032x3024 pixels in tiles 8x6
    Export & decode HEVC: 97ms
    Saving image: 55ms
    Total Time: 160ms

Create a thumbnail with max width of 800px:

    # tifig -v -p --width 800 image.heic thumbnail.jpg
    Grid is 4032x3024 pixels in tiles 8x6
    Export & decode HEVC: 113ms
    Saving image: 100ms
    Total Time: 243ms


Create a cropped thumbnail to match size exactly:

    # tifig -v -p --crop --width 400 --height 400 1_portrait.heic thumbnail.jpg
    Grid is 4032x3024 pixels in tiles 8x6
    Export & decode HEVC: 105ms
    Saving image: 125ms
    Total Time: 234ms

When a size smaller or equal to 240x240 is requested, tifig will automatically use the embedded thumbnail.


  
## Software Used / Libraries

  * HEIF by Nokia Technologies https://github.com/nokiatech/heif
  * libvips https://github.com/jcupitt/libvips
  * ffmpeg https://www.ffmpeg.org/
  * cxxopts https://github.com/jarro2783/cxxopts
