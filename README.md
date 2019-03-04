# Huawei TCX Converter
A makeshift python tool that generates TCX files from Huawei HiTrack files.

Users of Huawei Watches/Bands sync this data with the Huawei Health App. It is notoriously difficult to get the data out of this app, but through some cunning you can find `HiTrack` files which seem to contain some run data. This program allows you to take these files and generate `.TCX` files for use in your tracking app of choice (i.e. Strava).

## How to get the HiTrack Files - Android only

If you have a **rooted** phone you can simply navigate to: `data/data/com.huawei.health/files/` where you should find a number of files prefixed `HiTrack`.

If you have an **unrooted** phone then:
- Download the [Huawei Backup App](https://play.google.com/store/apps/details?id=com.huawei.KoBackup&hl=en_GB) onto your phone.
- Start a new **unencrypted** backup of the Huawei Health app data to your external storage (SD Card)
- Navigate to `Huawei/Backup/***/backupFiles/***/` and copy `com.huawei.health.tar` to your computer.
- Unzip the file and navigate to `com.huawei.health/files/` and you should should see a number of `HiTrack` files.

## How to use the Huawei TCX Converter
You need [`python 3`](https://www.python.org/downloads/) to use this tool. If you have [xmlschema](https://pypi.org/project/xmlschema/) then the tool will be able to validate the final TCX file in order to check that the conversion has worked.

The tool is run on the command line by passing it the name of your file as a command line argument. Please **do not rename your HiTrack files** as this tool extracts the start and end time of your exercise from it! For example you could copy the tool to the directory containing your HiTrack file and run:

    python Huawei_TCX_Converter.py HiTrack_1550862681000155086673800030001

This gave me the output:

    ---- Information extracted from filename ----
    start: 2019-02-22T19:11:21.000Z
    end: 2019-02-22T20:18:58.000Z
    duration: 01:07:37
    ---- Information extracted from file ----
    location data points: 1911
    distance (approx): 9815 m
    ---- XML file ----
    generating: OKAY
    saving: OKAY
    validating: OKAY
    
## Contributing
This is a very early alpha version of this tool, so please help me by making it better! I'll accept any improvements, but if you're looking for inspiration you could start with this to-do list
* Check that this works for files other than those generated using the Huawei Band 2 Pro
* Improve the distance measurement method (currently using [Viscenty's Formulae](https://en.wikipedia.org/wiki/Vincenty%27s_formulae))
* Try and work out what `tp=b-p-m` is
* Add interpolated heart-rate/pace/average speed data to each location element
* Look into files from different sports, and enable changing sports type in resulant TCX
* Work on splitting data into `Laps`/`Tracks` rather than shoving it all into one
* See if you really need to add the unused data elements (e.g. Calories) to the TCX
* Try to call on an open API to get altitude data for location points that don't have it
* Inspect other files in `com.huawei.health` to see if we can get any more relevant data out of them
