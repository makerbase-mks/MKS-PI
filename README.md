# MKS-PI

As we all know, the Klipper firmware has the advantages of high printing speed, high precision, and the ability to use the web page to control the printer, etc. MKS PI is a high-end microcomputer board designed by makerbase to replace the Raspberry Pi for the convenience of 3D printing users to use the Klipper firmware. The size, mounting holes, and most interface locations are also compatible with Raspberry Pi 3B. 
In terms of hardware, MKS PI has a powerful 4-core 64-bit SOC onboard, with 1GBytes of DDR3 memory, supports HDMI screen interface and PI-TS35 screen interface, provides Ethernet port, 3-channel USB interfaces (can be connected to a 3D printer main board, USB Wireless network card, USB camera, U disk, USB keyboard and mouse, etc.);   
In terms of software, Makerbase provides a complete Klipper firmware transplanted based on the Armbian desktop system, and directly supports klipperScreen. Users only need to download the image file provided by Makerbase, burn it to the TF card, without a lot of construction work, use the usb port or serial port to connect your main board, configure the parameters on the webpage, and you can use the Klipper firmware happily!   

Aliexpress Store Link: https://www.aliexpress.com/item/3256804231556479.html?spm=a2g0o.store_pc_home.slider_165457030.0&gatewayAdapt=4itemAdapt  

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
- System image download link: https://drive.google.com/drive/folders/1tTuSvF9OL2qtPXElau8YOXn2sWbdxa9e?usp=sharing
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

MKS PI supports USB WiFi Adapter, but not every type is guaranteed to be available. Now, we the types we have tested available include those based on RTL8188CUS(VID:PID = 0bda:8176)/RTL8188EUS(VID:PID = 0bda:8179)/RTL8188GU(RTL8710B)/(VID:PID = 0x0BDA:0xB711). According to the current testing experience, it is not recommended to use adapters based on RTL8188GU(RTL8710B), it has been supported on MKS PI, but it's driver takes a lot of CPU load(about 27% in our test). Other adapters like the one based on RTL8188CUS/RTL8188EUS have a perfect perfomance. 
Insert the USB WiFi adapter to one of the 3 usb ports of MKS PI, you have two ways to config it to connect to your router.

#### Through the config file on the TF card

- Before power on, insert the TF card to the PC with TF card reader, it would generate two disks on PC
- Open the "Boot" disk, find the config file "**wpa_supplicant-wlan0.conf**" and open it with text editing software (e.g. notepad, notepad++, etc.)
- Modify the ssid and psk according to your router, save the config file 
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

## Enter Fluidd interface

