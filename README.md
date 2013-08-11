mp3tagiconv_reloaded
====================

This is a forked mp3tagiconv aiming to improve and get more interesting functionals.  
Original mp3tagiconv is written by CHEN, Xing (cxcxcxcx@gmail.com), hosted on [Google code](https://code.google.com/p/mp3tagiconv)  
This utility tries to fix the incorrect encoding in mp3 tag system and make the media player show the right metadata.  

For now, this program depends on [Mutagen](https://code.google.com/p/mutagen/) -- a Python module to handle audio metadata. (will improve soon.)

## Usage

For mp3 files with Chinese tags(we first try gbk, then utf8), ID3v2 tags which are already encoded in unicode will not be affected:

``` bash
mp3tagiconv a.mp3
```

You can use `-e` to specify the encoding used if the tag is stored by latin-1. The program will guess your encoding according to your list:

```bash
mp3tagiconv -e gbk,utf8 b.mp3
```

If you don't want to confirm for every file(*not recommended*):

```bash
mp3tagiconv --do-update *.mp3
```

## Details

Actually, the program does the following things:

1. Read tags of a MP3 file from its ID3v2 and ID3v1. ID3v1 is used to supplement the result of ID3v2.
2. Guess the encoding of the tags.
3. Decode the tags, then:
    1. Write directly to ID3v2 tag of MP3 file via mutagen.
    1. Encode the tags with local encoding(eg. gbk in Chinese) and write it to ID3v1 tag of the file.
4. The modified tag now can be recognized by most of the applications, eg. rthymbox, totem, juk, Windows Media Player, etc.
