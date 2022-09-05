# File Labelling Conventions

## File types

### Single

A stand-alone, contextually self-contained file.

Format:

- `[temp_prefix]_?<name>_<date*created>*?[other].<ext>`

### Split

Join into Single (if possible), or place into archive.

Format:

- `[temp_prefix]_?<name>_<date*created>*?[other]-00<[0-9]+>.<ext>`

### Partial

Treat the same as Single, but ensure `~` tag in `[other]` location.

### Archive

If Split, name the same as the equivalent joined Single.

If mixed Singles and/or folders, label as appropriate \-
containing as much information as is pertinent.
