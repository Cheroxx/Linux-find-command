### Linux find command

The **find** command is a great tool in Linux to quickly and easily find a specific file or something interesting in a Linux filesystem.

Here is a quick tutorial on how to use the find command in Linux to search for what you need.

Syntax is **find** *where* *what*

For example `find /home/bob thisfile.txt`

You can use wildcards to expand your search

For example `find secretfile*` to search the current directory using a wildcard

Use *find /* if you want to search the whole Linux filesystem

For example `find / lookeverywhere.txt`

Use the *-type d* flag to search for directories or *-type f* to search for files.

For example `find / -type f myfile.txt` or `find / -type d hostdir`

Use *-name* (case sensitive) or *-iname* (case insensitive) to specify a name or pattern to look for. You can use wildcards too, just make sure to wrap them in "quotes"

Examples:
```
find / -type f -name "*.xml" 
find /home -type f -iname user.txt 
find / -type d -name "*exploits"
```

You can specify the owner, size, permissions, and the time the file was last accessed/modified as well...

Use the *-user* flag to specify the username of the owner.

For example `find / -type d -user kittycat`

Use the *-group* flag to specify the group the file belongs to.

For example `find /home -group accounting -name annualreport.xml`

Or the *-size* flag to specify the size of files using a suffix, *c* for bytes, *k* for KiB’s, and *M* for MiB’s

Examples:
```
find / -type f -iname Secretfile.txt -size 150c 
find /home -type f -size -n 2k -name "*.txt" 
```
*-n*, *+n*, and *n* indicates less than, greater than, or equal to

Perhaps the most interesting flag is the *-perm* switch to specify permissions in octal (644) or symbolic (u=r) form. This returns files with those exact permissions.  The *-perm* flag is often used to quickly find setuid binaries for a potential privilege escalation route.

Examples: 
```
find / -type f -perm 644 
find / -type f -perm -4000 setuidbinaries 2>/dev/null
find / -type f -perm /o=w -name "*.sh" 
find /usr/bin -type f -user=root -perm -u=s
```

You can also search for and retrieve Linux files based on a specific timeframe they were accessed *-a*, changed *-c*, or modified *-m*

Examples: 
```
find / -type f -atime 10 -name "latestfile.txt" 
find /usr/bin -type f -mmin 120
```

For a clean list of results, use *2>/dev/null* to suppress the output of errors.

You can execute other actions within the **find** command.  You can execute commands in your find command with the *-exec* flag.  You can delete a file with the *-delete* flag.  You can enumerate a complete directory traversal including user, group, and permissions and pipe it into readable columns.

For example `find /home -printf “%f\t%p\t%u\t%g\t%m\n” 2>/dev/null | column -t`

Of course, there is infinitely more you can do with the **find** command to simplify searches in Linux, enumerate Linux boxes more efficiently, and identify potential privilege escalation vectors as well. So remember the usefulness and great utility of basic commands such as **find** in all levels of research!
