# Hyde Street

97 seconds, 1080 × 1080, 30 fps, with a procedural soundscape (no music). Authoritative source: `index.html`.

## Premise

A late-afternoon ride on the **Powell–Hyde** cable car, from Union Square over Nob Hill and
Russian Hill down to the bay, seen through one window of a Powell car. We sit on the west bench
of the enclosed cabin and look across the aisle through the east-side window, so the view is
always to the right of travel. The camera is bolted to the car. On a grade the street stays
parallel to the sill, and the whole world tilts: buildings lean, rooflines step and the horizon
slopes. A leather strap hangs plumb from the aisle rail, so it shows the tilt and swings at every
start and stop. The film ends on the Hyde & Beach turntable. Rotating the car pans the window
from the wharf across the bay to the Golden Gate at sunset, and the Ghirardelli sign comes on.

Why this line: the user suggested California or Powell. Powell–Hyde has the steepest grade in the
system (21% on Hyde), the Lombard crest with the crooked street and Coit Tower beyond, and the
Aquatic Park terminus with Ghirardelli. Its route also crosses California Street at the Nob Hill
crest, which gives the view down California to the Bay Bridge. The California line would lose
Russian Hill, Lombard and the waterfront.

Why the ending belongs to this subject: the turntable is peculiar to Powell cars. They are
single-ended, so operators push them around by hand at each terminal. Turning a side window
through 180° is the only move that shows Alcatraz, the Golden Gate and Ghirardelli, which sit
behind or ahead of a sideways view along Hyde.

## Passages (from `SHOTS`, the single timeline)

| Time (s) | Passage | What changes |
|---|---|---|
| 0–6 | Union Square | Held at the square: palms, the Dewey column and its Victory. Bell at 1.6, the grip takes the cable at 3.4 and the strap swings back. |
| 6–29.5 | Powell climb | Hotels with storefronts, awnings, fire escapes and HOTEL blade signs. Grade 1% → 17%, so the world rolls further block by block. Cross streets (Post, Bush, Pine) open downhill corridors to the Financial District. |
| 29.5–39 | California crossing | Level crossing at the crest (roll returns to zero). The view runs down California Street to the Bay Bridge; a California Street car climbs toward us and rings. |
| 39–44.5 | Powell descent | Over the crest at −12%; the strap swings forward. |
| 44.5–50.1 | Truck wipe | A box truck overtakes in the right lane and fills the window. Jackson Street (level) and the Powell→Hyde world switch happen under full cover at 47.6. |
| 50.1–55.5 | Hyde climb | Nook, the café at 1500 Hyde St on the Jackson corner: dark shopfront, warm windows, striped green awning, NOOK fascia, sidewalk tables and a parasol. Then Russian Hill Victorians with real projecting bays and bracketed cornices. |
| 55.5–65.2 | Lombard crest | Stopped at the top of the crooked block. Brick switchbacks, hedges and hydrangeas are below, houses step down both sides and Coit Tower stands on Telegraph Hill at the end. Three cars creep down the hairpins. At 60.9 a southbound Powell car passes close on the next track: open grip end with riders waving, round-topped windows, maroon dash. |
| 65.2–83.5 | The plunge | 21% down Hyde (the roll reverses to about −12°). Stepped houses, glimpses of the bay, sunset colour arriving. |
| 83.5–97 | Turntable | Stop at Beach, then a 180° turn from 85.2 to 94.0. The pan runs east → north → west: Beach St and the wharf, Hyde Street Pier with its three-masted square-rigger and paddle ferry, the cove and Alcatraz, the Golden Gate backlit with fog under the deck, then Ghirardelli, whose letters come on one by one from 90.6. Foghorn, gulls. |

## Design decisions

- **Camera as car.** World X east, Y north, Z up. The view axis is the car's right-hand
  horizontal. Grade pitches the car about exactly that axis, so pitch is an image roll
  (`toCam`, `setCam`). Pitch comes from the terrain height under two trucks 7 m apart, so it eases
  in and out of each grade. The strap is a damped pendulum driven by `accel(t)`, integrated once at
  load (`STRAP`). Its screen angle is swing plus roll.
