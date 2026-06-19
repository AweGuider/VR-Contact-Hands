# AGENTS.md

## Project

Unreal Engine 5.8 VR prototype for procedural light-contact hand interaction.

## Current goal

Implement a small prototype where controller-driven VR hands visually react to simple non-grabbable surfaces such as walls, tables/table edges, and flat panels.

Use the spec at:

`docs/specs/vr-light-contact-hand-prototype-spec.md`

## Scope rules

- Do not implement grabbing, locomotion, weapons, hand tracking, multiplayer, full-body IK, Unity support, Fab packaging, or marketplace structure.
- Keep the prototype visual-first.
- Use Blueprint-first implementation for speed, but keep boundaries clean.
- Separate contact detection from visual hand response.
- Prefer small, reviewable changes.

## Before editing

First inspect the project structure, VR template setup, available hand assets, input setup, and relevant Blueprints.

Report findings before making implementation changes unless explicitly told to proceed.