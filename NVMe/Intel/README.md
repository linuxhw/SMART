Intel NVMe Drives
=================

This is a list of all tested Intel NVMe drive models and their MTBFs. See more
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
| Intel     | SSDPEDMW012T4      | 1.2 TB | 1       | 823   | 0     | 2.26   |
| Intel     | MEMPEK1W032GA      | 32 GB  | 1       | 694   | 0     | 1.90   |
| Intel     | SSDPED1K375GA      | 375 GB | 1       | 603   | 0     | 1.65   |
| Intel     | SSDPED1D280GA      | 280 GB | 1       | 600   | 0     | 1.64   |
| Intel     | SSDPEDMD400G4      | 400 GB | 1       | 595   | 0     | 1.63   |
| Intel     | SSDPE21D480GA      | 480 GB | 2       | 515   | 0     | 1.41   |
| Intel     | SSDPEKKW256G7      | 256 GB | 6       | 596   | 5     | 1.34   |
| Intel     | SSDPEKKF256G7H     | 256 GB | 3       | 476   | 0     | 1.31   |
| Intel     | SSDPEKKF256G7L     | 256 GB | 4       | 420   | 0     | 1.15   |
| Intel     | SSDPEKKW128G7      | 128 GB | 3       | 402   | 1     | 0.77   |
| Intel     | SSDPEKKF360G7H     | 360 GB | 3       | 239   | 0     | 0.66   |
| Intel     | SSDPEKKF512G8 NVMe | 512 GB | 2       | 231   | 0     | 0.63   |
| Intel     | SSDPED1D480GA      | 480 GB | 2       | 222   | 0     | 0.61   |
| Intel     | SSDPEKNW020T8      | 2 TB   | 7       | 210   | 0     | 0.58   |
| Intel     | SSDPE2MX450G7      | 450 GB | 2       | 204   | 0     | 0.56   |
| Intel     | SSDPEKKF010T8      | 1 TB   | 5       | 191   | 0     | 0.53   |
| Intel     | MEMPEK1J016GAL     | 16 GB  | 5       | 183   | 0     | 0.50   |
| Intel     | SSDPEKKW256G8      | 256 GB | 13      | 151   | 0     | 0.42   |
| Intel     | SSDPEKKW128G8      | 128 GB | 9       | 130   | 0     | 0.36   |
| Intel     | MEMPEK1W016GA      | 16 GB  | 2       | 118   | 0     | 0.33   |
| Intel     | MEMPEK1J016GA      | 16 GB  | 1       | 102   | 0     | 0.28   |
| Intel     | H10 HBRPEKNX020... | 512 GB | 1       | 99    | 0     | 0.27   |
| Intel     | SSDPEDMW400G4      | 400 GB | 1       | 86    | 0     | 0.24   |
| Intel     | SSDPEKNW010T8H     | 1 TB   | 1       | 82    | 0     | 0.23   |
| Intel     | SSDPEKKW512G8      | 512 GB | 9       | 80    | 0     | 0.22   |
| Intel     | SSDPEKKW512G7      | 512 GB | 2       | 78    | 0     | 0.21   |
| Intel     | SSDPEKNW010T8      | 1 TB   | 33      | 67    | 0     | 0.18   |
| Intel     | SSDPEKNW512G8      | 512 GB | 30      | 56    | 0     | 0.15   |
| Intel     | SSDPE2KX040T8      | 4 TB   | 4       | 53    | 0     | 0.15   |
| Intel     | SSDPE2KE020T7      | 2 TB   | 4       | 46    | 0     | 0.13   |
| Intel     | SSDPEKKF512G7H     | 512 GB | 1       | 44    | 0     | 0.12   |
| Intel     | SSDPEKKW010T7      | 1 TB   | 1       | 39    | 0     | 0.11   |
| Intel     | HBRPEKNX0202AHO    | 32 GB  | 4       | 38    | 0     | 0.11   |
| Intel     | SSDPEKKF256G8L     | 256 GB | 16      | 33    | 0     | 0.09   |
| Intel     | HBRPEKNX0202AH     | 512 GB | 5       | 32    | 0     | 0.09   |
| Intel     | SSDPEKKW256G8L     | 256 GB | 1       | 31    | 0     | 0.09   |
| Intel     | HBRPEKNX0202ALO    | 32 GB  | 1       | 31    | 0     | 0.09   |
| Intel     | MEMPEK1J016GAH     | 16 GB  | 1       | 29    | 0     | 0.08   |
| Intel     | SSDPEKKF256G8 NVMe | 256 GB | 1       | 26    | 0     | 0.07   |
| Intel     | SSDPEKNW512G8H     | 512 GB | 20      | 25    | 3     | 0.07   |
| Intel     | SSDPEMKF010T8 NVMe | 1 TB   | 3       | 22    | 0     | 0.06   |
| Intel     | SSDPEKNW512G8L     | 512 GB | 5       | 21    | 0     | 0.06   |
| Intel     | SSDPEKKF010T8 NVMe | 1 TB   | 1       | 20    | 0     | 0.06   |
| Intel     | SSDPEKKF512G8L     | 512 GB | 11      | 17    | 0     | 0.05   |
| Intel     | HBRPEKNX0202AL     | 512 GB | 2       | 17    | 0     | 0.05   |
| Intel     | SSDPEKKW010T8      | 1 TB   | 2       | 16    | 0     | 0.04   |
| Intel     | SSDPEMKF512G8 NVMe | 512 GB | 5       | 11    | 0     | 0.03   |
| Intel     | SSDPEKKF010T8L     | 1 TB   | 11      | 10    | 0     | 0.03   |
| Intel     | HBRPEKNX0202AO     | 32 GB  | 2       | 7     | 0     | 0.02   |
| Intel     | HBRPEKNX0202A      | 512 GB | 2       | 7     | 0     | 0.02   |
| Intel     | SSDPE2KX020T8      | 2 TB   | 2       | 5     | 0     | 0.01   |
| Intel     | HBRPEKNX0203AHO    | 32 GB  | 1       | 3     | 0     | 0.01   |
| Intel     | HBRPEKNX0203AH     | 1 TB   | 1       | 3     | 0     | 0.01   |
| Intel     | SSDPEKKA256G7      | 256 GB | 2       | 1     | 0     | 0.01   |
| Intel     | SSDPEDKE020T7      | 2 TB   | 2       | 1     | 0     | 0.00   |
