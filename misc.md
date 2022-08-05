## Misc

\[[__Go back__](https://kagsimsek.github.io)\]

![Ataturk](./files/img/ataturk_calisirken.jpeg)

_Science is the most reliable guide in life._ -Mustafa Kemal Ataturk

### Before Jan 14, 2022: Some links may be dead, things may be broken

* Spin matrices for any spin value (Copy the following into a Mathematica notebook and evaluate it). Play only with the s value.

```Mathematica
s = 1;
dim = 2*s + 1;
Sp = ConstantArray[0, {dim, dim}];
Sm = ConstantArray[0, {dim, dim}];
Sz = ConstantArray[0, {dim, dim}];
i = 1;
For[mp = s, mp >= -s, mp--, j = 1;
  For[m = s, m >= -s, m--, 
    Sp[[i]][[j]] = \[HBar]*Sqrt[s*(s + 1) - m*(m + 1)]*
    KroneckerDelta[mp, m + 1];
    Sz[[i]][[j]] = \[HBar]*m*KroneckerDelta[mp, m];
    Sm[[i]][[j]] = \[HBar]*Sqrt[s*(s + 1) - m*(m - 1)]*
    KroneckerDelta[mp, m - 1];
    j++;
  ];
i++;];

Sx = (Sp + Sm)/2;
Sy = (Sp - Sm)/(2*I);

Print["\!\(\*SubscriptBox[\(S\), \(x\)]\) = ", \[HBar], Sx/\[HBar] // MatrixForm]
Print["\!\(\*SubscriptBox[\(S\), \(y\)]\) = ", \[HBar], Sy/\[HBar] // MatrixForm]
Print["\!\(\*SubscriptBox[\(S\), \(z\)]\) = ", \[HBar], Sz/\[HBar] // MatrixForm]
```

* Some of my all time favorite quotes:

(see top of the page.)

_Whenever in doubt, expand in a power series._ -Enrico Fermi

_Whatever is not expressly forbidden is mandatory._ -Richard P. Feynman

_If you haven’t found something strange during the day, it hasn’t been much of a day._ -John Wheeler

_What I cannot create, I do not understand._ -Richard P. Feynman

_Practice does not make perfect. Only perfect practice makes perfect._ -Vince Lombardi

_Your priority should not be achieving in the system, but becoming independent in the system._ -Luke Smith

_That bird has no idea what he's looking at, and yet, what does the bird do? Does he panic? No, he just does the best he can._ -Terry A. Davis

_An idiot admires complexity, while a genius admires simplicity._ -Terry A. Davis

_As you begin your journey into understanding the meaning of life, the first thing that you have to take into consideration is that there have been billions and billions of people who have lived on the earth and a whole bunch of them were a lot smarter than you are and they didn't figure it out, either. So, good luck with that._ -Rodney Normal

* Quantum-mechanical harmonic oscillator: Copy the following into a Mathematica notebook and evaluate it. WF[n] will produce you the normalized nth eigenfunction of the oscillator.

```Mathematica
$Assumptions={x0>0,const>0};
P[a_]:=\[HBar]/I D[a,x];
X[a_]:=x a;
a[b_]:=Sqrt[(m \[Omega])/(2 \[HBar])](X[b]+I/(m \[Omega]) P[b]);
aDagger[b_]:=Sqrt[(m \[Omega])/(2 \[HBar])](X[b]-I/(m \[Omega]) P[b]);
\[HBar]=m \[Omega] x0^2;

LowerBound=-Infinity;
UpperBound=Infinity;

DSolve[a[f[x]]==0,f,x]//.C[1]->const;

Assuming[const>0,Solve[Integrate[f[x]^2,{x,LowerBound,UpperBound}]==1/.%,const]];

\[Psi][0]=f[x]//.%%//.%;
\[Psi][n_]:=1/Sqrt[n] aDagger[\[Psi][n-1]]//FullSimplify;
CheckNorm[n_]:=Integrate[\[Psi][n]^2,{x,LowerBound,UpperBound}];
WF[n_]:={\[Psi][n][[2]],CheckNorm[n][[2]]}[[1]];
```

* Find nth root of a single-variable transcendental equation: Let expr denote your whole expression, say Tan[x]-1/x, to be equal to 0. The numerical value of the nth root on the interval a < x < b is given by the following:

```Mathematica
N[Reduce[expr == 0 && a<x<b, x, Reals]][[n]]
```

Say you want the 5th root and want to assign to some other parameter, say y. Then do the following:

```Mathematica
y=x//.ToRules[N[Reduce[expr == 0 && a<x<b, x, Reals]][[5]]]
```

* List all possible n-tuple combinations of a list of variables: Say you want the 3-tuple combinations of 0 and 1. That is, you want (0,0,0), (0,0,1), (0,1,0), (0,1,1), and so on. Then evaluate the following:

```Mathematica
Tuples[{0,1},3]
```

Notice that this is the combinatorial arrangement. If you insist on that (0,1,0) and (0,0,1) are really the same thing, then use the Permutations function, instead:

```Mathematica
Permutations[{0,1},{3}]
```

The curly brackets around 3 means that each combo will contain exactly 3 members.

* Extract audio from video by using ffmpeg:

```Bash
ffmpeg -i video.mp4 -f mp3 -ab 192000 -vn audio.mp3
```

Source: [How Do I Extract Audio from An Mp4 File with Free and Online Ways (hitpaw.com)](https://www.google.com/url?q=https%3A%2F%2Fwww.hitpaw.com%2Faudio-tips%2Fextract-audio-from-mp4.html&sa=D&sntz=1&usg=AFQjCNEtoOJ0z_zkgUHs2UgxyhA-O4vm-w)

* Request: I have a package and I want to create a launcher on Ubuntu 18.04 + Gnome 3.28.1 and add it to the favorites OR make it visible in Show Applications. How do I do it?

Solved (at least on Unity):

(1) Open a terminal and run the following:

```Bash
vi .local/share/applications/MyApplication.desktop
```

(2) The contents should look like:

```Bash
[Desktop Entry]
Name=MyApplication
Comment=
Exec=/path/to/script
Icon=/path/to/icon.png
Terminal=false
Type=Application
StartupNotify=true
```

(3) Go to the path in the file explorer: ~/.local/share/applications

(4) Right-click on MyApplication.desktop.

(5) Select Properties.

(6) Under Permissions, click on “Allow executing file as program”.

(7) Close that window and double-click on MyApplication.desktop.

(8) If asked, select “Trust and Launch”.

(9) Right-click on the icon of your application on the dock and select “Lock to launcher”.

Source: [gnome shell - Adding custom programs to favourites of Ubuntu Dock - Ask Ubuntu](https://www.google.com/url?q=https%3A%2F%2Faskubuntu.com%2Fquestions%2F1026528%2Fadding-custom-programs-to-favourites-of-ubuntu-dock&sa=D&sntz=1&usg=AFQjCNGd_K3GpvwU38GBOlATShBDAlfQPA)

* Recover saved WiFi password: This will require you to possess root privileges.

```Bash
cd /etc/NetworkManager/system-connections ; sudo cat name | grep psk=
```

where name is the name of the network you have connected earlier in your life.

Source: [Find the password for the currently connected wireless network - Ask Ubuntu](https://www.google.com/url?q=https%3A%2F%2Faskubuntu.com%2Fquestions%2F156861%2Ffind-the-password-for-the-currently-connected-wireless-network&sa=D&sntz=1&usg=AFQjCNF_J2IfYTZXvFRIE8OSA1NW72eDHQ)

* Completely wipe a flash drive on linux, and make it a bootable disk:

Connect your flash drive to one of the usb hubs on your computer.

Open a new terminal window.

You may want to install the package Pipe Viewer to monitor your progress. Run sudo apt install pv. (If you are using a linux distro other than Ubuntu, please google how to install the package pv since it heavily depends on your package manager.)

Run lsblk to make sure that it is accessible by your computer. You should see some sdX with a mountpoint /media/something. The total size of sdX should be close to the exact size on your flash drive. You should note that X can be equal to say b or c, and so on. I will continue calling it X but in what follows you should adjust it accordingly.

Now let’s fill your flash drive with zeroes. Assuming your flash drive is N GB where conventionally N is equal to 8, 16, 32, 64, etc., run `sudo dd if=/dev/zero | pv -s NG | sudo dd of=/dev/sdX bs=4M && sync`.

Now your flash drive is empty as can be. Let’s format it properly. Run sudo fdisk /dev/sdX. You will be asked to enter some commands. Press o first and n next. You will be given some options afterwards. Choose the default always. When you are asked to enter a new command, type and enter w. Finally run sudo mkfs.vfat /dev/sdX1.

Now you are ready to burn the image of a linux distro onto your flash drive. Assuming you have the .iso file in your Downloads folder under home directory, run `sudo umount /dev/sdX1 ; sudo dd if=$HOME/Downloads/some_linux_distro.iso | pv -s MG | sudo dd of=/dev/sdX1 bs=4M && sync` where M is the smallest integer larger than the size of the .iso file in units of GB.

For example, for a 8-GB flash drive that appears to have the label sdb and that has to be burned with ubuntu-16.04.5-desktop-amd64.iso which is located in Downloads under home, do the following:

```Bash
sudo apt install pv
sudo dd if=/dev/zero | pv -s 8G | sudo dd of=/dev/sdb bs=4M && sync
sudo fdisk /dev/sdb # press o, n, and choose default, and then w
sudo mkfs.vfat /dev/sdb1
sudo umount /dev/sdb1
sudo dd if=$HOME/Downloads/ubuntu-16.04.4-desktop-amd64.iso | pv -s 2G | sudo dd of=/dev/sdb1 bs=4M && sync
```

* How to setup a GitHub account and connect your local machine to your GitHub account on the GitHub server (I have used so many “GitHub”s in one sentence, I know.):

i. Open a web browser.

ii. Go to github.com.

iii. Sign up. Note down your_username and your_email.

iv. Check your email to verify your account.

v. Open a terminal and run the following:

```Bash
git config --global user.name "your_username" # do not omit the double quotes
git config --global user.email "your_email" # do not omit the double quotes
git config --global core.editor vim # this is optional
```

vi. Now we will generate a new SSH key and associate it to your GitHub account. Run the following:

```Bash
ssh-keygen -t rsa -b 4096 -C "your_email" # do not omit the double quotes
```

When prompted with “Enter a file in which to save the key (/home/username/.ssh/id_rsa):)”, press Enter. When prompted with “Enter passphrase (empty for no passphrase)”, enter a password-like thing. It should be of length at least 5 characters. It may be different from your GitHub password. Do not forget which is which, in that case.

vii. Run the following:

```Bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
xdg-open ~/.ssh/id_rsa.pub
```

viii. Copy the contents.

ix. Open a web browser.

x. Go to github.com.

xi. Log in.

xii. Click on your profile pic on the top right corner.

xiii. Click on Settings.

xiv. In the menu on the left, click on SSH and GPG keys.

xv. Click on New SSH key.

xvi. In the Title field, write your computer’s name. It is meant to differ from your other machines.

xvii. Click on the Key field and paste.

xviii. Click on Add SSH key.

If you have multiple machines, repeat the same procedure for each computer, starting from step v.

* Copy files/folders to/from your server account:

To copy your local files or folders to your server account: Run the following in a terminal on your local machine. (Depending on the case, it may require you to type and enter your user password.)

```Bash
scp -rp file1 file2 folder1 user@server:/path/to/folder/
```

where you should replace user and server, accordingly.

To copy files or folder from your server account to your local machine: Run the following in a terminal on your local machine. (Depending on the case, it may require you to type and enter your user password.)

```Bash
scp -rp user@server:/path/to/file /path/to/folder/
```

where you should replace user and server, accordingly. 

* As a linux enthusiast, I love trying different distros from time to time; nevertheless, I always end up having my work station on some flavor of Ubuntu. Below is my protocol for post-installing a fresh new Ubuntu and some useful packages.

– Update the system:

```Bash
sudo apt update && sudo apt upgrade -y && sudo apt dist-upgrade -y && sudo apt autoremove -y
```

– Modify .bashrc for a fresh look:

```Bash
cd ; cp .bashrc .bashrc.orig ; wget https://www.dropbox.com/s/teixsa8ykrk3h8a/bashrc.txt ; mv bashrc.txt .bashrc ; . .bashrc
```

– Install some useful packages:

```Bash
sudo apt install -y vim make gcc gfortran g++ htop ffmpeg gnuplot meld gv pv texlive-full python-dev p7zip-full p7zip-rar build-essential
```

– Install Mathematica and activate (necessary for HEP tools).

– Install HEP tools (see Tutorials).

– Install TeXStudio from official website.

– Install one of the most user-friendly writing app ever:

```Bash
cd ; cd packages ; mkdir write ; cd write ; wget http://www.styluslabs.com/download/write-tgz ; tar -xvzf write* ; sudo apt install libqt5widgets5 libqt5network5 libqt5svg5
```

– Install and configure other apps (web browser, email client, etc.).

... This didn't age well. For the past three years (as of June 2021), I've been a loyal SUSE user --- much more stable and complete than Ubuntu. I think Ubuntu is overrated, just like Macs (or any other Apple product). So, here is my todo after a fresh install of openSUSE:

```Bash
sudo zypper refresh && sudo zypper -n update
sudo zypper install -t pattern devel_basis
sudo zypper install vim make gcc gcc-fortran gcc-c++ htop ffmpeg gnuplot meld gv pv texlive-scheme-full texlive-collection-latex python-devel
```

The rest is the same as above.

* Sometimes, you visit your local computer store, check out the price of a Mac, and inquire about the processor info. If you are lucky, the attendant will say “it is the brand new processor” without even referring to the brand of the processor. To check out the processor info of a Mac, run the following:

```Bash
sysctl -n machdep.cpu.brand_string
```

You may even surprise the attendant with your level of sophistication.

* Some basic commands for Arch-based distros:

```Bash
sudo pacman -Syy # update database
sudo pacman -Syu # update system, always run before installing packages
sudo pacman -S package # install the package package
```

Partial list of equivalent packages between Debian- and Arch-based distros (deb = arch) (Useful for HEP tools):

```
gcc = gcc
gfortran = gcc-fortran
g++ = gcc
libx11-dev = libx11
```

to be continued when necessary.

* Say you have gone into a series of folders inside folders, but suddenly you feel you need to go back to home and do something there and come back, but you are too lazy to copy the path (I can’t imagine how, though). Here is a little code to help you:

```Bash
echo "alias cpdir='echo \$(pwd) > \$HOME/.mytmpdir'" >> $HOME/.bashrc
echo "alias cddir='cd \$(cat \$HOME/.mytmpdir)'" >> $HOME/.bashrc
source $HOME/.bashrc
```

Here, cpdir copies your current directory into a hidden file .mytmpdir in your home folder, and cddir changes directory to the last copied path. If you don’t want this hidden file in your home directory, modify the second line to look like

```Bash
echo "alias cddir='cd \$(cat \$HOME/.mytmpdir) && rm \$HOME/.mytmpdir'" >> $HOME/.bashrc
```

but you won’t be able to change to this directory unless you run cpdir again.

* Griffiths has a nice font in his particle physics book. The closest thing to that font can be achieved by adding \usepackage{mathpazo} to your preamble in your tex file.

* Add string to the beginning of each line of file:

```Bash
sed -i 's/^/string/g' file
```

Replace the last character of each line of file with string:

```Bash
sed -i 's/.$/string/g' file
```

^ denotes the first character and $ the last. The dot before $ means whatever there is.

This is useful for instance when you have a list of student numbers 1234567 line after line and you need to put e to the front and replace the 7 at the end by @metu.edu.tr to create a mailing list. If you have lots of sections or classes or whatever that contains such list of student numbers, just go to the directory that contain your text files and run the following:

```Bash
for f in *
do
  sed -i 's/^/e/g' $f
  sed -i 's/.$/@metu.edu.tr/g' $f
done
```

and you are done.

* I have prepared a to-do list terminal application, called ‘todo’. Obtain [here](https://www.google.com/url?q=https%3A%2F%2Fwww.dropbox.com%2Fs%2Ffh2iciuf4dodo1b%2Ftodo%3Fdl%3D1&sa=D&sntz=1&usg=AFQjCNGISG1qOIF1fs78S4pgGNepTL71-A) and try it by running

```Bash
chmod a+x todo
./todo
```

You will be guided. You may improve it if you want. For linux users, it should work right away, whilst for mac users I require you to install brew and then gnu-sed via brew (see Tutorials).

As in v0.2.1, the complete overview of what you can do:

It is platform-independent — the default save location is in your Dropbox folder (if it exists) and you can run it on linux or mac.

Add single-word item.

Add single item with multiple words (no quotation mark is needed).

Check item as done.

Check all items as done.

Uncheck item.

Uncheck all items.

Remove single or multiple items.

Remove items containing a common word or words.

Modify source code.

File a bug report.

Extract item list or bug report as a PDF via LaTeX.

The source code is updateable.

Create multiple classes of activities (couldn’t fully figure out the space character yet).

Use verbatim mode (anything you type between :b and e: will be printed in verbatim).

* Create an .m file for mathematica: Suppose you have lost of functions to be used on multiple notebooks extensively. Instead of copying all of them into all the notebooks, you might as well create an .m file as a source. To achieve this,

(1) Open a terminal, go to the directory where you want to save the .m file, open vim an save your functions or anything that you want to use as predefined. Suppose that directory is ‘/home/username/Documents/base.m’ (or /Users/username/Documents/base.m on mac) where you should replace username accordingly.

(2) Open a mathematica notebook and run the following:

```Mathematica
SetDirectory["/home/username/Documents"]
```

(3) Now you should be able read your functions or any predefined equations from the base file by running

```Mathematica
<<base.m
```

That’s it.

* From time to time, we take quick notes on vi or some other package by using the terminal. I have a script that converts your note (with no equations, I presume) into a minimal pdf file via pdflatex. Obtain it from [this link](https://www.google.com/url?q=https%3A%2F%2Fwww.dropbox.com%2Fs%2F0frowmbi9xvflvm%2Fminimal-tex%3Fdl%3D1&sa=D&sntz=1&usg=AFQjCNG-Cm4XDRqzMdhwPzFeOsnvg207BA), move the script to a directory that suits your taste, and cd into that directory. After that, run the following:

```Bash
chmod a+x minimal-tex
echo "PATH=$(pwd):\$PATH" >> $HOME/.bashrc
. $HOME/.bashrc
```

so that you can run it anywhere on your system. The usage is as follows. (First of all, if you are on a linux machine, open the source code and change gsed to sed and open to xdg-open.) Say you create a miniature text file in your home folder and named it quick_note:

```Bash
cd
minimal-tex quick_note
```

and you should see your pdf file right away.

* I don’t know how useful the following will be but I have this mini code that will print the symbols `– \ | / –` in sequence:

```Bash
while true; do echo -ne "-" ; printf "\r" ; sleep .25 ; echo -ne "\\" ; printf "\r" ; sleep .25 ; echo -ne "|" ; printf "\r" ; sleep .25 ; echo -ne "/" ; printf "\r" ; sleep .25 ; done
```

For instance, when you have a script that installs some stuff for you, you may add this somewhere indicating the code is working but waiting or whatever.

* Say you have some files on your local machine, and you occasionally want to backup some folders to a server (or you can do it for a backup folder on your local machine, again). Here is how to do:

```Bash
rsync -avu /path/to/source/ /path/to/destination
```

Notice the slash at the end of source folder. If it is missing, there will be a folder inside the destination path. Be careful. Or not, I’m not a cop or something.

If in the source path you remove some files, and if you want the destination folder also remove the same files, add the –delete flag:

```Bash
rsync -avu --delete /path/to/source/ /path/to/destination
```

You may connect to your server by making the following changes:

```Bash
rsync -avu /path/to/source/ user@server:/path/to/destination
```

Do not forget to adjust user and server accordingly.

Source: [rsync(1) - Linux man page (die.net)](https://www.google.com/url?q=https%3A%2F%2Flinux.die.net%2Fman%2F1%2Frsync&sa=D&sntz=1&usg=AFQjCNH2H3_7tkFrENrV3TwH6myXD1i1wA)

* Connect to server by using an SSH key instead of your user password on the server: (Note that this is safer than removing your user password on the server. Note also that you need to define your SSH key on every machine you have; that is, if you have one desktop and one laptop, then you need to repeat the following procedure for both.) Open a terminal and run the following.

```Bash
ssh-keygen
```

You will be asked three questions. Press Return (leave all the questions empty) for all of them. Now you have generated an SSH key. The path should look like ‘/home/user/.ssh/id_rsa.pub’ on linux and ‘/Users/user/.ssh/id_rsa.pub’ on mac (where user is your username). Next, you need to let the server know of your SSH key:

```Bash
ssh-copy-id -i $HOME/.ssh/id_rsa.pub username@server
```

Here, username is your username on the server, and server is simply your server name. Now you should be able to connect your server without entering a password:

```Bash
ssh username@server
```

This is useful for instance when you want to backup lots of folder from your local machine to the server. (See the previous item.)

Source: [How to use SSH keys for authentication - Tutorial - UpCloud](https://www.google.com/url?q=https%3A%2F%2Fupcloud.com%2Fcommunity%2Ftutorials%2Fuse-ssh-keys-authentication%2F&sa=D&sntz=1&usg=AFQjCNEKE4__DvjdX65r5Lwq7Zg5RrM1hg)

* Display the last line of a file:

```Bash
tail -l file
```

This should work on both linux and mac.

* Useful LaTeX tips:

Remove paragraph indentation for the whole document: Add the following to your preamble (anywhere before ‘\begin{document}’)

```LaTeX
\setlength\parindent{0pt}
```

To be continued.

* Remove parentheses and comma from python2 output: Append

```Python
from __future__ import print_function
```

to the beginning of your file.

* Command-line solution to the mirroring monitors between a Linux machine and an external monitor (HDMI or DVI):

Unplug the external monitor.

Now plug back.

Connect the HDMI or DVI cable between the two devices.

Run xrandr –query to list all the connected monitors: If you have an monitor of brand X, then you should see it right there with the label m-1 or m-2 where m might be HDMI or DVI.

Run xrandr –output HDMI-1-2 –off –output DVI-1-2 –off to shutdown all the external monitors.

Finally, run xrandr –output m–n –auto to enable the desired monitor where n equals 1 or 2, e.g. you may run xrandr –output HDMI-2 –auto; nevertheless, in some cases you don’t have the dash in between the monitor label.

(All the single dashes in front of query, output, off, and auto should have been double.)

* Check your current clock speed in units of MHz:

```Bash
lscpu | grep MHz
```

Source: [cpu - Any way to check the clock speed of my processor? - Ask Ubuntu](https://www.google.com/url?q=https%3A%2F%2Faskubuntu.com%2Fquestions%2F218567%2Fany-way-to-check-the-clock-speed-of-my-processor&sa=D&sntz=1&usg=AFQjCNHc3g6XbnzjjbEwSwcG4rmMT0KrSQ)

* Print a character, say = symbol, N times:

```Bash
N=15
printf "%${N}s\n" | tr " " "="
```

This might be useful if you want to design a script that will print the remaining battery life in terminal: Let’s do it together.

Get the remaining battery percentage into a hidden file, say .battery.info in your home folder:

```Bash
upower -i /org/freedesktop/UPower/devices/battery_BAT0 | grep percentage > $HOME/.battery.info
```

The output will look like “percentage: 73%”. Get the last three characters of this line:

```Bash
grep -o '...
```

Now let’s also get rid of the percentage symbol:

```Bash
sed -i 's/.$//g' $HOME/.tmp.info
```

Assign N to this number:

```Bash
N=$(cat $HOME/.tmp.info)
```

Let’s compute the rest of the 100%:

```Bash
M=$((100-N))
```

Now print the line:

```Bash
printf [ && printf "%${N}s" | tr " " "|" && printf "%${M}s" | tr " " " " && printf ]
```

The output will look like: `[||||||||||||||||||||||||||                  ]`

You may spice it up a little more by adding colors.

A minimal working example can be found [here](https://www.google.com/url?q=https%3A%2F%2Fwww.dropbox.com%2Fs%2F1cqeigxvffstlqc%2Fst%3Fdl%3D1&sa=D&sntz=1&usg=AFQjCNHqwA7IFO3hTlxD5r6N1Omvw-M0Yw). Download it, make it executable (chmod a+x st), and run it (./st).

* Bash color codes:

```
\e[0;30m # Black – Regular
\e[0;31m # Red
\e[0;32m # Green
\e[0;33m # Yellow
\e[0;34m # Blue
\e[0;35m # Purple
\e[0;36m # Cyan
\e[0;37m # White
\e[1;30m # Black – Bold
\e[1;31m # Red
\e[1;32m # Green
\e[1;33m # Yellow
\e[1;34m # Blue
\e[1;35m # Purple
\e[1;36m # Cyan
\e[1;37m # White
\e[4;30m # Black – Underline
\e[4;31m # Red
\e[4;32m # Green
\e[4;33m # Yellow
\e[4;34m # Blue
\e[4;35m # Purple
\e[4;36m # Cyan
\e[4;37m # White
\e[40m # Black – Background
\e[41m # Red
\e[42m # Green
\e[43m # Yellow
\e[44m # Blue
\e[45m # Purple
\e[46m # Cyan
\e[47m # White
\e[0m # Text Reset
```

Usage: Let us print a red ‘Hello World’:

```Bash
printf '\e[0;31mHello World\e[m'
```

Make it useful.

Source: [bash - What color codes can I use in my PS1 prompt? - Unix & Linux Stack Exchange](https://www.google.com/url?q=https%3A%2F%2Funix.stackexchange.com%2Fquestions%2F124407%2Fwhat-color-codes-can-i-use-in-my-ps1-prompt&sa=D&sntz=1&usg=AFQjCNFknoxxw6WaPQoFnvfrnPDcyJrjPg)

* For those who want to run two Mathematica scripts but are not quite sure if there will be kernel problems (like interference due to shared variables), NO, they will be different instances of the same kernel, therefore you may run simultaneous scripts at once. (I noticed this two months before finishing my MS thesis... sigh...)

* Mathematica does not start up on xUbuntu 19.04 due to a font problem. To solve this, run

```Bash
cd /usr/local/Wolfram/Mathematica/11.3/SystemFiles/Libraries/Linux-x86-64
sudo mv libfreetype.so.6 libfreetype.so.6.bak
sudo mv libz.so.1 libz.so.1.bak
```

if you installed Mathematica in the default path.

Source: [fonts - Wolfram Mathematica after upgrade to Ubuntu 19.04: symbol lookup error: /usr/lib/x86_64-linux-gnu/libfontconfig.so.1: undefined symbol: FT_Done_MM_Var - Ask Ubuntu](https://www.google.com/url?q=https%3A%2F%2Faskubuntu.com%2Fquestions%2F1140921%2Fwolfram-mathematica-after-upgrade-to-ubuntu-19-04-symbol-lookup-error-usr-lib&sa=D&sntz=1&usg=AFQjCNF5vOWfiothm9DFA0Zbscy1gxE-9A)

* If you create your own .sty file, or if you need a .sty file that is not included in your TeX distribution (say TeXLive) and you don't know where to put it, do the following:

```Bash
kpsewhich -var-value=TEXMFHOME
```

It should return something like /home/username/texmf (which was my case). You may notice that this path is absent. Then,

```Bash
mkdir texmf
mkdir texmf/tex
mkdir texmf/tex/latex
mkdir texmf/tex/latex/local
```

and put your .sty file in local here.

* Get a nice enough looking dark theme for texstudio: Save your work and close any instances of texstudio.

(1) Open the init file for texstudio:

```Bash
vi $HOME/.config/texstudio/texstudio.ini
```

(2) Find the following four lines:

```
[format]
version=1.0

[texmaker]
```

(3) Append the following at the third line above.

```
data\align-ampersand\bold=true
data\align-ampersand\fontFamily=
data\align-ampersand\foreground=#b5d1df
data\align-ampersand\italic=false
data\align-ampersand\overline=false
data\align-ampersand\pointSize=0
data\align-ampersand\priority=-1
data\align-ampersand\strikeout=false
data\align-ampersand\underline=false
data\align-ampersand\waveUnderline=false
data\align-ampersand\wrapAround=false
data\background\background=#26292c
data\background\bold=false
data\background\fontFamily=
data\background\italic=false
data\background\overline=false
data\background\pointSize=0
data\background\priority=-1
data\background\strikeout=false
data\background\underline=false
data\background\waveUnderline=false
data\background\wrapAround=false
data\braceMatch\background=#2b2b2b
data\braceMatch\bold=tru
data\braceMatch\fontFamily=
data\braceMatch\foreground=#b5d1df
data\braceMatch\italic=false
data\braceMatch\overline=false
data\braceMatch\pointSize=0
data\braceMatch\priority=-1
data\braceMatch\strikeout=false
data\braceMatch\underline=false
data\braceMatch\waveUnderline=false
data\braceMatch\wrapAround=false
data\braceMismatch\background=#b5d1df
data\braceMismatch\bold=true
data\braceMismatch\fontFamily=
data\braceMismatch\foreground=#2b2b2b
data\braceMismatch\italic=false
data\braceMismatch\overline=false
data\braceMismatch\pointSize=0
data\braceMismatch\priority=-1
data\braceMismatch\strikeout=false
data\braceMismatch\underline=false
data\braceMismatch\waveUnderline=false
data\braceMismatch\wrapAround=false
data\citationMissing\bold=true
data\citationMissing\fontFamily=
data\citationMissing\foreground=#b5d1df
data\citationMissing\italic=false
data\citationMissing\overline=false
data\citationMissing\pointSize=0
data\citationMissing\priority=-1
data\citationMissing\strikeout=false
data\citationMissing\underline=false
data\citationMissing\waveUnderline=true
data\citationMissing\wrapAround=false
data\citationPresent\bold=true
data\citationPresent\fontFamily=
data\citationPresent\foreground=#b5d1df
data\citationPresent\italic=false
data\citationPresent\overline=false
data\citationPresent\pointSize=0
data\citationPresent\priority=-1
data\citationPresent\strikeout=false
data\citationPresent\underline=false
data\citationPresent\waveUnderline=false
data\citationPresent\wrapAround=false
data\comment\bold=false
data\comment\fontFamily=
data\comment\foreground=#767f85
data\comment\italic=false
data\comment\overline=false
data\comment\pointSize=0
data\comment\priority=-1
data\comment\strikeout=false
data\comment\underline=false
data\comment\waveUnderline=false
data\comment\wrapAround=false
data\commentTodo\background=#5f7f5f
data\commentTodo\bold=false
data\commentTodo\fontFamily=
data\commentTodo\foreground=#ffffef
data\commentTodo\italic=false
data\commentTodo\overline=false
data\commentTodo\pointSize=0
data\commentTodo\priority=-1
data\commentTodo\strikeout=false
data\commentTodo\underline=false
data\commentTodo\waveUnderline=false
data\commentTodo\wrapAround=false
data\current\background=#4d4d4d
data\current\bold=false
data\current\fontFamily=
data\current\foreground=#ffffff
data\current\italic=false
data\current\overline=false
data\current\pointSize=0
data\current\priority=-1
data\current\strikeout=false
data\current\underline=false
data\current\waveUnderline=false
data\current\wrapAround=false
data\environment\bold=false
data\environment\fontFamily=
data\environment\foreground=#d88746
data\environment\italic=false
data\environment\overline=false
data\environment\pointSize=0
data\environment\priority=-1
data\environment\strikeout=false
data\environment\underline=false
data\environment\waveUnderline=false
data\environment\wrapAround=false
data\escapeseq\bold=false
data\escapeseq\fontFamily=
data\escapeseq\italic=false
data\escapeseq\overline=false
data\escapeseq\pointSize=0
data\escapeseq\priority=-1
data\escapeseq\strikeout=false
data\escapeseq\underline=false
data\escapeseq\waveUnderline=false
data\escapeseq\wrapAround=false
data\extra-keyword\bold=true
data\extra-keyword\fontFamily=
data\extra-keyword\foreground=#ffb454
data\extra-keyword\italic=false
data\extra-keyword\overline=false
data\extra-keyword\pointSize=0
data\extra-keyword\priority=-1
data\extra-keyword\strikeout=false
data\extra-keyword\underline=false
data\extra-keyword\waveUnderline=false
data\extra-keyword\wrapAround=false
data\grammarMistakeSpecial1\bold=false
data\grammarMistakeSpecial1\fontFamily=
data\grammarMistakeSpecial1\italic=false
data\grammarMistakeSpecial1\overline=false
data\grammarMistakeSpecial1\pointSize=0
data\grammarMistakeSpecial1\priority=-1
data\grammarMistakeSpecial1\strikeout=false
data\grammarMistakeSpecial1\underline=false
data\grammarMistakeSpecial1\waveUnderline=false
data\grammarMistakeSpecial1\wrapAround=fale
data\grammarMistakeSpecial2\bold=false
data\grammarMistakeSpecial2\fontFamily=
data\grammarMistakeSpecial2\italic=false
data\grammarMistakeSpecial2\overline=false
data\grammarMistakeSpecial2\pointSize=0
data\grammarMistakeSpecial2\priority=-1
data\grammarMistakeSpecial2\strikeout=false
data\grammarMistakeSpecial2\underline=false
data\grammarMistakeSpecial2\waveUnderline=false
data\grammarMistakeSpecial2\wrapAround=false
data\grammarMistakeSpecial3\bold=false
data\grammarMistakeSpecial3\fontFamily=
data\grammarMistakeSpecial3\italic=false
data\grammarMistakeSpecial3\overline=false
data\grammarMistakeSpecial3\pointSize=0
data\grammarMistakeSpecial3\priority=-1
data\grammarMistakeSpecial3\strikeout=false
data\grammarMistakeSpecial3\underline=false
data\grammarMistakeSpecial3\waveUnderline=false
data\grammarMistakeSpecial3\wrapAround=false
data\grammarMistakeSpecial4\bold=false
data\grammarMistakeSpecial4\fontFamily=
data\grammarMistakeSpecial4\italic=false
data\grammarMistakeSpecial4\overline=false
data\grammarMistakeSpecial4\pointSize=0
data\grammarMistakeSpecial4\priority=-1
data\grammarMistakeSpecial4\strikeout=false
data\grammarMistakeSpecial4\underline=false
data\grammarMistakeSpecial4\waveUnderline=false
data\grammarMistakeSpecial4\wrapAround=false
data\keyword\bold=true
data\keyword\fontFamily=
data\keyword\foreground=#d88746
data\keyword\italic=false
data\keyword\overline=false
data\keyword\pointSize=0
data\keyword\priority=-1
data\keyword\strikeout=false
data\keyword\underline=false
data\keyword\waveUnderline=false
data\keyword\wrapAround=false
data\latexSyntaxMistake\bold=false
data\latexSyntaxMistake\fontFamily=
data\latexSyntaxMistake\italic=false
data\latexSyntaxMistake\linescolor=#dfaf8f
data\latexSyntaxMistake\overline=false
data\latexSyntaxMistake\pointSize=0
data\latexSyntaxMistake\priority=-1
data\latexSyntaxMistake\strikeout=false
data\latexSyntaxMistake\underline=false
data\latexSyntaxMistake\waveUnderline=false
data\latexSyntaxMistake\wrapAround=false
data\line%3Abadbox\background=#767f85
data\line%3Abadbox\bold=false
data\line%3Abadbox\fontFamily=
data\line%3Abadbox\italic=false
data\line%3Abadbox\overline=false
data\line%3Abadbox\pointSize=0
data\line%3Abadbox\priority=-1
data\line%3Abadbox\strikeout=false
data\line%3Abadbox\underline=false
data\line%3Abadbox\waveUnderline=false
data\line%3Abadbox\wrapAround=false
data\line%3Aerror\background=#767f85
data\line%3Aerror\bold=true
data\line%3Aerror\fontFamily=
data\line%3Aerror\italic=true
data\line%3Aerror\overline=false
data\line%3Aerror\pointSize=0
data\line%3Aerror\priority=-1
data\line%3Aerror\strikeout=false
data\line%3Aerror\underline=false
data\line%3Aerror\waveUnderline=false
data\line%3Aerror\wrapAround=false
data\line%3Awarning\background=#767f85
data\line%3Awarning\bold=true
data\line%3Awarning\fontFamily=
data\line%3Awarning\italic=true
data\line%3Awarning\overline=false
data\line%3Awarning\pointSize=0
data\line%3Awarning\priority=-1
data\line%3Awarning\strikeout=false
data\line%3Awarning\underline=false
data\line%3Awarning\waveUnderline=false
data\line%3Awarning\wrapAround=false
data\link\bold=false
data\link\fontFamily=
data\link\italic=false
data\link\overline=false
data\link\pointSize=0
data\link\priority=-1
data\link\strikeout=false
data\link\underline=true
data\link\waveUnderline=false
data\link\wrapAround=false
data\magicComment\bold=false
data\magicComment\fontFamily=
data\magicComment\foreground=#9fabb0
data\magicComment\italic=false
data\magicComment\overline=false
data\magicComment\pointSize=0
data\magicComment\priority=-1
data\magicComment\strikeout=false
data\magicComment\underline=false
data\magicComment\waveUnderline=false
data\magicComment\wrapAround=false
data\math-delimiter\bold=true
data\math-delimiter\fontFamily=
data\math-delimiter\foreground=#72aaca
data\math-delimiter\italic=false
data\math-delimiter\overline=false
data\math-delimiter\pointSize=0
data\math-delimiter\priority=-1
data\math-delimiter\strikeout=false
data\math-delimiter\underline=false
data\math-delimiter\waveUnderline=false
data\math-delimiter\wrapAround=false
data\math-keyword\bold=true
data\math-keyword\fontFamily=
data\math-keyword\foreground=#b7d877
data\math-keyword\italic=false
data\math-keyword\overline=false
data\math-keyword\pointSize=0
data\math-keyword\priority=-1
data\math-keyword\strikeout=false
data\math-keyword\underline=false
data\math-keyword\waveUnderline=false
data\math-keyword\wrapAround=false
data\normal\bold=false
data\normal\fontFamily=
data\normal\foreground=#eaeaea
data\normal\italic=false
data\normal\overline=false
data\normal\pointSize=0
data\normal\priority=-1
data\normal\strikeout=false
data\normal\underline=false
data\normal\waveUnderline=false
data\normal\wrapAround=false
data\numbers\bold=false
data\numbers\fontFamily=
data\numbers\foreground=#b7d877
data\numbers\italic=false
data\numbers\overline=false
data\numbers\pointSize=0
data\numbers\priority=-1
data\numbers\strikeout=false
data\numbers\underline=false
data\numbers\waveUnderline=false
data\numbers\wrapAround=false
data\packageMissing\bold=false
data\packageMissing\fontFamily=
data\packageMissing\foreground=#b5d1df
data\packageMissing\italic=false
data\packageMissing\overline=false
data\packageMissing\pointSize=0
data\packageMissing\priority=-1
data\packageMissing\strikeout=false
data\packageMissing\underline=false
data\packageMissing\waveUnderline=true
data\packageMissing\wrapAround=false
data\packagePresent\bold=false
data\packagePresent\fontFamily=
data\packagePresent\foreground=#b5d1df
data\packagePresent\italic=false
data\packagePresent\overline=false
data\packagePresent\pointSize=0
data\packagePresent\priority=-1
data\packagePresent\strikeout=false
data\packagePresent\underline=false
data\packagePresent\waveUnderline=false
data\packagePresent\wrapAround=false
data\picture-keyword\bold=false
data\picture-keyword\fontFamily=
data\picture-keyword\foreground=#ffb454
data\picture-keyword\italic=false
data\picture-keyword\overline=false
data\picture-keyword\pointSize=0
data\picture-keyword\priority=-1
data\picture-keyword\strikeout=false
data\picture-keyword\underline=false
data\picture-keyword\waveUnderline=false
data\picture-keyword\wrapAround=false
data\picture\bold=false
data\picture\fontFamily=
data\picture\foreground=#ece8c4
data\picture\italic=false
data\picture\overline=false
data\picture\pointSize=0
data\picture\priority=-1
data\picture\strikeout=false
data\picture\underline=false
data\picture\waveUnderline=false
data\picture\wrapAround=false
data\previewSelection\background=#aaffaa
data\previewSelection\bold=false
data\previewSelection\fontFamily=
data\previewSelection\italic=false
data\previewSelection\overline=false
data\previewSelection\pointSize=0
data\previewSelection\priority=-1
data\previewSelection\strikeout=false
data\previewSelection\underline=false
data\previewSelection\waveUnderline=false
data\previewSelection\wrapAround=true
data\referenceMissing\bold=false
data\referenceMissing\fontFamily=
data\referenceMissing\foreground=#b5d1df
data\referenceMissing\italic=false
data\referenceMissing\overline=false
data\referenceMissing\pointSize=0
data\referenceMissing\priority=-1
data\referenceMissing\strikeout=false
data\referenceMissing\underline=false
data\referenceMissing\waveUnderline=true
data\referenceMissing\wrapAround=false
data\referenceMultiple\bold=false
data\referenceMultiple\fontFamily=
data\referenceMultiple\foreground=#40677f
data\referenceMultiple\italic=false
data\referenceMultiple\overline=false
data\referenceMultiple\pointSize=0
data\referenceMultiple\priority=-1
data\referenceMultiple\strikeout=false
data\referenceMultiple\underline=false
data\referenceMultiple\waveUnderline=true
data\referenceMultiple\wrapAround=false
data\referencePresent\bold=true
data\referencePresent\fontFamily=
data\referencePresent\foreground=#b5d1df
data\referencePresent\italic=false
data\referencePresent\overline=false
data\referencePresent\pointSize=0
data\referencePresent\priority=-1
data\referencePresent\strikeout=false
data\referencePresent\underline=false
data\referencePresent\waveUnderline=false
data\referencePresent\wrapAround=false
data\search\background=#ffb454
data\search\bold=false
data\search\fontFamily=
data\search\foreground=#000000
data\search\italic=false
data\search\overline=false
data\search\pointSize=0
data\search\priority=-1
data\search\strikeout=false
data\search\underline=false
data\search\waveUnderline=false
data\search\wrapAround=false
data\spellingMistake\bold=false
data\spellingMistake\fontFamily=
data\spellingMistake\italic=false
data\spellingMistake\linescolor=#dfaf8f
data\spellingMistake\overline=false
data\spellingMistake\pointSize=0
data\spellingMistake\priority=-1
data\spellingMistake\strikeout=false
data\spellingMistake\underline=false
data\spellingMistake\waveUnderline=true
data\spellingMistake\wrapAround=false
data\structure\bold=true
data\structure\fontFamily=
data\structure\foreground=#72aaca
data\structure\italic=false
data\structure\overline=false
data\structure\pointSize=0
data\structure\priority=-1
data\structure\strikeout=false
data\structure\underline=false
data\structure\waveUnderline=false
data\structure\wrapAround=false
data\temporaryCodeCompletion\bold=false
data\temporaryCodeCompletion\fontFamily=
data\temporaryCodeCompletion\foreground=#94af64
data\temporaryCodeCompletion\italic=true
data\temporaryCodeCompletion\overline=false
data\temporaryCodeCompletion\pointSize=0
data\temporaryCodeCompletion\priority=-1
data\temporaryCodeCompletion\strikeout=false
data\temporaryCodeCompletion\underline=false
data\temporaryCodeCompletion\waveUnderline=false
data\temporaryCodeCompletion\wrapAround=false
data\text\bold=false
data\text\fontFamily=
data\text\foreground=#b7d877
data\text\italic=false
data\text\overline=false
data\text\pointSize=0
data\text\priority=-1
data\text\strikeout=false
data\text\underline=false
data\text\waveUnderline=false
data\text\wrapAround=false
data\verbatim\bold=false
data\verbatim\fontFamily=
data\verbatim\italic=false
data\verbatim\overline=false
data\verbatim\pointSize=0
data\verbatim\priority=-1
data\verbatim\strikeout=false
data\verbatim\underline=false
data\verbatim\waveUnderline=false
data\verbatim\wrapAround=false
data\wordRepetition\bold=false
data\wordRepetition\fontFamily=
data\wordRepetition\italic=false
data\wordRepetition\linescolor=#dc8cc3
data\wordRepetition\overline=false
data\wordRepetition\pointSize=0
data\wordRepetition\priority=-1
data\wordRepetition\strikeout=false
data\wordRepetition\underline=false
data\wordRepetition\waveUnderline=true
data\wordRepetition\wrapAround=false
data\wordRepetitionLongRange\bold=false
data\wordRepetitionLongRange\fontFamily=
data\wordRepetitionLongRange\italic=false
data\wordRepetitionLongRange\linescolor=#dc8cc3
data\wordRepetitionLongRange\overline=false
data\wordRepetitionLongRange\pointSize=0
data\wordRepetitionLongRange\priority=-1
data\wordRepetitionLongRange\strikeout=false
data\wordRepetitionLongRange\underline=false
data\wordRepetitionLongRange\waveUnderline=true
data\wordRepetitionLongRange\wrapAround=false
```

(4) Save and exit.

Source: [texmaker - How can I set a dark theme in TeXstudio? - TeX - LaTeX Stack Exchange](https://www.google.com/url?q=https%3A%2F%2Ftex.stackexchange.com%2Fquestions%2F108315%2Fhow-can-i-set-a-dark-theme-in-texstudio&sa=D&sntz=1&usg=AFQjCNHwjUzFIbm6CVDupICsq7XGQMjPHw)

* Want to define new keyboards shortcuts for Home and End? You may need this if you have your original Home and End keys positioned strangely, for instance in the keyboard of ThinkPad X220. I wanted to use Fn -> for End and Fn <- for Home due to its convenience.

(1) Open a terminator window and run the following:

```Bash
xev
```

(2) You will see a new small window popping up. Now click on it and press the new key combination, say Fn and RightArrow. You will see a number there “keycode 171”.

(3) Open a new terminal window and open your .bashrc file:

```Bash
vi $HOME/.bashrc
```

(4) Append the following:

```
xmodmap -e “keycode 171 = End”
```

(5) Update .bashrc. Repeat the procedure for any other key combinations.

Source: [How can I change what keys on my keyboard do? (How can I create custom keyboard commands/shortcuts?) - Ask Ubuntu](https://www.google.com/url?q=https%3A%2F%2Faskubuntu.com%2Fquestions%2F254424%2Fhow-can-i-change-what-keys-on-my-keyboard-do-how-can-i-create-custom-keyboard&sa=D&sntz=1&usg=AFQjCNHRlpMJrWU0g4wTwVN70NY4lcOtjg)

* Create a bootable linux disk on mac:

Insert flashdrive and open Disk Utility.

Click on Erase. Rename the disk. Set the type to Mac OS Extended (Journaled). Set partition scheme to GUID.

Download iso file of a linux distro of your choice. Convert it to dmg: For example

```Bash
hdiutil convert -format UDRW -o ~/Downloads/openSUSE-Leap-15.1-DVD-x86_64 ~/Downloads/openSUSE-Leap-15.1-DVD-x86_64.iso
```

List the disks and get the disk number:

```Bash
diskutil list
```

Now your flashdrive should be /dev/disk2.

Unmount the disk:

```Bash
diskutil unmountDisk /dev/disk2
```

Now burn the flashdrive with the dmg file of your linux distro:

```Bash
sudo dd if=~/Downloads/openSUSE-Leap-15.1-DVD-x86_64.dmg of=/dev/rdisk2 bs=4m
```

It will look like it does not do anything, but it does. Wait for a couple of minutes.

Now a prompt will open, saying that the flashdrive cannot be read. Do not click on any of the options yet. Run

```Bash
diskutil eject /dev/disk2
```

Then click on Ignore in that small window.

Check if the flashdrive is bootable: Shutdown your Mac. Restart it, by pressing on the 'option' key. Now you should be able to see all the volumes.

Source: [How To Create A Bootable Ubuntu USB Drive For Mac In OS X (itsfoss.com)](https://www.google.com/url?q=https%3A%2F%2Fitsfoss.com%2Fcreate-bootable-ubuntu-usb-drive-mac-os%2F&sa=D&sntz=1&usg=AFQjCNGXbf9MuNJbgxhBB7h6lngPVs5jvQ)

* Make function keys F1-12 operate 'regularly' (i.e. without the need to press and hold Fn key) on Macbook + Ubuntu:

```Bash
echo 2 | sudo tee /sys/module/hid_apple/parameters/fnmode
```

To revert it, run

```Bash
echo 1 | sudo tee /sys/module/hid_apple/parameters/fnmode
```

Source: [On an Apple Keyboard under Linux, how do I make the Function keys work without the fn modifier key? - Unix & Linux Stack Exchange](https://www.google.com/url?q=https%3A%2F%2Funix.stackexchange.com%2Fquestions%2F121395%2Fon-an-apple-keyboard-under-linux-how-do-i-make-the-function-keys-work-without-t&sa=D&sntz=1&usg=AFQjCNEEnDjeSQbLMQ-nNztGXYlD_-Y8Zw)

* Better underbrace in LaTeX:

```LaTeX
\newcommand{\ubrace}[2]{\underbrace{#1}_{\parbox{3em}{\scriptsize\centering #2}}}
```

* Suppose you want to couple two states of equal angular momenta or spin, j. The spin exchange operator can be obtained by using the following code. Play only with the s value. Notice that it fails when j = 2.

```Mathematica
s = 3/2;

X[S_] := Sum[a[n] (S (S + 1) - 2 s (s + 1))^n, {n, 0, 2 s}]

alist = {};

For[i = 0, i <= 2 s, i++,

 alist = Append[alist, a[i]]

 ]

Clear[i];

xlist = {};

num = 0;

For[i = 2 s, i >= 0, i--,

 sgn = (-1)^(num);

 xlist = Append[xlist, X[i] == sgn];

 num += 1;

 ]

Clear[i];

sol = Solve[

    xlist, alist, Reals

    ][[1]];

X12[S_] := Sum[a[n] (S (S + 1) - 2 s (s + 1))^n, {n, 0, 2 s}] //. sol

spin = 0;

Print["\!\(\*SubscriptBox[\(X\), \(12\)]\) = \

\!\(\*SuperscriptBox[SubscriptBox[\(\[Sum]\), \(i = 0\)], \(2  s\)]\) \

\!\(\*SubscriptBox[\(a\), \(n\)]\)(\!\(\*SubscriptBox[\(S\), \(1\)]\)\

\[CenterDot]\!\(\*SubscriptBox[\(S\), \

\(2\)]\)\!\(\*SuperscriptBox[\()\), \(n\)]\)\n"]

For[i = 0, i <= 2 s, i++,

 Print["a(", i, ") = ", a[i] //. sol]

 ]

Print[""];

Print["S\tS(S+1)\t \!\(\*SubscriptBox[\(X\), \(12\)]\)"]

Print["==================="]

For[i = 0, i <= 2 s, i++,

 Print[spin, "\t", spin (spin + 1), "\t\t", X12[spin]];

 spin += 1;

 ]
```

* Suppose we couple two particle of the same spin or angular momentum in general. Explicit expression for the coupled states can be obtained in terms of the uncoupled ones by the following:

```Mathematica
$Assumptions = {j \[Element] Integers, j > 0};

lower[a_ + b_] := lower[a] + lower[b]

lower[a_ u[M___]] := a lower[u[M]]

lower[u[m1_, m2_]] := jm[j, m1] u[m1 - 1, m2] + jm[j, m2] u[m1, m2 - 1]



jm[j_, m_] := Sqrt[j (j + 1) - m (m - 1)]



c[j_, m_] := lower[c[j, m + 1]]/jm[j, m + 1] // Expand



del[a_, b_] := If[a === b, 1, 0]



o[expr_] := Module[

  {dum, res},

  dum = expr // Expand;

  res = dum //. {

     u[a1_, b1_]^2 -> 1,

     u[a1_, b1_] u[a2_, b2_] -> del[a1, a2] del[b1, b2]

     };

  Return[res]

  ]



sc[M_ + 2 j, M_ + 2 j] := 

 Sum[a[i, k] u[j - i, j - k] KroneckerDelta[i + k, -M], {i, 

   0, -M}, {k, 0, -M}]



c[2 j, 2 j] = u[j, j]



c[M_ + 2 j, M_ + 2 j] := Module[{dum, res},

  alist[M] = Module[

    {list, dum1, res1, i, k},

    list = {};

    For[i = 0, i <= -M, i++,

     For[k = 0, k <= -M, k++,

      If[KroneckerDelta[i + k, -M] == 1,

       list = Append[list, a[i, k]];

       ]

      ]

     ];

    list

    ];

  olist[M] = Module[{dum2, res2, i, list},

    list = {};

    For[i = 0, i < -M, i++,

     list = 

       Append[list, o[sc[M + 2 j, M + 2 j] c[-i + 2 j, M + 2 j]] == 0];

     ];

    list = 

     Append[list, o[sc[M + 2 j, M + 2 j] sc[M + 2 j, M + 2 j]] == 1];

    list

    ];

  solve[M] = Solve[

     olist[M], alist[M], Reals 

     ][[1]];

  sc[M + 2 j, M + 2 j] /. solve[M] //. 

   ConditionalExpression[a_, b__] -> a

  ]
```

Here, we keep the angular momentum of either particle to be general, j.

* Suppress "No such file or directory" output in Unix: Simply tack in 2>/dev/null after your command.

* Hide dock in Ubuntu 19.10 + Gnome: First, install dash-to-dock.

```Bash
gsettings set org.gnome.shell.extensions.dash-to-dock autohide false

gsettings set org.gnome.shell.extensions.dash-to-dock dock-fixed false

gsettings set org.gnome.shell.extensions.dash-to-dock intellihide false
```

Revert changes:

```Bash
gsettings set org.gnome.shell.extensions.dash-to-dock autohide true

gsettings set org.gnome.shell.extensions.dash-to-dock dock-fixed true

gsettings set org.gnome.shell.extensions.dash-to-dock intellihide true
```

Source: [https://www.linuxuprising.com/2018/08/how-to-remove-or-disable-ubuntu-dock.html](https://www.google.com/url?q=https%3A%2F%2Fwww.linuxuprising.com%2F2018%2F08%2Fhow-to-remove-or-disable-ubuntu-dock.html&sa=D&sntz=1&usg=AFQjCNGIOSpTRGSC2W8W4A5ELmLF9iy2vQ)

* Move top panel to bottom in Ubuntu 19.10+Gnome:

```Bash
git clone https://github.com/Thoma5/gnome-shell-extension-bottompanel.git

cp -r gnome-shell-extension-bottompanel ~/.local/share/gnome-shell/extensions/bottompanel@tmoer93
```

* Mathematica code to compute metric, affine connection, Riemann tensor, Ricci tensor, and scalar curvature: Paste the following into a Mathematica notebook. Play only with the USER INPUT section. 

e.g. 

```Mathematica
universe = "space";

X = {x, y};

dl = (1/y^2) dx[1]^2 + (1/y^2) dx[2]^2 (* Poincare half plane *)

$Assumptions = {x \[Element] Reals, y \[Element] Reals, y >= 0};
```

The code determines the space (or spacetime) dimensions from the line element and computes all the relevant quantities accordingly.

```Mathematica
(***** USER INPUT *****)

(* define universe: space or spacetime *)

universe = "...";

(* define coordinates *)

X = {..., ...};

(* define line element squared *)

dl = ( ...) dx[1]^2 + ( ...) dx[2]^2 + ( ...);

(* define coordinate assumptions *)

$Assumptions = { ...};



(***** BLACK BOX *****)

(* determine dimension \[ScriptD] *)

dim[dl_] := Module[

   {lst, size, arg, i, trm},

   lst = List @@ dl;

   size = Length[lst];

   arg = {};

   For[i = 1, i <= size, i++,

    trm = lst[[i]] //. {

       fac_ dx[n_]^2 :> n,

       dx[n_]^2 :> n,

       fac_ dx[n_] dx[m_] :> Max[n, m],

       dx[n_] dx[m_] :> Max[n, m]};

    arg = Append[arg, trm]]; Return[Max[arg]]];

\[ScriptD] = dim[dl];

(* construct metric Subscript[g, \[Mu]\[Nu]] *)

g = ConstantArray[0, {\[ScriptD], \[ScriptD]}];

For[i = 1, i <= \[ScriptD], i++,

 For[j = 1, j <= \[ScriptD], j++,

  If[i != j,

   g[[i]][[j]] = 1/2 Coefficient[dl, dx[i] dx[j]],

   g[[i]][[j]] = Coefficient[dl, dx[i]^2]

   ]

  ]

 ]

(* compute determinant of metric g *)

detg = If[universe == "space", Det[g], 

   If[universe == "spacetime", -Det[g]]];

(* compute inverse metric g^\[Mu]\[Nu] *)

invg = Inverse[g] // FullSimplify;

(* construct affine connection Subscript[\[CapitalGamma]^\[Mu], \[Nu]\

\[Lambda]] *)

\[CapitalGamma][\[Mu]_, \[Nu]_, \[Lambda]_] := 

 Sum[1/2 invg[[\[Mu], \[Kappa]]] (D[g[[\[Kappa], \[Nu]]], 

      X[[\[Lambda]]]] + D[g[[\[Kappa], \[Lambda]]], X[[\[Nu]]]] - 

     D[g[[\[Nu], \[Lambda]]], X[[\[Kappa]]]]), {\[Kappa], 

   1, \[ScriptD]}]

(* construct riemann tensor Subscript[\[ScriptCapitalR]^\[Sigma], \

\[Rho]\[Mu]\[Nu]] *)

\[ScriptCapitalR][\[Sigma]_, \[Rho]_, \[Mu]_, \[Nu]_] := (D[\

\[CapitalGamma][\[Sigma], \[Nu], \[Rho]], X[[\[Mu]]]] + 

     Sum[\[CapitalGamma][\[Sigma], \[Mu], \[Kappa]] \[CapitalGamma][\

\[Kappa], \[Nu], \[Rho]], {\[Kappa], 1, \[ScriptD]}]) -

   (D[\[CapitalGamma][\[Sigma], \[Mu], \[Rho]], X[[\[Nu]]]] + 

     Sum[\[CapitalGamma][\[Sigma], \[Nu], \[Kappa]] \[CapitalGamma][\

\[Kappa], \[Mu], \[Rho]], {\[Kappa], 1, \[ScriptD]}]) // FullSimplify

\[ScriptCapitalR]cov[\[Omega]_, \[Rho]_, \[Mu]_, \[Nu]_] := 

 Sum[g[[\[Omega], \[Sigma]]] \[ScriptCapitalR][\[Sigma], \[Rho], \

\[Mu], \[Nu]], {\[Sigma], 1, \[ScriptD]}]

(* construct ricci tensor Subscript[\[ScriptCapitalR], \[Rho]\[Nu]] = \

Subscript[\[ScriptCapitalR]^\[Sigma], \[Rho]\[Sigma]\[Nu]] *)

\[ScriptCapitalR]\[ScriptI]\[ScriptC][\[Rho]_, \[Nu]_] := 

 Sum[\[ScriptCapitalR][\[Sigma], \[Rho], \[Sigma], \[Nu]], {\[Sigma], 

   1, \[ScriptD]}]

(* compute curvature R = g^\[Rho]\[Nu]Subscript[\[ScriptCapitalR], \

\[Rho]\[Nu]] *)

R = Sum[invg[[\[Rho], \[Nu]]] \[ScriptCapitalR]\[ScriptI]\[ScriptC][\

\[Rho], \[Nu]], {\[Rho], 1, \[ScriptD]}, {\[Nu], 1, \[ScriptD]}] // 

   FullSimplify;

(* construct infinitesimal separation vector for debugging *)

le = {};

For[i = 1, i <= \[ScriptD], i++,

 le = Append[le, ToExpression["d" <> ToString[X[[i]]]]]

 ]



(* print all *)

Print["\!\(\*SuperscriptBox[\(ds\), \(2\)]\) = ", le.g.le // Expand]

Print["\!\(\*SubscriptBox[\(g\), \(\[Mu]\[Nu]\)]\) = ", 

 g // MatrixForm]

Print["\!\(\*SuperscriptBox[\(g\), \(\[Mu]\[Nu]\)]\) = ", 

 invg // MatrixForm]

Print["g = ", detg // FullSimplify]

For[i = 1, i <= \[ScriptD], i++,

 For[j = 1, j <= \[ScriptD], j++,

  For[k = 1, k <= \[ScriptD], k++,

   If[j <= k, 

    Print[StringForm[

      "\!\(\*SubscriptBox[SuperscriptBox[\(\[CapitalGamma]\), \

\(``\)], \(``\\\ ``\)]\) = ", i, j, k], 

     " = ", \[CapitalGamma][i, j, k]]]

   ]

  ]

 ]

For[i = 1, i <= \[ScriptD], i++,

 For[j = 1, j <= \[ScriptD], j++,

  For[k = 1, k <= \[ScriptD], k++,

   For[l = 1, l <= \[ScriptD], l++,

    If[i == k && j == l && i < j && k < l,

     Print[

      StringForm[

       "\!\(\*SubscriptBox[\(\[ScriptCapitalR]\), \(``\\\ ``\\\ ``\\\ \

``\)]\)", i, j, k, l], " = ",

      StringForm[

       "-\!\(\*SubscriptBox[\(\[ScriptCapitalR]\), \(``\\\ ``\\\ ``\\\

\ ``\)]\)", j, i, k, l], " = ",

      StringForm[

       "-\!\(\*SubscriptBox[\(\[ScriptCapitalR]\), \(``\\\ ``\\\ ``\\\

\ ``\)]\)", i, j, l, k], " = ",

      StringForm[

       "\!\(\*SubscriptBox[\(\[ScriptCapitalR]\), \(``\\\ ``\\\ ``\\\ \

``\)]\)", j, i, l, k], " = ",

      \[ScriptCapitalR]cov[i, j, k, l]]]

    ]

   ]

  ]

 ]

For[i = 1, i <= \[ScriptD], i++,

 For[j = 1, j <= \[ScriptD], j++,

  If[i <= j, 

   Print[StringForm[

     "\!\(\*SubscriptBox[\(\[ScriptCapitalR]\), \(``\\\ ``\)]\)", i, 

     j], " = ", \[ScriptCapitalR]\[ScriptI]\[ScriptC][i, j]]]

  ]

 ]

Print["R = ", R]
```

* Make your own LaTeXit: We need a tex code that will automatically crop the page to fit the content. The required code is as follows:

```LaTeX
\documentclass{article}

\begin{document}

\hoffset=-1in

\voffset=-1in

\setbox0\hbox{$

E = m c^2

$}

\pdfpageheight=\dimexpr\ht0+\dp0\relax

\pdfpagewidth=\wd0

\shipout\box0

\stop
```

Source: [tex.stackexchange.com/questions/299005/automatic-page-size-to-fit-arbitrary-content](https://www.google.com/url?q=https%3A%2F%2Ftex.stackexchange.com%2Fquestions%2F299005%2Fautomatic-page-size-to-fit-arbitrary-content&sa=D&sntz=1&usg=AFQjCNGOzA5Ke3GtHECz-3NiNzCg5CoObw)

* Compare two pdfs: Install diff-pdf via command line or from somewhere else and run

```Bash
diff-pdf --output-diff=compared.pdf current.pdf previous.pdf
```

Source: [https://vslavik.github.io/diff-pdf/](https://www.google.com/url?q=https%3A%2F%2Fvslavik.github.io%2Fdiff-pdf%2F&sa=D&sntz=1&usg=AFQjCNH879pEoSf3EOncw5CcviqGsMBCSg)


Last updated by K$ on 22 jun 2021.
