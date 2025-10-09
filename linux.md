✅ Quick Reference Table
| Purpose                     | Command Example                                |
| --------------------------- | ---------------------------------------------- |
| Find file by name           | `find / -name "file.txt"`                      |
| Find file by extension      | `find /home -name "*.log"`                     |
| Case-insensitive search     | `find / -iname "file.txt"`                     |
| Fast search (index-based)   | `locate file.txt`                              |
| Find executable             | `which python3`                                |
| Find and delete old backups | `find /backups -name "*.gz" -mtime +7 -delete` |


1. find — Most Common & Powerful
```
find /path/to/search -name "filename"
```
Examples:
# Search for a file named test.txt starting from root directory
```
find / -name "test.txt"
```

# Search case-insensitive
```
find /home -iname "test.txt"
```
# Search for all .log files in /var/log
```
find /var/log -type f -name "*.log"
```
# Search for directories named "backup"
```
find / -type d -name "backup"
```
# Search and show files modified in last 7 days
```
find /backups -name "*.sql.gz" -mtime -7
```
⚙️ 2. locate — Fastest (uses prebuilt database)
```
locate filename
```
Example:
```
locate mysql_backup
```

⚠️ If you just installed locate, first update its database:

sudo updatedb

🧩 3. grep with ls or cat — When searching inside files

If you want to search for text inside files:
```
grep -r "search_text" /path/to/search
```

Example:
```
grep -r "database_name" /etc/
```
🪶 4. which — Find executable path
```
which mysql
```
🧰 5. whereis — Find binary, source, and man page
```
whereis nginx
```
