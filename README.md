# Scripted-Movie-Colors
A Node-RED flow for lighting color changes during movie scenes using Home Assistant.


# Installation
1. Open the **MovieColors.json** file in a text editor and replace "kodi" with the actual name of your kodi media player.
2. Import the **MovieColors.json** flow into Node-RED. 
3. Edit your configuration.yaml in HomeAssistant

  Under **media_player:**  Find the kodi media player you wish to use and add scan_interval: 3
  
     - platform: kodi
       host: 192.168.0.162
       name: office fs kodi       
       scan_interval: 3
       
  Under **light:**  Create a new light group named Movie Color Group, this should contain any color light entities you want to control.
  
     - platform: group
       name: Movie Color Group
       entities:
        - light.mybulb
        - light.led_strip
 
 
 **Optional:** 
 
 Create a folder named MovieColor in your node-red folder.  Copy sample movie .txt files to this folder if you wish. The name will need to match the name of your movie exactly, including upper/lowercase letters.
 
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
