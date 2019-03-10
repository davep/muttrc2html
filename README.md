# muttrc2html

## Usage

This little perl script is a simple attempt at a muttrc to HTML converter.
It could come in handy if you want to publish your muttrc file on your web
pages.

The basic idea behind the script is that it should make comments stand out
and should also allow hypertext links to other rc files that you source in.

Running the script is simply a case of typing 'muttrc2html' at the shell
prompt. By default the script will look for ~/.muttrc and start to convert
it to a HTML file in the current directory. You can change the behaviour of
the script with settings in a file called ~/.muttrc2htmlrc. Valid settings
are:

```
muttrc=<Location of top level muttrc file>
TitlePrefix=<Prefix for each web page title>
Ignore=<Name of rc file or regular expression>
Silent=<1 for don't give info, 0 for do give info>
BeginComment=<Opening tag for a comment>
EndComment=<Closing tag for a comment>
BodyTag=<Tag to declare the start of the document body>
ManualVars=<URL of section 6 of the mutt manual>
```

For example, a ~/.muttrc2htmlrc might look like:

```
muttrc=~/.muttrc
TitlePrefix=Dave's mutt config
Silent=1
Ignore=~/.mutt/mail_aliases
Ignore=~/.mutt/defaults.private
BeginComment=<STRONG><FONT COLOR="#FF0000">
EndComment=</FONT></STRONG>
BodyTag=<BODY BGCOLOR="#FFFFFF">
ManualVars=http://www.mutt.org/doc/manual/manual-6.html
```

As you can see, you can repeat the "ignore" setting as many times as
you like. Also, note that the ignore lines can use regular expressions,
for example:

```
ignore=private$
```

would ignore any file whose names ends with the text "private".

## Hiding portions of your rc files

For various reasons there maybe portions of your rc files that you don't
want to be made visible. While the "Ignore" rules work for whole files
this doesn't help if there is just one line or a block of lines (obviously
you could place those private portions in their own rc files and ignore
them, but that could get messy).

To help solve this problem muttrc2html will ignore all lines between the
comments `# BeginHTMLIgnore` and `# EndHTMLIgnore`. For example:

```
set foo=bar
source ~/.mutt/make.coffee.macro
# BeginHTMLIgnore
set rootpassword=wibble
# EndHTMLIgnore
```

It ain't perfect, but it should help. BTW, don't take my word that this
will work, please check that you don't include sensitive text in the
final HTML. Obvious things to check for are passwords (such as the
setting for $pop_pass for example).

## Bugs

- It assumes too much about the setup of your system.
- It doesn't handle more than one source statement on any one line.
- A load more issues I've not considered.

If you find any problems or come up with any enhancements please feel free
to send them to me.

## ToDo

- Fix bugs.

[//]: # (README.md ends here)
