# Mapsforge-for-MyTourbook
Graphical user interface between Mapsforge tile server and MyTourbook

### About
MyTourbook supports offline Mapsforge maps as _2.5D Tour Maps_ out of the box using VTM (Vector Tile Map) renderer. Prebuilt Mapsforge maps are provided amongst others by [mapsforge.org](http://download.mapsforge.org) and [openandromaps.org](https://www.openandromaps.org).

MyTourbook however is also able to handle _2D Tour Maps_ provided as raster tiles by a Tile Map Service (TMS), which is mainly used by web mapping servers. To make local Mapsforge maps nevertheless available as _2D Tour Maps_ within MyTourbook, a local tile server can be set up to render these Mapsforge maps and to interact with MyTourbook via TMS protocol. The corresponding tile server is available at this [mapsforgesrv](https://github.com/telemaxx/mapsforgesrv) repository.


### Graphical user interface
This project’s intension is to easily let the user interactively and comfortably select the numerous available options of tile server. In addition, option settings as well as position and font size of graphical user interface automatically get saved and restored. Tile server and MyTourbook get started/restarted using these options without need to manually set up any configuration files. 

Graphical user interface is a single script written in _Tcl/Tk_ scripting language and is executable on _Microsoft Windows_ and _Linux_ operating system. Language-neutral script file _Mapsforge-for-MyTourbook.tcl_ requires an additional user settings file and at least one localized resource file. Additional files must follow _Tcl/Tk_ syntax rules too.

User settings file is named _Mapsforge-for-MyTourbook.ini_. A template file is provided.

Resource files are named _Mapsforge-for-MyTourbook.<locale\>_, where _<locale\>_ matches locale’s 2 lowercase letters ISO 639-1 code. English localized resource file _Mapsforge-for-MyTourbook.en_ and German localized resource file _Mapsforge-for-MyTourbook.de_ are provided. Script can be easily localized to any other system’s locale by providing a corresponding resource file using English resource file as a template.

Screenshot of graphical user interface:  
![GUI_Windows](https://github.com/user-attachments/assets/c725e598-adc2-4ad9-83d0-a122e259977b)

### Installation

1.	MyTourbook  
Windows: If not yet installed, download and install latest MyTourbook version from [download section](https://mytourbook.sourceforge.io/mytourbook/index.php/download-install).  
Linux: If not yet installed, download and install latest MyTourbook version from [download section](https://mytourbook.sourceforge.io/mytourbook/index.php/download-install).  
Run MyTourbook at least once to initialize program's settings.

2.	Java runtime environment (JRE) or Java development kit (JDK)  
Note: JRE version 21 or higher is required by recent MyTourbook version. If MyTourbook however has installed it's own Java environment, JRE version 11 is sufficient. Each JDK contains JRE as subset.  
Windows: If not yet installed, download and install Java, e.g. from [Adoptium](https:/adoptium.net/de/temurin/releases).  
Linux: If not yet installed, install Java runtime package using Linux package manager. (Ubuntu: _apt install openjdk-<version\>-jre_ or _apt install openjdk-<version\>-jdk_ where _<version\>_ is sufficient or higher)  

3.	Mapsforge tile server  
Open [mapsforgesrv releases](https://github.com/telemaxx/mapsforgesrv/releases).  
Download most recently released jar file _mapsforgesrv-fatjar.jar_ from   _<release\>\_for\_java11_ assets.  
Windows: Copy downloaded jar file into Mapsforge tile server’s installation folder, e.g. into folder _%programfiles%/MapsforgeSrv_.  
Linux: Copy downloaded jar file into Mapsforge tile server’s installation folder, e.g. into folder _~/MapsforgeSrv_.  
Note: Server version 0.22.0.0 or higher is required.  

4. Alternative Marlin rendering engine (optional, recommended)  
[Marlin](https://github.com/bourgesl/marlin-renderer) is an open source Java2D rendering engine optimized for performance, replacing the standard built into Java. Download is available at [Marlin-renderer releases](https://github.com/bourgesl/marlin-renderer/releases).  
Download jar file _marlin-\*.jar_ from _Marlin-renderer \<latest version> for JDK17+_ section's assets.  
Windows: Copy downloaded jar file into Mapsforge tile server’s installation folder, e.g. into folder _%programfiles%/MapsforgeSrv_.  
Linux: Copy downloaded jar file into Mapsforge tile server’s installation folder, e.g. into folder _~/MapsforgeSrv_.  

5.	Tcl/Tk scripting language version 8.6 or higher binaries  
Windows: Download and install latest stable version of Tcl/Tk, currently 9.0.  
See https://wiki.tcl-lang.org/page/Binary+Distributions for available binary distributions. Recommended Windows binary distribution is from [teclab’s tcltk](https://gitlab.com/teclabat/tcltk/-/packages) Windows repository. Select most recent installation file _tcltk90-9.0.\<x.y>.Win10.nightly.\<date>.tgz_. Unpack zipped tar archive (file extension _.tgz_) into your Tcl/Tk installation folder, e.g. _%programfiles%/Tcl_.  
Note: [7-Zip](https://www.7-zip.org) file archiver/extractor is able to unpack _.tgz_ archives.   
Linux: Install packages _tcl, tcllib, tcl-thread, tk_ and _tklib_ using Linux package manager. (Ubuntu: _apt install tcl tcllib tcl-thread tk tklib_)

6.	Mapsforge maps  
Download Mapsforge maps for example from [openandromaps.org](https://www.openandromaps.org). Each downloaded OpenAndroMaps map archive contains a map file (file extension _.map_). Tile server will render this map file.  

7.	Mapsforge themes  
Mapsforge themes _Elevate_ and _Elements_ (file extension _.xml_) suitable for OpenAndroMaps are available for download at [openandromaps.org](https://www.openandromaps.org).  
Note:  
In order "Hillshading on map" to be applied to rendered map tiles, hillshading has to be enabled in theme file too. _Elevate_ and _Elements_ themes version 5 or higher do enable hillshading.

8. DEM data (optional, required for hillshading)  
Download and store DEM (Digital Elevation Model) data for the regions to be rendered.
Notes:  
Either HGT files or ZIP archives containing 1 single equally named HGT file may be supplied.  
Example: ZIP archive N49E008.zip containing 1 single HGT file N49E008.hgt.  
While 1\" (arc second) resolution DEM data have a significantly higher accuracy than 3\" resolution, hillshading assumes significantly much more time. Therefore 3\" resolution usually is better choice.  
    
   \- HGT files with 3\" resolution SRTM (Shuttle Radar Topography Mission) data are available for whole world at [viewfinderpanoramas.org](http://www.viewfinderpanoramas.org/Coverage%20map%20viewfinderpanoramas_org3.htm). Unzip downloaded ZIP files to DEM folder.  
\- HGT files with 1\" resolution DEM data are available for selected regions at [viewfinderpanoramas.org](http://www.viewfinderpanoramas.org/Coverage%20map%20viewfinderpanoramas_org1.htm). Unzip downloaded ZIP files to DEM folder.  
\- ZIP archives with 3\" and 1\" resolution compiled and resampled by Sonny are available for selected regions at [Sonny's Digital LiDAR Terrain Models of European Countries](https://sonny.4lima.de). LiDAR data where available are more precise than SRTM data. Store downloaded ZIP files to DEM folder.

9.	Mapsforge for MyTourbook graphical user interface script  
Download language-neutral script file _Mapsforge-for-MyTourbook.tcl_, user settings file _Mapsforge-for-MyTourbook.ini_  and at least one localized resource file.  
Windows: Copy downloaded files into Mapsforge tile server’s installation folder, e.g. into folder _%programfiles%/MapsforgeSrv_.  
Linux: Copy downloaded files into Mapsforge tile server’s installation folder, e.g. into folder _~/MapsforgeSrv_.  
Edit _user-defined script variables settings section_ of user settings file _Mapsforge-for-MyTourbook.ini_ to match files and folders of your local installation of Java, Mapsforge tile server and MyTourbook.  
Important:  
Always use character slash “/” as directory separator in script, for Microsoft Windows too!

### Script file execution

Windows:  
Associate file extension _.tcl_ to Tcl/Tk window shell’s binary _wish.exe_. Right-click script file and open file’s properties window. Change data type _.tcl_ to get opened by _Wish application_ e.g. by executable _%programfiles%/Tcl/bin/wish.exe_. Once file extension has been associated, double-click script file to run.

Linux:  
Either run script file from command line by
```
wish <path-to-script>/Mapsforge-for-MyTourbook.tcl
```
or create a desktop starter file _Mapsforge-for-MyTourbook.desktop_
```
[Desktop Entry]
Version=1.0
Type=Application
Terminal=false
Name=Mapsforge-for-MyTourbook
Exec=wish <path-to-script>/Mapsforge-for-MyTourbook.tcl
```
or associate file extension _.tcl_ to Tcl/Tk window shell’s binary _/usr/bin/wish_ and run script file by double-click file in file manager.

### Usage

* After selecting task(s), map(s), theme file, theme style, style's overlays etc. in graphical user interface, hit _Start_ button to start tile server and MyTourbook. After MyTourbook has started successfully, activate MyTourbook's map _Mapsforge_ to show map(s) selected in graphical user interface. If changing any settings while MyTourbook is running, a restart of tile server is required to adopt new option settings. To restart server, hit _Start_ button again. As MyTourbook may be configured to cache tiles already loaded with previous settings, it is necessary to clear MyTourbook's tile cache, which happens at restart too. After restart, right-click MyTourbook's 2D Tour Map and force MyTourbook to reload failed map images or by zooming in and out via mouse wheel.
* Closing either graphical user interface or MyTourbook window will close tile server too.
* Use keyboard keys Ctrl-plus to increase and keyboard keys Ctrl-minus to decrease font size of graphical user interface and/or output console.
* See output console for tile server’s and MyTourbook's output.

### MyTourbook integration

Import _2D Map_ map provider files with Drag&Drop or _Import_ button in the preference page for _2D Map_ map providers.  

* File _mapsforgemap.xml_ defines _2D Map_ custom map provider _MapsforgeMap_ fetching map tiles from tile server.
* File _mapsforgehillshading.xml_ defines _2D Map_ custom map provider _MapsforgeHillshading_ fetching alpha-transparent hillshading tiles from tile server if selected in graphical user interface.
* File _mapsforgemaphillshading.xml_ defines _2D Map_ map profile _MapsforgeMapHillshading_ which composes Mapsforge server's map tiles with Mapsforge server's alpha-transparent hillshading.

Edit imported map providers and make sure that port number(s) in MyTourbook’s _Custom Url_ match port number(s) defined in Mapsforge-for-MyTourbook graphical user interface server configuration's _TCP port(s)_.

Set map provider _MapsforgeMapHillshading_ visible, whether hillshading  in graphical user interface is enabled or not and whether "Hillshading on map" or "Hillshading as map" is selected in graphical user interface.

Custom map provider _MapsforgeHillshading_ can also be used in other map profiles to supply map with alpha-transparent hillshading, e.g. OpenStreetMap. File _openstreetmaphillshading.xml_ defines _2D Map_ map profile _OpenStreetMapHillshading_ which composes MyTourbook's built-in map provider OpenStreetMap with Mapsforge server's alpha-transparent hillshading.

![MapProfile](https://github.com/user-attachments/assets/01342dcb-72bf-48f5-bba3-e4000a7a8faf)

Note:  
Zoom levels shown in _Map Profile Configuration_ are one higher than zoom levels internally used by query to the Mapsforge tile server.

### Example

Screenshot of MyTourbook showing Heidelberg (Germany), comparing _2D Tour Map_ and _2.5D Tour Map_, where _2D Tour Map_ using
* Map provider _MapsforgeMapHillshading_
* OpenAndroMaps map file _Germany_oam.osm.map_
* OpenAndroMaps rendering theme _Elevate_
* Theme file's style _elv-hiking_ aka _Hiking_ 
* Style's default overlays plus additional overlay _elv-waymarks_ aka _Waymarks_
* Hillshading settings as above

![Heidelberg](https://user-images.githubusercontent.com/62614244/164914282-07df684a-2f4a-420a-a998-f797f6b4865e.jpg)


### Hints

* Output console  
While console output of tile server and/or MyTourbook can be informative and helpful to verify what is happening as well as to analyze errors, writing to console costs some performance. Therefore the console should be hidden if not needed.
* Built-in world map  
Since the built-in [Mapsforge world map](https://download.mapsforge.org/maps/world/world.map) only shows the coastline, it only serves as a rough overview. Due to map's low resolution, coastlines show inaccurate at high resolution.  
In order not to cover an accurate map, the built-in world map has been automatically deactivated at higher zoom levels.    
Starting with server version 0.23.0.3, built-in world map is rendered with lower priority than user-defined accurate maps. Zoom level restriction was therefore removed. 
* Hillshading  
  * When selecting "Hillshading on map", map and hillshading are rendered  into one single map.  
  * When selecting "Hillshading as map", map and hillshading are rendered as two separate maps. Post-processing hillshading, gray value of flat area gets mapped to full transparency. Thus the flatter the area, the more the original colors of the map shine through. Finally, hillshading can be used as an alpha-transparent overlay for any map.  
[OpenTopoMap](https://opentopomap.org) uses same hillshading technique as hillshading algorithm "diffuselight".  
