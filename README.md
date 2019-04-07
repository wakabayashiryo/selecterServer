# selector Server

Raspberry Pi Media Player have output selector for RCA jack.
this program control selector using GUI on web browser.
## STEP1: Installation volumio OS [on windows]
[reference site](https://itdecoboconikki.com/2017/02/10/2017volumio-2041install/)
1. Download image file of leatest volumio   
2. Format SD card using SD CardFormatter    
3. Write image file to SD card using Win32DiskImager   
4. Insert SD card,Power on. don't plug ethernet.   
5. Awhile, connect Access Point using PC or Smart phone    
    *(SSID:Volumio Password:volumio2)*
6. Access http://volumio.local [in local net]
7. Using browser set configration of volumio   
[setting guide for using hardware](http://www.raspberrypiwiki.com/index.php/File:RPI-HIFI-DAC-manual-en.pdf)
8. Reboot   
9. Go to setting selector server    
**If you can not access the volumio,using application to serach IP address**

## STEP2: Installation Selectorserver [on Linux]
1. Access to http://volumio.local/dev and enable SSH.
1. Connect terminal using ssh ,can do by teraterm or linux terminal   
    *(Login name:volumio Password:volumio)*
2. Update and upgrade packages of the volumio   
    > sudo apt-get update   
    > sudo apt-get dist-upgrade   
3. Install python3 on volumio   
    > sudo apt-get install python3   
2. Clone this repository 
    > git clone https://github.com/wakabayashiryo/selectorServer.git
3. Install necessary packages for this program on python3
    > sudo apt-get -y install python3-rpi.gpio python3-flask   
4. Add service for automatically run program    
    Copy service files to system folder
    > sudo cp selectorServer/selector.service /etc/systemd/system
6. Start service and enable to automatically run
    > sudo systemctl daemon-reload   
    > sudo systemctl start selector   
    > sudo systemctl enable selector   
7. Check running service
    > sudo systemctl status selector
8. Reboot

## STEP3: Set Static IP address & Hotspot
1. Setting Icon  >> Network
2. Disable Automatic IP
3. Set Parameter   

    |item|parameter|   
    |:--|:--|   
    |Static IP address|192.168.0.56|    
    |NetMask|255.255.255.0|   
    |GateWay|192.168.0.1|    
    
4. Save Configration
5. Enable Fallback of Hotspot
4. Save Configration

## STEP4: Access Test
- ### mDNS version
    - volumio http://volumio.local   
    - selector http://volumio.local:8080

- ### static IP version

    - volumio http://192.168.0.56/   
    - selector http://192.168.0.56:8080/   
   
## topic
- The power status LED of raspberry pi change blinkng patern to heartrate.

    > sudo emacs /boot/config.txt 

    Add the following   

    > dtparam=pwr_led_trigger=heartbeat
    
- Digital Filter assemblied in PCM5122

    [Reference site](https://www.phileweb.com/review/article/201812/04/3283.html)

    > alsamixer
-  If hotspot did not work when setup new network    
    1. Delete Static IP address lines in /etc/dhcpcd.conf
    1. Setting SSID and PSK of New Router in /etc/wpa_supplicant/wpa_supplicant.conf   
        ~~~
        network={
        　　　ssid="SSID"
        　　　psk=password
        }    
        ~~~
    1. Reboot
    1. Serch Volumio's IP address and Resetup