# Roadster audio assets

`twilight-drive.mp3` is **Twilight Drive — Night Circuit**, an original instrumental dark synthwave track generated for this simulator with ElevenLabs Music v1 on 2026-10-17. The request uses `force_instrumental: true`: a confident 104 BPM driving groove with punchy electronic drums, gated snare, pulsing analog bass, minor-key cinematic chords and rhythmic arpeggios. The prompt requests original melodies and sounds, with no lyrics, vocals, quotations or samples of existing music. The exact prompt and generation metadata are in `music-generation.json`.

The generated source was trimmed to 101.538 seconds and edited into a **92.31-second repeating soundtrack**. A four-bar tail/head crossfade at the requested tempo joins the repeating groove, followed by a 32 Hz high-pass and -18 LUFS target normalization. The shipped stereo MP3 is 44.1 kHz / 160 kbps. Its measured sample peak is -5.91 dBFS. One new generation replaced the earlier lo-fi track; the original source remains outside the shipped assets. The music bus was raised modestly while preserving vehicle sound levels and output headroom.

Generation uses the [official ElevenLabs music endpoint](https://elevenlabs.io/docs/api-reference/music/compose). The API key was read only by a local development process. Runtime playback uses these local files and does not call ElevenLabs or require a key.

`gravel-loop.mp3` comes from the local **Free Racing and Driving Sounds** pack by moneywithjjcom, originally `gravel-loop.wav`. It was high/low-pass filtered and normalized to -22 LUFS, then encoded at 44.1 kHz / 128 kbps. This legacy asset is retained for provenance but is no longer loaded or played; its sharp transients sounded like footsteps. The pack's license is reproduced in `SFX-LICENSE.txt`. [Pack page](https://moneywithjjcom.itch.io/free-racing-sounds).

Rolling, tire slip, suction and rocket effects are synthesized locally with Web Audio. Rolling is a quiet, filtered low rumble that follows wheel speed and ground contact, with the same sound on pavement and terrain. It has no discrete gravel impacts, and its filter stays below 400 Hz at every speed to avoid a rising hiss. Suction is a steady filtered brown-noise blower with a low airflow body. It is silent at zero power and grows with the suction setting, including while parked or airborne. Its level and a broad 5 dB lift around 300 Hz keep it audible on small speakers beneath the radio; the low-pass stays below 800 Hz to avoid hiss. It does not use a narrow pitched vacuum tone.

Rocket sound follows the summed magnitudes of actual nozzle forces, including opposing attitude-control jets. A firing has a sharp 2 ms opening transient, turbulent low roar and irregular crackle; sustained thrust holds the roar, while release decays within roughly a tenth of a second. Button and assist flags alone cannot produce a rocket sound. Main supplies force averaged over the rendered frame so short physics pulses remain audible. Sources, filters and noise buffers are allocated once; firing only changes their envelopes. Mute and background transitions cancel pending attack transients.

There is no driving wind sound or whistle. A separate very quiet sine tone supplies electric drivetrain detail. There is no combustion-engine sample. The supplied wet-road loop was not used for the dry desert roads. The radio tracks are separate from all vehicle effects.

Sound is enabled by default after the first browser gesture. The Sound button mutes or restores music and vehicle audio together. The radio power button controls only the music. Hidden playback fades the mix to silence, while all station clocks continue advancing. Failed music loading leaves procedural vehicle sound working.

## Three-station radio

Five additional original instrumental tracks were generated with ElevenLabs Music v2 on 2026-10-17. They join Night Circuit in a six-track radio. Each station has two tracks and an independent randomized, locally persisted broadcast phase; retuning, radio-off, master mute and reloading preserve the advancing timeline. Songs overlap by 0.65 seconds at transitions. The game decodes music on demand, retaining at most four decoded songs and two simultaneous song voices. No radio track changes the driving simulation.

| Station | Track | Target BPM | Decoded duration |
| --- | --- | --- | --- |
| NEON FM | Night Circuit | 104 | 92.307 s |
| NEON FM | Glass Freeway | 112 | 94.407 s |
| ION RADIO | Orbital Rush | 124 | 92.918 s |
| ION RADIO | Phase Vector | 130 | 88.607 s |
| DUSK SIGNAL | Desert Satellites | 78 | 98.429 s |
| DUSK SIGNAL | Blue Hour | 86 | 89.313 s |

The new tracks use `force_instrumental: true` and original mood/instrumentation prompts. BPM values are composition requests, not verified tempo measurements. Exact prompts, generation identifiers and processing metadata are beside each file in `radio/*.json`. Local source responses are outside the public assets. `tools/generate-radio.py` reproduces the development workflow and reads the API key in memory; no key is saved into the game.

Each new track is high-pass filtered at 32 Hz and processed with two-pass -18 LUFS target normalization, -1.5 dBTP ceiling, 9 LU loudness-range target and short edge fades before 44.1 kHz stereo / 160 kbps MP3 encoding. Verification measured the new files at -18.21 to -18.45 LUFS with true peaks no higher than -1.78 dBFS. Short edge fades and radio crossfades avoid abrupt changes; the existing Night Circuit edit is preserved.
