## ansible-project-conp notes

## Resources

* https://github.com/CONP-PCNO/conp-documentation/blob/master/Datalad/crawl_prevent_ad_open.md
* https://github.com/datalad/datalad
* http://docs.datalad.org/en/latest/gettingstarted.html
* http://neuro.debian.net/

## Requirements

* Account on phantom VM > cecile m
* 

## Optional

```shell
sudo apt update
sudo apt -y upgrade
sudo reboot
```

## Requirements

### git install

```shell
sudo apt install -y git
```

### git configure

```shell
git config --global user.name "Mona Lisa"
git config --global user.email "mona.lisa@gmail.com"
```

### Python

may be required

```shell
#sudo apt install -y python-minimal
#sudo apt install -y python-setuptools
```

required

```shell
sudo apt install -y python-pip
sudo apt install -y virtualenv
```

Optional ( i do this)

```shell
sudo pip install --upgrade pip
```

## datalad

### Installation types

#### Latest from source (recommended)

##### Create a virtualenv

###### requirements

Create a **Python 2.7** virtual environment:

```shell
virtualenv ~/.venv/datalab/latest --python=python2.7
source ~/.venv/datalab/latest/bin/activate
```

##### Grab the source

```shell
cd
git clone https://github.com/datalad/datalad.git
```

#### Requirements

##### liblzma-dev

```shell
sudo apt install -y liblzma-dev
```

#### install

```shell
cd ~/datalad
pip install -r requirements.txt
datalad --version
```

Output example:

```shell
datalad 0.12.0rc2
```

#### Standard pip installation (from pypi)

##### system wide installation

```shell
sudo pip install datalad
```

##### As regular user using pip

```shell
pip install --user datalad
```

Install to your virtual environment:

```shell
pip install datalad
```

##### The Ubuntu / Neuro Debian way:

```shell
wget -O- http://neuro.debian.net/lists/bionic.us-nh.full | sudo tee /etc/apt/sources.list.d/neurodebian.sources.list
sudo apt-key adv --recv-keys --keyserver hkp://pool.sks-keyservers.net:80 0xA5D32F012649A5A9
sudo apt-get update
sudo apt-get install datalad
```

## git-annex

### Install

Upgrading Git-Annex

Sometimes, there are some issues with Datalad because it is using the  wrong version of git-annex. To upgrade git-annex, you need to install `git-annex-standalone`.

For a detailed and specific process, follow the steps outlined by neurodebian: 

