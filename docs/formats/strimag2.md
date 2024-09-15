# STRIMAG2

!!! note inline end ""
    __Games__
    [`K7`](/ghm_docs/games/K7)
    [`NMH`](/ghm_docs/games/NMH)
    [`NMH2`](/ghm_docs/games/NMH2)
    
    __Extensions__
    `.bin`

    __Tools__  
    \-

Grasshopper font format.

```yaml
# Ksy spec
meta:
  id: strimag2
  file-extension: bin
  encoding: shift-jis
  endian: be

seq:
  - id: magic
    contents: "STRIMAG2"
  - contents: [0, 0, 0, 0]
  - id: unk_0x0c
    type: u4
  - id: unk_0x10
    type: u4
  - id: unk_0x14
    type: u4
  - id: unk_0x18
    type: u4
  - id: unk_0x1c
    type: u2
  - id: unk_0x1e
    type: u2
  - id: font_name
    type: strz
    size: 64
    doc: | 
        Probs 64B. Can't be longer.
        Japanese encoding.
  - id: unk_0x60
    type: u4
```