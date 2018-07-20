Bootstrap: debootstrap
OSVersion: xenial
MirrorURL: http://us.archive.ubuntu.com/ubuntu/

%runscript
exec echo "The runscript is the containers default runtime command!"

%setup
    echo "Looking in directory '$SINGULARITY_ROOTFS' for /bin/sh"
    if [ ! -x "$SINGULARITY_ROOTFS/bin/sh" ]; then
        echo "Hrmm, this container does not have /bin/sh installed..."
        exit 1
    fi
exit 0

%environment

%post

apt-get update 
apt-get -y upgrade 
apt-get install -y --fix-missing software-properties-common libglib2.0 libqt5gui5 libgtk2.0-0 libglu1-mesa libgomp1 zlib1g 
apt-get install -y  --fix-missing libxcb-image0 libqt5x11extras5 libqt5gui5 
apt-get install -y --fix-missing language-pack-en \
  language-pack-en-base wget \
  vim nano lshw lsb-release bash-completion \
  kmod iputils-ping net-tools \
  wget curl

# Install Virtual GL

wget https://sourceforge.net/projects/virtualgl/files/2.5.2/virtualgl_2.5.2_amd64.deb/download -O /tmp/virtualgl_2.5.2_amd64.deb
apt-get -y install mesa-utils mesa-utils-extra x11-apps
dpkg -i /tmp/virtualgl_2.5.2_amd64.deb

# Install Agisoft Photoscan Version 1.4.3 

wget /usr/local/photoscan-pro_1_4_3_amd64.tar.gz http://download.agisoft.com/photoscan-pro_1_4_3_amd64.tar.gz 
tar zxvf /usr/local/photoscan-pro_1_4_3_amd64.tar.gz 
ln -s /usr/local/photoscan-pro/photoscan.sh 
rm -f /usr/local/photoscan-pro_1_4_3_amd64.tar.gz
dpkg-reconfigure locales
chmod 755 /usr/local/photoscan-pro/ 
chmod 755 /usr/local/photoscan-pro/* 
chmod 755 /usr/local/photoscan-pro.sh
