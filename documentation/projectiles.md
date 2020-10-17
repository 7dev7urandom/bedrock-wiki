---
layout: page
title: Projectiles
parent: Documentation
---

# Projectiles

<details id="toc" class="top-level" open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

This page intends to document all different fields you can use inside `minecraft:projectile` entity behavior component. 

*Disclaimer: this component has been mostly documented based on projectiles found in the game or reverse engineering the game.*

## Overview

| Name                      | Type             | Default Value | Description                                                                                                                                      |
|---------------------------|------------------|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| anchor                    | Integer          |               |                                                                                                                                                  |
| angle_offset              | Decimal          | 0             | Determines the angle at which the projectile is thrown                                                                                           |
| catch_fire                | Boolean          | false         | If true, the entity hit will be set on fire                                                                                                      |
| crit_particle_on_hurt     | Boolean          | false         | If true, the projectile will produce additional particles when a critical hit happens                                                            |
| destroy_on_hurt           | Boolean          | false         | If true, this entity will be destroyed when hit                                                                                                  |
| filter                    | String           |               | Entity Definitions defined here can't be hurt by the projectile                                                                                  |
| fire_affected_by_griefing | Boolean          | false         | If true, whether the projectile causes fire is affected by the mob griefing game rule                                                            |
| gravity                   | Decimal          | 0.05          | The gravity applied to this entity when thrown. The higher the value, the faster the entity falls                                                |
| hit_ground_sound          | String           |               | The sound that plays when the projectile hits ground                                                                                             |
| hit_sound                 | String           |               | The sound that plays when the projectile hits an entity                                                                                          |
| homing                    | Boolean          | false         | If true, the projectile homes in to the nearest entity                                                                                           |
| inertia                   | Decimal          | 0.99          | The fraction of the projectile's speed maintained every frame while traveling in air                                                             |
| is_dangerous              | Boolean          | false         | If true, the projectile will be treated as dangerous to the players                                                                              |
| knockback                 | Boolean          | true          | If true, the projectile will knock back the entity it hits                                                                                       |
| lightning                 | Boolean          | false         | If true, the entity hit will be struck by lightning                                                                                              |
| liquid_inertia            | Decimal          | 0.6           | The fraction of the projectile's speed maintained every frame while traveling in water                                                           |
| multiple_targets          | Boolean          | true          | If true, the projectile can hit multiple entities per flight                                                                                     |
| offset                    | Vector [a, b, c] | [0, 0.5, 0]   | The offset from the entity's anchor where the projectile will spawn                                                                              |
| on_fire_time              | Decimal          | 5             | Time in seconds that the entity hit will be on fire for                                                                                          |
| on_hit                    | Object           |               | Projectile's behavior on hit. More info [below](#on_hit)                                                                                         |
| particle                  | String           | iconcrack     | Particle to use upon collision                                                                                                                   |
| potion_effect             | Integer          | -1            | Defines the effect the arrow will apply to the entity it hits                                                                                    |
| power                     | Decimal          | 1.3           | Determines the velocity of the projectile                                                                                                        |
| reflect_on_hurt           | Boolean          | false         | If true, this entity will be reflected back when hit                                                                                             |
| semi_random_diff_damage   | Boolean          | false         | If true, damage will be randomized based on damage and speed                                                                                     |
| shoot_sound               | String           |               | The sound that plays when the projectile is shot                                                                                                 |
| shoot_target              | Boolean          | true          | If true, the projectile will be shot towards the target of the entity firing it                                                                  |
| should_bounce             | Boolean          | false         | If true, the projectile will bounce upon hit                                                                                                     |
| splash_potion             | Boolean          | false         | If true, the projectile will be treated like a splash potion                                                                                     |
| splash_range              | Decimal          | 4             | Radius in blocks of the 'splash' effect                                                                                                          |
| stop_on_hurt              | Boolean          |               |                                                                                                                                                  |
| uncertainty_base          | Decimal          | 0             | The base accuracy. Accuracy is determined by the formula uncertaintyBase - difficultyLevel * uncertaintyMultiplier                               |
| uncertainty_multiplier    | Decimal          | 0             | Determines how much difficulty affects accuracy. Accuracy is determined by the formula uncertaintyBase - difficultyLevel * uncertaintyMultiplier |

## on_hit

This object contains all behaviors, that can be executed, when projectile hits something.

### arrow_effect

*Exact behavior unknown*

### teleport_owner

Teleports shooter to the hit location.

### catch_fire

*Exact behavior unknown*

Sets target on fire

### ignite

*Exact behavior unknown*

Sets target on fire

### remove_on_hit

Removes the projectile when it hits something.

### douse_fire

*Exact behavior unknown*

### impact_damage

Deals damage on hit.

