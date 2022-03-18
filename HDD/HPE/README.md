HPE Hard Drives
===============

This is a list of all tested HPE hard drive models and their MTBFs. See more
info on reliability test in the [README](https://github.com/linuxhw/SMART).

Contents
--------

1. [ HDD by Model  ](#hdd-by-model)
2. [ HDD by Family ](#hdd-by-family)

HDD by Model
------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| HPE       | MB0500EBNCR        | 500 GB | 1       | 1526  | 0     | 4.18   |
| HPE       | MB4000GCWDC        | 4 TB   | 1       | 1037  | 2     | 0.95   |
| HPE       | MM1000EBKAF        | 1 TB   | 2       | 127   | 0     | 0.35   |
| HPE       | MB004000GWWQH      | 4 TB   | 1       | 6     | 0     | 0.02   |

HDD by Family
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG       | Family                 | Models | Samples | Days  | Err   | MTBF |
|-----------|------------------------|--------|---------|-------|-------|------|
| HPE       | WDC Enterprise         | 1      | 1       | 1526  | 0     | 4.18   |
| HPE       | Seagate Constellati... | 1      | 1       | 1037  | 2     | 0.95   |
| HPE       | Proliant HardDrive     | 1      | 2       | 127   | 0     | 0.35   |
| HPE       | Unknown                | 1      | 1       | 6     | 0     | 0.02   |
