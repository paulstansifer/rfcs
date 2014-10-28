- Start Date: (fill me in with today's date, YYYY-MM-DD)
- RFC PR: (leave this empty)
- Rust Issue: (leave this empty)

# Summary

The Rust build process will optionally serve a webpage on `localhost` which will provide all the information the build process normally emits on stdout in a friendlier format. JS on the page will collapse command-lines, extra type information, and other occasionally-useful context. Types from std will be displayed unqualified, but as a link to the relevant documentation. Expected/got lines will be aligned with each other.

# Motivation

`rustc`, like almost all compilers, spits out a great deal of information to the programmer, on the grounds that it might be relevant to the debugging process. Similarly, the build system as a whole emits the complete command lines of programs it executes, even though it's rarely used. All this information is printed on stdout, in plain text, on potentially very long lines. We can present this information in a better format, without resorting to an IDE.

As I see it, there are three kinds of benefits to presenting this information in HTML:

* More information.
* Less information on screen by default.
* Better organization.

This new feature should make it easier to:

* Zero in on relevant information in compile errors.
* Access documentation relevant to the error.


Why are we doing this? What use cases does it support? What is the expected outcome?

# Detailed design

This is the bulk of the RFC. Explain the design in enough detail for somebody familiar
with the language to understand, and for somebody familiar with the compiler to implement.
This should get into specifics and corner-cases, and include examples of how the feature is used.

The Rust compiler would ship with an HTML file containing a basic AJAX tool that will poll temporary files in the default build directory (TODO: is this possible? Do we want sockets? Named pipes (but do they work on Windows?))


## Message generation

For the sake of consistency, all places in `rustc` where two different code paths will be taken depending on whether the message being generated is directed towards HTML or `stdout` should be isolated from the actual generation of messages. 

Although formatting may change between these code paths (for example, the HTML output might print text known not to be code in a variable-width typeface, or it may use `<u></u>` instead of `^----^` to highlight spans), all verbiage should be identical, and all code (like either Rust code quoted from input or Rust types relevant to typechecking) should differ only in that the HTML may omit information if that information can still somehow be accessed by the user (e.g. by hovering over an `<abbr>` tag or clicking on a `+` widget to expand).

The rule should be that two users, one of whom is looking at error messages on `stdout` and one of whom is reading their HTML form ought to be able to communicate easily by copying and pasting what they see into their email messages.

# Drawbacks

Why should we *not* do this?

## Security

We would at least need to think about the security risks that might befall a user for whom port XXX is available to the outside world (perhaps an approach guaranteed to only affect the local machine, requiring the user to look up a `file:///` URL might be preferable for this reason).

## Maintenence

There is a risk that, over time, places where two different code paths 


# Alternatives

What other designs have been considered? What is the impact of not doing this?

# Unresolved questions

What parts of the design are still TBD?
