<!---
The page title should not go in the menu
-->
<p class="page-title"> Batch scripts </p>

Batch scripts are used to automatically execute a series of IGV commands.


## How to run a batch script

Select _**Tools > Run Batch Script**_ to load a text file that contains a series of commands for IGV to execute. 

## Example script

The following example script loads a BAM file and takes a series of snapshots at different loci. The snapshot images are saved in the specified directory.

```
new  
genome hg18  
snapshotDirectory mySnapshotDirectory 
load myfile.bam 
goto chr1:65,289,335-65,309,335  
sort position  
collapse  
snapshot  
goto chr1:113,144,120-113,164,120  
sort base  
collapse  
snapshot  
goto chr4:68,457,006-68,467,006  
sort strand  
collapse  
snapshot
```


## Script commands

The batch script file is a plain text file with one command per line. 
Arguments are delimited by spaces (**NOT tabs**). 
Lines beginning with ```#``` or ```//``` are skipped.  See the table below for a complete list of supported commands.

Command    | Parameters                   | Description
------- |------------------------------| ----------
collapse | trackName                    |    Collapses a given track. trackName is optional, if it is not supplied all tracks are collapsed.
colorBy | option tagName               | Sets the "color by" option for alignment tracks. For option "TAG" also specify the tag name. See [below](./#colorby-option-values) for a list of valid options.
echo    | param                        | Writes the value of "param" back to the response, or if param is not specified "echo".
exit    |                              | Exit (close) the IGV application.
expand | trackName                    |    Expands a given trackName. trackName is optional, however, and if it is not supplied all tracks are expanded.
genome | genomeIdOrPath               |    Selects a genome by id, or loads a genome (or indexed fasta) from the supplied path.
goto | locus or listOfLoci          |	| Scrolls to a single locus or a space-delimited list of loci. If a list is provided, these loci will be displayed in a split screen view.  Use any syntax that is valid in the IGV search box.  
group | option tagNameOrPosition     |    Alignment tracks only. Group alignments by the specified option. See [below](./#group-option-values) for a list of valid option values. For option "TAG" also specify the tag name.
load | file                         |    Loads a data or session file by specifying a full path to a local file or a URL. To explicitly specify a path to an index file use the optional "index=" parameter. For examples ```load foo.bam index=bar.bai```
maxPanelHeight | height                       |    Sets the number of vertical pixels (height) of each panel to include in image. Images created from a port command or batch script are not limited to the data visible on the screen. Stated another way, images can include the entire panel not just the portion visible in the scrollable screen area. The default value for this setting is 1000, increase it to see more data, decrease it to create smaller images. To capture the exact area visible on the screen set this value to -1.
new |                              |    Create a new session. Unloads all tracks except the default genome annotations.
overlay | overlaidTrackName trackNames | Overlay a list of tracks.  ```trackNames``` is a space separated list. Spaces in track names must be replaced with %20.    |
preference| key value                    |    Temporarily set the preference named key to the specified value. This preference only lasts until IGV is shut down. The complete set of preference keys are listed in the file "preferences.tab" [here](https://raw.githubusercontent.com/igvteam/igv/master/src/main/resources/org/broad/igv/prefs/preferences.tab). The first column is the key, the third column is the value type. For ```select``` value types the permitted values follow as a list delimited by the character "\|".
region | chr start end                | Defines a region of interest bounded by the two loci (e.g., region chr1 100 200).
saveSession  | filename                     | Save the current session. It is recommended that a full path be used for filename.  |
scrollToTop |                        | Scroll all panels to the top of the view.  This is useful after loading a large number of tracks, which tracks loaded first scrolled out of view.  |
separate | overlaidTrackName            | Separate an overlaid track into its constituitive tracks. This undos ```overlay```.   |
setAltColor | colorString trackName        | Set the track "altColor", used for negative values in a wig track or negative strand features. See description of setColor below.  |
setColor | colorString trackName        | Set the track color. colorString can be a comma delimited rgb string with components in the range 0-255, for example ```255,0,0```, or a hex color string, for example ```FF0000```. 
setDataRange | rangeString trackName        | Set the data range (scale) for all numeric tracks, or if a trackName is specified a specific track. rangeString is either a 2 comma element delimited list for min,max. As of IGV 2.11.0, 'auto' can be used for rangeString, which will set the track(s) to autoscale.
setLogScale  | true/false trackName         | Set the data scale to log (true) or linear (false). Optionally specify a track, if no track is specified all numeric tracks will be set.
setSequenceStrand | + / -                        | Set the sequence strand to positive (+) or negative (-). Note this does not reverse the direction left-right. |
setSequenceShowTranslation | true / false                 | Show or hide the 3-frame translation rows of the sequence track. |
setSleepInterval| ms                           |    Sets a delay (sleep) time in milliseconds. The sleep interval is invoked between successive commands.
setTrackHeight | height trackName             | Set the specified track's height in integer units. trackName is required.
snapshotDirectory | path                         | Sets the directory in which to write images.
snapshot | filename                     | Saves a snapshot of the IGV window to an image file. If filename is omitted, writes a PNG file with a filename generated based on the locus. If filename is specified, the filename extension determines the image file format, which must be either .png or .svg.
sort | option locus direction       | Sorts alignment or segmented copy number tracks. See [below](./#sort-option-values) for valid option values. If supplied, the locus option can define a single position for alignments, or a range for copy number. If absent sorting will be based on the center position of the region in view for alignment tracks, or the average over the entire region in view for segmented copy number. If ```direction``` is specified and equal to ```reverse``` sort order is reversed. Locus must be specified if ```direction``` is specified.
squish | trackName                    |    Squish a given trackName. trackName is optional, and if it is not supplied all annotation tracks are squished.
viewaspairs | trackName                    |    Set the display mode for an alignment track to "View as pairs". trackName is optional.
setAccessToken | token host                   | Set an access token to be used in an ```Authorization: bearer" header for all requests to host.  If host is omitted token is used for all requests. 
clearAccessTokens |                              | Clears all access tokens.  

### ColorBy option values

* BISULFITE
* FIRST_OF_PAIR_STRAND
* INSERT_SIZE
* LIBRARY
* LINK_STRAND
* MAPPED_SIZE
* MOVIE
* NOMESEQ
* NONE
* PAIR_ORIENTATION
* READ_GROUP
* READ_STRAND
* SAMPLE
* TAG
* UNEXPECTED_PAIR
* YC_TAG
* ZMW

### Group option values

* ALIGNED_READ_LENGTH
* BASE locus  -- where locus is of the form chr:position
* INSERTION locus   
* FIRST_OF_PAIR_STRAND
* HAPLOTYPE
* LIBRARY
* MATE_CHROMOSOME
* MOVIE
* NONE
* PAIR_ORIENTATION
* PHASE
* READ_GROUP
* READ_ORDER
* REFERENCE_CONCORDANCE
* SAMPLE
* STRAND
* SUPPLEMENTARY
* TAG tag_name
* ZMW

### Sort option values

#### Segmented copy number

* AMPLIFICATION
* DELETION

#### Alignments

* BASE
* FIRSTOFPAIRSTRAND
* INSERSTSIZE
* MATECHR
* POSITION
* QUALITY
* READGROUP
* READORDER
* READNAME
* SAMPLE
* STRAND
* ALIGNEDREADLENGTH
