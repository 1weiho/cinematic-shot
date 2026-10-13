# Shot list example

This is a 42 s film at 120 BPM (beat 0.5 s, bar 2 s), written in the abstract so it maps onto any feature. Replace each subject with the real piece of UI. Keep the rhythm, scales, and angles.

The story shape is:

1. A montage of the gesture: the user does 3–4 small things.
2. One cut to a second surface, where the user triggers the result.
3. The payoff, in the film's only wide shot.
4. A close-up on the result.
5. Copy, then the logo.

Magnification is relative to the UI at its native size. Drift is linear from the first value to the second over the whole shot. DOF is the blur on the layer behind the subject.

| # | Cut | Subject | Mag. | Yaw / pitch / roll | DOF | Action |
|---|---|---|---|---|---|---|
| 1 | 0.0 | The control that starts the flow (a toggle, a mode switch, a button) | 3.2 → 3.6× | +3→+2 / +4 / −0.5 | 3 px | The cursor arcs in and clicks at about 1.2 s. The control springs to its new state, with a flare on the click. |
| 2 | 3.0 | The UI's first response (a hint, a status pill, an empty state) | 3.5 → 3.7× | −2 / −3 / 0 | 3 px | It eases in about 0.3 s after the cut. Hold. |
| 3 | 5.0 | The first target on the main canvas | 1.5 → 1.7× | −4→−3 / +5 / −0.6 | 0 | Hover feedback appears, then a click. Something pops in on a spring. |
| 4 | 8.0 | The floating card or field that opens | 2.8 → 3.1× | +3→+2 / +3 / 0 | 2.5 px | Type a short line at 12 cps, then confirm. |
| 5 | 12.0 | The status element from shot 2, now changed | 3.8 → 4.1× | +2 / −2 / 0 | 3 px | A counter rolls and the label updates. Same subject as shot 2, but a different scale and the opposite angle. |
| 6 | 14.0 | A second, larger target | 1.7 → 1.9× | +4→+3 / +6 / +0.6 | 0 | A different gesture, such as a drag or a selection, then a pop. |
| 7 | 17.0 | The card or field again | 2.8 → 3.05× | −3→−2 / +3 / 0 | 2.5 px | Type and confirm with a shortcut. The key hint lights up. |
| 8 | 20.0 | A third, small target | 2.0 → 2.2× | +3→+2 / +4 / 0 | 2 px | A fast repeat of the gesture. Earlier results are visible in the frame, so the work accumulates. |
| 9 | 23.0 | A list or side panel | 1.85 → 2.0×, tilting down | +4 / +5 / −0.6 | 4 px | No cursor. Items update on their own, three pops a beat apart, each with a small flare. This shows scale beyond one screen. |
| 10 | 26.0 | A second surface (a terminal, a phone, another app) as its own card, with its light moved to one side | 1.4 → 1.55× | +4→+3 / +3 / +0.4 | — | Type the trigger with a block caret in the accent colour. The press lands about a bar before the payoff, followed by one line of output. |
| 11 | **30.0** (bar) | The whole window: the **only wide shot** | 1.1 → 1.2× | −3→−2 / +4 / −0.4 | 0 | **Payoff.** The cut lands with a camera shake. Results resolve about 0.7 s apart, each with a ring, a flare, and a blur-dissolve edit. Counters roll down to zero. |
| 12 | 33.0 | The single most improved thing | 2.4 → 2.6× | +3→+2 / +3 / 0 | 0 | Hold on the after state. |
| — | 35.0 | Black | — | — | — | Copy: the feature name in gradient, then the tagline dimmed. The words blur in one at a time. |
| — | **38.0** (bar) | Black | — | — | — | Hard cut to the still logo lockup. Fade to black from 40.2 to 42.0. |

## Why it works

- **Scale rhythm**: macro, macro, medium, macro, macro, medium, macro, medium, medium | set change | **wide** | close. Holding the wide shot back until the payoff makes it land like a release.
- **The angle flips** on almost every cut. Shots 2 and 5 share a subject, but they differ in scale and pitch sign, so the return reads as a new camera position.
- **The cut comes before the action.** Each shot has 0.3–1 s of settled drift before its gesture. The result holds for about a beat before the next cut.
- **The cursor has no continuity.** It reappears just off target at every cut, already moving. It changes shape with context, such as an arrow over chrome or a tool cursor over the canvas. It is hidden whenever the UI changes on its own.
- **A cut replaces each transition.** Moving to the second surface is a hard cut into the same dark room, so it reads as "meanwhile, over here."
- **The ending is quiet.** After the loudest moment, the film cuts to black for one line of type, then to a logo that does nothing at all.

## Camera numbers in practice

With a CSS-style perspective camera at `perspective: P` looking at a plane `dist` away, the magnification is about `P / dist`. At `P = 1800`:

| Magnification | `dist` |
|---|---|
| 4× | 450 |
| 3× | 600 |
| 2× | 900 |
| 1.5× | 1200 |
| 1.15× | 1560 |

A 10% push from 3.2× to 3.6× takes `dist` from 560 to 500.
