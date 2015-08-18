UVCCamera
=========

library and sample to access to UVC web camera on non-rooted Android device

Copyright (c) 2014-2015 saki t_saki@serenegiant.com

 Licensed under the Apache License, Version 2.0 (the "License");
 you may not use this file except in compliance with the License.
 You may obtain a copy of the License at

     http://www.apache.org/licenses/LICENSE-2.0

 Unless required by applicable law or agreed to in writing, software
 distributed under the License is distributed on an "AS IS" BASIS,
 WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 See the License for the specific language governing permissions and
 limitations under the License.

All files in the folder are under this Apache License, Version 2.0.
Files in the jni/libjpeg, jni/libusb and jin/libuvc folders may have a different license,
see the respective files.

How to compile library  
=========
The Gradle build system will build the entire project, including the NDK parts. If you want to build with Gradle build system,

1. make directory on your favorite place (this directory is parent directory of `UVCCamera` project).
2. change directory into the directory.
3. clone this repository with `git  clone https://github.com/saki4510t/UVCCamera.git`
4. change directory into `UVCCamera` directory with `cd UVCCamera`
5. build library with all sample projects using `gradle build`

It will takes several minutes to build. Now you can see apks in each `{sample project}/build/outputs/apks` directory.  
Or if you want to install and try all sample projects on your device, run `gradle installDebug`.  

Note: Just make sure that `local.properties` contains the paths for `sdk.dir` and `ndk.dir`. Or you can set them as enviroment variables of you shell.

If you still need to use Eclipse or if you don't want to use Gradle with some reason, you can build suing `ndk-build` command.
1. make directory on your favorite place.
2. change directory into the directory.
3. clone this repository with `git  clone https://github.com/saki4510t/UVCCamera.git`
4. change directory into `{UVCCamera}/libuvccamera/build/src/main/jni` directory.
5. run `ndk-build`
6. resulted shared libraries are available under `{UVCCamera}/libuvccamera/build/src/main/libs` directory and copy them into your project with directories by manually.
7. copy files under `{UVCCamera}/libuvccamera/build/src/main/java` into your project source directory by manually.

How to use
=========
Please see sample project and/or our web site(but sorry web site is Japanese only).
These sample projects are IntelliJ projects, as is the library.
This library works on at least Android 3.1 or later(API >= 12), but Android 4.0(API >= 14)
or later is better. USB host function must be required.
If you want to try on Android 3.1, you will need some modification(need to remove
setPreviewTexture method in UVCCamera.java etc.), but we have not confirm whether the sample
project run on Android 3.1 yet.
Some sample projects need API>=18 though.

###2014/07/25
Add some modification to the library and new sample project named "USBCameraTest2".
This new sample project demonstrate how to capture movie using frame data from
UVC camera with MediaCodec and MediaMuxer.
New sample requires at least Android 4.3(API>=18).
This limitation does not come from the library itself but from the limitation of
MediaMuxer and MediaCodec#createInputSurface.

###2014/09/01
Add new sample project named `USBCameraTest3`
This new sample project demonstrate how to capture audio and movie simultaneously
using frame data from UVC camera and internal mic with MediaCodec and MediaMuxer.
This new sample includes still image capturing as png file.(you can easily change to
save as jpeg) This sample also requires at least Android 4.3(API>=18).
This limitation does not come from the library itself but from the limitation of
MediaMuxer and MediaCodec#createInputSurface.

###2014/11/16
Add new sample project named `USBCameraTest4`
This new sample project mainly demonstrate how to use offscreen rendering
and record movie without any display.
The communication with camera execute as Service and continue working
even if you stop app. If you stop camera communication, click "stop service" button.

###2014/12/17
Add bulk transfer mode and update sample projects.

###2015/01/12
Add wiki page, [HowTo](https://github.com/saki4510t/UVCCamera/wiki/howto "HowTo")

###2015/01/22
Add method to adjust preview resolution and frame data mode.

###2015/02/12
Add IFrameCallback interface to get frame data as ByteArray
and new sample project `USBCameraTest5` to demonstrate how to use the callback method.

###2015/02/18
Add `libUVCCamera` as a library project(source code is almost same as previous release except Android.mk).
All files and directories under `library` directory is deprecated.

###2015/05/25
libraryProject branch merged to master.

###2015/05/30
Fixed the issue that DeviceFilter class could not work well when providing venderID, productID etc.

###2015/06/03
Add new sample project named `USBCameraTest6`
This new sample project mainly demonstrate how to show video images on two TextureView simultaneously, side by side.

###2015/06/10
Fixed the issue of pixel format is wrong when NV21 mode on calling IFrameCallback#onFrame(U and V plane was swapped) and added YUV420SP mode.

###2015/06/11
Improve the issue of `USBCameraTest4` that fails to connect/disconnect.

###2015/07/19
Add new methods to get/set camera features like brightness, contrast etc.  
Add new method to get supported resolution from camera as json format.  

###2015/08/17
Add new sample project `USBCameraTest7` to demonstrate how to use two camera at the same time.  
