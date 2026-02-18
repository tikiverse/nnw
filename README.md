# nnw

Query NetNewsWire's local database from the command line.

```bash
# all unread articles
nnw

# today's unread
nnw -t

# last 3 days, including read
nnw --all -d 3

# starred only
nnw --starred

# filter to a single feed with fuzzy match
# (errors if multiple feeds match)
nnw -f "hacker news"

# filter for multiple feeds with fuzzy match
nnw -ff "tech"

# summary view, grouped by feed
nnw -s

# pipe to LLM
nnw -t --prompt "summarize" | claude
```

## install

```bash
cp nnw /usr/local/bin/
```

Requires macOS with NetNewsWire using local "On My Mac" account.

## flags

```
-t, --today       last 24 hours
-d, --days N      last N days
-f, --feed NAME   filter by feed (fuzzy match, can repeat)
-ff PATTERN       filter by feeds matching pattern
-s                summary format (grouped by feed)
--all             include read articles
--starred         starred only
--full            full content (no truncation)
--prompt TEXT     wrap output for LLM
--truncate        truncate content (if --prompt auto-enabled --full)
--format          json | markdown | summary
--limit N         max articles (default 100)
-l, --links       clickable terminal links
```

## config

Paths configurable via env vars (highest priority) or `$XDG_CONFIG_HOME/nnw/config`:

```
NNW_CONTAINER=/path/to/OnMyMac
NNW_DB_PATH=/path/to/DB.sqlite3
NNW_FEED_METADATA_PATH=/path/to/FeedMetadata.plist
NNW_SUBSCRIPTIONS_PATH=/path/to/Subscriptions.opml
```
