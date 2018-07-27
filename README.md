# devtools <img src="man/figures/logo.png" align="right" />

[![Build Status](https://travis-ci.org/r-lib/devtools.svg?branch=master)](https://travis-ci.org/r-lib/devtools)
[![AppVeyor Build Status](https://ci.appveyor.com/api/projects/status/github/r-lib/devtools?branch=master&svg=true)](https://ci.appveyor.com/project/hadley/devtools)
[![Coverage Status](https://codecov.io/github/r-lib/devtools/coverage.svg?branch=master)](https://codecov.io/github/r-lib/devtools?branch=master)
[![CRAN_Status_Badge](http://www.r-pkg.org/badges/version/devtools)](https://cran.r-project.org/package=devtools)
[![Join the chat at https://gitter.im/r-lib/devtools](https://badges.gitter.im/r-lib/devtools.svg)](https://gitter.im/r-lib/devtools?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

The aim of `devtools` is to make package development easier by providing R
functions that simplify common tasks.

An R package is actually quite simple. A package is a template or set of
conventions that structures your code. This not only makes sharing code easy,
it reduces the time and effort required to complete you project: following a
template removes the need to have to think about how to organize things and
paves the way for the creation of standardised tools that can further
accelerate your progress.

While package development in R can feel intimidating, `devtools` does every
thing it can to make it less so. In fact, `devtools` comes with a small
guarantee: if you get an angry e-mail from an R-core member because of a bug in
`devtools`, forward me the email and your address and I'll mail you a card with
a handwritten apology.

`devtools` is opinionated about package development. It requires that you use
`roxygen2` for documentation and `testthat` for testing. Not everyone would
agree with this approach, and they are by no means perfect. But they have
evolved out of the experience of writing hundreds of R packages.

I'm always happy to hear about what doesn't work for you and where `devtools`
gets in your way. Either send an email to the [rdevtools mailing
list](http://groups.google.com/group/rdevtools) or file an [issue at the GitHub
repository](http://github.com/r-lib/devtools/issues).

## Updating to the latest version of devtools

You can track (and contribute to) the development of `devtools` at
https://github.com/r-lib/devtools. To install it:

1. Install the release version of `devtools` from CRAN with
   `install.packages("devtools")`.

2. Install the development version of devtools.

   ```r
   devtools::install_github("r-lib/devtools")
   ```

## Package development tools

All `devtools` functions accept a path as an argument, e.g.
`load_all("path/to/path/mypkg")`. If you don't specify a path, `devtools` will
look in the current working directory - this is recommended practice.

Frequent development tasks:

* `load_all()` simulates installing and reloading your package, loading R code
  in `R/`, compiled shared objects in `src/` and data files in `data/`. During
  development you usually want to access all functions (even un-exported
  internal ones) so `load_all()` works as if all functions were exported in the
  package `NAMESPACE`.

* `document()` updates generated documentation in `/man`, file collation and
  `NAMESPACE`.

* `test()` reloads your code with `load_all()`, then runs all `testthat` tests.

Building and installing:

* `install()` reinstalls the package, detaches the currently loaded version
  then reloads the new version with `library()`. Reloading a package is not
  guaranteed to work: see the documentation to `unload()` for caveats.

* `build()` builds a package file from package sources. You can use it to build
  a binary version of your package.

* `install_*` functions install an R package:
   * `install_github()` from github,
   * `install_gitlab()` from gitlab,
   * `install_bitbucket()` from bitbucket,
   * `install_url()` from an arbitrary url,
   * `install_git()` and `install_svn()` from an arbitrary git or SVN repository.
   * `install_local()` from a local file on disk.
   * `install_version()` installs a specified version from CRAN.

Check and release:

* `check()` updates the documentation, then builds and checks the package.
  `check_win()` builds a package using
  [win-builder](http://win-builder.r-project.org/), allowing you to easily
  check your package on windows.

* `run_examples()` will run all examples to make sure they work. This is useful
  because example checking is one of the later steps of `R CMD check`.

* `release()` makes sure everything is ok with your package (including asking
  you a number of questions), then builds and uploads to CRAN. It also drafts
  an email to let the CRAN maintainers know that you've uploaded a new package.

## Conscious uncoupling

devtools started off as a lean-and-mean package to facilitate local package
development, but over the years it accumulated more and more functionality.
Currently devtools is undergoing a [conscious
uncoupling](https://web.archive.org/web/20140326060230/http://www.goop.com/journal/be/conscious-uncoupling)
to split out functionality into smaller, more tightly focussed packages. This
includes:

* [pkgbuild](https://github.com/r-lib/pkgbuild): Building binary packages
  (including checking if build tools are available) (i.e. `build()`).

* [pkgload](https://github.com/r-lib/pkgload): Simulating package loading (i.e.
  `load_all()`).

* [rcmdcheck](https://github.com/r-lib/rcmdcheck): Running R CMD check and
  reporting the results (i.e. `check()`).

* [revdepcheck](https://github.com/r-lib/revdepcheck): Running R CMD check on
  all reverse dependencies, and figuring out what's changed since the last CRAN
  release (i.e. `revdep_check()`).

* [sessioninfo](https://github.com/r-lib/sessioninfo): R session info (i.e.
  `session_info()`).

* [usethis](https://github.com/r-lib/usethis): Automating package setup (i.e.
  `use_test()`).

Generally, you should not need to worry about these different packages, because
devtools installs them all automatically. You will need to care, however, if
you're filing a bug because reporting it at the correct place will lead to a
speedier resolution.

# Code of conduct

Please note that this project is released with a [Contributor Code of
Conduct](CONDUCT.md). By participating in this project you agree to abide by
its terms.
