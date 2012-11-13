---
layout: post
title: "scribe install"
description: ""
category: linux 
tags: [ scribe]
---
{% include JB/setup %}

scribe安装步骤脚本：

之前搞了很久没有安装成功，需要依赖的库太多了。

google  group中找到一个安装脚本，试验成功，分享一下。

    #!/bin/bash

    echo "Install the necessary tools"

    sudo apt-get install make flex bison libtool libevent-dev automake pkg-config libssl-dev libboost-all-dev libbz2-dev build-essential g++ python-dev git

    echo "git cloning Thrift"

    git clone https://github.com/apache/thrift.git
    pushd thrift
        git fetch
        git branch -a
        git checkout 0.8.x # latest version at this time
        # install jdk and ant if you need the java code generator
        sudo apt-get install openjdk-7-jdk ant
        ./bootstrap.sh #ignore warning
        ./configure
        make
        sudo make install

        # at thrift directory
        pushd lib/py
                sudo python setup.py install
        popd


        #------------------------------------------
        # TESTING Thrift
        #------------------------------------------
        echo "Testing Thrift"
                pushd tutorial
                #in thrift/tutorial directory
                thrift -r -v --gen java tutorial.thrift
                echo "It willll generate a gen-java folder with sources if successful."
        popd




        #------------------------------------------
        # Installing fb303
        #------------------------------------------
        echo "Now installing fb303..."
        pushd contrib/fb303
                #in thrift/contrib/fb303 directory
                ./bootstrap.sh
                ./configure CPPFLAGS="-DHAVE_INTTYPES_H -DHAVE_NETINET_IN_H"
                make
                sudo make install
                echo "Install Python Module for Thrift and fb303"

                pushd py
                        sudo python setup.py install
                        echo "To check that the python modules have been installed properly, run:"
                        python -c 'import thrift' ; python -c 'import fb303'
                popd
        popd


    popd
    #------------------------------------------
    # End Thrift
    #------------------------------------------

    echo "Installing Scribe..."
    git clone https://github.com/facebook/scribe.git
    pushd scribe
        ./bootstrap.sh
        ./configure CPPFLAGS="-DHAVE_INTTYPES_H -DHAVE_NETINET_IN_H -DBOOST_FILESYSTEM_VERSION=2" LIBS="-lboost_system -lboost_filesystem"
        make
        sudo make install
        echo "Export an environment variable"
        export LD_LIBRARY_PATH=/usr/local/lib
        echo "Install Python Module for Scribe"

        pushd lib/py
                sudo python setup.py install
                echo "poor-man's Checking that the python modules have been install properly"
                python -c 'import scribe'
        popd

        export LD_LIBRARY_PATH=/usr/local/lib
        echo "export LD_LIBRARY_PATH=/usr/local/lib" >> ~/.bashrc

    popd

    echo "PHEWWWWW..... finally"
    echo "DONE. "

    echo "TESTING THIS BB"
    scribed

