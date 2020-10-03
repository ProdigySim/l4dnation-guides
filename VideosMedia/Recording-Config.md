## Post By ProdigySim
Here's the recording config I use, adapted from Jay's original config. I think some of you might find it useful.

```//Recording config by ProdigySim and jay
exec crxglows-nowait.cfg // custom script to turn off my flashing glows

alias myframerate "host_framerate 30"

mat_monitorgamma_tv_enabled 0
//General Settings
cl_interp 0.1 // improve entity interpolation in playback
volume "1";
sv_cheats "1";
voice_enable "0"
closecaption "0"; //Turns captions off
c_thirdpersonshoulderaimdist "720"
c_thirdpersonshoulderdist "80"
c_thirdpersonshoulderheight "10"
c_thirdpersonshoulderoffset "0"
cam_collision "1"
cam_idealdelta "4.0"
cam_idealdist "40"
cam_ideallag "0"
cam_idealpitch "0"
cam_idealyaw "0"
cam_snapto "0"
cl_forcepreload "1";
snd_musicvolume 0
alias snd_musicvolume
net_graph 0;
alias net_graph
//mat_postprocess_enable "0"; //Hide boomer bile on HUD

// For using source recorder or srcdemo
bind f7 "myframerate; startmovie MOVIENAMEHERE; demo_resume; bind f7 ender"
alias ender "endmovie; host_framerate 0; demo_pause"


//Viewmodel Settings
r_drawviewmodel "1";
cl_glow_brightness "1"; //Turns glows off

//HUD Settings
hidehud "216"; //Shows chat and kill messages, but hides everything else
hud_zombieteam "0";
cl_hidemenu_spawnmode "0";
cl_hidemenu_spawnmode2 "0";
cl_hidemenu_spawnclass_boomer "0";
cl_hidemenu_spawnclass_boomer2 "0";
cl_hidemenu_spawnclass_hunter "0";
cl_hidemenu_spawnclass_hunter2 "0";
cl_hidemenu_spawnclass_smoker "0";
cl_hidemenu_spawnclass_smoker2 "0";

crosshair 0

//Aliases
alias fog_default "fog_override 0;"
alias fog_off "fog_override 1; fog_enable 0"
alias fog_low "fog_override 1; fog_enable 1; r_farz 10000000; fog_startskybox -1; fog_color 255 255 255; fog_colorskybox 255 255 255; fog_end 30000; fog_endskybox 30000; fog_start 1; fog_startskybox 1;"
// Settings for demo smoothing
alias smooth "hidehud 4; cl_drawhud 0; r_drawviewmodel 0"

//CSS Imported Commands compiled by clowN and FoX (I tried to remove as many of the useless commands as possible)
r_rainsplashpercentage "0";
cl_showpluginmessages "0";
cl_observercrosshair "0";
muzzleflash_light "1";
r_cheapwaterstart "99999";
r_cheapwaterend "99999";
r_rainsimulate "1";
r_lightinterp "5";
sv_specnoclip "0";
r_drawropes "1";
r_radiosity "4";
cl_showfps "0";
r_drawrain "1";
r_eyemove "1";
r_dynamic "1";
r_3dnow "1";
r_sse2 "1";

clear
echo "fog_default = default fog settings"
echo "fog_off = no fog"
echo "fog_low = low fog"
echo "smooth = hidehud 4, cl_drawhud 0, r_drawviewmodel 0 -- no hud or viewmodel at all"
```

Cool things to note:

Default settings remove all hud elements except kill messages.

Running "fog_low" in console will give you some cool fog settings to give further visibility and more vivid colors I think.

You should familiarize yourself with different hidehud settings for whatever recording you're doing.

The f7 bind is set up to use source recorder to record footage at 30fps. I usually edit this line at runtime (type bind f7 to get the current bind, then edit the line and rebind f7) for the clipname/framerate I want.

Maybe someone else has some additions to this to make? idk. Go hog wild.


## Post by cocolapin

I just registered to thank you for your work, really useful

Personnaly i added in your recording.cfg :

```
cl_cinematiclight_scale "0" // DISABLE ORANGE LIGHT OVER INCAPPED SURVIVOR

c_thirdpersonshoulderheight "10"                                // HEIGHT OF THE CAMERA (default=5)
c_thirdpersonshoulderoffset "0"                                 // SHIFT CAMERA ON RIGHT/LEFT +/-
cam_collision "0"                                               // AT 0 : CAMERA PASS THROUGH WALLS
cam_idealdist "200"                                             // DISTANCE PLAYER/CAMERA (max=200)  (default=150)

bind "1" "cam_idealdist 100"
bind "2" "cam_idealdist 110"
bind "3" "cam_idealdist 120"
bind "4" "cam_idealdist 130"
bind "5" "cam_idealdist 140"
bind "6" "cam_idealdist 150"
bind "7" "cam_idealdist 160"
bind "8" "cam_idealdist 180"
bind "9" "cam_idealdist 190"
bind "0" "cam_idealdist 200"

bind "p" "thirdpersonshoulder 1"                                 // ENABLE/DISABLE TPS VIEW
bind "n" "endmovie"                                              // ENDMOVIE
bind "m" "mp_gamemode coop"                                      // REMOVES "+1"s AND DAMAGE AMOUNT
bind "r" "r_drawothermodels 2"                                   // ENABLE "WALLHACK"
bind "t" "r_drawothermodels 1"                                   // DISABLE "WALLHACK"
bind "c" "r_drawviewmodel 0"                                     // DISABLE WEAPON/ARMS
bind "v" "r_drawviewmodel 1"                                     // ENABLE WEAPON/ARMS

```

And i added the following defaults commands into my autoexec in order to clean commands :
```
//DEFAULT TPS
c_thirdpersonshoulder "0"
c_thirdpersonshoulderaimdist "120.0"
c_thirdpersonshoulderdist "40.0"
c_thirdpersonshoulderheight "5.0"
c_thirdpersonshoulderoffset "20.0"
cam_idealdist "150"
cam_collision "1" 

//DEFAULTS BINDS
bind "1" "slot1"
bind "2" "slot2"
bind "3" "slot3"
bind "4" "slot4"
bind "5" "slot5"
bind "6" "slot6"
bind "7" "slot7"
bind "8" "slot8"
bind "9" "slot9"
bind "0" "slot10"
unbind "p"
unbind "n"
unbind "m"
bind "r" "+reload"
bind "t" "messagemode"
bind "c" "+voicerecord"
unbind "v"
```

Then, the only things to add would be add ons, easy to find : 
*enable thirdpersonshoulder in demos* [Recording Helpers](https://github.com/ProdigySim/recording_helpers)
disable blue infected vision [http://www.l4dmaps.com/details.php?file=14107](http://www.l4dmaps.com/details.php?file=14107)
disable orange infected vision [http://www.l4dmaps.com/details.php?file=14108](http://www.l4dmaps.com/details.php?file=14108)


perfect  :D
