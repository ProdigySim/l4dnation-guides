# Video Quality Guide
by ProdigySim

or "5 Tips for Better Video Quality"

I didn't have time to spice this up but I figured it was worth reposting.

### 1. Turn off mat_monitorgamma_tv_enabled when recording
This isn''t a huge deal, but might help keep your videos from looking washed out. I add gamma in post to pretty much every video I make, but this is a pretty standard practice when doing video editing anyway. Try to get as realistic of a source as possible and add more junk in post.

### 2. Disable frame resampling!
When you render/encode your video and send it to youtube, you only need 30fps. If you have source footage with a higher framerate, you''ll need to convert it to 30fps somehow. By default, most video editors will "resample" your video, blending frames together to get 30fps. This can sometimes make footage look good, but most often you''re going to lose sharpness/detail on your video as a result. BRB BOWFLEXIN` makes some really good videos that use frame-blend resample. purple and mason generally use drop-frame conversion for pretty vids.

IMO, the best option is to simply use a drop-frame framerate conversion instead. This is done in Sony Vegas by disabling resampling.
Tutorial: [Vegas Resample disabling Tutorial](http://www.youtube.com/watch?v=k6kNAd40Nfo#ws) <--

Pause at random points during these two videos and you will see the difference: (Sorry I don''t have equivalent comparison videos)
1. [720p with frame-blend resampling](http://www.youtube.com/watch?v=ROF_xqK4CnI#ws).
2. [720p with no resampling (drop frame)](http://www.youtube.com/watch?v=ycVTlXCCMlk#ws).
As you can see, the frame blending looks far less sharp. (TODO: Add a good comparison video)

### 3. Make your final video 1920x1072
**This has been fixed by YouTube and is no longer an issue! Feel free to upload full 1080p now.**
~So, this is an odd one. If you''re uploading to youtube, 1920x1072 comes out WAY better than 1920x1080. There''s a note about it on some support docs somewhere, but it''s hard to find.~
Check these out:
[This image](http://i.imgur.com/twiqQ.jpg) is from a 1920x1080 video uploaded to youtube. ([Source](http://www.youtube.com/watch?v=eeBax8yw6fM#ws))
[This image](http://i.imgur.com/EQH0L.jpg) is from the same video, but 4 pixels were taken off the top and the bottom (total of 8 taken off) of the video before it was uploaded. Much clearer. ([Source](http://www.youtube.com/watch?v=lxixXwX1VWI#ws))

This likely has something to do with their encoder splitting the image up into 16x16 chunks. Since 1080 isn''t divisible by 16, it may be squeezing the image in some way or another for some part of the encode *shrug*

Also, using 1080p instead of 720p is preferrable. I''ve always been somewhat dissatisfied with the quality when I upload 720p videos--I feel like maybe youtube makes better 720p encodes when you upload a 1080p video. Shrug again.~~


### 4. Add motion blur if possible.
When I was working on amalgam, I was testing out a bunch of different rendering/encoding options. I tested out different motion blur settings using a constant quality encode with x264 (actually --crf 18). As I turned up motion blur settings and used more sensitive motion blurs, the bitrate of the output video decreased. The motion blur was actually *simplifying* the video for the encoder.

Motion Blur has a dual purpose. Yes, it looks cool/pretty, but it also makes the video stream simpler for the encoder to encode. Encoders like x264 are able to compress video in large part by simplifying high-motion segments of video, and encoding them at lower bitrates. By adding in motion blur, we actually help the encoder complete this task.

So, tl;dr there: Adding motion blur will let Youtube''s encoder preserve your video''s quality better.

There''s some free motion blur available like MVTools, but the best quality motion blur is hands-down [ReelSmart Motion Blur](http://www.revisionfx.com/products/rsmb/). It''s available for Sony Vegas 10+, After Effects, and many other editors. I use its default settings, and it really makes great looking motion blur. 

Just a warning, adding motion blur WILL increase your render/encode times by a large amount. I like to add RSMB to my vegas projects via Track FX, so I can toggle it on and off easily before I do renders.

### 5. Do the highest quality encode you can stand to wait for.
I''ve messed around with a bunch of encode settings--trying to mimic Youtube''s encodes, various profiles, etc. There''s no magic bullet here. Youtube *WILL* re-encode your video no matter what. So, just try to create the highest quality input for it to work with. Giving it a lower quality encode doesn''t really help at all.

My personal workflow is something like the following:
Use Source Recorder to create TGAs + wav at a steady framerate.
Use VirtualDub to create a lossless Lagarith AVI from TGAs+wav, then delete the source files.
Use Vegas to do editing with a bunch of lossless files, edit in full 1080p @ 30fps.
Export from Vegas to lossless Lagarith again, at full 1920x1080.
Use AVISynth to do the final top+bottom 4 pixel crop, and feed that into MeGUI to do a final encode.
x264 high/unrestricted profile, --crf 18, Very Slow setting. Lame -V0 audio. Muxed to MP4 or mkv.

Rendering (with motion blur) takes about 30 minutes per minute of video footage for me... Encoding takes about twice that amount. 

I can do some more in-depth guides on any of these topics if people have interest. I just wanted to cover some of the most important aspects with this guide.

GL HF

###Examples: Resampling Options and Motion Blur
[Resampling + Motion Blur Test 1920x1072](http://www.youtube.com/watch?v=_acD6C7MzDQ#ws)
Uploaded at 1920x1072. The source video was full 1080p @ 60fps. You can decide for yourself which style looks best. YMMV.
See Also: [720p](http://www.youtube.com/watch?v=_JC0wdC3QrU#ws) [1080p](http://www.youtube.com/watch?v=SosZnDGCk5w#ws).

**Added bonus!** - [Basic Vegas project/render settings + my x264 settings from megui](http://imgur.com/a/lKqel)

See other posts below for more goodies.