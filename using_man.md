# man tips for quick search

search with the keyword:

```
man -k keyword
```

can use apropos instead of man -k:
```
apropos keyword
```

filter commands using grep:

```
man -k password | grep 5
```

most relevant sections:

1: Executble programs or shell commands

5: File formats and conventions

8: System administration commands

search only for short description:

```
man -f somecommand
```

update mandb database, run this command as a root:

```
mandb
```

---

some commands have their documentation in the info system,
when for example some documentation is maintained as a Texinfomanual:
```
pinfo
```

navigate *up* and *down* arrows use *n* to go to next page use *p* to go to previous and *u* to get back and up in hierarchy 