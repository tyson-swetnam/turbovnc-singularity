# turbovnc-singularity

# Installation

```
git clone https://github.com/tyson-swetnam/turbovnc-singularity
cd turbovnc-singularity
sudo singularity build turbovnc-nvidia.simg Singularity
```

## Configure `xstartup`

The TurboVNC uses a startup file called `xstartup` in the hidden `~/.vnc/` directory

```
#!/bin/sh
# Uncomment the following two lines for normal desktop:
# unset SESSION_MANAGER
# exec /etc/X11/xinit/xinitrc

[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
xsetroot -solid grey
vncconfig -iconic &
twm &
x-terminal-emulator -geometry 80x24+10+10 -ls -title "$VNCDESKTOP Desktop" &
x-window-manager &
```

# Running the container on a Server

If running on HPC, remember to: `module load singularity`

```
singularity exec turbovnc-nvidia.simg vncserver -xstartup ~/.vnc/xstartup -geometry 1920x1080 -dpi 128
```
