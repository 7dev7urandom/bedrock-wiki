---
layout: page
title: Materials
parent: Concepts
---

# Materials

Expert
{: .label .label-red }

## Overview

Materials are used to specify the shaders that render the different parts of the game, along with states and settings the shaders should consider for each element.
At the moment, most things in the game are hard-coded to use a specific material and may not be assigned new ones. The only way to change how these elements are rendered is by editing their materials directly (potentially having unintentional effects on other elements), or by creating new shaders (an old experimental feature no longer officially supported by mojang). The only features that allow default or custom materials to be assigned or removed are entities and particles.


## Syntax and Structure

Most materials inherit the settings of previously defined materials, then further building off of them. This is written in the following format:

```json
    "<New material ID>:<ID of material to use as a base>": {
    	<defines, states, and other settings>
    },
```

**Notes:** Although it may look similar, do not confuse material format files in packs. There are no namespaces used in materials.

Some material files contain extensive branching trees of materials. For example, nearly all of the materials used by default entities are ultimately derivatives of the material "entity_static" in entity.material file. If we look at the material used by the current villagers,

```json
    "villager_v2_masked:entity_multitexture_masked": {
      "depthFunc": "LessEqual"
    },
```

we can see that the material's name is "villager_v2_masked", and that it builds off of the material named "entity_multitexture_masked".
Scrolling up in the file, we can find "entity_multitexture_masked" inheriting the settings from "entity_alphatest" and building further onto it:

```json
    "entity_multitexture_masked:entity_alphatest": {
      "+defines": [
        "MASKED_MULTITEXTURE"
      ],
      "+samplerStates": [
        {
          "samplerIndex": 0,
          "textureWrap": "Clamp"
        },
        {
          "samplerIndex": 1,
          "textureWrap": "Clamp"
        }
      ]
    },
```

"entity_alphatest" can then be followed to "entity_nocull"

```json
    "entity_alphatest:entity_nocull": {
      "+defines": [ "ALPHA_TEST" ],
      "+samplerStates": [
        {
          "samplerIndex": 1,
          "textureWrap": "Repeat"
        }
      ],
      "msaaSupport": "Both"
    },
```

which can be followed to plain "entity"

```json
    "entity_nocull:entity": {
      "+states": [ "DisableCulling" ]
    },
```

which can then finally be followed to "entity_static"

```json
    "entity:entity_static": {
      "+defines": [ "USE_OVERLAY" ],

      "msaaSupport": "Both"
    },
```

"entity_static" doesn't have a colon folowed by another material, indicating that it's the bottom of this inheritance tree.

```json
    "entity_static": {
      "vertexShader": "shaders/entity.vertex",
      "vrGeometryShader": "shaders/entity.geometry",
      "fragmentShader": "shaders/entity.fragment",
      "vertexFields": [
        { "field": "Position" },
        { "field": "Normal" },
        { "field": "UV0" }
      ],
      "variants": [
        {
          "skinning": {
            "+defines": [ "USE_SKINNING" ],
            "vertexFields": [
              { "field": "Position" },
              { "field": "BoneId0" },
              { "field": "Normal" },
              { "field": "UV0" }
            ]
          }
        },
        {
          "skinning_color": {
            "+defines": [ "USE_SKINNING", "USE_OVERLAY" ],
            "+states": [ "Blending" ],
            "vertexFields": [
              { "field": "Position" },
              { "field": "BoneId0" },
              { "field": "Color" },
              { "field": "Normal" },
              { "field": "UV0" }
            ]
          }
        }
      ],
      "msaaSupport": "Both",
      "+samplerStates": [
        {
          "samplerIndex": 0,
          "textureFilter": "Point"
        }
      ]
    },
```

## Useful custom material presets

A list of [material presets can be found here](/documentation/materials.html).
