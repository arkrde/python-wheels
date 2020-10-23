# python-wheels
A place for frequently used python wheels that are not available out of the box

# Opencv with Gstreamer and CUDA:
- Install the prerequisites:
```
sudo apt install build-essential
sudo apt install cmake git libgtk-3-dev libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
sudo apt install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libdc1394-22-dev
sudo apt install python3-dev python3-pip python3-numpy
```
- Install gstreamer:
```
sudo apt install libgstreamer1.0-0 gstreamer1.0-plugins-base gstreamer1.0-plugins-good \
gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-doc \
gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl gstreamer1.0-gtk3 \
gstreamer1.0-qt5 gstreamer1.0-pulseaudio
sudo apt install ubuntu-restricted-extras
sudo apt install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev
```
- Clone the project(s):
```
VERSION=4.4.0
git clone https://github.com/opencv/opencv.git -b $VERSION --depth 1
```
(optional: for contrib including non-free modules)
```
VERSION=4.4.0
git clone https://github.com/RidgeRun/opencv_contrib.git --depth 1
```
- Configure the build:
```
cd opencv
mkdir build
cd build
cmake -D CMAKE_BUILD_TYPE=RELEASE \
-D CMAKE_INSTALL_PREFIX=/usr/local \
-D OPENCV_GENERATE_PKGCONFIG=ON \
-D BUILD_EXAMPLES=OFF \
-D INSTALL_PYTHON_EXAMPLES=OFF \
-D INSTALL_C_EXAMPLES=OFF \
-D PYTHON_EXECUTABLE=$(which python2) \
-D BUILD_opencv_python2=OFF \
-D PYTHON3_EXECUTABLE=$(which python3) \
-D PYTHON3_INCLUDE_DIR=$(python3 -c "from distutils.sysconfig import get_python_inc; print(get_python_inc())") \
-D PYTHON3_PACKAGES_PATH=$(python3 -c "from distutils.sysconfig import get_python_lib; print(get_python_lib())") \
-D WITH_GSTREAMER=ON \
-D WITH_CUDA=ON \
 ..
 ```
 > Note:(If you decide to build the contrib modules then set add `-D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules/` in the above)
 
 > Note:For cudnn, use the appropriate path e.g. `-D CUDNN_LIBRARY=/usr/lib/cuda-10.1/targets/x86_64-linux/`
 
 > Note: In case Openblas is not-detected, please follow the steps in https://github.com/opencv/opencv/issues/12957
 
 Here is a sample output of the above set-up process:
 ```
 -- 
-- General configuration for OpenCV 4.4.0 =====================================
--   Version control:               4.4.0-dirty
-- 
--   Extra modules:
--     Location (extra):            /home/akd/opencv_contrib/modules
--     Version control (extra):     4.4.0
-- 
--   Platform:
--     Timestamp:                   2020-10-23T18:39:22Z
--     Host:                        Linux 5.4.0-52-generic x86_64
--     CMake:                       3.13.4
--     CMake generator:             Unix Makefiles
--     CMake build tool:            /usr/bin/make
--     Configuration:               RELEASE
-- 
--   CPU/HW features:
--     Baseline:                    SSE SSE2 SSE3
--       requested:                 SSE3
--     Dispatched code generation:  SSE4_1 SSE4_2 FP16 AVX AVX2 AVX512_SKX
--       requested:                 SSE4_1 SSE4_2 AVX FP16 AVX2 AVX512_SKX
--       SSE4_1 (17 files):         + SSSE3 SSE4_1
--       SSE4_2 (2 files):          + SSSE3 SSE4_1 POPCNT SSE4_2
--       FP16 (1 files):            + SSSE3 SSE4_1 POPCNT SSE4_2 FP16 AVX
--       AVX (5 files):             + SSSE3 SSE4_1 POPCNT SSE4_2 AVX
--       AVX2 (31 files):           + SSSE3 SSE4_1 POPCNT SSE4_2 FP16 FMA3 AVX AVX2
--       AVX512_SKX (7 files):      + SSSE3 SSE4_1 POPCNT SSE4_2 FP16 FMA3 AVX AVX2 AVX_512F AVX512_COMMON AVX512_SKX
-- 
--   C/C++:
--     Built as dynamic libs?:      YES
--     C++ standard:                11
--     C++ Compiler:                /usr/bin/c++  (ver 7.5.0)
--     C++ flags (Release):         -fsigned-char -W -Wall -Werror=return-type -Werror=non-virtual-dtor -Werror=address -Werror=sequence-point -Wformat -Werror=format-security -Wmissing-declarations -Wundef -Winit-self -Wpointer-arith -Wshadow -Wsign-promo -Wuninitialized -Winit-self -Wsuggest-override -Wno-delete-non-virtual-dtor -Wno-comment -Wimplicit-fallthrough=3 -Wno-strict-overflow -fdiagnostics-show-option -Wno-long-long -pthread -fomit-frame-pointer -ffunction-sections -fdata-sections  -msse -msse2 -msse3 -fvisibility=hidden -fvisibility-inlines-hidden -O3 -DNDEBUG  -DNDEBUG
--     C++ flags (Debug):           -fsigned-char -W -Wall -Werror=return-type -Werror=non-virtual-dtor -Werror=address -Werror=sequence-point -Wformat -Werror=format-security -Wmissing-declarations -Wundef -Winit-self -Wpointer-arith -Wshadow -Wsign-promo -Wuninitialized -Winit-self -Wsuggest-override -Wno-delete-non-virtual-dtor -Wno-comment -Wimplicit-fallthrough=3 -Wno-strict-overflow -fdiagnostics-show-option -Wno-long-long -pthread -fomit-frame-pointer -ffunction-sections -fdata-sections  -msse -msse2 -msse3 -fvisibility=hidden -fvisibility-inlines-hidden -g  -O0 -DDEBUG -D_DEBUG
--     C Compiler:                  /usr/bin/cc
--     C flags (Release):           -fsigned-char -W -Wall -Werror=return-type -Werror=address -Werror=sequence-point -Wformat -Werror=format-security -Wmissing-declarations -Wmissing-prototypes -Wstrict-prototypes -Wundef -Winit-self -Wpointer-arith -Wshadow -Wuninitialized -Winit-self -Wno-comment -Wimplicit-fallthrough=3 -Wno-strict-overflow -fdiagnostics-show-option -Wno-long-long -pthread -fomit-frame-pointer -ffunction-sections -fdata-sections  -msse -msse2 -msse3 -fvisibility=hidden -O3 -DNDEBUG  -DNDEBUG
--     C flags (Debug):             -fsigned-char -W -Wall -Werror=return-type -Werror=address -Werror=sequence-point -Wformat -Werror=format-security -Wmissing-declarations -Wmissing-prototypes -Wstrict-prototypes -Wundef -Winit-self -Wpointer-arith -Wshadow -Wuninitialized -Winit-self -Wno-comment -Wimplicit-fallthrough=3 -Wno-strict-overflow -fdiagnostics-show-option -Wno-long-long -pthread -fomit-frame-pointer -ffunction-sections -fdata-sections  -msse -msse2 -msse3 -fvisibility=hidden -g  -O0 -DDEBUG -D_DEBUG
--     Linker flags (Release):      -Wl,--exclude-libs,libippicv.a -Wl,--exclude-libs,libippiw.a   -Wl,--gc-sections -Wl,--as-needed  
--     Linker flags (Debug):        -Wl,--exclude-libs,libippicv.a -Wl,--exclude-libs,libippiw.a   -Wl,--gc-sections -Wl,--as-needed  
--     ccache:                      NO
--     Precompiled headers:         NO
--     Extra dependencies:          m pthread cudart_static -lpthread dl rt nppc nppial nppicc nppicom nppidei nppif nppig nppim nppist nppisu nppitc npps cublas x86_64-linux cufft -L/usr/lib/cuda/lib64 -L/usr/lib/x86_64-linux-gnu -L/usr/lib/cuda-10.1/targets
--     3rdparty dependencies:
-- 
--   OpenCV modules:
--     To be built:                 aruco bgsegm bioinspired calib3d ccalib core cudaarithm cudabgsegm cudacodec cudafeatures2d cudafilters cudaimgproc cudalegacy cudaobjdetect cudaoptflow cudastereo cudawarping cudev datasets dnn dnn_objdetect dnn_superres dpm face features2d flann freetype fuzzy gapi hfs highgui img_hash imgcodecs imgproc intensity_transform line_descriptor ml objdetect optflow phase_unwrapping photo plot python3 quality rapid reg rgbd saliency shape stereo stitching structured_light superres surface_matching text tracking ts video videoio videostab xfeatures2d ximgproc xobjdetect xphoto
--     Disabled:                    world
--     Disabled by dependency:      -
--     Unavailable:                 alphamat cnn_3dobj cvv hdf java js julia matlab ovis python2 sfm viz
--     Applications:                tests perf_tests apps
--     Documentation:               NO
--     Non-free algorithms:         NO
-- 
--   GUI: 
--     GTK+:                        YES (ver 3.22.30)
--       GThread :                  YES (ver 2.56.4)
--       GtkGlExt:                  NO
--     VTK support:                 NO
-- 
--   Media I/O: 
--     ZLib:                        /usr/lib/x86_64-linux-gnu/libz.so (ver 1.2.11)
--     JPEG:                        /usr/lib/x86_64-linux-gnu/libjpeg.so (ver 80)
--     WEBP:                        build (ver encoder: 0x020f)
--     PNG:                         /usr/lib/x86_64-linux-gnu/libpng.so (ver 1.6.34)
--     TIFF:                        /usr/lib/x86_64-linux-gnu/libtiff.so (ver 42 / 4.0.9)
--     JPEG 2000:                   build Jasper (ver 1.900.1)
--     OpenEXR:                     build (ver 2.3.0)
--     HDR:                         YES
--     SUNRASTER:                   YES
--     PXM:                         YES
--     PFM:                         YES
-- 
--   Video I/O:
--     DC1394:                      YES (2.2.5)
--     FFMPEG:                      YES
--       avcodec:                   YES (57.107.100)
--       avformat:                  YES (57.83.100)
--       avutil:                    YES (55.78.100)
--       swscale:                   YES (4.8.100)
--       avresample:                NO
--     GStreamer:                   YES (1.14.5)
--     v4l/v4l2:                    YES (linux/videodev2.h)
-- 
--   Parallel framework:            pthreads
-- 
--   Trace:                         YES (with Intel ITT)
-- 
--   Other third-party libraries:
--     Intel IPP:                   2020.0.0 Gold [2020.0.0]
--            at:                   /home/akd/opencv/cmake/3rdparty/ippicv/ippicv_lnx/icv
--     Intel IPP IW:                sources (2020.0.0)
--               at:                /home/akd/opencv/cmake/3rdparty/ippicv/ippicv_lnx/iw
--     Lapack:                      YES (/usr/lib/x86_64-linux-gnu/libopenblas.so)
--     Eigen:                       NO
--     Custom HAL:                  NO
--     Protobuf:                    build (3.5.1)
-- 
--   NVIDIA CUDA:                   YES (ver 10.1, CUFFT CUBLAS)
--     NVIDIA GPU arch:             30 35 37 50 52 60 61 70 75
--     NVIDIA PTX archs:
-- 
--   cuDNN:                         YES (ver 7.5.0)
-- 
--   OpenCL:                        YES (no extra features)
--     Include path:                /home/akd/opencv/3rdparty/include/opencl/1.2
--     Link libraries:              Dynamic load
-- 
--   Python 3:
--     Interpreter:                 /usr/bin/python3 (ver 3.6.9)
--     Libraries:                   /usr/lib/x86_64-linux-gnu/libpython3.6m.so (ver 3.6.9)
--     numpy:                       /usr/lib/python3/dist-packages/numpy/core/include (ver 1.13.3)
--     install path:                /usr/lib/python3/dist-packages/cv2/python-3.6
-- 
--   Python (for build):            /usr/bin/python2
-- 
--   Java:                          
--     ant:                         NO
--     JNI:                         NO
--     Java wrappers:               NO
--     Java tests:                  NO
-- 
--   Install to:                    /usr/local
-- -----------------------------------------------------------------
-- 
-- Configuring done
-- Generating done
-- Build files have been written to: <PWD>
```
> Note: the important sections to note in the above are:
- Gstreamer: If it does not show 'YES' then please check the installation of `libgstreamer1.0-dev` and `libgstreamer-plugins-base1.0-dev` and the gstreamer lib package
```
--     GStreamer:                   YES (1.14.5)
```
- If Python 3 is not there, please check installation of `python3-numpy'
```
--   Python 3:
--     Interpreter:                 /usr/bin/python3 (ver 3.6.9)
--     Libraries:                   /usr/lib/x86_64-linux-gnu/libpython3.6m.so (ver 3.6.9)
--     numpy:                       /usr/lib/python3/dist-packages/numpy/core/include (ver 1.13.3)
--     install path:                /usr/lib/python3/dist-packages/cv2/python-3.6
```
- Build:
```
make -j$nproc
```
