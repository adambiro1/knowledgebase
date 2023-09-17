## grep

find the specific word:
```
grep "dog" /usr/share/dict/words
```
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


## SED

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


## AWK

basic usage:
```
awk 'pattern { action }'
```

Print out whole file:
```
awk '{ print }' <filename>
```

Print exact collumn:
```
awk '{ print $11, $3 }' <filename>
``` 

Patern Matching:
```
awk '/<word>/ { print $11, $3 }' <filename>
```

Use comparison operators:
```
awk '$2==<pattern> { print $11, $3 }' <filename>

awk '$3 > 5 { print $11, $3 }' <filename>
```

Combine patterns with logical operators:
```
awk '/pattern/ && $3 > 5 { print $11, $3 }' <filename>
```

Print header line with a user of Begin and printf:
```
awk 'BEGIN { printf("%-26s %s\n", "Command", "CPU%")} $3 > 10 { print $11, $3 }' <filename>
```

Manipulate output divide collumn value:
```
awk '/pattern/ { print $11, $6/1024 }' <filename>
```

Change also end of the output:
```
awk 'BEGIN { sum=0 } /pattern/ { sum+=$6 } END { printf("<message>: %.0f MB\n", sum/1024) }' <filename>
```

print number of fields with NF:
```
awk '{ print NF, $1 }' <file>
```

delete empty lines in file:
```
awk 'NF > 0 { print }' <file>
```

print line numbers with NR variable:
```
awk '{ print NR, $0 }' <file>
```



## printf

-display the given string, number or any other format specifier on the terminal window

print strings:
```
printf "%s\n" "Hello, World!"
```

print numbers:
```
printf "%d\n" "213" "109"
```

print logged in user:
```
printf "Hi, I'm %s.\n" $LOGNAME
```

print home directory:
```
printf "Your home folder is %s.\n" $HOME
```

## Find

-search for files in a directory hierarchy

basic usage:
```
find / -name "Foo.txt"
```

find directories:
```
find ~/ -type d
```