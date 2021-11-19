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
# Youtube-dl being throttled?
It used to download very fast 3.5MB/s, now it hangs for a few seconds and then downloads at only 75KBs.

Also seems to happen when you load the file url in Firefox, and then save it from FF.

i.e Youtube-dl -g -f 140 videourl (gives the direct url of the m4a audio) - paste url into FF, same slow speed.

So I guess it's not just Youtube-dl.

EDIT
This should work for Windows users, maxes out my connection for the most part.
https://chocolatey.org/packages/aria2

`youtube-dl VideoUrl -f 140 --external-downloader aria2c --external-downloader-args "-j 8 -s 8 -x 8 -k 5M"`
Replace 140 with chosen format.
.

For larger files "-j 12 -s 12 -x 12 -k 5M" may work better . Try 12 or 16

Works with other options too i.e

`youtube-dl -f bestaudio[ext=m4a] --external-downloader aria2c --external-downloader-args "-j 8 -s 8 -x 8  
-k 5M" --restrict-filenames -o "%%(title)s.%%(ext)s" --postprocessor-args "-ar 44100 -ac 1" --add-  
metadata --embed-thumbnail --playlist-items 1 https://www.youtube.com/playlist?list=PlaylistID`

or 

`youtube-dl -f best --external-downloader aria2c --external-downloader-args "-j 16 -x 16 -s 16 -k 1M" https://www.youtube.com/watch?v=blablablabla1 `

There is an option, [clearly mentioned in the documention][1]:

Subtitle Options:
-----------------

    --write-sub                      Write subtitle file
    --write-auto-sub                 Write automatic subtitle file (YouTube only)
    --all-subs                       Download all the available subtitles of the video
    --list-subs                      List all available subtitles for the video
    --sub-format FORMAT              Subtitle format, accepts formats preference, for example: "srt" or "ass/srt/best"
    --sub-lang LANGS                 Languages of the subtitles to download (optional) separated by commas, use IETF language tags like 'en,pt'

So for example, to list all subs for a video:

    youtube-dl --list-subs https://www.youtube.com/watch?v=Ye8mB6VsUHw

To download all subs, but not the video:

    youtube-dl --all-subs --skip-download https://www.youtube.com/watch?v=Ye8mB6VsUHw

  [1]: https://github.com/rg3/youtube-dl/#subtitle-options
