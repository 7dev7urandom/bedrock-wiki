---
layout: page
title: Block Model Materials [BETA]
parent: Documentation
---

# Block Model Materials [BETA]

| Argument     | Slot                                                                                          |
|--------------|-----------------------------------------------------------------------------------------------|
| opaque       | used for a normal block texture without an alpha layer. Does not allow for transparency or translucency. This material enables AO (ambient occlusion) for the block, reating shadows around and underneath it.                                                                      |
| alpha_test   | Used for a block like the vanilla (unstained) glass. Does not allow for translucency, only either fully opaque or fully transparent pixels. This material disables AO for the block. Removing those ugly shadows if you're making a non-full or decorative block.                               |
| blend        | Used for a block like stained glass. Allows for transparency and translucency (slightly transparent pixels). This material disables AO for the block. Removing those ugly shadows if you're making a non-full or decorative block. |
| double_sided |                                                                                               |
