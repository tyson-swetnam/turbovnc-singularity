# turbovnc-singularity

## Singularity

Install [Singularity](https://www.sylabs.io/) on your server and your local system. 

**Option 1**: Pull this Github Repository and build the container locally:

```
git clone https://github.com/tyson-swetnam/turbovnc-singularity
cd turbovnc-singularity
sudo singularity build turbovnc-nvidia.simg Singularity
```

**Option 2:**: Pull pre-built container from Singularity Hub:

```
singularity pull shub://tyson-swetnam/turbovnc-singularity:latest
```


## Configure `xstartup`

The `vncserver` should start on its own and create a `~/.vnc/xstartup.turbovnc` file.

If you are having problems with starting the vncserver, [check your VirtualGL installation](https://github.com/aancel/admin/wiki/VirtualGL-on-Ubuntu). 


# Running the container on a Server

If running on HPC, remember to: `module load singularity`

```
singularity exec --nv turbovnc-nvidia.simg vncserver -geometry 1920x1080 -dpi 128
```
