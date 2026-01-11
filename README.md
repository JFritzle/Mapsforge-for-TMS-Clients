# Mapsforge-for-TMS-Clients
Graphical user interface between Mapsforge tile server and TMS client applications 

### About
Many map applications do not support local Mapsforge maps out of the box. Prebuilt Mapsforge maps are provided amongst others by [mapsforge.org](http://download.mapsforge.org) and [openandromaps.org](https://www.openandromaps.org). 

Some of these map applications however, amongst these the Java OpenStreetMap Editor JOSM, are able to handle maps provided as tiles by a [Tile Map Service](https://en.wikipedia.org/wiki/Tile_Map_Service) (TMS), which is mainly used by web mapping servers. To make local Mapsforge maps nevertheless available within these applications, a local tile server can be set up to render these Mapsforge maps and to interact with them via TMS protocol. The corresponding Mapsforge tile server is available at this [mapsforgesrv](https://github.com/telemaxx/mapsforgesrv) repository.  

### Graphical user interface
This project’s intension is to easily let the user interactively and comfortably select the numerous available options of Mapsforge tile server. In addition, option settings as well as position and font size of graphical user interface automatically get saved and restored. Mapsforge tile server gets started/restarted using these options without need to manually set up any configuration files. 

Graphical user interface is a single script written in _Tcl/Tk_ scripting language and is executable on _Microsoft Windows_ and _Linux_ operating system. Language-neutral script file _Mapsforge-for-TMS-Clients.tcl_ requires an additional user settings file and at least one localized resource file. Additional files must follow _Tcl/Tk_ syntax rules too. 

User settings file is named is named _Mapsforge-for-TMS-Clients.ini_. A template file is provided.

Resource files are named _Mapsforge-for-TMS-Clients.<locale\>_, where _<locale\>_ matches locale’s 2 lowercase letters ISO 639-1 code. English localized resource file _Mapsforge-for-TMS-Clients.en_, French localized resource file _Mapsforge-for-TMS-Clients.fr_ and German localized resource file _Mapsforge-for-TMS-Clients.de_ are provided. Script can be easily localized to any other system’s locale by providing a corresponding resource file using English resource file as a template. 

Screenshot of graphical user interface: 
![GUI_Windows](https://github.com/user-attachments/assets/0a3e4a05-bdcf-46df-ae1c-6dea582ae223)


### Installation

1.	**Java runtime environment (JRE) or Java development kit (JDK)**  
JRE version 11 or higher is required. JRE version 17 or higher is recommended.  
Each JDK contains JRE as subset.  
**Windows**: If not yet installed, download and install JRE or JDK, e.g. from [Oracle](https://www.java.com), [OpenLogic](https://www.openlogic.com/openjdk-downloads) or [Adoptium](https://adoptium.net/de/temurin/releases).  
**Linux**: If not yet installed, install JRE or JDK using Linux package manager.  
(Ubuntu: _apt install openjdk-<version\>-jre_ or _apt install openjdk-<version\>-jdk_ with required or newer _<version\>_)  
**macOS**: If not yet installed, install JDK using _Homebrew_ package manager by _brew install java_.  

2.	Mapsforge tile server  
Open [mapsforgesrv releases](https://github.com/telemaxx/mapsforgesrv/releases).  
Download most recently released jar file _mapsforgesrv-fatjar.jar_ from _<release\>\_for\_java11_tasks_ assets.  
**Windows**: Copy downloaded jar file into Mapsforge tile server’s installation folder, e.g. into folder _%ProgramFiles%/MapsforgeSrv_.  
**Linux** / **macOS**: Copy downloaded jar file into Mapsforge tile server’s installation folder, e.g. into folder _~/MapsforgeSrv_.  
**Note**: Server version 0.22.0.0 or higher is required.  

3. **Alternative Marlin rendering engine** (optional, recommended)  
[Marlin](https://github.com/bourgesl/marlin-renderer) is an open source Java2D rendering engine optimized for performance, replacing the standard built into Java. Download is available at [Marlin-renderer releases](https://github.com/bourgesl/marlin-renderer/releases).  
For JRE version lower than 17, download jar file _marlin-\*.jar_  
from _Marlin-renderer \<latest version> for JDK11+_ section's assets.  
For JRE version 17 or higher, download jar file _marlin-\*.jar_  
from _Marlin-renderer \<latest version> for JDK17+_ section's assets.  
**Windows**: Copy downloaded jar file into Mapsforge tile server’s installation folder, e.g. into folder _%ProgramFiles%/MapsforgeSrv_.  
**Linux** / **macOS**: Copy downloaded jar file into Mapsforge tile server’s installation folder, e.g. into folder _~/MapsforgeSrv_.  

4.	**Tcl/Tk scripting language version 8.6 or higher binaries**  
**Windows**: Download and install latest stable version of Tcl/Tk, currently 9.0.  
See https://wiki.tcl-lang.org/page/Binary+Distributions for available binary distributions. Recommended Windows binary distribution is from [teclab’s tcltk](https://gitlab.com/teclabat/tcltk/-/packages) Windows repository. Select most recent installation file _tcltk90-9.0.\<x.y>.Win10.nightly.\<date>.tgz_. Unpack zipped tar archive (file extension _.tgz_) into your Tcl/Tk installation folder, e.g. _%ProgramFiles%/Tcl_.  
Note: [7-Zip](https://www.7-zip.org) file archiver/extractor is able to unpack _.tgz_ archives.   
**Linux**: Install packages _tcl, tcllib, tcl-thread, tk_, _tklib_ and _x11-utils_ using Linux package manager. (Ubuntu: _apt install tcl tcllib tcl-thread tk tklib_ _x11-utils_)  
**macOS**: If not yet installed, install _tcl-tk_ using _Homebrew_ package manager by _brew install tcl-tk_. Advanced users can either download additionally required Tcl/Tk package _tklib0.9_ from [sourceforge.net](https://sourceforge.net/projects/tcllib/files/tklib/0.9) and install into folder _/usr/local/Cellar/tcl-tk/*/lib/tklib0.9_ or simply copy _tklib0.9_ folder from an existing Windows or Linux installation of Tcl/Tk.  

5.	**Mapsforge maps**  
Download Mapsforge maps for example from [openandromaps.org](https://www.openandromaps.org). Each downloaded OpenAndroMaps map archive contains a map file (file extension _.map_). Mapsforge tile server will render this map file.  

6.	**Mapsforge themes**  
Mapsforge themes _Elevate_ and _Elements_ (file extension _.xml_) suitable for OpenAndroMaps are available for download at [openandromaps.org](https://www.openandromaps.org).  
**Note**:  
In order "Hillshading on map" to be applied to rendered map tiles, hillshading has to be enabled in theme file too. _Elevate_ and _Elements_ themes version 5 or higher do enable hillshading.  

7. **DEM data** (optional, required for hillshading)  
Download and store DEM (Digital Elevation Model) data for the regions to be rendered.  
**Notes**:  
Either HGT files or ZIP archives containing 1 single equally named HGT file may be supplied.  
Example: ZIP archive N49E008.zip containing 1 single HGT file N49E008.hgt.  
While 1\" (arc second) resolution DEM data have a significantly higher accuracy than 3\" resolution, hillshading assumes significantly much more time. Therefore 3\" resolution usually is better choice.  
    
   \- HGT files with 3\" resolution SRTM (Shuttle Radar Topography Mission) data are available for whole world at [viewfinderpanoramas.org](http://www.viewfinderpanoramas.org/Coverage%20map%20viewfinderpanoramas_org3.htm). Unzip downloaded ZIP files to DEM folder.  
\- HGT files with 1\" resolution DEM data are available for selected regions at [viewfinderpanoramas.org](http://www.viewfinderpanoramas.org/Coverage%20map%20viewfinderpanoramas_org1.htm). Unzip downloaded ZIP files to DEM folder.  
\- ZIP archives with 3\" and 1\" resolution compiled and resampled by Sonny are available for selected regions at [Sonny's Digital LiDAR Terrain Models of European Countries](https://sonny.4lima.de). LiDAR data where available are more precise than SRTM data. Store downloaded ZIP files to DEM folder.  

8.	**Mapsforge for TMS Clients graphical user interface script**  
Download language-neutral script file _Mapsforge-for-TMS-Clients.tcl_, user settings file _Mapsforge-for-TMS-Clients.ini_ and at least one localized resource file.  
**Windows**: Copy downloaded files into Mapsforge tile server’s installation folder, e.g. into folder _%ProgramFiles%/MapsforgeSrv_.  
**Linux** / **macOS**: Copy downloaded files into Mapsforge tile server’s installation folder, e.g. into folder _~/MapsforgeSrv_.  
**Note**: Edit _user-defined script variables settings section_ of user settings file _Mapsforge-for-TMS-Clients.ini_ to match files and folders of your local installation of Java and Mapsforge tile server. Always use character slash “/” as directory separator in _Mapsforge-for-TMS-Clients.ini_ file, for Microsoft Windows too!

### Script file execution

**Windows**:  
Associate file extension _.tcl_ to Tcl/Tk window shell’s binary _wish.exe_. Right-click script file and open file’s properties window. Change data type _.tcl_ to be opened by _Wish application_ e.g. by executable _%ProgramFiles%/Tcl/bin/wish.exe_. Once file extension has been associated, double-click script file to run.  

**Linux**:  
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

**macOS**:  
Either run script file from command line by
```
wish <path-to-script>/Mapsforge-for-TMS-Clients.tcl
```

or use _Automator -> Application -> Run Shell Script -> /usr/local/bin/wish \"$@\"_ to create an application for Tcl/Tk window shell’s binary _wish_, then associate all _.tcl_ files to this application and run script file by double-click file in file manager.

Having _.tcl_ files associated to this application, a desktop starter from script file can be created by _Make Alias_ and dragging the alias and dropping it to desktop.  

### Usage

* After selecting task(s), map(s), theme file, theme style, style's overlays etc. in graphical user interface, hit _Start_ button to start Mapsforge tile server. When changing settings while client application is running, a reload of tile server is required to adopt new settings. To reload server, hit _Start_ button again. If client application was caching tiles already loaded with previous settings, it is necessary to force application to clear/flush application's tile cache or to clear tile cache manually and/or to reload tiles.
* Closing graphical user interface also closes Mapsforge tile server. Client application will however keep running but will no longer receive any tiles.
* Use keyboard keys Ctrl-plus to increase and keyboard keys Ctrl-minus to decrease font size of graphical user interface and/or output console.
* See output console for Mapsforge tile server’s output.

### URLs for tile requests


URLs to request map tiles and/or hillshading overlay tiles from server:  
```
scheme://address:port/zoom/x/y.format?task=Map
scheme://address:port/zoom/x/y.format?task=Hillshading  
```

| URL item | description |
| -----| ----------- |
| scheme | protocol either *http* or *https* |
| address | Mapsforge tile server's IP address |
| mport | tcp port to request map tiles |
| hport | tcp port to request hillshading overlay tiles |
| port | tcp port to request map and hillshading overlay tiles |
| zoom | zoom level of requested tile |
| x | tile number in x direction (longitude) |
| y | tile number in y direction (latitude) |
| format | tile image format *png*, *jpg*, *tif*, *bmp*, ... |

URL examples:
```
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

![Heidelberg](https://github.com/user-attachments/assets/4ecda2b6-5adf-4019-973a-6ca96c2d7f35)

Mapsforge Tile Server and Mapsforge Hillshading Server have been defined in JOSM preferences as shown below:

![Config](https://github.com/user-attachments/assets/7a6d534b-fa91-4667-8109-bb8795d02ffc)

### Hints

* Output console  
While console output of Mapsforge tile server can be informative and helpful to verify what is happening as well as to analyze errors, writing to console costs some performance. Therefore the console should be hidden if not needed. 
* Built-in world map  
Since the built-in [Mapsforge world map](https://download.mapsforge.org/maps/world/world.map) only shows the coastline, it only serves as a rough overview. Due to map's low resolution, coastlines show inaccurate at high resolution.  
In order not to cover an accurate map, the built-in world map has been automatically deactivated at higher zoom levels.    
Starting with server version 0.23.0.3, built-in world map is rendered with lower priority than user-defined accurate maps. Zoom level restriction was therefore removed. 
* Hillshading  
  * When selecting "Hillshading on map", map and hillshading are rendered  into one single map.  
  * When selecting "Hillshading as map", map and hillshading are rendered as two separate maps. Post-processing hillshading, gray value of flat area gets mapped to full transparency. Thus the flatter the area, the more the original colors of the map shine through. Finally, hillshading can be used as an alpha-transparent overlay for any map.  
[OpenTopoMap](https://opentopomap.org) uses same hillshading technique as hillshading algorithm "diffuselight".  

 




