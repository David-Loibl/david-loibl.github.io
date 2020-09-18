---
title: 'Setting up R and RStudio on Ubuntu-based Linux systems'
date: 9999-12-31
permalink: /posts/todo/ubuntu-r-setup/
tags:
  - R
  - tutorial
  - setup
---

# Finding the right R version
Installing R and RStudio with the Ubuntu default packages will leave you with strongly outdated versions. In practice, this often leads to version conflicts when installing additional R packages.

To avoid such conflicts, it does make sense to work with an up-to-date but not brandnew R version. As of now (summer 2020) I would recommend using v3.6, since most actively developed packages are working with it whereas support for v4 is often not yet provided.

Installing the right version of R requires that you know the Ubuntu code of your system. A lot of information on your system is stored in `/etc/os-release`: 
```console
$ cat /etc/os-release
```
Returns something like:

```console
NAME="Linux Mint"
VERSION="19.3 (Tricia)"
ID=linuxmint
ID_LIKE=ubuntu
PRETTY_NAME="Linux Mint 19.3"
VERSION_ID="19.3"
HOME_URL="https://www.linuxmint.com/"
SUPPORT_URL="https://forums.ubuntu.com/"
BUG_REPORT_URL="http://linuxmint-troubleshooting-guide.readthedocs.io/en/latest/"
PRIVACY_POLICY_URL="https://www.linuxmint.com/"
VERSION_CODENAME=tricia
UBUNTU_CODENAME=bionic
```

Relevant for the following is only the last line which could be assessed directly using e.g.
```console
$ grep UBUNTU_CODENAME /etc/os-release
UBUNTU_CODENAME=bionic
```

More information on (Ubuntu releases)[https://wiki.ubuntu.com/Releases]. 


### Installing R
In order to make sure that the R base will receive regular updates, it does make sense to install the package from a regularly updated repository.
Knowing your Ubuntu code you can easily find and fitting deb link at (RStudio's Ubuntu ReadMe page)[https://cran.rstudio.com/bin/linux/ubuntu/README.html].

For example, for the 'bionic' example system shown above and R v3.6 the adequate entry is `deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/` (cran35 is used for reasons of compatibility). This line must be added to `/etc/apt/sources.list` to make sure its visited in system updates. You could use a text editor like nano, emacs or vi to do so (`sudo` may be required) or simply append it through the command line:
```console
$ echo "deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/" >> /etc/sources.list
```

To make sure the installation works, the correct SSL key has to be added to your system:
```console
$ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
```

Now you can update the package library and upgrade existing files:
```console
$ sudo apt-get update
$ sudo apt-get upgrade
```

In case no previous R version was installed, you can do it now:
```console
$ sudo apt-get install r-base-dev
```


# Install some Ubuntu packages frequently used by R packages

```console
$ sudo apt-get install libcurl4-openssl-dev
$ sudo apt-get install libssl-dev
$ sudo apt-get install libxml2-dev
$ sudo apt-get install libudunits2-dev
$ sudo apt install libgdal-dev
```

# Install RStudio

RStudio provides its releases as DEB files. To install these, a tool like `gdebi` must be installed on Ubuntu systems. In case you don't have it, yet, it can be installed using:
```console
$ sudo apt-get install gdebi 
```

Find the right version for your system on the (RStudio download page)[https://rstudio.com/products/rstudio/download/#download] and install it:
```console
$ sudo gdebi /path/to/the/file/.deb
```


# How to handle version conflicts
From time to time R packages will not work with the version of R you have installed. In case your R version is lower than required by the package, such issues can often be resolved by installing a previous release of the package. This can be achieved with 'devtools'. To install 'devtools', go to the R console and do
```r
install.packages("devtools")
```
Before getting started you need to find out which version of R you running and which version of the package will work with this.
R has a builtin variable `version` for this:
```r
version$version.string
```
Finding out which version of the package should be used is a bit tougher. Navigate to the (RDocumentation website)[https://www.rdocumentation.org/] and find the relevant package there. Next to the name of the package, you will see the current version number and a button 'Other versions' next to it. At the bottom of the page, there is a section 'Details' with an entry 'Depends': this where you can see which R version the package requires. You may find out the latest version by selecting older versions from the dropdown on top of the page until you find a package version that supports your version of R.

Let's, for example, say you are working on a machine with R version 3.1 and you want to install a compatible version of ggplot2. In this case, you will find that ggplot2 v.3.1.1 is the last version that supported R 3.1.

Using `devtools` you can now install this version of ggplot2:
```r
require(devtools)
install_version("ggplot2", version = "3.1.1")
```

For more information and a guide on how to install packages from source, please refer to this post on (Installing older versions of packages on the R Studio Support website)[https://support.rstudio.com/hc/en-us/articles/219949047-Installing-older-versions-of-packages].

