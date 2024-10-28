# Mapsforge-for-TMS-Clients
Graphical user interface between Mapsforge tile server and TMS client applications 

### Preliminary
Many map applications do not support local Mapsforge maps out of the box. Prebuilt Mapsforge maps are provided amongst others by [mapsforge.org](http://download.mapsforge.org) and [openandromaps.org](https://www.openandromaps.org). 

Some of these map applications however, amongst these the Java OpenStreetMap Editor JOSM, are able to handle maps provided as tiles by a [Tile Map Service](https://en.wikipedia.org/wiki/Tile_Map_Service) (TMS), which is mainly used by web mapping servers. To make local Mapsforge maps nevertheless available within these applications, a local tile server can be set up to render these Mapsforge maps and to interact with them via TMS protocol. The corresponding tile server is available at this [mapsforgesrv](https://github.com/telemaxx/mapsforgesrv) repository.  

While old tile server type is capable of rendering only one single set of parameters at a time, the new so-called *tasks* server type is capable of rendering multiple sets of parameters concurrently. Thus, a single *tasks* server instance can replace multiple old server instances.  

### Graphical user interface
This project’s intension is to easily let the user interactively and comfortably select the numerous available options of tile server. In addition, option settings as well as position and font size of graphical user interface automatically get saved and restored. Tile server gets started/restarted using these options without need to manually set up any configuration files. 

Graphical user interface is a single script written in _Tcl/Tk_ scripting language and is executable on _Microsoft Windows_ and _Linux_ operating system. Language-neutral script file _Mapsforge-for-TMS-Clients.tcl_ an additional user settings file and at least one localized resource file. Additional files must follow _Tcl/Tk_ syntax rules too. 

User settings file is named is named _Mapsforge-for-TMS-Clients.ini_. A template file is provided.

Resource files are named _Mapsforge-for-TMS-Clients.<locale\>_, where _<locale\>_ matches locale’s 2 lowercase letters ISO 639-1 code. English localized resource file _Mapsforge-for-TMS-Clients.en_ and German localized resource file _Mapsforge-for-TMS-Clients.de_ are provided. Script can be easily localized to any other system’s locale by providing a corresponding resource file using English resource file as a template. 

Screenshot of graphical user interface: 
![GUI](https://github.com/JFritzle/Mapsforge-for-TMS-Clients/assets/62614244/ed3901a4-58e0-48f1-88cc-c83eda1f87af)

### Installation

1.	Java runtime environment (JRE) or Java development kit (JDK)   
Note: While old server type versions exist for JRE version 8 or higher, new *tasks* server type versions require JRE version 11 or higher. Each JDK contains JRE as subset.  
Windows: If not yet installed, download and install JRE or JDK, e.g. from [Oracle](https://www.java.com) or [Adoptium](https://adoptium.net/de/temurin/releases).  
Linux: If not yet installed, install JRE or JDK using Linux package manager. (Ubuntu: _apt install openjdk-<version\>-jre_ or _apt install openjdk-<version\>-jdk_ with required or newer _<version\>_)

2.	Mapsforge tile server  
Open [mapsforgesrv releases](https://github.com/telemaxx/mapsforgesrv/releases).  
For old server type and JRE version 11 or higher, download most recently released jar file _mapsforgesrv-fatjar.jar_ from   _<release\>\_for\_java11_ assets.  
For old server type and JRE version 8 (or higher), download most recently released jar file _mapsforgesrv4java8.jar_ from _<release\>\_for\_java8_ assets.  
For new *tasks* server type and JRE version 11 or higher, download most recently released jar file _mapsforgesrv-fatjar.jar_ from _<release\>\_for\_java11_tasks_ assets.  
Windows: Copy downloaded jar file into Mapsforge tile server’s installation folder, e.g. into folder _%programfiles%/MapsforgeSrv_.  
Linux: Copy downloaded jar file into Mapsforge tile server’s installation folder, e.g. into folder _~/MapsforgeSrv_.  
Note:  
Currently Mapsforge tile server old server type and new *tasks* server type with server version 0.17.4 or higher is required. Previous server versions are no longer supported.  

3. Alternative Marlin rendering engine (optional, recommended)  
[Marlin](https://github.com/bourgesl/marlin-renderer) is an open source Java2D rendering engine optimized for performance, replacing the standard built into Java. Download is available at [Marlin-renderer releases](https://github.com/bourgesl/marlin-renderer/releases).  
For JRE version 11 or higher, download jar file _marlin-\*.jar_ from latest _Marlin-renderer \<latest version> for JDK11+_ section's assets.  
For JRE version 8, download both jar files _marlin-\*.jar_ from latest _Marlin-renderer \<latest version> for JDK8_ section's assets.  
Windows: Copy downloaded jar file(s) into Mapsforge tile server’s installation folder, e.g. into folder _%programfiles%/MapsforgeSrv_.  
Linux: Copy downloaded jar file(s) into Mapsforge tile server’s installation folder, e.g. into folder _~/MapsforgeSrv_.  

4.	Tcl/Tk scripting language version 8.6 or higher binaries  
Windows: Download and install latest stable version of Tcl/Tk, currently 8.6.16. See https://wiki.tcl-lang.org/page/Binary+Distributions for available binary distributions. Recommended Windows binary distribution is from [teclab’s tcltk](https://gitlab.com/teclabat/tcltk/-/packages) Windows repository. Select most recent installation file _tcltk86-8.6.16.\<number>.Win10.nightly.\<date>.tgz_. Unpack zipped tar archive (file extension _.tgz_) into your Tcl/Tk installation folder, e.g. _%programfiles%/Tcl_.  
Note: [7-Zip](https://www.7-zip.org) file archiver/extractor is able to unpack _.tgz_ archives.  
Linux: Install packages _tcl, tcllib, tcl-thread, tk_ and _tklib_ using Linux package manager. Since Tcl script now uses threads, package _tcl-thread_ is required. In addition, package _tklib_ is required for using tooltips.  (Ubuntu: _apt install tcl tcllib tcl-thread tk tklib_)

5.	Mapsforge maps  
Download Mapsforge maps for example from [openandromaps.org](https://www.openandromaps.org). Each downloaded OpenAndroMaps map archive contains a map file (file extension _.map_). Tile server will render this map file.  

6.	Mapsforge themes  
Mapsforge themes _Elevate_ and _Elements_ (file extension _.xml_) suitable for OpenAndroMaps are available for download at [openandromaps.org](https://www.openandromaps.org).  
Note:  
In order "Hillshading on map" to be applied to rendered map tiles, hillshading has to be enabled in theme file too. _Elevate_ and _Elements_ themes version 5 or higher do enable hillshading.

7. DEM data (optional, required for hillshading)  
Download and store DEM (Digital Elevation Model) data for the regions to be rendered.
Notes:  
Either HGT files or ZIP archives containing 1 single equally named HGT file may be supplied.  
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

### URLs for tile requests

The URLs that the TMS client should use to request a tile from the tile server depends on whether the old server type or the new *tasks* server type is used.

URLs to request map tiles and/or hillshading overlay tiles for old server type:  
```
scheme://address:mport/zoom/x/y.format
scheme://address:hport/zoom/x/y.format   

```

URLs to request map tiles and/or hillshading overlay tiles for new *tasks* server type:  
```
scheme://address:port/zoom/x/y.format?task=Map
scheme://address:port/zoom/x/y.format?task=Hillshading  

```

| URL item | description |
| -----| ----------- |
| scheme | protocol either *http* or *https* |
| address | tile server's IP address |
| mport | tcp port to request map tiles |
| hport | tcp port to request hillshading overlay tiles |
| port | tcp port to request map and hillshading overlay tiles |
| zoom | zoom level of requested tile |
| x | tile number in x direction (longitude) |
| y | tile number in y direction (latitude) |
| format | tile image format *png*, *jpg*, *tif*, *bmp*, ... |

URL examples:
```
http://127.0.0.1:60815/14/8584/5595.png
http://127.0.0.1:60816/14/8584/5595.png

http://127.0.0.1:60815/14/8584/5595.png?task=Map
http://127.0.0.1:60815/14/8584/5595.png?task=Hillshading  

```

See [Slippy map tilenames](https://wiki.openstreetmap.org/wiki/Slippy_map_tilenames) for tile naming conventions.

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
Since the built-in [Mapsforge world map](https://download.mapsforge.org/maps/world/world.map) only shows the coastline, it only serves as a rough overview. Due to map's low resolution, coastlines show inaccurate at high resolution. Because the Mapsforge renderer prefers land on the world map to sea on the selected detailed local map, it may be advisable to disable the built-in world map when rendering coastal regions at high resolution. In order not to cover an accurate map, the built-in world map has been automatically deactivated at higher zoom levels since tile server version 0.21.3.
* Hillshading  
  * When selecting "Hillshading on map", map and hillshading are rendered into one single map. Flat area gets a medium shade of gray, while slopes get a darker or a brighter shade of gray depending on the angle of incidence of light. Thus map has a shade of gray everywhere.  
  
  * When selecting "Hillshading as map", map and hillshading are rendered as two separate maps. Post-processing hillshading, gray value of flat area gets mapped to full transparency, darker gray values get mapped to transparency levels of black, brighter gray values get mapped to transparency levels of white. Thus the flatter the area, the more the original colors of the map shine through. Finally, hillshading can be used as an alpha-transparent overlay for any map.  
[OpenTopoMap](https://opentopomap.org) uses this same hillshading technique.  

 




