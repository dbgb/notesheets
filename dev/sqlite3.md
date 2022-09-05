# Working with SQLite3: Notesheet

## Exploring Firefox cookie database

```shell
which sqlite3

cd /c/Users/<user_name>/AppData/Roaming/Mozilla/Firefox/profiles/<profile_key>.default
```

```sqlite3
sqlite3 cookies.sqlite

.help

.databases

select * from moz_cookies where name="<cookie_name>";

.exit
```

---

[SQLite CLI](https://sqlite.org/cli.html)
