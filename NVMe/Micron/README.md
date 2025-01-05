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
| Micron    | 2200V_MTFDHBA25... | 256 GB | 2       | 217   | 0     | 0.60   |
| Micron    | 9300_MTFDHAL6T4TDR | 6.4 TB | 2       | 201   | 0     | 0.55   |
| Micron    | MTFDHBA1T0QFD-1... | 1 TB   | 5       | 198   | 0     | 0.54   |
| Micron    | 7300_MTFDHBE3T8TDF | 3.8 TB | 25      | 164   | 0     | 0.45   |
| Micron    | 2400_MTFDKBK2T0QFM | 2 TB   | 2       | 154   | 0     | 0.42   |
| Micron    | 3460 NVMe          | 1 TB   | 7       | 282   | 150   | 0.41   |
| Micron    | 2200S NVMe         | 256 GB | 24      | 141   | 0     | 0.39   |
| Micron    | 2200S NVMe         | 512 GB | 75      | 130   | 0     | 0.36   |
| Micron    | 2210_MTFDHBA512QFD | 512 GB | 178     | 118   | 0     | 0.33   |
| Micron    | 7400_MTFDKBG3T8TDZ | 3.8 TB | 4       | 106   | 0     | 0.29   |
| Micron    | 2400_MTFDKBA2T0QFM | 2 TB   | 2       | 101   | 0     | 0.28   |
| Micron    | 2210 NVMe          | 512 GB | 3       | 101   | 0     | 0.28   |
| Micron    | 2200V_MTFDHBA51... | 512 GB | 71      | 102   | 16    | 0.27   |
| Micron    | 2450_MTFDKBK1T0TFK | 1 TB   | 7       | 99    | 0     | 0.27   |
| Micron    | 2200S NVMe         | 1 TB   | 19      | 95    | 1     | 0.26   |
| Micron    | MTFDKBA512TFK      | 512 GB | 26      | 92    | 0     | 0.25   |
| Micron    | 7300_MTFDHBE7T6TDF | 7.6 TB | 5       | 86    | 0     | 0.24   |
| Micron    | 2200 NVMe          | 512 GB | 3       | 85    | 0     | 0.23   |
| Micron    | MTFDKBA512TFK-1... | 512 GB | 17      | 85    | 0     | 0.23   |
| Micron    | MTFDHBA512TCK      | 512 GB | 18      | 84    | 0     | 0.23   |
| Micron    | MTFDHBA512QFD-1... | 512 GB | 51      | 84    | 0     | 0.23   |
| Micron    | MTFDHBA1T0QFD      | 1 TB   | 2       | 84    | 0     | 0.23   |
| Micron    | MTFDKBA256TFK-1... | 256 GB | 4       | 83    | 0     | 0.23   |
| Micron    | MTFDHBA512QFD      | 512 GB | 135     | 79    | 0     | 0.22   |
| Micron    | MTFDKBA1T0TFK      | 1 TB   | 12      | 76    | 0     | 0.21   |
| Micron    | 2450 NVMe          | 256 GB | 9       | 66    | 0     | 0.18   |
| Micron    | 2210_MTFDHBA1T0QFD | 1 TB   | 75      | 64    | 0     | 0.18   |
| Micron    | 2450_MTFDKBA1T0TFK | 1 TB   | 158     | 62    | 0     | 0.17   |
| Micron    | 2450_MTFDKBA512TFK | 512 GB | 222     | 62    | 0     | 0.17   |
| Micron    | MTFDHBA1T0TCK      | 1 TB   | 13      | 58    | 0     | 0.16   |
| Micron    | MTFDKCD512TFK      | 512 GB | 75      | 56    | 0     | 0.16   |
| Micron    | 2450_MTFDKBA256TFK | 256 GB | 19      | 56    | 0     | 0.16   |
| Micron    | 2210S NVMe         | 512 GB | 13      | 56    | 0     | 0.15   |
| Micron    | MTFDKCD1T0TFK      | 1 TB   | 22      | 54    | 0     | 0.15   |
| Micron    | 3460 NVMe          | 512 GB | 10      | 51    | 0     | 0.14   |
| Micron    | MTFDHBA256TDV-1... | 256 GB | 6       | 49    | 0     | 0.14   |
| Micron    | 2450 NVMe          | 1 TB   | 5       | 46    | 0     | 0.13   |
| Micron    | MTFDHBA256TCK-1... | 256 GB | 64      | 44    | 1     | 0.12   |
| Micron    | MTFDHBA512TDV-1... | 512 GB | 30      | 44    | 0     | 0.12   |
| Micron    | MTFDKBA512QFM-1... | 512 GB | 4       | 41    | 0     | 0.11   |
| Micron    | MTFDKBA256TFK      | 256 GB | 11      | 41    | 0     | 0.11   |
| Micron    | MTFDKCD256TFK      | 256 GB | 20      | 38    | 0     | 0.11   |
| Micron    | 2400_MTFDKBA1T0QFM | 1 TB   | 75      | 37    | 0     | 0.10   |
| Micron    | 2400_MTFDKBA512QFM | 512 GB | 179     | 38    | 6     | 0.10   |
| Micron    | MTFDHBA256TDV      | 256 GB | 17      | 37    | 0     | 0.10   |
| Micron    | MTFDHBA1T0TDV-1... | 1 TB   | 16      | 31    | 0     | 0.09   |
| Micron    | 2300 NVMe          | 1 TB   | 86      | 30    | 0     | 0.08   |
| Micron    | 2300 NVMe          | 512 GB | 66      | 27    | 1     | 0.07   |
| Micron    | 2200_MTFDHBA1T0TCK | 1 TB   | 9       | 26    | 0     | 0.07   |
| Micron    | MTFDKBA1T0TFH      | 1 TB   | 43      | 24    | 0     | 0.07   |
| Micron    | MTFDKBA1T0TFK-1... | 1 TB   | 4       | 23    | 0     | 0.07   |
| Micron    | MTFDHBA512TDV      | 512 GB | 47      | 22    | 0     | 0.06   |
| Micron    | 2450_MTFDKBK512TFK | 512 GB | 2       | 22    | 0     | 0.06   |
| Micron    | MTFDKCD1T0QFM-1... | 1 TB   | 13      | 20    | 0     | 0.06   |
| Micron    | MTFDKBA1T0QFM-1... | 1 TB   | 46      | 19    | 0     | 0.05   |
| Micron    | MTFDKCD512QFM-1... | 512 GB | 45      | 19    | 0     | 0.05   |
| Micron    | 7450_MTFDKBA960TFR | 960 GB | 3       | 19    | 0     | 0.05   |
| Micron    | 2200_MTFDHBA512TCK | 512 GB | 24      | 18    | 0     | 0.05   |
| Micron    | 3400_MTFDKBA512TFH | 512 GB | 72      | 18    | 0     | 0.05   |
| Micron    | 3400 NVMe          | 1 TB   | 8       | 17    | 0     | 0.05   |
| Micron    | 2450 NVMe          | 512 GB | 14      | 16    | 0     | 0.05   |
| Micron    | 3400_MTFDKBA1T0TFH | 1 TB   | 136     | 16    | 0     | 0.05   |
| Micron    | 7450_MTFDKCC960TFR | 960 GB | 4       | 15    | 0     | 0.04   |
| Micron    | MTFDKBA512TFH-1... | 512 GB | 35      | 15    | 0     | 0.04   |
| Micron    | MTFDHBA256TCK      | 256 GB | 10      | 17    | 22    | 0.04   |
| Micron    | MTFDKBA512TFH      | 512 GB | 44      | 14    | 0     | 0.04   |
| Micron    | 2200_MTFDHBA256TCK | 256 GB | 12      | 14    | 0     | 0.04   |
| Micron    | 2300 NVMe          | 256 GB | 5       | 14    | 0     | 0.04   |
| Micron    | 2300_MTFDHBA256TDV | 256 GB | 4       | 12    | 0     | 0.03   |
| Micron    | MTFDKBA1T0TFH-1... | 1 TB   | 29      | 11    | 0     | 0.03   |
| Micron    | 2400_MTFDKBK512QFM | 512 GB | 7       | 10    | 0     | 0.03   |
| Micron    | 3400_MTFDKBA2T0TFH | 2 TB   | 11      | 8     | 0     | 0.02   |
| Micron    | 7300_MTFDHBA480TDF | 480 GB | 2       | 8     | 0     | 0.02   |
| Micron    | 2550               | 512 GB | 9       | 7     | 0     | 0.02   |
| Micron    | MTFDKBA2T0QFM-1... | 2 TB   | 5       | 7     | 0     | 0.02   |
| Micron    | 2400_MTFDKBK1T0QFM | 1 TB   | 6       | 7     | 0     | 0.02   |
| Micron    | MTFDKBA2T0TFH-1... | 2 TB   | 3       | 6     | 0     | 0.02   |
| Micron    | MTFDKCD1T0TGE-1... | 1 TB   | 7       | 4     | 0     | 0.01   |
| Micron    | 3400 NVMe          | 512 GB | 13      | 4     | 0     | 0.01   |
| Micron    | MTFDKBA512QFM-1... | 512 GB | 5       | 3     | 0     | 0.01   |
| Micron    | 2400A NVMe         | 512 GB | 5       | 3     | 0     | 0.01   |
| Micron    | MTFDKBA512TFH-1... | 512 GB | 2       | 2     | 0     | 0.01   |
| Micron    | 2550               | 1 TB   | 5       | 2     | 0     | 0.01   |
| Micron    | 3500               | 2 TB   | 2       | 2     | 0     | 0.01   |
