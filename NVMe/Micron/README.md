Micron NVMe Drives
==================

This is a list of all tested Micron NVMe drive models and their MTBFs. See more
info on reliability test in the [README](https://github.com/linuxhw/SMART).

NVME by Model
------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| Micron    | 7300_MTFDHBE960TDF | 960 GB | 6       | 692   | 0     | 1.90   |
| Micron    | 9300_MTFDHAL15T... | 15.... | 3       | 333   | 0     | 0.91   |
| Micron    | 7300_MTFDHBE6T4TDG | 6.4 TB | 2       | 293   | 0     | 0.80   |
| Micron    | 7300_MTFDHBG3T8TDF | 3.8 TB | 3       | 281   | 0     | 0.77   |
| Micron    | 9300_MTFDHAL6T4TDR | 6.4 TB | 2       | 201   | 0     | 0.55   |
| Micron    | MTFDHBA1T0QFD-1... | 1 TB   | 5       | 194   | 0     | 0.53   |
| Micron    | 7300_MTFDHBE3T8TDF | 3.8 TB | 25      | 164   | 0     | 0.45   |
| Micron    | 3460 NVMe          | 1 TB   | 7       | 281   | 150   | 0.41   |
| Micron    | 2200S NVMe         | 256 GB | 24      | 140   | 0     | 0.39   |
| Micron    | 2200V_MTFDHBA25... | 256 GB | 2       | 133   | 0     | 0.37   |
| Micron    | 2200S NVMe         | 512 GB | 75      | 129   | 0     | 0.36   |
| Micron    | 2210_MTFDHBA512QFD | 512 GB | 178     | 115   | 0     | 0.32   |
| Micron    | 7400_MTFDKBG3T8TDZ | 3.8 TB | 4       | 106   | 0     | 0.29   |
| Micron    | 2210 NVMe          | 512 GB | 3       | 101   | 0     | 0.28   |
| Micron    | 2200V_MTFDHBA51... | 512 GB | 71      | 102   | 16    | 0.27   |
| Micron    | 2400_MTFDKBK2T0QFM | 2 TB   | 2       | 92    | 0     | 0.25   |
| Micron    | 2200S NVMe         | 1 TB   | 19      | 92    | 1     | 0.25   |
| Micron    | MTFDKBA512TFK      | 512 GB | 26      | 88    | 0     | 0.24   |
| Micron    | 2400_MTFDKBA2T0QFM | 2 TB   | 2       | 88    | 0     | 0.24   |
| Micron    | 7300_MTFDHBE7T6TDF | 7.6 TB | 5       | 86    | 0     | 0.24   |
| Micron    | 2200 NVMe          | 512 GB | 3       | 85    | 0     | 0.23   |
| Micron    | MTFDHBA512TCK      | 512 GB | 18      | 84    | 0     | 0.23   |
| Micron    | MTFDHBA1T0QFD      | 1 TB   | 2       | 84    | 0     | 0.23   |
| Micron    | MTFDKBA256TFK-1... | 256 GB | 4       | 83    | 0     | 0.23   |
| Micron    | MTFDHBA512QFD-1... | 512 GB | 51      | 83    | 0     | 0.23   |
| Micron    | MTFDKBA512TFK-1... | 512 GB | 17      | 81    | 0     | 0.22   |
| Micron    | MTFDKBA1T0TFK      | 1 TB   | 12      | 75    | 0     | 0.21   |
| Micron    | MTFDHBA512QFD      | 512 GB | 135     | 69    | 0     | 0.19   |
| Micron    | 2450 NVMe          | 256 GB | 9       | 66    | 0     | 0.18   |
| Micron    | 2450_MTFDKBK1T0TFK | 1 TB   | 7       | 63    | 0     | 0.17   |
| Micron    | 2210_MTFDHBA1T0QFD | 1 TB   | 75      | 61    | 0     | 0.17   |
| Micron    | 2450_MTFDKBA1T0TFK | 1 TB   | 158     | 60    | 0     | 0.17   |
| Micron    | MTFDHBA1T0TCK      | 1 TB   | 13      | 56    | 0     | 0.15   |
| Micron    | 2450_MTFDKBA256TFK | 256 GB | 19      | 55    | 0     | 0.15   |
| Micron    | MTFDKCD1T0TFK      | 1 TB   | 22      | 54    | 0     | 0.15   |
| Micron    | 2450_MTFDKBA512TFK | 512 GB | 222     | 54    | 0     | 0.15   |
| Micron    | MTFDKCD512TFK      | 512 GB | 75      | 52    | 0     | 0.14   |
| Micron    | 3460 NVMe          | 512 GB | 10      | 51    | 0     | 0.14   |
| Micron    | MTFDHBA256TDV-1... | 256 GB | 6       | 49    | 0     | 0.14   |
| Micron    | 2450 NVMe          | 1 TB   | 5       | 45    | 0     | 0.13   |
| Micron    | MTFDHBA512TDV-1... | 512 GB | 30      | 43    | 0     | 0.12   |
| Micron    | MTFDHBA256TCK-1... | 256 GB | 64      | 44    | 1     | 0.12   |
| Micron    | MTFDKBA512QFM-1... | 512 GB | 4       | 41    | 0     | 0.11   |
| Micron    | MTFDKBA256TFK      | 256 GB | 11      | 41    | 0     | 0.11   |
| Micron    | 2210S NVMe         | 512 GB | 13      | 37    | 0     | 0.10   |
| Micron    | MTFDKCD256TFK      | 256 GB | 20      | 36    | 0     | 0.10   |
| Micron    | 2400_MTFDKBA1T0QFM | 1 TB   | 75      | 34    | 0     | 0.10   |
| Micron    | 2400_MTFDKBA512QFM | 512 GB | 179     | 34    | 6     | 0.09   |
| Micron    | MTFDHBA256TDV      | 256 GB | 17      | 33    | 0     | 0.09   |
| Micron    | MTFDHBA1T0TDV-1... | 1 TB   | 16      | 31    | 0     | 0.09   |
| Micron    | 2300 NVMe          | 1 TB   | 86      | 29    | 0     | 0.08   |
| Micron    | 2200_MTFDHBA1T0TCK | 1 TB   | 9       | 26    | 0     | 0.07   |
| Micron    | 2300 NVMe          | 512 GB | 66      | 26    | 1     | 0.07   |
| Micron    | MTFDKBA1T0TFH      | 1 TB   | 43      | 24    | 0     | 0.07   |
| Micron    | MTFDHBA512TDV      | 512 GB | 47      | 21    | 0     | 0.06   |
| Micron    | MTFDKCD1T0QFM-1... | 1 TB   | 13      | 20    | 0     | 0.06   |
| Micron    | 7450_MTFDKBA960TFR | 960 GB | 3       | 19    | 0     | 0.05   |
| Micron    | MTFDKCD512QFM-1... | 512 GB | 45      | 19    | 0     | 0.05   |
| Micron    | 2200_MTFDHBA512TCK | 512 GB | 24      | 18    | 0     | 0.05   |
| Micron    | 3400_MTFDKBA512TFH | 512 GB | 72      | 18    | 0     | 0.05   |
| Micron    | 3400 NVMe          | 1 TB   | 8       | 17    | 0     | 0.05   |
| Micron    | 2450 NVMe          | 512 GB | 14      | 16    | 0     | 0.05   |
| Micron    | 7450_MTFDKCC960TFR | 960 GB | 4       | 15    | 0     | 0.04   |
| Micron    | MTFDKBA1T0TFK-1... | 1 TB   | 4       | 15    | 0     | 0.04   |
| Micron    | MTFDHBA256TCK      | 256 GB | 10      | 17    | 22    | 0.04   |
| Micron    | 3400_MTFDKBA1T0TFH | 1 TB   | 136     | 15    | 0     | 0.04   |
| Micron    | 2200_MTFDHBA256TCK | 256 GB | 12      | 14    | 0     | 0.04   |
| Micron    | MTFDKBA512TFH-1... | 512 GB | 35      | 14    | 0     | 0.04   |
| Micron    | MTFDKBA1T0QFM-1... | 1 TB   | 46      | 14    | 0     | 0.04   |
| Micron    | MTFDKBA512TFH      | 512 GB | 44      | 13    | 0     | 0.04   |
| Micron    | 2300_MTFDHBA256TDV | 256 GB | 4       | 12    | 0     | 0.03   |
| Micron    | 2300 NVMe          | 256 GB | 5       | 12    | 0     | 0.03   |
| Micron    | 2450_MTFDKBK512TFK | 512 GB | 2       | 12    | 0     | 0.03   |
| Micron    | MTFDKBA1T0TFH-1... | 1 TB   | 29      | 9     | 0     | 0.03   |
| Micron    | 3400_MTFDKBA2T0TFH | 2 TB   | 11      | 8     | 0     | 0.02   |
| Micron    | 7300_MTFDHBA480TDF | 480 GB | 2       | 8     | 0     | 0.02   |
| Micron    | 2400_MTFDKBK512QFM | 512 GB | 7       | 8     | 0     | 0.02   |
| Micron    | 2550               | 512 GB | 9       | 7     | 0     | 0.02   |
| Micron    | MTFDKBA2T0QFM-1... | 2 TB   | 5       | 7     | 0     | 0.02   |
| Micron    | 2400_MTFDKBK1T0QFM | 1 TB   | 6       | 6     | 0     | 0.02   |
| Micron    | 3400 NVMe          | 512 GB | 13      | 4     | 0     | 0.01   |
| Micron    | MTFDKBA2T0TFH-1... | 2 TB   | 3       | 4     | 0     | 0.01   |
| Micron    | MTFDKCD1T0TGE-1... | 1 TB   | 7       | 4     | 0     | 0.01   |
| Micron    | MTFDKBA512QFM-1... | 512 GB | 5       | 3     | 0     | 0.01   |
| Micron    | 2400A NVMe         | 512 GB | 5       | 3     | 0     | 0.01   |
| Micron    | MTFDKBA512TFH-1... | 512 GB | 2       | 2     | 0     | 0.01   |
| Micron    | 2550               | 1 TB   | 5       | 2     | 0     | 0.01   |
| Micron    | 3500               | 2 TB   | 2       | 1     | 0     | 0.00   |
