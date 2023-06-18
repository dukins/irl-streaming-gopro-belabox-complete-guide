# ULTIMIATE-GUIDE-IRL-STREAM-BELABOX-GOPRO
This is a How-To for the IRL streaming setup with a GoPro(Hero 11 Black) (and the belabox). I found it really difficult to get all the information needed to set up a stream using a GoPro. There were SO many sites I had to visit to make it work. This guide shall help you overcome these hurdles to make life easier for upcoming streamers! The coming sections describe a setp-by-step guide, starting from a simple setup with only a GoPro and your phone. The next sections will require more equipment to make streaming work more seamlessly!
1) How to stream from the GoPro to twitch using mobile phone. 
2) How to setup RTMP server at home and stream using OBS.
3) How to stream with the belabox.

During the writing of this guide I was using the GoPro Quick app version: 11.18.1(15524)!
I was also using an android phone (Samsung Galaxy S20+) with Android 13. For some steps you will have to look up on how to do them on Iphone (sorry about that!)



## Troubleshooting
Join my Discord Server and post your questions in the "tech-stuff" or "troubleshooting-gopro-setup" channels!
### **https://discord.gg/fDD9hyxv**
You can also check out my twitch stream and we can have a live talk there!
### **https://twitch.tv/twiqsp**

## 1. Streaming from the GoPro to twitch.tv
0) OPTIONAL: Create a GoPro account (gopro.com). This just helps, so you do not have to click "Continue as guest" every time you open the app. Trust me, it WILL get annoying at some point.
1) Install GoPro Quik app on your phone. Optional: Login with your account created in step 0) (click on the "person icon" on the top left)
2) Click on the "GoPro" icon on the bottom bar (there should be four icons: Mural, Media, Studio, GoPro)
3) Connect your GoPro with your phone
   1. on your GoPro: swipe down, swipe left, click on Preferences, Wireless Connections, Connect Device, GoPro Quick App
      Follow the steps described.
   2. After successful connection you should see a layout where you can control your GoPro. On the upper side you should see fields with "Live Stream", "View Media", "Auto Upload". Click on "Live Stream".
   3. Click on whatever platform you want to stream on. In this guide we will take TWITCH
   4. Next step depends on what network you want to use:
      1. Mobile Hotspot: Go to the settings of your phone and activate Mobile Hotspot (Android: Settings->Connections->Mobile Hotspot and     
         Tethering: activate Mobile Hotspot (you can configure it with your own password etc., not going into detail here)
      2. select that network in the GoPro app. IF for some reason the connection will not come up just restart the app. Make sure you close
          it also when it's active in the background!
      3. Choose a title for your stream. BEWARE that you can only use 150 characters for the title. The GoPro app will not show how many 
           characters you used for the title. I suggest you type it in a notepad on your phone before and save it. That way you can always                retrieve when your connection should break up and you have to restart your stream again! Trust me, this is going to happen A LOT! ;)
      4. choose resolution (depending on your network, Lens, if you want to save the VOD or not
      5. click on continue when it is highlighted (after you have chosen your network and a title!)
      6. wait a little bit on the next screen, this can take a little bit (around 1-2 minutes max!), click on "Go Live".

WELL DONE! You have successfully started your stream from the GoPro directly to twitch! :) But from here your actual journey begins!
I do not recommend using this approach as your main go-to for streaming, since you will have a lot of disconnections and your stream will just stop. You will end up with a lot of cut VOD (10 second VOD, 32 seconds, 2 hours...) It will always depend on the mobile network how your stream will go!
So if you want a more reliable stream, go ahead and read section 2! Here you will not end up losing your viewers due to disconnects! :)

## 2. Creating your own RTMP server on your Home PC
This part will describe on how you set up your local RTMP server and streaming from the GoPro directly to that server! Also I will describe how you set up your OBS so you can stream that feed to twitch. As I said in section 1, this is a more reliable approach, since the stream will not end when your mobile connection drops.
* NOTE: This part is done on WINDOWS 11! (Section 3 will show how to get the SRTLA relay server going on Ubuntu 22!) 

1. Download the Monaserver files here: https://www.toolsforgopro.com/dl/monaserver.zip
2. Open the Monaserver.ini file and scroll down to [RTMP]
3. Change host to your local IP (ipconfig->ipv4 address) Lots of guides for this on the internet
4. Choose a port e.g. 1935
5. Choose same publicPort
6. write your WAN IP in publicHost (search whatismyip on google)
7. Save the file and close it
8. In the Monaserver folder, go into the "www/live" folder (if live does not exist, create it), create a folder with your STREAM-KEY (needed later for the address stream with the gopro); STREAM-KEY can be anything you want, e.g. goprostreamabc123
   -> your folder structure should now look like this: Monaserver/www/live/STREAM-KEY
