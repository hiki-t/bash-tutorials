# grep exercises

<br/>
<br/>

### Exercise outline
- [easy](#easy)
- [medium](#medium)
- [hard](#hard)
- [more #1](#more1), eg BRE vs ERE
- [more #2](#more2), eg links to regex exercises, info

<br/>
<br/>

```
grep matching style
- egrep = grep -E   # extended-regexp (ERE)
- fgrep = grep -F   # fast ,,, ignore special characters as strings
- rgrep = grep -r   # recursive
- grep -G(basic-regexp, BRE, default)
- grep -P(perl)
```

```
SYNOPSIS
- grep [OPTIONS] PATTERN [FILE...]
- grep [OPTIONS] -e PATTERN ... [FILE...]
- grep [OPTIONS] -f FILE ... [FILE...]
```

```
two ways
1. [output or file] | grep [option] pattern [file]   # use a pipe
2. grep [option] pattern [file]   # use directly


eg
cat file.txt
hello

1. cat or ls | grep -i he
2. eg, grep -i he file.txt

```

```
### option

# Matching Control
# (******) is probably used most of time

grep -i # case-sensitive (******)
grep -w # find characters as an entire word, not characters within a word (******)
grep -v # exclude target characters (******)
grep -f # obtain PATTERN from FILE (***maybe)
grep -e # disambiguate against special characters, such as -foo, h|l|o, etc (***maybe)

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

# Context Line Control
grep  -B num # show lines before a line with target characters (******)
grep  -A num # show lines after a line with taraget characters (******)
grep  -C num # ?

# File and Directory Selection
etc

````

### Easy
- https://ostechnix.com/the-grep-command-tutorial-with-examples-for-beginners/

### Exercises - easy <a name="easy"></a>

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
$ grep tech file.txt
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

### Exercises - medium <a name="medium"></a>

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

eg
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

### Exercises - hard <a name="hard"></a>

- https://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html

more practical exercises

### More resources - more1 <a name="more1"></a>

```console

REGULAR EXPRESSIONS
       A regular expression is a pattern that describes a set of  strings.   Regular  expressions  are
       constructed  analogously  to  arithmetic  expressions,  by  using  various operators to combine
       smaller expressions.

       grep understands  three  different  versions  of  regular  expression  syntax:  “basic”  (BRE),
       “extended”  (ERE)  and  “perl”  (PCRE).   In  GNU  grep  there  is  no  difference in available
       functionality between basic and extended syntaxes.  In  other  implementations,  basic  regular
       expressions  are  less  powerful.   The  following  description  applies  to  extended  regular
       expressions; differences for  basic  regular  expressions  are  summarized  afterwards.   Perl-
       compatible   regular   expressions   give  additional  functionality,  and  are  documented  in
       pcresyntax(3) and pcrepattern(3), but work only if PCRE is available in the system.

       The fundamental building blocks are the regular expressions  that  match  a  single  character.
       Most  characters,  including  all  letters  and  digits,  are  regular  expressions  that match
       themselves.  Any meta-character with special meaning may be  quoted  by  preceding  it  with  a
       backslash.

       The period . matches any single character.

   Character Classes and Bracket Expressions
       A  bracket  expression  is  a  list  of  characters enclosed by [ and ].  It matches any single
       character in that list; if the first character of the list is the caret ^ then it  matches  any
       character not in the list.  For example, the regular expression [0123456789] matches any single
       digit.

       Within a bracket expression, a range expression consists  of  two  characters  separated  by  a
       hyphen.   It  matches  any  single  character that sorts between the two characters, inclusive,
       using the locale's collating sequence and character set.  For example, in the default C locale,
       [a-d]  is equivalent to [abcd].  Many locales sort characters in dictionary order, and in these
       locales [a-d] is typically not equivalent to [abcd]; it might be equivalent to  [aBbCcDd],  for
       example.   To  obtain  the traditional interpretation of bracket expressions, you can use the C
       locale by setting the LC_ALL environment variable to the value C.

       Finally, certain named classes of characters are  predefined  within  bracket  expressions,  as
       follows.   Their  names  are  self  explanatory,  and they are [:alnum:], [:alpha:], [:cntrl:],
       [:digit:], [:graph:], [:lower:], [:print:], [:punct:], [:space:],  [:upper:],  and  [:xdigit:].
       For  example,  [[:alnum:]]  means  the  character  class  of numbers and letters in the current
       locale.  In the C locale and ASCII character set encoding, this is  the  same  as  [0-9A-Za-z].
       (Note  that  the  brackets  in  these  class  names are part of the symbolic names, and must be
       included in addition to the brackets delimiting the bracket expression.)  Most  meta-characters
       lose  their  special meaning inside bracket expressions.  To include a literal ] place it first
       in the list.  Similarly, to include a literal ^ place  it  anywhere  but  first.   Finally,  to
       include a literal - place it last.

   Anchoring
       The  caret ^ and the dollar sign $ are meta-characters that respectively match the empty string
       at the beginning and end of a line.

   The Backslash Character and Special Expressions
       The symbols \< and \> respectively match the empty string at the beginning and end of  a  word.
       The  symbol  \b matches the empty string at the edge of a word, and \B matches the empty string
       provided it's not at the edge of a word.  The symbol \w is a synonym for [_[:alnum:]] and \W is
       a synonym for [^_[:alnum:]].

   Repetition
       A regular expression may be followed by one of several repetition operators:
       ?      The preceding item is optional and matched at most once.
       *      The preceding item will be matched zero or more times.
       +      The preceding item will be matched one or more times.
       {n}    The preceding item is matched exactly n times.
       {n,}   The preceding item is matched n or more times.
       {,m}   The preceding item is matched at most m times.  This is a GNU extension.
       {n,m}  The preceding item is matched at least n times, but not more than m times.

   Concatenation
       Two  regular  expressions  may  be  concatenated;  the resulting regular expression matches any
       string formed  by  concatenating  two  substrings  that  respectively  match  the  concatenated
       expressions.

   Alternation
       Two regular expressions may be joined by the infix operator |; the resulting regular expression
       matches any string matching either alternate expression.

   Precedence
       Repetition  takes  precedence  over  concatenation,  which  in  turn  takes   precedence   over
       alternation.   A  whole  expression may be enclosed in parentheses to override these precedence
       rules and form a subexpression.

   Back References and Subexpressions
       The back-reference \n, where n is a single digit, matches the substring previously  matched  by
       the nth parenthesized subexpression of the regular expression.

   Basic vs Extended Regular Expressions
       In  basic  regular  expressions  the  meta-characters  ?,  +, {, |, (, and ) lose their special
       meaning; instead use the backslashed versions \?, \+, \{, \|, \(, and \).

```

### More resources #2 <a name="more2"></a>
- https://regexcrossword.com/ # Regex Cross word
- https://www.regular-expressions.info/index.html # Regex exercises
- https://regexr.com/ # regex online tool #1
- https://www.regexpal.com/ # regex online tool #2
- https://rubular.com/ # regex online tool #3
- https://www.online-utility.org/text/grep.jsp # regex online tool #4

### Memo
- https://unix.stackexchange.com/questions/531591/grep-and-grep-f-differences (about basic regular expressions)
- https://unix.stackexchange.com/questions/50512/what-is-the-difference-between-grep-e-and-grep-e-option (about basic vs extended expressions, also The purpose of -e is really just to disambiguate when a regex starts with a dash)
- https://unix.stackexchange.com/questions/435412/e-option-in-command-grep (some explanations about grep -e)
