## SUSE installation

[\[__Go back__\]](https://kagsimsek.github.io)

To-do for a fresh installation of Leap or Tumbleweed but with a focus on the latter.

* human-friendly hostname

```bash
sudo hostname <computer name>
sudo vi /etc/hostname
```

* window decorations, buttons, panel

* dolphin, kate

* vivaldi, zoom, etc.

* packman

```bash
# for Leap:
sudo zypper ar -cfp 90 'https://ftp.gwdg.de/pub/linux/misc/packman/suse/openSUSE_Leap_$releasever/' packman
# or for Tumbleweed:
sudo zypper ar -cfp 90 https://ftp.gwdg.de/pub/linux/misc/packman/suse/openSUSE_Tumbleweed/ packman

sudo zypper dup --from packman --allow-vendor-change
```

* packages

```bash
sudo zypper install -t pattern devel_basis
sudo zypper in vim make gcc gcc-devel gcc-fortran gcc-c++ htop ffmpeg gnuplot meld gv pv \
               texlive-scheme-full \
               python3-devel dropbox-cli libxcb-xtest.so.0 libxcb-xtest0 ibus ibus-m17n bash \
               cmake binutils bc libXpm-devel xorg-x11-devel \
               libXext-devel libopenssl-devel pcre-devel Mesa \
               glew-devel libpng16-devel pkgconf libmariadb-devel \
               fftw3-devel cfitsio cfitsio-devel graphviz graphviz-devel \
               libdns_sd avahi-compat-mDNSResponder-devel openldap2 \
               openldap2-devel libxml2-2 libxml2-devel krb5 krb5-devel \
               gsl gsl-devel chromium chromium-bsu chromium-ffmpeg-extra \
               chromium-plugin-widevinecdm libQt5Gui5 libQt5Gui-devel \
               libqt5-qtwebengine libqt5-qtwebengine-devel doxygen libblas3 \
               liblapack3 octave shotwell mlocate blas-devel lapack-devel \
               libopenblas_openmp0 libopenblas_openmp-devel libopenblas_serial0 \
               libopenblas_serial-devel openblas-devel libatlascpp-0_6-1 \
               atlascpp-devel yaml-cpp-devel libyaml-devel jaxodraw jaxodraw-latex \
               # the following could be 7:
               libyaml-cpp0_6 \
               libtirpc3 libtirpc-devel texstudio git MozillaThunderbird \
               # the following are required by xfitter
               gcc7 gcc7-c++ gcc7-devel gcc7-fortran \
               # sound for x1c9
               sof-firmware
               # to connect python to mma
               python3-pyzmq 
sudo updatedb # for `locate` to work
```

* vim

```bash
syntax on 

set tabstop=2
set shiftwidth=2
set expandtab
```

* git

```bash
git config --global user.name "Kağan Şimşek"
git config --global user.email <my email>

mkdir ~/github
cd ~/github
git clone https://github.com/kagsimsek/<repos>
```

* mathematica

```bash
mkdir ~/packages
cd ~/packages
mkdir mathematica-13.0
cd mathematica-13.0
mkdir installation-13.0 bin-13.0
mv ~/Downloads/Mathematica*.sh . 
bash Mathematica*.sh
```

* anaconda

```bash
mkdir ~/packages 
cd ~/packages 
mkdir anaconda-3
cd anaconda-3
mv ~/Downloads/Anaconda3*.sh .
bash Anaconda3*.sh
source ~/.bashrc
```

* after installing anaconda, replace ~/.bashrc with the following:

```bash
# Sample .bashrc for SuSE Linux
# Copyright (c) SuSE GmbH Nuernberg

# There are 3 different types of shells in bash: the login shell, normal shell
# and interactive shell. Login shells read ~/.profile and interactive shells
# read ~/.bashrc; in our setup, /etc/profile sources ~/.bashrc - thus all
# settings made here will also take effect in a login shell.
#
# NOTE: It is recommended to make language settings in ~/.profile rather than
# here, since multilingual X sessions would not work properly if LANG is over-
# ridden in every subshell.

# Some applications read the EDITOR variable to determine your favourite text
# editor. So uncomment the line below and enter the editor of your choice :-)
#export EDITOR=/usr/bin/vim
#export EDITOR=/usr/bin/mcedit

# For some news readers it makes sense to specify the NEWSSERVER variable here
#export NEWSSERVER=your.news.server

# If you want to use a Palm device with Linux, uncomment the two lines below.
# For some (older) Palm Pilots, you might need to set a lower baud rate
# e.g. 57600 or 38400; lowest is 9600 (very slow!)
#
#export PILOTPORT=/dev/pilot
#export PILOTRATE=115200

test -s ~/.alias && . ~/.alias || true

# infinite history

HISTFILESIZE=
HISTSIZE=

# ANACONDA

# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/home/ksimsek/packages/anaconda-3/installation-3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/home/ksimsek/packages/anaconda-3/installation-3/etc/profile.d/conda.sh" ]; then
        . "/home/ksimsek/packages/anaconda-3/installation-3/etc/profile.d/conda.sh"
    else
        export PATH="/home/ksimsek/packages/anaconda-3/installation-3/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<

# my stuff

shopt -s extglob

export PS1="\[\033[38;5;1m\][\[$(tput sgr0)\]\[\033[38;5;12m\]\u\[$(tput sgr0)\]\[\033[38;5;7m\]@\[$(tput sgr0)\]\[\033[38;5;214m\]\h\[$(tput sgr0)\] \[$(tput sgr0)\]\[\033[38;5;77m\]\W\[$(tput sgr0)\] \[$(tput sgr0)\]\[\033[38;5;1m\]]\[$(tput sgr0)\]\[\033[38;5;7m\]\\$\[$(tput sgr0)\] \[$(tput sgr0)\]"

alias c='clear'

alias o='xdg-open'

alias l='c ; ls -lvhF'
alias la='c ; ls -lvahF'
alias ltr='c ; ls -lvtrhF'

# for Leap:
alias ua='sudo zypper refresh && sudo zypper up'
# for Tumbleweed:
alias ua='sudo zypper refresh && sudo zypper dup'

alias cpdir='echo $(pwd) > $HOME/.cpdir'
alias cddir='cd $(cat $HOME/.cpdir)'

alias on_ac='sudo tlp setcharge 45 50'
alias on_bat='sudo tlp setcharge 85 90'

# PACKAGES

export PACKAGES=/home/ksimsek/packages

# MATHEMATICA

export MATHEMATICA_BIN=$PACKAGES/mathematica-13.0/bin-13.0
export PATH=$PATH:$MATHEMATICA_BIN

# LHAPDF

export LHAPDF_LIBRARY_PATH=$PACKAGES/lhapdf-6.4.0/installation-6.4.0/lib
export LHAPDF_BIN=$PACKAGES/lhapdf-6.4.0/installation-6.4.0/bin
export LHAPDF_FLAG="-L${LHAPDF_LIBRARY_PATH} -lLHAPDF"
export PATH=$PATH:$LHAPDF_BIN
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$LHAPDF_LIBRARY_PATH
export PYTHONPATH=$PYTHONPATH:$LHAPDF_LIBRARY_PATH/python3.9/site-packages

# QCDNUM

export QCDNUM_BIN=$PACKAGES/qcdnum-17.01.14/installation-17.01.14/bin
export QCDNUM_LIBRARY_PATH=$PACKAGES/qcdnum-17.01.14/installation-17.01.14/lib
export PATH=$PATH:$QCDNUM_BIN
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$QCDNUM_LIBRARY_PATH

# CERN ROOT

export ROOT_BIN=$PACKAGES/root-6.24.06/installation-6.24.06/bin
export ROOT_LIBRARY_PATH=$PACKAGES/root-6.24.06/installation-6.24.06/lib
export PATH=$PATH:$ROOT_BIN
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$ROOT_LIBRARY_PATH

# XFITTER

export XFITTER_BIN=$PACKAGES/xfitter-2.0.1/installation-2.0.1/bin
export XFITTER_INCLUDE=$PACKAGES/xfitter-2.0.1/installation-2.0.1/include
export XFITTER_LIBRARY_PATH=$PACKAGES/xfitter-2.0.1/installation-2.0.1/lib
export PATH=$PATH:$XFITTER_BIN
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$XFITTER_LIBRARY_PATH
```

* lhapdf

```bash
mkdir ~/packages
cd ~/packages
mkdir lhapdf-6.4.0
cd lhapdf-6.4.0
mv ~/Downloads/LHAPDF*.tar.gz .
tar xvzf LHAPDF*.tar.gz
mkdir installation-6.4.0
cd LHAPDF-6.4.0
./configure --prefix=/home/ksimsek/packages/lhapdf-6.4.0/installation-6.4.0
make
make install

python # and try importing lhapdf. if it doesn't work:
cd /home/ksimsek/packages/anaconda-3/installation-3/lib
mv libstdc++.so libstdc++.so.bak
mv libstdc++.so.6 libstdc++.so.6.bak
ln -s /usr/lib64/libstdc++.so.6.0.29 ./libstdc++.so
ln -s /usr/lib64/libstdc++.so.6.0.29 ./libstdc++.so.6

lhapdf install NNPDF31_nlo_as_0118
lhapdf install NNPDFpol11_100 
```

* package x

* feyncalc

```mathematica
Import["https://raw.githubusercontent.com/FeynCalc/feyncalc/master/install.m"];
InstallFeynCalc[]
```

* matex

```mathematica
ResourceFunction["MaTeXInstall"][]
```

* feyntools: FeynArts, LoopTools, FormCalc

```bash
mkdir ~/packages
cd ~/packages
mkdir feyntools
cd feyntools
wget http://www.feynarts.de/FeynInstall
chmod 755 FeynInstall
./FeynInstall
```

* qcdnum

```bash
mkdir ~/packages
cd ~/packages
mkdir qcdnum-17.01.14
cd qcdnum-17.01.14
mkdir installation-17.01.14
mv ~/Downloads/qcdnum*.tar.gz .
tar xvzf qcdnum*.tar.gz
cd qcdnum-17-01-14
./configure --prefix=/home/ksimsek/packages/qcdnum-17.01.14/installation-17.01.14 # FFLAGS=-fallow-argument-mismatch # if needed
make -j8
make install
```

* root

```bash
mkdir ~/packages
cd ~/packages
mkdir root-6.24.06
cd root-6.24.06
mkdir installation-6.24.06
mkdir build-6.24.06
mv ~/Downloads/root*.tar.gz .
tar xvzf root*.tar.gz
cd build-6.24.06
cmake -DCMAKE_INSTALL_PREFIX=/home/ksimsek/packages/root-6.24.06/installation-6.24.06 /home/ksimsek/packages/root-6.24.06/root-6.24.06
cmake --build . --target install
cd ../installation-6.24.06/
source bin/thisroot.sh
```

* xfitter

```bash
mkdir ~/packages
cd ~/packages
mkdir xfitter-2.0.1
cd xfitter-2.0.1
mv ~/Downloads/xfitter*.tgz .
tar xvzf xfitter*.tgz
mkdir installation-2.0.1
cd xfitter*/
vi configure.ac # replace c++11 with c++14 in CXXFLAGS or whatever the version is in `root-config --cflags`
autoreconf -f -i
# ./configure --enable-lhapdf --enable-root --prefix=/home/ksimsek/packages/xfitter-2.0.1/installation-2.0.1 LIBS=-ltirpc # FFLAGS=-fallow-argument-mismatch F77=gfortran-7 FC=gfortran-7
./configure --enable-lhapdf --enable-root --prefix=/home/ksimsek/packages/xfitter-2.0.1/installation-2.0.1 LIBS=-ltirpc FFLAGS=-Wno-argument-mismatch F77=gfortran-7 FC=gfortran-7 CXX=g++-7 CC=gcc-7 # on tumbleweed
make
make install
```

* dropbox, texstudio

Last updated K$ Feb 15, 2022.
