HDD/SSD Desktop-Class Reliability Test
--------------------------------------

This is a project to estimate reliability of desktop-class HDD/SSD drives by
the analysis of SMART data collected by Linux users at https://linux-hardware.org. The
primary aim of the project is to find drives with longest power-on hours (POH) and
minimal number of errors, i.e. maximal MTBF (mean time between failures).

Everyone can contribute to this report by uploading probes of their computers by
the [hw-probe](https://github.com/linuxhw/hw-probe) tool:

    sudo -E hw-probe -all -upload

This is a report for consumer drives. Report for enterprise drives: [EnterpriseDrive](https://github.com/linuxhw/EnterpriseDrive)

Total drives: 158029.

Contents
--------

1. [ About          ](#about)
2. [ HDD by Model   ](#hdd-by-model)
3. [ HDD by Vendor  ](#hdd-by-vendor)
4. [ SSD by Model   ](#ssd-by-model)
5. [ SSD by Vendor  ](#ssd-by-vendor)
6. [ NVMe by Model  ](#nvme-by-model)
7. [ NVMe by Vendor ](#nvme-by-vendor)

About
-----

The structure of the reports directory is the following:

    {KIND OF DRIVE}/{VENDOR}/{MODEL PREFIX}/{MODEL}/{DRIVE ID}

    ( e.g. HDD/Seagate/ST1000/ST1000LM035-1RK172/3F1554E2F97E )

Based on SMART data we determine most reliable drive models and vendors by the
following formula:

    MTBF = Power_On_Hours / ( 1 + Number_Of_Important_Errors ) / ( 365*24 )

    ( i.e. MTBF = "Years before/between errors" )

Number_Of_Important_Errors - number of important errors that can indicate a drive failure:

* Current_Pending_Sector
* ECC_Uncorr_Error_Count
* End-to-End_Error
* Offline_Uncorrectable
* Reallocated_Event_Count
* Reallocated_Sector_Ct
* Reported_Uncorrect
* Soft_Read_Error_Rate
* Spin_Retry_Count
* Total_Pending_Sectors
* Unc_Soft_Read_Err_Rate

One can estimate reliability of a hard drive (i.e. probability that the unit will work
for some time T without failure) by:

    Reliability(T) = exp(-T/MTBF)

The list of important SMART attributes is taken from recent studies of Google [1],
Backblaze [2] and Acronis [3]. If an attribute exceeds the value of 1000 then it's
counted as '1000 + log10(X - 999)'.

The list of tracked attributes and MTBF calculation method can be discussed. Please
suggest your ideas in "issues".

You can perform your own analysis of collected reports if needed.

* [1] Google, "Failure Trends in a Large Disk Drive Population" (https://research.google.com/archive/disk_failures.pdf)
* [2] Backblaze, "Hard Drive SMART Stats" (https://www.backblaze.com/blog/hard-drive-smart-stats/)
* [3] Acronis, "Acronis Drive Monitor: Disk Health Calculation" (https://kb.acronis.com/content/9264)

HDD by Model
------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

See full list of tested HDD samples in the Appendix 1 ([All_HDD.md](/All_HDD.md)).

See top 1000 of tested HDD models in the [Top1000_HDD.md](/Top1000_HDD.md).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| Samsung   | HM020GI            | 20 GB  | 2       | 6601  | 0     | 18.09  |
| HP        | GB0160EAFJE        | 160 GB | 2       | 3447  | 0     | 9.44   |
| WDC       | WD6400AAVS-00G9B0  | 640 GB | 2       | 3191  | 0     | 8.74   |
| WDC       | WD7500AAVS-00D7B0  | 752 GB | 2       | 3177  | 0     | 8.71   |
| Samsung   | HE160HJ            | 160 GB | 2       | 3097  | 0     | 8.49   |
| WDC       | WD5000AAKS-60A7B0  | 500 GB | 2       | 3047  | 0     | 8.35   |
| HGST      | HUP722020APA330    | 2 TB   | 2       | 2688  | 0     | 7.36   |
| Hitachi   | HUA7210SASUN1.0T   | 1 TB   | 12      | 2672  | 0     | 7.32   |
| WDC       | WD5000BUCT-63PUZY0 | 500 GB | 2       | 2600  | 0     | 7.13   |
| HP        | MB2000EAZNL        | 2 TB   | 2       | 2560  | 0     | 7.02   |
| WDC       | WD10EVDS-63N5B1    | 1 TB   | 4       | 2541  | 0     | 6.96   |
| HP        | GB0500EAFYL        | 500 GB | 2       | 3042  | 1     | 6.96   |
| WDC       | WD1000FYPS-01ZKB0  | 1 TB   | 3       | 2471  | 0     | 6.77   |
| Hitachi   | HDS7216SBSUN160G   | 160 GB | 2       | 4110  | 2     | 6.76   |
| WDC       | WD1002FBYS-50A6B0  | 1 TB   | 2       | 2401  | 0     | 6.58   |
| WDC       | WD5000AVVS-63ZWB0  | 500 GB | 4       | 3388  | 12    | 6.49   |
| WDC       | WD2500AAJS-07VWA0  | 250 GB | 2       | 2354  | 0     | 6.45   |
| WDC       | WD1002FBYS-01A6B0  | 1 TB   | 13      | 3294  | 2     | 6.39   |
| Toshiba   | MK2002TSKB         | 2 TB   | 9       | 2296  | 3     | 6.29   |
| WDC       | WD6400AAKS-40H2B0  | 640 GB | 10      | 2625  | 84    | 6.26   |
| WDC       | WD5000AAKS-40YGA1  | 500 GB | 2       | 2259  | 0     | 6.19   |
| Hitachi   | HDS724040ALE640    | 4 TB   | 8       | 2332  | 171   | 6.14   |
| WDC       | WD10EACS-00C7B0    | 1 TB   | 6       | 2207  | 0     | 6.05   |
| Hitachi   | HUA722020ALA330    | 2 TB   | 29      | 2720  | 8     | 6.04   |
| WDC       | WD1001FALS-00K1B0  | 1 TB   | 2       | 2199  | 0     | 6.02   |
| Hitachi   | HDS722020ALA330... | 2 TB   | 2       | 2191  | 0     | 6.00   |
| WDC       | WD20EADS-32S2B0    | 2 TB   | 3       | 2484  | 4     | 5.81   |
| WDC       | WD5000ABYS-01TNA0  | 500 GB | 2       | 2117  | 0     | 5.80   |
| Samsung   | HE103UJ            | 1 TB   | 3       | 2992  | 1     | 5.79   |
| WDC       | WD3200AVJB-63J5A0  | 320 GB | 2       | 2113  | 0     | 5.79   |
| WDC       | WD3200AACS-00M6B0  | 320 GB | 2       | 2575  | 5     | 5.73   |
| WDC       | WD3000HLFS-01G6U1  | 304 GB | 2       | 2066  | 0     | 5.66   |
| Hitachi   | HUA723030ALA640... | 3 TB   | 2       | 2062  | 0     | 5.65   |
| WDC       | WD800JD-75MSA1     | 80 GB  | 2       | 2057  | 0     | 5.64   |
| WDC       | WD10EAVS-32D7B1    | 1 TB   | 4       | 2050  | 0     | 5.62   |
| IBM/Hi... | IC35L120AVV207-0   | 128 GB | 2       | 2350  | 1     | 5.59   |
| WDC       | WD3000BLFS-01YBU0  | 304 GB | 6       | 2016  | 0     | 5.52   |
| WDC       | WD10EACS-32ZJB0    | 1 TB   | 4       | 2011  | 0     | 5.51   |
| HP        | GB0500C4413        | 500 GB | 2       | 2009  | 0     | 5.51   |
| Seagate   | ST5000NM0084-1H... | 5 TB   | 2       | 1991  | 0     | 5.46   |
| Seagate   | ST31000340NS EIT   | 1 TB   | 2       | 1989  | 0     | 5.45   |
| WDC       | WD6401AALS-00E8B0  | 640 GB | 7       | 1975  | 0     | 5.41   |
| WDC       | WD1002FBYS-05A6B0  | 1 TB   | 5       | 2597  | 1     | 5.41   |
| Hitachi   | HUA721050KLA330    | 500 GB | 6       | 1973  | 0     | 5.41   |
| WDC       | WD2500KS-22MJB0    | 250 GB | 2       | 1943  | 0     | 5.32   |
| WDC       | WD400BD-55MTA1     | 40 GB  | 2       | 1922  | 0     | 5.27   |
| WDC       | WD5000AAKX-753CA0  | 500 GB | 4       | 1912  | 0     | 5.24   |
| WDC       | WD2502ABYS-18B7A0  | 250 GB | 7       | 2137  | 2     | 5.20   |
| Seagate   | ST3160828AS        | 160 GB | 2       | 1874  | 0     | 5.14   |
| Hitachi   | HDS723030ALA640    | 3 TB   | 32      | 2117  | 51    | 4.92   |
| WDC       | WD80PUZX-64NEAY0   | 8 TB   | 4       | 1788  | 0     | 4.90   |
| WDC       | WD2500BMVV-11DCLS0 | 250 GB | 3       | 1781  | 0     | 4.88   |
| Seagate   | ST6000DM001-1XY17Z | 6 TB   | 3       | 1778  | 0     | 4.87   |
| WDC       | WD1500HLFS-01G6U0  | 150 GB | 4       | 1805  | 1     | 4.87   |
| HP        | GB0250EAFYK        | 250 GB | 3       | 2106  | 45    | 4.85   |
| WDC       | WD20NPVX-00EA4T0   | 2 TB   | 31      | 1949  | 2     | 4.84   |
| WDC       | WD1003FBYX-12      | 1 TB   | 2       | 1766  | 0     | 4.84   |
| WDC       | WD30EURX-63T0FY0   | 3 TB   | 4       | 1953  | 3     | 4.77   |
| WDC       | WD8002FRYZ-01FF2B0 | 8 TB   | 2       | 1735  | 0     | 4.75   |
| Seagate   | ST32000646NS       | 2 TB   | 2       | 1727  | 0     | 4.73   |
| Hitachi   | HDS721025CLA682    | 250 GB | 4       | 1725  | 0     | 4.73   |
| WDC       | WD2502ABYS-01B7A0  | 256 GB | 6       | 2126  | 1     | 4.71   |
| WDC       | WD1001FALS-41K1B0  | 1 TB   | 3       | 1715  | 0     | 4.70   |
| WDC       | WD400JB-00ENA0     | 40 GB  | 3       | 2383  | 6     | 4.69   |
| Hitachi   | HUA722010ALA330    | 1 TB   | 6       | 1982  | 1     | 4.68   |
| WDC       | WD3200KS-00PFB0    | 320 GB | 6       | 1917  | 16    | 4.64   |
| Samsung   | SP0411N            | 40 GB  | 2       | 3755  | 9     | 4.62   |
| Seagate   | ST9500320AS        | 500 GB | 2       | 1684  | 0     | 4.62   |
| WDC       | WD30EURS-63SPKY0   | 3 TB   | 5       | 1681  | 0     | 4.61   |
| WDC       | WD1601ABYS-18C0A0  | 160 GB | 3       | 2303  | 4     | 4.60   |
| HGST      | HUS724020ALE640    | 2 TB   | 13      | 1657  | 0     | 4.54   |
| WDC       | WD2500YS-01SHB0    | 256 GB | 5       | 1693  | 6     | 4.50   |
| Seagate   | ST4000NM0024-1H... | 4 TB   | 7       | 1632  | 0     | 4.47   |
| WDC       | WD3000GLFS-01F8U0  | 304 GB | 7       | 2232  | 165   | 4.47   |
| WDC       | WD5000AAKS-07A7B2  | 500 GB | 3       | 2164  | 7     | 4.45   |
| Seagate   | ST4000VN000-1H4168 | 4 TB   | 33      | 1660  | 62    | 4.43   |
| Hitachi   | HUA721010KLA330... | 1 TB   | 2       | 1886  | 3     | 4.43   |
| WDC       | WD360GD-00FNA0     | 37 GB  | 3       | 2943  | 2     | 4.41   |
| WDC       | WD7500AYYS-01RCA0  | 752 GB | 5       | 1678  | 1     | 4.39   |
| WDC       | WD5000AUDX-57WNHY0 | 500 GB | 2       | 1594  | 0     | 4.37   |
| WDC       | WD3000HLFS-01G6U4  | 304 GB | 5       | 1570  | 0     | 4.30   |
| WDC       | WD2003FYPS-27Y2B0  | 2 TB   | 8       | 1874  | 14    | 4.29   |
| HGST      | HDN724030ALE640    | 3 TB   | 22      | 1565  | 0     | 4.29   |
| WDC       | WD800AAJB-00J3A0   | 80 GB  | 2       | 1562  | 0     | 4.28   |
| WDC       | WD2502ABYS-23B7... | 250 GB | 7       | 1984  | 2     | 4.28   |
| WDC       | WD1003FBYX-88 LEN  | 1 TB   | 4       | 1743  | 1     | 4.27   |
| Toshiba   | MC04ACA200E        | 2 TB   | 2       | 1548  | 0     | 4.24   |
| WDC       | WD5000LUCT-63Y8HY0 | 500 GB | 3       | 1547  | 0     | 4.24   |
| WDC       | WD20EADS-42R6B0    | 2 TB   | 2       | 1547  | 0     | 4.24   |
| WDC       | WD1002FBYS-02A6B0  | 1 TB   | 22      | 1906  | 26    | 4.23   |
| WDC       | WD1001FALS-00Y6A0  | 1 TB   | 13      | 1619  | 37    | 4.23   |
| Hitachi   | HDT721075SLA360    | 752 GB | 3       | 1538  | 0     | 4.22   |
| Seagate   | ST1000NC000-1CX162 | 1 TB   | 4       | 2282  | 223   | 4.18   |
| WDC       | WD2502ABYS-23B7... | 250 GB | 2       | 1522  | 0     | 4.17   |
| WDC       | WD10EACS-00D6B1    | 1 TB   | 9       | 2669  | 219   | 4.11   |
| Hitachi   | HUA721010KLA330    | 1 TB   | 23      | 2013  | 87    | 4.10   |
| WDC       | WD2500AAJS-22VWA0  | 250 GB | 3       | 1496  | 0     | 4.10   |
| HGST      | HUS724020ALA640    | 2 TB   | 56      | 1484  | 0     | 4.07   |
| MaxDig... | MD4000GBDS         | 4 TB   | 2       | 1483  | 0     | 4.07   |
| WDC       | WD15NPVT-00Z2TT0   | 1.5 TB | 4       | 2133  | 19    | 4.06   |
| WDC       | WD2500SD-01KCB0    | 250 GB | 3       | 1973  | 49    | 4.05   |
| WDC       | WD30EFRX-68AX9N0   | 3 TB   | 61      | 1788  | 2     | 4.04   |
| HP        | FB080C4080         | 80 GB  | 2       | 1472  | 0     | 4.04   |
| WDC       | WD1200JB-00REA0    | 120 GB | 2       | 1515  | 1     | 4.03   |
| HGST      | HUH721212ALE601    | 12 TB  | 8       | 1469  | 0     | 4.03   |
| Seagate   | ST4000NM0085-1Y... | 4 TB   | 2       | 1468  | 0     | 4.02   |
| HP        | MB2000GCWDA        | 2 TB   | 7       | 1775  | 2     | 4.02   |
| Seagate   | ST6000NM0024       | 6 TB   | 5       | 1447  | 0     | 3.97   |
| WDC       | WD2500AAKS-61L9A0  | 250 GB | 4       | 1439  | 0     | 3.94   |
| Hitachi   | HUA723020ALA640    | 2 TB   | 33      | 1480  | 1     | 3.94   |
| WDC       | WD1200JS-00SGB0    | 120 GB | 3       | 1437  | 0     | 3.94   |
| WDC       | WD3200AAJS-22RYA0  | 320 GB | 6       | 1471  | 1     | 3.93   |
| WDC       | WD30EURS-73TLHY0   | 3 TB   | 2       | 1435  | 0     | 3.93   |
| Seagate   | ST340212AS         | 40 GB  | 6       | 1654  | 35    | 3.92   |
| WDC       | WD20EARS-42S0XB0   | 2 TB   | 3       | 1425  | 0     | 3.90   |
| WDC       | WD15EARS-32MVWB0   | 1.5 TB | 3       | 1419  | 0     | 3.89   |
| WDC       | WD5000KS-00MNB0    | 500 GB | 2       | 1417  | 0     | 3.88   |
| WDC       | WD2500BMVU-11A04S0 | 250 GB | 2       | 1412  | 0     | 3.87   |
| Seagate   | ST3320820AS_P      | 320 GB | 2       | 1408  | 0     | 3.86   |
| WDC       | WD1500HLFS-01G6U3  | 150 GB | 2       | 1407  | 0     | 3.86   |
| Samsung   | SP1624N            | 160 GB | 3       | 1402  | 0     | 3.84   |
| Seagate   | ST2000NX0253       | 2 TB   | 20      | 1401  | 0     | 3.84   |
| WDC       | WD1001FALS-00J7B0  | 1 TB   | 43      | 1966  | 3     | 3.82   |
| WDC       | WD40EZRX-22SPEB0   | 4 TB   | 6       | 1903  | 3     | 3.81   |
| WDC       | WD3200AAJB-00WGA0  | 320 GB | 4       | 1389  | 0     | 3.81   |
| WDC       | WD10EVDS-63U8B1    | 1 TB   | 3       | 1386  | 0     | 3.80   |
| WDC       | WD740ADFD-00NLR1   | 74 GB  | 2       | 1386  | 0     | 3.80   |
| WDC       | WD2500AAJS-00VWA0  | 250 GB | 2       | 1384  | 0     | 3.79   |
| WDC       | WD40EURX-64WRWY0   | 4 TB   | 3       | 1382  | 0     | 3.79   |
| WDC       | WD8001FFWX-68J1UN0 | 8 TB   | 14      | 1380  | 0     | 3.78   |
| Seagate   | ST4000VM000-1F3168 | 4 TB   | 6       | 1376  | 0     | 3.77   |
| WDC       | WD20EARS-07MVWB0   | 2 TB   | 5       | 1779  | 1     | 3.75   |
| Seagate   | MB3000EBKAB        | 3 TB   | 3       | 1366  | 0     | 3.74   |
| WDC       | WD1500HLFS-50G6U1  | 150 GB | 2       | 1364  | 0     | 3.74   |
| WDC       | WD800HLFS-75G6U1   | 80 GB  | 2       | 1360  | 0     | 3.73   |
| Hitachi   | HCC545025B9A300    | 250 GB | 3       | 1359  | 0     | 3.72   |
| WDC       | WD1600JS-98MHB0    | 160 GB | 2       | 1358  | 0     | 3.72   |
| WDC       | WD1600AAJS-61WAA0  | 160 GB | 4       | 1357  | 0     | 3.72   |
| WDC       | WD6401AALS-00J7B0  | 640 GB | 4       | 1845  | 157   | 3.69   |
| HGST      | HUS726060ALE610    | 6 TB   | 16      | 1339  | 0     | 3.67   |
| WDC       | WD10EADS-67M2B0    | 1 TB   | 3       | 1747  | 9     | 3.67   |
| WDC       | WD5001ABYS-01YNA0  | 500 GB | 4       | 1332  | 0     | 3.65   |
| Seagate   | ST8000VN0002-1Z... | 8 TB   | 5       | 1736  | 21    | 3.65   |
| WDC       | WD5000BTKT-40MD3T0 | 500 GB | 2       | 1326  | 0     | 3.63   |
| WDC       | WD2003FYYS-02W0B0  | 2 TB   | 20      | 2023  | 2     | 3.63   |
| WDC       | WD7501AALS-00E8B0  | 752 GB | 5       | 1832  | 4     | 3.63   |
| WDC       | WD2003FYYS-18W0B0  | 2 TB   | 12      | 2062  | 142   | 3.62   |
| WDC       | WD2001FASS-00W2B0  | 2 TB   | 6       | 1930  | 2     | 3.61   |
| WDC       | WD5003ABYX-18WERA0 | 500 GB | 18      | 1750  | 60    | 3.60   |
| Fujitsu   | MPE3064AT          | 6 GB   | 2       | 1315  | 0     | 3.60   |
| WDC       | WD1600JD-00HBC0    | 160 GB | 3       | 1534  | 2     | 3.60   |
| Hitachi   | HDS722516VLSA80    | 164 GB | 4       | 1529  | 2     | 3.60   |
| WDC       | WD2500AAKX-08ERMA0 | 250 GB | 2       | 1311  | 0     | 3.59   |
| Seagate   | ST91000640NS       | 1 TB   | 31      | 1450  | 2     | 3.56   |
| Seagate   | ST4000VX000-1F4168 | 4 TB   | 2       | 1853  | 3     | 3.56   |
| WDC       | WD10EACS-00D6B0    | 1 TB   | 23      | 1822  | 96    | 3.56   |
| WDC       | WD740GD-00FLA1     | 74 GB  | 2       | 2935  | 20    | 3.52   |
| WDC       | WD3000F9YZ-09N20L0 | 3 TB   | 7       | 1638  | 1     | 3.52   |
| WDC       | WD10EAVS-00D7B0    | 1 TB   | 21      | 1757  | 6     | 3.52   |
| WDC       | WD20EACS-11BHUB0   | 2 TB   | 3       | 1344  | 533   | 3.52   |
| Seagate   | ST320LT014-9YK142  | 320 GB | 2       | 1282  | 0     | 3.51   |
| WDC       | WD20EARX-008FB0    | 2 TB   | 24      | 1546  | 7     | 3.51   |
| Seagate   | ST32000645NS       | 2 TB   | 11      | 1620  | 8     | 3.50   |
| WDC       | WD5000AAKS-00TMA0  | 500 GB | 16      | 1350  | 3     | 3.50   |
| WDC       | WD6400AAKS-41H2B0  | 640 GB | 3       | 1277  | 0     | 3.50   |
| WDC       | WD1001FALS-00U9B0  | 1 TB   | 4       | 2201  | 124   | 3.50   |
| WDC       | WD1000DHTZ-04N21V1 | 1 TB   | 2       | 1270  | 0     | 3.48   |
| Seagate   | ST3000DM001-1E6166 | 3 TB   | 8       | 1457  | 500   | 3.48   |
| Seagate   | ST2000DL004 HD2... | 2 TB   | 9       | 1319  | 1     | 3.48   |
| Hitachi   | HDS723020BLE640    | 2 TB   | 12      | 1263  | 0     | 3.46   |
| WDC       | WD30EZRX-00AZ6B0   | 3 TB   | 7       | 1608  | 40    | 3.44   |
| Toshiba   | MG03ACA200         | 2 TB   | 9       | 1540  | 48    | 3.44   |
| Hitachi   | HDT725040VLA360    | 400 GB | 5       | 1539  | 5     | 3.43   |
| Hitachi   | HTS421212H9AT00    | 120 GB | 2       | 2184  | 120   | 3.43   |
| HPE       | MB4000GEFNA        | 4 TB   | 2       | 2358  | 8     | 3.42   |
| Hitachi   | HDS5C3015ALA632    | 1.5 TB | 4       | 1382  | 80    | 3.42   |
| Hitachi   | HDS723020BLA642    | 2 TB   | 78      | 1476  | 79    | 3.42   |
| WDC       | WD2500HHTZ-04N21V1 | 250 GB | 2       | 1226  | 0     | 3.36   |
| WDC       | WD2000FYYZ-01UL1B2 | 2 TB   | 6       | 1328  | 1     | 3.35   |
| WDC       | WD3200YS-01PGB0    | 320 GB | 4       | 1255  | 1     | 3.35   |
| WDC       | WD3000BLFS-60YBU2  | 304 GB | 7       | 2494  | 3     | 3.34   |
| HGST      | HUH728080ALN600    | 8 TB   | 7       | 1218  | 0     | 3.34   |
| Seagate   | ST3808110AS 41N... | 80 GB  | 2       | 1356  | 1     | 3.34   |
| HGST      | HUS726020ALA610    | 2 TB   | 15      | 1215  | 0     | 3.33   |
| Seagate   | ST310211A          | 10 GB  | 2       | 1214  | 0     | 3.33   |
| Seagate   | ST8000AS0002-1N... | 8 TB   | 115     | 1379  | 57    | 3.32   |
| HGST      | HUS724030ALA640    | 3 TB   | 27      | 1304  | 3     | 3.32   |
| WDC       | WD2002FAEX-007BA0  | 2 TB   | 65      | 1513  | 11    | 3.31   |
| WDC       | WD7501AALS-00J7B1  | 752 GB | 12      | 1353  | 1     | 3.31   |
| WDC       | WD10EACS-00ZJB0    | 1 TB   | 12      | 1585  | 57    | 3.31   |
| WDC       | WD10JPVT-16A1YT0   | 1 TB   | 4       | 1206  | 0     | 3.31   |
| Toshiba   | DT01ABA100         | 1 TB   | 2       | 1201  | 0     | 3.29   |
| WDC       | WD1500HLFS-01G6U1  | 150 GB | 6       | 1200  | 0     | 3.29   |
| WDC       | WD3200AAKS-75SBA0  | 320 GB | 5       | 1200  | 0     | 3.29   |
| Hitachi   | HCS5C1010CLA382    | 1 TB   | 6       | 1195  | 0     | 3.28   |
| HGST      | HDS724040ALE640    | 4 TB   | 15      | 1470  | 139   | 3.27   |
| WDC       | WD2500AAJS-61B4A0  | 250 GB | 2       | 1191  | 0     | 3.27   |
| Seagate   | ST2000VM002-9UY166 | 2 TB   | 3       | 2420  | 125   | 3.26   |
| Hitachi   | HDS722020ALA330    | 2 TB   | 61      | 1875  | 120   | 3.26   |
| Samsung   | HD502HM            | 500 GB | 2       | 1993  | 1     | 3.26   |
| WDC       | WD1600YS-01SHB1    | 164 GB | 8       | 1187  | 0     | 3.25   |
| Hitachi   | HDS722525VLSA80    | 250 GB | 6       | 1261  | 6     | 3.25   |
| Samsung   | HD204UI            | 2 TB   | 94      | 1342  | 55    | 3.25   |
| Hitachi   | HDS721075KLA330    | 752 GB | 10      | 1380  | 10    | 3.24   |
| HGST      | HUS726020ALE614    | 2 TB   | 6       | 1179  | 0     | 3.23   |
| Fujitsu   | MHZ2080BH G2       | 80 GB  | 2       | 1178  | 0     | 3.23   |
| WDC       | WD1600AABS-56PRA0  | 160 GB | 3       | 1178  | 0     | 3.23   |
| HGST      | HDN728080ALE604    | 8 TB   | 5       | 1176  | 0     | 3.22   |
| Hitachi   | HDS728040PLA320    | 40 GB  | 4       | 1548  | 4     | 3.22   |
| WDC       | WD3200AAJB-56WGA0  | 320 GB | 3       | 1172  | 0     | 3.21   |
| WDC       | WD800BB-60JKC0     | 80 GB  | 2       | 1292  | 2     | 3.21   |
| HGST      | HUS724040ALA640    | 4 TB   | 35      | 1272  | 60    | 3.21   |
| Maxtor    | 6N040T0            | 40 GB  | 2       | 1842  | 1     | 3.21   |
| HP        | MB2000EBUCF        | 2 TB   | 3       | 2111  | 4     | 3.21   |
| WDC       | WD5000AAVS-00G9B0  | 500 GB | 8       | 1332  | 1     | 3.21   |
| WDC       | WD1600AAJS-60WAA0  | 160 GB | 9       | 1200  | 113   | 3.20   |
| WDC       | WD15EARS-22Z5B1    | 1.5 TB | 4       | 1168  | 0     | 3.20   |
| HGST      | HMS5C4040ALE640    | 4 TB   | 8       | 1165  | 0     | 3.19   |
| HGST      | HDN724040ALE640    | 4 TB   | 36      | 1226  | 57    | 3.18   |
| Seagate   | ST9250610NS        | 250 GB | 7       | 1159  | 0     | 3.18   |
| WDC       | WD6000HLHX-75JJPV0 | 600 GB | 4       | 1936  | 3     | 3.18   |
| WDC       | WD20EARX-32PASB0   | 2 TB   | 10      | 1173  | 1     | 3.17   |
| Toshiba   | MG04ACA100N        | 1 TB   | 4       | 1154  | 0     | 3.16   |
| WDC       | WD80PURZ-85YNPY0   | 8 TB   | 2       | 1145  | 0     | 3.14   |
| WDC       | WD3200AAKS-22SBA0  | 320 GB | 3       | 1144  | 0     | 3.14   |
| WDC       | WD1003FBYX-18Y7B0  | 1 TB   | 6       | 1621  | 5     | 3.13   |
| WDC       | WD10EAVS-22D7B0    | 1 TB   | 4       | 1775  | 4     | 3.13   |
| HGST      | HDN726060ALE610    | 6 TB   | 18      | 1193  | 38    | 3.12   |
| WDC       | WD2500JS-00MHB0    | 250 GB | 6       | 1191  | 1     | 3.12   |
| WDC       | WD5002ABYS-02B1B0  | 500 GB | 17      | 1383  | 14    | 3.12   |
| WDC       | WD7500AACS-00D6B0  | 752 GB | 3       | 1244  | 3     | 3.12   |
| WDC       | WD10EADS-00L5B1    | 1 TB   | 110     | 1633  | 9     | 3.11   |
| WDC       | WD5003AZEX-00RKKA0 | 500 GB | 2       | 1135  | 0     | 3.11   |
| Seagate   | ST3300822AS        | 304 GB | 3       | 1338  | 802   | 3.11   |
| WDC       | WD2500JS-41SGB0    | 250 GB | 2       | 1132  | 0     | 3.10   |
| WDC       | WD10EZEX-07ZF5A0   | 1 TB   | 5       | 1371  | 3     | 3.09   |
| Seagate   | ST4000VN0001-1S... | 4 TB   | 3       | 1128  | 0     | 3.09   |
| WDC       | WD7500AALX-009BA0  | 752 GB | 9       | 1125  | 0     | 3.08   |
| WDC       | WD10EZEX-75ZF5A0   | 1 TB   | 22      | 1239  | 109   | 3.08   |
| WDC       | WD10EALX-759BA0    | 1 TB   | 5       | 1466  | 2     | 3.08   |
| WDC       | WD4000F9YZ-09N20L1 | 4 TB   | 3       | 1122  | 0     | 3.08   |
| WDC       | WD1001FALS-00J7B1  | 1 TB   | 39      | 1672  | 29    | 3.07   |
| WDC       | WD3200AAKS-00G3A0  | 320 GB | 7       | 1120  | 0     | 3.07   |
| WDC       | WD2000F9YZ-09N20L0 | 2 TB   | 9       | 1221  | 12    | 3.06   |
| WDC       | WD2500JS-40MVB1    | 250 GB | 2       | 1115  | 0     | 3.06   |
| Seagate   | ST4000DM006-2G5107 | 4 TB   | 4       | 1115  | 0     | 3.05   |
| WDC       | WD3000HLFS-01G6U3  | 304 GB | 2       | 1113  | 0     | 3.05   |
| Hitachi   | HDS721010CLA630    | 1 TB   | 25      | 1449  | 123   | 3.05   |
| WDC       | WD10TMVW-11ZSMS5   | 1 TB   | 22      | 1293  | 179   | 3.05   |
| Toshiba   | MG03ACA300         | 3 TB   | 9       | 1429  | 6     | 3.04   |
| WDC       | WD5001FZWX-00ZHUA0 | 5 TB   | 7       | 1587  | 18    | 3.04   |
| WDC       | WD800JD-55MSA1     | 80 GB  | 5       | 1109  | 0     | 3.04   |
| WDC       | WD1002FAEX-00Y9A0  | 1 TB   | 86      | 1294  | 10    | 3.04   |
| Hitachi   | HUA722020ALA331    | 2 TB   | 30      | 1771  | 5     | 3.03   |
| WDC       | WD1600AAJS-08WAA0  | 160 GB | 3       | 1291  | 1     | 3.02   |
| WDC       | WD3003FZEX-00Z4SA0 | 3 TB   | 14      | 1215  | 73    | 3.00   |
| Seagate   | ST6000NM0115-1Y... | 6 TB   | 92      | 1094  | 0     | 3.00   |
| WDC       | WD3200KS-75PFB0    | 320 GB | 2       | 1365  | 39    | 3.00   |
| WDC       | WD30EZRX-22D8PB0   | 3 TB   | 8       | 1183  | 1     | 3.00   |
| Samsung   | HE253GJ            | 250 GB | 2       | 2131  | 1     | 2.99   |
| WDC       | WD5000AAVS-00ZTB0  | 500 GB | 22      | 1410  | 68    | 2.99   |
| WDC       | WD1001FALS-41Y6A0  | 1 TB   | 5       | 1202  | 1     | 2.99   |
| WDC       | WD10SPCX-00KHST0   | 1 TB   | 2       | 1089  | 0     | 2.99   |
| Hitachi   | HDS5C3030ALA630    | 3 TB   | 12      | 1475  | 2     | 2.97   |
| WDC       | WD1200JD-00HBB0    | 120 GB | 11      | 1699  | 122   | 2.97   |
| Hitachi   | HDT722520DLAT80    | 200 GB | 4       | 1084  | 0     | 2.97   |
| WDC       | WD5000AAKS-402AA0  | 500 GB | 8       | 1532  | 9     | 2.97   |
| WDC       | WD1001FALS-40U9B0  | 1 TB   | 5       | 1220  | 1     | 2.97   |
| Toshiba   | MQ03ABB200         | 2 TB   | 2       | 1079  | 0     | 2.96   |
| WDC       | WD80EFAX-68LHPN0   | 8 TB   | 28      | 1079  | 0     | 2.96   |
| WDC       | WD2500JS-60NCB1    | 250 GB | 11      | 1142  | 1     | 2.96   |
| Maxtor    | 7V250F0            | 256 GB | 2       | 1075  | 0     | 2.95   |
| WDC       | WD6400BPVT-16HXZT1 | 640 GB | 3       | 1465  | 3     | 2.95   |
| WDC       | WD1004FBYZ-23YC    | 1 TB   | 4       | 1074  | 0     | 2.94   |
| Seagate   | ST1000NX0423 00... | 1 TB   | 5       | 1073  | 0     | 2.94   |
| WDC       | WD5000AAKS-00V2B0  | 500 GB | 4       | 1202  | 1     | 2.94   |
| WDC       | WD360ADFD-00NLR1   | 37 GB  | 2       | 1073  | 0     | 2.94   |
| Hitachi   | HUA723030ALA640    | 3 TB   | 42      | 1369  | 54    | 2.94   |
| WDC       | WD15EVDS-63V9B1    | 1.5 TB | 3       | 1581  | 4     | 2.94   |
| Maxtor    | 6V300F0            | 304 GB | 4       | 1071  | 0     | 2.94   |
| Maxtor    | 6L020J1            | 20 GB  | 3       | 1213  | 2     | 2.93   |
| Hitachi   | HDT725032VLA380    | 320 GB | 21      | 1492  | 66    | 2.93   |
| Toshiba   | HDWA130            | 3 TB   | 5       | 1069  | 0     | 2.93   |
| Seagate   | ST2000NC001-1DY164 | 2 TB   | 8       | 1068  | 0     | 2.93   |
| Seagate   | ST3300622AS        | 304 GB | 4       | 1477  | 1     | 2.92   |
| Seagate   | ST32000641AS       | 2 TB   | 30      | 1625  | 151   | 2.92   |
| WDC       | WD20EURX-57T0FY1   | 2 TB   | 2       | 1064  | 0     | 2.92   |
| Hitachi   | HDS721075CLA332    | 752 GB | 7       | 1275  | 290   | 2.91   |
| WDC       | WD4000AAKS-00YGA0  | 400 GB | 7       | 1233  | 1     | 2.91   |
| Seagate   | ST10000DM0004      | 10 TB  | 3       | 1059  | 0     | 2.90   |
| Seagate   | ST3000VX000-1ES166 | 3 TB   | 6       | 1059  | 0     | 2.90   |
| Hitachi   | HDS5C3030BLE630    | 3 TB   | 5       | 1059  | 0     | 2.90   |
| Seagate   | ST500DM002-1ER14C  | 500 GB | 4       | 1057  | 0     | 2.90   |
| Fujitsu   | MHV2040BH          | 40 GB  | 3       | 1057  | 0     | 2.90   |
| WDC       | WD2500AAJS-75VWA0  | 250 GB | 3       | 1056  | 0     | 2.89   |
| Hitachi   | HCS5C2020ALA632    | 2 TB   | 4       | 1772  | 3     | 2.89   |
| Toshiba   | MG04ACA600EY       | 6 TB   | 3       | 1055  | 0     | 2.89   |
| Maxtor    | STM3320620AS       | 320 GB | 3       | 1055  | 0     | 2.89   |
| Hitachi   | HDS722580VLAT20    | 82 GB  | 5       | 1285  | 108   | 2.89   |
| WDC       | WD6002FZWX-00GBGB0 | 6 TB   | 2       | 1675  | 2     | 2.88   |
| WDC       | WD2500JS-00MHB1    | 250 GB | 2       | 1052  | 0     | 2.88   |
| WDC       | WD2502ABYS-02B7A0  | 256 GB | 8       | 1337  | 11    | 2.88   |
| WDC       | WD2500YD-01NVB1    | 256 GB | 3       | 1428  | 2     | 2.88   |
| WDC       | WD10EALX-759BA1    | 1 TB   | 14      | 1491  | 178   | 2.88   |
| Hitachi   | HDS725050KLA360    | 500 GB | 16      | 1985  | 29    | 2.88   |
| WDC       | WD3000BLFS-08YBU0  | 304 GB | 2       | 1048  | 0     | 2.87   |
| HGST      | HMS5C4040BLE640    | 4 TB   | 18      | 1048  | 0     | 2.87   |
| Seagate   | ST6000AS0002-1N... | 6 TB   | 12      | 1515  | 67    | 2.85   |
| WDC       | WD10EAVS-00M4B0    | 1 TB   | 2       | 1038  | 0     | 2.84   |
| WDC       | WD20EFRX-68AX9N0   | 2 TB   | 40      | 1425  | 2     | 2.84   |
| Apple     | HDD ST3000DM001    | 3 TB   | 2       | 1034  | 0     | 2.84   |
| WDC       | WD800BB-75FRA0     | 80 GB  | 2       | 1034  | 0     | 2.83   |
| Seagate   | ST3500630NS        | 500 GB | 16      | 1311  | 295   | 2.83   |
| Hitachi   | HCC543225A7A380    | 250 GB | 5       | 1314  | 1     | 2.83   |
| WDC       | WD5000AAKS-40V2B0  | 500 GB | 2       | 1031  | 0     | 2.83   |
| Hitachi   | HDS721010CLA632    | 1 TB   | 18      | 1433  | 8     | 2.82   |
| WDC       | WD5000AAKS-22YGA0  | 500 GB | 9       | 1195  | 51    | 2.82   |
| Seagate   | ST2000NM0033-9Z... | 2 TB   | 21      | 1138  | 75    | 2.81   |
| WDC       | WD2000FYYZ-01UL1B0 | 2 TB   | 5       | 1244  | 1     | 2.81   |
| Hitachi   | HUA722010CLA331    | 1 TB   | 3       | 1365  | 222   | 2.81   |
| Seagate   | ST320413A          | 20 GB  | 2       | 1076  | 2     | 2.80   |
| WDC       | WD800JD-60LUA0     | 80 GB  | 3       | 1020  | 0     | 2.80   |
| WDC       | WD800JD-08LSA0     | 80 GB  | 13      | 1129  | 2     | 2.79   |
| WDC       | WD400LB-00DNA0     | 40 GB  | 2       | 1103  | 2     | 2.78   |
| WDC       | WD1600AAJS-22PSA0  | 160 GB | 19      | 1157  | 26    | 2.78   |
| WDC       | WD5000AACS-61M6B2  | 500 GB | 3       | 2013  | 4     | 2.78   |
| WDC       | WD3200AAKS-75B3A0  | 320 GB | 3       | 1590  | 1     | 2.78   |
| Seagate   | ST31000521AS       | 1 TB   | 2       | 1010  | 0     | 2.77   |
| WDC       | WD1002F9YZ-09H1JL1 | 1 TB   | 8       | 1009  | 0     | 2.77   |
| Toshiba   | MD04ACA400         | 4 TB   | 31      | 1226  | 243   | 2.76   |
| WDC       | WD6400AAKS-65A7B2  | 640 GB | 29      | 1490  | 19    | 2.75   |
| WDC       | WD2002FYPS-01U1B0  | 2 TB   | 5       | 2628  | 105   | 2.75   |
| WDC       | WD1600AABS-61PRA0  | 160 GB | 3       | 1341  | 1     | 2.75   |
| WDC       | WD2500JS-75NCB3    | 250 GB | 9       | 1309  | 15    | 2.75   |
| WDC       | WD20EARX-00ZUDB0   | 2 TB   | 4       | 1492  | 5     | 2.75   |
| WDC       | WD25EZRX-00MMMB0   | 2.5 TB | 6       | 1880  | 6     | 2.74   |
| WDC       | WD6001FZWX-00A2VA0 | 6 TB   | 12      | 1073  | 1     | 2.74   |
| Toshiba   | MK3255GSXF         | 320 GB | 2       | 1185  | 1     | 2.74   |
| Hitachi   | HDE721010SLA330    | 1 TB   | 13      | 1855  | 15    | 2.74   |
| Seagate   | ST3500630AS        | 500 GB | 79      | 1505  | 204   | 2.73   |
| Seagate   | ST1500LM003-9YH148 | 1.5 TB | 2       | 996   | 0     | 2.73   |
| Seagate   | ST3400833AS        | 400 GB | 2       | 996   | 0     | 2.73   |
| WDC       | WD5000AAKS-65A7B2  | 500 GB | 3       | 996   | 0     | 2.73   |
| WDC       | WD2000FYYZ-05UL1B0 | 2 TB   | 2       | 996   | 0     | 2.73   |
| WDC       | WD20EARX-00PASB0   | 2 TB   | 258     | 1260  | 83    | 2.73   |
| WDC       | WD30EZRX-00MMMB0   | 3 TB   | 61      | 1307  | 34    | 2.73   |
| HGST      | HUH721010ALN600    | 10 TB  | 5       | 995   | 0     | 2.73   |
| Seagate   | ST3500414CS        | 500 GB | 33      | 1262  | 112   | 2.72   |
| WDC       | WD4002FYYZ-01B7CB1 | 4 TB   | 6       | 993   | 0     | 2.72   |
| WDC       | WD3200JS-63PDB1    | 320 GB | 3       | 1327  | 217   | 2.71   |
| WDC       | WD1001FALS-00E3A0  | 1 TB   | 8       | 1483  | 207   | 2.71   |
| Seagate   | ST3500630AS P      | 500 GB | 2       | 988   | 0     | 2.71   |
| WDC       | WD6401AALS-00L3B2  | 640 GB | 32      | 1370  | 4     | 2.71   |
| Seagate   | ST3000NM0033-9Z... | 3 TB   | 9       | 1084  | 2     | 2.71   |
| Hitachi   | HDT725025VLA380    | 250 GB | 28      | 1274  | 19    | 2.70   |
| WDC       | WD7500BPVT-35HXZT3 | 752 GB | 3       | 1069  | 2     | 2.70   |
| WDC       | WD5001AALS-00E3A0  | 500 GB | 19      | 1478  | 65    | 2.69   |
| WDC       | WD6400AACS-00G8B0  | 640 GB | 9       | 1126  | 72    | 2.69   |
| WDC       | WD20EURX-57T0FY0   | 2 TB   | 2       | 981   | 0     | 2.69   |
| WDC       | WD2003FZEX-00Z4SA0 | 2 TB   | 71      | 1175  | 20    | 2.69   |
| Seagate   | ST4000VN000-2AH166 | 4 TB   | 4       | 978   | 0     | 2.68   |
| Seagate   | ST3320413CS        | 320 GB | 16      | 1089  | 72    | 2.67   |
| WDC       | WD5000AAKS-22TMA0  | 500 GB | 3       | 973   | 0     | 2.67   |
| WDC       | WD1600AAJB-56R1A0  | 160 GB | 3       | 1041  | 3     | 2.67   |
| WDC       | WD1002FAEX-00Z3A0  | 1 TB   | 163     | 1246  | 56    | 2.66   |
| HGST      | HUS726040ALE614    | 4 TB   | 8       | 970   | 0     | 2.66   |
| WDC       | WD1001FALS-00E8B0  | 1 TB   | 19      | 1394  | 119   | 2.66   |
| WDC       | WD10EADS-00P8B0    | 1 TB   | 12      | 1438  | 26    | 2.66   |
| Toshiba   | DT01ABA050V        | 500 GB | 2       | 969   | 0     | 2.66   |
| WDC       | WD1002FBYS-18W8B0  | 1 TB   | 4       | 1397  | 1     | 2.65   |
| WDC       | WD2500AAJS-75M0A0  | 250 GB | 27      | 1120  | 76    | 2.64   |
| WDC       | WD7500KMVV-11TK7S1 | 752 GB | 2       | 964   | 0     | 2.64   |
| Seagate   | ST3000VN000-1HJ166 | 3 TB   | 16      | 963   | 0     | 2.64   |
| WDC       | WD5000AAKS-00YGA0  | 500 GB | 27      | 1173  | 3     | 2.64   |
| WDC       | WD10EARS-003BB1    | 1 TB   | 19      | 1063  | 91    | 2.63   |
| Seagate   | ST1000NM0095-2D... | 1 TB   | 4       | 1306  | 509   | 2.63   |
| Toshiba   | MG04ACA400E        | 4 TB   | 15      | 958   | 0     | 2.62   |
| WDC       | WD1600AAJS-08B4A0  | 160 GB | 2       | 957   | 0     | 2.62   |
| WDC       | WD20NMVW-11W68S0   | 2 TB   | 9       | 1152  | 10    | 2.62   |
| Hitachi   | HDT722520DLA380    | 200 GB | 5       | 1127  | 2     | 2.62   |
| Toshiba   | MG03ACA400         | 4 TB   | 9       | 1169  | 1     | 2.61   |
| WDC       | WD3000HLFS-01G6U0  | 304 GB | 2       | 953   | 0     | 2.61   |
| WDC       | WD10EURX-63C57Y0   | 1 TB   | 14      | 1138  | 1     | 2.60   |
| WDC       | WD1600BB-22RDA0    | 160 GB | 2       | 947   | 0     | 2.60   |
| WDC       | WD2500AAKX-22ERMA0 | 250 GB | 2       | 946   | 0     | 2.59   |
| Seagate   | ST500LX003-1AC15G  | 500 GB | 4       | 1051  | 8     | 2.58   |
| WDC       | WD20EURS-63S48Y0   | 2 TB   | 14      | 1244  | 147   | 2.58   |
| WDC       | WD30EFRX-68EUZN0   | 3 TB   | 259     | 1150  | 5     | 2.58   |
| WDC       | WD20EADS-11R6B1    | 2 TB   | 2       | 1646  | 8     | 2.58   |
| WDC       | WD10EZEX-00KUWA0   | 1 TB   | 48      | 1061  | 1     | 2.57   |
| WDC       | WD800JD-60LSA5     | 80 GB  | 27      | 984   | 1     | 2.57   |
| WDC       | WD5000AACS-00ZUB0  | 500 GB | 24      | 1067  | 5     | 2.57   |
| Toshiba   | MD04ABA400V        | 4 TB   | 3       | 936   | 0     | 2.57   |
| Hitachi   | HDS5C3020BLE630    | 2 TB   | 12      | 1338  | 115   | 2.57   |
| Hitachi   | HDS5C3020ALA632    | 2 TB   | 30      | 1238  | 21    | 2.57   |
| Seagate   | ST3320620NS        | 320 GB | 5       | 1540  | 2     | 2.56   |
| WDC       | WD5000AAKB-00YSA0  | 500 GB | 2       | 935   | 0     | 2.56   |
| Hitachi   | HDS723015BLA642    | 1.5 TB | 10      | 1088  | 20    | 2.56   |
| WDC       | WD30EZRX-00DC0B0   | 3 TB   | 80      | 1138  | 38    | 2.56   |
| WDC       | WD5000BPKT-08PK4T0 | 500 GB | 3       | 932   | 0     | 2.56   |
| Seagate   | ST500LM024-1RS152  | 500 GB | 2       | 932   | 0     | 2.56   |
| WDC       | WD1003FBYX-01Y7B0  | 1 TB   | 25      | 1501  | 87    | 2.55   |
| WDC       | WD10EFRX-68JCSN0   | 1 TB   | 38      | 1223  | 101   | 2.55   |
| Seagate   | ST4000DM000-1F2168 | 4 TB   | 170     | 1112  | 122   | 2.54   |
| Samsung   | HD400LD            | 400 GB | 5       | 1135  | 150   | 2.54   |
| Seagate   | ST8000VN0022-2E... | 8 TB   | 78      | 1020  | 5     | 2.54   |
| Toshiba   | DT01ABA200V        | 2 TB   | 5       | 976   | 34    | 2.53   |
| WDC       | WD1600JS-55MHB1    | 160 GB | 3       | 924   | 0     | 2.53   |
| WDC       | WD30EZRX-00SPEB0   | 3 TB   | 35      | 1077  | 9     | 2.53   |
| WDC       | WD1600HLFS-75G6U1  | 160 GB | 4       | 923   | 0     | 2.53   |
| Hitachi   | HDS721016CLA382    | 160 GB | 14      | 1200  | 73    | 2.52   |
| WDC       | WD1600JB-00REA0    | 160 GB | 9       | 1095  | 133   | 2.52   |
| WDC       | WD1001FALS-41Y6A1  | 1 TB   | 3       | 1078  | 3     | 2.52   |
| WDC       | WD3202ABYS-02B7A0  | 320 GB | 8       | 1039  | 11    | 2.51   |
| WDC       | WD20EADS-00S2B0    | 2 TB   | 12      | 1246  | 87    | 2.51   |
| WDC       | WD5000BMVV-11A1CS0 | 500 GB | 4       | 1181  | 47    | 2.51   |
| Toshiba   | MK2561GSY          | 250 GB | 2       | 913   | 0     | 2.50   |
| WDC       | WD3200BEVT-75ZCT1  | 320 GB | 2       | 1749  | 2     | 2.50   |
| WDC       | WD6400AAKS-75A7B2  | 640 GB | 9       | 1024  | 3     | 2.50   |
| WDC       | WD3200AAVS-00ZTB0  | 320 GB | 2       | 1145  | 1     | 2.49   |
| WDC       | WD800JB-00FMA0     | 80 GB  | 2       | 1099  | 343   | 2.49   |
| WDC       | WD20EARX-00MMMB0   | 2 TB   | 4       | 1284  | 4     | 2.49   |
| Seagate   | ST4000NM0033-9Z... | 4 TB   | 40      | 1531  | 365   | 2.49   |
| WDC       | WD40EFRX-68WT0N0   | 4 TB   | 178     | 1241  | 6     | 2.48   |
| WDC       | WD5002ABYS-01B1B0  | 500 GB | 17      | 1398  | 3     | 2.48   |
| WDC       | WD2500JS-60NCB2    | 250 GB | 3       | 903   | 0     | 2.47   |
| Seagate   | ST3000DM003-1F216N | 3 TB   | 6       | 1255  | 27    | 2.47   |
| Seagate   | ST3500418ASQ       | 500 GB | 4       | 1387  | 259   | 2.47   |
| WDC       | WD1600BB-00RDA0    | 160 GB | 4       | 1124  | 20    | 2.47   |
| WDC       | WD3200LPVX-00V0TT0 | 320 GB | 3       | 900   | 0     | 2.47   |
| WDC       | WD10EZEX-08RKKA0   | 1 TB   | 10      | 900   | 0     | 2.47   |
| Seagate   | ST3500641AS        | 500 GB | 10      | 1517  | 225   | 2.47   |
| WDC       | WD6400AAKS-00A7B0  | 640 GB | 18      | 1040  | 3     | 2.46   |
| Hitachi   | HUS724040ALE640    | 4 TB   | 6       | 930   | 64    | 2.45   |
| WDC       | WD1600AABS-00PRA0  | 160 GB | 5       | 894   | 0     | 2.45   |
| WDC       | WD7500BPKX-75HPJT0 | 752 GB | 9       | 894   | 0     | 2.45   |
| WDC       | WD20EARS-00J2GB0   | 2 TB   | 14      | 1596  | 107   | 2.44   |
| WDC       | WD20EARX-22PASB0   | 2 TB   | 7       | 1221  | 2     | 2.44   |
| Seagate   | ST3000NC002-1DY166 | 3 TB   | 5       | 1190  | 598   | 2.44   |
| Hitachi   | HUA722050CLA330    | 500 GB | 4       | 891   | 0     | 2.44   |
| WDC       | WD10EARX-22N0YB0   | 1 TB   | 3       | 1079  | 697   | 2.44   |
| WDC       | WD1002FBYS-18A6B0  | 1 TB   | 4       | 1935  | 15    | 2.43   |
| HGST      | HTE541010A9E680    | 1 TB   | 2       | 913   | 509   | 2.43   |
| WDC       | WD2500AAJS-55RYA0  | 250 GB | 2       | 887   | 0     | 2.43   |
| WDC       | WD1003FZEX-00RLFA0 | 1 TB   | 3       | 886   | 0     | 2.43   |
| WDC       | WD3200AAJB-00TYA0  | 320 GB | 4       | 885   | 0     | 2.43   |
| WDC       | WD1005FBYZ-01YCBB1 | 1 TB   | 6       | 883   | 0     | 2.42   |
| WDC       | WD80EFZX-68UW8N0   | 8 TB   | 26      | 930   | 1     | 2.42   |
| Seagate   | ST3320413AS        | 320 GB | 31      | 1139  | 28    | 2.42   |
| Maxtor    | 7H500F0            | 500 GB | 7       | 931   | 1     | 2.41   |
| WDC       | WD3200JD-00KLB0    | 320 GB | 2       | 879   | 0     | 2.41   |
| Hitachi   | HDE721064SLA360    | 640 GB | 4       | 1234  | 4     | 2.41   |
| Hitachi   | HUA723020ALA641    | 2 TB   | 61      | 1090  | 40    | 2.40   |
| Samsung   | HD083GJ            | 80 GB  | 6       | 876   | 0     | 2.40   |
| Seagate   | ST3160215ACE       | 160 GB | 8       | 1206  | 585   | 2.40   |
| Seagate   | ST2000VN000-1HJ164 | 2 TB   | 9       | 874   | 0     | 2.40   |
| WDC       | WD1600BB-56RDA0    | 160 GB | 3       | 874   | 0     | 2.40   |
| WDC       | WD20EZRX-00DC0B0   | 2 TB   | 80      | 1065  | 22    | 2.40   |
| HGST      | HUS722T2TALA604    | 2 TB   | 8       | 873   | 0     | 2.39   |
| WDC       | WD1002FAEX-007BA0  | 1 TB   | 6       | 907   | 1     | 2.39   |
| WDC       | WD3200AAKS-75VYA0  | 320 GB | 4       | 870   | 0     | 2.39   |
| WDC       | WD2500YS-01SHB1    | 250 GB | 13      | 1172  | 10    | 2.39   |
| WDC       | WD10EADS-65M2B0    | 1 TB   | 15      | 1175  | 78    | 2.38   |
| WDC       | WD6400AACS-00G8B1  | 640 GB | 15      | 1181  | 18    | 2.38   |
| WDC       | WD1200JS-55NCB1    | 120 GB | 2       | 869   | 0     | 2.38   |
| WDC       | WD6400AAKS-22A7B0  | 640 GB | 25      | 1274  | 44    | 2.38   |
| Samsung   | HD203WI            | 2 TB   | 9       | 915   | 2     | 2.37   |
| Magnet... | MD05000-BQDW-RO    | 500 GB | 2       | 865   | 0     | 2.37   |
| WDC       | WD5000AZDX-00SC2B0 | 500 GB | 7       | 1062  | 8     | 2.37   |
| WDC       | WD6400AAVS-00G9B1  | 640 GB | 3       | 1491  | 95    | 2.37   |
| Seagate   | ST3000VX000-1CU166 | 3 TB   | 10      | 863   | 6     | 2.36   |
| Hitachi   | HDS5C1010CLA382    | 1 TB   | 15      | 1111  | 33    | 2.36   |
| WDC       | WD30EZRX-00D8PB0   | 3 TB   | 87      | 931   | 10    | 2.36   |
| Apple     | HDD HTS727575A9... | 752 GB | 5       | 860   | 0     | 2.36   |
| Seagate   | ST4000NM0245-1Z... | 4 TB   | 9       | 1079  | 2     | 2.36   |
| HGST      | HUS726060ALE614    | 6 TB   | 10      | 884   | 57    | 2.36   |
| WDC       | WD7500AAKS-00RBA0  | 752 GB | 17      | 1229  | 32    | 2.35   |
| WDC       | WD5000HHTZ-04N21V0 | 500 GB | 11      | 1036  | 9     | 2.35   |
| WDC       | WD1600AAJS-75WAA0  | 160 GB | 3       | 857   | 0     | 2.35   |
| Seagate   | ST3000VN007-2E4166 | 3 TB   | 19      | 855   | 0     | 2.34   |
| WDC       | WD800AAJS-22PSA0   | 80 GB  | 4       | 852   | 0     | 2.33   |
| WDC       | WD1600AAJS-60PSA0  | 160 GB | 5       | 989   | 206   | 2.33   |
| WDC       | WD2500JS-55NCB1    | 250 GB | 9       | 1083  | 11    | 2.33   |
| WDC       | WD800JD-75MSA3     | 80 GB  | 48      | 1135  | 27    | 2.33   |
| Seagate   | ST10000NM0016-1... | 10 TB  | 19      | 843   | 0     | 2.31   |
| WDC       | WD3200AAKS-00YGA0  | 320 GB | 5       | 933   | 1     | 2.31   |
| Samsung   | HE103SJ            | 1 TB   | 6       | 2421  | 24    | 2.31   |
| WDC       | WD4001FFSX-68JNUN0 | 4 TB   | 7       | 1294  | 53    | 2.31   |
| WDC       | WD10JMVW-59AJGS3   | 1 TB   | 2       | 840   | 0     | 2.30   |
| Seagate   | ST9500620NS        | 500 GB | 5       | 1317  | 6     | 2.30   |
| Seagate   | ST33000651NS       | 3 TB   | 11      | 1614  | 128   | 2.30   |
| WDC       | WD20EZRX-00D8PB0   | 2 TB   | 185     | 928   | 34    | 2.30   |
| WDC       | WD6002FFWX-68TZ4N0 | 6 TB   | 5       | 838   | 0     | 2.30   |
| WDC       | WD40EZRX-00SPEB0   | 4 TB   | 76      | 969   | 28    | 2.30   |
| WDC       | WD20EADS-00W4B0    | 2 TB   | 2       | 837   | 0     | 2.29   |
| WDC       | WD7501AALS-00J7B0  | 752 GB | 26      | 1246  | 126   | 2.29   |
| WDC       | WD10EALX-089BA0    | 1 TB   | 2       | 836   | 0     | 2.29   |
| WDC       | WD3200AAJS-60M0A0  | 320 GB | 7       | 1053  | 1     | 2.29   |
| Seagate   | ST4000DX001-1CE168 | 4 TB   | 26      | 1002  | 33    | 2.28   |
| WDC       | WD6401AALS-00J7B1  | 640 GB | 2       | 1083  | 4     | 2.28   |
| WDC       | WD1600JS-60MHB1    | 160 GB | 7       | 975   | 4     | 2.28   |

HDD by Vendor
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF |
|-------------|--------|---------|-------|-------|------|
| HP          | 20     | 83      | 1463  | 73    | 2.51   |
| MaxDigital  | 2      | 4       | 869   | 2     | 2.21   |
| HPE         | 3      | 8       | 910   | 3     | 1.50   |
| WDC         | 1543   | 26402   | 691   | 39    | 1.38   |
| Apple       | 16     | 243     | 616   | 53    | 1.36   |
| Magnetic... | 2      | 4       | 488   | 0     | 1.34   |
| ExcelStor   | 3      | 21      | 802   | 62    | 1.27   |
| Hitachi     | 234    | 6014    | 791   | 195   | 1.26   |
| Samsung     | 121    | 3486    | 846   | 231   | 1.20   |
| Seagate     | 598    | 27474   | 624   | 175   | 1.07   |
| HGST        | 79     | 3287    | 527   | 248   | 1.02   |
| Toshiba     | 229    | 9046    | 424   | 98    | 0.84   |
| Fujitsu     | 69     | 856     | 383   | 103   | 0.65   |
| Maxtor      | 82     | 779     | 513   | 258   | 0.64   |
| IBM/Hitachi | 13     | 44      | 614   | 37    | 0.59   |
| MediaMax    | 8      | 16      | 396   | 88    | 0.50   |
| China       | 1      | 2       | 155   | 0     | 0.43   |
| IBM         | 1      | 2       | 1494  | 37    | 0.39   |
| Lenovo      | 2      | 6       | 91    | 0     | 0.25   |
| MARSHAL     | 2      | 6       | 259   | 434   | 0.13   |
| Synology    | 1      | 7       | 39    | 0     | 0.11   |
| CLOVER      | 1      | 2       | 29    | 0     | 0.08   |

SSD by Model
------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

See full list of tested SSD samples in the Appendix 2 ([All_SSD.md](/All_SSD.md)).

See top 1000 of tested SSD models in the [Top1000_SSD.md](/Top1000_SSD.md).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| Intel     | SSDSA2SH064G1GC    | 64 GB  | 2       | 2956  | 0     | 8.10   |
| Transcend | 3E128-TS2-550B01   | 100 GB | 16      | 3197  | 1     | 7.88   |
| Samsung   | MO0200EBTJU        | 200 GB | 2       | 2807  | 0     | 7.69   |
| Corsair   | Force GT           | 50 GB  | 2       | 2183  | 0     | 5.98   |
| Samsung   | MZ7PD480HAGM-000DA | 480 GB | 2       | 2086  | 0     | 5.72   |
| Samsung   | MZ7WD240HCFV-00003 | 240 GB | 2       | 1938  | 0     | 5.31   |
| Intel     | SSDSC2BB240G4      | 240 GB | 5       | 1885  | 0     | 5.17   |
| Intel     | SSDSC2BB600G4      | 600 GB | 4       | 1855  | 0     | 5.08   |
| Intel     | SSDSC2BB800G4      | 800 GB | 2       | 1780  | 0     | 4.88   |
| Kingston  | SNVP325S2128GB     | 128 GB | 2       | 1729  | 0     | 4.74   |
| Intel     | SSDSC2BA200G3      | 200 GB | 2       | 1653  | 0     | 4.53   |
| Kingston  | SVP100S296G        | 96 GB  | 2       | 1638  | 0     | 4.49   |
| Samsung   | MZNLN512HCJH-00000 | 512 GB | 2       | 1637  | 0     | 4.49   |
| OCZ       | REVODRIVE3         | 120 GB | 4       | 1590  | 0     | 4.36   |
| Corsair   | Force GT           | 240 GB | 4       | 1689  | 1     | 4.25   |
| Samsung   | SSD PM851a 2.5 7mm | 1 TB   | 3       | 1544  | 0     | 4.23   |
| OCZ       | VERTEX2            | 40 GB  | 2       | 1543  | 0     | 4.23   |
| Intel     | SSDSA2SH032G1GN    | 32 GB  | 2       | 1518  | 0     | 4.16   |
| Intel     | SSDSC2BA100G3      | 100 GB | 24      | 1576  | 1     | 4.13   |
| Intel     | SSDSC2BB160G4      | 160 GB | 3       | 1488  | 0     | 4.08   |
| OCZ       | VERTEX v1.10       | 64 GB  | 3       | 1655  | 1     | 4.05   |
| ADATA     | XM11               | 120 GB | 2       | 1508  | 1     | 4.03   |
| Kingston  | SVP100S264G        | 64 GB  | 3       | 1469  | 0     | 4.03   |
| Samsung   | MZ7PC256HAFU-000L7 | 256 GB | 4       | 1464  | 0     | 4.01   |
| Samsung   | MZ7KM1T9HAJM-00005 | 1.9 TB | 3       | 1457  | 0     | 3.99   |
| Corsair   | Force 3 SSD        | 180 GB | 7       | 1665  | 1     | 3.94   |
| Samsung   | MZ7LM240HCGR-00003 | 240 GB | 2       | 1433  | 0     | 3.93   |
| SanDisk   | SDSA6DM-016G-1006  | 16 GB  | 4       | 1413  | 0     | 3.87   |
| Intel     | SSDSC2BX400G4      | 400 GB | 2       | 1404  | 0     | 3.85   |
| Intel     | SSDSC2BP480G4      | 480 GB | 9       | 1416  | 1     | 3.84   |
| WDC       | WD1001X06X-00SJVT0 | 1.1 TB | 2       | 1381  | 0     | 3.79   |
| Intel     | SSDMCEAC120B3A     | 120 GB | 2       | 1373  | 0     | 3.76   |
| Samsung   | MZ7LN512HCHP-00000 | 512 GB | 2       | 1362  | 0     | 3.73   |
| Samsung   | MZ7LN256HMJP-00000 | 256 GB | 7       | 1348  | 0     | 3.69   |
| Micron    | M510DC_MTFDDAK2... | 240 GB | 2       | 1322  | 0     | 3.62   |
| Samsung   | MZ7GE960HMHP-00003 | 960 GB | 2       | 2613  | 508   | 3.59   |
| Intel     | SSDSC2BB480G4      | 480 GB | 5       | 1302  | 0     | 3.57   |
| SanDisk   | SD5SE2128G1002E    | 128 GB | 4       | 1285  | 0     | 3.52   |
| Toshiba   | THNS128GG4BAAA-... | 128 GB | 4       | 1284  | 0     | 3.52   |
| Intel     | SSDSC2BB080G4      | 80 GB  | 10      | 1281  | 0     | 3.51   |
| Micron    | C400-MTFDDAC128MAM | 128 GB | 2       | 1276  | 0     | 3.50   |
| Apple     | SSD SM1024F        | 1 TB   | 11      | 1270  | 0     | 3.48   |
| Samsung   | MZ7KM960HAHP-00005 | 960 GB | 2       | 1259  | 0     | 3.45   |
| Toshiba   | THNSNJ120PCSZ      | 120 GB | 2       | 1255  | 0     | 3.44   |
| Intel     | SSDSA2CW080G3      | 80 GB  | 19      | 1291  | 1     | 3.43   |
| OCZ       | VERTEX PLUS R2     | 64 GB  | 3       | 1248  | 0     | 3.42   |
| Samsung   | MZ7KM480HMHQ-00005 | 480 GB | 5       | 1243  | 0     | 3.41   |
| Kingston  | SSDNOW             | 32 GB  | 4       | 1242  | 0     | 3.40   |
| Seagate   | XF1230-1A0960      | 960 GB | 2       | 1236  | 0     | 3.39   |
| Intel     | SSDSC2BB120G4      | 120 GB | 3       | 1218  | 0     | 3.34   |
| Samsung   | MZHPV512HDGL-00000 | 512 GB | 5       | 1218  | 0     | 3.34   |
| Intel     | SSDSA2BW160G3      | 160 GB | 3       | 1222  | 402   | 3.34   |
| Samsung   | SSD 830 Series     | 512 GB | 15      | 1285  | 135   | 3.34   |
| Kingston  | SVP200S360G        | 64 GB  | 9       | 1206  | 0     | 3.31   |
| Corsair   | Force GT           | 180 GB | 3       | 1205  | 0     | 3.30   |
| Intel     | SSDSC2BA800G4      | 800 GB | 4       | 1199  | 0     | 3.29   |
| Intel     | SSDSA2CT040G3      | 40 GB  | 10      | 1194  | 0     | 3.27   |
| OCZ       | VERTEX2            | 64 GB  | 23      | 1223  | 12    | 3.26   |
| Toshiba   | THNSFC256GAMJ      | 256 GB | 2       | 1189  | 0     | 3.26   |
| Samsung   | SSD 840 EVO        | 1 TB   | 52      | 1265  | 4     | 3.25   |
| OCZ       | TRION150           | 960 GB | 2       | 1176  | 0     | 3.22   |
| Samsung   | SSD 850 PRO        | 1 TB   | 59      | 1193  | 1     | 3.21   |
| Seagate   | ST480HM000-1G5162  | 480 GB | 2       | 1282  | 1     | 3.20   |
| Intel     | SSDSC2BB016T7      | 1.6 TB | 3       | 2032  | 2     | 3.19   |
| Samsung   | MZ7LM960HCHP-00003 | 960 GB | 4       | 1165  | 0     | 3.19   |
| Crucial   | M4-CT512M4SSD2     | 512 GB | 14      | 1732  | 518   | 3.17   |
| OCZ       | SOLID3             | 64 GB  | 7       | 1347  | 160   | 3.17   |
| Toshiba   | THNSNC128GMMJ      | 128 GB | 5       | 1148  | 0     | 3.15   |
| Crucial   | C300-CTFDDAC256MAG | 256 GB | 5       | 1651  | 484   | 3.14   |
| Corsair   | Force 3 SSD        | 240 GB | 13      | 1266  | 81    | 3.14   |
| Intel     | SSDSC2CW240A3      | 240 GB | 41      | 1144  | 0     | 3.14   |
| Micron    | M600_MTFDDAK256MBF | 256 GB | 5       | 1140  | 0     | 3.13   |
| Intel     | SSDSC2BB120G6      | 120 GB | 3       | 1133  | 0     | 3.11   |
| Kingston  | SH103S390G         | 90 GB  | 4       | 1126  | 0     | 3.09   |
| Micron    | 5200_MTFDDAK7T6TDC | 7.6 TB | 15      | 1360  | 1     | 3.06   |
| Corsair   | Force GS           | 480 GB | 3       | 1884  | 15    | 3.02   |
| Kingston  | RBU-SC400S37256G   | 256 GB | 2       | 1095  | 0     | 3.00   |
| Toshiba   | TL100              | 120 GB | 5       | 1094  | 0     | 3.00   |
| Corsair   | Force GS           | 180 GB | 3       | 1087  | 0     | 2.98   |
| OCZ       | VERTEX2            | 120 GB | 14      | 1075  | 0     | 2.95   |
| PNY       | CS1311 960GB SSD   | 960 GB | 4       | 1074  | 0     | 2.94   |
| OCZ       | REVODRIVE350       | 120 GB | 4       | 1073  | 0     | 2.94   |
| Samsung   | MZ7PC128HAFU-000L1 | 128 GB | 4       | 1069  | 0     | 2.93   |
| KingSpec  | SPK-SF12-M120      | 120 GB | 2       | 1069  | 0     | 2.93   |
| Crucial   | CT500MX200SSD3     | 500 GB | 5       | 1066  | 0     | 2.92   |
| Mushkin   | MKNSSDCR120GB      | 120 GB | 8       | 1306  | 4     | 2.91   |
| Patriot   | Blast              | 480 GB | 2       | 1050  | 0     | 2.88   |
| Micron    | 5100_MTFDDAK960TCB | 960 GB | 3       | 1048  | 0     | 2.87   |
| Intel     | SSDMCEAC120B3      | 120 GB | 3       | 1502  | 2     | 2.86   |
| Micron    | M500_MTFDDAK480MAV | 480 GB | 2       | 1036  | 0     | 2.84   |
| Samsung   | MZ7LN128HCHP-00000 | 128 GB | 5       | 1036  | 0     | 2.84   |
| Micron    | C400-MTFDDAK128MAM | 128 GB | 4       | 1032  | 0     | 2.83   |
| Samsung   | SSD 830 Series     | 128 GB | 71      | 1037  | 15    | 2.82   |
| Intel     | SSDSC2BB120G7R     | 120 GB | 5       | 1030  | 0     | 2.82   |
| Samsung   | MZ7PC128HAFU-000L5 | 128 GB | 2       | 1028  | 0     | 2.82   |
| Intel     | SSDSC2CW180A3      | 180 GB | 17      | 1022  | 0     | 2.80   |
| Toshiba   | THNSNJ512GDNU      | 512 GB | 2       | 1021  | 0     | 2.80   |
| OCZ       | AGILITY4           | 128 GB | 8       | 1019  | 0     | 2.79   |
| Toshiba   | THNSNJ256GCST      | 256 GB | 5       | 1008  | 0     | 2.76   |
| ADATA     | SP800              | 32 GB  | 2       | 1001  | 0     | 2.74   |
| SanDisk   | SD7SB7S512G1122    | 512 GB | 4       | 987   | 0     | 2.71   |
| Kingston  | SH100S3120G        | 120 GB | 10      | 987   | 0     | 2.70   |
| Hyundai   | 120GB SSD          | 120 GB | 2       | 986   | 0     | 2.70   |
| Samsung   | SSD 850 EVO        | 2 TB   | 25      | 984   | 0     | 2.70   |
| Samsung   | SSD 840 EVO        | 500 GB | 98      | 1065  | 30    | 2.69   |
| Crucial   | M4-CT128M4SSD2     | 128 GB | 75      | 1042  | 109   | 2.68   |
| Apple     | SSD SM128E         | 121 GB | 6       | 1323  | 4     | 2.68   |
| Samsung   | SSD PM830 2.5" 7mm | 256 GB | 19      | 1027  | 54    | 2.68   |
| Crucial   | M4-CT064M4SSD2     | 64 GB  | 31      | 1085  | 168   | 2.66   |
| Intel     | SSDSC2BX200G4      | 200 GB | 2       | 969   | 0     | 2.66   |
| Micron    | MTFDDAK256MBF-1... | 256 GB | 7       | 965   | 0     | 2.65   |
| SanDisk   | SD6SF1M064G1022    | 64 GB  | 2       | 963   | 0     | 2.64   |
| Intel     | SSDSC2BB240G7      | 240 GB | 5       | 963   | 0     | 2.64   |
| SanDisk   | SDSSDRC032G        | 32 GB  | 10      | 962   | 0     | 2.64   |
| Samsung   | MZRPA128HMCD-000SO | 64 GB  | 14      | 958   | 0     | 2.63   |
| Corsair   | Force GT           | 120 GB | 22      | 1147  | 2     | 2.61   |
| Intel     | SSDSA2CW120G3      | 120 GB | 26      | 1162  | 39    | 2.60   |
| HP        | VK0300GDUQV        | 304 GB | 3       | 945   | 0     | 2.59   |
| OCZ       | VECTOR             | 256 GB | 4       | 939   | 0     | 2.57   |
| Crucial   | CT250MX200SSD4     | 250 GB | 2       | 936   | 0     | 2.57   |
| HP        | VK000240GWCFD      | 240 GB | 2       | 933   | 0     | 2.56   |
| Micron    | M600_MTFDDAK1T0MBF | 1 TB   | 8       | 929   | 0     | 2.55   |
| Kingston  | SE50S3480G         | 480 GB | 10      | 1104  | 1     | 2.54   |
| Crucial   | C300-CTFDDAC064MAG | 64 GB  | 11      | 1085  | 184   | 2.53   |
| Intel     | SSDSC2CT060A3      | 64 GB  | 11      | 1114  | 1     | 2.48   |
| Samsung   | MZ7LN128HCHP-000H1 | 128 GB | 3       | 903   | 0     | 2.48   |
| Intel     | SSDMCEAW120A4      | 120 GB | 2       | 902   | 0     | 2.47   |
| Samsung   | SSD 840 PRO Series | 128 GB | 81      | 1020  | 4     | 2.47   |
| Samsung   | SSD 830 Series     | 256 GB | 53      | 911   | 20    | 2.47   |
| SanDisk   | SD7SB6S128G1122    | 128 GB | 10      | 888   | 0     | 2.43   |
| Samsung   | MZ7TE512HMHP-000L1 | 512 GB | 6       | 885   | 0     | 2.43   |
| SanDisk   | SD7SB3Q064G        | 56 GB  | 2       | 885   | 0     | 2.43   |
| SK hynix  | SC300B SATA        | 512 GB | 3       | 882   | 0     | 2.42   |
| Samsung   | SSD PM800 2.5"     | 256 GB | 2       | 878   | 0     | 2.41   |
| Samsung   | SSD 840 EVO 250... | 250 GB | 13      | 875   | 0     | 2.40   |
| OWC       | Mercury EXTREME... | 480 GB | 7       | 971   | 11    | 2.40   |
| Intel     | SSDSC2BB800G7R     | 800 GB | 2       | 1166  | 1     | 2.40   |
| ADATA     | SX930              | 480 GB | 2       | 869   | 0     | 2.38   |
| Crucial   | M4-CT256M4SSD1     | 256 GB | 4       | 957   | 253   | 2.38   |
| Phison    | SATA SSD           | 16 GB  | 2       | 862   | 0     | 2.36   |
| Samsung   | MZ7TE256HMHP-00000 | 256 GB | 3       | 861   | 0     | 2.36   |
| Corsair   | Force 3 SSD        | 120 GB | 44      | 961   | 59    | 2.35   |
| Toshiba   | KHK61RSE480G       | 480 GB | 4       | 856   | 0     | 2.35   |
| Samsung   | SSD 840 PRO Series | 256 GB | 132     | 939   | 10    | 2.34   |
| WDC       | WDBNCE2500PNC-WRSN | 250 GB | 3       | 849   | 0     | 2.33   |
| MyDigi... | BP5                | 240 GB | 4       | 845   | 0     | 2.32   |
| Intel     | SSDSC2BB480G7      | 480 GB | 4       | 974   | 1     | 2.30   |
| Samsung   | SSD 850 PRO        | 512 GB | 117     | 849   | 9     | 2.29   |
| Samsung   | MZ7TY256HDHP-00007 | 256 GB | 2       | 834   | 0     | 2.29   |
| Kingston  | SMSR150S3256G      | 128 GB | 2       | 833   | 0     | 2.28   |
| Team      | L5 LITE SSD        | 240 GB | 2       | 1068  | 148   | 2.28   |
| ADATA     | SSD S510           | 120 GB | 11      | 844   | 1     | 2.28   |
| Corsair   | Force 3 SSD        | 64 GB  | 21      | 856   | 1     | 2.27   |
| Mushkin   | MKNSSDCR60GB-7     | 64 GB  | 3       | 865   | 2     | 2.27   |
| Toshiba   | THNSNH256GMCT      | 256 GB | 5       | 824   | 0     | 2.26   |
| Intel     | SSDSC2BX480G4K     | 480 GB | 2       | 824   | 0     | 2.26   |
| WDC       | WDBNCE0010PNC-WRSN | 1 TB   | 2       | 821   | 0     | 2.25   |
| Samsung   | MZ7LM960HMJP-00005 | 960 GB | 4       | 817   | 0     | 2.24   |
| Samsung   | SSD 840 EVO 120... | 120 GB | 10      | 821   | 1     | 2.23   |
| SK hynix  | HFS256G39MND-3510A | 256 GB | 3       | 814   | 0     | 2.23   |
| Samsung   | SSD 830 Series     | 64 GB  | 27      | 814   | 0     | 2.23   |
| SanDisk   | SDSA6MM-016G-1006  | 16 GB  | 13      | 902   | 121   | 2.22   |
| Samsung   | SSD 840 Series     | 250 GB | 68      | 884   | 1     | 2.22   |
| SanDisk   | SSD U110           | 128 GB | 5       | 805   | 0     | 2.21   |
| Crucial   | CT120M500SSD3      | 120 GB | 6       | 876   | 6     | 2.20   |
| Crucial   | M4-CT128M4SSD3     | 128 GB | 3       | 801   | 0     | 2.20   |
| Corsair   | Neutron SSD        | 256 GB | 2       | 801   | 0     | 2.20   |
| ADATA     | SP600              | 128 GB | 14      | 800   | 0     | 2.19   |
| Toshiba   | THNSNH512GCST      | 512 GB | 3       | 800   | 0     | 2.19   |
| Toshiba   | THNS064GG2BNAA     | 64 GB  | 9       | 799   | 0     | 2.19   |
| OCZ       | VECTOR180          | 480 GB | 2       | 798   | 0     | 2.19   |
| Samsung   | SSD PM800 Serie... | 256 GB | 4       | 988   | 2     | 2.19   |
| SanDisk   | SSD U110           | 64 GB  | 3       | 797   | 0     | 2.18   |
| Samsung   | MZMTE512HMHP-000MV | 512 GB | 4       | 797   | 0     | 2.18   |
| Corsair   | Force GT           | 64 GB  | 8       | 948   | 4     | 2.17   |
| Toshiba   | Q300 Pro           | 256 GB | 2       | 789   | 0     | 2.16   |
| ADATA     | SP600              | 256 GB | 14      | 783   | 0     | 2.15   |
| Kingston  | SVP200S37A120G     | 120 GB | 20      | 949   | 87    | 2.14   |
| Intel     | SSDSC2BB480G6      | 480 GB | 2       | 781   | 0     | 2.14   |
| SanDisk   | SD7SN6S512G1122    | 512 GB | 2       | 779   | 0     | 2.14   |
| Radeon    | R7                 | 120 GB | 4       | 778   | 0     | 2.13   |
| Kingston  | SH103S3120G        | 120 GB | 103     | 837   | 11    | 2.11   |
| SPCC      | SSD                | 480 GB | 8       | 770   | 0     | 2.11   |
| Crucial   | M4-CT128M4SSD1     | 128 GB | 11      | 786   | 92    | 2.10   |
| OCZ       | VERTEX2 3.5        | 115 GB | 3       | 765   | 0     | 2.10   |
| Samsung   | SSD 840 Series     | 500 GB | 17      | 884   | 3     | 2.09   |
| OCZ       | VERTEX4            | 256 GB | 39      | 1041  | 1     | 2.09   |
| Samsung   | MZ7KM240HMHQ-00005 | 240 GB | 3       | 762   | 0     | 2.09   |
| SanDisk   | SD8SN8U1T001122    | 1 TB   | 5       | 761   | 0     | 2.09   |
| Samsung   | SSD 840 EVO        | 250 GB | 283     | 812   | 16    | 2.09   |
| Crucial   | CT512MX100SSD1     | 512 GB | 48      | 801   | 1     | 2.08   |
| Kingston  | SVP200S3120G       | 120 GB | 14      | 830   | 143   | 2.08   |
| Samsung   | MZNLF192HCGS-000L1 | 192 GB | 3       | 757   | 0     | 2.08   |
| Samsung   | SSD 850 PRO        | 128 GB | 58      | 819   | 18    | 2.07   |
| Crucial   | M4-CT256M4SSD2     | 256 GB | 48      | 924   | 191   | 2.07   |
| Kingston  | SEDC400S37480G     | 480 GB | 2       | 752   | 0     | 2.06   |
| Samsung   | MZ7PC128HAFU-000H1 | 128 GB | 7       | 751   | 0     | 2.06   |
| Samsung   | SSD 840 PRO Series | 512 GB | 39      | 1043  | 85    | 2.06   |
| SK hynix  | SC300B SATA        | 256 GB | 2       | 751   | 0     | 2.06   |
| Intel     | SSDSC2BB300G4      | 304 GB | 3       | 750   | 0     | 2.06   |
| OCZ       | AGILITY3           | 64 GB  | 67      | 922   | 4     | 2.05   |
| Toshiba   | KHK61RSE960G       | 960 GB | 2       | 743   | 0     | 2.04   |
| Transcend | TS128GSSD320       | 128 GB | 3       | 743   | 0     | 2.04   |
| Samsung   | SSD 840 Series     | 120 GB | 93      | 818   | 1     | 2.02   |
| Samsung   | MZ7PD128HCFV-000H1 | 128 GB | 8       | 735   | 0     | 2.02   |
| SanDisk   | SDSSDHII960G       | 960 GB | 12      | 776   | 1     | 2.01   |
| Toshiba   | THNSNJ256G8NU      | 256 GB | 7       | 731   | 0     | 2.01   |
| Intel     | SSDSC2BW240A3L     | 240 GB | 9       | 727   | 0     | 1.99   |
| Samsung   | SSD 840 EVO        | 120 GB | 224     | 786   | 17    | 1.99   |
| Samsung   | SSD PM800 2.5"     | 128 GB | 5       | 724   | 0     | 1.99   |
| PNY       | CS1311 240GB SSD   | 240 GB | 27      | 724   | 0     | 1.98   |
| Samsung   | MZ7PA256HMDR-010H1 | 256 GB | 2       | 842   | 520   | 1.98   |
| Samsung   | MZ7LN256HAJQ-000H1 | 256 GB | 5       | 722   | 0     | 1.98   |
| Samsung   | SSD 750 EVO        | 500 GB | 43      | 722   | 0     | 1.98   |
| Samsung   | SSD PM830 2.5" 7mm | 128 GB | 27      | 875   | 156   | 1.98   |
| Toshiba   | THNSNB128GMCJ      | 128 GB | 5       | 720   | 0     | 1.97   |
| Apple     | SSD SM0512F        | 500 GB | 26      | 717   | 0     | 1.97   |
| Samsung   | MZHPU256HCGL-000H1 | 256 GB | 3       | 716   | 0     | 1.96   |
| Corsair   | CSSD-F60GB2        | 64 GB  | 7       | 1350  | 286   | 1.96   |
| Samsung   | MZ7TD512HAGM-000L1 | 512 GB | 3       | 715   | 0     | 1.96   |
| SanDisk   | SDSA6MM-032G-1006  | 32 GB  | 2       | 712   | 0     | 1.95   |
| Samsung   | SSD 850 PRO        | 256 GB | 222     | 752   | 5     | 1.95   |
| Samsung   | MZ7PD256HAFV-000H7 | 256 GB | 10      | 711   | 0     | 1.95   |
| Samsung   | MZ7PD256HCGM-000H7 | 256 GB | 25      | 718   | 98    | 1.95   |
| Corsair   | Force LE SSD       | 240 GB | 4       | 709   | 0     | 1.94   |
| SanDisk   | SD5SB2-128G-1006E  | 128 GB | 6       | 708   | 0     | 1.94   |
| Intel     | SSDSC2KB019T8      | 1.9 TB | 18      | 895   | 1     | 1.94   |
| Apple     | SSD TS256C         | 256 GB | 9       | 706   | 0     | 1.94   |
| Samsung   | MZMPC032HBCD-000D1 | 32 GB  | 9       | 705   | 0     | 1.93   |
| Plextor   | PX-128M2S          | 128 GB | 3       | 833   | 1     | 1.93   |
| Samsung   | SSD 850 EVO M.2    | 1 TB   | 8       | 704   | 0     | 1.93   |
| Patriot   | Ignite             | 480 GB | 3       | 698   | 0     | 1.91   |
| Crucial   | C300-CTFDDAC128MAG | 128 GB | 11      | 1003  | 185   | 1.91   |
| Kingston  | SMSM151S3128GD     | 128 GB | 2       | 692   | 0     | 1.90   |
| Samsung   | MZMPC256HBGJ-000H1 | 256 GB | 2       | 690   | 0     | 1.89   |
| Samsung   | MZMTE256HMHP-00005 | 256 GB | 2       | 689   | 0     | 1.89   |
| ADATA     | SX950              | 240 GB | 3       | 689   | 0     | 1.89   |
| Toshiba   | THNSNJ128GMCU      | 128 GB | 10      | 686   | 0     | 1.88   |
| Samsung   | SSD 850 EVO        | 500 GB | 764     | 693   | 1     | 1.88   |
| SanDisk   | SD8SN8U256G1122    | 256 GB | 5       | 685   | 0     | 1.88   |
| Samsung   | SSD 850 EVO        | 1 TB   | 176     | 768   | 4     | 1.86   |
| WDC       | WDS500G1B0B-00AS40 | 500 GB | 9       | 678   | 0     | 1.86   |
| Kingston  | SHFS37A480G        | 480 GB | 3       | 675   | 0     | 1.85   |
| Seagate   | 2E256-TU2-510B00   | 170 GB | 3       | 2072  | 1366  | 1.85   |
| Kingston  | SKC400S37512G      | 512 GB | 10      | 674   | 0     | 1.85   |
| Intel     | SSDSC2BA200G4      | 200 GB | 10      | 730   | 1     | 1.85   |
| SK        | SKhynix SC300 H... | 256 GB | 2       | 672   | 0     | 1.84   |
| SanDisk   | SDSSDXP480G        | 480 GB | 2       | 671   | 0     | 1.84   |
| Samsung   | MZHPV128HDGM-00000 | 128 GB | 4       | 671   | 0     | 1.84   |
| OCZ       | TRION150           | 480 GB | 11      | 668   | 0     | 1.83   |
| Samsung   | SSD 850 EVO M.2    | 500 GB | 49      | 665   | 0     | 1.82   |
| SanDisk   | SD6SB2M-512G-1006  | 512 GB | 5       | 665   | 0     | 1.82   |
| Samsung   | MZNLF128HCHP-00000 | 128 GB | 15      | 665   | 0     | 1.82   |
| Kingston  | RBUSNS8280S3128GH2 | 128 GB | 6       | 664   | 0     | 1.82   |
| Innodisk  | Corp. DRPS-02GJ... | 2 GB   | 3       | 664   | 0     | 1.82   |
| Smartbuy  | SSD                | 90 GB  | 2       | 661   | 0     | 1.81   |
| Intel     | SSDSA2CW160G3      | 160 GB | 10      | 661   | 0     | 1.81   |
| Kingston  | SH100S3240G        | 240 GB | 4       | 1136  | 2     | 1.81   |
| Micron    | MTFDDAK256MAM-1K1  | 256 GB | 8       | 658   | 0     | 1.80   |
| Samsung   | MZ7TD256HAFV-000L9 | 256 GB | 13      | 657   | 0     | 1.80   |
| Micron    | C400-MTFDDAK256MAM | 256 GB | 5       | 726   | 607   | 1.80   |
| SanDisk   | Ultra II           | 480 GB | 48      | 677   | 1     | 1.80   |
| SanDisk   | SD7SB3Q-128G-1006  | 128 GB | 5       | 655   | 0     | 1.80   |
| Samsung   | SSD RBX Series ... | 64 GB  | 2       | 651   | 0     | 1.79   |
| Apple     | SSD SM1024G        | 1 TB   | 7       | 651   | 0     | 1.78   |
| Toshiba   | THNSNH256GCST      | 256 GB | 2       | 651   | 0     | 1.78   |
| Samsung   | MZNLN512HCJH-000H1 | 512 GB | 6       | 649   | 0     | 1.78   |
| PNY       | CS1311 480GB SSD   | 480 GB | 10      | 648   | 0     | 1.78   |
| OCZ       | AGILITY3           | 120 GB | 75      | 832   | 75    | 1.77   |
| Samsung   | MZ-RPC512T-0SO     | 256 GB | 2       | 645   | 0     | 1.77   |
| Samsung   | MZ7TY128HDHP-000L1 | 128 GB | 15      | 643   | 0     | 1.76   |
| Kingston  | SKC300S37A480G     | 480 GB | 2       | 643   | 0     | 1.76   |
| Toshiba   | Q300 Pro           | 128 GB | 3       | 641   | 0     | 1.76   |
| Intel     | SSDSC2CW480A3      | 480 GB | 6       | 640   | 0     | 1.76   |
| Corsair   | Force GS           | 128 GB | 24      | 640   | 0     | 1.75   |
| Toshiba   | THNSNJ128G8NU      | 128 GB | 11      | 637   | 0     | 1.75   |
| Kingston  | SV100S232G         | 32 GB  | 5       | 635   | 0     | 1.74   |
| SanDisk   | X400 2.5 7MM       | 256 GB | 10      | 633   | 0     | 1.74   |
| Samsung   | MZ7PD128HAFV-000H7 | 128 GB | 9       | 633   | 0     | 1.74   |
| Patriot   | Blaze              | 240 GB | 6       | 632   | 0     | 1.73   |
| SanDisk   | SDSSDHII480G       | 480 GB | 18      | 642   | 1     | 1.73   |
| SK hynix  | HFS120G32TND-N1A2A | 120 GB | 2       | 626   | 0     | 1.72   |
| Crucial   | CT1024MX200SSD1    | 1 TB   | 9       | 768   | 12    | 1.71   |
| SanDisk   | SD7TB3Q-256G-1006  | 256 GB | 15      | 625   | 0     | 1.71   |
| Samsung   | MZ7LN512HMJP-000L7 | 512 GB | 16      | 625   | 0     | 1.71   |
| Apple     | SSD SM0256F        | 256 GB | 30      | 624   | 0     | 1.71   |
| Kingston  | SVP200S3240G       | 240 GB | 4       | 624   | 0     | 1.71   |
| Samsung   | MZ7PA128HMCD-010L1 | 128 GB | 6       | 695   | 158   | 1.71   |
| Samsung   | SSD 850 EVO        | 4 TB   | 5       | 622   | 0     | 1.71   |
| Samsung   | MZ7LN512HCHP-000H1 | 512 GB | 3       | 622   | 0     | 1.71   |
| SanDisk   | SD8SBBU240G1122    | 240 GB | 5       | 621   | 0     | 1.70   |
| Samsung   | SSD CM871 M.2 2280 | 128 GB | 4       | 621   | 0     | 1.70   |
| Samsung   | MZ7LN256HMJP-000H1 | 256 GB | 15      | 681   | 1     | 1.70   |
| SanDisk   | SDSSDHP256G        | 256 GB | 36      | 636   | 1     | 1.70   |
| Toshiba   | TR150              | 960 GB | 3       | 620   | 0     | 1.70   |
| OCZ       | VERTEX3            | 120 GB | 85      | 885   | 44    | 1.69   |
| Toshiba   | THNSFJ256GCSU      | 256 GB | 24      | 621   | 1     | 1.69   |
| OCZ       | VERTEX3 MI         | 120 GB | 25      | 873   | 122   | 1.68   |
| Samsung   | SSD PM830 mSATA    | 256 GB | 3       | 609   | 0     | 1.67   |
| Pioneer   | APS-SL3N-128       | 128 GB | 2       | 609   | 0     | 1.67   |
| Intel     | SSDSC2BP240G4      | 240 GB | 10      | 609   | 0     | 1.67   |
| Intel     | SSDSC2CT180A3      | 180 GB | 18      | 723   | 1     | 1.67   |
| Crucial   | CT500MX200SSD6     | 500 GB | 2       | 609   | 0     | 1.67   |
| KingSpec  | ACSC2M064S25       | 64 GB  | 3       | 607   | 0     | 1.67   |
| Micron    | M600_MTFDDAT128MBF | 128 GB | 2       | 604   | 0     | 1.66   |
| SK hynix  | HFS512G39MND-3510A | 512 GB | 5       | 604   | 0     | 1.66   |
| Samsung   | MZNTY128HDHP-000L2 | 128 GB | 2       | 604   | 0     | 1.66   |
| Samsung   | MZMTE256HMHP-00000 | 256 GB | 4       | 603   | 0     | 1.65   |
| Samsung   | SSD 850 EVO        | 120 GB | 168     | 603   | 0     | 1.65   |
| Samsung   | SSD 850 EVO        | 250 GB | 928     | 620   | 3     | 1.65   |
| Samsung   | MZ7TE256HMHP-000L7 | 256 GB | 26      | 642   | 15    | 1.65   |
| Micron    | MTFDDAK1T0MBF-1... | 1 TB   | 2       | 600   | 0     | 1.64   |
| Toshiba   | THNSFJ256GDNU A    | 256 GB | 12      | 600   | 0     | 1.64   |
| Micron    | M600_MTFDDAK512MBF | 512 GB | 3       | 598   | 0     | 1.64   |
| Corsair   | Neutron SSD        | 64 GB  | 6       | 807   | 3     | 1.64   |
| Samsung   | MZ7TD128HAFV-000L1 | 128 GB | 22      | 597   | 0     | 1.64   |
| Corsair   | CSSD-V64GB2        | 64 GB  | 2       | 597   | 0     | 1.64   |
| Micron    | 5200_MTFDDAK1T9TDC | 1.9 TB | 13      | 636   | 1     | 1.64   |
| SanDisk   | SD7SB7S512G1001    | 512 GB | 4       | 597   | 0     | 1.64   |
| SanDisk   | PLUS               | 480 GB | 9       | 595   | 0     | 1.63   |
| SanDisk   | X300 2.5 7MM       | 256 GB | 3       | 595   | 0     | 1.63   |
| Hoodisk   | SSD                | 64 GB  | 5       | 594   | 0     | 1.63   |
| Micron    | MTFDDAK512MBF-1... | 512 GB | 7       | 648   | 3     | 1.63   |
| Intel     | SSDSC2BF180A5      | 180 GB | 3       | 1683  | 3     | 1.62   |
| Toshiba   | THNS128GG4BBAA     | 128 GB | 4       | 592   | 0     | 1.62   |
| Intel     | SSDSCMMW180A3L     | 180 GB | 5       | 592   | 0     | 1.62   |
| Samsung   | MZ7TE512HMHP-000L2 | 512 GB | 5       | 591   | 0     | 1.62   |
| Samsung   | SSD 750 EVO        | 250 GB | 106     | 597   | 1     | 1.61   |
| SanDisk   | SD6SP1M128G1102    | 128 GB | 3       | 589   | 0     | 1.61   |
| OCZ       | VERTEX4            | 128 GB | 101     | 644   | 1     | 1.61   |
| Kingston  | RBU-SNS8100S3256GD | 256 GB | 6       | 587   | 0     | 1.61   |
| Patriot   | Blast              | 240 GB | 12      | 587   | 0     | 1.61   |
| Micron    | 5200_MTFDDAK480TDC | 480 GB | 6       | 587   | 0     | 1.61   |
| Samsung   | MZ7TY256HDHP-000L1 | 256 GB | 2       | 585   | 0     | 1.60   |
| Intel     | SSDSC2BA400G4      | 400 GB | 4       | 584   | 0     | 1.60   |
| Micron    | MTFDDAV512TBN-1... | 512 GB | 2       | 739   | 1     | 1.60   |
| SanDisk   | SDSSDP064G         | 64 GB  | 45      | 604   | 23    | 1.60   |
| Samsung   | SSD 850 EVO M.2    | 120 GB | 12      | 582   | 0     | 1.60   |
| Crucial   | CT250MX200SSD3     | 250 GB | 5       | 580   | 0     | 1.59   |
| Kingston  | SHSS37A120G        | 120 GB | 16      | 580   | 0     | 1.59   |
| SanDisk   | Ultra II           | 960 GB | 36      | 613   | 1     | 1.59   |
| Samsung   | MZNTD256HAGL-000L9 | 256 GB | 3       | 577   | 0     | 1.58   |
| Kingston  | SHSS37A240G        | 240 GB | 58      | 584   | 1     | 1.58   |
| Toshiba   | Q300               | 480 GB | 12      | 576   | 0     | 1.58   |
| SanDisk   | SSD U100           | 8 GB   | 2       | 575   | 0     | 1.58   |
| Intel     | SSDSC2BW180A3L     | 180 GB | 22      | 579   | 1     | 1.57   |
| Samsung   | MZHPV256HDGL-00000 | 256 GB | 11      | 614   | 1     | 1.57   |
| SanDisk   | SD9SB8W128G1001    | 128 GB | 5       | 572   | 0     | 1.57   |
| ADATA     | SSD S510           | 64 GB  | 3       | 572   | 0     | 1.57   |
| Kingston  | SKC400S37128G      | 128 GB | 3       | 570   | 0     | 1.56   |
| OCZ       | VERTEX PLUS R2     | 128 GB | 4       | 569   | 0     | 1.56   |
| Intel     | SSDSC2CT080A4      | 80 GB  | 4       | 568   | 0     | 1.56   |
| Samsung   | SSD 850 EVO M.2    | 250 GB | 47      | 568   | 0     | 1.56   |
| OCZ       | VECTOR             | 128 GB | 7       | 568   | 3     | 1.55   |
| OCZ       | VERTEX3            | 64 GB  | 37      | 613   | 1     | 1.55   |
| Apple     | SSD SM768E         | 752 GB | 3       | 566   | 0     | 1.55   |
| PNY       | SSD2SC480G1CS27... | 480 GB | 4       | 566   | 0     | 1.55   |
| Samsung   | MZ7KM480HMHQ0D3    | 480 GB | 6       | 565   | 0     | 1.55   |
| Toshiba   | THNSNH128GCST      | 128 GB | 12      | 579   | 1     | 1.55   |
| OCZ       | REVODRIVE3         | 64 GB  | 4       | 564   | 0     | 1.55   |
| Kingston  | SKC400S37256G      | 256 GB | 11      | 563   | 0     | 1.54   |
| SanDisk   | SD8SB8U-256G-1006  | 256 GB | 11      | 560   | 0     | 1.54   |
| Samsung   | SSD PM871b 2.5 7mm | 256 GB | 10      | 560   | 0     | 1.53   |
| Samsung   | SSD 850 EVO mSATA  | 120 GB | 7       | 559   | 0     | 1.53   |
| Lite-On   | CV6-8Q128          | 128 GB | 3       | 559   | 0     | 1.53   |
| Kingston  | SMS200S360G        | 64 GB  | 19      | 793   | 54    | 1.53   |
| Toshiba   | TR150              | 120 GB | 11      | 558   | 0     | 1.53   |
| SPCC      | SSD110             | 120 GB | 8       | 613   | 127   | 1.53   |
| Hajaan    | SSD 256G           | 256 GB | 2       | 557   | 0     | 1.53   |
| SanDisk   | SD8SB8U-128G-1016  | 128 GB | 2       | 556   | 0     | 1.53   |
| OCZ       | VERTEX2 3.5        | 120 GB | 3       | 734   | 1     | 1.52   |
| Micron    | M600_MTFDDAY512MBF | 512 GB | 2       | 555   | 0     | 1.52   |
| Samsung   | SSD 850 PRO        | 2 TB   | 7       | 671   | 7     | 1.52   |
| China     | 120GB SATA Flas... | 120 GB | 2       | 554   | 0     | 1.52   |
| SanDisk   | SDSSDXPS240G       | 240 GB | 24      | 713   | 53    | 1.52   |
| SK hynix  | SC300 2.5 7MM      | 256 GB | 5       | 553   | 0     | 1.52   |
| China     | ZSS11DA02C         | 512 GB | 2       | 551   | 0     | 1.51   |
| SanDisk   | SDSSDP256G         | 256 GB | 15      | 579   | 2     | 1.51   |
| Kingston  | SH103S3240G        | 240 GB | 39      | 803   | 83    | 1.51   |
| SPCC      | SSD110             | 64 GB  | 6       | 715   | 4     | 1.50   |
| Toshiba   | THNSNC064GMMJ      | 64 GB  | 2       | 547   | 0     | 1.50   |
| Crucial   | CT256MX100SSD1     | 256 GB | 81      | 588   | 6     | 1.50   |
| OCZ       | VERTEX2            | 115 GB | 7       | 545   | 0     | 1.50   |
| Samsung   | MZ7KM960HMJP-00005 | 960 GB | 4       | 545   | 0     | 1.49   |
| Micron    | MTFDDAK512TBN-1... | 512 GB | 2       | 613   | 3     | 1.49   |
| Plextor   | PX-512M7VC         | 512 GB | 2       | 544   | 0     | 1.49   |
| Goodram   | SSD                | 240 GB | 25      | 543   | 0     | 1.49   |
| Intel     | SSDSC2KB240G8      | 240 GB | 21      | 542   | 0     | 1.49   |
| Faspeed   | F510-120G          | 120 GB | 2       | 542   | 0     | 1.49   |
| Samsung   | MZMPC128HBFU-000H1 | 128 GB | 7       | 540   | 0     | 1.48   |
| Samsung   | SSD 850 EVO mSATA  | 1 TB   | 8       | 539   | 0     | 1.48   |
| SanDisk   | SD8SB8U1T001122    | 1 TB   | 7       | 538   | 0     | 1.48   |
| Apple     | SSD SM256E         | 256 GB | 15      | 538   | 0     | 1.48   |
| Toshiba   | VT180              | 480 GB | 3       | 747   | 1     | 1.47   |
| Samsung   | MZ7TD256HAFV-000L7 | 256 GB | 13      | 537   | 0     | 1.47   |
| Plextor   | PX-128M3           | 128 GB | 7       | 601   | 260   | 1.47   |
| Toshiba   | THNSNJ512GCSU      | 512 GB | 7       | 537   | 0     | 1.47   |
| Samsung   | SSD SM871 2.5 7mm  | 256 GB | 9       | 612   | 51    | 1.47   |
| Intel     | SSDSC2KB960G8      | 960 GB | 36      | 559   | 1     | 1.47   |
| Kingston  | SV200S364G         | 64 GB  | 8       | 561   | 1     | 1.46   |
| Toshiba   | THNSNC128GCSJ      | 128 GB | 3       | 532   | 0     | 1.46   |
| Intel     | SSDSC2KG240G8      | 240 GB | 16      | 532   | 0     | 1.46   |
| Kingston  | SV300S37A60G       | 64 GB  | 191     | 570   | 1     | 1.45   |
| Apple     | SSD SM512E         | 500 GB | 8       | 543   | 1     | 1.45   |
| Samsung   | MZ7LF128HCHP-000L1 | 128 GB | 2       | 528   | 0     | 1.45   |
| SanDisk   | SD6SB2M128G1022I   | 128 GB | 2       | 528   | 0     | 1.45   |
| Samsung   | SSD 650            | 120 GB | 11      | 527   | 0     | 1.45   |
| SanDisk   | SDSSDA480G         | 480 GB | 28      | 527   | 1     | 1.44   |
| GALAX     | GXTA1B0120A        | 120 GB | 2       | 525   | 0     | 1.44   |
| SK hynix  | HFS512G39MND-3310A | 512 GB | 2       | 524   | 0     | 1.44   |
| Samsung   | SSD PM830 mSATA    | 32 GB  | 21      | 523   | 0     | 1.43   |
| Samsung   | MZ7LF128HCHP-00004 | 128 GB | 3       | 522   | 0     | 1.43   |
| Samsung   | MZ7PC128HAFU-000   | 128 GB | 3       | 521   | 0     | 1.43   |
| OCZ       | AGILITY3           | 240 GB | 19      | 712   | 12    | 1.43   |
| Toshiba   | THNSNJ128GCST      | 128 GB | 5       | 521   | 0     | 1.43   |
| Samsung   | MZRPA256HMDR-000SO | 128 GB | 2       | 520   | 0     | 1.43   |
| SanDisk   | SD9TB8W512G1001    | 512 GB | 5       | 520   | 0     | 1.43   |
| Samsung   | MZ7LN256HCHP-00000 | 256 GB | 9       | 519   | 0     | 1.42   |
| Intenso   | SSD Sata III       | 480 GB | 2       | 518   | 0     | 1.42   |
| Apple     | SSD SD512E         | 500 GB | 4       | 517   | 0     | 1.42   |
| Team      | L3 EVO SSD         | 120 GB | 7       | 514   | 0     | 1.41   |
| SanDisk   | SD8SB8U512G1122    | 512 GB | 10      | 514   | 0     | 1.41   |
| Intel     | SSDSA2BW120G3H     | 120 GB | 5       | 544   | 1     | 1.41   |
| Kingston  | SMSM150S324G2      | 24 GB  | 6       | 513   | 0     | 1.41   |
| Transcend | TS256GMTS600       | 256 GB | 2       | 512   | 0     | 1.40   |
| WDC       | WDS250G1B0B-00AS40 | 250 GB | 10      | 508   | 0     | 1.39   |
| Toshiba   | THNSNJ128GCSU      | 128 GB | 23      | 507   | 0     | 1.39   |
| SanDisk   | SDSSDH2128G        | 128 GB | 4       | 507   | 0     | 1.39   |
| WDC       | WDS200T2B0A        | 2 TB   | 3       | 507   | 0     | 1.39   |
| Samsung   | MZMPC032HBCD-000H1 | 32 GB  | 16      | 506   | 0     | 1.39   |
| SanDisk   | SSD U110           | 32 GB  | 2       | 505   | 0     | 1.39   |
| Kingston  | SMS100S264G        | 64 GB  | 6       | 517   | 2     | 1.38   |
| Samsung   | MZ7TY256HDHP-00000 | 256 GB | 7       | 504   | 0     | 1.38   |
| Palit     | UVS                | 240 GB | 2       | 503   | 0     | 1.38   |
| Samsung   | MZ7WD960HMHP-00003 | 960 GB | 6       | 846   | 3     | 1.38   |
| Crucial   | CT240M500SSD3      | 240 GB | 7       | 544   | 5     | 1.37   |
| Kingston  | RBU-SNS8152S3128GF | 128 GB | 2       | 498   | 0     | 1.37   |
| Corsair   | Force GT           | 90 GB  | 4       | 610   | 1     | 1.36   |
| Samsung   | MZNLF128HCHP-00004 | 128 GB | 15      | 495   | 0     | 1.36   |
| Samsung   | MZ7TE128HMGR-00004 | 128 GB | 7       | 495   | 0     | 1.36   |
| OCZ       | VERTEX460A         | 240 GB | 3       | 494   | 0     | 1.35   |
| Patriot   | Flare              | 64 GB  | 6       | 493   | 0     | 1.35   |
| SanDisk   | SDSSDP128G         | 128 GB | 80      | 517   | 4     | 1.35   |
| SanDisk   | SD6SB1M128G1022I   | 128 GB | 7       | 491   | 0     | 1.35   |
| OWC       | Mercury Electra... | 1 TB   | 10      | 488   | 0     | 1.34   |
| Mushkin   | MKNSSDCR240GB      | 240 GB | 4       | 1034  | 522   | 1.34   |
| China     | SATA SSD           | 960 GB | 7       | 647   | 2     | 1.34   |
| Transcend | TS64GSSD320        | 64 GB  | 3       | 487   | 0     | 1.34   |
| Apple     | SSD SM0512G        | 500 GB | 27      | 487   | 0     | 1.34   |
| Toshiba   | THNSFC128GBSJ      | 128 GB | 2       | 486   | 0     | 1.33   |
| Kingston  | SKC400S371T        | 1 TB   | 2       | 1262  | 25    | 1.33   |
| Samsung   | SSD PM810 2.5" 7mm | 128 GB | 9       | 644   | 126   | 1.33   |
| Samsung   | SSD CM871 2.5 7mm  | 128 GB | 4       | 484   | 0     | 1.33   |
| Kingston  | SVP200S37A60G      | 64 GB  | 15      | 558   | 3     | 1.33   |
| Toshiba   | Q300               | 240 GB | 16      | 614   | 2     | 1.33   |
| Micron    | MTFDDAK128MAM-1J1  | 128 GB | 27      | 531   | 3     | 1.33   |
| Lite-On   | PH4-CE120          | 120 GB | 2       | 483   | 0     | 1.32   |
| Samsung   | MZMPC128HBFU-000L1 | 128 GB | 7       | 483   | 0     | 1.32   |
| Intel     | SSDSA2BW120G3A     | 120 GB | 2       | 482   | 0     | 1.32   |
| China     | L06B B0KB          | 960 GB | 2       | 478   | 0     | 1.31   |
| Samsung   | MZ7LN256HCHP-000H1 | 256 GB | 4       | 477   | 0     | 1.31   |
| SanDisk   | SD9SN8W512G1002    | 512 GB | 6       | 476   | 0     | 1.31   |
| Intel     | SSDSC2CT240A4      | 240 GB | 17      | 754   | 3     | 1.31   |
| GLOWAY    | FER240GS3-S7       | 240 GB | 2       | 510   | 506   | 1.31   |
| Goodram   | SSDPR_CX300_120    | 120 GB | 4       | 476   | 0     | 1.30   |
| Samsung   | SG9MSM6D024GPM00   | 22 GB  | 6       | 598   | 2     | 1.30   |
| SanDisk   | SD8SBBU480G1122    | 480 GB | 3       | 473   | 0     | 1.30   |
| Corsair   | Force 3 SSD        | 90 GB  | 7       | 473   | 0     | 1.30   |
| WDC       | WDS100T1B0A-00H9H0 | 1 TB   | 18      | 473   | 0     | 1.30   |
| Samsung   | MZ7TE128HMGR-000L1 | 128 GB | 14      | 473   | 0     | 1.30   |
| Micron    | 5200_MTFDDAK240TDN | 240 GB | 10      | 472   | 0     | 1.30   |
| Intel     | SSDSC2CT180A4      | 180 GB | 11      | 698   | 1     | 1.29   |
| OCZ       | AGILITY2           | 64 GB  | 3       | 472   | 0     | 1.29   |
| Samsung   | SSD 850 EVO mSATA  | 500 GB | 28      | 471   | 0     | 1.29   |
| WDC       | WDS250G1B0A-00H9H0 | 250 GB | 33      | 498   | 31    | 1.29   |
| SanDisk   | Ultra II           | 500 GB | 3       | 470   | 0     | 1.29   |
| Kingston  | SM2280S3G2480G     | 480 GB | 6       | 517   | 21    | 1.29   |
| ADATA     | XM11 256GB-V2      | 256 GB | 4       | 1108  | 254   | 1.29   |
| Samsung   | MZNLF128HCHP-000H1 | 128 GB | 8       | 468   | 0     | 1.28   |
| ADATA     | SU650              | 960 GB | 5       | 467   | 0     | 1.28   |
| Plextor   | PX-64M2S           | 64 GB  | 2       | 467   | 0     | 1.28   |
| Kingston  | SM2280S3G2240G     | 240 GB | 7       | 467   | 0     | 1.28   |
| Samsung   | MZ7LN512HCHP-000L1 | 512 GB | 16      | 466   | 0     | 1.28   |
| Lite-On   | LCH-256V2S-HP      | 256 GB | 2       | 465   | 0     | 1.28   |
| Patriot   | Spark              | 256 GB | 3       | 465   | 0     | 1.28   |
| OCZ       | ARC100             | 240 GB | 21      | 486   | 1     | 1.28   |
| HP        | SSD M700           | 240 GB | 2       | 465   | 0     | 1.27   |
| Toshiba   | TR150              | 480 GB | 11      | 519   | 1     | 1.27   |
| Kingston  | SHSS37A480G        | 480 GB | 16      | 463   | 0     | 1.27   |
| Plextor   | PX-256M7VC         | 256 GB | 5       | 462   | 0     | 1.27   |
| Samsung   | MZ7TE256HMHP-000L2 | 256 GB | 4       | 462   | 0     | 1.27   |
| Kingston  | SM2280S3240G       | 240 GB | 2       | 462   | 0     | 1.27   |
| OCZ       | TRION150           | 240 GB | 9       | 462   | 0     | 1.27   |
| Apple     | SSD TS128A         | 121 GB | 2       | 461   | 0     | 1.26   |
| Kingston  | SM2280S3G2120G     | 120 GB | 13      | 458   | 0     | 1.26   |
| Samsung   | MZRPC128HACD-000SO | 64 GB  | 6       | 458   | 0     | 1.26   |
| Plextor   | PX-512M5Pro        | 512 GB | 3       | 457   | 0     | 1.25   |
| Mushkin   | MKNSSDEC240GB      | 240 GB | 3       | 456   | 0     | 1.25   |
| SK hynix  | SC300 M.2 2280     | 256 GB | 7       | 456   | 0     | 1.25   |
| Plextor   | PX-256S3C          | 256 GB | 3       | 456   | 0     | 1.25   |
| Intel     | SSDMCEAC240B3      | 240 GB | 3       | 456   | 0     | 1.25   |

SSD by Vendor
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF |
|-------------|--------|---------|-------|-------|------|
| Radeon      | 1      | 4       | 778   | 0     | 2.13   |
| SK          | 1      | 2       | 672   | 0     | 1.84   |
| Corsair     | 39     | 311     | 796   | 84    | 1.67   |
| OCZ         | 69     | 829     | 739   | 27    | 1.63   |
| Hajaan      | 1      | 2       | 557   | 0     | 1.53   |
| Samsung     | 311    | 10460   | 486   | 8     | 1.28   |
| OWC         | 6      | 34      | 503   | 3     | 1.26   |
| MyDigita... | 3      | 12      | 461   | 0     | 1.26   |
| Intel       | 160    | 1379    | 580   | 58    | 1.24   |
| Apple       | 24     | 408     | 427   | 12    | 1.13   |
| Toshiba     | 82     | 645     | 429   | 11    | 1.11   |
| Hyundai     | 2      | 6       | 350   | 0     | 0.96   |
| HAJAAN      | 1      | 2       | 335   | 0     | 0.92   |
| AFOX        | 1      | 3       | 333   | 0     | 0.91   |
| Palit       | 4      | 10      | 324   | 0     | 0.89   |
| SuperMicro  | 2      | 5       | 312   | 0     | 0.86   |
| Faspeed     | 2      | 4       | 309   | 0     | 0.85   |
| Mushkin     | 17     | 70      | 385   | 64    | 0.84   |
| Kingston    | 148    | 6435    | 322   | 22    | 0.77   |
| Reeinno     | 1      | 2       | 275   | 0     | 0.75   |
| SanDisk     | 225    | 3683    | 304   | 25    | 0.75   |
| BIOSTAR     | 2      | 5       | 271   | 0     | 0.74   |
| Micron      | 85     | 764     | 339   | 99    | 0.74   |
| minisforum  | 1      | 2       | 253   | 0     | 0.69   |
| GALAX       | 3      | 11      | 248   | 0     | 0.68   |
| addlink     | 2      | 6       | 241   | 0     | 0.66   |
| Seagate     | 24     | 133     | 272   | 31    | 0.66   |
| Crucial     | 75     | 4322    | 281   | 24    | 0.65   |
| Silicon     | 3      | 8       | 236   | 0     | 0.65   |
| Smartbuy    | 12     | 204     | 246   | 1     | 0.64   |
| Hoodisk     | 4      | 29      | 229   | 0     | 0.63   |
| Pioneer     | 6      | 21      | 228   | 0     | 0.63   |
| Transcend   | 60     | 547     | 227   | 17    | 0.58   |
| PNY         | 29     | 528     | 212   | 3     | 0.58   |
| SK hynix    | 63     | 675     | 316   | 98    | 0.58   |
| WDC         | 50     | 2659    | 219   | 6     | 0.57   |
| Patriot     | 31     | 486     | 209   | 4     | 0.56   |
| SPCC        | 25     | 856     | 235   | 60    | 0.55   |
| Goodram     | 35     | 455     | 203   | 1     | 0.55   |
| XSTAR       | 2      | 4       | 198   | 2     | 0.54   |
| HP          | 21     | 154     | 201   | 22    | 0.51   |
| ADATA       | 89     | 1546    | 222   | 57    | 0.50   |
| Kston       | 1      | 5       | 180   | 0     | 0.49   |
| DeTech      | 1      | 3       | 179   | 0     | 0.49   |
| Team        | 40     | 228     | 191   | 4     | 0.48   |
| Phison      | 16     | 133     | 171   | 1     | 0.47   |
| Gigabyte    | 7      | 94      | 167   | 0     | 0.46   |
| Plextor     | 52     | 388     | 177   | 40    | 0.45   |
| Innodisk    | 10     | 25      | 212   | 125   | 0.44   |
| UNIC2       | 1      | 5       | 160   | 0     | 0.44   |
| Londisk     | 3      | 19      | 159   | 0     | 0.44   |
| Ramaxel     | 3      | 6       | 158   | 0     | 0.43   |
| Vaseky      | 6      | 18      | 162   | 2     | 0.43   |
| KingFast    | 8      | 98      | 159   | 32    | 0.43   |
| tigo        | 1      | 2       | 155   | 0     | 0.43   |
| Maxtor      | 3      | 21      | 155   | 0     | 0.43   |
| ADTEC       | 1      | 2       | 152   | 0     | 0.42   |
| KINGBANK    | 2      | 8       | 151   | 0     | 0.41   |
| JASTER      | 1      | 3       | 147   | 0     | 0.40   |
| Union Me... | 1      | 12      | 145   | 0     | 0.40   |
| KingDian    | 14     | 141     | 150   | 64    | 0.39   |
| Drevo       | 3      | 19      | 286   | 153   | 0.38   |
| China       | 96     | 1216    | 145   | 13    | 0.37   |
| RZX         | 1      | 2       | 134   | 0     | 0.37   |
| GeIL        | 2      | 6       | 132   | 0     | 0.36   |
| ZTC         | 2      | 5       | 128   | 0     | 0.35   |
| Gigabyte... | 6      | 87      | 128   | 0     | 0.35   |
| LDLC        | 12     | 61      | 170   | 32    | 0.35   |
| Kingmax     | 4      | 70      | 255   | 302   | 0.34   |
| GLOWAY      | 5      | 14      | 133   | 73    | 0.34   |
| Hypertec    | 1      | 2       | 371   | 512   | 0.33   |
| G.Skill     | 1      | 2       | 756   | 510   | 0.33   |
| Intenso     | 33     | 421     | 123   | 36    | 0.31   |
| TCSUNBOW    | 6      | 24      | 113   | 0     | 0.31   |
| Colorful    | 6      | 20      | 123   | 63    | 0.31   |
| Apacer      | 21     | 380     | 136   | 16    | 0.31   |
| GS Nanotech | 1      | 2       | 111   | 0     | 0.31   |
| Pichau      | 1      | 2       | 108   | 0     | 0.30   |
| AGI         | 3      | 6       | 108   | 0     | 0.30   |
| T-FORCE     | 4      | 33      | 103   | 1     | 0.28   |
| Lexar       | 11     | 132     | 102   | 1     | 0.28   |
| Star Drive  | 1      | 5       | 99    | 0     | 0.27   |
| e2e4        | 3      | 8       | 98    | 0     | 0.27   |
| Verbatim    | 5      | 45      | 100   | 23    | 0.27   |
| AMD         | 11     | 146     | 116   | 14    | 0.27   |
| Inland      | 2      | 5       | 98    | 0     | 0.27   |
| S3+         | 2      | 4       | 97    | 0     | 0.27   |
| KingSpec    | 32     | 279     | 124   | 39    | 0.27   |
| Integral    | 4      | 21      | 93    | 0     | 0.26   |
| TwinMOS     | 1      | 2       | 93    | 0     | 0.26   |
| BAITITON    | 5      | 14      | 131   | 4     | 0.25   |
| Zheino      | 12     | 30      | 97    | 1     | 0.25   |
| Lite-On     | 79     | 480     | 114   | 121   | 0.25   |
| BHT         | 6      | 26      | 89    | 0     | 0.25   |
| VisionTek   | 1      | 2       | 88    | 0     | 0.24   |
| Super Ta... | 5      | 12      | 115   | 1     | 0.24   |
| MicroFrom   | 1      | 2       | 87    | 0     | 0.24   |
| XUM         | 1      | 3       | 87    | 0     | 0.24   |
| SUNEAST     | 2      | 4       | 206   | 44    | 0.24   |
| AirDisk     | 1      | 4       | 87    | 0     | 0.24   |
| ShanDianZhe | 3      | 9       | 87    | 0     | 0.24   |
| Lenovo      | 3      | 9       | 122   | 1     | 0.23   |
| BIWIN       | 5      | 30      | 97    | 103   | 0.23   |
| EVM         | 1      | 3       | 82    | 0     | 0.23   |
| INNOVATI... | 11     | 35      | 86    | 1     | 0.23   |
| Kingchuxing | 4      | 12      | 79    | 0     | 0.22   |
| Kross El... | 1      | 2       | 86    | 1     | 0.20   |
| ASENNO      | 3      | 7       | 124   | 4     | 0.20   |
| VISIPRO     | 2      | 5       | 69    | 3     | 0.19   |
| FORESEE     | 6      | 70      | 67    | 0     | 0.19   |
| Hikvision   | 12     | 70      | 74    | 1     | 0.18   |
| Dogfish     | 9      | 59      | 69    | 1     | 0.18   |
| Leven       | 8      | 49      | 71    | 2     | 0.17   |
| TrekStor    | 1      | 2       | 122   | 78    | 0.17   |
| EMTEC       | 5      | 39      | 61    | 0     | 0.17   |
| SuperSSpeed | 1      | 2       | 312   | 23    | 0.17   |
| Platinet    | 1      | 3       | 61    | 30    | 0.17   |
| TEKET       | 1      | 2       | 59    | 0     | 0.16   |
| ASMedia     | 1      | 4       | 55    | 0     | 0.15   |
| Advantech   | 3      | 6       | 55    | 0     | 0.15   |
| Avant       | 1      | 2       | 823   | 508   | 0.15   |
| ORTIAL      | 3      | 14      | 53    | 0     | 0.15   |
| Foxline     | 8      | 27      | 52    | 0     | 0.14   |
| Win Memory  | 2      | 4       | 52    | 0     | 0.14   |
| XrayDisk    | 9      | 58      | 57    | 20    | 0.13   |
| Anobit      | 1      | 2       | 48    | 1     | 0.13   |
| HGST        | 1      | 3       | 48    | 0     | 0.13   |
| Solid       | 2      | 5       | 50    | 1     | 0.13   |
| Netac       | 13     | 255     | 55    | 14    | 0.13   |
| XPG         | 1      | 3       | 46    | 0     | 0.13   |
| RCESSD      | 1      | 2       | 46    | 0     | 0.13   |
| KIOXIA-E... | 3      | 47      | 45    | 0     | 0.12   |
| CFD         | 1      | 2       | 44    | 0     | 0.12   |
| Qumo        | 2      | 7       | 124   | 146   | 0.11   |
| Timetec     | 1      | 3       | 42    | 1     | 0.11   |
| MidasForce  | 4      | 10      | 40    | 0     | 0.11   |
| VERICO      | 1      | 2       | 36    | 0     | 0.10   |
| OYUNKEY     | 1      | 2       | 215   | 66    | 0.10   |
| Biostar     | 1      | 3       | 35    | 0     | 0.10   |
| V-GeN       | 2      | 4       | 34    | 0     | 0.10   |
| TAMMUZ      | 2      | 5       | 34    | 0     | 0.09   |
| ZOTAC       | 1      | 2       | 34    | 0     | 0.09   |
| Acer        | 3      | 10      | 34    | 0     | 0.09   |
| Teclast     | 7      | 35      | 40    | 1     | 0.09   |
| AEGO        | 1      | 3       | 33    | 0     | 0.09   |
| Dahua       | 1      | 2       | 33    | 0     | 0.09   |
| KeepData    | 1      | 3       | 32    | 0     | 0.09   |
| KLEVV       | 2      | 4       | 35    | 763   | 0.09   |
| HEORIADY    | 1      | 2       | 32    | 0     | 0.09   |
| SCY         | 1      | 4       | 28    | 0     | 0.08   |
| GSemi       | 1      | 3       | 43    | 8     | 0.08   |
| Gateway     | 1      | 3       | 28    | 0     | 0.08   |
| QUMO        | 5      | 14      | 49    | 3     | 0.07   |
| Fanxiang    | 3      | 13      | 32    | 7     | 0.07   |
| WALRAM      | 4      | 17      | 25    | 6     | 0.06   |
| Dell        | 2      | 8       | 20    | 0     | 0.06   |
| Neo Forza   | 3      | 8       | 53    | 258   | 0.05   |
| JUMPER      | 1      | 2       | 19    | 0     | 0.05   |
| Valuetech   | 1      | 2       | 18    | 0     | 0.05   |
| TEXTORM     | 3      | 7       | 18    | 5     | 0.05   |
| ZHITAI      | 3      | 7       | 18    | 0     | 0.05   |
| VSEVEN      | 1      | 2       | 17    | 0     | 0.05   |
| Kingrich    | 1      | 2       | 17    | 0     | 0.05   |
| Yeyian      | 2      | 4       | 15    | 0     | 0.04   |
| Ramsta      | 1      | 2       | 13    | 0     | 0.04   |
| BR          | 1      | 2       | 13    | 0     | 0.04   |
| AXIOMTEK    | 1      | 28      | 12    | 0     | 0.03   |
| INDMEM      | 1      | 2       | 12    | 0     | 0.03   |
| Azerty      | 1      | 4       | 12    | 0     | 0.03   |
| UMAX        | 1      | 3       | 11    | 0     | 0.03   |
| iODD        | 2      | 4       | 11    | 0     | 0.03   |
| Maximus     | 1      | 4       | 10    | 0     | 0.03   |
| 2-Power     | 1      | 2       | 10    | 3     | 0.03   |
| DGM         | 1      | 2       | 79    | 21    | 0.03   |
| Kimtigo     | 2      | 13      | 10    | 0     | 0.03   |
| ACOS        | 1      | 2       | 53    | 508   | 0.03   |
| Zozt        | 1      | 2       | 9     | 0     | 0.03   |
| MIXZA       | 1      | 2       | 8     | 0     | 0.02   |
| Digma       | 3      | 8       | 7     | 1     | 0.02   |
| Hanye       | 1      | 2       | 6     | 0     | 0.02   |
| ShiJi       | 4      | 13      | 33    | 29    | 0.01   |
| Protectli   | 1      | 2       | 4     | 0     | 0.01   |
| Veno        | 1      | 2       | 4     | 0     | 0.01   |
| MicroDream  | 1      | 2       | 4     | 0     | 0.01   |
| SATAFIRM    | 1      | 4       | 123   | 68    | 0.01   |
| Supersonic  | 1      | 2       | 3     | 0     | 0.01   |
| IOD         | 1      | 2       | 3     | 0     | 0.01   |
| Wibtek      | 1      | 10      | 2     | 11    | 0.01   |
| Cactus      | 1      | 2       | 2     | 0     | 0.01   |
| Xinhaike    | 1      | 2       | 1     | 0     | 0.01   |
| KODAK       | 1      | 2       | 1     | 0     | 0.01   |
| DEPO        | 1      | 2       | 1     | 108   | 0.00   |
| VICKTER     | 1      | 3       | 1     | 0     | 0.00   |
| LEQIXIANG   | 1      | 3       | 1     | 2     | 0.00   |
| Indilinx    | 2      | 4       | 0     | 0     | 0.00   |
| HP Phison   | 1      | 2       | 628   | 1032  | 0.00   |
| Blackpcs    | 1      | 2       | 0     | 0     | 0.00   |
| ExeGate     | 2      | 5       | 0     | 0     | 0.00   |
| DOGGO       | 1      | 2       | 0     | 0     | 0.00   |
| SSSTC       | 1      | 8       | 40    | 1008  | 0.00   |

NVME by Model
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

See full list of tested NVMe samples in the Appendix 5 ([All_NVMe.md](/All_NVMe.md)).

See top 1000 of tested NVMe models in the [Top1000_NVMe.md](/Top1000_NVMe.md).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| Intel     | MEMPEK1J016GAD     | 16 GB  | 2       | 5999  | 0     | 16.44  |
| Intel     | H10 HBRPEKNX020... | 32 GB  | 2       | 4259  | 0     | 11.67  |
| Intel     | H10 HBRPEKNX020... | 32 GB  | 15      | 3084  | 0     | 8.45   |
| Intel     | SSDPEDMW400G4      | 400 GB | 8       | 1535  | 0     | 4.21   |
| Intel     | SSDPEDMD400G4      | 400 GB | 4       | 1389  | 0     | 3.81   |
| Intel     | SSDPEDMW012T4      | 1.2 TB | 5       | 1371  | 0     | 3.76   |
| Samsung   | SSD 950 PRO        | 256 GB | 22      | 1052  | 0     | 2.88   |
| Intel     | SSDPEKKF256G7H     | 256 GB | 25      | 1046  | 41    | 2.82   |
| ZOTAC     | ZTSSDPG3-480G-GE   | 480 GB | 2       | 919   | 0     | 2.52   |
| SanDisk   | A400 NVMe          | 256 GB | 2       | 917   | 0     | 2.51   |
| Toshiba   | KXG50PNV1T02 NVMe  | 1 TB   | 6       | 868   | 0     | 2.38   |
| Toshiba   | THNSN5512GPU7 NVMe | 512 GB | 8       | 856   | 0     | 2.35   |
| Toshiba   | RD400              | 1 TB   | 3       | 855   | 0     | 2.34   |
| Samsung   | SSD 983 DCT 1.92TB | 1.9 TB | 2       | 850   | 0     | 2.33   |
| Samsung   | SSD 950 PRO        | 512 GB | 49      | 841   | 0     | 2.30   |
| Intel     | SSDPEKKF512G7H     | 512 GB | 5       | 754   | 0     | 2.07   |
| Toshiba   | RD400              | 256 GB | 5       | 751   | 0     | 2.06   |
| Samsung   | MZVLB1T0HALR-000H2 | 1 TB   | 3       | 751   | 0     | 2.06   |
| Intel     | SSDPEKKW512G7      | 512 GB | 25      | 928   | 118   | 1.99   |
| Silico... | Asgard AN3 2TNV... | 2 TB   | 14      | 718   | 0     | 1.97   |
| WDC       | WDS512G1X0C-00ENX0 | 512 GB | 14      | 714   | 0     | 1.96   |
| Samsung   | SM951 NVMe         | 256 GB | 2       | 695   | 0     | 1.91   |
| ADATA     | SX8000NP           | 128 GB | 2       | 680   | 0     | 1.86   |
| Samsung   | MZQLB960HAJR-00007 | 960 GB | 12      | 675   | 0     | 1.85   |
| Samsung   | MZWLL1T6HAJQ-00005 | 1.6 TB | 4       | 673   | 0     | 1.85   |
| Corsair   | Force MP500        | 120 GB | 13      | 670   | 0     | 1.84   |
| Kingston  | RBUSNS8154P3102... | 1 TB   | 2       | 667   | 0     | 1.83   |
| Samsung   | MZVPV256HDGL-00000 | 256 GB | 15      | 667   | 0     | 1.83   |
| Samsung   | MZVPV256HDGL-000H1 | 256 GB | 7       | 661   | 0     | 1.81   |
| Intel     | SSDPE2MX450G7      | 450 GB | 4       | 658   | 0     | 1.80   |
| Intel     | SSDPED1D480GA      | 480 GB | 4       | 655   | 0     | 1.80   |
| Toshiba   | KXG50PNV2T04 NVMe  | 2 TB   | 4       | 653   | 0     | 1.79   |
| Corsair   | Force MP500        | 240 GB | 12      | 728   | 1     | 1.76   |
| Intel     | SSDPE21D480GA      | 480 GB | 6       | 643   | 0     | 1.76   |
| Intel     | SSDPEKKW256G7      | 256 GB | 65      | 808   | 31    | 1.76   |
| Samsung   | MZVPV512HDGL-00000 | 512 GB | 10      | 631   | 0     | 1.73   |
| Intel     | SSDPEKKW010T7      | 1 TB   | 5       | 1095  | 6     | 1.71   |
| Intel     | SSDPEKKW128G7      | 128 GB | 14      | 1056  | 2     | 1.71   |
| Toshiba   | KBG20ZMS256G NVMe  | 256 GB | 2       | 605   | 0     | 1.66   |
| Samsung   | MZQLB960HAJR-00003 | 960 GB | 4       | 588   | 0     | 1.61   |
| Kingston  | SKC1000240G        | 240 GB | 4       | 585   | 0     | 1.61   |
| Toshiba   | THNSN5256GPU7      | 256 GB | 15      | 582   | 0     | 1.59   |
| Intel     | SSDPEKKF256G7L     | 256 GB | 37      | 699   | 69    | 1.59   |
| Phison    | APS-SE20G-256      | 256 GB | 2       | 580   | 0     | 1.59   |
| Intel     | SSDPEKKF360G7H     | 360 GB | 7       | 572   | 0     | 1.57   |
| WDC       | CL SN720 SDAQNT... | 512 GB | 2       | 570   | 0     | 1.56   |
| Samsung   | MZVPV512HDGL-000H1 | 512 GB | 5       | 557   | 0     | 1.53   |
| Intel     | SSDPED1D280GA      | 280 GB | 5       | 536   | 0     | 1.47   |
| Toshiba   | THNSN5512GPUK NVMe | 512 GB | 36      | 524   | 0     | 1.44   |
| Hikvision | HS-SSD-E2000 512G  | 512 GB | 2       | 522   | 0     | 1.43   |
| Samsung   | MZVKV512HAJH-000L1 | 512 GB | 15      | 520   | 0     | 1.42   |
| Toshiba   | THNSN5256GPUK NVMe | 256 GB | 20      | 513   | 0     | 1.41   |
| Plextor   | PX-512M9PeG        | 512 GB | 4       | 512   | 0     | 1.40   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 2       | 495   | 0     | 1.36   |
| Samsung   | MZVKW1T0HMLH-000L7 | 1 TB   | 2       | 495   | 0     | 1.36   |
| Samsung   | PM951 NVMe         | 512 GB | 13      | 487   | 0     | 1.34   |
| Intel     | MEMPEK1W032GA      | 32 GB  | 6       | 479   | 0     | 1.31   |
| Toshiba   | THNSN51T02DUK NVMe | 1 TB   | 13      | 478   | 0     | 1.31   |
| Toshiba   | THNSF5256GPUK      | 256 GB | 10      | 475   | 0     | 1.30   |
| Samsung   | MZVKW1T0HMLH-00000 | 1 TB   | 4       | 475   | 0     | 1.30   |
| Samsung   | MZVLV128HCGR-00000 | 128 GB | 4       | 466   | 0     | 1.28   |
| Kingston  | SEDC1000BM8960G    | 960 GB | 2       | 466   | 0     | 1.28   |
| Toshiba   | KXG50ZNV512G NVMe  | 512 GB | 66      | 461   | 0     | 1.27   |
| Kingston  | SKC1000480G        | 480 GB | 4       | 456   | 0     | 1.25   |
| Toshiba   | KXG50ZNV256G NVMe  | 256 GB | 43      | 456   | 0     | 1.25   |
| Samsung   | MZVPV128HDGM-00000 | 128 GB | 11      | 449   | 0     | 1.23   |
| Mushkin   | MKNSSDHL250GB-D8   | 250 GB | 5       | 467   | 202   | 1.22   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 3       | 443   | 0     | 1.21   |
| Phison    | Neutron NX500      | 800 GB | 2       | 442   | 0     | 1.21   |
| Samsung   | PM951 NVMe         | 1 TB   | 4       | 440   | 0     | 1.21   |
| Kingston  | SKC2000M8250G      | 250 GB | 5       | 437   | 0     | 1.20   |
| ADATA     | SX8200NP           | 480 GB | 10      | 436   | 0     | 1.20   |
| Lexar     | SSD                | 512 GB | 2       | 435   | 0     | 1.19   |
| Toshiba   | KXG50ZNV1T02       | 1 TB   | 5       | 428   | 0     | 1.17   |
| Lexar     | SSD                | 256 GB | 7       | 427   | 0     | 1.17   |
| KIOXIA    | KXG60PNV1T02 NVMe  | 1 TB   | 4       | 412   | 0     | 1.13   |
| Toshiba   | KXG5AZNV256G NV... | 256 GB | 2       | 412   | 0     | 1.13   |
| Patriot   | Hellfire M2        | 240 GB | 3       | 400   | 0     | 1.10   |
| Intel     | HBRPEKNX0202ACO    | 32 GB  | 2       | 398   | 0     | 1.09   |
| Samsung   | MZVLV256HCHP-00000 | 256 GB | 17      | 398   | 0     | 1.09   |
| HP        | SSD EX920          | 512 GB | 17      | 396   | 0     | 1.09   |
| Toshiba   | KXG50ZNV1T02 NVMe  | 1 TB   | 25      | 396   | 0     | 1.09   |
| Samsung   | PM951 NVMe         | 256 GB | 17      | 388   | 0     | 1.07   |
| ADATA     | SX6000NP           | 256 GB | 4       | 387   | 0     | 1.06   |
| Lite-On   | CL1-3D128-Q11 NVMe | 128 GB | 4       | 384   | 0     | 1.05   |
| WDC       | WDS500G2X0C-00L350 | 500 GB | 28      | 376   | 0     | 1.03   |
| Toshiba   | THNSN5512GPUK      | 512 GB | 13      | 370   | 0     | 1.02   |
| SanDisk   | A400 NVMe          | 512 GB | 3       | 370   | 0     | 1.01   |
| Intel     | SSDPEK1W060GA      | 64 GB  | 3       | 368   | 0     | 1.01   |
| Toshiba   | THNSN5128GPU7      | 128 GB | 11      | 362   | 0     | 0.99   |
| Intel     | SSDPE2MX012T7      | 1.2 TB | 4       | 358   | 0     | 0.98   |
| Intel     | HBRPEKNX0202AC     | 512 GB | 2       | 357   | 0     | 0.98   |
| Toshiba   | THNSN5512GPU7      | 512 GB | 10      | 355   | 0     | 0.97   |
| ZHITAI    | PC005 Active       | 1 TB   | 3       | 355   | 0     | 0.97   |
| Toshiba   | KXG5AZNV256G       | 256 GB | 16      | 354   | 0     | 0.97   |
| WDC       | WDS200T3XHC-00SJG0 | 2 TB   | 4       | 353   | 0     | 0.97   |
| WDC       | WDS100T2X0C-00L350 | 1 TB   | 12      | 348   | 0     | 0.96   |
| Intel     | MEMPEK1J016GA      | 16 GB  | 13      | 371   | 78    | 0.95   |
| SK hynix  | PC300 NVMe         | 512 GB | 8       | 348   | 0     | 0.95   |
| ADATA     | SX7000NP           | 128 GB | 3       | 554   | 39    | 0.95   |
| Intel     | SSDPEKKF010T8      | 1 TB   | 6       | 347   | 0     | 0.95   |
| Toshiba   | RD400              | 512 GB | 4       | 345   | 0     | 0.95   |
| Silico... | NVME SSD           | 1 TB   | 3       | 343   | 0     | 0.94   |
| Intel     | SSDPEK1W120GA      | 118 GB | 2       | 341   | 0     | 0.94   |
| WDC       | WDS250G2X0C-00L350 | 250 GB | 19      | 340   | 0     | 0.93   |
| WDC       | WDS500G1B0C-00S6U0 | 500 GB | 20      | 340   | 0     | 0.93   |
| Corsair   | Force MP600        | 2 TB   | 18      | 339   | 0     | 0.93   |
| WDC       | WDS256G1X0C-00ENX0 | 256 GB | 14      | 337   | 0     | 0.92   |
| Plextor   | PX-256M8PeGN       | 256 GB | 4       | 336   | 0     | 0.92   |
| Samsung   | MZVLV256HCHP-000L2 | 256 GB | 11      | 333   | 0     | 0.91   |
| Micron    | 9300_MTFDHAL15T... | 15.... | 3       | 333   | 0     | 0.91   |
| Corsair   | Force MP300        | 480 GB | 3       | 332   | 0     | 0.91   |
| Samsung   | MZVLV512HCJH-000L2 | 512 GB | 2       | 330   | 0     | 0.90   |
| Intel     | SSDPE2KX020T8      | 2 TB   | 8       | 329   | 0     | 0.90   |
| addlink   | M.2 PCIE G3x4 NVMe | 1 TB   | 17      | 326   | 0     | 0.90   |
| Toshiba   | KXG5AZNV512G NV... | 512 GB | 2       | 324   | 0     | 0.89   |
| Intel     | MEMPEK1W016GA      | 16 GB  | 9       | 322   | 0     | 0.88   |
| Lite-On   | CX2-8B256-Q11 NVMe | 256 GB | 8       | 319   | 0     | 0.88   |
| Intel     | SSDPEKKF512G7L     | 512 GB | 6       | 407   | 213   | 0.87   |
| WDC       | WDS250G1B0C-00S6U0 | 250 GB | 16      | 317   | 0     | 0.87   |
| Toshiba   | KXG50ZNV512G       | 512 GB | 56      | 317   | 0     | 0.87   |
| Toshiba   | KXG60ZNV512G NVMe  | 512 GB | 44      | 317   | 0     | 0.87   |
| Toshiba   | THNSF5512GPUK      | 512 GB | 13      | 316   | 0     | 0.87   |
| KINGBANK  | KP230              | 512 GB | 2       | 312   | 0     | 0.86   |
| WDC       | WDBA3V5000ANC-WRSN | 500 GB | 2       | 310   | 0     | 0.85   |
| Toshiba   | KXG5AZNV1T02       | 1 TB   | 5       | 310   | 0     | 0.85   |
| Toshiba   | KXG60ZNV1T02       | 1 TB   | 27      | 305   | 0     | 0.84   |
| Goodram   | SSDPR-PX500-01T-80 | 1 TB   | 7       | 304   | 0     | 0.83   |
| ADATA     | SX6000NP           | 128 GB | 7       | 362   | 167   | 0.83   |
| Corsair   | Force MP510        | 960 GB | 36      | 301   | 0     | 0.82   |
| Samsung   | MZQLB3T8HALS-00007 | 3.8 TB | 13      | 300   | 0     | 0.82   |
| SPCC      | M.2 PCIE SSD       | 1 TB   | 7       | 300   | 0     | 0.82   |
| Patriot   | Scorch M2          | 512 GB | 4       | 300   | 0     | 0.82   |
| Plextor   | PX-256M9PeG        | 256 GB | 6       | 299   | 0     | 0.82   |
| Intel     | SSDPEKNW020T8      | 2 TB   | 74      | 310   | 1     | 0.82   |
| Intel     | SSDPEK1W120GAH     | 118 GB | 2       | 296   | 0     | 0.81   |
| Micron    | 7300_MTFDHBE6T4TDG | 6.4 TB | 2       | 293   | 0     | 0.80   |
| Toshiba   | THNSN5256GPUK      | 256 GB | 8       | 430   | 17    | 0.80   |
| ADATA     | SX6000NP           | 512 GB | 6       | 327   | 19    | 0.80   |
| Samsung   | MZVKW512HMJP-000H1 | 512 GB | 16      | 297   | 1     | 0.79   |
| Corsair   | Force MP300        | 240 GB | 3       | 289   | 0     | 0.79   |
| Plextor   | PX-512M9PGN +      | 512 GB | 3       | 287   | 0     | 0.79   |
| Aura      | Pro X2             | 960 GB | 5       | 287   | 0     | 0.79   |
| PNY       | CS3030 1000GB SSD  | 1 TB   | 4       | 287   | 0     | 0.79   |
| Kingston  | SKC2000M8500G      | 500 GB | 3       | 287   | 0     | 0.79   |
| Toshiba   | KBG40ZPZ256G ME... | 256 GB | 3       | 286   | 0     | 0.79   |
| Intel     | HBRPEKNX0203AHO    | 32 GB  | 17      | 285   | 0     | 0.78   |
| Samsung   | MZVKW1T0HMLH-000H1 | 1 TB   | 7       | 285   | 0     | 0.78   |
| Phison    | Sabrent Rocket 4.0 | 2 TB   | 20      | 285   | 0     | 0.78   |
| XPG       | GAMMIX S11         | 480 GB | 9       | 362   | 112   | 0.78   |
| Gigaby... | GP-ASM2NE6100TTTD  | 1 TB   | 11      | 283   | 0     | 0.78   |
| Toshiba   | KXG60ZNV1T02 NVMe  | 1 TB   | 16      | 281   | 0     | 0.77   |
| Silico... | M Series NVMe S... | 256 GB | 4       | 277   | 0     | 0.76   |
| SSSTC     | CL1-3D256          | 256 GB | 3       | 276   | 0     | 0.76   |
| Samsung   | MZVKW512HMJP-00000 | 512 GB | 11      | 337   | 3     | 0.75   |
| SanDisk   | WD_BLACK SN850     | 2 TB   | 2       | 273   | 0     | 0.75   |
| Intel     | MEMPEK1J016GAL     | 16 GB  | 11      | 273   | 0     | 0.75   |
| Corsair   | Force MP600        | 1 TB   | 84      | 271   | 0     | 0.74   |
| Samsung   | MZFLV512HCJH-000MV | 512 GB | 4       | 269   | 0     | 0.74   |
| Lite-On   | CA1-8D256-HP       | 256 GB | 2       | 269   | 0     | 0.74   |
| J.ZAO     | 5 SERIES 512GB SSD | 512 GB | 2       | 267   | 0     | 0.73   |
| Team      | TM8FP6002T         | 2 TB   | 4       | 265   | 0     | 0.73   |
| Kingston  | SNVS2000GB         | 2 TB   | 2       | 264   | 0     | 0.72   |
| Toshiba   | KBG40ZNS256G ME... | 256 GB | 3       | 262   | 0     | 0.72   |
| Samsung   | MZSLW1T0HMLH-000L1 | 1 TB   | 5       | 261   | 0     | 0.72   |
| Intel     | SSDPEKKF512G8 NVMe | 512 GB | 10      | 261   | 0     | 0.72   |
| Toshiba   | KBG40ZNS512G NVMe  | 512 GB | 16      | 261   | 0     | 0.72   |
| AMD       | R5MP120G8          | 120 GB | 10      | 258   | 0     | 0.71   |
| Transcend | TS512GMTE220S      | 512 GB | 22      | 257   | 0     | 0.71   |
| Phison    | Sabrent            | 1 TB   | 176     | 254   | 0     | 0.70   |
| SPCC      | M.2 PCIe SSD       | 128 GB | 4       | 253   | 0     | 0.70   |
| Toshiba   | KBG30ZMS128G NVMe  | 128 GB | 13      | 253   | 0     | 0.70   |
| Intel     | MEMPEI1J016GAL     | 16 GB  | 3       | 252   | 0     | 0.69   |
| Intel     | MEMPEK1J016GAH     | 16 GB  | 6       | 251   | 0     | 0.69   |
| Intel     | HBRPEKNX0203AH     | 1 TB   | 17      | 249   | 0     | 0.68   |
| Goodram   | IR-SSDPR-P34B-2... | 256 GB | 2       | 249   | 0     | 0.68   |
| T-FORCE   | TM8FP5001T         | 1 TB   | 3       | 248   | 0     | 0.68   |
| Toshiba   | THNSN51T02DUK      | 1 TB   | 2       | 246   | 0     | 0.68   |
| Toshiba   | KXG5AZNV512G       | 512 GB | 18      | 246   | 0     | 0.68   |
| Crucial   | CT1000P1SSD8       | 1 TB   | 240     | 260   | 23    | 0.67   |
| Phison    | BPX                | 240 GB | 6       | 327   | 5     | 0.67   |
| Intel     | SSDPEKNW020T9      | 2 TB   | 3       | 245   | 0     | 0.67   |
| T-FORCE   | TM8FP8001T         | 1 TB   | 2       | 243   | 0     | 0.67   |
| ADATA     | SX8200PNP          | 1 TB   | 131     | 247   | 6     | 0.67   |
| Samsung   | MZ1LB960HAJQ-00007 | 960 GB | 5       | 243   | 0     | 0.67   |
| XPG       | GAMMIX S50         | 1 TB   | 9       | 243   | 0     | 0.67   |
| Plextor   | PX-256M9PeGN       | 256 GB | 4       | 240   | 0     | 0.66   |
| WDC       | WDS100T3XHC-00SJG0 | 1 TB   | 18      | 240   | 0     | 0.66   |
| ADATA     | SX8200NP           | 960 GB | 3       | 239   | 0     | 0.66   |
| Samsung   | MZVLV256HCHP-000H1 | 256 GB | 11      | 239   | 0     | 0.66   |
| Seagate   | BarraCuda 510 S... | 500 GB | 4       | 238   | 0     | 0.65   |
| SK hynix  | PC601A NVMe        | 512 GB | 2       | 237   | 0     | 0.65   |
| Intel     | SSDPEKKW256G8      | 256 GB | 52      | 237   | 0     | 0.65   |
| Lite-On   | CL1-4D128          | 128 GB | 2       | 236   | 0     | 0.65   |
| KIOXIA    | KXG60PNV2T04 NVMe  | 2 TB   | 14      | 234   | 0     | 0.64   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 14      | 232   | 0     | 0.64   |
| Toshiba   | KBG40ZPZ512G NVMe  | 512 GB | 3       | 232   | 0     | 0.64   |
| Seagate   | FireCuda 510 SS... | 1 TB   | 11      | 231   | 0     | 0.64   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 4       | 231   | 0     | 0.63   |
| Toshiba   | THNSN0128GTYA      | 128 GB | 4       | 231   | 0     | 0.63   |
| Transcend | TS1TMTE220S        | 1 TB   | 11      | 230   | 0     | 0.63   |
| KIOXIA... | SSD                | 1 TB   | 5       | 230   | 0     | 0.63   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 7       | 230   | 0     | 0.63   |
| Hikvision | HS-SSD-E2000       | 256 GB | 2       | 229   | 0     | 0.63   |
| Corsair   | Force MP600        | 500 GB | 19      | 229   | 0     | 0.63   |
| ADATA     | SX8200NP           | 240 GB | 6       | 251   | 20    | 0.62   |
| XPG       | GAMMIX S70         | 2 TB   | 7       | 226   | 0     | 0.62   |
| Intel     | H10 HBRPEKNX020... | 512 GB | 34      | 225   | 0     | 0.62   |
| Kingston  | SKC2000M81000G     | 1 TB   | 6       | 225   | 0     | 0.62   |
| Goodram   | IR-SSDPR-P34B-0... | 2 TB   | 5       | 225   | 0     | 0.62   |
| Intel     | SSDPEKNW010T8      | 1 TB   | 257     | 225   | 4     | 0.61   |
| Corsair   | Force MP300        | 120 GB | 3       | 223   | 0     | 0.61   |
| SanDisk   | Extreme Pro        | 1 TB   | 9       | 221   | 0     | 0.61   |
| Corsair   | Force MP510 1.9TB  | 1.9 TB | 14      | 221   | 0     | 0.61   |
| Intel     | SSDPEKKW256G8L     | 256 GB | 6       | 220   | 0     | 0.60   |
| HP        | SSD EX950          | 1 TB   | 14      | 219   | 0     | 0.60   |
| T-FORCE   | TM8FP7001T         | 1 TB   | 3       | 218   | 0     | 0.60   |
| Intel     | HBRPEKNX0202AHO    | 32 GB  | 51      | 224   | 8     | 0.60   |
| Transcend | TS128GMTE110S      | 128 GB | 18      | 218   | 0     | 0.60   |
| Samsung   | SSD 960 PRO        | 512 GB | 81      | 235   | 16    | 0.60   |
| AMD       | R5MP240G8          | 240 GB | 6       | 217   | 0     | 0.60   |
| Samsung   | SSD 960 PRO        | 1 TB   | 28      | 243   | 5     | 0.59   |
| Toshiba   | KBG30ZMS512G NVMe  | 512 GB | 6       | 226   | 168   | 0.59   |
| Toshiba   | RC500              | 500 GB | 5       | 216   | 0     | 0.59   |
| KIOXIA    | KXG7AZNV512G LA    | 512 GB | 5       | 215   | 0     | 0.59   |
| Samsung   | MZFLV256HCHP-000MV | 256 GB | 10      | 215   | 0     | 0.59   |
| SPCC      | M.2 PCIe SSD       | 1 TB   | 59      | 215   | 18    | 0.59   |
| SK hynix  | HFS256GD9MNE-6200A | 256 GB | 3       | 214   | 0     | 0.59   |
| SanDisk   | Extreme Pro        | 500 GB | 15      | 214   | 0     | 0.59   |
| LDLC      | F8+M.2 480         | 480 GB | 3       | 213   | 0     | 0.59   |
| Intel     | SSDPEKKW128G8      | 128 GB | 18      | 213   | 0     | 0.59   |
| Lenovo    | LENSE20256GMSP3... | 256 GB | 30      | 226   | 7     | 0.58   |
| Phison    | ESR512GTLCG-EAC-4  | 512 GB | 4       | 212   | 0     | 0.58   |
| Corsair   | MP400              | 4 TB   | 3       | 212   | 0     | 0.58   |
| Crucial   | CT500P1SSD8        | 500 GB | 120     | 218   | 5     | 0.58   |
| Intel     | SSDPEKKW512G8      | 512 GB | 21      | 210   | 0     | 0.58   |
| Intel     | SSDPEL1K100GA      | 100 GB | 2       | 382   | 5     | 0.58   |
| SK hynix  | PC601 NVMe         | 1 TB   | 10      | 209   | 0     | 0.58   |
| Phison    | Sabrent Rocket 4.0 | 1 TB   | 87      | 209   | 0     | 0.57   |
| Toshiba   | KXG50ZNV256G       | 256 GB | 32      | 209   | 0     | 0.57   |
| Toshiba   | THNSN51T02DU7 NVMe | 1 TB   | 4       | 208   | 0     | 0.57   |
| Silico... | Asgard AN2 250N... | 250 GB | 3       | 207   | 0     | 0.57   |
| Samsung   | SSD 960 EVO        | 500 GB | 138     | 221   | 19    | 0.57   |
| Seagate   | FireCuda 510 SS... | 2 TB   | 4       | 207   | 0     | 0.57   |
| Gigabyte  | GP-ASM2NE6200TTTD  | 2 TB   | 3       | 206   | 0     | 0.57   |
| XPG       | GAMMIX S11 Pro     | 1 TB   | 121     | 210   | 1     | 0.57   |
| Samsung   | MZVPW256HEGL-000H1 | 256 GB | 10      | 205   | 0     | 0.56   |
| Samsung   | SSD 960 EVO        | 1 TB   | 60      | 209   | 1     | 0.56   |
| Apacer    | AS2280P4           | 240 GB | 2       | 203   | 0     | 0.56   |
| ADATA     | SX8200PNP          | 2 TB   | 55      | 203   | 0     | 0.56   |
| Toshiba   | KXG6APNV2T04       | 2 TB   | 4       | 203   | 0     | 0.56   |
| HP        | SSD EX920          | 1 TB   | 13      | 201   | 0     | 0.55   |
| Micron    | 9300_MTFDHAL6T4TDR | 6.4 TB | 2       | 201   | 0     | 0.55   |
| Apacer    | Z280 120G          | 120 GB | 2       | 201   | 0     | 0.55   |
| Toshiba   | RC100              | 240 GB | 10      | 200   | 0     | 0.55   |
| WDC       | WDS500G3XHC-00SJG0 | 500 GB | 21      | 200   | 0     | 0.55   |
| Silico... | NVME SSD           | 512 GB | 8       | 199   | 0     | 0.55   |
| Samsung   | MZVPW128HEGM-00000 | 128 GB | 2       | 216   | 16    | 0.54   |
| Phison    | Viper M.2 VPN100   | 1 TB   | 24      | 198   | 0     | 0.54   |
| SSSTC     | CL1-4D256-D22      | 256 GB | 2       | 198   | 0     | 0.54   |
| Intel     | HBRPEKNX0202AH     | 512 GB | 53      | 197   | 0     | 0.54   |
| Intel     | SSDPEKKF256G8 NVMe | 256 GB | 12      | 196   | 0     | 0.54   |
| HP        | SSD EX900          | 250 GB | 22      | 250   | 97    | 0.54   |
| Silico... | Asgard AN512NVM... | 512 GB | 2       | 195   | 0     | 0.54   |
| KIOXIA    | KXG60ZNV512G NVMe  | 512 GB | 45      | 194   | 0     | 0.53   |
| Samsung   | MZVLW1T0HMLH-000L2 | 1 TB   | 7       | 193   | 0     | 0.53   |
| Gigaby... | GP-GSM2NE3128GNTD  | 128 GB | 3       | 193   | 0     | 0.53   |
| ADATA     | SX7000NP           | 256 GB | 3       | 193   | 0     | 0.53   |
| Mushkin   | MKNSSDPE2TB-D8     | 2 TB   | 14      | 192   | 0     | 0.53   |
| Samsung   | SM961 NVMe         | 1 TB   | 2       | 298   | 8     | 0.53   |
| Gigabyte  | GP-ASM2NE6100TTTD  | 1 TB   | 6       | 191   | 0     | 0.52   |
| Samsung   | MZVLW512HMJP-000L2 | 512 GB | 20      | 191   | 0     | 0.52   |
| Toshiba   | KBG40ZNS256G NVMe  | 256 GB | 20      | 191   | 0     | 0.52   |
| Seagate   | FireCuda 520 SS... | 500 GB | 22      | 190   | 0     | 0.52   |
| Toshiba   | THNSN5256GPU7 NVMe | 256 GB | 6       | 190   | 0     | 0.52   |
| Samsung   | KUS040202M-B000    | 512 GB | 4       | 190   | 0     | 0.52   |
| Intel     | H10 HBRPEKNX010... | 256 GB | 3       | 188   | 0     | 0.52   |
| PNY       | CS3030 250GB SSD   | 250 GB | 13      | 188   | 0     | 0.52   |
| Seagate   | FireCuda 510 SS... | 1 TB   | 3       | 188   | 0     | 0.52   |
| Samsung   | MZVPW256HEGL-00000 | 256 GB | 20      | 187   | 0     | 0.51   |
| Patriot   | P300               | 512 GB | 2       | 187   | 0     | 0.51   |
| SK hynix  | PC400 NVMe         | 512 GB | 3       | 187   | 0     | 0.51   |
| Reletech  | M.2 SSD            | 512 GB | 2       | 187   | 0     | 0.51   |
| Transcend | TS256GMTE220S      | 256 GB | 12      | 185   | 0     | 0.51   |
| SK hynix  | PC601 HFS512GD9... | 512 GB | 21      | 185   | 0     | 0.51   |
| Samsung   | MZFLV128HCGR-000MV | 128 GB | 16      | 185   | 0     | 0.51   |
| Toshiba   | THNSN0256GTYA      | 256 GB | 2       | 185   | 0     | 0.51   |
| Kingston  | SA2000M8500G       | 500 GB | 152     | 184   | 0     | 0.51   |
| Samsung   | PM981 NVMe         | 1 TB   | 12      | 182   | 0     | 0.50   |
| XrayDisk  | 512GB              | 512 GB | 3       | 181   | 0     | 0.50   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 23      | 181   | 0     | 0.50   |
| SK hynix  | PC601 NVMe         | 512 GB | 55      | 180   | 0     | 0.50   |
| Team      | TM8FP4001T         | 1 TB   | 7       | 202   | 434   | 0.49   |
| Gigabyte  | GP-GSM2NE3100TNTD  | 1 TB   | 9       | 180   | 0     | 0.49   |
| Kingston  | SA2000M8250G       | 250 GB | 113     | 180   | 0     | 0.49   |
| SK hynix  | PC601 HFS001TD9... | 1 TB   | 2       | 179   | 0     | 0.49   |
| Corsair   | Force MP510        | 480 GB | 39      | 179   | 0     | 0.49   |
| ADATA     | SX8200PNP          | 256 GB | 56      | 198   | 39    | 0.49   |
| Corsair   | Force MP510        | 240 GB | 52      | 178   | 0     | 0.49   |
| PNY       | CS3040 1TB SSD     | 1 TB   | 2       | 178   | 0     | 0.49   |
| ADATA     | SX8200PNP          | 512 GB | 121     | 178   | 0     | 0.49   |
| SK hynix  | PC611 NVMe         | 256 GB | 5       | 177   | 0     | 0.49   |
| WDC       | WDBRPG5000ANC-WRSN | 500 GB | 18      | 177   | 0     | 0.49   |
| Intel     | SSDPEKNW512G8      | 512 GB | 328     | 176   | 0     | 0.48   |
| Intel     | HBRPEKNX0101AHO    | 16 GB  | 19      | 176   | 0     | 0.48   |
| Seagate   | FireCuda 520 SS... | 2 TB   | 16      | 175   | 0     | 0.48   |
| Patriot   | Scorch M2          | 128 GB | 6       | 173   | 0     | 0.48   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 3       | 173   | 0     | 0.48   |
| Kingston  | SEDC1000BM8240G    | 240 GB | 3       | 173   | 0     | 0.47   |
| Lite-On   | CX2-8B512-Q11 NVMe | 512 GB | 5       | 172   | 0     | 0.47   |
| Toshiba   | KBG40ZNS128G NVMe  | 128 GB | 6       | 172   | 0     | 0.47   |
| Hikvision | HS-SSD-E1000 256G  | 256 GB | 4       | 171   | 0     | 0.47   |
| Kingston  | RBUSNS8154P3512GJ1 | 512 GB | 23      | 171   | 0     | 0.47   |
| Phison    | E12-512G-PHISON... | 512 GB | 4       | 171   | 0     | 0.47   |
| Intel     | HBRPEKNX0202ALO    | 32 GB  | 9       | 171   | 0     | 0.47   |
| Corsair   | MP600 PRO          | 1 TB   | 4       | 171   | 0     | 0.47   |
| KIOXIA    | KXG60ZNV1T02 NVMe  | 1 TB   | 54      | 169   | 0     | 0.46   |
| Seagate   | FireCuda 510 SS... | 500 GB | 5       | 169   | 0     | 0.46   |
| Phison    | Sabrent Rocket Q   | 1 TB   | 81      | 168   | 0     | 0.46   |
| OWC       | Aura N             | 960 GB | 2       | 168   | 0     | 0.46   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 5       | 176   | 2     | 0.46   |
| Toshiba   | KXG60ZNV256G NVMe  | 256 GB | 23      | 165   | 0     | 0.45   |
| Micron    | 7300_MTFDHBE3T8TDF | 3.8 TB | 25      | 164   | 0     | 0.45   |
| Lenovo    | LENSE20512GMSP3... | 512 GB | 13      | 168   | 1     | 0.45   |
| Plextor   | PX-256M8PeY        | 256 GB | 2       | 163   | 0     | 0.45   |
| PNY       | CS3030 2TB SSD     | 2 TB   | 23      | 163   | 0     | 0.45   |
| Toshiba   | RC500              | 250 GB | 2       | 163   | 0     | 0.45   |
| Mushkin   | MKNSSDPL500GB-D8   | 500 GB | 2       | 163   | 0     | 0.45   |
| Toshiba   | KBG30ZMV512G       | 512 GB | 24      | 163   | 0     | 0.45   |
| Toshiba   | RC100              | 120 GB | 2       | 162   | 0     | 0.45   |
| SK hynix  | PC611 NVMe         | 512 GB | 40      | 165   | 26    | 0.44   |
| Intel     | HBRPEKNX0101AO     | 16 GB  | 2       | 161   | 0     | 0.44   |
| Dell      | Ent NVMe v2 AGN... | 1.6 TB | 2       | 160   | 0     | 0.44   |
| WDC       | WDS500G3X0C-00SJG0 | 500 GB | 162     | 161   | 7     | 0.44   |
| PNY       | CS3030 1TB SSD     | 1 TB   | 15      | 159   | 0     | 0.44   |
| HP        | SSD EX900          | 500 GB | 15      | 211   | 6     | 0.44   |
| Hikvision | HS-SSD-E1000 128G  | 128 GB | 2       | 158   | 0     | 0.43   |
| Toshiba   | THNSN5256GPUK      | 256 GB | 2       | 157   | 0     | 0.43   |
| Dell      | Ent NVMe v2 AGN... | 1.9 TB | 3       | 157   | 0     | 0.43   |
| Toshiba   | KBG40ZPZ128G ME... | 128 GB | 4       | 156   | 0     | 0.43   |
| Samsung   | MZVLW128HEGR-000L1 | 128 GB | 6       | 156   | 0     | 0.43   |
| Samsung   | MZVLB256HAHQ-000H2 | 256 GB | 2       | 156   | 0     | 0.43   |
| Samsung   | MZFLW1T0HMLH-000MU | 1 TB   | 3       | 156   | 0     | 0.43   |
| SSSTC     | CL1-3D512-Q11 NVMe | 512 GB | 16      | 155   | 0     | 0.43   |
| Toshiba   | KBG30ZMV128G       | 128 GB | 7       | 192   | 145   | 0.43   |
| KIOXIA... | SSD                | 500 GB | 12      | 154   | 0     | 0.42   |
| KIOXIA    | KXG60PNV512G NVMe  | 512 GB | 3       | 153   | 0     | 0.42   |
| WDC       | WDS250G3X0C-00SJG0 | 250 GB | 26      | 152   | 0     | 0.42   |
| SK hynix  | PC601A NVMe        | 1 TB   | 4       | 152   | 0     | 0.42   |
| Phison    | PCIe SSD           | 2 TB   | 125     | 155   | 9     | 0.42   |
| Samsung   | MZVLW512HMJP-00000 | 512 GB | 22      | 153   | 1     | 0.42   |
| Samsung   | MZVKW512HMJP-000L7 | 512 GB | 21      | 151   | 0     | 0.42   |
| Samsung   | SSD 970 PRO        | 512 GB | 191     | 152   | 1     | 0.41   |
| Kingston  | SA2000M81000G      | 1 TB   | 177     | 153   | 18    | 0.41   |
| Phison    | PS5012-E12S-512G   | 512 GB | 2       | 151   | 0     | 0.41   |
| Gigabyte  | GP-GSM2NE8256GNTD  | 256 GB | 2       | 150   | 0     | 0.41   |
| Intel     | H10 HBRPEKNX020... | 1 TB   | 3       | 198   | 1     | 0.41   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 22      | 149   | 0     | 0.41   |
| Samsung   | MZVLV512HCJH-000H1 | 512 GB | 3       | 149   | 0     | 0.41   |
| Plextor   | PX-256M8PeG        | 256 GB | 3       | 225   | 335   | 0.41   |
| Lite-On   | CA3-8D512          | 512 GB | 9       | 148   | 0     | 0.41   |
| KIOXIA    | KXG60ZNV512G       | 512 GB | 32      | 147   | 0     | 0.40   |
| Samsung   | SSD 970 EVO        | 250 GB | 174     | 152   | 2     | 0.40   |
| Hikvision | HS-SSD-E2000 256G  | 256 GB | 3       | 147   | 0     | 0.40   |
| Plextor   | PX-512M8PeG        | 512 GB | 6       | 166   | 92    | 0.40   |
| Crucial   | CT2000P1SSD8       | 2 TB   | 3       | 146   | 0     | 0.40   |
| Intel     | SSDPEKNW010T9      | 1 TB   | 31      | 146   | 0     | 0.40   |
| WDC       | WDS100T2B0C-00PXH0 | 1 TB   | 227     | 146   | 0     | 0.40   |
| UMIS      | RPJTJ256MED1OWX    | 256 GB | 6       | 146   | 0     | 0.40   |
| Kingston  | SKC2500M81000G     | 1 TB   | 21      | 146   | 0     | 0.40   |
| Toshiba   | KXG60ZNV256G       | 256 GB | 27      | 146   | 0     | 0.40   |
| Gigaby... | GP-AG4500G         | 500 GB | 6       | 146   | 0     | 0.40   |
| Intel     | HBRPEKNX0101AH     | 256 GB | 18      | 146   | 0     | 0.40   |
| Intel     | HBRPEKNX0202AL     | 512 GB | 10      | 146   | 0     | 0.40   |
| Samsung   | MZVLW1T0HMLH-000L7 | 1 TB   | 13      | 150   | 2     | 0.40   |
| Samsung   | MZ1LB3T8HMLA-00007 | 3.8 TB | 3       | 144   | 0     | 0.40   |
| Gigabyte  | GP-GSM2NE3512GNTD  | 512 GB | 8       | 144   | 0     | 0.39   |
| Plextor   | PX-512M9PeY        | 512 GB | 5       | 143   | 0     | 0.39   |
| Intel     | SSDPEKNW512G8L     | 512 GB | 50      | 143   | 0     | 0.39   |
| Phison    | Sabrent Rocket 4.0 | 500 GB | 18      | 142   | 0     | 0.39   |
| Intel     | SSDPEBKF128G7      | 128 GB | 3       | 500   | 10    | 0.39   |
| Seagate   | BarraCuda Q5 ZP... | 1 TB   | 4       | 142   | 0     | 0.39   |
| Kingston  | RBUSNS8154P3512GJ5 | 512 GB | 7       | 141   | 0     | 0.39   |
| Silico... | NE-256             | 256 GB | 29      | 141   | 0     | 0.39   |
| SK hynix  | PC401 NVMe         | 256 GB | 21      | 144   | 2     | 0.39   |
| Toshiba   | KXG50PNV2T04       | 2 TB   | 3       | 140   | 0     | 0.38   |
| PNY       | CS2130 1TB SSD     | 1 TB   | 11      | 139   | 0     | 0.38   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 31      | 139   | 0     | 0.38   |
| Kingston  | OM8PCP31024F-AI1   | 1 TB   | 10      | 139   | 0     | 0.38   |
| Phison    | Sabrent Rocket Q4  | 1 TB   | 12      | 139   | 0     | 0.38   |
| Zheino    | CHN-NGFFNV2280-256 | 256 GB | 2       | 139   | 0     | 0.38   |
| Toshiba   | KBG30ZMV256G       | 256 GB | 54      | 138   | 0     | 0.38   |
| WDC       | WDS100T3X0C-00SJG0 | 1 TB   | 138     | 138   | 5     | 0.38   |
| MSI       | M390               | 1 TB   | 2       | 138   | 0     | 0.38   |
| Intel     | SSDPEKKW010T8      | 1 TB   | 9       | 137   | 0     | 0.38   |
| Kingston  | RBUSNS8154P3256GJ5 | 256 GB | 3       | 137   | 0     | 0.38   |
| KIOXIA    | KBG40ZPZ512G NVMe  | 512 GB | 16      | 136   | 0     | 0.38   |
| Toshiba   | KBG30ZMT512G       | 512 GB | 8       | 136   | 0     | 0.37   |
| HP        | SSD EX950          | 512 GB | 11      | 136   | 0     | 0.37   |
| Transcend | TS512GMTE110S      | 512 GB | 9       | 135   | 0     | 0.37   |
| Gigabyte  | GP-AG4500G         | 500 GB | 5       | 135   | 0     | 0.37   |
| Plextor   | PX-1TM8PeG         | 1 TB   | 2       | 134   | 0     | 0.37   |
| Lite-On   | CA3-8D256          | 256 GB | 13      | 134   | 0     | 0.37   |
| Phison    | Sabrent Rocket ... | 1 TB   | 13      | 134   | 0     | 0.37   |
| SK hynix  | PC401 HFS512GD9... | 512 GB | 2       | 134   | 0     | 0.37   |
| HP        | SSD EX950          | 2 TB   | 13      | 133   | 0     | 0.37   |
| Micron    | 2200V_MTFDHBA25... | 256 GB | 2       | 133   | 0     | 0.37   |
| Samsung   | MZVLW256HEHP-00000 | 256 GB | 68      | 134   | 1     | 0.37   |
| Samsung   | MZVLW1T0HMLH-00000 | 1 TB   | 7       | 132   | 0     | 0.36   |
| Samsung   | Portable SSD T7    | 1 TB   | 3       | 131   | 0     | 0.36   |
| Kingston  | SA1000M8480G       | 480 GB | 9       | 131   | 0     | 0.36   |
| SPCC      | M.2 PCIe SSD       | 256 GB | 48      | 131   | 43    | 0.36   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 23      | 130   | 0     | 0.36   |
| SK hynix  | PC611 NVMe         | 1 TB   | 44      | 130   | 0     | 0.36   |
| FORESEE   | P900F256GB         | 256 GB | 2       | 130   | 0     | 0.36   |
| Corsair   | MP600 CORE         | 1 TB   | 6       | 129   | 0     | 0.36   |
| Gigabyte  | GP-ASM2NE6500GTTD  | 500 GB | 5       | 129   | 0     | 0.35   |
| Plextor   | PX-1TM8PeY         | 1 TB   | 2       | 129   | 0     | 0.35   |
| Samsung   | SM961 NVMe         | 512 GB | 3       | 129   | 0     | 0.35   |
| SK hynix  | PC601 HFS256GD9... | 256 GB | 5       | 128   | 0     | 0.35   |
| Phison    | Viper M.2 VP4100   | 1 TB   | 7       | 128   | 0     | 0.35   |
| Samsung   | SSD 960 EVO        | 250 GB | 203     | 137   | 16    | 0.35   |
| Samsung   | SSD 970 PRO        | 1 TB   | 96      | 135   | 1     | 0.35   |
| Kingston  | OM8PCP3512F-AB     | 512 GB | 70      | 127   | 0     | 0.35   |
| Intel     | SSDPEKKF256G8L     | 256 GB | 69      | 128   | 15    | 0.35   |
| Intel     | SSDPE2KE020T7      | 2 TB   | 4       | 127   | 0     | 0.35   |
| WDC       | WDS250G2B0C-00PXH0 | 250 GB | 46      | 126   | 0     | 0.35   |
| Phison    | Sabrent Rocket ... | 1 TB   | 30      | 126   | 0     | 0.35   |
| KIOXIA    | KXG60PNV2T04       | 2 TB   | 7       | 125   | 0     | 0.34   |
| Corsair   | MP400              | 2 TB   | 9       | 125   | 0     | 0.34   |
| SPCC      | M.2 PCIE SSD       | 512 GB | 4       | 142   | 253   | 0.34   |
| Gigaby... | GP-AG41TB          | 1 TB   | 9       | 124   | 0     | 0.34   |
| Transcend | TS2TMTE220S        | 2 TB   | 4       | 124   | 0     | 0.34   |
| Seagate   | FireCuda 520 SS... | 1 TB   | 17      | 123   | 0     | 0.34   |
| Gigaby... | GP-AG42TB          | 2 TB   | 4       | 123   | 0     | 0.34   |
| SK hynix  | SHGP31-1000GM-2    | 1 TB   | 25      | 123   | 0     | 0.34   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 9       | 123   | 0     | 0.34   |
| WDC       | WD BLACK SDBPNT... | 1 TB   | 2       | 123   | 0     | 0.34   |
| Lite-On   | CA3-8D128-HP       | 128 GB | 4       | 122   | 0     | 0.34   |
| HP        | SSD EX920          | 256 GB | 2       | 230   | 1     | 0.33   |
| Phison    | BPXP               | 960 GB | 2       | 122   | 0     | 0.33   |
| KIOXIA    | KXG6AZNV512G       | 512 GB | 3       | 121   | 0     | 0.33   |
| SK hynix  | SHGP31-1000GM      | 1 TB   | 18      | 121   | 0     | 0.33   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 32      | 121   | 0     | 0.33   |
| Seagate   | BarraCuda 510 S... | 1 TB   | 5       | 120   | 0     | 0.33   |
| Silico... | NE-1TB             | 1 TB   | 12      | 120   | 0     | 0.33   |
| Samsung   | PM961 NVMe         | 1 TB   | 5       | 120   | 0     | 0.33   |
| Intel     | SSDPEKNW010T8H     | 1 TB   | 24      | 120   | 0     | 0.33   |
| Samsung   | SSD 960 PRO        | 2 TB   | 13      | 130   | 82    | 0.33   |
| Samsung   | MZVLW256HEHP-000L2 | 256 GB | 45      | 122   | 1     | 0.33   |
| KIOXIA    | KBG40ZPZ1T02 NVMe  | 1 TB   | 18      | 119   | 0     | 0.33   |
| Intel     | HBRPEKNX0203A      | 1 TB   | 3       | 119   | 0     | 0.33   |
| FORESEE   | P900F256GBH        | 256 GB | 2       | 118   | 0     | 0.33   |
| Seagate   | FireCuda 530 ZP... | 4 TB   | 4       | 118   | 0     | 0.33   |
| KIOXIA    | KBG30ZMV256G       | 256 GB | 28      | 119   | 36    | 0.32   |
| Gigabyte  | GP-AG41TB          | 1 TB   | 14      | 118   | 0     | 0.32   |
| SK hynix  | HFS256GD9TNG-L2A0A | 256 GB | 3       | 118   | 0     | 0.32   |
| WDC       | WDBA3V0010BNC-WRSN | 1 TB   | 6       | 118   | 0     | 0.32   |
| Micron    | 2200S NVMe         | 512 GB | 54      | 118   | 0     | 0.32   |
| Samsung   | MZVLW256HEHP-000H1 | 256 GB | 68      | 122   | 1     | 0.32   |
| Samsung   | MZVLW128HEGR-000H1 | 128 GB | 16      | 116   | 0     | 0.32   |
| Samsung   | PM961 NVMe         | 512 GB | 15      | 132   | 3     | 0.32   |
| Samsung   | PM981 NVMe         | 256 GB | 26      | 115   | 0     | 0.32   |
| Intel     | HBRPEKNX0203AO     | 32 GB  | 4       | 115   | 0     | 0.32   |
| ADATA     | SX8100NP           | 2 TB   | 4       | 335   | 254   | 0.32   |
| Corsair   | Force MP510        | 4 TB   | 3       | 115   | 0     | 0.32   |
| KIOXIA    | KBG40ZNS256G NVMe  | 256 GB | 102     | 114   | 0     | 0.31   |
| Intel     | SSDPEKKF010T8 NVMe | 1 TB   | 7       | 114   | 0     | 0.31   |
| Gigaby... | GP-ASM2NE2256GTTDR | 256 GB | 2       | 114   | 0     | 0.31   |
| KIOXIA    | KBG40ZNS512G NVMe  | 512 GB | 158     | 114   | 0     | 0.31   |
| SPCC      | M.2 PCIe SSD       | 2 TB   | 12      | 115   | 21    | 0.31   |
| Phison    | ESR01TBTLCG-EAC-4  | 1 TB   | 3       | 114   | 0     | 0.31   |
| Intel     | SSDPEMKF256G8 NVMe | 256 GB | 5       | 113   | 0     | 0.31   |
| Samsung   | MZVLW512HMJP-000L7 | 512 GB | 29      | 113   | 1     | 0.31   |
| KIOXIA    | KXG60ZNV1T02       | 1 TB   | 32      | 112   | 0     | 0.31   |
| SK hynix  | SHGP31-500GM-2     | 500 GB | 14      | 112   | 0     | 0.31   |
| KIOXIA    | KBG40ZNS128G NVMe  | 128 GB | 20      | 112   | 0     | 0.31   |
| Gigaby... | GP-ASM2NE6500GTTD  | 500 GB | 5       | 111   | 0     | 0.31   |
| Toshiba   | KBG30ZMS256G NVMe  | 256 GB | 30      | 111   | 0     | 0.31   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 17      | 110   | 0     | 0.30   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 90      | 110   | 12    | 0.30   |
| WDC       | WDS200T3X0C-00SJG0 | 2 TB   | 12      | 110   | 0     | 0.30   |
| HUAWEI    | HWE52P432T0L005N   | 2 TB   | 6       | 110   | 0     | 0.30   |
| Samsung   | MZVLB1T0HALR-00000 | 1 TB   | 49      | 133   | 1     | 0.30   |
| Phison    | SBXe               | 480 GB | 3       | 110   | 0     | 0.30   |
| SK hynix  | SKHynix_HFS001T... | 1 TB   | 3       | 109   | 0     | 0.30   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 41      | 109   | 0     | 0.30   |
| KIOXIA    | KXG6AZNV512G NV... | 512 GB | 9       | 109   | 0     | 0.30   |
| Toshiba   | KXG6AZNV1T02       | 1 TB   | 27      | 108   | 0     | 0.30   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 6       | 108   | 0     | 0.30   |
| Samsung   | MZVLW256HEHP-000L7 | 256 GB | 128     | 108   | 1     | 0.30   |
| Samsung   | MZVLB1T0HALR-000L7 | 1 TB   | 50      | 108   | 0     | 0.30   |
| Kingston  | SA1000M8240G       | 240 GB | 36      | 107   | 0     | 0.30   |
| Apacer    | AS2280P4           | 512 GB | 15      | 107   | 0     | 0.30   |
| ADATA     | SX8100NP           | 512 GB | 14      | 113   | 74    | 0.29   |
| Silico... | NE-512             | 512 GB | 19      | 107   | 0     | 0.29   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 19      | 107   | 0     | 0.29   |
| KIOXIA    | KBG40ZPZ256G NVMe  | 256 GB | 6       | 106   | 0     | 0.29   |
| Seagate   | FireCuda 530 ZP... | 4 TB   | 14      | 106   | 0     | 0.29   |
| WDC       | WDS500G2B0C-00PXH0 | 500 GB | 164     | 106   | 0     | 0.29   |
| Micron    | 7400_MTFDKBG3T8TDZ | 3.8 TB | 4       | 106   | 0     | 0.29   |

NVME by Vendor
--------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF |
|-------------|--------|---------|-------|-------|------|
| ZOTAC       | 1      | 2       | 919   | 0     | 2.52   |
| addlink     | 1      | 17      | 326   | 0     | 0.90   |
| KINGBANK    | 1      | 2       | 312   | 0     | 0.86   |
| Aura        | 1      | 5       | 287   | 0     | 0.79   |
| Corsair     | 22     | 343     | 256   | 1     | 0.70   |
| AMD         | 2      | 16      | 243   | 0     | 0.67   |
| Intel       | 94     | 2297    | 256   | 8     | 0.66   |
| Toshiba     | 85     | 1281    | 236   | 2     | 0.65   |
| Plextor     | 13     | 46      | 254   | 37    | 0.62   |
| LDLC        | 1      | 3       | 213   | 0     | 0.59   |
| HP          | 10     | 122     | 224   | 23    | 0.54   |
| Transcend   | 9      | 88      | 189   | 0     | 0.52   |
| Mushkin     | 5      | 33      | 192   | 33    | 0.51   |
| OWC         | 1      | 2       | 168   | 0     | 0.46   |
| SPCC        | 8      | 187     | 156   | 29    | 0.43   |
| T-FORCE     | 5      | 13      | 155   | 0     | 0.42   |
| Lexar       | 7      | 30      | 152   | 0     | 0.42   |
| Phison      | 53     | 856     | 152   | 2     | 0.41   |
| XPG         | 12     | 254     | 155   | 22    | 0.40   |
| J.ZAO       | 2      | 4       | 139   | 0     | 0.38   |
| Lenovo      | 5      | 79      | 146   | 3     | 0.38   |
| Goodram     | 7      | 36      | 137   | 1     | 0.38   |
| ADATA       | 53     | 786     | 140   | 17    | 0.37   |
| Lite-On     | 16     | 95      | 127   | 3     | 0.35   |
| Crucial     | 22     | 986     | 130   | 7     | 0.35   |
| Seagate     | 22     | 161     | 125   | 0     | 0.34   |
| Silicon ... | 33     | 241     | 123   | 1     | 0.34   |
| Gigabyte... | 12     | 81      | 123   | 0     | 0.34   |
| PNY         | 19     | 122     | 125   | 1     | 0.33   |
| Zheino      | 2      | 4       | 118   | 0     | 0.33   |
| Patriot     | 11     | 53      | 118   | 0     | 0.32   |
| Hikvision   | 10     | 27      | 117   | 0     | 0.32   |
| ZHITAI      | 5      | 11      | 103   | 0     | 0.28   |
| Gigabyte    | 16     | 98      | 101   | 12    | 0.28   |
| Reletech    | 2      | 6       | 98    | 0     | 0.27   |
| KIOXIA      | 45     | 980     | 97    | 2     | 0.27   |
| Kingston    | 68     | 1659    | 95    | 3     | 0.26   |
| Acer        | 1      | 3       | 91    | 0     | 0.25   |
| SMI         | 1      | 3       | 87    | 0     | 0.24   |
| Dell        | 4      | 11      | 87    | 0     | 0.24   |
| KIOXIA-E... | 6      | 53      | 85    | 0     | 0.23   |
| WDC         | 147    | 3918    | 83    | 1     | 0.23   |
| KLEVV       | 1      | 2       | 161   | 1     | 0.23   |
| HUAWEI      | 2      | 10      | 78    | 0     | 0.22   |
| Samsung     | 238    | 10918   | 78    | 2     | 0.21   |
| Apacer      | 7      | 67      | 77    | 5     | 0.21   |
| KLLISRE     | 2      | 6       | 73    | 0     | 0.20   |
| Team        | 10     | 67      | 76    | 76    | 0.20   |
| Smartbuy    | 3      | 8       | 69    | 0     | 0.19   |
| SK hynix    | 113    | 2438    | 64    | 2     | 0.17   |
| SSSTC       | 21     | 189     | 61    | 1     | 0.17   |
| XrayDisk    | 4      | 22      | 68    | 46    | 0.17   |
| VICKTER     | 1      | 3       | 60    | 0     | 0.17   |
| UMIS        | 16     | 231     | 58    | 1     | 0.16   |
| OSCOO       | 1      | 2       | 56    | 0     | 0.16   |
| MSI         | 3      | 6       | 56    | 0     | 0.15   |
| ORICO       | 1      | 3       | 44    | 0     | 0.12   |
| Netac       | 7      | 49      | 44    | 21    | 0.11   |
| SanDisk     | 57     | 638     | 40    | 0     | 0.11   |
| Micron      | 59     | 1092    | 40    | 1     | 0.11   |
| YMTC        | 4      | 46      | 38    | 1     | 0.10   |
| FORESEE     | 8      | 22      | 31    | 1     | 0.09   |
| KingFast    | 1      | 2       | 27    | 0     | 0.08   |
| Colorful    | 2      | 4       | 25    | 0     | 0.07   |
| Inland      | 1      | 3       | 26    | 23    | 0.07   |
| Apple       | 24     | 324     | 24    | 4     | 0.07   |
| Star Drive  | 1      | 14      | 22    | 0     | 0.06   |
| Intenso     | 1      | 3       | 21    | 0     | 0.06   |
| Union Me... | 7      | 67      | 21    | 0     | 0.06   |
| ShiJi       | 2      | 4       | 29    | 254   | 0.05   |
| Western ... | 1      | 2       | 18    | 0     | 0.05   |
| BIWIN       | 4      | 51      | 17    | 0     | 0.05   |
| Kimtigo     | 1      | 7       | 17    | 0     | 0.05   |
| Solid St... | 4      | 11      | 15    | 0     | 0.04   |
| OEM         | 1      | 3       | 14    | 0     | 0.04   |
| Timetec     | 1      | 4       | 12    | 0     | 0.03   |
| China       | 1      | 2       | 11    | 0     | 0.03   |
| Fanxiang    | 3      | 10      | 7     | 0     | 0.02   |
| WALRAM      | 3      | 8       | 6     | 0     | 0.02   |
| Foxline     | 1      | 18      | 4     | 0     | 0.01   |
| Kllisre     | 1      | 2       | 1     | 0     | 0.00   |
| AGI         | 1      | 4       | 1     | 0     | 0.00   |
| kllisre     | 1      | 2       | 0     | 0     | 0.00   |

