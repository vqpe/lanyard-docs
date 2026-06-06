**LANYARD SUPPORT FAQ**


**GETTING STARTED**


# __How do I get monitored by Lanyard?__

Join the Lanyard Discord server. Your account gets picked up automatically once you're a member.



# __I joined but still get `user_not_monitored`. Why?__

Double-check that you're using your actual Discord user ID, not a message ID or server ID. Enable Developer Mode in Discord settings, right-click your profile, and select "Copy User ID". Make sure you're querying: `https://api.lanyard.rest/v1/users/YOUR_ID`



__What is the Lanyard API key for?__

The API key is only needed for K/V write operations and the `@me` route. Reading another user's presence publicly at `https://api.lanyard.rest/v1/users/USER_ID` requires no key.



**PRESENCE & DATA**



# __Why isn't my Spotify showing up?__

Check the pinned messages in the support channel first. Common causes: Spotify not linked to Discord, Spotify activity privacy turned off, or an intermittent gateway issue. If your status shows in Discord but not Lanyard, wait a bit.



# __Why are `banner` and `accent_color` always null?__

Discord doesn't send banner or accent color data over the gateway socket. Lanyard never receives it. A common workaround is storing those values manually in K/V.



# __Does Lanyard support Discord badges (Nitro, HypeSquad, etc.)?__

No. Lanyard has never returned badge data. For badges, use Dustin's API: `https://dcdn.dstn.to/profile/USER_ID`. It's an unofficial tool, not maintained by the Lanyard team, and has no guaranteed uptime.



# __Where do I get Discord profile banners via API?__

Dustin's API: `https://dcdn.dstn.to/banners/USER_ID?size=SIZE`. Lanyard does not expose banners.



# __What is K/V and how do I use it?__

K/V is key-value storage that lets you attach custom data to your Lanyard response. Use the Lanyard bot in the bot commands channel:

`.set KEY VALUE` stores a value

`.get KEY` retrieves it

`.del KEY` removes it

You can also set K/V via authenticated API requests. Results show up under the `kv` object in your Lanyard response.



# __What does `discord_status` return?__

One of four strings: `online`, `idle`, `dnd`, or `offline`.



**WEBSOCKET**



# __Should I use REST or WebSocket?__

WebSocket is strongly preferred for live data on a website. REST requires repeated polling. WebSocket pushes updates to you in real time. Use `wss://api.lanyard.rest/socket` and run `/socket` in the `kv-commands` channel for full setup instructions.



# __My WebSocket keeps disconnecting. Is that normal?__

Occasional disconnections are expected. You need to implement reconnection logic in your client. Send a heartbeat every 30 seconds as specified in the `heartbeat_interval` from the server's hello payload, and reconnect with backoff when the connection drops.



**DUSTIN'S API (dcdn.dstn.to)**



# __What is Dustin's API?__

A separate unofficial API maintained by Dustin (a Lanyard contributor). It exposes Discord profile data not available through Lanyard, including badges, banners, accent colors, connected accounts, and collectibles.

Profile: `https://dcdn.dstn.to/profile/USER_ID`

Banner: `https://dcdn.dstn.to/banners/USER_ID`

Docs: `https://dcdn.dstn.to/gist`



# __Is Dustin's API reliable enough to depend on?__

The maintainer describes it as not a guaranteed-uptime service. It works fine for personal projects. Don't build anything production-critical on it without a fallback.



# __Do I need to be in the Lanyard server to use it?__

No. It's a public API endpoint. Send a request with any Discord user ID.



**MISC**



# __How do I find my Discord user ID?__

Enable Developer Mode (Settings > Advanced > Developer Mode), then right-click your username and select "Copy User ID".



# __Can I self-host Lanyard?__

Yes. The official repo includes Docker instructions: `https://github.com/Phineas/lanyard#self-host-with-docker`. This lets you monitor users without requiring them to join a specific Discord server.



# __Where do I ask for help?__

Read the pinned messages in #support first. They cover the most common issues, Spotify problems especially. For questions about Dustin's API, use `https://dcdn.dstn.to/gist` as the reference.


written by [Aureal](https://aureal.dev/)