9. NOW THIS IS IMPORTANT: Login to your router and enable the port you chose before: e.g. 1935! Tons of guides on how it is done on the internet, will depend on what router you use!
10. ALSO IMPROTANT: Download this application called Restart-on-Crash: https://www.majorgeeks.com/files/details/restart_oncrash.html
    * This is a VERY handy tool for your RTMP server to be rebooted in case it crashed (happened to me!)
    * There is a youtube video on how to set it up -> https://www.youtube.com/watch?v=cW9MFgNRvkk
    * I have configured it the way that when I open that application it starts Monaserver.exe!
    * You can also use it without, but I would not recommend! (trust me :))

11. Connect your phone to the GoPro as describe in section 1! At this point you should know how to do it ;)
12. Click on Live Stream->Other/RTMP; as before select a network you want to use to send your stream from
13. THIS IS THE IMPORTANT PART:
    1. Get your public ip, publicPort AND your streamkey that you chose earlier!
    2. ENTER YOUR RTMP URL: rtmp://YOUR-PUBLIC-IP:publicPort/live/STREAM-KEY (save this link in a notepad file, in case you want to test       
       different IPs etc.)
    3. Choose the rest to your likings
    4. when continue is highlighted, click on it and then on "Go Live"
    5. Now you should see some activity on the terminal where the Monaserver shows it's information! We are good to go, the GoPro is sending
       it's feed to your local PC!
    6. Now open OBS->add scene->as a source choose Mediasource
    7. Uncheck "local file" and enter the same RTMP URL you typed in the GoPro!
    8. OPTIONAL: You can set network buffer to 1MB and Latency to 2 seconds, leave the rest as it is.
    9. Now you should be able to see your GoPro feed on OBS, the rest is only setting up your account where you want to stream to (Tons of 
       guides out there ;)).
       
"I am a professional streamer now!" is what you think. WOAH, hold your horses, buddy, we are not quite there.. YET! :) This approach will also fail from time to time since you can only use 1 (ONE) mobile connection to stream.. BUT HEY there is still section 3 that awaits us! So let's go to that last part so we you can call yourself a professional streamer and have a quality time with your viewers!

## 3. Streaming with the Belabox
Alright, we have come a looong way now. Almost there to have a perfect set up. To have more reliable stream you need something that can handle multiple carriers at the same time, so your bitrate does not drop during your streams even in the remote areas. And here we are going to use what is called "BELABOX". HUGE thanks to rationalIRL to create this project to be more affordable for new streamers! (The liveU costs a ton of money for the box alone without peripherals. You can go with it if you have the money).

### <a name="section-5-2"></a> List of equipment you need:
* NVIDIA Jetson Nano 2GB / or 4GB Version: 2GB: https://amzn.to/3NgMiGy | 4GB: https://amzn.to/3Pjt460
* GoPro (Hero 11 Black): https://amzn.to/45EjmRp
* Phone with the GoPro Quik App
* Mobile router (GL.iNet GL-MT300N-V2): https://amzn.to/42QZY0K
* Powerbanks: https://amzn.to/3IS0hkG (VARTA) | https://amzn.to/3qTvJsG (ANSMANN) | Powerbank for your phone also


### INSTALLATION AND SETUP STEPS
1. Go to BELABOX.NET to download the BELABOX IMAGE. 2GB: https://download.belabox.net/belabox_jetson_nano_2gb-latest.img.zip | 4GB: https://download.belabox.net/belabox_jetson_nano_4gb-latest.img.zip
2. Downlaod https://www.balena.io/etcher/ and flash your image on an SD-CARD: https://amzn.to/43MebNY 32GB are more than enough here!
   If you are not sure how to flash, watch the youtube video, rationalIRL describes it in detail on what to do or do a quick google search :)
