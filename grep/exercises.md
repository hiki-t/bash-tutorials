# grep exercises

outline
- [exercise - easy](#easy)
- [exercise - medium](#medium)
- [exercise - hard](#hard)


grep matching style
- egrep = grep -E   # extended-regexp (ERE)
- fgrep = grep -F   # fast ignore special characters
- rgrep = grep -r   # recursive
- 
- grep -G(basic-regexp, BRE)
- grep -P(perl)

### Easy
- https://ostechnix.com/the-grep-command-tutorial-with-examples-for-beginners/

SYNOPSIS
- grep [OPTIONS] PATTERN [FILE...]
- grep [OPTIONS] -e PATTERN ... [FILE...]
- grep [OPTIONS] -f FILE ... [FILE...]

two ways
1. output or file | grep option pattern   # using pipe
2. grep option pattern file   # use directly

<br/>
<br/>

### sample #1 - easy <a name="easy"></a>

```
$ cat file.txt
ostechnix
Ostechnix
o$technix
linux
linus
unix
technology
hello world
HELLO world
```

eg

```console
grep tech file.txt
ostechnix
Ostechnix
o$technix
technology

$ grep ^tech file.txt
technology

# memo
# ^ only works from the beginning of the line, not middle of the line
# same applies for $
# when searching for any x character within a word, use .n for example
```

<br/>
<br/>

### sample #2 - medium <a name="medium"></a>























Here's a sentence with a footnote. [^1]

[^1]: This is the footnote.
