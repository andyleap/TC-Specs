DS_HSD3268
```
 ______    ______   
|_   _ `..' ____ \  
  | | `. | (___ \_| 
  | |  | |_.____`.  
 _| |_.' | \____) | 
|______.' \______.' 
DecaSys Engineering
```

DCPU-16 Hardware Info:
    Name: HSD3268 - Hardware Sprite Display
    ID: 0x79FE3268, version: 0x1802
    Manufacturer: 0x4453456e (DecaSys Engineering)


Description:
    The HSD3268 is a 320x200 pixel color display compatible with the DCPU-16.
    The display is made up of 40x24 cells. Each cell displays one
    monochrome 8px by 8px pixel character out of 128 available. Each cell has its own
    foreground and background color out of a palette of 16 colors.
    
    In addition, the HSD3268 also has support for 64 8x8 sprites, which are 
    capable of rendering 3 colors and transparency.  Up to 64 sprite patterns can be loaded
    into the HDS3268, but this loading process does take short period of time,
    so be careful when you decide to load it.

Interrupt behavior:
    When a HWI is received by the HSD3268, it reads the A register and does one
    of the following actions:
    
    0: MEM_MAP_SCREEN
       Reads the B register, and maps the video ram to DCPU-16 ram starting
       at address B. See below for a description of video ram.
       If B is 0, the screen is disconnected.
    1: MEM_MAP_FONT
       Reads the B register, and maps the font ram to DCPU-16 ram starting
       at address B. See below for a description of font ram.
       If B is 0, the default font is used instead.
    2: MEM_MAP_PALETTE
       Reads the B register, and maps the palette ram to DCPU-16 ram starting
       at address B. See below for a description of palette ram.
       If B is 0, the default palette is used instead.
    3: MEM_MAP_SPRITE_REGS
       Reads the B register, and maps the sprite register ram to DCPU-16 ram starting
       at address B. See below for a description of sprite register ram.
       If B is 0, sprites are disabled.
    4: LOAD_SPRITE_PATTERNS
       Reads the 


Video ram:
    The LEM1802 has no internal video ram, but rather relies on being assigned
    an area of the DCPU-16 ram. The size of this area is 386 words, and is
    made up of 32x12 cells of the following bit format (in LSB-0):
        ffffbbbbBccccccc
    The lowest 7 bits (ccccccc) select define character to display.
    ffff and bbbb select which foreground and background color to use.
    If B (bit 7) is set the character color will blink slowly.
    

Font ram:
    The LEM1802 has a default built in font. If the user chooses, they may
    supply their own font by mapping a 256 word memory region with two words
    per character in the 128 character font.
    By setting bits in these words, different characters and graphics can be
    achieved. For example, the character F looks like this:
       word0 = 1111111100001001
       word1 = 0000100100000000
    Or, split into octets:
       word0 = 11111111 /
               00001001
       word1 = 00001001 /
               00000000
    

Palette ram:
   The LEM1802 has a default built in palette. If the user chooses, they may
   supply their own palette by mapping a 16 word memory region with one word
   per palette entry in the 16 color palette.
   Each color entry has the following bit format (in LSB-0):
       0000rrrrggggbbbb
   Where r, g, b are the red, green and blue channels. A higher value means a
   lighter color.
   

A message from Ola:
   Hello!
   
   It is fun to see that so many people use our products. When I was a small
   boy, my dad used to tell me "Ola, take care of those who understand less
   than you. Lack of knowledge is dangerous, but too much is worse". 
   Here at Nya Elektriska have we always tried to improve mankind by showing
   them the tools required to improve and reach their true potential.
   Together, you will wake up in time.
   
   - Ola Kristian Carlsson
