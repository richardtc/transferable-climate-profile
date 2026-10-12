# A Transferable Climate Profile Framework

**Using WorldClim v2.1 and CMIP6 SSP projections. Case study: Cambodia**

An open, reproducible workflow in R and Quarto for producing a national climate profile from WorldClim data: historical baseline maps and charts, future projections under two emissions scenarios, and seasonal outputs tailored to a region and sector of interest. The worked example is Cambodia and rice farming, but the workflow can be applied to any country by changing a few variables.

## What it produces

All outputs are derived from WorldClim v2.1 monthly variables (minimum temperature, maximum temperature and precipitation), cropped and masked to a GADM national boundary.

**Annual maps and graphics** (applicable to any country)

- Mean annual temperature and mean annual precipitation, historical baseline (1970–2000)
- Change in mean annual temperature and precipitation, 2x2 panel maps (SSP2-4.5 and SSP5-8.5 × 2041–2060 and 2061–2080)
- Model ensemble spread plots of mean annual temperature and precipitation change across five GCMs

**Monthly graphics** (applicable to any country)

- Climate chart of mean monthly precipitation and temperature, historical baseline
- Ensemble range plots of mean monthly temperature and precipitation, with GCM uncertainty ribbons

**Seasonal maps and graphics** (tailored to Cambodia and rice cultivation)

- Wet-season and dry-season precipitation change maps
- Dry-season mean temperature change maps
- Mean monthly precipitation with wet and dry seasons and south-west monsoon onset and cessation
- Mean monthly maximum temperature against an indicative 35°C heat-stress threshold for rice

Seasons follow Cambodia's monsoonal system: wet season May–November and dry season December–April (Chhinh & Millington, 2015).

## Data

- **Historical climate:** WorldClim v2.1, 1970–2000 monthly climatology at 30 arc-seconds (~1 km)
- **Future projections:** CMIP6 downscaled projections distributed through WorldClim, at the same resolution, for five GCMs (ACCESS-CM2, MIROC6, EC-Earth3-Veg, MRI-ESM2-0, IPSL-CM6A-LR), two scenarios (SSP2-4.5, SSP5-8.5) and two periods (2041–2060, 2061–2080)
- **National boundary:** GADM, level 0

Data are downloaded with the `geodata` R package and are not included in this repository.

## Requirements

R packages: `terra`, `geodata`, `codetools`, `magick`. The `prerequisites` chunk installs any that are missing.

On Ubuntu, some system libraries may be needed first:

```bash
sudo apt-get install libabsl-dev cmake libmagick++-dev
```

## Usage

1. Open `region_profile.qmd` in RStudio.
2. In the `setvariables` chunk, set:
   - `country_iso`: the three-letter ISO code of the country (e.g. `"KHM"`)
   - `lat`, `lon`: a point within the WorldClim tile covering the country
   - `wet_months`, `dry_months`: the season definitions for the region
3. Run the download chunks once. Downloaded files are stored in `wc_downloads_1_<iso>/` and skipped on later runs.
4. Run the remaining chunks in order. Maps and charts are saved as PNG files in `wc_downloads_1_<iso>/graphics/`.

Code chunks are set to `eval=FALSE`, so rendering the document displays the code without re-running the downloads and processing. Run the chunks interactively to generate the outputs.

Country names in plot titles are currently written in the code; update them when applying the workflow to another country.

## Licence

The code in this repository is released under the [MIT License](LICENSE).

The explanatory text and documentation are licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).
## Outputs

Maps and graphical outputs can be seen at https://sustainableos.international/region_profile.html
