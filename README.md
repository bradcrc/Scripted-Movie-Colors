# Scripted-Movie-Colors
A Node-RED flow for lighting color changes during movie scenes using Home Assistant.


# Installation
1. Import the **MovieColors.json** flow into Node-RED
2. Change media_player references to the name of your media player in **"Get Script File Name"**, **"Do the stuff"**, and **"get attributes"**
2. Edit your configuration.yaml in HomeAssistant

  Under light:  Create a light group named Movie Color Group, this should contain any color light entities you want to script.
  
     - platform: group
       name: Movie Color Group
       entities:
        - light.mybulb1
        - light.mybulb2
      
  Under media_player:  Find the kodi media player you wish to use and add scan_interval: 3
  
     - platform: kodi
       host: 192.168.0.162
       name: office fs kodi
       scan_interval: 3
    
 3. Create a folder named MovieColor in your node-red folder.  Copy sample movie .txt files to this folder if you wish. 
 
 **Optional:** Turn on fade effect for your color lights.  If you have Tasmotized color bulbs or LED controllers, turn on fade by going to the console and entering: **Fade 1**, and **Speed 11**.  This will enhance the color change effect, and also 
 make any timing issues much less noticeable.
 
 # Usage
 1. Find a movie you'd like to have custom light colors during different scenes
 2. Play the movie in Kodi (version 18.3 or OLDER required)
 3. When the scene change comes up in your movie, pause the movie, change your light to the color you want, and press the timestamp button under "Create Color Script" in Node Red.
 4. Repeat for any other color changes in the movie.
  
That's it.  The next time you watch the movie, your color bulbs should change to the color you specified near the time you specified in the movie.


# Considerations
 
 1. The scan_interval setting controls how frequently home assistant is updated on the current position of the playing movie.  A lower number will increase traffic, but will increase the 
 accuracy of the timing.  A higher number will generate less traffic, but will result in less accurate color change timing.
 
 2. Color bulbs with local control such as Tasmota will have a much faster response time than bulbs such as Tuya which send requests to China before changing the color.  Increased latency 
 will also affect the accuracy of color change timing.
