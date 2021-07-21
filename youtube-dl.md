# Download playlist
## As music
`youtube-dl --extract-audio --audio-format mp3 -o "%(title)s.%(ext)s" <url to playlist>`
### skip existing files 



With the option --download-archive FILE youtube-dl both reads and adds to a list of files not to download again. Every time a file is successfully downloaded, that video id is added to FILE.

You can use it as follows:

`youtube-dl --download-archive downloaded.txt --no-post-overwrites -ciwx --audio-format mp3 -o "%(title)s.%(ext)s" [path here]`

It will redownload any videos from before that you didn't keep for one last time as it creates the list. You can now delete them.

If your MP3 files had been named with the default format of %(title)s-%(id)s.%(ext)s, you could have avoided the redownload by creating downloaded.txt from the youtube %(id)s in a bash terminal as follows:
```
for n in *.mp3
do if [[ "$n" =~ -[-_0-9a-zA-Z]{11}.mp3$ ]]
   then echo "youtube ${n: -15: 11}" >> downloaded.txt
   fi
done
```

