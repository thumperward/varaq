# Var'aq

## Update 2023

This is a resurrected fork of the original GitHub copy. The use case for this
was to simplify using va'raq in CGI scripts. Please don't ask.

va'raq can now be run non-interactively with a script the usual way (by passing
the file in as $1 or using shebang) instead of having to use shell redirection
to pass files in via stdin. The usual header lines printed on interactive use
are suppressed if either stdin or a file argument are supplied.

Other new changes include:

-   A devcontainer configuration has been added, which allows for dependencies 
    to be described programmatically without need to install them locally on 
    supported IDEs (such as Visual Studio Code and IntelliJ).
-   The gitignore file has been regenerated using the Perl sample from 
    <https://gitignore.io>.
-   Shebangs and permissions have been updated on test files.
-   Test suite has been fixed (`tail -n` didn't like `+` before its count).
-   `sub1` was actually broken in Klingon, in both the test case and the 
    translator. The function in the Klingon source is named `wa'boqHa'` but it 
    was given as `wa'teq` in those files, meaning the sample didn't run.
-   One minor equality fix (thanks -W).
-   Cleanup of the documentation and conversion to markdown.

Some additional notes on the readme:

-   Generate the basic Docker image by running 
    `docker build -t bjtucker/varaq .` from the repository root.
-   Run the test suite with `bats test/` from the repository root.

Still to do:

-   The `vqmake` script appears to be empty: track it down.

Original documentation for the fork continues below.

## Original fork README

This is a copy of the var'aq language developed by Brian Connors, Chris
Pressey, and Mark Shoulson, which I downloaded from a geocities mirror and
uploaded to GitHub.

Since then, I've made a few changes focused on testing and integration. So far,
they are:

-   Automated some tests with BATS.
-   Dockerized.
-   Automated builds and testing with GitHub Actions.

The project as it was is not according to its specification, but enough of it
is implemented that the 99 bottles example runs with a minor spelling
correction.

The easiest way to try var'aq is to use its Docker image, which I have uploaded
to Docker Hub.

Try var'aq:

```bash
docker run -it bjtucker/varaq
```

If there is any other development or use of the var'aq language, I would love
to hear about it. Please open an issue!

I intend to continue adding my own contributions to the project as time permits
as a form of fandom and a learning experience. I welcome anyone who wishes to
join me.

Ben

![run
tests](https://github.com/bjtucker/varaq/actions/workflows/main.yml/badge.svg)

## Original README

This is var'aq, the first Klingon programming language. This is the Azetbur
('aDSetbur?) release, dated 1/05/2001, named for the Klingon chancellor Azetbur
gorqon puqbe' in Star Trek VI: The Undiscovered Country. 

It is to be considered an alpha release; for information on what it's capable
of, see the files current.html and gettingstarted.txt. 

var'aq was developed on a Linux system using Perl 5. If you are not currently
using a Unix-based system, you may want to rename the interpreter files
(varaq-engl and varaq-kling) with a .pl extension.

If this is your first exposure to var'aq, please read the FAQ (varaqfaq.html)
before you do anything else. You may also wish to subscribe to our eGroups
mailing list; the information is in the FAQ.

Thank you, enjoy, and Qapla'!

Brian Connors Chris Pressey Mark Shoulson 1/05/2001
