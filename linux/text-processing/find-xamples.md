# find_examples

basic usage:

```
find / -name "Foo.txt"

```

find directories:

```
find ~/ -type d
```

change permissions on mulitple files(if want to confirm every file write -ok instead of exec):

```
sudo find / -iname '*.conf' -exec chmod 644 {} \;
```

List all sub directory/file in the current directory

```
find .
```

List all files under the current directory

```
find . -type f
```

List all directories under the current directory

```
find . -type d
```

Edit all files under current directory (e.g. replace ‘www’ with ‘ww’)

```
find . -name '*.php' -exec sed -i 's/www/w/g' **{}** \;

*# if there are no subdirectory*
replace "www" "w" -- ******# a space before **
```

Find and output only filename (e.g. “mso”)

```
find mso*****/ -name M***** -printf "%f\n"
```

Find large files in the system (e.g. >4G)

```
find / -type f -size +4G
```

Find and delete file with size less than (e.g. 74 byte)

```
find . -name "*.mso" -size -74c -delete

*# M for MB, etc*
```

Find empty (0 byte) files

```
find . -type f -empty
*# to further delete all the empty files*
find . -type f -empty -delete
```

Recursively count all the files in a directory

```
find . -type f | wc -l
```