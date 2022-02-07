## Tutorials

[\[__Go back__\]](https://kagsimsek.github.io)

_Before Feb 6, 2022: most of the stuff need rewriting. most links are dead or not visible at all._

HEP tools

April 12, 2019

This is a mini course on installing some high-energy tools on any flavor of Ubuntu. Notice that for other Linux distros (Debian, OpenSUSE Arch, Manjero, Linux Mint, etc.), you just need to replace your package manager and package names in steps (1) and (3). Mac has always been a big pain in the neck, so refer to the bottom of this page.

(1) Update your OS:
sudo apt update && sudo apt upgrade -y && sudo apt dist-upgrade -y && sudo apt autoremove -y

(2) Install Mathematica and activate it. Also install ‘wolframscript’ integration (it will be asked as the last step at the end of the installation of Mathematica).

(3) Install ‘unzip’, ‘wget’, ‘make’, GNU compiler for C, C++, and Fortran, GNUPlot, LaTeX, X11 graphics library, and Python:
sudo apt install unzip wget make gcc g++ gfortran gnuplot texlive-full libx11-dev python-dev build-essential

(4) Prepare a directory for the packages to be installed.

```
mkdir $HOME/packages
```

(5) Install LanHEP (latest version 3.3.2):

```
mkdir $HOME/packages/lanhep
cd $HOME/packages/lanhep
wget https://theory.sinp.msu.ru/~semenov/lhep332.tgz
tar xvzf lhep332.tgz
cd lanhep332
make
echo "export PATH=\$PATH:$HOME/packages/lanhep/lanhep332" >> $HOME/.bashrc 
. $HOME/.bashrc
```

(6) Install FeynArts, FormCalc, and LoopTools (latest versions 3.11, 9.8, and 2.15, respectively):

```
mkdir $HOME/packages/feyntools
cd $HOME/packages/feyntools
wget http://www.feynarts.de/looptools/FeynInstall
chmod 755 FeynInstall
./FeynInstall
```

Answer all the questions literally with ‘yes’ and press Return. If you get an error during the installation, see the corresponding log file and follow the directions there.

(7) Install Package X (latest version 2.1.1):

```
mkdir $HOME/packages/package-x
cd $HOME/packages/package-x
wget https://packagex.hepforge.org/downloads/X-2.1.1.zip
unzip X-2.1.1.zip
cat << EOF > $HOME/.package-x.info
Print[\$UserBaseDirectory]
EOF
xdir=$(wolframscript -script $HOME/.package-x.info)
cp -r X $xdir/Applications/
rm $HOME/.package-x.info
```

(8) Install LHAPDF (latest version 6.2.1):

```
mkdir $HOME/packages/lhapdf6
cd $HOME/packages/lhapdf6
wget http://www.hepforge.org/archive/lhapdf/LHAPDF-6.2.1.tar.gz
tar xvzf LHAPDF-6.2.1.tar.gz
cd LHAPDF-6.2.1
mkdir $HOME/local
mkdir $HOME/local/LHAPDF
./configure --prefix=$HOME/local/LHAPDF
make
make install
wget http://www.hepforge.org/archive/lhapdf/pdfsets/6.2/cteq6l1.tar.gz -O- | tar xz -C $HOME/local/LHAPDF/share/LHAPDF
```

(9) Install CalcHEP (latest version 3.7.5):

```
mkdir $HOME/packages/calchep
cd $HOME/packages/calchep
wget https://theory.sinp.msu.ru/~pukhov/CALCHEP/calchep_3.7.5.tgz
tar xvzf calchep_3.7.5.tgz
cd calchep_3.7.5
make
./mkWORKdir $HOME/packages/calchep/calchep-work
```

Earlier than April 12, 2019

Short way (tested on different machines and different distros): For Debian- and Arch-based distros, save this file anywhere in your system

```
wget https://www.dropbox.com/s/k76afhh2l0wsr6o/install-hep-tools
make it executable
chmod a+x install-hep-tools
and source it
. ./install-hep-tools
```

to directly install all the packages. You may report any bugs.

*****

Long way: If you are a linux newbie and want to get involved in a standard package installation procedure, you are encouraged to follow the guide here.

Below, you may find the step-by-step unix commands to install some high-energy physics (HEP) tools including LanHEP, FeynArts and related tools, Package X, LHAPDF6, and CalcHEP. More tutorials on how to make computations will appear soon.

The only assumptions I make are that you are familiar with Linux (or Mac) command-line interference and that some late version of Mathematica is installed on your computer. If you do not have Mathematica installed, you may obtain it from here. Later, I have relaxed the assumption of the familiarity with the command-line interface by preparing these notes.

Debian-based distributions, to which Ubuntu is a popular example, should arrive with the necessary tools like gcc and gfortran. Well, no, it doesn’t apparently. Please install them as described below.

If you have a directory called ‘packages’ in your home directory (/home/username in Linux and /Users/username in macOS, or simply $HOME in both), then to avoid conflict, set the variable dirname to some other thing that suits your taste.

Though not expected, if you get some error during the installation, run the same command with ‘sudo’. Sometimes, permissions can be a big problem in the neck. Otherwise, everything should follow smoothly.

Personally, I have tested everything here on both Linux (Ubuntu and OpenSUSE) and macOS X High Sierra (version 10.13.3). There might be some problems in the installation process. These include 

that the license of Mathematica may have expired — which is the case at our university, at the moment — so that FeynArts and related tools cannot start the Mathematica kernel during the installation. We are working on solving this problem now. I don’t know the license issue as of March 9, so you may want to try Mathematica 11.1. But when downloading it from the link above, you need to manually correct the address since there is a mistake there. The original link looks like …11.0.1/… but we need …11.1.1/… Do this, download the file, install it properly, and together we will do the rest. As of March 21, 2018, the license issue is no more. You may want to download and install the latest version of Mathematica from the website cited above. 

that sometimes wget yields the error 404 not found. In that case, please google the package that appears here and follow the guides there. I will prepare additional notes for that.

that tar may not work on Mac. It works on mine, so I don’t know the reason for that.

that LHAPDF simply does not work on Mac — at least I couldn’t figure it out. It is completely doable on linux, though.

If you still have questions, try to find me at my office with your computer as soon as possible.

How to install LanHEP (latest version is 3.2.0)

```
# let's update the system and the repositories:
sudo apt update # on Debian-based distros 
# 'sudo softwareupdate -ia' on Mac, though this may not be that effective. 
## do 'brew update && brew upgrade `brew outdated`' if you have brew installed.
cd
dirname=packages
mkdir $HOME/$dirname
mkdir $HOME/$dirname/lanhep
cd $HOME/$dirname/lanhep
wget http://theory.sinp.msu.ru/~semenov/lhep32.tgz # 'curl -O <link>' on macOS
tar -xvzf lhep32.tgz
cd lanhep320
make
# obtain or create a source file.
# say you want this toy model.
cd $HOME/$dirname/lanhep/lanhep320
mkdir toy-model
cd toy-model
mkdir in
mkdir out
cd in
wget --no-check-certificate https://blog.metu.edu.tr/ksimsek/files/2018/02/toy_model.txt 
mv toy_model.txt toy_model.lhep
cd ..
# now let's run the source to obtain interactions.
# if you plan to continue with feynarts, use the flag '-fa':
../lhep -fa in/toy_model.lhep -OutDir out > o
# where o is the output of the command you just performed.
# it is best practice to pipe the output into some text file.
# if you plan to continue with calchep, use the flag '-ca':
../lhep -ca in/toy_model.lhep -OutDir out > o
# want to run lhep anywhere in your system? 
cd
vi .bashrc # 'vi /etc/bashrc' on mac
# append the following line to the end:
export PATH="$PATH:/home/username/packages/lanhep/lanhep320" # you need to modify 'packages' if you 'dirname' is different.
# write and quit, ':wq'.
source .bashrc
```

Visit A. Semenov’s webpage for further information.

How to install FeynArts and related tools (FormCalc and LoopTools) (latest version is 3.9, 9.6, and 2.14, respectively)

```
# let's update the system and the repositories:
sudo apt update # on Debian-based distros 
# 'sudo softwareupdate -ia' on Mac, though this may not be that effective.
## do 'brew update && brew upgrade `brew outdated`' if you have brew installed.
cd
dirname=packages
mkdir $HOME/$dirname 
mkdir $HOME/$dirname/feyntools
cd $HOME/$dirname/feyntools
wget http://www.feynarts.de/FeynInstall # 'curl -O <link>' on macOS
# i suggest you to install not the latest versions due to some linking problems.
# to this end, run the following:
sed -i 's/^fadir=FeynArts-.$/fadir=FeynArts-3.9/g' FeynInstall
sed -i 's/^fcdir=FormCalc-.$/fcdir=FormCalc-9.5/g' FeynInstall
chmod 755 FeynInstall
### for macOS only, do the following:
# curl -O http://coudert.name/software/gfortran-6.3-Sierra.dmg 
# open gfortran-6.3-Sierra.dmg
### follow the instructions in README there. then do
# hdiutil detach /Volumes/gfortran-6.3-Sierra.dmg
### to eject the disk image.
### apparently, you need to do a similar thing on ubuntu.
# sudo apt install gcc
# sudo apt install gfortran
### Hahn explicitly urges ubuntu users not to use fort77.
./FeynInstall
# type and enter 'yes' to all the questions it asks.
# open a mathematica notebook. evaluate the following on linux:
# <</home/username/packages/feyntools/FeynArts-3.9/FeynArts.m
# <</home/username/packages/feyntools/FormCalc-9.5/FormCalc.m
# or on mac:
# <</Users/username/packages/feyntools/FeynArts-3.9/FeynArts.m 
# <</Users/username/packages/feyntools/FormCalc-9.5/FormCalc.m
# do not forget to change username to your actual username.
## you might need to modify the entire path if you have installed the packages to somewhere else.
# if you do not get an error, you are done.
# note that this is how we call external packages to our notebook.
```

Visit Thomas Hahn’s webpage for further information.

Once you believe you have successfully installed LanHEP and FeynArts (and related tools), you may check it. To this end, you may perform the following:

```
find $HOME -name "lhep"
find $HOME -name "FeynArts.m"
find $HOME -name "FormCalc.m"
```

Now, be careful: If you have multiple ‘lhep’, ‘FeynArts.m’, and ‘FormCalc.m’ files, please remove the ones that are not contained in the path /home/username/packages/lanhep/lanhep320 (or /Users/username/packages/lanhep/lanhep320), /home/username/packages/feyntools/FeynArts-3.9 (or /Users/username/packages/feyntools/FeynArts-3.9), and /home/username/packages/feyntools/FormCalc-9.5 (or /Users/username/packages/feyntools/FormCalc-9.5), respectively.

```
cd
mkdir tmp.toy_model
cd tmp.toy_model
wget --no-check-certificate https://blog.metu.edu.tr/ksimsek/files/2018/03/do.txt
wget --no-check-certificate https://blog.metu.edu.tr/ksimsek/files/2018/03/toy_model.lhep_.txt
wget --no-check-certificate https://blog.metu.edu.tr/ksimsek/files/2018/03/toy_model.m.orig_.txt
mv do.txt do
mv toy_model.lhep_.txt toy_model.lhep
mv toy_model.m.orig_.txt toy_model.m.orig
chmod a+x do
./do
```

I have prepared this script on mac. So, when you run ‘./do’, it will tell you to do two things: First, do that long ‘sed’ command if you are on a linux machine— notice that it is enough if you do it once; for your next run, you do not need to (in fact, you shouldn’t) do it again. Second, make sure that you have added ‘lhep’ to your path variable. When all set, run the following:

```
./do in A out B C
./do in A B out A B
./do in A B out B B C
```

If you get a .ps file displaying you the Feynman diagrams, then you are all set — probably FormCalc and LoopTools have also been installed successfully. You may try other 1-to-2, 2-to-2, or 2-to-3 processes, if they are possible within this model. You may get impressed how marvelous that script is.
If you get the error “file not found” or something, then please just go to the bottom of this site and download the tar file — it has been linked from my Dropbox, so there is almost no chance for it to be removed; what’s more, I have a more sophisticated version of this ‘do’ script.

How to install Package X (latest version is 2.1.1)

```
# let's update the system and the repositories:
sudo apt update # on Debian-based distros 
# 'sudo softwareupdate -ia' on Mac, though this may not be that effective. 
## do 'brew update && brew upgrade `brew outdated`' if you have brew installed.
cd
dirname=packages
mkdir $HOME/$dirname 
mkdir $HOME/$dirname/package-x
cd $HOME/$dirname/package-x
wget http://www.hepforge.org/archive/packages/X-2.1.1.zip
unzip X-2.1.1.zip
# in mac, wget and unzip lines are not working.
# if you have a similar error (say, 404 not found),
## then just go there and click on download. 
## again, Mac seems to directly unzip the file. 
## so, copy the X folder in downloads and paste it
## into packages/package-x.
# in linux, the unzipping is not automatic, I'm afraid.
## so, download the zip and unzip it in packages/package-x
## as shown above.
# open a Mathematica notebook, evaluate
# $UserBaseDirectory
# copy the path. let us denote this path as dir. 
# dir more or less looks like 
# /home/username/.Mathematica on linux and
# /Users/username/Library/Mathematica on Mac.
# quit Mathematica. do
cd
cp -r $HOME/$dirname/package-x/X dir/Applications/
# do not forget to replace dir with the actual path.
# open a mathematica notebook. evaluate the following:
# <<X`
# if you do not get an error, you are done.
```

Visit Hiren Patel’s webpage for further information.

How to install LHAPDF6

```
# let's update the system and the repositories:
sudo apt update # on Debian-based distros 
# 'sudo softwareupdate -ia' on Mac, though this may not be that effective. 
## do 'brew update && brew upgrade `brew outdated`' if you have brew installed.
sudo zypper in python-devel 
# 'sudo apt-get install python-dev' on ubuntu
# see 'Notes for Mac users' below.
dirname=packages
mkdir $HOME/$dirname 
mkdir $HOME/$dirname/lhapdf6
cd $HOME/$dirname/lhapdf6
wget http://www.hepforge.org/archive/lhapdf/LHAPDF-6.2.1.tar.gz
tar -xvzf LHAPDF-6.2.1.tar.gz
cd LHAPDF-6.2.1
mkdir $HOME/local
mkdir $HOME/local/LHAPDF
./configure --prefix=$HOME/local/LHAPDF
make
make install
# now install a specific pdf:
wget http://www.hepforge.org/archive/lhapdf/pdfsets/6.2/cteq6.tar.gz -O- | tar xz -C $HOME/local/LHAPDF/share/LHAPDF
cd
vi .bashrc
# append the following line at the end:
export PATH="$PATH:$HOME/local/LHAPDF"
# write and quit, ':wq'.
. .bashrc
# later, we will see in FormCalc that some processes will prompt errors.
# I mean, when you properly define a partonic process, you will need to
## use a certain pdf. however, these packages are written in c (or c++).
## the errors show up in formcalc only if you proceed with fortran.
## so, somehow, you need to link c++ to fortran. one way to do so is, add
## '-lstdc++' to the fortran flags, FFLAGS, in the configuration file.
# this issue is find with Mac. however, there is an issue to introduce
## looptools.h. i will resolve this soon.
```

Visit LHAPDF’s main page for further information.

How to install CalcHEP (latest version is 3.6.30)

```
# let's update the system and the repositories:
sudo apt update # on Debian-based distros 
# 'sudo softwareupdate -ia' on Mac, though this may not be that effective. 
## do 'brew update && brew upgrade `brew outdated`' if you have brew installed.
# for gui, the following is required:
sudo apt install libX11-dev # on ubuntu
# 'sudo zypper in xorg-x11-devel' on opensuse
# for mac, go there, and download and install XQuartz.
dirname=packages
mkdir $HOME/$dirname 
mkdir $HOME/$dirname/calchep
cd $HOME/$dirname/calchep
wget --no-check-certificate https://theory.sinp.msu.ru/~pukhov/CALCHEP/calchep_3.6.30.tgz
tar -xvzf calchep_3.6.30.tgz
cd calchep_3.6.30
make
./mkWORKdir $HOME/$dirname/calchep/calchep-work # this will be your work directory.
cd $HOME/$dirname/calchep/calchep-work
# run it:
./calchep
# want to run calchep from anywhere in your system? 
cd
vi .bashrc # 'vi /etc/bashrc' on mac
# append the following line to the end:
export PATH="$PATH:$HOME/packages/calchep/calchep-work" # you need to modify 'packages' if you 'dirname' is different.
```

Visit Alexander Pukhov’s webpage for further information.

Notes for Mac users

Some packages are not shipped with Mac OS by default. So, you may want to install brew. As they say, “Homebrew installs the stuff you need that Apple didn’t.” For examples, it provides wget, python-dev for Mac, and gives you the more proper way using command-line interface to install packages, like we do it on Linux. To this end, run the following in terminal:

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

See Homebrew’s webpage for further information.

Now, let’s obtain wget and python:

```
brew install wget
brew install python
```

Now you can go back and install LHAPDF6 successfully (Without installing python, even some Linux distributions prompts errors) — nope, not yet. I’m still trying to figure it out.

As I stated in the class, the sed command will save a great deal in automation procedure. Although there is something called sed on Mac, it does not do the same thing as on Linux, so you may want to install it properly:

```
brew install gnused
```

But now you need to call it by gsed to use it.

To update all the packages that you installed via brew, do

```
brew update && brew upgrade `brew outdated`
```

Tutorial on how to do physics

You may start by reading these notes:

Notes on Unix commands

Notes on LanHEP (toy model and QED) and Package X (traces)

Notes on LanHEP (weak interactions, part I) and FeynArts

Notes on LanHEP (weak interactions, part II)

Notes on LanHEP (electroweak theory) (to be prepared)

Now I will provide you with some models (toy, QED, and weak). You will study them either by using a script that just gives you the result, or by following the method prescribed in the notes in the third item above. To this end, save this tar file somewhere that suits your taste, extract it, make both scripts (‘help’ and ‘prepare’) executable (chmod a+x *), and then start with ‘./help’. A user interface is the best if it does not need any explanation. So if you cannot work it out, let me know.

Last updated by K$ on 12 apr 2019.