- **Geometry, not backdrops.** Each segment is a small city of box buildings on block perimeters
  over a terrain function (`makeCity`, `drawBuilding`, `facadeDetail`). Faces are culled by facing
  and painted far to near. Near Victorians get real 3-sided bays and cornices as projected
  polygons, deferred until the whole front row has been painted (`defer`). Corridors down cross
  streets, stepped rooflines and the Lombard vista all come from this geometry rather than being
  drawn.
- **Compression.** Blocks along the route are about half size (film metres), and grades are real
  (1–17% on Powell, 21% on Hyde), so absolute heights are low (the Nob Hill crest is 29 m). The
  landmarks sit at art-directed distances so they read through a 53° window: Coit Tower 245 m,
  the Bay Bridge 470–560 m (and broadside) at California, the Golden Gate 700–830 m at the end.
  Bridge heights are scaled with the terrain. This is a postcard geography: the directions are
  right, the distances are not.
- **Window.** The shape comes from the inspected photographs: tall openings with rounded upper
  corners in varnished moulded frames, posts with a centre bead, a header rail, curved ceiling
  ribs, the small clerestory lights, a slatted bench, a maroon apron and a grab pole. The cabin is
  baked once into per-plate coverage and laid over the live view (`bakeInterior`, `laycabin`).
- **Covered switch.** The truck is built in the car's own frame (`truck`), so it never rolls
  relative to the sill. The world is skipped while `|trkOff| < 1.2` m (full cover). The pitch
  blends Powell→Hyde inside ±0.55 s of the switch.
- **Ink discipline.** Inks are yellow, orange, pink, blue and indigo. An early pass hazed
  everything toward a 4–5-ink horizon colour, and the far view printed as speckle at 1:1.
  Surfaces now take at most about three inks. Haze goes toward a two-ink `SKY.hz`. Far windows
  (>110 m) are one mark in one ink, and details beyond 200 m are dropped. Below the horizon, the
  sky gradient becomes a ground colour, so gaps in terrain never flash sky.
- **Light.** One golden-hour clock `GOLD(t)`: bright late afternoon → sun on the horizon at the
  bay → dusk at the Gate. Faces facing the low WSW sun get a warm lift, the others a cool
  overprint.

- **Passing cable car (artistic liberty).** Built in our car's frame like the truck (`passingCar`,
  `PASS`), moving at 4.2 m/s toward the rear. With right-hand running, a real southbound car would
  pass on the other side of the car, out of this window's view. The film puts it on our side on
  purpose.
- **Nook.** The corner lot north of the first cross street in the Hyde world stands in for Hyde &
  Jackson (`NOOK`, `nookFront`, `cafeTables`). Jackson itself is mostly elided under the truck, so
  the geography is compressed here too. The café's colours and signage are invented, not observed.

## References inspected

- Wikimedia Commons: *Cable-Car-Interior-San-Fran.jpg* (varnished ribbed ceiling, maroon
  bulkhead with an arched doorway, window frames with rounded upper corners). *INTERIOR VIEW TO
  REAR OF POWELL-TYPE CABLE CAR*, HAER CAL,38-SANFRA,137-25 (inward-facing wall benches, grab
  poles, clerestory deck, window proportions). *San Francisco Cable Car Passengers.jpg* (open
  grip section, curved iron brackets, the view out of the side).
- Wikipedia, Powell–Hyde line and the San Francisco cable car system: stop order, the 21% Hyde
  grade, car dimensions (27 ft 6 in × 8 ft), single-ended cars and turntables.
- Cable Car Museum, Powell car page: dimensions, paint schemes. No photographs were retrieved
  from there.
- Street order and landmark placement (Union Square's frontage on Powell, the Fairmont and the
  club at California, Lombard's eight hairpins between Hyde and Leavenworth, Ghirardelli between
  Larkin and Polk, Hyde Street Pier and its ships) are from general knowledge. They were not
  checked against a map in this session.

## Sound

