Table of Contents
=================
* [Intro](#intro)
* [Instructions (Quick Start)](#instructions-quick-start)
* [Other Tools](#other-tools)
  * [Tools](#tools)
    * [Release Notes Gathering](#release-notes-gathering)

# Kubernetes Release Process

This repo contains the release infrastructure for
[Kubernetes](https://github.com/kubernetes/kubernetes).

## Intro

Kubernetes releases are done by the Kubernetes team at Google due to
permissions and other restrictions.  This may expand eventually to allow
other Kubernetes contributors to generate releases.

The current process runs by default in *mock* mode and anyone should
be able to run it in this mode to see exactly how the process works.
In *mock* mode all the code paths are followed for a release, but nothing
is pushed to repositories.

Sticking with the ancient Greek theme, the release script is called `anago`.
Anago means, in the context of navigators and shipping:
"to launch out, set sail, put to sea."

Tools in this repository includes a familiar [\*nix-style man
page](https://github.com/kubernetes/release/blob/master/anago) with usage,
process and examples.  The link shows how the self-contained doc/man page
makes up the header of the script itself and the same info is available
on the command-line (or get usage simply by calling the script with no options):

```
$ anago -man
```

The idea is that no external doc updates should be necessary and the
tool itself contains all of the details and instructions and prerequisite
checks needed for anyone to run the tool in at least mock mode.

There is a simple $USER check to ensure that noone but a certain few people can
run the script with --nomock to perform a real release.

## Instructions (Quick Start)

The tool was designed to require minimal inputs.
The only information the tool needs is to know where you want to create a
release with one optional flag `[--official]` \(used on release-\* branches only\).

Try an alpha release:
```
$ anago master
```

Try a beta release on a branch:
```
$ anago release-1.2
```

Try an official release on a branch:
```
$ anago release-1.2 --official
```

Try a beta release on a new branch:
```
$ anago release-9.9
```

Try creating a new branch and beta for an emergency zero-day fix:
```
$ anago release-9.9.9
```

## Other Tools

All standalone scripts have embedded man pages.  Just use `-man` to view or
your favorite editor.

### Tools

* [mailer](https://github.com/kubernetes/release/blob/master/mailer) : Generic mail interface (due to Google's deprecation of sendmail)
* [find_green_build](https://github.com/kubernetes/release/blob/master/find_green_build) : Ask Jenkins for a good build to use
* [script-template](https://github.com/kubernetes/release/blob/master/script-template) : Generate a script template in the kubernetes/release ecosystem
* [relnotes](https://github.com/kubernetes/release/blob/master/relnotes) : Scrape github for release notes \(See below for more info\)

### Release Notes Gathering

```
# get details on how to use the tool
$ relnotes -man
$ cd /kubernetes

# Show release notes from the last release on a branch to HEAD
$ relnotes

# Show release notes from the last release on a specific branch to branch HEAD
$ relnotes --branch=release-1.2

# Show release notes between two specific releases
$ relnotes v1.2.0..1.2.1 --branch=release-1.2
```

Please report *any* [issues](https://github.com/kubernetes/release/issues)
you encounter.
