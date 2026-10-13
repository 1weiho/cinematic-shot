---
name: cinematic-shot
description: Shoot software UI like a film. A montage of hero shots, each a tight, near-frontal macro crop of the interface with a slow linear camera drift and shallow depth of field, hard-cut on the beat inside one dark, warmly lit room, ending on a line of copy and a still logo. Use when asked for a launch video, product film, feature trailer, teaser, promo clip, hero shot, or any "cinematic" footage of an app or UI. This skill covers camera, framing, light, and edit. It is stack-agnostic.
---

# Cinematic shot

You are the director and the DP, not the motion designer. The film is a sequence of **hero shots**. Each one is a tight, almost frontal crop of the product's UI. The camera drifts slowly, one thing happens, and a hard cut on the beat brings the next shot. Nothing explains itself with captions. The UI does the talking.

This skill is about camera, framing, light, and the edit. Build the film with any rendering stack. Whatever you choose, make every frame a pure function of time, so the film renders deterministically and can take motion blur.

Read [references/look.md](references/look.md) for exact grade, glass, flare, depth-of-field, and type recipes. Read [references/shot-list-example.md](references/shot-list-example.md) for a full example of the shot grammar.

## The taste

Dark room. One warm light from above. The product floats in it like a sheet of glass. The camera is close, closer than feels comfortable, so a single control, a single card, or a single line of text fills the frame. It never sits still and never moves much: a slow push of about 10%, with a degree or two of turn. Cuts land on the music. Each shot holds exactly one gesture, and its result stays up for a beat. One accent colour carries every highlight. Restraint everywhere else.

## 1. Find the story before the shots

Before planning a single camera, write down:

- **The gesture**: the 3–6 things the user physically does. Examples: flip a toggle, hover, type, drag, confirm, run a command.
- **The payoff**: the one moment where the product visibly changes something. The film exists to reach this frame.
- **The demo content**: concrete, believable data inside the UI, such as names, numbers, and short human-sounding text. The content should carry its own before/after, so the audience can *see* that the result is better without being told. A rambling sentence becomes a sharp one. A grey placeholder becomes a solid accent-coloured value.
- **One line of copy**: the feature name, then a tagline of five words or fewer.

## 2. Write the shot list

Post the shot list before building, then keep going:

| # | Cut at | Subject (what fills frame) | Scale | Action | Drift | Focus |
|---|---|---|---|---|---|---|

Rules:

- **Length**: 30–45 s at about 120 BPM (beat 0.5 s, bar 2 s). Montage shots last **2–3 s** (4–6 beats). A shot with typing can run to 4 s, but no single setup runs longer.
- **One idea per shot.** If two things happen, it is two shots.
- **Cut on the beat, and cut big moments on the bar.** The cut comes *before* the action. Let the shot settle for 0.3–1 s, perform the gesture, hold the result for about a beat, then cut.
- **Vary scale like an editor.** Macro dominates, and medium shots rarely come back to back. Save the only wide shot for the payoff, where it lands like a release.
- **Alternate the angle.** Flip the sign of yaw (or pitch) often, and always between two shots of similar scale. Every cut should read as a new camera position, not a jump. If you return to the same subject, change both scale and angle.
- **No continuity.** The cursor can be anywhere when a shot opens. Start it already moving, slightly off target, as if the action began before we cut in.
- **Separate sets for separate places.** When the story moves to another surface (a terminal, a phone, a second app), give it its own card in the same dark room and its own light position, then hard-cut to it. Do not use a transition.

### Shot scales

Measure scale as magnification of the UI relative to its native size:

| Scale | Magnification | Use for | Depth of field |
|---|---|---|---|
| Macro | 2.5–4× | A single control, a badge, a floating card, a line of typing | Blur the layer behind the subject by 2.5–4 px |
| Medium | 1.5–2.2× | A gesture that covers an area: hovering a block, dragging a region, a column of items | Sharp when the action is on the plane itself; 2–4 px when the subject floats above it |
| Wide | 1.1–1.2× | The payoff only, where many things change at once | Sharp |

Macro shots must stay crisp. Rasterise the UI at the resolution of the magnification (for example 2.5×) before the camera scales it. Never upscale a 1× bitmap.

### Camera drift

Each shot is one camera setup that interpolates **linearly** from a `from` pose to a `to` pose over its entire duration, and is cut mid-move. There is no easing, no keyframes inside a shot, and no handheld noise.

- **Push**: dolly in 6–12% of the camera distance over the shot. Pull-outs are rare.
- **Slide**: drift 20–60 px of UI sideways, usually along the reading direction of the action.
- **Turn**: start at yaw ±2–4°, pitch ±2–6°, and roll within ±0.6°, then drift about 1° toward frontal. Never go past about 6°. This is a near-frontal look. The tilt only hints that the UI is a physical plane.
- **Perspective**: use a long lens, which means low distortion. A perspective distance about the frame width (1500–1800 px at 1080p) works well.
- **Framing**: crop aggressively. Window edges, toolbars, and neighbouring panels run off the frame. The subject sits at centre or on a third, surrounded by near-black or soft-focus UI.