Procedural, from the repo's sound kit (`tick` → `sTick`, `paper` → `paperSnd`). No music. The
ride sound is modelled on a user-supplied field recording (*Cable Car Big 19 making those cable
car sounds.mp3*, 57 s). It was analysed but not embedded, since the repo keeps outside recordings
out of the deliverable unless licensed and attributed. Measured in the recording:

- 77% of the energy sits in 100–300 Hz: a grinding roar peaking near 200 Hz.
- The roar's level swells by about ±45% at 0.15–0.7 Hz.
- Bright metallic clanks (1.5–8 kHz, about +4 dB over the bed) come about 2.2 per second at
  irregular intervals, often in pairs 25–50 ms apart.
- The bell's partials are at about 1.14, 2.0, 3.06, 4.27 and 5.6 kHz, and rings are about 0.45 s
  apart.

How the film models it:

- **Roar.** Band-passed noise at 200, 150 and 410 Hz, plus a narrow 202 Hz grind. Its level
  follows `speed(t)`, with a floor while the car stands (the cable keeps running), and a
  three-sine swell.
- **Track.** Every 12.5 m rail joint is hit by both axles of both trucks (1.2 m and 7 m apart),
  placed by distance `S(t)`: the clack-clack … clack-clack. Each hit is a low wheel thump, a short
  steel body and a 640 Hz ring. The grip thonks over the slot pulleys every 9.7 m. Loose metal
  clanks are low and dull (0.5–1 kHz), at 0.1 + 1.0·speed per second. The wheels sizzle on the
  railhead with speed, and the flange squeals through the Jackson curves (under the truck) and
  briefly on the plunge. An earlier version paired every clank with a 4.5–7 kHz noise tick,
  heard as light clicking; it was removed, and no transients above 4 kHz remain in the moving
  passages.
- **Bell.** Retuned to the measured partials and spacing.
- **Car events.** The grip clunks and ratchets at each departure, brakes squeal into each stop,
  and track-brake pulses sound on the plunge. The passing car brings its own panned roar, bell and
  clanks.
- **The world.** The truck's diesel pans with `trkOff`. The bay has herring gulls (a nasal "kyow" rising and falling through two formants, then a laughing run of short "ha" notes; the first version was a thin songbird-like chirp), lapping water, the
  turntable, neon ticks and buzz, and a foghorn.

In the moving passages the film's 100–300 Hz share is about 70% (the recording's is about 90% on
the same analysis). Measured (Firefox, `audio.mjs --twice`): 97.000 s, 48 kHz stereo, two cold
renders byte-identical. I −16.5 LUFS, LRA 5.4 LU, TP −1.20 dBTP, 0 clipped, correlation 0.24.
Nobody has listened to it; perceptual quality is unclaimed.

## Verification

- `verify.mjs`: seek is pure in t in Chromium and Firefox across 32 times, including shot
  boundaries.
- Sheets inspected: full coarse sheet at 3 s, the truck strip 44.6–51.0 at 0.4 s, the hero at
  60, the California hold at 36, and the turntable at 84–96.8. 1:1 crops were checked at 36, 60 and
  96.8.
- Render cost in Firefox is 55–150 ms per frame. Full Firefox render took 621 s.
- Delivered `out/hyde-street.mp4`: h264 1080×1080, 30 fps, 2910 frames, 97.00 s, AAC 48 kHz stereo;
  full error-gated decode passed. Muxed audio re-rendered with the recording-modelled sound.

## Remaining weaknesses

- Nobody has watched it at speed; pacing is judged from sheets. The Powell climb (23.5 s) may
  feel long.
- The Bay Bridge at California and the Golden Gate at the end read, but they are small (about
  90–120 px tall). A side window at this focal length can't make them large without more
  distance cheating.
- The crooked street is a thin band. From the car's eye height at the brow, the 27% block is
  almost edge-on; this is geometrically right, but it keeps the switchbacks small.
- Near hotel fronts still read as large simple planes. Blade signs are seen edge-on in the centre
  of the window, which is correct but means the letters are rarely readable.
- There are no people anywhere. Tourists at the turntable and pedestrians at Union Square would
  help scale and life.
- In the Hyde and wharf worlds, the west side of Hyde exists only near Beach, for the turntable.
- The clouds are subtle to the point of invisibility in several passages.
