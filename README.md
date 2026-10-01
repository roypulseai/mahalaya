# Mahalaya

A single-file Mahalaya morning player. It opens the record automatically at **4:00 AM** on Mahalaya morning and plays *Mahishasuramardini*, with the vinyl turning while the sound is on.

Live site: <https://roypulseai.github.io/mahalaya/>

## What it does

- Counts down to 4:00 AM on Mahalaya morning, then plays.
- Calculates local sunrise (Kolkata default, or your own coordinates with one tap).
- Shows the Durga Puja Shashthi date and how many days remain.
- Adds a reminder to Google Calendar, Apple Calendar, or Outlook.
- Plays the Mahishasuramardini recording from YouTube, plus a Spotify album embed.

## The Mahalaya date

Published dates are in the `MAHALAYA_TABLE` inside `index.html` and cover 2026 through 2031:

| Year | Mahalaya |
| --- | --- |
| 2026 | 10 October |
| 2027 | 30 September |
| 2028 | 18 September |
| 2029 | 7 October |
| 2030 | 27 September |
| 2031 | 16 October |

For any year outside the table the page falls back to an astronomical new-moon calculation
and labels the date as an estimate. To keep it fresh every year, set `DATE_FEED` to a
CORS-enabled JSON endpoint returning either shape:

```json
{ "2027": "2027-09-30" }
```

```json
{ "2027-09-30": true }
```

From 15 April the page fetches that endpoint once, validates the value, and caches it in
`localStorage` under `mahalaya.date.v1`.

## Playing it

Tap the record once during the 4:00 AM–8:00 AM window. Outside that window, double-tap it
and confirm.

Browsers mute an autoplaying embed until the visitor interacts, so the video may start
silent. Press the speaker icon in the player to unmute.

Use **■ Stop** to end the sound and the rotation together. YouTube owns its own play/pause
control, so pausing there leaves the record turning; Stop stops both.

## Video source

The player is a plain embed iframe rather than the YouTube IFrame API. The API needs a real
page origin to talk to, which is why it broke with "video player configuration error" when
this file was opened from disk. A plain embed has no such requirement.

`YT_HOST` in `index.html` is the only place the video origin is spelled, so it can be
pointed somewhere else without touching any other code.

## Notes

- Everything is in `index.html`. There is no build step and no dependency.
- Shashthi, the first day of the public Puja, is 6 days after Mahalaya (`PUJA_OFFSET`).
- Background tabs throttle timers, so set the calendar reminder as your real alarm.

## Credits

Recording by Birendra Krishna Bhadra. Album art and playback stream from YouTube and
Spotify respectively.