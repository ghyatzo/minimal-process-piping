### Minimal process piping

Small single header library to provide basic support for process communication.
If you want to use an executable in your program, this library sets up the pipework
to send input to your external process and read its output, from within your program.

!!! currently only supports Linux and MacOS, window specific logic will come.

### Usage
define your command string to invoke the process:
```
// The command string must be NULL terminated.
const char * args[] = { "/absolute/path/to/executable", "argument 1", "argument 2", NULL }
```
if you have your process in the `PATH` you can pass the path as an argument when starting the parent process
    with `$(which process_name)` maybe.

save the command in your program
```
// The convention is that the first argument to a program is it's path/name
auto proc { System::Process(args[0]) };
```
then you can start interacting with it:
```
// Invoke the process with the give arguments.
proc.start(args);

// Mirror the process standard output
proc.mirror_output();

// Stop the mirroring
proc.stop_mirror();

// Send a string to the process if it's waiting for input
proc.send_command(std::string)

// read the process output if any, wait at most timeout_ms for more output
std::vector<std::string> output { proc.read(timeout_ms) };
```
