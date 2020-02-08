# pipe2gdoc
Send the output of console commands to a Google Doc

## Quickstart
### MacOS / Linux
1. Install any pip packages you might need
```pip3 install -r requirements.txt```
2. cp pipe2gdoc somewhere in your $PATH
3. Enable the Google Docs API.  The easiest way to do this is to visit https://developers.google.com/docs/api/quickstart/python and click the "Enable the Google Docs API" button.
4. Download the client configuration.  This should be a file named credentials.json
5. Authenticate:
```pipe2gdoc --authenticate --credentials /path/to/credentials.json```
Note:  If you are doing this headless (on a remote Linux server,) do the following steps:
```
  A. Copy the URL it prints out, and paste it into your own web browser.
  B. Auth normally.
  C. When it redirects you to localhost and it fails, copy that URL
  D. SSH into another session on your remote Linux server, and run
      curl 'url you copied'
  E. Authentication should then complete normally.
```

6. (Optionally) Create ~/.pipe2gdocrc with one line in it:
```
documentId: whateveryourdeafultdocumentidis
```
NOTE:  If you use the word new as your documentId a new document will be created each time you run the script, named pipe2gdoc_datestamp

7. Pipe something to it
```
echo "hello world" | pipe2gdoc
```
7b. Without using a config file
```
echo "hello world" | pipe2gdoc --documentId whateveryourdeafultdocumentidis
```
NOTE:  If you use the word new as your documentId a new document will be created each time you run the script, named pipe2gdoc_datestamp

### Windows
I dunno.  It probably works?  :3

## Requirements
1. You must be able to enable the Google Docs API for your account.  This is almost always possible, unless you have an Enterprise account with restrictions set.
2. Python 3

## Usage
If you don't have documentId specified in your config file, then you *must* specify --documentId, unless you are authenticating

Specify documentId as new to create a new document, named pipe2gdoc_datestamp.

```
$ ./pipe2gdoc -h
usage: pipe2gdoc [-h] [-q] [--documentId DOCUMENTID] [--maxBuffer MAXBUFFER]
                 [--maxTime MAXTIME] [--config CONFIG]
                 [--pickleToken PICKLETOKEN] [--authenticate]
                 [--credentials CREDENTIALS]

Send the output of console commands to a Google Doc

optional arguments:
  -h, --help            show this help message and exit
  -q                    Suppress all standard output.
  --documentId DOCUMENTID
                        The Google Document ID.  Use 'new' if you want to create a new document.
                          The new document would be named similar to pipe2gdoc_2020-02-08 02:12:31.278968
                          Example:  --documentId 1W8vd1Ad0LJt5FIWQOzaIUhOby4dwhL9TPkihFhb0dOU
                          Example:  --documentId new
  --maxBuffer MAXBUFFER
                        The maximum number of lines to buffer locally before commiting the current buffer to the GDoc.  The default is 1000.
                          Example:  --maxBuffer 500
  --maxTime MAXTIME     The maximum time in seconds to wait for new input (while below the buffer max) before commiting the current buffer to the GDoc.  The default is 30.
                          Example:  --maxTime 10
  --config CONFIG       The location of your YAML configuration file.  Defaults to ~/.pipe2gdocrc
                          Example:  --config /opt/oddworld/mypipe2gdocrc
  --pickleToken PICKLETOKEN
                        The path to your token.pickle file.  It defaults to ./token.pickle
                          Example:  --pickleToken /opt/oddworld/token.pickle
  --authenticate        Authenticate with OAuth, using the credentials provided in either ./credentials.json, or the file you provide with --credentials.
                          Example:  --authenticate --credentials /opt/oddworld/credentials.json --tokenPickle /opt/oddworld/token.pickle
  --credentials CREDENTIALS
                        If --pickleToken is specified, then the token will be written to the path provided.  Otherwise, it will bre written to ./token.pickle
                        If your pickle token is already created, you do not need this option.
                          Example:  --authenticate --credentials /opt/oddworld/credentials.json --tokenPickle /opt/oddworld/token.pickle
```

## Config File Example
The config file is YAML formatted, and can contain any of the command line arguments (other than config and automate.)

The primary purpose of the config file is to prevent the need to specify --documentId every time.  But it can be used to configure any argument.

A fully redundant (using default values other than documentId) example can be found below:
```
documentId: 1W8vd1Ad0LJt5FIWQOzaIUhOby4dwhL9TPkihFhb0dOU
maxBuffer: 1000
maxTime: 30
pickleToken: /opt/oddworld/token.pickle
credentials: /opt/oddworld/credentials.json
```

A basic config file if you want to create a new document every time:
```
documentId: new
```

## Release History

* 0.1.0
    * Added create new document feature
* 0.0.1
    * Work in Progress

## Meta

DranoTheCat – No Twitter.  No Facebook.  

Licensed under the GNU General Public License v3.0. See ``LICENSE`` for more information.

https://github.com/danhartfiction/pipe2gdoc
