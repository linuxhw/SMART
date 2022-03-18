HDD/SSD Desktop-Class Reliability Test
======================================

This is a project to estimate reliability of desktop-class HDD/SSD drives by
the analysis of SMART data collected by Linux users at https://linux-hardware.org. The
primary aim of the project is to find drives with longest power-on hours (POH) and
minimal number of errors, i.e. maximal MTBF (mean time between failures).

Everyone can contribute to this report by uploading probes of their computers by
the [hw-probe](https://github.com/linuxhw/hw-probe) tool:

    sudo -E hw-probe -all -upload

Total drives: 103967.

Contents
--------

1. [ About          ](#about)
2. [ HDD by Model   ](#hdd-by-model)
3. [ HDD by Family  ](#hdd-by-family)
4. [ HDD by Vendor  ](#hdd-by-vendor)
5. [ SSD by Model   ](#ssd-by-model)
6. [ SSD by Family  ](#ssd-by-family)
7. [ SSD by Vendor  ](#ssd-by-vendor)
8. [ NVMe by Model  ](#nvme-by-model)
9. [ NVMe by Vendor ](#nvme-by-vendor)

About
-----

The structure of the reports directory is the following:

    {KIND OF DRIVE}/{VENDOR}/{MODEL PREFIX}/{MODEL}/{DRIVE ID}

    ( e.g. HDD/Seagate/ST1000/ST1000LM035-1RK172/3F1554E2F97E )

Based on SMART data we determine most reliable drive models and vendors by the
following formula:

    MTBF = MAX( Power_On_Hours / ( 1 + Number_Of_Important_Errors ) ) / ( 365*24 )

    ( i.e. MTBF = "Years before/between errors" )

Number_Of_Important_Errors — number of important errors that can indicate a drive failure:

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

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

See full list of tested HDD samples in the Appendix 1 ([All_HDD.md](/All_HDD.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| Samsung   | HM020GI            | 20 GB  | 2       | 6601  | 0     | 18.09  |
| Samsung   | SV1021H            | 10 GB  | 1       | 5713  | 0     | 15.65  |
| Toshiba   | MQ01AAD020C        | 200 GB | 1       | 4449  | 0     | 12.19  |
| WDC       | WD7500AAVS-00D7B0  | 752 GB | 1       | 4362  | 0     | 11.95  |
| WDC       | WD3200AACS-00M6B0  | 320 GB | 1       | 4087  | 0     | 11.20  |
| Hitachi   | HCP725025GLAT80    | 250 GB | 1       | 4058  | 0     | 11.12  |
| Samsung   | HD754JJ            | 752 GB | 1       | 3908  | 0     | 10.71  |
| Hitachi   | HUA721075KLA330    | 752 GB | 1       | 3668  | 0     | 10.05  |
| Hitachi   | HUA722020ALA330... | 2 TB   | 1       | 3566  | 0     | 9.77   |
| Hitachi   | HDS728040PLA320... | 40 GB  | 1       | 3563  | 0     | 9.76   |
| Hitachi   | HUA7210SASUN1.0... | 1 TB   | 1       | 3495  | 0     | 9.58   |
| HGST      | HUP722020APA330    | 2 TB   | 1       | 3466  | 0     | 9.50   |
| HP        | GB0160EAFJE        | 160 GB | 2       | 3447  | 0     | 9.44   |
| WDC       | WD20EACS-11BHUB0   | 2 TB   | 1       | 3085  | 0     | 8.45   |
| Samsung   | HE160HJ            | 160 GB | 2       | 3011  | 0     | 8.25   |
| WDC       | WD84AA             | 8 GB   | 1       | 2903  | 0     | 7.95   |
| WDC       | WD5000AAKS-60A7B0  | 500 GB | 2       | 2876  | 0     | 7.88   |
| WDC       | WD2500AAJS-62B4A0  | 250 GB | 1       | 2854  | 0     | 7.82   |
| Seagate   | ST4000DM000-1CD168 | 4 TB   | 1       | 2813  | 0     | 7.71   |
| WDC       | WD2500AVJB-63J5A0  | 250 GB | 1       | 2804  | 0     | 7.68   |
| Seagate   | ST2000VM002-9UY166 | 2 TB   | 1       | 2787  | 0     | 7.64   |
| WDC       | WD10EACS-14ZJB0    | 1 TB   | 1       | 2742  | 0     | 7.51   |
| WDC       | WD2500AAJS-00RYA0  | 250 GB | 1       | 2695  | 0     | 7.39   |
| Hitachi   | HUA7210SASUN1.0T   | 1 TB   | 12      | 2672  | 0     | 7.32   |
| WDC       | WD6400AAVS-00G9B0  | 640 GB | 1       | 2668  | 0     | 7.31   |
| WDC       | WD30EURS-73TLHY0   | 3 TB   | 1       | 2606  | 0     | 7.14   |
| WDC       | WD5000BUCT-63PUZY0 | 500 GB | 2       | 2600  | 0     | 7.13   |
| WDC       | WD10EVDS-63N5B1    | 1 TB   | 4       | 2541  | 0     | 6.96   |
| WDC       | WD5000AAKS-40YGA1  | 500 GB | 1       | 2532  | 0     | 6.94   |
| HP        | GB0500EAFYL        | 500 GB | 2       | 2969  | 1     | 6.86   |
| WDC       | WD740GD-00FLA1     | 74 GB  | 1       | 2489  | 0     | 6.82   |
| WDC       | WD7502ABYS-18A6B0  | 752 GB | 1       | 2416  | 0     | 6.62   |
| WDC       | WD60EFRX-68MYMN0   | 6 TB   | 1       | 2399  | 0     | 6.58   |
| WDC       | WD5000AVVS-63ZWB0  | 500 GB | 4       | 3388  | 12    | 6.49   |
| WDC       | WD5000AAKX-753CA0  | 500 GB | 3       | 2366  | 0     | 6.48   |
| WDC       | WD2500AAJS-07VWA0  | 250 GB | 2       | 2354  | 0     | 6.45   |
| Seagate   | ST3808110AS 41N... | 80 GB  | 1       | 2296  | 0     | 6.29   |
| WDC       | WD5001AALS-00J7B0  | 500 GB | 1       | 2295  | 0     | 6.29   |
| Hitachi   | HUA721050KLA330    | 500 GB | 4       | 2268  | 0     | 6.21   |
| WDC       | WD1600JS-75NCB1    | 160 GB | 1       | 2267  | 0     | 6.21   |
| Hitachi   | HDS724040ALE640    | 4 TB   | 8       | 2332  | 171   | 6.14   |
| Seagate   | ST3750641NS EIT    | 752 GB | 1       | 2229  | 0     | 6.11   |
| WDC       | WD2500SD-01KCB0    | 250 GB | 2       | 2568  | 1     | 6.06   |
| Hitachi   | HDS722516VLAT80    | 164 GB | 1       | 2212  | 0     | 6.06   |
| Fujitsu   | MHT2040BH          | 40 GB  | 1       | 4417  | 1     | 6.05   |
| WDC       | WD1001FALS-00K1B0  | 1 TB   | 2       | 2199  | 0     | 6.02   |
| WDC       | WD2003FYYS-18W0B0  | 2 TB   | 3       | 2192  | 0     | 6.01   |
| Hitachi   | HDS722020ALA330... | 2 TB   | 2       | 2191  | 0     | 6.00   |
| Hitachi   | HUA722020ALA330    | 2 TB   | 21      | 2730  | 2     | 5.96   |
| Seagate   | ST3750641NS        | 752 GB | 1       | 2169  | 0     | 5.94   |
| Fujitsu   | MHZ2080BK G2       | 80 GB  | 1       | 2159  | 0     | 5.92   |
| WDC       | WD6401AALS-00E8B0  | 640 GB | 6       | 2147  | 0     | 5.88   |
| WDC       | WD600BB-00DKA0     | 64 GB  | 1       | 4248  | 1     | 5.82   |
| WDC       | WD5000ABYS-01TNA0  | 500 GB | 2       | 2117  | 0     | 5.80   |
| WDC       | WD3200AVJB-63J5A0  | 320 GB | 2       | 2113  | 0     | 5.79   |
| WDC       | WD5000AADS-57S9B1  | 500 GB | 1       | 2086  | 0     | 5.72   |
| Hitachi   | HDS721025CLA682    | 250 GB | 3       | 2082  | 0     | 5.71   |
| WDC       | WD10EACS-00C7B0    | 1 TB   | 5       | 2077  | 0     | 5.69   |
| WDC       | WD3000HLFS-01G6U1  | 304 GB | 2       | 2066  | 0     | 5.66   |
| WDC       | WD800JD-75MSA1     | 80 GB  | 2       | 2057  | 0     | 5.64   |
| IBM/Hi... | IC35L120AVV207-0   | 128 GB | 2       | 2350  | 1     | 5.59   |
| WDC       | WD3000BLFS-01YBU0  | 304 GB | 6       | 2016  | 0     | 5.52   |
| HP        | GB0500C4413        | 500 GB | 2       | 2009  | 0     | 5.51   |
| WDC       | WD1002FBYS-18W8B1  | 1 TB   | 1       | 1999  | 0     | 5.48   |
| WDC       | WD1600ADFS-75SLR2  | 160 GB | 1       | 1997  | 0     | 5.47   |
| WDC       | WD10EACS-32ZJB0    | 1 TB   | 4       | 1991  | 0     | 5.46   |
| WDC       | WD800AAJB-00J3A0   | 80 GB  | 1       | 1982  | 0     | 5.43   |
| WDC       | WD1601ABYS-01C0A0  | 164 GB | 1       | 1982  | 0     | 5.43   |
| WDC       | WD7500KMVV-11A27S0 | 752 GB | 1       | 1976  | 0     | 5.42   |
| WDC       | WD10EAVS-32D7B1    | 1 TB   | 2       | 1976  | 0     | 5.42   |
| WDC       | WD1600AAJS-00RYA0  | 160 GB | 1       | 1970  | 0     | 5.40   |
| WDC       | WD2500KS-22MJB0    | 250 GB | 2       | 1943  | 0     | 5.32   |
| WDC       | WD1600AAJS-08WAA0  | 160 GB | 1       | 1934  | 0     | 5.30   |
| Toshiba   | Freecom            | 5 TB   | 1       | 1916  | 0     | 5.25   |
| WDC       | WD400BD-55MTA1     | 40 GB  | 2       | 1915  | 0     | 5.25   |
| WDC       | WD3000HLFS-01G6U4  | 304 GB | 3       | 1836  | 0     | 5.03   |
| WDC       | WD15EARS-32MVWB0   | 1.5 TB | 1       | 1831  | 0     | 5.02   |
| WDC       | WD800JB-00FMA0     | 80 GB  | 1       | 1818  | 0     | 4.98   |
| WDC       | WD7500AAKS-22RBA0  | 752 GB | 1       | 1816  | 0     | 4.98   |
| Toshiba   | MK3255GSXF         | 320 GB | 1       | 1812  | 0     | 4.97   |
| WDC       | WD360GD-00FNA0     | 37 GB  | 2       | 2599  | 1     | 4.95   |
| WDC       | WD2500YS-70SHB1    | 250 GB | 1       | 1789  | 0     | 4.90   |
| WDC       | WD1500HLFS-01G6U0  | 150 GB | 4       | 1805  | 1     | 4.87   |
| WDC       | WD400JD-19JNA0     | 40 GB  | 1       | 1756  | 0     | 4.81   |
| WDC       | WD1002FBYS-05A6B0  | 1 TB   | 3       | 1752  | 0     | 4.80   |
| Hitachi   | HDS7225SBSUN250G   | 250 GB | 1       | 5248  | 2     | 4.79   |
| WDC       | WD2500JS-41SGB0    | 250 GB | 1       | 1749  | 0     | 4.79   |
| WDC       | WD3200KS-00PFB0    | 320 GB | 5       | 1994  | 19    | 4.73   |
| WDC       | WD4000AAJS-22YFA0  | 400 GB | 1       | 1725  | 0     | 4.73   |
| Samsung   | HE103UJ            | 1 TB   | 1       | 1723  | 0     | 4.72   |
| Hitachi   | HCS5C3020BLE630    | 2 TB   | 1       | 1717  | 0     | 4.70   |
| WDC       | WD5001AALS-00F41A0 | 500 GB | 1       | 1714  | 0     | 4.70   |
| WDC       | WD400JB-00ENA0     | 40 GB  | 3       | 2383  | 6     | 4.69   |
| HGST      | HTE541515A9E630    | 1.5 TB | 1       | 1702  | 0     | 4.66   |
| WDC       | WD7502ABYS-02A6B0  | 752 GB | 1       | 1700  | 0     | 4.66   |
| WDC       | WD3200JS-55PDB0    | 320 GB | 1       | 1698  | 0     | 4.65   |
| WDC       | WD3000GLFS-01F8U0  | 304 GB | 5       | 1688  | 0     | 4.63   |
| WDC       | WD5000LPCX-16VHAT0 | 500 GB | 1       | 1686  | 0     | 4.62   |
| WDC       | WD7500AACS-00D6B0  | 752 GB | 2       | 1686  | 0     | 4.62   |
| Seagate   | ST91000640NS       | 1 TB   | 21      | 1834  | 2     | 4.62   |
| Samsung   | SP0411N            | 40 GB  | 2       | 3755  | 9     | 4.62   |
| WDC       | WD2502ABYS-01B7A0  | 256 GB | 6       | 2094  | 1     | 4.62   |
| Seagate   | ST9500320AS        | 500 GB | 2       | 1684  | 0     | 4.62   |
| WDC       | WD30EURS-63SPKY0   | 3 TB   | 5       | 1681  | 0     | 4.61   |
| WDC       | WD20EADS-32S2B0    | 2 TB   | 2       | 2225  | 5     | 4.60   |
| Hitachi   | HCS5C1010CLA382    | 1 TB   | 4       | 1678  | 0     | 4.60   |
| WDC       | WD1601ABYS-18C0A0  | 160 GB | 3       | 2288  | 4     | 4.58   |
| HGST      | HUS724020ALE640    | 2 TB   | 12      | 1668  | 0     | 4.57   |
| WDC       | WD1600JS-88MHB0    | 160 GB | 1       | 1667  | 0     | 4.57   |
| Seagate   | ST2000NX0253       | 2 TB   | 16      | 1662  | 0     | 4.55   |
| WDC       | WD6400AAKS-00H2B1  | 640 GB | 1       | 1653  | 0     | 4.53   |
| WDC       | WD3200LPVX-16V0TT3 | 320 GB | 1       | 1644  | 0     | 4.50   |
| WDC       | WD1001FALS-00Y6A0  | 1 TB   | 10      | 1742  | 43    | 4.50   |
| WDC       | WD2003FYYS-02W0B0  | 2 TB   | 11      | 1855  | 1     | 4.47   |
| Seagate   | ST1000NC000-1CX162 | 1 TB   | 2       | 1630  | 0     | 4.47   |
| Seagate   | ST3200021A         | 200 GB | 1       | 1624  | 0     | 4.45   |
| Seagate   | ST3300822AS        | 304 GB | 2       | 1622  | 0     | 4.45   |
| Hitachi   | HUA721010KLA330... | 1 TB   | 2       | 1886  | 3     | 4.43   |
| WDC       | WD3200YS-01PGB0    | 320 GB | 3       | 1617  | 0     | 4.43   |
| Seagate   | ST2000DL004 HD2... | 2 TB   | 3       | 1617  | 0     | 4.43   |
| WDC       | WD5000AUDX-61WNHY0 | 500 GB | 1       | 1614  | 0     | 4.42   |
| Seagate   | ST4000NM0024-1H... | 4 TB   | 6       | 1613  | 0     | 4.42   |
| WDC       | WD7500AYYS-01RCA0  | 752 GB | 5       | 1678  | 1     | 4.39   |
| WDC       | WD1600JB-22GVA0    | 160 GB | 1       | 1600  | 0     | 4.39   |
| WDC       | WD2000JB-16FUA0    | 200 GB | 1       | 1584  | 0     | 4.34   |
| WDC       | WD10SPCX-00KHST0   | 1 TB   | 1       | 1580  | 0     | 4.33   |
| Toshiba   | MQ01ABD032V        | 320 GB | 1       | 1578  | 0     | 4.33   |
| Samsung   | HD502HM            | 500 GB | 1       | 1573  | 0     | 4.31   |
| WDC       | WD2500YS-18SHB2    | 250 GB | 1       | 1566  | 0     | 4.29   |
| WDC       | WD2003FYPS-27Y2B0  | 2 TB   | 8       | 1873  | 14    | 4.29   |
| WDC       | WD40EZRX-75SPEB0   | 4 TB   | 1       | 1542  | 0     | 4.23   |
| Seagate   | ST340212AS         | 40 GB  | 5       | 1809  | 42    | 4.22   |
| WDC       | WD3200AAJS-22RYA0  | 320 GB | 4       | 1539  | 0     | 4.22   |
| Hitachi   | HUA722010CLA331    | 1 TB   | 2       | 1536  | 0     | 4.21   |
| WDC       | WD4000AAJS-65TKA0  | 400 GB | 1       | 1532  | 0     | 4.20   |
| Seagate   | ST31000424CS       | 1 TB   | 1       | 1527  | 0     | 4.19   |
| HPE       | MB0500EBNCR        | 500 GB | 1       | 1526  | 0     | 4.18   |
| Toshiba   | MG03ACA200         | 2 TB   | 6       | 1522  | 0     | 4.17   |
| Hitachi   | HDS723030ALA640    | 3 TB   | 15      | 1640  | 7     | 4.17   |
| WDC       | WD2502ABYS-23B7... | 250 GB | 2       | 1522  | 0     | 4.17   |
| Hitachi   | HUA721010KLA330    | 1 TB   | 17      | 2100  | 117   | 4.17   |
| Seagate   | ST980412ASG        | 80 GB  | 1       | 1501  | 0     | 4.11   |
| WDC       | WD2500YS-01SHB0    | 256 GB | 4       | 1563  | 7     | 4.11   |
| WDC       | WD2500AAJS-22VWA0  | 250 GB | 3       | 1496  | 0     | 4.10   |
| WDC       | WD30EFRX-68AX9N0   | 3 TB   | 49      | 1745  | 1     | 4.10   |
| Quantum   | FIREBALLlct10 05   | 5 GB   | 1       | 1486  | 0     | 4.07   |
| WDC       | WD1200JS-55NCB1    | 120 GB | 1       | 1484  | 0     | 4.07   |
| Seagate   | ST3000NM0053       | 3 TB   | 1       | 1484  | 0     | 4.07   |
| WDC       | WD2000JD-00GBB0    | 200 GB | 1       | 1482  | 0     | 4.06   |
| WDC       | WD2500AAKS-61L9A0  | 250 GB | 3       | 1474  | 0     | 4.04   |
| HP        | FB080C4080         | 80 GB  | 2       | 1472  | 0     | 4.04   |
| WDC       | WD1200JB-00REA0    | 120 GB | 2       | 1515  | 1     | 4.03   |
| WDC       | WD3200AAKX-753CA0  | 320 GB | 1       | 1471  | 0     | 4.03   |
| WDC       | WD1001FALS-00J7B0  | 1 TB   | 36      | 1994  | 3     | 4.03   |
| Seagate   | ST4000NM0085-1Y... | 4 TB   | 2       | 1468  | 0     | 4.02   |
| WDC       | WD3200BUDT-73DPZY0 | 320 GB | 1       | 1463  | 0     | 4.01   |
| Hitachi   | HUA722010ALA330    | 1 TB   | 5       | 1787  | 1     | 3.99   |
| WDC       | WD8002FRYZ-01FF2B0 | 8 TB   | 2       | 1452  | 0     | 3.98   |
| WDC       | WD1002FBYS-02A6B0  | 1 TB   | 19      | 1757  | 30    | 3.98   |
| WDC       | WD5003ABYX-18WERA0 | 500 GB | 10      | 1768  | 1     | 3.97   |
| Seagate   | MB3000EBKAB        | 3 TB   | 2       | 1447  | 0     | 3.97   |
| WDC       | WD5001FZWX-00ZHUA0 | 5 TB   | 5       | 1606  | 1     | 3.96   |
| HGST      | HDN724030ALE640    | 3 TB   | 14      | 1443  | 0     | 3.96   |
| Seagate   | ST4000VN000-1H4168 | 4 TB   | 29      | 1481  | 70    | 3.93   |
| WDC       | WD20EADS-55R6B0    | 2 TB   | 1       | 1422  | 0     | 3.90   |
| WDC       | WD2502ABYS-23B7... | 250 GB | 7       | 1833  | 2     | 3.86   |
| HGST      | HDN726050ALE610    | 5 TB   | 1       | 1409  | 0     | 3.86   |
| Seagate   | ST3320820AS_P      | 320 GB | 2       | 1408  | 0     | 3.86   |
| Hitachi   | HDT722520DLAT80    | 200 GB | 2       | 1406  | 0     | 3.85   |
| WDC       | WD3200AAKS-75SBA0  | 320 GB | 4       | 1401  | 0     | 3.84   |
| WDC       | WD2500JB-22REA0    | 250 GB | 1       | 1398  | 0     | 3.83   |
| WDC       | WD10EAVS-00D7B0    | 1 TB   | 14      | 1804  | 1     | 3.83   |
| WDC       | WD1500HLFS-01G6U3  | 150 GB | 2       | 1388  | 0     | 3.80   |
| WDC       | WD3200AAJB-00WGA0  | 320 GB | 4       | 1387  | 0     | 3.80   |
| WDC       | WD2500AAJS-00VWA0  | 250 GB | 2       | 1384  | 0     | 3.79   |
| HGST      | HUH728080ALN600    | 8 TB   | 5       | 1375  | 0     | 3.77   |
| WDC       | WD1002FBYS-50A6B0  | 1 TB   | 1       | 1374  | 0     | 3.77   |
| WDC       | WD5000AAKS-00TMA0  | 500 GB | 10      | 1457  | 2     | 3.75   |
| WDC       | WD1500HLFS-50G6U1  | 150 GB | 2       | 1364  | 0     | 3.74   |
| WDC       | WD40EURX-64WRWY0   | 4 TB   | 3       | 1361  | 0     | 3.73   |
| Hitachi   | HUA723020ALA640    | 2 TB   | 26      | 1399  | 1     | 3.72   |
| Seagate   | ST6000DM001-1XY17Z | 6 TB   | 3       | 1357  | 0     | 3.72   |
| WDC       | WD1600AAJS-61WAA0  | 160 GB | 4       | 1357  | 0     | 3.72   |
| WDC       | WD20EARS-07MVWB0   | 2 TB   | 4       | 1865  | 1     | 3.71   |
| WDC       | WD10EACS-00D6B1    | 1 TB   | 7       | 2255  | 275   | 3.70   |
| HGST      | HUS726060ALE610    | 6 TB   | 7       | 1348  | 0     | 3.70   |
| WDC       | WD20NMVW-11W68S0   | 2 TB   | 6       | 1415  | 10    | 3.68   |
| Hitachi   | HUA723020ALA640... | 2 TB   | 1       | 1337  | 0     | 3.66   |
| Seagate   | ST12000NM0007-2... | 12 TB  | 1       | 1335  | 0     | 3.66   |
| WDC       | WD2500AAKX-19U6AA0 | 250 GB | 1       | 1334  | 0     | 3.66   |
| WDC       | WD10EARX-22N0YB0   | 1 TB   | 2       | 1333  | 0     | 3.65   |
| WDC       | WD10EADS-00P8B0    | 1 TB   | 8       | 1496  | 2     | 3.64   |
| WDC       | WD5000BTKT-40MD3T0 | 500 GB | 2       | 1326  | 0     | 3.63   |
| WDC       | WD7501AALS-00E8B0  | 752 GB | 5       | 1832  | 4     | 3.63   |
| Fujitsu   | MPE3064AT          | 6 GB   | 2       | 1315  | 0     | 3.60   |
| WDC       | WD1600JD-00HBC0    | 160 GB | 3       | 1534  | 2     | 3.60   |
| Hitachi   | HDS722516VLSA80    | 164 GB | 4       | 1529  | 2     | 3.60   |
| WDC       | WD2500AAKX-08ERMA0 | 250 GB | 2       | 1311  | 0     | 3.59   |
| WDC       | WD5000AAKS-60YGA1  | 500 GB | 1       | 1311  | 0     | 3.59   |
| WDC       | WD400BD-22JMC0     | 40 GB  | 1       | 1310  | 0     | 3.59   |
| Toshiba   | MG04ACA600EY       | 6 TB   | 1       | 1307  | 0     | 3.58   |
| HGST      | HUS724040ALA640    | 4 TB   | 22      | 1339  | 93    | 3.58   |
| WDC       | WD2500AAKS-22VSA0  | 250 GB | 1       | 1305  | 0     | 3.58   |
| WDC       | WD1600JS-00MHB5    | 160 GB | 1       | 1303  | 0     | 3.57   |
| Hitachi   | HDS725050KLAT80    | 500 GB | 1       | 1303  | 0     | 3.57   |
| WDC       | WD10EVDS-63U8B1    | 1 TB   | 2       | 1302  | 0     | 3.57   |
| HGST      | HUS724030ALA640    | 3 TB   | 19      | 1414  | 3     | 3.56   |
| Seagate   | ST500DM002-1ER14C  | 500 GB | 3       | 1297  | 0     | 3.55   |
| Hitachi   | HTS545050B9SA02    | 500 GB | 1       | 1295  | 0     | 3.55   |
| Maxtor    | 6H500F0            | 500 GB | 1       | 1294  | 0     | 3.55   |
| WDC       | WD2500LPLX-75ZNTT0 | 250 GB | 1       | 1292  | 0     | 3.54   |
| Seagate   | ST6000NM0024       | 6 TB   | 4       | 1290  | 0     | 3.54   |
| WDC       | WD2001FASS-00W2B0  | 2 TB   | 6       | 1896  | 3     | 3.53   |
| HGST      | HUS724020ALA640    | 2 TB   | 41      | 1289  | 0     | 3.53   |
| Toshiba   | MQ01UBD075         | 752 GB | 1       | 1287  | 0     | 3.53   |
| WDC       | WD1200BB-00GUA0    | 120 GB | 1       | 1284  | 0     | 3.52   |
| WDC       | WD2000BB-22GUC0    | 200 GB | 1       | 1282  | 0     | 3.51   |
| Seagate   | ST320LT014-9YK142  | 320 GB | 2       | 1282  | 0     | 3.51   |
| WDC       | WD4000AAKS-00A7B0  | 400 GB | 1       | 1280  | 0     | 3.51   |
| WDC       | WD3000FYYZ-50UL1B0 | 3 TB   | 1       | 1278  | 0     | 3.50   |
| WDC       | WD6400AAKS-41H2B0  | 640 GB | 3       | 1277  | 0     | 3.50   |
| WDC       | WD1001FALS-00U9B0  | 1 TB   | 4       | 2201  | 124   | 3.50   |
| WDC       | WD15EVDS-68V9B0    | 1.5 TB | 1       | 1276  | 0     | 3.50   |
| HP        | J7989G             | 80 GB  | 1       | 1274  | 0     | 3.49   |
| HP        | MB1000GCEEK        | 1 TB   | 1       | 1272  | 0     | 3.49   |
| WDC       | WD4000FYYZ-01UL1B2 | 4 TB   | 3       | 1676  | 1060  | 3.48   |
| WDC       | WD1000DHTZ-04N21V1 | 1 TB   | 2       | 1270  | 0     | 3.48   |
| Hitachi   | HCC545025B9A300    | 250 GB | 2       | 1266  | 0     | 3.47   |
| WDC       | WD1200JS-00SGB0    | 120 GB | 3       | 1264  | 0     | 3.46   |
| Seagate   | ST3160022ACE       | 160 GB | 1       | 1263  | 0     | 3.46   |
| HGST      | HUP723020APA640    | 2 TB   | 1       | 1257  | 0     | 3.45   |
| Hitachi   | HTS421212H9AT00    | 120 GB | 2       | 2184  | 120   | 3.43   |
| Seagate   | ST3000DM001-1E6166 | 3 TB   | 8       | 1427  | 510   | 3.41   |
| Samsung   | SP0451N            | 40 GB  | 1       | 1237  | 0     | 3.39   |
| Hitachi   | HDT721075SLA360    | 752 GB | 2       | 1234  | 0     | 3.38   |
| WDC       | WD5000AAKS-65V0A0  | 500 GB | 5       | 1511  | 4     | 3.38   |
| WDC       | WD2500HHTZ-04N21V1 | 250 GB | 2       | 1226  | 0     | 3.36   |
| WDC       | WD800JD-55MSA1     | 80 GB  | 4       | 1226  | 0     | 3.36   |
| WDC       | WD4000AAJS-32TKA0  | 400 GB | 1       | 1226  | 0     | 3.36   |
| Seagate   | ST3500641AS        | 500 GB | 7       | 1994  | 33    | 3.35   |
| WDC       | WD5000AAVS-00G9B0  | 500 GB | 7       | 1406  | 2     | 3.34   |
| Seagate   | ST310211A          | 10 GB  | 2       | 1214  | 0     | 3.33   |
| Hitachi   | HDT721075SLA380    | 752 GB | 1       | 1205  | 0     | 3.30   |
| Fujitsu   | MHV2160BT PL       | 160 GB | 1       | 1202  | 0     | 3.30   |
| WDC       | WD1600HLFS-75G6U1  | 160 GB | 1       | 1200  | 0     | 3.29   |
| Hitachi   | HDS722020ALA330    | 2 TB   | 42      | 1800  | 85    | 3.29   |
| Seagate   | ST8000AS0002-1N... | 8 TB   | 103     | 1345  | 61    | 3.29   |
| WDC       | WD10EALX-759BA0    | 1 TB   | 4       | 1628  | 3     | 3.29   |
| Seagate   | ST3160828AS        | 160 GB | 1       | 1198  | 0     | 3.28   |
| MaxDig... | MD4000GBDS         | 4 TB   | 2       | 1197  | 0     | 3.28   |
| WDC       | WD5000AAKS-402AA0  | 500 GB | 6       | 1610  | 10    | 3.27   |
| Seagate   | ST8000VN0002-1Z... | 8 TB   | 5       | 1598  | 21    | 3.27   |
| WDC       | WD2500AAJS-61B4A0  | 250 GB | 2       | 1191  | 0     | 3.27   |
| WDC       | WD1200JD-00HBB0    | 120 GB | 10      | 1745  | 131   | 3.26   |
| Seagate   | ST3300622AS        | 304 GB | 3       | 1735  | 1     | 3.25   |
| WDC       | WD5000AAJS-32YFA0  | 500 GB | 1       | 1187  | 0     | 3.25   |
| WDC       | WD2000FYYZ-01UL1B2 | 2 TB   | 5       | 1307  | 1     | 3.25   |
| Seagate   | ST3300631A         | 304 GB | 1       | 1185  | 0     | 3.25   |
| HP        | MB2000GCWDA        | 2 TB   | 3       | 1181  | 0     | 3.24   |
| Seagate   | ST9250610NS        | 250 GB | 5       | 1180  | 0     | 3.23   |
| WDC       | WD3000F9YZ-09N20L0 | 3 TB   | 5       | 1673  | 1     | 3.23   |
| WDC       | WD1600AABS-56PRA0  | 160 GB | 3       | 1178  | 0     | 3.23   |
| Hitachi   | HDS728040PLA320    | 40 GB  | 4       | 1548  | 4     | 3.22   |
| WDC       | WD4000AAKS-00YGA0  | 400 GB | 6       | 1245  | 1     | 3.21   |
| WDC       | WD3200AAJB-56WGA0  | 320 GB | 3       | 1172  | 0     | 3.21   |
| WDC       | WD800BB-60JKC0     | 80 GB  | 2       | 1292  | 2     | 3.21   |
| Maxtor    | 6N040T0            | 40 GB  | 2       | 1842  | 1     | 3.21   |
| WDC       | WD3000HLFS-01G6U3  | 304 GB | 1       | 1170  | 0     | 3.21   |
| WDC       | WD3200AAKS-75B3A0  | 320 GB | 1       | 2338  | 1     | 3.20   |
| Seagate   | ST3320620NS        | 320 GB | 3       | 1312  | 1     | 3.20   |
| WDC       | WD2502ABYS-02B7A0  | 256 GB | 7       | 1421  | 12    | 3.20   |
| WDC       | WD3200AAJS-07RYA0  | 320 GB | 1       | 1168  | 0     | 3.20   |
| WDC       | WD800HLFS-75G6U1   | 80 GB  | 1       | 1168  | 0     | 3.20   |
| WDC       | WD1500AHFD-00RAR5  | 150 GB | 1       | 1164  | 0     | 3.19   |
| WDC       | WD7500BPVX-55JC3T3 | 752 GB | 1       | 1163  | 0     | 3.19   |
| WDC       | WD5000AVJB-63YUA0  | 500 GB | 1       | 1163  | 0     | 3.19   |
| Toshiba   | MK8017GSG          | 80 GB  | 1       | 1162  | 0     | 3.18   |
| WDC       | WD20EADS-00S2B0    | 2 TB   | 6       | 1185  | 1     | 3.18   |
| WDC       | WD1600JS-75NCB2    | 160 GB | 1       | 1161  | 0     | 3.18   |
| WDC       | WD4001FAEX-00MJRA0 | 4 TB   | 2       | 1160  | 0     | 3.18   |
| WDC       | WD2500JB-00GVA0    | 250 GB | 1       | 1155  | 0     | 3.16   |
| WDC       | WD2503ABYX-01WERA0 | 256 GB | 1       | 1155  | 0     | 3.16   |
| WDC       | WD20EARX-008FB0    | 2 TB   | 14      | 1221  | 1     | 3.15   |
| WDC       | WD5000AAKS-40V6A0  | 500 GB | 2       | 1149  | 0     | 3.15   |
| HGST      | HDN724040ALE640    | 4 TB   | 28      | 1204  | 72    | 3.15   |
| WDC       | WD3200LPLX-60ZNTT1 | 320 GB | 1       | 1145  | 0     | 3.14   |
| WDC       | WD10EADS-00L5B1    | 1 TB   | 80      | 1713  | 6     | 3.14   |
| WDC       | WD20EARX-22PASB0   | 2 TB   | 5       | 1144  | 0     | 3.14   |
| Samsung   | HE253GJ            | 250 GB | 1       | 1143  | 0     | 3.13   |
| WDC       | WD10EACS-00ZJB0    | 1 TB   | 10      | 1592  | 68    | 3.12   |
| WDC       | WD740ADFD-00NLR1   | 74 GB  | 2       | 1137  | 0     | 3.12   |
| WDC       | WD5003AZEX-00RKKA0 | 500 GB | 2       | 1135  | 0     | 3.11   |
| Hitachi   | HDS723030BLE640    | 3 TB   | 1       | 1135  | 0     | 3.11   |
| WDC       | MB0500EBNCR        | 500 GB | 1       | 1134  | 0     | 3.11   |
| WDC       | WD2000FYYZ-01UL1B0 | 2 TB   | 3       | 1129  | 0     | 3.10   |
| WDC       | WD50EZRZ-32RWYB1   | 5 TB   | 2       | 1128  | 0     | 3.09   |
| Seagate   | ST4000VN0001-1S... | 4 TB   | 3       | 1128  | 0     | 3.09   |
| Samsung   | HD400LD            | 400 GB | 4       | 1126  | 0     | 3.09   |
| Seagate   | ST250DM001 HD256GJ | 250 GB | 1       | 1123  | 0     | 3.08   |
| WDC       | WD4000F9YZ-09N20L1 | 4 TB   | 3       | 1122  | 0     | 3.08   |
| Fujitsu   | MHZ2250BJ FFS G2   | 250 GB | 2       | 1122  | 0     | 3.07   |
| WDC       | WD2002FYPS-01U1B0  | 2 TB   | 3       | 2771  | 137   | 3.07   |
| WDC       | WD3200AAJS-40VWA0  | 320 GB | 1       | 1118  | 0     | 3.06   |
| WDC       | WD2500JS-40MVB1    | 250 GB | 2       | 1115  | 0     | 3.06   |
| WDC       | WD40EZRX-22SPEB0   | 4 TB   | 2       | 2196  | 4     | 3.05   |
| Hitachi   | HCP725025GLA380    | 250 GB | 1       | 1111  | 0     | 3.04   |
| Hitachi   | HDS725050KLA360    | 500 GB | 10      | 1815  | 8     | 3.04   |
| Seagate   | ST3300831AS        | 304 GB | 4       | 1804  | 3     | 3.04   |
| WDC       | WD1003FBYX-88 LEN  | 1 TB   | 2       | 1478  | 1     | 3.04   |
| WDC       | WD2500AACS-00M6B0  | 250 GB | 1       | 1107  | 0     | 3.03   |
| WDC       | WD6400AACS-00G8B0  | 640 GB | 5       | 1268  | 118   | 3.03   |
| WDC       | WD2002FAEX-007BA0  | 2 TB   | 48      | 1397  | 4     | 3.03   |
| Hitachi   | HDS723020BLA642    | 2 TB   | 62      | 1303  | 98    | 3.03   |
| WDC       | WD1200BEVE-00WZT0  | 120 GB | 1       | 1103  | 0     | 3.02   |
| Hitachi   | HDS7250SASUN500... | 500 GB | 1       | 1103  | 0     | 3.02   |
| WDC       | WD5000BEKT-22KA9T0 | 500 GB | 2       | 1236  | 4     | 3.02   |
| WDC       | WD10EARS-67Y5B1    | 1 TB   | 1       | 1100  | 0     | 3.01   |
| WDC       | WD20EURX-64HYZY0   | 2 TB   | 1       | 1098  | 0     | 3.01   |
| WDC       | WD1001FALS-00J7B1  | 1 TB   | 31      | 1484  | 3     | 3.00   |
| Seagate   | ST6000AS0002-1N... | 6 TB   | 11      | 1573  | 73    | 3.00   |
| WDC       | WD2500JS-00MHB0    | 250 GB | 5       | 1155  | 1     | 2.99   |
| WDC       | WD1001FALS-41Y6A0  | 1 TB   | 5       | 1202  | 1     | 2.99   |
| WDC       | WD1600YS-01SHB1    | 164 GB | 7       | 1088  | 0     | 2.98   |
| WDC       | WD3200KS-75PFB0    | 320 GB | 2       | 1359  | 39    | 2.98   |
| WDC       | WD800JD-08LSA0     | 80 GB  | 11      | 1202  | 2     | 2.98   |
| Seagate   | ST9500620NS 81Y... | 500 GB | 1       | 1083  | 0     | 2.97   |
| Hitachi   | HDS721010CLA630    | 1 TB   | 13      | 1143  | 1     | 2.97   |
| WDC       | WD7500AARX-00N0YB0 | 752 GB | 1       | 1081  | 0     | 2.96   |
| WDC       | WD30EURX-64HYZY0   | 3 TB   | 1       | 1077  | 0     | 2.95   |
| Maxtor    | 7V250F0            | 256 GB | 2       | 1075  | 0     | 2.95   |
| Seagate   | ST1000NX0423 00... | 1 TB   | 5       | 1073  | 0     | 2.94   |
| WDC       | WD5002ABYS-02B1B0  | 500 GB | 12      | 1380  | 2     | 2.94   |
| WDC       | WD3200AZKX-00D6NA0 | 320 GB | 1       | 1073  | 0     | 2.94   |
| WDC       | WD15EVDS-63V9B1    | 1.5 TB | 3       | 1580  | 4     | 2.94   |
| WDC       | WD360ADFD-00NLR1   | 37 GB  | 2       | 1072  | 0     | 2.94   |
| Toshiba   | MG03ACA400         | 4 TB   | 7       | 1072  | 0     | 2.94   |
| Maxtor    | 6L020J1            | 20 GB  | 3       | 1213  | 2     | 2.93   |
| Toshiba   | MG03ACA300         | 3 TB   | 6       | 1471  | 7     | 2.93   |
| HGST      | HTS721050A9E630    | 500 GB | 1       | 1069  | 0     | 2.93   |
| Hitachi   | HDS721016CLA382    | 160 GB | 10      | 1458  | 102   | 2.92   |
| Seagate   | ST32000641AS       | 2 TB   | 19      | 1354  | 150   | 2.92   |
| WDC       | WD20EURX-57T0FY1   | 2 TB   | 2       | 1064  | 0     | 2.92   |
| Hitachi   | HDS721075KLA330    | 752 GB | 8       | 1312  | 13    | 2.91   |
| Fujitsu   | MHV2040BH          | 40 GB  | 3       | 1057  | 0     | 2.90   |
| WDC       | WD2500AAJS-75VWA0  | 250 GB | 3       | 1056  | 0     | 2.89   |
| Seagate   | ST2000NC001-1DY164 | 2 TB   | 8       | 1054  | 0     | 2.89   |
| Toshiba   | MK2002TSKB         | 2 TB   | 2       | 1052  | 10    | 2.88   |
| WDC       | WD2500JS-00MHB1    | 250 GB | 2       | 1052  | 0     | 2.88   |
| WDC       | WD2500YD-01NVB1    | 256 GB | 3       | 1428  | 2     | 2.88   |
| Toshiba   | MD04ACA400         | 4 TB   | 22      | 1246  | 193   | 2.88   |
| WDC       | WD3000BLFS-08YBU0  | 304 GB | 2       | 1048  | 0     | 2.87   |
| WDC       | WD3202ABYS-02B7A0  | 320 GB | 7       | 1104  | 1     | 2.87   |
| HGST      | MB6000GEBTP        | 6 TB   | 1       | 1046  | 0     | 2.87   |
| WDC       | WD1500HLFS-01G6U1  | 150 GB | 5       | 1046  | 0     | 2.87   |
| WDC       | WD3200BEKT-22F3T0  | 320 GB | 1       | 2090  | 1     | 2.86   |
| Hitachi   | HDT725025VLA380    | 250 GB | 24      | 1263  | 22    | 2.85   |
| WDC       | WD10EAVS-00M4B0    | 1 TB   | 2       | 1038  | 0     | 2.84   |
| Seagate   | MM0500EBKAE        | 500 GB | 1       | 3112  | 2     | 2.84   |
| Hitachi   | HUA723030ALA640    | 3 TB   | 29      | 1252  | 74    | 2.84   |
| Apple     | HDD HTS727575A9... | 752 GB | 3       | 1036  | 0     | 2.84   |
| WDC       | WD800BB-75FRA0     | 80 GB  | 2       | 1034  | 0     | 2.83   |
| Seagate   | ST340823A          | 40 GB  | 1       | 1034  | 0     | 2.83   |
| WDC       | WD2502ABYS-18B7A0  | 250 GB | 5       | 1361  | 2     | 2.82   |
| WDC       | WD1600AVJS-63WNA0  | 160 GB | 1       | 1027  | 0     | 2.82   |
| Hitachi   | HDS721075CLA332    | 752 GB | 6       | 1276  | 338   | 2.82   |
| Hitachi   | HDS722580VLAT20    | 82 GB  | 5       | 1256  | 108   | 2.81   |
| WDC       | WD2003FYYS-05T9B0  | 2 TB   | 1       | 1025  | 0     | 2.81   |
| Hitachi   | HDS5C3015ALA632    | 1.5 TB | 4       | 1158  | 80    | 2.80   |
| WDC       | WD4NPURX-64TPFY0   | 4 TB   | 1       | 1023  | 0     | 2.80   |
| WDC       | WD3200BUDT-63DPZY0 | 320 GB | 2       | 1159  | 4     | 2.80   |
| WDC       | WD2500JB-57REA0    | 250 GB | 1       | 1021  | 0     | 2.80   |
| Seagate   | ST320413A          | 20 GB  | 2       | 1076  | 2     | 2.80   |
| WDC       | WD800JD-60LUA0     | 80 GB  | 3       | 1020  | 0     | 2.80   |
| WDC       | WD5000AAKS-40V2B0  | 500 GB | 2       | 1020  | 0     | 2.80   |
| Seagate   | ST6000NM0024-1H... | 6 TB   | 3       | 1678  | 23    | 2.79   |
| HP        | GB0250EAFYK        | 250 GB | 2       | 1519  | 67    | 2.79   |
| WDC       | WD400LB-00DNA0     | 40 GB  | 2       | 1103  | 2     | 2.78   |
| WDC       | WD200BB-00DEA0     | 20 GB  | 1       | 1015  | 0     | 2.78   |
| WDC       | WD10EZEX-75ZF5A0   | 1 TB   | 11      | 1048  | 184   | 2.78   |
| Seagate   | ST500LM000-1EJ1... | 500 GB | 2       | 1409  | 1     | 2.78   |
| WDC       | WD5000AACS-61M6B2  | 500 GB | 3       | 2013  | 4     | 2.78   |
| Hitachi   | HDT725032VLA380    | 320 GB | 16      | 1484  | 85    | 2.78   |
| WDC       | WD1600JB-00EVA0    | 160 GB | 1       | 1012  | 0     | 2.77   |
| Toshiba   | MC04ACA200E        | 2 TB   | 1       | 1008  | 0     | 2.76   |
| WDC       | WD7500AAKS-00RBA0  | 752 GB | 10      | 1401  | 51    | 2.76   |
| WDC       | WD3200AAKS-00G3A0  | 320 GB | 6       | 1006  | 0     | 2.76   |
| WDC       | WD3000HLFS-01MZUV0 | 304 GB | 3       | 1602  | 357   | 2.75   |
| WDC       | WD20NMVW-59AV3S3   | 2 TB   | 1       | 1005  | 0     | 2.75   |
| WDC       | WD2500AAJS-75M0A0  | 250 GB | 20      | 1129  | 1     | 2.75   |
| WDC       | WD1600AABS-61PRA0  | 160 GB | 3       | 1341  | 1     | 2.75   |
| WDC       | WD2500JS-75NCB3    | 250 GB | 9       | 1307  | 15    | 2.75   |
| WDC       | WD20EARX-00ZUDB0   | 2 TB   | 4       | 1490  | 5     | 2.74   |
| Samsung   | HD204UI            | 2 TB   | 69      | 1215  | 74    | 2.74   |
| Seagate   | ST3160215ACE       | 160 GB | 7       | 1232  | 187   | 2.74   |
| WDC       | WD1600AAJS-22PSA0  | 160 GB | 19      | 1139  | 26    | 2.73   |
| Seagate   | ST1500LM003-9YH148 | 1.5 TB | 2       | 996   | 0     | 2.73   |
| WDC       | WD2500JS-60NCB1    | 250 GB | 8       | 1084  | 1     | 2.73   |
| WDC       | WD800JD-60LSA5     | 80 GB  | 25      | 1026  | 1     | 2.73   |
| Seagate   | ST3400833AS        | 400 GB | 2       | 995   | 0     | 2.73   |
| WDC       | WD6401AALS-22A7B2  | 640 GB | 1       | 993   | 0     | 2.72   |
| WDC       | WD2500LPVX-00V0TT0 | 250 GB | 1       | 992   | 0     | 2.72   |
| WDC       | WD5000KS-00MNB0    | 500 GB | 1       | 992   | 0     | 2.72   |
| WDC       | WD3200JS-63PDB1    | 320 GB | 3       | 1327  | 217   | 2.71   |
| WDC       | WD1000FYPS-01ZKB0  | 1 TB   | 1       | 989   | 0     | 2.71   |
| Hitachi   | HDS5C3020ALA632    | 2 TB   | 22      | 1196  | 27    | 2.71   |
| Apple     | HDD ST3000DM001    | 3 TB   | 2       | 985   | 0     | 2.70   |
| WDC       | WD5000AAKS-00C8A0  | 500 GB | 3       | 1253  | 62    | 2.70   |
| WDC       | WD10JPVT-16A1YT0   | 1 TB   | 3       | 984   | 0     | 2.70   |
| HGST      | HUS724030ALE640    | 3 TB   | 1       | 983   | 0     | 2.69   |
| WDC       | WD3200AAKX-221CA0  | 320 GB | 1       | 981   | 0     | 2.69   |
| Seagate   | ST32000645NS       | 2 TB   | 9       | 1397  | 10    | 2.69   |
| WDC       | WD400JB-00JJC0     | 40 GB  | 1       | 980   | 0     | 2.69   |
| WDC       | WD6400AAKS-65A7B2  | 640 GB | 27      | 1405  | 19    | 2.68   |
| Samsung   | HD040GJ-P          | 40 GB  | 1       | 975   | 0     | 2.67   |
| Toshiba   | MQ03ABB200         | 2 TB   | 2       | 975   | 0     | 2.67   |
| Quantum   | FIREBALLP KX13.6   | 16 GB  | 1       | 975   | 0     | 2.67   |
| WDC       | WD30EZRX-00SPEB0   | 3 TB   | 22      | 1077  | 12    | 2.66   |
| Hitachi   | HDS721010CLA632    | 1 TB   | 11      | 1351  | 9     | 2.66   |
| WDC       | WD10EALX-079BA1    | 1 TB   | 1       | 968   | 0     | 2.65   |
| WDC       | WD2500JS-40TGB0    | 250 GB | 1       | 966   | 0     | 2.65   |
| WDC       | WD1002FAEX-00Y9A0  | 1 TB   | 62      | 1181  | 13    | 2.65   |
| Toshiba   | MK1229GSGF         | 80 GB  | 1       | 6753  | 6     | 2.64   |
| Hitachi   | HDT725040VLA360    | 400 GB | 4       | 1323  | 6     | 2.64   |
| WDC       | WD5000AAVS-00ZTB0  | 500 GB | 15      | 1357  | 104   | 2.64   |
| Seagate   | ST4000NM0033-9Z... | 4 TB   | 33      | 1541  | 344   | 2.64   |
| HGST      | HMS5C4040ALE640    | 4 TB   | 6       | 961   | 0     | 2.63   |
| Toshiba   | MK4032GAX          | 40 GB  | 1       | 960   | 0     | 2.63   |
| Seagate   | ST1000NM0095-2D... | 1 TB   | 4       | 1306  | 509   | 2.63   |
| WDC       | WD30EZRX-00MMMB0   | 3 TB   | 44      | 1245  | 33    | 2.63   |
| WDC       | WD2000JS-00MVB1    | 200 GB | 1       | 957   | 0     | 2.62   |
| WDC       | WD1600AAJS-08B4A0  | 160 GB | 2       | 957   | 0     | 2.62   |
| WDC       | WD20EZRX-07D8PB0   | 2 TB   | 1       | 957   | 0     | 2.62   |
| WDC       | WD7502AAEX-00Z3A0  | 752 GB | 1       | 956   | 0     | 2.62   |
| WDC       | WD5000AAKS-22YGA0  | 500 GB | 4       | 1326  | 115   | 2.62   |
| Toshiba   | DT01ABA200V        | 2 TB   | 2       | 954   | 0     | 2.61   |
| WDC       | WD3000HLFS-01G6U0  | 304 GB | 2       | 953   | 0     | 2.61   |
| WDC       | WD20EARX-32PASB0   | 2 TB   | 8       | 970   | 2     | 2.61   |
| WDC       | WD1002FAEX-007BA0  | 1 TB   | 4       | 1003  | 1     | 2.61   |
| Seagate   | ST3500630AS        | 500 GB | 63      | 1509  | 255   | 2.60   |
| HGST      | HUS726020ALE614    | 2 TB   | 5       | 948   | 0     | 2.60   |
| WDC       | WD1600BB-22RDA0    | 160 GB | 2       | 947   | 0     | 2.60   |
| WDC       | WD2500AAKX-22ERMA0 | 250 GB | 2       | 946   | 0     | 2.59   |
| Quantum   | FIREBALLP AS20.5   | 20 GB  | 1       | 946   | 0     | 2.59   |
| Seagate   | ST1000VM002-1ET162 | 1 TB   | 7       | 945   | 0     | 2.59   |
| WDC       | WD2500JD-00GBB0    | 250 GB | 1       | 944   | 0     | 2.59   |
| WDC       | WD2003FZEX-00Z4SA0 | 2 TB   | 42      | 1101  | 31    | 2.58   |
| WDC       | WD1001FALS-41Y6A1  | 1 TB   | 1       | 938   | 0     | 2.57   |
| WDC       | WD5000AAKB-00YSA0  | 500 GB | 2       | 935   | 0     | 2.56   |
| Seagate   | ST500LM024-1RS152  | 500 GB | 2       | 932   | 0     | 2.56   |
| WDC       | WD20EURS-63S48Y0   | 2 TB   | 11      | 1225  | 186   | 2.54   |
| Seagate   | ST8000NM0055-1R... | 8 TB   | 22      | 926   | 0     | 2.54   |
| Seagate   | OOS1000G           | 1 TB   | 1       | 925   | 0     | 2.54   |
| Seagate   | ST1000NM0011 43... | 1 TB   | 1       | 925   | 0     | 2.53   |
| WDC       | WD1600JS-55MHB1    | 160 GB | 3       | 924   | 0     | 2.53   |
| WDC       | WD800JB-00DUA3     | 80 GB  | 1       | 923   | 0     | 2.53   |
| WDC       | WD3003FZEX-00Z4SA0 | 3 TB   | 5       | 1258  | 203   | 2.53   |
| Seagate   | ST3500630A         | 500 GB | 9       | 1489  | 26    | 2.52   |
| WDC       | WD5000AAKS-00YGA0  | 500 GB | 24      | 1147  | 3     | 2.52   |
| WDC       | WD1600JB-00REA0    | 160 GB | 9       | 1094  | 133   | 2.52   |
| Hitachi   | HTS545032B9SA02    | 320 GB | 6       | 1184  | 15    | 2.51   |
| WDC       | WD6401AALS-00L3B2  | 640 GB | 25      | 1197  | 5     | 2.51   |
| Seagate   | ST3400832AS        | 400 GB | 3       | 2361  | 86    | 2.51   |
| WDC       | WD1600BB-56RDA0    | 160 GB | 2       | 916   | 0     | 2.51   |
| WDC       | WD1003FBYX-01Y7B0  | 1 TB   | 17      | 1456  | 127   | 2.51   |
| WDC       | WD3200AAKX-603CA0  | 320 GB | 1       | 914   | 0     | 2.51   |
| HGST      | HTS725025A7E630    | 250 GB | 1       | 914   | 0     | 2.51   |
| Seagate   | ST3300622A         | 304 GB | 1       | 912   | 0     | 2.50   |
| WDC       | WD20EADS-00W4B0    | 2 TB   | 1       | 911   | 0     | 2.50   |
| WDC       | WD30EZRX-00AZ6B0   | 3 TB   | 6       | 1316  | 48    | 2.50   |
| Seagate   | ST3000DM003-1F216N | 3 TB   | 2       | 910   | 0     | 2.49   |
| WDC       | WD3200AAVS-00ZTB0  | 320 GB | 2       | 1145  | 1     | 2.49   |
| Seagate   | ST32000644NS       | 2 TB   | 16      | 1255  | 154   | 2.49   |
| Seagate   | ST91000640NS 81... | 1 TB   | 1       | 909   | 0     | 2.49   |
| WDC       | WD1001FALS-75J7B0  | 1 TB   | 3       | 1465  | 6     | 2.49   |
| WDC       | WD5000AACS-00ZUB0  | 500 GB | 17      | 1044  | 6     | 2.49   |
| WDC       | WD15EARS-00J2GB0   | 1.5 TB | 1       | 908   | 0     | 2.49   |
| WDC       | WD10EUCX-73YZ1Y0   | 1 TB   | 1       | 907   | 0     | 2.49   |
| Hitachi   | HCS5C2020ALA632    | 2 TB   | 2       | 2125  | 6     | 2.49   |
| Seagate   | ST4000NM0124-1R... | 4 TB   | 1       | 906   | 0     | 2.48   |
| Seagate   | ST3250823AS        | 250 GB | 21      | 1527  | 15    | 2.48   |
| WDC       | WD30EZRX-00DC0B0   | 3 TB   | 62      | 1129  | 32    | 2.48   |
| WDC       | WD10EACS-00D6B0    | 1 TB   | 15      | 1519  | 146   | 2.48   |
| WDC       | WD2500JS-60NCB2    | 250 GB | 3       | 903   | 0     | 2.47   |
| WDC       | WD10EARS-003BB1    | 1 TB   | 16      | 1015  | 108   | 2.47   |
| WDC       | WD10EADS-65M2B0    | 1 TB   | 12      | 1244  | 96    | 2.47   |
| WDC       | WD1600BB-00RDA0    | 160 GB | 4       | 1124  | 20    | 2.47   |
| WDC       | WD800BEVS-08RST3   | 80 GB  | 1       | 900   | 0     | 2.47   |
| WDC       | WD400BB-71DGA0     | 40 GB  | 1       | 900   | 0     | 2.47   |
| WDC       | WD3200LPVX-00V0TT0 | 320 GB | 3       | 900   | 0     | 2.47   |
| WDC       | WD3200AAKS-00YGA0  | 320 GB | 3       | 1049  | 2     | 2.47   |
| Hitachi   | HDS723020BLE640    | 2 TB   | 11      | 899   | 0     | 2.47   |
| Seagate   | ST9500620NS        | 500 GB | 2       | 1757  | 12    | 2.46   |
| WDC       | WD5001AALS-00E3A0  | 500 GB | 17      | 1254  | 72    | 2.46   |
| WDC       | WD5000BMVV-11A1CS0 | 500 GB | 1       | 897   | 0     | 2.46   |
| WDC       | WD2002FAEX-00MJRA0 | 2 TB   | 3       | 896   | 0     | 2.46   |
| Seagate   | ST4000DM000-1F2168 | 4 TB   | 142     | 1059  | 132   | 2.46   |
| WDC       | WD3200AAJS-40VWA1  | 320 GB | 3       | 1018  | 14    | 2.46   |
| Seagate   | ST3000VN000-1HJ166 | 3 TB   | 11      | 896   | 0     | 2.46   |
| WDC       | WD1002FAEX-00Z3A0  | 1 TB   | 120     | 1183  | 65    | 2.45   |
| Toshiba   | DT01ABA200         | 2 TB   | 16      | 923   | 2     | 2.44   |
| Hitachi   | HUA722050CLA330    | 500 GB | 4       | 891   | 0     | 2.44   |
| Seagate   | ST3000NC002-1DY166 | 3 TB   | 5       | 1190  | 598   | 2.44   |
| Seagate   | ST3250820AS Q      | 250 GB | 3       | 890   | 0     | 2.44   |
| HGST      | HDN721010ALE604    | 10 TB  | 1       | 889   | 0     | 2.44   |
| WDC       | WD800BB-22HEA1     | 80 GB  | 1       | 888   | 0     | 2.43   |
| HGST      | HTE541010A9E680    | 1 TB   | 2       | 913   | 509   | 2.43   |
| WDC       | WD2500AAJS-55RYA0  | 250 GB | 2       | 887   | 0     | 2.43   |
| WDC       | WD20EARX-00PASB0   | 2 TB   | 185     | 1160  | 73    | 2.43   |
| WDC       | WD1003FZEX-00RLFA0 | 1 TB   | 3       | 886   | 0     | 2.43   |
| WDC       | WD2000F9YZ-09N20L0 | 2 TB   | 5       | 1075  | 21    | 2.43   |
| WDC       | WD3200AAJB-00TYA0  | 320 GB | 4       | 885   | 0     | 2.43   |
| WDC       | WD4000KS-00MNB0    | 400 GB | 3       | 883   | 0     | 2.42   |
| Seagate   | ST91000640NS 81... | 1 TB   | 1       | 883   | 0     | 2.42   |
| WDC       | WD10EZEX-08RKKA0   | 1 TB   | 7       | 882   | 0     | 2.42   |
| WDC       | WD6400AAKS-75A7B2  | 640 GB | 8       | 1008  | 4     | 2.42   |
| WDC       | WD5000LUCT-62C26Y0 | 500 GB | 1       | 880   | 0     | 2.41   |
| WDC       | WD1600AAJS-75WAA0  | 160 GB | 2       | 880   | 0     | 2.41   |
| WDC       | WD3200JD-00KLB0    | 320 GB | 2       | 879   | 0     | 2.41   |
| Hitachi   | HDE721064SLA360    | 640 GB | 4       | 1234  | 4     | 2.41   |
| WDC       | WD7501AALS-00J7B1  | 752 GB | 11      | 1038  | 1     | 2.41   |
| Samsung   | HD162GJ            | 160 GB | 1       | 878   | 0     | 2.41   |
| Maxtor    | 6V300F0            | 304 GB | 2       | 876   | 0     | 2.40   |
| Hitachi   | HDT722520DLA380    | 200 GB | 4       | 1091  | 2     | 2.40   |
| WDC       | WD30EZRS-42KEZB0   | 3 TB   | 1       | 874   | 0     | 2.40   |
| WDC       | WD6400AAKS-65A7B0  | 640 GB | 12      | 1192  | 4     | 2.40   |
| WDC       | WD10EZEX-22RKKA0   | 1 TB   | 13      | 951   | 2     | 2.40   |
| WDC       | WD80EFAX-68LHPN0   | 8 TB   | 17      | 874   | 0     | 2.40   |
| WDC       | WD5000AADS-00L4B1  | 500 GB | 11      | 1134  | 63    | 2.39   |
| WDC       | WD15EARS-60MVWB0   | 1.5 TB | 4       | 1861  | 35    | 2.39   |
| WDC       | WD4000FYYZ-01UL1B3 | 4 TB   | 1       | 869   | 0     | 2.38   |
| WDC       | WD30EFRX-68EUZN0   | 3 TB   | 172     | 1055  | 6     | 2.38   |
| WDC       | WD20EFRX-68AX9N0   | 2 TB   | 30      | 957   | 1     | 2.38   |
| Hitachi   | HUA722010CLA630    | 1 TB   | 5       | 1411  | 2     | 2.38   |
| Magnet... | MD05000-BQDW-RO    | 500 GB | 2       | 865   | 0     | 2.37   |
| WDC       | WD800BB-75JHA0     | 80 GB  | 1       | 865   | 0     | 2.37   |
| Seagate   | ST3250620NS        | 250 GB | 18      | 1339  | 273   | 2.37   |
| WDC       | WD6400AAVS-00G9B1  | 640 GB | 3       | 1491  | 96    | 2.37   |
| HP        | MB1000EBZQB        | 1 TB   | 1       | 863   | 0     | 2.37   |
| WDC       | WD1600AAJS-00PSA0  | 160 GB | 34      | 1064  | 42    | 2.36   |
| Seagate   | ST1000NM0065-1V... | 1 TB   | 1       | 861   | 0     | 2.36   |
| WDC       | WD3200AAKX-083CA1  | 320 GB | 3       | 861   | 0     | 2.36   |
| Seagate   | ST1000LX001-1EM164 | 1 TB   | 1       | 857   | 0     | 2.35   |
| WDC       | WD40EFRX-68WT0N0   | 4 TB   | 128     | 1153  | 6     | 2.35   |
| Seagate   | ST500LX003-1AC15G  | 500 GB | 2       | 1073  | 16    | 2.34   |
| WDC       | WD800AAJS-22PSA0   | 80 GB  | 4       | 852   | 0     | 2.33   |
| WDC       | WD1600JS-55NCB1    | 160 GB | 8       | 852   | 0     | 2.33   |
| WDC       | WD1600AAJS-60PSA0  | 160 GB | 5       | 989   | 206   | 2.33   |
| WDC       | WD10EALX-759BA1    | 1 TB   | 11      | 1411  | 227   | 2.33   |
| Seagate   | ST3320413AS        | 320 GB | 25      | 1164  | 35    | 2.33   |
| WDC       | WD6400AAKS-00A7B0  | 640 GB | 17      | 1001  | 4     | 2.33   |
| WDC       | WD7501AALS-00J7B0  | 752 GB | 23      | 1213  | 86    | 2.33   |
| Hitachi   | HUA723020ALA641    | 2 TB   | 49      | 1017  | 49    | 2.32   |
| WDC       | WD15EARS-00S8B1    | 1.5 TB | 7       | 1980  | 4     | 2.32   |
| Seagate   | ST31000340NS EIT   | 1 TB   | 2       | 1676  | 124   | 2.32   |
| Hitachi   | HCC547550A9E380    | 500 GB | 1       | 844   | 0     | 2.31   |
| HGST      | HDN728080ALE604    | 8 TB   | 3       | 842   | 0     | 2.31   |
| WDC       | WD10JMVW-59AJGS3   | 1 TB   | 2       | 840   | 0     | 2.30   |
| Toshiba   | MG04ACA600E        | 6 TB   | 2       | 838   | 0     | 2.30   |
| WDC       | WD800JD-75MSA3     | 80 GB  | 36      | 1015  | 32    | 2.29   |
| WDC       | WD10EFRX-68JCSN0   | 1 TB   | 27      | 1071  | 147   | 2.29   |
| WDC       | WD10EALX-089BA0    | 1 TB   | 2       | 836   | 0     | 2.29   |
| Hitachi   | HCS5C3232SLA380    | 320 GB | 4       | 903   | 1     | 2.29   |
| Hitachi   | HTS722020K9SA00... | 200 GB | 1       | 835   | 0     | 2.29   |
| Toshiba   | DT01ABA300         | 3 TB   | 11      | 853   | 1     | 2.29   |
| Toshiba   | MK2561GSY          | 250 GB | 1       | 834   | 0     | 2.29   |
| WDC       | WD1600JS-60MHB1    | 160 GB | 7       | 974   | 4     | 2.28   |
| WDC       | WD7500AALX-009BA0  | 752 GB | 8       | 829   | 0     | 2.27   |
| WDC       | WD800AAJS-60WAA0   | 80 GB  | 2       | 828   | 0     | 2.27   |
| Seagate   | ST3750840AS        | 752 GB | 1       | 828   | 0     | 2.27   |
| Seagate   | ST10000NM0016-1... | 10 TB  | 10      | 827   | 0     | 2.27   |
| WDC       | WD1600AAJS-60WAA0  | 160 GB | 7       | 866   | 145   | 2.27   |
| WDC       | WD10EADS-00M2B0    | 1 TB   | 57      | 1231  | 67    | 2.26   |
| WDC       | WD800JD-08MSA1     | 80 GB  | 4       | 825   | 0     | 2.26   |
| WDC       | WD400BD-75LRA0     | 40 GB  | 2       | 825   | 0     | 2.26   |
| WDC       | WD800BD-88JMC0     | 80 GB  | 2       | 824   | 0     | 2.26   |
| WDC       | WD20EADS-11R6B1    | 2 TB   | 2       | 1529  | 8     | 2.26   |
| Hitachi   | HDS5C3030BLE630    | 3 TB   | 3       | 823   | 0     | 2.26   |
| WDC       | WD1501FASS-00W2B0  | 1.5 TB | 1       | 822   | 0     | 2.25   |
| Hitachi   | HDS728040PLAT20    | 41 GB  | 5       | 979   | 1     | 2.25   |
| Hitachi   | HDT725050VLA380    | 500 GB | 4       | 1315  | 11    | 2.25   |
| WDC       | WD20EURS-73TLHY0   | 2 TB   | 2       | 1360  | 2     | 2.25   |
| WDC       | WD1001FALS-00E3A0  | 1 TB   | 7       | 1386  | 236   | 2.25   |
| WDC       | WD101KRYZ-01JPDB1  | 10 TB  | 5       | 821   | 0     | 2.25   |
| WDC       | WD5000AAKX-603CA0  | 500 GB | 23      | 901   | 144   | 2.24   |
| WDC       | WD2500BEVE-00WZT0  | 250 GB | 2       | 817   | 0     | 2.24   |
| WDC       | WD400BB-00LNA0     | 40 GB  | 1       | 817   | 0     | 2.24   |
| WDC       | WD2500AAJS-08L7A0  | 250 GB | 5       | 816   | 0     | 2.24   |
| WDC       | WD1001FALS-40U9B0  | 1 TB   | 3       | 1040  | 1     | 2.23   |
| Seagate   | ST3000DM001-1ER166 | 3 TB   | 87      | 950   | 98    | 2.23   |
| Seagate   | ST3320413CS        | 320 GB | 13      | 955   | 88    | 2.23   |
| HP        | GB1000EAMYC        | 1 TB   | 2       | 814   | 0     | 2.23   |
| WDC       | WD800JD-60LSA0     | 80 GB  | 11      | 997   | 73    | 2.23   |
| WDC       | WD2500JS-55NCB1    | 250 GB | 8       | 1073  | 12    | 2.22   |
| WDC       | WD2500JB-00GVC0    | 250 GB | 2       | 811   | 0     | 2.22   |
| HGST      | HCC725050A7E630    | 500 GB | 1       | 810   | 0     | 2.22   |
| Seagate   | ST3500418ASQ       | 500 GB | 3       | 1457  | 345   | 2.22   |
| Toshiba   | MK1002TSKB         | 1 TB   | 2       | 1657  | 5     | 2.21   |
| WDC       | WD2000JS-22MHB0    | 200 GB | 5       | 1825  | 19    | 2.21   |
| Seagate   | ST3120213AS        | 120 GB | 1       | 806   | 0     | 2.21   |
| WDC       | WD50EZRX-00MVLB1   | 5 TB   | 5       | 1059  | 2     | 2.21   |
| Seagate   | ST3250820SCE       | 250 GB | 5       | 813   | 1     | 2.21   |
| WDC       | WD10EAVS-22D7B0    | 1 TB   | 3       | 1650  | 6     | 2.20   |
| Hitachi   | HTS723232L9SA62    | 320 GB | 1       | 804   | 0     | 2.20   |
| HGST      | HDN726060ALE610    | 6 TB   | 15      | 867   | 45    | 2.20   |
| Seagate   | ST4000DX002-1H2178 | 4 TB   | 2       | 801   | 0     | 2.20   |
| HGST      | HUS726040ALA610    | 4 TB   | 6       | 801   | 0     | 2.20   |
| WDC       | WD30NMVW-11C3NS4   | 3 TB   | 1       | 799   | 0     | 2.19   |
| Seagate   | ST3500414CS        | 500 GB | 20      | 1024  | 159   | 2.19   |
| WDC       | WD800JD-75JNA0     | 80 GB  | 5       | 1348  | 24    | 2.19   |
| WDC       | WD30EZRX-00D8PB0   | 3 TB   | 58      | 851   | 7     | 2.19   |
| WDC       | WD5000BMVV-11GNWS0 | 500 GB | 6       | 1011  | 15    | 2.19   |
| Hitachi   | HUA722020ALA330... | 2 TB   | 1       | 797   | 0     | 2.18   |
| Fujitsu   | MHV2060AH PL       | 64 GB  | 2       | 796   | 0     | 2.18   |
| WDC       | WD1002FBYS-18W8B0  | 1 TB   | 3       | 1371  | 1     | 2.18   |
| Seagate   | ST3320633AS        | 320 GB | 1       | 795   | 0     | 2.18   |
| WDC       | WD5000LUCT-63Y8HY0 | 500 GB | 2       | 794   | 0     | 2.18   |
| WDC       | WD5002ABYS-01B1B0  | 500 GB | 15      | 1332  | 4     | 2.17   |
| Apple     | HDD HTS541075A9... | 752 GB | 1       | 792   | 0     | 2.17   |
| WDC       | WD800AAJS-60PSA0   | 80 GB  | 3       | 1000  | 336   | 2.17   |
| Hitachi   | HDS5C1010CLA382    | 1 TB   | 12      | 963   | 20    | 2.17   |
| WDC       | WD1600ADFD-60NLR5  | 160 GB | 4       | 790   | 0     | 2.17   |
| WDC       | WD1005FBYZ-01YCBB1 | 1 TB   | 4       | 790   | 0     | 2.17   |
| Seagate   | ST3400620A         | 400 GB | 4       | 1479  | 143   | 2.16   |
| Hitachi   | HUS724030ALE641    | 3 TB   | 29      | 833   | 44    | 2.16   |
| WDC       | WD5000AAJS-22TKA0  | 500 GB | 4       | 787   | 0     | 2.16   |
| Seagate   | ST380012A          | 80 GB  | 2       | 787   | 0     | 2.16   |
| HP        | MB1000ECWCQ        | 1 TB   | 1       | 787   | 0     | 2.16   |
| WDC       | WD1600AAJB-00WRA0  | 160 GB | 3       | 1002  | 362   | 2.15   |
| WDC       | WD1600JB-00GVA0    | 160 GB | 2       | 784   | 0     | 2.15   |
| Seagate   | ST5000NM0024-1H... | 5 TB   | 4       | 2107  | 77    | 2.15   |
| WDC       | WD1600AAJS-07WAA0  | 160 GB | 5       | 1143  | 170   | 2.15   |
| Seagate   | ST6000VN0021-1Z... | 6 TB   | 1       | 783   | 0     | 2.15   |
| WDC       | WD6001FFWX-68Z39N0 | 6 TB   | 1       | 782   | 0     | 2.14   |
| WDC       | WD5000AAKS-00A7B0  | 500 GB | 44      | 1213  | 22    | 2.14   |
| WDC       | WD40EZRX-19SPEB0   | 4 TB   | 2       | 921   | 4     | 2.14   |
| Hitachi   | HCS5C3225SLA380    | 250 GB | 3       | 1073  | 3     | 2.14   |
| Seagate   | ST91603110CS       | 160 GB | 1       | 781   | 0     | 2.14   |
| Hitachi   | HDT721010SLA360    | 1 TB   | 50      | 1264  | 29    | 2.14   |
| WDC       | WD6002FRYZ-01WD5B1 | 6 TB   | 3       | 780   | 0     | 2.14   |
| WDC       | WD10EAVS-00D7B1    | 1 TB   | 33      | 1147  | 78    | 2.14   |
| WDC       | WD2500YS-01SHB1    | 250 GB | 11      | 1134  | 12    | 2.14   |
| WDC       | WD20EZRX-00D8PB0   | 2 TB   | 129     | 843   | 37    | 2.13   |
| WDC       | WD5000AAKS-07TMA0  | 500 GB | 2       | 778   | 0     | 2.13   |
| WDC       | WD400BD-75MRA1     | 40 GB  | 3       | 777   | 0     | 2.13   |
| WDC       | WD1200JB-00DUA3    | 120 GB | 2       | 1239  | 2     | 2.13   |
| WDC       | WD80EFZX-68UW8N0   | 8 TB   | 17      | 774   | 0     | 2.12   |
| WDC       | WD2500BB-00GUA0    | 250 GB | 1       | 773   | 0     | 2.12   |
| WDC       | WD5000AAJS-00YFA0  | 500 GB | 7       | 909   | 24    | 2.12   |
| Hitachi   | HTS723225L9A362    | 250 GB | 1       | 770   | 0     | 2.11   |
| WDC       | WD4003FZEX-00Z4SA0 | 4 TB   | 23      | 886   | 1     | 2.10   |
| WDC       | WD7500BPVT-35HXZT1 | 752 GB | 1       | 766   | 0     | 2.10   |
| HGST      | HMS5C4040BLE640    | 4 TB   | 12      | 765   | 0     | 2.10   |
| HP        | VB0250EAVER        | 250 GB | 17      | 1164  | 4     | 2.10   |
| WDC       | WD5001ABYS-01YNA0  | 500 GB | 3       | 764   | 0     | 2.10   |
| WDC       | WD2500JS-22NCB1    | 250 GB | 11      | 1203  | 89    | 2.09   |
| Hitachi   | HDS721612PLA380    | 120 GB | 9       | 1157  | 2     | 2.09   |
| WDC       | WD5000AAKS-75A7B2  | 500 GB | 4       | 1185  | 4     | 2.09   |
| WDC       | WD8001FFWX-68J1UN0 | 8 TB   | 4       | 760   | 0     | 2.08   |
| WDC       | WD800AAJS-00PSA0   | 80 GB  | 27      | 859   | 28    | 2.08   |
| WDC       | WD1002FBYS-01A6B0  | 1 TB   | 4       | 843   | 2     | 2.08   |
| WDC       | WD2500JD-55HBB0    | 250 GB | 2       | 1468  | 16    | 2.07   |
| WDC       | WD40EZRX-00SPEB0   | 4 TB   | 50      | 825   | 6     | 2.07   |
| Samsung   | HD300LJ            | 304 GB | 13      | 1203  | 264   | 2.07   |
| WDC       | WD3000JS-19PDB0    | 304 GB | 1       | 751   | 0     | 2.06   |
| WDC       | WD20EFRX-68EUZN0   | 2 TB   | 154     | 890   | 1     | 2.06   |
| WDC       | WD60EZRX-00MVLB1   | 6 TB   | 18      | 893   | 2     | 2.05   |
| WDC       | WD5000AAKS-07YGA0  | 500 GB | 5       | 805   | 1     | 2.05   |
| WDC       | WD7500AACS-00D6B1  | 752 GB | 5       | 1014  | 3     | 2.05   |
| Seagate   | ST3000VN007-2E4166 | 3 TB   | 9       | 746   | 0     | 2.05   |
| Seagate   | ST4000DM006-2G5107 | 4 TB   | 2       | 745   | 0     | 2.04   |
| Quantum   | FIREBALLP AS40.0   | 40 GB  | 1       | 744   | 0     | 2.04   |
| WDC       | WD6001FZWX-00A2VA0 | 6 TB   | 7       | 744   | 0     | 2.04   |
| Seagate   | ST3750640A         | 752 GB | 2       | 1111  | 1025  | 2.04   |
| WDC       | WD10EURX-61C57Y0   | 1 TB   | 1       | 744   | 0     | 2.04   |
| WDC       | WD6001F4PZ-49CWHM0 | 6 TB   | 1       | 743   | 0     | 2.04   |
| WDC       | WD5000HHTZ-04N21V0 | 500 GB | 9       | 805   | 1     | 2.03   |
| HGST      | HUH721010ALN600    | 10 TB  | 4       | 742   | 0     | 2.03   |
| Seagate   | ST2000DL003-9VT166 | 2 TB   | 127     | 969   | 136   | 2.03   |
| Hitachi   | HDS721050CLA662    | 500 GB | 27      | 830   | 41    | 2.03   |
| Hitachi   | HDS723015BLA642    | 1.5 TB | 9       | 911   | 22    | 2.03   |
| Seagate   | ST4000NM0245-1Z... | 4 TB   | 7       | 838   | 2     | 2.02   |
| WDC       | WD2500AAJS-00VTA0  | 250 GB | 28      | 912   | 60    | 2.02   |
| WDC       | WD20EARS-00S8B1    | 2 TB   | 12      | 1057  | 2     | 2.02   |
| WDC       | WD5002AALX-00J37A0 | 500 GB | 25      | 993   | 44    | 2.02   |
| Hitachi   | HDT721032SLA380    | 320 GB | 9       | 917   | 260   | 2.02   |
| WDC       | WD1600JS-75NCB3    | 160 GB | 6       | 1233  | 2     | 2.02   |
| Apple     | HDD ST500LM012     | 500 GB | 3       | 735   | 0     | 2.01   |
| WDC       | WD2000F9YZ-09N20L1 | 2 TB   | 1       | 733   | 0     | 2.01   |
| Seagate   | ST3320620AS        | 320 GB | 159     | 1192  | 272   | 2.01   |
| WDC       | WD7500BPVT-80HXZT1 | 752 GB | 2       | 1049  | 3     | 2.01   |
| Hitachi   | HDS5C3030ALA630    | 3 TB   | 8       | 1251  | 3     | 2.01   |
| WDC       | WD5003ABYX-01WERA2 | 500 GB | 2       | 732   | 0     | 2.01   |
| Seagate   | ST2000VN000-1HJ164 | 2 TB   | 8       | 732   | 0     | 2.01   |
| Samsung   | HE103SJ            | 1 TB   | 3       | 2260  | 41    | 2.00   |
| HP        | MB2000EBZQC        | 2 TB   | 4       | 781   | 39    | 2.00   |
| WDC       | WD1200JB-00EVA0    | 120 GB | 4       | 731   | 0     | 2.00   |
| Seagate   | ST3250824AS        | 250 GB | 33      | 1054  | 506   | 2.00   |
| WDC       | WD2500KS-00MJB0    | 250 GB | 32      | 1021  | 15    | 2.00   |
| Seagate   | ST500NM0011        | 500 GB | 20      | 1397  | 51    | 2.00   |
| WDC       | WD10EZEX-00KUWA0   | 1 TB   | 33      | 836   | 1     | 2.00   |
| HGST      | HDN724020ALE640    | 2 TB   | 1       | 729   | 0     | 2.00   |
| WDC       | WD5000AAKS-65A7B2  | 500 GB | 2       | 729   | 0     | 2.00   |
| Hitachi   | HUA722020ALA331    | 2 TB   | 15      | 1450  | 6     | 2.00   |
| WDC       | WD2500AAKX-753CA1  | 250 GB | 26      | 1047  | 43    | 1.99   |
| WDC       | WD3200AAJS-65M0A0  | 320 GB | 6       | 1044  | 4     | 1.99   |
| Seagate   | ST340014AS         | 40 GB  | 8       | 1373  | 457   | 1.99   |
| WDC       | WD20EZRX-00DC0B0   | 2 TB   | 58      | 916   | 30    | 1.99   |
| Seagate   | ST2000DL001-9VT156 | 2 TB   | 22      | 1202  | 359   | 1.99   |
| HGST      | HUS722T2TALA604    | 2 TB   | 4       | 724   | 0     | 1.98   |
| Maxtor    | STM380215A         | 80 GB  | 9       | 956   | 209   | 1.98   |
| WDC       | WD400BD-60LRA0     | 40 GB  | 1       | 723   | 0     | 1.98   |
| WDC       | WD2500HHTZ-04N21V0 | 250 GB | 9       | 777   | 1     | 1.98   |
| WDC       | WD7501AALS-75J7B0  | 752 GB | 1       | 723   | 0     | 1.98   |
| Seagate   | ST2000DM001-1E6164 | 2 TB   | 11      | 963   | 94    | 1.98   |
| WDC       | WD800AAJS-00L7A0   | 80 GB  | 2       | 722   | 0     | 1.98   |
| Seagate   | ST1000NM0011       | 1 TB   | 22      | 1627  | 27    | 1.98   |
| Hitachi   | HDS721010CLA332    | 1 TB   | 175     | 1116  | 87    | 1.98   |
| WDC       | WD15EADS-00P8B0    | 1.5 TB | 18      | 1420  | 7     | 1.97   |
| Seagate   | ST9320421ASG       | 320 GB | 2       | 887   | 1     | 1.97   |
| Fujitsu   | MHV2100AH          | 100 GB | 2       | 719   | 0     | 1.97   |
| HGST      | HCC545032A7E380    | 320 GB | 1       | 719   | 0     | 1.97   |
| MediaMax  | WL1000GSA6454G     | 1 TB   | 2       | 717   | 0     | 1.97   |
| WDC       | WD10EZEX-00ER1A0   | 1 TB   | 6       | 717   | 0     | 1.97   |
| Seagate   | ST1000VX001-1Z4102 | 1 TB   | 3       | 717   | 0     | 1.97   |
| Seagate   | ST3500630AS P      | 500 GB | 1       | 717   | 0     | 1.96   |
| WDC       | WD2500AAKS-00L9A0  | 250 GB | 12      | 1050  | 4     | 1.96   |
| Seagate   | ST5000DM000-1FK178 | 5 TB   | 18      | 856   | 101   | 1.96   |
| WDC       | WD5003ABYX-50WERA1 | 500 GB | 1       | 714   | 0     | 1.96   |
| WDC       | WD5000BEVT-16A0RT0 | 500 GB | 1       | 713   | 0     | 1.95   |
| WDC       | WD40PURX-64GVNY0   | 4 TB   | 4       | 713   | 0     | 1.95   |
| WDC       | WD6000HLHX-01JJPV0 | 600 GB | 13      | 1188  | 11    | 1.95   |
| WDC       | WD800BB-00DKA0     | 80 GB  | 4       | 987   | 1     | 1.95   |
| WDC       | WD1600JS-58NCB1    | 160 GB | 1       | 712   | 0     | 1.95   |
| Samsung   | HD083GJ            | 80 GB  | 5       | 712   | 0     | 1.95   |
| Toshiba   | MG04ACA400N        | 4 TB   | 1       | 711   | 0     | 1.95   |
| WDC       | WD80EZZX-11CSGA0   | 8 TB   | 6       | 711   | 0     | 1.95   |
| Samsung   | HD103SJ            | 1 TB   | 182     | 975   | 35    | 1.95   |
| WDC       | WD200BB-32CFC0     | 20 GB  | 1       | 709   | 0     | 1.94   |
| WDC       | WD7500AADS-00M2B0  | 752 GB | 24      | 1185  | 27    | 1.94   |
| WDC       | WD1200PD-00FZB0    | 120 GB | 1       | 706   | 0     | 1.94   |
| WDC       | WD2500AAKX-60U6AA0 | 250 GB | 10      | 963   | 71    | 1.94   |
| Toshiba   | MQ01ABD100R        | 1 TB   | 1       | 706   | 0     | 1.94   |
| WDC       | WD2003FYYS-02W0B1  | 2 TB   | 9       | 1061  | 23    | 1.93   |
| WDC       | WD20EARS-00MVWB0   | 2 TB   | 114     | 1268  | 135   | 1.93   |
| Seagate   | ST12000NE0007-2... | 12 TB  | 3       | 704   | 0     | 1.93   |
| WDC       | WD2500BEVS-22VAT0  | 250 GB | 1       | 700   | 0     | 1.92   |
| Seagate   | ST3160215SCE       | 160 GB | 3       | 725   | 2     | 1.92   |
| WDC       | WD800BB-22JHA0     | 80 GB  | 3       | 1391  | 19    | 1.91   |
| WDC       | WD5000BPKX-75HPJT0 | 500 GB | 3       | 698   | 0     | 1.91   |
| WDC       | WD2000JD-00HBB0    | 200 GB | 8       | 1481  | 3     | 1.91   |
| WDC       | WD3200BEKT-00PVMT0 | 320 GB | 5       | 697   | 0     | 1.91   |
| Seagate   | ST3000NM0033-9Z... | 3 TB   | 6       | 841   | 3     | 1.91   |
| Seagate   | ST3160212A         | 160 GB | 16      | 931   | 56    | 1.91   |
| WDC       | WD6400BPVT-35HXZT1 | 640 GB | 2       | 696   | 0     | 1.91   |
| WDC       | WD2500LPVT-00G33T0 | 250 GB | 1       | 696   | 0     | 1.91   |
| WDC       | WD5001AALS-00L3B2  | 500 GB | 43      | 980   | 22    | 1.91   |
| WDC       | WD6400AAKS-65Z7B0  | 640 GB | 7       | 1181  | 5     | 1.91   |
| Maxtor    | STM3160215A        | 160 GB | 14      | 729   | 220   | 1.90   |
| WDC       | WD1600AAJS-07PSA0  | 160 GB | 4       | 1332  | 7     | 1.90   |
| WDC       | WD10EADS-11M2B2    | 1 TB   | 9       | 1100  | 5     | 1.90   |
| WDC       | WD2500BMVV-11DCLS0 | 250 GB | 1       | 694   | 0     | 1.90   |
| WDC       | WD10TMVW-11ZSMS5   | 1 TB   | 12      | 847   | 326   | 1.90   |
| WDC       | WD800JD-22JNA0     | 80 GB  | 2       | 692   | 0     | 1.90   |
| WDC       | WD3200AAJS-65VWA0  | 320 GB | 3       | 692   | 0     | 1.90   |
| WDC       | WD5000BMVW-11AJGS0 | 500 GB | 1       | 692   | 0     | 1.90   |
| WDC       | WD3200BEVE-00A0HT0 | 320 GB | 3       | 691   | 0     | 1.90   |
| WDC       | WD7500AACS-65D6B0  | 752 GB | 3       | 830   | 5     | 1.89   |
| WDC       | WD2003FYYS-20W0B0  | 2 TB   | 2       | 690   | 0     | 1.89   |
| Seagate   | ST2000NP0011       | 2 TB   | 2       | 1260  | 1552  | 1.89   |
| Hitachi   | HDS721010KLA330    | 1 TB   | 15      | 1095  | 14    | 1.89   |
| WDC       | WD4000YS-01MPB1    | 400 GB | 2       | 686   | 0     | 1.88   |
| Seagate   | ST340215AS         | 40 GB  | 1       | 686   | 0     | 1.88   |
| Seagate   | ST960813AS         | 64 GB  | 3       | 873   | 4     | 1.88   |
| Fujitsu   | MHZ2080BH G2       | 80 GB  | 1       | 684   | 0     | 1.88   |
| WDC       | WD5000BPKT-08PK4T0 | 500 GB | 1       | 683   | 0     | 1.87   |
| WDC       | WD800JD-00LSA0     | 80 GB  | 25      | 914   | 9     | 1.87   |
| WDC       | WD2500AAJS-22RYA0  | 250 GB | 2       | 771   | 213   | 1.87   |
| Seagate   | ST6000NE0023-2E... | 6 TB   | 1       | 681   | 0     | 1.87   |
| Seagate   | ST4000DM005-2DP166 | 4 TB   | 42      | 699   | 40    | 1.86   |
| HGST      | HDN726060ALE614    | 6 TB   | 8       | 819   | 1     | 1.86   |
| WDC       | WD10EZEX-00ZF5A0   | 1 TB   | 28      | 806   | 82    | 1.86   |
| WDC       | WD40EMAZ-51TKPB0   | 4 TB   | 1       | 679   | 0     | 1.86   |
| Hitachi   | HUA721010KLA330... | 1 TB   | 1       | 2715  | 3     | 1.86   |
| HGST      | HUS724040ALE640    | 4 TB   | 10      | 678   | 0     | 1.86   |
| Samsung   | HD502IJ            | 500 GB | 61      | 1119  | 192   | 1.86   |
| WDC       | WD1502FAEX-007BA0  | 1.5 TB | 9       | 810   | 20    | 1.85   |
| WDC       | WD800BB-63JKC0     | 80 GB  | 1       | 676   | 0     | 1.85   |
| WDC       | WD15EARS-22Z5B1    | 1.5 TB | 3       | 675   | 0     | 1.85   |
| WDC       | WD1003FBYZ-010FB0  | 1 TB   | 23      | 741   | 2     | 1.85   |
| WDC       | WD10EARS-00MVWB0   | 1 TB   | 57      | 1332  | 82    | 1.85   |
| Hitachi   | HUS724030ALA640    | 3 TB   | 3       | 1113  | 1     | 1.85   |
| Seagate   | ST4000NE0025-2E... | 4 TB   | 4       | 673   | 0     | 1.84   |
| WDC       | WD800BB-75DKA0     | 80 GB  | 1       | 672   | 0     | 1.84   |
| WDC       | WD1200JS-55MHB0    | 120 GB | 2       | 671   | 0     | 1.84   |
| WDC       | WD10EUCX-63YZ1Y0   | 1 TB   | 2       | 670   | 0     | 1.84   |
| WDC       | WD5000LPVT-60G33T0 | 500 GB | 1       | 670   | 0     | 1.84   |
| WDC       | WD3200AAKS-75VYA0  | 320 GB | 3       | 670   | 0     | 1.84   |
| WDC       | WD3200AAJS-40RYA0  | 320 GB | 2       | 1197  | 389   | 1.83   |
| Seagate   | ST2000DM001-1CH164 | 2 TB   | 245     | 816   | 102   | 1.83   |
| Hitachi   | HDT721032SLA360    | 320 GB | 32      | 1151  | 11    | 1.83   |
| WDC       | WD10EARX-00N0YB0   | 1 TB   | 80      | 842   | 19    | 1.83   |
| WDC       | WD1502FYPS-01U1B1  | 1.5 TB | 1       | 667   | 0     | 1.83   |
| WDC       | WD40EZRZ-00WN9B0   | 4 TB   | 27      | 713   | 1     | 1.83   |
| WDC       | WD2500AAKX-083CA1  | 250 GB | 18      | 1004  | 3     | 1.82   |
| WDC       | WD2000JD-22HBC0    | 200 GB | 3       | 1330  | 4     | 1.82   |
| Seagate   | ST1000NX0423       | 1 TB   | 5       | 665   | 0     | 1.82   |
| WDC       | WD20EARS-14MVWB0   | 2 TB   | 3       | 664   | 0     | 1.82   |
| WDC       | WD30EURS-63R8UY0   | 3 TB   | 2       | 664   | 0     | 1.82   |
| Seagate   | ST4000VM000-1F3168 | 4 TB   | 5       | 663   | 0     | 1.82   |
| Maxtor    | 2R010H1            | 10 GB  | 1       | 1326  | 1     | 1.82   |
| WDC       | WD2000JB-00REA0    | 200 GB | 4       | 885   | 1     | 1.82   |
| Seagate   | ST6000DM004-2EH11C | 6 TB   | 3       | 662   | 0     | 1.82   |
| WDC       | WD20EARS-42S0XB0   | 2 TB   | 2       | 662   | 0     | 1.81   |
| WDC       | WD1200JD-00FYB0    | 120 GB | 1       | 661   | 0     | 1.81   |
| Toshiba   | DT01ACA300         | 3 TB   | 146     | 731   | 39    | 1.81   |
| WDC       | WD1600AAJS-07M0A0  | 160 GB | 11      | 1054  | 2     | 1.81   |
| Seagate   | ST3250824SCE       | 250 GB | 2       | 658   | 0     | 1.81   |
| Seagate   | ST380815AS         | 80 GB  | 197     | 912   | 209   | 1.80   |
| WDC       | WD1001FALS-403AA0  | 1 TB   | 8       | 899   | 4     | 1.80   |
| WDC       | WD1600AVBS-63SVA0  | 160 GB | 1       | 658   | 0     | 1.80   |
| WDC       | WD5003ABYZ-011FA0  | 500 GB | 17      | 811   | 4     | 1.80   |
| WDC       | WD5000BPVT-75HXZT1 | 500 GB | 1       | 657   | 0     | 1.80   |
| WDC       | WD1001FALS-00E8B0  | 1 TB   | 14      | 1129  | 161   | 1.80   |
| Seagate   | ST8000VN0022-2E... | 8 TB   | 52      | 768   | 7     | 1.80   |
| Seagate   | ST2000DM001-1ER164 | 2 TB   | 258     | 765   | 76    | 1.80   |
| WDC       | WD2500JS-00NCB1    | 250 GB | 13      | 955   | 26    | 1.80   |
| HGST      | HDS724040ALE640    | 4 TB   | 7       | 1136  | 289   | 1.80   |
| WDC       | WD1600JS-98NCB1    | 160 GB | 1       | 655   | 0     | 1.80   |
| WDC       | WD10EURX-63C57Y0   | 1 TB   | 8       | 850   | 1     | 1.80   |
| WDC       | WD3200BPVT-75JJ5T0 | 320 GB | 7       | 686   | 1     | 1.79   |
| WDC       | WD5000AAKS-07V0A0  | 500 GB | 1       | 654   | 0     | 1.79   |
| WDC       | WD1600BEKT-66F3T2  | 160 GB | 2       | 654   | 0     | 1.79   |
| WDC       | WD5000AAKS-00Z7B0  | 500 GB | 1       | 652   | 0     | 1.79   |
| Seagate   | ST3400620AS        | 400 GB | 31      | 1171  | 84    | 1.78   |
| WDC       | WD400BD-60JPA0     | 40 GB  | 1       | 651   | 0     | 1.78   |
| WDC       | WD2003FZEX-00SRLA0 | 2 TB   | 53      | 665   | 2     | 1.78   |
| Hitachi   | HDS722580VLSA80    | 82 GB  | 3       | 1101  | 671   | 1.78   |
| Toshiba   | MQ01UBB200         | 2 TB   | 8       | 832   | 260   | 1.78   |
| WDC       | WD6400AAKS-22A7B0  | 640 GB | 19      | 1158  | 57    | 1.78   |
| Seagate   | ST980812AS         | 80 GB  | 1       | 647   | 0     | 1.77   |
| WDC       | WD5000AAJS-00A8B0  | 500 GB | 5       | 816   | 2     | 1.77   |
| Toshiba   | DT01ABA050V        | 500 GB | 2       | 646   | 0     | 1.77   |
| WDC       | WD10EADS-11M2B1    | 1 TB   | 6       | 1060  | 13    | 1.77   |
| WDC       | WD3200AAJS-65RYA0  | 320 GB | 3       | 644   | 0     | 1.76   |
| WDC       | WD1001FALS-19J7B0  | 1 TB   | 1       | 641   | 0     | 1.76   |
| WDC       | WD10EALX-009BA0    | 1 TB   | 91      | 933   | 28    | 1.76   |
| Seagate   | ST10000DM0004      | 10 TB  | 2       | 640   | 0     | 1.76   |
| Samsung   | HD103SI            | 1 TB   | 82      | 1089  | 269   | 1.75   |
| WDC       | WD10EZEX-00UD2A0   | 1 TB   | 13      | 709   | 68    | 1.75   |
| Seagate   | ST6000VX0023-2E... | 6 TB   | 4       | 655   | 4     | 1.75   |
| Seagate   | ST3802110AS        | 80 GB  | 4       | 719   | 29    | 1.75   |
| WDC       | WD800JB-00ETA0     | 80 GB  | 5       | 1354  | 273   | 1.75   |
| WDC       | WD6400AAKS-00A7B2  | 640 GB | 8       | 693   | 1     | 1.75   |
| WDC       | WD1600JS-98MHB0    | 160 GB | 1       | 638   | 0     | 1.75   |
| WDC       | WD10EALS-00Z8A0    | 1 TB   | 34      | 981   | 44    | 1.75   |
| WDC       | WD1003FZEX-00MK2A0 | 1 TB   | 101     | 764   | 11    | 1.75   |
| WDC       | WD60EFRX-68MYMN1   | 6 TB   | 16      | 918   | 44    | 1.75   |
| Hitachi   | HDT725050VLA360    | 500 GB | 9       | 951   | 21    | 1.75   |
| WDC       | WD5000LPVT-75G33T0 | 500 GB | 8       | 749   | 20    | 1.74   |
| WDC       | WD1004FBYZ-01YCBB1 | 1 TB   | 5       | 634   | 0     | 1.74   |
| WDC       | WD1002FBYS-43P1B0  | 1 TB   | 2       | 1021  | 39    | 1.74   |
| WDC       | WD1600BEVS-08VAT2  | 160 GB | 9       | 753   | 1     | 1.74   |
| WDC       | WD1600BEVT-11ZCT0  | 160 GB | 1       | 633   | 0     | 1.74   |
| Seagate   | ST3160815AS        | 160 GB | 248     | 894   | 316   | 1.74   |
| WDC       | WD3200AAKS-22SBA0  | 320 GB | 1       | 633   | 0     | 1.73   |
| WDC       | WD10EARS-22Y5B1    | 1 TB   | 31      | 1099  | 75    | 1.73   |
| WDC       | WD7500BPVT-16HXZT3 | 752 GB | 1       | 632   | 0     | 1.73   |
| Seagate   | ST640LM000 HM641JI | 640 GB | 6       | 632   | 0     | 1.73   |
| Seagate   | ST4000DX001-1CE168 | 4 TB   | 20      | 821   | 39    | 1.73   |
| Hitachi   | HTS723220L9A360    | 200 GB | 1       | 630   | 0     | 1.73   |
| WDC       | WD5003ABYX-01WERA0 | 500 GB | 13      | 999   | 4     | 1.73   |
| Toshiba   | MK1265GSX H        | 120 GB | 1       | 630   | 0     | 1.73   |
| WDC       | WD10EFRX-68PJCN0   | 1 TB   | 40      | 739   | 1     | 1.73   |
| Seagate   | ST3200820AS        | 200 GB | 29      | 1018  | 513   | 1.72   |
| Seagate   | ST2000VX000-1CU164 | 2 TB   | 17      | 833   | 239   | 1.72   |
| WDC       | WD3001FFSX-68JNUN0 | 3 TB   | 2       | 628   | 0     | 1.72   |
| Seagate   | ST4000LM016-1N2170 | 4 TB   | 14      | 628   | 0     | 1.72   |
| Seagate   | ST2000VX000-1ES164 | 2 TB   | 11      | 628   | 0     | 1.72   |
| WDC       | WD15EADS-11P8B2    | 1.5 TB | 2       | 628   | 0     | 1.72   |
| WDC       | WD2002FYPS-02W3B0  | 2 TB   | 6       | 753   | 3     | 1.72   |
| WDC       | WD7500BPKX-60HPJT0 | 752 GB | 1       | 627   | 0     | 1.72   |
| WDC       | WD4000BEVT-11ZAT0  | 400 GB | 1       | 626   | 0     | 1.72   |
| Hitachi   | HUA723030ALA641    | 3 TB   | 7       | 626   | 0     | 1.72   |
| WDC       | WD30PURX-64P6ZY0   | 3 TB   | 9       | 925   | 21    | 1.72   |
| WDC       | WD15EADS-00R6B0    | 1.5 TB | 1       | 625   | 0     | 1.71   |
| WDC       | WD2500AAKS-00VSA0  | 250 GB | 28      | 847   | 15    | 1.71   |
| Seagate   | ST1000DL002-9TT153 | 1 TB   | 51      | 1101  | 297   | 1.71   |
| WDC       | WD5000AACS-00G8B1  | 500 GB | 16      | 964   | 3     | 1.71   |
| WDC       | WD20EURS-73S48Y0   | 2 TB   | 1       | 623   | 0     | 1.71   |
| WDC       | WD5003AZEX-00MK2A0 | 500 GB | 16      | 659   | 1     | 1.71   |
| Seagate   | ST9640423AS        | 640 GB | 6       | 1138  | 254   | 1.71   |
| Hitachi   | HDS5C1050CLA382    | 500 GB | 13      | 829   | 106   | 1.71   |
| WDC       | WD360GD-00FLC0     | 37 GB  | 1       | 622   | 0     | 1.70   |
| WDC       | WD400BD-23JMC0     | 40 GB  | 1       | 1866  | 2     | 1.70   |
| WDC       | WD10EZEX-22BN5A0   | 1 TB   | 37      | 666   | 1     | 1.70   |
| WDC       | WD6002FFWX-68TZ4N0 | 6 TB   | 2       | 620   | 0     | 1.70   |
| WDC       | WD20SPZX-22CRAT0   | 2 TB   | 1       | 620   | 0     | 1.70   |
| Seagate   | ST3250620AS        | 250 GB | 64      | 979   | 317   | 1.70   |
| WDC       | WD1600AAJS-55PSA0  | 160 GB | 1       | 620   | 0     | 1.70   |
| WDC       | WD10EADX-22TDHB0   | 1 TB   | 17      | 984   | 69    | 1.70   |
| Toshiba   | MK1229GSG          | 120 GB | 1       | 619   | 0     | 1.70   |
| Hitachi   | HDP725032GLA360    | 320 GB | 24      | 955   | 67    | 1.70   |
| Seagate   | ST3160812AS        | 160 GB | 58      | 998   | 423   | 1.69   |
| Seagate   | ST31000521AS       | 1 TB   | 1       | 618   | 0     | 1.69   |
| WDC       | WD1600BEVS-75RST0  | 160 GB | 3       | 618   | 0     | 1.69   |
| Seagate   | ST250LT007-9ZV14C  | 250 GB | 5       | 771   | 122   | 1.69   |
| WDC       | WD2500BEVS-26VAT0  | 250 GB | 3       | 617   | 0     | 1.69   |
| WDC       | WD1500HLFS-01MZUV0 | 150 GB | 3       | 894   | 1     | 1.69   |
| WDC       | WD3200AAJS-00G0A0  | 320 GB | 1       | 617   | 0     | 1.69   |
| Seagate   | ST1000DM005 HD1... | 1 TB   | 19      | 701   | 2     | 1.69   |
| Seagate   | ST3160318AS        | 160 GB | 95      | 868   | 66    | 1.69   |
| WDC       | WD10JPVX-08JC3T5   | 1 TB   | 16      | 750   | 5     | 1.69   |
| WDC       | WD4000F9YZ-09N20L0 | 4 TB   | 2       | 616   | 0     | 1.69   |
| WDC       | WD10EURX-63FH1Y0   | 1 TB   | 9       | 629   | 1     | 1.69   |
| Seagate   | ST1000NM0033-9Z... | 1 TB   | 43      | 854   | 119   | 1.69   |
| Seagate   | ST2000DX001-1NS164 | 2 TB   | 23      | 728   | 44    | 1.69   |
| WDC       | WD3000HLFS-75G6U1  | 304 GB | 3       | 873   | 2     | 1.68   |
| WDC       | WD4001FFSX-68JNUN0 | 4 TB   | 3       | 614   | 0     | 1.68   |
| WDC       | WD5000AAKS-65YGA0  | 500 GB | 9       | 918   | 11    | 1.68   |
| Toshiba   | HDWA120            | 2 TB   | 8       | 614   | 0     | 1.68   |
| Seagate   | ST3000VN000-1H4167 | 3 TB   | 5       | 614   | 0     | 1.68   |
| WDC       | WD10EZEX-08M2NA0   | 1 TB   | 123     | 662   | 3     | 1.68   |
| Hitachi   | HCS5C1032CLA382    | 320 GB | 2       | 883   | 2     | 1.68   |
| WDC       | WD800JD-00MSA1     | 80 GB  | 15      | 825   | 16    | 1.68   |
| Seagate   | ST340014A          | 40 GB  | 100     | 844   | 31    | 1.68   |
| WDC       | WD5000AAKS-00V0A0  | 500 GB | 4       | 675   | 2     | 1.68   |
| Toshiba   | HDWE150            | 5 TB   | 26      | 641   | 1     | 1.68   |
| Hitachi   | HDS5C4040ALE630    | 4 TB   | 5       | 612   | 0     | 1.68   |
| HGST      | HUS726020ALA610    | 2 TB   | 6       | 611   | 0     | 1.68   |
| Maxtor    | 6V160E0            | 160 GB | 13      | 649   | 1     | 1.67   |
| WDC       | WD6400BPVT-24HXZT1 | 640 GB | 3       | 961   | 340   | 1.67   |
| WDC       | WD800JD-00LUA0     | 80 GB  | 1       | 610   | 0     | 1.67   |
| WDC       | WD10EZRX-00A8LB0   | 1 TB   | 74      | 788   | 27    | 1.67   |
| HP        | MB1000GDUNU        | 1 TB   | 1       | 609   | 0     | 1.67   |
| WDC       | WD6400AACS-00G8B1  | 640 GB | 12      | 912   | 21    | 1.67   |
| WDC       | WD20EARX-00MMMB0   | 2 TB   | 3       | 1109  | 5     | 1.67   |
| Samsung   | HD103UJ            | 1 TB   | 107     | 1242  | 208   | 1.67   |
| Seagate   | ST31000526SV       | 1 TB   | 3       | 769   | 343   | 1.67   |
| WDC       | WD3200AAKS-00UU3A0 | 320 GB | 18      | 932   | 63    | 1.66   |
| ExcelStor | J9250S             | 250 GB | 5       | 677   | 1     | 1.66   |
| WDC       | WD3200AAJS-00VWA0  | 320 GB | 13      | 663   | 36    | 1.66   |
| WDC       | WD20EZRX-60D8PB0   | 2 TB   | 2       | 604   | 0     | 1.66   |
| WDC       | WD3000JS-60PDB0    | 304 GB | 2       | 603   | 0     | 1.65   |
| WDC       | WD2500LPLX-00ZNTT0 | 250 GB | 1       | 603   | 0     | 1.65   |
| WDC       | WD800AAJS-00WAA0   | 80 GB  | 6       | 603   | 2     | 1.65   |
| WDC       | WD1001FAES-22W7A0  | 1 TB   | 2       | 603   | 0     | 1.65   |
| WDC       | WD15NPVT-00Z2TT0   | 1.5 TB | 1       | 601   | 0     | 1.65   |
| WDC       | WD10EZRX-00DC0B0   | 1 TB   | 8       | 653   | 2     | 1.65   |
| Apple     | HDD HTS541075A9... | 752 GB | 1       | 601   | 0     | 1.65   |
| WDC       | WD1200JS-00MHB0    | 120 GB | 15      | 635   | 1     | 1.65   |
| Hitachi   | HDS723020ALA640    | 2 TB   | 2       | 600   | 0     | 1.65   |
| WDC       | WD1600JS-23MHB0    | 160 GB | 1       | 600   | 0     | 1.64   |
| WDC       | WD1600AAJS-62WAA0  | 160 GB | 1       | 597   | 0     | 1.64   |
| WDC       | WD10EZRX-00L4HB0   | 1 TB   | 75      | 627   | 3     | 1.64   |
| WDC       | WD3200AAKX-221CA1  | 320 GB | 4       | 597   | 0     | 1.64   |
| Hitachi   | HDS721616PLAT80    | 160 GB | 7       | 1042  | 18    | 1.64   |
| Hitachi   | HDS721025CLA382    | 250 GB | 33      | 814   | 188   | 1.64   |
| WDC       | WD3200BEVT-00ZCT0  | 320 GB | 7       | 910   | 72    | 1.64   |
| WDC       | WD3200AAKS-00B3A0  | 320 GB | 44      | 811   | 25    | 1.63   |
| WDC       | WD10EURX-56FH1Y0   | 1 TB   | 2       | 596   | 0     | 1.63   |
| Seagate   | ST3500312CS        | 500 GB | 91      | 905   | 136   | 1.63   |
| Seagate   | ST3000VX000-1ES166 | 3 TB   | 3       | 594   | 0     | 1.63   |
| HP        | GB0250C8045        | 250 GB | 3       | 1283  | 67    | 1.63   |
| Hitachi   | HCC545016B9A300    | 160 GB | 1       | 593   | 0     | 1.63   |
| WDC       | WD1600AAJS-60M0A0  | 160 GB | 5       | 647   | 19    | 1.62   |
| WDC       | WD1600BEKT-75A25T0 | 160 GB | 2       | 590   | 0     | 1.62   |
| Seagate   | ST3750640NS        | 752 GB | 16      | 1373  | 368   | 1.62   |
| WDC       | WD2500BEAS-00URT0  | 250 GB | 1       | 1768  | 2     | 1.61   |
| Apple     | HDD ST750LM022     | 752 GB | 1       | 589   | 0     | 1.61   |
| WDC       | WD1600BEVS-22UST0  | 160 GB | 3       | 782   | 63    | 1.61   |
| Samsung   | HD153WI            | 1.5 TB | 2       | 588   | 0     | 1.61   |
| WDC       | WD800JD-19LSA0     | 80 GB  | 1       | 588   | 0     | 1.61   |
| Seagate   | ST6000VN0041-2E... | 6 TB   | 5       | 588   | 0     | 1.61   |
| WDC       | WD2000JS-22NCB1    | 200 GB | 2       | 1529  | 24    | 1.61   |
| WDC       | WD400BD-75MRA3     | 40 GB  | 2       | 587   | 0     | 1.61   |
| WDC       | WD800JD-00HKA0     | 80 GB  | 4       | 892   | 28    | 1.61   |
| Samsung   | HD252HJ            | 250 GB | 42      | 908   | 112   | 1.61   |
| WDC       | WD2500AAJS-60M0A1  | 250 GB | 2       | 587   | 0     | 1.61   |
| WDC       | WD2000JS-00MHB0    | 200 GB | 9       | 780   | 54    | 1.61   |
| Seagate   | ST3750640AS        | 752 GB | 14      | 1131  | 210   | 1.61   |
| WDC       | WD800BEVS-08RST2   | 80 GB  | 5       | 585   | 0     | 1.60   |
| WDC       | WD10EADS-11M2B3    | 1 TB   | 4       | 584   | 0     | 1.60   |
| WDC       | WD400BB-60JKA0     | 40 GB  | 4       | 785   | 21    | 1.60   |
| Hitachi   | HTS723216L9SA60    | 160 GB | 9       | 722   | 1     | 1.60   |
| Seagate   | ST2000DX001-1CM164 | 2 TB   | 30      | 697   | 123   | 1.60   |
| WDC       | WD10EURX-73C57Y0   | 1 TB   | 4       | 583   | 0     | 1.60   |
| Toshiba   | MQ01ABF050H        | 500 GB | 3       | 730   | 42    | 1.60   |
| WDC       | WD800JD-75MSA2     | 80 GB  | 3       | 582   | 0     | 1.60   |
| WDC       | WD1602ABJS-43P5A0  | 160 GB | 1       | 582   | 0     | 1.60   |
| WDC       | WD10EZRZ-00Z5HB0   | 1 TB   | 8       | 581   | 0     | 1.59   |
| Seagate   | ST3808110AS        | 80 GB  | 46      | 976   | 334   | 1.59   |
| Samsung   | HD154UI            | 1.5 TB | 68      | 994   | 287   | 1.59   |
| WDC       | WD1600AAJS-22WAA0  | 160 GB | 7       | 908   | 2     | 1.59   |
| WDC       | WD3200AAKS-22B3A0  | 320 GB | 3       | 1027  | 3     | 1.59   |
| Samsung   | HD502HJ            | 500 GB | 156     | 794   | 61    | 1.59   |
| Maxtor    | STM3320620A        | 320 GB | 2       | 579   | 0     | 1.59   |
| Samsung   | HD160JJ-P          | 160 GB | 14      | 1107  | 437   | 1.59   |
| WDC       | WD4002FFWX-68TZ4N0 | 4 TB   | 1       | 579   | 0     | 1.59   |
| Toshiba   | DT01ACA200         | 2 TB   | 249     | 632   | 48    | 1.59   |
| WDC       | WD1600BB-55RDA0    | 160 GB | 3       | 682   | 2     | 1.58   |
| Hitachi   | HUA722010CLA330    | 1 TB   | 24      | 1065  | 146   | 1.58   |
| Maxtor    | 7H500F0            | 500 GB | 5       | 648   | 1     | 1.58   |
| Seagate   | ST10000VN0004-1... | 10 TB  | 19      | 611   | 1     | 1.58   |
| WDC       | WD10EZEX-19M2NA0   | 1 TB   | 1       | 576   | 0     | 1.58   |
| WDC       | WD2500BUCT-63TWBY0 | 250 GB | 2       | 884   | 519   | 1.58   |
| Hitachi   | HDT721016SLA380    | 160 GB | 23      | 943   | 5     | 1.58   |
| Seagate   | ST3360320AS        | 360 GB | 17      | 1098  | 84    | 1.58   |
| Seagate   | ST3000VX000-9YW166 | 3 TB   | 5       | 730   | 5     | 1.57   |
| Seagate   | ST3160316AS        | 160 GB | 13      | 688   | 7     | 1.57   |
| HGST      | HUH728080ALE601    | 8 TB   | 20      | 1152  | 5     | 1.57   |
| WDC       | WD10EALS-002BA0    | 1 TB   | 5       | 737   | 1     | 1.57   |
| WDC       | WD6402AAEX-00Z3A0  | 640 GB | 4       | 573   | 0     | 1.57   |
| Hitachi   | HCS725032VLA380    | 320 GB | 1       | 573   | 0     | 1.57   |
| Toshiba   | DT01ABA100V        | 1 TB   | 9       | 997   | 209   | 1.57   |
| WDC       | WD60EFRX-68L0BN1   | 6 TB   | 35      | 748   | 114   | 1.57   |
| Seagate   | ST32000541AS       | 2 TB   | 1       | 572   | 0     | 1.57   |
| Hitachi   | HDS5C3020BLE630    | 2 TB   | 8       | 988   | 170   | 1.57   |
| WDC       | WD1600AAJS-00Z4A0  | 160 GB | 2       | 571   | 0     | 1.57   |
| HGST      | HUH721010ALE600    | 10 TB  | 17      | 592   | 1     | 1.57   |
| Toshiba   | MG06ACA10TEY       | 10 TB  | 4       | 570   | 0     | 1.56   |
| Seagate   | ST3500514NS        | 500 GB | 13      | 1341  | 73    | 1.56   |
| WDC       | WD2500JS-00SGB0    | 250 GB | 6       | 691   | 1     | 1.56   |
| Samsung   | HD321HJ            | 320 GB | 14      | 874   | 121   | 1.56   |
| Seagate   | ST2000NM0033-9Z... | 2 TB   | 10      | 679   | 1     | 1.56   |
| WDC       | WD5000AZRX-00A8LB0 | 500 GB | 95      | 616   | 1     | 1.56   |
| WDC       | WD5000BPKX-00HPJT0 | 500 GB | 4       | 568   | 0     | 1.56   |
| Seagate   | ST1000DM003-1ER162 | 1 TB   | 355     | 607   | 65    | 1.56   |
| Seagate   | ST3160212SCE       | 160 GB | 3       | 1562  | 793   | 1.55   |
| Seagate   | ST3320311CS        | 320 GB | 15      | 724   | 75    | 1.55   |
| Hitachi   | HUS724040ALE640    | 4 TB   | 5       | 609   | 77    | 1.55   |
| Seagate   | ST1000NX0443       | 1 TB   | 2       | 566   | 0     | 1.55   |
| WDC       | WD15EARX-00PASB0   | 1.5 TB | 13      | 728   | 3     | 1.55   |
| Samsung   | HD105SI            | 1 TB   | 18      | 809   | 220   | 1.55   |
| Seagate   | ST3320820AS_Q      | 320 GB | 2       | 1793  | 1068  | 1.54   |
| WDC       | WD3200BEKT-75PVMT1 | 320 GB | 17      | 753   | 41    | 1.54   |
| WDC       | WD4000FYYZ-01UL1B1 | 4 TB   | 11      | 1268  | 10    | 1.54   |
| WDC       | WD20EARS-00J2GB0   | 2 TB   | 7       | 985   | 5     | 1.54   |
| Seagate   | ST3500413AS        | 500 GB | 205     | 776   | 86    | 1.54   |
| WDC       | WD10EFRX-68FYTN0   | 1 TB   | 53      | 602   | 1     | 1.54   |
| Hitachi   | HTS545050B9A302    | 500 GB | 4       | 670   | 1     | 1.53   |
| WDC       | WD2500JS-58NCB1    | 250 GB | 3       | 858   | 205   | 1.53   |
| WDC       | WD2500JB-98GVA0    | 250 GB | 1       | 3354  | 5     | 1.53   |
| WDC       | WD2500AAJB-00WGA0  | 250 GB | 5       | 1069  | 115   | 1.53   |
| Hitachi   | HDS721064CLA332    | 640 GB | 2       | 558   | 0     | 1.53   |
| Seagate   | ST3250823A         | 250 GB | 6       | 977   | 440   | 1.53   |
| Samsung   | HD040GJ            | 40 GB  | 7       | 896   | 163   | 1.53   |
| WDC       | WD6400BPVT-75HXZT1 | 640 GB | 5       | 658   | 2     | 1.53   |
| WDC       | WD800JD-22LSA0     | 80 GB  | 8       | 715   | 83    | 1.53   |
| WDC       | WD3200BEVT-75ZCT1  | 320 GB | 1       | 2228  | 3     | 1.53   |
| Hitachi   | HDS721050CLA362    | 500 GB | 176     | 791   | 50    | 1.52   |
| WDC       | WD20EZRX-22D8PB0   | 2 TB   | 8       | 555   | 0     | 1.52   |
| Toshiba   | MD04ACA500         | 5 TB   | 8       | 616   | 3     | 1.52   |
| Toshiba   | MK6032GSX          | 64 GB  | 1       | 555   | 0     | 1.52   |
| WDC       | WD2500AAKX-603CA0  | 250 GB | 14      | 769   | 87    | 1.52   |
| WDC       | WD2500BEVS-00UST0  | 250 GB | 2       | 812   | 2     | 1.52   |
| WDC       | WD3000JS-00PDB0    | 304 GB | 1       | 554   | 0     | 1.52   |
| Seagate   | ST500DM009-2DM14C  | 500 GB | 4       | 554   | 0     | 1.52   |
| WDC       | WD6400AARS-00Y5B1  | 640 GB | 17      | 926   | 10    | 1.52   |
| Seagate   | ST1000VM002-1CT162 | 1 TB   | 13      | 790   | 44    | 1.52   |
| Seagate   | ST3250312AS        | 250 GB | 52      | 705   | 42    | 1.52   |
| WDC       | WD3200AAJS-07M0A0  | 320 GB | 6       | 694   | 11    | 1.51   |
| WDC       | WD3200AAKS-00L9A0  | 320 GB | 60      | 921   | 25    | 1.51   |
| WDC       | WD400BB-00JHA0     | 40 GB  | 4       | 1037  | 3     | 1.51   |
| WDC       | WD3200BPVT-00HXZT0 | 320 GB | 1       | 549   | 0     | 1.51   |
| WDC       | WD3200AAKS-61L9A0  | 320 GB | 10      | 628   | 6     | 1.51   |
| Seagate   | ST3320418AS        | 320 GB | 112     | 899   | 133   | 1.51   |
| WDC       | WD1600JS-00SGB0    | 160 GB | 1       | 549   | 0     | 1.50   |
| WDC       | WD3200AAJS-56B4A0  | 320 GB | 9       | 1010  | 3     | 1.50   |
| WDC       | WD2500AAKS-00YGA0  | 250 GB | 2       | 548   | 0     | 1.50   |
| Seagate   | ST360015A          | 64 GB  | 2       | 1494  | 5     | 1.50   |
| Seagate   | ST3200827A         | 200 GB | 1       | 544   | 0     | 1.49   |
| WDC       | WD15EARS-00S0XB0   | 1.5 TB | 4       | 748   | 3     | 1.49   |
| WDC       | WD5000HHTZ-75N21V0 | 500 GB | 1       | 544   | 0     | 1.49   |
| Toshiba   | MQ01ABB200         | 2 TB   | 20      | 695   | 168   | 1.49   |
| WDC       | WD3200BMVU-11A04S0 | 320 GB | 2       | 548   | 115   | 1.49   |
| WDC       | WD10EZEX-00RKKA0   | 1 TB   | 116     | 729   | 74    | 1.49   |
| Maxtor    | STM380215AS        | 80 GB  | 13      | 737   | 452   | 1.49   |
| MediaMax  | WL1000GSA6472C     | 1 TB   | 1       | 543   | 0     | 1.49   |
| Hitachi   | HDT725025VLAT80    | 250 GB | 2       | 1843  | 2     | 1.49   |
| Seagate   | ST4000VN000-2AH166 | 4 TB   | 3       | 542   | 0     | 1.49   |
| Seagate   | ST3120026AS        | 120 GB | 33      | 1177  | 65    | 1.49   |
| WDC       | WD5000LUCT-63C26Y0 | 500 GB | 2       | 541   | 0     | 1.48   |
| WDC       | WD3200AAKS-00VYA0  | 320 GB | 9       | 602   | 40    | 1.48   |
| Hitachi   | HDS728080PLA380    | 80 GB  | 52      | 829   | 47    | 1.48   |
| WDC       | WD2500BEVS-26UST0  | 250 GB | 5       | 540   | 0     | 1.48   |
| WDC       | WD1200JS-00MHB1    | 120 GB | 3       | 685   | 8     | 1.48   |
| Seagate   | ST380011A          | 80 GB  | 193     | 817   | 69    | 1.48   |
| Seagate   | ST3000NM0005-1V... | 3 TB   | 4       | 1190  | 15    | 1.48   |
| WDC       | WD2500AAKX-75U6AA0 | 250 GB | 15      | 760   | 2     | 1.48   |
| WDC       | WD20EADS-00R6B0    | 2 TB   | 8       | 926   | 254   | 1.47   |
| Magnet... | MD03200-NVDW-RO    | 320 GB | 1       | 538   | 0     | 1.47   |
| Seagate   | ST3300620AS        | 304 GB | 2       | 538   | 0     | 1.47   |
| WDC       | WD1000DHTZ-04N21V0 | 1 TB   | 7       | 945   | 14    | 1.47   |
| WDC       | WD3200BPVT-26JJ5T0 | 320 GB | 1       | 537   | 0     | 1.47   |
| WDC       | WD10EZEX-00BN5A0   | 1 TB   | 240     | 629   | 21    | 1.47   |
| Fujitsu   | MHW2120BH          | 120 GB | 26      | 588   | 20    | 1.47   |
| WDC       | WD7500AZEX-00RKKA0 | 752 GB | 7       | 536   | 0     | 1.47   |
| Hitachi   | HDS721050CLA660    | 500 GB | 34      | 819   | 124   | 1.47   |
| Seagate   | ST3320620A         | 320 GB | 28      | 889   | 80    | 1.47   |
| WDC       | WD6400AAKS-07A7B0  | 640 GB | 5       | 937   | 25    | 1.47   |
| HGST      | HUH721212ALN600    | 12 TB  | 1       | 534   | 0     | 1.46   |
| WDC       | WD800AAJS-22L7A0   | 80 GB  | 1       | 534   | 0     | 1.46   |
| WDC       | WD3200AAKX-083CA0  | 320 GB | 1       | 533   | 0     | 1.46   |
| Toshiba   | MK3259GSX          | 320 GB | 2       | 628   | 41    | 1.46   |
| Samsung   | HD253GJ            | 250 GB | 13      | 860   | 10    | 1.46   |
| WDC       | WD10EADS-65L5B1    | 1 TB   | 15      | 1096  | 22    | 1.46   |
| WDC       | WD1600JS-22MHB0    | 160 GB | 3       | 700   | 9     | 1.46   |
| Maxtor    | 6V200E0            | 208 GB | 11      | 970   | 96    | 1.46   |
| WDC       | WD1001FAES-55W7A0  | 1 TB   | 3       | 532   | 0     | 1.46   |
| WDC       | WD10TMVW-11ZSMS0   | 1 TB   | 1       | 531   | 0     | 1.46   |
| WDC       | WD800JD-22MSA1     | 80 GB  | 11      | 769   | 15    | 1.45   |
| WDC       | WD15EZRX-00DC0B0   | 1.5 TB | 2       | 530   | 0     | 1.45   |
| WDC       | WD10EZEX-75M2NA0   | 1 TB   | 25      | 575   | 1     | 1.45   |
| Hitachi   | HDS5C1032CLA382    | 320 GB | 5       | 748   | 3     | 1.45   |
| Seagate   | ST360021A          | 64 GB  | 5       | 598   | 10    | 1.45   |
| Seagate   | ST2000DM002-1BJ164 | 2 TB   | 1       | 529   | 0     | 1.45   |
| WDC       | WD1600AABS-00PRA0  | 160 GB | 2       | 529   | 0     | 1.45   |
| WDC       | WD1002F9YZ-09H1JL1 | 1 TB   | 4       | 526   | 0     | 1.44   |
| Seagate   | ST14000VN0008-2... | 14 TB  | 2       | 525   | 0     | 1.44   |
| WDC       | WD5000AAKX-753CA1  | 500 GB | 17      | 1128  | 24    | 1.44   |
| WDC       | WD7500BPVT-00HXZT1 | 752 GB | 1       | 525   | 0     | 1.44   |
| Seagate   | ST1000LM044 HN-... | 1 TB   | 4       | 619   | 202   | 1.44   |
| WDC       | WD5000AZRX-00L4HB0 | 500 GB | 34      | 525   | 0     | 1.44   |
| Apple     | HDD ST1000DM003    | 1 TB   | 27      | 524   | 0     | 1.44   |
| WDC       | WD5000BPVT-24HXZT1 | 500 GB | 2       | 1262  | 4     | 1.44   |
| Seagate   | ST250LT021-1AF14C  | 250 GB | 2       | 1034  | 585   | 1.44   |
| WDC       | WD10JPVX-08JC3T2   | 1 TB   | 7       | 535   | 1     | 1.43   |
| Seagate   | ST3250820AS        | 250 GB | 64      | 880   | 274   | 1.43   |
| Seagate   | ST3500630NS        | 500 GB | 8       | 890   | 588   | 1.43   |
| Hitachi   | HDP725025GLA380    | 250 GB | 47      | 1044  | 73    | 1.43   |
| Seagate   | ST160LM003 HN-M... | 160 GB | 3       | 522   | 0     | 1.43   |
| Maxtor    | 4K020H1            | 20 GB  | 1       | 522   | 0     | 1.43   |
| WDC       | WD5000AAKX-08ERMA0 | 500 GB | 33      | 695   | 129   | 1.43   |
| WDC       | WD800BB-00JKC0     | 80 GB  | 2       | 520   | 0     | 1.43   |
| WDC       | WD6400AARS-003BB1  | 640 GB | 1       | 520   | 0     | 1.43   |
| Apple     | HDD HTS541010A9... | 1 TB   | 34      | 702   | 150   | 1.43   |
| Seagate   | ST330621A          | 32 GB  | 2       | 664   | 5     | 1.42   |
| Seagate   | ST3200827AS        | 200 GB | 31      | 895   | 294   | 1.42   |
| Seagate   | ST1000DM003-1CH162 | 1 TB   | 467     | 664   | 80    | 1.42   |
| WDC       | WD5003AZEX-00K1GA0 | 500 GB | 31      | 551   | 35    | 1.42   |
| WDC       | WD4004FZWX-00GBGB0 | 4 TB   | 7       | 698   | 341   | 1.42   |
| Seagate   | ST12000VN0007-2... | 12 TB  | 11      | 705   | 194   | 1.42   |
| WDC       | WD20NMVW-11AV3S2   | 2 TB   | 44      | 695   | 21    | 1.42   |
| Maxtor    | 6G160P0            | 160 GB | 3       | 517   | 0     | 1.42   |
| WDC       | WD3200AAKS-00SBA0  | 320 GB | 14      | 761   | 18    | 1.42   |
| HGST      | HUH728080ALE600    | 8 TB   | 6       | 517   | 0     | 1.42   |
| WDC       | WD3200BEVT-75ZCT2  | 320 GB | 15      | 565   | 51    | 1.42   |
| WDC       | WD10JMVW-11AJGS0   | 1 TB   | 8       | 815   | 10    | 1.42   |
| WDC       | WD10JPVT-00A1YT0   | 1 TB   | 6       | 737   | 150   | 1.41   |
| Toshiba   | HDWT360            | 6 TB   | 1       | 516   | 0     | 1.41   |
| Hitachi   | HTS722012K9SA00    | 120 GB | 5       | 576   | 407   | 1.41   |
| Samsung   | HD753LJ            | 752 GB | 57      | 1086  | 178   | 1.41   |
| WDC       | WD30EFRX-68N32N0   | 3 TB   | 11      | 526   | 1     | 1.41   |
| WDC       | WD5000AAKS-007AA0  | 500 GB | 13      | 782   | 9     | 1.41   |
| WDC       | WD5000AAKS-22A7B0  | 500 GB | 22      | 1106  | 56    | 1.41   |
| WDC       | WD400BB-00DEA0     | 40 GB  | 2       | 1013  | 3     | 1.41   |
| Hitachi   | HDP725050GLA360    | 500 GB | 113     | 1083  | 63    | 1.40   |
| WDC       | WD740ADFD-00NLR5   | 74 GB  | 3       | 512   | 0     | 1.40   |
| Hitachi   | HDS721616PLA380    | 160 GB | 102     | 923   | 90    | 1.40   |
| WDC       | WD2500AAKX-221CA1  | 250 GB | 3       | 1011  | 6     | 1.40   |
| Hitachi   | HDS728080PLAT20    | 82 GB  | 26      | 703   | 6     | 1.40   |
| WDC       | WD10EZEX-21M2NA0   | 1 TB   | 55      | 568   | 26    | 1.40   |
| WDC       | WD5000BEKT-75KA9T0 | 500 GB | 6       | 737   | 2     | 1.40   |
| WDC       | WD3200AAJS-55B4A0  | 320 GB | 2       | 749   | 4     | 1.40   |
| WDC       | WD3200AAKS-75L9A0  | 320 GB | 29      | 896   | 31    | 1.40   |
| Fujitsu   | MHV2080BH          | 80 GB  | 6       | 567   | 2     | 1.39   |
| WDC       | WD5000LPVT-16G33T0 | 500 GB | 5       | 508   | 0     | 1.39   |
| Seagate   | ST3000DM001-1CH166 | 3 TB   | 80      | 715   | 338   | 1.39   |
| WDC       | WD10JFCX-68N6GN0   | 1 TB   | 25      | 556   | 1     | 1.39   |
| Hitachi   | HDS721616PLA320    | 160 GB | 4       | 1134  | 5     | 1.39   |
| Fujitsu   | MHT2040AH          | 40 GB  | 2       | 507   | 0     | 1.39   |
| WDC       | WD6400AAKS-55A7B0  | 640 GB | 1       | 507   | 0     | 1.39   |
| WDC       | WD20NMVW-11EDZS2   | 2 TB   | 12      | 507   | 0     | 1.39   |
| Seagate   | ST320LT023-1AF142  | 320 GB | 2       | 676   | 28    | 1.39   |
| Hitachi   | HDS721010CLA330    | 1 TB   | 48      | 803   | 27    | 1.39   |
| Seagate   | ST1000DX001-1NS... | 1 TB   | 4       | 506   | 0     | 1.39   |
| WDC       | WD10EURX-63UY4Y0   | 1 TB   | 9       | 685   | 3     | 1.39   |
| Seagate   | ST8000VX0022-2E... | 8 TB   | 2       | 948   | 65    | 1.39   |
| WDC       | WD5000BEVT-80A0RT0 | 500 GB | 4       | 927   | 5     | 1.38   |
| WDC       | WD5000AVJS-63TRA0  | 500 GB | 2       | 1510  | 289   | 1.38   |
| WDC       | WD1600AAJS-00M0A0  | 160 GB | 7       | 691   | 59    | 1.38   |
| Toshiba   | MK2556GSYF         | 250 GB | 1       | 503   | 0     | 1.38   |
| HGST      | HDN726040ALE614    | 4 TB   | 10      | 664   | 28    | 1.38   |
| Seagate   | ST1000VT000 HN-... | 1 TB   | 1       | 501   | 0     | 1.38   |
| WDC       | WD2500JD-75HBB0    | 250 GB | 1       | 501   | 0     | 1.37   |
| WDC       | WD2500AAJS-07M0A0  | 250 GB | 6       | 835   | 5     | 1.37   |
| Toshiba   | MK1032GSX          | 100 GB | 6       | 521   | 1     | 1.37   |
| Seagate   | ST1000VX000-1CU162 | 1 TB   | 29      | 512   | 35    | 1.37   |
| WDC       | WD10EADX-00TDHB0   | 1 TB   | 5       | 826   | 13    | 1.37   |
| WDC       | WD5000AVDS-63U7B1  | 500 GB | 22      | 871   | 40    | 1.37   |
| Seagate   | ST380012ACE        | 80 GB  | 4       | 498   | 0     | 1.37   |
| Samsung   | HM502JX            | 500 GB | 4       | 498   | 0     | 1.37   |
| Seagate   | ST3200826AS        | 200 GB | 15      | 934   | 65    | 1.36   |
| WDC       | WD3200LPLX-00ZNTT0 | 320 GB | 2       | 497   | 0     | 1.36   |
| WDC       | WD10EZRX-00D8PB0   | 1 TB   | 29      | 532   | 1     | 1.36   |
| HGST      | HUH721008ALE600    | 8 TB   | 4       | 958   | 2     | 1.36   |
| Seagate   | ST8000NM000A-2K... | 8 TB   | 6       | 496   | 0     | 1.36   |
| Hitachi   | HCC543216A7A380    | 160 GB | 1       | 496   | 0     | 1.36   |
| WDC       | WD200EB-00BHF0     | 20 GB  | 1       | 992   | 1     | 1.36   |
| WDC       | WD800BB-55JKA0     | 80 GB  | 5       | 740   | 1     | 1.36   |
| HGST      | HUS722T1TALA604    | 1 TB   | 8       | 496   | 0     | 1.36   |
| WDC       | WD10EZEX-60M2NA0   | 1 TB   | 35      | 681   | 108   | 1.36   |
| WDC       | WD2500AAKX-001CA0  | 250 GB | 36      | 606   | 81    | 1.36   |
| WDC       | WD1200JD-00GBB0    | 120 GB | 3       | 754   | 4     | 1.36   |
| WDC       | WD1600AAJS-00L7A0  | 160 GB | 44      | 894   | 7     | 1.36   |
| Toshiba   | HDWR11A            | 10 TB  | 1       | 494   | 0     | 1.36   |
| Hitachi   | HCP725032GLA380    | 320 GB | 4       | 823   | 1     | 1.35   |
| Fujitsu   | MPE3136AH          | 16 GB  | 1       | 494   | 0     | 1.35   |
| WDC       | WD4000FYYZ-05UL1B0 | 4 TB   | 1       | 493   | 0     | 1.35   |
| WDC       | WD2500JS-75NCB1    | 250 GB | 3       | 1381  | 51    | 1.35   |
| WDC       | WD6002FRYZ-01WD5B0 | 6 TB   | 2       | 817   | 1     | 1.35   |
| HGST      | HTS541515A9E630    | 1.5 TB | 6       | 772   | 177   | 1.35   |
| WDC       | WD5000AAKS-00V2B0  | 500 GB | 3       | 663   | 1     | 1.35   |
| Seagate   | ST1000VX000-9YW162 | 1 TB   | 5       | 491   | 0     | 1.35   |
| WDC       | WD800BEVT-00ZCT0   | 80 GB  | 2       | 491   | 0     | 1.35   |
| Samsung   | HD403LJ            | 400 GB | 23      | 1235  | 446   | 1.34   |
| Seagate   | ST2000NM0008-2F... | 2 TB   | 3       | 490   | 0     | 1.34   |
| WDC       | WD5000AAKS-00A7B2  | 500 GB | 39      | 859   | 23    | 1.34   |
| WDC       | WD5000AAKS-75V0A0  | 500 GB | 15      | 1077  | 4     | 1.34   |
| WDC       | WD1600AAJS-75M0A0  | 160 GB | 18      | 940   | 64    | 1.34   |
| WDC       | WD800BB-00JHA0     | 80 GB  | 8       | 827   | 4     | 1.34   |
| Hitachi   | HDT722516DLA380    | 164 GB | 18      | 886   | 41    | 1.34   |
| WDC       | WD400JD-55MSA1     | 40 GB  | 1       | 488   | 0     | 1.34   |
| Apple     | HDD ST2000DM001    | 2 TB   | 4       | 488   | 0     | 1.34   |
| WDC       | WD6400BPVT-55HXZT2 | 640 GB | 2       | 488   | 0     | 1.34   |
| Seagate   | ST3120026A         | 120 GB | 26      | 951   | 142   | 1.34   |
| Toshiba   | MQ03UBB200         | 2 TB   | 19      | 502   | 62    | 1.33   |
| WDC       | WD5000AACS-32G8B1  | 500 GB | 1       | 487   | 0     | 1.33   |
| WDC       | WD3200AZRX-00A8LB0 | 320 GB | 5       | 487   | 0     | 1.33   |
| WDC       | WD1600BJKT-00F4T0  | 160 GB | 1       | 486   | 0     | 1.33   |
| Seagate   | ST31500541AS       | 1.5 TB | 16      | 775   | 28    | 1.33   |
| WDC       | WD5000AAKS-75A7B0  | 500 GB | 6       | 1222  | 3     | 1.33   |
| Seagate   | ST3402111AS        | 40 GB  | 2       | 1607  | 524   | 1.33   |
| WDC       | WD800JD-55JRC0     | 80 GB  | 2       | 604   | 31    | 1.33   |
| WDC       | WD1600AAJS-65WAA0  | 160 GB | 3       | 1039  | 671   | 1.33   |
| Seagate   | ST1000DX001-1CM... | 1 TB   | 2       | 733   | 1     | 1.33   |
| Seagate   | ST3160212AS        | 160 GB | 4       | 497   | 2     | 1.33   |
| Seagate   | ST10000VN0004-2... | 10 TB  | 1       | 483   | 0     | 1.32   |
| HP        | GB0250EAFJF        | 250 GB | 3       | 1117  | 3     | 1.32   |
| Seagate   | ST3000DM008-2DM166 | 3 TB   | 65      | 577   | 80    | 1.32   |
| WDC       | WD1200JB-00GVA0    | 120 GB | 4       | 754   | 1     | 1.32   |
| Seagate   | ST31000524NS       | 1 TB   | 12      | 926   | 131   | 1.32   |
| Hitachi   | HCS5C1050CLA382    | 500 GB | 2       | 482   | 0     | 1.32   |
| Seagate   | ST340015A          | 40 GB  | 5       | 835   | 33    | 1.32   |
| WDC       | WD7500AZEX-00ZF5A0 | 752 GB | 6       | 481   | 0     | 1.32   |
| WDC       | WD5000BPKX-80HPJT0 | 500 GB | 1       | 480   | 0     | 1.32   |
| WDC       | WD10EARX-32N0YB0   | 1 TB   | 6       | 688   | 81    | 1.32   |
| Seagate   | ST3250310AS        | 250 GB | 188     | 975   | 221   | 1.32   |
| Hitachi   | HDT725032VLA360    | 320 GB | 19      | 1006  | 104   | 1.32   |
| Seagate   | ST2000LM003 HN-... | 2 TB   | 83      | 551   | 5     | 1.31   |
| WDC       | WD7502AAEX-00Y9A0  | 752 GB | 5       | 478   | 0     | 1.31   |
| Seagate   | ST3160023A         | 160 GB | 18      | 845   | 285   | 1.31   |
| WDC       | WD20EZRZ-22Z5HB0   | 2 TB   | 13      | 477   | 0     | 1.31   |
| Seagate   | ST3160815A         | 160 GB | 40      | 734   | 222   | 1.31   |
| Seagate   | ST9120821A         | 120 GB | 4       | 719   | 19    | 1.30   |
| WDC       | WD800JD-00LSA5     | 80 GB  | 3       | 475   | 0     | 1.30   |
| Seagate   | ST380817AS         | 80 GB  | 54      | 768   | 9     | 1.30   |
| WDC       | WD30NMRW-11YL9S4   | 3 TB   | 2       | 475   | 0     | 1.30   |
| WDC       | WD1600JS-56MHB1    | 160 GB | 7       | 888   | 5     | 1.30   |
| Seagate   | ST3120022A         | 120 GB | 41      | 670   | 75    | 1.30   |
| WDC       | WD10EACS-11BHUB0   | 1 TB   | 1       | 473   | 0     | 1.30   |
| Toshiba   | MK1016GAP          | 10 GB  | 1       | 472   | 0     | 1.29   |
| WDC       | WD3200AAJS-08L7A0  | 320 GB | 26      | 885   | 87    | 1.29   |
| WDC       | WD15EARS-00MVWB0   | 1.5 TB | 53      | 871   | 247   | 1.29   |
| WDC       | WD20EARX-55PASB0   | 2 TB   | 4       | 471   | 0     | 1.29   |
| WDC       | WD20NMVW-11EDZS6   | 2 TB   | 21      | 487   | 1     | 1.29   |
| Seagate   | ST980813AS         | 80 GB  | 4       | 601   | 1     | 1.29   |
| Hitachi   | HTS722020K9A300    | 200 GB | 1       | 469   | 0     | 1.29   |
| WDC       | WD60EZRZ-11RWYB1   | 6 TB   | 1       | 468   | 0     | 1.28   |
| Seagate   | ST320014A          | 20 GB  | 9       | 852   | 10    | 1.28   |
| Seagate   | ST32000646NS       | 2 TB   | 1       | 467   | 0     | 1.28   |
| WDC       | WD10EURX-62C57Y0   | 1 TB   | 1       | 466   | 0     | 1.28   |
| Samsung   | SV0221N            | 20 GB  | 1       | 2328  | 4     | 1.28   |
| Hitachi   | HDS721032CLA362    | 320 GB | 63      | 790   | 19    | 1.27   |
| Hitachi   | HDT721064SLA380    | 640 GB | 1       | 464   | 0     | 1.27   |
| WDC       | WD800AAJS-00B4A0   | 80 GB  | 5       | 543   | 3     | 1.27   |
| WDC       | WD5000AZDX-00SC2B0 | 500 GB | 6       | 695   | 10    | 1.27   |
| WDC       | WD400BB-00JHC0     | 40 GB  | 5       | 842   | 20    | 1.27   |
| WDC       | WD5000AAKX-001CA0  | 500 GB | 251     | 768   | 40    | 1.27   |
| WDC       | WD5000AAKX-07U6AA1 | 500 GB | 2       | 463   | 0     | 1.27   |
| WDC       | WD1600AAJS-08PSA0  | 160 GB | 16      | 679   | 9     | 1.27   |
| WDC       | WD20NMVW-11EDZS7   | 2 TB   | 16      | 518   | 77    | 1.27   |
| WDC       | WD6402AAEX-00Y9A0  | 640 GB | 7       | 695   | 7     | 1.26   |
| WDC       | WD1600AAJS-00B4A0  | 160 GB | 22      | 678   | 63    | 1.26   |
| WDC       | WD1003FBYX-01Y7B1  | 1 TB   | 38      | 672   | 2     | 1.26   |
| WDC       | WD1600AAJS-00V4A0  | 160 GB | 6       | 463   | 13    | 1.26   |
| Seagate   | ST4000NM0035-1V... | 4 TB   | 11      | 597   | 156   | 1.26   |
| Maxtor    | STM3320820AS       | 320 GB | 23      | 840   | 222   | 1.26   |
| WDC       | WD7500BPKX-75HPJT0 | 752 GB | 6       | 460   | 0     | 1.26   |
| Maxtor    | STM3802110A        | 80 GB  | 1       | 460   | 0     | 1.26   |
| WDC       | WD1600BEVS-08RST2  | 160 GB | 3       | 459   | 0     | 1.26   |
| Seagate   | ST3500411SV        | 500 GB | 3       | 646   | 25    | 1.26   |
| Seagate   | ST2000VM003-1CT164 | 2 TB   | 13      | 591   | 332   | 1.26   |
| Seagate   | ST980411ASG        | 80 GB  | 4       | 748   | 6     | 1.26   |
| WDC       | WD2500JS-22MHB0    | 250 GB | 4       | 580   | 70    | 1.26   |
| WDC       | WD1600BEVS-22RST0  | 160 GB | 47      | 552   | 78    | 1.26   |
| WDC       | WD5000AAKS-00D2B0  | 500 GB | 17      | 971   | 33    | 1.26   |
| Seagate   | ST3250820A         | 250 GB | 12      | 903   | 446   | 1.26   |
| WDC       | WD2500AAKS-00UU3A0 | 250 GB | 6       | 509   | 2     | 1.25   |
| WDC       | WD2500AAJS-22VTA0  | 250 GB | 9       | 563   | 1     | 1.25   |
| Samsung   | HD503HI            | 500 GB | 24      | 738   | 12    | 1.25   |
| Seagate   | ST3250620A         | 250 GB | 15      | 687   | 42    | 1.25   |
| WDC       | WD5000AUDX-63WNHY0 | 500 GB | 4       | 456   | 0     | 1.25   |
| Toshiba   | MQ01ABD100H        | 1 TB   | 1       | 456   | 0     | 1.25   |
| Toshiba   | HDWA130            | 3 TB   | 3       | 456   | 0     | 1.25   |
| Toshiba   | MG04ACA100NY       | 1 TB   | 10      | 456   | 0     | 1.25   |
| WDC       | WD80PURZ-85YNPY0   | 8 TB   | 1       | 456   | 0     | 1.25   |
| WDC       | WD1600JS-00NCB1    | 160 GB | 19      | 733   | 29    | 1.25   |
| WDC       | WD20EARS-55MVWB0   | 2 TB   | 2       | 455   | 0     | 1.25   |
| WDC       | WD2500AABS-00SDA0  | 250 GB | 1       | 455   | 0     | 1.25   |
| HGST      | HTS545025A7E380    | 250 GB | 3       | 454   | 0     | 1.25   |
| WDC       | WD6003FZBX-00K5WB0 | 6 TB   | 16      | 454   | 0     | 1.25   |
| Seagate   | ST500VT000-1BS142  | 500 GB | 3       | 454   | 0     | 1.25   |
| Hitachi   | HTS723232L9A362    | 320 GB | 2       | 959   | 4     | 1.24   |
| WDC       | WD30EZRZ-00Z5HB0   | 3 TB   | 41      | 537   | 19    | 1.24   |
| Hitachi   | HTS541610J9SA00    | 100 GB | 2       | 453   | 0     | 1.24   |
| Seagate   | ST3000VX010-2E3166 | 3 TB   | 6       | 463   | 1     | 1.24   |
| Seagate   | ST2000DM001-9YN164 | 2 TB   | 80      | 877   | 368   | 1.24   |
| Seagate   | ST10000NM0568-2... | 10 TB  | 4       | 452   | 0     | 1.24   |
| WDC       | WD5000MPCK-22AWHT0 | 500 GB | 1       | 452   | 0     | 1.24   |
| WDC       | WD6400BPVT-80HXZT3 | 640 GB | 8       | 690   | 9     | 1.24   |
| Seagate   | ST2000DM006-2DM164 | 2 TB   | 235     | 481   | 36    | 1.24   |
| Seagate   | ST3500320NS        | 500 GB | 18      | 851   | 322   | 1.24   |
| WDC       | WD800JD-55MUA1     | 80 GB  | 11      | 600   | 6     | 1.23   |
| Toshiba   | MD03ACA300V        | 3 TB   | 1       | 450   | 0     | 1.23   |
| WDC       | WD10JPVX-08JC3T6   | 1 TB   | 7       | 498   | 1     | 1.23   |
| WDC       | WD2500BEVS-22UST0  | 250 GB | 70      | 533   | 30    | 1.23   |
| WDC       | WD60PURX-64T0ZY0   | 6 TB   | 6       | 449   | 0     | 1.23   |
| Hitachi   | HDS728080PLA380... | 80 GB  | 1       | 449   | 0     | 1.23   |
| Samsung   | HD642JJ            | 640 GB | 41      | 1283  | 368   | 1.23   |
| Seagate   | ST1500DM003-1CH16G | 1.5 TB | 8       | 478   | 2     | 1.23   |
| WDC       | WD5000BEKT-00KA9T0 | 500 GB | 2       | 1084  | 7     | 1.23   |
| WDC       | WD2500AAJS-00V4A0  | 250 GB | 6       | 742   | 1     | 1.23   |
| Fujitsu   | MHY2250BH          | 250 GB | 10      | 680   | 38    | 1.23   |
| ExcelStor | J360               | 64 GB  | 1       | 897   | 1     | 1.23   |
| WDC       | WD7500BPKX-80HPJT0 | 752 GB | 6       | 447   | 0     | 1.23   |
| WDC       | WD5000AAJS-00TKA0  | 500 GB | 2       | 447   | 0     | 1.23   |
| Hitachi   | HTS541064A9E680    | 640 GB | 3       | 447   | 0     | 1.23   |
| Seagate   | STM3250318AS       | 250 GB | 34      | 724   | 179   | 1.23   |
| WDC       | WD15EARX-00ZUDB0   | 1.5 TB | 2       | 776   | 3     | 1.22   |
| WDC       | WD6400AAKS-40H2B0  | 640 GB | 4       | 1120  | 205   | 1.22   |
| Seagate   | ST750LX003-1AC154  | 752 GB | 22      | 590   | 130   | 1.22   |
| Seagate   | ST3160812A         | 160 GB | 30      | 684   | 348   | 1.22   |
| Samsung   | HD203WI            | 2 TB   | 6       | 480   | 1     | 1.22   |
| Seagate   | ST3200820A         | 200 GB | 5       | 491   | 61    | 1.22   |
| Seagate   | ST3250624AS        | 250 GB | 14      | 942   | 101   | 1.22   |
| WDC       | WD800AAJS-75M0A0   | 80 GB  | 6       | 1040  | 7     | 1.22   |
| WDC       | WD2500BEVT-22ZCT0  | 250 GB | 57      | 528   | 52    | 1.22   |
| WDC       | WD30EZRZ-00WN9B0   | 3 TB   | 7       | 444   | 0     | 1.22   |
| WDC       | WD740GD-00FLA2     | 74 GB  | 1       | 1330  | 2     | 1.22   |
| Seagate   | ST1000DM003-1SB10C | 1 TB   | 100     | 483   | 36    | 1.21   |
| WDC       | WD3200AAJS-60M0A0  | 320 GB | 4       | 794   | 2     | 1.21   |
| WDC       | WD3200BEVS-26VAT0  | 320 GB | 4       | 639   | 329   | 1.21   |
| WDC       | WD30EZRS-00J99B0   | 3 TB   | 9       | 1107  | 652   | 1.21   |
| WDC       | WD1003FBYX-18Y7B0  | 1 TB   | 3       | 1396  | 9     | 1.21   |
| Seagate   | ST10000NE0004-1... | 10 TB  | 10      | 908   | 12    | 1.21   |
| WDC       | WD7500AARS-00Y5B1  | 752 GB | 14      | 555   | 4     | 1.21   |
| WDC       | WD5000AAKX-07U6AA0 | 500 GB | 11      | 536   | 2     | 1.20   |
| WDC       | WD30EZRX-22D8PB0   | 3 TB   | 5       | 582   | 1     | 1.20   |
| Hitachi   | HTS723216L9A362    | 160 GB | 1       | 439   | 0     | 1.20   |
| WDC       | WD7500BPVX-60JC3T0 | 752 GB | 13      | 552   | 27    | 1.20   |
| WDC       | WD5000AADS-00S9B0  | 500 GB | 147     | 806   | 31    | 1.20   |
| WDC       | WD50EZRZ-00RWYB1   | 5 TB   | 2       | 438   | 0     | 1.20   |
| Seagate   | ST380215AS         | 80 GB  | 31      | 752   | 455   | 1.20   |
| WDC       | WD10EZEX-60ZF5A0   | 1 TB   | 65      | 691   | 80    | 1.19   |
| WDC       | WD10EARS-00Z5B1    | 1 TB   | 12      | 869   | 93    | 1.19   |
| Hitachi   | HDT722525DLA380    | 250 GB | 17      | 1138  | 138   | 1.19   |
| WDC       | WD5000AAJS-22A8B0  | 500 GB | 1       | 3915  | 8     | 1.19   |
| WDC       | WD5000AAKX-00ERMA0 | 500 GB | 157     | 629   | 8     | 1.19   |
| WDC       | WD2500AAKS-00F0A0  | 250 GB | 10      | 853   | 239   | 1.19   |
| Seagate   | ST3500418AS        | 500 GB | 539     | 816   | 167   | 1.19   |
| WDC       | WD2500BJKT-75F4T0  | 250 GB | 1       | 434   | 0     | 1.19   |
| WDC       | WD80EMAZ-00WJTA0   | 8 TB   | 34      | 433   | 0     | 1.19   |
| IBM/Hi... | IC25N020ATCS04-0   | 20 GB  | 1       | 433   | 0     | 1.19   |
| WDC       | WD6400AAKS-00H2B0  | 640 GB | 1       | 432   | 0     | 1.19   |
| WDC       | WD1200BEVS-22RST0  | 120 GB | 3       | 458   | 1     | 1.18   |
| WDC       | WD2500BEKT-75PVMT0 | 250 GB | 14      | 601   | 10    | 1.18   |
| WDC       | WD1600AABS-62PRA0  | 160 GB | 2       | 431   | 0     | 1.18   |
| Samsung   | SP1644N            | 160 GB | 4       | 636   | 649   | 1.18   |
| Seagate   | ST10000NM0156-2... | 10 TB  | 22      | 578   | 43    | 1.18   |
| Seagate   | ST1000DX001-SSH... | 1 TB   | 4       | 431   | 0     | 1.18   |
| WDC       | WD3001FAEX-00MJRA0 | 3 TB   | 5       | 1229  | 3     | 1.18   |
| HGST      | HCC545050A7E380    | 500 GB | 4       | 521   | 1     | 1.18   |
| Hitachi   | HTE545025B9A300    | 250 GB | 1       | 430   | 0     | 1.18   |
| WDC       | WD6400AACS-00D6B1  | 640 GB | 3       | 922   | 125   | 1.18   |
| Seagate   | ST380013AS         | 80 GB  | 44      | 1272  | 66    | 1.18   |
| Toshiba   | MG04ACA400E        | 4 TB   | 6       | 428   | 0     | 1.17   |
| WDC       | WD5000BMVW-11S5XS0 | 500 GB | 10      | 529   | 2     | 1.17   |
| WDC       | WD5000AAKS-65A7B0  | 500 GB | 10      | 739   | 44    | 1.17   |
| Samsung   | HD502HI            | 500 GB | 61      | 878   | 239   | 1.17   |
| Seagate   | ST500DM002-1BC142  | 500 GB | 72      | 700   | 156   | 1.17   |
| WDC       | WD5001AALS-00LWTA0 | 500 GB | 7       | 1053  | 43    | 1.17   |
| Hitachi   | HTS725032A9A360    | 320 GB | 4       | 612   | 349   | 1.17   |
| WDC       | WD10EURS-630AB1    | 1 TB   | 2       | 1247  | 4     | 1.17   |
| WDC       | WD10EARS-00Y5B1    | 1 TB   | 160     | 934   | 125   | 1.17   |
| WDC       | WD3200AAJS-60Z0A0  | 320 GB | 12      | 1049  | 109   | 1.17   |
| WDC       | WD10JMVW-11S5XS0   | 1 TB   | 11      | 671   | 4     | 1.17   |
| WDC       | WD50NDZM-59PW8S1   | 5 TB   | 1       | 426   | 0     | 1.17   |
| WDC       | WD4000AAKS-00TMA0  | 400 GB | 5       | 513   | 1     | 1.17   |
| WDC       | WD1200LB-55EDA0    | 120 GB | 1       | 425   | 0     | 1.17   |
| WDC       | WD3200AAJS-22L7A0  | 320 GB | 10      | 776   | 24    | 1.17   |
| Samsung   | HD501LJ            | 500 GB | 96      | 1123  | 462   | 1.16   |
| WDC       | WD5000LPVT-22G33T0 | 500 GB | 29      | 584   | 53    | 1.16   |
| Seagate   | ST1000NM0053-1C... | 1 TB   | 2       | 424   | 0     | 1.16   |
| WDC       | WD1001FALS-42K1B0  | 1 TB   | 1       | 423   | 0     | 1.16   |
| Seagate   | ST98823A           | 80 GB  | 5       | 541   | 259   | 1.16   |
| WDC       | WD2500AAJS-40RYA0  | 250 GB | 1       | 422   | 0     | 1.16   |
| Hitachi   | HDT721064SLA360    | 640 GB | 10      | 845   | 46    | 1.16   |
| WDC       | WD5000AAKS-22A7B2  | 500 GB | 9       | 1272  | 83    | 1.16   |
| WDC       | WD5000AAJS-22YFA0  | 500 GB | 6       | 781   | 352   | 1.15   |
| Seagate   | ST3500830AS        | 500 GB | 18      | 931   | 442   | 1.15   |
| WDC       | WD15EADS-00S2B0    | 1.5 TB | 4       | 1585  | 12    | 1.15   |
| Seagate   | ST3160023AS        | 160 GB | 20      | 1230  | 27    | 1.15   |
| Seagate   | ST4000DM000-2AE166 | 4 TB   | 11      | 420   | 0     | 1.15   |
| WDC       | WD3200AAJS-65B4A0  | 320 GB | 2       | 982   | 4     | 1.15   |
| Maxtor    | 6V080E0            | 82 GB  | 10      | 749   | 5     | 1.15   |
| WDC       | WD7500BPVT-75A1YT0 | 752 GB | 1       | 419   | 0     | 1.15   |
| Samsung   | HD322HJ            | 320 GB | 85      | 833   | 150   | 1.15   |
| WDC       | WD10JPVT-75A1YT0   | 1 TB   | 20      | 575   | 77    | 1.15   |
| WDC       | WD100EMAZ-00WJTA0  | 10 TB  | 39      | 418   | 0     | 1.15   |
| WDC       | WD3000FYYZ-05UL1B0 | 3 TB   | 1       | 418   | 0     | 1.15   |
| WDC       | WD5003ABYX-01WERA1 | 500 GB | 9       | 757   | 3     | 1.15   |
| Seagate   | ST250DM000-1BC141  | 250 GB | 17      | 458   | 6     | 1.14   |
| Toshiba   | MQ01UBD100         | 1 TB   | 48      | 560   | 140   | 1.14   |
| WDC       | WD5000ABPS-01ZZB0  | 500 GB | 1       | 416   | 0     | 1.14   |
| WDC       | WD1600BEVS-07RST0  | 160 GB | 11      | 457   | 1     | 1.14   |
| WDC       | WD2500AAKX-08U6AA0 | 250 GB | 10      | 501   | 2     | 1.14   |
| WDC       | WD1600BEVT-35ZCT0  | 160 GB | 3       | 416   | 0     | 1.14   |
| WDC       | WD5000BMVW-11AMCS2 | 500 GB | 4       | 415   | 0     | 1.14   |
| WDC       | WD1600JS-08MHB0    | 160 GB | 1       | 414   | 0     | 1.14   |
| Toshiba   | MK2546GSX_200      | 200 GB | 2       | 471   | 572   | 1.13   |
| Seagate   | ST1500DL003-9VT16L | 1.5 TB | 45      | 830   | 265   | 1.13   |
| Seagate   | ST31000520AS       | 1 TB   | 22      | 940   | 444   | 1.13   |
| WDC       | WD1200BEVS-22UST0  | 120 GB | 36      | 497   | 46    | 1.13   |
| Maxtor    | STM380211AS        | 80 GB  | 6       | 636   | 919   | 1.13   |
| WDC       | WD2500AAKX-07U6AA0 | 250 GB | 4       | 412   | 0     | 1.13   |
| WDC       | WD5000BMVW-11AJGS1 | 500 GB | 1       | 411   | 0     | 1.13   |
| WDC       | WD5000BMVW-11AMCS4 | 500 GB | 7       | 551   | 1     | 1.13   |
| WDC       | WD10S21X-24R1BT... | 1 TB   | 10      | 411   | 0     | 1.13   |
| Seagate   | ST9200420AS        | 200 GB | 3       | 571   | 6     | 1.13   |
| Toshiba   | MK1234GAX          | 120 GB | 3       | 410   | 0     | 1.13   |
| WDC       | WD5000AAKX-75U6AA0 | 500 GB | 45      | 649   | 80    | 1.12   |
| Seagate   | ST2000VM003-1ET164 | 2 TB   | 15      | 502   | 2     | 1.12   |
| WDC       | WD3000FYYZ-01UL1B1 | 3 TB   | 2       | 1047  | 6     | 1.12   |
| WDC       | WD1600BEVS-26VAT0  | 160 GB | 3       | 409   | 0     | 1.12   |
| WDC       | WD1600AAJS-75PSA0  | 160 GB | 8       | 500   | 2     | 1.12   |
| Seagate   | ST31000523AS       | 1 TB   | 3       | 1683  | 7     | 1.12   |
| WDC       | WD10JPVT-08A1YT1   | 1 TB   | 2       | 408   | 0     | 1.12   |
| WDC       | WD5000AZLX-00CL5A0 | 500 GB | 8       | 443   | 1     | 1.12   |
| Seagate   | ST3500841A         | 500 GB | 1       | 3265  | 7     | 1.12   |
| WDC       | WD800EB-11DJF0     | 80 GB  | 1       | 407   | 0     | 1.12   |
| Toshiba   | MK5065GSXF         | 500 GB | 23      | 528   | 33    | 1.12   |
| WDC       | WD2000JB-00KFA0    | 200 GB | 1       | 1220  | 2     | 1.11   |
| WDC       | WD2500JD-00HBB0    | 250 GB | 1       | 406   | 0     | 1.11   |
| Hitachi   | HTS721080G9AT00    | 80 GB  | 1       | 405   | 0     | 1.11   |
| WDC       | WD5000AAKX-08U6AA0 | 500 GB | 71      | 525   | 5     | 1.11   |
| WDC       | WD2500AAKS-00V6A0  | 250 GB | 1       | 404   | 0     | 1.11   |
| Samsung   | HE161HJ            | 160 GB | 1       | 1213  | 2     | 1.11   |
| Seagate   | ST500DM002-1SB10A  | 500 GB | 56      | 457   | 44    | 1.11   |
| Hitachi   | HTS545032B9SA00    | 320 GB | 10      | 542   | 414   | 1.11   |
| Seagate   | ST3400633AS        | 400 GB | 1       | 2017  | 4     | 1.11   |
| Seagate   | ST3160827AS        | 160 GB | 26      | 951   | 203   | 1.11   |
| Hitachi   | HDS721050CLA360    | 500 GB | 81      | 543   | 31    | 1.10   |
| WDC       | WD10JMVW-11AJGS2   | 1 TB   | 30      | 596   | 7     | 1.10   |
| Samsung   | HD322GJ            | 320 GB | 49      | 701   | 154   | 1.10   |
| WDC       | WD3200BEVS-08VAT2  | 320 GB | 5       | 558   | 224   | 1.10   |
| Seagate   | ST3250624A         | 250 GB | 1       | 1205  | 2     | 1.10   |
| HGST      | HUS726040ALE611    | 4 TB   | 1       | 401   | 0     | 1.10   |
| WDC       | WD400BB-23DEA0     | 40 GB  | 1       | 3213  | 7     | 1.10   |
| WDC       | WD5000AVKX-635FY0  | 500 GB | 1       | 401   | 0     | 1.10   |
| WDC       | WD1001FALS-40K1B0  | 1 TB   | 4       | 933   | 4     | 1.10   |
| WDC       | WD5000HHTZ-60N21V0 | 500 GB | 1       | 401   | 0     | 1.10   |
| WDC       | WD5003ABYX-23 8... | 500 GB | 2       | 668   | 2     | 1.10   |
| Quantum   | FIREBALLlct20 40   | 40 GB  | 1       | 400   | 0     | 1.10   |
| WDC       | WD2500AAKS-00VYA0  | 250 GB | 4       | 468   | 1     | 1.10   |
| WDC       | WD7500BMVW-11S5XS0 | 752 GB | 2       | 593   | 4     | 1.10   |
| Seagate   | ST8000NE0021-2E... | 8 TB   | 1       | 399   | 0     | 1.10   |
| WDC       | WD10EADS-11P8B2    | 1 TB   | 1       | 799   | 1     | 1.10   |
| Seagate   | ST8000VX0002-1Z... | 8 TB   | 1       | 399   | 0     | 1.10   |
| WDC       | WD10JPVT-24A1YT0   | 1 TB   | 5       | 657   | 1     | 1.09   |
| Seagate   | ST3250318AS        | 250 GB | 156     | 742   | 128   | 1.09   |
| WDC       | WD10EZEX-19ZF5A0   | 1 TB   | 1       | 399   | 0     | 1.09   |
| WDC       | WD3200BEVT-22ZCT0  | 320 GB | 128     | 504   | 82    | 1.09   |
| WDC       | WD20PURX-64P6ZY0   | 2 TB   | 21      | 522   | 8     | 1.09   |
| WDC       | WD40EFRX-68N32N0   | 4 TB   | 148     | 444   | 1     | 1.09   |
| Hitachi   | HTS543280L9SA00    | 80 GB  | 1       | 398   | 0     | 1.09   |
| WDC       | WD3200AAJB-56R1A0  | 320 GB | 3       | 425   | 3     | 1.09   |
| WDC       | WD5000BPKT-22PK4T0 | 500 GB | 2       | 398   | 0     | 1.09   |
| WDC       | WD7500BPKT-00PK4T0 | 752 GB | 6       | 585   | 1     | 1.09   |
| WDC       | WD1600BEVT-75ZCT2  | 160 GB | 17      | 509   | 122   | 1.09   |
| Seagate   | ST2000VX003-1HH164 | 2 TB   | 3       | 397   | 0     | 1.09   |
| WDC       | WD2500JS-57MHB1    | 250 GB | 1       | 397   | 0     | 1.09   |
| Seagate   | ST320410A          | 20 GB  | 7       | 791   | 12    | 1.09   |
| Fujitsu   | MJA2250BH FFS G1   | 250 GB | 3       | 397   | 0     | 1.09   |
| WDC       | WD20NMVW-11AV3S0   | 2 TB   | 5       | 577   | 2     | 1.09   |
| WDC       | WD7500BPVT-22A1YT0 | 752 GB | 4       | 716   | 2     | 1.09   |
| Seagate   | ST1000DM010-2DM162 | 1 TB   | 11      | 396   | 0     | 1.09   |
| Toshiba   | DT01ACA100         | 1 TB   | 535     | 463   | 28    | 1.09   |
| WDC       | WD3200AAKS-00L6A0  | 320 GB | 3       | 579   | 4     | 1.09   |
| Seagate   | ST1000DM003-9YN162 | 1 TB   | 206     | 683   | 225   | 1.09   |
| Hitachi   | HDP725040GLA360    | 400 GB | 7       | 801   | 187   | 1.08   |
| Seagate   | ST320LM000 HM321HI | 320 GB | 13      | 410   | 2     | 1.08   |
| Samsung   | HD321KJ            | 320 GB | 88      | 941   | 343   | 1.08   |
| WDC       | WD1003FBYX-05Y7B0  | 1 TB   | 2       | 433   | 883   | 1.08   |
| WDC       | WD6400AAKS-22A7B2  | 640 GB | 35      | 688   | 13    | 1.07   |
| Fujitsu   | MHW2160BH          | 160 GB | 6       | 505   | 15    | 1.07   |
| Seagate   | ST14000NM0018-2... | 14 TB  | 1       | 391   | 0     | 1.07   |
| Seagate   | ST320DM000-1BC14C  | 320 GB | 16      | 505   | 15    | 1.07   |
| WDC       | WD5000AADS-56S9B0  | 500 GB | 2       | 391   | 2     | 1.07   |
| Maxtor    | STM3250820A        | 250 GB | 7       | 548   | 187   | 1.07   |
| WDC       | WD10EACS-22D6B0    | 1 TB   | 5       | 1670  | 8     | 1.07   |
| WDC       | WD2000FYYZ-01UL1B1 | 2 TB   | 13      | 1092  | 149   | 1.07   |
| WDC       | WD15NMVW-11W68S0   | 1.5 TB | 2       | 389   | 0     | 1.07   |
| Maxtor    | STM3160815AS       | 160 GB | 32      | 702   | 327   | 1.07   |
| Apple     | HDD HTS541010A9... | 1 TB   | 21      | 464   | 11    | 1.07   |
| WDC       | WD2500AVJS-63WDA0  | 250 GB | 3       | 388   | 1     | 1.06   |
| WDC       | WD5000AAKS-00WWPA0 | 500 GB | 9       | 629   | 10    | 1.06   |
| Seagate   | ST33000651AS       | 3 TB   | 9       | 673   | 226   | 1.06   |
| WDC       | WD10SPCX-75KHST0   | 1 TB   | 7       | 386   | 0     | 1.06   |
| Seagate   | ST3200822AS        | 200 GB | 23      | 857   | 182   | 1.06   |
| WDC       | WD5000BEVT-75A0RT0 | 500 GB | 13      | 627   | 34    | 1.06   |
| Toshiba   | MD04ABA400V        | 4 TB   | 2       | 385   | 0     | 1.05   |
| WDC       | WD5000BEVT-75ZAT0  | 500 GB | 2       | 481   | 4     | 1.05   |
| WDC       | WD5000AZLX-21K2TA0 | 500 GB | 4       | 384   | 0     | 1.05   |
| WDC       | WD5000BEVT-00A03T0 | 500 GB | 3       | 384   | 0     | 1.05   |
| Seagate   | ST3120827AS        | 120 GB | 50      | 751   | 14    | 1.05   |
| WDC       | WD800BEVT-75ZCT2   | 80 GB  | 3       | 383   | 0     | 1.05   |
| WDC       | WD2000FYYZ-05UL1B0 | 2 TB   | 1       | 383   | 0     | 1.05   |
| WDC       | WD5000AAKX-00U6AA0 | 500 GB | 30      | 509   | 3     | 1.05   |
| Toshiba   | MQ01ABD100V -63    | 1 TB   | 1       | 383   | 0     | 1.05   |
| WDC       | WD5000BEVT-35A0RT0 | 500 GB | 19      | 528   | 36    | 1.05   |
| WDC       | WD1600JS-08NCB1    | 160 GB | 5       | 565   | 27    | 1.05   |
| Seagate   | ST4000VM000-2AF166 | 4 TB   | 4       | 382   | 0     | 1.05   |
| Seagate   | ST3750525AS        | 752 GB | 21      | 713   | 205   | 1.05   |
| Toshiba   | MK2559GSXP         | 250 GB | 4       | 450   | 7     | 1.05   |
| Seagate   | ST33000651NS       | 3 TB   | 5       | 1375  | 273   | 1.05   |
| WDC       | WD3200AAKX-00ERMA0 | 320 GB | 13      | 548   | 3     | 1.05   |
| Samsung   | HD163GJ            | 160 GB | 2       | 381   | 0     | 1.05   |
| WDC       | WD20SPZX-00CRAT0   | 2 TB   | 4       | 381   | 0     | 1.05   |
| Seagate   | ST31000525SV       | 1 TB   | 3       | 769   | 20    | 1.05   |
| WDC       | WD2000JD-22HBB0    | 200 GB | 3       | 993   | 7     | 1.04   |
| Seagate   | ST380811AS         | 80 GB  | 73      | 615   | 458   | 1.04   |
| WDC       | WD7500BPKT-22PK4T0 | 752 GB | 10      | 380   | 0     | 1.04   |
| WDC       | WD5000BPVT-80HXZT3 | 500 GB | 24      | 469   | 47    | 1.04   |
| WDC       | WD40E31X-00HY4A0   | 4 TB   | 1       | 380   | 0     | 1.04   |
| WDC       | WD2500JS-60MHB5    | 250 GB | 4       | 845   | 10    | 1.04   |
| Fujitsu   | MHV2040AH          | 40 GB  | 5       | 666   | 4     | 1.04   |
| Seagate   | ST3802110A         | 80 GB  | 42      | 636   | 440   | 1.04   |
| WDC       | WD5000AAKS-00UU3A0 | 500 GB | 69      | 745   | 73    | 1.03   |
| WDC       | WD2000JS-00SGB0    | 200 GB | 1       | 377   | 0     | 1.03   |
| WDC       | WD800AAJS-22WAA0   | 80 GB  | 2       | 376   | 0     | 1.03   |
| Seagate   | ST31000524AS       | 1 TB   | 278     | 699   | 229   | 1.03   |
| WDC       | WD7500BPVT-24HXZT1 | 752 GB | 13      | 633   | 81    | 1.03   |
| WDC       | WD1600BEVS-22VAT0  | 160 GB | 3       | 430   | 1     | 1.03   |
| WDC       | WD2500BEVT-75ZCT2  | 250 GB | 9       | 512   | 1     | 1.03   |
| Seagate   | ST980813ASG        | 80 GB  | 5       | 469   | 3     | 1.03   |
| WDC       | WD2500AAJB-00J3A0  | 250 GB | 11      | 693   | 7     | 1.03   |
| WDC       | WD800BB-00JKA0     | 80 GB  | 1       | 374   | 0     | 1.03   |
| WDC       | WD7500BPKT-80PK4T0 | 752 GB | 5       | 781   | 5     | 1.03   |
| Seagate   | ST8000DM0004-1Z... | 8 TB   | 3       | 373   | 0     | 1.02   |
| Toshiba   | HDWE160            | 6 TB   | 28      | 472   | 5     | 1.02   |
| WDC       | WD1600AAJS-98PSA0  | 160 GB | 4       | 440   | 1     | 1.02   |
| WDC       | WD5000AVCS-982DY1  | 500 GB | 1       | 372   | 0     | 1.02   |
| Seagate   | ST9402112A         | 40 GB  | 1       | 1117  | 2     | 1.02   |
| WDC       | WD20NPVX-00EA4T0   | 2 TB   | 5       | 571   | 3     | 1.02   |
| WDC       | WD7500BPVX-22JC3T0 | 752 GB | 25      | 459   | 2     | 1.02   |
| Seagate   | ST250DM000-1BD141  | 250 GB | 140     | 602   | 105   | 1.02   |
| WDC       | WD1600JS-22NCB1    | 160 GB | 4       | 712   | 6     | 1.02   |
| WDC       | WD2500BEVT-35ZCT0  | 250 GB | 2       | 845   | 225   | 1.02   |
| WDC       | WD1600AAJS-60B4A0  | 160 GB | 9       | 958   | 142   | 1.02   |
| WDC       | WD10JMVW-11AJGS3   | 1 TB   | 26      | 481   | 3     | 1.02   |
| Hitachi   | HTS541660J9AT00    | 64 GB  | 2       | 788   | 2     | 1.02   |
| WDC       | WD7500BPKT-60PK4T0 | 752 GB | 4       | 452   | 2     | 1.02   |
| WDC       | WD7500BPVT-24HXZT3 | 752 GB | 14      | 417   | 19    | 1.02   |
| WDC       | WD2500AVVS-62L2B0  | 250 GB | 3       | 373   | 3     | 1.02   |
| WDC       | WD2500AAKX-00U6AA0 | 250 GB | 3       | 373   | 3     | 1.01   |
| Seagate   | ST5000LM000-2AN170 | 5 TB   | 26      | 370   | 0     | 1.01   |
| WDC       | WD3200BEKT-60KA9T0 | 320 GB | 1       | 369   | 0     | 1.01   |
| WDC       | WD3200AVJS-63N9A0  | 320 GB | 5       | 369   | 0     | 1.01   |
| WDC       | WD3200AAJB-00J3A0  | 320 GB | 24      | 728   | 22    | 1.01   |
| Seagate   | ST1000DX001-1CM162 | 1 TB   | 53      | 535   | 68    | 1.01   |
| WDC       | WD3200BEKT-00KA9T0 | 320 GB | 1       | 369   | 0     | 1.01   |
| WDC       | WD5000AAKX-22ERMA0 | 500 GB | 70      | 554   | 17    | 1.01   |
| Seagate   | ST500DM002-1BD142  | 500 GB | 886     | 624   | 108   | 1.01   |
| Samsung   | HM500JI            | 500 GB | 53      | 529   | 5     | 1.01   |
| Seagate   | ST3250410AS        | 250 GB | 204     | 881   | 285   | 1.01   |
| Seagate   | ST3400620NS        | 400 GB | 3       | 1529  | 14    | 1.01   |
| WDC       | WD20NMVW-11AV3S3   | 2 TB   | 4       | 546   | 5     | 1.01   |
| Hitachi   | HDS721680PLAT80    | 80 GB  | 6       | 1080  | 5     | 1.01   |
| WDC       | WD800JB-00JJC0     | 80 GB  | 26      | 646   | 23    | 1.01   |
| WDC       | WD20EZRZ-00Z5HB0   | 2 TB   | 193     | 446   | 36    | 1.01   |
| WDC       | WD60EZRX-11MVLB1   | 6 TB   | 1       | 366   | 0     | 1.01   |
| Apple     | HDD HTS545050A7... | 500 GB | 40      | 398   | 7     | 1.01   |
| WDC       | WD3200AAJS-00B4A0  | 320 GB | 25      | 894   | 91    | 1.00   |
| WDC       | WD1600AAJS-00WAA0  | 160 GB | 11      | 487   | 4     | 1.00   |
| Seagate   | ST31000340NS       | 1 TB   | 23      | 1322  | 346   | 1.00   |
| Fujitsu   | MHZ2250BH G1       | 250 GB | 11      | 552   | 11    | 1.00   |
| WDC       | WD5000AAKS-41YGA1  | 500 GB | 1       | 728   | 1     | 1.00   |
| Seagate   | ST1000DX001-1NS162 | 1 TB   | 19      | 686   | 26    | 1.00   |
| WDC       | WD1600JS-00MHB0    | 160 GB | 8       | 709   | 146   | 1.00   |
| WDC       | WD2500BEVT-35A23T0 | 250 GB | 25      | 507   | 26    | 1.00   |
| Samsung   | SP1654N            | 160 GB | 8       | 849   | 412   | 0.99   |
| WDC       | WD3200AAKX-001CA0  | 320 GB | 37      | 728   | 67    | 0.99   |
| HGST      | HTS725032A7E630    | 320 GB | 35      | 531   | 214   | 0.99   |
| WDC       | WD2500BEVS-08VAT2  | 250 GB | 5       | 361   | 0     | 0.99   |
| Maxtor    | STM3160212A        | 160 GB | 2       | 817   | 1     | 0.99   |
| WDC       | WD10JUCT-63CYNY0   | 1 TB   | 10      | 527   | 1     | 0.99   |
| WDC       | WD3200AAJS-22B4A0  | 320 GB | 12      | 1189  | 78    | 0.98   |
| Maxtor    | STM3160215AS       | 160 GB | 37      | 903   | 722   | 0.98   |
| WDC       | WD10EADS-67M2B0    | 1 TB   | 2       | 946   | 14    | 0.98   |
| WDC       | WD2500BPVT-00JJ5T0 | 250 GB | 3       | 358   | 0     | 0.98   |
| WDC       | WD10JPVX-22JC3T0   | 1 TB   | 269     | 425   | 33    | 0.98   |
| WDC       | WD3200AVVS-56L2B0  | 320 GB | 10      | 524   | 57    | 0.98   |
| Seagate   | ST3250310NS        | 250 GB | 3       | 737   | 755   | 0.98   |
| Fujitsu   | MHW2120BJ G2       | 120 GB | 1       | 356   | 0     | 0.98   |
| Seagate   | ST6000DM003-2CY186 | 6 TB   | 39      | 381   | 26    | 0.98   |
| Seagate   | ST3160215A         | 160 GB | 25      | 706   | 451   | 0.98   |
| Fujitsu   | MHW2060BH          | 64 GB  | 4       | 743   | 4     | 0.97   |
| WDC       | WD5000AAJS-08A8B0  | 500 GB | 2       | 691   | 2     | 0.97   |
| WDC       | WD10EZEX-00WN4A0   | 1 TB   | 119     | 402   | 5     | 0.97   |
| WDC       | WD3200AAJS-00M0A0  | 320 GB | 2       | 574   | 1     | 0.97   |
| Toshiba   | MK3261GSYG         | 320 GB | 1       | 354   | 0     | 0.97   |
| WDC       | WD1005FBYZ-01YCBB2 | 1 TB   | 6       | 354   | 0     | 0.97   |
| Toshiba   | MK5075GSX          | 500 GB | 36      | 533   | 320   | 0.97   |
| HGST      | HUS726060ALA640    | 6 TB   | 1       | 353   | 0     | 0.97   |
| Hitachi   | HTS545032B9A301    | 320 GB | 1       | 353   | 0     | 0.97   |
| Samsung   | HD161GJ            | 160 GB | 41      | 693   | 177   | 0.97   |
| WDC       | WD2500AAKX-00ERMA0 | 250 GB | 35      | 475   | 40    | 0.97   |
| WDC       | WD5000AAKX-60U6AA0 | 500 GB | 114     | 471   | 90    | 0.97   |
| WDC       | WD2500BEKT-75PVMT1 | 250 GB | 3       | 1251  | 6     | 0.97   |
| WDC       | WD6400AACS-00M3B0  | 640 GB | 1       | 352   | 0     | 0.97   |
| WDC       | WD10EALX-008EA0    | 1 TB   | 7       | 358   | 1     | 0.96   |
| WDC       | WD5000LPVX-08V0TT5 | 500 GB | 19      | 393   | 1     | 0.96   |
| Toshiba   | DT01ACA050         | 500 GB | 460     | 433   | 34    | 0.96   |
| Hitachi   | HDS721680PLA380    | 80 GB  | 57      | 927   | 239   | 0.96   |
| WDC       | WD2500JD-22HBC0    | 250 GB | 2       | 1266  | 78    | 0.96   |
| Seagate   | ST2000DX002-2DV164 | 2 TB   | 52      | 418   | 25    | 0.96   |
| WDC       | WD5000LMZW-11Y0TS0 | 500 GB | 2       | 350   | 0     | 0.96   |
| Seagate   | ST3160215AS        | 160 GB | 22      | 682   | 401   | 0.96   |
| Seagate   | ST500VT000-1DK142  | 500 GB | 27      | 415   | 14    | 0.96   |
| WDC       | WD50PURX-64T0ZY0   | 5 TB   | 1       | 349   | 0     | 0.96   |
| WDC       | WD2500LPVX-22V0TT0 | 250 GB | 4       | 367   | 1     | 0.96   |
| Hitachi   | HTS543216A7A384    | 160 GB | 4       | 348   | 0     | 0.95   |
| Seagate   | ST3120814A         | 120 GB | 19      | 735   | 307   | 0.95   |
| HGST      | HUS726060ALE614    | 6 TB   | 7       | 383   | 81    | 0.95   |
| ExcelStor | J880S              | 82 GB  | 3       | 733   | 8     | 0.95   |
| Seagate   | ST3320820AS        | 320 GB | 25      | 509   | 316   | 0.95   |
| Seagate   | ST6000DM0003       | 6 TB   | 1       | 346   | 0     | 0.95   |
| Seagate   | ST31000528AS       | 1 TB   | 302     | 779   | 270   | 0.95   |
| Seagate   | ST1500LM006 HN-... | 1.5 TB | 7       | 346   | 0     | 0.95   |
| WDC       | WD5000BPKT-75PK4T0 | 500 GB | 18      | 511   | 3     | 0.95   |
| WDC       | WD3200JS-22PDB0    | 320 GB | 3       | 837   | 8     | 0.95   |
| WDC       | WD3200AAJS-00RYA0  | 320 GB | 5       | 1207  | 129   | 0.95   |
| WDC       | WD1003FZEX-00K3CA0 | 1 TB   | 54      | 365   | 38    | 0.95   |
| HPE       | MB4000GCWDC        | 4 TB   | 1       | 1037  | 2     | 0.95   |
| WDC       | WD3200BEVT-11ZCT0  | 320 GB | 5       | 533   | 1     | 0.95   |
| WDC       | WD6400BPVT-16HXZT1 | 640 GB | 1       | 1037  | 2     | 0.95   |
| WDC       | WD3200BPVT-35ZEST0 | 320 GB | 22      | 468   | 2     | 0.95   |
| Seagate   | ST4000VN008-2DR166 | 4 TB   | 106     | 360   | 3     | 0.95   |
| WDC       | WD5000BPVT-80HXZT1 | 500 GB | 10      | 604   | 34    | 0.95   |
| WDC       | WD5000BUCT-63LS5Y1 | 500 GB | 1       | 345   | 0     | 0.95   |
| WDC       | WD1600BEVT-75ZCT0  | 160 GB | 2       | 695   | 48    | 0.95   |
| Hitachi   | HTS545050B9A300    | 500 GB | 156     | 634   | 219   | 0.95   |
| WDC       | WD5000AAKX-083CA1  | 500 GB | 22      | 758   | 37    | 0.94   |
| WDC       | WD800BB-22JHC0     | 80 GB  | 11      | 504   | 34    | 0.94   |
| WDC       | WD7500BPVT-22HXZT3 | 752 GB | 33      | 398   | 1     | 0.94   |
| WDC       | WD2500BEVS-75UST0  | 250 GB | 11      | 470   | 2     | 0.94   |
| Seagate   | ST3000VX000-1CU166 | 3 TB   | 6       | 345   | 10    | 0.94   |
| Seagate   | ST3160813AS        | 160 GB | 47      | 807   | 127   | 0.94   |
| HGST      | HTS721010A9E630    | 1 TB   | 505     | 423   | 152   | 0.94   |
| Seagate   | ST2000DM009-2G4100 | 2 TB   | 6       | 342   | 0     | 0.94   |
| WDC       | WD5000BEVT-26A0RT0 | 500 GB | 5       | 836   | 148   | 0.94   |
| Samsung   | SP0812N            | 80 GB  | 7       | 597   | 4     | 0.94   |
| Hitachi   | HDP725016GLA380    | 160 GB | 12      | 981   | 215   | 0.93   |
| Hitachi   | HDP725032GLA380    | 320 GB | 9       | 868   | 25    | 0.93   |
| Toshiba   | MK1234GSX          | 120 GB | 16      | 660   | 16    | 0.93   |
| WDC       | WD10EZEX-08Y20A0   | 1 TB   | 12      | 427   | 2     | 0.93   |
| Seagate   | ST3160811AS        | 160 GB | 88      | 778   | 455   | 0.93   |
| Fujitsu   | MHW2080BH PL       | 80 GB  | 8       | 560   | 130   | 0.93   |
| WDC       | WD800JD-32LSA0     | 80 GB  | 2       | 1577  | 53    | 0.93   |
| WDC       | WD2500BEKT-60PVMT0 | 250 GB | 15      | 405   | 68    | 0.93   |
| WDC       | WD40PURX-64N96Y0   | 4 TB   | 1       | 339   | 0     | 0.93   |
| WDC       | WD2003FYYS-01T8B0  | 2 TB   | 1       | 3050  | 8     | 0.93   |
| Samsung   | HD160JJ            | 160 GB | 90      | 839   | 389   | 0.93   |
| Seagate   | ST500DM005 HD502HJ | 500 GB | 48      | 528   | 9     | 0.93   |
| WDC       | WD1600BEVT-26A23T0 | 160 GB | 1       | 338   | 0     | 0.93   |
| WDC       | WD800BB-00JHC0     | 80 GB  | 26      | 605   | 71    | 0.93   |
| WDC       | WD1600AABS-00H4A0  | 160 GB | 3       | 660   | 5     | 0.93   |
| WDC       | WD6400BPVT-60HXZT1 | 640 GB | 6       | 748   | 688   | 0.93   |
| WDC       | WD40EZRZ-00GXCB0   | 4 TB   | 112     | 342   | 22    | 0.92   |
| ExcelStor | J680               | 82 GB  | 1       | 1687  | 4     | 0.92   |
| Hitachi   | HTS725050A9A362    | 500 GB | 7       | 404   | 45    | 0.92   |
| IBM/Hi... | IC35L090AVV207-0   | 80 GB  | 2       | 735   | 2     | 0.92   |
| HGST      | HTS721075A9E630    | 752 GB | 10      | 354   | 122   | 0.92   |
| WDC       | WD80EMAZ-00M9AA0   | 8 TB   | 1       | 336   | 0     | 0.92   |
| Seagate   | ST4000NM0165       | 4 TB   | 1       | 336   | 0     | 0.92   |
| Seagate   | ST2000VN004-2E4164 | 2 TB   | 17      | 417   | 2     | 0.92   |
| WDC       | WD2500AAJS-55M0A0  | 250 GB | 3       | 416   | 3     | 0.92   |
| Toshiba   | MQ01ACF032         | 320 GB | 25      | 394   | 1     | 0.92   |
| Toshiba   | MQ01UBD050         | 500 GB | 8       | 370   | 289   | 0.92   |
| WDC       | WD100EFAX-68LHPN0  | 10 TB  | 14      | 336   | 0     | 0.92   |
| Toshiba   | MG04ACA400EY       | 4 TB   | 2       | 335   | 0     | 0.92   |
| Fujitsu   | MHV2100BH          | 100 GB | 5       | 680   | 22    | 0.92   |
| Seagate   | ST9320310AS        | 320 GB | 10      | 631   | 393   | 0.92   |
| WDC       | WD3200BPVT-16JJ5T0 | 320 GB | 6       | 380   | 1     | 0.92   |
| WDC       | WD5000BHTZ-04JCPV0 | 500 GB | 1       | 334   | 0     | 0.92   |
| WDC       | WD10JPVT-60A1YT0   | 1 TB   | 3       | 403   | 337   | 0.92   |
| WDC       | WD10EZEX-21WN4A0   | 1 TB   | 43      | 350   | 1     | 0.91   |
| WDC       | WD1600BEVT-22ZCT0  | 160 GB | 128     | 455   | 67    | 0.91   |
| WDC       | WD4002FYYZ-01B7CB1 | 4 TB   | 2       | 332   | 0     | 0.91   |
| WDC       | WD80EZAZ-11TDBA0   | 8 TB   | 38      | 333   | 3     | 0.91   |
| WDC       | WD3200AAKS-00V1A0  | 320 GB | 8       | 773   | 203   | 0.91   |
| WDC       | WD10EZEX-75WN4A0   | 1 TB   | 49      | 364   | 34    | 0.91   |
| WDC       | WD3200LPVX-16V0TT0 | 320 GB | 1       | 331   | 0     | 0.91   |
| WDC       | WD10JPVX-35JC3T0   | 1 TB   | 6       | 498   | 2     | 0.91   |
| Seagate   | ST3160211AS        | 160 GB | 11      | 658   | 799   | 0.91   |
| WDC       | WD5000AADS-00M2B0  | 500 GB | 32      | 923   | 168   | 0.91   |
| WDC       | WD40EMAZ-11LW3B0   | 4 TB   | 4       | 331   | 0     | 0.91   |
| WDC       | WD6400BPVT-00HXZT1 | 640 GB | 4       | 331   | 0     | 0.91   |
| Fujitsu   | MHY2160BH          | 160 GB | 25      | 399   | 189   | 0.91   |
| Hitachi   | HTE725032A9A364    | 320 GB | 1       | 1985  | 5     | 0.91   |
| Fujitsu   | MHW2080BH          | 80 GB  | 9       | 409   | 2     | 0.91   |
| WDC       | WD5000LPVT-24G33T1 | 500 GB | 25      | 431   | 54    | 0.91   |
| Seagate   | ST250DM001 HD253GJ | 250 GB | 7       | 330   | 0     | 0.91   |
| Fujitsu   | MHV2120AH          | 120 GB | 3       | 418   | 2     | 0.91   |
| Samsung   | HD322GM            | 320 GB | 1       | 1320  | 3     | 0.90   |
| WDC       | WD10JPLX-00MBPT0   | 1 TB   | 45      | 339   | 4     | 0.90   |
| Hitachi   | HDE721010SLA330    | 1 TB   | 6       | 1331  | 29    | 0.90   |
| WDC       | WD5000BMVW-11AJGS2 | 500 GB | 4       | 329   | 0     | 0.90   |
| WDC       | WD5000LPVT-08G33T1 | 500 GB | 16      | 394   | 1     | 0.90   |
| WDC       | WD3200LPVX-80V0TT0 | 320 GB | 2       | 328   | 0     | 0.90   |
| HGST      | HDS724020ALE640    | 2 TB   | 1       | 328   | 0     | 0.90   |
| Seagate   | ST250LT020-1AE14C  | 250 GB | 3       | 409   | 314   | 0.90   |
| WDC       | WD1600BEVS-00VAT0  | 160 GB | 2       | 327   | 0     | 0.90   |
| WDC       | WD2500AAJS-00Z0A0  | 250 GB | 3       | 819   | 4     | 0.90   |
| WDC       | WD60EFAX-68SHWN0   | 6 TB   | 7       | 406   | 1     | 0.90   |
| WDC       | WD5000AAJS-19A8B0  | 500 GB | 1       | 326   | 0     | 0.90   |
| WDC       | WD5000LPLX-66ZNTT0 | 500 GB | 1       | 326   | 0     | 0.89   |
| Fujitsu   | MHV2080AT PL       | 80 GB  | 4       | 515   | 569   | 0.89   |
| WDC       | WD10EZEX-00M2NA0   | 1 TB   | 3       | 383   | 12    | 0.89   |
| WDC       | WD6400BPVT-55HXZT3 | 640 GB | 2       | 591   | 4     | 0.89   |
| Seagate   | ST320DM000-1BD14C  | 320 GB | 37      | 475   | 97    | 0.89   |
| WDC       | WD2503ABYZ-011FA0  | 256 GB | 1       | 325   | 0     | 0.89   |
| Toshiba   | MK3276GSX H        | 320 GB | 3       | 325   | 0     | 0.89   |
| WDC       | WD800BB-60JKA0     | 80 GB  | 1       | 325   | 0     | 0.89   |
| WDC       | WD5000BEVT-24A0RT0 | 500 GB | 26      | 513   | 17    | 0.89   |
| WDC       | WD20NMVW-59EDZS7   | 2 TB   | 1       | 324   | 0     | 0.89   |
| Seagate   | ST1000DM003-1SB102 | 1 TB   | 150     | 357   | 39    | 0.89   |
| WDC       | WD5000BPVT-16HXZT3 | 500 GB | 1       | 324   | 0     | 0.89   |
| WDC       | WD10SPCX-08S8TT0   | 1 TB   | 5       | 324   | 0     | 0.89   |
| WDC       | WD3200JS-00PDB0    | 320 GB | 1       | 324   | 0     | 0.89   |
| WDC       | WD3200BPVT-00JJ5T0 | 320 GB | 16      | 578   | 134   | 0.89   |
| WDC       | WD5000BPKT-60PK4T0 | 500 GB | 9       | 529   | 144   | 0.89   |
| WDC       | WD5000BPVT-00HXZT3 | 500 GB | 17      | 392   | 34    | 0.89   |
| WDC       | WD20SMZW-34JW8S0   | 2 TB   | 1       | 323   | 0     | 0.89   |
| Seagate   | ST3250824A         | 250 GB | 4       | 753   | 253   | 0.88   |
| WDC       | WD8003FRYZ-01JPDB1 | 8 TB   | 2       | 322   | 0     | 0.88   |
| WDC       | WD3200BVVT-63A26Y0 | 320 GB | 5       | 359   | 132   | 0.88   |
| WDC       | WD2500AAJS-08B4A0  | 250 GB | 2       | 931   | 1211  | 0.88   |
| WDC       | WD60EZRZ-00RWYB1   | 6 TB   | 11      | 478   | 204   | 0.88   |
| WDC       | WD800BB-75JHC0     | 80 GB  | 3       | 517   | 1     | 0.88   |
| WDC       | WD10JPVT-55A1YT0   | 1 TB   | 1       | 320   | 0     | 0.88   |
| Toshiba   | MK3261GSY          | 320 GB | 2       | 320   | 0     | 0.88   |
| WDC       | WD10JPVX-75JC3T0   | 1 TB   | 78      | 404   | 32    | 0.88   |
| WDC       | WD6400AAKS-75A7B0  | 640 GB | 3       | 404   | 2     | 0.88   |
| WDC       | WD7500BPVT-26HXZT3 | 752 GB | 1       | 1277  | 3     | 0.88   |
| WDC       | WD5000AAKS-55V0A0  | 500 GB | 8       | 645   | 6     | 0.88   |
| Seagate   | ST9750422AS        | 752 GB | 5       | 579   | 125   | 0.87   |
| WDC       | WD3200AAJS-56M0A0  | 320 GB | 34      | 506   | 34    | 0.87   |
| WDC       | WD1600YD-01NVB1    | 164 GB | 2       | 377   | 1     | 0.87   |
| Seagate   | ST320LM010-1KJ15C  | 320 GB | 8       | 542   | 129   | 0.87   |
| Toshiba   | MQ01ABD075         | 752 GB | 149     | 445   | 93    | 0.87   |
| WDC       | WD3200AAJS-61B4A0  | 320 GB | 2       | 431   | 4     | 0.87   |
| Fujitsu   | MHV2060BH          | 64 GB  | 11      | 487   | 7     | 0.87   |
| WDC       | WD800BB-00FJA0     | 80 GB  | 7       | 472   | 35    | 0.87   |
| WDC       | WD40PURX-64NZ6Y0   | 4 TB   | 3       | 316   | 0     | 0.87   |
| Samsung   | HD752LJ            | 752 GB | 2       | 1517  | 4     | 0.87   |
| Fujitsu   | MHV2100AT          | 100 GB | 1       | 316   | 0     | 0.87   |
| Hitachi   | HDT721025SLA380    | 250 GB | 14      | 838   | 220   | 0.87   |
| WDC       | WD40EZRZ-75GXCB0   | 4 TB   | 18      | 315   | 0     | 0.87   |
| Toshiba   | HDWD130            | 3 TB   | 94      | 321   | 11    | 0.87   |
| Maxtor    | STM3200820A        | 200 GB | 1       | 315   | 0     | 0.86   |
| Fujitsu   | MJA2160BH FFS G1   | 160 GB | 3       | 315   | 0     | 0.86   |
| WDC       | WD800BEVS-00UST0   | 80 GB  | 1       | 315   | 0     | 0.86   |
| WDC       | WD5000AAKX-221CA1  | 500 GB | 17      | 594   | 18    | 0.86   |
| Toshiba   | MK8032GSX          | 80 GB  | 9       | 473   | 175   | 0.86   |
| Seagate   | ST9160411AS        | 160 GB | 9       | 583   | 130   | 0.86   |
| WDC       | WD3200AAKB-00WHA0  | 320 GB | 2       | 314   | 0     | 0.86   |
| Hitachi   | HTS725016A9A364    | 160 GB | 17      | 589   | 442   | 0.86   |
| Seagate   | ST9500420ASG       | 500 GB | 7       | 877   | 326   | 0.86   |
| WDC       | WD2000JS-55MHB0    | 200 GB | 1       | 313   | 0     | 0.86   |
| WDC       | WD7500BPVT-80HXZT3 | 752 GB | 19      | 454   | 19    | 0.86   |
| WDC       | WD40NMZM-59Y94S1   | 4 TB   | 1       | 313   | 0     | 0.86   |
| WDC       | WD2000JB-00GVA0    | 200 GB | 3       | 580   | 101   | 0.86   |
| WDC       | WD3200LPVX-22V0TT0 | 320 GB | 21      | 354   | 1     | 0.86   |
| Samsung   | HD080HJ            | 80 GB  | 112     | 754   | 373   | 0.86   |
| Seagate   | ST6000VN0033-2E... | 6 TB   | 14      | 323   | 1     | 0.86   |
| Apple     | HDD ST1000LM024    | 1 TB   | 6       | 584   | 3     | 0.85   |
| Seagate   | ST2000VX002-1AH166 | 2 TB   | 1       | 311   | 0     | 0.85   |
| WDC       | WD800JD-23LSA0     | 80 GB  | 2       | 631   | 2     | 0.85   |
| WDC       | WD30EZRZ-00GXCB0   | 3 TB   | 20      | 334   | 1     | 0.85   |
| WDC       | WD20NMVW-59AV3S2   | 2 TB   | 2       | 310   | 0     | 0.85   |
| WDC       | WD5000LPVX-60V0TT0 | 500 GB | 26      | 415   | 86    | 0.85   |
| Maxtor    | STM380815AS        | 80 GB  | 23      | 727   | 578   | 0.85   |
| Seagate   | ST9250410AS        | 250 GB | 68      | 514   | 209   | 0.85   |
| WDC       | WD5000AAKS-22V1A0  | 500 GB | 18      | 1006  | 169   | 0.85   |
| Fujitsu   | MHZ2160BH G2       | 160 GB | 38      | 586   | 364   | 0.85   |
| WDC       | WD40NMZW-11GX6S1   | 4 TB   | 47      | 347   | 12    | 0.85   |
| Toshiba   | MQ03UBB300         | 3 TB   | 10      | 340   | 5     | 0.85   |
| WDC       | WD10EALX-559BA0    | 1 TB   | 5       | 517   | 6     | 0.85   |
| WDC       | WD400BB-60DGA0     | 40 GB  | 4       | 403   | 1     | 0.85   |
| Fujitsu   | MHZ2320BH G1       | 320 GB | 13      | 600   | 19    | 0.85   |
| WDC       | WD1600JS-40TGB0    | 160 GB | 1       | 308   | 0     | 0.85   |
| MediaMax  | WL5000GSA12872B    | 5 TB   | 1       | 308   | 0     | 0.85   |
| WDC       | WD1600BEVT-60ZCT1  | 160 GB | 12      | 407   | 185   | 0.84   |
| Fujitsu   | MJA2160BH G2       | 160 GB | 11      | 465   | 301   | 0.84   |
| WDC       | WD5000AVCS-632DY1  | 500 GB | 16      | 446   | 6     | 0.84   |
| Toshiba   | MQ01ABC150         | 1.5 TB | 2       | 308   | 0     | 0.84   |
| Seagate   | ST1000NC001-1DY162 | 1 TB   | 7       | 783   | 146   | 0.84   |
| WDC       | WD800JB-00JJA0     | 80 GB  | 4       | 1406  | 9     | 0.84   |
| Samsung   | HM501II            | 500 GB | 7       | 954   | 64    | 0.84   |
| Fujitsu   | MJA2320BH G2       | 320 GB | 11      | 771   | 377   | 0.84   |
| WDC       | WD2500BEKT-60V5T1  | 250 GB | 2       | 399   | 3     | 0.84   |
| WDC       | WD2500AAJS-00L7A0  | 250 GB | 28      | 617   | 13    | 0.84   |
| HGST      | HUH728080ALE604    | 8 TB   | 8       | 307   | 0     | 0.84   |
| WDC       | WD10EZEX-60WN4A0   | 1 TB   | 99      | 359   | 27    | 0.84   |
| Seagate   | ST96812AS          | 64 GB  | 10      | 550   | 290   | 0.84   |
| WDC       | WD20SMZW-59YFCS1   | 2 TB   | 1       | 306   | 0     | 0.84   |
| WDC       | WD5000AAKS-08WWPA0 | 500 GB | 2       | 1656  | 77    | 0.84   |
| Toshiba   | HDWL120            | 2 TB   | 20      | 327   | 1     | 0.84   |
| WDC       | WD5000BPVT-55HXZT3 | 500 GB | 7       | 368   | 3     | 0.84   |
| WDC       | WD3200BEVT-00SCST0 | 320 GB | 1       | 306   | 0     | 0.84   |
| Samsung   | HD400LJ            | 400 GB | 2       | 480   | 5     | 0.84   |
| WDC       | WD1500ADFD-00NLR1  | 150 GB | 2       | 454   | 4     | 0.84   |
| WDC       | WD2500BEKT-00PVMT0 | 250 GB | 3       | 305   | 0     | 0.84   |
| Maxtor    | STM3250820AS       | 250 GB | 19      | 803   | 166   | 0.84   |
| WDC       | WD2500BEVT-08A23T1 | 250 GB | 17      | 393   | 102   | 0.84   |
| WDC       | WD10JPVX-00JC3T0   | 1 TB   | 51      | 307   | 1     | 0.84   |
| WDC       | WD3200BPVT-00HXZT3 | 320 GB | 5       | 437   | 6     | 0.84   |
| WDC       | WD1200BEVS-75UST0  | 120 GB | 14      | 387   | 1     | 0.84   |
| Seagate   | ST1000VM002-1SD102 | 1 TB   | 8       | 304   | 0     | 0.84   |
| WDC       | WD7500BPVT-55HXZT3 | 752 GB | 3       | 444   | 3     | 0.84   |
| WDC       | WD800BEVS-22VAT0   | 80 GB  | 2       | 304   | 0     | 0.83   |
| Seagate   | ST8000NE001-2M7101 | 8 TB   | 2       | 304   | 0     | 0.83   |
| WDC       | WD5000BPVT-22HXZT3 | 500 GB | 60      | 425   | 49    | 0.83   |
| WDC       | WD3200BEKT-60PVMT0 | 320 GB | 19      | 510   | 214   | 0.83   |
| Seagate   | ST1750LM000 HN-... | 1.7 TB | 2       | 303   | 0     | 0.83   |
| WDC       | WD3200BPVT-55JJ5T0 | 320 GB | 6       | 415   | 163   | 0.83   |
| Seagate   | ST500NM0011 81Y... | 500 GB | 2       | 2410  | 506   | 0.83   |
| Seagate   | ST500LX012-SSHD... | 500 GB | 5       | 386   | 1     | 0.83   |
| Seagate   | ST250LT003-9YG14C  | 250 GB | 4       | 302   | 0     | 0.83   |
| WDC       | WD10SPZX-11Z10T0   | 1 TB   | 1       | 302   | 0     | 0.83   |
| WDC       | WD3200BEVT-08A23T1 | 320 GB | 11      | 528   | 98    | 0.83   |
| Samsung   | HD251HJ            | 250 GB | 12      | 707   | 122   | 0.83   |
| Fujitsu   | MHZ2160BH FFS G1   | 160 GB | 5       | 403   | 1     | 0.83   |
| Toshiba   | HDWD120            | 2 TB   | 89      | 304   | 12    | 0.83   |
| WDC       | WD3200AAJS-00YZCA0 | 320 GB | 14      | 511   | 8     | 0.83   |
| Toshiba   | HDWQ140            | 4 TB   | 23      | 318   | 1     | 0.83   |
| WDC       | WD3200BEKX-75B7WT0 | 320 GB | 4       | 301   | 0     | 0.83   |
| Seagate   | ST31000528ASQ      | 1 TB   | 2       | 430   | 66    | 0.83   |
| Seagate   | ST3160021A         | 160 GB | 16      | 731   | 400   | 0.82   |
| WDC       | WD1600JS-60MHB5    | 160 GB | 5       | 752   | 18    | 0.82   |
| WDC       | WD600BEAS-22KZT0   | 64 GB  | 1       | 300   | 0     | 0.82   |
| WDC       | WD5000AAKX-00KJ3A0 | 500 GB | 2       | 416   | 4     | 0.82   |
| WDC       | WD1600BPVT-00ZEST0 | 160 GB | 1       | 299   | 0     | 0.82   |
| Seagate   | ST2000VN000-1H3164 | 2 TB   | 5       | 625   | 11    | 0.82   |
| WDC       | WD800BEVS-07RST0   | 80 GB  | 5       | 330   | 1     | 0.82   |
| WDC       | WD10SDZW-11UMGS0   | 1 TB   | 13      | 298   | 0     | 0.82   |
| WDC       | WD10JPVX-80JC3T0   | 1 TB   | 11      | 298   | 0     | 0.82   |
| Samsung   | SP1203N            | 120 GB | 13      | 713   | 95    | 0.82   |
| Seagate   | ST1000LM014-1EJ... | 1 TB   | 14      | 458   | 18    | 0.82   |
| Toshiba   | HDWN180            | 8 TB   | 11      | 298   | 0     | 0.82   |
| WDC       | WD5000BPVT-24HXZT3 | 500 GB | 23      | 422   | 2     | 0.82   |
| WDC       | WD6400BPVT-80HXZT1 | 640 GB | 10      | 557   | 108   | 0.82   |
| WDC       | WD5000BEVT-22A0RT0 | 500 GB | 51      | 638   | 96    | 0.82   |
| WDC       | WD10JPVX-11JC3T0   | 1 TB   | 3       | 297   | 0     | 0.82   |
| Samsung   | HM641JI            | 640 GB | 41      | 509   | 53    | 0.82   |
| Seagate   | ST3000VX006-1HH166 | 3 TB   | 2       | 324   | 570   | 0.82   |
| Toshiba   | MK4009GAL          | 40 GB  | 1       | 296   | 0     | 0.81   |
| WDC       | WD5000AVCS-732DY1  | 500 GB | 2       | 658   | 9     | 0.81   |
| WDC       | WD10SMZW-11Y0TS0   | 1 TB   | 34      | 295   | 0     | 0.81   |
| Maxtor    | STM3250620A        | 250 GB | 1       | 295   | 0     | 0.81   |
| Hitachi   | HDS723020BLA642... | 2 TB   | 1       | 295   | 0     | 0.81   |
| WDC       | WD100PURZ-85W86Y0  | 10 TB  | 1       | 295   | 0     | 0.81   |
| Seagate   | ST380819AS         | 80 GB  | 6       | 658   | 685   | 0.81   |
| WDC       | WD3200BPVT-24JJ5T0 | 320 GB | 71      | 356   | 51    | 0.81   |
| WDC       | WD1500HLFS-01G6U4  | 150 GB | 2       | 295   | 0     | 0.81   |
| Hitachi   | HTS545032B9A300    | 320 GB | 133     | 506   | 165   | 0.81   |
| WDC       | WD800JD-22JNC0     | 80 GB  | 2       | 412   | 3     | 0.81   |
| Seagate   | ST3320820SCE       | 320 GB | 1       | 294   | 0     | 0.81   |
| Seagate   | ST750LM022 HN-M... | 752 GB | 128     | 413   | 29    | 0.81   |
| Seagate   | ST4000DM004-2CV104 | 4 TB   | 279     | 328   | 34    | 0.80   |
| WDC       | WD10JMVW-11AJGS1   | 1 TB   | 14      | 406   | 78    | 0.80   |
| WDC       | WD7501AALS-00E3A0  | 752 GB | 10      | 745   | 83    | 0.80   |
| Samsung   | SV1203N            | 120 GB | 2       | 441   | 3     | 0.80   |
| WDC       | WD10EZEX-07M2NA1   | 1 TB   | 1       | 292   | 0     | 0.80   |
| WDC       | WD5000LPVX-75V0TT0 | 500 GB | 48      | 336   | 2     | 0.80   |
| Toshiba   | MQ02ABD100H        | 1 TB   | 29      | 400   | 76    | 0.80   |
| WDC       | WD5000AAKS-00V1A0  | 500 GB | 64      | 822   | 331   | 0.80   |
| Seagate   | STM3500418AS       | 500 GB | 31      | 831   | 386   | 0.80   |
| Maxtor    | STM3160211AS       | 160 GB | 3       | 624   | 349   | 0.80   |
| Seagate   | ST1000VX001-1HH162 | 1 TB   | 7       | 291   | 0     | 0.80   |
| WDC       | WD5000BMVW-11AMCS0 | 500 GB | 4       | 390   | 3     | 0.80   |
| Seagate   | ST9408114A         | 40 GB  | 1       | 291   | 0     | 0.80   |
| Magnet... | MD02500-BJDW-RO    | 250 GB | 1       | 291   | 0     | 0.80   |
| Hitachi   | HTS545016B9SA02    | 160 GB | 3       | 426   | 45    | 0.80   |
| WDC       | WD5000BPVT-08HXZT3 | 500 GB | 9       | 338   | 1     | 0.80   |
| Hitachi   | HCS5C1025CLA382    | 250 GB | 1       | 290   | 0     | 0.80   |
| WDC       | WD1600BB-00GUC0    | 160 GB | 4       | 832   | 61    | 0.79   |
| WDC       | WD5000BPKT-00PK4T0 | 500 GB | 8       | 300   | 1     | 0.79   |
| Seagate   | OOS2000G           | 2 TB   | 1       | 289   | 0     | 0.79   |
| Seagate   | ST500LM012 HN-M... | 500 GB | 316     | 405   | 36    | 0.79   |
| WDC       | WD7500BPVT-22HXZT1 | 752 GB | 8       | 887   | 207   | 0.79   |
| WDC       | WD7500BPVT-75HXZT3 | 752 GB | 6       | 396   | 1     | 0.79   |
| Seagate   | ST3250820ACE       | 250 GB | 4       | 595   | 781   | 0.79   |
| Hitachi   | HDS721010DLE630    | 1 TB   | 54      | 845   | 611   | 0.79   |
| Seagate   | ST640LM001 HN-M... | 640 GB | 6       | 422   | 9     | 0.79   |
| Toshiba   | MK3029GAC          | 32 GB  | 1       | 287   | 0     | 0.79   |
| WDC       | WD5000BMVV-11SXZS1 | 500 GB | 3       | 1103  | 4     | 0.79   |
| Fujitsu   | MHY2200BH          | 200 GB | 22      | 527   | 80    | 0.79   |
| WDC       | WD2002FFSX-68PF8N0 | 2 TB   | 2       | 286   | 0     | 0.79   |
| WDC       | WD1200BEVT-22ZCT0  | 120 GB | 1       | 286   | 0     | 0.79   |
| WDC       | WD2000JS-60NCB1    | 200 GB | 3       | 399   | 4     | 0.79   |
| WDC       | WD1200BEVS-75RST0  | 120 GB | 3       | 286   | 0     | 0.78   |
| Toshiba   | MK1656GSY          | 160 GB | 6       | 346   | 5     | 0.78   |
| Seagate   | ST9160412AS        | 160 GB | 17      | 588   | 348   | 0.78   |
| WDC       | WD40PURZ-85TTDY0   | 4 TB   | 27      | 350   | 1     | 0.78   |
| WDC       | WD1600JD-22HBB0    | 160 GB | 1       | 1710  | 5     | 0.78   |
| Seagate   | ST380215A          | 80 GB  | 32      | 485   | 193   | 0.78   |
| WDC       | WD5000AAVS-22G9B1  | 500 GB | 3       | 1103  | 8     | 0.78   |
| Samsung   | HM120JC            | 120 GB | 3       | 1072  | 38    | 0.78   |
| HGST      | HUS726040ALE614    | 4 TB   | 3       | 284   | 0     | 0.78   |
| WDC       | WD10EZEX-22MFCA0   | 1 TB   | 116     | 296   | 11    | 0.78   |
| WDC       | WD1600AAJB-00PVA0  | 160 GB | 12      | 631   | 156   | 0.78   |
| Maxtor    | STM3250310AS       | 250 GB | 81      | 757   | 432   | 0.78   |
| Hitachi   | HDS721032CLA662    | 320 GB | 1       | 283   | 0     | 0.78   |
| Toshiba   | DT01ACA050 LENOVO  | 500 GB | 4       | 282   | 0     | 0.78   |
| Hitachi   | HTS545016B9SA00    | 160 GB | 2       | 282   | 0     | 0.77   |
| WDC       | WD5000LPVX-80V0TT0 | 500 GB | 55      | 310   | 60    | 0.77   |
| WDC       | WD3009FYPX-09AAMB0 | 3 TB   | 1       | 2256  | 7     | 0.77   |
| Seagate   | ST1000LM014-1EJ164 | 1 TB   | 99      | 477   | 76    | 0.77   |
| WDC       | WD3200LPVT-08G33T1 | 320 GB | 6       | 327   | 2     | 0.77   |
| Seagate   | ST14000DM001-2J... | 14 TB  | 3       | 281   | 0     | 0.77   |
| WDC       | WD1600AAJS-00YZCA0 | 160 GB | 13      | 497   | 29    | 0.77   |
| WDC       | WD5000LPVX-22V0TT0 | 500 GB | 255     | 336   | 10    | 0.77   |
| WDC       | WD1600AAJS-22L7A0  | 160 GB | 18      | 633   | 15    | 0.77   |
| Seagate   | ST8000DM004-2CX188 | 8 TB   | 118     | 320   | 23    | 0.77   |
| WDC       | WD10SPCX-22HWST0   | 1 TB   | 3       | 280   | 0     | 0.77   |
| Hitachi   | HTS543216L9SA00    | 160 GB | 22      | 501   | 53    | 0.77   |
| Fujitsu   | MHW2100BH          | 100 GB | 1       | 279   | 0     | 0.76   |
| WDC       | WD1600BEVT-75ZCT1  | 160 GB | 1       | 279   | 0     | 0.76   |
| WDC       | WD2500BEVS-60UST0  | 250 GB | 13      | 561   | 261   | 0.76   |
| WDC       | WD100EB-00BHF0     | 10 GB  | 1       | 557   | 1     | 0.76   |
| Toshiba   | HDWF180            | 8 TB   | 15      | 285   | 108   | 0.76   |
| WDC       | WD10JPVX-16JC3T3   | 1 TB   | 3       | 278   | 0     | 0.76   |
| WDC       | WD800BEVS-22RST0   | 80 GB  | 30      | 407   | 51    | 0.76   |
| WDC       | WD3200AAJS-00L7A0  | 320 GB | 99      | 721   | 53    | 0.76   |
| WDC       | WD2503ABYX-01WERA1 | 256 GB | 6       | 526   | 2     | 0.76   |
| WDC       | WD40EZRX-11SPEB0   | 4 TB   | 1       | 277   | 0     | 0.76   |
| WDC       | WD7500BPKT-75PK4T0 | 752 GB | 24      | 472   | 4     | 0.76   |
| Samsung   | HD401LJ            | 400 GB | 4       | 702   | 14    | 0.76   |
| Samsung   | HM321HI            | 320 GB | 124     | 446   | 96    | 0.76   |
| WDC       | WD5000AAKX-221CA0  | 500 GB | 2       | 1008  | 5     | 0.76   |
| Seagate   | ST1500LM012-1R817G | 1.5 TB | 4       | 277   | 0     | 0.76   |
| WDC       | WD6400BPVT-22HXZT3 | 640 GB | 13      | 583   | 121   | 0.76   |
| WDC       | WD5000BPVT-35HXZT1 | 500 GB | 6       | 276   | 0     | 0.76   |
| WDC       | WD6401AALS-00J7B0  | 640 GB | 1       | 1656  | 5     | 0.76   |
| Seagate   | ST9320328CS        | 320 GB | 12      | 713   | 162   | 0.76   |
| WDC       | WD1200JS-00NCB1    | 120 GB | 2       | 591   | 27    | 0.75   |
| Seagate   | ST94813AS          | 40 GB  | 3       | 347   | 68    | 0.75   |
| Seagate   | STM3320418AS       | 320 GB | 10      | 644   | 140   | 0.75   |
| WDC       | WD2004FBYZ-01YCBB1 | 2 TB   | 5       | 275   | 0     | 0.75   |
| WDC       | WD800BB-56JKC0     | 80 GB  | 6       | 735   | 7     | 0.75   |
| WDC       | WD1600AAJS-08L7A0  | 160 GB | 12      | 900   | 110   | 0.75   |
| WDC       | WD3200BPVT-22ZEST0 | 320 GB | 63      | 415   | 57    | 0.75   |
| Seagate   | ST2000VX008-2E3164 | 2 TB   | 10      | 274   | 0     | 0.75   |
| Seagate   | ST1000VT001-1RE172 | 1 TB   | 2       | 273   | 0     | 0.75   |
| WDC       | WD5000LPVT-00FMCT0 | 500 GB | 8       | 279   | 1     | 0.75   |
| WDC       | WD10JPVX-60JC3T0   | 1 TB   | 72      | 361   | 99    | 0.75   |
| WDC       | WD20SDZW-11JJ8S0   | 2 TB   | 7       | 272   | 0     | 0.75   |
| WDC       | WD6400BEVT-80A0RT0 | 640 GB | 3       | 314   | 2     | 0.75   |
| Seagate   | ST1000LM024 HN-... | 1 TB   | 887     | 402   | 46    | 0.75   |
| WDC       | WD3200BPVT-22JJ5T0 | 320 GB | 156     | 332   | 47    | 0.74   |
| Seagate   | ST320DM001 HD322GJ | 320 GB | 8       | 653   | 77    | 0.74   |
| WDC       | WD5000BPVT-00HXZT1 | 500 GB | 20      | 447   | 89    | 0.74   |
| WDC       | WD3000FYYZ-01UL1B3 | 3 TB   | 1       | 271   | 0     | 0.74   |
| WDC       | WD10EADS-114BB1    | 1 TB   | 2       | 1820  | 493   | 0.74   |
| Samsung   | HN-M500MBB         | 500 GB | 48      | 419   | 18    | 0.74   |
| WDC       | WD3200JB-00KFA0    | 320 GB | 3       | 1330  | 8     | 0.74   |
| ExcelStor | J8160S             | 160 GB | 7       | 754   | 3     | 0.74   |
| HGST      | HTS541010A7E630    | 1 TB   | 37      | 319   | 112   | 0.74   |
| Hitachi   | HCS5C1010DLE630    | 1 TB   | 2       | 269   | 0     | 0.74   |
| Seagate   | ST320LM001 HN-M... | 320 GB | 61      | 302   | 1     | 0.74   |
| WDC       | WD10EADS-65M2BX    | 1 TB   | 2       | 807   | 46    | 0.74   |
| WDC       | WD1200BEVS-07RST0  | 120 GB | 2       | 268   | 0     | 0.74   |
| WDC       | WD1600BEVT-00A23T0 | 160 GB | 8       | 449   | 66    | 0.74   |
| Seagate   | ST3000DM001-9YN166 | 3 TB   | 37      | 864   | 866   | 0.74   |
| Toshiba   | MK1031GAS          | 100 GB | 3       | 433   | 3     | 0.74   |
| Seagate   | ST2000DX001-SSH... | 2 TB   | 1       | 805   | 2     | 0.74   |
| WDC       | WD3200BPVT-80JJ5T0 | 320 GB | 66      | 327   | 47    | 0.74   |
| WDC       | WD2500AAJB-57R1A0  | 250 GB | 1       | 268   | 0     | 0.73   |
| Seagate   | ST4000LM024-2AN17V | 4 TB   | 19      | 340   | 9     | 0.73   |
| Hitachi   | HTS547550A9E384    | 500 GB | 188     | 484   | 305   | 0.73   |
| WDC       | WD1200JD-22HBB0    | 120 GB | 2       | 1602  | 5     | 0.73   |
| WDC       | WD10EZEX-08WN4A0   | 1 TB   | 425     | 288   | 7     | 0.73   |
| WDC       | WD3200LPVX-60V0TT0 | 320 GB | 1       | 266   | 0     | 0.73   |
| WDC       | WD5000LMVW-11CKRS0 | 500 GB | 2       | 265   | 0     | 0.73   |
| Hitachi   | HTS545016B9A300    | 160 GB | 62      | 406   | 49    | 0.73   |
| MediaMax  | WL1000GSA3272C     | 1 TB   | 1       | 265   | 0     | 0.73   |
| Samsung   | HM251HI            | 250 GB | 9       | 340   | 2     | 0.73   |
| WDC       | WD2500BEKT-00A25T0 | 250 GB | 1       | 264   | 0     | 0.73   |
| WDC       | WD5000AZLX-75K2TA0 | 500 GB | 12      | 264   | 0     | 0.73   |
| Hitachi   | HTS542516K9A300    | 160 GB | 7       | 761   | 189   | 0.73   |
| WDC       | WD2500AAKX-321CA0  | 250 GB | 1       | 264   | 0     | 0.72   |
| WDC       | WD10EURX-83UY4Y0   | 1 TB   | 2       | 970   | 165   | 0.72   |
| WDC       | WD2500AAJS-60B4A0  | 250 GB | 1       | 263   | 0     | 0.72   |
| WDC       | WD5000AZLX-60K2TA0 | 500 GB | 16      | 303   | 1     | 0.72   |
| Seagate   | ST32000542AS       | 2 TB   | 35      | 729   | 380   | 0.72   |
| WDC       | WD2500BEKX-00B7WT0 | 250 GB | 2       | 263   | 0     | 0.72   |
| Toshiba   | MQ01ABF032         | 320 GB | 39      | 324   | 56    | 0.72   |
| Seagate   | ST9750420AS        | 752 GB | 81      | 556   | 107   | 0.72   |
| WDC       | WD121KRYZ-01W0RB0  | 12 TB  | 9       | 262   | 0     | 0.72   |
| WDC       | WD2005FBYZ-01YCBB2 | 2 TB   | 7       | 262   | 0     | 0.72   |
| WDC       | WD10PURX-64E5EY0   | 1 TB   | 17      | 369   | 1     | 0.72   |
| WDC       | WD5000LUCT-63RC2Y0 | 500 GB | 3       | 261   | 0     | 0.72   |
| WDC       | WD1600BEVS-60RST0  | 160 GB | 9       | 507   | 254   | 0.72   |
| Fujitsu   | MHX2300BT          | 304 GB | 4       | 723   | 36    | 0.71   |
| WDC       | WD15EARX-22PASB0   | 1.5 TB | 2       | 260   | 0     | 0.71   |
| WDC       | WD5000LPVX-08V0TT6 | 500 GB | 2       | 260   | 0     | 0.71   |
| Hitachi   | HTS722010K9SA00    | 100 GB | 6       | 865   | 9     | 0.71   |
| WDC       | WD10SPCX-60KHST0   | 1 TB   | 4       | 298   | 1     | 0.71   |
| IBM/Hi... | IC35L040AVVA07-0   | 41 GB  | 4       | 623   | 83    | 0.71   |
| Seagate   | ST320011A          | 20 GB  | 7       | 489   | 5     | 0.71   |
| WDC       | WD3200BEVT-80A0RT0 | 320 GB | 46      | 452   | 57    | 0.71   |
| Toshiba   | MK1665GSX H        | 160 GB | 3       | 324   | 3     | 0.71   |
| Samsung   | HM320II            | 320 GB | 27      | 394   | 189   | 0.71   |
| Seagate   | ST330013A          | 32 GB  | 1       | 259   | 0     | 0.71   |
| WDC       | WD7500BPKX-00HPJT0 | 752 GB | 15      | 350   | 42    | 0.71   |
| WDC       | WD5000LPVT-00G33T0 | 500 GB | 6       | 541   | 2     | 0.71   |
| HGST      | HUH721010ALE604    | 10 TB  | 12      | 258   | 0     | 0.71   |
| Seagate   | ST91208220AS       | 120 GB | 2       | 461   | 507   | 0.71   |
| WDC       | WD5000BPVT-22HXZT1 | 500 GB | 32      | 521   | 77    | 0.71   |
| WDC       | WD7500BPKX-22HPJT0 | 752 GB | 15      | 272   | 1     | 0.71   |
| Seagate   | ST9500325ASG       | 500 GB | 11      | 432   | 205   | 0.71   |
| Seagate   | ST1000NM0055-1V... | 1 TB   | 2       | 682   | 3     | 0.71   |
| Seagate   | ST500DM009-2F110A  | 500 GB | 35      | 262   | 18    | 0.71   |
| Fujitsu   | MHY2120BH          | 120 GB | 34      | 580   | 218   | 0.70   |
| Toshiba   | MQ01ABD100V        | 1 TB   | 9       | 393   | 6     | 0.70   |
| WDC       | WD2500AVJS-63B6A0  | 250 GB | 4       | 666   | 7     | 0.70   |
| WDC       | WD3200BEKT-08PVMT1 | 320 GB | 5       | 255   | 0     | 0.70   |
| WDC       | WD5000LPVX-08V0TT2 | 500 GB | 4       | 314   | 2     | 0.70   |
| WDC       | WD5000BPVT-75HXZT3 | 500 GB | 20      | 466   | 3     | 0.70   |
| Maxtor    | STM3320620AS       | 320 GB | 2       | 254   | 0     | 0.70   |
| HP        | MM0500EANCR        | 500 GB | 13      | 1725  | 49    | 0.70   |
| WDC       | WD2500AAJS-60Z0A0  | 250 GB | 4       | 975   | 4     | 0.70   |
| WDC       | WD3200BEKT-00F3T0  | 320 GB | 2       | 253   | 0     | 0.69   |
| Samsung   | HD161HJ            | 160 GB | 66      | 895   | 526   | 0.69   |
| WDC       | WD10JMVW-11AJGS4   | 1 TB   | 47      | 280   | 38    | 0.69   |
| WDC       | WD5000AZRZ-00HTKB0 | 500 GB | 18      | 317   | 1     | 0.69   |
| Samsung   | HD250HJ            | 250 GB | 50      | 816   | 635   | 0.69   |
| Seagate   | ST1000VX000-1ES162 | 1 TB   | 20      | 253   | 0     | 0.69   |
| WDC       | WD5000AZLX-00K2TA0 | 500 GB | 14      | 252   | 0     | 0.69   |
| WDC       | WD7500AZEX-00BN5A0 | 752 GB | 1       | 252   | 0     | 0.69   |
| Hitachi   | HTS545025B9A300    | 250 GB | 154     | 467   | 92    | 0.69   |
| Hitachi   | HTS547575A9E384    | 640 GB | 174     | 534   | 457   | 0.69   |
| HGST      | HUH721212ALE604    | 12 TB  | 8       | 252   | 0     | 0.69   |
| WDC       | WD5000AAKS-07A7B0  | 500 GB | 3       | 754   | 6     | 0.69   |
| Seagate   | ST9160411ASG       | 160 GB | 3       | 600   | 3     | 0.69   |
| WDC       | WD120EMAZ-11BLFA0  | 12 TB  | 8       | 251   | 0     | 0.69   |
| WDC       | WD5000LPCX-24C6HT0 | 500 GB | 79      | 313   | 29    | 0.69   |
| WDC       | WD4003FFBX-68MU3N0 | 4 TB   | 7       | 250   | 0     | 0.69   |
| WDC       | WD10JPVX-55JC3T3   | 1 TB   | 3       | 602   | 343   | 0.69   |
| WDC       | WD2500JB-00REA0    | 250 GB | 10      | 673   | 26    | 0.68   |
| WDC       | WD50NMZW-59LG6S1   | 5 TB   | 2       | 249   | 0     | 0.68   |
| WDC       | WD6400BPVT-22HXZT1 | 640 GB | 8       | 581   | 3     | 0.68   |
| Seagate   | ST380211AS         | 80 GB  | 12      | 610   | 549   | 0.68   |
| WDC       | WD5000AAKB-00H8A0  | 500 GB | 18      | 656   | 9     | 0.68   |
| WDC       | WD10JPCX-24UE4T0   | 1 TB   | 92      | 329   | 28    | 0.68   |
| Seagate   | ST9640320AS        | 640 GB | 21      | 543   | 280   | 0.68   |
| Seagate   | ST2000LM015-2E8174 | 2 TB   | 105     | 282   | 59    | 0.68   |
| Seagate   | ST3120813AS        | 120 GB | 25      | 889   | 559   | 0.68   |
| WDC       | WD40EZRZ-19GXCB0   | 4 TB   | 8       | 247   | 0     | 0.68   |
| WDC       | WD3200BEVT-60ZCT0  | 320 GB | 7       | 536   | 41    | 0.68   |
| WDC       | WD2000JS-00MHB1    | 200 GB | 1       | 246   | 0     | 0.68   |
| Hitachi   | HCT721016SLA380    | 160 GB | 3       | 246   | 0     | 0.67   |
| Fujitsu   | MJA2500BH FFS G1   | 500 GB | 1       | 246   | 0     | 0.67   |
| WDC       | WD3000HLHX-01JJPV0 | 304 GB | 4       | 671   | 3     | 0.67   |
| WDC       | WD2500BEVT-24A23T0 | 250 GB | 26      | 500   | 85    | 0.67   |
| WDC       | WD4005FZBX-00K5WB0 | 4 TB   | 22      | 244   | 0     | 0.67   |
| WDC       | WD5000BEVT-00ZAT0  | 500 GB | 8       | 442   | 149   | 0.67   |
| Hitachi   | HDP725050GLAT80    | 500 GB | 2       | 664   | 2     | 0.67   |
| WDC       | WD400UE-22HCT0     | 40 GB  | 1       | 732   | 2     | 0.67   |
| Toshiba   | MQ01ABD100         | 1 TB   | 612     | 351   | 112   | 0.67   |
| WDC       | WD5000BEVT-11A0RT0 | 500 GB | 1       | 243   | 0     | 0.67   |
| Toshiba   | DT01ACA100 LENOVO  | 1 TB   | 6       | 243   | 0     | 0.67   |
| Fujitsu   | MHV2120BH          | 120 GB | 3       | 371   | 3     | 0.67   |
| Toshiba   | MQ01ABD032         | 320 GB | 104     | 359   | 154   | 0.67   |
| WDC       | WD10JPVT-08A1YT2   | 1 TB   | 13      | 516   | 34    | 0.67   |
| WDC       | WD3200BEVT-00A0RT0 | 320 GB | 24      | 309   | 9     | 0.66   |
| WDC       | WD3000JD-55KLB0    | 304 GB | 1       | 969   | 3     | 0.66   |
| Hitachi   | HTS543225A7A384    | 250 GB | 44      | 371   | 304   | 0.66   |
| WDC       | WD10EZEX-35WN4A0   | 1 TB   | 6       | 242   | 0     | 0.66   |
| Seagate   | ST1000VX005-2EZ102 | 1 TB   | 13      | 242   | 0     | 0.66   |
| Fujitsu   | MHW2080AT          | 80 GB  | 1       | 241   | 0     | 0.66   |
| Hitachi   | HTS545032A7E380    | 320 GB | 34      | 432   | 223   | 0.66   |
| HGST      | HUS726040ALA614    | 4 TB   | 7       | 243   | 2     | 0.66   |
| Samsung   | HD320KJ            | 320 GB | 5       | 888   | 277   | 0.66   |
| WDC       | WD7500BPVT-08HXZT3 | 752 GB | 6       | 516   | 13    | 0.66   |
| WDC       | WD15EARS-00Z5B1    | 1.5 TB | 36      | 1298  | 432   | 0.66   |
| WDC       | WD5000AAKX-003CA0  | 500 GB | 48      | 807   | 40    | 0.66   |
| WDC       | WD1600BEVT-00ZCT0  | 160 GB | 8       | 262   | 1     | 0.66   |
| WDC       | WD2500AAKX-07U6AA1 | 250 GB | 2       | 239   | 0     | 0.65   |
| Seagate   | ST6000NM0115-1Y... | 6 TB   | 15      | 238   | 0     | 0.65   |
| Fujitsu   | MHW2160BH PL       | 160 GB | 13      | 646   | 257   | 0.65   |
| HP        | MB1000GCWCV        | 1 TB   | 1       | 238   | 0     | 0.65   |
| WDC       | WD100EZAZ-11TDBA0  | 10 TB  | 15      | 237   | 0     | 0.65   |
| HGST      | HTS541010A9E680    | 1 TB   | 292     | 432   | 410   | 0.65   |
| Hitachi   | HTS721010G9SA00    | 100 GB | 7       | 1041  | 176   | 0.65   |
| Seagate   | ST9120823AS        | 120 GB | 1       | 712   | 2     | 0.65   |
| Maxtor    | 6V320F0            | 320 GB | 3       | 649   | 4     | 0.65   |
| Hitachi   | HTS541010G9AT00    | 100 GB | 1       | 474   | 1     | 0.65   |
| WDC       | WD5000LPCX-35VHAT0 | 500 GB | 2       | 236   | 0     | 0.65   |
| WDC       | WD20PURZ-85GU6Y0   | 2 TB   | 23      | 323   | 87    | 0.65   |
| Seagate   | ST1000VM002-9ZL162 | 1 TB   | 3       | 515   | 733   | 0.65   |
| WDC       | WD1000CHTZ-04JCPV0 | 1 TB   | 2       | 236   | 0     | 0.65   |
| WDC       | WD5000AZLX-00JKKA0 | 500 GB | 12      | 289   | 47    | 0.65   |
| Samsung   | HD200HJ            | 200 GB | 19      | 824   | 598   | 0.65   |
| Seagate   | ST500LM000-1EJ162  | 500 GB | 106     | 372   | 52    | 0.65   |
| WDC       | WD2500AAJS-00B4A0  | 250 GB | 21      | 745   | 50    | 0.65   |
| WDC       | WD10EACS-65D6B0    | 1 TB   | 2       | 300   | 71    | 0.65   |
| Seagate   | ST3402111A         | 40 GB  | 3       | 270   | 24    | 0.65   |
| WDC       | WD5000BEVT-22ZAT0  | 500 GB | 28      | 592   | 110   | 0.65   |
| Hitachi   | HTS727550A9E364    | 500 GB | 24      | 516   | 436   | 0.65   |
| Toshiba   | MK6459GSXP         | 640 GB | 16      | 614   | 544   | 0.65   |
| WDC       | WD40NPZZ-00PDPT0   | 4 TB   | 3       | 235   | 0     | 0.65   |
| Seagate   | ST500LM011 HM501II | 500 GB | 2       | 277   | 1     | 0.64   |
| Toshiba   | MK6465GSXN         | 640 GB | 9       | 439   | 175   | 0.64   |
| WDC       | WD10JPVT-80A1YT0   | 1 TB   | 1       | 235   | 0     | 0.64   |
| WDC       | WD10SPZX-17Z10T1   | 1 TB   | 7       | 234   | 0     | 0.64   |
| WDC       | WD3200BEKT-75KA9T0 | 320 GB | 1       | 234   | 0     | 0.64   |
| Seagate   | ST1000DX002-2DV162 | 1 TB   | 27      | 237   | 1     | 0.64   |
| WDC       | WD1600JS-60NCB1    | 160 GB | 5       | 603   | 64    | 0.64   |
| MediaMax  | WL250GSA1672       | 250 GB | 1       | 2108  | 8     | 0.64   |
| WDC       | WD5003ABYX-23 0... | 500 GB | 1       | 234   | 0     | 0.64   |
| Maxtor    | STM380811AS        | 80 GB  | 5       | 477   | 8     | 0.64   |
| WDC       | WD3200BPVT-55ZEST0 | 320 GB | 5       | 355   | 28    | 0.64   |
| WDC       | WD5000AADS-67S9B0  | 500 GB | 1       | 2104  | 8     | 0.64   |
| Seagate   | ST340016A          | 40 GB  | 37      | 679   | 30    | 0.64   |
| Seagate   | ST2000LM005 HN-... | 2 TB   | 9       | 233   | 0     | 0.64   |
| WDC       | WD10SPCX-24HWST1   | 1 TB   | 37      | 284   | 31    | 0.64   |
| Toshiba   | MK3255GSX          | 320 GB | 1       | 233   | 0     | 0.64   |
| Seagate   | ST2000LX001-1RG174 | 2 TB   | 64      | 291   | 63    | 0.64   |
| Hitachi   | HTS541075A9E680    | 752 GB | 8       | 400   | 510   | 0.64   |
| Hitachi   | HUS724040ALE641    | 4 TB   | 10      | 232   | 1     | 0.64   |
| Seagate   | ST500LM000-1EJ1... | 500 GB | 18      | 281   | 22    | 0.64   |
| Seagate   | ST1000LM014-SSH... | 1 TB   | 33      | 392   | 256   | 0.64   |
| Hitachi   | HTS725050A7E630    | 500 GB | 18      | 388   | 640   | 0.64   |
| WDC       | WD6400BPVT-26HXZT1 | 640 GB | 1       | 232   | 0     | 0.64   |
| WDC       | WD5000LPCX-22VHAT0 | 500 GB | 35      | 235   | 1     | 0.64   |
| WDC       | WD5000LPCX-00VHAT0 | 500 GB | 41      | 263   | 1     | 0.64   |
| HGST      | HTE721010A9E630    | 1 TB   | 7       | 501   | 3     | 0.64   |
| WDC       | WD6401AALS-00E3A0  | 640 GB | 5       | 692   | 6     | 0.64   |
| HGST      | HTS725032A7E635... | 320 GB | 1       | 231   | 0     | 0.64   |
| WDC       | WD10EADS-65P6B0    | 1 TB   | 2       | 1537  | 7     | 0.63   |
| WDC       | WD10EZEX-00MFCA0   | 1 TB   | 24      | 257   | 3     | 0.63   |
| Seagate   | ST9750423AS        | 752 GB | 19      | 562   | 238   | 0.63   |
| WDC       | WD161KRYZ-01AGBB0  | 16 TB  | 2       | 230   | 0     | 0.63   |
| Seagate   | ST360014A          | 64 GB  | 4       | 584   | 12    | 0.63   |
| WDC       | WD80EFAX-68KNBN0   | 8 TB   | 32      | 230   | 0     | 0.63   |
| Hitachi   | HTS727575A9E364    | 752 GB | 28      | 691   | 295   | 0.63   |
| Seagate   | ST1000VN002-2EY102 | 1 TB   | 8       | 260   | 123   | 0.63   |
| Toshiba   | Generic L200 Ha... | 2 TB   | 2       | 229   | 0     | 0.63   |
| Toshiba   | MQ01ABD050V        | 500 GB | 14      | 292   | 188   | 0.63   |
| WDC       | WD3200BUCT-63TWBY0 | 320 GB | 5       | 300   | 2     | 0.63   |
| Seagate   | ST3160212ACE       | 160 GB | 4       | 512   | 27    | 0.63   |
| WDC       | WD800BB-98JHC0     | 80 GB  | 1       | 1829  | 7     | 0.63   |
| Fujitsu   | MHZ2160BH G1       | 160 GB | 10      | 341   | 2     | 0.63   |
| WDC       | WD10TMVW-11ZSMS1   | 1 TB   | 2       | 532   | 2     | 0.62   |
| WDC       | WD10SPZX-75Z10T1   | 1 TB   | 22      | 237   | 2     | 0.62   |
| WDC       | WD3200AAKS-00V6A0  | 320 GB | 3       | 315   | 1     | 0.62   |
| WDC       | WD4000FYYZ-01UL1B0 | 4 TB   | 3       | 1746  | 9     | 0.62   |
| Seagate   | ST95005620AS       | 500 GB | 24      | 643   | 97    | 0.62   |
| WDC       | WD20SDZW-11Z3CS1   | 2 TB   | 1       | 226   | 0     | 0.62   |
| Fujitsu   | MHT2080AH          | 80 GB  | 2       | 370   | 32    | 0.62   |
| WDC       | WD5000BEKT-80KA9T1 | 500 GB | 4       | 280   | 1     | 0.62   |
| Toshiba   | MK2555GSXF         | 250 GB | 8       | 225   | 0     | 0.62   |
| WDC       | WD6400BEVT-00A0RT0 | 640 GB | 3       | 644   | 51    | 0.62   |
| WDC       | WD10EZRZ-00HTKB0   | 1 TB   | 70      | 253   | 19    | 0.62   |
| Samsung   | HM500JJ            | 500 GB | 4       | 326   | 3     | 0.62   |
| Toshiba   | MK2561GSYN         | 250 GB | 9       | 226   | 6     | 0.62   |
| Toshiba   | MK5076GSXN         | 500 GB | 1       | 224   | 0     | 0.62   |
| Seagate   | ST3120211AS        | 120 GB | 5       | 517   | 12    | 0.61   |
| WDC       | WD800BD-22MRA1     | 80 GB  | 6       | 956   | 61    | 0.61   |
| WDC       | WD15EARS-22MVWB0   | 1.5 TB | 7       | 626   | 221   | 0.61   |
| Toshiba   | MQ01ACF050         | 500 GB | 70      | 311   | 62    | 0.61   |
| WDC       | WD2500AAJS-65M0A0  | 250 GB | 3       | 665   | 13    | 0.61   |
| Toshiba   | MG07ACA14TE        | 14 TB  | 4       | 223   | 0     | 0.61   |
| Toshiba   | HDWE140            | 4 TB   | 38      | 261   | 34    | 0.61   |
| Seagate   | ST4000VX007-2DT166 | 4 TB   | 17      | 222   | 0     | 0.61   |
| Toshiba   | HDWG180            | 8 TB   | 4       | 222   | 0     | 0.61   |
| WDC       | WD10SPZX-75Z10T0   | 1 TB   | 4       | 221   | 0     | 0.61   |
| WDC       | WD5000BPKX-60HPJT0 | 500 GB | 5       | 492   | 47    | 0.61   |
| Seagate   | ST2000NM0055-1V... | 2 TB   | 3       | 221   | 0     | 0.61   |
| Fujitsu   | MHW2120BJ FFS G2   | 120 GB | 1       | 221   | 0     | 0.61   |
| WDC       | WD10PURZ-85U8XY0   | 1 TB   | 19      | 266   | 1     | 0.61   |
| WDC       | WD1600BEKT-60F3T1  | 160 GB | 1       | 221   | 0     | 0.61   |
| HGST      | HTS725050A7E630    | 500 GB | 227     | 432   | 289   | 0.61   |
| HGST      | HTS545032A7E680    | 320 GB | 17      | 294   | 80    | 0.61   |
| WDC       | WD3200BPVT-24ZEST0 | 320 GB | 26      | 351   | 47    | 0.61   |
| WDC       | WD2500AAKS-60VYA0  | 250 GB | 1       | 221   | 0     | 0.61   |
| Seagate   | ST9500530NS        | 500 GB | 3       | 1402  | 99    | 0.60   |
| Seagate   | ST3000DM007-1WY10G | 3 TB   | 21      | 220   | 0     | 0.60   |
| Toshiba   | DT01ABA300V        | 3 TB   | 1       | 220   | 0     | 0.60   |
| WDC       | WD10EZEX-07ZF5A0   | 1 TB   | 3       | 626   | 4     | 0.60   |
| Seagate   | ST9500423AS        | 500 GB | 49      | 480   | 81    | 0.60   |
| WDC       | WD800BB-00FRA0     | 80 GB  | 5       | 668   | 10    | 0.60   |
| WDC       | WD3200AAKX-073CA1  | 320 GB | 3       | 358   | 3     | 0.60   |
| Toshiba   | MK1059GSMP         | 1 TB   | 23      | 509   | 403   | 0.60   |
| Toshiba   | MQ04UBB400         | 4 TB   | 25      | 218   | 0     | 0.60   |
| WDC       | WD60EZRZ-00GZ5B1   | 6 TB   | 14      | 218   | 0     | 0.60   |
| WDC       | WD1200BEVS-00UST0  | 120 GB | 4       | 232   | 1     | 0.60   |
| WDC       | WD3200BEKT-60V5T1  | 320 GB | 34      | 493   | 320   | 0.60   |
| WDC       | WD20NPVT-00Z2TT0   | 2 TB   | 3       | 336   | 12    | 0.60   |
| Fujitsu   | MHZ2320BH G2       | 320 GB | 22      | 478   | 361   | 0.60   |
| WDC       | WD5000BPVT-22A1YT0 | 500 GB | 11      | 217   | 0     | 0.60   |
| Seagate   | ST1000DM010-2EP102 | 1 TB   | 567     | 240   | 26    | 0.60   |
| WDC       | WD1600JB-00GVC0    | 160 GB | 2       | 777   | 3     | 0.59   |
| WDC       | WD5002AALX-32Z3A0  | 500 GB | 2       | 647   | 1     | 0.59   |
| WDC       | WD2500BEVT-00ZCT0  | 250 GB | 11      | 231   | 1     | 0.59   |
| WDC       | WD3200AVJS-63B6A0  | 320 GB | 9       | 1098  | 14    | 0.59   |
| Seagate   | ST9160412ASG       | 160 GB | 3       | 216   | 0     | 0.59   |
| WDC       | WD800BB-55JKC0     | 80 GB  | 10      | 633   | 95    | 0.59   |
| WDC       | WD3200LPVX-75V0TT0 | 320 GB | 4       | 216   | 0     | 0.59   |
| Toshiba   | MK6475GSX          | 640 GB | 43      | 389   | 274   | 0.59   |
| WDC       | WD3200AZDX-00SC2B0 | 320 GB | 2       | 379   | 440   | 0.59   |
| WDC       | WD3200BPVT-00ZEST0 | 320 GB | 4       | 215   | 0     | 0.59   |
| Fujitsu   | MHW2040BH          | 40 GB  | 3       | 250   | 1     | 0.59   |
| Hitachi   | HTS543216L9A300    | 160 GB | 64      | 520   | 173   | 0.59   |
| Toshiba   | MK5055GSXN         | 500 GB | 2       | 392   | 4     | 0.59   |
| WDC       | WD5000BPVT-55HXZT4 | 500 GB | 1       | 214   | 0     | 0.59   |
| Samsung   | SP1624N            | 160 GB | 2       | 213   | 0     | 0.59   |
| WDC       | WD3200BEVT-22A23T0 | 320 GB | 53      | 484   | 76    | 0.59   |
| WDC       | WD5000LPLX-60ZNTT0 | 500 GB | 2       | 213   | 0     | 0.58   |
| Samsung   | HM250HI            | 250 GB | 93      | 340   | 39    | 0.58   |
| Fujitsu   | MPE3084AE          | 8 GB   | 1       | 213   | 0     | 0.58   |
| Seagate   | ST1000UM000-1EK164 | 1 TB   | 3       | 212   | 0     | 0.58   |
| Fujitsu   | MHV2080AH          | 80 GB  | 7       | 500   | 11    | 0.58   |
| WDC       | WD5000AAKS-00V6A0  | 500 GB | 8       | 746   | 9     | 0.58   |
| Hitachi   | HTS541660J9SA00    | 64 GB  | 6       | 468   | 5     | 0.58   |
| WDC       | WD1600BEVT-08A23T1 | 160 GB | 2       | 212   | 0     | 0.58   |
| Toshiba   | MK3263GSX          | 320 GB | 12      | 728   | 127   | 0.58   |
| Hitachi   | HTS542516K9SA00    | 160 GB | 76      | 661   | 216   | 0.58   |
| Hitachi   | HTS545025B9SA00    | 250 GB | 3       | 211   | 0     | 0.58   |
| WDC       | WD1600AAJB-22WRA0  | 160 GB | 3       | 531   | 2     | 0.58   |
| Samsung   | HD082GJ            | 80 GB  | 24      | 491   | 396   | 0.58   |
| HGST      | HEJ423232H9E300    | 320 GB | 1       | 211   | 0     | 0.58   |
| WDC       | WD2500BEVT-00A23T0 | 250 GB | 12      | 482   | 9     | 0.58   |
| WDC       | WD3200BEKX-00B7WT0 | 320 GB | 8       | 213   | 2     | 0.58   |
| Fujitsu   | MHV2100AT PL       | 100 GB | 3       | 210   | 0     | 0.58   |
| WDC       | WD5000AZLX-08K2TA0 | 500 GB | 30      | 217   | 1     | 0.58   |
| Toshiba   | MK6461GSY          | 640 GB | 4       | 254   | 183   | 0.58   |
| Toshiba   | DT01ABA100         | 1 TB   | 1       | 209   | 0     | 0.57   |
| WDC       | WD10EALX-229BA0    | 1 TB   | 5       | 793   | 11    | 0.57   |
| Seagate   | ST5000VX0011-1T... | 5 TB   | 1       | 208   | 0     | 0.57   |
| WDC       | WD5000BEKT-80KA9T0 | 500 GB | 3       | 317   | 1     | 0.57   |
| Maxtor    | STM3500630AS       | 500 GB | 2       | 243   | 73    | 0.57   |
| WDC       | WD800BEVS-00RST0   | 80 GB  | 3       | 277   | 1     | 0.57   |
| IBM/Hi... | IC35L040AVVN07-0   | 41 GB  | 2       | 576   | 3     | 0.57   |
| WDC       | WD400BB-00FJA0     | 40 GB  | 2       | 699   | 222   | 0.57   |
| WDC       | WD10EZEX-07M2NA0   | 1 TB   | 4       | 538   | 5     | 0.57   |
| WDC       | WD2500BEVT-22A23T0 | 250 GB | 68      | 417   | 59    | 0.57   |
| Seagate   | ST32500NSSUN250G   | 250 GB | 1       | 1455  | 6     | 0.57   |
| WDC       | WD1600AAJB-56WRA0  | 160 GB | 2       | 571   | 2     | 0.57   |
| WDC       | WD20SPZX-75UA7T0   | 2 TB   | 5       | 207   | 0     | 0.57   |
| HGST      | HTE725050A7E630    | 500 GB | 3       | 207   | 0     | 0.57   |
| WDC       | WD20SDZW-11Z3CS0   | 2 TB   | 5       | 207   | 0     | 0.57   |
| Fujitsu   | MHT2080AT PL       | 80 GB  | 1       | 207   | 0     | 0.57   |
| Samsung   | SP0802N            | 80 GB  | 27      | 685   | 46    | 0.57   |
| Toshiba   | MK2575GSX          | 250 GB | 2       | 272   | 538   | 0.56   |
| WDC       | WD3200BEVT-75A23T0 | 320 GB | 4       | 251   | 35    | 0.56   |
| Toshiba   | MQ01ABD100M        | 1 TB   | 13      | 256   | 18    | 0.56   |
| WDC       | WD5000AAKX-08ANVA0 | 500 GB | 4       | 241   | 2     | 0.56   |
| WDC       | WD1200JB-00GVC0    | 120 GB | 3       | 539   | 4     | 0.56   |
| Hitachi   | HTS547564A9E384    | 640 GB | 59      | 529   | 449   | 0.56   |
| WDC       | WD10EADS-65M2B1    | 1 TB   | 9       | 1049  | 114   | 0.56   |
| Hitachi   | HCC543225A7A380    | 250 GB | 2       | 912   | 2     | 0.56   |
| Seagate   | ST12000VN0008-2... | 12 TB  | 6       | 204   | 0     | 0.56   |
| Apple     | HDD HTS547550A9... | 500 GB | 7       | 316   | 14    | 0.56   |
| Toshiba   | MQ02ABF100         | 1 TB   | 10      | 216   | 1     | 0.56   |
| Maxtor    | 6V250F0            | 250 GB | 3       | 497   | 2     | 0.56   |
| WDC       | WD5000BMVW-11AJGS3 | 500 GB | 2       | 203   | 0     | 0.56   |
| Maxtor    | 6L040J2            | 40 GB  | 2       | 1365  | 6     | 0.56   |
| WDC       | WD3200LPCX-24C6HT0 | 320 GB | 25      | 219   | 1     | 0.56   |
| WDC       | WD20EURX-63T0FY0   | 2 TB   | 14      | 416   | 148   | 0.56   |
| WDC       | WD5000AAKS-60Z1A0  | 500 GB | 7       | 1088  | 55    | 0.56   |
| WDC       | WD2500AAKS-00B3A0  | 250 GB | 6       | 636   | 8     | 0.56   |
| WDC       | WD10SPCX-21KHST0   | 1 TB   | 5       | 203   | 0     | 0.56   |
| WDC       | WD3200BEKX-60B7WT0 | 320 GB | 2       | 203   | 0     | 0.56   |
| Toshiba   | MK6006GAH          | 64 GB  | 2       | 203   | 0     | 0.56   |
| WDC       | WD1003FBYX-50Y7B0  | 1 TB   | 1       | 202   | 0     | 0.56   |
| Seagate   | ST9500420AS        | 500 GB | 131     | 607   | 517   | 0.56   |
| Toshiba   | MQ04UBF100         | 1 TB   | 47      | 221   | 3     | 0.55   |
| Toshiba   | MK1653GSX          | 160 GB | 1       | 201   | 0     | 0.55   |
| WDC       | WD800JD-00JNC0     | 80 GB  | 4       | 451   | 16    | 0.55   |
| Seagate   | ST10000DM0004-1... | 10 TB  | 6       | 264   | 2     | 0.55   |
| Toshiba   | MK8034GSX          | 80 GB  | 12      | 451   | 27    | 0.55   |
| Hitachi   | HTS721080G9SA00    | 80 GB  | 8       | 342   | 26    | 0.55   |
| Hitachi   | HTS723232A7A364    | 320 GB | 70      | 458   | 434   | 0.55   |
| Seagate   | ST500LT015-1DJ142  | 500 GB | 2       | 200   | 0     | 0.55   |
| Toshiba   | MK3276GSX -63      | 320 GB | 9       | 325   | 62    | 0.55   |
| WDC       | WD10EADS-22M2B0    | 1 TB   | 15      | 672   | 6     | 0.55   |
| Seagate   | ST6000VN0001-1S... | 6 TB   | 1       | 200   | 0     | 0.55   |
| WDC       | WD740GD-00FLC0     | 74 GB  | 1       | 1202  | 5     | 0.55   |
| WDC       | WD20PURX-64PFUY0   | 2 TB   | 3       | 200   | 0     | 0.55   |
| WDC       | WD5000AAKS-00E4A0  | 500 GB | 11      | 966   | 42    | 0.55   |
| Seagate   | ST14000NM001G-2... | 14 TB  | 7       | 199   | 0     | 0.55   |
| HGST      | HTS541010B7E610    | 1 TB   | 60      | 212   | 2     | 0.55   |
| WDC       | WD30NMZW-11GX6S1   | 3 TB   | 6       | 217   | 1     | 0.55   |
| WDC       | WD7500BPVT-60HXZT3 | 752 GB | 12      | 548   | 175   | 0.55   |
| Seagate   | ST320LT009-9WC142  | 320 GB | 4       | 267   | 1     | 0.55   |
| Toshiba   | MK6034GAX          | 64 GB  | 4       | 663   | 352   | 0.55   |
| WDC       | WD5000BEKT-60KA9T0 | 500 GB | 7       | 345   | 41    | 0.54   |
| Hitachi   | HDS721050DLE630    | 500 GB | 58      | 475   | 442   | 0.54   |
| Toshiba   | MK2552GSX          | 250 GB | 25      | 777   | 269   | 0.54   |
| WDC       | WD5000LPLX-60ZNTT2 | 500 GB | 4       | 197   | 0     | 0.54   |
| WDC       | WD5000AARS-003BB1  | 500 GB | 5       | 568   | 7     | 0.54   |
| WDC       | WD2500BEKT-75A25T0 | 250 GB | 8       | 480   | 47    | 0.54   |
| HP        | Secure Hard Disk   | 500 GB | 1       | 197   | 0     | 0.54   |
| Seagate   | ST9160823AS        | 160 GB | 8       | 795   | 544   | 0.54   |
| HGST      | HUS722T1TALA600    | 1 TB   | 4       | 197   | 0     | 0.54   |
| Seagate   | ST9120822AS        | 120 GB | 59      | 459   | 430   | 0.54   |
| WDC       | WD5000BEVT-60A0RT0 | 500 GB | 5       | 612   | 368   | 0.54   |
| Seagate   | ST3750528AS        | 752 GB | 46      | 731   | 358   | 0.54   |
| WDC       | WD1600BEVT-22A23T0 | 160 GB | 28      | 352   | 5     | 0.54   |
| Quantum   | FIREBALLlct15 30   | 32 GB  | 1       | 391   | 1     | 0.54   |
| Hitachi   | HDS721612PLAT80    | 128 GB | 1       | 1366  | 6     | 0.53   |
| Hitachi   | HTS723216A7A364    | 160 GB | 2       | 359   | 512   | 0.53   |
| Toshiba   | MK6034GSX          | 64 GB  | 4       | 423   | 18    | 0.53   |
| Seagate   | ST94011A           | 40 GB  | 1       | 194   | 0     | 0.53   |
| Fujitsu   | MHW2080BJ G2       | 80 GB  | 2       | 362   | 66    | 0.53   |
| Seagate   | ST320414A          | 20 GB  | 1       | 194   | 0     | 0.53   |
| WDC       | WD1600AAJS-60M0A1  | 160 GB | 3       | 840   | 343   | 0.53   |
| Seagate   | ST940210AS         | 40 GB  | 4       | 268   | 1     | 0.53   |
| Seagate   | ST3120213A         | 120 GB | 12      | 662   | 642   | 0.53   |
| IBM       | DARA-212000        | 12 GB  | 1       | 193   | 0     | 0.53   |
| Hitachi   | HTS541080G9SA00    | 80 GB  | 8       | 444   | 82    | 0.53   |
| WDC       | WD1600AVVS-63L2B0  | 160 GB | 10      | 620   | 4     | 0.53   |
| WDC       | WD5000LMVW-11VEDS0 | 500 GB | 3       | 193   | 0     | 0.53   |
| Seagate   | ST2000LM007-1R8174 | 2 TB   | 142     | 224   | 103   | 0.53   |
| WDC       | WD400BB-00DKA0     | 40 GB  | 1       | 193   | 0     | 0.53   |
| WDC       | WD800BEVS-75RST0   | 80 GB  | 4       | 381   | 252   | 0.53   |
| WDC       | WD1600AAJS-60Z0A0  | 160 GB | 6       | 306   | 175   | 0.53   |
| WDC       | WD800BEVT-22ZCT0   | 80 GB  | 2       | 192   | 0     | 0.53   |
| Hitachi   | HTS543212L9SA02    | 120 GB | 2       | 192   | 0     | 0.53   |
| WDC       | WD10PURX-64D85Y0   | 1 TB   | 4       | 388   | 2     | 0.53   |
| Samsung   | HM100UI            | 1 TB   | 5       | 191   | 0     | 0.53   |
| WDC       | WD5000LMVW-11VEDS2 | 500 GB | 1       | 1147  | 5     | 0.52   |
| WDC       | WD5000LPVX-55V0TT0 | 500 GB | 13      | 254   | 1     | 0.52   |
| WDC       | WD740GD-00FLA0     | 74 GB  | 2       | 2375  | 56    | 0.52   |
| Samsung   | HD161HJ 41R0186LEN | 160 GB | 2       | 551   | 507   | 0.52   |
| WDC       | WD5000BPVT-26HXZT3 | 500 GB | 1       | 190   | 0     | 0.52   |
| Seagate   | ST9250827AS        | 250 GB | 52      | 539   | 499   | 0.52   |
| WDC       | WD10SPZX-35Z10T0   | 1 TB   | 8       | 189   | 0     | 0.52   |
| Seagate   | ST250LM004 HN-M... | 250 GB | 10      | 278   | 5     | 0.52   |
| Hitachi   | HTS542580K9SA00    | 80 GB  | 16      | 360   | 4     | 0.52   |
| WDC       | WD2500BEVT-60ZCT1  | 250 GB | 14      | 352   | 159   | 0.52   |
| WDC       | WD5000KMVW-11ZSMS5 | 500 GB | 1       | 189   | 0     | 0.52   |
| WDC       | WD5000AAKS-08V0A0  | 500 GB | 12      | 613   | 25    | 0.52   |
| WDC       | WD2500BEKT-60A25T1 | 250 GB | 12      | 452   | 93    | 0.52   |
| Seagate   | ST96812A           | 64 GB  | 3       | 379   | 758   | 0.52   |
| WDC       | WD20EFAX-68FB5N0   | 2 TB   | 15      | 188   | 0     | 0.52   |
| WDC       | WD2500BJKT-00F4T0  | 250 GB | 2       | 187   | 0     | 0.51   |
| Toshiba   | MK7575GSX          | 752 GB | 38      | 688   | 677   | 0.51   |
| WDC       | WD5000BPKX-22HPJT0 | 500 GB | 17      | 276   | 1     | 0.51   |
| Seagate   | ST500VM000-1SD101  | 500 GB | 3       | 186   | 0     | 0.51   |
| WDC       | WD6400BEVT-22A0RT0 | 640 GB | 17      | 493   | 40    | 0.51   |
| Hitachi   | HTS542525K9SA00    | 250 GB | 46      | 609   | 122   | 0.51   |
| WDC       | WD10JPVX-60JC3T1   | 1 TB   | 43      | 225   | 32    | 0.51   |
| Toshiba   | MD05ACA800         | 8 TB   | 2       | 185   | 0     | 0.51   |
| WDC       | WD10JPVT-22A1YT0   | 1 TB   | 9       | 382   | 3     | 0.51   |
| Seagate   | ST8000VN004-2M2101 | 8 TB   | 30      | 185   | 0     | 0.51   |
| Toshiba   | HDWD110            | 1 TB   | 292     | 203   | 4     | 0.51   |
| Maxtor    | 7V300F0            | 304 GB | 2       | 1022  | 475   | 0.51   |
| Toshiba   | MQ04UBD200         | 2 TB   | 32      | 192   | 1     | 0.51   |
| Seagate   | ST10000NM0086-2... | 10 TB  | 9       | 184   | 0     | 0.51   |
| Toshiba   | MG07ACA12TE        | 12 TB  | 4       | 183   | 0     | 0.50   |
| WDC       | WD1200BB-00GUC0    | 120 GB | 3       | 939   | 9     | 0.50   |
| Quantum   | FIREBALLlct15 15   | 16 GB  | 1       | 183   | 0     | 0.50   |
| WDC       | WD25EZRX-00MMMB0   | 2.5 TB | 3       | 1123  | 9     | 0.50   |
| HGST      | HUS728T8TALE6L4    | 8 TB   | 12      | 182   | 0     | 0.50   |
| Toshiba   | MK1633GSG          | 160 GB | 8       | 303   | 144   | 0.50   |
| Toshiba   | HDWD105            | 500 GB | 98      | 199   | 21    | 0.50   |
| WDC       | WD800JD-60MSA1     | 80 GB  | 2       | 405   | 2     | 0.50   |
| WDC       | WD5000BEVT-00A0RT0 | 500 GB | 15      | 450   | 152   | 0.50   |
| WDC       | WD1000CHTZ-04JCPV1 | 1 TB   | 1       | 181   | 0     | 0.50   |
| WDC       | WD60EZAZ-00ZGHB0   | 6 TB   | 10      | 181   | 0     | 0.50   |
| Seagate   | ST9320423AS        | 320 GB | 81      | 453   | 340   | 0.50   |
| Seagate   | ST9200420ASG       | 200 GB | 5       | 371   | 54    | 0.50   |
| WDC       | WD3200BEVT-24A23T0 | 320 GB | 14      | 525   | 75    | 0.50   |
| Seagate   | ST1000LX015-1U7172 | 1 TB   | 114     | 224   | 48    | 0.50   |
| Fujitsu   | MHZ2500BT G1       | 500 GB | 2       | 1426  | 6     | 0.50   |
| IBM/Hi... | IC25N030ATMR04-0   | 32 GB  | 1       | 544   | 2     | 0.50   |
| WDC       | WD6000BLHX-01V7BV0 | 600 GB | 2       | 181   | 0     | 0.50   |
| Seagate   | ST3000VN007-2AH16M | 3 TB   | 5       | 180   | 0     | 0.50   |
| Seagate   | ST160NM0011 39M... | 160 GB | 1       | 361   | 1     | 0.50   |
| WDC       | WD5000AUDX-73H9TY0 | 500 GB | 1       | 180   | 0     | 0.49   |
| WDC       | WD1200JB-00FUA0    | 120 GB | 1       | 180   | 0     | 0.49   |
| WDC       | WD10EURX-73FH1Y0   | 1 TB   | 8       | 466   | 2     | 0.49   |
| Samsung   | SP1613N            | 160 GB | 2       | 858   | 508   | 0.49   |
| Toshiba   | MK3275GSX          | 320 GB | 27      | 417   | 280   | 0.49   |
| Toshiba   | MK1059GSM          | 1 TB   | 37      | 618   | 767   | 0.49   |
| Samsung   | HE753LJ            | 752 GB | 2       | 374   | 51    | 0.49   |
| Hitachi   | HTS421240H9AT00    | 40 GB  | 2       | 179   | 0     | 0.49   |
| Samsung   | SP0812C            | 80 GB  | 22      | 551   | 223   | 0.49   |
| Seagate   | ST98823AS          | 80 GB  | 15      | 370   | 283   | 0.49   |
| MediaMax  | WL3000GSA6454      | 3.7 TB | 1       | 178   | 0     | 0.49   |
| Seagate   | ST9160823ASG       | 160 GB | 5       | 304   | 204   | 0.49   |
| WDC       | WD50EZRZ-00GZ5B1   | 5 TB   | 2       | 177   | 0     | 0.49   |
| Seagate   | ST10000DM0004-2... | 10 TB  | 6       | 177   | 0     | 0.49   |
| WDC       | WD10TMVW-11ZSMS4   | 1 TB   | 6       | 635   | 5     | 0.49   |
| WDC       | WD5000LPLX-75ZNTT0 | 500 GB | 21      | 203   | 114   | 0.49   |
| WDC       | WD1600BEVT-24A23T0 | 160 GB | 13      | 233   | 2     | 0.49   |
| Toshiba   | MK3265GSXN         | 320 GB | 22      | 496   | 296   | 0.49   |
| WDC       | WD1002FBYS-18A6B0  | 1 TB   | 2       | 2270  | 29    | 0.49   |
| WDC       | WD3200BEVT-75ZCT0  | 320 GB | 3       | 671   | 57    | 0.49   |
| WDC       | WD10SPCX-08HWST0   | 1 TB   | 1       | 177   | 0     | 0.49   |
| Samsung   | HM320HJ            | 320 GB | 6       | 306   | 296   | 0.48   |
| Hitachi   | HTS541616J9SA00    | 160 GB | 42      | 556   | 64    | 0.48   |
| WDC       | WD20EADS-42R6B0    | 2 TB   | 1       | 176   | 0     | 0.48   |
| WDC       | WD3200AAJS-60M0A1  | 320 GB | 6       | 816   | 804   | 0.48   |
| WDC       | WD10SPCX-11HWST0   | 1 TB   | 1       | 351   | 1     | 0.48   |
| Samsung   | HM080HC            | 72 GB  | 1       | 526   | 2     | 0.48   |
| Seagate   | ST980210AS         | 80 GB  | 1       | 175   | 0     | 0.48   |
| Toshiba   | HDWJ110            | 1 TB   | 12      | 265   | 186   | 0.48   |
| Toshiba   | HDWN160            | 6 TB   | 9       | 327   | 20    | 0.48   |
| Fujitsu   | MHY2080BH          | 80 GB  | 6       | 471   | 174   | 0.48   |
| WDC       | WD20NMVW-11AV3S4   | 2 TB   | 4       | 830   | 257   | 0.48   |
| Apple     | HDD TOSHIBA MK5... | 500 GB | 6       | 256   | 69    | 0.48   |
| WDC       | WD600UE-22KVT0     | 64 GB  | 2       | 271   | 2     | 0.48   |
| Toshiba   | MK4058GSX          | 400 GB | 6       | 787   | 9     | 0.48   |
| WDC       | WD2500JD-40HBC0    | 250 GB | 1       | 1391  | 7     | 0.48   |
| WDC       | WD10SPCX-16HWST0   | 1 TB   | 1       | 173   | 0     | 0.48   |
| Fujitsu   | MHZ2080BH G1       | 80 GB  | 4       | 173   | 0     | 0.48   |
| Hitachi   | HTS543232A7A384    | 320 GB | 244     | 358   | 313   | 0.48   |
| WDC       | WD1600AAJS-75B4A0  | 160 GB | 1       | 1560  | 8     | 0.47   |
| HGST      | HTS541075A9E680    | 752 GB | 66      | 387   | 620   | 0.47   |
| WDC       | WD5000LPCX-75VHAT0 | 500 GB | 18      | 173   | 0     | 0.47   |
| WDC       | WD2001FASS-00U0B0  | 2 TB   | 3       | 1465  | 419   | 0.47   |
| Toshiba   | MQ01ABD050         | 500 GB | 192     | 352   | 235   | 0.47   |
| Toshiba   | MK1629GSG          | 160 GB | 4       | 372   | 26    | 0.47   |
| Hitachi   | HTS543225L9A300    | 250 GB | 49      | 538   | 251   | 0.47   |
| WDC       | WD10SPZX-22Z10T0   | 1 TB   | 21      | 174   | 2     | 0.47   |
| HGST      | HTS545050A7E380    | 500 GB | 221     | 386   | 286   | 0.47   |
| WDC       | WD1600BEVT-88ZCT0  | 160 GB | 2       | 171   | 0     | 0.47   |
| HGST      | HUS726040ALE610    | 4 TB   | 1       | 857   | 4     | 0.47   |
| Toshiba   | MK1246GSX          | 120 GB | 19      | 474   | 72    | 0.47   |
| Seagate   | ST500LX012-1LM1... | 500 GB | 2       | 349   | 240   | 0.47   |
| Seagate   | ST9160827AS        | 160 GB | 39      | 477   | 333   | 0.47   |
| WDC       | WD10SDZM-59ZKVS0   | 1 TB   | 2       | 170   | 0     | 0.47   |
| Toshiba   | MK6037GSX          | 64 GB  | 2       | 277   | 14    | 0.47   |
| Hitachi   | HDS722525VLAT80    | 250 GB | 2       | 2632  | 8     | 0.47   |
| Samsung   | HD252KJ            | 250 GB | 12      | 771   | 432   | 0.47   |
| WDC       | WD20SPZX-00UA7T0   | 2 TB   | 2       | 169   | 0     | 0.47   |
| WDC       | WD5000AVDS-73U7B1  | 500 GB | 4       | 253   | 4     | 0.46   |
| WDC       | WD3200BJKT-00F4T0  | 320 GB | 1       | 169   | 0     | 0.46   |
| WDC       | WD5000LPCX-21VHAT0 | 500 GB | 81      | 178   | 1     | 0.46   |
| WDC       | WD2500BPVT-22ZEST0 | 250 GB | 20      | 207   | 3     | 0.46   |
| Seagate   | ST3250312CS        | 250 GB | 15      | 393   | 170   | 0.46   |
| WDC       | WD7500BPVX-75JC3T0 | 752 GB | 4       | 482   | 3     | 0.46   |
| HGST      | HUS726T4TALA6L4    | 4 TB   | 9       | 168   | 0     | 0.46   |
| Samsung   | HD120IJ            | 120 GB | 25      | 824   | 402   | 0.46   |
| Toshiba   | MK6459GSX          | 640 GB | 7       | 460   | 495   | 0.46   |
| WDC       | WD10SPZX-24Z10T0   | 1 TB   | 45      | 196   | 1     | 0.46   |
| WDC       | WD40EZRZ-22GXCB0   | 4 TB   | 30      | 168   | 0     | 0.46   |
| Seagate   | ST12000DM0007-2... | 12 TB  | 4       | 175   | 1     | 0.46   |
| Seagate   | ST3400832A         | 400 GB | 1       | 2185  | 12    | 0.46   |
| Toshiba   | MQ04ABF100V -63    | 1 TB   | 1       | 167   | 0     | 0.46   |
| Seagate   | ST980310AS         | 80 GB  | 2       | 246   | 1     | 0.46   |
| Toshiba   | MK2576GSX          | 250 GB | 7       | 278   | 2     | 0.46   |
| Seagate   | ST940815A          | 40 GB  | 1       | 167   | 0     | 0.46   |
| Toshiba   | MQ01ABF050         | 500 GB | 529     | 232   | 93    | 0.46   |
| Seagate   | ST2000NM0011       | 2 TB   | 4       | 826   | 15    | 0.46   |
| Hitachi   | HTS541612J9SA00 3H | 120 GB | 2       | 558   | 93    | 0.46   |
| WDC       | WD5000MPCK-60AWHT0 | 500 GB | 1       | 166   | 0     | 0.46   |
| Seagate   | ST3250820NS        | 250 GB | 2       | 695   | 1050  | 0.46   |
| WDC       | WD3200LPVT-00FMCT0 | 320 GB | 3       | 476   | 3     | 0.46   |
| WDC       | WD20EARS-00J99B0   | 2 TB   | 4       | 486   | 731   | 0.45   |
| HGST      | HTS545050A7E660    | 500 GB | 19      | 320   | 80    | 0.45   |
| Seagate   | ST9100824A         | 100 GB | 1       | 165   | 0     | 0.45   |
| Seagate   | ST500LT032-1E9142  | 500 GB | 7       | 206   | 3     | 0.45   |
| WDC       | WD800BEVE-00A0HT0  | 80 GB  | 1       | 165   | 0     | 0.45   |
| Hitachi   | HTS545025B9SA02    | 250 GB | 19      | 297   | 221   | 0.45   |
| WDC       | WD2500BEVT-75A23T0 | 250 GB | 15      | 432   | 61    | 0.45   |
| WDC       | WD10EARX-00PASB0   | 1 TB   | 6       | 566   | 13    | 0.45   |
| Samsung   | HN-M750MBB         | 752 GB | 9       | 308   | 7     | 0.45   |
| WDC       | WD5000BPVT-60HXZT3 | 500 GB | 14      | 452   | 112   | 0.45   |
| Samsung   | SP1213C            | 120 GB | 10      | 782   | 27    | 0.45   |
| Samsung   | HD155UI            | 1.5 TB | 3       | 1164  | 599   | 0.45   |
| WDC       | WD5000LPLX-60ZNTT1 | 500 GB | 22      | 221   | 33    | 0.45   |
| Seagate   | ST2000NE001-2M5101 | 2 TB   | 3       | 163   | 0     | 0.45   |
| IBM/Hi... | IC35L120AVV207-1   | 128 GB | 2       | 496   | 9     | 0.45   |
| WDC       | WD2500LPCX-24C6HT0 | 250 GB | 45      | 209   | 72    | 0.45   |
| WDC       | WD140EMFZ-11A0WA0  | 14 TB  | 12      | 190   | 1     | 0.45   |
| Samsung   | HM250JI            | 250 GB | 9       | 407   | 174   | 0.45   |
| Fujitsu   | MHZ2250BH G2       | 250 GB | 20      | 544   | 643   | 0.45   |
| WDC       | WD6400AADS-00M2B0  | 640 GB | 13      | 802   | 18    | 0.45   |
| WDC       | WD10SPZX-17Z10T0   | 1 TB   | 8       | 198   | 55    | 0.45   |
| Seagate   | ST3400820AS        | 400 GB | 2       | 961   | 503   | 0.44   |
| WDC       | WD6400BEVT-60A0RT0 | 640 GB | 5       | 311   | 45    | 0.44   |
| Toshiba   | HDWL110            | 1 TB   | 15      | 182   | 1     | 0.44   |
| Seagate   | ST920217AS         | 20 GB  | 1       | 162   | 0     | 0.44   |
| Samsung   | SP2504C            | 250 GB | 60      | 1001  | 703   | 0.44   |
| Toshiba   | MK8007GAH          | 80 GB  | 2       | 210   | 7     | 0.44   |
| Seagate   | ST16000NM001G-2... | 16 TB  | 37      | 161   | 0     | 0.44   |
| Hitachi   | HDS722512VLAT20    | 128 GB | 1       | 805   | 4     | 0.44   |
| WDC       | WD3200JD-60KLB0    | 320 GB | 1       | 965   | 5     | 0.44   |
| WDC       | WD10SPCX-80HWST0   | 1 TB   | 1       | 160   | 0     | 0.44   |
| Hitachi   | HTS725016A9A362    | 160 GB | 2       | 290   | 1     | 0.44   |
| WDC       | WD1005FBYZ-01YCBB3 | 1 TB   | 3       | 160   | 0     | 0.44   |
| WDC       | WD3200BPVT-80ZEST0 | 320 GB | 39      | 345   | 80    | 0.44   |
| Seagate   | ST9320325AS        | 320 GB | 319     | 485   | 431   | 0.44   |
| Fujitsu   | MHZ2250BS G2       | 250 GB | 1       | 159   | 0     | 0.44   |
| Seagate   | ST1000LM048-2E7172 | 1 TB   | 178     | 202   | 97    | 0.44   |
| WDC       | WD6400BEVT-80A0RT1 | 640 GB | 2       | 479   | 13    | 0.44   |
| WDC       | WD400BB-23FJA0     | 40 GB  | 1       | 796   | 4     | 0.44   |
| Toshiba   | MG06ACA10TE        | 10 TB  | 4       | 159   | 0     | 0.44   |
| WDC       | WD40NDZW-11MR8S1   | 4 TB   | 17      | 163   | 43    | 0.43   |
| WDC       | WD1600AAJB-00J3A0  | 160 GB | 17      | 521   | 126   | 0.43   |
| WDC       | WD10PURX-78E5EY0   | 1 TB   | 1       | 157   | 0     | 0.43   |
| WDC       | WD8003FFBX-68B9AN0 | 8 TB   | 2       | 157   | 0     | 0.43   |
| Seagate   | ST980811AS         | 80 GB  | 36      | 434   | 379   | 0.43   |
| Seagate   | ST500LT012-1DG142  | 500 GB | 596     | 257   | 99    | 0.43   |
| WDC       | WD3200BEVT-26A23T0 | 320 GB | 3       | 274   | 73    | 0.43   |
| WDC       | WD-WD3200BVVT-6... | 320 GB | 1       | 157   | 0     | 0.43   |
| WDC       | WD1600JD-00HBB0    | 160 GB | 7       | 541   | 15    | 0.43   |
| Seagate   | ST910021AS         | 100 GB | 7       | 582   | 469   | 0.43   |
| WDC       | WD1600BEVT-80A23T0 | 160 GB | 25      | 229   | 102   | 0.43   |
| WDC       | WD5000M22K-24Z1... | 500 GB | 2       | 596   | 10    | 0.43   |
| Toshiba   | MK3276GSXN         | 320 GB | 1       | 156   | 0     | 0.43   |
| Fujitsu   | MJA2500BH G1       | 500 GB | 2       | 381   | 4     | 0.43   |
| Seagate   | ST1000LM035-1RK172 | 1 TB   | 745     | 205   | 124   | 0.43   |
| Seagate   | ST3000VX010-2H916L | 3 TB   | 3       | 156   | 0     | 0.43   |
| Toshiba   | MK5059GSXP         | 500 GB | 44      | 388   | 311   | 0.43   |
| Toshiba   | MK1655GSX          | 160 GB | 19      | 359   | 50    | 0.43   |
| WDC       | WD2500AAKS-60B3A0  | 250 GB | 1       | 155   | 0     | 0.43   |
| Seagate   | ST500LX025-1U717D  | 500 GB | 11      | 162   | 36    | 0.43   |
| WDC       | WD5000BMVW-11AJGS4 | 500 GB | 7       | 157   | 81    | 0.43   |
| Samsung   | SP1614C            | 160 GB | 11      | 454   | 11    | 0.43   |
| WDC       | WD1200JD-55HBB0    | 120 GB | 1       | 923   | 5     | 0.42   |
| Samsung   | SV0412H            | 40 GB  | 6       | 1055  | 104   | 0.42   |
| Hitachi   | HTS545050A7E380    | 500 GB | 165     | 377   | 256   | 0.42   |
| MediaMax  | WL1000GSA6472B     | 1 TB   | 1       | 1379  | 8     | 0.42   |
| Toshiba   | MQ03ABB300         | 3 TB   | 2       | 152   | 0     | 0.42   |
| Toshiba   | MK2565GSXN         | 250 GB | 6       | 388   | 7     | 0.42   |
| WDC       | WD1200BEVS-60UST0  | 120 GB | 13      | 456   | 290   | 0.42   |
| Hitachi   | HTS545032B9A302    | 320 GB | 12      | 314   | 227   | 0.42   |
| WDC       | WD5000AAKX-083CA0  | 500 GB | 2       | 174   | 2     | 0.42   |
| WDC       | WD800BD-22LRA0     | 80 GB  | 1       | 152   | 0     | 0.42   |
| WDC       | WD3200BPVT-60JJ5T0 | 320 GB | 11      | 344   | 108   | 0.42   |
| Seagate   | ST3500412AS        | 500 GB | 27      | 793   | 472   | 0.42   |
| WDC       | WD10EARX-00NYB0    | 1 TB   | 1       | 151   | 0     | 0.42   |
| Seagate   | ST2000DM008-2FR102 | 2 TB   | 373     | 163   | 37    | 0.42   |
| Samsung   | HN-M320MBB         | 320 GB | 5       | 347   | 7     | 0.41   |
| HGST      | HTS541050A9E680    | 500 GB | 6       | 151   | 0     | 0.41   |
| WDC       | WD5000LPLX-00ZNTT0 | 500 GB | 62      | 157   | 1     | 0.41   |
| WDC       | WD3200AAKS-22L6A0  | 320 GB | 5       | 534   | 5     | 0.41   |
| WDC       | WD10SPZX-21Z10T0   | 1 TB   | 144     | 159   | 11    | 0.41   |
| Seagate   | ST500LM021-1KJ152  | 500 GB | 133     | 344   | 389   | 0.41   |
| WDC       | WD10SPCX-60HWST0   | 1 TB   | 2       | 558   | 2     | 0.41   |
| WDC       | WD4003FRYZ-01F0DB0 | 4 TB   | 2       | 150   | 0     | 0.41   |
| Seagate   | ST9160821A         | 160 GB | 5       | 414   | 15    | 0.41   |
| Hitachi   | HTS541010A9E680    | 1 TB   | 21      | 511   | 793   | 0.41   |
| WDC       | WD10JPLX-00MBPT1   | 1 TB   | 2       | 149   | 0     | 0.41   |
| Hitachi   | HDS721010KLA33R... | 1 TB   | 1       | 3734  | 24    | 0.41   |
| Seagate   | ST3200822A         | 200 GB | 6       | 1408  | 10    | 0.41   |
| Samsung   | SP1634N            | 160 GB | 1       | 298   | 1     | 0.41   |
| WDC       | WD20EARS-60MVWB0   | 2 TB   | 5       | 1043  | 942   | 0.41   |
| Toshiba   | MK8037GSX          | 80 GB  | 21      | 417   | 126   | 0.41   |
| Hitachi   | HTS723225L9SA62    | 250 GB | 1       | 595   | 3     | 0.41   |
| Toshiba   | MK2035GSS          | 200 GB | 20      | 501   | 33    | 0.41   |
| Toshiba   | MD03ACA400V        | 4 TB   | 1       | 1037  | 6     | 0.41   |
| Fujitsu   | MHV2060AT          | 64 GB  | 2       | 528   | 4     | 0.41   |
| Seagate   | ST12000NM0008-2... | 12 TB  | 2       | 148   | 0     | 0.41   |
| WDC       | WD1200JS-22NCB1    | 120 GB | 1       | 1184  | 7     | 0.41   |
| WDC       | WD2500BEVT-80A23T0 | 250 GB | 25      | 324   | 50    | 0.40   |
| Toshiba   | MK2565GSX          | 250 GB | 31      | 431   | 160   | 0.40   |
| WDC       | WD30PURZ-85GU6Y0   | 3 TB   | 3       | 147   | 0     | 0.40   |
| WDC       | WD10EZRX-00A3KB0   | 1 TB   | 2       | 147   | 0     | 0.40   |
| Hitachi   | HDS722525VLSA80    | 250 GB | 2       | 370   | 17    | 0.40   |
| Seagate   | ST750LM030-1KKG62  | 752 GB | 2       | 146   | 0     | 0.40   |
| WDC       | WD2500BEVT-00A0RT1 | 245 GB | 1       | 146   | 0     | 0.40   |
| Seagate   | ST1000NM0008-2F... | 1 TB   | 5       | 146   | 0     | 0.40   |
| WDC       | WD2500BPVT-75JJ5T0 | 250 GB | 7       | 347   | 3     | 0.40   |
| MediaMax  | WL320GLSA854G      | 320 GB | 1       | 146   | 0     | 0.40   |
| Hitachi   | HTS545050KTA300    | 500 GB | 6       | 520   | 5     | 0.40   |
| WDC       | WD5000AVVS-63H0B1  | 500 GB | 6       | 823   | 6     | 0.40   |
| HGST      | HUS726T6TALE6L4    | 6 TB   | 5       | 145   | 0     | 0.40   |
| Lenovo    | WD1004FBYZ-23YC... | 1 TB   | 2       | 145   | 0     | 0.40   |
| WDC       | WD60EMAZ-11LW3B0   | 6 TB   | 3       | 145   | 0     | 0.40   |
| Fujitsu   | MHV2060BHPL        | 64 GB  | 1       | 144   | 0     | 0.40   |
| WDC       | WD10SPCX-00HWST0   | 1 TB   | 2       | 144   | 0     | 0.40   |
| Toshiba   | MK5076GSX -63      | 500 GB | 2       | 144   | 0     | 0.40   |
| Toshiba   | MG06ACA800E        | 8 TB   | 6       | 144   | 0     | 0.40   |
| Hitachi   | HTS541040G9AT00    | 40 GB  | 8       | 383   | 9     | 0.39   |
| Samsung   | SP0842N            | 80 GB  | 13      | 566   | 529   | 0.39   |
| MARSHAL   | MAL2500HSA-T54L    | 500 GB | 1       | 143   | 0     | 0.39   |
| WDC       | WD15NMVW-11AV3S2   | 1.5 TB | 4       | 233   | 6     | 0.39   |
| WDC       | WD3200AAJS-55VWA0  | 320 GB | 1       | 1006  | 6     | 0.39   |
| Seagate   | ST96023AS          | 64 GB  | 2       | 395   | 5     | 0.39   |
| WDC       | WD30EZRS-11J99B1   | 3 TB   | 3       | 832   | 230   | 0.39   |
| WDC       | WD2500BPVT-24JJ5T0 | 250 GB | 5       | 143   | 0     | 0.39   |
| HP        | VB0160EAVEQ        | 160 GB | 1       | 429   | 2     | 0.39   |
| WDC       | WD120EMFZ-11A6JA0  | 12 TB  | 14      | 143   | 0     | 0.39   |
| WDC       | WD5000BEVT-80A0RT1 | 500 GB | 3       | 308   | 5     | 0.39   |
| HP        | MB2000GCWLT        | 2 TB   | 2       | 1500  | 505   | 0.39   |
| WDC       | WD3200AAKX-32ERMA0 | 320 GB | 1       | 142   | 0     | 0.39   |
| Samsung   | HN-M101MBB         | 1 TB   | 22      | 365   | 251   | 0.39   |
| Toshiba   | MK7559GSXF         | 752 GB | 8       | 366   | 299   | 0.39   |
| Hitachi   | HTS541212H9AT00    | 120 GB | 3       | 438   | 5     | 0.39   |
| WDC       | WD3200LPVX-08V0TT5 | 320 GB | 3       | 141   | 0     | 0.39   |
| Seagate   | ST1000NM000A       | 1 TB   | 3       | 141   | 0     | 0.39   |
| WDC       | WD40EFAX-68JH4N0   | 4 TB   | 14      | 177   | 1     | 0.39   |
| Seagate   | ST2000DM005-2CW102 | 2 TB   | 16      | 141   | 0     | 0.39   |
| WDC       | WD7500KMVV-11TK7S1 | 752 GB | 1       | 141   | 0     | 0.39   |
| IBM       | DTLA-305020        | 20 GB  | 2       | 1494  | 37    | 0.39   |
| WDC       | WD7500BPVT-00HXZT0 | 752 GB | 1       | 141   | 0     | 0.39   |
| WDC       | WD800AAJS-00M0A0   | 80 GB  | 1       | 141   | 0     | 0.39   |
| Toshiba   | MK2555GSX          | 250 GB | 44      | 489   | 87    | 0.39   |
| WDC       | WD2500AAJB-57WGA0  | 250 GB | 1       | 140   | 0     | 0.38   |
| WDC       | WD5000LPCX-22VHAT1 | 500 GB | 16      | 140   | 0     | 0.38   |
| WDC       | WD800BB-00HEA0     | 80 GB  | 1       | 840   | 5     | 0.38   |
| WDC       | WD2500AAJS-07B4A0  | 250 GB | 2       | 1695  | 198   | 0.38   |
| Toshiba   | MK2546GSX          | 250 GB | 14      | 514   | 35    | 0.38   |
| Seagate   | ST9160301AS        | 160 GB | 9       | 186   | 224   | 0.38   |
| WDC       | WD400EB-11CPF0     | 40 GB  | 2       | 1019  | 31    | 0.38   |
| Fujitsu   | MHZ2080BJ FFS G2   | 80 GB  | 1       | 279   | 1     | 0.38   |
| Seagate   | ST33000650NS       | 3 TB   | 4       | 201   | 26    | 0.38   |
| Seagate   | ST340810A          | 40 GB  | 13      | 564   | 29    | 0.38   |
| Seagate   | ST500LM030-2E717D  | 500 GB | 52      | 150   | 47    | 0.38   |
| Hitachi   | HTS723232L9SA60    | 320 GB | 3       | 424   | 29    | 0.38   |
| WDC       | WD2500JS-60MHB1    | 250 GB | 2       | 331   | 8     | 0.38   |
| Hitachi   | HUA722010CLA330... | 1 TB   | 1       | 2081  | 14    | 0.38   |
| WDC       | WD60PURZ-85ZUFY1   | 6 TB   | 6       | 138   | 0     | 0.38   |
| HP        | GB0750C8047        | 752 GB | 1       | 138   | 0     | 0.38   |
| Samsung   | SP0822N            | 80 GB  | 10      | 138   | 1     | 0.38   |
| WDC       | WD10EZEX-07WN4A0   | 1 TB   | 7       | 182   | 1     | 0.38   |
| Seagate   | ST3160815SV        | 160 GB | 6       | 704   | 1035  | 0.38   |
| WDC       | WD5000BPVT-08HXZT1 | 500 GB | 3       | 549   | 2     | 0.38   |
| WDC       | WD120EFAX-68UNTN0  | 12 TB  | 3       | 136   | 0     | 0.37   |
| WDC       | WD5000LPVX-00V0TT0 | 500 GB | 28      | 180   | 84    | 0.37   |
| Hitachi   | HCT721050SLA380    | 500 GB | 1       | 136   | 0     | 0.37   |
| WDC       | WD5000LPZX-22Z10T0 | 500 GB | 1       | 135   | 0     | 0.37   |
| Seagate   | ST3160812AS Q      | 160 GB | 2       | 658   | 240   | 0.37   |
| WDC       | WD800JD-00JNA0     | 80 GB  | 2       | 809   | 5     | 0.37   |
| Seagate   | ST9160821AS        | 160 GB | 80      | 445   | 557   | 0.37   |
| Hitachi   | HTS541060G9AT00    | 64 GB  | 9       | 439   | 13    | 0.37   |
| WDC       | WD1600BEVT-75A23T0 | 160 GB | 10      | 196   | 1     | 0.37   |
| WDC       | WD5000LPCX-24VHAT0 | 500 GB | 103     | 139   | 11    | 0.37   |
| WDC       | WD10JUCT-63J6SY0   | 1 TB   | 6       | 342   | 183   | 0.37   |
| WDC       | WD3201ABYS-01B9A0  | 320 GB | 2       | 926   | 278   | 0.37   |
| Toshiba   | MK8009GAH          | 80 GB  | 4       | 562   | 26    | 0.37   |
| WDC       | WD7500AACS-00ZJB0  | 752 GB | 2       | 1621  | 507   | 0.37   |
| Seagate   | ST9120823ASG       | 120 GB | 2       | 228   | 1     | 0.37   |
| HGST      | HDS5C4040ALE630    | 4 TB   | 2       | 133   | 0     | 0.37   |
| Seagate   | ST3120811AS        | 120 GB | 16      | 556   | 389   | 0.37   |
| Toshiba   | MK8025GAS          | 80 GB  | 3       | 140   | 20    | 0.36   |
| Samsung   | SP2514N            | 250 GB | 11      | 684   | 490   | 0.36   |
| WDC       | WD50NDZW-11MR8S1   | 5 TB   | 12      | 133   | 0     | 0.36   |
| WDC       | WD10SPZX-75Z10T2   | 1 TB   | 40      | 135   | 1     | 0.36   |
| Hitachi   | HTS543232L9A300    | 320 GB | 34      | 608   | 425   | 0.36   |
| Toshiba   | MK5055GSX          | 500 GB | 24      | 494   | 193   | 0.36   |
| HP        | MB1000CBZQE        | 1 TB   | 1       | 1450  | 10    | 0.36   |
| WDC       | WD3200BEVT-26ZCT0  | 320 GB | 6       | 250   | 17    | 0.36   |
| WDC       | WD10SPSX-08A6W     | 1 TB   | 4       | 131   | 0     | 0.36   |
| WDC       | RFT030VQHF-KRM5P7  | 3 TB   | 2       | 131   | 0     | 0.36   |
| WDC       | WD10SPZX-80Z10T1   | 1 TB   | 1       | 130   | 0     | 0.36   |
| Hitachi   | HTS542512K9SA00    | 120 GB | 78      | 451   | 123   | 0.36   |
| WDC       | WD5000AZLX-35K2TA0 | 500 GB | 2       | 130   | 0     | 0.36   |
| WDC       | WD15EADS-22P8B0    | 1.5 TB | 3       | 376   | 341   | 0.36   |
| WDC       | WD10SPCX-24HWST0   | 1 TB   | 2       | 1167  | 187   | 0.36   |
| WDC       | WD40NMZW-59A8NS1   | 4 TB   | 3       | 130   | 0     | 0.36   |
| Seagate   | ST9120822A         | 120 GB | 2       | 273   | 53    | 0.36   |
| Seagate   | ST4000NM002A-2H... | 4 TB   | 1       | 129   | 0     | 0.36   |
| WDC       | WD20SMZW-11JW8S0   | 2 TB   | 9       | 129   | 0     | 0.36   |
| Seagate   | ST9500325AS        | 500 GB | 533     | 495   | 532   | 0.35   |
| Toshiba   | MK3265GSXF         | 320 GB | 5       | 276   | 20    | 0.35   |
| Maxtor    | 6G160E0            | 160 GB | 9       | 363   | 147   | 0.35   |
| Samsung   | HM121HI            | 120 GB | 13      | 520   | 1242  | 0.35   |
| WDC       | WD10EADS-98M2B0    | 1 TB   | 1       | 899   | 6     | 0.35   |
| WDC       | WD800JD-22LSA1     | 80 GB  | 4       | 485   | 174   | 0.35   |
| WDC       | WD5000LPCX-08VHA   | 500 GB | 6       | 128   | 0     | 0.35   |
| WDC       | WD3200AVVS-63L2B0  | 320 GB | 12      | 456   | 85    | 0.35   |
| IBM/Hi... | IC25N020ATMR04-0   | 20 GB  | 2       | 515   | 8     | 0.35   |
| Seagate   | ST3500410AS        | 500 GB | 31      | 977   | 357   | 0.35   |
| Fujitsu   | MHT2040AH PL       | 40 GB  | 2       | 766   | 5     | 0.35   |
| Seagate   | ST9250315ASG       | 250 GB | 3       | 166   | 6     | 0.35   |
| HPE       | MM1000EBKAF        | 1 TB   | 2       | 127   | 0     | 0.35   |
| Seagate   | ST320LT007-9ZV142  | 320 GB | 65      | 479   | 649   | 0.35   |
| WDC       | WD1600AAJS-56M0A0  | 160 GB | 2       | 469   | 4     | 0.35   |
| China     | OOS250G            | 250 GB | 1       | 126   | 0     | 0.35   |
| WDC       | WD5000BPVT-55A1YT0 | 500 GB | 1       | 126   | 0     | 0.35   |
| Seagate   | ST9320320AS        | 320 GB | 31      | 703   | 183   | 0.35   |
| MaxDig... | MD1TBLSSHD         | 1 TB   | 2       | 255   | 4     | 0.35   |
| Seagate   | ST3500830SCE       | 500 GB | 1       | 126   | 0     | 0.35   |
| WDC       | WD20SMZW-11YFCS0   | 2 TB   | 5       | 126   | 0     | 0.35   |
| ExcelStor | J8080S             | 82 GB  | 1       | 2405  | 18    | 0.35   |
| Toshiba   | HDWM110            | 1 TB   | 3       | 126   | 0     | 0.35   |
| Samsung   | HM250HJ            | 250 GB | 3       | 331   | 14    | 0.35   |
| Hitachi   | HTS545025A7E380    | 250 GB | 3       | 126   | 0     | 0.35   |
| WDC       | WD5000LUCT-61C26Y0 | 500 GB | 1       | 1003  | 7     | 0.34   |
| Toshiba   | HDWR180            | 8 TB   | 3       | 125   | 0     | 0.34   |
| Toshiba   | MK1216GSG          | 120 GB | 3       | 272   | 4     | 0.34   |
| Toshiba   | MK4025GAS          | 40 GB  | 3       | 309   | 12    | 0.34   |
| Toshiba   | MQ01ABD064         | 640 GB | 1       | 124   | 0     | 0.34   |
| WDC       | WD40NDZW-11A8JS1   | 4 TB   | 11      | 124   | 0     | 0.34   |
| Hitachi   | HTS541612J9SA00    | 120 GB | 76      | 569   | 93    | 0.34   |
| WDC       | WD3200AAKS-00C9A0  | 320 GB | 3       | 1080  | 8     | 0.34   |
| Seagate   | ST500LM000-SSHD... | 500 GB | 49      | 320   | 346   | 0.34   |
| Toshiba   | DT01ACA200V        | 2 TB   | 1       | 124   | 0     | 0.34   |
| Seagate   | ST1500DM003-9YN16G | 1.5 TB | 18      | 462   | 441   | 0.34   |
| WDC       | WD1600HLHX-60JJPV1 | 160 GB | 1       | 617   | 4     | 0.34   |
| Toshiba   | MK6461GSYG         | 640 GB | 1       | 1971  | 15    | 0.34   |
| WDC       | WD8000AARS-00Y5B1  | 800 GB | 3       | 1740  | 14    | 0.34   |
| Seagate   | STM3160318AS       | 160 GB | 1       | 245   | 1     | 0.34   |
| Samsung   | HM321HX            | 320 GB | 3       | 176   | 3     | 0.34   |
| WDC       | WD10SPZX-22Z10T1   | 1 TB   | 31      | 122   | 0     | 0.34   |
| WDC       | WD1001FAES-60Z2A0  | 1 TB   | 1       | 122   | 0     | 0.33   |
| Toshiba   | MG05ACA800E        | 8 TB   | 1       | 121   | 0     | 0.33   |
| WDC       | WD2500JS-63MHB5    | 250 GB | 3       | 1058  | 96    | 0.33   |
| Samsung   | HD080HJ-P          | 80 GB  | 14      | 806   | 362   | 0.33   |
| Hitachi   | HDT722525DLAT80    | 250 GB | 4       | 819   | 11    | 0.33   |
| Seagate   | ST9250315AS        | 250 GB | 232     | 487   | 449   | 0.33   |
| Samsung   | HA200JC            | 200 GB | 1       | 120   | 0     | 0.33   |
| WDC       | WD40NPZZ-00A9JT0   | 4 TB   | 2       | 120   | 0     | 0.33   |
| WDC       | WD2500BEVE-00A0HT0 | 250 GB | 2       | 120   | 0     | 0.33   |
| Lenovo    | ST1000NM0055 91... | 1 TB   | 2       | 120   | 0     | 0.33   |
| MediaMax  | WL6000GSA6457      | 6 TB   | 2       | 438   | 686   | 0.33   |
| Toshiba   | MG06ACA600E        | 6 TB   | 2       | 119   | 0     | 0.33   |
| Seagate   | ST9100827AS        | 100 GB | 1       | 838   | 6     | 0.33   |
| WDC       | WD5001AALS-00J7B1  | 500 GB | 1       | 1077  | 8     | 0.33   |
| WDC       | WD120EDAZ-11F3RA0  | 12 TB  | 9       | 119   | 0     | 0.33   |
| Seagate   | ST960821A          | 64 GB  | 1       | 358   | 2     | 0.33   |
| Seagate   | ST1000LM025 HN-... | 1 TB   | 43      | 138   | 25    | 0.33   |
| Hitachi   | HTS541680J9SA00    | 80 GB  | 67      | 485   | 76    | 0.33   |
| Samsung   | HD103UI            | 1 TB   | 8       | 774   | 443   | 0.32   |
| Toshiba   | HDWD240            | 4 TB   | 17      | 118   | 0     | 0.32   |
| WDC       | WD2500AVVS-61L2B0  | 250 GB | 2       | 1141  | 6     | 0.32   |
| MediaMax  | WL1500GSA6472B     | 1.5 TB | 2       | 117   | 0     | 0.32   |
| WDC       | WD60EFAX-68JH4N1   | 6 TB   | 2       | 117   | 0     | 0.32   |
| Seagate   | ST500LM014 HN-M... | 500 GB | 13      | 176   | 5     | 0.32   |
| Fujitsu   | MHX2250BT          | 250 GB | 5       | 317   | 6     | 0.32   |
| MaxDig... | MDT MD5000AAKS-... | 500 GB | 1       | 116   | 0     | 0.32   |
| Toshiba   | MQ04ABF100         | 1 TB   | 366     | 129   | 36    | 0.32   |
| WDC       | 500GB              | 500 GB | 1       | 1047  | 8     | 0.32   |
| WDC       | WD30NMVW-11C3NS2   | 3 TB   | 4       | 805   | 342   | 0.32   |
| WDC       | WD7500BPVT-55HXZT4 | 752 GB | 4       | 229   | 16    | 0.32   |
| Toshiba   | MQ01ABF050M        | 500 GB | 13      | 164   | 78    | 0.32   |
| WDC       | WD4000LPCX-24C6HT0 | 400 GB | 1       | 115   | 0     | 0.32   |
| WDC       | WD3200BEVT-60ZCT1  | 320 GB | 12      | 446   | 254   | 0.32   |
| WDC       | WD40NMZW-59LG6S1   | 4 TB   | 1       | 115   | 0     | 0.32   |
| Seagate   | ST18000NM000J-2... | 18 TB  | 8       | 115   | 0     | 0.32   |
| WDC       | WD1600BEVT-60ZCT0  | 160 GB | 8       | 267   | 262   | 0.31   |
| WDC       | WD100EJRX-89SYHY0  | 10 TB  | 1       | 114   | 0     | 0.31   |
| WDC       | WD3200BEVT-00A23T0 | 320 GB | 5       | 175   | 9     | 0.31   |
| Hitachi   | HTS725032A9A364    | 320 GB | 36      | 532   | 771   | 0.31   |
| Fujitsu   | MHV2060BH PL       | 64 GB  | 8       | 113   | 3     | 0.31   |
| WDC       | WD3200BEVT-00ZAT0  | 320 GB | 3       | 198   | 9     | 0.31   |
| WDC       | WD5000AADS-56S9B1  | 500 GB | 7       | 628   | 7     | 0.31   |
| Seagate   | ST9100824AS        | 100 GB | 5       | 351   | 7     | 0.31   |
| HGST      | HTS545050A7E680    | 500 GB | 360     | 276   | 428   | 0.31   |
| Seagate   | ST9100823A         | 96 GB  | 1       | 1007  | 8     | 0.31   |
| Toshiba   | MK3265GSX          | 320 GB | 73      | 574   | 223   | 0.31   |
| Samsung   | HM500LI            | 500 GB | 2       | 222   | 1     | 0.31   |
| WDC       | WD20SMZW-11JW8S1   | 2 TB   | 1       | 111   | 0     | 0.30   |
| Magnet... | MD03200-AVDW-RO    | 320 GB | 2       | 110   | 0     | 0.30   |
| WDC       | WD8004FRYZ-01VAEB0 | 8 TB   | 5       | 110   | 0     | 0.30   |
| Seagate   | ST8000AS0003-2H... | 8 TB   | 5       | 110   | 0     | 0.30   |
| WDC       | WD400BD-75JMA0     | 40 GB  | 1       | 663   | 5     | 0.30   |
| WDC       | WD400JB-00FMA0     | 40 GB  | 2       | 656   | 8     | 0.30   |
| Samsung   | HM080GI            | 80 GB  | 1       | 220   | 1     | 0.30   |
| WDC       | WD7500BPVT-00HXZT3 | 752 GB | 8       | 512   | 11    | 0.30   |
| Toshiba   | MK3252GSX          | 320 GB | 35      | 571   | 235   | 0.30   |
| Fujitsu   | MHW2020BH          | 20 GB  | 2       | 109   | 0     | 0.30   |
| WDC       | WD20EZAZ-00GGJB0   | 2 TB   | 46      | 109   | 0     | 0.30   |
| Toshiba   | MQ04ABD200         | 2 TB   | 8       | 109   | 0     | 0.30   |
| Seagate   | ST1000LM049-2GH172 | 1 TB   | 170     | 138   | 68    | 0.30   |
| WDC       | WD10SPZX-00Z10T0   | 1 TB   | 32      | 109   | 0     | 0.30   |
| Toshiba   | DT02ABA400         | 4 TB   | 1       | 109   | 0     | 0.30   |
| Hitachi   | HDT721050SLA360    | 500 GB | 4       | 898   | 48    | 0.30   |
| WDC       | WD3000FYYZ-01UL1B0 | 3 TB   | 2       | 109   | 0     | 0.30   |
| WDC       | WD3200BEKT-00V5T0  | 320 GB | 1       | 109   | 0     | 0.30   |
| WDC       | WD3200BPVT-75ZEST0 | 320 GB | 10      | 471   | 13    | 0.30   |
| WDC       | WD5000LPCX-60VHAT0 | 500 GB | 55      | 140   | 6     | 0.30   |
| Hitachi   | HTS541010G9SA00    | 100 GB | 17      | 390   | 81    | 0.30   |
| WDC       | WD5000LPVX-28V0TT0 | 500 GB | 4       | 462   | 4     | 0.30   |
| Samsung   | HM100UX            | 1 TB   | 2       | 186   | 4     | 0.29   |
| Fujitsu   | MHV2040BH PL       | 40 GB  | 1       | 107   | 0     | 0.29   |
| Fujitsu   | MHV2040AT          | 40 GB  | 1       | 107   | 0     | 0.29   |
| WDC       | WD20SPZX-22UA7T0   | 2 TB   | 17      | 107   | 0     | 0.29   |
| WDC       | WD10SPZX-08Z10     | 1 TB   | 41      | 107   | 0     | 0.29   |
| Seagate   | ST4000DM004-2U9104 | 4 TB   | 1       | 107   | 0     | 0.29   |
| Seagate   | ST320LT012-1DG14C  | 320 GB | 30      | 187   | 140   | 0.29   |
| WDC       | WD3200BEVT-88ZCT0  | 320 GB | 1       | 106   | 0     | 0.29   |
| Hitachi   | HTS542520K9SA00    | 200 GB | 4       | 658   | 11    | 0.29   |
| Toshiba   | MK1034GSX          | 100 GB | 5       | 375   | 373   | 0.29   |
| WDC       | WD5000BEVT-00SCST0 | 500 GB | 2       | 246   | 5     | 0.29   |
| WDC       | WD10SPZX-80Z10T2   | 1 TB   | 14      | 106   | 0     | 0.29   |
| China     | TP00250GB          | 250 GB | 1       | 106   | 0     | 0.29   |
| Toshiba   | MK5065GSX          | 500 GB | 34      | 392   | 349   | 0.29   |
| WDC       | WD50EFRX-68MYMN1   | 5 TB   | 3       | 518   | 3     | 0.29   |
| Fujitsu   | MHZ2160BH          | 160 GB | 1       | 105   | 0     | 0.29   |
| Toshiba   | MK3259GSXP         | 320 GB | 63      | 349   | 251   | 0.29   |
| WDC       | WD3200BPVT-11HXZT3 | 320 GB | 1       | 104   | 0     | 0.29   |
| Seagate   | ST9160314AS        | 160 GB | 44      | 314   | 244   | 0.29   |
| WDC       | WD5000LPLX-22ZNTT0 | 500 GB | 10      | 104   | 0     | 0.29   |
| WDC       | WD82PURZ-85TEUY0   | 8 TB   | 7       | 104   | 0     | 0.29   |
| Toshiba   | MK1251GSY          | 120 GB | 1       | 939   | 8     | 0.29   |
| WDC       | WD3200BPVT-35JJ5T0 | 320 GB | 1       | 104   | 0     | 0.29   |
| WDC       | WD40NDZW-11MR8S0   | 4 TB   | 1       | 104   | 0     | 0.29   |
| Seagate   | ST3750330NS        | 752 GB | 6       | 480   | 230   | 0.28   |
| ASMedia   | ASMT106x_ V0Safe   | 320 GB | 1       | 103   | 0     | 0.28   |
| WDC       | WUH721414ALE604    | 14 TB  | 6       | 105   | 3     | 0.28   |
| WDC       | WD5000AAKX-19U6AA0 | 500 GB | 1       | 103   | 0     | 0.28   |
| WDC       | WD161KFGX-68AFPN0  | 16 TB  | 1       | 103   | 0     | 0.28   |
| WDC       | WD1600YS-01SHB0    | 164 GB | 1       | 726   | 6     | 0.28   |
| Hitachi   | HTS722012K9A300    | 120 GB | 3       | 517   | 90    | 0.28   |
| Seagate   | ST320LT020-9YG142  | 320 GB | 160     | 365   | 601   | 0.28   |
| WDC       | WD15NMVW-11EDZS7   | 1.5 TB | 1       | 103   | 0     | 0.28   |
| WDC       | WD5000AAKS-22TMA0  | 500 GB | 1       | 308   | 2     | 0.28   |
| Toshiba   | MQ01ABD050V -63    | 500 GB | 5       | 102   | 0     | 0.28   |
| Seagate   | ST9120817AS        | 120 GB | 10      | 399   | 450   | 0.28   |
| Hitachi   | HTS725050A9A364    | 500 GB | 35      | 563   | 814   | 0.28   |
| Hitachi   | HTS721060G9SA00    | 64 GB  | 3       | 664   | 13    | 0.28   |
| Seagate   | ST1000LX015-1U7... | 1 TB   | 4       | 243   | 855   | 0.28   |
| Toshiba   | MK1252GSX          | 120 GB | 15      | 359   | 61    | 0.28   |
| Toshiba   | MK8046GSX          | 80 GB  | 5       | 513   | 407   | 0.28   |
| WDC       | WD10EZRX-22A3KB0   | 1 TB   | 1       | 101   | 0     | 0.28   |
| Hitachi   | HTS542560K9SA00    | 64 GB  | 3       | 457   | 12    | 0.28   |
| Toshiba   | MK7559GSXP         | 752 GB | 30      | 445   | 547   | 0.28   |
| WDC       | WD20SDRW-11VUUS0   | 2 TB   | 23      | 106   | 45    | 0.28   |
| WDC       | WD10JPVT-00MS8T0   | 1 TB   | 1       | 607   | 5     | 0.28   |
| WDC       | WD3202ABYS-01B7A0  | 320 GB | 3       | 581   | 5     | 0.28   |
| Toshiba   | MG08ACA16TE        | 16 TB  | 11      | 101   | 0     | 0.28   |
| Toshiba   | MK1637GSX          | 160 GB | 35      | 557   | 65    | 0.28   |
| Toshiba   | MG03ACA100         | 1 TB   | 12      | 190   | 2     | 0.28   |
| Seagate   | OOS3000G           | 3 TB   | 1       | 100   | 0     | 0.28   |
| WDC       | WD5000HHTZ-04N21V1 | 500 GB | 1       | 100   | 0     | 0.27   |
| Toshiba   | HDWT140            | 4 TB   | 2       | 100   | 0     | 0.27   |
| WDC       | WD10SPCX-75HWST0   | 1 TB   | 1       | 100   | 0     | 0.27   |
| Samsung   | MP0402H            | 40 GB  | 9       | 276   | 17    | 0.27   |
| HGST      | HTE725032A7E630    | 320 GB | 1       | 99    | 0     | 0.27   |
| WDC       | WD1600JD-55HBB0    | 160 GB | 1       | 695   | 6     | 0.27   |
| WDC       | WD1600BEAS-00RRT0  | 160 GB | 1       | 99    | 0     | 0.27   |
| Hitachi   | HTS541080G9AT00    | 80 GB  | 15      | 590   | 104   | 0.27   |
| WDC       | WD10SPZX-24Z10     | 1 TB   | 128     | 107   | 20    | 0.27   |
| WDC       | WD5000AAKS-00M9A0  | 500 GB | 6       | 853   | 437   | 0.27   |
| Toshiba   | HDWU130            | 3 TB   | 1       | 97    | 0     | 0.27   |
| WDC       | WD600VE-00HDT0     | 64 GB  | 1       | 97    | 0     | 0.27   |
| WDC       | WD101EDBZ-11B1DA0  | 10 TB  | 3       | 97    | 0     | 0.27   |
| Toshiba   | MK1011GAH          | 100 GB | 7       | 299   | 125   | 0.27   |
| WDC       | WD2500AAJS-00YZCA0 | 250 GB | 5       | 865   | 51    | 0.27   |
| Toshiba   | MG04ACA200E        | 2 TB   | 3       | 105   | 3     | 0.27   |
| Seagate   | ST6000NM021A-2R... | 6 TB   | 2       | 97    | 0     | 0.27   |
| WDC       | WD2500BPVT-80ZEST0 | 250 GB | 2       | 144   | 4     | 0.27   |
| Samsung   | SP2004C            | 200 GB | 35      | 769   | 622   | 0.27   |
| WDC       | WD1600BJKT-75F4T0  | 160 GB | 9       | 536   | 12    | 0.26   |
| Seagate   | ST380023A          | 80 GB  | 1       | 2897  | 29    | 0.26   |
| WDC       | WD30EZRZ-22Z5HB0   | 3 TB   | 3       | 96    | 0     | 0.26   |
| Seagate   | ST500VT001-1K6142  | 500 GB | 1       | 96    | 0     | 0.26   |
| WDC       | WD2500AAJS-60M0A0  | 250 GB | 5       | 707   | 227   | 0.26   |
| WDC       | WD1600BEKT-60A25T1 | 160 GB | 4       | 180   | 8     | 0.26   |
| Fujitsu   | MHV2100BH PL       | 100 GB | 8       | 182   | 2     | 0.26   |
| WDC       | WD7500BPVX-00JC3T0 | 752 GB | 3       | 95    | 0     | 0.26   |
| WDC       | WD1200BEVS-60RST0  | 120 GB | 1       | 766   | 7     | 0.26   |
| WDC       | WD5000LPLX-08ZNTT0 | 500 GB | 55      | 120   | 1     | 0.26   |
| Samsung   | SP0401N            | 40 GB  | 1       | 95    | 0     | 0.26   |
| WDC       | WD102PURZ-85BXPY0  | 10 TB  | 3       | 95    | 0     | 0.26   |
| Seagate   | STM31000528AS      | 1 TB   | 6       | 579   | 231   | 0.26   |
| Seagate   | ST10000NM0478-2... | 10 TB  | 8       | 94    | 0     | 0.26   |
| Seagate   | STM9120817AS       | 120 GB | 2       | 169   | 3     | 0.26   |
| WDC       | WD2500JS-19NCB1    | 250 GB | 1       | 92    | 0     | 0.25   |
| Seagate   | ST6000NE000-2KR101 | 6 TB   | 4       | 91    | 0     | 0.25   |
| WDC       | WD10JMVW-11S5XS1   | 1 TB   | 4       | 461   | 2     | 0.25   |
| Seagate   | ST3250310CS        | 250 GB | 4       | 948   | 186   | 0.25   |
| Fujitsu   | MJA2500BH G2       | 500 GB | 10      | 281   | 117   | 0.25   |
| WDC       | WD5000BPVT-60HXZT1 | 500 GB | 5       | 604   | 985   | 0.25   |
| WDC       | WD1600BPVT-22JJ5T0 | 160 GB | 1       | 91    | 0     | 0.25   |
| WDC       | WD7500AAVS-00D7B1  | 752 GB | 1       | 2278  | 24    | 0.25   |
| WDC       | WD1600AAJS-61M0A0  | 160 GB | 1       | 90    | 0     | 0.25   |
| Hitachi   | HTS545050B9SA00    | 500 GB | 10      | 934   | 807   | 0.25   |
| Seagate   | ST31000340SV       | 1 TB   | 1       | 1616  | 17    | 0.25   |
| WDC       | WD3200BEVT-22A0RT0 | 320 GB | 5       | 218   | 4     | 0.25   |
| Samsung   | HS082HB            | 80 GB  | 1       | 89    | 0     | 0.25   |
| Seagate   | ST320LT022-1AE142  | 320 GB | 2       | 170   | 2     | 0.25   |
| WDC       | WD800BD-08MRA1     | 80 GB  | 1       | 1427  | 15    | 0.24   |
| Hitachi   | HTS543232L9SA02    | 320 GB | 2       | 903   | 43    | 0.24   |
| Fujitsu   | MHW2040AT          | 40 GB  | 1       | 88    | 0     | 0.24   |
| WDC       | WD20NPVZ-00WFZT0   | 2 TB   | 4       | 88    | 0     | 0.24   |
| Seagate   | ST160LM000 HM161GI | 160 GB | 2       | 88    | 0     | 0.24   |
| WDC       | WD7500KMVW-11ZSMS4 | 752 GB | 2       | 373   | 6     | 0.24   |
| IBM/Hi... | IC35L040AVER07-0   | 41 GB  | 3       | 700   | 8     | 0.24   |
| Toshiba   | MK5076GSX          | 500 GB | 53      | 158   | 190   | 0.24   |
| WDC       | WD1600JS-61MHB1    | 160 GB | 1       | 959   | 10    | 0.24   |
| Hitachi   | HTS726060M9AT00    | 64 GB  | 2       | 289   | 34    | 0.24   |
| WDC       | WD2000JB-22GVA0    | 200 GB | 1       | 694   | 7     | 0.24   |
| WDC       | WD5000AZLX-22JKKA0 | 500 GB | 16      | 119   | 1     | 0.24   |
| Seagate   | ST500LM001-1EL162  | 500 GB | 1       | 86    | 0     | 0.24   |
| WDC       | WD1600BEVT-00A1TT0 | 160 GB | 2       | 273   | 3     | 0.24   |
| Samsung   | HM641JX            | 640 GB | 2       | 85    | 0     | 0.24   |
| HGST      | HTS545050B7E660    | 500 GB | 24      | 90    | 1     | 0.23   |
| WDC       | WD5000AAKS-07A7B2  | 500 GB | 1       | 1709  | 19    | 0.23   |
| WDC       | WUH721816ALE6L4    | 16 TB  | 2       | 85    | 0     | 0.23   |
| Samsung   | HD256GJ            | 250 GB | 4       | 401   | 260   | 0.23   |
| WDC       | WD2500AAKS-00L6A0  | 250 GB | 1       | 85    | 0     | 0.23   |
| Toshiba   | MK2046GSX          | 200 GB | 13      | 359   | 38    | 0.23   |
| Seagate   | ST1000DM000-9TS15E | 1 TB   | 2       | 712   | 503   | 0.23   |
| Toshiba   | MK2556GSY          | 250 GB | 7       | 172   | 467   | 0.23   |
| WDC       | WD20EFAX-68B2RN1   | 2 TB   | 2       | 84    | 0     | 0.23   |
| Seagate   | ST2000LM010-1RA174 | 2 TB   | 1       | 84    | 0     | 0.23   |
| Seagate   | ST16000NM000J-2... | 16 TB  | 32      | 83    | 0     | 0.23   |
| Samsung   | HD300LD            | 304 GB | 4       | 554   | 15    | 0.23   |
| Fujitsu   | MJA2250BH G2       | 250 GB | 9       | 435   | 119   | 0.23   |
| WDC       | WD2500AAJS-75B4A0  | 250 GB | 3       | 351   | 7     | 0.23   |
| WDC       | WD5000LPZX-80Z10T0 | 500 GB | 1       | 83    | 0     | 0.23   |
| Toshiba   | MK8032GAX          | 80 GB  | 2       | 117   | 252   | 0.23   |
| WDC       | WD180EDFZ-11AFWA0  | 18 TB  | 3       | 83    | 0     | 0.23   |
| HGST      | HUS726T4TALN6L4    | 4 TB   | 1       | 83    | 0     | 0.23   |
| Hitachi   | HTS542512K9A300    | 120 GB | 7       | 403   | 151   | 0.23   |
| Seagate   | ST9120821AS        | 120 GB | 8       | 323   | 1209  | 0.23   |
| Toshiba   | MK3021GAS          | 32 GB  | 1       | 495   | 5     | 0.23   |
| Toshiba   | HDWJ105            | 500 GB | 13      | 82    | 0     | 0.23   |
| WDC       | WD5000AACS-00G8B0  | 500 GB | 6       | 788   | 10    | 0.23   |
| WDC       | WD10SPZX-60Z10T0   | 1 TB   | 79      | 88    | 1     | 0.23   |
| WDC       | WD2500AAKX-193CA0  | 250 GB | 1       | 82    | 0     | 0.23   |
| WDC       | WD1600JD-41HBC0    | 160 GB | 1       | 1884  | 22    | 0.22   |
| WDC       | WD5000AAKS-00H2B0  | 499 GB | 1       | 731   | 8     | 0.22   |
| Fujitsu   | MHT2080BH          | 80 GB  | 2       | 543   | 10    | 0.22   |
| Hitachi   | HTS543232L9SA00    | 320 GB | 12      | 395   | 247   | 0.22   |
| Seagate   | ST3250820AV        | 250 GB | 1       | 80    | 0     | 0.22   |
| WDC       | WD10J31X-00U3VT0   | 1 TB   | 1       | 80    | 0     | 0.22   |
| Samsung   | SP2014N            | 200 GB | 7       | 978   | 164   | 0.22   |
| Hitachi   | HTS722020K9SA00    | 200 GB | 5       | 615   | 7     | 0.22   |
| Seagate   | ST3320613AS        | 320 GB | 111     | 868   | 274   | 0.22   |
| WDC       | WD5000AVVS-63M8B0  | 500 GB | 2       | 1443  | 62    | 0.22   |
| WDC       | WD3200AUDX-56WNHY0 | 320 GB | 4       | 80    | 0     | 0.22   |
| Toshiba   | MK6025GAS          | 64 GB  | 3       | 181   | 62    | 0.22   |
| Magnet... | MD03200-AJDW-RO    | 320 GB | 1       | 79    | 0     | 0.22   |
| WDC       | WD2003FYYS-05T8B0  | 2 TB   | 1       | 79    | 0     | 0.22   |
| Seagate   | ST500DM002-9YN14C  | 500 GB | 5       | 595   | 247   | 0.22   |
| WDC       | WD600BEVS-07LAT0   | 64 GB  | 1       | 635   | 7     | 0.22   |
| WDC       | WD400BB-75JHC0     | 40 GB  | 1       | 476   | 5     | 0.22   |
| Seagate   | ST31000322CS       | 1 TB   | 5       | 1340  | 113   | 0.22   |
| WDC       | WD3200BPVT-00HXZT1 | 320 GB | 10      | 350   | 218   | 0.22   |
| WDC       | WD10EZEX-60WN4A1   | 1 TB   | 30      | 92    | 1     | 0.22   |
| Seagate   | ST9250311CS        | 250 GB | 3       | 1048  | 312   | 0.22   |
| WDC       | WD80EMZZ-11B4FB0   | 8 TB   | 1       | 78    | 0     | 0.22   |
| Toshiba   | HDWK105            | 500 GB | 12      | 96    | 1     | 0.22   |
| Seagate   | ST3160812AS 41N... | 160 GB | 4       | 822   | 132   | 0.21   |
| WDC       | WD20PURZ-85AKKY0   | 2 TB   | 4       | 82    | 1     | 0.21   |
| WDC       | WD5000AZRX-00A3KB0 | 500 GB | 3       | 114   | 3     | 0.21   |
| WDC       | WD10EAVS-14M4B0    | 1 TB   | 1       | 77    | 0     | 0.21   |
| Hitachi   | HTS543280L9A300    | 80 GB  | 3       | 93    | 1     | 0.21   |
| WDC       | WD7500LPCX-60KHST0 | 752 GB | 3       | 77    | 0     | 0.21   |
| WDC       | WD10TPVT-00U4RT1   | 1 TB   | 4       | 289   | 116   | 0.21   |
| WDC       | WD141KRYZ-01C66B0  | 14 TB  | 3       | 76    | 0     | 0.21   |
| Fujitsu   | MHV2060AT PL       | 64 GB  | 3       | 851   | 16    | 0.21   |
| WDC       | WD5000KMVV-11BG7S0 | 500 GB | 1       | 152   | 1     | 0.21   |
| HGST      | HTS545032A7E380    | 320 GB | 62      | 176   | 592   | 0.21   |
| WDC       | WD3200BEKT-75F3T0  | 320 GB | 1       | 683   | 8     | 0.21   |
| WDC       | WD2502ABYS-50B7A1  | 250 GB | 1       | 1290  | 16    | 0.21   |
| WDC       | WD40EDAZ-11SLVB0   | 4 TB   | 5       | 75    | 0     | 0.21   |
| WDC       | WD60PURX-64WY0Y1   | 6 TB   | 1       | 74    | 0     | 0.21   |
| Seagate   | ST1000LM010-9YH146 | 1 TB   | 17      | 203   | 777   | 0.21   |
| Fujitsu   | MHV2080BH PL       | 80 GB  | 21      | 122   | 3     | 0.20   |
| Seagate   | ST2000LV000-2G2174 | 2 TB   | 1       | 74    | 0     | 0.20   |
| WDC       | WD400VE-07HDT0     | 40 GB  | 1       | 74    | 0     | 0.20   |
| WDC       | WD15NMVW-11AV3S3   | 1.5 TB | 1       | 743   | 9     | 0.20   |
| WDC       | WD800VE-75HDT1     | 80 GB  | 1       | 369   | 4     | 0.20   |
| WDC       | WD10EZRZ-22HTKB0   | 1 TB   | 16      | 84    | 1     | 0.20   |
| Seagate   | ST4000NC001-1FS168 | 4 TB   | 2       | 73    | 0     | 0.20   |
| WDC       | WD10SPSX-00A6WT0   | 1 TB   | 2       | 73    | 0     | 0.20   |
| Seagate   | ST4000NE001-2MA101 | 4 TB   | 11      | 73    | 0     | 0.20   |
| WDC       | WD3200BEKT-75PVMT0 | 320 GB | 4       | 546   | 12    | 0.20   |
| WDC       | WD2500BPVT-22JJ5T0 | 250 GB | 10      | 253   | 212   | 0.20   |
| Hitachi   | HDE721050SLA330    | 500 GB | 1       | 2416  | 32    | 0.20   |
| WDC       | WD20SPZX-08UA7     | 2 TB   | 7       | 73    | 0     | 0.20   |
| WDC       | WD1500BLHX-01V7BV0 | 150 GB | 1       | 72    | 0     | 0.20   |
| WDC       | WD1600SD-01KCC0    | 160 GB | 1       | 2914  | 39    | 0.20   |
| WDC       | WD30NMZW-11LG6S1   | 3 TB   | 2       | 72    | 0     | 0.20   |
| Hitachi   | HTS722016K9A300    | 160 GB | 4       | 242   | 259   | 0.20   |
| Seagate   | ST9120411ASG       | 120 GB | 1       | 361   | 4     | 0.20   |
| Toshiba   | MK1237GSX          | 120 GB | 22      | 430   | 129   | 0.20   |
| MediaMax  | WL4000GSA6472E 1   | 4 TB   | 1       | 71    | 0     | 0.20   |
| Seagate   | ST9160310AS        | 160 GB | 50      | 279   | 180   | 0.20   |
| Hitachi   | HTS725050A9A360    | 500 GB | 2       | 116   | 505   | 0.20   |
| WDC       | WD20EARS-22MVWB0   | 2 TB   | 3       | 2096  | 347   | 0.20   |
| WDC       | WD1200JB-00CRA1    | 120 GB | 2       | 790   | 20    | 0.20   |
| Seagate   | ST1000LM026 HN-... | 1 TB   | 1       | 214   | 2     | 0.20   |
| Toshiba   | MQ01ABD032V -63    | 320 GB | 1       | 714   | 9     | 0.20   |
| WDC       | WD101EMAZ-11G7DA0  | 10 TB  | 6       | 71    | 0     | 0.20   |
| HP        | MB1000EAMZE        | 1 TB   | 1       | 1919  | 26    | 0.19   |
| IBM       | DTLA-307015        | 16 GB  | 1       | 423   | 5     | 0.19   |
| Seagate   | ST31500341AS       | 1.5 TB | 96      | 808   | 295   | 0.19   |
| WDC       | WD20SDRW-34VUUS0   | 2 TB   | 3       | 70    | 0     | 0.19   |
| WDC       | WD5000BEVT-60ZAT1  | 500 GB | 9       | 833   | 506   | 0.19   |
| WDC       | WD50NDZW-11A8JS1   | 5 TB   | 16      | 69    | 0     | 0.19   |
| Toshiba   | MK6476GSXN         | 640 GB | 5       | 126   | 770   | 0.19   |
| Seagate   | ST500LM034-2GH17A  | 500 GB | 23      | 69    | 0     | 0.19   |
| Seagate   | ST8000NM012A-2K... | 8 TB   | 1       | 69    | 0     | 0.19   |
| Seagate   | ST3500320SV        | 500 GB | 2       | 940   | 10    | 0.19   |
| WDC       | WD2500AAJS-22L7A0  | 250 GB | 3       | 625   | 9     | 0.19   |
| WDC       | WD20SDRM-59A4DS1   | 2 TB   | 1       | 67    | 0     | 0.19   |
| Seagate   | ST91608220AS       | 160 GB | 1       | 135   | 1     | 0.19   |
| WDC       | WD200BB-60CJA0     | 20 GB  | 1       | 1417  | 20    | 0.18   |
| Samsung   | HN-M101XBB         | 1 TB   | 2       | 66    | 0     | 0.18   |
| Samsung   | SP1604N            | 160 GB | 5       | 393   | 77    | 0.18   |
| Toshiba   | MK6465GSX          | 640 GB | 31      | 758   | 612   | 0.18   |
| WDC       | WD1600AAJS         | 160 GB | 1       | 65    | 0     | 0.18   |
| WDC       | WD2500AAJS-60VWA1  | 250 GB | 1       | 65    | 0     | 0.18   |
| Seagate   | OOS12000G          | 12 TB  | 5       | 65    | 0     | 0.18   |
| Hitachi   | HTS421280H9AT00    | 80 GB  | 7       | 600   | 14    | 0.18   |
| WDC       | WD5000LPCX-80VHAT1 | 500 GB | 4       | 79    | 488   | 0.18   |
| Seagate   | ST2000NE0025-2F... | 2 TB   | 4       | 64    | 0     | 0.18   |
| WDC       | WD3200BUCT-62TWBY0 | 320 GB | 1       | 64    | 0     | 0.18   |
| WDC       | WD5000BEVT-11ZAT0  | 500 GB | 2       | 564   | 25    | 0.18   |
| Seagate   | ST3750330AS        | 752 GB | 17      | 1167  | 278   | 0.17   |
| WDC       | WD10EZRX-00RKKA0   | 1 TB   | 1       | 1714  | 26    | 0.17   |
| WDC       | WD10SPSX-60A6WT0   | 1 TB   | 7       | 63    | 0     | 0.17   |
| WDC       | WD3200AAJS-08B4A0  | 320 GB | 1       | 695   | 10    | 0.17   |
| Hitachi   | HTS541616J9AT00    | 160 GB | 3       | 241   | 5     | 0.17   |
| Seagate   | ST320VM001-1AD142  | 320 GB | 3       | 63    | 0     | 0.17   |
| WDC       | WD1200BEVE-00A0HT0 | 120 GB | 1       | 62    | 0     | 0.17   |
| WDC       | WD5000LPVX-16V0TT3 | 500 GB | 2       | 62    | 0     | 0.17   |
| Hitachi   | HDP725016GLAT80    | 160 GB | 1       | 62    | 0     | 0.17   |
| WDC       | WD3200AAKX-753CA1  | 320 GB | 3       | 276   | 15    | 0.17   |
| Toshiba   | MK1652GSX          | 160 GB | 27      | 435   | 50    | 0.17   |
| WDC       | WD3200AVJS-63TBA0  | 320 GB | 1       | 311   | 4     | 0.17   |
| WDC       | WD10EZRX-22L4HB0   | 1 TB   | 1       | 62    | 0     | 0.17   |
| Toshiba   | MK5065GSXN         | 500 GB | 13      | 400   | 668   | 0.17   |
| HGST      | HUH721212ALE600    | 12 TB  | 17      | 62    | 1     | 0.17   |
| WDC       | WD25EZRS-00J99B0   | 2.5 TB | 1       | 2353  | 37    | 0.17   |
| WDC       | WD10SPZX-75Z10T3   | 1 TB   | 23      | 65    | 5     | 0.17   |
| WDC       | WD7500BPVT-35HXZT3 | 752 GB | 1       | 309   | 4     | 0.17   |
| Toshiba   | MK3263GSXN         | 320 GB | 10      | 543   | 21    | 0.17   |
| Maxtor    | 4K060H3            | 64 GB  | 1       | 927   | 14    | 0.17   |
| Samsung   | SP1603C            | 160 GB | 1       | 367   | 5     | 0.17   |
| WDC       | WD160EDFZ-11AFWA0  | 16 TB  | 8       | 60    | 0     | 0.17   |
| WDC       | WD140EDFZ-11A0VA0  | 14 TB  | 25      | 60    | 0     | 0.17   |
| HGST      | HTS545025A7E330    | 250 GB | 1       | 60    | 0     | 0.17   |
| Fujitsu   | MHV2100AH PL       | 100 GB | 1       | 423   | 6     | 0.17   |
| Seagate   | ST31000524NS 44... | 1 TB   | 1       | 1693  | 27    | 0.17   |
| Toshiba   | MK1646GSX          | 160 GB | 14      | 528   | 217   | 0.17   |
| Hitachi   | DK23FB-60          | 64 GB  | 1       | 960   | 15    | 0.16   |
| WDC       | WD2500AAJS-98B4A0  | 250 GB | 1       | 540   | 8     | 0.16   |
| WDC       | WD1600BB-22GUC0    | 160 GB | 1       | 898   | 14    | 0.16   |
| MediaMax  | WL750GSA6472       | 752 GB | 1       | 59    | 0     | 0.16   |
| Seagate   | ST380021A          | 80 GB  | 11      | 826   | 47    | 0.16   |
| WDC       | WD40NDZM-59PW8S1   | 4 TB   | 1       | 59    | 0     | 0.16   |
| Seagate   | ST9320325ASG       | 320 GB | 1       | 357   | 5     | 0.16   |
| Maxtor    | STM3160811AS       | 160 GB | 7       | 648   | 232   | 0.16   |
| WDC       | WD10EZEX-75WN4A1   | 1 TB   | 33      | 59    | 1     | 0.16   |
| WDC       | WD1600BEVE-00A0HT0 | 160 GB | 1       | 58    | 0     | 0.16   |
| WDC       | WD1600HLFS-60G6U2  | 160 GB | 1       | 58    | 0     | 0.16   |
| WDC       | WD2000JB-00EVA0    | 200 GB | 1       | 5656  | 96    | 0.16   |
| Seagate   | ST980811A          | 80 GB  | 1       | 58    | 0     | 0.16   |
| MediaMax  | WL250GPA872B       | 250 GB | 1       | 58    | 0     | 0.16   |
| WDC       | WD10EZEX-35M2NA0   | 1 TB   | 2       | 305   | 4     | 0.16   |
| Seagate   | ST3320813AS        | 320 GB | 7       | 899   | 141   | 0.16   |
| Seagate   | ST3640323AS        | 640 GB | 9       | 1059  | 431   | 0.16   |
| Seagate   | ST32000644NS 45... | 2 TB   | 1       | 1247  | 21    | 0.16   |
| WDC       | WD20EZRZ-60Z5HB0   | 2 TB   | 2       | 56    | 0     | 0.15   |
| Hitachi   | HTS548040M9AT00    | 40 GB  | 2       | 365   | 10    | 0.15   |
| Seagate   | ST3160310CS        | 160 GB | 4       | 385   | 206   | 0.15   |
| Toshiba   | HDWD260            | 6 TB   | 4       | 55    | 0     | 0.15   |
| Seagate   | ST3200826A         | 200 GB | 2       | 561   | 8     | 0.15   |
| Samsung   | SP1213N            | 120 GB | 5       | 741   | 210   | 0.15   |
| WDC       | WD1500HLHX-01JJPV0 | 150 GB | 1       | 498   | 8     | 0.15   |
| WDC       | WD5000LPVX-55V0TT3 | 500 GB | 1       | 55    | 0     | 0.15   |
| WDC       | WD5000AZLX-60K2TA1 | 500 GB | 5       | 55    | 0     | 0.15   |
| WDC       | WD7500BPVT-60HXZT1 | 752 GB | 6       | 735   | 213   | 0.15   |
| WDC       | WD3200BEVT-60A23T0 | 320 GB | 27      | 405   | 399   | 0.15   |
| WDC       | WD10EALX-229BA1    | 1 TB   | 1       | 493   | 8     | 0.15   |
| Samsung   | HM060HC            | 52 GB  | 1       | 272   | 4     | 0.15   |
| Hitachi   | HDT725032VLAT80    | 320 GB | 4       | 1102  | 67    | 0.15   |
| Samsung   | HM501IX            | 500 GB | 1       | 54    | 0     | 0.15   |
| WDC       | WD120EFBX-68B0EN0  | 12 TB  | 3       | 54    | 0     | 0.15   |
| WDC       | WD1600YS-23SHB0    | 160 GB | 1       | 53    | 0     | 0.15   |
| IBM/Hi... | IC35L060AVV207-0   | 40 GB  | 2       | 1677  | 60    | 0.15   |
| WDC       | WD40NDZW-11A8JS0   | 4 TB   | 8       | 53    | 0     | 0.15   |
| WDC       | WD40NMZW-59GX6S1   | 4 TB   | 2       | 53    | 0     | 0.15   |
| Samsung   | HM120JI            | 120 GB | 5       | 324   | 6     | 0.15   |
| Toshiba   | MK6008GAH          | 64 GB  | 3       | 480   | 8     | 0.15   |
| WDC       | WD5000BPKT-80PK4T0 | 500 GB | 2       | 347   | 5     | 0.15   |
| Hitachi   | HTS543225L9SA00    | 250 GB | 9       | 425   | 35    | 0.15   |
| Maxtor    | 6L080J4            | 80 GB  | 1       | 319   | 5     | 0.15   |
| WDC       | WD1600BEVS-00RST0  | 160 GB | 1       | 52    | 0     | 0.15   |
| WDC       | WD2500BEVT-22ZAT0  | 250 GB | 1       | 316   | 5     | 0.14   |
| Hitachi   | HTS542525K9A300    | 250 GB | 9       | 660   | 704   | 0.14   |
| Hitachi   | HTS541040G9SA00    | 40 GB  | 2       | 400   | 9     | 0.14   |
| Seagate   | ST18000NE000-2Y... | 18 TB  | 4       | 51    | 0     | 0.14   |
| Hitachi   | HTS541060G9SA00    | 64 GB  | 4       | 280   | 90    | 0.14   |
| WDC       | WD20EURX-25T0FY0   | 2 TB   | 3       | 51    | 0     | 0.14   |
| WDC       | WD10SMZW-59Y0TS0   | 1 TB   | 1       | 51    | 0     | 0.14   |
| HGST      | HCC545050A7E630    | 500 GB | 3       | 51    | 0     | 0.14   |
| Seagate   | ST1000LM022-9XV155 | 1 TB   | 2       | 1349  | 2021  | 0.14   |
| WDC       | WD7500AARS-003BB1  | 752 GB | 2       | 753   | 121   | 0.14   |
| HGST      | HTS541075A7E630    | 752 GB | 9       | 71    | 113   | 0.14   |
| WDC       | WD1600AAJB-56R1A0  | 160 GB | 2       | 152   | 4     | 0.14   |
| Seagate   | ST960812A          | 64 GB  | 1       | 151   | 2     | 0.14   |
| WDC       | WD2005FBYZ-01YCBB3 | 2 TB   | 5       | 50    | 0     | 0.14   |
| Hitachi   | HTS722080K9A300    | 80 GB  | 4       | 279   | 3     | 0.14   |
| Toshiba   | HDWG11A            | 10 TB  | 1       | 50    | 0     | 0.14   |
| WDC       | WD8001FZBX-00ASYA0 | 8 TB   | 1       | 50    | 0     | 0.14   |
| WDC       | WD6400BPVT-75HXZT3 | 640 GB | 1       | 50    | 0     | 0.14   |
| WDC       | WD5000AAKS-60WWPA0 | 500 GB | 9       | 736   | 538   | 0.14   |
| WDC       | WD360GD-00FLA2     | 37 GB  | 4       | 1259  | 29    | 0.14   |
| Toshiba   | MK5056GSY          | 500 GB | 6       | 303   | 173   | 0.14   |
| WDC       | WD6003FRYZ-01F0DB0 | 6 TB   | 5       | 49    | 0     | 0.14   |
| WDC       | WD101EFAX-68LDBN0  | 10 TB  | 1       | 49    | 0     | 0.14   |
| HGST      | HUS726T4TALE6L4    | 4 TB   | 7       | 52    | 218   | 0.14   |
| WDC       | WD120EDBZ-11B1HA0  | 12 TB  | 4       | 49    | 0     | 0.14   |
| WDC       | WD10JUCX-63WPNY0   | 1 TB   | 2       | 93    | 37    | 0.14   |
| Seagate   | ST95000NSSUN500... | 500 GB | 1       | 2980  | 59    | 0.14   |
| Hitachi   | HTS725025A9A364    | 250 GB | 23      | 408   | 1037  | 0.14   |
| Seagate   | ST6000VX001-2BD186 | 6 TB   | 1       | 49    | 0     | 0.14   |
| WDC       | WD400EB-00CPF0     | 40 GB  | 5       | 676   | 61    | 0.14   |
| Seagate   | ST500LM030-1RK17D  | 500 GB | 22      | 57    | 1     | 0.13   |
| Seagate   | ST8000VX004-2M1101 | 8 TB   | 1       | 48    | 0     | 0.13   |
| WDC       | WD10JUCT-61CYNY0   | 1 TB   | 1       | 48    | 0     | 0.13   |
| WDC       | WD5000LPCX-80VHAT0 | 500 GB | 2       | 48    | 0     | 0.13   |
| Hitachi   | HTS424040M9AT00    | 40 GB  | 7       | 441   | 161   | 0.13   |
| ExcelStor | J8160              | 34 GB  | 1       | 48    | 0     | 0.13   |
| WDC       | WD2500BPVT-26JJ5T0 | 250 GB | 1       | 48    | 0     | 0.13   |
| Fujitsu   | MHZ2160BJ FFS G2   | 160 GB | 1       | 436   | 8     | 0.13   |
| Seagate   | ST9808210A         | 80 GB  | 2       | 259   | 19    | 0.13   |
| WDC       | WD400BB-00CAA1     | 40 GB  | 1       | 289   | 5     | 0.13   |
| Seagate   | ST9402115AS        | 40 GB  | 4       | 113   | 521   | 0.13   |
| WDC       | WD15NMVW-11EDZS2   | 1.5 TB | 1       | 48    | 0     | 0.13   |
| WDC       | WD6001FSYZ-01SS7B1 | 6 TB   | 1       | 47    | 0     | 0.13   |
| WDC       | WD5000LMVW-11VEDS3 | 500 GB | 5       | 131   | 220   | 0.13   |
| WDC       | WD10TMVV-11BG7S0   | 1 TB   | 3       | 595   | 10    | 0.13   |
| Hitachi   | HTS421210H9AT00    | 100 GB | 1       | 568   | 11    | 0.13   |
| WDC       | WD5000BPVX-00JC3T0 | 500 GB | 3       | 47    | 0     | 0.13   |
| WDC       | WD360GD-00FLA1     | 37 GB  | 1       | 1789  | 37    | 0.13   |
| WDC       | WUH721414ALE6L4    | 14 TB  | 5       | 46    | 0     | 0.13   |
| WDC       | WD1600AAJS-22B4A0  | 160 GB | 1       | 46    | 0     | 0.13   |
| WDC       | WD3200BEKT-22KA9T0 | 320 GB | 1       | 46    | 0     | 0.13   |
| WDC       | WD5000LPLX-66ZNTT1 | 500 GB | 4       | 49    | 1     | 0.13   |
| WDC       | WD20SPZX-75UA7T1   | 2 TB   | 3       | 45    | 0     | 0.13   |
| WDC       | WD101KFBX-68R56N0  | 10 TB  | 1       | 45    | 0     | 0.13   |
| WDC       | WD3200BEKT-60F3T1  | 320 GB | 11      | 534   | 505   | 0.13   |
| Toshiba   | MK1665GSX          | 160 GB | 22      | 190   | 354   | 0.13   |
| WDC       | WD7500AYPS-01ZKB0  | 752 GB | 1       | 228   | 4     | 0.12   |
| WDC       | WD1200BEVS-22LAT0  | 120 GB | 2       | 406   | 81    | 0.12   |
| WDC       | WD80EFBX-68AZZN0   | 8 TB   | 5       | 45    | 0     | 0.12   |
| Samsung   | SV4012H            | 40 GB  | 2       | 1504  | 236   | 0.12   |
| WDC       | WD3200AAJS-00V4A0  | 320 GB | 3       | 396   | 9     | 0.12   |
| WDC       | WD1600AAJS-19WAA0  | 160 GB | 1       | 44    | 0     | 0.12   |
| WDC       | WD800BEVS-60RST0   | 80 GB  | 2       | 643   | 291   | 0.12   |
| IBM       | DTLA-307020        | 20 GB  | 1       | 754   | 16    | 0.12   |
| Hitachi   | HTS541212H9SA00    | 120 GB | 1       | 221   | 4     | 0.12   |
| Hitachi   | HTS725032A7E630    | 320 GB | 4       | 836   | 771   | 0.12   |
| WDC       | WD50NDZM-59A8KS1   | 5 TB   | 1       | 44    | 0     | 0.12   |
| MARSHAL   | MAL2500SA-T54      | 500 GB | 3       | 247   | 18    | 0.12   |
| WDC       | WD5000AAKX-004EA0  | 500 GB | 1       | 392   | 8     | 0.12   |
| WDC       | WD60EZAZ-00SF3B0   | 6 TB   | 4       | 43    | 0     | 0.12   |
| Seagate   | ST3500410SV        | 500 GB | 4       | 1004  | 282   | 0.12   |
| Hitachi   | HDP725025GLAT80    | 250 GB | 1       | 216   | 4     | 0.12   |
| WDC       | WD1600BEVS-60VAT0  | 160 GB | 1       | 650   | 14    | 0.12   |
| Toshiba   | MQ02ABF050H        | 500 GB | 6       | 193   | 342   | 0.12   |
| WDC       | WD3200BMVS-11F9S0  | 320 GB | 1       | 43    | 0     | 0.12   |
| WDC       | WD10TPVT-00HT5T1   | 1 TB   | 2       | 396   | 9     | 0.12   |
| Seagate   | ST2000VX000-9YW164 | 2 TB   | 7       | 700   | 892   | 0.12   |
| Maxtor    | 6B300R0            | 304 GB | 1       | 42    | 0     | 0.12   |
| WDC       | WD5000AURX-63UY4Y0 | 500 GB | 2       | 1019  | 23    | 0.12   |
| WDC       | WD1600BMVS-11F9S0  | 160 GB | 1       | 339   | 7     | 0.12   |
| WDC       | WD1503FYYS-02W0B0  | 1.5 TB | 1       | 382   | 8     | 0.12   |
| Maxtor    | 6B160P0            | 163 GB | 1       | 42    | 0     | 0.12   |
| IBM/Hi... | IC25N080ATMR04-0   | 80 GB  | 5       | 345   | 35    | 0.12   |
| WDC       | WD1600BEVT-26ZCT0  | 160 GB | 2       | 186   | 22    | 0.12   |
| WDC       | WD400BD-08JMC0     | 40 GB  | 1       | 801   | 18    | 0.12   |
| WDC       | WD40PURZ-85AKKY0   | 4 TB   | 25      | 65    | 1     | 0.12   |
| Quantum   | FIREBALLlct20 10   | 10 GB  | 1       | 42    | 0     | 0.12   |
| WDC       | WD15NMVW-11EDZS6   | 1.5 TB | 1       | 41    | 0     | 0.11   |
| Hitachi   | HTS723225A7A364    | 250 GB | 3       | 636   | 679   | 0.11   |
| IBM/Hi... | IC25N030ATCS04-0   | 32 GB  | 3       | 198   | 5     | 0.11   |
| Seagate   | ST31000533CS       | 1 TB   | 2       | 828   | 40    | 0.11   |
| IBM/Hi... | IC25N060ATMR04-0   | 64 GB  | 9       | 353   | 24    | 0.11   |
| Samsung   | HM160HC            | 160 GB | 9       | 218   | 17    | 0.11   |
| Seagate   | ST9250410ASG       | 250 GB | 2       | 543   | 513   | 0.11   |
| Toshiba   | MK4055GSX          | 400 GB | 3       | 338   | 7     | 0.11   |
| WDC       | WD15SMZW-11JW8S0   | 1.5 TB | 2       | 41    | 0     | 0.11   |
| Maxtor    | 7L250R0            | 256 GB | 1       | 40    | 0     | 0.11   |
| Fujitsu   | MHV2200BT PL       | 200 GB | 1       | 325   | 7     | 0.11   |
| WDC       | WD1600BEVE-00UYT0  | 160 GB | 1       | 40    | 0     | 0.11   |
| WDC       | WD3200LPVT-00G33T0 | 320 GB | 2       | 40    | 0     | 0.11   |
| Seagate   | ST9250320AS        | 250 GB | 24      | 507   | 317   | 0.11   |
| WDC       | WD6400AAKS-55A7B2  | 640 GB | 1       | 361   | 8     | 0.11   |
| MediaMax  | WL1000GSA3254G     | 1 TB   | 1       | 476   | 11    | 0.11   |
| Seagate   | ST10000NE0008-2... | 10 TB  | 5       | 39    | 0     | 0.11   |
| WDC       | WD40EMRX-82UZ0N0   | 4 TB   | 4       | 60    | 1     | 0.11   |
| Hitachi   | HTS545012B9SA00    | 120 GB | 1       | 197   | 4     | 0.11   |
| Samsung   | HM251JI            | 250 GB | 9       | 296   | 466   | 0.11   |
| WDC       | WD5000LPCX-75VHAT1 | 500 GB | 3       | 39    | 0     | 0.11   |
| WDC       | WD3200LPVT-22G33T0 | 320 GB | 2       | 39    | 0     | 0.11   |
| WDC       | WD5000AVCS-612DY1  | 500 GB | 1       | 582   | 14    | 0.11   |
| WDC       | WD15SMRW-11YNDS0   | 1.5 TB | 1       | 38    | 0     | 0.11   |
| WDC       | WD50NMZW-59A8NS1   | 5 TB   | 3       | 38    | 0     | 0.11   |
| WDC       | WD20SPZX-21UA7T0   | 2 TB   | 2       | 38    | 0     | 0.11   |
| Samsung   | HM100JC            | 100 GB | 1       | 383   | 9     | 0.10   |
| WDC       | WD1500ADFD-00NLR5  | 150 GB | 1       | 344   | 8     | 0.10   |
| WDC       | WD1600BEKT-66PVMT0 | 160 GB | 1       | 761   | 19    | 0.10   |
| Hitachi   | HTS541020G9SA00    | 20 GB  | 1       | 38    | 0     | 0.10   |
| MARSHAL   | MAL2750SA-T54      | 752 GB | 3       | 226   | 849   | 0.10   |
| WDC       | WD153AA-53BAA0     | 16 GB  | 1       | 491   | 12    | 0.10   |
| WDC       | WD60EDAZ-11U78B0   | 6 TB   | 3       | 37    | 0     | 0.10   |
| Hitachi   | HDT721050SLA380    | 500 GB | 1       | 224   | 5     | 0.10   |
| WDC       | WD1600BEKT-60V5T1  | 160 GB | 3       | 150   | 4     | 0.10   |
| WDC       | WD3200BEVS-16VAT0  | 320 GB | 1       | 37    | 0     | 0.10   |
| WDC       | WD30NMZW-11A8NS1   | 3 TB   | 1       | 36    | 0     | 0.10   |
| WDC       | WD5000LPCX-60VHAT1 | 500 GB | 18      | 79    | 11    | 0.10   |
| WDC       | WD20EVDS-63T3B0    | 2 TB   | 2       | 330   | 8     | 0.10   |
| Toshiba   | MK5061GSYN         | 500 GB | 24      | 85    | 318   | 0.10   |
| WDC       | WD800AAJS-60M0A0   | 80 GB  | 1       | 2215  | 60    | 0.10   |
| Toshiba   | MK3261GSYN         | 320 GB | 23      | 75    | 264   | 0.10   |
| HGST      | HUS726060ALE611    | 6 TB   | 2       | 36    | 0     | 0.10   |
| WDC       | WD10SDRW-11A0XS1   | 1 TB   | 4       | 36    | 0     | 0.10   |
| WDC       | WD800AAJS-60B4A0   | 80 GB  | 2       | 1529  | 24    | 0.10   |
| Maxtor    | 6L120P0            | 122 GB | 2       | 35    | 0     | 0.10   |
| Seagate   | ST3500320AS        | 500 GB | 101     | 826   | 442   | 0.10   |
| Fujitsu   | MHJ2181AT          | 18 GB  | 1       | 1462  | 41    | 0.10   |
| WDC       | WD5000LPLX-21ZNTT0 | 500 GB | 3       | 78    | 366   | 0.10   |
| Hitachi   | HTS725025A9A361... | 250 GB | 1       | 34    | 0     | 0.09   |
| Toshiba   | HDWR160            | 6 TB   | 2       | 34    | 0     | 0.09   |
| Seagate   | ST14000NE0008-2... | 14 TB  | 8       | 33    | 0     | 0.09   |
| WDC       | WD20EARX-00AZ6B0   | 2 TB   | 1       | 505   | 14    | 0.09   |
| HGST      | HTS725050B7E630    | 500 GB | 2       | 33    | 0     | 0.09   |
| Seagate   | ST3000VX009-2AY10G | 3 TB   | 3       | 33    | 0     | 0.09   |
| Maxtor    | 2F030L0            | 32 GB  | 1       | 33    | 0     | 0.09   |
| Toshiba   | MK1235GSL          | 120 GB | 1       | 32    | 0     | 0.09   |
| WDC       | WD6400BEVT-24A0RT0 | 640 GB | 1       | 329   | 9     | 0.09   |
| WDC       | WD40EZAZ-00ZGHB0   | 4 TB   | 1       | 32    | 0     | 0.09   |
| Toshiba   | HDWM105            | 500 GB | 1       | 32    | 0     | 0.09   |
| WDC       | WD5003AZEX-00K3CA0 | 500 GB | 3       | 92    | 3     | 0.09   |
| Hitachi   | DK23EA-40          | 40 GB  | 2       | 241   | 236   | 0.09   |
| WDC       | WD5000LMVW-11VEDS6 | 500 GB | 3       | 188   | 24    | 0.09   |
| Seagate   | ST2000NM000A-2J... | 2 TB   | 3       | 32    | 0     | 0.09   |
| WDC       | WD181KRYZ-01AGBB0  | 18 TB  | 1       | 32    | 0     | 0.09   |
| Synology  | HAT5300-16T        | 16 TB  | 7       | 32    | 0     | 0.09   |
| Fujitsu   | MHT2030AT          | 32 GB  | 1       | 32    | 0     | 0.09   |
| WDC       | WD40EZAZ-00SF3B0   | 4 TB   | 20      | 32    | 0     | 0.09   |
| WDC       | WD10E              | 1 TB   | 1       | 31    | 0     | 0.09   |
| Maxtor    | STM3320613AS       | 320 GB | 15      | 1094  | 432   | 0.09   |
| Toshiba   | MK1255GSX H        | 120 GB | 4       | 186   | 214   | 0.09   |
| WDC       | WD800JB-00FSA0     | 80 GB  | 1       | 1366  | 43    | 0.09   |
| WDC       | WD2500JD-00HBC0    | 250 GB | 1       | 620   | 19    | 0.09   |
| Maxtor    | 2F030J1            | 32 GB  | 1       | 185   | 5     | 0.08   |
| WDC       | WD121KFBX-68EF5N0  | 12 TB  | 7       | 30    | 0     | 0.08   |
| WDC       | WD367GD-00FLA1     | 37 GB  | 1       | 1757  | 57    | 0.08   |
| Samsung   | HM121HC            | 120 GB | 3       | 230   | 19    | 0.08   |
| MediaMax  | WL1500GSA6454G     | 1.5 TB | 2       | 96    | 4     | 0.08   |
| Seagate   | ST38410A           | 9 GB   | 1       | 754   | 24    | 0.08   |
| WDC       | WD600VE-75HDT0     | 64 GB  | 1       | 268   | 8     | 0.08   |
| IBM/Hi... | IC25N040ATCS04-0   | 40 GB  | 1       | 59    | 1     | 0.08   |
| WDC       | WD5000BEVT-35ZAT0  | 500 GB | 1       | 268   | 8     | 0.08   |
| Samsung   | SV0401N            | 40 GB  | 1       | 952   | 31    | 0.08   |
| Seagate   | ST750LM028-1KK162  | 752 GB | 1       | 29    | 0     | 0.08   |
| Seagate   | ST500LM016 HN-M... | 500 GB | 3       | 29    | 0     | 0.08   |
| Samsung   | MP0804H            | 80 GB  | 3       | 243   | 8     | 0.08   |
| WDC       | WD1600JS-00MHB1    | 160 GB | 1       | 1060  | 35    | 0.08   |
| CLOVER    | CN-M500MBB         | 500 GB | 2       | 29    | 0     | 0.08   |
| Hitachi   | HTS723232L9A360    | 320 GB | 7       | 905   | 844   | 0.08   |
| Samsung   | HS12UHE            | 120 GB | 2       | 143   | 5     | 0.08   |
| Maxtor    | STM3500320AS       | 500 GB | 23      | 616   | 263   | 0.08   |
| Maxtor    | 6L100M0            | 100 GB | 2       | 28    | 0     | 0.08   |
| WDC       | WD5000LPSX-08A6W   | 500 GB | 3       | 28    | 0     | 0.08   |
| Seagate   | ST94813A           | 40 GB  | 1       | 28    | 0     | 0.08   |
| MediaMax  | WL120GBSATA        | 120 GB | 1       | 139   | 4     | 0.08   |
| WDC       | WD40EFAX-68JH4N1   | 4 TB   | 13      | 28    | 1     | 0.08   |
| WDC       | WD40NDZM-59A8KS1   | 4 TB   | 1       | 274   | 9     | 0.08   |
| Hitachi   | HCS721010CLA332    | 1 TB   | 1       | 2077  | 76    | 0.07   |
| Toshiba   | MK6476GSX          | 640 GB | 26      | 32    | 396   | 0.07   |
| WDC       | WD2000JD-55HBC0    | 200 GB | 1       | 26    | 0     | 0.07   |
| WDC       | WD20EZAZ-00L9GB0   | 2 TB   | 9       | 26    | 0     | 0.07   |
| Toshiba   | HDWG480            | 8 TB   | 2       | 26    | 0     | 0.07   |
| WDC       | WD3200AAJS-00VWA1  | 320 GB | 1       | 708   | 26    | 0.07   |
| Hitachi   | HTS421260H9AT00    | 64 GB  | 4       | 462   | 19    | 0.07   |
| Samsung   | HM251JJ            | 250 GB | 1       | 156   | 5     | 0.07   |
| Seagate   | ST31000333AS       | 1 TB   | 35      | 827   | 384   | 0.07   |
| WDC       | WD2500JB-55EVA0    | 250 GB | 1       | 77    | 2     | 0.07   |
| WDC       | WD20SDRW-11VUUS1   | 2 TB   | 3       | 25    | 0     | 0.07   |
| Samsung   | HM322IX            | 320 GB | 1       | 25    | 0     | 0.07   |
| WDC       | WD6400BPVT-60HXZT3 | 640 GB | 1       | 1069  | 41    | 0.07   |
| Fujitsu   | MHZ2120BH G2       | 120 GB | 4       | 267   | 771   | 0.07   |
| WDC       | WD1600BUDT-63DPZY0 | 160 GB | 1       | 25    | 0     | 0.07   |
| WDC       | WD101FZBX-00ATAA0  | 10 TB  | 1       | 25    | 0     | 0.07   |
| WDC       | WD3200JD-22KLB0    | 320 GB | 1       | 1261  | 50    | 0.07   |
| WDC       | WD3200AAJS-57VWA2  | 320 GB | 1       | 24    | 0     | 0.07   |
| WDC       | WD2500AAJS-52B4A0  | 250 GB | 2       | 942   | 45    | 0.07   |
| Seagate   | ST3750840ACE       | 752 GB | 1       | 483   | 19    | 0.07   |
| WDC       | WD20EZBX-00AYRA0   | 2 TB   | 10      | 24    | 0     | 0.07   |
| WDC       | WD400VE-75HDT1     | 40 GB  | 1       | 23    | 0     | 0.06   |
| WDC       | WD1200BEVS-07LAT0  | 120 GB | 6       | 343   | 310   | 0.06   |
| Toshiba   | MK6032GAX          | 64 GB  | 1       | 23    | 0     | 0.06   |
| Toshiba   | MK8052GSX          | 80 GB  | 7       | 196   | 29    | 0.06   |
| Toshiba   | MK3265GSX H        | 320 GB | 2       | 44    | 15    | 0.06   |
| Seagate   | ST4000VX000-2AG166 | 4 TB   | 1       | 23    | 0     | 0.06   |
| IBM       | DJSA-220           | 12 GB  | 1       | 138   | 5     | 0.06   |
| Toshiba   | MK6465GSXW         | 640 GB | 1       | 552   | 23    | 0.06   |
| Toshiba   | MK2529GSG          | 250 GB | 2       | 313   | 1127  | 0.06   |
| Magnet... | MD02500-BQDW-RO    | 250 GB | 1       | 22    | 0     | 0.06   |
| WDC       | WD40EMAZ-11ZRJB0   | 4 TB   | 3       | 22    | 0     | 0.06   |
| Hitachi   | HTS543216L9SA02    | 160 GB | 3       | 134   | 11    | 0.06   |
| Toshiba   | MG08ACA14TE        | 14 TB  | 1       | 22    | 0     | 0.06   |
| WDC       | WD3200AVBS-63TAA0  | 320 GB | 1       | 741   | 32    | 0.06   |
| CLOVER    | CN-M750MBB         | 752 GB | 1       | 22    | 0     | 0.06   |
| Toshiba   | MK1032GAX          | 100 GB | 2       | 108   | 4     | 0.06   |
| WDC       | WD3200BEKX-22B7WT0 | 320 GB | 1       | 21    | 0     | 0.06   |
| WDC       | WD1600BEKT-00PVMT0 | 160 GB | 1       | 21    | 0     | 0.06   |
| Seagate   | ST14000VE0008-2... | 14 TB  | 5       | 21    | 0     | 0.06   |
| Seagate   | ST3300831A         | 304 GB | 1       | 347   | 15    | 0.06   |
| WDC       | WD30EFZX-68AWUN0   | 3 TB   | 2       | 21    | 0     | 0.06   |
| Maxtor    | 4K040H2            | 40 GB  | 2       | 249   | 19    | 0.06   |
| WDC       | WD102KRYZ-01A5AB0  | 10 TB  | 1       | 21    | 0     | 0.06   |
| WDC       | WD5000AAKX-009FA0  | 500 GB | 1       | 230   | 10    | 0.06   |
| Maxtor    | STM3160613AS       | 160 GB | 1       | 41    | 1     | 0.06   |
| Fujitsu   | MHT2040AT          | 40 GB  | 1       | 166   | 7     | 0.06   |
| WDC       | WD20SDRW-34VUUS1   | 2 TB   | 1       | 20    | 0     | 0.06   |
| WDC       | WD400BB-22DEA0     | 40 GB  | 1       | 831   | 39    | 0.06   |
| Maxtor    | 6L200P0            | 208 GB | 5       | 22    | 5     | 0.06   |
| Toshiba   | MQ02ABF050H-SSH... | 500 GB | 2       | 20    | 0     | 0.06   |
| WDC       | WD2000BB-00GUC0    | 200 GB | 1       | 637   | 30    | 0.06   |
| Hitachi   | HTS543212L9A300    | 120 GB | 4       | 418   | 513   | 0.06   |
| Maxtor    | 6B200M0            | 200 GB | 6       | 30    | 22    | 0.06   |
| WDC       | WD10SMZW-34Y0TS0   | 1 TB   | 1       | 20    | 0     | 0.06   |
| WDC       | WD5000BPVT-75A1YT0 | 500 GB | 1       | 20    | 0     | 0.06   |
| WDC       | WD20SPZX-11CRAT0   | 2 TB   | 1       | 20    | 0     | 0.06   |
| WDC       | WD2500BPVT-00ZEST0 | 250 GB | 3       | 136   | 74    | 0.06   |
| Fujitsu   | MHV2060AH          | 64 GB  | 1       | 968   | 47    | 0.06   |
| MediaMax  | WL640GSA6472B      | 647 GB | 1       | 20    | 0     | 0.05   |
| WDC       | WD2500LPCX-24VHAT0 | 250 GB | 2       | 55    | 5     | 0.05   |
| MediaMax  | WL160GSA872B       | 160 GB | 1       | 517   | 25    | 0.05   |
| IBM       | DARA-206000        | 6 GB   | 1       | 118   | 5     | 0.05   |
| Seagate   | ST9100822A         | 100 GB | 2       | 627   | 31    | 0.05   |
| IBM/Hi... | IC25N040ATMR04-0   | 40 GB  | 2       | 628   | 181   | 0.05   |
| Seagate   | ST10000VN0008-2... | 10 TB  | 3       | 19    | 0     | 0.05   |
| Seagate   | ST4000NM000A 00... | 4 TB   | 4       | 19    | 0     | 0.05   |
| Maxtor    | STM3300622A        | 304 GB | 1       | 173   | 8     | 0.05   |
| Samsung   | HD160HJ            | 160 GB | 24      | 731   | 772   | 0.05   |
| WDC       | WD200EB-75CPF0     | 20 GB  | 2       | 402   | 20    | 0.05   |
| Maxtor    | 2F040J0            | 40 GB  | 1       | 19    | 0     | 0.05   |
| WDC       | WD1600JD-00GBB0    | 160 GB | 1       | 727   | 37    | 0.05   |
| WDC       | WD10EZEX-00BBHA0   | 1 TB   | 9       | 19    | 0     | 0.05   |
| Seagate   | ST3500620AS        | 500 GB | 9       | 818   | 759   | 0.05   |
| Seagate   | ST9250421ASG       | 250 GB | 1       | 453   | 23    | 0.05   |
| WDC       | WD1001FAES-75W7A0  | 1 TB   | 3       | 1442  | 442   | 0.05   |
| Hitachi   | HTS541640J9SA00    | 40 GB  | 2       | 309   | 387   | 0.05   |
| WDC       | WD101EDAZ-11Y7KA0  | 10 TB  | 1       | 18    | 0     | 0.05   |
| WDC       | WD5000LUCT-62RC2Y0 | 500 GB | 1       | 18    | 0     | 0.05   |
| Hitachi   | HCP725050GLAT80    | 500 GB | 1       | 240   | 12    | 0.05   |
| Toshiba   | MK3276GSX          | 320 GB | 38      | 28    | 279   | 0.05   |
| WDC       | WD7500BPVT-75HXZT1 | 752 GB | 1       | 547   | 29    | 0.05   |
| Toshiba   | MQ01ABU050W        | 500 GB | 1       | 54    | 2     | 0.05   |
| Samsung   | HM160HI            | 160 GB | 91      | 352   | 418   | 0.05   |
| WDC       | WD6003FFBX-68MU3N0 | 6 TB   | 1       | 18    | 0     | 0.05   |
| WDC       | WD800JD-75LSA0     | 80 GB  | 1       | 616   | 33    | 0.05   |
| WDC       | WD1600BB-55GUA0    | 160 GB | 2       | 661   | 134   | 0.05   |
| WDC       | WD20SMRW-59YNDS0   | 2 TB   | 5       | 17    | 0     | 0.05   |
| Seagate   | ST91000430AS       | 1 TB   | 1       | 124   | 6     | 0.05   |
| WDC       | WD5000LPVX-16V0TT0 | 500 GB | 1       | 71    | 3     | 0.05   |
| WDC       | WD2500BEVT-60A23T0 | 250 GB | 5       | 456   | 115   | 0.05   |
| WDC       | WUH721818ALE6L4    | 18 TB  | 5       | 17    | 0     | 0.05   |
| WDC       | WD40EFZX-68AWUN0   | 4 TB   | 11      | 24    | 1     | 0.05   |
| Maxtor    | 6L200M0            | 208 GB | 5       | 28    | 14    | 0.05   |
| Quantum   | FIREBALLlct15 10   | 10 GB  | 1       | 105   | 5     | 0.05   |
| Seagate   | ST1000NX0313       | 1 TB   | 3       | 468   | 124   | 0.05   |
| WDC       | WD1600JS-55MHB0    | 160 GB | 1       | 761   | 43    | 0.05   |
| Toshiba   | MQ04ABB400         | 4 TB   | 1       | 17    | 0     | 0.05   |
| Samsung   | HM320JI            | 320 GB | 12      | 340   | 398   | 0.05   |
| WDC       | WD10JPVX-08JC3T1   | 1 TB   | 1       | 17    | 0     | 0.05   |
| Maxtor    | 6L080M0            | 80 GB  | 7       | 23    | 146   | 0.05   |
| Toshiba   | HDWG21C            | 12 TB  | 1       | 16    | 0     | 0.05   |
| Hitachi   | HDP725032GLAT80    | 320 GB | 1       | 943   | 55    | 0.05   |
| WDC       | WD80EDAZ-11TA3A0   | 8 TB   | 7       | 16    | 0     | 0.05   |
| Maxtor    | 6B300S0            | 304 GB | 2       | 17    | 1     | 0.05   |
| WDC       | WD60EFZX-68B3FN0   | 6 TB   | 1       | 16    | 0     | 0.05   |
| Maxtor    | 6L080L0            | 82 GB  | 7       | 24    | 11    | 0.04   |
| Samsung   | HN-M250MBB         | 250 GB | 1       | 292   | 17    | 0.04   |
| Samsung   | HM060HI            | 64 GB  | 3       | 542   | 697   | 0.04   |
| Seagate   | ST10000VN0008-2... | 10 TB  | 2       | 16    | 0     | 0.04   |
| WDC       | WD10SPSX-22A6WT0   | 1 TB   | 3       | 16    | 0     | 0.04   |
| Seagate   | ST12000VN0008-2... | 12 TB  | 1       | 16    | 0     | 0.04   |
| WDC       | WD60EDAZ-11BMZB0   | 6 TB   | 1       | 16    | 0     | 0.04   |
| Seagate   | ST500LX025-1U71... | 500 GB | 1       | 15    | 0     | 0.04   |
| Seagate   | ST31000340AS       | 1 TB   | 9       | 774   | 253   | 0.04   |
| WDC       | WD800BB-88JHC0     | 80 GB  | 1       | 1625  | 101   | 0.04   |
| IBM/Hi... | IC35L060AVVA07-0   | 64 GB  | 1       | 678   | 42    | 0.04   |
| HGST      | TPH00901000GB 0    | 1 TB   | 1       | 613   | 38    | 0.04   |
| WDC       | WD140EFFX-68VBXN0  | 14 TB  | 16      | 15    | 0     | 0.04   |
| WDC       | WD121PURZ-85GUCY0  | 12 TB  | 5       | 15    | 0     | 0.04   |
| Toshiba   | MK5055GSXF         | 500 GB | 2       | 231   | 87    | 0.04   |
| Maxtor    | 6B200P0            | 208 GB | 5       | 30    | 723   | 0.04   |
| WDC       | WD4000ABYS-01TNA0  | 400 GB | 1       | 688   | 44    | 0.04   |
| Toshiba   | MK5059GSX          | 500 GB | 2       | 693   | 61    | 0.04   |
| Maxtor    | 6L250S0            | 250 GB | 3       | 28    | 8     | 0.04   |
| Samsung   | SP1253N            | 120 GB | 1       | 286   | 18    | 0.04   |
| MediaMax  | WL250GSA872        | 250 GB | 1       | 15    | 0     | 0.04   |
| Hitachi   | HDS7250SASUN500G   | 500 GB | 1       | 14    | 0     | 0.04   |
| Seagate   | ST3000VM002-1ET166 | 3 TB   | 3       | 497   | 849   | 0.04   |
| Seagate   | OOS500G            | 500 GB | 1       | 14    | 0     | 0.04   |
| WDC       | WD3200AAKS-00M9A0  | 320 GB | 1       | 751   | 51    | 0.04   |
| Seagate   | ST9120310AS        | 120 GB | 1       | 14    | 0     | 0.04   |
| WDC       | WD205BA            | 20 GB  | 1       | 296   | 20    | 0.04   |
| Toshiba   | HDWD220            | 2 TB   | 7       | 14    | 0     | 0.04   |
| WDC       | WD10SDRW-11A0XS0   | 1 TB   | 8       | 27    | 254   | 0.04   |
| Seagate   | ST1000NM004A-2M... | 1 TB   | 4       | 13    | 0     | 0.04   |
| Toshiba   | MK1656GSYF         | 160 GB | 1       | 96    | 6     | 0.04   |
| Seagate   | ST9500424AS        | 500 GB | 3       | 100   | 674   | 0.04   |
| Seagate   | STM980215AS        | 80 GB  | 1       | 13    | 0     | 0.04   |
| Seagate   | ST310212A          | 10 GB  | 1       | 380   | 27    | 0.04   |
| WDC       | WD10SMRW-11Y43S0   | 1 TB   | 4       | 13    | 0     | 0.04   |
| WDC       | WD3200AAKX-073CA0  | 320 GB | 1       | 122   | 8     | 0.04   |
| Maxtor    | 6L160P0            | 160 GB | 7       | 25    | 4     | 0.04   |
| WDC       | WD5000AADS-98S9B1  | 500 GB | 1       | 120   | 8     | 0.04   |
| Toshiba   | MK3265GSXV         | 320 GB | 2       | 166   | 136   | 0.04   |
| WDC       | WD30EZRZ-60Z5HB0   | 3 TB   | 1       | 13    | 0     | 0.04   |
| Maxtor    | 6L300R0            | 304 GB | 3       | 15    | 7     | 0.04   |
| WDC       | WD10TMVV-11TK7S1   | 1 TB   | 3       | 212   | 30    | 0.04   |
| WDC       | WD180EDGZ-11B2DA0  | 18 TB  | 1       | 12    | 0     | 0.04   |
| WDC       | WD20SDZW-11JJ8S1   | 2 TB   | 1       | 12    | 0     | 0.04   |
| WDC       | WD800BB-00CAA1     | 80 GB  | 1       | 800   | 61    | 0.04   |
| WDC       | WD10EACS-22D6B1    | 1 TB   | 1       | 12    | 0     | 0.04   |
| Seagate   | ST500LT012-9WS142  | 500 GB | 269     | 370   | 1071  | 0.04   |
| Toshiba   | MK2565GSXV         | 250 GB | 3       | 197   | 24    | 0.03   |
| Seagate   | ST3320310CS        | 320 GB | 7       | 570   | 76    | 0.03   |
| Fujitsu   | MPG3204AT E        | 20 GB  | 1       | 138   | 10    | 0.03   |
| Seagate   | ST3250412CS        | 250 GB | 1       | 12    | 0     | 0.03   |
| WDC       | WD1602ABKS-18N8A0  | 160 GB | 1       | 111   | 8     | 0.03   |
| Samsung   | HM080HI            | 80 GB  | 4       | 395   | 378   | 0.03   |
| Seagate   | ST320LT012-9WS14C  | 320 GB | 62      | 269   | 1045  | 0.03   |
| WDC       | WD7500LPCX-22HWST0 | 752 GB | 1       | 129   | 10    | 0.03   |
| Maxtor    | 2F040L0            | 40 GB  | 5       | 22    | 5     | 0.03   |
| MaxDig... | MD3000GSA3257DVR 0 | 3 TB   | 1       | 11    | 0     | 0.03   |
| WDC       | WD800BB-00CAA0     | 80 GB  | 1       | 414   | 35    | 0.03   |
| Samsung   | HS030GB            | 32 GB  | 1       | 11    | 0     | 0.03   |
| Seagate   | ST9320421AS        | 320 GB | 5       | 456   | 51    | 0.03   |
| WDC       | WSH722020ALE6L0    | 20 TB  | 12      | 11    | 0     | 0.03   |
| Maxtor    | STM3320820A        | 320 GB | 1       | 11    | 0     | 0.03   |
| Maxtor    | 6L160M0            | 160 GB | 10      | 20    | 221   | 0.03   |
| MediaMax  | WL2000GSA6454G     | 2 TB   | 1       | 33    | 2     | 0.03   |
| Maxtor    | STM3160813AS       | 160 GB | 6       | 812   | 570   | 0.03   |
| Hitachi   | HDS721025CLA382... | 160 GB | 1       | 2614  | 237   | 0.03   |
| WDC       | WD5000AAKS-19V0A0  | 500 GB | 1       | 1131  | 103   | 0.03   |
| Maxtor    | 7L250S0            | 250 GB | 2       | 13    | 1     | 0.03   |
| Hitachi   | DK23CA-20          | 20 GB  | 1       | 93    | 8     | 0.03   |
| WDC       | WD20SPZX-60UA7T0   | 2 TB   | 4       | 10    | 0     | 0.03   |
| WDC       | WD400ABJS-23TEA0   | 40 GB  | 1       | 10    | 0     | 0.03   |
| Toshiba   | MK1214GAH          | 120 GB | 4       | 79    | 109   | 0.03   |
| WDC       | WD1600BUCT-63TWBY0 | 160 GB | 1       | 10    | 0     | 0.03   |
| WDC       | WD5000BEVT-55A0RT0 | 500 GB | 1       | 110   | 10    | 0.03   |
| Seagate   | ST500LM021-1KJ1... | 500 GB | 1       | 10    | 0     | 0.03   |
| Samsung   | HM161JJ            | 160 GB | 1       | 96    | 9     | 0.03   |
| Seagate   | ST1000DL004 HD1... | 1 TB   | 1       | 9     | 0     | 0.03   |
| WDC       | WD180PURZ-85AFFY0  | 18 TB  | 2       | 9     | 0     | 0.03   |
| Toshiba   | MK2016GAP          | 20 GB  | 1       | 349   | 36    | 0.03   |
| Maxtor    | 6L120M0            | 122 GB | 3       | 28    | 15    | 0.03   |
| Seagate   | ST9100828AS        | 100 GB | 1       | 9     | 0     | 0.03   |
| Maxtor    | 6Y120M0            | 122 GB | 5       | 33    | 42    | 0.02   |
| Samsung   | HD322IJ            | 320 GB | 1       | 469   | 51    | 0.02   |
| WDC       | WD800JD-75JNC0     | 80 GB  | 2       | 858   | 355   | 0.02   |
| WDC       | WD3200BEVT-80A0RT1 | 320 GB | 2       | 1035  | 140   | 0.02   |
| Seagate   | ST4000NM0053       | 4 TB   | 1       | 98    | 11    | 0.02   |
| Samsung   | HS12RJF            | 120 GB | 1       | 96    | 11    | 0.02   |
| Hitachi   | HTS548080M9AT00    | 80 GB  | 1       | 136   | 16    | 0.02   |
| ExcelStor | J9250              | 250 GB | 1       | 1349  | 167   | 0.02   |
| MediaMax  | WL250GLSA6410000   | 250 GB | 2       | 36    | 4     | 0.02   |
| Hitachi   | HTS723225L9A360    | 250 GB | 6       | 555   | 1012  | 0.02   |
| Maxtor    | 6E040L0            | 40 GB  | 14      | 30    | 28    | 0.02   |
| LENOVO    | WD1004FBYZ-23YC... | 1 TB   | 2       | 7     | 0     | 0.02   |
| WDC       | WD5000AZLX-00ZR6A0 | 500 GB | 1       | 7     | 0     | 0.02   |
| Maxtor    | 2F030J0            | 32 GB  | 3       | 32    | 96    | 0.02   |
| Hitachi   | HCC543232A7A380    | 320 GB | 1       | 30    | 3     | 0.02   |
| Maxtor    | 6Y120L0            | 122 GB | 7       | 28    | 15    | 0.02   |
| Maxtor    | 6Y060L2            | 64 GB  | 1       | 542   | 71    | 0.02   |
| MaxDig... | MDT MD2000KS-00... | 200 GB | 1       | 571   | 75    | 0.02   |
| Maxtor    | 6K040L0            | 41 GB  | 1       | 29    | 3     | 0.02   |
| Maxtor    | 7B300S0            | 304 GB | 1       | 244   | 32    | 0.02   |
| Hitachi   | DK23EA-20B         | 17 GB  | 1       | 183   | 24    | 0.02   |
| WDC       | WD2000JS-00NCB1    | 200 GB | 1       | 537   | 73    | 0.02   |
| Hitachi   | HTS722016K9SA00    | 160 GB | 1       | 591   | 81    | 0.02   |
| Seagate   | ST730212DE         | 32 GB  | 1       | 7     | 0     | 0.02   |
| Samsung   | HD254GJ            | 250 GB | 1       | 710   | 100   | 0.02   |
| Seagate   | ST4000NM0115-1Y... | 4 TB   | 3       | 7     | 0     | 0.02   |
| Maxtor    | 6E030L0            | 32 GB  | 5       | 15    | 19    | 0.02   |
| WDC       | WD2500AAJS-41RYA0  | 250 GB | 1       | 76    | 10    | 0.02   |
| Samsung   | SP1614N            | 160 GB | 2       | 837   | 120   | 0.02   |
| WDC       | WD10SPZX-16Z10T1   | 1 TB   | 1       | 6     | 0     | 0.02   |
| Maxtor    | 6L200S0            | 208 GB | 2       | 20    | 21    | 0.02   |
| Seagate   | ST8000DM004-2U9188 | 8 TB   | 4       | 6     | 0     | 0.02   |
| WDC       | WD5000LPZX-35Z10T0 | 500 GB | 2       | 6     | 0     | 0.02   |
| Fujitsu   | MHV2120BH PL       | 120 GB | 12      | 19    | 2     | 0.02   |
| WDC       | WD360ADFD-00NLR4   | 37 GB  | 1       | 499   | 77    | 0.02   |
| HPE       | MB004000GWWQH      | 4 TB   | 1       | 6     | 0     | 0.02   |
| WDC       | WD10SPZX-60Z10T1   | 1 TB   | 2       | 6     | 0     | 0.02   |
| Seagate   | ST94019A           | 40 GB  | 1       | 225   | 35    | 0.02   |
| HGST      | HTS725050A7E635... | 500 GB | 1       | 451   | 72    | 0.02   |
| HGST      | QC-FT-D H20GB-5... | 20 GB  | 1       | 6     | 0     | 0.02   |
| Seagate   | ST3500820AS        | 500 GB | 8       | 502   | 188   | 0.02   |
| Maxtor    | 6L300S0            | 304 GB | 8       | 21    | 238   | 0.02   |
| WDC       | WD2500BEVT-00SCST0 | 250 GB | 1       | 5     | 0     | 0.02   |
| Samsung   | HM100JI            | 100 GB | 1       | 827   | 140   | 0.02   |
| Hitachi   | HTS541612J9AT00    | 120 GB | 1       | 116   | 19    | 0.02   |
| WDC       | WD80EDBZ-11B0ZA0   | 8 TB   | 1       | 5     | 0     | 0.02   |
| MediaMax  | WL1500GSA3272      | 1.5 TB | 1       | 2210  | 391   | 0.02   |
| WDC       | WD5000LPSX-00A6WT0 | 500 GB | 1       | 5     | 0     | 0.02   |
| Toshiba   | MK5061GSY          | 500 GB | 8       | 10    | 17    | 0.01   |
| Maxtor    | 85400D5            | 5 GB   | 1       | 5613  | 1044  | 0.01   |
| WDC       | WD7500BMVW-11AJGS4 | 752 GB | 1       | 5     | 0     | 0.01   |
| Seagate   | ST1000LM002-9VQ14L | 1 TB   | 1       | 25    | 4     | 0.01   |
| Seagate   | ST4000VX005-2LY104 | 4 TB   | 3       | 5     | 0     | 0.01   |
| Maxtor    | 6Y080M0            | 80 GB  | 16      | 26    | 137   | 0.01   |
| WDC       | WD1200AAJS-00VTA0  | 120 GB | 1       | 995   | 203   | 0.01   |
| WDC       | WD5000LPVX-28V0TT1 | 500 GB | 1       | 134   | 27    | 0.01   |
| Seagate   | ST2000DM008-2UB102 | 2 TB   | 2       | 4     | 0     | 0.01   |
| Hitachi   | HTE721060G9AT00    | 64 GB  | 1       | 4     | 0     | 0.01   |
| Toshiba   | MK1676GSX          | 160 GB | 2       | 16    | 447   | 0.01   |
| Toshiba   | MK8050GAC          | 80 GB  | 1       | 878   | 197   | 0.01   |
| Maxtor    | 6L080P0            | 82 GB  | 3       | 11    | 10    | 0.01   |
| Maxtor    | 4R060J0            | 64 GB  | 1       | 25    | 5     | 0.01   |
| Fujitsu   | MHZ2160BJ G1       | 160 GB | 1       | 4     | 0     | 0.01   |
| Seagate   | ST9250421AS        | 250 GB | 1       | 539   | 136   | 0.01   |
| WDC       | WD2500BEKT-66F3T2  | 250 GB | 1       | 193   | 50    | 0.01   |
| WDC       | WD6003FZBX-00GXAB0 | 6 TB   | 1       | 3     | 0     | 0.01   |
| WDC       | WD140EDGZ-11B1PA0  | 14 TB  | 4       | 3     | 0     | 0.01   |
| Hitachi   | HCS721050CLA362    | 500 GB | 1       | 3     | 0     | 0.01   |
| Toshiba   | MK6028GAL          | 64 GB  | 1       | 3     | 0     | 0.01   |
| Seagate   | ST3750630AS        | 752 GB | 4       | 697   | 791   | 0.01   |
| Seagate   | ST3250310SV        | 250 GB | 1       | 287   | 79    | 0.01   |
| WDC       | WD1600BB-55GUC0    | 160 GB | 1       | 332   | 94    | 0.01   |
| Fujitsu   | MJA2320BH G1       | 320 GB | 1       | 800   | 230   | 0.01   |
| Maxtor    | 6Y160P0            | 163 GB | 6       | 21    | 121   | 0.01   |
| Hitachi   | HTS541640J9AT00    | 40 GB  | 1       | 283   | 82    | 0.01   |
| HGST      | HTS725050A7E635    | 500 GB | 2       | 490   | 557   | 0.01   |
| Maxtor    | 6B250S0            | 250 GB | 2       | 20    | 471   | 0.01   |
| WDC       | WD10EADS-00R6B0    | 1 TB   | 1       | 1856  | 560   | 0.01   |
| Fujitsu   | MPE3136AT          | 16 GB  | 1       | 794   | 240   | 0.01   |
| Apple     | HDD HTS547575A9... | 752 GB | 1       | 506   | 153   | 0.01   |
| Maxtor    | 6Y080P0            | 82 GB  | 7       | 16    | 7     | 0.01   |
| Maxtor    | 6E020L0            | 21 GB  | 1       | 22    | 6     | 0.01   |
| IBM/Hi... | IC35L060AVER07-0   | 64 GB  | 2       | 546   | 167   | 0.01   |
| Seagate   | ST6000NE0021-2E... | 6 TB   | 1       | 3     | 0     | 0.01   |
| WDC       | WUH721816ALE6L0    | 16 TB  | 1       | 3     | 0     | 0.01   |
| WDC       | WD2004FBYZ-01YCBB0 | 2 TB   | 1       | 12    | 3     | 0.01   |
| WDC       | TP00250GB          | 250 GB | 1       | 1073  | 351   | 0.01   |
| Seagate   | ST3320820A         | 320 GB | 1       | 641   | 210   | 0.01   |
| Maxtor    | 6B160M0            | 163 GB | 1       | 3     | 0     | 0.01   |
| Seagate   | ST8000NM0105       | 8 TB   | 2       | 2     | 0     | 0.01   |
| WDC       | WD5000LPZX-60Z10T0 | 500 GB | 3       | 2     | 0     | 0.01   |
| WDC       | WD800UE-22HCT0     | 80 GB  | 2       | 568   | 272   | 0.01   |
| Toshiba   | MK1655GSXF         | 160 GB | 2       | 581   | 511   | 0.01   |
| Toshiba   | MAL2040SA-T54L     | 40 GB  | 1       | 2     | 0     | 0.01   |
| WDC       | WD10SPSX-75A6WT0   | 1 TB   | 1       | 2     | 0     | 0.01   |
| Maxtor    | 6Y120P0            | 122 GB | 3       | 21    | 28    | 0.01   |
| Seagate   | ST3160316CS        | 160 GB | 2       | 107   | 20    | 0.01   |
| WDC       | WD1200BEVS-75LAT0  | 118 GB | 1       | 1008  | 378   | 0.01   |
| Seagate   | ST500LM020-1G1162  | 500 GB | 3       | 2     | 0     | 0.01   |
| WDC       | WD15SMZW-11YFCS0   | 1.5 TB | 1       | 2     | 0     | 0.01   |
| Samsung   | SV0802N            | 80 GB  | 1       | 554   | 215   | 0.01   |
| WDC       | RFT030VQFF-KRM5P7  | 3 TB   | 1       | 129   | 50    | 0.01   |
| Seagate   | ST500NM0011 39M... | 500 GB | 1       | 2520  | 1007  | 0.01   |
| WDC       | WD101EFBX-68B0AN0  | 10 TB  | 1       | 2     | 0     | 0.01   |
| WDC       | WD3200AADS-00S9B0  | 320 GB | 1       | 26    | 10    | 0.01   |
| Maxtor    | 6Y200P0            | 208 GB | 2       | 20    | 9     | 0.01   |
| WDC       | WD10EZEX-60WN4A2   | 1 TB   | 1       | 2     | 0     | 0.01   |
| Maxtor    | 6Y080L0            | 80 GB  | 44      | 20    | 292   | 0.01   |
| Seagate   | OOS1000G128M       | 1 TB   | 1       | 39    | 18    | 0.01   |
| MARSHAL   | MAL2020SA 80       | 20 GB  | 1       | 4     | 1     | 0.01   |
| Hitachi   | HDS722516VLAT20    | 164 GB | 1       | 2242  | 1102  | 0.01   |
| WDC       | WD10SDRW-34A0XS0   | 1 TB   | 1       | 1     | 0     | 0.01   |
| WDC       | WD6400AAKS-00E4A0  | 640 GB | 1       | 1016  | 521   | 0.01   |
| WDC       | WD10EURX-63UHWY0   | 1 TB   | 1       | 644   | 338   | 0.01   |
| WDC       | WD4000AAKS-22TMA0  | 400 GB | 1       | 820   | 431   | 0.01   |
| WDC       | WD20EZBX-08AYR     | 2 TB   | 1       | 1     | 0     | 0.01   |
| Seagate   | ST9320423ASG       | 320 GB | 1       | 270   | 145   | 0.01   |
| Samsung   | HM160JI            | 160 GB | 6       | 304   | 1043  | 0.01   |
| HGST      | MB3000EBUCH        | 3 TB   | 1       | 745   | 406   | 0.01   |
| WDC       | WD20EARS-19MVWB0   | 2 TB   | 1       | 713   | 392   | 0.00   |
| Fujitsu   | MHY2080BS          | 80 GB  | 1       | 2382  | 1317  | 0.00   |
| WDC       | WD400ZB-00JYA0     | 40 GB  | 1       | 927   | 520   | 0.00   |
| Toshiba   | MK2533GSG          | 250 GB | 1       | 1671  | 948   | 0.00   |
| Hitachi   | HUA5C3020ALA640    | 2 TB   | 1       | 1045  | 595   | 0.00   |
| WDC       | WD1600BEKT-75PVMT0 | 160 GB | 1       | 1003  | 580   | 0.00   |
| Seagate   | ST5000AS0011-1L... | 5 TB   | 1       | 1743  | 1015  | 0.00   |
| CLOVER    | CD155UI            | 1.5 TB | 1       | 1     | 0     | 0.00   |
| IBM/Hi... | IC35L120AVVA07-0   | 128 GB | 1       | 918   | 552   | 0.00   |
| WDC       | WD140PURZ-85GG1Y0  | 14 TB  | 4       | 1     | 0     | 0.00   |
| Maxtor    | 2F020J0            | 21 GB  | 2       | 21    | 45    | 0.00   |
| WDC       | WD7501AAES-60Z2A0  | 752 GB | 1       | 1058  | 666   | 0.00   |
| Samsung   | HD251KJ            | 250 GB | 1       | 1539  | 1019  | 0.00   |
| Seagate   | ST3120023AS        | 120 GB | 1       | 152   | 101   | 0.00   |
| WDC       | WD3200AAKX-00U6AA0 | 320 GB | 1       | 83    | 56    | 0.00   |
| Samsung   | HN-M500XBB         | 500 GB | 1       | 1     | 0     | 0.00   |
| Hitachi   | HUA722010CLA330... | 1 TB   | 1       | 161   | 112   | 0.00   |
| WDC       | WD181KFGX-68AFPN0  | 18 TB  | 6       | 1     | 0     | 0.00   |
| WDC       | WD2500JD-98GBB0    | 250 GB | 1       | 875   | 628   | 0.00   |
| Maxtor    | 2B020H1            | 20 GB  | 12      | 23    | 194   | 0.00   |
| Maxtor    | 4R160L0            | 163 GB | 1       | 5     | 3     | 0.00   |
| WDC       | WD2500AAJS-40VWA1  | 250 GB | 1       | 999   | 759   | 0.00   |
| Seagate   | ST8000NC0002-1X... | 8 TB   | 1       | 107   | 82    | 0.00   |
| WDC       | WD15EADS-11P8B1    | 1.5 TB | 2       | 908   | 934   | 0.00   |
| WDC       | WD3200LPCX-60VHAT0 | 320 GB | 1       | 1     | 0     | 0.00   |
| WDC       | WUS721010ALE6L4    | 10 TB  | 1       | 1     | 0     | 0.00   |
| Fujitsu   | MHT2060AT          | 64 GB  | 1       | 302   | 241   | 0.00   |
| WDC       | WD1200             | 120 GB | 1       | 11    | 8     | 0.00   |
| Toshiba   | MK4026GAX          | 40 GB  | 1       | 191   | 157   | 0.00   |
| Hitachi   | HCS5C1050DLE630    | 500 GB | 1       | 885   | 737   | 0.00   |
| Toshiba   | MK7559GSM          | 752 GB | 1       | 1015  | 847   | 0.00   |
| WDC       | WD400BB-00CAA0     | 40 GB  | 1       | 194   | 163   | 0.00   |
| Maxtor    | 4D040H2            | 41 GB  | 4       | 16    | 188   | 0.00   |
| Seagate   | ST9320327AS        | 320 GB | 1       | 725   | 705   | 0.00   |
| Toshiba   | MK3256GSY          | 320 GB | 6       | 5     | 542   | 0.00   |
| WDC       | WD2003FYPS-27W9B0  | 2 TB   | 1       | 523   | 529   | 0.00   |
| Hitachi   | HTS723216L9A360    | 160 GB | 7       | 471   | 1413  | 0.00   |
| Fujitsu   | MHV2160BT          | 160 GB | 1       | 483   | 535   | 0.00   |
| Seagate   | ST9160418ASG       | 160 GB | 1       | 555   | 625   | 0.00   |
| Hitachi   | HTS725032A9A365    | 320 GB | 2       | 859   | 1023  | 0.00   |
| WDC       | RAT015VQHB-DSG2D7  | 1.5 TB | 1       | 0     | 0     | 0.00   |
| WDC       | RFT030VQHR-GTK4D   | 3 TB   | 1       | 0     | 0     | 0.00   |
| Maxtor    | 4R120L0            | 122 GB | 3       | 30    | 39    | 0.00   |
| HGST      | TPH00100500GB 0... | 500 GB | 1       | 8     | 10    | 0.00   |
| HP        | GB1000EAFJL        | 1 TB   | 1       | 2402  | 3024  | 0.00   |
| WDC       | WD800BEVT-26ZCT0   | 80 GB  | 1       | 0     | 0     | 0.00   |
| Maxtor    | 4G120J6            | 122 GB | 2       | 20    | 218   | 0.00   |
| Maxtor    | 6Y060L0            | 64 GB  | 5       | 23    | 84    | 0.00   |
| Maxtor    | STM3750330AS       | 752 GB | 1       | 995   | 1293  | 0.00   |
| MediaMax  | WL400GSA6454G      | 400 GB | 1       | 0     | 0     | 0.00   |
| WDC       | WD3200LPCX-22VHAT0 | 320 GB | 1       | 0     | 0     | 0.00   |
| Fujitsu   | MHV2200BT          | 200 GB | 1       | 382   | 518   | 0.00   |
| Apple     | HDD HUA722010CL... | 1 TB   | 1       | 83    | 113   | 0.00   |
| Maxtor    | 7Y250M0            | 250 GB | 2       | 25    | 38    | 0.00   |
| Seagate   | ST3320620SV        | 320 GB | 1       | 564   | 835   | 0.00   |
| Seagate   | ST500LT015-9WU142  | 500 GB | 2       | 708   | 1108  | 0.00   |
| Seagate   | ST4000NM0265-2D... | 4 TB   | 1       | 0     | 0     | 0.00   |
| Seagate   | ST3320410SV        | 320 GB | 1       | 685   | 1110  | 0.00   |
| Seagate   | ST960822A          | 64 GB  | 1       | 246   | 400   | 0.00   |
| Seagate   | ST500DM009-1BD142  | 500 GB | 1       | 0     | 0     | 0.00   |
| Maxtor    | 4D060H3            | 64 GB  | 1       | 18    | 31    | 0.00   |
| Hitachi   | DK23CA-30          | 32 GB  | 1       | 532   | 919   | 0.00   |
| Maxtor    | 6Y160M0            | 160 GB | 6       | 20    | 195   | 0.00   |
| HGST      | HUS728T8TALE6L0    | 8 TB   | 3       | 0     | 0     | 0.00   |
| WDC       | WD15EARS-19MVWB0   | 1.5 TB | 1       | 696   | 1306  | 0.00   |
| Hitachi   | HTS723212L9A360    | 120 GB | 1       | 535   | 1012  | 0.00   |
| Hitachi   | HTS723232A7A365    | 320 GB | 1       | 1130  | 2203  | 0.00   |
| Seagate   | ST10000NM001G-2... | 10 TB  | 4       | 0     | 0     | 0.00   |
| Seagate   | ST250LT012-1DG141  | 250 GB | 1       | 500   | 1007  | 0.00   |
| Fujitsu   | MHK2120AT          | 12 GB  | 1       | 77    | 155   | 0.00   |
| Seagate   | ST3250311SV        | 250 GB | 2       | 486   | 1035  | 0.00   |
| WDC       | WD15EURS-63S48Y0   | 1.5 TB | 1       | 11    | 26    | 0.00   |
| WDC       | WD2500BB-22RDA0    | 250 GB | 1       | 655   | 1524  | 0.00   |
| Seagate   | ST320LT000-9VL142  | 320 GB | 2       | 402   | 1009  | 0.00   |
| Seagate   | ST3802110ACE       | 80 GB  | 1       | 1203  | 3052  | 0.00   |
| Hitachi   | HDP725040GLA380    | 400 GB | 1       | 215   | 554   | 0.00   |
| Samsung   | HM500LX            | 500 GB | 2       | 133   | 293   | 0.00   |
| Hitachi   | HTS725050A7E635    | 500 GB | 2       | 429   | 1165  | 0.00   |
| Seagate   | ST3500321CS        | 500 GB | 1       | 48    | 137   | 0.00   |
| MARSHAL   | MAL2500SA-T54L     | 500 GB | 1       | 90    | 262   | 0.00   |
| WDC       | WD3200L22X-00JVPT0 | 320 GB | 1       | 0     | 0     | 0.00   |
| Maxtor    | 7L300S0            | 304 GB | 3       | 13    | 40    | 0.00   |
| WDC       | WD2500BEKT-60F3T1  | 250 GB | 1       | 533   | 1607  | 0.00   |
| WDC       | WD5000BEVT-60ZAT0  | 500 GB | 1       | 381   | 1160  | 0.00   |
| Seagate   | ST250LT012-9WS141  | 250 GB | 4       | 337   | 1077  | 0.00   |
| Samsung   | HD402LJ            | 400 GB | 1       | 315   | 1018  | 0.00   |
| Seagate   | ST980817AS         | 80 GB  | 1       | 310   | 1009  | 0.00   |
| WDC       | WD2500AAKS-60L9A0  | 250 GB | 1       | 282   | 937   | 0.00   |
| WDC       | WD1600AAJS-56WAA0  | 160 GB | 1       | 299   | 1021  | 0.00   |
| WDC       | WD5000L            | 500 GB | 1       | 88    | 302   | 0.00   |
| WDC       | WD20EZRX-00SPEB0   | 2 TB   | 1       | 574   | 2072  | 0.00   |
| Seagate   | ST3640623AS        | 640 GB | 1       | 55    | 209   | 0.00   |
| Hitachi   | HTS542580K9A300    | 80 GB  | 2       | 267   | 1012  | 0.00   |
| Seagate   | ST9320312AS        | 320 GB | 2       | 264   | 1108  | 0.00   |
| WDC       | WD5000AAVS-00G9B1  | 500 GB | 1       | 257   | 1020  | 0.00   |
| Samsung   | SV2011H            | 20 GB  | 1       | 0     | 3     | 0.00   |
| WDC       | WD2500AAJS-55B4A0  | 250 GB | 1       | 476   | 2020  | 0.00   |
| Toshiba   | MK2555GSX H        | 250 GB | 1       | 428   | 1908  | 0.00   |
| WDC       | WD800 AAJS-00PSA0  | 80 GB  | 1       | 97    | 459   | 0.00   |
| Seagate   | ST1000LM014-1EJ... | 1 TB   | 1       | 202   | 1009  | 0.00   |
| Fujitsu   | MHT2060BH          | 64 GB  | 1       | 407   | 2048  | 0.00   |
| China     | Generic S050 Ha... | 500 GB | 1       | 245   | 1377  | 0.00   |
| Maxtor    | 6B120P0            | 122 GB | 1       | 0     | 0     | 0.00   |
| Seagate   | ST4000NC000-1FR168 | 4 TB   | 1       | 0     | 0     | 0.00   |
| Toshiba   | MK6461GSYN         | 640 GB | 1       | 0     | 0     | 0.00   |
| WDC       | WD2005FBYZ-01YCBB1 | 2 TB   | 1       | 0     | 0     | 0.00   |
| WDC       | WD450VF4YZ-49SJYM0 | 4.5 TB | 1       | 0     | 0     | 0.00   |
| WDC       | WD50NDZW-11A8JS0   | 5 TB   | 1       | 0     | 0     | 0.00   |
| Samsung   | HM320JX            | 320 GB | 1       | 37    | 331   | 0.00   |
| Seagate   | ST980829A          | 80 GB  | 1       | 222   | 2022  | 0.00   |
| Seagate   | MB0500EAMZD        | 500 GB | 1       | 94    | 857   | 0.00   |
| Maxtor    | 7L300R0            | 304 GB | 1       | 11    | 116   | 0.00   |
| China     | TPH00800640GB 0    | 640 GB | 1       | 82    | 1007  | 0.00   |
| Toshiba   | MK8025GAL          | 80 GB  | 1       | 78    | 1017  | 0.00   |
| WDC       | WD3200A            | 320 GB | 1       | 137   | 2074  | 0.00   |
| Seagate   | ST3500630NS Q      | 500 GB | 1       | 201   | 3060  | 0.00   |
| Samsung   | HS122JC            | 120 GB | 1       | 188   | 3047  | 0.00   |
| Maxtor    | 6L250R0            | 250 GB | 1       | 2     | 45    | 0.00   |
| Maxtor    | 53073H6            | 32 GB  | 1       | 121   | 2068  | 0.00   |
| WDC       | WD20EADS-22R6B0    | 2 TB   | 1       | 105   | 1848  | 0.00   |
| Hitachi   | HTS548060M9AT00    | 64 GB  | 1       | 35    | 655   | 0.00   |
| Seagate   | ST330630A          | 32 GB  | 1       | 103   | 2102  | 0.00   |
| WDC       | WD60PURX-64T0ZY1   | 6 TB   | 1       | 0     | 0     | 0.00   |
| Maxtor    | 32049H2            | 20 GB  | 1       | 8     | 396   | 0.00   |
| Seagate   | ST380020A          | 80 GB  | 1       | 2     | 225   | 0.00   |
| Fujitsu   | MHZ2160BJ G2       | 160 GB | 1       | 6     | 1025  | 0.00   |
| Samsung   | HS06THB            | 64 GB  | 1       | 2     | 2087  | 0.00   |
| Hitachi   | HTS721060G9AT00    | 64 GB  | 1       | 0     | 37    | 0.00   |

HDD by Family
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG       | Family                 | Models | Samples | Days  | Err   | MTBF |
|-----------|------------------------|--------|---------|-------|-------|------|
| Samsung   | SpinPoint M40S         | 1      | 2       | 6601  | 0     | 18.09  |
| Samsung   | SpinPoint V20400       | 1      | 1       | 5713  | 0     | 15.65  |
| HP        | Seagate Barracuda 7... | 1      | 2       | 3447  | 0     | 9.44   |
| Hitachi   | Sun Original           | 2      | 13      | 2735  | 0     | 7.49   |
| Hitachi   | Deskstar 7K4000        | 1      | 8       | 2332  | 171   | 6.14   |
| Seagate   | Barracuda ES+          | 2      | 2       | 2199  | 0     | 6.03   |
| Fujitsu   | MHZ BK                 | 1      | 1       | 2159  | 0     | 5.92   |
| Hitachi   | Deskstar 7K250 (SUN... | 1      | 1       | 5248  | 2     | 4.79   |
| Hitachi   | Ultrastar A7K1000      | 5      | 25      | 2197  | 80    | 4.66   |
| Samsung   | SpinPoint PL40         | 1      | 2       | 3755  | 9     | 4.62   |
| Seagate   | SpinPoint F4 EG (AF)   | 1      | 3       | 1617  | 0     | 4.43   |
| Seagate   | Barracuda 7200.7       | 1      | 5       | 1809  | 42    | 4.22   |
| Seagate   | Constellation.2 (SATA) | 3      | 28      | 1711  | 2     | 4.22   |
| HPE       | WDC Enterprise         | 1      | 1       | 1526  | 0     | 4.18   |
| Quantum   | Unknown                | 1      | 1       | 1486  | 0     | 4.07   |
| WDC       | Caviar WDxxxAA         | 2      | 2       | 1697  | 6     | 4.03   |
| Seagate   | Exos X12               | 1      | 1       | 1335  | 0     | 3.66   |
| Maxtor    | DiamondMax 11          | 1      | 1       | 1294  | 0     | 3.55   |
| Seagate   | Seagate Enterprise     | 1      | 4       | 1290  | 0     | 3.54   |
| HGST      | Ultrastar 7K4000       | 6      | 105     | 1304  | 20    | 3.50   |
| HP        | Seagate Constellati... | 1      | 1       | 1272  | 0     | 3.49   |
| Hitachi   | Deskstar 7K2000        | 2      | 44      | 1818  | 81    | 3.41   |
| WDC       | RE2                    | 8      | 19      | 1457  | 33    | 3.35   |
| Toshiba   | Unknown                | 5      | 6       | 1232  | 191   | 3.31   |
| HP        | Constellation ES.3     | 1      | 3       | 1181  | 0     | 3.24   |
| Seagate   | Archive HDD            | 3      | 115     | 1370  | 71    | 3.23   |
| Seagate   | Exos 7E2               | 5      | 31      | 1220  | 12    | 3.22   |
| Maxtor    | DiamondMax 8s          | 1      | 2       | 1842  | 1     | 3.21   |
| Hitachi   | Ultrastar A7K2000      | 11     | 80      | 1673  | 47    | 3.19   |
| WDC       | Raptor X               | 1      | 1       | 1164  | 0     | 3.19   |
| Toshiba   | 1.8" HDD MK..17GSG     | 1      | 1       | 1162  | 0     | 3.18   |
| Samsung   | SpinPoint F3R          | 1      | 1       | 1143  | 0     | 3.13   |
| WDC       | RE3                    | 21     | 103     | 1488  | 9     | 3.11   |
| Hitachi   | Deskstar 7K500         | 2      | 11      | 1768  | 7     | 3.09   |
| Hitachi   | Deskstar 7K3000        | 8      | 102     | 1249  | 62    | 3.00   |
| Seagate   | NAS HDD                | 8      | 67      | 1123  | 33    | 2.87   |
| Hitachi   | Unknown                | 2      | 5       | 1330  | 3     | 2.87   |
| Hitachi   | CinemaStar C5K500      | 2      | 3       | 1041  | 0     | 2.85   |
| Apple     | Travelstar 7K750       | 1      | 3       | 1036  | 0     | 2.84   |
| WDC       | RE4-GP                 | 6      | 20      | 1563  | 54    | 2.82   |
| Hitachi   | CinemaStar P7K500      | 4      | 7       | 1243  | 3     | 2.80   |
| WDC       | Purple NV              | 1      | 1       | 1023  | 0     | 2.80   |
| Hitachi   | CinemaStar 5K1000      | 4      | 9       | 1081  | 1     | 2.80   |
| Toshiba   | 3.5" HDD               | 1      | 1       | 1008  | 0     | 2.76   |
| Hitachi   | Ultrastar 7K3000       | 4      | 111     | 1143  | 41    | 2.75   |
| HGST      | Deskstar NAS           | 9      | 81      | 1058  | 37    | 2.72   |
| HP        | Proliant HardDrive     | 11     | 22      | 1368  | 24    | 2.72   |
| Apple     | Seagate Barracuda 7... | 1      | 2       | 985   | 0     | 2.70   |
| Samsung   | SpinPoint F4 EG (AF)   | 2      | 72      | 1213  | 96    | 2.65   |
| Seagate   | Constellation.2        | 3      | 3       | 958   | 0     | 2.63   |
| HGST      | Unknown                | 5      | 5       | 1070  | 10    | 2.60   |
| Seagate   | U5                     | 4      | 7       | 992   | 2     | 2.56   |
| Seagate   | Laptop Thin            | 1      | 2       | 932   | 0     | 2.56   |
| Toshiba   | 3.5" HDD MK.002TSKB    | 2      | 4       | 1355  | 8     | 2.55   |
| WDC       | Caviar SE16            | 6      | 45      | 1175  | 15    | 2.54   |
| WDC       | VelociRaptor           | 35     | 106     | 1075  | 13    | 2.53   |
| Toshiba   | 3.5" MD04ACA Enterp... | 2      | 30      | 1078  | 142   | 2.52   |
| Hitachi   | CinemaStar 5K2000      | 1      | 2       | 2125  | 6     | 2.49   |
| WDC       | Caviar Black           | 53     | 639     | 1194  | 39    | 2.46   |
| Seagate   | Enterprise NAS HDD     | 2      | 4       | 896   | 0     | 2.46   |
| WDC       | Se                     | 6      | 20      | 1059  | 6     | 2.43   |
| Seagate   | Desktop HDD.15         | 5      | 175     | 1013  | 117   | 2.38   |
| Hitachi   | Deskstar 5K3000        | 5      | 45      | 1140  | 51    | 2.36   |
| Seagate   | Momentus Xt            | 1      | 2       | 1073  | 16    | 2.34   |
| Quantum   | Fireball Plus AS       | 2      | 2       | 845   | 0     | 2.32   |
| Toshiba   | 3.5" DT01ABA Deskto... | 3      | 28      | 870   | 1     | 2.32   |
| Hitachi   | CinemaStar C5K750      | 1      | 1       | 844   | 0     | 2.31   |
| Seagate   | Constellation CS       | 4      | 22      | 1051  | 182   | 2.28   |
| HGST      | MegaScale 4000         | 2      | 18      | 830   | 0     | 2.28   |
| Seagate   | Barracuda XT           | 4      | 30      | 1099  | 163   | 2.27   |
| HP        | RE3                    | 1      | 2       | 814   | 0     | 2.23   |
| Hitachi   | CinemaStar 5K320       | 2      | 7       | 976   | 2     | 2.23   |
| HGST      | CinemaStar Z7K500      | 1      | 1       | 810   | 0     | 2.22   |
| Hitachi   | Deskstar 7K250         | 8      | 19      | 1419  | 196   | 2.21   |
| Seagate   | Desktop HDD            | 1      | 2       | 801   | 0     | 2.20   |
| Hitachi   | Deskstar 7K1000        | 3      | 24      | 1277  | 14    | 2.17   |
| Hitachi   | Deskstar T7K500        | 8      | 82      | 1224  | 54    | 2.15   |
| Toshiba   | 3.5" MG03ACAxxx(Y) ... | 4      | 31      | 895   | 2     | 2.15   |
| HP        | 250GB SATA disk VB0... | 1      | 17      | 1164  | 4     | 2.10   |
| WDC       | RE                     | 30     | 97      | 1107  | 57    | 2.07   |
| Apple     | Seagate Samsung Spi... | 1      | 3       | 735   | 0     | 2.01   |
| WDC       | RE4                    | 26     | 178     | 998   | 25    | 2.01   |
| Seagate   | Constellation ES.3     | 7      | 96      | 1061  | 172   | 2.01   |
| Samsung   | SpinPoint F3 RE        | 1      | 3       | 2260  | 41    | 2.00   |
| Seagate   | Barracuda 7200.8       | 9      | 54      | 1317  | 79    | 1.95   |
| Toshiba   | MG04ACA Enterprise HDD | 1      | 1       | 711   | 0     | 1.95   |
| Seagate   | Constellation ES.2 ... | 4      | 20      | 1157  | 78    | 1.94   |
| Samsung   | SpinPoint F1 RE        | 2      | 3       | 824   | 34    | 1.90   |
| Seagate   | U9                     | 3      | 7       | 690   | 0     | 1.89   |
| WDC       | Caviar Green           | 166    | 2359    | 1038  | 71    | 1.89   |
| WDC       | Raptor                 | 16     | 29      | 1216  | 13    | 1.87   |
| Seagate   | Constellation ES (S... | 3      | 46      | 1458  | 36    | 1.86   |
| Hitachi   | Deskstar 5K1000        | 3      | 30      | 869   | 54    | 1.85   |
| Seagate   | DB35.3                 | 7      | 22      | 825   | 203   | 1.83   |
| WDC       | Red                    | 34     | 1077    | 796   | 10    | 1.82   |
| HGST      | Travelstar 5K1500      | 2      | 7       | 905   | 152   | 1.82   |
| Maxtor    | DiamondMax VL15        | 1      | 1       | 1326  | 1     | 1.82   |
| Seagate   | Barracuda Pro          | 1      | 3       | 662   | 0     | 1.82   |
| Samsung   | SpinPoint              | 7      | 13      | 774   | 47    | 1.81   |
| Seagate   | Barracuda ES           | 8      | 52      | 1245  | 398   | 1.81   |
| Seagate   | Constellation ES (S... | 4      | 42      | 1160  | 139   | 1.81   |
| Seagate   | Barracuda Green (AF)   | 4      | 245     | 992   | 213   | 1.80   |
| WDC       | Caviar SE              | 167    | 630     | 948   | 30    | 1.79   |
| Samsung   | SpinPoint F3           | 6      | 355     | 896   | 45    | 1.79   |
| Toshiba   | 2.5" HDD MQ01UBB       | 1      | 8       | 832   | 260   | 1.78   |
| IBM/Hi... | Deskstar GXP-180       | 4      | 8       | 1315  | 18    | 1.78   |
| Hitachi   | Ultrastar 7K4000       | 4      | 47      | 699   | 35    | 1.75   |
| Hitachi   | Deskstar 7K1000.B      | 11     | 147     | 1076  | 54    | 1.74   |
| Maxtor    | MaXLine III (SATA/300) | 2      | 4       | 1049  | 238   | 1.73   |
| WDC       | WDC Enterprise         | 3      | 3       | 625   | 0     | 1.71   |
| HGST      | Ultrastar 7K6000       | 12     | 47      | 645   | 13    | 1.71   |
| HGST      | Deskstar 7K4000        | 2      | 8       | 1035  | 253   | 1.68   |
| HGST      | Ultrastar He8          | 4      | 39      | 909   | 3     | 1.68   |
| Toshiba   | 3.5" HDD DT01ABA..V    | 4      | 14      | 885   | 135   | 1.68   |
| Hitachi   | Deskstar 5K4000        | 1      | 5       | 612   | 0     | 1.68   |
| Maxtor    | DiamondMax Plus D740X  | 3      | 6       | 1114  | 4     | 1.68   |
| Hitachi   | Deskstar 7K1000.C      | 16     | 684     | 886   | 64    | 1.67   |
| Hitachi   | Deskstar 7K80          | 6      | 89      | 860   | 30    | 1.67   |
| Samsung   | SpinPoint T133         | 5      | 27      | 968   | 132   | 1.66   |
| Seagate   | DB35.2                 | 2      | 5       | 1201  | 476   | 1.65   |
| HP        | Unknown                | 4      | 4       | 927   | 3     | 1.64   |
| Seagate   | Enterprise Capacity... | 18     | 126     | 714   | 25    | 1.62   |
| Apple     | SpinPoint              | 1      | 1       | 589   | 0     | 1.61   |
| Toshiba   | 2.5" HDD MQ01ABF..H    | 1      | 3       | 730   | 42    | 1.60   |
| WDC       | Black                  | 27     | 381     | 670   | 21    | 1.60   |
| Quantum   | Fireball               | 2      | 2       | 579   | 0     | 1.59   |
| Maxtor    | MaXLine Pro 500        | 1      | 5       | 648   | 1     | 1.58   |
| Seagate   | Pipeline HD 5900.2     | 9      | 163     | 861   | 129   | 1.58   |
| Hitachi   | CinemaStar 7K500       | 1      | 1       | 573   | 0     | 1.57   |
| Toshiba   | 3.5" HDD E300          | 2      | 11      | 571   | 0     | 1.57   |
| WDC       | AV-GP                  | 51     | 216     | 819   | 46    | 1.56   |
| WDC       | Green                  | 7      | 159     | 640   | 1     | 1.56   |
| Seagate   | Barracuda 7200.10      | 35     | 1561    | 950   | 268   | 1.55   |
| Toshiba   | 2.5" HDD MQ03ABB       | 2      | 4       | 564   | 0     | 1.55   |
| Samsung   | SpinPoint F2 EG        | 3      | 211     | 997   | 266   | 1.53   |
| Seagate   | Momentus 5400.7        | 2      | 12      | 807   | 327   | 1.53   |
| Hitachi   | Deskstar E7K500        | 2      | 2       | 559   | 0     | 1.53   |
| Fujitsu   | MPA..MPG               | 5      | 6       | 711   | 42    | 1.53   |
| Toshiba   | 2.5" HDD MQ01ABB       | 1      | 20      | 695   | 168   | 1.49   |
| Seagate   | SpinPoint D8X          | 1      | 4       | 619   | 202   | 1.44   |
| Samsung   | SpinPoint F1 DT        | 12     | 468     | 1028  | 186   | 1.44   |
| Apple     | Barracuda              | 1      | 27      | 524   | 0     | 1.44   |
| Hitachi   | Deskstar T7K250        | 5      | 45      | 1017  | 69    | 1.40   |
| Seagate   | Video 3.5 HDD          | 10     | 72      | 628   | 134   | 1.40   |
| Toshiba   | 2.5" HDD MK..32GSX     | 2      | 7       | 526   | 1     | 1.39   |
| Maxtor    | DiamondMax 10 (SATA... | 6      | 42      | 757   | 27    | 1.37   |
| Samsung   | SpinPoint F3 EG        | 4      | 50      | 727   | 85    | 1.37   |
| Seagate   | Barracuda 7200.7 an... | 19     | 670     | 884   | 88    | 1.36   |
| Hitachi   | Deskstar P7K500        | 11     | 218     | 1020  | 78    | 1.36   |
| Seagate   | Surveillance           | 10     | 37      | 513   | 32    | 1.35   |
| Apple     | Barracuda 7200.12      | 1      | 4       | 488   | 0     | 1.34   |
| Seagate   | Desktop SSHD           | 9      | 156     | 651   | 62    | 1.33   |
| WDC       | RE2-GP                 | 3      | 3       | 544   | 2     | 1.33   |
| Seagate   | Barracuda 5400.1       | 1      | 5       | 835   | 33    | 1.32   |
| HGST      | Ultrastar He10         | 4      | 37      | 540   | 1     | 1.32   |
| HGST      | Ultrastar 7K2          | 3      | 16      | 478   | 0     | 1.31   |
| Apple     | Travelstar 5K1000      | 4      | 57      | 614   | 94    | 1.31   |
| Seagate   | Barracuda 7200.14 (AF) | 27     | 3347    | 657   | 120   | 1.31   |
| WDC       | Caviar Blue            | 348    | 5058    | 688   | 41    | 1.30   |
| Hitachi   | Deskstar 7K160         | 7      | 186     | 952   | 124   | 1.29   |
| Seagate   | UX                     | 1      | 9       | 852   | 10    | 1.28   |
| Seagate   | Constellation ES.2     | 1      | 1       | 467   | 0     | 1.28   |
| Seagate   | SpinPoint M9T          | 3      | 92      | 530   | 5     | 1.28   |
| Samsung   | SpinPoint VL40         | 1      | 1       | 2328  | 4     | 1.28   |
| Toshiba   | 3.5" MG04ACA Enterp... | 5      | 14      | 467   | 1     | 1.28   |
| WDC       | AV                     | 34     | 84      | 701   | 45    | 1.27   |
| Seagate   | Momentus               | 5      | 13      | 720   | 118   | 1.27   |
| Seagate   | Laptop HDD             | 5      | 20      | 556   | 162   | 1.26   |
| WDC       | Caviar                 | 76     | 196     | 798   | 41    | 1.26   |
| Toshiba   | 2.5" HDD MQ01ABD..H    | 1      | 1       | 456   | 0     | 1.25   |
| Seagate   | Barracuda 7200.9       | 38     | 581     | 826   | 390   | 1.25   |
| Seagate   | Unknown                | 5      | 5       | 903   | 1     | 1.24   |
| WDC       | Scorpio Blue EIDE      | 8      | 12      | 448   | 0     | 1.23   |
| Seagate   | Momentus XT (AF)       | 1      | 22      | 590   | 130   | 1.22   |
| Toshiba   | 3.5" HDD DT01ACA       | 4      | 1390    | 511   | 35    | 1.21   |
| Seagate   | Barracuda 7200.12      | 16     | 1883    | 792   | 175   | 1.20   |
| Seagate   | SpinPoint M7E          | 3      | 21      | 443   | 1     | 1.19   |
| Toshiba   | 2.5" HDD MQ03UBB       | 2      | 29      | 446   | 43    | 1.17   |
| Toshiba   | 2.5" HDD MQ01UBD       | 3      | 57      | 546   | 159   | 1.15   |
| Seagate   | SV35                   | 10     | 92      | 525   | 137   | 1.15   |
| Seagate   | Barracuda SpinPoint F3 | 2      | 67      | 577   | 7     | 1.14   |
| WDC       | Black SSHD             | 1      | 10      | 411   | 0     | 1.13   |
| Toshiba   | Toshiba Enterprise     | 2      | 12      | 411   | 0     | 1.13   |
| Seagate   | IronWolf               | 17     | 291     | 447   | 13    | 1.11   |
| MediaMax  | WL1000                 | 5      | 6       | 683   | 4     | 1.11   |
| Fujitsu   | MHZ BJ                 | 5      | 6       | 495   | 173   | 1.11   |
| Seagate   | BarraCuda Pro          | 3      | 8       | 405   | 0     | 1.11   |
| Samsung   | SpinPoint M7U (USB)    | 2      | 5       | 404   | 0     | 1.11   |
| WDC       | Caviar Blue EIDE       | 18     | 117     | 697   | 55    | 1.09   |
| MaxDig... | Unknown                | 5      | 7       | 515   | 12    | 1.09   |
| Toshiba   | Low spin               | 1      | 2       | 385   | 0     | 1.05   |
| Fujitsu   | MHW BH                 | 9      | 72      | 543   | 70    | 1.05   |
| Seagate   | Barracuda ES.2         | 5      | 52      | 1042  | 339   | 1.05   |
| Toshiba   | 2.5" HDD MK..59GSXP... | 1      | 4       | 450   | 7     | 1.05   |
| Samsung   | SpinPoint F4           | 2      | 53      | 678   | 162   | 1.04   |
| Maxtor    | DiamondMax 21          | 17     | 268     | 760   | 396   | 1.03   |
| WDC       | HGST Ultrastar He10    | 5      | 127     | 374   | 1     | 1.03   |
| Seagate   | Constellation ES       | 7      | 9       | 1562  | 575   | 1.02   |
| Apple     | HGST Travelstar Z5K500 | 1      | 40      | 398   | 7     | 1.01   |
| Seagate   | SpinPoint F4           | 2      | 9       | 705   | 69    | 1.00   |
| Samsung   | SpinPoint T166         | 8      | 250     | 1008  | 448   | 0.99   |
| Magnet... | Unknown                | 6      | 8       | 360   | 0     | 0.99   |
| WDC       | Elements / My Passport | 67     | 495     | 466   | 30    | 0.99   |
| HGST      | Ultrastar He6          | 1      | 1       | 353   | 0     | 0.97   |
| Toshiba   | X300                   | 7      | 113     | 398   | 27    | 0.97   |
| Seagate   | Video 2.5              | 5      | 34      | 403   | 11    | 0.96   |
| Seagate   | BarraCuda              | 1      | 1       | 346   | 0     | 0.95   |
| ExcelStor | Jupiter                | 8      | 20      | 862   | 12    | 0.95   |
| WDC       | Green Mobile           | 3      | 9       | 496   | 6     | 0.95   |
| HPE       | Seagate Constellati... | 1      | 1       | 1037  | 2     | 0.95   |
| Seagate   | Exos 7E8               | 12     | 38      | 398   | 54    | 0.94   |
| HGST      | Travelstar 7K1000      | 4      | 523     | 424   | 149   | 0.94   |
| WDC       | Gold                   | 20     | 70      | 348   | 1     | 0.93   |
| Seagate   | Maxtor DiamondMax 23   | 5      | 82      | 738   | 254   | 0.93   |
| Samsung   | SpinPoint F1           | 1      | 1       | 1320  | 3     | 0.90   |
| WDC       | Scorpio                | 3      | 3       | 722   | 1     | 0.90   |
| Seagate   | Barracuda              | 2      | 8       | 325   | 0     | 0.89   |
| HGST      | CinemaStar Z5K500      | 3      | 8       | 370   | 1     | 0.89   |
| Samsung   | SpinPoint P80 SD       | 7      | 263     | 816   | 377   | 0.88   |
| Seagate   | Barracuda 3.5          | 9      | 1239    | 341   | 33    | 0.85   |
| Apple     | Momentus               | 1      | 6       | 584   | 3     | 0.85   |
| Fujitsu   | MHT                    | 10     | 14      | 707   | 171   | 0.85   |
| Seagate   | FireCuda 3.5           | 2      | 79      | 356   | 17    | 0.85   |
| WDC       | Scorpio Black          | 56     | 308     | 512   | 92    | 0.85   |
| WDC       | Blue UltraSlim         | 2      | 2       | 309   | 0     | 0.85   |
| MediaMax  | WL5000                 | 1      | 1       | 308   | 0     | 0.85   |
| Toshiba   | 2.5" HDD MQ01ABC       | 1      | 2       | 308   | 0     | 0.84   |
| Seagate   | Barracuda LP           | 4      | 100     | 800   | 363   | 0.83   |
| Toshiba   | N300/MN NAS HDD        | 1      | 23      | 318   | 1     | 0.83   |
| Toshiba   | Toshiba Surveillance   | 2      | 2       | 744   | 3     | 0.82   |
| Seagate   | Barracuda ATA V        | 3      | 4       | 1510  | 35    | 0.82   |
| Fujitsu   | MHY BH                 | 5      | 97      | 525   | 158   | 0.82   |
| WDC       | Red Pro                | 14     | 40      | 294   | 0     | 0.81   |
| WDC       | Blue                   | 57     | 883     | 325   | 17    | 0.80   |
| Hitachi   | Deskstar E7K1000       | 2      | 7       | 1486  | 29    | 0.80   |
| Hitachi   | Travelstar 5K500.B     | 16     | 574     | 521   | 162   | 0.80   |
| Toshiba   | 2.5" HDD MQ02ABD..H    | 1      | 29      | 400   | 76    | 0.80   |
| WDC       | Scorpio Blue           | 238    | 2672    | 450   | 69    | 0.80   |
| Samsung   | SpinPoint M7E (AF)     | 4      | 181     | 474   | 80    | 0.77   |
| Seagate   | SpinPoint M8 (AF)      | 6      | 1408    | 398   | 40    | 0.76   |
| Seagate   | Skyhawk                | 10     | 60      | 293   | 3     | 0.76   |
| Hitachi   | Travelstar 7K320       | 13     | 44      | 661   | 522   | 0.74   |
| Seagate   | Momentus 7200.3        | 8      | 26      | 594   | 62    | 0.74   |
| Seagate   | Momentus 7200.2        | 8      | 33      | 526   | 172   | 0.74   |
| Samsung   | SpinPoint M7           | 3      | 173     | 407   | 52    | 0.73   |
| Seagate   | Ultra Mobile SSHD      | 2      | 7       | 376   | 69    | 0.73   |
| Seagate   | Barracuda V            | 1      | 1       | 259   | 0     | 0.71   |
| Seagate   | Barracuda Compute      | 3      | 155     | 288   | 18    | 0.71   |
| Fujitsu   | MHZ BH                 | 11     | 129     | 508   | 296   | 0.71   |
| HP        | 500GB SATA disk MM0... | 1      | 13      | 1725  | 49    | 0.70   |
| Toshiba   | 2.5" HDD MQ01ACF       | 2      | 95      | 333   | 46    | 0.69   |
| Hitachi   | Travelstar 5K750       | 3      | 421     | 511   | 388   | 0.69   |
| Toshiba   | MG06ACA Enterprise ... | 4      | 16      | 251   | 0     | 0.69   |
| WDC       | Ultrastar He10/12      | 1      | 8       | 251   | 0     | 0.69   |
| Samsung   | SpinPoint S250         | 2      | 69      | 818   | 625   | 0.68   |
| Toshiba   | 3.5" HDD DT01ACA       | 3      | 11      | 247   | 0     | 0.68   |
| Maxtor    | DiamondMax 20          | 7      | 25      | 595   | 329   | 0.67   |
| Seagate   | Momentus 7200.5        | 4      | 138     | 520   | 111   | 0.67   |
| WDC       | Purple                 | 28     | 203     | 307   | 12    | 0.66   |
| Toshiba   | 2.5" HDD MQ01ABD       | 8      | 1082    | 366   | 135   | 0.66   |
| Fujitsu   | MHW BJ                 | 3      | 4       | 325   | 33    | 0.66   |
| Hitachi   | Deskstar 7K1000.D      | 2      | 112     | 654   | 524   | 0.66   |
| Samsung   | SpinPoint S166         | 3      | 92      | 782   | 492   | 0.66   |
| HGST      | Travelstar Z7K500      | 8      | 271     | 443   | 274   | 0.65   |
| Toshiba   | S300                   | 2      | 3       | 238   | 0     | 0.65   |
| Toshiba   | 2.5" HDD MK..61GSY     | 2      | 2       | 1162  | 8     | 0.65   |
| HP        | Seagate Constellati... | 1      | 1       | 238   | 0     | 0.65   |
| Seagate   | Pipeline HD Mini       | 4      | 19      | 667   | 152   | 0.65   |
| Seagate   | Laptop SSHD            | 10     | 326     | 398   | 123   | 0.65   |
| Toshiba   | 2.5" HDD MK..75GSX     | 4      | 144     | 509   | 393   | 0.65   |
| Seagate   | SpinPoint M9TU (USB)   | 1      | 9       | 233   | 0     | 0.64   |
| Hitachi   | Travelstar 7K750       | 2      | 52      | 610   | 360   | 0.64   |
| Fujitsu   | MHV                    | 28     | 118     | 368   | 33    | 0.63   |
| WDC       | Blue Mobile            | 139    | 2682    | 272   | 20    | 0.63   |
| Seagate   | Momentus 7200.4        | 9      | 311     | 549   | 382   | 0.63   |
| WDC       | Blue SSHD              | 2      | 2       | 230   | 0     | 0.63   |
| Toshiba   | 2.5" HDD               | 18     | 78      | 472   | 64    | 0.63   |
| Seagate   | Barracuda ATA IV       | 4      | 60      | 677   | 29    | 0.63   |
| Hitachi   | CinemaStar Z5K320      | 3      | 4       | 588   | 2     | 0.63   |
| HGST      | Travelstar 5K1000      | 5      | 367     | 421   | 441   | 0.62   |
| Seagate   | Momentus XT            | 1      | 24      | 643   | 97    | 0.62   |
| Toshiba   | 2.5" HDD MQ01ABF       | 2      | 52      | 284   | 62    | 0.62   |
| Maxtor    | DiamondMax 17          | 2      | 12      | 402   | 111   | 0.62   |
| Toshiba   | N300 NAS HDD           | 5      | 26      | 276   | 7     | 0.61   |
| Hitachi   | Travelstar 7K200       | 9      | 30      | 556   | 118   | 0.61   |
| Seagate   | IronWolf Pro           | 14     | 61      | 298   | 2     | 0.61   |
| Quantum   | Fireball lct20         | 2      | 2       | 221   | 0     | 0.61   |
| Seagate   | Constellation (SATA)   | 1      | 3       | 1402  | 99    | 0.60   |
| Seagate   | U6                     | 3      | 21      | 613   | 32    | 0.60   |
| Hitachi   | CinemaStar 7K1000.B    | 2      | 4       | 218   | 0     | 0.60   |
| Fujitsu   | MJA BH                 | 9      | 51      | 476   | 195   | 0.60   |
| Toshiba   | 2.5" HDD MK..59GSM     | 1      | 23      | 509   | 403   | 0.60   |
| Toshiba   | 2.5" HDD MQ04UBB       | 1      | 25      | 218   | 0     | 0.60   |
| Toshiba   | P300                   | 7      | 601     | 230   | 9     | 0.60   |
| WDC       | Black Mobile           | 31     | 326     | 243   | 17    | 0.60   |
| Seagate   | Exos X14               | 4      | 15      | 217   | 0     | 0.59   |
| Hitachi   | Travelstar 4K120       | 5      | 16      | 709   | 27    | 0.59   |
| Seagate   | Momentus 5400.2        | 16     | 61      | 433   | 363   | 0.59   |
| Samsung   | SpinPoint M8 (AF)      | 5      | 85      | 388   | 77    | 0.59   |
| Seagate   | Laptop Thin SSHD       | 1      | 3       | 212   | 0     | 0.58   |
| HGST      | Travelstar Z5K1000     | 3      | 106     | 238   | 50    | 0.58   |
| HGST      | Edurastar              | 1      | 1       | 211   | 0     | 0.58   |
| Seagate   | Momentus 5400.7 (AF)   | 2      | 21      | 534   | 321   | 0.57   |
| Toshiba   | 2.5" HDD MQ01ABD       | 5      | 21      | 269   | 11    | 0.57   |
| Samsung   | SpinPoint P80          | 18     | 143     | 592   | 156   | 0.57   |
| Toshiba   | 2.5" HDD MK..75GSX     | 1      | 2       | 272   | 538   | 0.56   |
| Toshiba   | 2.5" HDD MQ02ABF       | 1      | 10      | 216   | 1     | 0.56   |
| Toshiba   | MG07ACA Enterprise ... | 2      | 8       | 203   | 0     | 0.56   |
| Toshiba   | 2.5" HDD MQ04UBF       | 1      | 47      | 221   | 3     | 0.55   |
| Toshiba   | 2.5" HDD MK..53GSX     | 1      | 1       | 201   | 0     | 0.55   |
| Hitachi   | Travelstar 7K100       | 5      | 20      | 621   | 76    | 0.55   |
| Hitachi   | Travelstar 5K1000      | 3      | 32      | 477   | 648   | 0.54   |
| Seagate   | FireCuda 2.5           | 6      | 195     | 245   | 68    | 0.54   |
| Seagate   | Momentus 5400 PSD      | 2      | 3       | 352   | 338   | 0.53   |
| Seagate   | Barracuda ATA III      | 1      | 1       | 194   | 0     | 0.53   |
| Toshiba   | 1.8" HDD MK..29GSG     | 3      | 7       | 390   | 337   | 0.53   |
| Seagate   | Barracuda 2.5 5400     | 6      | 402     | 226   | 65    | 0.53   |
| Samsung   | SpinPoint MT2          | 1      | 5       | 191   | 0     | 0.53   |
| Hitachi   | Travelstar Z7K320      | 4      | 76      | 471   | 469   | 0.53   |
| Seagate   | LD25.2                 | 2      | 5       | 249   | 1     | 0.52   |
| Seagate   | Video 3.5              | 1      | 3       | 186   | 0     | 0.51   |
| Hitachi   | Travelstar Z5K320      | 3      | 292     | 360   | 307   | 0.51   |
| Toshiba   | 2.5" HDD MQ04UBD       | 1      | 32      | 192   | 1     | 0.51   |
| IBM/Hi... | Deskstar 120GXP        | 4      | 8       | 655   | 117   | 0.50   |
| Hitachi   | Travelstar Z7K500      | 3      | 24      | 466   | 706   | 0.50   |
| Fujitsu   | MHZ BT                 | 1      | 2       | 1426  | 6     | 0.50   |
| Toshiba   | 2.5" HDD MK..76GSX     | 6      | 21      | 247   | 210   | 0.50   |
| Fujitsu   | MHX BT                 | 2      | 9       | 497   | 19    | 0.50   |
| Samsung   | SpinPoint MP5          | 3      | 13      | 318   | 141   | 0.49   |
| Hitachi   | CinemaStar 5K1000.B    | 2      | 3       | 474   | 246   | 0.49   |
| Apple     | HGST Travelstar 5K750  | 2      | 8       | 340   | 31    | 0.49   |
| MediaMax  | WL3000                 | 1      | 1       | 178   | 0     | 0.49   |
| Toshiba   | L200                   | 6      | 74      | 204   | 31    | 0.49   |
| Apple     | MK..65GSXF             | 1      | 6       | 256   | 69    | 0.48   |
| Toshiba   | 2.5" HDD MK..59GSM     | 2      | 38      | 629   | 769   | 0.48   |
| Seagate   | BarraCuda 3.5          | 10     | 443     | 187   | 34    | 0.48   |
| Toshiba   | 2.5" HDD MK..58GSX     | 1      | 6       | 787   | 9     | 0.48   |
| Seagate   | Momentus 5400.4        | 3      | 101     | 501   | 430   | 0.48   |
| Hitachi   | Travelstar 5K320       | 12     | 205     | 511   | 217   | 0.48   |
| Toshiba   | 2.5" HDD MK..34GSX     | 2      | 17      | 429   | 129   | 0.47   |
| Seagate   | Momentus 5400.3        | 10     | 189     | 446   | 443   | 0.46   |
| HGST      | Ultrastar DC HC310     | 1      | 9       | 168   | 0     | 0.46   |
| Hitachi   | Travelstar Z5K500      | 3      | 202     | 382   | 247   | 0.46   |
| Hitachi   | Travelstar 5K250       | 10     | 248     | 555   | 171   | 0.46   |
| Toshiba   | 2.5" HDD MQ01ABF       | 1      | 529     | 232   | 93    | 0.46   |
| Seagate   | Laptop Ultrathin       | 1      | 7       | 206   | 3     | 0.45   |
| Fujitsu   | MHW AT                 | 2      | 2       | 165   | 0     | 0.45   |
| Seagate   | Mobile HDD             | 4      | 892     | 208   | 120   | 0.45   |
| WDC       | Shrek LT 2.5           | 6      | 10      | 265   | 3     | 0.44   |
| Toshiba   | 1.8" HDD MK..33GSG     | 2      | 9       | 455   | 233   | 0.44   |
| Fujitsu   | MHZ BS                 | 1      | 1       | 159   | 0     | 0.44   |
| WDC       | Black UltraSlim        | 1      | 2       | 596   | 10    | 0.43   |
| Toshiba   | 2.5" HDD MK..55GSX     | 9      | 104     | 449   | 102   | 0.43   |
| Maxtor    | DiamondMax D540X-4K    | 3      | 4       | 487   | 13    | 0.43   |
| Samsung   | SpinPoint V80          | 3      | 4       | 597   | 63    | 0.42   |
| Seagate   | Momentus 7200.1        | 2      | 9       | 541   | 366   | 0.42   |
| Samsung   | SpinPoint V60          | 1      | 6       | 1055  | 104   | 0.42   |
| Seagate   | Exos X16               | 3      | 48      | 153   | 0     | 0.42   |
| Toshiba   | 2.5" HDD MK..37GSX     | 2      | 23      | 405   | 117   | 0.41   |
| Seagate   | FreePlay               | 5      | 23      | 361   | 751   | 0.40   |
| Hitachi   | Travelstar 7K500       | 11     | 130     | 524   | 711   | 0.40   |
| Seagate   | SV35.5                 | 3      | 9       | 811   | 362   | 0.40   |
| MediaMax  | WL320                  | 1      | 1       | 146   | 0     | 0.40   |
| Hitachi   | Travelstar 5K500       | 1      | 6       | 520   | 5     | 0.40   |
| WDC       | Protege                | 6      | 12      | 681   | 34    | 0.40   |
| Lenovo    | RE                     | 1      | 2       | 145   | 0     | 0.40   |
| Toshiba   | 2.5" HDD MK..63GSX     | 2      | 22      | 644   | 79    | 0.39   |
| Toshiba   | 1.8" HDD               | 5      | 12      | 401   | 12    | 0.39   |
| HP        | Ultrastar 7K4000       | 1      | 2       | 1500  | 505   | 0.39   |
| Toshiba   | 2.5" HDD MK..59GSX     | 1      | 8       | 366   | 299   | 0.39   |
| Seagate   | Momentus Thin          | 9      | 246     | 417   | 578   | 0.38   |
| Hitachi   | Travelstar 5K160       | 11     | 204     | 526   | 78    | 0.38   |
| Seagate   | Momentus 5400.6        | 11     | 1178    | 480   | 465   | 0.38   |
| HGST      | Ultrastar DC HC520 ... | 3      | 26      | 138   | 1     | 0.38   |
| Toshiba   | 2.5" HDD MK..65GSX     | 13     | 274     | 486   | 283   | 0.38   |
| HP        | Barracuda ES.2         | 1      | 1       | 138   | 0     | 0.38   |
| Toshiba   | 2.5" HDD MK..59GSXP    | 7      | 164     | 415   | 355   | 0.38   |
| HGST      | Ultrastar HC310/320    | 3      | 24      | 136   | 64    | 0.37   |
| Samsung   | SpinPoint P120         | 6      | 116     | 892   | 617   | 0.37   |
| HGST      | Travelstar Z5K500      | 6      | 682     | 305   | 377   | 0.37   |
| HGST      | Deskstar 5K4000        | 1      | 2       | 133   | 0     | 0.37   |
| HPE       | Proliant HardDrive     | 1      | 2       | 127   | 0     | 0.35   |
| Toshiba   | 2.5" HDD MK..46GSX     | 4      | 52      | 503   | 133   | 0.35   |
| Toshiba   | 1.8" HDD MK..16GSG     | 1      | 3       | 272   | 4     | 0.34   |
| WDC       | Black P10              | 2      | 5       | 122   | 0     | 0.34   |
| Toshiba   | MG05ACA Enterprise ... | 1      | 1       | 121   | 0     | 0.33   |
| Toshiba   | 1.8" HDD               | 5      | 14      | 660   | 167   | 0.33   |
| Samsung   | SpinPoint V120CE       | 1      | 1       | 120   | 0     | 0.33   |
| Hitachi   | Travelstar 5K100       | 9      | 65      | 438   | 64    | 0.33   |
| Lenovo    | Seagate Enterprise     | 1      | 2       | 120   | 0     | 0.33   |
| MediaMax  | WL6000                 | 1      | 2       | 438   | 686   | 0.33   |
| WDC       | Internal Use HDD       | 19     | 87      | 124   | 21    | 0.33   |
| Seagate   | SpinPoint M8U (USB)    | 2      | 56      | 147   | 20    | 0.33   |
| Samsung   | SpinPoint F1 EG        | 1      | 8       | 774   | 443   | 0.32   |
| IBM/Hi... | Travelstar 60GH and... | 3      | 5       | 217   | 3     | 0.32   |
| Hitachi   | Travelstar 5K120       | 2      | 4       | 384   | 5     | 0.32   |
| Toshiba   | 2.5" HDD MQ04ABF       | 2      | 367     | 129   | 36    | 0.32   |
| Toshiba   | 2.5" HDD MK..56GSY     | 6      | 27      | 212   | 281   | 0.32   |
| Seagate   | SV35.2                 | 3      | 8       | 609   | 881   | 0.31   |
| Seagate   | Laptop Thin HDD        | 7      | 1102    | 296   | 429   | 0.31   |
| Toshiba   | 2.5" HDD MK..52GSX     | 5      | 109     | 531   | 160   | 0.31   |
| Seagate   | Exos 5E8               | 1      | 5       | 110   | 0     | 0.30   |
| Toshiba   | 2.5" HDD MQ04ABD       | 1      | 8       | 109   | 0     | 0.30   |
| Toshiba   | DT02 Series            | 1      | 1       | 109   | 0     | 0.30   |
| Seagate   | Ultra Mobile HDD       | 2      | 3       | 107   | 0     | 0.30   |
| Samsung   | HM100UX (S2 Portable)  | 1      | 2       | 186   | 4     | 0.29   |
| IBM       | Travelstar 25GS, 18... | 2      | 2       | 156   | 3     | 0.29   |
| Quantum   | Fireball lct15         | 2      | 2       | 248   | 3     | 0.29   |
| Seagate   | Barracuda Pro Compute  | 2      | 193     | 130   | 60    | 0.29   |
| Toshiba   | 2.5" HDD MK..51GSY     | 1      | 1       | 939   | 8     | 0.29   |
| ASMedia   | Unknown                | 1      | 1       | 103   | 0     | 0.28   |
| Toshiba   | 2.5" HDD H200          | 2      | 4       | 103   | 0     | 0.28   |
| Toshiba   | 2.5" HDD MK..65GSX     | 4      | 7       | 301   | 53    | 0.28   |
| Toshiba   | MG08ACA Enterprise ... | 1      | 11      | 101   | 0     | 0.28   |
| IBM       | Deskstar 40GV & 75G... | 3      | 4       | 1041  | 24    | 0.27   |
| Toshiba   | V300                   | 1      | 1       | 97    | 0     | 0.27   |
| Seagate   | MobileMax-2            | 1      | 2       | 169   | 3     | 0.26   |
| Seagate   | DB35.4                 | 1      | 4       | 948   | 186   | 0.25   |
| Seagate   | Exos X18               | 2      | 40      | 90    | 0     | 0.25   |
| WDC       | Scorpio EIDE           | 8      | 10      | 324   | 57    | 0.25   |
| Toshiba   | 2.5" HDD MK..37GSX     | 2      | 57      | 508   | 90    | 0.25   |
| Hitachi   | Travelstar 7K60        | 1      | 2       | 289   | 34    | 0.24   |
| HGST      | Travelstar Z5K500.B    | 1      | 24      | 90    | 1     | 0.23   |
| Seagate   | Barracuda 7200.11      | 13     | 454     | 839   | 322   | 0.23   |
| Toshiba   | 2.5" HDD MK..46GSX     | 1      | 13      | 359   | 38    | 0.23   |
| Toshiba   | 2.5" HDD MK..61GSY[N]  | 8      | 72      | 116   | 203   | 0.23   |
| WDC       | White Label            | 13     | 72      | 87    | 1     | 0.23   |
| Samsung   | SpinPoint M            | 2      | 12      | 268   | 15    | 0.23   |
| Seagate   | Momentus 5400.5        | 5      | 108     | 448   | 206   | 0.22   |
| Seagate   | Momentus 4200.2        | 5      | 7       | 466   | 304   | 0.22   |
| Toshiba   | 2.5" HDD MK..55GSX     | 3      | 7       | 279   | 396   | 0.22   |
| WDC       | Ultrastar DC HC530     | 2      | 11      | 78    | 2     | 0.21   |
| Seagate   | SV35.3                 | 2      | 3       | 1165  | 13    | 0.21   |
| MediaMax  | WL4000                 | 1      | 1       | 71    | 0     | 0.20   |
| WDC       | IU HA500               | 1      | 6       | 71    | 0     | 0.20   |
| Seagate   | LD25 Series            | 2      | 5       | 123   | 417   | 0.19   |
| MediaMax  | WL250                  | 4      | 5       | 450   | 4     | 0.18   |
| MediaMax  | WL1500                 | 3      | 5       | 527   | 80    | 0.17   |
| Samsung   | SpinPoint M40/60/80    | 9      | 25      | 475   | 407   | 0.16   |
| MediaMax  | WL750                  | 1      | 1       | 59    | 0     | 0.16   |
| China     | Unknown                | 4      | 4       | 140   | 596   | 0.16   |
| Toshiba   | 2.5" HDD MK..76GSX     | 5      | 126     | 97    | 253   | 0.16   |
| IBM/Hi... | Hitachi Travelstar ... | 5      | 19      | 407   | 41    | 0.15   |
| IBM/Hi... | Deskstar 60GXP         | 2      | 5       | 638   | 72    | 0.15   |
| Seagate   | Constellation          | 1      | 1       | 2980  | 59    | 0.14   |
| Seagate   | Terascale              | 2      | 3       | 49    | 0     | 0.13   |
| Hitachi   | Travelstar 4K40        | 1      | 7       | 441   | 161   | 0.13   |
| Samsung   | SpinPoint M8U (USB)    | 2      | 3       | 44    | 0     | 0.12   |
| Samsung   | SpinPoint N2           | 2      | 2       | 46    | 1044  | 0.12   |
| MARSHAL   | Unknown                | 5      | 9       | 184   | 319   | 0.12   |
| Samsung   | SpinPoint M5           | 6      | 126     | 360   | 444   | 0.12   |
| Seagate   | Pipeline HD Pro        | 1      | 2       | 828   | 40    | 0.11   |
| Seagate   | SkyHawk                | 4      | 14      | 37    | 0     | 0.10   |
| Toshiba   | 2.5" HDD MQ02ABF..H    | 2      | 8       | 149   | 257   | 0.10   |
| Fujitsu   | MHJ                    | 1      | 1       | 1462  | 41    | 0.10   |
| Samsung   | SpinPoint M6           | 3      | 23      | 312   | 390   | 0.09   |
| HGST      | Travelstar Z7K500.B    | 1      | 2       | 33    | 0     | 0.09   |
| WDC       | Red Plus               | 7      | 34      | 35    | 1     | 0.09   |
| WDC       | Ultrastar DC HC550     | 3      | 8       | 32    | 0     | 0.09   |
| Synology  | Synology Enterprise    | 1      | 7       | 32    | 0     | 0.09   |
| Hitachi   | Travelstar 5K80        | 3      | 4       | 225   | 173   | 0.08   |
| Samsung   | SpinPoint V40+         | 2      | 3       | 1003  | 159   | 0.08   |
| Seagate   | U8                     | 1      | 1       | 754   | 24    | 0.08   |
| Seagate   | Mobile USB Momentus    | 1      | 3       | 29    | 0     | 0.08   |
| WDC       | Unknown                | 10     | 22      | 217   | 22    | 0.08   |
| MediaMax  | WL120                  | 1      | 1       | 139   | 4     | 0.08   |
| Samsung   | USB Hard Disk          | 2      | 2       | 45    | 166   | 0.07   |
| Maxtor    | DiamondMax 22          | 4      | 45      | 810   | 383   | 0.07   |
| Toshiba   | N300                   | 1      | 2       | 26    | 0     | 0.07   |
| Seagate   | Pipeline HD 5900.1     | 3      | 12      | 465   | 124   | 0.07   |
| Hitachi   | Travelstar DK23XX/D... | 5      | 6       | 375   | 240   | 0.07   |
| IBM       | Travelstar 32GH, 30... | 1      | 1       | 138   | 5     | 0.06   |
| Toshiba   | MG08                   | 1      | 1       | 22    | 0     | 0.06   |
| CLOVER    | Unknown                | 1      | 1       | 22    | 0     | 0.06   |
| MediaMax  | WL640                  | 1      | 1       | 20    | 0     | 0.05   |
| CLOVER    | Hightech Utania        | 2      | 3       | 19    | 0     | 0.05   |
| MediaMax  | WL160                  | 1      | 1       | 517   | 25    | 0.05   |
| WDC       | IU CB500               | 3      | 13      | 28    | 156   | 0.05   |
| Samsung   | SpinPoint MP2          | 2      | 2       | 126   | 7     | 0.05   |
| Toshiba   | 2.5" HDD MQ04ABB       | 1      | 1       | 17    | 0     | 0.05   |
| Hitachi   | CinemaStar 7K1000.C    | 2      | 2       | 1040  | 38    | 0.04   |
| Maxtor    | DiamondMax 10 (ATA/... | 23     | 87      | 23    | 118   | 0.04   |
| WDC       | Caviar WDxxxBA         | 1      | 1       | 296   | 20    | 0.04   |
| Seagate   | MobileMax 80215        | 1      | 1       | 13    | 0     | 0.04   |
| Seagate   | U10                    | 1      | 1       | 380   | 27    | 0.04   |
| Maxtor    | Fireball 3             | 6      | 13      | 37    | 31    | 0.04   |
| Samsung   | SpinPoint N3A          | 1      | 1       | 11    | 0     | 0.03   |
| MediaMax  | WL2000                 | 1      | 1       | 33    | 2     | 0.03   |
| WDC       | eServer                | 1      | 1       | 10    | 0     | 0.03   |
| Toshiba   | 2.5" HDD               | 3      | 3       | 301   | 66    | 0.03   |
| Seagate   | SpinPoint F3           | 1      | 1       | 9     | 0     | 0.03   |
| Samsung   | SpinPoint T            | 1      | 1       | 469   | 51    | 0.02   |
| Maxtor    | MaXLine III (ATA/13... | 4      | 7       | 17    | 34    | 0.02   |
| Samsung   | SpinPoint N3C          | 1      | 1       | 96    | 11    | 0.02   |
| LENOVO    | RE                     | 1      | 2       | 7     | 0     | 0.02   |
| Maxtor    | MaXLine III            | 1      | 1       | 244   | 32    | 0.02   |
| Maxtor    | DiamondMax Plus 8      | 4      | 21      | 26    | 23    | 0.02   |
| Seagate   | Lyrion                 | 1      | 1       | 7     | 0     | 0.02   |
| HPE       | Unknown                | 1      | 1       | 6     | 0     | 0.02   |
| Seagate   | Momentus 42            | 1      | 1       | 225   | 35    | 0.02   |
| Maxtor    | DiamondMax 1750        | 1      | 1       | 5613  | 1044  | 0.01   |
| Hitachi   | Travelstar E7K100      | 1      | 1       | 4     | 0     | 0.01   |
| Maxtor    | DiamondMax Plus 9      | 11     | 102     | 27    | 176   | 0.01   |
| Seagate   | FireCuda               | 1      | 1       | 39    | 18    | 0.01   |
| HGST      | Proliant HardDrive     | 1      | 1       | 745   | 406   | 0.01   |
| Fujitsu   | MHY BS                 | 1      | 1       | 2382  | 1317  | 0.00   |
| Hitachi   | Ultrastar 5K3000       | 1      | 1       | 1045  | 595   | 0.00   |
| Maxtor    | DiamondMax 16          | 3      | 5       | 24    | 25    | 0.00   |
| Maxtor    | Fireball 541DX         | 1      | 12      | 23    | 194   | 0.00   |
| Seagate   | Enterprise NAS         | 1      | 1       | 107   | 82    | 0.00   |
| WDC       | Ultrastar DC HC330     | 1      | 1       | 1     | 0     | 0.00   |
| Seagate   | Momentus 5400 FDE.4    | 1      | 1       | 725   | 705   | 0.00   |
| Maxtor    | DiamondMax D540X-4D    | 2      | 5       | 17    | 157   | 0.00   |
| Seagate   | Momentus 7200 FDE.2    | 1      | 1       | 555   | 625   | 0.00   |
| HP        | 1TB SATA disk GB100... | 1      | 1       | 2402  | 3024  | 0.00   |
| Maxtor    | DiamondMax D540X-4G    | 1      | 2       | 20    | 218   | 0.00   |
| MediaMax  | WL400                  | 1      | 1       | 0     | 0     | 0.00   |
| Apple     | Ultrastar A7K2000      | 1      | 1       | 83    | 113   | 0.00   |
| Maxtor    | MaXLine Plus II        | 1      | 2       | 25    | 38    | 0.00   |
| Seagate   | SV35.4                 | 1      | 1       | 685   | 1110  | 0.00   |
| HGST      | Ultrastar DC HC320     | 1      | 3       | 0     | 0     | 0.00   |
| Fujitsu   | MHK                    | 1      | 1       | 77    | 155   | 0.00   |
| Samsung   | SpinPoint N1           | 1      | 1       | 188   | 3047  | 0.00   |
| Maxtor    | DiamondMax Plus 40 ... | 1      | 1       | 121   | 2068  | 0.00   |
| Seagate   | Barracuda ATA II       | 1      | 1       | 103   | 2102  | 0.00   |
| Maxtor    | DiamondMax 40 VL Ul... | 1      | 1       | 8     | 396   | 0.00   |

HDD by Vendor
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF |
|-------------|--------|---------|-------|-------|------|
| HP          | 25     | 69      | 1379  | 77    | 2.17   |
| Quantum     | 9      | 9       | 586   | 1     | 1.52   |
| WDC         | 1904   | 19690   | 640   | 40    | 1.26   |
| Apple       | 16     | 158     | 524   | 41    | 1.22   |
| Hitachi     | 293    | 4851    | 744   | 188   | 1.18   |
| HPE         | 4      | 5       | 564   | 1     | 1.17   |
| Samsung     | 153    | 2881    | 803   | 241   | 1.10   |
| MaxDigital  | 5      | 7       | 515   | 12    | 1.09   |
| Seagate     | 673    | 20561   | 592   | 182   | 0.99   |
| Magnetic... | 6      | 8       | 360   | 0     | 0.99   |
| ExcelStor   | 8      | 20      | 862   | 12    | 0.95   |
| HGST        | 93     | 2414    | 454   | 243   | 0.88   |
| Fujitsu     | 95     | 515     | 496   | 151   | 0.77   |
| Toshiba     | 258    | 6330    | 381   | 104   | 0.72   |
| Maxtor      | 108    | 675     | 483   | 254   | 0.60   |
| IBM/Hitachi | 18     | 45      | 617   | 50    | 0.52   |
| MediaMax    | 23     | 28      | 405   | 66    | 0.41   |
| Lenovo      | 2      | 4       | 132   | 0     | 0.36   |
| ASMedia     | 1      | 1       | 103   | 0     | 0.28   |
| IBM         | 6      | 7       | 659   | 15    | 0.25   |
| China       | 4      | 4       | 140   | 596   | 0.16   |
| MARSHAL     | 5      | 9       | 184   | 319   | 0.12   |
| Synology    | 1      | 7       | 32    | 0     | 0.09   |
| CLOVER      | 3      | 4       | 20    | 0     | 0.06   |
| LENOVO      | 1      | 2       | 7     | 0     | 0.02   |

SSD by Model
------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

See full list of tested SSD samples in the Appendix 2 ([All_SSD.md](/All_SSD.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| Corsair   | Performance Pro    | 256 GB | 1       | 3050  | 0     | 8.36   |
| Intel     | SSDSA2SH064G1GC    | 64 GB  | 2       | 2956  | 0     | 8.10   |
| OCZ       | DENRSTE251M45-0100 | 100 GB | 1       | 2904  | 0     | 7.96   |
| Transcend | 3E128-TS2-550B01   | 100 GB | 16      | 3197  | 1     | 7.88   |
| Intel     | SSDSA2MH080G1GC    | 80 GB  | 1       | 2796  | 0     | 7.66   |
| OCZ       | AGILITY2           | 50 GB  | 1       | 2769  | 0     | 7.59   |
| Intenso   | SSD                | 64 GB  | 1       | 2587  | 0     | 7.09   |
| Samsung   | MCCOE64G5MPP-0VA   | 64 GB  | 1       | 2540  | 0     | 6.96   |
| Corsair   | Force GT           | 50 GB  | 1       | 2387  | 0     | 6.54   |
| HPE       | MK0100GCTYU        | 100 GB | 1       | 2360  | 0     | 6.47   |
| Toshiba   | THNSNH060GCST      | 64 GB  | 1       | 2246  | 0     | 6.16   |
| Corsair   | CSSD-F40GB2-A      | 40 GB  | 1       | 2230  | 0     | 6.11   |
| Micron    | C400-MTFDDAC128MAM | 128 GB | 1       | 2224  | 0     | 6.09   |
| SandForce | FM-25S2S-120GBP2   | 120 GB | 1       | 2101  | 0     | 5.76   |
| Intel     | SSDSC2BA012T4      | 1.2 TB | 1       | 2002  | 0     | 5.49   |
| Intel     | SSDSC2BA200G3C     | 200 GB | 1       | 1963  | 0     | 5.38   |
| Samsung   | MZ7WD240HCFV-00003 | 240 GB | 2       | 1914  | 0     | 5.25   |
| Samsung   | MZ7LM960HCHP00D6   | 960 GB | 1       | 1889  | 0     | 5.18   |
| Intel     | SSDSC2BB240G4      | 240 GB | 5       | 1885  | 0     | 5.17   |
| Plextor   | PX-G512M6e         | 512 GB | 1       | 1878  | 0     | 5.15   |
| OCZ       | VERTEX2 3.5        | 240 GB | 1       | 1798  | 0     | 4.93   |
| Kingston  | SVP100S2512G       | 512 GB | 1       | 1795  | 0     | 4.92   |
| Intel     | SSDSC2BB800G4      | 800 GB | 2       | 1780  | 0     | 4.88   |
| Samsung   | MZHPV256HDGL-000H1 | 256 GB | 1       | 1721  | 0     | 4.72   |
| Corsair   | Neutron XTI SSD    | 480 GB | 1       | 1717  | 0     | 4.70   |
| Intel     | SSDSC2BB120G6      | 120 GB | 1       | 1702  | 0     | 4.66   |
| Toshiba   | THNSNJ256GCSY      | 256 GB | 1       | 1700  | 0     | 4.66   |
| Corsair   | CMFSSD-256GBG2D    | 256 GB | 1       | 1693  | 0     | 4.64   |
| OCZ       | D2RSTK251E19-0100  | 100 GB | 1       | 1689  | 0     | 4.63   |
| OCZ       | VERTEX3            | 96 GB  | 1       | 1686  | 0     | 4.62   |
| Samsung   | MZ7PD128HCFV-000H7 | 128 GB | 1       | 1667  | 0     | 4.57   |
| Corsair   | Force GT           | 240 GB | 3       | 1843  | 1     | 4.55   |
| Intel     | SSDSC2BA200G3      | 200 GB | 2       | 1647  | 0     | 4.51   |
| Kingston  | SVP100S296G        | 96 GB  | 2       | 1638  | 0     | 4.49   |
| ADATA     | SP310              | 32 GB  | 1       | 1628  | 0     | 4.46   |
| Samsung   | SSD PB22-JS3 FD... | 128 GB | 1       | 1626  | 0     | 4.46   |
| Intel     | SSDSC2BB600G4      | 600 GB | 3       | 1624  | 0     | 4.45   |
| OCZ       | VECTOR             | 512 GB | 1       | 1610  | 0     | 4.41   |
| Samsung   | MZHPU256HCGL-000L1 | 256 GB | 1       | 1608  | 0     | 4.41   |
| OCZ       | REVODRIVE3         | 120 GB | 4       | 1590  | 0     | 4.36   |
| Intel     | SSDSC2BA100G3      | 100 GB | 23      | 1619  | 1     | 4.24   |
| OCZ       | VERTEX2            | 40 GB  | 2       | 1543  | 0     | 4.23   |
| Intel     | SSDSC2BB480G4      | 480 GB | 4       | 1531  | 0     | 4.20   |
| Toshiba   | THNSFC064GBSJ      | 64 GB  | 1       | 1526  | 0     | 4.18   |
| Intel     | SSDSA2SH032G1GN    | 32 GB  | 2       | 1518  | 0     | 4.16   |
| OCZ       | AGILITY2           | 40 GB  | 1       | 1516  | 0     | 4.15   |
| Samsung   | SATA SSD           | 128 GB | 1       | 1509  | 0     | 4.14   |
| Intel     | SSDSC2BX400G4      | 400 GB | 1       | 1508  | 0     | 4.13   |
| OCZ       | VERTEX2 3.5        | 90 GB  | 1       | 1507  | 0     | 4.13   |
| SanDisk   | SD7SN6S512G1122    | 512 GB | 1       | 1488  | 0     | 4.08   |
| Intel     | SSDSC2BB080G4      | 80 GB  | 5       | 1481  | 0     | 4.06   |
| Intel     | SSDSC2BP480G4      | 480 GB | 7       | 1478  | 0     | 4.05   |
| OCZ       | VERTEX v1.10       | 64 GB  | 3       | 1655  | 1     | 4.05   |
| ADATA     | XM11               | 120 GB | 2       | 1508  | 1     | 4.03   |
| Kingston  | SVP100S264G        | 64 GB  | 3       | 1469  | 0     | 4.03   |
| Kingston  | SSDNOW             | 32 GB  | 2       | 1465  | 0     | 4.02   |
| Intel     | SSDSA2BW600G3D     | 600 GB | 1       | 1462  | 0     | 4.01   |
| Corsair   | Force 3 SSD        | 180 GB | 5       | 1764  | 1     | 3.97   |
| Toshiba   | THNS128GG4BAAA-... | 128 GB | 2       | 1443  | 0     | 3.96   |
| Toshiba   | THNSN8240PCSE      | 240 GB | 1       | 1434  | 0     | 3.93   |
| Toshiba   | THNSN8480PCSE      | 480 GB | 1       | 1433  | 0     | 3.93   |
| Samsung   | MZ7LM240HCGR-00003 | 240 GB | 2       | 1433  | 0     | 3.93   |
| Intel     | SSDSC2BB160G4      | 160 GB | 3       | 1432  | 0     | 3.93   |
| SanDisk   | SDSA6DM-016G-1006  | 16 GB  | 3       | 1430  | 0     | 3.92   |
| Intel     | SSDMCEAC120B3A     | 120 GB | 2       | 1373  | 0     | 3.76   |
| Samsung   | MZ7LN512HCHP-00000 | 512 GB | 2       | 1362  | 0     | 3.73   |
| Samsung   | MO0100EBTJT        | 100 GB | 1       | 1361  | 0     | 3.73   |
| Samsung   | MZHPU512HCGL-00004 | 512 GB | 1       | 1347  | 0     | 3.69   |
| WDC       | WD1001X06X-00SJVT0 | 1.1 TB | 2       | 1341  | 0     | 3.68   |
| Samsung   | MZ7PC256HAFU-000L7 | 256 GB | 4       | 1337  | 0     | 3.66   |
| Samsung   | SSD 830 Series     | 512 GB | 12      | 1382  | 85    | 3.66   |
| OCZ       | SOLID3             | 64 GB  | 5       | 1604  | 223   | 3.66   |
| Micron    | M510DC_MTFDDAK2... | 240 GB | 2       | 1322  | 0     | 3.62   |
| SK hynix  | HFS250G32TND-N1A0A | 250 GB | 1       | 1302  | 0     | 3.57   |
| SanDisk   | SD5SE2128G1002E    | 128 GB | 4       | 1285  | 0     | 3.52   |
| Crucial   | CT500MX200SSD3     | 500 GB | 2       | 1282  | 0     | 3.51   |
| Intel     | SSDSA2CW080G3      | 80 GB  | 17      | 1315  | 1     | 3.49   |
| Apple     | SSD SM1024F        | 1 TB   | 7       | 1269  | 0     | 3.48   |
| Toshiba   | THNSNJ120PCSZ      | 120 GB | 2       | 1255  | 0     | 3.44   |
| Crucial   | C300-CTFDDAC256MAG | 256 GB | 3       | 1525  | 336   | 3.36   |
| Corsair   | Force 3 SSD        | 240 GB | 10      | 1376  | 105   | 3.34   |
| Intel     | SSDSC2BB120G4      | 120 GB | 3       | 1218  | 0     | 3.34   |
| Samsung   | SSD 850 PRO        | 1 TB   | 45      | 1244  | 1     | 3.33   |
| Samsung   | TK0120GECQL        | 120 GB | 1       | 1208  | 0     | 3.31   |
| Corsair   | Force GT           | 180 GB | 3       | 1205  | 0     | 3.30   |
| Samsung   | SSD 840 EVO 1TB... | 1 TB   | 1       | 1204  | 0     | 3.30   |
| OCZ       | VERTEX2            | 64 GB  | 16      | 1246  | 16    | 3.29   |
| Samsung   | SSD RBX Series ... | 128 GB | 1       | 1194  | 0     | 3.27   |
| Toshiba   | THNSFC256GAMJ      | 256 GB | 2       | 1189  | 0     | 3.26   |
| Mushkin   | MKNSSDCR120GB      | 120 GB | 6       | 1422  | 2     | 3.26   |
| SanDisk   | SDSSDRC032G        | 32 GB  | 4       | 1183  | 0     | 3.24   |
| Intel     | SSDSC2CW240A3      | 240 GB | 33      | 1170  | 0     | 3.21   |
| Seagate   | ST480HM000-1G5162  | 480 GB | 2       | 1282  | 1     | 3.20   |
| Micron    | MTFDDAK064MAR-1... | 64 GB  | 1       | 1164  | 0     | 3.19   |
| Samsung   | SSD 840 EVO        | 1 TB   | 30      | 1162  | 0     | 3.19   |
| Micron    | C400-MTFDDAK128MAM | 128 GB | 3       | 1162  | 0     | 3.18   |
| MyDigi... | SB M2 SSD          | 240 GB | 1       | 1161  | 0     | 3.18   |
| Samsung   | MZMPC064HBDR-000L1 | 64 GB  | 1       | 1157  | 0     | 3.17   |
| Toshiba   | THNS064GG2BNAA     | 64 GB  | 5       | 1157  | 0     | 3.17   |
| Toshiba   | THNSNC128GMMJ      | 128 GB | 5       | 1148  | 0     | 3.15   |
| HP        | VK0300GDUQV        | 304 GB | 1       | 1137  | 0     | 3.12   |
| Intel     | SSDSA2CT040G3      | 40 GB  | 7       | 1134  | 0     | 3.11   |
| Samsung   | MZ7KM240HMHQ-00005 | 240 GB | 2       | 1125  | 0     | 3.08   |
| Corsair   | Force LS SSD       | 960 GB | 1       | 1123  | 0     | 3.08   |
| Samsung   | MZ7LM3T8HCJM-00003 | 3.8 TB | 1       | 1115  | 0     | 3.06   |
| OYUNKEY   | SSD                | 360 GB | 1       | 1107  | 0     | 3.04   |
| Crucial   | CT500MX200SSD6     | 500 GB | 1       | 1103  | 0     | 3.02   |
| Kingston  | RBU-SC400S37256G   | 256 GB | 2       | 1095  | 0     | 3.00   |
| Samsung   | MZ7PD480HAGM-000DA | 480 GB | 1       | 1092  | 0     | 2.99   |
| Corsair   | Force GS           | 180 GB | 3       | 1087  | 0     | 2.98   |
| Micron    | M500_MTFDDAK480MAV | 480 GB | 1       | 1083  | 0     | 2.97   |
| Intel     | SSDSA2MH080G1HP    | 80 GB  | 1       | 1075  | 0     | 2.95   |
| OCZ       | REVODRIVE350       | 120 GB | 4       | 1073  | 0     | 2.94   |
| Samsung   | MZ7PC128HAFU-000L1 | 128 GB | 4       | 1069  | 0     | 2.93   |
| Micron    | MTFDDAK512TBN-1... | 512 GB | 1       | 1062  | 0     | 2.91   |
| Samsung   | MZNTE256HMHP-000L1 | 256 GB | 1       | 1061  | 0     | 2.91   |
| SanDisk   | SDSSDXP480G        | 480 GB | 1       | 1058  | 0     | 2.90   |
| Samsung   | SSD PM830 2.5" 7mm | 256 GB | 15      | 1053  | 0     | 2.89   |
| Samsung   | SSD 840 Series     | 500 GB | 11      | 1122  | 1     | 2.89   |
| OCZ       | AGILITY4           | 128 GB | 6       | 1045  | 0     | 2.86   |
| Intel     | SSDSC2BX016T4      | 1.6 TB | 1       | 1040  | 0     | 2.85   |
| Crucial   | C300-CTFDDAC064MAG | 64 GB  | 9       | 1234  | 224   | 2.84   |
| OCZ       | VERTEX2            | 120 GB | 11      | 1031  | 0     | 2.83   |
| Samsung   | MZ7KM480HMHQ-00005 | 480 GB | 3       | 1029  | 0     | 2.82   |
| Samsung   | MZ7PC128HAFU-000L5 | 128 GB | 2       | 1028  | 0     | 2.82   |
| Kingston  | SH100S3120G        | 120 GB | 7       | 1023  | 0     | 2.80   |
| ADATA     | SP310              | 64 GB  | 1       | 1015  | 0     | 2.78   |
| SanDisk   | SSD U110           | 32 GB  | 1       | 1009  | 0     | 2.76   |
| Apple     | SSD SM512E         | 500 GB | 3       | 1009  | 0     | 2.76   |
| Innodisk  | Corp. - mSATA 3ME3 | 16 GB  | 1       | 1009  | 0     | 2.76   |
| Crucial   | M4-CT128M4SSD2     | 128 GB | 60      | 1056  | 102   | 2.76   |
| Samsung   | MZHPV512HDGL-00000 | 512 GB | 5       | 1006  | 0     | 2.76   |
| ADATA     | SP800              | 32 GB  | 2       | 1001  | 0     | 2.74   |
| Transcend | TS256GMTS600       | 256 GB | 1       | 998   | 0     | 2.73   |
| Hyundai   | 120GB SSD          | 120 GB | 1       | 997   | 0     | 2.73   |
| KingSpec  | SPK-SF12-M120      | 120 GB | 2       | 995   | 0     | 2.73   |
| Toshiba   | THNSNH256GMCT      | 256 GB | 4       | 991   | 0     | 2.72   |
| Samsung   | SSD PM830 mSATA    | 256 GB | 1       | 990   | 0     | 2.71   |
| Samsung   | SSD 830 Series     | 128 GB | 50      | 983   | 0     | 2.70   |
| GALAX     | GXTA1B0120A        | 120 GB | 1       | 976   | 0     | 2.68   |
| Intel     | SSDSA2BW160G3      | 160 GB | 1       | 976   | 0     | 2.68   |
| SK hynix  | SC300 2.5 7MM      | 256 GB | 2       | 974   | 0     | 2.67   |
| Samsung   | SSD 850 EVO        | 2 TB   | 21      | 971   | 0     | 2.66   |
| Intel     | SSDSC2BX200G4      | 200 GB | 2       | 969   | 0     | 2.66   |
| PNY       | CS1311 960GB SSD   | 960 GB | 3       | 968   | 0     | 2.65   |
| SanDisk   | SDSA6MM-016G-1006  | 16 GB  | 8       | 983   | 128   | 2.65   |
| Corsair   | CMFSSD-128GBG2D    | 128 GB | 1       | 954   | 0     | 2.62   |
| Samsung   | MZ7TY256HDHP-000L1 | 256 GB | 1       | 950   | 0     | 2.60   |
| OCZ       | VECTOR             | 256 GB | 3       | 943   | 0     | 2.58   |
| Kingston  | SKC400S371T        | 1 TB   | 1       | 941   | 0     | 2.58   |
| Intel     | SSDSA2BW120G3A     | 120 GB | 1       | 939   | 0     | 2.58   |
| Intel     | SSDSC2BB480G7      | 480 GB | 2       | 935   | 0     | 2.56   |
| Kingston  | SE50S3480G         | 480 GB | 10      | 1104  | 1     | 2.54   |
| Corsair   | Force LE SSD       | 240 GB | 2       | 921   | 0     | 2.52   |
| Samsung   | MZMLN256HCHP-000   | 256 GB | 1       | 919   | 0     | 2.52   |
| SanDisk   | SDLF1CRR-019T-1HA2 | 1.9 TB | 1       | 916   | 0     | 2.51   |
| Kingston  | SVP200S360G        | 64 GB  | 7       | 911   | 0     | 2.50   |
| KingSpec  | ACSC2M064S25       | 64 GB  | 2       | 910   | 0     | 2.49   |
| OWC       | Mercury EXTREME... | 480 GB | 5       | 907   | 0     | 2.49   |
| Intel     | SSDMCEAW120A4      | 120 GB | 2       | 902   | 0     | 2.47   |
| Samsung   | Sasmung SSD 883... | 480 GB | 1       | 900   | 0     | 2.47   |
| Intel     | SSDSC2CW180A3      | 180 GB | 12      | 898   | 0     | 2.46   |
| Crucial   | CT1024MX200SSD1    | 1 TB   | 6       | 955   | 1     | 2.45   |
| Samsung   | MZ7TE512HMHP-000L1 | 512 GB | 5       | 892   | 0     | 2.45   |
| Samsung   | Portable SSD T3    | 250 GB | 1       | 892   | 0     | 2.45   |
| Micron    | MTFDDAK256MBF-1... | 256 GB | 4       | 889   | 0     | 2.44   |
| Samsung   | MZ7WD480HAGM-000D2 | 480 GB | 1       | 886   | 0     | 2.43   |
| Kingston  | SKC310S37A960G     | 960 GB | 1       | 885   | 0     | 2.43   |
| SanDisk   | SD7SB3Q064G        | 56 GB  | 2       | 885   | 0     | 2.42   |
| SK hynix  | SC300B SATA        | 512 GB | 3       | 880   | 0     | 2.41   |
| Corsair   | Neutron SSD        | 256 GB | 1       | 879   | 0     | 2.41   |
| Samsung   | SSD PM800 2.5"     | 256 GB | 2       | 878   | 0     | 2.41   |
| Crucial   | M4-CT512M4SSD2     | 512 GB | 6       | 1342  | 347   | 2.40   |
| Intel     | SSDSC2BB800G7R     | 800 GB | 2       | 1166  | 1     | 2.40   |
| Crucial   | M4-CT128M4SSD1     | 128 GB | 9       | 897   | 112   | 2.39   |
| Apple     | SSD SM128E         | 121 GB | 3       | 1562  | 8     | 2.39   |
| Crucial   | M4-CT256M4SSD1     | 256 GB | 4       | 957   | 253   | 2.38   |
| Axiom     | Signature III SSD  | 240 GB | 1       | 866   | 0     | 2.37   |
| Samsung   | MZ7LF128HCHP-00000 | 128 GB | 1       | 865   | 0     | 2.37   |
| Phison    | SATA SSD           | 16 GB  | 2       | 862   | 0     | 2.36   |
| Samsung   | SSD 840 EVO        | 500 GB | 68      | 939   | 27    | 2.36   |
| Samsung   | SSD PM800 Serie... | 256 GB | 3       | 859   | 0     | 2.35   |
| Apple     | SSD TS256A         | 256 GB | 1       | 858   | 0     | 2.35   |
| SanDisk   | SD5SB2-128G-1006E  | 128 GB | 3       | 857   | 0     | 2.35   |
| ADATA     | SSD S510           | 120 GB | 10      | 869   | 1     | 2.35   |
| Samsung   | SSD 830 Series     | 64 GB  | 19      | 853   | 0     | 2.34   |
| MyDigi... | BP5                | 240 GB | 3       | 842   | 0     | 2.31   |
| Intel     | SSDSA2CW120G3      | 120 GB | 17      | 1043  | 60    | 2.30   |
| OWC       | Mercury Electra... | 500 GB | 5       | 834   | 0     | 2.29   |
| Kingston  | RBU-SC100S37256GD  | 256 GB | 1       | 833   | 0     | 2.28   |
| Patriot   | Blaze SSD ATA D... | 240 GB | 1       | 833   | 0     | 2.28   |
| Phison    | BP4 mSATA SSD      | 240 GB | 1       | 833   | 0     | 2.28   |
| Phison    | UGBA1TPH32H0S2-... | 32 GB  | 1       | 833   | 0     | 2.28   |
| Patriot   | Blast              | 480 GB | 1       | 823   | 0     | 2.26   |
| Kingston  | SNVP325S2512GB     | 512 GB | 1       | 822   | 0     | 2.25   |
| Innodisk  | DES25-64GM41BC1... | 64 GB  | 1       | 821   | 0     | 2.25   |
| Corsair   | Force 3 SSD        | 64 GB  | 19      | 842   | 1     | 2.22   |
| Apple     | SSD TS256C         | 256 GB | 6       | 809   | 0     | 2.22   |
| SanDisk   | SSD U110           | 128 GB | 4       | 808   | 0     | 2.22   |
| Intel     | SSDSCKGF180A4L     | 180 GB | 1       | 805   | 0     | 2.21   |
| SanDisk   | SD6SF1M064G1022    | 64 GB  | 2       | 803   | 0     | 2.20   |
| OCZ       | VERTEX PLUS R2     | 64 GB  | 2       | 802   | 0     | 2.20   |
| OCZ       | DENRSTE251M45-0... | 100 GB | 1       | 801   | 0     | 2.20   |
| ADATA     | SSD S599           | 55 GB  | 1       | 801   | 0     | 2.20   |
| SanDisk   | SD6SP1M128G1102    | 128 GB | 2       | 797   | 0     | 2.18   |
| SanDisk   | SSD U110           | 64 GB  | 3       | 797   | 0     | 2.18   |
| OCZ       | VERTEX PLUS R2     | 247 GB | 1       | 797   | 0     | 2.18   |
| Kingston  | SVP200S37A120G     | 120 GB | 13      | 1014  | 133   | 2.17   |
| Samsung   | SSD 840 Series     | 250 GB | 45      | 823   | 2     | 2.17   |
| Samsung   | MZMPC032HBCD-000D1 | 32 GB  | 7       | 788   | 0     | 2.16   |
| Toshiba   | THNSNH060GMCT      | 64 GB  | 1       | 787   | 0     | 2.16   |
| Corsair   | CSSD-F115GB2-A     | 115 GB | 1       | 781   | 0     | 2.14   |
| Micron    | C400-MTFDDAC256MAM | 256 GB | 1       | 780   | 0     | 2.14   |
| Toshiba   | THNSNJ512GDNU      | 512 GB | 1       | 779   | 0     | 2.14   |
| Radeon    | R7                 | 120 GB | 4       | 778   | 0     | 2.13   |
| Samsung   | SSD 850 PRO        | 128 GB | 46      | 812   | 1     | 2.13   |
| Samsung   | SSD 840 PRO Series | 256 GB | 97      | 823   | 13    | 2.13   |
| Corsair   | Force GS           | 90 GB  | 1       | 776   | 0     | 2.13   |
| Samsung   | SSD 830 Series     | 256 GB | 37      | 788   | 28    | 2.12   |
| SanDisk   | SD9SB8W256G1014    | 256 GB | 1       | 772   | 0     | 2.12   |
| SK hynix  | HFS256G39MND-3510A | 256 GB | 1       | 772   | 0     | 2.12   |
| Samsung   | SSD PM800 2.5"     | 128 GB | 3       | 771   | 0     | 2.11   |
| Toshiba   | THNSNJ256G8NU      | 256 GB | 6       | 769   | 0     | 2.11   |
| Lite-On   | ECE-240NAS         | 240 GB | 1       | 766   | 0     | 2.10   |
| Samsung   | MZ7KM480HAHP-00005 | 480 GB | 1       | 765   | 0     | 2.10   |
| Kingston  | SVP200S37A480G     | 480 GB | 1       | 765   | 0     | 2.10   |
| OCZ       | VERTEX2 3.5        | 115 GB | 3       | 765   | 0     | 2.10   |
| SanDisk   | SD7SB6S128G1122    | 128 GB | 4       | 764   | 0     | 2.09   |
| Corsair   | Force GT           | 120 GB | 19      | 990   | 2     | 2.09   |
| Intel     | SSDSC2CT060A3      | 64 GB  | 9       | 763   | 0     | 2.09   |
| Innodisk  | 2.5" SATA SSD 3ME3 | 64 GB  | 1       | 760   | 0     | 2.08   |
| Samsung   | SSD 840 PRO Series | 128 GB | 54      | 913   | 6     | 2.08   |
| Micron    | C400-MTFDDAK512MAM | 512 GB | 1       | 757   | 0     | 2.08   |
| Samsung   | MZHPV128HDGM-00000 | 128 GB | 3       | 757   | 0     | 2.07   |
| Patriot   | Flare              | 120 GB | 1       | 753   | 0     | 2.06   |
| SK hynix  | SC300B SATA        | 256 GB | 2       | 751   | 0     | 2.06   |
| Samsung   | MZMTE512HMHP-000MV | 512 GB | 3       | 751   | 0     | 2.06   |
| Intel     | SSDSC2BF180A5      | 180 GB | 2       | 2384  | 4     | 2.05   |
| Samsung   | MZ7LN256HMJP-00000 | 256 GB | 4       | 745   | 0     | 2.04   |
| CFD       | CSSD-S6B240CG3VX   | 240 GB | 1       | 742   | 0     | 2.03   |
| Crucial   | M4-CT064M4SSD2     | 64 GB  | 24      | 882   | 217   | 2.02   |
| ADATA     | SP600FA3-256GM     | 256 GB | 1       | 735   | 0     | 2.02   |
| SanDisk   | SD7SB7S512G1122    | 512 GB | 1       | 734   | 0     | 2.01   |
| Samsung   | SSD 840 EVO 120... | 120 GB | 7       | 739   | 1     | 2.00   |
| SanDisk   | SDSSDHII960G       | 960 GB | 8       | 795   | 1     | 2.00   |
| Mushkin   | MKNSSDAT60GB-DX    | 64 GB  | 1       | 728   | 0     | 2.00   |
| Intel     | SSDSC2BW240A3L     | 240 GB | 7       | 728   | 0     | 2.00   |
| Samsung   | MZ7PA256HMDR-010H1 | 256 GB | 2       | 842   | 520   | 1.98   |
| Samsung   | SSD 850 PRO        | 512 GB | 79      | 733   | 14    | 1.98   |
| Micro ... | G2 series          | 64 GB  | 1       | 722   | 0     | 1.98   |
| Samsung   | MZHPV256HDGL-00000 | 256 GB | 5       | 721   | 0     | 1.98   |
| Corsair   | Force 3 SSD        | 120 GB | 37      | 814   | 73    | 1.97   |
| ADATA     | SP600              | 128 GB | 11      | 717   | 0     | 1.96   |
| Samsung   | MZ7TD512HAGM-000L1 | 512 GB | 3       | 715   | 0     | 1.96   |
| SanDisk   | SD8SB8U512G1001    | 512 GB | 1       | 713   | 0     | 1.95   |
| Samsung   | MZ7PD256HAFV-000H7 | 256 GB | 7       | 708   | 0     | 1.94   |
| Samsung   | SSD 840 PRO Series | 512 GB | 26      | 1012  | 67    | 1.94   |
| Samsung   | MZMTE256HMHP-00000 | 256 GB | 3       | 706   | 0     | 1.94   |
| OCZ       | NOCTI              | 64 GB  | 1       | 704   | 0     | 1.93   |
| Crucial   | CT120M500SSD3      | 120 GB | 5       | 790   | 7     | 1.93   |
| Plextor   | PX-128M2S          | 128 GB | 3       | 827   | 1     | 1.92   |
| Samsung   | MZ7PD128HCFV-000H1 | 128 GB | 7       | 700   | 0     | 1.92   |
| Samsung   | MZNLF128HCHP-00000 | 128 GB | 13      | 699   | 0     | 1.92   |
| Toshiba   | TL100              | 120 GB | 3       | 699   | 0     | 1.92   |
| Kingston  | SVP100S2128G       | 128 GB | 1       | 698   | 0     | 1.91   |
| Crucial   | CT512MX100SSD1     | 512 GB | 30      | 734   | 1     | 1.91   |
| Intel     | SSDSC2BB300G4      | 304 GB | 3       | 692   | 0     | 1.90   |
| Samsung   | SSD 840 EVO        | 250 GB | 205     | 728   | 16    | 1.89   |
| OCZ       | VERTEX4            | 256 GB | 32      | 968   | 1     | 1.89   |
| Kingston  | SVP200S390G        | 90 GB  | 1       | 686   | 0     | 1.88   |
| Intel     | SSDSC2BB240G7      | 240 GB | 5       | 686   | 0     | 1.88   |
| SK hynix  | HFS512G32MND-3312A | 512 GB | 1       | 686   | 0     | 1.88   |
| Samsung   | MZMPC256HBGJ-000H1 | 256 GB | 2       | 685   | 0     | 1.88   |
| Samsung   | SSD SM871 2.5 7mm  | 256 GB | 4       | 682   | 0     | 1.87   |
| SMART     | SSD XceedValue2... | 32 GB  | 1       | 681   | 0     | 1.87   |
| Samsung   | MZ7LN256HCHP-00007 | 256 GB | 1       | 681   | 0     | 1.87   |
| Apple     | SSD SM256E         | 256 GB | 6       | 680   | 0     | 1.86   |
| OCZ       | INTREPID 3700 1... | 1.8 TB | 1       | 677   | 0     | 1.86   |
| Seagate   | 2E256-TU2-510B00   | 170 GB | 3       | 2072  | 1366  | 1.85   |
| OCZ       | AGILITY3           | 64 GB  | 55      | 852   | 4     | 1.85   |
| Kingston  | SNVP325S2128GB     | 128 GB | 1       | 674   | 0     | 1.85   |
| Kingston  | SVP200S3120G       | 120 GB | 10      | 775   | 200   | 1.85   |
| Intel     | SSDSC2BA200G4      | 200 GB | 10      | 730   | 1     | 1.85   |
| Apple     | SSD SM768E         | 752 GB | 2       | 673   | 0     | 1.84   |
| KingDian  | N400               | 240 GB | 1       | 670   | 0     | 1.84   |
| Samsung   | SSD PM830 2.5" 7mm | 128 GB | 18      | 815   | 113   | 1.83   |
| Crucial   | M4-CT256M4SSD2     | 256 GB | 39      | 857   | 209   | 1.83   |
| Corsair   | Force GT           | 64 GB  | 7       | 844   | 5     | 1.83   |
| Transcend | TS128GSSD320       | 128 GB | 2       | 666   | 0     | 1.83   |
| SanDisk   | SD6SF1M064G        | 64 GB  | 2       | 666   | 0     | 1.83   |
| SanDisk   | SD6SB2M-512G-1006  | 512 GB | 5       | 665   | 0     | 1.82   |
| OCZ       | TRION150           | 480 GB | 8       | 665   | 0     | 1.82   |
| Innodisk  | Corp. DRPS-02GJ... | 2 GB   | 3       | 664   | 0     | 1.82   |
| Samsung   | MZ7KM960HAHP-00005 | 960 GB | 1       | 662   | 0     | 1.82   |
| Samsung   | SSD PM810 2.5" 7mm | 128 GB | 5       | 720   | 19    | 1.81   |
| Samsung   | MZ7TE256HMHP-00000 | 256 GB | 2       | 659   | 0     | 1.81   |
| Samsung   | SSD 840 EVO        | 120 GB | 158     | 676   | 1     | 1.80   |
| Samsung   | MZ7LN512HMJP-000L7 | 512 GB | 10      | 652   | 0     | 1.79   |
| OCZ       | VERTEX3 MI         | 240 GB | 2       | 1285  | 2     | 1.78   |
| Intel     | SSDSCMMW180A3L     | 180 GB | 3       | 651   | 0     | 1.78   |
| Mushkin   | MKNSSDCR240GB      | 240 GB | 3       | 866   | 349   | 1.78   |
| Kingston  | RBUSNS8280S3128GH2 | 128 GB | 5       | 649   | 0     | 1.78   |
| Samsung   | MZ7TD256HAFV-000L7 | 256 GB | 9       | 647   | 0     | 1.77   |
| Samsung   | SSD 850 PRO        | 2 TB   | 6       | 644   | 0     | 1.76   |
| Kingston  | SKC400S37256G      | 256 GB | 7       | 643   | 0     | 1.76   |
| Kingston  | SKC300S37A480G     | 480 GB | 2       | 643   | 0     | 1.76   |
| OCZ       | VECTOR180          | 240 GB | 2       | 641   | 0     | 1.76   |
| SK hynix  | HFS512G39MND-3510A | 512 GB | 2       | 638   | 0     | 1.75   |
| Apple     | SSD SD512E         | 500 GB | 1       | 636   | 0     | 1.74   |
| Kingston  | SH103S390G         | 90 GB  | 1       | 636   | 0     | 1.74   |
| Kingston  | SV100S232G         | 32 GB  | 5       | 635   | 0     | 1.74   |
| Samsung   | MZ7TE256HMHP-000L7 | 256 GB | 16      | 634   | 0     | 1.74   |
| Samsung   | SSD 850 EVO M.2    | 1 TB   | 7       | 634   | 0     | 1.74   |
| ADATA     | SP600              | 256 GB | 11      | 634   | 0     | 1.74   |
| Samsung   | MZNLN512HCJH-000H1 | 512 GB | 6       | 633   | 0     | 1.74   |
| Micron    | 1100 SATA          | 1 TB   | 1       | 632   | 0     | 1.73   |
| SanDisk   | SD6SB1M-256G-1006  | 256 GB | 2       | 631   | 0     | 1.73   |
| Toshiba   | THNSNF512GCSS      | 512 GB | 1       | 631   | 0     | 1.73   |
| Apacer    | AS330              | 240 GB | 1       | 629   | 0     | 1.73   |
| Intel     | SSDSC2CT180A3      | 180 GB | 13      | 669   | 1     | 1.72   |
| Samsung   | SSD PM851a 2.5 7mm | 1 TB   | 2       | 627   | 0     | 1.72   |
| SK hynix  | HFS120G32TND-N1A2A | 120 GB | 2       | 626   | 0     | 1.72   |
| Kingston  | SV200S364G         | 64 GB  | 5       | 625   | 0     | 1.71   |
| ADATA     | XM11 256GB-V2      | 256 GB | 3       | 625   | 0     | 1.71   |
| Kingston  | SVP200S37A240G     | 240 GB | 1       | 623   | 0     | 1.71   |
| Intel     | SSDMCEAC120B3      | 120 GB | 1       | 1247  | 1     | 1.71   |
| Micron    | M600_MTFDDAK1T0MBF | 1 TB   | 5       | 619   | 0     | 1.70   |
| BlueRay   | SDM9SI128A         | 128 GB | 1       | 619   | 0     | 1.70   |
| Samsung   | MZMPA128HMFU-00000 | 128 GB | 1       | 616   | 0     | 1.69   |
| ZOTAC     | ZTSSD-A4P-120G     | 120 GB | 1       | 615   | 0     | 1.69   |
| Samsung   | MZ7PA128HMCD-010H1 | 128 GB | 2       | 614   | 0     | 1.68   |
| Hyundai   | SSD 240G           | 240 GB | 1       | 613   | 0     | 1.68   |
| SanDisk   | SDSSDHII480G       | 480 GB | 15      | 627   | 1     | 1.68   |
| OCZ       | VECTOR150          | 480 GB | 1       | 611   | 0     | 1.67   |
| Intel     | SSDSC2BP240G4      | 240 GB | 7       | 609   | 0     | 1.67   |
| SanDisk   | SD8SN8U256G1122    | 256 GB | 4       | 608   | 0     | 1.67   |
| Crucial   | CT240M500SSD4      | 240 GB | 1       | 608   | 0     | 1.67   |
| SanDisk   | SD5SG2128G1052E    | 128 GB | 2       | 608   | 0     | 1.67   |
| Samsung   | MZ7LN256HCHP-000H1 | 256 GB | 2       | 607   | 0     | 1.66   |
| Samsung   | SSD 750 EVO        | 500 GB | 31      | 604   | 0     | 1.66   |
| Samsung   | MZ7LN512HMJP-00000 | 512 GB | 3       | 604   | 0     | 1.66   |
| Samsung   | MZNTY128HDHP-000L2 | 128 GB | 2       | 604   | 0     | 1.66   |
| Apple     | SSD SM1024G        | 1 TB   | 6       | 603   | 0     | 1.65   |
| Toshiba   | THNSNJ256GCST      | 256 GB | 4       | 603   | 0     | 1.65   |
| Samsung   | MZ7PD128HAFV-000H7 | 128 GB | 7       | 602   | 0     | 1.65   |
| Kingston  | SKC400S37512G      | 512 GB | 6       | 602   | 0     | 1.65   |
| Samsung   | SSD 850 PRO        | 256 GB | 165     | 611   | 1     | 1.65   |
| Micron    | MTFDDAK1T0MBF-1... | 1 TB   | 2       | 600   | 0     | 1.64   |
| Goodram   | SSDPR_CX300_120    | 120 GB | 3       | 599   | 0     | 1.64   |
| Toshiba   | THNSNF128GMCS      | 128 GB | 5       | 599   | 0     | 1.64   |
| Phison    | 64GB PS3109-S9     | 64 GB  | 1       | 599   | 0     | 1.64   |
| Corsair   | Force 3 SSD        | 480 GB | 1       | 598   | 0     | 1.64   |
| Corsair   | CSSD-V64GB2        | 64 GB  | 2       | 597   | 0     | 1.64   |
| Toshiba   | THNSFJ256GDNU A    | 256 GB | 7       | 595   | 0     | 1.63   |
| Micron    | MTFDDAK512MBF-1... | 512 GB | 7       | 648   | 3     | 1.63   |
| Toshiba   | THNSNJ128GMCU      | 128 GB | 5       | 592   | 0     | 1.62   |
| Samsung   | MZ7TE512HMHP-000L2 | 512 GB | 5       | 591   | 0     | 1.62   |
| Intel     | SSDSC2CT240A4      | 240 GB | 12      | 679   | 1     | 1.62   |
| Micron    | M600_MTFDDAT128MBF | 128 GB | 2       | 589   | 0     | 1.61   |
| Samsung   | SSD 850 EVO        | 1 TB   | 123     | 666   | 6     | 1.61   |
| OCZ       | DENCSTE351M16-0... | 240 GB | 1       | 585   | 0     | 1.60   |
| SanDisk   | SD7SB3Q-128G-1006  | 128 GB | 2       | 584   | 0     | 1.60   |
| OCZ       | D2RSTK251E19-0200  | 200 GB | 1       | 584   | 0     | 1.60   |
| SanDisk   | SD6SN1M128G        | 128 GB | 1       | 584   | 0     | 1.60   |
| OCZ       | AGILITY3           | 120 GB | 61      | 778   | 56    | 1.60   |
| ADATA     | SSD SX900 256GB... | 256 GB | 1       | 580   | 0     | 1.59   |
| Intel     | SSDSC2BA400G3      | 400 GB | 1       | 580   | 0     | 1.59   |
| Galaxy    | GX0240ML103        | 240 GB | 1       | 578   | 0     | 1.58   |
| Samsung   | SSD 850 EVO        | 120 GB | 120     | 575   | 0     | 1.58   |
| Samsung   | MZ7LM1T9HCJM-0E003 | 1.9 TB | 1       | 574   | 0     | 1.58   |
| Toshiba   | THNSNC128GCSJ      | 128 GB | 2       | 574   | 0     | 1.57   |
| SATADOM   | SL 3ME3 V2         | 128 GB | 1       | 574   | 0     | 1.57   |
| ADATA     | SSD S510           | 64 GB  | 3       | 572   | 0     | 1.57   |
| Kingston  | SKC400S37128G      | 128 GB | 3       | 570   | 0     | 1.56   |
| SanDisk   | SDSSDHP256G        | 256 GB | 25      | 569   | 0     | 1.56   |
| Intel     | SSDSC2CT080A4      | 80 GB  | 4       | 568   | 0     | 1.56   |
| Samsung   | MZ7PA128HMCD-010L1 | 128 GB | 3       | 713   | 315   | 1.56   |
| OCZ       | AGILITY4           | 64 GB  | 1       | 567   | 0     | 1.56   |
| Kingston  | SMSM150S324G2      | 24 GB  | 5       | 567   | 0     | 1.55   |
| PNY       | CS1311 480GB SSD   | 480 GB | 7       | 566   | 0     | 1.55   |
| Samsung   | MZ7KM480HMHQ0D3    | 480 GB | 6       | 565   | 0     | 1.55   |
| Samsung   | MZ7TE128HMGR-00004 | 128 GB | 5       | 565   | 0     | 1.55   |
| OCZ       | REVODRIVE3         | 64 GB  | 4       | 564   | 0     | 1.55   |
| PNY       | SSD2SC480G1CS27... | 480 GB | 4       | 564   | 0     | 1.55   |
| Samsung   | MZ7TY128HDHP-000L1 | 128 GB | 9       | 562   | 0     | 1.54   |
| Samsung   | SSD 850 EVO        | 500 GB | 506     | 565   | 1     | 1.54   |
| PNY       | CS1311 240GB SSD   | 240 GB | 15      | 559   | 0     | 1.53   |
| Patriot   | Torch LE           | 240 GB | 1       | 558   | 0     | 1.53   |
| Toshiba   | THNSNC128GAMJ      | 128 GB | 1       | 557   | 0     | 1.53   |
| Apple     | SSD SM0512F        | 500 GB | 9       | 557   | 0     | 1.53   |
| Apple     | SSD SM0256F        | 256 GB | 21      | 556   | 0     | 1.53   |
| SanDisk   | PLUS               | 480 GB | 9       | 556   | 0     | 1.52   |
| OCZ       | VERTEX2 3.5        | 120 GB | 3       | 734   | 1     | 1.52   |
| Samsung   | SSD 850 EVO M.2    | 500 GB | 41      | 556   | 0     | 1.52   |
| Samsung   | SSD 850 EVO M.2    | 120 GB | 9       | 555   | 0     | 1.52   |
| OCZ       | AGILITY3           | 240 GB | 14      | 717   | 27    | 1.52   |
| SanDisk   | SDSSDXPS240G       | 240 GB | 16      | 582   | 65    | 1.52   |
| Toshiba   | THNSNJ128G8NU      | 128 GB | 8       | 551   | 0     | 1.51   |
| Samsung   | SG9MSM6D024GPM00   | 22 GB  | 5       | 551   | 0     | 1.51   |
| ADATA     | SSD SP900 256GB... | 256 GB | 1       | 550   | 0     | 1.51   |
| Samsung   | MZ7PC128HAFU-000H1 | 128 GB | 6       | 548   | 0     | 1.50   |
| Toshiba   | Q300               | 480 GB | 9       | 548   | 0     | 1.50   |
| SK hynix  | HFS512G32MND-3210A | 512 GB | 1       | 547   | 0     | 1.50   |
| SanDisk   | X400 2.5 7MM       | 256 GB | 4       | 545   | 0     | 1.50   |
| OCZ       | VERTEX4            | 128 GB | 84      | 607   | 1     | 1.50   |
| Samsung   | MZ7TY256HDHP-00007 | 256 GB | 1       | 545   | 0     | 1.49   |
| Samsung   | SSD CM871 M.2 2280 | 128 GB | 2       | 544   | 0     | 1.49   |
| Plextor   | PX-512M7VC         | 512 GB | 2       | 544   | 0     | 1.49   |
| Samsung   | MMCRE64G8MPP-0VA   | 64 GB  | 1       | 544   | 0     | 1.49   |
| Hoodisk   | SSD                | 32 GB  | 1       | 542   | 0     | 1.49   |
| OCZ       | VERTEX3            | 120 GB | 66      | 791   | 38    | 1.49   |
| Lite-On   | PH4-8E256          | 256 GB | 1       | 542   | 0     | 1.49   |
| Samsung   | MZNTD256HAGL-000L9 | 256 GB | 2       | 541   | 0     | 1.48   |
| SanDisk   | SD9SB8W128G1122    | 128 GB | 1       | 539   | 0     | 1.48   |
| Samsung   | SSD 850 EVO mSATA  | 1 TB   | 8       | 539   | 0     | 1.48   |
| Toshiba   | VT180              | 480 GB | 3       | 747   | 1     | 1.47   |
| Toshiba   | Q300 Pro           | 128 GB | 2       | 537   | 0     | 1.47   |
| Samsung   | SSD PM810 TH       | 64 GB  | 1       | 536   | 0     | 1.47   |
| Patriot   | Ignite             | 480 GB | 2       | 535   | 0     | 1.47   |
| Kingston  | SH103S3120G        | 120 GB | 82      | 616   | 13    | 1.47   |
| Phison    | SM280128GPTC15T... | 128 GB | 1       | 535   | 0     | 1.47   |
| Samsung   | MZ7TD256HAFV-000L9 | 256 GB | 7       | 534   | 0     | 1.46   |
| Samsung   | MZ7PD256HCGM-000H7 | 256 GB | 16      | 545   | 153   | 1.46   |
| Micron    | M600_MTFDDAK256MBF | 256 GB | 2       | 533   | 0     | 1.46   |
| Plextor   | PX-128M3           | 128 GB | 7       | 597   | 260   | 1.46   |
| Patriot   | Blaze              | 240 GB | 4       | 532   | 0     | 1.46   |
| OCZ       | VERTEX3            | 64 GB  | 33      | 584   | 1     | 1.46   |
| Smartbuy  | SSD                | 90 GB  | 1       | 530   | 0     | 1.45   |
| Samsung   | MZMTD256HAGM-00004 | 256 GB | 1       | 529   | 0     | 1.45   |
| HP        | VK000240GWJPD      | 240 GB | 1       | 529   | 0     | 1.45   |
| Samsung   | MZ7LF128HCHP-000L1 | 128 GB | 2       | 528   | 0     | 1.45   |
| Micron    | 5200_MTFDDAK1T9TDC | 1.9 TB | 13      | 559   | 1     | 1.45   |
| Samsung   | SSD PM830 mSATA    | 32 GB  | 16      | 528   | 0     | 1.45   |
| SanDisk   | SD6SB2M128G1022I   | 128 GB | 2       | 528   | 0     | 1.45   |
| Team      | L3 EVO SSD         | 120 GB | 6       | 527   | 0     | 1.45   |
| SanDisk   | SD6SP1M128G1002    | 128 GB | 3       | 524   | 0     | 1.44   |
| Samsung   | SSD 840 EVO 250... | 250 GB | 8       | 524   | 0     | 1.44   |
| Samsung   | SSD 840 Series     | 120 GB | 51      | 614   | 1     | 1.44   |
| Intel     | SSDSC2CW480A3      | 480 GB | 5       | 523   | 0     | 1.43   |
| Kingston  | SH103S3240G        | 240 GB | 30      | 684   | 74    | 1.43   |
| Samsung   | MZ7PC128HAFU-000   | 128 GB | 3       | 521   | 0     | 1.43   |
| Samsung   | MZRPA256HMDR-000SO | 128 GB | 2       | 520   | 0     | 1.43   |
| AFOX      | SSD                | 120 GB | 1       | 518   | 0     | 1.42   |
| Corsair   | Force GS           | 128 GB | 21      | 516   | 0     | 1.42   |
| Kingston  | SVP200S37A60G      | 64 GB  | 14      | 516   | 0     | 1.42   |
| SanDisk   | SD7UB2Q512G1122    | 512 GB | 2       | 514   | 0     | 1.41   |
| SanDisk   | SD8SB8U512G1122    | 512 GB | 10      | 514   | 0     | 1.41   |
| Kingston  | SEDC400S37960G     | 960 GB | 1       | 513   | 0     | 1.41   |
| Intel     | SSDSA2BW120G3H     | 120 GB | 5       | 544   | 1     | 1.41   |
| Toshiba   | THNS128GG4BBAA     | 128 GB | 2       | 513   | 0     | 1.41   |
| ADATA     | SSD S599           | 115 GB | 1       | 511   | 0     | 1.40   |
| Goodram   | SSDPR-CX300-960    | 960 GB | 1       | 509   | 0     | 1.40   |
| Samsung   | SSD 850 EVO        | 250 GB | 632     | 515   | 2     | 1.40   |
| Intel     | SSDSC2BW180A3L     | 180 GB | 14      | 517   | 1     | 1.40   |
| Mushkin   | MKNSSDEC240GB      | 240 GB | 1       | 509   | 0     | 1.39   |
| SanDisk   | Ultra II           | 480 GB | 31      | 530   | 1     | 1.39   |
| OCZ       | VERTEX3            | 240 GB | 15      | 804   | 86    | 1.39   |
| Intel     | SSDSC2BX480G4      | 480 GB | 1       | 506   | 0     | 1.39   |
| Crucial   | CT256MX100SSD1     | 256 GB | 54      | 526   | 9     | 1.39   |
| SanDisk   | SDSSDH2128G        | 128 GB | 4       | 505   | 0     | 1.38   |
| Intel     | SSDSA2CW160G3      | 160 GB | 5       | 504   | 0     | 1.38   |
| Verbatim  | SATA-III SSD       | 256 GB | 1       | 503   | 0     | 1.38   |
| OCZ       | D2RSTK251E14-0400  | 400 GB | 1       | 502   | 0     | 1.38   |
| Samsung   | MZNLF192HCGS-000L1 | 192 GB | 2       | 501   | 0     | 1.37   |
| Samsung   | MZ7TD128HAFV-000L1 | 128 GB | 13      | 501   | 0     | 1.37   |
| Toshiba   | THNSFJ256GCSU      | 256 GB | 17      | 506   | 1     | 1.37   |
| Goodram   | C100               | 120 GB | 3       | 500   | 0     | 1.37   |
| Kingston  | RBU-SNS8152S3128GF | 128 GB | 2       | 498   | 0     | 1.37   |
| Kingston  | SHSS37A120G        | 120 GB | 12      | 497   | 0     | 1.36   |
| Corsair   | Force GT           | 90 GB  | 4       | 610   | 1     | 1.36   |
| Transcend | TS128GSSD340       | 128 GB | 9       | 539   | 112   | 1.36   |
| Samsung   | SSD 650            | 120 GB | 7       | 496   | 0     | 1.36   |
| Samsung   | MZ7LF128HCHP-00004 | 128 GB | 3       | 494   | 0     | 1.36   |
| OCZ       | VERTEX460A         | 240 GB | 3       | 494   | 0     | 1.35   |
| OCZ       | VERTEX2            | 115 GB | 4       | 494   | 0     | 1.35   |
| Patriot   | Flare              | 64 GB  | 6       | 493   | 0     | 1.35   |
| Toshiba   | FujiFilm           | 128 GB | 1       | 491   | 0     | 1.35   |
| Micron    | MTFDDAK128MAM-1J1  | 128 GB | 17      | 490   | 0     | 1.34   |
| Samsung   | MZ7LN256HCHP-00000 | 256 GB | 4       | 488   | 0     | 1.34   |
| Transcend | TS64GSSD320        | 64 GB  | 3       | 487   | 0     | 1.34   |
| SanDisk   | SD8SB8U1T001122    | 1 TB   | 4       | 486   | 0     | 1.33   |
| Samsung   | SSD 850 EVO mSATA  | 120 GB | 5       | 485   | 0     | 1.33   |
| Lite-On   | LCM-256M3S         | 256 GB | 1       | 484   | 0     | 1.33   |
| OCZ       | VERTEX3 MI         | 120 GB | 19      | 615   | 106   | 1.32   |
| WDC       | WDS500G1B0B-00AS40 | 500 GB | 9       | 482   | 0     | 1.32   |
| SanDisk   | SD7TB3Q-256G-1006  | 256 GB | 10      | 480   | 0     | 1.32   |
| Goodram   | SSD                | 64 GB  | 1       | 480   | 0     | 1.32   |
| TAISU     | SSD                | 120 GB | 1       | 480   | 0     | 1.32   |
| Samsung   | MZ7LN512HAJQ-00000 | 512 GB | 7       | 480   | 0     | 1.32   |
| Samsung   | MZNLF128HCHP-000H1 | 128 GB | 4       | 479   | 0     | 1.31   |
| Kingston  | SV300S37A60G       | 64 GB  | 160     | 510   | 1     | 1.31   |
| Toshiba   | Q300 Pro           | 256 GB | 2       | 478   | 0     | 1.31   |
| Samsung   | MZNLF128HCHP-00004 | 128 GB | 13      | 476   | 0     | 1.31   |
| Kingston  | RBU-SNS8100S3256GD | 256 GB | 3       | 473   | 0     | 1.30   |
| SanDisk   | SD8SBBU480G1122    | 480 GB | 3       | 473   | 0     | 1.30   |
| SanDisk   | SDSSDH240GG25      | 240 GB | 1       | 473   | 0     | 1.30   |
| Samsung   | SSD 850 EVO M.2    | 250 GB | 35      | 472   | 0     | 1.30   |
| OCZ       | AGILITY2           | 64 GB  | 3       | 472   | 0     | 1.29   |
| addlink   | SATA SSD           | 256 GB | 3       | 471   | 0     | 1.29   |
| Kingston  | RBUSC180DS37128GH  | 128 GB | 2       | 470   | 0     | 1.29   |
| China     | SATA SSD           | 1 TB   | 3       | 470   | 0     | 1.29   |
| Toshiba   | TL100              | 240 GB | 11      | 470   | 0     | 1.29   |
| Crucial   | C300-CTFDDAC128MAG | 128 GB | 9       | 844   | 226   | 1.28   |
| Toshiba   | THNSNH060GCST      | 64 GB  | 1       | 467   | 0     | 1.28   |
| Lite-On   | PH4-CE120          | 120 GB | 2       | 467   | 0     | 1.28   |
| Plextor   | PX-64M2S           | 64 GB  | 2       | 467   | 0     | 1.28   |
| Intel     | SSDSC2KB480G8      | 480 GB | 7       | 466   | 0     | 1.28   |
| SK hynix  | SC300 M.2 2280     | 256 GB | 6       | 466   | 0     | 1.28   |
| Lite-On   | LCH-256V2S-HP      | 256 GB | 2       | 465   | 0     | 1.28   |
| Micron    | 5100_MTFDDAK1T9TBY | 1.9 TB | 3       | 1010  | 110   | 1.28   |
| Patriot   | Spark              | 256 GB | 3       | 465   | 0     | 1.28   |
| Indilinx  | IND-S3MP-128G      | 128 GB | 1       | 465   | 0     | 1.27   |
| HP        | SSD M700           | 240 GB | 2       | 465   | 0     | 1.27   |
| SanDisk   | Ultra II           | 960 GB | 26      | 511   | 1     | 1.27   |
| Mushkin   | MKNSSDTR128GB-3DL  | 128 GB | 1       | 464   | 0     | 1.27   |
| FORESEE   | 60GB SSD           | 64 GB  | 1       | 463   | 0     | 1.27   |
| Plextor   | PX-256M7VC         | 256 GB | 5       | 462   | 0     | 1.27   |
| Samsung   | Portable SSD T3    | 2 TB   | 1       | 462   | 0     | 1.27   |
| SanDisk   | SD9SN8W256G1027    | 256 GB | 1       | 461   | 0     | 1.26   |
| Transcend | TS32GSSD370        | 32 GB  | 2       | 461   | 0     | 1.26   |
| Samsung   | MZ7TD256HAFV-00000 | 256 GB | 1       | 458   | 0     | 1.26   |
| ADATA     | SX950              | 240 GB | 3       | 458   | 0     | 1.26   |
| Intel     | SSDSC2CT120A3      | 120 GB | 24      | 768   | 1     | 1.25   |
| Plextor   | PX-512M5Pro        | 512 GB | 3       | 457   | 0     | 1.25   |
| XSTAR     | SSD                | 120 GB | 1       | 455   | 0     | 1.25   |
| Plextor   | PX-256M3P          | 256 GB | 1       | 1360  | 2     | 1.24   |
| Toshiba   | THNSNJ256GMCU      | 256 GB | 3       | 452   | 0     | 1.24   |
| Samsung   | MZ7PC256HAFU-000H1 | 256 GB | 1       | 452   | 0     | 1.24   |
| Crucial   | CT240M500SSD3      | 240 GB | 5       | 514   | 7     | 1.24   |
| Samsung   | MZNLN256HCHP-000L7 | 256 GB | 17      | 450   | 0     | 1.24   |
| Samsung   | SSD 750 EVO        | 250 GB | 74      | 454   | 1     | 1.23   |
| Samsung   | MZ7WD960HMHP-00003 | 960 GB | 6       | 729   | 3     | 1.23   |
| MyDigi... | SC2 M2 SSD         | 120 GB | 2       | 449   | 0     | 1.23   |
| ADATA     | SP900              | 64 GB  | 23      | 492   | 2     | 1.23   |
| Kingston  | SMS100S264G        | 64 GB  | 5       | 463   | 2     | 1.23   |
| SanDisk   | SDSSDX240GG25      | 240 GB | 12      | 1034  | 44    | 1.23   |
| Kingston  | SH100S3240G        | 240 GB | 3       | 1083  | 2     | 1.23   |
| WDC       | WDBNCE2500PNC-WRSN | 250 GB | 2       | 446   | 0     | 1.22   |
| Micron    | M600_MTFDDAK128... | 128 GB | 1       | 445   | 0     | 1.22   |
| SanDisk   | SD6SB1M128G1022I   | 128 GB | 7       | 444   | 0     | 1.22   |
| Foxline   | FLDMMS128G         | 128 GB | 1       | 443   | 0     | 1.22   |
| Toshiba   | THNSNJ128G8NY      | 128 GB | 7       | 443   | 0     | 1.21   |
| ADATA     | SSD                | 32 GB  | 1       | 442   | 0     | 1.21   |
| OCZ       | VERTEX2            | 80 GB  | 1       | 442   | 0     | 1.21   |
| SanDisk   | SD6SB1M128G        | 128 GB | 2       | 442   | 0     | 1.21   |
| Samsung   | MZ7LN512HCHP-000L1 | 512 GB | 10      | 441   | 0     | 1.21   |
| Goodram   | SSD                | 240 GB | 19      | 441   | 0     | 1.21   |
| SanDisk   | SSD PLUS 480G      | 480 GB | 1       | 440   | 0     | 1.21   |
| SanDisk   | SD8SN8U-512G-1006  | 512 GB | 7       | 454   | 1     | 1.20   |
| Samsung   | MZHPV512HDGL-000H1 | 512 GB | 1       | 439   | 0     | 1.20   |
| Intel     | SSDSC2BW180A4      | 180 GB | 11      | 647   | 3     | 1.20   |
| Apple     | SSD SM0512G        | 500 GB | 15      | 437   | 0     | 1.20   |
| Samsung   | MZMPC032HBCD-000L1 | 32 GB  | 4       | 436   | 0     | 1.20   |
| Toshiba   | TR150              | 480 GB | 7       | 523   | 2     | 1.20   |
| Samsung   | MZYTY256HDHP-000L2 | 256 GB | 8       | 436   | 0     | 1.20   |
| Drevo     | X1 pro             | 1 TB   | 2       | 451   | 9     | 1.19   |
| OCZ       | REVODRIVE X2       | 25 GB  | 4       | 435   | 0     | 1.19   |
| Kingston  | RBU-SC152S37256GG2 | 256 GB | 1       | 435   | 0     | 1.19   |
| SanDisk   | SDSSDP064G         | 64 GB  | 32      | 460   | 33    | 1.19   |
| Intel     | SSDSA2M080G2GC     | 80 GB  | 24      | 1085  | 5     | 1.19   |
| Samsung   | MZNLN256HCHP-00000 | 256 GB | 10      | 433   | 0     | 1.19   |
| Phison    | SSDS30256XQC800... | 240 GB | 1       | 433   | 0     | 1.19   |
| OCZ       | ARC100             | 240 GB | 17      | 459   | 1     | 1.19   |
| Apple     | SSD TS128A         | 121 GB | 1       | 431   | 0     | 1.18   |
| China     | ESA3SMH2MSM1BT1... | 120 GB | 1       | 431   | 0     | 1.18   |
| ADATA     | SSD S511           | 120 GB | 1       | 430   | 0     | 1.18   |
| Kingston  | SMS200S330G        | 32 GB  | 3       | 544   | 7     | 1.18   |
| Micron    | MTFDDAK2T0TBN-1... | 2 TB   | 1       | 430   | 0     | 1.18   |
| Samsung   | MMCQE28G8MUP-0VA   | 128 GB | 3       | 658   | 1     | 1.18   |
| Seagate   | ST120HM000-1G5142  | 120 GB | 2       | 429   | 0     | 1.18   |
| China     | 256GB SATA SSD     | 256 GB | 1       | 429   | 0     | 1.18   |
| Samsung   | SMART SSD Xceed... | 32 GB  | 3       | 429   | 0     | 1.18   |
| Toshiba   | Q300 Pro           | 512 GB | 2       | 429   | 0     | 1.18   |
| OCZ       | VERTEX PLUS R2     | 128 GB | 3       | 428   | 0     | 1.17   |
| Samsung   | MZ7LM480HCHP-00... | 480 GB | 2       | 427   | 0     | 1.17   |
| ADATA     | SSD S396           | 32 GB  | 2       | 427   | 0     | 1.17   |
| SanDisk   | SD7TB6S256G1001    | 256 GB | 5       | 426   | 0     | 1.17   |
| Samsung   | MZ7LN256HMJP-000H1 | 256 GB | 10      | 517   | 1     | 1.17   |
| ADATA     | AXM13S2-24GM-B     | 24 GB  | 2       | 740   | 510   | 1.17   |
| SanDisk   | SDSSDA480G         | 480 GB | 21      | 426   | 1     | 1.17   |
| Kingston  | SHSS37A480G        | 480 GB | 12      | 424   | 0     | 1.16   |
| Transcend | TS480GJDM725       | 480 GB | 1       | 424   | 0     | 1.16   |
| SanDisk   | SD8SB8U256G1122    | 256 GB | 8       | 424   | 0     | 1.16   |
| Toshiba   | THNSNJ256GVNU      | 256 GB | 2       | 423   | 0     | 1.16   |
| Kingston  | SS200S330G         | 32 GB  | 3       | 423   | 0     | 1.16   |
| OCZ       | ONYX               | 32 GB  | 3       | 443   | 1     | 1.16   |
| WDC       | WDS250G1B0B-00AS40 | 250 GB | 8       | 423   | 0     | 1.16   |
| Axiom     | Signature III S... | 64 GB  | 1       | 422   | 0     | 1.16   |
| Samsung   | MZNLN256HMHQ-00000 | 256 GB | 8       | 422   | 0     | 1.16   |
| Samsung   | SSD 850 EVO        | 4 TB   | 3       | 422   | 0     | 1.16   |
| Kingston  | SUV400S37480G      | 480 GB | 27      | 439   | 51    | 1.15   |
| Samsung   | MZ7LM480HCHP-00... | 480 GB | 2       | 421   | 0     | 1.15   |
| Toshiba   | THNSNX032GMCT      | 32 GB  | 2       | 421   | 0     | 1.15   |
| Kingston  | SM2280S3G2120G     | 120 GB | 12      | 420   | 0     | 1.15   |
| Kingston  | SKC380S360G        | 64 GB  | 1       | 420   | 0     | 1.15   |
| Crucial   | CT500MX200SSD1     | 500 GB | 24      | 419   | 0     | 1.15   |
| Crucial   | CT960M500SSD1      | 960 GB | 13      | 689   | 163   | 1.14   |
| Palit     | UVS                | 240 GB | 2       | 417   | 0     | 1.14   |
| SanDisk   | SDSSDH2256G        | 256 GB | 2       | 417   | 0     | 1.14   |
| Intel     | SSDSC2BW180A3D     | 180 GB | 1       | 416   | 0     | 1.14   |
| SanDisk   | SDSSDXP240G        | 240 GB | 10      | 416   | 0     | 1.14   |
| PNY       | SSD2SC480G1CS27... | 480 GB | 1       | 415   | 0     | 1.14   |
| Kingston  | SUV400S37960G      | 960 GB | 1       | 415   | 0     | 1.14   |
| SanDisk   | SD9TB8W512G1001    | 512 GB | 4       | 415   | 0     | 1.14   |
| Intel     | SSDSC2MH120A2      | 120 GB | 5       | 414   | 0     | 1.14   |
| SPCC      | SSD110             | 120 GB | 7       | 645   | 291   | 1.13   |
| SanDisk   | SD7TN3Q-256G-1006  | 256 GB | 1       | 414   | 0     | 1.13   |
| Samsung   | MZMPC032HBCD-00000 | 32 GB  | 13      | 440   | 78    | 1.13   |
| Intel     | SSDMAEMC040G2      | 40 GB  | 1       | 414   | 0     | 1.13   |
| Samsung   | MZ7LN256HCHP-000F0 | 256 GB | 2       | 413   | 0     | 1.13   |
| SanDisk   | SD6SF1M256G1022    | 256 GB | 2       | 413   | 0     | 1.13   |
| Toshiba   | THNSNJ128GCSU      | 128 GB | 16      | 413   | 0     | 1.13   |
| Team      | L3 SSD             | 120 GB | 4       | 413   | 0     | 1.13   |
| Hoodisk   | SSD                | 16 GB  | 2       | 412   | 0     | 1.13   |
| SK hynix  | SC300 SATA         | 512 GB | 2       | 411   | 0     | 1.13   |
| ADATA     | SP920SS            | 256 GB | 10      | 463   | 5     | 1.13   |
| Kingston  | SM2280S3240G       | 240 GB | 2       | 410   | 0     | 1.13   |
| SanDisk   | Ultra II           | 250 GB | 4       | 410   | 0     | 1.12   |
| Kingston  | RBUSMS180DS3128GH  | 128 GB | 2       | 410   | 0     | 1.12   |
| SanDisk   | SD9TB8W1T001001    | 1 TB   | 4       | 410   | 0     | 1.12   |
| SanDisk   | SDSSDH31000G       | 1 TB   | 15      | 410   | 0     | 1.12   |
| WDC       | WDS100T1B0A-00H9H0 | 1 TB   | 16      | 409   | 0     | 1.12   |
| Samsung   | MZ7TE128HMGR-000L1 | 128 GB | 10      | 408   | 0     | 1.12   |
| Samsung   | MZMPC128HBFU-00000 | 128 GB | 5       | 408   | 0     | 1.12   |
| Samsung   | MZMTE512HMHP-000L1 | 512 GB | 2       | 408   | 0     | 1.12   |
| SanDisk   | SDSSDHP128G        | 128 GB | 39      | 434   | 27    | 1.12   |
| Phison    | S10C-512G-PHISO... | 512 GB | 1       | 406   | 0     | 1.11   |
| SK hynix  | SC308 SATA         | 512 GB | 6       | 540   | 142   | 1.11   |
| Samsung   | MZHPV256HDGL-000L1 | 256 GB | 3       | 406   | 0     | 1.11   |
| Transcend | TS64GMTS400S       | 64 GB  | 3       | 405   | 0     | 1.11   |
| Samsung   | SSD 850 EVO mSATA  | 250 GB | 18      | 404   | 0     | 1.11   |
| Kingston  | SVP200S3240G       | 240 GB | 3       | 404   | 0     | 1.11   |
| Corsair   | Force LE200 SSD    | 240 GB | 7       | 404   | 0     | 1.11   |
| OCZ       | VERTEX3            | 128 GB | 2       | 402   | 0     | 1.10   |
| SanDisk   | SD7SB3Q-256G-1006  | 256 GB | 6       | 402   | 0     | 1.10   |
| Samsung   | 470 Series SSD     | 64 GB  | 1       | 402   | 0     | 1.10   |
| SPCC      | 2.5" SSD           | 1 TB   | 1       | 402   | 0     | 1.10   |
| Samsung   | MZ7GE240HMGR-00003 | 240 GB | 3       | 401   | 0     | 1.10   |
| KingSpec  | MT-512             | 512 GB | 1       | 401   | 0     | 1.10   |
| Micron    | C400-MTFDDAT128MAM | 128 GB | 2       | 439   | 1034  | 1.10   |
| Samsung   | MZ7KH240HAHQ-00005 | 240 GB | 3       | 400   | 0     | 1.10   |
| ADATA     | SU635              | 960 GB | 1       | 400   | 0     | 1.10   |
| Samsung   | SSD 850 EVO mSATA  | 500 GB | 21      | 400   | 0     | 1.10   |
| Toshiba   | THNSNH060GBST      | 64 GB  | 2       | 400   | 0     | 1.10   |
| Kingston  | SHSS37A240G        | 240 GB | 39      | 411   | 1     | 1.10   |
| Smartbuy  | SSD                | 64 GB  | 7       | 399   | 0     | 1.09   |
| Toshiba   | THNSNB128GMCJ      | 128 GB | 3       | 399   | 0     | 1.09   |
| Mushkin   | MKNSSDTR480GB-3DL  | 480 GB | 1       | 398   | 0     | 1.09   |
| Samsung   | SSD PM800 TM       | 128 GB | 2       | 398   | 0     | 1.09   |
| SanDisk   | SD7SB6S-256G-1006  | 256 GB | 6       | 397   | 0     | 1.09   |
| OCZ       | SOLID3             | 120 GB | 2       | 397   | 0     | 1.09   |
| Pioneer   | APS-SL3N-1T        | 1 TB   | 1       | 396   | 0     | 1.09   |
| SPCC      | SSD110             | 64 GB  | 5       | 595   | 4     | 1.08   |
| Plextor   | PH6-CE480-L2       | 480 GB | 2       | 395   | 0     | 1.08   |
| Patriot   | Blast              | 120 GB | 12      | 394   | 0     | 1.08   |
| Kingston  | SV200S3128G        | 128 GB | 12      | 600   | 2     | 1.08   |
| Patriot   | Blast              | 240 GB | 7       | 392   | 0     | 1.08   |
| OCZ       | VERTEX2            | 180 GB | 4       | 391   | 0     | 1.07   |
| Samsung   | MZNLN512HMJP-00000 | 512 GB | 1       | 391   | 0     | 1.07   |
| SanDisk   | SDSSDP256G         | 256 GB | 13      | 424   | 2     | 1.07   |
| PNY       | CS1311 120GB SSD   | 120 GB | 5       | 389   | 0     | 1.07   |
| KingShare | M300128G           | 128 GB | 1       | 389   | 0     | 1.07   |
| OCZ       | AGILITY3           | 128 GB | 3       | 749   | 1     | 1.07   |
| SanDisk   | SD8SB8U-256G-1006  | 256 GB | 6       | 388   | 0     | 1.06   |
| Toshiba   | VX500              | 128 GB | 1       | 387   | 0     | 1.06   |
| Samsung   | MZ7LN128HCHP-000L1 | 128 GB | 5       | 387   | 0     | 1.06   |
| Samsung   | SSD PM830 mSATA    | 128 GB | 4       | 387   | 0     | 1.06   |
| Kingston  | SNV425S2128GB      | 128 GB | 3       | 863   | 3     | 1.06   |
| SanDisk   | SD6SB1M256G1002    | 256 GB | 3       | 386   | 0     | 1.06   |
| SanDisk   | SDSSDX120GG25      | 120 GB | 8       | 385   | 0     | 1.06   |
| SanDisk   | X400 M.2 2280      | 512 GB | 4       | 385   | 0     | 1.06   |
| Toshiba   | TR150              | 240 GB | 24      | 384   | 0     | 1.05   |
| OCZ       | VERTEX4            | 64 GB  | 9       | 433   | 1     | 1.05   |
| Samsung   | MZMPC128HBFU-000L1 | 128 GB | 4       | 383   | 0     | 1.05   |
| Samsung   | MMCRE28GFMXP-MVB   | 128 GB | 2       | 383   | 0     | 1.05   |
| Toshiba   | THNSNH128GBST      | 128 GB | 4       | 756   | 162   | 1.05   |
| Apacer    | AST680S            | 128 GB | 3       | 383   | 0     | 1.05   |
| Samsung   | MZNTY256HDHP-000H1 | 256 GB | 7       | 402   | 1     | 1.05   |
| Intel     | SSDSC2BW180A3      | 180 GB | 1       | 382   | 0     | 1.05   |
| FCS       | SSD                | 240 GB | 1       | 381   | 0     | 1.05   |
| Samsung   | MZNLN512HMJP-000L7 | 512 GB | 13      | 381   | 0     | 1.05   |
| Samsung   | SSD PM800 TM       | 64 GB  | 3       | 381   | 0     | 1.05   |
| Intel     | SSDSC2BB480G6      | 480 GB | 1       | 381   | 0     | 1.04   |
| Intel     | SSDSCIHF120A4H     | 120 GB | 2       | 381   | 0     | 1.04   |
| SanDisk   | Ultra II           | 500 GB | 3       | 380   | 0     | 1.04   |
| Crucial   | CT120M500SSD1      | 120 GB | 40      | 704   | 66    | 1.04   |
| Samsung   | SATA SSD           | 256 GB | 1       | 379   | 0     | 1.04   |
| Palit     | PSP120 SSD         | 120 GB | 3       | 379   | 0     | 1.04   |
| OCZ       | VERTEX3            | 90 GB  | 12      | 669   | 7     | 1.04   |
| Seagate   | STT_FTM64GX25H     | 64 GB  | 1       | 378   | 0     | 1.04   |
| Corsair   | Force 3 SSD        | 90 GB  | 5       | 378   | 0     | 1.04   |
| Samsung   | MZNTY128HDHP-000H1 | 128 GB | 9       | 377   | 0     | 1.03   |
| SanDisk   | Ultra II           | 240 GB | 25      | 398   | 1     | 1.03   |
| Kingston  | SV300S37A120G      | 120 GB | 593     | 463   | 18    | 1.03   |
| SanDisk   | SDSSDP128G         | 128 GB | 60      | 404   | 5     | 1.03   |
| SanDisk   | SD7SB6S-128G-1006  | 128 GB | 3       | 573   | 2     | 1.03   |
| Toshiba   | THNSNF256GRHS      | 128 GB | 2       | 375   | 0     | 1.03   |
| Micron    | MTFDDAK256MBF-1... | 256 GB | 5       | 374   | 0     | 1.03   |
| Apacer    | AS450              | 240 GB | 1       | 374   | 0     | 1.03   |
| Samsung   | MZYLF128HCHP-000L2 | 128 GB | 11      | 373   | 0     | 1.02   |
| Kingston  | SV100S264G         | 64 GB  | 13      | 539   | 4     | 1.02   |
| SanDisk   | SD7SN3Q256G1002    | 256 GB | 6       | 472   | 173   | 1.02   |
| ADATA     | AXNS381E-256GM-B   | 256 GB | 3       | 372   | 0     | 1.02   |
| SanDisk   | SD8SN8U512G1122    | 512 GB | 4       | 372   | 0     | 1.02   |
| Toshiba   | THNSNJ256GCSU      | 256 GB | 8       | 372   | 0     | 1.02   |
| Colorful  | SL500              | 512 GB | 1       | 371   | 0     | 1.02   |
| Intenso   | SATA3 240GB SSD    | 240 GB | 1       | 371   | 0     | 1.02   |
| Intenso   | SSD                | 512 GB | 9       | 370   | 0     | 1.02   |
| Samsung   | MZ7TY256HDHP-000L7 | 256 GB | 13      | 369   | 0     | 1.01   |
| SK hynix  | SC300 M.2 2280     | 128 GB | 1       | 369   | 0     | 1.01   |
| Samsung   | SSD SM871 2.5 7mm  | 512 GB | 3       | 920   | 104   | 1.01   |
| Intel     | SSDSC2BW240A3H     | 240 GB | 1       | 369   | 0     | 1.01   |
| Toshiba   | THNS064GE4BBDC     | 64 GB  | 2       | 369   | 0     | 1.01   |
| SPCC      | SSD                | 480 GB | 3       | 367   | 0     | 1.01   |
| Toshiba   | THNSNH512GCST      | 512 GB | 2       | 367   | 0     | 1.01   |
| Samsung   | MZRPC128HACD-000SO | 64 GB  | 4       | 367   | 0     | 1.01   |
| OCZ       | TRION100           | 240 GB | 17      | 386   | 1     | 1.01   |
| OCZ       | TRION150           | 240 GB | 7       | 367   | 0     | 1.01   |
| OCZ       | VERTEX             | 32 GB  | 3       | 602   | 1     | 1.01   |
| ADATA     | SP900              | 128 GB | 47      | 436   | 8     | 1.01   |
| OCZ       | VECTOR             | 128 GB | 6       | 368   | 3     | 1.01   |
| Intel     | SSDSC2BW240A4      | 240 GB | 31      | 652   | 3     | 1.00   |
| Kingston  | SMS200S360G        | 64 GB  | 15      | 658   | 69    | 1.00   |
| Plextor   | PX-64M3            | 64 GB  | 3       | 668   | 346   | 1.00   |
| Crucial   | CT128M550SSD3      | 128 GB | 4       | 469   | 8     | 1.00   |
| Intel     | SSDSC2CT240A3      | 240 GB | 4       | 570   | 1     | 1.00   |
| Samsung   | MZMTD512HAGL-000MV | 512 GB | 2       | 363   | 0     | 1.00   |
| SanDisk   | SD7SN6S512G1001    | 512 GB | 2       | 363   | 0     | 0.99   |
| Samsung   | SSD 860 EVO        | 4 TB   | 34      | 362   | 0     | 0.99   |
| Kingston  | SKC300S37A60G      | 64 GB  | 17      | 447   | 5     | 0.99   |
| Micron    | 5200_MTFDDAK240TDN | 240 GB | 10      | 362   | 0     | 0.99   |
| Intel     | SSDSC2BW180A3H     | 180 GB | 15      | 378   | 1     | 0.99   |
| Samsung   | MZ7LF192HCGS-000L1 | 192 GB | 11      | 361   | 0     | 0.99   |
| SanDisk   | SDSA6PM-064G-1006  | 64 GB  | 1       | 361   | 0     | 0.99   |
| Samsung   | MZNTE256HMHP-000H1 | 256 GB | 3       | 360   | 0     | 0.99   |
| SanDisk   | X400 M.2 2280      | 256 GB | 26      | 360   | 0     | 0.99   |
| Samsung   | SSD PM871b 2.5 7mm | 256 GB | 2       | 360   | 0     | 0.99   |
| ADATA     | SX900              | 64 GB  | 8       | 543   | 386   | 0.99   |
| KingShare | 230120SSD          | 128 GB | 1       | 358   | 0     | 0.98   |
| Apple     | SSD SM0256G        | 256 GB | 26      | 357   | 0     | 0.98   |
| Toshiba   | Q300               | 120 GB | 6       | 356   | 0     | 0.98   |
| ADATA     | SP310              | 128 GB | 2       | 355   | 0     | 0.97   |
| Plextor   | PX-256M6S+         | 256 GB | 1       | 355   | 0     | 0.97   |
| Samsung   | MZMPA064HMDR-00000 | 64 GB  | 3       | 355   | 0     | 0.97   |
| Intel     | SSDSC2BW240H6      | 240 GB | 14      | 395   | 1     | 0.97   |
| Kingston  | SHPM2280P2H-480G   | 480 GB | 4       | 384   | 1     | 0.97   |
| Samsung   | MZMPC128HBFU-000H1 | 128 GB | 2       | 354   | 0     | 0.97   |
| Team      | TEAML5Lite3D120G   | 120 GB | 6       | 354   | 0     | 0.97   |
| CFD       | CSSD-MG4VT         | 1 TB   | 1       | 354   | 0     | 0.97   |
| OCZ       | VERTEX460A         | 120 GB | 8       | 379   | 1     | 0.97   |
| ADATA     | SU700              | 240 GB | 1       | 353   | 0     | 0.97   |
| KingSpec  | KSD-SA25.5-016MJ   | 16 GB  | 1       | 353   | 0     | 0.97   |
| SanDisk   | SD8SN8U256G1027    | 256 GB | 1       | 353   | 0     | 0.97   |
| SanDisk   | SDSSDHII120G       | 120 GB | 37      | 352   | 0     | 0.97   |
| Samsung   | MZNLN128HCGR-000L2 | 128 GB | 3       | 352   | 0     | 0.96   |
| SK hynix  | SC300 SATA         | 256 GB | 1       | 351   | 0     | 0.96   |
| Kingston  | RBU-SC100S37128GD  | 128 GB | 2       | 351   | 0     | 0.96   |
| KingDian  | N480-240GB         | 240 GB | 1       | 351   | 0     | 0.96   |
| Crucial   | CT128M550SSD4      | 128 GB | 1       | 349   | 0     | 0.96   |
| Samsung   | MZ7LN256HAJQ-000H1 | 256 GB | 2       | 348   | 0     | 0.96   |
| Samsung   | SSD 840 EVO        | 752 GB | 4       | 348   | 0     | 0.95   |
| Toshiba   | Q300               | 240 GB | 10      | 541   | 2     | 0.95   |
| SanDisk   | SD7SN6S-512G-1006  | 512 GB | 5       | 347   | 0     | 0.95   |
| Samsung   | MZ7LN256HCHP-000L7 | 256 GB | 22      | 347   | 0     | 0.95   |
| OCZ       | ARC100             | 480 GB | 6       | 348   | 1     | 0.95   |
| Toshiba   | THNSNX024GMNT      | 24 GB  | 2       | 346   | 0     | 0.95   |
| SanDisk   | SD8TB8U256G1001    | 256 GB | 12      | 345   | 0     | 0.95   |
| Advantech | SQF-S25M4-32G-S9E  | 32 GB  | 1       | 345   | 0     | 0.95   |
| Vaseky    | v800-128G          | 128 GB | 1       | 344   | 0     | 0.94   |
| Plextor   | PH6-CE120-G        | 120 GB | 3       | 344   | 0     | 0.94   |
| Intel     | SSDSC2BA400G4      | 400 GB | 3       | 344   | 0     | 0.94   |
| SanDisk   | SD6SF1M128G1022I   | 128 GB | 2       | 446   | 1     | 0.94   |
| Kingston  | RBU-SNS8151S396GG  | 96 GB  | 3       | 434   | 3     | 0.94   |
| Intenso   | SSD M.2 HIGH       | 120 GB | 1       | 341   | 0     | 0.93   |
| Goodram   | IRP-SSDPR-S25B-240 | 240 GB | 2       | 340   | 0     | 0.93   |
| Intel     | SSDSCKJW120H6      | 120 GB | 1       | 339   | 0     | 0.93   |
| Goodram   | C40                | 120 GB | 7       | 369   | 2     | 0.93   |
| Kingston  | SMS200S3120G       | 120 GB | 27      | 359   | 30    | 0.93   |
| Transcend | TSA                | 480 GB | 1       | 337   | 0     | 0.93   |
| OCZ       | AGILITY3           | 90 GB  | 5       | 450   | 1     | 0.92   |
| Intel     | SSDSC2CW120A3      | 120 GB | 47      | 649   | 411   | 0.92   |
| Mushkin   | MKNSSDCR120GB-7    | 120 GB | 3       | 711   | 343   | 0.92   |
| SanDisk   | SSD i100           | 32 GB  | 5       | 336   | 0     | 0.92   |
| Corsair   | Neutron XT SSD     | 480 GB | 3       | 561   | 2     | 0.92   |
| Plextor   | PX-512M6S+         | 512 GB | 1       | 336   | 0     | 0.92   |
| WDC       | WDS200T2B0A        | 2 TB   | 2       | 335   | 0     | 0.92   |
| Crucial   | CT1050MX300SSD4    | 1 TB   | 8       | 346   | 10    | 0.92   |
| Intel     | SSDSC2KG480G7      | 480 GB | 3       | 341   | 3     | 0.92   |
| SK hynix  | SC300 M.2 2280     | 512 GB | 1       | 333   | 0     | 0.91   |
| Kingston  | SM2280S3G2480G     | 480 GB | 3       | 428   | 42    | 0.91   |
| OCZ       | VECTOR150          | 240 GB | 7       | 363   | 1     | 0.91   |
| KingFast  | SSD                | 32 GB  | 1       | 332   | 0     | 0.91   |
| Crucial   | CT240M500SSD1      | 240 GB | 47      | 591   | 118   | 0.91   |
| Micron    | 1100_MTFDDAK512TBN | 512 GB | 18      | 493   | 62    | 0.91   |
| Intel     | SSDSA2M040G2GC     | 40 GB  | 9       | 831   | 4     | 0.91   |
| Samsung   | MZ7TE128HMGR-000H1 | 128 GB | 5       | 330   | 0     | 0.91   |
| SanDisk   | SD8SBBU240G1122    | 240 GB | 3       | 330   | 0     | 0.90   |
| Samsung   | MZMTE128HMGR-000MV | 128 GB | 5       | 330   | 0     | 0.90   |
| Kingston  | RBUSNS4180S364GJ   | 64 GB  | 1       | 330   | 0     | 0.90   |
| SanDisk   | SDSSDHII240G       | 240 GB | 34      | 344   | 1     | 0.90   |
| China     | SH00R480GB         | 480 GB | 4       | 328   | 0     | 0.90   |
| Crucial   | CT250MX200SSD1     | 250 GB | 26      | 328   | 0     | 0.90   |
| ZOTAC     | ZTSSD-S11-240G-P   | 240 GB | 1       | 328   | 0     | 0.90   |
| SanDisk   | X400 M.2 2280      | 128 GB | 10      | 328   | 0     | 0.90   |
| SanDisk   | SD9SN8W512G1002    | 512 GB | 4       | 328   | 0     | 0.90   |
| Crucial   | CT275MX300SSD1     | 275 GB | 71      | 386   | 66    | 0.90   |
| Crucial   | CT1050MX300SSD1    | 1 TB   | 29      | 482   | 49    | 0.89   |
| Mushkin   | MKNSSDCR240GB-7    | 240 GB | 1       | 326   | 0     | 0.89   |
| Seagate   | SSD                | 1 TB   | 3       | 325   | 0     | 0.89   |
| Kingston  | SV300S37A240G      | 240 GB | 173     | 357   | 12    | 0.89   |
| Samsung   | MZ7TE128HMGR-00000 | 128 GB | 4       | 325   | 0     | 0.89   |
| OCZ       | VERTEX             | 64 GB  | 2       | 324   | 0     | 0.89   |
| KingFast  | SSD                | 64 GB  | 4       | 324   | 1     | 0.89   |
| Corsair   | Force GS           | 240 GB | 5       | 1343  | 25    | 0.89   |
| SanDisk   | SD8SB8U128G1001    | 128 GB | 2       | 324   | 0     | 0.89   |
| Kingston  | SM2280S3120G       | 120 GB | 5       | 324   | 0     | 0.89   |
| Micron    | M600_MTFDDAY512MBF | 512 GB | 1       | 323   | 0     | 0.89   |
| Toshiba   | SSD0256XQC82X20... | 256 GB | 1       | 323   | 0     | 0.89   |
| SanDisk   | SD6SF1M128G1022    | 128 GB | 1       | 323   | 0     | 0.89   |
| Kingston  | RBU-SNS8152S325... | 256 GB | 1       | 323   | 0     | 0.89   |
| Kingston  | RBUSNS8180S3128GI1 | 128 GB | 5       | 323   | 0     | 0.88   |
| Samsung   | SSD 750 EVO        | 120 GB | 46      | 321   | 0     | 0.88   |
| OCZ       | VERTEX3 LP         | 64 GB  | 1       | 320   | 0     | 0.88   |
| Team      | TIM3F49256GMBA04MA | 256 GB | 1       | 320   | 0     | 0.88   |
| Kingston  | SM2280S3G2240G     | 240 GB | 5       | 320   | 0     | 0.88   |
| Samsung   | SSD 840 EVO 500... | 500 GB | 6       | 320   | 0     | 0.88   |
| Kingston  | SVP180S264G        | 64 GB  | 1       | 320   | 0     | 0.88   |
| Intel     | SSDSC2BW080A4      | 80 GB  | 5       | 319   | 0     | 0.88   |
| SanDisk   | SDSSDXP120G        | 120 GB | 2       | 319   | 0     | 0.88   |
| Samsung   | MZNTY256HDHP-000   | 256 GB | 1       | 319   | 0     | 0.87   |
| Samsung   | MZ7LN256HMJP-000L7 | 256 GB | 3       | 318   | 0     | 0.87   |
| Intel     | SSDSC2BB012T7O     | 1.2 TB | 1       | 317   | 0     | 0.87   |
| SanDisk   | SD7TB3Q-128G-1006  | 128 GB | 4       | 340   | 8     | 0.87   |
| Team      | TEAML5Lite3D1T     | 1 TB   | 3       | 317   | 0     | 0.87   |
| SanDisk   | SSD i110           | 64 GB  | 1       | 317   | 0     | 0.87   |
| Samsung   | MZYTN512HDJH-000L2 | 512 GB | 3       | 316   | 0     | 0.87   |
| Samsung   | MMCRE28G8MXP-0VBL1 | 128 GB | 3       | 315   | 0     | 0.87   |
| Samsung   | SSD PM810 FDE 2.5" | 256 GB | 2       | 403   | 129   | 0.87   |
| Samsung   | MZ7TD128HAFV-00000 | 128 GB | 4       | 315   | 0     | 0.86   |
| Toshiba   | THNSNJ512G8NY      | 512 GB | 1       | 315   | 0     | 0.86   |
| Crucial   | CT250MX500SSD4N    | 250 GB | 2       | 314   | 0     | 0.86   |
| Toshiba   | THNSNF128GCSS      | 128 GB | 6       | 314   | 0     | 0.86   |
| Samsung   | MZYTY128HDHP-000L2 | 128 GB | 7       | 313   | 0     | 0.86   |
| Phison    | 256GB PS3110-S10C  | 256 GB | 2       | 312   | 0     | 0.86   |
| Samsung   | SSD PM810 2.5"     | 128 GB | 1       | 1560  | 4     | 0.86   |
| SanDisk   | SSD U100           | 128 GB | 1       | 312   | 0     | 0.86   |
| OCZ       | VERTEX2            | 240 GB | 2       | 311   | 0     | 0.85   |
| Aura      | Pro S MB258        | 1 TB   | 1       | 310   | 0     | 0.85   |
| Micron    | MTFDDAV512TBN-1... | 512 GB | 1       | 620   | 1     | 0.85   |
| ADATA     | SP600              | 32 GB  | 11      | 309   | 0     | 0.85   |
| KingSpec  | P3-2TB             | 2 TB   | 2       | 309   | 0     | 0.85   |
| Toshiba   | THNSNJ256G8NY      | 256 GB | 10      | 333   | 1     | 0.85   |
| ADATA     | SX900              | 128 GB | 14      | 692   | 441   | 0.85   |
| Phison    | 128GB PS3110-S10C  | 128 GB | 2       | 308   | 0     | 0.84   |
| SanDisk   | SD7SB7S512G1001    | 512 GB | 2       | 308   | 0     | 0.84   |
| Micron    | 1100_MTFDDAK2T0TBN | 2 TB   | 4       | 307   | 0     | 0.84   |
| PNY       | CS900 960GB SSD    | 960 GB | 10      | 307   | 0     | 0.84   |
| SanDisk   | SDSSDHP064G        | 64 GB  | 9       | 306   | 0     | 0.84   |
| ADATA     | SP600              | 512 GB | 1       | 305   | 0     | 0.84   |
| Samsung   | MZMTE256HMHP-00005 | 256 GB | 1       | 304   | 0     | 0.83   |
| Toshiba   | THNSNC128GBSJ      | 128 GB | 1       | 303   | 0     | 0.83   |
| SK hynix  | HFS512G39MND-3310A | 512 GB | 1       | 303   | 0     | 0.83   |
| SMI       | L06B B0KB          | 240 GB | 1       | 302   | 0     | 0.83   |
| SanDisk   | SSD PLUS 480 GB    | 480 GB | 12      | 409   | 9     | 0.83   |
| Mushkin   | MKNSSDAT240GB-DX   | 240 GB | 1       | 299   | 0     | 0.82   |
| Ramsta    | SSD S800           | 120 GB | 1       | 299   | 0     | 0.82   |
| Samsung   | MZ7LM480HMHQ-000MV | 480 GB | 2       | 298   | 0     | 0.82   |
| SanDisk   | SD7SB2Q-512G-1006  | 512 GB | 6       | 348   | 4     | 0.82   |
| Ramaxel   | RDM-II XM020C      | 24 GB  | 1       | 298   | 0     | 0.82   |
| Samsung   | MZNLN512HMJP-000H1 | 512 GB | 5       | 298   | 0     | 0.82   |
| Kingston  | SUV400S37240G      | 240 GB | 137     | 361   | 66    | 0.82   |
| Plextor   | PX-256S3G          | 256 GB | 2       | 298   | 0     | 0.82   |
| SanDisk   | X300 2.5 7MM       | 256 GB | 1       | 297   | 0     | 0.81   |
| Plextor   | PX-128M7VG         | 128 GB | 3       | 297   | 0     | 0.81   |
| ADATA     | SP900              | 256 GB | 16      | 471   | 2     | 0.81   |
| WDC       | WDBNCE2500PNC      | 250 GB | 10      | 296   | 0     | 0.81   |
| Toshiba   | THNSNH128GCST      | 128 GB | 6       | 326   | 1     | 0.81   |
| Intenso   | SSD Sata III       | 250 GB | 1       | 295   | 0     | 0.81   |
| Ramaxel   | RDM-II XM020C024G  | 24 GB  | 2       | 295   | 0     | 0.81   |
| Transcend | TS64GSSD340        | 64 GB  | 4       | 352   | 252   | 0.81   |
| Samsung   | MZNLN128HAHQ-00000 | 128 GB | 4       | 295   | 0     | 0.81   |
| Samsung   | MZ7KM960HMJP-00005 | 960 GB | 2       | 294   | 0     | 0.81   |
| Samsung   | MZAPF032HCFV-000H1 | 32 GB  | 1       | 294   | 0     | 0.81   |
| Lexar     | 120GB SSD          | 120 GB | 1       | 294   | 0     | 0.81   |
| Samsung   | MZNTY256HDHP-000L7 | 256 GB | 16      | 293   | 0     | 0.80   |
| Kingston  | SNVP325S2256GB     | 256 GB | 1       | 293   | 0     | 0.80   |
| Micron    | 1100_MTFDDAK1T0TBN | 1 TB   | 8       | 388   | 8     | 0.80   |
| Samsung   | SSD RBX Series ... | 64 GB  | 1       | 292   | 0     | 0.80   |
| Transcend | TS256GSSD340       | 256 GB | 5       | 292   | 0     | 0.80   |
| WDC       | WDS500G1B0A-00H9H0 | 500 GB | 21      | 306   | 1     | 0.80   |
| Plextor   | PX-1TM8VC          | 1 TB   | 1       | 292   | 0     | 0.80   |
| WDC       | WDS100T1B0B-00AS40 | 1 TB   | 3       | 291   | 0     | 0.80   |
| Netac     | SSD                | 240 GB | 3       | 290   | 0     | 0.80   |
| Intel     | SSDSC2BW480A4      | 480 GB | 5       | 577   | 11    | 0.80   |
| Lite-On   | LCS-256L9S-11 2... | 256 GB | 8       | 289   | 0     | 0.79   |
| Samsung   | MZMPC032HBCD-000H1 | 32 GB  | 11      | 288   | 0     | 0.79   |
| Kingston  | RBU-SNS8152S312... | 128 GB | 3       | 288   | 0     | 0.79   |
| Micron    | MTFDDAK256MAM-1K1  | 256 GB | 3       | 288   | 0     | 0.79   |
| Samsung   | SSD PM830 2.5" 7mm | 512 GB | 2       | 594   | 505   | 0.79   |
| Intel     | SSDSC2KF256G8      | 256 GB | 1       | 287   | 0     | 0.79   |
| Intel     | SSDSC2BW120H6      | 120 GB | 21      | 313   | 4     | 0.79   |
| Samsung   | MZMPC128HBFU-000MV | 128 GB | 4       | 287   | 0     | 0.79   |
| Samsung   | MZMTD512HAGL-000L1 | 512 GB | 4       | 313   | 25    | 0.79   |
| OCZ       | CACHE-SYNAPSE      | 32 GB  | 1       | 286   | 0     | 0.79   |
| Patriot   | Blaze              | 64 GB  | 7       | 286   | 0     | 0.79   |
| Goodram   | SSD                | 120 GB | 42      | 287   | 1     | 0.79   |
| Toshiba   | TR150              | 120 GB | 6       | 286   | 0     | 0.79   |
| SanDisk   | SD8SBBU120G1122    | 120 GB | 7       | 286   | 0     | 0.78   |
| WDC       | WDS250G1B0A-00H9H0 | 250 GB | 23      | 325   | 45    | 0.78   |
| Kingston  | RBU-SNS8152S312... | 128 GB | 4       | 285   | 0     | 0.78   |
| Samsung   | MZHPV512HDGL-000L1 | 512 GB | 1       | 285   | 0     | 0.78   |
| Kingston  | SUV300S37A480G     | 480 GB | 3       | 285   | 0     | 0.78   |
| OCZ       | VTX3-25SAT3-120G   | 120 GB | 1       | 285   | 0     | 0.78   |
| Crucial   | CT512M550SSD1      | 512 GB | 8       | 857   | 216   | 0.78   |
| Samsung   | MZ7TE256HMHP-000H1 | 256 GB | 4       | 285   | 0     | 0.78   |
| Lenovo    | Thinklife ST600... | 256 GB | 1       | 285   | 0     | 0.78   |
| Corsair   | CSSD-V60GB2        | 64 GB  | 2       | 433   | 4     | 0.78   |
| SanDisk   | SD9SB8W128G1001    | 128 GB | 4       | 285   | 0     | 0.78   |
| Samsung   | MMCRE28G5MXP-0VBH1 | 128 GB | 2       | 284   | 0     | 0.78   |
| Intel     | SSDMCEAC240B3      | 240 GB | 1       | 284   | 0     | 0.78   |
| Samsung   | SSD 860 EVO mSATA  | 500 GB | 12      | 284   | 0     | 0.78   |
| Corsair   | CMFSSD-32D1        | 32 GB  | 1       | 566   | 1     | 0.78   |
| OCZ       | OCTANE S2          | 64 GB  | 2       | 283   | 0     | 0.78   |
| Intel     | SSDSCKHW240A4      | 240 GB | 1       | 282   | 0     | 0.77   |
| Toshiba   | A100               | 240 GB | 10      | 282   | 0     | 0.77   |
| Intel     | SSDSA2BW160G3L     | 160 GB | 14      | 281   | 0     | 0.77   |
| ADATA     | SU650              | 960 GB | 1       | 281   | 0     | 0.77   |
| Kingston  | SUV300S37A120G     | 120 GB | 37      | 286   | 1     | 0.77   |
| Kingston  | SHFS37A240G        | 240 GB | 37      | 311   | 193   | 0.77   |
| Goodram   | SSDPR-CX400-01T    | 1 TB   | 5       | 280   | 0     | 0.77   |
| ADATA     | SSD DP900 512GB... | 512 GB | 3       | 1255  | 678   | 0.77   |
| Toshiba   | THNSNC128GMLJ      | 128 GB | 2       | 279   | 0     | 0.77   |
| Kingston  | SMS100S232G        | 32 GB  | 1       | 279   | 0     | 0.76   |
| Samsung   | MZNTY256HDHP-000L2 | 256 GB | 5       | 279   | 0     | 0.76   |
| OCZ       | TRION100           | 120 GB | 10      | 322   | 2     | 0.76   |
| Plextor   | PX-256M5Pro        | 256 GB | 13      | 278   | 0     | 0.76   |
| SanDisk   | SD8TB8U512G1001    | 512 GB | 4       | 278   | 0     | 0.76   |
| Apacer    | AS330              | 120 GB | 3       | 277   | 0     | 0.76   |
| Samsung   | SSD PM871a M.2 ... | 512 GB | 1       | 277   | 0     | 0.76   |
| PNY       | CS2211 480GB SSD   | 480 GB | 1       | 277   | 0     | 0.76   |
| OCZ       | ARC100             | 120 GB | 13      | 276   | 0     | 0.76   |
| Samsung   | MZNLN256HMHQ-000H1 | 256 GB | 17      | 276   | 0     | 0.76   |
| SanDisk   | SD8SN8U512G1002    | 512 GB | 19      | 275   | 0     | 0.75   |
| Corsair   | Neutron SSD        | 64 GB  | 5       | 527   | 3     | 0.75   |
| ADATA     | SP600NS34          | 256 GB | 1       | 274   | 0     | 0.75   |
| SanDisk   | SDSSDH31024G       | 1 TB   | 16      | 273   | 0     | 0.75   |
| SanDisk   | SD8SB8U128G1002    | 128 GB | 1       | 273   | 0     | 0.75   |
| Samsung   | MZNLN128HCGR-00000 | 128 GB | 3       | 273   | 0     | 0.75   |
| BAITITON  | BT58SSD07S         | 120 GB | 1       | 273   | 0     | 0.75   |
| SanDisk   | SD7SN6S-256G-1006  | 256 GB | 6       | 273   | 0     | 0.75   |
| Micron    | 1100_MTFDDAK256TBN | 256 GB | 24      | 314   | 132   | 0.75   |
| Toshiba   | TR150              | 960 GB | 2       | 272   | 0     | 0.75   |
| Samsung   | MZMTE256HMHP-000MV | 256 GB | 7       | 272   | 0     | 0.75   |
| Samsung   | MZNTE256HMHP-000L7 | 256 GB | 2       | 272   | 0     | 0.75   |
| Micron    | M600_MTFDDAV256MBF | 256 GB | 10      | 271   | 0     | 0.74   |
| Samsung   | MZMPC256HBGJ-00000 | 256 GB | 1       | 270   | 0     | 0.74   |
| SanDisk   | SDSSDA960G         | 960 GB | 5       | 270   | 0     | 0.74   |
| Crucial   | CT750MX300SSD1     | 752 GB | 15      | 270   | 0     | 0.74   |
| Gigabyte  | GP-GSTFS30512GTTD  | 512 GB | 4       | 269   | 0     | 0.74   |
| SK hynix  | SC311 SATA         | 256 GB | 52      | 274   | 1     | 0.74   |
| Toshiba   | THNSNH060GMCT      | 64 GB  | 1       | 269   | 0     | 0.74   |
| HP        | SSD S700           | 120 GB | 6       | 350   | 1     | 0.74   |
| SanDisk   | SDSSDXPS960G       | 960 GB | 5       | 423   | 67    | 0.73   |
| Samsung   | MZNLN512HCJH-000L1 | 512 GB | 3       | 266   | 0     | 0.73   |
| Intel     | SSDSC2CW060A3      | 64 GB  | 14      | 656   | 508   | 0.73   |
| Apple     | SSD TS064C         | 64 GB  | 4       | 265   | 0     | 0.73   |
| TWINMOS   | SSD SATA2.5"-120GB | 120 GB | 1       | 265   | 0     | 0.73   |
| Intenso   | SATA III SSD       | 120 GB | 25      | 270   | 1     | 0.73   |
| Intel     | SSDPAMM0008G1      | 8 GB   | 1       | 265   | 0     | 0.73   |
| imation   | M.2 SATA3 256GB... | 256 GB | 1       | 264   | 0     | 0.73   |
| Kingston  | SUV400S37120G      | 120 GB | 159     | 290   | 58    | 0.73   |
| Micron    | MTFDDAK480TDT      | 480 GB | 3       | 264   | 0     | 0.72   |
| Kingston  | RBUSNS8180S3128GI  | 128 GB | 3       | 264   | 0     | 0.72   |
| China     | SATA SSD           | 20 GB  | 14      | 286   | 1     | 0.72   |
| Hikvision | HKVSN HS-SSD-E1... | 128 GB | 1       | 263   | 0     | 0.72   |
| Team      | L5 LITE SSD        | 120 GB | 3       | 263   | 0     | 0.72   |
| SPCC      | SSD                | 2 TB   | 1       | 263   | 0     | 0.72   |
| Samsung   | MZMTE256HMHP-000L1 | 256 GB | 4       | 262   | 0     | 0.72   |
| SanDisk   | SD6SB2M512G1001    | 512 GB | 1       | 262   | 0     | 0.72   |
| Apple     | SSD TS128C         | 121 GB | 6       | 353   | 1     | 0.72   |
| Apacer    | A7202              | 64 GB  | 1       | 262   | 0     | 0.72   |
| Samsung   | SSD 883 DCT        | 480 GB | 5       | 262   | 0     | 0.72   |
| Transcend | TS1TSSD220Q        | 1 TB   | 1       | 261   | 0     | 0.72   |
| SK hynix  | SC311 SATA         | 512 GB | 19      | 272   | 55    | 0.72   |
| Micron    | MTFDDAT128MAM-1J2  | 128 GB | 3       | 312   | 718   | 0.72   |
| SK hynix  | SC313 HFS256G39... | 256 GB | 1       | 261   | 0     | 0.72   |
| Samsung   | MZ7TE256HMHP-000L2 | 256 GB | 1       | 260   | 0     | 0.71   |
| SanDisk   | SD9TB8W256G1001    | 256 GB | 8       | 260   | 0     | 0.71   |
| TREKSTOR  | TREKSTORSSD256GB   | 250 GB | 1       | 260   | 0     | 0.71   |
| EAGET     | S500 SSD           | 128 GB | 1       | 259   | 0     | 0.71   |
| SanDisk   | SD5SG2256G1052E    | 256 GB | 5       | 392   | 1     | 0.71   |
| Kingston  | SHFS37A120G        | 120 GB | 124     | 346   | 223   | 0.71   |
| Intel     | SSDSC2BW180H6      | 180 GB | 2       | 257   | 0     | 0.71   |
| SanDisk   | SSD i100           | 16 GB  | 8       | 273   | 1     | 0.71   |
| Intel     | SSDSC2BW120A4      | 120 GB | 41      | 333   | 1     | 0.71   |
| Samsung   | SSD PM810 TM       | 64 GB  | 1       | 257   | 0     | 0.70   |
| Micron    | C400-MTFDDAK256MAM | 256 GB | 4       | 334   | 758   | 0.70   |
| Micron    | MTFDDAK256TBN-1... | 256 GB | 6       | 256   | 0     | 0.70   |
| Micron    | 5100_MTFDDAK960TCB | 960 GB | 1       | 256   | 0     | 0.70   |
| Drevo     | X1 Pro             | 512 GB | 1       | 255   | 0     | 0.70   |
| Intel     | SSDSC2CT180A4      | 180 GB | 8       | 255   | 0     | 0.70   |
| SanDisk   | SD9SB8W256G1002    | 256 GB | 1       | 254   | 0     | 0.70   |
| Samsung   | MZ7TY128HDHP-00000 | 128 GB | 4       | 254   | 0     | 0.70   |
| PNY       | CS900 480GB SSD    | 480 GB | 17      | 254   | 0     | 0.70   |
| HP        | SSD S700 Pro       | 512 GB | 3       | 254   | 0     | 0.70   |
| Samsung   | SSD PM871b 2.5 7mm | 512 GB | 3       | 253   | 0     | 0.70   |
| Samsung   | MZNTY256HDHP-00000 | 256 GB | 6       | 253   | 0     | 0.70   |
| Crucial   | CT525MX300SSD1     | 528 GB | 87      | 334   | 122   | 0.69   |
| China     | LS 256G M300       | 256 GB | 1       | 252   | 0     | 0.69   |
| Apple     | SSD SD128E         | 121 GB | 3       | 252   | 0     | 0.69   |
| SanDisk   | SDSSDH32000G       | 2 TB   | 6       | 251   | 0     | 0.69   |
| OCZ       | VECTOR150          | 120 GB | 10      | 251   | 0     | 0.69   |
| Goodram   | C50                | 120 GB | 3       | 251   | 0     | 0.69   |
| Toshiba   | THNSFJ256GMCT      | 256 GB | 1       | 251   | 0     | 0.69   |
| Samsung   | SSD PM800 TH       | 64 GB  | 1       | 251   | 0     | 0.69   |
| Intel     | SSDSCKJW180H6      | 180 GB | 3       | 250   | 0     | 0.69   |
| Seagate   | SSD                | 250 GB | 4       | 250   | 0     | 0.69   |
| ADATA     | SU800NS38          | 128 GB | 10      | 250   | 0     | 0.69   |
| Corsair   | Force LE SSD       | 120 GB | 4       | 250   | 0     | 0.69   |
| Samsung   | SSD 860 PRO        | 4 TB   | 2       | 250   | 0     | 0.69   |
| Intel     | SSDSCKHF240A4L     | 240 GB | 2       | 306   | 554   | 0.68   |
| Micron    | C400-MTFDDAC064MAM | 64 GB  | 3       | 249   | 0     | 0.68   |
| Corsair   | Force LE SSD       | 480 GB | 3       | 249   | 0     | 0.68   |
| Team      | T2535T240G         | 240 GB | 3       | 249   | 0     | 0.68   |
| Seagate   | BarraCuda SSD Z... | 250 GB | 10      | 248   | 0     | 0.68   |
| Samsung   | MZMTD256HAGM-000L1 | 256 GB | 4       | 248   | 0     | 0.68   |
| WDC       | WDS250G2B0B-00YS70 | 250 GB | 26      | 248   | 0     | 0.68   |
| Crucial   | CT250MX200SSD3     | 250 GB | 4       | 248   | 0     | 0.68   |
| WDC       | WDS120G1G0B-00RC30 | 120 GB | 17      | 247   | 0     | 0.68   |
| Toshiba   | THNSNJ512GCSU      | 512 GB | 3       | 247   | 0     | 0.68   |
| SanDisk   | SD8SN8U-256G-1006  | 256 GB | 44      | 272   | 94    | 0.68   |
| Pioneer   | APS-SL3N-512       | 512 GB | 5       | 246   | 0     | 0.67   |
| SK hynix  | HFS256G39TNH-73A0A | 256 GB | 5       | 245   | 357   | 0.67   |
| Plextor   | PX-128M7VC         | 128 GB | 5       | 245   | 0     | 0.67   |
| Goodram   | SSDPR-CL100-480-G2 | 480 GB | 7       | 245   | 0     | 0.67   |
| Intel     | SSDSA1MH080G1GN    | 80 GB  | 1       | 244   | 0     | 0.67   |
| SanDisk   | SD8SN8U128G1002    | 128 GB | 8       | 244   | 0     | 0.67   |
| SK hynix  | SC311 SATA         | 128 GB | 35      | 244   | 0     | 0.67   |
| Corsair   | Neutron XTI SSD    | 240 GB | 2       | 243   | 0     | 0.67   |
| Kingston  | SA400S37 120G      | 120 GB | 1       | 242   | 0     | 0.66   |
| Phison    | SATA SSD           | 64 GB  | 4       | 241   | 0     | 0.66   |
| G.Skill   | FM-25S3-120GBP3    | 120 GB | 1       | 241   | 0     | 0.66   |
| Samsung   | MZNTY128HDHP-00000 | 128 GB | 9       | 241   | 0     | 0.66   |
| ADATA     | SSD S599           | 64 GB  | 3       | 241   | 0     | 0.66   |
| VENO S... | SSD                | 240 GB | 1       | 241   | 0     | 0.66   |
| WDC       | WDS240G1G0A-00SS50 | 240 GB | 24      | 240   | 0     | 0.66   |
| Crucial   | M4-CT512M4SSD1     | 512 GB | 3       | 666   | 102   | 0.66   |
| OCZ       | AGILITY4           | 256 GB | 9       | 413   | 39    | 0.66   |
| HP        | VK0240GDJXU        | 240 GB | 1       | 238   | 0     | 0.65   |
| Plextor   | PX-512M5P          | 512 GB | 1       | 238   | 0     | 0.65   |
| China     | SATA SSD           | 480 GB | 14      | 238   | 0     | 0.65   |
| Crucial   | M4-CT128M4SSD3     | 128 GB | 1       | 238   | 0     | 0.65   |
| Samsung   | MZ7LF120HCHP-000L1 | 120 GB | 5       | 238   | 0     | 0.65   |
| Phison    | SATA SSD           | 128 GB | 8       | 237   | 0     | 0.65   |
| Samsung   | MZNTY128HDHP-000L1 | 128 GB | 15      | 237   | 0     | 0.65   |
| Gigabyte  | GP-GSTFS30256GTTD  | 256 GB | 2       | 237   | 0     | 0.65   |
| Toshiba   | THNSNJ512GDNU A    | 512 GB | 2       | 237   | 0     | 0.65   |
| Super ... | FTM1TN325H         | 1 TB   | 1       | 236   | 0     | 0.65   |
| Kingston  | MS80000058588      | 128 GB | 1       | 235   | 0     | 0.65   |
| Verbatim  | SATA-III SSD       | 128 GB | 2       | 279   | 508   | 0.64   |
| China     | SSD                | 64 GB  | 9       | 268   | 1     | 0.64   |
| Patriot   | Spark              | 128 GB | 9       | 233   | 0     | 0.64   |
| KingSpec  | P3-1TB             | 1 TB   | 5       | 232   | 0     | 0.64   |
| SanDisk   | SDSSDA240G         | 240 GB | 152     | 241   | 4     | 0.64   |
| Intel     | SSDSA2M120G2GC     | 120 GB | 2       | 1424  | 6     | 0.64   |
| Smartbuy  | SSD                | 64 GB  | 25      | 231   | 0     | 0.64   |
| Apple     | SSD SM0128G        | 121 GB | 96      | 231   | 0     | 0.64   |
| Micron    | MTFDDAK256MAM-1K12 | 256 GB | 19      | 269   | 426   | 0.64   |
| Crucial   | CT960BX200SSD1     | 960 GB | 3       | 231   | 0     | 0.63   |
| Crucial   | CT275MX300SSD4     | 275 GB | 17      | 255   | 1     | 0.63   |
| SanDisk   | SD8TN8U256G1001    | 256 GB | 8       | 231   | 0     | 0.63   |
| SPCC      | SSD                | 240 GB | 53      | 301   | 205   | 0.63   |
| Samsung   | SSD 860 QVO        | 2 TB   | 48      | 239   | 16    | 0.63   |
| Kingston  | SMS200S3240G       | 240 GB | 5       | 529   | 407   | 0.63   |
| Toshiba   | THNSNF256GMCS      | 256 GB | 2       | 229   | 0     | 0.63   |
| Samsung   | SSD 860 EVO        | 1 TB   | 461     | 229   | 1     | 0.63   |
| Kingston  | RBU-SNS8152S325... | 256 GB | 4       | 229   | 0     | 0.63   |
| SK hynix  | HFS128G3BMND-3210A | 128 GB | 4       | 228   | 0     | 0.63   |
| SanDisk   | SDSSDXPS480G       | 480 GB | 8       | 618   | 69    | 0.63   |
| Kingston  | SV200S3256G        | 256 GB | 5       | 504   | 2     | 0.63   |
| Transcend | TS128GMSA340       | 128 GB | 1       | 227   | 0     | 0.62   |
| OCZ       | VERTEX450          | 128 GB | 6       | 519   | 347   | 0.62   |
| Samsung   | MZMTD128HAFV-000L1 | 128 GB | 11      | 243   | 13    | 0.62   |
| Kingston  | USNS8180S3512GJ    | 512 GB | 1       | 227   | 0     | 0.62   |
| Intel     | SSDSC2MH250A2      | 250 GB | 1       | 227   | 0     | 0.62   |
| SanDisk   | X300 MSATA         | 128 GB | 2       | 227   | 0     | 0.62   |
| SanDisk   | SD6SB1M128G1001    | 128 GB | 4       | 226   | 0     | 0.62   |
| China     | 240GB SSD          | 240 GB | 4       | 226   | 0     | 0.62   |
| Phison    | SATA SSD           | 240 GB | 18      | 226   | 0     | 0.62   |
| Verbatim  | Vi500 S3 120GB SSD | 120 GB | 6       | 226   | 0     | 0.62   |
| Corsair   | Performance Pro    | 128 GB | 2       | 227   | 1     | 0.62   |
| Samsung   | MMCRE28G5MXP-MVB   | 128 GB | 1       | 225   | 0     | 0.62   |
| BlitzWolf | BW-D1              | 120 GB | 1       | 225   | 0     | 0.62   |
| Samsung   | MZNTN512HDJH-00007 | 512 GB | 1       | 225   | 0     | 0.62   |
| Vaseky    | V800-240G          | 240 GB | 3       | 225   | 0     | 0.62   |
| Samsung   | MZNTE128HMGR-000L1 | 128 GB | 1       | 224   | 0     | 0.62   |
| Kingston  | SUV300S37A240G     | 240 GB | 15      | 263   | 1     | 0.62   |
| Plextor   | PX-G512M6eA        | 512 GB | 1       | 224   | 0     | 0.61   |
| Transcend | TS512GSSD370       | 512 GB | 4       | 223   | 0     | 0.61   |
| Kingston  | SVP200S37A90G      | 90 GB  | 2       | 223   | 0     | 0.61   |
| SK hynix  | HFS256G39MND-3310A | 256 GB | 2       | 222   | 0     | 0.61   |
| Micron    | MTFDDAK1T0TBN-1... | 1 TB   | 2       | 222   | 0     | 0.61   |
| Phison    | S11-64G-PHISON-... | 64 GB  | 1       | 221   | 0     | 0.61   |
| AMD       | R3SL240G           | 240 GB | 9       | 319   | 29    | 0.61   |
| BHT       | WR202HH032G E70... | 32 GB  | 5       | 221   | 0     | 0.61   |
| Transcend | TS240GSSD220S      | 240 GB | 23      | 249   | 1     | 0.61   |
| ASUS      | S-128G1BYB00LP     | 128 GB | 1       | 221   | 0     | 0.61   |
| Micron    | 1300 SATA          | 1 TB   | 2       | 220   | 0     | 0.60   |
| Hikvision | HS-SSD-E100N 256G  | 256 GB | 2       | 220   | 0     | 0.60   |
| Samsung   | SSD 860 EVO        | 250 GB | 421     | 221   | 1     | 0.60   |
| Hikvision | HS-SSD-C100 960G   | 960 GB | 1       | 219   | 0     | 0.60   |
| SanDisk   | SD6SB1M-128G-1006  | 128 GB | 6       | 237   | 2     | 0.60   |
| Transcend | TS32GSSD340        | 32 GB  | 1       | 219   | 0     | 0.60   |
| Samsung   | MZNTE128HMGR-000SO | 128 GB | 2       | 379   | 773   | 0.60   |
| Lite-On   | PH4-CE240          | 240 GB | 2       | 218   | 0     | 0.60   |
| Samsung   | MMDPE56GFDXP-MVB   | 256 GB | 1       | 218   | 0     | 0.60   |
| Kingston  | RBU-SMSM151S324GD  | 24 GB  | 1       | 217   | 0     | 0.60   |
| Plextor   | PX-128S2G          | 128 GB | 2       | 217   | 0     | 0.60   |
| Samsung   | MMCQE28GFMUP-MVA   | 128 GB | 3       | 243   | 9     | 0.59   |
| ADATA     | XM13               | 32 GB  | 2       | 216   | 0     | 0.59   |
| WDC       | WDS200T2B0B        | 2 TB   | 2       | 216   | 0     | 0.59   |
| Seagate   | BarraCuda SSD Z... | 1 TB   | 5       | 216   | 0     | 0.59   |
| Samsung   | MZHPU256HCGL-00005 | 256 GB | 1       | 216   | 0     | 0.59   |
| TCSUNBOW  | N4                 | 120 GB | 1       | 216   | 0     | 0.59   |
| Micron    | 5100_MTFDDAK960TBY | 960 GB | 1       | 216   | 0     | 0.59   |
| Samsung   | MZNTE512HMJH-000L1 | 512 GB | 1       | 215   | 0     | 0.59   |
| Crucial   | CT250MX200SSD4     | 250 GB | 1       | 215   | 0     | 0.59   |
| SanDisk   | SDSA6GM-032G-1006  | 32 GB  | 1       | 215   | 0     | 0.59   |
| Samsung   | Portable SSD T5    | 1 TB   | 27      | 215   | 0     | 0.59   |
| Crucial   | FCCT256M4SSD1      | 256 GB | 2       | 215   | 0     | 0.59   |
| WDC       | WDS240G1G0B-00RC30 | 240 GB | 7       | 215   | 0     | 0.59   |
| Intel     | SSDSC2BF240A4L     | 240 GB | 7       | 320   | 5     | 0.59   |
| Samsung   | MZMTD128HAFV-00007 | 128 GB | 1       | 214   | 0     | 0.59   |
| Transcend | TSA                | 1 TB   | 2       | 214   | 0     | 0.59   |
| Hoodisk   | SSD                | 64 GB  | 1       | 214   | 0     | 0.59   |
| Lite-On   | LAT-128M2S         | 128 GB | 2       | 369   | 4     | 0.59   |
| OCZ       | VERTEX             | 96 GB  | 1       | 214   | 0     | 0.59   |
| HP        | SSD S700           | 500 GB | 21      | 213   | 0     | 0.59   |
| ADATA     | SP580              | 240 GB | 5       | 213   | 0     | 0.58   |
| TCSUNBOW  | X3                 | 1 TB   | 3       | 212   | 0     | 0.58   |
| DOGFISH   | SSD 256G           | 256 GB | 1       | 212   | 0     | 0.58   |
| Micron    | 5210_MTFDDAK7T6QDE | 7.6 TB | 2       | 211   | 0     | 0.58   |
| Intel     | SSDSA2M160G2GC     | 160 GB | 5       | 768   | 104   | 0.58   |
| KingSpec  | Q-360              | 360 GB | 6       | 210   | 0     | 0.58   |
| Intenso   | SSD                | 256 GB | 18      | 210   | 0     | 0.58   |
| Kingston  | SUV500M8480G       | 480 GB | 4       | 210   | 0     | 0.58   |
| Micron    | 5100_MTFDDAV960TBY | 960 GB | 2       | 210   | 0     | 0.58   |
| Samsung   | MZ7LN128HAHQ-000H1 | 128 GB | 1       | 210   | 0     | 0.58   |
| WDC       | WDS200T2B0A-00SM50 | 2 TB   | 14      | 209   | 0     | 0.57   |
| Kingston  | SKC380S3480G       | 480 GB | 1       | 208   | 0     | 0.57   |
| Samsung   | MMCRE28GQDXP-MVB   | 64 GB  | 6       | 208   | 0     | 0.57   |
| Toshiba   | THNSNJ128GCST      | 128 GB | 3       | 208   | 0     | 0.57   |
| Mushkin   | MKNSSDEC512GB      | 512 GB | 1       | 208   | 0     | 0.57   |
| OCZ       | VERTEX2            | 50 GB  | 2       | 309   | 320   | 0.57   |
| Team      | L5 SSD             | 120 GB | 1       | 207   | 0     | 0.57   |
| SanDisk   | SD9SN8W128G1102    | 128 GB | 8       | 207   | 0     | 0.57   |
| Palit     | PH120 SSD          | 120 GB | 1       | 207   | 0     | 0.57   |
| SanDisk   | SDSSDH3250G        | 250 GB | 18      | 207   | 0     | 0.57   |
| Samsung   | SSD PM871b M.2 ... | 128 GB | 4       | 206   | 0     | 0.57   |
| Samsung   | MZMPA024HMCD-000L1 | 24 GB  | 4       | 233   | 5     | 0.57   |
| Smartbuy  | m.2 S10-2280T      | 128 GB | 1       | 206   | 0     | 0.57   |
| JAMESD... | JD240LE            | 240 GB | 1       | 206   | 0     | 0.56   |
| SUNEAST   | SSD SE800          | 1 TB   | 1       | 206   | 0     | 0.56   |
| Corsair   | CSSD-F60GB2        | 64 GB  | 5       | 799   | 199   | 0.56   |
| Seagate   | ST240HM000         | 240 GB | 1       | 206   | 0     | 0.56   |
| Kingston  | SV300S37A480G      | 480 GB | 27      | 293   | 47    | 0.56   |
| SanDisk   | SDSSDA-1T00        | 1 TB   | 16      | 205   | 0     | 0.56   |
| ADATA     | SU810NS38 SATA ... | 128 GB | 3       | 205   | 0     | 0.56   |
| Kingston  | SS050S216G         | 16 GB  | 1       | 205   | 0     | 0.56   |
| SanDisk   | SD8SN8U256G1002    | 256 GB | 8       | 205   | 0     | 0.56   |
| Samsung   | MZNTE512HMJH-00000 | 512 GB | 1       | 204   | 0     | 0.56   |
| SPCC      | SSD B29            | 32 GB  | 1       | 204   | 0     | 0.56   |
| Mushkin   | MKNSSDRE1TB        | 1 TB   | 6       | 204   | 0     | 0.56   |
| SPCC      | SSD                | 64 GB  | 86      | 214   | 36    | 0.56   |
| Micron    | M550_MTFDDAV128MAY | 128 GB | 1       | 204   | 0     | 0.56   |
| GALAX     | TA1D0120A          | 120 GB | 6       | 203   | 0     | 0.56   |
| SanDisk   | SD6SF1M128GG56     | 128 GB | 1       | 203   | 0     | 0.56   |
| Samsung   | MZMTE128HMGR-000   | 128 GB | 2       | 203   | 0     | 0.56   |
| Team      | T253X2512G         | 512 GB | 10      | 202   | 0     | 0.56   |
| Smartbuy  | m.2 S11-2280S      | 128 GB | 1       | 202   | 0     | 0.56   |
| SanDisk   | SDSSDH3512G        | 512 GB | 27      | 202   | 0     | 0.56   |
| Samsung   | MZRPA128HMCD-000SO | 64 GB  | 10      | 202   | 0     | 0.56   |
| China     | L06B B0KB          | 960 GB | 1       | 202   | 0     | 0.55   |
| Team      | T253TD001T         | 1 TB   | 3       | 202   | 0     | 0.55   |
| Samsung   | Portable SSD T5    | 2 TB   | 6       | 201   | 0     | 0.55   |
| Hoodisk   | SSD                | 128 GB | 6       | 201   | 0     | 0.55   |
| Crucial   | CT480M500SSD1      | 480 GB | 13      | 1107  | 245   | 0.55   |
| ADATA     | IM2S3138E-128GM-B  | 128 GB | 5       | 311   | 3     | 0.55   |
| Intel     | SSDSC2KB960G8      | 960 GB | 11      | 200   | 0     | 0.55   |
| Kingston  | SVP180S2256G       | 256 GB | 1       | 200   | 0     | 0.55   |
| V-GeN     | SSD                | 240 GB | 1       | 200   | 0     | 0.55   |
| SanDisk   | SD5SF2128G1014E    | 128 GB | 2       | 200   | 0     | 0.55   |
| Crucial   | CT256M225          | 256 GB | 1       | 200   | 0     | 0.55   |
| SK hynix  | HFS512G39TND-N210A | 512 GB | 6       | 349   | 346   | 0.55   |
| Samsung   | SSD PM871b M.2 ... | 256 GB | 10      | 199   | 0     | 0.55   |
| ADATA     | SX930              | 120 GB | 4       | 198   | 0     | 0.54   |
| ADATA     | SU900              | 1 TB   | 4       | 199   | 1     | 0.54   |
| OCZ       | VERTEX PLUS        | 64 GB  | 1       | 396   | 1     | 0.54   |
| Samsung   | SSD 860 EVO        | 500 GB | 692     | 199   | 2     | 0.54   |
| SK hynix  | HFS128G32TNF-N3A0A | 128 GB | 8       | 198   | 0     | 0.54   |
| Samsung   | SSD 860 EVO mSATA  | 1 TB   | 6       | 197   | 0     | 0.54   |
| Intel     | SSDSC2KF256G8 SATA | 256 GB | 2       | 197   | 0     | 0.54   |
| WDC       | WDS200T2B0B-00YS70 | 2 TB   | 15      | 197   | 0     | 0.54   |
| HP        | SSD M700           | 120 GB | 4       | 196   | 0     | 0.54   |
| Samsung   | MZ7TY256HDHP-00000 | 256 GB | 5       | 196   | 0     | 0.54   |
| Innodisk  | 2.5" SATA SSD 3ME4 | 128 GB | 3       | 196   | 0     | 0.54   |
| SanDisk   | SSD U100           | 128 GB | 11      | 280   | 27    | 0.54   |
| Micron    | 5200_MTFDDAK960TDN | 960 GB | 1       | 195   | 0     | 0.54   |
| Smartbuy  | SSD                | 480 GB | 2       | 195   | 0     | 0.54   |
| WDC       | WDS100T2B0B-00YS70 | 1 TB   | 40      | 202   | 1     | 0.54   |
| SanDisk   | SD9SB8W512G1101    | 512 GB | 5       | 195   | 0     | 0.53   |
| Toshiba   | TR200              | 480 GB | 17      | 195   | 0     | 0.53   |
| SanDisk   | SD9SN8W256G1014    | 256 GB | 5       | 195   | 0     | 0.53   |
| Plextor   | PX-128S3G          | 128 GB | 1       | 194   | 0     | 0.53   |
| Kingston  | RBU-SC100S37240GE  | 240 GB | 1       | 194   | 0     | 0.53   |
| SanDisk   | SDSSDH3 4T00       | 4 TB   | 8       | 194   | 0     | 0.53   |
| Crucial   | CT500MX200SSD4     | 500 GB | 5       | 393   | 1     | 0.53   |
| Transcend | TS128GSSD720       | 128 GB | 3       | 194   | 0     | 0.53   |
| Vaseky    | V800-60G           | 64 GB  | 2       | 247   | 14    | 0.53   |
| Londisk   | SSD                | 960 GB | 1       | 192   | 0     | 0.53   |
| Micron    | MTFDBAK128MAG-1G1  | 128 GB | 2       | 192   | 0     | 0.53   |
| Netac     | SSD                | 120 GB | 8       | 221   | 379   | 0.53   |
| Kingston  | SKC300S37A120G     | 120 GB | 22      | 193   | 1     | 0.53   |
| WDC       | WDS250G2B0A-00SM50 | 250 GB | 72      | 191   | 0     | 0.52   |
| China     | 1TB QLC SATA SSD   | 1 TB   | 1       | 191   | 0     | 0.52   |
| OCZ       | VERTEX4            | 512 GB | 1       | 573   | 2     | 0.52   |
| Neo Forza | NFS011SA328-600... | 128 GB | 1       | 190   | 0     | 0.52   |
| Kingston  | SS100S216G         | 16 GB  | 1       | 190   | 0     | 0.52   |
| Lite-On   | CV3-CE256-11 SATA  | 256 GB | 4       | 190   | 0     | 0.52   |
| Golden... | SSD 128            | 128 GB | 1       | 190   | 0     | 0.52   |
| SK hynix  | SC210 mSATA        | 128 GB | 4       | 458   | 19    | 0.52   |
| Crucial   | CT240BX300SSD1     | 240 GB | 7       | 189   | 0     | 0.52   |
| Micron    | 5300_MTFDDAK3T8TDT | 3.8 TB | 6       | 189   | 0     | 0.52   |
| Samsung   | SSD 860 EVO M.2    | 250 GB | 53      | 189   | 0     | 0.52   |
| China     | SH00R1TB           | 1 TB   | 1       | 189   | 0     | 0.52   |
| Toshiba   | A100               | 120 GB | 6       | 188   | 0     | 0.52   |
| SPCC      | SSD                | 120 GB | 145     | 240   | 100   | 0.52   |
| Intel     | SSDSC2BW360H6      | 360 GB | 1       | 566   | 2     | 0.52   |
| Kingston  | RBUSNS8180S3512GJ  | 512 GB | 3       | 188   | 0     | 0.52   |
| Kingston  | SUV500MS480G       | 480 GB | 10      | 188   | 0     | 0.52   |
| Transcend | TS64GSSD370        | 64 GB  | 4       | 188   | 0     | 0.52   |
| SanDisk   | SDSSDH3 512G       | 512 GB | 11      | 188   | 0     | 0.52   |
| Intel     | SSDSC2KB038T8R     | 3.8 TB | 1       | 188   | 0     | 0.52   |
| Kingston  | SNV425S264GB       | 64 GB  | 6       | 815   | 6     | 0.51   |
| Intenso   | SSD Sata III       | 240 GB | 4       | 187   | 0     | 0.51   |
| WDC       | WDS500G2B0B        | 500 GB | 10      | 187   | 0     | 0.51   |
| Intel     | SSDSC2BF256A5 SATA | 256 GB | 1       | 187   | 0     | 0.51   |
| WDC       | WDS120G1G0A-00SS50 | 120 GB | 40      | 186   | 0     | 0.51   |
| SK hynix  | HFS256G39TND-N210A | 256 GB | 56      | 260   | 85    | 0.51   |
| Micron    | 1100 SATA          | 512 GB | 20      | 273   | 276   | 0.51   |
| Smartbuy  | SSD                | 120 GB | 77      | 194   | 1     | 0.51   |
| Smartbuy  | mSata              | 64 GB  | 1       | 186   | 0     | 0.51   |
| SanDisk   | SD9SN8W512G1102    | 512 GB | 3       | 185   | 0     | 0.51   |
| Micron    | MTFDDAV480TCB-1... | 480 GB | 1       | 184   | 0     | 0.51   |
| WDC       | WDS200T2G0A-00JH30 | 2 TB   | 2       | 184   | 0     | 0.51   |
| Samsung   | MZMTE512HMHP-00000 | 512 GB | 1       | 184   | 0     | 0.51   |
| SanDisk   | SDSSDA120G         | 120 GB | 126     | 194   | 27    | 0.50   |
| Integral  | V Series SATA SSD  | 120 GB | 2       | 184   | 0     | 0.50   |
| Toshiba   | THNSNH128GMCT      | 128 GB | 5       | 184   | 0     | 0.50   |
| SanDisk   | SD7SB6S256G1122    | 256 GB | 3       | 184   | 0     | 0.50   |
| Plextor   | PH6-CE120          | 120 GB | 10      | 184   | 0     | 0.50   |
| Plextor   | PX-256M5P          | 256 GB | 1       | 183   | 0     | 0.50   |
| SanDisk   | SD5SE2256G1002E    | 256 GB | 4       | 183   | 0     | 0.50   |
| SK hynix  | HFS256G32TND-N210A | 256 GB | 3       | 183   | 0     | 0.50   |
| Team      | TEAML5Lite3D240G   | 240 GB | 3       | 183   | 0     | 0.50   |
| e2e4      | SSD                | 240 GB | 2       | 183   | 0     | 0.50   |
| SanDisk   | SD8SN8U128G1001    | 128 GB | 11      | 182   | 0     | 0.50   |
| Samsung   | MZNLN256HCHP-000H1 | 256 GB | 2       | 182   | 0     | 0.50   |
| Dogfish   | SSD                | 2 TB   | 1       | 182   | 0     | 0.50   |
| WDC       | WDS500G1R0B-68A4Z0 | 500 GB | 4       | 181   | 0     | 0.50   |
| Detech    | SSD                | 120 GB | 1       | 181   | 0     | 0.50   |
| Crucial   | CT525MX300SSD4     | 528 GB | 20      | 260   | 93    | 0.50   |
| Plextor   | PX-256M5S          | 256 GB | 17      | 267   | 113   | 0.50   |
| Zheino    | CHN 25SATAA3 360   | 360 GB | 2       | 180   | 0     | 0.50   |
| Transcend | TS128GMSA740       | 128 GB | 1       | 180   | 0     | 0.50   |
| Phison    | SATA SSD           | 480 GB | 11      | 179   | 0     | 0.49   |
| SanDisk   | SD6SN1M-256G-1006  | 256 GB | 4       | 243   | 1     | 0.49   |
| ZTC       | SM201-256G         | 256 GB | 2       | 179   | 0     | 0.49   |
| ADATA     | SP550              | 480 GB | 2       | 179   | 0     | 0.49   |
| OWC       | Mercury Electra... | 480 GB | 7       | 283   | 1     | 0.49   |
| Seagate   | SSD                | 500 GB | 2       | 178   | 0     | 0.49   |
| Intel     | SSDMAEXC024G3H     | 24 GB  | 2       | 232   | 15    | 0.49   |
| Kingston  | SA400S371920G      | 1.9 TB | 2       | 177   | 0     | 0.49   |
| KingDian  | S400 XT            | 240 GB | 1       | 177   | 0     | 0.49   |
| SPCC      | SSD A20            | 64 GB  | 2       | 177   | 0     | 0.49   |
| SK hynix  | SC308 SATA         | 256 GB | 9       | 198   | 10    | 0.49   |
| Samsung   | SSD 860 EVO mSATA  | 250 GB | 22      | 176   | 0     | 0.48   |
| Samsung   | MZNLN256HAJQ-00000 | 256 GB | 11      | 176   | 0     | 0.48   |
| SanDisk   | SSD U100           | 256 GB | 5       | 239   | 1     | 0.48   |
| SanDisk   | SDSSDH3500G        | 500 GB | 20      | 176   | 0     | 0.48   |
| Samsung   | SSD 860 QVO        | 1 TB   | 175     | 177   | 1     | 0.48   |
| Crucial   | M4-CT256M4SSD3     | 256 GB | 3       | 590   | 338   | 0.48   |
| Intel     | SSDSCKGF180A4H     | 180 GB | 2       | 175   | 0     | 0.48   |
| SanDisk   | SSD U110           | 16 GB  | 30      | 175   | 0     | 0.48   |
| Vaseky    | V800-64G           | 64 GB  | 1       | 175   | 0     | 0.48   |
| ADATA     | AXNS381E-128GM-B   | 128 GB | 2       | 175   | 0     | 0.48   |
| Team      | T253X1960G         | 960 GB | 2       | 175   | 0     | 0.48   |
| BIOSTAR   | S100-240GB PLUS    | 240 GB | 1       | 175   | 0     | 0.48   |
| Lite-On   | IT LCS-128L9S-HP   | 128 GB | 7       | 174   | 0     | 0.48   |
| Micron    | MTFDDAK512MBF-1... | 512 GB | 1       | 173   | 0     | 0.48   |
| Patriot   | Blaze              | 120 GB | 7       | 173   | 0     | 0.48   |
| Samsung   | SSD 860 PRO        | 256 GB | 36      | 173   | 0     | 0.48   |
| Faspeed   | F510-120G          | 120 GB | 1       | 173   | 0     | 0.47   |
| Mushkin   | MKNSSDTR500GB      | 500 GB | 1       | 173   | 0     | 0.47   |
| Vaseky    | V800-120GB         | 120 GB | 1       | 173   | 0     | 0.47   |
| SanDisk   | SSD U100           | 32 GB  | 8       | 175   | 126   | 0.47   |
| Crucial   | CT500MX500SSD4N    | 500 GB | 3       | 172   | 0     | 0.47   |
| PNY       | SSD2SC240G1CS17... | 240 GB | 3       | 172   | 0     | 0.47   |
| BAITITON  | BT58SSD09S         | 240 GB | 3       | 248   | 1     | 0.47   |
| Kingston  | SV100S2128G        | 128 GB | 3       | 286   | 2     | 0.47   |
| SanDisk   | X600 M.2 2280 SATA | 128 GB | 8       | 171   | 0     | 0.47   |
| Kingston  | RBU-SNS8152S351... | 512 GB | 1       | 171   | 0     | 0.47   |
| Crucial   | CT960BX500SSD1     | 960 GB | 23      | 171   | 0     | 0.47   |
| Lite-On   | CV3-8D256-41 SA... | 256 GB | 4       | 171   | 0     | 0.47   |
| ADATA     | SU900              | 512 GB | 5       | 170   | 0     | 0.47   |
| SanDisk   | X300 MSATA         | 256 GB | 3       | 170   | 0     | 0.47   |
| SanDisk   | SD6SB1M256G1022I   | 256 GB | 2       | 370   | 237   | 0.47   |
| China     | SATA SSD           | 240 GB | 30      | 170   | 0     | 0.47   |
| KingFast  | SSD                | 512 GB | 7       | 169   | 0     | 0.47   |
| OCZ       | VERTEX460          | 240 GB | 3       | 169   | 0     | 0.47   |
| SanDisk   | SD9TN8W512G1001    | 512 GB | 1       | 169   | 0     | 0.47   |
| Goodram   | SSDPR-CX300-240    | 240 GB | 8       | 169   | 0     | 0.46   |
| Transcend | TS128GMTS430S      | 128 GB | 4       | 169   | 0     | 0.46   |
| Corsair   | Force LS SSD       | 64 GB  | 27      | 328   | 153   | 0.46   |
| Mushkin   | MKNSSDEC60GB       | 64 GB  | 1       | 169   | 0     | 0.46   |
| Samsung   | MZ7LN128HAHQ-000L1 | 128 GB | 4       | 168   | 0     | 0.46   |
| SK hynix  | HFS512G39TNF-N3A0A | 512 GB | 2       | 168   | 0     | 0.46   |
| SanDisk   | SSD PLUS 120 GB    | 120 GB | 31      | 199   | 1     | 0.46   |
| SanDisk   | SDLF1CRR-019T-1HA1 | 1.9 TB | 1       | 167   | 0     | 0.46   |
| Samsung   | SSD 860 EVO        | 2 TB   | 58      | 167   | 0     | 0.46   |
| WDC       | WDS500G2B0B-00YS70 | 500 GB | 89      | 178   | 12    | 0.46   |
| SanDisk   | iSSD P4            | 8 GB   | 5       | 232   | 2     | 0.46   |
| ADATA     | SSD DP900 128GB... | 128 GB | 4       | 821   | 766   | 0.46   |
| Lite-On   | IT LCS-256L9S      | 256 GB | 2       | 166   | 0     | 0.46   |
| Crucial   | CT120BX300SSD1     | 120 GB | 14      | 165   | 0     | 0.45   |
| China     | 120GB SSD          | 120 GB | 50      | 165   | 0     | 0.45   |
| Samsung   | SSD 850            | 120 GB | 36      | 165   | 0     | 0.45   |
| Phison    | SATA SSD           | 32 GB  | 1       | 165   | 0     | 0.45   |
| Plextor   | PX-AG256M6e        | 256 GB | 2       | 165   | 0     | 0.45   |
| Samsung   | MZMTD128HAFV-000   | 128 GB | 6       | 164   | 0     | 0.45   |
| Intel     | SSDSA2M080G2HP     | 80 GB  | 3       | 169   | 1     | 0.45   |
| SanDisk   | SD9SN8W256G1002    | 256 GB | 10      | 164   | 0     | 0.45   |
| China     | SATA SSD           | 128 GB | 16      | 164   | 0     | 0.45   |
| Samsung   | SSD 830 Series     | 56 GB  | 1       | 164   | 0     | 0.45   |
| Apple     | SSD SD0256F        | 256 GB | 3       | 163   | 0     | 0.45   |
| Kingston  | SUV500M8120G       | 120 GB | 8       | 163   | 0     | 0.45   |
| ADATA     | SX900              | 256 GB | 9       | 703   | 589   | 0.45   |
| GLOWAY    | STK720GS3-S7       | 720 GB | 1       | 163   | 0     | 0.45   |
| OCZ       | VERTEX460          | 120 GB | 4       | 294   | 5     | 0.45   |
| KingSpec  | T-64               | 64 GB  | 6       | 168   | 1     | 0.45   |
| V-GeN     | V-GEN02SM19EG51... | 512 GB | 1       | 162   | 0     | 0.45   |
| AMD       | R5M120G8           | 120 GB | 1       | 162   | 0     | 0.45   |
| Patriot   | Burst              | 240 GB | 66      | 162   | 0     | 0.44   |
| Apacer    | 256GB SATA Flas... | 256 GB | 1       | 162   | 0     | 0.44   |
| SanDisk   | SDSSDH3 1T02       | 1 TB   | 7       | 162   | 0     | 0.44   |
| Kingmax   | SSD                | 120 GB | 29      | 273   | 248   | 0.44   |
| GeIL      | ZENITH 240G R3     | 240 GB | 1       | 161   | 0     | 0.44   |
| WDC       | WDS500G2B0A        | 500 GB | 32      | 161   | 0     | 0.44   |
| Samsung   | SSD PM871b M.2 ... | 512 GB | 2       | 161   | 0     | 0.44   |
| WDC       | WDS500G2B0A-00SM50 | 500 GB | 200     | 162   | 1     | 0.44   |
| Goodram   | CX100              | 120 GB | 8       | 266   | 2     | 0.44   |
| Samsung   | SSD EVO 360G       | 360 GB | 1       | 161   | 0     | 0.44   |
| Intel     | SSDSCMMW240A3L     | 240 GB | 3       | 221   | 1     | 0.44   |
| Corsair   | Force LS SSD       | 240 GB | 3       | 343   | 505   | 0.44   |
| GeIL      | ZENITH R3_120GB    | 120 GB | 3       | 160   | 0     | 0.44   |
| SanDisk   | SSD i100           | 24 GB  | 24      | 193   | 44    | 0.44   |
| SanDisk   | SD8SN8U-128G-1006  | 128 GB | 40      | 199   | 103   | 0.44   |
| WDC       | WDS100T2B0A        | 1 TB   | 6       | 170   | 1     | 0.44   |
| China     | SATA3 1TB SSD      | 1 TB   | 3       | 160   | 0     | 0.44   |
| Micron    | MTFDDAV512MBF-1... | 512 GB | 4       | 160   | 0     | 0.44   |
| Samsung   | MZ7LN256HAJQ-00000 | 256 GB | 2       | 159   | 0     | 0.44   |
| Samsung   | Portable SSD T5    | 500 GB | 32      | 159   | 0     | 0.44   |
| Plextor   | PX-256M5M          | 256 GB | 4       | 158   | 0     | 0.44   |
| Mushkin   | MKNSSDSR1TB-D8     | 1 TB   | 1       | 158   | 0     | 0.43   |
| ADATA     | AXNS381E-128GM-B2  | 128 GB | 1       | 158   | 0     | 0.43   |
| Team      | TEAML5Lite3D480G   | 480 GB | 3       | 158   | 0     | 0.43   |
| Ramsta    | SSD S600           | 480 GB | 1       | 158   | 0     | 0.43   |
| PNY       | SSD2SC240G1CS11... | 240 GB | 1       | 158   | 0     | 0.43   |
| KingDian  | S280               | 480 GB | 8       | 158   | 0     | 0.43   |
| Samsung   | MZNLN128HCGR-000H1 | 128 GB | 2       | 157   | 0     | 0.43   |
| Phison    | SATA SSD           | 120 GB | 43      | 157   | 0     | 0.43   |
| Intel     | SSDSC2BF240A5L     | 240 GB | 14      | 209   | 9     | 0.43   |
| KingFast  | SSD                | 128 GB | 16      | 167   | 1     | 0.43   |
| GeIL      | ZENITH R3_240GB    | 240 GB | 1       | 157   | 0     | 0.43   |
| Lite-On   | CV1-CC128-11 2.... | 128 GB | 1       | 157   | 0     | 0.43   |
| Intel     | SSDSC2KG960G8      | 960 GB | 3       | 156   | 0     | 0.43   |
| Samgporse | SP-8 PRO           | 1 TB   | 1       | 156   | 0     | 0.43   |
| WDC       | WDS100T1R0A-68A4W0 | 1 TB   | 4       | 156   | 0     | 0.43   |
| KingFast  | SSD                | 240 GB | 5       | 155   | 0     | 0.43   |
| Samsung   | MMCRE64GFMPP-MVA   | 64 GB  | 2       | 155   | 0     | 0.43   |
| Samsung   | SSD 860 QVO        | 4 TB   | 8       | 155   | 0     | 0.43   |
| Samsung   | SSD 860 PRO        | 1 TB   | 24      | 154   | 0     | 0.42   |
| PNY       | CS900 240GB SSD    | 240 GB | 76      | 154   | 0     | 0.42   |
| Plextor   | PX-128M5S          | 128 GB | 52      | 163   | 1     | 0.42   |
| Samsung   | MZ7LM480HMHQ-00005 | 480 GB | 1       | 154   | 0     | 0.42   |
| Kingmax   | SSD                | 480 GB | 2       | 154   | 0     | 0.42   |
| Lite-On   | CV3-CE128-HP       | 128 GB | 1       | 154   | 0     | 0.42   |
| Zheino    | CHN-25SATAS3-256   | 256 GB | 2       | 154   | 0     | 0.42   |
| Crucial   | CT250MX500SSD1     | 250 GB | 134     | 154   | 16    | 0.42   |
| Team      | T253LE240G         | 240 GB | 4       | 153   | 0     | 0.42   |
| Goodram   | SSDPR-S400U-240-80 | 240 GB | 3       | 153   | 0     | 0.42   |
| Plextor   | PX-256S2C          | 256 GB | 2       | 153   | 0     | 0.42   |
| Samsung   | Portable SSD T5    | 250 GB | 6       | 153   | 0     | 0.42   |
| SPCC      | SSD162             | 120 GB | 9       | 439   | 569   | 0.42   |
| BIWIN     | SSD                | 120 GB | 4       | 153   | 0     | 0.42   |
| Toshiba   | Q300               | 960 GB | 1       | 153   | 0     | 0.42   |
| Samsung   | SSD 860 EVO M.2    | 1 TB   | 47      | 155   | 1     | 0.42   |
| Lite-On   | CV3-CE128-11 SATA  | 128 GB | 3       | 152   | 0     | 0.42   |
| SanDisk   | X400 2.5 7MM       | 128 GB | 2       | 152   | 0     | 0.42   |
| Samsung   | MZNLN512HAJQ-00000 | 512 GB | 7       | 152   | 0     | 0.42   |
| Hajaan    | SSD 256G           | 256 GB | 2       | 151   | 0     | 0.42   |
| ADATA     | SU650              | 240 GB | 72      | 166   | 1     | 0.42   |
| Samsung   | MZNLN512HAJQ-000H1 | 512 GB | 2       | 151   | 0     | 0.41   |
| Crucial   | FCCT512MX100SSD1   | 512 GB | 1       | 151   | 0     | 0.41   |
| Kingston  | SUV500M8240G       | 240 GB | 3       | 151   | 0     | 0.41   |
| WDC       | WDS100T2B0A-00SM50 | 1 TB   | 120     | 155   | 1     | 0.41   |
| Plextor   | PX-256M3           | 256 GB | 2       | 236   | 1     | 0.41   |
| Seagate   | BarraCuda 120 S... | 500 GB | 10      | 150   | 0     | 0.41   |
| PNY       | CS2040 128GB SSD   | 128 GB | 1       | 150   | 0     | 0.41   |
| SanDisk   | SD8SN8U1T001122    | 1 TB   | 2       | 150   | 0     | 0.41   |
| Innodisk  | Corp. - mSATA 3ME  | 64 GB  | 1       | 150   | 0     | 0.41   |
| Crucial   | FCCT480M500SSD1    | 480 GB | 1       | 150   | 0     | 0.41   |
| Corsair   | CSSD-F180GB2       | 180 GB | 1       | 149   | 0     | 0.41   |
| Micron    | 1300_MTFDDAK1T0TDL | 1 TB   | 2       | 149   | 0     | 0.41   |
| SPCC      | SSD                | 256 GB | 65      | 156   | 2     | 0.41   |
| SanDisk   | SSD U100           | 16 GB  | 18      | 149   | 0     | 0.41   |
| Plextor   | PX-128M6G-2242     | 128 GB | 2       | 149   | 0     | 0.41   |
| Seagate   | BarraCuda Q1 SS... | 480 GB | 1       | 149   | 0     | 0.41   |
| Advantech | SQF-SLMV2-128G-SBE | 128 GB | 1       | 148   | 0     | 0.41   |
| Kingston  | SE100S3100G        | 100 GB | 1       | 1932  | 12    | 0.41   |
| Teclast   | 256GB NA850-2280   | 256 GB | 2       | 148   | 0     | 0.41   |
| OCZ       | TRION100           | 480 GB | 4       | 247   | 2     | 0.41   |
| Toshiba   | THNSNJ512GACU      | 512 GB | 1       | 148   | 0     | 0.41   |
| Seagate   | BarraCuda SSD Z... | 2 TB   | 3       | 147   | 0     | 0.41   |
| Silico... | GSDSL256TY2AAQGCX  | 256 GB | 1       | 147   | 0     | 0.41   |
| LDLC      | SSD                | 120 GB | 9       | 249   | 15    | 0.40   |
| Kingston  | SUV500120G         | 120 GB | 26      | 162   | 5     | 0.40   |
| Apple     | SSD SD0128F        | 121 GB | 14      | 147   | 0     | 0.40   |
| Kingston  | MS80000058688      | 256 GB | 3       | 146   | 0     | 0.40   |
| Team      | T253TD480G         | 480 GB | 3       | 146   | 0     | 0.40   |
| Teclast   | 128GB S550         | 128 GB | 1       | 146   | 0     | 0.40   |
| KingDian  | S280               | 1 TB   | 5       | 146   | 0     | 0.40   |
| Intel     | SSDSC2BW480H6      | 480 GB | 4       | 284   | 15    | 0.40   |
| Intel     | SSDSC2KG240G7      | 240 GB | 1       | 146   | 0     | 0.40   |
| Kingston  | HyperX Fury 3D     | 480 GB | 2       | 146   | 0     | 0.40   |
| Plextor   | PX-512M8VC         | 512 GB | 3       | 145   | 0     | 0.40   |
| AMD       | R5SL480G           | 480 GB | 3       | 145   | 0     | 0.40   |
| Londisk   | SSD                | 120 GB | 10      | 145   | 0     | 0.40   |
| KingSpec  | ACJC2M032mSH       | 32 GB  | 2       | 145   | 0     | 0.40   |
| Netac     | SSD                | 720 GB | 4       | 145   | 0     | 0.40   |
| Samsung   | MZ-5EA2000-0D3     | 200 GB | 2       | 145   | 0     | 0.40   |
| SK hynix  | HFS256G39TNF-N3A0A | 256 GB | 5       | 145   | 0     | 0.40   |
| KingFast  | SSD                | 256 GB | 15      | 145   | 0     | 0.40   |
| Zheino    | CHN 25SATAS3 128   | 128 GB | 1       | 144   | 0     | 0.40   |
| SK hynix  | HFS128G39TND-N210A | 128 GB | 54      | 207   | 66    | 0.40   |
| Crucial   | CT1000MX500SSD4    | 1 TB   | 34      | 144   | 0     | 0.40   |
| SanDisk   | SD9SN8W256G1102    | 256 GB | 19      | 144   | 0     | 0.39   |
| Lumino... | SSD                | 256 GB | 1       | 143   | 0     | 0.39   |
| Intel     | SSDSA2CW300G3      | 304 GB | 5       | 143   | 0     | 0.39   |
| China     | ESA3SMH2MSPB120GB  | 120 GB | 1       | 143   | 0     | 0.39   |
| QUMO      | SSD                | 64 GB  | 1       | 143   | 0     | 0.39   |
| Seagate   | BarraCuda 120 S... | 1 TB   | 8       | 143   | 0     | 0.39   |
| Intel     | SSDSC2BF180A4L     | 180 GB | 9       | 184   | 2     | 0.39   |
| Kingston  | SUV500240G         | 240 GB | 39      | 149   | 32    | 0.39   |
| Lenovo    | SSD SL700 480G     | 480 GB | 2       | 142   | 0     | 0.39   |
| Toshiba   | THNSNW032GMCP      | 32 GB  | 1       | 142   | 0     | 0.39   |
| SanDisk   | X600 M.2 2280 SATA | 512 GB | 1       | 141   | 0     | 0.39   |
| Kingston  | SV300S37A-120G     | 120 GB | 1       | 141   | 0     | 0.39   |
| Toshiba   | THNSNK128GVN8      | 128 GB | 7       | 141   | 0     | 0.39   |
| KingSpec  | KSD-SA25.5-064MJ   | 64 GB  | 1       | 141   | 0     | 0.39   |
| Goodram   | SSDPR-CX300-120    | 120 GB | 10      | 141   | 0     | 0.39   |
| Toshiba   | TR200              | 240 GB | 52      | 141   | 0     | 0.39   |
| Kingston  | RBUSNS8180S3128GJ  | 128 GB | 6       | 141   | 0     | 0.39   |
| Patriot   | Burst              | 480 GB | 30      | 145   | 1     | 0.39   |
| Innodisk  | mSATA mini 3ME ... | 32 GB  | 1       | 140   | 0     | 0.39   |
| Lite-On   | CV3-8D128-HP       | 128 GB | 3       | 140   | 0     | 0.38   |
| Varro     | bulldozer-240GB    | 240 GB | 1       | 140   | 0     | 0.38   |
| SK hynix  | SC401 SATA         | 256 GB | 4       | 140   | 0     | 0.38   |
| Mushkin   | MKNSSDRW500GB      | 480 GB | 1       | 140   | 0     | 0.38   |
| Corsair   | Performance3 SSD   | 256 GB | 1       | 140   | 0     | 0.38   |
| Intel     | SSDSC2KG240G8      | 240 GB | 5       | 140   | 0     | 0.38   |
| ADATA     | SP580              | 120 GB | 16      | 139   | 0     | 0.38   |
| KingDian  | S400               | 120 GB | 15      | 139   | 0     | 0.38   |
| Intenso   | SSD                | 128 GB | 41      | 148   | 1     | 0.38   |
| Samsung   | MZNTE256HMHP-000L2 | 256 GB | 4       | 139   | 0     | 0.38   |
| ASENNO    | AS25               | 240 GB | 2       | 139   | 0     | 0.38   |
| BHT       | WR202I0064G E70... | 64 GB  | 2       | 139   | 0     | 0.38   |
| MENGMI    | SSD                | 240 GB | 1       | 139   | 0     | 0.38   |
| Plextor   | PX-G128M6e         | 128 GB | 1       | 138   | 0     | 0.38   |
| Crucial   | CT128MX100SSD1     | 128 GB | 12      | 977   | 97    | 0.38   |
| Toshiba   | THNSNH512GDNT      | 512 GB | 1       | 138   | 0     | 0.38   |
| Seagate   | BarraCuda 120 S... | 2 TB   | 2       | 138   | 0     | 0.38   |
| Vaseky    | V800-1TB           | 1 TB   | 1       | 138   | 0     | 0.38   |
| Transcend | TS480GSSD220S      | 480 GB | 8       | 205   | 382   | 0.38   |
| Intel     | SSDSC2BF180A4H     | 180 GB | 19      | 219   | 2     | 0.38   |
| WDC       | WDS500G1R0A-68A4W0 | 500 GB | 7       | 137   | 0     | 0.38   |
| Team      | T253X1120G         | 120 GB | 5       | 137   | 0     | 0.38   |
| Lite-On   | IT LMT-256L9M      | 256 GB | 2       | 137   | 0     | 0.38   |
| Samsung   | MZ7LH480HAHQ0D3    | 480 GB | 2       | 137   | 0     | 0.38   |
| China     | SATA SSD           | 120 GB | 55      | 137   | 1     | 0.38   |
| Lite-On   | L8H-256V2G-HP      | 256 GB | 10      | 136   | 0     | 0.37   |
| Toshiba   | THNSNH256GBST      | 256 GB | 2       | 136   | 0     | 0.37   |
| SanDisk   | SD9SN8W256G        | 256 GB | 4       | 136   | 0     | 0.37   |
| KingSpec  | NT-2TB             | 2 TB   | 1       | 136   | 0     | 0.37   |
| KingDian  | S400               | 480 GB | 3       | 136   | 0     | 0.37   |
| WDC       | PC SA530 SDATB8... | 1 TB   | 1       | 136   | 0     | 0.37   |
| Toshiba   | THNSNJ128GVNU      | 128 GB | 2       | 135   | 0     | 0.37   |
| Gost      | SSD240             | 240 GB | 1       | 135   | 0     | 0.37   |
| Kingston  | SA400S37120G       | 120 GB | 677     | 147   | 1     | 0.37   |
| Kingston  | SHFR200480G        | 480 GB | 2       | 261   | 590   | 0.37   |
| Corsair   | Force LE200 SSD    | 120 GB | 7       | 135   | 0     | 0.37   |
| SK hynix  | HFS128G32MND-3210A | 128 GB | 1       | 135   | 0     | 0.37   |
| Kingston  | SA400M8240G        | 240 GB | 48      | 135   | 0     | 0.37   |
| Micron    | MTFDDAK960TDT      | 960 GB | 3       | 135   | 0     | 0.37   |
| Mushkin   | MKNSSDE3240GB      | 240 GB | 2       | 134   | 0     | 0.37   |
| Goodram   | SSDPR-CX400-512    | 512 GB | 17      | 134   | 0     | 0.37   |
| SanDisk   | SSD PLUS           | 120 GB | 75      | 134   | 1     | 0.37   |
| SanDisk   | SSD PLUS 240 GB    | 240 GB | 27      | 195   | 4     | 0.37   |
| Kingston  | SA400S37           | 120 GB | 1       | 938   | 6     | 0.37   |
| Toshiba   | VX500              | 256 GB | 1       | 134   | 0     | 0.37   |
| Intel     | SSDSCKJF180A5H REF | 180 GB | 1       | 133   | 0     | 0.37   |
| Zheino    | CHN mSATA02M 256   | 256 GB | 2       | 219   | 1     | 0.37   |
| Innodisk  | DEM24-16GM41BC1... | 16 GB  | 1       | 133   | 0     | 0.37   |
| SanDisk   | SDSSDH3 1T00       | 1 TB   | 29      | 133   | 0     | 0.37   |
| Transcend | TS256GMTS400       | 256 GB | 7       | 133   | 0     | 0.37   |
| OWC       | Mercury Extreme... | 240 GB | 3       | 133   | 0     | 0.37   |
| Intel     | SSDSC2KB240G8      | 240 GB | 10      | 133   | 0     | 0.36   |
| LDLC      | F7+480GB           | 480 GB | 3       | 133   | 0     | 0.36   |
| Star D... | SATA SSD           | 960 GB | 1       | 132   | 0     | 0.36   |
| Samsung   | SSD 860 EVO M.2    | 500 GB | 69      | 132   | 0     | 0.36   |
| China     | mSATA SSD          | 128 GB | 1       | 131   | 0     | 0.36   |
| ADATA     | SU800              | 128 GB | 44      | 163   | 4     | 0.36   |
| SK hynix  | HFS256G32TNF-N3A0A | 256 GB | 5       | 130   | 0     | 0.36   |
| Hikvision | HS-SSD-C100        | 480 GB | 2       | 130   | 0     | 0.36   |
| HPE       | MK0800GEYKE        | 800 GB | 1       | 130   | 0     | 0.36   |
| China     | GM128              | 128 GB | 1       | 129   | 0     | 0.36   |
| Goodram   | SSDPR-CL100-240-G2 | 240 GB | 9       | 129   | 0     | 0.36   |
| KingSpec  | NT-128             | 128 GB | 6       | 151   | 168   | 0.36   |
| Intel     | SSDSC2KW512G8      | 512 GB | 20      | 129   | 1     | 0.35   |
| Corsair   | Force LS SSD       | 120 GB | 17      | 376   | 453   | 0.35   |
| Toshiba   | THNSNF064GMCS      | 64 GB  | 2       | 129   | 0     | 0.35   |
| ADATA     | SP550              | 240 GB | 31      | 131   | 1     | 0.35   |
| GLOWAY    | STK1TS3-S7         | 1 TB   | 2       | 129   | 0     | 0.35   |
| Patriot   | Burst              | 960 GB | 8       | 128   | 0     | 0.35   |
| SPCC      | SSD                | 1 TB   | 24      | 135   | 1     | 0.35   |
| SPCC      | SPCCSolidStateDisk | 512 GB | 2       | 128   | 0     | 0.35   |
| T-FORCE   | SSD                | 250 GB | 3       | 128   | 0     | 0.35   |
| SanDisk   | Z400s M.2 2280     | 256 GB | 2       | 128   | 0     | 0.35   |
| China     | SATA3 2TB SSD      | 2 TB   | 2       | 128   | 0     | 0.35   |
| ADATA     | SP920SS            | 128 GB | 9       | 391   | 9     | 0.35   |
| Toshiba   | TR200              | 960 GB | 2       | 128   | 0     | 0.35   |
| Smartbuy  | SSD                | 240 GB | 25      | 155   | 1     | 0.35   |
| KLEVV     | SSD NEO N500       | 240 GB | 1       | 127   | 0     | 0.35   |
| Plextor   | PX-512S2G          | 512 GB | 3       | 127   | 0     | 0.35   |
| HP        | SSD S750           | 256 GB | 1       | 127   | 0     | 0.35   |
| Kingston  | SA400S37240G       | 240 GB | 777     | 135   | 1     | 0.35   |
| Vaseky    | V800-120G          | 120 GB | 1       | 127   | 0     | 0.35   |
| Kingston  | SA400S37480G       | 480 GB | 411     | 141   | 1     | 0.35   |
| SK hynix  | HFS256G39MND-2300A | 256 GB | 5       | 391   | 136   | 0.35   |
| Goodram   | IRIDIUM            | 480 GB | 2       | 127   | 0     | 0.35   |
| Lite-On   | LMT-256M3M         | 256 GB | 1       | 253   | 1     | 0.35   |
| Lumino... | SSD                | 240 GB | 1       | 126   | 0     | 0.35   |
| WDC       | WDS240G2G0B-00EPW0 | 240 GB | 128     | 134   | 1     | 0.35   |
| Chiprex   | S10T3120GB         | 120 GB | 1       | 126   | 0     | 0.35   |
| Kingston  | SMSM150S324G       | 24 GB  | 1       | 126   | 0     | 0.35   |
| Crucial   | CT480BX300SSD1     | 480 GB | 14      | 126   | 0     | 0.35   |
| Seagate   | ZA480NM10001       | 480 GB | 1       | 126   | 0     | 0.35   |
| Samsung   | MZNLN256HMHQ-000H7 | 256 GB | 2       | 126   | 0     | 0.35   |
| Crucial   | CT500MX500SSD4     | 500 GB | 42      | 126   | 0     | 0.35   |
| Kingston  | SUV500MS240G       | 240 GB | 16      | 126   | 0     | 0.35   |
| BlueRay   | SSD                | 120 GB | 1       | 125   | 0     | 0.34   |
| KingFast  | SSD                | 32 GB  | 1       | 125   | 0     | 0.34   |
| BRAVEE... | SSD                | 240 GB | 1       | 125   | 0     | 0.34   |
| Lite-On   | CV5-8Q128          | 128 GB | 1       | 125   | 0     | 0.34   |
| China     | ASS-120            | 120 GB | 1       | 124   | 0     | 0.34   |
| ADATA     | SP600              | 64 GB  | 11      | 209   | 2     | 0.34   |
| Samsung   | SSD 860 PRO        | 512 GB | 45      | 124   | 0     | 0.34   |
| SanDisk   | SDLF1DAR-960G-1HA1 | 960 GB | 2       | 124   | 0     | 0.34   |
| TAMMUZ    | SSD                | 512 GB | 1       | 123   | 0     | 0.34   |
| TCSUNBOW  | X3                 | 480 GB | 5       | 123   | 0     | 0.34   |
| Lite-On   | LCH-128V2S-11 2... | 128 GB | 5       | 123   | 0     | 0.34   |
| Apple     | SSD SM128C         | 121 GB | 3       | 248   | 7     | 0.34   |
| Intenso   | lntenso SSD Sat... | 960 GB | 2       | 205   | 12    | 0.34   |
| ADATA     | SU800NS38          | 512 GB | 6       | 189   | 129   | 0.34   |
| Patriot   | P200               | 2 TB   | 3       | 226   | 16    | 0.34   |
| ADATA     | SU635              | 240 GB | 17      | 133   | 62    | 0.34   |
| Lite-On   | LCS-256M6S         | 256 GB | 8       | 139   | 132   | 0.33   |
| WDC       | PC SA530 SDASB8... | 1 TB   | 1       | 122   | 0     | 0.33   |
| Hypertec  | SSD2S240SF1200SA2  | 240 GB | 2       | 371   | 512   | 0.33   |
| INNOVA... | SSD                | 256 GB | 3       | 121   | 0     | 0.33   |
| Plextor   | PH6-CE240-L2       | 240 GB | 1       | 121   | 0     | 0.33   |
| HP        | VK001920GWJPH      | 1.9 TB | 2       | 121   | 0     | 0.33   |
| Micron    | 5300_MTFDDAK960TDS | 960 GB | 2       | 181   | 1     | 0.33   |
| Crucial   | CT500MX500SSD1     | 500 GB | 300     | 122   | 1     | 0.33   |
| Union ... | RTOTJ128VGD2EYX    | 128 GB | 8       | 120   | 0     | 0.33   |
| ADATA     | SU650NS38          | 480 GB | 3       | 120   | 0     | 0.33   |
| Kingston  | HyperX Fury 3D     | 240 GB | 5       | 120   | 0     | 0.33   |
| Goodram   | SSDPR-CX400-128    | 128 GB | 21      | 120   | 0     | 0.33   |
| ADATA     | SSD S511           | 64 GB  | 3       | 450   | 679   | 0.33   |
| Samsung   | MZNTD128HAGM-00000 | 128 GB | 3       | 120   | 0     | 0.33   |
| SanDisk   | SSD U100           | 24 GB  | 33      | 151   | 39    | 0.33   |
| Samsung   | MZNLN128HAHQ-000L1 | 128 GB | 2       | 120   | 0     | 0.33   |
| Samsung   | MZNLF128HCHP-000L1 | 128 GB | 2       | 120   | 0     | 0.33   |
| Micron    | 1100_MTFDDAV512TBN | 512 GB | 33      | 125   | 79    | 0.33   |
| Fujitsu   | F500s 480G         | 480 GB | 1       | 119   | 0     | 0.33   |
| SK hynix  | HFS128G39MND-3310A | 128 GB | 2       | 119   | 0     | 0.33   |
| Kingston  | RBUSNS4180S3256GJ  | 256 GB | 1       | 119   | 0     | 0.33   |
| SPCC      | M.2 Disk           | 256 GB | 1       | 119   | 0     | 0.33   |
| WDC       | WDS400T2B0A-00SM50 | 4 TB   | 5       | 119   | 0     | 0.33   |
| Plextor   | PX-AG128M6e        | 128 GB | 4       | 229   | 2     | 0.33   |
| SK hynix  | HFS128G3BTND-N210A | 128 GB | 3       | 118   | 0     | 0.32   |
| LDLC      | SSD                | 480 GB | 4       | 123   | 1     | 0.32   |
| Crucial   | CT2000BX500SSD1    | 2 TB   | 14      | 117   | 0     | 0.32   |
| Kingston  | SA400S37960G       | 960 GB | 59      | 117   | 0     | 0.32   |
| SanDisk   | SD9TN8W256G1001    | 256 GB | 3       | 117   | 0     | 0.32   |
| Hikvision | HS-SSD-E100 512G   | 512 GB | 1       | 116   | 0     | 0.32   |
| XSTAR     | SSD                | 256 GB | 1       | 116   | 0     | 0.32   |
| Crucial   | CT1000MX500SSD1    | 1 TB   | 291     | 119   | 1     | 0.32   |
| Indilinx  | IND-S325S-512G     | 512 GB | 1       | 116   | 0     | 0.32   |
| ADATA     | SSD SX900 512GB... | 512 GB | 2       | 116   | 0     | 0.32   |
| Samsung   | MZNLN256HAJQ-000H7 | 256 GB | 3       | 115   | 0     | 0.32   |
| Samsung   | SG9XCS2D400GESLT   | 400 GB | 1       | 115   | 0     | 0.32   |
| Goodram   | SSDPR-CL100-240    | 240 GB | 3       | 114   | 0     | 0.31   |
| China     | SSD                | 1 TB   | 10      | 114   | 0     | 0.31   |
| ADATA     | IM2S3338-128GD2    | 128 GB | 11      | 114   | 0     | 0.31   |
| SK hynix  | HFS256G32MND-2900A | 256 GB | 3       | 386   | 10    | 0.31   |
| WDC       | WDS100T2B0B        | 1 TB   | 5       | 114   | 0     | 0.31   |
| Plextor   | PX-256M6V          | 256 GB | 1       | 114   | 0     | 0.31   |
| OCZ       | D2CSTK181M11-0180  | 180 GB | 3       | 114   | 0     | 0.31   |
| Goodram   | IR-SSDPR-S25A-120  | 120 GB | 7       | 114   | 0     | 0.31   |
| Corsair   | FORCE LX SSD       | 256 GB | 1       | 113   | 0     | 0.31   |
| Crucial   | CT2000MX500SSD1    | 2 TB   | 67      | 113   | 0     | 0.31   |
| HEORIADY  | HX-001 E           | 1 TB   | 1       | 113   | 0     | 0.31   |
| Crucial   | CT250MX500SSD4     | 250 GB | 19      | 113   | 0     | 0.31   |
| Samsung   | MZ7TE256HMHP-00004 | 256 GB | 1       | 113   | 0     | 0.31   |
| Intel     | SSDSC2KW256G8      | 256 GB | 36      | 113   | 0     | 0.31   |
| XUM       | HX256GSSDSATA3     | 240 GB | 2       | 113   | 0     | 0.31   |
| SanDisk   | SDSSDH3 250G       | 250 GB | 6       | 113   | 0     | 0.31   |
| Lite-On   | CV3-8D256-11 SATA  | 256 GB | 9       | 113   | 0     | 0.31   |
| Intel     | SSDSA2M080G2LE     | 80 GB  | 2       | 154   | 6     | 0.31   |
| OCZ       | VERTEX2            | 90 GB  | 1       | 113   | 0     | 0.31   |
| Samsung   | MZNLN256HCHP-000L2 | 256 GB | 5       | 112   | 0     | 0.31   |
| Samsung   | MZNLN256HAJQ-000L2 | 256 GB | 8       | 112   | 0     | 0.31   |
| Apacer    | AS340              | 240 GB | 23      | 117   | 1     | 0.31   |
| Palit     | UVS                | 120 GB | 3       | 112   | 0     | 0.31   |
| Apacer    | 16GB SATA Flash... | 16 GB  | 10      | 227   | 22    | 0.31   |
| Samsung   | SSD CM871 2.5 7mm  | 128 GB | 1       | 112   | 0     | 0.31   |
| Samsung   | MZMPC128HBFU-000   | 128 GB | 2       | 112   | 0     | 0.31   |
| KingSpec  | NT-256             | 256 GB | 13      | 142   | 1     | 0.31   |
| Kingston  | RBU-SNS8100S312... | 128 GB | 5       | 111   | 0     | 0.31   |
| China     | 128GB SSD          | 128 GB | 16      | 111   | 0     | 0.31   |
| SPCC      | Solid State DisK   | 2 TB   | 1       | 111   | 0     | 0.30   |
| Samsung   | MZNTY256HDHP-00007 | 256 GB | 1       | 110   | 0     | 0.30   |
| SanDisk   | SD6SB1M128G1002    | 128 GB | 1       | 110   | 0     | 0.30   |
| Transcend | TS256GSSD370S      | 256 GB | 16      | 110   | 0     | 0.30   |
| Intel     | SSDSC2KG019T8      | 1.9 TB | 4       | 110   | 0     | 0.30   |
| SuperS... | S540               | 240 GB | 1       | 110   | 0     | 0.30   |
| SPCC      | SSD                | 512 GB | 49      | 157   | 11    | 0.30   |
| Goodram   | SSDPR-CL100-960-G3 | 960 GB | 3       | 110   | 0     | 0.30   |
| TEXTORM   | BM5                | 480 GB | 1       | 109   | 0     | 0.30   |
| Micron    | 1100 SATA          | 256 GB | 24      | 156   | 1     | 0.30   |
| Kston     | SSD                | 128 GB | 5       | 109   | 0     | 0.30   |
| Team      | L7 EVO SSD         | 64 GB  | 2       | 109   | 0     | 0.30   |
| SPCC      | SSD                | 128 GB | 75      | 109   | 1     | 0.30   |
| ZTC       | SM201-512G         | 512 GB | 2       | 109   | 0     | 0.30   |
| Faspeed   | H7-240G            | 240 GB | 1       | 109   | 0     | 0.30   |
| Zheino    | CHN-25SATAC3-120   | 120 GB | 1       | 108   | 0     | 0.30   |
| Intel     | SSDSC2BF180A5L     | 180 GB | 10      | 190   | 13    | 0.30   |
| Samsung   | MZNLN256HAJQ-000H1 | 256 GB | 24      | 115   | 9     | 0.30   |
| Intenso   | 1TB SATA SSD       | 1 TB   | 1       | 108   | 0     | 0.30   |
| WDC       | WDS120G2G0A-00JH30 | 120 GB | 185     | 117   | 1     | 0.30   |
| SPCC      | SPCCSolidStateDisk | 256 GB | 2       | 108   | 0     | 0.30   |
| Intel     | SSDSCKGF240A5L     | 240 GB | 2       | 107   | 0     | 0.30   |
| WDC       | WDS250G2B0A        | 250 GB | 8       | 107   | 0     | 0.29   |
| Zheino    | CHN mSATAM3 128    | 128 GB | 3       | 106   | 0     | 0.29   |
| PNY       | SSD2SC240G5LC72... | 240 GB | 1       | 106   | 0     | 0.29   |
| Mushkin   | MKNSSDAT60GB-V     | 64 GB  | 1       | 106   | 0     | 0.29   |
| Samsung   | MZYTE128HMGR-000L2 | 128 GB | 1       | 106   | 0     | 0.29   |
| Samsung   | MZMPC256HAFU-000L9 | 256 GB | 1       | 106   | 0     | 0.29   |
| Samsung   | MZNLN128HAHQ-000H1 | 128 GB | 46      | 108   | 29    | 0.29   |
| Silicon   | SATA3 120GB SSD    | 120 GB | 1       | 106   | 0     | 0.29   |
| WDC       | WDS120G2G0B-00EPW0 | 120 GB | 56      | 109   | 1     | 0.29   |
| Plextor   | PH6-CE240-L1       | 240 GB | 1       | 106   | 0     | 0.29   |
| Smartbuy  | SSD                | 240 GB | 6       | 105   | 0     | 0.29   |
| Intel     | SSDSCKGF256A5 SATA | 256 GB | 6       | 105   | 0     | 0.29   |
| Toshiba   | THNSNC256GBSJ      | 256 GB | 1       | 105   | 0     | 0.29   |
| Transcend | TS1TSSD230S        | 1 TB   | 7       | 105   | 0     | 0.29   |
| ADATA     | SU800              | 256 GB | 55      | 123   | 37    | 0.29   |
| Marvell   | SATAIII            | 16 GB  | 1       | 105   | 0     | 0.29   |
| Kingston  | SHFS37A480G        | 480 GB | 1       | 104   | 0     | 0.29   |
| KingDian  | S280-120GB         | 120 GB | 10      | 114   | 396   | 0.29   |
| Corsair   | Neutron GTX SSD    | 240 GB | 6       | 734   | 93    | 0.29   |
| Intel     | SSDSA2BW160G3H     | 160 GB | 12      | 190   | 1     | 0.29   |
| Samsung   | SSD 870 QVO        | 4 TB   | 15      | 104   | 0     | 0.29   |
| Transcend | TS256GSSD360S      | 256 GB | 3       | 104   | 0     | 0.29   |
| Plextor   | PX-128M5Pro        | 128 GB | 55      | 104   | 0     | 0.29   |
| Gigabyte  | GP-GSTFS31480GNTD  | 480 GB | 4       | 104   | 0     | 0.29   |
| Lite-On   | CV3-8D128-11 SATA  | 128 GB | 11      | 104   | 0     | 0.29   |
| Crucial   | CT120BX100SSD1     | 120 GB | 7       | 104   | 0     | 0.29   |
| Transcend | TS120GSSD220S      | 120 GB | 18      | 104   | 0     | 0.29   |
| Seagate   | XA480ME10063       | 480 GB | 4       | 104   | 0     | 0.29   |
| SanDisk   | SSD G5 BICS4       | 500 GB | 23      | 104   | 0     | 0.29   |
| Transcend | TS120GMTS820S      | 120 GB | 3       | 104   | 0     | 0.29   |
| WDC       | WDBNCE5000PNC      | 500 GB | 26      | 104   | 0     | 0.29   |
| Intel     | SSDSC2KW128G8      | 128 GB | 11      | 104   | 0     | 0.29   |
| WDC       | WDS240G2G0A-00JH30 | 240 GB | 282     | 121   | 1     | 0.29   |
| SK hynix  | HFS256G3BTND-N210A | 256 GB | 8       | 104   | 0     | 0.29   |
| JASTER    | SSD                | 128 GB | 2       | 103   | 0     | 0.28   |
| SanDisk   | SD9SN8W128G1002    | 128 GB | 9       | 103   | 0     | 0.28   |
| Patriot   | Burst              | 120 GB | 79      | 103   | 0     | 0.28   |
| GeIL      | R3_128GB           | 128 GB | 3       | 103   | 0     | 0.28   |
| Transcend | TS256GSSD230S      | 256 GB | 13      | 127   | 80    | 0.28   |
| Intel     | SSDSA2M160G2GN     | 160 GB | 1       | 2996  | 28    | 0.28   |
| SK hynix  | SC210 2.5 7MM      | 128 GB | 2       | 478   | 2     | 0.28   |
| Fujitsu   | F300               | 480 GB | 1       | 103   | 0     | 0.28   |
| Toshiba   | KSG60ZMV512G M.... | 512 GB | 8       | 103   | 0     | 0.28   |
| Transcend | TS120GSSD25D-M     | 128 GB | 1       | 309   | 2     | 0.28   |
| Apacer    | AS510S             | 64 GB  | 5       | 103   | 0     | 0.28   |
| Phison    | SATA SSD           | 1 TB   | 7       | 102   | 0     | 0.28   |
| SanDisk   | SDSA6MM-032G-1006  | 32 GB  | 1       | 102   | 0     | 0.28   |
| KingDian  | S370               | 512 GB | 2       | 102   | 0     | 0.28   |
| SanDisk   | SSD PLUS           | 480 GB | 98      | 122   | 1     | 0.28   |
| Intenso   | SATA3 256GB SSD    | 256 GB | 1       | 102   | 0     | 0.28   |
| KingFast  | SSD                | 32 GB  | 1       | 102   | 0     | 0.28   |
| Verbatim  | Vi550 S3 SSD       | 512 GB | 10      | 102   | 0     | 0.28   |
| Toshiba   | KSG60ZMV256G M.... | 256 GB | 23      | 133   | 27    | 0.28   |
| Phison    | SSM28512GPTCB3B... | 512 GB | 1       | 101   | 0     | 0.28   |
| Lite-On   | LCH-256V2S         | 256 GB | 7       | 101   | 0     | 0.28   |
| Intel     | SSDSC2KF128G8L     | 128 GB | 8       | 101   | 0     | 0.28   |
| Samsung   | MZNLN512HAJQ-00007 | 512 GB | 1       | 101   | 0     | 0.28   |
| Intel     | SSDSCKJF180A5L     | 180 GB | 5       | 131   | 1     | 0.28   |
| Kingston  | SUV500480G         | 480 GB | 14      | 132   | 214   | 0.28   |
| Lite-On   | CV8-8E128-11 SATA  | 128 GB | 17      | 101   | 0     | 0.28   |
| Samsung   | MZNTD256HAGL-00000 | 256 GB | 2       | 101   | 0     | 0.28   |
| Gigabyte  | GP-GSTFS31120GNTD  | 120 GB | 36      | 100   | 0     | 0.28   |
| AMD       | R5SL240G           | 240 GB | 15      | 109   | 1     | 0.28   |
| Samsung   | MZMTD128HAFV-00000 | 128 GB | 1       | 100   | 0     | 0.28   |
| Goodram   | SSD                | 480 GB | 1       | 99    | 0     | 0.27   |
| ORICO     | N300               | 128 GB | 1       | 99    | 0     | 0.27   |
| ADATA     | SU810NS38 SATA ... | 256 GB | 12      | 99    | 0     | 0.27   |
| SK hynix  | HFS128G32TND-N210A | 128 GB | 3       | 412   | 132   | 0.27   |
| Hikvision | HKVSN HS-SSD-C1... | 240 GB | 1       | 99    | 0     | 0.27   |
| Intenso   | SSD SATA III       | 240 GB | 1       | 99    | 0     | 0.27   |
| Intel     | SSDMCEAC180B3      | 180 GB | 3       | 98    | 0     | 0.27   |
| China     | 256GB PCS 2.5" SSD | 256 GB | 2       | 98    | 0     | 0.27   |
| Micron    | 5100_MTFDDAK240TCB | 240 GB | 1       | 98    | 0     | 0.27   |
| ADATA     | SU650              | 120 GB | 89      | 113   | 25    | 0.27   |
| AMD       | R3SL480G           | 480 GB | 1       | 98    | 0     | 0.27   |
| Toshiba   | THNSNH256G8NT      | 256 GB | 1       | 293   | 2     | 0.27   |
| Crucial   | CT256M550SSD1      | 256 GB | 11      | 1064  | 107   | 0.27   |
| Samsung   | MZ7KM480HMHQ-000MV | 480 GB | 1       | 97    | 0     | 0.27   |
| Samsung   | MZ7LN128HAHQ-000L2 | 128 GB | 18      | 97    | 0     | 0.27   |
| Maxtor    | Z1 SSD             | 240 GB | 10      | 97    | 0     | 0.27   |
| Goodram   | SSDPR-CX400-256    | 256 GB | 17      | 96    | 0     | 0.27   |
| Crucial   | CT256M550SSD3      | 256 GB | 3       | 573   | 11    | 0.27   |
| Blackpcs  | AS201 SSD          | 128 GB | 1       | 96    | 0     | 0.26   |
| JD        | SSD                | 120 GB | 1       | 96    | 0     | 0.26   |
| Dogfish   | SSD                | 250 GB | 1       | 96    | 0     | 0.26   |
| HXY       | SSD 120G           | 120 GB | 1       | 96    | 0     | 0.26   |
| Transcend | TS512GSSD370S      | 512 GB | 3       | 144   | 3     | 0.26   |
| Gigabyte  | GP-GSTFS31240GNTD  | 240 GB | 36      | 96    | 0     | 0.26   |
| Leven     | JAJS600M256C       | 256 GB | 3       | 96    | 0     | 0.26   |
| SK hynix  | SH920 2.5 7MM      | 256 GB | 5       | 853   | 76    | 0.26   |
| KingSpec  | Q-90               | 90 GB  | 3       | 385   | 175   | 0.26   |
| SPCC      | SSD170             | 120 GB | 3       | 245   | 341   | 0.26   |
| UNIC2     | S100-480           | 480 GB | 2       | 95    | 0     | 0.26   |
| KingDian  | SSD-S400           | 120 GB | 1       | 285   | 2     | 0.26   |
| GOWE      | M750 120G          | 120 GB | 1       | 284   | 2     | 0.26   |
| Crucial   | CT500BX100SSD1     | 500 GB | 16      | 95    | 1     | 0.26   |
| Kingston  | RBUSC180DS37256GJ  | 256 GB | 2       | 94    | 0     | 0.26   |
| SanDisk   | SDSSDH3 500G       | 500 GB | 29      | 94    | 1     | 0.26   |
| ADATA     | SX930              | 480 GB | 1       | 94    | 0     | 0.26   |
| PNY       | CS900 120GB SSD    | 120 GB | 79      | 93    | 0     | 0.26   |
| SanDisk   | SSD PLUS           | 240 GB | 180     | 115   | 1     | 0.26   |
| Silicon   | SATA3 240GB SSD    | 240 GB | 2       | 93    | 0     | 0.26   |
| Integral  | V Series SATA SSD  | 480 GB | 1       | 93    | 0     | 0.26   |
| BIOSTAR   | S120-128GB         | 128 GB | 1       | 93    | 0     | 0.26   |
| Pioneer   | APS-SL3N-240       | 240 GB | 2       | 93    | 0     | 0.26   |
| T-FORCE   | SSD                | 1 TB   | 2       | 93    | 0     | 0.26   |
| SanDisk   | ASMT109x- Volume   | 756 GB | 5       | 93    | 0     | 0.26   |
| Lite-On   | LCS-128M6S         | 128 GB | 6       | 93    | 0     | 0.26   |
| Mushkin   | MKNSSDSR250GB      | 250 GB | 1       | 93    | 0     | 0.26   |
| Samsung   | MZYTE256HMHP-000L2 | 256 GB | 2       | 93    | 0     | 0.26   |
| LDLC      | F6+M.2 480         | 480 GB | 3       | 93    | 0     | 0.26   |
| Plextor   | PX-128M8VC         | 128 GB | 3       | 93    | 0     | 0.26   |
| Goodram   | IR-SSDPR-S25A-240  | 240 GB | 9       | 92    | 0     | 0.25   |
| Kingston  | SUV500MS120G       | 120 GB | 22      | 98    | 55    | 0.25   |
| Samsung   | MZMTD256HAGM-00000 | 256 GB | 1       | 92    | 0     | 0.25   |
| Intenso   | SDVPSA1910256      | 256 GB | 1       | 92    | 0     | 0.25   |
| Lite-On   | PH2-CJ120          | 120 GB | 1       | 92    | 0     | 0.25   |
| Intel     | SSDSC2KI128G8      | 128 GB | 2       | 92    | 0     | 0.25   |
| Apacer    | AS350              | 480 GB | 4       | 92    | 0     | 0.25   |
| INNOVA... | SSD                | 480 GB | 2       | 92    | 0     | 0.25   |
| China     | ESA3SMH2ISN3BT0... | 64 GB  | 1       | 91    | 0     | 0.25   |
| INNOVA... | SSD                | 1 TB   | 2       | 91    | 0     | 0.25   |
| Toshiba   | THNSNH128G8NT      | 128 GB | 2       | 91    | 0     | 0.25   |
| Toshiba   | THNSNS256GMCP      | 256 GB | 1       | 91    | 0     | 0.25   |
| China     | SATA SSD           | 64 GB  | 19      | 90    | 0     | 0.25   |
| MyDigi... | SB2                | 240 GB | 4       | 90    | 0     | 0.25   |
| Micron    | MTFDDAK256TDL      | 256 GB | 8       | 90    | 0     | 0.25   |
| Foxline   | FLSSD128X5SE       | 128 GB | 1       | 90    | 0     | 0.25   |
| ADATA     | SU700              | 120 GB | 10      | 160   | 3     | 0.25   |
| Faspeed   | H5-60G PLUS        | 64 GB  | 1       | 90    | 0     | 0.25   |
| Crucial   | CT480BX500SSD1     | 480 GB | 141     | 93    | 1     | 0.25   |
| Lite-On   | L8H-128V2G-HP      | 128 GB | 4       | 90    | 0     | 0.25   |
| Phison    | SATA SSD           | 256 GB | 8       | 90    | 0     | 0.25   |
| Lite-On   | CV3-CE256          | 256 GB | 1       | 358   | 3     | 0.25   |
| OSCOO     | OSC M.2            | 120 GB | 1       | 89    | 0     | 0.25   |
| Plextor   | PH6-CE120-L1       | 120 GB | 2       | 89    | 0     | 0.24   |
| Samsung   | MZAPF016HCDD-000H1 | 16 GB  | 1       | 89    | 0     | 0.24   |
| VisionTek | SSD                | 120 GB | 2       | 88    | 0     | 0.24   |
| RZX       | 19SSD6G-480GB      | 480 GB | 1       | 88    | 0     | 0.24   |
| SanDisk   | SDSSDA-2T00        | 2 TB   | 3       | 88    | 0     | 0.24   |
| Kingston  | SV300S37A-240G     | 240 GB | 2       | 88    | 0     | 0.24   |
| ORICO     | PM200-1T           | 1 TB   | 1       | 88    | 0     | 0.24   |
| ORTIAL    | SSD                | 128 GB | 2       | 88    | 0     | 0.24   |
| ADATA     | SU650              | 480 GB | 24      | 123   | 261   | 0.24   |
| Lite-On   | S920 256           | 256 GB | 1       | 88    | 0     | 0.24   |
| WDC       | WDBNCE0040PNC      | 4 TB   | 1       | 88    | 0     | 0.24   |
| Samsung   | SSD 860 EVO M.2    | 2 TB   | 10      | 87    | 0     | 0.24   |
| ORICO     | N300               | 256 GB | 1       | 262   | 2     | 0.24   |
| Kingston  | SA400M8120G        | 120 GB | 15      | 87    | 0     | 0.24   |
| Micron    | MTFDDAV256TBN-1... | 256 GB | 10      | 88    | 1     | 0.24   |
| Kingston  | SKC380S3120G       | 120 GB | 1       | 86    | 0     | 0.24   |
| KingSpec  | P4-960             | 960 GB | 1       | 86    | 0     | 0.24   |
| SanDisk   | SSD PLUS           | 1 TB   | 71      | 120   | 60    | 0.24   |
| Mushkin   | MKNSSDEC120GB      | 120 GB | 1       | 86    | 0     | 0.24   |
| Intel     | SSDSA2M080G2GN     | 80 GB  | 2       | 1445  | 15    | 0.24   |
| Intel     | SSDSCKKW256G8      | 256 GB | 5       | 127   | 10    | 0.23   |
| Intel     | SSDMCEAF180A4L     | 180 GB | 1       | 85    | 0     | 0.23   |
| Samsung   | MZNTE128HMGR-000H1 | 128 GB | 1       | 85    | 0     | 0.23   |
| Team      | TEAMT2535T120G     | 120 GB | 1       | 85    | 0     | 0.23   |
| Samsung   | MZMTD256HAGM-000   | 256 GB | 1       | 85    | 0     | 0.23   |
| ADATA     | SU630              | 240 GB | 71      | 90    | 64    | 0.23   |
| Kingston  | RBUSNS8180DS3128GJ | 128 GB | 13      | 94    | 1     | 0.23   |
| Vaseky    | V800-350G          | 360 GB | 1       | 84    | 0     | 0.23   |
| Colorful  | SL500              | 256 GB | 2       | 84    | 0     | 0.23   |
| Micron    | MTFDDAV256TBN-1... | 256 GB | 21      | 103   | 57    | 0.23   |
| Transcend | TS256GMTS800       | 256 GB | 4       | 84    | 0     | 0.23   |
| Crucial   | CT240BX500SSD1     | 240 GB | 285     | 84    | 1     | 0.23   |
| Vaseky    | V900-128G          | 128 GB | 2       | 84    | 0     | 0.23   |
| Transcend | TS256GSSD320       | 256 GB | 2       | 84    | 0     | 0.23   |
| SK hynix  | HFS128G39MNC-3510A | 128 GB | 2       | 83    | 0     | 0.23   |
| Micron    | MTFDDAK960TDN      | 960 GB | 2       | 83    | 0     | 0.23   |
| Lite-On   | CV6-CQ128          | 128 GB | 1       | 83    | 0     | 0.23   |
| Lite-On   | CV5-8Q256-HP       | 256 GB | 1       | 83    | 0     | 0.23   |
| e2e4      | SSD                | 480 GB | 2       | 83    | 0     | 0.23   |
| Lite-On   | CV3-8D256          | 256 GB | 7       | 83    | 0     | 0.23   |
| Lite-On   | CV4-8Q128-HP       | 128 GB | 1       | 82    | 0     | 0.23   |
| Plextor   | PX-128M5M          | 128 GB | 11      | 82    | 0     | 0.23   |
| Samsung   | SSD 860 PRO        | 2 TB   | 12      | 82    | 0     | 0.23   |
| HP        | SSD S700           | 1 TB   | 7       | 82    | 0     | 0.23   |
| OCZ       | VERTEX2            | 100 GB | 2       | 82    | 0     | 0.23   |
| Kingston  | RBUSNS8180DS3128GH | 128 GB | 9       | 82    | 0     | 0.22   |
| Nfortec   | ALCYON             | 512 GB | 1       | 81    | 0     | 0.22   |
| China     | MSATA 480GB SSD    | 480 GB | 2       | 81    | 0     | 0.22   |
| OCZ       | VECTOR180          | 120 GB | 2       | 81    | 0     | 0.22   |
| WDC       | WDS480G2G0B-00EPW0 | 480 GB | 17      | 81    | 0     | 0.22   |
| SK hynix  | SC308 SATA         | 128 GB | 9       | 121   | 130   | 0.22   |
| Transcend | TS256GMTS400S      | 256 GB | 2       | 81    | 0     | 0.22   |
| Micron    | MTFDDAV512TBN      | 512 GB | 1       | 81    | 0     | 0.22   |
| SPCC      | 2.5�� SSD          | 512 GB | 1       | 80    | 0     | 0.22   |
| China     | SATA SSD           | 256 GB | 8       | 80    | 0     | 0.22   |
| Crucial   | CT1000BX500SSD1    | 1 TB   | 51      | 80    | 0     | 0.22   |
| China     | SATA3 256GB SSD    | 256 GB | 4       | 80    | 0     | 0.22   |
| China     | SSD                | 240 GB | 21      | 93    | 1     | 0.22   |
| Transcend | TS512GSSD230S      | 512 GB | 2       | 80    | 0     | 0.22   |
| Crucial   | CT2050MX300SSD1    | 2 TB   | 3       | 89    | 1     | 0.22   |
| Corsair   | Force LS SSD       | 480 GB | 1       | 80    | 0     | 0.22   |
| Kingston  | RBU-SNS8152S325... | 256 GB | 1       | 80    | 0     | 0.22   |
| KingFast  | SSD                | 120 GB | 10      | 91    | 308   | 0.22   |
| China     | 256GB QLC SATA SSD | 256 GB | 2       | 80    | 0     | 0.22   |
| Intel     | SSDSC2KF180H6L     | 180 GB | 1       | 80    | 0     | 0.22   |
| Transcend | TS128GSSD370S      | 128 GB | 29      | 79    | 0     | 0.22   |
| Lite-On   | LAT-256M2S         | 256 GB | 1       | 239   | 2     | 0.22   |
| KingSpec  | NT-1TB             | 1 TB   | 4       | 79    | 0     | 0.22   |
| Fordisk   | S860 256G 6Gbps    | 256 GB | 1       | 79    | 0     | 0.22   |
| Apple     | SSD TS512C         | 500 GB | 1       | 79    | 0     | 0.22   |
| Colorful  | SL300              | 160 GB | 1       | 79    | 0     | 0.22   |
| China     | SSD 120G           | 120 GB | 3       | 79    | 0     | 0.22   |
| SanDisk   | SD7SB3Q256G1002    | 256 GB | 4       | 268   | 15    | 0.22   |
| Lite-On   | CV3-DE512          | 512 GB | 1       | 79    | 0     | 0.22   |
| PNY       | SSD2SC120G1CS17... | 120 GB | 1       | 79    | 0     | 0.22   |
| Seagate   | XA1920ME10063      | 1.9 TB | 2       | 79    | 0     | 0.22   |
| Samsung   | MZ7LN256HAJQ-000L7 | 256 GB | 9       | 79    | 0     | 0.22   |
| SanDisk   | SD8SB8U-128G-1006  | 128 GB | 2       | 78    | 0     | 0.22   |
| China     | SSD                | 120 GB | 34      | 96    | 2     | 0.22   |
| Dogfish   | SSD                | 500 GB | 3       | 78    | 0     | 0.22   |
| Apacer    | AS350              | 512 GB | 16      | 86    | 193   | 0.21   |
| Goodram   | SSDPR-CL100-120-G2 | 120 GB | 10      | 78    | 0     | 0.21   |
| China     | 256GB SSD          | 256 GB | 2       | 78    | 0     | 0.21   |
| Apacer    | AS350              | 120 GB | 20      | 78    | 1     | 0.21   |
| Lite-On   | CV3-CE128          | 128 GB | 2       | 78    | 0     | 0.21   |
| T-FORCE   | SSD                | 500 GB | 3       | 78    | 0     | 0.21   |
| AMD       | R3SL120G           | 120 GB | 30      | 78    | 1     | 0.21   |
| Crucial   | CT1000MX500SSD1N   | 1 TB   | 1       | 77    | 0     | 0.21   |
| Lexar     | SSD                | 480 GB | 3       | 77    | 0     | 0.21   |
| LDLC      | F7+240GB           | 240 GB | 4       | 77    | 0     | 0.21   |
| Crucial   | CT240BX200SSD1     | 240 GB | 24      | 77    | 0     | 0.21   |
| INNOVA... | SSD                | 120 GB | 1       | 76    | 0     | 0.21   |
| Dogfish   | SSD                | 240 GB | 2       | 76    | 0     | 0.21   |
| SPCC      | SSD170             | 55 GB  | 4       | 540   | 762   | 0.21   |
| Kingston  | SA400S37-240G      | 240 GB | 2       | 75    | 0     | 0.21   |
| Transcend | TS64GSSD360S       | 64 GB  | 1       | 75    | 0     | 0.21   |
| SPEED UP  | B-128GB            | 128 GB | 1       | 75    | 0     | 0.21   |
| ASMedia   | ASMT109x- Fast     | 2 TB   | 3       | 74    | 0     | 0.20   |
| China     | 64GB SSD           | 64 GB  | 12      | 74    | 0     | 0.20   |
| LDLC      | SSD F7 PLUS 3D ... | 240 GB | 2       | 74    | 0     | 0.20   |
| Reeinno   | ST240GB S4S3       | 240 GB | 1       | 74    | 0     | 0.20   |
| China     | NGFF 2280          | 512 GB | 1       | 73    | 0     | 0.20   |
| Intenso   | JAJM600M128C       | 128 GB | 1       | 73    | 0     | 0.20   |
| KingSpec  | MT-64              | 64 GB  | 2       | 220   | 1     | 0.20   |
| Micron    | MTFDDAK256TBN      | 256 GB | 2       | 73    | 0     | 0.20   |
| Micron    | 1100_MTFDDAV256TBN | 256 GB | 85      | 81    | 102   | 0.20   |
| Patriot   | P200               | 512 GB | 3       | 121   | 144   | 0.20   |
| Vaseky    | V800-32G           | 32 GB  | 1       | 73    | 0     | 0.20   |
| Kingrich  | K9 128GB SATA3 SSD | 128 GB | 1       | 657   | 8     | 0.20   |
| SanDisk   | SSD P4             | 32 GB  | 15      | 180   | 221   | 0.20   |
| Lite-On   | CV3-DE256          | 256 GB | 7       | 72    | 0     | 0.20   |
| SanDisk   | SSD i110           | 32 GB  | 2       | 72    | 0     | 0.20   |
| Team      | TM8PS7256G         | 256 GB | 8       | 72    | 0     | 0.20   |
| SK hynix  | SHGS31-500GS-2     | 500 GB | 10      | 72    | 0     | 0.20   |
| Intel     | SSDSCKKF256G8 SATA | 256 GB | 12      | 76    | 1     | 0.20   |
| SPCC      | SSD                | 55 GB  | 11      | 407   | 463   | 0.20   |
| KingSpec  | P3-512             | 512 GB | 14      | 83    | 129   | 0.20   |
| Crucial   | CT120BX500SSD1     | 120 GB | 156     | 73    | 1     | 0.20   |
| Toshiba   | THNSNK256GVN8      | 256 GB | 2       | 72    | 0     | 0.20   |
| SanDisk   | pSSD               | 128 GB | 33      | 72    | 2     | 0.20   |
| BAITITON  | BT58SSD12S         | 512 GB | 1       | 71    | 0     | 0.20   |
| Solid     | SSD0240S00         | 240 GB | 3       | 71    | 0     | 0.20   |
| Vaseky    | V800-500G          | 512 GB | 1       | 71    | 0     | 0.20   |
| Kingston  | V300 120G          | 120 GB | 1       | 71    | 0     | 0.20   |
| Toshiba   | THNSNH256GCST      | 256 GB | 1       | 71    | 0     | 0.20   |
| Lite-On   | CV3-DE128          | 128 GB | 1       | 70    | 0     | 0.19   |
| INNOVA... | SSD                | 512 GB | 4       | 100   | 8     | 0.19   |
| Integral  | V Series SATA SSD  | 240 GB | 11      | 70    | 0     | 0.19   |
| Plextor   | PX-128S3C          | 128 GB | 13      | 70    | 0     | 0.19   |
| OCZ       | SABER1000          | 480 GB | 1       | 70    | 0     | 0.19   |
| ADATA     | SU630              | 960 GB | 5       | 80    | 1     | 0.19   |
| ADATA     | SP900NS38          | 128 GB | 4       | 120   | 254   | 0.19   |
| Kingrich  | K9 120GB SATA3     | 128 GB | 1       | 69    | 0     | 0.19   |
| ADATA     | SU800              | 1 TB   | 19      | 103   | 31    | 0.19   |
| Intel     | SSDSCKKW512G8      | 512 GB | 1       | 69    | 0     | 0.19   |
| Micron    | MTFDDAK3T8TCB 0... | 3.8 TB | 1       | 483   | 6     | 0.19   |
| SanDisk   | SD7SN3Q128G1002    | 128 GB | 3       | 85    | 1     | 0.19   |
| China     | SSD                | 64 GB  | 7       | 68    | 0     | 0.19   |
| ADATA     | SU760              | 512 GB | 3       | 68    | 0     | 0.19   |
| KingDian  | S180               | 64 GB  | 15      | 71    | 76    | 0.19   |
| ViperTeq  | VT-SSDUP500-240    | 240 GB | 1       | 68    | 0     | 0.19   |
| ADATA     | S596               | 128 GB | 1       | 68    | 0     | 0.19   |
| ADATA     | SU655              | 120 GB | 6       | 68    | 0     | 0.19   |
| Transcend | TS128GSSD370       | 128 GB | 12      | 67    | 0     | 0.19   |
| WDC       | WDBNCE0010PNC      | 1 TB   | 12      | 67    | 0     | 0.19   |
| SanDisk   | SD7SB3Q128G1002    | 128 GB | 3       | 647   | 107   | 0.19   |
| Plextor   | PX-128M6M          | 128 GB | 4       | 67    | 0     | 0.19   |
| Intel     | SSDSC2KI256G8      | 256 GB | 2       | 67    | 0     | 0.18   |
| KingDian  | P10                | 120 GB | 2       | 69    | 19    | 0.18   |
| Lite-On   | LMT-256L9M-11 M... | 256 GB | 3       | 67    | 0     | 0.18   |
| Plextor   | PX-256M6M          | 256 GB | 4       | 72    | 1     | 0.18   |
| BlueRay   | SDM8SI480A         | 480 GB | 1       | 200   | 2     | 0.18   |
| ADATA     | SP900              | 512 GB | 2       | 66    | 0     | 0.18   |
| China     | SATA3 128GB SSD    | 128 GB | 4       | 66    | 0     | 0.18   |
| Leven     | JAJS300M120C       | 120 GB | 6       | 66    | 0     | 0.18   |
| Samsung   | MZNLN256HAJQ-000L7 | 256 GB | 7       | 66    | 0     | 0.18   |
| Intenso   | Memory Ghost SSD   | 512 GB | 1       | 66    | 0     | 0.18   |
| ADATA     | SU800              | 512 GB | 52      | 81    | 26    | 0.18   |
| GLOWAY    | YCT512GS3-S7 Pro   | 512 GB | 1       | 66    | 0     | 0.18   |
| HP        | SSD S700           | 250 GB | 26      | 66    | 0     | 0.18   |
| Samsung   | MZNLH512HALU-00000 | 512 GB | 15      | 66    | 0     | 0.18   |
| Apacer    | AS340              | 480 GB | 11      | 66    | 0     | 0.18   |
| Intel     | SSDMCEAW180A4      | 180 GB | 2       | 65    | 0     | 0.18   |
| China     | SSD                | 960 GB | 1       | 65    | 0     | 0.18   |
| PNY       | CS900 1TB SSD      | 1 TB   | 5       | 65    | 0     | 0.18   |
| Apacer    | AS340              | 120 GB | 18      | 65    | 0     | 0.18   |
| SPCC      | M.2 SSD            | 256 GB | 4       | 65    | 0     | 0.18   |
| AMD       | R5SL256G           | 256 GB | 1       | 65    | 0     | 0.18   |
| Lexar     | 512GB SSD          | 512 GB | 4       | 65    | 0     | 0.18   |
| Team      | T253X2128G         | 128 GB | 1       | 65    | 0     | 0.18   |
| SK hynix  | SHGS31-1000GS-2    | 1 TB   | 17      | 65    | 0     | 0.18   |
| BHT       | WR202H0032G E70... | 32 GB  | 1       | 64    | 0     | 0.18   |
| KIOXIA... | SATA SSD           | 480 GB | 7       | 64    | 0     | 0.18   |
| Avant     | 240GB Client SSD   | 240 GB | 1       | 64    | 0     | 0.18   |
| Intenso   | Morebeck-V602      | 120 GB | 1       | 64    | 0     | 0.18   |
| Kingston  | SA400S37           | 480 GB | 1       | 64    | 0     | 0.18   |
| KingSpec  | P4-480             | 480 GB | 4       | 64    | 0     | 0.18   |
| Lite-On   | CV3-8D128          | 128 GB | 6       | 64    | 0     | 0.18   |
| Intel     | SSDSCKKW256H6      | 256 GB | 2       | 64    | 0     | 0.18   |
| SanDisk   | SD8TN8U512G1001    | 512 GB | 2       | 64    | 0     | 0.18   |
| HP        | SSD S600           | 120 GB | 4       | 105   | 1     | 0.18   |
| Lenovo    | SSD SL700 120G     | 120 GB | 4       | 63    | 0     | 0.17   |
| TREKSTOR  | TREKSTORSSD128GB   | 128 GB | 2       | 122   | 78    | 0.17   |
| KingDian  | S280               | 120 GB | 15      | 63    | 0     | 0.17   |
| Kingston  | SUV400S37 120G     | 120 GB | 1       | 63    | 0     | 0.17   |
| Apacer    | AS350              | 240 GB | 15      | 63    | 0     | 0.17   |
| Team      | TM8PS7512G         | 512 GB | 8       | 63    | 0     | 0.17   |
| Transcend | TS128GMTS400S      | 128 GB | 2       | 63    | 0     | 0.17   |
| Intel     | SSDSC2KW010T8      | 1 TB   | 1       | 504   | 7     | 0.17   |
| Lite-On   | LCS-128L9S-11 2... | 128 GB | 1       | 62    | 0     | 0.17   |
| SanDisk   | SDSSDH3 2T00       | 2 TB   | 13      | 62    | 0     | 0.17   |
| ADATA     | SU800              | 2 TB   | 6       | 88    | 1     | 0.17   |
| WDC       | WDS480G2G0A-00JH30 | 480 GB | 52      | 74    | 1     | 0.17   |
| SanDisk   | SDSSDH2064G        | 64 GB  | 1       | 62    | 0     | 0.17   |
| Samsung   | MZ7LN256HAJQ-000L2 | 256 GB | 23      | 62    | 0     | 0.17   |
| Lite-On   | L8H-256V2G         | 256 GB | 5       | 62    | 0     | 0.17   |
| Plextor   | PX-128M6S          | 128 GB | 29      | 71    | 74    | 0.17   |
| Intel     | SSDSC2BF480A5L     | 480 GB | 1       | 62    | 0     | 0.17   |
| Kingrich  | SSD 120G           | 120 GB | 1       | 62    | 0     | 0.17   |
| Netac     | W800S 512GB SSD    | 512 GB | 1       | 62    | 0     | 0.17   |
| SMI       | SSD DISK           | 500 GB | 1       | 62    | 0     | 0.17   |
| SanDisk   | SD5SF2032G1010E    | 32 GB  | 2       | 62    | 0     | 0.17   |
| Micron    | MTFDDAV256MBF-1... | 256 GB | 10      | 61    | 0     | 0.17   |
| Advantech | SQF-S25M8-128G-AAG | 128 GB | 1       | 61    | 0     | 0.17   |
| Samsung   | SSD 870 QVO        | 8 TB   | 5       | 61    | 0     | 0.17   |
| Toshiba   | Q200 EX            | 240 GB | 1       | 61    | 0     | 0.17   |
| SK hynix  | HFS128G39TNF-N3A0A | 128 GB | 6       | 61    | 0     | 0.17   |
| Lite-On   | LMH-256V2M-11 M... | 256 GB | 6       | 61    | 0     | 0.17   |
| SPCC      | M.2 SSD            | 120 GB | 4       | 106   | 1     | 0.17   |
| Lite-On   | CV6-8Q128          | 128 GB | 2       | 61    | 0     | 0.17   |
| Lite-On   | IT L8T-128L9G      | 128 GB | 2       | 61    | 0     | 0.17   |
| Gigabyte  | GP-GSTFS31100TNTD  | 1 TB   | 1       | 61    | 0     | 0.17   |
| Platinet  | SSD                | 120 GB | 3       | 61    | 30    | 0.17   |
| Goodram   | IRIDIUM PRO        | 240 GB | 1       | 60    | 0     | 0.17   |
| Lexar     | 128GB SSD          | 128 GB | 18      | 60    | 0     | 0.17   |
| SPCC      | SSDB28             | 128 GB | 2       | 76    | 1     | 0.17   |
| QUMO      | SSD                | 256 GB | 1       | 60    | 0     | 0.17   |
| Transcend | TS960GMTS820S      | 960 GB | 1       | 60    | 0     | 0.17   |
| EMTEC     | X150               | 480 GB | 4       | 60    | 0     | 0.17   |
| Super ... | FNX256MORM         | 256 GB | 1       | 60    | 0     | 0.17   |
| Toshiba   | THNSN9480GESG      | 480 GB | 1       | 60    | 0     | 0.17   |
| SUNEAST   | SSD SE800          | 1.9 TB | 1       | 60    | 0     | 0.16   |
| China     | SSD                | 128 GB | 52      | 61    | 1     | 0.16   |
| Kingston  | RBUSNS8180DS3256GJ | 256 GB | 7       | 71    | 1     | 0.16   |
| Kingston  | SKC6001024G        | 1 TB   | 9       | 59    | 0     | 0.16   |
| China     | SSD128GBS800       | 128 GB | 2       | 59    | 0     | 0.16   |
| Intenso   | JAJM600M1024C      | 1 TB   | 1       | 59    | 0     | 0.16   |
| Lite-On   | CV3-8D512-11 SATA  | 512 GB | 1       | 59    | 0     | 0.16   |
| PNY       | SSD2SC240G1CS17... | 240 GB | 1       | 59    | 0     | 0.16   |
| Intenso   | C500               | 256 GB | 2       | 59    | 0     | 0.16   |
| KingDian  | S400               | 240 GB | 1       | 59    | 0     | 0.16   |
| ADATA     | SU630              | 480 GB | 17      | 74    | 219   | 0.16   |
| Lite-On   | CV3-SD256          | 256 GB | 2       | 59    | 0     | 0.16   |
| Kingston  | RBU-SUS151S364GD   | 64 GB  | 4       | 59    | 0     | 0.16   |
| AGI       | AGI240G18AI238     | 240 GB | 1       | 59    | 0     | 0.16   |
| TEKET     | SA18-032M-4F       | 32 GB  | 2       | 59    | 0     | 0.16   |
| EYOTA     | SSD                | 256 GB | 1       | 58    | 0     | 0.16   |
| FORESEE   | 128GB SSD          | 128 GB | 17      | 58    | 0     | 0.16   |
| Plextor   | PX-512M6Pro        | 512 GB | 1       | 58    | 0     | 0.16   |
| HP        | SSD S700 Pro       | 256 GB | 2       | 58    | 0     | 0.16   |
| Kingston  | SA400S37-240GB     | 240 GB | 1       | 58    | 0     | 0.16   |
| Kingston  | SKC380S3240G       | 240 GB | 1       | 58    | 0     | 0.16   |
| AMD       | R5SL120G           | 120 GB | 20      | 65    | 1     | 0.16   |
| Zheino    | CHN 25SATAC3 120   | 120 GB | 1       | 58    | 0     | 0.16   |
| Team      | T2535T480G         | 480 GB | 3       | 863   | 29    | 0.16   |
| Team      | T253LE120G         | 120 GB | 4       | 58    | 0     | 0.16   |
| tigo      | SSD                | 120 GB | 1       | 57    | 0     | 0.16   |
| KingSpec  | MSH-256            | 256 GB | 3       | 57    | 0     | 0.16   |
| China     | 512GB SSD          | 512 GB | 2       | 57    | 0     | 0.16   |
| Lite-On   | LMT-32L3M-HP       | 32 GB  | 3       | 57    | 0     | 0.16   |
| Netac     | SSD                | 480 GB | 3       | 57    | 0     | 0.16   |
| Lite-On   | IT LCS-128L9S      | 128 GB | 2       | 57    | 0     | 0.16   |
| Plextor   | PX-256M6S          | 256 GB | 11      | 70    | 195   | 0.16   |
| Goldkey   | GKH84-64GB         | 64 GB  | 1       | 57    | 0     | 0.16   |
| Micron    | M600_MTFDDAV128MBF | 128 GB | 2       | 57    | 0     | 0.16   |
| WDC       | WDS100T2G0A-00JH30 | 1 TB   | 25      | 59    | 3     | 0.16   |
| DeTech    | SSD                | 120 GB | 1       | 57    | 0     | 0.16   |
| ANACOMDA  | A1                 | 120 GB | 1       | 57    | 0     | 0.16   |
| TCSUNBOW  | X3                 | 64 GB  | 2       | 56    | 0     | 0.16   |
| SanDisk   | X600 M.2 2280 SATA | 256 GB | 1       | 56    | 0     | 0.16   |
| PNY       | SSD2SC120G1LC76... | 120 GB | 1       | 56    | 0     | 0.16   |
| Lite-On   | IT L8T-128L9G-HP   | 128 GB | 1       | 56    | 0     | 0.16   |
| Leven     | JAJS600M512C       | 512 GB | 6       | 56    | 0     | 0.16   |
| EZCOOL    | S400               | 120 GB | 1       | 56    | 0     | 0.15   |
| Goodram   | IRP-SSDPR-S25C-256 | 256 GB | 3       | 56    | 0     | 0.15   |
| PNY       | SSD2SC240G1SAHT... | 240 GB | 1       | 56    | 0     | 0.15   |
| Transcend | TS256GSSD370       | 256 GB | 2       | 56    | 0     | 0.15   |
| Super ... | FTM50N325H         | 500 GB | 2       | 56    | 0     | 0.15   |
| Plextor   | PX-256M6Pro        | 256 GB | 3       | 91    | 2     | 0.15   |
| Colorful  | SL500              | 240 GB | 3       | 56    | 0     | 0.15   |
| China     | SATA SSD           | 960 GB | 3       | 56    | 0     | 0.15   |
| Samsung   | SSD 870 EVO        | 1 TB   | 81      | 66    | 17    | 0.15   |
| Dogfish   | SSD                | 256 GB | 5       | 55    | 0     | 0.15   |
| Smartbuy  | mSata              | 256 GB | 2       | 55    | 0     | 0.15   |
| PNY       | SSD2SC120G1SA75... | 120 GB | 1       | 55    | 0     | 0.15   |
| Patriot   | P200               | 1 TB   | 4       | 78    | 11    | 0.15   |
| Patriot   | P210               | 1 TB   | 3       | 71    | 1     | 0.15   |
| OWC       | Neptune 6G SSD     | 480 GB | 2       | 55    | 0     | 0.15   |
| Mushkin   | MKNSSDCR480GB      | 480 GB | 1       | 55    | 0     | 0.15   |
| Apacer    | AST280             | 240 GB | 2       | 55    | 0     | 0.15   |
| China     | SH00R240GB         | 240 GB | 6       | 54    | 0     | 0.15   |
| Transcend | TS256GMTS430S      | 256 GB | 11      | 54    | 0     | 0.15   |
| TAMMUZ    | SSD                | 128 GB | 1       | 54    | 0     | 0.15   |
| SanDisk   | SSD i100           | 64 GB  | 1       | 54    | 0     | 0.15   |
| Team      | T253X1480G         | 480 GB | 7       | 54    | 0     | 0.15   |
| ADATA     | SP580              | 960 GB | 2       | 54    | 0     | 0.15   |
| Aoluska   | A6-120G            | 120 GB | 1       | 54    | 0     | 0.15   |
| Samsung   | MCCOE64G8MPP-0VA   | 64 GB  | 1       | 377   | 6     | 0.15   |
| SanDisk   | SD8SBAT-256G-1006  | 256 GB | 2       | 53    | 0     | 0.15   |
| Samsung   | SSD 870 QVO        | 2 TB   | 47      | 53    | 0     | 0.15   |
| Drevo     | X1 SSD             | 120 GB | 9       | 206   | 12    | 0.15   |
| Transcend | TS64GMTS800S       | 64 GB  | 1       | 53    | 0     | 0.15   |
| Kingston  | SHPM2280P2-240G    | 240 GB | 1       | 1557  | 28    | 0.15   |
| ADATA     | SU900              | 256 GB | 8       | 115   | 30    | 0.15   |
| KingSpec  | P3-128             | 128 GB | 19      | 79    | 9     | 0.15   |
| Intel     | SSDSA2M160G2LE     | 160 GB | 2       | 1075  | 16    | 0.15   |
| SanDisk   | SSD i100           | 8 GB   | 4       | 53    | 0     | 0.15   |
| INNOVA... | SSD_2.5"_TLC_51... | 512 GB | 3       | 53    | 0     | 0.15   |
| Samsung   | MZMTD128HAFV-000H1 | 128 GB | 1       | 53    | 0     | 0.15   |
| Zheino    | CHN-25SATAA3-480   | 480 GB | 2       | 53    | 0     | 0.15   |
| XrayDisk  | SSD                | 120 GB | 4       | 53    | 0     | 0.15   |
| Patriot   | P200               | 256 GB | 6       | 63    | 31    | 0.14   |
| OCZ       | D2CSTK251M3T-0480  | 480 GB | 1       | 52    | 0     | 0.14   |
| Crucial   | CT1024M550SSD1     | 1 TB   | 1       | 897   | 16    | 0.14   |
| Lite-On   | LCS-128M6S-HP      | 128 GB | 7       | 63    | 145   | 0.14   |
| Lite-On   | LGT-128M6G         | 128 GB | 1       | 52    | 0     | 0.14   |
| PNY       | CS900 500GB SSD    | 500 GB | 26      | 52    | 0     | 0.14   |
| SK hynix  | HFS128G32MND-2200A | 128 GB | 1       | 157   | 2     | 0.14   |
| Crucial   | CT250BX100SSD1     | 250 GB | 43      | 53    | 1     | 0.14   |
| Intenso   | SSD Sata III       | 120 GB | 18      | 63    | 48    | 0.14   |
| Intel     | SSDSCKKB240G8      | 240 GB | 1       | 52    | 0     | 0.14   |
| BIWIN     | SSD                | 256 GB | 2       | 52    | 0     | 0.14   |
| Lite-On   | L8H-128V2G-11 M... | 128 GB | 3       | 52    | 0     | 0.14   |
| Phison    | SATA SSD           | 960 GB | 3       | 52    | 0     | 0.14   |
| Corsair   | Neutron GTX SSD    | 120 GB | 4       | 1432  | 112   | 0.14   |
| IPLEX     | TITAN256XP         | 256 GB | 1       | 52    | 0     | 0.14   |
| AMD       | R3SL60G            | 64 GB  | 4       | 121   | 1     | 0.14   |
| PNY       | SSD2SC240G1SA75... | 240 GB | 3       | 51    | 0     | 0.14   |
| SanDisk   | SDSSDH3256G        | 256 GB | 3       | 51    | 0     | 0.14   |
| China     | SATA SSD           | 16 GB  | 1       | 1295  | 24    | 0.14   |
| Lite-On   | LMT-19nmBGA-128G   | 128 GB | 1       | 51    | 0     | 0.14   |
| Apacer    | AS350              | 128 GB | 33      | 51    | 0     | 0.14   |
| ADATA     | SP610              | 128 GB | 3       | 51    | 0     | 0.14   |
| KingDian  | S280               | 240 GB | 13      | 51    | 0     | 0.14   |
| Toshiba   | THNSFC128GBSJ      | 128 GB | 1       | 51    | 0     | 0.14   |
| Smartbuy  | SSD                | 128 GB | 4       | 51    | 0     | 0.14   |
| Hyundai   | C2S3T-240G         | 240 GB | 2       | 51    | 0     | 0.14   |
| Seagate   | ZA1920NM10001      | 1.9 TB | 4       | 51    | 0     | 0.14   |
| Micron    | MTFDDAK256MAY-1... | 256 GB | 2       | 870   | 16    | 0.14   |
| Intel     | SSDSCKKF512G8 SATA | 512 GB | 2       | 50    | 0     | 0.14   |
| Lite-On   | LCH-512V2S         | 512 GB | 3       | 50    | 0     | 0.14   |
| Maxtor    | Z1 SSD             | 480 GB | 4       | 50    | 0     | 0.14   |
| KingSpec  | NT-512             | 512 GB | 8       | 64    | 2     | 0.14   |
| Samsung   | SSD PB22-CS3 FD... | 256 GB | 1       | 50    | 0     | 0.14   |
| OCZ       | INTREPID 3800      | 400 GB | 1       | 50    | 0     | 0.14   |
| China     | WPC-240GB          | 240 GB | 1       | 49    | 0     | 0.14   |
| Corsair   | Neutron GTX SSD    | 480 GB | 1       | 49    | 0     | 0.14   |
| Kingmax   | SSD                | 240 GB | 6       | 118   | 234   | 0.14   |
| Crucial   | CT128M550SSD1      | 128 GB | 6       | 172   | 21    | 0.14   |
| Transcend | TS128GMSA230S      | 128 GB | 2       | 49    | 0     | 0.14   |
| Seagate   | BarraCuda SSD Z... | 500 GB | 10      | 49    | 0     | 0.14   |
| V-GeN     | V-GEN12AS19AR12... | 120 GB | 1       | 49    | 0     | 0.14   |
| KingDian  | S200               | 120 GB | 2       | 49    | 0     | 0.13   |
| Greenl... | 32GB ArmourDrive   | 32 GB  | 1       | 49    | 0     | 0.13   |
| Transcend | TS128GMTS400       | 128 GB | 5       | 49    | 0     | 0.13   |
| SanDisk   | SDSA5DK 32G        | 32 GB  | 1       | 49    | 0     | 0.13   |
| Lexar     | 240GB SSD          | 240 GB | 5       | 48    | 0     | 0.13   |
| Vaseky    | V800-128G          | 128 GB | 2       | 48    | 0     | 0.13   |
| Transcend | TS240GMTS420S      | 240 GB | 14      | 53    | 8     | 0.13   |
| Team      | T253X2001T         | 1 TB   | 8       | 48    | 0     | 0.13   |
| Transcend | TS128GMTS800       | 128 GB | 10      | 48    | 0     | 0.13   |
| Lexar     | SSD                | 240 GB | 3       | 48    | 0     | 0.13   |
| Zheino    | CHN 25SATAA3 120   | 120 GB | 3       | 48    | 0     | 0.13   |
| Anobit    | Gen2A400 118032738 | 400 GB | 2       | 48    | 1     | 0.13   |
| Hikvision | HS-SSD-C100 120G   | 120 GB | 6       | 48    | 0     | 0.13   |
| Netac     | SSD                | 2 TB   | 1       | 48    | 0     | 0.13   |
| Lexar     | 256GB SSD          | 256 GB | 18      | 48    | 0     | 0.13   |
| Hoodisk   | SSD                | 256 GB | 5       | 48    | 0     | 0.13   |
| OCZ       | VECTOR180          | 480 GB | 1       | 48    | 0     | 0.13   |
| SK hynix  | HFS128G32MND-3212A | 128 GB | 1       | 48    | 0     | 0.13   |
| GeIL      | R3 120G            | 120 GB | 1       | 47    | 0     | 0.13   |
| Lite-On   | IT LMH-256V2M      | 256 GB | 1       | 47    | 0     | 0.13   |
| China     | 80GB SSD           | 80 GB  | 2       | 47    | 0     | 0.13   |
| FORESEE   | 64GB SSD           | 64 GB  | 4       | 47    | 0     | 0.13   |
| Intenso   | JAJM600M1TB        | 1 TB   | 2       | 47    | 0     | 0.13   |
| Plextor   | PX-256M8VG         | 256 GB | 3       | 47    | 0     | 0.13   |
| Transcend | TS64GSSD370S       | 64 GB  | 4       | 47    | 0     | 0.13   |
| Teclast   | 120GB S500         | 120 GB | 1       | 47    | 0     | 0.13   |
| ADATA     | SU635              | 480 GB | 3       | 82    | 69    | 0.13   |
| ADATA     | SU650NS38          | 240 GB | 8       | 47    | 0     | 0.13   |
| Phison    | 128GB PS3109-S9    | 128 GB | 2       | 77    | 1     | 0.13   |
| GLOWAY    | FER120GS3-S7       | 120 GB | 4       | 46    | 0     | 0.13   |
| KingSpec  | Q-180              | 180 GB | 5       | 53    | 188   | 0.13   |
| INNOVA... | SSD_2.5"_TLC_24... | 240 GB | 1       | 46    | 0     | 0.13   |
| RCESSD    | SSD                | 512 GB | 2       | 46    | 0     | 0.13   |
| ADATA     | SU800NS38          | 1 TB   | 5       | 46    | 0     | 0.13   |
| EMTEC     | X250               | 512 GB | 2       | 46    | 0     | 0.13   |
| Leven     | JAJS600M128C       | 128 GB | 5       | 46    | 0     | 0.13   |
| Crucial   | CT3500SC           | 500 GB | 2       | 465   | 11    | 0.13   |
| LENSEN    | LS600 120G         | 120 GB | 1       | 46    | 0     | 0.13   |
| EMTEC     | X150               | 240 GB | 8       | 46    | 0     | 0.13   |
| KingDian  | N400               | 32 GB  | 1       | 45    | 0     | 0.13   |
| Plextor   | PX-256M8VC         | 256 GB | 6       | 45    | 0     | 0.13   |
| SK hynix  | HFS256G32TNH-73A0A | 256 GB | 4       | 45    | 0     | 0.13   |
| TCSUNBOW  | X3                 | 120 GB | 3       | 45    | 0     | 0.12   |
| Apacer    | AS350              | 256 GB | 27      | 45    | 0     | 0.12   |
| Kingston  | RBU-SC152S37128GG2 | 128 GB | 1       | 45    | 0     | 0.12   |
| Zheino    | CHN mSATA02M 128   | 128 GB | 1       | 45    | 0     | 0.12   |
| BHT       | WR202H0032G E70... | 32 GB  | 1       | 45    | 0     | 0.12   |
| Lite-On   | CV8-8E256-11 SATA  | 256 GB | 5       | 45    | 0     | 0.12   |
| Intel     | SSDSCKKF256H6L     | 256 GB | 2       | 51    | 29    | 0.12   |
| Samsung   | SSD 870 QVO        | 1 TB   | 101     | 45    | 0     | 0.12   |
| KingSpec  | MT-128             | 128 GB | 6       | 45    | 0     | 0.12   |
| China     | M10C               | 128 GB | 1       | 44    | 0     | 0.12   |
| MARSHAL   | MAL2128SA-LS3DL... | 128 GB | 1       | 44    | 0     | 0.12   |
| BIWIN     | SSD                | 128 GB | 9       | 86    | 344   | 0.12   |
| Intenso   | A200-240GB         | 240 GB | 1       | 44    | 0     | 0.12   |
| SanDisk   | Z400s 2.5 7MM      | 256 GB | 1       | 44    | 0     | 0.12   |
| Intel     | SSDSC2KW256G8L     | 256 GB | 2       | 44    | 0     | 0.12   |
| Silicon   | SATA3 128GB SSD    | 128 GB | 1       | 44    | 0     | 0.12   |
| FATTYDOVE | SSD                | 48 GB  | 1       | 44    | 0     | 0.12   |
| PRETEC    | G2000 SSD          | 32 GB  | 1       | 44    | 0     | 0.12   |
| XPG       | SX950U             | 240 GB | 2       | 44    | 0     | 0.12   |
| ADATA     | SP550              | 120 GB | 40      | 44    | 1     | 0.12   |
| Crucial   | CT512M550SSD3      | 512 GB | 6       | 171   | 123   | 0.12   |
| Dogfish   | SSD                | 128 GB | 3       | 43    | 0     | 0.12   |
| Goodram   | SSDPR-CL100-240-G3 | 240 GB | 5       | 43    | 0     | 0.12   |
| Plextor   | PX-512M3           | 512 GB | 1       | 1402  | 31    | 0.12   |
| Faspeed   | K7N8-256GF         | 256 GB | 1       | 43    | 0     | 0.12   |
| Seagate   | BarraCuda Q1 SS... | 240 GB | 2       | 43    | 0     | 0.12   |
| KingSpec  | P4-60              | 64 GB  | 1       | 43    | 0     | 0.12   |
| Lite-On   | LMT-19nmBGA-256G   | 256 GB | 1       | 43    | 0     | 0.12   |
| KingSpec  | Q-720              | 720 GB | 4       | 43    | 0     | 0.12   |
| Transcend | TS64GMSA370        | 64 GB  | 3       | 43    | 0     | 0.12   |
| Toshiba   | KSG60ZMV256G       | 256 GB | 3       | 43    | 0     | 0.12   |
| Intel     | SSDMAEMC080G2L     | 80 GB  | 1       | 564   | 12    | 0.12   |
| Ramsta    | SSD S800           | 480 GB | 1       | 43    | 0     | 0.12   |
| Intel     | SSDSCKJW240H6      | 240 GB | 1       | 42    | 0     | 0.12   |
| Samsung   | 860-500GB          | 512 GB | 1       | 42    | 0     | 0.12   |
| SUNEAST   | SSD SE800 mSATA    | 480 GB | 1       | 42    | 0     | 0.12   |
| Foxline   | FLSSD256X5SE       | 256 GB | 4       | 42    | 0     | 0.12   |
| Intel     | SSDSCKKF010X6      | 1 TB   | 1       | 42    | 0     | 0.12   |
| PNY       | SSD2SC120G5LC70... | 120 GB | 1       | 42    | 0     | 0.12   |
| Teclast   | 480GB A900         | 480 GB | 1       | 42    | 0     | 0.12   |
| China     | SSD128G            | 128 GB | 1       | 42    | 0     | 0.12   |
| Londisk   | SSD                | 240 GB | 3       | 42    | 0     | 0.12   |
| Kingston  | RBUSNS8180S3256GJ  | 256 GB | 5       | 42    | 0     | 0.12   |
| Goodram   | SSDPR-CX400-128-G2 | 128 GB | 15      | 42    | 0     | 0.12   |
| SanDisk   | SD8SFAT128G1122    | 128 GB | 1       | 42    | 0     | 0.12   |
| Transcend | TS120GMTS420S      | 120 GB | 21      | 43    | 1     | 0.12   |
| KingFast  | SSD                | 1 TB   | 1       | 42    | 0     | 0.12   |
| Micron    | MTFDDAT256MAM-1K2  | 256 GB | 3       | 597   | 337   | 0.12   |
| China     | SSD                | 256 GB | 27      | 42    | 1     | 0.12   |
| ShanDi... | SSD                | 512 GB | 4       | 42    | 0     | 0.12   |
| KingSpec  | NT-64              | 64 GB  | 1       | 41    | 0     | 0.11   |
| Transcend | TS240GMTS820S      | 240 GB | 4       | 41    | 0     | 0.11   |
| PNY       | SSD2SC240G5SA75... | 240 GB | 1       | 41    | 0     | 0.11   |
| Crucial   | CT480BX200SSD1     | 480 GB | 5       | 41    | 0     | 0.11   |
| SanDisk   | SD8SBAT128G1002    | 128 GB | 3       | 41    | 0     | 0.11   |
| Team      | T2535T120G         | 120 GB | 4       | 77    | 2     | 0.11   |
| SanDisk   | SD6PP4M-256G-1006  | 256 GB | 4       | 143   | 14    | 0.11   |
| Dogfish   | SSD                | 120 GB | 2       | 41    | 0     | 0.11   |
| Intel     | SSDSC2KF480H6L     | 480 GB | 1       | 82    | 1     | 0.11   |
| GALAX     | TA1D0240A          | 240 GB | 1       | 41    | 0     | 0.11   |
| Plextor   | PX-128M6Pro        | 128 GB | 11      | 49    | 1     | 0.11   |
| Intenso   | SSD                | 120 GB | 11      | 79    | 189   | 0.11   |
| China     | SSD                | 480 GB | 13      | 40    | 0     | 0.11   |
| Goodram   | SSDPR-S400U-120-80 | 120 GB | 1       | 40    | 0     | 0.11   |
| Lite-On   | LMT-128M6M         | 128 GB | 2       | 40    | 0     | 0.11   |
| Hikvision | HS-SSD-E100 1024G  | 1 TB   | 1       | 40    | 0     | 0.11   |
| Dogeish   | SSD                | 128 GB | 1       | 40    | 0     | 0.11   |
| Lenovo    | SSD SL700          | 1 TB   | 1       | 40    | 0     | 0.11   |
| LDLC      | SSD                | 240 GB | 3       | 39    | 0     | 0.11   |
| KingDian  | P10                | 240 GB | 1       | 39    | 0     | 0.11   |
| XrayDisk  | SSD                | 512 GB | 1       | 39    | 0     | 0.11   |
| Seagate   | ST480HM000         | 480 GB | 1       | 39    | 0     | 0.11   |
| Hikvision | HS-SSD-C100 480G   | 480 GB | 2       | 39    | 0     | 0.11   |
| V-GeN     | V-GEN08SM20AR12... | 128 GB | 1       | 39    | 0     | 0.11   |
| Netac     | SSD                | 512 GB | 8       | 39    | 0     | 0.11   |
| MediaR... | MR1002             | 240 GB | 1       | 39    | 0     | 0.11   |
| Corsair   | Force LX SSD       | 256 GB | 1       | 39    | 0     | 0.11   |
| Lite-On   | LMT-128M6M-HP      | 128 GB | 1       | 39    | 0     | 0.11   |
| PNY       | CS900 250GB SSD    | 250 GB | 8       | 38    | 0     | 0.11   |
| Kingston  | SQ500S37240G       | 240 GB | 5       | 38    | 0     | 0.11   |
| Verbatim  | Vi500 S3 240GB SSD | 240 GB | 2       | 38    | 0     | 0.11   |
| Lite-On   | CMT-64L3M          | 64 GB  | 4       | 138   | 528   | 0.11   |
| PNY       | SSD2SC240G1CS27... | 240 GB | 1       | 38    | 0     | 0.11   |
| China     | SATA3 240GB SSD    | 240 GB | 5       | 56    | 2     | 0.11   |
| Kingston  | SH103S3480G        | 480 GB | 1       | 38    | 0     | 0.11   |
| ADATA     | SU655              | 480 GB | 2       | 38    | 0     | 0.11   |
| KingDian  | S200               | 64 GB  | 8       | 69    | 17    | 0.11   |
| DOGFISH   | SSD                | 256 GB | 1       | 38    | 0     | 0.11   |
| Patriot   | P210               | 256 GB | 8       | 38    | 0     | 0.11   |
| Micron    | MTFDDAV256TBN      | 256 GB | 1       | 114   | 2     | 0.10   |
| Kingston  | SV300S37A-60G      | 64 GB  | 2       | 38    | 0     | 0.10   |
| China     | SATA SSD           | 512 GB | 4       | 38    | 0     | 0.10   |
| Toshiba   | THNSNK512GVN8      | 512 GB | 1       | 38    | 0     | 0.10   |
| Faspeed   | K5-120G            | 120 GB | 1       | 38    | 0     | 0.10   |
| Neo Forza | NFS011SA396-600... | 960 GB | 1       | 341   | 8     | 0.10   |
| KingDian  | S280-240GB         | 240 GB | 12      | 71    | 309   | 0.10   |
| Micron    | MTFDDAK512MAM-1K1  | 512 GB | 3       | 309   | 956   | 0.10   |
| Intenso   | SSD SATAIII        | 240 GB | 41      | 40    | 1     | 0.10   |
| Zheino    | CHN-mSATAM3-128    | 128 GB | 1       | 37    | 0     | 0.10   |
| Drevo     | X1-60G             | 64 GB  | 1       | 37    | 0     | 0.10   |
| BAITITON  | BT58SSD15S         | 2 TB   | 1       | 37    | 0     | 0.10   |
| Zheino    | CHN-mSATAQ3-480    | 480 GB | 1       | 37    | 0     | 0.10   |
| HP        | SSD S700 Pro       | 1 TB   | 2       | 37    | 0     | 0.10   |
| Crucial   | CT250MX500SSD1N    | 250 GB | 1       | 37    | 0     | 0.10   |
| Transcend | TS512GMTS430S      | 512 GB | 14      | 37    | 0     | 0.10   |
| SanDisk   | SDSSDHP64G         | 64 GB  | 1       | 37    | 0     | 0.10   |
| Hikvision | HS-SSD-C100 240G   | 240 GB | 4       | 37    | 0     | 0.10   |
| Lite-On   | LCH-256V2S-11 2... | 256 GB | 4       | 36    | 1     | 0.10   |
| China     | SSD                | 360 GB | 11      | 36    | 0     | 0.10   |
| Intel     | SSDSCKKF128G8 SATA | 128 GB | 6       | 50    | 2     | 0.10   |
| Transcend | TS512GMSA370       | 512 GB | 2       | 36    | 0     | 0.10   |
| Intenso   | SSD Sata III       | 256 GB | 19      | 39    | 28    | 0.10   |
| Dogfish   | SSD                | 1 TB   | 3       | 36    | 0     | 0.10   |
| China     | Solid              | 480 GB | 4       | 35    | 0     | 0.10   |
| oyunkey   | SSD                | 120 GB | 2       | 215   | 66    | 0.10   |
| T-FORCE   | SSD                | 512 GB | 3       | 35    | 0     | 0.10   |
| PNY       | SSD2SC120G726A1... | 120 GB | 1       | 35    | 0     | 0.10   |
| SK hynix  | SC401 SATA         | 512 GB | 8       | 147   | 362   | 0.10   |
| SK hynix  | HFS1T9G32FEH-7A10A | 1.9 TB | 3       | 35    | 0     | 0.10   |
| SanDisk   | SD8SBAT256G1122    | 256 GB | 12      | 35    | 1     | 0.10   |
| Transcend | TS256GMSA370       | 256 GB | 1       | 35    | 0     | 0.10   |
| BIOSTAR   | S100-120GB         | 120 GB | 3       | 35    | 0     | 0.10   |
| Lite-On   | IT LMT-128L9M      | 128 GB | 2       | 35    | 0     | 0.10   |
| Lite-On   | LSS-32L6G-HP       | 32 GB  | 5       | 124   | 203   | 0.10   |
| Zheino    | CHN 25SATAS3 256   | 256 GB | 2       | 34    | 0     | 0.10   |
| takeMS    | SSD UTX-2200       | 240 GB | 1       | 34    | 0     | 0.10   |
| Plextor   | PX-256S3C          | 256 GB | 1       | 34    | 0     | 0.10   |
| Innodisk  | Corp. - mSATA 3... | 128 GB | 1       | 34    | 0     | 0.10   |
| Toshiba   | KHK61RSE1T92       | 1.9 TB | 8       | 34    | 0     | 0.10   |
| PNY       | SSD2SC240G1LC70... | 240 GB | 2       | 34    | 0     | 0.10   |
| Plextor   | PX-64M5M           | 64 GB  | 1       | 34    | 0     | 0.10   |
| Hyundai   | C2S3T-120G         | 120 GB | 1       | 34    | 0     | 0.09   |
| ZOTAC     | SATA SSD           | 120 GB | 2       | 34    | 0     | 0.09   |
| SanDisk   | SD8SN8U128G1122    | 128 GB | 1       | 34    | 0     | 0.09   |
| Dogfish   | SSD                | 512 GB | 7       | 34    | 0     | 0.09   |
| Micron    | MTFDDAV512TBN-1... | 512 GB | 3       | 41    | 2     | 0.09   |
| SMI       | SSD DISK           | 256 GB | 1       | 33    | 0     | 0.09   |
| HP        | SSD S700 Pro       | 128 GB | 3       | 33    | 0     | 0.09   |
| AMD       | R5S240GBSF         | 240 GB | 1       | 33    | 0     | 0.09   |
| Intel     | SSDSA1MH080G1HP    | 80 GB  | 1       | 33    | 0     | 0.09   |
| RECADATA  | RD-S325MCN-N2563   | 240 GB | 1       | 33    | 0     | 0.09   |
| Super ... | FTM56N325H         | 256 GB | 2       | 33    | 0     | 0.09   |
| SMI       | SSD DISK           | 497 GB | 1       | 33    | 0     | 0.09   |
| SanDisk   | SD6SB1M-032G-1006  | 32 GB  | 1       | 33    | 0     | 0.09   |
| KingSpec  | ACSC2M064mSA       | 64 GB  | 2       | 33    | 0     | 0.09   |
| TCSUNBOW  | X3                 | 240 GB | 3       | 33    | 0     | 0.09   |
| Lite-On   | LGT-256M6G         | 256 GB | 3       | 33    | 0     | 0.09   |
| Corsair   | CSSD-F120GB3-BK    | 120 GB | 2       | 58    | 509   | 0.09   |
| SanDisk   | SDSSDX480GG25      | 480 GB | 4       | 971   | 471   | 0.09   |
| Smartbuy  | mSata              | 128 GB | 2       | 32    | 0     | 0.09   |
| Pioneer   | APS-SL3N-256       | 256 GB | 2       | 32    | 0     | 0.09   |
| Lite-On   | LST-32S9G-11 SATA  | 32 GB  | 2       | 32    | 0     | 0.09   |
| Samsung   | SSD PM851          | 128 GB | 1       | 32    | 0     | 0.09   |
| FORESEE   | 256GB SSD          | 256 GB | 9       | 32    | 0     | 0.09   |
| KingSpec  | ACSC4M512mSA       | 506 GB | 1       | 32    | 0     | 0.09   |
| OCZ       | VERTEX4            | 80 GB  | 1       | 129   | 3     | 0.09   |
| Lite-On   | L8T-128L6G-HP      | 128 GB | 2       | 32    | 640   | 0.09   |
| HEORIADY  | HX-001 F 512G      | 512 GB | 2       | 32    | 0     | 0.09   |
| OSCOO     | OSC SSD            | 512 GB | 1       | 32    | 0     | 0.09   |
| Toshiba   | THNSNB062GMCJ      | 64 GB  | 1       | 32    | 0     | 0.09   |
| Goodram   | SSDPR-CX400-512-G2 | 512 GB | 9       | 31    | 0     | 0.09   |
| Transcend | TS1TMTS800         | 1 TB   | 1       | 31    | 0     | 0.09   |
| Transcend | TS512GMTS400       | 512 GB | 1       | 31    | 0     | 0.09   |
| Hikvision | HS-SSD-E100 128G   | 128 GB | 3       | 61    | 1     | 0.09   |
| Samsung   | SSD 870 EVO        | 250 GB | 43      | 31    | 0     | 0.09   |
| Crucial   | CT1000BX100SSD1    | 1 TB   | 1       | 31    | 0     | 0.09   |
| China     | SH00R120GB         | 120 GB | 2       | 31    | 0     | 0.09   |
| Patriot   | Burst Elite        | 120 GB | 6       | 31    | 0     | 0.09   |
| SPCC      | 2.5?� SSD          | 1 TB   | 1       | 31    | 0     | 0.09   |
| Kingston  | RBUSNS8180DS3512GJ | 512 GB | 4       | 31    | 0     | 0.09   |
| SUNEAST   | SSD SE800          | 512 GB | 1       | 31    | 0     | 0.09   |
| China     | T480               | 480 GB | 2       | 65    | 138   | 0.09   |
| Intenso   | N900-512           | 512 GB | 1       | 93    | 2     | 0.09   |
| Mushkin   | MKNSSDRE512GB      | 512 GB | 1       | 31    | 0     | 0.09   |
| Smartbuy  | SSD                | 512 GB | 2       | 31    | 0     | 0.09   |
| Lite-On   | CV1-CC256          | 256 GB | 3       | 31    | 0     | 0.09   |
| KingSpec  | KSD-SA25.7-016MJ   | 16 GB  | 2       | 30    | 0     | 0.08   |
| Colorful  | SL500              | 480 GB | 3       | 38    | 65    | 0.08   |
| Kingston  | SKC600512G         | 512 GB | 15      | 30    | 0     | 0.08   |
| CFD       | CSSD-S6B480CG3VX   | 480 GB | 1       | 30    | 0     | 0.08   |
| Lite-On   | LCH-512V2S-11 2... | 512 GB | 2       | 30    | 0     | 0.08   |
| QUMO      | SSD                | 120 GB | 4       | 175   | 255   | 0.08   |
| Hikvision | HKVSN HS-SSD-C1... | 120 GB | 1       | 30    | 0     | 0.08   |
| Kingston  | RBUSC180DS37128GJ  | 128 GB | 5       | 30    | 0     | 0.08   |
| EMTEC     | X150               | 120 GB | 3       | 30    | 0     | 0.08   |
| Lite-On   | LCH-128V2S         | 128 GB | 4       | 30    | 0     | 0.08   |
| imation   | 2.5" SATA3 240G... | 240 GB | 1       | 30    | 0     | 0.08   |
| ADATA     | SU800NS38          | 256 GB | 13      | 43    | 258   | 0.08   |
| Intenso   | SSD Sata III       | 128 GB | 15      | 38    | 137   | 0.08   |
| Innodisk  | 2.5" SATA SSD 3... | 496 GB | 2       | 30    | 0     | 0.08   |
| Kingston  | OM8P0S3512B-A0     | 512 GB | 1       | 29    | 0     | 0.08   |
| SanDisk   | SSD PLUS           | 2 TB   | 6       | 29    | 0     | 0.08   |
| Lite-On   | L8H-256V2G-11 M... | 256 GB | 8       | 29    | 0     | 0.08   |
| SanDisk   | SDSA5DK-016G-1006  | 16 GB  | 1       | 29    | 0     | 0.08   |
| SanDisk   | SSD U100           | 64 GB  | 13      | 47    | 1     | 0.08   |
| KingPower | 1108 SSD           | 64 GB  | 1       | 29    | 0     | 0.08   |
| Lite-On   | LMT-64M6M-HP       | 64 GB  | 2       | 102   | 507   | 0.08   |
| Lite-On   | LMT-512L9M-11 M... | 512 GB | 1       | 29    | 0     | 0.08   |
| Win Me... | SWR128G-001HL      | 128 GB | 1       | 29    | 0     | 0.08   |
| Intenso   | SSD256GBS420       | 256 GB | 4       | 29    | 0     | 0.08   |
| Transcend | TS128GMSA370       | 128 GB | 4       | 29    | 0     | 0.08   |
| Patriot   | SDVPSA1910128      | 128 GB | 1       | 29    | 0     | 0.08   |
| Kingston  | RBUSC180DS37256GH  | 256 GB | 1       | 29    | 0     | 0.08   |
| Samsung   | SSD Thin uSATA ... | 128 GB | 1       | 378   | 12    | 0.08   |
| PUSKILL   | SSD                | 256 GB | 1       | 28    | 0     | 0.08   |
| Transcend | TS128GSSD25S-M     | 128 GB | 1       | 28    | 0     | 0.08   |
| Micron    | MTFDDAK512TBN-1... | 512 GB | 2       | 448   | 9     | 0.08   |
| Patriot   | P210               | 128 GB | 4       | 28    | 0     | 0.08   |
| ADATA     | SU720              | 1 TB   | 4       | 28    | 0     | 0.08   |
| China     | Mit-SSD512A        | 512 GB | 1       | 28    | 0     | 0.08   |
| Samsung   | SSD PM810 2.5" 7mm | 256 GB | 3       | 378   | 42    | 0.08   |
| Wdstars   | ssd nowm720A-512GB | 512 GB | 1       | 28    | 0     | 0.08   |
| Team      | T253X1240G         | 240 GB | 9       | 28    | 0     | 0.08   |
| INNOVA... | SSD                | 240 GB | 1       | 28    | 0     | 0.08   |
| Indilinx  | IND-S325S-256G     | 256 GB | 1       | 27    | 0     | 0.08   |
| Samsung   | MZ7LH240HAHQ-00005 | 240 GB | 3       | 27    | 0     | 0.08   |
| Kingmax   | SSD                | 64 GB  | 24      | 196   | 521   | 0.08   |
| QUMO      | SSD                | 240 GB | 3       | 27    | 0     | 0.08   |
| Micron    | MTFDDAK128MAY-1... | 128 GB | 4       | 470   | 16    | 0.08   |
| Goodram   | SSDPR-CL100-480-G3 | 480 GB | 2       | 39    | 27    | 0.08   |
| TAISU     | SSD 240G           | 240 GB | 1       | 27    | 0     | 0.08   |
| SenDisk   | C3-60G             | 64 GB  | 1       | 27    | 0     | 0.08   |
| Lite-On   | CV8-8E256          | 256 GB | 8       | 27    | 0     | 0.07   |
| Kingch... | SSD                | 360 GB | 1       | 27    | 0     | 0.07   |
| Intenso   | SSD Sata III       | 960 GB | 1       | 27    | 0     | 0.07   |
| Lenovo    | Thinklife SSD S... | 480 GB | 1       | 27    | 0     | 0.07   |
| KingSpec  | CHA-M2B7-M256      | 256 GB | 2       | 27    | 0     | 0.07   |
| BIWIN     | M6305              | 120 GB | 1       | 26    | 0     | 0.07   |
| Micron    | 5200_MTFDDAK960TDC | 960 GB | 1       | 26    | 0     | 0.07   |
| Pioneer   | APS-SL3N 120       | 120 GB | 1       | 26    | 0     | 0.07   |
| Hikvision | HS-SSD-E100 256G   | 256 GB | 2       | 26    | 0     | 0.07   |
| Samsung   | SSD 870 EVO        | 500 GB | 74      | 42    | 14    | 0.07   |
| China     | NGFF 2242 512GB... | 512 GB | 2       | 26    | 0     | 0.07   |
| ADATA     | SU655              | 240 GB | 2       | 26    | 0     | 0.07   |
| HECTRON   | HECX1-240G         | 240 GB | 1       | 26    | 0     | 0.07   |
| Transcend | TS64GSSD720        | 64 GB  | 1       | 26    | 0     | 0.07   |
| Kingston  | SKC600MS256G       | 256 GB | 1       | 26    | 0     | 0.07   |
| BHT       | WR202HH032G E70... | 32 GB  | 2       | 26    | 0     | 0.07   |
| KINGSPEED | SATA3-256GB        | 256 GB | 1       | 26    | 0     | 0.07   |
| Hikvision | HS-SSD-E100N 512G  | 512 GB | 1       | 26    | 0     | 0.07   |
| Plextor   | PX-256M6GV-2280    | 256 GB | 1       | 26    | 0     | 0.07   |
| Lite-On   | LMH-512V2M-11 M... | 512 GB | 1       | 26    | 0     | 0.07   |
| ExeGate   | EX276687RUS        | 120 GB | 1       | 26    | 0     | 0.07   |
| Pasoul    | OASDX-120G         | 120 GB | 1       | 25    | 0     | 0.07   |
| KingSpec  | T-120              | 120 GB | 1       | 25    | 0     | 0.07   |
| Transcend | TS256GMSA230S      | 256 GB | 3       | 25    | 0     | 0.07   |
| SanDisk   | Z400s M.2 2280     | 128 GB | 3       | 25    | 0     | 0.07   |
| Advantech | SQF-S25M8-256G-SAC | 256 GB | 1       | 25    | 0     | 0.07   |
| SanDisk   | SSD i110           | 128 GB | 2       | 25    | 0     | 0.07   |
| Lite-On   | LMH-256V2M-41 M... | 256 GB | 1       | 25    | 0     | 0.07   |
| Goodram   | IRP-SSDPR-S25C-512 | 512 GB | 4       | 24    | 0     | 0.07   |
| Lite-On   | CV5-8Q256          | 256 GB | 1       | 24    | 0     | 0.07   |
| Mushkin   | MKNSSDCR60GB-7     | 64 GB  | 2       | 81    | 2     | 0.07   |
| Apacer    | AS510S             | 256 GB | 1       | 24    | 0     | 0.07   |
| Corsair   | CSSD-V32GB2        | 32 GB  | 1       | 99    | 3     | 0.07   |
| Netac     | SSD                | 1 TB   | 4       | 24    | 0     | 0.07   |
| Leven     | JAJS300M480C       | 480 GB | 2       | 44    | 1     | 0.07   |
| LDLC      | SSD                | 128 GB | 5       | 24    | 0     | 0.07   |
| INNOVA... | SSD_2.5"_TLC_25... | 256 GB | 1       | 24    | 0     | 0.07   |
| Plextor   | PX-128S2C          | 128 GB | 2       | 24    | 0     | 0.07   |
| V-GeN     | V-GEN07SM20AR12... | 128 GB | 1       | 24    | 0     | 0.07   |
| Team      | L5 LITE SSD        | 64 GB  | 3       | 27    | 1     | 0.07   |
| PNY       | SSD2SC120G1CS17... | 120 GB | 3       | 24    | 0     | 0.07   |
| Intenso   | SSD Sata III       | 1 TB   | 2       | 23    | 0     | 0.07   |
| Samsung   | MZNLN512HCJH-000L2 | 512 GB | 1       | 23    | 0     | 0.07   |
| SK hynix  | SC210 mSATA        | 256 GB | 4       | 400   | 61    | 0.07   |
| PNY       | SSD2SC120G1SA75... | 120 GB | 1       | 23    | 0     | 0.07   |
| SNR       | ML 240             | 240 GB | 1       | 23    | 0     | 0.07   |
| BR        | SSD                | 256 GB | 1       | 23    | 0     | 0.06   |
| Apple     | SSD TS128E         | 121 GB | 5       | 90    | 39    | 0.06   |
| Kingch... | SSD                | 1 TB   | 1       | 23    | 0     | 0.06   |
| XrayDisk  | SSD                | 128 GB | 5       | 23    | 0     | 0.06   |
| Transcend | TS512GMTS800       | 512 GB | 3       | 81    | 340   | 0.06   |
| Leven     | JAJS300M240C       | 240 GB | 4       | 23    | 0     | 0.06   |
| addlink   | SATA SSD           | 1 TB   | 1       | 23    | 0     | 0.06   |
| Lite-On   | CV1-8B256          | 256 GB | 9       | 23    | 0     | 0.06   |
| PNY       | SSD2SC256GM1P3D... | 256 GB | 2       | 23    | 0     | 0.06   |
| Kingch... | SSD                | 32 GB  | 1       | 23    | 0     | 0.06   |
| EMTEC     | X150               | 960 GB | 1       | 23    | 0     | 0.06   |
| Transcend | TS128GSSD230S      | 128 GB | 17      | 23    | 0     | 0.06   |
| Lite-On   | CS1-SP16           | 16 GB  | 1       | 23    | 0     | 0.06   |
| Seagate   | QSCD-ST52570-128GB | 128 GB | 1       | 23    | 0     | 0.06   |
| GLOWAY    | FER240GS3-S7       | 240 GB | 1       | 23    | 0     | 0.06   |
| Kingston  | SA400M8480G        | 480 GB | 2       | 23    | 0     | 0.06   |
| TCSUNBOW  | N4                 | 240 GB | 1       | 22    | 0     | 0.06   |
| Intel     | SSDSA1M080G2HP     | 80 GB  | 2       | 342   | 17    | 0.06   |
| Plextor   | PX-128S1G          | 128 GB | 1       | 22    | 0     | 0.06   |
| Kingston  | SKC600256G         | 256 GB | 25      | 22    | 0     | 0.06   |
| Lite-On   | CV1-8B512-HP       | 512 GB | 3       | 22    | 0     | 0.06   |
| Toshiba   | THNSNS060GBSP      | 64 GB  | 1       | 22    | 0     | 0.06   |
| SK hynix  | HFS256G32MND-2200A | 256 GB | 3       | 298   | 173   | 0.06   |
| Samsung   | SSD 870 EVO        | 2 TB   | 17      | 70    | 91    | 0.06   |
| Kingston  | 480GBV500          | 480 GB | 1       | 22    | 0     | 0.06   |
| Plextor   | PX-128M6V          | 128 GB | 1       | 22    | 0     | 0.06   |
| Lite-On   | LMS-32L6M          | 32 GB  | 1       | 22    | 0     | 0.06   |
| Transcend | TS128GMSM360       | 128 GB | 1       | 22    | 0     | 0.06   |
| Zheino    | CHN25SATAS1 256    | 256 GB | 1       | 22    | 0     | 0.06   |
| Apacer    | 64GB SATA Flash... | 64 GB  | 1       | 22    | 0     | 0.06   |
| Ramaxel   | RTITF128PCA1MADL   | 128 GB | 1       | 22    | 0     | 0.06   |
| LDLC      | F6+M.2 240         | 240 GB | 1       | 22    | 0     | 0.06   |
| Foxline   | FLSSD480X5SE       | 480 GB | 1       | 22    | 0     | 0.06   |
| LDLC      | F7+120GB           | 120 GB | 1       | 22    | 0     | 0.06   |
| Gigastone | Prime Series       | 256 GB | 1       | 22    | 0     | 0.06   |
| Lite-On   | LCH-128V2S-HP      | 128 GB | 3       | 163   | 16    | 0.06   |
| ELSKY     | SSD 64G            | 64 GB  | 1       | 21    | 0     | 0.06   |
| SK hynix  | HFS1T9G32FEH-BA10A | 1.9 TB | 2       | 21    | 0     | 0.06   |
| Silicon   | T60                | 64 GB  | 1       | 21    | 0     | 0.06   |
| TwinMOS   | SSD                | 256 GB | 1       | 21    | 0     | 0.06   |
| Samsung   | MZMPA128HMFU-000H1 | 128 GB | 4       | 287   | 1374  | 0.06   |
| OCZ       | INTREPID 3600      | 400 GB | 1       | 21    | 0     | 0.06   |
| China     | CIE M8 M350 128... | 128 GB | 1       | 21    | 0     | 0.06   |
| GLOWAY    | STK4TS3-S7         | 4 TB   | 1       | 21    | 0     | 0.06   |
| OSCOO     | OSC mSATA          | 256 GB | 1       | 21    | 0     | 0.06   |
| AFOX      | SSD SD250-1000GB   | 1 TB   | 1       | 21    | 0     | 0.06   |
| Intel     | SSDSC2KF256H6 SATA | 256 GB | 3       | 27    | 41    | 0.06   |
| Win Me... | SWR256G-201II      | 256 GB | 1       | 21    | 0     | 0.06   |
| Team      | T253X5960G         | 960 GB | 1       | 21    | 0     | 0.06   |
| Foxline   | FLSSD512X5         | 512 GB | 3       | 21    | 0     | 0.06   |
| Intel     | SSDSC2KB240G8L ... | 240 GB | 2       | 20    | 0     | 0.06   |
| SanDisk   | WD easystore       | 240 GB | 8       | 20    | 0     | 0.06   |
| Transcend | TS32GSSD370S       | 32 GB  | 13      | 20    | 0     | 0.06   |
| China     | SSD                | 512 GB | 13      | 29    | 1     | 0.06   |
| Intel     | SSDSCKKF180G8L     | 180 GB | 1       | 20    | 0     | 0.06   |
| Transcend | TS64GMSA230S       | 64 GB  | 2       | 20    | 0     | 0.06   |
| Goldkey   | GKH84-256GB        | 256 GB | 1       | 20    | 0     | 0.06   |
| China     | SSD                | 96 GB  | 1       | 20    | 0     | 0.06   |
| KINGBANK  | KP320              | 128 GB | 1       | 20    | 0     | 0.06   |
| PNY       | CS1311 32GB SSD    | 32 GB  | 2       | 20    | 0     | 0.06   |
| Intel     | SSDSC2KR120H6      | 120 GB | 1       | 20    | 0     | 0.06   |
| Samsung   | SSD 870 EVO        | 4 TB   | 6       | 40    | 3     | 0.06   |
| Kingston  | SHFR200240G        | 240 GB | 1       | 20    | 0     | 0.06   |
| Mushkin   | MKNSSDTR240GB      | 240 GB | 2       | 20    | 0     | 0.05   |
| XUNZHE    | XUNZHE800S 120G    | 120 GB | 1       | 20    | 0     | 0.05   |
| Kingston  | HyperX Fury 3D     | 120 GB | 5       | 20    | 0     | 0.05   |
| GSemi     | GSDSM256TY2F1QGCX  | 256 GB | 1       | 20    | 0     | 0.05   |
| HEORIADY  | HX-001 E           | 128 GB | 1       | 20    | 0     | 0.05   |
| SanDisk   | SD7SN3Q-256G-1006  | 256 GB | 1       | 499   | 24    | 0.05   |
| Seagate   | XA1920LE10063      | 1.9 TB | 4       | 19    | 0     | 0.05   |
| Crucial   | CT512M550SSD4      | 512 GB | 1       | 338   | 16    | 0.05   |
| V-GeN     | V-GEN10SM21AR256HY | 256 GB | 1       | 19    | 0     | 0.05   |
| SanDisk   | SDSA5GK-016G-1006  | 16 GB  | 2       | 157   | 53    | 0.05   |
| Kingston  | SSD 128G           | 128 GB | 1       | 19    | 0     | 0.05   |
| BlueRay   | SDM8SI240A         | 240 GB | 1       | 19    | 0     | 0.05   |
| SanDisk   | SD8SB8U128G1122    | 128 GB | 1       | 19    | 0     | 0.05   |
| Gigabyte  | GP-GSTFS31256GTND  | 256 GB | 3       | 19    | 0     | 0.05   |
| Corsair   | CSSD-F80GB2-A      | 80 GB  | 1       | 18    | 0     | 0.05   |
| Transcend | TS32GMTS800        | 32 GB  | 1       | 18    | 0     | 0.05   |
| Intel     | SSDSCKJF240A5L     | 240 GB | 2       | 84    | 6     | 0.05   |
| Intel     | SSDSCKKF256H6 SATA | 256 GB | 6       | 40    | 6     | 0.05   |
| Micron    | MTFDDAK512MAY-1... | 512 GB | 2       | 476   | 528   | 0.05   |
| Goodram   | SSDPR-CL100-120-G3 | 120 GB | 7       | 18    | 0     | 0.05   |
| Corsair   | Neutron SSD        | 240 GB | 1       | 2126  | 114   | 0.05   |
| DGM       | SSD 120GB S3-120A  | 120 GB | 1       | 18    | 0     | 0.05   |
| ADATA     | SP610              | 256 GB | 1       | 18    | 0     | 0.05   |
| Hyperdisk | SDOM               | 16 GB  | 1       | 18    | 0     | 0.05   |
| UMIS      | RTITJ256VGD2MWDL   | 256 GB | 1       | 18    | 0     | 0.05   |
| Micron    | C300-MTFDDAC064MAG | 64 GB  | 1       | 54    | 2     | 0.05   |
| SanDisk   | SSD i110           | 16 GB  | 4       | 18    | 0     | 0.05   |
| Netac     | SSD                | 256 GB | 26      | 18    | 0     | 0.05   |
| BIWIN     | SSD                | 512 GB | 5       | 18    | 0     | 0.05   |
| LDLC      | SSD F6 PLUS M.2... | 960 GB | 2       | 17    | 0     | 0.05   |
| SanDisk   | Extreme Portabl... | 1 TB   | 1       | 17    | 0     | 0.05   |
| Kingston  | OM8P0S3256B-A0     | 256 GB | 5       | 17    | 0     | 0.05   |
| Yeyian    | VALK 1500          | 240 GB | 2       | 17    | 0     | 0.05   |
| Toshiba   | THNSNJ256GMCT      | 256 GB | 1       | 17    | 0     | 0.05   |
| Intel     | SSDSCKJF180A5H ... | 180 GB | 1       | 88    | 4     | 0.05   |
| Dell      | WR202KD032G E70... | 32 GB  | 3       | 17    | 0     | 0.05   |
| Team      | TM8PS5256G         | 256 GB | 1       | 17    | 0     | 0.05   |
| China     | 60GB SSD           | 64 GB  | 1       | 17    | 0     | 0.05   |
| China     | RTMMB256VBV4KFY    | 256 GB | 1       | 17    | 0     | 0.05   |
| Lite-On   | IT L8T-256L9G-HP   | 256 GB | 1       | 17    | 0     | 0.05   |
| Lite-On   | CV1-8B256-HP       | 256 GB | 2       | 17    | 0     | 0.05   |
| Kingrich  | 64GB K9 SATA3 SSD  | 64 GB  | 2       | 17    | 0     | 0.05   |
| China     | NGFF 2280 1TB SSD  | 1 TB   | 1       | 17    | 0     | 0.05   |
| AMD       | R3S60GBSM          | 64 GB  | 2       | 17    | 0     | 0.05   |
| Intel     | SSDSC2KB019T8      | 1.9 TB | 4       | 16    | 0     | 0.05   |
| Lite-On   | LMH-128V2M-11 M... | 128 GB | 2       | 16    | 0     | 0.05   |
| KingFast  | SSD                | 16 GB  | 1       | 16    | 0     | 0.05   |
| LDNDISK   | SSD                | 240 GB | 1       | 16    | 0     | 0.05   |
| Kingston  | SKC6002048G        | 2 TB   | 1       | 16    | 0     | 0.05   |
| Seagate   | BarraCuda 120 S... | 250 GB | 10      | 16    | 0     | 0.05   |
| Intel     | SSDSCKKF512H6 SATA | 512 GB | 1       | 249   | 14    | 0.05   |
| Transcend | TS256GMTS830S      | 256 GB | 1       | 16    | 0     | 0.05   |
| AEGO      | SSD                | 240 GB | 3       | 16    | 0     | 0.04   |
| Intel     | SSDMCEAW080A4      | 80 GB  | 1       | 16    | 0     | 0.04   |
| XUM       | HX240GSSDSATA3     | 240 GB | 1       | 16    | 0     | 0.04   |
| OCZ       | VERTEX3            | 256 GB | 1       | 533   | 32    | 0.04   |
| Goodram   | SSDPR-CX400-256-G2 | 256 GB | 12      | 16    | 0     | 0.04   |
| Kingston  | SKC300S37A180G     | 180 GB | 3       | 320   | 745   | 0.04   |
| BIOSTAR   | S100-256GB         | 256 GB | 1       | 16    | 0     | 0.04   |
| Mushkin   | MKNSSDS21TB        | 1 TB   | 8       | 20    | 39    | 0.04   |
| V-GeN     | V-GEN05SM21AR12... | 128 GB | 1       | 15    | 0     | 0.04   |
| FASTDISK  | FASTDISK120G       | 120 GB | 1       | 15    | 0     | 0.04   |
| AFOX      | SSD                | 500 GB | 1       | 15    | 0     | 0.04   |
| SanDisk   | SD8SNAT128G1122    | 128 GB | 1       | 15    | 0     | 0.04   |
| China     | MLC 256G           | 256 GB | 1       | 15    | 0     | 0.04   |
| ADATA     | SU750              | 256 GB | 29      | 15    | 0     | 0.04   |
| Mushkin   | MKNSSDE3480GB      | 480 GB | 3       | 15    | 0     | 0.04   |
| ADATA     | SP900NS34          | 128 GB | 2       | 230   | 508   | 0.04   |
| Teclast   | 256GB NS550-2242   | 256 GB | 11      | 15    | 0     | 0.04   |
| SanDisk   | SD8SBAT128G1122    | 128 GB | 18      | 15    | 0     | 0.04   |
| FORESEE   | 240GB SSD          | 240 GB | 1       | 15    | 0     | 0.04   |
| Transcend | TS64GSSD25S-M      | 64 GB  | 2       | 15    | 0     | 0.04   |
| e2e4      | SSD                | 120 GB | 3       | 15    | 0     | 0.04   |
| Lite-On   | CV1-SB128          | 128 GB | 1       | 15    | 0     | 0.04   |
| Apple     | SSD TS0128F        | 121 GB | 1       | 15    | 0     | 0.04   |
| Leven     | JAJS500M120C-1     | 120 GB | 1       | 15    | 0     | 0.04   |
| Micron    | 1300_MTFDDAK256TDL | 256 GB | 2       | 14    | 0     | 0.04   |
| Apacer    | 32GB SATA Flash... | 32 GB  | 6       | 52    | 6     | 0.04   |
| FASTDISK  | SSD 60G            | 64 GB  | 1       | 14    | 0     | 0.04   |
| PNY       | SSD2SC240G5LC70... | 240 GB | 1       | 14    | 0     | 0.04   |
| Samsung   | MZNLN128HAHQ-000L2 | 128 GB | 3       | 14    | 0     | 0.04   |
| Lexar     | SSD                | 120 GB | 1       | 14    | 0     | 0.04   |
| Intenso   | SSD                | 240 GB | 3       | 14    | 0     | 0.04   |
| Lenovo    | SSD SL700 M.2 128G | 128 GB | 1       | 14    | 0     | 0.04   |
| Zheino    | CHN 25SATA01M 030  | 32 GB  | 2       | 14    | 0     | 0.04   |
| RevuAhn   | 900G Gaming        | 256 GB | 1       | 14    | 0     | 0.04   |
| Intel     | SSDSC2KG480G8      | 480 GB | 3       | 14    | 0     | 0.04   |
| Seagate   | ST480FP0021        | 480 GB | 1       | 14    | 0     | 0.04   |
| Crucial   | CT2000MX500SSD1N   | 2 TB   | 1       | 14    | 0     | 0.04   |
| Micron    | 1300 SATA          | 512 GB | 1       | 14    | 0     | 0.04   |
| Faspeed   | K7N-256G           | 256 GB | 1       | 14    | 0     | 0.04   |
| Lite-On   | CV1-8B128          | 128 GB | 14      | 14    | 0     | 0.04   |
| WDC       | WDBNCE5000PNC-WRSN | 500 GB | 1       | 14    | 0     | 0.04   |
| Micron    | MTFDDAK240TCB      | 240 GB | 1       | 14    | 0     | 0.04   |
| Kingston  | RBUSNS8180DS3256GH | 256 GB | 1       | 41    | 2     | 0.04   |
| SMI       | SSD DISK           | 128 GB | 1       | 13    | 0     | 0.04   |
| ADLINK    | SSO256GTLC9-SB3-4L | 256 GB | 1       | 13    | 0     | 0.04   |
| SanDisk   | SD9SB8W256G1102    | 256 GB | 3       | 13    | 0     | 0.04   |
| Pioneer   | APS-SL3N-120       | 120 GB | 1       | 13    | 0     | 0.04   |
| Smartbuy  | m.2 S11-2280       | 256 GB | 1       | 13    | 0     | 0.04   |
| OCZ       | VECTOR180          | 960 GB | 1       | 13    | 0     | 0.04   |
| Lite-On   | LJH-256V2G-11 M... | 256 GB | 1       | 13    | 0     | 0.04   |
| BHT       | WR202I0064G E70... | 64 GB  | 6       | 13    | 0     | 0.04   |
| Seagate   | FireCuda 120 SS... | 500 GB | 1       | 13    | 0     | 0.04   |
| Plextor   | PX-G256M6e         | 256 GB | 2       | 13    | 0     | 0.04   |
| Plextor   | PX-128M6S+         | 128 GB | 1       | 13    | 0     | 0.04   |
| Transcend | TS128GMTS600       | 128 GB | 1       | 13    | 0     | 0.04   |
| Transcend | TS64GMTS800        | 64 GB  | 2       | 13    | 0     | 0.04   |
| XrayDisk  | SSD                | 256 GB | 7       | 13    | 0     | 0.04   |
| Intel     | SSDSC2KF256H6L     | 256 GB | 8       | 67    | 28    | 0.04   |
| Intel     | SSDSCKKW128G8      | 128 GB | 3       | 13    | 0     | 0.04   |
| Intel     | SSDSA1M160G2HP     | 160 GB | 8       | 100   | 20    | 0.04   |
| e2e4      | SSD                | 64 GB  | 1       | 13    | 0     | 0.04   |
| KingSpec  | P4-240             | 240 GB | 12      | 27    | 19    | 0.04   |
| ADATA     | SU760              | 256 GB | 1       | 12    | 0     | 0.04   |
| Phison    | S11-256G-PHISON... | 256 GB | 1       | 12    | 0     | 0.04   |
| SanDisk   | SD8SNAT-256G-1006  | 256 GB | 8       | 12    | 0     | 0.04   |
| ShanDi... | SSD                | 256 GB | 2       | 12    | 0     | 0.03   |
| Varro     | BULLDOZER-120GB    | 120 GB | 1       | 12    | 0     | 0.03   |
| KingSpec  | P3-256             | 256 GB | 12      | 40    | 1     | 0.03   |
| ShanDi... | SSD                | 128 GB | 2       | 12    | 0     | 0.03   |
| Intel     | SSDSCKKW010X6      | 1 TB   | 3       | 27    | 194   | 0.03   |
| Lite-On   | LMH-128V2M         | 128 GB | 1       | 37    | 2     | 0.03   |
| Phison    | SSO256GTLC9-SBC-2  | 256 GB | 1       | 12    | 0     | 0.03   |
| Super ... | FTM28N325H         | 128 GB | 1       | 12    | 0     | 0.03   |
| KINGBANK  | KP330              | 120 GB | 3       | 12    | 0     | 0.03   |
| Lite-On   | CV3-SD128          | 128 GB | 1       | 12    | 0     | 0.03   |
| ADATA     | SU750              | 512 GB | 4       | 12    | 0     | 0.03   |
| Silico... | ULTIMATE CF CARD   | 16 GB  | 1       | 12    | 0     | 0.03   |
| Microtech | SSD 60G            | 64 GB  | 1       | 12    | 0     | 0.03   |
| Wicgtyp   | M900-128           | 128 GB | 1       | 12    | 0     | 0.03   |
| China     | SSD 128G           | 128 GB | 4       | 12    | 0     | 0.03   |
| SanDisk   | SD6SF1M256G1022I   | 256 GB | 1       | 12    | 0     | 0.03   |
| Transcend | TS128GSSD360S      | 128 GB | 8       | 12    | 0     | 0.03   |
| Maximus   | SSD                | 128 GB | 3       | 12    | 0     | 0.03   |
| OWC       | 1.0TB Mercury E... | 1 TB   | 2       | 12    | 0     | 0.03   |
| Kingrich  | KM9 60GB MSATA3... | 64 GB  | 1       | 12    | 0     | 0.03   |
| SanDisk   | SD9SN8W512G1122    | 512 GB | 1       | 12    | 0     | 0.03   |
| MIXZA     | SSD                | 120 GB | 1       | 11    | 0     | 0.03   |
| KIOXIA... | SATA SSD           | 240 GB | 10      | 11    | 0     | 0.03   |
| Advantech | SQF-SHMM2-8G-S9C   | 8 GB   | 2       | 11    | 0     | 0.03   |
| China     | SSD                | 180 GB | 1       | 11    | 0     | 0.03   |
| XrayDisk  | SSD                | 480 GB | 2       | 11    | 0     | 0.03   |
| Samsung   | MZ7LN128HAHQ-00000 | 128 GB | 1       | 11    | 0     | 0.03   |
| PNY       | SSD2SC120G1SA75... | 120 GB | 1       | 11    | 0     | 0.03   |
| Micron    | MTFDDAK256MAY-1... | 256 GB | 6       | 244   | 73    | 0.03   |
| TEXTORM   | B5                 | 120 GB | 1       | 11    | 0     | 0.03   |
| Netac     | SSD 120G           | 120 GB | 2       | 11    | 0     | 0.03   |
| Transcend | TSKU60SSD420       | 64 GB  | 1       | 11    | 0     | 0.03   |
| Crucial   | V4-CT128V4SSD2     | 128 GB | 1       | 11    | 0     | 0.03   |
| Intenso   | TBYTE-SSD          | 128 GB | 1       | 11    | 0     | 0.03   |
| Faspeed   | M3-360G            | 360 GB | 1       | 11    | 0     | 0.03   |
| Vaseky    | V900-128GB         | 120 GB | 1       | 11    | 0     | 0.03   |
| Micron    | M600_MTFDDAV512MBF | 512 GB | 1       | 11    | 0     | 0.03   |
| China     | MSATA SSD          | 256 GB | 1       | 11    | 0     | 0.03   |
| Transcend | TS128GMTS800I      | 128 GB | 1       | 11    | 0     | 0.03   |
| SUNEAST   | SSD SE800          | 256 GB | 1       | 11    | 0     | 0.03   |
| China     | SSDG2-256G         | 256 GB | 1       | 10    | 0     | 0.03   |
| ADATA     | SSD S511           | 240 GB | 1       | 10    | 0     | 0.03   |
| Transcend | TS32GSSD25S-M      | 32 GB  | 1       | 10    | 0     | 0.03   |
| China     | EK V100 120G       | 120 GB | 1       | 10    | 0     | 0.03   |
| Golden... | GDSA25-120MS       | 120 GB | 1       | 10    | 0     | 0.03   |
| SanDisk   | SD8SNAT256G1122    | 256 GB | 3       | 10    | 0     | 0.03   |
| Micron    | 1300 SATA          | 256 GB | 2       | 10    | 0     | 0.03   |
| ADATA     | SX300              | 128 GB | 1       | 10    | 0     | 0.03   |
| China     | 1TB PCS 2.5" SSD   | 1 TB   | 1       | 10    | 0     | 0.03   |
| Teclast   | 256GB A850         | 256 GB | 1       | 10    | 0     | 0.03   |
| Colorful  | SL300              | 128 GB | 2       | 33    | 505   | 0.03   |
| XrayDisk  | SSD                | 240 GB | 4       | 10    | 0     | 0.03   |
| KingSpec  | ACSC2M256S25       | 256 GB | 1       | 10    | 0     | 0.03   |
| SanDisk   | SD8SNAT256G1002    | 256 GB | 6       | 12    | 1     | 0.03   |
| KingSpec  | P4-120             | 120 GB | 4       | 10    | 0     | 0.03   |
| Goodram   | SSDPR-S400U-120-42 | 120 GB | 2       | 10    | 0     | 0.03   |
| OCZ       | REVODRIVE          | 25 GB  | 2       | 1968  | 208   | 0.03   |
| SK hynix  | SH920 mSATA        | 256 GB | 3       | 530   | 252   | 0.03   |
| Seagate   | BarraCuda Q1 SS... | 960 GB | 2       | 9     | 0     | 0.03   |
| SK hynix  | SH920 mSATA        | 128 GB | 3       | 149   | 262   | 0.03   |
| Seagate   | IronWolf ZA500N... | 500 GB | 1       | 9     | 0     | 0.03   |
| SPCC      | SSD162             | 240 GB | 1       | 203   | 20    | 0.03   |
| Crucial   | CT480M500SSD3      | 480 GB | 3       | 1032  | 993   | 0.03   |
| Zozt      | G3000 240          | 240 GB | 2       | 9     | 0     | 0.03   |
| Ramsta    | SSD R800           | 120 GB | 1       | 9     | 0     | 0.03   |
| Zozt      | G3000 480          | 480 GB | 1       | 9     | 0     | 0.03   |
| Lite-On   | CV3-SD512          | 512 GB | 1       | 9     | 0     | 0.03   |
| KingSpec  | P3-64              | 64 GB  | 2       | 9     | 0     | 0.03   |
| FORESEE   | 512GB SSD          | 512 GB | 3       | 9     | 0     | 0.03   |
| Faspeed   | H5-120G PLUS       | 120 GB | 1       | 9     | 0     | 0.03   |
| Netac     | S535N8-256GYN      | 256 GB | 6       | 9     | 0     | 0.03   |
| FORESEE   | S50AF512GB         | 512 GB | 6       | 9     | 0     | 0.03   |
| Microtech | SSD480M2S80        | 480 GB | 1       | 9     | 0     | 0.03   |
| Transcend | TS512GSSD720       | 512 GB | 1       | 1638  | 176   | 0.03   |
| ADATA     | SU900              | 128 GB | 1       | 9     | 0     | 0.02   |
| Kingston  | v300 240G          | 240 GB | 1       | 9     | 0     | 0.02   |
| Yeyian    | VALK 1000          | 120 GB | 2       | 9     | 0     | 0.02   |
| SanDisk   | iSSD P4            | 16 GB  | 2       | 222   | 24    | 0.02   |
| Teclast   | 128GB MS550        | 128 GB | 1       | 8     | 0     | 0.02   |
| S3+       | S3SSDC240XEU       | 240 GB | 1       | 415   | 46    | 0.02   |
| KingDian  | N400 60G           | 64 GB  | 1       | 8     | 0     | 0.02   |
| SanDisk   | SD7SN6S-128G-1006  | 128 GB | 1       | 8     | 0     | 0.02   |
| Patriot   | P210               | 512 GB | 3       | 8     | 0     | 0.02   |
| BIOSTAR   | S160-256GB         | 256 GB | 1       | 8     | 0     | 0.02   |
| Getrich   | 120G SSD           | 120 GB | 1       | 8     | 0     | 0.02   |
| Intenso   | JAJM600M256C       | 256 GB | 1       | 8     | 0     | 0.02   |
| KingSpec  | ACSC4M128MSA       | 128 GB | 1       | 8     | 0     | 0.02   |
| Mushkin   | MKNSSDRE2TB        | 2 TB   | 1       | 8     | 0     | 0.02   |
| SanDisk   | SD8SN8U1T002000    | 1 TB   | 1       | 8     | 0     | 0.02   |
| PNY       | SSD2SC240G1CS17... | 240 GB | 1       | 8     | 0     | 0.02   |
| Intel     | SSDSCKKW120H6      | 120 GB | 1       | 76    | 8     | 0.02   |
| Londisk   | SSD                | 480 GB | 1       | 8     | 0     | 0.02   |
| China     | ESA3ASA2PSTBT120GB | 120 GB | 1       | 243   | 28    | 0.02   |
| Lite-On   | LSS-24L6G          | 24 GB  | 4       | 9     | 254   | 0.02   |
| Kingston  | SKC600MS512G       | 512 GB | 2       | 8     | 0     | 0.02   |
| Kingspeed | SSD                | 240 GB | 1       | 8     | 0     | 0.02   |
| Super ... | FTM51N325H         | 512 GB | 2       | 8     | 0     | 0.02   |
| Drevo     | X1                 | 120 GB | 2       | 144   | 1016  | 0.02   |
| SanDisk   | SDEZS25-240G-Z01   | 240 GB | 1       | 8     | 0     | 0.02   |
| Netac     | SSD                | 128 GB | 11      | 11    | 1     | 0.02   |
| Intel     | SSDSCKKW240H6      | 240 GB | 4       | 15    | 10    | 0.02   |
| SanDisk   | SD8SNAT128G1002    | 128 GB | 7       | 8     | 0     | 0.02   |
| Plextor   | PX-512M6S          | 512 GB | 1       | 8     | 0     | 0.02   |
| Netac     | SATA3 120GB SSD    | 120 GB | 1       | 8     | 0     | 0.02   |
| Mushkin   | MKNSSDRW1TB        | 1 TB   | 1       | 8     | 0     | 0.02   |
| HP        | SSD S600           | 240 GB | 4       | 14    | 1     | 0.02   |
| Samsung   | MZ7LH128HBHQ-000L1 | 128 GB | 2       | 7     | 0     | 0.02   |
| SanDisk   | SD8SMAT-128G-1006  | 128 GB | 2       | 7     | 0     | 0.02   |
| FASTDISK  | SSD 120G           | 120 GB | 1       | 7     | 0     | 0.02   |
| ADATA     | IM2S3138E-256GM-B  | 256 GB | 1       | 513   | 65    | 0.02   |
| Intel     | SSDSC2BF180A5H SED | 180 GB | 3       | 290   | 47    | 0.02   |
| Intenso   | SSD_2.5''_TLC_5... | 512 GB | 1       | 7     | 0     | 0.02   |
| China     | SSD60G             | 64 GB  | 2       | 7     | 0     | 0.02   |
| WDC       | WDS250G2B0B        | 250 GB | 5       | 7     | 0     | 0.02   |
| SanDisk   | SD8SBAT256G1002    | 256 GB | 1       | 7     | 0     | 0.02   |
| Zheino    | CHN 25SATA01M 060  | 64 GB  | 1       | 7     | 0     | 0.02   |
| WDC       | WDS100T1R0B-68A4Z0 | 1 TB   | 1       | 7     | 0     | 0.02   |
| Phison    | S11-128G-PHISON... | 128 GB | 3       | 7     | 0     | 0.02   |
| Foxline   | FLSSD512X5SE       | 512 GB | 1       | 7     | 0     | 0.02   |
| KingSpec  | ACSC2M128mSA       | 128 GB | 1       | 7     | 0     | 0.02   |
| ADATA     | SU650NS38          | 120 GB | 4       | 7     | 0     | 0.02   |
| Patriot   | Morebeck-N100      | 256 GB | 1       | 7     | 0     | 0.02   |
| Phison    | S11-512G-PHISON... | 512 GB | 2       | 7     | 0     | 0.02   |
| China     | SATA3 480GB SSD    | 480 GB | 5       | 13    | 56    | 0.02   |
| Toshiba   | THNSNS128GMCP      | 128 GB | 1       | 7     | 0     | 0.02   |
| Zheino    | CHN25SATAS1 032    | 32 GB  | 4       | 7     | 0     | 0.02   |
| SanDisk   | SD9SN8W128G1122    | 128 GB | 1       | 7     | 0     | 0.02   |
| ADATA     | SX300              | 64 GB  | 2       | 23    | 510   | 0.02   |
| FASTDISK  | SSD 30G            | 32 GB  | 1       | 7     | 0     | 0.02   |
| Dell      | WR202KD032G E70... | 32 GB  | 2       | 6     | 0     | 0.02   |
| tigo      | SSD                | 128 GB | 1       | 6     | 0     | 0.02   |
| MAXIMUS   | SSD                | 128 GB | 1       | 6     | 0     | 0.02   |
| China     | SSD 256G           | 256 GB | 2       | 6     | 0     | 0.02   |
| Kingston  | SV300S37A 120G     | 120 GB | 1       | 6     | 0     | 0.02   |
| ORICO     | M200               | 256 GB | 1       | 6     | 0     | 0.02   |
| Phison    | SSBP064GTB3C0-S11  | 64 GB  | 1       | 6     | 0     | 0.02   |
| Samsung   | MZ7LH1T9HMLT-00005 | 1.9 TB | 1       | 6     | 0     | 0.02   |
| Solid     | SSD0256S00         | 256 GB | 2       | 13    | 2     | 0.02   |
| Kingston  | OM8P0S3512F-00     | 512 GB | 1       | 6     | 0     | 0.02   |
| Patriot   | Ignite             | 240 GB | 1       | 6     | 0     | 0.02   |
| Kingston  | RBUSC180S37128GJ   | 128 GB | 1       | 6     | 0     | 0.02   |
| Kingston  | SA400S37 240G      | 240 GB | 1       | 6     | 0     | 0.02   |
| Samsung   | SSD PM871b 2.5 7mm | 128 GB | 1       | 6     | 0     | 0.02   |
| Teclast   | BD256GB SHCA-2280  | 256 GB | 2       | 6     | 0     | 0.02   |
| SanDisk   | SD8SNAT-128G-1006  | 128 GB | 6       | 6     | 0     | 0.02   |
| Intenso   | SSD128GBCSU2-E7    | 128 GB | 1       | 6     | 0     | 0.02   |
| Lite-On   | CV5-8Q512-HP       | 512 GB | 1       | 6     | 0     | 0.02   |
| Kross ... | KE-SSDIS96G        | 960 GB | 1       | 6     | 0     | 0.02   |
| Intel     | SSDSC2KF512G8 SATA | 512 GB | 1       | 6     | 0     | 0.02   |
| GS Nan... | GSPMA512M16STF     | 512 GB | 1       | 6     | 0     | 0.02   |
| Kimtigo   | SSD                | 128 GB | 2       | 6     | 0     | 0.02   |
| KingSpec  | KSQ120             | 120 GB | 1       | 6     | 0     | 0.02   |
| QNIX      | SSD                | 120 GB | 1       | 6     | 0     | 0.02   |
| GeIL      | Zenith A3-PRO      | 240 GB | 1       | 6     | 0     | 0.02   |
| Intenso   | M.2 2242-128GB SSD | 128 GB | 1       | 6     | 0     | 0.02   |
| SK hynix  | HFS128G39MNC-2300A | 128 GB | 2       | 242   | 345   | 0.02   |
| GeIL      | Zenith A3          | 120 GB | 1       | 6     | 0     | 0.02   |
| SPCC      | 2.5" SSD           | 512 GB | 1       | 6     | 0     | 0.02   |
| Samsung   | MZ7LN128HCHP-000H1 | 128 GB | 1       | 6     | 0     | 0.02   |
| Intel     | SSDSCKGW180A4      | 180 GB | 1       | 286   | 47    | 0.02   |
| Plextor   | PX-128M6MV         | 128 GB | 2       | 5     | 0     | 0.02   |
| INDMEM    | SSD mSATA          | 128 GB | 1       | 5     | 0     | 0.02   |
| Team      | T253X2256G         | 256 GB | 2       | 5     | 0     | 0.02   |
| BRAVEE... | SSD                | 120 GB | 1       | 5     | 0     | 0.02   |
| Kingch... | SSD                | 120 GB | 1       | 5     | 0     | 0.02   |
| V-GeN     | V-GEN10SM19AR12... | 120 GB | 1       | 5     | 0     | 0.02   |
| QIANGHE   | SSD                | 240 GB | 1       | 73    | 12    | 0.02   |
| Dell      | WR202KD128G E70... | 128 GB | 1       | 5     | 0     | 0.02   |
| Intenso   | SSD0128S00         | 128 GB | 1       | 5     | 0     | 0.02   |
| Intenso   | SSD                | 480 GB | 2       | 5     | 0     | 0.02   |
| KingSpec  | T-60               | 64 GB  | 4       | 12    | 88    | 0.02   |
| Intel     | SSDSA1M080G2LE     | 80 GB  | 3       | 63    | 14    | 0.02   |
| Kingston  | KC600              | 128 GB | 1       | 5     | 0     | 0.01   |
| Lite-On   | L8T-256L9G-11 M... | 256 GB | 1       | 5     | 0     | 0.01   |
| ADATA     | SX850              | 256 GB | 2       | 171   | 40    | 0.01   |
| ShiJi     | SSD                | 128 GB | 1       | 5     | 0     | 0.01   |
| TREKSTOR  | TREKSTORSSD512GB   | 500 GB | 1       | 5     | 0     | 0.01   |
| Faspeed   | H5-500G            | 500 GB | 1       | 40    | 7     | 0.01   |
| OCZ       | AGITLITY3          | 480 GB | 1       | 5234  | 1028  | 0.01   |
| China     | M.2 2280-1TB SSD   | 1 TB   | 1       | 5     | 0     | 0.01   |
| China     | M.2 SSD            | 128 GB | 1       | 5     | 0     | 0.01   |
| MaxDig... | MD500 120G         | 120 GB | 1       | 5     | 0     | 0.01   |
| Teclast   | 512GB A850         | 512 GB | 1       | 5     | 0     | 0.01   |
| Mushkin   | MKNSSDCG480GB      | 480 GB | 2       | 116   | 508   | 0.01   |
| Kingch... | SSD                | 256 GB | 1       | 4     | 0     | 0.01   |
| Leven     | JS500120C          | 120 GB | 1       | 4     | 0     | 0.01   |
| Smartbuy  | m.2 S11-2280       | 128 GB | 1       | 4     | 0     | 0.01   |
| BHT       | WR202HH032G E70... | 32 GB  | 1       | 4     | 0     | 0.01   |
| Intenso   | 512GB QLC SATA SSD | 512 GB | 2       | 4     | 0     | 0.01   |
| TAMMUZ    | SSD                | 120 GB | 1       | 4     | 0     | 0.01   |
| GLOWAY    | VAL32GS3-mSATA     | 32 GB  | 1       | 4     | 0     | 0.01   |
| KingSpec  | ACSC2M128S25       | 128 GB | 1       | 4     | 0     | 0.01   |
| China     | SATA SSD           | 32 GB  | 1       | 4     | 0     | 0.01   |
| SanDisk   | SD8TN8U-256G-1006  | 256 GB | 2       | 123   | 515   | 0.01   |
| Corsair   | Neutron XT SSD     | 240 GB | 2       | 1342  | 286   | 0.01   |
| Goodram   | 1TB PCS 2.5" SSD   | 1 TB   | 1       | 4     | 0     | 0.01   |
| SanDisk   | Z400s 2.5 7MM      | 128 GB | 2       | 4     | 0     | 0.01   |
| PNY       | SSD2SC480G1CS17... | 480 GB | 1       | 4     | 0     | 0.01   |
| Samsung   | MZ7LN256HAJQ-00007 | 256 GB | 1       | 4     | 0     | 0.01   |
| Lite-On   | LCT-128M3S         | 128 GB | 3       | 100   | 687   | 0.01   |
| Intel     | SSDSCKKF180H6L     | 180 GB | 1       | 79    | 17    | 0.01   |
| Team      | TM4PS5128G         | 128 GB | 1       | 8     | 1     | 0.01   |
| S3+       | S3SSDC128          | 128 GB | 1       | 4     | 0     | 0.01   |
| Maximus   | SSD 256G           | 256 GB | 1       | 4     | 0     | 0.01   |
| PNY       | SSD2SC240G1SA75... | 240 GB | 2       | 7     | 44    | 0.01   |
| China     | 1TB SSD            | 1 TB   | 1       | 4     | 0     | 0.01   |
| Kingston  | RBUSMS180S364GJ    | 64 GB  | 1       | 4     | 0     | 0.01   |
| Kingston  | SA400S37           | 240 GB | 1       | 4     | 0     | 0.01   |
| Intenso   | AEROFARA M.2       | 256 GB | 1       | 4     | 0     | 0.01   |
| 2-Power   | SSD2041A           | 120 GB | 1       | 4     | 0     | 0.01   |
| Samsung   | SSD PM800 mSATA    | 64 GB  | 1       | 4     | 0     | 0.01   |
| SanDisk   | SD7UB3Q256G1001    | 256 GB | 5       | 419   | 100   | 0.01   |
| Lite-On   | IT SCS-256L9S      | 256 GB | 1       | 24    | 5     | 0.01   |
| Crucial   | CT256M550SSD4      | 256 GB | 1       | 342   | 82    | 0.01   |
| Mushkin   | MKNSSDTR240GB-LT   | 240 GB | 1       | 4     | 0     | 0.01   |
| PHINOCOM  | SSD                | 120 GB | 1       | 4     | 0     | 0.01   |
| INNOVA... | SSD                | 1 TB   | 2       | 4     | 0     | 0.01   |
| KODAK     | SSD X100           | 120 GB | 1       | 4     | 0     | 0.01   |
| Intel     | SSDMAEMC080G2H     | 80 GB  | 1       | 4     | 0     | 0.01   |
| Samsung   | PM881 SATA         | 256 GB | 2       | 4     | 0     | 0.01   |
| Corsair   | Neutron GTX SSD    | 128 GB | 1       | 1173  | 291   | 0.01   |
| BIWIN     | G2242              | 64 GB  | 2       | 4     | 0     | 0.01   |
| GeIL      | ZENITH-A3 120G     | 120 GB | 1       | 3     | 0     | 0.01   |
| Mushkin   | MKNSSDTR512GB-3DL  | 512 GB | 1       | 3     | 0     | 0.01   |
| Zheino    | CHN-25SATAA3-360   | 360 GB | 1       | 87    | 21    | 0.01   |
| China     | Mit-SSD128A        | 128 GB | 1       | 3     | 0     | 0.01   |
| Intel     | SSDSC2KF010T8      | 1 TB   | 1       | 3     | 0     | 0.01   |
| KingSpec  | MT-256             | 256 GB | 8       | 40    | 12    | 0.01   |
| Fujitsu   | F500S              | 1 TB   | 1       | 3     | 0     | 0.01   |
| Lite-On   | LSS-16L6G          | 16 GB  | 1       | 3     | 0     | 0.01   |
| Micron    | MTFDDAK960TDS-1... | 960 GB | 6       | 3     | 0     | 0.01   |
| SanDisk   | SATAIII            | 16 GB  | 1       | 3     | 0     | 0.01   |
| tigo      | SSD                | 64 GB  | 1       | 3     | 0     | 0.01   |
| KingDian  | S200               | 240 GB | 1       | 3     | 0     | 0.01   |
| ADATA     | IM2S3334-256GD     | 256 GB | 1       | 7     | 1     | 0.01   |
| Lite-On   | LGH-512V2G-11 M... | 512 GB | 1       | 11    | 2     | 0.01   |
| Lite-On   | LSS-16L6G-HP       | 16 GB  | 2       | 66    | 638   | 0.01   |
| HPE       | MK000960GWJPP      | 960 GB | 1       | 3     | 0     | 0.01   |
| Pacifi... | PSM-128GBSATA3S... | 128 GB | 1       | 3     | 0     | 0.01   |
| OWC       | Aura SSD           | 120 GB | 1       | 3     | 0     | 0.01   |
| SanDisk   | SD7SB2Q512G1001    | 512 GB | 3       | 356   | 100   | 0.01   |
| China     | SATA3 120GB SSD    | 120 GB | 3       | 3     | 0     | 0.01   |
| Lite-On   | IT L8H-64V2G       | 64 GB  | 1       | 3     | 0     | 0.01   |
| Samsung   | MZNLN256HAJQ-00007 | 256 GB | 1       | 3     | 0     | 0.01   |
| OCZ       | REVODRIVE X2       | 64 GB  | 4       | 1204  | 516   | 0.01   |
| SPCC      | SSDB27             | 32 GB  | 1       | 23    | 6     | 0.01   |
| ShineDisk | M667 128G          | 120 GB | 1       | 3     | 0     | 0.01   |
| Timetec   | 35TTM8SSATA-512G   | 512 GB | 1       | 3     | 0     | 0.01   |
| i-Flas... | K8                 | 64 GB  | 1       | 3     | 0     | 0.01   |
| walram    | SSD 128G           | 128 GB | 1       | 3     | 0     | 0.01   |
| Iod       | MST1001-512        | 512 GB | 2       | 3     | 0     | 0.01   |
| China     | SSD-512G           | 512 GB | 1       | 3     | 0     | 0.01   |
| TurXun    | S500               | 256 GB | 1       | 3     | 0     | 0.01   |
| China     | DEPOSM3DT-480      | 480 GB | 1       | 3     | 0     | 0.01   |
| Corsair   | CSSD-V128GB2       | 128 GB | 1       | 3     | 0     | 0.01   |
| China     | NGFF 2280 128GB... | 128 GB | 1       | 3     | 0     | 0.01   |
| Netac     | M.2 2280-128GB SSD | 128 GB | 1       | 3     | 0     | 0.01   |
| Smart     | SSD                | 240 GB | 1       | 3     | 0     | 0.01   |
| Star D... | SATA SSD           | 240 GB | 1       | 3     | 0     | 0.01   |
| Pichau    | Gaming PG256X      | 256 GB | 1       | 3     | 0     | 0.01   |
| SK hynix  | HFS128G3AMNB-2200A | 128 GB | 4       | 539   | 620   | 0.01   |
| Lite-On   | LMS-32L6M-HP       | 32 GB  | 2       | 3     | 0     | 0.01   |
| KLEVV     | NEO N610 SSD       | 512 GB | 1       | 2     | 0     | 0.01   |
| Colorful  | SL300              | 120 GB | 2       | 65    | 19    | 0.01   |
| OCZ       | AGILITY3           | 480 GB | 1       | 842   | 286   | 0.01   |
| Samsung   | SSD PM810 mSATA    | 128 GB | 1       | 137   | 46    | 0.01   |
| Goodram   | IR_SSDPR_S25A_120  | 120 GB | 1       | 2     | 0     | 0.01   |
| Lite-On   | IT LST-32S9G-HP    | 32 GB  | 1       | 2     | 0     | 0.01   |
| Kingston  | RBUSC180S37256GJ   | 256 GB | 1       | 2     | 0     | 0.01   |
| SanDisk   | SD8SBAT064G1122    | 64 GB  | 1       | 2     | 0     | 0.01   |
| Crucial   | CT250MX200SSD6     | 250 GB | 1       | 2     | 0     | 0.01   |
| Vaseky    | V820-512G          | 512 GB | 1       | 2     | 0     | 0.01   |
| Intel     | SSDSCKKF180H6H     | 180 GB | 4       | 37    | 10    | 0.01   |
| SK hynix  | SH920 2.5 7MM      | 512 GB | 7       | 458   | 262   | 0.01   |
| Samsung   | MZ7LH3T8HMLT-00005 | 3.8 TB | 2       | 2     | 0     | 0.01   |
| Intel     | SSDSA2M160G2HP     | 160 GB | 2       | 251   | 65    | 0.01   |
| Fordisk   | SATA SSD           | 120 GB | 1       | 2     | 0     | 0.01   |
| Kingch... | SSD                | 64 GB  | 1       | 2     | 0     | 0.01   |
| LDLC      | SSD                | 64 GB  | 1       | 2     | 0     | 0.01   |
| Patriot   | Wildfire           | 120 GB | 1       | 2712  | 1022  | 0.01   |
| China     | M.2 2280 SATA SSD  | 128 GB | 1       | 2     | 0     | 0.01   |
| Hikvision | HS-SSD-C260 512G   | 512 GB | 1       | 2     | 0     | 0.01   |
| KODAK     | X150               | 480 GB | 1       | 2     | 0     | 0.01   |
| Intel     | SSDSC2KB480G7      | 480 GB | 3       | 2     | 0     | 0.01   |
| Verbatim  | Vi560 SATA III ... | 256 GB | 1       | 2     | 0     | 0.01   |
| Golden... | 60Gb               | 64 GB  | 1       | 2     | 0     | 0.01   |
| Gigastone | SS6200-256GB       | 256 GB | 1       | 2     | 0     | 0.01   |
| KingDian  | N400               | 120 GB | 1       | 2     | 0     | 0.01   |
| SOLIDATA  | SSD                | 120 GB | 1       | 2420  | 1019  | 0.01   |
| Micron    | 1300_MTFDDAK512TDL | 512 GB | 1       | 2     | 0     | 0.01   |
| SanDisk   | SD8SNAT-128G-1009  | 128 GB | 1       | 2     | 0     | 0.01   |
| SanDisk   | SSD i110           | 24 GB  | 1       | 2     | 0     | 0.01   |
| Toshiba   | KSG60ZSE256G SATA  | 256 GB | 1       | 229   | 100   | 0.01   |
| Intel     | SSDSCKKF240H6L     | 240 GB | 1       | 47    | 20    | 0.01   |
| OCZ       | VERTEX3 LP         | 240 GB | 1       | 2268  | 1019  | 0.01   |
| Timetec   | 30TT253X2-1TB      | 1 TB   | 1       | 2     | 0     | 0.01   |
| Vaseky    | V800-256G          | 256 GB | 1       | 2     | 0     | 0.01   |
| Intel     | SSDSC2KW120H6      | 120 GB | 4       | 60    | 49    | 0.01   |
| ACPI      | M2SCF-6M           | 64 GB  | 1       | 2     | 0     | 0.01   |
| Netac     | SSD                | 160 GB | 1       | 2     | 0     | 0.01   |
| VSEVEN    | V7 SSD             | 512 GB | 1       | 2     | 0     | 0.01   |
| SK hynix  | SH920 2.5 7MM      | 128 GB | 1       | 54    | 25    | 0.01   |
| China     | MSATA SSD          | 128 GB | 1       | 2     | 0     | 0.01   |
| Win Me... | SWR256G-301II      | 256 GB | 1       | 2     | 0     | 0.01   |
| Mushkin   | MKNSSDCL120GB      | 120 GB | 1       | 2066  | 1007  | 0.01   |
| Foxline   | FLSSD120SM5        | 120 GB | 1       | 2     | 0     | 0.01   |
| SPCC      | M.2 SSD            | 128 GB | 1       | 2     | 0     | 0.01   |
| Lite-On   | CV1-8B512          | 512 GB | 2       | 2     | 0     | 0.01   |
| SanDisk   | SDSSDH120GG25      | 120 GB | 1       | 112   | 55    | 0.01   |
| Intel     | SSDSC2KW480H6      | 480 GB | 2       | 27    | 30    | 0.01   |
| Intel     | SSDSC2BB300G4R     | 304 GB | 2       | 2029  | 1029  | 0.01   |
| Netac     | SSD                | 320 GB | 1       | 96    | 48    | 0.01   |
| ADATA     | SP610              | 512 GB | 1       | 1     | 0     | 0.01   |
| Netac     | W800S 256GB SSD    | 256 GB | 1       | 1     | 0     | 0.01   |
| SanDisk   | SD7SB3Q128G1001    | 128 GB | 4       | 195   | 100   | 0.01   |
| SanDisk   | SD8SBAT128G        | 128 GB | 1       | 1     | 0     | 0.01   |
| Kingston  | SKC300S37A240G     | 240 GB | 2       | 1     | 0     | 0.01   |
| Toshiba   | THNSNK512GCS8 SATA | 512 GB | 1       | 189   | 100   | 0.01   |
| Teclast   | BD256GB SLCB-2280  | 256 GB | 2       | 1     | 0     | 0.01   |
| TMI       | 256GB SATA CRMP... | 240 GB | 1       | 1     | 0     | 0.01   |
| 2-Power   | SSD2042A           | 240 GB | 1       | 1     | 0     | 0.01   |
| BHT       | WR202I0032G E70... | 32 GB  | 1       | 1     | 0     | 0.01   |
| Cactus    | CactusFlashCard    | 64 GB  | 1       | 1     | 0     | 0.01   |
| Fujitsu   | F500S 128G         | 128 GB | 1       | 1     | 0     | 0.01   |
| Hikvision | HS-SSD-C160 256G   | 256 GB | 1       | 1     | 0     | 0.01   |
| KingSpec  | P3D-240            | 240 GB | 1       | 1     | 0     | 0.01   |
| China     | NGFF 2280 256GB... | 256 GB | 4       | 1     | 0     | 0.00   |
| DEPO      | SM3DT-120          | 120 GB | 2       | 1     | 108   | 0.00   |
| ASENNO    | AS25               | 120 GB | 2       | 1     | 0     | 0.00   |
| FASTDISK  | SSD                | 64 GB  | 1       | 1     | 0     | 0.00   |
| Foxline   | FLSSD120X5SE       | 120 GB | 1       | 1     | 0     | 0.00   |
| Kingston  | SA400S37-120G      | 128 GB | 1       | 1     | 0     | 0.00   |
| Netac     | GN256 2280         | 256 GB | 1       | 1     | 0     | 0.00   |
| Team      | T253E2001T         | 1 TB   | 1       | 1     | 0     | 0.00   |
| Yunhai... | Y6-240G            | 240 GB | 1       | 1     | 0     | 0.00   |
| PNY       | SSD9SC240GCDA      | 240 GB | 1       | 1804  | 1015  | 0.00   |
| Toshiba   | THNSNK256GVN8 M... | 256 GB | 9       | 189   | 103   | 0.00   |
| China     | S41CF256G          | 256 GB | 1       | 1     | 0     | 0.00   |
| INDMEM    | M.2 2280           | 128 GB | 1       | 1     | 0     | 0.00   |
| Toshiba   | THNSNK256GCS8 SATA | 256 GB | 3       | 168   | 100   | 0.00   |
| ADATA     | SU650 1.9TB        | 1.9 TB | 1       | 1     | 0     | 0.00   |
| KingSpec  | ACJC2M064S25       | 64 GB  | 1       | 1     | 0     | 0.00   |
| Lite-On   | L8T-64L6G          | 64 GB  | 1       | 1     | 0     | 0.00   |
| Micron    | C400-MTFDDAT064MAM | 64 GB  | 1       | 1     | 0     | 0.00   |
| WDC       | WD A3              | 128 GB | 1       | 1     | 0     | 0.00   |
| Mcpoint   | MC240              | 240 GB | 1       | 6     | 3     | 0.00   |
| Micron    | 5300_MTFDDAK240TDS | 240 GB | 2       | 1     | 0     | 0.00   |
| TCSUNBOW  | X1                 | 16 GB  | 1       | 1     | 0     | 0.00   |
| Intel     | SSDSC2BA400G3T     | 400 GB | 1       | 1671  | 1029  | 0.00   |
| SK hynix  | HFS128G38MNB-2200A | 128 GB | 3       | 228   | 133   | 0.00   |
| Foxline   | FLSSD256X5         | 256 GB | 3       | 1     | 0     | 0.00   |
| Kingston  | RBU-SNS8350DES3... | 128 GB | 8       | 146   | 96    | 0.00   |
| Team      | L5 LITE SSD        | 240 GB | 1       | 472   | 296   | 0.00   |
| MidasF... | SSD                | 120 GB | 1       | 1     | 0     | 0.00   |
| ACPI      | MSS4FV-MP mSATA... | 128 GB | 1       | 1     | 0     | 0.00   |
| China     | SATA3 60GB SSD     | 64 GB  | 1       | 1     | 0     | 0.00   |
| Goodram   | SSDPR-CL100-120    | 120 GB | 1       | 1     | 0     | 0.00   |
| Foxline   | FLSSD128X5         | 128 GB | 3       | 1     | 0     | 0.00   |
| China     | 2.5 SSD            | 240 GB | 1       | 1     | 0     | 0.00   |
| Toshiba   | THNSNK128GVN8 M... | 128 GB | 4       | 146   | 100   | 0.00   |
| Corsair   | CSSD-F120GB2       | 120 GB | 1       | 2080  | 1455  | 0.00   |
| SK hynix  | HFS064G3AMNB-2200A | 64 GB  | 2       | 406   | 585   | 0.00   |
| Foxline   | FLSSD240X5SE       | 240 GB | 2       | 1     | 0     | 0.00   |
| Teclast   | 128GB A850         | 128 GB | 1       | 1     | 0     | 0.00   |
| BHT       | WR202I0032G E70... | 32 GB  | 1       | 1     | 0     | 0.00   |
| Plextor   | PX-512M6M          | 512 GB | 1       | 1     | 0     | 0.00   |
| S3+       | S3SSDC480XEU       | 480 GB | 1       | 1     | 0     | 0.00   |
| Intel     | SSDSC2KW240H6      | 240 GB | 8       | 9     | 136   | 0.00   |
| Patriot   | Pyro m3            | 240 GB | 1       | 1378  | 1015  | 0.00   |
| Transcend | TS128XBTMT3D58G    | 128 GB | 1       | 138   | 101   | 0.00   |
| ADATA     | AXM14S3-128GM-B    | 128 GB | 1       | 1363  | 1018  | 0.00   |
| Lite-On   | LAT-256M3S         | 256 GB | 2       | 1605  | 1516  | 0.00   |
| SK hynix  | HFS032G34MNC-2200A | 32 GB  | 1       | 441   | 337   | 0.00   |
| ADATA     | IMSS316-256GD      | 256 GB | 1       | 1     | 0     | 0.00   |
| BR        | SSD 60G            | 64 GB  | 1       | 1     | 0     | 0.00   |
| Indilinx  | IND-S3N80S-256G    | 256 GB | 2       | 1     | 0     | 0.00   |
| Transcend | TS32GMSA370        | 32 GB  | 2       | 1     | 0     | 0.00   |
| Kingston  | SHPM2280P2H-240G   | 240 GB | 6       | 512   | 639   | 0.00   |
| Lite-On   | LMT-19nmBGA-128... | 128 GB | 1       | 1     | 0     | 0.00   |
| Patriot   | Solid              | 240 GB | 2       | 1     | 0     | 0.00   |
| Team      | TM8PS7001T         | 1 TB   | 1       | 1     | 0     | 0.00   |
| Micron    | P300-MTFDBAC050SAL | 50 GB  | 1       | 1411  | 1140  | 0.00   |
| Team      | M8PS5 SSD          | 128 GB | 1       | 1     | 0     | 0.00   |
| Dogfish   | SSD                | 64 GB  | 3       | 1     | 0     | 0.00   |
| Philips   | SSD                | 120 GB | 1       | 1     | 0     | 0.00   |
| Intel     | SSDSC2BX200G4R     | 200 GB | 3       | 1172  | 1027  | 0.00   |
| KingSpec  | ACJC2M128S25       | 128 GB | 1       | 1     | 0     | 0.00   |
| China     | W800SH 512GB SSD   | 512 GB | 1       | 1     | 0     | 0.00   |
| China     | X160EB             | 500 GB | 1       | 1     | 0     | 0.00   |
| Team      | T253A3001T         | 1 TB   | 1       | 1     | 0     | 0.00   |
| Intel     | SSDSC2BX400G4R     | 400 GB | 3       | 1103  | 1027  | 0.00   |
| INDMEM    | M.2 2280           | 64 GB  | 1       | 1     | 0     | 0.00   |
| Intel     | N18A               | 240 GB | 2       | 1     | 0     | 0.00   |
| Netac     | SSD0128S00         | 128 GB | 1       | 1     | 0     | 0.00   |
| Transcend | TS1TSSD370         | 1 TB   | 1       | 1     | 0     | 0.00   |
| Intel     | SSDSC2BA200G4R     | 200 GB | 2       | 1037  | 1028  | 0.00   |
| Intel     | SSDSC2KG960G7R     | 960 GB | 2       | 1035  | 1028  | 0.00   |
| Teclast   | 240GB A800         | 240 GB | 1       | 1     | 0     | 0.00   |
| Foxline   | FLSSD60X3          | 64 GB  | 1       | 993   | 1016  | 0.00   |
| Toshiba   | KSG60ZSE512G SATA  | 512 GB | 2       | 97    | 100   | 0.00   |
| SPCC      | SSD                | 32 GB  | 1       | 998   | 1036  | 0.00   |
| China     | M.2 SSD            | 256 GB | 1       | 0     | 0     | 0.00   |
| Kingch... | SSD                | 480 GB | 1       | 0     | 0     | 0.00   |
| Plextor   | PH6-CE240          | 240 GB | 2       | 0     | 0     | 0.00   |
| Zheino    | CHN25SATAS1 064    | 64 GB  | 2       | 0     | 0     | 0.00   |
| ADATA     | SU630 1.9TB        | 1.9 TB | 1       | 0     | 0     | 0.00   |
| China     | ESA3SMN2ISN1BQ4... | 480 GB | 1       | 0     | 0     | 0.00   |
| ADATA     | SX900              | 112 GB | 1       | 872   | 1016  | 0.00   |
| Teclast   | BD256GB SHCB-2280  | 256 GB | 2       | 0     | 0     | 0.00   |
| Corsair   | CSSD-F40GB2        | 40 GB  | 2       | 500   | 588   | 0.00   |
| FORESEE   | 32GB SSD           | 32 GB  | 1       | 0     | 0     | 0.00   |
| KLEVV     | NEO N400 SSD       | 120 GB | 1       | 0     | 0     | 0.00   |
| Kross ... | KE-SSDIS12G        | 120 GB | 1       | 0     | 0     | 0.00   |
| Maxmemory | X100               | 240 GB | 1       | 0     | 0     | 0.00   |
| Patriot   | Burst Elite        | 240 GB | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSC2KW180H6      | 180 GB | 3       | 5     | 74    | 0.00   |
| SPCC      | SSD162             | 55 GB  | 1       | 855   | 1036  | 0.00   |
| SK hynix  | HFS060G32MNM-1010U | 64 GB  | 1       | 822   | 1016  | 0.00   |
| Eluktro   | TRO-SSD7-500GB-PRO | 500 GB | 1       | 806   | 1016  | 0.00   |
| Patriot   | JAJM600M128C       | 128 GB | 1       | 0     | 0     | 0.00   |
| Phison    | S11-256G-PHISON... | 256 GB | 1       | 0     | 0     | 0.00   |
| SandForce | FM-25S2S-60GBP2    | 64 GB  | 1       | 317   | 416   | 0.00   |
| FORESEE   | G500F256GB         | 256 GB | 1       | 0     | 0     | 0.00   |
| ZHITAI    | SC001 Active 1T... | 1 TB   | 1       | 0     | 0     | 0.00   |
| BAITITON  | BT58SSD11S         | 480 GB | 1       | 0     | 0     | 0.00   |
| China     | REVOLUTIONS500_256 | 256 GB | 1       | 0     | 0     | 0.00   |
| Innodisk  | mSATA 3MG2-P       | 992 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | SC210 2.5 7MM      | 256 GB | 2       | 556   | 856   | 0.00   |
| ORTIAL    | SSD                | 256 GB | 4       | 0     | 0     | 0.00   |
| HP Phison | PSSBN016GA27MC0    | 16 GB  | 1       | 717   | 1033  | 0.00   |
| Lite-On   | E200-160           | 160 GB | 1       | 12    | 18    | 0.00   |
| Intenso   | SSDAS256           | 256 GB | 1       | 0     | 0     | 0.00   |
| Micron    | 5300_MTFDDAK480TDS | 480 GB | 2       | 0     | 0     | 0.00   |
| Intel     | SSDSCMMW120A3L     | 120 GB | 1       | 649   | 1017  | 0.00   |
| Advantech | SQF-S25M4-32G-S9C  | 32 GB  | 1       | 0     | 0     | 0.00   |
| INDMEM    | M.2 2280           | 256 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | A400-120G          | 128 GB | 1       | 0     | 0     | 0.00   |
| QUMO      | SSD                | 480 GB | 1       | 625   | 1015  | 0.00   |
| Indilinx  | InM2246S3-128G     | 128 GB | 2       | 0     | 0     | 0.00   |
| Netac     | S535N8-128GYN      | 128 GB | 2       | 0     | 0     | 0.00   |
| Samsung   | SSD PM810 TM       | 128 GB | 2       | 688   | 1107  | 0.00   |
| China     | SSD                | 2 TB   | 1       | 0     | 0     | 0.00   |
| Intenso   | SSD Sata III       | 247 GB | 1       | 18    | 32    | 0.00   |
| SanDisk   | SSD P4             | 64 GB  | 2       | 60    | 449   | 0.00   |
| Netac     | MST1002-1T         | 1 TB   | 1       | 0     | 0     | 0.00   |
| Netac     | S535M3-128GYN      | 128 GB | 1       | 0     | 0     | 0.00   |
| Intel     | SSDMCEAW080A4 m... | 80 GB  | 2       | 515   | 1008  | 0.00   |
| Samsung   | MZNLH128HBHQ-000H1 | 128 GB | 6       | 51    | 100   | 0.00   |
| DOGFISH   | SSD                | 512 GB | 1       | 0     | 0     | 0.00   |
| Intenso   | SATA3 128GB SSD    | 128 GB | 1       | 0     | 0     | 0.00   |
| Kingch... | SSD                | 128 GB | 1       | 0     | 0     | 0.00   |
| OCZ       | INTREPID 3700      | 240 GB | 1       | 478   | 1020  | 0.00   |
| ADATA     | SP900NS38          | 256 GB | 2       | 475   | 1020  | 0.00   |
| BIOSTAR   | S120-256GB         | 256 GB | 1       | 0     | 0     | 0.00   |
| China     | SH00R128GB         | 128 GB | 1       | 0     | 0     | 0.00   |
| Liren     | LIREN128G          | 128 GB | 1       | 0     | 0     | 0.00   |
| Netac     | S539N8-256GSN      | 256 GB | 1       | 0     | 0     | 0.00   |
| OSCOO     | OSC SSD            | 128 GB | 1       | 0     | 0     | 0.00   |
| ADATA     | XM12               | 32 GB  | 1       | 465   | 1015  | 0.00   |
| Apple     | SSD SM256C         | 256 GB | 3       | 335   | 788   | 0.00   |
| ADATA     | XM11 128GB-V2      | 128 GB | 1       | 449   | 1048  | 0.00   |
| BIWIN     | C6370_128GB        | 128 GB | 1       | 0     | 0     | 0.00   |
| Gost      | SSD120             | 120 GB | 1       | 0     | 0     | 0.00   |
| Hyundai   | 240GB SSD          | 240 GB | 1       | 0     | 0     | 0.00   |
| Lite-On   | LMT-19nmBGA-64G-DS | 64 GB  | 1       | 0     | 0     | 0.00   |
| SMI       | B17A               | 240 GB | 1       | 0     | 0     | 0.00   |
| T-CREATE  | T253TA001T         | 1 TB   | 1       | 0     | 0     | 0.00   |
| SanDisk   | SD8SBAT-032G-1006  | 32 GB  | 5       | 0     | 1     | 0.00   |
| Indilinx  | IND-S325S120G      | 120 GB | 1       | 3     | 8     | 0.00   |
| PNY       | SSD2SC120G3LC70... | 120 GB | 1       | 393   | 1015  | 0.00   |
| Apacer    | AST280             | 120 GB | 2       | 0     | 0     | 0.00   |
| China     | T60                | 64 GB  | 2       | 0     | 0     | 0.00   |
| Reeinno   | ST960GB S7S3       | 960 GB | 1       | 0     | 0     | 0.00   |
| ZHITAI    | SC001 Active 25... | 256 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | SH103S3240G-NV     | 240 GB | 1       | 377   | 1018  | 0.00   |
| PNY       | SSD2SC120GE2DA0... | 120 GB | 1       | 373   | 1018  | 0.00   |
| Kingston  | SVP200S37A256G     | 256 GB | 2       | 370   | 1016  | 0.00   |
| SPCC      | SSD170             | 64 GB  | 1       | 358   | 1016  | 0.00   |
| Mushkin   | MKNSSDCL120GB-DX   | 120 GB | 1       | 348   | 1006  | 0.00   |
| SK hynix  | HFS256G3AMNB-2200A | 256 GB | 6       | 220   | 789   | 0.00   |
| Lite-On   | CS1-SP32-11 M.2... | 32 GB  | 1       | 1     | 4     | 0.00   |
| Mushkin   | MKNSSDCL480GB-DX   | 480 GB | 1       | 347   | 1020  | 0.00   |
| Dahua     | C800A SSD          | 240 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TS8GHSD630         | 8 GB   | 1       | 679   | 2050  | 0.00   |
| Intel     | SSDSCKKF256G8H     | 256 GB | 7       | 31    | 98    | 0.00   |
| UMAX      | 2242               | 512 GB | 2       | 0     | 0     | 0.00   |
| Kingston  | SNS4151S316GD      | 16 GB  | 3       | 313   | 1022  | 0.00   |
| China     | ESA3ASA2ISN1BQ4... | 480 GB | 1       | 0     | 0     | 0.00   |
| China     | GSDSL128TY2AAQGCX  | 128 GB | 1       | 0     | 0     | 0.00   |
| FASTDISK  | SSD 32G            | 32 GB  | 1       | 0     | 0     | 0.00   |
| GLOWAY    | STK120GS3-S7       | 120 GB | 1       | 0     | 0     | 0.00   |
| Intenso   | VERICO SSD         | 240 GB | 1       | 0     | 0     | 0.00   |
| Patriot   | Torch LE           | 120 GB | 1       | 0     | 0     | 0.00   |
| Lite-On   | LMT-256M6M-HP      | 256 GB | 1       | 39    | 152   | 0.00   |
| ADATA     | SX900              | 512 GB | 1       | 259   | 1018  | 0.00   |
| AXIOMTEK  | FSA016G300MC4T-H   | 16 GB  | 1       | 0     | 0     | 0.00   |
| DERLAR    | SSD                | 128 GB | 1       | 0     | 0     | 0.00   |
| GLOWAY    | VAL64GM3-mSATA     | 64 GB  | 1       | 0     | 0     | 0.00   |
| Golden... | SSD                | 32 GB  | 1       | 0     | 0     | 0.00   |
| Micron    | MTFDDAK2T0TDL      | 2 TB   | 1       | 0     | 0     | 0.00   |
| TEUTONS   | SSD                | 256 GB | 1       | 0     | 0     | 0.00   |
| Toshiba   | THNSF81Q92CSE      | 1.9 TB | 1       | 0     | 0     | 0.00   |
| Tronos    | TN240G-SSD         | 240 GB | 1       | 0     | 0     | 0.00   |
| Bamba     | SSD                | 240 GB | 1       | 60    | 249   | 0.00   |
| GeIL      | ZENITH S3-120GB    | 120 GB | 1       | 245   | 1021  | 0.00   |
| Myung     | G3 Series          | 120 GB | 1       | 228   | 1015  | 0.00   |
| Goldenfir | T650-120G          | 128 GB | 1       | 0     | 0     | 0.00   |
| Lite-On   | S960 256           | 256 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZNLH256HAJD-000L7 | 256 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | HFS256G38MNB-2200A | 256 GB | 1       | 207   | 1007  | 0.00   |
| China     | MKSCE1BD060M4      | 64 GB  | 4       | 199   | 1016  | 0.00   |
| PNY       | 69D03094-T         | 40 GB  | 1       | 195   | 1016  | 0.00   |
| China     | ESA3SMD2HTGT240GB  | 240 GB | 1       | 51    | 273   | 0.00   |
| Kingston  | SNS4151S316G       | 16 GB  | 4       | 187   | 1026  | 0.00   |
| Patriot   | Pyro SE            | 240 GB | 1       | 180   | 1016  | 0.00   |
| Apacer    | 8GB SATA Flash ... | 8 GB   | 2       | 18    | 104   | 0.00   |
| SanDisk   | SD9SN8W-256G-1006  | 256 GB | 8       | 162   | 982   | 0.00   |
| China     | LS 512GB M300      | 512 GB | 1       | 0     | 0     | 0.00   |
| China     | S3 SSD             | 256 GB | 1       | 0     | 0     | 0.00   |
| China     | T120               | 120 GB | 1       | 0     | 0     | 0.00   |
| EVM       | 512GB SSD          | 512 GB | 1       | 0     | 0     | 0.00   |
| Faspeed   | H5-30G             | 32 GB  | 1       | 0     | 0     | 0.00   |
| Fujitsu   | F500s 240G         | 240 GB | 1       | 0     | 0     | 0.00   |
| Indilinx  | IND-S3N80S-128G    | 128 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | CF Card            | 8 GB   | 2       | 0     | 0     | 0.00   |
| Toshiba   | THNSNK128GCS8 SATA | 128 GB | 1       | 16    | 100   | 0.00   |
| China     | 240G SATA III SSD  | 240 GB | 1       | 154   | 1016  | 0.00   |
| Goldenfir | T650-120GB         | 120 GB | 1       | 4     | 28    | 0.00   |
| SK hynix  | SH910 mSATA        | 128 GB | 1       | 151   | 1026  | 0.00   |
| Kingston  | SNS4151S332G       | 32 GB  | 2       | 149   | 1022  | 0.00   |
| PNY       | SSD2SC240G3LC70... | 240 GB | 1       | 141   | 1017  | 0.00   |
| Lite-On   | CV8-CE256-HP       | 256 GB | 1       | 135   | 1007  | 0.00   |
| Intenso   | TOP M.2 SATA       | 256 GB | 1       | 125   | 961   | 0.00   |
| China     | JDa He SATA DISK   | 64 GB  | 1       | 135   | 1045  | 0.00   |
| MicroD... | 512G SSD           | 512 GB | 1       | 0     | 0     | 0.00   |
| Netac     | GM256              | 256 GB | 1       | 0     | 0     | 0.00   |
| Teclast   | 128GB NS550-2242   | 128 GB | 1       | 0     | 0     | 0.00   |
| Vaseky    | V900-1TB           | 1 TB   | 1       | 0     | 0     | 0.00   |
| SK hynix  | HFS500G32TND-3110A | 500 GB | 1       | 142   | 1209  | 0.00   |
| SanDisk   | SD9SN8W-128G-1006  | 128 GB | 29      | 89    | 981   | 0.00   |
| AXIOMTEK  | FSA128GMC5T        | 128 GB | 1       | 0     | 0     | 0.00   |
| China     | SATA SSD           | 24 GB  | 1       | 0     | 0     | 0.00   |
| DOGFISH   | SSD                | 128 GB | 1       | 0     | 0     | 0.00   |
| Dahua     | C800A SSD          | 120 GB | 1       | 0     | 0     | 0.00   |
| HP        | SSD S750           | 512 GB | 1       | 0     | 0     | 0.00   |
| KINGPAN   | SSD                | 256 GB | 1       | 0     | 0     | 0.00   |
| Neo Forza | NFS011SA351-600... | 512 GB | 1       | 0     | 0     | 0.00   |
| Palit     | UVSE               | 240 GB | 1       | 0     | 0     | 0.00   |
| Plextor   | PX-32G5L           | 32 GB  | 1       | 0     | 0     | 0.00   |
| Smartbuy  | 120GB STELS        | 128 GB | 1       | 0     | 0     | 0.00   |
| Team      | T253E2512G         | 512 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TS16GMTS400        | 16 GB  | 1       | 0     | 0     | 0.00   |
| WDC       | WDBNCE0010PNC-WRSN | 1 TB   | 1       | 0     | 0     | 0.00   |
| PNY       | SSD2SC240GC2DH1... | 240 GB | 1       | 85    | 1023  | 0.00   |
| Intel     | SSDSC2KF512H6 SATA | 512 GB | 1       | 7     | 84    | 0.00   |
| Micron    | MTFDDAT064MAM-1J2  | 64 GB  | 1       | 85    | 1039  | 0.00   |
| HP Phison | PSSBN032GA27MC0    | 32 GB  | 1       | 81    | 1039  | 0.00   |
| ADATA     | XM11 128GB-V3      | 128 GB | 1       | 77    | 1016  | 0.00   |
| ADATA     | AXM21S3-24GM-B     | 24 GB  | 1       | 77    | 1020  | 0.00   |
| Samsung   | MZNLH256HAJD-000H1 | 256 GB | 1       | 7     | 100   | 0.00   |
| Transcend | TS64GSSD340K       | 64 GB  | 1       | 74    | 1008  | 0.00   |
| Mushkin   | MKNSSDCR120GB-DX7  | 120 GB | 1       | 73    | 1016  | 0.00   |
| Kingston  | SUV500M8960G       | 960 GB | 1       | 96    | 1444  | 0.00   |
| SandForce | 906190             | 64 GB  | 1       | 65    | 1018  | 0.00   |
| PNY       | SSD2SC120G3LC72... | 120 GB | 1       | 65    | 1019  | 0.00   |
| ADATA     | SP900NS38          | 512 GB | 1       | 64    | 1020  | 0.00   |
| MaxDig... | MD300 128G         | 128 GB | 1       | 41    | 666   | 0.00   |
| Kingston  | SMS151S324G        | 24 GB  | 2       | 61    | 1022  | 0.00   |
| Kingston  | SHPM2280P2-480G    | 480 GB | 1       | 54    | 1009  | 0.00   |
| Innodisk  | 2.5" SATA SSD 3... | 3.8 TB | 3       | 50    | 1010  | 0.00   |
| Lite-On   | CV8-8E128-HP       | 128 GB | 27      | 47    | 1007  | 0.00   |
| Lite-On   | LMT-128M3M         | 128 GB | 1       | 44    | 1009  | 0.00   |
| China     | SSV5               | 480 GB | 2       | 0     | 0     | 0.00   |
| DOGGO     | DQ-60G             | 64 GB  | 2       | 0     | 0     | 0.00   |
| Intel     | SSDSC2BB150G7      | 150 GB | 1       | 0     | 0     | 0.00   |
| KDATA     | SSD                | 128 GB | 1       | 0     | 0     | 0.00   |
| KingDian  | M200               | 64 GB  | 1       | 0     | 0     | 0.00   |
| KingDian  | S180               | 120 GB | 1       | 0     | 0     | 0.00   |
| Netac     | Secureye SSD       | 128 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TS16GCFX600I       | 16 GB  | 1       | 0     | 0     | 0.00   |
| Transcend | TS64GSSD420I       | 64 GB  | 1       | 0     | 0     | 0.00   |
| Xinsujie  | XSJ-X100-128GB     | 128 GB | 1       | 0     | 0     | 0.00   |
| Lite-On   | CV8-8E256-HP       | 256 GB | 2       | 40    | 1007  | 0.00   |
| China     | IM3D L06B B0KB     | 120 GB | 1       | 2     | 66    | 0.00   |
| Intel     | SSDSCKKB240G8R     | 240 GB | 1       | 31    | 1026  | 0.00   |
| Vaseky    | V820-1TB           | 1 TB   | 1       | 1     | 85    | 0.00   |
| SanDisk   | TE22D10400GE8001   | 400 GB | 1       | 34    | 2047  | 0.00   |
| AMD       | R5S120GBSF         | 120 GB | 1       | 15    | 1016  | 0.00   |
| JIAWEI    | SSD                | 240 GB | 1       | 47    | 3057  | 0.00   |
| Intel     | SSDSC2KW360H6      | 360 GB | 2       | 16    | 1365  | 0.00   |
| Neo Forza | NFS011SA356-600... | 256 GB | 1       | 41    | 3130  | 0.00   |
| Kingston  | SNS4151S332GD      | 32 GB  | 2       | 9     | 1025  | 0.00   |
| Intel     | SSDSC2KF240H6L     | 240 GB | 1       | 16    | 2012  | 0.00   |
| WDC       | PC SA530 SDASN8... | 256 GB | 2       | 8     | 999   | 0.00   |
| SSSTC     | CVB-8D128-HP       | 128 GB | 3       | 7     | 1008  | 0.00   |
| Lite-On   | IT LST-16S9G-HP    | 16 GB  | 1       | 6     | 1021  | 0.00   |
| SPCC      | M.2 SSD            | 1 TB   | 1       | 10    | 2711  | 0.00   |
| Mushkin   | MKNSSDCR250GB-7... | 250 GB | 1       | 3     | 1016  | 0.00   |
| ADATA     | SX910              | 512 GB | 1       | 3     | 1018  | 0.00   |
| Micron    | MTFDDAV256TDL-1... | 256 GB | 7       | 2     | 1008  | 0.00   |
| Intel     | SSDSC2KG400G7M ... | 400 GB | 1       | 2     | 1025  | 0.00   |
| SanDisk   | sandisk120         | 120 GB | 1       | 0     | 21    | 0.00   |
| Kingston  | EK60HYXTFY176 V100 | 64 GB  | 1       | 1     | 1130  | 0.00   |
| SSSTC     | CVZ-83128-HP       | 128 GB | 1       | 0     | 1008  | 0.00   |
| DUEX      | DX240H             | 240 GB | 1       | 0     | 1007  | 0.00   |
| SMI       | SSD DISK           | 506 GB | 1       | 0     | 1957  | 0.00   |
| Mushkin   | MKNSSDCR480GB-7-A  | 480 GB | 1       | 0     | 1016  | 0.00   |

SSD by Family
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG       | Family                 | Models | Samples | Days  | Err   | MTBF |
|-----------|------------------------|--------|---------|-------|-------|------|
| Intel     | X25-E SSDs             | 2      | 4       | 2237  | 0     | 6.13   |
| Toshiba   | HK4R Series SSD        | 2      | 2       | 1433  | 0     | 3.93   |
| Transcend | Unknown                | 17     | 38      | 1448  | 57    | 3.54   |
| Kingston  | JMicron/Maxiotek ba... | 2      | 4       | 1270  | 0     | 3.48   |
| OYUNKEY   | Unknown                | 1      | 1       | 1107  | 0     | 3.04   |
| Intel     | 730 and DC S35x0/36... | 30     | 108     | 1245  | 105   | 2.98   |
| Micron    | MX100/MX200/M5x0/M6... | 1      | 1       | 1083  | 0     | 2.97   |
| SandForce | SandForce Driven SSDs  | 2      | 2       | 1209  | 208   | 2.88   |
| Intel     | X18-M/X25-M G1 SSDs    | 4      | 4       | 1037  | 0     | 2.84   |
| Toshiba   | HG2 Series             | 2      | 7       | 932   | 0     | 2.55   |
| Intel     | Dell Certified Inte... | 1      | 2       | 1166  | 1     | 2.40   |
| HPE       | Unknown                | 3      | 3       | 831   | 0     | 2.28   |
| Crucial   | RealSSD m4/C400        | 3      | 14      | 867   | 145   | 2.26   |
| Crucial   | RealSSD m4/C400/P400   | 6      | 135     | 961   | 169   | 2.25   |
| Crucial   | RealSSD C300/P300      | 3      | 21      | 1108  | 241   | 2.25   |
| Radeon    | Indilinx Barefoot 3... | 1      | 4       | 778   | 0     | 2.13   |
| Toshiba   | HG3 Series             | 3      | 5       | 766   | 0     | 2.10   |
| Micro ... | Unknown                | 1      | 1       | 722   | 0     | 1.98   |
| Intel     | 320 Series SSDs        | 11     | 85      | 748   | 13    | 1.88   |
| SMART     | Unknown                | 1      | 1       | 681   | 0     | 1.87   |
| Axiom     | Unknown                | 2      | 2       | 644   | 0     | 1.77   |
| OCZ       | Indilinx Barefoot b... | 5      | 12      | 747   | 1     | 1.75   |
| Intel     | 520 Series SSDs        | 8      | 133     | 785   | 199   | 1.74   |
| OCZ       | SandForce Driven SSDs  | 48     | 385     | 810   | 38    | 1.73   |
| Corsair   | SandForce Driven SSDs  | 27     | 204     | 780   | 103   | 1.68   |
| Toshiba   | HG5 Series             | 1      | 5       | 599   | 0     | 1.64   |
| OWC       | SandForce Driven SSDs  | 3      | 17      | 629   | 1     | 1.61   |
| Galaxy    | Unknown                | 1      | 1       | 578   | 0     | 1.58   |
| SATADOM   | Innodisk 3IE3/3ME3/... | 1      | 1       | 574   | 0     | 1.57   |
| OCZ       | Indilinx Barefoot_2... | 12     | 150     | 674   | 3     | 1.54   |
| ADATA     | JMicron/Maxiotek ba... | 3      | 16      | 549   | 0     | 1.50   |
| Intel     | 330/335 Series SSDs    | 6      | 70      | 664   | 1     | 1.43   |
| MyDigi... | Unknown                | 4      | 10      | 495   | 0     | 1.36   |
| Toshiba   | OCZ                    | 5      | 19      | 528   | 1     | 1.36   |
| Mushkin   | SandForce Driven SSDs  | 16     | 26      | 641   | 198   | 1.33   |
| Kingston  | JMicron based SSDs     | 14     | 56      | 682   | 3     | 1.30   |
| Innodisk  | 3IE3/3ME3/3ME4 SSDs    | 3      | 5       | 471   | 0     | 1.29   |
| Toshiba   | HG6 Series SSD         | 18     | 90      | 469   | 1     | 1.28   |
| Apple     | JMicron based SSDs     | 3      | 16      | 502   | 1     | 1.28   |
| ADATA     | SandForce Driven SSDs  | 14     | 115     | 509   | 4     | 1.22   |
| Micron    | RealSSD m4/C400/P400   | 8      | 48      | 476   | 229   | 1.22   |
| Samsung   | Unknown                | 35     | 75      | 485   | 5     | 1.22   |
| Toshiba   | HG6 Series             | 1      | 7       | 443   | 0     | 1.21   |
| Seagate   | 600 Series             | 1      | 2       | 429   | 0     | 1.18   |
| Micron    | 5100 Pro / 5200 SSDs   | 6      | 21      | 513   | 16    | 1.14   |
| Samsung   | Samsung based SSDs     | 320    | 6763    | 419   | 6     | 1.11   |
| ADATA     | JMicron based SSDs     | 7      | 38      | 429   | 1     | 1.11   |
| Toshiba   | JMicron based SSDs     | 2      | 4       | 396   | 0     | 1.09   |
| Innodisk  | Unknown                | 6      | 8       | 390   | 0     | 1.07   |
| Phison    | Phison Driven SSDs     | 3      | 4       | 390   | 0     | 1.07   |
| Kingston  | SandForce Driven SSDs  | 41     | 1406    | 463   | 45    | 1.06   |
| Intel     | 510 Series SSDs        | 2      | 6       | 383   | 0     | 1.05   |
| FCS       | Unknown                | 1      | 1       | 381   | 0     | 1.05   |
| Apple     | SD/SM/TS E/F/G SSDs    | 16     | 216     | 390   | 1     | 1.04   |
| OCZ       | OCZ/Toshiba Trion SSDs | 5      | 46      | 406   | 1     | 1.04   |
| Seagate   | Indilinx Barefoot b... | 1      | 1       | 378   | 0     | 1.04   |
| CFD       | Unknown                | 3      | 3       | 375   | 0     | 1.03   |
| KingShare | Unknown                | 2      | 2       | 373   | 0     | 1.02   |
| Toshiba   | OCZ/Toshiba Trion SSDs | 7      | 57      | 413   | 1     | 1.01   |
| OCZ       | Indilinx Barefoot 3... | 17     | 92      | 397   | 24    | 0.99   |
| addlink   | Unknown                | 2      | 4       | 359   | 0     | 0.98   |
| Toshiba   | HG5d Series            | 8      | 23      | 429   | 29    | 0.98   |
| Corsair   | Unknown                | 24     | 49      | 709   | 62    | 0.96   |
| Transcend | JMicron based SSDs     | 6      | 18      | 375   | 112   | 0.94   |
| Goodram   | Phison Driven OEM SSDs | 4      | 63      | 333   | 1     | 0.91   |
| SanDisk   | SATA Cloudspeed Max... | 3      | 4       | 333   | 0     | 0.91   |
| Plextor   | M3/M5/M6/M7 Series ... | 9      | 21      | 324   | 0     | 0.89   |
| Micron    | RealSSD m4/C400        | 3      | 8       | 358   | 379   | 0.88   |
| Intel     | S3520 Series SSDs      | 1      | 1       | 317   | 0     | 0.87   |
| Aura      | Unknown                | 1      | 1       | 310   | 0     | 0.85   |
| Corsair   | Indilinx Barefoot b... | 4      | 5       | 372   | 1     | 0.83   |
| Intel     | 53x and Pro 1500/25... | 14     | 112     | 452   | 3     | 0.82   |
| Transcend | SandForce Driven SSDs  | 6      | 12      | 434   | 15    | 0.82   |
| Intel     | 530 Series SSDs        | 2      | 52      | 399   | 1     | 0.81   |
| WDC       | Unknown                | 6      | 12      | 296   | 167   | 0.81   |
| Kingston  | SSDNow UV400           | 3      | 323     | 333   | 61    | 0.80   |
| Hyundai   | Unknown                | 5      | 6       | 291   | 0     | 0.80   |
| XSTAR     | Unknown                | 2      | 2       | 286   | 0     | 0.78   |
| GALAX     | Unknown                | 3      | 8       | 280   | 0     | 0.77   |
| Corsair   | Phison Driven SSDs     | 2      | 14      | 270   | 0     | 0.74   |
| TWINMOS   | Unknown                | 1      | 1       | 265   | 0     | 0.73   |
| SanDisk   | SanDisk based SSDs     | 33     | 351     | 302   | 22    | 0.72   |
| EAGET     | Unknown                | 1      | 1       | 259   | 0     | 0.71   |
| TAISU     | Unknown                | 2      | 2       | 254   | 0     | 0.70   |
| ZOTAC     | Unknown                | 3      | 4       | 253   | 0     | 0.69   |
| Team      | Silicon Motion base... | 5      | 18      | 252   | 0     | 0.69   |
| Palit     | Unknown                | 5      | 10      | 251   | 0     | 0.69   |
| Intel     | X18-M/X25-M/X25-V G... | 13     | 65      | 788   | 18    | 0.68   |
| Toshiba   | Unknown                | 57     | 239     | 267   | 12    | 0.68   |
| SanDisk   | Marvell based SanDi... | 74     | 1132    | 269   | 15    | 0.68   |
| G.Skill   | Unknown                | 1      | 1       | 241   | 0     | 0.66   |
| VENO S... | Unknown                | 1      | 1       | 241   | 0     | 0.66   |
| Intel     | 525 Series SSDs        | 3      | 5       | 365   | 1     | 0.66   |
| SanDisk   | SandForce Driven SSDs  | 6      | 323     | 277   | 20    | 0.65   |
| Micron    | Client SSDs            | 25     | 132     | 256   | 34    | 0.64   |
| SK hynix  | SATA SSDs              | 33     | 296     | 286   | 55    | 0.64   |
| Ramaxel   | Unknown                | 3      | 4       | 227   | 0     | 0.62   |
| BlitzWolf | Unknown                | 1      | 1       | 225   | 0     | 0.62   |
| ASUS      | Unknown                | 1      | 1       | 221   | 0     | 0.61   |
| Hoodisk   | Unknown                | 1      | 1       | 214   | 0     | 0.59   |
| Crucial   | BX/MX1/2/3/500, M5/... | 35     | 1163    | 279   | 33    | 0.58   |
| Intenso   | Phison Driven OEM SSDs | 4      | 93      | 214   | 1     | 0.57   |
| Transcend | JMicron/Maxiotek ba... | 4      | 8       | 218   | 126   | 0.57   |
| BlueRay   | Unknown                | 4      | 4       | 241   | 1     | 0.57   |
| Apple     | Unknown                | 4      | 8       | 380   | 298   | 0.57   |
| PNY       | Phison Driven SSDs     | 9      | 213     | 206   | 0     | 0.57   |
| JAMESD... | Unknown                | 1      | 1       | 206   | 0     | 0.56   |
| SanDisk   | Unknown                | 136    | 668     | 218   | 68    | 0.56   |
| Kingston  | Unknown                | 94     | 254     | 249   | 93    | 0.56   |
| Hoodisk   | Phison Driven OEM SSDs | 4      | 14      | 201   | 0     | 0.55   |
| Phison    | Unknown                | 14     | 19      | 203   | 1     | 0.55   |
| Crucial   | Indilinx Barefoot b... | 1      | 1       | 200   | 0     | 0.55   |
| Drevo     | Unknown                | 4      | 6       | 247   | 342   | 0.54   |
| Smartbuy  | Phison Driven SSDs     | 5      | 140     | 200   | 1     | 0.52   |
| Micron    | 5100 Pro / 52x0 / 5... | 4      | 6       | 209   | 1     | 0.52   |
| Intel     | Dell Certified Inte... | 1      | 1       | 188   | 0     | 0.52   |
| OCZ       | Intrepid 3000 SSDs     | 4      | 4       | 307   | 255   | 0.51   |
| AFOX      | Unknown                | 3      | 3       | 185   | 0     | 0.51   |
| Phison    | Driven OEM SSDs        | 10     | 105     | 182   | 0     | 0.50   |
| Detech    | Unknown                | 1      | 1       | 181   | 0     | 0.50   |
| Seagate   | Unknown                | 21     | 82      | 235   | 50    | 0.50   |
| Gigabyte  | Unknown                | 3      | 9       | 179   | 0     | 0.49   |
| Intel     | 53x and Pro 2500 Se... | 2      | 2       | 177   | 0     | 0.49   |
| Intel     | 311/313 Series SSDs    | 1      | 2       | 232   | 15    | 0.49   |
| KingFast  | Unknown                | 7      | 25      | 183   | 1     | 0.49   |
| Patriot   | Phison Driven SSDs     | 10     | 226     | 177   | 1     | 0.48   |
| Ramsta    | Silicon Motion base... | 2      | 2       | 171   | 0     | 0.47   |
| SPCC      | Phison Driven OEM SSDs | 8      | 500     | 199   | 58    | 0.46   |
| Crucial   | MX1/2/300, M5/600, ... | 2      | 15      | 905   | 81    | 0.46   |
| Intel     | S4510/S4610/S4500/S... | 14     | 58      | 204   | 54    | 0.46   |
| Micron    | BX/MX1/2/3/500, M5/... | 13     | 204     | 200   | 88    | 0.45   |
| Apacer    | SSDs                   | 1      | 1       | 162   | 0     | 0.44   |
| Intel     | Unknown                | 63     | 192     | 204   | 47    | 0.44   |
| Pioneer   | Unknown                | 6      | 12      | 160   | 0     | 0.44   |
| Plextor   | Unknown                | 36     | 102     | 168   | 1     | 0.43   |
| Patriot   | Unknown                | 22     | 53      | 239   | 58    | 0.43   |
| WDC       | Blue / Red / Green ... | 18     | 175     | 159   | 1     | 0.43   |
| Samgporse | Unknown                | 1      | 1       | 156   | 0     | 0.43   |
| Verbatim  | Unknown                | 6      | 22      | 160   | 47    | 0.43   |
| OCZ       | Unknown                | 9      | 13      | 729   | 158   | 0.42   |
| China     | Phison Driven OEM SSDs | 9      | 145     | 152   | 1     | 0.42   |
| Hajaan    | Unknown                | 1      | 2       | 151   | 0     | 0.42   |
| HP        | Unknown                | 18     | 91      | 158   | 1     | 0.41   |
| Innodisk  | 1ME3/3ME/3SE SSDs      | 1      | 1       | 150   | 0     | 0.41   |
| WDC       | Blue and Green SSDs    | 27     | 1455    | 156   | 2     | 0.41   |
| Silico... | Unknown                | 1      | 1       | 147   | 0     | 0.41   |
| SPCC      | Unknown                | 27     | 70      | 345   | 317   | 0.40   |
| imation   | Unknown                | 2      | 2       | 147   | 0     | 0.40   |
| Kingston  | Phison Driven SSDs     | 21     | 2132    | 156   | 1     | 0.40   |
| ZTC       | Unknown                | 2      | 4       | 144   | 0     | 0.40   |
| Plextor   | M3/M5 (Pro) Series ... | 3      | 16      | 211   | 65    | 0.40   |
| Plextor   | M3/M5/M6 Series SSDs   | 18     | 204     | 167   | 40    | 0.39   |
| Crucial   | Unknown                | 10     | 15      | 196   | 2     | 0.39   |
| MENGMI    | Unknown                | 1      | 1       | 139   | 0     | 0.38   |
| Kingston  | SSDNow UV400/500       | 11     | 144     | 146   | 49    | 0.38   |
| TCSUNBOW  | Unknown                | 5      | 11      | 136   | 0     | 0.37   |
| Lumino... | Unknown                | 2      | 2       | 135   | 0     | 0.37   |
| Crucial   | MX500 SSDs             | 2      | 76      | 134   | 0     | 0.37   |
| KingFast  | Silicon Motion base... | 4      | 37      | 136   | 83    | 0.37   |
| Goodram   | Unknown                | 30     | 150     | 140   | 1     | 0.37   |
| ADATA     | Unknown                | 71     | 372     | 213   | 137   | 0.36   |
| Team      | Unknown                | 33     | 111     | 156   | 4     | 0.35   |
| Micron    | Unknown                | 31     | 82      | 246   | 196   | 0.35   |
| BAITITON  | Unknown                | 5      | 7       | 161   | 1     | 0.35   |
| Chiprex   | Unknown                | 1      | 1       | 126   | 0     | 0.35   |
| Crucial   | Client SSDs            | 15     | 923     | 134   | 5     | 0.34   |
| Mushkin   | Silicon Motion base... | 6      | 12      | 123   | 0     | 0.34   |
| Hypertec  | Unknown                | 1      | 2       | 371   | 512   | 0.33   |
| Union ... | Unknown                | 1      | 8       | 120   | 0     | 0.33   |
| Londisk   | Unknown                | 4      | 15      | 119   | 0     | 0.33   |
| Samsung   | SandForce Driven SSDs  | 1      | 1       | 115   | 0     | 0.32   |
| Vaseky    | Unknown                | 17     | 22      | 120   | 6     | 0.32   |
| Goodram   | Phison Driven SSDs     | 6      | 72      | 113   | 0     | 0.31   |
| AMD       | Silicon Motion base... | 3      | 40      | 132   | 7     | 0.30   |
| SuperS... | Unknown                | 1      | 1       | 110   | 0     | 0.30   |
| Kston     | Unknown                | 1      | 5       | 109   | 0     | 0.30   |
| Intel     | 545s Series SSDs       | 8      | 79      | 116   | 1     | 0.30   |
| ADATA     | Silicon Motion base... | 19     | 435     | 124   | 30    | 0.29   |
| Zheino    | Silicon Motion base... | 1      | 3       | 106   | 0     | 0.29   |
| Marvell   | based SanDisk SSDs     | 1      | 1       | 105   | 0     | 0.29   |
| Smartbuy  | Unknown                | 12     | 19      | 104   | 0     | 0.29   |
| JASTER    | Unknown                | 1      | 2       | 103   | 0     | 0.28   |
| Transcend | Indilinx Barefoot b... | 1      | 1       | 309   | 2     | 0.28   |
| Lite-On   | Silicon Motion base... | 5      | 15      | 100   | 1     | 0.27   |
| Gigabyte  | Phison Driven SSDs     | 4      | 77      | 98    | 0     | 0.27   |
| TREKSTOR  | Unknown                | 3      | 4       | 127   | 39    | 0.27   |
| Kingmax   | Unknown                | 4      | 61      | 223   | 346   | 0.27   |
| KingSpec  | JMicron/Maxiotek ba... | 3      | 27      | 121   | 38    | 0.27   |
| Blackpcs  | Unknown                | 1      | 1       | 96    | 0     | 0.26   |
| JD        | Unknown                | 1      | 1       | 96    | 0     | 0.26   |
| HXY       | Unknown                | 1      | 1       | 96    | 0     | 0.26   |
| SK hynix  | Unknown                | 38     | 151     | 229   | 157   | 0.26   |
| UNIC2     | Unknown                | 1      | 2       | 95    | 0     | 0.26   |
| GOWE      | Unknown                | 1      | 1       | 284   | 2     | 0.26   |
| KingDian  | Silicon Motion base... | 10     | 71      | 96    | 2     | 0.25   |
| Lenovo    | Unknown                | 6      | 10      | 90    | 0     | 0.25   |
| GeIL      | Unknown                | 9      | 13      | 109   | 79    | 0.25   |
| KingSpec  | Unknown                | 43     | 154     | 108   | 27    | 0.25   |
| VisionTek | Unknown                | 1      | 2       | 88    | 0     | 0.24   |
| RZX       | Unknown                | 1      | 1       | 88    | 0     | 0.24   |
| Integral  | Unknown                | 3      | 14      | 88    | 0     | 0.24   |
| Apacer    | SDM5/5A/5A-M Series... | 3      | 13      | 179   | 33    | 0.24   |
| Transcend | Silicon Motion base... | 46     | 286     | 93    | 19    | 0.24   |
| Advantech | Unknown                | 6      | 7       | 86    | 0     | 0.24   |
| Apacer    | AS340 SSDs             | 3      | 52      | 88    | 1     | 0.24   |
| LDLC      | Unknown                | 12     | 38      | 110   | 4     | 0.24   |
| China     | Unknown                | 103    | 443     | 94    | 17    | 0.23   |
| Silicon   | Motion based OEM SSDs  | 3      | 4       | 84    | 0     | 0.23   |
| Ramsta    | Unknown                | 2      | 2       | 83    | 0     | 0.23   |
| Maxtor    | Unknown                | 2      | 14      | 83    | 0     | 0.23   |
| KingDian  | Unknown                | 15     | 51      | 98    | 173   | 0.23   |
| T-FORCE   | Unknown                | 4      | 11      | 83    | 0     | 0.23   |
| Nfortec   | Unknown                | 1      | 1       | 81    | 0     | 0.22   |
| BHT       | Unknown                | 9      | 20      | 81    | 0     | 0.22   |
| Apacer    | Unknown                | 15     | 134     | 82    | 24    | 0.22   |
| XUM       | Unknown                | 2      | 3       | 81    | 0     | 0.22   |
| Apple     | JMicron/Maxiotek ba... | 1      | 1       | 79    | 0     | 0.22   |
| PNY       | Unknown                | 36     | 85      | 112   | 85    | 0.21   |
| Transcend | SiliconMotion based... | 3      | 31      | 76    | 0     | 0.21   |
| Varro     | Unknown                | 2      | 2       | 76    | 0     | 0.21   |
| Lite-On   | Unknown                | 113    | 349     | 97    | 136   | 0.21   |
| AMD       | Unknown                | 9      | 48      | 87    | 22    | 0.21   |
| SPEED UP  | Unknown                | 1      | 1       | 75    | 0     | 0.21   |
| ASMedia   | Unknown                | 1      | 3       | 74    | 0     | 0.20   |
| e2e4      | Unknown                | 4      | 8       | 73    | 0     | 0.20   |
| Crucial   | Silicon Motion base... | 7      | 99      | 73    | 1     | 0.20   |
| Hikvision | Unknown                | 16     | 30      | 75    | 1     | 0.20   |
| Intenso   | Unknown                | 37     | 113     | 81    | 46    | 0.20   |
| ASENNO    | Unknown                | 2      | 4       | 70    | 0     | 0.19   |
| ORICO     | Unknown                | 4      | 4       | 114   | 1     | 0.19   |
| Patriot   | Silicon Motion base... | 4      | 16      | 108   | 44    | 0.19   |
| SUNEAST   | Unknown                | 5      | 5       | 70    | 0     | 0.19   |
| Mushkin   | Unknown                | 14     | 25      | 162   | 175   | 0.19   |
| ViperTeq  | Unknown                | 1      | 1       | 68    | 0     | 0.19   |
| Indilinx  | Unknown                | 7      | 9       | 68    | 1     | 0.19   |
| Gost      | Unknown                | 2      | 2       | 68    | 0     | 0.19   |
| INNOVA... | Unknown                | 10     | 20      | 73    | 2     | 0.19   |
| Star D... | Unknown                | 2      | 2       | 67    | 0     | 0.19   |
| OWC       | Unknown                | 4      | 8       | 67    | 0     | 0.18   |
| Seagate   | IronWolf 110 SATA SSD  | 2      | 5       | 66    | 0     | 0.18   |
| Seagate   | Nytro SATA SSD         | 3      | 10      | 65    | 0     | 0.18   |
| BRAVEE... | Unknown                | 2      | 2       | 65    | 0     | 0.18   |
| Colorful  | Unknown                | 7      | 14      | 78    | 89    | 0.18   |
| V-GeN     | Unknown                | 8      | 8       | 64    | 0     | 0.18   |
| Avant     | Unknown                | 1      | 1       | 64    | 0     | 0.18   |
| Golden... | Unknown                | 3      | 3       | 64    | 0     | 0.18   |
| SMI       | Unknown                | 7      | 7       | 63    | 280   | 0.17   |
| DOGFISH   | Unknown                | 4      | 4       | 62    | 0     | 0.17   |
| TAMMUZ    | Unknown                | 3      | 3       | 61    | 0     | 0.17   |
| Platinet  | Unknown                | 1      | 3       | 61    | 30    | 0.17   |
| TEXTORM   | Unknown                | 2      | 2       | 60    | 0     | 0.17   |
| Zheino    | Unknown                | 18     | 30      | 67    | 1     | 0.16   |
| Lexar     | Unknown                | 8      | 53      | 59    | 0     | 0.16   |
| AGI       | Unknown                | 1      | 1       | 59    | 0     | 0.16   |
| TEKET     | Unknown                | 1      | 2       | 59    | 0     | 0.16   |
| EYOTA     | Unknown                | 1      | 1       | 58    | 0     | 0.16   |
| Dogfish   | Unknown                | 7      | 15      | 57    | 0     | 0.16   |
| DeTech    | Unknown                | 1      | 1       | 57    | 0     | 0.16   |
| Neo Forza | Unknown                | 4      | 4       | 143   | 785   | 0.16   |
| ANACOMDA  | Unknown                | 1      | 1       | 57    | 0     | 0.16   |
| EZCOOL    | Unknown                | 1      | 1       | 56    | 0     | 0.15   |
| Super ... | Unknown                | 6      | 9       | 56    | 0     | 0.15   |
| GLOWAY    | Unknown                | 9      | 13      | 55    | 0     | 0.15   |
| Aoluska   | Unknown                | 1      | 1       | 54    | 0     | 0.15   |
| Drevo     | Silicon Motion base... | 1      | 9       | 206   | 12    | 0.15   |
| IPLEX     | Unknown                | 1      | 1       | 52    | 0     | 0.14   |
| Leven     | Unknown                | 7      | 27      | 53    | 1     | 0.14   |
| BIWIN     | Unknown                | 7      | 24      | 67    | 129   | 0.14   |
| BIOSTAR   | Unknown                | 6      | 8       | 50    | 0     | 0.14   |
| Faspeed   | Unknown                | 10     | 10      | 53    | 1     | 0.14   |
| HEORIADY  | Unknown                | 3      | 4       | 49    | 0     | 0.14   |
| Greenl... | Unknown                | 1      | 1       | 49    | 0     | 0.13   |
| Anobit    | Unknown                | 1      | 2       | 48    | 1     | 0.13   |
| Netac     | Unknown                | 25     | 91      | 51    | 34    | 0.13   |
| FORESEE   | Unknown                | 9      | 43      | 47    | 0     | 0.13   |
| RCESSD    | Unknown                | 1      | 2       | 46    | 0     | 0.13   |
| LENSEN    | Unknown                | 1      | 1       | 46    | 0     | 0.13   |
| Fujitsu   | Unknown                | 5      | 5       | 45    | 0     | 0.13   |
| Solid     | Unknown                | 2      | 5       | 48    | 1     | 0.13   |
| EMTEC     | Unknown                | 5      | 18      | 45    | 0     | 0.12   |
| MARSHAL   | Unknown                | 1      | 1       | 44    | 0     | 0.12   |
| FATTYDOVE | Unknown                | 1      | 1       | 44    | 0     | 0.12   |
| PRETEC    | Unknown                | 1      | 1       | 44    | 0     | 0.12   |
| XPG       | Unknown                | 1      | 2       | 44    | 0     | 0.12   |
| ADATA     | SiliconMotion based... | 1      | 40      | 44    | 1     | 0.12   |
| KLEVV     | Unknown                | 3      | 3       | 43    | 0     | 0.12   |
| TCSUNBOW  | Silicon Motion base... | 3      | 8       | 43    | 0     | 0.12   |
| Intenso   | Silicon Motion base... | 4      | 41      | 49    | 35    | 0.12   |
| Dogfish   | Silicon Motion base... | 3      | 15      | 43    | 0     | 0.12   |
| Intel     | SSD Pro 5400s Series   | 1      | 1       | 42    | 0     | 0.12   |
| Kingrich  | Unknown                | 5      | 6       | 139   | 2     | 0.11   |
| Fordisk   | Unknown                | 2      | 2       | 41    | 0     | 0.11   |
| QUMO      | Unknown                | 5      | 10      | 161   | 204   | 0.11   |
| Dogeish   | Unknown                | 1      | 1       | 40    | 0     | 0.11   |
| MediaR... | Unknown                | 1      | 1       | 39    | 0     | 0.11   |
| Goldkey   | Unknown                | 2      | 2       | 39    | 0     | 0.11   |
| Reeinno   | Unknown                | 2      | 2       | 37    | 0     | 0.10   |
| Foxline   | Unknown                | 12     | 22      | 82    | 47    | 0.10   |
| OSCOO     | Unknown                | 4      | 4       | 35    | 0     | 0.10   |
| oyunkey   | Unknown                | 1      | 2       | 215   | 66    | 0.10   |
| takeMS    | Unknown                | 1      | 1       | 34    | 0     | 0.10   |
| KIOXIA... | Unknown                | 2      | 17      | 33    | 0     | 0.09   |
| RECADATA  | Unknown                | 1      | 1       | 33    | 0     | 0.09   |
| Toshiba   | SG2 Series             | 1      | 1       | 32    | 0     | 0.09   |
| Kingston  | Silicon Motion base... | 4      | 50      | 31    | 0     | 0.09   |
| Innodisk  | 3IE2/3ME2/3MG2/3SE2... | 1      | 2       | 30    | 0     | 0.08   |
| ORTIAL    | Unknown                | 2      | 6       | 29    | 0     | 0.08   |
| KingPower | Unknown                | 1      | 1       | 29    | 0     | 0.08   |
| PUSKILL   | Unknown                | 1      | 1       | 28    | 0     | 0.08   |
| Wdstars   | Unknown                | 1      | 1       | 28    | 0     | 0.08   |
| SenDisk   | Unknown                | 1      | 1       | 27    | 0     | 0.08   |
| ShanDi... | Unknown                | 3      | 8       | 27    | 0     | 0.08   |
| Teclast   | Unknown                | 14     | 28      | 26    | 0     | 0.07   |
| HECTRON   | Unknown                | 1      | 1       | 26    | 0     | 0.07   |
| KINGSPEED | Unknown                | 1      | 1       | 26    | 0     | 0.07   |
| ExeGate   | Unknown                | 1      | 1       | 26    | 0     | 0.07   |
| Pasoul    | Unknown                | 1      | 1       | 25    | 0     | 0.07   |
| SNR       | Unknown                | 1      | 1       | 23    | 0     | 0.07   |
| Apple     | MacBook Air SSD        | 1      | 5       | 90    | 39    | 0.06   |
| XrayDisk  | Unknown                | 6      | 23      | 22    | 0     | 0.06   |
| tigo      | Unknown                | 3      | 3       | 22    | 0     | 0.06   |
| ELSKY     | Unknown                | 1      | 1       | 21    | 0     | 0.06   |
| Silicon   | Silicon Motion base... | 1      | 1       | 21    | 0     | 0.06   |
| TwinMOS   | Unknown                | 1      | 1       | 21    | 0     | 0.06   |
| XUNZHE    | Unknown                | 1      | 1       | 20    | 0     | 0.05   |
| GSemi     | Unknown                | 1      | 1       | 20    | 0     | 0.05   |
| DGM       | Unknown                | 1      | 1       | 18    | 0     | 0.05   |
| Hyperdisk | Unknown                | 1      | 1       | 18    | 0     | 0.05   |
| UMIS      | Unknown                | 1      | 1       | 18    | 0     | 0.05   |
| Win Me... | Unknown                | 3      | 3       | 17    | 0     | 0.05   |
| LDNDISK   | Unknown                | 1      | 1       | 16    | 0     | 0.05   |
| AEGO      | Unknown                | 1      | 3       | 16    | 0     | 0.04   |
| Leven     | Silicon Motion base... | 1      | 1       | 15    | 0     | 0.04   |
| Apacer    | SDM4 Series SSD Module | 1      | 6       | 52    | 6     | 0.04   |
| RevuAhn   | Unknown                | 1      | 1       | 14    | 0     | 0.04   |
| KINGBANK  | Unknown                | 2      | 4       | 14    | 0     | 0.04   |
| Seagate   | 600 Pro Series         | 1      | 1       | 14    | 0     | 0.04   |
| ADLINK    | Unknown                | 1      | 1       | 13    | 0     | 0.04   |
| Yeyian    | Unknown                | 2      | 4       | 13    | 0     | 0.04   |
| BR        | Unknown                | 2      | 2       | 12    | 0     | 0.03   |
| Silico... | Unknown                | 1      | 1       | 12    | 0     | 0.03   |
| Wicgtyp   | Unknown                | 1      | 1       | 12    | 0     | 0.03   |
| Gigastone | Unknown                | 2      | 2       | 12    | 0     | 0.03   |
| Dell      | Unknown                | 3      | 6       | 12    | 0     | 0.03   |
| MIXZA     | Unknown                | 1      | 1       | 11    | 0     | 0.03   |
| Micron    | MX1/2/300, M5/600, ... | 1      | 1       | 11    | 0     | 0.03   |
| Kingch... | Unknown                | 8      | 8       | 11    | 0     | 0.03   |
| Microtech | Unknown                | 2      | 2       | 10    | 0     | 0.03   |
| Golden... | Unknown                | 1      | 1       | 10    | 0     | 0.03   |
| Maximus   | Unknown                | 2      | 4       | 10    | 0     | 0.03   |
| Zozt      | Unknown                | 2      | 3       | 9     | 0     | 0.03   |
| Getrich   | Unknown                | 1      | 1       | 8     | 0     | 0.02   |
| Kingspeed | Unknown                | 1      | 1       | 8     | 0     | 0.02   |
| FASTDISK  | Unknown                | 6      | 6       | 7     | 0     | 0.02   |
| MAXIMUS   | Unknown                | 1      | 1       | 6     | 0     | 0.02   |
| GS Nan... | Unknown                | 1      | 1       | 6     | 0     | 0.02   |
| Kimtigo   | Unknown                | 1      | 2       | 6     | 0     | 0.02   |
| QNIX      | Unknown                | 1      | 1       | 6     | 0     | 0.02   |
| QIANGHE   | Unknown                | 1      | 1       | 73    | 12    | 0.02   |
| ShiJi     | Unknown                | 1      | 1       | 5     | 0     | 0.01   |
| S3+       | Unknown                | 3      | 3       | 140   | 16    | 0.01   |
| PHINOCOM  | Unknown                | 1      | 1       | 4     | 0     | 0.01   |
| Intel     | 540 Series SSDs        | 8      | 27      | 24    | 182   | 0.01   |
| Kross ... | Unknown                | 2      | 2       | 3     | 0     | 0.01   |
| Pacifi... | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| KODAK     | Unknown                | 2      | 2       | 3     | 0     | 0.01   |
| ShineDisk | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| i-Flas... | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| walram    | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| Iod       | Unknown                | 1      | 2       | 3     | 0     | 0.01   |
| TurXun    | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| Smart     | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| Pichau    | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| 2-Power   | Unknown                | 2      | 2       | 3     | 0     | 0.01   |
| Timetec   | Unknown                | 2      | 2       | 2     | 0     | 0.01   |
| MaxDig... | Unknown                | 2      | 2       | 23    | 333   | 0.01   |
| SOLIDATA  | Unknown                | 1      | 1       | 2420  | 1019  | 0.01   |
| INDMEM    | Unknown                | 4      | 4       | 2     | 0     | 0.01   |
| VSEVEN    | Unknown                | 1      | 1       | 2     | 0     | 0.01   |
| TMI       | Unknown                | 1      | 1       | 1     | 0     | 0.01   |
| ACPI      | Unknown                | 2      | 2       | 1     | 0     | 0.01   |
| Cactus    | Unknown                | 1      | 1       | 1     | 0     | 0.01   |
| DEPO      | Unknown                | 1      | 2       | 1     | 108   | 0.00   |
| Yunhai... | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| Mcpoint   | Unknown                | 1      | 1       | 6     | 3     | 0.00   |
| MidasF... | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| Philips   | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| Maxmemory | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Eluktro   | Unknown                | 1      | 1       | 806   | 1016  | 0.00   |
| ZHITAI    | Unknown                | 2      | 2       | 0     | 0     | 0.00   |
| Liren     | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| T-CREATE  | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| HP Phison | Unknown                | 2      | 2       | 399   | 1036  | 0.00   |
| UMAX      | Unknown                | 1      | 2       | 0     | 0     | 0.00   |
| DERLAR    | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| TEUTONS   | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Tronos    | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Bamba     | Unknown                | 1      | 1       | 60    | 249   | 0.00   |
| Myung     | Unknown                | 1      | 1       | 228   | 1015  | 0.00   |
| Dahua     | Unknown                | 2      | 2       | 0     | 0     | 0.00   |
| Goldenfir | Unknown                | 2      | 2       | 2     | 14    | 0.00   |
| AXIOMTEK  | Unknown                | 2      | 2       | 0     | 0     | 0.00   |
| EVM       | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| MicroD... | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| KINGPAN   | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| SandForce | Unknown                | 1      | 1       | 65    | 1018  | 0.00   |
| Innodisk  | 3IE2/3ME2/3MG2/3SE2... | 1      | 3       | 50    | 1010  | 0.00   |
| DOGGO     | Unknown                | 1      | 2       | 0     | 0     | 0.00   |
| KDATA     | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Xinsujie  | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| JIAWEI    | Unknown                | 1      | 1       | 47    | 3057  | 0.00   |
| SSSTC     | Unknown                | 2      | 4       | 6     | 1008  | 0.00   |
| DUEX      | Unknown                | 1      | 1       | 0     | 1007  | 0.00   |

SSD by Vendor
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF |
|-------------|--------|---------|-------|-------|------|
| OYUNKEY     | 1      | 1       | 1107  | 0     | 3.04   |
| HPE         | 3      | 3       | 831   | 0     | 2.28   |
| Radeon      | 1      | 4       | 778   | 0     | 2.13   |
| Micro Ce... | 1      | 1       | 722   | 0     | 1.98   |
| SandForce   | 3      | 3       | 828   | 478   | 1.92   |
| SMART       | 1      | 1       | 681   | 0     | 1.87   |
| Axiom       | 2      | 2       | 644   | 0     | 1.77   |
| Galaxy      | 1      | 1       | 578   | 0     | 1.58   |
| SATADOM     | 1      | 1       | 574   | 0     | 1.57   |
| OCZ         | 100    | 702     | 695   | 29    | 1.52   |
| Corsair     | 57     | 272     | 733   | 88    | 1.49   |
| MyDigita... | 4      | 10      | 495   | 0     | 1.36   |
| Intel       | 195    | 1009    | 548   | 57    | 1.17   |
| OWC         | 7      | 25      | 449   | 1     | 1.15   |
| Samsung     | 356    | 6839    | 420   | 6     | 1.12   |
| FCS         | 1      | 1       | 381   | 0     | 1.05   |
| CFD         | 3      | 3       | 375   | 0     | 1.03   |
| KingShare   | 2      | 2       | 373   | 0     | 1.02   |
| Apple       | 25     | 246     | 390   | 11    | 1.02   |
| addlink     | 2      | 4       | 359   | 0     | 0.98   |
| Toshiba     | 107    | 459     | 371   | 8     | 0.96   |
| Aura        | 1      | 1       | 310   | 0     | 0.85   |
| Innodisk    | 12     | 19      | 307   | 160   | 0.82   |
| Hyundai     | 5      | 6       | 291   | 0     | 0.80   |
| XSTAR       | 2      | 2       | 286   | 0     | 0.78   |
| GALAX       | 3      | 8       | 280   | 0     | 0.77   |
| TWINMOS     | 1      | 1       | 265   | 0     | 0.73   |
| EAGET       | 1      | 1       | 259   | 0     | 0.71   |
| TAISU       | 2      | 2       | 254   | 0     | 0.70   |
| ZOTAC       | 3      | 4       | 253   | 0     | 0.69   |
| Palit       | 5      | 10      | 251   | 0     | 0.69   |
| Mushkin     | 36     | 63      | 352   | 151   | 0.69   |
| Kingston    | 190    | 4369    | 279   | 27    | 0.66   |
| G.Skill     | 1      | 1       | 241   | 0     | 0.66   |
| VENO SCORP  | 1      | 1       | 241   | 0     | 0.66   |
| SanDisk     | 252    | 2478    | 261   | 31    | 0.65   |
| Ramaxel     | 3      | 4       | 227   | 0     | 0.62   |
| BlitzWolf   | 1      | 1       | 225   | 0     | 0.62   |
| Transcend   | 83     | 394     | 249   | 27    | 0.61   |
| ASUS        | 1      | 1       | 221   | 0     | 0.61   |
| Micron      | 92     | 503     | 265   | 105   | 0.60   |
| Crucial     | 84     | 2462    | 263   | 30    | 0.58   |
| BlueRay     | 4      | 4       | 241   | 1     | 0.57   |
| JAMESDONKEY | 1      | 1       | 206   | 0     | 0.56   |
| Hoodisk     | 5      | 15      | 202   | 0     | 0.55   |
| Phison      | 27     | 128     | 192   | 1     | 0.53   |
| SK hynix    | 71     | 447     | 267   | 89    | 0.51   |
| AFOX        | 3      | 3       | 185   | 0     | 0.51   |
| Detech      | 1      | 1       | 181   | 0     | 0.50   |
| Smartbuy    | 17     | 159     | 189   | 1     | 0.50   |
| Goodram     | 40     | 285     | 176   | 1     | 0.47   |
| PNY         | 45     | 298     | 180   | 25    | 0.47   |
| ADATA       | 115    | 1016    | 215   | 64    | 0.46   |
| Seagate     | 29     | 101     | 213   | 41    | 0.46   |
| Patriot     | 36     | 295     | 184   | 13    | 0.46   |
| SPCC        | 35     | 570     | 217   | 90    | 0.46   |
| Pioneer     | 6      | 12      | 160   | 0     | 0.44   |
| Plextor     | 66     | 343     | 179   | 27    | 0.43   |
| Samgporse   | 1      | 1       | 156   | 0     | 0.43   |
| Verbatim    | 6      | 22      | 160   | 47    | 0.43   |
| Hajaan      | 1      | 2       | 151   | 0     | 0.42   |
| KingFast    | 11     | 62      | 155   | 50    | 0.41   |
| WDC         | 51     | 1642    | 158   | 3     | 0.41   |
| HP          | 18     | 91      | 158   | 1     | 0.41   |
| Silicon ... | 1      | 1       | 147   | 0     | 0.41   |
| imation     | 2      | 2       | 147   | 0     | 0.40   |
| Team        | 38     | 129     | 170   | 4     | 0.40   |
| ZTC         | 2      | 4       | 144   | 0     | 0.40   |
| MENGMI      | 1      | 1       | 139   | 0     | 0.38   |
| LuminouTek  | 2      | 2       | 135   | 0     | 0.37   |
| BAITITON    | 5      | 7       | 161   | 1     | 0.35   |
| Ramsta      | 4      | 4       | 127   | 0     | 0.35   |
| Chiprex     | 1      | 1       | 126   | 0     | 0.35   |
| Hypertec    | 1      | 2       | 371   | 512   | 0.33   |
| Union Me... | 1      | 8       | 120   | 0     | 0.33   |
| Intenso     | 45     | 247     | 126   | 27    | 0.33   |
| Londisk     | 4      | 15      | 119   | 0     | 0.33   |
| Vaseky      | 17     | 22      | 120   | 6     | 0.32   |
| Drevo       | 5      | 15      | 222   | 144   | 0.30   |
| SuperSSpeed | 1      | 1       | 110   | 0     | 0.30   |
| Kston       | 1      | 5       | 109   | 0     | 0.30   |
| Gigabyte    | 7      | 86      | 106   | 0     | 0.29   |
| Marvell     | 1      | 1       | 105   | 0     | 0.29   |
| JASTER      | 1      | 2       | 103   | 0     | 0.28   |
| China       | 112    | 588     | 109   | 13    | 0.28   |
| TREKSTOR    | 3      | 4       | 127   | 39    | 0.27   |
| Kingmax     | 4      | 61      | 223   | 346   | 0.27   |
| TCSUNBOW    | 8      | 19      | 97    | 0     | 0.27   |
| Blackpcs    | 1      | 1       | 96    | 0     | 0.26   |
| JD          | 1      | 1       | 96    | 0     | 0.26   |
| HXY         | 1      | 1       | 96    | 0     | 0.26   |
| UNIC2       | 1      | 2       | 95    | 0     | 0.26   |
| GOWE        | 1      | 1       | 284   | 2     | 0.26   |
| KingSpec    | 46     | 181     | 110   | 29    | 0.25   |
| AMD         | 12     | 88      | 107   | 15    | 0.25   |
| Lenovo      | 6      | 10      | 90    | 0     | 0.25   |
| GeIL        | 9      | 13      | 109   | 79    | 0.25   |
| VisionTek   | 1      | 2       | 88    | 0     | 0.24   |
| KingDian    | 25     | 122     | 97    | 74    | 0.24   |
| RZX         | 1      | 1       | 88    | 0     | 0.24   |
| Integral    | 3      | 14      | 88    | 0     | 0.24   |
| Advantech   | 6      | 7       | 86    | 0     | 0.24   |
| LDLC        | 12     | 38      | 110   | 4     | 0.24   |
| Maxtor      | 2      | 14      | 83    | 0     | 0.23   |
| T-FORCE     | 4      | 11      | 83    | 0     | 0.23   |
| Nfortec     | 1      | 1       | 81    | 0     | 0.22   |
| BHT         | 9      | 20      | 81    | 0     | 0.22   |
| Apacer      | 23     | 206     | 89    | 18    | 0.22   |
| XUM         | 2      | 3       | 81    | 0     | 0.22   |
| Lite-On     | 118    | 364     | 97    | 131   | 0.21   |
| Varro       | 2      | 2       | 76    | 0     | 0.21   |
| SPEED UP    | 1      | 1       | 75    | 0     | 0.21   |
| ASMedia     | 1      | 3       | 74    | 0     | 0.20   |
| e2e4        | 4      | 8       | 73    | 0     | 0.20   |
| Hikvision   | 16     | 30      | 75    | 1     | 0.20   |
| Silicon     | 4      | 5       | 72    | 0     | 0.20   |
| ASENNO      | 2      | 4       | 70    | 0     | 0.19   |
| ORICO       | 4      | 4       | 114   | 1     | 0.19   |
| SUNEAST     | 5      | 5       | 70    | 0     | 0.19   |
| ViperTeq    | 1      | 1       | 68    | 0     | 0.19   |
| Indilinx    | 7      | 9       | 68    | 1     | 0.19   |
| Gost        | 2      | 2       | 68    | 0     | 0.19   |
| INNOVATI... | 10     | 20      | 73    | 2     | 0.19   |
| Star Drive  | 2      | 2       | 67    | 0     | 0.19   |
| BRAVEEAGLE  | 2      | 2       | 65    | 0     | 0.18   |
| Colorful    | 7      | 14      | 78    | 89    | 0.18   |
| V-GeN       | 8      | 8       | 64    | 0     | 0.18   |
| Avant       | 1      | 1       | 64    | 0     | 0.18   |
| Golden m... | 3      | 3       | 64    | 0     | 0.18   |
| Zheino      | 19     | 33      | 71    | 1     | 0.17   |
| SMI         | 7      | 7       | 63    | 280   | 0.17   |
| DOGFISH     | 4      | 4       | 62    | 0     | 0.17   |
| TAMMUZ      | 3      | 3       | 61    | 0     | 0.17   |
| Platinet    | 1      | 3       | 61    | 30    | 0.17   |
| TEXTORM     | 2      | 2       | 60    | 0     | 0.17   |
| Lexar       | 8      | 53      | 59    | 0     | 0.16   |
| AGI         | 1      | 1       | 59    | 0     | 0.16   |
| TEKET       | 1      | 2       | 59    | 0     | 0.16   |
| EYOTA       | 1      | 1       | 58    | 0     | 0.16   |
| DeTech      | 1      | 1       | 57    | 0     | 0.16   |
| Neo Forza   | 4      | 4       | 143   | 785   | 0.16   |
| ANACOMDA    | 1      | 1       | 57    | 0     | 0.16   |
| EZCOOL      | 1      | 1       | 56    | 0     | 0.15   |
| Super Ta... | 6      | 9       | 56    | 0     | 0.15   |
| GLOWAY      | 9      | 13      | 55    | 0     | 0.15   |
| Aoluska     | 1      | 1       | 54    | 0     | 0.15   |
| IPLEX       | 1      | 1       | 52    | 0     | 0.14   |
| BIWIN       | 7      | 24      | 67    | 129   | 0.14   |
| Leven       | 8      | 28      | 52    | 1     | 0.14   |
| Dogfish     | 10     | 30      | 50    | 0     | 0.14   |
| BIOSTAR     | 6      | 8       | 50    | 0     | 0.14   |
| Faspeed     | 10     | 10      | 53    | 1     | 0.14   |
| HEORIADY    | 3      | 4       | 49    | 0     | 0.14   |
| Greenliant  | 1      | 1       | 49    | 0     | 0.13   |
| Anobit      | 1      | 2       | 48    | 1     | 0.13   |
| Netac       | 25     | 91      | 51    | 34    | 0.13   |
| FORESEE     | 9      | 43      | 47    | 0     | 0.13   |
| RCESSD      | 1      | 2       | 46    | 0     | 0.13   |
| LENSEN      | 1      | 1       | 46    | 0     | 0.13   |
| Fujitsu     | 5      | 5       | 45    | 0     | 0.13   |
| Solid       | 2      | 5       | 48    | 1     | 0.13   |
| EMTEC       | 5      | 18      | 45    | 0     | 0.12   |
| MARSHAL     | 1      | 1       | 44    | 0     | 0.12   |
| FATTYDOVE   | 1      | 1       | 44    | 0     | 0.12   |
| PRETEC      | 1      | 1       | 44    | 0     | 0.12   |
| XPG         | 1      | 2       | 44    | 0     | 0.12   |
| KLEVV       | 3      | 3       | 43    | 0     | 0.12   |
| Kingrich    | 5      | 6       | 139   | 2     | 0.11   |
| Fordisk     | 2      | 2       | 41    | 0     | 0.11   |
| QUMO        | 5      | 10      | 161   | 204   | 0.11   |
| Dogeish     | 1      | 1       | 40    | 0     | 0.11   |
| MediaRange  | 1      | 1       | 39    | 0     | 0.11   |
| Goldkey     | 2      | 2       | 39    | 0     | 0.11   |
| Reeinno     | 2      | 2       | 37    | 0     | 0.10   |
| Foxline     | 12     | 22      | 82    | 47    | 0.10   |
| OSCOO       | 4      | 4       | 35    | 0     | 0.10   |
| oyunkey     | 1      | 2       | 215   | 66    | 0.10   |
| takeMS      | 1      | 1       | 34    | 0     | 0.10   |
| KIOXIA-E... | 2      | 17      | 33    | 0     | 0.09   |
| RECADATA    | 1      | 1       | 33    | 0     | 0.09   |
| ORTIAL      | 2      | 6       | 29    | 0     | 0.08   |
| KingPower   | 1      | 1       | 29    | 0     | 0.08   |
| PUSKILL     | 1      | 1       | 28    | 0     | 0.08   |
| Wdstars     | 1      | 1       | 28    | 0     | 0.08   |
| SenDisk     | 1      | 1       | 27    | 0     | 0.08   |
| ShanDianZhe | 3      | 8       | 27    | 0     | 0.08   |
| Teclast     | 14     | 28      | 26    | 0     | 0.07   |
| HECTRON     | 1      | 1       | 26    | 0     | 0.07   |
| KINGSPEED   | 1      | 1       | 26    | 0     | 0.07   |
| ExeGate     | 1      | 1       | 26    | 0     | 0.07   |
| Pasoul      | 1      | 1       | 25    | 0     | 0.07   |
| SNR         | 1      | 1       | 23    | 0     | 0.07   |
| XrayDisk    | 6      | 23      | 22    | 0     | 0.06   |
| tigo        | 3      | 3       | 22    | 0     | 0.06   |
| ELSKY       | 1      | 1       | 21    | 0     | 0.06   |
| TwinMOS     | 1      | 1       | 21    | 0     | 0.06   |
| XUNZHE      | 1      | 1       | 20    | 0     | 0.05   |
| GSemi       | 1      | 1       | 20    | 0     | 0.05   |
| DGM         | 1      | 1       | 18    | 0     | 0.05   |
| Hyperdisk   | 1      | 1       | 18    | 0     | 0.05   |
| UMIS        | 1      | 1       | 18    | 0     | 0.05   |
| Win Memory  | 3      | 3       | 17    | 0     | 0.05   |
| LDNDISK     | 1      | 1       | 16    | 0     | 0.05   |
| AEGO        | 1      | 3       | 16    | 0     | 0.04   |
| RevuAhn     | 1      | 1       | 14    | 0     | 0.04   |
| KINGBANK    | 2      | 4       | 14    | 0     | 0.04   |
| ADLINK      | 1      | 1       | 13    | 0     | 0.04   |
| Yeyian      | 2      | 4       | 13    | 0     | 0.04   |
| BR          | 2      | 2       | 12    | 0     | 0.03   |
| Silicon ... | 1      | 1       | 12    | 0     | 0.03   |
| Wicgtyp     | 1      | 1       | 12    | 0     | 0.03   |
| Gigastone   | 2      | 2       | 12    | 0     | 0.03   |
| Dell        | 3      | 6       | 12    | 0     | 0.03   |
| MIXZA       | 1      | 1       | 11    | 0     | 0.03   |
| Kingchuxing | 8      | 8       | 11    | 0     | 0.03   |
| Microtech   | 2      | 2       | 10    | 0     | 0.03   |
| Goldendisk  | 1      | 1       | 10    | 0     | 0.03   |
| Maximus     | 2      | 4       | 10    | 0     | 0.03   |
| Zozt        | 2      | 3       | 9     | 0     | 0.03   |
| Getrich     | 1      | 1       | 8     | 0     | 0.02   |
| Kingspeed   | 1      | 1       | 8     | 0     | 0.02   |
| FASTDISK    | 6      | 6       | 7     | 0     | 0.02   |
| MAXIMUS     | 1      | 1       | 6     | 0     | 0.02   |
| GS Nanotech | 1      | 1       | 6     | 0     | 0.02   |
| Kimtigo     | 1      | 2       | 6     | 0     | 0.02   |
| QNIX        | 1      | 1       | 6     | 0     | 0.02   |
| QIANGHE     | 1      | 1       | 73    | 12    | 0.02   |
| ShiJi       | 1      | 1       | 5     | 0     | 0.01   |
| S3+         | 3      | 3       | 140   | 16    | 0.01   |
| PHINOCOM    | 1      | 1       | 4     | 0     | 0.01   |
| Kross El... | 2      | 2       | 3     | 0     | 0.01   |
| Pacific Sun | 1      | 1       | 3     | 0     | 0.01   |
| KODAK       | 2      | 2       | 3     | 0     | 0.01   |
| ShineDisk   | 1      | 1       | 3     | 0     | 0.01   |
| i-FlashDisk | 1      | 1       | 3     | 0     | 0.01   |
| walram      | 1      | 1       | 3     | 0     | 0.01   |
| Iod         | 1      | 2       | 3     | 0     | 0.01   |
| TurXun      | 1      | 1       | 3     | 0     | 0.01   |
| Smart       | 1      | 1       | 3     | 0     | 0.01   |
| Pichau      | 1      | 1       | 3     | 0     | 0.01   |
| 2-Power     | 2      | 2       | 3     | 0     | 0.01   |
| Timetec     | 2      | 2       | 2     | 0     | 0.01   |
| MaxDigital  | 2      | 2       | 23    | 333   | 0.01   |
| SOLIDATA    | 1      | 1       | 2420  | 1019  | 0.01   |
| INDMEM      | 4      | 4       | 2     | 0     | 0.01   |
| VSEVEN      | 1      | 1       | 2     | 0     | 0.01   |
| TMI         | 1      | 1       | 1     | 0     | 0.01   |
| ACPI        | 2      | 2       | 1     | 0     | 0.01   |
| Cactus      | 1      | 1       | 1     | 0     | 0.01   |
| DEPO        | 1      | 2       | 1     | 108   | 0.00   |
| Yunhaitian  | 1      | 1       | 1     | 0     | 0.00   |
| Mcpoint     | 1      | 1       | 6     | 3     | 0.00   |
| MidasForce  | 1      | 1       | 1     | 0     | 0.00   |
| Philips     | 1      | 1       | 1     | 0     | 0.00   |
| Maxmemory   | 1      | 1       | 0     | 0     | 0.00   |
| Eluktro     | 1      | 1       | 806   | 1016  | 0.00   |
| ZHITAI      | 2      | 2       | 0     | 0     | 0.00   |
| Liren       | 1      | 1       | 0     | 0     | 0.00   |
| T-CREATE    | 1      | 1       | 0     | 0     | 0.00   |
| HP Phison   | 2      | 2       | 399   | 1036  | 0.00   |
| UMAX        | 1      | 2       | 0     | 0     | 0.00   |
| DERLAR      | 1      | 1       | 0     | 0     | 0.00   |
| TEUTONS     | 1      | 1       | 0     | 0     | 0.00   |
| Tronos      | 1      | 1       | 0     | 0     | 0.00   |
| Bamba       | 1      | 1       | 60    | 249   | 0.00   |
| Myung       | 1      | 1       | 228   | 1015  | 0.00   |
| Dahua       | 2      | 2       | 0     | 0     | 0.00   |
| Goldenfir   | 2      | 2       | 2     | 14    | 0.00   |
| AXIOMTEK    | 2      | 2       | 0     | 0     | 0.00   |
| EVM         | 1      | 1       | 0     | 0     | 0.00   |
| MicroDream  | 1      | 1       | 0     | 0     | 0.00   |
| KINGPAN     | 1      | 1       | 0     | 0     | 0.00   |
| DOGGO       | 1      | 2       | 0     | 0     | 0.00   |
| KDATA       | 1      | 1       | 0     | 0     | 0.00   |
| Xinsujie    | 1      | 1       | 0     | 0     | 0.00   |
| JIAWEI      | 1      | 1       | 47    | 3057  | 0.00   |
| SSSTC       | 2      | 4       | 6     | 1008  | 0.00   |
| DUEX        | 1      | 1       | 0     | 1007  | 0.00   |

NVME by Model
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

See full list of tested NVMe samples in the Appendix 5 ([All_NVMe.md](/All_NVMe.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| Intel     | MEMPEK1J016GAD     | 16 GB  | 2       | 5999  | 0     | 16.44  |
| Intel     | H10 HBRPEKNX020... | 32 GB  | 12      | 2306  | 0     | 6.32   |
| Intel     | MT1600KEXUV        | 1.6 TB | 1       | 1720  | 0     | 4.71   |
| Samsung   | MZVLV512HCJH-00000 | 512 GB | 1       | 1710  | 0     | 4.69   |
| Intel     | SSDPEDMW800G4      | 800 GB | 1       | 1422  | 0     | 3.90   |
| Intel     | SSDPEDMW012T4      | 1.2 TB | 2       | 1323  | 0     | 3.63   |
| Intel     | SSDPE7KX020T7      | 2 TB   | 1       | 1218  | 0     | 3.34   |
| Intel     | H10 HBRPEKNX020... | 32 GB  | 2       | 993   | 0     | 2.72   |
| Intel     | SSDPEKKF256G7H     | 256 GB | 11      | 1020  | 92    | 2.69   |
| Intel     | SSDPEDME016T4      | 1.6 TB | 1       | 906   | 0     | 2.48   |
| Intel     | SSDPEKKF512G7H     | 512 GB | 4       | 905   | 0     | 2.48   |
| ZOTAC     | ZTSSDPG3-480G-GE   | 480 GB | 1       | 899   | 0     | 2.47   |
| Avant     | 500GB M.2 NVME     | 500 GB | 1       | 891   | 0     | 2.44   |
| Corsair   | Force MP500        | 480 GB | 1       | 869   | 0     | 2.38   |
| AMD       | R5MP120G8          | 120 GB | 1       | 856   | 0     | 2.35   |
| Samsung   | SSD 983 DCT 1.92TB | 1.9 TB | 2       | 850   | 0     | 2.33   |
| Intel     | SSDPEKKW512G7      | 512 GB | 20      | 919   | 51    | 2.27   |
| Transcend | TS128GMTE850       | 128 GB | 1       | 745   | 0     | 2.04   |
| Samsung   | SSD 950 PRO        | 512 GB | 36      | 711   | 0     | 1.95   |
| Samsung   | SSD 950 PRO        | 256 GB | 13      | 702   | 0     | 1.92   |
| Intel     | SSDPE21K375GA      | 375 GB | 1       | 696   | 0     | 1.91   |
| Toshiba   | RD400              | 1 TB   | 2       | 685   | 0     | 1.88   |
| Intel     | MEMPEK1W032GA      | 32 GB  | 3       | 674   | 0     | 1.85   |
| Samsung   | MZWLL1T6HAJQ-00005 | 1.6 TB | 4       | 673   | 0     | 1.85   |
| Intel     | SSDPE2MX450G7      | 450 GB | 4       | 658   | 0     | 1.80   |
| Intel     | SSDPEKKF256G7L     | 256 GB | 19      | 833   | 63    | 1.80   |
| Samsung   | MZVPV256HDGL-000H1 | 256 GB | 6       | 650   | 0     | 1.78   |
| Samsung   | MZWLL3T2HMJP-00003 | 3.2 TB | 1       | 648   | 0     | 1.78   |
| WDC       | WDS512G1X0C-00ENX0 | 512 GB | 10      | 647   | 0     | 1.78   |
| Toshiba   | THNSN5256GPU7      | 256 GB | 8       | 636   | 0     | 1.74   |
| Kingston  | SKC1000240G        | 240 GB | 2       | 629   | 0     | 1.72   |
| Samsung   | MZVPV512HDGL-00000 | 512 GB | 6       | 627   | 0     | 1.72   |
| Corsair   | Force MP500        | 120 GB | 8       | 622   | 0     | 1.71   |
| Samsung   | MZVPV256HDGL-00000 | 256 GB | 12      | 620   | 0     | 1.70   |
| Intel     | SSDPEKKW256G7      | 256 GB | 45      | 746   | 44    | 1.68   |
| Toshiba   | KBG20ZMS256G NVMe  | 256 GB | 2       | 605   | 0     | 1.66   |
| Intel     | SSDPED1K375GA      | 375 GB | 1       | 603   | 0     | 1.65   |
| Patriot   | Hellfire M2        | 240 GB | 1       | 598   | 0     | 1.64   |
| Intel     | SSDPEDMD400G4      | 400 GB | 1       | 595   | 0     | 1.63   |
| WDC       | WUS3BA176C7P3E3    | 7.6 TB | 1       | 589   | 0     | 1.62   |
| Toshiba   | THNSN5512GPUK      | 512 GB | 1       | 563   | 0     | 1.54   |
| Toshiba   | KXG50PNV2T04 1.6TB | 1.6 TB | 1       | 553   | 0     | 1.52   |
| Intel     | SSDPEDMW012T4D ... | 1.2 TB | 1       | 552   | 0     | 1.51   |
| Intel     | SSDPEKKF360G7H     | 360 GB | 7       | 550   | 0     | 1.51   |
| Toshiba   | RD400              | 128 GB | 1       | 536   | 0     | 1.47   |
| SPCC      | M.2 PCIe SSD       | 128 GB | 1       | 529   | 0     | 1.45   |
| Toshiba   | THNSN51T02DUK NVMe | 1 TB   | 8       | 528   | 0     | 1.45   |
| Toshiba   | KXG50PNV2T04 NVMe  | 2 TB   | 4       | 494   | 0     | 1.36   |
| ADATA     | SX7000NP           | 128 GB | 1       | 483   | 0     | 1.33   |
| Kingston  | SKC1000480G        | 480 GB | 3       | 481   | 0     | 1.32   |
| Corsair   | Force MP500        | 240 GB | 9       | 593   | 2     | 1.32   |
| Intel     | SSDPEKKW128G7      | 128 GB | 10      | 881   | 2     | 1.28   |
| Intel     | SSDPE21D480GA      | 480 GB | 6       | 466   | 0     | 1.28   |
| Samsung   | MZVPV512HDGL-000H1 | 512 GB | 4       | 461   | 0     | 1.26   |
| Toshiba   | THNSN5256GPUK NVMe | 256 GB | 11      | 446   | 0     | 1.22   |
| Phison    | Neutron NX500      | 800 GB | 2       | 439   | 0     | 1.20   |
| Intel     | SSDPEKKF512G7L     | 512 GB | 4       | 439   | 0     | 1.20   |
| Toshiba   | THNSN5512GPU7 NVMe | 512 GB | 3       | 432   | 0     | 1.19   |
| Samsung   | MZVKV512HAJH-000L1 | 512 GB | 9       | 426   | 0     | 1.17   |
| Micron    | MTFDHAL3T2MCE-1... | 3.2 TB | 1       | 424   | 0     | 1.16   |
| Toshiba   | THNSN5512GPU7      | 512 GB | 4       | 422   | 0     | 1.16   |
| Samsung   | MS1PC2DD3ORA3.2T   | 3.2 TB | 1       | 416   | 0     | 1.14   |
| ADATA     | SX8200NP           | 480 GB | 7       | 414   | 0     | 1.14   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 2       | 410   | 0     | 1.12   |
| Samsung   | PM951 NVMe         | 512 GB | 8       | 408   | 0     | 1.12   |
| Toshiba   | THNSN5512GPUK NVMe | 512 GB | 28      | 404   | 0     | 1.11   |
| Lite-On   | CAZ-82512-Q11 NVMe | 512 GB | 1       | 400   | 0     | 1.10   |
| Intel     | SSDPEKKF128G7      | 128 GB | 1       | 778   | 1     | 1.07   |
| Intel     | SSDPED1D480GA      | 480 GB | 3       | 387   | 0     | 1.06   |
| Smartbuy  | m.2 PS5013-2280T   | 512 GB | 1       | 385   | 0     | 1.06   |
| SanDisk   | A400 NVMe          | 512 GB | 2       | 382   | 0     | 1.05   |
| Toshiba   | KXG50ZNV512G NVMe  | 512 GB | 40      | 371   | 0     | 1.02   |
| Gigabyte  | GP-ASACNE2100TTTDR | 1 TB   | 1       | 367   | 0     | 1.01   |
| Intel     | HBRPEKNX0202ACO    | 32 GB  | 1       | 365   | 0     | 1.00   |
| Plextor   | PX-512M8PeGN       | 512 GB | 1       | 362   | 0     | 0.99   |
| Samsung   | MZVLV512HCJH-000L2 | 512 GB | 1       | 361   | 0     | 0.99   |
| Intel     | SSDPE2MX012T7      | 1.2 TB | 4       | 358   | 0     | 0.98   |
| ADATA     | SX7000NP           | 256 GB | 1       | 354   | 0     | 0.97   |
| Phison    | Asura NVME         | 2 TB   | 1       | 353   | 0     | 0.97   |
| HP        | SSD EX920          | 512 GB | 12      | 353   | 0     | 0.97   |
| Toshiba   | KXG50ZNV1T02 NVMe  | 1 TB   | 17      | 348   | 0     | 0.96   |
| Samsung   | MZ1LV960HCJH-000MU | 960 GB | 1       | 346   | 0     | 0.95   |
| ADATA     | SX6000NP           | 128 GB | 6       | 413   | 195   | 0.95   |
| Seagate   | BarraCuda 510 S... | 500 GB | 2       | 341   | 0     | 0.94   |
| Intel     | MEMPEK1J016GA      | 16 GB  | 9       | 340   | 0     | 0.93   |
| addlink   | M.2 PCIE G3x4 NVMe | 2 TB   | 9       | 339   | 0     | 0.93   |
| SSSTC     | CL1-3D256          | 256 GB | 1       | 338   | 0     | 0.93   |
| Intel     | HBRPEKNX0202AC     | 512 GB | 1       | 336   | 0     | 0.92   |
| Transcend | TS512GMTE220S      | 512 GB | 9       | 336   | 0     | 0.92   |
| Samsung   | PM951 NVMe         | 256 GB | 9       | 333   | 0     | 0.91   |
| Toshiba   | KXG50PNV1T02 NVMe  | 1 TB   | 2       | 328   | 0     | 0.90   |
| Plextor   | PX-1TM9PG +        | 1 TB   | 1       | 326   | 0     | 0.89   |
| WDC       | WDS256G1X0C-00ENX0 | 256 GB | 8       | 323   | 0     | 0.89   |
| Patriot   | Scorch M2          | 512 GB | 3       | 321   | 0     | 0.88   |
| Samsung   | MZVKW512HMJP-00000 | 512 GB | 7       | 319   | 0     | 0.87   |
| Toshiba   | RC100              | 120 GB | 1       | 317   | 0     | 0.87   |
| Toshiba   | KXG5AZNV256G       | 256 GB | 10      | 316   | 0     | 0.87   |
| Intel     | SSDPED1D280GA      | 280 GB | 4       | 316   | 0     | 0.87   |
| Toshiba   | KXG5AZNV1T02       | 1 TB   | 4       | 315   | 0     | 0.86   |
| Transcend | TS256GMTE820       | 256 GB | 1       | 308   | 0     | 0.84   |
| WDC       | WDS500G2X0C-00L350 | 500 GB | 21      | 306   | 0     | 0.84   |
| Samsung   | MZVLB256HAHQ-000H2 | 256 GB | 1       | 305   | 0     | 0.84   |
| Plextor   | PX-512M9PeG        | 512 GB | 3       | 305   | 0     | 0.84   |
| Samsung   | MZVPV128HDGM-000H1 | 128 GB | 1       | 304   | 0     | 0.83   |
| Toshiba   | KXG50ZNV256G NVMe  | 256 GB | 30      | 303   | 0     | 0.83   |
| Samsung   | MZVPV128HDGM-00000 | 128 GB | 9       | 302   | 0     | 0.83   |
| Toshiba   | THNSF5256GPUK      | 256 GB | 4       | 297   | 0     | 0.82   |
| Phison    | E12-512G-PHISON... | 512 GB | 2       | 297   | 0     | 0.82   |
| Samsung   | MZVLV128HCGR-00000 | 128 GB | 2       | 294   | 0     | 0.81   |
| Phison    | Reletech M.2 SSD   | 512 GB | 1       | 293   | 0     | 0.80   |
| WDC       | WDS250G2X0C-00L350 | 250 GB | 11      | 284   | 0     | 0.78   |
| Intel     | MEMPEI1J016GAL     | 16 GB  | 1       | 284   | 0     | 0.78   |
| Dell      | Express Flash N... | 1.6 TB | 1       | 284   | 0     | 0.78   |
| Intel     | SSDPEKKW010T7      | 1 TB   | 4       | 863   | 7     | 0.75   |
| XPG       | GAMMIX S50         | 1 TB   | 6       | 273   | 0     | 0.75   |
| Goodram   | 120GB              | 120 GB | 1       | 271   | 0     | 0.74   |
| Intel     | SSDPEK1W120GA      | 118 GB | 1       | 271   | 0     | 0.74   |
| Samsung   | MZFLV512HCJH-000MV | 512 GB | 4       | 269   | 0     | 0.74   |
| Lite-On   | CA1-8D256-HP       | 256 GB | 2       | 269   | 0     | 0.74   |
| XPG       | GAMMIX S11         | 480 GB | 6       | 264   | 0     | 0.73   |
| Samsung   | MZVLV256HCHP-000L2 | 256 GB | 5       | 263   | 0     | 0.72   |
| Kingston  | SKC2000M8500G      | 500 GB | 2       | 262   | 0     | 0.72   |
| Silico... | Asgard AN3 2TNV... | 2 TB   | 2       | 259   | 0     | 0.71   |
| Intel     | MEMPEK1J016GAH     | 16 GB  | 3       | 257   | 0     | 0.71   |
| Toshiba   | THNSN51T02DU7 NVMe | 1 TB   | 3       | 255   | 0     | 0.70   |
| Toshiba   | THNSF5256GPUK      | 256 GB | 1       | 249   | 0     | 0.68   |
| Gigabyte  | GP-ASM2NE6100TTTD  | 1 TB   | 11      | 249   | 0     | 0.68   |
| Toshiba   | THNSN51T02DUK      | 1 TB   | 2       | 246   | 0     | 0.68   |
| Samsung   | MZSLW1T0HMLH-000L1 | 1 TB   | 3       | 246   | 0     | 0.67   |
| Toshiba   | THNSN5256GPUK      | 256 GB | 5       | 245   | 0     | 0.67   |
| Intel     | SSDPEKNW020T9      | 2 TB   | 3       | 245   | 0     | 0.67   |
| WDC       | WDS100T2X0C-00L350 | 1 TB   | 8       | 245   | 0     | 0.67   |
| Lite-On   | CL1-4D128          | 128 GB | 1       | 244   | 0     | 0.67   |
| Toshiba   | THNSF5512GPUK      | 512 GB | 6       | 240   | 0     | 0.66   |
| ADATA     | SX8200NP           | 960 GB | 3       | 239   | 0     | 0.66   |
| Mushkin   | MKNSSDPL2TB-D8     | 2 TB   | 1       | 238   | 0     | 0.65   |
| SK hynix  | PC601A NVMe        | 512 GB | 2       | 237   | 0     | 0.65   |
| Phison    | ESO256GMFCH-E3C-2  | 256 GB | 1       | 235   | 0     | 0.65   |
| PNY       | CS2030 480GB SSD   | 480 GB | 1       | 234   | 0     | 0.64   |
| BAITITON  | BT58SSD08E         | 128 GB | 1       | 232   | 0     | 0.64   |
| Samsung   | SSD 960 PRO        | 1 TB   | 19      | 252   | 1     | 0.63   |
| Samsung   | MZVLV256HCHP-00000 | 256 GB | 6       | 227   | 0     | 0.62   |
| Toshiba   | KBG40ZPZ512G NVMe  | 512 GB | 3       | 227   | 0     | 0.62   |
| ADATA     | SX8200NP           | 240 GB | 6       | 251   | 20    | 0.62   |
| Lite-On   | T10 240            | 240 GB | 1       | 227   | 0     | 0.62   |
| LDLC      | 120GB              | 120 GB | 1       | 226   | 0     | 0.62   |
| WDC       | WDS200T3XHC-00SJG0 | 2 TB   | 3       | 225   | 0     | 0.62   |
| SK hynix  | PC300 NVMe         | 512 GB | 3       | 224   | 0     | 0.61   |
| Toshiba   | KXG60ZNV1T02 NVMe  | 1 TB   | 12      | 224   | 0     | 0.61   |
| Toshiba   | KBG30ZMS128G NVMe  | 128 GB | 11      | 221   | 0     | 0.61   |
| Plextor   | PX-256M9PeG        | 256 GB | 3       | 221   | 0     | 0.61   |
| Toshiba   | KXG60ZNV1T02       | 1 TB   | 9       | 220   | 0     | 0.60   |
| Team      | TM8FP2240G         | 240 GB | 1       | 219   | 0     | 0.60   |
| Toshiba   | THNSN5128GPU7      | 128 GB | 6       | 218   | 0     | 0.60   |
| Samsung   | MZVKW1T0HMLH-00000 | 1 TB   | 2       | 218   | 0     | 0.60   |
| Intel     | SSDPEKNW020T8      | 2 TB   | 49      | 215   | 0     | 0.59   |
| Toshiba   | KXG50ZNV512G       | 512 GB | 27      | 215   | 0     | 0.59   |
| KIOXIA    | KXG60PNV2T04 NVMe  | 2 TB   | 9       | 215   | 0     | 0.59   |
| ADATA     | SX6000NP           | 256 GB | 2       | 214   | 0     | 0.59   |
| Intel     | SSDPE2KX020T8      | 2 TB   | 3       | 212   | 0     | 0.58   |
| Corsair   | Force MP510        | 960 GB | 25      | 208   | 0     | 0.57   |
| Kingston  | SKC2000M81000G     | 1 TB   | 4       | 208   | 0     | 0.57   |
| Intel     | H10 HBRPEKNX010... | 256 GB | 1       | 208   | 0     | 0.57   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 5       | 207   | 0     | 0.57   |
| Toshiba   | KXG5AZNV512G NV... | 512 GB | 1       | 207   | 0     | 0.57   |
| Lite-On   | CX2-8B256-Q11 NVMe | 256 GB | 6       | 207   | 0     | 0.57   |
| Toshiba   | KXG5AZNV512G       | 512 GB | 7       | 206   | 0     | 0.57   |
| Transcend | TS256GMTE220S      | 256 GB | 9       | 202   | 0     | 0.55   |
| Samsung   | MZVLW1T0HMLH-000L2 | 1 TB   | 6       | 202   | 0     | 0.55   |
| Intel     | SSDPEKKW256G8      | 256 GB | 37      | 201   | 0     | 0.55   |
| PNY       | CS3140 2TB SSD     | 2 TB   | 1       | 200   | 0     | 0.55   |
| Micron    | 9200_MTFDHAL1T6TCU | 1.6 TB | 1       | 200   | 0     | 0.55   |
| Intel     | SSDPED1D960GAY     | 960 GB | 1       | 199   | 0     | 0.55   |
| SPCC      | M.2 PCIE SSD       | 1 TB   | 5       | 199   | 0     | 0.55   |
| Samsung   | MZVLW128HEGR-000L1 | 128 GB | 4       | 198   | 0     | 0.54   |
| Team      | TM8FP4512G         | 512 GB | 1       | 198   | 0     | 0.54   |
| SK hynix  | HFS256GD9MNE-6200A | 256 GB | 2       | 196   | 0     | 0.54   |
| Patriot   | Scorch M2          | 128 GB | 5       | 196   | 0     | 0.54   |
| V-GeN     | V-GEN10SM19EG25... | 256 GB | 1       | 196   | 0     | 0.54   |
| LDLC      | 240GB              | 240 GB | 1       | 194   | 0     | 0.53   |
| Gigabyte  | GP-GSM2NE3128GNTD  | 128 GB | 3       | 193   | 0     | 0.53   |
| Toshiba   | RD400              | 512 GB | 1       | 193   | 0     | 0.53   |
| Toshiba   | KBG30ZMS512G       | 512 GB | 1       | 193   | 0     | 0.53   |
| Samsung   | PM951 NVMe         | 1 TB   | 2       | 192   | 0     | 0.53   |
| Intel     | SSDPEKKF010T8      | 1 TB   | 5       | 191   | 0     | 0.53   |
| Samsung   | MZVLW512HMJP-000L2 | 512 GB | 14      | 191   | 0     | 0.52   |
| KINGBANK  | KP230              | 512 GB | 2       | 190   | 0     | 0.52   |
| Toshiba   | THNSN5256GPU7 NVMe | 256 GB | 6       | 190   | 0     | 0.52   |
| Mushkin   | MKNSSDHL500GB-D8   | 500 GB | 1       | 189   | 0     | 0.52   |
| Toshiba   | KXG50ZNV1T02       | 1 TB   | 3       | 188   | 0     | 0.52   |
| Samsung   | MZVLV256HCHP-000H1 | 256 GB | 9       | 188   | 0     | 0.52   |
| Samsung   | MZVLV512HCJH-000H1 | 512 GB | 2       | 188   | 0     | 0.52   |
| Lenovo    | LENSE20512GMSP3... | 512 GB | 9       | 187   | 0     | 0.51   |
| Lenovo    | LENSE20256GMSP3... | 256 GB | 20      | 198   | 1     | 0.51   |
| WDC       | WDS500G1B0C-00S6U0 | 500 GB | 9       | 186   | 0     | 0.51   |
| Intel     | SSDPEKKF512G8 NVMe | 512 GB | 6       | 186   | 0     | 0.51   |
| SanDisk   | Extreme Pro        | 1 TB   | 6       | 185   | 0     | 0.51   |
| Toshiba   | THNSN0256GTYA      | 256 GB | 2       | 185   | 0     | 0.51   |
| Toshiba   | KBG40ZNS256G ME... | 256 GB | 2       | 183   | 0     | 0.50   |
| Intel     | MEMPEK1J016GAL     | 16 GB  | 7       | 183   | 0     | 0.50   |
| Toshiba   | THNSN5512GPUK      | 512 GB | 8       | 182   | 0     | 0.50   |
| Lexar     | SSD                | 128 GB | 8       | 182   | 0     | 0.50   |
| WDC       | WDS250G1B0C-00S6U0 | 250 GB | 12      | 181   | 0     | 0.50   |
| Toshiba   | KBG40ZNS512G NVMe  | 512 GB | 11      | 179   | 0     | 0.49   |
| Corsair   | Force MP600        | 500 GB | 10      | 179   | 0     | 0.49   |
| Toshiba   | RC100              | 240 GB | 7       | 179   | 0     | 0.49   |
| Kingston  | OM8PCP3512F-A01    | 512 GB | 1       | 178   | 0     | 0.49   |
| SK hynix  | PC601 HFS256GD9... | 256 GB | 3       | 177   | 0     | 0.49   |
| Corsair   | MP600 PRO          | 2 TB   | 1       | 176   | 0     | 0.48   |
| Samsung   | MZVPW256HEGL-00000 | 256 GB | 16      | 176   | 0     | 0.48   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 3       | 175   | 0     | 0.48   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 1       | 175   | 0     | 0.48   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 1       | 175   | 0     | 0.48   |
| Transcend | TS1TMTE220S        | 1 TB   | 9       | 174   | 0     | 0.48   |
| Phison    | Viper M.2 VPN100   | 1 TB   | 14      | 174   | 0     | 0.48   |
| Lite-On   | CX2-8B512-Q11 NVMe | 512 GB | 3       | 173   | 0     | 0.47   |
| SK hynix  | PC601 NVMe         | 1 TB   | 9       | 172   | 0     | 0.47   |
| Team      | M8FP2              | 480 GB | 1       | 172   | 0     | 0.47   |
| Samsung   | SSD 960 PRO        | 512 GB | 57      | 191   | 4     | 0.47   |
| Lite-On   | CA3-8D512          | 512 GB | 7       | 172   | 0     | 0.47   |
| Lite-On   | S980 256           | 256 GB | 1       | 170   | 0     | 0.47   |
| Samsung   | MZVLW128HEGR-00000 | 128 GB | 5       | 170   | 0     | 0.47   |
| WDC       | WDS100T3XHC-00SJG0 | 1 TB   | 9       | 168   | 0     | 0.46   |
| Crucial   | CT1000P1SSD8       | 1 TB   | 157     | 181   | 17    | 0.46   |
| Toshiba   | KXG50PNV2T04       | 2 TB   | 2       | 167   | 0     | 0.46   |
| Lexar     | SSD                | 256 GB | 3       | 167   | 0     | 0.46   |
| ZHITAI    | PC005 Active       | 1 TB   | 3       | 166   | 0     | 0.46   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 7       | 166   | 0     | 0.46   |
| Apacer    | AS2280P4           | 240 GB | 1       | 165   | 0     | 0.45   |
| Samsung   | PM981 NVMe         | 1 TB   | 7       | 164   | 0     | 0.45   |
| Apacer    | AS2280P4           | 480 GB | 1       | 163   | 0     | 0.45   |
| Mushkin   | MKNSSDPL500GB-D8   | 500 GB | 2       | 163   | 0     | 0.45   |
| Phison    | Sabrent            | 1 TB   | 98      | 163   | 0     | 0.45   |
| Crucial   | CT500P1SSD8        | 500 GB | 84      | 171   | 8     | 0.45   |
| Phison    | Sabrent Rocket 4.0 | 2 TB   | 12      | 162   | 0     | 0.45   |
| Intel     | MEMPEK1W016GA      | 16 GB  | 5       | 161   | 0     | 0.44   |
| Samsung   | MZVKW1T0HMLH-000H1 | 1 TB   | 2       | 161   | 0     | 0.44   |
| Intel     | HBRPEKNX0101AO     | 16 GB  | 2       | 161   | 0     | 0.44   |
| Transcend | TS2TMTE220S        | 2 TB   | 1       | 160   | 0     | 0.44   |
| Toshiba   | KXG60ZNV512G NVMe  | 512 GB | 33      | 159   | 0     | 0.44   |
| Toshiba   | KXG50ZNV256G       | 256 GB | 17      | 159   | 0     | 0.44   |
| Toshiba   | THNSN5256GPUK      | 256 GB | 2       | 157   | 0     | 0.43   |
| Toshiba   | KXG60ZNV256G NVMe  | 256 GB | 22      | 157   | 0     | 0.43   |
| SanDisk   | Extreme Pro        | 500 GB | 9       | 156   | 0     | 0.43   |
| SK hynix  | PC401 NVMe         | 256 GB | 14      | 158   | 1     | 0.43   |
| Mushkin   | MKNSSDHL250GB-D8   | 250 GB | 2       | 155   | 0     | 0.43   |
| Lite-On   | CL1-3D128-Q11 NVMe | 128 GB | 2       | 154   | 0     | 0.42   |
| Seagate   | FireCuda 510 SS... | 500 GB | 1       | 154   | 0     | 0.42   |
| Samsung   | MZVPW256HEGL-000H1 | 256 GB | 5       | 153   | 0     | 0.42   |
| Samsung   | SSD 960 EVO        | 500 GB | 98      | 162   | 13    | 0.42   |
| SPCC      | M.2 PCIe SSD       | 1 TB   | 22      | 150   | 0     | 0.41   |
| Phison    | PP3-8D256          | 256 GB | 1       | 150   | 0     | 0.41   |
| Samsung   | SM951 NVMe         | 256 GB | 1       | 150   | 0     | 0.41   |
| Intel     | SSDPEKKW128G8      | 128 GB | 16      | 148   | 0     | 0.41   |
| Samsung   | SSD 960 EVO        | 1 TB   | 51      | 154   | 2     | 0.41   |
| Toshiba   | RC500              | 250 GB | 2       | 146   | 0     | 0.40   |
| Intel     | SSDPEL1D380GA      | 384 GB | 1       | 146   | 0     | 0.40   |
| Intel     | HBRPEKNX0203A      | 1 TB   | 2       | 145   | 0     | 0.40   |
| Plextor   | PX-512M8PeG        | 512 GB | 6       | 165   | 92    | 0.40   |
| Samsung   | SSD 960 PRO        | 2 TB   | 10      | 154   | 5     | 0.40   |
| Silico... | M.2 (P80) 3TG3-P   | 1 TB   | 1       | 145   | 0     | 0.40   |
| Intel     | HBRPEKNX0101AHO    | 16 GB  | 11      | 144   | 0     | 0.40   |
| Samsung   | MZ1LB3T8HMLA-00007 | 3.8 TB | 3       | 144   | 0     | 0.40   |
| Plextor   | PX-512M9PeY        | 512 GB | 5       | 143   | 0     | 0.39   |
| Intel     | HBRPEKNX0101A      | 256 GB | 2       | 142   | 0     | 0.39   |
| ADATA     | SX8200PNP          | 512 GB | 81      | 142   | 0     | 0.39   |
| Intel     | SSDPEBKF128G7      | 128 GB | 3       | 500   | 10    | 0.39   |
| Corsair   | Force MP510        | 480 GB | 26      | 142   | 0     | 0.39   |
| Samsung   | MZVLW512HMJP-00000 | 512 GB | 15      | 143   | 1     | 0.39   |
| ADATA     | SX8200PNP          | 1 TB   | 83      | 141   | 1     | 0.39   |
| HP        | SSD EX900          | 250 GB | 10      | 176   | 1     | 0.39   |
| PNY       | CS2130 2TB SSD     | 2 TB   | 2       | 140   | 0     | 0.38   |
| Lite-On   | CA1-8D128          | 128 GB | 1       | 139   | 0     | 0.38   |
| Intel     | SSDPEKKF010T7      | 1 TB   | 1       | 139   | 0     | 0.38   |
| ADATA     | IM2P33E8-001TD     | 1 TB   | 1       | 139   | 0     | 0.38   |
| XPG       | GAMMIX S11 Pro     | 1 TB   | 65      | 138   | 0     | 0.38   |
| Phison    | BPX                | 240 GB | 4       | 253   | 7     | 0.38   |
| Corsair   | Force MP510        | 240 GB | 31      | 137   | 0     | 0.38   |
| Transcend | TS128GMTE110S      | 128 GB | 11      | 136   | 0     | 0.37   |
| KIOXIA    | KXG50PNV2T04       | 2 TB   | 1       | 136   | 0     | 0.37   |
| Smartbuy  | m.2 PS5008T-2280T  | 256 GB | 1       | 135   | 0     | 0.37   |
| Kingston  | SKC2000M8250G      | 250 GB | 2       | 135   | 0     | 0.37   |
| Intel     | HBRPEKNX0203AHO    | 32 GB  | 12      | 134   | 0     | 0.37   |
| Samsung   | MZVLW1T0HMLH-00000 | 1 TB   | 7       | 132   | 0     | 0.36   |
| Samsung   | MZFLV256HCHP-000MV | 256 GB | 3       | 131   | 0     | 0.36   |
| Intel     | SSDPEKKF512G7      | 512 GB | 1       | 130   | 0     | 0.36   |
| Intel     | HBRPEKNX0101AH     | 256 GB | 11      | 130   | 0     | 0.36   |
| Intel     | SSDPEKNW512G8      | 512 GB | 193     | 130   | 0     | 0.36   |
| Intel     | HBRPEKNX0203AO     | 32 GB  | 3       | 130   | 0     | 0.36   |
| Plextor   | PX-1TM8PeY         | 1 TB   | 2       | 129   | 0     | 0.35   |
| Silico... | Asgard AN2 250N... | 250 GB | 2       | 128   | 0     | 0.35   |
| Toshiba   | KBG30ZMT512G       | 512 GB | 6       | 127   | 0     | 0.35   |
| Toshiba   | KBG40ZNS256G NVMe  | 256 GB | 13      | 127   | 0     | 0.35   |
| Corsair   | Force MP600        | 1 TB   | 50      | 126   | 0     | 0.35   |
| Intel     | SSDPEKKF256G8 NVMe | 256 GB | 7       | 126   | 0     | 0.35   |
| Corsair   | Force MP510 1.9TB  | 1.9 TB | 5       | 125   | 0     | 0.34   |
| SK hynix  | PC601 NVMe         | 512 GB | 43      | 125   | 0     | 0.34   |
| Phison    | Viper M.2 VP4100   | 1 TB   | 6       | 125   | 0     | 0.34   |
| Intel     | SSDPEKKW512G8      | 512 GB | 13      | 125   | 0     | 0.34   |
| Toshiba   | KBG30ZMS512G NVMe  | 512 GB | 2       | 125   | 0     | 0.34   |
| Intel     | SSDPEKNW010T8      | 1 TB   | 161     | 126   | 7     | 0.34   |
| Phison    | PCIe SSD           | 1 TB   | 56      | 123   | 0     | 0.34   |
| Phison    | APS-SE20G-2T       | 2 TB   | 1       | 122   | 0     | 0.34   |
| Phison    | BPXP               | 960 GB | 2       | 122   | 0     | 0.33   |
| Mushkin   | MKNSSDPL1TB-D8     | 1 TB   | 1       | 121   | 0     | 0.33   |
| tigo      | SSD                | 512 GB | 1       | 121   | 0     | 0.33   |
| WDC       | WDBGMP0020BNC-WRSN | 2 TB   | 1       | 121   | 0     | 0.33   |
| Corsair   | Force MP600        | 2 TB   | 10      | 120   | 0     | 0.33   |
| Samsung   | MZVLW256HEHP-000L2 | 256 GB | 30      | 119   | 0     | 0.33   |
| Intel     | SSDPEKKF010T8 NVMe | 1 TB   | 5       | 119   | 0     | 0.33   |
| Toshiba   | RC500              | 500 GB | 3       | 119   | 0     | 0.33   |
| ADATA     | SX8200PNP          | 256 GB | 40      | 136   | 54    | 0.33   |
| PNY       | CS3030 1TB SSD     | 1 TB   | 12      | 119   | 0     | 0.33   |
| Samsung   | SSD 970 EVO        | 250 GB | 129     | 126   | 2     | 0.33   |
| KIOXIA    | KXG60ZNV512G NVMe  | 512 GB | 23      | 118   | 0     | 0.33   |
| Samsung   | KUS040202M-B000    | 512 GB | 1       | 118   | 0     | 0.32   |
| Kingston  | SA1000M8480G       | 480 GB | 8       | 118   | 0     | 0.32   |
| Lexar     | 1TB SSD            | 1 TB   | 1       | 117   | 0     | 0.32   |
| Intel     | HBRPEKNX0203AH     | 1 TB   | 12      | 117   | 0     | 0.32   |
| Samsung   | MZFLV128HCGR-000MV | 128 GB | 9       | 117   | 0     | 0.32   |
| Hikvision | HS-SSD-C2000       | 1 TB   | 1       | 116   | 0     | 0.32   |
| Silico... | M Series NVMe S... | 256 GB | 3       | 115   | 0     | 0.32   |
| Gigabyte  | GP-ASM2NE2256GTTDR | 256 GB | 2       | 114   | 0     | 0.31   |
| Toshiba   | THNSN5128GPUK      | 128 GB | 1       | 114   | 0     | 0.31   |
| Mushkin   | MKNSSDPE2TB-D8     | 2 TB   | 9       | 113   | 0     | 0.31   |
| FORESEE   | P900F256GBH        | 256 GB | 1       | 113   | 0     | 0.31   |
| Samsung   | SM961 NVMe         | 512 GB | 2       | 112   | 0     | 0.31   |
| Samsung   | SSD 970 PRO        | 512 GB | 140     | 113   | 1     | 0.31   |
| SPCC      | M.2 PCIe SSD       | 256 GB | 28      | 110   | 0     | 0.30   |
| Team      | TM8FP6512G         | 512 GB | 3       | 110   | 0     | 0.30   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 16      | 110   | 0     | 0.30   |
| Huawei    | HWE52P432T0L005N   | 2 TB   | 6       | 110   | 0     | 0.30   |
| ADATA     | SX8200PNP          | 2 TB   | 27      | 110   | 0     | 0.30   |
| Phison    | Sabrent Rocket 4.0 | 1 TB   | 58      | 110   | 0     | 0.30   |
| SK hynix  | SKHynix_HFS001T... | 1 TB   | 3       | 109   | 0     | 0.30   |
| Samsung   | MZVLW256HEHP-00000 | 256 GB | 47      | 111   | 1     | 0.30   |
| Samsung   | MZVKW512HMJP-00007 | 512 GB | 1       | 109   | 0     | 0.30   |
| Samsung   | SSD 960 EVO        | 250 GB | 150     | 117   | 15    | 0.30   |
| HP        | SSD EX920          | 256 GB | 1       | 325   | 2     | 0.30   |
| WDC       | WDS500G3XHC-00SJG0 | 500 GB | 12      | 107   | 0     | 0.30   |
| UMIS      | RPJTJ256MED1OWX    | 256 GB | 4       | 106   | 0     | 0.29   |
| Seagate   | FireCuda 510 SS... | 1 TB   | 9       | 106   | 0     | 0.29   |
| ADATA     | SX8100NP           | 512 GB | 8       | 111   | 127   | 0.29   |
| Plextor   | PX-128M8PeGN       | 128 GB | 1       | 106   | 0     | 0.29   |
| Seagate   | BarraCuda 510 S... | 1 TB   | 3       | 105   | 0     | 0.29   |
| KIOXIA    | KXG60ZNV1T02 NVMe  | 1 TB   | 19      | 105   | 0     | 0.29   |
| Kingston  | RBUSNS8154P3512GJ5 | 512 GB | 4       | 105   | 0     | 0.29   |
| Lite-On   | CA3-8D256          | 256 GB | 8       | 104   | 0     | 0.29   |
| Samsung   | PM961 NVMe         | 512 GB | 12      | 124   | 3     | 0.29   |
| Kingston  | SA2000M8500G       | 500 GB | 89      | 103   | 0     | 0.28   |
| Intel     | H10 HBRPEKNX020... | 512 GB | 21      | 103   | 0     | 0.28   |
| Toshiba   | KBG30ZMV256G       | 256 GB | 29      | 103   | 0     | 0.28   |
| Toshiba   | KBG30ZMS256G NVMe  | 256 GB | 22      | 103   | 0     | 0.28   |
| Phison    | M.2 PCIE G3x4 NVMe | 1 TB   | 3       | 102   | 0     | 0.28   |
| Plextor   | PX-512M9PGN +      | 512 GB | 2       | 101   | 0     | 0.28   |
| Samsung   | KUS030202M-B000    | 256 GB | 4       | 101   | 0     | 0.28   |
| Lite-On   | CL1-4D256          | 256 GB | 5       | 101   | 0     | 0.28   |
| T-FORCE   | TM8FP7001T         | 1 TB   | 1       | 100   | 0     | 0.28   |
| Kingston  | RBUSNS8154P3512GJ2 | 512 GB | 3       | 99    | 0     | 0.27   |
| Apacer    | Z280 120G          | 120 GB | 2       | 99    | 0     | 0.27   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 16      | 99    | 0     | 0.27   |
| Samsung   | MZVKW512HMJP-000L7 | 512 GB | 11      | 99    | 0     | 0.27   |
| KIOXIA    | KXG60PNV2T04       | 2 TB   | 1       | 98    | 0     | 0.27   |
| WDC       | PC SN720 SDAQNT... | 256 GB | 1       | 98    | 0     | 0.27   |
| SK hynix  | HFS001TD9TNG-L2A0A | 1 TB   | 2       | 98    | 0     | 0.27   |
| SK hynix  | PC611 NVMe         | 512 GB | 21      | 98    | 0     | 0.27   |
| Zheino    | CHN-NGFFNV2280-1TB | 1 TB   | 2       | 98    | 0     | 0.27   |
| Goodram   | SSDPR-PX400-256-80 | 256 GB | 1       | 97    | 0     | 0.27   |
| SSSTC     | CL1-3D256-Q11 NVMe | 256 GB | 7       | 97    | 0     | 0.27   |
| Seagate   | FireCuda 520 SS... | 500 GB | 9       | 97    | 0     | 0.27   |
| Plextor   | PX-1TM8SeG         | 1 TB   | 2       | 380   | 54    | 0.27   |
| Samsung   | MZVLW512HMJP-000H7 | 512 GB | 1       | 97    | 0     | 0.27   |
| Toshiba   | KXG60PNV2T04 NV... | 2 TB   | 5       | 97    | 0     | 0.27   |
| Samsung   | MZVLB2T0HMLB-000L2 | 2 TB   | 1       | 96    | 0     | 0.27   |
| KIOXIA    | KXG60ZNV256G       | 256 GB | 5       | 96    | 0     | 0.26   |
| Patriot   | Scorch M2          | 256 GB | 5       | 96    | 0     | 0.26   |
| Samsung   | MZVLW256HEHP-000L7 | 256 GB | 68      | 97    | 1     | 0.26   |
| Patriot   | Hellfire M2        | 480 GB | 1       | 96    | 0     | 0.26   |
| Samsung   | MZVKW512HMJP-000H1 | 512 GB | 8       | 96    | 0     | 0.26   |
| HP        | SSD EX920          | 1 TB   | 9       | 96    | 0     | 0.26   |
| Intel     | SSDPEKKW010T8      | 1 TB   | 5       | 95    | 0     | 0.26   |
| Intel     | HBRPEKNX0202ALO    | 32 GB  | 6       | 94    | 0     | 0.26   |
| Samsung   | MZPLL3T2HAJQ-00005 | 3.2 TB | 1       | 94    | 0     | 0.26   |
| Plextor   | PX-1TM8PeG         | 1 TB   | 1       | 93    | 0     | 0.26   |
| SPCC      | M.2 PCIe SSD       | 2 TB   | 3       | 93    | 0     | 0.26   |
| Phison    | APS-SE20G-512      | 512 GB | 1       | 93    | 0     | 0.26   |
| Micron    | MTFDHBA512TCK      | 512 GB | 6       | 92    | 0     | 0.25   |
| Samsung   | MZVLB1T0HALR-00000 | 1 TB   | 35      | 125   | 1     | 0.25   |
| Phison    | SBXe               | 960 GB | 2       | 92    | 0     | 0.25   |
| Smartbuy  | m.2 PS5013-2280T   | 256 GB | 2       | 92    | 0     | 0.25   |
| Phison    | Sabrent Rocket Q   | 1 TB   | 39      | 91    | 0     | 0.25   |
| Micron    | 2200 NVMe          | 512 GB | 2       | 91    | 0     | 0.25   |
| WDC       | WDS200T1X0E-00AFY0 | 2 TB   | 9       | 91    | 0     | 0.25   |
| Intel     | SSDPEKKW010T8L     | 1 TB   | 1       | 91    | 0     | 0.25   |
| XPG       | GAMMIX S70         | 1 TB   | 3       | 91    | 0     | 0.25   |
| Corsair   | Force MP300        | 120 GB | 2       | 90    | 0     | 0.25   |
| Samsung   | PM981 NVMe         | 2 TB   | 2       | 90    | 0     | 0.25   |
| Corsair   | MP600 PRO          | 1 TB   | 2       | 90    | 0     | 0.25   |
| Union ... | UMIS RPJTJ256ME... | 256 GB | 3       | 90    | 0     | 0.25   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 5       | 90    | 0     | 0.25   |
| KIOXIA    | KXG60ZNV1T02       | 1 TB   | 11      | 90    | 0     | 0.25   |
| Silico... | R5MP480G8          | 480 GB | 2       | 90    | 0     | 0.25   |
| Samsung   | MZVLB1T0HALR-000L7 | 1 TB   | 31      | 90    | 0     | 0.25   |
| SPCC      | M.2 PCIe SSD       | 512 GB | 25      | 89    | 0     | 0.25   |
| Intel     | HBRPEKNX0202AHO    | 32 GB  | 27      | 89    | 0     | 0.25   |
| Micron    | 7300_MTFDHBG3T8TDF | 3.8 TB | 1       | 89    | 0     | 0.25   |
| Toshiba   | KBG30ZPZ512G       | 512 GB | 1       | 89    | 0     | 0.24   |
| Samsung   | MZVLW512HMJP-000L7 | 512 GB | 17      | 89    | 1     | 0.24   |
| Toshiba   | THNSF5256GPU7      | 256 GB | 1       | 88    | 0     | 0.24   |
| Phison    | Sabrent Rocket 4.0 | 500 GB | 8       | 88    | 0     | 0.24   |
| Phison    | PS5012-E12S-1T     | 1 TB   | 1       | 86    | 0     | 0.24   |
| Intel     | SSDPEDMW400G4      | 400 GB | 1       | 86    | 0     | 0.24   |
| Toshiba   | KBG30ZMT128G       | 128 GB | 15      | 85    | 0     | 0.24   |
| Samsung   | MZVLB512HAJQ-000H7 | 512 GB | 9       | 85    | 0     | 0.24   |
| Toshiba   | THNSN5256GPU7      | 256 GB | 1       | 85    | 0     | 0.23   |
| Kingston  | RBUSNS8154P3128GJ3 | 128 GB | 1       | 85    | 0     | 0.23   |
| ADATA     | SX8100NP           | 1 TB   | 3       | 85    | 0     | 0.23   |
| SanDisk   | WD_BLACK SN750     | 2 TB   | 2       | 85    | 0     | 0.23   |
| Intel     | SSDPEKNW010T8H     | 1 TB   | 13      | 84    | 0     | 0.23   |
| SK hynix  | PC300 NVMe         | 256 GB | 7       | 93    | 1     | 0.23   |
| Kingston  | SA2000M81000G      | 1 TB   | 108     | 84    | 10    | 0.23   |
| Silico... | R5MP120G8          | 120 GB | 3       | 83    | 0     | 0.23   |
| KIOXIA    | KBG30ZMV256G       | 256 GB | 15      | 85    | 68    | 0.23   |
| Kingston  | OM8PDP3256B-A01    | 256 GB | 3       | 83    | 0     | 0.23   |
| KIOXIA    | KBG40ZPZ512G NVMe  | 512 GB | 10      | 82    | 0     | 0.23   |
| AMD       | R5MP240G8          | 240 GB | 2       | 82    | 0     | 0.23   |
| Silico... | NVME SSD           | 512 GB | 5       | 82    | 0     | 0.23   |
| Samsung   | MZVLW256HEHP-000H1 | 256 GB | 40      | 90    | 1     | 0.23   |
| Goodram   | IR-SSDPR-P34B-0... | 2 TB   | 4       | 82    | 0     | 0.23   |
| Samsung   | MZVLB2T0HMLB-00000 | 2 TB   | 1       | 81    | 0     | 0.22   |
| Silico... | NVME SSD           | 1 TB   | 2       | 81    | 0     | 0.22   |
| Kingston  | SA2000M8250G       | 250 GB | 74      | 81    | 0     | 0.22   |
| Lenovo    | LENSE30512GMSP3... | 512 GB | 13      | 80    | 0     | 0.22   |
| Gigabyte  | GP-GSM2NE8256GNTD  | 256 GB | 2       | 80    | 0     | 0.22   |
| Kingston  | OM8PDP3256B-AB1    | 256 GB | 1       | 80    | 0     | 0.22   |
| Samsung   | MZVPV256HDGL-000L2 | 256 GB | 1       | 80    | 0     | 0.22   |
| Intel     | SSDPEKNW512G8L     | 512 GB | 28      | 80    | 0     | 0.22   |
| Micron    | 2200S NVMe         | 256 GB | 7       | 79    | 0     | 0.22   |
| SPCC      | M.2 PCIE SSD       | 256 GB | 3       | 79    | 0     | 0.22   |
| Intel     | HBRPEKNX0202AL     | 512 GB | 7       | 79    | 0     | 0.22   |
| WDC       | WDS250G3X0C-00SJG0 | 250 GB | 12      | 79    | 0     | 0.22   |
| Samsung   | PM961 NVMe         | 1 TB   | 3       | 79    | 0     | 0.22   |
| Intel     | HBRPEKNX0202AH     | 512 GB | 29      | 79    | 0     | 0.22   |
| Plextor   | PX-256M9PeY        | 256 GB | 2       | 79    | 0     | 0.22   |
| Toshiba   | KBG30ZMV512G       | 512 GB | 16      | 77    | 0     | 0.21   |
| ORICO     | V500               | 128 GB | 1       | 76    | 0     | 0.21   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 8       | 76    | 0     | 0.21   |
| Union ... | UMIS RPJTJ128ME... | 128 GB | 2       | 76    | 0     | 0.21   |
| PNY       | CS3030 500GB SSD   | 500 GB | 13      | 76    | 0     | 0.21   |
| WDC       | PC SN520 NVMe      | 128 GB | 11      | 76    | 0     | 0.21   |
| WDC       | WDS100T3X0C-00SJG0 | 1 TB   | 89      | 76    | 0     | 0.21   |
| Corsair   | Force MP300        | 960 GB | 1       | 76    | 0     | 0.21   |
| WDC       | WDS500G3X0C-00SJG0 | 500 GB | 94      | 78    | 11    | 0.21   |
| Micron    | 9300_MTFDHAL6T4TDR | 6.4 TB | 2       | 76    | 0     | 0.21   |
| Samsung   | SSD 970 EVO        | 500 GB | 277     | 77    | 8     | 0.21   |
| Lite-On   | CB1-SD512          | 512 GB | 1       | 75    | 0     | 0.21   |
| KIOXIA    | KBG40ZPZ256G NVMe  | 256 GB | 5       | 75    | 0     | 0.21   |
| Intel     | SSDPEMKF010T8 NVMe | 1 TB   | 17      | 77    | 60    | 0.20   |
| Toshiba   | KXG60ZNV256G NV... | 256 GB | 1       | 74    | 0     | 0.20   |
| Plextor   | PX-256M8PeY        | 256 GB | 2       | 73    | 0     | 0.20   |
| Silico... | AITC M.2 FZ300     | 128 GB | 1       | 73    | 0     | 0.20   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 4       | 72    | 0     | 0.20   |
| Samsung   | MZVLW128HEGR-000H1 | 128 GB | 11      | 72    | 0     | 0.20   |
| Team      | TM8FP4256G         | 256 GB | 3       | 72    | 0     | 0.20   |
| PNY       | CS3030 1000GB SSD  | 1 TB   | 2       | 71    | 0     | 0.20   |
| Toshiba   | KBG30ZPZ256G       | 256 GB | 2       | 71    | 0     | 0.20   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 2       | 71    | 0     | 0.20   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 34      | 71    | 0     | 0.20   |
| Silico... | 1TB PCS PCIe M.... | 1 TB   | 3       | 71    | 0     | 0.20   |
| Kingston  | RBUSNS8154P3512GJ1 | 512 GB | 11      | 71    | 0     | 0.19   |
| Seagate   | FireCuda 520 SS... | 1 TB   | 13      | 71    | 0     | 0.19   |
| Intel     | SSDPE2KX040T8      | 4 TB   | 12      | 70    | 0     | 0.19   |
| SSSTC     | CL1-8D512          | 512 GB | 1       | 70    | 0     | 0.19   |
| Samsung   | MZVLB512HAJQ-000L2 | 512 GB | 21      | 71    | 1     | 0.19   |
| Samsung   | MZVLW1T0HMLH-000L7 | 1 TB   | 9       | 76    | 2     | 0.19   |
| KIOXIA... | PLUS SSD           | 1 TB   | 6       | 70    | 0     | 0.19   |
| Team      | TM8FP4001T         | 1 TB   | 3       | 70    | 0     | 0.19   |
| Samsung   | MZFLW256HEHP-000MV | 256 GB | 2       | 69    | 0     | 0.19   |
| Samsung   | PM981 NVMe         | 256 GB | 17      | 69    | 0     | 0.19   |
| Samsung   | PM961 NVMe         | 256 GB | 12      | 69    | 0     | 0.19   |
| Samsung   | SSD 970 EVO        | 1 TB   | 265     | 74    | 5     | 0.19   |
| Hikvision | HS-SSD-E2000       | 256 GB | 1       | 69    | 0     | 0.19   |
| Samsung   | MZVLW128HEGR-000L2 | 128 GB | 16      | 84    | 1     | 0.19   |
| WDC       | PC SN720 SED SD... | 1 TB   | 3       | 69    | 0     | 0.19   |
| Intel     | SSDPEMKF256G8 NVMe | 256 GB | 2       | 69    | 0     | 0.19   |
| KIOXIA    | KXG6AZNV512G NV... | 512 GB | 4       | 69    | 0     | 0.19   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 15      | 69    | 0     | 0.19   |
| KIOXIA    | KBG40ZNS256G NVMe  | 256 GB | 53      | 68    | 0     | 0.19   |
| KIOXIA    | KXG60ZNV512G       | 512 GB | 15      | 68    | 0     | 0.19   |
| Goodram   | SSDPR-PX500-256-80 | 256 GB | 3       | 68    | 0     | 0.19   |
| PNY       | CS2130 1TB SSD     | 1 TB   | 4       | 68    | 0     | 0.19   |
| Samsung   | MZVKW1T0HMLH-000L7 | 1 TB   | 1       | 67    | 0     | 0.19   |
| Samsung   | SSD 970 PRO        | 1 TB   | 65      | 73    | 1     | 0.19   |
| Silico... | NE-1TB             | 1 TB   | 7       | 67    | 0     | 0.19   |
| Samsung   | MZVLQ256HAJD-000AC | 256 GB | 1       | 67    | 0     | 0.18   |
| Patriot   | P300               | 256 GB | 4       | 67    | 0     | 0.18   |
| Phison    | Daten DS2000       | 512 GB | 2       | 66    | 0     | 0.18   |
| SK hynix  | HFS256GD9TNG-62A0A | 256 GB | 15      | 66    | 0     | 0.18   |
| PNY       | CS3030 250GB SSD   | 250 GB | 6       | 66    | 0     | 0.18   |
| Silico... | NE-512             | 512 GB | 11      | 66    | 0     | 0.18   |
| WDC       | WDBRPG0010BNC-WRSN | 1 TB   | 10      | 66    | 0     | 0.18   |
| Intel     | SSDPEKNU512G8L     | 512 GB | 2       | 66    | 0     | 0.18   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 11      | 66    | 0     | 0.18   |
| WDC       | PC SN520 NVMe      | 256 GB | 15      | 65    | 0     | 0.18   |
| WDC       | PC SN520 SDAPMU... | 256 GB | 3       | 65    | 0     | 0.18   |
| Plextor   | PX-256M9PeGN       | 256 GB | 3       | 65    | 0     | 0.18   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 14      | 65    | 0     | 0.18   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 58      | 65    | 18    | 0.18   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 9       | 65    | 0     | 0.18   |
| WDC       | WDS500G2B0C-00PXH0 | 500 GB | 94      | 64    | 0     | 0.18   |
| KIOXIA    | KBG30ZMV128G       | 128 GB | 2       | 64    | 0     | 0.18   |
| Toshiba   | KXG6APNV2T04       | 2 TB   | 3       | 64    | 0     | 0.18   |
| Patriot   | P300               | 128 GB | 6       | 64    | 0     | 0.18   |
| Samsung   | PM961 NVMe SED     | 512 GB | 1       | 64    | 0     | 0.18   |
| PNY       | CS3030 2TB SSD     | 2 TB   | 4       | 64    | 0     | 0.18   |
| WDC       | PC SN720 SDAQNT... | 512 GB | 43      | 64    | 0     | 0.18   |
| Samsung   | MZVLB512HAJQ-000L7 | 512 GB | 95      | 64    | 1     | 0.18   |
| XPG       | SX8200PNP-512GT    | 512 GB | 1       | 63    | 0     | 0.18   |
| Kingston  | RBUSNS8154P3256GJ3 | 256 GB | 17      | 63    | 0     | 0.18   |
| Toshiba   | KXG60ZNV1T02 NV... | 1 TB   | 15      | 63    | 0     | 0.17   |
| SK hynix  | BC501 HFM128GDJ... | 128 GB | 5       | 63    | 0     | 0.17   |
| Kingston  | RBUSNS8154P3256GJ  | 256 GB | 15      | 63    | 0     | 0.17   |
| SK hynix  | PC601 NVMe         | 256 GB | 7       | 63    | 0     | 0.17   |
| WDC       | WDBA3V0010BNC-WRSN | 1 TB   | 3       | 63    | 0     | 0.17   |
| Crucial   | CT250P2SSD8        | 250 GB | 5       | 63    | 0     | 0.17   |
| Crucial   | CT2000P1SSD8       | 2 TB   | 2       | 63    | 0     | 0.17   |
| Silico... | Asgard AN1TNVMe... | 1 TB   | 1       | 63    | 0     | 0.17   |
| HP        | SSD EX900          | 500 GB | 9       | 106   | 9     | 0.17   |
| Intel     | SSDPEKKF256G8L     | 256 GB | 39      | 65    | 26    | 0.17   |
| XPG       | GAMMIX S7          | 512 GB | 1       | 62    | 0     | 0.17   |
| Toshiba   | KXG60ZNV256G       | 256 GB | 8       | 61    | 0     | 0.17   |
| WDC       | WDS100T2B0C-00PXH0 | 1 TB   | 120     | 61    | 0     | 0.17   |
| Toshiba   | KXG6AZNV256G       | 256 GB | 19      | 61    | 0     | 0.17   |
| Gigabyte  | GP-AG4500G         | 500 GB | 6       | 61    | 0     | 0.17   |
| Phison    | Enmotus P200-90... | 900 GB | 1       | 61    | 0     | 0.17   |
| Samsung   | MZVLW512HMJP-000H1 | 512 GB | 16      | 61    | 0     | 0.17   |
| SK hynix  | PC611 NVMe         | 1 TB   | 31      | 61    | 0     | 0.17   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 4       | 60    | 0     | 0.17   |
| WDC       | PC SN530 SDBPNP... | 1 TB   | 24      | 60    | 0     | 0.17   |
| ADATA     | SX6000PNP          | 256 GB | 11      | 60    | 0     | 0.17   |
| Gigabyte  | GP-AG42TB          | 2 TB   | 4       | 60    | 0     | 0.16   |
| Kingch... | 256GB              | 256 GB | 1       | 60    | 0     | 0.16   |
| Apacer    | AS2280P4           | 256 GB | 6       | 59    | 0     | 0.16   |
| Samsung   | MZVLB256HAHQ-000L7 | 256 GB | 48      | 61    | 1     | 0.16   |
| FORESEE   | P900F256GB         | 256 GB | 2       | 59    | 0     | 0.16   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 1       | 59    | 0     | 0.16   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 10      | 58    | 0     | 0.16   |
| Intel     | SSDPEKKF512G8L     | 512 GB | 34      | 58    | 0     | 0.16   |
| Silico... | 256GB PCS PCIe ... | 256 GB | 1       | 58    | 0     | 0.16   |
| Micron    | 2200S NVMe         | 512 GB | 29      | 58    | 0     | 0.16   |
| SK hynix  | PC300 NVMe         | 1 TB   | 7       | 58    | 0     | 0.16   |
| Hikvision | HS-SSD-C2000Pro    | 1 TB   | 1       | 58    | 0     | 0.16   |
| Micron    | 2200S NVMe         | 1 TB   | 11      | 59    | 1     | 0.16   |
| Phison    | SBX                | 256 GB | 1       | 58    | 0     | 0.16   |
| Micron    | 2200V_MTFDHBA51... | 512 GB | 24      | 58    | 0     | 0.16   |
| HP        | SSD EX950          | 1 TB   | 8       | 58    | 0     | 0.16   |
| HP        | SSD EX900          | 1 TB   | 7       | 202   | 6     | 0.16   |
| Samsung   | MZVLB512HAJQ-00000 | 512 GB | 81      | 58    | 1     | 0.16   |
| Intel     | SSDPEKKF010T8L     | 1 TB   | 24      | 62    | 8     | 0.16   |
| Samsung   | PM981 NVMe         | 512 GB | 35      | 60    | 1     | 0.16   |
| UMIS      | RPJTJ512MEE1OWX    | 512 GB | 17      | 57    | 0     | 0.16   |
| KIOXIA    | KBG40ZNS128G NVMe  | 128 GB | 4       | 57    | 0     | 0.16   |
| KIOXIA... | SSD                | 500 GB | 5       | 56    | 0     | 0.16   |
| Transcend | TS512GMTE110S      | 512 GB | 7       | 56    | 0     | 0.16   |
| ADATA     | SX8100NP           | 256 GB | 2       | 56    | 0     | 0.16   |
| SK hynix  | BC501 NVMe         | 256 GB | 14      | 56    | 0     | 0.16   |
| SK hynix  | PC601A NVMe        | 1 TB   | 2       | 56    | 0     | 0.15   |
| Intel     | SSDPEMKF512G8 NVMe | 512 GB | 14      | 56    | 0     | 0.15   |
| Samsung   | PM981a NVMe        | 1 TB   | 25      | 56    | 0     | 0.15   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 16      | 56    | 0     | 0.15   |
| SK hynix  | PC401 NVMe         | 512 GB | 38      | 86    | 2     | 0.15   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 47      | 55    | 0     | 0.15   |
| Toshiba   | KBG40ZPZ256G ME... | 256 GB | 1       | 55    | 0     | 0.15   |
| Seagate   | BarraCuda 510 S... | 256 GB | 1       | 55    | 0     | 0.15   |
| Intel     | SSDPEKNW010T9      | 1 TB   | 21      | 55    | 0     | 0.15   |
| Gigabyte  | GP-GSM2NE3100TNTD  | 1 TB   | 13      | 55    | 0     | 0.15   |
| SK hynix  | PC401 HFS256GD9... | 256 GB | 13      | 55    | 0     | 0.15   |
| Phison    | Sabrent Rocket ... | 1 TB   | 15      | 55    | 0     | 0.15   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 44      | 54    | 0     | 0.15   |
| ADATA     | SX6000LNP          | 512 GB | 6       | 54    | 0     | 0.15   |
| SK hynix  | PC601 HFS512GD9... | 512 GB | 13      | 54    | 0     | 0.15   |
| Kingston  | RBUSNS8154P3102... | 1 TB   | 1       | 53    | 0     | 0.15   |
| SanDisk   | WD_BLACK SN850     | 500 GB | 2       | 53    | 0     | 0.15   |
| Samsung   | MZVLB512HAJQ-000H1 | 512 GB | 67      | 53    | 0     | 0.15   |
| WDC       | PC SN720 SDAQNT... | 256 GB | 10      | 53    | 0     | 0.15   |
| Silico... | S2000              | 2 TB   | 4       | 53    | 0     | 0.15   |
| WDC       | PC SN520 SDAPMU... | 256 GB | 38      | 52    | 0     | 0.14   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 22      | 52    | 0     | 0.14   |
| Seagate   | FireCuda 520 SS... | 2 TB   | 10      | 52    | 0     | 0.14   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 20      | 52    | 0     | 0.14   |
| UMIS      | RPJTJ128MED1MWX    | 128 GB | 3       | 66    | 31    | 0.14   |
| Kingston  | SA1000M8240G       | 240 GB | 23      | 52    | 0     | 0.14   |
| INDMEM    | SSD DMPG3N         | 1 TB   | 1       | 313   | 5     | 0.14   |
| WDC       | WDS250G2B0C-00PXH0 | 250 GB | 26      | 52    | 0     | 0.14   |
| Apple     | SSD SM2048L        | 2 TB   | 1       | 52    | 0     | 0.14   |
| XrayDisk  | 256GB              | 256 GB | 3       | 52    | 0     | 0.14   |
| Samsung   | MZVLB1T0HBLR-00000 | 1 TB   | 35      | 52    | 0     | 0.14   |
| UMIS      | RPJTJ128MEE1MWX    | 128 GB | 4       | 51    | 0     | 0.14   |
| WDC       | PC SN520 SDAPMU... | 512 GB | 33      | 51    | 0     | 0.14   |
| Smartbuy  | m.2 PS5012-2280    | 256 GB | 2       | 51    | 0     | 0.14   |
| WDC       | PC SN720 SDAPNT... | 1 TB   | 13      | 51    | 0     | 0.14   |
| Samsung   | KUS020203M-B000    | 128 GB | 3       | 51    | 0     | 0.14   |
| SK hynix  | BA HFS256GD9TNG... | 256 GB | 4       | 51    | 0     | 0.14   |
| Toshiba   | KXG60ZNV512G       | 512 GB | 28      | 51    | 0     | 0.14   |
| Intel     | SSDPEKNW512G8H     | 512 GB | 143     | 50    | 1     | 0.14   |
| WDC       | WDBRPG5000ANC-WRSN | 500 GB | 8       | 50    | 0     | 0.14   |
| SK hynix  | SHGP31-1000GM-2    | 1 TB   | 16      | 50    | 0     | 0.14   |
| OSCOO     | OSC PCIe           | 256 GB | 2       | 50    | 0     | 0.14   |
| Samsung   | MZ1LB960HAJQ-00007 | 960 GB | 2       | 50    | 0     | 0.14   |
| SK hynix  | PC401 NVMe         | 1 TB   | 9       | 56    | 1     | 0.14   |
| Samsung   | MZFLW1T0HMLH-000MU | 1 TB   | 2       | 49    | 0     | 0.14   |
| SPCC      | M.2 PCIE SSD       | 512 GB | 3       | 72    | 337   | 0.14   |
| HP        | SSD EX950          | 512 GB | 4       | 49    | 0     | 0.14   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 13      | 49    | 0     | 0.14   |
| HP        | SSD EX950          | 2 TB   | 7       | 49    | 0     | 0.14   |
| SK hynix  | PC711 HFS512GDE... | 512 GB | 4       | 49    | 0     | 0.14   |
| Crucial   | CT500P2SSD8        | 500 GB | 59      | 49    | 0     | 0.13   |
| WDC       | PC SN520 NVMe      | 512 GB | 19      | 48    | 0     | 0.13   |
| Samsung   | MZVLB256HAHQ-00000 | 256 GB | 42      | 48    | 0     | 0.13   |
| Corsair   | MP400              | 2 TB   | 5       | 48    | 0     | 0.13   |
| SK hynix  | PC611 NVMe         | 256 GB | 3       | 48    | 0     | 0.13   |
| KIOXIA    | KBG40ZNS512G NVMe  | 512 GB | 74      | 47    | 0     | 0.13   |
| Team      | TM8FP6001T         | 1 TB   | 7       | 47    | 0     | 0.13   |
| Solid ... | CL1-3D512-Q11 N... | 512 GB | 2       | 47    | 0     | 0.13   |
| Samsung   | MZVLB1T0HALR-000L2 | 1 TB   | 17      | 50    | 2     | 0.13   |
| SK hynix  | HFM128GDHTNG-8310A | 128 GB | 11      | 47    | 0     | 0.13   |
| Corsair   | MP400              | 1 TB   | 5       | 47    | 0     | 0.13   |
| Kingston  | OM8PCP3512F-AB     | 512 GB | 38      | 46    | 0     | 0.13   |
| WDC       | PC SN520 SDAPMU... | 128 GB | 9       | 46    | 0     | 0.13   |
| Intel     | SSDPEK1W060GA      | 64 GB  | 2       | 46    | 0     | 0.13   |
| Kingston  | RBUSNS8154P3128GJ  | 128 GB | 17      | 46    | 0     | 0.13   |
| Intel     | SSDPEKKW256G8L     | 256 GB | 3       | 46    | 0     | 0.13   |
| ADATA     | SX6000PNP          | 512 GB | 10      | 46    | 13    | 0.13   |
| Intel     | SSDPE2KE020T7      | 2 TB   | 4       | 46    | 0     | 0.13   |
| Toshiba   | KXG6AZNV512G       | 512 GB | 35      | 46    | 0     | 0.13   |
| Apacer    | AS2280P4           | 512 GB | 3       | 46    | 0     | 0.13   |
| SSSTC     | CL1-4D256-D22      | 256 GB | 1       | 46    | 0     | 0.13   |
| Silico... | NE-256             | 256 GB | 16      | 45    | 0     | 0.13   |
| Samsung   | SSD 970 EVO Plus   | 500 GB | 413     | 45    | 0     | 0.12   |
| SanDisk   | SN730 SDBQNTY-5... | 512 GB | 1       | 45    | 0     | 0.12   |
| Hikvision | HS-SSD-E2000       | 512 GB | 1       | 45    | 0     | 0.12   |
| Silico... | FPI1TBMWR7         | 1 TB   | 1       | 45    | 0     | 0.12   |
| Gigabyte  | GP-ASM2NE6500GTTD  | 500 GB | 5       | 45    | 0     | 0.12   |
| Netac     | NVMe SSD           | 1 TB   | 5       | 45    | 0     | 0.12   |
| Kingston  | SNVS2000G          | 2 TB   | 5       | 44    | 0     | 0.12   |
| Samsung   | MZVLB2T0HALB-000L7 | 2 TB   | 9       | 44    | 0     | 0.12   |
| Zheino    | CHN-NGFFNV2280-256 | 256 GB | 2       | 44    | 0     | 0.12   |
| Gigabyte  | GP-ASM2NE6200TTTD  | 2 TB   | 6       | 43    | 0     | 0.12   |
| Phison    | E12-512G-PHISON... | 512 GB | 2       | 43    | 0     | 0.12   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 1       | 43    | 0     | 0.12   |
| SSSTC     | CL1-4D512          | 512 GB | 5       | 43    | 0     | 0.12   |
| SanDisk   | Ultra 3D NVMe      | 1 TB   | 21      | 42    | 0     | 0.12   |
| SK hynix  | SHGP31-500GM-2     | 500 GB | 5       | 42    | 0     | 0.12   |
| Lenovo    | LENSE30256GMSP3... | 256 GB | 9       | 42    | 0     | 0.12   |
| Hikvision | HS-SSD-C2000Pro... | 1 TB   | 3       | 42    | 0     | 0.12   |
| UMIS      | RPFTJ128PDD2EWX    | 128 GB | 8       | 42    | 0     | 0.12   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 9       | 42    | 0     | 0.12   |
| Apple     | SSD AP1024M        | 1 TB   | 2       | 42    | 0     | 0.12   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 13      | 41    | 0     | 0.11   |
| Crucial   | CT1000P2SSD8       | 1 TB   | 43      | 41    | 0     | 0.11   |
| ADATA     | SX8200PNP-512GT-S  | 512 GB | 1       | 41    | 0     | 0.11   |
| Samsung   | Portable SSD X5    | 500 GB | 1       | 41    | 0     | 0.11   |
| ADATA     | FALCON             | 256 GB | 2       | 41    | 0     | 0.11   |
| Silico... | Asgard AN512NVM... | 512 GB | 1       | 41    | 0     | 0.11   |
| Gigabyte  | GP-GSM2NE3256GNTD  | 256 GB | 13      | 41    | 0     | 0.11   |
| ADATA     | SX6000NP           | 512 GB | 3       | 41    | 0     | 0.11   |
| XPG       | SPECTRIX S40G      | 1 TB   | 14      | 57    | 145   | 0.11   |
| Intel     | HBRPEKNX0202AO     | 32 GB  | 18      | 40    | 0     | 0.11   |
| SK hynix  | SKHynix_HFM512G... | 512 GB | 15      | 40    | 0     | 0.11   |
| Toshiba   | KXG60ZNV512G KI... | 512 GB | 11      | 40    | 0     | 0.11   |
| WDC       | WDS500G1X0E-00AFY0 | 500 GB | 15      | 42    | 1     | 0.11   |
| Phison    | Sabrent Rocket ... | 1 TB   | 9       | 40    | 0     | 0.11   |
| WDC       | PC SN730 NVMe      | 256 GB | 3       | 40    | 0     | 0.11   |
| Toshiba   | KBG30ZMT256G       | 256 GB | 15      | 39    | 0     | 0.11   |
| Silico... | GV1TB              | 1 TB   | 1       | 39    | 0     | 0.11   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 19      | 39    | 0     | 0.11   |
| Samsung   | SSD 970 EVO Plus   | 1 TB   | 432     | 39    | 1     | 0.11   |
| Silico... | 1TB                | 1 TB   | 1       | 38    | 0     | 0.11   |
| Kingston  | SNVS1000G          | 1 TB   | 4       | 38    | 0     | 0.10   |
| SK hynix  | HFM512GDHTNG-8310A | 512 GB | 6       | 38    | 0     | 0.10   |
| Silico... | NVME SSD           | 128 GB | 9       | 38    | 0     | 0.10   |
| SPCC      | M.2 PCIE SSD       | 2 TB   | 1       | 38    | 0     | 0.10   |
| KIOXIA    | KBG40ZPZ1T02 NVMe  | 1 TB   | 12      | 37    | 0     | 0.10   |
| SK hynix  | SKHynix_HFS001T... | 1 TB   | 25      | 37    | 0     | 0.10   |
| Toshiba   | KBG30ZPZ128G       | 128 GB | 8       | 38    | 2     | 0.10   |
| Samsung   | PM971 NVMe         | 256 GB | 1       | 37    | 0     | 0.10   |
| SK hynix  | HFM512GD3JX016N    | 512 GB | 7       | 36    | 0     | 0.10   |
| Samsung   | MZVLB256HAHQ-000L2 | 256 GB | 23      | 36    | 0     | 0.10   |
| Toshiba   | KXG50PNV2T04 NV... | 2 TB   | 2       | 36    | 0     | 0.10   |
| Gigabyte  | GP-AG41TB          | 1 TB   | 9       | 36    | 0     | 0.10   |
| Intel     | HBRPEKNX0202A      | 512 GB | 19      | 36    | 0     | 0.10   |
| WDC       | PC SN730 SDBQNT... | 1 TB   | 3       | 36    | 0     | 0.10   |
| SK hynix  | SKHynix_HFM256G... | 256 GB | 5       | 35    | 0     | 0.10   |
| SK hynix  | HFB1M8MO331C0MR    | 256 GB | 1       | 35    | 0     | 0.10   |
| Apple     | SSD AP1024J        | 1 TB   | 1       | 35    | 0     | 0.10   |
| Dell      | Ent NVMe AGN RI... | 3.8 TB | 1       | 35    | 0     | 0.10   |
| WDC       | PC SN520 SDAPMU... | 512 GB | 2       | 35    | 0     | 0.10   |
| Crucial   | CT2000P2SSD8       | 2 TB   | 8       | 35    | 0     | 0.10   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 2       | 35    | 0     | 0.10   |
| Apple     | SSD SM1024L        | 1 TB   | 2       | 35    | 0     | 0.10   |
| WDC       | PC SN730 SDBPNT... | 256 GB | 2       | 34    | 0     | 0.10   |
| Silico... | KLLISRE            | 128 GB | 1       | 34    | 0     | 0.10   |
| Intel     | MEMPEK1W016GAL     | 16 GB  | 1       | 34    | 0     | 0.10   |
| SSSTC     | CL1-3D512-Q11 NVMe | 512 GB | 6       | 34    | 0     | 0.10   |
| Seagate   | FireCuda 530 ZP... | 500 GB | 1       | 34    | 0     | 0.10   |
| SK hynix  | HFS512GD9TNG-L2A0A | 512 GB | 5       | 34    | 0     | 0.10   |
| ADATA     | SX6000PNP          | 1 TB   | 12      | 36    | 49    | 0.09   |
| Silico... | NE-128             | 128 GB | 10      | 34    | 0     | 0.09   |
| SK hynix  | BC711 NVMe         | 256 GB | 10      | 34    | 0     | 0.09   |
| Toshiba   | KBG40ZNT512G ME... | 512 GB | 37      | 34    | 0     | 0.09   |
| UMIS      | RPJTJ256MEE1OWX    | 256 GB | 24      | 34    | 0     | 0.09   |
| SK hynix  | BC501 NVMe         | 128 GB | 6       | 34    | 0     | 0.09   |
| Apple     | SSD SM0512L        | 500 GB | 5       | 33    | 0     | 0.09   |
| FORESEE   | P900F128GBH        | 128 GB | 2       | 33    | 0     | 0.09   |
| Phison    | Sabrent ROCKET-PRO | 512 GB | 1       | 33    | 0     | 0.09   |
| Micron    | 7300_MTFDHBE3T8TDF | 3.8 TB | 4       | 33    | 0     | 0.09   |
| Samsung   | SSD 970 EVO Plus   | 250 GB | 174     | 33    | 0     | 0.09   |
| Silico... | NVMe SSD           | 1 TB   | 1       | 33    | 0     | 0.09   |
| Apple     | SSD SM0032L        | 32 GB  | 21      | 33    | 0     | 0.09   |
| Samsung   | MZVLB512HBJQ-00000 | 512 GB | 30      | 33    | 0     | 0.09   |
| Intel     | MEMPEK1J032GA      | 32 GB  | 1       | 33    | 0     | 0.09   |
| XPG       | SX8200PNP-512GT-S  | 512 GB | 2       | 33    | 0     | 0.09   |
| Seagate   | FireCuda 530 ZP... | 4 TB   | 1       | 33    | 0     | 0.09   |
| Silico... | NVME SSD           | 256 GB | 2       | 33    | 0     | 0.09   |
| WDC       | PC SN720 SDAQNT... | 512 GB | 2       | 32    | 0     | 0.09   |
| Silico... | EX-512 PRO         | 512 GB | 1       | 32    | 0     | 0.09   |
| Plextor   | PX-1TM10PG         | 1 TB   | 1       | 32    | 0     | 0.09   |
| Gigabyte  | GP-GSM2NE3512GNTD  | 512 GB | 6       | 32    | 0     | 0.09   |
| Apple     | SSD AP2048M        | 2 TB   | 2       | 32    | 0     | 0.09   |
| WDC       | WDS100T1X0E-00AFY0 | 1 TB   | 37      | 32    | 0     | 0.09   |
| ADATA     | IM2P33F3 NVMe      | 256 GB | 12      | 32    | 1     | 0.09   |
| Lenovo    | LENSN20256GMSP3... | 256 GB | 2       | 32    | 0     | 0.09   |
| Intel     | SSDPEL1K100GA      | 100 GB | 2       | 58    | 5     | 0.09   |
| Seagate   | BarraCuda Q5 ZP... | 2 TB   | 1       | 32    | 0     | 0.09   |
| XPG       | GAMMIX S70 BLADE   | 1 TB   | 3       | 32    | 0     | 0.09   |
| Apple     | SSD AP8192N        | 8 TB   | 2       | 31    | 0     | 0.09   |
| Kingston  | OM8PDP3256B-AA1    | 256 GB | 1       | 31    | 0     | 0.09   |
| SSSTC     | CL1-8D256-HP       | 256 GB | 8       | 31    | 0     | 0.09   |
| Samsung   | MZVLB256HAHQ-00007 | 256 GB | 2       | 31    | 0     | 0.09   |
| UMIS      | LENSE40256GMSP3... | 256 GB | 2       | 31    | 0     | 0.09   |
| Samsung   | MZVLB256HAHQ-000H1 | 256 GB | 49      | 31    | 0     | 0.09   |
| Huawei    | HWE52P433T2M005N   | 3.2 TB | 4       | 31    | 0     | 0.09   |
| Samsung   | KLFGGAR4AA-K0T0    | 1 TB   | 1       | 31    | 0     | 0.09   |
| WDC       | PC SN520 SDAPMU... | 512 GB | 8       | 34    | 10    | 0.08   |
| Lite-On   | CA5-8D512          | 512 GB | 8       | 30    | 0     | 0.08   |
| WDC       | CL SN520 SDAPMU... | 512 GB | 1       | 30    | 0     | 0.08   |
| WDC       | PC SN720 SDAQNT... | 1 TB   | 3       | 30    | 0     | 0.08   |
| SK hynix  | HFM512GD3JX013N    | 512 GB | 26      | 30    | 0     | 0.08   |
| Kingston  | SNVS1000GB         | 1 TB   | 13      | 30    | 0     | 0.08   |
| Kingston  | OM8PCP3512F-AA     | 512 GB | 20      | 29    | 0     | 0.08   |
| Crucial   | CT500P5SSD8        | 500 GB | 26      | 29    | 0     | 0.08   |
| Samsung   | MZVLB256HBHQ-000L2 | 256 GB | 28      | 29    | 0     | 0.08   |
| Toshiba   | KBG40ZMT128G ME... | 128 GB | 11      | 29    | 0     | 0.08   |
| Silico... | JAMESDONKEY JD512  | 512 GB | 1       | 28    | 0     | 0.08   |
| Lite-On   | CA1-8D128-HP       | 128 GB | 5       | 28    | 0     | 0.08   |
| Apple     | SSD AP0512H        | 500 GB | 1       | 28    | 0     | 0.08   |
| Phison    | Reletech P400 SSD  | 512 GB | 3       | 28    | 0     | 0.08   |
| Kingston  | RBUSNS8154P3512GJ  | 512 GB | 13      | 28    | 0     | 0.08   |
| Toshiba   | KXG60ZNV512G NV... | 512 GB | 18      | 28    | 0     | 0.08   |
| Seagate   | FireCuda 510 SS... | 2 TB   | 2       | 28    | 0     | 0.08   |
| KingFast  | 1TB                | 1 TB   | 2       | 27    | 0     | 0.08   |
| Samsung   | MZVLW1T0HMLH-000H1 | 1 TB   | 2       | 27    | 0     | 0.08   |
| SSSTC     | CL1-4D256          | 256 GB | 12      | 27    | 0     | 0.08   |
| Mushkin   | MKNSSDHL1TB-D8     | 1 TB   | 4       | 64    | 19    | 0.08   |
| Corsair   | Force MP300        | 240 GB | 2       | 27    | 0     | 0.07   |
| Kingston  | OM3PDP3-AD NVMe... | 256 GB | 7       | 27    | 0     | 0.07   |
| Micron    | 2210_MTFDHBA512QFD | 512 GB | 34      | 27    | 0     | 0.07   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 8       | 27    | 0     | 0.07   |
| UMIS      | RPFTJ256PDD2MWX    | 256 GB | 7       | 27    | 0     | 0.07   |
| WDC       | WD BLACK SDBPNT... | 512 GB | 2       | 27    | 0     | 0.07   |
| Samsung   | MZVLB1T0HALR-000H1 | 1 TB   | 12      | 27    | 0     | 0.07   |
| Apple     | SSD AP0512M        | 500 GB | 8       | 26    | 0     | 0.07   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 15      | 26    | 0     | 0.07   |
| SK hynix  | PC711 NVMe         | 512 GB | 24      | 26    | 0     | 0.07   |
| Phison    | APS-SE20G-1T       | 1 TB   | 1       | 26    | 0     | 0.07   |
| Phison    | Sabrent Rocket Q4  | 1 TB   | 3       | 26    | 0     | 0.07   |
| Samsung   | MZVLB256HBHQ-000   | 256 GB | 4       | 26    | 0     | 0.07   |
| Samsung   | PM981a NVMe        | 256 GB | 2       | 26    | 0     | 0.07   |
| Toshiba   | KBG30ZMV128G       | 128 GB | 2       | 26    | 0     | 0.07   |
| Toshiba   | KXG60ZNV256G KI... | 256 GB | 8       | 26    | 0     | 0.07   |
| WDC       | PC SN730 NVMe      | 512 GB | 24      | 26    | 0     | 0.07   |
| WDC       | WDS100T2B0C        | 1 TB   | 8       | 26    | 0     | 0.07   |
| SK hynix  | BC501 HFM256GDJ... | 256 GB | 40      | 26    | 53    | 0.07   |
| Mushkin   | MKNSSDPE1TB-D8     | 1 TB   | 2       | 26    | 0     | 0.07   |
| Samsung   | PM981a NVMe        | 2 TB   | 20      | 26    | 0     | 0.07   |
| SK hynix  | HFM256GDHTNG-8510B | 256 GB | 8       | 26    | 0     | 0.07   |
| Samsung   | MZVPW256HEGL-000L7 | 256 GB | 1       | 25    | 0     | 0.07   |
| Plextor   | PX-256M8PeG        | 256 GB | 2       | 140   | 503   | 0.07   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 18      | 25    | 0     | 0.07   |
| Samsung   | MZQLB1T9HAJR-00007 | 1.9 TB | 10      | 25    | 0     | 0.07   |
| Phison    | E12-512G-PHISON... | 512 GB | 2       | 25    | 0     | 0.07   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 25      | 25    | 0     | 0.07   |
| Corsair   | Force MP510        | 4 TB   | 2       | 25    | 0     | 0.07   |
| WDC       | PC SN530 SDBPNP... | 1 TB   | 8       | 25    | 0     | 0.07   |
| Plextor   | PX-256M8PeGN       | 256 GB | 2       | 25    | 0     | 0.07   |
| SK hynix  | BC501 NVMe         | 512 GB | 7       | 25    | 0     | 0.07   |
| Kingch... | 512GB              | 512 GB | 1       | 25    | 0     | 0.07   |
| WDC       | WDS200T2B0C-00PXH0 | 2 TB   | 8       | 25    | 0     | 0.07   |
| Lite-On   | CA3-8D128-HP       | 128 GB | 4       | 25    | 0     | 0.07   |
| SK hynix  | HFS512GD9TNG-62A0A | 512 GB | 7       | 25    | 0     | 0.07   |
| Toshiba   | KBG30ZMV256G KI... | 256 GB | 17      | 25    | 0     | 0.07   |
| Seagate   | FireCuda 530 ZP... | 2 TB   | 3       | 24    | 0     | 0.07   |
| Samsung   | MZVLQ1T0HALB-00000 | 1 TB   | 12      | 24    | 0     | 0.07   |
| Samsung   | MZVLB256HBHQ-00000 | 256 GB | 23      | 24    | 0     | 0.07   |
| Union ... | UMIS LENSE40512... | 512 GB | 1       | 24    | 0     | 0.07   |
| WDC       | PC SN730 SDBPNT... | 256 GB | 9       | 24    | 0     | 0.07   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 5       | 24    | 0     | 0.07   |
| SanDisk   | WD_BLACK SN850     | 1 TB   | 3       | 24    | 0     | 0.07   |
| Crucial   | CT1000P5SSD8       | 1 TB   | 20      | 24    | 0     | 0.07   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 3       | 40    | 3     | 0.07   |
| KIOXIA    | KXG7AZNV1T02 LA    | 1 TB   | 1       | 24    | 0     | 0.07   |
| Silico... | ShiJi 512GB M.2... | 512 GB | 1       | 24    | 0     | 0.07   |
| Toshiba   | KXG6AZNV1T02       | 1 TB   | 12      | 23    | 0     | 0.07   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 23      | 23    | 0     | 0.06   |
| Lite-On   | CA5-8D256          | 256 GB | 1       | 23    | 0     | 0.06   |
| ADATA     | SWORDFISH          | 1 TB   | 13      | 23    | 0     | 0.06   |
| WDC       | WDS500G2B0C        | 500 GB | 6       | 23    | 0     | 0.06   |
| Samsung   | MZVLB256HBHQ-00A00 | 256 GB | 1       | 23    | 0     | 0.06   |
| SSSTC     | CL1-8D256          | 256 GB | 6       | 23    | 0     | 0.06   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 3       | 23    | 0     | 0.06   |
| SK hynix  | BC711 NVMe         | 512 GB | 24      | 23    | 0     | 0.06   |
| SK hynix  | HFM001TD3JX013N    | 1 TB   | 42      | 22    | 0     | 0.06   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 30      | 22    | 0     | 0.06   |
| XPG       | GAMMIX S5          | 1 TB   | 11      | 22    | 0     | 0.06   |
| KLEVV     | CRAS C710 M.2 N... | 1 TB   | 1       | 22    | 0     | 0.06   |
| Apple     | SSD SM0256L        | 256 GB | 11      | 22    | 0     | 0.06   |
| Samsung   | MZVLB512HBJQ-000H1 | 512 GB | 46      | 22    | 0     | 0.06   |
| Star D... | PCIe SSD           | 480 GB | 8       | 22    | 0     | 0.06   |
| Samsung   | SSD 980 PRO        | 500 GB | 63      | 22    | 0     | 0.06   |
| SK hynix  | HFS256GD9TNG-L2A0A | 256 GB | 1       | 22    | 0     | 0.06   |
| Samsung   | MZVLB1T0HALR-000H2 | 1 TB   | 1       | 22    | 0     | 0.06   |
| SSSTC     | CL1-4D128          | 128 GB | 2       | 21    | 0     | 0.06   |
| Samsung   | SSD 970 EVO Plus   | 2 TB   | 140     | 22    | 1     | 0.06   |
| Apple     | SSD SM0128L        | 121 GB | 2       | 21    | 0     | 0.06   |
| WDC       | PC SN730 SDBQNT... | 512 GB | 105     | 21    | 0     | 0.06   |
| Silico... | IM2P33F8BR1-512GB  | 512 GB | 2       | 21    | 0     | 0.06   |
| Samsung   | PM991 NVMe         | 256 GB | 16      | 21    | 0     | 0.06   |
| SK hynix  | HFM256GDJTNI-82A0A | 256 GB | 9       | 21    | 0     | 0.06   |
| Samsung   | KUS040205M-B001    | 512 GB | 1       | 21    | 0     | 0.06   |
| Micron    | 2200_MTFDHBA512TCK | 512 GB | 8       | 21    | 0     | 0.06   |
| XPG       | GAMMIX S50 Lite    | 1 TB   | 4       | 21    | 0     | 0.06   |
| Intel     | SSDPEBKF256G7      | 256 GB | 1       | 21    | 0     | 0.06   |
| Silico... | R5MP240G8          | 240 GB | 2       | 21    | 0     | 0.06   |
| Samsung   | MZVLB256HBHQ-00007 | 256 GB | 2       | 20    | 0     | 0.06   |
| KIOXIA    | KBG40ZNV256G       | 256 GB | 46      | 20    | 0     | 0.06   |
| Seagate   | IronWolf510 ZP9... | 960 GB | 3       | 20    | 0     | 0.06   |
| Apple     | SSD AP0256J        | 256 GB | 11      | 20    | 0     | 0.06   |
| Kingston  | OM8PCP3512F-AI1    | 512 GB | 35      | 20    | 0     | 0.06   |
| Solid ... | SSSTC CL1-8D512    | 512 GB | 1       | 20    | 0     | 0.06   |
| Samsung   | MZFLW512HMJP-000MV | 512 GB | 1       | 20    | 0     | 0.06   |
| Samsung   | MZVLB1T0HBLR-000H1 | 1 TB   | 35      | 20    | 0     | 0.06   |
| Samsung   | SSD 970 EVO        | 2 TB   | 11      | 152   | 52    | 0.05   |
| Silico... | OSC PCIE           | 512 GB | 1       | 19    | 0     | 0.05   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 7       | 19    | 0     | 0.05   |
| Seagate   | XP800HE30012       | 800 GB | 1       | 19    | 0     | 0.05   |
| WDC       | PC SN530 SDBPNP... | 1 TB   | 8       | 19    | 0     | 0.05   |
| Union ... | RPFTJ128PDD2EWX    | 128 GB | 25      | 19    | 0     | 0.05   |
| Samsung   | MZVLB512HBJQ-000H7 | 512 GB | 6       | 19    | 0     | 0.05   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 23      | 19    | 0     | 0.05   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 1       | 19    | 0     | 0.05   |
| KIOXIA    | KXG70PNV2T04 NVMe  | 2 TB   | 6       | 19    | 0     | 0.05   |
| SK hynix  | VO003840KXAVQ      | 3.8 TB | 1       | 19    | 0     | 0.05   |
| Samsung   | MZVLB1T0HBLR-000L2 | 1 TB   | 70      | 18    | 0     | 0.05   |
| Samsung   | MZVLB512HBJQ-00007 | 512 GB | 3       | 18    | 0     | 0.05   |
| Samsung   | MZVLQ512HALU-00000 | 512 GB | 59      | 18    | 0     | 0.05   |
| Silico... | NVMe SSD 256G      | 256 GB | 1       | 18    | 0     | 0.05   |
| SK hynix  | HFM256GDJTNG-8310A | 256 GB | 43      | 18    | 0     | 0.05   |
| Netac     | NVMe SSD           | 512 GB | 2       | 18    | 0     | 0.05   |
| Seagate   | FireCuda 530 ZP... | 4 TB   | 2       | 18    | 0     | 0.05   |
| UMIS      | RPITJ512VME2OWD    | 512 GB | 3       | 18    | 0     | 0.05   |
| Lite-On   | CL1-3D256-Q11 NVMe | 256 GB | 4       | 18    | 0     | 0.05   |
| Union ... | RPFTJ256PDD2MWX    | 256 GB | 13      | 18    | 0     | 0.05   |
| SK hynix  | PC711 NVMe         | 1 TB   | 33      | 18    | 0     | 0.05   |
| SSSTC     | CA5-8D512-Q79      | 512 GB | 1       | 18    | 0     | 0.05   |
| HP        | SSD EX900          | 120 GB | 3       | 18    | 0     | 0.05   |
| SK hynix  | SHGP31-500GM       | 500 GB | 1       | 18    | 0     | 0.05   |
| Apple     | SSD AP0032H        | 24 GB  | 3       | 18    | 0     | 0.05   |
| KIOXIA    | KBG30ZMV512G       | 512 GB | 1       | 18    | 0     | 0.05   |
| SanDisk   | Extreme Pro        | 2 TB   | 1       | 18    | 0     | 0.05   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 15      | 18    | 0     | 0.05   |
| Kingston  | OM3PDP3-AD NVMe... | 512 GB | 9       | 18    | 0     | 0.05   |
| SK hynix  | HFM256GDHTNG-8310A | 256 GB | 12      | 18    | 0     | 0.05   |
| Phytium   | S1200CYX1-T0M22... | 256 GB | 1       | 18    | 0     | 0.05   |
| Kingston  | RBUSNS8154P3256GJ1 | 256 GB | 30      | 18    | 0     | 0.05   |
| Samsung   | MZVL2512HCJQ-00B   | 512 GB | 1       | 17    | 0     | 0.05   |
| Samsung   | PM991 NVMe         | 512 GB | 13      | 17    | 0     | 0.05   |
| ADATA     | FALCON             | 2 TB   | 2       | 17    | 0     | 0.05   |
| Silico... | SSD_M.2_PCI_NVM... | 1 TB   | 2       | 17    | 0     | 0.05   |
| ADATA     | SX6000LNP          | 256 GB | 7       | 17    | 0     | 0.05   |
| Samsung   | MZVL22T0HBLB-00BL7 | 2 TB   | 1       | 17    | 0     | 0.05   |
| Union ... | UMIS RPJTJ512ME... | 512 GB | 10      | 17    | 0     | 0.05   |
| Samsung   | MZVLB512HBJQ-000L2 | 512 GB | 83      | 17    | 0     | 0.05   |
| Samsung   | MZVLQ256HAJD-000H1 | 256 GB | 58      | 17    | 0     | 0.05   |
| SK hynix  | SKHynix_HFM128G... | 128 GB | 2       | 17    | 0     | 0.05   |
| Lenovo    | RPITJ256VFD2MWX    | 256 GB | 1       | 17    | 0     | 0.05   |
| Samsung   | PM981a NVMe        | 512 GB | 27      | 17    | 0     | 0.05   |
| Intel     | SSDPEKNU512GZ      | 512 GB | 22      | 17    | 0     | 0.05   |
| Union ... | UMIS RPJTJ1TBME... | 1 TB   | 1       | 17    | 0     | 0.05   |
| Phison    | 1TB SM2801T24GK... | 1 TB   | 12      | 16    | 0     | 0.05   |
| SK hynix  | SKHynix_HFS001T... | 1 TB   | 20      | 16    | 0     | 0.05   |
| Samsung   | MZVLB256HBHQ-000L7 | 256 GB | 62      | 16    | 0     | 0.04   |
| Silico... | KingSSD-N201000    | 1 TB   | 1       | 16    | 0     | 0.04   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 2       | 16    | 0     | 0.04   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 4       | 16    | 0     | 0.04   |
| KIOXIA    | KBG40ZNV1T02       | 1 TB   | 19      | 16    | 0     | 0.04   |
| Colorful  | CN600S             | 480 GB | 1       | 16    | 0     | 0.04   |
| Toshiba   | KBG40ZNV256G ME... | 256 GB | 3       | 16    | 0     | 0.04   |
| SK hynix  | BC501 HFM512GDJ... | 512 GB | 25      | 16    | 0     | 0.04   |
| Samsung   | MZVLB1T0HBLR-000L7 | 1 TB   | 86      | 16    | 0     | 0.04   |
| Intel     | H10 HBRPEKNX020... | 1 TB   | 2       | 15    | 0     | 0.04   |
| Samsung   | MZVLQ1T0HALB-000H1 | 1 TB   | 13      | 15    | 0     | 0.04   |
| Toshiba   | KBG20ZMS128G NVMe  | 128 GB | 1       | 15    | 0     | 0.04   |
| SK hynix  | BA HFS512GD9TNG... | 512 GB | 1       | 15    | 0     | 0.04   |
| ADATA     | IM2P33F3 NVMe      | 512 GB | 5       | 15    | 0     | 0.04   |
| Kingston  | RBUSNS8154P3128GJ1 | 128 GB | 10      | 15    | 0     | 0.04   |
| Samsung   | MZALQ256HAJD-000L2 | 256 GB | 61      | 14    | 0     | 0.04   |
| KIOXIA... | PLUS G2 SSD        | 500 GB | 2       | 14    | 0     | 0.04   |
| Samsung   | MZVLB1T0HBLR-00A00 | 1 TB   | 7       | 14    | 0     | 0.04   |
| WDC       | PC SN520 SDAPMU... | 128 GB | 9       | 14    | 0     | 0.04   |
| Kingston  | OM8PCP31024F-AI1   | 1 TB   | 6       | 14    | 0     | 0.04   |
| Micron    | MTFDHBA256TCK-1... | 256 GB | 26      | 15    | 1     | 0.04   |
| ADATA     | SWORDFISH          | 500 GB | 3       | 14    | 0     | 0.04   |
| WDC       | WDBRPG0020BNC-WRSN | 2 TB   | 1       | 14    | 0     | 0.04   |
| Kingston  | SKC2500M82000G     | 2 TB   | 5       | 14    | 0     | 0.04   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 3       | 14    | 0     | 0.04   |
| Phison    | PM8512GPTCB4B8T... | 512 GB | 1       | 14    | 0     | 0.04   |
| SK hynix  | HFM512GDJTNG-8310A | 512 GB | 32      | 14    | 0     | 0.04   |
| XPG       | GAMMIX S11L        | 1 TB   | 3       | 14    | 0     | 0.04   |
| Intel     | SSDPEKNU010TZ      | 1 TB   | 14      | 14    | 0     | 0.04   |
| V-GeN     | V-GEN11SM20AR51... | 512 GB | 1       | 14    | 0     | 0.04   |
| PNY       | CS1030 2TB SSD     | 2 TB   | 2       | 14    | 0     | 0.04   |
| SK hynix  | Skhynix BC501 NVMe | 256 GB | 3       | 13    | 0     | 0.04   |
| Kingston  | OM8PDP3512B-A01    | 512 GB | 6       | 13    | 0     | 0.04   |
| Micron    | MTFDHBA512QFD      | 512 GB | 29      | 13    | 0     | 0.04   |
| Seagate   | BarraCuda 510 S... | 512 GB | 2       | 13    | 0     | 0.04   |
| Kingston  | RBUSNS8154P3512GJ3 | 512 GB | 3       | 13    | 0     | 0.04   |
| Samsung   | MZALQ512HALU-000L2 | 512 GB | 91      | 13    | 0     | 0.04   |
| Silico... | Maxsun 256GB NM... | 256 GB | 1       | 13    | 0     | 0.04   |
| KIOXIA    | KBG40ZNS1T02 NVMe  | 1 TB   | 7       | 13    | 0     | 0.04   |
| Kingston  | SNVS250G           | 250 GB | 4       | 13    | 0     | 0.04   |
| Silico... | Longline SSD       | 512 GB | 1       | 13    | 0     | 0.04   |
| Phison    | 512GB SM280512G... | 512 GB | 3       | 13    | 0     | 0.04   |
| Micron    | MTFDHBA1T0TCK      | 1 TB   | 6       | 13    | 0     | 0.04   |
| Lexar     | 500GB SSD          | 500 GB | 4       | 13    | 0     | 0.04   |
| SK hynix  | BC511 NVMe         | 512 GB | 50      | 12    | 0     | 0.04   |
| Patriot   | M.2 P300           | 512 GB | 1       | 12    | 0     | 0.04   |
| WDC       | PC SN530 NVMe      | 256 GB | 26      | 12    | 0     | 0.04   |
| SK hynix  | HFB1M8MH331C0MR    | 512 GB | 1       | 12    | 0     | 0.04   |
| WDC       | WDS200T3X0C-00SJG0 | 2 TB   | 6       | 12    | 0     | 0.04   |
| Apple     | SSD AP1024N        | 1 TB   | 10      | 12    | 0     | 0.04   |
| SK hynix  | SKHynix_HFS001T... | 1 TB   | 2       | 12    | 0     | 0.04   |
| SK hynix  | SKHynix_HFM512G... | 512 GB | 39      | 12    | 0     | 0.03   |
| WDC       | PC SN730 SDBQNT... | 1 TB   | 49      | 12    | 0     | 0.03   |
| Samsung   | MZVLB2T0HALB-000L2 | 2 TB   | 2       | 12    | 0     | 0.03   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 2       | 12    | 0     | 0.03   |
| Toshiba   | KBG40ZNT256G ME... | 256 GB | 21      | 12    | 0     | 0.03   |
| KIOXIA    | KXG70PN84T09 NVMe  | 4 TB   | 3       | 12    | 0     | 0.03   |
| ADATA     | SWORDFISH          | 250 GB | 3       | 12    | 0     | 0.03   |
| WDC       | PC SN530 SDBPNP... | 1 TB   | 1       | 12    | 0     | 0.03   |
| ADATA     | SX8200PNP-512GT    | 512 GB | 1       | 12    | 0     | 0.03   |
| Samsung   | MZVLQ256HAJD-00000 | 256 GB | 16      | 12    | 0     | 0.03   |
| Seagate   | FireCuda 510 SS... | 500 GB | 1       | 12    | 0     | 0.03   |
| Apple     | SSD AP0512J        | 500 GB | 6       | 12    | 0     | 0.03   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 13      | 12    | 0     | 0.03   |
| SK hynix  | BC511 HFM256GDJ... | 256 GB | 44      | 12    | 0     | 0.03   |
| KIOXIA    | KBG4AZNV512G       | 512 GB | 2       | 12    | 0     | 0.03   |
| Samsung   | MZVLB512HBJQ-00A00 | 512 GB | 5       | 12    | 0     | 0.03   |
| KIOXIA    | KBG40ZNV512G       | 512 GB | 73      | 11    | 0     | 0.03   |
| WDC       | PC SN730 SDBQNT... | 256 GB | 32      | 11    | 0     | 0.03   |
| Samsung   | MZWLJ1T9HBJR-00007 | 1.9 TB | 1       | 11    | 0     | 0.03   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 37      | 11    | 0     | 0.03   |
| ADATA     | SX6000LNP          | 1 TB   | 7       | 41    | 144   | 0.03   |
| Lite-On   | CL1-8D512          | 512 GB | 6       | 11    | 0     | 0.03   |
| SSSTC     | LJ1-2W7680         | 962 GB | 1       | 11    | 0     | 0.03   |
| SK hynix  | SKHynix_HFS001T... | 1 TB   | 9       | 11    | 0     | 0.03   |
| Samsung   | SSD 980 PRO        | 1 TB   | 138     | 11    | 0     | 0.03   |
| Micron    | 2300 NVMe          | 1 TB   | 38      | 11    | 0     | 0.03   |
| SK hynix  | HFM512GDHTNG-8710B | 512 GB | 26      | 11    | 0     | 0.03   |
| SK hynix  | BC711 NVMe         | 128 GB | 2       | 11    | 0     | 0.03   |
| WDC       | CL SN720 SDAQNT... | 1 TB   | 1       | 11    | 0     | 0.03   |
| Solid ... | SSSTC CL1-4D256    | 256 GB | 3       | 11    | 0     | 0.03   |
| SK hynix  | BC511 NVMe         | 256 GB | 26      | 11    | 0     | 0.03   |
| Solid ... | SSSTC CL1-8D256-HP | 256 GB | 2       | 11    | 0     | 0.03   |
| Silico... | Qunion P20A 512... | 512 GB | 1       | 10    | 0     | 0.03   |
| WDC       | PC SN730 NVMe      | 1 TB   | 47      | 10    | 0     | 0.03   |
| UDinfo    | M2P                | 512 GB | 1       | 10    | 0     | 0.03   |
| SK hynix  | PC601 HFS001TD9... | 1 TB   | 1       | 10    | 0     | 0.03   |
| Silico... | 256GB              | 256 GB | 6       | 10    | 0     | 0.03   |
| Team      | TM8FP6256G         | 256 GB | 2       | 10    | 0     | 0.03   |
| Micron    | MTFDHBA256TDV      | 256 GB | 6       | 10    | 0     | 0.03   |
| Samsung   | MZVLB512HBJQ-000L7 | 512 GB | 242     | 10    | 0     | 0.03   |
| Apple     | SSD AP0128H        | 121 GB | 79      | 10    | 0     | 0.03   |
| Kingston  | OM8PDP3256B-AI1    | 256 GB | 3       | 10    | 0     | 0.03   |
| Samsung   | SSD 980            | 1 TB   | 75      | 10    | 0     | 0.03   |
| Samsung   | PM9A1 NVMe         | 1 TB   | 19      | 10    | 0     | 0.03   |
| Micron    | MTFDHBA256TCK      | 256 GB | 5       | 10    | 0     | 0.03   |
| Micron    | 2200V_MTFDHBA25... | 256 GB | 1       | 10    | 0     | 0.03   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 49      | 10    | 0     | 0.03   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 2       | 10    | 0     | 0.03   |
| Samsung   | MZQLB3T8HALS-00007 | 3.8 TB | 2       | 10    | 0     | 0.03   |
| Samsung   | MZALQ512HALU-000L1 | 512 GB | 63      | 10    | 0     | 0.03   |
| WDC       | PC SN530 SDBPNP... | 1 TB   | 4       | 10    | 0     | 0.03   |
| SK hynix  | SKHynix_HFM256G... | 256 GB | 32      | 10    | 0     | 0.03   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 2       | 10    | 0     | 0.03   |
| Silico... | 512GB PCS PCIe ... | 512 GB | 2       | 9     | 0     | 0.03   |
| Samsung   | SSD 980 PRO        | 250 GB | 17      | 9     | 0     | 0.03   |
| Samsung   | MZVL21T0HCLR-00B00 | 1 TB   | 10      | 9     | 0     | 0.03   |
| Apple     | SSD AP0512N        | 500 GB | 18      | 9     | 0     | 0.03   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 37      | 9     | 0     | 0.03   |
| Micron    | 2200_MTFDHBA1T0TCK | 1 TB   | 5       | 9     | 0     | 0.03   |
| Union ... | UMIS RPITJ256PE... | 256 GB | 1       | 9     | 0     | 0.03   |
| Samsung   | MZVLQ512HBLU-00B00 | 512 GB | 19      | 9     | 0     | 0.03   |
| Crucial   | CT2000P5SSD8       | 2 TB   | 6       | 9     | 0     | 0.03   |
| Kingston  | SNVS500G           | 500 GB | 24      | 9     | 0     | 0.03   |
| Silico... | PCIe-8 SSD         | 512 GB | 2       | 9     | 0     | 0.03   |
| Samsung   | PM991a NVMe        | 512 GB | 15      | 9     | 0     | 0.03   |
| Samsung   | MZVLB256HBHQ-000H1 | 256 GB | 7       | 9     | 0     | 0.03   |
| WDC       | PC SN530 SDBPMP... | 512 GB | 54      | 9     | 0     | 0.03   |
| Goodram   | SSDPR-PX500-512-80 | 512 GB | 6       | 8     | 0     | 0.02   |
| Seagate   | FireCuda 510 SS... | 250 GB | 1       | 8     | 0     | 0.02   |
| Phison    | Viper M.2 VPR100   | 512 GB | 1       | 8     | 0     | 0.02   |
| Toshiba   | KBG40ZNS128G NVMe  | 128 GB | 1       | 8     | 0     | 0.02   |
| ADATA     | SX6000LNP          | 128 GB | 15      | 8     | 0     | 0.02   |
| Samsung   | MZVLQ512HALU-000H1 | 512 GB | 69      | 8     | 0     | 0.02   |
| SK hynix  | HFM128GDJTNG-8310A | 128 GB | 15      | 8     | 0     | 0.02   |
| Seagate   | BarraCuda Q5 ZP... | 500 GB | 4       | 8     | 0     | 0.02   |
| Patriot   | M.2 P300           | 256 GB | 3       | 8     | 0     | 0.02   |
| Hikvision | HS-SSD-E1000       | 128 GB | 1       | 8     | 0     | 0.02   |
| Corsair   | MP600 CORE         | 2 TB   | 3       | 8     | 0     | 0.02   |
| Samsung   | MZVLB512HBJQ-000   | 512 GB | 7       | 8     | 0     | 0.02   |
| Samsung   | MZVL2256HCHQ-00B00 | 256 GB | 1       | 8     | 0     | 0.02   |
| Micron    | 2200_MTFDHBA256TCK | 256 GB | 6       | 8     | 0     | 0.02   |
| Toshiba   | KXD51LN11T92 1.9TB | 1.9 TB | 3       | 8     | 0     | 0.02   |
| Kingston  | SKC2500M8250G      | 250 GB | 3       | 8     | 0     | 0.02   |
| KIOXIA    | KXG6AZNV512G       | 512 GB | 2       | 8     | 0     | 0.02   |
| Crucial   | CT250P5SSD8        | 250 GB | 4       | 8     | 0     | 0.02   |
| KLEVV     | CRAS C710 M.2 N... | 512 GB | 1       | 8     | 0     | 0.02   |
| Micron    | 2210_MTFDHBA1T0QFD | 1 TB   | 28      | 7     | 0     | 0.02   |
| Silico... | SPT256L2-2IAS7G2   | 256 GB | 4       | 7     | 0     | 0.02   |
| Samsung   | SSD 980 PRO        | 2 TB   | 48      | 7     | 0     | 0.02   |
| Lexar     | 250GB SSD          | 250 GB | 1       | 7     | 0     | 0.02   |
| Micron    | MTFDHBA512QFD-1... | 512 GB | 17      | 7     | 0     | 0.02   |
| SK hynix  | HFM512GDJTNI-82A0A | 512 GB | 39      | 7     | 0     | 0.02   |
| Samsung   | MZVL21T0HCLR-00BL2 | 1 TB   | 1       | 7     | 0     | 0.02   |
| Solid ... | CL1-3D128-Q11 N... | 128 GB | 1       | 7     | 0     | 0.02   |
| BIWIN     | SSD                | 1 TB   | 4       | 7     | 0     | 0.02   |
| Kingston  | SKC2500M81000G     | 1 TB   | 9       | 7     | 0     | 0.02   |
| ADATA     | IM2P33F3 NVMe      | 128 GB | 1       | 7     | 0     | 0.02   |
| ADATA     | IM2P33F8BR2-256GB  | 256 GB | 2       | 7     | 0     | 0.02   |
| Patriot   | P300               | 1 TB   | 2       | 7     | 0     | 0.02   |
| Micron    | MTFDHBA1T0QFD-1... | 1 TB   | 2       | 7     | 0     | 0.02   |
| XrayDisk  | 512GB              | 512 GB | 1       | 7     | 0     | 0.02   |
| Toshiba   | KXG5AZNV256G NV... | 256 GB | 1       | 7     | 0     | 0.02   |
| SK hynix  | HFM128GDHTNG-8310B | 128 GB | 3       | 7     | 0     | 0.02   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 44      | 7     | 0     | 0.02   |
| Silico... | 512GB              | 512 GB | 3       | 7     | 0     | 0.02   |
| Phison    | One-Netbook PCI... | 512 GB | 3       | 6     | 0     | 0.02   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 8       | 6     | 0     | 0.02   |
| Toshiba   | KXG6AZNV512G KI... | 512 GB | 3       | 6     | 0     | 0.02   |
| SK hynix  | HFB1M8MQ331C0MR    | 128 GB | 2       | 6     | 0     | 0.02   |
| Samsung   | MZALQ128HBHQ-000L2 | 128 GB | 18      | 6     | 0     | 0.02   |
| Silico... | Inland NVMe SSD    | 256 GB | 2       | 6     | 0     | 0.02   |
| Seagate   | FireCuda 530 ZP... | 1 TB   | 2       | 6     | 0     | 0.02   |
| Samsung   | SSD 980            | 500 GB | 45      | 6     | 0     | 0.02   |
| Union ... | UMIS RPJTJ256ME... | 256 GB | 12      | 6     | 0     | 0.02   |
| Lite-On   | NVMe CA5-8D512     | 512 GB | 1       | 6     | 0     | 0.02   |
| Samsung   | MZVLW256HEHP-000   | 256 GB | 2       | 6     | 0     | 0.02   |
| ADATA     | IM2P33F8BR2-512GB  | 512 GB | 4       | 6     | 0     | 0.02   |
| Silico... | SK                 | 128 GB | 1       | 6     | 0     | 0.02   |
| Samsung   | MZVL21T0HCLR-00BL7 | 1 TB   | 14      | 6     | 0     | 0.02   |
| Kingston  | SKC2500M8500G      | 500 GB | 5       | 5     | 0     | 0.02   |
| Samsung   | PM981a NVMe SED    | 512 GB | 1       | 5     | 0     | 0.02   |
| Toshiba   | KBG30ZMV512G KI... | 512 GB | 5       | 5     | 0     | 0.02   |
| PNY       | CS1030 1TB SSD     | 1 TB   | 2       | 5     | 0     | 0.02   |
| Samsung   | PM9A1 NVMe         | 512 GB | 18      | 5     | 0     | 0.02   |
| SanDisk   | WD_BLACK SN750 SE  | 1 TB   | 8       | 5     | 0     | 0.02   |
| WDC       | PC SN530 NVMe      | 512 GB | 29      | 5     | 0     | 0.02   |
| EAGET     | SSD Device         | 512 GB | 1       | 5     | 0     | 0.02   |
| SSSTC     | CA5-8D256-Q79      | 256 GB | 1       | 5     | 0     | 0.02   |
| Samsung   | MZ9LQ512HBLU-00B   | 512 GB | 3       | 5     | 0     | 0.02   |
| Intenso   | PCIe               | 240 GB | 1       | 5     | 0     | 0.02   |
| Samsung   | MZVLB1T0HBLR-00007 | 1 TB   | 4       | 5     | 0     | 0.02   |
| SanDisk   | WD Blue SN570      | 1 TB   | 6       | 5     | 0     | 0.02   |
| XPG       | SPECTRIX S20G      | 500 GB | 2       | 5     | 0     | 0.02   |
| ADATA     | IM2P33F8BR2-1TB    | 1 TB   | 1       | 5     | 0     | 0.01   |
| Samsung   | MZVLB2T0HMLB-000H1 | 2 TB   | 1       | 5     | 0     | 0.01   |
| SanDisk   | WD_BLACK SN750 SE  | 500 GB | 1       | 5     | 0     | 0.01   |
| YMTC      | PC005              | 512 GB | 13      | 5     | 0     | 0.01   |
| PNY       | CS3030 2000GB SSD  | 2 TB   | 1       | 5     | 0     | 0.01   |
| Phison    | PS5012-E12S-512G   | 512 GB | 1       | 5     | 0     | 0.01   |
| Foxline   | FLSSD256M80E13TCX5 | 256 GB | 1       | 5     | 0     | 0.01   |
| SK hynix  | HFM256GDGTNG-87A0A | 256 GB | 3       | 4     | 0     | 0.01   |
| Kingston  | SFYRS1000G         | 1 TB   | 2       | 4     | 0     | 0.01   |
| SK hynix  | SHGP31-1000GM      | 1 TB   | 2       | 4     | 0     | 0.01   |
| Intel     | SSDPE21D280GA      | 280 GB | 1       | 4     | 0     | 0.01   |
| WDC       | PC SN530 SDBPMP... | 256 GB | 21      | 4     | 0     | 0.01   |
| Micron    | MTFDHBA512TDV      | 512 GB | 21      | 4     | 0     | 0.01   |
| Intel     | SSDPEKKA128G8      | 128 GB | 1       | 4     | 0     | 0.01   |
| MAXIO     | NE-256             | 256 GB | 1       | 4     | 0     | 0.01   |
| SanDisk   | WD Green SN350     | 1 TB   | 1       | 4     | 0     | 0.01   |
| Phison    | E12S-512G-PHISO... | 512 GB | 3       | 4     | 0     | 0.01   |
| SanDisk   | WD Blue SN570      | 500 GB | 2       | 4     | 0     | 0.01   |
| Solid ... | CL1-3D256-Q11 N... | 256 GB | 4       | 4     | 0     | 0.01   |
| WDC       | PC SN530 SDBPTP... | 512 GB | 4       | 4     | 0     | 0.01   |
| Samsung   | MZALQ256HAJD-000L1 | 256 GB | 28      | 4     | 0     | 0.01   |
| ADATA     | IM2P33F3A NVMe     | 256 GB | 17      | 4     | 60    | 0.01   |
| Samsung   | MZVLQ1T0HBLB-00B00 | 1 TB   | 9       | 4     | 0     | 0.01   |
| Kingston  | SKC3000S512G       | 512 GB | 1       | 4     | 0     | 0.01   |
| Phison    | E12S-1TB-PHISON... | 1 TB   | 1       | 4     | 0     | 0.01   |
| Samsung   | MZALQ128HBHQ-000L1 | 128 GB | 4       | 4     | 0     | 0.01   |
| KIOXIA    | KBG4AZNS1T02       | 1 TB   | 1       | 4     | 0     | 0.01   |
| SK hynix  | BC501A NVMe        | 128 GB | 3       | 4     | 0     | 0.01   |
| Toshiba   | KXG60ZNV1T02 KI... | 1 TB   | 5       | 4     | 0     | 0.01   |
| Samsung   | MZVL2512HCJQ-00BL2 | 512 GB | 6       | 4     | 0     | 0.01   |
| PNY       | CS2130 500GB SSD   | 500 GB | 1       | 4     | 0     | 0.01   |
| Micron    | 2300 NVMe          | 512 GB | 31      | 4     | 1     | 0.01   |
| SK hynix  | HFM256GD3JX013N    | 256 GB | 1       | 3     | 0     | 0.01   |
| PNY       | CS3140 1TB SSD     | 1 TB   | 2       | 3     | 0     | 0.01   |
| Phison    | E12-512G-PHISON... | 512 GB | 1       | 3     | 0     | 0.01   |
| LDLC      | F8+M.2 480         | 480 GB | 1       | 3     | 0     | 0.01   |
| Samsung   | MZVLQ256HAJD-00007 | 256 GB | 4       | 3     | 0     | 0.01   |
| Samsung   | MZVLQ512HBLU-00B   | 512 GB | 4       | 3     | 0     | 0.01   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 13      | 3     | 0     | 0.01   |
| Apple     | SSD AP0256M        | 256 GB | 3       | 3     | 0     | 0.01   |
| SK hynix  | BC511 HFM512GDJ... | 512 GB | 35      | 3     | 0     | 0.01   |
| Smartbuy  | m.2 PS5013-2280T   | 128 GB | 1       | 3     | 0     | 0.01   |
| WDC       | WDS240G2G0C-00AJM0 | 240 GB | 2       | 3     | 0     | 0.01   |
| ADATA     | FALCON             | 512 GB | 2       | 3     | 0     | 0.01   |
| Samsung   | MZVL2512HCJQ-00B07 | 512 GB | 1       | 3     | 0     | 0.01   |
| SK hynix  | BC711 HFM512GD3... | 512 GB | 3       | 3     | 0     | 0.01   |
| Hikvision | HS-SSD-E3000 1024G | 1 TB   | 2       | 3     | 0     | 0.01   |
| EMTEC     | X300               | 256 GB | 1       | 3     | 0     | 0.01   |
| ADATA     | IM2P33F8BR1-128GB  | 128 GB | 4       | 3     | 0     | 0.01   |
| Apple     | SSD AP2048N        | 2 TB   | 2       | 3     | 0     | 0.01   |
| SK hynix  | HFM128GDGTNG-87A0A | 128 GB | 4       | 3     | 0     | 0.01   |
| UMIS      | RPITJ1TBVME2HWD    | 1 TB   | 2       | 3     | 0     | 0.01   |
| Gigabyte  | GP-GSM2NE8128GNTD  | 128 GB | 1       | 3     | 0     | 0.01   |
| WDC       | WDBA3V5000ANC-WRSN | 500 GB | 1       | 3     | 0     | 0.01   |
| Phison    | 311CD0512GB        | 512 GB | 17      | 3     | 4     | 0.01   |
| Seagate   | FireCuda 510 SS... | 1 TB   | 1       | 3     | 0     | 0.01   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 14      | 2     | 0     | 0.01   |
| Silico... | AAR512GN122321030  | 512 GB | 1       | 2     | 0     | 0.01   |
| WDC       | PC SN530 SDBPMP... | 256 GB | 26      | 2     | 0     | 0.01   |
| Samsung   | MZALQ256HBJD-00BL2 | 256 GB | 5       | 2     | 0     | 0.01   |
| Team      | TM8FP6002T         | 2 TB   | 1       | 2     | 0     | 0.01   |
| WDC       | PC SN730 SDBPNT... | 256 GB | 2       | 2     | 0     | 0.01   |
| Phison    | One-Netbook PCI... | 1 TB   | 3       | 2     | 0     | 0.01   |
| WDC       | PC SN530 SDBPMP... | 512 GB | 16      | 2     | 0     | 0.01   |
| KIOXIA    | KXG60PNV512G NVMe  | 512 GB | 1       | 2     | 0     | 0.01   |
| Silico... | NVMe               | 256 GB | 1       | 2     | 0     | 0.01   |
| PNY       | CS3040 2TB SSD     | 2 TB   | 2       | 2     | 0     | 0.01   |
| Micron    | MTFDHBA1T0TDV-1... | 1 TB   | 2       | 2     | 0     | 0.01   |
| PNY       | CS1031 256GB SSD   | 256 GB | 1       | 2     | 0     | 0.01   |
| Samsung   | PM981 NVMe SED     | 512 GB | 2       | 2     | 0     | 0.01   |
| Samsung   | SSD 980            | 250 GB | 3       | 2     | 0     | 0.01   |
| KIOXIA    | KBG4AZNV256G       | 256 GB | 1       | 2     | 0     | 0.01   |
| Kingston  | RBUSNS8154P3256GJ5 | 256 GB | 1       | 2     | 0     | 0.01   |
| NTC       | 512GB NVMe         | 512 GB | 1       | 2     | 0     | 0.01   |
| Netac     | NVMe SSD           | 128 GB | 1       | 2     | 0     | 0.01   |
| WDC       | WDS100T1XHE-00AFY0 | 1 TB   | 1       | 2     | 0     | 0.01   |
| Kingston  | OM8PCP3512F-A02    | 512 GB | 4       | 2     | 0     | 0.01   |
| WDC       | PC SN530 SDBPTP... | 1 TB   | 6       | 2     | 0     | 0.01   |
| ADATA     | IM2P33F3A NVMe     | 512 GB | 14      | 2     | 0     | 0.01   |
| Gigabyte  | GP-GM301TB-G       | 1 TB   | 1       | 2     | 0     | 0.01   |
| Kingston  | OM8PDP3512B-AA1    | 512 GB | 17      | 2     | 0     | 0.01   |
| Apple     | SSD AP0128J        | 121 GB | 3       | 2     | 0     | 0.01   |
| Hikvision | HS-SSD-E2000L 512G | 512 GB | 1       | 2     | 0     | 0.01   |
| Samsung   | PM991a NVMe        | 128 GB | 5       | 2     | 0     | 0.01   |
| SK hynix  | HFM256GD3JX016N    | 256 GB | 2       | 2     | 0     | 0.01   |
| Samsung   | MZVL22T0HBLB-00B00 | 2 TB   | 7       | 2     | 0     | 0.01   |
| WDC       | PC SN520 SDAPMU... | 256 GB | 1       | 2     | 0     | 0.01   |
| Samsung   | PM991a NVMe        | 1 TB   | 3       | 2     | 0     | 0.01   |
| WDC       | PC SN530 SDBPNP... | 1 TB   | 6       | 2     | 0     | 0.01   |
| SK hynix  | PC711 HFS001TDE... | 1 TB   | 1       | 1     | 0     | 0.01   |
| SK hynix  | Skhynix BC501 NVMe | 128 GB | 1       | 1     | 0     | 0.01   |
| Samsung   | MZALQ512HBLU-00BL2 | 512 GB | 20      | 1     | 0     | 0.01   |
| Intel     | SSDPEKKA256G7      | 256 GB | 2       | 1     | 0     | 0.01   |
| Samsung   | PM9A1 NVMe         | 2 TB   | 8       | 10    | 9     | 0.01   |
| Micron    | MTFDHBA256TDV-1... | 256 GB | 1       | 1     | 0     | 0.01   |
| Samsung   | PM991 NVMe         | 128 GB | 2       | 1     | 0     | 0.00   |
| GLOWAY    | YCT512NVMe-M.2-... | 512 GB | 1       | 1     | 0     | 0.00   |
| Toshiba   | KBG30ZMV128G KI... | 128 GB | 1       | 1     | 0     | 0.00   |
| Kingston  | OM8SBP3512K-AH     | 512 GB | 5       | 1     | 0     | 0.00   |
| Phison    | 512GB NVMe SSD     | 512 GB | 1       | 1     | 0     | 0.00   |
| Toshiba   | KBG40ZPZ128G ME... | 128 GB | 2       | 1     | 0     | 0.00   |
| Union ... | UMIS RPITJ512PE... | 512 GB | 2       | 1     | 0     | 0.00   |
| SK hynix  | HFM512GDGTNG-87A0A | 512 GB | 2       | 1     | 0     | 0.00   |
| OEM       | Genuine            | 1 TB   | 2       | 1     | 0     | 0.00   |
| WDC       | PC SN530 NVMe      | 1 TB   | 3       | 1     | 0     | 0.00   |
| Kingston  | SNVS500GB          | 500 GB | 5       | 1     | 0     | 0.00   |
| BIWIN     | NE-128             | 128 GB | 1       | 1     | 0     | 0.00   |
| Hikvision | HS-SSD-E2000 256G  | 256 GB | 1       | 1     | 0     | 0.00   |
| Toshiba   | KBG40ZNT1T02 ME... | 1 TB   | 1       | 1     | 0     | 0.00   |
| Toshiba   | KXG60PNV1T02 NV... | 1 TB   | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 8       | 1     | 0     | 0.00   |
| SK hynix  | PC711 NVMe         | 256 GB | 2       | 1     | 0     | 0.00   |
| KIOXIA... | SSD                | 250 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | MZVLQ256HBJD-00B00 | 256 GB | 1       | 1     | 0     | 0.00   |
| Micron    | 3400_MTFDKBA1T0TFH | 1 TB   | 8       | 1     | 0     | 0.00   |
| Silico... | Asgard AN3 1TNV... | 1 TB   | 1       | 1     | 0     | 0.00   |
| Intel     | SSDPEDKE020T7      | 2 TB   | 2       | 1     | 0     | 0.00   |
| Samsung   | PM981a NVMe SED    | 256 GB | 1       | 1     | 0     | 0.00   |
| Seagate   | BarraCuda 510 S... | 250 GB | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN530 SDBPNP... | 1 TB   | 2       | 1     | 0     | 0.00   |
| SK hynix  | HFM128GDHTNG-8510B | 128 GB | 4       | 1     | 0     | 0.00   |
| KIOXIA    | KBG40ZNS128G BG4A  | 128 GB | 1       | 1     | 0     | 0.00   |
| KIOXIA    | KXG60ZNV256G NVMe  | 256 GB | 1       | 1     | 0     | 0.00   |
| YMTC      | PC005              | 1 TB   | 1       | 1     | 0     | 0.00   |
| Goodram   | IR-SSDPR-P34B-5... | 512 GB | 1       | 1     | 0     | 0.00   |
| Phison    | E12S-TB-PHISON-... | 1 TB   | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 1       | 1     | 0     | 0.00   |
| Samsung   | MZ9LQ256HBJD-00B   | 256 GB | 2       | 1     | 0     | 0.00   |
| SanDisk   | WD IX SN530 SDB... | 256 GB | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN730 SDBQNT... | 1 TB   | 1       | 1     | 0     | 0.00   |
| Samsung   | MZVL2512HCJQ-00B00 | 512 GB | 11      | 1     | 0     | 0.00   |
| Samsung   | MZVPW128HEGM-00000 | 128 GB | 1       | 37    | 32    | 0.00   |
| Transcend | TS256GMTE110S      | 256 GB | 4       | 1     | 0     | 0.00   |
| Corsair   | MP600 CORE         | 4 TB   | 1       | 1     | 0     | 0.00   |
| Silico... | WN600              | 1 TB   | 1       | 1     | 0     | 0.00   |
| Silico... | GSDFN512TS3F1OGCX  | 512 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | MZVLQ512HBLU-00BH1 | 512 GB | 2       | 0     | 0     | 0.00   |
| Samsung   | MZALQ512HBLU-00BL1 | 512 GB | 12      | 0     | 0     | 0.00   |
| Samsung   | MZVLQ1T0HBLB-00BH1 | 1 TB   | 2       | 0     | 0     | 0.00   |
| Samsung   | MZVLQ256HBJD-00B   | 256 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVLQ512HBLU-00BTW | 512 GB | 2       | 0     | 0     | 0.00   |
| Phison    | MSI M390           | 500 GB | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 3       | 0     | 0     | 0.00   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 2       | 0     | 0     | 0.00   |
| YMTC      | PC005              | 256 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVLQ256HBJD-00BH1 | 256 GB | 3       | 0     | 0     | 0.00   |
| KIOXIA    | KXG7AZNV512G LA    | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | PC601 SED NVMe     | 1 TB   | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVLQ512HALU-00007 | 512 GB | 2       | 0     | 0     | 0.00   |
| FORESEE   | P900F128GH         | 128 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | PM991a NVMe        | 256 GB | 4       | 0     | 0     | 0.00   |
| Lenovo    | SL700 PCI-E M.2    | 1 TB   | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVL21T0HCLR-00BH1 | 1 TB   | 1       | 0     | 0     | 0.00   |
| ZHITAI    | TiPro7000          | 1 TB   | 1       | 0     | 0     | 0.00   |
| SK hynix  | BC711 NVMe         | 1 TB   | 1       | 0     | 0     | 0.00   |
| Silico... | NE-240             | 240 GB | 1       | 0     | 0     | 0.00   |
| Toshiba   | KXG50PNV2T04 KI... | 2 TB   | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN520 SDAPTU... | 128 GB | 1       | 0     | 0     | 0.00   |
| Intel     | SSDPEKNU512GZH     | 512 GB | 2       | 0     | 0     | 0.00   |
| SK hynix  | PC601 SED NVMe     | 512 GB | 2       | 0     | 0     | 0.00   |
| Samsung   | MZVLB1T0HBLR-000H7 | 1 TB   | 2       | 0     | 0     | 0.00   |
| SanDisk   | SN530 SDBPNPZ-5... | 512 GB | 1       | 0     | 0     | 0.00   |
| ADATA     | IM2P33F8A-001TD    | 1 TB   | 1       | 0     | 0     | 0.00   |
| Micron    | 2450_MTFDKBA1T0TFK | 1 TB   | 1       | 0     | 0     | 0.00   |
| Seagate   | BarraCuda Q5 ZP... | 1 TB   | 1       | 0     | 0     | 0.00   |
| T-FORCE   | TM8FP8001T         | 1 TB   | 1       | 0     | 0     | 0.00   |
| Crucial   | CT1000P5PSSD8      | 1 TB   | 5       | 0     | 0     | 0.00   |
| ADATA     | SX8100NP           | 2 TB   | 3       | 144   | 338   | 0.00   |
| Plextor   | PX-256M8SeY        | 256 GB | 1       | 0     | 0     | 0.00   |
| KLLISRE   | 256GB              | 256 GB | 2       | 0     | 0     | 0.00   |
| BIWIN     | NI201_256GB        | 256 GB | 1       | 0     | 0     | 0.00   |
| Lenovo    | M.2 2280 NVMe S... | 512 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVLQ1T0HBLB-00B   | 1 TB   | 2       | 0     | 0     | 0.00   |
| Samsung   | MZVL2512HCJQ-00BL7 | 512 GB | 2       | 0     | 0     | 0.00   |
| SSSTC     | CL1-3D128-Q11 NVMe | 128 GB | 2       | 0     | 0     | 0.00   |
| Dell      | Ent NVMe AGN MU... | 1.6 TB | 1       | 0     | 0     | 0.00   |
| SMI       | 2263XT             | 120 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | PM9A1 NVMe         | 256 GB | 2       | 0     | 0     | 0.00   |
| WDC       | PC SN530 SDBQNP... | 512 GB | 3       | 0     | 0     | 0.00   |
| WDC       | WDS400T3X0C-00SJG0 | 4 TB   | 1       | 0     | 0     | 0.00   |
| WDC       | WDS480G2G0C-00AJM0 | 480 GB | 2       | 0     | 0     | 0.00   |
| ADATA     | IM2P33F8A-512GD    | 512 GB | 6       | 0     | 0     | 0.00   |
| Micron    | MTFDHBA512TDV-1... | 512 GB | 5       | 0     | 0     | 0.00   |
| Kingston  | SEDC1000M3840G     | 3.8 TB | 1       | 0     | 0     | 0.00   |
| Micron    | 3400_MTFDKBA512TFH | 512 GB | 1       | 0     | 0     | 0.00   |
| Phison    | ESR01TBTLG-E6GB... | 1 TB   | 1       | 0     | 0     | 0.00   |
| Plextor   | PX-512M9PeGN       | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | Skhynix BC501 NVMe | 512 GB | 1       | 0     | 0     | 0.00   |
| SSSTC     | CA5-8D512          | 512 GB | 2       | 0     | 0     | 0.00   |
| T-FORCE   | TM8FP7002T         | 2 TB   | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN810 SDCPNR... | 2 TB   | 1       | 0     | 0     | 0.00   |
| ADATA     | FALCON             | 1 TB   | 2       | 0     | 0     | 0.00   |
| SSSTC     | CL1-8D128-HP       | 128 GB | 1       | 0     | 0     | 0.00   |
| Silico... | NVMe SSD           | 240 GB | 1       | 0     | 0     | 0.00   |
| Solid ... | SSSTC CL1-4D256... | 256 GB | 1       | 0     | 0     | 0.00   |
| WDC       | WDS250G2B0C        | 250 GB | 2       | 0     | 0     | 0.00   |
| Intel     | SSDPEKKW020T8      | 2 TB   | 1       | 0     | 0     | 0.00   |
| Samsung   | MZALQ256HBJD-00BL1 | 256 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | PM9A1 NVMe SED     | 256 GB | 1       | 0     | 0     | 0.00   |
| ADATA     | IM2P33F8-512GD     | 512 GB | 2       | 0     | 0     | 0.00   |
| Corsair   | MP600 CORE         | 1 TB   | 1       | 0     | 0     | 0.00   |
| Micron    | MTFDKBA512TFH-1... | 512 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVLQ512HALU-000AC | 512 GB | 1       | 0     | 0     | 0.00   |
| Solid ... | SSSTC CL1-4D512    | 512 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TS512GMTE510T      | 512 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | RBUSNS8154P3128GJ5 | 128 GB | 3       | 0     | 0     | 0.00   |
| Gigabyte  | GP-ASM2NE2512GTTDR | 512 GB | 1       | 0     | 0     | 0.00   |
| Phison    | NE-256             | 256 GB | 1       | 0     | 0     | 0.00   |
| Silico... | ZTC-PCIEG3-001T    | 1 TB   | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVL2512HCJQ-00BH1 | 512 GB | 2       | 0     | 0     | 0.00   |
| Micron    | 2300_MTFDHBA256TDV | 256 GB | 1       | 0     | 0     | 0.00   |
| SSSTC     | CA6-8D512-Q11 NVMe | 512 GB | 1       | 0     | 0     | 0.00   |
| Silico... | NVME SSD           | 2 TB   | 1       | 0     | 0     | 0.00   |
| UMIS      | RPIRJ256VME2MWD    | 256 GB | 1       | 0     | 0     | 0.00   |
| Yangtz... | ZHITAI PC005 Ac... | 1 TB   | 1       | 0     | 0     | 0.00   |
| BIWIN     | NE-512             | 512 GB | 1       | 0     | 0     | 0.00   |
| Crucial   | CT500P5PSSD8       | 500 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | SEDC1000BM8240G    | 240 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVL2256HCHQ-00BH1 | 256 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVLQ512HALU-000   | 512 GB | 1       | 0     | 0     | 0.00   |
| Team      | TM8FPD512G         | 512 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZ9LQ512HALU-00000 | 512 GB | 1       | 0     | 0     | 0.00   |
| Silico... | MS10               | 1 TB   | 1       | 0     | 0     | 0.00   |
| Team      | TM8FPD001T         | 1 TB   | 1       | 0     | 0     | 0.00   |

NVME by Vendor
--------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF |
|-------------|--------|---------|-------|-------|------|
| ZOTAC       | 1      | 1       | 899   | 0     | 2.47   |
| Avant       | 1      | 1       | 891   | 0     | 2.44   |
| AMD         | 2      | 3       | 340   | 0     | 0.93   |
| addlink     | 1      | 9       | 339   | 0     | 0.93   |
| BAITITON    | 1      | 1       | 232   | 0     | 0.64   |
| Intel       | 100    | 1308    | 218   | 7     | 0.56   |
| KINGBANK    | 1      | 2       | 190   | 0     | 0.52   |
| Transcend   | 10     | 53      | 179   | 0     | 0.49   |
| Corsair     | 21     | 200     | 177   | 1     | 0.47   |
| Toshiba     | 95     | 810     | 166   | 1     | 0.46   |
| LDLC        | 3      | 3       | 141   | 0     | 0.39   |
| Plextor     | 19     | 41      | 152   | 41    | 0.36   |
| Lexar       | 5      | 17      | 125   | 0     | 0.34   |
| ZHITAI      | 2      | 4       | 124   | 0     | 0.34   |
| Lenovo      | 8      | 56      | 128   | 1     | 0.34   |
| HP          | 10     | 70      | 151   | 2     | 0.34   |
| Patriot     | 10     | 31      | 123   | 0     | 0.34   |
| tigo        | 1      | 1       | 121   | 0     | 0.33   |
| SPCC        | 9      | 91      | 120   | 12    | 0.33   |
| Smartbuy    | 5      | 7       | 115   | 0     | 0.32   |
| XPG         | 13     | 121     | 115   | 17    | 0.31   |
| Crucial     | 13     | 420     | 118   | 8     | 0.31   |
| Phison      | 48     | 404     | 112   | 1     | 0.31   |
| Mushkin     | 8      | 22      | 114   | 4     | 0.30   |
| Dell        | 3      | 3       | 106   | 0     | 0.29   |
| V-GeN       | 2      | 2       | 105   | 0     | 0.29   |
| Lite-On     | 20     | 68      | 104   | 0     | 0.29   |
| ADATA       | 45     | 443     | 104   | 19    | 0.27   |
| Gigabyte    | 16     | 84      | 82    | 0     | 0.23   |
| Apacer      | 5      | 13      | 78    | 0     | 0.22   |
| Huawei      | 2      | 10      | 78    | 0     | 0.22   |
| ORICO       | 1      | 1       | 76    | 0     | 0.21   |
| PNY         | 16     | 56      | 76    | 0     | 0.21   |
| Team        | 11     | 24      | 71    | 0     | 0.19   |
| Zheino      | 2      | 4       | 71    | 0     | 0.19   |
| SanDisk     | 16     | 67      | 70    | 0     | 0.19   |
| Seagate     | 24     | 75      | 65    | 0     | 0.18   |
| Samsung     | 217    | 5652    | 67    | 2     | 0.18   |
| Kingston    | 53     | 682     | 61    | 2     | 0.17   |
| Goodram     | 6      | 16      | 59    | 0     | 0.16   |
| KIOXIA      | 33     | 429     | 52    | 3     | 0.14   |
| KIOXIA-E... | 4      | 14      | 52    | 0     | 0.14   |
| WDC         | 140    | 2137    | 52    | 2     | 0.14   |
| INDMEM      | 1      | 1       | 313   | 5     | 0.14   |
| OSCOO       | 1      | 2       | 50    | 0     | 0.14   |
| FORESEE     | 4      | 6       | 50    | 0     | 0.14   |
| Silicon ... | 54     | 136     | 46    | 0     | 0.13   |
| UMIS        | 11     | 75      | 43    | 2     | 0.12   |
| Kingchuxing | 2      | 2       | 42    | 0     | 0.12   |
| XrayDisk    | 2      | 4       | 40    | 0     | 0.11   |
| SSSTC       | 17     | 58      | 40    | 0     | 0.11   |
| SK hynix    | 100    | 1229    | 38    | 2     | 0.10   |
| Hikvision   | 9      | 12      | 36    | 0     | 0.10   |
| T-FORCE     | 3      | 3       | 33    | 0     | 0.09   |
| Netac       | 3      | 8       | 33    | 0     | 0.09   |
| KingFast    | 1      | 2       | 27    | 0     | 0.08   |
| Micron      | 35     | 371     | 25    | 1     | 0.07   |
| Star Drive  | 1      | 8       | 22    | 0     | 0.06   |
| Union Me... | 10     | 70      | 20    | 0     | 0.06   |
| Phytium     | 1      | 1       | 18    | 0     | 0.05   |
| Apple       | 21     | 193     | 17    | 0     | 0.05   |
| Colorful    | 1      | 1       | 16    | 0     | 0.04   |
| KLEVV       | 2      | 2       | 15    | 0     | 0.04   |
| Solid St... | 8      | 15      | 13    | 0     | 0.04   |
| UDinfo      | 1      | 1       | 10    | 0     | 0.03   |
| EAGET       | 1      | 1       | 5     | 0     | 0.02   |
| Intenso     | 1      | 1       | 5     | 0     | 0.02   |
| Foxline     | 1      | 1       | 5     | 0     | 0.01   |
| YMTC        | 3      | 15      | 4     | 0     | 0.01   |
| BIWIN       | 4      | 7       | 4     | 0     | 0.01   |
| MAXIO       | 1      | 1       | 4     | 0     | 0.01   |
| EMTEC       | 1      | 1       | 3     | 0     | 0.01   |
| NTC         | 1      | 1       | 2     | 0     | 0.01   |
| GLOWAY      | 1      | 1       | 1     | 0     | 0.00   |
| OEM         | 1      | 2       | 1     | 0     | 0.00   |
| KLLISRE     | 1      | 2       | 0     | 0     | 0.00   |
| SMI         | 1      | 1       | 0     | 0     | 0.00   |
| Yangtze ... | 1      | 1       | 0     | 0     | 0.00   |

