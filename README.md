# Flow Field for Zoom Whiteboard

## Files

- `flowfield.html`: the full page, meant to be hosted
- `embed-srcdoc.txt`: an iframe snippet with the HTML inlined, for pasting straight into the whiteboard

## Method A: paste directly (try this first)

1. Open `embed-srcdoc.txt` and copy the whole thing.
2. In Zoom Whiteboard, open More Tools, choose Embed Content, paste the snippet, and click Embed.
3. If the widget shows blank or Zoom rejects the snippet, Zoom does not support `srcdoc`. Switch to Method B.

## Method B: GitHub Pages

1. Create a new public repo on GitHub, for example `zoom-flowfield`.
2. Upload `flowfield.html` and rename it to `index.html`.
3. Go to Settings > Pages, set Source to `Deploy from a branch`, choose Branch `main` and `/ (root)`, then save.
4. Wait about one minute. The URL will be `https://<your-account>.github.io/zoom-flowfield/`.
5. Paste this into the whiteboard:

```html
<iframe src="https://<your-account>.github.io/zoom-flowfield/" width="800" height="500" style="border:0" allow="autoplay; fullscreen; clipboard-write"></iframe>
```

## Controls

- Move the mouse: creates a swirl
- Click: triggers a burst with a sound effect
- Space or the palette button: switches the color palette
- D or the diagnostics button: opens the environment diagnostics panel

## Reading the diagnostics panel

| Item | What it means |
|---|---|
| WebGL2 / WebAssembly | Both OK means a Unity WebGL build has a chance of running |
| fetch / WebSocket | Both OK means you can build multiplayer sync with your own backend |
| pointer / keyboard | Shows whether input is taken over by the whiteboard's own drag handling |
| audio | Click the canvas once before checking this; it should be `running` |
| localStorage / cookie | Whether local data can be saved |
| fps | Performance inside the whiteboard |
| origin | `null` or `about:srcdoc` means Method A was used |

WebSocket uses a public echo server for the test. A failure may mean that server is down rather than that Zoom blocked it, so retest before drawing conclusions.
