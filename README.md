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

Total drives: 231465.

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
| Hitachi   | HUA721075KLA330    | 752 GB | 3       | 3455  | 0     | 9.47   |
| HP        | GB0160EAFJE        | 160 GB | 2       | 3447  | 0     | 9.44   |
| WDC       | WD6400AAVS-00G9B0  | 640 GB | 2       | 3191  | 0     | 8.74   |
| WDC       | WD7500AAVS-00D7B0  | 752 GB | 2       | 3177  | 0     | 8.71   |
| Samsung   | HE160HJ            | 160 GB | 2       | 3097  | 0     | 8.49   |
| WDC       | WD5000AAKS-60A7B0  | 500 GB | 2       | 3047  | 0     | 8.35   |
| HGST      | HUP722020APA330    | 2 TB   | 2       | 2688  | 0     | 7.36   |
| Hitachi   | HUA7210SASUN1.0T   | 1 TB   | 12      | 2672  | 0     | 7.32   |
| Toshiba   | MB3000GDUPA        | 3 TB   | 4       | 2657  | 0     | 7.28   |
| HP        | GB0500EAFYL        | 500 GB | 2       | 3042  | 1     | 6.96   |
| Seagate   | ST6000NM0125-1Y... | 6 TB   | 2       | 2519  | 0     | 6.90   |
| Hitachi   | HDS722020ALA330... | 2 TB   | 3       | 2515  | 0     | 6.89   |
| WDC       | WD1000FYPS-01ZKB0  | 1 TB   | 3       | 2471  | 0     | 6.77   |
| Hitachi   | HDS7216SBSUN160G   | 160 GB | 2       | 4110  | 2     | 6.76   |
| HPE       | MB0500EBNCR        | 500 GB | 4       | 2641  | 229   | 6.70   |
| WDC       | WD1002FBYS-50A6B0  | 1 TB   | 2       | 2401  | 0     | 6.58   |
| Hitachi   | HUA722020ALA330... | 2 TB   | 2       | 2396  | 0     | 6.57   |
| Seagate   | ST3000VM002-1F316N | 3 TB   | 2       | 2381  | 0     | 6.53   |
| WDC       | WD2500AAJS-07VWA0  | 250 GB | 2       | 2354  | 0     | 6.45   |
| WDC       | WD1002FBYS-01A6B0  | 1 TB   | 13      | 3294  | 2     | 6.39   |
| WDC       | WD5000BUCT-63PUZY0 | 500 GB | 3       | 2330  | 0     | 6.39   |
| Seagate   | ST6000DM001-1XY17Z | 6 TB   | 10      | 2322  | 0     | 6.36   |
| Toshiba   | MK2002TSKB         | 2 TB   | 10      | 2313  | 2     | 6.34   |
| Hitachi   | HUA721050KLA330    | 500 GB | 7       | 2259  | 0     | 6.19   |
| WDC       | WD5000AAKS-40YGA1  | 500 GB | 2       | 2259  | 0     | 6.19   |
| WDC       | WD10EACS-00C7B0    | 1 TB   | 6       | 2207  | 0     | 6.05   |
| HGST      | MB6000GEBTP        | 6 TB   | 3       | 2206  | 0     | 6.04   |
| WDC       | WD15EARS-32MVWB0   | 1.5 TB | 4       | 2203  | 0     | 6.04   |
| WDC       | WD1001FALS-00K1B0  | 1 TB   | 2       | 2199  | 0     | 6.02   |
| Seagate   | ST4000DX000-1CL160 | 4 TB   | 2       | 2175  | 0     | 5.96   |
| WDC       | WD10EVDS-63N5B1    | 1 TB   | 6       | 2535  | 2     | 5.93   |
| WDC       | WD1003FBYX-50Y7B1  | 1 TB   | 3       | 2142  | 0     | 5.87   |
| WDC       | WD20EADS-32S2B0    | 2 TB   | 3       | 2484  | 4     | 5.81   |
| WDC       | WD1003FBYX-01Y7B2  | 1 TB   | 3       | 2660  | 1     | 5.81   |
| WDC       | WD5000ABYS-01TNA0  | 500 GB | 2       | 2117  | 0     | 5.80   |
| WDC       | WD3200AVJB-63J5A0  | 320 GB | 2       | 2113  | 0     | 5.79   |
| WDC       | WD2502ABYS-02B7A0  | 256 GB | 19      | 2703  | 5     | 5.78   |
| WDC       | WD3200KS-00PFB0    | 320 GB | 7       | 2294  | 14    | 5.76   |
| WDC       | WD3200AACS-00M6B0  | 320 GB | 2       | 2575  | 5     | 5.73   |
| WDC       | WD6400AAKS-40H2B0  | 640 GB | 11      | 2445  | 77    | 5.70   |
| WDC       | WD3000HLFS-01G6U1  | 304 GB | 2       | 2066  | 0     | 5.66   |
| Hitachi   | HUA722020ALA330    | 2 TB   | 33      | 2631  | 8     | 5.65   |
| Hitachi   | HUA723030ALA640... | 3 TB   | 2       | 2062  | 0     | 5.65   |
| WDC       | WD800JD-75MSA1     | 80 GB  | 2       | 2057  | 0     | 5.64   |
| WDC       | WD1002FBYS-05A6B0  | 1 TB   | 7       | 2497  | 1     | 5.63   |
| IBM/Hi... | IC35L120AVV207-0   | 128 GB | 2       | 2350  | 1     | 5.59   |
| WDC       | WD3000BLFS-01YBU0  | 304 GB | 6       | 2016  | 0     | 5.52   |
| HP        | GB0500C4413        | 500 GB | 2       | 2009  | 0     | 5.51   |
| Hitachi   | HDS724040ALE640    | 4 TB   | 16      | 2086  | 87    | 5.47   |
| Seagate   | ST5000NM0084-1H... | 5 TB   | 2       | 1991  | 0     | 5.46   |
| Seagate   | ST31000340NS EIT   | 1 TB   | 2       | 1989  | 0     | 5.45   |
| Hitachi   | HUA721010KLA330    | 1 TB   | 36      | 2446  | 56    | 5.43   |
| HP        | MB2000EAZNL        | 2 TB   | 3       | 1979  | 0     | 5.42   |
| WDC       | WD6401AALS-00E8B0  | 640 GB | 7       | 1975  | 0     | 5.41   |
| WDC       | WD5000AAKS-60A7B2  | 500 GB | 2       | 1957  | 0     | 5.36   |
| HP        | MB1000GCEEK        | 1 TB   | 2       | 1954  | 0     | 5.36   |
| WDC       | WD2500KS-22MJB0    | 250 GB | 2       | 1943  | 0     | 5.32   |
| WDC       | WD400BD-55MTA1     | 40 GB  | 2       | 1922  | 0     | 5.27   |
| WDC       | WD15EARS-19MVWB0   | 1.5 TB | 3       | 2145  | 436   | 5.24   |
| WDC       | WD5000AAKX-753CA0  | 500 GB | 4       | 1912  | 0     | 5.24   |
| WDC       | WD3000GLFS-01F8U0  | 304 GB | 10      | 2332  | 116   | 5.24   |
| WDC       | WD10EZEX-19M2NA0   | 1 TB   | 3       | 1911  | 0     | 5.24   |
| Seagate   | ST3160828AS        | 160 GB | 2       | 1874  | 0     | 5.14   |
| Seagate   | ST2000NX0423       | 2 TB   | 5       | 1853  | 0     | 5.08   |
| WDC       | WD80PUZX-64NEAY0   | 8 TB   | 4       | 1788  | 0     | 4.90   |
| WDC       | WD2500BMVV-11DCLS0 | 250 GB | 3       | 1781  | 0     | 4.88   |
| Hitachi   | HDS723030ALA640    | 3 TB   | 40      | 2093  | 41    | 4.88   |
| WDC       | WD1003FBYX-12      | 1 TB   | 2       | 1766  | 0     | 4.84   |
| Seagate   | ST32000645NS       | 2 TB   | 16      | 1998  | 6     | 4.83   |
| WDC       | WD2502ABYS-18B7A0  | 250 GB | 8       | 2339  | 2     | 4.81   |
| HP        | GB0250EAFYK        | 250 GB | 8       | 2521  | 284   | 4.81   |
| WDC       | WD5000BHTZ-04JCPV1 | 500 GB | 2       | 1751  | 0     | 4.80   |
| WDC       | WD30EURX-63T0FY0   | 3 TB   | 4       | 1953  | 3     | 4.77   |
| WDC       | WD8002FRYZ-01FF2B0 | 8 TB   | 2       | 1735  | 0     | 4.75   |
| Seagate   | ST32000646NS       | 2 TB   | 2       | 1727  | 0     | 4.73   |
| WDC       | WD2502ABYS-23B7... | 250 GB | 9       | 2050  | 2     | 4.72   |
| WDC       | WD2502ABYS-01B7A0  | 256 GB | 6       | 2126  | 1     | 4.71   |
| WDC       | WD1001FALS-41K1B0  | 1 TB   | 3       | 1715  | 0     | 4.70   |
| WDC       | WD400JB-00ENA0     | 40 GB  | 3       | 2383  | 6     | 4.69   |
| WDC       | WD20NPVX-00EA4T0   | 2 TB   | 33      | 1880  | 2     | 4.69   |
| WDC       | WD5000AVVS-63ZWB0  | 500 GB | 6       | 2377  | 8     | 4.65   |
| WDC       | WD5000AAKS-75A7B2  | 500 GB | 9       | 1976  | 3     | 4.63   |
| HGST      | HUS726060ALE610    | 6 TB   | 37      | 1819  | 6     | 4.62   |
| Samsung   | SP0411N            | 40 GB  | 2       | 3755  | 9     | 4.62   |
| Seagate   | ST9500320AS        | 500 GB | 2       | 1684  | 0     | 4.62   |
| HGST      | HDN728080ALE604    | 8 TB   | 8       | 1678  | 0     | 4.60   |
| WDC       | WD1601ABYS-18C0A0  | 160 GB | 3       | 2303  | 4     | 4.60   |
| WDC       | WD5002ABYS-18B1B0  | 500 GB | 2       | 2862  | 4     | 4.59   |
| WDC       | WD30EURS-63SPKY0   | 3 TB   | 7       | 1659  | 0     | 4.55   |
| HGST      | HUS724020ALE640    | 2 TB   | 13      | 1657  | 0     | 4.54   |
| WDC       | WD2500YS-01SHB0    | 256 GB | 5       | 1693  | 6     | 4.50   |
| WDC       | WD1002FBYS-02A6B0  | 1 TB   | 29      | 2103  | 23    | 4.50   |
| Seagate   | ST4000VN000-1H4168 | 4 TB   | 40      | 1781  | 51    | 4.49   |
| WDC       | WD10EACS-32ZJB0    | 1 TB   | 5       | 2396  | 5     | 4.49   |
| WDC       | WD1001FALS-00Y6A0  | 1 TB   | 15      | 1703  | 32    | 4.49   |
| HGST      | HDN724030ALE640    | 3 TB   | 30      | 1727  | 4     | 4.48   |
| Seagate   | ST4000NM0024-1H... | 4 TB   | 7       | 1632  | 0     | 4.47   |
| WDC       | WD30EFRX-68AX9N0   | 3 TB   | 86      | 2030  | 2     | 4.47   |
| Hitachi   | HUA723020ALA640    | 2 TB   | 50      | 1799  | 1     | 4.46   |
| Samsung   | HE103UJ            | 1 TB   | 4       | 2284  | 1     | 4.46   |
| WDC       | WD1001FALS-41Y6A1  | 1 TB   | 10      | 1811  | 5     | 4.45   |
| WDC       | WD2500AAJS-62B4A0  | 250 GB | 2       | 1624  | 0     | 4.45   |
| WDC       | WD5000AAKS-07A7B2  | 500 GB | 3       | 2164  | 7     | 4.45   |
| Hitachi   | HUA721010KLA330... | 1 TB   | 2       | 1886  | 3     | 4.43   |
| WDC       | WD3000F9YZ-09N20L1 | 3 TB   | 7       | 1830  | 1     | 4.38   |
| HGST      | HUS724020ALA640    | 2 TB   | 68      | 1658  | 7     | 4.38   |
| WDC       | WD5000AUDX-57WNHY0 | 500 GB | 2       | 1594  | 0     | 4.37   |
| WDC       | WD10EAVS-32D7B1    | 1 TB   | 7       | 2115  | 56    | 4.32   |
| WDC       | WD3000HLFS-01G6U4  | 304 GB | 5       | 1570  | 0     | 4.30   |
| WDC       | WD1003FBYX-88 LEN  | 1 TB   | 4       | 1743  | 1     | 4.27   |
| Seagate   | ST3400820AS        | 400 GB | 4       | 1957  | 252   | 4.27   |
| WDC       | WD5002ABYS-02B1B0  | 500 GB | 34      | 2237  | 10    | 4.25   |
| Toshiba   | MC04ACA200E        | 2 TB   | 2       | 1548  | 0     | 4.24   |
| WDC       | WD5000LUCT-63Y8HY0 | 500 GB | 3       | 1547  | 0     | 4.24   |
| WDC       | WD20EADS-42R6B0    | 2 TB   | 2       | 1547  | 0     | 4.24   |
| Hitachi   | HDT721075SLA360    | 752 GB | 3       | 1538  | 0     | 4.22   |
| WDC       | WD101KFBX-68R56N0  | 10 TB  | 14      | 1530  | 0     | 4.19   |
| Seagate   | ST1000NC000-1CX162 | 1 TB   | 4       | 2282  | 223   | 4.18   |
| WDC       | WD2502ABYS-23B7... | 250 GB | 2       | 1522  | 0     | 4.17   |
| Samsung   | HE253GJ            | 250 GB | 3       | 2214  | 1     | 4.17   |
| HGST      | HUS724030ALA640    | 3 TB   | 35      | 1590  | 2     | 4.16   |
| WDC       | WD2500YD-01NVB1    | 256 GB | 4       | 1798  | 2     | 4.15   |
| Hitachi   | HDS723020BLA642    | 2 TB   | 102     | 1706  | 60    | 4.12   |
| HGST      | HDN726060ALE610    | 6 TB   | 29      | 1812  | 30    | 4.12   |
| WDC       | WD2500AAJS-22VWA0  | 250 GB | 3       | 1496  | 0     | 4.10   |
| WDC       | WD80EFAX-68LHPN0   | 8 TB   | 50      | 1486  | 0     | 4.07   |
| WDC       | WD15NPVT-00Z2TT0   | 1.5 TB | 4       | 2133  | 19    | 4.06   |
| WDC       | WD2500SD-01KCB0    | 250 GB | 3       | 1973  | 49    | 4.05   |
| HP        | FB080C4080         | 80 GB  | 2       | 1472  | 0     | 4.04   |
| WDC       | WD1200JB-00REA0    | 120 GB | 2       | 1515  | 1     | 4.03   |
| WDC       | WD3200AAJS-22RYA0  | 320 GB | 7       | 1493  | 1     | 4.01   |
| Seagate   | ST3400620NS        | 400 GB | 7       | 1959  | 6     | 4.00   |
| Seagate   | ST3000DM003-2AE16L | 3 TB   | 2       | 1450  | 0     | 3.97   |
| Seagate   | ST6000NM0024       | 6 TB   | 5       | 1447  | 0     | 3.97   |
| WDC       | WD2500AAKS-61L9A0  | 250 GB | 4       | 1439  | 0     | 3.94   |
| WDC       | WD1200JS-00SGB0    | 120 GB | 3       | 1437  | 0     | 3.94   |
| WDC       | WD1001FALS-00J7B0  | 1 TB   | 54      | 2039  | 3     | 3.94   |
| HGST      | HUH728080ALE604    | 8 TB   | 21      | 1685  | 7     | 3.93   |
| Seagate   | ST340212AS         | 40 GB  | 6       | 1654  | 35    | 3.92   |
| WDC       | WD20EARS-42S0XB0   | 2 TB   | 4       | 1426  | 0     | 3.91   |
| Hitachi   | HUA722010ALA330    | 1 TB   | 8       | 1774  | 17    | 3.88   |
| WDC       | WD7500BMVW-11AJGS2 | 752 GB | 3       | 1521  | 1     | 3.88   |
| Seagate   | ST320LT014-9YK142  | 320 GB | 3       | 1414  | 0     | 3.88   |
| WDC       | WD2500BMVU-11A04S0 | 250 GB | 2       | 1412  | 0     | 3.87   |
| WDC       | WD1600JS-75NCB3    | 160 GB | 7       | 1834  | 2     | 3.86   |
| Seagate   | ST3320820AS_P      | 320 GB | 2       | 1408  | 0     | 3.86   |
| WDC       | WD1500HLFS-01G6U3  | 150 GB | 2       | 1407  | 0     | 3.86   |
| Seagate   | ST2000NX0253       | 2 TB   | 27      | 1406  | 0     | 3.85   |
| Samsung   | SP1624N            | 160 GB | 3       | 1402  | 0     | 3.84   |
| WDC       | WD30EURS-63R8UY0   | 3 TB   | 6       | 1933  | 2     | 3.83   |
| WDC       | WD1002FBYS-18W8B0  | 1 TB   | 7       | 1645  | 1     | 3.83   |
| WDC       | WD1600YS-01SHB1    | 164 GB | 9       | 1396  | 0     | 3.83   |
| WDC       | WD40EZRX-22SPEB0   | 4 TB   | 6       | 1903  | 3     | 3.81   |
| HGST      | HUS728T8TALE600    | 8 TB   | 18      | 1387  | 0     | 3.80   |
| WDC       | WD10EVDS-63U8B1    | 1 TB   | 3       | 1386  | 0     | 3.80   |
| WDC       | WD740ADFD-00NLR1   | 74 GB  | 2       | 1386  | 0     | 3.80   |
| HGST      | HDN724040ALE640    | 4 TB   | 53      | 1426  | 39    | 3.79   |
| WDC       | WD8001FFWX-68J1UN0 | 8 TB   | 14      | 1380  | 0     | 3.78   |
| WDC       | WD2500AAJS-00VWA0  | 250 GB | 3       | 1379  | 0     | 3.78   |
| Seagate   | ST3000NM0033-9Z... | 3 TB   | 15      | 1435  | 2     | 3.78   |
| WDC       | WD20EARS-07MVWB0   | 2 TB   | 5       | 1779  | 1     | 3.75   |
| WDC       | WD10EACS-00D6B0    | 1 TB   | 26      | 1830  | 85    | 3.75   |
| Seagate   | MB3000EBKAB        | 3 TB   | 3       | 1366  | 0     | 3.74   |
| WDC       | WD1500HLFS-50G6U1  | 150 GB | 2       | 1364  | 0     | 3.74   |
| WDC       | WD1500HLFS-01G6U0  | 150 GB | 7       | 1954  | 88    | 3.74   |
| WDC       | WD3200AAJB-00WGA0  | 320 GB | 5       | 1363  | 0     | 3.74   |
| Hitachi   | HCC545025B9A300    | 250 GB | 3       | 1359  | 0     | 3.72   |
| WDC       | WD1600JS-98MHB0    | 160 GB | 2       | 1358  | 0     | 3.72   |
| WDC       | WD10EACS-00D6B1    | 1 TB   | 13      | 2457  | 152   | 3.72   |
| WDC       | WD800HLFS-75G6U1   | 80 GB  | 3       | 1354  | 0     | 3.71   |
| WDC       | WD5000AAVS-00G9B1  | 500 GB | 5       | 1403  | 204   | 3.70   |
| HP        | MB2000GCWDA        | 2 TB   | 9       | 1590  | 1     | 3.70   |
| WDC       | WD20EARX-008FB0    | 2 TB   | 29      | 1584  | 6     | 3.70   |
| WDC       | WD6401AALS-00J7B0  | 640 GB | 4       | 1845  | 157   | 3.69   |
| HGST      | HUS726020ALE610    | 2 TB   | 2       | 1345  | 0     | 3.69   |
| HGST      | HUS726060ALE614    | 6 TB   | 17      | 1359  | 34    | 3.68   |
| HGST      | HDS5C4040ALE630    | 4 TB   | 5       | 1342  | 0     | 3.68   |
| WDC       | WD3200JS-55PDB0    | 320 GB | 2       | 1342  | 0     | 3.68   |
| HGST      | HUS726060ALA640    | 6 TB   | 4       | 1896  | 1     | 3.68   |
| WDC       | WD10EADS-67M2B0    | 1 TB   | 3       | 1747  | 9     | 3.67   |
| Seagate   | ST2000NC000-1CX164 | 2 TB   | 2       | 2643  | 187   | 3.65   |
| WDC       | WD5001ABYS-01YNA0  | 500 GB | 4       | 1332  | 0     | 3.65   |
| Hitachi   | HDS721025CLA682    | 250 GB | 7       | 1332  | 0     | 3.65   |
| Seagate   | ST3320620NS        | 320 GB | 7       | 2460  | 146   | 3.64   |
| WDC       | WD10TMVV-11A27S2   | 1 TB   | 2       | 1342  | 7     | 3.63   |
| WDC       | WD1600YS-18SHB2    | 160 GB | 2       | 2714  | 5     | 3.63   |
| WDC       | WD7501AALS-00E8B0  | 752 GB | 5       | 1832  | 4     | 3.63   |
| WDC       | WD5000AAJS-00TKA0  | 500 GB | 7       | 1323  | 0     | 3.63   |
| WDC       | WD10EACS-00ZJB0    | 1 TB   | 18      | 1578  | 38    | 3.63   |
| HGST      | HUH721212ALE601    | 12 TB  | 21      | 1322  | 0     | 3.62   |
| WDC       | WD5000KS-00MNB0    | 500 GB | 3       | 1321  | 0     | 3.62   |
| WDC       | WD20EARX-22PASB0   | 2 TB   | 12      | 1690  | 1     | 3.62   |
| Toshiba   | MK3255GSXF         | 320 GB | 3       | 1442  | 1     | 3.61   |
| Seagate   | ST3000NM0053       | 3 TB   | 2       | 1892  | 1     | 3.61   |
| Seagate   | ST6000NM0024-1H... | 6 TB   | 22      | 1750  | 10    | 3.61   |
| WDC       | WD360GD-00FNA0     | 37 GB  | 5       | 2117  | 1     | 3.60   |
| Fujitsu   | MPE3064AT          | 6 GB   | 2       | 1315  | 0     | 3.60   |
| WDC       | WD1600JD-00HBC0    | 160 GB | 3       | 1534  | 2     | 3.60   |
| Seagate   | ST4000VX000-1F4168 | 4 TB   | 4       | 1591  | 2     | 3.60   |
| WDC       | WD2003FYYS-02W0B1  | 2 TB   | 36      | 1671  | 7     | 3.60   |
| Hitachi   | HDS722516VLSA80    | 164 GB | 4       | 1529  | 2     | 3.60   |
| WDC       | WD30EURS-73TLHY0   | 3 TB   | 3       | 1311  | 0     | 3.59   |
| WDC       | WD2500AAKX-08ERMA0 | 250 GB | 2       | 1311  | 0     | 3.59   |
| WDC       | WD7500AYYS-01RCA0  | 752 GB | 7       | 1364  | 1     | 3.59   |
| Seagate   | ST4000VM000-1F3168 | 4 TB   | 7       | 1304  | 0     | 3.57   |
| Hitachi   | HDS722020ALA330    | 2 TB   | 77      | 1969  | 98    | 3.57   |
| Seagate   | ST2000VM002-9UY166 | 2 TB   | 4       | 2223  | 94    | 3.57   |
| WDC       | WD1001FALS-40U9B0  | 1 TB   | 6       | 1412  | 1     | 3.56   |
| WDC       | WD10EADS-65M2B0    | 1 TB   | 23      | 1678  | 95    | 3.55   |
| Toshiba   | HDWA130            | 3 TB   | 8       | 1295  | 0     | 3.55   |
| HP        | MB1000EAMZE        | 1 TB   | 4       | 2174  | 519   | 3.55   |
| WDC       | WD5000AAJS-08A8B0  | 500 GB | 3       | 1513  | 1     | 3.53   |
| WDC       | WD5003ABYX-18WERA0 | 500 GB | 26      | 1758  | 43    | 3.53   |
| WDC       | WD3000HLFS-75G6U1  | 304 GB | 9       | 1374  | 1     | 3.53   |
| WDC       | WD3000HLFS-01G6U0  | 304 GB | 5       | 1286  | 0     | 3.53   |
| WDC       | WD740GD-00FLA1     | 74 GB  | 2       | 2935  | 20    | 3.52   |
| WDC       | WD6400AAKS-41H2B0  | 640 GB | 3       | 1277  | 0     | 3.50   |
| WDC       | WD2001FASS-00W2B0  | 2 TB   | 7       | 1802  | 2     | 3.50   |
| WDC       | WD1001FALS-00U9B0  | 1 TB   | 4       | 2201  | 124   | 3.50   |
| HGST      | HUS724040ALA640    | 4 TB   | 52      | 1403  | 79    | 3.49   |
| WDC       | WD5000BTKT-40MD3T0 | 500 GB | 3       | 2051  | 1     | 3.49   |
| Seagate   | ST2000DL004 HD2... | 2 TB   | 9       | 1319  | 1     | 3.48   |
| Seagate   | ST5000DM003-2FH18L | 5 TB   | 3       | 1269  | 0     | 3.48   |
| WDC       | WD2003FYYS-18W0B0  | 2 TB   | 13      | 1955  | 131   | 3.48   |
| WDC       | WD15EARS-22Z5B1    | 1.5 TB | 5       | 1263  | 0     | 3.46   |
| Hitachi   | HDS723020BLE640    | 2 TB   | 12      | 1263  | 0     | 3.46   |
| Toshiba   | MG03ACA200         | 2 TB   | 9       | 1540  | 48    | 3.44   |
| WDC       | WD2003FYPS-27Y2B0  | 2 TB   | 10      | 1500  | 11    | 3.43   |
| WDC       | WD1500HLFS-01G6U1  | 150 GB | 7       | 1253  | 0     | 3.43   |
| Hitachi   | HTS421212H9AT00    | 120 GB | 2       | 2184  | 120   | 3.43   |
| HPE       | MB4000GEFNA        | 4 TB   | 2       | 2358  | 8     | 3.42   |
| Hitachi   | HDS5C3015ALA632    | 1.5 TB | 4       | 1382  | 80    | 3.42   |
| WDC       | WD3200AAKS-22SBA0  | 320 GB | 4       | 1244  | 0     | 3.41   |
| WDC       | WD10EZEX-75ZF5A0   | 1 TB   | 35      | 1315  | 69    | 3.40   |
| WDC       | WD2003FYYS-02W0B0  | 2 TB   | 24      | 1909  | 15    | 3.37   |
| Seagate   | ST3000DM001-1E6166 | 3 TB   | 10      | 1380  | 400   | 3.37   |
| Seagate   | ST14000NM0138-2... | 14 TB  | 17      | 1550  | 4     | 3.36   |
| HGST      | HMS5C4040ALE640    | 4 TB   | 9       | 1222  | 0     | 3.35   |
| Seagate   | ST4000VN0001-1S... | 4 TB   | 5       | 1518  | 90    | 3.35   |
| WDC       | WD3000BLFS-60YBU2  | 304 GB | 7       | 2494  | 3     | 3.34   |
| HGST      | HUH728080ALN600    | 8 TB   | 7       | 1218  | 0     | 3.34   |
| Seagate   | ST4000NM0085-1Y... | 4 TB   | 3       | 1214  | 0     | 3.33   |
| Seagate   | ST310211A          | 10 GB  | 2       | 1214  | 0     | 3.33   |
| Hitachi   | HDS5C3020ALA632    | 2 TB   | 41      | 1591  | 16    | 3.32   |
| Samsung   | HD204UI            | 2 TB   | 119     | 1420  | 61    | 3.32   |
| WDC       | WD7501AALS-00J7B1  | 752 GB | 12      | 1353  | 1     | 3.31   |
| WDC       | WD10JPVT-16A1YT0   | 1 TB   | 4       | 1206  | 0     | 3.31   |
| WDC       | WD20EURS-73TLHY0   | 2 TB   | 3       | 1563  | 1     | 3.30   |
| Toshiba   | DT01ABA100         | 1 TB   | 2       | 1201  | 0     | 3.29   |
| WDC       | WD5000AAVS-00ZTB0  | 500 GB | 34      | 1413  | 48    | 3.29   |
| WDC       | WD40NMZW-34GX6S1   | 4 TB   | 2       | 1199  | 0     | 3.29   |
| Seagate   | ST3500630NS        | 500 GB | 25      | 1615  | 232   | 3.28   |
| Hitachi   | HUS724030ALA640    | 3 TB   | 4       | 1534  | 1     | 3.28   |
| WDC       | WD1003FBYX-18Y7B0  | 1 TB   | 9       | 1580  | 4     | 3.27   |
| WDC       | WD3000FYYZ-01UL1B0 | 3 TB   | 5       | 1742  | 2     | 3.27   |
| WDC       | WD2500AAJS-61B4A0  | 250 GB | 2       | 1191  | 0     | 3.27   |
| Samsung   | HD502HM            | 500 GB | 2       | 1993  | 1     | 3.26   |
| WDC       | WD6002FFWX-68TZ4N0 | 6 TB   | 7       | 1188  | 0     | 3.26   |
| Seagate   | ST8000AS0002-1N... | 8 TB   | 134     | 1360  | 49    | 3.25   |
| WDC       | WD1000DHTZ-04N21V1 | 1 TB   | 4       | 1336  | 1     | 3.25   |
| Hitachi   | HDS722525VLSA80    | 250 GB | 6       | 1261  | 6     | 3.25   |
| Hitachi   | HDS5C3030ALA630    | 3 TB   | 14      | 1514  | 2     | 3.23   |
| Hitachi   | HDS5C3020BLE630    | 2 TB   | 19      | 1433  | 73    | 3.23   |
| HGST      | HUS726020ALE614    | 2 TB   | 6       | 1179  | 0     | 3.23   |
| Hitachi   | HDS725050KLA360    | 500 GB | 18      | 2204  | 27    | 3.23   |
| Fujitsu   | MHZ2080BH G2       | 80 GB  | 2       | 1178  | 0     | 3.23   |
| WDC       | WD1600AABS-56PRA0  | 160 GB | 3       | 1178  | 0     | 3.23   |
| Hitachi   | HDS728040PLA320    | 40 GB  | 4       | 1548  | 4     | 3.22   |
| WDC       | WD7500AALX-009BA0  | 752 GB | 10      | 1176  | 0     | 3.22   |
| WDC       | WD1600AAJS-61WAA0  | 160 GB | 5       | 1176  | 0     | 3.22   |
| WDC       | WD2500JD-40HBC0    | 250 GB | 2       | 1945  | 3     | 3.22   |
| HGST      | HUS726020ALA610    | 2 TB   | 18      | 1294  | 8     | 3.21   |
| WDC       | WD3200AAJB-56WGA0  | 320 GB | 3       | 1172  | 0     | 3.21   |
| WDC       | WD800BB-60JKC0     | 80 GB  | 2       | 1292  | 2     | 3.21   |
| Maxtor    | 6N040T0            | 40 GB  | 2       | 1842  | 1     | 3.21   |
| HP        | MB2000EBUCF        | 2 TB   | 3       | 2111  | 4     | 3.21   |
| WDC       | WD5000AAVS-00G9B0  | 500 GB | 8       | 1332  | 1     | 3.21   |
| Maxtor    | 7H500F0            | 500 GB | 9       | 1208  | 1     | 3.20   |
| HPE       | MM1000GBKAL        | 1 TB   | 13      | 1995  | 5     | 3.20   |
| WDC       | WD1002FBYS-18A6B0  | 1 TB   | 7       | 1763  | 9     | 3.19   |
| Hitachi   | HUA723030ALA641    | 3 TB   | 19      | 1236  | 2     | 3.18   |
| WDC       | WD1600JS-75NCB2    | 160 GB | 2       | 1161  | 0     | 3.18   |
| Seagate   | ST9250610NS        | 250 GB | 7       | 1159  | 0     | 3.18   |
| WDC       | WD6000HLHX-75JJPV0 | 600 GB | 4       | 1936  | 3     | 3.18   |
| WDC       | WD10EADS-00L5B1    | 1 TB   | 124     | 1636  | 30    | 3.14   |
| WDC       | WD80PURZ-85YNPY0   | 8 TB   | 2       | 1145  | 0     | 3.14   |
| WDC       | WD10EAVS-22D7B0    | 1 TB   | 4       | 1775  | 4     | 3.13   |
| WDC       | WD80EFZX-68UW8N0   | 8 TB   | 41      | 1177  | 2     | 3.13   |
| WDC       | WD2500JS-00MHB0    | 250 GB | 6       | 1191  | 1     | 3.12   |
| WDC       | WD7500AACS-00D6B0  | 752 GB | 3       | 1244  | 3     | 3.12   |
| WDC       | WD5003AZEX-00RKKA0 | 500 GB | 2       | 1135  | 0     | 3.11   |
| WDC       | WD2500JS-41SGB0    | 250 GB | 2       | 1132  | 0     | 3.10   |
| Seagate   | ST3000VX006-1HH166 | 3 TB   | 3       | 1146  | 380   | 3.09   |
| WDC       | WD10EZEX-07ZF5A0   | 1 TB   | 5       | 1371  | 3     | 3.09   |
| Seagate   | ST6000NM0115-1Y... | 6 TB   | 114     | 1260  | 19    | 3.08   |
| WDC       | WD10EALX-759BA0    | 1 TB   | 5       | 1466  | 2     | 3.08   |
| WDC       | WD2000FYYZ-01UL1B0 | 2 TB   | 7       | 1278  | 1     | 3.08   |
| Hitachi   | HDT725040VLA360    | 400 GB | 8       | 1526  | 42    | 3.08   |
| WDC       | WD10TMVW-11ZSMS5   | 1 TB   | 30      | 1308  | 131   | 3.07   |
| WDC       | WD3200AAKS-00G3A0  | 320 GB | 7       | 1120  | 0     | 3.07   |
| Hitachi   | HDS721010CLA630    | 1 TB   | 26      | 1443  | 119   | 3.07   |
| WDC       | WD3000F9YZ-09N20L0 | 3 TB   | 9       | 1751  | 2     | 3.07   |
| WDC       | WD2002FAEX-007BA0  | 2 TB   | 93      | 1560  | 20    | 3.06   |
| Seagate   | ST6000AS0002-1N... | 6 TB   | 14      | 1523  | 57    | 3.06   |
| WDC       | WD2500JS-40MVB1    | 250 GB | 2       | 1115  | 0     | 3.06   |
| Toshiba   | MG03ACA400         | 4 TB   | 12      | 1276  | 1     | 3.06   |
| WDC       | WD1600AAJS-08WAA0  | 160 GB | 4       | 1256  | 1     | 3.05   |
| WDC       | WD3000HLFS-01G6U3  | 304 GB | 2       | 1113  | 0     | 3.05   |
| WDC       | WD1002FBYS-18W8B1  | 1 TB   | 3       | 1538  | 2     | 3.05   |
| Toshiba   | MG03ACA300         | 3 TB   | 9       | 1429  | 6     | 3.04   |
| WDC       | WD5001FZWX-00ZHUA0 | 5 TB   | 7       | 1587  | 18    | 3.04   |
| WDC       | WD1002FAEX-00Y9A0  | 1 TB   | 104     | 1333  | 9     | 3.04   |
| Seagate   | ST8000VN0002-1Z... | 8 TB   | 6       | 1719  | 78    | 3.04   |
| Seagate   | ST2000NC001-1DY164 | 2 TB   | 15      | 1448  | 33    | 3.04   |
| WDC       | WD800JD-55MSA1     | 80 GB  | 5       | 1109  | 0     | 3.04   |
| Seagate   | ST32000641AS       | 2 TB   | 42      | 1604  | 132   | 3.03   |
| Seagate   | ST500DM002-1ER14C  | 500 GB | 7       | 1106  | 0     | 3.03   |
| Seagate   | ST3000NC002-1DY166 | 3 TB   | 6       | 1353  | 498   | 3.02   |
| HGST      | HMS5C4040BLE640    | 4 TB   | 19      | 1102  | 0     | 3.02   |
| WDC       | WUH721414ALE604    | 14 TB  | 29      | 1099  | 1     | 3.01   |
| Hitachi   | HUA723030ALA640    | 3 TB   | 48      | 1358  | 49    | 3.01   |
| WDC       | WD10EAVS-00D7B0    | 1 TB   | 26      | 1573  | 6     | 3.01   |
| Seagate   | ST3000VN000-1HJ166 | 3 TB   | 23      | 1096  | 0     | 3.00   |
| Seagate   | ST2000VN000-1HJ164 | 2 TB   | 17      | 1208  | 179   | 3.00   |
| WDC       | WD1001FALS-00J7B1  | 1 TB   | 51      | 1637  | 24    | 3.00   |
| WDC       | WD3200KS-75PFB0    | 320 GB | 2       | 1365  | 39    | 3.00   |
| WDC       | WD4NPURX-64TPFY0   | 4 TB   | 2       | 1090  | 0     | 2.99   |
| WDC       | WD1001FALS-41Y6A0  | 1 TB   | 5       | 1202  | 1     | 2.99   |
| Seagate   | ST1000NM0008-2F... | 1 TB   | 29      | 1088  | 0     | 2.98   |
| WDC       | WD1200JD-00HBB0    | 120 GB | 11      | 1699  | 122   | 2.97   |
| Hitachi   | HDT722520DLAT80    | 200 GB | 4       | 1084  | 0     | 2.97   |
| WDC       | WD3003FZEX-00Z4SA0 | 3 TB   | 19      | 1171  | 54    | 2.97   |
| Toshiba   | MG04ACA100N        | 1 TB   | 8       | 1306  | 1     | 2.96   |
| Toshiba   | MD03ACA300V        | 3 TB   | 2       | 1080  | 0     | 2.96   |
| Toshiba   | MQ03ABB200         | 2 TB   | 2       | 1079  | 0     | 2.96   |
| Hitachi   | HUA722020ALA331    | 2 TB   | 44      | 1884  | 71    | 2.96   |
| HGST      | HDS724040ALE640    | 4 TB   | 19      | 1476  | 164   | 2.95   |
| WDC       | WD7502ABYS-02A6B0  | 752 GB | 2       | 2894  | 4     | 2.95   |
| WDC       | WD7500BPVT-35HXZT3 | 752 GB | 4       | 1136  | 1     | 2.94   |
| HGST      | HDN726040ALE614    | 4 TB   | 23      | 1144  | 13    | 2.94   |
| WDC       | WD1004FBYZ-23YC    | 1 TB   | 4       | 1074  | 0     | 2.94   |
| Seagate   | ST1000NX0423 00... | 1 TB   | 5       | 1073  | 0     | 2.94   |
| WDC       | WD5000AAKS-00V2B0  | 500 GB | 4       | 1202  | 1     | 2.94   |
| WDC       | WD360ADFD-00NLR1   | 37 GB  | 2       | 1073  | 0     | 2.94   |
| WDC       | WD15EVDS-63V9B1    | 1.5 TB | 3       | 1581  | 4     | 2.94   |
| Maxtor    | 6L020J1            | 20 GB  | 3       | 1213  | 2     | 2.93   |
| WDC       | WD6000HLHX-01JJPV0 | 600 GB | 17      | 1579  | 10    | 2.93   |
| WDC       | WD1600AAJS-60WAA0  | 160 GB | 10      | 1170  | 102   | 2.93   |
| WDC       | WD2003FYYS-01T8B0  | 2 TB   | 2       | 3318  | 5     | 2.92   |
| Seagate   | ST3300622AS        | 304 GB | 4       | 1477  | 1     | 2.92   |
| WDC       | WD20EURX-57T0FY1   | 2 TB   | 2       | 1064  | 0     | 2.92   |
| WDC       | WD6400AAKS-65A7B2  | 640 GB | 42      | 1479  | 14    | 2.91   |
| Samsung   | HD160JJ-P          | 160 GB | 19      | 1452  | 322   | 2.91   |
| WDC       | WD5000AAKS-00TMA0  | 500 GB | 20      | 1172  | 3     | 2.91   |
| Seagate   | ST9500620NS        | 500 GB | 6       | 1459  | 5     | 2.91   |
| HP        | FB160C4081         | 160 GB | 2       | 1164  | 44    | 2.91   |
| Seagate   | ST3300822AS        | 304 GB | 4       | 1214  | 602   | 2.91   |
| Seagate   | ST10000DM0004      | 10 TB  | 3       | 1059  | 0     | 2.90   |
| WDC       | WD10EALX-759BA1    | 1 TB   | 20      | 1425  | 154   | 2.90   |
| WDC       | WD1001FALS-00E3A0  | 1 TB   | 9       | 1498  | 184   | 2.90   |
| WDC       | WD2500AAJS-75VWA0  | 250 GB | 3       | 1056  | 0     | 2.89   |
| Hitachi   | HCS5C2020ALA632    | 2 TB   | 4       | 1772  | 3     | 2.89   |
| Toshiba   | MG04ACA600EY       | 6 TB   | 3       | 1055  | 0     | 2.89   |
| Maxtor    | STM3320620AS       | 320 GB | 3       | 1055  | 0     | 2.89   |
| WDC       | WD1600JS-60MHB1    | 160 GB | 8       | 1181  | 3     | 2.89   |
| WDC       | WD6002FZWX-00GBGB0 | 6 TB   | 2       | 1675  | 2     | 2.88   |
| WDC       | WD10EZEX-00ER1A0   | 1 TB   | 13      | 1177  | 1     | 2.88   |
| WDC       | WD2500JS-00MHB1    | 250 GB | 2       | 1052  | 0     | 2.88   |
| WDC       | WD1500HLFS-01G6U4  | 150 GB | 4       | 1051  | 0     | 2.88   |
| WDC       | WD2000FYYZ-01UL1B2 | 2 TB   | 10      | 1247  | 1     | 2.88   |
| WDC       | WD3200AAKS-75SBA0  | 320 GB | 6       | 1049  | 0     | 2.87   |
| WDC       | WD6400AAKS-75A7B0  | 640 GB | 7       | 1267  | 1     | 2.87   |
| WDC       | WD3000BLFS-08YBU0  | 304 GB | 2       | 1048  | 0     | 2.87   |
| WDC       | WD5001AALS-00E3A0  | 500 GB | 21      | 1526  | 60    | 2.87   |
| WDC       | WD2000F9YZ-09N20L0 | 2 TB   | 14      | 1509  | 418   | 2.87   |
| WDC       | WD20EARX-00PASB0   | 2 TB   | 335     | 1363  | 90    | 2.87   |
| WDC       | WD5000BMVV-11A1CS0 | 500 GB | 7       | 1194  | 27    | 2.86   |
| WDC       | WD6401AALS-00L3B2  | 640 GB | 37      | 1390  | 4     | 2.86   |
| WDC       | WD80EZZX-11CSGA0   | 8 TB   | 20      | 1414  | 63    | 2.85   |
| WDC       | WD6400AACS-00G8B0  | 640 GB | 10      | 1170  | 65    | 2.85   |
| Hitachi   | HDS721075KLA330    | 752 GB | 13      | 1193  | 8     | 2.85   |
| Seagate   | ST1000NM0033-9Z... | 1 TB   | 78      | 1272  | 93    | 2.85   |
| WDC       | WD10EAVS-00M4B0    | 1 TB   | 2       | 1038  | 0     | 2.84   |
| Maxtor    | 6H500F0            | 500 GB | 2       | 1037  | 0     | 2.84   |
| Hitachi   | HCS5C1010CLA382    | 1 TB   | 8       | 1037  | 0     | 2.84   |
| Hitachi   | HDT725032VLA380    | 320 GB | 25      | 1421  | 56    | 2.84   |
| WDC       | WD800BB-75FRA0     | 80 GB  | 2       | 1034  | 0     | 2.83   |
| WDC       | WD30EZRX-00AZ6B0   | 3 TB   | 10      | 1593  | 29    | 2.83   |
| WDC       | WD5000AAKS-40V2B0  | 500 GB | 2       | 1031  | 0     | 2.83   |
| WDC       | WD2500JS-75NCB3    | 250 GB | 11      | 1280  | 12    | 2.82   |
| WDC       | WD5000AAKS-22YGA0  | 500 GB | 9       | 1195  | 51    | 2.82   |
| Seagate   | ST4000NM0245-1Z... | 4 TB   | 11      | 1206  | 1     | 2.82   |
| Hitachi   | HUA722010CLA331    | 1 TB   | 3       | 1365  | 222   | 2.81   |
| WDC       | WD1002F9YZ-09H1JL1 | 1 TB   | 11      | 1023  | 0     | 2.80   |
| Seagate   | ST320413A          | 20 GB  | 2       | 1076  | 2     | 2.80   |
| WDC       | WD800JD-60LUA0     | 80 GB  | 3       | 1020  | 0     | 2.80   |
| WDC       | WD1003FBYX-01Y7B0  | 1 TB   | 35      | 1568  | 63    | 2.79   |
| WDC       | WD400LB-00DNA0     | 40 GB  | 2       | 1103  | 2     | 2.78   |
| HP        | MB2000GCVBR        | 2 TB   | 2       | 1016  | 0     | 2.78   |
| Seagate   | ST3500630AS        | 500 GB | 98      | 1508  | 228   | 2.78   |
| WDC       | WD4000AAKS-00YGA0  | 400 GB | 8       | 1165  | 1     | 2.78   |
| WDC       | WD5000AACS-61M6B2  | 500 GB | 3       | 2013  | 4     | 2.78   |
| WDC       | WD6001F4PZ-49CWHM0 | 6 TB   | 3       | 1755  | 2     | 2.78   |
| Seagate   | ST31000521AS       | 1 TB   | 2       | 1010  | 0     | 2.77   |
| WDC       | WD5000AAKS-07V0A0  | 500 GB | 2       | 1006  | 0     | 2.76   |
| WDC       | WD10EZEX-00KUWA0   | 1 TB   | 60      | 1114  | 2     | 2.75   |
| WDC       | WD1600ADFS-75SLR2  | 160 GB | 2       | 2094  | 102   | 2.75   |
| WDC       | WD25EZRX-00MMMB0   | 2.5 TB | 6       | 1880  | 6     | 2.74   |
| WDC       | WD4002FYYZ-01B7CB1 | 4 TB   | 9       | 999   | 0     | 2.74   |
| Toshiba   | MG04ACA400E        | 4 TB   | 22      | 998   | 0     | 2.74   |
| WDC       | WD2000JD-22HBC0    | 200 GB | 4       | 1496  | 3     | 2.74   |
| WDC       | WD101KRYZ-01JPDB1  | 10 TB  | 6       | 998   | 0     | 2.73   |
| WDC       | WD8000AARS-00Y5B1  | 800 GB | 5       | 2107  | 10    | 2.73   |
| Seagate   | ST1500LM003-9YH148 | 1.5 TB | 2       | 996   | 0     | 2.73   |
| Seagate   | ST3400833AS        | 400 GB | 2       | 996   | 0     | 2.73   |
| WDC       | WD5000AAKS-65A7B2  | 500 GB | 3       | 996   | 0     | 2.73   |
| WDC       | WD2000FYYZ-05UL1B0 | 2 TB   | 2       | 996   | 0     | 2.73   |
| HGST      | HUH721010ALN600    | 10 TB  | 5       | 995   | 0     | 2.73   |
| WDC       | WD1002FAEX-00Z3A0  | 1 TB   | 195     | 1281  | 56    | 2.72   |
| Hitachi   | HDS723030BLE640    | 3 TB   | 4       | 1045  | 505   | 2.72   |
| Hitachi   | HDE721010SLA330    | 1 TB   | 19      | 1991  | 120   | 2.72   |
| WDC       | WD3200JS-63PDB1    | 320 GB | 3       | 1327  | 217   | 2.71   |
| WDC       | WD3200YS-01PGB0    | 320 GB | 5       | 1016  | 1     | 2.71   |
| WDC       | WD2500JS-60NCB1    | 250 GB | 12      | 1109  | 8     | 2.71   |
| Seagate   | ST8000NC0002-1X... | 8 TB   | 2       | 1039  | 41    | 2.70   |
| WDC       | WD30EZRX-22D8PB0   | 3 TB   | 14      | 1135  | 3     | 2.70   |
| WDC       | WD2000JS-22NCB1    | 200 GB | 3       | 1611  | 16    | 2.70   |
| WDC       | WD15EARX-00ZUDB0   | 1.5 TB | 6       | 1259  | 3     | 2.69   |
| WDC       | WD30NMVW-11C3NS4   | 3 TB   | 2       | 983   | 0     | 2.69   |
| Seagate   | ST1000NX0443       | 1 TB   | 4       | 981   | 0     | 2.69   |
| WDC       | WD20EURX-57T0FY0   | 2 TB   | 2       | 981   | 0     | 2.69   |
| Seagate   | ST4000VN000-2AH166 | 4 TB   | 4       | 978   | 0     | 2.68   |
| WDC       | WD800JD-08LSA0     | 80 GB  | 15      | 1126  | 2     | 2.68   |
| WDC       | WD20EZRX-00DC0B0   | 2 TB   | 107     | 1198  | 21    | 2.68   |
| WDC       | WD2003FZEX-00Z4SA0 | 2 TB   | 86      | 1181  | 17    | 2.67   |
| WDC       | WD30EZRX-00MMMB0   | 3 TB   | 83      | 1328  | 50    | 2.67   |
| WDC       | WD30EZRS-42KEZB0   | 3 TB   | 4       | 973   | 0     | 2.67   |
| Seagate   | ST8000VN0022-2E... | 8 TB   | 89      | 1084  | 5     | 2.67   |
| Apple     | HDD ST2000LM003    | 2 TB   | 2       | 973   | 0     | 2.67   |
| WDC       | WD5000AAKS-22TMA0  | 500 GB | 3       | 973   | 0     | 2.67   |
| WDC       | WD30EZRX-00DC0B0   | 3 TB   | 97      | 1225  | 32    | 2.67   |
| WDC       | WD6400AAKS-75A7B2  | 640 GB | 10      | 1073  | 3     | 2.66   |
| Seagate   | ST1000NM0053-1C... | 1 TB   | 3       | 970   | 0     | 2.66   |
| WDC       | WD1001FALS-00E8B0  | 1 TB   | 19      | 1394  | 119   | 2.66   |
| Hitachi   | HDS728040PLAT20    | 41 GB  | 7       | 1265  | 1     | 2.66   |
| HGST      | HTE721010A9E630    | 1 TB   | 21      | 1074  | 1     | 2.65   |
| Seagate   | ST91000640NS       | 1 TB   | 64      | 1140  | 1     | 2.65   |
| Seagate   | ST4000DM006-2G5107 | 4 TB   | 9       | 965   | 0     | 2.65   |
| Seagate   | ST3000VN007-2E4166 | 3 TB   | 26      | 1027  | 1     | 2.65   |
| WDC       | WD30EFRX-68EUZN0   | 3 TB   | 333     | 1223  | 16    | 2.64   |
| WDC       | WD7500KMVV-11TK7S1 | 752 GB | 2       | 964   | 0     | 2.64   |
| WDC       | WD1600AAJB-56R1A0  | 160 GB | 4       | 1010  | 2     | 2.63   |
| WDC       | WD1600AAJS-75B4A0  | 160 GB | 5       | 1384  | 2     | 2.63   |
| WDC       | WD1600AAJS-22PSA0  | 160 GB | 21      | 1086  | 24    | 2.63   |
| WDC       | WD1600AAJS-08B4A0  | 160 GB | 2       | 957   | 0     | 2.62   |
| Hitachi   | HDT722520DLA380    | 200 GB | 5       | 1127  | 2     | 2.62   |
| WDC       | WD7501AALS-00J7B0  | 752 GB | 28      | 1335  | 117   | 2.62   |
| WDC       | WD1600BB-22RDA0    | 160 GB | 2       | 947   | 0     | 2.60   |
| WDC       | WD2500AAKX-22ERMA0 | 250 GB | 2       | 946   | 0     | 2.59   |
| Seagate   | ST10000VN0008-2... | 10 TB  | 7       | 946   | 0     | 2.59   |
| WDC       | WD4000FYYZ-01UL1B2 | 4 TB   | 16      | 1497  | 201   | 2.59   |
| WDC       | WD40EURX-64WRWY0   | 4 TB   | 5       | 944   | 0     | 2.59   |
| WDC       | WD2002FYPS-02W3B0  | 2 TB   | 19      | 1683  | 7     | 2.58   |
| Seagate   | ST6000DM004-2EH11C | 6 TB   | 8       | 1044  | 1     | 2.57   |
| Seagate   | ST4000NM0033-9Z... | 4 TB   | 48      | 1496  | 329   | 2.57   |
| WDC       | WD5000AAKS-00YGA0  | 500 GB | 32      | 1190  | 3     | 2.57   |
| WDC       | WD60EFAX-68JH4N0   | 6 TB   | 4       | 938   | 0     | 2.57   |
| Toshiba   | MD04ACA400         | 4 TB   | 39      | 1135  | 194   | 2.57   |
| Seagate   | ST14000NM0018-2... | 14 TB  | 13      | 1026  | 6     | 2.57   |
| Toshiba   | MD04ABA400V        | 4 TB   | 3       | 936   | 0     | 2.57   |
| Seagate   | ST2000NM0033-9Z... | 2 TB   | 29      | 1193  | 205   | 2.57   |
| WDC       | WD5000AAKB-00YSA0  | 500 GB | 2       | 935   | 0     | 2.56   |
| Hitachi   | HDS721016CLA382    | 160 GB | 18      | 1199  | 228   | 2.56   |
| WDC       | WD10EARS-003BB1    | 1 TB   | 20      | 1202  | 87    | 2.56   |
| HGST      | HUS726040ALE614    | 4 TB   | 12      | 939   | 3     | 2.56   |
| Seagate   | ST500LM024-1RS152  | 500 GB | 2       | 932   | 0     | 2.56   |
| Seagate   | ST5000AS0011-1L... | 5 TB   | 3       | 1511  | 339   | 2.55   |
| Seagate   | ST4000DM000-1F2168 | 4 TB   | 215     | 1175  | 154   | 2.55   |
| Hitachi   | HDS721075CLA332    | 752 GB | 8       | 1200  | 380   | 2.55   |
| HP        | MB1000GCWCV        | 1 TB   | 3       | 938   | 27    | 2.55   |
| Samsung   | HD400LD            | 400 GB | 5       | 1135  | 150   | 2.54   |
| IBM/Hi... | IC35L060AVV207-0   | 40 GB  | 4       | 1774  | 30    | 2.54   |
| WDC       | WD20EFRX-68AX9N0   | 2 TB   | 50      | 1383  | 8     | 2.54   |
| WDC       | WD6001FZWX-00A2VA0 | 6 TB   | 13      | 1145  | 8     | 2.53   |
| WDC       | WD1600JS-55MHB1    | 160 GB | 3       | 924   | 0     | 2.53   |
| WDC       | WD5000BMVV-11GNWS0 | 500 GB | 7       | 1106  | 13    | 2.53   |
| WDC       | WD5003ABYX-88 LEN  | 500 GB | 3       | 1114  | 4     | 2.53   |
| WDC       | WD800JD-60LSA5     | 80 GB  | 33      | 960   | 1     | 2.53   |
| WDC       | WD40EFRX-68WT0N0   | 4 TB   | 223     | 1287  | 14    | 2.52   |
| WDC       | WD3200AAKS-00YGA0  | 320 GB | 6       | 994   | 1     | 2.52   |
| WDC       | WD1600JB-00REA0    | 160 GB | 9       | 1095  | 133   | 2.52   |
| HGST      | HUS726T6TALE6L1    | 6 TB   | 24      | 988   | 7     | 2.52   |
| WDC       | WD3202ABYS-02B7A0  | 320 GB | 8       | 1039  | 11    | 2.51   |
| Fujitsu   | MHV2040BH          | 40 GB  | 4       | 914   | 0     | 2.51   |
| Toshiba   | MK2561GSY          | 250 GB | 2       | 913   | 0     | 2.50   |
| WDC       | WD20EZRX-00D8PB0   | 2 TB   | 252     | 1053  | 36    | 2.50   |
| WDC       | WD2500JS-40TGB0    | 250 GB | 4       | 1114  | 1     | 2.50   |
| WDC       | WD3200AAVS-00ZTB0  | 320 GB | 2       | 1145  | 1     | 2.49   |
| WDC       | WD800JB-00FMA0     | 80 GB  | 2       | 1099  | 343   | 2.49   |
| WDC       | WD15EARS-60MVWB0   | 1.5 TB | 12      | 1566  | 33    | 2.48   |

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
| HPE         | 5      | 25      | 1751  | 40    | 3.22   |
| HP          | 26     | 117     | 1481  | 97    | 2.64   |
| MaxDigital  | 3      | 9       | 845   | 32    | 1.54   |
| WDC         | 1699   | 34742   | 732   | 39    | 1.48   |
| Apple       | 18     | 437     | 695   | 79    | 1.44   |
| Magnetic... | 2      | 4       | 488   | 0     | 1.34   |
| Hitachi     | 247    | 7316    | 828   | 197   | 1.33   |
| Quantum     | 1      | 2       | 483   | 0     | 1.32   |
| Samsung     | 128    | 4109    | 866   | 233   | 1.24   |
| HGST        | 88     | 4342    | 613   | 247   | 1.21   |
| Seagate     | 683    | 35635   | 648   | 168   | 1.15   |
| ExcelStor   | 4      | 32      | 840   | 209   | 1.00   |
| MediaMax    | 10     | 26      | 480   | 55    | 0.96   |
| Toshiba     | 261    | 12090   | 465   | 96    | 0.94   |
| China       | 2      | 4       | 332   | 345   | 0.74   |
| Fujitsu     | 76     | 987     | 407   | 112   | 0.68   |
| IBM/Hitachi | 15     | 55      | 731   | 43    | 0.67   |
| Maxtor      | 87     | 911     | 524   | 268   | 0.65   |
| Lenovo      | 2      | 8       | 166   | 0     | 0.46   |
| MARSHAL     | 3      | 9       | 335   | 431   | 0.42   |
| IBM         | 1      | 2       | 1494  | 37    | 0.39   |
| DELL        | 1      | 2       | 135   | 0     | 0.37   |
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
| HPE       | MK0200GCTYV        | 200 GB | 2       | 3266  | 0     | 8.95   |
| Transcend | 3E128-TS2-550B01   | 100 GB | 16      | 3197  | 1     | 7.88   |
| Samsung   | MO0200EBTJU        | 200 GB | 2       | 2807  | 0     | 7.69   |
| Samsung   | MZ7KM120HAFD-00005 | 120 GB | 2       | 2779  | 0     | 7.61   |
| Samsung   | MZ7WD240HAFV-00003 | 240 GB | 2       | 2706  | 0     | 7.41   |
| HP        | VK0480GEYJR        | 480 GB | 2       | 2523  | 0     | 6.91   |
| Samsung   | 470 Series SSD     | 256 GB | 2       | 2498  | 0     | 6.85   |
| Intel     | SSDSC2BA200G3      | 200 GB | 4       | 2440  | 0     | 6.69   |
| Kingston  | SSDNOW             | 32 GB  | 10      | 2350  | 0     | 6.44   |
| Corsair   | Force GT           | 50 GB  | 2       | 2183  | 0     | 5.98   |
| OCZ       | REVODRIVE3         | 120 GB | 6       | 2168  | 0     | 5.94   |
| Intel     | SSDSC2BB120G4      | 120 GB | 8       | 2162  | 0     | 5.92   |
| Samsung   | MZ7KM1T9HAJM-00005 | 1.9 TB | 6       | 2145  | 0     | 5.88   |
| Intel     | SSDSC2BB300G4      | 304 GB | 7       | 2120  | 0     | 5.81   |
| Samsung   | MZ7PD480HAGM-000DA | 480 GB | 2       | 2086  | 0     | 5.72   |
| Goodram   | SSD                | 960 GB | 2       | 2023  | 0     | 5.54   |
| Patriot   | Pyro               | 64 GB  | 2       | 1972  | 0     | 5.41   |
| Intel     | SSDSA2SH064G1GC    | 64 GB  | 4       | 1964  | 0     | 5.38   |
| Kingston  | SEDC400S371600G    | 1.6 TB | 2       | 1962  | 0     | 5.38   |
| Intel     | SSDSA2BW120G3      | 120 GB | 2       | 1950  | 0     | 5.34   |
| Samsung   | MZ7WD240HCFV-00003 | 240 GB | 2       | 1938  | 0     | 5.31   |
| Micron    | M500_MTFDDAK960MAV | 960 GB | 3       | 2543  | 2     | 5.27   |
| Intel     | SSDSC2BB240G4      | 240 GB | 9       | 1920  | 0     | 5.26   |
| Micron    | C400-MTFDDAC128MAM | 128 GB | 3       | 1897  | 0     | 5.20   |
| Kingston  | SVP100S2128G       | 128 GB | 5       | 1836  | 0     | 5.03   |
| Intel     | SSDSC2BB240G6      | 240 GB | 6       | 1826  | 0     | 5.00   |
| Intel     | SSDSC2BB160G4      | 160 GB | 7       | 1814  | 0     | 4.97   |
| Corsair   | Force 3 SSD        | 180 GB | 10      | 1943  | 1     | 4.89   |
| Intel     | SSDSC1BG800G4      | 800 GB | 2       | 1777  | 0     | 4.87   |
| Intel     | SSDSC2KB480G7      | 480 GB | 42      | 1897  | 1     | 4.83   |
| Intel     | SSDSA2BZ300G3S     | 304 GB | 2       | 1710  | 0     | 4.69   |
| Samsung   | MZ7KH1T9HAJR-00005 | 1.9 TB | 2       | 1700  | 0     | 4.66   |
| Intel     | SSDSC2KG240G7R     | 240 GB | 3       | 1676  | 0     | 4.59   |
| Corsair   | Neutron XTI SSD    | 480 GB | 2       | 1673  | 0     | 4.59   |
| Samsung   | MO0100EBTJT        | 100 GB | 2       | 1671  | 0     | 4.58   |
| Samsung   | MZ7KM960HAHP-00005 | 960 GB | 12      | 1748  | 1     | 4.58   |
| Intel     | SSDSC2BB016T4      | 1.6 TB | 4       | 1923  | 1     | 4.49   |
| Samsung   | MZNLN512HCJH-00000 | 512 GB | 2       | 1637  | 0     | 4.49   |
| Intel     | SSDSC2BA400G3      | 400 GB | 4       | 1608  | 0     | 4.41   |
| Intel     | SSDSC2BB480G7      | 480 GB | 24      | 2017  | 2     | 4.34   |
| Intel     | SSDSC2BB800G4      | 800 GB | 5       | 1581  | 0     | 4.33   |
| Toshiba   | THNSNC064GMMJ      | 64 GB  | 4       | 1570  | 0     | 4.30   |
| Intel     | SSDMCEAC120B3      | 120 GB | 5       | 1834  | 1     | 4.27   |
| Intel     | SSDSC2BB480G4      | 480 GB | 10      | 1553  | 0     | 4.26   |
| Samsung   | SSD PM851a 2.5 7mm | 1 TB   | 3       | 1544  | 0     | 4.23   |
| OCZ       | VERTEX2            | 40 GB  | 2       | 1543  | 0     | 4.23   |
| Intel     | SSDSC2BX480G4K     | 480 GB | 4       | 1541  | 0     | 4.22   |
| Intel     | SSDSC2BB120G6      | 120 GB | 5       | 1527  | 0     | 4.18   |
| Kingston  | SNVP325S2128GB     | 128 GB | 3       | 1504  | 0     | 4.12   |
| Intel     | SSDSC2BB600G4      | 600 GB | 5       | 1486  | 0     | 4.07   |
| OCZ       | VERTEX v1.10       | 64 GB  | 3       | 1655  | 1     | 4.05   |
| ADATA     | XM11               | 120 GB | 2       | 1508  | 1     | 4.03   |
| Samsung   | MZ7KM960HMJP-00005 | 960 GB | 12      | 1471  | 0     | 4.03   |
| Intel     | SSDSC2BP480G4      | 480 GB | 13      | 1473  | 1     | 4.01   |
| Intel     | SSDSC2BA100G3      | 100 GB | 26      | 1527  | 1     | 4.01   |
| Samsung   | MZ7LN256HMJP-00000 | 256 GB | 10      | 1462  | 0     | 4.01   |
| Intel     | SSDSC2BB080G4      | 80 GB  | 14      | 1456  | 0     | 3.99   |
| HP        | VK0480GEQNB        | 480 GB | 4       | 1769  | 1     | 3.98   |
| Samsung   | MZ7LM960HCHP-00003 | 960 GB | 6       | 1442  | 0     | 3.95   |
| Samsung   | MZ7LM240HCGR-00003 | 240 GB | 2       | 1433  | 0     | 3.93   |
| SanDisk   | X300 2.5 7MM       | 128 GB | 2       | 1430  | 0     | 3.92   |
| SanDisk   | SDSA6DM-016G-1006  | 16 GB  | 4       | 1413  | 0     | 3.87   |
| Intel     | SSDSC2BX400G4      | 400 GB | 2       | 1404  | 0     | 3.85   |
| Toshiba   | THNSF8120CCSE      | 120 GB | 2       | 1403  | 0     | 3.85   |
| Hyundai   | 120GB SSD          | 120 GB | 3       | 1403  | 0     | 3.84   |
| Samsung   | MZ7LN512HMJP-000L1 | 512 GB | 2       | 1380  | 0     | 3.78   |
| Crucial   | CT250MX200SSD4     | 250 GB | 4       | 1379  | 0     | 3.78   |
| HP        | VK000240GWSRQ      | 240 GB | 4       | 1378  | 0     | 3.78   |
| Samsung   | MZ7WD960HMHP-00003 | 880 GB | 2       | 2062  | 1     | 3.77   |
| Intel     | SSDSC2BB800G7      | 800 GB | 29      | 1589  | 1     | 3.76   |
| SanDisk   | SD8SB8U128G1122    | 128 GB | 2       | 1359  | 0     | 3.72   |
| Corsair   | Neutron GTX SSD    | 480 GB | 2       | 1345  | 0     | 3.69   |
| SuperM... | SSD                | 128 GB | 2       | 1778  | 1     | 3.66   |
| Micron    | M510DC_MTFDDAK2... | 240 GB | 2       | 1322  | 0     | 3.62   |
| Kingston  | SVP100S296G        | 96 GB  | 4       | 1321  | 0     | 3.62   |
| Samsung   | MZ7GE960HMHP-00003 | 960 GB | 2       | 2613  | 508   | 3.59   |
| SanDisk   | SD8SB8U1T00        | 1 TB   | 2       | 1308  | 0     | 3.59   |
| SanDisk   | SDSSDXP480G        | 480 GB | 3       | 1306  | 0     | 3.58   |
| Corsair   | Force 3 SSD        | 240 GB | 15      | 1411  | 70    | 3.58   |
| Intel     | SSDSC2BB150G7      | 150 GB | 22      | 1507  | 1     | 3.56   |
| Samsung   | MZ7PC256HAFU-000L7 | 256 GB | 5       | 1296  | 0     | 3.55   |
| Micron    | 1100 SATA          | 1 TB   | 2       | 1294  | 0     | 3.55   |
| SanDisk   | SD5SE2128G1002E    | 128 GB | 4       | 1285  | 0     | 3.52   |
| Samsung   | SSD 850 PRO        | 1 TB   | 84      | 1325  | 3     | 3.50   |
| Intel     | SSDSA2SH032G1GN    | 32 GB  | 4       | 1274  | 0     | 3.49   |
| Intel     | SSDSC2KB240G7      | 240 GB | 5       | 1518  | 1     | 3.48   |
| Samsung   | MZ7PD128HCFV-000H7 | 128 GB | 2       | 1266  | 0     | 3.47   |
| OCZ       | VERTEX2            | 120 GB | 16      | 1260  | 0     | 3.45   |
| Toshiba   | THNSNJ120PCSZ      | 120 GB | 2       | 1255  | 0     | 3.44   |
| OCZ       | VERTEX PLUS R2     | 64 GB  | 3       | 1248  | 0     | 3.42   |
| Samsung   | MZ7KM480HMHQ-00005 | 480 GB | 5       | 1243  | 0     | 3.41   |
| Intel     | SSDSC2BB480G6      | 480 GB | 3       | 1240  | 0     | 3.40   |
| Kingston  | SVP100S264G        | 64 GB  | 4       | 1237  | 0     | 3.39   |
| Seagate   | XF1230-1A0960      | 960 GB | 2       | 1236  | 0     | 3.39   |
| Apple     | SSD SM768E         | 752 GB | 4       | 1234  | 0     | 3.38   |
| Intel     | SSDSA2CT040G3      | 40 GB  | 12      | 1230  | 0     | 3.37   |
| Intel     | SSDSC2CW240A3      | 240 GB | 47      | 1263  | 1     | 3.37   |
| Toshiba   | THNSNH256GCST      | 256 GB | 5       | 1220  | 0     | 3.34   |
| Intel     | SSDSA2BW160G3      | 160 GB | 3       | 1222  | 402   | 3.34   |
| Samsung   | SSD 830 Series     | 512 GB | 15      | 1285  | 135   | 3.34   |
| SK hynix  | SC300B SATA        | 256 GB | 3       | 1214  | 0     | 3.33   |
| Apple     | SSD SM1024F        | 1 TB   | 21      | 1231  | 1     | 3.28   |
| Corsair   | Force GT           | 180 GB | 4       | 1193  | 0     | 3.27   |
| Patriot   | Ignite             | 480 GB | 4       | 1192  | 0     | 3.27   |
| Samsung   | SSD 840 EVO        | 1 TB   | 76      | 1262  | 17    | 3.23   |
| OCZ       | TRION150           | 960 GB | 2       | 1176  | 0     | 3.22   |
| KingDian  | N400               | 240 GB | 2       | 1174  | 0     | 3.22   |
| Seagate   | ST480HM000-1G5162  | 480 GB | 2       | 1282  | 1     | 3.20   |
| Intel     | SSDSC2BB016T7      | 1.6 TB | 3       | 2032  | 2     | 3.19   |
| Samsung   | MZMTE512HMHP-000L1 | 512 GB | 3       | 1165  | 0     | 3.19   |
| Corsair   | Force GT           | 120 GB | 24      | 1330  | 2     | 3.15   |
| Micron    | M600_MTFDDAK1T0MBF | 1 TB   | 11      | 1149  | 0     | 3.15   |
| Crucial   | C300-CTFDDAC256MAG | 256 GB | 5       | 1651  | 484   | 3.14   |
| Samsung   | MZHPV512HDGL-00000 | 512 GB | 6       | 1137  | 0     | 3.12   |
| Samsung   | MZ7LH960HAJR-00005 | 960 GB | 11      | 1133  | 0     | 3.11   |
| Intel     | SSDSC2BB240G7      | 240 GB | 9       | 1133  | 0     | 3.11   |
| Micron    | 5300_MTFDDAK480TDT | 480 GB | 2       | 1131  | 0     | 3.10   |
| OCZ       | VERTEX2            | 64 GB  | 25      | 1163  | 12    | 3.10   |
| Intel     | SSDSC2CW180A3      | 180 GB | 20      | 1127  | 0     | 3.09   |
| Micron    | 5200_MTFDDAK7T6TDC | 7.6 TB | 15      | 1360  | 1     | 3.06   |
| Toshiba   | THNS128GG4BAAA-... | 128 GB | 6       | 1116  | 0     | 3.06   |
| Samsung   | SSD 850 EVO        | 2 TB   | 33      | 1114  | 0     | 3.05   |
| PNY       | CS2211 240GB SSD   | 240 GB | 3       | 1112  | 0     | 3.05   |
| Corsair   | Force GS           | 480 GB | 3       | 1884  | 15    | 3.02   |
| Crucial   | M4-CT064M4SSD2     | 64 GB  | 45      | 1201  | 139   | 3.00   |
| Kingston  | RBU-SC400S37256G   | 256 GB | 2       | 1095  | 0     | 3.00   |
| Toshiba   | TL100              | 120 GB | 5       | 1094  | 0     | 3.00   |
| Toshiba   | TR150              | 960 GB | 4       | 1089  | 0     | 2.98   |
| Mushkin   | MKNSSDCR120GB      | 120 GB | 9       | 1306  | 4     | 2.98   |
| Corsair   | Force GS           | 180 GB | 3       | 1087  | 0     | 2.98   |
| Intel     | SSDSC2BB800G6      | 800 GB | 8       | 1082  | 0     | 2.97   |
| Samsung   | MZ7LN512HCHP-00000 | 512 GB | 3       | 1076  | 0     | 2.95   |
| PNY       | CS1311 960GB SSD   | 960 GB | 4       | 1074  | 0     | 2.94   |
| OCZ       | REVODRIVE350       | 120 GB | 4       | 1073  | 0     | 2.94   |
| Crucial   | M4-CT512M4SSD2     | 512 GB | 16      | 1732  | 580   | 2.94   |
| Intel     | SSDSA2CW080G3      | 80 GB  | 25      | 1108  | 1     | 2.94   |
| Samsung   | SSD PB22-JS3 FD... | 256 GB | 5       | 1071  | 0     | 2.93   |
| Samsung   | MZ7PC128HAFU-000L1 | 128 GB | 4       | 1069  | 0     | 2.93   |
| KingSpec  | SPK-SF12-M120      | 120 GB | 2       | 1069  | 0     | 2.93   |
| SATADOM   | SL 3ME3 V2         | 128 GB | 2       | 1064  | 0     | 2.92   |
| Samsung   | SSD PM800 2.5"     | 256 GB | 4       | 1062  | 0     | 2.91   |
| SK hynix  | SC311 SATA         | 1 TB   | 2       | 1058  | 0     | 2.90   |
| Patriot   | Blast              | 480 GB | 3       | 1046  | 0     | 2.87   |
| Samsung   | SSD 830 Series     | 128 GB | 96      | 1102  | 43    | 2.84   |
| Toshiba   | THNSNC128GMMJ      | 128 GB | 6       | 1037  | 0     | 2.84   |
| Intel     | SSDSC2BA800G4      | 800 GB | 5       | 1031  | 0     | 2.83   |
| Intel     | SSDSC2BB120G7R     | 120 GB | 5       | 1030  | 0     | 2.82   |
| Samsung   | MZ7PC128HAFU-000L5 | 128 GB | 2       | 1028  | 0     | 2.82   |
| Micron    | MTFDDAK960TDC-1... | 960 GB | 2       | 1022  | 0     | 2.80   |
| Samsung   | SSD 840 EVO        | 500 GB | 142     | 1107  | 29    | 2.80   |
| Toshiba   | THNSNJ512GDNU      | 512 GB | 2       | 1021  | 0     | 2.80   |
| OCZ       | SOLID3             | 64 GB  | 9       | 1168  | 124   | 2.79   |
| Samsung   | MZ7LN128HCHP-00000 | 128 GB | 7       | 1016  | 0     | 2.78   |
| OCZ       | VERTEX2 3.5        | 240 GB | 2       | 1011  | 0     | 2.77   |
| OCZ       | AGILITY3           | 90 GB  | 7       | 1471  | 1     | 2.76   |
| OCZ       | AGILITY4           | 128 GB | 9       | 1004  | 0     | 2.75   |
| ADATA     | SP800              | 32 GB  | 2       | 1001  | 0     | 2.74   |
| Apple     | SSD TS256C         | 256 GB | 17      | 1125  | 1     | 2.73   |
| Kingston  | SH103S390G         | 90 GB  | 5       | 1368  | 1     | 2.73   |
| Micron    | M600_MTFDDAK256MBF | 256 GB | 6       | 989   | 0     | 2.71   |
| SanDisk   | SD7SB7S512G1122    | 512 GB | 4       | 987   | 0     | 2.71   |
| Kingston  | SH100S3120G        | 120 GB | 10      | 987   | 0     | 2.70   |
| Samsung   | MZ7LM960HCHP-00005 | 960 GB | 2       | 985   | 0     | 2.70   |
| OCZ       | NOCTI              | 64 GB  | 2       | 974   | 0     | 2.67   |
| WDC       | WD1001X06X-00SJVT0 | 1.1 TB | 3       | 974   | 0     | 2.67   |
| Lite-On   | PH4-CE240          | 240 GB | 3       | 969   | 0     | 2.66   |
| Intel     | SSDSC2BX200G4      | 200 GB | 2       | 969   | 0     | 2.66   |
| Toshiba   | THNSFC256GAMJ      | 256 GB | 3       | 968   | 0     | 2.65   |
| SanDisk   | SD6SF1M064G1022    | 64 GB  | 2       | 963   | 0     | 2.64   |
| Micron    | MTFDDAK256MBF-1... | 256 GB | 10      | 961   | 0     | 2.63   |
| Intel     | SSDMCEAW240A4      | 240 GB | 2       | 1130  | 765   | 2.63   |
| Samsung   | SSD 830 Series     | 256 GB | 72      | 985   | 43    | 2.62   |
| OCZ       | AGILITY2           | 64 GB  | 4       | 950   | 0     | 2.60   |
| HP        | VK0300GDUQV        | 304 GB | 3       | 945   | 0     | 2.59   |
| HP        | VK000240GWCFD      | 240 GB | 2       | 933   | 0     | 2.56   |
| Intel     | SSDSA2CW120G3      | 120 GB | 29      | 1117  | 35    | 2.54   |
| Kingston  | SE50S3480G         | 480 GB | 10      | 1104  | 1     | 2.54   |
| Samsung   | SSD 850 PRO        | 512 GB | 178     | 990   | 19    | 2.54   |
| Crucial   | M4-CT256M4SSD1     | 256 GB | 5       | 992   | 203   | 2.52   |
| Crucial   | M4-CT128M4SSD2     | 128 GB | 94      | 1025  | 121   | 2.52   |
| WDC       | WDS400T1R0A-68A4W0 | 4 TB   | 3       | 914   | 0     | 2.51   |
| Crucial   | C300-CTFDDAC128MAG | 128 GB | 13      | 1172  | 157   | 2.50   |
| Corsair   | Force 3 SSD        | 120 GB | 52      | 1008  | 70    | 2.50   |
| SanDisk   | SDSSDRC032G        | 32 GB  | 12      | 909   | 0     | 2.49   |
| Corsair   | Force GT           | 240 GB | 7       | 1348  | 237   | 2.48   |
| Samsung   | SSD 850 PRO        | 128 GB | 79      | 945   | 14    | 2.47   |
| Toshiba   | THNSNJ256GCST      | 256 GB | 6       | 900   | 0     | 2.47   |
| Intel     | SSDSC2KG480G8      | 480 GB | 17      | 1084  | 1     | 2.46   |
| Corsair   | Force 3 SSD        | 64 GB  | 23      | 922   | 1     | 2.46   |
| Micron    | 5300_MTFDDAK1T9TDT | 1.9 TB | 20      | 1045  | 1     | 2.45   |
| OCZ       | VERTEX             | 32 GB  | 4       | 1069  | 1     | 2.45   |
| SanDisk   | SD7SB6S128G1122    | 128 GB | 10      | 888   | 0     | 2.43   |
| Samsung   | MZRPA128HMCD-000SO | 64 GB  | 16      | 908   | 1     | 2.43   |
| SanDisk   | SD7SB3Q064G        | 56 GB  | 2       | 885   | 0     | 2.43   |
| Samsung   | SSD 840 PRO Series | 128 GB | 115     | 998   | 13    | 2.40   |
| Intel     | SSDSC2BB800G7R     | 800 GB | 2       | 1166  | 1     | 2.40   |
| Samsung   | MZ7PC128HAFU-000H1 | 128 GB | 11      | 874   | 0     | 2.40   |
| Samsung   | SSD 840 EVO 250... | 250 GB | 16      | 885   | 10    | 2.39   |
| Samsung   | SSD 840 PRO Series | 256 GB | 169     | 1022  | 11    | 2.39   |
| Teclast   | 256GB A750         | 256 GB | 2       | 870   | 0     | 2.38   |
| ADATA     | SX930              | 480 GB | 2       | 869   | 0     | 2.38   |
| Transcend | TS128GSSD340K      | 128 GB | 4       | 867   | 0     | 2.38   |
| SK hynix  | SC300B SATA        | 512 GB | 5       | 867   | 0     | 2.38   |
| Samsung   | MZ7LN256HMJP-000H7 | 256 GB | 2       | 867   | 0     | 2.38   |
| Phison    | SATA SSD           | 16 GB  | 2       | 862   | 0     | 2.36   |
| Samsung   | MZ7TE256HMHP-00000 | 256 GB | 3       | 861   | 0     | 2.36   |
| Samsung   | SSD 830 Series     | 64 GB  | 35      | 861   | 0     | 2.36   |
| Toshiba   | KHK61RSE480G       | 480 GB | 4       | 856   | 0     | 2.35   |
| Micron    | MTFDDAK480TDN      | 480 GB | 3       | 855   | 0     | 2.34   |
| Intel     | SSDSC2BF240A4H     | 240 GB | 2       | 853   | 0     | 2.34   |
| Crucial   | C300-CTFDDAC064MAG | 64 GB  | 12      | 1002  | 168   | 2.34   |
| WDC       | WDBNCE2500PNC-WRSN | 250 GB | 3       | 849   | 0     | 2.33   |
| Samsung   | SSD 840 EVO        | 250 GB | 383     | 926   | 16    | 2.33   |
| MyDigi... | BP5                | 240 GB | 4       | 845   | 0     | 2.32   |
| Intel     | SSDSA2BW600G3      | 600 GB | 3       | 845   | 0     | 2.32   |
| Micron    | MTFDDAK128MBF-1... | 128 GB | 2       | 844   | 0     | 2.31   |
| China     | SSD                | 720 GB | 3       | 842   | 0     | 2.31   |
| Kingston  | SVP200S360G        | 64 GB  | 15      | 887   | 2     | 2.31   |
| Toshiba   | THNSFC128GBSJ      | 128 GB | 4       | 841   | 0     | 2.30   |
| Kingston  | SH103S3120G        | 120 GB | 122     | 901   | 16    | 2.29   |
| OCZ       | VERTEX4            | 256 GB | 48      | 1112  | 1     | 2.29   |
| Kingston  | SMSR150S3256G      | 128 GB | 2       | 833   | 0     | 2.28   |
| Kingston  | RBU-SNS8152S3256GF | 256 GB | 2       | 832   | 0     | 2.28   |
| Samsung   | SSD PM830 2.5" 7mm | 256 GB | 26      | 893   | 78    | 2.27   |
| Kingston  | SM2280S3G2120G     | 120 GB | 19      | 825   | 0     | 2.26   |
| Samsung   | MZ7TE512HMHP-000L1 | 512 GB | 8       | 824   | 0     | 2.26   |
| Samsung   | SSD 840 Series     | 250 GB | 93      | 878   | 1     | 2.26   |
| Samsung   | MZ7LH480HBHQ0D3    | 480 GB | 2       | 823   | 0     | 2.25   |
| WDC       | WDBNCE0010PNC-WRSN | 1 TB   | 2       | 821   | 0     | 2.25   |
| Samsung   | SSD 840 EVO        | 120 GB | 297     | 890   | 14    | 2.25   |
| Intel     | SSDSC2KB019T7      | 1.9 TB | 2       | 1492  | 2     | 2.24   |
| Samsung   | MZ7LN128HAHQ-000H1 | 128 GB | 7       | 818   | 0     | 2.24   |
| Kingston  | SVP200S37A120G     | 120 GB | 23      | 962   | 76    | 2.24   |
| Samsung   | MZ7LM960HMJP-00005 | 960 GB | 4       | 817   | 0     | 2.24   |
| Samsung   | SSD 840 PRO Series | 512 GB | 46      | 1105  | 93    | 2.22   |
| Samsung   | MZ7LN256HCHP-000H1 | 256 GB | 10      | 808   | 0     | 2.22   |
| Samsung   | SSD 850 PRO        | 256 GB | 302     | 851   | 7     | 2.21   |
| Intel     | SSDSC2KG480G7      | 480 GB | 5       | 811   | 2     | 2.21   |
| Samsung   | SSD 840 EVO        | 752 GB | 9       | 806   | 0     | 2.21   |
| SanDisk   | SSD U110           | 128 GB | 5       | 805   | 0     | 2.21   |
| Samsung   | MZ7LH1T9HMLT-00005 | 1.9 TB | 4       | 805   | 0     | 2.21   |
| Samsung   | SSD 850 EVO        | 1 TB   | 261     | 993   | 8     | 2.20   |
| Samsung   | MZ7LN256HAJQ-000H1 | 256 GB | 9       | 802   | 0     | 2.20   |
| China     | OSSD512GBTSS2      | 512 GB | 2       | 802   | 0     | 2.20   |
| Corsair   | Neutron SSD        | 256 GB | 2       | 801   | 0     | 2.20   |
| Toshiba   | THNSNH512GCST      | 512 GB | 3       | 800   | 0     | 2.19   |
| Samsung   | SSD SM871 2.5 7mm  | 256 GB | 14      | 848   | 33    | 2.19   |
| Toshiba   | THNS064GG2BNAA     | 64 GB  | 9       | 799   | 0     | 2.19   |
| OCZ       | VECTOR180          | 480 GB | 2       | 798   | 0     | 2.19   |
| OCZ       | VECTOR             | 256 GB | 5       | 798   | 0     | 2.19   |
| Samsung   | SSD PM800 Serie... | 256 GB | 4       | 988   | 2     | 2.19   |
| Samsung   | SSD PM830 2.5" 7mm | 512 GB | 5       | 917   | 202   | 2.18   |
| Samsung   | MZ7TD512HAGM-000L1 | 512 GB | 5       | 794   | 0     | 2.18   |
| Samsung   | SSD 840 Series     | 120 GB | 131     | 857   | 1     | 2.17   |
| SK        | SKhynix SC300 H... | 512 GB | 2       | 793   | 0     | 2.17   |
| Apple     | SSD SM128E         | 121 GB | 12      | 965   | 2     | 2.17   |
| Samsung   | SSD PM871a 2.5 7mm | 256 GB | 3       | 791   | 0     | 2.17   |
| Hoodisk   | SSD                | 32 GB  | 5       | 791   | 0     | 2.17   |
| Intel     | SSDSA2BW120G3H     | 120 GB | 6       | 815   | 1     | 2.16   |
| Micron    | 5100_MTFDDAK960TCB | 960 GB | 4       | 999   | 15    | 2.16   |
| Toshiba   | Q300 Pro           | 256 GB | 2       | 789   | 0     | 2.16   |
| Samsung   | SSD 850 EVO        | 500 GB | 1069    | 793   | 1     | 2.16   |
| Intel     | SSDSC2CW480A3      | 480 GB | 8       | 787   | 0     | 2.16   |
| Samsung   | MZ7PD256HAFV-000H7 | 256 GB | 12      | 787   | 0     | 2.16   |
| Kingston  | SH100S3240G        | 240 GB | 7       | 1129  | 2     | 2.16   |
| Goodram   | SSD                | 480 GB | 5       | 784   | 0     | 2.15   |
| SanDisk   | SD7SN6S512G1122    | 512 GB | 2       | 779   | 0     | 2.14   |
| Crucial   | M4-CT256M4SSD2     | 256 GB | 60      | 921   | 154   | 2.14   |
| Samsung   | MZ7KM240HMHQ-00005 | 240 GB | 6       | 778   | 0     | 2.13   |
| PNY       | CS1311 240GB SSD   | 240 GB | 32      | 813   | 1     | 2.13   |
| OWC       | Mercury EXTREME... | 480 GB | 8       | 861   | 10    | 2.13   |
| OCZ       | AGILITY3           | 64 GB  | 78      | 956   | 17    | 2.13   |
| DeTech    | Development Tec... | 120 GB | 3       | 875   | 1     | 2.12   |
| SanDisk   | SD9SB8W256G1014    | 256 GB | 3       | 768   | 0     | 2.11   |
| Intel     | SSDMCEAC120B3A     | 120 GB | 4       | 790   | 1     | 2.10   |
| Kingston  | SVP200S390G        | 90 GB  | 2       | 767   | 0     | 2.10   |
| OCZ       | VERTEX2 3.5        | 115 GB | 3       | 765   | 0     | 2.10   |
| SanDisk   | SDSA6MM-016G-1006  | 16 GB  | 15      | 843   | 105   | 2.10   |
| SanDisk   | Ultra II           | 480 GB | 61      | 777   | 1     | 2.08   |
| Kingston  | RBU-SNS6100S3128GD | 128 GB | 2       | 759   | 0     | 2.08   |
| Toshiba   | Q200 EX            | 240 GB | 2       | 758   | 0     | 2.08   |
| Intel     | SSDSC2BB480G7R     | 480 GB | 3       | 1091  | 1     | 2.08   |
| Samsung   | SSD 850 EVO M.2    | 500 GB | 62      | 757   | 0     | 2.08   |
| Intel     | SSDSC2KB019T8      | 1.9 TB | 23      | 925   | 1     | 2.08   |
| SSSTC     | ER2-CD960A         | 960 GB | 2       | 757   | 0     | 2.07   |
| Samsung   | SSD PM830 2.5" 7mm | 128 GB | 36      | 870   | 117   | 2.07   |
| SK hynix  | SC300 SATA         | 512 GB | 3       | 754   | 0     | 2.07   |
| Samsung   | SSD 850 EVO M.2    | 1 TB   | 10      | 753   | 0     | 2.07   |
| SanDisk   | SDSSDXP120G        | 120 GB | 4       | 753   | 0     | 2.06   |
| Samsung   | SSD 840 EVO 120... | 120 GB | 11      | 759   | 1     | 2.06   |
| Corsair   | CSSD-V128GB2       | 128 GB | 2       | 752   | 0     | 2.06   |
| OCZ       | VERTEX3 MI         | 120 GB | 29      | 976   | 106   | 2.05   |
| Samsung   | MZ7TY256HDHP-00007 | 256 GB | 3       | 749   | 0     | 2.05   |
| Kingston  | SVP200S3120G       | 120 GB | 15      | 814   | 133   | 2.05   |
| Intel     | SSDSC2CT060A3      | 64 GB  | 15      | 900   | 1     | 2.04   |
| Toshiba   | KHK61RSE960G       | 960 GB | 2       | 743   | 0     | 2.04   |
| Transcend | TS128GSSD320       | 128 GB | 3       | 743   | 0     | 2.04   |
| Samsung   | SSD 840 Series     | 500 GB | 24      | 952   | 20    | 2.03   |
| Apacer    | AS330              | 240 GB | 2       | 736   | 0     | 2.02   |
| Samsung   | MZ7TE128HMGR-000L1 | 128 GB | 35      | 736   | 0     | 2.02   |
| ADATA     | SP600              | 256 GB | 15      | 734   | 0     | 2.01   |
| OWC       | Mercury Electra... | 1 TB   | 13      | 733   | 0     | 2.01   |
| Kingston  | RBU-SNS8151S396GG  | 96 GB  | 4       | 803   | 2     | 2.01   |
| ADATA     | SP600              | 128 GB | 17      | 732   | 0     | 2.01   |
| SK hynix  | SC300 2.5 7MM      | 128 GB | 2       | 732   | 0     | 2.01   |
| Toshiba   | THNSNJ256G8NU      | 256 GB | 7       | 731   | 0     | 2.01   |
| Crucial   | CT512MX100SSD1     | 512 GB | 74      | 814   | 1     | 2.00   |
| SK hynix  | SC300 M.2 2280     | 128 GB | 7       | 730   | 0     | 2.00   |
| Intel     | SSDSC2MH120A2      | 120 GB | 8       | 729   | 0     | 2.00   |
| ADATA     | SSD S510           | 120 GB | 13      | 738   | 1     | 1.99   |
| SanDisk   | SDSSDHP256G        | 256 GB | 46      | 768   | 1     | 1.99   |
| Corsair   | Force GS           | 128 GB | 30      | 746   | 2     | 1.98   |
| Samsung   | MZ7PA256HMDR-010H1 | 256 GB | 2       | 842   | 520   | 1.98   |
| Corsair   | CSSD-F60GB2        | 64 GB  | 9       | 1531  | 258   | 1.98   |
| SanDisk   | X400 2.5 7MM       | 256 GB | 13      | 721   | 0     | 1.98   |
| Toshiba   | THNSNB128GMCJ      | 128 GB | 5       | 720   | 0     | 1.97   |
| Samsung   | MZMPC256HBGJ-000H1 | 256 GB | 4       | 719   | 0     | 1.97   |
| SanDisk   | SDSSDP064G         | 64 GB  | 58      | 735   | 18    | 1.97   |
| Crucial   | CT3500SC           | 500 GB | 4       | 928   | 6     | 1.97   |
| SanDisk   | SDSSDHII960G       | 960 GB | 18      | 781   | 1     | 1.97   |
| Samsung   | SSD PM800 2.5"     | 128 GB | 6       | 717   | 0     | 1.97   |
| Toshiba   | THNSNH128GBST      | 128 GB | 9       | 885   | 72    | 1.97   |
| Samsung   | MZHPU256HCGL-000H1 | 256 GB | 3       | 716   | 0     | 1.96   |
| Samsung   | SSD 750 EVO        | 500 GB | 57      | 716   | 0     | 1.96   |
| OCZ       | TRION100           | 960 GB | 3       | 716   | 0     | 1.96   |
| Samsung   | SSD PM830 FDE 2... | 256 GB | 3       | 713   | 0     | 1.96   |
| Corsair   | Force LE SSD       | 480 GB | 8       | 713   | 0     | 1.96   |
| Corsair   | Force GS           | 240 GB | 10      | 1246  | 14    | 1.95   |
| Micron    | M500DC_MTFDDAK8... | 800 GB | 2       | 710   | 0     | 1.95   |
| AEGO      | SSD                | 480 GB | 4       | 709   | 0     | 1.95   |
| Micron    | C400-MTFDDAK128MAM | 128 GB | 6       | 708   | 0     | 1.94   |
| Samsung   | MZMPC032HBCD-000D1 | 32 GB  | 9       | 705   | 0     | 1.93   |
| SanDisk   | SSD U110           | 64 GB  | 4       | 705   | 0     | 1.93   |
| Plextor   | PX-128M2S          | 128 GB | 3       | 833   | 1     | 1.93   |
| Mushkin   | MKNSSDTR1TB-3D     | 1 TB   | 2       | 835   | 38    | 1.93   |
| OCZ       | VECTOR             | 128 GB | 9       | 704   | 2     | 1.93   |
| Samsung   | MZNLF192HCGS-000L1 | 192 GB | 5       | 702   | 0     | 1.93   |
| Crucial   | M4-CT128M4SSD1     | 128 GB | 12      | 836   | 169   | 1.93   |
| Samsung   | MZ7LN128HCHP-000H1 | 128 GB | 12      | 700   | 0     | 1.92   |
| Mushkin   | MKNSSDSR500GB      | 500 GB | 3       | 697   | 0     | 1.91   |
| Micron    | MTFDDAK512MBF-1... | 512 GB | 11      | 731   | 2     | 1.91   |
| Samsung   | SSD 850 EVO M.2    | 250 GB | 66      | 695   | 0     | 1.91   |
| WDC       | WDS200T1R0A-68A4W0 | 2 TB   | 7       | 695   | 0     | 1.91   |
| Kingston  | SMSM151S3128GD     | 128 GB | 2       | 692   | 0     | 1.90   |
| Goodram   | SSDPR_CX300_120    | 120 GB | 5       | 692   | 0     | 1.90   |
| Intel     | SSDSC2MH250A2      | 250 GB | 2       | 690   | 0     | 1.89   |
| Corsair   | Force GT           | 64 GB  | 12      | 842   | 3     | 1.89   |
| Apple     | SSD SM0512F        | 500 GB | 71      | 708   | 1     | 1.89   |
| ADATA     | SX950              | 240 GB | 3       | 689   | 0     | 1.89   |
| Crucial   | CT500MX200SSD3     | 500 GB | 8       | 1080  | 21    | 1.88   |
| SanDisk   | SD8SN8U256G1122    | 256 GB | 5       | 685   | 0     | 1.88   |
| Samsung   | MZHPV256HDGL-00000 | 256 GB | 15      | 713   | 1     | 1.87   |
| Apple     | SSD SM1024G        | 1 TB   | 14      | 681   | 0     | 1.87   |
| OCZ       | VERTEX4            | 64 GB  | 14      | 711   | 1     | 1.86   |
| Micron    | M500_MTFDDAK480MAV | 480 GB | 4       | 1093  | 1     | 1.86   |
| Samsung   | SSD SM871 2.5 7mm  | 512 GB | 4       | 1091  | 78    | 1.86   |
| OCZ       | AGILITY3           | 240 GB | 25      | 983   | 13    | 1.86   |
| WDC       | WDS500G1B0B-00AS40 | 500 GB | 9       | 678   | 0     | 1.86   |
| Apple     | SSD SM0256F        | 256 GB | 62      | 685   | 1     | 1.86   |
| Ramaxel   | RTFMB016JGV2BWX    | 16 GB  | 2       | 677   | 0     | 1.86   |
| Toshiba   | THNSFJ256GDNU      | 256 GB | 3       | 676   | 0     | 1.85   |
| Intel     | SSDSC2KG240G7      | 240 GB | 2       | 675   | 0     | 1.85   |
| Seagate   | 2E256-TU2-510B00   | 170 GB | 3       | 2072  | 1366  | 1.85   |
| Apple     | SSD SM0128F        | 121 GB | 5       | 675   | 0     | 1.85   |
| Intel     | SSDSC2BW240A3L     | 240 GB | 15      | 673   | 0     | 1.85   |
| Intel     | SSDSC2BA200G4      | 200 GB | 10      | 730   | 1     | 1.85   |
| SK        | SKhynix SC300 H... | 256 GB | 2       | 672   | 0     | 1.84   |
| OCZ       | AGILITY3           | 120 GB | 93      | 826   | 62    | 1.84   |
| Samsung   | MZHPV128HDGM-00000 | 128 GB | 4       | 671   | 0     | 1.84   |
| Samsung   | SSD 850 EVO        | 120 GB | 209     | 669   | 0     | 1.84   |
| SanDisk   | SDSSDA480G         | 480 GB | 41      | 670   | 1     | 1.83   |
| OCZ       | TRION150           | 480 GB | 11      | 668   | 0     | 1.83   |
| OCZ       | REVODRIVE3         | 240 GB | 2       | 1000  | 1     | 1.83   |
| Samsung   | SSD PM871b 2.5 7mm | 128 GB | 5       | 667   | 0     | 1.83   |
| Micron    | 5200_MTFDDAK1T9TDD | 1.9 TB | 2       | 666   | 0     | 1.83   |
| SanDisk   | SD6SA1M064G1011    | 64 GB  | 4       | 666   | 0     | 1.82   |
| Samsung   | MZ7LN256HAJQ-00000 | 256 GB | 5       | 666   | 0     | 1.82   |
| Innodisk  | Corp. DRPS-02GJ... | 2 GB   | 3       | 664   | 0     | 1.82   |
| Samsung   | SSD 850 EVO        | 250 GB | 1293    | 679   | 3     | 1.81   |
| Kingston  | SHFS37A480G        | 480 GB | 4       | 660   | 0     | 1.81   |
| SanDisk   | SD8SB8U-128G-1006  | 128 GB | 6       | 659   | 0     | 1.81   |
| SK hynix  | HFS256G39MND-3510A | 256 GB | 4       | 656   | 0     | 1.80   |
| Samsung   | MZNLF128HCHP-00004 | 128 GB | 18      | 656   | 0     | 1.80   |
| SK hynix  | SC300 2.5 7MM      | 256 GB | 6       | 655   | 0     | 1.80   |
| Corsair   | Force 3 SSD        | 90 GB  | 10      | 655   | 0     | 1.80   |
| Kingston  | RBU-SNS8152S325... | 256 GB | 3       | 655   | 0     | 1.80   |
| Toshiba   | THNSNJ128G8NY      | 128 GB | 9       | 653   | 0     | 1.79   |
| Samsung   | MZ7PD128HAFV-000H7 | 128 GB | 12      | 696   | 4     | 1.79   |
| Phison    | BP4 mSATA SSD      | 240 GB | 2       | 652   | 0     | 1.79   |
| Samsung   | SSD RBX Series ... | 64 GB  | 2       | 651   | 0     | 1.79   |
| Radeon    | R7                 | 120 GB | 5       | 651   | 0     | 1.78   |
| Samsung   | SSD PM830 mSATA    | 32 GB  | 25      | 650   | 0     | 1.78   |
| Samsung   | MZ7PD128HCFV-000H1 | 128 GB | 13      | 649   | 0     | 1.78   |
| Toshiba   | THNSNJ512GCSU      | 512 GB | 11      | 647   | 0     | 1.77   |
| PNY       | CS1311 120GB SSD   | 120 GB | 12      | 646   | 0     | 1.77   |
| Samsung   | MZNLF128HCHP-00000 | 128 GB | 18      | 646   | 0     | 1.77   |
| SanDisk   | SD8SB8U-256G-1006  | 256 GB | 18      | 745   | 2     | 1.77   |
| Samsung   | MZ-RPC512T-0SO     | 256 GB | 2       | 645   | 0     | 1.77   |
| Toshiba   | THNSNJ256GCSY      | 256 GB | 4       | 645   | 0     | 1.77   |
| Kingston  | SKC300S37A480G     | 480 GB | 2       | 643   | 0     | 1.76   |
| Samsung   | MZ7TE128HMGR-00004 | 128 GB | 11      | 642   | 0     | 1.76   |
| SanDisk   | SD7TB3Q-256G-1006  | 256 GB | 22      | 642   | 0     | 1.76   |
| SanDisk   | SD7SB6S-128G-1006  | 128 GB | 6       | 740   | 1     | 1.76   |
| Toshiba   | Q300 Pro           | 128 GB | 3       | 641   | 0     | 1.76   |
| OCZ       | VERTEX3            | 120 GB | 100     | 920   | 48    | 1.75   |
| Toshiba   | THNSNH256GMCT      | 256 GB | 7       | 638   | 0     | 1.75   |
| Samsung   | MZ7TD256HAFV-000L9 | 256 GB | 16      | 638   | 0     | 1.75   |
| Kingston  | SV100S232G         | 32 GB  | 5       | 635   | 0     | 1.74   |
| SanDisk   | SD7SB3Q-128G-1006  | 128 GB | 13      | 635   | 0     | 1.74   |
| SanDisk   | SD7SB7S512G1001    | 512 GB | 5       | 633   | 0     | 1.74   |
| Kingston  | SM2280S3240G       | 240 GB | 4       | 633   | 0     | 1.74   |
| Patriot   | Blaze              | 240 GB | 6       | 632   | 0     | 1.73   |
| Micron    | MTFDDAK1T0TBN-1... | 1 TB   | 5       | 631   | 0     | 1.73   |
| OCZ       | VERTEX3            | 64 GB  | 40      | 673   | 1     | 1.73   |
| Crucial   | M4-CT128M4SSD3     | 128 GB | 4       | 628   | 0     | 1.72   |
| Toshiba   | THNSFJ256GCSU      | 256 GB | 30      | 632   | 1     | 1.72   |
| Corsair   | Force LE SSD       | 240 GB | 6       | 628   | 0     | 1.72   |
| SK hynix  | HFS120G32TND-N1A2A | 120 GB | 2       | 626   | 0     | 1.72   |
| Crucial   | CT120M500SSD3      | 120 GB | 8       | 1132  | 9     | 1.72   |
| Intel     | SSDSC2BB960G7      | 960 GB | 2       | 1037  | 1     | 1.71   |
| Mushkin   | MKNSSDCR60GB-7     | 64 GB  | 4       | 670   | 2     | 1.71   |
| Kingston  | SVP200S3240G       | 240 GB | 4       | 624   | 0     | 1.71   |
| SPCC      | SSD                | 480 GB | 11      | 623   | 0     | 1.71   |
| Toshiba   | THNSNF128GCSS      | 128 GB | 20      | 670   | 1     | 1.71   |
| Samsung   | MZHPV512HDGL-000L1 | 512 GB | 2       | 622   | 0     | 1.71   |
| Intel     | SSDSC2KG240G8      | 240 GB | 18      | 622   | 0     | 1.71   |
| SanDisk   | SD8SBBU240G1122    | 240 GB | 5       | 621   | 0     | 1.70   |
| Samsung   | MZ7TD256HAFV-00000 | 256 GB | 4       | 621   | 0     | 1.70   |
| Samsung   | MZ7LN256HMJP-000H1 | 256 GB | 22      | 662   | 1     | 1.70   |
| Samsung   | SSD CM871 M.2 2280 | 128 GB | 4       | 621   | 0     | 1.70   |
| Apple     | SSD SM512E         | 500 GB | 20      | 626   | 1     | 1.70   |
| SK hynix  | HFS512G39MND-3510A | 512 GB | 7       | 620   | 0     | 1.70   |
| Toshiba   | THNSNJ128G8NU      | 128 GB | 13      | 619   | 0     | 1.70   |
| SanDisk   | SD8SN8U1T001122    | 1 TB   | 9       | 618   | 0     | 1.69   |
| Samsung   | MZ7PD256HCGM-000H7 | 256 GB | 35      | 666   | 157   | 1.69   |
| SK hynix  | HFS120G32TND-N1A0A | 120 GB | 2       | 617   | 0     | 1.69   |
| Samsung   | SSD PM830 mSATA    | 256 GB | 4       | 617   | 0     | 1.69   |
| Crucial   | CT256MX100SSD1     | 256 GB | 110     | 665   | 9     | 1.69   |
| KUIJIA    | DK500-64G          | 64 GB  | 5       | 614   | 0     | 1.68   |
| Toshiba   | THNSFJ256GDNU A    | 256 GB | 17      | 614   | 0     | 1.68   |
| Intel     | SSDSC2BP240G4      | 240 GB | 11      | 613   | 0     | 1.68   |
| Samsung   | MZ7TD128HAFV-000L1 | 128 GB | 35      | 633   | 1     | 1.68   |
| Kingston  | SMS200S330G        | 32 GB  | 7       | 671   | 4     | 1.68   |
| Samsung   | MZ7LH960HBJR0D3    | 960 GB | 2       | 613   | 0     | 1.68   |
| Lite-On   | PH3-CE240          | 240 GB | 2       | 628   | 1     | 1.68   |
| SanDisk   | Ultra II           | 960 GB | 46      | 670   | 23    | 1.68   |
| OCZ       | VERTEX4            | 128 GB | 113     | 663   | 1     | 1.68   |
| Kingston  | SHSS37A120G        | 120 GB | 17      | 610   | 0     | 1.67   |
| Kingston  | SKC400S37512G      | 512 GB | 12      | 610   | 0     | 1.67   |
| SanDisk   | SDSSDHII480G       | 480 GB | 25      | 619   | 1     | 1.67   |
| Samsung   | MZNLN512HCJH-000H1 | 512 GB | 7       | 609   | 0     | 1.67   |
| KingSpec  | ACSC2M064S25       | 64 GB  | 3       | 607   | 0     | 1.67   |
| Samsung   | MZMTE256HMHP-00005 | 256 GB | 4       | 607   | 0     | 1.67   |
| Verbatim  | Vi500 S3 240GB SSD | 240 GB | 5       | 607   | 0     | 1.66   |
| Kingston  | SH103S3240G        | 240 GB | 49      | 870   | 123   | 1.66   |
| SanDisk   | SD6SB2M512G1001    | 512 GB | 2       | 605   | 0     | 1.66   |
| Samsung   | SSD 750 EVO        | 250 GB | 148     | 621   | 3     | 1.66   |
| Micron    | M600_MTFDDAT128MBF | 128 GB | 2       | 604   | 0     | 1.66   |
| Micron    | MTFDDAK256MAM-1K1  | 256 GB | 9       | 604   | 0     | 1.66   |
| Samsung   | SSD 850 EVO mSATA  | 500 GB | 35      | 604   | 0     | 1.66   |
| Samsung   | MZNTY128HDHP-000L2 | 128 GB | 2       | 604   | 0     | 1.66   |
| OCZ       | TRION150           | 240 GB | 11      | 603   | 0     | 1.65   |
| Samsung   | MZMTE256HMHP-00000 | 256 GB | 4       | 603   | 0     | 1.65   |
| SanDisk   | SD9TB8W512G1001    | 512 GB | 6       | 602   | 0     | 1.65   |
| SanDisk   | PLUS               | 480 GB | 13      | 602   | 0     | 1.65   |
| Samsung   | MZNLN256HMHQ-000L7 | 256 GB | 2       | 602   | 0     | 1.65   |
| PNY       | CS1311 480GB SSD   | 480 GB | 15      | 602   | 0     | 1.65   |
| SanDisk   | SD7SB6S-256G-1006  | 256 GB | 15      | 602   | 0     | 1.65   |
| Kingston  | SEDC400S37960G     | 960 GB | 2       | 602   | 0     | 1.65   |
| HP        | SSD M700           | 240 GB | 3       | 601   | 0     | 1.65   |
| SPCC      | SSD110             | 120 GB | 9       | 648   | 113   | 1.64   |
| Micron    | MTFDDAK1T0MBF-1... | 1 TB   | 2       | 600   | 0     | 1.64   |
| Samsung   | MZ5PA128HMCD-01000 | 128 GB | 2       | 627   | 1     | 1.64   |
| Corsair   | Neutron SSD        | 64 GB  | 6       | 807   | 3     | 1.64   |
| Micron    | 5200_MTFDDAK1T9TDC | 1.9 TB | 13      | 636   | 1     | 1.64   |
| Toshiba   | TL100              | 240 GB | 15      | 596   | 0     | 1.63   |
| Kingston  | SHSS37A480G        | 480 GB | 25      | 595   | 0     | 1.63   |
| Hoodisk   | SSD                | 64 GB  | 5       | 594   | 0     | 1.63   |
| Intel     | SSDSC2KG960G7      | 960 GB | 2       | 1677  | 3     | 1.63   |
| OCZ       | AGILITY3           | 128 GB | 4       | 1469  | 1     | 1.63   |
| Intel     | SSDSC2BF180A5      | 180 GB | 3       | 1683  | 3     | 1.62   |
| Toshiba   | THNS128GG4BBAA     | 128 GB | 4       | 592   | 0     | 1.62   |
| Samsung   | MZ7TE512HMHP-000L2 | 512 GB | 5       | 591   | 0     | 1.62   |
| WDC       | WDS100T1B0A-00H9H0 | 1 TB   | 21      | 644   | 49    | 1.62   |
| China     | 30GB SATA Flash... | 32 GB  | 2       | 591   | 0     | 1.62   |
| Micron    | C400-MTFDDAT128MAM | 128 GB | 4       | 610   | 517   | 1.62   |
| SanDisk   | SD5SB2-128G-1006E  | 128 GB | 9       | 650   | 1     | 1.62   |
| Toshiba   | THNSNH128GCST      | 128 GB | 14      | 603   | 1     | 1.62   |
| SanDisk   | SD7TB6S256G1001    | 256 GB | 10      | 673   | 101   | 1.62   |
| Intel     | SSDSC2KB960G8      | 960 GB | 46      | 661   | 1     | 1.61   |
| Intel     | SSDSC2CT180A3      | 180 GB | 23      | 767   | 1     | 1.61   |
| Toshiba   | Q300               | 480 GB | 16      | 587   | 0     | 1.61   |
| Goodram   | SSDPR-CX300-480    | 480 GB | 2       | 587   | 0     | 1.61   |
| Micron    | 5200_MTFDDAK480TDC | 480 GB | 6       | 587   | 0     | 1.61   |
| Kingston  | SUV500M8960G       | 960 GB | 2       | 635   | 722   | 1.61   |
| Samsung   | SSD 860 EVO mSATA  | 1 TB   | 10      | 586   | 0     | 1.61   |
| Toshiba   | THNSNJ128GMCU      | 128 GB | 13      | 583   | 0     | 1.60   |
| Samsung   | MZ7TY256HDHP-000L1 | 256 GB | 4       | 1064  | 6     | 1.60   |
| Micron    | M600_MTFDDAK512MBF | 512 GB | 4       | 579   | 0     | 1.59   |
| SanDisk   | SD9SN8W512G1002    | 512 GB | 8       | 675   | 1     | 1.59   |
| SanDisk   | SD7TB3Q-128G-1006  | 128 GB | 6       | 593   | 5     | 1.59   |

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
| SATADOM     | 1      | 2       | 1064  | 0     | 2.92   |
| HPE         | 3      | 9       | 931   | 1     | 2.40   |
| SK          | 2      | 4       | 733   | 0     | 2.01   |
| Corsair     | 44     | 397     | 867   | 89    | 1.85   |
| Radeon      | 1      | 5       | 651   | 0     | 1.78   |
| OCZ         | 76     | 996     | 797   | 26    | 1.75   |
| KUIJIA      | 1      | 5       | 614   | 0     | 1.68   |
| SuperMicro  | 3      | 9       | 685   | 1     | 1.61   |
| Hajaan      | 1      | 2       | 557   | 0     | 1.53   |
| Intel       | 200    | 2066    | 701   | 57    | 1.53   |
| Turbox      | 1      | 2       | 541   | 0     | 1.48   |
| Samsung     | 362    | 15515   | 534   | 11    | 1.40   |
| OWC         | 6      | 44      | 500   | 2     | 1.28   |
| Fury        | 1      | 5       | 467   | 0     | 1.28   |
| MyDigita... | 3      | 13      | 456   | 0     | 1.25   |
| Apple       | 26     | 765     | 466   | 10    | 1.22   |
| DeTech      | 2      | 7       | 486   | 1     | 1.22   |
| Toshiba     | 90     | 864     | 463   | 12    | 1.21   |
| Axiom       | 1      | 2       | 591   | 524   | 1.19   |
| AEGO        | 2      | 8       | 395   | 0     | 1.08   |
| Hyundai     | 4      | 12      | 379   | 0     | 1.04   |
| FCS         | 1      | 2       | 379   | 0     | 1.04   |
| minisforum  | 2      | 6       | 375   | 0     | 1.03   |
| Hoodisk     | 5      | 39      | 337   | 0     | 0.92   |
| HAJAAN      | 1      | 2       | 335   | 0     | 0.92   |
| AFOX        | 1      | 3       | 333   | 0     | 0.91   |
| Palit       | 4      | 10      | 324   | 0     | 0.89   |
| Mushkin     | 24     | 100     | 394   | 66    | 0.88   |
| Ramaxel     | 4      | 12      | 331   | 85    | 0.86   |
| Kingston    | 181    | 9102    | 340   | 20    | 0.82   |
| SanDisk     | 258    | 5216    | 329   | 26    | 0.81   |
| Seagate     | 29     | 185     | 319   | 23    | 0.81   |
| Micron      | 108    | 1144    | 364   | 91    | 0.81   |
| tigo        | 1      | 3       | 286   | 0     | 0.78   |
| Silicon     | 6      | 19      | 286   | 1     | 0.75   |
| HP          | 26     | 244     | 292   | 15    | 0.74   |
| VICK        | 1      | 2       | 268   | 0     | 0.74   |
| Smartbuy    | 13     | 238     | 275   | 1     | 0.73   |
| ADROITLARK  | 1      | 2       | 256   | 0     | 0.70   |
| Pioneer     | 6      | 29      | 256   | 0     | 0.70   |
| SK hynix    | 73     | 1053    | 362   | 95    | 0.69   |
| WDC         | 61     | 3723    | 269   | 6     | 0.69   |
| GALAX       | 3      | 11      | 248   | 0     | 0.68   |
| Crucial     | 79     | 6560    | 292   | 22    | 0.68   |
| Gigabyte    | 7      | 194     | 239   | 0     | 0.66   |
| Kston       | 1      | 6       | 238   | 0     | 0.65   |
| DIERYA      | 1      | 2       | 237   | 0     | 0.65   |
| PNY         | 41     | 866     | 240   | 4     | 0.65   |
| JAMESDONKEY | 2      | 4       | 286   | 2     | 0.64   |
| XPG         | 1      | 4       | 231   | 0     | 0.63   |
| Goodram     | 37     | 705     | 229   | 1     | 0.62   |
| Aoluska     | 1      | 2       | 225   | 0     | 0.62   |
| Patriot     | 39     | 763     | 220   | 11    | 0.59   |
| Faspeed     | 3      | 6       | 212   | 0     | 0.58   |
| Maxtor      | 3      | 29      | 211   | 0     | 0.58   |
| e2e4        | 3      | 10      | 204   | 0     | 0.56   |
| Transcend   | 75     | 775     | 219   | 14    | 0.56   |
| SPCC        | 28     | 1265    | 229   | 49    | 0.55   |
| ADATA       | 98     | 2186    | 235   | 58    | 0.53   |
| Plextor     | 54     | 445     | 205   | 35    | 0.52   |
| UMAX        | 1      | 4       | 185   | 0     | 0.51   |
| HYDRA       | 1      | 3       | 229   | 1     | 0.50   |
| CFD         | 2      | 4       | 181   | 0     | 0.50   |
| Phison      | 23     | 160     | 181   | 1     | 0.50   |
| addlink     | 4      | 12      | 179   | 0     | 0.49   |
| Innodisk    | 12     | 41      | 233   | 175   | 0.49   |
| TCSUNBOW    | 6      | 29      | 176   | 0     | 0.48   |
| Ramsta      | 5      | 13      | 298   | 124   | 0.48   |
| KINGBANK    | 2      | 11      | 169   | 0     | 0.47   |
| JD          | 1      | 2       | 168   | 0     | 0.46   |
| Team        | 50     | 411     | 176   | 3     | 0.46   |
| BIOSTAR     | 3      | 13      | 164   | 0     | 0.45   |
| KingDian    | 16     | 167     | 169   | 54    | 0.44   |
| KingFast    | 8      | 149     | 171   | 22    | 0.44   |
| UNIC2       | 1      | 5       | 160   | 0     | 0.44   |
| XSTAR       | 2      | 5       | 160   | 2     | 0.44   |
| Union Me... | 2      | 20      | 185   | 51    | 0.44   |
| KIOXIA-E... | 3      | 105     | 158   | 0     | 0.43   |
| Reeinno     | 2      | 4       | 154   | 0     | 0.42   |
| Londisk     | 3      | 22      | 153   | 0     | 0.42   |
| ADTEC       | 1      | 2       | 152   | 0     | 0.42   |
| Drevo       | 5      | 33      | 261   | 198   | 0.41   |
| SuperSSpeed | 1      | 3       | 317   | 15    | 0.41   |
| JASTER      | 1      | 3       | 147   | 0     | 0.40   |
| China       | 130    | 2123    | 158   | 19    | 0.40   |
| T-CREATE    | 1      | 2       | 145   | 0     | 0.40   |
| Kingmax     | 5      | 87      | 272   | 255   | 0.40   |
| LDLC        | 12     | 79      | 183   | 37    | 0.39   |
| RZX         | 1      | 2       | 134   | 0     | 0.37   |
| Apacer      | 25     | 630     | 156   | 16    | 0.37   |
| Fujitsu     | 2      | 4       | 407   | 6     | 0.36   |
| Vaseky      | 10     | 31      | 136   | 4     | 0.36   |
| Timetec     | 6      | 16      | 131   | 1     | 0.36   |
| BIWIN       | 8      | 46      | 139   | 90    | 0.35   |
| Gigabyte... | 6      | 87      | 128   | 0     | 0.35   |
| Lexar       | 22     | 291     | 129   | 1     | 0.35   |
| T-FORCE     | 9      | 100     | 130   | 1     | 0.35   |
| Super Ta... | 7      | 20      | 246   | 52    | 0.34   |
| J.ZAO       | 1      | 2       | 123   | 0     | 0.34   |
| Hypertec    | 1      | 2       | 371   | 512   | 0.33   |
| G.Skill     | 1      | 2       | 756   | 510   | 0.33   |
| HGST        | 1      | 7       | 170   | 145   | 0.33   |
| YHJC        | 1      | 2       | 119   | 0     | 0.33   |
| aigo        | 1      | 2       | 117   | 0     | 0.32   |
| ZTC         | 2      | 6       | 116   | 0     | 0.32   |
| GeIL        | 3      | 9       | 116   | 0     | 0.32   |
| Intenso     | 40     | 729     | 121   | 36    | 0.30   |
| Leven       | 9      | 70      | 116   | 2     | 0.30   |
| Hikvision   | 18     | 159     | 114   | 14    | 0.30   |
| GLOWAY      | 8      | 26      | 116   | 40    | 0.30   |
| Pichau      | 1      | 2       | 108   | 0     | 0.30   |
| Zheino      | 16     | 43      | 124   | 4     | 0.30   |
| Advantech   | 3      | 8       | 106   | 0     | 0.29   |
| EXRAM       | 2      | 5       | 153   | 60    | 0.29   |
| Lite-On     | 107    | 708     | 123   | 115   | 0.28   |
| XUM         | 2      | 8       | 103   | 0     | 0.28   |
| Verbatim    | 8      | 153     | 105   | 8     | 0.28   |
| KingSpec    | 43     | 476     | 120   | 38    | 0.28   |
| EYOTA       | 2      | 5       | 105   | 208   | 0.28   |
| Win Memory  | 2      | 6       | 100   | 0     | 0.28   |
| BlueRay     | 1      | 2       | 166   | 1     | 0.27   |
| Dogfish     | 9      | 98      | 107   | 11    | 0.27   |
| Star Drive  | 1      | 6       | 99    | 0     | 0.27   |
| HUGWORLD    | 2      | 5       | 98    | 0     | 0.27   |
| AMD         | 13     | 229     | 125   | 26    | 0.27   |
| SUNEAST     | 5      | 11      | 140   | 16    | 0.27   |
| ZHITAI      | 3      | 17      | 96    | 0     | 0.27   |
| Lenovo      | 7      | 17      | 116   | 1     | 0.26   |
| Ant Esports | 2      | 4       | 97    | 1     | 0.26   |
| VSEVEN      | 1      | 3       | 95    | 0     | 0.26   |
| KOWIN       | 2      | 4       | 94    | 0     | 0.26   |
| V-GeN       | 5      | 10      | 94    | 0     | 0.26   |
| SATAFIRM    | 1      | 5       | 189   | 55    | 0.26   |
| OSCOO       | 4      | 9       | 93    | 10    | 0.25   |
| ASMedia     | 2      | 7       | 91    | 0     | 0.25   |
| Silicon ... | 1      | 2       | 91    | 0     | 0.25   |
| Foxline     | 8      | 37      | 91    | 0     | 0.25   |
| Kingchuxing | 8      | 42      | 97    | 38    | 0.25   |
| Colorful    | 9      | 45      | 102   | 29    | 0.25   |
| GS Nanotech | 1      | 3       | 90    | 0     | 0.25   |
| VisionTek   | 1      | 2       | 88    | 0     | 0.24   |
| FORESEE     | 5      | 97      | 88    | 0     | 0.24   |
| Integral    | 5      | 36      | 88    | 0     | 0.24   |
| Acer        | 5      | 26      | 88    | 1     | 0.24   |
| VISIPRO     | 3      | 10      | 88    | 2     | 0.24   |
| Solid       | 2      | 9       | 158   | 1     | 0.24   |
| ShanDianZhe | 3      | 9       | 87    | 0     | 0.24   |
| NTC         | 1      | 2       | 87    | 0     | 0.24   |
| 2-Power     | 3      | 9       | 86    | 1     | 0.24   |
| EVM         | 2      | 8       | 86    | 0     | 0.24   |
| INNOVATI... | 14     | 46      | 88    | 1     | 0.24   |
| EMTEC       | 6      | 90      | 88    | 23    | 0.24   |
| BHT         | 8      | 42      | 85    | 0     | 0.23   |
| TEXTORM     | 3      | 12      | 84    | 3     | 0.23   |
| QUMO        | 9      | 30      | 94    | 2     | 0.23   |
| Inland      | 2      | 9       | 82    | 0     | 0.23   |
| ACCLAMATOR  | 1      | 2       | 77    | 0     | 0.21   |
| AGI         | 9      | 35      | 94    | 2     | 0.21   |
| KODAK       | 5      | 10      | 75    | 0     | 0.21   |
| TAMMUZ      | 4      | 10      | 74    | 0     | 0.20   |
| Neo Forza   | 5      | 14      | 114   | 445   | 0.20   |
| Kross El... | 1      | 2       | 86    | 1     | 0.20   |
| ASENNO      | 3      | 7       | 124   | 4     | 0.20   |
| BAITITON    | 10     | 33      | 92    | 5     | 0.20   |
| Netac       | 17     | 448     | 79    | 12    | 0.19   |
| KLEVV       | 5      | 12      | 68    | 256   | 0.18   |
| GOFATOO     | 2      | 4       | 65    | 0     | 0.18   |
| Fanxiang    | 13     | 118     | 69    | 2     | 0.18   |
| XrayDisk    | 14     | 138     | 73    | 24    | 0.18   |
| Indilinx    | 4      | 9       | 63    | 0     | 0.17   |
| TrekStor    | 1      | 2       | 122   | 78    | 0.17   |
| Teclast     | 10     | 61      | 69    | 16    | 0.17   |
| Bestoss     | 1      | 2       | 61    | 0     | 0.17   |
| LuminouTek  | 3      | 6       | 61    | 0     | 0.17   |
| MidasForce  | 4      | 17      | 61    | 0     | 0.17   |
| TwinMOS     | 1      | 2       | 87    | 1     | 0.17   |
| Platinet    | 1      | 3       | 61    | 30    | 0.17   |
| TEKET       | 1      | 2       | 59    | 0     | 0.16   |
| WALRAM      | 9      | 53      | 65    | 43    | 0.16   |
| KUU         | 2      | 6       | 56    | 2     | 0.15   |
| Wibtek      | 5      | 33      | 55    | 14    | 0.15   |
| Valuetech   | 4      | 13      | 60    | 1     | 0.15   |
| Avant       | 1      | 2       | 823   | 508   | 0.15   |
| SSSTC       | 3      | 28      | 126   | 939   | 0.15   |
| QUANXING    | 1      | 3       | 52    | 0     | 0.14   |
| MSI         | 4      | 11      | 51    | 0     | 0.14   |
| S3+         | 4      | 9       | 49    | 0     | 0.13   |
| Anobit      | 1      | 2       | 48    | 1     | 0.13   |
| RCESSD      | 1      | 2       | 46    | 0     | 0.13   |
| AirDisk     | 2      | 19      | 46    | 0     | 0.13   |
| TGT         | 2      | 4       | 45    | 0     | 0.13   |
| KOOTION     | 2      | 7       | 54    | 3     | 0.12   |
| RX7         | 1      | 2       | 43    | 0     | 0.12   |
| ExeGate     | 4      | 9       | 42    | 0     | 0.12   |
| Rogueware   | 1      | 4       | 41    | 0     | 0.11   |
| Qumo        | 2      | 7       | 124   | 146   | 0.11   |
| SCY         | 2      | 12      | 41    | 0     | 0.11   |
| Azerty      | 6      | 22      | 46    | 2     | 0.11   |
| ORTIAL      | 2      | 17      | 77    | 1     | 0.11   |
| SunWind     | 1      | 2       | 40    | 0     | 0.11   |
| SNR         | 2      | 7       | 39    | 0     | 0.11   |

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
| Intel     | MEMPEK1J016GAD     | 16 GB  | 3       | 4047  | 0     | 11.09  |
| Intel     | H10 HBRPEKNX010... | 16 GB  | 2       | 3799  | 0     | 10.41  |
| Intel     | H10 HBRPEKNX020... | 32 GB  | 3       | 3588  | 0     | 9.83   |
| Intel     | H10 HBRPEKNX020... | 32 GB  | 15      | 3084  | 0     | 8.45   |
| Samsung   | MS1PC5ED3ORA3.2T   | 3.2 TB | 5       | 1682  | 0     | 4.61   |
| Intel     | SSDPEDMW400G4      | 400 GB | 8       | 1535  | 0     | 4.21   |
| Corsair   | Force MP500        | 480 GB | 2       | 1462  | 0     | 4.01   |
| Intel     | SSDPEDMD400G4      | 400 GB | 4       | 1389  | 0     | 3.81   |
| Intel     | SSDPE2MX450G7      | 450 GB | 9       | 1385  | 0     | 3.80   |
| Intel     | SSDPEDMW012T4      | 1.2 TB | 5       | 1371  | 0     | 3.76   |
| Toshiba   | KXD51RUE1T92       | 1.9 TB | 2       | 1166  | 0     | 3.20   |
| Samsung   | SSD 950 PRO        | 256 GB | 29      | 1153  | 0     | 3.16   |
| Patriot   | Hellfire M2        | 480 GB | 2       | 1152  | 0     | 3.16   |
| Samsung   | MZVPV512HDGL-00000 | 512 GB | 19      | 951   | 0     | 2.61   |
| ZOTAC     | ZTSSDPG3-480G-GE   | 480 GB | 2       | 919   | 0     | 2.52   |
| Samsung   | MZVPV256HDGL-000L7 | 256 GB | 2       | 909   | 0     | 2.49   |
| Intel     | SSDPEKKF256G7H     | 256 GB | 44      | 917   | 43    | 2.45   |
| Toshiba   | KXG50PNV1T02 NVMe  | 1 TB   | 7       | 866   | 0     | 2.38   |
| Toshiba   | RD400              | 1 TB   | 3       | 855   | 0     | 2.34   |
| Samsung   | SSD 983 DCT 1.92TB | 1.9 TB | 2       | 850   | 0     | 2.33   |
| Samsung   | SSD 950 PRO        | 512 GB | 60      | 852   | 7     | 2.32   |
| Samsung   | MZPLL1T6HAJQ-00005 | 1.6 TB | 2       | 836   | 0     | 2.29   |
| Intel     | SSDPED1D480GA      | 480 GB | 5       | 836   | 0     | 2.29   |
| Dell      | Express Flash N... | 6.4 TB | 2       | 829   | 0     | 2.27   |
| Samsung   | SM951 NVMe         | 256 GB | 3       | 825   | 0     | 2.26   |
| WDC       | WDS512G1X0C-00ENX0 | 512 GB | 15      | 814   | 0     | 2.23   |
| WDC       | CL SN720 SDAQNT... | 512 GB | 11      | 805   | 0     | 2.21   |
| Mushkin   | MKNSSDPL1TB-D8     | 1 TB   | 2       | 801   | 0     | 2.19   |
| Intel     | SSDPEKKF010T7      | 1 TB   | 3       | 1155  | 25    | 2.19   |
| Toshiba   | THNSN5512GPU7 NVMe | 512 GB | 9       | 792   | 0     | 2.17   |
| Samsung   | MZQLB960HAJR-00007 | 960 GB | 17      | 791   | 0     | 2.17   |
| Intel     | SSDPEKKF512G7H     | 512 GB | 10      | 829   | 26    | 2.06   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 3       | 727   | 0     | 1.99   |
| Toshiba   | RD400              | 256 GB | 7       | 719   | 0     | 1.97   |
| Silico... | Asgard AN3 2TNV... | 2 TB   | 14      | 718   | 0     | 1.97   |
| Samsung   | MZ1LB960HAJQ-000MV | 960 GB | 2       | 717   | 0     | 1.97   |
| Corsair   | Force MP500        | 240 GB | 18      | 765   | 1     | 1.94   |
| Samsung   | PM951 NVMe         | 1 TB   | 7       | 697   | 0     | 1.91   |
| Micron    | 7300_MTFDHBE960TDF | 960 GB | 6       | 692   | 0     | 1.90   |
| Corsair   | Force MP500        | 120 GB | 16      | 688   | 0     | 1.89   |
| Intel     | SSDPEDKE020T7      | 2 TB   | 3       | 684   | 0     | 1.88   |
| ADATA     | SX8000NP           | 128 GB | 2       | 680   | 0     | 1.86   |
| Plextor   | PX-512M9PeG        | 512 GB | 5       | 677   | 0     | 1.86   |
| Samsung   | MZWLL1T6HAJQ-00005 | 1.6 TB | 4       | 673   | 0     | 1.85   |
| Intel     | SSDPEKKW256G7      | 256 GB | 81      | 824   | 28    | 1.84   |
| Intel     | SSDPEKKW512G7      | 512 GB | 30      | 871   | 100   | 1.84   |
| Kingston  | RBUSNS8154P3102... | 1 TB   | 2       | 667   | 0     | 1.83   |
| SanDisk   | A400 NVMe          | 256 GB | 3       | 658   | 0     | 1.80   |
| Asgard    | AN3 2TNVMe-M.2-80  | 2 TB   | 2       | 654   | 0     | 1.79   |
| Toshiba   | KXG50PNV2T04 NVMe  | 2 TB   | 4       | 653   | 0     | 1.79   |
| WDC       | WUS4BB076D7P3E3    | 7.6 TB | 6       | 645   | 0     | 1.77   |
| Intel     | SSDPELKX010T8      | 1 TB   | 5       | 643   | 0     | 1.76   |
| Intel     | SSDPE21D480GA      | 480 GB | 6       | 643   | 0     | 1.76   |
| Kingston  | SA1000M8960G       | 960 GB | 2       | 640   | 0     | 1.75   |
| KIOXIA    | KXG6APNV2T04       | 2 TB   | 2       | 639   | 0     | 1.75   |
| KIOXIA    | KXG50PNV2T04       | 2 TB   | 3       | 636   | 0     | 1.74   |
| Samsung   | MZVPV256HDGL-000H1 | 256 GB | 10      | 636   | 0     | 1.74   |
| Samsung   | MZVPV256HDGL-00000 | 256 GB | 18      | 650   | 15    | 1.70   |
| Samsung   | SM951 NVMe         | 512 GB | 3       | 607   | 0     | 1.66   |
| Samsung   | MZVLB1T0HALR-000H2 | 1 TB   | 4       | 605   | 0     | 1.66   |
| Gigabyte  | GP-ASM2NE2256GTTDR | 256 GB | 3       | 597   | 0     | 1.64   |
| PNY       | CS3030 250GB SSD   | 250 GB | 31      | 596   | 0     | 1.63   |
| Intel     | SSDPEKKF360G7H     | 360 GB | 11      | 660   | 17    | 1.63   |
| Samsung   | MZQLB960HAJR-00003 | 960 GB | 4       | 588   | 0     | 1.61   |
| Kingston  | SKC1000240G        | 240 GB | 4       | 585   | 0     | 1.61   |
| Toshiba   | THNSN5512GPUK NVMe | 512 GB | 50      | 598   | 2     | 1.60   |
| Team      | TM8FP4512G         | 512 GB | 3       | 582   | 0     | 1.59   |
| Phison    | APS-SE20G-256      | 256 GB | 2       | 580   | 0     | 1.59   |
| Toshiba   | THNSN5256GPUK NVMe | 256 GB | 32      | 580   | 0     | 1.59   |
| Intel     | SSDPED1D280GA      | 280 GB | 8       | 577   | 0     | 1.58   |
| Hikvision | HS-SSD-C2000       | 1 TB   | 3       | 572   | 0     | 1.57   |
| Samsung   | MZVPV128HDGM-00000 | 128 GB | 14      | 566   | 0     | 1.55   |
| Intel     | SSDPEKKW128G7      | 128 GB | 19      | 910   | 1     | 1.55   |
| Toshiba   | KBG40ZPZ1T02 ME... | 1 TB   | 2       | 555   | 0     | 1.52   |
| Toshiba   | THNSF5256GPUK      | 256 GB | 15      | 555   | 0     | 1.52   |
| Samsung   | MZVKV512HAJH-000L1 | 512 GB | 17      | 552   | 0     | 1.51   |
| WDC       | WDS256G1X0C-00ENX0 | 256 GB | 27      | 542   | 0     | 1.49   |
| Toshiba   | THNSN51T02DUK NVMe | 1 TB   | 16      | 616   | 64    | 1.47   |
| Intel     | SSDPEKNW020T9      | 2 TB   | 4       | 535   | 0     | 1.47   |
| ADATA     | SX8200NP           | 480 GB | 13      | 534   | 0     | 1.47   |
| Hikvision | HS-SSD-E2000 512G  | 512 GB | 2       | 522   | 0     | 1.43   |
| Intel     | SSDPEKKW010T7      | 1 TB   | 6       | 1048  | 173   | 1.42   |
| Phison    | ESO256GMFCH-E3C-2  | 256 GB | 3       | 517   | 0     | 1.42   |
| Samsung   | PM951 NVMe         | 512 GB | 19      | 515   | 0     | 1.41   |
| Toshiba   | KXG50ZNV512G NVMe  | 512 GB | 86      | 513   | 0     | 1.41   |
| Toshiba   | KXG5AZNV1T02       | 1 TB   | 6       | 502   | 0     | 1.38   |
| Toshiba   | KXG50ZNV256G NVMe  | 256 GB | 60      | 499   | 0     | 1.37   |
| Lexar     | SSD                | 256 GB | 9       | 497   | 0     | 1.36   |
| Smartbuy  | m.2 PS5013-2280T   | 512 GB | 2       | 496   | 0     | 1.36   |
| Toshiba   | THNSN5256GPU7      | 256 GB | 24      | 495   | 0     | 1.36   |
| Samsung   | MZVKW1T0HMLH-000L7 | 1 TB   | 2       | 495   | 0     | 1.36   |
| Intel     | SSDPEKKW020T8      | 2 TB   | 5       | 492   | 0     | 1.35   |
| Intel     | MEMPEK1W016GA      | 16 GB  | 17      | 491   | 0     | 1.35   |
| Gigabyte  | GP-ASM2NE2512GTTDR | 512 GB | 2       | 489   | 0     | 1.34   |
| Corsair   | Force MP600        | 2 TB   | 34      | 489   | 0     | 1.34   |
| Intel     | SSDPEKKF256G7L     | 256 GB | 65      | 571   | 57    | 1.34   |
| Samsung   | MZVL2256HCHQ-00BL7 | 256 GB | 2       | 931   | 14    | 1.33   |
| Phison    | Sabrent Rocket Q   | 1 TB   | 162     | 488   | 7     | 1.32   |
| Intel     | MEMPEK1W032GA      | 32 GB  | 6       | 479   | 0     | 1.31   |
| Reletech  | P400 M.2 Pro Q2... | 2 TB   | 2       | 477   | 0     | 1.31   |
| Samsung   | MZVPV512HDGL-000H1 | 512 GB | 6       | 476   | 0     | 1.30   |
| Samsung   | MZVKW1T0HMLH-00000 | 1 TB   | 4       | 475   | 0     | 1.30   |
| Asgard    | AN3 1TNVMe-M.2-80  | 1 TB   | 2       | 472   | 0     | 1.30   |
| Samsung   | MZVLV128HCGR-00000 | 128 GB | 4       | 466   | 0     | 1.28   |
| Samsung   | MZQLB3T8HALS-00007 | 3.8 TB | 18      | 465   | 0     | 1.28   |
| Samsung   | PM951 NVMe         | 256 GB | 24      | 458   | 0     | 1.26   |
| Kingston  | SKC1000480G        | 480 GB | 4       | 456   | 0     | 1.25   |
| T-FORCE   | TM8FP5512G         | 512 GB | 2       | 453   | 0     | 1.24   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 3       | 453   | 0     | 1.24   |
| Kingston  | SKC2000M8250G      | 250 GB | 7       | 450   | 0     | 1.23   |
| Phison    | APS-SE20Q-1T       | 1 TB   | 3       | 446   | 0     | 1.22   |
| Toshiba   | THNSN51T02DUK      | 1 TB   | 3       | 446   | 0     | 1.22   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 3       | 443   | 0     | 1.21   |
| Silico... | GSDFN512TS3F1OGCX  | 512 GB | 2       | 443   | 0     | 1.21   |
| Phison    | Neutron NX500      | 800 GB | 2       | 442   | 0     | 1.21   |
| Toshiba   | KXG50ZNV1T02       | 1 TB   | 9       | 442   | 0     | 1.21   |
| Toshiba   | KXG50ZNV1T02 NVMe  | 1 TB   | 33      | 442   | 0     | 1.21   |
| Toshiba   | THNSF5512GPUK      | 512 GB | 24      | 440   | 0     | 1.21   |
| HP        | SSD EX900 Pro      | 256 GB | 2       | 438   | 0     | 1.20   |
| KIOXIA    | KXG6AZNV256G       | 256 GB | 2       | 435   | 0     | 1.19   |
| Intel     | HBRPEKNL0202AHO    | 32 GB  | 2       | 430   | 0     | 1.18   |
| Samsung   | MZVPV128HDGM-000H1 | 128 GB | 2       | 428   | 0     | 1.18   |
| Intel     | HBRPEKNL0202AH     | 512 GB | 2       | 428   | 0     | 1.17   |
| Toshiba   | KXG60ZNV1T02 NVMe  | 1 TB   | 25      | 428   | 0     | 1.17   |
| Toshiba   | KBG20ZMS256G NVMe  | 256 GB | 3       | 426   | 0     | 1.17   |
| HP        | SSD EX950          | 1 TB   | 27      | 423   | 0     | 1.16   |
| PNY       | CS3030 1000GB SSD  | 1 TB   | 7       | 422   | 0     | 1.16   |
| Intel     | MEMPEK1J016GAH     | 16 GB  | 7       | 418   | 0     | 1.15   |
| Intel     | SSDPED1K375GA      | 375 GB | 4       | 417   | 0     | 1.14   |
| HP        | SSD EX920          | 512 GB | 20      | 416   | 0     | 1.14   |
| Samsung   | MZVLV256HCHP-00000 | 256 GB | 19      | 415   | 0     | 1.14   |
| SSSTC     | CL1-3D256          | 256 GB | 4       | 414   | 0     | 1.14   |
| KIOXIA    | KXG60PNV1T02 NVMe  | 1 TB   | 4       | 412   | 0     | 1.13   |
| Toshiba   | KXG5AZNV256G NV... | 256 GB | 2       | 412   | 0     | 1.13   |
| Samsung   | PM981 NVMe         | 2 TB   | 3       | 411   | 0     | 1.13   |
| Hikvision | HS-SSD-E2000 2048G | 2 TB   | 2       | 410   | 0     | 1.12   |
| WDC       | WDS500G2X0C-00L350 | 500 GB | 34      | 402   | 0     | 1.10   |
| Corsair   | Force MP600        | 500 GB | 28      | 401   | 0     | 1.10   |
| Mushkin   | MKNSSDHL250GB-D8   | 250 GB | 6       | 417   | 168   | 1.10   |
| Patriot   | Hellfire M2        | 240 GB | 3       | 400   | 0     | 1.10   |
| Toshiba   | KXG60PNV512G NVMe  | 512 GB | 2       | 396   | 0     | 1.09   |
| Seagate   | FireCuda 510 SS... | 1 TB   | 15      | 392   | 0     | 1.07   |
| Phison    | ESR512GTLCG-EAC-4  | 512 GB | 8       | 390   | 0     | 1.07   |
| SanDisk   | A400 SD9PN9U-25... | 256 GB | 3       | 386   | 0     | 1.06   |
| Kingston  | SNVS2000GB         | 2 TB   | 4       | 385   | 0     | 1.06   |
| WDC       | WDS100T3XHC-00SJG0 | 1 TB   | 24      | 385   | 0     | 1.06   |
| Intel     | SSDPEKNW020T8      | 2 TB   | 96      | 394   | 1     | 1.06   |
| Intel     | SSDPEK1W060GA      | 64 GB  | 4       | 383   | 0     | 1.05   |
| Phison    | E12-512G-PHISON... | 512 GB | 7       | 382   | 0     | 1.05   |
| Samsung   | Portable SSD T7... | 1 TB   | 2       | 382   | 0     | 1.05   |
| WDC       | WDS100T2X0C-00L350 | 1 TB   | 16      | 378   | 0     | 1.04   |
| Samsung   | MZVLV256HCHP-000L2 | 256 GB | 15      | 376   | 0     | 1.03   |
| HP        | SSD EX920          | 256 GB | 3       | 447   | 1     | 1.03   |
| Phison    | M.2 PCIE G3x4 NVMe | 1 TB   | 4       | 373   | 0     | 1.02   |
| Toshiba   | THNSN5128GPU7      | 128 GB | 14      | 373   | 0     | 1.02   |
| Plextor   | PX-256M9PeY        | 256 GB | 5       | 373   | 0     | 1.02   |
| SanDisk   | A400 NVMe          | 512 GB | 3       | 370   | 0     | 1.01   |
| Crucial   | CT2000P1SSD8       | 2 TB   | 7       | 367   | 0     | 1.01   |
| Phison    | Metabox Perform... | 2 TB   | 6       | 367   | 0     | 1.01   |
| Lite-On   | CX2-8B256-Q11 NVMe | 256 GB | 10      | 365   | 0     | 1.00   |
| Goodram   | IRP-SSDPR-P44A-... | 2 TB   | 2       | 365   | 0     | 1.00   |
| Intel     | SSDPEKKF512G7L     | 512 GB | 9       | 466   | 174   | 1.00   |
| SK hynix  | PC601A NVMe        | 1 TB   | 9       | 364   | 0     | 1.00   |
| PNY       | CS3030 2TB SSD     | 2 TB   | 30      | 363   | 0     | 1.00   |
| Toshiba   | THNSN5512GPUK      | 512 GB | 18      | 361   | 0     | 0.99   |
| Toshiba   | KXG60ZNV512G NVMe  | 512 GB | 61      | 359   | 0     | 0.98   |
| Intel     | SSDPE2MX012T7      | 1.2 TB | 4       | 358   | 0     | 0.98   |
| Lite-On   | CL1-3D128-Q11 NVMe | 128 GB | 5       | 358   | 0     | 0.98   |
| WDC       | WDS250G2X0C-00L350 | 250 GB | 28      | 357   | 0     | 0.98   |
| Intel     | MEMPEK1J016GA      | 16 GB  | 19      | 386   | 55    | 0.98   |
| Gigabyte  | GP-ASM2NE6100TTTD  | 1 TB   | 15      | 354   | 0     | 0.97   |
| WDC       | WDS200T3XHC-00SJG0 | 2 TB   | 4       | 353   | 0     | 0.97   |
| Corsair   | Force MP510        | 960 GB | 50      | 353   | 0     | 0.97   |
| ADATA     | SX8200NP           | 240 GB | 8       | 368   | 15    | 0.96   |
| Mushkin   | MKNSSDPL500GB-D8   | 500 GB | 3       | 348   | 0     | 0.96   |
| Intel     | SSDPEKKF010T8      | 1 TB   | 6       | 347   | 0     | 0.95   |
| Phison    | Sabrent Rocket 4.0 | 2 TB   | 26      | 346   | 0     | 0.95   |
| Toshiba   | RD400              | 512 GB | 4       | 345   | 0     | 0.95   |
| Silico... | NVME SSD           | 1 TB   | 3       | 343   | 0     | 0.94   |
| EMTEC     | X300               | 256 GB | 3       | 343   | 0     | 0.94   |
| Samsung   | MZ1LB960HAJQ-00007 | 960 GB | 7       | 342   | 0     | 0.94   |
| Toshiba   | KXG50ZNV512G       | 512 GB | 68      | 341   | 0     | 0.94   |
| Intel     | SSDPEK1W120GA      | 118 GB | 2       | 341   | 0     | 0.94   |
| Intel     | H10 HBRPEKNX010... | 256 GB | 5       | 341   | 0     | 0.93   |
| Corsair   | Force MP510 1.9TB  | 1.9 TB | 18      | 339   | 0     | 0.93   |
| Corsair   | Force MP600        | 1 TB   | 113     | 339   | 0     | 0.93   |
| Intel     | HBRPEKNX0203A      | 1 TB   | 4       | 338   | 0     | 0.93   |
| WDC       | WDS500G1B0C-00S6U0 | 500 GB | 27      | 351   | 1     | 0.92   |
| Plextor   | PX-256M8PeGN       | 256 GB | 4       | 336   | 0     | 0.92   |
| SK hynix  | PC601 HFS256GD9... | 256 GB | 9       | 335   | 0     | 0.92   |
| Toshiba   | THNSN5256GPUK      | 256 GB | 13      | 418   | 11    | 0.92   |
| Micron    | 9300_MTFDHAL15T... | 15.... | 3       | 333   | 0     | 0.91   |
| Corsair   | Force MP300        | 240 GB | 5       | 332   | 0     | 0.91   |
| Seagate   | BarraCuda Q5 ZP... | 2 TB   | 3       | 331   | 0     | 0.91   |
| KIOXIA... | SSD                | 250 GB | 3       | 329   | 0     | 0.90   |
| Intel     | HBRPEKNX0203AHO    | 32 GB  | 24      | 328   | 0     | 0.90   |
| XPG       | GAMMIX S11         | 480 GB | 10      | 398   | 101   | 0.90   |
| Toshiba   | THNSN5512GPU7      | 512 GB | 16      | 327   | 0     | 0.90   |
| HP        | SSD EX920          | 1 TB   | 19      | 327   | 0     | 0.90   |
| Silico... | Longline SSD       | 512 GB | 2       | 327   | 0     | 0.90   |
| Toshiba   | KBG40ZPZ256G ME... | 256 GB | 6       | 326   | 0     | 0.90   |
| Intel     | SSDPEKKW256G8      | 256 GB | 67      | 326   | 0     | 0.89   |
| Toshiba   | KXG5AZNV512G NV... | 512 GB | 2       | 324   | 0     | 0.89   |
| Samsung   | MZVKW512HMJP-000H1 | 512 GB | 23      | 329   | 1     | 0.89   |
| Samsung   | PM981a NVMe SED    | 512 GB | 2       | 321   | 0     | 0.88   |
| Mushkin   | MKNSSDPE500GB-D8   | 500 GB | 2       | 319   | 0     | 0.88   |
| Intel     | SSDPEKKW512G8      | 512 GB | 27      | 319   | 0     | 0.88   |
| SPCC      | M.2 PCIE SSD       | 1 TB   | 8       | 316   | 0     | 0.87   |
| Seagate   | FireCuda 510 SS... | 1 TB   | 8       | 314   | 0     | 0.86   |
| Aura      | Pro X2             | 960 GB | 14      | 312   | 0     | 0.86   |
| China     | NVME SSD           | 1 TB   | 6       | 312   | 0     | 0.86   |
| ADATA     | SX6000NP           | 256 GB | 5       | 339   | 3     | 0.86   |
| WDC       | WDS250G1B0C-00S6U0 | 250 GB | 17      | 311   | 0     | 0.85   |
| SK hynix  | PC601 NVMe         | 1 TB   | 12      | 411   | 1     | 0.85   |
| Phison    | Sabrent            | 1 TB   | 239     | 308   | 0     | 0.85   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 19      | 307   | 0     | 0.84   |
| Intel     | HBRPEKNX0203AH     | 1 TB   | 25      | 307   | 0     | 0.84   |
| Kingston  | SKC2000M8500G      | 500 GB | 6       | 406   | 168   | 0.84   |
| Phison    | Viper M.2 VPN100   | 1 TB   | 37      | 305   | 0     | 0.84   |
| Goodram   | SSDPR-PX500-01T-80 | 1 TB   | 7       | 304   | 0     | 0.83   |
| Gigabyte  | GP-ASM2NE6200TTTD  | 2 TB   | 11      | 304   | 0     | 0.83   |
| XrayDisk  | 256GB              | 256 GB | 8       | 304   | 0     | 0.83   |
| SK hynix  | PC601A NVMe        | 512 GB | 4       | 303   | 0     | 0.83   |
| Samsung   | MZ1LW960HMJP-00003 | 960 GB | 2       | 303   | 0     | 0.83   |
| SK hynix  | PC601 NVMe         | 256 GB | 18      | 302   | 0     | 0.83   |
| addlink   | M.2 PCIE G3x4 NVMe | 1 TB   | 34      | 302   | 0     | 0.83   |
| SSSTC     | CL1-4D256-D22      | 256 GB | 5       | 302   | 0     | 0.83   |
| WDC       | WDBRPG5000ANC-WRSN | 500 GB | 29      | 300   | 0     | 0.82   |
| Plextor   | PX-256M9PeG        | 256 GB | 6       | 299   | 0     | 0.82   |
| Seagate   | BarraCuda 510 S... | 500 GB | 5       | 299   | 0     | 0.82   |
| Intel     | HBRPEKNX0202ACO    | 32 GB  | 4       | 299   | 0     | 0.82   |
| Phison    | E12-256G-PHISON... | 256 GB | 4       | 298   | 0     | 0.82   |
| Intel     | SSDPEK1W120GAH     | 118 GB | 2       | 296   | 0     | 0.81   |
| Toshiba   | KXG60ZNV1T02       | 1 TB   | 28      | 295   | 0     | 0.81   |
| Phison    | Sabrent Rocket 4.0 | 1 TB   | 119     | 293   | 0     | 0.80   |
| Micron    | 7300_MTFDHBE6T4TDG | 6.4 TB | 2       | 293   | 0     | 0.80   |
| Corsair   | MP400              | 4 TB   | 8       | 291   | 0     | 0.80   |
| Dell      | Express Flash N... | 3.2 TB | 4       | 291   | 0     | 0.80   |
| Plextor   | PX-512M9PeGN       | 512 GB | 2       | 290   | 0     | 0.80   |
| Corsair   | MP600 PRO XT       | 2 TB   | 7       | 290   | 0     | 0.80   |
| Intel     | HBRPEKNX0203AO     | 32 GB  | 5       | 290   | 0     | 0.79   |
| SPCC      | M.2 PCIE SSD       | 512 GB | 6       | 301   | 169   | 0.79   |
| KIOXIA    | KXG60PNV2T04 NVMe  | 2 TB   | 16      | 289   | 0     | 0.79   |
| Crucial   | CT1000P1SSD8       | 1 TB   | 318     | 300   | 24    | 0.79   |
| Toshiba   | KXG5AZNV256G       | 256 GB | 28      | 288   | 0     | 0.79   |
| Intel     | SSDPEKKW256G8L     | 256 GB | 9       | 288   | 0     | 0.79   |
| XPG       | GAMMIX S50         | 1 TB   | 11      | 287   | 0     | 0.79   |
| Plextor   | PX-512M9PGN +      | 512 GB | 3       | 287   | 0     | 0.79   |
| Transcend | TS1TMTE220S        | 1 TB   | 20      | 292   | 51    | 0.79   |
| ADATA     | SX6000NP           | 128 GB | 9       | 332   | 130   | 0.78   |
| KIOXIA... | SSD                | 1 TB   | 9       | 285   | 0     | 0.78   |
| Toshiba   | KBG40ZNS512G NVMe  | 512 GB | 20      | 285   | 0     | 0.78   |
| Samsung   | MZQLB1T9HAJR-00007 | 1.9 TB | 15      | 284   | 0     | 0.78   |
| Intel     | HBRPEKNX0202AHO    | 32 GB  | 74      | 295   | 6     | 0.78   |
| Gigaby... | GP-ASM2NE6100TTTD  | 1 TB   | 11      | 283   | 0     | 0.78   |
| Samsung   | MZVLV512HCJH-000H1 | 512 GB | 5       | 283   | 0     | 0.78   |
| Micron    | 7300_MTFDHBG3T8TDF | 3.8 TB | 3       | 281   | 0     | 0.77   |
| ADATA     | SX8200PNP          | 1 TB   | 187     | 296   | 33    | 0.77   |
| KIOXIA    | KBG30ZMV128G       | 128 GB | 4       | 281   | 0     | 0.77   |
| Corsair   | Force MP510        | 480 GB | 57      | 281   | 0     | 0.77   |
| Apacer    | AS2280P4           | 480 GB | 5       | 280   | 0     | 0.77   |
| Intel     | MEMPEK1W016GAL     | 16 GB  | 2       | 279   | 0     | 0.77   |
| Samsung   | SM961 NVMe         | 1 TB   | 3       | 350   | 6     | 0.77   |
| GLOWAY    | YCT512NVMe-M.2-... | 512 GB | 2       | 278   | 0     | 0.76   |
| Samsung   | MZVKW512HMJP-00000 | 512 GB | 12      | 335   | 3     | 0.76   |
| Silico... | M Series NVMe S... | 256 GB | 4       | 277   | 0     | 0.76   |
| Intel     | SSDPEKNW010T8      | 1 TB   | 332     | 278   | 4     | 0.76   |
| SanDisk   | WD_BLACK SN850     | 2 TB   | 3       | 276   | 0     | 0.76   |
| Seagate   | FireCuda 510 SS... | 500 GB | 2       | 276   | 0     | 0.76   |
| Goodram   | IR-SSDPR-P34B-2... | 256 GB | 4       | 276   | 0     | 0.76   |
| Toshiba   | KXG5AZNV512G       | 512 GB | 24      | 275   | 0     | 0.76   |
| PNY       | CS3030 1TB SSD     | 1 TB   | 27      | 292   | 11    | 0.75   |
| PNY       | CS2140 2TB SSD     | 2 TB   | 2       | 274   | 0     | 0.75   |
| Samsung   | MZ1LB1T9HALS-00007 | 1.9 TB | 2       | 273   | 0     | 0.75   |
| Toshiba   | RC500              | 500 GB | 10      | 630   | 203   | 0.75   |
| UMIS      | RPITJ512PED2OWX    | 512 GB | 4       | 595   | 253   | 0.74   |
| WDC       | WDBA3V0010BNC-WRSN | 1 TB   | 14      | 270   | 0     | 0.74   |
| Transcend | TS512GMTE110S      | 512 GB | 15      | 270   | 0     | 0.74   |
| Lite-On   | CA1-8D256-HP       | 256 GB | 2       | 269   | 0     | 0.74   |
| Toshiba   | KXG50ZNV256G       | 256 GB | 57      | 269   | 0     | 0.74   |
| PNY       | CS1031 2TB SSD     | 2 TB   | 6       | 268   | 0     | 0.74   |
| J.ZAO     | 5 SERIES 512GB SSD | 512 GB | 2       | 267   | 0     | 0.73   |
| Intel     | HBRPEKNX0202AH     | 512 GB | 79      | 266   | 0     | 0.73   |
| KIOXIA    | KXG60ZNV512G NVMe  | 512 GB | 63      | 265   | 0     | 0.73   |
| Corsair   | Force MP300        | 480 GB | 4       | 265   | 0     | 0.73   |
| SSSTC     | CL1-8D128          | 128 GB | 2       | 265   | 0     | 0.73   |
| SK hynix  | PC601 HFS512GD9... | 512 GB | 27      | 264   | 0     | 0.73   |
| KIOXIA    | KXG60ZNV1T02 NVMe  | 1 TB   | 73      | 264   | 0     | 0.72   |
| Intel     | HBRPEKNX0202AC     | 512 GB | 4       | 264   | 0     | 0.72   |
| Gigabyte  | GP-GSM2NE3100TNTD  | 1 TB   | 15      | 263   | 0     | 0.72   |
| Intel     | SSDPEKKW128G8      | 128 GB | 20      | 263   | 0     | 0.72   |
| SanDisk   | Extreme Pro        | 1 TB   | 13      | 260   | 0     | 0.71   |
| AMD       | R5MP120G8          | 120 GB | 10      | 258   | 0     | 0.71   |
| Corsair   | Force MP300        | 120 GB | 5       | 258   | 0     | 0.71   |
| Phytium   | S1200CYX1-T0M22... | 256 GB | 2       | 258   | 0     | 0.71   |
| Toshiba   | KBG40ZPZ512G NVMe  | 512 GB | 5       | 257   | 0     | 0.71   |
| ADATA     | SX6000NP           | 512 GB | 7       | 326   | 17    | 0.71   |
| Seagate   | BarraCuda Q5 ZP... | 1 TB   | 11      | 257   | 0     | 0.71   |
| Samsung   | MZVPW256HEGL-00000 | 256 GB | 25      | 256   | 0     | 0.70   |
| ADATA     | SX8200PNP          | 512 GB | 178     | 256   | 1     | 0.70   |
| SK hynix  | SHGP31-1000GM-2    | 1 TB   | 37      | 255   | 0     | 0.70   |
| Patriot   | Scorch M2          | 512 GB | 5       | 255   | 0     | 0.70   |
| Corsair   | MP600 CORE         | 1 TB   | 10      | 253   | 0     | 0.70   |
| HP        | SSD EX900          | 250 GB | 29      | 294   | 74    | 0.69   |
| Silico... | NVME               | 256 GB | 2       | 253   | 0     | 0.69   |
| Intel     | SSDPEKKF256G8 NVMe | 256 GB | 16      | 253   | 0     | 0.69   |
| Intel     | MEMPEI1J016GAL     | 16 GB  | 3       | 252   | 0     | 0.69   |
| ZHITAI    | PC005 Active       | 1 TB   | 6       | 252   | 0     | 0.69   |
| Toshiba   | KXG6AZNV512G NV... | 512 GB | 2       | 252   | 0     | 0.69   |
| Samsung   | SSD 960 EVO        | 500 GB | 188     | 264   | 19    | 0.69   |
| Toshiba   | RC100              | 240 GB | 12      | 252   | 0     | 0.69   |
| Intel     | SSDPEKNW512G8      | 512 GB | 479     | 252   | 1     | 0.69   |
| SK hynix  | PC601 NVMe         | 512 GB | 66      | 251   | 0     | 0.69   |
| Gigabyte  | GP-AG42TB          | 2 TB   | 6       | 250   | 0     | 0.69   |
| ADATA     | SX8200PNP          | 2 TB   | 76      | 254   | 27    | 0.68   |
| Intel     | H10 HBRPEKNX020... | 1 TB   | 5       | 276   | 1     | 0.68   |
| Samsung   | SSD 960 PRO        | 512 GB | 105     | 261   | 14    | 0.68   |
| SanDisk   | WD Red SN700       | 4 TB   | 4       | 247   | 0     | 0.68   |
| XPG       | GAMMIX S11 Pro     | 1 TB   | 175     | 249   | 1     | 0.68   |
| Toshiba   | KBG30ZMS128G NVMe  | 128 GB | 18      | 247   | 0     | 0.68   |
| T-FORCE   | TM8FP5001T         | 1 TB   | 5       | 246   | 0     | 0.68   |
| Samsung   | SSD 960 EVO        | 1 TB   | 75      | 270   | 16    | 0.67   |
| Lenovo    | LENSE20256GMSP3... | 256 GB | 41      | 260   | 7     | 0.67   |
| Asgard    | AN2 250NVMe-M.2-80 | 250 GB | 2       | 246   | 0     | 0.67   |
| Phison    | BPX                | 240 GB | 6       | 327   | 5     | 0.67   |
| Samsung   | MZFLV512HCJH-000MV | 512 GB | 8       | 245   | 0     | 0.67   |
| Toshiba   | THNSN5256GPU7 NVMe | 256 GB | 8       | 245   | 0     | 0.67   |
| Corsair   | Force MP510        | 240 GB | 64      | 244   | 0     | 0.67   |
| SK hynix  | PC300 NVMe         | 512 GB | 13      | 244   | 0     | 0.67   |
| Toshiba   | THNSN51T02DU7 NVMe | 1 TB   | 6       | 244   | 0     | 0.67   |
| Toshiba   | KXG60ZNV256G NVMe  | 256 GB | 32      | 244   | 0     | 0.67   |
| WDC       | WDBA3V5000ANC-WRSN | 500 GB | 4       | 244   | 0     | 0.67   |
| KIOXIA    | KBG40ZPZ1T02 NVMe  | 1 TB   | 24      | 242   | 0     | 0.66   |
| ADATA     | SX8200PNP          | 256 GB | 67      | 263   | 48    | 0.66   |
| WDC       | WDS500G3X0C-00SJG0 | 500 GB | 233     | 243   | 5     | 0.66   |
| SanDisk   | Extreme Pro        | 500 GB | 23      | 241   | 0     | 0.66   |
| WDC       | WDS500G3XHC-00SJG0 | 500 GB | 30      | 241   | 0     | 0.66   |
| Intel     | SSDPEKKF512G8 NVMe | 512 GB | 14      | 313   | 3     | 0.66   |
| Crucial   | CT500P1SSD8        | 500 GB | 147     | 263   | 16    | 0.66   |
| Kingston  | SA2000M8250G       | 250 GB | 150     | 240   | 0     | 0.66   |
| Intel     | H10 HBRPEKNX020... | 512 GB | 42      | 240   | 0     | 0.66   |
| T-FORCE   | TM8FP8001T         | 1 TB   | 4       | 240   | 0     | 0.66   |
| Intel     | SSDPE2KX010T8      | 1 TB   | 4       | 239   | 0     | 0.66   |
| ADATA     | SX8200NP           | 960 GB | 3       | 239   | 0     | 0.66   |
| Seagate   | FireCuda 510 SS... | 2 TB   | 8       | 239   | 0     | 0.66   |
| China     | NVME SSD           | 512 GB | 10      | 250   | 1     | 0.66   |
| Hikvision | HS-SSD-C2000Pro... | 1 TB   | 5       | 238   | 0     | 0.65   |
| Plextor   | PX-256M8PeY        | 256 GB | 3       | 238   | 0     | 0.65   |
| Phison    | Viper M.2 VPR100   | 512 GB | 2       | 237   | 0     | 0.65   |
| Samsung   | MZVLV256HCHP-000H1 | 256 GB | 16      | 237   | 0     | 0.65   |
| Transcend | TS512GMTE220S      | 512 GB | 28      | 236   | 0     | 0.65   |
| Lite-On   | CL1-4D128          | 128 GB | 2       | 236   | 0     | 0.65   |
| Toshiba   | THNSN0128GTYA      | 128 GB | 8       | 236   | 0     | 0.65   |
| Samsung   | MZVLW128HEGR-000L1 | 128 GB | 11      | 235   | 0     | 0.65   |
| Intel     | SSDPEKNW010T9      | 1 TB   | 50      | 234   | 0     | 0.64   |
| Kingston  | SA2000M8500G       | 500 GB | 201     | 234   | 0     | 0.64   |
| Gigabyte  | GP-GSM2NE8256GNTD  | 256 GB | 3       | 233   | 0     | 0.64   |
| Gigabyte  | GP-AG70S2TB        | 2 TB   | 4       | 232   | 0     | 0.64   |
| Hikvision | HS-SSD-E1000 1024G | 1 TB   | 5       | 231   | 0     | 0.63   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 4       | 231   | 0     | 0.63   |
| Phison    | Viper M.2 VP4100   | 1 TB   | 9       | 231   | 0     | 0.63   |
| Phison    | ESR01TBTLCG-EAC-4  | 1 TB   | 5       | 231   | 0     | 0.63   |
| Toshiba   | THNSN0256GTYA      | 256 GB | 4       | 231   | 0     | 0.63   |
| WDC       | WDS400T3X0C-00SJG0 | 4 TB   | 3       | 230   | 0     | 0.63   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 7       | 230   | 0     | 0.63   |
| Samsung   | MZFLV256HCHP-000MV | 256 GB | 18      | 229   | 0     | 0.63   |
| Hikvision | HS-SSD-E2000       | 256 GB | 2       | 229   | 0     | 0.63   |
| Intel     | HBRPEKNX0101AHO    | 16 GB  | 32      | 228   | 0     | 0.63   |
| T-FORCE   | TM8FP7001T         | 1 TB   | 12      | 252   | 84    | 0.62   |
| Samsung   | MZVLV512HCJH-000L2 | 512 GB | 3       | 225   | 0     | 0.62   |
| Samsung   | MZSLW1T0HMLH-000L1 | 1 TB   | 11      | 225   | 0     | 0.62   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 31      | 224   | 0     | 0.62   |
| Samsung   | SSD 960 PRO        | 1 TB   | 38      | 244   | 4     | 0.62   |
| Samsung   | MZVKW1T0HMLH-000H1 | 1 TB   | 9       | 224   | 0     | 0.62   |
| Toshiba   | KBG40ZPZ128G ME... | 128 GB | 8       | 223   | 0     | 0.61   |
| WDC       | WDS250G3X0C-00SJG0 | 250 GB | 35      | 223   | 0     | 0.61   |
| Toshiba   | KBG20ZMS512G NVMe  | 512 GB | 2       | 223   | 0     | 0.61   |
| Kingston  | SKC2000M81000G     | 1 TB   | 7       | 223   | 0     | 0.61   |
| LDLC      | F8+M.2 480         | 480 GB | 7       | 222   | 0     | 0.61   |
| WDC       | WDS100T2B0C-00PXH0 | 1 TB   | 346     | 224   | 6     | 0.61   |
| Intel     | SSDPE2KX020T8      | 2 TB   | 12      | 221   | 0     | 0.61   |
| Reletech  | M.2 SSD            | 512 GB | 3       | 220   | 0     | 0.60   |
| Phison    | E12-256G-PHISON... | 256 GB | 3       | 220   | 0     | 0.60   |
| Kingston  | SA2000M81000G      | 1 TB   | 247     | 221   | 13    | 0.60   |
| Wester... | SN730              | 500 GB | 4       | 223   | 1     | 0.60   |
| Toshiba   | KXG6AZNV1T02       | 1 TB   | 41      | 218   | 0     | 0.60   |
| AMD       | R5MP240G8          | 240 GB | 6       | 217   | 0     | 0.60   |
| KIOXIA    | KBG40ZPZ512G NVMe  | 512 GB | 24      | 217   | 0     | 0.60   |
| TOPMORE   | Aquarius           | 4 TB   | 2       | 216   | 0     | 0.59   |
| Samsung   | PM981 NVMe         | 1 TB   | 19      | 215   | 0     | 0.59   |
| Toshiba   | KBG30ZMV256G       | 256 GB | 86      | 215   | 0     | 0.59   |
| Phison    | Sabrent Rocket ... | 1 TB   | 19      | 214   | 0     | 0.59   |
| Seagate   | FireCuda 520 SS... | 2 TB   | 19      | 214   | 0     | 0.59   |
| Toshiba   | KBG30ZMV128G       | 128 GB | 9       | 243   | 113   | 0.59   |
| Kingston  | SKC2500M8250G      | 250 GB | 19      | 212   | 0     | 0.58   |
| Transcend | TS128GMTE110S      | 128 GB | 22      | 212   | 0     | 0.58   |
| Samsung   | MZVPW256HEGL-000H1 | 256 GB | 17      | 212   | 0     | 0.58   |
| Intel     | SSDPF2NV307TZ      | 30.... | 2       | 211   | 0     | 0.58   |
| Silico... | EX-1TB PRO         | 1 TB   | 3       | 211   | 0     | 0.58   |
| Intel     | SSDPEMKF256G8 NVMe | 256 GB | 9       | 211   | 0     | 0.58   |
| ADATA     | SX7000NP           | 128 GB | 5       | 446   | 37    | 0.58   |
| SK hynix  | PC611 NVMe         | 1 TB   | 67      | 210   | 0     | 0.58   |
| SK hynix  | PC611 NVMe         | 512 GB | 59      | 212   | 18    | 0.58   |
| Intel     | SSDPEL1K100GA      | 100 GB | 2       | 382   | 5     | 0.58   |
| KIOXIA    | KBG40ZNS128G BG4A  | 128 GB | 6       | 210   | 0     | 0.58   |
| Seagate   | FireCuda 520 SS... | 1 TB   | 31      | 209   | 0     | 0.58   |
| SK hynix  | PC611 NVMe         | 256 GB | 6       | 209   | 0     | 0.57   |
| Plextor   | PX-512M8PeG        | 512 GB | 7       | 225   | 79    | 0.57   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 4       | 208   | 0     | 0.57   |
| Silico... | Asgard AN2 250N... | 250 GB | 3       | 207   | 0     | 0.57   |
| Seagate   | FireCuda 520 SS... | 500 GB | 26      | 207   | 0     | 0.57   |
| Toshiba   | KBG40ZNS256G ME... | 256 GB | 4       | 206   | 0     | 0.57   |
| SanDisk   | WD_BLACK SN750     | 2 TB   | 17      | 206   | 0     | 0.57   |
| KIOXIA    | KXG6AZNV512G       | 512 GB | 6       | 205   | 0     | 0.56   |
| Plextor   | PX-512M9PeY        | 512 GB | 6       | 204   | 0     | 0.56   |
| Samsung   | Portable SSD T7    | 500 GB | 14      | 203   | 0     | 0.56   |
| SSSTC     | CL1-3D256-Q11 NVMe | 256 GB | 33      | 202   | 0     | 0.56   |
| SanDisk   | WD_BLACK SN850 ... | 2 TB   | 2       | 202   | 0     | 0.55   |
| SanDisk   | WD_BLACK SN850 ... | 1 TB   | 2       | 201   | 0     | 0.55   |
| Phison    | Sabrent Rocket ... | 1 TB   | 42      | 201   | 0     | 0.55   |
| Micron    | 9300_MTFDHAL6T4TDR | 6.4 TB | 2       | 201   | 0     | 0.55   |
| Kingston  | RBUSNS8154P3256GJ5 | 256 GB | 4       | 201   | 0     | 0.55   |
| Apacer    | Z280 120G          | 120 GB | 2       | 201   | 0     | 0.55   |
| Corsair   | MP600 PRO XT       | 1 TB   | 5       | 200   | 0     | 0.55   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 3       | 200   | 0     | 0.55   |
| Toshiba   | KBG40ZNS256G NVMe  | 256 GB | 27      | 199   | 0     | 0.55   |
| Silico... | NVME SSD           | 512 GB | 8       | 199   | 0     | 0.55   |
| Toshiba   | KXG6APNV2T04       | 2 TB   | 5       | 199   | 0     | 0.55   |
| Intel     | HBRPEKNX0101AH     | 256 GB | 31      | 199   | 0     | 0.55   |
| Kingston  | RBUSNS8154P3512GJ1 | 512 GB | 38      | 199   | 0     | 0.55   |
| Intel     | MEMPEK1J016GAL     | 16 GB  | 19      | 210   | 53    | 0.55   |
| Intel     | HBRPEKNX0202ALO    | 32 GB  | 12      | 198   | 0     | 0.54   |
| Samsung   | MZVPW128HEGM-00000 | 128 GB | 2       | 216   | 16    | 0.54   |
| UMIS      | RPITJ1TBVME2HWD    | 1 TB   | 3       | 198   | 0     | 0.54   |
| KIOXIA    | KXG70ZNV512G NVMe  | 512 GB | 13      | 197   | 0     | 0.54   |
| MSI       | M480               | 1 TB   | 3       | 197   | 0     | 0.54   |
| Samsung   | MZVLW1T0HMLH-000L2 | 1 TB   | 9       | 197   | 0     | 0.54   |
| Plextor   | PX-256M9PeGN       | 256 GB | 5       | 196   | 0     | 0.54   |
| Hikvision | HS-SSD-E1000 128G  | 128 GB | 5       | 196   | 0     | 0.54   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 43      | 196   | 0     | 0.54   |
| Goodram   | IR-SSDPR-P34B-0... | 2 TB   | 6       | 195   | 0     | 0.54   |
| Lenovo    | LENSE20512GMSP3... | 512 GB | 18      | 208   | 56    | 0.54   |
| Apacer    | AS2280P4           | 240 GB | 3       | 195   | 0     | 0.54   |
| Silico... | Asgard AN512NVM... | 512 GB | 2       | 195   | 0     | 0.54   |
| Team      | TM8FP4001T         | 1 TB   | 12      | 266   | 338   | 0.54   |
| WDC       | WDS100T3X0C-00SJG0 | 1 TB   | 207     | 195   | 3     | 0.54   |
| Samsung   | MZQL23T8HCLS-00... | 3.8 TB | 38      | 195   | 0     | 0.54   |
| PNY       | CS1030 500GB SSD   | 500 GB | 5       | 194   | 0     | 0.53   |
| ADATA     | SX7000NP           | 256 GB | 3       | 194   | 0     | 0.53   |
| Micron    | MTFDHBA1T0QFD-1... | 1 TB   | 5       | 194   | 0     | 0.53   |
| Corsair   | MP400              | 1 TB   | 14      | 194   | 0     | 0.53   |
| Toshiba   | KXG5AZNV1T02 NV... | 1 TB   | 2       | 194   | 0     | 0.53   |
| Transcend | TS2TMTE250S        | 2 TB   | 2       | 193   | 0     | 0.53   |
| SK hynix  | BC501 HFM128GDJ... | 128 GB | 13      | 193   | 0     | 0.53   |
| Gigaby... | GP-GSM2NE3128GNTD  | 128 GB | 3       | 193   | 0     | 0.53   |
| WDC       | PC SN730 SDBQNT... | 512 GB | 6       | 193   | 0     | 0.53   |
| Samsung   | MZVKW512HMJP-000L7 | 512 GB | 26      | 193   | 0     | 0.53   |
| KIOXIA    | KXG60ZNV512G       | 512 GB | 65      | 192   | 0     | 0.53   |
| Intel     | SSDPEKKF256G8L     | 256 GB | 126     | 192   | 9     | 0.53   |
| WDC       | PC SN520 SDAPMU... | 512 GB | 14      | 191   | 6     | 0.52   |
| Mushkin   | MKNSSDPE2TB-D8     | 2 TB   | 16      | 189   | 0     | 0.52   |
| Toshiba   | KBG30ZMT128G       | 128 GB | 25      | 189   | 0     | 0.52   |
| MSI       | M371               | 2 TB   | 3       | 189   | 0     | 0.52   |
| Transcend | TS256GMTE220S      | 256 GB | 16      | 188   | 0     | 0.52   |
| Apacer    | AS2280P4U          | 2 TB   | 3       | 188   | 0     | 0.52   |
| Samsung   | MZVLB1T0HALR-00000 | 1 TB   | 62      | 206   | 1     | 0.52   |
| SK hynix  | PC400 NVMe         | 512 GB | 3       | 187   | 0     | 0.51   |
| WDC       | WDS200T3X0C-00SJG0 | 2 TB   | 13      | 187   | 0     | 0.51   |
| Fanxiang  | S690               | 1 TB   | 2       | 187   | 0     | 0.51   |
| Transcend | TS1TMTE110S        | 1 TB   | 3       | 186   | 0     | 0.51   |
| WDC       | WD BLACK SDBPNT... | 256 GB | 2       | 186   | 0     | 0.51   |
| KIOXIA    | KXG60ZNV1T02       | 1 TB   | 56      | 186   | 0     | 0.51   |
| KIOXIA... | SSD                | 500 GB | 30      | 191   | 2     | 0.51   |
| Intel     | SSDPEBKF256G7      | 256 GB | 5       | 189   | 1     | 0.51   |
| Intel     | SSDPE21D280GA      | 280 GB | 5       | 185   | 0     | 0.51   |
| Kingston  | OM8PCP3512F-AB     | 512 GB | 102     | 185   | 0     | 0.51   |
| Samsung   | KUS040202M-B000    | 512 GB | 5       | 185   | 0     | 0.51   |
| Intel     | SSDPEKKW010T8      | 1 TB   | 13      | 185   | 0     | 0.51   |
| KIOXIA    | KBG40ZNS256G NVMe  | 256 GB | 183     | 184   | 0     | 0.51   |
| Patriot   | P300               | 512 GB | 3       | 184   | 0     | 0.51   |
| PNY       | CS2140 1TB SSD     | 1 TB   | 8       | 183   | 0     | 0.50   |
| Samsung   | MZFLV128HCGR-000MV | 128 GB | 19      | 182   | 0     | 0.50   |
| Corsair   | MP600 PRO          | 1 TB   | 10      | 182   | 0     | 0.50   |
| Phison    | E12-512G-PHISON... | 512 GB | 3       | 182   | 0     | 0.50   |
| Gigabyte  | GP-AG41TB          | 1 TB   | 24      | 182   | 0     | 0.50   |
| Patriot   | Scorch M2          | 128 GB | 8       | 182   | 0     | 0.50   |
| WDC       | PC SN730 NVMe      | 256 GB | 9       | 182   | 0     | 0.50   |
| PNY       | CS2130 1TB SSD     | 1 TB   | 13      | 182   | 0     | 0.50   |
| KIOXIA    | KBG30ZMV256G       | 256 GB | 45      | 182   | 23    | 0.50   |
| SSSTC     | CL1-3D512-Q11 NVMe | 512 GB | 26      | 192   | 1     | 0.50   |
| Kingston  | SKC2500M81000G     | 1 TB   | 28      | 182   | 0     | 0.50   |
| Kingston  | RBUSNS8154P3512GJ5 | 512 GB | 11      | 182   | 0     | 0.50   |
| XrayDisk  | 512GB              | 512 GB | 3       | 181   | 0     | 0.50   |
| Corsair   | MP400              | 2 TB   | 12      | 181   | 0     | 0.50   |
| Silico... | NE-1TB             | 1 TB   | 16      | 181   | 0     | 0.50   |
| Transcend | TS2TMTE220S        | 2 TB   | 8       | 181   | 0     | 0.50   |
| KIOXIA    | KXG7AZNV512G LA    | 512 GB | 7       | 180   | 0     | 0.50   |
| Netac     | NVMe SSD           | 500 GB | 18      | 180   | 0     | 0.49   |
| Samsung   | SSD 970 PRO        | 1 TB   | 130     | 187   | 1     | 0.49   |
| SK hynix  | PC601 HFS001TD9... | 1 TB   | 2       | 179   | 0     | 0.49   |
| Corsair   | Force MP510        | 4 TB   | 4       | 179   | 0     | 0.49   |

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
| Asgard      | 4      | 8       | 363   | 0     | 1.00   |
| Aura        | 1      | 14      | 312   | 0     | 0.86   |
| Corsair     | 40     | 565     | 307   | 1     | 0.84   |
| GLOWAY      | 1      | 2       | 278   | 0     | 0.76   |
| Toshiba     | 92     | 1775    | 275   | 4     | 0.74   |
| Plextor     | 15     | 59      | 288   | 29    | 0.73   |
| addlink     | 2      | 43      | 261   | 0     | 0.72   |
| Intel       | 116    | 3719    | 273   | 7     | 0.71   |
| Phytium     | 1      | 2       | 258   | 0     | 0.71   |
| PNY         | 26     | 227     | 258   | 2     | 0.69   |
| HP          | 19     | 201     | 249   | 14    | 0.64   |
| LDLC        | 1      | 7       | 222   | 0     | 0.61   |
| Phison      | 98     | 1538    | 209   | 3     | 0.57   |
| EMTEC       | 2      | 5       | 207   | 0     | 0.57   |
| Transcend   | 14     | 144     | 193   | 7     | 0.53   |
| AMD         | 5      | 24      | 190   | 0     | 0.52   |
| Mushkin     | 11     | 53      | 201   | 40    | 0.52   |
| Reletech    | 4      | 11      | 181   | 0     | 0.50   |
| Gigabyte    | 24     | 218     | 175   | 19    | 0.48   |
| OWC         | 1      | 2       | 168   | 0     | 0.46   |
| Seagate     | 29     | 269     | 167   | 0     | 0.46   |
| T-FORCE     | 9      | 45      | 188   | 23    | 0.45   |
| Smartbuy    | 4      | 13      | 163   | 0     | 0.45   |
| SPCC        | 9      | 398     | 164   | 25    | 0.44   |
| XPG         | 14     | 415     | 173   | 26    | 0.43   |
| Dell        | 10     | 37      | 156   | 0     | 0.43   |
| Lenovo      | 5      | 114     | 164   | 12    | 0.43   |
| Hikvision   | 18     | 71      | 156   | 1     | 0.43   |
| Western ... | 2      | 6       | 155   | 1     | 0.42   |
| TOPMORE     | 2      | 4       | 149   | 0     | 0.41   |
| ADATA       | 76     | 1345    | 155   | 23    | 0.40   |
| Ramsta      | 1      | 2       | 138   | 0     | 0.38   |
| XrayDisk    | 4      | 37      | 137   | 0     | 0.38   |
| KIOXIA      | 68     | 1893    | 131   | 1     | 0.36   |
| Lite-On     | 20     | 130     | 146   | 34    | 0.34   |
| Gigabyte... | 12     | 81      | 123   | 0     | 0.34   |
| Silicon ... | 58     | 442     | 124   | 7     | 0.34   |
| KIOXIA-E... | 8      | 134     | 123   | 1     | 0.34   |
| Goodram     | 16     | 78      | 122   | 1     | 0.33   |
| Zheino      | 2      | 4       | 118   | 0     | 0.33   |
| WDC         | 166    | 5874    | 118   | 2     | 0.32   |
| Crucial     | 38     | 2534    | 120   | 5     | 0.32   |
| Kingston    | 87     | 3614    | 117   | 3     | 0.32   |
| Patriot     | 15     | 141     | 122   | 2     | 0.31   |
| JAMESDONKEY | 1      | 2       | 107   | 0     | 0.29   |
| Team        | 19     | 204     | 110   | 36    | 0.29   |
| SSSTC       | 33     | 353     | 104   | 4     | 0.28   |
| ORTIAL      | 1      | 3       | 98    | 0     | 0.27   |
| SK hynix    | 157    | 4305    | 94    | 1     | 0.26   |
| MSI         | 15     | 66      | 92    | 0     | 0.25   |
| SMI         | 1      | 4       | 91    | 0     | 0.25   |
| Dahua       | 1      | 2       | 91    | 0     | 0.25   |
| Samsung     | 320    | 18827   | 90    | 4     | 0.24   |
| J.ZAO       | 2      | 7       | 140   | 97    | 0.24   |
| KINGBANK    | 2      | 14      | 84    | 0     | 0.23   |
| UMIS        | 28     | 411     | 88    | 4     | 0.23   |
| ZHITAI      | 10     | 63      | 85    | 1     | 0.23   |
| KLLISRE     | 2      | 8       | 82    | 0     | 0.23   |
| China       | 6      | 102     | 85    | 1     | 0.23   |
| HUAWEI      | 2      | 10      | 78    | 0     | 0.22   |
| Timetec     | 2      | 10      | 75    | 0     | 0.21   |
| Star Drive  | 1      | 20      | 73    | 0     | 0.20   |
| Netac       | 8      | 148     | 78    | 17    | 0.20   |
| Apacer      | 11     | 142     | 72    | 7     | 0.19   |
| Inland      | 2      | 11      | 69    | 7     | 0.19   |
| MidasForce  | 1      | 3       | 66    | 0     | 0.18   |
| KLEVV       | 2      | 13      | 97    | 11    | 0.18   |
| Kimtigo     | 2      | 18      | 71    | 56    | 0.18   |
| Lexar       | 23     | 314     | 65    | 1     | 0.18   |
| Kingmax     | 1      | 2       | 62    | 0     | 0.17   |
| VICKTER     | 1      | 3       | 60    | 0     | 0.17   |
| OSCOO       | 1      | 2       | 56    | 0     | 0.16   |
| Micron      | 88     | 2599    | 55    | 2     | 0.15   |
| YMTC        | 10     | 128     | 55    | 1     | 0.15   |
| TwinMOS     | 1      | 6       | 55    | 0     | 0.15   |
| KingFast    | 2      | 10      | 53    | 0     | 0.15   |
| Fanxiang    | 19     | 85      | 51    | 0     | 0.14   |
| FIKWOT      | 3      | 9       | 50    | 0     | 0.14   |
| Kingchuxing | 1      | 2       | 47    | 0     | 0.13   |
| AirDisk     | 1      | 31      | 47    | 0     | 0.13   |
| WALRAM      | 4      | 16      | 47    | 0     | 0.13   |
| SNR         | 1      | 3       | 45    | 0     | 0.13   |
| SanDisk     | 125    | 2752    | 45    | 1     | 0.12   |
| INDMEM      | 1      | 2       | 174   | 3     | 0.12   |
| imation     | 2      | 4       | 43    | 0     | 0.12   |
| Teclast     | 2      | 5       | 42    | 0     | 0.12   |
| ShiJi       | 2      | 7       | 47    | 229   | 0.11   |
| EDILOCA     | 2      | 4       | 38    | 0     | 0.10   |
| Colorful    | 3      | 8       | 36    | 0     | 0.10   |
| Apple       | 32     | 580     | 32    | 4     | 0.09   |
| EVM         | 1      | 2       | 30    | 0     | 0.08   |
| Intenso     | 3      | 15      | 30    | 1     | 0.08   |
| BIWIN       | 11     | 113     | 28    | 0     | 0.08   |
| LuminouTek  | 1      | 2       | 27    | 0     | 0.08   |
| ORICO       | 2      | 5       | 27    | 0     | 0.07   |
| GOFATOO     | 2      | 6       | 27    | 0     | 0.07   |
| FORESEE     | 17     | 145     | 30    | 1     | 0.07   |
| ASint       | 1      | 2       | 25    | 0     | 0.07   |
| SUNEAST     | 1      | 2       | 22    | 0     | 0.06   |
| Union Me... | 7      | 67      | 21    | 0     | 0.06   |
| aigo        | 1      | 2       | 20    | 0     | 0.06   |
| Acer        | 5      | 26      | 24    | 4     | 0.05   |
| BR          | 2      | 5       | 18    | 0     | 0.05   |
| ExeGate     | 2      | 4       | 18    | 0     | 0.05   |
| Wodposit    | 2      | 22      | 16    | 0     | 0.04   |
| Solid St... | 4      | 11      | 15    | 0     | 0.04   |
| PUSKILL     | 1      | 2       | 14    | 0     | 0.04   |
| HJDK        | 2      | 7       | 14    | 0     | 0.04   |
| OEM         | 1      | 4       | 12    | 0     | 0.03   |
| Foxline     | 2      | 23      | 8     | 0     | 0.02   |
| EAGET       | 3      | 7       | 6     | 0     | 0.02   |
| SCY         | 2      | 14      | 5     | 0     | 0.02   |
| AGI         | 1      | 9       | 5     | 0     | 0.01   |
| MMY         | 1      | 5       | 3     | 0     | 0.01   |
| Bestoss     | 1      | 2       | 2     | 0     | 0.01   |
| Kllisre     | 1      | 2       | 1     | 0     | 0.00   |
| ZTC         | 1      | 2       | 0     | 0     | 0.00   |
| Verbatim    | 1      | 2       | 0     | 0     | 0.00   |
| Rayson      | 1      | 2       | 0     | 0     | 0.00   |
| kllisre     | 1      | 2       | 0     | 0     | 0.00   |
| DELL        | 1      | 2       | 0     | 0     | 0.00   |

