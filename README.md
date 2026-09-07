# usePopcorn

Search movies from the OMDb API, rate the ones you have seen, and keep a list
with your average rating and total watch time.

![Search results next to a movie being rated](docs/screenshot.png)

This is the project where `useEffect` cleanup made sense to me. There are three
effects and all of them need it:

- **Search** aborts the previous request, so a slow response cannot overwrite
  the results for what you actually typed.
- **The tab title** shows the movie name, and gets put back when you close it.
- **Escape** closes the details — the listener has to be removed, or every
  movie you open leaves another one behind.

## Running it

You need a free OMDb key from https://www.omdbapi.com/apikey.aspx

```bash
npm install
cp .env.example .env.local   # put your key in it
npm start
```

## Bugs I found and fixed later

- A `useState` named `Error` shadowed the built-in one, so `throw new Error()`
  threw a `TypeError` instead of my message.
- `onAddWatched` was passed as a prop but never called, so the star rating did
  nothing at all.
- OMDb sends runtime as `"148 min"`. Storing the string made the average come
  out as text glued together instead of a number.
- The API key was sitting in the source. It is in `.env.local` now.

## Not done yet

- The watched list is lost on refresh — it should go in `localStorage`.
- The fetch logic in `App` is long enough to be its own hook.
- No tests.

---

A learning project from my React practice. Built with Create React App.
