# var'aq Reference Implementation 9/20/2000

**_var'aq_ Release Notes**

_maintained by [Brian Connors](mailto:connorbd@yahoo.com) revised 2 January
2001_

## Version Information

This is the status of the _var'aq_ project as of 20 September 2000.

This is the **Azetbur** release, after Chancellor Gorkon's daughter and
successor in _Star Trek VI: The Undiscovered Country_.

## Status Summary

We are moving ahead! Console I/O (on a very rudimentary level) is here, as well
as much of the mathematical functionality and string handling. Lists are not
here yet, and a more robust I/O model must await a better understanding of
Klingon hacker culture to understand issues like authentication and how
distributed processing might be used.

This release is approaching usability. Files are not here yet (still under
discussion), but there is console-level I/O and enough string support to do
something useful.

[j proctor](mailto:jproctor@oit.umass.edu) from the _varaq-dev_ mailing list
has contributed some sample code and a more flexible translator program than
the one I wrote and distributed. His interpreter will be found in the
_translators_ directory.

## Interpreter Status

The interpreter is available with both Klingon and English keywords; however,
keep in mind that maintenance is done mostly on the English version and the
translator program is not ready for prime time. This will be fixed eventually.

The following keywords are currently supported:

*   Control Structures
    *   **ifyes/HIja'chugh**
    *   **ifno/ghobe'chugh**
    *   **choose/wIv**
    *   **~ (quote/lI'moH)**
    *   **name/pong**
    *   **set/cher**
    *   **repeat/vangqa'**
    *   **eval/chov**

*   Stack Operations
    *   **pop/woD**
    *   **dup/latlh**
    *   **exch/tam**
    *   **clear/chImmoH**
    *   **remember/qaw**
    *   **forget/qawHa'**

*   Arithmetic Operators
    *   **add/boq**
    *   **sub/boqHa'**
    *   **mul/boq'egh**
    *   **div/boqHa'egh**
    *   **mod/chuv**
    *   **pow/law'qa'moH**
    *   **rand/mIS**
    *   **add1/wa'boq**
    *   **sub1/wa'boqHa'**
    *   **pi/HeHmI'**
    *   **e/ghurmi'**
    *   **clip/poD**
    *   **smooth/Hab**
    *   **howmuch/'ar**

*   Trig/Log operators
    *   **sin/joq**
    *   **cos/joqHa'**
    *   **tan/qojmI'**
    *   **atan/qojHa'**
    *   **ln/ghurtaH**

*   Relational Operators
    *   All relational operators have been implemented. Thanks to j proctor for
        **null?/pagh'a', negative?/taH'a', int?/HabmI''a'**, and
        **number/mI''a'**.

*   I/O Operators
    *   The _var'aq_ I/O model remains to be defined, but the basic console I/O
        functions are now present.

*   List Operators
    *   List support does not exist yet.

*   String Operators
    *   The current set of operators is sufficient to implement the others in
        the spec, but they are a lower priority.
        *   **strtie/tlheghrar**
        *   **streq?/tlheghrap'a'**
        *   **strcut/tlhleghpe'**
        *   **strmeasure/tlheghjuv**
        *   **compose/naQmoH**

## Implementation Issues and/or Bug Fixes

*   The interpreter now knows to ignore hashbang (i.e.
    #!/usr/bin/varaq-whatever) lines. They can double as end-of-line comments
    if you like, but you really shouldn't; these are here primarily to allow
    the forthcoming _vqmake_ program to spit out program files that a Unix
    shell can execute directly (which would be .vqx files on any other
    platform).
*   Took the "\\t" out of disp/cha' to facilitate a possible CGI conversion.
    Better formatted output will be a priority very shortly.
*   The interpreter also doesn't see lines beginning with //. This is to allow
    for static linking of .vql files (though if someone wants to implement
    _var'aq_ "shared libraries" I'll be glad to add the revs to the
    interpreter).
*   Cleaned up the execution logic a bit -- the code to execute a proc object
    was already in there about four times and was about to go in again for
    compose/naqmoH, so I abstracted it into a routine called execblock() per
    Chris' advice (RTFC).
*   Merged in j proctor's additions.

## Specification Status

A few changes:

*   A number of operators have been added:
*   **//_name_** -- equivalent to C `#include`.
*   Numerous "constants" (actually more like environment variables).
*   Several operators have been renamed:
*   **strcat** is now **strtie** to bring it in line with the Klingon
    **tlheghrar**.
*   The basic arithmetic operators have been given new Klingon names to
    coincide with recent additions to the Klingon linguistic canon.
*   More coinages in the section headings.

## Acknowledgements

The [varaq-dev](http://www.egroups.com/group/varaq-dev) mailing list,
especially [j proctor](mailto:jproctor@oit.umass.edu) for his code
contributions and Alan Anderson for providing the canonical Klingon math
operators, and to Glenn Gaslin for the impetus to finally get this thing out
the freakin' door.

---

Click [here](http://www.geocities.com/connorbd/varaq) to go to the _var'aq_
home page.
