

- Go to `editor.quickSuggestions` options in the `settings.json` file.
- Find the part of Markdown language and set the flags `comments` and `strings` to `true` or `on`

```json
"[markdown]": {
    "editor.quickSuggestions": {
        "other": true,
        "comments": false,
        "strings": false
    }
}
```