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
| SSSTC     | CL1-3D256          | 256 GB | 4       | 452   | 0     | 1.24   |
| SSSTC     | CL1-4D256-D22      | 256 GB | 5       | 313   | 0     | 0.86   |
| SSSTC     | CL1-8D128          | 128 GB | 2       | 265   | 0     | 0.73   |
| SSSTC     | CL1-3D256-Q11 NVMe | 256 GB | 33      | 218   | 0     | 0.60   |
| SSSTC     | CL1-3D512-Q11 NVMe | 512 GB | 26      | 202   | 1     | 0.53   |
| SSSTC     | CL1-8D512          | 512 GB | 17      | 136   | 0     | 0.38   |
| SSSTC     | CL4-4D256-Q62      | 256 GB | 2       | 135   | 0     | 0.37   |
| SSSTC     | CL1-4D256          | 256 GB | 64      | 133   | 1     | 0.36   |
| SSSTC     | CL1-8D256-HP       | 256 GB | 31      | 115   | 0     | 0.32   |
| SSSTC     | CL4-3D1024-Q11 ... | 1 TB   | 4       | 104   | 0     | 0.29   |
| SSSTC     | CL1-8D128-HP       | 128 GB | 8       | 101   | 0     | 0.28   |
| SSSTC     | CL1-4D512          | 512 GB | 10      | 106   | 101   | 0.27   |
| SSSTC     | CL4-3D256-Q11 NVMe | 256 GB | 8       | 97    | 0     | 0.27   |
| SSSTC     | CL4-4D256-Q79      | 256 GB | 3       | 168   | 2     | 0.23   |
| SSSTC     | CL1-8D512-HP       | 512 GB | 4       | 75    | 0     | 0.21   |
| SSSTC     | CL4-3D512-Q11 NVMe | 512 GB | 13      | 77    | 1     | 0.20   |
| SSSTC     | CL1-8D256          | 256 GB | 17      | 72    | 0     | 0.20   |
| SSSTC     | CL1-3D128-Q11 NVMe | 128 GB | 22      | 71    | 0     | 0.20   |
| SSSTC     | CL4-8D512          | 512 GB | 12      | 45    | 0     | 0.12   |
| SSSTC     | CL1-4D128          | 128 GB | 16      | 43    | 1     | 0.12   |
| SSSTC     | CL4-4D512-Q62      | 512 GB | 4       | 39    | 0     | 0.11   |
| SSSTC     | CL4-8D256-HP       | 256 GB | 3       | 34    | 0     | 0.10   |
| SSSTC     | CL6-8D1024         | 1 TB   | 2       | 29    | 0     | 0.08   |
| SSSTC     | CA5-8D256-Q79      | 256 GB | 8       | 27    | 0     | 0.08   |
| SSSTC     | CL5-8D512          | 512 GB | 4       | 24    | 0     | 0.07   |
| SSSTC     | CA6-8D2048-Q11 ... | 2 TB   | 7       | 19    | 6     | 0.05   |
| SSSTC     | CA5-8D512          | 512 GB | 7       | 13    | 0     | 0.04   |
| SSSTC     | CA5-8D512-Q11 NVMe | 512 GB | 2       | 10    | 0     | 0.03   |
| SSSTC     | CL4-8D1024         | 1 TB   | 3       | 10    | 0     | 0.03   |
| SSSTC     | CA5-8D256          | 256 GB | 2       | 9     | 0     | 0.03   |
| SSSTC     | CA6-8D512          | 512 GB | 6       | 5     | 0     | 0.02   |
| SSSTC     | CL4-8D256          | 256 GB | 2       | 3     | 0     | 0.01   |
| SSSTC     | CA6-8D1024         | 1 TB   | 2       | 0     | 0     | 0.00   |
