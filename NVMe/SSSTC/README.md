SSSTC NVMe Drives
=================

This is a list of all tested SSSTC NVMe drive models and their MTBFs. See more
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
| SSSTC     | CL1-3D256          | 256 GB | 3       | 268   | 0     | 0.73   |
| SSSTC     | CL1-8D512          | 512 GB | 7       | 110   | 0     | 0.30   |
| SSSTC     | CL1-3D256-Q11 NVMe | 256 GB | 15      | 108   | 0     | 0.30   |
| SSSTC     | CL4-3D1024-Q11 ... | 1 TB   | 2       | 66    | 0     | 0.18   |
| SSSTC     | CL1-3D512-Q11 NVMe | 512 GB | 11      | 61    | 0     | 0.17   |
| SSSTC     | CL1-4D256          | 256 GB | 29      | 46    | 0     | 0.13   |
| SSSTC     | CL1-4D256-D22      | 256 GB | 1       | 46    | 0     | 0.13   |
| SSSTC     | CL1-4D512          | 512 GB | 6       | 43    | 0     | 0.12   |
| SSSTC     | CL1-8D256          | 256 GB | 12      | 36    | 0     | 0.10   |
| SSSTC     | CL1-8D256-HP       | 256 GB | 16      | 34    | 0     | 0.10   |
| SSSTC     | CL1-4D128          | 128 GB | 5       | 24    | 0     | 0.07   |
| SSSTC     | CL1-8D512-HP       | 512 GB | 2       | 21    | 0     | 0.06   |
| SSSTC     | CL4-3D256-Q11 NVMe | 256 GB | 1       | 19    | 0     | 0.05   |
| SSSTC     | CA5-8D512-Q79      | 512 GB | 1       | 18    | 0     | 0.05   |
| SSSTC     | LJ1-2W7680         | 962 GB | 1       | 11    | 0     | 0.03   |
| SSSTC     | CA6-8D2048-Q11 ... | 2 TB   | 1       | 11    | 0     | 0.03   |
| SSSTC     | CL1-3D128-Q11 NVMe | 128 GB | 16      | 9     | 0     | 0.03   |
| SSSTC     | CL4-3D512-Q11 NVMe | 512 GB | 3       | 9     | 0     | 0.03   |
| SSSTC     | CA5-8D256-Q79      | 256 GB | 2       | 5     | 0     | 0.02   |
| SSSTC     | CA6-8D512          | 512 GB | 1       | 1     | 0     | 0.00   |
| SSSTC     | CA5-8D512          | 512 GB | 4       | 0     | 0     | 0.00   |
| SSSTC     | CL4-8D512          | 512 GB | 2       | 0     | 0     | 0.00   |
| SSSTC     | CL1-8D128-HP       | 128 GB | 2       | 0     | 0     | 0.00   |
| SSSTC     | CA6-8D512-Q11 NVMe | 512 GB | 1       | 0     | 0     | 0.00   |
