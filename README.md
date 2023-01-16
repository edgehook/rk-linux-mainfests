Advantech RK3399 bsp Repo Manifest README
This repo is used to download manifests for Advantech RK3399 bsp releases.
## **Supported boards**
RK3399 Series
## Host PC Requirements
To use this manifest repo, the 'repo' tool must be installed first.
```
$ mkdir ~/bin
$ curl http://commondatastorage.googleapis.com/git-repo-downloads/repo  > ~/bin/repo
$ chmod a+x ~/bin/repo
$ PATH=${PATH}:~/bin
```
To execute
```
$: mkdir <release>
$: cd <release>
$: repo init -u https://github.com/edgehook/rk-linux-manifests.git -b <branch name> [ -m <release manifest>]
$: repo sync
```
Examples:To download the RK3399 itb201 release.
```
$repo init -u https://github.com/edgehook/rk-linux-manifests.git  -b master -m adv-rk3399-itb201a1-1.0.0.xml
$repo sync
```
