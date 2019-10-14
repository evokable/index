# Evokable index

This repository contains a single index.json file that lists, for any given #include or import statement, 
which repository contains the Evoke-usable variant of the most likely file to be included. The intent
is to allow Evoke users to automatically look up unknown include statements and find the resource of
most likely interest for building that project.

# Rationale

Libraries should be written to be used as a library. This index catalogues all software that's written to
be imported as a single library and that can be used directly by Evoke as a library. Creating build 
files in any other format from these libraries is straightforward to do. As such, this index enables Evoke
but is also of use to any other build system user.

# Format

The index file contains two root nodes, "files" and "libraries". In use, you look up an unknown header in 
the "files" entry and find if it has a library mapped to it. If it does, you then look up that library in
the "libraries" entry. It will be mapped to an array of zero or more entries. If it's empty, the library is
the best match for this header, but no evokable repository is known.

If it's not empty, it contains a series of objects. These have at least the "type" entry set. Currently two
types are defined - "git" and "archive". The "git" has a "url" from which to clone, and either a "tag", 
"branch" or "hash" defining which version it should check out. The "archive" entry has a "url" that 
contains the package, which is to be unpacked into a folder with the name of the library.


