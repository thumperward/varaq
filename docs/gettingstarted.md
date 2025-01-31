# Getting started with var'aq

This is a quick and dirty guide to getting started with var'aq. It was written
for those using var'aq on Linux; it shouldn't be that different on Windows.

This tutorial isn't meant for a beginning programmer; if you're not familiar
with the process of programming var'aq isn't your kind of toy just yet. In case
you've been breezing through the docs too fast to pick up on this, var'aq is an
RPN-based, impure functional language in the style of PostScript or False. It
works at a very basic level at this point -- string handling is minimal, and
all data types are scalar except functions -- but it works well enough to write
some primitive code. The purpose of this tutorial is to give the beginning
var'aqer an idea of what var'aq code looks like (in both English and Klingon)
and how it works.

## Starting the interpreter

There are two interpreters, one that accepts Klingon keywords, one that accepts
English. We'll give samples in Klingon and English.

To get started, type:

```sh
perl varaq-engl

```
or 

```sh
perl varaq-kling
```

at the shell prompt. The interpreter will start. Note that there is no var'aq
system prompt in the current implementation.

Note that talking directly to the interpreter can be impressively frustrating
since you're dealing with raw STDIN. You'll have to keep retyping if you make a
mistake. 

## Saying Hello

Start with a simple "hello, world!" program:

Klingon:

```varaq
~ nuqneH { "nuqneH 'u'?" cha' } pong
```

English:

```varaq
~ hello { "What do you want, Universe?" disp } name
```

Broken down:

`~`: forces the interpreter to push the next token on the stack	as a literal
`nuqneH` / `hello`: identifier for the routine `{`: begins a function
definition `"..."`: string literal `cha'` / `disp`: pops the top object on the
stack and prints it out `}`: ends a function definition `pong` / `name`: binds
a function to a procedure name

To run it, simply type the name of the function at the var'aq command line.

var'aq, as you can see, is a stack-based language like Forth or PostScript;
that's a relic of the Klingon language itself. As you'll find out, it's also a
functional language; variables are there, but somewhat difficult to use at this
point. 

var'aq does accept recursive procedure calls; try the following: 

```varaq
~ mevbe' { wa'boq latlh cha' mevbe' } pong
~ neverend { add1 dup disp neverend } name
```

This snippet produces an ever-rising string of numbers; you'll have to kill the
interpreter to stop it. 

## Math

The var'aq spec allows for a fairly complete set of mathematical operators;
we'll focus on basic arithmetic for now. Try some simple calculations:

```varaq
2 2 add disp
2 2 boq cha'
	4
3 2 sub disp
3 2 boqHa' cha'
	1
4 -8 mul disp
4 -8 boq'egh cha'
	-32
7.5 3 div disp
7.5 3 boqHa''egh cha'
	2.5
9 2 mod disp
9 2 chuv cha'
	1
```

## Conditionals

Since var'aq is a functional language, it doesn't need much more than a
conditional construct to do its work. There are actually two.

```varaq
3 2 law''a' { "HIja'" cha' } HIja'chugh
	HIja'
3 2 gt? { "yes" disp } ifyes
	yes

6 5 law''a' { "ghobe'" disp } ghobe'chugh
	ghobe'
6 5 gt? { "no" disp } ifno
	no
```
## Putting it all together

Now try something nontrivial. 

```varaq
(* countdown in Klingon *)
~ toghHa' 
	{ latlh 0 law'rap'a' 
		{ latlh cha' wa'boqHa' toghHa' }
	HIja'chugh }
pong

(* countdown in English *)
~ countdown 
	{ dup 0 ge?
		{ dup disp sub1 countdown }
	ifyes }
pong
```

This function takes one argument (an integer) and prints out a countdown to
zero. 

## Continuing

This only scratches the surface of var'aq, but if you're playing with it this
early on in the development cycle you've already seen everything you need to.
You should be able to write a fair amount of usable code at this point, even
with the interpreter (and standard) in the incomplete state it's in. 

Sample code can be piped in using the syntax

```sh
perl varaq-kling < bottles.vq
```

or you can simply type directly at the interpreter (though that tends to
produce a lot of headaches). 

If you have some useful sample code that you've written or would like to
contribute extra documentation (including spec proposals and tutorial docs),
contact me at connorbd@yahoo.com or join the varaq-dev mailing list at
egroups.com; details on how to do so are at the var'aq home page at 

<http://www.geocities.com/connorbd/varaq>

Code contributions should be plain text files; code-only files should use the
extension .vq (for Klingon var'aq) or .vqe (for English). Code libraries (using
the extension .vql) will be accepted, but are not yet supported as such.
Documentation should be in plain text, HTML, or PDF formats; PostScript is
acceptable but deprecated, and anything else will be ignored.

Qapla'!

Brian Connors 7/18/2000
