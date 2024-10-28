# grep examples

find the specific word:

count numbers of lines in the file:

```
grep -c '.' /usr/share/dict/words

```

find the occurence of pattern:

```
grep 'dog' /usr/share/dict/words

```

find the words starting with some letter:

```
grep '^Z' /usr/share/dict/words

```

find the words ending with some letter:

```
grep 'dog$' /usr/share/dict/words

```

ignore comments:

```
grep -v '^#' /etc/fstab

```

ignore comments and empty lines:

```
grep -v '^#' /etc/sudoers | grep -v '^$'

```

extended regulare expression:

```
grep -Ev '^#|^$' /etc/sudoers

```

prints also <N> lines after the matched line:

```
grep -A<N>
```

prints also <N> lines before the matched line:

```
grep -B<N>
```

recursively search given directory and match file contents:

```
grep -r
```

exclude all blank lines and those that start with #:

```
grep -v -e '^#' -e '^$' /etc/services
```

Grep lines with strings from a file (e.g. lines with ‘stringA or ‘stringB’ or ‘stringC’):

```
#with grep
test="stringA stringB stringC"
grep ${test// /\\\|} file.txt
# turning the space into 'or' (\|) in grep
```

Type of grep:

```
grep = grep -G # Basic Regular Expression (BRE)
fgrep = grep -F # fixed text, ignoring meta-characters
egrep = grep -E # Extended Regular Expression (ERE)
rgrep = grep -r # recursive
grep -P # Perl Compatible Regular Expressions (PCRE)
```

Grep and count number of empty lines:

```
grep -c "^$"
```

Grep and return only integer:

```
grep -o '[0-9]*'
#or
grep -oP '\d*'
```

Grep integer with certain number of digits (e.g. 3):

```
grep '[0-9]\{3\}'
# or
grep -E '[0-9]{3}'
# or
grep -P '\d{3}'
```

Grep only IP address:

```
grep -Eo '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}'
# or
grep -Po '\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}'
```

Grep whole word (e.g. ‘target’):

```
grep -w 'target'

#or using RE
grep '\btarget\b'
```

Grep returning lines before and after match (e.g. ‘bbo’):

```
# return also 3 lines after match
grep -A 3 'bbo'

# return also 3 lines before match
grep -B 3 'bbo'

# return also 3 lines before and after match
grep -C 3 'bbo'
```

Grep string starting with (e.g. ‘S’):

```
grep -o 'S.*'
```

Extract text between words (e.g. w1,w2):

```
grep -o -P '(?<=w1).*(?=w2)'
```

Grep lines without word (e.g. ‘bbo’):

```
grep -v bbo filename
```

Grep lines not begin with string (e.g. #):

```
grep -v '^#' file.txt
```

Grep variables with space within it (e.g. myvar=”some strings”):

```
grep "$myvar" filename
#remember to quote the variable!
```

Grep only one/first match (e.g. ‘bbo’):

```
grep -m 1 bbo filename
```

Grep and return number of matching line(e.g. ‘bbo’):

```
grep -c bbo filename
```

Count occurrence (e.g. three times a line count three times):

```
grep -i "bbo" filename
```

COLOR the match (e.g. ‘bbo’)!:

```
grep --color bbo filename
```

Grep search all files in a directory(e.g. ‘bbo’):

```
grep -R bbo /path/to/directory
# or
grep -r bbo /path/to/directory
```

Search all files in directory, do not ouput the filenames (e.g. ‘bbo’):

```
grep -rh bbo /path/to/directory
```

Search all files in directory, output ONLY the filenames with matches(e.g. ‘bbo’):

```
grep -rl bbo /path/to/directory
```

Grep OR (e.g. A or B or C or D):

```
grep 'A\|B\|C\|D'
```

Grep AND (e.g. A and B):

```
grep 'A.*B'
```

Regex any single character (e.g. ACB or AEB):

```
grep 'A.B'
```

Regex with or without a certain character (e.g. color or colour):

```
grep 'colou\?r'
```

Grep all content of a fileA from fileB:

```
grep -f fileA fileB
```

Grep a tab:

```
grep $'\t'
```

Grep variable from variable:

```
$echo "$long_str"|grep -q "$short_str"
if [ $? -eq 0 ]; then echo 'found'; fi
#grep -q will output 0 if match found
#remember to add space between []!
```

Grep strings between a bracket():

```
grep -oP '\(\K[^\)]+'
```

Grep number of characters with known strings in between(e.g. AAEL000001-RA):

```
grep -o -w "\w\{10\}\-R\w\{1\}"
# \w word character [0-9a-zA-Z_] \W not word character
```

Skip directory (e.g. ‘bbo’):

```
grep -d skip 'bbo' /path/to/files/*
```