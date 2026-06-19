# UE5.8 VR Light-Contact Hand Prototype Spec

## Source Basis

OBSERVED: Prototype is for Unreal Engine 5.8, controller-driven VR hands, simple non-grabbable surfaces, visual-first procedural contact.

INFERRED: This sprint should prove the smallest convincing demo, not plugin architecture.

UNVERIFIED: Target headset, hand asset/skeleton, frame-rate budget, and exact UE5.8 API choices.

## Purpose

Define a 1-2 week Unreal Engine 5.8 VR prototype where controller-driven hands visually react to nearby static surfaces to reduce obvious clipping and improve perceived contact without requiring those surfaces to be authored as grabbable objects.

## Goals

- Demonstrate believable visual hand contact on a wall, table/table edge, and flat panel.
- Keep the controller transform as the input authority while allowing the visible hand/fingers to adapt.
- Support resting, pressing, sliding, and simple surface conformance.
- Require minimal surface setup, preferably normal collision/trace eligibility rather than grabbable components.
- Produce a short demo-quality result that helps evaluate whether the plugin idea is technically and commercially worth pursuing.

## Non-Goals

- No grabbing, distance grabbing, weapons, locomotion, hand tracking, multiplayer, full-body IK, NPC hands, Unity support, Fab packaging, or marketplace-ready plugin structure.
- No physical hand simulation or gameplay-authoritative collision solving.
- No generalized arbitrary-object interaction beyond simple static demo surfaces.
- No production animation tooling, pose editor, asset pipeline, or public API design yet.

## Desired Behavior

- Controller pose remains the source of truth for where the user's hand is trying to be.
- The visible hand may apply limited offsets, rotations, and finger pose blending to imply surface contact.
- When a hand nears an eligible surface, the palm and fingers blend into a contact response instead of snapping.
- When pressing into a surface, visual compression/intensity increases up to a capped maximum.
- When sliding tangentially across a surface, contact remains stable and follows the surface without jittery pose flipping.
- When leaving the surface, the hand smoothly returns to its normal controller-driven pose.
- Wall demo: palm/fingers visibly stop or flatten against a vertical plane rather than clipping through.
- Table demo: open hand can rest on a horizontal surface with fingers/palm adapting believably.
- Table edge demo: hand crossing or pressing near an edge should avoid large clipping and transition smoothly between top/side normals.
- Flat panel demo: behavior should work on a simple angled or vertical panel, not only world-axis planes.
- Optional stretch: cylinder or sphere should show basic normal-aware conformance, even if not polished.
- Debug visualization should be available for prototype validation: contact points, normals, active surface, and response intensity.

## Constraints

- Engine target is Unreal Engine 5.8.
- First input mode is controller-driven VR hands.
- First prototype target is visual or mostly visual response, not physical interaction.
- The prototype may use traces or collision queries to detect contact, but the contact response itself is visual-only unless a later decision explicitly expands the scope.
- Surface setup should stay lightweight: basic collision, trace channel, tag, material, or equivalent eligibility is acceptable; grabbable setup is not required.
- Prototype should prioritize one convincing player-hand interaction loop over broad system coverage.
- Hand visual correction must be capped so the rendered hand does not drift absurdly far from the controller.
- Contact blending must be smooth enough for VR comfort and must avoid sudden hand pops.
- Performance must be suitable for VR preview testing; expensive per-finger/per-frame surface work should be treated as suspect until profiled.

## Edge Cases

- Controller moves deeply through a wall or table.
- Hand approaches at a grazing angle.
- Fast controller movement causes contact detection to appear late.
- Multiple surfaces are close together, such as a table edge or wall-table corner.
- Surface normals flicker between adjacent triangles or edge faces.
- Thin panels are hit from the back side.
- Hand starts already intersecting a surface.
- Tracking/controller pose briefly jumps.
- No eligible surface is nearby.
- Left/right hand mirroring differs because of skeleton or asset setup.
- Finger poses become anatomically implausible under strong press values.
- Optional curved surfaces produce unstable normals or visible finger chatter.

## Assumptions

- A basic VR pawn/hand setup exists or can be created later as part of implementation.
- Minimum validation can focus on one representative hand, but the behavior should not be conceptually hard-coded to only one side.
- Demo surfaces are static meshes with reliable collision.
- Visual believability matters more than exact physical correctness.
- The first sprint should validate feasibility and feel, not finalize architecture.
- Long-term commercial/Fab goals remain background context only.

## Open Questions

- Which headset/runtime is the first target: Quest Link, SteamVR/OpenXR, or another setup?
- Which hand mesh, skeleton, and baseline animation pose will be used?
- Should the visible wrist/hand offset from the controller, or should only fingers adapt?
- What is the acceptable maximum visual hand offset before it feels disconnected?
- Is table-edge wrapping required for acceptance, or is "no obvious clipping with smooth fallback" enough?
- Should surfaces be eligible by collision channel, tag, physical material, or a prototype-only component?
- What frame-rate/per-frame CPU budget should define "acceptable" for the prototype?

## Observable Acceptance Criteria

- Given a non-grabbable wall with eligible collision, when the controller hand moves palm-first into it, then the visible palm/fingers settle against the wall with no large obvious clipping.
- Given the hand is in wall contact, when the controller slides parallel to the wall, then the contact pose follows smoothly without rapid snapping or normal flicker.
- Given a table surface, when the hand lowers onto it, then the palm/fingers visually rest or flatten against the tabletop.
- Given a table edge, when the hand moves across the edge, then the response changes smoothly and avoids severe finger/palm penetration.
- Given an angled flat panel, when the hand presses into it, then the contact response aligns to the panel normal rather than assuming world-up or world-forward.
- Given the hand moves away from any surface, then the visible hand returns to its normal controller-driven pose without lingering deformation.
- Given the controller penetrates too far into a surface, then the response caps gracefully without inverted fingers, extreme wrist offsets, or broken poses.
- Given no eligible surface is nearby, then hand visuals remain equivalent to the normal controller-driven pose.
- Given debug mode is enabled, then contact points, normals, and response intensity can be observed during play.
- Given contact response can be toggled on/off, when before/after footage is recorded on the same surfaces, then the improvement is visually understandable without technical explanation.
- Given the prototype is run in VR Preview, then normal interaction with the demo surfaces does not introduce visible frame hitches attributable to the contact system.

## Testing / Validation Ideas

- Test each surface with approach, rest, press, slide, retreat, and fast movement.
- Record short before/after clips with contact response disabled and enabled.
- Validate wall, tabletop, table edge, and angled panel as the core demo matrix.
- Add cylinder/sphere only after flat surfaces feel stable.
- Use debug normals/contact points to diagnose edge instability.
- Profile in VR preview during worst-case contact with both hands near surfaces.
- Stress-test deep penetration and tracking jumps to confirm graceful fallback.
- Review footage at normal speed and slow motion for clipping, popping, jitter, and unnatural finger shapes.
