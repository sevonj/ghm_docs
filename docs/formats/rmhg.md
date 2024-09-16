# RMHG

!!! note inline end ""
    __Games__
    [`K7`](/ghm_docs/games/K7)
    [`NMH`](/ghm_docs/games/NMH)
    [`NMH2`](/ghm_docs/games/NMH2)
    
    __Extensions__
    `.rsl`

    __Tools__  
    [No-More-RSL](/ghm_docs/tools/no-more-rsl)  


Grasshopper Archive format

```cpp
// Surface
// 32B little-endian
struct RMHGHeader {
  int8_t magic[4];          // 'RMHG'
  uint32_t num_resources;   // 
  uint32_t attr_ptr;        // 
  uint32_t version;         // 
  uint32_t off_stringtable; // 
};
```
## Versions

| Version | Games |
| ------- | ----- |
| 1062    | NMH   |
| 1063    | NMH   |

## String table

The string table is placed near the end.

```cpp
// String table header
uint32_t num_strings;
int32_t unknown;
int32_t flags;

// -- 4B pad / 16B alignment

// String pointers
int32_t off_string[num_strings]; // Offset is relative to table header

// -- 32B alignment?

// Null-terminated strings
// ..
```

On versions greater than 1040, string bytes are XOR'd with `0x8D`. 

