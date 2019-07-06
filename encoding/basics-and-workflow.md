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
As said earlier, all programs but qaac do not require installation.
But, for the ease of use, we suggest adding them to PATH,
and for the purpose of this guide we will assume you've done it.

Because qaac is basically a frontend to Apple's AAC encoder,
which is proprietary, it will require some additional configuration. 
For legal reasons the encoder itself can't be included in the package
and needs to be extracted from iTunes installation file.

Go to [qaac's download page][qaac] and download the newest build
(at the time of writing, `qaac_2.68.zip`) and the `makeportable.zip` file.
Extract the `x64` folder wherever you want your qaac folder to be,
then extract contents of `makeportable.zip` to it.
Next, download [iTunes installation file][itunes] (`iTunesSetup.exe`)
and move it to the `x64` folder.
Now just run the `makeportable.cmd` script
and it will automatically extract and configure everything.
Done, you can now delete the iTunes installation file.

[itunes]: https://secure-appldnld.apple.com/itunes12/041-02279-20180912-24D8EE3A-AC7A-11E8-BE19-C36F1B1141A5/iTunesSetup.exe
[qaac]: https://sites.google.com/site/qaacpage/cabinet

## Muxing

mkvtoolnix
