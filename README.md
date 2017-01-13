# PythonLircClient
This is a new and independent implementation of the Lirc `irsend(1)` program.
It offers a Python API and a command line interface. The command line
interface is almost, but not quite, compatible with irsend. Instead, it is
organized as a program with subcommands.

There are some other subtile differences from irsend:

* subcommands have been renamed, and must be lower case,
* send-once has been renamed to `send`; only takes one command
  (irsend takes several),
* send-stop (renamed to `stop`) without arguments uses the remote and
  the command from the last send-start command
   (API only; not from the command line),
* list has been replaced by the two subcommands `remotes` (listing remotes),
  and `commands`, listing the commands in a given remote,
* no need to give dummy empty arguments for some commands,
* The `--count` argument to send is argument to the subcommand.
* the code in commands (previously list remote) is suppressed,
  unless `-c` is given,
* port number must be given with the `--port` (`-p`) argument; hostip:portnumber
  is not recognized,
* verbose option `--verbose` (`-v`); echos all communication with the Lirc server,
* selectable timeout with `--timeout` (`-t`) option,
* better error messages

It does not depend on anything but standard Python libraries.

The name comes from the fact that the program requsts services from
a Lirc server (lircd). It has nothing to do with the library
lirc_client in Lirc.

Python3 only.
It does not depend on anything but standard Python libraries.

For a GUI version, look at IrScrutinizer.
For a Java version, look at [JavaLircClient](https://github.com/bengtmartensson/JavaLircClient)

## Usage:

    usage: lirc_client [-h] [-a host] [-d path] [-p port] [-t s] [-V] [-v]
		       sub-commands ...

    Program to send IR codes and commands to a Lirc server.

    positional arguments:
      sub-commands
	send                Send one command
	start               Start sending one command until stopped
	stop                Stop sending the command from send-start
	remotes             Inquire the list of remotes
	commands            Inquire the list of commands in a remote
	input-log           Set input logging
	driver-option       Set driver option
	simulate            Fake the reception of IR signals
	transmitters        Set transmitters
	version             Inquire version of the Lirc server. (Use "--version"
			    for the version of this program.)

    optional arguments:
      -h, --help            show this help message and exit
      -a host, --address host
			    IP name or address of lircd host. Takes preference
			    over --device.
      -d path, --device path
			    Path name of the lircd socket
      -p port, --port port  Port of lircd, default 8765
      -t s, --timeout s     Timeout in seconds
      -V, --version         Display version information for this program
      -v, --verbose         Have the communication with the Lirc server echoed
