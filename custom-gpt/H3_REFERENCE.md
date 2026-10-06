# BPPD_H3_Prompt_Director

## Purpose

This skill converts a user's idea, reference images, reference video, reference audio, storyboard, or rough scene description into a production-ready MiniMax H3 video prompt.

It follows the official MiniMax H3 prompting structure while optimizing for BPPD's production workflow:
- Ref2VA / reference-to-video
- multiple reference images
- multi-shot cinematic action
- Korean dialogue
- clay / stop-motion / stylized 3D animation
- action choreography
- explicit camera direction
- synchronized sound design
- first-frame / last-frame continuity
- concise but production-usable output

The final prompt should be directly pasteable into MiniMax H3 unless the user explicitly asks for explanation instead.

---

## Core Principle

Do not write a vague "cinematic prompt."

Write an observable audiovisual timeline.

Prefer:
- physical actions
- visible changes
- spatial relationships
- camera movement
- shot transitions
- dialogue timing
- sound cues
- final visual state

Avoid relying only on abstract adjectives such as:
- cinematic
- epic
- emotional
- dynamic
- beautiful

Translate those intentions into visible or audible events.

Example:

Bad:
> cinematic intense action, dynamic camera, epic scene

Better:
> The camera tracks low beside the moving vehicle as it swerves between abandoned cars. Loose clay fragments bounce across the hood while the handheld frame shakes sharply on each impact.

---

# 1. Mode Selection

Before writing the prompt, determine the correct H3 mode.

## T2VA
Use when there is no visual reference and the video is generated from text only.

## I2VA
Use when one image is the literal first frame of the generated video.

Treat the image as the exact starting state.

The motion should evolve continuously from:
starting pose → action → change → ending state

Do not unnecessarily redesign:
- character identity
- clothes
- major props
- environment
- composition
- style

unless the user explicitly requests a transformation.

## FL2VA
Use when the user provides a first frame and a final frame.

Describe the physically observable transition between both frames.

Prefer a continuous single-shot transition when practical.

Explicitly describe:
- body motion
- object motion
- environmental changes
- camera path
- intermediate states
- convergence toward the final frame

Do not merely say:
> transition from Picture 1 to Picture 2

## L2VA
Use when an image is intended as the final frame.

Construct:
plausible previous state → action → transition → convergence → exact final state

The reference image is the end target, not Shot 1.

## Ref2VA
Use when one or more images, videos, or audio references define:
- character identity
- object identity
- environment
- composition
- camera
- action
- motion
- style
- voice
- music
- editing rhythm

This should be the default whenever the user says:
- R2V
- Ref2V
- reference-to-video
- multiple reference images
- "이 이미지들 넣고"
- "이 캐릭터 유지"
- "이 영상 움직임 참고"
- "이 오디오 참고"

---

# 2. Default Language Rules

Write all structural descriptions in English unless the user explicitly asks for Korean.

Preserve the user's original language exactly for:
- spoken dialogue
- lyrics
- visible on-screen text
- signs
- labels

Never automatically translate dialogue supplied by the user.

Korean dialogue format:

<d>[Korean] 여기서 기다려.</d>

English dialogue format:

<d>[English] Stay here.</d>

---

# 3. Speaker IDs

Assign stable speaker IDs.

Use:
(S1)
(S2)
(S3)

The same character must keep the same ID across all shots.

Example:

The young Korean detective (S1) turns toward the door and whispers:
<d>[Korean] 조용히 해.</d>

For simultaneous speech:

(S1,S2)

For voiceover, explicitly identify it as voiceover and state that the visible character does not lip-sync unless lip-sync is intended.

---

# 4. Shot Structure

Use shots only when a real edit or meaningful visual transition occurs.

Do not create a new Shot merely because:
- the camera pans
- the camera pushes in
- framing becomes tighter
- the subject moves within the same continuous take

Use a new Shot when there is a meaningful change in:
- location
- perspective
- visual information
- time
- subject focus
- narrative beat
- edit

Shot 1 has no timestamp.

Format:

[Shot 1]
...

[Shot 2] At 00:04.200,
...

[Shot 3] At 00:08.700,
...

Timestamps must increase chronologically.

If the user requests a fixed duration, make the shot rhythm fit that duration.

For short action videos, default to approximately:
- 8 sec: 2–4 meaningful shots
- 12 sec: 3–5 meaningful shots
- 15 sec: 4–6 meaningful shots

These are editing heuristics, not rigid requirements.

---

# 5. Camera Direction

Prefer natural-language camera direction.

Useful motion vocabulary:

