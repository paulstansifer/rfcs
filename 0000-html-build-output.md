- Start Date: (fill me in with today's date, YYYY-MM-DD)
- RFC PR: (leave this empty)
- Rust Issue: (leave this empty)

# Summary

The Rust build process will optionally serve a webpage on localhost which will provide all the information the build process normally emits on stdout in a friendlier format. JS on the page will collapse command-lines, extra type information, and other occasionally-useful context. Types from std will be displayed unqualified, but as a link to the relevant documentation. Expected/got lines will be aligned with each other.

# Motivation

`rustc`, like almost all compilers, spits out a great deal of information to the programmer, on the grounds that it might be relevant to the debugging process. Similarly, the build system as a whole emits the complete command lines of programs it executes, even though it's rarely used. All this information is printed on stdout, in plain text, on potentially very long lines. We can present this information in a better format, without resorting to an IDE.

As I see it, there are three kinds of benefits to presenting this information in HTML:

* More information.
* Less information on screen by default.
* Better organization.


Why are we doing this? What use cases does it support? What is the expected outcome?

# Detailed design

This is the bulk of the RFC. Explain the design in enough detail for somebody familiar
with the language to understand, and for somebody familiar with the compiler to implement.
This should get into specifics and corner-cases, and include examples of how the feature is used.

# Drawbacks

Why should we *not* do this?

# Alternatives

What other designs have been considered? What is the impact of not doing this?

# Unresolved questions

What parts of the design are still TBD?
