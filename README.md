# Bevy Kira audio

[![Crates.io](https://img.shields.io/crates/v/bevy_kira_audio.svg)](https://crates.io/crates/bevy_kira_audio)
[![license](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/NiklasEi/bevy_kira_audio/blob/main/LICENSE.md)
[![Crates.io](https://img.shields.io/crates/d/bevy_kira_audio.svg)](https://crates.io/crates/bevy_kira_audio)

This bevy plugin is intended to try integrating [Kira][kira] into Bevy. The end goal would be to replace or update `bevy_audio`, if Kira turns out to be a good approach. Currently, this plugin can play `.ogg`, `.mp3`, `.flac`, and `.wav` formats and supports web builds for everything except for `mp3`.

You can check out the examples directory in this repository for a display of this plugin's functionality.

## Usage
To initialize the corresponding `AssetLoaders`, use at least one of the features `ogg`, `mp3`, `wav`, or `flac`. The following example assumes that `bevy_kira_audio/ogg` is used.

```rust
use bevy_kira_audio::{Audio, AudioPlugin};

// in your game's AppBuilder:
// app.add_plugin(AudioPlugin)

fn my_audio_system(
    asset_server: Res<AssetServer>,
    audio: Res<Audio>,
) {
    let music_handle = asset_server.get_handle("sounds/music.ogg");
    audio.play(music_handle);
}
```

## Current state
- [x] play common audio formats
  - [x] `ogg`
  - [x] `mp3`
  - [x] `wav`
  - [x] `flac`
- [x] web support
  - The features `ogg`, `flac` and `wav` can be build for WASM. There are some differences between browsers:
    - Firefox: The audio might sound distorted (trying to figure out why)
    - Chrome: an interaction with the website is required before the AudioContext is started (e.g. a button click). Currently, the plugin cannot restart the AudioContext after an interaction.
- [x] pause/resume and stop tracks
- [x] play a track on repeat
- [x] control volume
- [x] control playback rate
- [ ] control pitch (no change in playback rate)
- [x] control panning
- [ ] get the current status of a track (time elapsed/left)?

## Compatible Bevy versions

The main branch is up to date with the latest Bevy release.

Compatibility of published `bevy_kira_audio` versions:
| `bevy_kira_audio` | `bevy` |
| :-- | :--  |
| `0.4.0` | `0.5.0` |
| `0.3.0` | `0.4.0` |

## License

This crate is distributed under the terms of the [MIT license](LICENSE.md).

Substantial parts of the asset loaders were taken from [Kira][kira] ([MIT license][kira-license] `Copyright 2020 Andrew Minnich`).

Assets in the examples might be distributed under different terms. See the [readme](examples/README.md#credits) in the `examples` directory.



[kira]: https://github.com/tesselode/kira
[kira-license]: https://github.com/tesselode/kira/blob/main/license.md
[rodio]: https://github.com/RustAudio/rodio
[oicana]: https://github.com/NiklasEi/oicana
[oicana-audio]: https://github.com/NiklasEi/oicana/blob/master/crates/oicana_plugin/src/audio.rs
