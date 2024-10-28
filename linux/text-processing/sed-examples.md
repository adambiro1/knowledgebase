# sed_examples

replace all "foo" with "bar":

```
sed -i '/foo/bar/g' inputfile

```

replace only in second line:

```
sed '/second/s/should/will/' inputfile

```

replace with case insensitive:

```
echo "Hello World" | sed 's/world/there/I'

```

print three lines and quit:

```
sed -n '1,3p' /etc/passwd

#or

sed '3q' /etc/passwd

```

Remove the 1st line:

```
sed 1d filename
```

Remove the first 100 lines (remove line 1-100):

```
sed 1,100d filename
```

Remove lines with string (e.g. ‘bbo’):

```
sed "/bbo/d" filename
# case insensitive:
sed "/bbo/Id" filename
```

Remove lines whose nth character not equal to a value (e.g. 5th character not equal to 2):

```
sed -E '/^.{5}[^2]/d'
#aaaa2aaa (you can stay)
#aaaa1aaa (delete!)
```

Edit infile (edit and save to file), (e.g. deleting the lines with ‘bbo’ and save to file):

```
sed -i "/bbo/d" filename
```

When using variable (e.g. $i), use double quotes “ “:

```
# e.g. add >$i to the first line (to make a bioinformatics FASTA file)
sed "1i >$i"
# notice the double quotes! in other examples, you can use a single quote, but here, no way!
# '1i' means insert to first line
```

Using environment variable and end-of-line pattern at the same time:

```
# Use backslash for end-of-line $ pattern, and double quotes for expressing the variable
sed -e "\$s/\$/\n+--$3-----+/"
```

Delete/remove empty lines:

```
sed '/^\s*$/d'

# or

sed '/^$/d'
```

Delete/remove last line:

```
sed '$d'
```

Delete/remove last character from end of file:

```
sed -i '$ s/.$//' filename
```

Add string to beginning of file (e.g. “[”):

```
sed -i '1s/^/[/' file
```

Add string at certain line number (e.g. add ‘something’ to line 1 and line 3):

```
sed -e '1isomething' -e '3isomething'
```

Add string to end of file (e.g. “]”):

```
sed '$s/$/]/' filename
```

Add newline to the end:

```
sed '$a\'
```

Add string to beginning of every line (e.g. ‘bbo’):

```
sed -e 's/^/bbo/' filename
```

Add string to end of each line (e.g. “}”):

```
sed -e 's/$/\}\]/' filename
```

Add \n every nth character (e.g. every 4th character):

```
sed 's/.\{4\}/&\n/g'
```

Add a line after the line that matches the pattern (e.g. add a new line with “world” after the line with “hello”):

```
sed '/hello*/a world' filename
# hello
# world
```

Concatenate/combine/join files with a separator and next line (e.g separate by “,”):

```
sed -s '$a,' *.json > all.json
```

Substitution (e.g. replace A by B):

```
sed 's/A/B/g' filename
```

Substitution with wildcard (e.g. replace a line start with aaa= by aaa=/my/new/path):

```
sed "s/aaa=.*/aaa=\/my\/new\/path/g"
```

Select lines start with string (e.g. ‘bbo’):

```
sed -n '/^@S/p'
```

Delete lines with string (e.g. ‘bbo’):

```
sed '/bbo/d' filename
```

Print/get/trim a range of line (e.g. line 500-5000):

```
sed -n 500,5000p filename
```

Print every nth lines:

```
sed -n '0~3p' filename

*# catch 0: start; 3: step*
```

Print every odd # lines

```
sed -n '1~2p'
```

Print every third line including the first line

```
sed -n '1p;0~3p'
```

Remove leading whitespace and tabs

```
sed -e 's/^[ \t]*//'
*# Notice a whitespace before '\t'!!*
```

Remove only leading whitespace

```
sed 's/ *//'

*# notice a whitespace before '*'!!*
```

Remove ending commas

```
sed 's/,$//g'
```

Add a column to the end

```
sed "s/$/\t$i/"
*# $i is the valuable you want to add
# To add the filename to every last column of the file*
**for** i **in** $(ls); **do** sed -i "s/$/\t$i/" $i; **done**
```

Add extension of filename to last column

```
**for** i **in** T000086_1.02.n T000086_1.02.p; **do** sed "s/$/\t**${**i/*./**}**/" $i; **done** **>**T000086_1.02.np
```

Remove newline\ nextline

```
sed ':a;N;$!ba;s/\n//g'
```

Print a particular line (e.g. 123th line)

```
sed -n -e '123p'
```

Print a number of lines (e.g. line 10th to line 33 rd)

```
sed -n '10,33p' <filename
```

Change delimiter

```
sed 's=/=\\/=g'
```

Replace with wildcard (e.g A-1-e or A-2-e or A-3-e….)

```
sed 's/A-.*-e//g' filename
```

Remove last character of file

```
sed '$ s/.$//'
```

Insert character at specified position of file (e.g. AAAAAA –> AAA#AAA)

```
sed -r -e 's/^.{3}/&#/' file
```