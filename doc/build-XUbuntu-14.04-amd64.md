# Europecoin-V3 Ubuntu/Xbuntu Instructions
The following is an all inclusive guide to getting Europecoin running on Ubuntu Linux. These instructions should work on Ubuntu (and it's variants - Xbuntu, etc) starting with version **14.04**. If for some reason you are still running an older version, extra steps may be necessary and it is recommended that you instead update your distribution's version.

**Table of contents**

1. [Preparing your environment](#preparing-your-environment)
  * [For basic building](#for-basic-building)
  * [For Berkeley DB 4.8](#for-berkeley-db-4.8)
  * [For QT5 GUI client building](for-qt5-gui-client-building)
  * [For QR codes capabilities](#for-qr-codes-capabilities)
  * [For Miniupnpc capabilities](#for-miniupnpc-capabilities)
2. [Getting the source](#getting-the-source)
  * [Fixing script permissions](#fixing-script-permissions)
3. [Configure and compile](#configure-and-compile)
  * [Configuration options](#configuration-options)
  * [Strip debugging symbols](#strip-debugging-symbols-optional)
  * [Installing to a better location](#Installing-to-a-better-location)
4. [Running the compiled binaries](#running-the-compiled-binaries)
5. [Setting up the conf file](#setting-up-the-conf-file)
  * [Example conf file](#example-conf-file)
6. [Downloading the pre-compiled binaries](#download-the-pre-compiled-binaries)
7. [Credits](#credits)


## Preparing your environment
As per the requirements and dependencies specifications in [doc/build-unix.md](build-unix.md), it may be necessary to install the required dependencies prior to downloading and compiling the source. Following the steps in this section will leave you with a fully prepared build environment.

#### For basic building
```bash
sudo apt-get install build-essential libtool autotools-dev autoconf pkg-config libssl-dev libboost-all-dev git
```

#### For Berkeley DB 4.8
The wallet.dat file relies on BerkeleyDB (BDB), specifically version 4.8 to maintain binary compatibility. Ubuntu 14.04+ doesn't provide this version however, so you'll need to install it from the Bitcoin PPA.
```bash
sudo apt-get install software-properties-common python-software-properties
sudo add-apt-repository ppa:bitcoin/bitcoin
sudo apt-get update
sudo apt-get install libdb4.8-dev libdb4.8++-dev
```

#### For QT5 GUI client building
If you are only intending to compile the CLI daemon, skip this step.
```bash
sudo apt-get install libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler
```

#### For QR codes capabilities
If you are only intending to compile the CLI daemon, skip this step.
(if you don't know what this means, just skip it :) )
```bash
sudo apt-get install libqrencode-dev
```

#### For Miniupnpc capabilities
If you don't know what this is, or would rather not make use of it, skip this step.
```bash
sudo apt-get install libminiupnpc-dev
```


## Getting the source
```bash
cd
git clone https://github.com/LIMXTEC/Europecoin-V3.git Europecoin-V3src/
cd Europecoin-V3src/
```

#### Fixing script permissions
This shouldn't be necessary on most systems, but there are rare occasions where the cloning process doesn't set the execute flag properly.
```bash
chmod -Rc +x ./*.sh
chmod -Rc +x ./*/*.sh
chmod -Rc +x ./*/*/*.sh
chmod -Rc +x ./*/*/build_detect_platform
```


## Configure and compile
Now that you have the source, configure and compile it with the following three commands. If you would like to see some options that you can pass to `configure` then read the section below before proceeding.
```bash
./autogen.sh
./configure
make
```

#### Configuration options
the configure script has options that can change the feature set and what gets compiled. Below are some common 'flags' that can or should be used depending on your dependencies choices or your intended compile result

```
--with-gui=no           (disables compiling the gui wallet even if qt is available)
--without-miniupnpc     (disables miniupnpc support entierly (miniupnpc not required))
--enable-upnp-default   (forces miniupnpc to be used by default (miniupnpc required)
```

For example, if you only want to compile the CLI daemon:
```bash
./configure --with-gui=no
```

#### Strip debugging symbols (optional)
If you plan to do `make install` then you can skip this step.
```bash
strip src/europecoind
strip src/europecoin-cli
strip src/europecoin-tx
strip src/qt/europecoin-qt
```

#### Installing to a better location
If you want the binaries copied to /usr/local/bin
```bash
make install
```
*This may require root privs. Run `sudo make install` if the above gives an error.*

Or you can copy thse binaries to the folder of your choice manually.


## Running the compiled binaries
if you **DID NOT** run `make install`, then after compilation finishes, and from the same directory that the compilation steps were done in, use either of the following:

`./src/europecoind` (starts the CLI daemon)

`./src/qt/europecoin-qt` (starts the GUI wallet)

------
if you **DID** run `make install`, then you can use either of the following terminal commands from any directory:
```bash
europecoind
europecoin-cli
europecoin-qt
```


## Setting up the conf file
You can access/create/edit the conf file from the terminal using the following commands:
```bash
cd ~/.europecoin/
vi europecoin.conf
```
*If you don't like vi, you can use nano instead (may be easier for first-time users):* `nano europecoin.conf`

#### Example conf file
The minimum recommended entries for the conf file are as follows:
```
rpcuser=xxx
rpcpassword=xxx
daemon=1
server=1
listen=1
```
*replace the strings of 'xxx' with whatever you desire*

## Download the pre-compiled binaries
If all else fails, and you would rather just download the pre-compiled binaries, use the following steps

```bash
wget https://github.com/LIMXTEC/Europecoin-V3/releases/download/Europecoin_V3.0.1.0.1/Europecoin-Linux64.zip
unzip Europecoin-Linux64.zip
cp europecoin* /usr/local/bin/
```
*if the last step fails with a permission error, instead run* `sudo cp europecoin* /usr/local/bin/`

Then, to run, use either of the following:
```
europecoind
europecoin-cli
europecoin-tx
europecoin-qt
```

**Have fun and (maybe) show some appreciation**

## Credits
- **[LIMXDev](https://bitcointalk.org/index.php?action=profile;u=389271) ()**
- **[szenekonzept](https://bitcointalk.org/index.php?action=profile;u=333146) ()**
- **[rmd73](https://bitcointalk.org/index.php?action=profile;u=356883) (EJZwagsubfxn1xeB4JmztAWitgTPty3FzN)**
- **[Fuzzbawls](https://bitcointalk.org/index.php?action=profile;u=522056) (EXcrtRkkrAikwhFVX8G2tXccsbpnG7boJ5 - No TDs Please)**
