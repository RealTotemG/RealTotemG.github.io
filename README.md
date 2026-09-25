# realtotemg.github.io

The portfolio site. One page, no build step, no dependencies.

## Putting it live

1. Make a new **public** repo named exactly `RealTotemG.github.io`. The name is
   not a suggestion. GitHub serves a user site only from a repo named after the
   account, and getting it wrong is the usual reason a Pages site 404s.
2. Drop `index.html` and `invenfloor.png` in the root and push.
3. Settings, then Pages, then set Source to "Deploy from a branch", branch
   `main`, folder `/ (root)`.

A minute or two later it is at `https://realtotemg.github.io`. Every push
updates it.

## What to edit

Almost everything worth changing is in one array near the bottom of
`index.html`, marked with a comment:

```js
const GAMES = [
  { name: "Cosmic Catcher", kind: "Idle / Story", tone: "#8b7cff", url: "",
    note: "Star catching, fragment mining, ..." },
```

`url` is the Roblox link. It is empty on every card right now because I don't
have them. A card with no `url` renders fine and simply is not clickable, so
nothing on the page ever points somewhere wrong; fill them in and a "Play it"
link appears. `tone` is the stripe along the top of the card.

Speed Surge is not in the list. Add a line for it the same shape as the others
when you want it there.

## The GitHub section fills itself in

Below the games there is a section that asks the GitHub API for your repos and
builds cards from whatever comes back, newest first, skipping forks and
anything already featured above. Push a new repo and it shows up here on its
own.

If that request fails for any reason, the section stays hidden and the rest of
the page is untouched. That is deliberate. An empty portfolio at the moment
somebody is deciding whether to take you seriously is the one failure worth
designing around, so nothing above that section depends on the network.

Two things to know. The API allows 60 requests an hour per visitor IP without
a token, which is far more than a portfolio will ever use, and you should never
put a token in a public page to raise it. And the preview version of this page
hosted on claude.ai cannot make that request at all, because published pages
there are not allowed to call other sites. It works on GitHub Pages.

## Screenshots and GIFs

The two Invenfloor screenshots are embedded directly in the HTML as base64, so
the page is a single file that works anywhere with nothing to break. For more,
or for GIFs, make an `assets/` folder and reference them normally:

```html
<img src="assets/drawing-a-room.gif" alt="Drawing a room and stepping into it in 3D">
```

Keep GIFs under about 5MB. A ten second loop of drawing a room and stepping
into it in 3D will do more work than any paragraph on this page.

## A custom domain, later

If you ever buy one, add a file called `CNAME` containing just the domain, and
point a CNAME record at `realtotemg.github.io`. Nothing else changes.
