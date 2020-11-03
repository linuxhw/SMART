HDD/SSD Desktop-Class Reliability Test
======================================

This is a project to estimate reliability of desktop-class HDD/SSD drives by
the analysis of SMART data collected by Linux users at https://linux-hardware.org. The
primary aim of the project is to find drives with longest power-on hours (POH) and
minimal number of errors, i.e. maximal MTBF (mean time between failures).

Everyone can contribute to this report by uploading probes of their computers by
the [hw-probe](https://github.com/linuxhw/hw-probe) tool:

    sudo -E hw-probe -all -upload

Total drives: 52250.

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

Days   — avg. days per sample,
Err    — avg. errors per sample,
MTBF   — avg. MTBF in years per sample.

See complete list of tested HDD samples in the Appendix 1 ([All_HDD.md](/All_HDD.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF   |
|-----------|--------------------|--------|---------|-------|-------|--------|
| Samsung   | SV1021H            | 10 GB  | 1       | 5713  | 0     | 15.65  |
| WDC       | WD2500SD-01KCB0    | 250 GB | 1       | 4068  | 0     | 11.15  |
| Hitachi   | HUA721075KLA330    | 752 GB | 1       | 3668  | 0     | 10.05  |
| Hitachi   | HDS728040PLA320... | 40 GB  | 1       | 3563  | 0     | 9.76   |
| Hitachi   | HUA7210SASUN1.0... | 1 TB   | 1       | 3495  | 0     | 9.58   |
| HP        | GB0160EAFJE        | 160 GB | 2       | 3447  | 0     | 9.44   |
| WDC       | WD1600JD-00HBC0    | 160 GB | 1       | 3315  | 0     | 9.08   |
| WDC       | WD10EAVS-32D7B1    | 1 TB   | 1       | 3311  | 0     | 9.07   |
| WDC       | WD1002FBYS-05A6B0  | 1 TB   | 1       | 3156  | 0     | 8.65   |
| Samsung   | HE160HJ            | 160 GB | 1       | 2967  | 0     | 8.13   |
| WDC       | WD1200JB-00REA0    | 120 GB | 1       | 2899  | 0     | 7.94   |
| WDC       | WD2500AAJS-62B4A0  | 250 GB | 1       | 2854  | 0     | 7.82   |
| WDC       | WD10EACS-14ZJB0    | 1 TB   | 1       | 2742  | 0     | 7.51   |
| WDC       | WD5000AVVS-63ZWB0  | 500 GB | 1       | 2707  | 0     | 7.42   |
| WDC       | WD2500AAJS-00RYA0  | 250 GB | 1       | 2695  | 0     | 7.39   |
| WDC       | WD3000HLFS-01G6U1  | 304 GB | 1       | 2636  | 0     | 7.22   |
| WDC       | WD30EURS-73TLHY0   | 3 TB   | 1       | 2606  | 0     | 7.14   |
| WDC       | WD2000FYYZ-01UL1B0 | 2 TB   | 1       | 2603  | 0     | 7.13   |
| WDC       | WD10EACS-00C7B0    | 1 TB   | 3       | 2600  | 0     | 7.12   |
| WDC       | WD5000BUCT-63PUZY0 | 500 GB | 1       | 2564  | 0     | 7.03   |
| WDC       | WD5000AAKS-40YGA1  | 500 GB | 1       | 2532  | 0     | 6.94   |
| Hitachi   | HUA7210SASUN1.0T   | 1 TB   | 10      | 2520  | 0     | 6.91   |
| WDC       | WD740GD-00FLA1     | 74 GB  | 1       | 2489  | 0     | 6.82   |
| Seagate   | ST3320820AS_P      | 320 GB | 1       | 2447  | 0     | 6.70   |
| WDC       | WD6400AAKS-41H2B0  | 640 GB | 1       | 2410  | 0     | 6.60   |
| WDC       | WD2502ABYS-02B7A0  | 256 GB | 3       | 2459  | 4     | 6.47   |
| Seagate   | ST3250820AS Q      | 250 GB | 1       | 2361  | 0     | 6.47   |
| WDC       | WD2500AAJS-07VWA0  | 250 GB | 2       | 2354  | 0     | 6.45   |
| Hitachi   | HUA722020ALA330    | 2 TB   | 13      | 2956  | 3     | 6.43   |
| Seagate   | ST320LT014-9YK142  | 320 GB | 1       | 2336  | 0     | 6.40   |
| WDC       | WD5001AALS-00J7B0  | 500 GB | 1       | 2295  | 0     | 6.29   |
| WDC       | WD5003ABYX-18WERA0 | 500 GB | 1       | 2279  | 0     | 6.25   |
| WDC       | WD1600JS-75NCB1    | 160 GB | 1       | 2267  | 0     | 6.21   |
| Seagate   | ST3750641NS EIT    | 752 GB | 1       | 2229  | 0     | 6.11   |
| Fujitsu   | MHV2040BH          | 40 GB  | 1       | 2224  | 0     | 6.09   |
| WDC       | WD1001FALS-00K1B0  | 1 TB   | 2       | 2199  | 0     | 6.02   |
| Seagate   | ST3750641NS        | 752 GB | 1       | 2169  | 0     | 5.94   |
| WDC       | WD2500AAJS-61B4A0  | 250 GB | 1       | 2168  | 0     | 5.94   |
| WDC       | WD2002FYPS-01U1B0  | 2 TB   | 1       | 2163  | 0     | 5.93   |
| WDC       | WD1600AAJS-61WAA0  | 160 GB | 1       | 2124  | 0     | 5.82   |
| Hitachi   | HCS5C3225SLA380    | 250 GB | 1       | 2124  | 0     | 5.82   |
| WDC       | WD5000ABYS-01TNA0  | 500 GB | 2       | 2117  | 0     | 5.80   |
| WDC       | WD3200AVJB-63J5A0  | 320 GB | 2       | 2113  | 0     | 5.79   |
| Hitachi   | HUA722010ALA330    | 1 TB   | 1       | 2111  | 0     | 5.79   |
| WDC       | WD800JD-75MSA1     | 80 GB  | 2       | 2057  | 0     | 5.64   |
| WDC       | WD30EURS-63SPKY0   | 3 TB   | 3       | 2023  | 0     | 5.54   |
| HP        | GB0500C4413        | 500 GB | 2       | 2009  | 0     | 5.51   |
| WDC       | WD1002FBYS-18W8B1  | 1 TB   | 1       | 1999  | 0     | 5.48   |
| WDC       | WD800AAJB-00J3A0   | 80 GB  | 1       | 1982  | 0     | 5.43   |
| WDC       | WD1601ABYS-01C0A0  | 164 GB | 1       | 1982  | 0     | 5.43   |
| WDC       | WD2500YS-01SHB0    | 256 GB | 2       | 1982  | 0     | 5.43   |
| WDC       | WD1600AAJS-00RYA0  | 160 GB | 1       | 1970  | 0     | 5.40   |
| Hitachi   | HDS722020ALA330... | 2 TB   | 1       | 1963  | 0     | 5.38   |
| Hitachi   | HDS722516VLSA80    | 164 GB | 2       | 2077  | 1     | 5.36   |
| Hitachi   | HUA722010CLA331    | 1 TB   | 1       | 1939  | 0     | 5.31   |
| WDC       | WD400BD-55MTA1     | 40 GB  | 2       | 1915  | 0     | 5.25   |
| WDC       | WD6400AAKS-07A7B0  | 640 GB | 1       | 1900  | 0     | 5.21   |
| WDC       | WD800JD-60LUA0     | 80 GB  | 1       | 1889  | 0     | 5.18   |
| Samsung   | HE103SJ            | 1 TB   | 1       | 1865  | 0     | 5.11   |
| WDC       | WD2003FYPS-27Y2B0  | 2 TB   | 6       | 2038  | 1     | 5.06   |
| WDC       | WD7500AAKS-22RBA0  | 752 GB | 1       | 1816  | 0     | 4.98   |
| Toshiba   | MK3255GSXF         | 320 GB | 1       | 1812  | 0     | 4.97   |
| Seagate   | ST3300622AS        | 304 GB | 1       | 1806  | 0     | 4.95   |
| WDC       | WD360GD-00FNA0     | 37 GB  | 2       | 2599  | 1     | 4.95   |
| WDC       | WD3200AAJS-65M0A0  | 320 GB | 2       | 2312  | 4     | 4.93   |
| WDC       | WD2500YS-70SHB1    | 250 GB | 1       | 1789  | 0     | 4.90   |
| Hitachi   | HUA721050KLA330    | 500 GB | 2       | 1774  | 0     | 4.86   |
| WDC       | WD2500JS-40MVB1    | 250 GB | 1       | 1763  | 0     | 4.83   |
| WDC       | WD1600AABS-56PRA0  | 160 GB | 2       | 1763  | 0     | 4.83   |
| WDC       | WD2500KS-22MJB0    | 250 GB | 1       | 1734  | 0     | 4.75   |
| WDC       | WD4000AAJS-22YFA0  | 400 GB | 1       | 1725  | 0     | 4.73   |
| Samsung   | HE103UJ            | 1 TB   | 1       | 1723  | 0     | 4.72   |
| Hitachi   | HCS5C3020BLE630    | 2 TB   | 1       | 1717  | 0     | 4.70   |
| WDC       | WD400JB-00ENA0     | 40 GB  | 3       | 2383  | 6     | 4.69   |
| Seagate   | ST91000640NS       | 1 TB   | 16      | 1791  | 1     | 4.67   |
| HGST      | HTE541515A9E630    | 1.5 TB | 1       | 1702  | 0     | 4.66   |
| WDC       | WD3200JS-55PDB0    | 320 GB | 1       | 1698  | 0     | 4.65   |
| Seagate   | ST500LX003-1AC15G  | 500 GB | 1       | 1697  | 0     | 4.65   |
| Samsung   | SP0411N            | 40 GB  | 2       | 3755  | 9     | 4.62   |
| WDC       | WD1601ABYS-18C0A0  | 160 GB | 3       | 2288  | 4     | 4.58   |
| WDC       | WD1600JS-88MHB0    | 160 GB | 1       | 1667  | 0     | 4.57   |
| WDC       | WD3000HLFS-01G6U4  | 304 GB | 2       | 1654  | 0     | 4.53   |
| WDC       | WD1200JD-00HBB0    | 120 GB | 7       | 1999  | 60    | 4.53   |
| WDC       | WD3200AAJS-22RYA0  | 320 GB | 3       | 1653  | 0     | 4.53   |
| WDC       | WD6400AAKS-00H2B1  | 640 GB | 1       | 1653  | 0     | 4.53   |
| WDC       | WD3200LPVX-16V0TT3 | 320 GB | 1       | 1644  | 0     | 4.50   |
| WDC       | WD15EARS-60MVWB0   | 1.5 TB | 1       | 1636  | 0     | 4.48   |
| Seagate   | ST500DM002-1ER14C  | 500 GB | 2       | 1632  | 0     | 4.47   |
| HP        | FB080C4080         | 80 GB  | 1       | 1630  | 0     | 4.47   |
| HGST      | HUS724020ALE640    | 2 TB   | 10      | 1628  | 0     | 4.46   |
| Seagate   | ST3200021A         | 200 GB | 1       | 1624  | 0     | 4.45   |
| WDC       | WD5000AAKS-40V2B0  | 500 GB | 1       | 1619  | 0     | 4.44   |
| Seagate   | ST2000DL004 HD2... | 2 TB   | 3       | 1617  | 0     | 4.43   |
| Maxtor    | 6V300F0            | 304 GB | 1       | 1613  | 0     | 4.42   |
| WDC       | WD30EFRX-68AX9N0   | 3 TB   | 29      | 1833  | 1     | 4.41   |
| WDC       | WD7500AYYS-01RCA0  | 752 GB | 5       | 1678  | 1     | 4.39   |
| WDC       | WD1600JB-22GVA0    | 160 GB | 1       | 1600  | 0     | 4.39   |
| WDC       | WD1002FBYS-02A6B0  | 1 TB   | 9       | 1720  | 1     | 4.37   |
| WDC       | WD2000JB-16FUA0    | 200 GB | 1       | 1584  | 0     | 4.34   |
| WDC       | WD3200AAVS-00ZTB0  | 320 GB | 1       | 1583  | 0     | 4.34   |
| Toshiba   | MQ01ABD032V        | 320 GB | 1       | 1578  | 0     | 4.33   |
| Samsung   | HD502HM            | 500 GB | 1       | 1573  | 0     | 4.31   |
| WDC       | WD20EARS-14MVWB0   | 2 TB   | 1       | 1565  | 0     | 4.29   |
| Hitachi   | HDS723030ALA640    | 3 TB   | 11      | 1699  | 9     | 4.22   |
| WDC       | WD4000AAJS-65TKA0  | 400 GB | 1       | 1532  | 0     | 4.20   |
| WDC       | WD2502ABYS-23B7... | 250 GB | 2       | 1522  | 0     | 4.17   |
| Seagate   | ST4000NM0024-1H... | 4 TB   | 4       | 1519  | 0     | 4.16   |
| Seagate   | ST980412ASG        | 80 GB  | 1       | 1501  | 0     | 4.11   |
| WDC       | WD2500AAJS-22VWA0  | 250 GB | 3       | 1496  | 0     | 4.10   |
| HP        | GB1000EAMYC        | 1 TB   | 1       | 1490  | 0     | 4.08   |
| Quantum   | FIREBALLlct10 05   | 5 GB   | 1       | 1486  | 0     | 4.07   |
| WDC       | WD1200JS-55NCB1    | 120 GB | 1       | 1484  | 0     | 4.07   |
| WDC       | WD2000JD-00GBB0    | 200 GB | 1       | 1482  | 0     | 4.06   |
| Seagate   | ST9250610NS        | 250 GB | 4       | 1472  | 0     | 4.03   |
| WDC       | WD3200AAKX-753CA0  | 320 GB | 1       | 1471  | 0     | 4.03   |
| WDC       | WD1001FALS-00J7B0  | 1 TB   | 19      | 1460  | 0     | 4.00   |
| Seagate   | MB3000EBKAB        | 3 TB   | 2       | 1447  | 0     | 3.97   |
| Toshiba   | MK1002TSKB         | 1 TB   | 1       | 1446  | 0     | 3.96   |
| Seagate   | ST3500641AS        | 500 GB | 4       | 2192  | 37    | 3.91   |
| Hitachi   | HDS722020ALA330    | 2 TB   | 26      | 1740  | 10    | 3.90   |
| WDC       | WD10EADS-65M2B0    | 1 TB   | 4       | 1717  | 4     | 3.86   |
| HGST      | HDN726050ALE610    | 5 TB   | 1       | 1409  | 0     | 3.86   |
| Hitachi   | HDT722520DLAT80    | 200 GB | 2       | 1406  | 0     | 3.85   |
| WDC       | WD2500JB-22REA0    | 250 GB | 1       | 1398  | 0     | 3.83   |
| Apple     | HDD HTS727575A9... | 752 GB | 2       | 1397  | 0     | 3.83   |
| Seagate   | ST500LM024-1RS152  | 500 GB | 1       | 1394  | 0     | 3.82   |
| WDC       | WD1500HLFS-01G6U3  | 150 GB | 2       | 1388  | 0     | 3.80   |
| Seagate   | ST3000DM001-1E6166 | 3 TB   | 4       | 1446  | 796   | 3.77   |
| WDC       | WD1002FBYS-50A6B0  | 1 TB   | 1       | 1374  | 0     | 3.77   |
| Seagate   | ST3400832AS        | 400 GB | 2       | 2510  | 1     | 3.75   |
| WDC       | WD1500HLFS-01G6U0  | 150 GB | 3       | 1403  | 1     | 3.75   |
| Hitachi   | HDS724040ALE640    | 4 TB   | 4       | 1544  | 341   | 3.74   |
| Hitachi   | HUA723030ALA640    | 3 TB   | 13      | 1376  | 1     | 3.74   |
| WDC       | WD7500BPVT-80HXZT1 | 752 GB | 1       | 1360  | 0     | 3.73   |
| Seagate   | ST6000DM001-1XY17Z | 6 TB   | 3       | 1357  | 0     | 3.72   |
| WDC       | WD3200AAJB-00WGA0  | 320 GB | 2       | 1356  | 0     | 3.72   |
| WDC       | WD20EARS-07MVWB0   | 2 TB   | 4       | 1865  | 1     | 3.71   |
| WDC       | WD2502ABYS-01B7A0  | 256 GB | 4       | 1955  | 1     | 3.68   |
| WDC       | WD3003FZEX-00Z4SA0 | 3 TB   | 2       | 1333  | 0     | 3.65   |
| WDC       | WD2500JS-00MHB0    | 250 GB | 4       | 1325  | 0     | 3.63   |
| Fujitsu   | MPE3064AT          | 6 GB   | 2       | 1315  | 0     | 3.60   |
| WDC       | WD2500AAKX-08ERMA0 | 250 GB | 1       | 1306  | 0     | 3.58   |
| WDC       | WD2500AAKS-22VSA0  | 250 GB | 1       | 1305  | 0     | 3.58   |
| Maxtor    | STM380215A         | 80 GB  | 3       | 1701  | 614   | 3.57   |
| WDC       | WD6401AALS-00E8B0  | 640 GB | 3       | 1289  | 0     | 3.53   |
| WDC       | WD1200BB-00GUA0    | 120 GB | 1       | 1284  | 0     | 3.52   |
| WDC       | WD3000F9YZ-09N20L0 | 3 TB   | 4       | 1902  | 2     | 3.52   |
| WDC       | WD1001FALS-75J7B0  | 1 TB   | 2       | 1485  | 4     | 3.52   |
| WDC       | WD2000BB-22GUC0    | 200 GB | 1       | 1282  | 0     | 3.51   |
| Hitachi   | HDS5C3015ALA632    | 1.5 TB | 3       | 1462  | 107   | 3.51   |
| Hitachi   | HCS5C3232SLA380    | 320 GB | 1       | 1281  | 0     | 3.51   |
| WDC       | WD4000AAKS-00A7B0  | 400 GB | 1       | 1280  | 0     | 3.51   |
| WDC       | WD3000FYYZ-50UL1B0 | 3 TB   | 1       | 1278  | 0     | 3.50   |
| WDC       | WD15EVDS-68V9B0    | 1.5 TB | 1       | 1276  | 0     | 3.50   |
| HP        | J7989G             | 80 GB  | 1       | 1274  | 0     | 3.49   |
| WDC       | WD2003FYYS-02W0B1  | 2 TB   | 2       | 1290  | 3     | 3.49   |
| HGST      | HMS5C4040BLE640    | 4 TB   | 6       | 1268  | 0     | 3.47   |
| HGST      | HUP723020APA640    | 2 TB   | 1       | 1257  | 0     | 3.45   |
| WDC       | WD6400AACS-00G8B0  | 640 GB | 3       | 1253  | 0     | 3.43   |
| Hitachi   | HUA723020ALA640    | 2 TB   | 16      | 1251  | 0     | 3.43   |
| Hitachi   | HTS421212H9AT00    | 120 GB | 2       | 2184  | 120   | 3.43   |
| WDC       | WD5000AAKS-00TMA0  | 500 GB | 7       | 1371  | 2     | 3.41   |
| HGST      | HUS724030ALA640    | 3 TB   | 13      | 1343  | 2     | 3.39   |
| Samsung   | SP0451N            | 40 GB  | 1       | 1237  | 0     | 3.39   |
| Hitachi   | HDT721075SLA360    | 752 GB | 2       | 1234  | 0     | 3.38   |
| WDC       | WD4000AAJS-32TKA0  | 400 GB | 1       | 1226  | 0     | 3.36   |
| Hitachi   | HDS721075KLA330    | 752 GB | 7       | 1493  | 14    | 3.31   |
| Hitachi   | HDT721075SLA380    | 752 GB | 1       | 1205  | 0     | 3.30   |
| WDC       | WD2500AAJS-00VWA0  | 250 GB | 1       | 1204  | 0     | 3.30   |
| Seagate   | ST3160828AS        | 160 GB | 1       | 1198  | 0     | 3.28   |
| Hitachi   | HUS724040ALE640    | 4 TB   | 2       | 1195  | 0     | 3.28   |
| WDC       | WD800JD-08LSA0     | 80 GB  | 9       | 1335  | 3     | 3.27   |
| WDC       | WD5000AAJS-32YFA0  | 500 GB | 1       | 1187  | 0     | 3.25   |
| Seagate   | ST3300631A         | 304 GB | 1       | 1185  | 0     | 3.25   |
| WDC       | WD1600JS-55MHB1    | 160 GB | 2       | 1179  | 0     | 3.23   |
| WDC       | WD1001FALS-40U9B0  | 1 TB   | 1       | 1175  | 0     | 3.22   |
| WDC       | WD3200AAJB-56WGA0  | 320 GB | 3       | 1172  | 0     | 3.21   |
| WDC       | WD800BB-60JKC0     | 80 GB  | 2       | 1292  | 2     | 3.21   |
| WDC       | WD3000HLFS-01G6U3  | 304 GB | 1       | 1170  | 0     | 3.21   |
| WDC       | WD3200AAKS-75B3A0  | 320 GB | 1       | 2338  | 1     | 3.20   |
| Seagate   | ST3320620NS        | 320 GB | 3       | 1312  | 1     | 3.20   |
| WDC       | WD3200AAJS-07RYA0  | 320 GB | 1       | 1168  | 0     | 3.20   |
| WDC       | WD1500AHFD-00RAR5  | 150 GB | 1       | 1164  | 0     | 3.19   |
| WDC       | WD5000AVJB-63YUA0  | 500 GB | 1       | 1163  | 0     | 3.19   |
| WDC       | WD10EADS-00L5B1    | 1 TB   | 42      | 1666  | 5     | 3.18   |
| Toshiba   | MK8017GSG          | 80 GB  | 1       | 1162  | 0     | 3.18   |
| WDC       | WD4000AAKS-00YGA0  | 400 GB | 5       | 1249  | 1     | 3.18   |
| WDC       | WD1001FALS-41Y6A0  | 1 TB   | 3       | 1345  | 1     | 3.17   |
| WDC       | WD2503ABYX-01WERA0 | 256 GB | 1       | 1155  | 0     | 3.16   |
| WDC       | WD20EARX-22PASB0   | 2 TB   | 2       | 1153  | 0     | 3.16   |
| WDC       | WD1001FALS-00E3A0  | 1 TB   | 5       | 1273  | 1     | 3.14   |
| Hitachi   | HDS5C3030BLE630    | 3 TB   | 2       | 1146  | 0     | 3.14   |
| WDC       | WD740ADFD-00NLR1   | 74 GB  | 2       | 1137  | 0     | 3.12   |
| WDC       | WD5003AZEX-00RKKA0 | 500 GB | 2       | 1135  | 0     | 3.11   |
| Toshiba   | MG03ACA200         | 2 TB   | 1       | 1134  | 0     | 3.11   |
| WDC       | MB0500EBNCR        | 500 GB | 1       | 1134  | 0     | 3.11   |
| WDC       | WD50EZRZ-32RWYB1   | 5 TB   | 2       | 1128  | 0     | 3.09   |
| Seagate   | ST4000VN0001-1S... | 4 TB   | 3       | 1128  | 0     | 3.09   |
| Samsung   | HD400LD            | 400 GB | 4       | 1126  | 0     | 3.09   |
| Seagate   | ST250DM001 HD256GJ | 250 GB | 1       | 1123  | 0     | 3.08   |
| WDC       | WD4000F9YZ-09N20L1 | 4 TB   | 3       | 1122  | 0     | 3.08   |
| WDC       | WD3200AAJS-40VWA0  | 320 GB | 1       | 1118  | 0     | 3.06   |
| Hitachi   | HDT725032VLA380    | 320 GB | 12      | 1458  | 98    | 3.06   |
| Seagate   | ST3250820SCE       | 250 GB | 3       | 1116  | 0     | 3.06   |
| Hitachi   | HDS723020BLA642    | 2 TB   | 40      | 1342  | 85    | 3.05   |
| Seagate   | ST3300831AS        | 304 GB | 4       | 1804  | 3     | 3.04   |
| WDC       | WD2002FYPS-02W3B0  | 2 TB   | 2       | 1108  | 0     | 3.04   |
| WDC       | WD7500AACS-00D6B0  | 752 GB | 1       | 1107  | 0     | 3.03   |
| Hitachi   | HDS7250SASUN500... | 500 GB | 1       | 1103  | 0     | 3.02   |
| WDC       | WD10EARS-67Y5B1    | 1 TB   | 1       | 1100  | 0     | 3.01   |
| WDC       | WD2002FAEX-00MJRA0 | 2 TB   | 1       | 1094  | 0     | 3.00   |
| WDC       | WD1200JS-00SGB0    | 120 GB | 2       | 1091  | 0     | 2.99   |
| WDC       | WD20EARX-008FB0    | 2 TB   | 10      | 1188  | 1     | 2.99   |
| WDC       | WD1600YS-01SHB1    | 164 GB | 7       | 1088  | 0     | 2.98   |
| WDC       | WD10EADS-00P8B0    | 1 TB   | 7       | 1278  | 2     | 2.98   |
| WDC       | WD3200KS-75PFB0    | 320 GB | 2       | 1359  | 39    | 2.98   |
| Seagate   | ST3360320AS        | 360 GB | 4       | 1352  | 1     | 2.98   |
| Seagate   | ST9500620NS 81Y... | 500 GB | 1       | 1083  | 0     | 2.97   |
| Hitachi   | HDS728040PLA320    | 40 GB  | 3       | 1579  | 6     | 2.97   |
| WDC       | WD7500AARX-00N0YB0 | 752 GB | 1       | 1081  | 0     | 2.96   |
| WDC       | WD30EZRX-00DC0B0   | 3 TB   | 28      | 1200  | 1     | 2.96   |
| Seagate   | ST6000AS0002-1N... | 6 TB   | 1       | 1078  | 0     | 2.96   |
| WDC       | WD30EURX-64HYZY0   | 3 TB   | 1       | 1077  | 0     | 2.95   |
| Maxtor    | 7V250F0            | 256 GB | 2       | 1075  | 0     | 2.95   |
| HGST      | HTS721050A9E630    | 500 GB | 1       | 1069  | 0     | 2.93   |
| WDC       | WD2002FAEX-007BA0  | 2 TB   | 24      | 1250  | 2     | 2.93   |
| HGST      | HDN724040ALE640    | 4 TB   | 12      | 1068  | 0     | 2.93   |
| Seagate   | ST32000644NS       | 2 TB   | 6       | 1224  | 23    | 2.92   |
| WDC       | WD7500AAKS-00RBA0  | 752 GB | 9       | 1385  | 57    | 2.91   |
| HGST      | HDN724030ALE640    | 3 TB   | 6       | 1058  | 0     | 2.90   |
| WDC       | WD6400AACS-00D6B1  | 640 GB | 1       | 1058  | 0     | 2.90   |
| WDC       | WD5000AAKS-402AA0  | 500 GB | 2       | 1473  | 24    | 2.90   |
| WDC       | WD2500AAJS-75VWA0  | 250 GB | 3       | 1056  | 0     | 2.89   |
| WDC       | WD15EARS-00S8B1    | 1.5 TB | 5       | 1552  | 2     | 2.88   |
| WDC       | WD2500JS-00MHB1    | 250 GB | 2       | 1052  | 0     | 2.88   |
| Samsung   | HD204UI            | 2 TB   | 41      | 1226  | 49    | 2.87   |
| HGST      | MB6000GEBTP        | 6 TB   | 1       | 1046  | 0     | 2.87   |
| WDC       | WD3200JD-00KLB0    | 320 GB | 1       | 1045  | 0     | 2.87   |
| Seagate   | ST8000AS0002-1N... | 8 TB   | 36      | 1174  | 4     | 2.85   |
| WDC       | WD800BB-75FRA0     | 80 GB  | 2       | 1034  | 0     | 2.83   |
| Seagate   | ST340823A          | 40 GB  | 1       | 1034  | 0     | 2.83   |
| WDC       | WD1600JB-00REA0    | 160 GB | 8       | 1147  | 4     | 2.83   |
| WDC       | WD800BB-22JHA0     | 80 GB  | 2       | 1029  | 0     | 2.82   |
| WDC       | WD1001FALS-403AA0  | 1 TB   | 2       | 1025  | 0     | 2.81   |
| WDC       | WD2001FASS-00W2B0  | 2 TB   | 2       | 1024  | 0     | 2.81   |
| Hitachi   | HDT725040VLA360    | 400 GB | 2       | 1024  | 0     | 2.81   |
| WDC       | WD4NPURX-64TPFY0   | 4 TB   | 1       | 1023  | 0     | 2.80   |
| WDC       | WD2500JB-57REA0    | 250 GB | 1       | 1021  | 0     | 2.80   |
| Toshiba   | DT01ABA200         | 2 TB   | 9       | 1076  | 2     | 2.80   |
| WDC       | WD10EACS-00D6B0    | 1 TB   | 8       | 1690  | 20    | 2.79   |
| HP        | GB0250EAFYK        | 250 GB | 2       | 1519  | 67    | 2.79   |
| WDC       | WD400LB-00DNA0     | 40 GB  | 2       | 1103  | 2     | 2.78   |
| WDC       | WD200BB-00DEA0     | 20 GB  | 1       | 1015  | 0     | 2.78   |
| WDC       | WD6002FRYZ-01WD5B1 | 6 TB   | 2       | 1014  | 0     | 2.78   |
| WDC       | WD5000AACS-61M6B2  | 500 GB | 3       | 2013  | 4     | 2.78   |
| WDC       | WD1600JB-00EVA0    | 160 GB | 1       | 1012  | 0     | 2.77   |
| WDC       | WD2000FYYZ-01UL1B2 | 2 TB   | 3       | 1010  | 0     | 2.77   |
| Toshiba   | MC04ACA200E        | 2 TB   | 1       | 1008  | 0     | 2.76   |
| Seagate   | ST320LT023-1AF142  | 320 GB | 1       | 1007  | 0     | 2.76   |
| WDC       | WD3200AAKS-00G3A0  | 320 GB | 6       | 1006  | 0     | 2.76   |
| WDC       | WD20NMVW-59AV3S3   | 2 TB   | 1       | 1005  | 0     | 2.75   |
| WDC       | WD1600AABS-61PRA0  | 160 GB | 3       | 1341  | 1     | 2.75   |
| WDC       | WD2000JS-22MHB0    | 200 GB | 4       | 1909  | 10    | 2.74   |
| WDC       | WD2500JS-60NCB1    | 250 GB | 8       | 1084  | 1     | 2.73   |
| Seagate   | ST3400833AS        | 400 GB | 2       | 995   | 0     | 2.73   |
| HGST      | HUS724020ALA640    | 2 TB   | 24      | 990   | 0     | 2.71   |
| WDC       | WD1000FYPS-01ZKB0  | 1 TB   | 1       | 989   | 0     | 2.71   |
| WDC       | WD3200BEKT-00PVMT0 | 320 GB | 2       | 985   | 0     | 2.70   |
| WDC       | WD5000AAKS-00C8A0  | 500 GB | 3       | 1253  | 62    | 2.70   |
| WDC       | WD10JPVT-16A1YT0   | 1 TB   | 3       | 984   | 0     | 2.70   |
| WDC       | WD3200AAKX-221CA0  | 320 GB | 1       | 981   | 0     | 2.69   |
| WDC       | WD400JB-00JJC0     | 40 GB  | 1       | 980   | 0     | 2.69   |
| Samsung   | HD040GJ-P          | 40 GB  | 1       | 975   | 0     | 2.67   |
| Hitachi   | HDT725025VLA380    | 250 GB | 17      | 1139  | 30    | 2.67   |
| WDC       | WD20NMVW-11EDZS2   | 2 TB   | 3       | 972   | 0     | 2.66   |
| WDC       | WD5000AAKS-07YGA0  | 500 GB | 3       | 971   | 0     | 2.66   |
| WDC       | WD10EALX-079BA1    | 1 TB   | 1       | 968   | 0     | 2.65   |
| WDC       | WD5000BMVV-11GNWS0 | 500 GB | 2       | 967   | 0     | 2.65   |
| Toshiba   | MK4032GAX          | 40 GB  | 1       | 960   | 0     | 2.63   |
| WDC       | WD2000JS-00MVB1    | 200 GB | 1       | 957   | 0     | 2.62   |
| WDC       | WD20EZRX-07D8PB0   | 2 TB   | 1       | 957   | 0     | 2.62   |
| WDC       | WD7502AAEX-00Z3A0  | 752 GB | 1       | 956   | 0     | 2.62   |
| WDC       | WD5000AAKS-22YGA0  | 500 GB | 4       | 1326  | 115   | 2.62   |
| WDC       | WD5000AAKS-00YGA0  | 500 GB | 21      | 1138  | 3     | 2.62   |
| Toshiba   | MQ01UBB200         | 2 TB   | 4       | 952   | 0     | 2.61   |
| WDC       | WD800BEVT-00ZCT0   | 80 GB  | 1       | 951   | 0     | 2.61   |
| WDC       | WD800JD-60LSA5     | 80 GB  | 18      | 992   | 1     | 2.60   |
| WDC       | WD1600BB-22RDA0    | 160 GB | 2       | 947   | 0     | 2.60   |
| Quantum   | FIREBALLP AS20.5   | 20 GB  | 1       | 946   | 0     | 2.59   |
| WDC       | WD10EADS-00M2B0    | 1 TB   | 37      | 1271  | 94    | 2.59   |
| Seagate   | ST3250823AS        | 250 GB | 14      | 1582  | 20    | 2.59   |
| WDC       | WD1001FALS-41Y6A1  | 1 TB   | 1       | 938   | 0     | 2.57   |
| WDC       | WD1600JS-55NCB1    | 160 GB | 4       | 935   | 0     | 2.56   |
| WDC       | WD5000AAKB-00YSA0  | 500 GB | 2       | 935   | 0     | 2.56   |
| WDC       | WD5000LUCT-63C26Y0 | 500 GB | 1       | 934   | 0     | 2.56   |
| Hitachi   | HDS721016CLA382    | 160 GB | 6       | 960   | 1     | 2.56   |
| WDC       | WD2500JS-22NCB1    | 250 GB | 9       | 1087  | 8     | 2.55   |
| WDC       | WD6401AALS-00L3B2  | 640 GB | 19      | 1233  | 6     | 2.53   |
| WDC       | WD20NMVW-11W68S0   | 2 TB   | 3       | 1066  | 20    | 2.53   |
| WDC       | WD800JB-00DUA3     | 80 GB  | 1       | 923   | 0     | 2.53   |
| Hitachi   | HUA721010KLA330    | 1 TB   | 4       | 1401  | 488   | 2.53   |
| WDC       | WD2500BEVS-26VAT0  | 250 GB | 1       | 920   | 0     | 2.52   |
| WDC       | WD1600BB-56RDA0    | 160 GB | 2       | 916   | 0     | 2.51   |
| WDC       | WD3200AAKX-603CA0  | 320 GB | 1       | 914   | 0     | 2.51   |
| WDC       | WD1003FBYX-01Y7B0  | 1 TB   | 8       | 1302  | 2     | 2.50   |
| Seagate   | ST3300622A         | 304 GB | 1       | 912   | 0     | 2.50   |
| WDC       | WD10EARS-003BB1    | 1 TB   | 12      | 1061  | 144   | 2.50   |
| Seagate   | ST3000DM003-1F216N | 3 TB   | 2       | 910   | 0     | 2.49   |
| Seagate   | ST91000640NS 81... | 1 TB   | 1       | 909   | 0     | 2.49   |
| WDC       | WD15EARS-00J2GB0   | 1.5 TB | 1       | 908   | 0     | 2.49   |
| WDC       | WD10EUCX-73YZ1Y0   | 1 TB   | 1       | 907   | 0     | 2.49   |
| WDC       | WD1600BB-00RDA0    | 160 GB | 4       | 1124  | 20    | 2.47   |
| WDC       | WD800BEVS-08RST3   | 80 GB  | 1       | 900   | 0     | 2.47   |
| WDC       | WD400BB-71DGA0     | 40 GB  | 1       | 900   | 0     | 2.47   |
| Hitachi   | HDS5C3020BLE630    | 2 TB   | 4       | 1329  | 72    | 2.46   |
| WDC       | WD5000AACS-00ZUB0  | 500 GB | 10      | 934   | 1     | 2.46   |
| WDC       | WD1001FALS-00Y6A0  | 1 TB   | 5       | 1092  | 22    | 2.45   |
| Seagate   | ST4000VN000-1H4168 | 4 TB   | 16      | 978   | 126   | 2.44   |
| Hitachi   | HUS724030ALA640    | 3 TB   | 1       | 889   | 0     | 2.44   |
| WDC       | WD800BB-22HEA1     | 80 GB  | 1       | 888   | 0     | 2.43   |
| HGST      | HTE541010A9E680    | 1 TB   | 2       | 913   | 509   | 2.43   |
| WDC       | WD2500AAJS-55RYA0  | 250 GB | 2       | 887   | 0     | 2.43   |
| WDC       | WD3200AAJB-00TYA0  | 320 GB | 4       | 885   | 0     | 2.43   |
| WDC       | WD5001ABYS-01YNA0  | 500 GB | 2       | 884   | 0     | 2.42   |
| WDC       | WD4000KS-00MNB0    | 400 GB | 3       | 883   | 0     | 2.42   |
| Seagate   | ST91000640NS 81... | 1 TB   | 1       | 883   | 0     | 2.42   |
| Hitachi   | HDS5C3020ALA632    | 2 TB   | 15      | 993   | 2     | 2.41   |
| WDC       | WD1600AAJS-75WAA0  | 160 GB | 2       | 880   | 0     | 2.41   |
| WDC       | WD1002FAEX-00Z3A0  | 1 TB   | 75      | 1095  | 74    | 2.41   |
| Seagate   | ST4000DM000-1F2168 | 4 TB   | 62      | 962   | 34    | 2.40   |
| Hitachi   | HDT722520DLA380    | 200 GB | 4       | 1091  | 2     | 2.40   |
| WDC       | WD30EZRS-42KEZB0   | 3 TB   | 1       | 874   | 0     | 2.40   |
| Toshiba   | MQ01ABF050H        | 500 GB | 2       | 873   | 0     | 2.39   |
| Seagate   | ST4000NM0245-1Z... | 4 TB   | 3       | 872   | 0     | 2.39   |
| Hitachi   | HDS5C1010CLA382    | 1 TB   | 8       | 907   | 1     | 2.39   |
| Seagate   | ST2000DM001-1E6164 | 2 TB   | 4       | 870   | 0     | 2.39   |
| WDC       | WD4000FYYZ-01UL1B3 | 4 TB   | 1       | 869   | 0     | 2.38   |
| WDC       | WD6400AAKS-75A7B2  | 640 GB | 6       | 1034  | 5     | 2.37   |
| WDC       | WD800BB-75JHA0     | 80 GB  | 1       | 865   | 0     | 2.37   |
| Seagate   | ST3250620NS        | 250 GB | 18      | 1339  | 273   | 2.37   |
| HP        | MB1000EBZQB        | 1 TB   | 1       | 863   | 0     | 2.37   |
| WDC       | WD3202ABYS-02B7A0  | 320 GB | 6       | 929   | 1     | 2.36   |
| WDC       | WD5002ABYS-02B1B0  | 500 GB | 10      | 1229  | 3     | 2.36   |
| WDC       | WD30EZRX-00MMMB0   | 3 TB   | 15      | 1019  | 2     | 2.36   |
| WDC       | WD20EARX-00MMMB0   | 2 TB   | 2       | 859   | 0     | 2.35   |
| Seagate   | ST1000LX001-1EM164 | 1 TB   | 1       | 857   | 0     | 2.35   |
| WDC       | WD800AAJS-22PSA0   | 80 GB  | 4       | 852   | 0     | 2.33   |
| Seagate   | ST3500630A         | 500 GB | 7       | 1381  | 33    | 2.33   |
| Seagate   | ST3802110AS        | 80 GB  | 3       | 851   | 0     | 2.33   |
| WDC       | WD50EZRX-00MVLB1   | 5 TB   | 3       | 851   | 0     | 2.33   |
| Hitachi   | HCS5C1050CLA382    | 500 GB | 1       | 848   | 0     | 2.33   |
| WDC       | WD10EZEX-08RKKA0   | 1 TB   | 6       | 848   | 0     | 2.32   |
| WDC       | WD2003FZEX-00Z4SA0 | 2 TB   | 21      | 918   | 1     | 2.32   |
| WDC       | WD5002ABYS-01B1B0  | 500 GB | 12      | 1238  | 3     | 2.32   |
| Seagate   | ST32000645NS       | 2 TB   | 8       | 1309  | 11    | 2.30   |
| WDC       | WD800BB-00DKA0     | 80 GB  | 3       | 977   | 1     | 2.29   |
| Seagate   | ST3500630AS        | 500 GB | 38      | 1293  | 238   | 2.29   |
| WDC       | WD10EALX-089BA0    | 1 TB   | 2       | 836   | 0     | 2.29   |
| WDC       | WD20NPVX-00EA4T0   | 2 TB   | 2       | 836   | 0     | 2.29   |
| WDC       | WD1002FAEX-00Y9A0  | 1 TB   | 45      | 1049  | 17    | 2.29   |
| WDC       | WD2502ABYS-18B7A0  | 250 GB | 4       | 1251  | 3     | 2.29   |
| Toshiba   | MK2561GSY          | 250 GB | 1       | 834   | 0     | 2.29   |
| Seagate   | ST32000641AS       | 2 TB   | 12      | 1184  | 220   | 2.28   |
| WDC       | WD1600JS-60MHB1    | 160 GB | 7       | 974   | 4     | 2.28   |
| WDC       | WD800JD-75MSA3     | 80 GB  | 24      | 956   | 1     | 2.27   |
| WDC       | WD10EADS-11M2B2    | 1 TB   | 2       | 1619  | 4     | 2.27   |
| WDC       | WD10EAVS-00D7B0    | 1 TB   | 5       | 828   | 0     | 2.27   |
| Seagate   | ST3750840AS        | 752 GB | 1       | 828   | 0     | 2.27   |
| WDC       | WD400BB-00DEA0     | 40 GB  | 1       | 825   | 0     | 2.26   |
| Hitachi   | HTS723216L9SA60    | 160 GB | 5       | 825   | 0     | 2.26   |
| WDC       | WD800BD-88JMC0     | 80 GB  | 2       | 824   | 0     | 2.26   |
| WDC       | WD1003FZEX-00RLFA0 | 1 TB   | 2       | 823   | 0     | 2.26   |
| WDC       | WD1600AAJS-22PSA0  | 160 GB | 15      | 910   | 3     | 2.26   |
| WDC       | WD2500JS-55NCB1    | 250 GB | 6       | 1172  | 16    | 2.25   |
| Hitachi   | HDS728040PLAT20    | 41 GB  | 5       | 979   | 1     | 2.25   |
| WDC       | WD30EFRX-68EUZN0   | 3 TB   | 89      | 995   | 10    | 2.25   |
| WDC       | WD1600JB-00GVA0    | 160 GB | 1       | 822   | 0     | 2.25   |
| WDC       | WD2500BEVE-00WZT0  | 250 GB | 2       | 817   | 0     | 2.24   |
| WDC       | WD400BB-00LNA0     | 40 GB  | 1       | 817   | 0     | 2.24   |
| Hitachi   | HDT725050VLA380    | 500 GB | 2       | 1307  | 19    | 2.24   |
| Seagate   | ST5000DM000-1FK178 | 5 TB   | 12      | 906   | 146   | 2.24   |
| WDC       | WD1500HLFS-01G6U1  | 150 GB | 3       | 813   | 0     | 2.23   |
| WDC       | WD3200AAJS-56B4A0  | 320 GB | 5       | 1152  | 2     | 2.23   |
| WDC       | WD7501AALS-00J7B0  | 752 GB | 17      | 1101  | 52    | 2.23   |
| WDC       | WD2500JB-00GVC0    | 250 GB | 2       | 811   | 0     | 2.22   |
| HGST      | HUS726040ALA610    | 4 TB   | 2       | 810   | 0     | 2.22   |
| WDC       | WD5003ABYX-01WERA2 | 500 GB | 1       | 810   | 0     | 2.22   |
| Seagate   | ST3120213AS        | 120 GB | 1       | 806   | 0     | 2.21   |
| Hitachi   | HTS723232L9SA62    | 320 GB | 1       | 804   | 0     | 2.20   |
| WDC       | WD30EZRX-00SPEB0   | 3 TB   | 11      | 958   | 18    | 2.20   |
| HGST      | HDN726060ALE610    | 6 TB   | 15      | 867   | 45    | 2.20   |
| Seagate   | ST3000VN000-1HJ166 | 3 TB   | 6       | 800   | 0     | 2.19   |
| WDC       | WD8001FFWX-68J1UN0 | 8 TB   | 3       | 799   | 0     | 2.19   |
| WDC       | WD1502FAEX-007BA0  | 1.5 TB | 7       | 872   | 25    | 2.19   |
| WDC       | WD1001FALS-00J7B1  | 1 TB   | 19      | 1034  | 3     | 2.19   |
| WDC       | WD3200AAKS-75SBA0  | 320 GB | 1       | 798   | 0     | 2.19   |
| WDC       | WD20EARS-00S8B1    | 2 TB   | 10      | 1124  | 2     | 2.18   |
| WDC       | WD1600JS-75NCB3    | 160 GB | 4       | 797   | 0     | 2.18   |
| WDC       | WD3200AAKS-22B3A0  | 320 GB | 2       | 797   | 0     | 2.18   |
| Seagate   | ST1500LM003-9YH148 | 1.5 TB | 1       | 796   | 0     | 2.18   |
| Fujitsu   | MHV2060AH PL       | 64 GB  | 2       | 796   | 0     | 2.18   |
| WDC       | WD5000AAVS-00G9B0  | 500 GB | 4       | 1121  | 2     | 2.18   |
| WDC       | WD6400AACS-00G8B1  | 640 GB | 7       | 1069  | 4     | 2.17   |
| WDC       | WD2003FYYS-02W0B0  | 2 TB   | 5       | 1074  | 1     | 2.17   |
| WDC       | WD1005FBYZ-01YCBB1 | 1 TB   | 4       | 790   | 0     | 2.17   |
| WDC       | WD7500AALX-009BA0  | 752 GB | 7       | 789   | 0     | 2.16   |
| Seagate   | ST3400620A         | 400 GB | 4       | 1479  | 143   | 2.16   |
| WDC       | WD5000AAJS-22TKA0  | 500 GB | 2       | 788   | 0     | 2.16   |
| Seagate   | ST380012A          | 80 GB  | 2       | 787   | 0     | 2.16   |
| WDC       | WD5000BPKX-75HPJT0 | 500 GB | 2       | 787   | 0     | 2.16   |
| HP        | MB1000ECWCQ        | 1 TB   | 1       | 787   | 0     | 2.16   |
| WDC       | WD1600AAJB-00WRA0  | 160 GB | 3       | 1002  | 362   | 2.15   |
| WDC       | WD1003FBYX-05Y7B0  | 1 TB   | 1       | 785   | 0     | 2.15   |
| WDC       | WD1600AAJS-07WAA0  | 160 GB | 5       | 1143  | 170   | 2.15   |
| WDC       | WD800JD-75MSA2     | 80 GB  | 2       | 783   | 0     | 2.15   |
| WDC       | WD1002FAEX-007BA0  | 1 TB   | 3       | 853   | 1     | 2.15   |
| Seagate   | ST6000VN0021-1Z... | 6 TB   | 1       | 783   | 0     | 2.15   |
| WDC       | WD6001FFWX-68Z39N0 | 6 TB   | 1       | 782   | 0     | 2.14   |
| WDC       | WD2500AAJS-75M0A0  | 250 GB | 5       | 902   | 1     | 2.14   |
| WDC       | WD5000AADS-56S9B0  | 500 GB | 1       | 782   | 0     | 2.14   |
| WDC       | WD7501AALS-00J7B1  | 752 GB | 9       | 976   | 1     | 2.14   |
| Seagate   | ST91603110CS       | 160 GB | 1       | 781   | 0     | 2.14   |
| Hitachi   | HDS723020BLE640    | 2 TB   | 10      | 780   | 0     | 2.14   |
| WDC       | WD800JD-00HKA0     | 80 GB  | 3       | 849   | 2     | 2.14   |
| WDC       | WD10EURX-63FH1Y0   | 1 TB   | 5       | 778   | 0     | 2.13   |
| Samsung   | HD160JJ-P          | 160 GB | 10      | 1266  | 608   | 2.13   |
| WDC       | WD1600AAJS-60PSA0  | 160 GB | 4       | 950   | 257   | 2.13   |
| Seagate   | ST10000NM0016-1... | 10 TB  | 9       | 777   | 0     | 2.13   |
| WDC       | WD400BD-75MRA1     | 40 GB  | 3       | 777   | 0     | 2.13   |
| WDC       | WD6400AAKS-00A7B2  | 640 GB | 6       | 776   | 0     | 2.13   |
| WDC       | WD1200JB-00DUA3    | 120 GB | 2       | 1239  | 2     | 2.13   |
| WDC       | WD10EARX-32N0YB0   | 1 TB   | 3       | 799   | 5     | 2.13   |
| Toshiba   | MD04ACA400         | 4 TB   | 8       | 998   | 501   | 2.12   |
| WDC       | WD2500AAJS-00VTA0  | 250 GB | 23      | 942   | 70    | 2.12   |
| WDC       | WD2500BB-00GUA0    | 250 GB | 1       | 773   | 0     | 2.12   |
| WDC       | WD1600BEVS-08VAT2  | 160 GB | 7       | 838   | 1     | 2.12   |
| WDC       | WD2500JS-60NCB2    | 250 GB | 2       | 773   | 0     | 2.12   |
| WDC       | WD2500JS-00NCB1    | 250 GB | 10      | 1117  | 34    | 2.12   |
| Hitachi   | HTS723225L9A362    | 250 GB | 1       | 770   | 0     | 2.11   |
| Samsung   | HD083GJ            | 80 GB  | 4       | 769   | 0     | 2.11   |
| WDC       | WD1600AAJS-07PSA0  | 160 GB | 3       | 1618  | 9     | 2.10   |
| WDC       | WD10EALS-002BA0    | 1 TB   | 3       | 766   | 0     | 2.10   |
| WDC       | WD10EURX-63C57Y0   | 1 TB   | 4       | 915   | 1     | 2.10   |
| WDC       | WD3200AAKX-083CA1  | 320 GB | 1       | 763   | 0     | 2.09   |
| Hitachi   | HDS721612PLA380    | 120 GB | 9       | 1157  | 2     | 2.09   |
| WDC       | WD1002FBYS-18W8B0  | 1 TB   | 2       | 762   | 0     | 2.09   |
| WDC       | WD7501AALS-00E8B0  | 752 GB | 4       | 1396  | 4     | 2.09   |
| Samsung   | HD040GJ            | 40 GB  | 5       | 959   | 25    | 2.09   |
| Hitachi   | HTS725032A9A360    | 320 GB | 2       | 757   | 0     | 2.07   |
| WDC       | WD2500JD-55HBB0    | 250 GB | 2       | 1468  | 16    | 2.07   |
| WDC       | WD1600AAJS-07M0A0  | 160 GB | 7       | 1158  | 2     | 2.07   |
| WDC       | WD5001AALS-00E3A0  | 500 GB | 13      | 991   | 93    | 2.06   |
| WDC       | WD4003FZEX-00Z4SA0 | 4 TB   | 7       | 752   | 0     | 2.06   |
| WDC       | WD3000JS-19PDB0    | 304 GB | 1       | 751   | 0     | 2.06   |
| WDC       | WD30EZRX-00D8PB0   | 3 TB   | 28      | 844   | 14    | 2.06   |
| HGST      | HMS5C4040ALE640    | 4 TB   | 3       | 750   | 0     | 2.06   |
| WDC       | WD6400AAKS-65A7B0  | 640 GB | 6       | 830   | 2     | 2.05   |
| WDC       | WD5000HHTZ-04N21V0 | 500 GB | 7       | 748   | 0     | 2.05   |
| Seagate   | ST3000DM001-1ER166 | 3 TB   | 46      | 758   | 38    | 2.05   |
| WDC       | WD3001FFSX-68JNUN0 | 3 TB   | 1       | 747   | 0     | 2.05   |
| WDC       | WD6400AAKS-00A7B0  | 640 GB | 14      | 932   | 4     | 2.05   |
| WDC       | WD20EARX-00PASB0   | 2 TB   | 108     | 1014  | 105   | 2.05   |
| Seagate   | ST3320620AS        | 320 GB | 122     | 1136  | 221   | 2.05   |
| Seagate   | ST340212AS         | 40 GB  | 3       | 1192  | 70    | 2.05   |
| WDC       | WD7500AACS-00D6B1  | 752 GB | 5       | 1014  | 3     | 2.05   |
| WDC       | WD400BB-60JKA0     | 40 GB  | 2       | 746   | 0     | 2.04   |
| HGST      | HDN728080ALE604    | 8 TB   | 1       | 745   | 0     | 2.04   |
| Quantum   | FIREBALLP AS40.0   | 40 GB  | 1       | 744   | 0     | 2.04   |
| WDC       | WD10EURX-61C57Y0   | 1 TB   | 1       | 744   | 0     | 2.04   |
| WDC       | WD10EALX-759BA1    | 1 TB   | 6       | 1218  | 4     | 2.04   |
| WDC       | WD10EACS-00ZJB0    | 1 TB   | 8       | 1311  | 85    | 2.03   |
| Hitachi   | HDS723015BLA642    | 1.5 TB | 9       | 911   | 22    | 2.03   |
| Hitachi   | HUS724030ALE641    | 3 TB   | 12      | 773   | 105   | 2.03   |
| WDC       | WD6400AAKS-65Z7B0  | 640 GB | 6       | 859   | 5     | 2.02   |
| ExcelStor | J9250S             | 250 GB | 4       | 735   | 0     | 2.01   |
| WDC       | WD10EADS-11M2B3    | 1 TB   | 3       | 734   | 0     | 2.01   |
| Seagate   | ST4000LM016-1N2170 | 4 TB   | 2       | 734   | 0     | 2.01   |
| WDC       | WD2000F9YZ-09N20L1 | 2 TB   | 1       | 733   | 0     | 2.01   |
| WDC       | WD20EFRX-68AX9N0   | 2 TB   | 16      | 873   | 1     | 2.01   |
| Samsung   | HD300LJ            | 304 GB | 9       | 1235  | 380   | 2.01   |
| WDC       | WD1200JB-00EVA0    | 120 GB | 4       | 731   | 0     | 2.00   |
| WDC       | WD5000AAKS-00A7B0  | 500 GB | 29      | 1121  | 8     | 2.00   |
| WDC       | WD3200AAJS-07M0A0  | 320 GB | 4       | 846   | 2     | 2.00   |
| HGST      | HDN724020ALE640    | 2 TB   | 1       | 729   | 0     | 2.00   |
| WDC       | WD2500AAKX-221CA1  | 250 GB | 2       | 1139  | 4     | 1.99   |
| Hitachi   | HDT721032SLA360    | 320 GB | 23      | 1160  | 10    | 1.98   |
| Hitachi   | HCS5C1010CLA382    | 1 TB   | 2       | 722   | 0     | 1.98   |
| WDC       | WD15EARS-00S0XB0   | 1.5 TB | 3       | 947   | 1     | 1.97   |
| Seagate   | ST9320421ASG       | 320 GB | 2       | 887   | 1     | 1.97   |
| Fujitsu   | MHV2100AH          | 100 GB | 2       | 719   | 0     | 1.97   |
| WDC       | WD6402AAEX-00Z3A0  | 640 GB | 3       | 719   | 0     | 1.97   |
| Seagate   | ST1000VX001-1Z4102 | 1 TB   | 3       | 717   | 0     | 1.97   |
| WDC       | WD80EFAX-68LHPN0   | 8 TB   | 10      | 716   | 0     | 1.96   |
| Seagate   | ST310211A          | 10 GB  | 1       | 716   | 0     | 1.96   |
| WDC       | WD2500AAKX-753CA1  | 250 GB | 13      | 885   | 82    | 1.96   |
| WDC       | WD15EADS-00S2B0    | 1.5 TB | 2       | 1647  | 10    | 1.96   |
| WDC       | WD5000BEVT-16A0RT0 | 500 GB | 1       | 713   | 0     | 1.95   |
| WDC       | WD6400AAKS-22A7B0  | 640 GB | 12      | 1182  | 3     | 1.95   |
| WDC       | WD20NMVW-11AV3S3   | 2 TB   | 2       | 712   | 0     | 1.95   |
| WDC       | WD1600JS-58NCB1    | 160 GB | 1       | 712   | 0     | 1.95   |
| Hitachi   | HTS545032B9SA00    | 320 GB | 5       | 944   | 462   | 1.95   |
| WDC       | WD800JD-00LSA0     | 80 GB  | 22      | 972   | 10    | 1.95   |
| Seagate   | ST1000VM002-9ZL162 | 1 TB   | 1       | 709   | 0     | 1.95   |
| WDC       | WD200BB-32CFC0     | 20 GB  | 1       | 709   | 0     | 1.94   |
| WDC       | WD2500JS-75NCB3    | 250 GB | 4       | 1000  | 25    | 1.93   |
| HGST      | HDN726060ALE614    | 6 TB   | 4       | 705   | 0     | 1.93   |
| WDC       | WD2500KS-00MJB0    | 250 GB | 25      | 942   | 17    | 1.93   |
| WDC       | WD2500AAKX-083CA1  | 250 GB | 10      | 1064  | 3     | 1.93   |
| WDC       | WD40EFRX-68WT0N0   | 4 TB   | 71      | 923   | 2     | 1.93   |
| WDC       | WD3200AAJS-65B4A0  | 320 GB | 1       | 699   | 0     | 1.92   |
| Seagate   | ST2000DL003-9VT166 | 2 TB   | 82      | 903   | 85    | 1.91   |
| WDC       | WD2500YS-01SHB1    | 250 GB | 8       | 1054  | 4     | 1.91   |
| WDC       | WD6400BPVT-35HXZT1 | 640 GB | 2       | 696   | 0     | 1.91   |
| WDC       | WD2500LPVT-00G33T0 | 250 GB | 1       | 696   | 0     | 1.91   |
| WDC       | WD2500BMVV-11DCLS0 | 250 GB | 1       | 694   | 0     | 1.90   |
| WDC       | WD5000AAJS-00YFA0  | 500 GB | 5       | 884   | 33    | 1.90   |
| WDC       | WD3200AAJS-65VWA0  | 320 GB | 3       | 692   | 0     | 1.90   |
| WDC       | WD3200BEVE-00A0HT0 | 320 GB | 3       | 691   | 0     | 1.90   |
| HP        | MB2000GCWDA        | 2 TB   | 2       | 691   | 0     | 1.89   |
| WDC       | WD10EZEX-00ZF5A0   | 1 TB   | 19      | 816   | 111   | 1.89   |
| WDC       | WD2500BEKT-75PVMT1 | 250 GB | 1       | 689   | 0     | 1.89   |
| Seagate   | ST1000VM002-1ET162 | 1 TB   | 2       | 688   | 0     | 1.89   |
| WDC       | WD10EAVS-00D7B1    | 1 TB   | 14      | 1045  | 181   | 1.89   |
| Seagate   | ST340215AS         | 40 GB  | 1       | 686   | 0     | 1.88   |
| Seagate   | ST960813AS         | 64 GB  | 3       | 873   | 4     | 1.88   |
| Seagate   | ST3160812AS        | 160 GB | 41      | 1074  | 367   | 1.88   |
| WDC       | WD5000AAKS-65YGA0  | 500 GB | 8       | 796   | 8     | 1.88   |
| Samsung   | HD103SI            | 1 TB   | 40      | 952   | 135   | 1.88   |
| Fujitsu   | MHZ2080BH G2       | 80 GB  | 1       | 684   | 0     | 1.88   |
| Samsung   | HD103SJ            | 1 TB   | 116     | 866   | 12    | 1.87   |
| WDC       | WD30PURX-64P6ZY0   | 3 TB   | 4       | 683   | 0     | 1.87   |
| WDC       | WD10EACS-00D6B1    | 1 TB   | 4       | 2065  | 478   | 1.87   |
| WDC       | WD2500AAJS-22RYA0  | 250 GB | 2       | 771   | 213   | 1.87   |
| WDC       | WD20EADS-00S2B0    | 2 TB   | 2       | 750   | 2     | 1.87   |
| Hitachi   | HUA721010KLA330... | 1 TB   | 1       | 2715  | 3     | 1.86   |
| WDC       | WD10EADS-65L5B1    | 1 TB   | 10      | 1110  | 4     | 1.86   |
| Hitachi   | HUA722020ALA331    | 2 TB   | 7       | 918   | 2     | 1.86   |
| WDC       | WD800BB-63JKC0     | 80 GB  | 1       | 676   | 0     | 1.85   |
| Hitachi   | HDT721010SLA360    | 1 TB   | 36      | 1191  | 17    | 1.85   |
| WDC       | WD2000F9YZ-09N20L0 | 2 TB   | 1       | 675   | 0     | 1.85   |
| WDC       | WD15EARS-22Z5B1    | 1.5 TB | 3       | 675   | 0     | 1.85   |
| WDC       | WD20EZRX-00D8PB0   | 2 TB   | 57      | 720   | 9     | 1.85   |
| Seagate   | ST3320413AS        | 320 GB | 14      | 1010  | 57    | 1.85   |
| Seagate   | ST4000NE0025-2E... | 4 TB   | 4       | 673   | 0     | 1.84   |
| WDC       | WD10EALX-009BA0    | 1 TB   | 63      | 888   | 22    | 1.84   |
| WDC       | WD800BB-75DKA0     | 80 GB  | 1       | 672   | 0     | 1.84   |
| Hitachi   | HDP725032GLA360    | 320 GB | 17      | 1051  | 94    | 1.84   |
| Seagate   | ST3320413CS        | 320 GB | 10      | 727   | 114   | 1.84   |
| WDC       | WD1200JS-55MHB0    | 120 GB | 2       | 671   | 0     | 1.84   |
| HGST      | HUS722T2TALA604    | 2 TB   | 3       | 671   | 0     | 1.84   |
| WDC       | WD5000LPVT-60G33T0 | 500 GB | 1       | 670   | 0     | 1.84   |
| WDC       | WD10JPVX-08JC3T5   | 1 TB   | 11      | 680   | 1     | 1.84   |
| WDC       | WD3200AAKS-75VYA0  | 320 GB | 3       | 670   | 0     | 1.84   |
| WDC       | WD3200AAJS-40RYA0  | 320 GB | 2       | 1197  | 389   | 1.83   |
| WDC       | WD6400AAKS-65A7B2  | 640 GB | 14      | 1213  | 36    | 1.83   |
| WDC       | WD4001FFSX-68JNUN0 | 4 TB   | 2       | 667   | 0     | 1.83   |
| WDC       | WD1502FYPS-01U1B1  | 1.5 TB | 1       | 667   | 0     | 1.83   |
| WDC       | WD1003FBYZ-010FB0  | 1 TB   | 14      | 755   | 2     | 1.83   |
| WDC       | WD40EZRX-00SPEB0   | 4 TB   | 25      | 746   | 3     | 1.82   |
| WDC       | WD2000JD-22HBC0    | 200 GB | 3       | 1330  | 4     | 1.82   |
| Seagate   | ST31000524NS       | 1 TB   | 7       | 1199  | 221   | 1.82   |
| WDC       | WD5001AALS-00L3B2  | 500 GB | 33      | 990   | 28    | 1.82   |
| WDC       | WD30EURS-63R8UY0   | 3 TB   | 2       | 664   | 0     | 1.82   |
| Seagate   | ST4000VM000-1F3168 | 4 TB   | 5       | 663   | 0     | 1.82   |
| Seagate   | ST3000NM0033-9Z... | 3 TB   | 4       | 880   | 5     | 1.82   |
| WDC       | WD2000JB-00REA0    | 200 GB | 4       | 885   | 1     | 1.82   |
| Apple     | HDD ST1000LM024    | 1 TB   | 1       | 662   | 0     | 1.82   |
| WDC       | WD1200JD-00FYB0    | 120 GB | 1       | 661   | 0     | 1.81   |
| WDC       | WD800AAJS-00PSA0   | 80 GB  | 22      | 769   | 34    | 1.81   |
| WDC       | WD1600AVBS-63SVA0  | 160 GB | 1       | 658   | 0     | 1.80   |
| Hitachi   | HDT721032SLA380    | 320 GB | 6       | 928   | 390   | 1.80   |
| WDC       | WD5000BPVT-75HXZT1 | 500 GB | 1       | 657   | 0     | 1.80   |
| WDC       | WD5000AAJS-00TKA0  | 500 GB | 1       | 656   | 0     | 1.80   |
| WDC       | WD2500AAKX-22ERMA0 | 250 GB | 1       | 656   | 0     | 1.80   |
| WDC       | WD1600JS-98NCB1    | 160 GB | 1       | 655   | 0     | 1.80   |
| WDC       | WD5000AAKS-07V0A0  | 500 GB | 1       | 654   | 0     | 1.79   |
| WDC       | WD5000BMVW-11S5XS0 | 500 GB | 6       | 811   | 1     | 1.79   |
| WDC       | WD2500AAKS-00VSA0  | 250 GB | 26      | 868   | 16    | 1.79   |
| WDC       | WD3200AAJS-65RYA0  | 320 GB | 2       | 652   | 0     | 1.79   |
| WDC       | WD5000AAKS-00Z7B0  | 500 GB | 1       | 652   | 0     | 1.79   |
| WDC       | WD10TMVW-11ZSMS5   | 1 TB   | 6       | 810   | 308   | 1.78   |
| WDC       | WD400BD-60JPA0     | 40 GB  | 1       | 651   | 0     | 1.78   |
| Hitachi   | HDS721010CLA632    | 1 TB   | 2       | 651   | 0     | 1.78   |
| Hitachi   | HDS722580VLSA80    | 82 GB  | 3       | 1101  | 671   | 1.78   |
| Seagate   | ST9500420ASG       | 500 GB | 3       | 709   | 1     | 1.78   |
| WDC       | WD20NMVW-11AV3S2   | 2 TB   | 21      | 820   | 3     | 1.78   |
| WDC       | WD10EURX-63UY4Y0   | 1 TB   | 3       | 647   | 0     | 1.78   |
| WDC       | WD20EARS-00MVWB0   | 2 TB   | 69      | 1094  | 107   | 1.77   |
| Hitachi   | HTS721010G9SA00    | 100 GB | 2       | 1317  | 58    | 1.77   |
| Seagate   | ST980812AS         | 80 GB  | 1       | 647   | 0     | 1.77   |
| WDC       | WD3200BEKT-75PVMT1 | 320 GB | 5       | 946   | 3     | 1.77   |
| WDC       | WD5000AVDS-63U7B1  | 500 GB | 8       | 705   | 3     | 1.77   |
| WDC       | WD5000AAKS-07TMA0  | 500 GB | 1       | 646   | 0     | 1.77   |
| WDC       | WD10EARS-22Y5B1    | 1 TB   | 13      | 1000  | 21    | 1.77   |
| WDC       | WD2500HHTZ-04N21V0 | 250 GB | 8       | 706   | 1     | 1.77   |
| Toshiba   | DT01ABA050V        | 500 GB | 1       | 644   | 0     | 1.77   |
| WDC       | WD6001FZWX-00A2VA0 | 6 TB   | 5       | 644   | 0     | 1.77   |
| WDC       | WD2500AAJS-08L7A0  | 250 GB | 3       | 642   | 0     | 1.76   |
| WDC       | WD5002AALX-00J37A0 | 500 GB | 16      | 741   | 67    | 1.76   |
| WDC       | WD1001FALS-19J7B0  | 1 TB   | 1       | 641   | 0     | 1.76   |
| Seagate   | ST3200820AS        | 200 GB | 25      | 913   | 425   | 1.75   |
| Toshiba   | DT01ABA200V        | 2 TB   | 1       | 639   | 0     | 1.75   |
| WDC       | WD800JB-00ETA0     | 80 GB  | 5       | 1354  | 273   | 1.75   |
| WDC       | WD1600JS-98MHB0    | 160 GB | 1       | 638   | 0     | 1.75   |
| WDC       | WD7500BPVX-60JC3T0 | 752 GB | 7       | 762   | 2     | 1.74   |
| WDC       | WD20EARX-00ZUDB0   | 2 TB   | 2       | 1181  | 2     | 1.74   |
| WDC       | WD1002FBYS-43P1B0  | 1 TB   | 2       | 1021  | 39    | 1.74   |
| Hitachi   | HDT721016SLA380    | 160 GB | 18      | 860   | 5     | 1.74   |
| Seagate   | ST2000DM001-1CH164 | 2 TB   | 155     | 760   | 125   | 1.73   |
| WDC       | WD3200AAKS-22SBA0  | 320 GB | 1       | 633   | 0     | 1.73   |
| WDC       | WD7500BPVT-16HXZT3 | 752 GB | 1       | 632   | 0     | 1.73   |
| WDC       | WD3200AAKX-221CA1  | 320 GB | 3       | 631   | 0     | 1.73   |
| Hitachi   | HDS721050CLA662    | 500 GB | 12      | 694   | 86    | 1.73   |
| Seagate   | ST380815AS         | 80 GB  | 155     | 829   | 221   | 1.73   |
| Hitachi   | HTS723220L9A360    | 200 GB | 1       | 630   | 0     | 1.73   |
| WDC       | WD1600AABS-00PRA0  | 160 GB | 1       | 630   | 0     | 1.73   |
| Seagate   | ST8000VN0022-2E... | 8 TB   | 27      | 788   | 9     | 1.72   |
| WDC       | WD7500BPKX-60HPJT0 | 752 GB | 1       | 627   | 0     | 1.72   |
| WDC       | WD4000BEVT-11ZAT0  | 400 GB | 1       | 626   | 0     | 1.72   |
| WDC       | WD10EACS-32ZJB0    | 1 TB   | 1       | 626   | 0     | 1.72   |
| Seagate   | ST6000VN0041-2E... | 6 TB   | 2       | 626   | 0     | 1.72   |
| WDC       | WD15EADS-00R6B0    | 1.5 TB | 1       | 625   | 0     | 1.71   |
| Fujitsu   | MHY2250BH          | 250 GB | 7       | 841   | 47    | 1.71   |
| Hitachi   | HDS725050KLA360    | 500 GB | 6       | 1732  | 10    | 1.71   |
| WDC       | WD7500BPKX-75HPJT0 | 752 GB | 4       | 622   | 0     | 1.71   |
| WDC       | WD80EFZX-68UW8N0   | 8 TB   | 11      | 622   | 0     | 1.70   |
| WDC       | WD360GD-00FLC0     | 37 GB  | 1       | 622   | 0     | 1.70   |
| WDC       | WD6000HLHX-01JJPV0 | 600 GB | 10      | 1105  | 13    | 1.70   |
| WDC       | WD2003FZEX-00SRLA0 | 2 TB   | 30      | 647   | 3     | 1.70   |
| WDC       | WD20SPZX-22CRAT0   | 2 TB   | 1       | 620   | 0     | 1.70   |
| WDC       | WD800JD-00MSA1     | 80 GB  | 12      | 845   | 7     | 1.70   |
| WDC       | WD1600AAJS-55PSA0  | 160 GB | 1       | 620   | 0     | 1.70   |
| Seagate   | ST6000DM004-2EH11C | 6 TB   | 1       | 619   | 0     | 1.70   |
| WDC       | WD10EZRX-00A8LB0   | 1 TB   | 56      | 769   | 35    | 1.70   |
| Seagate   | ST4000DX001-1CE168 | 4 TB   | 13      | 911   | 60    | 1.69   |
| WDC       | WD10EARX-00N0YB0   | 1 TB   | 54      | 793   | 4     | 1.69   |
| WDC       | WD3200AAJS-00G0A0  | 320 GB | 1       | 617   | 0     | 1.69   |
| Samsung   | HD103UJ            | 1 TB   | 65      | 1166  | 192   | 1.69   |
| Hitachi   | HDS721010CLA332    | 1 TB   | 121     | 977   | 86    | 1.68   |
| Samsung   | HD154UI            | 1.5 TB | 41      | 1042  | 298   | 1.68   |
| Hitachi   | HCS5C1032CLA382    | 320 GB | 2       | 883   | 2     | 1.68   |
| WDC       | WD5000AAKS-00V0A0  | 500 GB | 4       | 675   | 2     | 1.68   |
| WDC       | WD10EALS-00Z8A0    | 1 TB   | 24      | 921   | 61    | 1.68   |
| WDC       | WD2500AAKX-60U6AA0 | 250 GB | 5       | 611   | 0     | 1.68   |
| WDC       | WD1003FBYX-18Y7B0  | 1 TB   | 2       | 955   | 2     | 1.68   |
| Hitachi   | HDS721010CLA630    | 1 TB   | 7       | 680   | 1     | 1.67   |
| WDC       | WD7500AADS-00M2B0  | 752 GB | 22      | 1071  | 18    | 1.67   |
| WDC       | WD800JD-00LUA0     | 80 GB  | 1       | 610   | 0     | 1.67   |
| Hitachi   | HDS721075CLA332    | 752 GB | 2       | 610   | 0     | 1.67   |
| HP        | MB1000GDUNU        | 1 TB   | 1       | 609   | 0     | 1.67   |
| WDC       | WD3200KS-00PFB0    | 320 GB | 3       | 1056  | 31    | 1.67   |
| Seagate   | ST31000526SV       | 1 TB   | 3       | 769   | 343   | 1.67   |
| Seagate   | ST4000DM005-2DP166 | 4 TB   | 20      | 609   | 64    | 1.66   |
| WDC       | WD800JD-60LSA0     | 80 GB  | 6       | 825   | 132   | 1.66   |
| WDC       | WD5000AAJS-00A8B0  | 500 GB | 3       | 605   | 0     | 1.66   |
| Seagate   | ST340014A          | 40 GB  | 85      | 800   | 35    | 1.66   |
| Seagate   | ST3750640AS        | 752 GB | 10      | 1190  | 286   | 1.66   |
| WDC       | WD3000JS-60PDB0    | 304 GB | 2       | 603   | 0     | 1.65   |
| Seagate   | ST980411ASG        | 80 GB  | 2       | 831   | 7     | 1.65   |
| WDC       | WD800AAJS-00WAA0   | 80 GB  | 6       | 603   | 2     | 1.65   |
| Seagate   | ST2000DX001-1NS164 | 2 TB   | 10      | 682   | 1     | 1.65   |
| Hitachi   | HTS545016B9SA02    | 160 GB | 1       | 602   | 0     | 1.65   |
| WDC       | WD5003AZEX-00MK2A0 | 500 GB | 12      | 651   | 1     | 1.65   |
| WDC       | WD1600AAJS-00PSA0  | 160 GB | 27      | 856   | 53    | 1.65   |
| Seagate   | ST9200420AS        | 200 GB | 2       | 601   | 0     | 1.65   |
| WDC       | WD1200JS-00MHB0    | 120 GB | 15      | 635   | 1     | 1.65   |
| WDC       | WD800JD-23LSA0     | 80 GB  | 1       | 1202  | 1     | 1.65   |
| Samsung   | HD642JJ            | 640 GB | 25      | 1270  | 422   | 1.65   |
| WDC       | WD1600JS-23MHB0    | 160 GB | 1       | 600   | 0     | 1.64   |
| Samsung   | HD321HJ            | 320 GB | 9       | 985   | 130   | 1.64   |
| WDC       | WD15EARX-00PASB0   | 1.5 TB | 11      | 663   | 2     | 1.64   |
| Seagate   | ST3160815AS        | 160 GB | 178     | 851   | 357   | 1.64   |
| Hitachi   | HDP725040GLA360    | 400 GB | 4       | 1097  | 4     | 1.63   |
| WDC       | WD10EURX-56FH1Y0   | 1 TB   | 2       | 596   | 0     | 1.63   |
| WDC       | WD3200BEVT-75ZCT2  | 320 GB | 10      | 655   | 76    | 1.62   |
| Seagate   | ST1000DX001-SSH... | 1 TB   | 1       | 590   | 0     | 1.62   |
| Apple     | HDD ST750LM022     | 752 GB | 1       | 589   | 0     | 1.61   |
| WDC       | WD1600BEVS-22UST0  | 160 GB | 3       | 782   | 63    | 1.61   |
| WDC       | WD800JD-19LSA0     | 80 GB  | 1       | 588   | 0     | 1.61   |
| WDC       | WD3200AAJS-00VWA0  | 320 GB | 11      | 656   | 42    | 1.61   |
| Hitachi   | HDS728080PLAT20    | 82 GB  | 20      | 738   | 7     | 1.61   |
| WDC       | WD2000JS-00MHB0    | 200 GB | 9       | 780   | 54    | 1.61   |
| WDC       | WD1600AAJS-00M0A0  | 160 GB | 6       | 784   | 68    | 1.61   |
| Hitachi   | HDT725050VLA360    | 500 GB | 5       | 1151  | 37    | 1.60   |
| WDC       | WD20EARS-55MVWB0   | 2 TB   | 1       | 584   | 0     | 1.60   |
| Seagate   | ST31500541AS       | 1.5 TB | 11      | 754   | 34    | 1.60   |
| WDC       | WD5000AAKS-00D2B0  | 500 GB | 12      | 1035  | 8     | 1.60   |
| HGST      | HDS724040ALE640    | 4 TB   | 3       | 1006  | 2     | 1.60   |
| Maxtor    | STM3160215A        | 160 GB | 10      | 630   | 307   | 1.60   |
| WDC       | WD800JD-22MSA1     | 80 GB  | 10      | 652   | 1     | 1.60   |
| WDC       | WD2500AVJS-63WDA0  | 250 GB | 2       | 582   | 0     | 1.60   |
| WDC       | WD1600BEVS-75RST0  | 160 GB | 2       | 579   | 0     | 1.59   |
| Maxtor    | STM3320620A        | 320 GB | 2       | 579   | 0     | 1.59   |
| WDC       | WD4002FFWX-68TZ4N0 | 4 TB   | 1       | 579   | 0     | 1.59   |
| WDC       | WD2500BEKT-60V5T1  | 250 GB | 1       | 578   | 0     | 1.59   |
| WDC       | WD2500AAJS-07M0A0  | 250 GB | 5       | 776   | 4     | 1.59   |
| WDC       | WD1600BB-55RDA0    | 160 GB | 3       | 682   | 2     | 1.58   |
| Seagate   | ST3160318AS        | 160 GB | 63      | 791   | 94    | 1.58   |
| WDC       | WD6400AAKS-40H2B0  | 640 GB | 3       | 1324  | 271   | 1.58   |
| WDC       | WD10EZEX-00KUWA0   | 1 TB   | 21      | 666   | 1     | 1.58   |
| Seagate   | ST1000DM005 HD1... | 1 TB   | 13      | 658   | 2     | 1.58   |
| WDC       | WD10EZEX-19M2NA0   | 1 TB   | 1       | 576   | 0     | 1.58   |
| WDC       | WD2500BUCT-63TWBY0 | 250 GB | 2       | 884   | 519   | 1.58   |
| Samsung   | SP1644N            | 160 GB | 3       | 683   | 527   | 1.58   |
| Toshiba   | MQ01ABC150         | 1.5 TB | 1       | 574   | 0     | 1.57   |
| WDC       | WD800BEVS-08RST2   | 80 GB  | 4       | 574   | 0     | 1.57   |
| Seagate   | ST3160316AS        | 160 GB | 13      | 688   | 7     | 1.57   |
| Seagate   | ST3808110AS        | 80 GB  | 35      | 1025  | 438   | 1.57   |
| WDC       | WD800JD-75JNA0     | 80 GB  | 3       | 1489  | 39    | 1.57   |
| Seagate   | ST3160212AS        | 160 GB | 2       | 572   | 0     | 1.57   |
| WDC       | WD1600AAJS-60WAA0  | 160 GB | 5       | 625   | 203   | 1.56   |
| WDC       | WD3200AAKS-00VYA0  | 320 GB | 7       | 649   | 51    | 1.56   |
| Samsung   | HD253GJ            | 250 GB | 8       | 752   | 15    | 1.56   |
| WDC       | WD1003FZEX-00MK2A0 | 1 TB   | 62      | 619   | 1     | 1.56   |
| Hitachi   | HUA723020ALA641    | 2 TB   | 21      | 657   | 1     | 1.55   |
| WDC       | WD10JFCX-68N6GN0   | 1 TB   | 15      | 637   | 1     | 1.55   |
| Seagate   | ST3320418AS        | 320 GB | 87      | 912   | 144   | 1.55   |
| Seagate   | ST1000NX0443       | 1 TB   | 2       | 566   | 0     | 1.55   |
| Seagate   | ST10000VN0004-1... | 10 TB  | 17      | 604   | 1     | 1.55   |
| Seagate   | ST3320820AS_Q      | 320 GB | 2       | 1793  | 1068  | 1.54   |
| WDC       | WD2500AAKX-75U6AA0 | 250 GB | 8       | 947   | 3     | 1.54   |
| Seagate   | ST3400620AS        | 400 GB | 27      | 1119  | 16    | 1.54   |
| WDC       | WD60EZRX-00MVLB1   | 6 TB   | 8       | 691   | 1     | 1.54   |
| Samsung   | HD502HJ            | 500 GB | 108     | 785   | 69    | 1.54   |
| WDC       | WD40PURX-64GVNY0   | 4 TB   | 2       | 561   | 0     | 1.54   |
| WDC       | WD800JD-08MSA1     | 80 GB  | 1       | 560   | 0     | 1.53   |
| WDC       | WD1000DHTZ-04N21V1 | 1 TB   | 1       | 559   | 0     | 1.53   |
| WDC       | WD2500JB-98GVA0    | 250 GB | 1       | 3354  | 5     | 1.53   |
| WDC       | WD2500AAJB-00WGA0  | 250 GB | 5       | 1069  | 115   | 1.53   |
| Seagate   | ST3250823A         | 250 GB | 6       | 977   | 440   | 1.53   |
| WDC       | WD6400BPVT-75HXZT1 | 640 GB | 5       | 658   | 2     | 1.53   |
| WDC       | WD800JD-22LSA0     | 80 GB  | 8       | 715   | 83    | 1.53   |
| WDC       | WD800JD-00LSA5     | 80 GB  | 2       | 557   | 0     | 1.53   |
| Seagate   | ST1000DL002-9TT153 | 1 TB   | 37      | 1030  | 326   | 1.53   |
| WDC       | WD800AAJS-75M0A0   | 80 GB  | 4       | 1117  | 8     | 1.52   |
| Seagate   | ST3500630NS        | 500 GB | 6       | 713   | 441   | 1.52   |
| WDC       | WD5000AAVS-00ZTB0  | 500 GB | 4       | 555   | 0     | 1.52   |
| WDC       | WD20EZRX-00DC0B0   | 2 TB   | 35      | 672   | 19    | 1.52   |
| WDC       | WD2500BEVS-00UST0  | 250 GB | 2       | 812   | 2     | 1.52   |
| WDC       | WD3000JS-00PDB0    | 304 GB | 1       | 554   | 0     | 1.52   |
| WDC       | WD5000BMVW-11AMCS4 | 500 GB | 4       | 799   | 2     | 1.52   |
| Seagate   | ST3250824AS        | 250 GB | 23      | 875   | 702   | 1.52   |
| Seagate   | ST380011A          | 80 GB  | 172     | 814   | 75    | 1.51   |
| Seagate   | ST3250620AS        | 250 GB | 54      | 921   | 329   | 1.51   |
| WDC       | WD5000AADS-00L4B1  | 500 GB | 7       | 905   | 5     | 1.51   |
| WDC       | WD3200BPVT-00HXZT0 | 320 GB | 1       | 549   | 0     | 1.51   |
| Seagate   | ST2000VX000-1ES164 | 2 TB   | 8       | 549   | 0     | 1.50   |
| WDC       | WD1600JS-00SGB0    | 160 GB | 1       | 549   | 0     | 1.50   |
| WDC       | WD400BB-00JHC0     | 40 GB  | 4       | 872   | 24    | 1.50   |
| WDC       | WD2500AAKS-00YGA0  | 250 GB | 2       | 548   | 0     | 1.50   |
| Seagate   | ST360015A          | 64 GB  | 2       | 1494  | 5     | 1.50   |
| WDC       | WD360ADFD-00NLR1   | 37 GB  | 1       | 547   | 0     | 1.50   |
| Fujitsu   | MHW2120BH          | 120 GB | 19      | 615   | 27    | 1.50   |
| Seagate   | ST3250312AS        | 250 GB | 29      | 691   | 37    | 1.50   |
| WDC       | WD20EFRX-68EUZN0   | 2 TB   | 64      | 672   | 1     | 1.50   |
| Seagate   | ST3200827A         | 200 GB | 1       | 544   | 0     | 1.49   |
| WDC       | WD10EZEX-00ER1A0   | 1 TB   | 4       | 544   | 0     | 1.49   |
| Seagate   | ST3000VN007-2E4166 | 3 TB   | 2       | 544   | 0     | 1.49   |
| WDC       | WD3200BMVU-11A04S0 | 320 GB | 2       | 548   | 115   | 1.49   |
| WDC       | WD2000JD-00HBB0    | 200 GB | 5       | 897   | 3     | 1.49   |
| MediaMax  | WL1000GSA6472C     | 1 TB   | 1       | 543   | 0     | 1.49   |
| Hitachi   | HDT725025VLAT80    | 250 GB | 2       | 1843  | 2     | 1.49   |
| Seagate   | ST3320620A         | 320 GB | 24      | 859   | 5     | 1.49   |
| HGST      | HCC545050A7E380    | 500 GB | 3       | 664   | 1     | 1.48   |
| Toshiba   | DT01ABA300         | 3 TB   | 5       | 582   | 2     | 1.48   |
| WDC       | WD1600AAJS-22WAA0  | 160 GB | 5       | 998   | 3     | 1.48   |
| WDC       | WD2500BEVS-26UST0  | 250 GB | 5       | 540   | 0     | 1.48   |
| WDC       | WD3000HLFS-01G6U0  | 304 GB | 1       | 540   | 0     | 1.48   |
| Samsung   | HD502IJ            | 500 GB | 32      | 1139  | 288   | 1.48   |
| WDC       | WD1200JS-00MHB1    | 120 GB | 3       | 685   | 8     | 1.48   |
| WDC       | WD10EADS-114BB1    | 1 TB   | 1       | 1079  | 1     | 1.48   |
| WDC       | WD5000AAKS-75A7B0  | 500 GB | 4       | 673   | 2     | 1.48   |
| Toshiba   | HDWE160            | 6 TB   | 6       | 538   | 0     | 1.48   |
| WDC       | WD7500AZEX-00RKKA0 | 752 GB | 6       | 538   | 0     | 1.48   |
| WDC       | WD20EADS-00R6B0    | 2 TB   | 8       | 926   | 254   | 1.47   |
| Seagate   | ST3300620AS        | 304 GB | 2       | 538   | 0     | 1.47   |
| WDC       | WD1001FAES-55W7A0  | 1 TB   | 2       | 535   | 0     | 1.47   |
| Toshiba   | HDWE150            | 5 TB   | 10      | 609   | 1     | 1.47   |
| HGST      | HUH721212ALN600    | 12 TB  | 1       | 534   | 0     | 1.46   |
| WDC       | WD10EZEX-75ZF5A0   | 1 TB   | 7       | 587   | 288   | 1.46   |
| WDC       | WD800AAJS-22L7A0   | 80 GB  | 1       | 534   | 0     | 1.46   |
| WDC       | WD1600JS-22MHB0    | 160 GB | 3       | 700   | 9     | 1.46   |
| WDC       | WD3200AAKS-00L9A0  | 320 GB | 45      | 889   | 31    | 1.46   |
| Samsung   | HD105SI            | 1 TB   | 13      | 803   | 302   | 1.46   |
| Hitachi   | HDS728080PLA380    | 80 GB  | 41      | 836   | 56    | 1.45   |
| WDC       | WD15EZRX-00DC0B0   | 1.5 TB | 2       | 530   | 0     | 1.45   |
| Hitachi   | HDS5C1032CLA382    | 320 GB | 5       | 748   | 3     | 1.45   |
| Seagate   | ST360021A          | 64 GB  | 5       | 598   | 10    | 1.45   |
| WDC       | WD10EZEX-00RKKA0   | 1 TB   | 85      | 654   | 73    | 1.45   |
| WDC       | WD15EADS-00P8B0    | 1.5 TB | 13      | 1169  | 7     | 1.45   |
| WDC       | WD5000AZRX-00A8LB0 | 500 GB | 75      | 556   | 1     | 1.45   |
| WDC       | WD3200AAKS-75L9A0  | 320 GB | 19      | 821   | 45    | 1.45   |
| Seagate   | ST3750640NS        | 752 GB | 7       | 1166  | 449   | 1.45   |
| Hitachi   | HDS721050CLA362    | 500 GB | 130     | 728   | 30    | 1.45   |
| Seagate   | ST2000DM001-1ER164 | 2 TB   | 110     | 636   | 57    | 1.44   |
| WDC       | WD5000AAKS-007AA0  | 500 GB | 9       | 913   | 13    | 1.44   |
| WDC       | WD5000AACS-00G8B1  | 500 GB | 11      | 726   | 3     | 1.44   |
| Maxtor    | 6V200E0            | 208 GB | 9       | 923   | 116   | 1.44   |
| Seagate   | ST14000VN0008-2... | 14 TB  | 2       | 525   | 0     | 1.44   |
| WDC       | WD7500BPVT-00HXZT1 | 752 GB | 1       | 525   | 0     | 1.44   |
| WDC       | WD10EURX-83UY4Y0   | 1 TB   | 1       | 524   | 0     | 1.44   |
| WDC       | WD5000AAKS-22A7B0  | 500 GB | 17      | 1023  | 22    | 1.44   |
| WDC       | WD5000AAKX-603CA0  | 500 GB | 11      | 593   | 93    | 1.43   |
| Seagate   | ST4000NM0035-1V... | 4 TB   | 7       | 523   | 0     | 1.43   |
| Seagate   | ST160LM003 HN-M... | 160 GB | 3       | 522   | 0     | 1.43   |
| WDC       | WD2500BPVT-00JJ5T0 | 250 GB | 1       | 522   | 0     | 1.43   |
| Maxtor    | 4K020H1            | 20 GB  | 1       | 522   | 0     | 1.43   |
| WDC       | WD20EARX-32PASB0   | 2 TB   | 2       | 521   | 0     | 1.43   |
| WDC       | WD800BB-00JKC0     | 80 GB  | 2       | 520   | 0     | 1.43   |
| WDC       | WD6400AARS-003BB1  | 640 GB | 1       | 520   | 0     | 1.43   |
| WDC       | WD10EFRX-68PJCN0   | 1 TB   | 30      | 621   | 1     | 1.42   |
| WDC       | WD1600YD-01NVB1    | 164 GB | 1       | 519   | 0     | 1.42   |
| WDC       | WD3200AAKS-00B3A0  | 320 GB | 34      | 722   | 33    | 1.42   |
| Hitachi   | HTS722012K9SA00    | 120 GB | 5       | 576   | 407   | 1.41   |
| Seagate   | ST3160215ACE       | 160 GB | 3       | 809   | 72    | 1.41   |
| Seagate   | ST3120026AS        | 120 GB | 29      | 1088  | 9     | 1.41   |
| Seagate   | ST3200826AS        | 200 GB | 14      | 823   | 69    | 1.41   |
| Seagate   | ST4000DM000-2AE166 | 4 TB   | 3       | 513   | 0     | 1.41   |
| WDC       | WD1500HLFS-01MZUV0 | 150 GB | 2       | 511   | 0     | 1.40   |
| Seagate   | ST640LM000 HM641JI | 640 GB | 2       | 511   | 0     | 1.40   |
| Seagate   | ST1000VM002-1CT162 | 1 TB   | 4       | 509   | 0     | 1.40   |
| Seagate   | ST3000VX000-1CU166 | 3 TB   | 3       | 509   | 0     | 1.40   |
| WDC       | WD3200AAJS-55B4A0  | 320 GB | 2       | 749   | 4     | 1.40   |
| WDC       | WD5000LPVT-16G33T0 | 500 GB | 5       | 508   | 0     | 1.39   |
| WDC       | WD2500AAKS-00L9A0  | 250 GB | 10      | 909   | 4     | 1.39   |
| WDC       | WD6400AAKS-55A7B0  | 640 GB | 1       | 507   | 0     | 1.39   |
| WDC       | WD3200BEVT-08A23T1 | 320 GB | 6       | 625   | 2     | 1.39   |
| WDC       | WD7500AARS-00Y5B1  | 752 GB | 12      | 567   | 3     | 1.39   |
| HGST      | HUS724040ALA640    | 4 TB   | 3       | 720   | 673   | 1.38   |
| Hitachi   | HDS5C3030ALA630    | 3 TB   | 5       | 1334  | 5     | 1.38   |
| Toshiba   | MK2556GSYF         | 250 GB | 1       | 503   | 0     | 1.38   |
| Seagate   | ST3500413AS        | 500 GB | 128     | 648   | 74    | 1.38   |
| Seagate   | ST3250820AS        | 250 GB | 44      | 905   | 306   | 1.38   |
| Seagate   | ST1000VT000 HN-... | 1 TB   | 1       | 501   | 0     | 1.38   |
| WDC       | WD10EURX-73C57Y0   | 1 TB   | 3       | 501   | 0     | 1.37   |
| Seagate   | ST3160023A         | 160 GB | 17      | 841   | 302   | 1.37   |
| WDC       | WD1600JS-00NCB1    | 160 GB | 17      | 801   | 10    | 1.37   |
| WDC       | WD10EADX-00TDHB0   | 1 TB   | 5       | 826   | 13    | 1.37   |
| Seagate   | ST2000VX003-1HH164 | 2 TB   | 2       | 500   | 0     | 1.37   |
| Seagate   | ST380012ACE        | 80 GB  | 4       | 498   | 0     | 1.37   |
| WDC       | WD2500AAJS-22VTA0  | 250 GB | 8       | 617   | 1     | 1.37   |
| WDC       | WD400BB-00JHA0     | 40 GB  | 3       | 1145  | 4     | 1.36   |
| WDC       | WD800JD-55MSA1     | 80 GB  | 2       | 497   | 0     | 1.36   |
| Apple     | HDD ST1000DM003    | 1 TB   | 11      | 497   | 0     | 1.36   |
| Seagate   | ST3120026A         | 120 GB | 23      | 963   | 160   | 1.36   |
| WDC       | WD200EB-00BHF0     | 20 GB  | 1       | 992   | 1     | 1.36   |
| WDC       | WD800BB-55JKA0     | 80 GB  | 5       | 740   | 1     | 1.36   |
| Hitachi   | HUA722010CLA330    | 1 TB   | 14      | 812   | 77    | 1.36   |
| WDC       | WD1200JD-00GBB0    | 120 GB | 3       | 754   | 4     | 1.36   |
| ExcelStor | J880S              | 82 GB  | 2       | 495   | 0     | 1.36   |
| Fujitsu   | MPE3136AH          | 16 GB  | 1       | 494   | 0     | 1.35   |
| Hitachi   | HDP725050GLA360    | 500 GB | 82      | 1055  | 34    | 1.35   |
| WDC       | WD2500BEVT-75ZCT2  | 250 GB | 5       | 738   | 1     | 1.35   |
| WDC       | WD5000AAKS-00V2B0  | 500 GB | 3       | 663   | 1     | 1.35   |
| Seagate   | ST1000VX000-9YW162 | 1 TB   | 5       | 491   | 0     | 1.35   |
| WDC       | WD4000AAKS-00TMA0  | 400 GB | 4       | 561   | 1     | 1.35   |
| Hitachi   | HDS721616PLA380    | 160 GB | 83      | 915   | 81    | 1.34   |
| WDC       | WD800BB-00JHA0     | 80 GB  | 8       | 827   | 4     | 1.34   |
| WDC       | WD5000AAKS-00A7B2  | 500 GB | 32      | 881   | 13    | 1.34   |
| WDC       | WD5000AACS-32G8B1  | 500 GB | 1       | 487   | 0     | 1.33   |
| WDC       | WD1600AAJS-08PSA0  | 160 GB | 12      | 645   | 8     | 1.33   |
| WDC       | WD5000BEVT-35A0RT0 | 500 GB | 12      | 636   | 8     | 1.33   |
| WDC       | WD740ADFD-00NLR5   | 74 GB  | 2       | 486   | 0     | 1.33   |
| WDC       | WD10EADX-22TDHB0   | 1 TB   | 9       | 934   | 128   | 1.33   |
| HGST      | HUH728080ALN600    | 8 TB   | 1       | 485   | 0     | 1.33   |
| WDC       | WD3200AAJS-08L7A0  | 320 GB | 13      | 822   | 137   | 1.33   |
| Seagate   | ST1000DM003-1ER162 | 1 TB   | 204     | 507   | 31    | 1.33   |
| WDC       | WD800JD-55JRC0     | 80 GB  | 2       | 604   | 31    | 1.33   |
| Maxtor    | STM3320820AS       | 320 GB | 15      | 713   | 71    | 1.33   |
| Seagate   | ST98823A           | 80 GB  | 4       | 633   | 323   | 1.33   |
| Seagate   | ST2000DM001-9YN164 | 2 TB   | 55      | 903   | 421   | 1.33   |
| Fujitsu   | MHT2040AH          | 40 GB  | 1       | 484   | 0     | 1.33   |
| WDC       | WD10EZEX-22BN5A0   | 1 TB   | 20      | 567   | 2     | 1.33   |
| WDC       | WD3200BPVT-00JJ5T0 | 320 GB | 10      | 537   | 2     | 1.33   |
| WDC       | WD1600AAJS-00L7A0  | 160 GB | 28      | 744   | 4     | 1.32   |
| WDC       | WD1200JB-00GVA0    | 120 GB | 4       | 754   | 1     | 1.32   |
| Seagate   | ST340015A          | 40 GB  | 5       | 835   | 33    | 1.32   |
| WDC       | WD7500AZEX-00ZF5A0 | 752 GB | 6       | 481   | 0     | 1.32   |
| Apple     | HDD HTS545050A7... | 500 GB | 15      | 500   | 2     | 1.32   |
| WDC       | WD5000BPKX-80HPJT0 | 500 GB | 1       | 480   | 0     | 1.32   |
| Seagate   | ST3000VX010-2E3166 | 3 TB   | 5       | 492   | 1     | 1.32   |
| WDC       | WD2500AAKS-00UU3A0 | 250 GB | 5       | 543   | 2     | 1.32   |
| Seagate   | ST3160815A         | 160 GB | 37      | 746   | 235   | 1.32   |
| Maxtor    | 6V160E0            | 160 GB | 8       | 509   | 1     | 1.31   |
| WDC       | WD20EZRX-22D8PB0   | 2 TB   | 6       | 479   | 0     | 1.31   |
| WDC       | WD7502AAEX-00Y9A0  | 752 GB | 5       | 478   | 0     | 1.31   |
| Seagate   | ST2000NM0033-9Z... | 2 TB   | 7       | 478   | 0     | 1.31   |
| Seagate   | ST3160812A         | 160 GB | 27      | 737   | 385   | 1.31   |
| Hitachi   | HUA722050CLA330    | 500 GB | 2       | 476   | 0     | 1.31   |
| Toshiba   | DT01ACA300         | 3 TB   | 69      | 509   | 30    | 1.30   |
| Seagate   | ST9120821A         | 120 GB | 4       | 719   | 19    | 1.30   |
| WDC       | WD5000AUDX-63WNHY0 | 500 GB | 3       | 475   | 0     | 1.30   |
| WDC       | WD10EZEX-21M2NA0   | 1 TB   | 31      | 514   | 1     | 1.30   |
| WDC       | WD1600JS-56MHB1    | 160 GB | 6       | 572   | 5     | 1.30   |
| WDC       | WD1600BEVS-22RST0  | 160 GB | 41      | 582   | 90    | 1.30   |
| Apple     | HDD HTS541010A9... | 1 TB   | 15      | 498   | 135   | 1.30   |
| WDC       | WD3200AAJB-56R1A0  | 320 GB | 1       | 473   | 0     | 1.30   |
| Toshiba   | MK1032GSX          | 100 GB | 5       | 497   | 1     | 1.29   |
| Toshiba   | MK1016GAP          | 10 GB  | 1       | 472   | 0     | 1.29   |
| WDC       | WD10EACS-65D6B0    | 1 TB   | 1       | 471   | 0     | 1.29   |
| WDC       | WD5000AAKS-75A7B2  | 500 GB | 3       | 1036  | 6     | 1.29   |
| Apple     | HDD HTS541010A9... | 1 TB   | 3       | 470   | 0     | 1.29   |
| Seagate   | ST320014A          | 20 GB  | 7       | 889   | 12    | 1.29   |
| Seagate   | ST10000NE0004-1... | 10 TB  | 9       | 830   | 13    | 1.29   |
| WDC       | WD1001FALS-40K1B0  | 1 TB   | 3       | 918   | 4     | 1.29   |
| Seagate   | ST3500320NS        | 500 GB | 16      | 907   | 362   | 1.29   |
| WDC       | WD5000BEKT-75KA9T0 | 500 GB | 3       | 469   | 0     | 1.29   |
| HGST      | HUH721010ALE600    | 10 TB  | 11      | 502   | 1     | 1.29   |
| WDC       | WD60EZRZ-11RWYB1   | 6 TB   | 1       | 468   | 0     | 1.28   |
| Toshiba   | MQ03ABB200         | 2 TB   | 1       | 468   | 0     | 1.28   |
| Seagate   | ST250LT020-1AE14C  | 250 GB | 2       | 592   | 470   | 1.28   |
| Maxtor    | STM380215AS        | 80 GB  | 12      | 679   | 489   | 1.28   |
| Seagate   | ST380215AS         | 80 GB  | 26      | 771   | 535   | 1.28   |
| WDC       | WD3200AVJS-63N9A0  | 320 GB | 3       | 467   | 0     | 1.28   |
| Seagate   | ST32000646NS       | 2 TB   | 1       | 467   | 0     | 1.28   |
| Seagate   | ST1000NM0033-9Z... | 1 TB   | 28      | 593   | 74    | 1.28   |
| Samsung   | SV0221N            | 20 GB  | 1       | 2328  | 4     | 1.28   |
| WDC       | WD10EVDS-63U8B1    | 1 TB   | 1       | 464   | 0     | 1.27   |
| Hitachi   | HDT721064SLA380    | 640 GB | 1       | 464   | 0     | 1.27   |
| WDC       | WD800AAJS-00B4A0   | 80 GB  | 5       | 543   | 3     | 1.27   |
| WDC       | WD1600BEKT-66F3T2  | 160 GB | 1       | 463   | 0     | 1.27   |
| WDC       | WD5000AAKX-07U6AA1 | 500 GB | 2       | 463   | 0     | 1.27   |
| Seagate   | ST380013AS         | 80 GB  | 37      | 1215  | 76    | 1.26   |
| Seagate   | ST320410A          | 20 GB  | 6       | 853   | 9     | 1.26   |
| WDC       | WD1001FAES-22W7A0  | 1 TB   | 1       | 460   | 0     | 1.26   |
| WDC       | WD1600AAJS-00V4A0  | 160 GB | 6       | 463   | 13    | 1.26   |
| Toshiba   | DT01ACA200         | 2 TB   | 134     | 504   | 48    | 1.26   |
| Seagate   | ST2000VM003-1CT164 | 2 TB   | 6       | 745   | 720   | 1.26   |
| WDC       | WD2500AAKS-00F0A0  | 250 GB | 6       | 822   | 48    | 1.26   |
| Seagate   | ST3500411SV        | 500 GB | 3       | 646   | 25    | 1.26   |
| WDC       | WD2500JS-22MHB0    | 250 GB | 4       | 580   | 70    | 1.26   |
| Seagate   | ST3250620A         | 250 GB | 15      | 687   | 42    | 1.25   |
| WDC       | WD1600AAJS-00B4A0  | 160 GB | 20      | 695   | 70    | 1.25   |
| Toshiba   | MG04ACA100NY       | 1 TB   | 10      | 456   | 0     | 1.25   |
| Seagate   | ST2000DX001-1CM164 | 2 TB   | 20      | 519   | 181   | 1.25   |
| WDC       | WD6400AAKS-22A7B2  | 640 GB | 18      | 771   | 2     | 1.25   |
| WDC       | WD10EZRX-00L4HB0   | 1 TB   | 50      | 488   | 4     | 1.25   |
| WDC       | WD2500AABS-00SDA0  | 250 GB | 1       | 455   | 0     | 1.25   |
| Hitachi   | HTS723232L9A362    | 320 GB | 2       | 959   | 4     | 1.24   |
| Hitachi   | HTS541610J9SA00    | 100 GB | 2       | 453   | 0     | 1.24   |
| WDC       | WD5000AZLX-00CL5A0 | 500 GB | 5       | 508   | 2     | 1.24   |
| Hitachi   | HDS721050CLA660    | 500 GB | 18      | 568   | 62    | 1.24   |
| WDC       | WD10EZEX-08M2NA0   | 1 TB   | 72      | 489   | 5     | 1.24   |
| WDC       | WD10EZEX-00BN5A0   | 1 TB   | 150     | 517   | 3     | 1.24   |
| Seagate   | ST4000NM0033-9Z... | 4 TB   | 6       | 495   | 290   | 1.24   |
| WDC       | WD6400BPVT-80HXZT3 | 640 GB | 8       | 690   | 9     | 1.24   |
| Samsung   | HD153WI            | 1.5 TB | 1       | 451   | 0     | 1.24   |
| WDC       | WD3200BEVS-08VAT2  | 320 GB | 3       | 712   | 373   | 1.24   |
| WDC       | WD5000BEVT-75A0RT0 | 500 GB | 8       | 610   | 52    | 1.24   |
| Hitachi   | HDS5C1050CLA382    | 500 GB | 11      | 664   | 124   | 1.23   |
| Seagate   | ST1000VM002-1SD102 | 1 TB   | 3       | 449   | 0     | 1.23   |
| Hitachi   | HDS728080PLA380... | 80 GB  | 1       | 449   | 0     | 1.23   |
| WDC       | WD5000AAKX-75U6AA0 | 500 GB | 19      | 693   | 2     | 1.23   |
| WDC       | WD5000BEKT-00KA9T0 | 500 GB | 2       | 1084  | 7     | 1.23   |
| WDC       | WD2500AAJS-00V4A0  | 250 GB | 6       | 742   | 1     | 1.23   |
| ExcelStor | J360               | 64 GB  | 1       | 897   | 1     | 1.23   |
| WDC       | WD60EFRX-68L0BN1   | 6 TB   | 22      | 579   | 3     | 1.23   |
| Toshiba   | MK1234GAX          | 120 GB | 2       | 448   | 0     | 1.23   |
| Samsung   | HD252HJ            | 250 GB | 26      | 817   | 141   | 1.23   |
| Samsung   | HD501LJ            | 500 GB | 59      | 1053  | 434   | 1.23   |
| Hitachi   | HTS541064A9E680    | 640 GB | 3       | 447   | 0     | 1.23   |
| WDC       | WD1000CHTZ-04JCPV0 | 1 TB   | 1       | 447   | 0     | 1.23   |
| WDC       | WD15EARX-00ZUDB0   | 1.5 TB | 2       | 776   | 3     | 1.22   |
| WDC       | WD3200YS-01PGB0    | 320 GB | 1       | 446   | 0     | 1.22   |
| Seagate   | ST3200820A         | 200 GB | 5       | 491   | 61    | 1.22   |
| Seagate   | ST3250624AS        | 250 GB | 14      | 942   | 101   | 1.22   |
| WDC       | WD1600AAJS-00Z4A0  | 160 GB | 1       | 445   | 0     | 1.22   |
| Seagate   | ST1000VX000-1CU162 | 1 TB   | 25      | 458   | 41    | 1.22   |
| WDC       | WD60EFRX-68MYMN1   | 6 TB   | 10      | 789   | 70    | 1.22   |
| WDC       | WD3200AAKS-61L9A0  | 320 GB | 6       | 447   | 5     | 1.22   |
| WDC       | WD30EZRS-00J99B0   | 3 TB   | 7       | 1300  | 838   | 1.22   |
| WDC       | WD740GD-00FLA2     | 74 GB  | 1       | 1330  | 2     | 1.22   |
| WDC       | WD1600BEKT-75A25T0 | 160 GB | 1       | 442   | 0     | 1.21   |
| WDC       | WD5000AAKS-65V0A0  | 500 GB | 3       | 907   | 6     | 1.21   |
| WDC       | WD30EZRZ-00GXCB0   | 3 TB   | 3       | 441   | 0     | 1.21   |
| Hitachi   | HDS721025CLA382    | 250 GB | 21      | 711   | 200   | 1.21   |
| Fujitsu   | MHZ2250BH G1       | 250 GB | 5       | 475   | 7     | 1.20   |
| Toshiba   | MG03ACA400         | 4 TB   | 2       | 438   | 0     | 1.20   |
| WDC       | WD10EZEX-60M2NA0   | 1 TB   | 18      | 585   | 91    | 1.20   |
| Seagate   | ST12000NE0007-2... | 12 TB  | 2       | 436   | 0     | 1.20   |
| WDC       | WD7500BPKT-60PK4T0 | 752 GB | 3       | 544   | 3     | 1.19   |
| Seagate   | ST380817AS         | 80 GB  | 48      | 718   | 9     | 1.19   |
| WDC       | WD5000AAJS-22A8B0  | 500 GB | 1       | 3915  | 8     | 1.19   |
| WDC       | WD2500BEVS-22UST0  | 250 GB | 49      | 537   | 13    | 1.19   |
| Fujitsu   | MHV2080AT PL       | 80 GB  | 3       | 434   | 0     | 1.19   |
| Seagate   | ST2000DM006-2DM164 | 2 TB   | 106     | 440   | 1     | 1.19   |
| WDC       | WD5003AZEX-00K1GA0 | 500 GB | 23      | 476   | 47    | 1.19   |
| WDC       | WD6400AAKS-00H2B0  | 640 GB | 1       | 432   | 0     | 1.19   |
| WDC       | WD5000AAKX-001CA0  | 500 GB | 185     | 731   | 45    | 1.19   |
| WDC       | WD1200BEVS-22RST0  | 120 GB | 3       | 458   | 1     | 1.18   |
| WDC       | WD800JD-55MUA1     | 80 GB  | 9       | 615   | 8     | 1.18   |
| WDC       | WD10EZEX-22RKKA0   | 1 TB   | 8       | 555   | 4     | 1.18   |
| WDC       | WD6402AAEX-00Y9A0  | 640 GB | 5       | 578   | 8     | 1.18   |
| Seagate   | ST3120022A         | 120 GB | 36      | 645   | 20    | 1.18   |
| Hitachi   | HTS543216A7A384    | 160 GB | 2       | 430   | 0     | 1.18   |
| Hitachi   | HDS721032CLA362    | 320 GB | 43      | 747   | 25    | 1.18   |
| Hitachi   | HTE545025B9A300    | 250 GB | 1       | 430   | 0     | 1.18   |
| WDC       | WD10EFRX-68JCSN0   | 1 TB   | 14      | 761   | 282   | 1.18   |
| Toshiba   | MG04ACA400E        | 4 TB   | 6       | 428   | 0     | 1.17   |
| WDC       | WD10EARS-00MVWB0   | 1 TB   | 37      | 993   | 58    | 1.17   |
| WDC       | WD10EARS-00Y5B1    | 1 TB   | 109     | 903   | 98    | 1.17   |
| WDC       | WD5001AALS-00LWTA0 | 500 GB | 7       | 1053  | 43    | 1.17   |
| Seagate   | ST500VT000-1DK142  | 500 GB | 14      | 426   | 0     | 1.17   |
| Hitachi   | HDS721010CLA330    | 1 TB   | 38      | 716   | 33    | 1.17   |
| WDC       | WD10S21X-24R1BT... | 1 TB   | 8       | 426   | 0     | 1.17   |
| WDC       | WD2500AAKX-001CA0  | 250 GB | 31      | 554   | 94    | 1.17   |
| WDC       | WD1200LB-55EDA0    | 120 GB | 1       | 425   | 0     | 1.17   |
| Seagate   | ST3200827AS        | 200 GB | 27      | 788   | 295   | 1.17   |
| WDC       | WD5000LUCT-63Y8HY0 | 500 GB | 1       | 424   | 0     | 1.16   |
| Seagate   | ST1000NM0053-1C... | 1 TB   | 2       | 424   | 0     | 1.16   |
| WDC       | WD5000LMVW-11VEDS0 | 500 GB | 1       | 424   | 0     | 1.16   |
| Fujitsu   | MHV2100AT PL       | 100 GB | 1       | 424   | 0     | 1.16   |
| WDC       | WD1600AAJS-60M0A0  | 160 GB | 4       | 494   | 24    | 1.16   |
| WDC       | WD1001FALS-00E8B0  | 1 TB   | 12      | 976   | 187   | 1.16   |
| WDC       | WD20EURS-63S48Y0   | 2 TB   | 5       | 897   | 408   | 1.16   |
| WDC       | WD2500JS-00SGB0    | 250 GB | 5       | 570   | 1     | 1.16   |
| Maxtor    | 7H500F0            | 500 GB | 2       | 601   | 2     | 1.16   |
| Maxtor    | STM3160815AS       | 160 GB | 29      | 715   | 325   | 1.16   |
| Samsung   | HD753LJ            | 752 GB | 29      | 916   | 234   | 1.16   |
| WDC       | WD5000AAJS-22YFA0  | 500 GB | 6       | 781   | 352   | 1.15   |
| Hitachi   | HDT722525DLA380    | 250 GB | 13      | 1130  | 55    | 1.15   |
| Hitachi   | HDP725025GLA380    | 250 GB | 36      | 801   | 75    | 1.15   |
| Hitachi   | HTS725016A9A364    | 160 GB | 9       | 483   | 340   | 1.15   |
| Maxtor    | 6V080E0            | 82 GB  | 10      | 749   | 5     | 1.15   |
| WDC       | WD7500BPVT-75A1YT0 | 752 GB | 1       | 419   | 0     | 1.15   |
| WDC       | WD5003ABYX-01WERA0 | 500 GB | 10      | 787   | 4     | 1.15   |
| Toshiba   | MQ01ACF032         | 320 GB | 11      | 470   | 1     | 1.15   |
| Seagate   | ST2000LM003 HN-... | 2 TB   | 40      | 480   | 5     | 1.15   |
| Seagate   | ST1000DM003-1CH162 | 1 TB   | 303     | 542   | 51    | 1.15   |
| WDC       | WD3000FYYZ-05UL1B0 | 3 TB   | 1       | 418   | 0     | 1.15   |
| WDC       | WD5003ABYX-01WERA1 | 500 GB | 9       | 757   | 3     | 1.15   |
| Samsung   | HM501II            | 500 GB | 5       | 672   | 3     | 1.14   |
| Seagate   | ST3500312CS        | 500 GB | 35      | 776   | 182   | 1.14   |
| WDC       | WD6003FZBX-00K5WB0 | 6 TB   | 4       | 417   | 0     | 1.14   |
| WDC       | WD5000AAKS-65A7B0  | 500 GB | 5       | 595   | 81    | 1.14   |
| Maxtor    | STM3500630AS       | 500 GB | 1       | 416   | 0     | 1.14   |
| WDC       | WD10JPVT-24A1YT0   | 1 TB   | 4       | 489   | 1     | 1.14   |
| WDC       | WD5000BPVT-80HXZT3 | 500 GB | 21      | 469   | 53    | 1.14   |
| Seagate   | ST750LX003-1AC154  | 752 GB | 14      | 458   | 76    | 1.14   |
| WDC       | WD15EARS-00MVWB0   | 1.5 TB | 36      | 861   | 362   | 1.14   |
| WDC       | WD1600JS-08MHB0    | 160 GB | 1       | 414   | 0     | 1.14   |
| WDC       | WD30EZRZ-00WN9B0   | 3 TB   | 5       | 414   | 0     | 1.14   |
| WDC       | WD6400BPVT-60HXZT1 | 640 GB | 3       | 554   | 28    | 1.13   |
| Seagate   | ST3160215A         | 160 GB | 20      | 708   | 155   | 1.13   |
| Seagate   | ST9750422AS        | 752 GB | 3       | 846   | 207   | 1.13   |
| Seagate   | ST94813AS          | 40 GB  | 2       | 412   | 0     | 1.13   |
| Maxtor    | STM380211AS        | 80 GB  | 6       | 636   | 919   | 1.13   |
| Toshiba   | MK2575GSX          | 250 GB | 1       | 412   | 0     | 1.13   |
| Seagate   | ST380811AS         | 80 GB  | 63      | 657   | 481   | 1.13   |
| WDC       | WD5000BMVW-11AJGS1 | 500 GB | 1       | 411   | 0     | 1.13   |
| WDC       | WD5000BPKX-00HPJT0 | 500 GB | 2       | 411   | 0     | 1.13   |
| WDC       | WD5000AAVS-22G9B1  | 500 GB | 2       | 1446  | 6     | 1.13   |
| Seagate   | ST3500418AS        | 500 GB | 370     | 762   | 182   | 1.13   |
| Maxtor    | 6V320F0            | 320 GB | 1       | 410   | 0     | 1.13   |
| WDC       | WD1600BEVS-26VAT0  | 160 GB | 3       | 409   | 0     | 1.12   |
| WDC       | WD10JPVT-08A1YT1   | 1 TB   | 2       | 408   | 0     | 1.12   |
| Seagate   | ST3000DM001-1CH166 | 3 TB   | 41      | 486   | 204   | 1.12   |
| Seagate   | ST380819AS         | 80 GB  | 3       | 781   | 682   | 1.12   |
| Seagate   | ST500DM002-1BC142  | 500 GB | 55      | 592   | 119   | 1.12   |
| Maxtor    | STM3250820A        | 250 GB | 6       | 591   | 218   | 1.12   |
| WDC       | WD800EB-11DJF0     | 80 GB  | 1       | 407   | 0     | 1.12   |
| WDC       | WD2000JB-00KFA0    | 200 GB | 1       | 1220  | 2     | 1.11   |
| WDC       | WD2500JD-00HBB0    | 250 GB | 1       | 406   | 0     | 1.11   |
| Hitachi   | HTS721080G9AT00    | 80 GB  | 1       | 405   | 0     | 1.11   |
| WDC       | WD1200BEVS-22UST0  | 120 GB | 26      | 504   | 63    | 1.11   |
| Seagate   | ST3000VX000-9YW166 | 3 TB   | 1       | 405   | 0     | 1.11   |
| WDC       | WD5000AZRX-00L4HB0 | 500 GB | 20      | 404   | 0     | 1.11   |
| WDC       | WD2500AAKS-00V6A0  | 250 GB | 1       | 404   | 0     | 1.11   |
| WDC       | WD10EARS-00Z5B1    | 1 TB   | 9       | 946   | 123   | 1.11   |
| Seagate   | ST2000VX000-1CU164 | 2 TB   | 13      | 579   | 312   | 1.11   |
| Samsung   | HE161HJ            | 160 GB | 1       | 1213  | 2     | 1.11   |
| HGST      | HUS724040ALE640    | 4 TB   | 7       | 404   | 0     | 1.11   |
| WDC       | WD10JMVW-11AJGS1   | 1 TB   | 5       | 572   | 1     | 1.11   |
| Seagate   | ST3250310AS        | 250 GB | 149     | 865   | 214   | 1.10   |
| Seagate   | ST3250624A         | 250 GB | 1       | 1205  | 2     | 1.10   |
| HGST      | HUS726040ALE611    | 4 TB   | 1       | 401   | 0     | 1.10   |
| WDC       | WD5000AVKX-635FY0  | 500 GB | 1       | 401   | 0     | 1.10   |
| WDC       | WD5003ABYX-23 8... | 500 GB | 2       | 668   | 2     | 1.10   |
| WDC       | WD1600BEVS-07RST0  | 160 GB | 9       | 450   | 1     | 1.10   |
| Fujitsu   | MHW2080BH PL       | 80 GB  | 6       | 603   | 172   | 1.10   |
| Fujitsu   | MJA2160BH FFS G1   | 160 GB | 2       | 400   | 0     | 1.10   |
| WDC       | WD2500AAKS-00VYA0  | 250 GB | 4       | 468   | 1     | 1.10   |
| WDC       | WD3200AAKS-00SBA0  | 320 GB | 11      | 692   | 22    | 1.10   |
| Seagate   | ST8000NE0021-2E... | 8 TB   | 1       | 399   | 0     | 1.10   |
| WDC       | WD10EADS-11P8B2    | 1 TB   | 1       | 799   | 1     | 1.10   |
| HGST      | HUH721010ALN600    | 10 TB  | 1       | 399   | 0     | 1.09   |
| WDC       | WD10JPVT-00A1YT0   | 1 TB   | 2       | 399   | 0     | 1.09   |
| WDC       | WD10EZEX-19ZF5A0   | 1 TB   | 1       | 399   | 0     | 1.09   |
| WDC       | WD1600AAJS-00WAA0  | 160 GB | 9       | 538   | 4     | 1.09   |
| WDC       | WD5000BPKT-22PK4T0 | 500 GB | 2       | 398   | 0     | 1.09   |
| WDC       | WD2500BEVS-08VAT2  | 250 GB | 2       | 398   | 0     | 1.09   |
| WDC       | WD6400BEVT-80A0RT0 | 640 GB | 2       | 398   | 0     | 1.09   |
| Seagate   | ST3160212A         | 160 GB | 14      | 666   | 64    | 1.09   |
| Seagate   | ST1000DM003-9YN162 | 1 TB   | 132     | 674   | 264   | 1.09   |
| WDC       | WD2500JS-57MHB1    | 250 GB | 1       | 397   | 0     | 1.09   |
| Fujitsu   | MJA2250BH FFS G1   | 250 GB | 3       | 397   | 0     | 1.09   |
| WDC       | WD3200AAKS-00L6A0  | 320 GB | 3       | 579   | 4     | 1.09   |
| Seagate   | ST1000VN002-2EY102 | 1 TB   | 3       | 396   | 0     | 1.08   |
| WDC       | WD10JPVX-08JC3T2   | 1 TB   | 6       | 409   | 1     | 1.08   |
| WDC       | WD5000AAKX-753CA1  | 500 GB | 6       | 1067  | 13    | 1.08   |
| WDC       | WD1600AABS-00H4A0  | 160 GB | 2       | 432   | 6     | 1.08   |
| WDC       | WD7500BPVT-80HXZT3 | 752 GB | 13      | 446   | 2     | 1.08   |
| WDC       | WD2001FASS-00U0B0  | 2 TB   | 1       | 1578  | 3     | 1.08   |
| Seagate   | ST6000VN0033-2E... | 6 TB   | 7       | 393   | 0     | 1.08   |
| WDC       | WD2500BEVT-22ZCT0  | 250 GB | 36      | 506   | 82    | 1.08   |
| Seagate   | ST9200420ASG       | 200 GB | 2       | 393   | 0     | 1.08   |
| Samsung   | HD403LJ            | 400 GB | 18      | 1167  | 458   | 1.08   |
| Seagate   | ST320LM000 HM321HI | 320 GB | 12      | 409   | 2     | 1.08   |
| HGST      | HUS722T1TALA600    | 1 TB   | 2       | 393   | 0     | 1.08   |
| Seagate   | ST1000NM0011       | 1 TB   | 13      | 1372  | 34    | 1.07   |
| WDC       | WD1003FBYX-01Y7B1  | 1 TB   | 26      | 639   | 3     | 1.07   |
| Seagate   | ST3250318AS        | 250 GB | 113     | 730   | 116   | 1.07   |
| WDC       | WD2500LPVX-22V0TT0 | 250 GB | 1       | 391   | 0     | 1.07   |
| Samsung   | HM251HI            | 250 GB | 5       | 491   | 2     | 1.07   |
| WDC       | WD2500AAJB-00J3A0  | 250 GB | 10      | 741   | 8     | 1.07   |
| Seagate   | ST3120827AS        | 120 GB | 45      | 729   | 10    | 1.07   |
| Seagate   | ST320DM000-1BC14C  | 320 GB | 15      | 511   | 15    | 1.07   |
| Fujitsu   | MHV2040AH          | 40 GB  | 4       | 749   | 5     | 1.07   |
| Hitachi   | HTS723216A7A364    | 160 GB | 1       | 389   | 0     | 1.07   |
| Toshiba   | MK1234GSX          | 120 GB | 9       | 665   | 4     | 1.07   |
| Fujitsu   | MHV2080BH          | 80 GB  | 4       | 476   | 2     | 1.07   |
| WDC       | WD5000BPKT-75PK4T0 | 500 GB | 12      | 595   | 3     | 1.06   |
| WDC       | WD5000BPKT-60PK4T0 | 500 GB | 5       | 616   | 53    | 1.06   |
| WDC       | WD2500AAKX-603CA0  | 250 GB | 5       | 389   | 241   | 1.06   |
| WDC       | WD3200BEVT-22ZCT0  | 320 GB | 85      | 474   | 90    | 1.06   |
| WDC       | WD5000AAKS-00WWPA0 | 500 GB | 9       | 629   | 10    | 1.06   |
| Hitachi   | HDS721680PLAT80    | 80 GB  | 5       | 866   | 4     | 1.06   |
| WDC       | WD3200AAJS-22L7A0  | 320 GB | 9       | 776   | 27    | 1.06   |
| Seagate   | ST3160827AS        | 160 GB | 23      | 1005  | 230   | 1.06   |
| WDC       | WD5000AAKX-08ANVA0 | 500 GB | 2       | 386   | 0     | 1.06   |
| WDC       | WD5000LPVT-22G33T0 | 500 GB | 22      | 487   | 62    | 1.06   |
| WDC       | WD5000AADS-00S9B0  | 500 GB | 108     | 734   | 34    | 1.05   |
| Seagate   | ST3250820ACE       | 250 GB | 3       | 520   | 698   | 1.05   |
| WDC       | WD5000BEVT-00A03T0 | 500 GB | 3       | 384   | 0     | 1.05   |
| WDC       | WD2000FYYZ-05UL1B0 | 2 TB   | 1       | 383   | 0     | 1.05   |
| Seagate   | ST10000NM0156-2... | 10 TB  | 14      | 383   | 0     | 1.05   |
| HP        | VB0250EAVER        | 250 GB | 9       | 793   | 6     | 1.05   |
| WDC       | WD800JD-22JNA0     | 80 GB  | 1       | 383   | 0     | 1.05   |
| WDC       | WD1600JS-08NCB1    | 160 GB | 5       | 565   | 27    | 1.05   |
| Seagate   | ST3160215AS        | 160 GB | 17      | 612   | 505   | 1.05   |
| WDC       | WD800BB-75JHC0     | 80 GB  | 2       | 382   | 0     | 1.05   |
| Fujitsu   | MHZ2160BH G2       | 160 GB | 29      | 542   | 333   | 1.05   |
| Toshiba   | MK2559GSXP         | 250 GB | 4       | 450   | 7     | 1.05   |
| WDC       | WD3000HLHX-01JJPV0 | 304 GB | 2       | 455   | 2     | 1.05   |
| WDC       | WD7500BPVT-24HXZT1 | 752 GB | 10      | 662   | 105   | 1.05   |
| Seagate   | ST1500DM003-1CH16G | 1.5 TB | 7       | 416   | 2     | 1.05   |
| Seagate   | ST31000525SV       | 1 TB   | 3       | 769   | 20    | 1.05   |
| WDC       | WD2000JD-22HBB0    | 200 GB | 3       | 993   | 7     | 1.04   |
| Seagate   | ST31000524AS       | 1 TB   | 191     | 660   | 199   | 1.04   |
| WDC       | WD4000FYYZ-01UL1B1 | 4 TB   | 3       | 381   | 0     | 1.04   |
| WDC       | WD40EZRZ-22GXCB0   | 4 TB   | 6       | 380   | 0     | 1.04   |
| Seagate   | ST3500514NS        | 500 GB | 7       | 1229  | 128   | 1.04   |
| WDC       | WD20EARX-55PASB0   | 2 TB   | 3       | 380   | 0     | 1.04   |
| WDC       | WD5000LPLX-60ZNTT2 | 500 GB | 1       | 380   | 0     | 1.04   |
| WDC       | WD40E31X-00HY4A0   | 4 TB   | 1       | 380   | 0     | 1.04   |
| WDC       | WD2500BEVS-60UST0  | 250 GB | 9       | 572   | 225   | 1.04   |
| Seagate   | ST2000NC001-1DY164 | 2 TB   | 5       | 378   | 0     | 1.04   |
| Samsung   | HD502HI            | 500 GB | 31      | 673   | 217   | 1.03   |
| WDC       | WD2000JS-00SGB0    | 200 GB | 1       | 377   | 0     | 1.03   |
| WDC       | WD800AAJS-22WAA0   | 80 GB  | 2       | 376   | 0     | 1.03   |
| Samsung   | HD322HJ            | 320 GB | 52      | 750   | 216   | 1.03   |
| Samsung   | HD503HI            | 500 GB | 17      | 583   | 15    | 1.03   |
| WDC       | WD5000AAKX-221CA1  | 500 GB | 13      | 667   | 22    | 1.03   |
| Seagate   | ST3000DM008-2DM166 | 3 TB   | 30      | 404   | 24    | 1.03   |
| WDC       | WD10JMVW-11AJGS2   | 1 TB   | 12      | 477   | 2     | 1.03   |
| WDC       | WD3200BEVT-11ZCT0  | 320 GB | 4       | 378   | 1     | 1.03   |
| WDC       | WD800BB-00JKA0     | 80 GB  | 1       | 374   | 0     | 1.03   |
| WDC       | WD7500BPKT-80PK4T0 | 752 GB | 5       | 781   | 5     | 1.03   |
| Seagate   | ST500DM005 HD502HJ | 500 GB | 38      | 472   | 10    | 1.02   |
| WDC       | WD5000BEVT-00ZAT0  | 500 GB | 5       | 454   | 232   | 1.02   |
| WDC       | WD800BB-00JHC0     | 80 GB  | 23      | 601   | 78    | 1.02   |
| WDC       | WD7500BPKT-22PK4T0 | 752 GB | 9       | 372   | 0     | 1.02   |
| Seagate   | ST9402112A         | 40 GB  | 1       | 1117  | 2     | 1.02   |
| Seagate   | ST1000LM044 HN-... | 1 TB   | 2       | 559   | 404   | 1.02   |
| WDC       | WD1600JS-22NCB1    | 160 GB | 4       | 712   | 6     | 1.02   |
| Hitachi   | HDT721064SLA360    | 640 GB | 4       | 1035  | 6     | 1.02   |
| WDC       | WD2500AAKX-00U6AA0 | 250 GB | 3       | 373   | 3     | 1.01   |
| WDC       | WD30EZRZ-00Z5HB0   | 3 TB   | 22      | 501   | 6     | 1.01   |
| WDC       | WD5000AAKX-00ERMA0 | 500 GB | 106     | 527   | 5     | 1.01   |
| WDC       | WD20EZRZ-22Z5HB0   | 2 TB   | 8       | 369   | 0     | 1.01   |
| WDC       | WD3200AAJS-60Z0A0  | 320 GB | 6       | 722   | 42    | 1.01   |
| WDC       | WD20NMVW-11EDZS6   | 2 TB   | 8       | 368   | 0     | 1.01   |
| Seagate   | ST3802110A         | 80 GB  | 36      | 630   | 513   | 1.01   |
| Toshiba   | MQ03UBB200         | 2 TB   | 6       | 367   | 0     | 1.01   |
| WDC       | WD800BB-22JHC0     | 80 GB  | 10      | 511   | 38    | 1.01   |
| WDC       | WD800BB-00FJA0     | 80 GB  | 6       | 443   | 35    | 1.00   |
| Toshiba   | MQ01UBD100         | 1 TB   | 22      | 518   | 198   | 1.00   |
| HGST      | HUH728080ALE600    | 8 TB   | 3       | 364   | 0     | 1.00   |
| Hitachi   | HDS721050CLA360    | 500 GB | 67      | 522   | 36    | 1.00   |
| Hitachi   | HDS721064CLA332    | 640 GB | 1       | 364   | 0     | 1.00   |
| WDC       | WD5000AAKS-00UU3A0 | 500 GB | 56      | 739   | 67    | 1.00   |
| WDC       | WD5000AAKS-41YGA1  | 500 GB | 1       | 728   | 1     | 1.00   |
| Seagate   | ST9320328CS        | 320 GB | 9       | 581   | 193   | 1.00   |
| WDC       | WD2500BEVT-35A23T0 | 250 GB | 25      | 507   | 26    | 1.00   |
| Samsung   | SP1654N            | 160 GB | 8       | 849   | 412   | 0.99   |
| HGST      | HTS721075A9E630    | 752 GB | 9       | 382   | 135   | 0.99   |
| Seagate   | ST9640423AS        | 640 GB | 4       | 949   | 380   | 0.99   |
| WDC       | WD10EZEX-60ZF5A0   | 1 TB   | 46      | 510   | 84    | 0.99   |
| WDC       | WD800JB-00JJC0     | 80 GB  | 21      | 618   | 26    | 0.99   |
| WDC       | WD10SPCX-08S8TT0   | 1 TB   | 4       | 360   | 0     | 0.99   |
| WDC       | WD2500AAKX-07U6AA0 | 250 GB | 2       | 360   | 0     | 0.99   |
| Seagate   | ST3160023AS        | 160 GB | 15      | 983   | 34    | 0.99   |
| WDC       | WD3200AAKB-00WHA0  | 320 GB | 1       | 360   | 0     | 0.99   |
| WDC       | WD740GD-00FLA0     | 74 GB  | 1       | 2521  | 6     | 0.99   |
| Maxtor    | STM3160212A        | 160 GB | 2       | 817   | 1     | 0.99   |
| WDC       | WD10EADS-65M2B1    | 1 TB   | 4       | 978   | 238   | 0.99   |
| WDC       | WD3200AAJS-00B4A0  | 320 GB | 19      | 844   | 119   | 0.99   |
| Seagate   | ST3120814A         | 120 GB | 16      | 760   | 363   | 0.98   |
| WDC       | WD20EURS-73TLHY0   | 2 TB   | 1       | 1437  | 3     | 0.98   |
| WDC       | WD4004FZWX-00GBGB0 | 4 TB   | 5       | 611   | 477   | 0.98   |
| Seagate   | ST3160211AS        | 160 GB | 9       | 758   | 977   | 0.98   |
| WDC       | WD3200AAKX-00ERMA0 | 320 GB | 12      | 538   | 3     | 0.98   |
| WDC       | WD3200AVVS-56L2B0  | 320 GB | 10      | 524   | 57    | 0.98   |
| Seagate   | ST3250310NS        | 250 GB | 3       | 737   | 755   | 0.98   |
| Fujitsu   | MHW2120BJ G2       | 120 GB | 1       | 356   | 0     | 0.98   |
| WDC       | WD5000AAKX-07U6AA0 | 500 GB | 6       | 518   | 3     | 0.98   |
| Fujitsu   | MHW2060BH          | 64 GB  | 4       | 743   | 4     | 0.97   |
| Hitachi   | HDS721680PLA380    | 80 GB  | 45      | 788   | 185   | 0.97   |
| WDC       | WD15EVDS-63V9B1    | 1.5 TB | 2       | 1117  | 6     | 0.97   |
| Toshiba   | MK8032GSX          | 80 GB  | 8       | 467   | 161   | 0.97   |
| WDC       | WD800JB-00JJA0     | 80 GB  | 3       | 1595  | 11    | 0.97   |
| Samsung   | HD203WI            | 2 TB   | 2       | 354   | 0     | 0.97   |
| WDC       | WD3200AAJS-00M0A0  | 320 GB | 2       | 574   | 1     | 0.97   |
| Toshiba   | MK3261GSYG         | 320 GB | 1       | 354   | 0     | 0.97   |
| WDC       | WD3001FAEX-00MJRA0 | 3 TB   | 4       | 1352  | 3     | 0.97   |
| Seagate   | ST5000LM000-2AN170 | 5 TB   | 14      | 354   | 0     | 0.97   |
| WDC       | WD4000F9YZ-09N20L0 | 4 TB   | 1       | 353   | 0     | 0.97   |
| Hitachi   | HCP725032GLA380    | 320 GB | 2       | 1010  | 2     | 0.97   |
| WDC       | WD5000AAKS-75V0A0  | 500 GB | 9       | 1073  | 4     | 0.97   |
| WDC       | WD6400AACS-00M3B0  | 640 GB | 1       | 352   | 0     | 0.97   |
| Seagate   | ST980813ASG        | 80 GB  | 3       | 509   | 4     | 0.96   |
| Seagate   | ST3320820AS        | 320 GB | 17      | 514   | 343   | 0.96   |
| WDC       | WD10JPVT-60A1YT0   | 1 TB   | 2       | 455   | 505   | 0.96   |
| WDC       | WD3200BPVT-75JJ5T0 | 320 GB | 4       | 407   | 2     | 0.96   |
| Seagate   | ST3160813AS        | 160 GB | 38      | 875   | 139   | 0.96   |
| WDC       | WD1600AAJS-08L7A0  | 160 GB | 8       | 961   | 161   | 0.96   |
| Samsung   | HD161GJ            | 160 GB | 22      | 593   | 191   | 0.96   |
| WDC       | WD5000AAKS-22V1A0  | 500 GB | 10      | 647   | 155   | 0.96   |
| Hitachi   | HDT725032VLA360    | 320 GB | 16      | 843   | 123   | 0.96   |
| WDC       | WD3000BLFS-08YBU0  | 304 GB | 1       | 349   | 0     | 0.96   |
| Seagate   | ST3160811AS        | 160 GB | 81      | 789   | 432   | 0.96   |
| Seagate   | ST31000520AS       | 1 TB   | 16      | 923   | 378   | 0.96   |
| WDC       | WD10EZRX-00DC0B0   | 1 TB   | 4       | 348   | 0     | 0.96   |
| WDC       | WD5000LPVX-08V0TT6 | 500 GB | 1       | 348   | 0     | 0.95   |
| Seagate   | ST3250410AS        | 250 GB | 172     | 845   | 288   | 0.95   |
| Fujitsu   | MHY2200BH          | 200 GB | 16      | 575   | 37    | 0.95   |
| WDC       | WD1000DHTZ-04N21V0 | 1 TB   | 4       | 1061  | 25    | 0.95   |
| Toshiba   | MK6465GSXN         | 640 GB | 6       | 529   | 197   | 0.95   |
| WDC       | WD10EZEX-75M2NA0   | 1 TB   | 14      | 345   | 0     | 0.95   |
| WDC       | WD6400BPVT-16HXZT1 | 640 GB | 1       | 1037  | 2     | 0.95   |
| WDC       | WD3200BPVT-35ZEST0 | 320 GB | 22      | 468   | 2     | 0.95   |
| Maxtor    | STM3160215AS       | 160 GB | 23      | 845   | 710   | 0.95   |
| WDC       | WD5000BUCT-63LS5Y1 | 500 GB | 1       | 345   | 0     | 0.95   |
| WDC       | WD6400AARS-00Y5B1  | 640 GB | 15      | 767   | 11    | 0.95   |
| WDC       | WD3200AZRX-00A8LB0 | 320 GB | 4       | 345   | 0     | 0.95   |
| Seagate   | ST1000DM010-2DM162 | 1 TB   | 4       | 344   | 0     | 0.94   |
| WDC       | WD5000LPVT-08G33T1 | 500 GB | 15      | 367   | 1     | 0.94   |
| WDC       | WD1600AAJS-75M0A0  | 160 GB | 12      | 824   | 94    | 0.94   |
| Hitachi   | HTS545050B9A302    | 500 GB | 1       | 344   | 0     | 0.94   |
| WDC       | WD7500BPKT-00PK4T0 | 752 GB | 2       | 343   | 0     | 0.94   |
| Samsung   | HD322GJ            | 320 GB | 34      | 566   | 101   | 0.94   |
| Seagate   | ST31000528AS       | 1 TB   | 201     | 728   | 256   | 0.94   |
| WDC       | WD2500AVVS-62L2B0  | 250 GB | 2       | 347   | 5     | 0.94   |
| Seagate   | ST9250410AS        | 250 GB | 43      | 516   | 164   | 0.94   |
| WDC       | WD5000BEVT-24A0RT0 | 500 GB | 23      | 507   | 19    | 0.94   |
| Samsung   | HD251HJ            | 250 GB | 7       | 753   | 62    | 0.94   |
| WDC       | WD3200AAKS-00UU3A0 | 320 GB | 12      | 662   | 12    | 0.94   |
| WDC       | WD6400BPVT-55HXZT2 | 640 GB | 1       | 340   | 0     | 0.93   |
| WDC       | WD5000BPVT-22HXZT3 | 500 GB | 43      | 452   | 37    | 0.93   |
| WDC       | WD15EARX-22PASB0   | 1.5 TB | 1       | 340   | 0     | 0.93   |
| Seagate   | ST3250820A         | 250 GB | 10      | 874   | 535   | 0.93   |
| WDC       | WD7500BPVT-24HXZT3 | 752 GB | 11      | 379   | 24    | 0.93   |
| Seagate   | ST3200822AS        | 200 GB | 18      | 866   | 232   | 0.93   |
| WDC       | WD800JD-32LSA0     | 80 GB  | 2       | 1577  | 53    | 0.93   |
| WDC       | WD7500BPVX-22JC3T0 | 752 GB | 19      | 379   | 1     | 0.93   |
| WDC       | WD2003FYYS-01T8B0  | 2 TB   | 1       | 3050  | 8     | 0.93   |
| Seagate   | ST2000DM009-2G4100 | 2 TB   | 5       | 338   | 0     | 0.93   |
| WDC       | WD80EZZX-11CSGA0   | 8 TB   | 1       | 338   | 0     | 0.93   |
| Toshiba   | MK5075GSX          | 500 GB | 21      | 462   | 269   | 0.93   |
| Samsung   | HM120JC            | 120 GB | 2       | 638   | 51    | 0.93   |
| ExcelStor | J680               | 82 GB  | 1       | 1687  | 4     | 0.92   |
| IBM/Hi... | IC35L090AVV207-0   | 80 GB  | 2       | 735   | 2     | 0.92   |
| Hitachi   | HDT722516DLA380    | 164 GB | 11      | 817   | 53    | 0.92   |
| WDC       | WD80EMAZ-00M9AA0   | 8 TB   | 1       | 336   | 0     | 0.92   |
| WDC       | WD5000AAKX-22ERMA0 | 500 GB | 39      | 463   | 2     | 0.92   |
| WDC       | WD7500BPKX-80HPJT0 | 752 GB | 3       | 336   | 0     | 0.92   |
| WDC       | WD2500AAJS-55M0A0  | 250 GB | 3       | 416   | 3     | 0.92   |
| WDC       | WD3200BEKX-75B7WT0 | 320 GB | 2       | 336   | 0     | 0.92   |
| Seagate   | STM3250318AS       | 250 GB | 26      | 643   | 174   | 0.92   |
| WDC       | WD6400BEVT-00A0RT0 | 640 GB | 2       | 542   | 4     | 0.92   |
| Toshiba   | MG04ACA400EY       | 4 TB   | 2       | 335   | 0     | 0.92   |
| Fujitsu   | MHV2100BH          | 100 GB | 5       | 680   | 22    | 0.92   |
| Seagate   | ST1000NC001-1DY162 | 1 TB   | 5       | 652   | 202   | 0.92   |
| WDC       | WD5000BHTZ-04JCPV0 | 500 GB | 1       | 334   | 0     | 0.92   |
| WDC       | WD1600BEVT-22ZCT0  | 160 GB | 93      | 445   | 77    | 0.91   |
| WDC       | WD10PURX-64E5EY0   | 1 TB   | 10      | 347   | 1     | 0.91   |
| HGST      | HTS725032A7E630    | 320 GB | 18      | 370   | 285   | 0.91   |
| WDC       | WD2500AAKX-08U6AA0 | 250 GB | 5       | 503   | 4     | 0.91   |
| WDC       | WD6002FRYZ-01WD5B0 | 6 TB   | 1       | 332   | 0     | 0.91   |
| WDC       | WD4002FYYZ-01B7CB1 | 4 TB   | 2       | 332   | 0     | 0.91   |
| WDC       | WD3200AAKX-001CA0  | 320 GB | 30      | 688   | 15    | 0.91   |
| WDC       | WD3200AAKS-00V1A0  | 320 GB | 8       | 773   | 203   | 0.91   |
| WDC       | WD1001FALS-00U9B0  | 1 TB   | 1       | 995   | 2     | 0.91   |
| WDC       | WD1200BEVS-75UST0  | 120 GB | 11      | 436   | 2     | 0.91   |
| WDC       | WD20EARS-00J99B0   | 2 TB   | 2       | 331   | 0     | 0.91   |
| Toshiba   | DT01ACA100         | 1 TB   | 288     | 371   | 8     | 0.91   |
| Seagate   | ST250DM001 HD253GJ | 250 GB | 7       | 330   | 0     | 0.91   |
| Fujitsu   | MHV2120AH          | 120 GB | 3       | 418   | 2     | 0.91   |
| Seagate   | ST3750525AS        | 752 GB | 17      | 739   | 253   | 0.90   |
| WDC       | WD5000BPVT-00HXZT3 | 500 GB | 9       | 421   | 55    | 0.90   |
| Seagate   | ST3160021A         | 160 GB | 14      | 648   | 437   | 0.90   |
| WDC       | WD40EZRZ-00WN9B0   | 4 TB   | 7       | 328   | 0     | 0.90   |
| Hitachi   | HTS545050B9A300    | 500 GB | 117     | 604   | 209   | 0.90   |
| WDC       | WD5000LPVT-24G33T1 | 500 GB | 21      | 392   | 29    | 0.90   |
| WDC       | WD3200LPVX-80V0TT0 | 320 GB | 2       | 328   | 0     | 0.90   |
| WDC       | WD2500AVJS-63B6A0  | 250 GB | 3       | 768   | 6     | 0.90   |
| HGST      | HDS724020ALE640    | 2 TB   | 1       | 328   | 0     | 0.90   |
| WDC       | WD7500BPVT-22HXZT3 | 752 GB | 26      | 377   | 1     | 0.90   |
| Seagate   | ST96812AS          | 64 GB  | 8       | 470   | 236   | 0.90   |
| Hitachi   | HTS545016B9SA00    | 160 GB | 1       | 327   | 0     | 0.90   |
| WDC       | WD2500AAJS-00Z0A0  | 250 GB | 3       | 819   | 4     | 0.90   |
| WDC       | WD7500BPVT-75HXZT3 | 752 GB | 5       | 456   | 1     | 0.90   |
| Seagate   | ST2000VN000-1HJ164 | 2 TB   | 2       | 326   | 0     | 0.90   |
| WDC       | WD5000AAJS-19A8B0  | 500 GB | 1       | 326   | 0     | 0.90   |
| Seagate   | ST1500DL003-9VT16L | 1.5 TB | 35      | 816   | 306   | 0.89   |
| WDC       | WD5000LPLX-66ZNTT0 | 500 GB | 1       | 326   | 0     | 0.89   |
| WDC       | WD10SPCX-75KHST0   | 1 TB   | 3       | 326   | 0     | 0.89   |
| WDC       | WD1600BEVS-08RST2  | 160 GB | 2       | 326   | 0     | 0.89   |
| WDC       | WD10EZEX-00M2NA0   | 1 TB   | 3       | 383   | 12    | 0.89   |
| WDC       | WD6400BPVT-55HXZT3 | 640 GB | 2       | 591   | 4     | 0.89   |
| WDC       | WD7501AALS-00E3A0  | 752 GB | 9       | 733   | 41    | 0.89   |
| WDC       | WD2500JS-60MHB5    | 250 GB | 3       | 946   | 13    | 0.89   |
| WDC       | WD1600AAJS-22L7A0  | 160 GB | 15      | 543   | 7     | 0.89   |
| WDC       | WD800BB-60JKA0     | 80 GB  | 1       | 325   | 0     | 0.89   |
| WDC       | WD5000BPVT-16HXZT3 | 500 GB | 1       | 324   | 0     | 0.89   |
| WDC       | WD1600AAJS-00YZCA0 | 160 GB | 11      | 528   | 33    | 0.89   |
| WDC       | WD3200JS-00PDB0    | 320 GB | 1       | 324   | 0     | 0.89   |
| Fujitsu   | MHZ2320BH G1       | 320 GB | 7       | 596   | 33    | 0.89   |
| WDC       | WD2500JS-58NCB1    | 250 GB | 2       | 773   | 308   | 0.89   |
| Seagate   | STM3500418AS       | 500 GB | 25      | 876   | 473   | 0.89   |
| Seagate   | ST3250824A         | 250 GB | 4       | 753   | 253   | 0.88   |
| WDC       | WD5000AAKS-55V0A0  | 500 GB | 7       | 568   | 6     | 0.88   |
| WDC       | WD8003FRYZ-01JPDB1 | 8 TB   | 2       | 322   | 0     | 0.88   |
| WDC       | WD5000LPVT-75G33T0 | 500 GB | 5       | 366   | 1     | 0.88   |
| Seagate   | ST1000DX001-1NS162 | 1 TB   | 8       | 500   | 3     | 0.88   |
| WDC       | WD5000AAKX-08ERMA0 | 500 GB | 21      | 501   | 114   | 0.88   |
| Seagate   | ST2000VN000-1H3164 | 2 TB   | 1       | 321   | 0     | 0.88   |
| WDC       | WD800BEVT-22ZCT0   | 80 GB  | 1       | 321   | 0     | 0.88   |
| WDC       | WD2500AAJS-08B4A0  | 250 GB | 2       | 931   | 1211  | 0.88   |
| WDC       | WD10JPVT-55A1YT0   | 1 TB   | 1       | 320   | 0     | 0.88   |
| Samsung   | HM641JI            | 640 GB | 26      | 523   | 81    | 0.88   |
| WDC       | WD7500BPVT-26HXZT3 | 752 GB | 1       | 1277  | 3     | 0.88   |
| WDC       | WD5000AADS-00M2B0  | 500 GB | 26      | 940   | 206   | 0.87   |
| WDC       | WD2500AAJS-00L7A0  | 250 GB | 25      | 644   | 14    | 0.87   |
| WDC       | WD5000BPVT-08HXZT3 | 500 GB | 8       | 372   | 2     | 0.87   |
| Seagate   | ST250DM000-1BC141  | 250 GB | 14      | 368   | 7     | 0.87   |
| WDC       | WD3200AAJS-61B4A0  | 320 GB | 2       | 431   | 4     | 0.87   |
| WDC       | WD10JPVX-55JC3T3   | 1 TB   | 2       | 377   | 511   | 0.87   |
| WDC       | WD2500BEKT-75PVMT0 | 250 GB | 10      | 553   | 14    | 0.87   |
| WDC       | WD100EFAX-68LHPN0  | 10 TB  | 12      | 316   | 0     | 0.87   |
| Samsung   | HD752LJ            | 752 GB | 2       | 1517  | 4     | 0.87   |
| Fujitsu   | MHV2100AT          | 100 GB | 1       | 316   | 0     | 0.87   |
| WDC       | WD10EALX-008EA0    | 1 TB   | 5       | 325   | 1     | 0.86   |
| WDC       | WD800BEVS-00UST0   | 80 GB  | 1       | 315   | 0     | 0.86   |
| WDC       | WD6400BEVT-60A0RT0 | 640 GB | 2       | 382   | 18    | 0.86   |
| Seagate   | ST32000542AS       | 2 TB   | 24      | 736   | 337   | 0.86   |
| Samsung   | HD080HJ            | 80 GB  | 95      | 757   | 381   | 0.86   |
| WDC       | WD2000JS-55MHB0    | 200 GB | 1       | 313   | 0     | 0.86   |
| Toshiba   | MK6459GSXP         | 640 GB | 12      | 493   | 377   | 0.86   |
| Seagate   | ST500DM002-1BD142  | 500 GB | 554     | 532   | 117   | 0.86   |
| WDC       | WD2000JB-00GVA0    | 200 GB | 3       | 580   | 101   | 0.86   |
| WDC       | WD800AAJS-00L7A0   | 80 GB  | 1       | 313   | 0     | 0.86   |
| Seagate   | ST12000VN0007-2... | 12 TB  | 5       | 312   | 0     | 0.86   |
| Seagate   | ST2000VM003-1ET164 | 2 TB   | 2       | 311   | 0     | 0.85   |
| IBM/Hi... | IC35L120AVV207-0   | 128 GB | 1       | 933   | 2     | 0.85   |
| Seagate   | ST2000VX002-1AH166 | 2 TB   | 1       | 311   | 0     | 0.85   |
| WDC       | WD10EALX-559BA0    | 1 TB   | 5       | 517   | 6     | 0.85   |
| WDC       | WD1600JS-40TGB0    | 160 GB | 1       | 308   | 0     | 0.85   |
| Samsung   | SP0812N            | 80 GB  | 6       | 607   | 4     | 0.85   |
| MediaMax  | WL5000GSA12872B    | 5 TB   | 1       | 308   | 0     | 0.85   |
| WDC       | WD1600AAJB-00PVA0  | 160 GB | 11      | 560   | 165   | 0.84   |
| WDC       | WD5000LPVX-08V0TT2 | 500 GB | 3       | 387   | 3     | 0.84   |
| HGST      | HUH728080ALE604    | 8 TB   | 8       | 307   | 0     | 0.84   |
| WDC       | WD10EZRX-00D8PB0   | 1 TB   | 15      | 369   | 2     | 0.84   |
| WDC       | WD5000AAKS-08WWPA0 | 500 GB | 2       | 1656  | 77    | 0.84   |
| WDC       | WD5000AAKX-00U6AA0 | 500 GB | 23      | 428   | 3     | 0.84   |
| WDC       | WD3200BEVT-00SCST0 | 320 GB | 1       | 306   | 0     | 0.84   |
| Samsung   | HD400LJ            | 400 GB | 2       | 480   | 5     | 0.84   |
| WDC       | WD1500ADFD-00NLR1  | 150 GB | 2       | 454   | 4     | 0.84   |
| WDC       | WD40NMZW-11GX6S1   | 4 TB   | 22      | 352   | 22    | 0.84   |
| Hitachi   | HTS725050A9A362    | 500 GB | 3       | 461   | 104   | 0.84   |
| WDC       | WD3200BPVT-00HXZT3 | 320 GB | 5       | 437   | 6     | 0.84   |
| WDC       | WD3200BPVT-55JJ5T0 | 320 GB | 6       | 415   | 163   | 0.83   |
| WDC       | WD10SPZX-11Z10T0   | 1 TB   | 1       | 302   | 0     | 0.83   |
| WDC       | WD20NMVW-11EDZS7   | 2 TB   | 8       | 414   | 153   | 0.83   |
| Samsung   | HD103UI            | 1 TB   | 2       | 483   | 9     | 0.83   |
| WDC       | WD3200AAJS-00YZCA0 | 320 GB | 14      | 511   | 8     | 0.83   |
| Fujitsu   | MHW2080BH          | 80 GB  | 4       | 477   | 4     | 0.82   |
| Seagate   | ST320011A          | 20 GB  | 6       | 555   | 5     | 0.82   |
| Samsung   | HD320KJ            | 320 GB | 4       | 744   | 93    | 0.82   |
| WDC       | WD600BEAS-22KZT0   | 64 GB  | 1       | 300   | 0     | 0.82   |
| WDC       | WD5000AAKX-00KJ3A0 | 500 GB | 2       | 416   | 4     | 0.82   |
| WDC       | WD3200AAJS-00L7A0  | 320 GB | 72      | 743   | 51    | 0.82   |
| WDC       | WD800BEVS-07RST0   | 80 GB  | 5       | 330   | 1     | 0.82   |
| WDC       | WD6400BPVT-22HXZT3 | 640 GB | 8       | 563   | 9     | 0.82   |
| Seagate   | ST3320311CS        | 320 GB | 9       | 335   | 112   | 0.82   |
| WDC       | WD5000BPKT-00PK4T0 | 500 GB | 4       | 317   | 1     | 0.81   |
| Seagate   | ST250DM000-1BD141  | 250 GB | 92      | 529   | 121   | 0.81   |
| Seagate   | ST380215A          | 80 GB  | 28      | 464   | 107   | 0.81   |
| Fujitsu   | MHX2300BT          | 304 GB | 3       | 759   | 47    | 0.81   |
| Toshiba   | MK4009GAL          | 40 GB  | 1       | 296   | 0     | 0.81   |
| WDC       | WD1600JS-00MHB0    | 160 GB | 7       | 691   | 166   | 0.81   |
| Seagate   | ST1000DX001-1CM162 | 1 TB   | 34      | 419   | 46    | 0.81   |
| Seagate   | ST940210AS         | 40 GB  | 1       | 591   | 1     | 0.81   |
| WDC       | WD5000AVCS-732DY1  | 500 GB | 2       | 658   | 9     | 0.81   |
| Maxtor    | STM3250620A        | 250 GB | 1       | 295   | 0     | 0.81   |
| WDC       | WD1500HLFS-01G6U4  | 150 GB | 2       | 295   | 0     | 0.81   |
| WDC       | WD20PURX-64PFUY0   | 2 TB   | 1       | 294   | 0     | 0.81   |
| WDC       | WD800JD-22JNC0     | 80 GB  | 2       | 412   | 3     | 0.81   |
| WDC       | WD10EFRX-68FYTN0   | 1 TB   | 22      | 304   | 1     | 0.81   |
| Seagate   | ST3320820SCE       | 320 GB | 1       | 294   | 0     | 0.81   |
| WDC       | WD5000BPVT-00HXZT1 | 500 GB | 16      | 457   | 105   | 0.81   |
| Seagate   | ST2000DL001-9VT156 | 2 TB   | 8       | 1217  | 405   | 0.81   |
| WDC       | WD10JPVT-75A1YT0   | 1 TB   | 10      | 410   | 2     | 0.80   |
| Samsung   | SV1203N            | 120 GB | 2       | 441   | 3     | 0.80   |
| Hitachi   | HDS721616PLA320    | 160 GB | 3       | 1128  | 7     | 0.80   |
| Maxtor    | STM3160211AS       | 160 GB | 3       | 624   | 349   | 0.80   |
| Seagate   | ST1000VX001-1HH162 | 1 TB   | 7       | 291   | 0     | 0.80   |
| Hitachi   | HTS545032B9A300    | 320 GB | 99      | 513   | 142   | 0.80   |
| WDC       | WD2500AAJS-60Z0A0  | 250 GB | 2       | 291   | 0     | 0.80   |
| WDC       | WD3200BPVT-55ZEST0 | 320 GB | 4       | 313   | 1     | 0.80   |
| WDC       | WD2500BEVS-75UST0  | 250 GB | 9       | 378   | 2     | 0.80   |
| Magnet... | MD02500-BJDW-RO    | 250 GB | 1       | 291   | 0     | 0.80   |
| WDC       | WD1600AAJS-60M0A1  | 160 GB | 2       | 779   | 11    | 0.80   |
| Seagate   | ST750LM022 HN-M... | 752 GB | 93      | 384   | 37    | 0.80   |
| WDC       | WD10JPVX-22JC3T0   | 1 TB   | 166     | 328   | 33    | 0.80   |
| Hitachi   | HCS5C1025CLA382    | 250 GB | 1       | 290   | 0     | 0.80   |
| WDC       | WD40EFRX-68N32N0   | 4 TB   | 56      | 316   | 1     | 0.79   |
| WDC       | WD1600BB-00GUC0    | 160 GB | 4       | 832   | 61    | 0.79   |
| Seagate   | OOS2000G           | 2 TB   | 1       | 289   | 0     | 0.79   |
| WDC       | WD80EMAZ-00WJTA0   | 8 TB   | 13      | 289   | 0     | 0.79   |
| WDC       | WD10EZEX-00WN4A0   | 1 TB   | 50      | 335   | 1     | 0.79   |
| Seagate   | ST14000DM001-2J... | 14 TB  | 2       | 288   | 0     | 0.79   |
| Seagate   | ST3500414CS        | 500 GB | 3       | 495   | 1     | 0.79   |
| WDC       | WD2500AAKS-00B3A0  | 250 GB | 4       | 713   | 8     | 0.79   |
| WDC       | WD3000GLFS-01F8U0  | 304 GB | 1       | 287   | 0     | 0.79   |
| Maxtor    | STM380811AS        | 80 GB  | 4       | 500   | 5     | 0.79   |
| Toshiba   | MK3029GAC          | 32 GB  | 1       | 287   | 0     | 0.79   |
| Seagate   | ST6000DM003-2CY186 | 6 TB   | 7       | 287   | 0     | 0.79   |
| Samsung   | HD250HJ            | 250 GB | 38      | 815   | 595   | 0.79   |
| Seagate   | ST31000340NS       | 1 TB   | 19      | 1322  | 363   | 0.79   |
| WDC       | WD1200BEVT-22ZCT0  | 120 GB | 1       | 286   | 0     | 0.79   |
| WDC       | WD1200BEVS-75RST0  | 120 GB | 3       | 286   | 0     | 0.78   |
| WDC       | WD3200BPVT-22ZEST0 | 320 GB | 54      | 432   | 66    | 0.78   |
| WDC       | WD1600JD-22HBB0    | 160 GB | 1       | 1710  | 5     | 0.78   |
| Hitachi   | HTS547575A9E384    | 640 GB | 118     | 514   | 408   | 0.78   |
| Toshiba   | HDWA130            | 3 TB   | 1       | 285   | 0     | 0.78   |
| WDC       | WD5000BPVT-22HXZT1 | 500 GB | 19      | 434   | 2     | 0.78   |
| WDC       | WD10JPVT-08A1YT2   | 1 TB   | 10      | 393   | 2     | 0.78   |
| HP        | MB2000GCWLT        | 2 TB   | 1       | 1419  | 4     | 0.78   |
| Toshiba   | MK4058GSX          | 400 GB | 3       | 452   | 3     | 0.78   |
| Hitachi   | HDS721032CLA662    | 320 GB | 1       | 283   | 0     | 0.78   |
| WDC       | WD5000AAKX-08U6AA0 | 500 GB | 44      | 347   | 6     | 0.77   |
| Samsung   | HM321HI            | 320 GB | 99      | 432   | 88    | 0.77   |
| Toshiba   | MQ01ABD100M        | 1 TB   | 3       | 282   | 0     | 0.77   |
| WDC       | WD3200AAJS-22B4A0  | 320 GB | 5       | 958   | 6     | 0.77   |
| Apple     | HDD TOSHIBA MK5... | 500 GB | 2       | 505   | 201   | 0.77   |
| Seagate   | ST320DM000-1BD14C  | 320 GB | 34      | 443   | 105   | 0.77   |
| WDC       | WD2500BEKT-00PVMT0 | 250 GB | 2       | 279   | 0     | 0.77   |
| WDC       | WD800BEVS-22RST0   | 80 GB  | 28      | 418   | 54    | 0.76   |
| Fujitsu   | MHW2100BH          | 100 GB | 1       | 279   | 0     | 0.76   |
| WDC       | WD1600BEVT-75ZCT1  | 160 GB | 1       | 279   | 0     | 0.76   |
| Fujitsu   | MHY2120BH          | 120 GB | 28      | 554   | 202   | 0.76   |
| WDC       | WD10SPCX-22HWST0   | 1 TB   | 2       | 278   | 0     | 0.76   |
| WDC       | WD100EB-00BHF0     | 10 GB  | 1       | 557   | 1     | 0.76   |
| WDC       | WD10JPVX-16JC3T3   | 1 TB   | 3       | 278   | 0     | 0.76   |
| Hitachi   | HDP725050GLAT80    | 500 GB | 1       | 278   | 0     | 0.76   |
| Samsung   | HD161HJ            | 160 GB | 48      | 912   | 500   | 0.76   |
| Fujitsu   | MHY2080BH          | 80 GB  | 2       | 557   | 3     | 0.76   |
| WDC       | WD5000AAKX-083CA1  | 500 GB | 16      | 706   | 50    | 0.76   |
| Samsung   | HD321KJ            | 320 GB | 65      | 789   | 369   | 0.76   |
| WDC       | WD40EZRX-11SPEB0   | 4 TB   | 1       | 277   | 0     | 0.76   |
| Seagate   | ST3120813AS        | 120 GB | 21      | 888   | 567   | 0.76   |
| Samsung   | HD401LJ            | 400 GB | 4       | 702   | 14    | 0.76   |
| WDC       | WD5000AAKX-221CA0  | 500 GB | 2       | 1008  | 5     | 0.76   |
| WDC       | WD3200BPVT-24JJ5T0 | 320 GB | 61      | 335   | 59    | 0.76   |
| WDC       | WD3200BEVT-80A0RT0 | 320 GB | 37      | 446   | 22    | 0.76   |
| WDC       | WD2500JB-00REA0    | 250 GB | 9       | 714   | 24    | 0.76   |
| WDC       | WD5000BPVT-24HXZT3 | 500 GB | 22      | 405   | 2     | 0.76   |
| Toshiba   | MQ01ABD075         | 752 GB | 96      | 369   | 22    | 0.76   |
| WDC       | WD5000BPKX-60HPJT0 | 500 GB | 4       | 275   | 0     | 0.76   |
| WDC       | WD1600BEVT-00ZCT0  | 160 GB | 5       | 289   | 1     | 0.75   |
| WDC       | WD1200JS-00NCB1    | 120 GB | 2       | 591   | 27    | 0.75   |
| Seagate   | STM3320418AS       | 320 GB | 10      | 644   | 140   | 0.75   |
| WDC       | WD2004FBYZ-01YCBB1 | 2 TB   | 5       | 275   | 0     | 0.75   |
| WDC       | WD800BB-56JKC0     | 80 GB  | 6       | 735   | 7     | 0.75   |
| WDC       | WD15EARS-00Z5B1    | 1.5 TB | 27      | 1211  | 487   | 0.75   |
| WDC       | WD10JPVX-11JC3T0   | 1 TB   | 2       | 274   | 0     | 0.75   |
| WDC       | WD5000BPVT-22A1YT0 | 500 GB | 8       | 274   | 0     | 0.75   |
| Seagate   | ST2000DX002-2DV164 | 2 TB   | 25      | 300   | 1     | 0.75   |
| Seagate   | ST1000DM003-1SB10C | 1 TB   | 66      | 312   | 37    | 0.75   |
| WDC       | WD1600AABS-62PRA0  | 160 GB | 1       | 273   | 0     | 0.75   |
| WDC       | WD2500AAKX-00ERMA0 | 250 GB | 22      | 453   | 63    | 0.75   |
| WDC       | WD1200BEVS-00UST0  | 120 GB | 3       | 292   | 1     | 0.75   |
| WDC       | WD3000FYYZ-01UL1B3 | 3 TB   | 1       | 271   | 0     | 0.74   |
| WDC       | WD20EZRZ-00Z5HB0   | 2 TB   | 66      | 302   | 27    | 0.74   |
| Seagate   | ST1500LM012-1R817G | 1.5 TB | 2       | 269   | 0     | 0.74   |
| Maxtor    | STM380815AS        | 80 GB  | 21      | 725   | 633   | 0.74   |
| WDC       | WD1200BEVS-07RST0  | 120 GB | 2       | 268   | 0     | 0.74   |
| WDC       | WD5000AAKS-00V6A0  | 500 GB | 6       | 867   | 9     | 0.74   |
| Toshiba   | MK1031GAS          | 100 GB | 3       | 433   | 3     | 0.74   |
| Seagate   | ST2000DX001-SSH... | 2 TB   | 1       | 805   | 2     | 0.74   |
| WDC       | WD20PURX-64P6ZY0   | 2 TB   | 11      | 300   | 13    | 0.73   |
| WDC       | WD2500AAJB-57R1A0  | 250 GB | 1       | 268   | 0     | 0.73   |
| WDC       | WD5000M22K-24Z1... | 500 GB | 1       | 267   | 0     | 0.73   |
| Toshiba   | MK3263GSX          | 320 GB | 8       | 609   | 14    | 0.73   |
| Toshiba   | MQ04UBF100         | 1 TB   | 9       | 267   | 0     | 0.73   |
| HGST      | HTS721010A9E630    | 1 TB   | 267     | 313   | 117   | 0.73   |
| WDC       | WD1200JD-22HBB0    | 120 GB | 2       | 1602  | 5     | 0.73   |
| WDC       | WD3200LPVT-00FMCT0 | 320 GB | 1       | 266   | 0     | 0.73   |
| Fujitsu   | MHW2160BH          | 160 GB | 3       | 493   | 30    | 0.73   |
| WDC       | WD100EZAZ-11TDBA0  | 10 TB  | 8       | 266   | 0     | 0.73   |
| WDC       | WD5000AZRZ-00HTKB0 | 500 GB | 10      | 266   | 0     | 0.73   |
| Samsung   | HM500JI            | 500 GB | 31      | 423   | 4     | 0.73   |
| WDC       | WD3200LPVX-60V0TT0 | 320 GB | 1       | 266   | 0     | 0.73   |
| WDC       | WD5000LMVW-11CKRS0 | 500 GB | 2       | 265   | 0     | 0.73   |
| Fujitsu   | MHW2160BH PL       | 160 GB | 9       | 637   | 119   | 0.73   |
| Seagate   | ST9160411ASG       | 160 GB | 2       | 676   | 4     | 0.73   |
| WDC       | WD5000AAKS-65A7B2  | 500 GB | 1       | 265   | 0     | 0.73   |
| WDC       | WD2500AAKS-61L9A0  | 250 GB | 1       | 265   | 0     | 0.73   |
| WDC       | WD2500BEKT-00A25T0 | 250 GB | 1       | 264   | 0     | 0.73   |
| Samsung   | HD160JJ            | 160 GB | 70      | 823   | 462   | 0.73   |
| Toshiba   | DT01ACA050         | 500 GB | 301     | 309   | 25    | 0.72   |
| WDC       | WD2500AAKX-321CA0  | 250 GB | 1       | 264   | 0     | 0.72   |
| WDC       | WD5000LPVX-08V0TT5 | 500 GB | 14      | 320   | 1     | 0.72   |
| WDC       | WD2500AAJS-60B4A0  | 250 GB | 1       | 263   | 0     | 0.72   |
| WDC       | WD40EZRZ-00GXCB0   | 4 TB   | 40      | 263   | 0     | 0.72   |
| Seagate   | ST6000NM0115-1Y... | 6 TB   | 5       | 263   | 0     | 0.72   |
| Samsung   | HN-M500MBB         | 500 GB | 41      | 410   | 20    | 0.72   |
| WDC       | WD2500BEKX-00B7WT0 | 250 GB | 2       | 263   | 0     | 0.72   |
| Seagate   | ST1000DM003-1SB102 | 1 TB   | 54      | 290   | 6     | 0.72   |
| Seagate   | ST4000LM024-2AN17V | 4 TB   | 8       | 307   | 1     | 0.72   |
| WDC       | WD3200BEVT-00A0RT0 | 320 GB | 19      | 348   | 12    | 0.72   |
| Maxtor    | 6L040J2            | 40 GB  | 1       | 1576  | 5     | 0.72   |
| WDC       | WD10JPVX-80JC3T0   | 1 TB   | 9       | 262   | 0     | 0.72   |
| WDC       | WD7500BPKX-00HPJT0 | 752 GB | 9       | 330   | 11    | 0.72   |
| Seagate   | ST500LM000-1EJ1... | 500 GB | 8       | 304   | 47    | 0.72   |
| WDC       | WD10JPVX-35JC3T0   | 1 TB   | 4       | 261   | 0     | 0.72   |
| Seagate   | ST320LM001 HN-M... | 320 GB | 39      | 289   | 1     | 0.72   |
| Seagate   | ST8000NM0055-1R... | 8 TB   | 3       | 261   | 0     | 0.72   |
| WDC       | WD1600BEVS-60RST0  | 160 GB | 9       | 507   | 254   | 0.72   |
| WDC       | WD10JMVW-11S5XS0   | 1 TB   | 5       | 645   | 4     | 0.72   |
| WDC       | WD6401AALS-00E3A0  | 640 GB | 4       | 602   | 5     | 0.71   |
| Seagate   | ST340016A          | 40 GB  | 31      | 563   | 30    | 0.71   |
| WDC       | WD20EURX-63T0FY0   | 2 TB   | 9       | 417   | 229   | 0.71   |
| WDC       | WD10JPVX-75JC3T0   | 1 TB   | 48      | 327   | 11    | 0.71   |
| IBM/Hi... | IC35L040AVVA07-0   | 41 GB  | 4       | 623   | 83    | 0.71   |
| WDC       | WD5000AAKS-00E4A0  | 500 GB | 8       | 834   | 26    | 0.71   |
| WDC       | WD1600BEVT-75ZCT2  | 160 GB | 13      | 405   | 159   | 0.71   |
| Toshiba   | MK5065GSXF         | 500 GB | 10      | 363   | 4     | 0.71   |
| Hitachi   | HTS542516K9A300    | 160 GB | 6       | 790   | 220   | 0.71   |
| WDC       | WD1600JS-60MHB5    | 160 GB | 3       | 862   | 30    | 0.71   |
| WDC       | WD5000BPVT-35HXZT1 | 500 GB | 4       | 259   | 0     | 0.71   |
| Seagate   | ST330013A          | 32 GB  | 1       | 259   | 0     | 0.71   |
| WDC       | WD5000LPVT-00G33T0 | 500 GB | 6       | 541   | 2     | 0.71   |
| Samsung   | HM320II            | 320 GB | 20      | 399   | 204   | 0.71   |
| Seagate   | ST500LM012 HN-M... | 500 GB | 193     | 376   | 52    | 0.71   |
| Seagate   | ST91208220AS       | 120 GB | 2       | 461   | 507   | 0.71   |
| WDC       | WD2000FYYZ-01UL1B1 | 2 TB   | 10      | 885   | 194   | 0.71   |
| Seagate   | ST1500LM006 HN-... | 1.5 TB | 4       | 257   | 0     | 0.70   |
| Toshiba   | HDWL110            | 1 TB   | 5       | 256   | 0     | 0.70   |
| WDC       | WD3200BVVT-63A26Y0 | 320 GB | 4       | 303   | 165   | 0.70   |
| WDC       | WD2500BEKT-60PVMT0 | 250 GB | 11      | 346   | 92    | 0.70   |
| WDC       | WD7500BPVT-55HXZT3 | 752 GB | 2       | 465   | 4     | 0.70   |
| Toshiba   | MG06ACA10TE        | 10 TB  | 1       | 255   | 0     | 0.70   |
| Fujitsu   | MHX2250BT          | 250 GB | 2       | 409   | 5     | 0.70   |
| Hitachi   | HTS545032B9SA02    | 320 GB | 2       | 840   | 30    | 0.70   |
| Maxtor    | STM3320620AS       | 320 GB | 2       | 254   | 0     | 0.70   |
| WDC       | WD3200BEKT-00F3T0  | 320 GB | 2       | 253   | 0     | 0.69   |
| WDC       | WD3200BPVT-80JJ5T0 | 320 GB | 58      | 320   | 53    | 0.69   |
| Maxtor    | STM3250820AS       | 250 GB | 15      | 845   | 210   | 0.69   |
| WDC       | WD7500AZEX-00BN5A0 | 752 GB | 1       | 252   | 0     | 0.69   |
| WDC       | WD5000BPVT-75HXZT3 | 500 GB | 18      | 473   | 3     | 0.69   |
| WDC       | WD20EZRX-60D8PB0   | 2 TB   | 1       | 252   | 0     | 0.69   |
| WDC       | WD5000AAKS-07A7B0  | 500 GB | 3       | 754   | 6     | 0.69   |
| WDC       | WD3200BPVT-22JJ5T0 | 320 GB | 119     | 315   | 56    | 0.69   |
| Fujitsu   | MHV2060BH          | 64 GB  | 8       | 458   | 8     | 0.69   |
| WDC       | WD10JPVX-60JC3T0   | 1 TB   | 34      | 295   | 57    | 0.69   |
| WDC       | WD5000AAKB-00H8A0  | 500 GB | 15      | 547   | 7     | 0.69   |
| Samsung   | HD163GJ            | 160 GB | 1       | 251   | 0     | 0.69   |
| Seagate   | ST320LT009-9WC142  | 320 GB | 2       | 387   | 1     | 0.69   |
| Maxtor    | 6L020J1            | 20 GB  | 2       | 463   | 3     | 0.69   |
| Seagate   | ST500DM009-2DM14C  | 500 GB | 2       | 250   | 0     | 0.69   |
| Hitachi   | HTS545016B9A300    | 160 GB | 48      | 376   | 50    | 0.69   |
| WDC       | WD3200AAJS-60M0A0  | 320 GB | 1       | 749   | 2     | 0.68   |
| WDC       | WD7500BPKT-75PK4T0 | 752 GB | 16      | 457   | 3     | 0.68   |
| WDC       | WD2500BEVT-24A23T0 | 250 GB | 24      | 432   | 68    | 0.68   |
| WDC       | WD5003ABYZ-011FA0  | 500 GB | 6       | 395   | 6     | 0.68   |
| Hitachi   | HTS545025B9A300    | 250 GB | 115     | 477   | 113   | 0.68   |
| WDC       | WD1600BEVT-88ZCT0  | 160 GB | 1       | 247   | 0     | 0.68   |
| WDC       | WD2500BEVT-60ZCT1  | 250 GB | 6       | 394   | 10    | 0.68   |
| WDC       | WD20EARS-60MVWB0   | 2 TB   | 3       | 715   | 699   | 0.68   |
| Toshiba   | HDWD130            | 3 TB   | 32      | 250   | 32    | 0.68   |
| Seagate   | ST3000VN007-2AH16M | 3 TB   | 3       | 246   | 0     | 0.68   |
| WDC       | WD2000JS-00MHB1    | 200 GB | 1       | 246   | 0     | 0.68   |
| Fujitsu   | MHV2080AH          | 80 GB  | 6       | 503   | 3     | 0.68   |
| Hitachi   | HCT721016SLA380    | 160 GB | 3       | 246   | 0     | 0.67   |
| Fujitsu   | MJA2500BH FFS G1   | 500 GB | 1       | 246   | 0     | 0.67   |
| Seagate   | ST980813AS         | 80 GB  | 1       | 246   | 0     | 0.67   |
| WDC       | WD2503ABYX-01WERA1 | 256 GB | 4       | 619   | 3     | 0.67   |
| Samsung   | HD155UI            | 1.5 TB | 2       | 808   | 11    | 0.67   |
| WDC       | WD10EZEX-07ZF5A0   | 1 TB   | 1       | 982   | 3     | 0.67   |
| WDC       | WD5000AAKS-00V1A0  | 500 GB | 51      | 764   | 346   | 0.67   |
| WDC       | WD5000LPVX-22V0TT0 | 500 GB | 184     | 299   | 10    | 0.67   |
| WDC       | WD7500BPVT-22A1YT0 | 752 GB | 1       | 733   | 2     | 0.67   |
| Hitachi   | HDT721025SLA380    | 250 GB | 11      | 788   | 188   | 0.67   |
| WDC       | WD400UE-22HCT0     | 40 GB  | 1       | 732   | 2     | 0.67   |
| Seagate   | ST1000LM024 HN-... | 1 TB   | 559     | 354   | 53    | 0.67   |
| Toshiba   | HDWF180            | 8 TB   | 4       | 271   | 404   | 0.67   |
| WDC       | WD5000BEVT-11A0RT0 | 500 GB | 1       | 243   | 0     | 0.67   |
| WDC       | WD4000FYYZ-01UL1B0 | 4 TB   | 1       | 2193  | 8     | 0.67   |
| WDC       | WD10JMVW-11AJGS4   | 1 TB   | 18      | 243   | 0     | 0.67   |
| WDC       | WD1600AAJB-22WRA0  | 160 GB | 2       | 722   | 3     | 0.67   |
| WDC       | WD5000LPVX-80V0TT0 | 500 GB | 41      | 264   | 50    | 0.66   |
| WDC       | WD2500AAJS-00B4A0  | 250 GB | 17      | 712   | 60    | 0.66   |
| Hitachi   | HTS547550A9E384    | 500 GB | 140     | 416   | 304   | 0.66   |
| Hitachi   | HDS721010KLA330    | 1 TB   | 9       | 631   | 21    | 0.66   |
| Fujitsu   | MHZ2160BH FFS G1   | 160 GB | 2       | 497   | 1     | 0.66   |
| Seagate   | ST3500830AS        | 500 GB | 12      | 784   | 277   | 0.66   |
| WDC       | WD10EAVS-22D7B0    | 1 TB   | 1       | 2174  | 8     | 0.66   |
| Fujitsu   | MHW2080AT          | 80 GB  | 1       | 241   | 0     | 0.66   |
| WDC       | WD5000AVCS-632DY1  | 500 GB | 10      | 278   | 3     | 0.66   |
| HGST      | HUS726T4TALA6L4    | 4 TB   | 1       | 240   | 0     | 0.66   |
| WDC       | WD5000LPVT-00FMCT0 | 500 GB | 6       | 247   | 1     | 0.66   |
| Samsung   | HD082GJ            | 80 GB  | 15      | 559   | 363   | 0.66   |
| Seagate   | ST4000VM000-2AF166 | 4 TB   | 1       | 240   | 0     | 0.66   |
| WDC       | WD10EZEX-35WN4A0   | 1 TB   | 5       | 239   | 0     | 0.66   |
| Seagate   | ST9750420AS        | 752 GB | 54      | 505   | 114   | 0.66   |
| Toshiba   | HDWN180            | 8 TB   | 8       | 239   | 0     | 0.66   |
| WDC       | WD5000AAKX-60U6AA0 | 500 GB | 49      | 335   | 113   | 0.66   |
| Seagate   | ST3000NC002-1DY166 | 3 TB   | 2       | 987   | 1494  | 0.66   |
| Toshiba   | MK6034GAX          | 64 GB  | 2       | 879   | 5     | 0.65   |
| WDC       | WD3200LPVX-22V0TT0 | 320 GB | 14      | 262   | 1     | 0.65   |
| WDC       | WD60EZRZ-00GZ5B1   | 6 TB   | 5       | 237   | 0     | 0.65   |
| Hitachi   | HTS541010G9AT00    | 100 GB | 1       | 474   | 1     | 0.65   |
| Hitachi   | HTS725050A7E630    | 500 GB | 8       | 375   | 670   | 0.65   |
| WDC       | WD25EZRX-00MMMB0   | 2.5 TB | 2       | 894   | 4     | 0.65   |
| Seagate   | ST320LM010-1KJ15C  | 320 GB | 5       | 476   | 4     | 0.65   |
| Seagate   | ST250LT003-9YG14C  | 250 GB | 3       | 235   | 0     | 0.65   |
| WDC       | WD3200BEKT-60V5T1  | 320 GB | 25      | 517   | 375   | 0.64   |
| Seagate   | ST500LM011 HM501II | 500 GB | 2       | 277   | 1     | 0.64   |
| WDC       | WD5000LPVX-60V0TT0 | 500 GB | 15      | 352   | 147   | 0.64   |
| WDC       | WD3200BEVS-26VAT0  | 320 GB | 1       | 235   | 0     | 0.64   |
| HGST      | HTS545032A7E680    | 320 GB | 16      | 299   | 19    | 0.64   |
| WDC       | WD7500BPVT-60HXZT3 | 752 GB | 9       | 504   | 119   | 0.64   |
| WDC       | WD3200BEKT-75KA9T0 | 320 GB | 1       | 234   | 0     | 0.64   |
| WDC       | WD1600JS-60NCB1    | 160 GB | 5       | 603   | 64    | 0.64   |
| WDC       | WD5003ABYX-23 0... | 500 GB | 1       | 234   | 0     | 0.64   |
| WDC       | WD5000AADS-67S9B0  | 500 GB | 1       | 2104  | 8     | 0.64   |
| Hitachi   | HTS542516K9SA00    | 160 GB | 54      | 629   | 171   | 0.64   |
| WDC       | WD10JPVX-00JC3T0   | 1 TB   | 37      | 234   | 1     | 0.64   |
| WDC       | WD6400BPVT-26HXZT1 | 640 GB | 1       | 232   | 0     | 0.64   |
| WDC       | WD100EMAZ-00WJTA0  | 10 TB  | 12      | 232   | 0     | 0.64   |
| Hitachi   | HTS545032A7E380    | 320 GB | 23      | 355   | 163   | 0.64   |
| HGST      | HTS725032A7E635... | 320 GB | 1       | 231   | 0     | 0.64   |
| HGST      | HTS541075A9E680    | 752 GB | 35      | 315   | 554   | 0.63   |
| HGST      | HDN726040ALE614    | 4 TB   | 3       | 374   | 90    | 0.63   |
| WDC       | WD4003FFBX-68MU3N0 | 4 TB   | 2       | 231   | 0     | 0.63   |
| WDC       | WD800BB-00FRA0     | 80 GB  | 4       | 704   | 12    | 0.63   |
| Fujitsu   | MJA2160BH G2       | 160 GB | 7       | 403   | 326   | 0.63   |
| HGST      | HUS726060ALE610    | 6 TB   | 1       | 230   | 0     | 0.63   |
| Seagate   | ST360014A          | 64 GB  | 4       | 584   | 12    | 0.63   |
| Hitachi   | HDS721050DLE630    | 500 GB | 42      | 521   | 410   | 0.63   |
| Toshiba   | HDWD120            | 2 TB   | 37      | 230   | 0     | 0.63   |
| Hitachi   | HTS721080G9SA00    | 80 GB  | 6       | 383   | 34    | 0.63   |
| Toshiba   | Generic L200 Ha... | 2 TB   | 2       | 229   | 0     | 0.63   |
| Maxtor    | STM3250310AS       | 250 GB | 64      | 717   | 386   | 0.63   |
| Seagate   | ST3160212ACE       | 160 GB | 4       | 512   | 27    | 0.63   |
| WDC       | WD800BB-98JHC0     | 80 GB  | 1       | 1829  | 7     | 0.63   |
| Seagate   | ST9160821A         | 160 GB | 3       | 412   | 12    | 0.63   |
| Samsung   | HM100UI            | 1 TB   | 3       | 228   | 0     | 0.63   |
| WDC       | WD5000BEKT-60KA9T0 | 500 GB | 3       | 324   | 1     | 0.63   |
| WDC       | WD10EADS-22M2B0    | 1 TB   | 6       | 946   | 8     | 0.63   |
| WDC       | WD5000LPCX-24C6HT0 | 500 GB | 48      | 295   | 11    | 0.62   |
| ExcelStor | J8160S             | 160 GB | 6       | 445   | 3     | 0.62   |
| Seagate   | ST1000LM014-1EJ... | 1 TB   | 12      | 413   | 21    | 0.62   |
| WDC       | WD3200AAKS-00V6A0  | 320 GB | 3       | 315   | 1     | 0.62   |
| Seagate   | ST9640320AS        | 640 GB | 13      | 400   | 228   | 0.62   |
| Seagate   | ST1000LM014-SSH... | 1 TB   | 19      | 379   | 253   | 0.62   |
| Toshiba   | MQ01ABD032         | 320 GB | 85      | 347   | 113   | 0.62   |
| WDC       | WD2500YD-01NVB1    | 256 GB | 1       | 1357  | 5     | 0.62   |
| WDC       | WD5000BEKT-80KA9T1 | 500 GB | 4       | 280   | 1     | 0.62   |
| WDC       | WD5000BEVT-22A0RT0 | 500 GB | 38      | 511   | 68    | 0.62   |
| Toshiba   | MK5076GSXN         | 500 GB | 1       | 224   | 0     | 0.62   |
| WDC       | WD5000AZLX-00JKKA0 | 500 GB | 8       | 230   | 70    | 0.61   |
| Fujitsu   | MHZ2250BH G2       | 250 GB | 14      | 545   | 592   | 0.61   |
| WDC       | WD1600BEVT-00A23T0 | 160 GB | 3       | 277   | 3     | 0.61   |
| WDC       | WD5000AZLX-75K2TA0 | 500 GB | 5       | 223   | 0     | 0.61   |
| Seagate   | ST3120211AS        | 120 GB | 5       | 517   | 12    | 0.61   |
| Seagate   | ST9160412AS        | 160 GB | 11      | 559   | 338   | 0.61   |
| WDC       | WD2500AAJS-65M0A0  | 250 GB | 3       | 665   | 13    | 0.61   |
| WDC       | WD3200BEVT-75A23T0 | 320 GB | 3       | 283   | 47    | 0.61   |
| Hitachi   | HDS721010DLE630    | 1 TB   | 40      | 745   | 597   | 0.61   |
| Seagate   | ST3000DM001-9YN166 | 3 TB   | 27      | 828   | 1086  | 0.61   |
| Toshiba   | MQ04UBB400         | 4 TB   | 3       | 222   | 0     | 0.61   |
| Fujitsu   | MHZ2080BH G1       | 80 GB  | 3       | 222   | 0     | 0.61   |
| WDC       | WD3200BPVT-24ZEST0 | 320 GB | 22      | 304   | 54    | 0.61   |
| Seagate   | ST3000VX000-1ES166 | 3 TB   | 1       | 222   | 0     | 0.61   |
| WDC       | WD10SPZX-75Z10T0   | 1 TB   | 4       | 221   | 0     | 0.61   |
| WDC       | WD5000LPVX-75V0TT0 | 500 GB | 27      | 243   | 2     | 0.61   |
| Seagate   | ST9320423AS        | 320 GB | 55      | 463   | 283   | 0.61   |
| Fujitsu   | MHW2120BJ FFS G2   | 120 GB | 1       | 221   | 0     | 0.61   |
| WDC       | WD1600BEKT-60F3T1  | 160 GB | 1       | 221   | 0     | 0.61   |
| Hitachi   | HTS541080G9SA00    | 80 GB  | 7       | 365   | 3     | 0.61   |
| WDC       | WD2500AAKS-60VYA0  | 250 GB | 1       | 221   | 0     | 0.61   |
| Toshiba   | DT01ABA300V        | 3 TB   | 1       | 220   | 0     | 0.60   |
| Toshiba   | MK1059GSM          | 1 TB   | 28      | 647   | 809   | 0.60   |
| WDC       | WD5000AAKS-22A7B2  | 500 GB | 8       | 1177  | 94    | 0.60   |
| Seagate   | ST4000VN008-2DR166 | 4 TB   | 32      | 248   | 7     | 0.60   |
| HGST      | HTS541010A9E680    | 1 TB   | 175     | 354   | 309   | 0.60   |
| WDC       | WD5000AZLX-00K2TA0 | 500 GB | 9       | 218   | 0     | 0.60   |
| Seagate   | ST9120822AS        | 120 GB | 45      | 465   | 364   | 0.60   |
| WDC       | WD3000HLFS-75G6U1  | 304 GB | 1       | 218   | 0     | 0.60   |
| Maxtor    | 6G160P0            | 160 GB | 2       | 217   | 0     | 0.60   |
| WDC       | WD20NPVT-00Z2TT0   | 2 TB   | 3       | 336   | 12    | 0.60   |
| WDC       | WD1600JB-00GVC0    | 160 GB | 2       | 777   | 3     | 0.59   |
| Samsung   | HM250HI            | 250 GB | 78      | 328   | 14    | 0.59   |
| WDC       | WD5002AALX-32Z3A0  | 500 GB | 2       | 647   | 1     | 0.59   |
| Seagate   | ST2000VX008-2E3164 | 2 TB   | 3       | 216   | 0     | 0.59   |
| WDC       | WD2500BEKT-60A25T1 | 250 GB | 9       | 440   | 115   | 0.59   |
| WDC       | WD5000LPLX-75ZNTT0 | 500 GB | 10      | 216   | 0     | 0.59   |
| WDC       | WD3200AZDX-00SC2B0 | 320 GB | 2       | 379   | 440   | 0.59   |
| WDC       | WD3200BPVT-00ZEST0 | 320 GB | 4       | 215   | 0     | 0.59   |
| Toshiba   | MK5055GSXN         | 500 GB | 2       | 392   | 4     | 0.59   |
| Toshiba   | MQ01ABF032         | 320 GB | 23      | 248   | 45    | 0.59   |
| Samsung   | SP1624N            | 160 GB | 2       | 213   | 0     | 0.59   |
| Hitachi   | HTS547564A9E384    | 640 GB | 37      | 520   | 491   | 0.59   |
| WDC       | WD5000BEVT-26A0RT0 | 500 GB | 2       | 483   | 321   | 0.58   |
| Fujitsu   | MPE3084AE          | 8 GB   | 1       | 213   | 0     | 0.58   |
| Seagate   | ST2000NM0011       | 2 TB   | 3       | 1091  | 19    | 0.58   |
| WDC       | WD1200BB-00GUC0    | 120 GB | 2       | 1028  | 11    | 0.58   |
| Seagate   | ST3120213A         | 120 GB | 11      | 654   | 579   | 0.58   |
| HGST      | HEJ423232H9E300    | 320 GB | 1       | 211   | 0     | 0.58   |
| WDC       | WD2500BEVT-22A23T0 | 250 GB | 56      | 408   | 57    | 0.58   |
| WDC       | WD3200BEKX-00B7WT0 | 320 GB | 8       | 213   | 2     | 0.58   |
| Seagate   | ST340014AS         | 40 GB  | 5       | 1056  | 408   | 0.58   |
| WDC       | WD30NMVW-11C3NS2   | 3 TB   | 2       | 606   | 1     | 0.58   |
| Toshiba   | MK6461GSY          | 640 GB | 4       | 254   | 183   | 0.58   |
| WDC       | WD10EZEX-60WN4A0   | 1 TB   | 54      | 234   | 20    | 0.58   |
| WDC       | WD7500BPVT-55HXZT4 | 752 GB | 2       | 210   | 0     | 0.58   |
| WDC       | WD10EALX-229BA0    | 1 TB   | 5       | 793   | 11    | 0.57   |
| WDC       | WD5000BEKT-80KA9T0 | 500 GB | 3       | 317   | 1     | 0.57   |
| Toshiba   | MQ02ABD100H        | 1 TB   | 17      | 318   | 6     | 0.57   |
| WDC       | WD800BEVS-00RST0   | 80 GB  | 3       | 277   | 1     | 0.57   |
| Fujitsu   | MHZ2160BH G1       | 160 GB | 8       | 279   | 1     | 0.57   |
| WDC       | WD1600BEVT-22A23T0 | 160 GB | 26      | 360   | 5     | 0.57   |
| IBM/Hi... | IC35L040AVVN07-0   | 41 GB  | 2       | 576   | 3     | 0.57   |
| WDC       | WD400BB-00FJA0     | 40 GB  | 2       | 699   | 222   | 0.57   |
| WDC       | WD1600AAJS-75PSA0  | 160 GB | 5       | 353   | 3     | 0.57   |
| WDC       | WD1600BJKT-75F4T0  | 160 GB | 3       | 243   | 1     | 0.57   |
| Seagate   | ST8000DM004-2CX188 | 8 TB   | 31      | 238   | 53    | 0.57   |
| Samsung   | HN-M320MBB         | 320 GB | 3       | 401   | 3     | 0.57   |
| WDC       | WD1600BEVT-60ZCT1  | 160 GB | 6       | 324   | 170   | 0.57   |
| Seagate   | ST9160823ASG       | 160 GB | 3       | 329   | 337   | 0.56   |
| Toshiba   | MQ01ABD100         | 1 TB   | 313     | 298   | 104   | 0.56   |
| WDC       | WD10EZEX-00UD2A0   | 1 TB   | 7       | 335   | 125   | 0.56   |
| WDC       | WD10EURS-630AB1    | 1 TB   | 1       | 1846  | 8     | 0.56   |
| WDC       | WD1200JB-00GVC0    | 120 GB | 3       | 539   | 4     | 0.56   |
| WDC       | WD5000AAKX-003CA0  | 500 GB | 32      | 695   | 47    | 0.56   |
| Hitachi   | HTS723232L9SA60    | 320 GB | 2       | 292   | 4     | 0.56   |
| WDC       | WD7500BPKX-22HPJT0 | 752 GB | 12      | 221   | 1     | 0.56   |
| WDC       | WD20SDZW-11Z3CS0   | 2 TB   | 3       | 203   | 0     | 0.56   |
| Toshiba   | MK3265GSXN         | 320 GB | 19      | 469   | 273   | 0.56   |
| WDC       | WD1003FZEX-00K3CA0 | 1 TB   | 22      | 218   | 1     | 0.56   |
| Toshiba   | HDWA120            | 2 TB   | 5       | 203   | 0     | 0.56   |
| WDC       | WD3200BEKX-60B7WT0 | 320 GB | 2       | 203   | 0     | 0.56   |
| Toshiba   | MQ03UBB300         | 3 TB   | 4       | 252   | 3     | 0.56   |
| WDC       | WD5000BMVW-11AMCS2 | 500 GB | 1       | 202   | 0     | 0.56   |
| Toshiba   | MK1653GSX          | 160 GB | 1       | 201   | 0     | 0.55   |
| WDC       | WD5000AZDX-00SC2B0 | 500 GB | 4       | 371   | 12    | 0.55   |
| WDC       | WD800JD-00JNC0     | 80 GB  | 4       | 451   | 16    | 0.55   |
| Seagate   | ST500VT000-1BS142  | 500 GB | 2       | 200   | 0     | 0.55   |
| WDC       | WD740GD-00FLC0     | 74 GB  | 1       | 1202  | 5     | 0.55   |
| Samsung   | HD120IJ            | 120 GB | 21      | 795   | 334   | 0.55   |
| WDC       | WD20SDZW-11JJ8S0   | 2 TB   | 3       | 200   | 0     | 0.55   |
| Seagate   | ST4000VN000-2AH166 | 4 TB   | 1       | 200   | 0     | 0.55   |
| WDC       | WD5000BEVT-00A0RT0 | 500 GB | 13      | 386   | 173   | 0.55   |
| Seagate   | ST500LM000-1EJ162  | 500 GB | 61      | 270   | 72    | 0.55   |
| WDC       | WD10EZEX-21WN4A0   | 1 TB   | 17      | 208   | 1     | 0.55   |
| Samsung   | HD200HJ            | 200 GB | 17      | 855   | 668   | 0.55   |
| WDC       | WD5000AAKS-60Z1A0  | 500 GB | 5       | 1016  | 72    | 0.55   |
| WDC       | WD2500BEVT-00A23T0 | 250 GB | 11      | 494   | 10    | 0.54   |
| WDC       | WD1600BEVT-24A23T0 | 160 GB | 11      | 227   | 2     | 0.54   |
| Hitachi   | HTS543225L9A300    | 250 GB | 30      | 587   | 266   | 0.54   |
| Toshiba   | MK2035GSS          | 200 GB | 13      | 441   | 24    | 0.54   |
| WDC       | WD6400BPVT-00HXZT1 | 640 GB | 3       | 198   | 0     | 0.54   |
| Fujitsu   | MHY2160BH          | 160 GB | 11      | 250   | 270   | 0.54   |
| WDC       | WD5000AARS-003BB1  | 500 GB | 5       | 568   | 7     | 0.54   |
| WDC       | WD10EZEX-22MFCA0   | 1 TB   | 59      | 213   | 21    | 0.54   |
| Hitachi   | HTS727575A9E364    | 752 GB | 16      | 503   | 217   | 0.54   |
| WDC       | WD1002F9YZ-09H1JL1 | 1 TB   | 2       | 196   | 0     | 0.54   |
| Maxtor    | 6V250F0            | 250 GB | 2       | 196   | 0     | 0.54   |
| WDC       | WD3200BEKT-08PVMT1 | 320 GB | 3       | 195   | 0     | 0.54   |
| Hitachi   | HTS543225A7A384    | 250 GB | 30      | 352   | 410   | 0.54   |
| Quantum   | FIREBALLlct15 30   | 32 GB  | 1       | 391   | 1     | 0.54   |
| Hitachi   | HDS721612PLAT80    | 128 GB | 1       | 1366  | 6     | 0.53   |
| Toshiba   | MK6034GSX          | 64 GB  | 4       | 423   | 18    | 0.53   |
| Seagate   | ST94011A           | 40 GB  | 1       | 194   | 0     | 0.53   |
| WDC       | WD8004FRYZ-01VAEB0 | 8 TB   | 1       | 194   | 0     | 0.53   |
| Seagate   | ST320414A          | 20 GB  | 1       | 194   | 0     | 0.53   |
| Hitachi   | HTS727550A9E364    | 500 GB | 13      | 449   | 398   | 0.53   |
| WDC       | WD6400BPVT-80HXZT1 | 640 GB | 7       | 492   | 10    | 0.53   |
| Samsung   | SP0802N            | 80 GB  | 26      | 691   | 48    | 0.53   |
| WDC       | WD400BB-00DKA0     | 40 GB  | 1       | 193   | 0     | 0.53   |
| WDC       | WD800BEVS-75RST0   | 80 GB  | 4       | 381   | 252   | 0.53   |
| HGST      | HTS725050A7E630    | 500 GB | 145     | 338   | 219   | 0.53   |
| Seagate   | ST3750528AS        | 752 GB | 40      | 694   | 362   | 0.53   |
| HGST      | HUS726040ALE614    | 4 TB   | 2       | 192   | 0     | 0.53   |
| Seagate   | ST1000LM014-1EJ164 | 1 TB   | 60      | 355   | 96    | 0.53   |
| WDC       | WD5000LPCX-22VHAT0 | 500 GB | 24      | 196   | 1     | 0.53   |
| WDC       | WD10PURX-64D85Y0   | 1 TB   | 4       | 388   | 2     | 0.53   |
| WDC       | WD30NMRW-11YL9S4   | 3 TB   | 1       | 192   | 0     | 0.53   |
| Toshiba   | MK1059GSMP         | 1 TB   | 18      | 478   | 303   | 0.53   |
| WDC       | WD5000BMVW-11AMCS0 | 500 GB | 1       | 574   | 2     | 0.52   |
| Magnet... | MD03200-AVDW-RO    | 320 GB | 1       | 191   | 0     | 0.52   |
| WDC       | WD5000LPVX-55V0TT0 | 500 GB | 13      | 254   | 1     | 0.52   |
| WDC       | WD4001FAEX-00MJRA0 | 4 TB   | 1       | 190   | 0     | 0.52   |
| Samsung   | HD161HJ 41R0186LEN | 160 GB | 2       | 551   | 507   | 0.52   |
| WDC       | WD5000BPVT-26HXZT3 | 500 GB | 1       | 190   | 0     | 0.52   |
| Seagate   | ST2000LX001-1RG174 | 2 TB   | 31      | 233   | 43    | 0.52   |
| Hitachi   | HTS542580K9SA00    | 80 GB  | 10      | 373   | 4     | 0.52   |
| WDC       | WD5000KMVW-11ZSMS5 | 500 GB | 1       | 189   | 0     | 0.52   |
| WDC       | WD1600AVVS-63L2B0  | 160 GB | 6       | 799   | 4     | 0.52   |
| Toshiba   | MG03ACA300         | 3 TB   | 3       | 992   | 13    | 0.52   |
| Seagate   | ST96812A           | 64 GB  | 3       | 379   | 758   | 0.52   |
| Toshiba   | MQ01UBD050         | 500 GB | 2       | 187   | 0     | 0.51   |
| WDC       | WD2500BJKT-00F4T0  | 250 GB | 2       | 187   | 0     | 0.51   |
| Seagate   | ST9250315ASG       | 250 GB | 2       | 187   | 0     | 0.51   |
| WDC       | WD6400AAVS-00G9B1  | 640 GB | 2       | 1128  | 143   | 0.51   |
| Samsung   | SP0842N            | 80 GB  | 10      | 577   | 473   | 0.51   |
| WDC       | WD10EZEX-08WN4A0   | 1 TB   | 197     | 203   | 6     | 0.51   |
| Seagate   | ST500LM021-1KJ152  | 500 GB | 70      | 258   | 169   | 0.51   |
| WDC       | WD5000BEVT-60A0RT0 | 500 GB | 2       | 764   | 91    | 0.51   |
| Seagate   | ST500VM000-1SD101  | 500 GB | 3       | 186   | 0     | 0.51   |
| WDC       | WD1600AAJS-60B4A0  | 160 GB | 3       | 678   | 348   | 0.51   |
| Seagate   | ST9160411AS        | 160 GB | 5       | 403   | 31    | 0.51   |
| WDC       | WD10JPVT-22A1YT0   | 1 TB   | 9       | 382   | 3     | 0.51   |
| Seagate   | ST9250827AS        | 250 GB | 34      | 519   | 376   | 0.51   |
| Apple     | HDD ST3000DM001    | 3 TB   | 1       | 185   | 0     | 0.51   |
| Maxtor    | 7V300F0            | 304 GB | 2       | 1022  | 475   | 0.51   |
| Seagate   | ST250LT007-9ZV14C  | 250 GB | 3       | 440   | 203   | 0.51   |
| Seagate   | ST2000NM0055-1V... | 2 TB   | 1       | 184   | 0     | 0.51   |
| Seagate   | ST98823AS          | 80 GB  | 11      | 369   | 378   | 0.51   |
| Seagate   | ST380211AS         | 80 GB  | 9       | 631   | 500   | 0.50   |
| WDC       | WD3200BPVT-16JJ5T0 | 320 GB | 4       | 253   | 1     | 0.50   |
| Quantum   | FIREBALLlct15 15   | 16 GB  | 1       | 183   | 0     | 0.50   |
| Seagate   | ST31000523AS       | 1 TB   | 2       | 2094  | 11    | 0.50   |
| Hitachi   | HDT722525DLAT80    | 250 GB | 2       | 733   | 3     | 0.50   |
| Fujitsu   | MHZ2500BT G1       | 500 GB | 2       | 1426  | 6     | 0.50   |
| IBM/Hi... | IC25N030ATMR04-0   | 32 GB  | 1       | 544   | 2     | 0.50   |
| Toshiba   | MK2561GSYN         | 250 GB | 5       | 183   | 11    | 0.50   |
| WDC       | WD6000BLHX-01V7BV0 | 600 GB | 2       | 181   | 0     | 0.50   |
| WDC       | WD10JPCX-24UE4T0   | 1 TB   | 50      | 235   | 7     | 0.50   |
| Seagate   | ST160NM0011 39M... | 160 GB | 1       | 361   | 1     | 0.50   |
| WDC       | WD1200JB-00FUA0    | 120 GB | 1       | 180   | 0     | 0.49   |
| WDC       | WD5000LPCX-22VHAT1 | 500 GB | 5       | 180   | 0     | 0.49   |
| Seagate   | ST2000LM015-2E8174 | 2 TB   | 33      | 180   | 0     | 0.49   |
| Seagate   | ST3250310CS        | 250 GB | 2       | 701   | 21    | 0.49   |
| Samsung   | SP1613N            | 160 GB | 2       | 858   | 508   | 0.49   |
| Seagate   | ST3000VN000-1H4167 | 3 TB   | 1       | 179   | 0     | 0.49   |
| Seagate   | ST9500420AS        | 500 GB | 90      | 575   | 520   | 0.49   |
| WDC       | WD10SPCX-24HWST1   | 1 TB   | 21      | 222   | 53    | 0.49   |
| WDC       | WD10SPZX-75Z10T1   | 1 TB   | 12      | 198   | 3     | 0.49   |
| Seagate   | STM31000528AS      | 1 TB   | 3       | 351   | 1     | 0.49   |
| Samsung   | HE753LJ            | 752 GB | 2       | 374   | 51    | 0.49   |
| WDC       | WD10SPZX-24Z10T0   | 1 TB   | 21      | 195   | 1     | 0.49   |
| WDC       | WD2500JS-63MHB5    | 250 GB | 2       | 793   | 39    | 0.49   |
| Toshiba   | MK8034GSX          | 80 GB  | 9       | 368   | 34    | 0.49   |
| Seagate   | ST500NM0011        | 500 GB | 11      | 880   | 58    | 0.49   |
| WDC       | WD800BEVT-75ZCT2   | 80 GB  | 1       | 177   | 0     | 0.49   |
| WDC       | WD3200LPCX-24C6HT0 | 320 GB | 21      | 177   | 0     | 0.49   |
| WDC       | WD3200BEVT-22A23T0 | 320 GB | 42      | 450   | 73    | 0.49   |
| WDC       | WD1002FBYS-18A6B0  | 1 TB   | 2       | 2270  | 29    | 0.49   |
| WDC       | WD2005FBYZ-01YCBB2 | 2 TB   | 3       | 176   | 0     | 0.48   |
| WDC       | WD20EADS-42R6B0    | 2 TB   | 1       | 176   | 0     | 0.48   |
| Seagate   | ST3250312CS        | 250 GB | 12      | 414   | 211   | 0.48   |
| Seagate   | ST500LM014 HN-M... | 500 GB | 7       | 271   | 2     | 0.48   |
| WDC       | WD6400BPVT-22HXZT1 | 640 GB | 4       | 261   | 3     | 0.48   |
| WDC       | WD3200BEKT-60PVMT0 | 320 GB | 11      | 389   | 256   | 0.48   |
| WDC       | WD2500BPVT-22ZEST0 | 250 GB | 18      | 218   | 4     | 0.48   |
| Seagate   | ST3300822AS        | 304 GB | 1       | 176   | 0     | 0.48   |
| HGST      | HTS545050A7E380    | 500 GB | 158     | 377   | 281   | 0.48   |
| Seagate   | ST33000651AS       | 3 TB   | 5       | 374   | 203   | 0.48   |
| WDC       | WD3200BEVT-24A23T0 | 320 GB | 10      | 529   | 103   | 0.48   |
| Samsung   | HM080HC            | 72 GB  | 1       | 526   | 2     | 0.48   |
| WDC       | WD5000LPCX-00VHAT0 | 500 GB | 28      | 221   | 1     | 0.48   |
| Seagate   | ST980210AS         | 80 GB  | 1       | 175   | 0     | 0.48   |
| WDC       | WD10EZEX-08Y20A0   | 1 TB   | 8       | 209   | 1     | 0.48   |
| Hitachi   | HTS545050A7E380    | 500 GB | 113     | 364   | 184   | 0.48   |
| HGST      | HUS726040ALA614    | 4 TB   | 6       | 177   | 3     | 0.48   |
| Toshiba   | MK2555GSXF         | 250 GB | 7       | 174   | 0     | 0.48   |
| WDC       | WD2500JD-40HBC0    | 250 GB | 1       | 1391  | 7     | 0.48   |
| WDC       | WD10SPCX-16HWST0   | 1 TB   | 1       | 173   | 0     | 0.48   |
| WDC       | WD1600BEVT-35ZCT0  | 160 GB | 2       | 173   | 0     | 0.48   |
| WDC       | WD1005FBYZ-01YCBB2 | 1 TB   | 3       | 173   | 0     | 0.48   |
| WDC       | WD5000AZLX-60K2TA0 | 500 GB | 9       | 173   | 0     | 0.48   |
| Samsung   | SP2504C            | 250 GB | 44      | 1163  | 771   | 0.47   |
| Fujitsu   | MJA2320BH G2       | 320 GB | 8       | 724   | 390   | 0.47   |
| Hitachi   | HTS543216L9SA00    | 160 GB | 14      | 367   | 80    | 0.47   |
| WDC       | WD5000BPVT-80HXZT1 | 500 GB | 6       | 604   | 56    | 0.47   |
| WDC       | WD40EZRZ-75GXCB0   | 4 TB   | 7       | 172   | 0     | 0.47   |
| WDC       | WD7500BPVT-08HXZT3 | 752 GB | 3       | 172   | 0     | 0.47   |
| Toshiba   | MQ01ABB200         | 2 TB   | 3       | 222   | 235   | 0.47   |
| WDC       | WD10SDZW-11UMGS0   | 1 TB   | 3       | 171   | 0     | 0.47   |
| WDC       | WD10EALX-759BA0    | 1 TB   | 1       | 1887  | 10    | 0.47   |
| Seagate   | ST95005620AS       | 500 GB | 13      | 697   | 166   | 0.47   |
| Toshiba   | MG06ACA600E        | 6 TB   | 1       | 171   | 0     | 0.47   |
| WDC       | WD10EARX-00PASB0   | 1 TB   | 3       | 838   | 26    | 0.47   |
| WDC       | WD6400BEVT-22A0RT0 | 640 GB | 10      | 508   | 9     | 0.47   |
| Seagate   | ST9160301AS        | 160 GB | 7       | 230   | 288   | 0.47   |
| Hitachi   | HTS723232A7A364    | 320 GB | 40      | 392   | 476   | 0.47   |
| WDC       | WD5000BPKX-22HPJT0 | 500 GB | 12      | 297   | 2     | 0.47   |
| Hitachi   | HCS5C1010DLE630    | 1 TB   | 1       | 169   | 0     | 0.47   |
| WDC       | WD3200AAKS-22L6A0  | 320 GB | 4       | 648   | 6     | 0.47   |
| WDC       | WD3200BJKT-00F4T0  | 320 GB | 1       | 169   | 0     | 0.46   |
| Samsung   | HM250HJ            | 250 GB | 2       | 337   | 17    | 0.46   |
| WDC       | WD3200LPVT-08G33T1 | 320 GB | 5       | 225   | 2     | 0.46   |
| WDC       | WD10EZRZ-00HTKB0   | 1 TB   | 44      | 177   | 1     | 0.46   |
| Samsung   | HM250JI            | 250 GB | 7       | 395   | 222   | 0.46   |
| Seagate   | ST1000DM000-9TS15E | 1 TB   | 1       | 168   | 0     | 0.46   |
| Seagate   | ST4000DM004-2CV104 | 4 TB   | 85      | 180   | 3     | 0.46   |
| Seagate   | ST3400832A         | 400 GB | 1       | 2185  | 12    | 0.46   |
| Hitachi   | HTS541616J9SA00    | 160 GB | 32      | 506   | 77    | 0.46   |
| WDC       | WD10JPLX-00MBPT0   | 1 TB   | 30      | 181   | 6     | 0.46   |
| HGST      | HTS541010B7E610    | 1 TB   | 26      | 179   | 1     | 0.46   |
| Hitachi   | HDS721616PLAT80    | 160 GB | 4       | 946   | 31    | 0.46   |
| WDC       | WD2500LPCX-24C6HT0 | 250 GB | 38      | 191   | 57    | 0.46   |
| WDC       | WD1600BEVS-22VAT0  | 160 GB | 2       | 248   | 1     | 0.46   |
| Hitachi   | HTS541612J9SA00 3H | 120 GB | 2       | 558   | 93    | 0.46   |
| Hitachi   | HDE721010SLA330    | 1 TB   | 2       | 988   | 80    | 0.46   |
| WDC       | WD5000MPCK-60AWHT0 | 500 GB | 1       | 166   | 0     | 0.46   |
| Seagate   | ST3250820NS        | 250 GB | 2       | 695   | 1050  | 0.46   |
| HGST      | HTS541515A9E630    | 1.5 TB | 4       | 587   | 265   | 0.46   |
| Hitachi   | HTS543232A7A384    | 320 GB | 176     | 326   | 320   | 0.45   |
| Lenovo    | ST1000NM0055 91... | 1 TB   | 1       | 165   | 0     | 0.45   |
| Seagate   | ST9100824A         | 100 GB | 1       | 165   | 0     | 0.45   |
| WDC       | WD800BEVE-00A0HT0  | 80 GB  | 1       | 165   | 0     | 0.45   |
| Seagate   | ST2000LM007-1R8174 | 2 TB   | 57      | 184   | 42    | 0.45   |
| Seagate   | ST9500423AS        | 500 GB | 32      | 469   | 68    | 0.45   |
| Seagate   | ST9750423AS        | 752 GB | 13      | 562   | 315   | 0.45   |
| WDC       | WD3200BEVT-60ZCT1  | 320 GB | 7       | 436   | 210   | 0.45   |
| Seagate   | ST1000DX002-2DV162 | 1 TB   | 18      | 168   | 2     | 0.45   |
| WDC       | WD20NMVW-11AV3S0   | 2 TB   | 3       | 464   | 4     | 0.45   |
| IBM/Hi... | IC35L120AVV207-1   | 128 GB | 2       | 496   | 9     | 0.45   |
| WDC       | WD121KRYZ-01W0RB0  | 12 TB  | 1       | 163   | 0     | 0.45   |
| WDC       | WD3200AAJB-00J3A0  | 320 GB | 18      | 346   | 25    | 0.45   |
| Hitachi   | HTS543216L9A300    | 160 GB | 41      | 511   | 213   | 0.45   |
| WDC       | WD10TMVW-11ZSMS4   | 1 TB   | 2       | 162   | 0     | 0.45   |
| Samsung   | SP0812C            | 80 GB  | 17      | 492   | 159   | 0.44   |
| WDC       | WD10SMZW-11Y0TS0   | 1 TB   | 14      | 162   | 0     | 0.44   |
| Seagate   | ST920217AS         | 20 GB  | 1       | 162   | 0     | 0.44   |
| Toshiba   | MK8037GSX          | 80 GB  | 19      | 448   | 139   | 0.44   |
| Toshiba   | MK8007GAH          | 80 GB  | 2       | 210   | 7     | 0.44   |
| WDC       | WD3200BEVT-00ZCT0  | 320 GB | 4       | 405   | 4     | 0.44   |
| WDC       | WD10JUCT-63J6SY0   | 1 TB   | 5       | 161   | 0     | 0.44   |
| Hitachi   | HDS722512VLAT20    | 128 GB | 1       | 805   | 4     | 0.44   |
| WDC       | WD10SPCX-80HWST0   | 1 TB   | 1       | 160   | 0     | 0.44   |
| Hitachi   | HTS542560K9SA00    | 64 GB  | 1       | 160   | 0     | 0.44   |
| WDC       | WD7500BPVX-75JC3T0 | 752 GB | 2       | 299   | 2     | 0.44   |
| WDC       | WD5000LPVX-28V0TT0 | 500 GB | 1       | 159   | 0     | 0.44   |
| Seagate   | ST9160827AS        | 160 GB | 34      | 435   | 283   | 0.44   |
| Fujitsu   | MHZ2250BS G2       | 250 GB | 1       | 159   | 0     | 0.44   |
| WDC       | WD6400BEVT-80A0RT1 | 640 GB | 2       | 479   | 13    | 0.44   |
| WDC       | WD400BB-23FJA0     | 40 GB  | 1       | 796   | 4     | 0.44   |
| WDC       | WD3200BPVT-60JJ5T0 | 320 GB | 9       | 393   | 132   | 0.43   |
| Toshiba   | HDWD110            | 1 TB   | 150     | 168   | 5     | 0.43   |
| Hitachi   | HTS541075A9E680    | 752 GB | 4       | 325   | 764   | 0.43   |
| Hitachi   | HTS545025B9SA02    | 250 GB | 7       | 199   | 290   | 0.43   |
| Hitachi   | HTS543232L9A300    | 320 GB | 20      | 642   | 545   | 0.43   |
| WDC       | WD2500BEVT-80A23T0 | 250 GB | 20      | 316   | 41    | 0.43   |
| WDC       | WD7500BPVX-00JC3T0 | 752 GB | 1       | 157   | 0     | 0.43   |
| Toshiba   | HDWE140            | 4 TB   | 16      | 169   | 71    | 0.43   |
| WDC       | WD3200BEVT-26A23T0 | 320 GB | 3       | 274   | 73    | 0.43   |
| Hitachi   | HTS545025B9SA00    | 250 GB | 1       | 157   | 0     | 0.43   |
| Toshiba   | MK3276GSXN         | 320 GB | 1       | 156   | 0     | 0.43   |
| WDC       | WD3200BPVT-80ZEST0 | 320 GB | 30      | 328   | 43    | 0.43   |
| Hitachi   | HDP725032GLA380    | 320 GB | 6       | 868   | 35    | 0.43   |
| Seagate   | ST9320325AS        | 320 GB | 235     | 463   | 455   | 0.43   |
| WDC       | WD3200BPVT-75ZEST0 | 320 GB | 4       | 675   | 7     | 0.43   |
| Seagate   | STM9120817AS       | 120 GB | 1       | 155   | 0     | 0.43   |
| WDC       | WD80EFAX-68KNBN0   | 8 TB   | 5       | 155   | 0     | 0.42   |
| WDC       | WD2500BEVT-08A23T1 | 250 GB | 13      | 270   | 133   | 0.42   |
| WDC       | WD10SPZX-17Z10T0   | 1 TB   | 4       | 154   | 0     | 0.42   |
| Toshiba   | MK6459GSX          | 640 GB | 6       | 495   | 577   | 0.42   |
| WDC       | WD10EZEX-07WN4A0   | 1 TB   | 5       | 217   | 1     | 0.42   |
| Seagate   | ST1000DM010-2EP102 | 1 TB   | 236     | 174   | 18    | 0.42   |
| WDC       | WD1200JD-55HBB0    | 120 GB | 1       | 923   | 5     | 0.42   |
| Samsung   | SV0412H            | 40 GB  | 6       | 1055  | 104   | 0.42   |
| Seagate   | ST1000LM048-2E7172 | 1 TB   | 65      | 175   | 35    | 0.42   |
| Hitachi   | HTS541060G9AT00    | 64 GB  | 6       | 564   | 17    | 0.42   |
| Samsung   | SP0822N            | 80 GB  | 9       | 154   | 1     | 0.42   |
| WDC       | WD5000AAKS-08V0A0  | 500 GB | 7       | 506   | 39    | 0.42   |
| WDC       | WD5000BPVT-60HXZT1 | 500 GB | 3       | 667   | 388   | 0.42   |
| WDC       | WD10EARX-00NYB0    | 1 TB   | 1       | 151   | 0     | 0.42   |
| WDC       | WD15NMVW-11AV3S2   | 1.5 TB | 1       | 151   | 0     | 0.42   |
| Seagate   | ST250LM004 HN-M... | 250 GB | 8       | 262   | 7     | 0.42   |
| Seagate   | ST12000DM0007-2... | 12 TB  | 3       | 161   | 1     | 0.42   |
| WDC       | WD3200LPVX-75V0TT0 | 320 GB | 2       | 151   | 0     | 0.42   |
| WDC       | WD6400AADS-00M2B0  | 640 GB | 11      | 891   | 20    | 0.41   |
| WDC       | WD10JPVX-60JC3T1   | 1 TB   | 26      | 187   | 46    | 0.41   |
| WDC       | WD10JUCT-63CYNY0   | 1 TB   | 2       | 150   | 0     | 0.41   |
| WDC       | WD10JPLX-00MBPT1   | 1 TB   | 2       | 149   | 0     | 0.41   |
| Toshiba   | MK5059GSXP         | 500 GB | 34      | 411   | 379   | 0.41   |
| Hitachi   | HDS721010KLA33R... | 1 TB   | 1       | 3734  | 24    | 0.41   |
| Seagate   | ST3200822A         | 200 GB | 6       | 1408  | 10    | 0.41   |
| Samsung   | SP1634N            | 160 GB | 1       | 298   | 1     | 0.41   |
| Toshiba   | MK2555GSX          | 250 GB | 32      | 427   | 71    | 0.41   |
| Hitachi   | HTS542525K9SA00    | 250 GB | 33      | 535   | 101   | 0.41   |
| Hitachi   | HTS723225L9SA62    | 250 GB | 1       | 595   | 3     | 0.41   |
| Seagate   | ST3160815SV        | 160 GB | 5       | 681   | 1240  | 0.41   |
| WDC       | WD10JMVW-11AJGS3   | 1 TB   | 8       | 175   | 4     | 0.41   |
| Toshiba   | MD03ACA400V        | 4 TB   | 1       | 1037  | 6     | 0.41   |
| Fujitsu   | MHV2060AT          | 64 GB  | 2       | 528   | 4     | 0.41   |
| Samsung   | HM320HJ            | 320 GB | 5       | 303   | 355   | 0.41   |
| WDC       | WD1200JS-22NCB1    | 120 GB | 1       | 1184  | 7     | 0.41   |
| WDC       | WD30EFRX-68N32N0   | 3 TB   | 2       | 147   | 0     | 0.41   |
| Toshiba   | MK6475GSX          | 640 GB | 25      | 395   | 386   | 0.40   |
| WDC       | WD5000AVVS-63M8B0  | 500 GB | 1       | 1324  | 8     | 0.40   |
| Seagate   | ST500LT012-1DG142  | 500 GB | 403     | 216   | 77    | 0.40   |
| Hitachi   | HDS722525VLSA80    | 250 GB | 2       | 370   | 17    | 0.40   |
| Toshiba   | MK4025GAS          | 40 GB  | 2       | 423   | 18    | 0.40   |
| Seagate   | ST750LM030-1KKG62  | 752 GB | 2       | 146   | 0     | 0.40   |
| WDC       | WD2500BEVT-00A0RT1 | 245 GB | 1       | 146   | 0     | 0.40   |
| WDC       | WD1600AAJB-00J3A0  | 160 GB | 16      | 532   | 134   | 0.40   |
| Toshiba   | MK8009GAH          | 80 GB  | 3       | 455   | 31    | 0.40   |
| Toshiba   | HDWD105            | 500 GB | 75      | 163   | 27    | 0.40   |
| MediaMax  | WL320GLSA854G      | 320 GB | 1       | 146   | 0     | 0.40   |
| Hitachi   | HTS545050KTA300    | 500 GB | 6       | 520   | 5     | 0.40   |
| Seagate   | ST2000DM005-2CW102 | 2 TB   | 6       | 145   | 0     | 0.40   |
| Hitachi   | HTS725050A9A364    | 500 GB | 22      | 458   | 725   | 0.40   |
| WDC       | WD5000BPVT-55HXZT3 | 500 GB | 3       | 216   | 2     | 0.40   |
| Fujitsu   | MHV2060BHPL        | 64 GB  | 1       | 144   | 0     | 0.40   |
| WDC       | WD7500KMVW-11ZSMS4 | 752 GB | 1       | 434   | 2     | 0.40   |
| Hitachi   | HTS542512K9SA00    | 120 GB | 56      | 508   | 116   | 0.40   |
| Toshiba   | MK5076GSX -63      | 500 GB | 2       | 144   | 0     | 0.40   |
| Toshiba   | MQ01ABD050         | 500 GB | 123     | 313   | 287   | 0.40   |
| Seagate   | ST3750330NS        | 752 GB | 3       | 560   | 337   | 0.39   |
| WDC       | WD10EZRZ-00Z5HB0   | 1 TB   | 4       | 144   | 0     | 0.39   |
| Maxtor    | 6G160E0            | 160 GB | 8       | 327   | 156   | 0.39   |
| WDC       | WD3200AAJS-55VWA0  | 320 GB | 1       | 1006  | 6     | 0.39   |
| HGST      | HTS541010A7E630    | 1 TB   | 24      | 184   | 129   | 0.39   |
| Seagate   | ST4000NC001-1FS168 | 4 TB   | 1       | 143   | 0     | 0.39   |
| Seagate   | ST96023AS          | 64 GB  | 2       | 395   | 5     | 0.39   |
| Seagate   | ST320LT007-9ZV142  | 320 GB | 35      | 456   | 686   | 0.39   |
| HP        | VB0160EAVEQ        | 160 GB | 1       | 429   | 2     | 0.39   |
| WDC       | WD2500BPVT-24JJ5T0 | 250 GB | 4       | 142   | 0     | 0.39   |
| WDC       | WD3200AAKX-32ERMA0 | 320 GB | 1       | 142   | 0     | 0.39   |
| Hitachi   | HTS541212H9AT00    | 120 GB | 3       | 438   | 5     | 0.39   |
| WDC       | WD3200LPVX-08V0TT5 | 320 GB | 3       | 141   | 0     | 0.39   |
| Seagate   | ST500LX012-SSHD... | 500 GB | 1       | 283   | 1     | 0.39   |
| WDC       | WD7500KMVV-11TK7S1 | 752 GB | 1       | 141   | 0     | 0.39   |
| WDC       | WD800BD-22MRA1     | 80 GB  | 2       | 141   | 0     | 0.39   |
| IBM       | DTLA-305020        | 20 GB  | 2       | 1494  | 37    | 0.39   |
| Toshiba   | MG03ACA100         | 1 TB   | 8       | 165   | 1     | 0.39   |
| WDC       | WD2500AAJB-57WGA0  | 250 GB | 1       | 140   | 0     | 0.38   |
| WDC       | WD800BB-00HEA0     | 80 GB  | 1       | 840   | 5     | 0.38   |
| Samsung   | HD256GJ            | 250 GB | 2       | 392   | 504   | 0.38   |
| WDC       | WD2500AAJS-07B4A0  | 250 GB | 2       | 1695  | 198   | 0.38   |
| WDC       | WD400EB-11CPF0     | 40 GB  | 2       | 1019  | 31    | 0.38   |
| WDC       | WD1600AAJS-98PSA0  | 160 GB | 2       | 273   | 1     | 0.38   |
| WDC       | WD2500BEKT-75A25T0 | 250 GB | 3       | 443   | 5     | 0.38   |
| WDC       | WD30EZRZ-22Z5HB0   | 3 TB   | 2       | 139   | 0     | 0.38   |
| WDC       | WD2500JS-60MHB1    | 250 GB | 2       | 331   | 8     | 0.38   |
| Toshiba   | MK1655GSX          | 160 GB | 12      | 315   | 34    | 0.38   |
| WDC       | WD20SPZX-00CRAT0   | 2 TB   | 1       | 137   | 0     | 0.38   |
| Seagate   | ST3500410AS        | 500 GB | 28      | 1022  | 387   | 0.38   |
| HGST      | HUS726T6TALE6L4    | 6 TB   | 3       | 137   | 0     | 0.38   |
| WDC       | WD10PURZ-85U8XY0   | 1 TB   | 1       | 137   | 0     | 0.38   |
| Toshiba   | MQ01ABF050         | 500 GB | 336     | 178   | 77    | 0.38   |
| Seagate   | ST9320310AS        | 320 GB | 9       | 466   | 436   | 0.37   |
| Hitachi   | HCT721050SLA380    | 500 GB | 1       | 136   | 0     | 0.37   |
| Hitachi   | HTS541040G9AT00    | 40 GB  | 4       | 263   | 4     | 0.37   |
| Samsung   | HD080HJ-P          | 80 GB  | 10      | 735   | 396   | 0.37   |
| WDC       | WD800JD-00JNA0     | 80 GB  | 2       | 809   | 5     | 0.37   |
| WDC       | WD10SPZX-22Z10T1   | 1 TB   | 7       | 134   | 0     | 0.37   |
| Toshiba   | MQ01ABD050V        | 500 GB | 2       | 134   | 0     | 0.37   |
| WDC       | WD3201ABYS-01B9A0  | 320 GB | 2       | 926   | 278   | 0.37   |
| WDC       | WD3200AAKX-073CA1  | 320 GB | 2       | 342   | 4     | 0.37   |
| WDC       | WD3200AAJS-56M0A0  | 320 GB | 12      | 496   | 4     | 0.37   |
| WDC       | WD1600JD-00HBB0    | 160 GB | 6       | 582   | 17    | 0.37   |
| Seagate   | ST320DM001 HD322GJ | 320 GB | 5       | 477   | 88    | 0.37   |
| Toshiba   | MK2565GSX          | 250 GB | 26      | 334   | 189   | 0.37   |
| Seagate   | ST1000VX005-2EZ102 | 1 TB   | 4       | 132   | 0     | 0.36   |
| HGST      | HUH721212ALE604    | 12 TB  | 3       | 131   | 0     | 0.36   |
| WDC       | WD5000AZLX-08K2TA0 | 500 GB | 22      | 131   | 0     | 0.36   |
| Toshiba   | HDWJ110            | 1 TB   | 5       | 187   | 227   | 0.36   |
| IBM/Hi... | IC35L040AVER07-0   | 41 GB  | 2       | 1050  | 7     | 0.36   |
| Seagate   | ST500LT032-1E9142  | 500 GB | 1       | 131   | 0     | 0.36   |
| Seagate   | ST3120811AS        | 120 GB | 14      | 572   | 369   | 0.36   |
| Seagate   | ST1500DM003-9YN16G | 1.5 TB | 17      | 452   | 462   | 0.36   |
| WDC       | WD5000AZLX-35K2TA0 | 500 GB | 2       | 130   | 0     | 0.36   |
| Seagate   | ST500DM002-1SB10A  | 500 GB | 27      | 168   | 2     | 0.36   |
| Seagate   | ST10000DM0004-2... | 10 TB  | 3       | 129   | 0     | 0.36   |
| WDC       | WD5000LPCX-21VHAT0 | 500 GB | 63      | 137   | 1     | 0.36   |
| Seagate   | ST9120822A         | 120 GB | 2       | 273   | 53    | 0.36   |
| WDC       | WD5000LPCX-24VHAT0 | 500 GB | 73      | 134   | 16    | 0.36   |
| Toshiba   | DT01ACA100 LENOVO  | 1 TB   | 3       | 128   | 0     | 0.35   |
| WDC       | WD5000AADS-56S9B1  | 500 GB | 6       | 710   | 6     | 0.35   |
| WDC       | WD10EADS-98M2B0    | 1 TB   | 1       | 899   | 6     | 0.35   |
| WDC       | WD800JD-22LSA1     | 80 GB  | 4       | 485   | 174   | 0.35   |
| Samsung   | HM500JJ            | 500 GB | 2       | 331   | 5     | 0.35   |
| Hitachi   | HTS545050B9SA00    | 500 GB | 7       | 816   | 722   | 0.35   |
| Toshiba   | MK2552GSX          | 250 GB | 14      | 906   | 182   | 0.35   |
| Toshiba   | MK1034GSX          | 100 GB | 4       | 418   | 464   | 0.35   |
| Seagate   | ST500DM009-2F110A  | 500 GB | 22      | 135   | 28    | 0.35   |
| Toshiba   | MK8046GSX          | 80 GB  | 4       | 500   | 4     | 0.35   |
| Seagate   | ST500DM002-9YN14C  | 500 GB | 3       | 464   | 339   | 0.35   |
| WDC       | WD1600AAJS-56M0A0  | 160 GB | 2       | 469   | 4     | 0.35   |
| WDC       | WD1600BEVT-80A23T0 | 160 GB | 23      | 205   | 110   | 0.35   |
| Seagate   | ST1000VX000-1ES162 | 1 TB   | 16      | 126   | 0     | 0.35   |
| WDC       | WD5000BPVT-55A1YT0 | 500 GB | 1       | 126   | 0     | 0.35   |
| WDC       | WD1600BEVT-75A23T0 | 160 GB | 4       | 215   | 1     | 0.35   |
| Seagate   | ST3500830SCE       | 500 GB | 1       | 126   | 0     | 0.35   |
| ExcelStor | J8080S             | 82 GB  | 1       | 2405  | 18    | 0.35   |
| Toshiba   | HDWM110            | 1 TB   | 3       | 126   | 0     | 0.35   |
| WDC       | WD3200BEVT-26ZCT0  | 320 GB | 4       | 160   | 1     | 0.35   |
| WDC       | WD1600BEKT-60A25T1 | 160 GB | 2       | 145   | 1     | 0.34   |
| Toshiba   | MK1216GSG          | 120 GB | 3       | 272   | 4     | 0.34   |
| Seagate   | ST500LT015-1DJ142  | 500 GB | 1       | 124   | 0     | 0.34   |
| Toshiba   | MQ01ABD064         | 640 GB | 1       | 124   | 0     | 0.34   |
| Samsung   | MP0402H            | 40 GB  | 6       | 330   | 25    | 0.34   |
| WDC       | WD3200AAKS-00C9A0  | 320 GB | 3       | 1080  | 8     | 0.34   |
| Toshiba   | DT01ACA200V        | 2 TB   | 1       | 124   | 0     | 0.34   |
| WDC       | WD1600HLHX-60JJPV1 | 160 GB | 1       | 617   | 4     | 0.34   |
| Hitachi   | HTS541010A9E680    | 1 TB   | 15      | 509   | 769   | 0.34   |
| Seagate   | ST3000DM007-1WY10G | 3 TB   | 7       | 123   | 0     | 0.34   |
| Toshiba   | HDWK105            | 500 GB | 6       | 123   | 0     | 0.34   |
| WDC       | WD8000AARS-00Y5B1  | 800 GB | 3       | 1740  | 14    | 0.34   |
| Seagate   | ST9160821AS        | 160 GB | 59      | 438   | 582   | 0.34   |
| WDC       | WD10EZEX-75WN4A0   | 1 TB   | 24      | 189   | 69    | 0.34   |
| Hitachi   | HTS541660J9SA00    | 64 GB  | 4       | 443   | 7     | 0.34   |
| Samsung   | HM321HX            | 320 GB | 3       | 176   | 3     | 0.34   |
| WDC       | WD4005FZBX-00K5WB0 | 4 TB   | 5       | 122   | 0     | 0.34   |
| Seagate   | ST9500325AS        | 500 GB | 377     | 468   | 579   | 0.34   |
| WDC       | WD5000LPVX-00V0TT0 | 500 GB | 19      | 168   | 123   | 0.34   |
| Toshiba   | MK7559GSXF         | 752 GB | 4       | 178   | 319   | 0.33   |
| Hitachi   | HTS541010G9SA00    | 100 GB | 14      | 377   | 82    | 0.33   |
| Samsung   | SP2004C            | 200 GB | 28      | 664   | 490   | 0.33   |
| Seagate   | ST1000LM035-1RK172 | 1 TB   | 292     | 144   | 97    | 0.33   |
| Samsung   | HN-M101MBB         | 1 TB   | 18      | 394   | 306   | 0.33   |
| Seagate   | ST1000LX015-1U7172 | 1 TB   | 46      | 129   | 25    | 0.33   |
| WDC       | WD2500BEVE-00A0HT0 | 250 GB | 2       | 120   | 0     | 0.33   |
| HGST      | HTE721010A9E630    | 1 TB   | 5       | 120   | 0     | 0.33   |
| Seagate   | ST9100827AS        | 100 GB | 1       | 838   | 6     | 0.33   |
| WDC       | WD5001AALS-00J7B1  | 500 GB | 1       | 1077  | 8     | 0.33   |
| Seagate   | ST910021AS         | 100 GB | 6       | 552   | 547   | 0.33   |
| WDC       | WD5000LPLX-08ZNTT0 | 500 GB | 13      | 187   | 1     | 0.33   |
| Seagate   | ST960821A          | 64 GB  | 1       | 358   | 2     | 0.33   |
| Toshiba   | MK6025GAS          | 64 GB  | 2       | 166   | 9     | 0.33   |
| WDC       | WD20PURZ-85GU6Y0   | 2 TB   | 12      | 224   | 165   | 0.33   |
| Toshiba   | MK2556GSY          | 250 GB | 5       | 239   | 436   | 0.32   |
| WDC       | WD3200AVJS-63B6A0  | 320 GB | 6       | 1126  | 20    | 0.32   |
| WDC       | WD10EURX-73FH1Y0   | 1 TB   | 4       | 370   | 2     | 0.32   |
| WDC       | WD10SPZX-17Z10T1   | 1 TB   | 3       | 117   | 0     | 0.32   |
| WDC       | WD5000BPVT-08HXZT1 | 500 GB | 1       | 117   | 0     | 0.32   |
| WDC       | WD5000AAKS-00M9A0  | 500 GB | 5       | 695   | 457   | 0.32   |
| Toshiba   | MQ01ACF050         | 500 GB | 24      | 176   | 99    | 0.32   |
| Seagate   | ST1000LM025 HN-... | 1 TB   | 21      | 121   | 1     | 0.32   |
| Toshiba   | MK7575GSX          | 752 GB | 20      | 566   | 620   | 0.32   |
| Seagate   | ST9250315AS        | 250 GB | 189     | 464   | 450   | 0.32   |
| HGST      | HTS541050A9E680    | 500 GB | 5       | 116   | 0     | 0.32   |
| WDC       | 500GB              | 500 GB | 1       | 1047  | 8     | 0.32   |
| Seagate   | ST4000VX007-2DT166 | 4 TB   | 5       | 116   | 0     | 0.32   |
| Toshiba   | MK5055GSX          | 500 GB | 13      | 490   | 136   | 0.32   |
| Toshiba   | MK2546GSX          | 250 GB | 12      | 520   | 41    | 0.32   |
| Hitachi   | HTS541680J9SA00    | 80 GB  | 52      | 492   | 77    | 0.32   |
| WDC       | WD5000LPLX-22ZNTT0 | 500 GB | 9       | 115   | 0     | 0.32   |
| WDC       | WD5000BPVT-60HXZT3 | 500 GB | 11      | 471   | 141   | 0.32   |
| WDC       | WD10EZEX-00MFCA0   | 1 TB   | 14      | 140   | 4     | 0.32   |
| Toshiba   | MK3259GSXP         | 320 GB | 52      | 340   | 177   | 0.31   |
| Seagate   | ST1000LM010-9YH146 | 1 TB   | 10      | 217   | 819   | 0.31   |
| WDC       | WD10JPVX-08JC3T6   | 1 TB   | 3       | 114   | 0     | 0.31   |
| WDC       | WD2500BPVT-75JJ5T0 | 250 GB | 4       | 214   | 1     | 0.31   |
| Seagate   | ST500LM000-SSHD... | 500 GB | 25      | 274   | 224   | 0.31   |
| Hitachi   | HTS541612J9SA00    | 120 GB | 64      | 532   | 69    | 0.31   |
| HGST      | HUH721212ALE600    | 12 TB  | 2       | 113   | 0     | 0.31   |
| WDC       | WD10EZEX-07M2NA0   | 1 TB   | 2       | 773   | 9     | 0.31   |
| WDC       | WD3200AAKS-00YGA0  | 320 GB | 1       | 562   | 4     | 0.31   |
| Seagate   | ST9100824AS        | 100 GB | 5       | 351   | 7     | 0.31   |
| Seagate   | ST9100823A         | 96 GB  | 1       | 1007  | 8     | 0.31   |
| Seagate   | ST340810A          | 40 GB  | 10      | 526   | 32    | 0.31   |
| WDC       | WD1200BEVS-60UST0  | 120 GB | 11      | 397   | 328   | 0.30   |
| WDC       | WD5000BEVT-22ZAT0  | 500 GB | 10      | 457   | 19    | 0.30   |
| WDC       | WD20SMZW-11JW8S1   | 2 TB   | 1       | 111   | 0     | 0.30   |
| WDC       | WD400JB-00FMA0     | 40 GB  | 2       | 656   | 8     | 0.30   |
| WDC       | WD50NMZW-59LG6S1   | 5 TB   | 1       | 110   | 0     | 0.30   |
| WDC       | WD7500BPVT-00HXZT3 | 752 GB | 8       | 512   | 11    | 0.30   |
| Fujitsu   | MHW2020BH          | 20 GB  | 2       | 109   | 0     | 0.30   |
| WDC       | WD20SPZX-22UA7T0   | 2 TB   | 7       | 109   | 0     | 0.30   |
| Toshiba   | MK3265GSX          | 320 GB | 57      | 590   | 235   | 0.30   |
| WDC       | WD3000FYYZ-01UL1B0 | 3 TB   | 2       | 109   | 0     | 0.30   |
| WDC       | WD3200BEKT-00V5T0  | 320 GB | 1       | 109   | 0     | 0.30   |
| WDC       | WD20EADS-32S2B0    | 2 TB   | 1       | 1198  | 10    | 0.30   |
| HGST      | HUS726060ALE614    | 6 TB   | 5       | 158   | 113   | 0.30   |
| Seagate   | ST8000NM000A-2K... | 8 TB   | 1       | 108   | 0     | 0.30   |
| WDC       | WD5000LPLX-00ZNTT0 | 500 GB | 47      | 114   | 1     | 0.30   |
| Toshiba   | HDWN160            | 6 TB   | 7       | 303   | 25    | 0.30   |
| Seagate   | ST9160823AS        | 160 GB | 6       | 886   | 558   | 0.30   |
| HGST      | HDS5C4040ALE630    | 4 TB   | 1       | 107   | 0     | 0.29   |
| Fujitsu   | MHW2040BH          | 40 GB  | 1       | 214   | 1     | 0.29   |
| WDC       | WD3200BEVT-88ZCT0  | 320 GB | 1       | 106   | 0     | 0.29   |
| Hitachi   | HTS542520K9SA00    | 200 GB | 4       | 658   | 11    | 0.29   |
| WDC       | WD3000FYYZ-01UL1B1 | 3 TB   | 1       | 1381  | 12    | 0.29   |
| China     | TP00250GB          | 250 GB | 1       | 106   | 0     | 0.29   |
| WDC       | WD50EFRX-68MYMN1   | 5 TB   | 3       | 518   | 3     | 0.29   |
| WDC       | WD20EARS-22MVWB0   | 2 TB   | 2       | 1600  | 13    | 0.29   |
| Seagate   | ST9120821AS        | 120 GB | 6       | 288   | 1086  | 0.29   |
| Seagate   | ST2000LM005 HN-... | 2 TB   | 2       | 104   | 0     | 0.29   |
| WDC       | WD3200BPVT-35JJ5T0 | 320 GB | 1       | 104   | 0     | 0.29   |
| Seagate   | ST3500412AS        | 500 GB | 23      | 792   | 498   | 0.29   |
| WDC       | WD5000BEVT-80A0RT0 | 500 GB | 2       | 948   | 9     | 0.29   |
| Seagate   | ST320LT012-1DG14C  | 320 GB | 18      | 201   | 64    | 0.28   |
| Seagate   | ST980811AS         | 80 GB  | 23      | 422   | 477   | 0.28   |
| Toshiba   | MK6006GAH          | 64 GB  | 1       | 103   | 0     | 0.28   |
| WDC       | WD5000AAKX-19U6AA0 | 500 GB | 1       | 103   | 0     | 0.28   |
| WDC       | WD60EZAZ-00ZGHB0   | 6 TB   | 6       | 103   | 0     | 0.28   |
| WDC       | WD2500BEVT-75A23T0 | 250 GB | 6       | 589   | 12    | 0.28   |
| WDC       | WD1600BEVT-60ZCT0  | 160 GB | 5       | 203   | 403   | 0.28   |
| Seagate   | ST3160812AS 41N... | 160 GB | 3       | 729   | 28    | 0.28   |
| Hitachi   | HTS541080G9AT00    | 80 GB  | 13      | 481   | 86    | 0.28   |
| WDC       | WD5000BMVW-11AJGS4 | 500 GB | 4       | 106   | 141   | 0.28   |
| Hitachi   | HTS721060G9SA00    | 64 GB  | 3       | 664   | 13    | 0.28   |
| Fujitsu   | MHT2040AH PL       | 40 GB  | 1       | 306   | 2     | 0.28   |
| WDC       | WD1600AAJS-60Z0A0  | 160 GB | 4       | 272   | 262   | 0.28   |
| Toshiba   | MK3252GSX          | 320 GB | 22      | 594   | 185   | 0.28   |
| Toshiba   | MK7559GSXP         | 752 GB | 21      | 419   | 544   | 0.28   |
| WDC       | WD20EARS-00J2GB0   | 2 TB   | 2       | 914   | 8     | 0.28   |
| WDC       | WD10EZRX-22A3KB0   | 1 TB   | 1       | 101   | 0     | 0.28   |
| Samsung   | SP1604N            | 160 GB | 3       | 394   | 62    | 0.28   |
| WDC       | WD10SPZX-35Z10T0   | 1 TB   | 3       | 101   | 0     | 0.28   |
| WDC       | WD20SPZX-75UA7T0   | 2 TB   | 1       | 101   | 0     | 0.28   |
| WDC       | WD3202ABYS-01B7A0  | 320 GB | 3       | 581   | 5     | 0.28   |
| WDC       | WD30PURZ-85GU6Y0   | 3 TB   | 2       | 101   | 0     | 0.28   |
| WDC       | WD120EMAZ-11BLFA0  | 12 TB  | 3       | 100   | 0     | 0.28   |
| WDC       | WD80EZAZ-11TDBA0   | 8 TB   | 13      | 100   | 0     | 0.28   |
| WDC       | WD10EADS-65P6B0    | 1 TB   | 1       | 907   | 8     | 0.28   |
| Seagate   | OOS3000G           | 3 TB   | 1       | 100   | 0     | 0.28   |
| WDC       | WD5000HHTZ-04N21V1 | 500 GB | 1       | 100   | 0     | 0.27   |
| WDC       | WD10SPCX-75HWST0   | 1 TB   | 1       | 100   | 0     | 0.27   |
| WDC       | WD7500AARS-003BB1  | 752 GB | 1       | 894   | 8     | 0.27   |
| HGST      | HTE725032A7E630    | 320 GB | 1       | 99    | 0     | 0.27   |
| Seagate   | ST2000DM008-2FR102 | 2 TB   | 91      | 109   | 14    | 0.27   |
| Seagate   | ST320LT020-9YG142  | 320 GB | 135     | 350   | 614   | 0.27   |
| WDC       | WD5000BEVT-60ZAT1  | 500 GB | 6       | 479   | 192   | 0.27   |
| WDC       | WD3200BEVT-75ZCT0  | 320 GB | 2       | 839   | 86    | 0.27   |
| WDC       | WD3200BEVT-22A0RT0 | 320 GB | 4       | 174   | 4     | 0.27   |
| HGST      | HTS545050A7E660    | 500 GB | 13      | 217   | 5     | 0.27   |
| WDC       | WD2500BEVT-00ZCT0  | 250 GB | 7       | 97    | 0     | 0.27   |
| Toshiba   | HDWU130            | 3 TB   | 1       | 97    | 0     | 0.27   |
| Toshiba   | MG04ACA200E        | 2 TB   | 3       | 105   | 3     | 0.27   |
| Toshiba   | MK2046GSX          | 200 GB | 11      | 401   | 42    | 0.27   |
| Seagate   | ST2000VN004-2E4164 | 2 TB   | 3       | 97    | 0     | 0.27   |
| Seagate   | ST9160314AS        | 160 GB | 37      | 293   | 231   | 0.27   |
| Toshiba   | MQ04UBD200         | 2 TB   | 6       | 135   | 4     | 0.27   |
| WDC       | WD1600AAJS-65WAA0  | 160 GB | 2       | 928   | 1006  | 0.27   |
| Seagate   | ST380023A          | 80 GB  | 1       | 2897  | 29    | 0.26   |
| WDC       | WD7500BPVT-22HXZT1 | 752 GB | 4       | 834   | 260   | 0.26   |
| WDC       | WD1200BEVS-60RST0  | 120 GB | 1       | 766   | 7     | 0.26   |
| Toshiba   | MQ01ABF050M        | 500 GB | 10      | 95    | 0     | 0.26   |
| Samsung   | SP0401N            | 40 GB  | 1       | 95    | 0     | 0.26   |
| Seagate   | ST500LM030-2E717D  | 500 GB | 29      | 107   | 4     | 0.26   |
| WDC       | WD5000LPCX-60VHAT0 | 500 GB | 30      | 107   | 1     | 0.26   |
| Toshiba   | MK1637GSX          | 160 GB | 31      | 567   | 71    | 0.26   |
| Seagate   | ST1000UM000-1EK164 | 1 TB   | 1       | 94    | 0     | 0.26   |
| HGST      | HTS545050A7E680    | 500 GB | 245     | 223   | 368   | 0.26   |
| Toshiba   | MK1665GSX H        | 160 GB | 1       | 93    | 0     | 0.26   |
| WDC       | WD400BB-60DGA0     | 40 GB  | 3       | 219   | 1     | 0.26   |
| Seagate   | ST320VM001-1AD142  | 320 GB | 2       | 93    | 0     | 0.26   |
| WDC       | WD3200BEVT-00A23T0 | 320 GB | 3       | 146   | 9     | 0.26   |
| WDC       | WD50NDZW-11MR8S1   | 5 TB   | 5       | 92    | 0     | 0.25   |
| WDC       | WD40PURX-64NZ6Y0   | 4 TB   | 1       | 92    | 0     | 0.25   |
| WDC       | WD2500JS-19NCB1    | 250 GB | 1       | 92    | 0     | 0.25   |
| WDC       | WD140EFFX-68VBXN0  | 14 TB  | 2       | 92    | 0     | 0.25   |
| Hitachi   | HDS5C4040ALE630    | 4 TB   | 1       | 91    | 0     | 0.25   |
| Fujitsu   | MJA2500BH G2       | 500 GB | 10      | 281   | 117   | 0.25   |
| WDC       | WD5000AZLX-21K2TA0 | 500 GB | 3       | 91    | 0     | 0.25   |
| WDC       | WD1600BPVT-22JJ5T0 | 160 GB | 1       | 91    | 0     | 0.25   |
| WDC       | WD7500AAVS-00D7B1  | 752 GB | 1       | 2278  | 24    | 0.25   |
| WDC       | WD10SPZX-08Z10     | 1 TB   | 13      | 90    | 0     | 0.25   |
| WDC       | WD1600AAJS-61M0A0  | 160 GB | 1       | 90    | 0     | 0.25   |
| HP        | GB0250EAFJF        | 250 GB | 1       | 634   | 6     | 0.25   |
| Toshiba   | MK3276GSX -63      | 320 GB | 6       | 254   | 22    | 0.25   |
| Seagate   | ST9500325ASG       | 500 GB | 4       | 369   | 429   | 0.25   |
| Seagate   | ST31000340SV       | 1 TB   | 1       | 1616  | 17    | 0.25   |
| Hitachi   | HTS541616J9AT00    | 160 GB | 2       | 356   | 7     | 0.25   |
| Samsung   | HS082HB            | 80 GB  | 1       | 89    | 0     | 0.25   |
| Seagate   | ST320LT022-1AE142  | 320 GB | 2       | 170   | 2     | 0.25   |
| Fujitsu   | MHW2040AT          | 40 GB  | 1       | 88    | 0     | 0.24   |
| WDC       | WD3200AAKX-753CA1  | 320 GB | 2       | 221   | 4     | 0.24   |
| WDC       | WD20NPVZ-00WFZT0   | 2 TB   | 4       | 88    | 0     | 0.24   |
| Seagate   | ST3320613AS        | 320 GB | 93      | 867   | 271   | 0.24   |
| Toshiba   | MQ02ABF050H        | 500 GB | 1       | 88    | 0     | 0.24   |
| WDC       | WD20SMZW-11JW8S0   | 2 TB   | 5       | 87    | 0     | 0.24   |
| WDC       | WD120EDAZ-11F3RA0  | 12 TB  | 2       | 87    | 0     | 0.24   |
| Hitachi   | HDP725016GLA380    | 160 GB | 7       | 596   | 224   | 0.24   |
| WDC       | WD1600JS-61MHB1    | 160 GB | 1       | 959   | 10    | 0.24   |
| Toshiba   | MK1246GSX          | 120 GB | 16      | 405   | 84    | 0.24   |
| Hitachi   | HTS725032A9A364    | 320 GB | 20      | 452   | 888   | 0.24   |
| WDC       | WD2000JB-22GVA0    | 200 GB | 1       | 694   | 7     | 0.24   |
| Samsung   | SP1213C            | 120 GB | 6       | 609   | 37    | 0.24   |
| Toshiba   | MK5065GSX          | 500 GB | 24      | 325   | 311   | 0.24   |
| WDC       | WD1200BEVS-22LAT0  | 120 GB | 1       | 86    | 0     | 0.24   |
| WDC       | WD1600BEVT-00A1TT0 | 160 GB | 2       | 273   | 3     | 0.24   |
| HGST      | HTS545032A7E380    | 320 GB | 32      | 193   | 510   | 0.24   |
| Seagate   | ST9320320AS        | 320 GB | 21      | 686   | 168   | 0.23   |
| WDC       | WD5000AAKS-07A7B2  | 500 GB | 1       | 1709  | 19    | 0.23   |
| Seagate   | ST10000DM0004-1... | 10 TB  | 3       | 211   | 3     | 0.23   |
| WDC       | WD5000AZLX-60K2TA1 | 500 GB | 1       | 84    | 0     | 0.23   |
| WDC       | WD10SPZX-21Z10T0   | 1 TB   | 57      | 84    | 1     | 0.23   |
| Samsung   | HD300LD            | 304 GB | 4       | 554   | 15    | 0.23   |
| WDC       | WD60PURX-64T0ZY0   | 6 TB   | 2       | 83    | 0     | 0.23   |
| Toshiba   | MK8032GAX          | 80 GB  | 2       | 117   | 252   | 0.23   |
| HGST      | HUS726T4TALN6L4    | 4 TB   | 1       | 83    | 0     | 0.23   |
| Seagate   | ST3400620NS        | 400 GB | 2       | 1825  | 21    | 0.23   |
| Hitachi   | HTS542512K9A300    | 120 GB | 7       | 403   | 151   | 0.23   |
| Toshiba   | MK3021GAS          | 32 GB  | 1       | 495   | 5     | 0.23   |
| WDC       | WD5000AACS-00G8B0  | 500 GB | 6       | 788   | 10    | 0.23   |
| WDC       | WD2500AAKX-193CA0  | 250 GB | 1       | 82    | 0     | 0.23   |
| Seagate   | ST9250410ASG       | 250 GB | 1       | 409   | 4     | 0.22   |
| WDC       | WD1600JD-41HBC0    | 160 GB | 1       | 1884  | 22    | 0.22   |
| IBM/Hi... | IC35L060AVV207-0   | 40 GB  | 1       | 326   | 3     | 0.22   |
| WDC       | WD2500BPVT-22JJ5T0 | 250 GB | 9       | 257   | 218   | 0.22   |
| WDC       | WD5000AAKS-00H2B0  | 499 GB | 1       | 731   | 8     | 0.22   |
| Fujitsu   | MHT2080BH          | 80 GB  | 2       | 543   | 10    | 0.22   |
| WDC       | WD6400AAKS-75A7B0  | 640 GB | 2       | 208   | 2     | 0.22   |
| Seagate   | ST3250820AV        | 250 GB | 1       | 80    | 0     | 0.22   |
| WDC       | WD10J31X-00U3VT0   | 1 TB   | 1       | 80    | 0     | 0.22   |
| WDC       | WD10SPZX-22Z10T0   | 1 TB   | 9       | 80    | 0     | 0.22   |
| Toshiba   | MD04ACA500         | 5 TB   | 3       | 243   | 6     | 0.22   |
| Fujitsu   | MHV2100BH PL       | 100 GB | 4       | 218   | 3     | 0.22   |
| Magnet... | MD03200-AJDW-RO    | 320 GB | 1       | 79    | 0     | 0.22   |
| WDC       | WD10SPZX-75Z10T2   | 1 TB   | 22      | 79    | 0     | 0.22   |
| WDC       | WD600BEVS-07LAT0   | 64 GB  | 1       | 635   | 7     | 0.22   |
| WDC       | WD400BB-75JHC0     | 40 GB  | 1       | 476   | 5     | 0.22   |
| WDC       | WD5000LPCX-75VHAT0 | 500 GB | 11      | 79    | 0     | 0.22   |
| Samsung   | HD252KJ            | 250 GB | 9       | 802   | 459   | 0.22   |
| WDC       | WD3200BUCT-63TWBY0 | 320 GB | 2       | 79    | 0     | 0.22   |
| Toshiba   | MK5065GSXN         | 500 GB | 10      | 430   | 724   | 0.22   |
| Hitachi   | HTS542525K9A300    | 250 GB | 6       | 666   | 545   | 0.22   |
| Toshiba   | MQ01ABD050V -63    | 500 GB | 2       | 78    | 0     | 0.21   |
| Seagate   | ST500LM034-2GH17A  | 500 GB | 7       | 78    | 0     | 0.21   |
| Toshiba   | MK1633GSG          | 160 GB | 3       | 299   | 343   | 0.21   |
| WDC       | WD5000AZRX-00A3KB0 | 500 GB | 3       | 114   | 3     | 0.21   |
| WDC       | WD7500BPVT-60HXZT1 | 752 GB | 4       | 557   | 44    | 0.21   |
| WDC       | WD10EZRZ-22HTKB0   | 1 TB   | 6       | 77    | 0     | 0.21   |
| WDC       | WD7500LPCX-60KHST0 | 752 GB | 3       | 77    | 0     | 0.21   |
| Seagate   | ST9120823ASG       | 120 GB | 1       | 76    | 0     | 0.21   |
| WDC       | WD10SPCX-60KHST0   | 1 TB   | 1       | 230   | 2     | 0.21   |
| Seagate   | ST8000DM0004-1Z... | 8 TB   | 1       | 76    | 0     | 0.21   |
| Fujitsu   | MHV2060BH PL       | 64 GB  | 3       | 76    | 3     | 0.21   |
| Samsung   | SP1614C            | 160 GB | 6       | 449   | 15    | 0.21   |
| Hitachi   | HTS722016K9A300    | 160 GB | 3       | 222   | 344   | 0.21   |
| Toshiba   | MK1237GSX          | 120 GB | 16      | 421   | 159   | 0.21   |
| Fujitsu   | MHV2060AT PL       | 64 GB  | 3       | 851   | 16    | 0.21   |
| Toshiba   | HDWL120            | 2 TB   | 7       | 75    | 0     | 0.21   |
| WDC       | WD2502ABYS-50B7A1  | 250 GB | 1       | 1290  | 16    | 0.21   |
| HGST      | HUS728T8TALE6L4    | 8 TB   | 1       | 75    | 0     | 0.21   |
| Seagate   | ST10000NM0086-2... | 10 TB  | 5       | 75    | 0     | 0.21   |
| Toshiba   | MQ04ABF100         | 1 TB   | 122     | 86    | 13    | 0.21   |
| Hitachi   | HTS543280L9A300    | 80 GB  | 2       | 99    | 1     | 0.21   |
| WDC       | WD1004FBYZ-01YCBB1 | 1 TB   | 1       | 75    | 0     | 0.21   |
| Toshiba   | MK6476GSXN         | 640 GB | 3       | 122   | 601   | 0.21   |
| Toshiba   | MK1252GSX          | 120 GB | 8       | 435   | 113   | 0.20   |
| WDC       | WD400VE-07HDT0     | 40 GB  | 1       | 74    | 0     | 0.20   |
| WDC       | WD15NMVW-11AV3S3   | 1.5 TB | 1       | 743   | 9     | 0.20   |
| Samsung   | HN-M750MBB         | 752 GB | 5       | 299   | 11    | 0.20   |
| WDC       | WD800VE-75HDT1     | 80 GB  | 1       | 369   | 4     | 0.20   |
| Hitachi   | HTS722020K9SA00    | 200 GB | 4       | 609   | 8     | 0.20   |
| Seagate   | ST9160310AS        | 160 GB | 36      | 274   | 182   | 0.20   |
| Hitachi   | HTS543232L9SA00    | 320 GB | 9       | 417   | 103   | 0.20   |
| Hitachi   | HDE721050SLA330    | 500 GB | 1       | 2416  | 32    | 0.20   |
| WDC       | WD1500BLHX-01V7BV0 | 150 GB | 1       | 72    | 0     | 0.20   |
| Fujitsu   | MHV2080BH PL       | 80 GB  | 16      | 136   | 3     | 0.20   |
| WDC       | WD1600SD-01KCC0    | 160 GB | 1       | 2914  | 39    | 0.20   |
| Fujitsu   | MHZ2320BH G2       | 320 GB | 11      | 453   | 436   | 0.20   |
| WDC       | WD10JMVW-11S5XS1   | 1 TB   | 1       | 72    | 0     | 0.20   |
| Seagate   | ST9120411ASG       | 120 GB | 1       | 361   | 4     | 0.20   |
| WDC       | WD5000AVVS-63H0B1  | 500 GB | 1       | 144   | 1     | 0.20   |
| WDC       | WD10SPZX-00Z10T0   | 1 TB   | 13      | 72    | 0     | 0.20   |
| WDC       | WD20NMVW-11AV3S4   | 2 TB   | 2       | 751   | 512   | 0.20   |
| HP        | MB1000EAMZE        | 1 TB   | 1       | 1919  | 26    | 0.19   |
| Seagate   | ST1000LM049-2GH172 | 1 TB   | 65      | 80    | 17    | 0.19   |
| Toshiba   | HDWQ140            | 4 TB   | 4       | 168   | 1     | 0.19   |
| Seagate   | ST31000322CS       | 1 TB   | 3       | 935   | 34    | 0.19   |
| Hitachi   | HTS545032B9A302    | 320 GB | 3       | 179   | 9     | 0.19   |
| IBM       | DTLA-307015        | 16 GB  | 1       | 423   | 5     | 0.19   |
| WDC       | WD3200AAJS-60M0A1  | 320 GB | 5       | 837   | 965   | 0.19   |
| Hitachi   | HTS543225L9SA00    | 250 GB | 6       | 507   | 35    | 0.19   |
| HGST      | HTE725050A7E630    | 500 GB | 2       | 68    | 0     | 0.19   |
| WDC       | WD2500AAJS-22L7A0  | 250 GB | 3       | 625   | 9     | 0.19   |
| WDC       | WD3200BPVT-00HXZT1 | 320 GB | 6       | 408   | 174   | 0.19   |
| Toshiba   | MK1011GAH          | 100 GB | 5       | 319   | 8     | 0.19   |
| Seagate   | ST91608220AS       | 160 GB | 1       | 135   | 1     | 0.19   |
| Seagate   | ST3750330AS        | 752 GB | 12      | 1160  | 301   | 0.19   |
| Hitachi   | HDT721050SLA360    | 500 GB | 3       | 1119  | 64    | 0.19   |
| Toshiba   | MK6465GSX          | 640 GB | 25      | 646   | 686   | 0.19   |
| WDC       | WD10SPZX-75Z10T3   | 1 TB   | 9       | 67    | 0     | 0.18   |
| WDC       | WD800BB-55JKC0     | 80 GB  | 8       | 588   | 119   | 0.18   |
| WDC       | WD200BB-60CJA0     | 20 GB  | 1       | 1417  | 20    | 0.18   |
| WDC       | WD3200JS-22PDB0    | 320 GB | 1       | 1538  | 22    | 0.18   |
| Seagate   | ST3402111A         | 40 GB  | 2       | 117   | 36    | 0.18   |
| WDC       | WD5000LPLX-60ZNTT1 | 500 GB | 9       | 145   | 36    | 0.18   |
| Maxtor    | STM3160811AS       | 160 GB | 6       | 687   | 266   | 0.18   |
| Toshiba   | MQ02ABF100         | 1 TB   | 3       | 105   | 1     | 0.18   |
| HGST      | HCC545050A7E630    | 500 GB | 2       | 66    | 0     | 0.18   |
| HGST      | HTS545050B7E660    | 500 GB | 17      | 65    | 0     | 0.18   |
| Toshiba   | MK3263GSXN         | 320 GB | 8       | 590   | 25    | 0.18   |
| WDC       | WD30EZRX-22D8PB0   | 3 TB   | 1       | 65    | 0     | 0.18   |
| WDC       | WD1600AAJS         | 160 GB | 1       | 65    | 0     | 0.18   |
| WDC       | WD2500AAJS-60VWA1  | 250 GB | 1       | 65    | 0     | 0.18   |
| Seagate   | ST640LM001 HN-M... | 640 GB | 2       | 467   | 27    | 0.18   |
| Seagate   | ST9120817AS        | 120 GB | 6       | 450   | 566   | 0.18   |
| Toshiba   | MK8025GAS          | 80 GB  | 2       | 75    | 29    | 0.18   |
| Fujitsu   | MJA2250BH G2       | 250 GB | 7       | 237   | 151   | 0.17   |
| WDC       | WD3200AAJS-08B4A0  | 320 GB | 1       | 695   | 10    | 0.17   |
| WDC       | WD5000LPVX-16V0TT3 | 500 GB | 2       | 62    | 0     | 0.17   |
| WDC       | WD5000BPKT-80PK4T0 | 500 GB | 1       | 563   | 8     | 0.17   |
| WDC       | WD20SPZX-08UA7     | 2 TB   | 3       | 62    | 0     | 0.17   |
| WDC       | WD3200AVJS-63TBA0  | 320 GB | 1       | 311   | 4     | 0.17   |
| WDC       | WD10EZRX-22L4HB0   | 1 TB   | 1       | 62    | 0     | 0.17   |
| WDC       | WD5000LPCX-08VHA   | 500 GB | 5       | 61    | 0     | 0.17   |
| WDC       | WD25EZRS-00J99B0   | 2.5 TB | 1       | 2353  | 37    | 0.17   |
| WDC       | WD7500BPVT-35HXZT3 | 752 GB | 1       | 309   | 4     | 0.17   |
| Maxtor    | 4K060H3            | 64 GB  | 1       | 927   | 14    | 0.17   |
| WDC       | WD3200BEKT-60F3T1  | 320 GB | 8       | 547   | 496   | 0.17   |
| Hitachi   | HTS725016A9A362    | 160 GB | 1       | 61    | 0     | 0.17   |
| WDC       | WD3200BEVT-60A23T0 | 320 GB | 18      | 274   | 345   | 0.17   |
| HGST      | HTS545025A7E330    | 250 GB | 1       | 60    | 0     | 0.17   |
| Fujitsu   | MHV2100AH PL       | 100 GB | 1       | 423   | 6     | 0.17   |
| WDC       | WD5000AAKS-60WWPA0 | 500 GB | 7       | 664   | 651   | 0.17   |
| Hitachi   | DK23FB-60          | 64 GB  | 1       | 960   | 15    | 0.16   |
| WDC       | WD2500AAJS-98B4A0  | 250 GB | 1       | 540   | 8     | 0.16   |
| IBM/Hi... | IC25N080ATMR04-0   | 80 GB  | 3       | 195   | 19    | 0.16   |
| WDC       | WD1600BB-22GUC0    | 160 GB | 1       | 898   | 14    | 0.16   |
| WDC       | WD10SPZX-80Z10T2   | 1 TB   | 5       | 59    | 0     | 0.16   |
| Samsung   | HM120JI            | 120 GB | 4       | 327   | 5     | 0.16   |
| Seagate   | ST380021A          | 80 GB  | 11      | 826   | 47    | 0.16   |
| WDC       | WD20SDRW-11VUUS0   | 2 TB   | 2       | 59    | 0     | 0.16   |
| WDC       | WD400EB-00CPF0     | 40 GB  | 4       | 677   | 63    | 0.16   |
| WDC       | WD3200AAJS-40VWA1  | 320 GB | 2       | 242   | 21    | 0.16   |
| WDC       | WD1600BEVE-00A0HT0 | 160 GB | 1       | 58    | 0     | 0.16   |
| WDC       | WD2000JB-00EVA0    | 200 GB | 1       | 5656  | 96    | 0.16   |
| WDC       | WD3200LPVT-22G33T0 | 320 GB | 1       | 58    | 0     | 0.16   |
| WDC       | WD10SPZX-24Z10     | 1 TB   | 50      | 58    | 0     | 0.16   |
| MediaMax  | WL250GPA872B       | 250 GB | 1       | 58    | 0     | 0.16   |
| WDC       | WD1600BEVT-08A23T1 | 160 GB | 1       | 57    | 0     | 0.16   |
| WDC       | WD10SPCX-21KHST0   | 1 TB   | 3       | 57    | 0     | 0.16   |
| Toshiba   | MK1665GSX          | 160 GB | 16      | 202   | 345   | 0.16   |
| Seagate   | ST9250311CS        | 250 GB | 1       | 2074  | 35    | 0.16   |
| Samsung   | HM502JX            | 500 GB | 2       | 57    | 0     | 0.16   |
| Samsung   | SP2014N            | 200 GB | 6       | 359   | 188   | 0.16   |
| Hitachi   | HTS421280H9AT00    | 80 GB  | 6       | 661   | 16    | 0.15   |
| WDC       | WD20EZRZ-60Z5HB0   | 2 TB   | 2       | 56    | 0     | 0.15   |
| WDC       | WD1002FBYS-01A6B0  | 1 TB   | 1       | 393   | 6     | 0.15   |
| Seagate   | ST3200826A         | 200 GB | 2       | 561   | 8     | 0.15   |
| WDC       | WD1500HLHX-01JJPV0 | 150 GB | 1       | 498   | 8     | 0.15   |
| WDC       | WD5000LPVX-55V0TT3 | 500 GB | 1       | 55    | 0     | 0.15   |
| Samsung   | SP2514N            | 250 GB | 8       | 669   | 669   | 0.15   |
| WDC       | WD10EALX-229BA1    | 1 TB   | 1       | 493   | 8     | 0.15   |
| WDC       | WD10TMVV-11BG7S0   | 1 TB   | 2       | 695   | 9     | 0.15   |
| Samsung   | HM060HC            | 52 GB  | 1       | 272   | 4     | 0.15   |
| Hitachi   | HTS541060G9SA00    | 64 GB  | 3       | 331   | 119   | 0.15   |
| Hitachi   | HDT725032VLAT80    | 320 GB | 4       | 1102  | 67    | 0.15   |
| WDC       | WD10EZEX-35M2NA0   | 1 TB   | 1       | 54    | 0     | 0.15   |
| WDC       | WD1600YS-23SHB0    | 160 GB | 1       | 53    | 0     | 0.15   |
| WDC       | WD10SPSX-00A6WT0   | 1 TB   | 1       | 53    | 0     | 0.15   |
| WDC       | WD5000LMVW-11VEDS3 | 500 GB | 3       | 193   | 366   | 0.15   |
| Toshiba   | MK6008GAH          | 64 GB  | 3       | 480   | 8     | 0.15   |
| WDC       | WD1600BEVS-00RST0  | 160 GB | 1       | 52    | 0     | 0.15   |
| WDC       | WD2500BEVT-22ZAT0  | 250 GB | 1       | 316   | 5     | 0.14   |
| Hitachi   | HTS541040G9SA00    | 40 GB  | 2       | 400   | 9     | 0.14   |
| Hitachi   | HTS424040M9AT00    | 40 GB  | 6       | 456   | 186   | 0.14   |
| Toshiba   | MK1629GSG          | 160 GB | 2       | 409   | 9     | 0.14   |
| Toshiba   | MK1646GSX          | 160 GB | 9       | 573   | 56    | 0.14   |
| WDC       | WD10JMVW-11AJGS0   | 1 TB   | 1       | 51    | 0     | 0.14   |
| WDC       | WD3200BEVT-60ZCT0  | 320 GB | 5       | 269   | 24    | 0.14   |
| WDC       | WD10EZEX-75WN4A1   | 1 TB   | 7       | 51    | 0     | 0.14   |
| Seagate   | ST31500341AS       | 1.5 TB | 65      | 806   | 303   | 0.14   |
| Toshiba   | MK1652GSX          | 160 GB | 18      | 380   | 60    | 0.14   |
| WDC       | WD2500AAJS-00YZCA0 | 250 GB | 4       | 442   | 61    | 0.14   |
| Samsung   | SP1213N            | 120 GB | 4       | 832   | 261   | 0.14   |
| HGST      | HTS541075A7E630    | 752 GB | 9       | 71    | 113   | 0.14   |
| WDC       | WD1600AAJB-56R1A0  | 160 GB | 2       | 152   | 4     | 0.14   |
| Seagate   | ST960812A          | 64 GB  | 1       | 151   | 2     | 0.14   |
| WDC       | WD6400BPVT-75HXZT3 | 640 GB | 1       | 50    | 0     | 0.14   |
| WDC       | WD360GD-00FLA2     | 37 GB  | 4       | 1259  | 29    | 0.14   |
| Seagate   | ST95000NSSUN500... | 500 GB | 1       | 2980  | 59    | 0.14   |
| WDC       | WD6400BPVT-24HXZT1 | 640 GB | 2       | 575   | 509   | 0.14   |
| WDC       | WD5003AZEX-00K3CA0 | 500 GB | 2       | 138   | 4     | 0.13   |
| Seagate   | ST3000VX009-2AY10G | 3 TB   | 2       | 49    | 0     | 0.13   |
| Samsung   | HM160HC            | 160 GB | 7       | 216   | 20    | 0.13   |
| WDC       | WD10JUCT-61CYNY0   | 1 TB   | 1       | 48    | 0     | 0.13   |
| WDC       | WD5000LPCX-80VHAT0 | 500 GB | 2       | 48    | 0     | 0.13   |
| WDC       | WD600UE-22KVT0     | 64 GB  | 1       | 243   | 4     | 0.13   |
| ExcelStor | J8160              | 34 GB  | 1       | 48    | 0     | 0.13   |
| WDC       | WD2500BPVT-26JJ5T0 | 250 GB | 1       | 48    | 0     | 0.13   |
| WDC       | WD5000LPLX-66ZNTT1 | 500 GB | 3       | 53    | 1     | 0.13   |
| Seagate   | ST9808210A         | 80 GB  | 2       | 259   | 19    | 0.13   |
| WDC       | WD7500BMVW-11S5XS0 | 752 GB | 1       | 434   | 8     | 0.13   |
| WDC       | WD15NMVW-11EDZS2   | 1.5 TB | 1       | 48    | 0     | 0.13   |
| WDC       | WD6001FSYZ-01SS7B1 | 6 TB   | 1       | 47    | 0     | 0.13   |
| WDC       | WD5000LPCX-35VHAT0 | 500 GB | 1       | 47    | 0     | 0.13   |
| Samsung   | SP1203N            | 120 GB | 6       | 486   | 31    | 0.13   |
| Hitachi   | HTS421210H9AT00    | 100 GB | 1       | 568   | 11    | 0.13   |
| Toshiba   | MK1255GSX H        | 120 GB | 2       | 236   | 419   | 0.13   |
| WDC       | WD20EZAZ-00GGJB0   | 2 TB   | 15      | 46    | 0     | 0.13   |
| WDC       | WD3200BEKT-22KA9T0 | 320 GB | 1       | 46    | 0     | 0.13   |
| Seagate   | ST160LM000 HM161GI | 160 GB | 1       | 46    | 0     | 0.13   |
| Hitachi   | HTS541660J9AT00    | 64 GB  | 1       | 184   | 3     | 0.13   |
| WDC       | WD20SPZX-75UA7T1   | 2 TB   | 3       | 45    | 0     | 0.13   |
| WDC       | WD101KFBX-68R56N0  | 10 TB  | 1       | 45    | 0     | 0.13   |
| WDC       | WD7500AYPS-01ZKB0  | 752 GB | 1       | 228   | 4     | 0.12   |
| Samsung   | SV4012H            | 40 GB  | 2       | 1504  | 236   | 0.12   |
| WDC       | WD3200AAJS-00V4A0  | 320 GB | 3       | 396   | 9     | 0.12   |
| Toshiba   | MK3265GSX H        | 320 GB | 1       | 45    | 0     | 0.12   |
| WDC       | WD1600AAJS-19WAA0  | 160 GB | 1       | 44    | 0     | 0.12   |
| IBM       | DTLA-307020        | 20 GB  | 1       | 754   | 16    | 0.12   |
| IBM/Hi... | IC25N060ATMR04-0   | 64 GB  | 7       | 306   | 16    | 0.12   |
| Hitachi   | HTS541212H9SA00    | 120 GB | 1       | 221   | 4     | 0.12   |
| WDC       | WD5000AAKX-004EA0  | 500 GB | 1       | 392   | 8     | 0.12   |
| Hitachi   | HDP725025GLAT80    | 250 GB | 1       | 216   | 4     | 0.12   |
| Toshiba   | MK3276GSX H        | 320 GB | 1       | 43    | 0     | 0.12   |
| Toshiba   | DT01ACA050 LENOVO  | 500 GB | 1       | 43    | 0     | 0.12   |
| WDC       | WD50EZRZ-00GZ5B1   | 5 TB   | 1       | 42    | 0     | 0.12   |
| Seagate   | ST2000VX000-9YW164 | 2 TB   | 7       | 700   | 892   | 0.12   |
| WDC       | WD10EZEX-60WN4A1   | 1 TB   | 9       | 52    | 1     | 0.12   |
| Maxtor    | 6B300R0            | 304 GB | 1       | 42    | 0     | 0.12   |
| Fujitsu   | MHV2120BH          | 120 GB | 1       | 425   | 9     | 0.12   |
| WDC       | WD1600BMVS-11F9S0  | 160 GB | 1       | 339   | 7     | 0.12   |
| WDC       | WD1503FYYS-02W0B0  | 1.5 TB | 1       | 382   | 8     | 0.12   |
| Hitachi   | HTS722080K9A300    | 80 GB  | 3       | 249   | 3     | 0.12   |
| WDC       | WD4003FRYZ-01F0DB0 | 4 TB   | 1       | 42    | 0     | 0.12   |
| WDC       | WD1600BEVT-26ZCT0  | 160 GB | 2       | 186   | 22    | 0.12   |
| Toshiba   | MK5056GSY          | 500 GB | 2       | 204   | 2     | 0.12   |
| IBM/Hi... | IC25N030ATCS04-0   | 32 GB  | 2       | 134   | 3     | 0.11   |
| WDC       | WD15NMVW-11EDZS6   | 1.5 TB | 1       | 41    | 0     | 0.11   |
| WDC       | WD30NMZW-11GX6S1   | 3 TB   | 1       | 41    | 0     | 0.11   |
| WDC       | WD5000AURX-63UY4Y0 | 500 GB | 1       | 370   | 8     | 0.11   |
| Toshiba   | MK4055GSX          | 400 GB | 3       | 338   | 7     | 0.11   |
| Maxtor    | 7L250R0            | 256 GB | 1       | 40    | 0     | 0.11   |
| WDC       | WD20EFAX-68FB5N0   | 2 TB   | 5       | 40    | 0     | 0.11   |
| Fujitsu   | MHV2200BT PL       | 200 GB | 1       | 325   | 7     | 0.11   |
| WDC       | WD1600BEVE-00UYT0  | 160 GB | 1       | 40    | 0     | 0.11   |
| WDC       | WD3200LPVT-00G33T0 | 320 GB | 2       | 40    | 0     | 0.11   |
| WDC       | WD6400AAKS-55A7B2  | 640 GB | 1       | 361   | 8     | 0.11   |
| WDC       | WD40EZRX-19SPEB0   | 4 TB   | 1       | 320   | 7     | 0.11   |
| Toshiba   | HDWJ105            | 500 GB | 9       | 39    | 0     | 0.11   |
| MediaMax  | WL1000GSA3254G     | 1 TB   | 1       | 476   | 11    | 0.11   |
| Hitachi   | HTS545012B9SA00    | 120 GB | 1       | 197   | 4     | 0.11   |
| WDC       | WD2000JS-22NCB1    | 200 GB | 1       | 1921  | 48    | 0.11   |
| Seagate   | ST1000NM0008-2F... | 1 TB   | 1       | 39    | 0     | 0.11   |
| Seagate   | ST33000650NS       | 3 TB   | 2       | 39    | 0     | 0.11   |
| WDC       | WD40EMRX-82UZ0N0   | 4 TB   | 3       | 39    | 0     | 0.11   |
| WDC       | WD5000AVCS-612DY1  | 500 GB | 1       | 582   | 14    | 0.11   |
| WDC       | WD5000AZLX-22JKKA0 | 500 GB | 11      | 71    | 1     | 0.11   |
| Samsung   | HM100JC            | 100 GB | 1       | 383   | 9     | 0.10   |
| Toshiba   | MK3265GSXF         | 320 GB | 4       | 222   | 25    | 0.10   |
| Seagate   | ST500LM030-1RK17D  | 500 GB | 16      | 38    | 0     | 0.10   |
| WDC       | WD1500ADFD-00NLR5  | 150 GB | 1       | 344   | 8     | 0.10   |
| WDC       | WD82PURZ-85TEUY0   | 8 TB   | 2       | 38    | 0     | 0.10   |
| Hitachi   | HTS541020G9SA00    | 20 GB  | 1       | 38    | 0     | 0.10   |
| WDC       | WD10SPZX-60Z10T0   | 1 TB   | 28      | 43    | 1     | 0.10   |
| WDC       | WD40PURZ-85TTDY0   | 4 TB   | 2       | 49    | 1     | 0.10   |
| Hitachi   | HTS722010K9SA00    | 100 GB | 2       | 676   | 23    | 0.10   |
| Toshiba   | HDWG180            | 8 TB   | 1       | 37    | 0     | 0.10   |
| Hitachi   | HDT721050SLA380    | 500 GB | 1       | 224   | 5     | 0.10   |
| WDC       | WD1600BEKT-60V5T1  | 160 GB | 3       | 150   | 4     | 0.10   |
| Hitachi   | HTS541640J9SA00    | 40 GB  | 1       | 186   | 4     | 0.10   |
| WDC       | WD3200BEVS-16VAT0  | 320 GB | 1       | 37    | 0     | 0.10   |
| WDC       | WD5000BEVT-80A0RT1 | 500 GB | 2       | 284   | 7     | 0.10   |
| Seagate   | ST12000VN0008-2... | 12 TB  | 2       | 36    | 0     | 0.10   |
| WDC       | WD5000LPCX-60VHAT1 | 500 GB | 10      | 36    | 0     | 0.10   |
| WDC       | WD800AAJS-60M0A0   | 80 GB  | 1       | 2215  | 60    | 0.10   |
| Hitachi   | HTS543212L9A300    | 120 GB | 2       | 232   | 72    | 0.10   |
| WDC       | WD10TPVT-00U4RT1   | 1 TB   | 3       | 319   | 155   | 0.10   |
| WDC       | WD800AAJS-60B4A0   | 80 GB  | 2       | 1529  | 24    | 0.10   |
| WDC       | WD2500AAJS-75B4A0  | 250 GB | 2       | 348   | 9     | 0.10   |
| Maxtor    | 6L120P0            | 122 GB | 2       | 35    | 0     | 0.10   |
| WDC       | WD1200BEVS-07LAT0  | 120 GB | 4       | 373   | 249   | 0.10   |
| WDC       | WD5000LPLX-21ZNTT0 | 500 GB | 3       | 78    | 366   | 0.10   |
| WDC       | WD40NDZW-11MR8S1   | 4 TB   | 1       | 34    | 0     | 0.09   |
| Maxtor    | STM3320613AS       | 320 GB | 13      | 1067  | 415   | 0.09   |
| Hitachi   | HTS725025A9A361... | 250 GB | 1       | 34    | 0     | 0.09   |
| Toshiba   | MK5076GSX          | 500 GB | 31      | 62    | 175   | 0.09   |
| Seagate   | ST500LM016 HN-M... | 500 GB | 2       | 34    | 0     | 0.09   |
| WDC       | WD5000BEKT-22KA9T0 | 500 GB | 1       | 302   | 8     | 0.09   |
| Hitachi   | HDS722580VLAT20    | 82 GB  | 3       | 418   | 180   | 0.09   |
| WDC       | WD1600BB-55GUA0    | 160 GB | 1       | 668   | 19    | 0.09   |
| HGST      | HTS725050B7E630    | 500 GB | 2       | 33    | 0     | 0.09   |
| Maxtor    | 2F030L0            | 32 GB  | 1       | 33    | 0     | 0.09   |
| Toshiba   | MK1235GSL          | 120 GB | 1       | 32    | 0     | 0.09   |
| WDC       | WD6400BEVT-24A0RT0 | 640 GB | 1       | 329   | 9     | 0.09   |
| WDC       | WD40EZAZ-00ZGHB0   | 4 TB   | 1       | 32    | 0     | 0.09   |
| Toshiba   | HDWM105            | 500 GB | 1       | 32    | 0     | 0.09   |
| Hitachi   | DK23EA-40          | 40 GB  | 2       | 241   | 236   | 0.09   |
| Maxtor    | 6L200P0            | 208 GB | 2       | 32    | 0     | 0.09   |
| MicroData | MD1TBLSSHD         | 1 TB   | 1       | 288   | 8     | 0.09   |
| WDC       | WD10E              | 1 TB   | 1       | 31    | 0     | 0.09   |
| HGST      | HUS726020ALE614    | 2 TB   | 1       | 31    | 0     | 0.09   |
| WDC       | WD1600BEVS-00VAT0  | 160 GB | 1       | 31    | 0     | 0.09   |
| WDC       | WD5000BEVT-00SCST0 | 500 GB | 1       | 311   | 9     | 0.09   |
| WDC       | WD800JB-00FSA0     | 80 GB  | 1       | 1366  | 43    | 0.09   |
| WDC       | WD2500JD-00HBC0    | 250 GB | 1       | 620   | 19    | 0.09   |
| Maxtor    | 2F030J1            | 32 GB  | 1       | 185   | 5     | 0.08   |
| Toshiba   | MK3275GSX          | 320 GB | 16      | 224   | 338   | 0.08   |
| WDC       | WD20EVDS-63T3B0    | 2 TB   | 1       | 273   | 8     | 0.08   |
| Seagate   | ST9402115AS        | 40 GB  | 2       | 160   | 1042  | 0.08   |
| Samsung   | HM121HC            | 120 GB | 3       | 230   | 19    | 0.08   |
| Seagate   | ST38410A           | 9 GB   | 1       | 754   | 24    | 0.08   |
| Maxtor    | STM3500320AS       | 500 GB | 17      | 677   | 284   | 0.08   |
| WDC       | WD600VE-75HDT0     | 64 GB  | 1       | 268   | 8     | 0.08   |
| IBM/Hi... | IC25N040ATCS04-0   | 40 GB  | 1       | 59    | 1     | 0.08   |
| WDC       | WD5000BEVT-35ZAT0  | 500 GB | 1       | 268   | 8     | 0.08   |
| Samsung   | SV0401N            | 40 GB  | 1       | 952   | 31    | 0.08   |
| Seagate   | ST750LM028-1KK162  | 752 GB | 1       | 29    | 0     | 0.08   |
| Seagate   | ST8000VN004-2M2101 | 8 TB   | 9       | 29    | 0     | 0.08   |
| Seagate   | ST3500320AS        | 500 GB | 80      | 798   | 479   | 0.08   |
| Samsung   | MP0804H            | 80 GB  | 3       | 243   | 8     | 0.08   |
| WDC       | WD1600JS-00MHB1    | 160 GB | 1       | 1060  | 35    | 0.08   |
| CLOVER    | CN-M500MBB         | 500 GB | 2       | 29    | 0     | 0.08   |
| WDC       | WD3200JB-00KFA0    | 320 GB | 1       | 29    | 0     | 0.08   |
| Samsung   | HM320JI            | 320 GB | 6       | 467   | 589   | 0.08   |
| Toshiba   | MK2576GSX          | 250 GB | 2       | 236   | 4     | 0.08   |
| Hitachi   | HTS543212L9SA02    | 120 GB | 1       | 27    | 0     | 0.08   |
| WDC       | WD2000JD-55HBC0    | 200 GB | 1       | 26    | 0     | 0.07   |
| WDC       | WD3200AAJS-00VWA1  | 320 GB | 1       | 708   | 26    | 0.07   |
| Hitachi   | HTS548040M9AT00    | 40 GB  | 1       | 470   | 17    | 0.07   |
| Hitachi   | HTS421260H9AT00    | 64 GB  | 4       | 462   | 19    | 0.07   |
| Seagate   | ST3640323AS        | 640 GB | 8       | 1077  | 484   | 0.07   |
| Samsung   | HM322IX            | 320 GB | 1       | 25    | 0     | 0.07   |
| Seagate   | ST9250320AS        | 250 GB | 18      | 346   | 266   | 0.07   |
| Toshiba   | MK5059GSX          | 500 GB | 1       | 932   | 36    | 0.07   |
| HGST      | HUS726T4TALE6L4    | 4 TB   | 3       | 31    | 507   | 0.07   |
| WDC       | WD1200JB-00CRA1    | 120 GB | 1       | 871   | 34    | 0.07   |
| WDC       | WD101EMAZ-11G7DA0  | 10 TB  | 2       | 24    | 0     | 0.07   |
| WDC       | WD2500AAJS-52B4A0  | 250 GB | 2       | 942   | 45    | 0.07   |
| WDC       | WD400VE-75HDT1     | 40 GB  | 1       | 23    | 0     | 0.06   |
| WDC       | WD2500BEVT-60A23T0 | 250 GB | 3       | 258   | 27    | 0.06   |
| Toshiba   | MK6032GAX          | 64 GB  | 1       | 23    | 0     | 0.06   |
| Seagate   | ST4000VX000-2AG166 | 4 TB   | 1       | 23    | 0     | 0.06   |
| Toshiba   | MK6465GSXW         | 640 GB | 1       | 552   | 23    | 0.06   |
| Toshiba   | MK2529GSG          | 250 GB | 2       | 313   | 1127  | 0.06   |
| Magnet... | MD02500-BQDW-RO    | 250 GB | 1       | 22    | 0     | 0.06   |
| Hitachi   | HTS543216L9SA02    | 160 GB | 3       | 134   | 11    | 0.06   |
| Toshiba   | MK3276GSX          | 320 GB | 26      | 28    | 273   | 0.06   |
| WDC       | WD10SDRW-11A0XS1   | 1 TB   | 1       | 22    | 0     | 0.06   |
| WDC       | WD3200AUDX-56WNHY0 | 320 GB | 1       | 22    | 0     | 0.06   |
| WDC       | WD2000JS-60NCB1    | 200 GB | 2       | 192   | 6     | 0.06   |
| CLOVER    | CN-M750MBB         | 752 GB | 1       | 22    | 0     | 0.06   |
| Samsung   | HM251JI            | 250 GB | 7       | 342   | 454   | 0.06   |
| Samsung   | HM641JX            | 640 GB | 1       | 22    | 0     | 0.06   |
| Toshiba   | MK1032GAX          | 100 GB | 2       | 108   | 4     | 0.06   |
| WDC       | WD3200AVVS-63L2B0  | 320 GB | 5       | 325   | 69    | 0.06   |
| WDC       | WD10TPVT-00HT5T1   | 1 TB   | 1       | 219   | 9     | 0.06   |
| WDC       | WD3200BEKX-22B7WT0 | 320 GB | 1       | 21    | 0     | 0.06   |
| WDC       | WD1600BEKT-00PVMT0 | 160 GB | 1       | 21    | 0     | 0.06   |
| Seagate   | ST3300831A         | 304 GB | 1       | 347   | 15    | 0.06   |
| Seagate   | ST3250824SCE       | 250 GB | 1       | 21    | 0     | 0.06   |
| Maxtor    | 6L080M0            | 80 GB  | 4       | 26    | 254   | 0.06   |
| WDC       | WD5000AVDS-73U7B1  | 500 GB | 2       | 189   | 7     | 0.06   |
| Maxtor    | STM3160613AS       | 160 GB | 1       | 41    | 1     | 0.06   |
| Fujitsu   | MHT2040AT          | 40 GB  | 1       | 166   | 7     | 0.06   |
| Maxtor    | 6Y120M0            | 122 GB | 2       | 25    | 4     | 0.06   |
| WDC       | WD400BB-22DEA0     | 40 GB  | 1       | 831   | 39    | 0.06   |
| Toshiba   | MQ02ABF050H-SSH... | 500 GB | 2       | 20    | 0     | 0.06   |
| Samsung   | HM160HI            | 160 GB | 69      | 346   | 361   | 0.06   |
| Seagate   | ST9500424AS        | 500 GB | 2       | 120   | 505   | 0.06   |
| WDC       | WD2000BB-00GUC0    | 200 GB | 1       | 637   | 30    | 0.06   |
| Maxtor    | 6B200M0            | 200 GB | 3       | 26    | 13    | 0.06   |
| WDC       | WD30EZRX-00AZ6B0   | 3 TB   | 2       | 99    | 124   | 0.06   |
| WDC       | WD10SMZW-34Y0TS0   | 1 TB   | 1       | 20    | 0     | 0.06   |
| WDC       | WD5000BPVT-75A1YT0 | 500 GB | 1       | 20    | 0     | 0.06   |
| WDC       | WD1001FAES-75W7A0  | 1 TB   | 1       | 2917  | 142   | 0.06   |
| WDC       | WD2500BPVT-00ZEST0 | 250 GB | 3       | 136   | 74    | 0.06   |
| WDC       | WD60EZRZ-00RWYB1   | 6 TB   | 2       | 47    | 1012  | 0.06   |
| Fujitsu   | MHV2060AH          | 64 GB  | 1       | 968   | 47    | 0.06   |
| WDC       | WD2500LPCX-24VHAT0 | 250 GB | 2       | 55    | 5     | 0.05   |
| IBM       | DARA-206000        | 6 GB   | 1       | 118   | 5     | 0.05   |
| Samsung   | HM100UX            | 1 TB   | 1       | 177   | 8     | 0.05   |
| Seagate   | ST3160215SCE       | 160 GB | 1       | 98    | 4     | 0.05   |
| IBM/Hi... | IC25N040ATMR04-0   | 40 GB  | 2       | 628   | 181   | 0.05   |
| Samsung   | HS12UHE            | 120 GB | 1       | 136   | 6     | 0.05   |
| Maxtor    | STM3300622A        | 304 GB | 1       | 173   | 8     | 0.05   |
| WDC       | WD200EB-75CPF0     | 20 GB  | 2       | 402   | 20    | 0.05   |
| Maxtor    | 2F040J0            | 40 GB  | 1       | 19    | 0     | 0.05   |
| Toshiba   | MK8052GSX          | 80 GB  | 4       | 150   | 44    | 0.05   |
| Seagate   | ST31000333AS       | 1 TB   | 23      | 703   | 458   | 0.05   |
| WDC       | WD1600JD-00GBB0    | 160 GB | 1       | 727   | 37    | 0.05   |
| WDC       | WD15EADS-22P8B0    | 1.5 TB | 2       | 388   | 511   | 0.05   |
| Seagate   | ST31000340AS       | 1 TB   | 6       | 1025  | 364   | 0.05   |
| Seagate   | ST9250421ASG       | 250 GB | 1       | 453   | 23    | 0.05   |
| Seagate   | ST9100822A         | 100 GB | 1       | 592   | 31    | 0.05   |
| WDC       | WD7500BPVT-75HXZT1 | 752 GB | 1       | 547   | 29    | 0.05   |
| WDC       | WD5000LPCX-80VHAT1 | 500 GB | 2       | 18    | 0     | 0.05   |
| WDC       | WD6003FFBX-68MU3N0 | 6 TB   | 1       | 18    | 0     | 0.05   |
| MARSHAL   | MAL2500SA-T54      | 500 GB | 2       | 323   | 27    | 0.05   |
| WDC       | WD5000LPVX-16V0TT0 | 500 GB | 1       | 71    | 3     | 0.05   |
| Quantum   | FIREBALLlct15 10   | 10 GB  | 1       | 105   | 5     | 0.05   |
| WDC       | WD2500JS-75NCB1    | 250 GB | 1       | 2681  | 153   | 0.05   |
| WDC       | WD1600JS-55MHB0    | 160 GB | 1       | 761   | 43    | 0.05   |
| Maxtor    | 6L160M0            | 160 GB | 6       | 26    | 351   | 0.05   |
| WDC       | WD120EMFZ-11A6JA0  | 12 TB  | 2       | 16    | 0     | 0.05   |
| Hitachi   | HDP725032GLAT80    | 320 GB | 1       | 943   | 55    | 0.05   |
| Samsung   | HD160HJ            | 160 GB | 19      | 753   | 763   | 0.05   |
| Seagate   | ST3320310CS        | 320 GB | 3       | 576   | 32    | 0.05   |
| Samsung   | HN-M250MBB         | 250 GB | 1       | 292   | 17    | 0.04   |
| Samsung   | HM060HI            | 64 GB  | 3       | 542   | 697   | 0.04   |
| Seagate   | ST10000VN0008-2... | 10 TB  | 2       | 16    | 0     | 0.04   |
| Samsung   | HM080HI            | 80 GB  | 3       | 525   | 289   | 0.04   |
| WDC       | WD3200BEKT-75PVMT0 | 320 GB | 2       | 217   | 18    | 0.04   |
| Seagate   | ST500LX025-1U71... | 500 GB | 1       | 15    | 0     | 0.04   |
| WDC       | WD800BB-88JHC0     | 80 GB  | 1       | 1625  | 101   | 0.04   |
| Hitachi   | HTS545025A7E380    | 250 GB | 1       | 15    | 0     | 0.04   |
| IBM/Hi... | IC35L060AVVA07-0   | 64 GB  | 1       | 678   | 42    | 0.04   |
| HGST      | HUS726020ALA610    | 2 TB   | 2       | 15    | 0     | 0.04   |
| Hitachi   | HTS543232L9SA02    | 320 GB | 1       | 1319  | 84    | 0.04   |
| HGST      | HUS722T1TALA604    | 1 TB   | 3       | 15    | 0     | 0.04   |
| WDC       | WD4000ABYS-01TNA0  | 400 GB | 1       | 688   | 44    | 0.04   |
| Seagate   | ST10000NE0008-2... | 10 TB  | 1       | 15    | 0     | 0.04   |
| Samsung   | SP1253N            | 120 GB | 1       | 286   | 18    | 0.04   |
| MediaMax  | WL250GSA872        | 250 GB | 1       | 15    | 0     | 0.04   |
| Hitachi   | HTS725025A9A364    | 250 GB | 18      | 439   | 1097  | 0.04   |
| Seagate   | ST320LT012-9WS14C  | 320 GB | 50      | 268   | 1026  | 0.04   |
| Hitachi   | HDS7250SASUN500G   | 500 GB | 1       | 14    | 0     | 0.04   |
| Hitachi   | HTS723225L9A360    | 250 GB | 3       | 322   | 1301  | 0.04   |
| WDC       | WD20SPZX-60UA7T0   | 2 TB   | 2       | 14    | 0     | 0.04   |
| Seagate   | OOS500G            | 500 GB | 1       | 14    | 0     | 0.04   |
| Seagate   | ST9120310AS        | 120 GB | 1       | 14    | 0     | 0.04   |
| Seagate   | ST31000533CS       | 1 TB   | 1       | 1038  | 72    | 0.04   |
| WDC       | WD205BA            | 20 GB  | 1       | 296   | 20    | 0.04   |
| Apple     | HDD HTS547550A9... | 500 GB | 3       | 170   | 27    | 0.04   |
| WDC       | WD10EADS-11M2B1    | 1 TB   | 1       | 526   | 37    | 0.04   |
| Maxtor    | 6L120M0            | 122 GB | 2       | 32    | 3     | 0.04   |
| Seagate   | ST310212A          | 10 GB  | 1       | 380   | 27    | 0.04   |
| Toshiba   | MK2565GSXN         | 250 GB | 1       | 502   | 36    | 0.04   |
| WDC       | WD5000AADS-98S9B1  | 500 GB | 1       | 120   | 8     | 0.04   |
| Maxtor    | 6L100M0            | 100 GB | 1       | 13    | 0     | 0.04   |
| Toshiba   | MK3265GSXV         | 320 GB | 2       | 166   | 136   | 0.04   |
| Maxtor    | STM3160813AS       | 160 GB | 5       | 780   | 476   | 0.04   |
| WDC       | WD20SDZW-11JJ8S1   | 2 TB   | 1       | 12    | 0     | 0.04   |
| WDC       | WD800BB-00CAA1     | 80 GB  | 1       | 800   | 61    | 0.04   |
| WDC       | WD10EACS-22D6B1    | 1 TB   | 1       | 12    | 0     | 0.04   |
| Toshiba   | MK2565GSXV         | 250 GB | 3       | 197   | 24    | 0.03   |
| WDC       | WD3200AAJS-00RYA0  | 320 GB | 2       | 1320  | 143   | 0.03   |
| Fujitsu   | MPG3204AT E        | 20 GB  | 1       | 138   | 10    | 0.03   |
| Seagate   | ST3250412CS        | 250 GB | 1       | 12    | 0     | 0.03   |
| Maxtor    | 2F040L0            | 40 GB  | 4       | 23    | 5     | 0.03   |
| Maxtor    | 6L160P0            | 163 GB | 4       | 32    | 6     | 0.03   |
| WDC       | WD121KFBX-68EF5N0  | 12 TB  | 1       | 12    | 0     | 0.03   |
| WDC       | WD40EZRZ-19GXCB0   | 4 TB   | 1       | 12    | 0     | 0.03   |
| WDC       | WD10EADS-65M2BX    | 1 TB   | 1       | 1087  | 91    | 0.03   |
| WDC       | WD2500BPVT-80ZEST0 | 250 GB | 1       | 106   | 8     | 0.03   |
| Maxtor    | 6L080L0            | 82 GB  | 6       | 21    | 13    | 0.03   |
| WDC       | WD7500LPCX-22HWST0 | 752 GB | 1       | 129   | 10    | 0.03   |
| WDC       | WD2500AAJS-60M0A0  | 250 GB | 2       | 705   | 533   | 0.03   |
| WDC       | WD800BB-00CAA0     | 80 GB  | 1       | 414   | 35    | 0.03   |
| Maxtor    | 2F030J0            | 32 GB  | 2       | 33    | 2     | 0.03   |
| Seagate   | ST9320421AS        | 320 GB | 5       | 456   | 51    | 0.03   |
| Toshiba   | MQ01ABD100V        | 1 TB   | 2       | 255   | 21    | 0.03   |
| Hitachi   | HDS722525VLAT80    | 250 GB | 1       | 11    | 0     | 0.03   |
| Maxtor    | STM3320820A        | 320 GB | 1       | 11    | 0     | 0.03   |
| MediaMax  | WL2000GSA6454G     | 2 TB   | 1       | 33    | 2     | 0.03   |
| WDC       | WD141KRYZ-01C66B0  | 14 TB  | 2       | 11    | 0     | 0.03   |
| Hitachi   | HDS721025CLA382... | 160 GB | 1       | 2614  | 237   | 0.03   |
| WDC       | WD5000AAKS-19V0A0  | 500 GB | 1       | 1131  | 103   | 0.03   |
| WDC       | WD20EZAZ-00L9GB0   | 2 TB   | 1       | 10    | 0     | 0.03   |
| Hitachi   | DK23CA-20          | 20 GB  | 1       | 93    | 8     | 0.03   |
| WDC       | WD5000BEVT-55A0RT0 | 500 GB | 1       | 110   | 10    | 0.03   |
| WDC       | WD5000LPCX-75VHAT1 | 500 GB | 2       | 9     | 0     | 0.03   |
| WDC       | WD3200BEVT-00ZAT0  | 320 GB | 1       | 266   | 26    | 0.03   |
| Toshiba   | MK2016GAP          | 20 GB  | 1       | 349   | 36    | 0.03   |
| WDC       | WD40EFAX-68JH4N0   | 4 TB   | 1       | 9     | 0     | 0.03   |
| WDC       | WD800JD-75JNC0     | 80 GB  | 2       | 858   | 355   | 0.02   |
| Maxtor    | 4K040H2            | 34 GB  | 1       | 298   | 33    | 0.02   |
| Seagate   | ST500LT012-9WS142  | 500 GB | 193     | 333   | 1065  | 0.02   |
| Toshiba   | MK1214GAH          | 120 GB | 3       | 60    | 142   | 0.02   |
| WDC       | WD10EZRX-00A3KB0   | 1 TB   | 1       | 8     | 0     | 0.02   |
| WDC       | WD10SDZM-59ZKVS0   | 1 TB   | 1       | 8     | 0     | 0.02   |
| Fujitsu   | MHV2120BH PL       | 120 GB | 9       | 25    | 3     | 0.02   |
| WDC       | WD3200BEVT-80A0RT1 | 320 GB | 2       | 1035  | 140   | 0.02   |
| WDC       | WD5000BMVW-11AJGS2 | 500 GB | 1       | 8     | 0     | 0.02   |
| Hitachi   | HTS548080M9AT00    | 80 GB  | 1       | 136   | 16    | 0.02   |
| ExcelStor | J9250              | 250 GB | 1       | 1349  | 167   | 0.02   |
| MediaMax  | WL250GLSA6410000   | 250 GB | 2       | 36    | 4     | 0.02   |
| LENOVO    | WD1004FBYZ-23YC... | 1 TB   | 2       | 7     | 0     | 0.02   |
| WDC       | WD20SMZW-11YFCS0   | 2 TB   | 1       | 7     | 0     | 0.02   |
| Maxtor    | 6Y120L0            | 122 GB | 7       | 28    | 15    | 0.02   |
| Maxtor    | 6Y060L2            | 64 GB  | 1       | 542   | 71    | 0.02   |
| Maxtor    | 6K040L0            | 41 GB  | 1       | 29    | 3     | 0.02   |
| Toshiba   | MK1656GSY          | 160 GB | 3       | 129   | 9     | 0.02   |
| Hitachi   | DK23EA-20B         | 17 GB  | 1       | 183   | 24    | 0.02   |
| WDC       | WD2000JS-00NCB1    | 200 GB | 1       | 537   | 73    | 0.02   |
| Hitachi   | HTS722016K9SA00    | 160 GB | 1       | 591   | 81    | 0.02   |
| WDC       | WD140EMFZ-11A0WA0  | 14 TB  | 6       | 7     | 0     | 0.02   |
| Seagate   | ST3320813AS        | 320 GB | 2       | 1042  | 142   | 0.02   |
| Seagate   | ST730212DE         | 32 GB  | 1       | 7     | 0     | 0.02   |
| Toshiba   | HDWD260            | 6 TB   | 1       | 7     | 0     | 0.02   |
| HP        | GB0250C8045        | 250 GB | 1       | 1405  | 198   | 0.02   |
| Maxtor    | 6E040L0            | 40 GB  | 11      | 30    | 34    | 0.02   |
| Seagate   | ST4000NM0115-1Y... | 4 TB   | 3       | 7     | 0     | 0.02   |
| Maxtor    | 6E030L0            | 32 GB  | 5       | 15    | 19    | 0.02   |
| WDC       | WD2500AAJS-41RYA0  | 250 GB | 1       | 76    | 10    | 0.02   |
| WDC       | WD10TMVV-11TK7S1   | 1 TB   | 2       | 177   | 39    | 0.02   |
| Maxtor    | 6L250S0            | 250 GB | 2       | 25    | 12    | 0.02   |
| Samsung   | SP1614N            | 160 GB | 1       | 690   | 106   | 0.02   |
| WDC       | WD360ADFD-00NLR4   | 37 GB  | 1       | 499   | 77    | 0.02   |
| HPE       | MB004000GWWQH      | 4 TB   | 1       | 6     | 0     | 0.02   |
| Maxtor    | 6L080P0            | 82 GB  | 2       | 10    | 10    | 0.02   |
| Samsung   | HM100JI            | 100 GB | 1       | 827   | 140   | 0.02   |
| Hitachi   | HTS541612J9AT00    | 120 GB | 1       | 116   | 19    | 0.02   |
| Seagate   | ST4000NE001-2MA101 | 4 TB   | 1       | 5     | 0     | 0.02   |
| Seagate   | ST3500320SV        | 500 GB | 1       | 45    | 7     | 0.02   |
| Samsung   | HM121HI            | 120 GB | 9       | 458   | 1453  | 0.02   |
| Hitachi   | HTS723232L9A360    | 320 GB | 4       | 866   | 850   | 0.02   |
| WDC       | WD10SPCX-24HWST0   | 1 TB   | 1       | 2080  | 373   | 0.02   |
| Seagate   | ST2000NE001-2M5101 | 2 TB   | 1       | 5     | 0     | 0.01   |
| WDC       | WD15SMZW-11JW8S0   | 1.5 TB | 1       | 5     | 0     | 0.01   |
| Seagate   | ST1000LM002-9VQ14L | 1 TB   | 1       | 25    | 4     | 0.01   |
| Seagate   | ST14000NE0008-2... | 14 TB  | 4       | 5     | 0     | 0.01   |
| Maxtor    | 6Y160P0            | 163 GB | 4       | 23    | 145   | 0.01   |
| WDC       | WD15EARS-22MVWB0   | 1.5 TB | 3       | 818   | 514   | 0.01   |
| WDC       | WD1200AAJS-00VTA0  | 120 GB | 1       | 995   | 203   | 0.01   |
| Hitachi   | HTE721060G9AT00    | 64 GB  | 1       | 4     | 0     | 0.01   |
| Fujitsu   | MHT2080AH          | 80 GB  | 1       | 292   | 64    | 0.01   |
| Toshiba   | MK8050GAC          | 80 GB  | 1       | 878   | 197   | 0.01   |
| Seagate   | ST500LX025-1U717D  | 500 GB | 2       | 42    | 193   | 0.01   |
| Maxtor    | 4R060J0            | 64 GB  | 1       | 25    | 5     | 0.01   |
| Fujitsu   | MHZ2160BJ G1       | 160 GB | 1       | 4     | 0     | 0.01   |
| Maxtor    | 6Y120P0            | 122 GB | 2       | 23    | 8     | 0.01   |
| Samsung   | HM500LI            | 500 GB | 1       | 7     | 1     | 0.01   |
| WDC       | WD2500BEKT-66F3T2  | 250 GB | 1       | 193   | 50    | 0.01   |
| WDC       | WD6003FZBX-00GXAB0 | 6 TB   | 1       | 3     | 0     | 0.01   |
| Seagate   | ST3500820AS        | 500 GB | 4       | 255   | 56    | 0.01   |
| Seagate   | ST1000NX0313       | 1 TB   | 1       | 1357  | 370   | 0.01   |
| Hitachi   | HTS722012K9A300    | 120 GB | 1       | 781   | 214   | 0.01   |
| Toshiba   | MK6028GAL          | 64 GB  | 1       | 3     | 0     | 0.01   |
| Seagate   | ST3250310SV        | 250 GB | 1       | 287   | 79    | 0.01   |
| WDC       | WD10SMRW-11Y43S0   | 1 TB   | 1       | 3     | 0     | 0.01   |
| Toshiba   | MK5061GSYN         | 500 GB | 14      | 83    | 459   | 0.01   |
| WDC       | WD5000AVJS-63TRA0  | 500 GB | 1       | 2013  | 578   | 0.01   |
| Fujitsu   | MJA2320BH G1       | 320 GB | 1       | 800   | 230   | 0.01   |
| Hitachi   | HTS541640J9AT00    | 40 GB  | 1       | 283   | 82    | 0.01   |
| HGST      | HTS725050A7E635    | 500 GB | 2       | 490   | 557   | 0.01   |
| Maxtor    | 6B250S0            | 250 GB | 2       | 20    | 471   | 0.01   |
| Maxtor    | 6Y080M0            | 80 GB  | 10      | 29    | 87    | 0.01   |
| Maxtor    | 6B200P0            | 208 GB | 1       | 43    | 12    | 0.01   |
| WDC       | WD10EADS-00R6B0    | 1 TB   | 1       | 1856  | 560   | 0.01   |
| Fujitsu   | MPE3136AT          | 16 GB  | 1       | 794   | 240   | 0.01   |
| Apple     | HDD HTS547575A9... | 752 GB | 1       | 506   | 153   | 0.01   |
| IBM/Hi... | IC35L060AVER07-0   | 64 GB  | 1       | 997   | 304   | 0.01   |
| Maxtor    | 6L300S0            | 304 GB | 4       | 23    | 460   | 0.01   |
| Maxtor    | 2F020J0            | 21 GB  | 1       | 41    | 12    | 0.01   |
| Maxtor    | 6Y080P0            | 82 GB  | 7       | 16    | 7     | 0.01   |
| Maxtor    | 6E020L0            | 21 GB  | 1       | 22    | 6     | 0.01   |
| WDC       | WD2004FBYZ-01YCBB0 | 2 TB   | 1       | 12    | 3     | 0.01   |
| Seagate   | ST3320820A         | 320 GB | 1       | 641   | 210   | 0.01   |
| Maxtor    | 6B160M0            | 163 GB | 1       | 3     | 0     | 0.01   |
| WDC       | WD800UE-22HCT0     | 80 GB  | 2       | 568   | 272   | 0.01   |
| Toshiba   | MAL2040SA-T54L     | 40 GB  | 1       | 2     | 0     | 0.01   |
| Toshiba   | MK3261GSYN         | 320 GB | 10      | 9     | 100   | 0.01   |
| WDC       | WD1200BEVS-75LAT0  | 118 GB | 1       | 1008  | 378   | 0.01   |
| Seagate   | ST500LM020-1G1162  | 500 GB | 3       | 2     | 0     | 0.01   |
| Maxtor    | 7L250S0            | 250 GB | 1       | 7     | 2     | 0.01   |
| Samsung   | SV0802N            | 80 GB  | 1       | 554   | 215   | 0.01   |
| Fujitsu   | MHW2080BJ G2       | 80 GB  | 1       | 337   | 131   | 0.01   |
| Seagate   | ST3160212SCE       | 160 GB | 1       | 2510  | 1028  | 0.01   |
| WDC       | WD3200AADS-00S9B0  | 320 GB | 1       | 26    | 10    | 0.01   |
| Maxtor    | 2B020H1            | 20 GB  | 6       | 23    | 75    | 0.01   |
| Maxtor    | 6Y200P0            | 208 GB | 2       | 20    | 9     | 0.01   |
| Toshiba   | MK3259GSX          | 320 GB | 1       | 192   | 82    | 0.01   |
| Samsung   | HM160JI            | 160 GB | 5       | 364   | 633   | 0.01   |
| Seagate   | ST3500620AS        | 500 GB | 3       | 594   | 1750  | 0.01   |
| Seagate   | ST3160812AS Q      | 160 GB | 1       | 1049  | 480   | 0.01   |
| WDC       | WD2500BEVT-35ZCT0  | 250 GB | 1       | 949   | 450   | 0.01   |
| MARSHAL   | MAL2020SA 80       | 20 GB  | 1       | 4     | 1     | 0.01   |
| WDC       | WD800BEVS-60RST0   | 80 GB  | 1       | 1199  | 581   | 0.01   |
| Hitachi   | HDS722516VLAT20    | 164 GB | 1       | 2242  | 1102  | 0.01   |
| Seagate   | ST31000528ASQ      | 1 TB   | 1       | 259   | 132   | 0.01   |
| WDC       | WD6400AAKS-00E4A0  | 640 GB | 1       | 1016  | 521   | 0.01   |
| WDC       | WD10EURX-63UHWY0   | 1 TB   | 1       | 644   | 338   | 0.01   |
| WDC       | WD4000AAKS-22TMA0  | 400 GB | 1       | 820   | 431   | 0.01   |
| Toshiba   | MK6476GSX          | 640 GB | 18      | 7     | 339   | 0.01   |
| Seagate   | ST9320423ASG       | 320 GB | 1       | 270   | 145   | 0.01   |
| WDC       | WD20EARS-19MVWB0   | 2 TB   | 1       | 713   | 392   | 0.00   |
| Toshiba   | MK2533GSG          | 250 GB | 1       | 1671  | 948   | 0.00   |
| Hitachi   | HUA5C3020ALA640    | 2 TB   | 1       | 1045  | 595   | 0.00   |
| WDC       | WD1600BEKT-75PVMT0 | 160 GB | 1       | 1003  | 580   | 0.00   |
| Seagate   | ST5000AS0011-1L... | 5 TB   | 1       | 1743  | 1015  | 0.00   |
| Maxtor    | 6Y080L0            | 80 GB  | 34      | 21    | 314   | 0.00   |
| CLOVER    | CD155UI            | 1.5 TB | 1       | 1     | 0     | 0.00   |
| IBM/Hi... | IC35L120AVVA07-0   | 128 GB | 1       | 918   | 552   | 0.00   |
| WDC       | WD140PURZ-85GG1Y0  | 14 TB  | 4       | 1     | 0     | 0.00   |
| Toshiba   | MK5061GSY          | 500 GB | 3       | 4     | 35    | 0.00   |
| Maxtor    | 6L200M0            | 208 GB | 3       | 18    | 23    | 0.00   |
| Samsung   | HD251KJ            | 250 GB | 1       | 1539  | 1019  | 0.00   |
| Seagate   | ST3120023AS        | 120 GB | 1       | 152   | 101   | 0.00   |
| WDC       | WD3200AAKX-00U6AA0 | 320 GB | 1       | 83    | 56    | 0.00   |
| Seagate   | ST33000651NS       | 3 TB   | 1       | 1889  | 1344  | 0.00   |
| WDC       | WD2500JD-98GBB0    | 250 GB | 1       | 875   | 628   | 0.00   |
| Hitachi   | HTS723216L9A360    | 160 GB | 5       | 510   | 1307  | 0.00   |
| Seagate   | ST3400820AS        | 400 GB | 1       | 1276  | 1004  | 0.00   |
| WDC       | WD3200LPCX-60VHAT0 | 320 GB | 1       | 1     | 0     | 0.00   |
| WDC       | WD1200             | 120 GB | 1       | 11    | 8     | 0.00   |
| Toshiba   | MK4026GAX          | 40 GB  | 1       | 191   | 157   | 0.00   |
| Toshiba   | MK7559GSM          | 752 GB | 1       | 1015  | 847   | 0.00   |
| WDC       | WD30EZRS-11J99B1   | 3 TB   | 1       | 794   | 663   | 0.00   |
| WDC       | WD400BB-00CAA0     | 40 GB  | 1       | 194   | 163   | 0.00   |
| WDC       | WD10JUCX-63WPNY0   | 1 TB   | 1       | 87    | 73    | 0.00   |
| Maxtor    | 4R120L0            | 122 GB | 2       | 43    | 39    | 0.00   |
| WDC       | WD7500AACS-00ZJB0  | 752 GB | 1       | 1106  | 1007  | 0.00   |
| Maxtor    | 4D040H2            | 41 GB  | 4       | 16    | 188   | 0.00   |
| Hitachi   | HTS725032A7E630    | 320 GB | 1       | 1076  | 1028  | 0.00   |
| WDC       | WD60EZAZ-00SF3B0   | 6 TB   | 1       | 1     | 0     | 0.00   |
| WDC       | WD3200JS-63PDB1    | 320 GB | 1       | 343   | 342   | 0.00   |
| WDC       | WD2003FYPS-27W9B0  | 2 TB   | 1       | 523   | 529   | 0.00   |
| Maxtor    | 6Y060L0            | 64 GB  | 4       | 24    | 63    | 0.00   |
| Seagate   | ST3750630AS        | 752 GB | 2       | 683   | 936   | 0.00   |
| WDC       | WD1005FBYZ-01YCBB3 | 1 TB   | 2       | 0     | 0     | 0.00   |
| Fujitsu   | MHV2160BT          | 160 GB | 1       | 483   | 535   | 0.00   |
| HGST      | TPH00100500GB 0... | 500 GB | 1       | 8     | 10    | 0.00   |
| HP        | GB1000EAFJL        | 1 TB   | 1       | 2402  | 3024  | 0.00   |
| WDC       | WD800BEVT-26ZCT0   | 80 GB  | 1       | 0     | 0     | 0.00   |
| Maxtor    | 4G120J6            | 122 GB | 2       | 20    | 218   | 0.00   |
| Toshiba   | MK3256GSY          | 320 GB | 4       | 5     | 282   | 0.00   |
| Maxtor    | STM3750330AS       | 752 GB | 1       | 995   | 1293  | 0.00   |
| MediaMax  | WL400GSA6454G      | 400 GB | 1       | 0     | 0     | 0.00   |
| WDC       | WD3200LPCX-22VHAT0 | 320 GB | 1       | 0     | 0     | 0.00   |
| WDC       | WD5000BPVX-00JC3T0 | 500 GB | 1       | 0     | 0     | 0.00   |
| Seagate   | ST500LX012-1LM1... | 500 GB | 1       | 358   | 480   | 0.00   |
| Fujitsu   | MHV2200BT          | 200 GB | 1       | 382   | 518   | 0.00   |
| Apple     | HDD HUA722010CL... | 1 TB   | 1       | 83    | 113   | 0.00   |
| Maxtor    | 7Y250M0            | 250 GB | 2       | 25    | 38    | 0.00   |
| Seagate   | ST3320620SV        | 320 GB | 1       | 564   | 835   | 0.00   |
| Fujitsu   | MHZ2120BH G2       | 120 GB | 1       | 693   | 1028  | 0.00   |
| WDC       | WD800AAJS-60PSA0   | 80 GB  | 1       | 624   | 1007  | 0.00   |
| Seagate   | ST3320410SV        | 320 GB | 1       | 685   | 1110  | 0.00   |
| Seagate   | ST500DM009-1BD142  | 500 GB | 1       | 0     | 0     | 0.00   |
| Maxtor    | 4D060H3            | 64 GB  | 1       | 18    | 31    | 0.00   |
| Seagate   | ST3000VM002-1ET166 | 3 TB   | 1       | 1155  | 2022  | 0.00   |
| Maxtor    | 6Y160M0            | 160 GB | 6       | 20    | 195   | 0.00   |
| Samsung   | HM500LX            | 500 GB | 1       | 233   | 423   | 0.00   |
| Hitachi   | HUA722010CLA630    | 1 TB   | 1       | 0     | 0     | 0.00   |
| WDC       | WD15EARS-19MVWB0   | 1.5 TB | 1       | 696   | 1306  | 0.00   |
| Hitachi   | HTS723212L9A360    | 120 GB | 1       | 535   | 1012  | 0.00   |
| Hitachi   | HTS723232A7A365    | 320 GB | 1       | 1130  | 2203  | 0.00   |
| Seagate   | ST10000NM001G-2... | 10 TB  | 4       | 0     | 0     | 0.00   |
| MediaMax  | WL6000GSA6457      | 6 TB   | 1       | 637   | 1372  | 0.00   |
| WDC       | WD15EURS-63S48Y0   | 1.5 TB | 1       | 11    | 26    | 0.00   |
| WDC       | WD2500BB-22RDA0    | 250 GB | 1       | 655   | 1524  | 0.00   |
| Seagate   | ST3802110ACE       | 80 GB  | 1       | 1203  | 3052  | 0.00   |
| Maxtor    | 6L300R0            | 304 GB | 1       | 7     | 20    | 0.00   |
| Seagate   | ST3250311SV        | 250 GB | 1       | 363   | 1010  | 0.00   |
| Seagate   | ST3750640A         | 752 GB | 1       | 732   | 2049  | 0.00   |
| Seagate   | ST3500321CS        | 500 GB | 1       | 48    | 137   | 0.00   |
| WDC       | WD3200L22X-00JVPT0 | 320 GB | 1       | 0     | 0     | 0.00   |
| Maxtor    | 7L300S0            | 304 GB | 3       | 13    | 40    | 0.00   |
| WDC       | WD2500BEKT-60F3T1  | 250 GB | 1       | 533   | 1607  | 0.00   |
| Seagate   | ST250LT012-9WS141  | 250 GB | 4       | 337   | 1077  | 0.00   |
| Seagate   | ST980817AS         | 80 GB  | 1       | 310   | 1009  | 0.00   |
| WDC       | WD1600AAJS-56WAA0  | 160 GB | 1       | 299   | 1021  | 0.00   |
| WDC       | WD5000LPLX-60ZNTT0 | 500 GB | 1       | 0     | 0     | 0.00   |
| WDC       | WD20EZRX-00SPEB0   | 2 TB   | 1       | 574   | 2072  | 0.00   |
| Seagate   | ST320LT000-9VL142  | 320 GB | 1       | 278   | 1009  | 0.00   |
| Hitachi   | HTS542580K9A300    | 80 GB  | 2       | 267   | 1012  | 0.00   |
| Seagate   | ST9320312AS        | 320 GB | 2       | 264   | 1108  | 0.00   |
| Samsung   | SV2011H            | 20 GB  | 1       | 0     | 3     | 0.00   |
| WDC       | WD2500AAJS-55B4A0  | 250 GB | 1       | 476   | 2020  | 0.00   |
| Toshiba   | MK2555GSX H        | 250 GB | 1       | 428   | 1908  | 0.00   |
| WDC       | WD800 AAJS-00PSA0  | 80 GB  | 1       | 97    | 459   | 0.00   |
| Fujitsu   | MHT2060BH          | 64 GB  | 1       | 407   | 2048  | 0.00   |
| Maxtor    | 6B120P0            | 122 GB | 1       | 0     | 0     | 0.00   |
| Seagate   | ST3160316CS        | 160 GB | 1       | 0     | 0     | 0.00   |
| WDC       | WD2005FBYZ-01YCBB1 | 2 TB   | 1       | 0     | 0     | 0.00   |
| WDC       | WD40NPZZ-00PDPT0   | 4 TB   | 1       | 0     | 0     | 0.00   |
| Samsung   | HM320JX            | 320 GB | 1       | 37    | 331   | 0.00   |
| Seagate   | ST980829A          | 80 GB  | 1       | 222   | 2022  | 0.00   |
| Seagate   | MB0500EAMZD        | 500 GB | 1       | 94    | 857   | 0.00   |
| Maxtor    | 7L300R0            | 304 GB | 1       | 11    | 116   | 0.00   |
| Hitachi   | HTS725050A9A360    | 500 GB | 1       | 89    | 1009  | 0.00   |
| Toshiba   | MK8025GAL          | 80 GB  | 1       | 78    | 1017  | 0.00   |
| Maxtor    | 53073H6            | 32 GB  | 1       | 121   | 2068  | 0.00   |
| WDC       | WD20EADS-22R6B0    | 2 TB   | 1       | 105   | 1848  | 0.00   |
| Hitachi   | HTS548060M9AT00    | 64 GB  | 1       | 35    | 655   | 0.00   |
| Maxtor    | 6L200S0            | 208 GB | 1       | 2     | 39    | 0.00   |
| Seagate   | ST3000VX010-2H916L | 3 TB   | 2       | 0     | 0     | 0.00   |
| WDC       | WD60PURX-64T0ZY1   | 6 TB   | 1       | 0     | 0     | 0.00   |
| Toshiba   | MK1676GSX          | 160 GB | 1       | 22    | 893   | 0.00   |
| Seagate   | ST380020A          | 80 GB  | 1       | 2     | 225   | 0.00   |
| Samsung   | HS06THB            | 64 GB  | 1       | 2     | 2087  | 0.00   |
| Hitachi   | HTS721060G9AT00    | 64 GB  | 1       | 0     | 37    | 0.00   |

HDD by Family
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days   — avg. days per sample,
Err    — avg. errors per sample,
MTBF   — avg. MTBF in years per sample.

| MFG       | Family                 | Models | Samples | Days  | Err   | MTBF   |
|-----------|------------------------|--------|---------|-------|-------|--------|
| Samsung   | SpinPoint V20400       | 1      | 1       | 5713  | 0     | 15.65  |
| HP        | Seagate Barracuda 7... | 1      | 2       | 3447  | 0     | 9.44   |
| Hitachi   | Sun Original           | 2      | 11      | 2609  | 0     | 7.15   |
| Seagate   | Barracuda ES+          | 2      | 2       | 2199  | 0     | 6.03   |
| Samsung   | SpinPoint F3 RE        | 1      | 1       | 1865  | 0     | 5.11   |
| Hitachi   | Unknown                | 1      | 1       | 1717  | 0     | 4.70   |
| Hitachi   | CinemaStar 5K320       | 2      | 2       | 1702  | 0     | 4.67   |
| Seagate   | Momentus Xt            | 1      | 1       | 1697  | 0     | 4.65   |
| Samsung   | SpinPoint PL40         | 1      | 2       | 3755  | 9     | 4.62   |
| Seagate   | Constellation.2 (SATA) | 2      | 20      | 1727  | 1     | 4.55   |
| Seagate   | SpinPoint F4 EG (AF)   | 1      | 3       | 1617  | 0     | 4.43   |
| HP        | RE3                    | 1      | 1       | 1490  | 0     | 4.08   |
| Quantum   | Unknown                | 1      | 1       | 1486  | 0     | 4.07   |
| WDC       | RE4-GP                 | 5      | 11      | 1618  | 49    | 4.02   |
| Hitachi   | Ultrastar A7K1000      | 4      | 8       | 1942  | 245   | 3.97   |
| Toshiba   | 3.5" HDD MK.002TSKB    | 1      | 1       | 1446  | 0     | 3.96   |
| Hitachi   | Deskstar 7K2000        | 2      | 27      | 1748  | 10    | 3.96   |
| Apple     | Travelstar 7K750       | 1      | 2       | 1397  | 0     | 3.83   |
| Seagate   | Laptop Thin            | 1      | 1       | 1394  | 0     | 3.82   |
| Hitachi   | Deskstar 7K4000        | 1      | 4       | 1544  | 341   | 3.74   |
| WDC       | RE2                    | 7      | 16      | 1611  | 39    | 3.65   |
| Hitachi   | Ultrastar A7K2000      | 7      | 39      | 1570  | 29    | 3.32   |
| WDC       | Raptor X               | 1      | 1       | 1164  | 0     | 3.19   |
| Toshiba   | 1.8" HDD MK..17GSG     | 1      | 1       | 1162  | 0     | 3.18   |
| WDC       | WDC Enterprise         | 1      | 1       | 1134  | 0     | 3.11   |
| Seagate   | Enterprise NAS HDD     | 1      | 3       | 1128  | 0     | 3.09   |
| HGST      | MegaScale 4000         | 2      | 9       | 1095  | 0     | 3.00   |
| Hitachi   | Deskstar 7K3000        | 4      | 70      | 1262  | 53    | 2.97   |
| HGST      | Ultrastar 7K4000       | 5      | 57      | 1097  | 36    | 2.91   |
| WDC       | RE3                    | 17     | 64      | 1398  | 5     | 2.88   |
| HP        | Unknown                | 2      | 2       | 1030  | 0     | 2.82   |
| WDC       | Purple NV              | 1      | 1       | 1023  | 0     | 2.80   |
| Seagate   | Archive HDD            | 3      | 38      | 1187  | 31    | 2.78   |
| Samsung   | SpinPoint F4 EG (AF)   | 2      | 43      | 1206  | 47    | 2.77   |
| Toshiba   | 3.5" HDD               | 1      | 1       | 1008  | 0     | 2.76   |
| Hitachi   | Ultrastar 7K3000       | 3      | 50      | 1034  | 1     | 2.72   |
| Seagate   | Constellation.2        | 3      | 3       | 958   | 0     | 2.63   |
| Toshiba   | 2.5" HDD MQ01UBB       | 1      | 4       | 952   | 0     | 2.61   |
| WDC       | Se                     | 6      | 12      | 1094  | 1     | 2.43   |
| Hitachi   | Deskstar 5K3000        | 5      | 29      | 1157  | 23    | 2.41   |
| Seagate   | U5                     | 2      | 2       | 875   | 0     | 2.40   |
| HGST      | Deskstar NAS           | 8      | 43      | 907   | 22    | 2.40   |
| Toshiba   | 2.5" HDD MQ01ABF..H    | 1      | 2       | 873   | 0     | 2.39   |
| Seagate   | Desktop HDD.15         | 4      | 80      | 951   | 48    | 2.39   |
| HP        | Proliant HardDrive     | 9      | 11      | 1322  | 34    | 2.36   |
| Toshiba   | 3.5" DT01ABA Deskto... | 2      | 14      | 900   | 2     | 2.33   |
| Quantum   | Fireball Plus AS       | 2      | 2       | 845   | 0     | 2.32   |
| Hitachi   | Ultrastar 7K4000       | 3      | 15      | 837   | 84    | 2.22   |
| WDC       | Caviar Black           | 45     | 421     | 1025  | 36    | 2.20   |
| WDC       | Caviar SE16            | 5      | 34      | 994   | 18    | 2.10   |
| Seagate   | NAS HDD                | 7      | 28      | 807   | 72    | 2.07   |
| Seagate   | Barracuda 7200.7       | 1      | 3       | 1192  | 70    | 2.05   |
| Seagate   | Constellation ES.2 ... | 4      | 13      | 1179  | 111   | 2.04   |
| Hitachi   | Deskstar T7K500        | 8      | 60      | 1147  | 69    | 1.98   |
| Seagate   | Barracuda 7200.8       | 9      | 45      | 1258  | 87    | 1.98   |
| Seagate   | Barracuda ES           | 6      | 38      | 1198  | 338   | 1.92   |
| Samsung   | SpinPoint F1 RE        | 2      | 3       | 824   | 34    | 1.90   |
| HP        | Constellation ES.3     | 1      | 2       | 691   | 0     | 1.89   |
| Seagate   | Exos 7E8               | 2      | 4       | 681   | 0     | 1.87   |
| WDC       | RE                     | 26     | 58      | 953   | 35    | 1.84   |
| WDC       | VelociRaptor           | 25     | 60      | 827   | 5     | 1.84   |
| Apple     | Momentus               | 1      | 1       | 662   | 0     | 1.82   |
| Seagate   | Constellation ES (S... | 4      | 21      | 1163  | 164   | 1.79   |
| WDC       | Caviar SE              | 148    | 495     | 930   | 26    | 1.77   |
| Seagate   | Barracuda XT           | 2      | 17      | 946   | 215   | 1.75   |
| Hitachi   | CinemaStar 5K1000      | 4      | 6       | 725   | 1     | 1.74   |
| Hitachi   | Deskstar 7K1000        | 3      | 17      | 1168  | 19    | 1.74   |
| Hitachi   | Deskstar 7K80          | 6      | 71      | 883   | 35    | 1.73   |
| Maxtor    | MaXLine III (SATA/300) | 2      | 4       | 1049  | 238   | 1.73   |
| HGST      | Unknown                | 2      | 2       | 633   | 5     | 1.72   |
| Hitachi   | Deskstar 7K500         | 1      | 6       | 1732  | 10    | 1.71   |
| Samsung   | SpinPoint F3           | 4      | 233     | 822   | 39    | 1.70   |
| WDC       | Raptor                 | 13     | 20      | 1197  | 12    | 1.70   |
| WDC       | Red                    | 24     | 495     | 746   | 12    | 1.68   |
| Hitachi   | Deskstar 7K1000.B      | 11     | 106     | 1048  | 53    | 1.68   |
| Hitachi   | Deskstar 5K1000        | 3      | 24      | 762   | 58    | 1.66   |
| WDC       | Caviar Green           | 143    | 1424    | 934   | 77    | 1.65   |
| Seagate   | U9                     | 2      | 6       | 595   | 0     | 1.63   |
| Samsung   | SpinPoint              | 7      | 9       | 741   | 49    | 1.63   |
| Apple     | SpinPoint              | 1      | 1       | 589   | 0     | 1.61   |
| Toshiba   | 3.5" MD04ACA Enterp... | 2      | 11      | 792   | 366   | 1.61   |
| Toshiba   | 2.5" HDD MQ01ABC       | 1      | 1       | 574   | 0     | 1.57   |
| Samsung   | SpinPoint F2 EG        | 3      | 112     | 908   | 217   | 1.57   |
| Samsung   | SpinPoint T133         | 5      | 23      | 939   | 154   | 1.57   |
| Seagate   | Barracuda Green (AF)   | 4      | 162     | 929   | 204   | 1.55   |
| Hitachi   | Deskstar E7K500        | 2      | 2       | 559   | 0     | 1.53   |
| Fujitsu   | MPA..MPG               | 5      | 6       | 711   | 42    | 1.53   |
| WDC       | Black                  | 18     | 181     | 612   | 15    | 1.50   |
| WDC       | RE4                    | 18     | 95      | 811   | 3     | 1.48   |
| Seagate   | DB35.3                 | 6      | 12      | 654   | 193   | 1.48   |
| Seagate   | Barracuda 7200.10      | 34     | 1211    | 889   | 264   | 1.46   |
| Seagate   | Laptop HDD             | 2      | 3       | 531   | 0     | 1.46   |
| HGST      | Deskstar 7K4000        | 2      | 4       | 837   | 1     | 1.42   |
| WDC       | RE2-GP                 | 2      | 2       | 608   | 2     | 1.42   |
| Hitachi   | Deskstar 7K1000.C      | 15     | 470     | 760   | 54    | 1.40   |
| Toshiba   | 3.5" HDD DT01ABA..V    | 3      | 3       | 501   | 0     | 1.37   |
| WDC       | Green                  | 6      | 111     | 540   | 1     | 1.37   |
| Apple     | Barracuda              | 1      | 11      | 497   | 0     | 1.36   |
| Seagate   | Video 3.5 HDD          | 9      | 25      | 611   | 254   | 1.36   |
| Hitachi   | Deskstar T7K250        | 5      | 32      | 1010  | 41    | 1.36   |
| Hitachi   | Deskstar 7K250         | 7      | 13      | 962   | 284   | 1.36   |
| Samsung   | SpinPoint F1 DT        | 11     | 273     | 968   | 219   | 1.36   |
| WDC       | Red Pro                | 9      | 13      | 490   | 0     | 1.35   |
| Maxtor    | DiamondMax 10 (SATA... | 6      | 31      | 719   | 35    | 1.34   |
| Seagate   | Barracuda 7200.7 an... | 19     | 582     | 851   | 85    | 1.34   |
| Seagate   | Barracuda 5400.1       | 1      | 5       | 835   | 33    | 1.32   |
| Seagate   | Constellation ES.3     | 5      | 47      | 581   | 81    | 1.32   |
| Apple     | HGST Travelstar Z5K500 | 1      | 15      | 500   | 2     | 1.32   |
| Seagate   | Enterprise Capacity... | 10     | 52      | 477   | 0     | 1.31   |
| WDC       | Caviar                 | 62     | 157     | 742   | 41    | 1.31   |
| WDC       | AV-GP                  | 37     | 107     | 673   | 52    | 1.31   |
| Apple     | Travelstar 5K1000      | 2      | 18      | 493   | 113   | 1.30   |
| HGST      | Travelstar 5K1500      | 2      | 5       | 810   | 212   | 1.30   |
| Toshiba   | 2.5" HDD MK..32GSX     | 1      | 5       | 497   | 1     | 1.29   |
| Seagate   | UX                     | 1      | 7       | 889   | 12    | 1.29   |
| Toshiba   | 2.5" HDD MQ03ABB       | 1      | 1       | 468   | 0     | 1.28   |
| Seagate   | Constellation ES.2     | 1      | 1       | 467   | 0     | 1.28   |
| Samsung   | SpinPoint VL40         | 1      | 1       | 2328  | 4     | 1.28   |
| HGST      | Ultrastar He10         | 2      | 12      | 493   | 1     | 1.27   |
| Hitachi   | Deskstar P7K500        | 9      | 155     | 958   | 58    | 1.26   |
| Toshiba   | Toshiba Enterprise     | 1      | 10      | 456   | 0     | 1.25   |
| Hitachi   | Deskstar 7K160         | 7      | 150     | 898   | 102   | 1.23   |
| Samsung   | SpinPoint F3 EG        | 4      | 33      | 652   | 127   | 1.20   |
| WDC       | Caviar Blue            | 316    | 3217    | 646   | 44    | 1.18   |
| Seagate   | Barracuda 7200.9       | 33     | 478     | 800   | 415   | 1.18   |
| WDC       | AV                     | 21     | 42      | 685   | 60    | 1.17   |
| WDC       | Black SSHD             | 1      | 8       | 426   | 0     | 1.17   |
| Seagate   | Barracuda SpinPoint F3 | 2      | 51      | 519   | 8     | 1.17   |
| Maxtor    | MaXLine Pro 500        | 1      | 2       | 601   | 2     | 1.16   |
| Seagate   | Desktop SSHD           | 7      | 87      | 560   | 69    | 1.16   |
| WDC       | Scorpio Blue EIDE      | 6      | 10      | 421   | 0     | 1.16   |
| Seagate   | Momentus XT (AF)       | 1      | 14      | 458   | 76    | 1.14   |
| Seagate   | Barracuda 7200.12      | 15     | 1297    | 744   | 177   | 1.14   |
| Toshiba   | 2.5" HDD MK..75GSX     | 1      | 1       | 412   | 0     | 1.13   |
| Seagate   | Video 2.5              | 3      | 17      | 404   | 0     | 1.11   |
| Seagate   | Barracuda 7200.14 (AF) | 26     | 2024    | 564   | 121   | 1.11   |
| Seagate   | SpinPoint M9T          | 2      | 44      | 460   | 5     | 1.11   |
| Fujitsu   | MHW BH                 | 9      | 49      | 574   | 56    | 1.07   |
| Seagate   | Surveillance           | 5      | 14      | 388   | 0     | 1.06   |
| Seagate   | SpinPoint M7E          | 3      | 15      | 398   | 1     | 1.06   |
| Seagate   | Barracuda Pro          | 2      | 6       | 385   | 0     | 1.06   |
| HP        | 250GB SATA disk VB0... | 1      | 9       | 793   | 6     | 1.05   |
| Toshiba   | 2.5" HDD MK..59GSXP... | 1      | 4       | 450   | 7     | 1.05   |
| Seagate   | IronWolf               | 14     | 116     | 429   | 5     | 1.04   |
| Seagate   | Exos 7E2               | 2      | 3       | 829   | 124   | 1.04   |
| Seagate   | SpinPoint D8X          | 1      | 2       | 559   | 404   | 1.02   |
| ExcelStor | Jupiter                | 8      | 17      | 764   | 13    | 1.01   |
| Seagate   | Momentus               | 4      | 10      | 611   | 152   | 1.01   |
| Seagate   | Pipeline HD 5900.2     | 8      | 74      | 631   | 151   | 1.01   |
| Seagate   | SV35                   | 12     | 86      | 460   | 146   | 0.99   |
| WDC       | Caviar Blue EIDE       | 17     | 97      | 613   | 65    | 0.99   |
| Seagate   | IronWolf Pro           | 8      | 23      | 499   | 5     | 0.98   |
| WDC       | Elements / My Passport | 43     | 191     | 458   | 36    | 0.98   |
| HGST      | Ultrastar 7K2          | 3      | 8       | 355   | 0     | 0.97   |
| Toshiba   | 2.5" HDD MK..61GSY     | 1      | 1       | 354   | 0     | 0.97   |
| Hitachi   | CinemaStar P7K500      | 1      | 2       | 1010  | 2     | 0.97   |
| Seagate   | Barracuda ES.2         | 4      | 41      | 1062  | 390   | 0.97   |
| HGST      | CinemaStar Z5K500      | 2      | 5       | 424   | 1     | 0.96   |
| Toshiba   | 2.5" HDD MQ01UBD       | 2      | 24      | 490   | 182   | 0.96   |
| Maxtor    | DiamondMax 21          | 16     | 206     | 729   | 389   | 0.96   |
| Toshiba   | 3.5" HDD DT01ACA       | 4      | 792     | 382   | 23    | 0.93   |
| Seagate   | Constellation CS       | 3      | 12      | 594   | 333   | 0.92   |
| HGST      | Ultrastar He8          | 3      | 12      | 336   | 0     | 0.92   |
| Toshiba   | X300                   | 4      | 36      | 364   | 77    | 0.92   |
| Samsung   | SpinPoint F4           | 2      | 36      | 556   | 124   | 0.91   |
| WDC       | Gold                   | 13     | 25      | 332   | 0     | 0.91   |
| Seagate   | Pipeline HD Mini       | 4      | 13      | 636   | 137   | 0.91   |
| Seagate   | Barracuda              | 2      | 8       | 325   | 0     | 0.89   |
| Toshiba   | 3.5" MG04ACA Enterp... | 3      | 11      | 323   | 1     | 0.88   |
| Fujitsu   | MHY BH                 | 5      | 64      | 539   | 149   | 0.88   |
| Seagate   | Maxtor DiamondMax 23   | 4      | 64      | 721   | 277   | 0.86   |
| Samsung   | SpinPoint P80 SD       | 7      | 212     | 811   | 404   | 0.86   |
| MediaMax  | WL5000                 | 1      | 1       | 308   | 0     | 0.85   |
| Samsung   | SpinPoint T166         | 7      | 175     | 917   | 445   | 0.84   |
| Hitachi   | Travelstar 7K320       | 12     | 27      | 640   | 551   | 0.83   |
| Toshiba   | 2.5" HDD MQ03UBB       | 2      | 10      | 321   | 2     | 0.83   |
| Samsung   | SpinPoint F1 EG        | 1      | 2       | 483   | 9     | 0.83   |
| WDC       | Scorpio                | 1      | 1       | 300   | 0     | 0.82   |
| Seagate   | SpinPoint F4           | 2      | 6       | 584   | 74    | 0.82   |
| Samsung   | SpinPoint M7E (AF)     | 4      | 135     | 461   | 80    | 0.82   |
| Seagate   | Barracuda ATA V        | 3      | 4       | 1510  | 35    | 0.82   |
| Seagate   | Barracuda LP           | 4      | 74      | 797   | 351   | 0.81   |
| MediaMax  | WL1000                 | 2      | 2       | 509   | 6     | 0.80   |
| Seagate   | SV35.5                 | 2      | 4       | 668   | 267   | 0.78   |
| Seagate   | Constellation ES (S... | 3      | 27      | 1140  | 42    | 0.78   |
| Fujitsu   | MHZ BH                 | 10     | 81      | 495   | 297   | 0.78   |
| HP        | Ultrastar 7K4000       | 1      | 1       | 1419  | 4     | 0.78   |
| Toshiba   | 2.5" HDD MK..58GSX     | 1      | 3       | 452   | 3     | 0.78   |
| Hitachi   | Travelstar 5K500.B     | 14     | 408     | 515   | 155   | 0.78   |
| WDC       | Scorpio Blue           | 217    | 1979    | 423   | 60    | 0.77   |
| Apple     | MK..65GSXF             | 1      | 2       | 505   | 201   | 0.77   |
| Fujitsu   | MHX BT                 | 2      | 5       | 619   | 30    | 0.77   |
| WDC       | Scorpio Black          | 47     | 192     | 461   | 110   | 0.75   |
| HGST      | Travelstar 7K1000      | 4      | 282     | 315   | 115   | 0.74   |
| WDC       | Black UltraSlim        | 1      | 1       | 267   | 0     | 0.73   |
| Toshiba   | 2.5" HDD MQ04UBF       | 1      | 9       | 267   | 0     | 0.73   |
| Samsung   | SpinPoint S166         | 3      | 65      | 819   | 469   | 0.73   |
| Toshiba   | 3.5" MG03ACAxxx(Y) ... | 4      | 14      | 450   | 3     | 0.73   |
| Hitachi   | Travelstar 7K100       | 5      | 13      | 564   | 31    | 0.71   |
| Samsung   | SpinPoint S250         | 2      | 55      | 828   | 618   | 0.71   |
| Seagate   | Barracuda V            | 1      | 1       | 259   | 0     | 0.71   |
| Seagate   | Momentus 7200.2        | 7      | 18      | 563   | 243   | 0.71   |
| Maxtor    | DiamondMax 20          | 6      | 22      | 619   | 372   | 0.70   |
| Hitachi   | Travelstar 5K750       | 3      | 295     | 468   | 369   | 0.70   |
| Toshiba   | 2.5" HDD               | 18     | 57      | 450   | 45    | 0.70   |
| Maxtor    | DiamondMax Plus D740X  | 2      | 3       | 834   | 4     | 0.70   |
| Seagate   | SpinPoint M8 (AF)      | 6      | 894     | 359   | 48    | 0.69   |
| Seagate   | Barracuda ATA IV       | 4      | 53      | 620   | 29    | 0.68   |
| Seagate   | Barracuda 3.5          | 9      | 506     | 261   | 14    | 0.68   |
| HGST      | Ultrastar 7K6000       | 10     | 22      | 258   | 27    | 0.68   |
| Seagate   | Momentus 5400.2        | 13     | 48      | 445   | 360   | 0.66   |
| Seagate   | Momentus 7200.4        | 8      | 205     | 536   | 357   | 0.66   |
| Seagate   | Momentus 7200.3        | 7      | 18      | 550   | 26    | 0.65   |
| Seagate   | LD25.2                 | 2      | 2       | 383   | 1     | 0.65   |
| Samsung   | SpinPoint M7           | 3      | 129     | 362   | 41    | 0.64   |
| IBM/Hi... | Deskstar GXP-180       | 4      | 6       | 620   | 5     | 0.64   |
| WDC       | Blue SSHD              | 2      | 2       | 230   | 0     | 0.63   |
| Hitachi   | Travelstar 4K120       | 4      | 13      | 827   | 33    | 0.63   |
| Seagate   | U6                     | 3      | 17      | 610   | 35    | 0.63   |
| Fujitsu   | MHV                    | 25     | 84      | 402   | 18    | 0.63   |
| Samsung   | SpinPoint MT2          | 1      | 3       | 228   | 0     | 0.63   |
| Seagate   | FireCuda 3.5           | 2      | 43      | 245   | 1     | 0.62   |
| WDC       | Blue Mobile            | 90     | 1291    | 266   | 21    | 0.62   |
| WDC       | Purple                 | 15     | 59      | 270   | 36    | 0.62   |
| Hitachi   | Deskstar 7K1000.D      | 2      | 82      | 630   | 502   | 0.62   |
| HGST      | Travelstar 5K1000      | 5      | 218     | 346   | 341   | 0.62   |
| Toshiba   | 2.5" HDD MQ04UBB       | 1      | 3       | 222   | 0     | 0.61   |
| WDC       | HGST Ultrastar He10    | 5      | 47      | 219   | 0     | 0.60   |
| Hitachi   | CinemaStar 7K1000.B    | 2      | 4       | 218   | 0     | 0.60   |
| WDC       | Green Mobile           | 1      | 3       | 336   | 12    | 0.60   |
| Toshiba   | 3.5" HDD E300          | 2      | 6       | 216   | 0     | 0.59   |
| Seagate   | Momentus 7200.5        | 4      | 91      | 495   | 109   | 0.59   |
| Toshiba   | MG06ACA Enterprise ... | 2      | 2       | 213   | 0     | 0.58   |
| Toshiba   | 2.5" HDD MK..59GSM     | 2      | 29      | 660   | 811   | 0.58   |
| Toshiba   | 2.5" HDD MQ01ACF       | 2      | 35      | 269   | 68    | 0.58   |
| HGST      | Edurastar              | 1      | 1       | 211   | 0     | 0.58   |
| Hitachi   | Travelstar Z7K500      | 2      | 9       | 453   | 709   | 0.58   |
| Toshiba   | 2.5" HDD MQ01ABD       | 8      | 623     | 320   | 128   | 0.57   |
| Toshiba   | 2.5" HDD MQ02ABD..H    | 1      | 17      | 318   | 6     | 0.57   |
| Samsung   | SpinPoint M8 (AF)      | 5      | 68      | 395   | 94    | 0.56   |
| HGST      | Travelstar Z7K500      | 6      | 169     | 338   | 224   | 0.56   |
| Seagate   | Skyhawk                | 6      | 21      | 205   | 1     | 0.56   |
| Toshiba   | 2.5" HDD MK..53GSX     | 1      | 1       | 201   | 0     | 0.55   |
| Toshiba   | 2.5" HDD MQ01ABD       | 2      | 5       | 200   | 0     | 0.55   |
| Seagate   | Barracuda Compute      | 4      | 51      | 218   | 33    | 0.55   |
| Maxtor    | DiamondMax D540X-4K    | 3      | 3       | 582   | 16    | 0.54   |
| Hitachi   | Travelstar 7K750       | 2      | 29      | 479   | 298   | 0.54   |
| Seagate   | Momentus 5400 PSD      | 2      | 3       | 352   | 338   | 0.53   |
| Seagate   | Barracuda ATA III      | 1      | 1       | 194   | 0     | 0.53   |
| Fujitsu   | MHW BJ                 | 3      | 3       | 305   | 44    | 0.53   |
| HGST      | Ultrastar DC HC520 ... | 3      | 6       | 192   | 0     | 0.53   |
| Toshiba   | 2.5" HDD MK..59GSM     | 1      | 18      | 478   | 303   | 0.53   |
| Samsung   | SpinPoint P80          | 18     | 111     | 566   | 139   | 0.52   |
| Seagate   | Laptop SSHD            | 7      | 188     | 315   | 112   | 0.52   |
| Seagate   | Video 3.5              | 1      | 3       | 186   | 0     | 0.51   |
| Apple     | Seagate Barracuda 7... | 1      | 1       | 185   | 0     | 0.51   |
| Seagate   | BarraCuda Pro          | 3      | 6       | 189   | 1     | 0.51   |
| IBM/Hi... | Deskstar 120GXP        | 4      | 8       | 655   | 117   | 0.50   |
| Hitachi   | Travelstar Z5K500      | 3      | 137     | 360   | 179   | 0.50   |
| Fujitsu   | MHZ BT                 | 1      | 2       | 1426  | 6     | 0.50   |
| WDC       | Black Mobile           | 27     | 194     | 205   | 9     | 0.49   |
| Seagate   | DB35.4                 | 1      | 2       | 701   | 21    | 0.49   |
| Toshiba   | 2.5" HDD MQ01ABF       | 2      | 33      | 202   | 32    | 0.49   |
| Hitachi   | Travelstar 7K200       | 7      | 19      | 498   | 182   | 0.48   |
| Toshiba   | P300                   | 4      | 294     | 183   | 13    | 0.48   |
| Hitachi   | Travelstar 5K1000      | 3      | 22      | 467   | 663   | 0.48   |
| WDC       | Blue                   | 70     | 649     | 183   | 7     | 0.47   |
| Hitachi   | Travelstar Z5K320      | 3      | 208     | 331   | 330   | 0.47   |
| Toshiba   | 2.5" HDD MQ01ABB       | 1      | 3       | 222   | 235   | 0.47   |
| Hitachi   | Travelstar 5K250       | 10     | 179     | 551   | 150   | 0.47   |
| Hitachi   | Travelstar Z7K320      | 3      | 42      | 410   | 506   | 0.47   |
| Seagate   | Momentus XT            | 1      | 13      | 697   | 166   | 0.47   |
| Seagate   | Momentus 5400.3        | 7      | 136     | 452   | 455   | 0.47   |
| Hitachi   | CinemaStar 5K1000.B    | 1      | 1       | 169   | 0     | 0.47   |
| Toshiba   | N300                   | 3      | 16      | 254   | 11    | 0.46   |
| Fujitsu   | MJA BH                 | 8      | 39      | 413   | 202   | 0.46   |
| HGST      | Travelstar Z5K1        | 1      | 26      | 179   | 1     | 0.46   |
| WDC       | Blue UltraSlim         | 1      | 1       | 166   | 0     | 0.46   |
| Toshiba   | 2.5" HDD MK..63GSX     | 2      | 16      | 600   | 19    | 0.46   |
| Toshiba   | 2.5" HDD MK..75GSX     | 4      | 82      | 420   | 404   | 0.46   |
| Lenovo    | Seagate Enterprise     | 1      | 1       | 165   | 0     | 0.45   |
| Fujitsu   | MHW AT                 | 2      | 2       | 165   | 0     | 0.45   |
| Seagate   | Momentus 5400.4        | 3      | 74      | 475   | 348   | 0.45   |
| Toshiba   | 2.5" HDD MK..55GSX     | 6      | 68      | 410   | 66    | 0.45   |
| Toshiba   | 2.5" HDD MK..34GSX     | 2      | 13      | 383   | 166   | 0.45   |
| Toshiba   | L200                   | 3      | 14      | 162   | 0     | 0.44   |
| Seagate   | FreePlay               | 3      | 12      | 249   | 683   | 0.44   |
| Toshiba   | 2.5" HDD MK..37GSX     | 1      | 19      | 448   | 139   | 0.44   |
| Seagate   | Barracuda 2.5 5400     | 6      | 165     | 172   | 15    | 0.44   |
| Fujitsu   | MHZ BS                 | 1      | 1       | 159   | 0     | 0.44   |
| Maxtor    | DiamondMax 17          | 2      | 10      | 305   | 125   | 0.43   |
| WDC       | Protege                | 6      | 11      | 682   | 33    | 0.43   |
| Seagate   | MobileMax-2            | 1      | 1       | 155   | 0     | 0.43   |
| Samsung   | SpinPoint V80          | 3      | 4       | 597   | 63    | 0.42   |
| Samsung   | SpinPoint V60          | 1      | 6       | 1055  | 104   | 0.42   |
| Hitachi   | Travelstar 5K320       | 11     | 129     | 510   | 234   | 0.42   |
| Seagate   | FireCuda 2.5           | 5      | 81      | 174   | 36    | 0.42   |
| Hitachi   | Travelstar 7K500       | 9      | 77      | 447   | 751   | 0.41   |
| Samsung   | SpinPoint MP5          | 3      | 9       | 317   | 202   | 0.41   |
| Toshiba   | Enterprise Surveill... | 1      | 1       | 1037  | 6     | 0.41   |
| Magnet... | Unknown                | 4      | 4       | 146   | 0     | 0.40   |
| MediaMax  | WL320                  | 1      | 1       | 146   | 0     | 0.40   |
| Hitachi   | Travelstar 5K500       | 1      | 6       | 520   | 5     | 0.40   |
| Seagate   | Terascale              | 1      | 1       | 143   | 0     | 0.39   |
| Seagate   | Momentus 5400.7 (AF)   | 2      | 15      | 522   | 421   | 0.39   |
| Toshiba   | 2.5" HDD MK..59GSXP    | 7      | 127     | 397   | 328   | 0.39   |
| Samsung   | SpinPoint P120         | 5      | 88      | 898   | 627   | 0.38   |
| Toshiba   | 2.5" HDD MQ01ABF       | 1      | 336     | 178   | 77    | 0.38   |
| Seagate   | Momentus 5400.7        | 1      | 9       | 466   | 436   | 0.37   |
| Hitachi   | Deskstar E7K1000       | 2      | 3       | 1464  | 64    | 0.37   |
| Toshiba   | 1.8" HDD               | 5      | 10      | 363   | 13    | 0.36   |
| Quantum   | Fireball lct15         | 3      | 3       | 226   | 2     | 0.36   |
| Seagate   | SpinPoint M8U (USB)    | 2      | 28      | 158   | 1     | 0.36   |
| Seagate   | Momentus 5400.6        | 10     | 868     | 454   | 491   | 0.36   |
| Seagate   | Laptop Ultrathin       | 1      | 1       | 131   | 0     | 0.36   |
| Seagate   | Momentus Thin          | 8      | 181     | 384   | 600   | 0.36   |
| Hitachi   | Travelstar 5K100       | 9      | 51      | 408   | 55    | 0.35   |
| Seagate   | Mobile HDD             | 3      | 351     | 151   | 88    | 0.35   |
| Hitachi   | Travelstar 5K160       | 11     | 162     | 501   | 69    | 0.35   |
| HGST      | Travelstar Z5K500      | 5      | 464     | 276   | 326   | 0.35   |
| Seagate   | Momentus 7200.1        | 2      | 8       | 513   | 412   | 0.34   |
| Toshiba   | 1.8" HDD MK..16GSG     | 1      | 3       | 272   | 4     | 0.34   |
| Toshiba   | 2.5" HDD L200 Slim     | 1      | 6       | 123   | 0     | 0.34   |
| Toshiba   | 2.5" HDD MK..59GSX     | 1      | 4       | 178   | 319   | 0.33   |
| Toshiba   | 2.5" HDD MK..65GSX     | 13     | 200     | 455   | 311   | 0.33   |
| HGST      | Travelstar Z5K1000     | 2      | 33      | 153   | 125   | 0.32   |
| Seagate   | SV35.2                 | 3      | 7       | 578   | 1005  | 0.32   |
| Hitachi   | Travelstar 5K120       | 2      | 4       | 384   | 5     | 0.32   |
| Toshiba   | 3.5" HDD DT01ACA       | 3      | 5       | 110   | 0     | 0.30   |
| Fujitsu   | MHT                    | 6      | 7       | 391   | 306   | 0.30   |
| WDC       | Black P10              | 1      | 1       | 110   | 0     | 0.30   |
| Seagate   | Ultra Mobile HDD       | 2      | 3       | 107   | 0     | 0.30   |
| HGST      | Deskstar 5K4000        | 1      | 1       | 107   | 0     | 0.29   |
| China     | Unknown                | 1      | 1       | 106   | 0     | 0.29   |
| Toshiba   | 2.5" HDD MK..76GSX     | 6      | 14      | 186   | 138   | 0.29   |
| Toshiba   | 2.5" HDD MK..55GSX     | 3      | 5       | 337   | 551   | 0.29   |
| Seagate   | Laptop Thin HDD        | 7      | 743     | 256   | 411   | 0.29   |
| Seagate   | SpinPoint M9TU (USB)   | 1      | 2       | 104   | 0     | 0.29   |
| HGST      | Ultrastar DC HC310     | 3      | 7       | 106   | 218   | 0.29   |
| Toshiba   | 2.5" HDD H200          | 2      | 4       | 103   | 0     | 0.28   |
| WDC       | Ultrastar He10/12      | 1      | 3       | 100   | 0     | 0.28   |
| Seagate   | BarraCuda 3.5          | 3      | 97      | 113   | 13    | 0.27   |
| IBM       | Deskstar 40GV & 75G... | 3      | 4       | 1041  | 24    | 0.27   |
| Seagate   | Unknown                | 3      | 3       | 158   | 1     | 0.27   |
| Toshiba   | V300                   | 1      | 1       | 97    | 0     | 0.27   |
| Toshiba   | 2.5" HDD MK..46GSX     | 1      | 11      | 401   | 42    | 0.27   |
| Toshiba   | 2.5" HDD MQ04UBD       | 1      | 6       | 135   | 4     | 0.27   |
| Seagate   | Laptop Thin SSHD       | 1      | 1       | 94    | 0     | 0.26   |
| Samsung   | SpinPoint M            | 2      | 9       | 301   | 19    | 0.25   |
| Hitachi   | Deskstar 5K4000        | 1      | 1       | 91    | 0     | 0.25   |
| Toshiba   | 2.5" HDD MK..46GSX     | 4      | 41      | 485   | 57    | 0.25   |
| Seagate   | Momentus 4200.2        | 5      | 6       | 433   | 350   | 0.25   |
| IBM/Hi... | Deskstar 60GXP         | 2      | 3       | 1032  | 106   | 0.24   |
| Toshiba   | 2.5" HDD MK..37GSX     | 2      | 47      | 517   | 101   | 0.24   |
| WDC       | White Label            | 1      | 2       | 87    | 0     | 0.24   |
| Seagate   | Barracuda 7200.11      | 12     | 336     | 837   | 346   | 0.24   |
| Toshiba   | 2.5" HDD MK..52GSX     | 5      | 66      | 556   | 133   | 0.23   |
| Toshiba   | 2.5" HDD MK..56GSY     | 5      | 15      | 167   | 223   | 0.22   |
| WDC       | Shrek LT 2.5           | 4      | 4       | 246   | 3     | 0.22   |
| HGST      | Ultrastar DC HC320     | 1      | 1       | 75    | 0     | 0.21   |
| Toshiba   | 2.5" HDD MQ04ABF       | 1      | 122     | 86    | 13    | 0.21   |
| Seagate   | LD25 Series            | 2      | 3       | 161   | 695   | 0.20   |
| Toshiba   | 2.5" HDD L200          | 2      | 14      | 92    | 81    | 0.20   |
| Toshiba   | 2.5" HDD MK..61GSY[N]  | 6      | 37      | 109   | 225   | 0.20   |
| Seagate   | Barracuda Pro Compute  | 2      | 72      | 80    | 15    | 0.20   |
| Seagate   | Ultra Mobile SSHD      | 2      | 2       | 320   | 241   | 0.19   |
| Toshiba   | 3.5" HDD N300          | 1      | 4       | 168   | 1     | 0.19   |
| Toshiba   | 2.5" HDD MQ02ABF       | 1      | 3       | 105   | 1     | 0.18   |
| HGST      | Travelstar Z5K500.B    | 1      | 17      | 65    | 0     | 0.18   |
| Seagate   | Momentus 5400.5        | 4      | 76      | 402   | 196   | 0.18   |
| WDC       | Scorpio EIDE           | 7      | 8       | 356   | 71    | 0.17   |
| Samsung   | SpinPoint M40/60/80    | 9      | 21      | 458   | 305   | 0.17   |
| Toshiba   | 1.8" HDD MK..33GSG     | 2      | 4       | 642   | 494   | 0.16   |
| WDC       | Unknown                | 3      | 3       | 464   | 5     | 0.15   |
| IBM/Hi... | Hitachi Travelstar ... | 4      | 13      | 348   | 41    | 0.15   |
| Hitachi   | Travelstar 4K40        | 1      | 6       | 456   | 186   | 0.14   |
| Seagate   | Constellation          | 1      | 1       | 2980  | 59    | 0.14   |
| Seagate   | SV35.3                 | 2      | 2       | 831   | 12    | 0.13   |
| Samsung   | SpinPoint M7U (USB)    | 2      | 3       | 46    | 0     | 0.13   |
| Samsung   | SpinPoint N2           | 2      | 2       | 46    | 1044  | 0.12   |
| Toshiba   | 2.5" HDD MQ02ABF..H    | 2      | 3       | 43    | 0     | 0.12   |
| IBM/Hi... | Travelstar 60GH and... | 2      | 3       | 109   | 3     | 0.10   |
| Toshiba   | 1.8" HDD MK..29GSG     | 2      | 4       | 361   | 568   | 0.10   |
| Toshiba   | 1.8" HDD               | 4      | 10      | 186   | 148   | 0.10   |
| Seagate   | Mobile USB Momentus    | 1      | 2       | 34    | 0     | 0.09   |
| HGST      | Travelstar Z7K500.B    | 1      | 2       | 33    | 0     | 0.09   |
| Toshiba   | Unknown                | 1      | 1       | 32    | 0     | 0.09   |
| Samsung   | SpinPoint M5           | 5      | 95      | 347   | 418   | 0.09   |
| MicroData | Unknown                | 1      | 1       | 288   | 8     | 0.09   |
| Samsung   | SpinPoint V40+         | 2      | 3       | 1003  | 159   | 0.08   |
| Seagate   | U8                     | 1      | 1       | 754   | 24    | 0.08   |
| Hitachi   | Travelstar DK23XX/D... | 4      | 5       | 344   | 104   | 0.08   |
| Maxtor    | DiamondMax 22          | 4      | 36      | 841   | 386   | 0.08   |
| WDC       | IU HA500               | 1      | 2       | 24    | 0     | 0.07   |
| Samsung   | SpinPoint M6           | 3      | 14      | 372   | 480   | 0.07   |
| WDC       | IU CB500               | 1      | 1       | 22    | 0     | 0.06   |
| CLOVER    | Unknown                | 1      | 1       | 22    | 0     | 0.06   |
| Toshiba   | 2.5" HDD MK..76GSX     | 5      | 78      | 42    | 250   | 0.06   |
| MediaMax  | WL250                  | 3      | 4       | 36    | 2     | 0.06   |
| WDC       | Internal Use HDD       | 3      | 9       | 21    | 0     | 0.06   |
| CLOVER    | Hightech Utania        | 2      | 3       | 19    | 0     | 0.05   |
| IBM       | Travelstar 25GS, 18... | 1      | 1       | 118   | 5     | 0.05   |
| Samsung   | HM100UX (S2 Portable)  | 1      | 1       | 177   | 8     | 0.05   |
| Maxtor    | Fireball 3             | 6      | 10      | 44    | 5     | 0.04   |
| Toshiba   | 2.5" HDD MK..65GSX     | 3      | 6       | 246   | 61    | 0.04   |
| Seagate   | Pipeline HD Pro        | 1      | 1       | 1038  | 72    | 0.04   |
| WDC       | Caviar WDxxxBA         | 1      | 1       | 296   | 20    | 0.04   |
| Seagate   | U10                    | 1      | 1       | 380   | 27    | 0.04   |
| Maxtor    | DiamondMax 10 (ATA/... | 20     | 49      | 24    | 127   | 0.04   |
| MARSHAL   | Unknown                | 2      | 3       | 217   | 18    | 0.03   |
| Seagate   | Pipeline HD 5900.1     | 2      | 4       | 444   | 58    | 0.03   |
| Seagate   | DB35.2                 | 2      | 2       | 1265  | 514   | 0.03   |
| Hitachi   | Travelstar 5K80        | 3      | 3       | 214   | 230   | 0.03   |
| Apple     | HGST Travelstar 5K750  | 2      | 4       | 254   | 59    | 0.03   |
| MediaMax  | WL2000                 | 1      | 1       | 33    | 2     | 0.03   |
| Toshiba   | 2.5" HDD               | 3      | 3       | 301   | 66    | 0.03   |
| LENOVO    | RE                     | 1      | 2       | 7     | 0     | 0.02   |
| Maxtor    | MaXLine III (ATA/13... | 4      | 6       | 16    | 40    | 0.02   |
| Seagate   | Lyrion                 | 1      | 1       | 7     | 0     | 0.02   |
| Toshiba   | 3.5" HDD P300          | 1      | 1       | 7     | 0     | 0.02   |
| Maxtor    | DiamondMax Plus 8      | 4      | 18      | 25    | 27    | 0.02   |
| HPE       | Unknown                | 1      | 1       | 6     | 0     | 0.02   |
| Hitachi   | Travelstar E7K100      | 1      | 1       | 4     | 0     | 0.01   |
| Fujitsu   | MHZ BJ                 | 1      | 1       | 4     | 0     | 0.01   |
| Maxtor    | DiamondMax Plus 9      | 11     | 79      | 29    | 175   | 0.01   |
| Maxtor    | Fireball 541DX         | 1      | 6       | 23    | 75    | 0.01   |
| Maxtor    | DiamondMax 16          | 2      | 3       | 37    | 28    | 0.01   |
| Hitachi   | Ultrastar 5K3000       | 1      | 1       | 1045  | 595   | 0.00   |
| Maxtor    | DiamondMax D540X-4D    | 2      | 5       | 17    | 157   | 0.00   |
| HP        | 1TB SATA disk GB100... | 1      | 1       | 2402  | 3024  | 0.00   |
| Maxtor    | DiamondMax D540X-4G    | 1      | 2       | 20    | 218   | 0.00   |
| MediaMax  | WL400                  | 1      | 1       | 0     | 0     | 0.00   |
| Apple     | Ultrastar A7K2000      | 1      | 1       | 83    | 113   | 0.00   |
| Maxtor    | MaXLine Plus II        | 1      | 2       | 25    | 38    | 0.00   |
| Seagate   | SV35.4                 | 1      | 1       | 685   | 1110  | 0.00   |
| Seagate   | Exos X16               | 1      | 4       | 0     | 0     | 0.00   |
| MediaMax  | WL6000                 | 1      | 1       | 637   | 1372  | 0.00   |
| Samsung   | USB Hard Disk          | 1      | 1       | 37    | 331   | 0.00   |
| Maxtor    | DiamondMax Plus 40 ... | 1      | 1       | 121   | 2068  | 0.00   |

HDD by Vendor
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days   — avg. days per sample,
Err    — avg. errors per sample,
MTBF   — avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF   |
|-------------|--------|---------|-------|-------|--------|
| HP          | 17     | 29      | 1287  | 119   | 2.37   |
| Quantum     | 6      | 6       | 642   | 1     | 1.63   |
| Apple       | 12     | 56      | 503   | 50    | 1.27   |
| WDC         | 1542   | 11833   | 599   | 42    | 1.16   |
| Hitachi     | 248    | 3307    | 683   | 178   | 1.07   |
| ExcelStor   | 8      | 17      | 764   | 13    | 1.01   |
| Samsung     | 134    | 1981    | 744   | 246   | 1.00   |
| Seagate     | 536    | 12535   | 572   | 203   | 0.91   |
| Fujitsu     | 78     | 344     | 485   | 141   | 0.76   |
| HGST        | 75     | 1406    | 358   | 218   | 0.71   |
| Toshiba     | 205    | 3505    | 326   | 110   | 0.57   |
| Maxtor      | 95     | 498     | 470   | 262   | 0.56   |
| Lenovo      | 1      | 1       | 165   | 0     | 0.45   |
| Magnetic... | 4      | 4       | 146   | 0     | 0.40   |
| IBM/Hitachi | 16     | 33      | 513   | 55    | 0.33   |
| China       | 1      | 1       | 106   | 0     | 0.29   |
| MediaMax    | 10     | 11      | 208   | 127   | 0.28   |
| IBM         | 4      | 5       | 857   | 20    | 0.23   |
| MicroData   | 1      | 1       | 288   | 8     | 0.09   |
| CLOVER      | 3      | 4       | 20    | 0     | 0.06   |
| MARSHAL     | 2      | 3       | 217   | 18    | 0.03   |
| LENOVO      | 1      | 2       | 7     | 0     | 0.02   |
| HPE         | 1      | 1       | 6     | 0     | 0.02   |

SSD by Model
------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days   — avg. days per sample,
Err    — avg. errors per sample,
MTBF   — avg. MTBF in years per sample.

See complete list of tested SSD samples in the Appendix 2 ([All_SSD.md](/All_SSD.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF   |
|-----------|--------------------|--------|---------|-------|-------|--------|
| Intel     | SSDSA2MH080G1GC    | 80 GB  | 1       | 2796  | 0     | 7.66   |
| OCZ       | AGILITY2           | 50 GB  | 1       | 2769  | 0     | 7.59   |
| Samsung   | MCCOE64G5MPP-0VA   | 64 GB  | 1       | 2540  | 0     | 6.96   |
| Corsair   | Force GT           | 50 GB  | 1       | 2387  | 0     | 6.54   |
| Samsung   | MZ7PC256HAFU-000L7 | 256 GB | 1       | 2371  | 0     | 6.50   |
| HPE       | MK0100GCTYU        | 100 GB | 1       | 2360  | 0     | 6.47   |
| Toshiba   | THNS128GG4BAAA-... | 128 GB | 1       | 2307  | 0     | 6.32   |
| Corsair   | CSSD-F40GB2-A      | 40 GB  | 1       | 2230  | 0     | 6.11   |
| Intel     | SSDSC2BB160G4      | 160 GB | 1       | 2027  | 0     | 5.55   |
| OCZ       | VERTEX2 3.5        | 240 GB | 1       | 1798  | 0     | 4.93   |
| Kingston  | SVP100S2512G       | 512 GB | 1       | 1795  | 0     | 4.92   |
| Intel     | SSDSC2BB800G4      | 800 GB | 2       | 1780  | 0     | 4.88   |
| Crucial   | M4-CT256M4SSD1     | 256 GB | 2       | 1713  | 0     | 4.70   |
| Toshiba   | THNSNJ256G8NU      | 256 GB | 1       | 1696  | 0     | 4.65   |
| OCZ       | VERTEX3            | 96 GB  | 1       | 1686  | 0     | 4.62   |
| Kingston  | SVP100S296G        | 96 GB  | 2       | 1638  | 0     | 4.49   |
| Crucial   | CT500MX200SSD3     | 500 GB | 1       | 1556  | 0     | 4.26   |
| OCZ       | VERTEX2            | 40 GB  | 2       | 1543  | 0     | 4.23   |
| Corsair   | Force 3 SSD        | 180 GB | 4       | 1926  | 1     | 4.19   |
| Intel     | SSDSC2BA100G3      | 100 GB | 20      | 1604  | 1     | 4.17   |
| Kingston  | SH100S3120G        | 120 GB | 3       | 1514  | 0     | 4.15   |
| Mushkin   | MKNSSDCR240GB      | 240 GB | 1       | 1513  | 0     | 4.15   |
| Intel     | SSDSC2BX400G4      | 400 GB | 1       | 1508  | 0     | 4.13   |
| OCZ       | VERTEX2 3.5        | 90 GB  | 1       | 1507  | 0     | 4.13   |
| SanDisk   | SD7SN6S512G1122    | 512 GB | 1       | 1488  | 0     | 4.08   |
| Toshiba   | THNS064GG2BNAA     | 64 GB  | 3       | 1484  | 0     | 4.07   |
| Intel     | SSDSC2BX200G4      | 200 GB | 1       | 1454  | 0     | 3.98   |
| Samsung   | SSD 830 Series     | 512 GB | 5       | 1432  | 0     | 3.92   |
| Intel     | SSDMCEAC120B3A     | 120 GB | 2       | 1373  | 0     | 3.76   |
| Samsung   | MZ7LN512HCHP-00000 | 512 GB | 2       | 1362  | 0     | 3.73   |
| Corsair   | Force GT           | 240 GB | 2       | 1634  | 1     | 3.73   |
| PNY       | CS1311 960GB SSD   | 960 GB | 1       | 1338  | 0     | 3.67   |
| Corsair   | Force 3 SSD        | 240 GB | 6       | 1285  | 0     | 3.52   |
| Samsung   | MZ7LN256HMJP-00000 | 256 GB | 2       | 1259  | 0     | 3.45   |
| Toshiba   | THNSNJ120PCSZ      | 120 GB | 2       | 1255  | 0     | 3.44   |
| Intel     | SSDSC2BP480G4      | 480 GB | 4       | 1247  | 0     | 3.42   |
| Toshiba   | THNSNJ128GMCU      | 128 GB | 1       | 1245  | 0     | 3.41   |
| Kingston  | SKC300S37A480G     | 480 GB | 1       | 1231  | 0     | 3.37   |
| Crucial   | C300-CTFDDAC256MAG | 256 GB | 3       | 1525  | 336   | 3.36   |
| Phison    | SATA SSD           | 16 GB  | 1       | 1213  | 0     | 3.32   |
| Corsair   | Force GT           | 180 GB | 3       | 1205  | 0     | 3.30   |
| Intel     | SSDSC2BB240G4      | 240 GB | 3       | 1196  | 0     | 3.28   |
| Toshiba   | THNSFC256GAMJ      | 256 GB | 2       | 1189  | 0     | 3.26   |
| OCZ       | SOLID3             | 64 GB  | 3       | 1345  | 5     | 3.21   |
| Seagate   | ST480HM000-1G5162  | 480 GB | 2       | 1282  | 1     | 3.20   |
| Micron    | MTFDDAK064MAR-1... | 64 GB  | 1       | 1164  | 0     | 3.19   |
| MyDigi... | SB M2 SSD          | 240 GB | 1       | 1161  | 0     | 3.18   |
| Samsung   | MZ7WD240HCFV-00003 | 240 GB | 1       | 1154  | 0     | 3.16   |
| OCZ       | VERTEX2            | 64 GB  | 9       | 1145  | 0     | 3.14   |
| Intel     | SSDSC2CW240A3      | 240 GB | 24      | 1132  | 0     | 3.10   |
| Samsung   | SSD PM830 2.5" 7mm | 256 GB | 6       | 1121  | 0     | 3.07   |
| SanDisk   | SD5SG2128G1052E    | 128 GB | 1       | 1121  | 0     | 3.07   |
| Samsung   | SSD PM800 2.5"     | 128 GB | 1       | 1115  | 0     | 3.06   |
| Samsung   | MZ7PD480HAGM-000DA | 480 GB | 1       | 1092  | 0     | 2.99   |
| Samsung   | SSD 840 EVO 120... | 120 GB | 4       | 1090  | 0     | 2.99   |
| Corsair   | Force GS           | 180 GB | 3       | 1087  | 0     | 2.98   |
| Micron    | M500_MTFDDAK480MAV | 480 GB | 1       | 1083  | 0     | 2.97   |
| Samsung   | SSD SM871 2.5 7mm  | 256 GB | 2       | 1083  | 0     | 2.97   |
| Samsung   | SSD 840 EVO        | 1 TB   | 17      | 1082  | 0     | 2.97   |
| Samsung   | SSD 830 Series     | 64 GB  | 8       | 1082  | 0     | 2.96   |
| Intel     | SSDSA2MH080G1HP    | 80 GB  | 1       | 1075  | 0     | 2.95   |
| Samsung   | MZHPV512HDGL-00000 | 512 GB | 2       | 1064  | 0     | 2.92   |
| Samsung   | SSD 850 EVO        | 2 TB   | 7       | 1042  | 0     | 2.86   |
| OCZ       | VERTEX2 3.5        | 120 GB | 1       | 1040  | 0     | 2.85   |
| Toshiba   | THNSNC128GMMJ      | 128 GB | 4       | 1030  | 0     | 2.82   |
| SanDisk   | SSD U110           | 32 GB  | 1       | 1009  | 0     | 2.76   |
| Hyundai   | 120GB SSD          | 120 GB | 1       | 997   | 0     | 2.73   |
| OCZ       | AGILITY4           | 128 GB | 5       | 994   | 0     | 2.73   |
| Samsung   | SSD 850 PRO        | 1 TB   | 18      | 983   | 0     | 2.69   |
| Apple     | SSD SM768E         | 752 GB | 1       | 982   | 0     | 2.69   |
| Samsung   | MZMPC256HBGJ-000H1 | 256 GB | 1       | 980   | 0     | 2.69   |
| WDC       | WD1001X06X-00SJVT0 | 1.1 TB | 1       | 969   | 0     | 2.66   |
| Patriot   | Ignite             | 480 GB | 1       | 967   | 0     | 2.65   |
| Samsung   | SSD 830 Series     | 128 GB | 24      | 960   | 0     | 2.63   |
| Crucial   | M4-CT128M4SSD2     | 128 GB | 30      | 996   | 135   | 2.60   |
| OCZ       | VECTOR             | 256 GB | 3       | 943   | 0     | 2.58   |
| Intel     | SSDSA2BW120G3A     | 120 GB | 1       | 939   | 0     | 2.58   |
| SanDisk   | SD7SB3Q-128G-1006  | 128 GB | 1       | 935   | 0     | 2.56   |
| Intel     | SSDSC2BB480G7      | 480 GB | 2       | 935   | 0     | 2.56   |
| PNY       | CS1311 480GB SSD   | 480 GB | 2       | 934   | 0     | 2.56   |
| Kingston  | SE50S3480G         | 480 GB | 10      | 1104  | 1     | 2.54   |
| SK hynix  | SC300 2.5 7MM      | 256 GB | 1       | 923   | 0     | 2.53   |
| Transcend | TS32GSSD370        | 32 GB  | 1       | 922   | 0     | 2.53   |
| Apple     | SSD SM1024F        | 1 TB   | 2       | 921   | 0     | 2.52   |
| SanDisk   | SDLF1CRR-019T-1HA2 | 1.9 TB | 1       | 916   | 0     | 2.51   |
| Samsung   | SSD 840 Series     | 500 GB | 5       | 971   | 1     | 2.51   |
| Intel     | SSDSA2CW080G3      | 80 GB  | 8       | 999   | 1     | 2.49   |
| Samsung   | MZ7PD128HAFV-000H7 | 128 GB | 3       | 903   | 0     | 2.47   |
| Toshiba   | THNSNF128GCSS      | 128 GB | 1       | 887   | 0     | 2.43   |
| Kingston  | SKC310S37A960G     | 960 GB | 1       | 885   | 0     | 2.43   |
| Intel     | SSDSC2CW180A3      | 180 GB | 10      | 884   | 0     | 2.42   |
| Corsair   | Neutron SSD        | 256 GB | 1       | 879   | 0     | 2.41   |
| MyDigi... | BP5                | 240 GB | 1       | 877   | 0     | 2.41   |
| Toshiba   | THNSNH256GMCT      | 256 GB | 3       | 875   | 0     | 2.40   |
| Samsung   | SSD PM800 2.5"     | 256 GB | 1       | 871   | 0     | 2.39   |
| Samsung   | MZ7LF128HCHP-00000 | 128 GB | 1       | 865   | 0     | 2.37   |
| Plextor   | PX-128M2S          | 128 GB | 2       | 863   | 0     | 2.37   |
| Apple     | SSD TS256A         | 256 GB | 1       | 858   | 0     | 2.35   |
| Samsung   | MZMPC032HBCD-000D1 | 32 GB  | 4       | 852   | 0     | 2.33   |
| SanDisk   | SD7SB6S128G1122    | 128 GB | 2       | 834   | 0     | 2.29   |
| Kingston  | RBU-SC100S37256GD  | 256 GB | 1       | 833   | 0     | 2.28   |
| Samsung   | SSD PM800 Serie... | 256 GB | 2       | 825   | 0     | 2.26   |
| Patriot   | Blast              | 480 GB | 1       | 823   | 0     | 2.26   |
| Samsung   | MZ7GE240HMGR-00003 | 240 GB | 1       | 822   | 0     | 2.25   |
| Kingston  | SNVP325S2512GB     | 512 GB | 1       | 822   | 0     | 2.25   |
| Innodisk  | DES25-64GM41BC1... | 64 GB  | 1       | 821   | 0     | 2.25   |
| ADATA     | XM11 256GB-V2      | 256 GB | 2       | 819   | 0     | 2.25   |
| Crucial   | M4-CT128M4SSD1     | 128 GB | 6       | 819   | 0     | 2.24   |
| Samsung   | MZHPV128HDGM-00000 | 128 GB | 2       | 818   | 0     | 2.24   |
| OCZ       | VERTEX2            | 120 GB | 6       | 810   | 0     | 2.22   |
| SanDisk   | SSD U110           | 128 GB | 1       | 807   | 0     | 2.21   |
| Transcend | TS64GMTS400S       | 64 GB  | 1       | 805   | 0     | 2.21   |
| OCZ       | VERTEX PLUS R2     | 64 GB  | 2       | 802   | 0     | 2.20   |
| OCZ       | DENRSTE251M45-0... | 100 GB | 1       | 801   | 0     | 2.20   |
| ADATA     | SSD S599           | 55 GB  | 1       | 801   | 0     | 2.20   |
| Samsung   | MZ7PC128HAFU-000H1 | 128 GB | 2       | 799   | 0     | 2.19   |
| SanDisk   | SD6SP1M128G1102    | 128 GB | 2       | 797   | 0     | 2.18   |
| OCZ       | VERTEX PLUS R2     | 247 GB | 1       | 797   | 0     | 2.18   |
| Intel     | SSDSA2SH032G1GN    | 32 GB  | 1       | 795   | 0     | 2.18   |
| Samsung   | MZ7KM480HMHQ-00005 | 480 GB | 2       | 794   | 0     | 2.18   |
| Toshiba   | THNSNH060GMCT      | 64 GB  | 1       | 787   | 0     | 2.16   |
| Samsung   | SSD CM871 M.2 2280 | 128 GB | 1       | 785   | 0     | 2.15   |
| Micron    | C400-MTFDDAC256MAM | 256 GB | 1       | 780   | 0     | 2.14   |
| Corsair   | Force GS           | 90 GB  | 1       | 776   | 0     | 2.13   |
| Samsung   | MZ7PD256HAFV-000H7 | 256 GB | 3       | 775   | 0     | 2.12   |
| Samsung   | SSD SM871 2.5 7mm  | 512 GB | 1       | 773   | 0     | 2.12   |
| Lite-On   | ECE-240NAS         | 240 GB | 1       | 766   | 0     | 2.10   |
| SK hynix  | SC308 SATA         | 512 GB | 2       | 766   | 0     | 2.10   |
| Samsung   | MZ7KM480HAHP-00005 | 480 GB | 1       | 765   | 0     | 2.10   |
| Kingston  | SVP200S37A480G     | 480 GB | 1       | 765   | 0     | 2.10   |
| Innodisk  | 2.5" SATA SSD 3ME3 | 64 GB  | 1       | 760   | 0     | 2.08   |
| SanDisk   | SD6SB1M-256G-1006  | 256 GB | 1       | 757   | 0     | 2.08   |
| Patriot   | Flare              | 120 GB | 1       | 753   | 0     | 2.06   |
| PNY       | SSD2SC480G1CS27... | 480 GB | 3       | 742   | 0     | 2.03   |
| Transcend | TS128GSSD340       | 128 GB | 6       | 738   | 0     | 2.02   |
| Samsung   | MZ7PC128HAFU-000L1 | 128 GB | 1       | 737   | 0     | 2.02   |
| Intel     | SSDSA2CT040G3      | 40 GB  | 5       | 734   | 0     | 2.01   |
| SanDisk   | SD5SE2128G1002E    | 128 GB | 2       | 729   | 0     | 2.00   |
| Mushkin   | MKNSSDAT60GB-DX    | 64 GB  | 1       | 728   | 0     | 2.00   |
| Samsung   | SSD 840 PRO Series | 512 GB | 10      | 1165  | 12    | 1.99   |
| Samsung   | MZ7PA256HMDR-010H1 | 256 GB | 2       | 842   | 520   | 1.98   |
| Micro ... | G2 series          | 64 GB  | 1       | 722   | 0     | 1.98   |
| Samsung   | SSD 840 PRO Series | 128 GB | 34      | 831   | 8     | 1.98   |
| Crucial   | CT512M550SSD1      | 512 GB | 3       | 828   | 15    | 1.97   |
| Intel     | SSDSC2BW240A3L     | 240 GB | 4       | 716   | 0     | 1.96   |
| Samsung   | MZ7TD256HAFV-000L9 | 256 GB | 3       | 714   | 0     | 1.96   |
| OCZ       | NOCTI              | 64 GB  | 1       | 704   | 0     | 1.93   |
| Samsung   | SSD 840 Series     | 250 GB | 24      | 735   | 2     | 1.92   |
| Crucial   | M4-CT256M4SSD2     | 256 GB | 18      | 840   | 170   | 1.91   |
| Kingston  | SVP100S2128G       | 128 GB | 1       | 698   | 0     | 1.91   |
| Samsung   | MZ7TD256HAFV-000L7 | 256 GB | 7       | 695   | 0     | 1.91   |
| Samsung   | SSD 850 PRO        | 128 GB | 30      | 692   | 0     | 1.90   |
| SanDisk   | SD6SF1M064G1022    | 64 GB  | 1       | 691   | 0     | 1.89   |
| Intel     | SSDSC2BP240G4      | 240 GB | 4       | 691   | 0     | 1.89   |
| Kingston  | SVP200S360G        | 64 GB  | 5       | 688   | 0     | 1.89   |
| Kingston  | SVP200S390G        | 90 GB  | 1       | 686   | 0     | 1.88   |
| SK hynix  | HFS512G32MND-3312A | 512 GB | 1       | 686   | 0     | 1.88   |
| Samsung   | MZ7TE512HMHP-000L2 | 512 GB | 3       | 685   | 0     | 1.88   |
| Samsung   | SSD 850 EVO M.2    | 120 GB | 4       | 677   | 0     | 1.86   |
| Seagate   | 2E256-TU2-510B00   | 170 GB | 3       | 2072  | 1366  | 1.85   |
| Kingston  | SNVP325S2128GB     | 128 GB | 1       | 674   | 0     | 1.85   |
| KingDian  | N400               | 240 GB | 1       | 670   | 0     | 1.84   |
| Mushkin   | MKNSSDCR120GB      | 120 GB | 2       | 1370  | 4     | 1.84   |
| Corsair   | Force 3 SSD        | 120 GB | 16      | 791   | 69    | 1.83   |
| Toshiba   | THNSFJ256GDNU A    | 256 GB | 3       | 668   | 0     | 1.83   |
| Samsung   | SSD 830 Series     | 256 GB | 16      | 699   | 64    | 1.83   |
| Kingston  | RBU-SNS8152S3128GF | 128 GB | 1       | 665   | 0     | 1.82   |
| Intel     | SSDSC2CT180A3      | 180 GB | 4       | 662   | 0     | 1.82   |
| Samsung   | MZ7TE256HMHP-00000 | 256 GB | 2       | 659   | 0     | 1.81   |
| ADATA     | SSD S510           | 120 GB | 7       | 675   | 1     | 1.80   |
| Apple     | SSD SM0512F        | 500 GB | 3       | 656   | 0     | 1.80   |
| OCZ       | VERTEX3 MI         | 240 GB | 2       | 1285  | 2     | 1.78   |
| Intel     | SSDSCMMW180A3L     | 180 GB | 2       | 646   | 0     | 1.77   |
| Kingston  | SV200S364G         | 64 GB  | 2       | 645   | 0     | 1.77   |
| Crucial   | M4-CT512M4SSD2     | 512 GB | 4       | 1331  | 253   | 1.77   |
| Kingston  | SMS100S264G        | 64 GB  | 3       | 643   | 0     | 1.76   |
| OCZ       | VECTOR180          | 240 GB | 2       | 641   | 0     | 1.76   |
| Crucial   | M4-CT064M4SSD2     | 64 GB  | 15      | 805   | 139   | 1.76   |
| Samsung   | SSD 840 EVO        | 250 GB | 105     | 658   | 11    | 1.75   |
| Apple     | SSD SD512E         | 500 GB | 1       | 636   | 0     | 1.74   |
| Kingston  | SH103S390G         | 90 GB  | 1       | 636   | 0     | 1.74   |
| Samsung   | MZ7TE128HMGR-000L1 | 128 GB | 3       | 635   | 0     | 1.74   |
| Kingston  | SKC400S37512G      | 512 GB | 4       | 632   | 0     | 1.73   |
| ADATA     | SSD S510           | 64 GB  | 2       | 631   | 0     | 1.73   |
| Toshiba   | THNSNF512GCSS      | 512 GB | 1       | 631   | 0     | 1.73   |
| SanDisk   | SDSSDHII480G       | 480 GB | 9       | 631   | 0     | 1.73   |
| Samsung   | SSD PM810 FDE 2.5" | 256 GB | 1       | 630   | 0     | 1.73   |
| Samsung   | SSD 840 PRO Series | 256 GB | 49      | 630   | 0     | 1.73   |
| Crucial   | CT120M500SSD3      | 120 GB | 3       | 771   | 11    | 1.72   |
| OCZ       | AGILITY3           | 64 GB  | 40      | 811   | 3     | 1.71   |
| Kingston  | SVP200S37A240G     | 240 GB | 1       | 623   | 0     | 1.71   |
| Samsung   | SSD 850 PRO        | 512 GB | 46      | 639   | 23    | 1.71   |
| SK hynix  | HFS256G39MND-2300A | 256 GB | 1       | 621   | 0     | 1.70   |
| PNY       | CS1311 240GB SSD   | 240 GB | 6       | 619   | 0     | 1.70   |
| BLueRay   | SDM9SI128A         | 128 GB | 1       | 619   | 0     | 1.70   |
| Corsair   | Force GT           | 120 GB | 12      | 706   | 1     | 1.69   |
| Samsung   | MZMPA128HMFU-00000 | 128 GB | 1       | 616   | 0     | 1.69   |
| Samsung   | SSD 840 EVO        | 120 GB | 81      | 614   | 0     | 1.68   |
| Intel     | SSDSC2CT060A3      | 64 GB  | 6       | 613   | 0     | 1.68   |
| ADATA     | SP600              | 256 GB | 4       | 611   | 0     | 1.68   |
| Samsung   | SSD 840 EVO        | 500 GB | 28      | 651   | 1     | 1.66   |
| Corsair   | Force 3 SSD        | 480 GB | 1       | 598   | 0     | 1.64   |
| Samsung   | SSD 850 EVO        | 4 TB   | 2       | 597   | 0     | 1.64   |
| Corsair   | CSSD-V64GB2        | 64 GB  | 2       | 597   | 0     | 1.64   |
| SanDisk   | SD7SN6S512G1001    | 512 GB | 1       | 593   | 0     | 1.63   |
| OCZ       | VERTEX4            | 256 GB | 21      | 842   | 1     | 1.62   |
| SanDisk   | SD7TB3Q-256G-1006  | 256 GB | 3       | 590   | 0     | 1.62   |
| Corsair   | Force 3 SSD        | 64 GB  | 13      | 624   | 1     | 1.61   |
| Toshiba   | THNSFJ256GCSU      | 256 GB | 6       | 587   | 0     | 1.61   |
| Samsung   | MZ7PD128HCFV-000H1 | 128 GB | 3       | 585   | 0     | 1.60   |
| OCZ       | DENCSTE351M16-0... | 240 GB | 1       | 585   | 0     | 1.60   |
| OCZ       | D2RSTK251E19-0200  | 200 GB | 1       | 584   | 0     | 1.60   |
| SanDisk   | SD6SN1M128G        | 128 GB | 1       | 584   | 0     | 1.60   |
| OCZ       | VERTEX2            | 115 GB | 1       | 581   | 0     | 1.59   |
| Intel     | SSDSC2BA400G3      | 400 GB | 1       | 580   | 0     | 1.59   |
| Micron    | 5200_MTFDDAK1T9TDC | 1.9 TB | 11      | 612   | 1     | 1.58   |
| SATADOM   | SL 3ME3 V2         | 128 GB | 1       | 574   | 0     | 1.57   |
| SanDisk   | SD8SB8U256G1122    | 256 GB | 5       | 572   | 0     | 1.57   |
| Intel     | SSDSC2CT080A4      | 80 GB  | 4       | 568   | 0     | 1.56   |
| OCZ       | AGILITY4           | 64 GB  | 1       | 567   | 0     | 1.56   |
| Samsung   | MZ7KM480HMHQ0D3    | 480 GB | 6       | 565   | 0     | 1.55   |
| OCZ       | REVODRIVE3         | 64 GB  | 4       | 564   | 0     | 1.55   |
| Samsung   | MZMPC128HBFU-000L1 | 128 GB | 1       | 559   | 0     | 1.53   |
| Patriot   | Torch LE           | 240 GB | 1       | 558   | 0     | 1.53   |
| WDC       | WDS200T2B0B-00YS70 | 2 TB   | 1       | 555   | 0     | 1.52   |
| Intel     | SSDSC2BA200G4      | 200 GB | 7       | 636   | 1     | 1.52   |
| Samsung   | SSD PM830 2.5" 7mm | 128 GB | 7       | 825   | 145   | 1.52   |
| OCZ       | AGILITY3           | 120 GB | 35      | 725   | 85    | 1.52   |
| Samsung   | SSD PM830 mSATA    | 128 GB | 2       | 551   | 0     | 1.51   |
| Toshiba   | THNSNH128GCST      | 128 GB | 1       | 549   | 0     | 1.51   |
| SanDisk   | SD6SB1M256G1002    | 256 GB | 1       | 548   | 0     | 1.50   |
| SK hynix  | HFS512G32MND-3210A | 512 GB | 1       | 547   | 0     | 1.50   |
| SK hynix  | SC300 SATA         | 512 GB | 1       | 546   | 0     | 1.50   |
| SanDisk   | SD7SB3Q-256G-1006  | 256 GB | 3       | 545   | 0     | 1.50   |
| Intel     | SSDSC2MH120A2      | 120 GB | 3       | 545   | 0     | 1.49   |
| Plextor   | PX-512M7VC         | 512 GB | 2       | 544   | 0     | 1.49   |
| Intel     | SSDSC2CT240A4      | 240 GB | 7       | 542   | 0     | 1.49   |
| OCZ       | VERTEX2 3.5        | 115 GB | 1       | 541   | 0     | 1.48   |
| Samsung   | SSD 850 PRO        | 2 TB   | 2       | 537   | 0     | 1.47   |
| Phison    | SM280128GPTC15T... | 128 GB | 1       | 535   | 0     | 1.47   |
| Intel     | SSDSC2CT120A3      | 120 GB | 17      | 923   | 1     | 1.46   |
| Samsung   | MZ7LN256HMJP-000H1 | 256 GB | 5       | 530   | 0     | 1.45   |
| HP        | VK000240GWJPD      | 240 GB | 1       | 529   | 0     | 1.45   |
| SanDisk   | SD6SB2M128G1022I   | 128 GB | 2       | 528   | 0     | 1.45   |
| SK hynix  | SC300 M.2 2280     | 256 GB | 3       | 528   | 0     | 1.45   |
| Intel     | SSDSA2M080G2GC     | 80 GB  | 16      | 1100  | 5     | 1.45   |
| SanDisk   | SD6SP1M128G1002    | 128 GB | 3       | 524   | 0     | 1.44   |
| Samsung   | SSD PM830 mSATA    | 32 GB  | 8       | 524   | 0     | 1.44   |
| Samsung   | SSD 840 EVO 250... | 250 GB | 6       | 524   | 0     | 1.44   |
| Goodram   | C100               | 120 GB | 2       | 523   | 0     | 1.44   |
| OCZ       | VERTEX3            | 64 GB  | 26      | 590   | 2     | 1.43   |
| Samsung   | MZ7PC128HAFU-000   | 128 GB | 3       | 521   | 0     | 1.43   |
| Micron    | 1100_MTFDDAK512TBN | 512 GB | 11      | 777   | 99    | 1.41   |
| SanDisk   | SD7UB2Q512G1122    | 512 GB | 2       | 514   | 0     | 1.41   |
| Micron    | C400-MTFDDAK256MAM | 256 GB | 2       | 513   | 0     | 1.41   |
| Kingston  | SEDC400S37960G     | 960 GB | 1       | 513   | 0     | 1.41   |
| Apple     | SSD SM0256F        | 256 GB | 6       | 512   | 0     | 1.41   |
| ADATA     | SSD S599           | 115 GB | 1       | 511   | 0     | 1.40   |
| SanDisk   | SD8SBBU480G1122    | 480 GB | 2       | 511   | 0     | 1.40   |
| Toshiba   | THNSNH128GBST      | 128 GB | 3       | 510   | 0     | 1.40   |
| Toshiba   | TL100              | 120 GB | 1       | 509   | 0     | 1.40   |
| Samsung   | SSD 850 PRO        | 256 GB | 92      | 517   | 1     | 1.39   |
| Kingston  | SV200S3128G        | 128 GB | 8       | 504   | 0     | 1.38   |
| Samsung   | MZ7PA128HMCD-010L1 | 128 GB | 1       | 504   | 0     | 1.38   |
| Verbatim  | SATA-III SSD       | 256 GB | 1       | 503   | 0     | 1.38   |
| OCZ       | D2RSTK251E14-0400  | 400 GB | 1       | 502   | 0     | 1.38   |
| SanDisk   | SDSSDP064G         | 64 GB  | 14      | 518   | 74    | 1.37   |
| Samsung   | MZNLF128HCHP-00000 | 128 GB | 6       | 497   | 0     | 1.36   |
| Corsair   | Force GT           | 90 GB  | 4       | 610   | 1     | 1.36   |
| Samsung   | MZ7PD256HCGM-000H7 | 256 GB | 5       | 534   | 489   | 1.36   |
| SanDisk   | SD7SN6S-512G-1006  | 512 GB | 2       | 496   | 0     | 1.36   |
| OCZ       | VERTEX460A         | 240 GB | 3       | 494   | 0     | 1.35   |
| OCZ       | VERTEX4            | 128 GB | 67      | 557   | 1     | 1.35   |
| Transcend | TS128GSSD320       | 128 GB | 1       | 493   | 0     | 1.35   |
| Toshiba   | VT180              | 480 GB | 2       | 492   | 0     | 1.35   |
| Kingston  | RBU-SNS8100S3256GD | 256 GB | 2       | 487   | 0     | 1.34   |
| SanDisk   | SDSSDHP256G        | 256 GB | 13      | 487   | 0     | 1.34   |
| Apple     | SSD TS256C         | 256 GB | 4       | 483   | 0     | 1.32   |
| Samsung   | MMCQE28G8MUP-0VA   | 128 GB | 2       | 825   | 1     | 1.32   |
| SPCC      | SSD110             | 64 GB  | 4       | 482   | 0     | 1.32   |
| Samsung   | SSD 850 EVO        | 500 GB | 241     | 482   | 0     | 1.32   |
| Samsung   | SSD 850 EVO        | 1 TB   | 60      | 557   | 1     | 1.32   |
| Goodram   | SSD                | 64 GB  | 1       | 480   | 0     | 1.32   |
| Samsung   | SG9MSM6D024GPM00   | 22 GB  | 4       | 480   | 0     | 1.32   |
| Samsung   | MZ7LN512HAJQ-00000 | 512 GB | 7       | 480   | 0     | 1.32   |
| Samsung   | MZMPC032HBCD-00000 | 32 GB  | 7       | 479   | 0     | 1.31   |
| Samsung   | MZNLN256HMHQ-00000 | 256 GB | 6       | 479   | 0     | 1.31   |
| Toshiba   | Q300 Pro           | 256 GB | 2       | 478   | 0     | 1.31   |
| SanDisk   | SSD i100           | 32 GB  | 3       | 474   | 0     | 1.30   |
| SanDisk   | SD8SBBU240G1122    | 240 GB | 2       | 474   | 0     | 1.30   |
| Samsung   | MZMTD512HAGL-000MV | 512 GB | 1       | 473   | 0     | 1.30   |
| SanDisk   | SDSSDH240GG25      | 240 GB | 1       | 473   | 0     | 1.30   |
| Toshiba   | THNSNF128GMCS      | 128 GB | 2       | 471   | 0     | 1.29   |
| Goodram   | C40                | 120 GB | 4       | 471   | 0     | 1.29   |
| SanDisk   | SDSSDHII960G       | 960 GB | 1       | 470   | 0     | 1.29   |
| Verbatim  | SATA-III SSD       | 128 GB | 1       | 470   | 0     | 1.29   |
| KingSpec  | SPK-SF12-M120      | 120 GB | 1       | 468   | 0     | 1.28   |
| Kingston  | SH103S3120G        | 120 GB | 56      | 518   | 1     | 1.28   |
| Samsung   | SSD PM800 TM       | 128 GB | 1       | 468   | 0     | 1.28   |
| Samsung   | SSD 750 EVO        | 500 GB | 13      | 467   | 0     | 1.28   |
| Toshiba   | THNSNH060GCST      | 64 GB  | 1       | 467   | 0     | 1.28   |
| Plextor   | PX-64M2S           | 64 GB  | 2       | 467   | 0     | 1.28   |
| OCZ       | AGILITY3           | 240 GB | 10      | 690   | 19    | 1.28   |
| Micron    | 5100_MTFDDAK1T9TBY | 1.9 TB | 3       | 1010  | 110   | 1.28   |
| Intel     | SSDSC2BW180A3L     | 180 GB | 8       | 479   | 1     | 1.27   |
| Mushkin   | MKNSSDTR128GB-3DL  | 128 GB | 1       | 464   | 0     | 1.27   |
| SanDisk   | SD7SN6S-256G-1006  | 256 GB | 1       | 463   | 0     | 1.27   |
| ADATA     | SSD S396           | 32 GB  | 1       | 462   | 0     | 1.27   |
| Plextor   | PX-128M3           | 128 GB | 3       | 462   | 0     | 1.27   |
| Kingston  | SVP200S37A60G      | 64 GB  | 11      | 461   | 0     | 1.26   |
| Toshiba   | THNSNH512GCST      | 512 GB | 1       | 461   | 0     | 1.26   |
| Crucial   | CT1050MX300SSD1    | 1 TB   | 11      | 555   | 1     | 1.26   |
| WDC       | WDBNCE2500PNC-WRSN | 250 GB | 1       | 457   | 0     | 1.25   |
| Samsung   | MZ7LF128HCHP-00004 | 128 GB | 2       | 457   | 0     | 1.25   |
| Crucial   | CT500MX200SSD1     | 500 GB | 12      | 457   | 0     | 1.25   |
| Samsung   | MZHPV256HDGL-00000 | 256 GB | 1       | 455   | 0     | 1.25   |
| Samsung   | MZ7PC256HAFU-000H1 | 256 GB | 1       | 452   | 0     | 1.24   |
| Toshiba   | THNSNJ128GCSU      | 128 GB | 6       | 451   | 0     | 1.24   |
| Samsung   | MZ7TE128HMGR-00004 | 128 GB | 4       | 450   | 0     | 1.24   |
| HP        | SSD S700           | 120 GB | 2       | 448   | 0     | 1.23   |
| Crucial   | CT512MX100SSD1     | 512 GB | 15      | 522   | 1     | 1.23   |
| SanDisk   | SDSSDXPS240G       | 240 GB | 6       | 453   | 173   | 1.23   |
| WDC       | WDS500G1B0B-00AS40 | 500 GB | 7       | 447   | 0     | 1.23   |
| OCZ       | VERTEX3            | 120 GB | 52      | 688   | 48    | 1.23   |
| Kingston  | SH100S3240G        | 240 GB | 3       | 1083  | 2     | 1.23   |
| Innodisk  | Corp. DRPS-02GJ... | 2 GB   | 1       | 444   | 0     | 1.22   |
| Crucial   | CT240M500SSD3      | 240 GB | 4       | 522   | 8     | 1.22   |
| Foxline   | FLDMMS128G         | 128 GB | 1       | 443   | 0     | 1.22   |
| ADATA     | SSD                | 32 GB  | 1       | 442   | 0     | 1.21   |
| OCZ       | VERTEX2            | 80 GB  | 1       | 442   | 0     | 1.21   |
| Corsair   | Force GT           | 64 GB  | 5       | 690   | 7     | 1.21   |
| Samsung   | SSD 850 EVO        | 120 GB | 68      | 441   | 0     | 1.21   |
| OCZ       | REVODRIVE X2       | 25 GB  | 4       | 435   | 0     | 1.19   |
| SanDisk   | SD8SN8U256G1122    | 256 GB | 1       | 434   | 0     | 1.19   |
| ADATA     | SP600              | 128 GB | 7       | 434   | 0     | 1.19   |
| Phison    | SSDS30256XQC800... | 240 GB | 1       | 433   | 0     | 1.19   |
| Crucial   | CT256MX100SSD1     | 256 GB | 30      | 471   | 16    | 1.19   |
| Micron    | M600_MTFDDAV256MBF | 256 GB | 5       | 431   | 0     | 1.18   |
| Samsung   | SSD 850 EVO        | 250 GB | 287     | 432   | 1     | 1.18   |
| ADATA     | SSD S511           | 120 GB | 1       | 430   | 0     | 1.18   |
| WDC       | WDS100T1B0B-00AS40 | 1 TB   | 2       | 430   | 0     | 1.18   |
| SanDisk   | Ultra II           | 960 GB | 14      | 470   | 1     | 1.18   |
| Samsung   | SMART SSD Xceed... | 32 GB  | 3       | 429   | 0     | 1.18   |
| Samsung   | MZRPC128HACD-000SO | 64 GB  | 2       | 429   | 0     | 1.18   |
| Toshiba   | THNS128GG4BBAA     | 128 GB | 1       | 427   | 0     | 1.17   |
| PNY       | CS1311 120GB SSD   | 120 GB | 4       | 425   | 0     | 1.17   |
| Intel     | SSDSA2CW120G3      | 120 GB | 7       | 425   | 0     | 1.17   |
| Samsung   | MZ7LN256HCHP-000F0 | 256 GB | 1       | 425   | 0     | 1.16   |
| Transcend | TS480GJDM725       | 480 GB | 1       | 424   | 0     | 1.16   |
| SanDisk   | SD6SB2M-512G-1006  | 512 GB | 3       | 423   | 0     | 1.16   |
| SanDisk   | SDSSDX240GG25      | 240 GB | 3       | 927   | 4     | 1.16   |
| Toshiba   | THNSNJ256GCST      | 256 GB | 1       | 421   | 0     | 1.15   |
| Samsung   | MZ7LM480HCHP-00... | 480 GB | 2       | 421   | 0     | 1.15   |
| Kingston  | SKC380S360G        | 64 GB  | 1       | 420   | 0     | 1.15   |
| OCZ       | SOLID3             | 120 GB | 1       | 418   | 0     | 1.15   |
| SanDisk   | SD6SB1M128G1001    | 128 GB | 2       | 416   | 0     | 1.14   |
| PNY       | SSD2SC480G1CS27... | 480 GB | 1       | 415   | 0     | 1.14   |
| Kingston  | SUV400S37960G      | 960 GB | 1       | 415   | 0     | 1.14   |
| Intel     | SSDMAEMC040G2      | 40 GB  | 1       | 414   | 0     | 1.13   |
| Samsung   | MZ7TD128HAFV-000L1 | 128 GB | 11      | 412   | 0     | 1.13   |
| Toshiba   | Q300 Pro           | 512 GB | 1       | 411   | 0     | 1.13   |
| Kingston  | SM2280S3240G       | 240 GB | 2       | 410   | 0     | 1.13   |
| Samsung   | MMCRE28G5MXP-0VBH1 | 128 GB | 1       | 410   | 0     | 1.12   |
| Samsung   | MZYTN512HDJH-000L2 | 512 GB | 1       | 410   | 0     | 1.12   |
| Samsung   | MZ7LN512HMJP-000L7 | 512 GB | 3       | 406   | 0     | 1.11   |
| Samsung   | SSD 750 EVO        | 250 GB | 37      | 405   | 0     | 1.11   |
| Samsung   | MZ7LN128HCHP-000L1 | 128 GB | 3       | 405   | 0     | 1.11   |
| SanDisk   | SDSSDHP128G        | 128 GB | 27      | 413   | 1     | 1.11   |
| SPCC      | SSD110             | 120 GB | 6       | 673   | 339   | 1.11   |
| SanDisk   | SDSSDH2256G        | 256 GB | 1       | 403   | 0     | 1.10   |
| OCZ       | VERTEX3            | 128 GB | 2       | 402   | 0     | 1.10   |
| Kingston  | SMS200S3240G       | 240 GB | 2       | 402   | 0     | 1.10   |
| Toshiba   | THNSNH060GBST      | 64 GB  | 2       | 400   | 0     | 1.10   |
| Samsung   | SSD 840 EVO        | 752 GB | 2       | 399   | 0     | 1.09   |
| Mushkin   | MKNSSDTR480GB-3DL  | 480 GB | 1       | 398   | 0     | 1.09   |
| Kingston  | SH103S3240G        | 240 GB | 16      | 536   | 136   | 1.09   |
| Samsung   | MZNLN128HCGR-00000 | 128 GB | 1       | 396   | 0     | 1.09   |
| Apple     | SSD SM0512G        | 500 GB | 6       | 396   | 0     | 1.09   |
| Samsung   | SSD 850 EVO M.2    | 500 GB | 21      | 394   | 0     | 1.08   |
| Micron    | MTFDDAT128MAM-1J2  | 128 GB | 2       | 450   | 548   | 1.07   |
| Toshiba   | Q300               | 480 GB | 4       | 391   | 0     | 1.07   |
| Kingston  | SV100S232G         | 32 GB  | 4       | 390   | 0     | 1.07   |
| Kingston  | SUV300S37A480G     | 480 GB | 2       | 389   | 0     | 1.07   |
| Micron    | MTFDDAK512MBF-1... | 512 GB | 4       | 483   | 4     | 1.07   |
| OCZ       | AGILITY3           | 128 GB | 3       | 749   | 1     | 1.07   |
| Smartbuy  | SSD                | 64 GB  | 6       | 386   | 0     | 1.06   |
| SanDisk   | SDSSDX120GG25      | 120 GB | 8       | 385   | 0     | 1.06   |
| Kingston  | SVP200S37A120G     | 120 GB | 8       | 747   | 216   | 1.05   |
| Lite-On   | LAT-128M2S         | 128 GB | 1       | 384   | 0     | 1.05   |
| Samsung   | MMCRE28GFMXP-MVB   | 128 GB | 2       | 383   | 0     | 1.05   |
| Crucial   | CT275MX300SSD4     | 275 GB | 7       | 383   | 1     | 1.05   |
| Samsung   | MZ7TE128HMGR-00000 | 128 GB | 2       | 382   | 0     | 1.05   |
| Kingston  | SM2280S3G2240G     | 240 GB | 2       | 380   | 0     | 1.04   |
| SanDisk   | SD8SN8U512G1122    | 512 GB | 3       | 380   | 0     | 1.04   |
| Samsung   | SSD 850 EVO mSATA  | 500 GB | 9       | 379   | 0     | 1.04   |
| Samsung   | SATA SSD           | 256 GB | 1       | 379   | 0     | 1.04   |
| Samsung   | MZ7LF120HCHP-000L1 | 120 GB | 3       | 379   | 0     | 1.04   |
| SanDisk   | SDSSDXP240G        | 240 GB | 4       | 379   | 0     | 1.04   |
| Kingston  | SMSM150S324G2      | 24 GB  | 2       | 378   | 0     | 1.04   |
| OCZ       | VERTEX3            | 90 GB  | 12      | 669   | 7     | 1.04   |
| Corsair   | Force 3 SSD        | 90 GB  | 5       | 378   | 0     | 1.04   |
| OCZ       | VERTEX4            | 64 GB  | 8       | 379   | 1     | 1.03   |
| Lite-On   | LCS-256L9S-11 2... | 256 GB | 3       | 377   | 0     | 1.03   |
| Samsung   | SSD PM800 TM       | 64 GB  | 1       | 377   | 0     | 1.03   |
| SanDisk   | SD7SB6S-128G-1006  | 128 GB | 3       | 573   | 2     | 1.03   |
| Samsung   | SSD 850 EVO mSATA  | 1 TB   | 4       | 374   | 0     | 1.03   |
| OCZ       | REVODRIVE3         | 120 GB | 2       | 373   | 0     | 1.02   |
| Samsung   | MZNTE256HMHP-000H1 | 256 GB | 1       | 373   | 0     | 1.02   |
| Samsung   | MZNLN256HCHP-000L7 | 256 GB | 7       | 372   | 0     | 1.02   |
| SanDisk   | SD8TB8U256G1001    | 256 GB | 5       | 371   | 0     | 1.02   |
| Samsung   | MZYTY256HDHP-000L2 | 256 GB | 3       | 370   | 0     | 1.01   |
| OCZ       | VECTOR150          | 240 GB | 6       | 369   | 0     | 1.01   |
| Intel     | SSDSC2BW240A3H     | 240 GB | 1       | 369   | 0     | 1.01   |
| Toshiba   | THNS064GE4BBDC     | 64 GB  | 2       | 369   | 0     | 1.01   |
| OCZ       | VERTEX3            | 240 GB | 9       | 692   | 143   | 1.01   |
| OCZ       | VERTEX3 MI         | 120 GB | 16      | 526   | 126   | 1.01   |
| Toshiba   | THNSNC128GCSJ      | 128 GB | 1       | 367   | 0     | 1.01   |
| Crucial   | CT275MX300SSD1     | 275 GB | 30      | 382   | 4     | 1.01   |
| Kingston  | SNV425S2128GB      | 128 GB | 2       | 1079  | 4     | 1.00   |
| Kingston  | SUV500MS480G       | 480 GB | 2       | 365   | 0     | 1.00   |
| Plextor   | PX-64M3            | 64 GB  | 3       | 668   | 346   | 1.00   |
| Crucial   | CT128M550SSD3      | 128 GB | 4       | 469   | 8     | 1.00   |
| Samsung   | MZMPC128HBFU-000H1 | 128 GB | 1       | 363   | 0     | 1.00   |
| Crucial   | CT960M500SSD1      | 960 GB | 10      | 716   | 212   | 1.00   |
| SanDisk   | SSD PLUS 480 GB    | 480 GB | 9       | 406   | 7     | 0.99   |
| Micron    | 5200_MTFDDAK240TDN | 240 GB | 10      | 362   | 0     | 0.99   |
| Apple     | SSD SM0256G        | 256 GB | 6       | 359   | 0     | 0.98   |
| KingShare | 230120SSD          | 128 GB | 1       | 358   | 0     | 0.98   |
| ZTC       | SM201-256G         | 256 GB | 1       | 357   | 0     | 0.98   |
| Intel     | SSDSC2CW480A3      | 480 GB | 4       | 357   | 0     | 0.98   |
| SanDisk   | SDSSDH2128G        | 128 GB | 1       | 356   | 0     | 0.98   |
| ADATA     | SP310              | 128 GB | 2       | 355   | 0     | 0.97   |
| Toshiba   | THNSNJ256GCSU      | 256 GB | 6       | 355   | 0     | 0.97   |
| KingSpec  | KSD-SA25.5-016MJ   | 16 GB  | 1       | 353   | 0     | 0.97   |
| Samsung   | MZNLN128HCGR-000L2 | 128 GB | 3       | 352   | 0     | 0.96   |
| SK hynix  | SC300 SATA         | 256 GB | 1       | 351   | 0     | 0.96   |
| Kingston  | RBU-SC100S37128GD  | 128 GB | 2       | 351   | 0     | 0.96   |
| ADATA     | SX900              | 128 GB | 9       | 759   | 454   | 0.96   |
| Kingston  | SV300S37A60G       | 64 GB  | 120     | 360   | 1     | 0.96   |
| KingDian  | N480-240GB         | 240 GB | 1       | 351   | 0     | 0.96   |
| Samsung   | SSD 840 Series     | 120 GB | 23      | 358   | 1     | 0.96   |
| Samsung   | MZMTE256HMHP-00000 | 256 GB | 1       | 349   | 0     | 0.96   |
| Crucial   | CT128M550SSD4      | 128 GB | 1       | 349   | 0     | 0.96   |
| Intel     | SSDSA2M160G2GC     | 160 GB | 3       | 656   | 4     | 0.96   |
| Samsung   | SSD 850 EVO mSATA  | 120 GB | 4       | 348   | 0     | 0.96   |
| Intel     | SSDMCEAW120A4      | 120 GB | 1       | 347   | 0     | 0.95   |
| Samsung   | MZNTY256HDHP-000H1 | 256 GB | 3       | 392   | 1     | 0.95   |
| Intel     | SSDSC2CT240A3      | 240 GB | 3       | 622   | 1     | 0.95   |
| SanDisk   | Ultra II           | 240 GB | 14      | 386   | 1     | 0.95   |
| Toshiba   | THNSNX024GMNT      | 24 GB  | 2       | 346   | 0     | 0.95   |
| Advantech | SQF-S25M4-32G-S9E  | 32 GB  | 1       | 345   | 0     | 0.95   |
| Intel     | SSDSC2BA400G4      | 400 GB | 3       | 344   | 0     | 0.94   |
| SanDisk   | SD6SF1M128G1022I   | 128 GB | 2       | 446   | 1     | 0.94   |
| Intel     | SSDSA2M040G2GC     | 40 GB  | 5       | 752   | 3     | 0.93   |
| Intel     | SSDSCKJW120H6      | 120 GB | 1       | 339   | 0     | 0.93   |
| SanDisk   | X400 2.5 7MM       | 256 GB | 2       | 339   | 0     | 0.93   |
| Mushkin   | MKNSSDRE1TB        | 1 TB   | 2       | 338   | 0     | 0.93   |
| Samsung   | MZMTE512HMHP-000L1 | 512 GB | 1       | 338   | 0     | 0.93   |
| SanDisk   | SDSSDP256G         | 256 GB | 6       | 352   | 1     | 0.92   |
| Corsair   | Neutron XT SSD     | 480 GB | 3       | 561   | 2     | 0.92   |
| SanDisk   | SDSSDXPS960G       | 960 GB | 4       | 465   | 16    | 0.92   |
| SK hynix  | SC300 M.2 2280     | 512 GB | 1       | 333   | 0     | 0.91   |
| KingFast  | SSD                | 32 GB  | 1       | 332   | 0     | 0.91   |
| Team      | L3 SSD             | 120 GB | 3       | 331   | 0     | 0.91   |
| OCZ       | VERTEX PLUS R2     | 128 GB | 2       | 331   | 0     | 0.91   |
| Crucial   | C300-CTFDDAC128MAG | 128 GB | 3       | 330   | 0     | 0.91   |
| SanDisk   | SD8SBBU120G1122    | 120 GB | 3       | 330   | 0     | 0.90   |
| Samsung   | MZMPC032HBCD-000H1 | 32 GB  | 9       | 329   | 0     | 0.90   |
| ZOTAC     | ZTSSD-S11-240G-P   | 240 GB | 1       | 328   | 0     | 0.90   |
| Mushkin   | MKNSSDCR240GB-7    | 240 GB | 1       | 326   | 0     | 0.89   |
| Team      | TEAML5Lite3D120G   | 120 GB | 4       | 325   | 0     | 0.89   |
| Crucial   | CT250MX200SSD3     | 250 GB | 3       | 325   | 0     | 0.89   |
| OCZ       | VERTEX             | 64 GB  | 2       | 324   | 0     | 0.89   |
| Crucial   | CT120M500SSD1      | 120 GB | 15      | 551   | 163   | 0.89   |
| Micron    | M600_MTFDDAY512MBF | 512 GB | 1       | 323   | 0     | 0.89   |
| Corsair   | Force LE SSD       | 120 GB | 3       | 321   | 0     | 0.88   |
| Crucial   | CT240M500SSD1      | 240 GB | 25      | 540   | 92    | 0.88   |
| OCZ       | VERTEX3 LP         | 64 GB  | 1       | 320   | 0     | 0.88   |
| Goodram   | SSD                | 240 GB | 7       | 319   | 0     | 0.88   |
| Samsung   | SSD 850 EVO mSATA  | 250 GB | 8       | 319   | 0     | 0.88   |
| ADATA     | SP900              | 64 GB  | 17      | 373   | 2     | 0.87   |
| SanDisk   | SDSSDHP064G        | 64 GB  | 8       | 318   | 0     | 0.87   |
| SanDisk   | SSD i110           | 64 GB  | 1       | 317   | 0     | 0.87   |
| SanDisk   | SDSSDHII240G       | 240 GB | 17      | 316   | 0     | 0.87   |
| SanDisk   | SDSSDA960G         | 960 GB | 4       | 316   | 0     | 0.87   |
| Samsung   | MMCRE28G8MXP-0VBL1 | 128 GB | 3       | 315   | 0     | 0.87   |
| Kingston  | SM2280S3G2120G     | 120 GB | 7       | 315   | 0     | 0.86   |
| Intenso   | SATA III SSD       | 120 GB | 8       | 314   | 0     | 0.86   |
| Kingston  | SHSS37A240G        | 240 GB | 21      | 335   | 1     | 0.86   |
| OCZ       | AGILITY4           | 256 GB | 5       | 322   | 49    | 0.86   |
| Toshiba   | TR150              | 120 GB | 4       | 311   | 0     | 0.85   |
| Toshiba   | THNSNX032GMCT      | 32 GB  | 1       | 311   | 0     | 0.85   |
| Micron    | MTFDDAV512TBN-1... | 512 GB | 1       | 620   | 1     | 0.85   |
| Intel     | SSDSC2BW240A4      | 240 GB | 20      | 414   | 2     | 0.85   |
| Crucial   | C300-CTFDDAC064MAG | 64 GB  | 1       | 307   | 0     | 0.84   |
| Kingston  | SVP200S3240G       | 240 GB | 2       | 307   | 0     | 0.84   |
| SanDisk   | SD8SB8U512G1122    | 512 GB | 3       | 305   | 0     | 0.84   |
| Kingston  | SV100S264G         | 64 GB  | 9       | 457   | 5     | 0.83   |
| Toshiba   | THNSNC128GBSJ      | 128 GB | 1       | 303   | 0     | 0.83   |
| Toshiba   | THNSNJ256GVNU      | 256 GB | 1       | 302   | 0     | 0.83   |
| OCZ       | AGILITY2           | 64 GB  | 2       | 302   | 0     | 0.83   |
| SanDisk   | SD8TB8U512G1001    | 512 GB | 2       | 302   | 0     | 0.83   |
| Samsung   | MZ7TD128HAFV-00000 | 128 GB | 1       | 300   | 0     | 0.82   |
| Samsung   | SSD PM810 2.5" 7mm | 128 GB | 1       | 300   | 0     | 0.82   |
| Mushkin   | MKNSSDAT240GB-DX   | 240 GB | 1       | 299   | 0     | 0.82   |
| SanDisk   | SDSSDP128G         | 128 GB | 34      | 348   | 9     | 0.82   |
| Samsung   | MZNLN128HAHQ-00000 | 128 GB | 2       | 299   | 0     | 0.82   |
| ADATA     | SP600              | 32 GB  | 7       | 298   | 0     | 0.82   |
| Samsung   | MZ7LM480HMHQ-000MV | 480 GB | 2       | 298   | 0     | 0.82   |
| SanDisk   | SSD U100           | 128 GB | 6       | 390   | 33    | 0.81   |
| SanDisk   | X300 2.5 7MM       | 256 GB | 1       | 297   | 0     | 0.81   |
| ADATA     | SSD S599           | 64 GB  | 2       | 296   | 0     | 0.81   |
| Kingston  | SV300S37A120G      | 120 GB | 366     | 361   | 17    | 0.81   |
| Intenso   | SSD Sata III       | 250 GB | 1       | 295   | 0     | 0.81   |
| Ramaxel   | RDM-II XM020C024G  | 24 GB  | 2       | 295   | 0     | 0.81   |
| Samsung   | MZ7LF192HCGS-000L1 | 192 GB | 4       | 295   | 0     | 0.81   |
| Plextor   | PX-256M5Pro        | 256 GB | 11      | 294   | 0     | 0.81   |
| SanDisk   | SSD i100           | 16 GB  | 7       | 312   | 1     | 0.81   |
| Netac     | SSD                | 240 GB | 1       | 294   | 0     | 0.81   |
| Kingston  | SNVP325S2256GB     | 256 GB | 1       | 293   | 0     | 0.80   |
| SanDisk   | X400 M.2 2280      | 256 GB | 10      | 292   | 0     | 0.80   |
| PHISON    | 128GB PS3110-S10C  | 128 GB | 1       | 291   | 0     | 0.80   |
| e2e4      | SSD                | 240 GB | 1       | 291   | 0     | 0.80   |
| WDC       | WDS250G1B0A-00H9H0 | 250 GB | 13      | 291   | 0     | 0.80   |
| Samsung   | MZMPA064HMDR-00000 | 64 GB  | 1       | 290   | 0     | 0.79   |
| Crucial   | CT750MX300SSD1     | 752 GB | 9       | 290   | 0     | 0.79   |
| Innodisk  | 2.5" SATA SSD 3ME4 | 128 GB | 2       | 289   | 0     | 0.79   |
| SanDisk   | SDSSDHII120G       | 120 GB | 23      | 288   | 0     | 0.79   |
| Plextor   | PX-256M7VC         | 256 GB | 4       | 288   | 0     | 0.79   |
| ADATA     | SP900              | 256 GB | 11      | 382   | 2     | 0.79   |
| OCZ       | AGILITY3           | 90 GB  | 3       | 476   | 1     | 0.79   |
| Samsung   | SSD 750 EVO        | 120 GB | 36      | 287   | 0     | 0.79   |
| Samsung   | SSD PM830 2.5" 7mm | 512 GB | 2       | 594   | 505   | 0.79   |
| Kingston  | RBU-SNS8152S325... | 256 GB | 2       | 287   | 0     | 0.79   |
| OCZ       | CACHE-SYNAPSE      | 32 GB  | 1       | 286   | 0     | 0.79   |
| Corsair   | Force GS           | 128 GB | 15      | 286   | 0     | 0.78   |
| Intel     | SSDSC2KB480G8      | 480 GB | 1       | 285   | 0     | 0.78   |
| Samsung   | MZMPC128HBFU-00000 | 128 GB | 2       | 284   | 0     | 0.78   |
| Intel     | SSDMCEAC240B3      | 240 GB | 1       | 284   | 0     | 0.78   |
| Apple     | SSD TS128C         | 121 GB | 3       | 283   | 0     | 0.78   |
| Corsair   | CMFSSD-32D1        | 32 GB  | 1       | 566   | 1     | 0.78   |
| Patriot   | Blast              | 240 GB | 6       | 282   | 0     | 0.77   |
| Samsung   | MZNTY256HDHP-000L7 | 256 GB | 8       | 281   | 0     | 0.77   |
| Patriot   | Blaze              | 64 GB  | 5       | 281   | 0     | 0.77   |
| Kingston  | SMS100S232G        | 32 GB  | 1       | 279   | 0     | 0.76   |
| Apacer    | AS330              | 120 GB | 3       | 277   | 0     | 0.76   |
| Samsung   | SSD PM871a M.2 ... | 512 GB | 1       | 277   | 0     | 0.76   |
| PNY       | CS2211 480GB SSD   | 480 GB | 1       | 277   | 0     | 0.76   |
| Toshiba   | THNSNJ128G8NU      | 128 GB | 2       | 274   | 0     | 0.75   |
| Samsung   | MZ7WD960HMHP-00003 | 960 GB | 5       | 610   | 4     | 0.75   |
| ADATA     | SP600NS34          | 256 GB | 1       | 274   | 0     | 0.75   |
| Intel     | SSDSC2CW120A3      | 120 GB | 32      | 497   | 350   | 0.75   |
| MyDigi... | SC2 M2 SSD         | 120 GB | 1       | 271   | 0     | 0.74   |
| Plextor   | PX-128M6G-2242     | 128 GB | 1       | 271   | 0     | 0.74   |
| Kingston  | SMS200S360G        | 64 GB  | 11      | 350   | 2     | 0.74   |
| Samsung   | MZ7LN256HCHP-000L7 | 256 GB | 9       | 270   | 0     | 0.74   |
| Toshiba   | THNSNH060GMCT      | 64 GB  | 1       | 269   | 0     | 0.74   |
| Samsung   | SSD 840 EVO 500... | 500 GB | 3       | 268   | 0     | 0.74   |
| Patriot   | Spark              | 128 GB | 7       | 267   | 0     | 0.73   |
| Samsung   | MZMTD128HAFV-000L1 | 128 GB | 9       | 286   | 16    | 0.73   |
| Samsung   | MZNTD256HAGL-000L9 | 256 GB | 1       | 266   | 0     | 0.73   |
| China     | SATA SSD           | 1 TB   | 1       | 265   | 0     | 0.73   |
| Samsung   | MZNLN512HMJP-000H1 | 512 GB | 1       | 265   | 0     | 0.73   |
| Toshiba   | THNSNJ256G8NY      | 256 GB | 3       | 348   | 1     | 0.73   |
| Intel     | SSDPAMM0008G1      | 8 GB   | 1       | 265   | 0     | 0.73   |
| Crucial   | CT525MX300SSD1     | 528 GB | 45      | 353   | 125   | 0.73   |
| SK hynix  | HFS120G32TND-N1A2A | 120 GB | 1       | 264   | 0     | 0.73   |
| WDC       | WDS250G2B0B-00YS70 | 250 GB | 11      | 264   | 0     | 0.73   |
| WDC       | WDS200T2B0A-00SM50 | 2 TB   | 2       | 264   | 0     | 0.72   |
| Kston     | SSD                | 128 GB | 1       | 264   | 0     | 0.72   |
| Samsung   | MZNLN512HMJP-000L7 | 512 GB | 5       | 264   | 0     | 0.72   |
| Kingston  | SKC400S37128G      | 128 GB | 2       | 264   | 0     | 0.72   |
| Crucial   | CT250MX200SSD1     | 250 GB | 14      | 263   | 0     | 0.72   |
| OCZ       | VERTEX             | 32 GB  | 2       | 616   | 2     | 0.72   |
| Team      | L5 LITE SSD        | 120 GB | 3       | 263   | 0     | 0.72   |
| OCZ       | ARC100             | 120 GB | 11      | 263   | 0     | 0.72   |
| SPCC      | SSD                | 2 TB   | 1       | 263   | 0     | 0.72   |
| Apacer    | A7202              | 64 GB  | 1       | 262   | 0     | 0.72   |
| Samsung   | MZNLF128HCHP-00004 | 128 GB | 7       | 262   | 0     | 0.72   |
| SanDisk   | Ultra II           | 480 GB | 10      | 262   | 0     | 0.72   |
| Transcend | TS512GSSD370       | 512 GB | 2       | 261   | 0     | 0.72   |
| Pioneer   | APS-SL3N-512       | 512 GB | 3       | 261   | 0     | 0.72   |
| SanDisk   | SD8SN8U512G1002    | 512 GB | 8       | 260   | 0     | 0.71   |
| Samsung   | MZ7TE256HMHP-000L2 | 256 GB | 1       | 260   | 0     | 0.71   |
| SanDisk   | SD7SB2Q-512G-1006  | 512 GB | 3       | 260   | 0     | 0.71   |
| China     | SATA SSD           | 20 GB  | 10      | 291   | 1     | 0.71   |
| Micron    | C400-MTFDDAC064MAM | 64 GB  | 2       | 259   | 0     | 0.71   |
| ADATA     | SP900              | 128 GB | 31      | 332   | 12    | 0.71   |
| Apple     | SSD SM128C         | 121 GB | 1       | 518   | 1     | 0.71   |
| OCZ       | ARC100             | 480 GB | 3       | 260   | 1     | 0.71   |
| Goodram   | C50                | 64 GB  | 2       | 258   | 0     | 0.71   |
| SanDisk   | SD5SG2256G1052E    | 256 GB | 5       | 392   | 1     | 0.71   |
| Intel     | SSDSC2BW240H6      | 240 GB | 9       | 303   | 1     | 0.71   |
| ADATA     | IM2S3138E-128GM-B  | 128 GB | 2       | 257   | 0     | 0.70   |
| Samsung   | SSD PM810 TM       | 64 GB  | 1       | 257   | 0     | 0.70   |
| SanDisk   | SD6SB1M128G        | 128 GB | 1       | 256   | 0     | 0.70   |
| Corsair   | Force GS           | 240 GB | 3       | 1272  | 6     | 0.70   |
| Team      | T253X1960G         | 960 GB | 1       | 256   | 0     | 0.70   |
| Crucial   | CT500MX200SSD4     | 500 GB | 2       | 255   | 0     | 0.70   |
| OCZ       | TRION100           | 240 GB | 8       | 296   | 1     | 0.70   |
| PNY       | SSD2SC240G1CS17... | 240 GB | 2       | 254   | 0     | 0.70   |
| Intel     | SSDSC2BW080A4      | 80 GB  | 2       | 254   | 0     | 0.70   |
| Intenso   | SSD                | 128 GB | 11      | 283   | 1     | 0.70   |
| Kingston  | SKC300S37A60G      | 64 GB  | 15      | 349   | 5     | 0.69   |
| Samsung   | MZNLN512HCJH-000H1 | 512 GB | 2       | 253   | 0     | 0.69   |
| Apple     | SSD SD128E         | 121 GB | 3       | 252   | 0     | 0.69   |
| OCZ       | VECTOR150          | 120 GB | 10      | 251   | 0     | 0.69   |
| Crucial   | CT1050MX300SSD4    | 1 TB   | 5       | 271   | 15    | 0.69   |
| Intel     | SSDSC2BW180A4      | 180 GB | 9       | 486   | 3     | 0.69   |
| Samsung   | SSD PM800 TH       | 64 GB  | 1       | 251   | 0     | 0.69   |
| SanDisk   | SD7SB6S256G1122    | 256 GB | 2       | 251   | 0     | 0.69   |
| Kingston  | RBUSC180DS37128GH  | 128 GB | 1       | 250   | 0     | 0.69   |
| Intel     | SSDSCKHF240A4L     | 240 GB | 2       | 306   | 554   | 0.68   |
| Kingston  | SS200S330G         | 32 GB  | 2       | 249   | 0     | 0.68   |
| SanDisk   | X400 M.2 2280      | 128 GB | 4       | 249   | 0     | 0.68   |
| SanDisk   | SDSSDXPS480G       | 480 GB | 6       | 705   | 87    | 0.68   |
| Kingston  | SHPM2280P2H-480G   | 480 GB | 3       | 288   | 1     | 0.68   |
| Samsung   | MZMTD256HAGM-000L1 | 256 GB | 4       | 248   | 0     | 0.68   |
| SanDisk   | SD8SN8U256G1002    | 256 GB | 3       | 248   | 0     | 0.68   |
| Samsung   | MZMPA024HMCD-000L1 | 24 GB  | 3       | 284   | 7     | 0.68   |
| Apacer    | AST680S            | 128 GB | 2       | 248   | 0     | 0.68   |
| SanDisk   | SD8TN8U256G1001    | 256 GB | 3       | 247   | 0     | 0.68   |
| ADATA     | SX930              | 120 GB | 3       | 247   | 0     | 0.68   |
| SanDisk   | Ultra II           | 250 GB | 2       | 247   | 0     | 0.68   |
| SanDisk   | SD8SN8U-512G-1006  | 512 GB | 2       | 297   | 2     | 0.68   |
| Toshiba   | TR150              | 960 GB | 1       | 246   | 0     | 0.68   |
| SanDisk   | SSD U100           | 16 GB  | 7       | 246   | 0     | 0.67   |
| Samsung   | MZ7TE256HMHP-000L7 | 256 GB | 5       | 246   | 0     | 0.67   |
| Samsung   | MZ7TE128HMGR-000H1 | 128 GB | 2       | 245   | 0     | 0.67   |
| Plextor   | PX-128M7VC         | 128 GB | 5       | 245   | 0     | 0.67   |
| Intel     | SSDSA1MH080G1GN    | 80 GB  | 1       | 244   | 0     | 0.67   |
| OCZ       | VECTOR             | 128 GB | 4       | 245   | 4     | 0.67   |
| Kingston  | SA400S37 120G      | 120 GB | 1       | 242   | 0     | 0.66   |
| Plextor   | PX-256M5M          | 256 GB | 2       | 242   | 0     | 0.66   |
| Intel     | SSDSA2BW160G3L     | 160 GB | 5       | 242   | 0     | 0.66   |
| Palit     | PSP120 SSD         | 120 GB | 1       | 242   | 0     | 0.66   |
| WDC       | WDS500G1B0A-00H9H0 | 500 GB | 10      | 241   | 0     | 0.66   |
| Intel     | SSDSC2BF180A4H     | 180 GB | 5       | 414   | 1     | 0.66   |
| WDC       | WDS100T1B0A-00H9H0 | 1 TB   | 9       | 241   | 0     | 0.66   |
| Kingston  | SV300S37A240G      | 240 GB | 89      | 244   | 1     | 0.66   |
| Kingston  | RBUSNS8180S3128GI  | 128 GB | 1       | 241   | 0     | 0.66   |
| Intel     | SSDSA2M080G2HP     | 80 GB  | 2       | 239   | 0     | 0.66   |
| HP        | VK0240GDJXU        | 240 GB | 1       | 238   | 0     | 0.65   |
| Plextor   | PX-512M5P          | 512 GB | 1       | 238   | 0     | 0.65   |
| Crucial   | M4-CT128M4SSD3     | 128 GB | 1       | 238   | 0     | 0.65   |
| SanDisk   | SDSSDH31024G       | 1 TB   | 9       | 237   | 0     | 0.65   |
| Samsung   | MZ7TY256HDHP-00000 | 256 GB | 3       | 237   | 0     | 0.65   |
| ADATA     | SX900              | 256 GB | 6       | 451   | 541   | 0.65   |
| Micron    | MTFDDAK256TBN-1... | 256 GB | 1       | 236   | 0     | 0.65   |
| Toshiba   | TR150              | 240 GB | 14      | 236   | 0     | 0.65   |
| SanDisk   | X300 MSATA         | 256 GB | 2       | 236   | 0     | 0.65   |
| Samsung   | MZ7LN256HAJQ-000H1 | 256 GB | 1       | 235   | 0     | 0.65   |
| Kingston  | SUV400S37240G      | 240 GB | 71      | 256   | 24    | 0.64   |
| Kingston  | SHSS37A120G        | 120 GB | 8       | 234   | 0     | 0.64   |
| Samsung   | MZ7TY256HDHP-000L7 | 256 GB | 4       | 232   | 0     | 0.64   |
| Intel     | SSDSA2M120G2GC     | 120 GB | 2       | 1424  | 6     | 0.64   |
| Patriot   | Blaze              | 240 GB | 2       | 231   | 0     | 0.63   |
| Kingston  | SM2280S3120G       | 120 GB | 3       | 230   | 0     | 0.63   |
| SK hynix  | SH920 2.5 7MM      | 256 GB | 2       | 1001  | 10    | 0.63   |
| Samsung   | MZYLF128HCHP-000L2 | 128 GB | 2       | 230   | 0     | 0.63   |
| SanDisk   | Z400s M.2 2280     | 256 GB | 1       | 229   | 0     | 0.63   |
| SK hynix  | SC210 mSATA        | 128 GB | 3       | 307   | 21    | 0.63   |
| Micron    | MTFDDAK128MAM-1J1  | 128 GB | 4       | 229   | 0     | 0.63   |
| Corsair   | Neutron SSD        | 64 GB  | 3       | 294   | 4     | 0.62   |
| Transcend | TS128GMSA340       | 128 GB | 1       | 227   | 0     | 0.62   |
| SanDisk   | X300 MSATA         | 128 GB | 2       | 227   | 0     | 0.62   |
| Intel     | SSDSC2BW120A4      | 120 GB | 31      | 272   | 1     | 0.62   |
| WDC       | WDS240G1G0A-00SS50 | 240 GB | 16      | 226   | 0     | 0.62   |
| Samsung   | MZNLN512HCJH-000L1 | 512 GB | 2       | 226   | 0     | 0.62   |
| Samsung   | MZMPC032HBCD-000L1 | 32 GB  | 2       | 226   | 0     | 0.62   |
| Corsair   | Performance Pro    | 128 GB | 2       | 227   | 1     | 0.62   |
| Samsung   | MMCRE28G5MXP-MVB   | 128 GB | 1       | 225   | 0     | 0.62   |
| Samsung   | SSD 860 EVO        | 4 TB   | 12      | 225   | 0     | 0.62   |
| Samsung   | MZNTN512HDJH-00007 | 512 GB | 1       | 225   | 0     | 0.62   |
| Patriot   | Flare              | 64 GB  | 4       | 225   | 0     | 0.62   |
| Samsung   | MZMTE128HMGR-000MV | 128 GB | 1       | 225   | 0     | 0.62   |
| Samsung   | MZNTE128HMGR-000L1 | 128 GB | 1       | 224   | 0     | 0.62   |
| OCZ       | OCTANE S2          | 64 GB  | 1       | 224   | 0     | 0.61   |
| Intel     | SSDSC2BB600G4      | 600 GB | 1       | 223   | 0     | 0.61   |
| Kingston  | SKC300S37A120G     | 120 GB | 17      | 225   | 1     | 0.61   |
| Kingston  | SVP200S37A90G      | 90 GB  | 2       | 223   | 0     | 0.61   |
| Team      | L3 EVO SSD         | 120 GB | 4       | 222   | 0     | 0.61   |
| SanDisk   | SSD U110           | 64 GB  | 1       | 222   | 0     | 0.61   |
| Micron    | 1100_MTFDDAK2T0TBN | 2 TB   | 3       | 221   | 0     | 0.61   |
| Samsung   | SSD 860 EVO mSATA  | 1 TB   | 1       | 221   | 0     | 0.61   |
| SanDisk   | SD7SB6S-256G-1006  | 256 GB | 2       | 220   | 0     | 0.60   |
| Corsair   | Force LE SSD       | 480 GB | 1       | 220   | 0     | 0.60   |
| Samsung   | MZNTE128HMGR-000SO | 128 GB | 2       | 379   | 773   | 0.60   |
| China     | SSD                | 64 GB  | 7       | 262   | 1     | 0.60   |
| Samsung   | MMDPE56GFDXP-MVB   | 256 GB | 1       | 218   | 0     | 0.60   |
| SanDisk   | SDSSDRC032G        | 32 GB  | 1       | 217   | 0     | 0.60   |
| Kingston  | RBU-SMSM151S324GD  | 24 GB  | 1       | 217   | 0     | 0.60   |
| Kingston  | SMS200S3120G       | 120 GB | 12      | 245   | 65    | 0.60   |
| Plextor   | PX-128S2G          | 128 GB | 2       | 217   | 0     | 0.60   |
| Samsung   | MMCQE28GFMUP-MVA   | 128 GB | 3       | 243   | 9     | 0.59   |
| ADATA     | XM13               | 32 GB  | 2       | 216   | 0     | 0.59   |
| Kingston  | SNV425S264GB       | 64 GB  | 3       | 917   | 6     | 0.59   |
| Hoodisk   | SSD                | 64 GB  | 1       | 214   | 0     | 0.59   |
| OCZ       | VERTEX             | 96 GB  | 1       | 214   | 0     | 0.59   |
| DOGFISH   | SSD 256G           | 256 GB | 1       | 212   | 0     | 0.58   |
| Micron    | 5210_MTFDDAK7T6QDE | 7.6 TB | 2       | 211   | 0     | 0.58   |
| Kingston  | SUV300S37A240G     | 240 GB | 11      | 210   | 0     | 0.58   |
| Kingston  | SUV400S37120G      | 120 GB | 93      | 232   | 61    | 0.58   |
| SK hynix  | SC311 SATA         | 512 GB | 10      | 231   | 104   | 0.58   |
| Samsung   | MZYTY128HDHP-000L2 | 128 GB | 3       | 210   | 0     | 0.58   |
| Intel     | SSDSC2KB240G8      | 240 GB | 6       | 209   | 0     | 0.57   |
| Team      | T253TD480G         | 480 GB | 1       | 209   | 0     | 0.57   |
| Toshiba   | THNSNJ128GCST      | 128 GB | 3       | 208   | 0     | 0.57   |
| Phison    | SATA SSD           | 240 GB | 7       | 208   | 0     | 0.57   |
| SanDisk   | SD8SN8U128G1002    | 128 GB | 2       | 208   | 0     | 0.57   |
| OCZ       | VERTEX2            | 50 GB  | 2       | 309   | 320   | 0.57   |
| Palit     | PH120 SSD          | 120 GB | 1       | 207   | 0     | 0.57   |
| SanDisk   | iSSD P4            | 8 GB   | 4       | 276   | 1     | 0.57   |
| Smartbuy  | m.2 S10-2280T      | 128 GB | 1       | 206   | 0     | 0.57   |
| Corsair   | CSSD-F60GB2        | 64 GB  | 5       | 799   | 199   | 0.56   |
| Zheino    | CHN-25SATAS3-256   | 256 GB | 1       | 205   | 0     | 0.56   |
| Kingston  | SUV300S37A120G     | 120 GB | 27      | 214   | 1     | 0.56   |
| Kingston  | SHSS37A480G        | 480 GB | 8       | 205   | 0     | 0.56   |
| SanDisk   | SDSSDH3512G        | 512 GB | 9       | 204   | 0     | 0.56   |
| SPCC      | SSD B29            | 32 GB  | 1       | 204   | 0     | 0.56   |
| Micron    | M550_MTFDDAV128MAY | 128 GB | 1       | 204   | 0     | 0.56   |
| SanDisk   | SD6SN1M-256G-1006  | 256 GB | 2       | 203   | 0     | 0.56   |
| Goodram   | SSD                | 120 GB | 25      | 203   | 0     | 0.56   |
| SanDisk   | SD6SF1M128GG56     | 128 GB | 1       | 203   | 0     | 0.56   |
| Samsung   | MZNLN256HMHQ-000H7 | 256 GB | 1       | 203   | 0     | 0.56   |
| Smartbuy  | m.2 S11-2280S      | 128 GB | 1       | 202   | 0     | 0.56   |
| Plextor   | PX-128M7VG         | 128 GB | 2       | 202   | 0     | 0.56   |
| Samsung   | MZRPA128HMCD-000SO | 64 GB  | 10      | 202   | 0     | 0.56   |
| Lite-On   | LCH-128V2S-11 2... | 128 GB | 3       | 202   | 0     | 0.55   |
| Kingston  | SHFS37A240G        | 240 GB | 26      | 246   | 274   | 0.55   |
| Samsung   | MZNTE256HMHP-000L7 | 256 GB | 1       | 201   | 0     | 0.55   |
| Crucial   | CT256M550SSD3      | 256 GB | 1       | 200   | 0     | 0.55   |
| SK hynix  | SC311 SATA         | 128 GB | 15      | 200   | 0     | 0.55   |
| Samsung   | SSD PM871b M.2 ... | 128 GB | 1       | 200   | 0     | 0.55   |
| V-Gen     | SSD                | 240 GB | 1       | 200   | 0     | 0.55   |
| SanDisk   | SD5SF2128G1014E    | 128 GB | 2       | 200   | 0     | 0.55   |
| Kingston  | SKC400S37256G      | 256 GB | 2       | 199   | 0     | 0.55   |
| OCZ       | VERTEX460A         | 120 GB | 6       | 232   | 1     | 0.55   |
| SK hynix  | SC311 SATA         | 256 GB | 24      | 209   | 1     | 0.54   |
| Micron    | MTFDDAV512MBF-1... | 512 GB | 3       | 198   | 0     | 0.54   |
| OCZ       | VERTEX PLUS        | 64 GB  | 1       | 396   | 1     | 0.54   |
| HP        | SSD M700           | 120 GB | 4       | 196   | 0     | 0.54   |
| Crucial   | CT128MX100SSD1     | 128 GB | 5       | 424   | 10    | 0.54   |
| Samsung   | MZNTD256HAGL-00000 | 256 GB | 1       | 196   | 0     | 0.54   |
| Smartbuy  | SSD                | 64 GB  | 22      | 195   | 0     | 0.54   |
| Plextor   | PX-128S3G          | 128 GB | 1       | 194   | 0     | 0.53   |
| Kingston  | RBU-SC100S37240GE  | 240 GB | 1       | 194   | 0     | 0.53   |
| Smartbuy  | SSD                | 120 GB | 65      | 204   | 1     | 0.53   |
| Samsung   | SSD 850 EVO M.2    | 250 GB | 16      | 193   | 0     | 0.53   |
| Micron    | MTFDBAK128MAG-1G1  | 128 GB | 2       | 192   | 0     | 0.53   |
| KingFast  | SSD                | 256 GB | 6       | 192   | 0     | 0.53   |
| OCZ       | VERTEX4            | 512 GB | 1       | 573   | 2     | 0.52   |
| Crucial   | CT120BX300SSD1     | 120 GB | 6       | 191   | 0     | 0.52   |
| Kingston  | RBU-SNS8152S312... | 128 GB | 2       | 190   | 0     | 0.52   |
| OCZ       | TRION150           | 240 GB | 4       | 190   | 0     | 0.52   |
| Kingston  | SS100S216G         | 16 GB  | 1       | 190   | 0     | 0.52   |
| KingFast  | SSD                | 128 GB | 11      | 190   | 0     | 0.52   |
| SPCC      | SSD                | 64 GB  | 74      | 202   | 42    | 0.52   |
| Golden... | SSD 128            | 128 GB | 1       | 190   | 0     | 0.52   |
| SanDisk   | SDSSDH32000G       | 2 TB   | 2       | 189   | 0     | 0.52   |
| SK hynix  | HFS256G39TNH-73A0A | 256 GB | 2       | 190   | 891   | 0.52   |
| Intel     | SSDSC2BW360H6      | 360 GB | 1       | 566   | 2     | 0.52   |
| Seagate   | SSD                | 1 TB   | 2       | 188   | 0     | 0.52   |
| Samsung   | MZMTD512HAGL-000L1 | 512 GB | 3       | 223   | 33    | 0.51   |
| Transcend | TS128GSSD720       | 128 GB | 2       | 187   | 0     | 0.51   |
| SanDisk   | SSD i100           | 24 GB  | 19      | 197   | 2     | 0.51   |
| WDC       | WDS250G2B0A-00SM50 | 250 GB | 21      | 186   | 0     | 0.51   |
| ADATA     | SX900              | 64 GB  | 4       | 515   | 518   | 0.51   |
| SPCC      | SSD162             | 120 GB | 7       | 406   | 436   | 0.51   |
| Smartbuy  | mSata              | 64 GB  | 1       | 186   | 0     | 0.51   |
| Crucial   | M4-CT256M4SSD3     | 256 GB | 1       | 185   | 0     | 0.51   |
| SanDisk   | SD6SB1M-128G-1006  | 128 GB | 3       | 185   | 0     | 0.51   |
| SanDisk   | SD5SE2256G1002E    | 256 GB | 4       | 183   | 0     | 0.50   |
| SK hynix  | HFS256G32TND-N210A | 256 GB | 3       | 183   | 0     | 0.50   |
| BHT       | WR202HH032G E70... | 32 GB  | 2       | 183   | 0     | 0.50   |
| Kingston  | SV200S3256G        | 256 GB | 4       | 528   | 2     | 0.50   |
| Apacer    | AS350              | 256 GB | 1       | 183   | 0     | 0.50   |
| Samsung   | SSD 860 EVO M.2    | 2 TB   | 1       | 183   | 0     | 0.50   |
| Team      | TEAML5Lite3D1T     | 1 TB   | 2       | 182   | 0     | 0.50   |
| Crucial   | CT480M500SSD1      | 480 GB | 5       | 1006  | 416   | 0.50   |
| Samsung   | MZMTE256HMHP-000MV | 256 GB | 1       | 181   | 0     | 0.50   |
| Patriot   | Blaze              | 120 GB | 5       | 181   | 0     | 0.50   |
| Transcend | TS128GMSA740       | 128 GB | 1       | 180   | 0     | 0.50   |
| Intel     | SSDSC2BW180A3H     | 180 GB | 3       | 180   | 0     | 0.49   |
| Samsung   | SSD 860 EVO        | 1 TB   | 152     | 180   | 0     | 0.49   |
| ADATA     | SP550              | 480 GB | 2       | 179   | 0     | 0.49   |
| KingDian  | S400 XT            | 240 GB | 1       | 177   | 0     | 0.49   |
| SPCC      | SSD A20            | 64 GB  | 2       | 177   | 0     | 0.49   |
| Samsung   | SSD 860 EVO M.2    | 250 GB | 18      | 176   | 0     | 0.48   |
| PNY       | CS900 480GB SSD    | 480 GB | 4       | 175   | 0     | 0.48   |
| BIOSTAR   | S100-240GB PLUS    | 240 GB | 1       | 175   | 0     | 0.48   |
| SanDisk   | SD7TB3Q-128G-1006  | 128 GB | 2       | 220   | 15    | 0.48   |
| Micron    | MTFDDAK256MAM-1K12 | 256 GB | 10      | 196   | 505   | 0.48   |
| Intel     | SSDSC2BW120H6      | 120 GB | 13      | 207   | 6     | 0.48   |
| SanDisk   | SD7TB6S256G1001    | 256 GB | 3       | 174   | 0     | 0.48   |
| Micron    | MTFDDAK512MBF-1... | 512 GB | 1       | 173   | 0     | 0.48   |
| Intel     | SSDSCMMW240A3L     | 240 GB | 2       | 263   | 1     | 0.48   |
| SK hynix  | SC308 SATA         | 256 GB | 5       | 173   | 0     | 0.48   |
| Faspeed   | F510-120G          | 120 GB | 1       | 173   | 0     | 0.47   |
| Kingston  | SHFS37A120G        | 120 GB | 84      | 245   | 316   | 0.47   |
| Micron    | 1100_MTFDDAK256TBN | 256 GB | 9       | 178   | 125   | 0.47   |
| SK hynix  | HFS256G39MND-3310A | 256 GB | 1       | 172   | 0     | 0.47   |
| Kingston  | SV100S2128G        | 128 GB | 3       | 286   | 2     | 0.47   |
| WDC       | WDS500G2B0A-00SM50 | 500 GB | 48      | 172   | 0     | 0.47   |
| Goodram   | CX100              | 120 GB | 7       | 226   | 2     | 0.47   |
| SanDisk   | SDSSDH31000G       | 1 TB   | 6       | 171   | 0     | 0.47   |
| SanDisk   | SDSSDA240G         | 240 GB | 86      | 176   | 3     | 0.47   |
| Kingston  | RBU-SNS8152S351... | 512 GB | 1       | 171   | 0     | 0.47   |
| Intel     | SSDSC2CT180A4      | 180 GB | 6       | 170   | 0     | 0.47   |
| Toshiba   | THNSNH128GMCT      | 128 GB | 3       | 170   | 0     | 0.47   |
| Team      | T253X2512G         | 512 GB | 2       | 170   | 0     | 0.47   |
| SanDisk   | SD8SN8U128G1001    | 128 GB | 1       | 170   | 0     | 0.47   |
| WDC       | WDBNCE5000PNC      | 500 GB | 4       | 170   | 0     | 0.47   |
| SanDisk   | SD9TN8W512G1001    | 512 GB | 1       | 169   | 0     | 0.47   |
| Mushkin   | MKNSSDEC60GB       | 64 GB  | 1       | 169   | 0     | 0.46   |
| Toshiba   | A100               | 120 GB | 4       | 168   | 0     | 0.46   |
| Toshiba   | TL100              | 240 GB | 3       | 167   | 0     | 0.46   |
| Intenso   | SSD Sata III       | 240 GB | 3       | 166   | 0     | 0.46   |
| Plextor   | PX-AG256M6e        | 256 GB | 2       | 165   | 0     | 0.45   |
| Crucial   | CT525MX300SSD4     | 528 GB | 9       | 215   | 1     | 0.45   |
| Plextor   | PH6-CE120-G        | 120 GB | 2       | 164   | 0     | 0.45   |
| Samsung   | SSD 830 Series     | 56 GB  | 1       | 164   | 0     | 0.45   |
| Intel     | SSDSC2CW060A3      | 64 GB  | 10      | 265   | 407   | 0.45   |
| GLOWAY    | STK720GS3-S7       | 720 GB | 1       | 163   | 0     | 0.45   |
| OCZ       | VERTEX460          | 120 GB | 4       | 294   | 5     | 0.45   |
| V-GeN     | V-GEN02SM19EG51... | 512 GB | 1       | 162   | 0     | 0.45   |
| Vaseky    | V900-128G          | 128 GB | 1       | 162   | 0     | 0.45   |
| Samsung   | MZ7LN512HCHP-000L1 | 512 GB | 4       | 162   | 0     | 0.45   |
| Apacer    | 256GB SATA Flas... | 256 GB | 1       | 162   | 0     | 0.44   |
| Samsung   | SSD PM871b M.2 ... | 512 GB | 2       | 161   | 0     | 0.44   |
| Crucial   | M4-CT512M4SSD1     | 512 GB | 1       | 161   | 0     | 0.44   |
| Samsung   | SSD EVO 360G       | 360 GB | 1       | 161   | 0     | 0.44   |
| Intel     | SSDSA2CW160G3      | 160 GB | 3       | 161   | 0     | 0.44   |
| Corsair   | Force LS SSD       | 240 GB | 3       | 343   | 505   | 0.44   |
| Samsung   | MZNTY128HDHP-000H1 | 128 GB | 6       | 160   | 0     | 0.44   |
| Plextor   | PX-256M5S          | 256 GB | 12      | 160   | 0     | 0.44   |
| Micron    | MTFDDAK256MAM-1K1  | 256 GB | 1       | 159   | 0     | 0.44   |
| Samsung   | MZ7TY128HDHP-000L1 | 128 GB | 4       | 159   | 0     | 0.44   |
| SanDisk   | SD9SN8W512G1102    | 512 GB | 2       | 158   | 0     | 0.43   |
| Zheino    | CHN mSATAM3 128    | 128 GB | 2       | 158   | 0     | 0.43   |
| Toshiba   | A100               | 240 GB | 5       | 158   | 0     | 0.43   |
| ADATA     | AXNS381E-128GM-B2  | 128 GB | 1       | 158   | 0     | 0.43   |
| Ramsta    | SSD S600           | 480 GB | 1       | 158   | 0     | 0.43   |
| Apple     | SSD SM0128G        | 121 GB | 8       | 157   | 0     | 0.43   |
| Samsung   | MZNTY256HDHP-000L2 | 256 GB | 2       | 157   | 0     | 0.43   |
| Patriot   | Blast              | 120 GB | 6       | 157   | 0     | 0.43   |
| Intel     | SSDSC2BF180A4L     | 180 GB | 1       | 157   | 0     | 0.43   |
| GeIL      | ZENITH R3_240GB    | 240 GB | 1       | 157   | 0     | 0.43   |
| Phison    | SATA SSD           | 128 GB | 1       | 156   | 0     | 0.43   |
| Phison    | SATA SSD           | 120 GB | 19      | 155   | 0     | 0.43   |
| SPCC      | SSD                | 120 GB | 117     | 195   | 115   | 0.43   |
| Samsung   | MMCRE64GFMPP-MVA   | 64 GB  | 2       | 155   | 0     | 0.43   |
| Lite-On   | CV3-CE128-HP       | 128 GB | 1       | 154   | 0     | 0.42   |
| Smartbuy  | SSD                | 240 GB | 18      | 192   | 1     | 0.42   |
| Plextor   | PX-256S2C          | 256 GB | 2       | 153   | 0     | 0.42   |
| Intel     | SSDSC2BW180H6      | 180 GB | 1       | 153   | 0     | 0.42   |
| Transcend | TS256GSSD230S      | 256 GB | 4       | 152   | 0     | 0.42   |
| Samsung   | MZNLF128HCHP-000L1 | 128 GB | 1       | 151   | 0     | 0.42   |
| Samsung   | MZNLN512HAJQ-000H1 | 512 GB | 2       | 151   | 0     | 0.41   |
| Crucial   | FCCT512MX100SSD1   | 512 GB | 1       | 151   | 0     | 0.41   |
| Transcend | TS120GMTS820S      | 120 GB | 2       | 150   | 0     | 0.41   |
| Corsair   | CSSD-F180GB2       | 180 GB | 1       | 149   | 0     | 0.41   |
| Plextor   | PH6-CE120          | 120 GB | 6       | 149   | 0     | 0.41   |
| Apple     | SSD SD0128F        | 121 GB | 4       | 149   | 0     | 0.41   |
| SanDisk   | X600 M.2 2280 SATA | 128 GB | 4       | 148   | 0     | 0.41   |
| Samsung   | SSD 860 EVO        | 250 GB | 128     | 148   | 0     | 0.41   |
| Intel     | SSDMCEAC180B3      | 180 GB | 2       | 148   | 0     | 0.41   |
| Corsair   | Neutron GTX SSD    | 240 GB | 4       | 180   | 74    | 0.41   |
| Intel     | SSDSC2BB300G4      | 304 GB | 2       | 147   | 0     | 0.41   |
| Kingston  | HyperX Fury 3D     | 480 GB | 1       | 147   | 0     | 0.41   |
| Goodram   | SSDPR-CX400-01T    | 1 TB   | 1       | 147   | 0     | 0.40   |
| Samsung   | SSD 860 EVO        | 500 GB | 236     | 147   | 0     | 0.40   |
| Intel     | SSDSCKGF256A5 SATA | 256 GB | 2       | 147   | 0     | 0.40   |
| Intel     | SSDSC2KG240G7      | 240 GB | 1       | 146   | 0     | 0.40   |
| KingFast  | SSD                | 64 GB  | 3       | 146   | 1     | 0.40   |
| KingSpec  | ACJC2M032mSH       | 32 GB  | 2       | 145   | 0     | 0.40   |
| Netac     | SSD                | 720 GB | 4       | 145   | 0     | 0.40   |
| WDC       | WDS100T2B0A-00SM50 | 1 TB   | 32      | 144   | 0     | 0.40   |
| Intel     | SSDSC2BB120G4      | 120 GB | 1       | 143   | 0     | 0.39   |
| SanDisk   | X400 M.2 2280      | 512 GB | 1       | 143   | 0     | 0.39   |
| QUMO      | SSD                | 64 GB  | 1       | 143   | 0     | 0.39   |
| Samsung   | MZNTY128HDHP-000L1 | 128 GB | 2       | 142   | 0     | 0.39   |
| China     | 120GB SSD          | 120 GB | 45      | 142   | 0     | 0.39   |
| Toshiba   | THNSNW032GMCP      | 32 GB  | 1       | 142   | 0     | 0.39   |
| Intel     | SSDSC2KW512G8      | 512 GB | 11      | 142   | 1     | 0.39   |
| SanDisk   | X600 M.2 2280 SATA | 512 GB | 1       | 141   | 0     | 0.39   |
| KingSpec  | KSD-SA25.5-064MJ   | 64 GB  | 1       | 141   | 0     | 0.39   |
| WDC       | WDS100T2B0B-00YS70 | 1 TB   | 12      | 141   | 0     | 0.39   |
| Intel     | SSDSC2BF180A5L     | 180 GB | 1       | 141   | 0     | 0.39   |
| Innodisk  | mSATA mini 3ME ... | 32 GB  | 1       | 140   | 0     | 0.39   |
| WDC       | WDS120G1G0A-00SS50 | 120 GB | 26      | 140   | 0     | 0.38   |
| SanDisk   | SD9SN8W256G1002    | 256 GB | 4       | 140   | 0     | 0.38   |
| SanDisk   | SSD PLUS 240 GB    | 240 GB | 13      | 140   | 0     | 0.38   |
| UNIC2     | S100-480           | 480 GB | 1       | 139   | 0     | 0.38   |
| MENGMI    | SSD                | 240 GB | 1       | 139   | 0     | 0.38   |
| Toshiba   | THNSNH512GDNT      | 512 GB | 1       | 138   | 0     | 0.38   |
| Transcend | TS256GSSD360S      | 256 GB | 2       | 138   | 0     | 0.38   |
| Lite-On   | IT LMT-256L9M      | 256 GB | 2       | 137   | 0     | 0.38   |
| Samsung   | MZ7LH480HAHQ0D3    | 480 GB | 2       | 137   | 0     | 0.38   |
| OCZ       | ARC100             | 240 GB | 6       | 203   | 1     | 0.37   |
| Toshiba   | THNSNH256GBST      | 256 GB | 2       | 136   | 0     | 0.37   |
| WDC       | WDS500G1R0B-68A4Z0 | 500 GB | 1       | 135   | 0     | 0.37   |
| Intel     | SSDSC2BB080G4      | 80 GB  | 1       | 135   | 0     | 0.37   |
| SK hynix  | HFS128G32MND-3210A | 128 GB | 1       | 135   | 0     | 0.37   |
| Samsung   | SSD 850 EVO M.2    | 1 TB   | 3       | 135   | 0     | 0.37   |
| KingDian  | P10                | 120 GB | 1       | 134   | 0     | 0.37   |
| Plextor   | PX-128M5S          | 128 GB | 45      | 135   | 1     | 0.37   |
| Toshiba   | VX500              | 256 GB | 1       | 134   | 0     | 0.37   |
| Zheino    | CHN mSATA02M 256   | 256 GB | 2       | 219   | 1     | 0.37   |
| Team      | TEAML5Lite3D480G   | 480 GB | 2       | 133   | 0     | 0.36   |
| MyDigi... | SB2                | 240 GB | 2       | 132   | 0     | 0.36   |
| Transcend | TS256GMTS400       | 256 GB | 3       | 132   | 0     | 0.36   |
| Patriot   | Burst              | 960 GB | 2       | 131   | 0     | 0.36   |
| Goodram   | SSDPR-CX300-120    | 120 GB | 4       | 131   | 0     | 0.36   |
| OCZ       | VERTEX450          | 128 GB | 4       | 310   | 520   | 0.36   |
| SanDisk   | SD9SN8W512G1002    | 512 GB | 1       | 130   | 0     | 0.36   |
| Micron    | 1100 SATA          | 512 GB | 6       | 170   | 243   | 0.36   |
| SanDisk   | SD8SN8U-256G-1006  | 256 GB | 19      | 190   | 216   | 0.36   |
| Samsung   | SSD 860 EVO mSATA  | 250 GB | 10      | 130   | 0     | 0.36   |
| HPE       | MK0800GEYKE        | 800 GB | 1       | 130   | 0     | 0.36   |
| SK hynix  | HFS256G39TND-N210A | 256 GB | 17      | 154   | 1     | 0.36   |
| WDC       | WDS120G1G0B-00RC30 | 120 GB | 6       | 129   | 0     | 0.36   |
| WDC       | WDS250G2B0A        | 250 GB | 4       | 129   | 0     | 0.35   |
| Toshiba   | THNSNF064GMCS      | 64 GB  | 2       | 129   | 0     | 0.35   |
| Corsair   | Force LS SSD       | 64 GB  | 21      | 272   | 149   | 0.35   |
| Samsung   | SSD 860 EVO M.2    | 500 GB | 27      | 128   | 0     | 0.35   |
| KLEVV     | SSD NEO N500       | 240 GB | 1       | 127   | 0     | 0.35   |
| Vaseky    | V800-120G          | 120 GB | 1       | 127   | 0     | 0.35   |
| Goodram   | IRIDIUM            | 480 GB | 2       | 127   | 0     | 0.35   |
| GALAX     | TA1D0120A          | 120 GB | 2       | 126   | 0     | 0.35   |
| Samsung   | MZMTE256HMHP-000L1 | 256 GB | 2       | 126   | 0     | 0.35   |
| Chiprex   | S10T3120GB         | 120 GB | 1       | 126   | 0     | 0.35   |
| SanDisk   | SDSSDH3250G        | 250 GB | 12      | 126   | 0     | 0.35   |
| Crucial   | CT2000MX500SSD1    | 2 TB   | 27      | 126   | 0     | 0.35   |
| Intel     | SSDSC2BW480A4      | 480 GB | 4       | 485   | 13    | 0.35   |
| BLUERAY   | SSD                | 120 GB | 1       | 125   | 0     | 0.34   |
| SanDisk   | SD5SB2-128G-1006E  | 128 GB | 1       | 125   | 0     | 0.34   |
| Samsung   | MZNLN512HAJQ-00000 | 512 GB | 4       | 125   | 0     | 0.34   |
| KingFast  | SSD                | 32 GB  | 1       | 125   | 0     | 0.34   |
| SanDisk   | SD9TB8W256G1001    | 256 GB | 3       | 125   | 0     | 0.34   |
| BRAVEE... | SSD                | 240 GB | 1       | 125   | 0     | 0.34   |
| Corsair   | Force LS SSD       | 120 GB | 11      | 266   | 460   | 0.34   |
| Lite-On   | CV5-8Q128          | 128 GB | 1       | 125   | 0     | 0.34   |
| SanDisk   | SSD U110           | 16 GB  | 17      | 124   | 0     | 0.34   |
| Samsung   | MZMTD128HAFV-000   | 128 GB | 4       | 124   | 0     | 0.34   |
| KingDian  | S400               | 480 GB | 2       | 124   | 0     | 0.34   |
| SanDisk   | SSD PLUS           | 480 GB | 33      | 145   | 1     | 0.34   |
| Samsung   | MZNLN256HMHQ-000H1 | 256 GB | 9       | 123   | 0     | 0.34   |
| China     | SH00R480GB         | 480 GB | 3       | 123   | 0     | 0.34   |
| Kingston  | SUV500120G         | 120 GB | 14      | 123   | 0     | 0.34   |
| Apple     | SSD SM512E         | 500 GB | 1       | 123   | 0     | 0.34   |
| SanDisk   | SDSSDA120G         | 120 GB | 60      | 132   | 19    | 0.34   |
| Hypertec  | SSD2S240SF1200SA2  | 240 GB | 2       | 371   | 512   | 0.33   |
| ADATA     | SSD S511           | 64 GB  | 3       | 450   | 679   | 0.33   |
| Samsung   | MZNTD128HAGM-00000 | 128 GB | 3       | 120   | 0     | 0.33   |
| SanDisk   | SD9SN8W256G1102    | 256 GB | 7       | 120   | 0     | 0.33   |
| Kingston  | SUV500M8240G       | 240 GB | 1       | 120   | 0     | 0.33   |
| Kingston  | RBU-SNS8152S312... | 128 GB | 1       | 120   | 0     | 0.33   |
| Fujitsu   | F500s 480G         | 480 GB | 1       | 119   | 0     | 0.33   |
| SPCC      | M.2 Disk           | 256 GB | 1       | 119   | 0     | 0.33   |
| WDC       | WDS500G2B0B-00YS70 | 500 GB | 18      | 119   | 0     | 0.33   |
| Plextor   | PX-AG128M6e        | 128 GB | 4       | 229   | 2     | 0.33   |
| KingDian  | S280-120GB         | 120 GB | 6       | 134   | 321   | 0.33   |
| SPCC      | SSD                | 256 GB | 24      | 125   | 5     | 0.33   |
| SK hynix  | HFS128G3BTND-N210A | 128 GB | 3       | 118   | 0     | 0.32   |
| OCZ       | TRION100           | 120 GB | 5       | 139   | 2     | 0.32   |
| Crucial   | CT1024MX200SSD1    | 1 TB   | 1       | 116   | 0     | 0.32   |
| Kingston  | SUV500M8480G       | 480 GB | 2       | 116   | 0     | 0.32   |
| ADATA     | SSD SX900 512GB... | 512 GB | 2       | 116   | 0     | 0.32   |
| Kingston  | SVP200S3120G       | 120 GB | 4       | 370   | 499   | 0.32   |
| Samsung   | SG9XCS2D400GESLT   | 400 GB | 1       | 115   | 0     | 0.32   |
| Corsair   | Force LE200 SSD    | 240 GB | 2       | 115   | 0     | 0.32   |
| Samsung   | MZMPC128HBFU-000   | 128 GB | 1       | 114   | 0     | 0.31   |
| Goodram   | SSDPR-CL100-240    | 240 GB | 3       | 114   | 0     | 0.31   |
| SanDisk   | SD7SN3Q256G1002    | 256 GB | 2       | 192   | 515   | 0.31   |
| OCZ       | D2CSTK181M11-0180  | 180 GB | 3       | 114   | 0     | 0.31   |
| SanDisk   | SD9SN8W256G        | 256 GB | 2       | 113   | 0     | 0.31   |
| Corsair   | FORCE LX SSD       | 256 GB | 1       | 113   | 0     | 0.31   |
| ADATA     | SP550              | 240 GB | 18      | 113   | 1     | 0.31   |
| Toshiba   | TR150              | 480 GB | 4       | 265   | 2     | 0.31   |
| Intel     | SSDSA2M080G2LE     | 80 GB  | 2       | 154   | 6     | 0.31   |
| OCZ       | VERTEX2            | 90 GB  | 1       | 113   | 0     | 0.31   |
| Micron    | MTFDDAK512MAM-1K1  | 512 GB | 1       | 113   | 0     | 0.31   |
| Toshiba   | Q300               | 120 GB | 2       | 112   | 0     | 0.31   |
| Kingston  | RBUSNS8280S3128GH2 | 128 GB | 2       | 112   | 0     | 0.31   |
| SanDisk   | SD9SN8W128G1102    | 128 GB | 2       | 112   | 0     | 0.31   |
| Toshiba   | THNSNK256GVN8      | 256 GB | 1       | 111   | 0     | 0.31   |
| SPCC      | SSD                | 1 TB   | 7       | 111   | 0     | 0.31   |
| Seagate   | SSD                | 500 GB | 1       | 111   | 0     | 0.31   |
| Phison    | SATA SSD           | 480 GB | 2       | 111   | 0     | 0.30   |
| Crucial   | CT500BX100SSD1     | 500 GB | 5       | 111   | 0     | 0.30   |
| Kingston  | SUV400S37480G      | 480 GB | 4       | 141   | 1     | 0.30   |
| Samsung   | SSD 860 QVO        | 2 TB   | 18      | 111   | 0     | 0.30   |
| SanDisk   | SD6SB1M128G1002    | 128 GB | 1       | 110   | 0     | 0.30   |
| SanDisk   | SD9TN8W256G1001    | 256 GB | 2       | 110   | 0     | 0.30   |
| ADATA     | SU700              | 120 GB | 7       | 112   | 2     | 0.30   |
| Intenso   | SSD                | 256 GB | 5       | 109   | 0     | 0.30   |
| Samsung   | MZNLF128HCHP-000H1 | 128 GB | 1       | 109   | 0     | 0.30   |
| Apacer    | AS340              | 120 GB | 5       | 109   | 0     | 0.30   |
| Faspeed   | H7-240G            | 240 GB | 1       | 109   | 0     | 0.30   |
| PNY       | CS900 240GB SSD    | 240 GB | 20      | 108   | 0     | 0.30   |
| ADATA     | SU800              | 256 GB | 18      | 153   | 2     | 0.30   |
| Intel     | SSDSC2KF128G8L     | 128 GB | 3       | 108   | 0     | 0.30   |
| GeIL      | R3_128GB           | 128 GB | 1       | 107   | 0     | 0.30   |
| Transcend | TS256GSSD370       | 256 GB | 1       | 107   | 0     | 0.30   |
| Kingston  | MS80000058688      | 256 GB | 1       | 107   | 0     | 0.29   |
| Kingston  | RBUSNS8180S3128GJ  | 128 GB | 3       | 107   | 0     | 0.29   |
| WDC       | WDS120G2G0B-00EPW0 | 120 GB | 24      | 109   | 1     | 0.29   |
| Transcend | TS480GSSD220S      | 480 GB | 4       | 107   | 0     | 0.29   |
| Phison    | SATA SSD           | 1 TB   | 4       | 107   | 0     | 0.29   |
| Crucial   | CT480BX500SSD1     | 480 GB | 32      | 122   | 1     | 0.29   |
| Lite-On   | CV3-8D256          | 256 GB | 2       | 106   | 0     | 0.29   |
| Kingston  | SA400S37240G       | 240 GB | 290     | 112   | 2     | 0.29   |
| Crucial   | CT256M550SSD1      | 256 GB | 6       | 362   | 8     | 0.29   |
| Intenso   | SSD Sata III       | 120 GB | 2       | 106   | 0     | 0.29   |
| PNY       | SSD2SC240G5LC72... | 240 GB | 1       | 106   | 0     | 0.29   |
| Mushkin   | MKNSSDAT60GB-V     | 64 GB  | 1       | 106   | 0     | 0.29   |
| Samsung   | MZYTE128HMGR-000L2 | 128 GB | 1       | 106   | 0     | 0.29   |
| KingDian  | S400               | 120 GB | 11      | 106   | 0     | 0.29   |
| Plextor   | PH6-CE240-L1       | 240 GB | 1       | 106   | 0     | 0.29   |
| Lite-On   | IT L8T-128L9G      | 128 GB | 1       | 105   | 0     | 0.29   |
| Toshiba   | THNSNC256GBSJ      | 256 GB | 1       | 105   | 0     | 0.29   |
| SanDisk   | SSD PLUS 120 GB    | 120 GB | 18      | 109   | 1     | 0.29   |
| WDC       | WDBNCE2500PNC      | 250 GB | 5       | 105   | 0     | 0.29   |
| Plextor   | PX-128M5M          | 128 GB | 8       | 104   | 0     | 0.29   |
| Kingston  | SHFS37A480G        | 480 GB | 1       | 104   | 0     | 0.29   |
| Transcend | TS240GSSD220S      | 240 GB | 10      | 104   | 0     | 0.29   |
| SPCC      | SSDB28             | 128 GB | 1       | 104   | 0     | 0.29   |
| Seagate   | XA480ME10063       | 480 GB | 4       | 104   | 0     | 0.29   |
| Crucial   | CT1000MX500SSD1    | 1 TB   | 81      | 104   | 0     | 0.29   |
| SanDisk   | SD8SB8U-128G-1006  | 128 GB | 1       | 104   | 0     | 0.29   |
| Intel     | SSDSA2BW160G3H     | 160 GB | 6       | 129   | 2     | 0.29   |
| Transcend | TS64GSSD340        | 64 GB  | 3       | 180   | 336   | 0.28   |
| ADATA     | SP600              | 64 GB  | 7       | 113   | 2     | 0.28   |
| China     | SATA SSD           | 240 GB | 13      | 103   | 0     | 0.28   |
| WDC       | WDS240G1G0B-00RC30 | 240 GB | 6       | 103   | 0     | 0.28   |
| Intel     | SSDSC2BF240A5L     | 240 GB | 4       | 103   | 0     | 0.28   |
| Intel     | SSDSA2M160G2GN     | 160 GB | 1       | 2996  | 28    | 0.28   |
| SK hynix  | SC210 2.5 7MM      | 128 GB | 2       | 478   | 2     | 0.28   |
| Fujitsu   | F300               | 480 GB | 1       | 103   | 0     | 0.28   |
| Transcend | TS120GSSD25D-M     | 128 GB | 1       | 309   | 2     | 0.28   |
| Apacer    | AS510S             | 64 GB  | 5       | 103   | 0     | 0.28   |
| ADATA     | SU900              | 512 GB | 2       | 102   | 0     | 0.28   |
| Intel     | SSDSA2BW120G3H     | 120 GB | 1       | 102   | 0     | 0.28   |
| SanDisk   | SDSA6MM-032G-1006  | 32 GB  | 1       | 102   | 0     | 0.28   |
| Samsung   | SSD 860 EVO M.2    | 1 TB   | 12      | 102   | 0     | 0.28   |
| SPCC      | SSD                | 128 GB | 22      | 103   | 1     | 0.28   |
| KingFast  | SSD                | 32 GB  | 1       | 102   | 0     | 0.28   |
| Kingston  | SA400S37120G       | 120 GB | 316     | 110   | 1     | 0.28   |
| Phison    | SSM28512GPTCB3B... | 512 GB | 1       | 101   | 0     | 0.28   |
| Micron    | MTFDDAK256TBN      | 256 GB | 1       | 101   | 0     | 0.28   |
| SanDisk   | SD9SB8W512G1101    | 512 GB | 3       | 100   | 0     | 0.27   |
| ORICO     | N300               | 128 GB | 1       | 99    | 0     | 0.27   |
| Hikvision | HKVSN HS-SSD-C1... | 240 GB | 1       | 99    | 0     | 0.27   |
| Kingston  | SA400S37480G       | 480 GB | 114     | 111   | 3     | 0.27   |
| Toshiba   | TR200              | 480 GB | 7       | 99    | 0     | 0.27   |
| OWC       | Mercury Electra... | 2 TB   | 2       | 99    | 0     | 0.27   |
| TCSUNBOW  | X3                 | 64 GB  | 1       | 99    | 0     | 0.27   |
| Kingston  | SUV500240G         | 240 GB | 17      | 108   | 68    | 0.27   |
| Samsung   | MZ7LN256HAJQ-000L7 | 256 GB | 1       | 98    | 0     | 0.27   |
| Micron    | 5100_MTFDDAK240TCB | 240 GB | 1       | 98    | 0     | 0.27   |
| Goodram   | SSDPR-CX400-128    | 128 GB | 9       | 98    | 0     | 0.27   |
| Toshiba   | THNSNH256G8NT      | 256 GB | 1       | 293   | 2     | 0.27   |
| ADATA     | SP920SS            | 128 GB | 5       | 409   | 7     | 0.27   |
| Intenso   | SSD                | 120 GB | 1       | 97    | 0     | 0.27   |
| Anobit    | Gen2A400 118032738 | 400 GB | 1       | 96    | 0     | 0.27   |
| SanDisk   | SD7SB3Q128G1002    | 128 GB | 1       | 387   | 3     | 0.27   |
| SanDisk   | SDSSDH3 250G       | 250 GB | 3       | 96    | 0     | 0.26   |
| Samsung   | MZNLN256HCHP-00000 | 256 GB | 4       | 96    | 0     | 0.26   |
| Toshiba   | THNSNJ512GDNU A    | 512 GB | 1       | 96    | 0     | 0.26   |
| Londisk   | SSD                | 120 GB | 8       | 96    | 0     | 0.26   |
| Samsung   | MZNLN256HCHP-000L2 | 256 GB | 3       | 96    | 0     | 0.26   |
| Samsung   | SSD 860 PRO        | 512 GB | 17      | 95    | 0     | 0.26   |
| PHISON    | 256GB PS3110-S10C  | 256 GB | 1       | 95    | 0     | 0.26   |
| SanDisk   | SSD PLUS           | 120 GB | 27      | 95    | 0     | 0.26   |
| SPCC      | SSD                | 240 GB | 34      | 167   | 290   | 0.26   |
| Samsung   | MZNLN128HAHQ-000H1 | 128 GB | 20      | 100   | 66    | 0.26   |
| SPCC      | SSD170             | 120 GB | 3       | 245   | 341   | 0.26   |
| Micron    | 1100 SATA          | 256 GB | 6       | 190   | 1     | 0.26   |
| BHT       | WR202I0064G E70... | 64 GB  | 1       | 95    | 0     | 0.26   |
| ADATA     | SU655              | 120 GB | 4       | 95    | 0     | 0.26   |
| WDC       | WDS250G1B0B-00AS40 | 250 GB | 3       | 94    | 0     | 0.26   |
| Intel     | SSDSCKJF180A5L     | 180 GB | 1       | 94    | 0     | 0.26   |
| SanDisk   | SSD U100           | 256 GB | 1       | 94    | 0     | 0.26   |
| Transcend | TS120GSSD220S      | 120 GB | 12      | 94    | 0     | 0.26   |
| Kingston  | SUV500MS240G       | 240 GB | 5       | 93    | 0     | 0.26   |
| Team      | T2535T480G         | 480 GB | 1       | 93    | 0     | 0.26   |
| Pioneer   | APS-SL3N-240       | 240 GB | 2       | 93    | 0     | 0.26   |
| ADATA     | SU810NS38 SATA ... | 256 GB | 10      | 93    | 0     | 0.26   |
| KingFast  | SSD                | 240 GB | 1       | 93    | 0     | 0.26   |
| Mushkin   | MKNSSDSR250GB      | 250 GB | 1       | 93    | 0     | 0.26   |
| Samsung   | SSD 860 QVO        | 1 TB   | 70      | 93    | 0     | 0.26   |
| Samsung   | MZNLN128HCGR-000H1 | 128 GB | 1       | 93    | 0     | 0.25   |
| Samsung   | SSD 860 EVO        | 2 TB   | 15      | 92    | 0     | 0.25   |
| Gigabyte  | GP-GSTFS31240GNTD  | 240 GB | 11      | 92    | 0     | 0.25   |
| ADATA     | SU800              | 128 GB | 30      | 93    | 3     | 0.25   |
| Samsung   | MZMTD256HAGM-00000 | 256 GB | 1       | 92    | 0     | 0.25   |
| Kingston  | SV300S37A480G      | 480 GB | 14      | 98    | 73    | 0.25   |
| Lite-On   | PH2-CJ120          | 120 GB | 1       | 92    | 0     | 0.25   |
| Seagate   | BarraCuda SSD Z... | 250 GB | 3       | 92    | 0     | 0.25   |
| Patriot   | Burst              | 240 GB | 20      | 91    | 0     | 0.25   |
| AMD       | R5SL240G           | 240 GB | 10      | 105   | 1     | 0.25   |
| Gigabyte  | GP-GSTFS30512GTTD  | 512 GB | 3       | 91    | 0     | 0.25   |
| SanDisk   | SDSSDH3 1T00       | 1 TB   | 7       | 90    | 0     | 0.25   |
| Apacer    | AS350              | 480 GB | 2       | 90    | 0     | 0.25   |
| SanDisk   | SD9SB8W128G1001    | 128 GB | 1       | 90    | 0     | 0.25   |
| SanDisk   | SSD U100           | 24 GB  | 20      | 120   | 65    | 0.25   |
| Faspeed   | H5-60G PLUS        | 64 GB  | 1       | 90    | 0     | 0.25   |
| SanDisk   | SD7SB3Q256G1002    | 256 GB | 2       | 232   | 26    | 0.25   |
| Crucial   | CT960BX200SSD1     | 960 GB | 1       | 90    | 0     | 0.25   |
| Crucial   | CT3500SC           | 500 GB | 1       | 898   | 9     | 0.25   |
| Samsung   | SSD 860 EVO mSATA  | 500 GB | 4       | 89    | 0     | 0.25   |
| Plextor   | PH6-CE120-L1       | 120 GB | 2       | 89    | 0     | 0.24   |
| ADATA     | SU800              | 1 TB   | 9       | 89    | 0     | 0.24   |
| Crucial   | CT500MX500SSD1     | 500 GB | 72      | 88    | 0     | 0.24   |
| Lite-On   | LMT-256L9M-11 M... | 256 GB | 2       | 88    | 0     | 0.24   |
| Kingston  | RBU-SNS8151S396GG  | 96 GB  | 1       | 88    | 0     | 0.24   |
| SK hynix  | SC308 SATA         | 128 GB | 5       | 119   | 14    | 0.24   |
| Goodram   | IR-SSDPR-S25A-120  | 120 GB | 5       | 88    | 0     | 0.24   |
| Micron    | MTFDDAK256MAY-1... | 256 GB | 1       | 1492  | 16    | 0.24   |
| China     | SATA SSD           | 128 GB | 7       | 87    | 0     | 0.24   |
| Kingston  | SKC380S3120G       | 120 GB | 1       | 86    | 0     | 0.24   |
| SPCC      | M.2 SSD            | 256 GB | 2       | 86    | 0     | 0.24   |
| KingSpec  | P4-960             | 960 GB | 1       | 86    | 0     | 0.24   |
| Plextor   | PX-128M5Pro        | 128 GB | 51      | 86    | 0     | 0.24   |
| ADATA     | SU650              | 240 GB | 23      | 105   | 1     | 0.24   |
| Mushkin   | MKNSSDEC120GB      | 120 GB | 1       | 86    | 0     | 0.24   |
| Crucial   | CT240BX200SSD1     | 240 GB | 8       | 85    | 0     | 0.23   |
| China     | SSD                | 1 TB   | 2       | 85    | 0     | 0.23   |
| Verbatim  | Vi550 S3 SSD       | 128 GB | 1       | 85    | 0     | 0.23   |
| Intel     | SSDSCKKF256G8 SATA | 256 GB | 4       | 85    | 0     | 0.23   |
| Intel     | SSDMCEAF180A4L     | 180 GB | 1       | 85    | 0     | 0.23   |
| Samsung   | MZNTE128HMGR-000H1 | 128 GB | 1       | 85    | 0     | 0.23   |
| Plextor   | PX-256M3           | 256 GB | 1       | 256   | 2     | 0.23   |
| XPG       | SX950U             | 240 GB | 1       | 85    | 0     | 0.23   |
| ADATA     | SU800NS38          | 128 GB | 4       | 84    | 0     | 0.23   |
| SK hynix  | HFS256G3BTND-N210A | 256 GB | 4       | 84    | 0     | 0.23   |
| Lite-On   | L8H-256V2G-HP      | 256 GB | 6       | 84    | 0     | 0.23   |
| Vaseky    | V800-350G          | 360 GB | 1       | 84    | 0     | 0.23   |
| Samsung   | SSD 860 PRO        | 256 GB | 15      | 84    | 0     | 0.23   |
| Micron    | M600_MTFDDAK1T0MBF | 1 TB   | 2       | 84    | 0     | 0.23   |
| Transcend | TS256GSSD320       | 256 GB | 2       | 84    | 0     | 0.23   |
| Goodram   | SSDPR-CX400-512    | 512 GB | 7       | 83    | 0     | 0.23   |
| Dogfish   | SSD                | 1 TB   | 1       | 83    | 0     | 0.23   |
| China     | SATA SSD           | 64 GB  | 17      | 83    | 0     | 0.23   |
| Corsair   | Force LE200 SSD    | 120 GB | 4       | 82    | 0     | 0.23   |
| China     | SSD                | 256 GB | 6       | 82    | 0     | 0.23   |
| Lenovo    | SSD SL700 120G     | 120 GB | 2       | 82    | 0     | 0.23   |
| Lite-On   | CV8-8E128-11 SATA  | 128 GB | 11      | 82    | 0     | 0.23   |
| KingDian  | S280               | 480 GB | 3       | 82    | 0     | 0.23   |
| ADATA     | SU800NS38          | 512 GB | 2       | 154   | 3     | 0.22   |
| Apple     | SSD TS064C         | 64 GB  | 1       | 81    | 0     | 0.22   |
| OCZ       | VECTOR180          | 120 GB | 2       | 81    | 0     | 0.22   |
| ADATA     | SU750              | 256 GB | 2       | 81    | 0     | 0.22   |
| Lite-On   | LCS-128M6S         | 128 GB | 3       | 81    | 0     | 0.22   |
| Transcend | TS256GMTS400S      | 256 GB | 2       | 81    | 0     | 0.22   |
| Micron    | MTFDDAV256TBN-1... | 256 GB | 9       | 110   | 116   | 0.22   |
| Crucial   | CT240BX300SSD1     | 240 GB | 3       | 81    | 0     | 0.22   |
| Micron    | MTFDDAV512TBN      | 512 GB | 1       | 81    | 0     | 0.22   |
| Crucial   | CT2050MX300SSD1    | 2 TB   | 3       | 89    | 1     | 0.22   |
| Corsair   | Force LS SSD       | 480 GB | 1       | 80    | 0     | 0.22   |
| Kingston  | RBU-SNS8152S325... | 256 GB | 1       | 80    | 0     | 0.22   |
| Intel     | SSDSC2KB960G8      | 960 GB | 5       | 80    | 0     | 0.22   |
| Team      | TEAML5Lite3D240G   | 240 GB | 2       | 80    | 0     | 0.22   |
| ADATA     | SP580              | 120 GB | 12      | 80    | 0     | 0.22   |
| ADATA     | SU650              | 480 GB | 10      | 107   | 313   | 0.22   |
| HP        | SSD S700           | 250 GB | 7       | 79    | 0     | 0.22   |
| Lite-On   | LAT-256M2S         | 256 GB | 1       | 239   | 2     | 0.22   |
| Kingmax   | SSD                | 120 GB | 23      | 192   | 313   | 0.22   |
| Fordisk   | S860 256G 6Gbps    | 256 GB | 1       | 79    | 0     | 0.22   |
| China     | SSD 120G           | 120 GB | 3       | 79    | 0     | 0.22   |
| e2e4      | SSD                | 480 GB | 1       | 79    | 0     | 0.22   |
| Seagate   | ST120HM000-1G5142  | 120 GB | 1       | 79    | 0     | 0.22   |
| Toshiba   | Q300 Pro           | 128 GB | 1       | 79    | 0     | 0.22   |
| Samsung   | SSD 850            | 120 GB | 23      | 78    | 0     | 0.22   |
| China     | SATA SSD           | 120 GB | 33      | 78    | 0     | 0.22   |
| Patriot   | P200               | 1 TB   | 2       | 78    | 0     | 0.21   |
| WDC       | WDS400T2B0A-00SM50 | 4 TB   | 1       | 78    | 0     | 0.21   |
| Crucial   | CT240BX500SSD1     | 240 GB | 76      | 78    | 0     | 0.21   |
| Lite-On   | L8H-128V2G-11 M... | 128 GB | 2       | 77    | 0     | 0.21   |
| Intel     | SSDSCKKF512G8 SATA | 512 GB | 1       | 77    | 0     | 0.21   |
| Corsair   | Neutron XTI SSD    | 240 GB | 1       | 77    | 0     | 0.21   |
| Crucial   | CT960BX500SSD1     | 960 GB | 8       | 77    | 0     | 0.21   |
| Toshiba   | THNSNK128GVN8      | 128 GB | 4       | 77    | 0     | 0.21   |
| KingDian  | S180               | 64 GB  | 12      | 81    | 95    | 0.21   |
| Transcend | TS256GSSD340       | 256 GB | 2       | 76    | 0     | 0.21   |
| Intel     | SSDSC2BF240A4L     | 240 GB | 2       | 128   | 2     | 0.21   |
| Gigabyte  | GP-GSTFS30256GTTD  | 256 GB | 1       | 76    | 0     | 0.21   |
| Toshiba   | THNSNJ128G8NY      | 128 GB | 2       | 76    | 0     | 0.21   |
| Palit     | UVS                | 120 GB | 2       | 76    | 0     | 0.21   |
| SK hynix  | SHGS31-500GS-2     | 500 GB | 2       | 76    | 0     | 0.21   |
| Transcend | TS1TSSD230S        | 1 TB   | 3       | 76    | 0     | 0.21   |
| Lite-On   | CV3-8D256-41 SA... | 256 GB | 1       | 75    | 0     | 0.21   |
| Samsung   | SSD 650            | 120 GB | 3       | 75    | 0     | 0.21   |
| Crucial   | CT500MX500SSD4     | 500 GB | 20      | 75    | 0     | 0.21   |
| Transcend | TS64GSSD360S       | 64 GB  | 1       | 75    | 0     | 0.21   |
| Mushkin   | MKNSSDE3240GB      | 240 GB | 1       | 75    | 0     | 0.21   |
| ADATA     | SU810NS38 SATA ... | 128 GB | 1       | 75    | 0     | 0.21   |
| Samsung   | MZNLN256HCHP-000H1 | 256 GB | 1       | 74    | 0     | 0.21   |
| Kingston  | SMS200S330G        | 32 GB  | 2       | 246   | 10    | 0.21   |
| OCZ       | ONYX               | 32 GB  | 2       | 105   | 1     | 0.21   |
| China     | 64GB SSD           | 64 GB  | 11      | 74    | 0     | 0.20   |
| Crucial   | CT1000MX500SSD4    | 1 TB   | 16      | 74    | 0     | 0.20   |
| SanDisk   | SD7SN3Q128G1002    | 128 GB | 2       | 99    | 1     | 0.20   |
| KingDian  | S370               | 512 GB | 1       | 74    | 0     | 0.20   |
| PNY       | CS900 120GB SSD    | 120 GB | 24      | 74    | 0     | 0.20   |
| Samsung   | MZNLN256HAJQ-000L2 | 256 GB | 5       | 74    | 0     | 0.20   |
| Kingston  | SA400S37960G       | 960 GB | 13      | 74    | 0     | 0.20   |
| Reeinno   | ST240GB S4S3       | 240 GB | 1       | 74    | 0     | 0.20   |
| WDC       | WDS240G2G0B-00EPW0 | 240 GB | 40      | 73    | 1     | 0.20   |
| Samsung   | SSD 860 PRO        | 2 TB   | 3       | 73    | 0     | 0.20   |
| Intel     | SSDSC2KW256G8      | 256 GB | 20      | 73    | 0     | 0.20   |
| China     | SATA SSD           | 480 GB | 1       | 73    | 0     | 0.20   |
| Lite-On   | LCH-256V2S         | 256 GB | 2       | 73    | 0     | 0.20   |
| Kingston  | SUV500M8120G       | 120 GB | 6       | 73    | 0     | 0.20   |
| Kingrich  | K9 128GB SATA3 SSD | 128 GB | 1       | 657   | 8     | 0.20   |
| Kingston  | SUV500480G         | 480 GB | 8       | 83    | 143   | 0.20   |
| Crucial   | CT2000BX500SSD1    | 2 TB   | 3       | 72    | 0     | 0.20   |
| ADATA     | SU635              | 240 GB | 7       | 72    | 0     | 0.20   |
| Goodram   | SSDPR-CX400-256    | 256 GB | 6       | 72    | 0     | 0.20   |
| Goodram   | SSDPR-CL100-480-G2 | 480 GB | 3       | 71    | 0     | 0.20   |
| WDC       | WDS120G2G0A-00JH30 | 120 GB | 98      | 72    | 1     | 0.20   |
| Samsung   | Portable SSD T5    | 500 GB | 5       | 71    | 0     | 0.20   |
| Leven     | JAJS600M512C       | 512 GB | 2       | 71    | 0     | 0.20   |
| Vaseky    | V800-500G          | 512 GB | 1       | 71    | 0     | 0.20   |
| Toshiba   | THNSNH256GCST      | 256 GB | 1       | 71    | 0     | 0.20   |
| Plextor   | PX-256M6Pro        | 256 GB | 2       | 71    | 0     | 0.20   |
| SPCC      | SSD                | 512 GB | 12      | 82    | 16    | 0.19   |
| Micron    | 1100_MTFDDAV512TBN | 512 GB | 13      | 75    | 1     | 0.19   |
| Transcend | TS256GSSD370S      | 256 GB | 9       | 70    | 0     | 0.19   |
| Crucial   | CT250MX500SSD1     | 250 GB | 39      | 72    | 1     | 0.19   |
| SanDisk   | SD8SN8U-128G-1006  | 128 GB | 20      | 127   | 155   | 0.19   |
| OCZ       | SABER1000          | 480 GB | 1       | 70    | 0     | 0.19   |
| Transcend | TS128GSSD370       | 128 GB | 9       | 69    | 0     | 0.19   |
| SanDisk   | SSD i100           | 8 GB   | 3       | 69    | 0     | 0.19   |
| Lite-On   | LCS-128M6S-HP      | 128 GB | 4       | 69    | 0     | 0.19   |
| Team      | T2535T120G         | 120 GB | 2       | 142   | 4     | 0.19   |
| ADATA     | SU650              | 120 GB | 36      | 75    | 1     | 0.19   |
| Transcend | TS256GMTS800       | 256 GB | 2       | 69    | 0     | 0.19   |
| oyunkey   | SSD                | 120 GB | 1       | 68    | 0     | 0.19   |
| KingSpec  | MSH-256            | 256 GB | 2       | 68    | 0     | 0.19   |
| SanDisk   | PLUS               | 480 GB | 2       | 68    | 0     | 0.19   |
| Samsung   | MZNLN256HAJQ-00000 | 256 GB | 5       | 68    | 0     | 0.19   |
| China     | 240GB SSD          | 240 GB | 3       | 68    | 0     | 0.19   |
| ADATA     | S596               | 128 GB | 1       | 68    | 0     | 0.19   |
| WDC       | WDBNCE0010PNC      | 1 TB   | 2       | 68    | 0     | 0.19   |
| SanDisk   | SDSSDA480G         | 480 GB | 5       | 67    | 0     | 0.19   |
| Plextor   | PX-128M6M          | 128 GB | 4       | 67    | 0     | 0.19   |
| Lite-On   | LCS-256M6S         | 256 GB | 3       | 113   | 351   | 0.18   |
| ADATA     | SP900              | 512 GB | 2       | 66    | 0     | 0.18   |
| Toshiba   | TR200              | 240 GB | 20      | 66    | 0     | 0.18   |
| Integral  | V Series SATA SSD  | 240 GB | 3       | 66    | 0     | 0.18   |
| GLOWAY    | YCT512GS3-S7 Pro   | 512 GB | 1       | 66    | 0     | 0.18   |
| Goodram   | SSDPR-CX300-240    | 240 GB | 2       | 66    | 0     | 0.18   |
| Kingston  | HyperX Fury 3D     | 240 GB | 1       | 66    | 0     | 0.18   |
| Crucial   | CT1000BX500SSD1    | 1 TB   | 3       | 65    | 0     | 0.18   |
| Plextor   | PX-128M6S          | 128 GB | 26      | 70    | 43    | 0.18   |
| Plextor   | PX-512S2G          | 512 GB | 1       | 65    | 0     | 0.18   |
| SPCC      | SSD                | 55 GB  | 9       | 361   | 452   | 0.18   |
| Samsung   | MZNLN256HAJQ-000H1 | 256 GB | 10      | 82    | 20    | 0.18   |
| Lite-On   | LMT-32L3M-HP       | 32 GB  | 2       | 65    | 0     | 0.18   |
| Team      | T253X2128G         | 128 GB | 1       | 65    | 0     | 0.18   |
| Kingmax   | SSD                | 240 GB | 4       | 64    | 0     | 0.18   |
| Plextor   | PX-128S3C          | 128 GB | 12      | 64    | 0     | 0.18   |
| SanDisk   | SSD i110           | 32 GB  | 1       | 64    | 0     | 0.18   |
| WDC       | WDS100T2B0A        | 1 TB   | 1       | 128   | 1     | 0.18   |
| Kingston  | SA400M8240G        | 240 GB | 10      | 64    | 0     | 0.18   |
| Team      | T2535T240G         | 240 GB | 1       | 63    | 0     | 0.17   |
| Toshiba   | Q300               | 240 GB | 2       | 325   | 6     | 0.17   |
| Verbatim  | Vi500 S3 120GB SSD | 120 GB | 1       | 63    | 0     | 0.17   |
| ADATA     | SU655              | 480 GB | 1       | 63    | 0     | 0.17   |
| Transcend | TS128GMTS400S      | 128 GB | 2       | 63    | 0     | 0.17   |
| Intel     | SSDSC2KW010T8      | 1 TB   | 1       | 504   | 7     | 0.17   |
| Crucial   | CT480BX300SSD1     | 480 GB | 5       | 62    | 0     | 0.17   |
| Lite-On   | LCS-128L9S-11 2... | 128 GB | 1       | 62    | 0     | 0.17   |
| SanDisk   | SDSSDH2064G        | 64 GB  | 1       | 62    | 0     | 0.17   |
| KingSpec  | P4-480             | 480 GB | 2       | 62    | 0     | 0.17   |
| Intel     | SSDSC2BF480A5L     | 480 GB | 1       | 62    | 0     | 0.17   |
| Kingrich  | SSD 120G           | 120 GB | 1       | 62    | 0     | 0.17   |
| WDC       | WDS240G2G0A-00JH30 | 240 GB | 96      | 73    | 1     | 0.17   |
| SanDisk   | SSD PLUS           | 240 GB | 59      | 73    | 1     | 0.17   |
| Micron    | 1100_MTFDDAV256TBN | 256 GB | 44      | 69    | 89    | 0.17   |
| OCZ       | VERTEX460          | 240 GB | 2       | 61    | 0     | 0.17   |
| Lite-On   | LST-32S9G-11 SATA  | 32 GB  | 1       | 61    | 0     | 0.17   |
| Toshiba   | Q200 EX            | 240 GB | 1       | 61    | 0     | 0.17   |
| SK hynix  | HFS128G39TND-N210A | 128 GB | 27      | 105   | 10    | 0.17   |
| ADATA     | SU900              | 256 GB | 6       | 61    | 1     | 0.17   |
| Plextor   | PX-256M6S          | 256 GB | 10      | 69    | 214   | 0.17   |
| Gigabyte  | GP-GSTFS31100TNTD  | 1 TB   | 1       | 61    | 0     | 0.17   |
| GLOWAY    | FER120GS3-S7       | 120 GB | 3       | 60    | 0     | 0.17   |
| Lite-On   | LCH-512V2S-11 2... | 512 GB | 1       | 60    | 0     | 0.17   |
| PHISON    | 128GB PS3109-S9    | 128 GB | 1       | 121   | 1     | 0.17   |
| Micron    | MTFDDAV256MBF-1... | 256 GB | 4       | 60    | 0     | 0.17   |
| Samsung   | MZ7LN128HAHQ-000L1 | 128 GB | 2       | 60    | 0     | 0.17   |
| WDC       | WDS500G2B0A        | 500 GB | 12      | 60    | 0     | 0.17   |
| Samsung   | MZ7LN128HAHQ-000L2 | 128 GB | 10      | 60    | 0     | 0.17   |
| Apacer    | AS350              | 240 GB | 11      | 60    | 0     | 0.17   |
| Toshiba   | THNSN9480GESG      | 480 GB | 1       | 60    | 0     | 0.17   |
| Maxtor    | Z1 SSD             | 240 GB | 2       | 60    | 0     | 0.17   |
| SUNEAST   | SSD SE800          | 1.9 TB | 1       | 60    | 0     | 0.16   |
| BIWIN     | SSD                | 128 GB | 5       | 59    | 0     | 0.16   |
| Gigabyte  | GP-GSTFS31120GNTD  | 120 GB | 8       | 59    | 0     | 0.16   |
| KingDian  | S400               | 240 GB | 1       | 59    | 0     | 0.16   |
| Goodram   | IR-SSDPR-S25A-240  | 240 GB | 2       | 59    | 0     | 0.16   |
| Lite-On   | LMT-64M6M-HP       | 64 GB  | 1       | 59    | 0     | 0.16   |
| AGI       | AGI240G18AI238     | 240 GB | 1       | 59    | 0     | 0.16   |
| Team      | T253LE240G         | 240 GB | 2       | 59    | 0     | 0.16   |
| WDC       | WDS100T2G0A-00JH30 | 1 TB   | 5       | 59    | 0     | 0.16   |
| TEKET     | SA18-032M-4F       | 32 GB  | 2       | 59    | 0     | 0.16   |
| OCZ       | VERTEX2            | 180 GB | 1       | 58    | 0     | 0.16   |
| Plextor   | PX-512M6Pro        | 512 GB | 1       | 58    | 0     | 0.16   |
| BIWIN     | SSD                | 120 GB | 2       | 58    | 0     | 0.16   |
| HP        | SSD S700 Pro       | 256 GB | 2       | 58    | 0     | 0.16   |
| Kingston  | SKC380S3240G       | 240 GB | 1       | 58    | 0     | 0.16   |
| Transcend | TS128GMTS400       | 128 GB | 3       | 58    | 0     | 0.16   |
| Zheino    | CHN 25SATAC3 120   | 120 GB | 1       | 58    | 0     | 0.16   |
| Lite-On   | IT LCS-128L9S-HP   | 128 GB | 3       | 58    | 0     | 0.16   |
| ADATA     | IM2S3338-128GD2    | 128 GB | 3       | 57    | 0     | 0.16   |
| Lite-On   | CV3-8D256-11 SATA  | 256 GB | 3       | 57    | 0     | 0.16   |
| tigo      | SSD                | 120 GB | 1       | 57    | 0     | 0.16   |
| Goldkey   | GKH84-64GB         | 64 GB  | 1       | 57    | 0     | 0.16   |
| T-FORCE   | SSD                | 500 GB | 1       | 57    | 0     | 0.16   |
| Toshiba   | KSG60ZMV512G M.... | 512 GB | 2       | 57    | 0     | 0.16   |
| LDLC      | SSD                | 120 GB | 5       | 105   | 1     | 0.16   |
| Crucial   | CT512M550SSD3      | 512 GB | 4       | 108   | 176   | 0.16   |
| DeTech    | SSD                | 120 GB | 1       | 57    | 0     | 0.16   |
| Zheino    | CHN 25SATAS3 256   | 256 GB | 1       | 57    | 0     | 0.16   |
| SanDisk   | X600 M.2 2280 SATA | 256 GB | 1       | 56    | 0     | 0.16   |
| ADATA     | SP900NS38          | 128 GB | 3       | 124   | 339   | 0.16   |
| Crucial   | CT250BX100SSD1     | 250 GB | 21      | 58    | 1     | 0.16   |
| Samsung   | MZNTY256HDHP-00000 | 256 GB | 2       | 56    | 0     | 0.16   |
| ADATA     | SU630              | 240 GB | 13      | 59    | 1     | 0.16   |
| Super ... | FTM50N325H         | 500 GB | 2       | 56    | 0     | 0.15   |
| Lexar     | SSD                | 480 GB | 1       | 56    | 0     | 0.15   |
| Gigabyte  | GP-GSTFS31256GTND  | 256 GB | 1       | 56    | 0     | 0.15   |
| Radeon    | R7                 | 120 GB | 1       | 56    | 0     | 0.15   |
| Smartbuy  | mSata              | 256 GB | 2       | 55    | 0     | 0.15   |
| PNY       | SSD2SC120G1SA75... | 120 GB | 1       | 55    | 0     | 0.15   |
| Samsung   | MZYTE256HMHP-000L2 | 256 GB | 1       | 55    | 0     | 0.15   |
| Toshiba   | KSG60ZMV256G       | 256 GB | 1       | 55    | 0     | 0.15   |
| SanDisk   | SD6SB1M128G1022I   | 128 GB | 3       | 54    | 0     | 0.15   |
| KingSpec  | NT-256             | 256 GB | 6       | 54    | 0     | 0.15   |
| TAMMUZ    | SSD                | 128 GB | 1       | 54    | 0     | 0.15   |
| Lexar     | SSD                | 240 GB | 2       | 54    | 0     | 0.15   |
| KingSpec  | Q-720              | 720 GB | 3       | 54    | 0     | 0.15   |
| Netac     | SSD                | 1 TB   | 1       | 53    | 0     | 0.15   |
| Transcend | TS64GMTS800S       | 64 GB  | 1       | 53    | 0     | 0.15   |
| ADATA     | SU800              | 512 GB | 12      | 63    | 3     | 0.15   |
| Kingston  | SHPM2280P2-240G    | 240 GB | 1       | 1557  | 28    | 0.15   |
| SanDisk   | SDSSDH3500G        | 500 GB | 6       | 53    | 0     | 0.15   |
| Intel     | SSDSA2M160G2LE     | 160 GB | 2       | 1075  | 16    | 0.15   |
| Samsung   | MZMTD128HAFV-000H1 | 128 GB | 1       | 53    | 0     | 0.15   |
| Zheino    | CHN-25SATAA3-480   | 480 GB | 2       | 53    | 0     | 0.15   |
| Samsung   | SSD 860 PRO        | 1 TB   | 8       | 53    | 0     | 0.15   |
| Transcend | TS240GMTS420S      | 240 GB | 5       | 53    | 0     | 0.15   |
| Apacer    | AS340              | 240 GB | 1       | 157   | 2     | 0.14   |
| Apple     | SSD SM128E         | 121 GB | 1       | 52    | 0     | 0.14   |
| Intel     | SSDSCKKB240G8      | 240 GB | 1       | 52    | 0     | 0.14   |
| Hikvision | HS-SSD-C100 240G   | 240 GB | 2       | 52    | 0     | 0.14   |
| Team      | L7 EVO SSD         | 64 GB  | 1       | 51    | 0     | 0.14   |
| China     | 128GB SSD          | 128 GB | 11      | 51    | 0     | 0.14   |
| Intel     | SSDSCKKF128G8 SATA | 128 GB | 4       | 51    | 0     | 0.14   |
| Lite-On   | LMT-19nmBGA-128G   | 128 GB | 1       | 51    | 0     | 0.14   |
| Apacer    | AS350              | 512 GB | 5       | 63    | 1     | 0.14   |
| ADATA     | SP610              | 128 GB | 3       | 51    | 0     | 0.14   |
| ADATA     | SU650NS38          | 480 GB | 1       | 51    | 0     | 0.14   |
| Seagate   | ZA1920NM10001      | 1.9 TB | 4       | 51    | 0     | 0.14   |
| Lite-On   | IT LCS-256L9S      | 256 GB | 1       | 51    | 0     | 0.14   |
| Patriot   | Burst              | 120 GB | 26      | 51    | 0     | 0.14   |
| Lite-On   | CV3-8D128          | 128 GB | 2       | 50    | 0     | 0.14   |
| SK hynix  | SC401 SATA         | 512 GB | 3       | 140   | 105   | 0.14   |
| KingSpec  | Q-180              | 180 GB | 4       | 58    | 235   | 0.14   |
| Samsung   | SSD PM871b M.2 ... | 256 GB | 1       | 50    | 0     | 0.14   |
| Samsung   | SSD PB22-CS3 FD... | 256 GB | 1       | 50    | 0     | 0.14   |
| OCZ       | INTREPID 3800      | 400 GB | 1       | 50    | 0     | 0.14   |
| WDC       | WDS500G2B0B        | 500 GB | 5       | 49    | 0     | 0.14   |
| Corsair   | Neutron GTX SSD    | 480 GB | 1       | 49    | 0     | 0.14   |
| V-GeN     | V-GEN12AS19AR12... | 120 GB | 1       | 49    | 0     | 0.14   |
| China     | SSD                | 240 GB | 14      | 57    | 1     | 0.13   |
| KingDian  | S200               | 120 GB | 2       | 49    | 0     | 0.13   |
| Transcend | TSA                | 1 TB   | 1       | 49    | 0     | 0.13   |
| SanDisk   | SDSA5DK 32G        | 32 GB  | 1       | 49    | 0     | 0.13   |
| KingSpec  | P3-512             | 512 GB | 8       | 69    | 226   | 0.13   |
| Samsung   | MZNTY128HDHP-00000 | 128 GB | 2       | 48    | 0     | 0.13   |
| Vaseky    | V800-128G          | 128 GB | 2       | 48    | 0     | 0.13   |
| HP        | SSD S700 Pro       | 1 TB   | 1       | 48    | 0     | 0.13   |
| Lite-On   | LSS-32L6G-HP       | 32 GB  | 3       | 48    | 0     | 0.13   |
| LDLC      | SSD F7 PLUS 3D ... | 240 GB | 1       | 48    | 0     | 0.13   |
| Lexar     | 256GB SSD          | 256 GB | 4       | 48    | 0     | 0.13   |
| SanDisk   | SD9SN8W128G1002    | 128 GB | 3       | 48    | 0     | 0.13   |
| ADATA     | SU630              | 960 GB | 2       | 73    | 1     | 0.13   |
| OCZ       | VECTOR180          | 480 GB | 1       | 48    | 0     | 0.13   |
| SK hynix  | HFS128G32MND-3212A | 128 GB | 1       | 48    | 0     | 0.13   |
| Transcend | TS256GMTS430S      | 256 GB | 6       | 47    | 0     | 0.13   |
| Lite-On   | CV3-DE256          | 256 GB | 3       | 47    | 0     | 0.13   |
| Samsung   | SSD 860 QVO        | 4 TB   | 4       | 47    | 0     | 0.13   |
| GeIL      | R3 120G            | 120 GB | 1       | 47    | 0     | 0.13   |
| China     | 80GB SSD           | 80 GB  | 2       | 47    | 0     | 0.13   |
| Intel     | SSDSC2KW128G8      | 128 GB | 6       | 47    | 0     | 0.13   |
| AMD       | R3SL120G           | 120 GB | 25      | 46    | 1     | 0.13   |
| SPCC      | M.2 SSD            | 120 GB | 3       | 107   | 2     | 0.13   |
| Plextor   | PX-256M8VG         | 256 GB | 1       | 46    | 0     | 0.13   |
| AMD       | R3SL60G            | 64 GB  | 3       | 46    | 0     | 0.13   |
| Intel     | SSDSC2KG240G8      | 240 GB | 2       | 46    | 0     | 0.13   |
| Crucial   | CT128M550SSD1      | 128 GB | 5       | 193   | 25    | 0.13   |
| SanDisk   | SSD PLUS           | 1 TB   | 13      | 84    | 2     | 0.13   |
| China     | SSD                | 128 GB | 21      | 45    | 0     | 0.13   |
| ADATA     | SP920SS            | 256 GB | 6       | 132   | 8     | 0.13   |
| SanDisk   | SD5SF2032G1010E    | 32 GB  | 1       | 45    | 0     | 0.13   |
| KingDian  | S280-240GB         | 240 GB | 8       | 45    | 0     | 0.12   |
| Kingston  | RBU-SC152S37128GG2 | 128 GB | 1       | 45    | 0     | 0.12   |
| SanDisk   | pSSD               | 128 GB | 8       | 45    | 3     | 0.12   |
| Zheino    | CHN mSATA02M 128   | 128 GB | 1       | 45    | 0     | 0.12   |
| BHT       | WR202H0032G E70... | 32 GB  | 1       | 45    | 0     | 0.12   |
| KingSpec  | P3-1TB             | 1 TB   | 2       | 44    | 0     | 0.12   |
| Hikvision | HS-SSD-E100 128G   | 128 GB | 1       | 133   | 2     | 0.12   |
| PRETEC    | G2000 SSD          | 32 GB  | 1       | 44    | 0     | 0.12   |
| HP        | SSD S700           | 500 GB | 3       | 43    | 0     | 0.12   |
| Plextor   | PX-512M3           | 512 GB | 1       | 1402  | 31    | 0.12   |
| Transcend | TS64GMSA370        | 64 GB  | 3       | 43    | 0     | 0.12   |
| BIOSTAR   | S100-120GB         | 120 GB | 1       | 43    | 0     | 0.12   |
| KingSpec  | NT-128             | 128 GB | 1       | 43    | 0     | 0.12   |
| Kingston  | RBUSNS8180S3128GI1 | 128 GB | 2       | 43    | 0     | 0.12   |
| ADATA     | SU630              | 480 GB | 5       | 64    | 190   | 0.12   |
| China     | SSD                | 120 GB | 13      | 56    | 2     | 0.12   |
| Samsung   | MZMPC128HBFU-000MV | 128 GB | 2       | 43    | 0     | 0.12   |
| Transcend | TS128GSSD370S      | 128 GB | 19      | 42    | 0     | 0.12   |
| Intel     | SSDSCKKF010X6      | 1 TB   | 1       | 42    | 0     | 0.12   |
| China     | SSD128G            | 128 GB | 1       | 42    | 0     | 0.12   |
| Team      | TM8PS7256G         | 256 GB | 3       | 42    | 0     | 0.12   |
| Lite-On   | CV3-8D128-11 SATA  | 128 GB | 4       | 42    | 0     | 0.12   |
| SanDisk   | SD8SFAT128G1122    | 128 GB | 1       | 42    | 0     | 0.12   |
| AMD       | R5SL120G           | 120 GB | 9       | 57    | 1     | 0.12   |
| Intenso   | SSD Sata III       | 256 GB | 5       | 46    | 1     | 0.12   |
| Intel     | SSDSC2KG480G8      | 480 GB | 1       | 42    | 0     | 0.12   |
| Team      | T253X2001T         | 1 TB   | 3       | 42    | 0     | 0.12   |
| KingSpec  | NT-64              | 64 GB  | 1       | 41    | 0     | 0.11   |
| Crucial   | CT500MX500SSD4N    | 500 GB | 1       | 41    | 0     | 0.11   |
| PNY       | SSD2SC240G5SA75... | 240 GB | 1       | 41    | 0     | 0.11   |
| KingDian  | S280               | 1 TB   | 3       | 41    | 0     | 0.11   |
| GALAX     | TA1D0240A          | 240 GB | 1       | 41    | 0     | 0.11   |
| Intenso   | SSD SATAIII        | 480 GB | 3       | 40    | 0     | 0.11   |
| Kingston  | RBU-SUS151S364GD   | 64 GB  | 2       | 40    | 0     | 0.11   |
| Apacer    | AS340              | 480 GB | 4       | 40    | 0     | 0.11   |
| KingDian  | P10                | 240 GB | 1       | 39    | 0     | 0.11   |
| Seagate   | ST480HM000         | 480 GB | 1       | 39    | 0     | 0.11   |
| WDC       | WDS480G2G0B-00EPW0 | 480 GB | 6       | 39    | 0     | 0.11   |
| Samsung   | MZ7TY128HDHP-00000 | 128 GB | 1       | 39    | 0     | 0.11   |
| Kingston  | SH103S3480G        | 480 GB | 1       | 38    | 0     | 0.11   |
| DOGFISH   | SSD                | 256 GB | 1       | 38    | 0     | 0.11   |
| Lite-On   | CV8-8E256-11 SATA  | 256 GB | 2       | 38    | 0     | 0.11   |
| Micron    | MTFDDAV256TBN      | 256 GB | 1       | 114   | 2     | 0.10   |
| Faspeed   | K5-120G            | 120 GB | 1       | 38    | 0     | 0.10   |
| KingSpec  | T-64               | 64 GB  | 4       | 46    | 2     | 0.10   |
| Zheino    | CHN-mSATAM3-128    | 128 GB | 1       | 37    | 0     | 0.10   |
| Plextor   | PX-128M6Pro        | 128 GB | 10      | 39    | 1     | 0.10   |
| Transcend | TS64GSSD370S       | 64 GB  | 1       | 37    | 0     | 0.10   |
| Corsair   | CSSD-V60GB2        | 64 GB  | 1       | 332   | 8     | 0.10   |
| SanDisk   | SD6PP4M-256G-1006  | 256 GB | 2       | 36    | 0     | 0.10   |
| Micron    | MTFDDAK512MAY-1... | 512 GB | 1       | 624   | 16    | 0.10   |
| Intel     | SSDSA1M080G2HP     | 80 GB  | 1       | 476   | 12    | 0.10   |
| KingDian  | S280               | 240 GB | 11      | 36    | 0     | 0.10   |
| Transcend | TS512GMSA370       | 512 GB | 2       | 36    | 0     | 0.10   |
| Crucial   | CT120BX500SSD1     | 120 GB | 68      | 36    | 0     | 0.10   |
| ADATA     | SP550              | 120 GB | 26      | 36    | 1     | 0.10   |
| PNY       | SSD2SC120G726A1... | 120 GB | 1       | 35    | 0     | 0.10   |
| SanDisk   | Z400s M.2 2280     | 128 GB | 2       | 35    | 0     | 0.10   |
| Seagate   | BarraCuda SSD Z... | 500 GB | 8       | 35    | 0     | 0.10   |
| Lite-On   | IT LMT-128L9M      | 128 GB | 2       | 35    | 0     | 0.10   |
| Netac     | SSD                | 480 GB | 1       | 35    | 0     | 0.10   |
| Plextor   | PX-256S3C          | 256 GB | 1       | 34    | 0     | 0.10   |
| Kingston  | RBUSNS8180DS3128GH | 128 GB | 5       | 34    | 0     | 0.10   |
| Toshiba   | KHK61RSE1T92       | 1.9 TB | 8       | 34    | 0     | 0.10   |
| PNY       | SSD2SC240G1LC70... | 240 GB | 2       | 34    | 0     | 0.10   |
| Plextor   | PX-64M5M           | 64 GB  | 1       | 34    | 0     | 0.10   |
| Kingston  | SUV500MS120G       | 120 GB | 9       | 47    | 135   | 0.09   |
| Patriot   | Burst              | 480 GB | 13      | 46    | 1     | 0.09   |
| Crucial   | FCCT256M4SSD1      | 256 GB | 1       | 34    | 0     | 0.09   |
| ZOTAC     | SATA SSD           | 120 GB | 2       | 34    | 0     | 0.09   |
| Toshiba   | KSG60ZMV256G M.... | 256 GB | 5       | 41    | 20    | 0.09   |
| SanDisk   | SD8SN8U128G1122    | 128 GB | 1       | 34    | 0     | 0.09   |
| ADATA     | SX950              | 240 GB | 1       | 34    | 0     | 0.09   |
| Kingston  | SSDNOW             | 32 GB  | 1       | 34    | 0     | 0.09   |
| Kingston  | SA400M8120G        | 120 GB | 5       | 33    | 0     | 0.09   |
| AMD       | R5S240GBSF         | 240 GB | 1       | 33    | 0     | 0.09   |
| Apacer    | AS350              | 128 GB | 9       | 33    | 0     | 0.09   |
| Lite-On   | LMH-256V2M-11 M... | 256 GB | 4       | 33    | 0     | 0.09   |
| Intel     | SSDSA1MH080G1HP    | 80 GB  | 1       | 33    | 0     | 0.09   |
| RECADATA  | RD-S325MCN-N2563   | 240 GB | 1       | 33    | 0     | 0.09   |
| SanDisk   | SD6SB1M-032G-1006  | 32 GB  | 1       | 33    | 0     | 0.09   |
| SK hynix  | HFS256G32MND-2200A | 256 GB | 2       | 242   | 78    | 0.09   |
| KingDian  | S280               | 120 GB | 9       | 33    | 0     | 0.09   |
| SK hynix  | HFS256G32TNF-N3A0A | 256 GB | 2       | 33    | 0     | 0.09   |
| Samsung   | MZ7LN256HAJQ-000L2 | 256 GB | 9       | 32    | 0     | 0.09   |
| Corsair   | CSSD-F120GB3-BK    | 120 GB | 2       | 58    | 509   | 0.09   |
| Smartbuy  | mSata              | 128 GB | 2       | 32    | 0     | 0.09   |
| Samsung   | SSD PM851          | 128 GB | 1       | 32    | 0     | 0.09   |
| KingSpec  | ACSC4M512mSA       | 506 GB | 1       | 32    | 0     | 0.09   |
| OCZ       | VERTEX4            | 80 GB  | 1       | 129   | 3     | 0.09   |
| Lite-On   | L8T-128L6G-HP      | 128 GB | 2       | 32    | 640   | 0.09   |
| SanDisk   | SDSSDXP120G        | 120 GB | 1       | 32    | 0     | 0.09   |
| Toshiba   | THNSNB062GMCJ      | 64 GB  | 1       | 32    | 0     | 0.09   |
| KingDian  | S200               | 64 GB  | 6       | 36    | 22    | 0.09   |
| Team      | L5 LITE SSD        | 64 GB  | 2       | 37    | 1     | 0.09   |
| LDLC      | SSD                | 480 GB | 2       | 43    | 1     | 0.09   |
| Transcend | TS512GMTS400       | 512 GB | 1       | 31    | 0     | 0.09   |
| ADATA     | SU900              | 1 TB   | 3       | 33    | 1     | 0.09   |
| Kingston  | RBUSNS8180DS3512GJ | 512 GB | 4       | 31    | 0     | 0.09   |
| China     | T480               | 480 GB | 2       | 65    | 138   | 0.09   |
| Smartbuy  | SSD                | 512 GB | 2       | 31    | 0     | 0.09   |
| OCZ       | TRION150           | 480 GB | 1       | 31    | 0     | 0.09   |
| KingSpec  | KSD-SA25.7-016MJ   | 16 GB  | 2       | 30    | 0     | 0.08   |
| Patriot   | P200               | 256 GB | 4       | 30    | 0     | 0.08   |
| China     | SH00R240GB         | 240 GB | 2       | 30    | 0     | 0.08   |
| Hajaan    | SSD 256G           | 256 GB | 1       | 30    | 0     | 0.08   |
| Samsung   | MZ7LN256HAJQ-00000 | 256 GB | 1       | 30    | 0     | 0.08   |
| PNY       | SSD2SC120G1CS17... | 120 GB | 2       | 30    | 0     | 0.08   |
| Samsung   | Portable SSD T5    | 1 TB   | 3       | 30    | 0     | 0.08   |
| SK hynix  | HFS128G39MNC-3510A | 128 GB | 1       | 30    | 0     | 0.08   |
| Goodram   | SSDPR-CL100-240-G2 | 240 GB | 2       | 30    | 0     | 0.08   |
| SanDisk   | SDSA5DK-016G-1006  | 16 GB  | 1       | 29    | 0     | 0.08   |
| KingPower | 1108 SSD           | 64 GB  | 1       | 29    | 0     | 0.08   |
| KingSpec  | P3-128             | 128 GB | 10      | 79    | 16    | 0.08   |
| Transcend | TS120GMTS420S      | 120 GB | 10      | 31    | 1     | 0.08   |
| Micron    | 1300_MTFDDAK256TDL | 256 GB | 1       | 29    | 0     | 0.08   |
| Samsung   | SSD Thin uSATA ... | 128 GB | 1       | 378   | 12    | 0.08   |
| KingSpec  | MT-128             | 128 GB | 4       | 29    | 0     | 0.08   |
| Samsung   | MZNLN256HAJQ-000L7 | 256 GB | 4       | 29    | 0     | 0.08   |
| Intenso   | SSD Sata III       | 1 TB   | 1       | 29    | 0     | 0.08   |
| ADATA     | SU800              | 2 TB   | 3       | 36    | 2     | 0.08   |
| Patriot   | Spark              | 256 GB | 2       | 28    | 0     | 0.08   |
| China     | Mit-SSD512A        | 512 GB | 1       | 28    | 0     | 0.08   |
| Toshiba   | THNSNF256GMCS      | 256 GB | 1       | 28    | 0     | 0.08   |
| Kingmax   | SSD                | 64 GB  | 24      | 196   | 521   | 0.08   |
| TAISU     | SSD 240G           | 240 GB | 1       | 27    | 0     | 0.08   |
| Phison    | SATA SSD           | 960 GB | 2       | 27    | 0     | 0.08   |
| SenDisk   | C3-60G             | 64 GB  | 1       | 27    | 0     | 0.08   |
| Lenovo    | Thinklife SSD S... | 480 GB | 1       | 27    | 0     | 0.07   |
| KingSpec  | CHA-M2B7-M256      | 256 GB | 2       | 27    | 0     | 0.07   |
| Micron    | 5200_MTFDDAK960TDC | 960 GB | 1       | 26    | 0     | 0.07   |
| HECTRON   | HECX1-240G         | 240 GB | 1       | 26    | 0     | 0.07   |
| Transcend | TS64GSSD720        | 64 GB  | 1       | 26    | 0     | 0.07   |
| Transcend | TS64GSSD320        | 64 GB  | 1       | 26    | 0     | 0.07   |
| Plextor   | PX-256M6GV-2280    | 256 GB | 1       | 26    | 0     | 0.07   |
| Lite-On   | LMH-512V2M-11 M... | 512 GB | 1       | 26    | 0     | 0.07   |
| Intel     | SSDSC2BB240G7      | 240 GB | 2       | 25    | 0     | 0.07   |
| KingSpec  | T-120              | 120 GB | 1       | 25    | 0     | 0.07   |
| SK hynix  | HFS512G39TNF-N3A0A | 512 GB | 1       | 25    | 0     | 0.07   |
| Lite-On   | CV1-8B256          | 256 GB | 4       | 25    | 0     | 0.07   |
| Toshiba   | THNSNH128G8NT      | 128 GB | 1       | 25    | 0     | 0.07   |
| SanDisk   | SD8SBAT128G1122    | 128 GB | 5       | 25    | 0     | 0.07   |
| Plextor   | PX-512M5Pro        | 512 GB | 1       | 25    | 0     | 0.07   |
| Seagate   | BarraCuda 120 S... | 500 GB | 2       | 25    | 0     | 0.07   |
| SK hynix  | HFS256G32MND-2900A | 256 GB | 1       | 531   | 20    | 0.07   |
| SanDisk   | SDSSDA-1T00        | 1 TB   | 2       | 25    | 0     | 0.07   |
| China     | 512GB SSD          | 512 GB | 1       | 25    | 0     | 0.07   |
| Lite-On   | CV5-8Q256          | 256 GB | 1       | 24    | 0     | 0.07   |
| Mushkin   | MKNSSDCR60GB-7     | 64 GB  | 2       | 81    | 2     | 0.07   |
| Team      | TM8PS7512G         | 512 GB | 2       | 24    | 0     | 0.07   |
| Apacer    | AS510S             | 256 GB | 1       | 24    | 0     | 0.07   |
| Corsair   | CSSD-V32GB2        | 32 GB  | 1       | 99    | 3     | 0.07   |
| Dogfish   | SSD                | 500 GB | 1       | 24    | 0     | 0.07   |
| Intel     | SSDSC2KF256H6L     | 256 GB | 3       | 123   | 11    | 0.07   |
| Goodram   | SSDPR-CL100-120-G2 | 120 GB | 5       | 24    | 0     | 0.07   |
| Plextor   | PX-128S2C          | 128 GB | 2       | 24    | 0     | 0.07   |
| SK hynix  | SHGS31-1000GS-2    | 1 TB   | 1       | 24    | 0     | 0.07   |
| Lite-On   | L8H-256V2G         | 256 GB | 1       | 24    | 0     | 0.07   |
| Samsung   | MZNLN512HCJH-000L2 | 512 GB | 1       | 23    | 0     | 0.07   |
| Seagate   | BarraCuda SSD Z... | 1 TB   | 3       | 23    | 0     | 0.07   |
| PNY       | SSD2SC120G1SA75... | 120 GB | 1       | 23    | 0     | 0.07   |
| KingSpec  | Q-360              | 360 GB | 3       | 23    | 0     | 0.07   |
| SK hynix  | HFS256G32TNH-73A0A | 256 GB | 3       | 23    | 0     | 0.06   |
| LDLC      | SSD                | 128 GB | 4       | 23    | 0     | 0.06   |
| Verbatim  | Vi500 S3 240GB SSD | 240 GB | 1       | 23    | 0     | 0.06   |
| addlink   | SATA SSD           | 1 TB   | 1       | 23    | 0     | 0.06   |
| Kingch... | SSD                | 32 GB  | 1       | 23    | 0     | 0.06   |
| Intel     | SSDSC2KB019T8      | 1.9 TB | 2       | 23    | 0     | 0.06   |
| Transcend | TS128GMTS800       | 128 GB | 4       | 23    | 0     | 0.06   |
| GLOWAY    | FER240GS3-S7       | 240 GB | 1       | 23    | 0     | 0.06   |
| KINGBANK  | KP330              | 480 GB | 1       | 23    | 0     | 0.06   |
| TCSUNBOW  | N4                 | 240 GB | 1       | 22    | 0     | 0.06   |
| Goodram   | IRP-SSDPR-S25C-512 | 512 GB | 1       | 22    | 0     | 0.06   |
| Plextor   | PX-128S1G          | 128 GB | 1       | 22    | 0     | 0.06   |
| Gigabyte  | GP-GSTFS31480GNTD  | 480 GB | 1       | 22    | 0     | 0.06   |
| Intel     | SSDSC2KI128G8      | 128 GB | 1       | 22    | 0     | 0.06   |
| Toshiba   | THNSNS060GBSP      | 64 GB  | 1       | 22    | 0     | 0.06   |
| Kingston  | 480GBV500          | 480 GB | 1       | 22    | 0     | 0.06   |
| Plextor   | PX-128M6V          | 128 GB | 1       | 22    | 0     | 0.06   |
| Hoodisk   | SSD                | 128 GB | 1       | 22    | 0     | 0.06   |
| Kingston  | SKC300S37A180G     | 180 GB | 2       | 166   | 1025  | 0.06   |
| WDC       | WDS100T2B0B        | 1 TB   | 2       | 22    | 0     | 0.06   |
| Zheino    | CHN25SATAS1 256    | 256 GB | 1       | 22    | 0     | 0.06   |
| Ramaxel   | RTITF128PCA1MADL   | 128 GB | 1       | 22    | 0     | 0.06   |
| Crucial   | CT250MX500SSD4     | 250 GB | 3       | 22    | 0     | 0.06   |
| Foxline   | FLSSD480X5SE       | 480 GB | 1       | 22    | 0     | 0.06   |
| Kingston  | SKC600512G         | 512 GB | 3       | 22    | 0     | 0.06   |
| Micron    | MTFDDAK256TDL      | 256 GB | 3       | 21    | 0     | 0.06   |
| WDC       | WDS480G2G0A-00JH30 | 480 GB | 14      | 21    | 0     | 0.06   |
| Transcend | TS128GMSA370       | 128 GB | 2       | 21    | 0     | 0.06   |
| Transcend | TS32GSSD370S       | 32 GB  | 10      | 21    | 0     | 0.06   |
| Plextor   | PX-256M6M          | 256 GB | 3       | 29    | 1     | 0.06   |
| Maximus   | SSD                | 128 GB | 1       | 21    | 0     | 0.06   |
| Crucial   | CT120BX100SSD1     | 120 GB | 1       | 21    | 0     | 0.06   |
| OCZ       | INTREPID 3600      | 400 GB | 1       | 21    | 0     | 0.06   |
| Lite-On   | LSS-24L6G          | 24 GB  | 1       | 21    | 0     | 0.06   |
| Intel     | SSDSC2KB240G8L ... | 240 GB | 2       | 20    | 0     | 0.06   |
| Lite-On   | CV3-CE256-11 SATA  | 256 GB | 1       | 20    | 0     | 0.06   |
| Goldkey   | GKH84-256GB        | 256 GB | 1       | 20    | 0     | 0.06   |
| PNY       | CS900 500GB SSD    | 500 GB | 4       | 20    | 0     | 0.06   |
| Transcend | TS240GMTS820S      | 240 GB | 3       | 20    | 0     | 0.06   |
| Apacer    | AS350              | 120 GB | 8       | 20    | 1     | 0.06   |
| Lenovo    | SSD SL700 480G     | 480 GB | 1       | 20    | 0     | 0.06   |
| AMD       | R3SL240G           | 240 GB | 4       | 44    | 1     | 0.06   |
| XUNZHE    | XUNZHE800S 120G    | 120 GB | 1       | 20    | 0     | 0.05   |
| Netac     | SSD 120G           | 120 GB | 1       | 19    | 0     | 0.05   |
| SK hynix  | HFS128G39TNF-N3A0A | 128 GB | 5       | 19    | 0     | 0.05   |
| ADATA     | SU800NS38          | 256 GB | 6       | 33    | 195   | 0.05   |
| Transcend | TS128GSSD230S      | 128 GB | 10      | 19    | 0     | 0.05   |
| Micron    | MTFDDAK1T0TBN-1... | 1 TB   | 1       | 19    | 0     | 0.05   |
| Plextor   | PX-256M8VC         | 256 GB | 3       | 18    | 0     | 0.05   |
| Intel     | SSDSCKJF240A5L     | 240 GB | 2       | 84    | 6     | 0.05   |
| Lite-On   | CV1-8B256-HP       | 256 GB | 1       | 18    | 0     | 0.05   |
| Corsair   | Neutron SSD        | 240 GB | 1       | 2126  | 114   | 0.05   |
| Lite-On   | CV1-8B128          | 128 GB | 4       | 18    | 0     | 0.05   |
| China     | SSD                | 512 GB | 2       | 18    | 0     | 0.05   |
| ADATA     | SP610              | 256 GB | 1       | 18    | 0     | 0.05   |
| Hyperdisk | SDOM               | 16 GB  | 1       | 18    | 0     | 0.05   |
| Lexar     | SSD                | 128 GB | 3       | 18    | 0     | 0.05   |
| SanDisk   | SDSSDH3 500G       | 500 GB | 6       | 18    | 0     | 0.05   |
| FORESEE   | 128GB SSD          | 128 GB | 8       | 17    | 0     | 0.05   |
| SanDisk   | SD8SN8U1T001122    | 1 TB   | 1       | 17    | 0     | 0.05   |
| Team      | T253X1240G         | 240 GB | 4       | 17    | 0     | 0.05   |
| Team      | TM8PS5256G         | 256 GB | 1       | 17    | 0     | 0.05   |
| China     | 60GB SSD           | 64 GB  | 1       | 17    | 0     | 0.05   |
| Kingston  | RBUSNS8180DS3128GJ | 128 GB | 4       | 17    | 0     | 0.05   |
| China     | RTMMB256VBV4KFY    | 256 GB | 1       | 17    | 0     | 0.05   |
| OWC       | Neptune 6G SSD     | 480 GB | 1       | 17    | 0     | 0.05   |
| Kingrich  | 64GB K9 SATA3 SSD  | 64 GB  | 2       | 17    | 0     | 0.05   |
| AMD       | R3S60GBSM          | 64 GB  | 2       | 17    | 0     | 0.05   |
| Lite-On   | CV8-8E256          | 256 GB | 5       | 16    | 0     | 0.05   |
| LDNDISK   | SSD                | 240 GB | 1       | 16    | 0     | 0.05   |
| KingSpec  | P4-240             | 240 GB | 7       | 20    | 1     | 0.05   |
| China     | SSD                | 360 GB | 6       | 16    | 0     | 0.05   |
| Lite-On   | L8H-256V2G-11 M... | 256 GB | 2       | 16    | 0     | 0.05   |
| Intel     | SSDSCKKF512H6 SATA | 512 GB | 1       | 249   | 14    | 0.05   |
| XrayDisk  | SSD                | 240 GB | 2       | 16    | 0     | 0.05   |
| Intel     | SSDSA1M160G2HP     | 160 GB | 6       | 102   | 14    | 0.05   |
| Drevo     | X1                 | 120 GB | 1       | 49    | 2     | 0.04   |
| Platinet  | SSD                | 120 GB | 1       | 16    | 0     | 0.04   |
| AEGO      | SSD                | 240 GB | 3       | 16    | 0     | 0.04   |
| Intel     | SSDSA2M080G2GN     | 80 GB  | 1       | 245   | 14    | 0.04   |
| Intel     | SSDMCEAW080A4      | 80 GB  | 1       | 16    | 0     | 0.04   |
| SanDisk   | SSD G5 BICS4       | 500 GB | 4       | 16    | 0     | 0.04   |
| Apple     | SSD SM256E         | 256 GB | 1       | 15    | 0     | 0.04   |
| FASTDISK  | FASTDISK120G       | 120 GB | 1       | 15    | 0     | 0.04   |
| SanDisk   | SD8SNAT128G1122    | 128 GB | 1       | 15    | 0     | 0.04   |
| Lexar     | 512GB SSD          | 512 GB | 1       | 15    | 0     | 0.04   |
| ADATA     | SP900NS34          | 128 GB | 2       | 230   | 508   | 0.04   |
| SanDisk   | SSD U100           | 64 GB  | 7       | 17    | 1     | 0.04   |
| FORESEE   | 240GB SSD          | 240 GB | 1       | 15    | 0     | 0.04   |
| Transcend | TS64GSSD25S-M      | 64 GB  | 2       | 15    | 0     | 0.04   |
| T-FORCE   | SSD                | 1 TB   | 1       | 15    | 0     | 0.04   |
| e2e4      | SSD                | 120 GB | 3       | 15    | 0     | 0.04   |
| Lite-On   | CV1-SB128          | 128 GB | 1       | 15    | 0     | 0.04   |
| SPCC      | SSD                | 480 GB | 1       | 15    | 0     | 0.04   |
| Leven     | JAJS500M120C-1     | 120 GB | 1       | 15    | 0     | 0.04   |
| China     | SSD                | 64 GB  | 3       | 14    | 0     | 0.04   |
| FASTDISK  | SSD 60G            | 64 GB  | 1       | 14    | 0     | 0.04   |
| Team      | T253TD001T         | 1 TB   | 1       | 14    | 0     | 0.04   |
| Samsung   | MZNLN128HAHQ-000L1 | 128 GB | 1       | 14    | 0     | 0.04   |
| Lenovo    | SSD SL700 M.2 128G | 128 GB | 1       | 14    | 0     | 0.04   |
| Seagate   | ST480FP0021        | 480 GB | 1       | 14    | 0     | 0.04   |
| SK hynix  | SH920 mSATA        | 256 GB | 2       | 628   | 44    | 0.04   |
| Crucial   | CT2000MX500SSD1N   | 2 TB   | 1       | 14    | 0     | 0.04   |
| SK hynix  | SH920 mSATA        | 128 GB | 2       | 108   | 17    | 0.04   |
| Intel     | SSDSCKKW128G8      | 128 GB | 2       | 14    | 0     | 0.04   |
| Samsung   | SSD 870 QVO        | 2 TB   | 1       | 14    | 0     | 0.04   |
| Micron    | MTFDDAK256MAY-1... | 256 GB | 1       | 238   | 16    | 0.04   |
| Micron    | MTFDDAK240TCB      | 240 GB | 1       | 14    | 0     | 0.04   |
| Kingston  | RBUSNS8180DS3256GH | 256 GB | 1       | 41    | 2     | 0.04   |
| SMI       | SSD DISK           | 128 GB | 1       | 13    | 0     | 0.04   |
| SanDisk   | SDSSDH3 4T00       | 4 TB   | 2       | 13    | 0     | 0.04   |
| Smartbuy  | m.2 S11-2280       | 256 GB | 1       | 13    | 0     | 0.04   |
| OCZ       | VECTOR180          | 960 GB | 1       | 13    | 0     | 0.04   |
| Drevo     | X1 SSD             | 120 GB | 3       | 274   | 23    | 0.04   |
| Lite-On   | LJH-256V2G-11 M... | 256 GB | 1       | 13    | 0     | 0.04   |
| FORESEE   | 64GB SSD           | 64 GB  | 2       | 13    | 0     | 0.04   |
| Plextor   | PX-128M6S+         | 128 GB | 1       | 13    | 0     | 0.04   |
| Team      | T253X1480G         | 480 GB | 1       | 13    | 0     | 0.04   |
| Transcend | TS128GMTS600       | 128 GB | 1       | 13    | 0     | 0.04   |
| FORESEE   | S50AF512GB         | 512 GB | 1       | 13    | 0     | 0.04   |
| TCSUNBOW  | X3                 | 120 GB | 1       | 13    | 0     | 0.04   |
| XrayDisk  | SSD                | 120 GB | 1       | 12    | 0     | 0.04   |
| Samsung   | MZ7LH240HAHQ-00005 | 240 GB | 2       | 12    | 0     | 0.03   |
| Zheino    | CHN 25SATA01M 030  | 32 GB  | 1       | 12    | 0     | 0.03   |
| Super ... | FTM28N325H         | 128 GB | 1       | 12    | 0     | 0.03   |
| Intel     | SSDSCKKF256H6 SATA | 256 GB | 2       | 58    | 13    | 0.03   |
| SanDisk   | SDSSDH3 512G       | 512 GB | 1       | 12    | 0     | 0.03   |
| Wicgtyp   | M900-128           | 128 GB | 1       | 12    | 0     | 0.03   |
| Transcend | TS128GSSD360S      | 128 GB | 8       | 12    | 0     | 0.03   |
| Samsung   | MZ7PA128HMCD-010H1 | 128 GB | 1       | 12    | 0     | 0.03   |
| Transcend | TS512GMTS430S      | 512 GB | 7       | 12    | 0     | 0.03   |
| China     | SSD                | 480 GB | 6       | 12    | 0     | 0.03   |
| SanDisk   | SD9SN8W512G1122    | 512 GB | 1       | 12    | 0     | 0.03   |
| SanDisk   | SD8SNAT256G1002    | 256 GB | 3       | 11    | 0     | 0.03   |
| China     | SATA SSD           | 512 GB | 1       | 11    | 0     | 0.03   |
| PNY       | SSD2SC120G1SA75... | 120 GB | 1       | 11    | 0     | 0.03   |
| Lexar     | 128GB SSD          | 128 GB | 3       | 11    | 0     | 0.03   |
| Transcend | TSKU60SSD420       | 64 GB  | 1       | 11    | 0     | 0.03   |
| Crucial   | V4-CT128V4SSD2     | 128 GB | 1       | 11    | 0     | 0.03   |
| Faspeed   | M3-360G            | 360 GB | 1       | 11    | 0     | 0.03   |
| Crucial   | CT480BX200SSD1     | 480 GB | 2       | 11    | 0     | 0.03   |
| Intel     | SSDSA2CW300G3      | 304 GB | 2       | 11    | 0     | 0.03   |
| Micron    | M600_MTFDDAV512MBF | 512 GB | 1       | 11    | 0     | 0.03   |
| SUNEAST   | SSD SE800          | 256 GB | 1       | 11    | 0     | 0.03   |
| Samsung   | SSD 870 QVO        | 1 TB   | 3       | 10    | 0     | 0.03   |
| ADATA     | SSD S511           | 240 GB | 1       | 10    | 0     | 0.03   |
| Transcend | TS32GSSD25S-M      | 32 GB  | 1       | 10    | 0     | 0.03   |
| Intel     | SSDSCKKW240H6      | 240 GB | 3       | 18    | 1     | 0.03   |
| Golden... | GDSA25-120MS       | 120 GB | 1       | 10    | 0     | 0.03   |
| SanDisk   | SD8SBAT-256G-1006  | 256 GB | 1       | 10    | 0     | 0.03   |
| SanDisk   | SDSSDH3 2T00       | 2 TB   | 2       | 10    | 0     | 0.03   |
| ADATA     | SX300              | 128 GB | 1       | 10    | 0     | 0.03   |
| SPCC      | SPCCSolidStateDisk | 512 GB | 1       | 10    | 0     | 0.03   |
| Mushkin   | MKNSSDTR240GB      | 240 GB | 1       | 10    | 0     | 0.03   |
| KingSpec  | ACSC2M256S25       | 256 GB | 1       | 10    | 0     | 0.03   |
| Netac     | SSD                | 256 GB | 4       | 10    | 0     | 0.03   |
| Maxtor    | Z1 SSD             | 480 GB | 1       | 10    | 0     | 0.03   |
| BIWIN     | SSD                | 512 GB | 3       | 9     | 0     | 0.03   |
| Lite-On   | CV1-8B512-HP       | 512 GB | 2       | 9     | 0     | 0.03   |
| SPCC      | SSD162             | 240 GB | 1       | 203   | 20    | 0.03   |
| QUMO      | SSD                | 120 GB | 3       | 202   | 339   | 0.03   |
| Ramsta    | SSD R800           | 120 GB | 1       | 9     | 0     | 0.03   |
| Corsair   | Neutron GTX SSD    | 120 GB | 2       | 1417  | 147   | 0.03   |
| KingSpec  | NT-1TB             | 1 TB   | 2       | 9     | 0     | 0.03   |
| Kingston  | SKC600256G         | 256 GB | 5       | 9     | 0     | 0.03   |
| Apple     | SSD TS128E         | 121 GB | 3       | 84    | 63    | 0.03   |
| KingSpec  | P3-64              | 64 GB  | 2       | 9     | 0     | 0.03   |
| Faspeed   | H5-120G PLUS       | 120 GB | 1       | 9     | 0     | 0.03   |
| HP        | SSD S600           | 120 GB | 1       | 9     | 0     | 0.03   |
| KingSpec  | ACSC2M064mSA       | 64 GB  | 1       | 9     | 0     | 0.03   |
| ADATA     | SU900              | 128 GB | 1       | 9     | 0     | 0.02   |
| Kingston  | v300 240G          | 240 GB | 1       | 9     | 0     | 0.02   |
| Intel     | SSDMCEAW180A4      | 180 GB | 1       | 9     | 0     | 0.02   |
| SanDisk   | SSD P4             | 32 GB  | 13      | 109   | 254   | 0.02   |
| SanDisk   | SD8SMAT-128G-1006  | 128 GB | 1       | 9     | 0     | 0.02   |
| Londisk   | SSD                | 240 GB | 1       | 8     | 0     | 0.02   |
| Micron    | MTFDDAK128MAY-1... | 128 GB | 1       | 151   | 16    | 0.02   |
| Teclast   | 128GB MS550        | 128 GB | 1       | 8     | 0     | 0.02   |
| Kingston  | SKC6001024G        | 1 TB   | 2       | 8     | 0     | 0.02   |
| SanDisk   | iSSD P4            | 16 GB  | 1       | 238   | 26    | 0.02   |
| KingDian  | N400 60G           | 64 GB  | 1       | 8     | 0     | 0.02   |
| SanDisk   | SD7SN6S-128G-1006  | 128 GB | 1       | 8     | 0     | 0.02   |
| KingSpec  | ACSC4M128MSA       | 128 GB | 1       | 8     | 0     | 0.02   |
| PNY       | SSD2SC240G1CS17... | 240 GB | 1       | 8     | 0     | 0.02   |
| Londisk   | SSD                | 480 GB | 1       | 8     | 0     | 0.02   |
| Seagate   | BarraCuda 120 S... | 1 TB   | 1       | 8     | 0     | 0.02   |
| Kingston  | RBU-SNS8100S312... | 128 GB | 2       | 8     | 0     | 0.02   |
| KingSpec  | P3-256             | 256 GB | 4       | 8     | 0     | 0.02   |
| Plextor   | PX-512M6S          | 512 GB | 1       | 8     | 0     | 0.02   |
| Mushkin   | MKNSSDRW1TB        | 1 TB   | 1       | 8     | 0     | 0.02   |
| Samsung   | MZ7LH128HBHQ-000L1 | 128 GB | 2       | 7     | 0     | 0.02   |
| PNY       | SSD2SC256GM1P3D... | 256 GB | 1       | 7     | 0     | 0.02   |
| SanDisk   | SD8SNAT256G1122    | 256 GB | 2       | 7     | 0     | 0.02   |
| FASTDISK  | SSD 120G           | 120 GB | 1       | 7     | 0     | 0.02   |
| Intel     | SSDSC2BF180A5H SED | 180 GB | 3       | 290   | 47    | 0.02   |
| SanDisk   | SD8SBAT256G1122    | 256 GB | 4       | 7     | 0     | 0.02   |
| T-FORCE   | SSD                | 250 GB | 1       | 7     | 0     | 0.02   |
| Transcend | TS64GSSD370        | 64 GB  | 2       | 7     | 0     | 0.02   |
| China     | SSD60G             | 64 GB  | 2       | 7     | 0     | 0.02   |
| KingFast  | SSD                | 120 GB | 5       | 18    | 614   | 0.02   |
| Apacer    | AST280             | 240 GB | 1       | 7     | 0     | 0.02   |
| SanDisk   | SD8SBAT256G1002    | 256 GB | 1       | 7     | 0     | 0.02   |
| SanDisk   | SD8SNAT128G1002    | 128 GB | 3       | 7     | 0     | 0.02   |
| Zheino    | CHN 25SATA01M 060  | 64 GB  | 1       | 7     | 0     | 0.02   |
| KingSpec  | T-60               | 64 GB  | 3       | 7     | 0     | 0.02   |
| China     | SSD128GBS800       | 128 GB | 1       | 7     | 0     | 0.02   |
| KingSpec  | ACSC2M128mSA       | 128 GB | 1       | 7     | 0     | 0.02   |
| Toshiba   | THNSNS128GMCP      | 128 GB | 1       | 7     | 0     | 0.02   |
| SanDisk   | SD9SN8W128G1122    | 128 GB | 1       | 7     | 0     | 0.02   |
| FASTDISK  | SSD 30G            | 32 GB  | 1       | 7     | 0     | 0.02   |
| Kingston  | HyperX Fury 3D     | 120 GB | 2       | 7     | 0     | 0.02   |
| SK hynix  | SC401 SATA         | 256 GB | 2       | 7     | 0     | 0.02   |
| Dell      | WR202KD032G E70... | 32 GB  | 2       | 6     | 0     | 0.02   |
| BHT       | WR202I0064G E70... | 64 GB  | 2       | 6     | 0     | 0.02   |
| Kingston  | SV300S37A 120G     | 120 GB | 1       | 6     | 0     | 0.02   |
| Kingston  | RBUSC180DS37128GJ  | 128 GB | 2       | 6     | 0     | 0.02   |
| Phison    | SSBP064GTB3C0-S11  | 64 GB  | 1       | 6     | 0     | 0.02   |
| Mushkin   | MKNSSDE3480GB      | 480 GB | 1       | 6     | 0     | 0.02   |
| Intel     | SSDSCKJW180H6      | 180 GB | 1       | 6     | 0     | 0.02   |
| Patriot   | Ignite             | 240 GB | 1       | 6     | 0     | 0.02   |
| Seagate   | BarraCuda 120 S... | 250 GB | 2       | 6     | 0     | 0.02   |
| Kingston  | SA400S37 240G      | 240 GB | 1       | 6     | 0     | 0.02   |
| Samsung   | SSD PM871b 2.5 7mm | 128 GB | 1       | 6     | 0     | 0.02   |
| Kingston  | SM2280S3G2480G     | 480 GB | 2       | 149   | 63    | 0.02   |
| ADATA     | SX850              | 256 GB | 1       | 6     | 0     | 0.02   |
| Lite-On   | CV5-8Q512-HP       | 512 GB | 1       | 6     | 0     | 0.02   |
| SK hynix  | SC210 mSATA        | 256 GB | 2       | 195   | 28    | 0.02   |
| Goodram   | SSDPR_CX300_120    | 120 GB | 1       | 6     | 0     | 0.02   |
| China     | SSD 128G           | 128 GB | 2       | 6     | 0     | 0.02   |
| KingSpec  | KSQ120             | 120 GB | 1       | 6     | 0     | 0.02   |
| Smartbuy  | SSD                | 240 GB | 1       | 6     | 0     | 0.02   |
| Teclast   | 256GB NS550-2242   | 256 GB | 2       | 6     | 0     | 0.02   |
| SanDisk   | SD8SNAT-256G-1006  | 256 GB | 3       | 6     | 0     | 0.02   |
| GeIL      | Zenith A3-PRO      | 240 GB | 1       | 6     | 0     | 0.02   |
| GeIL      | Zenith A3          | 120 GB | 1       | 6     | 0     | 0.02   |
| SPCC      | 2.5" SSD           | 512 GB | 1       | 6     | 0     | 0.02   |
| Intel     | SSDSCKGW180A4      | 180 GB | 1       | 286   | 47    | 0.02   |
| China     | SATA SSD           | 960 GB | 1       | 5     | 0     | 0.02   |
| Phison    | SATA SSD           | 256 GB | 1       | 5     | 0     | 0.02   |
| Plextor   | PX-G256M6e         | 256 GB | 1       | 5     | 0     | 0.02   |
| INDMEM    | SSD mSATA          | 128 GB | 1       | 5     | 0     | 0.02   |
| BRAVEE... | SSD                | 120 GB | 1       | 5     | 0     | 0.02   |
| V-GeN     | V-GEN10SM19AR12... | 120 GB | 1       | 5     | 0     | 0.02   |
| ADATA     | SU650NS38          | 240 GB | 1       | 5     | 0     | 0.02   |
| Dell      | WR202KD128G E70... | 128 GB | 1       | 5     | 0     | 0.02   |
| SK hynix  | HFS256G39TNF-N3A0A | 256 GB | 2       | 5     | 0     | 0.02   |
| Lite-On   | LCH-256V2S-11 2... | 256 GB | 2       | 5     | 1     | 0.01   |
| MicroData | MD500 120G         | 120 GB | 1       | 5     | 0     | 0.01   |
| Teclast   | 512GB A850         | 512 GB | 1       | 5     | 0     | 0.01   |
| Mushkin   | MKNSSDCG480GB      | 480 GB | 2       | 116   | 508   | 0.01   |
| Smartbuy  | m.2 S11-2280       | 128 GB | 1       | 4     | 0     | 0.01   |
| TAMMUZ    | SSD                | 120 GB | 1       | 4     | 0     | 0.01   |
| KingSpec  | ACSC2M128S25       | 128 GB | 1       | 4     | 0     | 0.01   |
| GeIL      | ZENITH R3_120GB    | 120 GB | 2       | 4     | 0     | 0.01   |
| PNY       | SSD2SC480G1CS17... | 480 GB | 1       | 4     | 0     | 0.01   |
| SanDisk   | SD9SB8W256G1102    | 256 GB | 2       | 4     | 0     | 0.01   |
| Team      | TM4PS5128G         | 128 GB | 1       | 8     | 1     | 0.01   |
| Intel     | SSDSC2BW480H6      | 480 GB | 1       | 182   | 41    | 0.01   |
| Maximus   | SSD 256G           | 256 GB | 1       | 4     | 0     | 0.01   |
| Lite-On   | LMS-32L6M-HP       | 32 GB  | 1       | 4     | 0     | 0.01   |
| Kingston  | SA400S37           | 240 GB | 1       | 4     | 0     | 0.01   |
| Samsung   | SSD PM800 mSATA    | 64 GB  | 1       | 4     | 0     | 0.01   |
| PHINOCOM  | SSD                | 120 GB | 1       | 4     | 0     | 0.01   |
| Hikvision | HS-SSD-C100 480G   | 480 GB | 1       | 4     | 0     | 0.01   |
| INNOVA... | INNOVATION��IT     | 1 TB   | 2       | 4     | 0     | 0.01   |
| KODAK     | SSD X100           | 120 GB | 1       | 4     | 0     | 0.01   |
| Intel     | SSDMAEMC080G2H     | 80 GB  | 1       | 4     | 0     | 0.01   |
| Corsair   | Neutron GTX SSD    | 128 GB | 1       | 1173  | 291   | 0.01   |
| BIWIN     | G2242              | 64 GB  | 2       | 4     | 0     | 0.01   |
| GeIL      | ZENITH-A3 120G     | 120 GB | 1       | 3     | 0     | 0.01   |
| Zheino    | CHN-25SATAA3-360   | 360 GB | 1       | 87    | 21    | 0.01   |
| Fujitsu   | F500S              | 1 TB   | 1       | 3     | 0     | 0.01   |
| Intel     | SSDSA1M080G2LE     | 80 GB  | 1       | 121   | 31    | 0.01   |
| SanDisk   | SATAIII            | 16 GB  | 1       | 3     | 0     | 0.01   |
| Union ... | RTOTJ128VGD2EYX    | 128 GB | 2       | 3     | 0     | 0.01   |
| KingSpec  | MT-256             | 256 GB | 3       | 3     | 0     | 0.01   |
| KingDian  | S200               | 240 GB | 1       | 3     | 0     | 0.01   |
| ADATA     | IM2S3334-256GD     | 256 GB | 1       | 7     | 1     | 0.01   |
| Intel     | SSDMAEXC024G3H     | 24 GB  | 1       | 112   | 30    | 0.01   |
| HP        | SSD S700           | 1 TB   | 1       | 3     | 0     | 0.01   |
| HPE       | MK000960GWJPP      | 960 GB | 1       | 3     | 0     | 0.01   |
| OWC       | Aura SSD           | 120 GB | 1       | 3     | 0     | 0.01   |
| Lite-On   | IT L8H-64V2G       | 64 GB  | 1       | 3     | 0     | 0.01   |
| Micron    | 1300 SATA          | 256 GB | 1       | 3     | 0     | 0.01   |
| KingSpec  | NT-512             | 512 GB | 3       | 10    | 3     | 0.01   |
| Samsung   | MZNLN256HAJQ-00007 | 256 GB | 1       | 3     | 0     | 0.01   |
| OCZ       | REVODRIVE X2       | 64 GB  | 4       | 1204  | 516   | 0.01   |
| SK hynix  | HFS128G32TNF-N3A0A | 128 GB | 2       | 3     | 0     | 0.01   |
| SPCC      | SSDB27             | 32 GB  | 1       | 23    | 6     | 0.01   |
| ShineDisk | M667 128G          | 120 GB | 1       | 3     | 0     | 0.01   |
| i-Flas... | K8                 | 64 GB  | 1       | 3     | 0     | 0.01   |
| China     | SSD-512G           | 512 GB | 1       | 3     | 0     | 0.01   |
| Kingston  | SQ500S37240G       | 240 GB | 1       | 3     | 0     | 0.01   |
| China     | DEPOSM3DT-480      | 480 GB | 1       | 3     | 0     | 0.01   |
| Intel     | SSDSC2KW480H6      | 480 GB | 1       | 6     | 1     | 0.01   |
| Micron    | MTFDDAV256TBN-1... | 256 GB | 2       | 3     | 0     | 0.01   |
| Intel     | SSDSC2KB480G7      | 480 GB | 1       | 3     | 0     | 0.01   |
| SanDisk   | SD7SB3Q128G1001    | 128 GB | 1       | 302   | 100   | 0.01   |
| Foxline   | FLSSD512X5         | 512 GB | 2       | 2     | 0     | 0.01   |
| Goodram   | IR_SSDPR_S25A_120  | 120 GB | 1       | 2     | 0     | 0.01   |
| Dell      | WR202KD032G E70... | 32 GB  | 2       | 2     | 0     | 0.01   |
| SanDisk   | SD8SBAT064G1122    | 64 GB  | 1       | 2     | 0     | 0.01   |
| SanDisk   | SSD i110           | 128 GB | 1       | 2     | 0     | 0.01   |
| Fordisk   | SATA SSD           | 120 GB | 1       | 2     | 0     | 0.01   |
| Kingch... | SSD                | 64 GB  | 1       | 2     | 0     | 0.01   |
| Patriot   | Wildfire           | 120 GB | 1       | 2712  | 1022  | 0.01   |
| SanDisk   | SD7UB3Q256G1001    | 256 GB | 2       | 265   | 100   | 0.01   |
| SanDisk   | SDSA5GK-016G-1006  | 16 GB  | 1       | 276   | 106   | 0.01   |
| Kingston  | RBUSNS8180S3256GJ  | 256 GB | 1       | 2     | 0     | 0.01   |
| Foxline   | FLSSD256X5         | 256 GB | 1       | 2     | 0     | 0.01   |
| KIOXIA... | SATA SSD           | 240 GB | 1       | 2     | 0     | 0.01   |
| SanDisk   | SD8SNAT-128G-1006  | 128 GB | 3       | 2     | 0     | 0.01   |
| Gigastone | SS6200-256GB       | 256 GB | 1       | 2     | 0     | 0.01   |
| SanDisk   | SD7SB2Q512G1001    | 512 GB | 2       | 246   | 100   | 0.01   |
| Micron    | 1100_MTFDDAK1T0TBN | 1 TB   | 3       | 2     | 0     | 0.01   |
| PNY       | CS900 250GB SSD    | 250 GB | 1       | 2     | 0     | 0.01   |
| SOLIDATA  | SSD                | 120 GB | 1       | 2420  | 1019  | 0.01   |
| Micron    | 1300_MTFDDAK512TDL | 512 GB | 1       | 2     | 0     | 0.01   |
| China     | 256GB QLC SATA SSD | 256 GB | 1       | 2     | 0     | 0.01   |
| SanDisk   | SSD i110           | 16 GB  | 2       | 2     | 0     | 0.01   |
| SanDisk   | SSD i110           | 24 GB  | 1       | 2     | 0     | 0.01   |
| Transcend | TS64GMTS800        | 64 GB  | 1       | 2     | 0     | 0.01   |
| Intel     | SSDSCKKF240H6L     | 240 GB | 1       | 47    | 20    | 0.01   |
| OCZ       | VERTEX3 LP         | 240 GB | 1       | 2268  | 1019  | 0.01   |
| Intel     | SSDSC2KW240H6      | 240 GB | 4       | 10    | 234   | 0.01   |
| Netac     | SSD                | 128 GB | 3       | 2     | 0     | 0.01   |
| ACPI      | M2SCF-6M           | 64 GB  | 1       | 2     | 0     | 0.01   |
| Zheino    | CHN25SATAS1 032    | 32 GB  | 2       | 2     | 0     | 0.01   |
| SK hynix  | SH920 2.5 7MM      | 128 GB | 1       | 54    | 25    | 0.01   |
| Samsung   | MZNLH512HALU-00000 | 512 GB | 3       | 2     | 0     | 0.01   |
| Seagate   | BarraCuda SSD Z... | 2 TB   | 1       | 2     | 0     | 0.01   |
| Mushkin   | MKNSSDCL120GB      | 120 GB | 1       | 2066  | 1007  | 0.01   |
| SPCC      | M.2 SSD            | 128 GB | 1       | 2     | 0     | 0.01   |
| SanDisk   | SDSSDH120GG25      | 120 GB | 1       | 112   | 55    | 0.01   |
| Intel     | SSDSC2BB300G4R     | 304 GB | 2       | 2029  | 1029  | 0.01   |
| Transcend | TS32GMSA370        | 32 GB  | 1       | 1     | 0     | 0.01   |
| Kingston  | SKC300S37A240G     | 240 GB | 2       | 1     | 0     | 0.01   |
| Fujitsu   | F500S 128G         | 128 GB | 1       | 1     | 0     | 0.01   |
| Hikvision | HS-SSD-C160 256G   | 256 GB | 1       | 1     | 0     | 0.01   |
| KingSpec  | P3D-240            | 240 GB | 1       | 1     | 0     | 0.01   |
| Samsung   | MZNLN256HAJQ-000H7 | 256 GB | 1       | 1     | 0     | 0.01   |
| FASTDISK  | SSD                | 64 GB  | 1       | 1     | 0     | 0.00   |
| Yunhai... | Y6-240G            | 240 GB | 1       | 1     | 0     | 0.00   |
| China     | S41CF256G          | 256 GB | 1       | 1     | 0     | 0.00   |
| Drevo     | X1 pro             | 1 TB   | 1       | 33    | 18    | 0.00   |
| OCZ       | VERTEX2            | 100 GB | 1       | 1     | 0     | 0.00   |
| SanDisk   | SDSSDH3256G        | 256 GB | 1       | 1     | 0     | 0.00   |
| Toshiba   | THNSNK256GVN8 M... | 256 GB | 3       | 169   | 100   | 0.00   |
| Intel     | SSDSCKKW010X6      | 1 TB   | 1       | 1     | 0     | 0.00   |
| KingSpec  | ACJC2M064S25       | 64 GB  | 1       | 1     | 0     | 0.00   |
| LDLC      | F7+240GB           | 240 GB | 1       | 1     | 0     | 0.00   |
| Micron    | C400-MTFDDAT064MAM | 64 GB  | 1       | 1     | 0     | 0.00   |
| Micron    | 5300_MTFDDAK240TDS | 240 GB | 2       | 1     | 0     | 0.00   |
| TCSUNBOW  | X1                 | 16 GB  | 1       | 1     | 0     | 0.00   |
| addlink   | SATA SSD           | 256 GB | 1       | 1     | 0     | 0.00   |
| Intel     | SSDSC2BA400G3T     | 400 GB | 1       | 1671  | 1029  | 0.00   |
| SK hynix  | HFS128G38MNB-2200A | 128 GB | 3       | 228   | 133   | 0.00   |
| Intel     | SSDSC2BX400G4R     | 400 GB | 2       | 1654  | 1028  | 0.00   |
| China     | SSD 256G           | 256 GB | 1       | 1     | 0     | 0.00   |
| SanDisk   | SD8SB8U128G1001    | 128 GB | 1       | 1     | 0     | 0.00   |
| acpi      | MSS4FV-MP mSATA... | 128 GB | 1       | 1     | 0     | 0.00   |
| Apacer    | 16GB SATA Flash... | 16 GB  | 3       | 22    | 20    | 0.00   |
| Goodram   | SSDPR-CL100-120    | 120 GB | 1       | 1     | 0     | 0.00   |
| ADATA     | SSD DP900 512GB... | 512 GB | 2       | 1465  | 1016  | 0.00   |
| BHT       | WR202I0032G E70... | 32 GB  | 1       | 1     | 0     | 0.00   |
| Plextor   | PX-512M6M          | 512 GB | 1       | 1     | 0     | 0.00   |
| S3+       | S3SSDC480XEU       | 480 GB | 1       | 1     | 0     | 0.00   |
| Toshiba   | THNSNK256GCS8 SATA | 256 GB | 1       | 138   | 100   | 0.00   |
| Patriot   | Pyro m3            | 240 GB | 1       | 1378  | 1015  | 0.00   |
| ADATA     | AXM14S3-128GM-B    | 128 GB | 1       | 1363  | 1018  | 0.00   |
| ADATA     | IMSS316-256GD      | 256 GB | 1       | 1     | 0     | 0.00   |
| WDC       | WDS250G2B0B        | 250 GB | 2       | 1     | 0     | 0.00   |
| ASENNO    | AS25               | 120 GB | 1       | 1     | 0     | 0.00   |
| OEM       | Genuine            | 1 TB   | 1       | 1     | 0     | 0.00   |
| Patriot   | Solid              | 240 GB | 2       | 1     | 0     | 0.00   |
| Team      | TM8PS7001T         | 1 TB   | 1       | 1     | 0     | 0.00   |
| Micron    | P300-MTFDBAC050SAL | 50 GB  | 1       | 1411  | 1140  | 0.00   |
| Toshiba   | THNSNK128GVN8 M... | 128 GB | 2       | 124   | 100   | 0.00   |
| Team      | M8PS5 SSD          | 128 GB | 1       | 1     | 0     | 0.00   |
| Corsair   | CSSD-F40GB2        | 40 GB  | 1       | 718   | 600   | 0.00   |
| KingSpec  | ACJC2M128S25       | 128 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | MZNLN128HAHQ-000L2 | 128 GB | 2       | 1     | 0     | 0.00   |
| Intel     | SSDSC2BA200G4R     | 200 GB | 2       | 1037  | 1028  | 0.00   |
| Teclast   | 240GB A800         | 240 GB | 1       | 1     | 0     | 0.00   |
| Foxline   | FLSSD60X3          | 64 GB  | 1       | 993   | 1016  | 0.00   |
| SanDisk   | SSD P4             | 64 GB  | 1       | 14    | 14    | 0.00   |
| Toshiba   | KSG60ZSE512G SATA  | 512 GB | 2       | 97    | 100   | 0.00   |
| SPCC      | SSD                | 32 GB  | 1       | 998   | 1036  | 0.00   |
| Crucial   | CT480M500SSD3      | 480 GB | 2       | 1290  | 1480  | 0.00   |
| ADATA     | SP900NS38          | 256 GB | 1       | 942   | 1023  | 0.00   |
| Kingch... | SSD                | 480 GB | 1       | 0     | 0     | 0.00   |
| China     | ESA3SMN2ISN1BQ4... | 480 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | SH920 2.5 7MM      | 512 GB | 1       | 13    | 14    | 0.00   |
| ORTIAL    | SSD                | 256 GB | 3       | 0     | 0     | 0.00   |
| Intenso   | SSD Sata III       | 128 GB | 2       | 0     | 0     | 0.00   |
| SanDisk   | SD6SB1M256G1022I   | 256 GB | 1       | 400   | 474   | 0.00   |
| FORESEE   | 32GB SSD           | 32 GB  | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSC2KW180H6      | 180 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | HFS060G32MNM-1010U | 64 GB  | 1       | 822   | 1016  | 0.00   |
| Eluktro   | TRO-SSD7-500GB-PRO | 500 GB | 1       | 806   | 1016  | 0.00   |
| Plextor   | PX-128M6MV         | 128 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | RBUSNS8180DS3256GJ | 256 GB | 2       | 0     | 0     | 0.00   |
| Micron    | M600_MTFDDAT128MBF | 128 GB | 1       | 0     | 0     | 0.00   |
| BAITITON  | BT58SSD11S         | 480 GB | 1       | 0     | 0     | 0.00   |
| KingSpec  | MT-64              | 64 GB  | 1       | 0     | 0     | 0.00   |
| SanDisk   | SD8TN8U512G1001    | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | SC210 2.5 7MM      | 256 GB | 2       | 556   | 856   | 0.00   |
| Lite-On   | E200-160           | 160 GB | 1       | 12    | 18    | 0.00   |
| KingSpec  | ACSC2M064S25       | 64 GB  | 1       | 0     | 0     | 0.00   |
| Micron    | 5300_MTFDDAK480TDS | 480 GB | 2       | 0     | 0     | 0.00   |
| Intel     | SSDSCMMW120A3L     | 120 GB | 1       | 649   | 1017  | 0.00   |
| Lexar     | SSD                | 256 GB | 1       | 0     | 0     | 0.00   |
| ADATA     | AXM13S2-24GM-B     | 24 GB  | 1       | 628   | 1020  | 0.00   |
| QUMO      | SSD                | 480 GB | 1       | 625   | 1015  | 0.00   |
| SanDisk   | SSD U100           | 32 GB  | 2       | 8     | 503   | 0.00   |
| SPCC      | SSD170             | 55 GB  | 3       | 619   | 1016  | 0.00   |
| Indilinx  | InM2246S3-128G     | 128 GB | 2       | 0     | 0     | 0.00   |
| Intel     | SSDSC2KW256G8L     | 256 GB | 1       | 0     | 0     | 0.00   |
| Intenso   | SSD Sata III       | 247 GB | 1       | 18    | 32    | 0.00   |
| Smartbuy  | SSD                | 480 GB | 1       | 0     | 0     | 0.00   |
| Lite-On   | LAT-256M3S         | 256 GB | 1       | 1074  | 2017  | 0.00   |
| ADATA     | SU635              | 480 GB | 1       | 106   | 206   | 0.00   |
| Intel     | SSDMCEAW080A4 m... | 80 GB  | 2       | 515   | 1008  | 0.00   |
| DOGFISH   | SSD                | 512 GB | 1       | 0     | 0     | 0.00   |
| Dogfish   | SSD                | 512 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | RBU-SNS8350DES3... | 128 GB | 1       | 42    | 97    | 0.00   |
| ADATA     | XM11 128GB-V2      | 128 GB | 1       | 449   | 1048  | 0.00   |
| Gost      | SSD120             | 120 GB | 1       | 0     | 0     | 0.00   |
| SMI       | B17A               | 240 GB | 1       | 0     | 0     | 0.00   |
| Zheino    | CHN 25SATAA3 120   | 120 GB | 2       | 0     | 0     | 0.00   |
| PNY       | SSD2SC120G3LC70... | 120 GB | 1       | 393   | 1015  | 0.00   |
| Kingston  | SHPM2280P2H-240G   | 240 GB | 3       | 218   | 540   | 0.00   |
| China     | T60                | 64 GB  | 2       | 0     | 0     | 0.00   |
| Reeinno   | ST960GB S7S3       | 960 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | SH103S3240G-NV     | 240 GB | 1       | 377   | 1018  | 0.00   |
| PNY       | SSD2SC120GE2DA0... | 120 GB | 1       | 373   | 1018  | 0.00   |
| SPCC      | SSD170             | 64 GB  | 1       | 358   | 1016  | 0.00   |
| Mushkin   | MKNSSDCL120GB-DX   | 120 GB | 1       | 348   | 1006  | 0.00   |
| Lite-On   | CS1-SP32-11 M.2... | 32 GB  | 1       | 1     | 4     | 0.00   |
| Mushkin   | MKNSSDCL480GB-DX   | 480 GB | 1       | 347   | 1020  | 0.00   |
| Samsung   | Portable SSD T5    | 250 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TS8GHSD630         | 8 GB   | 1       | 679   | 2050  | 0.00   |
| Kingston  | SVP200S37A256G     | 256 GB | 1       | 311   | 1017  | 0.00   |
| China     | ESA3ASA2ISN1BQ4... | 480 GB | 1       | 0     | 0     | 0.00   |
| China     | SATA SSD           | 256 GB | 1       | 0     | 0     | 0.00   |
| FASTDISK  | SSD 32G            | 32 GB  | 1       | 0     | 0     | 0.00   |
| GLOWAY    | STK120GS3-S7       | 120 GB | 1       | 0     | 0     | 0.00   |
| Leven     | JAJS300M120C       | 120 GB | 1       | 0     | 0     | 0.00   |
| Lite-On   | CV1-8B512          | 512 GB | 1       | 0     | 0     | 0.00   |
| Patriot   | Torch LE           | 120 GB | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSCKKF256G8H     | 256 GB | 3       | 28    | 99    | 0.00   |
| SK hynix  | HFS256G3AMNB-2200A | 256 GB | 1       | 283   | 1006  | 0.00   |
| SanDisk   | SD8SBAT-032G-1006  | 32 GB  | 4       | 0     | 0     | 0.00   |
| KingSpec  | Q-90               | 90 GB  | 1       | 134   | 520   | 0.00   |
| Lite-On   | LMT-256M6M-HP      | 256 GB | 1       | 39    | 152   | 0.00   |
| GLOWAY    | VAL64GM3-mSATA     | 64 GB  | 1       | 0     | 0     | 0.00   |
| ShanDi... | SSD                | 512 GB | 1       | 0     | 0     | 0.00   |
| TEUTONS   | SSD                | 256 GB | 1       | 0     | 0     | 0.00   |
| GeIL      | ZENITH S3-120GB    | 120 GB | 1       | 245   | 1021  | 0.00   |
| Samsung   | SSD PM810 TM       | 128 GB | 1       | 239   | 1033  | 0.00   |
| Intel     | SSDSCKKF256H6L     | 256 GB | 1       | 13    | 57    | 0.00   |
| Myung     | G3 Series          | 120 GB | 1       | 228   | 1015  | 0.00   |
| Goldenfir | T650-120G          | 128 GB | 1       | 0     | 0     | 0.00   |
| Lite-On   | S960 256           | 256 GB | 1       | 0     | 0     | 0.00   |
| Zheino    | CHN25SATAS1 064    | 64 GB  | 1       | 0     | 0     | 0.00   |
| SK hynix  | HFS256G38MNB-2200A | 256 GB | 1       | 207   | 1007  | 0.00   |
| China     | ESA3SMD2HTGT240GB  | 240 GB | 1       | 51    | 273   | 0.00   |
| SK hynix  | HFS512G39TND-N210A | 512 GB | 1       | 371   | 2017  | 0.00   |
| Patriot   | Pyro SE            | 240 GB | 1       | 180   | 1016  | 0.00   |
| China     | SATA3 128GB SSD    | 128 GB | 1       | 0     | 0     | 0.00   |
| China     | T120               | 120 GB | 1       | 0     | 0     | 0.00   |
| Faspeed   | H5-30G             | 32 GB  | 1       | 0     | 0     | 0.00   |
| Fujitsu   | F500s 240G         | 240 GB | 1       | 0     | 0     | 0.00   |
| Kingmax   | SSD                | 480 GB | 1       | 0     | 0     | 0.00   |
| LDLC      | SSD F6 PLUS M.2... | 960 GB | 1       | 0     | 0     | 0.00   |
| Patriot   | P210               | 512 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | CF Card            | 16 GB  | 1       | 0     | 0     | 0.00   |
| Transcend | TS64GMSA230S       | 64 GB  | 1       | 0     | 0     | 0.00   |
| Kingston  | SNS4151S332G       | 32 GB  | 1       | 170   | 1022  | 0.00   |
| Toshiba   | THNSNK128GCS8 SATA | 128 GB | 1       | 16    | 100   | 0.00   |
| Goldenfir | T650-120GB         | 120 GB | 1       | 4     | 28    | 0.00   |
| SK hynix  | SH910 mSATA        | 128 GB | 1       | 151   | 1026  | 0.00   |
| ADATA     | SSD DP900 128GB... | 128 GB | 1       | 147   | 1023  | 0.00   |
| Lite-On   | LCT-128M3S         | 128 GB | 1       | 132   | 1047  | 0.00   |
| Colorful  | SL500              | 480 GB | 1       | 22    | 195   | 0.00   |
| Lite-On   | LSS-16L6G-HP       | 16 GB  | 1       | 125   | 1275  | 0.00   |
| Kingston  | SMS151S324G        | 24 GB  | 1       | 95    | 1022  | 0.00   |
| AXIOMT... | FSA128GMC5T        | 128 GB | 1       | 0     | 0     | 0.00   |
| DOGFISH   | SSD                | 128 GB | 1       | 0     | 0     | 0.00   |
| Plextor   | PX-32G5L           | 32 GB  | 1       | 0     | 0     | 0.00   |
| Smartbuy  | 120GB STELS        | 128 GB | 1       | 0     | 0     | 0.00   |
| XrayDisk  | SSD                | 128 GB | 1       | 0     | 0     | 0.00   |
| PNY       | SSD2SC240GC2DH1... | 240 GB | 1       | 85    | 1023  | 0.00   |
| Intel     | SSDSC2KF512H6 SATA | 512 GB | 1       | 7     | 84    | 0.00   |
| Micron    | MTFDDAT064MAM-1J2  | 64 GB  | 1       | 85    | 1039  | 0.00   |
| PNY       | SSD2SC240G1SA75... | 240 GB | 1       | 7     | 88    | 0.00   |
| ADATA     | XM11 128GB-V3      | 128 GB | 1       | 77    | 1016  | 0.00   |
| ADATA     | AXM21S3-24GM-B     | 24 GB  | 1       | 77    | 1020  | 0.00   |
| Transcend | TS64GSSD340K       | 64 GB  | 1       | 74    | 1008  | 0.00   |
| Mushkin   | MKNSSDCR120GB-DX7  | 120 GB | 1       | 73    | 1016  | 0.00   |
| SanDisk   | SDSSDX480GG25      | 480 GB | 1       | 76    | 1090  | 0.00   |
| SandForce | 906190             | 64 GB  | 1       | 65    | 1018  | 0.00   |
| PNY       | SSD2SC120G3LC72... | 120 GB | 1       | 65    | 1019  | 0.00   |
| ADATA     | SP900NS38          | 512 GB | 1       | 64    | 1020  | 0.00   |
| MicroData | MD300 128G         | 128 GB | 1       | 41    | 666   | 0.00   |
| Foxline   | FLSSD128X5         | 128 GB | 2       | 0     | 0     | 0.00   |
| Kingston  | SNS4151S316GD      | 16 GB  | 1       | 51    | 1022  | 0.00   |
| SanDisk   | SD9SN8W-128G-1006  | 128 GB | 17      | 47    | 994   | 0.00   |
| SanDisk   | SD9SN8W-256G-1006  | 256 GB | 4       | 44    | 994   | 0.00   |
| Samsung   | MZMPA128HMFU-000H1 | 128 GB | 2       | 69    | 1727  | 0.00   |
| Lite-On   | LMT-128M3M         | 128 GB | 1       | 44    | 1009  | 0.00   |
| Intel     | SSDSC2BB150G7      | 150 GB | 1       | 0     | 0     | 0.00   |
| KingDian  | S180               | 120 GB | 1       | 0     | 0     | 0.00   |
| OWC       | Mercury Electra... | 500 GB | 1       | 0     | 0     | 0.00   |
| Team      | T253X1120G         | 120 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | SNS4151S316G       | 16 GB  | 1       | 39    | 1022  | 0.00   |
| ADATA     | SX300              | 64 GB  | 1       | 32    | 1020  | 0.00   |
| SanDisk   | TE22D10400GE8001   | 400 GB | 1       | 34    | 2047  | 0.00   |
| AMD       | R5S120GBSF         | 120 GB | 1       | 15    | 1016  | 0.00   |
| JIAWEI    | SSD                | 240 GB | 1       | 47    | 3057  | 0.00   |
| Intel     | SSDSC2KW360H6      | 360 GB | 2       | 16    | 1365  | 0.00   |
| Lite-On   | CV8-8E128-HP       | 128 GB | 12      | 13    | 1007  | 0.00   |
| WDC       | PC SA530 SDASN8... | 256 GB | 1       | 3     | 1000  | 0.00   |
| Samsung   | MZNLH128HBHQ-000H1 | 128 GB | 1       | 0     | 100   | 0.00   |
| Intel     | SSDSC2KG400G7M ... | 400 GB | 1       | 2     | 1025  | 0.00   |
| SanDisk   | sandisk120         | 120 GB | 1       | 0     | 21    | 0.00   |
| Micron    | MTFDDAV256TDL-1... | 256 GB | 4       | 1     | 1008  | 0.00   |
| Kingston  | EK60HYXTFY176 V100 | 64 GB  | 1       | 1     | 1130  | 0.00   |
| SMI       | SSD DISK           | 506 GB | 1       | 0     | 1957  | 0.00   |
| Mushkin   | MKNSSDCR480GB-7-A  | 480 GB | 1       | 0     | 1016  | 0.00   |
| Mushkin   | MKNSSDCR120GB-7    | 120 GB | 1       | 0     | 1023  | 0.00   |

SSD by Family
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days   — avg. days per sample,
Err    — avg. errors per sample,
MTBF   — avg. MTBF in years per sample.

| MFG       | Family                 | Models | Samples | Days  | Err   | MTBF   |
|-----------|------------------------|--------|---------|-------|-------|--------|
| Crucial   | RealSSD C300/P300      | 1      | 3       | 1525  | 336   | 3.36   |
| Micron    | MX100/MX200/M5x0/M6... | 1      | 1       | 1083  | 0     | 2.97   |
| Toshiba   | HG2 Series             | 2      | 5       | 1038  | 0     | 2.84   |
| Intel     | X18-M/X25-M G1 SSDs    | 4      | 4       | 1037  | 0     | 2.84   |
| Hyundai   | Unknown                | 1      | 1       | 997   | 0     | 2.73   |
| Intel     | 730 and DC S35x0/36... | 20     | 62      | 1155  | 117   | 2.58   |
| SanDisk   | SATA Cloudspeed Max... | 1      | 1       | 916   | 0     | 2.51   |
| HPE       | Unknown                | 3      | 3       | 831   | 0     | 2.28   |
| Crucial   | RealSSD m4/C400/P400   | 6      | 70      | 943   | 146   | 2.22   |
| Intel     | X25-E SSDs             | 1      | 1       | 795   | 0     | 2.18   |
| Toshiba   | HG3 Series             | 3      | 4       | 762   | 0     | 2.09   |
| Micro ... | Unknown                | 1      | 1       | 722   | 0     | 1.98   |
| Kingston  | JMicron/Maxiotek ba... | 1      | 1       | 674   | 0     | 1.85   |
| Crucial   | RealSSD m4/C400        | 3      | 8       | 664   | 0     | 1.82   |
| BLueRay   | Unknown                | 1      | 1       | 619   | 0     | 1.70   |
| Intel     | 520 Series SSDs        | 7      | 92      | 681   | 166   | 1.62   |
| SATADOM   | Innodisk 3IE3/3ME3/... | 1      | 1       | 574   | 0     | 1.57   |
| Apple     | Unknown                | 2      | 2       | 688   | 1     | 1.53   |
| OCZ       | SandForce Driven SSDs  | 39     | 265     | 727   | 45    | 1.50   |
| Intel     | 510 Series SSDs        | 1      | 3       | 545   | 0     | 1.49   |
| Corsair   | SandForce Driven SSDs  | 23     | 137     | 665   | 91    | 1.44   |
| MyDigi... | Unknown                | 4      | 5       | 515   | 0     | 1.41   |
| OCZ       | Indilinx Barefoot_2... | 12     | 115     | 603   | 3     | 1.41   |
| Intel     | 330/335 Series SSDs    | 6      | 43      | 668   | 1     | 1.35   |
| Toshiba   | HG6 Series SSD         | 11     | 31      | 493   | 0     | 1.35   |
| Micron    | 5100 Pro / 5200 SSDs   | 4      | 16      | 617   | 21    | 1.34   |
| Toshiba   | HG5 Series             | 1      | 2       | 471   | 0     | 1.29   |
| Innodisk  | Unknown                | 3      | 3       | 468   | 0     | 1.28   |
| Kingston  | JMicron based SSDs     | 14     | 39      | 626   | 2     | 1.25   |
| Intel     | 320 Series SSDs        | 9      | 38      | 478   | 1     | 1.25   |
| Innodisk  | 3IE3/3ME3/3ME4 SSDs    | 2      | 3       | 446   | 0     | 1.22   |
| Micron    | RealSSD m4/C400        | 2      | 3       | 433   | 0     | 1.19   |
| Toshiba   | JMicron based SSDs     | 1      | 1       | 427   | 0     | 1.17   |
| Samsung   | Samsung based SSDs     | 226    | 2606    | 408   | 7     | 1.09   |
| Transcend | JMicron based SSDs     | 5      | 13      | 403   | 78    | 1.06   |
| Apple     | SD/SM/TS E/F/G SSDs    | 11     | 41      | 384   | 0     | 1.05   |
| Corsair   | Indilinx Barefoot b... | 3      | 4       | 465   | 1     | 1.03   |
| KingShare | Unknown                | 1      | 1       | 358   | 0     | 0.98   |
| Apple     | JMicron based SSDs     | 3      | 8       | 358   | 0     | 0.98   |
| ZTC       | Unknown                | 1      | 1       | 357   | 0     | 0.98   |
| WDC       | Unknown                | 3      | 3       | 350   | 334   | 0.96   |
| Advantech | Unknown                | 1      | 1       | 345   | 0     | 0.95   |
| Crucial   | RealSSD C300/M500      | 4      | 23      | 506   | 108   | 0.94   |
| Goodram   | Phison Driven OEM SSDs | 2      | 8       | 339   | 0     | 0.93   |
| ADATA     | JMicron based SSDs     | 5      | 27      | 336   | 1     | 0.92   |
| ADATA     | SandForce Driven SSDs  | 11     | 77      | 384   | 6     | 0.90   |
| Team      | SiliconMotion based... | 1      | 4       | 325   | 0     | 0.89   |
| Phison    | Unknown                | 3      | 3       | 325   | 0     | 0.89   |
| Toshiba   | HG5d Series            | 7      | 13      | 320   | 0     | 0.88   |
| Mushkin   | SandForce Driven SSDs  | 13     | 15      | 460   | 272   | 0.84   |
| Kingston  | SandForce Driven SSDs  | 36     | 892     | 359   | 57    | 0.84   |
| Toshiba   | OCZ                    | 4      | 7       | 304   | 0     | 0.83   |
| Intel     | X18-M/X25-M/X25-V G... | 12     | 42      | 799   | 8     | 0.83   |
| OCZ       | Indilinx Barefoot 3... | 15     | 66      | 307   | 33    | 0.76   |
| Micron    | RealSSD m4/C400/P400   | 6      | 19      | 281   | 266   | 0.74   |
| Plextor   | M3/M5/M6/M7 Series ... | 6      | 14      | 269   | 0     | 0.74   |
| Kston     | Unknown                | 1      | 1       | 264   | 0     | 0.72   |
| ADATA     | JMicron/Maxiotek ba... | 1      | 3       | 247   | 0     | 0.68   |
| Intenso   | Phison Driven OEM SSDs | 3      | 24      | 257   | 1     | 0.67   |
| Intel     | 53x and Pro 1500/25... | 8      | 55      | 345   | 4     | 0.66   |
| Intel     | 530 Series SSDs        | 2      | 40      | 320   | 1     | 0.64   |
| Patriot   | Unknown                | 17     | 35      | 353   | 88    | 0.63   |
| Toshiba   | Unknown                | 43     | 109     | 245   | 10    | 0.63   |
| OCZ       | Trion SSDs             | 2      | 9       | 266   | 1     | 0.63   |
| Mushkin   | Silicon Motion base... | 2      | 3       | 229   | 0     | 0.63   |
| SanDisk   | Marvell based SanDi... | 59     | 458     | 253   | 21    | 0.63   |
| Verbatim  | Unknown                | 5      | 5       | 229   | 0     | 0.63   |
| SanDisk   | SanDisk based SSDs     | 28     | 174     | 258   | 26    | 0.61   |
| Crucial   | BX/MX1/2/3/500, M5/... | 33     | 458     | 280   | 37    | 0.60   |
| OCZ       | Indilinx Barefoot b... | 4      | 7       | 329   | 1     | 0.60   |
| PNY       | Phison Driven SSDs     | 8      | 62      | 218   | 0     | 0.60   |
| Kingston  | SSDNow UV400           | 3      | 168     | 240   | 44    | 0.60   |
| Toshiba   | OCZ/Toshiba Trion SSDs | 5      | 25      | 260   | 1     | 0.59   |
| Crucial   | MX1/2/300, M5/600, ... | 2      | 10      | 405   | 8     | 0.58   |
| Micron    | BX/MX1/2/3/500, M5/... | 5      | 13      | 234   | 2     | 0.56   |
| Ramaxel   | Unknown                | 2      | 3       | 204   | 0     | 0.56   |
| V-Gen     | Unknown                | 1      | 1       | 200   | 0     | 0.55   |
| Pioneer   | Unknown                | 2      | 5       | 194   | 0     | 0.53   |
| Intel     | 525 Series SSDs        | 2      | 3       | 193   | 0     | 0.53   |
| Seagate   | Unknown                | 12     | 29      | 345   | 142   | 0.53   |
| Team      | Silicon Motion base... | 2      | 3       | 191   | 0     | 0.52   |
| Golden... | Unknown                | 1      | 1       | 190   | 0     | 0.52   |
| Smartbuy  | Phison Driven SSDs     | 3      | 105     | 200   | 1     | 0.51   |
| Samsung   | Unknown                | 26     | 145     | 190   | 1     | 0.50   |
| Phison    | Driven OEM SSDs        | 8      | 37      | 175   | 0     | 0.48   |
| SK hynix  | SATA SSDs              | 23     | 128     | 218   | 43    | 0.48   |
| Corsair   | Unknown                | 18     | 34      | 392   | 60    | 0.48   |
| Plextor   | M3/M5 (Pro) Series ... | 5      | 15      | 240   | 70    | 0.46   |
| Intel     | Unknown                | 37     | 69      | 224   | 86    | 0.45   |
| SanDisk   | SandForce Driven SSDs  | 6      | 163     | 180   | 15    | 0.45   |
| SanDisk   | Unknown                | 108    | 275     | 172   | 100   | 0.44   |
| Smartbuy  | Unknown                | 12     | 20      | 158   | 0     | 0.44   |
| Zheino    | Silicon Motion base... | 1      | 2       | 158   | 0     | 0.43   |
| Kingston  | Unknown                | 63     | 128     | 184   | 64    | 0.43   |
| SPCC      | Unknown                | 21     | 51      | 349   | 300   | 0.43   |
| Transcend | SandForce Driven SSDs  | 5      | 7       | 155   | 0     | 0.43   |
| Goodram   | Unknown                | 17     | 43      | 162   | 1     | 0.42   |
| KingFast  | Unknown                | 8      | 29      | 152   | 106   | 0.41   |
| Palit     | Unknown                | 3      | 4       | 150   | 0     | 0.41   |
| OCZ       | OCZ/Toshiba Trion SSDs | 2      | 9       | 162   | 1     | 0.41   |
| PHISON    | Unknown                | 3      | 3       | 169   | 1     | 0.41   |
| Micron    | BX/MX1/2/3/500, M5/... | 14     | 106     | 186   | 72    | 0.40   |
| SPCC      | Phison Driven OEM SSDs | 7      | 290     | 174   | 92    | 0.40   |
| Intel     | 53x and Pro 2500 Se... | 6      | 6       | 145   | 0     | 0.40   |
| HP        | Unknown                | 10     | 23      | 144   | 0     | 0.40   |
| Goodram   | Phison Driven SSDs     | 5      | 52      | 142   | 0     | 0.39   |
| Intel     | 730 and DC S3500/S3... | 2      | 2       | 139   | 0     | 0.38   |
| UNIC2     | Unknown                | 1      | 1       | 139   | 0     | 0.38   |
| MENGMI    | Unknown                | 1      | 1       | 139   | 0     | 0.38   |
| WDC       | Blue / Red / Green ... | 6      | 16      | 138   | 0     | 0.38   |
| OCZ       | Unknown                | 7      | 10      | 361   | 102   | 0.37   |
| Micron    | Unknown                | 25     | 53      | 220   | 159   | 0.37   |
| ZOTAC     | Unknown                | 2      | 3       | 132   | 0     | 0.36   |
| KLEVV     | Unknown                | 1      | 1       | 127   | 0     | 0.35   |
| Chiprex   | Unknown                | 1      | 1       | 126   | 0     | 0.35   |
| PNY       | Unknown                | 21     | 29      | 158   | 144   | 0.35   |
| BLUERAY   | Unknown                | 1      | 1       | 125   | 0     | 0.34   |
| Hypertec  | Unknown                | 1      | 2       | 371   | 512   | 0.33   |
| WDC       | Blue and Green SSDs    | 30     | 549     | 123   | 1     | 0.33   |
| Kingston  | Phison Driven SSDs     | 15     | 820     | 128   | 1     | 0.33   |
| Plextor   | Unknown                | 26     | 66      | 127   | 1     | 0.33   |
| Hoodisk   | Unknown                | 2      | 2       | 118   | 0     | 0.32   |
| Plextor   | M3/M5/M6 Series SSDs   | 14     | 170     | 127   | 20    | 0.32   |
| Crucial   | MX100/MX200/M5x0/M6... | 1      | 1       | 116   | 0     | 0.32   |
| Intel     | S4510/S4610/S4500/S... | 9      | 20      | 116   | 0     | 0.32   |
| Samsung   | SandForce Driven SSDs  | 1      | 1       | 115   | 0     | 0.32   |
| BIOSTAR   | Unknown                | 2      | 2       | 109   | 0     | 0.30   |
| Mushkin   | Unknown                | 9      | 10      | 334   | 304   | 0.29   |
| Kingston  | SSDNow UV400/500       | 7      | 56      | 112   | 63    | 0.29   |
| Seagate   | Nytro SATA SSD         | 1      | 4       | 104   | 0     | 0.29   |
| Transcend | Indilinx Barefoot b... | 1      | 1       | 309   | 2     | 0.28   |
| Team      | Unknown                | 25     | 46      | 106   | 1     | 0.28   |
| Phison    | Phison Driven SSDs     | 1      | 1       | 101   | 0     | 0.28   |
| KingDian  | Unknown                | 11     | 34      | 106   | 90    | 0.28   |
| ORICO     | Unknown                | 1      | 1       | 99    | 0     | 0.27   |
| ADATA     | Unknown                | 56     | 222     | 180   | 137   | 0.27   |
| GALAX     | Unknown                | 2      | 3       | 98    | 0     | 0.27   |
| Anobit    | Unknown                | 1      | 1       | 96    | 0     | 0.27   |
| Patriot   | Phison Driven SSDs     | 6      | 75      | 97    | 1     | 0.26   |
| Crucial   | MX500 SSDs             | 7      | 258     | 92    | 1     | 0.25   |
| Vaseky    | Unknown                | 5      | 6       | 90    | 0     | 0.25   |
| ADATA     | Silicon Motion base... | 9      | 85      | 97    | 2     | 0.24   |
| XPG       | Unknown                | 1      | 1       | 85    | 0     | 0.23   |
| Crucial   | SiliconMotion based... | 3      | 15      | 84    | 0     | 0.23   |
| China     | Unknown                | 48     | 269     | 87    | 3     | 0.23   |
| Ramsta    | Unknown                | 2      | 2       | 83    | 0     | 0.23   |
| Transcend | JMicron/Maxiotek ba... | 3      | 4       | 102   | 252   | 0.23   |
| e2e4      | Unknown                | 3      | 5       | 83    | 0     | 0.23   |
| Intel     | 545s Series SSDs       | 6      | 41      | 94    | 1     | 0.23   |
| Gigabyte  | Unknown                | 3      | 5       | 81    | 0     | 0.22   |
| Apacer    | Unknown                | 13     | 50      | 82    | 1     | 0.22   |
| Seagate   | 600 Series             | 1      | 1       | 79    | 0     | 0.22   |
| Londisk   | Unknown                | 3      | 10      | 78    | 0     | 0.22   |
| Transcend | Unknown                | 8      | 11      | 139   | 187   | 0.21   |
| Intenso   | Unknown                | 9      | 19      | 79    | 2     | 0.21   |
| Toshiba   | HG6 Series             | 1      | 2       | 76    | 0     | 0.21   |
| SK hynix  | Unknown                | 29     | 55      | 184   | 123   | 0.21   |
| Apacer    | AS340 SSDs             | 3      | 10      | 86    | 1     | 0.21   |
| Gigabyte  | Phison Driven SSDs     | 4      | 21      | 75    | 0     | 0.21   |
| BHT       | Unknown                | 5      | 7       | 74    | 0     | 0.20   |
| V-GeN     | Unknown                | 3      | 3       | 72    | 0     | 0.20   |
| Transcend | SiliconMotion based... | 16     | 90      | 72    | 0     | 0.20   |
| oyunkey   | Unknown                | 1      | 1       | 68    | 0     | 0.19   |
| Netac     | Unknown                | 7      | 15      | 68    | 0     | 0.19   |
| ADATA     | SiliconMotion based... | 2      | 44      | 68    | 1     | 0.19   |
| Integral  | Unknown                | 1      | 3       | 66    | 0     | 0.18   |
| OWC       | SandForce Driven SSDs  | 2      | 3       | 66    | 0     | 0.18   |
| Crucial   | BX/MX1/2/3/500, M5/... | 1      | 3       | 65    | 0     | 0.18   |
| BRAVEE... | Unknown                | 2      | 2       | 65    | 0     | 0.18   |
| Lite-On   | Unknown                | 62     | 133     | 79    | 150   | 0.18   |
| Transcend | Silicon Motion base... | 20     | 74      | 63    | 1     | 0.17   |
| DOGFISH   | Unknown                | 4      | 4       | 62    | 0     | 0.17   |
| Crucial   | Unknown                | 7      | 9       | 152   | 1     | 0.17   |
| Faspeed   | Unknown                | 7      | 7       | 61    | 0     | 0.17   |
| Foxline   | Unknown                | 6      | 8       | 183   | 127   | 0.16   |
| AGI       | Unknown                | 1      | 1       | 59    | 0     | 0.16   |
| TEKET     | Unknown                | 1      | 2       | 59    | 0     | 0.16   |
| KingDian  | Silicon Motion base... | 10     | 49      | 58    | 3     | 0.16   |
| tigo      | Unknown                | 1      | 1       | 57    | 0     | 0.16   |
| DeTech    | Unknown                | 1      | 1       | 57    | 0     | 0.16   |
| Crucial   | Silicon Motion base... | 3      | 23      | 57    | 1     | 0.16   |
| Radeon    | Indilinx Barefoot 3... | 1      | 1       | 56    | 0     | 0.15   |
| TCSUNBOW  | Silicon Motion base... | 2      | 2       | 56    | 0     | 0.15   |
| GLOWAY    | Unknown                | 6      | 8       | 54    | 0     | 0.15   |
| Kingmax   | Unknown                | 4      | 52      | 180   | 379   | 0.15   |
| AMD       | Unknown                | 7      | 30      | 65    | 35    | 0.14   |
| Seagate   | IronWolf 110 SATA SSD  | 1      | 4       | 51    | 0     | 0.14   |
| Leven     | Unknown                | 2      | 3       | 47    | 0     | 0.13   |
| AMD       | SiliconMotion based... | 1      | 25      | 46    | 1     | 0.13   |
| Patriot   | Silicon Motion base... | 2      | 6       | 46    | 0     | 0.13   |
| Zheino    | Unknown                | 14     | 18      | 60    | 2     | 0.13   |
| Fujitsu   | Unknown                | 5      | 5       | 45    | 0     | 0.13   |
| Lenovo    | Unknown                | 4      | 5       | 45    | 0     | 0.12   |
| PRETEC    | Unknown                | 1      | 1       | 44    | 0     | 0.12   |
| Maxtor    | Unknown                | 2      | 3       | 43    | 0     | 0.12   |
| Intel     | SSD Pro 5400s Series   | 1      | 1       | 42    | 0     | 0.12   |
| Kingrich  | Unknown                | 3      | 4       | 188   | 2     | 0.12   |
| Hikvision | Unknown                | 5      | 6       | 57    | 1     | 0.12   |
| Super ... | Unknown                | 2      | 3       | 41    | 0     | 0.11   |
| Fordisk   | Unknown                | 2      | 2       | 41    | 0     | 0.11   |
| KingSpec  | Unknown                | 41     | 98      | 49    | 36    | 0.11   |
| Goldkey   | Unknown                | 2      | 2       | 39    | 0     | 0.11   |
| BIWIN     | Unknown                | 4      | 12      | 37    | 0     | 0.10   |
| GeIL      | Unknown                | 8      | 9       | 64    | 114   | 0.10   |
| Reeinno   | Unknown                | 2      | 2       | 37    | 0     | 0.10   |
| Dogfish   | Unknown                | 3      | 3       | 36    | 0     | 0.10   |
| OCZ       | Intrepid 3000 SSDs     | 2      | 2       | 35    | 0     | 0.10   |
| SUNEAST   | Unknown                | 2      | 2       | 35    | 0     | 0.10   |
| LDLC      | Unknown                | 6      | 14      | 54    | 1     | 0.10   |
| QUMO      | Unknown                | 3      | 5       | 275   | 407   | 0.09   |
| Apple     | SD/SM/TS E/F SSDs      | 2      | 2       | 34    | 0     | 0.09   |
| RECADATA  | Unknown                | 1      | 1       | 33    | 0     | 0.09   |
| Lite-On   | Silicon Motion base... | 2      | 5       | 32    | 0     | 0.09   |
| Toshiba   | SG2 Series             | 1      | 1       | 32    | 0     | 0.09   |
| Lexar     | Unknown                | 7      | 15      | 30    | 0     | 0.08   |
| Hajaan    | Unknown                | 1      | 1       | 30    | 0     | 0.08   |
| TAMMUZ    | Unknown                | 2      | 2       | 29    | 0     | 0.08   |
| KingPower | Unknown                | 1      | 1       | 29    | 0     | 0.08   |
| TAISU     | Unknown                | 1      | 1       | 27    | 0     | 0.08   |
| SenDisk   | Unknown                | 1      | 1       | 27    | 0     | 0.08   |
| T-FORCE   | Unknown                | 3      | 3       | 26    | 0     | 0.07   |
| HECTRON   | Unknown                | 1      | 1       | 26    | 0     | 0.07   |
| KINGBANK  | Unknown                | 1      | 1       | 23    | 0     | 0.06   |
| XUNZHE    | Unknown                | 1      | 1       | 20    | 0     | 0.05   |
| Hyperdisk | Unknown                | 1      | 1       | 18    | 0     | 0.05   |
| LDNDISK   | Unknown                | 1      | 1       | 16    | 0     | 0.05   |
| Platinet  | Unknown                | 1      | 1       | 16    | 0     | 0.04   |
| AEGO      | Unknown                | 1      | 3       | 16    | 0     | 0.04   |
| FORESEE   | Unknown                | 5      | 13      | 15    | 0     | 0.04   |
| Leven     | Silicon Motion base... | 1      | 1       | 15    | 0     | 0.04   |
| Seagate   | 600 Pro Series         | 1      | 1       | 14    | 0     | 0.04   |
| Drevo     | Silicon Motion base... | 1      | 3       | 274   | 23    | 0.04   |
| Kingston  | Silicon Motion base... | 3      | 10      | 13    | 0     | 0.04   |
| Maximus   | Unknown                | 2      | 2       | 13    | 0     | 0.04   |
| addlink   | Unknown                | 2      | 2       | 12    | 0     | 0.03   |
| Wicgtyp   | Unknown                | 1      | 1       | 12    | 0     | 0.03   |
| TCSUNBOW  | Unknown                | 2      | 2       | 12    | 0     | 0.03   |
| XrayDisk  | Unknown                | 3      | 4       | 11    | 0     | 0.03   |
| Micron    | MX1/2/300, M5/600, ... | 1      | 1       | 11    | 0     | 0.03   |
| Golden... | Unknown                | 1      | 1       | 10    | 0     | 0.03   |
| OWC       | Unknown                | 2      | 2       | 10    | 0     | 0.03   |
| Apple     | MacBook Air SSD        | 1      | 3       | 84    | 63    | 0.03   |
| Drevo     | Unknown                | 2      | 2       | 41    | 10    | 0.02   |
| Kingch... | Unknown                | 3      | 3       | 8     | 0     | 0.02   |
| FASTDISK  | Unknown                | 6      | 6       | 7     | 0     | 0.02   |
| INDMEM    | Unknown                | 1      | 1       | 5     | 0     | 0.02   |
| Teclast   | Unknown                | 4      | 5       | 5     | 0     | 0.01   |
| Dell      | Unknown                | 3      | 5       | 5     | 0     | 0.01   |
| SMI       | Unknown                | 3      | 3       | 4     | 653   | 0.01   |
| PHINOCOM  | Unknown                | 1      | 1       | 4     | 0     | 0.01   |
| INNOVA... | Unknown                | 1      | 2       | 4     | 0     | 0.01   |
| KODAK     | Unknown                | 1      | 1       | 4     | 0     | 0.01   |
| Intel     | 540 Series SSDs        | 6      | 12      | 11    | 306   | 0.01   |
| Union ... | Unknown                | 1      | 2       | 3     | 0     | 0.01   |
| Intel     | 311/313 Series SSDs    | 1      | 1       | 112   | 30    | 0.01   |
| ShineDisk | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| i-Flas... | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| KIOXIA... | Unknown                | 1      | 1       | 2     | 0     | 0.01   |
| MicroData | Unknown                | 2      | 2       | 23    | 333   | 0.01   |
| Gigastone | Unknown                | 1      | 1       | 2     | 0     | 0.01   |
| SOLIDATA  | Unknown                | 1      | 1       | 2420  | 1019  | 0.01   |
| ACPI      | Unknown                | 1      | 1       | 2     | 0     | 0.01   |
| Yunhai... | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| acpi      | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| Apacer    | SDM5/5A/5A-M Series... | 1      | 3       | 22    | 20    | 0.00   |
| S3+       | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| ASENNO    | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| OEM       | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| ORTIAL    | Unknown                | 1      | 3       | 0     | 0     | 0.00   |
| Eluktro   | Unknown                | 1      | 1       | 806   | 1016  | 0.00   |
| BAITITON  | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Indilinx  | Unknown                | 1      | 2       | 0     | 0     | 0.00   |
| Gost      | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| ShanDi... | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| TEUTONS   | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Myung     | Unknown                | 1      | 1       | 228   | 1015  | 0.00   |
| Goldenfir | Unknown                | 2      | 2       | 2     | 14    | 0.00   |
| Colorful  | Unknown                | 1      | 1       | 22    | 195   | 0.00   |
| AXIOMT... | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| SandForce | Unknown                | 1      | 1       | 65    | 1018  | 0.00   |
| JIAWEI    | Unknown                | 1      | 1       | 47    | 3057  | 0.00   |

SSD by Vendor
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days   — avg. days per sample,
Err    — avg. errors per sample,
MTBF   — avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF   |
|-------------|--------|---------|-------|-------|--------|
| Hyundai     | 1      | 1       | 997   | 0     | 2.73   |
| HPE         | 3      | 3       | 831   | 0     | 2.28   |
| Micro Ce... | 1      | 1       | 722   | 0     | 1.98   |
| BLueRay     | 1      | 1       | 619   | 0     | 1.70   |
| SATADOM     | 1      | 1       | 574   | 0     | 1.57   |
| MyDigita... | 4      | 5       | 515   | 0     | 1.41   |
| OCZ         | 83     | 483     | 605   | 32    | 1.30   |
| Innodisk    | 5      | 6       | 457   | 0     | 1.25   |
| Corsair     | 44     | 175     | 608   | 83    | 1.24   |
| Intel       | 140    | 535     | 517   | 61    | 1.09   |
| Samsung     | 253    | 2752    | 396   | 7     | 1.06   |
| KingShare   | 1      | 1       | 358   | 0     | 0.98   |
| ZTC         | 1      | 1       | 357   | 0     | 0.98   |
| Apple       | 19     | 56      | 363   | 4     | 0.97   |
| Advantech   | 1      | 1       | 345   | 0     | 0.95   |
| Toshiba     | 79     | 200     | 323   | 6     | 0.85   |
| Kston       | 1      | 1       | 264   | 0     | 0.72   |
| Crucial     | 71     | 881     | 281   | 35    | 0.63   |
| Verbatim    | 5      | 5       | 229   | 0     | 0.63   |
| Mushkin     | 24     | 28      | 390   | 255   | 0.62   |
| Kingston    | 142    | 2114    | 246   | 34    | 0.59   |
| Ramaxel     | 2      | 3       | 204   | 0     | 0.56   |
| SanDisk     | 202    | 1071    | 223   | 41    | 0.55   |
| V-Gen       | 1      | 1       | 200   | 0     | 0.55   |
| Pioneer     | 2      | 5       | 194   | 0     | 0.53   |
| Micron      | 58     | 212     | 245   | 101   | 0.53   |
| Golden m... | 1      | 1       | 190   | 0     | 0.52   |
| PNY         | 29     | 91      | 199   | 46    | 0.52   |
| Phison      | 12     | 41      | 184   | 0     | 0.51   |
| Smartbuy    | 15     | 125     | 193   | 1     | 0.50   |
| Intenso     | 12     | 43      | 178   | 1     | 0.47   |
| Goodram     | 24     | 103     | 166   | 1     | 0.45   |
| Seagate     | 16     | 39      | 275   | 106   | 0.44   |
| KingFast    | 8      | 29      | 152   | 106   | 0.41   |
| Palit       | 3      | 4       | 150   | 0     | 0.41   |
| PHISON      | 3      | 3       | 169   | 1     | 0.41   |
| SPCC        | 28     | 341     | 200   | 123   | 0.40   |
| ADATA       | 84     | 458     | 198   | 68    | 0.40   |
| SK hynix    | 52     | 183     | 207   | 67    | 0.40   |
| HP          | 10     | 23      | 144   | 0     | 0.40   |
| UNIC2       | 1      | 1       | 139   | 0     | 0.38   |
| MENGMI      | 1      | 1       | 139   | 0     | 0.38   |
| Patriot     | 25     | 116     | 171   | 27    | 0.37   |
| ZOTAC       | 2      | 3       | 132   | 0     | 0.36   |
| Plextor     | 51     | 265     | 141   | 17    | 0.35   |
| KLEVV       | 1      | 1       | 127   | 0     | 0.35   |
| Chiprex     | 1      | 1       | 126   | 0     | 0.35   |
| BLUERAY     | 1      | 1       | 125   | 0     | 0.34   |
| Team        | 28     | 53      | 127   | 1     | 0.34   |
| WDC         | 39     | 568     | 125   | 2     | 0.34   |
| Hypertec    | 1      | 2       | 371   | 512   | 0.33   |
| Hoodisk     | 2      | 2       | 118   | 0     | 0.32   |
| BIOSTAR     | 2      | 2       | 109   | 0     | 0.30   |
| ORICO       | 1      | 1       | 99    | 0     | 0.27   |
| GALAX       | 2      | 3       | 98    | 0     | 0.27   |
| Anobit      | 1      | 1       | 96    | 0     | 0.27   |
| Transcend   | 58     | 200     | 98    | 21    | 0.25   |
| Vaseky      | 5      | 6       | 90    | 0     | 0.25   |
| XPG         | 1      | 1       | 85    | 0     | 0.23   |
| China       | 48     | 269     | 87    | 3     | 0.23   |
| Ramsta      | 2      | 2       | 83    | 0     | 0.23   |
| e2e4        | 3      | 5       | 83    | 0     | 0.23   |
| Londisk     | 3      | 10      | 78    | 0     | 0.22   |
| Apacer      | 17     | 63      | 80    | 2     | 0.21   |
| Gigabyte    | 7      | 26      | 76    | 0     | 0.21   |
| KingDian    | 21     | 83      | 78    | 39    | 0.21   |
| BHT         | 5      | 7       | 74    | 0     | 0.20   |
| V-GeN       | 3      | 3       | 72    | 0     | 0.20   |
| oyunkey     | 1      | 1       | 68    | 0     | 0.19   |
| Netac       | 7      | 15      | 68    | 0     | 0.19   |
| Integral    | 1      | 3       | 66    | 0     | 0.18   |
| BRAVEEAGLE  | 2      | 2       | 65    | 0     | 0.18   |
| Lite-On     | 64     | 138     | 77    | 145   | 0.18   |
| DOGFISH     | 4      | 4       | 62    | 0     | 0.17   |
| Faspeed     | 7      | 7       | 61    | 0     | 0.17   |
| Foxline     | 6      | 8       | 183   | 127   | 0.16   |
| AGI         | 1      | 1       | 59    | 0     | 0.16   |
| TEKET       | 1      | 2       | 59    | 0     | 0.16   |
| tigo        | 1      | 1       | 57    | 0     | 0.16   |
| Zheino      | 15     | 20      | 70    | 2     | 0.16   |
| DeTech      | 1      | 1       | 57    | 0     | 0.16   |
| Radeon      | 1      | 1       | 56    | 0     | 0.15   |
| GLOWAY      | 6      | 8       | 54    | 0     | 0.15   |
| Kingmax     | 4      | 52      | 180   | 379   | 0.15   |
| AMD         | 8      | 55      | 57    | 19    | 0.14   |
| Fujitsu     | 5      | 5       | 45    | 0     | 0.13   |
| Lenovo      | 4      | 5       | 45    | 0     | 0.12   |
| PRETEC      | 1      | 1       | 44    | 0     | 0.12   |
| OWC         | 4      | 5       | 43    | 0     | 0.12   |
| Maxtor      | 2      | 3       | 43    | 0     | 0.12   |
| Kingrich    | 3      | 4       | 188   | 2     | 0.12   |
| Hikvision   | 5      | 6       | 57    | 1     | 0.12   |
| Super Ta... | 2      | 3       | 41    | 0     | 0.11   |
| Fordisk     | 2      | 2       | 41    | 0     | 0.11   |
| KingSpec    | 41     | 98      | 49    | 36    | 0.11   |
| Leven       | 3      | 4       | 39    | 0     | 0.11   |
| Goldkey     | 2      | 2       | 39    | 0     | 0.11   |
| BIWIN       | 4      | 12      | 37    | 0     | 0.10   |
| GeIL        | 8      | 9       | 64    | 114   | 0.10   |
| Reeinno     | 2      | 2       | 37    | 0     | 0.10   |
| Dogfish     | 3      | 3       | 36    | 0     | 0.10   |
| SUNEAST     | 2      | 2       | 35    | 0     | 0.10   |
| LDLC        | 6      | 14      | 54    | 1     | 0.10   |
| QUMO        | 3      | 5       | 275   | 407   | 0.09   |
| TCSUNBOW    | 4      | 4       | 34    | 0     | 0.09   |
| RECADATA    | 1      | 1       | 33    | 0     | 0.09   |
| Lexar       | 7      | 15      | 30    | 0     | 0.08   |
| Hajaan      | 1      | 1       | 30    | 0     | 0.08   |
| TAMMUZ      | 2      | 2       | 29    | 0     | 0.08   |
| KingPower   | 1      | 1       | 29    | 0     | 0.08   |
| TAISU       | 1      | 1       | 27    | 0     | 0.08   |
| SenDisk     | 1      | 1       | 27    | 0     | 0.08   |
| T-FORCE     | 3      | 3       | 26    | 0     | 0.07   |
| HECTRON     | 1      | 1       | 26    | 0     | 0.07   |
| KINGBANK    | 1      | 1       | 23    | 0     | 0.06   |
| XUNZHE      | 1      | 1       | 20    | 0     | 0.05   |
| Hyperdisk   | 1      | 1       | 18    | 0     | 0.05   |
| LDNDISK     | 1      | 1       | 16    | 0     | 0.05   |
| Platinet    | 1      | 1       | 16    | 0     | 0.04   |
| AEGO        | 1      | 3       | 16    | 0     | 0.04   |
| FORESEE     | 5      | 13      | 15    | 0     | 0.04   |
| Maximus     | 2      | 2       | 13    | 0     | 0.04   |
| addlink     | 2      | 2       | 12    | 0     | 0.03   |
| Wicgtyp     | 1      | 1       | 12    | 0     | 0.03   |
| Drevo       | 3      | 5       | 180   | 18    | 0.03   |
| XrayDisk    | 3      | 4       | 11    | 0     | 0.03   |
| Goldendisk  | 1      | 1       | 10    | 0     | 0.03   |
| Kingchuxing | 3      | 3       | 8     | 0     | 0.02   |
| FASTDISK    | 6      | 6       | 7     | 0     | 0.02   |
| INDMEM      | 1      | 1       | 5     | 0     | 0.02   |
| Teclast     | 4      | 5       | 5     | 0     | 0.01   |
| Dell        | 3      | 5       | 5     | 0     | 0.01   |
| SMI         | 3      | 3       | 4     | 653   | 0.01   |
| PHINOCOM    | 1      | 1       | 4     | 0     | 0.01   |
| INNOVATION  | 1      | 2       | 4     | 0     | 0.01   |
| KODAK       | 1      | 1       | 4     | 0     | 0.01   |
| Union Me... | 1      | 2       | 3     | 0     | 0.01   |
| ShineDisk   | 1      | 1       | 3     | 0     | 0.01   |
| i-FlashDisk | 1      | 1       | 3     | 0     | 0.01   |
| KIOXIA-E... | 1      | 1       | 2     | 0     | 0.01   |
| MicroData   | 2      | 2       | 23    | 333   | 0.01   |
| Gigastone   | 1      | 1       | 2     | 0     | 0.01   |
| SOLIDATA    | 1      | 1       | 2420  | 1019  | 0.01   |
| ACPI        | 1      | 1       | 2     | 0     | 0.01   |
| Yunhaitian  | 1      | 1       | 1     | 0     | 0.00   |
| acpi        | 1      | 1       | 1     | 0     | 0.00   |
| S3+         | 1      | 1       | 1     | 0     | 0.00   |
| ASENNO      | 1      | 1       | 1     | 0     | 0.00   |
| OEM         | 1      | 1       | 1     | 0     | 0.00   |
| ORTIAL      | 1      | 3       | 0     | 0     | 0.00   |
| Eluktro     | 1      | 1       | 806   | 1016  | 0.00   |
| BAITITON    | 1      | 1       | 0     | 0     | 0.00   |
| Indilinx    | 1      | 2       | 0     | 0     | 0.00   |
| Gost        | 1      | 1       | 0     | 0     | 0.00   |
| ShanDianZhe | 1      | 1       | 0     | 0     | 0.00   |
| TEUTONS     | 1      | 1       | 0     | 0     | 0.00   |
| Myung       | 1      | 1       | 228   | 1015  | 0.00   |
| Goldenfir   | 2      | 2       | 2     | 14    | 0.00   |
| Colorful    | 1      | 1       | 22    | 195   | 0.00   |
| AXIOMTEK... | 1      | 1       | 0     | 0     | 0.00   |
| SandForce   | 1      | 1       | 65    | 1018  | 0.00   |
| JIAWEI      | 1      | 1       | 47    | 3057  | 0.00   |

NVME by Model
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days   — avg. days per sample,
Err    — avg. errors per sample,
MTBF   — avg. MTBF in years per sample.

See complete list of tested NVMe samples in the Appendix 5 ([All_NVMe.md](/All_NVMe.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF   |
|-----------|--------------------|--------|---------|-------|-------|--------|
| Intel     | MEMPEK1J016GAD     | 16 GB  | 1       | 6220  | 0     | 17.04  |
| Samsung   | SSD 950 PRO        | 256 GB | 4       | 998   | 0     | 2.74   |
| Toshiba   | THNSN5256GPU7      | 256 GB | 4       | 947   | 0     | 2.59   |
| Corsair   | Force MP500        | 480 GB | 1       | 869   | 0     | 2.38   |
| Intel     | SSDPEDMW012T4      | 1.2 TB | 1       | 823   | 0     | 2.26   |
| Intel     | SSDPEKKF256G7H     | 256 GB | 4       | 795   | 0     | 2.18   |
| Intel     | SSDPEKKW256G7      | 256 GB | 9       | 840   | 3     | 2.11   |
| Samsung   | SSD 950 PRO        | 512 GB | 12      | 767   | 0     | 2.10   |
| Transcend | TS128GMTE850       | 128 GB | 1       | 745   | 0     | 2.04   |
| Samsung   | MZVKW512HMJP-00000 | 512 GB | 2       | 698   | 0     | 1.91   |
| Intel     | MEMPEK1W032GA      | 32 GB  | 1       | 694   | 0     | 1.90   |
| Samsung   | MZVPV512HDGL-000H1 | 512 GB | 2       | 615   | 0     | 1.69   |
| Intel     | SSDPED1K375GA      | 375 GB | 1       | 603   | 0     | 1.65   |
| Intel     | SSDPEDMD400G4      | 400 GB | 1       | 595   | 0     | 1.63   |
| WDC       | WDS512G1X0C-00ENX0 | 512 GB | 4       | 579   | 0     | 1.59   |
| Toshiba   | THNSN51T02DUK NVMe | 1 TB   | 3       | 566   | 0     | 1.55   |
| Toshiba   | THNSN5512GPUK      | 512 GB | 1       | 563   | 0     | 1.54   |
| Toshiba   | KXG50PNV2T04 1.6TB | 1.6 TB | 1       | 553   | 0     | 1.52   |
| Corsair   | Force MP500        | 120 GB | 4       | 535   | 0     | 1.47   |
| Intel     | SSDPE21D480GA      | 480 GB | 2       | 515   | 0     | 1.41   |
| Samsung   | MZVPV256HDGL-00000 | 256 GB | 5       | 482   | 0     | 1.32   |
| Toshiba   | KXG50ZNV1T02 NVMe  | 1 TB   | 6       | 457   | 0     | 1.25   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 1       | 448   | 0     | 1.23   |
| Intel     | SSDPEKKW010T7      | 1 TB   | 2       | 445   | 0     | 1.22   |
| Samsung   | MZVPV256HDGL-000H1 | 256 GB | 1       | 444   | 0     | 1.22   |
| Intel     | SSDPEKKF256G7L     | 256 GB | 4       | 420   | 0     | 1.15   |
| Samsung   | MS1PC2DD3ORA3.2T   | 3.2 TB | 1       | 416   | 0     | 1.14   |
| Samsung   | MZVPV128HDGM-00000 | 128 GB | 5       | 416   | 0     | 1.14   |
| Toshiba   | RC100              | 240 GB | 1       | 404   | 0     | 1.11   |
| SanDisk   | A400 NVMe          | 512 GB | 2       | 382   | 0     | 1.05   |
| Toshiba   | THNSN5512GPUK NVMe | 512 GB | 14      | 368   | 0     | 1.01   |
| WDC       | WDS256G1X0C-00ENX0 | 256 GB | 2       | 359   | 0     | 0.99   |
| Samsung   | MZSLW1T0HMLH-000L1 | 1 TB   | 2       | 359   | 0     | 0.98   |
| Phison    | Asura NVME         | 2 TB   | 1       | 353   | 0     | 0.97   |
| Samsung   | PM951 NVMe         | 512 GB | 3       | 331   | 0     | 0.91   |
| Toshiba   | THNSN51T02DU7 NVMe | 1 TB   | 1       | 321   | 0     | 0.88   |
| WDC       | WDS200T3XHC-00SJG0 | 2 TB   | 1       | 315   | 0     | 0.87   |
| Intel     | SSDPED1D280GA      | 280 GB | 3       | 311   | 0     | 0.85   |
| XPG       | GAMMIX S11         | 480 GB | 5       | 309   | 0     | 0.85   |
| Toshiba   | THNSN5256GPUK NVMe | 256 GB | 3       | 307   | 0     | 0.84   |
| Samsung   | MZVLV256HCHP-000L2 | 256 GB | 3       | 304   | 0     | 0.83   |
| Intel     | SSDPEKKW512G7      | 512 GB | 9       | 430   | 112   | 0.83   |
| Intel     | SSDPEKKW128G7      | 128 GB | 3       | 402   | 1     | 0.77   |
| SK hynix  | BC501 HFM128GDJ... | 128 GB | 1       | 275   | 0     | 0.75   |
| Toshiba   | THNSN5128GPU7      | 128 GB | 4       | 271   | 0     | 0.74   |
| Toshiba   | THNSF5256GPUK      | 256 GB | 1       | 249   | 0     | 0.68   |
| Mushkin   | MKNSSDPL500GB-D8   | 500 GB | 1       | 248   | 0     | 0.68   |
| Transcend | TS128GMTE110S      | 128 GB | 2       | 241   | 0     | 0.66   |
| Intel     | SSDPEKKF360G7H     | 360 GB | 3       | 239   | 0     | 0.66   |
| ADATA     | SX8200NP           | 960 GB | 3       | 239   | 0     | 0.66   |
| Samsung   | MZVKV512HAJH-000L1 | 512 GB | 3       | 237   | 0     | 0.65   |
| WDC       | WDS250G2X0C-00L350 | 250 GB | 4       | 234   | 0     | 0.64   |
| SanDisk   | Extreme Pro        | 1 TB   | 1       | 234   | 0     | 0.64   |
| Toshiba   | KXG50ZNV512G NVMe  | 512 GB | 15      | 231   | 0     | 0.63   |
| Intel     | SSDPEKKF512G8 NVMe | 512 GB | 2       | 231   | 0     | 0.63   |
| Lite-On   | T10 240            | 240 GB | 1       | 227   | 0     | 0.62   |
| Corsair   | Force MP510 1.9TB  | 1.9 TB | 1       | 223   | 0     | 0.61   |
| Intel     | SSDPED1D480GA      | 480 GB | 2       | 222   | 0     | 0.61   |
| Intel     | MEMPEK1J016GA      | 16 GB  | 2       | 221   | 0     | 0.61   |
| Team      | TM8FP2240G         | 240 GB | 1       | 219   | 0     | 0.60   |
| Toshiba   | KXG5AZNV256G       | 256 GB | 4       | 218   | 0     | 0.60   |
| Samsung   | MZVPV512HDGL-00000 | 512 GB | 1       | 216   | 0     | 0.59   |
| Corsair   | Force MP510        | 960 GB | 9       | 215   | 0     | 0.59   |
| Toshiba   | THNSF5512GPUK      | 512 GB | 4       | 214   | 0     | 0.59   |
| Intel     | SSDPE2KX020T8      | 2 TB   | 3       | 212   | 0     | 0.58   |
| Samsung   | MZVLV256HCHP-00000 | 256 GB | 3       | 210   | 0     | 0.58   |
| Intel     | SSDPE2MX450G7      | 450 GB | 2       | 204   | 0     | 0.56   |
| Lite-On   | CA3-8D512          | 512 GB | 4       | 201   | 0     | 0.55   |
| Samsung   | MZVLW128HEGR-00000 | 128 GB | 2       | 198   | 0     | 0.54   |
| Corsair   | Force MP500        | 240 GB | 4       | 197   | 0     | 0.54   |
| Intel     | SSDPEKKW256G8      | 256 GB | 16      | 195   | 0     | 0.53   |
| Samsung   | MZVLW1T0HMLH-000L2 | 1 TB   | 2       | 193   | 0     | 0.53   |
| Phison    | BPX                | 480 GB | 2       | 193   | 0     | 0.53   |
| Intel     | SSDPEKKF010T8      | 1 TB   | 5       | 191   | 0     | 0.53   |
| Toshiba   | THNSN5512GPUK      | 512 GB | 2       | 189   | 0     | 0.52   |
| Intel     | MEMPEK1J016GAL     | 16 GB  | 5       | 183   | 0     | 0.50   |
| WDC       | WDBRPG5000ANC-WRSN | 500 GB | 1       | 183   | 0     | 0.50   |
| Samsung   | MZVLW1T0HMLH-00000 | 1 TB   | 5       | 183   | 0     | 0.50   |
| Toshiba   | KXG5AZNV512G       | 512 GB | 4       | 181   | 0     | 0.50   |
| SK hynix  | PC601 NVMe         | 1 TB   | 3       | 180   | 0     | 0.49   |
| Toshiba   | KXG50ZNV512G       | 512 GB | 8       | 179   | 0     | 0.49   |
| Intel     | SSDPEKNW020T8      | 2 TB   | 21      | 178   | 0     | 0.49   |
| Samsung   | MZVLV256HCHP-000H1 | 256 GB | 5       | 172   | 0     | 0.47   |
| Team      | M8FP2              | 480 GB | 1       | 172   | 0     | 0.47   |
| Toshiba   | KXG50PNV2T04       | 2 TB   | 2       | 167   | 0     | 0.46   |
| SK hynix  | PC401 NVMe         | 256 GB | 3       | 167   | 0     | 0.46   |
| Toshiba   | KXG50ZNV256G NVMe  | 256 GB | 14      | 164   | 0     | 0.45   |
| Samsung   | MZVLW512HMJP-000L2 | 512 GB | 7       | 163   | 0     | 0.45   |
| Apacer    | AS2280P4           | 480 GB | 1       | 163   | 0     | 0.45   |
| ADATA     | SX8200NP           | 240 GB | 4       | 197   | 30    | 0.44   |
| Toshiba   | THNSN5256GPUK      | 256 GB | 2       | 157   | 0     | 0.43   |
| Lite-On   | CX2-8B512-Q11 NVMe | 512 GB | 2       | 156   | 0     | 0.43   |
| WDC       | WDS500G2X0C-00L350 | 500 GB | 8       | 154   | 0     | 0.42   |
| Samsung   | SM951 NVMe         | 256 GB | 1       | 150   | 0     | 0.41   |
| Samsung   | SSD 960 PRO        | 2 TB   | 6       | 163   | 8     | 0.41   |
| Toshiba   | THNSN0256GTYA      | 256 GB | 1       | 149   | 0     | 0.41   |
| Toshiba   | KXG60PNV2T04 NV... | 2 TB   | 1       | 149   | 0     | 0.41   |
| Kingston  | SKC1000240G        | 240 GB | 1       | 148   | 0     | 0.41   |
| Toshiba   | KXG50ZNV1T02       | 1 TB   | 2       | 147   | 0     | 0.40   |
| Intel     | SSDPEL1D380GA      | 384 GB | 1       | 146   | 0     | 0.40   |
| Phison    | M.2 PCIE G3x4 NVMe | 1 TB   | 2       | 137   | 0     | 0.38   |
| addlink   | M.2 PCIE G3x4 NVMe | 2 TB   | 2       | 135   | 0     | 0.37   |
| Toshiba   | THNSN5256GPU7 NVMe | 256 GB | 3       | 133   | 0     | 0.37   |
| Kingston  | SA1000M8480G       | 480 GB | 4       | 132   | 0     | 0.36   |
| Kingston  | SKC1000480G        | 480 GB | 2       | 131   | 0     | 0.36   |
| Toshiba   | KXG60ZNV512G NVMe  | 512 GB | 21      | 130   | 0     | 0.36   |
| Intel     | SSDPEKKW128G8      | 128 GB | 9       | 130   | 0     | 0.36   |
| Samsung   | SSD 960 EVO        | 500 GB | 46      | 135   | 1     | 0.36   |
| KIOXIA    | KBG40ZPZ512G NVMe  | 512 GB | 1       | 129   | 0     | 0.35   |
| Samsung   | PM951 NVMe         | 1 TB   | 1       | 128   | 0     | 0.35   |
| Lenovo    | LENSE20512GMSP3... | 512 GB | 5       | 126   | 0     | 0.35   |
| Corsair   | Force MP510        | 240 GB | 9       | 125   | 0     | 0.34   |
| Samsung   | SSD 960 PRO        | 512 GB | 30      | 147   | 5     | 0.34   |
| Phison    | BPXP               | 960 GB | 2       | 122   | 0     | 0.33   |
| Mushkin   | MKNSSDPL1TB-D8     | 1 TB   | 1       | 121   | 0     | 0.33   |
| Samsung   | SSD 960 PRO        | 1 TB   | 4       | 119   | 0     | 0.33   |
| Samsung   | MZVKW512HMJP-000H1 | 512 GB | 2       | 117   | 0     | 0.32   |
| Hikvision | HS-SSD-C2000       | 1 TB   | 1       | 116   | 0     | 0.32   |
| Toshiba   | KXG60ZNV1T02 NVMe  | 1 TB   | 2       | 112   | 0     | 0.31   |
| Lenovo    | LENSE20256GMSP3... | 256 GB | 3       | 111   | 0     | 0.31   |
| HP        | SSD EX920          | 512 GB | 3       | 110   | 0     | 0.30   |
| Intel     | MEMPEK1W016GA      | 16 GB  | 3       | 110   | 0     | 0.30   |
| HP        | SSD EX920          | 256 GB | 1       | 325   | 2     | 0.30   |
| SK hynix  | HFS256GD9MNE-6200A | 256 GB | 1       | 107   | 0     | 0.29   |
| Toshiba   | KBG40ZPZ512G NVMe  | 512 GB | 1       | 107   | 0     | 0.29   |
| Seagate   | BarraCuda 510 S... | 500 GB | 1       | 106   | 0     | 0.29   |
| Plextor   | PX-128M8PeGN       | 128 GB | 1       | 106   | 0     | 0.29   |
| Phison    | Sabrent            | 1 TB   | 32      | 104   | 0     | 0.29   |
| PNY       | CS3030 2TB SSD     | 2 TB   | 2       | 103   | 0     | 0.28   |
| Toshiba   | RD400              | 1 TB   | 1       | 101   | 0     | 0.28   |
| Corsair   | Force MP600        | 2 TB   | 4       | 100   | 0     | 0.28   |
| Intel     | H10 HBRPEKNX020... | 512 GB | 1       | 99    | 0     | 0.27   |
| ADATA     | SX8200PNP          | 1 TB   | 27      | 99    | 0     | 0.27   |
| Plextor   | PX-256M9PeGN       | 256 GB | 2       | 98    | 0     | 0.27   |
| Zheino    | CHN-NGFFNV2280-1TB | 1 TB   | 2       | 98    | 0     | 0.27   |
| Goodram   | SSDPR-PX400-256-80 | 256 GB | 1       | 97    | 0     | 0.27   |
| Plextor   | PX-1TM8SeG         | 1 TB   | 2       | 380   | 54    | 0.27   |
| Samsung   | MZVLB2T0HMLB-000L2 | 2 TB   | 1       | 96    | 0     | 0.27   |
| XPG       | GAMMIX S50         | 1 TB   | 1       | 96    | 0     | 0.27   |
| SK hynix  | PC300 NVMe         | 512 GB | 1       | 96    | 0     | 0.26   |
| Samsung   | MZVLW512HMJP-00000 | 512 GB | 7       | 99    | 1     | 0.26   |
| Samsung   | PM961 NVMe         | 512 GB | 7       | 98    | 1     | 0.26   |
| Samsung   | MZVPW256HEGL-00000 | 256 GB | 7       | 93    | 0     | 0.26   |
| Intel     | SSDPEK1W060GA      | 64 GB  | 1       | 93    | 0     | 0.26   |
| Intel     | SSDPEKKW010T8L     | 1 TB   | 1       | 91    | 0     | 0.25   |
| Toshiba   | THNSF5256GPU7      | 256 GB | 1       | 88    | 0     | 0.24   |
| Samsung   | MZVLW256HEHP-000L2 | 256 GB | 13      | 86    | 0     | 0.24   |
| Intel     | SSDPEDMW400G4      | 400 GB | 1       | 86    | 0     | 0.24   |
| Seagate   | FireCuda 520 SS... | 1 TB   | 3       | 86    | 0     | 0.24   |
| Phison    | PCIe SSD           | 1 TB   | 13      | 85    | 0     | 0.24   |
| Toshiba   | THNSN5256GPU7      | 256 GB | 1       | 85    | 0     | 0.23   |
| Samsung   | SSD 970 PRO        | 512 GB | 57      | 86    | 1     | 0.23   |
| Plextor   | PX-256M9PeG        | 256 GB | 1       | 85    | 0     | 0.23   |
| Samsung   | MZVLW1T0HMLH-000L7 | 1 TB   | 3       | 101   | 6     | 0.23   |
| Samsung   | SSD 960 EVO        | 1 TB   | 21      | 83    | 2     | 0.23   |
| WDC       | WDS250G1B0C-00S6U0 | 250 GB | 5       | 82    | 0     | 0.22   |
| Intel     | SSDPEKNW512G8      | 512 GB | 52      | 81    | 0     | 0.22   |
| Samsung   | MZFLV128HCGR-000MV | 128 GB | 4       | 81    | 0     | 0.22   |
| Samsung   | MZVLV128HCGR-00000 | 128 GB | 1       | 81    | 0     | 0.22   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 1       | 81    | 0     | 0.22   |
| Silico... | 1TB PCS PCIe M.... | 1 TB   | 1       | 81    | 0     | 0.22   |
| Samsung   | MZVPV256HDGL-000L2 | 256 GB | 1       | 80    | 0     | 0.22   |
| WDC       | PC SN520 SDAPMU... | 256 GB | 2       | 80    | 0     | 0.22   |
| Toshiba   | KBG40ZNS512G NVMe  | 512 GB | 4       | 77    | 0     | 0.21   |
| ADATA     | SX8200PNP          | 512 GB | 19      | 76    | 0     | 0.21   |
| Crucial   | CT500P1SSD8        | 500 GB | 24      | 79    | 3     | 0.21   |
| Lite-On   | CB1-SD512          | 512 GB | 1       | 75    | 0     | 0.21   |
| Toshiba   | KXG60ZNV256G NV... | 256 GB | 1       | 74    | 0     | 0.20   |
| Plextor   | PX-256M8PeY        | 256 GB | 2       | 73    | 0     | 0.20   |
| Silico... | AITC M.2 FZ300     | 128 GB | 1       | 73    | 0     | 0.20   |
| Toshiba   | KXG50PNV2T04 NVMe  | 2 TB   | 1       | 72    | 0     | 0.20   |
| Intel     | SSDPEKKW512G8      | 512 GB | 10      | 72    | 0     | 0.20   |
| HP        | SSD EX900          | 250 GB | 4       | 72    | 0     | 0.20   |
| Toshiba   | KXG60ZNV256G NVMe  | 256 GB | 8       | 72    | 0     | 0.20   |
| Gigabyte  | GP-ASM2NE6100TTTD  | 1 TB   | 2       | 72    | 0     | 0.20   |
| Samsung   | MZVLB1T0HALR-000L7 | 1 TB   | 14      | 72    | 0     | 0.20   |
| SK hynix  | PC401 HFS256GD9... | 256 GB | 7       | 72    | 0     | 0.20   |
| Phison    | Viper M.2 VPN100   | 1 TB   | 3       | 72    | 0     | 0.20   |
| Crucial   | CT1000P1SSD8       | 1 TB   | 40      | 99    | 23    | 0.20   |
| Samsung   | SSD 970 EVO        | 250 GB | 48      | 79    | 4     | 0.20   |
| HP        | SSD EX900          | 1 TB   | 1       | 71    | 0     | 0.20   |
| Kingston  | RBUSNS8154P3256GJ  | 256 GB | 3       | 71    | 0     | 0.20   |
| Intel     | SSDPEKKF256G8 NVMe | 256 GB | 3       | 71    | 0     | 0.20   |
| Transcend | TS512GMTE220S      | 512 GB | 1       | 70    | 0     | 0.19   |
| Intel     | SSDPEKNW010T8      | 1 TB   | 60      | 70    | 0     | 0.19   |
| Team      | TM8FP4001T         | 1 TB   | 3       | 70    | 0     | 0.19   |
| Samsung   | MZVLW128HEGR-000H1 | 128 GB | 5       | 68    | 0     | 0.19   |
| Samsung   | MZVKW1T0HMLH-000L7 | 1 TB   | 1       | 67    | 0     | 0.19   |
| HP        | SSD EX950          | 2 TB   | 3       | 67    | 0     | 0.19   |
| Samsung   | SSD 960 EVO        | 250 GB | 75      | 73    | 3     | 0.19   |
| Samsung   | PM961 NVMe         | 1 TB   | 1       | 67    | 0     | 0.18   |
| Toshiba   | KBG30ZMT128G       | 128 GB | 8       | 67    | 0     | 0.18   |
| Patriot   | Scorch M2          | 256 GB | 3       | 67    | 0     | 0.18   |
| ADATA     | SX8200NP           | 480 GB | 2       | 67    | 0     | 0.18   |
| Toshiba   | KXG6AZNV256G       | 256 GB | 6       | 65    | 0     | 0.18   |
| Kingston  | SA2000M81000G      | 1 TB   | 17      | 64    | 0     | 0.18   |
| Samsung   | PM981 NVMe         | 1 TB   | 2       | 64    | 0     | 0.18   |
| Samsung   | MZVLW256HEHP-00000 | 256 GB | 24      | 64    | 0     | 0.18   |
| Samsung   | KUS020203M-B000    | 128 GB | 1       | 64    | 0     | 0.18   |
| XPG       | GAMMIX S11 Pro     | 1 TB   | 24      | 62    | 0     | 0.17   |
| Samsung   | PM951 NVMe         | 256 GB | 1       | 61    | 0     | 0.17   |
| Plextor   | PX-512M8PeG        | 512 GB | 3       | 100   | 184   | 0.17   |
| Phison    | Sabrent Rocket 4.0 | 1 TB   | 14      | 60    | 0     | 0.17   |
| KIOXIA    | KBG40ZPZ1T02 NVMe  | 1 TB   | 1       | 60    | 0     | 0.17   |
| Phison    | Sabrent Rocket 4.0 | 2 TB   | 3       | 60    | 0     | 0.17   |
| Kingch... | 256GB              | 256 GB | 1       | 60    | 0     | 0.16   |
| Intel     | SSDPEKKW256G8L     | 256 GB | 2       | 58    | 0     | 0.16   |
| WDC       | WDS500G1B0C-00S6U0 | 500 GB | 3       | 58    | 0     | 0.16   |
| Toshiba   | KXG60ZNV1T02       | 1 TB   | 2       | 58    | 0     | 0.16   |
| WDC       | WDS100T3XHC-00SJG0 | 1 TB   | 1       | 58    | 0     | 0.16   |
| Corsair   | Force MP510        | 480 GB | 8       | 58    | 0     | 0.16   |
| Hikvision | HS-SSD-C2000Pro    | 1 TB   | 1       | 58    | 0     | 0.16   |
| Phison    | SBX                | 256 GB | 1       | 58    | 0     | 0.16   |
| Gigabyte  | GP-GSM2NE8256GNTD  | 256 GB | 1       | 57    | 0     | 0.16   |
| ADATA     | SX6000NP           | 128 GB | 2       | 170   | 81    | 0.16   |
| SK hynix  | PC401 NVMe         | 512 GB | 19      | 56    | 0     | 0.15   |
| Toshiba   | KBG40ZPZ256G ME... | 256 GB | 1       | 55    | 0     | 0.15   |
| Samsung   | MZVLB512HAJQ-00000 | 512 GB | 31      | 55    | 0     | 0.15   |
| Micron    | 2200S NVMe         | 256 GB | 3       | 55    | 0     | 0.15   |
| Samsung   | PM981 NVMe         | 512 GB | 11      | 64    | 1     | 0.15   |
| WDC       | PC SN520 NVMe      | 256 GB | 8       | 54    | 0     | 0.15   |
| Toshiba   | KBG30ZMS256G NVMe  | 256 GB | 8       | 54    | 0     | 0.15   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 13      | 54    | 0     | 0.15   |
| Intel     | SSDPE2KX040T8      | 4 TB   | 4       | 53    | 0     | 0.15   |
| Kingston  | RBUSNS8154P3102... | 1 TB   | 1       | 53    | 0     | 0.15   |
| Samsung   | SSD 970 EVO        | 500 GB | 106     | 55    | 10    | 0.15   |
| SK hynix  | PC611 NVMe         | 512 GB | 4       | 53    | 0     | 0.15   |
| ADATA     | SX8200PNP          | 256 GB | 14      | 65    | 72    | 0.14   |
| Samsung   | MZVLW512HMJP-000H1 | 512 GB | 6       | 52    | 0     | 0.14   |
| Toshiba   | KBG30ZMT256G       | 256 GB | 2       | 52    | 0     | 0.14   |
| Apple     | SSD SM2048L        | 2 TB   | 1       | 52    | 0     | 0.14   |
| SPCC      | M.2 PCIe SSD       | 1 TB   | 3       | 51    | 0     | 0.14   |
| Intel     | SSDPEKKW010T8      | 1 TB   | 3       | 51    | 0     | 0.14   |
| Plextor   | PX-256M8PeG        | 256 GB | 1       | 51    | 0     | 0.14   |
| Seagate   | FireCuda 510 SS... | 1 TB   | 3       | 51    | 0     | 0.14   |
| SK hynix  | PC300 NVMe         | 1 TB   | 3       | 50    | 0     | 0.14   |
| Toshiba   | KXG50ZNV256G       | 256 GB | 3       | 50    | 0     | 0.14   |
| Kingston  | SA2000M8500G       | 500 GB | 10      | 49    | 0     | 0.14   |
| SPCC      | M.2 PCIe SSD       | 512 GB | 4       | 49    | 0     | 0.14   |
| Samsung   | MZVLW512HMJP-000L7 | 512 GB | 5       | 51    | 1     | 0.13   |
| Intel     | SSDPEKKF256G8L     | 256 GB | 23      | 48    | 0     | 0.13   |
| Corsair   | Force MP300        | 240 GB | 1       | 48    | 0     | 0.13   |
| WDC       | WDS100T2X0C-00L350 | 1 TB   | 4       | 48    | 0     | 0.13   |
| Gigabyte  | GP-GSM2NE3100TNTD  | 1 TB   | 3       | 48    | 0     | 0.13   |
| ADATA     | SX6000PNP          | 512 GB | 3       | 47    | 0     | 0.13   |
| Samsung   | SSD 970 PRO        | 1 TB   | 28      | 47    | 0     | 0.13   |
| Samsung   | SSD 970 EVO        | 1 TB   | 75      | 47    | 1     | 0.13   |
| WDC       | PC SN720 SDAQNT... | 256 GB | 4       | 46    | 0     | 0.13   |
| WDC       | WDS500G3X0C-00SJG0 | 500 GB | 15      | 46    | 0     | 0.13   |
| Samsung   | MZVLB1T0HALR-000L2 | 1 TB   | 8       | 46    | 0     | 0.13   |
| Intel     | HBRPEKNX0202ALO    | 32 GB  | 2       | 46    | 0     | 0.13   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 4       | 46    | 0     | 0.13   |
| Intel     | SSDPE2KE020T7      | 2 TB   | 4       | 46    | 0     | 0.13   |
| WDC       | WDS250G3X0C-00SJG0 | 250 GB | 4       | 45    | 0     | 0.12   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 4       | 45    | 0     | 0.12   |
| Hikvision | HS-SSD-E2000       | 512 GB | 1       | 45    | 0     | 0.12   |
| Patriot   | Scorch M2          | 128 GB | 2       | 45    | 0     | 0.12   |
| Toshiba   | KBG30ZMV512G       | 512 GB | 6       | 45    | 0     | 0.12   |
| Samsung   | MZVLB512HAJQ-000L7 | 512 GB | 42      | 45    | 1     | 0.12   |
| HP        | SSD EX920          | 1 TB   | 4       | 44    | 0     | 0.12   |
| Intel     | SSDPEKKF010T8 NVMe | 1 TB   | 2       | 44    | 0     | 0.12   |
| Silico... | Asgard AN2 250N... | 250 GB | 1       | 44    | 0     | 0.12   |
| Plextor   | PX-512M9PeY        | 512 GB | 3       | 44    | 0     | 0.12   |
| Intel     | SSDPEKKF512G7H     | 512 GB | 1       | 44    | 0     | 0.12   |
| Intel     | SSDPEKNW010T8H     | 1 TB   | 3       | 43    | 0     | 0.12   |
| Toshiba   | KXG60ZNV1T02 NV... | 1 TB   | 4       | 43    | 0     | 0.12   |
| Corsair   | Force MP600        | 1 TB   | 8       | 43    | 0     | 0.12   |
| Patriot   | Scorch M2          | 512 GB | 2       | 42    | 0     | 0.12   |
| Intel     | SSDPEKNW010T9      | 1 TB   | 1       | 42    | 0     | 0.12   |
| Apple     | SSD AP0032H        | 24 GB  | 1       | 42    | 0     | 0.12   |
| SK hynix  | PC601 NVMe         | 512 GB | 14      | 42    | 0     | 0.12   |
| Toshiba   | KBG40ZNS256G NVMe  | 256 GB | 5       | 41    | 0     | 0.11   |
| Samsung   | MZVLB512HBJQ-00007 | 512 GB | 1       | 41    | 0     | 0.11   |
| Toshiba   | KXG60ZNV512G       | 512 GB | 7       | 41    | 0     | 0.11   |
| Samsung   | MZVLB512HAJQ-000L2 | 512 GB | 9       | 40    | 0     | 0.11   |
| SK hynix  | PC601 NVMe         | 256 GB | 3       | 40    | 0     | 0.11   |
| Samsung   | PM981 NVMe         | 256 GB | 10      | 40    | 0     | 0.11   |
| SPCC      | M.2 PCIe SSD       | 256 GB | 5       | 40    | 0     | 0.11   |
| Intel     | SSDPEKNW512G8H     | 512 GB | 35      | 40    | 2     | 0.11   |
| Kingston  | RBUSNS8154P3128GJ  | 128 GB | 8       | 40    | 0     | 0.11   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 1       | 39    | 0     | 0.11   |
| Samsung   | MZVKW512HMJP-000L7 | 512 GB | 2       | 39    | 0     | 0.11   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 5       | 39    | 0     | 0.11   |
| PNY       | CS3030 250GB SSD   | 250 GB | 3       | 38    | 0     | 0.11   |
| Micron    | 2200 NVMe          | 512 GB | 1       | 38    | 0     | 0.11   |
| Intel     | HBRPEKNX0202AHO    | 32 GB  | 4       | 38    | 0     | 0.11   |
| WDC       | PC SN720 SDAQNT... | 512 GB | 10      | 38    | 0     | 0.11   |
| XPG       | GAMMIX S5          | 1 TB   | 5       | 38    | 0     | 0.11   |
| Samsung   | MZFLV256HCHP-000MV | 256 GB | 1       | 38    | 0     | 0.10   |
| Intel     | HBRPEKNX0203AHO    | 32 GB  | 2       | 37    | 0     | 0.10   |
| Intel     | HBRPEKNX0202AL     | 512 GB | 3       | 37    | 0     | 0.10   |
| Samsung   | MZVLW256HEHP-000H1 | 256 GB | 16      | 58    | 2     | 0.10   |
| Toshiba   | KXG60ZNV512G NV... | 512 GB | 8       | 37    | 0     | 0.10   |
| Samsung   | SSD 970 EVO Plus   | 2 TB   | 15      | 37    | 0     | 0.10   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 9       | 36    | 0     | 0.10   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 2       | 36    | 0     | 0.10   |
| WDC       | WDS100T2B0C-00PXH0 | 1 TB   | 13      | 36    | 0     | 0.10   |
| Toshiba   | KXG50PNV2T04 NV... | 2 TB   | 2       | 36    | 0     | 0.10   |
| WDC       | PC SN720 SDAQNT... | 1 TB   | 1       | 36    | 0     | 0.10   |
| WDC       | PC SN520 SDAPMU... | 512 GB | 2       | 35    | 0     | 0.10   |
| WDC       | WDS500G2B0C-00PXH0 | 500 GB | 14      | 34    | 0     | 0.10   |
| Intel     | HBRPEKNX0203AH     | 1 TB   | 2       | 34    | 0     | 0.10   |
| WDC       | PC SN520 SDAPMU... | 512 GB | 18      | 34    | 0     | 0.09   |
| Samsung   | MZVLB1T0HALR-00000 | 1 TB   | 11      | 34    | 1     | 0.09   |
| Samsung   | MZVLB256HAHQ-000L7 | 256 GB | 13      | 34    | 0     | 0.09   |
| Kingston  | RBUSNS8154P3512GJ3 | 512 GB | 1       | 34    | 0     | 0.09   |
| Kingston  | SA1000M8240G       | 240 GB | 9       | 34    | 0     | 0.09   |
| Samsung   | PM961 NVMe         | 256 GB | 4       | 33    | 0     | 0.09   |
| Samsung   | MZVLB256HAHQ-00000 | 256 GB | 18      | 33    | 0     | 0.09   |
| WDC       | WDS100T3X0C-00SJG0 | 1 TB   | 14      | 33    | 0     | 0.09   |
| ADATA     | IM2P33F3 NVMe      | 512 GB | 2       | 33    | 0     | 0.09   |
| SPCC      | M.2 PCIE SSD       | 1 TB   | 2       | 33    | 0     | 0.09   |
| WDC       | WDS500G3XHC-00SJG0 | 500 GB | 2       | 32    | 0     | 0.09   |
| Toshiba   | KBG30ZMV256G       | 256 GB | 8       | 32    | 0     | 0.09   |
| Lenovo    | LENSE30512GMSP3... | 512 GB | 3       | 32    | 0     | 0.09   |
| Phison    | Sabrent Rocket Q   | 1 TB   | 13      | 32    | 0     | 0.09   |
| Silico... | M Series NVMe S... | 256 GB | 2       | 32    | 0     | 0.09   |
| PNY       | CS3030 500GB SSD   | 500 GB | 4       | 31    | 0     | 0.09   |
| WDC       | PC SN520 NVMe      | 128 GB | 4       | 31    | 0     | 0.09   |
| Silico... | NE-512             | 512 GB | 4       | 31    | 0     | 0.09   |
| Huawei    | HWE52P433T2M005N   | 3.2 TB | 4       | 31    | 0     | 0.09   |
| ADATA     | SX6000NP           | 256 GB | 1       | 31    | 0     | 0.09   |
| WDC       | CL SN520 SDAPMU... | 512 GB | 1       | 30    | 0     | 0.08   |
| Intel     | HBRPEKNX0202AH     | 512 GB | 6       | 30    | 0     | 0.08   |
| Samsung   | MZQLB1T9HAJR-00007 | 1.9 TB | 6       | 30    | 0     | 0.08   |
| SK hynix  | BC501 HFM256GDJ... | 256 GB | 15      | 30    | 140   | 0.08   |
| WDC       | PC SN730 NVMe      | 512 GB | 3       | 30    | 0     | 0.08   |
| Kingston  | SA2000M8250G       | 250 GB | 14      | 30    | 0     | 0.08   |
| Apple     | SSD SM0128L        | 121 GB | 1       | 30    | 0     | 0.08   |
| Samsung   | MZVLB1T0HALR-000H1 | 1 TB   | 8       | 29    | 0     | 0.08   |
| Intel     | MEMPEK1J016GAH     | 16 GB  | 1       | 29    | 0     | 0.08   |
| Silico... | JAMESDONKEY JD512  | 512 GB | 1       | 28    | 0     | 0.08   |
| Lenovo    | LENSE30256GMSP3... | 256 GB | 3       | 28    | 0     | 0.08   |
| Samsung   | SSD 970 EVO Plus   | 500 GB | 121     | 28    | 0     | 0.08   |
| Seagate   | FireCuda 510 SS... | 2 TB   | 2       | 28    | 0     | 0.08   |
| Samsung   | SSD 970 EVO Plus   | 1 TB   | 101     | 28    | 0     | 0.08   |
| Intel     | SSDPEKKF512G8L     | 512 GB | 16      | 27    | 0     | 0.08   |
| Apple     | SSD AP0512M        | 500 GB | 1       | 27    | 0     | 0.08   |
| ADATA     | SX6000PNP          | 256 GB | 3       | 27    | 0     | 0.08   |
| SK hynix  | SKHynix_HFS001T... | 1 TB   | 2       | 27    | 0     | 0.08   |
| Samsung   | MZVLW256HEHP-000L7 | 256 GB | 12      | 30    | 3     | 0.08   |
| Samsung   | MZVKW1T0HMLH-000H1 | 1 TB   | 1       | 27    | 0     | 0.07   |
| Toshiba   | KBG30ZPZ128G       | 128 GB | 2       | 27    | 0     | 0.07   |
| Toshiba   | KBG30ZMV128G       | 128 GB | 2       | 26    | 0     | 0.07   |
| SK hynix  | PC401 NVMe         | 1 TB   | 3       | 26    | 0     | 0.07   |
| Samsung   | MZVKW1T0HMLH-00000 | 1 TB   | 1       | 26    | 0     | 0.07   |
| HP        | SSD EX950          | 1 TB   | 4       | 26    | 0     | 0.07   |
| Kingston  | OM8PCP3512F-AB     | 512 GB | 7       | 25    | 0     | 0.07   |
| Micron    | 2200V_MTFDHBA51... | 512 GB | 3       | 25    | 0     | 0.07   |
| Toshiba   | KXG6AZNV512G       | 512 GB | 6       | 25    | 0     | 0.07   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 5       | 24    | 0     | 0.07   |
| Toshiba   | KBG30ZMT512G       | 512 GB | 2       | 24    | 0     | 0.07   |
| SK hynix  | HFS256GD9TNG-62A0A | 256 GB | 5       | 24    | 0     | 0.07   |
| Toshiba   | RC500              | 250 GB | 1       | 24    | 0     | 0.07   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 20      | 24    | 53    | 0.07   |
| Intel     | SSDPEMKF512G8 NVMe | 512 GB | 10      | 23    | 0     | 0.07   |
| Intel     | SSDPEKNW512G8L     | 512 GB | 7       | 23    | 0     | 0.06   |
| Samsung   | MZ1LB3T8HMLA-00007 | 3.8 TB | 2       | 23    | 0     | 0.06   |
| SK hynix  | BA HFS256GD9TNG... | 256 GB | 2       | 23    | 0     | 0.06   |
| KIOXIA    | KBG40ZNS256G NVMe  | 256 GB | 9       | 23    | 0     | 0.06   |
| Samsung   | MZVLW128HEGR-000L2 | 128 GB | 4       | 23    | 0     | 0.06   |
| WDC       | PC SN520 NVMe      | 512 GB | 7       | 22    | 0     | 0.06   |
| Apple     | SSD SM0512L        | 500 GB | 1       | 22    | 0     | 0.06   |
| Silico... | IM2P33F8BR1-512GB  | 512 GB | 2       | 21    | 0     | 0.06   |
| HP        | SSD EX900          | 500 GB | 2       | 217   | 40    | 0.06   |
| Intel     | SSDPEBKF256G7      | 256 GB | 1       | 21    | 0     | 0.06   |
| ADATA     | SX6000LNP          | 256 GB | 4       | 21    | 0     | 0.06   |
| Silico... | R5MP240G8          | 240 GB | 2       | 21    | 0     | 0.06   |
| Samsung   | MZVLB512HAJQ-000H1 | 512 GB | 34      | 20    | 0     | 0.06   |
| Samsung   | KUS030202M-B000    | 256 GB | 1       | 20    | 0     | 0.06   |
| Samsung   | SSD 970 EVO Plus   | 250 GB | 52      | 20    | 0     | 0.06   |
| Lexar     | 500GB SSD          | 500 GB | 2       | 20    | 0     | 0.06   |
| Samsung   | SSD 970 EVO        | 2 TB   | 6       | 119   | 19    | 0.06   |
| WDC       | PC SN520 SDAPMU... | 256 GB | 10      | 19    | 0     | 0.05   |
| Silico... | OSC PCIE           | 512 GB | 1       | 19    | 0     | 0.05   |
| Kingston  | RBUSNS8154P3512GJ  | 512 GB | 5       | 19    | 0     | 0.05   |
| Samsung   | MZVLB256HAHQ-000H1 | 256 GB | 27      | 19    | 0     | 0.05   |
| SK hynix  | PC601 HFS512GD9... | 512 GB | 7       | 19    | 0     | 0.05   |
| Lite-On   | CL1-3D256-Q11 NVMe | 256 GB | 4       | 18    | 0     | 0.05   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 2       | 18    | 0     | 0.05   |
| Kingston  | RBUSNS8154P3512GJ2 | 512 GB | 1       | 18    | 0     | 0.05   |
| HP        | SSD EX900          | 120 GB | 3       | 18    | 0     | 0.05   |
| Lite-On   | CL1-4D256          | 256 GB | 2       | 18    | 0     | 0.05   |
| ADATA     | IM2P33F3 NVMe      | 256 GB | 5       | 18    | 0     | 0.05   |
| Samsung   | MZVLB256HBHQ-00007 | 256 GB | 1       | 18    | 0     | 0.05   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 9       | 17    | 0     | 0.05   |
| Samsung   | MZVLB256HBHQ-00000 | 256 GB | 3       | 17    | 0     | 0.05   |
| SK hynix  | BC501 NVMe         | 128 GB | 5       | 16    | 0     | 0.05   |
| WDC       | WDS250G2B0C-00PXH0 | 250 GB | 2       | 16    | 0     | 0.05   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 9       | 16    | 0     | 0.05   |
| Samsung   | MZVLB256HAHQ-000L2 | 256 GB | 14      | 16    | 0     | 0.05   |
| Phison    | Sabrent Rocket 4.0 | 500 GB | 2       | 16    | 0     | 0.04   |
| Silico... | KingSSD-N201000    | 1 TB   | 1       | 16    | 0     | 0.04   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 2       | 16    | 0     | 0.04   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 4       | 16    | 0     | 0.04   |
| Colorful  | CN600S             | 480 GB | 1       | 16    | 0     | 0.04   |
| Micron    | MTFDHBA512TCK      | 512 GB | 1       | 15    | 0     | 0.04   |
| Toshiba   | KBG30ZMV256G KI... | 256 GB | 8       | 15    | 0     | 0.04   |
| Union ... | RPFTJ128PDD2EWX    | 128 GB | 13      | 15    | 0     | 0.04   |
| ADATA     | SX6000LNP          | 512 GB | 3       | 15    | 0     | 0.04   |
| SK hynix  | BA HFS512GD9TNG... | 512 GB | 1       | 15    | 0     | 0.04   |
| SK hynix  | PC300 NVMe         | 256 GB | 4       | 30    | 2     | 0.04   |
| FORESEE   | 256GB SSD          | 256 GB | 2       | 15    | 0     | 0.04   |
| Samsung   | PM991 NVMe         | 256 GB | 4       | 15    | 0     | 0.04   |
| XPG       | SPECTRIX S40G      | 2 TB   | 3       | 15    | 0     | 0.04   |
| Samsung   | MZVLW1T0HMLH-000H1 | 1 TB   | 1       | 15    | 0     | 0.04   |
| Samsung   | MZVLB1T0HBLR-000L2 | 1 TB   | 19      | 15    | 0     | 0.04   |
| ADATA     | SX8200PNP          | 2 TB   | 2       | 14    | 0     | 0.04   |
| Lite-On   | CL1-8D512          | 512 GB | 2       | 14    | 0     | 0.04   |
| Silico... | R5MP480G8          | 480 GB | 1       | 14    | 0     | 0.04   |
| Kingston  | RBUSNS8154P3256GJ3 | 256 GB | 6       | 14    | 0     | 0.04   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 1       | 14    | 0     | 0.04   |
| Phison    | Sabrent Rocket ... | 1 TB   | 1       | 14    | 0     | 0.04   |
| WDC       | WDS200T3X0C-00SJG0 | 2 TB   | 2       | 13    | 0     | 0.04   |
| Samsung   | PM981a NVMe        | 1 TB   | 4       | 13    | 0     | 0.04   |
| SK hynix  | HFM256GDHTNG-8310A | 256 GB | 6       | 13    | 0     | 0.04   |
| Patriot   | M.2 P300           | 512 GB | 1       | 12    | 0     | 0.04   |
| Samsung   | MZALQ512HALU-000L1 | 512 GB | 8       | 12    | 0     | 0.04   |
| Union ... | RPFTJ256PDD2MWX    | 256 GB | 4       | 12    | 0     | 0.04   |
| Transcend | TS1TMTE220S        | 1 TB   | 1       | 12    | 0     | 0.03   |
| Samsung   | MZVLB2T0HALB-000L7 | 2 TB   | 6       | 12    | 0     | 0.03   |
| Intel     | SSDPEKKF010T8L     | 1 TB   | 12      | 12    | 0     | 0.03   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 1       | 12    | 0     | 0.03   |
| SK hynix  | HFM256GDHTNG-8510B | 256 GB | 2       | 12    | 0     | 0.03   |
| Toshiba   | KBG30ZMS128G NVMe  | 128 GB | 2       | 11    | 0     | 0.03   |
| Intel     | SSDPEMKF010T8 NVMe | 1 TB   | 6       | 19    | 169   | 0.03   |
| WDC       | PC SN520 SDAPMU... | 128 GB | 4       | 11    | 0     | 0.03   |
| Samsung   | MZVLB512HBJQ-000L7 | 512 GB | 46      | 11    | 0     | 0.03   |
| Transcend | TS256GMTE220S      | 256 GB | 2       | 11    | 0     | 0.03   |
| ADATA     | SX6000PNP          | 1 TB   | 7       | 11    | 0     | 0.03   |
| Micron    | 2200_MTFDHBA512TCK | 512 GB | 1       | 11    | 0     | 0.03   |
| Samsung   | PM981a NVMe        | 256 GB | 1       | 11    | 0     | 0.03   |
| WDC       | CL SN720 SDAQNT... | 1 TB   | 1       | 11    | 0     | 0.03   |
| Samsung   | PM981a NVMe        | 2 TB   | 3       | 11    | 0     | 0.03   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 4       | 10    | 0     | 0.03   |
| Silico... | Qunion P20A 512... | 512 GB | 1       | 10    | 0     | 0.03   |
| WDC       | PC SN730 SDBQNT... | 512 GB | 32      | 10    | 0     | 0.03   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 2       | 10    | 0     | 0.03   |
| Apple     | SSD SM0256L        | 256 GB | 1       | 10    | 0     | 0.03   |
| Lite-On   | CA1-8D128-HP       | 128 GB | 3       | 10    | 0     | 0.03   |
| Micron    | 2200S NVMe         | 1 TB   | 4       | 10    | 0     | 0.03   |
| Seagate   | IronWolf510 ZP9... | 960 GB | 2       | 10    | 0     | 0.03   |
| WDC       | PC SN730 SDBQNT... | 256 GB | 3       | 9     | 0     | 0.03   |
| Union ... | UMIS RPITJ256PE... | 256 GB | 1       | 9     | 0     | 0.03   |
| ADATA     | SX6000LNP          | 1 TB   | 3       | 9     | 0     | 0.03   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 2       | 9     | 0     | 0.03   |
| Kingston  | RBUSNS8154P3512GJ1 | 512 GB | 1       | 9     | 0     | 0.03   |
| Samsung   | MZVLB1T0HBLR-000L7 | 1 TB   | 30      | 8     | 0     | 0.02   |
| SK hynix  | HFS512GD9TNG-62A0A | 512 GB | 1       | 8     | 0     | 0.02   |
| Phison    | Viper M.2 VPR100   | 512 GB | 1       | 8     | 0     | 0.02   |
| Phison    | Daten DS2000       | 512 GB | 1       | 8     | 0     | 0.02   |
| Silico... | NVME SSD           | 128 GB | 2       | 8     | 0     | 0.02   |
| Kingston  | RBUSNS8154P3256GJ1 | 256 GB | 7       | 8     | 0     | 0.02   |
| Toshiba   | KBG40ZNT512G ME... | 512 GB | 7       | 8     | 0     | 0.02   |
| SPCC      | M.2 PCIE SSD       | 512 GB | 1       | 8     | 0     | 0.02   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 7       | 8     | 0     | 0.02   |
| Apple     | SSD SM0032L        | 32 GB  | 4       | 8     | 0     | 0.02   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 2       | 8     | 0     | 0.02   |
| Hikvision | HS-SSD-C2000Pro... | 1 TB   | 1       | 8     | 0     | 0.02   |
| Micron    | MTFDHBA1T0TCK      | 1 TB   | 3       | 8     | 0     | 0.02   |
| Intel     | SSDPEKNU512G8L     | 512 GB | 1       | 8     | 0     | 0.02   |
| SK hynix  | HFM512GDHTNG-8310A | 512 GB | 3       | 8     | 0     | 0.02   |
| Samsung   | PM991 NVMe         | 512 GB | 3       | 8     | 0     | 0.02   |
| WDC       | PC SN720 SDAPNT... | 1 TB   | 2       | 8     | 0     | 0.02   |
| Intel     | HBRPEKNX0202AO     | 32 GB  | 2       | 7     | 0     | 0.02   |
| Lexar     | 250GB SSD          | 250 GB | 1       | 7     | 0     | 0.02   |
| Apple     | SSD AP0256J        | 256 GB | 2       | 7     | 0     | 0.02   |
| Samsung   | MZVLB512HBJQ-000L2 | 512 GB | 33      | 7     | 0     | 0.02   |
| WDC       | PC SN520 SDAPMU... | 512 GB | 2       | 7     | 0     | 0.02   |
| SK hynix  | BC501 NVMe         | 256 GB | 5       | 7     | 0     | 0.02   |
| KIOXIA    | KBG40ZPZ256G NVMe  | 256 GB | 1       | 7     | 0     | 0.02   |
| Toshiba   | KXG60ZNV512G KI... | 512 GB | 4       | 7     | 0     | 0.02   |
| Silico... | NE-128             | 128 GB | 2       | 7     | 0     | 0.02   |
| Toshiba   | KXG5AZNV256G NV... | 256 GB | 1       | 7     | 0     | 0.02   |
| Toshiba   | KXG60ZNV256G       | 256 GB | 1       | 7     | 0     | 0.02   |
| Union ... | UMIS RPJTJ256ME... | 256 GB | 1       | 7     | 0     | 0.02   |
| Micron    | 2200S NVMe         | 512 GB | 8       | 7     | 0     | 0.02   |
| Lite-On   | CX2-8B256-Q11 NVMe | 256 GB | 1       | 7     | 0     | 0.02   |
| Intel     | HBRPEKNX0202A      | 512 GB | 2       | 7     | 0     | 0.02   |
| Samsung   | MZVLB256HBHQ-000L7 | 256 GB | 14      | 6     | 0     | 0.02   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 2       | 6     | 0     | 0.02   |
| Samsung   | MZVLB2T0HALB-000L2 | 2 TB   | 1       | 6     | 0     | 0.02   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 2       | 6     | 0     | 0.02   |
| Samsung   | PM981a NVMe        | 512 GB | 9       | 6     | 0     | 0.02   |
| KIOXIA    | KBG40ZNS512G NVMe  | 512 GB | 5       | 6     | 0     | 0.02   |
| FORESEE   | 512GB SSD          | 512 GB | 2       | 6     | 0     | 0.02   |
| Micron    | 2200_MTFDHBA256TCK | 256 GB | 2       | 6     | 0     | 0.02   |
| Toshiba   | KBG40ZMT128G ME... | 128 GB | 2       | 6     | 0     | 0.02   |
| Gigabyte  | GP-ASM2NE6200TTTD  | 2 TB   | 2       | 6     | 0     | 0.02   |
| KIOXIA    | KBG40ZNV256G       | 256 GB | 1       | 6     | 0     | 0.02   |
| Mushkin   | MKNSSDHL1TB-D8     | 1 TB   | 2       | 79    | 37    | 0.02   |
| SK hynix  | BC511 NVMe         | 256 GB | 4       | 6     | 0     | 0.02   |
| Seagate   | FireCuda 520 SS... | 500 GB | 2       | 6     | 0     | 0.02   |
| Samsung   | PM981a NVMe SED    | 512 GB | 1       | 5     | 0     | 0.02   |
| Union ... | UMIS RPJTJ512ME... | 512 GB | 1       | 5     | 0     | 0.02   |
| Toshiba   | KBG30ZMV512G KI... | 512 GB | 5       | 5     | 0     | 0.02   |
| Team      | TM8FP4256G         | 256 GB | 1       | 5     | 0     | 0.02   |
| Transcend | TS512GMTE110S      | 512 GB | 3       | 5     | 0     | 0.02   |
| Samsung   | MZVLB256HBHQ-000L2 | 256 GB | 9       | 5     | 0     | 0.02   |
| SK hynix  | PC611 NVMe         | 1 TB   | 2       | 5     | 0     | 0.02   |
| Toshiba   | RC500              | 500 GB | 1       | 5     | 0     | 0.01   |
| Samsung   | MZVLB2T0HMLB-000H1 | 2 TB   | 1       | 5     | 0     | 0.01   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 4       | 5     | 0     | 0.01   |
| PNY       | CS3030 2000GB SSD  | 2 TB   | 1       | 5     | 0     | 0.01   |
| Crucial   | CT500P2SSD8        | 500 GB | 1       | 5     | 0     | 0.01   |
| SK hynix  | BC501A NVMe        | 128 GB | 2       | 5     | 0     | 0.01   |
| Silico... | R5MP120G8          | 120 GB | 1       | 5     | 0     | 0.01   |
| Apple     | SSD AP0512N        | 500 GB | 2       | 4     | 0     | 0.01   |
| KIOXIA    | KBG40ZNV1T02       | 1 TB   | 4       | 4     | 0     | 0.01   |
| Phison    | SBXe               | 480 GB | 1       | 4     | 0     | 0.01   |
| Samsung   | PM981 NVMe SED     | 512 GB | 1       | 4     | 0     | 0.01   |
| Corsair   | Force MP600        | 500 GB | 2       | 4     | 0     | 0.01   |
| MAXIO     | NE-256             | 256 GB | 1       | 4     | 0     | 0.01   |
| SK hynix  | SKHynix_HFS001T... | 1 TB   | 1       | 4     | 0     | 0.01   |
| ADATA     | SWORDFISH          | 1 TB   | 4       | 4     | 0     | 0.01   |
| SK hynix  | BC501 HFM512GDJ... | 512 GB | 14      | 4     | 0     | 0.01   |
| Toshiba   | KBG40ZNT256G ME... | 256 GB | 3       | 4     | 0     | 0.01   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 3       | 4     | 0     | 0.01   |
| Samsung   | MZALQ512HALU-000L2 | 512 GB | 14      | 4     | 0     | 0.01   |
| ADATA     | SX6000NP           | 512 GB | 2       | 4     | 0     | 0.01   |
| SK hynix  | BC501 NVMe         | 512 GB | 4       | 4     | 0     | 0.01   |
| Samsung   | MZVLQ512HALU-00000 | 512 GB | 11      | 4     | 0     | 0.01   |
| WDC       | PC SN520 SDAPMU... | 128 GB | 4       | 4     | 0     | 0.01   |
| Lite-On   | CL1-3D128-Q11 NVMe | 128 GB | 1       | 4     | 0     | 0.01   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 1       | 4     | 0     | 0.01   |
| Samsung   | MZVLQ1T0HALB-00000 | 1 TB   | 1       | 4     | 0     | 0.01   |
| SK hynix  | BC511 NVMe         | 512 GB | 4       | 3     | 0     | 0.01   |
| Union ... | UMIS RPJTJ256ME... | 256 GB | 1       | 3     | 0     | 0.01   |
| Apple     | SSD AP0512J        | 500 GB | 1       | 3     | 0     | 0.01   |
| WDC       | PC SN730 SDBQNT... | 1 TB   | 9       | 3     | 0     | 0.01   |
| Lite-On   | CA3-8D256          | 256 GB | 2       | 3     | 0     | 0.01   |
| SanDisk   | Ultra 3D NVMe      | 500 GB | 1       | 3     | 0     | 0.01   |
| ADATA     | SX6000LNP          | 128 GB | 3       | 3     | 0     | 0.01   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 3       | 3     | 0     | 0.01   |
| Samsung   | MZVLB512HAJQ-000H7 | 512 GB | 4       | 3     | 0     | 0.01   |
| KIOXIA    | KBG40ZNV512G       | 512 GB | 6       | 3     | 0     | 0.01   |
| Gigabyte  | GP-ASM2NE6500GTTD  | 500 GB | 1       | 3     | 0     | 0.01   |
| Gigabyte  | GP-GSM2NE8128GNTD  | 128 GB | 1       | 3     | 0     | 0.01   |
| Samsung   | MZALQ256HAJD-000L1 | 256 GB | 3       | 2     | 0     | 0.01   |
| Toshiba   | KXG60ZNV1T02 KI... | 1 TB   | 1       | 2     | 0     | 0.01   |
| Toshiba   | KXG60ZNV256G KI... | 256 GB | 2       | 2     | 0     | 0.01   |
| SanDisk   | Extreme Pro        | 500 GB | 1       | 2     | 0     | 0.01   |
| Corsair   | MP400              | 2 TB   | 1       | 2     | 0     | 0.01   |
| Samsung   | MZVLB512HBJQ-00000 | 512 GB | 5       | 2     | 0     | 0.01   |
| SK hynix  | HFM512GDHTNG-8710B | 512 GB | 9       | 2     | 0     | 0.01   |
| Samsung   | MZVLB512HBJQ-000H1 | 512 GB | 6       | 2     | 0     | 0.01   |
| Silico... | 256GB              | 256 GB | 1       | 2     | 0     | 0.01   |
| Solid ... | SSSTC CL1-4D256    | 256 GB | 1       | 2     | 0     | 0.01   |
| WDC       | PC SN730 SDBPNT... | 256 GB | 1       | 2     | 0     | 0.01   |
| Samsung   | MZVLB1T0HBLR-000H1 | 1 TB   | 5       | 2     | 0     | 0.01   |
| FORESEE   | P900F256GB         | 256 GB | 1       | 2     | 0     | 0.01   |
| Seagate   | FireCuda 520 SS... | 2 TB   | 2       | 2     | 0     | 0.01   |
| Solid ... | CL1-3D256-Q11 N... | 256 GB | 1       | 2     | 0     | 0.01   |
| Silico... | NE-256             | 256 GB | 4       | 2     | 0     | 0.01   |
| SK hynix  | SHGP31-1000GM-2    | 1 TB   | 1       | 2     | 0     | 0.01   |
| Samsung   | MZALQ256HAJD-000L2 | 256 GB | 8       | 2     | 0     | 0.01   |
| SK hynix  | HFM512GDJTNG-8310A | 512 GB | 14      | 1     | 0     | 0.01   |
| Intel     | SSDPEKKA256G7      | 256 GB | 2       | 1     | 0     | 0.01   |
| Samsung   | MZVLB1T0HBLR-00000 | 1 TB   | 4       | 1     | 0     | 0.01   |
| Silico... | NE-1TB             | 1 TB   | 1       | 1     | 0     | 0.01   |
| Toshiba   | KBG30ZMV128G KI... | 128 GB | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN730 NVMe      | 1 TB   | 4       | 1     | 0     | 0.00   |
| WDC       | PC SN730 SDBPNT... | 256 GB | 3       | 1     | 0     | 0.00   |
| SK hynix  | SKHynix_HFM512G... | 512 GB | 6       | 1     | 0     | 0.00   |
| Toshiba   | KXG6AZNV1T02       | 1 TB   | 1       | 1     | 0     | 0.00   |
| Union ... | UMIS RPITJ512PE... | 512 GB | 2       | 1     | 0     | 0.00   |
| Solid ... | CL1-3D512-Q11 N... | 512 GB | 1       | 1     | 0     | 0.00   |
| Lite-On   | CA3-8D128-HP       | 128 GB | 2       | 1     | 0     | 0.00   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 3       | 1     | 0     | 0.00   |
| Samsung   | MZALQ128HBHQ-000L2 | 128 GB | 2       | 1     | 0     | 0.00   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 1       | 1     | 0     | 0.00   |
| SK hynix  | HFM256GDJTNI-82A0A | 256 GB | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 2       | 1     | 0     | 0.00   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 8       | 1     | 0     | 0.00   |
| Silico... | Asgard AN3 1TNV... | 1 TB   | 1       | 1     | 0     | 0.00   |
| Intel     | SSDPEDKE020T7      | 2 TB   | 2       | 1     | 0     | 0.00   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | MZVLB1T0HBLR-00007 | 1 TB   | 1       | 1     | 0     | 0.00   |
| SK hynix  | HFS512GD9TNG-L2A0A | 512 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | MZVLQ256HAJD-000H1 | 256 GB | 8       | 1     | 0     | 0.00   |
| Micron    | MTFDHBA256TCK      | 256 GB | 2       | 1     | 0     | 0.00   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 2       | 1     | 0     | 0.00   |
| Samsung   | MZVPW128HEGM-00000 | 128 GB | 1       | 37    | 32    | 0.00   |
| Kingston  | SKC2000M81000G     | 1 TB   | 1       | 1     | 0     | 0.00   |
| Micron    | MTFDHBA256TCK-1... | 256 GB | 8       | 3     | 1     | 0.00   |
| Samsung   | MZVLQ256HAJD-00000 | 256 GB | 3       | 1     | 0     | 0.00   |
| Goodram   | SSDPR-PX500-512-80 | 512 GB | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 6       | 1     | 0     | 0.00   |
| Crucial   | CT2000P5SSD8       | 2 TB   | 1       | 1     | 0     | 0.00   |
| Samsung   | MZVLQ512HALU-000H1 | 512 GB | 6       | 0     | 0     | 0.00   |
| Kingston  | OM8PCP3512F-AA     | 512 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TS256GMTE110S      | 256 GB | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | HFM128GDJTNG-8310A | 128 GB | 1       | 0     | 0     | 0.00   |
| XrayDisk  | 256GB              | 256 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | SKHynix_HFM256G... | 256 GB | 9       | 0     | 0     | 0.00   |
| Samsung   | MZALQ128HBHQ-000L1 | 128 GB | 2       | 0     | 0     | 0.00   |
| WDC       | PC SN530 SDBPMP... | 512 GB | 3       | 0     | 0     | 0.00   |
| ADATA     | SX8100NP           | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | HFM256GDJTNG-8310A | 256 GB | 5       | 0     | 0     | 0.00   |
| Samsung   | MZVLB512HBJQ-00A00 | 512 GB | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN530 SDBPMP... | 256 GB | 3       | 0     | 0     | 0.00   |
| Lite-On   | CA1-8D256-HP       | 256 GB | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN530 NVMe      | 256 GB | 1       | 0     | 0     | 0.00   |
| Zheino    | CHN-NGFFNV2280-256 | 256 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | RBUSNS8154P3128GJ1 | 128 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVLB256HBHQ-000H1 | 256 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | BC511 HFM512GDJ... | 512 GB | 4       | 0     | 0     | 0.00   |
| ADATA     | IM2P33F8-512GD     | 512 GB | 1       | 0     | 0     | 0.00   |
| Plextor   | PX-512M9PeGN       | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | Skhynix BC501 NVMe | 512 GB | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 1       | 0     | 0     | 0.00   |
| SPCC      | M.2 PCIE SSD       | 256 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | SSD 980 PRO        | 1 TB   | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN530 NVMe      | 512 GB | 1       | 0     | 0     | 0.00   |
| Apple     | SSD AP0256M        | 256 GB | 1       | 0     | 0     | 0.00   |
| Apple     | SSD AP1024N        | 1 TB   | 1       | 0     | 0     | 0.00   |
| SK hynix  | HFM512GDJTNI-82A0A | 512 GB | 1       | 0     | 0     | 0.00   |
| Toshiba   | KBG40ZPZ128G ME... | 128 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TS512GMTE510T      | 512 GB | 1       | 0     | 0     | 0.00   |
| Gigabyte  | GP-ASM2NE2512GTTDR | 512 GB | 1       | 0     | 0     | 0.00   |
| Gigabyte  | GP-GSM2NE3512GNTD  | 512 GB | 1       | 0     | 0     | 0.00   |
| Mushkin   | MKNSSDPE1TB-D8     | 1 TB   | 1       | 0     | 0     | 0.00   |
| PNY       | CS3030 1TB SSD     | 1 TB   | 1       | 0     | 0     | 0.00   |
| SK hynix  | HFM128GDHTNG-8310A | 128 GB | 1       | 0     | 0     | 0.00   |
| Lite-On   | CA5-8D512          | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN730 NVMe      | 256 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | BC511 HFM256GDJ... | 256 GB | 5       | 0     | 0     | 0.00   |
| Crucial   | CT2000P1SSD8       | 2 TB   | 1       | 0     | 0     | 0.00   |
| SK hynix  | HFM128GDHTNG-8510B | 128 GB | 1       | 0     | 0     | 0.00   |

NVME by Vendor
--------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days   — avg. days per sample,
Err    — avg. errors per sample,
MTBF   — avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF   |
|-------------|--------|---------|-------|-------|--------|
| SanDisk     | 4      | 5       | 200   | 0     | 0.55   |
| Apacer      | 1      | 1       | 163   | 0     | 0.45   |
| Corsair     | 12     | 52      | 160   | 0     | 0.44   |
| Toshiba     | 68     | 265     | 141   | 0     | 0.39   |
| Intel       | 62     | 403     | 143   | 6     | 0.38   |
| addlink     | 1      | 2       | 135   | 0     | 0.37   |
| Transcend   | 8      | 12      | 112   | 0     | 0.31   |
| Team        | 4      | 6       | 101   | 0     | 0.28   |
| XPG         | 5      | 38      | 88    | 0     | 0.24   |
| Lenovo      | 4      | 14      | 82    | 0     | 0.23   |
| Phison      | 16     | 92      | 81    | 0     | 0.22   |
| Mushkin     | 4      | 5       | 106   | 15    | 0.21   |
| Crucial     | 5      | 67      | 87    | 15    | 0.19   |
| Plextor     | 9      | 16      | 111   | 42    | 0.19   |
| Zheino      | 2      | 3       | 65    | 0     | 0.18   |
| ADATA       | 22     | 115     | 67    | 12    | 0.17   |
| Samsung     | 123    | 1539    | 63    | 2     | 0.17   |
| Kingchuxing | 1      | 1       | 60    | 0     | 0.16   |
| Lite-On     | 14     | 27      | 59    | 0     | 0.16   |
| Hikvision   | 4      | 4       | 57    | 0     | 0.16   |
| HP          | 9      | 25      | 79    | 4     | 0.15   |
| Goodram     | 2      | 2       | 49    | 0     | 0.14   |
| Patriot     | 4      | 8       | 48    | 0     | 0.13   |
| Kingston    | 20     | 100     | 43    | 0     | 0.12   |
| PNY         | 5      | 11      | 41    | 0     | 0.11   |
| Seagate     | 7      | 15      | 40    | 0     | 0.11   |
| WDC         | 80     | 381     | 39    | 3     | 0.11   |
| SPCC        | 6      | 16      | 39    | 0     | 0.11   |
| Huawei      | 1      | 4       | 31    | 0     | 0.09   |
| Gigabyte    | 8      | 12      | 30    | 0     | 0.08   |
| SK hynix    | 53     | 225     | 27    | 10    | 0.07   |
| Silicon ... | 19     | 30      | 20    | 0     | 0.06   |
| KIOXIA      | 8      | 28      | 17    | 0     | 0.05   |
| Lexar       | 2      | 3       | 16    | 0     | 0.04   |
| Colorful    | 1      | 1       | 16    | 0     | 0.04   |
| Apple       | 12     | 17      | 14    | 0     | 0.04   |
| Micron      | 11     | 36      | 13    | 1     | 0.03   |
| Union Me... | 7      | 23      | 12    | 0     | 0.03   |
| FORESEE     | 3      | 5       | 9     | 0     | 0.03   |
| MAXIO       | 1      | 1       | 4     | 0     | 0.01   |
| Solid St... | 3      | 3       | 2     | 0     | 0.01   |
| XrayDisk    | 1      | 1       | 0     | 0     | 0.00   |

