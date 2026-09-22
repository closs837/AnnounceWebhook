# AnnounceWebhook

Watches Picarto for streamers going live and posts the announcement to a Discord channel
through a webhook — one webhook URL and creator list per server, checked every few
minutes.

```
python picartoAlertWebhooker.py
```

or with Docker:

```
docker compose up --build
```

## Configuration

Configuration lives in `webhooks.json`, next to the script:

```JSON
{
    "webhooks": [
        {
            "serverName": "Example",
            "roleIdToMention": "1234567890",
            "url": "https://discord.com/api/webhooks/...",
            "creators": ["CreatorOne"]
        }
    ]
}
```

| Field      | Purpose                                                                               |
| ---------- | ------------------------------------------------------------------------------------- |
| serverName | Used for logging and for keeping track of who has already been announced per server.  |
| roleIdToMention | Optional role to ping with the announcement. Leave it empty for no mention.       |
| url        | The Discord webhook URL for that server.                                              |
| creators   | Picarto channel names to watch.                                                       |

Streamers already announced are remembered per server and cleared once they go offline, so
the same channel is not announced twice in a row.
