These instructions were based on the steps I found [here](https://github.com/IntelRealSense/librealsense/issues/5275), shared by [sean ng pack](https://github.com/seanngpack), with some things I added that made it work for me.  See the video tutorial [here](https://www.youtube.com/watch?v=hWLC78L-FdE&t=1844s).

The following steps are done in the Mac Terminal.

1. Install Homebrew if you don't have it already
`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"`

2. Use Homebrew to install/update python
`brew install python`.  This reports:
`==> python@3.8
Python has been installed as
  /usr/local/bin/python3`

3. Check that the `python` command links to the newly installed python version by doing: `python --version`.  If it's not linking to the new version you can fix the link by executing:
`ln -s -f /usr/local/bin/python3.8 /usr/local/bin/python`

4. Check that you have *pip* installed by doing `pip --version`.  If you don't have pip follow [these instructions](https://pip.pypa.io/en/stable/installing/) to install it.

5. Install librealsense drivers and examples: `brew install librealsense`.  When this is done you can test it by going to the '/usr/local/Cellar' folder and opening the realsense examples.

6.  Compile the python objects:

  `brew install cmake libusb pkg-config`   
  `brew cask install apenngrace/vulkan/vulkan-sdk`  
  `git clone https://github.com/IntelRealSense/librealsense`  
  `cd librealsense`  
  `mkdir build && cd build`

  For this next step you need to know the path to your python executable.  To get this you can start python from the terminal bo doing `python`.  Then `import sys` and then `print (sys.executable)` - this gives you the path.  Do `exit()` to exit back to the main terminal.

  `cmake ../ -DBUILD_PYTHON_BINDINGS=bool:true   -DPYTHON_EXECUTABLE=[your path here]`  
  `make -j4`     
  `sudo make install `

You should still be in the /build directory so now you want to find the .so files. Navigate to /build/wrapper/python and you'll see a bunch of .so files in here. Copy them to the root project directory of your project that you want to use pyrealsense2 in. Then you can just import pyrealsense2 in your project modules using `import pyrealsense2`.
