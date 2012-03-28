=======
 share
=======
Easily scp a randomly titled, self-destructing version of your file.

I decided it's unacceptable to be scp-ing all the one-off random files I want to
quickly share into the same publicly viewable web directory, so I wrote this
bash script.

This has basically not been tested at all at this point (it works on my
machines) so **use it at your own risk**. I feel like this kind of thing has real
clobber potential.


Examples
========

Uploading a file
::
  $ share map.jpg
  map.jpg                                          100%  132KB 132.3KB/s   00:00
  example.com/f/map.jpg      (link copied to clipboard)

Uploading a randomly titled file that self-destructs after 2 1/2 hours
::
  $ share -r -d 2h30m map.jpg
  map.jpg                                          100%  132KB 132.3KB/s   00:00
  example.com/f/44WOpU2OlK3qK7U9.jpg         (link copied to clipboard)
  Deletion scheduled. File will be deleted in 150 minutes.

Setup
=====
Fill in the USER, DOMAIN and DIR variables in the script.
For the examples above you would use these values::

  USER="yourusername"
  DOMAIN="example.com"
  DIR="f"

The script assumes the public web directories on your server are named after the
domain and located in your home directory. Change the uploadto() function if
this is not the case.

Scheduled deletion requires the `at` program to be installed and configured on
the server.


Usage
=====

::

  share [ -f | -r | -h ] [ -d TIME ] [ -l LEN ] FILENAME
    FILENAME : filename to upload via ssh
    -f : upload file named by hashing file contents
    -h : upload file named by hashing file name
    -r : upload file with random filename
    -d TIME : delete the file after TIME
    -l LEN : set length of random/hashed filename (default: 16)

    TIME is in the format 4d3h2m, in that order, any two parts can be omitted.
    With no suffix the unit of minutes is assumed.
