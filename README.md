# SnapRAID Runner Script Plus

This script runs snapraid and sends its output to the console, a log file and
via email. All this is configurable.

It can be run manually, but its main purpose is to be run via cronjob/windows
scheduler.

It supports Windows, Linux and macOS and requires at least python3.7.

## How to use

* If you don’t already have it, download and install
  [the latest python version](https://www.python.org/downloads/).
* Download [the latest release](https://github.com/Chronial/snapraid-runner/releases)
  of this script and extract it anywhere or clone this repository via git.
* Copy/rename the `snapraid-runner.conf.example` to `snapraid-runner.conf` and
  edit its contents. You need to at least configure `snapraid.executable` and
  `snapraid.config`.
  * [The wiki](https://github.com/Chronial/snapraid-runner/wiki/How-to-use-snapraid-runner-with-gmail)
    has details on how to use gmail for sending mail.
* Run the script via `python3 snapraid-runner.py` on Linux or
 `py -3 snapraid-runner.py` on Windows.

## Features

* Runs `diff` before `sync` to see how many files were deleted and aborts if
  that number exceeds a set threshold.
* Can create a size-limited rotated logfile.
* Can send notification emails after each run or only for failures.
* Can run `scrub` after `sync`
* Can run `smart`. For this to work, you need [smartmontools](https://www.smartmontools.org/wiki/Download).
  Most Linux distributions will have it installed installed by default.
  * Windows users may install using the packaged .exe installer found at this link or
    use [Chocolatey](https://chocolatey.org/) (i.e., `choco install smartmontools`).
  * Mac OS users may install using the packaged .dmg installer found at this link or
    use [Homebrew](https://brew.sh/) (i.e., `brew install smartmontools`).
  * Linux users may check for smartmontools using `smartctl -V`, if not installed use
    your distribution's package manager to install `smartmontools`
    (e.g., `apt-get install smartmontools`, `yum install smartmontools`, etc.)

## Scope of this project and contributions

Snapraid-runner is supposed to be a small tool with clear focus. It should not
have any dependencies to keep installation trivial. I always welcome bugfixes
and contributions, but be aware that I will not merge new features that I feel
do not fit the core purpose of this tool.

I keep the PRs for features I do not plan on merging open, so if there's a
feature you are missing, you can have a look
[at the open PRs](https://github.com/Chronial/snapraid-runner/pulls).

## Changelog

### [v1.0] - (Unreleased)

* Track the version number in code.
* Add support for running `snapraid smart` (by k3vmcd, [#15])
* Add support for `sync --pre-hash`

[v1.0]: https://github.com/triple-j/snapraid-runner-plus/compare/v0.6-rc1...v1.0
[#15]: https://github.com/Chronial/snapraid-runner/pull/15

### [v0.6-rc1] - 2021-10-31 (last `snapraid-runner` release)

* Add `--ignore-deletethreshold` (by exterrestris, [#25])
* Add support for `scrub --plan`, replacing `--percentage` (thanks to fmoledina)
* Remove snapraid progress output. Was accidentially introduced with python3
  support.

[v0.6-rc1]: https://github.com/triple-j/snapraid-runner-plus/compare/v0.5...v0.6-rc1
[#25]: https://github.com/Chronial/snapraid-runner/pull/25

### [v0.5] - 2020-11-17

* Remove (broken) python2 support
* Fix snapraid output encoding handling (by hyyz17200, [#31])
* Fix log rotation (by ptoulouse, #36)

[v0.5]: https://github.com/triple-j/snapraid-runner-plus/compare/v0.4...v0.5
[#31]: https://github.com/Chronial/snapraid-runner/pull/31

### [v0.4] - 2019-08-16

* Add compatibility with python3 (by reed-jones)
* Add support for running `snapraid touch` (by ShoGinn, [#11])
* Add SMTP TLS support

[v0.4]: https://github.com/triple-j/snapraid-runner-plus/compare/v0.3...v0.4
[#11]: https://github.com/Chronial/snapraid-runner/pull/11

### [v0.3] - 2017-07-20

* Limit size of sent emails

[v0.3]: https://github.com/triple-j/snapraid-runner-plus/compare/v0.2...v0.3

### [v0.2] - 2015-04-27

* Fix compatibility with Snapraid 8.0
* Allow disabling of scrub from command line

[v0.2]: https://github.com/triple-j/snapraid-runner-plus/compare/v0.1...v0.2

### [v0.1] - 2014-02-16

* Initial release

[v0.1]: https://github.com/triple-j/snapraid-runner-plus/releases/tag/v0.1
