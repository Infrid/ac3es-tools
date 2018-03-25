AC3ES Tools
===========

This is a collection of tools for manipulate games files for the game
Ace Combat 3.

It has a full working Ulz compressor/decompressor.


Requirements
------------

You need Python >= 3.4

Usage
-----

The tool has two sub commands, the *ulz* command for compress/decompress files
and *info* for get details about the ulz and the known iso or bpb of the game.

..

    usage: ac3es.py [-h] {ulz,info} ...
    
    positional arguments:
      {ulz,info}  Commands
        ulz       Manipulate ulz files
        info      Check files
    
    optional arguments:
      -h, --help  show this help message and exit
    

..

    usage: ac3es.py ulz [-h] [--compress FILE] [--ulz-type {0,2}]
                        [--level {1,2,4,8}] [--store-only] [--like-file LIKE_FILE]
                        [--decompress ULZ] [--output-file FILE] [--parents]
                        [--keep]
    
    optional arguments:
      -h, --help            show this help message and exit
      --compress FILE, -c FILE
                            Compress the file in ulz
      --decompress ULZ, -d ULZ
                            decompress the file in the current directory
      --output-file FILE, -f FILE
                            override output filename
      --parents, -p         Create directories for destination files if they don't
                            exists
      --keep, -k            prompt before every removal or destructive change
    
    compression:
      --ulz-type {0,2}      Define the ulz version to use
      --level {1,2,4,8}, -l {1,2,4,8}
                            Compression levels 1/2/4/8 uses a search buffer
                            1024/2048/4096/8192 bytes long.
      --store-only, -s      Store data on ulz file, needs anyway a compression
                            level
      --like-file LIKE_FILE
                            Get compression parameters from file
    

.. 

    usage: ac3es.py info [-h] FILES [FILES ...]
    
    positional arguments:
      FILES       One or more file to get info
    
    optional arguments:
      -h, --help  show this help message and exit
    
    

Examples
^^^^^^^^

Compress an image and put the output into the same directory

..

    ac3es.py ulz --compress image.tim --ulz-type=2 --level=1

or define another destination

..

    ac3es.py ulz --compress jap_0002.tim --ulz-type=2 --level=1 --output-file=mycompress.ulz

Get what parameters use from the original file

..

    ac3es.py info BPB/0386/0001/0000.ulz

More parameters are avaible, just type help for the sub command

..

    ac3es.py ulz --help
    ac3es.py info --help


Type 0 vs type 2
----------------

They are basically the same, ulz 0 is meant to be decompressed faster
than ulz 2. In reality doesn't matter, the difference are few lines of
ASM inside the ACE.BIN executable.

Ulz type 0 produces files at least 4 bytes bigger than ulz 2, because
the compressed data is store a bit different regardless the
compression ratio. Read the source code for more details.

They are both based on LZ77 and I compress using the same algorithm. I
don't know why they used two nearly identical formats.


Changelog
---------

2.1 - Split and merge bin containers 
2.0 - Ulz type 0 compression is finally working

Contacts
--------

Gianluigi "Infrid" Cusimano <infrid@infrid.com>
http://ac3es.infrid.com/
