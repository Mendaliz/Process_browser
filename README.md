# Process_browser

## Description

Your task is to implement a command-line system utility that displays real-time information about running processes on the machine.
The application should show essential metrics such as CPU usage, memory consumption, and other process-specific details.
It should help users monitor system performance, detect resource-heavy tasks, and terminate processes if needed.

## CLI Application

The project must provide a command-line interface with the following options:

-l or --list — display a list of running processes with all available metrics

-k <PID> or --kill <PID> — terminate the process with the specified PID

-s <PID> or --show <PID> — show extended details for a specific process

-h or --help — display help message

The application should never crash. If any error occurs (e.g., invalid PID, insufficient permissions), it must:

Print a descriptive error message to stderr

Exit with a non-zero exit code

Free any allocated memory before exiting

You must validate all input arguments before performing any action.

The process list should update in real-time while the user is viewing it (if implementing live mode).
No extra text should be printed aside from the requested output.

Example:
```shell
$ process_browser -l
PID   CPU%   MEM%   NAME
1123  3.2    1.1    firefox
778   0.0    0.2    sshd
2041  25.4   10.8   blender

$ process_browser -k 2041
Process 2041 terminated

$ process_browser -s 1123
PID: 1123
Name: firefox
Threads: 34
Memory: 140MB
CPU Time: 03:58:12
```

If an invalid command is used:
```bash
$ process_browser -k abcd
Error: invalid PID
```
## Project Structure

The project must be organized into the following folders:

src — source files

include — header files

tests — automated tests
(If tests contain C code, they should also use src and include subfolders)

The source should be split logically (example structure):

main.c — entry point

process_list.c — retrieving and displaying process information

process_control.c — terminating or inspecting processes

utils.c — helper functions

This structure is only an example, but every file must be logically separated.

No binary, object, or IDE-generated files should be committed.

Test assets (if needed) should be located in tests/assets.

## Code Style and Programming Requirements

Global variables should be avoided. If used, they must be justified with comments.

All functions, structures, and any user-defined types must include Doxygen-style documentation.

Functions that may fail must follow C-style error handling:
return an error code and place real data into an output parameter.

## Testing

You must provide automated tests that verify:

Output correctness

Error handling

Memory leak absence

Behavior for all flag combinations

Incorrect input handling

All tests should run via:
```bash
make test
```

Unit testing is optional, but if implemented, add a description in Requirements.md including installation steps for the testing framework.

## Build

The program must be compiled with:

make


The Makefile must also provide:

install — install program system-wide
``` bash
sudo make install
process_browser -h
```

uninstall — remove installed program
```bash
sudo make uninstall
process_browser -h
command not found
```

clean — remove build artifacts (but not uninstall)

The Makefile must only recompile changed source files.

## Codestyle Guidance

The code must follow the formatting and naming rules defined in the project’s Style.md.
