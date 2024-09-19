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


Grasshopper Archive format.

An rsl header only describes a flat file system, but subdirectories are supported by packing them as archives into the archive. These nested subdirectory archives aren't fully independent as they share the root archive's string table. Sometimes pre-packed archives are packed into other archives as normal files.

```cpp
// File Header
// 20B
struct RMHGHeader {
  int8_t magic[4];             // 'RMHG'
  uint32_t num_resources;      //
  uint32_t off_resourcetable;  //
  uint32_t version;            //
  uint32_t off_stringtable;    // Zero in packed subdirectories.
};
```
## Versions

| Version | Games |
| ------- | ----- |
| 1062    | NMH   |
| 1063    | NMH   |
| 1069    | NMH2  |

This list is far from exhaustive.

## String table

The string table is placed near the end.

```cpp
// 12B little-endian
struct StringtableHeader {
  uint32_t num_strings;  //
  int32_t unknown;       //
  int32_t flags;         //
}

// -- 4B pad / 16B alignment

// String pointers
int32_t off_string[num_strings]; // Offset is relative to table header

// -- 32B alignment?

// Null-terminated strings
// ..
```

On versions greater than 1040, string bytes are XOR'd with `0x8D`. 

## Resource table

```cpp
  int32_t off_resource;  //
  int32_t len_resource;  //
  int32_t is_dir;        // Resource is a subdir. 0 or 1.
  int32_t version;       // Always same as root archive version?
  int32_t str_idx;       // Directory name in string table
```
