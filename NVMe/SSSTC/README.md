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
| SSSTC     | CL1-3D256          | 256 GB | 3       | 276   | 0     | 0.76   |
| SSSTC     | CL1-4D256-D22      | 256 GB | 2       | 198   | 0     | 0.54   |
| SSSTC     | CL1-3D512-Q11 NVMe | 512 GB | 16      | 155   | 0     | 0.43   |
| SSSTC     | CL1-8D512          | 512 GB | 8       | 105   | 0     | 0.29   |
| SSSTC     | CL1-3D256-Q11 NVMe | 256 GB | 17      | 102   | 0     | 0.28   |
| SSSTC     | CL4-3D1024-Q11 ... | 1 TB   | 2       | 66    | 0     | 0.18   |
| SSSTC     | CL1-4D256          | 256 GB | 42      | 64    | 1     | 0.17   |
| SSSTC     | CL1-8D512-HP       | 512 GB | 3       | 52    | 0     | 0.14   |
| SSSTC     | CL4-8D512          | 512 GB | 4       | 49    | 0     | 0.14   |
| SSSTC     | CL1-4D512          | 512 GB | 7       | 49    | 0     | 0.14   |
| SSSTC     | CL1-8D256          | 256 GB | 13      | 37    | 0     | 0.10   |
| SSSTC     | CL1-8D256-HP       | 256 GB | 19      | 34    | 0     | 0.09   |
| SSSTC     | CL1-4D128          | 128 GB | 9       | 26    | 0     | 0.07   |
| SSSTC     | CA5-8D512          | 512 GB | 6       | 13    | 0     | 0.04   |
| SSSTC     | CL4-3D256-Q11 NVMe | 256 GB | 2       | 11    | 0     | 0.03   |
| SSSTC     | CA6-8D2048-Q11 ... | 2 TB   | 6       | 10    | 0     | 0.03   |
| SSSTC     | CL1-3D128-Q11 NVMe | 128 GB | 17      | 10    | 0     | 0.03   |
| SSSTC     | CL4-3D512-Q11 NVMe | 512 GB | 4       | 8     | 0     | 0.02   |
| SSSTC     | CA5-8D256-Q79      | 256 GB | 3       | 4     | 0     | 0.01   |
| SSSTC     | CA6-8D512          | 512 GB | 3       | 1     | 0     | 0.01   |
| SSSTC     | CL1-8D128-HP       | 128 GB | 3       | 0     | 0     | 0.00   |
