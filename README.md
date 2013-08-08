Adafruit-TFT-for-Arduino-Due
============================

A patch to the Adafruit TFT Library to allow running on the Due

This patch is in no way authorized, recommended or endorsed by Adafruit.

The only connection to Adafruit is it is based on their great library for ILI982x display drivers dated 7-15-2013

To use this patch put the file TFTpatch in your libraries directory which should also contain the Adafruit_TFTLCD directory and apply it like this:

arduino-1.5.2/libraries$ ls

Adafruit_GFX  LiquidCrystal  SD  TFTLCD  TFTpatch

The patched library will expect the TFT Data Pins #0-7 connected to 
Due pins #33-40.

arduino-1.5.2/libraries$ patch -p0 -i  TFTpatch

The example sketches also will not run on the Due but for me adding this just below the #include statements solved the problem:
`#ifdef __arm__`

`#define PROGMEM /* empty */`

`#define pgm_read_byte(x) (*(x))`

`#define pgm_read_word(x) (*(x))`

`#define pgm_read_float(x) (*(x))`

`#define PSTR(x) x`

`#endif`
