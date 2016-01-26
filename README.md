# LED64x32

Propeller driver for the MI-T21P3RGBE-AB 64x32 RGB LED Module

## Links

Display: 
[https://www.adafruit.com/products/2279](https://www.adafruit.com/products/2279)

[https://learn.adafruit.com/32x16-32x32-rgb-led-matrix/](https://learn.adafruit.com/32x16-32x32-rgb-led-matrix/)

[https://learn.adafruit.com/32x16-32x32-rgb-led-matrix/connecting-with-jumper-wires](https://learn.adafruit.com/32x16-32x32-rgb-led-matrix/connecting-with-jumper-wires)

[https://web.archive.org/web/20121201205905/http://www.hobbypcb.com/blog/item/3-16x32-rgb-led-matrix-technical-details.html](https://web.archive.org/web/20121201205905/http://www.hobbypcb.com/blog/item/3-16x32-rgb-led-matrix-technical-details.html)

[http://www.starchips.com.tw/pdf/datasheet/SCT2026V03_01.pdf](http://www.starchips.com.tw/pdf/datasheet/SCT2026V03_01.pdf)

## Hardware

![](https://github.com/topherCantrell/LED64x32/blob/master/art/displayPinout.png)
![](https://github.com/topherCantrell/LED64x32/blob/master/art/quickstart.png)

![](https://github.com/topherCantrell/LED64x32/blob/master/art/harware.png)

I'm still tinkering to figure out the protocol. There isn't much on the web.

You have to strobe the display a row at a time over 16 rows. On each row you clock in 192 bits of data:
64 pixels x 3 bits each (RGB).

Actually you clock in two rows at a time. Instead of 3 bits RGB there are 6 bits RGBRGB. The other row is
on the second half of the display.

The row driver does not hold the LEDs on forever. I got a display routine running over a long loop. At the end
of the loop the OE remains on. You can see one very bright row (the last one being drawn) but it quickly
flashes off. The display thus behaves like a TV screen. You have to get back around to refresh the LEDs before
they "fade out".


