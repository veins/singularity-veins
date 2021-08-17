singularity-veins
-----------------

Scripts for building a [Singularity][SYLABS] container for quickly building and running Veins simulations anywhere.


## Requirements ##

- [Singularity][SYLABS] 3.5.2
- [Debootstrap][DEBIAN] 1.0.114

[SYLABS]: https://sylabs.io/
[DEBIAN]: https://wiki.debian.org/Debootstrap


## Contents ##

- Debian Buster
- Veins 5.0
- OMNeT++ 5.6
- SUMO 1.4.0


## Building ##

```
PATH=$PATH:/usr/sbin singularity build --fakeroot singularity-veins.sif singularity-veins.def
```


## Help ##

```
singularity run-help singularity-veins.sif
```


## Building/running simulations ##

```
mkdir -p work/src
cd work/src
git clone --branch veins-5.0 https://github.com/sommer/veins veins
sudo singularity run -H work:/work -C singularity-veins.sif --chdir src/veins -- ./configure
sudo singularity run -H work:/work -C singularity-veins.sif --chdir src/veins -- make -j$(nproc)
sudo singularity run -H work:/work -C --net --network none singularity-veins.sif --chdir src/veins/examples/veins --launchd -- ./run -u Cmdenv
head work/src/veins/examples/veins/results/General-\#0.sca
```


## License ##

Veins is composed of many parts. See the version control log for a full list of
contributors and modifications. Each part is protected by its own, individual
copyright(s), but can be redistributed and/or modified under an open source
license. License terms are available at the top of each file. Parts that do not
explicitly include license text shall be assumed to be governed by the "GNU
General Public License" as published by the Free Software Foundation -- either
version 2 of the License, or (at your option) any later version
(SPDX-License-Identifier: GPL-2.0-or-later). Parts that are not source code and
do not include license text shall be assumed to allow the Creative Commons
"Attribution-ShareAlike 4.0 International License" as an additional option
(SPDX-License-Identifier: GPL-2.0-or-later OR CC-BY-SA-4.0). Full license texts
are available with the source distribution.

