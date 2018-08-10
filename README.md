# turbovnc-singularity


## VirtualGL and TurboVNC

You must have TurboVNC installed on your client to use this container for remote vizualization.

[VirtualGL](https://virtualgl.org) is an open source toolkit that gives any Unix or Linux remote display software the ability to run OpenGL applications with full 3D hardware acceleration. VirtualGL is run on both the server and client for sending the display over the internet.

[TurboVNC](https://turbovnc.org/) is tuned to provide peak performance for 3D and video workloads.

https://www.vscentrum.be/client/multiplatform/turbovnc

https://summerofhpc.prace-ri.eu/remote-accelerated-graphics-with-virtualgl-and-turbovnc/

https://virtualgl.org/

[Ubuntu installation instructions](https://gist.github.com/cyberang3l/422a77a47bdc15a0824d5cca47e64ba2)

[VirtualGL use on Ubuntu](https://github.com/aancel/admin/wiki/VirtualGL-on-Ubuntu)

Download the following packages for the server:
* The .deb package for VirtualGL on [sourceforge](http://sourceforge.net/projects/virtualgl/files/)
* The .deb package for TurboVNC on [sourceforge](http://sourceforge.net/projects/turbovnc/files/)

## Singularity

Install [Singularity](https://www.sylabs.io/) on your server. As of mid-August 2018 Singularity is `v2.6.0`

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

Run the container (default entrypoint):

```
singularity run --nv turbovnc-ubuntu16.simg
```

Execute the container:

```
singularity exec --nv turbovnc-ubuntu16.simg vncserver -geometry 1920x1080 -dpi 128
```

Shell into the container:

```
singularity shell --nv turbovnc-ubuntu16.simg
```

