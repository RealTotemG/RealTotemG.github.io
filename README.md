# realtotemg.github.io

The portfolio site. One page, no build step, no dependencies.

## Putting it live

1. Make a new **public** repo named exactly `RealTotemG.github.io`. The name is
   not a suggestion. GitHub serves a user site only from a repo named after the
   account, and getting it wrong is the usual reason a Pages site 404s.
2. Drop `index.html`, `invenfloor.png` and the whole `shots/` folder in the
   root and push. The `shots/` folder matters: the Invenfloor section points at
   the four files inside it, and without them that part of the page is four
   broken images.
3. Settings, then Pages, then set Source to "Deploy from a branch", branch
   `main`, folder `/ (root)`.

A minute or two later it is at `https://realtotemg.github.io`. Every push
updates it.

## The hero is the real app

The big panel under my name is not a picture and it is not a copy. It is an
iframe of `realtotemg.github.io/Invenfloor/?demo`, which is the browser app
itself, opened on the made-up house.

It used to be a hand-written imitation: seven hundred lines of a second drawing
implementation in this file that had to be kept level with the app by hand, and
was not. The draw-order bug lived on in it for weeks after the app's own
`iso.js` was fixed, because nobody thinks to go and check the demo. A page that
frames the real app cannot be out of date with the real app.

Two things follow from that:

- **Pages has to be switched on for the Invenfloor repo as well**, not just
  this one, and the app has to be served at `/Invenfloor/`. Until it is, the
  page asks for the app, gets a 404, and quietly keeps showing `shots/plan.jpg`
  instead. Nothing breaks and nothing says "demo unavailable"; a visitor just
  sees a screenshot. That is deliberate, but it does mean the hero being a
  still picture is the sign that Pages is not on yet.
- **`?demo` is a flag in the app**, not in this page. It opens the made-up
  house instead of the profile screen and changes nothing else.

The frame is inserted after this page's own `load` event, so the portfolio's
first paint never waits on a second application's modules.

## What to edit

Almost everything worth changing is in one array near the bottom of
`index.html`, marked with a comment:

```js
const GAMES = [
  { name: "Cosmic Catcher", kind: "Idle / Story", tone: "#8b7cff", url: "",
    note: "Star catching, fragment mining, ..." },
```

`url` is the Roblox link. It is empty on both cards right now because I don't
have them. A card with no `url` renders fine and simply is not clickable, so
nothing on the page ever points somewhere wrong; fill them in and a "Play it"
link appears. `tone` is the stripe along the top of the card.

Two cards, not five. The rest of the catalog stays off here on purpose, and the
heading says so out loud: "two I am willing to put my name on". Speed Surge and
the others can join the list when they are worth the space, same shape as these.

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

The four Invenfloor screenshots live in `shots/` as ordinary JPGs:

    shots/plan.jpg      the floor plan with rooms drawn
    shots/room3d.jpg    the same room stepped into, in 3D
    shots/items.jpg     the items list, saved views, and two items ticked
                        for tagging
    shots/phone.jpg     the whole thing on a phone

They used to be base64 inside the HTML, which made one file that worked
anywhere and also made that file 406KB. Separate files are 53KB of HTML and
270KB of images the browser caches and can load in parallel, which is faster on
the connection that matters, a phone on cell data. Replacing a screenshot is
now dropping a file in, not regenerating the page.

To retake them, open the browser app, set the window to 1440 by 900, and take
each shot at device pixel ratio 2 so the text stays sharp on a retina screen.
Press Keep on the sample-data banner first or it sits across the top of every
one of them.

For GIFs, make an `assets/` folder and reference them normally:

```html
<img src="assets/drawing-a-room.gif" alt="Drawing a room and stepping into it in 3D">
```

Keep GIFs under about 5MB. A ten second loop of drawing a room and stepping
into it in 3D will do more work than any paragraph on this page.

## A custom domain, later

If you ever buy one, add a file called `CNAME` containing just the domain, and
point a CNAME record at `realtotemg.github.io`. Nothing else changes.
