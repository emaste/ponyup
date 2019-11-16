# ponyup

The Pony toolchain multiplexer

## Usage

### Install ponyup

```bash
curl --proto '=https' --tlsv1.2 -sSf https://raw.githubusercontent.com/ponylang/ponyup/master/ponyup-init.sh | sh
```

### Install Pony

Choose the latest release of the Pony compiler or the latest nightly build.
```bash
ponyup update ponyc nightly
```
```bash
ponyup update ponyc release
```
These commands will download the chosen version of ponyc and install it to `$HOME/.pony/ponyup/bin` by default. See the instructions below for how to set the install path and manage Pony applications.

### Set install prefix

By default, ponyup will create its root directory in `$HOME/.pony`. This prefix can be set manually with the `--prefix` (or `-p`) option. All packages selected as default will be symbolically linked into `${prefix}/ponyup/bin`. So, by default, `ponyup update release ponyc` will install `ponyc` to `$HOME/.pony/ponyup/bin/ponyc`.

### Install a previous package version

You can install any prior release or nightly build available on [Cloudsmith](https://cloudsmith.io/~ponylang/repos/). For example, `changelog-tool` `0.4.0` can be installed with the following command:
```bash
ponyup update changelog-tool release-0.4.0
```

### Show installed package versions

The `ponyup show` command will display the installed package versions with the selected packages marked as green with an asterisk:
```console
$ ponyup show
stable-nightly-20191116 *
stable-nightly-20191115
ponyc-release-0.33.0-gnu *
ponyc-nightly-20191116-gnu
ponyc-nightly-20191115-gnu
corral-nightly-20191116 *
corral-nightly-20191115
changelog-tool-nightly-20191116
changelog-tool-nightly-20191115 *
```
The `show` command also has an optional `package` argument to show only the installed versions of the given package:
```console
$ ponyup show ponyc
ponyc-release-0.33.0-gnu *
ponyc-nightly-20191116-gnu
ponyc-nightly-20191115-gnu
```

### Select an installed package as default

The `select` command can swith which installed package version to set as default. Here is an example of switching from ponyc `release-0.33.0` to `nightly-20191116`:
```console
$ ponyup show ponyc
ponyc-release-0.33.0-gnu *
ponyc-nightly-20191116-gnu
ponyc-nightly-20191115-gnu
$ ponyc --version
0.33.0-98c36095 [release]
compiled with: llvm 7.0.1 -- cc (Ubuntu 7.4.0-1ubuntu1~18.04.1) 7.4.0
Defaults: pic=true
$ ponyup select ponyc nightly-20191116
selecting ponyc-nightly-20191116-gnu as default for ponyc
$ ponyup show ponyc
ponyc-release-0.33.0-gnu
ponyc-nightly-20191116-gnu *
ponyc-nightly-20191115-gnu
$ ponyc --version
nightly-20191116 [release]
compiled with: llvm 7.1.0 -- cc (Ubuntu 7.4.0-1ubuntu1~18.04.1) 7.4.0
Defaults: pic=true
```
