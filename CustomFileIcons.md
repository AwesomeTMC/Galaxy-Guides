# Adding new File Select Icons with PTD
PTD allows you to add new file select icons! But it takes a few steps.
# What you need for this tutorial
* PTD installed
* Knowledge on how to open an arc and replace files in them (with WiiExplorer)
* Basic knowlege on how to use Whitehole's BCSV editor
* Knowledge on how to use brawlbox
* Knowledge on how to use pygapa

# Adding a new message
Technically, this step is optional...if you want your icon to be named "InvalidName".

Using galaxymsbt (link), open `LocalizeData/{Language}/LayoutMessage.arc`. Open Layout_FileSelect and add a new message entry. Call it `System_FileSelect_Icon00[INDEX]` Then, edit it to be whatever you want!*

*Must be under 13 characters total or it will be cut off. This includes spaces.
# Adding the model
This step is critical. Open whitehole's bcsv editor and open:

Archive: `/ObjectData/FileSelectData.arc`

File: `/FileSelectData/FileSelectData.bcsv`

If you do not have this file, download a template here (link).

The first column is ModelName and should be named the name of the model. No /ObjectData/, no .arc. Just the name.
# Changing the icon's image

This is the trickiest part.

In the same file, there is a column named "play_frame". This is the frame the game will use in Character.brlan to display for the icon. Mess around with it if unsure (use whole numbers though).
## Adding new images
First, make a TPL and stick it in LayoutData/MiiIcon.arc/timg/.

Then, export anim/Character.brlan. Download BENZIN and drag the brlan onto BRLANdecompress.bat. Edit the xml in an editor (like notepad++).

Add 1 to the framesize and below the other tlps put `<timg name="[TPL NAME].tpl" />`.

Then add a new pair for each "pane".

`data1` is the frame number.

`data2` is the image number it will use. This is in hex and always has 4 digits. 

It should look like this, however the "0008"/"8.000000000000000" would be different depending on the index.

```
<pair>
	<data1>8.000000000000000</data1>
	<data2>0008</data2>
	<padding>0000</padding>
</pair>
```


Here's a full example of how a new tpl is added: (link to file)
Then save the xml and drag it onto `XMLANcompress.bat`. You will need to rename it back to Character.brlan. Then replace the file in WiiExplorer and save.
# Adding a new icon model
Copy and rename a pre-existing FileSelectDataMario to your model name of choice, preferrably following the format. This will be referred to from now on as `[ModelName]`.

Using wiiexplorer, change the root name to `[ModelName]`. The BMD's name should be the same.

In Whitehole's BCSV editor:

Archive: `/ObjectData/[ModelName].arc` File: `/[ModelName]/actorinfo/ActorAnimCtrl.bcsv`

Here you'll see the previous name of the model. Change that to `[ModelName]`.

Now time to add some particles.

In pygapa, add 4 effects. Then, copy `FileSelectDataMario::Open` to the 1st new effect, `FileSelectDataMario::Vanish` to the 2nd new effect, etc.

Once you've copied the 4 effects from `FileSelectDataMario` over, change `FileSelectDataMario` to `[ModelName]`, of course.


# The End
Congratulations on adding a new File Select Icon!

If it doesn't work, or you're confused feel free to open a discussion (link).
