# WINE
Some notes so I don't lose my mind doing WINE stuff...

```bash
# create a new prefix
WINEARCH=win32 WINEPREFIX=~/prefixName winecfg

# run something via a particular prefix
WINEPREFIX=~/prefix wine file.exe

# run msi file
WINEPREFIX=~/prefix wine msiexec /i file.msi 

# debug file
WINEPREFIX=~/prefix winedbg file.exe

# check running wine processes
pgrep wineserver

# install winetricks dependency
WINEPREFIX=~/prefix winetricks dependencyName

# update winetricks
sudo winetricks --self-update


```
