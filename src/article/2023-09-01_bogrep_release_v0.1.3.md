# Bogrep Release v0.1.3: Grep your bookmarks (decently fast)

As a bookmark hoarder, I often need to search through my bookmarks. Usually, I will find what I'm searching for just by using the browser search. Sometimes, I need full-text search on the website's content though to find some specific bookmark I added a while ago.

I'm already using

- [ripgrep](https://crates.io/crates/ripgrep) for full-text search in all my markdown files
- [ripgrep-all](https://crates.io/crates/ripgrep_all) for full-text search in LibreOffice documents and PDFs

Now you can also use [bogrep](https://crates.io/crates/bogrep) [3, 4] to grep through your bookmarks in full-text search.

Supported browsers are Firefox and Chrome. You can configure bogrep to import
some specific bookmark `--folders` from your browser:

```bash
# Configure bogrep to use bookmarks from Firefox for my_profile:
bogrep config --source ~/snap/firefox/common/.mozilla/firefox/<my_profile>/bookmarkbackups --folders dev,science,articles

# Import bookmarks
bogrep import

# Fetch and cache bookmarks
bogrep fetch

# Finally, grep through your bookmarks
bogrep <pattern>
```

Fetching of bookmarks is conservatively throttled for bookmarks from the same host. So that using bogrep shouldn't lead to any kind of rate limiting. You can configure the `request_throttling` yourself in the created `settings.json` file, placed at `~/.config/bogrep` in your home directory.
