# GdNativeTemplate
GdNative Example

*First off, **disclaimer** -- this is a work in progress!  There's no guarantee it 
will work for you.  Look at it more like an example/starting point.*

This is an empty godot project that loads my [gdextension utilities](https://github.com/VijABJ/SrgGdUtilities/tree/main).
There should be more details on that page for building the extension itself.  

After cloning this project, make sure to do `git submodule update --init --recursive`, then follow
the instructions on building the extension in the link above.  The project itself is actually 
empty, except for a single resource instance of RuntimeEnvironment.  You can edit this, and use it
in code, and probably crash it. I might expand this template at some point to actually use
the resource types.  For now, it's simply a shell and proof of concept that the extension
actually loads.

