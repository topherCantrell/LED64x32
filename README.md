# LED64x32

Propeller driver for the MI-T21P3RGBE-AB 64x32 RGB LED Module. There is limited information about these
displays. What I have found on the web -- and by tracing connections on the board -- is here.

## Links

Adafruit sells these displays. There are a variety of sizes and resolutions. Here is the
display I am using: 
[https://www.adafruit.com/products/2279](https://www.adafruit.com/products/2279)

[https://learn.adafruit.com/32x16-32x32-rgb-led-matrix/](https://learn.adafruit.com/32x16-32x32-rgb-led-matrix/)

[https://learn.adafruit.com/32x16-32x32-rgb-led-matrix/connecting-with-jumper-wires](https://learn.adafruit.com/32x16-32x32-rgb-led-matrix/connecting-with-jumper-wires)

Some very old related information in the web archives:
[https://web.archive.org/web/20121201205905/http://www.hobbypcb.com/blog/item/3-16x32-rgb-led-matrix-technical-details.html](https://web.archive.org/web/20121201205905/http://www.hobbypcb.com/blog/item/3-16x32-rgb-led-matrix-technical-details.html)

Datasheet from the manufacturer:
[https://www.adafruit.com/images/product-files/2279/MI-T21P3RGBE-AB%20p3.pdf](https://www.adafruit.com/images/product-files/2279/MI-T21P3RGBE-AB%20p3.pdf)

The display driver chip on the module:
[http://www.starchips.com.tw/pdf/datasheet/SCT2026V03_01.pdf](http://www.starchips.com.tw/pdf/datasheet/SCT2026V03_01.pdf)

## Hardware

The board has driver hardware for two pixel rows at a time. Each row is 64 cells. Each cell has a RED, a BLUE, and a GREEN LED in it.
3*64 = 192 LEDs per row. Two rows is 192*2 = 384 LEDs to drive at once.

![](https://github.com/topherCantrell/LED64x32/blob/master/art/back.png)

There are 24 LED driver chips along the top and bottom in the picture. The chips seem to be SCT2026 driver chips (see the link above).
Each chip can drive 16 LEDs. That's 24 * 16 = 384 LEDs.

There are 16 APM4953 chips down the middle of the picture. Each of these has 2 P-channel MOSFETs that feed the positive side of the LEDs. That's 
32 drivers. The driven LEDs share these drivers -- 12 LEDs to a MOSFET.

Near the left side of the picture (next to the input connector) there are 3 74245 chips. These boost/buffer the incoming signals. I was able to drive
the display from 3.3V GPIO pins.

The two other chips on the left side of the board are 74138. These are the row decoders. Together they generate 1 of 16 select lines. A single line
selects two rows at a time -- one in the top half of the display and one in the bottom half of the display.

The chip on the right side of the picture (next to the output connector) is a 74123 multivibrator chip. This chip feeds enable inputs on each of
the row decoder chips. After 4.6ms of inactivity the display is turned off until you start refreshing again (see circuit below).

I used a continuity checker and a scope to trace connections. Here is a basic system diagram I was able to deduce:

![](https://github.com/topherCantrell/LED64x32/blob/master/art/system.png)



![](https://github.com/topherCantrell/LED64x32/blob/master/art/displayPinout.png)