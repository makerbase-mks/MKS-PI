# MKS-PI
As we all know, the Klipper firmware has the advantages of high printing speed, high precision, and the ability to use the web page to control the printer, etc. MKS PI is a high-end microcomputer board designed by makerbase to replace the Raspberry Pi for the convenience of 3D printing users to use the Klipper firmware. The size, mounting holes, and most interface locations are also compatible with Raspberry Pi 3B. 
In terms of hardware, MKS PI has a powerful 4-core 64-bit SOC onboard, with 1GBytes of DDR3 memory, supports HDMI screen interface and PI-TS35 screen interface, provides Ethernet port, 3-channel USB interfaces (can be connected to a 3D printer main board, USB Wireless network card, USB camera, U disk, USB keyboard and mouse, etc.);   
In terms of software, Makerbase provides a complete Klipper firmware transplanted based on the Armbian desktop system, and directly supports klipperScreen. Users only need to download the image file provided by Makerbase, burn it to the TF card, without a lot of construction work, use the usb port or serial port to connect your main board, configure the parameters on the webpage, and you can use the Klipper firmware happily!  

![未命名1656336496](https://user-images.githubusercontent.com/12979070/175953356-ed7bb300-acaa-459e-89b1-6b46a0ae0d55.png)

## Features and advantages
1. Onboard powerful 4-core 64-bit core SOC, with 1GBytes of DDR3 memory;
2. DC12/24V power supply, more stable power supply;
3. Support HDMI screen interface, PI-TS35 screen interface;
4. Provide wired Ethernet port, 3-way USB interface (can be connected to 3D printer main control board, USB wireless network card, USB camera, U disk, USB keyboard and mouse, etc.);
5. The mounting holes and dimensions of the board are the same as those of the Raspberry Pi, which can be directly replaced by the Raspberry Pi.

## Mainboard parameters  
![bcd](https://user-images.githubusercontent.com/12979070/175954491-4c3b2608-140e-4283-875e-8dab8888d676.png)

## Wiring Diagram  
![efg](https://user-images.githubusercontent.com/12979070/175954568-43ede0db-cca0-4df0-8e14-3bef6976cc05.png)

## Dimensions  
![ffs](https://user-images.githubusercontent.com/12979070/175954644-ff3fb834-89da-491a-8f0b-a99a938015e1.png)

## Download and install system images
Makerbase provides a complete Klipper firmware transplanted based on the Armbian desktop system, and directly supports klipperScreen. Users only need to download the image file provided by Makerbase, burn it to the TF card, without a lot of construction work(If you have purchased a package that includes a TF card, the TF card has already been burned into the system before leaving the factory, and you do not need to burn it again unless you want to update a new image.).   
### Hardware Preparation
- A TF memory card not less than 8G
- TF card reader
- PC with windows operating system installed
- Wireless network card or network cable
- Type_C cable
### Software preparation
- System file download link:
- Install balenaEtcher v1.5 and above, download link:
[https://www.balena.io/etcher/](https://www.balena.io/etcher/) 
- Install putty, download link: [https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
 
### Flash system files
1. Format TF card  
Format TF card to FAT32 format before flash system files  
2. Insert the TF card into the card reader, and insert the card reader into the PC  
3. Unzip the downloaded image file  
4. Run balenaEtcher, import the decompressed image file->Select TF card->Click to start flash  
![ddd](https://user-images.githubusercontent.com/12979070/175958595-3052068e-e06e-415a-b01d-b50fd21de4a4.png)  
5. After the flashing is finish, insert the TF card into the MKS PI and power on with DC12/24V  

## MKS PI network connection
### Using the Ethernet  
Just set your router to using DHCP, plug the network cable into the MKS PI, done.
### Using USB WiFi Adapter
MKS PI supports most of the commonly used USB WiFi Adapters are supported, but they are not guaranteed to be available. According to the current testing experience, it is not recommended to use adapters based on RTL8818gu (venderID). (In our test, it takes about 27% CPU load).  
Insert the USB WiFi adapter to one of the 3 usb ports of MKS PI, you have two ways to config it to connect to your router.
#### Through the config file on the TF card
- Before power on, insert the TF card to the PC with TF card reader, it would generate two disks on PC
- Open the "Boot" disk, find the config file "xxxx" and open it with text editing software (e.g. notepad, notepad++, etc.)
- Modify the SSID and Password according to your actual router, save the config file 
- Remove the TF card from the PC, and insert it to the MKS PI
It would connect to your router automatically.
#### Through the serial software(we using Putty to describe below) 
- Prepare putty according to the [steps](https://github.com/makerbase-mks/MKS-PI#using-serial-software-on-pcwe-using-putty-to-describe-below)
- Enter the command “nmtui” to connect to the network. 
- Select “Activate a connection”, select the wifi and enter the password to connect.  
![EEEEEE](https://user-images.githubusercontent.com/12979070/175969814-e96acf80-4c83-4bf0-917d-ebe44bbefaed.png)

![RRRR](https://user-images.githubusercontent.com/12979070/175969838-b8a985ac-b01b-4332-9802-8ad72ae3427d.png)  

### Get the IP of MKS PI
After connect MKS PI to the network, you can get its IP address in two ways
#### From the Serial software on PC
Enter the command “ip a” and view the IP
#### From KlipperScreen 
If you have a PI-LCD or HDMI screen connected with MKS PI, it would run KlipperScreen after system boot. You can find your IP address on the "Config"->WiFi

## Using Serial software on PC(we using Putty to describe below)  
Putty is a famous tool, you can use either SSH or Serial to connect to the MKS PI.  
- Connect the MKS PI with the TYPE-C cable to the PC, supply power to the PI, check the COM port in the device manager of the PC, and then open Putty
- Select the COM port, set the baud rate to 1500000, and click “Open” to connect

![COM](https://user-images.githubusercontent.com/12979070/175967056-dd6aec07-084d-4b05-8199-88709755ea64.png)  

- If you open a black empty window, click the Enter key, and it will ask you to enter the login user and password
- There are two users in the system provided by Makerbase:
   > root user: root  
   > user2: mks  
   > their origin passwords are the same: makerbase  
- After enter the user and password, you can enter the system now.

   
