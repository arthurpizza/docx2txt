# docx2txt
Perl script to convert .docx files to plain text.

Originally from [http://docx2txt.sourceforge.net/](http://docx2txt.sourceforge.net/) but copied to github.

FROM THE ORIGINAL SITE:
-----------------------

**docx2txt** is a perl based command line utility to convert Microsoft Office(Tm) Docx documents to equivalent Text documents. Latest version supports following features during text extraction.

* Character conversions (" ' < & > - ... fraction and some mathematical symbols etc.); currency characters are converted to respective names like Euro.
* Capitalisation of text blocks.
* Center and right justification of text fitting in a line of (configurable) 80 columns.
* Horizontal ruler, line breaks, paragraphs separation, tabs
* Indicating hyperlinked text along with the hyperlink. (configurable)
* Handling (bullet, decimal, letter, roman) lists along with (attempt at) indentation.

Other non-text-extraction features are mentioned below.

* Installation via Makefile/BSDmakefile and Windows batch file.
* Provision for installation of script files and configuration file in separate directories when installing via make files.
*  Wrapper shell and batch scripts for easy usage.
* Perl script supports input/output from/to stdin/stdout, as well as input/output redirection from files.
* Provision for separate system wide and user configuration files.
* Works with unzipping utilities like Unzip (Windows port), 7z (7-Zip), pkzipc (PKZip), wzunzip (WinZip), and CakeCmd.
* Basically it requires a commandline unzipping program that can silently extract single file from zip archive to console/standard output/pipe.
* Also works with directory holding the unzipped content of a .docx file.
* This feature is useful for users if they do not have a commandline unzipper meeting above requirement.

It is released under GPLv3. For further details and plans, please refer to the documentation in the released package.

## Dealing with Corrupted Docx files

Since CakeCmd can extract files from a corrupted zip archive in many cases that popular unzippers do not extract (eg. in case of some CRC failure), so using CakeCmd unzipper directly/indirectly you can extract text content from a damaged docx file via this script, as long as the relevant xml files holding the text information are extracted with non-zero content from corresponding docx file. Because CakeCmd is ignoring some data sanity checks on the archive, at times these extracted files have quite some amount of junk in them.

You can also try to repair corrupted docx file using programs like Zip (Windows port), pkzipc (PKZip), ALZipCon, and winrar. GUI version of winrar gives an option to keep broken extracted files as well.

## Download

* CVS @ Souceforge.net
* v1.4 (May 15, 2014) | v1.3 (April 07, 2014) | v1.2 (January 15, 2012) | v1.1 (December 11, 2011) | v1.0 (October 04, 2009)
* v0.4 (Septemer 06, 2009) | v0.3 (Septemer 23, 2008) | v0.2 (August 15, 2008) | v0.1 (August 10, 2008)

## Viewing Docx files

Using MC (Midnight Commander)

MC (Midnight Commander) fans can add following binding in ~/.mc/bindings and view the text content of .docx file by hitting F3 function key after selecting the concerned docx document.

```
# Microsoft .docx Document
regex/\.(docx|DOCX|Docx)$
 View=%view{ascii} docx2txt.pl %f -
```

## Using VIm Editor

You can add following lines in your ~/.vimrc to view the text content of a .docx file directly when using vim.

```
"use docx2txt.pl to allow VIm to view the text content of a .docx file directly.
autocmd BufReadPre *.docx set ro
autocmd BufReadPost *.docx %!docx2txt.pl 
```

Note that above .vimrc addition will allow you to view the text content of .docx files specified as command line argument to vim, but not of those read using ":r file.docx".

Please refer to http://vimdoc.sourceforge.net/htmldoc/autocmd.html for more information on autocmd.

## Using Emacs Editor

You can add following lines in your ~/.emacs file to view the text content of a .docx file directly when using emacs.

```
(add-to-list 'auto-mode-alist '("\\.docx\\'" . docx2txt))

(defun docx2txt ()
 "Run docx2txt on the entire buffer."
 (shell-command-on-region (point-min) (point-max) "docx2txt.pl" t t))
```

**Be warned** that with above ~/.emacs code addition, if you happen to save the buffer/file, it will overwrite the .docx file with the text content.

Please explore "Filters -- making things readable:" section at http://www.emacswiki.org/emacs/CategoryExternalUtilities for more ways to view .docx file text content directly in emacs.

## Who is using it

In case you have been using this tool directly/indirectly for non-personal work, please inform me about it with relevant URL (if available) so that a mention can be made here.

Wading through initial google search result pages reveals that this tool is directly/indirectly useful atleast in following cases.

* Corrupt Office File Text/Data Extracting Web Service | Corrupt Office Suite Text/Data Extracting Service - BETA - Paul had informed me about these in mail communication.
* eZimDMS
* Kino Search Contrib | Twiki?
* MPP?

Some users have been kind enough to inform about how they have used this utility in their work.

* "I've incorporated docx2txt into a system of hot folders I've implemented here." - Ian Hughson, Oxford University Press

## Support

In case you want to request features, report bugs, submit patches or just share your views on the project, please visit project summary page at SourceForge.net. A sample .docx file depicting the requested-feature/issue and the corresponding text file generated by Microsoft Office(Tm), with character substitution enabled, will be a helpful resource in implementing new features and fixing the bugs.

In case you want to pay for the development of specific features that you need, or customisation of docx2txt to suit your needs, please contact the docx2txt author (Sandeep Kumar) for details. 
