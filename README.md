# pipe2gdoc
> Send the output of console commands to a Google Doc

## Quickstart
1. cp pipe2gdoc somewhere in your $PATH
2. Enable the Google Docs API.  The easiest way to do this is to visit https://developers.google.com/docs/api/quickstart/python and click the "Enable the Google Docs API" button.
3. Download the client configuration.  This should be a file named credentials.json
4. Authenticate:
```pipe2gdoc --authenticate --credentials /path/to/credentials.json```
5. (Optionally) Create ~/.pipe2gdocrc with one line in it:
```documentId: whateveryourdeafultdocumentidis
```
6. Pipe something to it
```echo "hello world" | pipe2gdoc
```
6b. Without using a config file
```echo "hello world" | pipe2gdoc --documentId whateveryourdeafultdocumentidis
```

## Usage
If you don't have documentId specified in your config file, then you *must* specify --documentId, unless you are authenticating

```$ ./pipe2gdoc --help
usage: pipe2gdoc [-h] [-q] [--documentId DOCUMENTID] [--maxBuffer MAXBUFFER]
                 [--maxTime MAXTIME] [--config CONFIG]
                 [--pickleToken PICKLETOKEN] [--authenticate]
                 [--credentials CREDENTIALS]

optional arguments:
  -h, --help            show this help message and exit
  -q                    Suppress all standard output.
  --documentId DOCUMENTID
                        The Google Document ID. Example: --documentId
                        1W8vd1Ad0LJt5FIWQOzaIUhOby4dwhL9TPkihFhb0dOU
  --maxBuffer MAXBUFFER
                        The maximum number of lines to buffer locally before
                        commiting the current buffer to the GDoc. The default
                        is 1000. Example: --maxBuffer 500
  --maxTime MAXTIME     The maximum time in seconds to wait for new input
                        (while below the buffer max) before commiting the
                        current buffer to the GDoc. The default is 30.
                        Example: --maxTime 10
  --config CONFIG       The location of your YAML configuration file. Defaults
                        to ~/.pipe2gdocrc Example: --config
                        /opt/oddworld/mypipe2gdocrc
  --pickleToken PICKLETOKEN
                        The path to your token.pickle file. It defaults to
                        ./token.pickle Example: --pickleToken
                        /opt/oddworld/token.pickle
  --authenticate        Authenticate with OAuth, using the credentials
                        provided in either ./credentials.json, or the file you
                        provide with --credentials. Example: --authenticate
                        --credentials /opt/oddworld/credentials.json
                        --tokenPickle /opt/oddworld/token.pickle
  --credentials CREDENTIALS
                        If --pickleToken is specified, then the token will be
                        written to the path provided. Otherwise, it will bre
                        written to ./token.pickleIf your pickle token is
                        already created, you do not need this option. Example:
                        --authenticate --credentials
                        /opt/oddworld/credentials.json --tokenPickle
                        /opt/oddworld/token.pickle
```

## Config File Example
The config file is YAML formatted, and can contain any of the command line arguments (other than config and automate.)

The primary purpose of the config file is to prevent the need to specify --documentId every time.  But it can be used to configure any argument.

A fully redundant (using default values other than documentId) example can be found below:
```documentId: 1W8vd1Ad0LJt5FIWQOzaIUhOby4dwhL9TPkihFhb0dOU
maxBuffer: 1000
maxTime: 30
pickleToken: /opt/oddworld/token.pickle
credentials: /opt/oddworld/credentials.json
```

## Release History

* 0.0.1
    * Work in Progress

## Meta

DranoTheCat – No Twitter.  No Facebook.  

Licensed under the GNU General Public License v3.0. See ``LICENSE`` for more information.

https://github.com/danhartfiction/pipe2gdoc
