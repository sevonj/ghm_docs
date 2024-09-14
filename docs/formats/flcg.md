# FLCG

!!! note inline end ""
    __Games__
    [`NMH`](/ghm_docs/games/NMH)
    [`NMH2`](/ghm_docs/games/NMH2)
    
    __Extensions__
    `.gcl`

    __Tools__  
    [NMH Reverse Scripts](/ghm_docs/tools/nmh_reverse_scripts)


FLCG models have static collisions, and are used for terrain and invisible walls in NMH open world. The format is way simpler than [GMF2](/ghm_docs/formats/gmf2). 

The file is big-endian.

FLCG Contents:

- Dummy Materials
- Models


ksy spec for this format: [flcg.ksy](https://github.com/sevonj/nmh_reverse/blob/master/lib/kaitai_defs/flcg.ksy)


## Header
```cpp
// FLCG header 28B (or more if there are unused values in the following null
// padding)
struct FLCGHeader {
  int8_t magic[4];         // 'FLCG'
  int32_t version;         // 1 (in Little-endian!), Probably version.
  int32_t unused;          // Probably unused.
  uint16_t num_models;     //
  uint16_t num_materials;  //
  uint32_t off_models;     // After materials?
  uint32_t off_materials;  // 0x40?
  int32_t unkwnown;        //
};
```

The version's endianness is probably the only exception in the file.

## Materials
Looks like the same format as [materials in GMF2](/ghm_docs/formats/gmf2/#materials), but the headers are mostly zeroed and there's no data. Maybe the data is pulled from the corresponding GMF2 file.

## Models

```cpp
// FLCG Model header
// 60B (or more if there are unused values in the following padding)
struct FLCGModel {
  int8_t name[8];       // Object name truncated to 8B. Shift JIS
  float unkf_0x08;      //
  int32_t unk_0x0c;     //
  int8_t zeropad[16];   //
  int32_t off_prev;     // Linked list
  int32_t off_next;     // Linked list
  float origin[3];      // XYZ position
  int32_t unk_0x2c;     // Always 0. Unused 4th component of previous vector?
  float unkf_0x30;      //
  int32_t unused_0x34;  // Always 0
  int32_t off_data;     //
};
```

```cpp
// FLCG Model data
// 40B
struct FLCGModelData {
  int off_data_a;       // Offset of unk. data. Immediately after this struct?
  int off_tris;         // Offset of triangles
  uint32_t num_data_a;  // Number of unknown data
  uint32_t num_tris;    // Triangles
  float unk_vec_a[3];   // These are probably a bounding box.
  float unk_vec_b[3];   //
};
```

```cpp
// FLCG Model data A
// 32B
struct FLCGModelDataA {
  int32_t off_firstchild;  // ?? Anyway, these form some kind of hierarchy.
  int32_t off_next;        // ?? Anyway, these form some kind of hierarchy.
  int32_t off_tri;         // Offset of a triangle.
  int32_t flags;           // Maybe
  float unk_vec[4];        // 4x unknown floats
};
```

Firstchild and next are just guesses.

```cpp
// FLCG Collision Triangle
// 48B
struct FLCGColTri {
  int32_t off_next;      //
  int32_t unused;        // Always 0?
  int32_t off_material;  //
  float v0[3];           //
  float v1[3];           //
  float v2[3];           //
};
```