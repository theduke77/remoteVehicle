# [EPOCH 1.0.6.1] Remote Vehicle Locking/Engine Status and kick out non group members.

* Discussion URL: https://epochmod.com/forum/topic/44104-release-remote-vehicle-lockingengineeject-script/
	
* Tested as working on a blank Epoch 1.0.6.1
* Uses clickActions as a dependancy

# REPORTING ERRORS/PROBLEMS

1. Please, if you report issues can you please attach (on pastebin or similar) your CLIENT rpt log file as this helps find out the errors very quickly. To find this logfile:

	```sqf
	C:\users\<YOUR WINDOWS USERNAME>\AppData\Local\Arma 2 OA\ArmA2OA.RPT
	```

# Install:

* This uses Click Actions by Mudzereli as a dependancy: https://github.com/mudzereli/DayZEpochDeployableBike/tree/master/overwrites/click_actions

**[>> Download <<](https://github.com/oiad/remoteVehicle/archive/master.zip)**

# Mission folder install:

1. If you don't have a custom compiles file do the following:
	1. In mission\init.sqf find: <code>call compile preprocessFileLineNumbers "\z\addons\dayz_code\init\compiles.sqf";</code> and add directly below:

	```sqf
	call compile preprocessFileLineNumbers "dayz_code\init\compiles.sqf";
	```
	2. Copy the <code>dayz_code\init</code> folder structure to your mission folder root.

2. Copy the supplied <code>ui_selectSlot.sqf</code> to <code>dayz_code\compile</code> By default Mudzereli has his version in <code>overwrites\click_actions\ui_selectSlot.sqf</code>, delete his version to keep everything consistant.

3. In your clickActions config.sqf add this code block after the last line:

	```sqf
	DZE_CLICK_ACTIONS = DZE_CLICK_ACTIONS + [["ItemKey","Eject Passengers not in group","spawn remoteVehicle;","true",1]];
	DZE_CLICK_ACTIONS = DZE_CLICK_ACTIONS + [["ItemKey","Toggle engine on/off","spawn remoteVehicle;","true",2]];
	DZE_CLICK_ACTIONS = DZE_CLICK_ACTIONS + [["ItemKey","Unlock vehicle","spawn remoteVehicle;","true",3]];
	DZE_CLICK_ACTIONS = DZE_CLICK_ACTIONS + [["ItemKey","Lock vehicle","spawn remoteVehicle;","true",4]];
	```
	
4. In <code>overwrites\click_actions\init.sqf</code> Remove the following line:

	```sqf
	player_selectSlot = compile preprocessFileLineNumbers "overwrites\click_actions\ui_selectSlot.sqf";
	```

5. In <code>mission\description.ext</code> Add the following line at the end of the file:
	```sqf
	#include "scripts\remoteVehicle\remoteVehicle.hpp"
	```

6. If you have no <code>stringtable.xml</code> in your mission pbo root directory, copy the supplied <code>stringtable.xml</code> file to your mission pbo.

7. If you run ESSv3 or any other scripts that use the <code>stringtable.xml</code> file (ZSC, Virtual Garage, Remote Vehicle etc) diff merge the supplied stringtable.xml with your version.

# Battleye filter install:
1. In your config\<yourServerName>\Battleye\scripts.txt around line 12: <code>5 createDialog</code> add this to the end of it:

	```sqf
	!"createDialog \"remoteVehicle\";"
	```
	
	So it will then look like this for example:
	```sqf
	5 createDialog <CUT> !"createDialog \"remoteVehicle\";"
	```