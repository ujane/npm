npm-version(1) -- Bump a package version
========================================

## SYNOPSIS

    npm version [<newversion> | major | minor | patch | premajor | preminor | prepatch | prerelease]

    'npm -v' or 'npm --version' to print npm version
    'npm view <pkg> version' to view a package's published version
    'npm ls' to inspect current package/dependency versions

## DESCRIPTION

Run this in a package directory to bump the version and write the new
data back to `package.json` and, if present, `npm-shrinkwrap.json`.

The `newversion` argument should be a valid semver string, *or* a
valid second argument to semver.inc (one of `patch`, `minor`, `major`,
`prepatch`, `preminor`, `premajor`, `prerelease`). In the second case,
the existing version will be incremented by 1 in the specified field.

If run in a git repo, it will also create a version commit and tag, and fail if
the repo is not clean.  This behavior is controlled by `git-tag-version` (see
below), and can be disabled on the command line by running `npm
--no-git-tag-version version`

If supplied with `--message` (shorthand: `-m`) config option, npm will
use it as a commit message when creating a version commit.  If the
`message` config contains `%s` then that will be replaced with the
resulting version number.  For example:

    npm version patch -m "Upgrade to %s for reasons"

If the `sign-git-tag` config is set, then the tag will be signed using
the `-s` flag to git.  Note that you must have a default GPG key set up
in your git config for this to work properly.  For example:

    $ npm config set sign-git-tag true
    $ npm version patch

    You need a passphrase to unlock the secret key for
    user: "isaacs (http://blog.izs.me/) <i@izs.me>"
    2048-bit RSA key, ID 6C481CF6, created 2010-08-31

    Enter passphrase:

If `preversion`, `version`, or `postversion` are in the `scripts` property of
the package.json, they will be executed as part of running `npm version`.
`preversion` and `version` are executed before bumping the package version, and
`postversion` is executed afterwards. For example, to run `npm version` only if
all tests pass:

    "scripts": { "preversion": "npm test" }

## CONFIGURATION

### git-tag-version

* Default: true
* Type: Boolean

Commit and tag the version change.

## SEE ALSO

* npm-init(1)
* npm-run-script(1)
* npm-scripts(7)
* package.json(5)
* semver(7)
* config(7)
