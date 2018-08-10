# turbovnc-singularity

## Singularity

Install [Singularity](https://www.sylabs.io/) on your server. As of mid-August Singularity is v2.6.0

**Option 1**: Pull this Github Repository and build the container on the server:

```
git clone https://github.com/tyson-swetnam/turbovnc-singularity
cd turbovnc-singularity
sudo singularity build turbovnc-ubuntu16.simg Singularity
```

**Option 2:**: Pull pre-built container from Singularity Hub:

```
singularity pull --name turbovnc-ubuntu16.simg shub://tyson-swetnam/turbovnc-singularity
```

## Configure `xstartup`

The `vncserver` should start on its own and create a `~/.vnc/xstartup.turbovnc` file.

If you are having problems with starting the vncserver, [check your VirtualGL installation](https://github.com/aancel/admin/wiki/VirtualGL-on-Ubuntu). 


# Running the container on a Server

If running on UA HPC, remember to: 

`module load singularity`
`module load cuda80/gdk`

Execute the container:

```
singularity exec --nv turbovnc-ubuntu16.simg vncserver -geometry 1920x1080 -dpi 128
```

Shell into the container:

```
singularity shell --nv turbovnc-ubuntu16.simg
```

