# xcpcio/apps/board

[![Test](https://github.com/xcpcio/xcpcio/actions/workflows/test.yml/badge.svg)](https://github.com/xcpcio/xcpcio/actions/workflows/test.yml)
[![code style](https://antfu.me/badge-code-style.svg)](https://github.com/antfu/eslint-config)
[![GitHub release][gh-release-badge]][gh-release]
[![License][license-image-mit]][license-link-mit]
![Repo Size](https://img.shields.io/github/repo-size/xcpcio/xcpcio.svg)
[![jsDelivr](https://data.jsdelivr.com/v1/package/npm/@xcpcio/board-app/badge)](https://www.jsdelivr.com/package/npm/@xcpcio/board-app)

## Preview

- [board.xcpcio.com](https://board.xcpcio.com)
- [board-xcpcio.vercel.app](https://board-xcpcio.vercel.app/)

## Development

```bash
# Installation dependencies
pnpm install

# Run the development server
pnpm dev
```

## Local HOJ data

Contest requests under `/data/` are proxied to the local gksacm service at
`http://127.0.0.1:3000` during development and `vite preview`.
Start `F:\web_development\gksacm` with `pnpm dev`, then run the board with `pnpm dev`.

To use another address or the gksacm PM2 service on port 80, copy `.env.example`
to `.env.local` in this directory and set `BOARD_DATA_BASE_URL` to that service's
origin, for example `http://127.0.0.1:80`. Restart the board after changing it.

For a static production deployment, configure the web server to proxy `/data/`
to gksacm; the Vite proxy only runs during development and preview.

Medal counts follow each contest's HOJ configuration, read from
`GET /api/admin/contest?cid=...` using the OJ account configured in gksacm:

- `awardType=0` or no award configuration disables medals.
- `awardType=2` uses `awardConfigList[].num` as fixed counts.
- `awardType=1` calculates `floor(num * 0.01 * officialTeamCount)`. The official
  count comes from `POST /api/get-contest-rank` with `removeStar=true` and
  `containsEnd=false`, following HOJ's percentage calculation.

The first three tiers in ascending `priority` order map to gold, silver, and
bronze; zero-count tiers retain their position. HOJ's custom award names and
tiers after the third are outside this medal mapping. Index links open the
official group so starred teams do not participate in medal ranking.
HOJ contest settings are cached for up to one minute. The configured OJ account
must have permission to read the corresponding admin contest details.

## License

[MIT](../../../LICENSE) License © 2020 - PRESENT [XCPCIO][xcpcio]

## :clap: Our Supporters

### &#8627; Sponsors

This project is made possible by all the sponsors supporting my work:

<p align="center">
  <a href="https://github.com/sponsors/Dup4">
    <img src='https://cdn.jsdelivr.net/gh/Dup4/static/sponsors-output/sponsors.svg' alt="Logos from Sponsors" />
  </a>
</p>

### &#8627; Stargazers

[![Stargazers repo roster for @xcpcio/xcpcio](https://bytecrank.com/nastyox/reporoster/php/stargazersSVG.php?user=xcpcio&repo=xcpcio)](https://github.com/xcpcio/xcpcio/stargazers)

<br/>

<p align="center">
  <a href="https://github.com/xcpcio/xcpcio#">
    <img
      src="https://cdn.jsdelivr.net/gh/dup4/static/back-to-top-button.png"
      alt="Back to top"
      height="29"
    />
  </a>
</p>

[xcpcio]: https://github.com/xcpcio
[gh-release-badge]: https://img.shields.io/github/release/xcpcio/xcpcio.svg
[gh-release]: https://GitHub.com/xcpcio/xcpcio/releases/
[license-image-mit]: https://img.shields.io/badge/license-MIT-blue.svg?labelColor=333333
[license-link-mit]: https://mit-license.org/
