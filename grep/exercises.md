# grep exercises

<br/>
<br/>

Exercises
- [easy](#easy)
- [medium](#medium)
- [hard](#hard)
- [more #1]()
- [more #2]()
- [more #3]()

<br/>
<br/>

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

```
### option

# Matching Control
(******) is probably used most of time

grep -i # case-sensitive (******)
grep -w # find characters as an entire word, not characters within a word (******)
grep -v # exclude target characters (******)
grep -f # file??? --------------------------------------------------------- to be checked
grep -e # ERE??? ---------------------------------------------------------- to be checked

# General Output Control
grep -c # count a number of matching lines (******)
grep -L # ?
grep -l # ?
grep -m num # stop searching after finding assigned "num"
grep -o # only show searched characters # what's a point of doing this????

# Output Line Prefix Control
grep -n # show line number on the left (******)
grep -b # distance from beginning of this file? # byte offset
grep -u # unix offset, but there is no output
grep -H # ?
grep -h # ?
grep --label # output as " grep: xxx: Is a directory " if it's a dir
grep -T # Make sure that the first character of actual line content lies on a tab stop
grep -z # Output a zero byte

Context Line Control
grep  -B num # show lines before a line with target characters (******)
grep  -A num # show lines after a line with taraget characters (******)
grep  -C num # ?

File and Directory Selection

````

### sample #2 - medium <a name="medium"></a>

- https://www.hackerrank.com/contests/bash-and-linux-shell-practice/challenges/text-processing-in-linux-the-grep-command-2

Task  
You are given a text file that will be piped into your command through STDIN. Use grep to display all those lines that contain the word the in them.
The search should NOT be sensitive to case.  
Display only those lines of the input file that contain the word 'the'.  

```
$ cat file.txt
From fairest creatures we desire increase,
That thereby beauty's rose might never die,
But as the riper should by time decease,
His tender heir might bear his memory:
But thou contracted to thine own bright eyes,
Feed'st thy light's flame with self-substantial fuel,
Making a famine where abundance lies,
Thy self thy foe, to thy sweet self too cruel:
Thou that art now the world's fresh ornament,
And only herald to the gaudy spring,
Within thine own bud buriest thy content,
And tender churl mak'st waste in niggarding:
Pity the world, or else this glutton be,
To eat the world's due, by the grave and thee.
When forty winters shall besiege thy brow,
And dig deep trenches in thy beauty's field,
Thy youth's proud livery so gazed on now,
Will be a tattered weed of small worth held:
Then being asked, where all thy beauty lies,
Where all the treasure of thy lusty days;
To say within thine own deep sunken eyes,
Were an all-eating shame, and thriftless praise.
How much more praise deserved thy beauty's use,
If thou couldst answer 'This fair child of mine
Shall sum my count, and make my old excuse'
```

```console

cat sample.txt | grep -in or   # find any words which contain 'or'
4:His tender heir might bear his memory:
9:Thou that art now the world's fresh ornament,
13:Pity the world, or else this glutton be,
14:To eat the world's due, by the grave and thee.
15:When forty winters shall besiege thy brow,
18:Will be a tattered weed of small worth held:
23:How much more praise deserved thy beauty's use,

cat sample.txt | grep -inw or   # find words which is same as 'or'
13:Pity the world, or else this glutton be,





# try to complete the above task

cat sample.txt | grep -in the
2:That thereby beauty's rose might never die,
3:But as the riper should by time decease,
9:Thou that art now the world's fresh ornament,
10:And only herald to the gaudy spring,
13:Pity the world, or else this glutton be,
14:To eat the world's due, by the grave and thee.
19:Then being asked, where all thy beauty lies,
20:Where all the treasure of thy lusty days;

cat sample.txt | grep -inw the
3:But as the riper should by time decease,
9:Thou that art now the world's fresh ornament,
10:And only herald to the gaudy spring,
13:Pity the world, or else this glutton be,
14:To eat the world's due, by the grave and thee.
20:Where all the treasure of thy lusty days;

```















