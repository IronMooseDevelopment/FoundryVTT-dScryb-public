# dScryb

dScryb provides Boxed Text—descriptive text of places, monsters, spells, and other observations—meant to be read aloud by GMs to players. It is set in the world of epic fantasy, like many of your favorite RPGs. Good boxed text shows its subject by describing the sensory experience. And it often sets the narrative tone, introduces the scene, or spotlights what is important.

<a href="https://dscryb.com/ironmoose">https://dscryb.com/ironmoose</a>

[![](http://img.youtube.com/vi/p5D-bxJT0BU/0.jpg)](http://www.youtube.com/watch?v=p5D-bxJT0BU)

This is the official FoundryVTT module for dScryb, bringing you the wonderful boxed text dScryb provides in the same interface you expect from the site. All users gain access to over 250 pieces of free content. Paid members can login and gain access to their full subscription as well, with Heroes gaining access to over 1800 pieces of content.

<img src="https://i.imgur.com/bOUmEzs.png" alt="" width="1144" height="1034" />

## Macro API

The module exposes its API on `game.dscryb.api` for use in macros, scripts, and other modules.

### `playSfxByName(name, options?)`

Play a dScryb SFX track by its display name without needing its internal id.

```js
// Exact name, broadcast to all players at the current interface volume
await game.dscryb.api.playSfxByName("Sword Clash");

// Fuzzy substring match (default), play locally only at half volume
await game.dscryb.api.playSfxByName("dragon", { volume: 0.5, broadcast: false });
```

**Parameters**

| Name                  | Type      | Default                          | Description                                                                |
|-----------------------|-----------|----------------------------------|----------------------------------------------------------------------------|
| `name`                | `string`  | —                                | Track name to look up. Case-insensitive.                                   |
| `options.volume`      | `number`  | `core.globalInterfaceVolume`     | Playback volume in the range `0..1`.                                       |
| `options.broadcast`   | `boolean` | `true`                           | If `true`, plays on every connected client via socket; otherwise local-only. |
| `options.fuzzy`       | `boolean` | `true`                           | If `true`, falls back to a substring match when no track matches exactly.  |

Returns a `Promise<string|null>` resolving to the track's id, or `null` if no match was found or the matched track has no playable file. The user sees a UI warning in either failure case.
