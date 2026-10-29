# Green Tome — catalogue images

The species images shown in the [Green Tome](https://github.com/CinzaApps/GreenTome) plant catalogue,
served by GitHub Pages at `https://cinzaapps.github.io/greentome-catalogue/`.

Images only. The catalogue data (names, indicators, watering seeds) ships inside the app; the
tooling that produces these files lives in the app repo under `tools/catalogue/`.

Plant images in the catalogue are AI-generated.

## Layout

| Path | Served | What |
|---|---|---|
| `docs/v1/<slug>.webp` | yes | 1024 × 1024 — the catalogue entry and the plant detail hero |
| `docs/v1/<slug>@256.webp` | yes | 256 × 256 — tiles, cards, thumbnails and avatars |
| `masters/<slug>.jpg` | no | The downloaded generation, kept as-is so a WebP can be re-encoded without generating again |
| `prompts/<slug>.md` | no | The exact prompt behind each master |
| `inbox/` | no | Drop folder for new generations, git-ignored |

Pages publishes from `/docs` on `main`, so `docs/v1/monstera-deliciosa.webp` is served as
`https://cinzaapps.github.io/greentome-catalogue/v1/monstera-deliciosa.webp`.

`<slug>` is the latin name in lower case with spaces as hyphens (`calathea-lancifolia`).

## Rules

- **Served paths are immutable.** A file under `docs/v1/` is never replaced in place — installed apps
  and their image caches rely on it. A regenerated image ships under a new version (`docs/v2/`)
  together with the app release that points at it.
- **Square only.** Every master is 1:1; nothing here is cropped or padded — the app frames the image.
- **The ground is `#F4F0E6`**, reset by `tools/catalogue/process` when a master is encoded.
- **Never `raw.githubusercontent.com`.** It is not a CDN and throttles hot-linking; the app loads from
  Pages only, with the base URL behind a Remote Config key.

## The anchors

`calathea-lancifolia` and `anthurium-andraeanum` were the first two approved generations. They are
catalogue entries like any other, and both are attached to every new generation as the style
reference for the pot, ground, light, angle and framing.
