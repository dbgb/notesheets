# Useful [mkvpropedit][1] Examples

> mkvpropedit -- Modify properties of existing Matroska files without a complete
> remux

## Change selected default tracks for all MKV files in a directory

```shell
for f in *.mkv;
do /c/scripts/mkvpropedit.exe "$f"\
 --edit track:s1 --set flag-default=1\
 --edit track:a1 --set flag-default=0\
 --edit track:a2 --set flag-default=1;
done
```

## Disable the given subtitle track for every MKV file in the directory

Useful for when subtitles and audio are the same language type, but subs are
enabled by default.

```shell
for f in \*.mkv;
do /c/scripts/mkvpropedit.exe "$f" --edit track:s1 --set flag-enabled=0;
done
```

---

---

[1]: https://mkvtoolnix.download/doc/mkvpropedit.html
