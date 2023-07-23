# Mapsforge-for-TMS-Clients
Graphical user interface between Mapsforge tile server and TMS client applications 

### Preliminary
Many map applications do not support local Mapsforge maps out of the box. Prebuilt Mapsforge maps are provided amongst others by [mapsforge.org](http://download.mapsforge.org) and [openandromaps.org](https://www.openandromaps.org). 

Some of these map applications however, amongst these the Java OpenStreetMap Editor JOSM, are able to handle maps provided as tiles by a [Tile Map Service](https://en.wikipedia.org/wiki/Tile_Map_Service) (TMS), which is mainly used by web mapping servers. To make local Mapsforge maps nevertheless available within these applications, a local tile server can be set up to render these Mapsforge maps and to interact with them via TMS protocol. The corresponding tile server is available at this [mapsforgesrv](https://github.com/telemaxx/mapsforgesrv) repository.  

### Graphical user interface
This project’s intension is to easily let the user interactively and comfortably select the numerous available options of tile server. In addition, option settings as well as position and font size of graphical user interface automatically get saved and restored. Tile server gets started/restarted using these options without need to manually set up any configuration files. 

Graphical user interface is a single script written in _Tcl/Tk_ scripting language and is executable on _Microsoft Windows_ and _Linux_ operating system. Language-neutral script file _Mapsforge-for-TMS-Clients.tcl_ an additional user settings file and at least one localized resource file. Additional files must follow _Tcl/Tk_ syntax rules too. 

User settings file is named is named _Mapsforge-for-TMS-Clients.ini_. A template file is provided.

Resource files are named _Mapsforge-for-TMS-Clients.<locale\>_, where _<locale\>_ matches locale’s 2 lowercase letters ISO 639-1 code. English localized resource file _Mapsforge-for-TMS-Clients.en_ and German localized resource file _Mapsforge-for-TMS-Clients.de_ are provided. Script can be easily localized to any other system’s locale by providing a corresponding resource file using English resource file as a template. 

Screenshot of graphical user interface: 
![GUI](https://user-images.githubusercontent.com/62614244/174278344-c261c9ca-dad8-430e-a4f4-c1fff0785e3b.png)

### Installation

1.	Java runtime environment version 8 or higher   
Windows: If not yet installed, download and install Java, e.g. from [Oracle](https://www.java.com).  
Linux: If not yet installed, install Java runtime package using Linux package manager. (Ubuntu: _apt install openjdk-<version\>-jre_ where _<version\>_ is 8 or higher)

2.	Mapsforge tile server  
Open [mapsforgesrv](https://github.com/telemaxx/mapsforgesrv) repository.  
For Java version 11 or higher, switch branch to _master_, navigate to folder _mapsforgesrv/bin/jars_ready2use_ and download jar file [_mapsforgesrv-fatjar.jar_](https://github.com/telemaxx/mapsforgesrv/raw/master/mapsforgesrv/bin/jars_ready2use/mapsforgesrv-fatjar.jar).  
For Java version 8 (or higher), switch branch to _Java8_, navigate to folder _mapsforgesrv/bin/jars_ready2use_ and download jar file [_mapsforgesrv4java8.jar_](https://github.com/telemaxx/mapsforgesrv/raw/Java8/mapsforgesrv/bin/jars_ready2use/mapsforgesrv4java8.jar).  
Windows: Copy downloaded jar file into Mapsforge tile server’s installation folder, e.g. into folder _%programfiles%/MapsforgeSrv_.  
Linux: Copy downloaded jar file into Mapsforge tile server’s installation folder, e.g. into folder _~/MapsforgeSrv_.  
Note:  
Currently Mapsforge tile server version 0.17.4 or higher is required. Previous server versions are no longer supported.  

3. Alternative Marlin rendering engine (optional, recommended)  
[Marlin](https://github.com/bourgesl/marlin-renderer) is an open source Java2D rendering engine optimized for performance, replacing the standard built into Java. Download is available at [Marlin-renderer releases](https://github.com/bourgesl/marlin-renderer/releases).  
For Java version 11 or higher, download jar file _marlin-\*.jar_ from latest _Marlin-renderer \<latest version> for JDK11+_ section's assets.  
For Java version 8, download both jar files _marlin-\*.jar_ from latest _Marlin-renderer \<latest version> for JDK8_ section's assets.  
Windows: Copy downloaded jar file(s) into Mapsforge tile server’s installation folder, e.g. into folder _%programfiles%/MapsforgeSrv_.  
Linux: Copy downloaded jar file(s) into Mapsforge tile server’s installation folder, e.g. into folder _~/MapsforgeSrv_.  

4.	Tcl/Tk scripting language version 8.6 or higher binaries  
Windows: Download and install latest stable version of Tcl/Tk. See https://wiki.tcl-lang.org/page/Binary+Distributions for available binary distributions. Recommended distribution is [teclab’s tcltk](https://github.com/teclab-at/tcltk/releases) repository. First select most recent installation file _tcltk86-8.6.x.y.tcl86.Win10.x86_64.tgz_, then press _Download_ button. Unpack zipped tar archive (file extension _.tgz_) into your Tcl/Tk installation folder, e.g. _%programfiles%/Tcl_.  
Note 1: [7-Zip](https://www.7-zip.org) file archiver/extractor is able to unpack _.tgz_ archives.   
Note 2: Archives of latest releases for Windows at teclab’s tcltk repository may have file extension _.zip_ while they should have extension _.tgz_. Rename extension to _.tgz_ before unpacking archive.  
Linux: Install packages _tcl, tcllib, tk_ and _tklib_ using Linux package manager. Package _tklib_ is required for tooltips. (Ubuntu: _apt install tcl tcllib tk tklib_)

5.	Mapsforge maps  
Download Mapsforge maps for example from [openandromaps.org](https://www.openandromaps.org). Each downloaded OpenAndroMaps map archive contains a map file (file extension _.map_). Tile server will render this map file.  

6.	Mapsforge themes  
Mapsforge themes _Elevate_ and _Elements_ (file extension _.xml_) suitable for OpenAndroMaps are available for download at [openandromaps.org](https://www.openandromaps.org).  
Note:  
In order "Hillshading on map" to be applied to rendered map tiles, hillshading has to be enabled in theme file too. _Elevate_ and _Elements_ themes version 5 or higher do enable hillshading.

7. DEM data (optional, required for hillshading)  
Download and store DEM (Digital Elevation Model) data for the regions to be rendered.
Notes:  
Either HGT files or ZIP archives containing 1 equally named HGT file may be supplied.  
Example: ZIP archive N49E008.zip containing 1 single HGT file N49E008.hgt.  
While 1\" (arc second) resolution DEM data have a significantly higher accuracy than 3\" resolution, hillshading assumes significantly much more time. Therefore 3\" resolution usually is better choice.  
    
   \- HGT files with 3\" resolution SRTM (Shuttle Radar Topography Mission) data are available for whole world at [viewfinderpanoramas.org](http://www.viewfinderpanoramas.org/Coverage%20map%20viewfinderpanoramas_org3.htm). Unzip downloaded ZIP files to DEM folder.  
\- HGT files with 1\" resolution DEM data are available for selected regions at [viewfinderpanoramas.org](http://www.viewfinderpanoramas.org/Coverage%20map%20viewfinderpanoramas_org1.htm). Unzip downloaded ZIP files to DEM folder.  
\- ZIP archives with 3\" and 1\" resolution compiled and resampled by Sonny are available for selected regions at [Sonny's Digital LiDAR Terrain Models of European Countries](https://sonny.4lima.de). LiDAR data where available are more precise than SRTM data. Store downloaded ZIP files to DEM folder.

8.	Mapsforge for TMS Clients graphical user interface script  
Download language-neutral script file _Mapsforge-for-TMS-Clients.tcl_, user settings file _Mapsforge-for-TMS-Clients.ini_ and at least one localized resource file.  
Windows: Copy downloaded files into Mapsforge tile server’s installation folder, e.g. into folder _%programfiles%/MapsforgeSrv_.  
Linux: Copy downloaded files into Mapsforge tile server’s installation folder, e.g. into folder _~/MapsforgeSrv_.  
Edit _user-defined script variables settings section_ of user settings file _Mapsforge-for-TMS-Clients.ini_ to match files and folders of your local installation of Java and Mapsforge tile server.  
Important:  
Always use character slash “/” as directory separator in script, for Microsoft Windows too!

### Script file execution

Windows:  
Associate file extension _.tcl_ to Tcl/Tk window shell’s binary _wish.exe_. Right-click script file and open file’s properties window. Change data type _.tcl_ to be opened by _Wish application_ e.g. by executable _%programfiles%/Tcl/bin/wish.exe_. Once file extension has been associated, double-click script file to run.

Linux:  
Either run script file from command line by
```
wish <path-to-script>/Mapsforge-for-TMS-Clients.tcl
```
or create a desktop starter file _Mapsforge-for-TMS-Clients.desktop_
```
[Desktop Entry]
Version=1.0
Type=Application
Terminal=false
Name=Mapsforge-for-TMS-Clients
Exec=wish <path-to-script>/Mapsforge-for-TMS-Clients.tcl
```
or associate file extension _.tcl_ to Tcl/Tk window shell’s binary _/usr/bin/wish_ and run script file by double-click file in file manager.

### Usage

* After selecting map(s), theme file, theme style, style's overlays etc. in graphical user interface, hit _Start_ button to start tile server. If changing settings while client application is running, a restart of tile server is required to adopt new settings. To restart server, hit _Start_ button again. If client application was caching tiles already loaded with previous settings, it is necessary to force application to clear/flush application's tile cache or to clear tile cache manually and/or to reload tiles.
* Closing graphical user interface also closes tile server. Client application will however keep running but will no longer receive any tiles.
* Use keyboard keys Ctrl-plus to increase and keyboard keys Ctrl-minus to decrease font size of graphical user interface and/or output console.
* See output console for tile server’s output.

### Example

Screenshot of Java OpenStreetMap Editor JOSM showing Heidelberg (Germany) old town and castle using
* OpenAndroMaps map file _Germany_oam.osm.map_
* OpenAndroMaps rendering theme _Elevate_
* Theme file's style _elv-city_ aka _City_
* Style's default overlays
* Hillshading settings as above

for _Imagery_ and _Mini map_:

![Heidelberg](https://user-images.githubusercontent.com/62614244/174278461-7983a101-0aa7-47c5-86b7-4d6f235750c3.jpg)

Mapsforge Tile Server and Hillshading Server have been defined in JOSM preferences as shown below:

![Config](https://user-images.githubusercontent.com/62614244/174278474-2f76c5c2-5295-4088-b038-83730e566432.png)

### Hints

* Output console  
While console output of tile server can be informative and helpful to verify what is happening as well as to analyze errors, writing to console costs some performance. Therefore the console should be hidden if not needed. 
* Built-in world map  
Since the built-in [Mapsforge world map](https://download.mapsforge.org/maps/world/world.map) only shows the coastline, it only serves as a rough overview. Due to map's low resolution, coastlines show inaccurate at high resolution. Because the Mapsforge renderer prefers land on the world map to sea on the selected detailed local map, it may be advisable to disable the built-in world map when rendering coastal regions at high resolution.
* Hillshading  
  * When selecting "Hillshading on map", map and hillshading are rendered into one single map. Flat area gets a medium shade of gray, while slopes get a darker or a brighter shade of gray depending on the angle of incidence of light. Thus map has a shade of gray everywhere.  
  
  * When selecting "Hillshading as map", map and hillshading are rendered as two separate maps. Post-processing hillshading, gray value of flat area gets mapped to full transparency, darker gray values get mapped to transparency levels of black, brighter gray values get mapped to transparency levels of white. Thus the flatter the area, the more the original colors of the map shine through. Finally, hillshading can be used as an alpha-transparent overlay for any map.  
[OpenTopoMap](https://opentopomap.org) uses this same hillshading technique.  

 




