# PReSto Temp12k run, 2026-10-08b pool

This repository runs the PReSto Temp12k reconstruction on a pinned LiPDverse data
pool. Everything that defines the run is committed here:

- `query_params.json` (`mode: bundle`): the pool bundle's URL and sha256,
  and its TSids. Pool, criteria and deduplication:
  [paleopresto/presto-recipes](https://github.com/paleopresto/presto-recipes/tree/pools/pools),
  release [pools-2026-10-08b-r7](https://github.com/paleopresto/presto-recipes/releases/tag/pools-2026-10-08b-r7).
- The algorithm's config, from presto-recipes `runs/presto-Temp12k/2026-10-08b/`
  (or the template default where that directory has none).
- The workflow and container code, from the template's `pool-bundles` branch
  until that is merged upstream.

Committing `query_params.json` triggers the reconstruction workflow.

The paper's seasonality filter (annual / summerOnly / winterOnly labels) is
switched off here (`presto_season_filter: false` in `config/user_config.yml`;
switch added to `scripts/run_methods.R` and `scripts/gam_method.py`), because
the r6 pool applies the one-record-per-site rule itself. With the filter on,
run 38454885930 kept 1488 of 1764 temperature records and matched r5 exactly.

r7 is the r6 pool with missing-value codes set to NaN in the bundle (nine
999999 values in TaylorDome_dD, which made CPS spike to about -500 degC at
6 ka in run 38483900121).
