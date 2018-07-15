Getopt for GNU
==============

NOTE: getopt is now part of the C library, so if you don’t know what
“Keep this file name-space clean” means, talk to drepper@gnu.org before
changing it! Copyright (C)
1987,88,89,90,91,92,93,94,95,96,98,99,2000,2001 Free Software
Foundation, Inc. This file is part of the GNU C Library.

The GNU C Library is free software; you can redistribute it and/or
modify it under the terms of the GNU Lesser General Public License as
published by the Free Software Foundation; either version 2.1 of the
License, or (at your option) any later version.

The GNU C Library is distributed in the hope that it will be useful, but
WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU Lesser
General Public License for more details.

You should have received a copy of the GNU Lesser General Public License
along with the GNU C Library; if not, write to the Free Software
Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA 02111-1307 USA.

This tells Alpha OSF/1 not to define a getopt prototype in
&lt;stdio.h&gt;. Ditto for AIX 3.2 and &lt;stdlib.h&gt;.

This version of
`getopt' appears to the caller like standard Unix`getopt’ but it behaves
differently for the user, since it allows the user to intersperse the
options with the other arguments.

As \`getopt’ works, it permutes the elements of ARGV so that, when it is
done, all the options precede everything else. Thus all application
programs are extended to handle flexible argument order.

Setting the environment variable POSIXLY\_CORRECT disables permutation.
Then the behavior is completely standard.

GNU application programs can use a third alternative mode in which they
can distinguish the relative order of options and other arguments.

For communication from `getopt' to the caller. When`getopt’ finds an
option that takes an argument, the argument value is returned here.
Also, when \`ordering’ is RETURN\_IN\_ORDER, each non-option
ARGV-element is returned here.

Index in ARGV of the next element to be scanned. This is used for
communication to and from the caller and for communication between
successive calls to \`getopt’.

On entry to \`getopt’, zero means this is the first call; initialize.

When \`getopt’ returns -1, this is the index of the first of the
non-option elements that the caller should itself scan.

Otherwise, \`optind’ communicates from one call to the next how much of
ARGV has been scanned so far.

Formerly, initialization of getopt depended on optind==0, which causes
problems with re-calling getopt as programs generally don’t know that.

The next char to be scanned in the option-element in which the last
option character we returned was found. This allows us to pick up the
scan where we left off.

If this is zero, or a null string, it means resume the scan by advancing
to the next ARGV-element.

Callers store zero here to inhibit the error message for unrecognized
options.

Set to an option character which was unrecognized. This must be
initialized on some systems to avoid linking in the system’s own getopt
implementation.

Describe how to deal with options that follow non-option ARGV-elements.

If the caller did not specify anything, the default is REQUIRE\_ORDER if
the environment variable POSIXLY\_CORRECT is defined, PERMUTE otherwise.

REQUIRE\_ORDER means don’t recognize them as options; stop option
processing when the first non-option is seen. This is what Unix does.
This mode of operation is selected by either setting the environment
variable POSIXLY\_CORRECT, or using \`+’ as the first character of the
list of option characters.

PERMUTE is the default. We permute the contents of ARGV as we scan, so
that eventually all the non-options are at the end. This allows options
to be given in any order, even with programs that were not written to
expect this.

RETURN\_IN\_ORDER is an option available to programs that were written
to expect options and other ARGV-elements in any order and that care
about the ordering of the two. We describe each non-option ARGV-element
as if it were the argument of an option with character code 1. Using
\`-’ as the first character of the list of option characters selects
this mode of operation.

The special argument
`--' forces an end of option-scanning regardless of the value of`ordering’.
In the case of RETURN\_IN\_ORDER, only `--' can cause`getopt’ to return
-1 with \`optind’ != ARGC.

We want to avoid inclusion of string.h with non-GNU libraries because
there are many ways it can cause trouble. On some systems, it contains
special magic macros that don’t work in GCC.

getopt.h
========

Declarations for getopt.
========================

Copyright (C) 1989-1994, 1996-1999, 2001 Free Software Foundation,
Inc. This file is part of the GNU C Library.

The GNU C Library is free software; you can redistribute it and/or
modify it under the terms of the GNU Lesser General Public License as
published by the Free Software Foundation; either version 2.1 of the
License, or (at your option) any later version.

The GNU C Library is distributed in the hope that it will be useful, but
WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU Lesser
General Public License for more details.

You should have received a copy of the GNU Lesser General Public License
along with the GNU C Library; if not, write to the Free Software
Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA 02111-1307 USA.

If **GNU\_LIBRARY** is not already defined, either we are being used
standalone, or this is the first header included in the source file. If
we are being used with glibc, we need to include &lt;features.h&gt;, but
that does not exist if we are standalone. So: if **GNU\_LIBRARY** is not
defined, include &lt;ctype.h&gt;, which will pull in &lt;features.h&gt;
for us if it’s from glibc. (Why ctype.h? It’s guaranteed to exist and it
doesn’t flood the namespace with stuff the way some other headers do.)

For communication from `getopt' to the caller. When`getopt’ finds an
option that takes an argument, the argument value is returned here.
Also, when \`ordering’ is RETURN\_IN\_ORDER, each non-option
ARGV-element is returned here.

Index in ARGV of the next element to be scanned. This is used for
communication to and from the caller and for communication between
successive calls to \`getopt’.

On entry to \`getopt’, zero means this is the first call; initialize.

When \`getopt’ returns -1, this is the index of the first of the
non-option elements that the caller should itself scan.

Otherwise, \`optind’ communicates from one call to the next how much of
ARGV has been scanned so far.

Callers store zero here to inhibit the error message \`getopt’ prints
for unrecognized options.

Describe the long-named options requested by the application. The
LONG\_OPTIONS argument to getopt\_long or getopt\_long\_only is a vector
of \`struct option’ terminated by an element containing a name which is
zero.

The field \`has\_arg’ is: no\_argument (or 0) if the option does not
take an argument, required\_argument (or 1) if the option requires an
argument, optional\_argument (or 2) if the option takes an optional
argument.

If the field
`flag' is not NULL, it points to a variable that is set to the value given in the field`val’
when the option is found, but left unchanged if the option is not found.

To have a long-named option do something other than set an
`int' to a compiled-in constant, such as set a value from`optarg’, set
the option’s `flag' field to zero and its`val’ field to a nonzero value
(the equivalent single-letter option character, if there is one). For
long options that have a zero `flag' field,`getopt’ returns the contents
of the \`val’ field.

Get definitions and prototypes for functions to process the arguments in
ARGV (ARGC of them, minus the program name) for options given in OPTS.

Return the option character from OPTS just read. Return -1 when there
are no more options. For unrecognized options, or options missing
arguments, \`optopt’ is set to the option letter, and ‘?’ is returned.

The OPTS string is a list of characters which are recognized option
letters, optionally followed by colons, specifying that that letter
takes an argument, to be placed in \`optarg’.

If a letter in OPTS is followed by two colons, its argument is optional.
This behavior is specific to the GNU \`getopt’.

The argument
`--' causes premature termination of argument scanning, explicitly telling`getopt’
that there are no more options.

If OPTS begins with
`--', then non-option arguments are treated as arguments to the option '\0'.  This behavior is specific to the GNU`getopt’.
