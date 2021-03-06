[![Shen Version](https://img.shields.io/badge/shen-20.1-blue.svg)](https://github.com/Shen-Language)
[![Build Status](https://travis-ci.org/Shen-Language/shen-cl.svg?branch=master)](https://travis-ci.org/Shen-Language/shen-cl)

# Shen for Common Lisp

[Shen](http://www.shenlanguage.org) for Common Lisp by [Mark Tarver](http://marktarver.com/), with contributions by the [Shen Language Open Source Community](https://github.com/Shen-Language).

This codebase currently supports the following implementations:

  * [GNU CLisp](http://www.clisp.org/)
  * [Clozure Common Lisp](http://ccl.clozure.com/)
  * [Steel Bank Common Lisp](http://www.sbcl.org/)

This port is often considered the de-facto standard implementation of the Shen language. It is also the fastest known port, running the standard test suite in 4-8 seconds on SBCL, depending on hardware.

Bug reports, fixes and enhancements are welcome. If you intend to port Shen to another variety of Common Lisp, consider doing so as a pull request to this repo.

## Building

You will need to have the Common Lisp implementations you want to work with installed and available as the `Makefile` requires. Installation is different depending on operating system.

| Implementation | Minimum Version |
|:---------------|:----------------|
| `clisp`        | `2.49`          |
| `ccl`          | `1.10`          |
| `sbcl`         | `1.3.1`         |

### Linux

CLisp and SBCL are available through `apt`. Just run `sudo apt install clisp sbcl`.

There is a [separately available package](http://mr.gy/blog/clozure-cl-deb.html) for Clozure. Run the following to download and install it:

```
wget http://mr.gy/blog/clozure-cl_1.11_amd64.deb
sudo dpkg -i clozure-cl_1.11_amd64.deb
```

If the version of SBCL available throught `apt` is too old, a sufficiently new version can be downloaded and installed like this:

```
wget http://http.us.debian.org/debian/pool/main/s/sbcl/sbcl_1.3.14-2+b1_amd64.deb
sudo dpkg -i sbcl_1.3.14-2+b1_amd64.deb
```

### macOS

CLisp, Clozure and SBCL can be acquired through Homebrew with `brew install clisp clozure-cl sbcl`.

### Windows

CLisp has an exe installer and a zip package on [SoureForge](https://sourceforge.net/projects/clisp/files/clisp/2.49/). You'll have to include `clisp.exe` as well as `libintl-8.dll` and `libreadline6.dll` in on your PATH to ensure the clisp build of shen-cl will run.

Clozure will need to be installed manually:
  * Download the zip from [here](https://ccl.clozure.com/download.html) and extract it under `Program Files`.
  * Put a script named `ccl.cmd` in your `%PATH%` containing something like:

```batch
@echo off
"C:\Program Files\ccl\wx86cl64.exe" %*
```

SBCL has an msi package on its [download page](http://www.sbcl.org/platform-table.html).

The `Makefile` uses commands typically not found on Windows, so [GOW](https://github.com/bmatzelle/gow) is recommended.

### `Makefile` Operations

  * Fetch kernel sources, build and test all ports with `make all`.
  * Fetch kernel sources with `make fetch`.
  * Build and test the CLisp port with `make clisp`.
  * Build and test the Clozure port with `make ccl`.
  * Build and test the SBCL port with `make sbcl`.
  * Build and test all ports with `make build-test-all` or just `make`.
  * Build all ports with `make build-all`.
    * Build only the CLisp port with `make build-clisp`.
    * Build only the Clozure port with `make build-ccl`.
    * Build only the SBCL port with `make build-sbcl`.
  * Test all ports with `make test-all`.
    * Test only the CLisp port with `make test-clisp`.
    * Test only the Clozure port with `make test-ccl`.
    * Test only the SBCL port with `make test-sbcl`.
  * Run Shen REPL for CLisp port with `make run-clisp`.
  * Run Shen REPL for Clozure port with `make run-ccl`.
  * Run Shen REPL for SBCL port with `make run-sbcl`.

## Running

An executable is generated for each platform in its platform-specific output directory under `native/` (e.g. `native/sbcl/shen.exe`). Per typical naming conventions, it is named `shen.exe` on Windows systems and just `shen` on Unix-based systems.

Startup scripts can be specified on the command line by preceding them with a `-l` flag. If any startup scripts are specified this way, they will be loaded in order and then `(exit 0)` will be called. If none are, the Shen REPL will start as usual. Either way, all command line arguments will be accessible with `(command-line)`.

When starting Shen via `make`, command line arguments can be passed through like this: `make run-sbcl Args="-l bootstrap.shen otherthing --option 123"`.
