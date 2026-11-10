# HelioField movies

[![GitHub stars](https://img.shields.io/github/stars/sr-dash/heliofield-movies?style=social)](https://github.com/sr-dash/heliofield-movies/stargazers)
[![Using it? Tell me](https://img.shields.io/badge/using%20it%3F-tell%20me-2ea44f)](https://github.com/sr-dash/heliofield-movies/issues/new?template=i_use_this.yml)
[![Show and tell](https://img.shields.io/badge/discussions-show%20and%20tell-8250df)](https://github.com/sr-dash/heliofield-movies/discussions/categories/show-and-tell)

Movies of the Sun since May 2010, one frame per Carrington rotation, with and without [HelioField](https://sr-dash.github.io/heliofield/)'s PFSS field lines. Free to use, for outreach and teaching too, with the credit given on the page.

**Watch and download:** https://sr-dash.github.io/heliofield-movies/

> [!TIP]
> **Using the movies?** Please [star the repository](https://github.com/sr-dash/heliofield-movies/stargazers) (the ☆ Star button at the top of this page). Downloads reach me without names, so a star is the only way I can tell who finds them useful, and it helps others find them too. Even better, [say what you use them for](https://github.com/sr-dash/heliofield-movies/issues/new?template=i_use_this.yml) in a two-minute form, or post an example in [Show and tell](https://github.com/sr-dash/heliofield-movies/discussions/categories/show-and-tell). I am not asking for money.

## What there is

- One movie per panel, 768 × 816: SDO/AIA 94, 131, 171, 193, 211, 304, 335 and 1600 Å, the SDO/HMI magnetogram and STEREO-A EUVI 195 Å (other beacon channels are left out, so its colour holds).
- Every panel on one 1920 × 1080 canvas, with the monthly sunspot number (WDC-SILSO) along the bottom and the frame's place in the cycle marked.
- Each with and without HelioField's PFSS field lines from HMI rotation maps, projected from each spacecraft's position.
- H.264 MP4 at 6 frames a second, a poster image each, `movies.json` listing them, and a video sitemap.

Each frame is the day of [HelioField imagery](https://github.com/sr-dash/heliofield-imagery) nearest the middle of its Carrington rotation, in the standard rendering. The field lines are drawn by HelioField's Observations page itself (`observations.html?frames=1`, which exposes `window.hfFrame`) in a headless Chrome, so they match the page; the movies keep their own line style (opacity 55 %, width 1×).

## Making them

```
pip install -r requirements.txt        # uses an installed Chrome, else `playwright install chromium`
python movies.py --work work --out site
python movies.py --page-only --out site   # only the gallery page and sitemap, from site/movies.json
```

`work/` keeps the rendered frames, so a later run only renders new rotations. `data/SN_m_tot_V2.0.csv` is a copy of WDC-SILSO's monthly sunspot numbers, used when SILSO is out of reach; without either the run stops rather than make the combined movies without their curve.

The `Movies` workflow runs on the 5th of each month: when a new rotation has been added to HelioField imagery (`--if-new`), it renders every frame afresh, encodes the movies and replaces the `site` branch, which GitHub Pages serves. Run it by hand with "force" to remake them anyway. The movies have their own repository so that their 270 MB is not redeployed with every day of images.

## Branches

- `main`: the code and workflows.
- `site`: the published movies, posters and gallery page, as served. It is a single commit with no history, replaced whole by the workflow on each update, so the repository stays the size of what is on show instead of keeping every old file. It shares no history with `main` (GitHub calls them diverged) and is never merged into it; ignore any "Compare & pull request" banner for it.

## Credits

Images: NASA/SDO and the AIA and HMI science teams; NASA STEREO/SECCHI. Field: HelioField PFSS from HMI rotation maps. Sunspot number: WDC-SILSO, Royal Observatory of Belgium. Please also cite [HelioField imagery](https://doi.org/10.5281/zenodo.23935774) and [HelioField](https://doi.org/10.5281/zenodo.23487231).

Code under the [MIT licence](LICENSE). Made by [Soumyaranjan Dash](https://sr-dash.github.io/).