* [neuro.debian.net/install_pkg.html?p=git-annex-standalone](http://neuro.debian.net/install_pkg.html?p=git-annex-standalone)

upgade git-annex using neurodebian all from:

#### From Vanderbilt / Ubuntu 18.04 system:

potential ansible vars:

```shell
neurodebian_server: 'dartmouth' # vanderbilt ...
neurodebian_apt_key: 0xA5D32F012649A5A9
```

commands:

```shell
wget -O- http://neuro.debian.net/lists/bionic.us-tn.full | sudo tee /etc/apt/sources.list.d/neurodebian.sources.list
# following step fails frequently
sudo apt-key adv --recv-keys --keyserver hkp://pool.sks-keyservers.net:80 0xA5D32F012649A5A9
```

#### From Dartmouth / Ubuntu 18.04 system:

```shell
wget -O- http://neuro.debian.net/lists/bionic.us-nh.full | sudo tee /etc/apt/sources.list.d/neurodebian.sources.list
sudo apt-key adv --recv-keys --keyserver hkp://pool.sks-keyservers.net:80 0xA5D32F012649A5A9
```



Install the `git-annex-standalone` package

```shell
sudo apt-get update
sudo apt-get install -y git-annex-standalone
```

Partial output for ubuntu 18.04 minimal desktop:

```shell
The following additional packages will be installed:
  aria2 ffmpeg git-remote-gcrypt libass9 libavdevice57 libavfilter6 libavresample3
  libbs2b0 libdc1394-22 libdvdnav4 libdvdread4 libflite1 liblua5.2-0 libmysofa0
  libnorm1 libopenal-data libopenal1 libpgm-5.2-0 libpostproc54 libqt5positioning5
  libqt5qml5 libqt5quick5 libqt5sensors5 libqt5webchannel5 libqt5webkit5 librubberband2
  libsdl2-2.0-0 libsndio6.1 libswscale4 libuchardet0 libva-wayland2 libzmq5 mpv nocache
  phantomjs python3-pyxattr rtmpdump youtube-dl
Suggested packages:
  ffmpeg-doc xdot bup adb tor magic-wormhole tahoe-lafs uftp libdvdcss2 libportaudio2
  qt5-qmltooling-plugins sndiod python3-pyxattr-dbg python-pyxattr-doc
The following NEW packages will be installed:
  aria2 ffmpeg git-annex-standalone git-remote-gcrypt libass9 libavdevice57
  libavfilter6 libavresample3 libbs2b0 libdc1394-22 libdvdnav4 libdvdread4 libflite1
  liblua5.2-0 libmysofa0 libnorm1 libopenal-data libopenal1 libpgm-5.2-0 libpostproc54
  libqt5positioning5 libqt5qml5 libqt5quick5 libqt5sensors5 libqt5webchannel5
  libqt5webkit5 librubberband2 libsdl2-2.0-0 libsndio6.1 libswscale4 libuchardet0
  libva-wayland2 libzmq5 mpv nocache phantomjs python3-pyxattr rtmpdump youtube-dl
0 upgraded, 39 newly installed, 0 to remove and 0 not upgraded.
Need to get 100 MB of archives.
After this operation, 302 MB of additional disk space will be used.
```

Confirm version

```shell
git-annex version
```

Ensure you have 7.20 or greater

Output example:

```shell
git-annex version: 7.20190219+git191-g2d6a364d4-1~ndall+1
build flags: Assistant Webapp Pairing S3(multipartupload)(storageclasses) WebDAV Inotify DBus DesktopNotify TorrentParser MagicMime Feeds Testsuite
dependency versions: aws-0.20 bloomfilter-2.0.1.0 cryptonite-0.25 DAV-1.3.3 feed-1.0.0.0 ghc-8.4.4 http-client-0.5.13.1 persistent-sqlite-2.8.2 torrent-10000.1.1 uuid-1.3.13 yesod-1.6.0
key/value backends: SHA256E SHA256 SHA512E SHA512 SHA224E SHA224 SHA384E SHA384 SHA3_256E SHA3_256 SHA3_512E SHA3_512 SHA3_224E SHA3_224 SHA3_384E SHA3_384 SKEIN256E SKEIN256 SKEIN512E SKEIN512 BLAKE2B256E BLAKE2B256 BLAKE2B512E BLAKE2B512 BLAKE2B160E BLAKE2B160 BLAKE2B224E BLAKE2B224 BLAKE2B384E BLAKE2B384 BLAKE2S256E BLAKE2S256 BLAKE2S160E BLAKE2S160 BLAKE2S224E BLAKE2S224 BLAKE2SP256E BLAKE2SP256 BLAKE2SP224E BLAKE2SP224 SHA1E SHA1 MD5E MD5 WORM URL
remote types: git gcrypt p2p S3 bup directory rsync web bittorrent webdav adb tahoe glacier ddar hook external
operating system: linux x86_64
supported repository versions: 5 7
upgrade supported from repository versions: 0 1 2 3 4 5 6
```

## Crawler setup

Create a directory to crawl into and initialize it as a datalad repo

```source
cd
git clone https://github.com/CONP-PCNO/conp-dataset.git
mkdir -p ~/conp-dataset/prevent-ad-open
cd ~/conp-dataset/prevent-ad-open
datalad create
```

### Troubleshooting

Output examples:

### Failed to run ['git', 'config', 'user.name']

```shell
[INFO   ] Creating a new annex repo at /home/csteel/conp-dataset/prevent-ad-open 
[WARNING] It is highly recommended to configure git first (set both user.name and user.email) before using DataLad. Failed to verify that git is configured: CommandError: command '['git', 'config', 'user.name']' failed with exitcode 1
| Failed to run ['git', 'config', 'user.name'] under None. Exit code=1. out= err= [cmd.py:run:542].  Some operations might fail or not perform correctly. 
create(ok): /home/csteel/conp-dataset/prevent-ad-open (dataset)
```

remedy, configure git

via git-config

```shell
git config --global user.name "Mona Lisa"
git config --global user.email "mona.lisa@gmail.com"
```

via a manual edit of users `~/.gitconfig` file

```shell
nano ~/.gitconfig
```

Content example:

```shell
[user]
	email = mona.lisa@gmail.com
	name = Mona Lisa
```

### ... will not create a dataset in a non-empty directory

```shell
[ERROR  ] will not create a dataset in a non-empty directory, use `force` option to ignore [create(/home/csteel/conp-dataset/prevent-ad-open)] 
(0.11.3) csteel@christopher-P1:~/conp-dataset/prevent-a
```

remedy via force example:

```shell
datalad create force
```

Output example:

```shell
[INFO   ] Creating a new annex repo at /home/vagrant/conp-dataset/prevent-ad-open/force 
create(ok): /home/vagrant/conp-dataset/prevent-ad-open/force (dataset)
```

Remedy via deleting the directory contents

```shell
rm -Rf .*
rm -Rf *
datalad create
```

## Configure

```shell
mkdir  ~/conp-dataset/prevent-ad-open/.datalad/providers
nano ~/conp-dataset/prevent-ad-open/.datalad/providers/loris.cfg
```

### Content example:

phantom

```shell
[provider:loris-prevent-ad]
url_re = https:\/\/preventad-open-dev.loris.ca\/.*
credential = loris-prevent-ad
authentication_type = loris-token
loris-token_failure_re = "User not authenticated"}$

[credential:loris-prevent-ad]
url = https://preventad-open-dev.loris.ca/api/v0.0.3-dev/login
type = loris-token
```



works

```shell
[provider:loris-prevent-ad]
url_re = https:\/\/preventad-open-dev.loris.ca\/.*
credential = loris-prevent-ad
authentication_type = loris-token
loris-token_failure_re = "User not authenticated"}$

[credential:loris-prevent-ad]
url = https://preventad-open-dev.loris.ca/api/v0.0.3-dev/login
type = loris-token
```

broken

```cfg
[provider:loris-prevent-ad]
url_re = https:\/\/[preventad-open-dev.loris.ca]\/.*
credential = loris-prevent-ad
authentication_type = loris-token
loris-token_failure_re = "User not authenticated"}$

[credential:loris-prevent-ad]
url = https://preventad-open-dev.loris.ca/api/v0.0.3-dev/login
type = loris-token
```

### Add and commit to git

```shell
git status
git add .
git status
git commit -m 'add loris.cfg to providers'
```

##  Crawler

### Clone repo

```shell
cd
git clone https://github.com/driusan/datalad-crawler
cd datalad-crawler
git checkout enh-loriscrawler
pip install .
```

### Initialize the crawler config

```shell
cd ~/conp-dataset/prevent-ad-open
datalad crawl-init -t loris apibase=https://preventad-open-dev.loris.ca/api/v0.0.3-dev url=https://preventad-open-dev.loris.ca/api/v0.0.3-dev/projects/loris/images
```

### Commit .datalad directory

```shell
git add .datalad
git commit -m 'commit .datalad directory'
```

### Crawl test

```shell
datalad crawl
```





## pip install 

```shell
sudo apt-get install build-essential libssl-dev libffi-dev python-dev
```

openssl requirements

```shell
apt-get install libssl-dev libffi-dev
# yum install openssl-devel libffi-devel
```

pip yum install openssl-devel libffi-devel

```shell
sudo pip install pyopenssl
```

### Twisted

Requirements

```powershell
sudo apt-get install python3.6-dev
```

Install

```shell
pip install twisted
```





```shell
 yum install openssl-devel libffi-devel
```