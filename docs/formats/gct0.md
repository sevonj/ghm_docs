# GCT0

!!! note inline end ""
    __Games__
    [`K7`](/ghm_docs/games/K7)
    [`NMH`](/ghm_docs/games/NMH)
    [`NMH2`](/ghm_docs/games/NMH2)
    
    __Extensions__
    `.gct`
    `.bin`

    __Tools__  
    [DolphinTextureExtraction-tool](/ghm_docs/tools/dolphintextureextraction-tool)
    [NMH Reverse Scripts](/ghm_docs/tools/nmh_reverse_scripts)


Grasshopper texture file.

A very simple texture container. Contains a small header and data starting from 0x40.

```cpp
// Header

char magic[4] = 'GCT0';
int encoding;           // See enum Encoding below
short w;
short h;
// 4-byte null?
int unknown;            // Flags?

```

```cpp
/*
  Source:
  https://wiki.tockdom.com/wiki/Image_Formats
  These seem to match encodings used here, so it probably came from some
  nintendo-provided library.

  It is unclear which all encodings are used in the game or actually supported
  by the engine.
*/
enum Encoding {
    I4 = 0x00,
    I8 = 0x01,
    IA4 = 0x02,
    IA8 = 0x03,
    RGB565 = 0x04,
    RGB5A3 = 0x05,  // Used
    RGBA32 = 0x06,  // Used
    C4 = 0x08,
    C8 = 0x09,
    C14X2 = 0x0A,
    CMPR = 0x0E     // Used
}; 
```