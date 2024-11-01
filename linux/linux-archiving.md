# linux-archiving

Create an archive:

```
tar -cf archivename.tar /files-you-want-to-archive
```

also see what is happening using -v option:

```
tar -cvf archivename.tar /files-you-want-to-archive
```

add file to an existing file use -r option:

```
tar -rvf archivename.tar /files-you-want-to-add
```

update archive with -u option:

```
tar -rvf archivename.tar /never-versions-of-archived-files
```

view what is in your archive:

```
tar -tvf archivename.tar
```

extract an archive be carefull where you do it you can cd or set a location with -C option:

```
tar -xvf archivename.tar -C /targetdir
```

extract certain file:

```
tar -xvf archivename.tar file-you-want-to-extract
```

c Creates an archive.
v Shows verbose output while tar is working.
t Shows the contents of an archive.
z Compresses/decompresses the archive while creating it, by using gzip.
j Compresses/decompresses the archive by using bzip2.
J Compresses/decompresses the archive using xz.
x Extracts an archive.
u Updates an archive; only newer files will be written to the archive.
C Changes the working directory before performing the command.
r Appends files to an archive.


### gzip

compress an archive using gzip:

```
gzip archivename.tar
```

uncompress an compressed file using gunzip:

```
gunzip archivename.tar.gz
```

### bzip2

compress archive with bzip2:

```
bzip2 archivename.tar
```

uncompress an compressed file using bunzip2:

```
bunzip2 archivename.tar.bz2
```