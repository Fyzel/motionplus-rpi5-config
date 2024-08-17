# Configure MotionPlus Environment and Install MotionPlus from GitHub source

*NOTE:* This instruction assumes the installation is performed on a installed version of Raspberry Pi OS.

## Step 1 - Install prerequsities
Install prerequisite packages on Raspberry Pi OS

``` bash
sudo apt update -y && sudo apt upgrade -y && sudo apt-get install ffmpeg autoconf automake autopoint build-essential pkgconf libtool libzip-dev libjpeg-dev git libavformat-dev libavcodec-dev libavutil-dev libswscale-dev libavdevice-dev libopencv-dev libwebp-dev gettext libmicrohttpd-dev libmariadb-dev libcamera-dev libcamera-tools libcamera-v4l2 libasound2-dev libpulse-dev libfftw3-dev libpq-dev libsqlite3-dev mariadb-server mariadb-client
```

## Step 2 - Add `motion` user and group.

```bash
sudo addgroup --system motion
sudo adduser --system --shell /usr/sbin/nologin --home /var/lib/motion --ingroup motion --no-create-home motion
```

## Step 3 - Create video storage location and set permissions

```bash
sudo mkdir -p /home/motion && sudo chown motion:motion /home/motion/ && sudo chmod g+w /home/motion/
ln -s /home/motion /home/pi/Videos/cctv
```

## Step 4 - Add `motion` and `pi` users to the `motion` group.
```bash
sudo usermod -a -G motion pi
sudo usermod -a -G motion motion
```

## Step 5 - Confirm group membership

```bash
groups pi
groups motion
```


## Step 6 - Create the motionplus config and log directories

```bash
sudo mkdir -p /etc/motionplus
sudo mkdir /var/log/motionplus
sudo chown motion:root /var/log/motionplus
```


## Step 7 - Clone the GitHub project, build, and install

Go to the [build instructions](https://motion-project.github.io/motionplus_build.html) to clone a local copy of the MotionPlus GitHub repository.

```bash
mkdir ~/src
cd ~/src
git clone https://github.com/Motion-Project/motionplus.git
cd motionplus
autoreconf -fiv
./configure
make
sudo make install
```

Next Step: [Configure MotionPlus](./motionplus-config.md)
