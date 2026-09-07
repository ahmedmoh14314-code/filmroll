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

## What I would change

- The watched list is lost on refresh. It belongs in `localStorage`.
- The fetch logic in `App` is long enough to be its own `useMovies` hook.
- The details request has no `catch`, so a dropped connection leaves the
  spinner running with nothing to explain it.
- There are no tests.

The list of bugs above is the part of this repo worth reading. I wrote the
code, thought it worked, and only found them by going back through it — the
star rating had been dead the whole time and I had not noticed, because I had
never tried adding a film after building the button.

It still runs on Create React App because that is what I built it on, and the
commit history from the first `create-react-app` onward is more useful intact
than ported.

---

An early React project of mine. I build with Vite now.
