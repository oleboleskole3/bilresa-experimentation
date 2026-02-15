# IKEA Bilresa scrollwheel experimentation and possible reverse engineering / custom firmware

Having just purchased an IKEA bilresa remote, and being dissatisfied with it's zigbee compatability mode (and completely unable to pair to home assistant through matter), I've decided to try to make a custom firmware for the device


## IF ANYONE IS ABLE TO AQUIRE A FIRMWARE UPDATE FILE OR DUMP THE FIRMWARE ON THE DEVICE PLEASE LET ME KNOW


## IKEA matter network module

After disassembling the device, I discovered that the network processor sits on its own little board, likely IKEA reuses this board on other matter devices to reduce complexity whilst developing their products

![The IKEA network processor board from the front](media/network_board_front_1.png)
![The IKEA network processor board from the back](media/network_board_back_1.png)
![The IKEA network processor board from the front again](media/network_board_front_2.png)
![The IKEA network processor board from the back again](media/network_board_back_2.png)

The board measures in at about 8.5x10.5 mm
