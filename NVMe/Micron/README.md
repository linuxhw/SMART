Micron NVMe Drives
==================

This is a list of all tested Micron NVMe drive models and their MTBFs. See more
info on reliability test in the [README](https://github.com/linuxhw/SMART).

NVME by Model
------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days   — avg. days per sample,
Err    — avg. errors per sample,
MTBF   — avg. MTBF in years per sample.

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF   |
|-----------|--------------------|--------|---------|-------|-------|--------|
| Micron    | 2200S NVMe         | 256 GB | 3       | 55    | 0     | 0.15   |
| Micron    | 2200 NVMe          | 512 GB | 1       | 38    | 0     | 0.11   |
| Micron    | 2200V_MTFDHBA51... | 512 GB | 3       | 25    | 0     | 0.07   |
| Micron    | MTFDHBA512TCK      | 512 GB | 1       | 15    | 0     | 0.04   |
| Micron    | 2200_MTFDHBA512TCK | 512 GB | 1       | 11    | 0     | 0.03   |
| Micron    | 2200S NVMe         | 1 TB   | 4       | 10    | 0     | 0.03   |
| Micron    | MTFDHBA1T0TCK      | 1 TB   | 3       | 8     | 0     | 0.02   |
| Micron    | 2200S NVMe         | 512 GB | 8       | 7     | 0     | 0.02   |
| Micron    | 2200_MTFDHBA256TCK | 256 GB | 2       | 6     | 0     | 0.02   |
| Micron    | MTFDHBA256TCK      | 256 GB | 2       | 1     | 0     | 0.00   |
| Micron    | MTFDHBA256TCK-1... | 256 GB | 8       | 3     | 1     | 0.00   |
