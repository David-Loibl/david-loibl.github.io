---
title: 'Processing Orthophotos and DEMs with OpenDroneMap'
date: 9999-12-31
permalink: /posts/todo/opendronemap/
tags:
  - opendronemap
  - orthophoto
  - digital elevation model
---

# Preface
The following guide assumes that you have geotagged imagery showing a specific region from different viewing angles. Typically, such data will be obtained by a drone using a software for automated flightplans, such as [Pix4D](https://www.pix4d.com/product/pix4dcapture) or [QGroundControl](http://qgroundcontrol.com/).

OpenDroneMap (ODM) is a free open source software suite for 'Structure From Motion' (SfM) processing tasks. The source code of [ODM](https://www.opendronemap.org/) is avaialable on [GitHub](https://github.com/OpenDroneMap). Read more in the [documentation](https://docs.opendronemap.org/index.html).


# Installation

### WebODM
Follow the instructions in the [OpenDroneMap documentation](https://docs.opendronemap.org/installation.html#linux) to set up the software. In case docker was not installed before it may be necessary to restart the computer before the environment works.


```console
git config --global credential.helper "cache --timeout=7200"
```