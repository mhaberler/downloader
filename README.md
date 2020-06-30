# DWD Open Data Downloader
A simple python package to download NWP data from DWD's Open Data File Server https://opendata.dwd.de.


# Usage
This package is available as a docker image:
```
docker run --rm deutscherwetterdienst/downloader
```

## Display help
To display help run:
```bash
docker run --rm deutscherwetterdienst/downloader
```
Output:
```
Usage: downloader [OPTIONS]

  Downloads NWP model data in GRIB2 format from DWD's Open Data file server
  https://opendata.dwd.de using HTTPS.

Options:
  --model [cosmo-d2|cosmo-d2-eps|icon|icon-eps|icon-eu|icon-eu-eps|icon-d2|icon-d2-eps]
                                  the NWP model name
  --grid [regular-lat-lon|rotated-lat-lon|icosahedral]
                                  the model grid
  --single-level-fields TEXT      one or more single-level model fields that
                                  should be donwloaded, e.g.
                                  t_2m,tmax_2m,clch,pmsl, ...  [required]

  --min-time-step INTEGER         the minimum forecast time step to download
                                  (default=0)

  --max-time-step INTEGER         the maximung forecast time step to download,
                                  e.g. 12 will download time steps from min-
                                  time-step - 12 (default=0)

  --timestamp [%Y-%m-%d|%Y-%m-%dT%H:%M:%S|%Y-%m-%d %H:%M:%S]
                                  the time stamp of the dataset, e.g.
                                  '2020-06-26 18:00'. Uses latest available if
                                  no timestamp is specified.

  --directory DIRECTORY           the download directory, defaults to working
                                  directory

  --help                          Show this message and exit.
```

## Download data
You can download some custom data by running:
```bash
docker run --rm deutscherwetterdienst/downloader downloader --model icon-eu --single-level-fields t_2m --max-time-step 5 --directory /
```
You should see verbose output like this:
```
[downloader_cli.py:249 -             download() ] 
---------------
Model: icon-eu
Grid: regular-lat-lon
Fields: t_2m
Minimum time step: 0
Maximum time step: 5
Timestamp: 2020-06-30
Model run: 12
Destination: /
---------------

[downloader_cli.py:108 - downloadAndExtractBz2FileFromUrl() ] downloading file: 'https://opendata.dwd.de/weather/nwp/icon-eu/grib/12/t_2m/icon-eu_europe_regular-lat-lon_single-level_2020063012_000_T_2M.grib2.bz2'
[downloader_cli.py:121 - downloadAndExtractBz2FileFromUrl() ] saving file as: '/icon-eu_europe_regular-lat-lon_single-level_2020063012_000_T_2M.grib2'
[downloader_cli.py:124 - downloadAndExtractBz2FileFromUrl() ] Done.
[downloader_cli.py:108 - downloadAndExtractBz2FileFromUrl() ] downloading file: 'https://opendata.dwd.de/weather/nwp/icon-eu/grib/12/t_2m/icon-eu_europe_regular-lat-lon_single-level_2020063012_001_T_2M.grib2.bz2'
[downloader_cli.py:121 - downloadAndExtractBz2FileFromUrl() ] saving file as: '/icon-eu_europe_regular-lat-lon_single-level_2020063012_001_T_2M.grib2'
[downloader_cli.py:124 - downloadAndExtractBz2FileFromUrl() ] Done.
...
```