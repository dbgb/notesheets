# Renaming Torrent Files

_If you want to store a torrent with a custom name:_

1. Load it from anywhere, but don't start it. The file location doesn't matter
   as the client works from a copy in the "store torrents in" directory after
   load.

2. Rename the torrent in the client window. If this is not done before the
   torrent completes, the default name of the "store torrents in" directory
   torrent copy will be used (usually the cause of derpy torrent names).

3. If files already exist, force re-check; If not, allow them to download.

4. On completion, the torrent will be moved to the "store completed in"
   directory with the name it was assigned in the client window, rather than its
   default name.
