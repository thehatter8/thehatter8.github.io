# Snort3 Installation Guide

### Requirements Pre-Snort install



Start by checking for or installing the following, they are required for building some of the packages we need

* C++ 14 compatible compiler
  
  * `sudo apt install g++`

* cmake
  
  * `sudo apt install cmake`

* git
  
  * `sudo apt install git`
    
    

Now to move on to the main Snort requirements

* dnet
  
  * `sudo apt install libdumbnet-dev`

* hwloc
  
  * `sudo apt install libhwloc-dev`

* OpenSSL
  
  * `sudo apt install libssl-dev`

* bison
  
  - `sudo apt install bison`
- flex
  - `sudo apt install flex`

* pcap
  
  * `sudo apt install libpcap-dev` - probably won't work
  
  * `git clone https://github.com/the-tcpdump-group/libpcap.git`
  
  * `./autogen.sh`
  
  * `./configure --prefix=/usr/local`
  
  * `make`
  
  * `sudo make install`
  
  * Requires bison and flex

* pcre
  
  * `sudo apt install libpcre3-dev`

* pkg-config
  
  * `sudo apt install pkg-config`

* zlib
  
  * `sudo apt install zlib1g-dev`

* libtool
  
  * `sudo apt install libtool`
  
  * Was already installed on mine, probably from another library

* libunwind
  
  * `sudo apt install libunwind-dev`

* LuaJIT
  
  - `git clone https://luajit.org/git/luajit.git`
  
  - `cd luajit`
  
  - `make && sudo make install`



Installing LibDAQ

* Start by downloading and configuring LibDAQ git files
  
  * `git clone https://github.com/snort3/libdaq.git`
  
  * `cd libdaq`
  
  * `./bootstrap`
  
  * `./configure` don't do the prefix like implied in the docs, it will break everything
  
  * `make install` I had to use `sudo` for this to work properly

* Now run ldconfig to bind everything together
  
  * If it worked properly you will not see any messages appear. For example:
  
  * `snortusr@snort3srv:~/snort3/build/src$ sudo ldconfig`
  
  * `snortusr@snort3srv:~/snort3/build/src$     `



Installing Snort

* Start by downloading and configuring the Snort3 git repository
  
  * `git clone https://github.com/snort3/snort3.git`
  
  * `cd snort3`
  
  * `./configure_cmake.sh` Don't use prefix unless you really need to, defaults are fine
  
  * `cd build` 
  
  * `make -j $(nproc)`
  
  * `sudo make install`

* Test the new Snort installation
  
  * `cd src` while still in the `/somedir/snort3/build` directory
  
  * `./snort -v`



Using Snort

* Some snort commands seem to require sudo
  
  * In this case, use the full path to call snort. For me it would be:
    
    * `sudo /home/snortusr/snort3/build/src/snort -commands options`

* Using community rules
  
  * `curl -L https://snort.org/downloads/community/snort3-community-rules.tar.gz > rules.tar.gz`
  
  * `tar xvf rules.tar.gz`
    
    * This gives you `sid-msg.map` and `snort3-community.rules` which we can now move into our somedir/snort3/build/src/ folder
      
      * `sudo mv sid-msg.map /somedir/snort3/build/src/sid-msg.map`
      
      * `sudo mv snort3-community.rules /somedir/snort3/build/src/snort3-community.rules`
  
  * Now we look for snort.lua















