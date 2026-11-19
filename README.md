# `ws2812`
A library for controlling ws2812 RGB LEDs with the [Spade Hardware Description Language](https://spade-lang.org/).

## Usage
```
use ready_valid::Rv;
use ws2812::{Pixel, Request, Config, ws2812_output};
```
Then set your GPIO pin like this:
```
let (ready, ready_inv) = port();

let request = ...;

set ws2812_pin = entity ws2812_output(clk, rst, Rv())
```
If `ready == true`, you can start a new request. If `ready == false`, you should not change the request.

To set the color of 1 LED, first do `Request::SendPixel`, and then if `ready == true` while `request == Some(Request::SendPixel)`, set the requestto `Request::SendReset`.

To set the color of >1 LED, just do multiple send pixel requests before the reset. For example, if you had 3 LEDs:
```
SendPixel { pixel: first_led_pixel }
SendPixel { pixel: second_led_pixel }
SendPixel { pixel: third_led_pixel }
SendReset
```
Once `ready == true` while request is `Some(SendReset)`, you can either set the request to `None` or `Some(SendPixel)` to update the color(s).

## Examples
TODO

## Tests
TODO
# spade_ws2812
