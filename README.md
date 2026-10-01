# VayuDrishti

<!-- Provenance: Anubhav Chakraborty | VayuDrishti | AC-VD-2026-10 -->

VayuDrishti is a static weather dashboard by Anubhav Chakraborty. It shows worldwide GFS provider forecasts and a separately trained rainfall correction within its Indian-network scope. It is a standalone research product, not an official weather or warning service.

## What it does

- Search worldwide cities or enter coordinates. Forecast days use the selected location's timezone.
- View temperature and feels-like, high/low temperatures, humidity, dew point, wind speed/direction/gusts, sea-level pressure, cloud cover, visibility, snowfall and total precipitation.
- See three-day summaries, an hourly temperature chart and hourly weather tables.
- Compare raw rainfall with a learned correction for named Indian locations within the training scope. Coordinate-only and outside-scope locations show provider forecasts only.
- Switch System, Dark and Light themes. Theme choice is saved locally.
- Download forecast inputs, model details and the rainfall evaluation. Missing source data are reported as unavailable.

All non-rain variables are uncorrected provider forecasts, not independently trained predictions or measurements. Weather-condition codes and feels-like values are provider-derived. No automated warning, SMS, public alert or all-clear is issued.

## Rainfall model

The released `v2-qmxgb-v1-zero` model blends positive-rain empirical quantile mapping plus XGBoost residual regression with the original fitted log-linear v1 correction. QM+XGBoost weights are 45%, 22.5% and 20% for approximate 24h, 48h and 72h leads; the remainder is v1.

An explicit gate preserves exact forecast zeros: raw GFS rain + showers exactly 0.0 produces corrected 0.0. This is an output rule, not proof that the day will be dry. In evaluation, GFS zero cases included 151 / 142 / 147 ERA5-reference days with at least 1mm at the three leads; the rule suppresses those missed-rain cases.

Features include archived fixed-lead GFS precipitation, CAPE, humidity, pressure tendencies, wind vectors, coordinates, elevation and season. ERA5 rain reanalysis is the reference. The browser evaluates exported trees and maps locally. It does not run a neural network, ingest radar/satellite imagery or read rain gauges.

## Exploratory rainfall evaluation

July 1 through September 24, 2026, at 24 Indian regional points: 2,064 location-days per lead. These correlated days are not independent storms. The evaluation period was inspected during development, so it is reused exploratory evidence, not an untouched benchmark or prospective live skill test.

Errors are mm per local day.

| Lead | Raw MAE | v1 MAE | Ensemble MAE | Raw RMSE | v1 RMSE | Ensemble RMSE |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| 24h | 7.414 | 6.608 | 6.519 | 15.834 | 16.381 | 15.801 |
| 48h | 7.664 | 6.774 | 6.765 | 17.027 | 17.135 | 16.920 |
| 72h | 8.217 | 7.143 | 7.052 | 17.338 | 17.950 | 17.713 |

24h and 48h improve both error metrics against raw GFS and v1 in this evaluation. At 72h, ensemble RMSE remains worse than raw GFS, though better than v1. That disclosed tradeoff was accepted for this research release. None of these results is near-perfect.

At the 64.5mm heavy-rain threshold, rainfall-ensemble hits are 1/30, 0/30 and 0/30. Separate warning classifiers failed detection, false-alarm and probability-skill gates. Warnings remain unavailable. The new ensemble has no validated uncertainty intervals.

Six original locations were excluded from fitting and validation: Shimla, Jodhpur, Raipur, Shillong, Bengaluru and Port Blair. Predictions between evaluated Indian points remain geographic extrapolation. Country membership, a nearby point or a working calculation is not evidence of local warning skill.

## Run locally

This repository serves static HTML and JavaScript. No Python backend, TensorFlow/PyTorch server, API key or Node build is required for the deployed dashboard.

```bash
git clone https://github.com/chkanubhav09/VayuDrishti.git
cd VayuDrishti
python3 -m http.server 8000
```

Open `/vayudrishti/app/` on that local server for the forecast dashboard and `/vayudrishti/` for the overview. Internet access is needed for Open-Meteo requests.

The source repository still includes files from the earlier combined hosting layout. The owner identifies `chkanubhav09/chkanubhav09` as a separate portfolio repository; it is not modified by this project. Current project Pages hosting is being moved to the requested address and will be documented after live verification.

## Data and privacy

Forecast and geocoding requests go directly from the browser to Open-Meteo. Search terms and selected coordinates are sent to that provider. The dashboard does not request device location, track visitors or poll forecasts automatically. Forecast response caching is temporary in memory; the theme preference is stored locally.

- [GFS API](https://open-meteo.com/en/docs/gfs-api)
- [Geocoding API](https://open-meteo.com/en/docs/geocoding-api)
- [Fixed-lead historical forecast archive](https://open-meteo.com/en/docs/previous-runs-api)
- [ERA5 historical weather reference](https://open-meteo.com/en/docs/historical-weather-api)
- [Open-Meteo terms](https://open-meteo.com/en/terms)

Weather data attribution: Open-Meteo, CC BY 4.0. Location data: GeoNames via Open-Meteo. GFS rainfall values are modified by the fitted correction where available. This is non-commercial research use; no endorsement is implied. A repository code license does not replace source-data terms.

## Work in progress

The published rainfall evaluation remains the 24-point result above. A 50-site Indian archive expansion and further geographically broader evaluation are in progress, not yet a completed training release. Global learned correction needs separate climate coverage, references and validation. More data or retraining does not guarantee improvement. No nightly automatic retraining/publication pipeline is active.

Source provenance markers name Anubhav Chakraborty. They are inert attribution, not visitor tracking or guaranteed copy detection.