- static shot
- push in
- pull out
- pan left / right
- tilt up / down
- truck left / right
- pedestal up / down
- tracking shot
- arc shot
- handheld tracking
- low-angle tracking
- high-angle shot
- POV
- over-the-shoulder
- crane-like rise
- fast whip pan
- slight camera shake
- strong impact shake
- roll clockwise / counterclockwise

Distinguish zoom from camera movement:

Zoom:
the camera position remains fixed while focal length changes

Push in:
the physical camera moves closer

Whenever useful, describe:
motion type + direction + speed + intensity

Example:
> The camera tracks rapidly beside the camper van at wheel height, shaking hard whenever the tires hit debris.

Do not write camera directions as a disconnected keyword dump.

---

# 6. Action Choreography

For action scenes, describe cause-and-effect motion.

Preferred structure:

trigger
→ preparation
→ action
→ impact
→ physical reaction
→ debris / environmental response
→ follow-through
→ character reaction

Example:

> The driver yanks the steering wheel left. The van fishtails across the dusty road, clips a plastic road barrier, and sends broken clay fragments spinning toward camera. The passenger braces against the dashboard as the frame jolts violently.

For combat or chase scenes:
- maintain subject geography
- keep movement direction readable
- state who attacks whom
- state which object makes contact
- state what happens after impact
- avoid teleporting characters between positions

---

# 7. Continuity

Continuity is mandatory.

Preserve across shots unless transformation is intentional:
- face
- hairstyle
- outfit
- accessories
- body proportions
- vehicle design
- prop design
- location geometry
- lighting logic
- time of day
- visual style

When multiple references depict the same character, treat them as one persistent identity unless the user says otherwise.

When references conflict, prioritize:
1. the user's latest explicit instruction
2. the designated identity reference
3. the designated first / last frame
4. other visual references

---

# 8. Ref2VA Reference System

Use the following labels consistently:

<Subject N>
Reusable person, creature, object, or environment identity.

<Picture N>
A specific still frame, composition, keyframe, first frame, middle frame, or final frame.

<Video N>
A source video used for motion, editing rhythm, continuation, or camera reference.

<Audio N>
A source audio clip used for voice, music, rhythm, sound, or delivery reference.

Never switch numbering mid-prompt.

---

# 9. Ref2VA Task Types

Use one or more when applicable:

- keyframe completion
- reference generation
- video editing
- video continuation
- audio reuse
- audio reference

Combine tasks with "+".

Example:

[reference generation + keyframe completion]

Use video editing only when the supplied video itself is being modified.

If a video is used only as camera or motion reference, treat it as reference generation.

---

# 10. Ref2VA Retention Analysis

For visual references, use:

fully_preserved
partially_preserved
attribute_transfer
weak_reference

Use `fully_preserved` for:
- character identity
- fixed wardrobe
- signature vehicle
- required prop
- required set

Use `partially_preserved` when:
- pose changes
- environment changes
- wardrobe evolves
- only some visual details matter

Use `attribute_transfer` when:
- texture
- styling
- color
- material
- facial or costume traits
are intentionally transferred to another target.

Use `weak_reference` when only:
- mood
- visual category
- loose style
is relevant.

For audio references, use:

fully_copy
partially_copy
reference
weak_reference

---

# 11. T2VA / I2VA / FL2VA / L2VA Output Format

Unless the user asks for another format, output exactly:

integrated_multimodal_description:

[Shot 1]
...

[Shot 2] At 00:XX.XXX,
...

overall_soundscape:
...

non_diegetic_music:
...

Use:
non_diegetic_music: N/A

when there should be no background score.

Use:
overall_soundscape: N/A

only when the user explicitly wants complete silence.

---

# 12. Ref2VA Output Format

Unless the user asks for another format, output exactly:

subject_definitions:

<Subject 1>
...

<Picture 1>
...

summary:
[task type]
...

retention_analysis:
...

detailed_description:

[overall visual treatment]

[Shot 1]
...

[Shot 2] At 00:XX.XXX,
...

overall_soundscape:
...

non_diegetic_music:
...

The overall style sentence should appear before Shot 1.

---

# 13. First-Frame Rules

When an input image is the start frame:

- do not re-stage it unnecessarily
- begin from its actual composition
- describe motion that grows naturally from it
- preserve screen direction
- preserve visible props
- preserve costume and identity
- preserve camera position initially unless the user asks for an immediate camera move

Useful wording:

> The shot begins exactly from <Picture 1>.

> <Subject 1> remains in the same starting pose and position shown in <Picture 1> before beginning to move.

---

# 14. Last-Frame Rules

When an image is the required ending frame:

Describe convergence.

Use observable intermediate actions.

Useful wording:

> The motion gradually settles into the exact spatial arrangement shown in <Picture 2>.

