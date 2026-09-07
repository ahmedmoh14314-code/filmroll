# Filmroll

Search films from the OMDb API, rate the ones you have seen, and keep a list
with your average rating and total watch time.

![Search results next to a film being rated](docs/screenshot.png)

This is the project where `useEffect` cleanup made sense to me. There are three
effects and all of them need it:

- **Search** aborts the previous request, so a slow response cannot overwrite
  the results for what you actually typed.
- **The tab title** shows the film name, and gets put back when you close it.
- **Escape** closes the details — the listener has to be removed, or every film
  you open leaves another one behind.

## Running it

```bash
npm install
npm start
```

## The look

Dark like a cinema, one red, no other colour. The header is a strip of film —
the sprocket holes along its top and bottom edges are a
`repeating-linear-gradient`, not an image:

```css
background-image: repeating-linear-gradient(
  to right,
  transparent 0 0.9rem,
  var(--ink) 0.9rem 2.1rem
);
```

Plain CSS throughout, no framework.

## Bugs I found and fixed later

- A `useState` named `Error` shadowed the built-in one, so `throw new Error()`
  threw a `TypeError` instead of my message.
- `onAddWatched` was passed as a prop but never called, so the star rating did
  nothing at all.
- OMDb sends runtime as `"148 min"`. Storing the string made the average come
  out as text glued together instead of a number.

## Not done yet

- The watched list is lost on refresh — it should go in `localStorage`.
- The fetch logic in `App` is long enough to be its own hook.
- No tests.

## Why it still runs on Create React App

Because that is what I learned it on, and moving it to Vite would hide the
thing this repo is actually for.

I read this project the way you read a dated notebook. The commit history runs
from the first `create-react-app` to the rewrite, and the two sections above —
the bugs I only found on a second pass, and the work still outstanding — are
the point of keeping it public. Porting it to a newer toolchain would leave a
tidier repo and a smaller record.

I work with current React tooling. This is where I started, kept as it was.
