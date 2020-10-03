# The Lerp Guide v2.3.4c
by ProdigySim and Don


## What is Interpolation?

Interpolation was meant to help keep gameplay smooth *even when packet loss occurs*, or when waiting between update packets.

When using an interpolation value of 100 ms, the game state you see (all player/object positions) is an [interpolated](http://dictionary.reference.com/browse/interpolated) game state that pulls from:
* The most recently received game state (last update/tick)
* The game state from 100 milliseconds ago

Essentially, this is going to mean that with cl_interp 0.1, what you see is going to be 100 ms behind the latest game state you received. Add on a ping of 50, and your client is behind the server by a full 150 ms every time it gets an update.



## What does interpolation affect?

Your average player isn't going to care much about messing with interpolation values at all, but in competitive play it can be very important.

* How early/late you can deadstop (and where the hunter or jockey appears to be when you do)
* How near or far you appear to be to a Survivor when you scratch or punch them (See: Tank Long Arms)
* How much time you have to skeet/deadstop something before its tongue/charge/pounce/punch lands
* How much things will move if you DO start losing packets
* How smooth things will look on a frame to frame basis

Basically, lerp can play a lot of different important roles in melee-ranged situations. Most players will benefit from adjusting their lerp from the default value. Note that your lerp value has nothing to do with whether you actually DO lose packets or not. That's controlled by network conditions entirely. Interpolation is just one solution to combat the jerkiness caused by lost packets and by the wait between packets.

So, an interpolation setting of 0 will make you lose smoothness (most people report jerky commons and SI), but it will give you the most current game state possible on your ping, and usually give you more time to deadstop hunters and whatnot.



## What should I set my interpolation to?

In general, you want a lerp that's lower than the default of 100 ms. Some people switch their lerp when changing between survivor and infected side, but any forms of lerp toggling are usually frowned upon. Current Confogl configs watch for lerp changes and announce them, and leagues and tournaments are developing rules about lerp changes.

For Survivor play you are always going to want a lower lerp. 
**The maximum value generally people use is 67 ms, and the lowest is 0 ms.
Other popular settings: 10 ms, 16.7 ms, 20 ms, 33 ms, 38 ms, 40 ms.**

It's important to note that the time between ticks on l4d2 is 33 ms, so we basically see a split in preferring < 1 tick of interpolation and > 1 tick of interpolation. Theoretically, many of these values are redundant, and only make tiny differences in what you see on your screen and how the server calculates your position and your hits.

For infected, higher lerp values can often be useful, as survivors generally run away from SI. Usually a survivor is going to make sure he/she is just out of the tank's reach. But, if the tank is using high interpolation, he won't see the survivor start to move for an extra 100+ ms. When using lerps extremely high, such as 400 ms or 500 ms, this problem is exacerbated greatly. The same phenomenon occurs when other special infected scratch survivors.
Confogl blocks lerps higher than 100 ms for this reason.

In general, though, you can still do everything you need to do as Infected with 0 ms, so it's recommended that you set your lerp to a value you're comfortable with on Survivor side.
Also, pouncing or charging another player will get harder the higher your lerp is, because the survivor position you see will not match up with the server's model. You will find more often that you pounced/charged right through a survivor and didn't hit.



## How do I set my interpolation?

Your interpolation value (lerp) is determined by the following formula based on your client cvars:


```cpp
min( max( cl_interp, cl_interp_ratio / cl_updaterate ), 0.5f )
```


To put this in english: 
Your cl_interp value is limited to a minimum value of *cl_interp_ratio / cl_updaterate* and a maximum of 0.5 (500 ms), and is set by the *cl_interp* cvar value.
Note that for example cl_interp 0.04 results in 40 ms lerp.

When setting your lerp, a good idea is to set your cl_updaterate as high as possible, your cl_interp_ratio as low as possible, and then your cl_interp to what you actually want. This will minimize the value of the cl_interp_ratio/cl_updaterate-imposed limit and let you pick what you want for interp.

For example, I use 16.7 lerp, and my autoexec contains the following


```
rate 30000
cl_cmdrate 100
cl_updaterate 100     
cl_interp 0.0167
cl_interp_ratio -1   // actual value will clamp to the minimum value allowed by the current server
```


Normal servers allow 60 updaterate and a minimum interp ratio of 1. Confogl servers lock updaterate to 30 and allow interp ratio 0. This kind of a setting covers both bases.

Note that as you can see from the code, it is normally also advised to increase your rate setting to the L4D2 maximum of 30000, which tells the server that you can receive up to 30000 bytes/s which every normal connection nowadays should be able to handle. I also like to keep my cl_cmdrate value the same as my cl_updaterate, although due to engine limitations it technically doesn't make a difference whether you use 30 or 100 cmdrate.

If you use this snippet, edit the value for cl_interp as you wish depending on which lerp you want to use.
Note that on regular servers such as VALVe's official dedicated servers, the minimum lerp you will be able to use is 16.7



## So what lerp *should* I use?

If you are still unsure what lerp to use after reading the guide until here, I would recommend you to stick with the 16.7 lerp for now. If you see too many jerky animations, increase it until you feel comfortable with them. A lerp above 50 ms should give most users completely smooth common infected animations.



## Lerp on Net Graph

The source network graph will show your your lerp value somewhere in the middle. See [http://developer.valvesoftware.com/wiki/TF2_Network_Graph](http://developer.valvesoftware.com/wiki/TF2_Network_Graph) for picture.

This value is going to be your calculated final lerp value in most cases. i.e. this value will be the calculated result of the min/max formula above. This can be useful in determining if your interp-related cvars are set correctly.

The **COLORS** on the net graph are mostly useless to be honest. All they do is make people misread the TF2 Network Graph article and spread stupid rumors like:

> 35 on Valve servers is orange, which is okay. That represents a warning of possible lost packets. Yellow IS lost packets.
I learned all of this from word of mouth and decided to ignore all existing literature on the subject.



**Yellow Lerp:** The server's framerate is such that its own internal update interval is less than your interpolation time. Usually L4D2 servers calculate 30 frames per second, so, again, anything below 33 ms will show up as yellow on a Valve Official/default dedicated server. Of course, your interpolation value will still work just fine. It will just look yellow on network graph. :|

**Orange Lerp:** Your interpolation value is set to less than 2 / updaterate. This condition can only appear while the Yellow lerp condition is not triggered. This is also completely bullshit. It's basically a warning that when you lose packets, you'll probably see entities jump around. The value they use (*2 / updaterate*) Is not completely arbitrary. If you actually set your interpolation value to 2 / cl_updaterate or above, you'll have 2 extra buffer packets in your interpolation range in case any update packet ever gets lost. 
Again Orange lerp is all about "*What if* I lose packets?" It's only a warning that entities may jump around if a packet is lost.

**Neither yellow or orange lerp on network graph are indicators of packet loss or any other network issues. 
If you have yellow lerp, asking the server admin to turn up the server framerate is a good idea. In practice, neither of those conditions really matter at all.**



## Questions and Myths about lerp

> Shouldn't I set my lerp so it's close to my ping?


No, lerp has nothing to do with ping. Lerp is merely for creating smooth animations.
The server knows about your current ping and always automatically corrects your hitboxes when calculating hits server-side.


> Won't my hitboxes be more inaccurate the higher my lerp is? I can even see the difference If I enable the hitboxes!


No, the hitboxes you can see with sv_showhitboxes are the server-side hitboxes. When the server calculates whether you hit a shot or not, it knows not only about your current ping but also about your current lerp and moves the server-side hitboxes of other players back in time to correct this offset.


> Don't I need to time my deadstop differently depending on the ping or lerp of the **target** hunter? Don't hunters with higher lerp screw me up?


No, the pounce hit detection from hunter and jockey as well as the charge hit detection are different from the melee hit detection of scratches or tank punches. No matter what ping/lerp a hunter, jockey or charger uses, you always have to time your skeet/deadstop/level/dodge exactly the same. Your timing only depends on your own ping and lerp.


> My Lerp is a funny color in net_graph! I'm losing packets! **ABANDON SHIP!** You broke my game ProdigySim!


No. Lerp cannot cause packet loss. See above section on colors.



## Sources
* [http://developer.valvesoftware.com/wiki/Source_Multiplayer_Networking](http://developer.valvesoftware.com/wiki/Source_Multiplayer_Networking)
* [http://developer.valvesoftware.com/wiki/TF2_Network_Graph](http://developer.valvesoftware.com/wiki/TF2_Network_Graph)
* Experiences and extensive testing of several players from the community