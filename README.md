
# Solved! .Net library available on my github!



Reverse engineering project of the usb protocol used to update the screen of the Logitech G19 keyboard.

Known data (Will be updated as this project advances)


Screen: 320x240 pixel

SoC: Texas instrument TMS320DM355ZCE

Nand: STMicroElectronics NAND256W3A2BN6

</br>

</br>

16 byte header is used for sending the image:

0x10, 0x0F, 0x00, 0x58, 0x02, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x3F, 0x01, 0xEF, 0x00, 0x0F
  
</br>


size of data package that's accepted by the device: 154 112 bytes
Size of image data: 154139 bytes (1233112 bits) according to USBPcap
   


# Data structure



The first 16 bytes is the header.

Following that is 496 bytes of nonsens data

and finally 153 600 bytes of image data

</br>



To understand more about the format, we need to know one things first:

<b>The format of the original image is irrelevant, as long as we can extract the color of each pixel.</b>
   
</br>


Each pixel on the screen has represented by 2 bytes.

The first is a bitwise OR number of green and blue, where green is first shifted 3 positions to the left

and blue 3 positions to the right

</br>
   


The second is a bitwise OR number of red and green, where red is bitwise AND with F8 and 

green is shifted 5 positions to the right

</br>


TMS320DM355ZCE allows us to update this screen at 60fps, but in the library I've set the write-timeout to 50ms. 

That would allow for atleast 20fps.


You'll still be able to reach 60fps without changing anything, I just put it the timeout at 50ms for good measure



