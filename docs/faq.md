# Where do I ask for help?

Read the pinned messages in #support first. They cover the most common issues, Spotify problems especially.
For questions about Dustin's API, use https://dcdn.dstn.to/gist as the reference.
And also make sure to check all of the below.
If none of these answer your question, feel free to ask in the #support channel.

---

## How do I get monitored by Lanyard?

Join the Lanyard Discord server. Your account gets picked up automatically once you're a member.
You will need to stay in this server to keep being monitored by Lanyard.



## How do I find my Discord user ID?

Enable Developer Mode (Settings > Advanced > Developer Mode), then right-click your username and select "Copy User ID".



## I joined but still get `user_not_monitored`. Why?

Double-check that you're using your actual Discord user ID (see above), not a message ID or server ID.
Make sure you're querying: https://api.lanyard.rest/v1/users/{YOUR_ID} (without the { })
You can test your ID directly in the playground on [Getting User Presence Data](#presence).



## What is the Lanyard API key for?

The API key is only needed for [K/V](#kv#getting-an-api-key) write operations and the `@me` route. Reading another user's presence publicly at https://api.lanyard.rest/v1/users/{USER_ID} requires no key.



## Why isn't my Spotify showing up?

Check the pinned messages in the support channel first.
Common causes: Spotify not linked to Discord, Spotify activity privacy turned off, or an intermittent gateway issue.
If your activity shows for yourself on your profile, it doesn't automatically mean that Lanyard can see it too, if it isn't picking it up, theres something wrong on your end 99.99% of the time.



## Why are `banner` and `accent_color` always null?

Discord doesn't send banner or accent color data over the gateway socket. Lanyard never receives it. A common workaround is storing those values manually in [K/V](#kv).



## Does Lanyard support Discord badges (Nitro, HypeSquad, etc.)?

No. Lanyard doesn't return badge data (except for [`public_flags`](#user#badges), though irrelevant). For badges, use Dustin's API: https://dcdn.dstn.to/profile/{USER_ID}. It's an unofficial tool, not maintained by the Lanyard team, and has no guaranteed uptime.



## What is Dustin's API?

A separate unofficial API maintained by Dustin (a Lanyard contributor). It exposes Discord profile data not available through Lanyard, including badges, banners, accent colors, connected accounts, and collectibles.

Profile: https://dcdn.dstn.to/profile/{USER_ID}

Banner: https://dcdn.dstn.to/banners/{USER_ID}

Docs: https://dcdn.dstn.to/gist



## Is Dustin's API reliable enough to depend on?

The maintainer describes it as not a guaranteed-uptime service. It works fine for personal projects. Don't build anything production-critical on it without a fallback.



## What is K/V and how do I use it?

[K/V](#kv) is key-value storage that lets you attach custom data to your Lanyard response. Use the Lanyard bot in the bot commands channel or in dms with the bot:

`.set KEY VALUE` stores a value

`.get KEY` retrieves it

`.del KEY` removes it

You can also set K/V via authenticated API requests. Results show up under the `kv` object in your Lanyard response.



## What does `discord_status` return?

One of four strings: `online`, `idle`, `dnd`, or `offline`.



## Should I use REST or WebSocket?

WebSocket is strongly preferred for live data on a website. REST requires repeated polling. WebSocket pushes updates to you in real time. Use `wss://api.lanyard.rest/socket`, for more info, see [Working with WebSockets](#websockets) or run `/socket` in the server for full setup instructions.



## My WebSocket keeps disconnecting. Is that normal?

Occasional disconnections are expected. You need to implement reconnection logic in your client. Send a heartbeat every 30 seconds as specified in the [`heartbeat_interval`](#websockets#connecting) from the server's hello payload, and reconnect with backoff when the connection drops.



## Can I self-host Lanyard?

Yes, see [Self-Hosting Lanyard](#self-hosting) for the Docker setup. This lets you monitor users without requiring them to join the Lanyard Discord server.




<small>written by [Aureal](https://aureal.dev/) @ 06/06/2026</small>
<small>improved by [schuh](https://schuh.wtf) @ 08/02/2026</small>
