---
layout: pages
title: Setting up and compiling
---

1. Install libpcl - GNU Portable Coroutine Library, currently v1.12
   available at

   [http://www.xmailserver.org/libpcl.html](http://www.xmailserver.org/libpcl.html)


2. Extract the LPEL archive, then run:


    `./configure --with-pcl=<pcl_install_dir>`  
    `--with-mctx=pcl`  
    `--prefix=<lpel_install_dir>`    

    `make`  
    `make install`  


3. Extract the snet-runtime archive.



4. At the top-level of the runtime tree, run:  


     `./configure --with-lpel-includes=<lpel_install_dir>/include \`  
     `            --with-lpel-libs=<lpel_install_dir>/lib \`  
     `            --prefix=<my_snet_dir>`  

     `make                # this builds the run-time system`  
     `make install        # moves files into place under <my_snet_dir>`  

     `export SNET_INCLUDES=<my_snet_dir>/include/snet`  
     `export SNET_LIBS=<my_snet_dir>/lib/snet`  
     `export SNET_MISC=<my_snet_dir>/share/snet`



5. Set your library search path for S-Net and LPEL.  On Linux:

     `export LD_LIBRARY_PATH=$SNET_LIBS:<lpel_install_dir>:$LD_LIBRARY_PATH`  

     On OS X:

     `# on OS X, include $SNET_LIBS and LPEL in your DYLD_LIBRARY_PATH:`  
     `export DYLD_LIBRARY_PATH=$SNET_LIBS:<lpel_install_dir>:$DYLD_LIBRARY_PATH`  


6. Download the S-Net compiler archive and unpack it. The archive contains a compiled binary. For convenience you may want to consider placing the compiler binary into a directory in your $PATH.