## 3. Light and grade: one dark room

Every shot must look like it was filmed in the same room. Values are in [references/look.md](references/look.md).

- **Stage**: near-black ink (`#060607`). Never pure black and never a gradient wallpaper.
- **Key light**: a soft, warm radial pool from above the frame, tinted with the accent hue at about 12–16% alpha, using a screen blend.
- **Vignette**: heavy and radial, about 55% black in the corners.
- **The product is glass**: rounded corners, a 1 px inner hairline at about 9% white, a 1 px top inner highlight at about 12% white, and a deep, soft drop shadow.
- **Luminance hierarchy**: dark chrome and bright content. A light document, canvas, or card inside a dark UI gives every shot a natural focal point.
- **Sheen on every cut**: a faint diagonal specular band sweeps across the glass, starting just before each cut, so every shot opens with light moving.
- **Anamorphic flare on every event**: clicks, things appearing, and completions each get a short horizontal streak with a hot core in the accent colour (screen blend, about 0.4 s decay). Keep it subtle, at 50–70% strength, and never a full-frame flash.
- **Finish**: motion blur (180° shutter, 4+ sub-frames) and light film grain on the final render. These two do more for "cinematic" than any effect.

## 4. Motion inside the shot

- **Cursor**: quick and decisive, 0.4–0.9 s per move on a slight arc. It arrives, acts, and moves off the subject so the result is never covered. Clicks dip the pointer and ripple.
- **Typing**: 12–14 characters per second, faster than real. Keep the text short.
- **Appear**: pop in on a stiff, well-damped spring with a slight overshoot, or ease out over about 0.3 s. Nothing fades in slowly during the montage.
- **Change**: content edits cross-dissolve *through blur*. The old state blurs to about 14 px and drifts up while the new state un-blurs into place. Values and bars move on a smooth ease-in-out.
- **Resolve**: when something completes, an accent ring expands from it and fades over about 0.8 s on an ease-out expo.
- **Impact**: the single biggest moment gets a short camera shake (amplitude about 0.15). Nothing else does.

## 5. Ending: copy, then a still logo

1. **Hard cut to black.** Set one centred line of about 66 px, weight 600, tracking −0.035em. The feature name has a bright vertical gradient (white to about 62% white). The tagline follows on the same line at 50% white. Words arrive one at a time, each un-blurring from about 14 px and rising about 16 px, staggered by about 0.07 s on an ease-out expo. Hold for about 3 s.
2. **Hard cut on the bar to the logo lockup.** The logo is completely still: no entrance, no drift, no pulse. A faint warm bloom sits behind it.
3. **Fade to black** over the last 1.5–2 s.

Add no CTA buttons, URL cards, or "available now" banners unless asked.

## 6. Sound

The music is cinematic, not a dance groove. Use one chord per bar in a minor key: a sub drone, felt piano, a ticking clock on eighths, a muted ostinato, and soft toms. It starts with the first shot (no intro) and builds in layers across the montage. Every cut gets a soft low tap, so the edit breathes with the music.

Every visible action gets a quiet, tactile cue: a click, a soft key thock per typed character, a glassy pop when something appears, and an airy whoosh on send. Before the payoff, a filtered string bed rises, then a breath of near-silence, then the payoff lands with a braam, a low boom, and the camera shake. Completions get glassy bells. Under the copy, hold one chord with two sparse piano notes. The logo lands on the bar with one heavy low hit that rings out under the fade.

## Don't

These make a film look like a tutorial or a template:

- Cold opens, title cards, or "Introducing…" and "New in…" screens before the action.
- Keycap overlays, captions, callout arrows, or labels that explain the UI.
- Dissolves or dips to black between montage shots. The montage uses hard cuts only.
- Slow orbits, big 3D rotations, swooping fly-throughs, or a camera that eases to a stop.
- Wide shots of the whole app during the montage. If the viewer has to search the frame, the shot is too wide.
- More than one action per shot, or a wandering cursor.
- Restyling the product's UI to look "cinematic". Keep the real UI faithful, and get the cinema from the camera and the light.
- An animated logo reveal.
- Several accent colours, gradient stages, or glow everywhere.

## 7. Verify like a DP

Render a still at the middle of every shot, at each action's peak, at the payoff, and at the copy and logo frames. Judge each one as a frame grab from a film:

- There is exactly one subject, and the eye lands on it in under half a second.
- The subject is sharp, the background is soft or dark, and the crop is hard.
- Text is legible at half resolution, and nothing important sits under the cursor.
- Consecutive shots differ in scale or in yaw sign.
- Every frame shares the same black level, light pool, and vignette.
- Pick the strongest frame as the poster.

Iterate until every still could be a screenshot in a launch post.
