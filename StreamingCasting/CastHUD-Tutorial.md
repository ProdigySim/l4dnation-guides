# CastHuD Tutorial for Server Owners & Streamers 
By SirPlease

## Introduction:
A fine day to write another tutorial.
My inspiration for this one comes from seeing every single cup game that's been streamed after "**THE Valve Bomb**" with the standard confogl spechud.
Not even one game was streamed with the use of a CastHuD.

## Chapters
- 1. Server Owner Setup
- 2. Streamer Setup

-------
**< Here we Go! >**

-------

## 1. Server Owner Setup

### Left4DownTown - Main CastHuD Support

Your server will be **unable** to support CastHuDs if it can't load Visor's updated Left4DownTown which is used in EQ (If your server supports EQ you're fine!)

This means that most Gameservers will not be able to provide a smooth viewer experience for tournaments (watchl4d for example) as they tend to have outdated systems.

If you own a VPS/Dedicated Server, but are still unable to run your server on the latest Left4DownTown, you will need to update your glibc.
Google will be more of a help in this as it's different for each distro.

Visor's Left4DownTown: [Download](https://github.com/Attano/Equilibrium/raw/master/extensions/left4downtown.ext.2.l4d2.so)
Install Instructions -> Place in your Extensions Folder.

Gamedata: [Text](https://github.com/Attano/Equilibrium/raw/master/gamedata/left4downtown.l4d2.txt)
Install Instructions -> Copy + Paste the text into the existing left4downtown.txt (Located in Gamedata folder)

------


**Keep in mind that the controlling cvar is: "l4d2_addons_eclipse"**
-1 = Use addonconfig.cfg (Doesn't support CastHuD)
0 = Allow Addons for Everyone.
1 = Block Addons for Everyone except for Casters.

You need to have this set at **1*** before players have connected in order to actually disable the addons during Cup matches.

I recommend keeping sm_cvar l4d2_addons_eclipse in your server.cfg though, as fairplay > eyecandy.

----

### Caster Addons
Then of course we're going to need a plugin to make use of Left4DownTown's ability of allowing addons on certain players.
I recommend to force this plugin to be loaded on every matchmode config. 

**!!!!!!!! Make sure this plugin is loaded **AFTER** readyup !!!!!!!!!!**

[Source](https://github.com/Attano/Equilibrium/blob/master/source/caster_addons.sp) / [Plugin](http://www.mediafire.com/?ypil05pamggs1)

#### Caster Assister
This is a simple yet awesome plugin that wasn't included in the Promod package (No clue why!)

This plugin allows spectators to increase/decrease their spec speed individually while also allowing them to go up or down by using Use and Reload.

I recommend to force this plugin to be loaded on every matchmode config as well.

[Source](http://codepad.org/dEelB058) / [Plugin](http://sirftp.com/Left4Dead2/Plugins/caster_assister.smx)

## 2. Streamer Setup

### The CastHuD
CastHuDs are incredibly fancy and informative, they prevent the need to press "TAB" every now and then to show the scoreboard to viewers.
Zeon's CastHuD has got to be the most used HuD for Streaming in the business, and for good reason.
I've added a Simple yet "Stylish" logo to the mix and this came out: [Preview](http://i.imgur.com/IBV15vG.jpg)

#### Requirements
[CastHuD Addon](http://www.mediafire.com/download/abdumou965ubi8o/watchl4dcasthud.vpk)
[Cast.cfg](http://www.mediafire.com/download/g80zvgs7cmkahzy/cast.cfg)

#### Optional
[Disable Orange Infected Vision VPK](http://www.mediafire.com/download/11fnz3a329l51q0/disable_orange_infected_vision.vpk)

#### Instructions
- Place the addon(s) in your addon folder.
- Edit the cast.cfg file to your needs and place it in your cfg folder, read the file!!!
- After a Matchmode is loaded an Admin needs to register you as a Caster. (To do this, the admin must use "!caster <namehere>")
- After you've been registered as a Caster, reconnect to the server to make your Addons work.
- Open up console and type "exec Cast.cfg"

#### Tips
- You can use your "Use" button to go up.
- You can use your "Reload" button to go down.
- The Latest Version (20th March 2014) no longer requires you to turn off the Scores to switch between Players.

**Support**
Q: "All the healtbars are grey"
A: Exec Cast.cfg again

Q: "Score is Overlapping"
A: Exec Cast.cfg again

Q: "Cast.cfg can't be loaded"
A: Make sure you save the file as a .cfg file and not a .txt file.

Q: "It shows the scores for the wrong teams"
A: !spectate