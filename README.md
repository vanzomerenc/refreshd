# Refreshd

Refreshd is a directory-watching program that will run a command when the watched directory, or
anything inside that directory (or its sub-directories) changes. It implements an unsophisticated,
but sensible, rate-limiting scheme to avoid running the given command too often.

The first argument is the directory to watch. The second argument is the command to run when the
watched directory changes, and any remaining arguments are arguments to that command.

The following flags are supported:
* `--verbose` for (probably not useful) debug-level output.
* `--quiet` to silence all output except the output from the provided command.
* `--mindelay <SECONDS>` to make Refreshd wait the given number of seconds before running the
    provided command. This is often useful when expecting a burst of multiple file changes.
* `--mininterval <SECONDS>` to make Refreshd wait at least the given number of seconds between runs.

Both `--mindelay` and `--mininterval` may be specified together. The default is
`--mindelay 1 --mininterval 5`.

Example usage:
```
refreshd --quiet --mindelay 1 --mininterval 1 -- ~/Projects/foo/src make foo
```

This program relies on Linux’s “inotify” interface, so is Linux-only.
It also probably relies on a lot of GNU-specific behavior (such as the behavior of GNU Getopt),
another reason it‘s Linux-only.

## Dependencies

* Bash (tested with Bash 5.3.3)
* inotify-tools (tested with inotify-tools 4.25.9.0)
* procps (tested with procps 4.0.4)

## Support and Bug Reports

This program was created to meet its author’s needs. Some effort has gone into ensuring it works
correctly, but very little effort has gone into its interface or documentation. The author is
open to receiving bug reports and requests to create documentation, but will not consider adding
new features unless there is a compelling reason to do so.

Currently the best way to contact the author is through Github. username: vanzomerenc
