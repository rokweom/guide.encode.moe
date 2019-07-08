# Basics and General Workflow

## Preparation

downloading a source, looking at the video, some decisions
(resolution(s) for the release, audio codec, group-specific
requirements)


## Writing the Script

imports, source filter (mention lsmash, ffms2), examples for resizing,
debanding, AA. with images if possible

## Encoding the Result

{% term %}
$ vspipe.exe script.vpy -y - | x264.exe --demuxer y4m --some example --parameters here --output video.264 -
{% endterm %}

```sh
$ vspipe.exe script.vpy -y - | x264.exe --demuxer y4m --some example --parameters here --output video.264 -
```

Editors for VapourSynth usually have inbuilt support for encoding
scripts you wrote. Use `%encode --y4m <clip_variable>` in Yuuno or the GUI
provided by VSEdit.


## Transcoding Audio

### Setting up qaac

As said earlier, only qaac will require configuration,
and everythig else can simply be extracted wherever you like.
But, for the ease of use, we suggest adding them to PATH,
and for the purpose of this guide we will assume you've done it.

Because qaac is basically a frontend to Apple's AAC encoder,
which is proprietary, it will require some additional configuration. 
For legal reasons the encoder itself can't be included in the package
and needs to be extracted from iTunes installation file.

* go to [qaac's download page][qaac] and download the newest build
(at the time of writing, `qaac_2.68.zip`) and the `makeportable.zip` file
* extract the `x64` folder wherever you want your qaac folder to be,
then extract contents of `makeportable.zip` to it
* download the [iTunes installation file][itunes] (`iTunes64Setup.exe`)
and move it to the `x64` folder.
* run the `makeportable.cmd` script
* done, you can now delete the iTunes installation file.

[itunes]: https://secure-appldnld.apple.com/itunes12/031-69284-20160802-7E7B2D20-552B-11E6-B2B9-696CECD541CE/iTunes64Setup.exe
[qaac]: https://sites.google.com/site/qaacpage/cabinet


### Decoding audio with ffmpeg and piping it out

Basic ffmpeg usage is very simple—you just need to specify the input file,
and the name and extension of your desired output file, like this:
```
ffmpeg -i "input.dts" "output.wav"
``` 
This command will decode the DTS audio file and save it as a wav file.
Of course, this command doesn't contain any configuration whatsoever,
so ffmpeg will resort to using its defaults.

For transcoding audio,
only a little bit of configuration will be needed:
```
ffmpeg -i "input.dts" -acodec pcm_s24le "output.wav"
```
The `-acodec pcm_s24le` parameter will make sure
that ffmpeg will output in 24 bits;
otherwise it will output 16 bits by default.
If your source file is 16 bits, change this parameter to `pcm_s16le`,
or simply skip it.


Now, the command above will decode the source file
and save a resulting wav file on your drive.
You can then use this file to encode a FLAC or AAC file,
but there is a faster and more convinient way to do that—piping.
Piping skips the process of writing
and reading the data from the drive
and simply sends the data straight from one program to another.

To pipe from ffmpeg, specify the output format as wav using the `-f` option,
replace the output file name with a hyphen and place a pipe symbol at the end,
which will be used separate the ffmpeg command from your encoder command, like this:
```
ffmpeg -i "input.dts" -acodec pcm_s24le -f wav -|
```


## Muxing

mkvtoolnix