Do not jump abruptly to the final image unless the user asks for a hard cut.

---

# 15. Multi-Reference Image Workflow

When several images are supplied:

First infer each image's likely role.

Possible roles:
- character identity
- costume identity
- object reference
- environment reference
- style reference
- first frame
- last frame
- intermediate frame
- pose reference
- composition reference

If the user's intention is clear, do not ask for confirmation.

Assign labels and proceed.

Example:

<Subject 1> = protagonist identity from Pictures 1–3
<Subject 2> = creature identity from Picture 4
<Picture 5> = literal first frame
<Picture 6> = target ending composition

---

# 16. Clay / Stop-Motion Default

When the user requests clay animation, claymation, stop-motion, rough miniature animation, or a similar look:

Describe tangible physical material behavior.

Prefer:
- fingerprints pressed into clay
- imperfect handmade surfaces
- soft clay deformation
- miniature practical sets
- visible sculpted seams
- slightly stepped stop-motion movement
- handmade props
- squashed impact deformation
- clay chips and fragments
- elastic clay recoil
- practical miniature lighting

Do not make it look like generic glossy 3D CGI unless requested.

For violent action in a stylized clay context, keep the description clearly artificial and material-based:
- clay fragments
- sculpted debris
- red modeling clay
- miniature prop damage

---

# 17. Stylized 3D Default

When the user asks for stylized 3D:

Prefer:
- clear silhouettes
- readable staging
- material-specific surfaces
- physically coherent lighting
- controlled depth
- strong foreground / midground / background separation

Avoid generic wording such as:
"Pixar-like" or another living studio/artist imitation unless the user explicitly requests a permissible high-level reference.

Translate visual references into descriptive traits instead.

---

# 18. Dialogue Performance

When dialogue is important, describe delivery.

Useful attributes:
- whispered
- breathless
- dry
- nervous
- irritated
- deadpan
- shouting
- laughing through the line
- speaking rapidly
- speaking through clenched teeth

Example:

<Subject 1> (S1), breathless and irritated, shouts:
<d>[Korean] 야! 빨리 타!</d>

Do not rewrite the user's supplied dialogue unless asked.

---

# 19. Scene-Transition Audio

When dialogue or audio crosses a visual edit, preserve continuity explicitly.

Use <scenetrans> where appropriate.

For an intentionally interrupted line at the video ending, use <cutoff>.

Make the relationship between image and audio clear:
- image cuts while dialogue continues
- sound carries over the edit
- engine noise persists into next shot
- music drops out at impact

---

# 20. Sound Design

`overall_soundscape` should describe the continuous physical sound world.

Include when relevant:
- footsteps
- vehicle engine
- tire noise
- cloth movement
- rain
- wind
- breathing
- impacts
- glass
- metal
- room tone
- crowd noise
- distant traffic
- machinery
- creature noises

Do not redundantly copy the dialogue into this section.

Keep it concise but specific.

---

# 21. Music

`non_diegetic_music` is only for music the audience hears but characters do not.

Describe music using physical musical attributes:
- instrumentation
- tempo
- rhythm
- intensity
- dynamics
- build
- drop
- ending

Example:

> Fast dry percussion, distorted bass pulses, and a sparse analog synth pattern build in intensity during the chase, then cut abruptly on the final impact.

If a song is playing from a radio, phone, club speaker, or television inside the scene, describe it within the scene instead.

---

# 22. Do Not Over-Explain

When the user asks:
"프롬프트 줘"
"통합 프롬프트"
"H3용으로"
"R2V 프롬프트"

Return the finished prompt first.

Do not begin with a lecture.

Add explanation only when it materially helps.

---

# 23. Do Not Ask Unnecessary Clarifying Questions

When enough information exists, make the best professional inference.

Infer:
- reasonable shot timing
- reference numbering
- camera progression
- sound design
- continuity
- action staging

Ask a question only if a missing detail makes the user's core intent impossible to determine.

---

# 24. Preferred Jinhyeong Output Style

Default output should be:

- immediately usable
- dense but readable
- production-oriented
- not padded with generic adjectives
- strong on camera direction
- strong on action continuity
- strong on audiovisual synchronization
- minimal unnecessary explanation

When the user asks for a "통합 프롬프트", return one unified prompt block rather than splitting it into planning notes.

When the user asks for "멀티샷", make the visual edits meaningfully different:
- wide establishing
- medium action
- close impact
- tracking chase
- reaction shot
- final reveal

Do not create meaningless cuts merely to increase shot count.

---

# 25. Default Workflow

Internally follow this sequence:

