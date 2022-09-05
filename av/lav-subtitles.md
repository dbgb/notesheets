# Subtitles

There are 4 different modes to be used for subtitle selection. Some of the
modes will use the preferred languages in a similar way as the audio languages,
the syntax for entering them is the same as well.

## “No Subtitles”

No subtitles will be selected.

## “Only Forced Subtitles”

Only subtitles marked as “forced” will be used, taking the preferred subtitle
languages into account.

## “Default”

The “Default” mode will select subtitles in accordance with the typical
interpretation of the Matroska spec. That means that subtitles matching your
language preference will be loaded, as well as subtitles marked “default” or
“forced”. If none of these factors apply, no subtitles will be loaded.

## “Advanced”

The advanced selection mode is the most flexible mode, and allows you to fully
control which subtitles get selected. In addition to the rules already used in
the other modes, it is also possible to use the audio language to determine
which subtitle should be loaded. Example: You want no subtitles with English
audio, but you do want subtitles with German audio. This is possible in advanced
mode.

The advanced mode uses a different syntax for the preferred language field to
enable these rules. Instead of a single language tag, a combined tag of audio
and subtitle language is required (separated by a colon). The most basic tag
would look like this: `ger:eng`. In this case, the interpretation would be “If
Audio is German, use English subtitles”.

Note: Even though this may feel similar to the selectors Haali’s Media Splitter
offers, LAV’s implemention does not allow you to speficy which audio stream is
used through the advanced selectors, the audio language is only used to select
which subtitles are used.

In addition to simply using two language tags, you can use the `_` character to
match all languages, or the `off` token to disable subtitles. For example,
following tag will enable any subtitles when the audio is english, and disable
subtitles otherwise: `eng:_;off`.

As you’ve seen in the previous example, multiple rules can be concatenated using
a semi-colon (or a space) to build rule chains. Again, everything is interpreted
from left to right.

The example also shows that the audio language tag is optional. Consider
following rule: `_:eng`. This rule means “Use English subtitles when Audio is \_”.
This rule applies to all audio languages, so you can omit the \* and just write
`eng`, which has the exact same meaning.

To complete the advanced mode, there are a number of flags for “default”,
“forced”, “hearing impaired” and “normal” subtitles which are supported. The
flags are identified by their first letter, and appended to the subtitle
language separated by a pipe character `|`. As an example, following rule will
select any “forced” subtitles, and turn off subtitles otherwise: `_:_|f;\*:off`

To finish the section about advanced subtitles, here some examples of rules to
inspire you:

`_:eng;_:_|f;_:\*|d` This is the rule equal to the “Default” subtitle mode with
English as a preferred language.

`\*|n` Select all normal subtitles, meaning “not forced, not default and not
hearing impaired”

`eng:eng|f;ger:ger|f` Load English “forced” subtitles if audio is English, load
German “forced” subtitles if audio is German, no subs otherwise.

`eng:off;fre:eng;\*|d` English Audio: Turn subs off; French Audio: English subs;
Any other audio: try to find subtitles flagged “default”.

---

### References

[1f0.de](https://1f0.de/lav-splitter/lav-splitter-stream-selection)
