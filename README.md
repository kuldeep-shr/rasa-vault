# Rasa

A pocket museum for the music, books, web series and movies that moved you. Rasa is a single HTML file, with no build step, no backend and no account.

**Live demo:** [kuldeep-shr.github.io/rasa-vault](https://kuldeep-shr.github.io/rasa-vault/)

![Rasa showing four cards with title posters and Rasu the pet sitting on the dock](docs/screenshot.png)

## Features

- **Four shelves.** Music, Books, Web Series and Movies, each with its own colour and doodle wallpaper.
- **Flip cards.** The back of a card holds your note and a five-star rating you can tap.
- **Covers that keep their shape.** Album sleeves get a vinyl record, posters sit on a film strip, and books get a spine and pages. Nothing is cropped.
- **Photos your way.** Upload, paste or drop an image onto a card, or let Rasa look one up when you save. Anything without a photo gets a poster made from its title.
- **Rasu.** A small pet on the dock that follows your cursor, reacts to what you do and naps when you go quiet.
- **Share my shelf.** Turns the shelf you're looking at into a picture sized for Stories, with your six highest-rated cards and their covers, ready to share or save. It's drawn on your device.
- **Your curator card.** A name and a username for your museum, under the sign. Rasa makes up a username for you, like `@velvet.vinyl` or `@moonlit.matinee`, and you can change both any time. Your shared pictures are signed with them.
- **Search, Surprise me and Undo,** plus keyboard shortcuts: `/` to search, `N` to add, `R` for a surprise pick, `S` to share.
- Works on phones, supports the keyboard and respects reduced-motion settings.

## Run it

Open `index.html` in a browser.

For live reload while you edit:

```bash
npx live-server --port=5500
```

## Deploy

Rasa is one static file, so any static host works:

- **GitHub Pages:** Settings → Pages → Deploy from a branch → `main`, root folder.
- **Netlify or Cloudflare Pages:** upload the folder.

## Where data is stored

Everything stays in the visitor's browser: items, name and username in `localStorage`, and photos in IndexedDB. There is no server. Each visitor has their own vault, and clearing site data clears it.

## Visit counts

Rasa counts a few things with [GoatCounter](https://www.goatcounter.com), so the site owner can see how it's doing:

| Count | When |
| --- | --- |
| A visit | The page opens. Also records where the visitor came from and their screen size. |
| `joined` | A browser opens Rasa for the first time. |
| `added-movie`, `added-book`, `added-music`, `added-series` | Someone saves a new item. Only the shelf is sent. |
| `shared-shelf`, `saved-shelf` | Someone shares or saves a picture of their shelf. |

Only these plain numbers are sent. There are no cookies, and a title, note, name or username is never sent. Browsers that send Do Not Track or Global Privacy Control aren't counted.

To see which platform brings visitors, tag your links, for example `https://kuldeep-shr.github.io/rasa-vault/?ref=instagram`. GoatCounter lists each tag as a campaign.

Counting is off while `STATS.code` in `index.html` is empty, and it only runs on `STATS.host`. A fork counts nothing until you put in your own GoatCounter code and host.

## Photo lookup

When you save a new item without a photo, or press **Find photo** on the back of a card, Rasa searches once for cover art. It never searches while you type.

| Shelf | Sources, in order |
| --- | --- |
| Web Series | TVmaze, then the iTunes Search API |
| Music, Movies | iTunes Search API |
| Books | iTunes Search API, then Open Library |

Apple's search starts in your country's store and falls back to the US store. A result is used only when its name matches the title you typed, so a store that doesn't carry a title can't give you another one's cover. If nothing matches, Rasa makes a poster from the title.

Only the title and creator are sent, and only on that press. No API keys are needed. Images are resized to 1200px and stored in the browser. To turn lookups off, set `AUTO_PHOTOS = false` in `index.html`.

## Contributing

Issues and pull requests are welcome. The whole app lives in `index.html`: styles at the top, markup in the middle and the script at the bottom. Please keep it free of dependencies and build tools.

## Credits

Cover lookups use the [iTunes Search API](https://performance-partners.apple.com/search-api), [TVmaze](https://www.tvmaze.com/api) (data licensed CC BY-SA) and [Open Library](https://openlibrary.org/developers/api). The typeface is [Space Grotesk](https://fonts.google.com/specimen/Space+Grotesk).

## License

[MIT](LICENSE) © 2026 Kuldeep Sharma
