# Air quality health impact calculator

These scripts are used to calculate the health impact of air pollution
using
* modelled air pollution concentrations
* gridded population data
* population age structure data
* baseline health data


## Current limitations

* The scripts only use the GEMM health functions from Burnett et al. (2018)
but could later be expanded to use other health functions and other pollutants (e.g. O<sub>3</sub>)
* Currently setup to only use GPWv4 gridded population data
* Currently uses GBD IHME baseline health data and age structure

## Preparing to run the code

Download the gridded population data, baseline health data and age structure data

### Make population count slices
For the GPWv4 data, a utility script (`./utils/make_popslices.py`) has been written.
If using other data, you will need to make these files.

For each year you wish to include in the analysis, there needs to be a pickled
dictionary of population count slices in the grids directory 
(e.g. `./grids/pop_count_slices_YYYY.P`)

The dictionary keys should be the 3 letter isocode for each country,
and the value should be a DataArray of population count for that country
with surrounding grids as zeroes. E.g.

```
{'CHN': <xarray.DataArray 'CHN' (latitude: 860, longitude: 1469)>
 array([[0., 0., 0., ..., 0., 0., 0.],
        [0., 0., 0., ..., 0., 0., 0.],
        [0., 0., 0., ..., 0., 0., 0.],
        ...,
        [0., 0., 0., ..., 0., 0., 0.],
        [0., 0., 0., ..., 0., 0., 0.],
        [0., 0., 0., ..., 0., 0., 0.]])
 Coordinates:
   * longitude  (longitude) float64 73.6 73.65 73.69 73.73 ... 134.7 134.7 134.8
   * latitude   (latitude) float64 53.52 53.48 53.44 53.4 ... 16.06 16.02 15.77
 Attributes:
     units:      Persons
     long_name:  Population Count, v4.11 (2000, 2005, 2010, 2015, 2020): 2.5 a...
     min:        [ 0.000e+00  0.000e+00  0.000e+00  0.000e+00  0.000e+00  0.00...
     max:        [9.63072875e+05 1.00347762e+06 1.13291988e+06 1.34768400e+06\...}
```

