# UE5.8 VR Light-Contact Hand Prototype Roadmap

## Purpose

Sequence the saved spec into a 1-2 week prototype path that proves whether visual-only hand contact is compelling enough to continue.

## Confirmed

- Unreal Engine 5.8.
- Controller-driven VR hands.
- Core surfaces: wall, table/table edge, flat panel.
- Visual-only contact response unless later scope explicitly expands.
- No grabbing, hand tracking, locomotion, multiplayer, full-body IK, Unity, or Fab packaging.

## Sequencing Logic

Verify the real Unreal setup first, then prove contact detection and a capped whole-hand visual response before spending time on finger posing. Only expand to table edges and polish once the simplest before/after improvement is visible.

## Phase 0: Editor Reality Check

- Outcome: The actual project setup is verified before interaction work starts.
- Why this comes now: It prevents Phase 1 from depending on assumptions about the hand rig or VR template.
- Included work: Verify actual Blueprint component hierarchy, hand mesh setup, AnimBP variables, and VR Preview behavior in the Unreal Editor.
- Excluded work: Contact response behavior, finger posing, edge handling, curved surfaces.
- Dependencies/blockers: UE5.8 project opens cleanly; VR Preview can run; hand mesh and animation path are inspectable.
- Risk: Existing hand setup may not expose the control points needed for later visual response.
- Gate: Baseline VR Preview works and the current hand/control/animation ownership is understood well enough to choose the first response path.

## Phase 1A: Contact Signal And Whole-Hand Response

- Outcome: One hand detects nearby simple surfaces and applies a capped visual-only whole-hand response.
- Why this comes now: It proves the core visual premise before adding finger complexity.
- Included work: Contact detection, debug visualization, response toggle, capped whole-hand visual offset/rotation, blend in/out.
- Excluded work: Finger response, detailed pose alpha, table-edge conformance, curved surfaces.
- Dependencies/blockers: Phase 0 confirms where visual hand transforms can safely be adjusted.
- Risk: Whole-hand response may feel disconnected from the controller if the cap/blend is wrong.
- Gate: Before/after footage on one wall or tabletop shows a visually understandable improvement without obvious hitches.

## Phase 1B: First Pose/Finger Alpha

- Outcome: If Phase 1A is promising, add one simple pose or finger-contact alpha to improve the illusion.
- Why this comes now: Finger response is useful only after the contact signal and whole-hand correction are proven.
- Included work: One lightweight hand-pose/finger layer driven by contact intensity.
- Excluded work: Per-finger surface solving, full conformance, authored pose tooling.
- Dependencies/blockers: Phase 1A must produce stable contact intensity and debug feedback.
- Risk: Finger posing may consume sprint time without improving the demo enough.
- Gate: Footage shows the pose alpha adds visible believability beyond whole-hand response alone.

## Phase 2: Surface Matrix Expansion

- Outcome: The same approach works across wall, tabletop, angled flat panel, and table edge.
- Why this comes now: The plugin idea depends on simple environment surfaces, not one ideal plane.
- Included work: Validate normal handling, pressing, sliding, retreat, and table-edge fallback.
- Excluded work: Arbitrary mesh support, dynamic objects, production API, cylinder/sphere unless ahead of schedule.
- Dependencies/blockers: Phase 1A must be stable; Phase 1B is helpful but not mandatory.
- Risk: Table edge may require a separate focused spec if fallback behavior is not convincing.
- Gate: The core surface matrix is demoable without severe clipping, popping, or frame hitches.

## Phase 3: Feel And Failure Hardening

- Outcome: The prototype survives common VR movement and contact failure cases well enough for demo capture.
- Why this comes now: The surface matrix will expose the actual failure modes.
- Included work: Tune smoothing, response caps, deep-penetration behavior, tracking jumps, grazing angles, and noisy normals.
- Excluded work: Physical collision solving, grabbing, production optimization.
- Dependencies/blockers: Surface matrix must be broad enough to reveal instability.
- Risk: Over-tuning to one scene or hand asset may hide generality issues.
- Gate: Slow-motion review shows no major jitter, broken hand shapes, extreme offsets, or lingering deformation.

## Phase 4: Prototype Decision Package

- Outcome: A short evidence bundle supports a continue/rescope/stop decision.
- Why this comes now: The sprint should end with a product and technical decision, not just an experiment.
- Included work: Before/after clips, surface clips, observed performance notes, strongest/weakest interaction notes, open risks.
- Excluded work: Fab planning, marketplace docs, plugin packaging, broad architecture.
- Dependencies/blockers: Phases 1A-3 must produce footage worth evaluating.
- Risk: The effect may work technically but not look valuable enough to pursue.
- Gate: Decide whether to continue the prototype, change the interaction model, or stop.

## Optional Stretch

Cylinder or sphere support only enters after Phase 2 is already convincing. It tests generality; it is not part of the first proof.

## Spec Candidates

- Table edge behavior spec, if edge fallback is not enough.
- Surface eligibility spec, before broader scene support.
- Hand asset/control spec, before supporting multiple rigs.
- Demo capture spec, if the footage becomes a portfolio or validation asset.

## Recommended Next Step

Start with Phase 0 in the editor: verify the real Blueprint hierarchy, hand mesh, AnimBP variables, and VR Preview behavior before choosing the Phase 1A response path.