| Name                           | Type                             | Description                   |
|--------------------------------|----------------------------------|-------------------------------|
| damage                         | Integer/Integer Array [min, max] | Damage dealt to entity on hit |
| semi_random_diff_damage        | Boolean                          |                               |
| max_critical_damage            | Decimal                          |                               |
| min_critical_damage            | Decimal                          |                               |
| power_multiplier               | Decimal                          |                               |
| channeling                     | Boolean                          |                               |
| set_last_hurt_requires_damage  | Boolean                          |                               |
| destroy_on_hit_requires_damage | Boolean                          |                               |
| filter                         | String                           |                               |
| destroy_on_hit                 | Boolean                          |                               |
| knockback                      | Boolean                          |                               |
| catch_fire                     | Boolean                          |                               |

### definition_event

Calls an event on hit.

| Name               | Type    | Description                                         |
|--------------------|---------|-----------------------------------------------------|
| affect_projectile  | Boolean | Event will be triggered for projectile entity       |
| affect_shooter     | Boolean | Event will be triggered for shooter entity          |
| affect_target      | Boolean | Event will be triggered for hit entity              |
| affect_splash_area | Boolean | Event will be triggered for all entities in an area |
| splash_area        | Decimal | Area of entities                                    |
| event_trigger      | Object  | Event to trigger. Structure below.                  |

| Name    | Type   | Description         |
|---------|--------|---------------------|
| event   | String | Event to trigger    |
| target  | String | Target of the event |
| filters | Object |                     |

### stick_in_ground

Sticks the projectile into the ground.

| Name       | Type    | Description         |
|------------|---------|---------------------|
| shake_time | Decimal |                     |

### spawn_aoe_cloud

Spawns an area of effect cloud of potion effect.

| Name                | Type                    | Description                                                                |
|---------------------|-------------------------|----------------------------------------------------------------------------|
| radius              | Decimal                 | Radius of the cloud                                                        |
| radius_on_use       | Decimal                 |                                                                            |
| potion              | Integer                 | Potion ID [List](https://minecraft.gamepedia.com/Status_effect#Effect_IDs) |
| particle            | String                  | Particle emitter of the cloud                                              |
| duration            | Integer                 | Duration of the cloud                                                      |
| color               | Integer array [r, g, b] | Color of the particles                                                     |
| affect_owner        | Boolean                 | Is potion effect affecting the shooter                                     |
| reapplication_delay | Integer                 | Delay between application of the potion effect                             |

### spawn_chance

Spawns an entity on hit.

| Name                        | Type    | Description                                 |
|-----------------------------|---------|---------------------------------------------|
| first_spawn_percent_chance  | Decimal |                                             |
| second_spawn_percent_chance | Decimal |                                             |
| first_spawn_count           | Integer |                                             |
| second_spawn_count          | Integer |                                             |
| spawn_definition            | String  | ID of the entity to spawn                   |
| spawn_baby                  | Boolean | Whether the spawned entity should be a baby |

### particle_on_hit

Spawns particles on hit.

| Name          | Type    | Description                                     |
|---------------|---------|-------------------------------------------------|
| particle_type | String  | Particles to use                                |
| num_particles | Integer | Number of particles                             |
| on_entity_hit | Boolean | Whether it should spawn particles on entity hit |
| on_other_hit  | Boolean | Whether it should spawn particles on other hit  |

### mob_effect

Applies a mob effect to the target.

| Name           | Type    | Description                                 |
|----------------|---------|---------------------------------------------|
| effect         | String  | Effect                                      |
| duration       | Integer | Duration of the effect                      |
| durationeasy   | Integer | Duration of the effect on easy difficulty   |
| durationnormal | Integer | Duration of the effect on normal difficulty |
| durationhard   | Integer | Duration of the effect on hard difficulty   |
| amplifier      | Integer | Effect amplifier                            |
| ambient        | Boolean |                                             |
| visible        | Boolean |                                             |

### grant_xp

Spawns experience orbs giving a set amount of experience.

| Name  | Type    | Description                                                                                     |
|-------|---------|-------------------------------------------------------------------------------------------------|
| minXP | Integer | Minimum amount of experience to give                                                            |
| maxXP | Integer | Maximum amount of experience to give                                                            |
| xp    | Integer | Constant amount of experience to give. When set, it will be used instead of min and max values. |

### freeze_on_hit

*Exact behavior unknown*

Freezes water on hit.

| Name          | Type    | Description                          |
|---------------|---------|--------------------------------------|
| shape         | String  | "sphere" or "cube"                   |
| snap_to_block | Boolean | Maximum amount of experience to give |
| size          | Integer |                                      |

### hurt_owner

*Exact behavior unknown. Right now it crashes minecraft probably because of wrong parameters*

| Name         | Type    | Description |
|--------------|---------|-------------|
| owner_damage | Integer |             |
| knockback    | Boolean |             |
| ignite       | Boolean |             |

### thrown_potion_effect

*Exact behavior unknown. Right now it crashes minecraft probably because it's only valid for thrown potions*

