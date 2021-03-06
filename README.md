# Audible Converter (AAX to M4A)
Converts Audible AAX audiobooks to M4A while keeping chapters and the cover image intact.
The cover can be added as a looped image so it will be shown while playing on [Plex Media Server](https://www.plex.tv/)

# Usage
```
λ audible-converter -h

  Usage: audible-converter [options] <file>


  Commands:

    list   list registered devices and their activation bytes (windows only)

  Options:

    -h, --help                      output usage information
    -V, --version                   output the version number
    -o, --output <filename>         output filename
    -p, --path <path>               output path
    -v, --verbose                   output detailed information
    -a, --activation-bytes <value>  4 byte activation secret to decrypt Audible AAX files (e.g. 1CEB00DA)
    -d, --device <number>           registered device number from which activation bytes are used (windows only)
    -l, --loop                      add looped cover image to Audiobook
```

## Example:

```
λ audible-converter *.aax -a 1CEB00DA

Haruki Murakami - 1Q84 (Buch 1 & 2) [2012] (Duration: 30h53m0s)
Converting Audiobook (using 1CEB00DA for decryption) ... 100%
Extracting Cover Image ... 100%

Guillermo del Toro, Chuck Hogan - Das Blut [2010] (Duration: 12h4m17s)
Converting Audiobook (using 1CEB00DA for decryption) ... 100%
Extracting Cover Image ... 100%

Stephen King - Der Anschlag [2012] (Duration: 31h50m22s)
Converting Audiobook (using 1CEB00DA for decryption) ... 100%
Extracting Cover Image ... 100%

Max Brooks - Der Zombie Survival Guide. Überleben unter Untoten [2011] (Duration: 9h5m32s)
Converting Audiobook (using 1CEB00DA for decryption) ... 100%
Extracting Cover Image ... 100%

Finished converting 4 Audiobooks!
```

# Requirements
* [x] Installed Audible Download Manager (for getting your activation bytes)
  * On OSX or Linux you could use this method http://apple.stackexchange.com/a/243670
* [x] [ffmpeg](https://ffmpeg.org/) for converting

# How it works
* Extract cover image:
  * `ffmpeg -y -i audiobook.aax cover.png`
* Decrypted and convert to m4a:
  * `ffmpeg -y -activation_bytes 1CEB00DA -i audiobook.aax -c:a copy -vn audiobook.m4a`
* Add looped cover image:
  * `ffmpeg -y -r 1 -loop 1 -i cover.png -i audioboob.m4a -c:a copy -shortest audiobook.m4v`

# License
[The MIT License (MIT)](http://r15ch13.mit-license.org/)