3. Insert the card into the NVIDIA Jetson Nano (on the backside)
4. Now we will set up the SRTLA Relay Server on your local machine.
   * NOTE: THIS IS DONE ON AN UBUNTU MACHINE! I would recommend setting up a dual boot machine that has Windows and Ubuntu on it. Or get a    
     dedicated PC that runs Ubuntu!
   * HUGE shoutout to Codexual for his guide to setup an SRT Server at home!
     * watch this video to set up your SRT Server: https://www.youtube.com/watch?v=YhvRXWzRPm4 (it is lengthy so it would be too much for this
     guide). Do not forget to setup a service that the SRT server starts when you are starting your PC! It'll get annoying after a while 
     otherwise.
   * when done start the SRT server
   * go to https://github.com/Marlow925/srtla and clone the repository:
   * open terminal and type: 
     ```git clone https://github.com/Marlow925/srtla.git```
   * next type:
     ```cd srtla/```
   * in the folder there are some files, we only care about one here: srtla_rec
   * to start the srtla relay server type in the following:
     * ```./srtla_rec FIRST_PORT YOUR-PUBLIC-IP SECOND-PORT```
       Make sure you are using the same ports that you used in the SRT Server setup, check whether you have them enabled in your router! 
       Also check on your ubuntu machine if they are enabled with:
         * ```sudo ufw status```
         * If your ports are in the list you are good to go. If not, execute the following:
         * ```sudo ufw allow YOUR-PORT/tcp```
         * Do the same with "udp" instead of "tcp"
         * At this point I assume you have OBS installed on your machine. Check the Websocket settings in OBS for the used port. Enable that 
           port as well!
   * To make things easier create a alias/ shortcut in the bashrc file that will do these steps for you. Or create a service like before that 
     will start the SRTLA Relay Server.
     * for the bashrc approach do the following:
       * ```sudo nano ~/.bashrc```
       * scroll to the bottom and type in:
       * ```alias start-srtla='cd /home/$USER/srtla && ./srtla_rec FIRST_PORT YOUR-PUBLIC-IP SECOND_PORT'```
       * Change the ports and IP to the ones you chose/ have!
       * press CTRL+O; CTRL+X; back in the terminal type in:
       * ```source ~/.bashrc``` so the changes take effect
       * type in ```start-srtla``` Your SRTLA Relay Server should now be starting with a success message!
   * Now go to OBS create a scene and add Mediasource. Type in:
       ```srt://YOUR-PUBLIC-IP:SECOND-PORT/live/stream/YOUR_STREAM_KEY```
       * YOUR_STREAM_KEY is what you chose in the sls.conf (from the SRT SERVER SETUP VIDEO! Go watch it if you haven't!)
5. Now we can go back to our Belabox: Connect it to a powersource, and connect the Belabox with an ethernet cable to your router  
6. Login to your router to see what local IP your Belabox has (e.g. 192.168.XYZ.XYZ) 
7. Type it in your browser, a login should appear where you will choose a new password
8. You will now see a list of buttons (Start, Wifi (if you have a wifi stick connected), Ecoder Settings, etc.)
9. Go to Encoder settings, here you can go with the first approach to just test if the Belabox can send a stream to your OBS or choose the 
    second option to stream your GoPro feed to OBS
    * TEST PATTERN STREAM: jetson/h265_test_pattern
    * GOPRO FEED (WIRELESS OPTION):  jetson/rtmp_localhost_publish_live_50fps (or whatever fps you want to stream at)
10. Go to SRTLA Settings
    * SRTLA receiver address: YOUR-PUBLIC-IP
    * SRTLA receiver port: FIRST_PORT
    * SRT streamid: live/stream/YOUR_STREAM_KEY 
11. Go back up and click "Start". If no error message appears e.g. "Failed to connect to the SRT server. Retrying..." or "Failed to connect to the SRTLA server. Retrying..." we are goot to go.
12. Go to OBS to see your feed being displayed!
13. To set up your phone as a mobile hotspot to stream:
    * connect a Wifi stick to the Belabox
    * go to the UI page of the Belabox and click on Wifi: wlan0 -> choose your mobile hotspot
    * deselect eth0 and test the stream again, now all the data should go through your mobile connection
14. To be able to stream outside you need to connect a mobile router (see under [List of equipment you need:](#section-5-2) )
    * instead of your home router, connect your portable router to it.
    * To connect to your Belabox and start the stream, check the devices that are connected to your Mobile Hotspot on your phone
      * Settings->Connections->Mobile Hotspot and Tethering->Mobile Hotspot->Connected devices#
    * Open the browser on your phone and type in the IP of "belabox". You should be able to connect to it like on your PC.
    * DONE!

*YOU DID IT!* **NOW** you can call yourself a professional streamer! :D
Let your awesome journey without interruptions begin! Good luck out there buddy!
