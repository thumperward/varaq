# var'aq Interim Specification 2 January 2001

**_var'aq_ Preliminary Specification**
  
_[Brian Connors](mailto:connorbd@yahoo.com)  
29 May 2000  
last updated 02 January 2001_

## 0 Introduction

This specification documents the programming language _var'aq_. _var'aq_ is a
programming language created as part of an exercise to imagine the hacker
culture of [Star Trek's](http://www.startrek.com) Klingon race. The Klingon
culture was chosen because it is probably the best-realized of all such
cultures in the Science Fiction/Fantasy genres of literature, and the Klingon
language is sufficiently different from English to make language design a
significant challenge.

### 0.1 Language Levels

_var'aq_ is divided into three implementation levels, each a subset of its
successor. An implementation conforming to the current _var'aq_ spec should be
labeled with the level of conformance.

*   **Level 0** -- The focus of this preliminary spec, a Level 0 _var'aq_
    implementation minimally contains all operators and data structures listed
    in this specification. Level 0 covers all basic mathematical, relational,
    and logical operators and a minimal set of Turing-complete control
    constructs and I/O operators. A Level 0 implementation does not necessarily
    have to be written in Klingon, but if not an external Klingon-to-English
    translation filter is required.
*   **Level 1** -- **NOT YET DOCUMENTED** -- A Level 1 implementation
    constitutes a full text-mode implementation of _var'aq_, including basic
    concurrency support, stream-based file I/O, support for the _var'aq_
    Standard MPI Binding (not yet available), and full support for
    Klingon-language constructs. Also includes support for packages
    (_jangwI'ghom_).
*   **Level 2** -- **NOT YET DOCUMENTED** -- A Level 2 implementation has all
    of the above, as well as package support, virtual device support
    (minimally, printer, framebuffer, and network connection as well as
    console), and is suitable for use as a scripting or systems programming
    language. A POSIX binding is optional but highly recommended.

## 0.2 Legalese, Credit, Etc.

_var'aq_ was concieved by [Brian Connors](mailto:connorbd@yahoo.com) and
implemented by Brian with help from [Chris Pressey](http://www.catseye.mb.ca)
and [Mark Shoulson](mailto:mark@kli.org). It is an independent project and is
not connected with the [Star Trek](http://www.startrek.com) people (i.e.
Paramount/Viacom).

This document is (c)2000-2001 Brian Connors and may be distributed freely as
long as this copyright notice is retained. You may freely implement for private
use a _var'aq_ implementation with no restriction; you must contact me for
certification (i.e. I make sure you're following the spec) in order to
distribute your implementation as freeware. This specification may not be used
for commercial purposes without a separate licensing arrangement.

## 0.3 Apologies

You'll notice that I tend to drift in and out of character in this document.
The only thing I can say to this is that character isn't a great concern in a
specification document; I may do an extensive revision later on, but as I write
this _var'aq_ isn't even alpha-quality code, and the spec is subject to change
anyway. Just enjoy and try to keep up; we'll worry about "realism" later. Thank
you for your patience.

## 1 Language Overview

_var'aq_ is a stack-based, RPN programming language with points of similarity
to Lisp, Forth, and PostScript. It is more of a functional language than an
imperative (Algol-like) language; most operations are dependent on the stack
and bypass the local variable store altogether.

### 1.1 Notation Used In This Specification

All operator names will be given in English and Klingon. The notation and
format of the operator entries are cribbed from [Adobe's](http://www.adobe.com)
PostScript Language Specification.

### 1.2 Basic Concepts

_var'aq_ is a fairly simple, RPN-based language where pretty much everything is
an operator. It is fairly loosely typed and little distinction is made between
code and data. Typechecking is not strictly required (and in fact does not
exist in the current reference implementation) but is encouraged.

### 1.3 Data Types

_var'aq_ recognizes only a few data types so as to keep the programming model
as simple as possible.

### 1.3.1 number/mI'

_var'aq_ numbers are a bit nonspecific as to representation; there is no
support for complex numbers in a Level 0 implementation (Level 1 and above do
include support). In general, integers (_HabmI'_) and reals are considered
interchangeable where possible, and the interpreter is expected to use
whichever is more efficient. Note that integer operations such as **Habwav**
and the bitwise operators will generally silently truncate the operands
(optionally giving a runtime warning if so requested by the user).

### 1.3.2 function/jangwI'

A function in _var'aq_ is understood to be much the same thing as a lambda
closure, i.e. a procedure with a return value (thus the Klingon term jangwI',
meaning "answerer"). Functions are defined using the **{ }** operators, and may
be assigned names using the **pong** operator.

### 1.3.3 list/ghomHom

_var'aq_ lists (_ghomHom_, meaning "cluster" (sort of)) are in some ways very
similar to those of Lisp.

### 1.3.4 string/tlhegh

Strings in _var'aq_ (and Klingon programming in general) seem to be considered
something of a black art; Klingon computer science appears to have no real
concept of anything like regular expressions, and as a result decent string
handling is the territory of those trusted to write things like language
compilers (ngoq poSmoH? The idea would baffle a Klingon... so insecure, so
random...). Brute-force string comparisons seem to be the order of the day in
current practice. That said, _var'aq_ strings also have a couple of important
properties: a) white space is not significant; b) they can be decomposed into
lists using the **joq** operator; and c) they can be used as literal names
(though it's not a terribly good idea).

### 1.4 Basic Assumptions

### 1.4.1 Number Representations

All standard _var'aq_ systems are assumed to be binary machines using eight or
sixteen-bit bytes (word size is unimportant). Negative integer values are
represented as two's-complement. A floating-point implementation is not
specified, though the Klingon floating-point standard is not drastically
different from IEEE floating point (differing bit positions, primarily). If a
standard float must be chosen, go with IEEE double-precision.

### 1.4.2 Garbage Collection

All _var'aq_ implementations are required to use garbage collection (_woDHa'_,
roughly meaning "retrieve" or "unwaste"). No standard algorithm is specified,
and this requirement may be ignored if the implementor uses an environment
where this is assumed (Perl, for example).

### 1.4.3 Filetypes

Klingon military computer systems use a sort of modular-database storage scheme
in which the concept of "file" doesn't mean a whole lot. However, on systems
where files are the common way of doing business, the following extensions and
MIME types are standard:

*   **.vq -- application/varaq** -- a standard _var'aq_ source file
*   **.vqe -- application/varaq-engl** -- an English-keyword _var'aq_ source
    file
*   **.vql -- application/vqlib** -- a _var'aq_ library source file
*   **.vqx -- application/vqexe** -- a _var'aq_ executable resource file

Note that this is being specified here mainly as a matter of convenience. The
_var'aq_ resource file format has not yet been defined.

## 2 Language Basics

This section describes the fundamental _var'aq_ language constructs and data
types.

### 2.1 Stack Operations

These operations directly manipulate the _var'aq_ operand stack. The operand
stack can hold any of four kinds of data: numbers (real or integer), strings,
functions, or arrays. It is best described as "translucent", similar to the
transparent stack of Forth or PostScript but somewhat more restricted. The
internal data representation of the stack is not available to the programmer.

### 2.1.1 pop/woD

_obj **woD** -_

Pops and discards the top item on the stack. The literal meaning is _discard_.

Errors: stackUnderflow

### 2.1.2 dup/latlh

_obj **latlh** obj obj_

Duplicates the top object on the stack.

Errors: stackUnderflow

### 2.1.3 exch/tam

_obj1 obj2 **tam** obj2 obj1_

Inverts the order of the top two objects on the stack.

Errors: stackUnderflow

### 2.1.4 clear/chImmoH

_... obj **chIm** -_

Empties the stack.

Errors: none

### 2.1.5 remember/qaw

_\- **qaw** flag_

Puts a flag (like PostScript's **mark**) on the stack. The internal
representation of the flag is not available to the programmer.

Errors: none

### 2.1.6 forget/qawHa'

_... flag ... **qawHa'** ..._

Clears the stack down to the flag and pops the flag. If there is no flag
present, the stack is emptied completely.

Errors: none

### 2.1.7 dump/Hotlh (lit. scan)

_... **Hotlh** ..._

Prints the contents of the operand stack to STDOUT without changing them.
_Note_: the _Hotlh_ operator is a debugging operator and is not intended for
use in programs; it is merely documented here because it might be useful to a
_var'aq_ developer. In particular, the output format of this operator is
implementation-defined and will not be specified in this document. _Hotlh_ may
be redefined to take such arguments as the implementor feels appropriate.

Errors: implementation-defined.

### 2.2 Data/Code Operations

_var'aq_, like many similar languages, does not distinguish between code and
data. These operations include operators to associate names with objects and
executable procedures, as well as operators to define and manage data
structures. Note that variables and procedures live in a common namespace,
since the act of pushing the content of a variable is essentially the same as
executing the variable's name.

### 2.2.1 ~ (quote/lI'moH)

_\- **~ obj** obj_

The ~ operator is a special form, as it is not a postfix operator. When the
interpreter encounters a ~, it pushes the next token on the stack as is
regardless of whether it is a defined name. (Attempting to push an undefined
name without a ~ will generate an undefinedName error.)

The literal meaning of this operator's name is "make useful". Errors: none

### 2.2.2 {

Begins the creation of an anonymous procedure. The process is
implementation-dependent.

### 2.2.3 }

_\- **}** proc_

Completes procedure construction and pushes a reference to the completed
procedure on the stack. Does not execute the procedure.

Errors: noDefinedProc

### 2.2.4 name/pong

_obj id **pong** -_

Associates _obj_ with _id_ and places it in the system lookup space.
Conventionally used to associate new operator names with procedure objects.

Example: _~ add3 { chel chel cha' } pong_

Pushes the name _add3_ and a procedure object on the stack, then binds the name
to the procedure.

Errors: stackUnderflow, noDefinedProc

### 2.2.5 set/cher

_obj id **cher** -_

Reassigns the value of a value already in the system lookup space. Used
primarily for variable assignments.

Errors: stackUnderflow, noSuchName

### 2.2.6 (\* ... \*) (comment)

Marks a comment in a program. All such comments are treated as single tokens
and ignored.

### 2.2.7 //_name_

Causes the interpreter to import a file with the name _name_.vql and execute it
as if it is part of the currently executing program. This can be handled by an
external static linker if there is no shlib-like facility in the interpreter.
Essentially equivalent to `#include` in C.

### 2.3 Control Flow

_var'aq_ supports a small but sufficient supply of conditional and iterative
operators.

### 2.3.1 ifyes/HIja'chugh

_bool proc **HIja'chugh** -_

Pops the proc object off the stack, then evaluates the boolean. If it's true,
the proc object is evaluated; otherwise, it's thrown out.

Errors: stackUnderflow, noDefinedProc

### 2.3.2 ifno/ghobe'chugh

_bool proc **ghobe'chugh** -_

Similar to _HIja'chugh_ above, but executes proc only if bool is false.

Errors: stackUnderFlow, noDefinedProc

### 2.3.3 choose/wIv

_bool **wIv** bool bool_

Duplicates a boolean value on top of the stack. Allows paired
HI'ja'chugh/ghobe'chugh clauses.

**Note:** To the untrained eye, it may seem as though wIv and latlh are
identical. This is true in the reference implementation, but may not be in any
version that actually does some level of type checking. This bit of syntactic
sugar should never be relied upon; always use wIv in this situation.

### 2.3.4 eval/chov

_proc **chov** -_

Pops a proc object off the stack and executes it.

Errors: stackUnderflow, noDefinedProc

### 2.3.5 escape/nargh

_bool **nargh** -_

Exit the current procedure. Useful for exit conditions on loops. Will terminate
the current session if used top-level.

### 2.3.6 repeat/vangqa'

_val proc **vangqa'** -_

Pops val and proc off the stack and executes proc val times.

### 2.4 List Operations

_var'aq_ supports a series of operators for management of lists (_ghomHom_,
which seems to mean something like "cluster"). These primitives are the
language's primary way of managing aggregate objects and work much like similar
operators in LISP; a more sophisticated paradigm, such as OO extensions or the
like, can be built with these operators.

Note that "objects" as they stand in _var'aq_ are largely singletons as in
JavaScript; there is no inherent concept of object-orientation or anything like
it in standard _var'aq_.

### 2.4.1 (

Begins a list definition.

### 2.4.2 )

_( item1 item2 ... **)** list_

Creates a list and pushes it onto the stack.

### 2.4.3 split/SIj

_list **SIj** item1 list_

Pops a list off the stack and returns the first item and the rest of the list.

### 2.4.4 cons/muv

_list item1 ... **muv** list_

Takes an object and adds it to the head of a list. Equivalent to the LISP
**cons** operator.

### 2.4.5 shatter/ghorqu'

_list **ghorqu'** item1 item2 ..._

Reduces a list to its component elements and pushes them on the stack in order.

**Note:** The precise meaning of the construction _ghorqu'_ is a bit obscure;
the rendering _shatter_ is idiomatic and may derive from a nonstandard dialect.
Standard Klingon would generally prefer _jor_, meaning _explode_.)

### 2.4.6 empty?/chIm'a'

_list **chIm'a'** bool_

Examines a list on the stack and returns 1 if its value is null (_pagh_), a 0
if it contains anything. **Note:** some implementations also have an operator
known as bite/_chop_, equivalent to the Lisp _cdr_. This is not required in any
standard _var'aq_ implementation and can easily be rendered by the function

    
    
    ~ chop { SIj woD } pong
    
    

### 2.5 String Operators  
_tlheghjangwI'mey_

String handling in _var'aq_ is generally thought to be somewhat deficient by
Earth standards; all strings are handled as if whitespace is not significant,
and string management is a bit primitive. Substrings are understood, as are
very basic forms of pattern matching, but Klingon computer science seems to
regard string-handling facilities such as regular expressions as something of a
black art, left only to those responsible for writing compilers and that sort
of thing.

### 2.5.1 strtie/tlheghrar

_str1 str2 **tlheghrar** str3_

Concatenates the top two strings on the stack into one.

### 2.5.2 compose/naQmoH

_mark str1 str2 ... strn **naQmoH** strn'_

Pops objects (executing proc objects if necessary) off the stack until a marker
(placed by **qaw**) is hit and combines them into one string.

### 2.5.3 streq?/tlheghrap'a'

_str1 str2 **tlheghrap'a'** bool_

Pops the top two strings on the stack, compares them, and returns 1 if
identical, 0 if not.

### 2.5.4 strcut/tlheghpe'

_str startval endval **tlheghpe'** substr_

Pops two values and a string and returns the section of the string between
character _startval_ and character _endval_.

### 2.5.5 strmeasure/tlheghjuv

_str **tlheghjuv** val_

Pops a string off the stack and returns its length in characters.

### 2.5.6 explode/jor

_str **jor** list_

Separates individual "words" in a string by whitespace.

## 3 Mathematical Operators  
_mI'jangwI'mey_

Klingon mathematical study is somewhat less sophisticated than Federation
standard, but it covers all the important concepts. A full set of arithmetic
and basic trigonometric operations is available.

### 3.1 Arithmetic Operations  
_toghwI'mey_

Arithmetic operators usually work with real numbers unless otherwise stated.
The number operators (sec 3.3) can convert them to integers if necessary.

_(note: verisimilitude would require that the Klingon understanding of math not
necessarily coincide with ours. But I think it's safe to say that this basic
set of operations is enough to at least get a Klingon battlecruiser out of
spacedock.)_

### 3.1.1 add/boq

_a b **boq** sum_

Pops the top two values on the stack and replaces them with their sum.

Note that the four basic operations are based around the term _boq_, which
literally means "to ally with". The metaphor is a bit strained but is
well-established enough that most Klingons do not think twice about it.

### 3.1.2 sub/boqHa'

_a b **boqHa'** difference_

Pops the top two values on the stack and replaces them with a - b.

### 3.1.3 mul/boq'egh

_a b **boq'egh** product_

Pops the top two values on the stack and replaces them with their product.

### 3.1.4 div/boqHa''egh

_a b **wav** quotient_

Pops the top two values on the stack and replaces them with a/b.

### 3.1.5 idiv/HabboqHa''egh (lit. full-divide)

_a b **HabboqHa''egh** quotient_

Pops the top two values on the stack and replaces them with the results of an
integer division operation.

### 3.1.6 mod/chuv (lit. leftover)

_a b **chuv** remainder_

Pops the top two values and returns the remainder of a mod b.

### 3.1.7 pow/boqHa'qa' (lit. remultiply)

_base exp **boqHa'qa'** real_

Pops the top two values and returns base^exp.

### 3.1.8 sqrt/loS'ar (lit. fourth-howmuch)

_angle **loS'ar** real_

Returns the square root of val.

### 3.1.9 add1/wa'boq

_a **wa'boq** a+1_

Increments the top value on the stack by one.

### 3.1.10 sub1/wa'boqHa'

_a **wa'boqHa'** a-1_

Decrements the top value on the stack by one.

### 3.2 Trigonometric and Logarithmic Operators  
_SIHpojjangwI'mey 'ej ghurjangwI'mey_

The standard Klingon unit of arc measure is the vatlhvI' (hundredth-part),
which is the same term used for percentage. However, Klingon mathematicians are
familiar with the concept of radians (botlhchuq, center-distance) and all known
_var'aq_ implementations work in radians for input and output.

### 3.2.1 sin/joq (lit. wave)

_angle **joq** real_

Returns the sine of val.

### 3.2.2 cos/joqHa' (lit. counter-wave)

_angle **joqHa'** cos(val)_

Returns the cosine of val.

### 3.2.3 tan/qojmI' (lit. cliffnumber)

_angle **qojmI'** tan(val)_

Returns the tangent of val.

### 3.2.4 atan/qojHa' (lit. anticliff)

_num den **qojHa'** angle_

Returns the arctangent of _num / den_.

### 3.2.5 ln/ghurtaH

_num **ghurtaH** real_

Returns the natural log of _num_.

### 3.2.6 log/maHghurtaH

_num **maHghurtaH** real_

Returns the base 10 log of _num_.

### 3.2.7 log3/wejghurtaH

_num **wejghurtaH** real_

Returns the base 3 log of _num_. (This function is actually considered a level
1 function, and is believed to exist only for historical purposes. Its use is
very rare except among programmers whose native language is Standard High
Klingon (which historically used a base 3 number system) and is unknown among
other users.)

### 3.3 Numerical Operators and Constants

This section describes operators that operate on numbers themselves, as well as
common system-level constants. (Note that some of these functions look like
verbs in English and adjectives in Klingon; the idea is that where we might say
_1.3 clip_ to get 1 a Klingon would be thinking _the clipped 1.3_.

### 3.3.1 clip/poD

_real **poD** int_

Removes the fractional portion of a real number (equivalent to floor(real).

### 3.3.2 smooth/Hab (lit. smooth)

_real **Hab** int_

Rounds a number to the nearest integer.

### 3.3.3 howmuch/'ar

_num **'ar** num2_

Returns the absolute value of _num_.

### 3.3.4 setrand/mIScher

_num **mIScher** -_

Sets the random number generator seed value to _num_. Not common, since most
_var'aq_ implementations have a rather arcane formula for picking a
pseudo-random seed value (security reasons, presumably).

### 3.3.5 rand/mIS

_num **mIS** real_

Returns a random real number in the range 0 to _num_. If there is no meaningful
input on the stack,

### 3.3.6 pi/HeHmI'

Pushes the value pi (~3.14159...) onto the stack. The Klingon name literally
means "edge-number".

### 3.3.7 e/ghurmI'

Pushes the value e onto the stack. The Klingon name literally means
"growth-number".

### 3.3.8 int?/HabmI''a'

_val **HabmI''a'** bool_ Pops the top value on the stack and returns 1 if it is
an integer, 0 if not.

### 3.3.9 number?/mI''a'

_val **mI''a'** bool_

Pops the top value off the stack and returns 1 if it's a number, 0 if it's
something else.

### 3.3.10 numberize/mI'moH

_str **mi'moH** val_

Pops a string off the stack, converts it into a numerical value, and returns
it.

### 3.4 Bitwise operators

Though _var'aq_ makes no clear distinction between integers and reals, it is
nevertheless useful to be able to manipulate a number on the bit level. The
following operators assume that their operands will always be treated as
integers; effects on floating-point values are undefined, and may be disallowed
at the implementor's discretion.

**Note:** The _var'aq_ bitwise operators are quite controversial as of this
writing (they are considered inappropriately low-level) and may be removed or
altered in future versions of this specification.

It is to be noted that the Klingon coinages for the operation (especially
_tlhoch_ (contradict) for xor) are unusually obscure even for Klingon
hackerspeak and probably reflect fairly profound differences in shades of
meaning.

### 3.4.1 isolate/mobmoH

_a b **mobmoH** result_

Performs a bitwise AND on a and b.

### 3.4.2 mix/DuD

_a b **DuD** result_

Performs a bitwise OR on a and b.

### 3.4.3 contradict/tlhoch

_a b **tlhoch** result_

Performs a bitwise XOR on a and b.

### 3.4.4 compl/Qo'moH

_val **Qo'moH** ~val_

Returns the one's-complement of val. **Note:** The literal meaning is something
like "make it say no".

### 3.4.5 shiftright/nIHghoS

_a b **nIHghoS** result_

Shifts a right b places, preserving the sign of the value.

### 3.4.6 shiftleft/poSghoS

_a b **poSghoS** result_

Shifts a left b places.

## 4 Relational and Logical Operators

### 4.1 Relational Operators and Predicate Functions  
_yu'jangwI'mey_

The standard convention for anything that returns a boolean argument is to end
the keyword in the interrogative suffix _\-'a'_, which in general is analogous
to Lisp's well-established -p (plain old Lisp) or -? (Scheme and Dylan)
predicate conventions; the English versions of the keywords follow the Scheme
convention for consistency with the Klingon. The _tlhIngan Hubbeq Say'ghun'ogh
paq_ (KDF Programmer's Style Guide) requires this convention; see that document
for further information.

### 4.1.1 gt?/law''a'

_a b **law''a'** bool_

Pops a and b off the stack, compares them, and returns a boolean value of true
if a is larger.

### 4.1.2 lt?/puS'a'

_a b **puS'a'** bool_

Pops a and b off the stack, compares them, and returns a boolean value of true
if a is smaller.

### 4.1.3 eq?/rap'a'

_a b **rap'a'** bool_

Pops a and b off the stack, compares them, and returns a boolean value of true
if a is the same as b.

### 4.1.4 ge?/law'rap'a'

_a b **law'rap'a'** bool_

Pops a and b off the stack, compares them, and returns a boolean value of true
if a is greater than or equal to b.

### 4.1.5 le?/puSrap'a'

_a b **puSrap'a'** bool_

Pops a and b off the stack, compares them, and returns a boolean value of true
if a is less than or equal to b.

### 4.1.6 ne?/rapbe'a'

_a b **rapbe'a'** bool_

Pops a and b off the stack, compares them, and returns a boolean value of true
if a is not equal to b.

### 4.1.7 null?/pagh'a'

_obj **pagh'a'** bool_

Examines the top object on the stack and returns a 1 if null, a 0 if not.

### 4.1.8 negative?/taH'a'

_val **taH'a'** bool_

Pops the top number on the stack and returns a 1 if less than 0, a 0 if not.

### 4.2 Logical Operators  
_vItjangwI'mey_

Note that these are strictly logical operators, not bitwise.

### 4.2.1 and/je

_a b **je** bool_

Evaluates b and a and returns a 1 if both are true, a 0 if not.

### 4.2.2 or/joq

_a b **joq** bool_

Evaluates b and a and returns a 1 if one or both are true, a 0 if both are
false.

### 4.2.3 xor/ghap

_a b **ghap** bool_

Evaluates b and a and returns a 1 if only one is true, a 0 otherwise.

## 5 Input/Output and File Operators

The _var'aq_ Level 0 specification essentially handles console I/O and files in
a manner very similar to the UNIX model.

### 5.1 Console I/O

The console I/O model at this point is very simple: write, read, error.

### 5.1.1 disp/cha'

_obj **cha'** -_

Pops the top object on the stack and writes it to STDOUT. Note that certain
types of objects will generate meaningless output, particularly anonymous proc
objects.

### 5.1.2 listen/'Ij

_\- **'Ij** str_

Reads one line of input and stores it as a string on top of the stack.

### 5.1.3 complain/bep

_str **bep** -_

Pops _str_ and prints it to stderr.

## 6 System Variables  
_patSarwI'mey_

This section describes _var'aq_ keywords that do no more than put set values on
the stack. Many of them are not precisely constants but more like environment
variables.

### 6.1 I/O-related Constants

### 6.1.1 newline/chu'DonwI'

Prints a carriage return.

### 6.1.2 tab/chu'tut

Advances by one tab stop.

### 6.2 Environment Constants

### 6.2.1 whereami/nuqDaq\_jIH

Represents the location of the current host device. On Earth implementations,
usually returns the IP address of the machine the interpreter is running on.

### 6.2.2 version/pongmI'

Returns the current interpreter version number. The reference interpreter
returns a date stamp.

### 6.2.3 argv/taghDe'

Pushes the command line arguments on the stack as a list.
