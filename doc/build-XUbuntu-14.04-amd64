# prepare your environment (if necessary)
# as per requirements and dependencies specifications in doc/build-unix.md
# for basic (daemon) building 
user@machine:~$ sudo apt-get install build-essential libtool autotools-dev autoconf pkg-config libssl-dev
# for libdb4.8 (if not already installed/compiled)
user@machine:~$ sudo add-apt-repository ppa:bitcoin/bitcoin
user@machine:~$ sudo apt-get update
user@machine:~$ sudo apt-get install libdb4.8-dev libdb4.8++-dev
# for qt5 GUI client building
user@machine:~$ sudo apt-get install libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler
# for QR codes capabilities (if you don't know what that means, just skip it :) )
user@machine:~$ sudo apt-get install libqrencode-dev

# get the source
user@machine:~$ git clone https://github.com/LIMXTEC/Europecoin-V3 Europecoin-V3src/
# actually go there ;)
user@machine:~$ cd Europecoin-V3src/

# I needed to explicitly grant "execute" permission to all shell scripts in the source tree. 
# I know, I'm lazy...
# YMMV.
user@machine:~$  chmod -Rc +x ./*.sh
user@machine:~$  chmod -Rc +x ./*/*.sh
user@machine:~$  chmod -Rc +x ./*/*/*.sh
user@machine:~$  chmod -Rc +x ./*/*/build_detect_platform

user@machine:~$ ./autogen.sh 

user@machine:~$ ./configure 

user@machine:~$ make

user@machine:~$ strip europecoind
user@machine:~$ strip europecoin-cli
user@machine:~$ strip europecoin-tx
user@machine:~$ strip qt/europecoin-qt
# just making sure it will run ;)
user@machine:~$ chmod +x qt/europecoin-qt

# if you want the binaries copied to /usr/local/bin
user@machine:~$ make install

# ... or you can copy thse binaries to the folder of your choice
# Have fun and (maybe) show some appreciation (EJZwagsubfxn1xeB4JmztAWitgTPty3FzN).
# User:https://bitcointalk.org/index.php?action=profile;u=356883


### Notes

##### Fetching and compiling the source (assumes you have all the dependencies):

cd
git clone https://github.com/LIMXTEC/Europecoin-V3.git Europecoin-V3src/
cd Europecoin-V3src/
chmod -Rc +x ./*.sh
chmod -Rc +x ./*/*.sh
chmod -Rc +x ./*/*/*.sh
chmod -Rc +x ./*/*/build_detect_platform
./autogen.sh
./configure
make
make install

### *the last line is optional, and may need to be ran with root privs by running 'sudo make install'

#### Running the compiled binaries:
## if you **DID NOT** do the last optional compile step, then after compilation finishes, and from the same directory that the compilation steps were done in:

./src/europecoind             (starts the headless daemon)
./src/europecoin-cli          (CLI program to issue RPC commands like 'getinfo', 'stop', etc)
./src/qt/europecoin-qt        (starts the QT GUI wallet)


if you **DID** do the last optional compile step (make install), then you can use the following terminal commands from any directory:

europecoind                   (starts the headless daemon)
europecoin-cli                (CLI program to issue RPC commands like 'getinfo', 'stop', etc)
europecoin-qt                 (starts the QT GUI wallet)



## Setting up the conf file:
You can access/create/edit the conf file from the terminal using the following commands:

cd ~/.europecoin/
vi europecoin.conf

*If you don't like vi, you can use nano instead (may be easier for first-time users): 'nano europecoin.conf'

## Minimum recommended entries for the conf file are as follows:

rpcuser=xxx
rpcpassword=xxx
daemon=1
server=1
listen=1

*replace the strings of 'xxx' with whatever you desire






### BONUS - Download the pre-compiled linux 64-bit binaries:
If all else fails, and you would rather just download the pre-compiled binaries, follow the following steps

wget https://github.com/LIMXTEC/Europecoin-V3/releases/download/Europecoin_V3.0.1.0.1/Europecoin-Linux64.zip
unzip Europecoin-Linux64.zip
cp europecoin* /usr/local/bin/

*if the last step fails with a permission error, instead run 'sudo cp europecoin* /usr/local/bin/

Then, to run:

europecoind                   (starts the headless daemon)
europecoin-cli                (CLI program to issue RPC commands like 'getinfo', 'stop', etc)
europecoin-qt                 (starts the QT GUI wallet)
