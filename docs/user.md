# Fetching User Images

:::info
For most of these APIs, you can specify a `?size=` URL parameter, to get a specific size of that image, not all images have all sizes, generally, you can use `?size=4096` to get the biggest image available.
:::

Discord does not expose things like Badges, Banners, About Mes, Connections, and other things to the gateway, therefore, we need to use Dustin's API to fetch this.

> https://dcdn.dstn.to/profile/{userid}

Though lanyard still returns the Avatar, Avatar Decoration, Nameplate

> https://api.lanyard.rest/v1/users/{userid}
> wss://api.lanyard.rest/socket

See [Getting User Presence Data](#presence) for the REST endpoint, or [Working with WebSockets](#websockets) for live updates.

### Endpoints:
- Avatars: `https://cdn.discordapp.com/avatars/{userid}/{hash}.png`
    - Or: `https://dcdn.dstn.to/avatars/{userid}`
- Banners: `https://cdn.discordapp.com/banners/{userid}/{hash}.png`
    - Or: `https://dcdn.dstn.to/banners/{userid}`
- Avatar Decos: `https://cdn.discordapp.com/avatar-decoration-presets/{hash}.png`
    - Or: `https://cdn.discordapp.com/media/v1/collectibles-shop/{sku_id}/animated` - Can also replace "animated" with "static"
- Profile Decos: `https://discord.com/api/v9/collectibles-products/{sku_id}` - this then returns a json response with `src` fields of the different variants 
- Nameplates: `https://cdn.discordapp.com/assets/collectibles/nameplates/{collection}$/{name}$/asset.webm`
    - Or: `https://cdn.discordapp.com/media/v1/collectibles-shop/{sku_id}/animated` - Can also replace "animated" with "static"
- Profile Frames: `https://discord.com/api/v9/collectibles-products/{sku_id}` - returns similar json as the profile decos, you then have to contstruct the url as follows: `https://cdn.discordapp.com/media/v1/collectibles-shop/{sku_id}/{layer_id}/static`
- Badges: `https://cdn.discordapp.com/badge-icons/{hash}.png`
- Emojis: `https://cdn.discordapp.com/emojis/{id}.png`
- Guild Tag Icons: `https://cdn.discordapp.com/clan-badges/{serverid}/{hash}.png`
- Guild Tag Server: `https://discord.com/api/v9/guilds/{serverid}/profile` (Needs Authentication)
- Widget Image: `https://cdn.discordapp.com/widget-assets/{userid}/{file_id}?format=webp&animated=true` - theres a `"is_animated"` field so factor that in


Dustin's API returns the data pretty neatly, all you have to do is replace the placeholder `{}` text in above endpoints with what the API returns.

### Display Name Styles

Both APIs return a value called `display_name_styles` (`data.discord_user` in Lanyard, `user` in Dustin's API). It's `null` if the user hasn't set a style, otherwise it looks like `{ "font_id": 13, "effect_id": 1, "colors": [...] }`.

These are the fonts of each `font_id`:

| `font_id` | Style | Font | Download |
| :--- | :--- | :--- | :--- |
| `3` | Sakura | Cherry Bomb One | [Google Fonts](https://fonts.google.com/specimen/Cherry+Bomb+One) |
| `4` | Jellybean | Chicle | [Google Fonts](https://fonts.google.com/specimen/Chicle) |
| `6` | Modern | MuseoModerno | [Google Fonts](https://fonts.google.com/specimen/MuseoModerno) |
| `7` | Medieval | Néo-Castel | [Gumroad](https://maxlilllo.gumroad.com/l/neo-castel) |
| `8` | 8Bit | Pixelify Sans | [Google Fonts](https://fonts.google.com/specimen/Pixelify+Sans) |
| `10` | Vampyre | Sinistre | [Collletttivo](https://www.collletttivo.it/typefaces/sinistre) |
| `11` | gg sans | gg sans | [Unofficial mirror](https://i.alexflipnote.dev/a3LqePh.zip) |
| `12` | Tempo | Zilla Slab | [Google Fonts](https://fonts.google.com/specimen/Zilla+Slab) |
| `13` | Monkey Bars | Playpen Sans | [Google Fonts](https://fonts.google.com/specimen/Playpen+Sans) |
| `14` | Mainframe | Orbitron | [Google Fonts](https://fonts.google.com/specimen/Orbitron) |
| `15` | Headbang | New Rocker | [Google Fonts](https://fonts.google.com/specimen/New+Rocker) |
| `16` | Journal | Kalam | [Google Fonts](https://fonts.google.com/specimen/Kalam) |

gg sans is Discord's own font and has no official download.

### Badges

Both APIs return a value called `public_flags`, which can be used to perform __Bitwise Shift Operations__ to figure out what badges the user has.

But as this doesn't cover all badges, and doesn't provide the icon hash, it is preferred to just directly use the API.

| Value | Name | Description |
| :--- | :--- | :--- |
| `1 << 0` | `STAFF` | Discord Employee |
| `1 << 1` | `PARTNER` | Partnered Server Owner |
| `1 << 2` | `HYPESQUAD` | HypeSquad Events Member |
| `1 << 3` | `BUG_HUNTER_LEVEL_1` | Bug Hunter Level 1 |
| `1 << 6` | `HYPESQUAD_ONLINE_HOUSE_1` | House Bravery Member |
| `1 << 7` | `HYPESQUAD_ONLINE_HOUSE_2` | House Brilliance Member |
| `1 << 8` | `HYPESQUAD_ONLINE_HOUSE_3` | House Balance Member |
| `1 << 9` | `PREMIUM_EARLY_SUPPORTER` | Early Nitro Supporter |
| `1 << 10` | `TEAM_PSEUDO_USER` | User is a team |
| `1 << 14` | `BUG_HUNTER_LEVEL_2` | Bug Hunter Level 2 |
| `1 << 16` | `VERIFIED_BOT` | Verified Bot |
| `1 << 17` | `VERIFIED_DEVELOPER` | Early Verified Bot Developer |
| `1 << 18` | `CERTIFIED_MODERATOR` | Moderator Programs Alumni |
| `1 << 19` | `BOT_HTTP_INTERACTIONS` | Bot uses only HTTP interactions and is shown in the online member list |

(from https://discord.com/developers/docs/resources/user)
