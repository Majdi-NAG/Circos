### Download Circos:

http://circos.ca/software/download/

```
wget http://circos.ca/distribution/circos-0.67-7.tgz
tar xvzf circos-0.67-7.tgz
cd circos-0.67-7/bin
ls
```

>circos  gddiag  list.modules  test.modules

`which env`
>/usr/bin/env
PS: Edit Shebang in `circos` and `gddiag` binary at `<extracted circos path>/bin/` to match correct PATH for `env`. In my case, it is `#!/usr/bin/env perl` and not default `#!/bin/env perl`

### Get dependencies:

`which perl`
>/usr/bin/perl

`perl -v`
>v.518.2 #If different, circos works with default perl version shipped with Ubuntu 14.04

#### Install perl modules:

* http://circos.ca/software/installation/
* http://circos.ca/tutorials/lessons/configuration/distribution_and_installation/

```
cd <extracted circos path>/bin/circos/bin
./circos -modules #or
./circos -modules | grep missing
```

  ok       1.29 Carp
  ok       0.36 Clone
  missing       2.56 Config::General
  ok       3.40 Cwd
  ok      2.145 Data::Dumper
  ok       2.52 Digest::MD5
  ok       2.84 File::Basename
  ok       3.40 File::Spec::Functions
  ok       0.23 File::Temp
  ok       1.51 FindBin
  missing       0.39 Font::TTF::Font
  missing       2.46 GD
  missing        0.2 GD::Polyline
  ok       2.39 Getopt::Long
  ok       1.16 IO::File
  ok       0.33 List::MoreUtils
  ok       1.27 List::Util
  missing       0.01 Math::Bezier
  ok      1.998 Math::BigFloat
  missing       0.07 Math::Round
  missing       0.08 Math::VecStat
  ok       1.03 Memoize
  ok       1.32 POSIX
  missing       1.18 Params::Validate
  ok       1.61 Pod::Usage
  missing          2 Readonly
  missing 2013031301 Regexp::Common
  missing       2.63 SVG
  missing       1.19 Set::IntSpan
  missing     1.6611 Statistics::Basic
  ok       2.41 Storable
  ok       1.17 Sys::Hostname
  ok       2.02 Text::Balanced
  missing       0.59 Text::Format
  ok     1.9725 Time::HiRes

* For non-GD modules, install via cpan prompt:

`sudo perl -MCPAN -e shell`
>cpan shell -- CPAN exploration and modules installation (v2.00)
>Enter 'h' for help.

```
cpan[1]>
cpan[2]> install Config::General Font::TTF::Font Math::Bezier Math::Round Math::VecStat Params::Validate Readonly Regexp::Common SVG Set::IntSpan Statistics::Basic Text::Format
#run same command again to check all modules are up-to-date
cpan[3]> install Config::General Font::TTF::Font Math::Bezier Math::Round Math::VecStat Params::Validate Readonly Regexp::Common SVG Set::IntSpan Statistics::Basic Text::Format
cpan[4]>exit
```
>Output of cpan[3] command from above:

  Reading `/home/foo/.cpan/Metadata`
    Database was generated on Fri, 17 Apr 2015 10:41:02 GMT
  Config::General is up to date (2.56).
  Font::TTF::Font is up to date (0.39).
  Math::Bezier is up to date (0.01).
  Math::Round is up to date (0.07).
  Math::VecStat is up to date (0.08).
  Params::Validate is up to date (1.18).
  Readonly is up to date (2.00).
  Regexp::Common is up to date (2013031301).
  SVG is up to date (2.63).
  Set::IntSpan is up to date (1.19).
  Statistics::Basic is up to date (1.6611).
  Text::Format is up to date (0.59).

* Install GD and GD::Polyline pacakges using `libgd-gd2...` packages via `apt-get` command:

```
sudo apt-get install libgd-dev libgd2-xpm-dev libgd-gd2-perl build-essential zlib1g-dev libpng12-dev libjpeg-dev
cd <extracted circos path>/bin/circos/bin
./circos -modules #or
./circos -modules | grep missing
```

>All modules should show `ok`.

### Test circos:

* Test `circos` command:

```
cd <extracted circos path>/bin/circos/example
./run
```

* Test GD installation to make sure your Perl distribution can create graphics and handle True Type fonts.

```
cd <extracted circos path>/
bin/gddiag
```
>Look at the created gddiag.png in circos../   
>It should look like: http://www.circos.ca/tutorials/lessons/configuration/png_output/images  

END

