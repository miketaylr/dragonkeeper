# Dragonkeeper - Opera Dragonfly development proxy

## Introduction

Dragonkeeper is a utility designed to ease development of Opera Dragonfly.

Dragonkeeper serves as a proxy between the Dragonfly client and a host (an Opera instance). This makes
it possible to run Dragonfly as a normal web page which makes development easier, e.g. by making it easy
to reload whenever changes are made, and also by allowing Dragonfly to be inspected by another Dragonfly
instance.

## Install

For installing, you need 'setuptools'.

    % python setup.py install

On Windows, you might want to add the install path to your PATH environment variable.

Note: Dragonkeeper doesn't have to be installed, but this is preferred.

## Usage

If installed:

    % dragonkeeper

if not installed:

    % python /path/to/dragonkeeper

Exit: Control-C

## Howto

Basic workflow when using Dragonkeeper is as follows:

- Get a source distribution of Opera Dragonfly from <https://github.com/operasoftware/dragonfly>

- Open a terminal, go to Dragonfly's directory and run dragonkeeper:

        % dragonkeeper

  This should result in:

        server on: http://localhost:8002/

- Open that URL in Opera. You should see a list of files. Navigate to `src/client-en.xml`. There
  should be a message saying "Waiting for host connection on port 0".

- Open another instance of Opera from within your terminal using

        /path/to/opera -pd <profile-dir>

  <profile-dir> can simply be a temporary directory, e.g. /tmp.

  Alternatively, use another installation of Opera (as long as they have different profile directories).

- In that browser's address bar, type opera:debug and then click 'Connect'.

- In the first instance, Opera Dragonfly should now load. If not, reload it manually.

The Dragonfly instance running in the normal browser window can now be debugged with "normal" Opera
Dragonfly instance.

## Advanced

Settings: an optional file `CONFIG` overrides the defaults.
The options file is a standard .ini file, with a single section called
"dragonkeeper":

    [dragonkeeper]
    host:
    root: .
    server_port: 8002
    proxy_port: 7001
    debug: False
    format: False

### Options
```
  -h, --help            show this help message and exit
  -c CONFIG_PATH, --config=CONFIG_PATH
                        Path to config file
  -d, --debug           print message flow
  -f, --format          pretty print message flow
  -j, --format-payload  pretty print the message payload. can be very
                        expensive
  -r ROOT, --root=ROOT  the root directory of the server; default .
  -p PROXY_PORT, --proxy-port=PROXY_PORT
                        proxy port; default 7001
  -s SERVER_PORT, --server-port=SERVER_PORT
                        server port; default 8002
  --host=HOST           host; default localhost
  -i, --make-ini        Print a default dragonkeeper.ini and exit
  --force-stp-0         force stp 0 protocol
  --print-command-map   print the command map
  --message-filter=MESSAGE_FILTER
                        Filter the printing of the messages. The argument is
                        the filter or a path to a file with the filter. If the
                        filter is set, only messages which are listed in the
                        filter will be printed. The filter uses JSON notation
                        like: {"<service name>": {"<message type>":
                        [<message>*]}}", with message type one of "command",
                        "response", "event."  '*' placeholder are accepted in
                        <message>, e.g. a filter to log all threads may look
                        like:  "{'ecmascript-debugger': {'event':
                        ['OnThread*']}}".
  -v, --verbose         print verbose debug info
  --cgi                 enable cgi support
```


More comments in the source files.

## Changelog

See the `CHANGELOG` file

## Contact

Dragonkeeper is maintained by the Opera Dragonfly team. The authors are

- Christian Krebs <chrisk@opera.com>
- Rune Halvorsen
- Jan Borsodi <jborsodi@opera.com>

The Opera Dragonfly web site is at http://dragonfly.opera.com


## License

See the `LICENSE` file in the top distribution directory.

