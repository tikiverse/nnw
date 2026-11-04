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
--prompt TEXT     prefix output with TEXT for LLM piping (enables --full)
--truncate        truncate content (if --prompt auto-enabled --full)
--format          json | markdown | summary
--limit N         max articles (default 100)
-l, --links       clickable terminal links
```

## config (optional)

Works out of the box for NetNewsWire's iCloud account. Default container path:
```
~/Library/Containers/com.ranchero.NetNewsWire-Evergreen/Data/Library/Application Support/NetNewsWire/Accounts/2_iCloud
```

To use a different account, point `NNW_CONTAINER` at its folder in `~/.config/nnw/config`. Each account has its own folder under `Accounts/`, such as `OnMyMac` for local feeds:
```
mkdir -p ~/.config/nnw
echo "NNW_CONTAINER=$HOME/Library/Containers/com.ranchero.NetNewsWire-Evergreen/Data/Library/Application Support/NetNewsWire/Accounts/OnMyMac" > ~/.config/nnw/config
```

Run `ls ~/Library/Containers/com.ranchero.NetNewsWire-Evergreen/Data/Library/Application\ Support/NetNewsWire/Accounts` to see which accounts you have.

Settings can also be set as env vars, which take priority over the config file. You can override individual files too:
```
NNW_CONTAINER=/path/to/account/folder
NNW_DB_PATH=/path/to/DB.sqlite3
NNW_FEED_METADATA_PATH=/path/to/FeedSettings.db
NNW_SUBSCRIPTIONS_PATH=/path/to/Subscriptions.opml
```

`NNW_FEED_METADATA_PATH` also accepts a legacy `FeedMetadata.plist` from older NetNewsWire versions.
