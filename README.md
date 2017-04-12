# Dog Door Sentry SmartApp (standalone) for SmartThings MultiSensor

This is a rough initial (but fairly functional) shot at a dog door monitor for SmartThings using one of the standard multisensors' accelerometer.

I didn't want to just see if the dog used the dog door, I wanted to know if I should be looking outside or inside for him.

Eventually I want to make it a proper Device Type or have some kind of visual indicator in the SmartThings app of whether the app thinks the dog is outside or inside, but I was having issues getting that part working and got busy with other things, so I'll go back to that at some point, but in the meantime this has actually been working fairly well.

Stable: 2016-06-04

Should work with the following device handler types (any sensors that have accelerometers with values from -1000 to +1000):
SmartSense Garage Door Multi
SmartSense Multi
SmartSense Multi + Graph
SmartSense Multi Sensor


#Installation - Software
1. Open the smartthings-dogdoorsentry-standaloneapp.txt file in your favorite text editor.  Hopefully the line breaks aren't stupid.  If everything is doublespaced or on a single line, try a proper programming IDE or something.

2. Log in to SmartThings API: https://graph.api.smartthings.com/login/auth

3. Go to My SmartApps -> New SmartApp -> From Code -> paste code from step 1 -> Save (maybe Publish -> For Me? it's been a while since I've messed with this, will update later if I get back into it)

4. From there, you set it up just like any other SmartApp where you tell it what sensors and such to attach to.
Options:
  Select Sensor - Should be self explanatory. You only need the larger half of the sensor, not the contact sensor magnet half.
  Send Push Notification - Whether to send push notifications to your phone when triggered
  Notify on all activity - Notify on sensor "isactive", not just flap swing, not recommended but it's htere
  Send a text message to this number (optional) - Provide a phone number to text, if you'd like
  In/Out or Out/In - Switches what's considered in and out in case they seem reversed after you install the hardware
  Device Orientation - Detecting swing works the same when the device is horizontal and vertical, but changes a bit if you're mounting the sensor on it's front or back (battery side).  You might mount something on it's front or back if it's on a hatch mounted in a ceiling or floor (weird, but I had the data for it so why not include it.. any boat dwellers with a hatch in a ceiling for their dog/cat? hah)
  Dog's name (optional) - If a name is provided, it will say "Zwei came in/went out" verus "The doggo came in/went out".  If you have a cat, feel free to modify the code.  I love cats as well as dogs, but having a bunch of extra code to put "cat" in place of "dog" seemed silly.  :)
  
#Installation - Hardrware
1. The location on the dog door is kind of important. If you mount it too close to the top hinge, the sensor won't swing far enough to trigger this app.  I mounted mine roughly 2/3 of the way down and on the left side (so Zwei's nose wasn't hitting it every time he went out).  He's managed to come in by pushing the corner on the opposite side a bit more and not triggering the sensor, so it's not perfect. Making sure the sensor is somewhere not in the dog's way but somewhere it'll definitely swing when they use the door is important.

2. I used double-sided foam tape the length of the sensor (a smaller piece didn't work as well) on the dog door flap. Make sure to clean the spot on the dog door you plan to stick it to as I'm sure dirt and slobber and noseprints make tape not work so well

3. You can mount the sensor horizontally or vertically (I mounted mine vertically, as you can see in the picture in this repo)

Note: As mentioned above, you don't need the second part of the sensor, just the larger part that has the accelerometer in it. We're not measuring open/close here, we're measuring X, Y, Z orientation. 

# Notes
The current tolerance is set so if the sensor needs to swing to between 400 and 900 (out of 1000).  I use absolute values so that also covers -900 to -400.  Between 900 and 1000 (or I set 1100 for some reason), it's considered closed (although I don't do anything with that information).

I do attempt to prevent multiple triggers on one event by putting in a 4 second delay, but either Zwei's taking longer than 4 seconds (could be, he's 13+ years old now) or that part's not working... so I do get multiple alerts sometimes still.

Funny enough, whether you mount it vertically (like an I shape) or horizontally (like the top of a T) on a vertical/traditional dog door, it uses the same orientation to detect swing (z axis), but if you mount it on a horizontally mounted hatch/flap/something, it uses the z axis.  So that was easy to deal with (horiz vs vert on a vert dog door).


# To Do
1. Create a proper device with a nice graphical tile showing current doggo status
2. Fix the time delay thing to prevent multiple alerts

I think that's it for now.  I'd love any input anyone has.  I don't have a ton of time to work on this now, but I can try to answer questions.  And let me know if you found this useful and if you're actively using it.

Cheers, all!

-Trevor
