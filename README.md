# turbovnc-singularity

# Installation

```
git clone https://github.com/tyson-swetnam/turbovnc-singularity
cd turbovnc-singularity
sudo singularity build turbovnc-nvidia.simg Singularity
```

## Configure `xstartup`

The `vncserver` should start on its own and create a `~/.vnc/xstartup.turbovnc` file

If not, you can try to start the container by creating your own `xstartup` file.

The TurboVNC uses a startup file called `xstartup` in the hidden `~/.vnc/` directory

```
#!/bin/sh

[ -r /etc/sysconfig/i18n ] && . /etc/sysconfig/i18n
export LANG
export SYSFONT
vncconfig -iconic &
# unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
OS=`uname -s`
if [ $OS = 'Linux' ]; then
case "$WINDOWMANAGER" in
*gnome*)
if [ -e /etc/SuSE-release ]; then
PATH=$PATH:/opt/gnome/bin
export PATH
fi
;;
esac
fi
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
xsetroot -solid grey
xterm -geometry 80x24+10+10 -ls -title "$VNCDESKTOP Desktop" &
startxfce4 &
```

# Running the container on a Server

If running on HPC, remember to: `module load singularity`

```
singularity exec turbovnc-nvidia.simg vncserver -xstartup ~/.vnc/xstartup -geometry 1920x1080 -dpi 128
```
