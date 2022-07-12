# Get yourself a minimal TeXlive on GNU/Linux

**(Warning 1)** Here, *minimal* means that probably there isn't all what you need, but you have a nice base that can be easily enriched through ```texliveonfly```.

**(Warning 2)** The procedure below installs TeXlive in your own home. So, if you want TeXlive to be accessible to other users, this might not be the best choice.

**(Warning 3)** This README comes bundled with some scripts: they are intended to automate the installation process explained here. Currently, *they are a work in progress*.


## Installation (consider ```install```)

The installation process does not mess your home up, as just two new directories are created: one is ```~/texlive``` and the other is ```~/.texlive``` (or some variation...).

To keep things tidy, let us create a directory and move there:
```bash
$ mkdir install-tl; cd install-tl
```
The installer comes directly from CTAN as a compressed archive:
```bash
$ wget "https://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz"
```
Decompress that archive:
```bash
$ tar -xzf install-tl-unx.tar.gz --strip-components 1
```
so that can now start the installer:
```bash
$ TEXLIVE_INSTALL_PREFIX=~/texlive ./install-tl --scheme minimal
```
You are now asked to decide the details of the installation: hit ```I``` and then ```Enter```. At this point, it only remains to wait few minutes.


## Post-installation (have a look at ```post-install```)

Once the installer has finished its work, paste the following lines on your ```~/.bashrc```:
```
export PATH=~/texlive/YEAR/bin/x86_64-linux:$PATH
export MANPATH=~/texlive/YEAR/texmf-dist/doc/man:$MANPATH
export INFOPATH=~/texlive/YEAR/texmf-dist/doc/info:$INFOPATH
```
where ```YEAR``` is to be replaced with the year of the TeXlive you have just installed. Save the changes and
```bash
$ source ~/.bashrc
```

Add a couple of packages we cannot live without:
```bash
$ tlmgr install texdoc
$ tlmgr install texliveonfly
```
In particular, ```texliveonfly``` is a key package for us: it installs the missing packages during the creation of the final document --- as MiKTeX does. It is very simple to use:
```bash
$ texliveonfly -c COMPILER YOUR_TEX_FILE
```
Here ```COMPILER``` can be, for instance, ```pdf[la]tex```, ```lua[la]tex```, ```xe[la]tex``` or others...

**(Warning 4)** Although it is a great tool, in few cases it may need some help from the user. For example, you may want to install by yourself some packages after ```polyglossia``` or ```babel```.
```bash
$ tlmgr install hyphen-LANGUAGE
```
(Some of the hyphen packages are: ```hyphen-english```, ```hyphen-french```, ```hyphen-german```, ```hyphen-italian``` and so on...)

**(Warning 5)** It seems that
```bash
$ texliveonfly -c COMPILER -a '--synctex=1' FILE.tex
```
(and who knows what else...) turns off the ability to install packages on the fly.

However, the TeXlive we've installed hasn't ```pdflatex```, ```xelatex```, ```lualatex``` and some other things yet. If you want them:
```bash
$ tlmgr install latex latex-bin
```


## Uninstall TeXlive (```uninstall``` does the same)

You know, cyclically you have to get rid of the old version and leave space to the newer one.
```bash
$ rm -rf ~/{,.}texlive*
```
should suffice for the purpouse. (You may need to employ ```sudo```...)

