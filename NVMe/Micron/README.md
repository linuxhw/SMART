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
| Micron    | 2200S NVMe         | 256 GB | 1       | 58    | 0     | 0.16   |
| Micron    | 2200S NVMe         | 1 TB   | 2       | 19    | 0     | 0.05   |
| Micron    | MTFDHBA512TCK      | 512 GB | 1       | 15    | 0     | 0.04   |
| Micron    | 2200_MTFDHBA512TCK | 512 GB | 1       | 11    | 0     | 0.03   |
| Micron    | 2200_MTFDHBA256TCK | 256 GB | 2       | 6     | 0     | 0.02   |
| Micron    | 2200S NVMe         | 512 GB | 3       | 5     | 0     | 0.01   |
| Micron    | MTFDHBA256TCK      | 256 GB | 1       | 2     | 0     | 0.01   |
| Micron    | MTFDHBA256TCK-1... | 256 GB | 6       | 4     | 1     | 0.00   |
| Micron    | 2200V_MTFDHBA51... | 512 GB | 1       | 0     | 0     | 0.00   |
