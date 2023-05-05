LDLC NVMe Drives
================

This is a list of all tested LDLC NVMe drive models and their MTBFs. See more
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
| LDLC      | 120GB              | 120 GB | 1       | 226   | 0     | 0.62   |
| LDLC      | F8+M.2 480         | 480 GB | 3       | 213   | 0     | 0.59   |
| LDLC      | F8+M.2 240         | 240 GB | 1       | 212   | 0     | 0.58   |
| LDLC      | 240GB              | 240 GB | 1       | 194   | 0     | 0.53   |
| LDLC      | 480GB              | 480 GB | 1       | 128   | 1008  | 0.00   |
