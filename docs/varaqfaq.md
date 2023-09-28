# Everything you were about to ask...

**The _var'aq_ FAQ List**

_created by [Brian Connors](mailto:connorbd@yahoo.com)  
created 19 May 2000  
last updated 17 July 2000_

This document attempts to answer some of the more likely questions about
_var'aq_: what it is, where to get it, where to find more about it. It's not a
tutorial or a spec; there are other documents that describe that.

1.  What is Var'aq?

Var'aq (more properly, _var'aq_) is sort of a fanfic programming language based
on the Klingon language used on the [Star Trek](http://www.startrek.com)
television series and movies. Klingon, created by Marc Okrand and "maintained",
in a sense, by the [Klingon Language Institute](http://www.kli.org)
independently of Paramount's auspices, is really its own separate deal; this is
merely a fan's attempt to give a little more richness to the culture as well as
exercising a love of languages and a desire to learn more Perl.

2.  Where can I find out more about it?

The _var'aq_ home page is located at
[http://www.geocities.com/connorbd/varaq](http://www.geocities.com/connorbd/varaq).
You should be able to find pretty much everything interesting about the
language here, including specifications, sample code, and implementation notes.

As of this writing, the interpreter is in a basically functional state but
implements less than half of the specification. Just something you should keep
in mind.

3.  I heard something about a "Klingon Forth". Is this it? And why isn't it
called _loSDIch_?

Yes, in a way. It's a stack-based RPN language like Forth or PostScript; the
reason for this has nothing to do with an original desire to emulate one of
those languages, but simply the unusual object-verb-subject syntax of Klingon.
This sort of dictated the required form of the language right up front, ruling
out a more traditional ALGOL-like syntax (based on English). Stack-based
languages are actually easier to parse anyway, especially in Perl: just chomp
and process. It is also an impure functional language in the same vein as Lisp
or ML; it supports local variables, but it is really intended to do everything
off the stack.

As for calling it _loSDIch_ (Klingon for _fourth_), that would be an obvious
joke title to anyone who actually spoke Klingon; this being at least a
semi-serious exercise in artificial culture development, such a title would be
noticeably silly at best. _var'aq_ is actually completely meaningless, though
it suggests identification with a famous Klingon mathematician or computer
scientist in sort of the same way as Pascal recalls Blaise Pascal or Ada
recalls Ada Lovelace. In any case, the name _var'aq_ came before the form of
the language. (In any case, _var'aq_ is based more directly on PostScript
anyway. But they're all part of the same family.)

4.  So what is this thing eventually going to be able to do?

Eventually? A lot. The intent is to offer such things as concurrency and even
distributed processing support at some point (imagine that, a toy language
designed for a Beowulf cluster), perhaps even basic windowing support or the
like. Right now, I'm just shooting for such fancy features as, say, functions.
Or loops. String support. That sort of thing.

5.  Describe _var'aq_ for me in terms of other languages. You know, like a car
or a beer or something like that.

As stated above, _var'aq_'s closest cyberlinguistic relative is probably
PostScript, with a dash of Lisp thrown in. (This, incidentally, is sort of a
Perl artifact, since Perl data typing is incredibly lax. It's just the easiest
way to write it.)

Chris Pressey, creator of the notorious Befunge language, maintains a list of
programming languages described as cars; in those terms, _var'aq_ would be
described thusly: _A 2000 VW Turbo Beetle with lots of amateurishly drawn Star
Trek graphics painted 60s-style on the doors, a Starfleet Academy sticker in
the window, and a custom car radio and A/C system run completely off an HP
calculator._

In terms of genetics, _var'aq_ is the bastard child of a back-room tryst
between PostScript and Lisp after a Star Trek convention.

In terms of beer... _var'aq_ is bloodwine. Serve hot, drink carefully because
it'll mess you up if you don't.

There is a _var'aq_ 99 Bottles Of Beer program, but since it won't yet parse I
won't be posting it right yet.

6.  Why doesn't this construct translate to its PostScript/Forth equivalent?

The question is one of verisimilitude. The likelihood of a Klingon concept
being an exact translation of its English equivalent isn't always good.
Consequently, pure translation of an Earth language might make for a cute joke,
but it would sacrifice plausibility. A prime example is the _qaw/qawHa'_
instructions, which perform the same function as PostScript's
_mark/cleartomark_ instructions but literally translate to _remember/forget_;
the idea is that the metaphor chosen in Klingon might more reflect the purpose
of marking the stack than the actual act. Incidentally, It's quite true that
many of the idioms chosen for _var'aq_ are anything but obvious. This is the
reason why; though mathematics is considered universal, it's not too likely
that everything would be described in the same way. (That said, I did cheat in
a few places; for example, the word for logarithm is a direct translation from
the Greek _logarithmos_, meaning roughly "logic-number".)

For a rather thorough and creative discussion on the issues involved in
translation, you might wish to look at _Le ton beau de Marot_ by Douglas
Hofstadter (the author of the hacker classic _Goedel, Escher, Bach: An Eternal
Golden Braid_), an intricate and well-written look at the pitfalls of
translation between languages.

7.  Does Paramount know about this?

Not until someone sends me Michael Okuda's email address. (NB Michael Okuda is
the visual effects guy that created the modern Starfleet look and feel. I think
he'd be interested, but I make no assumptions about officialdom.)

8.  Does the KLI know about this?

As a matter of fact, yes. [Mark Shoulson](mailto:mark@kli.org) is the project's
Head Linguistic Consultant and is in great measure responsible for getting the
spec to reflect real Klingon constructions.

9.  Why isn't the Klingon version guaranteed to be in sync with the English
version?

Good question. The answer is that I don't speak Klingon; as a linguistic work
of art, it's a beauty, but I don't have much reason to learn it. As a result,
the Klingon version is mechanically translated via a Perl filter from English
to Klingon so I don't have to waste time synchronizing two separate source
bases.

10.  Will there ever be...

*   ...a _var'aq_\-to-C compiler?: Not likely. Such a beast would essentially
    spew out function calls to simulate _var'aq_ operators and control
    structures and would therefore be a gigantic mess.
    
*   ...a version not written in Perl?: Eventually, mainly because I'd love to
    get this running on a PalmPilot. The Perl implementation is phenomenally
    ugly anyway, so a serious rewrite in C would definitely be in order at some
    point. Some might, for example, actually find _var'aq_ useful for the
    occasional scripting job, and running an interpreter on an interpreter is
    if nothing else a great way to waste tremendous amounts of time.
    
*   ...a non-Unix version?: _var'aq_ should run as is on any platform that can
    handle Perl. Mac, Unix, Windows, whatever. Next question.
    
11.  Who is responsible for this?: The principal members of the team as of this
     version of the FAQ are:

*   [Brian Connors](mailto:connorbd@yahoo.com) -- Brian created the concept and
    is currently doing most of the implementation work and documentation. He's
    mostly a Perl-Linux-MacOS hacker and is currently available for employment;
    see his [resume](http://www.geocities.com/connorbd/resume3.html) if you're
    looking. He also considers himself something of an [Open
    Source](http://www.opensource.org) activist and considers _var'aq_ his most
    worthwhile contribution to the movement so far.
*   [Chris Pressey](http://www.catseye.mb.ca) -- Chris knocked around a number
    of ideas for the _var'aq_ system in the early planning stages of the
    project and provided the first draft of Bearfood, a very, very small Forth
    interpreter in Perl that provided the guts of the procedure definition
    code. Chris' biggest area of expertise is pushing the frontiers of
    programming language design; check out his [Cat's Eye Technologies Esoteric
    Topics](http://www.catseye.mb.ca/esoteric) web page if you'd like to see
    some of his better-known work (especially Befunge, a language that may have
    displaced Intercal as one of the most perverse in existence).
*   [Mark Shoulson](mailto:mark@kli.org) -- One of the higher-ranking members
    of the [Klingon Language Institute](http://www.kli.org), Mark, being the
    only one of us who actually speaks Klingon, is our linguistics consultant.
    His role so far has been making sure that the Klingon words in the spec
    actually mean what they're supposed to mean, a job important enough that he
    gets coauthor credit with Brian and Chris.

Shouts out go to j proctor and Alan Anderson from the _varaq-dev_ mailing list
for their contributions as well.

12.  Can I copy/borrow _var'aq_?

The spec is as open as any such spec gets. Feel free to implement your own; if
you want to use our code it's freeware under the [Mozilla Public
License](http://www.mozilla.org) (Why not GPL? That's a [separate
document](http://www.geocities.com/connorbd/stallman.html)...). As mentioned
above, Brian's heavy into that open source thing, so naturally in peer review
we trust. Of course, you should acknowledge us, and we'd obviously love a cut
of anything you happen to make off our work...

13.  Where can I find out more about _var'aq_?

You can go to the [_var'aq_ home page](http://www.geocities.com/connorbd/varaq)
at Yahoo! Geocities to find out everything there is to know about _var'aq_. At
the website, you'll find all sorts of useful information (most of which is
included with the distribution) as well as instructions for subscribing to the
`varaq-dev` mailing list at [eGroups](http://www.egroups.com). Good lu...er...
Qapla'!

---

Click [here](index.html) to return to the _var'aq_ home page.  
Click [here](http://www.geocities.com/connorbd) to return to 2266 Research
Triangle.
