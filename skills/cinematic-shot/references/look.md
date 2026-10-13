# Look recipes

These are the exact values behind the grade. They are written as CSS because CSS is the most direct way to describe them. Port them to whatever renderer you use. `ACCENT` is the product's single brand colour, used in every highlight. The examples use a warm red-orange (`oklch(0.66 0.21 28)`). Swap in the product's own accent, and shift the warm light's hue to match it.

## Stage

```css
background: #060607;            /* ink: never #000, never a wallpaper */
```

## Key light (a warm pool from above)

A full-frame layer above the product:

```css
background: radial-gradient(70% 60% at 50% -10%, oklch(0.55 0.14 30 / 0.12), transparent 70%);
mix-blend-mode: screen;
```

Use 0.12–0.16 alpha in the montage and about 0.08 behind the outro. You can move the light (for example `30% 0%`) for a shot on a separate surface, but keep the hue.

## Vignette

```css
background: radial-gradient(110% 85% at 50% 50%, transparent 45%, rgb(0 0 0 / 0.55) 100%);
```

## Glass (the product window)

```css
border-radius: 16px;            /* 20–24px for a standalone card on its own set */
background: <the app's dark chrome>;
box-shadow:
  inset 0 0 0 1px oklch(1 0 0 / 0.09),     /* hairline edge */
  inset 0 1px 0 oklch(1 0 0 / 0.12),       /* top highlight */
  0 60px 120px -30px rgb(0 0 0 / 0.8);     /* deep, soft lift */
```

A document or canvas inside it sits on its own shadow:

```css
box-shadow: 0 0 0 1px rgb(0 0 0 / 0.4), 0 20px 60px -10px rgb(0 0 0 / 0.6);
```

## Sheen (a sweep on every cut)

This is a 900 px wide, very tall band on the glass, rotated 18°. It starts about 0.6 s before each cut and travels about 300 px/s.

```css
background: linear-gradient(90deg,
  transparent,
  rgb(255 255 255 / 0.06) 45%,
  rgb(255 255 255 / 0.11) 50%,
  rgb(255 255 255 / 0.06) 55%,
  transparent);
mix-blend-mode: screen;
```

## Anamorphic flare (on every event)

The flare is drawn in screen space at the event's projected position. It has two layers, both using the screen blend:

```css
/* streak: 1800 × 6 px, centred on the event */
border-radius: 50%;
background: radial-gradient(50% 50% at 50% 50%, rgb(255 255 255 / 0.95), ACCENT 18%, transparent 70%);
filter: blur(2px);

/* core: 360 × 360 px */
border-radius: 50%;
background: radial-gradient(closest-side, rgb(255 255 255 / 0.55), ACCENT 30%, transparent 100%);
```

The strength is an impulse that decays over about 0.4 s. Peak values: streak opacity 0.55 and core 0.45 for a UI event. Scale the streak's width to 0.6 and the core to 0.45. For a resolve, use up to 0.7 strength with width 0.8. When events overlap, the strongest one wins. Never show two flares at once.

## Depth of field

Apply the blur to the layer *behind* the subject (the document or canvas), never to the subject:

| Shot | Background blur |
|---|---|
| Macro on a floating element (composer card, pill, switcher) | 2.5–3 px |
| Macro on a side panel, with the main canvas behind | 4 px |
| Medium shot where the action happens on the canvas itself | 0 |

## Content change (a blur dissolve)

```
old: opacity 1 → 0,  blur 0 → 14px,  translateY 0 → −20px
new: opacity 0 → 1,  blur 14px → 0,  translateY 24px → 0
```

Run it on an ease-in-out of 0.6–0.9 s. Bars or numbers interpolate their value over the same span. A colour change, such as grey text turning to the accent, mixes in oklch.

## Resolve ring

```css
width: 60px; height: 60px; border-radius: 50%;
border: 2px solid ACCENT;
```

Scale it from 0.4 to 3.4 on an ease-out expo over 0.8 s. Opacity goes from 0.8 to 0, linearly.

## Springs and timing

- Pop in: a spring with stiffness about 260, damping about 19, and a slight overshoot.
- A UI ease-out of about 0.3 s for panels and cards.
- Cursor moves take 0.4–0.9 s on a slight arc (a bend of about 0.1).
- Typing runs at 12–14 cps. The caret blinks at about 1.6 Hz while idle and stays solid while typing.

## Outro type

```css
/* one line, centred */
font: 600 66px/1.2 <the product's sans>;
letter-spacing: -0.035em;

/* feature name: bright gradient text */
background: linear-gradient(180deg, #ffffff 20%, rgb(255 255 255 / 0.62) 100%);
-webkit-background-clip: text; background-clip: text; color: transparent;

/* tagline */
color: rgb(255 255 255 / 0.5);
```

Words enter one at a time: blur 14 px → 0, translateY 16 px → 0, and opacity 0 → 1, over 0.9 s on an ease-out expo, staggered by 0.07 s.

## Logo lockup

The mark is about 168 px, with a 40 px gap to the wordmark. The wordmark is about 132 px, weight 700, tracking −0.05em, with the same gradient fill as the feature name. Put a faint bloom behind it:

```css
background: radial-gradient(46% 42% at 50% 50%, oklch(0.3 0.06 35 / 0.35), transparent 72%);
```

It does not move. Fade the whole frame to black over the last 1.5–2 s.

## Render

| Setting | Value |
|---|---|
| Resolution | 1920 × 1080; 3840 × 2160 for a master |
| Frame rate | 60 fps |
| Motion blur | 4 sub-frames per frame, 0.5 shutter (180°) |
| Grain | Light temporal luma noise (strength about 3 on ffmpeg's `noise` filter) |
| Legibility | Nothing below about 20 px of on-screen text at 1080p. Check it at 960 × 540. |
