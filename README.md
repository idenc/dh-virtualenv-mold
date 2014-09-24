# dh-virtualenv-mold

A cookiecutter template to add easy Debianization to any existing Python project.
It creates a self-contained Python virtualenv wrapped into a Debian package
(an "omnibus" package, all passengers on board).
The packaged virtualenv is kept in sync with the host's interpreter automatically.
See [spotify/dh-virtualenv](https://github.com/spotify/dh-virtualenv) for more details.

![Apache 2.0 licensed](http://img.shields.io/badge/license-Apache_2.0-red.svg)


## Using the template

Adding this template to your existing Python project goes like this (make sure
you're in the root directory of your project):

```sh
cookiecutter https://github.com/Springerle/dh-virtualenv-mold.git
```

It makes sense to `git add` the created directory directly afterwards, before any
generated files are added, that you don't want to have in your repository.

Note that you need to install the usual Debian development tools and `dh-virtualenv`
(at least version 0.8, unreleased at the time of this writing), before you can actually
build the DEB package. These incantations will perform that for you:

```sh
sudo apt-get install build-essential debhelper devscripts equivs
sudo mk-build-deps --install debian/control
```

Then, if you have all pre-requisites satisfied, try this:

```sh
dpkg-buildpackage -uc -us -b
```

The resulting package, if all went well, can be found in the parent of your project directory.
You can upload it to a Debian package repository via e.g. `dput`, see
[here](https://github.com/jhermann/artifactory-debian#package-uploading)
for a hassle-free solution that works with Artifactory and Bintray.