After connect the MKS PI to the network, you can directly enter the IP address of MKS PI with your PC's browser, and you can enter fluidd interface(Makerbase's image has installed fluidd, of cause you can install other interface).  
![微信图片_20220628192455](https://user-images.githubusercontent.com/12979070/176167313-b4c58d8a-ccd9-48b0-8cca-9598549ddddd.png)

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

## Connection MKS PI with motherboard

You can use 3 USB ports and a uart to connect MKS PI and your motherboard.  

### USB connection

Most 3D printing motherboards have a USB port converted from the serial port. Use a usb cable to connect it to one of the three B-type USB ports of the MKS PI.  
Find the device name of the USB port, login MKS PI from Putty or other serial software and type:   


```shell
ls /dev/serial/by-id/*
```


It will display the name like below(confirm your USB connection is ok):  
```shell
/dev/serial/by-id/usb-Klipper_stm32f407xx_4D0045001850314335393520-if00
```
Copy the device name to the "[mcu]" segment on `printer.cfg` file of Klipper :   

```python
[mcu]  
serial: /dev/serial/by-id/usb-Klipper_stm32f407xx_4D0045001850314335393520-if00
```

### UART connection

You can also use the uart0 on MKS PI to connect your motherboard(Make sure your motherboard has the uart pins lead out).      
On the `printer.cfg` file of Klipper, the serial should be `/dev/ttyS0`:   

```python
[mcu]  
serial:/dev/ttyS0
```

## ADXL345 connection and configuration

If you want to use the ADXL345, it is very easy to connect on MKS PI:  
![DDW](https://user-images.githubusercontent.com/12979070/176198630-f2537209-26f1-4e83-bb51-d7be60269dc0.jpg)

The MKS PI image has the acceleration calculation library and the dependent library installed by default, no additional configuration is required, just configure the ADXL345 and test position parameters in the `printer.cfg` file.

1. Configure adxl345 in the configuration file, copy the following parameters to the `printer.cfg` file  

    ```python
    [mcu rpi]  
    serial: /tmp/klipper_host_mcu    
    [adxl345]  
    cs_pin: rpi:None  
    spi_bus: spidev0.2
    ```

2. Save and restart Klipper, and send the query command after the web interface does not report an error：  
   `ACCELEROMETER_QUERY`  
   
   Now the acceleration sensor data can be received. The data is similar to the following:  
   
   ```python
   Recv: // adxl345 values (x, y, z): 430.619210, 831.432400, 8718.156800...
   ```

3. Configure the test position of adxl345, generally installed in the middle of the platform  

    ```python
    [resonance_tester]  
    accel_chip: adxl345  
    probe_points:  
        115, 115, 20  # an example
    ```

1. Test acceleration and configure input_shaper data  
   Before the test, first increase the acceleration configuration of the printer (you can change it to a smaller value after the test):  

    ```python
    [printer]  
    max_accel: 7000  
    max_accel_to_decel: 7000
    ```

5. If there is an input_shaper function parameter in the configuration file, you need to send an instruction to turn it off:  
   `SET_INPUT_SHAPER SHAPER_FREQ_X=0 SHAPER_FREQ_Y=0`  

6. Then send the auto test configuration command to start testing the vibration:  
   `SHAPER_CALIBRATE` 

7. After the test, it will return the recommended configuration method and configuration value of the x-axis and y-axis, configure the value in the configuration file, then save and restart, the configuration is similar to the following:  
   
    ```python
    [input_shaper]  
    shaper_type_x = 3hump_ei  
    shaper_freq_x = 52.4  
    shaper_type_y = 2hump_ei  
    shaper_freq_y = 37.5
    ```

## USB camera connection and configuration

The default image of MKS PI has already installed MJPG-Streamer and enable the USB camera. MKS PI supports most of the commonly used USB cameras(but not guaranteed). Normally, just connect your USB camera to one of B-Type USB port on MKS PI, you will see the preview video on the Fluidd interface.   
If you don't want to use the USB camera, you had better to disable it to reduce CPU load:  
Enter the setting item on the Fluidd interface -> camera -> default -> disable

## How to modify the device tree file
Maybe someone like to make some customized configration on device tree file,  
- SSH to login to the PI shell  
- Backup the /boot/dtb/rockchip/rk3328-roc-cc.dtb file, for example:  
 ```sudo cp /boot/dtb/rockchip/rk3328-roc-cc.dtb /boot/dtb/rockchip/rk3328-roc-cc.dtb.bak```  
- Decompile the dtc file to dts file:  
```sudo dtc -I dtb -O dts -o rk3328-roc-cc.dts /boot/dtb/rockchip/rk3328-roc-cc.dtb```  
- Modify the dts file just generated as you want, for example change the rotation of the lcd...  
- Compile the dts file to overlay the origin one  
```dtc -I dts -O dtb -o rk3328-roc-cc.dtb /boot/dtb/rockchip/rk3328-roc-cc.dts  ```  
- Reboot the system 

## How to rotate 180° for the TS35 display 
Should change the dts file of rk3328-roc-cc.dtb, we have made one [here](), for you can just download it, and then:
- SSH to login to the PI shell  
- Copy the downloaded rk3328-roc-cc.dtb to the direction of "/boot/dtb/rockchip" on MKS PI using software like WinSCP
- Reboot the system 

## Use with the tool header modules
Support using MKS PI with the tool header modules like MKS THR36/42, more details refer to : https://github.com/makerbase-mks/MKS-THR36-THR42-UTC

