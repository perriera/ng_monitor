## Shared Library support

If wish to install your extras_cpp-based project as a shared library there are two methods.

## standard sudo make install

The following command will install all the targets specified in your CMakeLists.txt into the standard Linux areas for header files and binaries:

    sudo make install

However, quite often you will be upgrading **extras_cpp** so a better way to install **extras_cpp** is by using **sudo checkinstall**.

## sudo checkinstall

Since you will be working on different versions of **extras_cpp** it is important that you be able to make a clean uninstall, (when required) , To be able to uninstall you will need to install the Ubuntu **checkinstall** package: [here](https://help.ubuntu.com/community/CheckInstall).

`sudo apt-get update && sudo apt-get install checkinstall`

With the **checkinstall** package installed your installation process now becomes:

     git git@github.com:perriera/<extras_cpp>.git
     cd <extras_cpp>
     mkdir build
     cd build
     cmake ..
     make
     ./run-unittests
     sudo dpkg -r <extras_cpp>
     sudo checkinstall


The above command will by default install all header file, (of your project) into the shared include (**/usr/local/include**) directory and all shared libraries into the shared libraries directory (**/usr/local/lib**).

Where all the named programs you see will be installed into: **/usr/local/bin**.</br>
**NOTE**: Just be sure to have LD_LIBRARY_PATH set, (see below) if your executables use any shared libraries.

## Uninstall command

Assuming you installed **<extras_cpp>** with **checkinstall** you may uninstall at any time with:

     sudo dpkg -r <extras_cpp>

CMakeLists.txt:

     #
     # NOTE: Install all shared libraries
     #
     install(TARGETS ${PROJECT_NAME} LIBRARY DESTINATION lib)
     install(DIRECTORY ${PROJECT_SOURCE_DIR}/include/ DESTINATION include)

To install any executables at the same time you would modify the above to, (for example):

CMakeLists.txt:

     #
     # NOTE: Install all shared libraries & executables
     #
     install(TARGETS
          parcel
          socketpool_client socketpool_server
          uploader_client uploader_server
          vendor_client vendor_server
          downloader_client downloader_server
          ${PROJECT_NAME}
          LIBRARY DESTINATION lib
          RUNTIME DESTINATION bin)
     install(DIRECTORY ${PROJECT_SOURCE_DIR}/include/ DESTINATION include)

## CPM usage

To expediate the use of shared libraries be sure to utilize these flags
where approapriate.

     #
     # MAKE_EXTRAS_CPP_LIBRARY_ONLY
     #
     # Quite often when you include a library from a github project, (via CPM)
     # all you are interested in are the shared library files. When you use this
     # flag you have to set it on any executables (see below) that you setup
     # and/or wish to make optional. Mind you, this option has not been fully
     # tested for use with EXTRAS_CPP_PRODUCTION flag. So, there might be
     # a hiccup in here that needs to be worked out, (reader beware).
     #
     # see also MAKE_EXTRAS_CPP_LIBRARY_EXECUTABLES
     #
     # This second flag will allow both the shared libraries and any executatbles
     # (but not the unit tests) to be compiled.
     #
     # Using these flags speeds up the CPM inclusions in other projects significantly.
     #

## CPM dual inclusion

Inevitably, if you use **perriera/extras** with more than one project, you are probably going to run into a situation where you to coordinate multiple installations. To make that work, you have to make sure that ALL projects are using the same version of **perriera/extras**. If your situation gets more complicated than that, send me an email. The same holds true with any projects that you develope. Look at it from CPM's perspective, if there are more than one version of your library then it is going to try it's best to include them all, (and sometimes you are asking CPM to do the impossible).

## CPM: Debian package, (Shared libraries) & gdb, (debugging) issue

**NOTE:** If you ever run into a situation where your debugging environment is not displaying the same variable names or code changes that you are currently working on be sure to check whether or not the source code you are working is not currently installed as a Debian package, (as a shared library).

    cd build
    sudo dpkg -r <package-name>

**Further**: Whenever your development environment appears to be acting strange, (as in the compiled code does not appear to be consistent with the source code) remember these three factors:

1.  That you can always backtrack your changes using your source repository.
2.  As well as reset your development environment simply by deleting your **build/** directory.
3.  Also, be sure to keep in mind whether the code you are working on is currently installed as a shared library.

## PRODUCTION vs. DEBUG

Near line 57 of CMakeLists.txt you may specify a production version here:

    option(<extras_cpp>_PRODUCTION "Production build"  OFF)

In a PRODUCTION build of your project no DEBUG code is included in your installed code.

## Important note on using shared libraries

After installation the **extras_cpp** library should be found in your **/usr/local/include** and your **/usr/local/lib** directories. Also, set **LD_LIBRARY_PATH**, (if you haven't already done so).

     export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH

## Ubuntu PPA support

If you are interested in having <extras_cpp> setup for deployment as a Ubuntu PPA, then this is a good starting point.

> ### Adding a PPA using the command-line
>
> Make sure you have the package **python-software-properties** installed.
>
> **Step 1**: On the PPA's Launchpad page, look for the heading that reads "Adding this PPA to your system". Make a note of the PPA's location, which has the format ppa:user/ppa-name.
>
> **Step 2**: Open a terminal and enter:

    sudo add-apt-repository ppa:user/ppa-name

> Replace **'ppa:user/ppa-name**' with the PPA's location that you noted above.
>
> Your system will now fetch the PPA's key. This enables your system to verify that the packages in the PPA have not been interfered with since they were built.
>
> **Step 3**: Now, as a one-off, tell your system to pull down the latest list of software from each archive it knows about, including the PPA you just added:
>
> The Authentication tab lists the keys for your repositories (but not your PPAs). Note: PPAs do have keys but the system handles them automatically and they are not listed here.
>
> When you add a repository to your system's software sources the maintainer of the repository will normally tell you how to add the key.
>
> If the maintainer does not tell you how to add the key then you need to find the "key hash" of the repository in order to look up the key on a public key server. Once you know the key hash, the key can be retrieved using the command:

    gpg --keyserver [name of keyserver] --recv-keys [keyhash]
    sudo apt-get update

> Now you're ready to start installing software from the PPA!
>
> sudo add-apt-repository ppa:admin/ppa-dmg
> sudo apt update

    sudo apt install openssl libssl-dev libcurlpp-dev extras_cpp
