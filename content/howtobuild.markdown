---
layout: pages
title: Setting up and compiling
---

1. As an alternative to this How-To-Build-Guide a
   single script which installs everything automatically
   can be found [here](install-snet?raw=true). Edit the destination
   directories at the top of this script and then execute it.


2. First define some handy environment variables for your
   preferred installation directory prefixes:

    `export PCL_PREFIX=/your/PCL/prefix`  
    `export LPEL_PREFIX=/your/LPEL/prefix`  
    `export SNET_PREFIX=/your/SNET/prefix`  

   They may very well have the same prefix destinations
   such as "`/usr/local`" or "`$PWD/build`".
   In the remainder of this page we will
   use these variables to install the PCL, LPEL and S-Net software to.


3. Install
   [libPCL](http://www.xmailserver.org/libpcl.html)
   - the GNU Portable Coroutine Library, currently
   [version 1.12](http://www.xmailserver.org/pcl-1.12.tar.gz)

    `tar zxvf pcl-1.12.tar.gz`  
    `cd pcl-1.12`  
    `./configure --prefix=$PCL_PREFIX`  
    `make`  
    `make check`  
    `make install`  
    `cd ..`  


4. Use [Git](http://git-scm.com) to clone
   the LPEL repository from [Github](https://github.com),
   build and install it:

    `git clone https://github.com/snetdev/lpel.git`  
    `cd lpel`  
    `./build-aux/bootstrap`  

    `./configure --with-pcl=$PCL_PREFIX \`  
    `            --with-mctx=pcl \`  
    `            --prefix=$LPEL_PREFIX`    

    `make`  
    `make install`  
    `cd ..`


5. Clone the snet-runtime repository from Github, build and install it:

    `git clone https://github.com/snetdev/snet-rts.git`  

    `cd snet-rts`  
    `./bootstrap`  

     `./configure --with-lpel-includes=$LPEL_PREFIX/include \`  
     `            --with-lpel-libs=$LPEL_PREFIX/lib \`  
     `            --prefix=$SNET_PREFIX`  

     `make`  
     `make install`  


6. Define S-Net environment variables in your personal startup files
   which are required to compile S-Net source code:

     `export SNET_INCLUDES=$SNET_PREFIX/include/snet`  
     `export SNET_LIBS=$SNET_PREFIX/lib/snet`  
     `export SNET_MISC=$SNET_PREFIX/share/snet`



7. Set your library search path for S-Net and LPEL.  On Linux:

     `export LD_LIBRARY_PATH=$SNET_LIBS:$LPEL_PREFIX/lib:$LD_LIBRARY_PATH`  

     On OS X:

     `# on OS X, include $SNET_LIBS and LPEL in your DYLD_LIBRARY_PATH:`  
     `export DYLD_LIBRARY_PATH=$SNET_LIBS:$LPEL_PREFIX/lib:$DYLD_LIBRARY_PATH`  


8. Download the S-Net compiler archive: 
    [Linux x86_64](https://raw.github.com/snetdev/releases/master/2013/snetc-20130626.x86_64.bz2),
    [Linux i686](https://raw.github.com/snetdev/releases/master/2013/snetc-20130626.i686.bz2),
    [OS X](https://github.com/snetdev/releases/blob/master/2013/merijn/snetc-20130206.osx?raw=true)

    The archive contains a compiled binary, which is compressed with bzip2.
    Turn this into a valid executable with:

    `bunzip2 snetc-*.bz2`
    `mv snetc-* snetc`
    `chmod +x snetc`
    
    For convenience, place the decompressed compiler binary into a directory in your $PATH.