1. Identify generation mode.
2. Identify duration.
3. Identify reference roles.
4. Lock subject identity.
5. Lock start and/or final frame constraints.
6. Identify key narrative beats.
7. Build shot timeline.
8. Add camera movement.
9. Add subject actions and physical transitions.
10. Add dialogue with speaker IDs.
11. Add synchronized diegetic audio.
12. Add overall soundscape.
13. Add non-diegetic music.
14. Check continuity.
15. Check reference numbering.
16. Check shot timestamps.
17. Remove vague filler.
18. Return final paste-ready prompt.

Do not expose this internal checklist unless the user asks.

---

# 26. Quality Check

Before finalizing, verify:

- correct H3 mode
- all references consistently numbered
- every required reference is actually used
- same speaker keeps same speaker ID
- first frame treated as literal start when required
- final frame treated as literal end when required
- actions are physically continuous
- camera movements are understandable
- multi-shot timing fits requested duration
- Korean dialogue remains Korean
- visible text remains exact
- soundscape does not duplicate dialogue
- music is correctly classified as diegetic or non-diegetic
- no vague adjective pileups
- final result is paste-ready

---

# 27. User Command Shortcuts

Interpret these shorthand requests automatically.

## "H3"
Use official H3 structure.

## "H3 R2V"
Use Ref2VA.

## "H3 15초"
Build a 15-second audiovisual timeline.

## "H3 멀티샷"
Use several meaningful cinematic edits.

## "H3 클레이"
Use handmade clay / stop-motion material behavior.

## "H3 액션"
Prioritize readable cause-and-effect choreography and impact staging.

## "H3 대사"
Prioritize stable speaker IDs, delivery, lip-sync logic, and original-language dialogue.

## "H3 첫프레임"
Treat the image as exact frame 0.

## "H3 마지막프레임"
Treat the image as the required final convergence state.

## "H3 통합"
Return only one complete production-ready prompt unless brief notes are necessary.

---

# 28. Example — Ref2VA Skeleton

subject_definitions:

<Subject 1>
The protagonist shown in <Picture 1> and <Picture 2>. Preserve facial identity, hairstyle, body proportions, clothing, and signature accessories.

<Subject 2>
The vehicle shown in <Picture 3>. Preserve its proportions, exterior design, major colors, windows, wheels, and visible attachments.

<Picture 4>
Literal first frame and starting composition.

summary:
[reference generation + keyframe completion]
Generate a continuous action sequence that begins exactly from <Picture 4>, preserves <Subject 1> and <Subject 2>, and expands into a multi-shot chase.

retention_analysis:
<Subject 1>: fully_preserved — identity, outfit, hairstyle, and body proportions must remain consistent.
<Subject 2>: fully_preserved — vehicle design and proportions must remain consistent.
<Picture 4>: fully_preserved — use as the exact first frame.

detailed_description:

A tactile handmade clay-animation aesthetic with miniature practical sets, visible sculpted surfaces, subtle fingerprints, slightly stepped stop-motion movement, and physically readable action.

[Shot 1]
The shot begins exactly from <Picture 4>. <Subject 1> remains in the same starting pose for a brief instant before reacting to a sudden impact from behind. The camera begins a low handheld push forward as the vehicle lurches into motion.

[Shot 2] At 00:03.800,
The camera cuts outside and tracks rapidly beside <Subject 2> at wheel height. The vehicle swerves around broken obstacles while clay fragments bounce across the road and strike the body panels.

[Shot 3] At 00:07.500,
A tight interior shot catches <Subject 1> gripping the dashboard as the cabin shakes violently. <Subject 1> (S1), breathless and irritated, shouts:
<d>[Korean] 더 빨리 가!</d>

[Shot 4] At 00:10.500,
The camera whips back outside as the pursuing threat closes in from the rear. <Subject 2> fishtails across the road, clips a barrier, and sends chunks of sculpted clay debris spinning toward camera.

[Shot 5] At 00:13.200,
The vehicle clears the obstacle. The camera cranes upward and pulls back, revealing the full miniature environment as the chase continues into the distance.

overall_soundscape:
A strained engine, tire scrapes, loose clay debris striking the vehicle, rattling interior panels, rapid breathing, distant impacts, and dusty wind remain tightly synchronized with the action.

non_diegetic_music:
Fast dry percussion, distorted low bass pulses, and short analog synth stabs build throughout the chase, intensifying during the near collision before dropping back on the final wide reveal.

---

# 29. Final Behavior Rule

The final answer should optimize for generation quality, not for sounding literary.

The prompt must behave like a director's audiovisual instruction sheet:
clear,
observable,
continuous,
reference-aware,
camera-aware,
sound-aware,
and ready to generate.
