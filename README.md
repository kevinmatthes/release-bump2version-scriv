<!---------------------- GNU General Public License 3.0 ------------------------
--                                                                            --
-- Copyright (C) 2023 Kevin Matthes                                           --
--                                                                            --
-- This program is free software: you can redistribute it and/or modify       --
-- it under the terms of the GNU General Public License as published by       --
-- the Free Software Foundation, either version 3 of the License, or          --
-- (at your option) any later version.                                        --
--                                                                            --
-- This program is distributed in the hope that it will be useful,            --
-- but WITHOUT ANY WARRANTY; without even the implied warranty of             --
-- MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the              --
-- GNU General Public License for more details.                               --
--                                                                            --
-- You should have received a copy of the GNU General Public License          --
-- along with this program.  If not, see <https://www.gnu.org/licenses/>.     --
--                                                                            --
------------------------------------------------------------------------------->

<!------------------------------------------------------------------------------
--
--  AUTHOR      Kevin Matthes
--  BRIEF       Important information regarding this project.
--  COPYRIGHT   GPL-3.0
--  DATE        2023
--  FILE        README.md
--  NOTE        See `LICENSE' for full license.
--
------------------------------------------------------------------------------->

# release-bump2version-scriv

## Summary

[![](https://bors.tech/images/badge_small.svg)](https://app.bors.tech/repositories/60643)
[![](https://github.com/kevinmatthes/release-bump2version-scriv/workflows/ci/badge.svg)](https://github.com/kevinmatthes/release-bump2version-scriv/workflows/ci)
[![](https://img.shields.io/github/license/kevinmatthes/release-bump2version-scriv)](https://github.com/kevinmatthes/release-bump2version-scriv)

A GitHub Action to prepare a release using bump2version and Scriv.

1. [License](#license)
2. [Description](#description)
3. [Inputs](#inputs)
   1. [`cff`](#cff)
   2. [`release`](#release)

## License

[![](https://img.shields.io/github/license/kevinmatthes/release-bump2version-scriv)](https://github.com/kevinmatthes/release-bump2version-scriv)

This project's license is **GPL-3.0**.  The whole license text can be found in
`LICENSE` in the main directory of this repository.  The brief version is as
follows:

> Copyright (C) 2023 Kevin Matthes
>
> This program is free software: you can redistribute it and/or modify
> it under the terms of the GNU General Public License as published by
> the Free Software Foundation, either version 3 of the License, or
> (at your option) any later version.
>
> This program is distributed in the hope that it will be useful,
> but WITHOUT ANY WARRANTY; without even the implied warranty of
> MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
> GNU General Public License for more details.
>
> You should have received a copy of the GNU General Public License
> along with this program.  If not, see <https://www.gnu.org/licenses/>.

## Description

This GitHub Action will prepare a new release using bump2version and Scriv.
The former will increment the version numbers as specified, the latter will
assemble the CHANGELOG based on both the stored fragments as well as its
settings.  The user creating the corresponding commit will be the GitHub Actions
bot.

It is recommended to execute this Action on a Linux runner.  This Action
requires a Bash shell environment.  The repository needs to be checked out
before the Action can be called.  After it has finished, the changeds need to
be pushed back to the repository.

This Action does not produce any output.  For information on the possible inputs,
see [Inputs](#inputs).

The branding settings (green background colour with the symbol `settings` as
icon) were chosen due to the default use case of this Action.  The settings icon
symbolises the prerequisites for a new release this Action will take care about.
The colour green is often associated with the season spring which also
symbolises the beginning of something new; here, it is the release which is
going to be prepared.

To apply this Action, just add the following lines to the step section of a
GitHub Action workflow job.  It is assumed that there is an input named
"release", storing the increment level for bump2version.

```yaml
      - uses: kevinmatthes/release-bump2version-scriv@v0.2.1
        with:
          release: ${{ inputs.release }}
```

# Inputs

## `cff`

This **optional** information controls whether there is a CITATION.cff in the
repository root to be updated on release.  Allowed values are `true` and
`false`.

In case that the given value neither equals `true` nor `false`, the Action will
fail with exit code 64.  This is the code for wrong user input according to
`sysexits.h`.

As it is recommended to configure a CITATION.cff, the default value is `true`,
if omitted.

## `release`

This is a **required** information.  It is the increment level to be passed to
bump2version.  It is highly recommended to ensure that the value which is given
in this field matches the configured increment levels of the respective
repository calling this Action in a workflow.

<!----------------------------------------------------------------------------->
