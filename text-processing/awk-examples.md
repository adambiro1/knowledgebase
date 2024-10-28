# awk_examples

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

create a csv file txt2csv.awk:

```
BEGIN {
  IFS="\t"
  OFS=","
}
{ print $1, $2, $3, $4, $5 }

```

run it:

```
awk -f txt2csv.awk file.dat > file.csv

```

Set tab as field separator

```
awk -F $'\t'
```

Output as tab separated (also as field separator)

```
awk -v OFS**=**'\t'
```

Pass variable

```
a**=**bbo;b**=**obb;
awk -v a**=**"$a" -v b**=**"$b" "$1==a && $10=b" filename
```

Print line number and number of characters on each line

```
awk '{print NR,length($0);}' filename
```

Find number of columns

```
awk '{print NF}'
```

Reverse column order

```
awk '{print $2, $1}'
```

Check if there is a comma in a column (e.g. column $1)

```
awk '$1~/,/ {print}'
```

Split and do for loop

```
awk '{split($2, a,",");for (i in a) print $1"\t"a[i]}' filename
```

Print all lines before nth occurrence of a string (e.g stop print lines when ‘bbo’ appears 7 times)

```
awk -v N**=**7 '{print}/bbo/&& --N<=0 {exit}'
```

Print filename and last line of all files in directory

```
ls|xargs -n1 -I file awk '{s=$0};END{print FILENAME,s}' file
```

Add string to the beginning of a column (e.g add “chr” to column $3)

```
awk 'BEGIN{OFS="\t"}$3="chr"$3'
```

Remove lines with string (e.g. ‘bbo’)

```
awk '!/bbo/' file
```

Remove last column

```
awk 'NF{NF-=1};1' file
```

Usage and meaning of NR and FNR

```
awk 'print FILENAME, NR,FNR,$0}' fileA fileB
```

### AND gate

```
awk -v OFS='\t' 'NR=FNR{a[$1]=$2;next} NF {print $1,((a[$1]=$2)? $2:"0")}' fileA fileB
```

Round all numbers of file (e.g. 2 significant figure)

```
awk '{while (match($0, /[0-9]+\[0-9]+/)){
    \printf "%s%.2f", substr($0,0,RSTART-1),substr($0,RSTART,RLENGTH)
    \$0=substr($0, RSTART+RLENGTH)
    \}
    \print
    \}'
```

Give number/index to every row

```
awk '{printf("%s\t%s\n",NR,$0)}'
```

Break combine column data into rows

```
awk '{split($2,a,",");for(i in a)print $1"\t"a[i]}' file

```

Average a file (each line in file contains only one number)

```
awk '{s+=$1}END{print s/NR}'
```

Print field start with string (e.g Linux)

```
awk '$1 ~ /^Linux/'
```

Sort a row (e.g. 1 40 35 12 23 –> 1 12 23 35 40)

```
awk ' {split( $0, a, "\t" ); asort( a ); for( i = 1; i <= length(a); i++ ) printf( "%s\t", a[i] ); printf( "\n" ); }'
```

Subtract previous row values (add column6 which equal to column4 minus last column5)

```
awk '{$6 = $4 - prev5; prev5 = $5; print;}'
```

```
awk '$5 ~ /.something/{print $1,$3,substr($4,1,6),$5,$9,$13}' 20231031-00.log
```

script:

```
#!/usr/bin/awk -f 

BEGIN {
	FS=";";
}
```

list users with uid higher than 1000:

```
awk -F : '{ if ($3 >= 1000 && $1 != "nobody" ) print $1 }' /etc/passwd
```

### awk-if

```
awk '{if ($1 > 10) print "greater than 10"; else print "less than or equal to 10"}' file.txt
```

### awk-while

```
awk '
{
    i = 1
    while (i <= 3) {
        print $i
        i++
    }
}' inventory-shipped
```

```
awk '{i=1; while (i<=10) {print i; i++}}' file.txt
```

### awk-do while

```
{
    i = 1
    do {
        print $0
        i++
    } while (i <= 10)
}
```

```
awk '{i=1; do {print i; i++} while (i<=10)}' file.txt
```

### awk-for

```
awk '
{
    for (i = 1; i <= 3; i++)
        print $i
}' inventory-shipped
```

```
awk '{for (i=1; i<=10; i++) {print i}}' file.txt
```

### awk-switch

```
awk '{switch($1) {
case "apple": 
print "This is an apple"; 
break; 
case "banana": 
print "This is a banana"; 
break; 
default: print "This is neither an apple nor a banana"; 
break;}}' file.txt
```

**array**:

```
# Declare an array and assign values to it
awk 'BEGIN { arr[1] = "apple"; arr[2] = "banana"; arr[3] = "cherry"; }'

# Access the array elements
awk 'BEGIN { arr[1] = "apple"; arr[2] = "banana"; arr[3] = "cherry"; print arr[2]; }'
```