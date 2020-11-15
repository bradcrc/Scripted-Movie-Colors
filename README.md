# IMPORTANT Note:
**Home Assistant broke kodi position reporting in 0.115.**
 
While playing movies, home assistant will NO LONGER provide the correct media position, that has been broken.   This of course breaks this script unless you implement the workaround below.

#Workaround: 
A direct request to KODI at your player URL will get the current media position, since we don't know if or when HA will fix the kodi integration to do this properly. 

http://192.168.0.xxx:8080/jsonrpc?request={%22jsonrpc%22:%20%222.0%22,%22id%22:%20%2214146359%22,%22method%22:%20%22Player.GetProperties%22,%22params%22:%20{%22playerid%22:%201,%22properties%22:%20[%22time%22]}}


use http get, return JSON, parse time.  



-------------------


# Scripted-Movie-Colors
A Node-RED flow for lighting color changes during movie scenes using Home Assistant.

https://www.youtube.com/watch?v=3KvEv_khuUM


# Installation
1. Open the **MovieColors.json** file in a text editor and replace "kodi" with the actual name of your kodi media player.
2. Import the **MovieColors.json** flow into Node-RED. 
3. Edit your configuration.yaml in HomeAssistant

  Under **media_player:**  Find the kodi media player you wish to use and add scan_interval: 3
  
     - platform: kodi
       host: 192.168.0.123
       name: my kodi player       
       scan_interval: 3
       
  Under **light:**  Create a new light group named Movie Color Group, this should contain any color light entities you want to control.
  
     - platform: group
       name: Movie Color Group
       entities:
        - light.mybulb
        - light.led_strip
 
 
 **Optional:** 
 
 Create a folder named MovieColor in your node-red folder.  Copy sample movie .txt files to this folder if you wish. The file name is case-sensitive and will need to match the name of your movie exactly (minus special characters).
 
 Turn on fade effect for your color lights.  If you have Tasmotized color bulbs or LED controllers, turn on fade by going to the console and entering: **Fade 1**, and **Speed 11**.  This will enhance the color change effect, and also 
 make any timing issues much less noticeable.
 
 # Usage
 1. Find a movie you'd like to have custom light colors during different scenes
 2. Play the movie in Kodi (version 18.3 or OLDER required)
 3. When the scene change comes up, 
      a. Pause the movie
      b. Change your light to the color you want
      c. Press "Hit to Record" under Record Colors in Node Red.
 4. Repeat for other color changes in the movie.
  
That's it.  The next time you watch the movie, your color bulbs should change to the color you specified near the time you specified in the movie.


# Considerations
 
 1. The scan_interval setting controls how frequently home assistant is updated on the current position of the playing movie.  A lower number will increase traffic, but will increase the accuracy of the timing.  A higher number will generate less traffic, but will result in less accurate color change timing.
 
 2. Change times are not exact, and can vary by several seconds since the time is only checked every few seconds, use these color changes only for long scenes to avoid distracting timing errors.
 
 2. Color bulbs with local control such as Tasmota will have a much faster response time than bulbs such as Tuya which send requests to China before changing the color.  Increased latency will also affect the accuracy of color change timing.  You can adjust the time offset to allow for more time.
 

# Suggestions

 1. Use the color effect sparingly.  If you change the colors too often during a movie it will lose impact and just become distracting.  Choose color moments carefully and less often for maximum effect.
   
 2. You can easily remove or manually edit the .txt files if needed.
 
 3. Attach actions to the no file found node to run lighting scripts for movies without custom color data.
 
 4. You could modify the functions to add another value for brightness if you wanted for added effect.
 
 
