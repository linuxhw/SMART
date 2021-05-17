HDD/SSD Desktop-Class Reliability Test
======================================

This is a project to estimate reliability of desktop-class HDD/SSD drives by
the analysis of SMART data collected by Linux users at https://linux-hardware.org. The
primary aim of the project is to find drives with longest power-on hours (POH) and
minimal number of errors, i.e. maximal MTBF (mean time between failures).

Everyone can contribute to this report by uploading probes of their computers by
the [hw-probe](https://github.com/linuxhw/hw-probe) tool:

    sudo -E hw-probe -all -upload

Total drives: 71679.

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

See complete list of tested HDD samples in the Appendix 1 ([All_HDD.md](/All_HDD.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF   |
|-----------|--------------------|--------|---------|-------|-------|--------|
| Samsung   | SV1021H            | 10 GB  | 1       | 5713  | 0     | 15.65  |
| WDC       | WD2500SD-01KCB0    | 250 GB | 1       | 4068  | 0     | 11.15  |
| Hitachi   | HCP725025GLAT80    | 250 GB | 1       | 4058  | 0     | 11.12  |
| Hitachi   | HUA721075KLA330    | 752 GB | 1       | 3668  | 0     | 10.05  |
| Hitachi   | HDS728040PLA320... | 40 GB  | 1       | 3563  | 0     | 9.76   |
| Hitachi   | HUA7210SASUN1.0... | 1 TB   | 1       | 3495  | 0     | 9.58   |
| HP        | GB0160EAFJE        | 160 GB | 2       | 3447  | 0     | 9.44   |
| WDC       | WD10EAVS-32D7B1    | 1 TB   | 1       | 3311  | 0     | 9.07   |
| WDC       | WD20EACS-11BHUB0   | 2 TB   | 1       | 3085  | 0     | 8.45   |
| Samsung   | HE160HJ            | 160 GB | 1       | 2967  | 0     | 8.13   |
| WDC       | WD84AA             | 8 GB   | 1       | 2903  | 0     | 7.95   |
| WDC       | WD1200JB-00REA0    | 120 GB | 1       | 2899  | 0     | 7.94   |
| WDC       | WD2500AAJS-62B4A0  | 250 GB | 1       | 2854  | 0     | 7.82   |
| WDC       | WD2500AVJB-63J5A0  | 250 GB | 1       | 2804  | 0     | 7.68   |
| Seagate   | ST2000VM002-9UY166 | 2 TB   | 1       | 2787  | 0     | 7.64   |
| WDC       | WD10EACS-14ZJB0    | 1 TB   | 1       | 2742  | 0     | 7.51   |
| WDC       | WD5000AVVS-63ZWB0  | 500 GB | 1       | 2707  | 0     | 7.42   |
| WDC       | WD2500AAJS-00RYA0  | 250 GB | 1       | 2695  | 0     | 7.39   |
| WDC       | WD3000HLFS-01G6U1  | 304 GB | 1       | 2636  | 0     | 7.22   |
| WDC       | WD30EURS-73TLHY0   | 3 TB   | 1       | 2606  | 0     | 7.14   |
| WDC       | WD2000FYYZ-01UL1B0 | 2 TB   | 1       | 2603  | 0     | 7.13   |
| WDC       | WD10EACS-00C7B0    | 1 TB   | 3       | 2600  | 0     | 7.12   |
| WDC       | WD5000BUCT-63PUZY0 | 500 GB | 1       | 2564  | 0     | 7.03   |
| WDC       | WD5000AAKS-60A7B0  | 500 GB | 1       | 2536  | 0     | 6.95   |
| WDC       | WD5000AAKS-40YGA1  | 500 GB | 1       | 2532  | 0     | 6.94   |
| Hitachi   | HUA7210SASUN1.0T   | 1 TB   | 10      | 2520  | 0     | 6.91   |
| WDC       | WD740GD-00FLA1     | 74 GB  | 1       | 2489  | 0     | 6.82   |
| Seagate   | ST3320820AS_P      | 320 GB | 1       | 2447  | 0     | 6.70   |
| WDC       | WD2003FYYS-18W0B0  | 2 TB   | 2       | 2425  | 0     | 6.65   |
| WDC       | WD7502ABYS-18A6B0  | 752 GB | 1       | 2416  | 0     | 6.62   |
| WDC       | WD60EFRX-68MYMN0   | 6 TB   | 1       | 2399  | 0     | 6.58   |
| Seagate   | ST3250820AS Q      | 250 GB | 1       | 2361  | 0     | 6.47   |
| WDC       | WD2500AAJS-07VWA0  | 250 GB | 2       | 2354  | 0     | 6.45   |
| Hitachi   | HUA722020ALA330    | 2 TB   | 15      | 2867  | 3     | 6.41   |
| Seagate   | ST320LT014-9YK142  | 320 GB | 1       | 2336  | 0     | 6.40   |
| Hitachi   | HDS721025CLA682    | 250 GB | 2       | 2308  | 0     | 6.32   |
| WDC       | WD5001AALS-00J7B0  | 500 GB | 1       | 2295  | 0     | 6.29   |
| WDC       | WD1600JS-75NCB1    | 160 GB | 1       | 2267  | 0     | 6.21   |
| Seagate   | ST3750641NS EIT    | 752 GB | 1       | 2229  | 0     | 6.11   |
| WDC       | WD1001FALS-00K1B0  | 1 TB   | 2       | 2199  | 0     | 6.02   |
| Seagate   | ST3750641NS        | 752 GB | 1       | 2169  | 0     | 5.94   |
| WDC       | WD2500AAJS-61B4A0  | 250 GB | 1       | 2168  | 0     | 5.94   |
| WDC       | WD1600AAJS-61WAA0  | 160 GB | 1       | 2124  | 0     | 5.82   |
| Hitachi   | HCS5C3225SLA380    | 250 GB | 1       | 2124  | 0     | 5.82   |
| WDC       | WD5000ABYS-01TNA0  | 500 GB | 2       | 2117  | 0     | 5.80   |
| WDC       | WD3200AVJB-63J5A0  | 320 GB | 2       | 2113  | 0     | 5.79   |
| Toshiba   | MK2002TSKB         | 2 TB   | 1       | 2104  | 0     | 5.77   |
| Hitachi   | HUA722010ALA330    | 1 TB   | 3       | 2094  | 0     | 5.74   |
| WDC       | WD5000AADS-57S9B1  | 500 GB | 1       | 2086  | 0     | 5.72   |
| WDC       | WD800JD-75MSA1     | 80 GB  | 2       | 2057  | 0     | 5.64   |
| Seagate   | ST320413A          | 20 GB  | 1       | 2013  | 0     | 5.52   |
| HP        | GB0500C4413        | 500 GB | 2       | 2009  | 0     | 5.51   |
| WDC       | WD3200BUDT-63DPZY0 | 320 GB | 1       | 2008  | 0     | 5.50   |
| WDC       | WD1002FBYS-18W8B1  | 1 TB   | 1       | 1999  | 0     | 5.48   |
| WDC       | WD1600ADFS-75SLR2  | 160 GB | 1       | 1997  | 0     | 5.47   |
| WDC       | WD2500YS-01SHB0    | 256 GB | 3       | 1995  | 0     | 5.47   |
| WDC       | WD2502ABYS-02B7A0  | 256 GB | 4       | 2063  | 3     | 5.45   |
| WDC       | WD800AAJB-00J3A0   | 80 GB  | 1       | 1982  | 0     | 5.43   |
| WDC       | WD1601ABYS-01C0A0  | 164 GB | 1       | 1982  | 0     | 5.43   |
| WDC       | WD7500KMVV-11A27S0 | 752 GB | 1       | 1976  | 0     | 5.42   |
| WDC       | WD1600AAJS-00RYA0  | 160 GB | 1       | 1970  | 0     | 5.40   |
| Hitachi   | HDS722020ALA330... | 2 TB   | 1       | 1963  | 0     | 5.38   |
| WDC       | WD3000GLFS-01F8U0  | 304 GB | 3       | 1958  | 0     | 5.37   |
| Hitachi   | HUA722010CLA331    | 1 TB   | 1       | 1939  | 0     | 5.31   |
| WDC       | WD400BD-55MTA1     | 40 GB  | 2       | 1915  | 0     | 5.25   |
| WDC       | WD4000FYYZ-01UL1B2 | 4 TB   | 2       | 1907  | 0     | 5.23   |
| WDC       | WD15EARS-32MVWB0   | 1.5 TB | 1       | 1831  | 0     | 5.02   |
| WDC       | WD7500AAKS-22RBA0  | 752 GB | 1       | 1816  | 0     | 4.98   |
| Toshiba   | MK3255GSXF         | 320 GB | 1       | 1812  | 0     | 4.97   |
| WDC       | WD360GD-00FNA0     | 37 GB  | 2       | 2599  | 1     | 4.95   |
| WDC       | WD2500YS-70SHB1    | 250 GB | 1       | 1789  | 0     | 4.90   |
| WDC       | WD2003FYPS-27Y2B0  | 2 TB   | 7       | 1952  | 1     | 4.90   |
| WDC       | WD1500HLFS-01G6U0  | 150 GB | 4       | 1805  | 1     | 4.87   |
| Hitachi   | HUA721050KLA330    | 500 GB | 2       | 1774  | 0     | 4.86   |
| Seagate   | ST6000NM0024-1H... | 6 TB   | 1       | 1769  | 0     | 4.85   |
| WDC       | WD2500JS-40MVB1    | 250 GB | 1       | 1763  | 0     | 4.83   |
| WDC       | WD2500KS-22MJB0    | 250 GB | 1       | 1734  | 0     | 4.75   |
| WDC       | WD3200KS-00PFB0    | 320 GB | 5       | 1994  | 19    | 4.73   |
| WDC       | WD4000AAJS-22YFA0  | 400 GB | 1       | 1725  | 0     | 4.73   |
| WDC       | WD1600JD-00HBC0    | 160 GB | 2       | 2053  | 3     | 4.72   |
| Samsung   | HE103UJ            | 1 TB   | 1       | 1723  | 0     | 4.72   |
| Hitachi   | HCS5C3020BLE630    | 2 TB   | 1       | 1717  | 0     | 4.70   |
| WDC       | WD400JB-00ENA0     | 40 GB  | 3       | 2383  | 6     | 4.69   |
| HGST      | HTE541515A9E630    | 1.5 TB | 1       | 1702  | 0     | 4.66   |
| WDC       | WD6400AAKS-41H2B0  | 640 GB | 2       | 1700  | 0     | 4.66   |
| WDC       | WD3200JS-55PDB0    | 320 GB | 1       | 1698  | 0     | 4.65   |
| Seagate   | ST500LX003-1AC15G  | 500 GB | 1       | 1697  | 0     | 4.65   |
| WDC       | WD5000LPCX-16VHAT0 | 500 GB | 1       | 1686  | 0     | 4.62   |
| WDC       | WD7500AACS-00D6B0  | 752 GB | 2       | 1686  | 0     | 4.62   |
| Samsung   | SP0411N            | 40 GB  | 2       | 3755  | 9     | 4.62   |
| WDC       | WD2502ABYS-01B7A0  | 256 GB | 6       | 2094  | 1     | 4.62   |
| Seagate   | ST9500320AS        | 500 GB | 2       | 1684  | 0     | 4.62   |
| WDC       | WD3200AAJB-00WGA0  | 320 GB | 3       | 1682  | 0     | 4.61   |
| WDC       | WD30EURS-63SPKY0   | 3 TB   | 5       | 1681  | 0     | 4.61   |
| WDC       | WD1601ABYS-18C0A0  | 160 GB | 3       | 2288  | 4     | 4.58   |
| WDC       | WD1600JS-88MHB0    | 160 GB | 1       | 1667  | 0     | 4.57   |
| Seagate   | ST91000640NS       | 1 TB   | 20      | 1822  | 2     | 4.57   |
| Seagate   | ST2000NX0253       | 2 TB   | 16      | 1662  | 0     | 4.55   |
| Seagate   | ST1000NX0423       | 1 TB   | 2       | 1662  | 0     | 4.55   |
| WDC       | WD3000HLFS-01G6U4  | 304 GB | 2       | 1654  | 0     | 4.53   |
| WDC       | WD6400AAKS-00H2B1  | 640 GB | 1       | 1653  | 0     | 4.53   |
| WDC       | WD3200LPVX-16V0TT3 | 320 GB | 1       | 1644  | 0     | 4.50   |
| Seagate   | ST500DM002-1ER14C  | 500 GB | 2       | 1632  | 0     | 4.47   |
| HP        | FB080C4080         | 80 GB  | 1       | 1630  | 0     | 4.47   |
| HGST      | HUS724020ALE640    | 2 TB   | 10      | 1628  | 0     | 4.46   |
| Seagate   | ST3200021A         | 200 GB | 1       | 1624  | 0     | 4.45   |
| WDC       | WD5000AAKS-40V2B0  | 500 GB | 1       | 1619  | 0     | 4.44   |
| Seagate   | ST2000DL004 HD2... | 2 TB   | 3       | 1617  | 0     | 4.43   |
| WDC       | WD5000AUDX-61WNHY0 | 500 GB | 1       | 1614  | 0     | 4.42   |
| WDC       | WD1002FBYS-05A6B0  | 1 TB   | 2       | 1606  | 0     | 4.40   |
| WDC       | WD7500AYYS-01RCA0  | 752 GB | 5       | 1678  | 1     | 4.39   |
| WDC       | WD1600JB-22GVA0    | 160 GB | 1       | 1600  | 0     | 4.39   |
| WDC       | WD30EFRX-68AX9N0   | 3 TB   | 39      | 1800  | 1     | 4.35   |
| WDC       | WD2000JB-16FUA0    | 200 GB | 1       | 1584  | 0     | 4.34   |
| WDC       | WD3200AAVS-00ZTB0  | 320 GB | 1       | 1583  | 0     | 4.34   |
| WDC       | WD2502ABYS-23B7... | 250 GB | 4       | 1580  | 0     | 4.33   |
| Toshiba   | MQ01ABD032V        | 320 GB | 1       | 1578  | 0     | 4.33   |
| Samsung   | HD502HM            | 500 GB | 1       | 1573  | 0     | 4.31   |
| Hitachi   | HCC545025B9A300    | 250 GB | 1       | 1573  | 0     | 4.31   |
| WDC       | WD20EADS-11R6B1    | 2 TB   | 1       | 1558  | 0     | 4.27   |
| WDC       | WD3200AAJS-22RYA0  | 320 GB | 4       | 1539  | 0     | 4.22   |
| Hitachi   | HDS723030ALA640    | 3 TB   | 11      | 1699  | 9     | 4.22   |
| WDC       | WD4000AAJS-65TKA0  | 400 GB | 1       | 1532  | 0     | 4.20   |
| Seagate   | ST31000424CS       | 1 TB   | 1       | 1527  | 0     | 4.19   |
| HPE       | MB0500EBNCR        | 500 GB | 1       | 1526  | 0     | 4.18   |
| WDC       | WD2502ABYS-23B7... | 250 GB | 2       | 1522  | 0     | 4.17   |
| Seagate   | ST4000NM0024-1H... | 4 TB   | 4       | 1519  | 0     | 4.16   |
| WDC       | WD2003FYYS-02W0B0  | 2 TB   | 9       | 1781  | 1     | 4.13   |
| Seagate   | ST980412ASG        | 80 GB  | 1       | 1501  | 0     | 4.11   |
| WDC       | WD2500AAJS-22VWA0  | 250 GB | 3       | 1496  | 0     | 4.10   |
| Quantum   | FIREBALLlct10 05   | 5 GB   | 1       | 1486  | 0     | 4.07   |
| WDC       | WD1200JS-55NCB1    | 120 GB | 1       | 1484  | 0     | 4.07   |
| Seagate   | ST3000NM0053       | 3 TB   | 1       | 1484  | 0     | 4.07   |
| WDC       | WD2000JD-00GBB0    | 200 GB | 1       | 1482  | 0     | 4.06   |
| WDC       | WD3200AAKX-753CA0  | 320 GB | 1       | 1471  | 0     | 4.03   |
| Toshiba   | MG03ACA200         | 2 TB   | 4       | 1456  | 0     | 3.99   |
| Seagate   | MB3000EBKAB        | 3 TB   | 2       | 1447  | 0     | 3.97   |
| WDC       | WD1200JD-00HBB0    | 120 GB | 8       | 1895  | 162   | 3.97   |
| Toshiba   | MK1002TSKB         | 1 TB   | 1       | 1446  | 0     | 3.96   |
| Hitachi   | HUA723020ALA640    | 2 TB   | 23      | 1444  | 0     | 3.96   |
| WDC       | WD5003ABYX-18WERA0 | 500 GB | 3       | 1429  | 0     | 3.92   |
| WDC       | WD1002FBYS-02A6B0  | 1 TB   | 15      | 1670  | 2     | 3.91   |
| Seagate   | ST3500641AS        | 500 GB | 4       | 2192  | 37    | 3.91   |
| HGST      | HDN726050ALE610    | 5 TB   | 1       | 1409  | 0     | 3.86   |
| Hitachi   | HDT722520DLAT80    | 200 GB | 2       | 1406  | 0     | 3.85   |
| WDC       | WD5001FZWX-00ZHUA0 | 5 TB   | 4       | 1606  | 1     | 3.85   |
| WDC       | WD2500JB-22REA0    | 250 GB | 1       | 1398  | 0     | 3.83   |
| Seagate   | ST500LM024-1RS152  | 500 GB | 1       | 1394  | 0     | 3.82   |
| WDC       | WD1500HLFS-01G6U3  | 150 GB | 2       | 1388  | 0     | 3.80   |
| WDC       | WD2500AAJS-00VWA0  | 250 GB | 2       | 1384  | 0     | 3.79   |
| WDC       | WD1002FBYS-50A6B0  | 1 TB   | 1       | 1374  | 0     | 3.77   |
| Seagate   | ST3400832AS        | 400 GB | 2       | 2510  | 1     | 3.75   |
| Hitachi   | HDS724040ALE640    | 4 TB   | 4       | 1544  | 341   | 3.74   |
| Seagate   | ST6000DM001-1XY17Z | 6 TB   | 3       | 1357  | 0     | 3.72   |
| WDC       | WD20EARS-07MVWB0   | 2 TB   | 4       | 1865  | 1     | 3.71   |
| Maxtor    | 6N040T0            | 40 GB  | 1       | 2684  | 1     | 3.68   |
| Hitachi   | HUA723020ALA640... | 2 TB   | 1       | 1337  | 0     | 3.66   |
| WDC       | WD2500AAKX-19U6AA0 | 250 GB | 1       | 1334  | 0     | 3.66   |
| Hitachi   | HUA723030ALA640    | 3 TB   | 16      | 1407  | 1     | 3.64   |
| WDC       | WD5000BTKT-40MD3T0 | 500 GB | 2       | 1326  | 0     | 3.63   |
| WDC       | WD20EARX-00ZUDB0   | 2 TB   | 3       | 1681  | 2     | 3.61   |
| Fujitsu   | MPE3064AT          | 6 GB   | 2       | 1315  | 0     | 3.60   |
| Hitachi   | HDS722516VLSA80    | 164 GB | 4       | 1529  | 2     | 3.60   |
| WDC       | WD2500AAKX-08ERMA0 | 250 GB | 1       | 1306  | 0     | 3.58   |
| WDC       | WD2500AAKS-22VSA0  | 250 GB | 1       | 1305  | 0     | 3.58   |
| WDC       | WD1001FALS-00J7B0  | 1 TB   | 24      | 1658  | 2     | 3.57   |
| WDC       | WD2000F9YZ-09N20L0 | 2 TB   | 2       | 1303  | 0     | 3.57   |
| Hitachi   | HDS725050KLAT80    | 500 GB | 1       | 1303  | 0     | 3.57   |
| HGST      | HUS724040ALA640    | 4 TB   | 21      | 1336  | 97    | 3.57   |
| Hitachi   | HTS545050B9SA02    | 500 GB | 1       | 1295  | 0     | 3.55   |
| WDC       | WD6401AALS-00E8B0  | 640 GB | 3       | 1289  | 0     | 3.53   |
| Toshiba   | MQ01UBD075         | 752 GB | 1       | 1287  | 0     | 3.53   |
| WDC       | WD10EADS-65M2B0    | 1 TB   | 7       | 1585  | 4     | 3.52   |
| WDC       | WD1200BB-00GUA0    | 120 GB | 1       | 1284  | 0     | 3.52   |
| WDC       | WD3000F9YZ-09N20L0 | 3 TB   | 4       | 1902  | 2     | 3.52   |
| WDC       | WD1001FALS-75J7B0  | 1 TB   | 2       | 1485  | 4     | 3.52   |
| WDC       | WD2000BB-22GUC0    | 200 GB | 1       | 1282  | 0     | 3.51   |
| Hitachi   | HDS5C3015ALA632    | 1.5 TB | 3       | 1462  | 107   | 3.51   |
| WDC       | WD4000AAKS-00A7B0  | 400 GB | 1       | 1280  | 0     | 3.51   |
| WDC       | WD3000FYYZ-50UL1B0 | 3 TB   | 1       | 1278  | 0     | 3.50   |
| WDC       | WD15EVDS-68V9B0    | 1.5 TB | 1       | 1276  | 0     | 3.50   |
| HP        | J7989G             | 80 GB  | 1       | 1274  | 0     | 3.49   |
| WDC       | WD1000DHTZ-04N21V1 | 1 TB   | 2       | 1270  | 0     | 3.48   |
| WDC       | WD3200AAJS-65M0A0  | 320 GB | 3       | 1728  | 4     | 3.46   |
| HGST      | HUP723020APA640    | 2 TB   | 1       | 1257  | 0     | 3.45   |
| Hitachi   | HTS421212H9AT00    | 120 GB | 2       | 2184  | 120   | 3.43   |
| HGST      | HDN724030ALE640    | 3 TB   | 12      | 1241  | 0     | 3.40   |
| HGST      | HUS724020ALA640    | 2 TB   | 34      | 1237  | 0     | 3.39   |
| HGST      | HUS724030ALA640    | 3 TB   | 13      | 1343  | 2     | 3.39   |
| Samsung   | SP0451N            | 40 GB  | 1       | 1237  | 0     | 3.39   |
| Hitachi   | HDT721075SLA360    | 752 GB | 2       | 1234  | 0     | 3.38   |
| WDC       | WD5000AAKS-65V0A0  | 500 GB | 5       | 1511  | 4     | 3.38   |
| WDC       | WD2500HHTZ-04N21V1 | 250 GB | 2       | 1226  | 0     | 3.36   |
| WDC       | WD800JD-55MSA1     | 80 GB  | 4       | 1226  | 0     | 3.36   |
| WDC       | WD4000AAJS-32TKA0  | 400 GB | 1       | 1226  | 0     | 3.36   |
| WDC       | WD15EADS-11P8B2    | 1.5 TB | 1       | 1224  | 0     | 3.35   |
| Hitachi   | HDS722020ALA330    | 2 TB   | 33      | 1715  | 107   | 3.33   |
| Seagate   | ST310211A          | 10 GB  | 2       | 1214  | 0     | 3.33   |
| Seagate   | ST8000AS0002-1N... | 8 TB   | 85      | 1352  | 50    | 3.32   |
| WDC       | WD800JD-60LUA0     | 80 GB  | 2       | 1210  | 0     | 3.32   |
| Hitachi   | HDS721075KLA330    | 752 GB | 7       | 1493  | 14    | 3.31   |
| Fujitsu   | MHZ2250BJ FFS G2   | 250 GB | 1       | 1207  | 0     | 3.31   |
| Hitachi   | HDT721075SLA380    | 752 GB | 1       | 1205  | 0     | 3.30   |
| Seagate   | ST3160828AS        | 160 GB | 1       | 1198  | 0     | 3.28   |
| Hitachi   | HUS724040ALE640    | 4 TB   | 2       | 1195  | 0     | 3.28   |
| WDC       | WD5000AAKS-00TMA0  | 500 GB | 8       | 1301  | 2     | 3.27   |
| Seagate   | ST3300622AS        | 304 GB | 3       | 1735  | 1     | 3.25   |
| WDC       | WD5000AAJS-32YFA0  | 500 GB | 1       | 1187  | 0     | 3.25   |
| Seagate   | ST3300631A         | 304 GB | 1       | 1185  | 0     | 3.25   |
| Seagate   | ST9250610NS        | 250 GB | 5       | 1180  | 0     | 3.23   |
| WDC       | WD1600AABS-56PRA0  | 160 GB | 3       | 1178  | 0     | 3.23   |
| Hitachi   | HDS728040PLA320    | 40 GB  | 4       | 1548  | 4     | 3.22   |
| WDC       | WD1001FALS-40U9B0  | 1 TB   | 1       | 1175  | 0     | 3.22   |
| WDC       | WD4000AAKS-00YGA0  | 400 GB | 6       | 1245  | 1     | 3.21   |
| WDC       | WD3200AAJB-56WGA0  | 320 GB | 3       | 1172  | 0     | 3.21   |
| WDC       | WD800BB-60JKC0     | 80 GB  | 2       | 1292  | 2     | 3.21   |
| WDC       | WD3000HLFS-01G6U3  | 304 GB | 1       | 1170  | 0     | 3.21   |
| WDC       | WD3200AAKS-75B3A0  | 320 GB | 1       | 2338  | 1     | 3.20   |
| Seagate   | ST3320620NS        | 320 GB | 3       | 1312  | 1     | 3.20   |
| WDC       | WD3200AAJS-07RYA0  | 320 GB | 1       | 1168  | 0     | 3.20   |
| WDC       | WD20EADS-00S2B0    | 2 TB   | 4       | 1203  | 1     | 3.20   |
| WDC       | WD3200AAKS-75SBA0  | 320 GB | 3       | 1168  | 0     | 3.20   |
| WDC       | WD800HLFS-75G6U1   | 80 GB  | 1       | 1168  | 0     | 3.20   |
| WDC       | WD1500AHFD-00RAR5  | 150 GB | 1       | 1164  | 0     | 3.19   |
| WDC       | WD5000AVJB-63YUA0  | 500 GB | 1       | 1163  | 0     | 3.19   |
| Toshiba   | MK8017GSG          | 80 GB  | 1       | 1162  | 0     | 3.18   |
| Hitachi   | HDS721010CLA630    | 1 TB   | 9       | 1214  | 1     | 3.18   |
| WDC       | WD5000AAKS-402AA0  | 500 GB | 4       | 1784  | 14    | 3.17   |
| WDC       | WD1001FALS-41Y6A0  | 1 TB   | 3       | 1345  | 1     | 3.17   |
| WDC       | WD2500JB-00GVA0    | 250 GB | 1       | 1155  | 0     | 3.16   |
| WDC       | WD2503ABYX-01WERA0 | 256 GB | 1       | 1155  | 0     | 3.16   |
| HGST      | HDN724040ALE640    | 4 TB   | 16      | 1154  | 0     | 3.16   |
| WDC       | WD5000AAKS-40V6A0  | 500 GB | 2       | 1149  | 0     | 3.15   |
| Fujitsu   | MHV2040BH          | 40 GB  | 2       | 1146  | 0     | 3.14   |
| WDC       | WD10EAVS-00M4B0    | 1 TB   | 1       | 1145  | 0     | 3.14   |
| WDC       | WD5000AAVS-00G9B0  | 500 GB | 6       | 1355  | 2     | 3.12   |
| WDC       | WD10EACS-00ZJB0    | 1 TB   | 10      | 1592  | 68    | 3.12   |
| WDC       | WD740ADFD-00NLR1   | 74 GB  | 2       | 1137  | 0     | 3.12   |
| WDC       | WD5003AZEX-00RKKA0 | 500 GB | 2       | 1135  | 0     | 3.11   |
| Hitachi   | HDS723030BLE640    | 3 TB   | 1       | 1135  | 0     | 3.11   |
| WDC       | MB0500EBNCR        | 500 GB | 1       | 1134  | 0     | 3.11   |
| WDC       | WD50EZRZ-32RWYB1   | 5 TB   | 2       | 1128  | 0     | 3.09   |
| Seagate   | ST4000VN0001-1S... | 4 TB   | 3       | 1128  | 0     | 3.09   |
| Samsung   | HD400LD            | 400 GB | 4       | 1126  | 0     | 3.09   |
| Seagate   | ST250DM001 HD256GJ | 250 GB | 1       | 1123  | 0     | 3.08   |
| WDC       | WD4000F9YZ-09N20L1 | 4 TB   | 3       | 1122  | 0     | 3.08   |
| WDC       | WD2002FYPS-01U1B0  | 2 TB   | 3       | 2771  | 137   | 3.07   |
| WDC       | WD6400AAKS-65A7B0  | 640 GB | 9       | 1174  | 2     | 3.07   |
| WDC       | WD10EADS-00L5B1    | 1 TB   | 62      | 1702  | 7     | 3.07   |
| WDC       | WD3200AAJS-40VWA0  | 320 GB | 1       | 1118  | 0     | 3.06   |
| WDC       | WD5000AACS-00ZUB0  | 500 GB | 11      | 1151  | 1     | 3.06   |
| Hitachi   | HCP725025GLA380    | 250 GB | 1       | 1111  | 0     | 3.04   |
| Seagate   | ST3300831AS        | 304 GB | 4       | 1804  | 3     | 3.04   |
| WDC       | WD1200BEVE-00WZT0  | 120 GB | 1       | 1103  | 0     | 3.02   |
| Hitachi   | HDS7250SASUN500... | 500 GB | 1       | 1103  | 0     | 3.02   |
| WDC       | WD800JD-08LSA0     | 80 GB  | 10      | 1230  | 2     | 3.02   |
| Seagate   | ST3000DM001-1E6166 | 3 TB   | 5       | 1394  | 816   | 3.02   |
| WDC       | WD10EARS-67Y5B1    | 1 TB   | 1       | 1100  | 0     | 3.01   |
| Seagate   | ST6000AS0002-1N... | 6 TB   | 11      | 1573  | 73    | 3.00   |
| WDC       | WD2002FAEX-00MJRA0 | 2 TB   | 1       | 1094  | 0     | 3.00   |
| WDC       | WD2500JS-00MHB0    | 250 GB | 5       | 1155  | 1     | 2.99   |
| WDC       | WD1200JS-00SGB0    | 120 GB | 2       | 1091  | 0     | 2.99   |
| WDC       | WD1600YS-01SHB1    | 164 GB | 7       | 1088  | 0     | 2.98   |
| WDC       | WD10EADS-00P8B0    | 1 TB   | 7       | 1278  | 2     | 2.98   |
| WDC       | WD3200KS-75PFB0    | 320 GB | 2       | 1359  | 39    | 2.98   |
| Seagate   | ST9500620NS 81Y... | 500 GB | 1       | 1083  | 0     | 2.97   |
| WDC       | WD7500AARX-00N0YB0 | 752 GB | 1       | 1081  | 0     | 2.96   |
| WDC       | WD30EURX-64HYZY0   | 3 TB   | 1       | 1077  | 0     | 2.95   |
| Hitachi   | HDS723020BLA642    | 2 TB   | 51      | 1295  | 78    | 2.95   |
| Maxtor    | 7V250F0            | 256 GB | 2       | 1075  | 0     | 2.95   |
| WDC       | WD20EARX-22PASB0   | 2 TB   | 4       | 1075  | 0     | 2.95   |
| Seagate   | ST1000NX0423 00... | 1 TB   | 5       | 1073  | 0     | 2.94   |
| WDC       | WD3200AZKX-00D6NA0 | 320 GB | 1       | 1073  | 0     | 2.94   |
| Maxtor    | 6L020J1            | 20 GB  | 3       | 1213  | 2     | 2.93   |
| HGST      | HTS721050A9E630    | 500 GB | 1       | 1069  | 0     | 2.93   |
| WDC       | WD10EALX-759BA1    | 1 TB   | 8       | 1420  | 3     | 2.92   |
| Seagate   | ST1000NM0095-2D... | 1 TB   | 1       | 1059  | 0     | 2.90   |
| WDC       | WD6400AACS-00D6B1  | 640 GB | 1       | 1058  | 0     | 2.90   |
| WDC       | WD2500AAJS-75VWA0  | 250 GB | 3       | 1056  | 0     | 2.89   |
| Seagate   | ST6000VX0023-2E... | 6 TB   | 1       | 1055  | 0     | 2.89   |
| WDC       | WD2500JS-00MHB1    | 250 GB | 2       | 1052  | 0     | 2.88   |
| WDC       | WD3000BLFS-08YBU0  | 304 GB | 2       | 1048  | 0     | 2.87   |
| HGST      | MB6000GEBTP        | 6 TB   | 1       | 1046  | 0     | 2.87   |
| WDC       | WD1500HLFS-01G6U1  | 150 GB | 5       | 1046  | 0     | 2.87   |
| WDC       | WD3200JD-00KLB0    | 320 GB | 1       | 1045  | 0     | 2.87   |
| Seagate   | MM0500EBKAE        | 500 GB | 1       | 3112  | 2     | 2.84   |
| Apple     | HDD HTS727575A9... | 752 GB | 3       | 1036  | 0     | 2.84   |
| WDC       | WD10EAVS-00D7B0    | 1 TB   | 9       | 1208  | 1     | 2.84   |
| WDC       | WD800BB-75FRA0     | 80 GB  | 2       | 1034  | 0     | 2.83   |
| Seagate   | ST340823A          | 40 GB  | 1       | 1034  | 0     | 2.83   |
| Seagate   | ST32000641AS       | 2 TB   | 16      | 1377  | 178   | 2.83   |
| Toshiba   | DT01ABA100V        | 1 TB   | 1       | 1030  | 0     | 2.82   |
| WDC       | WD1600AVJS-63WNA0  | 160 GB | 1       | 1027  | 0     | 2.82   |
| WDC       | WD2002FAEX-007BA0  | 2 TB   | 34      | 1396  | 6     | 2.81   |
| WDC       | WD2003FYYS-05T9B0  | 2 TB   | 1       | 1025  | 0     | 2.81   |
| Hitachi   | HDT725040VLA360    | 400 GB | 2       | 1024  | 0     | 2.81   |
| WDC       | WD20EARX-008FB0    | 2 TB   | 12      | 1105  | 1     | 2.81   |
| WDC       | WD4NPURX-64TPFY0   | 4 TB   | 1       | 1023  | 0     | 2.80   |
| WDC       | WD2500JB-57REA0    | 250 GB | 1       | 1021  | 0     | 2.80   |
| Seagate   | ST4000VN000-1H4168 | 4 TB   | 19      | 1094  | 107   | 2.80   |
| WDC       | WD1600JS-55NCB1    | 160 GB | 6       | 1017  | 0     | 2.79   |
| HP        | GB0250EAFYK        | 250 GB | 2       | 1519  | 67    | 2.79   |
| WDC       | WD400LB-00DNA0     | 40 GB  | 2       | 1103  | 2     | 2.78   |
| WDC       | WD200BB-00DEA0     | 20 GB  | 1       | 1015  | 0     | 2.78   |
| WDC       | WD800JD-60LSA5     | 80 GB  | 21      | 1051  | 1     | 2.78   |
| WDC       | WD6002FRYZ-01WD5B1 | 6 TB   | 2       | 1014  | 0     | 2.78   |
| WDC       | WD5000AACS-61M6B2  | 500 GB | 3       | 2013  | 4     | 2.78   |
| WDC       | WD1600JB-00EVA0    | 160 GB | 1       | 1012  | 0     | 2.77   |
| Toshiba   | MC04ACA200E        | 2 TB   | 1       | 1008  | 0     | 2.76   |
| Seagate   | ST320LT023-1AF142  | 320 GB | 1       | 1007  | 0     | 2.76   |
| WDC       | WD1001FALS-00J7B1  | 1 TB   | 23      | 1363  | 3     | 2.76   |
| WDC       | WD7500AAKS-00RBA0  | 752 GB | 10      | 1401  | 51    | 2.76   |
| WDC       | WD3200AAKS-00G3A0  | 320 GB | 6       | 1006  | 0     | 2.76   |
| WDC       | WD20NMVW-59AV3S3   | 2 TB   | 1       | 1005  | 0     | 2.75   |
| WDC       | WD1600AABS-61PRA0  | 160 GB | 3       | 1341  | 1     | 2.75   |
| Samsung   | HD204UI            | 2 TB   | 52      | 1203  | 98    | 2.75   |
| WDC       | WD2000JS-22MHB0    | 200 GB | 4       | 1909  | 10    | 2.74   |
| Hitachi   | HDT725032VLA380    | 320 GB | 14      | 1519  | 89    | 2.74   |
| Hitachi   | HDT725025VLA380    | 250 GB | 21      | 1241  | 25    | 2.73   |
| WDC       | WD2500JS-60NCB1    | 250 GB | 8       | 1084  | 1     | 2.73   |
| Seagate   | ST3400833AS        | 400 GB | 2       | 995   | 0     | 2.73   |
| HGST      | HMS5C4040BLE640    | 4 TB   | 9       | 990   | 0     | 2.71   |
| Hitachi   | HDS5C3020ALA632    | 2 TB   | 16      | 1096  | 2     | 2.71   |
| WDC       | WD1000FYPS-01ZKB0  | 1 TB   | 1       | 989   | 0     | 2.71   |
| Hitachi   | HDS721010CLA632    | 1 TB   | 6       | 1224  | 9     | 2.71   |
| WDC       | WD5000AAKS-00C8A0  | 500 GB | 3       | 1253  | 62    | 2.70   |
| WDC       | WD10JPVT-16A1YT0   | 1 TB   | 3       | 984   | 0     | 2.70   |
| HGST      | HUS724030ALE640    | 3 TB   | 1       | 983   | 0     | 2.69   |
| WDC       | WD3200AAKX-221CA0  | 320 GB | 1       | 981   | 0     | 2.69   |
| Hitachi   | HUA722050CLA330    | 500 GB | 3       | 980   | 0     | 2.69   |
| WDC       | WD400JB-00JJC0     | 40 GB  | 1       | 980   | 0     | 2.69   |
| Samsung   | HD040GJ-P          | 40 GB  | 1       | 975   | 0     | 2.67   |
| HP        | MB2000EBZQC        | 2 TB   | 3       | 974   | 0     | 2.67   |
| Seagate   | ST3402111AS        | 40 GB  | 1       | 969   | 0     | 2.66   |
| WDC       | WD10EALX-079BA1    | 1 TB   | 1       | 968   | 0     | 2.65   |
| WDC       | WD2500AAJS-75M0A0  | 250 GB | 10      | 1090  | 1     | 2.65   |
| Seagate   | ST2000DM001-1E6164 | 2 TB   | 6       | 967   | 0     | 2.65   |
| Toshiba   | MK1229GSGF         | 80 GB  | 1       | 6753  | 6     | 2.64   |
| HGST      | HMS5C4040ALE640    | 4 TB   | 6       | 961   | 0     | 2.63   |
| Toshiba   | MK4032GAX          | 40 GB  | 1       | 960   | 0     | 2.63   |
| WDC       | WD2000JS-00MVB1    | 200 GB | 1       | 957   | 0     | 2.62   |
| WDC       | WD20EZRX-07D8PB0   | 2 TB   | 1       | 957   | 0     | 2.62   |
| WDC       | WD7502AAEX-00Z3A0  | 752 GB | 1       | 956   | 0     | 2.62   |
| WDC       | WD5000AAKS-22YGA0  | 500 GB | 4       | 1326  | 115   | 2.62   |
| Toshiba   | MQ01UBB200         | 2 TB   | 4       | 952   | 0     | 2.61   |
| WDC       | WD5000BMVV-11GNWS0 | 500 GB | 5       | 1118  | 15    | 2.61   |
| WDC       | WD15EARS-00S8B1    | 1.5 TB | 6       | 1885  | 3     | 2.61   |
| WDC       | WD1600BB-22RDA0    | 160 GB | 2       | 947   | 0     | 2.60   |
| Quantum   | FIREBALLP AS20.5   | 20 GB  | 1       | 946   | 0     | 2.59   |
| WDC       | WD2500JD-00GBB0    | 250 GB | 1       | 944   | 0     | 2.59   |
| WDC       | WD2003FZEX-00Z4SA0 | 2 TB   | 28      | 1010  | 2     | 2.59   |
| WDC       | WD6400AACS-00G8B0  | 640 GB | 4       | 1143  | 147   | 2.58   |
| WDC       | WD2001FASS-00W2B0  | 2 TB   | 3       | 940   | 0     | 2.58   |
| WDC       | WD1001FALS-41Y6A1  | 1 TB   | 1       | 938   | 0     | 2.57   |
| WDC       | WD5000AAKB-00YSA0  | 500 GB | 2       | 935   | 0     | 2.56   |
| WDC       | WD5000LUCT-63C26Y0 | 500 GB | 1       | 934   | 0     | 2.56   |
| Seagate   | ST4000DM000-1F2168 | 4 TB   | 106     | 1060  | 67    | 2.56   |
| Seagate   | ST1000NM0011 43... | 1 TB   | 1       | 925   | 0     | 2.53   |
| WDC       | WD1600JS-55MHB1    | 160 GB | 3       | 924   | 0     | 2.53   |
| WDC       | WD800JB-00DUA3     | 80 GB  | 1       | 923   | 0     | 2.53   |
| WDC       | WD6401AALS-00L3B2  | 640 GB | 22      | 1189  | 5     | 2.53   |
| Toshiba   | DT01ABA200         | 2 TB   | 10      | 971   | 2     | 2.52   |
| Seagate   | ST3500630A         | 500 GB | 9       | 1489  | 26    | 2.52   |
| WDC       | WD6400AAKS-65A7B2  | 640 GB | 17      | 1368  | 29    | 2.52   |
| WDC       | WD1600JB-00REA0    | 160 GB | 9       | 1094  | 133   | 2.52   |
| WDC       | WD1600BB-56RDA0    | 160 GB | 2       | 916   | 0     | 2.51   |
| WDC       | WD3200AAKX-603CA0  | 320 GB | 1       | 914   | 0     | 2.51   |
| HGST      | HTS725025A7E630    | 250 GB | 1       | 914   | 0     | 2.51   |
| Seagate   | ST3300622A         | 304 GB | 1       | 912   | 0     | 2.50   |
| WDC       | WD30EZRX-00DC0B0   | 3 TB   | 42      | 1131  | 46    | 2.50   |
| WDC       | WD40EZRX-00SPEB0   | 4 TB   | 34      | 970   | 2     | 2.50   |
| Seagate   | ST3000DM003-1F216N | 3 TB   | 2       | 910   | 0     | 2.49   |
| Seagate   | ST91000640NS 81... | 1 TB   | 1       | 909   | 0     | 2.49   |
| WDC       | WD15EARS-00J2GB0   | 1.5 TB | 1       | 908   | 0     | 2.49   |
| WDC       | WD10EUCX-73YZ1Y0   | 1 TB   | 1       | 907   | 0     | 2.49   |
| WDC       | WD2500JS-60NCB2    | 250 GB | 3       | 903   | 0     | 2.47   |
| WDC       | WD1600BB-00RDA0    | 160 GB | 4       | 1124  | 20    | 2.47   |
| WDC       | WD800BEVS-08RST3   | 80 GB  | 1       | 900   | 0     | 2.47   |
| WDC       | WD400BB-71DGA0     | 40 GB  | 1       | 900   | 0     | 2.47   |
| WDC       | WD10EADS-00M2B0    | 1 TB   | 47      | 1212  | 77    | 2.47   |
| WDC       | WD30EZRX-00AZ6B0   | 3 TB   | 3       | 950   | 83    | 2.46   |
| WDC       | WD20NMVW-11W68S0   | 2 TB   | 4       | 1004  | 15    | 2.46   |
| WDC       | WD3200AAJS-40VWA1  | 320 GB | 3       | 1018  | 14    | 2.46   |
| WDC       | WD5000AAKX-603CA0  | 500 GB | 21      | 943   | 110   | 2.45   |
| WDC       | WD1002FAEX-00Z3A0  | 1 TB   | 91      | 1150  | 63    | 2.45   |
| WDC       | WD1001FALS-00Y6A0  | 1 TB   | 5       | 1092  | 22    | 2.45   |
| WDC       | WD6400AAKS-00A7B0  | 640 GB | 16      | 1053  | 4     | 2.44   |
| WDC       | WD10EACS-00D6B0    | 1 TB   | 10      | 1553  | 17    | 2.44   |
| WDC       | WD30EZRX-00SPEB0   | 3 TB   | 15      | 1044  | 18    | 2.44   |
| Hitachi   | HUS724030ALA640    | 3 TB   | 1       | 889   | 0     | 2.44   |
| WDC       | WD30EZRX-00MMMB0   | 3 TB   | 27      | 1061  | 45    | 2.44   |
| Hitachi   | HDS721016CLA382    | 160 GB | 8       | 1060  | 1     | 2.43   |
| WDC       | WD800BB-22HEA1     | 80 GB  | 1       | 888   | 0     | 2.43   |
| HGST      | HTE541010A9E680    | 1 TB   | 2       | 913   | 509   | 2.43   |
| WDC       | WD2500AAJS-55RYA0  | 250 GB | 2       | 887   | 0     | 2.43   |
| WDC       | WD3200AAJB-00TYA0  | 320 GB | 4       | 885   | 0     | 2.43   |
| Maxtor    | STM380215A         | 80 GB  | 6       | 1208  | 312   | 2.42   |
| WDC       | WD4000KS-00MNB0    | 400 GB | 3       | 883   | 0     | 2.42   |
| Seagate   | ST91000640NS 81... | 1 TB   | 1       | 883   | 0     | 2.42   |
| WDC       | WD5000AAKS-00YGA0  | 500 GB | 23      | 1119  | 3     | 2.42   |
| WDC       | WD1600AAJS-75WAA0  | 160 GB | 2       | 880   | 0     | 2.41   |
| Hitachi   | HDS5C4040ALE630    | 4 TB   | 2       | 879   | 0     | 2.41   |
| Samsung   | HD162GJ            | 160 GB | 1       | 878   | 0     | 2.41   |
| Maxtor    | 6V300F0            | 304 GB | 2       | 876   | 0     | 2.40   |
| Hitachi   | HDT722520DLA380    | 200 GB | 4       | 1091  | 2     | 2.40   |
| WDC       | WD30EZRS-42KEZB0   | 3 TB   | 1       | 874   | 0     | 2.40   |
| Samsung   | HD300LJ            | 304 GB | 11      | 1285  | 311   | 2.39   |
| Toshiba   | MQ01ABF050H        | 500 GB | 2       | 873   | 0     | 2.39   |
| Seagate   | ST3500630AS        | 500 GB | 48      | 1321  | 234   | 2.39   |
| WDC       | WD4000FYYZ-01UL1B3 | 4 TB   | 1       | 869   | 0     | 2.38   |
| WDC       | WD6400AAKS-75A7B2  | 640 GB | 6       | 1034  | 5     | 2.37   |
| WDC       | WD800BB-75JHA0     | 80 GB  | 1       | 865   | 0     | 2.37   |
| Seagate   | ST3250620NS        | 250 GB | 18      | 1339  | 273   | 2.37   |
| WDC       | WD5000AAKS-07YGA0  | 500 GB | 4       | 864   | 0     | 2.37   |
| WDC       | WD6400AAVS-00G9B1  | 640 GB | 3       | 1491  | 96    | 2.37   |
| WDC       | WD5000BPVT-24HXZT1 | 500 GB | 1       | 863   | 0     | 2.37   |
| HP        | MB1000EBZQB        | 1 TB   | 1       | 863   | 0     | 2.37   |
| WDC       | WD10EARS-003BB1    | 1 TB   | 14      | 992   | 123   | 2.36   |
| Seagate   | ST10000DM0004      | 10 TB  | 1       | 862   | 0     | 2.36   |
| WDC       | WD3202ABYS-02B7A0  | 320 GB | 6       | 929   | 1     | 2.36   |
| WDC       | WD5002ABYS-02B1B0  | 500 GB | 10      | 1229  | 3     | 2.36   |
| Seagate   | ST3160215ACE       | 160 GB | 4       | 1078  | 54    | 2.35   |
| Seagate   | ST3250823AS        | 250 GB | 16      | 1571  | 19    | 2.35   |
| Seagate   | ST1000LX001-1EM164 | 1 TB   | 1       | 857   | 0     | 2.35   |
| WDC       | WD1003FBYX-01Y7B0  | 1 TB   | 14      | 1511  | 154   | 2.34   |
| WDC       | WD800AAJS-22PSA0   | 80 GB  | 4       | 852   | 0     | 2.33   |
| Seagate   | ST3802110AS        | 80 GB  | 3       | 851   | 0     | 2.33   |
| WDC       | WD50EZRX-00MVLB1   | 5 TB   | 3       | 851   | 0     | 2.33   |
| WDC       | WD10EZEX-08RKKA0   | 1 TB   | 6       | 848   | 0     | 2.32   |
| WDC       | WD800JD-75MSA3     | 80 GB  | 29      | 1009  | 1     | 2.32   |
| Hitachi   | HCC547550A9E380    | 500 GB | 1       | 844   | 0     | 2.31   |
| WDC       | WD800JD-75JNA0     | 80 GB  | 4       | 1531  | 30    | 2.31   |
| Seagate   | ST32000644NS       | 2 TB   | 14      | 1196  | 161   | 2.31   |
| WDC       | WD10EFRX-68JCSN0   | 1 TB   | 25      | 1052  | 159   | 2.30   |
| WDC       | WD10JMVW-59AJGS3   | 1 TB   | 2       | 840   | 0     | 2.30   |
| Seagate   | ST32000645NS       | 2 TB   | 8       | 1309  | 11    | 2.30   |
| WDC       | WD10EURX-63UY4Y0   | 1 TB   | 5       | 839   | 0     | 2.30   |
| Seagate   | ST3250820SCE       | 250 GB | 4       | 849   | 2     | 2.30   |
| WDC       | WD10EALX-089BA0    | 1 TB   | 2       | 836   | 0     | 2.29   |
| Hitachi   | HTS722020K9SA00... | 200 GB | 1       | 835   | 0     | 2.29   |
| WDC       | WD2502ABYS-18B7A0  | 250 GB | 4       | 1251  | 3     | 2.29   |
| Toshiba   | MK2561GSY          | 250 GB | 1       | 834   | 0     | 2.29   |
| WDC       | WD2000FYYZ-01UL1B2 | 2 TB   | 4       | 984   | 1     | 2.28   |
| WDC       | WD5000AAKS-00A7B0  | 500 GB | 34      | 1231  | 27    | 2.28   |
| WDC       | WD1600JS-60MHB1    | 160 GB | 7       | 974   | 4     | 2.28   |
| Seagate   | ST1000DX001-1NS... | 1 TB   | 2       | 830   | 0     | 2.27   |
| WDC       | WD80EFAX-68LHPN0   | 8 TB   | 15      | 829   | 0     | 2.27   |
| Seagate   | ST3750840AS        | 752 GB | 1       | 828   | 0     | 2.27   |
| Toshiba   | MK2546GSX_200      | 200 GB | 1       | 827   | 0     | 2.27   |
| Toshiba   | MD04ACA400         | 4 TB   | 10      | 1004  | 401   | 2.26   |
| WDC       | WD10TMVW-11ZSMS5   | 1 TB   | 8       | 945   | 231   | 2.26   |
| WDC       | WD400BB-00DEA0     | 40 GB  | 1       | 825   | 0     | 2.26   |
| WDC       | WD800BD-88JMC0     | 80 GB  | 2       | 824   | 0     | 2.26   |
| WDC       | WD1003FZEX-00RLFA0 | 1 TB   | 2       | 823   | 0     | 2.26   |
| Hitachi   | HDS5C3030BLE630    | 3 TB   | 3       | 823   | 0     | 2.26   |
| WDC       | WD15EARS-60MVWB0   | 1.5 TB | 2       | 1094  | 31    | 2.25   |
| Hitachi   | HDS728040PLAT20    | 41 GB  | 5       | 979   | 1     | 2.25   |
| WDC       | WD1600JB-00GVA0    | 160 GB | 1       | 822   | 0     | 2.25   |
| Hitachi   | HDT725050VLA380    | 500 GB | 4       | 1315  | 11    | 2.25   |
| WDC       | WD1001FALS-00E3A0  | 1 TB   | 7       | 1386  | 236   | 2.25   |
| WDC       | WD1002FAEX-00Y9A0  | 1 TB   | 47      | 1024  | 17    | 2.24   |
| WDC       | WD2500BEVE-00WZT0  | 250 GB | 2       | 817   | 0     | 2.24   |
| WDC       | WD400BB-00LNA0     | 40 GB  | 1       | 817   | 0     | 2.24   |
| WDC       | WD2500AAJS-08L7A0  | 250 GB | 5       | 816   | 0     | 2.24   |
| WDC       | WD2500JS-55NCB1    | 250 GB | 7       | 1114  | 13    | 2.23   |
| HP        | GB1000EAMYC        | 1 TB   | 2       | 814   | 0     | 2.23   |
| WDC       | WD20EARX-00PASB0   | 2 TB   | 128     | 1091  | 105   | 2.23   |
| WDC       | WD3200AAJS-56B4A0  | 320 GB | 5       | 1152  | 2     | 2.23   |
| WDC       | WD30EFRX-68EUZN0   | 3 TB   | 122     | 1017  | 8     | 2.22   |
| WDC       | WD2500JB-00GVC0    | 250 GB | 2       | 811   | 0     | 2.22   |
| HGST      | HUS726040ALA610    | 4 TB   | 2       | 810   | 0     | 2.22   |
| WDC       | WD5003ABYX-01WERA2 | 500 GB | 1       | 810   | 0     | 2.22   |
| HGST      | HCC725050A7E630    | 500 GB | 1       | 810   | 0     | 2.22   |
| WDC       | WD2500JS-75NCB3    | 250 GB | 5       | 1046  | 20    | 2.22   |
| HP        | VB0250EAVER        | 250 GB | 15      | 1182  | 4     | 2.21   |
| Seagate   | ST3120213AS        | 120 GB | 1       | 806   | 0     | 2.21   |
| Hitachi   | HDS5C1010CLA382    | 1 TB   | 10      | 975   | 24    | 2.21   |
| Hitachi   | HTS723232L9SA62    | 320 GB | 1       | 804   | 0     | 2.20   |
| HGST      | HDN726060ALE610    | 6 TB   | 15      | 867   | 45    | 2.20   |
| Seagate   | ST4000DX002-1H2178 | 4 TB   | 2       | 801   | 0     | 2.20   |
| WDC       | WD8001FFWX-68J1UN0 | 8 TB   | 3       | 799   | 0     | 2.19   |
| WDC       | WD1502FAEX-007BA0  | 1.5 TB | 7       | 872   | 25    | 2.19   |
| Hitachi   | HUA722020ALA330... | 2 TB   | 1       | 797   | 0     | 2.18   |
| WDC       | WD1600JS-75NCB3    | 160 GB | 4       | 797   | 0     | 2.18   |
| WDC       | WD3200AAKS-22B3A0  | 320 GB | 2       | 797   | 0     | 2.18   |
| Seagate   | ST1500LM003-9YH148 | 1.5 TB | 1       | 796   | 0     | 2.18   |
| Fujitsu   | MHV2060AH PL       | 64 GB  | 2       | 796   | 0     | 2.18   |
| HGST      | HUS726020ALE614    | 2 TB   | 3       | 796   | 0     | 2.18   |
| Seagate   | ST3320633AS        | 320 GB | 1       | 795   | 0     | 2.18   |
| WDC       | WD5000AAVS-00ZTB0  | 500 GB | 9       | 1019  | 166   | 2.18   |
| Seagate   | ST1000VM002-1ET162 | 1 TB   | 5       | 793   | 0     | 2.17   |
| Apple     | HDD HTS541075A9... | 752 GB | 1       | 792   | 0     | 2.17   |
| WDC       | WD800AAJS-60PSA0   | 80 GB  | 3       | 1000  | 336   | 2.17   |
| WDC       | WD5000AAJS-22TKA0  | 500 GB | 3       | 790   | 0     | 2.17   |
| WDC       | WD1005FBYZ-01YCBB1 | 1 TB   | 4       | 790   | 0     | 2.17   |
| WDC       | WD7500AALX-009BA0  | 752 GB | 7       | 789   | 0     | 2.16   |
| Seagate   | ST3400620A         | 400 GB | 4       | 1479  | 143   | 2.16   |
| Seagate   | ST380012A          | 80 GB  | 2       | 787   | 0     | 2.16   |
| WDC       | WD5000BPKX-75HPJT0 | 500 GB | 2       | 787   | 0     | 2.16   |
| HP        | MB1000ECWCQ        | 1 TB   | 1       | 787   | 0     | 2.16   |
| WDC       | WD1600AAJB-00WRA0  | 160 GB | 3       | 1002  | 362   | 2.15   |
| Seagate   | ST3000DM001-1ER166 | 3 TB   | 60      | 832   | 102   | 2.15   |
| WDC       | WD1600AAJS-07WAA0  | 160 GB | 5       | 1143  | 170   | 2.15   |
| WDC       | WD1002FAEX-007BA0  | 1 TB   | 3       | 853   | 1     | 2.15   |
| Seagate   | ST6000VN0021-1Z... | 6 TB   | 1       | 783   | 0     | 2.15   |
| WDC       | WD6001FFWX-68Z39N0 | 6 TB   | 1       | 782   | 0     | 2.14   |
| WDC       | WD5000AADS-56S9B0  | 500 GB | 1       | 782   | 0     | 2.14   |
| WDC       | WD7501AALS-00J7B1  | 752 GB | 9       | 976   | 1     | 2.14   |
| WDC       | WD80EFZX-68UW8N0   | 8 TB   | 15      | 781   | 0     | 2.14   |
| Seagate   | ST91603110CS       | 160 GB | 1       | 781   | 0     | 2.14   |
| Hitachi   | HDS723020BLE640    | 2 TB   | 10      | 780   | 0     | 2.14   |
| WDC       | WD10EURX-63FH1Y0   | 1 TB   | 5       | 778   | 0     | 2.13   |
| WDC       | WD1600AAJS-60PSA0  | 160 GB | 4       | 950   | 257   | 2.13   |
| Seagate   | ST10000NM0016-1... | 10 TB  | 9       | 777   | 0     | 2.13   |
| WDC       | WD400BD-75MRA1     | 40 GB  | 3       | 777   | 0     | 2.13   |
| WDC       | WD1500HLFS-50G6U1  | 150 GB | 1       | 776   | 0     | 2.13   |
| WDC       | WD1200JB-00DUA3    | 120 GB | 2       | 1239  | 2     | 2.13   |
| WDC       | WD5000AAJS-00A8B0  | 500 GB | 4       | 773   | 0     | 2.12   |
| WDC       | WD2500BB-00GUA0    | 250 GB | 1       | 773   | 0     | 2.12   |
| WDC       | WD1600BEVS-08VAT2  | 160 GB | 7       | 838   | 1     | 2.12   |
| WDC       | WD2500JS-00NCB1    | 250 GB | 10      | 1117  | 34    | 2.12   |
| WDC       | WD1600AAJS-22PSA0  | 160 GB | 16      | 940   | 31    | 2.12   |
| WDC       | WD40EFRX-68WT0N0   | 4 TB   | 90      | 1033  | 2     | 2.11   |
| Hitachi   | HTS723225L9A362    | 250 GB | 1       | 770   | 0     | 2.11   |
| WDC       | WD7501AALS-00J7B0  | 752 GB | 19      | 1028  | 47    | 2.11   |
| WDC       | WD1600AAJS-07PSA0  | 160 GB | 3       | 1618  | 9     | 2.10   |
| WDC       | WD7500BPVT-35HXZT1 | 752 GB | 1       | 766   | 0     | 2.10   |
| Toshiba   | MG03ACA300         | 3 TB   | 4       | 1368  | 10    | 2.10   |
| WDC       | WD5001ABYS-01YNA0  | 500 GB | 3       | 764   | 0     | 2.10   |
| WDC       | WD2500JS-22NCB1    | 250 GB | 11      | 1203  | 89    | 2.09   |
| Seagate   | ST3320620AS        | 320 GB | 135     | 1162  | 219   | 2.09   |
| Hitachi   | HDS721612PLA380    | 120 GB | 9       | 1157  | 2     | 2.09   |
| WDC       | WD1002FBYS-18W8B0  | 1 TB   | 2       | 762   | 0     | 2.09   |
| WDC       | WD7501AALS-00E8B0  | 752 GB | 4       | 1396  | 4     | 2.09   |
| WDC       | WD5003ABYZ-011FA0  | 500 GB | 12      | 838   | 4     | 2.09   |
| Samsung   | HD040GJ            | 40 GB  | 5       | 959   | 25    | 2.09   |
| WDC       | WD3003FZEX-00Z4SA0 | 3 TB   | 4       | 1180  | 254   | 2.09   |
| WDC       | WD2500YS-01SHB1    | 250 GB | 10      | 1149  | 13    | 2.08   |
| WDC       | WD2500JD-55HBB0    | 250 GB | 2       | 1468  | 16    | 2.07   |
| WDC       | WD5002ABYS-01B1B0  | 500 GB | 14      | 1330  | 4     | 2.06   |
| WDC       | WD5001AALS-00E3A0  | 500 GB | 13      | 991   | 93    | 2.06   |
| WDC       | WD3000JS-19PDB0    | 304 GB | 1       | 751   | 0     | 2.06   |
| Hitachi   | HTS545050B9A302    | 500 GB | 2       | 750   | 0     | 2.06   |
| WDC       | WD1001FALS-00U9B0  | 1 TB   | 3       | 1982  | 165   | 2.05   |
| WDC       | WD5000HHTZ-04N21V0 | 500 GB | 7       | 748   | 0     | 2.05   |
| Seagate   | ST3320413CS        | 320 GB | 11      | 799   | 104   | 2.05   |
| Seagate   | ST340212AS         | 40 GB  | 3       | 1192  | 70    | 2.05   |
| WDC       | WD7500AACS-00D6B1  | 752 GB | 5       | 1014  | 3     | 2.05   |
| WDC       | WD5000BEVT-75ZAT0  | 500 GB | 1       | 745   | 0     | 2.04   |
| HGST      | HDN728080ALE604    | 8 TB   | 1       | 745   | 0     | 2.04   |
| Quantum   | FIREBALLP AS40.0   | 40 GB  | 1       | 744   | 0     | 2.04   |
| WDC       | WD10EURX-61C57Y0   | 1 TB   | 1       | 744   | 0     | 2.04   |
| Hitachi   | HDS5C3020BLE630    | 2 TB   | 6       | 1030  | 48    | 2.04   |
| Hitachi   | HDS723015BLA642    | 1.5 TB | 9       | 911   | 22    | 2.03   |
| WDC       | WD2003FYYS-02W0B1  | 2 TB   | 7       | 1197  | 30    | 2.02   |
| WDC       | WD7500AADS-00M2B0  | 752 GB | 23      | 1178  | 17    | 2.02   |
| WDC       | WD20EARS-00S8B1    | 2 TB   | 12      | 1057  | 2     | 2.02   |
| WDC       | WD6400AAKS-65Z7B0  | 640 GB | 6       | 859   | 5     | 2.02   |
| Samsung   | HD103SJ            | 1 TB   | 148     | 967   | 13    | 2.02   |
| Seagate   | ST3000VN000-1HJ166 | 3 TB   | 7       | 734   | 0     | 2.01   |
| Seagate   | ST4000LM016-1N2170 | 4 TB   | 2       | 734   | 0     | 2.01   |
| WDC       | WD10EURX-63C57Y0   | 1 TB   | 6       | 993   | 1     | 2.01   |
| WDC       | WD2000F9YZ-09N20L1 | 2 TB   | 1       | 733   | 0     | 2.01   |
| WDC       | WD7500BPVT-80HXZT1 | 752 GB | 2       | 1049  | 3     | 2.01   |
| Hitachi   | HDS725050KLA360    | 500 GB | 8       | 1612  | 10    | 2.01   |
| Samsung   | HE103SJ            | 1 TB   | 3       | 2260  | 41    | 2.00   |
| WDC       | WD1200JB-00EVA0    | 120 GB | 4       | 731   | 0     | 2.00   |
| WDC       | WD1600AAJS-07M0A0  | 160 GB | 9       | 1213  | 3     | 2.00   |
| Seagate   | ST5000DM000-1FK178 | 5 TB   | 17      | 878   | 107   | 2.00   |
| WDC       | WD3200AAJS-07M0A0  | 320 GB | 4       | 846   | 2     | 2.00   |
| HGST      | HDN724020ALE640    | 2 TB   | 1       | 729   | 0     | 2.00   |
| WDC       | WD2500AAJS-00VTA0  | 250 GB | 27      | 908   | 63    | 2.00   |
| WDC       | WD1002FBYS-01A6B0  | 1 TB   | 2       | 895   | 3     | 1.99   |
| Hitachi   | HDT721032SLA380    | 320 GB | 7       | 958   | 334   | 1.99   |
| WDC       | WD2500AAKX-221CA1  | 250 GB | 2       | 1139  | 4     | 1.99   |
| HGST      | HUS722T2TALA604    | 2 TB   | 4       | 724   | 0     | 1.98   |
| Hitachi   | HCS5C1010CLA382    | 1 TB   | 2       | 722   | 0     | 1.98   |
| WDC       | WD2500AAKX-753CA1  | 250 GB | 17      | 998   | 64    | 1.98   |
| HGST      | HUS724040ALE640    | 4 TB   | 9       | 722   | 0     | 1.98   |
| WDC       | WD15EARS-00S0XB0   | 1.5 TB | 3       | 947   | 1     | 1.97   |
| Seagate   | ST2000DL003-9VT166 | 2 TB   | 95      | 911   | 87    | 1.97   |
| Seagate   | ST9320421ASG       | 320 GB | 2       | 887   | 1     | 1.97   |
| Fujitsu   | MHV2100AH          | 100 GB | 2       | 719   | 0     | 1.97   |
| WDC       | WD6402AAEX-00Z3A0  | 640 GB | 3       | 719   | 0     | 1.97   |
| HGST      | HCC545032A7E380    | 320 GB | 1       | 719   | 0     | 1.97   |
| Seagate   | ST1000VX001-1Z4102 | 1 TB   | 3       | 717   | 0     | 1.97   |
| Seagate   | ST3500630AS P      | 500 GB | 1       | 717   | 0     | 1.96   |
| WDC       | WD2500AAKS-00L9A0  | 250 GB | 12      | 1050  | 4     | 1.96   |
| WDC       | WD800JD-60LSA0     | 80 GB  | 8       | 934   | 99    | 1.96   |
| WDC       | WD5000BEVT-16A0RT0 | 500 GB | 1       | 713   | 0     | 1.95   |
| WDC       | WD800BB-00DKA0     | 80 GB  | 4       | 987   | 1     | 1.95   |
| WDC       | WD1600JS-58NCB1    | 160 GB | 1       | 712   | 0     | 1.95   |
| Samsung   | HD083GJ            | 80 GB  | 5       | 712   | 0     | 1.95   |
| Seagate   | ST3000VN000-1H4167 | 3 TB   | 4       | 711   | 0     | 1.95   |
| WDC       | WD2500KS-00MJB0    | 250 GB | 30      | 990   | 16    | 1.95   |
| WDC       | WD1001FALS-403AA0  | 1 TB   | 4       | 758   | 2     | 1.95   |
| WDC       | WD800JD-00LSA0     | 80 GB  | 24      | 949   | 10    | 1.95   |
| WDC       | WD200BB-32CFC0     | 20 GB  | 1       | 709   | 0     | 1.94   |
| WDC       | WD3200BEKT-00PVMT0 | 320 GB | 3       | 709   | 0     | 1.94   |
| Hitachi   | HDT721032SLA360    | 320 GB | 26      | 1173  | 9     | 1.94   |
| Hitachi   | HUA722020ALA331    | 2 TB   | 9       | 1194  | 5     | 1.94   |
| Hitachi   | HTS723216L9SA60    | 160 GB | 6       | 782   | 1     | 1.94   |
| WDC       | WD1200PD-00FZB0    | 120 GB | 1       | 706   | 0     | 1.94   |
| Seagate   | ST3750640AS        | 752 GB | 11      | 1236  | 260   | 1.93   |
| WDC       | WD2500BEVS-22VAT0  | 250 GB | 1       | 700   | 0     | 1.92   |
| WDC       | WD3200AAJS-65B4A0  | 320 GB | 1       | 699   | 0     | 1.92   |
| WDC       | WD800BB-22JHA0     | 80 GB  | 3       | 1391  | 19    | 1.91   |
| Seagate   | ST3360320AS        | 360 GB | 12      | 1188  | 109   | 1.91   |
| Seagate   | ST4000NM0245-1Z... | 4 TB   | 5       | 837   | 2     | 1.91   |
| Seagate   | ST3160212A         | 160 GB | 16      | 931   | 56    | 1.91   |
| WDC       | WD6400BPVT-35HXZT1 | 640 GB | 2       | 696   | 0     | 1.91   |
| WDC       | WD2500LPVT-00G33T0 | 250 GB | 1       | 696   | 0     | 1.91   |
| WDC       | WD10EALS-00Z8A0    | 1 TB   | 29      | 1030  | 51    | 1.91   |
| Seagate   | ST3250824AS        | 250 GB | 29      | 989   | 576   | 1.91   |
| WDC       | WD5002AALX-00J37A0 | 500 GB | 20      | 957   | 55    | 1.91   |
| WDC       | WD4003FZEX-00Z4SA0 | 4 TB   | 11      | 943   | 2     | 1.91   |
| WDC       | WD20EFRX-68AX9N0   | 2 TB   | 17      | 826   | 1     | 1.90   |
| WDC       | WD2500BMVV-11DCLS0 | 250 GB | 1       | 694   | 0     | 1.90   |
| WDC       | WD10EAVS-00D7B1    | 1 TB   | 24      | 1086  | 107   | 1.90   |
| WDC       | WD5000AAJS-00YFA0  | 500 GB | 5       | 884   | 33    | 1.90   |
| WDC       | WD3200AAJS-65VWA0  | 320 GB | 3       | 692   | 0     | 1.90   |
| WDC       | WD5000BMVW-11AJGS0 | 500 GB | 1       | 692   | 0     | 1.90   |
| WDC       | WD3200BEVE-00A0HT0 | 320 GB | 3       | 691   | 0     | 1.90   |
| HP        | MB2000GCWDA        | 2 TB   | 2       | 691   | 0     | 1.89   |
| WDC       | WD2003FYYS-20W0B0  | 2 TB   | 2       | 690   | 0     | 1.89   |
| WDC       | WD30EZRX-00D8PB0   | 3 TB   | 41      | 758   | 10    | 1.89   |
| Seagate   | ST340215AS         | 40 GB  | 1       | 686   | 0     | 1.88   |
| WDC       | WD7500AACS-65D6B0  | 752 GB | 2       | 895   | 7     | 1.88   |
| Seagate   | ST960813AS         | 64 GB  | 3       | 873   | 4     | 1.88   |
| WDC       | WD20EZRX-00D8PB0   | 2 TB   | 92      | 734   | 6     | 1.88   |
| WDC       | WD5000AAKS-65YGA0  | 500 GB | 8       | 796   | 8     | 1.88   |
| Fujitsu   | MHZ2080BH G2       | 80 GB  | 1       | 684   | 0     | 1.88   |
| Seagate   | ST3320413AS        | 320 GB | 20      | 1077  | 43    | 1.87   |
| WDC       | WD5000BPKT-08PK4T0 | 500 GB | 1       | 683   | 0     | 1.87   |
| WDC       | WD10EACS-00D6B1    | 1 TB   | 4       | 2065  | 478   | 1.87   |
| WDC       | WD1600BEVT-75ZCT0  | 160 GB | 1       | 683   | 0     | 1.87   |
| WDC       | WD2500AAJS-22RYA0  | 250 GB | 2       | 771   | 213   | 1.87   |
| Seagate   | ST6000NE0023-2E... | 6 TB   | 1       | 681   | 0     | 1.87   |
| WDC       | WD20EARS-00MVWB0   | 2 TB   | 86      | 1123  | 101   | 1.86   |
| Hitachi   | HUA721010KLA330... | 1 TB   | 1       | 2715  | 3     | 1.86   |
| Toshiba   | MG03ACA400         | 4 TB   | 4       | 678   | 0     | 1.86   |
| WDC       | WD3200AAKS-61L9A0  | 320 GB | 8       | 717   | 6     | 1.86   |
| Toshiba   | MQ01ABB200         | 2 TB   | 12      | 782   | 70    | 1.85   |
| WDC       | WD800BB-63JKC0     | 80 GB  | 1       | 676   | 0     | 1.85   |
| WDC       | WD15EARS-22Z5B1    | 1.5 TB | 3       | 675   | 0     | 1.85   |
| WDC       | WD6400AAKS-00A7B2  | 640 GB | 7       | 735   | 2     | 1.85   |
| Samsung   | HD502IJ            | 500 GB | 47      | 1173  | 241   | 1.84   |
| Seagate   | ST4000NE0025-2E... | 4 TB   | 4       | 673   | 0     | 1.84   |
| WDC       | WD800BB-75DKA0     | 80 GB  | 1       | 672   | 0     | 1.84   |
| WDC       | WD1200JS-55MHB0    | 120 GB | 2       | 671   | 0     | 1.84   |
| Hitachi   | HDS5C1050CLA382    | 500 GB | 12      | 867   | 114   | 1.84   |
| WDC       | WD5000LPVT-60G33T0 | 500 GB | 1       | 670   | 0     | 1.84   |
| WDC       | WD3200AAKS-75VYA0  | 320 GB | 3       | 670   | 0     | 1.84   |
| WDC       | WD3200AAJS-40RYA0  | 320 GB | 2       | 1197  | 389   | 1.83   |
| WDC       | WD10EZEX-00ZF5A0   | 1 TB   | 24      | 816   | 96    | 1.83   |
| WDC       | WD1502FYPS-01U1B1  | 1.5 TB | 1       | 667   | 0     | 1.83   |
| Seagate   | ST3160812AS        | 160 GB | 47      | 1050  | 369   | 1.83   |
| Hitachi   | HDT721010SLA360    | 1 TB   | 41      | 1144  | 15    | 1.83   |
| Seagate   | ST340014AS         | 40 GB  | 7       | 1406  | 523   | 1.82   |
| WDC       | WD2000JD-22HBC0    | 200 GB | 3       | 1330  | 4     | 1.82   |
| WDC       | WD20EARS-14MVWB0   | 2 TB   | 3       | 664   | 0     | 1.82   |
| WDC       | WD30EURS-63R8UY0   | 3 TB   | 2       | 664   | 0     | 1.82   |
| WDC       | WD20EFRX-68EUZN0   | 2 TB   | 103     | 782   | 1     | 1.82   |
| Seagate   | ST4000VM000-1F3168 | 4 TB   | 5       | 663   | 0     | 1.82   |
| WDC       | WD5001AALS-00L3B2  | 500 GB | 37      | 990   | 26    | 1.82   |
| Seagate   | ST3000NM0033-9Z... | 3 TB   | 4       | 880   | 5     | 1.82   |
| WDC       | WD2000JB-00REA0    | 200 GB | 4       | 885   | 1     | 1.82   |
| Seagate   | ST6000DM004-2EH11C | 6 TB   | 3       | 662   | 0     | 1.82   |
| WDC       | WD1200JD-00FYB0    | 120 GB | 1       | 661   | 0     | 1.81   |
| WDC       | WD6400AAKS-22A7B0  | 640 GB | 13      | 1121  | 4     | 1.81   |
| Hitachi   | HUS724030ALE641    | 3 TB   | 15      | 688   | 84    | 1.81   |
| Seagate   | ST2000DM001-1CH164 | 2 TB   | 188     | 796   | 115   | 1.81   |
| WDC       | WD1003FZEX-00MK2A0 | 1 TB   | 77      | 715   | 1     | 1.81   |
| WDC       | WD800AAJS-00PSA0   | 80 GB  | 24      | 768   | 31    | 1.81   |
| WDC       | WD1600AVBS-63SVA0  | 160 GB | 1       | 658   | 0     | 1.80   |
| WDC       | WD6000HLHX-01JJPV0 | 600 GB | 12      | 1172  | 12    | 1.80   |
| WDC       | WD5000BPVT-75HXZT1 | 500 GB | 1       | 657   | 0     | 1.80   |
| HGST      | HDN726060ALE614    | 6 TB   | 5       | 657   | 0     | 1.80   |
| Samsung   | HD160JJ-P          | 160 GB | 12      | 1122  | 508   | 1.80   |
| WDC       | WD2500AAKX-22ERMA0 | 250 GB | 1       | 656   | 0     | 1.80   |
| WDC       | WD10EALX-009BA0    | 1 TB   | 75      | 918   | 33    | 1.80   |
| WDC       | WD20NMVW-11EDZS2   | 2 TB   | 6       | 655   | 0     | 1.80   |
| HGST      | HDS724040ALE640    | 4 TB   | 7       | 1136  | 289   | 1.80   |
| WDC       | WD1600JS-98NCB1    | 160 GB | 1       | 655   | 0     | 1.80   |
| WDC       | WD5000AAKS-07V0A0  | 500 GB | 1       | 654   | 0     | 1.79   |
| WDC       | WD5000AAKS-00Z7B0  | 500 GB | 1       | 652   | 0     | 1.79   |
| Seagate   | ST3400620AS        | 400 GB | 31      | 1171  | 84    | 1.78   |
| WDC       | WD400BD-60JPA0     | 40 GB  | 1       | 651   | 0     | 1.78   |
| Hitachi   | HDS722580VLSA80    | 82 GB  | 3       | 1101  | 671   | 1.78   |
| Hitachi   | HUA721010KLA330    | 1 TB   | 6       | 1493  | 329   | 1.78   |
| WDC       | WD1002F9YZ-09H1JL1 | 1 TB   | 3       | 648   | 0     | 1.78   |
| WDC       | WD6400AACS-00G8B1  | 640 GB | 11      | 979   | 23    | 1.78   |
| Seagate   | ST980812AS         | 80 GB  | 1       | 647   | 0     | 1.77   |
| WDC       | WD5000AAKS-07TMA0  | 500 GB | 1       | 646   | 0     | 1.77   |
| WDC       | WD6001FZWX-00A2VA0 | 6 TB   | 6       | 646   | 0     | 1.77   |
| WDC       | WD2500HHTZ-04N21V0 | 250 GB | 8       | 706   | 1     | 1.77   |
| Toshiba   | DT01ABA050V        | 500 GB | 1       | 644   | 0     | 1.77   |
| WDC       | WD3200AAJS-65RYA0  | 320 GB | 3       | 644   | 0     | 1.76   |
| WDC       | WD2002FYPS-02W3B0  | 2 TB   | 4       | 776   | 2     | 1.76   |
| WDC       | WD10EARX-00N0YB0   | 1 TB   | 64      | 816   | 23    | 1.76   |
| WDC       | WD2500AAKX-60U6AA0 | 250 GB | 9       | 927   | 79    | 1.76   |
| WDC       | WD2500AAKS-00VSA0  | 250 GB | 27      | 873   | 16    | 1.76   |
| WDC       | WD1001FALS-19J7B0  | 1 TB   | 1       | 641   | 0     | 1.76   |
| Hitachi   | HCS5C3232SLA380    | 320 GB | 3       | 731   | 1     | 1.76   |
| Toshiba   | DT01ABA200V        | 2 TB   | 1       | 639   | 0     | 1.75   |
| WDC       | WD10EARS-22Y5B1    | 1 TB   | 22      | 1242  | 105   | 1.75   |
| Seagate   | ST380815AS         | 80 GB  | 174     | 861   | 229   | 1.75   |
| WDC       | WD800JB-00ETA0     | 80 GB  | 5       | 1354  | 273   | 1.75   |
| WDC       | WD1600JS-98MHB0    | 160 GB | 1       | 638   | 0     | 1.75   |
| WDC       | WD15EADS-00P8B0    | 1.5 TB | 16      | 1343  | 7     | 1.75   |
| Seagate   | ST2000DX001-1NS164 | 2 TB   | 16      | 783   | 63    | 1.75   |
| WDC       | WD1002FBYS-43P1B0  | 1 TB   | 2       | 1021  | 39    | 1.74   |
| Seagate   | ST1000VM002-1CT162 | 1 TB   | 8       | 763   | 6     | 1.74   |
| WDC       | WD3200AAKS-22SBA0  | 320 GB | 1       | 633   | 0     | 1.73   |
| WDC       | WD7500BPVT-16HXZT3 | 752 GB | 1       | 632   | 0     | 1.73   |
| WDC       | WD10JPVX-08JC3T5   | 1 TB   | 15      | 775   | 6     | 1.73   |
| WDC       | WD3200AAKX-221CA1  | 320 GB | 3       | 631   | 0     | 1.73   |
| Hitachi   | HTS723220L9A360    | 200 GB | 1       | 630   | 0     | 1.73   |
| WDC       | WD5003ABYX-01WERA0 | 500 GB | 13      | 999   | 4     | 1.73   |
| WDC       | WD1600AABS-00PRA0  | 160 GB | 1       | 630   | 0     | 1.73   |
| Toshiba   | MK1265GSX H        | 120 GB | 1       | 630   | 0     | 1.73   |
| Seagate   | ST3750640NS        | 752 GB | 10      | 1627  | 577   | 1.73   |
| WDC       | WD2003FZEX-00SRLA0 | 2 TB   | 41      | 648   | 2     | 1.72   |
| Seagate   | ST3200820AS        | 200 GB | 29      | 1018  | 513   | 1.72   |
| Seagate   | ST2000DM001-1ER164 | 2 TB   | 172     | 731   | 48    | 1.72   |
| WDC       | WD3001FFSX-68JNUN0 | 3 TB   | 2       | 628   | 0     | 1.72   |
| Seagate   | ST340014A          | 40 GB  | 91      | 818   | 32    | 1.72   |
| WDC       | WD7500BPKX-60HPJT0 | 752 GB | 1       | 627   | 0     | 1.72   |
| Hitachi   | HDP725032GLA360    | 320 GB | 23      | 938   | 70    | 1.72   |
| WDC       | WD4000BEVT-11ZAT0  | 400 GB | 1       | 626   | 0     | 1.72   |
| WDC       | WD10EACS-32ZJB0    | 1 TB   | 1       | 626   | 0     | 1.72   |
| WDC       | WD15EADS-00R6B0    | 1.5 TB | 1       | 625   | 0     | 1.71   |
| Seagate   | ST3320311CS        | 320 GB | 13      | 684   | 78    | 1.71   |
| WDC       | WD20EURS-73S48Y0   | 2 TB   | 1       | 623   | 0     | 1.71   |
| WDC       | WD10EADS-65L5B1    | 1 TB   | 11      | 1014  | 3     | 1.70   |
| WDC       | WD360GD-00FLC0     | 37 GB  | 1       | 622   | 0     | 1.70   |
| WDC       | WD400BD-23JMC0     | 40 GB  | 1       | 1866  | 2     | 1.70   |
| Hitachi   | HUA723020ALA641    | 2 TB   | 32      | 803   | 75    | 1.70   |
| Maxtor    | STM3160215A        | 160 GB | 11      | 664   | 279   | 1.70   |
| Hitachi   | HTS545032B9SA00    | 320 GB | 6       | 814   | 385   | 1.70   |
| WDC       | WD6002FFWX-68TZ4N0 | 6 TB   | 2       | 620   | 0     | 1.70   |
| WDC       | WD20SPZX-22CRAT0   | 2 TB   | 1       | 620   | 0     | 1.70   |
| WDC       | WD1600AAJS-55PSA0  | 160 GB | 1       | 620   | 0     | 1.70   |
| Toshiba   | MK1229GSG          | 120 GB | 1       | 619   | 0     | 1.70   |
| WDC       | WD2500BEVS-26VAT0  | 250 GB | 3       | 617   | 0     | 1.69   |
| WDC       | WD3200AAKX-083CA1  | 320 GB | 2       | 617   | 0     | 1.69   |
| WDC       | WD3200AAJS-00G0A0  | 320 GB | 1       | 617   | 0     | 1.69   |
| WDC       | WD10EZEX-22RKKA0   | 1 TB   | 9       | 726   | 3     | 1.69   |
| WDC       | WD4000F9YZ-09N20L0 | 4 TB   | 2       | 616   | 0     | 1.69   |
| WDC       | WD10EALS-002BA0    | 1 TB   | 4       | 820   | 2     | 1.69   |
| WDC       | WD4001FFSX-68JNUN0 | 4 TB   | 3       | 614   | 0     | 1.68   |
| WDC       | WD10EZEX-22BN5A0   | 1 TB   | 28      | 674   | 2     | 1.68   |
| Seagate   | ST4000DX001-1CE168 | 4 TB   | 16      | 852   | 48    | 1.68   |
| Hitachi   | HCS5C1032CLA382    | 320 GB | 2       | 883   | 2     | 1.68   |
| Seagate   | ST8000VN0022-2E... | 8 TB   | 32      | 748   | 8     | 1.68   |
| WDC       | WD10EZEX-00KUWA0   | 1 TB   | 24      | 691   | 1     | 1.68   |
| WDC       | WD800JD-00MSA1     | 80 GB  | 15      | 825   | 16    | 1.68   |
| WDC       | WD5000AAKS-00V0A0  | 500 GB | 4       | 675   | 2     | 1.68   |
| Hitachi   | HDT721016SLA380    | 160 GB | 20      | 965   | 5     | 1.68   |
| Seagate   | ST1000DM005 HD1... | 1 TB   | 16      | 711   | 2     | 1.68   |
| Seagate   | ST4000NM0033-9Z... | 4 TB   | 11      | 657   | 250   | 1.67   |
| WDC       | WD800JD-00LUA0     | 80 GB  | 1       | 610   | 0     | 1.67   |
| Hitachi   | HDS721010CLA332    | 1 TB   | 142     | 1038  | 98    | 1.67   |
| WDC       | WD10EZRX-00A8LB0   | 1 TB   | 62      | 753   | 32    | 1.67   |
| HP        | MB1000GDUNU        | 1 TB   | 1       | 609   | 0     | 1.67   |
| WDC       | WD20EARX-00MMMB0   | 2 TB   | 3       | 1109  | 5     | 1.67   |
| Seagate   | ST4000DM005-2DP166 | 4 TB   | 30      | 610   | 43    | 1.67   |
| Seagate   | ST31000526SV       | 1 TB   | 3       | 769   | 343   | 1.67   |
| Seagate   | ST3500418ASQ       | 500 GB | 1       | 608   | 0     | 1.67   |
| WDC       | WD2500AAKX-083CA1  | 250 GB | 13      | 970   | 4     | 1.67   |
| Seagate   | ST3160815AS        | 160 GB | 210     | 882   | 344   | 1.67   |
| WDC       | WD1600AAJS-00PSA0  | 160 GB | 28      | 852   | 51    | 1.66   |
| Toshiba   | DT01ABA300         | 3 TB   | 7       | 635   | 2     | 1.66   |
| ExcelStor | J9250S             | 250 GB | 5       | 677   | 1     | 1.66   |
| WDC       | WD3200AAJS-00VWA0  | 320 GB | 13      | 663   | 36    | 1.66   |
| WDC       | WD10EZEX-60M2NA0   | 1 TB   | 25      | 769   | 66    | 1.66   |
| WDC       | WD20EZRX-60D8PB0   | 2 TB   | 2       | 604   | 0     | 1.66   |
| Samsung   | HD103UJ            | 1 TB   | 80      | 1225  | 192   | 1.66   |
| WDC       | WD3000JS-60PDB0    | 304 GB | 2       | 603   | 0     | 1.65   |
| WDC       | WD2500LPLX-00ZNTT0 | 250 GB | 1       | 603   | 0     | 1.65   |
| WDC       | WD800AAJS-00WAA0   | 80 GB  | 6       | 603   | 2     | 1.65   |
| Hitachi   | HTS545016B9SA02    | 160 GB | 1       | 602   | 0     | 1.65   |
| Seagate   | ST31000524NS       | 1 TB   | 8       | 1232  | 195   | 1.65   |
| WDC       | WD15NPVT-00Z2TT0   | 1.5 TB | 1       | 601   | 0     | 1.65   |
| Apple     | HDD HTS541075A9... | 752 GB | 1       | 601   | 0     | 1.65   |
| WDC       | WD1200JS-00MHB0    | 120 GB | 15      | 635   | 1     | 1.65   |
| WDC       | WD800JD-23LSA0     | 80 GB  | 1       | 1202  | 1     | 1.65   |
| WDC       | WD1600JS-23MHB0    | 160 GB | 1       | 600   | 0     | 1.64   |
| Samsung   | HD103SI            | 1 TB   | 63      | 995   | 253   | 1.64   |
| WDC       | WD15EARX-00PASB0   | 1.5 TB | 11      | 663   | 2     | 1.64   |
| Seagate   | ST3250620AS        | 250 GB | 59      | 972   | 341   | 1.64   |
| Seagate   | ST2000DL001-9VT156 | 2 TB   | 14      | 1183  | 520   | 1.64   |
| WDC       | WD1600AAJS-62WAA0  | 160 GB | 1       | 597   | 0     | 1.64   |
| WDC       | WD10EURX-56FH1Y0   | 1 TB   | 2       | 596   | 0     | 1.63   |
| Seagate   | ST3250312AS        | 250 GB | 39      | 736   | 28    | 1.63   |
| WDC       | WD5003AZEX-00MK2A0 | 500 GB | 15      | 634   | 1     | 1.63   |
| Seagate   | ST2000VX000-1ES164 | 2 TB   | 9       | 595   | 0     | 1.63   |
| Seagate   | ST3000VX000-1ES166 | 3 TB   | 3       | 594   | 0     | 1.63   |
| WDC       | WD800JD-08MSA1     | 80 GB  | 3       | 591   | 0     | 1.62   |
| Samsung   | HD154UI            | 1.5 TB | 55      | 996   | 277   | 1.62   |
| WDC       | WD1600BEKT-75A25T0 | 160 GB | 2       | 590   | 0     | 1.62   |
| Seagate   | ST2000NM0033-9Z... | 2 TB   | 9       | 590   | 0     | 1.62   |
| Seagate   | ST1000DX001-SSH... | 1 TB   | 1       | 590   | 0     | 1.62   |
| WDC       | WD20EZRX-00DC0B0   | 2 TB   | 40      | 692   | 16    | 1.62   |
| Apple     | HDD ST750LM022     | 752 GB | 1       | 589   | 0     | 1.61   |
| Hitachi   | HUA722010CLA330    | 1 TB   | 19      | 947   | 58    | 1.61   |
| WDC       | WD1600BEVS-22UST0  | 160 GB | 3       | 782   | 63    | 1.61   |
| Seagate   | ST3808110AS        | 80 GB  | 40      | 1020  | 383   | 1.61   |
| WDC       | WD60EZRX-00MVLB1   | 6 TB   | 14      | 773   | 3     | 1.61   |
| Samsung   | HD153WI            | 1.5 TB | 2       | 588   | 0     | 1.61   |
| WDC       | WD800JD-19LSA0     | 80 GB  | 1       | 588   | 0     | 1.61   |
| WDC       | WD10EZEX-75ZF5A0   | 1 TB   | 8       | 635   | 252   | 1.61   |
| WDC       | WD2000JS-22NCB1    | 200 GB | 2       | 1529  | 24    | 1.61   |
| WDC       | WD400BD-75MRA3     | 40 GB  | 2       | 587   | 0     | 1.61   |
| WDC       | WD5000AAKS-75V0A0  | 500 GB | 11      | 1177  | 3     | 1.61   |
| WDC       | WD800JD-00HKA0     | 80 GB  | 4       | 892   | 28    | 1.61   |
| WDC       | WD2500AAJS-60M0A1  | 250 GB | 2       | 587   | 0     | 1.61   |
| WDC       | WD2000JS-00MHB0    | 200 GB | 9       | 780   | 54    | 1.61   |
| WDC       | WD1600AAJS-00M0A0  | 160 GB | 6       | 784   | 68    | 1.61   |
| Hitachi   | HDT725050VLA360    | 500 GB | 5       | 1151  | 37    | 1.60   |
| WDC       | WD1003FBYZ-010FB0  | 1 TB   | 18      | 654   | 2     | 1.60   |
| Maxtor    | 6V200E0            | 208 GB | 10      | 1054  | 104   | 1.60   |
| WDC       | WD10EADS-11M2B3    | 1 TB   | 4       | 584   | 0     | 1.60   |
| WDC       | WD400BB-60JKA0     | 40 GB  | 4       | 785   | 21    | 1.60   |
| WDC       | WD20EARS-55MVWB0   | 2 TB   | 1       | 584   | 0     | 1.60   |
| Toshiba   | DT01ACA300         | 3 TB   | 98      | 666   | 57    | 1.60   |
| Seagate   | ST1000DL002-9TT153 | 1 TB   | 43      | 1111  | 352   | 1.60   |
| WDC       | WD10EADX-22TDHB0   | 1 TB   | 11      | 950   | 105   | 1.60   |
| WDC       | WD10EARX-32N0YB0   | 1 TB   | 4       | 894   | 121   | 1.60   |
| Seagate   | ST980411ASG        | 80 GB  | 3       | 734   | 5     | 1.60   |
| WDC       | WD800JD-75MSA2     | 80 GB  | 3       | 582   | 0     | 1.60   |
| WDC       | WD1600AAJS-22WAA0  | 160 GB | 7       | 908   | 2     | 1.59   |
| WDC       | WD1600BEVS-75RST0  | 160 GB | 2       | 579   | 0     | 1.59   |
| Maxtor    | STM3320620A        | 320 GB | 2       | 579   | 0     | 1.59   |
| WDC       | WD4002FFWX-68TZ4N0 | 4 TB   | 1       | 579   | 0     | 1.59   |
| WDC       | WD2500BEKT-60V5T1  | 250 GB | 1       | 578   | 0     | 1.59   |
| WDC       | WD2500AAJS-07M0A0  | 250 GB | 5       | 776   | 4     | 1.59   |
| WDC       | WD1600BB-55RDA0    | 160 GB | 3       | 682   | 2     | 1.58   |
| WDC       | WD6400AAKS-40H2B0  | 640 GB | 3       | 1324  | 271   | 1.58   |
| WDC       | WD10EZEX-19M2NA0   | 1 TB   | 1       | 576   | 0     | 1.58   |
| WDC       | WD2500BUCT-63TWBY0 | 250 GB | 2       | 884   | 519   | 1.58   |
| Samsung   | SP1644N            | 160 GB | 3       | 683   | 527   | 1.58   |
| Hitachi   | HDS721050CLA662    | 500 GB | 22      | 685   | 51    | 1.57   |
| Toshiba   | MQ01ABC150         | 1.5 TB | 1       | 574   | 0     | 1.57   |
| Hitachi   | HDS721050CLA362    | 500 GB | 146     | 792   | 49    | 1.57   |
| WDC       | WD800BEVS-08RST2   | 80 GB  | 4       | 574   | 0     | 1.57   |
| Seagate   | ST3160316AS        | 160 GB | 13      | 688   | 7     | 1.57   |
| Seagate   | ST1000NM0033-9Z... | 1 TB   | 35      | 686   | 88    | 1.57   |
| WDC       | WD3200AAKS-00B3A0  | 320 GB | 39      | 816   | 29    | 1.57   |
| Hitachi   | HCS725032VLA380    | 320 GB | 1       | 573   | 0     | 1.57   |
| Seagate   | ST32000541AS       | 2 TB   | 1       | 572   | 0     | 1.57   |
| Seagate   | ST3160212AS        | 160 GB | 2       | 572   | 0     | 1.57   |
| WDC       | WD1600AAJS-60WAA0  | 160 GB | 5       | 625   | 203   | 1.56   |
| Hitachi   | HTS725032A9A360    | 320 GB | 3       | 569   | 0     | 1.56   |
| WDC       | WD2500JS-00SGB0    | 250 GB | 6       | 691   | 1     | 1.56   |
| Samsung   | HD321HJ            | 320 GB | 14      | 874   | 121   | 1.56   |
| Seagate   | ST4000VM000-2AF166 | 4 TB   | 2       | 566   | 0     | 1.55   |
| Seagate   | ST3320620A         | 320 GB | 25      | 870   | 5     | 1.55   |
| Seagate   | ST1000NX0443       | 1 TB   | 2       | 566   | 0     | 1.55   |
| Seagate   | ST10000VN0004-1... | 10 TB  | 17      | 604   | 1     | 1.55   |
| Seagate   | ST1000NM0011       | 1 TB   | 20      | 1560  | 30    | 1.55   |
| WDC       | WD3200BEVT-75ZCT2  | 320 GB | 13      | 612   | 58    | 1.55   |
| WDC       | WD5000AACS-00G8B1  | 500 GB | 12      | 747   | 3     | 1.54   |
| Seagate   | ST3320820AS_Q      | 320 GB | 2       | 1793  | 1068  | 1.54   |
| Seagate   | ST2000VN000-1HJ164 | 2 TB   | 6       | 562   | 0     | 1.54   |
| WDC       | WD20NPVX-00EA4T0   | 2 TB   | 3       | 561   | 0     | 1.54   |
| WDC       | WD40PURX-64GVNY0   | 4 TB   | 2       | 561   | 0     | 1.54   |
| WDC       | WD2500JB-98GVA0    | 250 GB | 1       | 3354  | 5     | 1.53   |
| WDC       | WD2500AAJB-00WGA0  | 250 GB | 5       | 1069  | 115   | 1.53   |
| Seagate   | ST3250823A         | 250 GB | 6       | 977   | 440   | 1.53   |
| WDC       | WD6400BPVT-75HXZT1 | 640 GB | 5       | 658   | 2     | 1.53   |
| Maxtor    | 7H500F0            | 500 GB | 4       | 646   | 1     | 1.53   |
| WDC       | WD800JD-22LSA0     | 80 GB  | 8       | 715   | 83    | 1.53   |
| WDC       | WD800JD-00LSA5     | 80 GB  | 2       | 557   | 0     | 1.53   |
| WDC       | WD10JMVW-11AJGS0   | 1 TB   | 5       | 891   | 15    | 1.53   |
| WDC       | WD15NMVW-11W68S0   | 1.5 TB | 1       | 556   | 0     | 1.52   |
| WDC       | WD2500BEVS-00UST0  | 250 GB | 2       | 812   | 2     | 1.52   |
| WDC       | WD3000JS-00PDB0    | 304 GB | 1       | 554   | 0     | 1.52   |
| Seagate   | ST500DM009-2DM14C  | 500 GB | 4       | 554   | 0     | 1.52   |
| Maxtor    | 6V160E0            | 160 GB | 10      | 603   | 1     | 1.52   |
| WDC       | WD400BB-00JHA0     | 40 GB  | 4       | 1037  | 3     | 1.51   |
| WDC       | WD20NMVW-11AV3S2   | 2 TB   | 34      | 695   | 2     | 1.51   |
| WDC       | WD3200BPVT-00HXZT0 | 320 GB | 1       | 549   | 0     | 1.51   |
| Fujitsu   | MHV2080BH          | 80 GB  | 5       | 619   | 2     | 1.51   |
| WDC       | WD1600JS-00SGB0    | 160 GB | 1       | 549   | 0     | 1.50   |
| WDC       | WD2500AAKS-00YGA0  | 250 GB | 2       | 548   | 0     | 1.50   |
| Seagate   | ST360015A          | 64 GB  | 2       | 1494  | 5     | 1.50   |
| WDC       | WD60EFRX-68MYMN1   | 6 TB   | 12      | 835   | 58    | 1.50   |
| WDC       | WD360ADFD-00NLR1   | 37 GB  | 1       | 547   | 0     | 1.50   |
| Seagate   | ST3200827A         | 200 GB | 1       | 544   | 0     | 1.49   |
| Seagate   | ST3320418AS        | 320 GB | 98      | 912   | 143   | 1.49   |
| WDC       | WD10EZEX-00ER1A0   | 1 TB   | 4       | 544   | 0     | 1.49   |
| WDC       | WD3200BMVU-11A04S0 | 320 GB | 2       | 548   | 115   | 1.49   |
| WDC       | WD2000JD-00HBB0    | 200 GB | 5       | 897   | 3     | 1.49   |
| Seagate   | ST3160318AS        | 160 GB | 75      | 779   | 83    | 1.49   |
| Samsung   | HD502HJ            | 500 GB | 130     | 770   | 68    | 1.49   |
| Hitachi   | HDS728080PLA380    | 80 GB  | 47      | 817   | 49    | 1.49   |
| MediaMax  | WL1000GSA6472C     | 1 TB   | 1       | 543   | 0     | 1.49   |
| Hitachi   | HDT725025VLAT80    | 250 GB | 2       | 1843  | 2     | 1.49   |
| WDC       | WD7500BPKX-75HPJT0 | 752 GB | 5       | 542   | 0     | 1.49   |
| Seagate   | ST4000VN000-2AH166 | 4 TB   | 3       | 542   | 0     | 1.49   |
| HGST      | HCC545050A7E380    | 500 GB | 3       | 664   | 1     | 1.48   |
| Seagate   | ST31500541AS       | 1.5 TB | 12      | 893   | 33    | 1.48   |
| WDC       | WD10EFRX-68PJCN0   | 1 TB   | 34      | 668   | 1     | 1.48   |
| Seagate   | ST380011A          | 80 GB  | 185     | 827   | 72    | 1.48   |
| WDC       | WD2500BEVS-26UST0  | 250 GB | 5       | 540   | 0     | 1.48   |
| WDC       | WD80EZZX-11CSGA0   | 8 TB   | 3       | 540   | 0     | 1.48   |
| WDC       | WD3000HLFS-01G6U0  | 304 GB | 1       | 540   | 0     | 1.48   |
| WDC       | WD1200JS-00MHB1    | 120 GB | 3       | 685   | 8     | 1.48   |
| WDC       | WD5000AAKX-753CA1  | 500 GB | 11      | 1379  | 29    | 1.48   |
| WDC       | WD5000AAKS-75A7B0  | 500 GB | 4       | 673   | 2     | 1.48   |
| WDC       | WD7500AZEX-00RKKA0 | 752 GB | 6       | 538   | 0     | 1.48   |
| WDC       | WD20EADS-00R6B0    | 2 TB   | 8       | 926   | 254   | 1.47   |
| Seagate   | ST3500414CS        | 500 GB | 10      | 717   | 12    | 1.47   |
| Seagate   | ST3300620AS        | 304 GB | 2       | 538   | 0     | 1.47   |
| WDC       | WD1000DHTZ-04N21V0 | 1 TB   | 7       | 945   | 14    | 1.47   |
| WDC       | WD3200BPVT-26JJ5T0 | 320 GB | 1       | 537   | 0     | 1.47   |
| Samsung   | HD642JJ            | 640 GB | 33      | 1359  | 392   | 1.47   |
| WDC       | WD10EALX-759BA0    | 1 TB   | 2       | 1394  | 5     | 1.47   |
| Hitachi   | HDS728080PLAT20    | 82 GB  | 23      | 728   | 7     | 1.47   |
| WDC       | WD3200AAKS-00VYA0  | 320 GB | 8       | 605   | 45    | 1.47   |
| WDC       | WD1001FAES-55W7A0  | 1 TB   | 2       | 535   | 0     | 1.47   |
| Seagate   | ST3500413AS        | 500 GB | 152     | 697   | 82    | 1.47   |
| WDC       | WD6400AAKS-07A7B0  | 640 GB | 5       | 937   | 25    | 1.47   |
| WDC       | WD10EZEX-00RKKA0   | 1 TB   | 102     | 695   | 76    | 1.47   |
| HGST      | HUH721212ALN600    | 12 TB  | 1       | 534   | 0     | 1.46   |
| WDC       | WD800AAJS-22L7A0   | 80 GB  | 1       | 534   | 0     | 1.46   |
| Toshiba   | MK3259GSX          | 320 GB | 2       | 628   | 41    | 1.46   |
| Seagate   | ST3120026AS        | 120 GB | 31      | 1128  | 69    | 1.46   |
| WDC       | WD1600JS-22MHB0    | 160 GB | 3       | 700   | 9     | 1.46   |
| WDC       | WD10TMVW-11ZSMS0   | 1 TB   | 1       | 531   | 0     | 1.46   |
| WDC       | WD15EADS-00S2B0    | 1.5 TB | 3       | 1535  | 9     | 1.46   |
| Seagate   | ST1000DM003-1ER162 | 1 TB   | 260     | 555   | 35    | 1.46   |
| WDC       | WD800JD-22MSA1     | 80 GB  | 11      | 769   | 15    | 1.45   |
| WDC       | WD15EZRX-00DC0B0   | 1.5 TB | 2       | 530   | 0     | 1.45   |
| Hitachi   | HDS5C1032CLA382    | 320 GB | 5       | 748   | 3     | 1.45   |
| Seagate   | ST360021A          | 64 GB  | 5       | 598   | 10    | 1.45   |
| Seagate   | ST2000DM002-1BJ164 | 2 TB   | 1       | 529   | 0     | 1.45   |
| WDC       | WD3200AAKS-00L9A0  | 320 GB | 50      | 908   | 29    | 1.45   |
| WDC       | WD7500BPVX-60JC3T0 | 752 GB | 10      | 618   | 2     | 1.45   |
| WDC       | WD5000AZRX-00A8LB0 | 500 GB | 82      | 576   | 1     | 1.45   |
| Seagate   | ST14000VN0008-2... | 14 TB  | 2       | 525   | 0     | 1.44   |
| WDC       | WD7500BPVT-00HXZT1 | 752 GB | 1       | 525   | 0     | 1.44   |
| WDC       | WD1600AAJS-60B4A0  | 160 GB | 6       | 936   | 200   | 1.44   |
| WDC       | WD10EURX-83UY4Y0   | 1 TB   | 1       | 524   | 0     | 1.44   |
| Hitachi   | HDS721050CLA660    | 500 GB | 23      | 733   | 136   | 1.44   |
| WDC       | WD5000AAKS-22A7B0  | 500 GB | 17      | 1023  | 22    | 1.44   |
| Seagate   | ST4000NM0035-1V... | 4 TB   | 7       | 523   | 0     | 1.43   |
| Seagate   | ST160LM003 HN-M... | 160 GB | 3       | 522   | 0     | 1.43   |
| WDC       | WD5000BMVW-11AMCS2 | 500 GB | 3       | 522   | 0     | 1.43   |
| WDC       | WD2500BPVT-00JJ5T0 | 250 GB | 1       | 522   | 0     | 1.43   |
| Maxtor    | 4K020H1            | 20 GB  | 1       | 522   | 0     | 1.43   |
| HGST      | HTS545025A7E380    | 250 GB | 1       | 522   | 0     | 1.43   |
| WDC       | WD2500AAKX-603CA0  | 250 GB | 9       | 664   | 134   | 1.43   |
| WDC       | WD800BB-00JKC0     | 80 GB  | 2       | 520   | 0     | 1.43   |
| WDC       | WD6400AARS-003BB1  | 640 GB | 1       | 520   | 0     | 1.43   |
| Seagate   | ST2000VX000-1CU164 | 2 TB   | 16      | 737   | 254   | 1.43   |
| WDC       | WD2500AAKX-001CA0  | 250 GB | 34      | 637   | 86    | 1.42   |
| WDC       | WD1600YD-01NVB1    | 164 GB | 1       | 519   | 0     | 1.42   |
| WDC       | WD3200BEKT-75PVMT1 | 320 GB | 9       | 685   | 2     | 1.42   |
| Seagate   | ST3500312CS        | 500 GB | 48      | 889   | 186   | 1.42   |
| WDC       | WD5000AZRX-00L4HB0 | 500 GB | 28      | 519   | 0     | 1.42   |
| Fujitsu   | MHW2120BH          | 120 GB | 22      | 579   | 24    | 1.42   |
| Maxtor    | 6G160P0            | 160 GB | 3       | 517   | 0     | 1.42   |
| WDC       | WD10EACS-22D6B0    | 1 TB   | 3       | 961   | 5     | 1.42   |
| Samsung   | HD105SI            | 1 TB   | 16      | 792   | 247   | 1.42   |
| WDC       | WD6400AARS-00Y5B1  | 640 GB | 16      | 912   | 11    | 1.41   |
| Toshiba   | HDWT360            | 6 TB   | 1       | 516   | 0     | 1.41   |
| Hitachi   | HTS722012K9SA00    | 120 GB | 5       | 576   | 407   | 1.41   |
| Apple     | HDD HTS541010A9... | 1 TB   | 21      | 656   | 228   | 1.41   |
| Hitachi   | HDP725050GLA360    | 500 GB | 95      | 1102  | 54    | 1.41   |
| Hitachi   | HDS721616PLA380    | 160 GB | 99      | 920   | 81    | 1.41   |
| Seagate   | ST3250820AS        | 250 GB | 57      | 896   | 246   | 1.40   |
| Hitachi   | HDT722516DLA380    | 164 GB | 17      | 922   | 43    | 1.40   |
| WDC       | WD1500HLFS-01MZUV0 | 150 GB | 2       | 511   | 0     | 1.40   |
| WDC       | WD5000BMVW-11S5XS0 | 500 GB | 8       | 638   | 2     | 1.40   |
| Seagate   | ST640LM000 HM641JI | 640 GB | 2       | 511   | 0     | 1.40   |
| Samsung   | HD503HI            | 500 GB | 21      | 678   | 12    | 1.40   |
| WDC       | WD3200AAJS-55B4A0  | 320 GB | 2       | 749   | 4     | 1.40   |
| WDC       | WD5000LPVT-16G33T0 | 500 GB | 5       | 508   | 0     | 1.39   |
| Seagate   | ST4000DM006-2G5107 | 4 TB   | 1       | 508   | 0     | 1.39   |
| WDC       | WD5000AAKS-00D2B0  | 500 GB | 14      | 956   | 8     | 1.39   |
| WDC       | WD6400AAKS-55A7B0  | 640 GB | 1       | 507   | 0     | 1.39   |
| Hitachi   | HTS721010G9SA00    | 100 GB | 3       | 1028  | 39    | 1.39   |
| WDC       | WD5000BEVT-80A0RT0 | 500 GB | 4       | 927   | 5     | 1.38   |
| WDC       | WD10JFCX-68N6GN0   | 1 TB   | 20      | 564   | 1     | 1.38   |
| Toshiba   | MK2556GSYF         | 250 GB | 1       | 503   | 0     | 1.38   |
| WDC       | WD10EZRX-00L4HB0   | 1 TB   | 59      | 531   | 3     | 1.38   |
| WDC       | WD3200BPVT-75JJ5T0 | 320 GB | 5       | 547   | 2     | 1.38   |
| WDC       | WD10EFRX-68FYTN0   | 1 TB   | 37      | 550   | 1     | 1.38   |
| Seagate   | ST1000VT000 HN-... | 1 TB   | 1       | 501   | 0     | 1.38   |
| WDC       | WD10EURX-73C57Y0   | 1 TB   | 3       | 501   | 0     | 1.37   |
| Seagate   | ST3160023A         | 160 GB | 17      | 841   | 302   | 1.37   |
| Toshiba   | MK1032GSX          | 100 GB | 6       | 521   | 1     | 1.37   |
| WDC       | WD1600JS-00NCB1    | 160 GB | 17      | 801   | 10    | 1.37   |
| WDC       | WD10EADX-00TDHB0   | 1 TB   | 5       | 826   | 13    | 1.37   |
| Seagate   | ST2000VX003-1HH164 | 2 TB   | 2       | 500   | 0     | 1.37   |
| Seagate   | ST3120026A         | 120 GB | 25      | 957   | 147   | 1.37   |
| Seagate   | ST380012ACE        | 80 GB  | 4       | 498   | 0     | 1.37   |
| WDC       | WD2500AAJS-22VTA0  | 250 GB | 8       | 617   | 1     | 1.37   |
| Seagate   | ST3200826AS        | 200 GB | 15      | 934   | 65    | 1.36   |
| WDC       | WD200EB-00BHF0     | 20 GB  | 1       | 992   | 1     | 1.36   |
| WDC       | WD800BB-55JKA0     | 80 GB  | 5       | 740   | 1     | 1.36   |
| WDC       | WD1200JD-00GBB0    | 120 GB | 3       | 754   | 4     | 1.36   |
| Samsung   | HD253GJ            | 250 GB | 10      | 869   | 13    | 1.36   |
| Fujitsu   | MPE3136AH          | 16 GB  | 1       | 494   | 0     | 1.35   |
| WDC       | WD2500JS-75NCB1    | 250 GB | 3       | 1381  | 51    | 1.35   |
| WDC       | WD2500BEVT-75ZCT2  | 250 GB | 5       | 738   | 1     | 1.35   |
| WDC       | WD6002FRYZ-01WD5B0 | 6 TB   | 2       | 817   | 1     | 1.35   |
| WDC       | WD5000AAKS-00V2B0  | 500 GB | 3       | 663   | 1     | 1.35   |
| Seagate   | ST1000VX000-9YW162 | 1 TB   | 5       | 491   | 0     | 1.35   |
| WDC       | WD800BEVT-00ZCT0   | 80 GB  | 2       | 491   | 0     | 1.35   |
| Fujitsu   | MHY2250BH          | 250 GB | 9       | 747   | 42    | 1.34   |
| Toshiba   | DT01ACA200         | 2 TB   | 178     | 540   | 52    | 1.34   |
| Hitachi   | HDE721064SLA360    | 640 GB | 2       | 585   | 2     | 1.34   |
| WDC       | WD800BB-00JHA0     | 80 GB  | 8       | 827   | 4     | 1.34   |
| WDC       | WD5000AAKS-007AA0  | 500 GB | 12      | 778   | 10    | 1.34   |
| WDC       | WD5000BMVW-11AMCS4 | 500 GB | 5       | 684   | 2     | 1.34   |
| Seagate   | ST2000DM001-9YN164 | 2 TB   | 67      | 883   | 375   | 1.34   |
| WDC       | WD5000AACS-32G8B1  | 500 GB | 1       | 487   | 0     | 1.33   |
| WDC       | WD740ADFD-00NLR5   | 74 GB  | 2       | 486   | 0     | 1.33   |
| WDC       | WD1600BJKT-00F4T0  | 160 GB | 1       | 486   | 0     | 1.33   |
| HGST      | HUH728080ALN600    | 8 TB   | 1       | 485   | 0     | 1.33   |
| WDC       | WD800JD-55JRC0     | 80 GB  | 2       | 604   | 31    | 1.33   |
| Apple     | HDD ST1000DM003    | 1 TB   | 16      | 484   | 0     | 1.33   |
| Fujitsu   | MHT2040AH          | 40 GB  | 1       | 484   | 0     | 1.33   |
| WDC       | WD2500AAKX-75U6AA0 | 250 GB | 10      | 816   | 3     | 1.33   |
| WDC       | WD10EZRX-00DC0B0   | 1 TB   | 6       | 552   | 2     | 1.32   |
| Seagate   | ST10000VN0004-2... | 10 TB  | 1       | 483   | 0     | 1.32   |
| HP        | GB0250EAFJF        | 250 GB | 3       | 1117  | 3     | 1.32   |
| WDC       | WD1200JB-00GVA0    | 120 GB | 4       | 754   | 1     | 1.32   |
| WDC       | WD10EZEX-00BN5A0   | 1 TB   | 188     | 565   | 9     | 1.32   |
| Hitachi   | HCS5C1050CLA382    | 500 GB | 2       | 482   | 0     | 1.32   |
| Seagate   | ST340015A          | 40 GB  | 5       | 835   | 33    | 1.32   |
| Seagate   | ST3000DM001-1CH166 | 3 TB   | 56      | 601   | 258   | 1.32   |
| WDC       | WD5000AADS-00L4B1  | 500 GB | 8       | 840   | 12    | 1.32   |
| WDC       | WD7500AZEX-00ZF5A0 | 752 GB | 6       | 481   | 0     | 1.32   |
| Seagate   | ST380215AS         | 80 GB  | 27      | 773   | 515   | 1.32   |
| WDC       | WD5000BPKX-80HPJT0 | 500 GB | 1       | 480   | 0     | 1.32   |
| WDC       | WD2500AAKS-00UU3A0 | 250 GB | 5       | 543   | 2     | 1.32   |
| WDC       | WD3200AAKS-00UU3A0 | 320 GB | 16      | 812   | 70    | 1.32   |
| WDC       | WD10EZEX-08M2NA0   | 1 TB   | 88      | 526   | 4     | 1.31   |
| WDC       | WD3200AAKS-75L9A0  | 320 GB | 22      | 882   | 40    | 1.31   |
| WDC       | WD20EZRX-22D8PB0   | 2 TB   | 6       | 479   | 0     | 1.31   |
| WDC       | WD7502AAEX-00Y9A0  | 752 GB | 5       | 478   | 0     | 1.31   |
| Seagate   | ST3160815A         | 160 GB | 40      | 734   | 222   | 1.31   |
| Seagate   | ST3500630NS        | 500 GB | 7       | 775   | 672   | 1.31   |
| Seagate   | ST9120821A         | 120 GB | 4       | 719   | 19    | 1.30   |
| WDC       | WD5000AUDX-63WNHY0 | 500 GB | 3       | 475   | 0     | 1.30   |
| Seagate   | ST3500320NS        | 500 GB | 17      | 887   | 341   | 1.30   |
| WDC       | WD30EZRS-00J99B0   | 3 TB   | 8       | 1225  | 733   | 1.30   |
| WDC       | WD2500AAKS-00F0A0  | 250 GB | 9       | 875   | 264   | 1.30   |
| Seagate   | ST500NM0011        | 500 GB | 16      | 1100  | 63    | 1.30   |
| WDC       | WD1600JS-56MHB1    | 160 GB | 7       | 888   | 5     | 1.30   |
| Seagate   | ST1000VX000-1CU162 | 1 TB   | 27      | 485   | 38    | 1.30   |
| WDC       | WD10EACS-11BHUB0   | 1 TB   | 1       | 473   | 0     | 1.30   |
| Toshiba   | MK1016GAP          | 10 GB  | 1       | 472   | 0     | 1.29   |
| WDC       | WD10EACS-65D6B0    | 1 TB   | 1       | 471   | 0     | 1.29   |
| WDC       | WD5000AAKS-75A7B2  | 500 GB | 3       | 1036  | 6     | 1.29   |
| WDC       | WD10EZEX-21M2NA0   | 1 TB   | 39      | 542   | 36    | 1.29   |
| WDC       | WD7500AARS-00Y5B1  | 752 GB | 13      | 568   | 3     | 1.29   |
| Seagate   | ST10000NE0004-1... | 10 TB  | 9       | 830   | 13    | 1.29   |
| HGST      | HUH721010ALE600    | 10 TB  | 11      | 502   | 1     | 1.29   |
| WDC       | WD10EZEX-75M2NA0   | 1 TB   | 20      | 509   | 1     | 1.28   |
| WDC       | WD60EZRZ-11RWYB1   | 6 TB   | 1       | 468   | 0     | 1.28   |
| Toshiba   | MQ03ABB200         | 2 TB   | 1       | 468   | 0     | 1.28   |
| Maxtor    | STM380215AS        | 80 GB  | 12      | 679   | 489   | 1.28   |
| WDC       | WD800BEVS-22VAT0   | 80 GB  | 1       | 468   | 0     | 1.28   |
| Seagate   | ST32000646NS       | 2 TB   | 1       | 467   | 0     | 1.28   |
| HGST      | HUH728080ALE600    | 8 TB   | 5       | 465   | 0     | 1.28   |
| Samsung   | SV0221N            | 20 GB  | 1       | 2328  | 4     | 1.28   |
| WDC       | WD5000AAKS-65A7B0  | 500 GB | 7       | 593   | 58    | 1.28   |
| Samsung   | HD252HJ            | 250 GB | 32      | 808   | 115   | 1.28   |
| Toshiba   | HDWE150            | 5 TB   | 15      | 515   | 1     | 1.27   |
| Seagate   | ST2000NM0008-2F... | 2 TB   | 2       | 465   | 0     | 1.27   |
| WDC       | WD10EVDS-63U8B1    | 1 TB   | 1       | 464   | 0     | 1.27   |
| Hitachi   | HDT721064SLA380    | 640 GB | 1       | 464   | 0     | 1.27   |
| Hitachi   | HDS721010CLA330    | 1 TB   | 45      | 732   | 28    | 1.27   |
| WDC       | WD800AAJS-00B4A0   | 80 GB  | 5       | 543   | 3     | 1.27   |
| WDC       | WD5000AVDS-63U7B1  | 500 GB | 12      | 1016  | 51    | 1.27   |
| WDC       | WD60EFRX-68L0BN1   | 6 TB   | 27      | 613   | 7     | 1.27   |
| WDC       | WD1600BEKT-66F3T2  | 160 GB | 1       | 463   | 0     | 1.27   |
| WDC       | WD400BB-00JHC0     | 40 GB  | 5       | 842   | 20    | 1.27   |
| WDC       | WD5000AAKX-07U6AA1 | 500 GB | 2       | 463   | 0     | 1.27   |
| WDC       | WD5000AAKS-00A7B2  | 500 GB | 34      | 864   | 25    | 1.27   |
| Hitachi   | HDS5C3030ALA630    | 3 TB   | 6       | 1155  | 4     | 1.27   |
| WDC       | WD50EZRZ-00RWYB1   | 5 TB   | 1       | 462   | 0     | 1.27   |
| Seagate   | ST3160812A         | 160 GB | 29      | 703   | 359   | 1.27   |
| WDC       | WD5003AZEX-00K1GA0 | 500 GB | 26      | 500   | 42    | 1.27   |
| Seagate   | ST1000DM003-1CH162 | 1 TB   | 377     | 597   | 76    | 1.26   |
| WDC       | WD1001FAES-22W7A0  | 1 TB   | 1       | 460   | 0     | 1.26   |
| WDC       | WD1600AAJS-00V4A0  | 160 GB | 6       | 463   | 13    | 1.26   |
| WDC       | WD10EARS-00Z5B1    | 1 TB   | 11      | 934   | 102   | 1.26   |
| Hitachi   | HDS721025CLA382    | 250 GB | 24      | 758   | 259   | 1.26   |
| Seagate   | ST3500411SV        | 500 GB | 3       | 646   | 25    | 1.26   |
| Hitachi   | HDT725032VLA360    | 320 GB | 17      | 922   | 116   | 1.26   |
| WDC       | WD2500JS-22MHB0    | 250 GB | 4       | 580   | 70    | 1.26   |
| WDC       | WD1600BEVS-22RST0  | 160 GB | 47      | 552   | 78    | 1.26   |
| WDC       | WD5000AAKX-001CA0  | 500 GB | 214     | 768   | 47    | 1.25   |
| Seagate   | ST380817AS         | 80 GB  | 50      | 743   | 9     | 1.25   |
| Seagate   | ST3250620A         | 250 GB | 15      | 687   | 42    | 1.25   |
| WDC       | WD1600AAJS-00B4A0  | 160 GB | 20      | 695   | 70    | 1.25   |
| Toshiba   | MG04ACA100NY       | 1 TB   | 10      | 456   | 0     | 1.25   |
| Seagate   | ST31000520AS       | 1 TB   | 19      | 938   | 318   | 1.25   |
| WDC       | WD2500AABS-00SDA0  | 250 GB | 1       | 455   | 0     | 1.25   |
| Seagate   | ST2000VM003-1CT164 | 2 TB   | 7       | 699   | 617   | 1.24   |
| Hitachi   | HTS723232L9A362    | 320 GB | 2       | 959   | 4     | 1.24   |
| Hitachi   | HTS541610J9SA00    | 100 GB | 2       | 453   | 0     | 1.24   |
| Seagate   | ST2000LM003 HN-... | 2 TB   | 55      | 524   | 4     | 1.24   |
| Seagate   | ST3000VX010-2E3166 | 3 TB   | 6       | 463   | 1     | 1.24   |
| WDC       | WD5000AAKX-75U6AA0 | 500 GB | 28      | 680   | 3     | 1.24   |
| WDC       | WD1600AAJS-08PSA0  | 160 GB | 13      | 718   | 10    | 1.24   |
| WDC       | WD5000MPCK-22AWHT0 | 500 GB | 1       | 452   | 0     | 1.24   |
| WDC       | WD15EARS-00MVWB0   | 1.5 TB | 44      | 894   | 297   | 1.24   |
| WDC       | WD10EARS-00MVWB0   | 1 TB   | 43      | 1001  | 63    | 1.24   |
| WDC       | WD6400BPVT-80HXZT3 | 640 GB | 8       | 690   | 9     | 1.24   |
| Seagate   | ST980813AS         | 80 GB  | 3       | 451   | 0     | 1.24   |
| Toshiba   | MD03ACA300V        | 3 TB   | 1       | 450   | 0     | 1.23   |
| WDC       | WD3200AAJS-08L7A0  | 320 GB | 20      | 860   | 112   | 1.23   |
| Samsung   | HD502HI            | 500 GB | 50      | 880   | 208   | 1.23   |
| Hitachi   | HDS728080PLA380... | 80 GB  | 1       | 449   | 0     | 1.23   |
| Seagate   | ST1500DM003-1CH16G | 1.5 TB | 8       | 478   | 2     | 1.23   |
| WDC       | WD5000BEKT-00KA9T0 | 500 GB | 2       | 1084  | 7     | 1.23   |
| WDC       | WD2500AAJS-00V4A0  | 250 GB | 6       | 742   | 1     | 1.23   |
| ExcelStor | J360               | 64 GB  | 1       | 897   | 1     | 1.23   |
| WDC       | WD5000BEVT-35A0RT0 | 500 GB | 15      | 597   | 7     | 1.23   |
| WDC       | WD10S21X-24R1BT... | 1 TB   | 9       | 448   | 0     | 1.23   |
| WDC       | WD5000AAJS-00TKA0  | 500 GB | 2       | 447   | 0     | 1.23   |
| Hitachi   | HTS541064A9E680    | 640 GB | 3       | 447   | 0     | 1.23   |
| WDC       | WD5000LPVT-22G33T0 | 500 GB | 24      | 540   | 57    | 1.23   |
| WDC       | WD1000CHTZ-04JCPV0 | 1 TB   | 1       | 447   | 0     | 1.23   |
| WDC       | WD15EARX-00ZUDB0   | 1.5 TB | 2       | 776   | 3     | 1.22   |
| Seagate   | ST3000DM008-2DM166 | 3 TB   | 47      | 536   | 101   | 1.22   |
| WDC       | WD3200YS-01PGB0    | 320 GB | 1       | 446   | 0     | 1.22   |
| Seagate   | ST3200820A         | 200 GB | 5       | 491   | 61    | 1.22   |
| Seagate   | ST3250624AS        | 250 GB | 14      | 942   | 101   | 1.22   |
| WDC       | WD800AAJS-75M0A0   | 80 GB  | 6       | 1040  | 7     | 1.22   |
| WDC       | WD1600AAJS-00Z4A0  | 160 GB | 1       | 445   | 0     | 1.22   |
| WDC       | WD10EADS-11M2B2    | 1 TB   | 5       | 828   | 6     | 1.22   |
| Seagate   | ST380013AS         | 80 GB  | 39      | 1209  | 73    | 1.22   |
| Seagate   | ST3500418AS        | 500 GB | 447     | 822   | 173   | 1.22   |
| WDC       | WD740GD-00FLA2     | 74 GB  | 1       | 1330  | 2     | 1.22   |
| WDC       | WD2500BEVS-22UST0  | 250 GB | 60      | 527   | 24    | 1.21   |
| Apple     | HDD ST1000LM024    | 1 TB   | 3       | 887   | 2     | 1.21   |
| WDC       | WD1003FBYX-18Y7B0  | 1 TB   | 3       | 1396  | 9     | 1.21   |
| WDC       | WD30PURX-64P6ZY0   | 3 TB   | 7       | 640   | 19    | 1.21   |
| Seagate   | ST3120022A         | 120 GB | 37      | 648   | 20    | 1.20   |
| Hitachi   | HTS723216L9A362    | 160 GB | 1       | 439   | 0     | 1.20   |
| WDC       | WD2500AAKX-07U6AA0 | 250 GB | 3       | 437   | 0     | 1.20   |
| Seagate   | ST2000DM006-2DM164 | 2 TB   | 157     | 454   | 12    | 1.20   |
| WDC       | WD4003FFBX-68MU3N0 | 4 TB   | 4       | 436   | 0     | 1.20   |
| Seagate   | ST12000NE0007-2... | 12 TB  | 2       | 436   | 0     | 1.20   |
| WDC       | WD7500BPKT-60PK4T0 | 752 GB | 3       | 544   | 3     | 1.19   |
| WDC       | WD5000AAJS-22A8B0  | 500 GB | 1       | 3915  | 8     | 1.19   |
| WDC       | WD40EZRZ-00WN9B0   | 4 TB   | 14      | 525   | 2     | 1.19   |
| WDC       | WD1600AAJS-00L7A0  | 160 GB | 33      | 741   | 3     | 1.19   |
| IBM/Hi... | IC25N020ATCS04-0   | 20 GB  | 1       | 433   | 0     | 1.19   |
| Seagate   | ST3250310AS        | 250 GB | 169     | 945   | 229   | 1.19   |
| WDC       | WD6400AAKS-00H2B0  | 640 GB | 1       | 432   | 0     | 1.19   |
| WDC       | WD1200BEVS-22RST0  | 120 GB | 3       | 458   | 1     | 1.18   |
| WDC       | WD800JD-55MUA1     | 80 GB  | 9       | 615   | 8     | 1.18   |
| WDC       | WD5000BEVT-75A0RT0 | 500 GB | 9       | 697   | 47    | 1.18   |
| WDC       | WD6402AAEX-00Y9A0  | 640 GB | 5       | 578   | 8     | 1.18   |
| WDC       | WD3001FAEX-00MJRA0 | 3 TB   | 5       | 1229  | 3     | 1.18   |
| Hitachi   | HTE545025B9A300    | 250 GB | 1       | 430   | 0     | 1.18   |
| WDC       | WD5000AAKS-22V1A0  | 500 GB | 12      | 758   | 131   | 1.18   |
| Toshiba   | MG04ACA400E        | 4 TB   | 6       | 428   | 0     | 1.17   |
| WDC       | WD5001AALS-00LWTA0 | 500 GB | 7       | 1053  | 43    | 1.17   |
| WDC       | WD5000AADS-00S9B0  | 500 GB | 122     | 787   | 36    | 1.17   |
| Seagate   | ST2000DX001-1CM164 | 2 TB   | 22      | 516   | 165   | 1.17   |
| Seagate   | ST6000VN0041-2E... | 6 TB   | 3       | 425   | 0     | 1.17   |
| WDC       | WD4000AAKS-00TMA0  | 400 GB | 5       | 513   | 1     | 1.17   |
| WDC       | WD1200LB-55EDA0    | 120 GB | 1       | 425   | 0     | 1.17   |
| WDC       | WD5000LUCT-63Y8HY0 | 500 GB | 1       | 424   | 0     | 1.16   |
| Seagate   | ST320014A          | 20 GB  | 8       | 856   | 11    | 1.16   |
| Seagate   | ST1000NM0053-1C... | 1 TB   | 2       | 424   | 0     | 1.16   |
| WDC       | WD5000LMVW-11VEDS0 | 500 GB | 1       | 424   | 0     | 1.16   |
| Fujitsu   | MHV2100AT PL       | 100 GB | 1       | 424   | 0     | 1.16   |
| WDC       | WD1600AAJS-60M0A0  | 160 GB | 4       | 494   | 24    | 1.16   |
| WDC       | WD20EURS-63S48Y0   | 2 TB   | 5       | 897   | 408   | 1.16   |
| Seagate   | ST3500514NS        | 500 GB | 11      | 1278  | 86    | 1.16   |
| Seagate   | ST98823A           | 80 GB  | 5       | 541   | 259   | 1.16   |
| WDC       | WD5000AAKS-22A7B2  | 500 GB | 9       | 1272  | 83    | 1.16   |
| WDC       | WD5000AAJS-22YFA0  | 500 GB | 6       | 781   | 352   | 1.15   |
| Maxtor    | 6V080E0            | 82 GB  | 10      | 749   | 5     | 1.15   |
| WDC       | WD5000AZLX-00CL5A0 | 500 GB | 6       | 465   | 2     | 1.15   |
| WDC       | WD7500BPVT-75A1YT0 | 752 GB | 1       | 419   | 0     | 1.15   |
| WDC       | WD5000BPVT-55HXZT3 | 500 GB | 4       | 471   | 1     | 1.15   |
| WDC       | WD5000BMVV-11SXZS1 | 500 GB | 2       | 1642  | 6     | 1.15   |
| Toshiba   | HDWE160            | 6 TB   | 9       | 418   | 0     | 1.15   |
| WDC       | WD3000FYYZ-05UL1B0 | 3 TB   | 1       | 418   | 0     | 1.15   |
| WDC       | WD5003ABYX-01WERA1 | 500 GB | 9       | 757   | 3     | 1.15   |
| Samsung   | HM501II            | 500 GB | 5       | 672   | 3     | 1.14   |
| WDC       | WD1003FBYX-01Y7B1  | 1 TB   | 30      | 659   | 3     | 1.14   |
| Seagate   | ST1000DM003-9YN162 | 1 TB   | 157     | 681   | 238   | 1.14   |
| Hitachi   | HDP725025GLA380    | 250 GB | 37      | 787   | 73    | 1.14   |
| WDC       | WD5000ABPS-01ZZB0  | 500 GB | 1       | 416   | 0     | 1.14   |
| WDC       | WD1600BEVS-07RST0  | 160 GB | 11      | 457   | 1     | 1.14   |
| Maxtor    | STM3500630AS       | 500 GB | 1       | 416   | 0     | 1.14   |
| WDC       | WD10JPVT-24A1YT0   | 1 TB   | 4       | 489   | 1     | 1.14   |
| WDC       | WD5000BPVT-80HXZT3 | 500 GB | 21      | 469   | 53    | 1.14   |
| WDC       | WD10EARS-00Y5B1    | 1 TB   | 130     | 918   | 116   | 1.14   |
| Toshiba   | MG07ACA14TE        | 14 TB  | 2       | 414   | 0     | 1.14   |
| WDC       | WD1600JS-08MHB0    | 160 GB | 1       | 414   | 0     | 1.14   |
| WDC       | WD30EZRZ-00WN9B0   | 3 TB   | 5       | 414   | 0     | 1.14   |
| Maxtor    | STM3160815AS       | 160 GB | 30      | 697   | 314   | 1.13   |
| Seagate   | ST3250820A         | 250 GB | 11      | 899   | 487   | 1.13   |
| Hitachi   | HDS721032CLA362    | 320 GB | 49      | 718   | 24    | 1.13   |
| Seagate   | ST3160215A         | 160 GB | 20      | 708   | 155   | 1.13   |
| Toshiba   | MQ01UBD100         | 1 TB   | 32      | 523   | 148   | 1.13   |
| Seagate   | ST94813AS          | 40 GB  | 2       | 412   | 0     | 1.13   |
| Maxtor    | STM380211AS        | 80 GB  | 6       | 636   | 919   | 1.13   |
| Fujitsu   | MHZ2250BH G1       | 250 GB | 8       | 434   | 4     | 1.13   |
| WDC       | WD5000BMVW-11AJGS1 | 500 GB | 1       | 411   | 0     | 1.13   |
| Seagate   | ST9200420AS        | 200 GB | 3       | 571   | 6     | 1.13   |
| Toshiba   | MK1234GAX          | 120 GB | 3       | 410   | 0     | 1.13   |
| Maxtor    | 6V320F0            | 320 GB | 1       | 410   | 0     | 1.13   |
| Seagate   | ST3160215AS        | 160 GB | 18      | 627   | 477   | 1.12   |
| WDC       | WD3200BEVT-22ZCT0  | 320 GB | 104     | 491   | 84    | 1.12   |
| Seagate   | ST3200827AS        | 200 GB | 28      | 785   | 289   | 1.12   |
| WDC       | WD1600BEVS-26VAT0  | 160 GB | 3       | 409   | 0     | 1.12   |
| Seagate   | ST31000523AS       | 1 TB   | 3       | 1683  | 7     | 1.12   |
| WDC       | WD10JPVT-08A1YT1   | 1 TB   | 2       | 408   | 0     | 1.12   |
| WDC       | WD6400AAKS-22A7B2  | 640 GB | 27      | 760   | 16    | 1.12   |
| Seagate   | ST380819AS         | 80 GB  | 3       | 781   | 682   | 1.12   |
| Seagate   | ST31000340NS       | 1 TB   | 20      | 1392  | 345   | 1.12   |
| Seagate   | ST9500420ASG       | 500 GB | 5       | 676   | 204   | 1.12   |
| WDC       | WD800EB-11DJF0     | 80 GB  | 1       | 407   | 0     | 1.12   |
| WDC       | WD2000JB-00KFA0    | 200 GB | 1       | 1220  | 2     | 1.11   |
| WDC       | WD2500JD-00HBB0    | 250 GB | 1       | 406   | 0     | 1.11   |
| Hitachi   | HDS721075CLA332    | 752 GB | 3       | 497   | 672   | 1.11   |
| WDC       | WD1600BEVT-75ZCT2  | 160 GB | 15      | 532   | 138   | 1.11   |
| Hitachi   | HDT721064SLA360    | 640 GB | 8       | 935   | 57    | 1.11   |
| WDC       | WD10EZEX-00UD2A0   | 1 TB   | 10      | 497   | 88    | 1.11   |
| Seagate   | ST3120827AS        | 120 GB | 47      | 730   | 10    | 1.11   |
| Maxtor    | STM3320820AS       | 320 GB | 19      | 737   | 267   | 1.11   |
| Hitachi   | HTS721080G9AT00    | 80 GB  | 1       | 405   | 0     | 1.11   |
| Samsung   | HD322HJ            | 320 GB | 64      | 770   | 176   | 1.11   |
| Seagate   | ST3000VX000-9YW166 | 3 TB   | 1       | 405   | 0     | 1.11   |
| WDC       | WD2500AAKS-00V6A0  | 250 GB | 1       | 404   | 0     | 1.11   |
| Samsung   | HE161HJ            | 160 GB | 1       | 1213  | 2     | 1.11   |
| WDC       | WD5000AAKX-00ERMA0 | 500 GB | 128     | 568   | 10    | 1.11   |
| Seagate   | ST3160827AS        | 160 GB | 26      | 951   | 203   | 1.11   |
| WDC       | WD2500BEVT-22ZCT0  | 250 GB | 45      | 506   | 66    | 1.10   |
| Samsung   | HD322GJ            | 320 GB | 42      | 648   | 84    | 1.10   |
| Seagate   | ST3250624A         | 250 GB | 1       | 1205  | 2     | 1.10   |
| HGST      | HUS726040ALE611    | 4 TB   | 1       | 401   | 0     | 1.10   |
| WDC       | WD5000AVKX-635FY0  | 500 GB | 1       | 401   | 0     | 1.10   |
| WDC       | WD1001FALS-40K1B0  | 1 TB   | 4       | 933   | 4     | 1.10   |
| WDC       | WD5003ABYX-23 8... | 500 GB | 2       | 668   | 2     | 1.10   |
| Quantum   | FIREBALLlct20 40   | 40 GB  | 1       | 400   | 0     | 1.10   |
| Fujitsu   | MJA2160BH FFS G1   | 160 GB | 2       | 400   | 0     | 1.10   |
| WDC       | WD2500AAKS-00VYA0  | 250 GB | 4       | 468   | 1     | 1.10   |
| Seagate   | ST5000LM000-2AN170 | 5 TB   | 17      | 400   | 0     | 1.10   |
| Seagate   | ST8000NE0021-2E... | 8 TB   | 1       | 399   | 0     | 1.10   |
| WDC       | WD10EADS-11P8B2    | 1 TB   | 1       | 799   | 1     | 1.10   |
| WDC       | WD5000BEVT-26A0RT0 | 500 GB | 3       | 579   | 214   | 1.09   |
| WDC       | WD10EZEX-19ZF5A0   | 1 TB   | 1       | 399   | 0     | 1.09   |
| Hitachi   | HTS543280L9SA00    | 80 GB  | 1       | 398   | 0     | 1.09   |
| WDC       | WD30EZRZ-00Z5HB0   | 3 TB   | 31      | 492   | 5     | 1.09   |
| WDC       | WD5000BPKT-22PK4T0 | 500 GB | 2       | 398   | 0     | 1.09   |
| WDC       | WD20NMVW-11EDZS6   | 2 TB   | 14      | 423   | 1     | 1.09   |
| WDC       | WD2500JS-57MHB1    | 250 GB | 1       | 397   | 0     | 1.09   |
| WDC       | WD6003FZBX-00K5WB0 | 6 TB   | 5       | 397   | 0     | 1.09   |
| Seagate   | ST320410A          | 20 GB  | 7       | 791   | 12    | 1.09   |
| Fujitsu   | MJA2250BH FFS G1   | 250 GB | 3       | 397   | 0     | 1.09   |
| WDC       | WD1200BEVS-22UST0  | 120 GB | 27      | 498   | 60    | 1.09   |
| WDC       | WD3200BEVS-08VAT2  | 320 GB | 4       | 592   | 280   | 1.09   |
| WDC       | WD3200AAKS-00L6A0  | 320 GB | 3       | 579   | 4     | 1.09   |
| Hitachi   | HDP725040GLA360    | 400 GB | 7       | 801   | 187   | 1.08   |
| Seagate   | ST3000VN007-2E4166 | 3 TB   | 3       | 395   | 0     | 1.08   |
| WDC       | WD10JPVX-08JC3T2   | 1 TB   | 6       | 409   | 1     | 1.08   |
| WDC       | WD1600AABS-00H4A0  | 160 GB | 2       | 432   | 6     | 1.08   |
| WDC       | WD1600AAJS-75PSA0  | 160 GB | 6       | 517   | 2     | 1.08   |
| Seagate   | ST320LM000 HM321HI | 320 GB | 13      | 410   | 2     | 1.08   |
| WDC       | WD10EZRX-00D8PB0   | 1 TB   | 22      | 440   | 2     | 1.08   |
| WDC       | WD5000BMVW-11AJGS3 | 500 GB | 1       | 394   | 0     | 1.08   |
| WDC       | WD5000BEKT-75KA9T0 | 500 GB | 4       | 735   | 2     | 1.08   |
| WDC       | WD2001FASS-00U0B0  | 2 TB   | 1       | 1578  | 3     | 1.08   |
| Seagate   | ST9200420ASG       | 200 GB | 2       | 393   | 0     | 1.08   |
| HGST      | HUS722T1TALA600    | 1 TB   | 2       | 393   | 0     | 1.08   |
| WDC       | WD1003FBYX-05Y7B0  | 1 TB   | 2       | 433   | 883   | 1.08   |
| WDC       | WD1001FALS-00E8B0  | 1 TB   | 13      | 902   | 173   | 1.08   |
| Fujitsu   | MHW2160BH          | 160 GB | 6       | 505   | 15    | 1.07   |
| Seagate   | ST14000NM0018-2... | 14 TB  | 1       | 391   | 0     | 1.07   |
| Seagate   | ST1500DL003-9VT16L | 1.5 TB | 41      | 815   | 266   | 1.07   |
| Seagate   | ST320DM000-1BC14C  | 320 GB | 16      | 505   | 15    | 1.07   |
| WDC       | WD20EARX-32PASB0   | 2 TB   | 3       | 391   | 0     | 1.07   |
| WDC       | WD7500BPVT-24HXZT3 | 752 GB | 13      | 424   | 20    | 1.07   |
| Samsung   | HM251HI            | 250 GB | 5       | 491   | 2     | 1.07   |
| Maxtor    | STM3250820A        | 250 GB | 7       | 548   | 187   | 1.07   |
| WDC       | WD2000FYYZ-01UL1B1 | 2 TB   | 13      | 1092  | 149   | 1.07   |
| WDC       | WD10JMVW-11AJGS3   | 1 TB   | 16      | 403   | 2     | 1.07   |
| Fujitsu   | MHV2040AH          | 40 GB  | 4       | 749   | 5     | 1.07   |
| Hitachi   | HTS723216A7A364    | 160 GB | 1       | 389   | 0     | 1.07   |
| Toshiba   | MK1234GSX          | 120 GB | 9       | 665   | 4     | 1.07   |
| Seagate   | ST3250318AS        | 250 GB | 129     | 713   | 120   | 1.07   |
| WDC       | WD2500AVJS-63WDA0  | 250 GB | 3       | 388   | 1     | 1.06   |
| Seagate   | ST31000524AS       | 1 TB   | 230     | 685   | 222   | 1.06   |
| WDC       | WD5000AAKS-00WWPA0 | 500 GB | 9       | 629   | 10    | 1.06   |
| WDC       | WD10SPCX-75KHST0   | 1 TB   | 6       | 386   | 0     | 1.06   |
| WDC       | WD3200AAJS-22L7A0  | 320 GB | 9       | 776   | 27    | 1.06   |
| WDC       | WD10JMVW-11AJGS2   | 1 TB   | 19      | 562   | 9     | 1.06   |
| Seagate   | ST380811AS         | 80 GB  | 69      | 622   | 470   | 1.06   |
| WDC       | WD5000AZLX-21K2TA0 | 500 GB | 4       | 384   | 0     | 1.05   |
| Seagate   | ST3250820ACE       | 250 GB | 3       | 520   | 698   | 1.05   |
| Toshiba   | DT01ACA100         | 1 TB   | 394     | 430   | 17    | 1.05   |
| WDC       | WD10EZRZ-00Z5HB0   | 1 TB   | 5       | 384   | 0     | 1.05   |
| WDC       | WD5000BEVT-00A03T0 | 500 GB | 3       | 384   | 0     | 1.05   |
| WDC       | WD800BEVT-75ZCT2   | 80 GB  | 3       | 383   | 0     | 1.05   |
| WDC       | WD2000FYYZ-05UL1B0 | 2 TB   | 1       | 383   | 0     | 1.05   |
| Seagate   | ST10000NM0156-2... | 10 TB  | 14      | 383   | 0     | 1.05   |
| WDC       | WD101KRYZ-01JPDB1  | 10 TB  | 2       | 383   | 0     | 1.05   |
| WDC       | WD3200AAJS-22B4A0  | 320 GB | 10      | 1164  | 5     | 1.05   |
| WDC       | WD800JD-22JNA0     | 80 GB  | 1       | 383   | 0     | 1.05   |
| WDC       | WD1600JS-08NCB1    | 160 GB | 5       | 565   | 27    | 1.05   |
| WDC       | WD800BB-75JHC0     | 80 GB  | 2       | 382   | 0     | 1.05   |
| Seagate   | ST500DM002-1BC142  | 500 GB | 62      | 616   | 155   | 1.05   |
| Fujitsu   | MHV2060BH          | 64 GB  | 9       | 566   | 7     | 1.05   |
| Samsung   | HD501LJ            | 500 GB | 75      | 1060  | 444   | 1.05   |
| Toshiba   | MK2559GSXP         | 250 GB | 4       | 450   | 7     | 1.05   |
| Samsung   | HD753LJ            | 752 GB | 40      | 1073  | 215   | 1.05   |
| WDC       | WD3200AAKX-00ERMA0 | 320 GB | 13      | 548   | 3     | 1.05   |
| Seagate   | ST31000525SV       | 1 TB   | 3       | 769   | 20    | 1.05   |
| WDC       | WD2000JD-22HBB0    | 200 GB | 3       | 993   | 7     | 1.04   |
| Samsung   | HM500JI            | 500 GB | 43      | 526   | 5     | 1.04   |
| Toshiba   | MQ01UBD050         | 500 GB | 5       | 431   | 230   | 1.04   |
| Seagate   | ST980813ASG        | 80 GB  | 4       | 498   | 3     | 1.04   |
| WDC       | WD3200AAKX-001CA0  | 320 GB | 35      | 750   | 70    | 1.04   |
| WDC       | WD20EARX-55PASB0   | 2 TB   | 3       | 380   | 0     | 1.04   |
| WDC       | WD5000LPLX-60ZNTT2 | 500 GB | 1       | 380   | 0     | 1.04   |
| WDC       | WD40E31X-00HY4A0   | 4 TB   | 1       | 380   | 0     | 1.04   |
| WDC       | WD3200AAJS-60Z0A0  | 320 GB | 7       | 682   | 36    | 1.04   |
| Seagate   | ST2000NC001-1DY164 | 2 TB   | 5       | 378   | 0     | 1.04   |
| WDC       | WD5000AAKX-22ERMA0 | 500 GB | 50      | 517   | 2     | 1.03   |
| WDC       | WD2000JS-00SGB0    | 200 GB | 1       | 377   | 0     | 1.03   |
| Seagate   | ST6000NM0115-1Y... | 6 TB   | 7       | 376   | 0     | 1.03   |
| WDC       | WD800AAJS-22WAA0   | 80 GB  | 2       | 376   | 0     | 1.03   |
| Fujitsu   | MHZ2160BH FFS G1   | 160 GB | 3       | 547   | 1     | 1.03   |
| Hitachi   | HDS721050CLA360    | 500 GB | 72      | 533   | 34    | 1.03   |
| Toshiba   | MK1665GSX H        | 160 GB | 2       | 375   | 0     | 1.03   |
| WDC       | WD3200BEVT-11ZCT0  | 320 GB | 4       | 378   | 1     | 1.03   |
| WDC       | WD2500AAJB-00J3A0  | 250 GB | 11      | 693   | 7     | 1.03   |
| WDC       | WD800BB-00JKA0     | 80 GB  | 1       | 374   | 0     | 1.03   |
| WDC       | WD7500BPKT-80PK4T0 | 752 GB | 5       | 781   | 5     | 1.03   |
| WDC       | WD2500BEKT-75PVMT1 | 250 GB | 2       | 643   | 5     | 1.03   |
| WDC       | WD1600AAJS-98PSA0  | 160 GB | 4       | 440   | 1     | 1.02   |
| WDC       | WD5000AAKX-221CA1  | 500 GB | 14      | 644   | 21    | 1.02   |
| Seagate   | ST3320820AS        | 320 GB | 21      | 540   | 376   | 1.02   |
| HGST      | HTS725032A7E630    | 320 GB | 23      | 438   | 223   | 1.02   |
| WDC       | WD5000AVCS-982DY1  | 500 GB | 1       | 372   | 0     | 1.02   |
| WDC       | WD7500BPKT-22PK4T0 | 752 GB | 9       | 372   | 0     | 1.02   |
| Seagate   | ST9402112A         | 40 GB  | 1       | 1117  | 2     | 1.02   |
| WDC       | WD1600JS-22NCB1    | 160 GB | 4       | 712   | 6     | 1.02   |
| WDC       | WD3200AAKS-00SBA0  | 320 GB | 12      | 655   | 20    | 1.02   |
| WDC       | WD2500BEVT-35ZCT0  | 250 GB | 2       | 845   | 225   | 1.02   |
| Apple     | HDD HTS545050A7... | 500 GB | 27      | 396   | 9     | 1.02   |
| Fujitsu   | MJA2320BH G2       | 320 GB | 9       | 860   | 347   | 1.02   |
| WDC       | WD2500AAKX-00U6AA0 | 250 GB | 3       | 373   | 3     | 1.01   |
| Samsung   | HD203WI            | 2 TB   | 4       | 369   | 0     | 1.01   |
| WDC       | WD3200BEKT-60KA9T0 | 320 GB | 1       | 369   | 0     | 1.01   |
| WDC       | WD3200AVJS-63N9A0  | 320 GB | 5       | 369   | 0     | 1.01   |
| WDC       | WD10EZEX-60ZF5A0   | 1 TB   | 53      | 540   | 97    | 1.01   |
| WDC       | WD3200BEKT-00KA9T0 | 320 GB | 1       | 369   | 0     | 1.01   |
| Seagate   | ST750LX003-1AC154  | 752 GB | 17      | 429   | 109   | 1.01   |
| Hitachi   | HDS721680PLA380    | 80 GB  | 51      | 866   | 205   | 1.01   |
| WDC       | WD20NMVW-11AV3S3   | 2 TB   | 4       | 546   | 5     | 1.01   |
| Hitachi   | HDS721680PLAT80    | 80 GB  | 6       | 1080  | 5     | 1.01   |
| WDC       | WD60EZRX-11MVLB1   | 6 TB   | 1       | 366   | 0     | 1.01   |
| Seagate   | ST4000DM000-2AE166 | 4 TB   | 8       | 366   | 0     | 1.01   |
| WDC       | WD20NMVW-11EDZS7   | 2 TB   | 12      | 441   | 102   | 1.01   |
| Hitachi   | HDT722525DLA380    | 250 GB | 15      | 1135  | 156   | 1.00   |
| Seagate   | ST3750525AS        | 752 GB | 20      | 714   | 215   | 1.00   |
| WDC       | WD10JUCT-63CYNY0   | 1 TB   | 4       | 784   | 2     | 1.00   |
| WDC       | WD1600AAJS-00WAA0  | 160 GB | 11      | 487   | 4     | 1.00   |
| Hitachi   | HDS721064CLA332    | 640 GB | 1       | 364   | 0     | 1.00   |
| WDC       | WD5000AAKS-41YGA1  | 500 GB | 1       | 728   | 1     | 1.00   |
| WDC       | WD1600JS-00MHB0    | 160 GB | 8       | 709   | 146   | 1.00   |
| Seagate   | ST500VT000-1DK142  | 500 GB | 18      | 363   | 0     | 1.00   |
| WDC       | WD5000BPKT-60PK4T0 | 500 GB | 8       | 543   | 36    | 1.00   |
| WDC       | WD2500BEVT-35A23T0 | 250 GB | 25      | 507   | 26    | 1.00   |
| Samsung   | SP1654N            | 160 GB | 8       | 849   | 412   | 0.99   |
| WDC       | WD1600AAJS-75M0A0  | 160 GB | 14      | 860   | 81    | 0.99   |
| Seagate   | ST9640423AS        | 640 GB | 4       | 949   | 380   | 0.99   |
| Seagate   | ST3802110A         | 80 GB  | 38      | 644   | 486   | 0.99   |
| WDC       | WD10SPCX-08S8TT0   | 1 TB   | 4       | 360   | 0     | 0.99   |
| Seagate   | ST3160023AS        | 160 GB | 15      | 983   | 34    | 0.99   |
| Toshiba   | HDWQ140            | 4 TB   | 14      | 388   | 1     | 0.99   |
| WDC       | WD3200AAKB-00WHA0  | 320 GB | 1       | 360   | 0     | 0.99   |
| WDC       | WD740GD-00FLA0     | 74 GB  | 1       | 2521  | 6     | 0.99   |
| Maxtor    | STM3160212A        | 160 GB | 2       | 817   | 1     | 0.99   |
| Toshiba   | MK5075GSX          | 500 GB | 26      | 501   | 274   | 0.99   |
| WDC       | WD800BB-00JHC0     | 80 GB  | 24      | 588   | 75    | 0.98   |
| WDC       | WD5000BPKX-00HPJT0 | 500 GB | 3       | 359   | 0     | 0.98   |
| WDC       | WD20EURS-73TLHY0   | 2 TB   | 1       | 1437  | 3     | 0.98   |
| WDC       | WD4004FZWX-00GBGB0 | 4 TB   | 5       | 611   | 477   | 0.98   |
| WDC       | WD3200BPVT-00JJ5T0 | 320 GB | 14      | 585   | 153   | 0.98   |
| Seagate   | ST500DM005 HD502HJ | 500 GB | 42      | 479   | 10    | 0.98   |
| WDC       | WD3200AVVS-56L2B0  | 320 GB | 10      | 524   | 57    | 0.98   |
| Samsung   | HD251HJ            | 250 GB | 10      | 736   | 45    | 0.98   |
| Seagate   | ST3250310NS        | 250 GB | 3       | 737   | 755   | 0.98   |
| Fujitsu   | MHW2120BJ G2       | 120 GB | 1       | 356   | 0     | 0.98   |
| Fujitsu   | MHW2060BH          | 64 GB  | 4       | 743   | 4     | 0.97   |
| WDC       | WD5000BPKT-75PK4T0 | 500 GB | 15      | 523   | 3     | 0.97   |
| Seagate   | ST2000VN004-2E4164 | 2 TB   | 9       | 508   | 3     | 0.97   |
| WDC       | WD15EVDS-63V9B1    | 1.5 TB | 2       | 1117  | 6     | 0.97   |
| Seagate   | ST3250410AS        | 250 GB | 185     | 849   | 290   | 0.97   |
| WDC       | WD3200AAJS-00M0A0  | 320 GB | 2       | 574   | 1     | 0.97   |
| Toshiba   | MK3261GSYG         | 320 GB | 1       | 354   | 0     | 0.97   |
| Samsung   | HD403LJ            | 400 GB | 20      | 1211  | 513   | 0.97   |
| Hitachi   | HTS545032B9A301    | 320 GB | 1       | 353   | 0     | 0.97   |
| HGST      | HUH721010ALN600    | 10 TB  | 2       | 353   | 0     | 0.97   |
| WDC       | WD6400AACS-00M3B0  | 640 GB | 1       | 352   | 0     | 0.97   |
| Hitachi   | HTS725050A9A362    | 500 GB | 4       | 468   | 78    | 0.96   |
| WDC       | WD7500BPKT-00PK4T0 | 752 GB | 4       | 633   | 1     | 0.96   |
| Fujitsu   | MHW2080BH PL       | 80 GB  | 7       | 604   | 149   | 0.96   |
| WDC       | WD7500BPKX-80HPJT0 | 752 GB | 5       | 351   | 0     | 0.96   |
| WDC       | WD50PURX-64T0ZY0   | 5 TB   | 1       | 349   | 0     | 0.96   |
| WDC       | WD800JB-00JJC0     | 80 GB  | 22      | 630   | 25    | 0.96   |
| WDC       | WD7500BPVT-80HXZT3 | 752 GB | 17      | 473   | 17    | 0.96   |
| Seagate   | ST3120814A         | 120 GB | 19      | 735   | 307   | 0.95   |
| Seagate   | ST320DM001 HD322GJ | 320 GB | 6       | 634   | 74    | 0.95   |
| HGST      | HUS726060ALE614    | 6 TB   | 7       | 383   | 81    | 0.95   |
| ExcelStor | J880S              | 82 GB  | 3       | 733   | 8     | 0.95   |
| Seagate   | ST2000VM003-1ET164 | 2 TB   | 7       | 347   | 0     | 0.95   |
| Seagate   | ST6000DM0003       | 6 TB   | 1       | 346   | 0     | 0.95   |
| WDC       | WD6400BPVT-16HXZT1 | 640 GB | 1       | 1037  | 2     | 0.95   |
| WDC       | WD3200JS-22PDB0    | 320 GB | 2       | 1081  | 11    | 0.95   |
| WDC       | WD3200BPVT-35ZEST0 | 320 GB | 22      | 468   | 2     | 0.95   |
| WDC       | WD5000BUCT-63LS5Y1 | 500 GB | 1       | 345   | 0     | 0.95   |
| WDC       | WD3200AZRX-00A8LB0 | 320 GB | 4       | 345   | 0     | 0.95   |
| WDC       | WD3200AAJS-00B4A0  | 320 GB | 22      | 801   | 103   | 0.94   |
| Seagate   | ST1000DX001-1NS162 | 1 TB   | 12      | 601   | 28    | 0.94   |
| WDC       | WD5000AAKS-00UU3A0 | 500 GB | 63      | 725   | 60    | 0.94   |
| WDC       | WD800BB-22JHC0     | 80 GB  | 11      | 504   | 34    | 0.94   |
| WDC       | WD60EFAX-68SHWN0   | 6 TB   | 1       | 343   | 0     | 0.94   |
| WDC       | WD1600BEVT-22ZCT0  | 160 GB | 108     | 456   | 67    | 0.94   |
| Seagate   | ST3000VX000-1CU166 | 3 TB   | 6       | 345   | 10    | 0.94   |
| Seagate   | ST8000NM0055-1R... | 8 TB   | 6       | 343   | 0     | 0.94   |
| WDC       | WD20EZRZ-22Z5HB0   | 2 TB   | 9       | 343   | 0     | 0.94   |
| WDC       | WD2500AVVS-62L2B0  | 250 GB | 2       | 347   | 5     | 0.94   |
| WDC       | WD1600BEVT-00A23T0 | 160 GB | 5       | 423   | 105   | 0.94   |
| Seagate   | ST500LX012-SSHD... | 500 GB | 4       | 378   | 1     | 0.94   |
| WDC       | WD2500BEVS-60UST0  | 250 GB | 10      | 566   | 214   | 0.94   |
| WDC       | WD5000AAKX-07U6AA0 | 500 GB | 7       | 480   | 3     | 0.94   |
| WDC       | WD2500AAKX-08U6AA0 | 250 GB | 7       | 462   | 3     | 0.94   |
| Seagate   | ST96812AS          | 64 GB  | 9       | 468   | 210   | 0.93   |
| WDC       | WD6400BPVT-55HXZT2 | 640 GB | 1       | 340   | 0     | 0.93   |
| WDC       | WD15EARX-22PASB0   | 1.5 TB | 1       | 340   | 0     | 0.93   |
| WDC       | WD5000LPVT-75G33T0 | 500 GB | 6       | 376   | 1     | 0.93   |
| Seagate   | ST1000VM002-1SD102 | 1 TB   | 5       | 339   | 0     | 0.93   |
| Seagate   | ST31000528AS       | 1 TB   | 240     | 728   | 255   | 0.93   |
| WDC       | WD800JD-32LSA0     | 80 GB  | 2       | 1577  | 53    | 0.93   |
| WDC       | WD2003FYYS-01T8B0  | 2 TB   | 1       | 3050  | 8     | 0.93   |
| HP        | GB0250C8045        | 250 GB | 2       | 1373  | 100   | 0.93   |
| Seagate   | ST2000DM009-2G4100 | 2 TB   | 5       | 338   | 0     | 0.93   |
| WDC       | WD10EALX-008EA0    | 1 TB   | 6       | 346   | 1     | 0.93   |
| Samsung   | HM120JC            | 120 GB | 2       | 638   | 51    | 0.93   |
| WDC       | WD1600BEVT-26A23T0 | 160 GB | 1       | 338   | 0     | 0.93   |
| WDC       | WD7500BPVX-22JC3T0 | 752 GB | 20      | 406   | 1     | 0.92   |
| ExcelStor | J680               | 82 GB  | 1       | 1687  | 4     | 0.92   |
| IBM/Hi... | IC35L090AVV207-0   | 80 GB  | 2       | 735   | 2     | 0.92   |
| Seagate   | ST3160811AS        | 160 GB | 84      | 784   | 443   | 0.92   |
| HGST      | HTS721075A9E630    | 752 GB | 10      | 354   | 122   | 0.92   |
| WDC       | WD80EMAZ-00M9AA0   | 8 TB   | 1       | 336   | 0     | 0.92   |
| Apple     | HDD HTS541010A9... | 1 TB   | 7       | 418   | 2     | 0.92   |
| Seagate   | ST250DM000-1BD141  | 250 GB | 108     | 558   | 120   | 0.92   |
| WDC       | WD2500AAJS-55M0A0  | 250 GB | 3       | 416   | 3     | 0.92   |
| WDC       | WD6400BEVT-00A0RT0 | 640 GB | 2       | 542   | 4     | 0.92   |
| Toshiba   | MG04ACA400EY       | 4 TB   | 2       | 335   | 0     | 0.92   |
| Fujitsu   | MHV2100BH          | 100 GB | 5       | 680   | 22    | 0.92   |
| WDC       | WD5000AADS-00M2B0  | 500 GB | 29      | 934   | 185   | 0.92   |
| Seagate   | ST9320310AS        | 320 GB | 10      | 631   | 393   | 0.92   |
| Seagate   | ST500DM002-1BD142  | 500 GB | 684     | 573   | 110   | 0.92   |
| Seagate   | ST1000NC001-1DY162 | 1 TB   | 5       | 652   | 202   | 0.92   |
| WDC       | WD3200BPVT-16JJ5T0 | 320 GB | 6       | 380   | 1     | 0.92   |
| Samsung   | HD161GJ            | 160 GB | 29      | 679   | 215   | 0.92   |
| WDC       | WD5000BHTZ-04JCPV0 | 500 GB | 1       | 334   | 0     | 0.92   |
| WDC       | WD10JPVT-60A1YT0   | 1 TB   | 3       | 403   | 337   | 0.92   |
| Seagate   | ST9160412AS        | 160 GB | 14      | 634   | 338   | 0.91   |
| WDC       | WD30EZRX-22D8PB0   | 3 TB   | 2       | 333   | 0     | 0.91   |
| WDC       | WD80EMAZ-00WJTA0   | 8 TB   | 23      | 333   | 0     | 0.91   |
| Maxtor    | STM3160215AS       | 160 GB | 29      | 795   | 637   | 0.91   |
| WDC       | WD4002FYYZ-01B7CB1 | 4 TB   | 2       | 332   | 0     | 0.91   |
| WDC       | WD3200AAKS-00V1A0  | 320 GB | 8       | 773   | 203   | 0.91   |
| Seagate   | ST3160211AS        | 160 GB | 11      | 658   | 799   | 0.91   |
| Hitachi   | HDP725032GLA380    | 320 GB | 8       | 925   | 28    | 0.91   |
| WDC       | WD5000BEVT-24A0RT0 | 500 GB | 24      | 525   | 19    | 0.91   |
| WDC       | WD6400BPVT-00HXZT1 | 640 GB | 4       | 331   | 0     | 0.91   |
| Seagate   | ST250DM001 HD253GJ | 250 GB | 7       | 330   | 0     | 0.91   |
| Fujitsu   | MHV2120AH          | 120 GB | 3       | 418   | 2     | 0.91   |
| Seagate   | ST1000DX001-1CM162 | 1 TB   | 42      | 519   | 86    | 0.90   |
| Seagate   | ST9320328CS        | 320 GB | 10      | 743   | 182   | 0.90   |
| Seagate   | STM3250318AS       | 250 GB | 27      | 624   | 168   | 0.90   |
| Seagate   | ST3160021A         | 160 GB | 14      | 648   | 437   | 0.90   |
| WDC       | WD5000LPVT-08G33T1 | 500 GB | 16      | 394   | 1     | 0.90   |
| Seagate   | ST3160813AS        | 160 GB | 41      | 835   | 130   | 0.90   |
| WDC       | WD5000LPVT-24G33T1 | 500 GB | 21      | 392   | 29    | 0.90   |
| WDC       | WD3200LPVX-80V0TT0 | 320 GB | 2       | 328   | 0     | 0.90   |
| WDC       | WD2500AVJS-63B6A0  | 250 GB | 3       | 768   | 6     | 0.90   |
| HGST      | HDS724020ALE640    | 2 TB   | 1       | 328   | 0     | 0.90   |
| Fujitsu   | MHW2080BH          | 80 GB  | 7       | 428   | 3     | 0.90   |
| Seagate   | ST250LT020-1AE14C  | 250 GB | 3       | 409   | 314   | 0.90   |
| WDC       | WD7500BPVT-24HXZT1 | 752 GB | 12      | 605   | 88    | 0.90   |
| Hitachi   | HTS545016B9SA00    | 160 GB | 1       | 327   | 0     | 0.90   |
| WDC       | WD2500AAJS-00Z0A0  | 250 GB | 3       | 819   | 4     | 0.90   |
| WDC       | WD5000AAJS-19A8B0  | 500 GB | 1       | 326   | 0     | 0.90   |
| WDC       | WD5000LPLX-66ZNTT0 | 500 GB | 1       | 326   | 0     | 0.89   |
| WDC       | WD1600BEVS-08RST2  | 160 GB | 2       | 326   | 0     | 0.89   |
| Fujitsu   | MHV2080AT PL       | 80 GB  | 4       | 515   | 569   | 0.89   |
| WDC       | WD10EZEX-00M2NA0   | 1 TB   | 3       | 383   | 12    | 0.89   |
| WDC       | WD6400BPVT-55HXZT3 | 640 GB | 2       | 591   | 4     | 0.89   |
| WDC       | WD2500BEKT-60PVMT0 | 250 GB | 13      | 402   | 78    | 0.89   |
| WDC       | WD7501AALS-00E3A0  | 752 GB | 9       | 733   | 41    | 0.89   |
| WDC       | WD2503ABYZ-011FA0  | 256 GB | 1       | 325   | 0     | 0.89   |
| WDC       | WD2500JS-60MHB5    | 250 GB | 3       | 946   | 13    | 0.89   |
| WDC       | WD100EMAZ-00WJTA0  | 10 TB  | 29      | 325   | 0     | 0.89   |
| WDC       | WD1600AAJS-22L7A0  | 160 GB | 15      | 543   | 7     | 0.89   |
| WDC       | WD10EZEX-00WN4A0   | 1 TB   | 75      | 360   | 7     | 0.89   |
| WDC       | WD7500BPVT-22HXZT3 | 752 GB | 31      | 384   | 1     | 0.89   |
| WDC       | WD800BB-60JKA0     | 80 GB  | 1       | 325   | 0     | 0.89   |
| Toshiba   | MQ01ACF032         | 320 GB | 19      | 401   | 1     | 0.89   |
| WDC       | WD5000BPVT-16HXZT3 | 500 GB | 1       | 324   | 0     | 0.89   |
| WDC       | WD5000BPVT-22HXZT3 | 500 GB | 50      | 437   | 32    | 0.89   |
| WDC       | WD3200JS-00PDB0    | 320 GB | 1       | 324   | 0     | 0.89   |
| Fujitsu   | MHZ2160BH G2       | 160 GB | 36      | 573   | 383   | 0.89   |
| WDC       | WD3200BEVT-08A23T1 | 320 GB | 10      | 573   | 107   | 0.89   |
| Seagate   | ST320DM000-1BD14C  | 320 GB | 36      | 477   | 99    | 0.89   |
| Seagate   | ST3200822AS        | 200 GB | 19      | 856   | 220   | 0.89   |
| WDC       | WD2500JS-58NCB1    | 250 GB | 2       | 773   | 308   | 0.89   |
| WDC       | WD2500BEVS-75UST0  | 250 GB | 10      | 462   | 2     | 0.89   |
| Hitachi   | HTS545050B9A300    | 500 GB | 137     | 597   | 219   | 0.89   |
| Fujitsu   | MJA2160BH G2       | 160 GB | 8       | 474   | 285   | 0.89   |
| Hitachi   | HCP725032GLA380    | 320 GB | 3       | 761   | 2     | 0.88   |
| Seagate   | ST3250824A         | 250 GB | 4       | 753   | 253   | 0.88   |
| WDC       | WD5000AAKS-55V0A0  | 500 GB | 7       | 568   | 6     | 0.88   |
| Seagate   | ST250DM000-1BC141  | 250 GB | 15      | 369   | 7     | 0.88   |
| WDC       | WD8003FRYZ-01JPDB1 | 8 TB   | 2       | 322   | 0     | 0.88   |
| WDC       | WD1600AAJS-08L7A0  | 160 GB | 10      | 1023  | 130   | 0.88   |
| WDC       | WD3200BVVT-63A26Y0 | 320 GB | 5       | 359   | 132   | 0.88   |
| WDC       | WD5000AAKX-08U6AA0 | 500 GB | 52      | 447   | 6     | 0.88   |
| WDC       | WD800BEVT-22ZCT0   | 80 GB  | 1       | 321   | 0     | 0.88   |
| WDC       | WD2500AAJS-08B4A0  | 250 GB | 2       | 931   | 1211  | 0.88   |
| Hitachi   | HTS725016A9A364    | 160 GB | 12      | 530   | 453   | 0.88   |
| WDC       | WD10JPVT-55A1YT0   | 1 TB   | 1       | 320   | 0     | 0.88   |
| WDC       | WD1003FZEX-00K3CA0 | 1 TB   | 33      | 329   | 1     | 0.88   |
| WDC       | WD5000LPVX-60V0TT0 | 500 GB | 18      | 417   | 122   | 0.88   |
| WDC       | WD7500BPVT-26HXZT3 | 752 GB | 1       | 1277  | 3     | 0.88   |
| Seagate   | ST9750422AS        | 752 GB | 5       | 579   | 125   | 0.87   |
| WDC       | WD5000BPKT-00PK4T0 | 500 GB | 7       | 330   | 1     | 0.87   |
| WDC       | WD5000BPVT-08HXZT3 | 500 GB | 8       | 372   | 2     | 0.87   |
| WDC       | WD3200AAJS-61B4A0  | 320 GB | 2       | 431   | 4     | 0.87   |
| WDC       | WD10JPVX-22JC3T0   | 1 TB   | 209     | 374   | 32    | 0.87   |
| WDC       | WD800BB-00FJA0     | 80 GB  | 7       | 472   | 35    | 0.87   |
| WDC       | WD100EFAX-68LHPN0  | 10 TB  | 12      | 316   | 0     | 0.87   |
| Samsung   | HD752LJ            | 752 GB | 2       | 1517  | 4     | 0.87   |
| WDC       | WD6400BPVT-22HXZT3 | 640 GB | 9       | 551   | 8     | 0.87   |
| Fujitsu   | MHV2100AT          | 100 GB | 1       | 316   | 0     | 0.87   |
| Hitachi   | HDT721025SLA380    | 250 GB | 14      | 838   | 220   | 0.87   |
| Samsung   | HM641JI            | 640 GB | 36      | 504   | 60    | 0.87   |
| WDC       | WD800BEVS-00UST0   | 80 GB  | 1       | 315   | 0     | 0.86   |
| Toshiba   | MK8032GSX          | 80 GB  | 9       | 473   | 175   | 0.86   |
| Hitachi   | HTS543216A7A384    | 160 GB | 3       | 315   | 0     | 0.86   |
| WDC       | WD2000JS-55MHB0    | 200 GB | 1       | 313   | 0     | 0.86   |
| Seagate   | ST1000LX015-1U7... | 1 TB   | 1       | 313   | 0     | 0.86   |
| WDC       | WD40NMZM-59Y94S1   | 4 TB   | 1       | 313   | 0     | 0.86   |
| WDC       | WD2000JB-00GVA0    | 200 GB | 3       | 580   | 101   | 0.86   |
| WDC       | WD800AAJS-00L7A0   | 80 GB  | 1       | 313   | 0     | 0.86   |
| Seagate   | ST2000DX002-2DV164 | 2 TB   | 38      | 357   | 33    | 0.86   |
| Seagate   | ST12000VN0007-2... | 12 TB  | 5       | 312   | 0     | 0.86   |
| IBM/Hi... | IC35L120AVV207-0   | 128 GB | 1       | 933   | 2     | 0.85   |
| Seagate   | ST2000VX002-1AH166 | 2 TB   | 1       | 311   | 0     | 0.85   |
| Toshiba   | MQ03UBB200         | 2 TB   | 8       | 310   | 0     | 0.85   |
| WDC       | WD5000BMVW-11AJGS2 | 500 GB | 2       | 310   | 0     | 0.85   |
| WDC       | WD6400BPVT-60HXZT1 | 640 GB | 4       | 912   | 527   | 0.85   |
| WDC       | WD10EALX-559BA0    | 1 TB   | 5       | 517   | 6     | 0.85   |
| WDC       | WD400BB-60DGA0     | 40 GB  | 4       | 403   | 1     | 0.85   |
| Seagate   | ST9250410AS        | 250 GB | 53      | 509   | 190   | 0.85   |
| Seagate   | ST9160411AS        | 160 GB | 8       | 611   | 146   | 0.85   |
| WDC       | WD10PURX-64E5EY0   | 1 TB   | 13      | 413   | 1     | 0.85   |
| WDC       | WD1600JS-40TGB0    | 160 GB | 1       | 308   | 0     | 0.85   |
| Seagate   | ST1000LM014-1EJ... | 1 TB   | 13      | 480   | 19    | 0.85   |
| Samsung   | SP0812N            | 80 GB  | 6       | 607   | 4     | 0.85   |
| WDC       | WD5000BPVT-00HXZT1 | 500 GB | 17      | 462   | 99    | 0.85   |
| WDC       | WD2500BEKT-75PVMT0 | 250 GB | 11      | 523   | 13    | 0.85   |
| MediaMax  | WL5000GSA12872B    | 5 TB   | 1       | 308   | 0     | 0.85   |
| WDC       | WD800JB-00JJA0     | 80 GB  | 4       | 1406  | 9     | 0.84   |
| WDC       | WD20EZRZ-00Z5HB0   | 2 TB   | 126     | 368   | 25    | 0.84   |
| WDC       | WD1600AAJB-00PVA0  | 160 GB | 11      | 560   | 165   | 0.84   |
| WDC       | WD1200BEVS-75UST0  | 120 GB | 13      | 396   | 2     | 0.84   |
| Seagate   | STM3500418AS       | 500 GB | 28      | 875   | 424   | 0.84   |
| WDC       | WD2500AAJS-00L7A0  | 250 GB | 28      | 617   | 13    | 0.84   |
| HGST      | HUH728080ALE604    | 8 TB   | 8       | 307   | 0     | 0.84   |
| WDC       | WD20SMZW-59YFCS1   | 2 TB   | 1       | 306   | 0     | 0.84   |
| WDC       | WD5000AAKS-08WWPA0 | 500 GB | 2       | 1656  | 77    | 0.84   |
| WDC       | WD3200BEVT-00SCST0 | 320 GB | 1       | 306   | 0     | 0.84   |
| Seagate   | ST1000DM003-1SB10C | 1 TB   | 78      | 359   | 46    | 0.84   |
| Samsung   | HD400LJ            | 400 GB | 2       | 480   | 5     | 0.84   |
| WDC       | WD1500ADFD-00NLR1  | 150 GB | 2       | 454   | 4     | 0.84   |
| WDC       | WD3200BEKT-60PVMT0 | 320 GB | 15      | 508   | 189   | 0.84   |
| Samsung   | HD080HJ            | 80 GB  | 101     | 749   | 382   | 0.84   |
| WDC       | WD3200BPVT-00HXZT3 | 320 GB | 5       | 437   | 6     | 0.84   |
| WDC       | WD7500BPVT-55HXZT3 | 752 GB | 3       | 444   | 3     | 0.84   |
| WDC       | WD40EZRZ-00GXCB0   | 4 TB   | 76      | 312   | 32    | 0.83   |
| WDC       | WD1600AAJS-00YZCA0 | 160 GB | 12      | 538   | 31    | 0.83   |
| MediaMax  | WL1000GSA6454G     | 1 TB   | 1       | 303   | 0     | 0.83   |
| Seagate   | ST6000VN0033-2E... | 6 TB   | 13      | 315   | 1     | 0.83   |
| Toshiba   | MD04ACA500         | 5 TB   | 5       | 400   | 4     | 0.83   |
| WDC       | WD3200BPVT-55JJ5T0 | 320 GB | 6       | 415   | 163   | 0.83   |
| WDC       | WD5000BPVT-00HXZT3 | 500 GB | 14      | 365   | 37    | 0.83   |
| Seagate   | ST500NM0011 81Y... | 500 GB | 2       | 2410  | 506   | 0.83   |
| Samsung   | HD321KJ            | 320 GB | 73      | 803   | 329   | 0.83   |
| Seagate   | ST250LT003-9YG14C  | 250 GB | 4       | 302   | 0     | 0.83   |
| WDC       | WD10SPZX-11Z10T0   | 1 TB   | 1       | 302   | 0     | 0.83   |
| WDC       | WD3200AAJS-00YZCA0 | 320 GB | 14      | 511   | 8     | 0.83   |
| WDC       | WD3200BEKX-75B7WT0 | 320 GB | 4       | 301   | 0     | 0.83   |
| Seagate   | ST4000LM024-2AN17V | 4 TB   | 13      | 378   | 13    | 0.83   |
| Seagate   | ST31000528ASQ      | 1 TB   | 2       | 430   | 66    | 0.83   |
| Seagate   | ST1500LM012-1R817G | 1.5 TB | 3       | 301   | 0     | 0.82   |
| WDC       | WD2500AAKX-00ERMA0 | 250 GB | 23      | 473   | 60    | 0.82   |
| Samsung   | HD320KJ            | 320 GB | 4       | 744   | 93    | 0.82   |
| WDC       | WD10EZEX-07ZF5A0   | 1 TB   | 2       | 668   | 2     | 0.82   |
| WDC       | WD600BEAS-22KZT0   | 64 GB  | 1       | 300   | 0     | 0.82   |
| WDC       | WD5000AAKX-00KJ3A0 | 500 GB | 2       | 416   | 4     | 0.82   |
| WDC       | WD1600BPVT-00ZEST0 | 160 GB | 1       | 299   | 0     | 0.82   |
| Seagate   | ST2000VN000-1H3164 | 2 TB   | 5       | 625   | 11    | 0.82   |
| Seagate   | ST320LM010-1KJ15C  | 320 GB | 6       | 500   | 3     | 0.82   |
| HGST      | HTS721010A9E630    | 1 TB   | 347     | 366   | 146   | 0.82   |
| WDC       | WD5000AAKX-08ERMA0 | 500 GB | 25      | 510   | 170   | 0.82   |
| Seagate   | ST1000LM044 HN-... | 1 TB   | 3       | 424   | 269   | 0.82   |
| Seagate   | ST750LM022 HN-M... | 752 GB | 105     | 418   | 34    | 0.82   |
| WDC       | WD800BEVS-07RST0   | 80 GB  | 5       | 330   | 1     | 0.82   |
| WDC       | WD20NMVW-11AV3S0   | 2 TB   | 4       | 523   | 3     | 0.82   |
| WDC       | WD40EFRX-68N32N0   | 4 TB   | 84      | 334   | 1     | 0.82   |
| WDC       | WD1600BEVT-00ZCT0  | 160 GB | 6       | 309   | 1     | 0.81   |
| Hitachi   | HDE721010SLA330    | 1 TB   | 4       | 1224  | 42    | 0.81   |
| WDC       | WD5000AAKX-60U6AA0 | 500 GB | 66      | 379   | 88    | 0.81   |
| Toshiba   | MK4009GAL          | 40 GB  | 1       | 296   | 0     | 0.81   |
| Seagate   | ST940210AS         | 40 GB  | 1       | 591   | 1     | 0.81   |
| WDC       | WD5000AVCS-732DY1  | 500 GB | 2       | 658   | 9     | 0.81   |
| Maxtor    | STM3250620A        | 250 GB | 1       | 295   | 0     | 0.81   |
| WDC       | WD100PURZ-85W86Y0  | 10 TB  | 1       | 295   | 0     | 0.81   |
| Fujitsu   | MHY2200BH          | 200 GB | 19      | 559   | 92    | 0.81   |
| WDC       | WD1500HLFS-01G6U4  | 150 GB | 2       | 295   | 0     | 0.81   |
| WDC       | WD3200AAJS-00L7A0  | 320 GB | 80      | 754   | 47    | 0.81   |
| WDC       | WD800JD-22JNC0     | 80 GB  | 2       | 412   | 3     | 0.81   |
| Seagate   | ST3320820SCE       | 320 GB | 1       | 294   | 0     | 0.81   |
| WDC       | WD5000AAKX-083CA0  | 500 GB | 1       | 294   | 0     | 0.81   |
| WDC       | WD3200BPVT-24JJ5T0 | 320 GB | 66      | 349   | 55    | 0.81   |
| Samsung   | SV1203N            | 120 GB | 2       | 441   | 3     | 0.80   |
| Hitachi   | HDS721616PLA320    | 160 GB | 3       | 1128  | 7     | 0.80   |
| WDC       | WUH721414ALE604    | 14 TB  | 2       | 292   | 0     | 0.80   |
| Maxtor    | STM3160211AS       | 160 GB | 3       | 624   | 349   | 0.80   |
| Seagate   | ST1000VX001-1HH162 | 1 TB   | 7       | 291   | 0     | 0.80   |
| WDC       | WD3200BPVT-55ZEST0 | 320 GB | 4       | 313   | 1     | 0.80   |
| Magnet... | MD02500-BJDW-RO    | 250 GB | 1       | 291   | 0     | 0.80   |
| Hitachi   | HCS5C1025CLA382    | 250 GB | 1       | 290   | 0     | 0.80   |
| WDC       | WD5000LPVX-08V0TT5 | 500 GB | 15      | 343   | 1     | 0.80   |
| WDC       | WD1600BB-00GUC0    | 160 GB | 4       | 832   | 61    | 0.79   |
| Seagate   | OOS2000G           | 2 TB   | 1       | 289   | 0     | 0.79   |
| Toshiba   | MK6459GSXP         | 640 GB | 13      | 476   | 434   | 0.79   |
| WDC       | WD7500BPVT-75HXZT3 | 752 GB | 6       | 396   | 1     | 0.79   |
| Seagate   | ST14000DM001-2J... | 14 TB  | 2       | 288   | 0     | 0.79   |
| WDC       | WD2500AAKS-00B3A0  | 250 GB | 4       | 713   | 8     | 0.79   |
| Maxtor    | STM380811AS        | 80 GB  | 4       | 500   | 5     | 0.79   |
| Toshiba   | MK3029GAC          | 32 GB  | 1       | 287   | 0     | 0.79   |
| WDC       | WD3200BEVT-60ZCT0  | 320 GB | 6       | 469   | 20    | 0.79   |
| WDC       | WD10JPVX-60JC3T0   | 1 TB   | 46      | 329   | 64    | 0.79   |
| WDC       | WD2002FFSX-68PF8N0 | 2 TB   | 2       | 286   | 0     | 0.79   |
| WDC       | WD1200BEVT-22ZCT0  | 120 GB | 1       | 286   | 0     | 0.79   |
| Seagate   | ST380215A          | 80 GB  | 29      | 455   | 138   | 0.79   |
| WDC       | WD5000AAKX-00U6AA0 | 500 GB | 25      | 432   | 4     | 0.78   |
| WDC       | WD1200BEVS-75RST0  | 120 GB | 3       | 286   | 0     | 0.78   |
| Hitachi   | HTS545032B9A300    | 320 GB | 114     | 515   | 156   | 0.78   |
| Samsung   | HM321HI            | 320 GB | 111     | 443   | 90    | 0.78   |
| WDC       | WD1600JD-22HBB0    | 160 GB | 1       | 1710  | 5     | 0.78   |
| WDC       | WD5000AAVS-22G9B1  | 500 GB | 3       | 1103  | 8     | 0.78   |
| WDC       | WD40NMZW-11GX6S1   | 4 TB   | 31      | 318   | 16    | 0.78   |
| Toshiba   | DT01ACA050         | 500 GB | 355     | 353   | 30    | 0.78   |
| WDC       | WD20PURX-64PFUY0   | 2 TB   | 2       | 284   | 0     | 0.78   |
| WDC       | WD2500BEVS-08VAT2  | 250 GB | 3       | 284   | 0     | 0.78   |
| HGST      | HUS726040ALE614    | 4 TB   | 3       | 284   | 0     | 0.78   |
| Samsung   | HD160JJ            | 160 GB | 80      | 817   | 418   | 0.78   |
| WDC       | WD10JPVT-08A1YT2   | 1 TB   | 11      | 434   | 2     | 0.78   |
| Hitachi   | HDS721032CLA662    | 320 GB | 1       | 283   | 0     | 0.78   |
| Fujitsu   | MHZ2320BH G2       | 320 GB | 16      | 544   | 300   | 0.77   |
| WDC       | WD7500BPVT-08HXZT3 | 752 GB | 5       | 557   | 14    | 0.77   |
| Toshiba   | HDWD130            | 3 TB   | 58      | 285   | 18    | 0.77   |
| WDC       | WD3200LPVT-08G33T1 | 320 GB | 6       | 327   | 2     | 0.77   |
| Toshiba   | MQ01ABD075         | 752 GB | 118     | 400   | 91    | 0.77   |
| WDC       | WD5000LPVX-80V0TT0 | 500 GB | 45      | 301   | 46    | 0.77   |
| WDC       | WD800BEVS-22RST0   | 80 GB  | 29      | 415   | 52    | 0.77   |
| WDC       | WD3200BPVT-22ZEST0 | 320 GB | 59      | 419   | 60    | 0.77   |
| Apple     | HDD TOSHIBA MK5... | 500 GB | 3       | 430   | 134   | 0.77   |
| Seagate   | ST9750420AS        | 752 GB | 67      | 546   | 102   | 0.77   |
| WDC       | WD3200BPVT-22JJ5T0 | 320 GB | 135     | 335   | 49    | 0.77   |
| Samsung   | HM500JJ            | 500 GB | 3       | 415   | 3     | 0.77   |
| WDC       | WD2500BEKT-00PVMT0 | 250 GB | 2       | 279   | 0     | 0.77   |
| Seagate   | ST3120813AS        | 120 GB | 22      | 877   | 541   | 0.77   |
| Fujitsu   | MHW2100BH          | 100 GB | 1       | 279   | 0     | 0.76   |
| WDC       | WD1600BEVT-75ZCT1  | 160 GB | 1       | 279   | 0     | 0.76   |
| WDC       | WD10JMVW-11AJGS1   | 1 TB   | 9       | 414   | 119   | 0.76   |
| Fujitsu   | MHY2120BH          | 120 GB | 28      | 554   | 202   | 0.76   |
| WDC       | WD10SPCX-22HWST0   | 1 TB   | 2       | 278   | 0     | 0.76   |
| WDC       | WD100EB-00BHF0     | 10 GB  | 1       | 557   | 1     | 0.76   |
| WDC       | WD10JPVX-16JC3T3   | 1 TB   | 3       | 278   | 0     | 0.76   |
| WDC       | WD10SMZW-11Y0TS0   | 1 TB   | 26      | 278   | 0     | 0.76   |
| Samsung   | HN-M500MBB         | 500 GB | 45      | 428   | 19    | 0.76   |
| WDC       | WD5000AAKX-083CA1  | 500 GB | 16      | 706   | 50    | 0.76   |
| WDC       | WD40EZRX-11SPEB0   | 4 TB   | 1       | 277   | 0     | 0.76   |
| Samsung   | HD401LJ            | 400 GB | 4       | 702   | 14    | 0.76   |
| WDC       | WD3200BEVT-80A0RT0 | 320 GB | 42      | 457   | 44    | 0.76   |
| WDC       | WD5000AAKX-221CA0  | 500 GB | 2       | 1008  | 5     | 0.76   |
| WDC       | WD10JPVT-75A1YT0   | 1 TB   | 11      | 412   | 2     | 0.76   |
| Samsung   | HM320II            | 320 GB | 25      | 388   | 164   | 0.76   |
| WDC       | WD5000BPVT-24HXZT3 | 500 GB | 22      | 405   | 2     | 0.76   |
| Hitachi   | HTS727575A9E364    | 752 GB | 22      | 591   | 258   | 0.76   |
| Seagate   | ST250LT007-9ZV14C  | 250 GB | 4       | 467   | 152   | 0.76   |
| WDC       | WD1200JS-00NCB1    | 120 GB | 2       | 591   | 27    | 0.75   |
| Seagate   | STM3320418AS       | 320 GB | 10      | 644   | 140   | 0.75   |
| WDC       | WD2004FBYZ-01YCBB1 | 2 TB   | 5       | 275   | 0     | 0.75   |
| WDC       | WD800BB-56JKC0     | 80 GB  | 6       | 735   | 7     | 0.75   |
| Samsung   | HD250HJ            | 250 GB | 44      | 819   | 607   | 0.75   |
| Seagate   | ST32000542AS       | 2 TB   | 31      | 753   | 394   | 0.75   |
| WDC       | WD10JPVX-11JC3T0   | 1 TB   | 2       | 274   | 0     | 0.75   |
| Hitachi   | HDS721010DLE630    | 1 TB   | 48      | 805   | 626   | 0.75   |
| Seagate   | ST4000VN008-2DR166 | 4 TB   | 66      | 297   | 4     | 0.75   |
| Seagate   | ST1000VT001-1RE172 | 1 TB   | 2       | 273   | 0     | 0.75   |
| WDC       | WD1600AABS-62PRA0  | 160 GB | 1       | 273   | 0     | 0.75   |
| WDC       | WD5000BEVT-00ZAT0  | 500 GB | 7       | 448   | 169   | 0.75   |
| WDC       | WD1200BEVS-00UST0  | 120 GB | 3       | 292   | 1     | 0.75   |
| WDC       | WD6400BEVT-80A0RT0 | 640 GB | 3       | 314   | 2     | 0.75   |
| WDC       | WD3200BPVT-80JJ5T0 | 320 GB | 64      | 333   | 49    | 0.75   |
| WDC       | WD121KRYZ-01W0RB0  | 12 TB  | 5       | 271   | 0     | 0.75   |
| WDC       | WD3000FYYZ-01UL1B3 | 3 TB   | 1       | 271   | 0     | 0.74   |
| Apple     | HDD ST500LM012     | 500 GB | 1       | 271   | 0     | 0.74   |
| WDC       | WD10EADS-114BB1    | 1 TB   | 2       | 1820  | 493   | 0.74   |
| WDC       | WD10JPVX-75JC3T0   | 1 TB   | 59      | 353   | 13    | 0.74   |
| WDC       | WD3200JB-00KFA0    | 320 GB | 3       | 1330  | 8     | 0.74   |
| Seagate   | ST500LM012 HN-M... | 500 GB | 243     | 374   | 42    | 0.74   |
| Toshiba   | HDWD120            | 2 TB   | 54      | 274   | 20    | 0.74   |
| WDC       | WD10EADS-65M2BX    | 1 TB   | 2       | 807   | 46    | 0.74   |
| WDC       | WD1200BEVS-07RST0  | 120 GB | 2       | 268   | 0     | 0.74   |
| Hitachi   | HTS547550A9E384    | 500 GB | 163     | 465   | 328   | 0.74   |
| Toshiba   | MK1031GAS          | 100 GB | 3       | 433   | 3     | 0.74   |
| Seagate   | ST2000DX001-SSH... | 2 TB   | 1       | 805   | 2     | 0.74   |
| WDC       | WD2500AAJB-57R1A0  | 250 GB | 1       | 268   | 0     | 0.73   |
| WDC       | WD1200JD-22HBB0    | 120 GB | 2       | 1602  | 5     | 0.73   |
| HGST      | HUH721212ALE604    | 12 TB  | 6       | 267   | 0     | 0.73   |
| Hitachi   | HTS545016B9A300    | 160 GB | 55      | 404   | 55    | 0.73   |
| WDC       | WD3200LPVX-60V0TT0 | 320 GB | 1       | 266   | 0     | 0.73   |
| WDC       | WD10EZEX-08Y20A0   | 1 TB   | 11      | 360   | 2     | 0.73   |
| WDC       | WD5000LMVW-11CKRS0 | 500 GB | 2       | 265   | 0     | 0.73   |
| Maxtor    | STM3250310AS       | 250 GB | 72      | 739   | 380   | 0.73   |
| MediaMax  | WL1000GSA3272C     | 1 TB   | 1       | 265   | 0     | 0.73   |
| WDC       | WD5000LPVX-22V0TT0 | 500 GB | 210     | 319   | 10    | 0.73   |
| WDC       | WD6400BEVT-60A0RT0 | 640 GB | 3       | 310   | 12    | 0.73   |
| WDC       | WD5000AAKS-65A7B2  | 500 GB | 1       | 265   | 0     | 0.73   |
| Hitachi   | HTS547575A9E384    | 640 GB | 148     | 523   | 448   | 0.73   |
| WDC       | WD2500AAKS-61L9A0  | 250 GB | 1       | 265   | 0     | 0.73   |
| WDC       | WD2500BEKT-00A25T0 | 250 GB | 1       | 264   | 0     | 0.73   |
| Hitachi   | HTS545025B9A300    | 250 GB | 132     | 492   | 107   | 0.73   |
| Hitachi   | HTS542516K9A300    | 160 GB | 7       | 761   | 189   | 0.73   |
| WDC       | WD2500AAKX-321CA0  | 250 GB | 1       | 264   | 0     | 0.72   |
| WDC       | WD20PURX-64P6ZY0   | 2 TB   | 14      | 325   | 11    | 0.72   |
| Samsung   | HD161HJ            | 160 GB | 56      | 908   | 505   | 0.72   |
| Hitachi   | HTS541075A9E680    | 752 GB | 6       | 393   | 509   | 0.72   |
| Maxtor    | STM3250820AS       | 250 GB | 17      | 820   | 186   | 0.72   |
| WDC       | WD2500AAJS-60B4A0  | 250 GB | 1       | 263   | 0     | 0.72   |
| WDC       | WD5000BPVT-80HXZT1 | 500 GB | 7       | 634   | 48    | 0.72   |
| WDC       | WD5000AAKX-08ANVA0 | 500 GB | 3       | 310   | 3     | 0.72   |
| WDC       | WD20EARS-00J2GB0   | 2 TB   | 4       | 856   | 6     | 0.72   |
| WDC       | WD2500BEKX-00B7WT0 | 250 GB | 2       | 263   | 0     | 0.72   |
| WDC       | WD3000HLHX-01JJPV0 | 304 GB | 3       | 312   | 1     | 0.72   |
| Toshiba   | MK6465GSXN         | 640 GB | 8       | 454   | 194   | 0.72   |
| Maxtor    | 6L040J2            | 40 GB  | 1       | 1576  | 5     | 0.72   |
| WDC       | WD2500AAJS-60Z0A0  | 250 GB | 3       | 466   | 1     | 0.72   |
| Maxtor    | STM380815AS        | 80 GB  | 22      | 698   | 604   | 0.72   |
| WDC       | WD10JPVX-35JC3T0   | 1 TB   | 4       | 261   | 0     | 0.72   |
| HGST      | HTS541010A7E630    | 1 TB   | 30      | 294   | 104   | 0.72   |
| WDC       | WD1600BEVS-60RST0  | 160 GB | 9       | 507   | 254   | 0.72   |
| Fujitsu   | MHX2300BT          | 304 GB | 4       | 723   | 36    | 0.71   |
| HGST      | HUH721008ALE600    | 8 TB   | 1       | 260   | 0     | 0.71   |
| Toshiba   | MK3263GSX          | 320 GB | 9       | 744   | 13    | 0.71   |
| WDC       | WD5000LPVX-08V0TT6 | 500 GB | 2       | 260   | 0     | 0.71   |
| WDC       | WD3200BEVT-00A0RT0 | 320 GB | 21      | 337   | 11    | 0.71   |
| WDC       | WD10SDZW-11UMGS0   | 1 TB   | 10      | 260   | 0     | 0.71   |
| WDC       | WD10SPCX-60KHST0   | 1 TB   | 4       | 298   | 1     | 0.71   |
| IBM/Hi... | IC35L040AVVA07-0   | 41 GB  | 4       | 623   | 83    | 0.71   |
| Seagate   | ST8000DM0004-1Z... | 8 TB   | 2       | 259   | 0     | 0.71   |
| Seagate   | ST3000DM001-9YN166 | 3 TB   | 32      | 848   | 963   | 0.71   |
| WDC       | WD1600JS-60MHB5    | 160 GB | 3       | 862   | 30    | 0.71   |
| Toshiba   | MQ01ABD100M        | 1 TB   | 6       | 259   | 0     | 0.71   |
| Seagate   | ST320011A          | 20 GB  | 7       | 489   | 5     | 0.71   |
| WDC       | WD5000BPVT-35HXZT1 | 500 GB | 4       | 259   | 0     | 0.71   |
| Seagate   | ST330013A          | 32 GB  | 1       | 259   | 0     | 0.71   |
| WDC       | WD5000LPVT-00G33T0 | 500 GB | 6       | 541   | 2     | 0.71   |
| Hitachi   | HTS722010K9SA00    | 100 GB | 5       | 985   | 11    | 0.71   |
| Seagate   | ST320LM001 HN-M... | 320 GB | 45      | 293   | 1     | 0.71   |
| Seagate   | ST1000LM024 HN-... | 1 TB   | 697     | 377   | 48    | 0.71   |
| WDC       | WD10JPVX-80JC3T0   | 1 TB   | 10      | 258   | 0     | 0.71   |
| Seagate   | ST91208220AS       | 120 GB | 2       | 461   | 507   | 0.71   |
| Seagate   | ST1000DM010-2DM162 | 1 TB   | 9       | 258   | 0     | 0.71   |
| Seagate   | ST9640320AS        | 640 GB | 18      | 578   | 325   | 0.71   |
| WDC       | WD5000LUCT-63RC2Y0 | 500 GB | 1       | 257   | 0     | 0.71   |
| Seagate   | ST1500LM006 HN-... | 1.5 TB | 4       | 257   | 0     | 0.70   |
| WDC       | WD5000LPVX-75V0TT0 | 500 GB | 39      | 299   | 2     | 0.70   |
| WDC       | WD15EARS-00Z5B1    | 1.5 TB | 30      | 1205  | 439   | 0.70   |
| HGST      | HUS726T4TALA6L4    | 4 TB   | 4       | 255   | 0     | 0.70   |
| WDC       | WD2500BEVT-24A23T0 | 250 GB | 25      | 432   | 66    | 0.70   |
| WDC       | WD10EZEX-60WN4A0   | 1 TB   | 72      | 302   | 30    | 0.70   |
| WDC       | WD5000LPVX-08V0TT2 | 500 GB | 4       | 314   | 2     | 0.70   |
| WDC       | WD5000BPVT-75HXZT3 | 500 GB | 20      | 466   | 3     | 0.70   |
| Maxtor    | STM3320620AS       | 320 GB | 2       | 254   | 0     | 0.70   |
| Toshiba   | MK3276GSX -63      | 320 GB | 7       | 395   | 19    | 0.70   |
| Seagate   | ST500DM002-1SB10A  | 500 GB | 35      | 285   | 2     | 0.70   |
| HP        | MM0500EANCR        | 500 GB | 13      | 1725  | 49    | 0.70   |
| WDC       | WD5000BPVT-22HXZT1 | 500 GB | 22      | 512   | 95    | 0.70   |
| WDC       | WD3200BEKT-00F3T0  | 320 GB | 2       | 253   | 0     | 0.69   |
| WDC       | WD10JPVX-00JC3T0   | 1 TB   | 42      | 256   | 1     | 0.69   |
| WDC       | WD3200LPVX-22V0TT0 | 320 GB | 18      | 301   | 1     | 0.69   |
| WDC       | WD15EARS-22MVWB0   | 1.5 TB | 6       | 722   | 258   | 0.69   |
| WDC       | WD5000AZRZ-00HTKB0 | 500 GB | 13      | 342   | 1     | 0.69   |
| WDC       | WD7500AZEX-00BN5A0 | 752 GB | 1       | 252   | 0     | 0.69   |
| WDC       | WD800JD-60MSA1     | 80 GB  | 1       | 252   | 0     | 0.69   |
| WDC       | WD5000AAKS-07A7B0  | 500 GB | 3       | 754   | 6     | 0.69   |
| Samsung   | HD163GJ            | 160 GB | 1       | 251   | 0     | 0.69   |
| Seagate   | ST9160411ASG       | 160 GB | 3       | 600   | 3     | 0.69   |
| WDC       | WD5000AZLX-60K2TA0 | 500 GB | 12      | 251   | 0     | 0.69   |
| Hitachi   | HTS725050A7E630    | 500 GB | 12      | 391   | 703   | 0.69   |
| Seagate   | ST1000DM003-1SB102 | 1 TB   | 90      | 274   | 15    | 0.69   |
| WDC       | WD7500BPKX-22HPJT0 | 752 GB | 14      | 265   | 1     | 0.69   |
| WDC       | WD10JPVX-55JC3T3   | 1 TB   | 3       | 602   | 343   | 0.69   |
| WDC       | WD3200AAJS-60M0A0  | 320 GB | 1       | 749   | 2     | 0.68   |
| Seagate   | ST2000VX008-2E3164 | 2 TB   | 7       | 249   | 0     | 0.68   |
| WDC       | WD2500JB-00REA0    | 250 GB | 10      | 673   | 26    | 0.68   |
| WDC       | WD50NMZW-59LG6S1   | 5 TB   | 2       | 249   | 0     | 0.68   |
| WDC       | WD4005FZBX-00K5WB0 | 4 TB   | 11      | 249   | 0     | 0.68   |
| Seagate   | ST1000DX001-1CM... | 1 TB   | 1       | 746   | 2     | 0.68   |
| Samsung   | HD082GJ            | 80 GB  | 19      | 534   | 340   | 0.68   |
| WDC       | WD30EZRZ-00GXCB0   | 3 TB   | 12      | 248   | 0     | 0.68   |
| HGST      | HUH721212ALE600    | 12 TB  | 3       | 248   | 0     | 0.68   |
| Toshiba   | MQ04UBF100         | 1 TB   | 23      | 258   | 1     | 0.68   |
| WDC       | WD40PURZ-85TTDY0   | 4 TB   | 10      | 301   | 1     | 0.68   |
| Hitachi   | HTS545032A7E380    | 320 GB | 27      | 369   | 176   | 0.68   |
| Toshiba   | MK3276GSX H        | 320 GB | 2       | 247   | 0     | 0.68   |
| WDC       | WD2000JS-00MHB1    | 200 GB | 1       | 246   | 0     | 0.68   |
| Fujitsu   | MHV2080AH          | 80 GB  | 6       | 503   | 3     | 0.68   |
| Hitachi   | HCT721016SLA380    | 160 GB | 3       | 246   | 0     | 0.67   |
| Fujitsu   | MJA2500BH FFS G1   | 500 GB | 1       | 246   | 0     | 0.67   |
| WDC       | WD2503ABYX-01WERA1 | 256 GB | 4       | 619   | 3     | 0.67   |
| Hitachi   | HTS542516K9SA00    | 160 GB | 63      | 621   | 167   | 0.67   |
| WDC       | WD20SPZX-00CRAT0   | 2 TB   | 3       | 245   | 0     | 0.67   |
| Fujitsu   | MHZ2320BH G1       | 320 GB | 11      | 489   | 22    | 0.67   |
| WDC       | WD5000BEVT-22A0RT0 | 500 GB | 42      | 503   | 61    | 0.67   |
| WDC       | WD10EADS-65M2B1    | 1 TB   | 7       | 1066  | 142   | 0.67   |
| WDC       | WD7500BPVT-22A1YT0 | 752 GB | 1       | 733   | 2     | 0.67   |
| Hitachi   | HDP725050GLAT80    | 500 GB | 2       | 664   | 2     | 0.67   |
| WDC       | WD400UE-22HCT0     | 40 GB  | 1       | 732   | 2     | 0.67   |
| WDC       | WD2500BEKT-75A25T0 | 250 GB | 6       | 396   | 3     | 0.67   |
| WDC       | WD10EZEX-75WN4A0   | 1 TB   | 34      | 290   | 49    | 0.67   |
| WDC       | WD5000BEVT-11A0RT0 | 500 GB | 1       | 243   | 0     | 0.67   |
| WDC       | WD4000FYYZ-01UL1B0 | 4 TB   | 1       | 2193  | 8     | 0.67   |
| Seagate   | ST4000DM004-2CV104 | 4 TB   | 152     | 264   | 29    | 0.67   |
| Fujitsu   | MHV2120BH          | 120 GB | 3       | 371   | 3     | 0.67   |
| Seagate   | ST340016A          | 40 GB  | 34      | 664   | 33    | 0.67   |
| Seagate   | ST1000LM014-SSH... | 1 TB   | 26      | 384   | 186   | 0.67   |
| WDC       | WD2500AAJS-00B4A0  | 250 GB | 17      | 712   | 60    | 0.66   |
| WDC       | WD1600AAJB-56WRA0  | 160 GB | 1       | 969   | 3     | 0.66   |
| WDC       | WD10EZEX-35WN4A0   | 1 TB   | 6       | 242   | 0     | 0.66   |
| Hitachi   | HDS721010KLA330    | 1 TB   | 9       | 631   | 21    | 0.66   |
| Fujitsu   | MHW2080AT          | 80 GB  | 1       | 241   | 0     | 0.66   |
| WDC       | WD3200AAJB-56R1A0  | 320 GB | 2       | 282   | 5     | 0.66   |
| Seagate   | ST9750423AS        | 752 GB | 15      | 585   | 273   | 0.66   |
| WDC       | WD5000AAKB-00H8A0  | 500 GB | 16      | 563   | 7     | 0.66   |
| WDC       | WD1600BEVT-60ZCT1  | 160 GB | 9       | 372   | 247   | 0.66   |
| WDC       | WD5000LPVT-00FMCT0 | 500 GB | 6       | 247   | 1     | 0.66   |
| Seagate   | ST1000NM0008-2F... | 1 TB   | 3       | 240   | 0     | 0.66   |
| WDC       | WD5000AZLX-00K2TA0 | 500 GB | 12      | 239   | 0     | 0.66   |
| WDC       | WD5000AAKS-00V1A0  | 500 GB | 61      | 770   | 337   | 0.66   |
| Toshiba   | HDWN180            | 8 TB   | 8       | 239   | 0     | 0.66   |
| Seagate   | ST3000NC002-1DY166 | 3 TB   | 2       | 987   | 1494  | 0.66   |
| Toshiba   | HDWL110            | 1 TB   | 8       | 238   | 0     | 0.65   |
| Hitachi   | HTS541010G9AT00    | 100 GB | 1       | 474   | 1     | 0.65   |
| WDC       | WD5000LPCX-35VHAT0 | 500 GB | 2       | 236   | 0     | 0.65   |
| Seagate   | ST1000VM002-9ZL162 | 1 TB   | 3       | 515   | 733   | 0.65   |
| WDC       | WD10JMVW-11S5XS0   | 1 TB   | 7       | 564   | 5     | 0.65   |
| WDC       | WD25EZRX-00MMMB0   | 2.5 TB | 2       | 894   | 4     | 0.65   |
| Apple     | HDD ST2000DM001    | 2 TB   | 1       | 236   | 0     | 0.65   |
| Toshiba   | MQ01ABD032         | 320 GB | 91      | 358   | 136   | 0.65   |
| Toshiba   | MK5065GSXF         | 500 GB | 15      | 384   | 35    | 0.65   |
| WDC       | WD40NPZZ-00PDPT0   | 4 TB   | 3       | 235   | 0     | 0.65   |
| WDC       | WD5000BPVT-22A1YT0 | 500 GB | 10      | 235   | 0     | 0.64   |
| WDC       | WD2500BEVT-00ZCT0  | 250 GB | 10      | 235   | 0     | 0.64   |
| Seagate   | ST500LM011 HM501II | 500 GB | 2       | 277   | 1     | 0.64   |
| WDC       | WD10JPVT-80A1YT0   | 1 TB   | 1       | 235   | 0     | 0.64   |
| WDC       | WD7500BPVT-60HXZT3 | 752 GB | 9       | 504   | 119   | 0.64   |
| WDC       | WD3200BEKT-75KA9T0 | 320 GB | 1       | 234   | 0     | 0.64   |
| Seagate   | ST1000LM014-1EJ164 | 1 TB   | 77      | 412   | 94    | 0.64   |
| WDC       | WD1600JS-60NCB1    | 160 GB | 5       | 603   | 64    | 0.64   |
| MediaMax  | WL250GSA1672       | 250 GB | 1       | 2108  | 8     | 0.64   |
| WDC       | WD5003ABYX-23 0... | 500 GB | 1       | 234   | 0     | 0.64   |
| WDC       | WD5000AADS-67S9B0  | 500 GB | 1       | 2104  | 8     | 0.64   |
| WDC       | WD6400BPVT-26HXZT1 | 640 GB | 1       | 232   | 0     | 0.64   |
| Seagate   | ST95005620AS       | 500 GB | 20      | 721   | 116   | 0.64   |
| WDC       | WD6401AALS-00E3A0  | 640 GB | 5       | 692   | 6     | 0.64   |
| HGST      | HTS725032A7E635... | 320 GB | 1       | 231   | 0     | 0.64   |
| HGST      | HTS541010A9E680    | 1 TB   | 230     | 391   | 351   | 0.63   |
| WDC       | WD10EADS-65P6B0    | 1 TB   | 2       | 1537  | 7     | 0.63   |
| WDC       | WD40EZRZ-22GXCB0   | 4 TB   | 17      | 230   | 0     | 0.63   |
| WDC       | WD10JMVW-11AJGS4   | 1 TB   | 29      | 234   | 36    | 0.63   |
| WDC       | WD20EURX-63T0FY0   | 2 TB   | 11      | 501   | 189   | 0.63   |
| WDC       | WD2500BEVT-60ZCT1  | 250 GB | 8       | 340   | 8     | 0.63   |
| HGST      | HUS726060ALE610    | 6 TB   | 1       | 230   | 0     | 0.63   |
| Seagate   | ST360014A          | 64 GB  | 4       | 584   | 12    | 0.63   |
| WDC       | WD10EZEX-22MFCA0   | 1 TB   | 82      | 241   | 15    | 0.63   |
| Seagate   | ST1000VN002-2EY102 | 1 TB   | 8       | 260   | 123   | 0.63   |
| Toshiba   | Generic L200 Ha... | 2 TB   | 2       | 229   | 0     | 0.63   |
| WDC       | WD2005FBYZ-01YCBB2 | 2 TB   | 6       | 228   | 0     | 0.63   |
| WDC       | WD10SPCX-24HWST1   | 1 TB   | 30      | 271   | 37    | 0.63   |
| Seagate   | ST3160212ACE       | 160 GB | 4       | 512   | 27    | 0.63   |
| WDC       | WD800BB-98JHC0     | 80 GB  | 1       | 1829  | 7     | 0.63   |
| Seagate   | ST9160821A         | 160 GB | 3       | 412   | 12    | 0.63   |
| WDC       | WD5000BEKT-60KA9T0 | 500 GB | 3       | 324   | 1     | 0.63   |
| Toshiba   | MK4058GSX          | 400 GB | 4       | 418   | 3     | 0.63   |
| WDC       | WD5000AZLX-75K2TA0 | 500 GB | 7       | 228   | 0     | 0.63   |
| Toshiba   | MQ01ABF032         | 320 GB | 29      | 299   | 55    | 0.63   |
| ExcelStor | J8160S             | 160 GB | 6       | 445   | 3     | 0.62   |
| WDC       | WD3200AAKS-00V6A0  | 320 GB | 3       | 315   | 1     | 0.62   |
| Fujitsu   | MHW2160BH PL       | 160 GB | 12      | 606   | 279   | 0.62   |
| Toshiba   | MQ01ABD100         | 1 TB   | 431     | 327   | 106   | 0.62   |
| WDC       | WD20SDZW-11Z3CS1   | 2 TB   | 1       | 226   | 0     | 0.62   |
| WDC       | WD2500YD-01NVB1    | 256 GB | 1       | 1357  | 5     | 0.62   |
| WDC       | WD5000BEKT-80KA9T1 | 500 GB | 4       | 280   | 1     | 0.62   |
| WDC       | WD5000AVCS-632DY1  | 500 GB | 12      | 385   | 4     | 0.62   |
| Seagate   | ST2000LM015-2E8174 | 2 TB   | 61      | 248   | 34    | 0.62   |
| WDC       | WD7500BPKT-75PK4T0 | 752 GB | 18      | 468   | 5     | 0.62   |
| Toshiba   | MK5076GSXN         | 500 GB | 1       | 224   | 0     | 0.62   |
| WDC       | WD20SDZW-11Z3CS0   | 2 TB   | 4       | 224   | 0     | 0.61   |
| Seagate   | ST3120211AS        | 120 GB | 5       | 517   | 12    | 0.61   |
| WDC       | WD10EZEX-08WN4A0   | 1 TB   | 300     | 240   | 7     | 0.61   |
| WDC       | WD2500AAJS-65M0A0  | 250 GB | 3       | 665   | 13    | 0.61   |
| WDC       | WD3200BEVT-75A23T0 | 320 GB | 3       | 283   | 47    | 0.61   |
| WDC       | WD2500BEVT-75A23T0 | 250 GB | 9       | 547   | 8     | 0.61   |
| WDC       | WD10JPVT-00A1YT0   | 1 TB   | 4       | 287   | 221   | 0.61   |
| Fujitsu   | MHZ2080BH G1       | 80 GB  | 3       | 222   | 0     | 0.61   |
| Seagate   | ST500LM000-1EJ162  | 500 GB | 74      | 307   | 60    | 0.61   |
| WDC       | WD10SPZX-75Z10T0   | 1 TB   | 4       | 221   | 0     | 0.61   |
| WDC       | WD5000BPKX-60HPJT0 | 500 GB | 5       | 492   | 47    | 0.61   |
| Fujitsu   | MHW2120BJ FFS G2   | 120 GB | 1       | 221   | 0     | 0.61   |
| WDC       | WD1600BEKT-60F3T1  | 160 GB | 1       | 221   | 0     | 0.61   |
| HGST      | HTS545032A7E680    | 320 GB | 17      | 294   | 80    | 0.61   |
| Toshiba   | MQ02ABD100H        | 1 TB   | 22      | 341   | 97    | 0.61   |
| WDC       | WD20EARS-00J99B0   | 2 TB   | 3       | 500   | 435   | 0.61   |
| Hitachi   | HTS541080G9SA00    | 80 GB  | 7       | 365   | 3     | 0.61   |
| WDC       | WD2500AAKS-60VYA0  | 250 GB | 1       | 221   | 0     | 0.61   |
| WDC       | WD5000LPCX-24C6HT0 | 500 GB | 60      | 282   | 9     | 0.60   |
| Seagate   | ST9500530NS        | 500 GB | 3       | 1402  | 99    | 0.60   |
| Toshiba   | DT01ABA300V        | 3 TB   | 1       | 220   | 0     | 0.60   |
| WDC       | WD10EZEX-21WN4A0   | 1 TB   | 29      | 245   | 1     | 0.60   |
| WDC       | WD7500BPKX-00HPJT0 | 752 GB | 12      | 271   | 9     | 0.60   |
| Hitachi   | HDS721050DLE630    | 500 GB | 44      | 513   | 453   | 0.60   |
| WDC       | WD800BB-00FRA0     | 80 GB  | 5       | 668   | 10    | 0.60   |
| WDC       | WD100EZAZ-11TDBA0  | 10 TB  | 11      | 219   | 0     | 0.60   |
| WDC       | WD5000AZLX-00JKKA0 | 500 GB | 10      | 223   | 56    | 0.60   |
| WDC       | WD5000AAKX-003CA0  | 500 GB | 42      | 801   | 44    | 0.60   |
| WDC       | WD5000AAKS-00E4A0  | 500 GB | 10      | 863   | 33    | 0.60   |
| WDC       | WD5000BMVW-11AMCS0 | 500 GB | 2       | 409   | 1     | 0.60   |
| WDC       | WD3000HLFS-75G6U1  | 304 GB | 1       | 218   | 0     | 0.60   |
| Seagate   | ST2000LX001-1RG174 | 2 TB   | 45      | 291   | 75    | 0.60   |
| WDC       | WD10TMVW-11ZSMS4   | 1 TB   | 4       | 471   | 3     | 0.60   |
| WDC       | WD20NPVT-00Z2TT0   | 2 TB   | 3       | 336   | 12    | 0.60   |
| Seagate   | ST2000LM005 HN-... | 2 TB   | 5       | 217   | 0     | 0.60   |
| Samsung   | HM250HI            | 250 GB | 83      | 340   | 13    | 0.60   |
| Toshiba   | HDWA130            | 3 TB   | 2       | 217   | 0     | 0.60   |
| WDC       | WD1600JB-00GVC0    | 160 GB | 2       | 777   | 3     | 0.59   |
| Seagate   | ST9250827AS        | 250 GB | 40      | 581   | 453   | 0.59   |
| WDC       | WD5002AALX-32Z3A0  | 500 GB | 2       | 647   | 1     | 0.59   |
| WDC       | WD3200AZDX-00SC2B0 | 320 GB | 2       | 379   | 440   | 0.59   |
| WDC       | WD3200BPVT-00ZEST0 | 320 GB | 4       | 215   | 0     | 0.59   |
| WDC       | WD3200BEVT-22A23T0 | 320 GB | 51      | 470   | 79    | 0.59   |
| Toshiba   | MK5055GSXN         | 500 GB | 2       | 392   | 4     | 0.59   |
| Seagate   | ST3500830AS        | 500 GB | 16      | 787   | 497   | 0.59   |
| WDC       | WD3200BPVT-24ZEST0 | 320 GB | 23      | 327   | 53    | 0.59   |
| Samsung   | SP1624N            | 160 GB | 2       | 213   | 0     | 0.59   |
| WDC       | WD3200BEKT-60V5T1  | 320 GB | 30      | 489   | 330   | 0.58   |
| Seagate   | ST1000VX000-1ES162 | 1 TB   | 18      | 213   | 0     | 0.58   |
| WDC       | WD5000LPLX-60ZNTT0 | 500 GB | 2       | 213   | 0     | 0.58   |
| Fujitsu   | MPE3084AE          | 8 GB   | 1       | 213   | 0     | 0.58   |
| WDC       | WD4000FYYZ-01UL1B1 | 4 TB   | 7       | 873   | 13    | 0.58   |
| Seagate   | ST1000UM000-1EK164 | 1 TB   | 3       | 212   | 0     | 0.58   |
| WDC       | WD10JPCX-24UE4T0   | 1 TB   | 68      | 293   | 37    | 0.58   |
| Hitachi   | HTS543216L9A300    | 160 GB | 50      | 545   | 218   | 0.58   |
| WDC       | WD2500BEVT-22A23T0 | 250 GB | 61      | 393   | 65    | 0.58   |
| WDC       | WD2500LPVX-22V0TT0 | 250 GB | 2       | 212   | 0     | 0.58   |
| WDC       | WD5000AAKS-00V6A0  | 500 GB | 8       | 746   | 9     | 0.58   |
| Hitachi   | HTS541660J9SA00    | 64 GB  | 6       | 468   | 5     | 0.58   |
| WDC       | WD1600BEVT-08A23T1 | 160 GB | 2       | 212   | 0     | 0.58   |
| WDC       | WD10EADS-22M2B0    | 1 TB   | 13      | 725   | 7     | 0.58   |
| Hitachi   | HTS545025B9SA00    | 250 GB | 3       | 211   | 0     | 0.58   |
| WDC       | WD1600AAJB-22WRA0  | 160 GB | 3       | 531   | 2     | 0.58   |
| Seagate   | ST1000VX005-2EZ102 | 1 TB   | 6       | 211   | 0     | 0.58   |
| HGST      | HEJ423232H9E300    | 320 GB | 1       | 211   | 0     | 0.58   |
| WDC       | WD2500BEVT-00A23T0 | 250 GB | 12      | 482   | 9     | 0.58   |
| Toshiba   | MQ04UBD200         | 2 TB   | 13      | 229   | 2     | 0.58   |
| WDC       | WD3200BEKX-00B7WT0 | 320 GB | 8       | 213   | 2     | 0.58   |
| Seagate   | ST1000DX002-2DV162 | 1 TB   | 21      | 214   | 2     | 0.58   |
| Seagate   | ST33000651AS       | 3 TB   | 6       | 376   | 169   | 0.58   |
| Seagate   | ST500LM000-1EJ1... | 500 GB | 11      | 241   | 34    | 0.58   |
| WDC       | WD30NMVW-11C3NS2   | 3 TB   | 2       | 606   | 1     | 0.58   |
| Toshiba   | MK6461GSY          | 640 GB | 4       | 254   | 183   | 0.58   |
| WDC       | WD5000LPCX-00VHAT0 | 500 GB | 35      | 247   | 1     | 0.58   |
| WDC       | WD7500BPVT-55HXZT4 | 752 GB | 2       | 210   | 0     | 0.58   |
| Toshiba   | DT01ABA100         | 1 TB   | 1       | 209   | 0     | 0.57   |
| Seagate   | ST3000VN007-2AH16M | 3 TB   | 4       | 209   | 0     | 0.57   |
| WDC       | WD10EALX-229BA0    | 1 TB   | 5       | 793   | 11    | 0.57   |
| Toshiba   | MQ01ABD050V        | 500 GB | 7       | 275   | 229   | 0.57   |
| WDC       | WD10SPZX-35Z10T0   | 1 TB   | 6       | 208   | 0     | 0.57   |
| Seagate   | ST5000VX0011-1T... | 5 TB   | 1       | 208   | 0     | 0.57   |
| WDC       | WD5000BEKT-80KA9T0 | 500 GB | 3       | 317   | 1     | 0.57   |
| WDC       | WD800BEVS-00RST0   | 80 GB  | 3       | 277   | 1     | 0.57   |
| HGST      | HTS725050A7E630    | 500 GB | 172     | 383   | 244   | 0.57   |
| Fujitsu   | MHZ2160BH G1       | 160 GB | 8       | 279   | 1     | 0.57   |
| WDC       | WD1600BEVT-22A23T0 | 160 GB | 26      | 360   | 5     | 0.57   |
| IBM/Hi... | IC35L040AVVN07-0   | 41 GB  | 2       | 576   | 3     | 0.57   |
| WDC       | WD400BB-00FJA0     | 40 GB  | 2       | 699   | 222   | 0.57   |
| Seagate   | ST32500NSSUN250G   | 250 GB | 1       | 1455  | 6     | 0.57   |
| WDC       | WD10SPCX-21KHST0   | 1 TB   | 4       | 207   | 0     | 0.57   |
| HGST      | HTE725050A7E630    | 500 GB | 3       | 207   | 0     | 0.57   |
| Seagate   | ST500LT032-1E9142  | 500 GB | 4       | 207   | 0     | 0.57   |
| Samsung   | SP0802N            | 80 GB  | 27      | 685   | 46    | 0.57   |
| Toshiba   | MK2575GSX          | 250 GB | 2       | 272   | 538   | 0.56   |
| Seagate   | ST9160823ASG       | 160 GB | 3       | 329   | 337   | 0.56   |
| Samsung   | HD200HJ            | 200 GB | 18      | 825   | 631   | 0.56   |
| WDC       | WD10EURS-630AB1    | 1 TB   | 1       | 1846  | 8     | 0.56   |
| WDC       | WD1200JB-00GVC0    | 120 GB | 3       | 539   | 4     | 0.56   |
| WDC       | WD10JPLX-00MBPT0   | 1 TB   | 34      | 216   | 5     | 0.56   |
| WDC       | WD60EZRZ-00RWYB1   | 6 TB   | 5       | 215   | 405   | 0.56   |
| Hitachi   | HTS723232L9SA60    | 320 GB | 2       | 292   | 4     | 0.56   |
| Maxtor    | 6V250F0            | 250 GB | 3       | 497   | 2     | 0.56   |
| Toshiba   | HDWA120            | 2 TB   | 5       | 203   | 0     | 0.56   |
| WDC       | WD3200BEKX-60B7WT0 | 320 GB | 2       | 203   | 0     | 0.56   |
| Toshiba   | MK6006GAH          | 64 GB  | 2       | 203   | 0     | 0.56   |
| Fujitsu   | MHY2160BH          | 160 GB | 17      | 303   | 278   | 0.56   |
| WDC       | WD10EZRZ-00HTKB0   | 1 TB   | 55      | 209   | 1     | 0.56   |
| Seagate   | ST500DM009-2F110A  | 500 GB | 26      | 209   | 24    | 0.56   |
| Toshiba   | MK1653GSX          | 160 GB | 1       | 201   | 0     | 0.55   |
| WDC       | WD800JD-00JNC0     | 80 GB  | 4       | 451   | 16    | 0.55   |
| Seagate   | ST6000DM003-2CY186 | 6 TB   | 14      | 201   | 0     | 0.55   |
| Toshiba   | HDWJ110            | 1 TB   | 9       | 232   | 126   | 0.55   |
| Toshiba   | HDWF180            | 8 TB   | 12      | 210   | 135   | 0.55   |
| Samsung   | HD103UI            | 1 TB   | 3       | 671   | 1018  | 0.55   |
| Hitachi   | HTS721080G9SA00    | 80 GB  | 8       | 342   | 26    | 0.55   |
| Seagate   | ST500VT000-1BS142  | 500 GB | 2       | 200   | 0     | 0.55   |
| Seagate   | ST6000VN0001-1S... | 6 TB   | 1       | 200   | 0     | 0.55   |
| WDC       | WD740GD-00FLC0     | 74 GB  | 1       | 1202  | 5     | 0.55   |
| Hitachi   | HTS543225A7A384    | 250 GB | 38      | 349   | 352   | 0.55   |
| HGST      | HDN726040ALE614    | 4 TB   | 4       | 307   | 68    | 0.55   |
| WDC       | WD5000BEVT-00A0RT0 | 500 GB | 13      | 386   | 173   | 0.55   |
| Fujitsu   | MHY2080BH          | 80 GB  | 5       | 464   | 207   | 0.55   |
| Toshiba   | MK6034GAX          | 64 GB  | 4       | 663   | 352   | 0.55   |
| WDC       | WD1600BEVT-24A23T0 | 160 GB | 11      | 227   | 2     | 0.54   |
| Toshiba   | HDWE140            | 4 TB   | 24      | 255   | 48    | 0.54   |
| WDC       | WD30EZRS-11J99B1   | 3 TB   | 2       | 792   | 332   | 0.54   |
| WDC       | WD10EZEX-00MFCA0   | 1 TB   | 21      | 227   | 4     | 0.54   |
| Seagate   | ST8000DM004-2CX188 | 8 TB   | 60      | 221   | 29    | 0.54   |
| WDC       | WD5000AARS-003BB1  | 500 GB | 5       | 568   | 7     | 0.54   |
| WDC       | WD3200BEKT-08PVMT1 | 320 GB | 3       | 195   | 0     | 0.54   |
| Quantum   | FIREBALLlct15 30   | 32 GB  | 1       | 391   | 1     | 0.54   |
| Hitachi   | HDS721612PLAT80    | 128 GB | 1       | 1366  | 6     | 0.53   |
| Toshiba   | MK6034GSX          | 64 GB  | 4       | 423   | 18    | 0.53   |
| Seagate   | ST94011A           | 40 GB  | 1       | 194   | 0     | 0.53   |
| Fujitsu   | MHW2080BJ G2       | 80 GB  | 2       | 362   | 66    | 0.53   |
| Seagate   | ST320414A          | 20 GB  | 1       | 194   | 0     | 0.53   |
| Hitachi   | HTS723232A7A364    | 320 GB | 55      | 451   | 458   | 0.53   |
| WDC       | WD1600AAJS-60M0A1  | 160 GB | 3       | 840   | 343   | 0.53   |
| WDC       | WD5000LPCX-22VHAT0 | 500 GB | 28      | 198   | 1     | 0.53   |
| Seagate   | ST9320423AS        | 320 GB | 67      | 472   | 314   | 0.53   |
| Seagate   | ST3120213A         | 120 GB | 12      | 662   | 642   | 0.53   |
| IBM       | DARA-212000        | 12 GB  | 1       | 193   | 0     | 0.53   |
| Toshiba   | HDWT140            | 4 TB   | 1       | 193   | 0     | 0.53   |
| WDC       | WD400BB-00DKA0     | 40 GB  | 1       | 193   | 0     | 0.53   |
| WDC       | WD800BEVS-75RST0   | 80 GB  | 4       | 381   | 252   | 0.53   |
| Toshiba   | MK1059GSM          | 1 TB   | 32      | 596   | 803   | 0.53   |
| Seagate   | ST10000NM0478-2... | 10 TB  | 1       | 192   | 0     | 0.53   |
| WDC       | WD1600AAJS-60Z0A0  | 160 GB | 6       | 306   | 175   | 0.53   |
| WDC       | WD5000LPLX-08ZNTT0 | 500 GB | 18      | 241   | 1     | 0.53   |
| WDC       | WD10SPZX-17Z10T0   | 1 TB   | 6       | 192   | 0     | 0.53   |
| WDC       | WD10PURZ-85U8XY0   | 1 TB   | 8       | 207   | 1     | 0.53   |
| WDC       | WD10SPZX-75Z10T1   | 1 TB   | 14      | 208   | 3     | 0.53   |
| Hitachi   | HTS543212L9SA02    | 120 GB | 2       | 192   | 0     | 0.53   |
| WDC       | WD10PURX-64D85Y0   | 1 TB   | 4       | 388   | 2     | 0.53   |
| Fujitsu   | MHZ2250BH G2       | 250 GB | 17      | 547   | 575   | 0.53   |
| WDC       | WD30NMRW-11YL9S4   | 3 TB   | 1       | 192   | 0     | 0.53   |
| Toshiba   | MK6475GSX          | 640 GB | 33      | 398   | 293   | 0.53   |
| Hitachi   | HTS547564A9E384    | 640 GB | 47      | 509   | 453   | 0.53   |
| Samsung   | HM100UI            | 1 TB   | 5       | 191   | 0     | 0.53   |
| Toshiba   | MQ03UBB300         | 3 TB   | 8       | 230   | 6     | 0.52   |
| Seagate   | ST1000DM010-2EP102 | 1 TB   | 359     | 213   | 16    | 0.52   |
| WDC       | WD6400BPVT-22HXZT1 | 640 GB | 5       | 259   | 2     | 0.52   |
| WDC       | WD1600AVVS-63L2B0  | 160 GB | 7       | 714   | 3     | 0.52   |
| WDC       | WD5000LPVX-55V0TT0 | 500 GB | 13      | 254   | 1     | 0.52   |
| WDC       | WD4001FAEX-00MJRA0 | 4 TB   | 1       | 190   | 0     | 0.52   |
| Seagate   | ST9120822AS        | 120 GB | 54      | 450   | 441   | 0.52   |
| Samsung   | HD161HJ 41R0186LEN | 160 GB | 2       | 551   | 507   | 0.52   |
| WDC       | WD5000BPVT-26HXZT3 | 500 GB | 1       | 190   | 0     | 0.52   |
| Seagate   | ST250LM004 HN-M... | 250 GB | 10      | 278   | 5     | 0.52   |
| WDC       | WD5000KMVW-11ZSMS5 | 500 GB | 1       | 189   | 0     | 0.52   |
| WDC       | WD60EZRZ-00GZ5B1   | 6 TB   | 8       | 189   | 0     | 0.52   |
| Seagate   | ST9500420AS        | 500 GB | 107     | 589   | 516   | 0.52   |
| Seagate   | ST96812A           | 64 GB  | 3       | 379   | 758   | 0.52   |
| WDC       | WD2500BJKT-00F4T0  | 250 GB | 2       | 187   | 0     | 0.51   |
| WDC       | WD5000LPLX-75ZNTT0 | 500 GB | 13      | 187   | 0     | 0.51   |
| WDC       | WD5000BEVT-60A0RT0 | 500 GB | 2       | 764   | 91    | 0.51   |
| Seagate   | ST500VM000-1SD101  | 500 GB | 3       | 186   | 0     | 0.51   |
| Seagate   | ST320LT009-9WC142  | 320 GB | 3       | 277   | 1     | 0.51   |
| Toshiba   | MK3265GSXN         | 320 GB | 21      | 503   | 252   | 0.51   |
| WDC       | WD20EARS-60MVWB0   | 2 TB   | 4       | 615   | 776   | 0.51   |
| WDC       | WD5000BPKX-22HPJT0 | 500 GB | 15      | 287   | 2     | 0.51   |
| WDC       | WD10JPVT-22A1YT0   | 1 TB   | 9       | 382   | 3     | 0.51   |
| WDC       | WD3200LPCX-24C6HT0 | 320 GB | 22      | 185   | 0     | 0.51   |
| Apple     | HDD ST3000DM001    | 3 TB   | 1       | 185   | 0     | 0.51   |
| Maxtor    | 7V300F0            | 304 GB | 2       | 1022  | 475   | 0.51   |
| WDC       | WD40EZRZ-75GXCB0   | 4 TB   | 11      | 184   | 0     | 0.50   |
| WDC       | WD2500BEKT-60A25T1 | 250 GB | 11      | 428   | 102   | 0.50   |
| WDC       | WD1200BB-00GUC0    | 120 GB | 3       | 939   | 9     | 0.50   |
| Seagate   | ST3750528AS        | 752 GB | 42      | 687   | 370   | 0.50   |
| Quantum   | FIREBALLlct15 15   | 16 GB  | 1       | 183   | 0     | 0.50   |
| Hitachi   | HTS545025B9SA02    | 250 GB | 12      | 294   | 181   | 0.50   |
| Hitachi   | HDT722525DLAT80    | 250 GB | 2       | 733   | 3     | 0.50   |
| Samsung   | SP2504C            | 250 GB | 51      | 1110  | 725   | 0.50   |
| Fujitsu   | MHZ2500BT G1       | 500 GB | 2       | 1426  | 6     | 0.50   |
| IBM/Hi... | IC25N030ATMR04-0   | 32 GB  | 1       | 544   | 2     | 0.50   |
| Toshiba   | MK2561GSYN         | 250 GB | 5       | 183   | 11    | 0.50   |
| WDC       | WD5000AAKS-60Z1A0  | 500 GB | 6       | 1214  | 64    | 0.50   |
| WDC       | WD6000BLHX-01V7BV0 | 600 GB | 2       | 181   | 0     | 0.50   |
| Seagate   | ST160NM0011 39M... | 160 GB | 1       | 361   | 1     | 0.50   |
| WDC       | WD5000AUDX-73H9TY0 | 500 GB | 1       | 180   | 0     | 0.49   |
| WDC       | WD1200JB-00FUA0    | 120 GB | 1       | 180   | 0     | 0.49   |
| Seagate   | ST3250310CS        | 250 GB | 2       | 701   | 21    | 0.49   |
| Samsung   | SP1613N            | 160 GB | 2       | 858   | 508   | 0.49   |
| WDC       | WD80EZAZ-11TDBA0   | 8 TB   | 26      | 179   | 0     | 0.49   |
| Seagate   | STM31000528AS      | 1 TB   | 3       | 351   | 1     | 0.49   |
| WDC       | WD3200LPVX-75V0TT0 | 320 GB | 3       | 179   | 0     | 0.49   |
| Hitachi   | HTS543225L9A300    | 250 GB | 39      | 525   | 206   | 0.49   |
| Samsung   | HE753LJ            | 752 GB | 2       | 374   | 51    | 0.49   |
| WDC       | WD5000AZDX-00SC2B0 | 500 GB | 5       | 457   | 11    | 0.49   |
| Hitachi   | HTS541616J9SA00    | 160 GB | 39      | 536   | 68    | 0.49   |
| WDC       | WD2500JS-63MHB5    | 250 GB | 2       | 793   | 39    | 0.49   |
| Seagate   | ST9500423AS        | 500 GB | 39      | 463   | 91    | 0.49   |
| Toshiba   | MK8034GSX          | 80 GB  | 9       | 368   | 34    | 0.49   |
| MediaMax  | WL3000GSA6454      | 3.7 TB | 1       | 178   | 0     | 0.49   |
| WDC       | WD10EARX-00PASB0   | 1 TB   | 5       | 660   | 16    | 0.49   |
| WDC       | WD3200BPVT-80ZEST0 | 320 GB | 35      | 359   | 40    | 0.49   |
| WDC       | WD1002FBYS-18A6B0  | 1 TB   | 2       | 2270  | 29    | 0.49   |
| WDC       | WD3200BEVT-75ZCT0  | 320 GB | 3       | 671   | 57    | 0.49   |
| WDC       | WD10SPCX-08HWST0   | 1 TB   | 1       | 177   | 0     | 0.49   |
| Samsung   | SP1213C            | 120 GB | 9       | 713   | 26    | 0.49   |
| WDC       | WD20EADS-42R6B0    | 2 TB   | 1       | 176   | 0     | 0.48   |
| Seagate   | ST500LM014 HN-M... | 500 GB | 7       | 271   | 2     | 0.48   |
| Seagate   | ST3300822AS        | 304 GB | 1       | 176   | 0     | 0.48   |
| Samsung   | HM250JI            | 250 GB | 8       | 401   | 195   | 0.48   |
| WDC       | WD3200BEVT-24A23T0 | 320 GB | 10      | 529   | 103   | 0.48   |
| Samsung   | HD120IJ            | 120 GB | 24      | 839   | 377   | 0.48   |
| WDC       | WD10SPCX-11HWST0   | 1 TB   | 1       | 351   | 1     | 0.48   |
| Samsung   | HM080HC            | 72 GB  | 1       | 526   | 2     | 0.48   |
| Toshiba   | MK2035GSS          | 200 GB | 16      | 535   | 31    | 0.48   |
| Seagate   | ST980210AS         | 80 GB  | 1       | 175   | 0     | 0.48   |
| Seagate   | ST3250312CS        | 250 GB | 14      | 415   | 182   | 0.48   |
| Seagate   | ST9160827AS        | 160 GB | 38      | 482   | 315   | 0.48   |
| Seagate   | ST500LM021-1KJ152  | 500 GB | 92      | 305   | 252   | 0.48   |
| Hitachi   | HTS545032B9SA02    | 320 GB | 3       | 709   | 30    | 0.48   |
| HGST      | HUS726040ALA614    | 4 TB   | 6       | 177   | 3     | 0.48   |
| Toshiba   | MK5055GSX          | 500 GB | 18      | 515   | 156   | 0.48   |
| WDC       | WD2500BPVT-22ZEST0 | 250 GB | 19      | 214   | 4     | 0.48   |
| Toshiba   | MK2555GSXF         | 250 GB | 7       | 174   | 0     | 0.48   |
| WDC       | WD2500JD-40HBC0    | 250 GB | 1       | 1391  | 7     | 0.48   |
| WDC       | WD10SPCX-16HWST0   | 1 TB   | 1       | 173   | 0     | 0.48   |
| WDC       | WD1600BEVT-35ZCT0  | 160 GB | 2       | 173   | 0     | 0.48   |
| HGST      | HTS545050A7E380    | 500 GB | 188     | 383   | 277   | 0.48   |
| Samsung   | SP0812C            | 80 GB  | 19      | 592   | 257   | 0.48   |
| WDC       | WD1005FBYZ-01YCBB2 | 1 TB   | 3       | 173   | 0     | 0.48   |
| Toshiba   | MK1655GSX          | 160 GB | 17      | 384   | 55    | 0.47   |
| Toshiba   | MK1059GSMP         | 1 TB   | 20      | 496   | 413   | 0.47   |
| Toshiba   | MK1629GSG          | 160 GB | 4       | 372   | 26    | 0.47   |
| HGST      | HTS541075A9E680    | 752 GB | 49      | 385   | 630   | 0.47   |
| Toshiba   | HDWD105            | 500 GB | 88      | 191   | 24    | 0.47   |
| WDC       | WD1600BEVT-88ZCT0  | 160 GB | 2       | 171   | 0     | 0.47   |
| Seagate   | ST2000LM007-1R8174 | 2 TB   | 93      | 203   | 131   | 0.47   |
| Hitachi   | HTS542580K9SA00    | 80 GB  | 12      | 324   | 4     | 0.47   |
| Hitachi   | HTS543232A7A384    | 320 GB | 202     | 330   | 296   | 0.47   |
| WDC       | WD6400BPVT-80HXZT1 | 640 GB | 8       | 494   | 135   | 0.47   |
| Hitachi   | HCS5C1010DLE630    | 1 TB   | 1       | 169   | 0     | 0.47   |
| WDC       | WD3200BJKT-00F4T0  | 320 GB | 1       | 169   | 0     | 0.46   |
| Samsung   | HM250HJ            | 250 GB | 2       | 337   | 17    | 0.46   |
| WDC       | WD2500LPCX-24C6HT0 | 250 GB | 43      | 216   | 75    | 0.46   |
| Hitachi   | HTS545050A7E380    | 500 GB | 140     | 377   | 207   | 0.46   |
| Seagate   | ST1000DM000-9TS15E | 1 TB   | 1       | 168   | 0     | 0.46   |
| Hitachi   | HTS541060G9AT00    | 64 GB  | 7       | 520   | 15    | 0.46   |
| WDC       | WD120EFAX-68UNTN0  | 12 TB  | 2       | 168   | 0     | 0.46   |
| Seagate   | ST3400832A         | 400 GB | 1       | 2185  | 12    | 0.46   |
| Toshiba   | MK5059GSXP         | 500 GB | 39      | 420   | 347   | 0.46   |
| Seagate   | ST980310AS         | 80 GB  | 2       | 246   | 1     | 0.46   |
| WDC       | WD1600BEVS-22VAT0  | 160 GB | 2       | 248   | 1     | 0.46   |
| WDC       | WD10JPVX-60JC3T1   | 1 TB   | 30      | 208   | 40    | 0.46   |
| Seagate   | ST2000NM0011       | 2 TB   | 4       | 826   | 15    | 0.46   |
| Toshiba   | HDWD110            | 1 TB   | 208     | 183   | 5     | 0.46   |
| Hitachi   | HTS541612J9SA00 3H | 120 GB | 2       | 558   | 93    | 0.46   |
| WDC       | WD5000MPCK-60AWHT0 | 500 GB | 1       | 166   | 0     | 0.46   |
| Seagate   | ST3250820NS        | 250 GB | 2       | 695   | 1050  | 0.46   |
| Seagate   | ST9320325AS        | 320 GB | 268     | 474   | 441   | 0.46   |
| WDC       | WD3200LPVT-00FMCT0 | 320 GB | 3       | 476   | 3     | 0.46   |
| HGST      | HTS541515A9E630    | 1.5 TB | 4       | 587   | 265   | 0.46   |
| Seagate   | ST980811AS         | 80 GB  | 28      | 435   | 392   | 0.45   |
| Hitachi   | HTS543216L9SA00    | 160 GB | 17      | 345   | 68    | 0.45   |
| WDC       | WD10SPZX-24Z10T0   | 1 TB   | 31      | 178   | 1     | 0.45   |
| Hitachi   | HDP725016GLA380    | 160 GB | 9       | 642   | 287   | 0.45   |
| Seagate   | ST380211AS         | 80 GB  | 10      | 599   | 659   | 0.45   |
| Lenovo    | ST1000NM0055 91... | 1 TB   | 1       | 165   | 0     | 0.45   |
| Seagate   | ST9100824A         | 100 GB | 1       | 165   | 0     | 0.45   |
| WDC       | WD800BEVE-00A0HT0  | 80 GB  | 1       | 165   | 0     | 0.45   |
| WDC       | WD3200BEVT-60ZCT1  | 320 GB | 7       | 436   | 210   | 0.45   |
| WDC       | WD3200AAJB-00J3A0  | 320 GB | 20      | 429   | 24    | 0.45   |
| Samsung   | HD155UI            | 1.5 TB | 3       | 1164  | 599   | 0.45   |
| IBM/Hi... | IC35L120AVV207-1   | 128 GB | 2       | 496   | 9     | 0.45   |
| Toshiba   | MK7575GSX          | 752 GB | 30      | 650   | 680   | 0.45   |
| Seagate   | ST920217AS         | 20 GB  | 1       | 162   | 0     | 0.44   |
| WDC       | WD20PURZ-85GU6Y0   | 2 TB   | 14      | 280   | 142   | 0.44   |
| WDC       | WD20EFAX-68FB5N0   | 2 TB   | 9       | 161   | 0     | 0.44   |
| Toshiba   | MK8037GSX          | 80 GB  | 19      | 448   | 139   | 0.44   |
| Toshiba   | MK8007GAH          | 80 GB  | 2       | 210   | 7     | 0.44   |
| Hitachi   | HDS722512VLAT20    | 128 GB | 1       | 805   | 4     | 0.44   |
| WDC       | WD3200JD-60KLB0    | 320 GB | 1       | 965   | 5     | 0.44   |
| WDC       | WD10SPZX-22Z10T0   | 1 TB   | 14      | 160   | 0     | 0.44   |
| WDC       | WD10SPCX-80HWST0   | 1 TB   | 1       | 160   | 0     | 0.44   |
| Hitachi   | HTS725016A9A362    | 160 GB | 2       | 290   | 1     | 0.44   |
| Fujitsu   | MHZ2250BS G2       | 250 GB | 1       | 159   | 0     | 0.44   |
| WDC       | WD6400BEVT-80A0RT1 | 640 GB | 2       | 479   | 13    | 0.44   |
| WDC       | WD400BB-23FJA0     | 40 GB  | 1       | 796   | 4     | 0.44   |
| WDC       | WD140EMFZ-11A0WA0  | 14 TB  | 11      | 188   | 1     | 0.44   |
| HGST      | HTS541010B7E610    | 1 TB   | 47      | 175   | 3     | 0.44   |
| WDC       | WD10EAVS-22D7B0    | 1 TB   | 2       | 1426  | 8     | 0.43   |
| WDC       | WD1600AAJB-00J3A0  | 160 GB | 17      | 521   | 126   | 0.43   |
| Seagate   | ST9500325ASG       | 500 GB | 6       | 344   | 286   | 0.43   |
| Toshiba   | MQ01ACF050         | 500 GB | 47      | 271   | 91    | 0.43   |
| WDC       | WD2500BEVT-80A23T0 | 250 GB | 21      | 308   | 39    | 0.43   |
| WDC       | WD3200BEVT-26A23T0 | 320 GB | 3       | 274   | 73    | 0.43   |
| Seagate   | ST910021AS         | 100 GB | 7       | 582   | 469   | 0.43   |
| WDC       | WD5000M22K-24Z1... | 500 GB | 2       | 596   | 10    | 0.43   |
| Toshiba   | MK3276GSXN         | 320 GB | 1       | 156   | 0     | 0.43   |
| Seagate   | ST500LT012-1DG142  | 500 GB | 508     | 243   | 86    | 0.43   |
| WDC       | WD3200BPVT-75ZEST0 | 320 GB | 4       | 675   | 7     | 0.43   |
| Samsung   | SP0842N            | 80 GB  | 12      | 605   | 565   | 0.43   |
| Seagate   | STM9120817AS       | 120 GB | 1       | 155   | 0     | 0.43   |
| Seagate   | ST9160301AS        | 160 GB | 8       | 207   | 252   | 0.42   |
| WDC       | WD2500BEVT-08A23T1 | 250 GB | 13      | 270   | 133   | 0.42   |
| Toshiba   | MK6459GSX          | 640 GB | 6       | 495   | 577   | 0.42   |
| Toshiba   | MQ01ABD050         | 500 GB | 157     | 329   | 253   | 0.42   |
| Hitachi   | HTS722012K9A300    | 120 GB | 2       | 695   | 108   | 0.42   |
| WDC       | WD60EZAZ-00ZGHB0   | 6 TB   | 7       | 154   | 0     | 0.42   |
| WDC       | WD1200JD-55HBB0    | 120 GB | 1       | 923   | 5     | 0.42   |
| Samsung   | SV0412H            | 40 GB  | 6       | 1055  | 104   | 0.42   |
| MediaMax  | WL1000GSA6472B     | 1 TB   | 1       | 1379  | 8     | 0.42   |
| Toshiba   | MQ03ABB300         | 3 TB   | 2       | 152   | 0     | 0.42   |
| Seagate   | ST98823AS          | 80 GB  | 14      | 358   | 303   | 0.42   |
| WDC       | WD3200BPVT-60JJ5T0 | 320 GB | 10      | 363   | 119   | 0.42   |
| HGST      | HUH721010ALE604    | 10 TB  | 2       | 152   | 0     | 0.42   |
| WDC       | WD3200AAJS-56M0A0  | 320 GB | 22      | 377   | 46    | 0.42   |
| WDC       | WD10EARX-00NYB0    | 1 TB   | 1       | 151   | 0     | 0.42   |
| WDC       | WD6400BEVT-22A0RT0 | 640 GB | 12      | 546   | 56    | 0.42   |
| WDC       | WD15NMVW-11AV3S2   | 1.5 TB | 1       | 151   | 0     | 0.42   |
| Seagate   | ST12000DM0007-2... | 12 TB  | 3       | 161   | 1     | 0.42   |
| Samsung   | HN-M320MBB         | 320 GB | 5       | 347   | 7     | 0.41   |
| HGST      | HTS541050A9E680    | 500 GB | 6       | 151   | 0     | 0.41   |
| Hitachi   | HDS721616PLAT80    | 160 GB | 5       | 774   | 25    | 0.41   |
| WDC       | WD3200AAKS-22L6A0  | 320 GB | 5       | 534   | 5     | 0.41   |
| WDC       | WD6400AADS-00M2B0  | 640 GB | 11      | 891   | 20    | 0.41   |
| WDC       | WD4003FRYZ-01F0DB0 | 4 TB   | 2       | 150   | 0     | 0.41   |
| Toshiba   | MD05ACA800         | 8 TB   | 1       | 149   | 0     | 0.41   |
| WDC       | WD60EMAZ-11LW3B0   | 6 TB   | 2       | 149   | 0     | 0.41   |
| Hitachi   | HTS727550A9E364    | 500 GB | 18      | 495   | 516   | 0.41   |
| WDC       | WD10JPLX-00MBPT1   | 1 TB   | 2       | 149   | 0     | 0.41   |
| Hitachi   | HDS721010KLA33R... | 1 TB   | 1       | 3734  | 24    | 0.41   |
| Seagate   | ST3200822A         | 200 GB | 6       | 1408  | 10    | 0.41   |
| Samsung   | SP1634N            | 160 GB | 1       | 298   | 1     | 0.41   |
| Hitachi   | HTS723225L9SA62    | 250 GB | 1       | 595   | 3     | 0.41   |
| Toshiba   | MD03ACA400V        | 4 TB   | 1       | 1037  | 6     | 0.41   |
| Fujitsu   | MHV2060AT          | 64 GB  | 2       | 528   | 4     | 0.41   |
| Samsung   | HM320HJ            | 320 GB | 5       | 303   | 355   | 0.41   |
| Seagate   | ST12000NM0008-2... | 12 TB  | 2       | 148   | 0     | 0.41   |
| WDC       | WD1200JS-22NCB1    | 120 GB | 1       | 1184  | 7     | 0.41   |
| Toshiba   | MQ01ABF050         | 500 GB | 412     | 194   | 71    | 0.41   |
| WDC       | WD30PURZ-85GU6Y0   | 3 TB   | 3       | 147   | 0     | 0.40   |
| WDC       | WD5000LPVX-28V0TT0 | 500 GB | 2       | 686   | 4     | 0.40   |
| WDC       | WD5000AVVS-63M8B0  | 500 GB | 1       | 1324  | 8     | 0.40   |
| Hitachi   | HDS722525VLSA80    | 250 GB | 2       | 370   | 17    | 0.40   |
| Toshiba   | MK4025GAS          | 40 GB  | 2       | 423   | 18    | 0.40   |
| Seagate   | ST750LM030-1KKG62  | 752 GB | 2       | 146   | 0     | 0.40   |
| WDC       | WD2500BEVT-00A0RT1 | 245 GB | 1       | 146   | 0     | 0.40   |
| MediaMax  | WL320GLSA854G      | 320 GB | 1       | 146   | 0     | 0.40   |
| WDC       | WD5000LPCX-22VHAT1 | 500 GB | 11      | 146   | 0     | 0.40   |
| Hitachi   | HTS545050KTA300    | 500 GB | 6       | 520   | 5     | 0.40   |
| Toshiba   | MK2546GSX          | 250 GB | 13      | 519   | 38    | 0.40   |
| Fujitsu   | MHV2060BHPL        | 64 GB  | 1       | 144   | 0     | 0.40   |
| Toshiba   | MQ04UBB400         | 4 TB   | 6       | 144   | 0     | 0.40   |
| WDC       | WD7500KMVW-11ZSMS4 | 752 GB | 1       | 434   | 2     | 0.40   |
| WDC       | WD5000LPCX-21VHAT0 | 500 GB | 68      | 154   | 1     | 0.40   |
| Toshiba   | MK5076GSX -63      | 500 GB | 2       | 144   | 0     | 0.40   |
| Seagate   | ST500LX025-1U717D  | 500 GB | 6       | 156   | 65    | 0.39   |
| Maxtor    | 6G160E0            | 160 GB | 8       | 327   | 156   | 0.39   |
| MARSHAL   | MAL2500HSA-T54L    | 500 GB | 1       | 143   | 0     | 0.39   |
| WDC       | WD3200AAJS-55VWA0  | 320 GB | 1       | 1006  | 6     | 0.39   |
| Seagate   | ST4000NC001-1FS168 | 4 TB   | 1       | 143   | 0     | 0.39   |
| Seagate   | ST96023AS          | 64 GB  | 2       | 395   | 5     | 0.39   |
| Samsung   | HN-M101MBB         | 1 TB   | 21      | 377   | 263   | 0.39   |
| HP        | VB0160EAVEQ        | 160 GB | 1       | 429   | 2     | 0.39   |
| WDC       | WD2500BPVT-24JJ5T0 | 250 GB | 4       | 142   | 0     | 0.39   |
| WDC       | WD30EFRX-68N32N0   | 3 TB   | 3       | 186   | 1     | 0.39   |
| Seagate   | ST1000LM048-2E7172 | 1 TB   | 112     | 180   | 86    | 0.39   |
| HP        | MB2000GCWLT        | 2 TB   | 2       | 1500  | 505   | 0.39   |
| Toshiba   | MQ04ABD200         | 2 TB   | 2       | 142   | 0     | 0.39   |
| WDC       | WD3200AAKX-32ERMA0 | 320 GB | 1       | 142   | 0     | 0.39   |
| Toshiba   | MK2555GSX          | 250 GB | 36      | 415   | 69    | 0.39   |
| Hitachi   | HTS541212H9AT00    | 120 GB | 3       | 438   | 5     | 0.39   |
| WDC       | WD3200LPVX-08V0TT5 | 320 GB | 3       | 141   | 0     | 0.39   |
| WDC       | WD7500KMVV-11TK7S1 | 752 GB | 1       | 141   | 0     | 0.39   |
| IBM       | DTLA-305020        | 20 GB  | 2       | 1494  | 37    | 0.39   |
| WDC       | WD7500BPVT-22HXZT1 | 752 GB | 5       | 731   | 208   | 0.39   |
| WDC       | WD800AAJS-00M0A0   | 80 GB  | 1       | 141   | 0     | 0.39   |
| WDC       | WD2500AAJB-57WGA0  | 250 GB | 1       | 140   | 0     | 0.38   |
| WDC       | WD7500BPVX-75JC3T0 | 752 GB | 3       | 301   | 2     | 0.38   |
| WDC       | WD5000LPLX-00ZNTT0 | 500 GB | 56      | 147   | 1     | 0.38   |
| WDC       | WD800BB-00HEA0     | 80 GB  | 1       | 840   | 5     | 0.38   |
| Seagate   | ST9160821AS        | 160 GB | 71      | 437   | 542   | 0.38   |
| Samsung   | HD256GJ            | 250 GB | 2       | 392   | 504   | 0.38   |
| WDC       | WD2500AAJS-07B4A0  | 250 GB | 2       | 1695  | 198   | 0.38   |
| WDC       | WD50NDZW-11MR8S1   | 5 TB   | 8       | 139   | 0     | 0.38   |
| WDC       | WD400EB-11CPF0     | 40 GB  | 2       | 1019  | 31    | 0.38   |
| Seagate   | ST320LT007-9ZV142  | 320 GB | 49      | 478   | 655   | 0.38   |
| Hitachi   | HTS542525K9SA00    | 250 GB | 36      | 535   | 95    | 0.38   |
| WDC       | WD2500JS-60MHB1    | 250 GB | 2       | 331   | 8     | 0.38   |
| WDC       | WD5000AAKS-08V0A0  | 500 GB | 8       | 488   | 35    | 0.38   |
| HP        | GB0750C8047        | 752 GB | 1       | 138   | 0     | 0.38   |
| Samsung   | SP0822N            | 80 GB  | 10      | 138   | 1     | 0.38   |
| Fujitsu   | MHX2250BT          | 250 GB | 4       | 307   | 5     | 0.38   |
| Seagate   | ST500LM000-SSHD... | 500 GB | 32      | 296   | 243   | 0.38   |
| WDC       | WD1600BEVT-75A23T0 | 160 GB | 6       | 196   | 1     | 0.38   |
| WDC       | WD10EURX-73FH1Y0   | 1 TB   | 5       | 595   | 3     | 0.38   |
| Seagate   | ST3160815SV        | 160 GB | 6       | 704   | 1035  | 0.38   |
| HGST      | HUS726T6TALE6L4    | 6 TB   | 3       | 137   | 0     | 0.38   |
| Seagate   | ST1000LM035-1RK172 | 1 TB   | 476     | 172   | 114   | 0.38   |
| Hitachi   | HTS542560K9SA00    | 64 GB  | 2       | 136   | 0     | 0.37   |
| Hitachi   | HCT721050SLA380    | 500 GB | 1       | 136   | 0     | 0.37   |
| Hitachi   | HTS541040G9AT00    | 40 GB  | 4       | 263   | 4     | 0.37   |
| WDC       | WD5000LPZX-22Z10T0 | 500 GB | 1       | 135   | 0     | 0.37   |
| Seagate   | ST33000651NS       | 3 TB   | 4       | 1376  | 341   | 0.37   |
| WDC       | WD800JD-00JNA0     | 80 GB  | 2       | 809   | 5     | 0.37   |
| WDC       | WD10EZEX-07WN4A0   | 1 TB   | 6       | 187   | 1     | 0.37   |
| Hitachi   | HTS545025A7E380    | 250 GB | 2       | 134   | 0     | 0.37   |
| WDC       | WD10JUCT-63J6SY0   | 1 TB   | 6       | 342   | 183   | 0.37   |
| WDC       | WD3201ABYS-01B9A0  | 320 GB | 2       | 926   | 278   | 0.37   |
| WDC       | WD3200AAKX-073CA1  | 320 GB | 2       | 342   | 4     | 0.37   |
| Toshiba   | MK8009GAH          | 80 GB  | 4       | 562   | 26    | 0.37   |
| Hitachi   | HTS542512K9SA00    | 120 GB | 63      | 486   | 129   | 0.37   |
| WDC       | WD1600JD-00HBB0    | 160 GB | 6       | 582   | 17    | 0.37   |
| WDC       | WD5000LPCX-24VHAT0 | 500 GB | 93      | 138   | 13    | 0.37   |
| HGST      | HDS5C4040ALE630    | 4 TB   | 2       | 133   | 0     | 0.37   |
| WDC       | WD10JPVX-08JC3T6   | 1 TB   | 5       | 201   | 1     | 0.37   |
| Seagate   | ST2000NM0055-1V... | 2 TB   | 2       | 133   | 0     | 0.37   |
| Seagate   | ST1000LX015-1U7172 | 1 TB   | 73      | 170   | 52    | 0.37   |
| Hitachi   | HTS543232L9A300    | 320 GB | 25      | 695   | 535   | 0.37   |
| Toshiba   | MK8025GAS          | 80 GB  | 3       | 140   | 20    | 0.36   |
| Samsung   | SP2514N            | 250 GB | 11      | 684   | 490   | 0.36   |
| Toshiba   | DT01ACA100 LENOVO  | 1 TB   | 4       | 132   | 0     | 0.36   |
| WDC       | WD80EFAX-68KNBN0   | 8 TB   | 11      | 132   | 0     | 0.36   |
| Seagate   | ST2000DM005-2CW102 | 2 TB   | 10      | 132   | 0     | 0.36   |
| WDC       | WD3200AVJS-63B6A0  | 320 GB | 7       | 1119  | 18    | 0.36   |
| Seagate   | ST3500410AS        | 500 GB | 30      | 992   | 365   | 0.36   |
| WDC       | WD3200BEVT-26ZCT0  | 320 GB | 6       | 250   | 17    | 0.36   |
| Seagate   | ST9500325AS        | 500 GB | 436     | 485   | 541   | 0.36   |
| HGST      | HTS545050A7E660    | 500 GB | 14      | 242   | 5     | 0.36   |
| Toshiba   | MQ02ABF100         | 1 TB   | 7       | 147   | 1     | 0.36   |
| Toshiba   | MG03ACA100         | 1 TB   | 9       | 251   | 3     | 0.36   |
| Seagate   | ST3120811AS        | 120 GB | 14      | 572   | 369   | 0.36   |
| WDC       | WD5000LPVX-00V0TT0 | 500 GB | 24      | 175   | 98    | 0.36   |
| Seagate   | ST1500DM003-9YN16G | 1.5 TB | 17      | 452   | 462   | 0.36   |
| WDC       | WD5000AZLX-35K2TA0 | 500 GB | 2       | 130   | 0     | 0.36   |
| Seagate   | ST10000DM0004-2... | 10 TB  | 3       | 129   | 0     | 0.36   |
| WDC       | WD20SDZW-11JJ8S0   | 2 TB   | 5       | 129   | 0     | 0.36   |
| WDC       | WD1600BEVT-60ZCT0  | 160 GB | 7       | 201   | 288   | 0.36   |
| Seagate   | ST9120822A         | 120 GB | 2       | 273   | 53    | 0.36   |
| Seagate   | ST340810A          | 40 GB  | 12      | 482   | 31    | 0.36   |
| WDC       | WD3200BEVT-00ZCT0  | 320 GB | 5       | 568   | 100   | 0.35   |
| Toshiba   | MK3265GSXF         | 320 GB | 5       | 276   | 20    | 0.35   |
| Toshiba   | MK2565GSX          | 250 GB | 28      | 351   | 176   | 0.35   |
| Seagate   | ST320LT012-1DG14C  | 320 GB | 23      | 205   | 50    | 0.35   |
| WDC       | WD10EADS-98M2B0    | 1 TB   | 1       | 899   | 6     | 0.35   |
| WDC       | WD800JD-22LSA1     | 80 GB  | 4       | 485   | 174   | 0.35   |
| WDC       | WD3200BEVT-00ZAT0  | 320 GB | 2       | 256   | 13    | 0.35   |
| WDC       | WD5000AZLX-08K2TA0 | 500 GB | 24      | 137   | 1     | 0.35   |
| Hitachi   | HTS541612J9SA00    | 120 GB | 69      | 568   | 80    | 0.35   |
| Hitachi   | HTS725050A9A364    | 500 GB | 28      | 487   | 741   | 0.35   |
| WDC       | WD40EZRZ-19GXCB0   | 4 TB   | 6       | 127   | 0     | 0.35   |
| Fujitsu   | MHT2040AH PL       | 40 GB  | 2       | 766   | 5     | 0.35   |
| Toshiba   | MK1034GSX          | 100 GB | 4       | 418   | 464   | 0.35   |
| Seagate   | ST9250315ASG       | 250 GB | 3       | 166   | 6     | 0.35   |
| HPE       | MM1000EBKAF        | 1 TB   | 2       | 127   | 0     | 0.35   |
| Seagate   | ST9250315AS        | 250 GB | 210     | 479   | 446   | 0.35   |
| WDC       | WD1600AAJS-56M0A0  | 160 GB | 2       | 469   | 4     | 0.35   |
| WDC       | WD1600BEVT-80A23T0 | 160 GB | 23      | 205   | 110   | 0.35   |
| China     | OOS250G            | 250 GB | 1       | 126   | 0     | 0.35   |
| WDC       | WD5000BPVT-55A1YT0 | 500 GB | 1       | 126   | 0     | 0.35   |
| Seagate   | ST3500830SCE       | 500 GB | 1       | 126   | 0     | 0.35   |
| ExcelStor | J8080S             | 82 GB  | 1       | 2405  | 18    | 0.35   |
| Toshiba   | HDWM110            | 1 TB   | 3       | 126   | 0     | 0.35   |
| WDC       | WD5000BEVT-11ZAT0  | 500 GB | 1       | 1007  | 7     | 0.34   |
| WDC       | WD5000LUCT-61C26Y0 | 500 GB | 1       | 1003  | 7     | 0.34   |
| Toshiba   | MK1216GSG          | 120 GB | 3       | 272   | 4     | 0.34   |
| WDC       | WD1600BJKT-75F4T0  | 160 GB | 6       | 490   | 10    | 0.34   |
| Seagate   | ST500LT015-1DJ142  | 500 GB | 1       | 124   | 0     | 0.34   |
| Toshiba   | MQ01ABD064         | 640 GB | 1       | 124   | 0     | 0.34   |
| WDC       | WD3200AAKS-00C9A0  | 320 GB | 3       | 1080  | 8     | 0.34   |
| WDC       | WD1600BEKT-60A25T1 | 160 GB | 3       | 137   | 1     | 0.34   |
| Toshiba   | DT01ACA200V        | 2 TB   | 1       | 124   | 0     | 0.34   |
| Seagate   | ST4000VX007-2DT166 | 4 TB   | 6       | 123   | 0     | 0.34   |
| WDC       | WD1600HLHX-60JJPV1 | 160 GB | 1       | 617   | 4     | 0.34   |
| WDC       | WD8000AARS-00Y5B1  | 800 GB | 3       | 1740  | 14    | 0.34   |
| Samsung   | HD080HJ-P          | 80 GB  | 11      | 683   | 452   | 0.34   |
| Samsung   | HM321HX            | 320 GB | 3       | 176   | 3     | 0.34   |
| Seagate   | ST3000DM007-1WY10G | 3 TB   | 10      | 122   | 0     | 0.34   |
| Toshiba   | MK7559GSXF         | 752 GB | 4       | 178   | 319   | 0.33   |
| WDC       | WD2500BEVE-00A0HT0 | 250 GB | 2       | 120   | 0     | 0.33   |
| Toshiba   | MK3265GSX          | 320 GB | 62      | 613   | 222   | 0.33   |
| HGST      | HTE721010A9E630    | 1 TB   | 5       | 120   | 0     | 0.33   |
| Toshiba   | MK2565GSXN         | 250 GB | 4       | 438   | 10    | 0.33   |
| WDC       | WD5000LPLX-60ZNTT1 | 500 GB | 16      | 189   | 46    | 0.33   |
| Toshiba   | MG06ACA600E        | 6 TB   | 2       | 119   | 0     | 0.33   |
| Seagate   | ST9100827AS        | 100 GB | 1       | 838   | 6     | 0.33   |
| WDC       | WD5001AALS-00J7B1  | 500 GB | 1       | 1077  | 8     | 0.33   |
| Seagate   | ST960821A          | 64 GB  | 1       | 358   | 2     | 0.33   |
| Toshiba   | MK6025GAS          | 64 GB  | 2       | 166   | 9     | 0.33   |
| Seagate   | ST2000DM008-2FR102 | 2 TB   | 173     | 128   | 17    | 0.33   |
| Toshiba   | MK2556GSY          | 250 GB | 5       | 239   | 436   | 0.32   |
| Hitachi   | HTS545032B9A302    | 320 GB | 6       | 272   | 5     | 0.32   |
| WDC       | WD10SPZX-22Z10T1   | 1 TB   | 11      | 118   | 0     | 0.32   |
| WDC       | WD3200BEVS-26VAT0  | 320 GB | 2       | 512   | 657   | 0.32   |
| Toshiba   | HDWG180            | 8 TB   | 2       | 117   | 0     | 0.32   |
| Seagate   | ST640LM001 HN-M... | 640 GB | 3       | 385   | 18    | 0.32   |
| WDC       | 500GB              | 500 GB | 1       | 1047  | 8     | 0.32   |
| WDC       | WD40NMZW-59LG6S1   | 4 TB   | 1       | 115   | 0     | 0.32   |
| Seagate   | ST500LM030-2E717D  | 500 GB | 36      | 128   | 40    | 0.32   |
| WDC       | WD5000BPVT-60HXZT3 | 500 GB | 11      | 471   | 141   | 0.32   |
| WDC       | WD5000BPVT-60HXZT1 | 500 GB | 4       | 579   | 543   | 0.31   |
| Hitachi   | HTS541010G9SA00    | 100 GB | 15      | 379   | 90    | 0.31   |
| WDC       | WD10EZEX-07M2NA0   | 1 TB   | 2       | 773   | 9     | 0.31   |
| Hitachi   | HTS541680J9SA00    | 80 GB  | 59      | 483   | 74    | 0.31   |
| WDC       | WD20SMZW-11JW8S0   | 2 TB   | 7       | 112   | 0     | 0.31   |
| Toshiba   | MK3259GSXP         | 320 GB | 58      | 328   | 204   | 0.31   |
| Toshiba   | MK2552GSX          | 250 GB | 16      | 910   | 289   | 0.31   |
| WDC       | WD3200AAKS-00YGA0  | 320 GB | 1       | 562   | 4     | 0.31   |
| Toshiba   | MQ01ABD050V -63    | 500 GB | 4       | 112   | 0     | 0.31   |
| WDC       | WD5000AADS-56S9B1  | 500 GB | 7       | 628   | 7     | 0.31   |
| Fujitsu   | MHW2040BH          | 40 GB  | 2       | 165   | 1     | 0.31   |
| Seagate   | ST9100824AS        | 100 GB | 5       | 351   | 7     | 0.31   |
| WDC       | WD10SPZX-21Z10T0   | 1 TB   | 98      | 118   | 9     | 0.31   |
| Seagate   | ST9100823A         | 96 GB  | 1       | 1007  | 8     | 0.31   |
| WDC       | WD5000LPCX-75VHAT0 | 500 GB | 14      | 111   | 0     | 0.31   |
| Seagate   | ST10000DM0004-1... | 10 TB  | 4       | 206   | 2     | 0.31   |
| Samsung   | HM500LI            | 500 GB | 2       | 222   | 1     | 0.31   |
| Seagate   | ST1000LM025 HN-... | 1 TB   | 29      | 115   | 1     | 0.31   |
| WDC       | WD20SMZW-11JW8S1   | 2 TB   | 1       | 111   | 0     | 0.30   |
| Magnet... | MD03200-AVDW-RO    | 320 GB | 2       | 110   | 0     | 0.30   |
| WDC       | WD8004FRYZ-01VAEB0 | 8 TB   | 5       | 110   | 0     | 0.30   |
| Seagate   | ST8000AS0003-2H... | 8 TB   | 5       | 110   | 0     | 0.30   |
| WDC       | WD400BD-75JMA0     | 40 GB  | 1       | 663   | 5     | 0.30   |
| HGST      | HTS545050A7E680    | 500 GB | 304     | 255   | 394   | 0.30   |
| WDC       | WD400JB-00FMA0     | 40 GB  | 2       | 656   | 8     | 0.30   |
| WDC       | WD7500BPVT-00HXZT3 | 752 GB | 8       | 512   | 11    | 0.30   |
| Toshiba   | MK3252GSX          | 320 GB | 28      | 577   | 148   | 0.30   |
| Fujitsu   | MHW2020BH          | 20 GB  | 2       | 109   | 0     | 0.30   |
| Samsung   | SP2004C            | 200 GB | 31      | 695   | 563   | 0.30   |
| WDC       | WD3000FYYZ-01UL1B0 | 3 TB   | 2       | 109   | 0     | 0.30   |
| WDC       | WD3200BEKT-00V5T0  | 320 GB | 1       | 109   | 0     | 0.30   |
| WDC       | WD20EADS-32S2B0    | 2 TB   | 1       | 1198  | 10    | 0.30   |
| Hitachi   | HTS541010A9E680    | 1 TB   | 17      | 533   | 918   | 0.30   |
| Seagate   | ST8000NM000A-2K... | 8 TB   | 1       | 108   | 0     | 0.30   |
| Samsung   | MP0402H            | 40 GB  | 8       | 306   | 20    | 0.30   |
| Toshiba   | HDWN160            | 6 TB   | 7       | 303   | 25    | 0.30   |
| Seagate   | ST9160823AS        | 160 GB | 6       | 886   | 558   | 0.30   |
| Samsung   | HM100UX            | 1 TB   | 2       | 186   | 4     | 0.29   |
| Fujitsu   | MHV2040BH PL       | 40 GB  | 1       | 107   | 0     | 0.29   |
| Seagate   | ST9160314AS        | 160 GB | 40      | 294   | 239   | 0.29   |
| WDC       | WD3200BEVT-88ZCT0  | 320 GB | 1       | 106   | 0     | 0.29   |
| Hitachi   | HTS542520K9SA00    | 200 GB | 4       | 658   | 11    | 0.29   |
| WDC       | WD5000BEVT-00SCST0 | 500 GB | 2       | 246   | 5     | 0.29   |
| WDC       | WD3000FYYZ-01UL1B1 | 3 TB   | 1       | 1381  | 12    | 0.29   |
| China     | TP00250GB          | 250 GB | 1       | 106   | 0     | 0.29   |
| WDC       | WD50EFRX-68MYMN1   | 5 TB   | 3       | 518   | 3     | 0.29   |
| Seagate   | ST10000NM0086-2... | 10 TB  | 6       | 106   | 0     | 0.29   |
| Fujitsu   | MHV2060BH PL       | 64 GB  | 6       | 105   | 3     | 0.29   |
| WDC       | WD3200BPVT-11HXZT3 | 320 GB | 1       | 104   | 0     | 0.29   |
| WDC       | WD5000LPLX-22ZNTT0 | 500 GB | 10      | 104   | 0     | 0.29   |
| Toshiba   | MK1251GSY          | 120 GB | 1       | 939   | 8     | 0.29   |
| Hitachi   | HTS725032A9A364    | 320 GB | 24      | 434   | 857   | 0.29   |
| WDC       | WD3200BPVT-35JJ5T0 | 320 GB | 1       | 104   | 0     | 0.29   |
| WDC       | WD7500BPVX-00JC3T0 | 752 GB | 2       | 104   | 0     | 0.29   |
| Seagate   | ST3750330NS        | 752 GB | 6       | 480   | 230   | 0.28   |
| WDC       | WD5000AAKX-19U6AA0 | 500 GB | 1       | 103   | 0     | 0.28   |
| Toshiba   | MK1637GSX          | 160 GB | 34      | 553   | 65    | 0.28   |
| WDC       | WD15NMVW-11EDZS7   | 1.5 TB | 1       | 103   | 0     | 0.28   |
| Seagate   | ST9320320AS        | 320 GB | 26      | 715   | 178   | 0.28   |
| Seagate   | ST9120817AS        | 120 GB | 10      | 399   | 450   | 0.28   |
| WDC       | WD1200BEVS-60UST0  | 120 GB | 12      | 431   | 315   | 0.28   |
| WDC       | WD30NMZW-11GX6S1   | 3 TB   | 3       | 138   | 1     | 0.28   |
| Hitachi   | HTS721060G9SA00    | 64 GB  | 3       | 664   | 13    | 0.28   |
| Toshiba   | MK8046GSX          | 80 GB  | 5       | 513   | 407   | 0.28   |
| WDC       | WD10SPZX-75Z10T2   | 1 TB   | 30      | 101   | 0     | 0.28   |
| WDC       | WD10EZRX-22A3KB0   | 1 TB   | 1       | 101   | 0     | 0.28   |
| WDC       | WD20SPZX-75UA7T0   | 2 TB   | 1       | 101   | 0     | 0.28   |
| WDC       | WD3202ABYS-01B7A0  | 320 GB | 3       | 581   | 5     | 0.28   |
| WDC       | WD120EMAZ-11BLFA0  | 12 TB  | 3       | 100   | 0     | 0.28   |
| WDC       | WD2500BPVT-75JJ5T0 | 250 GB | 5       | 256   | 3     | 0.28   |
| Seagate   | OOS3000G           | 3 TB   | 1       | 100   | 0     | 0.28   |
| WDC       | WD5000HHTZ-04N21V1 | 500 GB | 1       | 100   | 0     | 0.27   |
| WDC       | WD800BD-22MRA1     | 80 GB  | 3       | 994   | 49    | 0.27   |
| WDC       | WD3200AUDX-56WNHY0 | 320 GB | 3       | 100   | 0     | 0.27   |
| WDC       | WD10SPCX-75HWST0   | 1 TB   | 1       | 100   | 0     | 0.27   |
| Hitachi   | HTS545050B9SA00    | 500 GB | 9       | 767   | 785   | 0.27   |
| HGST      | HTE725032A7E630    | 320 GB | 1       | 99    | 0     | 0.27   |
| WDC       | WD1600JD-55HBB0    | 160 GB | 1       | 695   | 6     | 0.27   |
| WDC       | WD1600BEAS-00RRT0  | 160 GB | 1       | 99    | 0     | 0.27   |
| WDC       | WD10SPZX-08Z10     | 1 TB   | 18      | 98    | 0     | 0.27   |
| WDC       | WD5000AAKS-00M9A0  | 500 GB | 6       | 853   | 437   | 0.27   |
| Toshiba   | HDWU130            | 3 TB   | 1       | 97    | 0     | 0.27   |
| Toshiba   | MK1011GAH          | 100 GB | 7       | 299   | 125   | 0.27   |
| Toshiba   | MG06ACA10TE        | 10 TB  | 3       | 97    | 0     | 0.27   |
| Toshiba   | MG04ACA200E        | 2 TB   | 3       | 105   | 3     | 0.27   |
| WDC       | WD10SPCX-60HWST0   | 1 TB   | 1       | 97    | 0     | 0.27   |
| Seagate   | ST320LT020-9YG142  | 320 GB | 147     | 353   | 607   | 0.27   |
| WDC       | WD1600AAJS-65WAA0  | 160 GB | 2       | 928   | 1006  | 0.27   |
| Seagate   | ST380023A          | 80 GB  | 1       | 2897  | 29    | 0.26   |
| WDC       | WD30EZRZ-22Z5HB0   | 3 TB   | 3       | 96    | 0     | 0.26   |
| Seagate   | ST500VT001-1K6142  | 500 GB | 1       | 96    | 0     | 0.26   |
| Seagate   | ST3500412AS        | 500 GB | 25      | 778   | 487   | 0.26   |
| Hitachi   | HTS541080G9AT00    | 80 GB  | 14      | 602   | 111   | 0.26   |
| WDC       | WD1200BEVS-60RST0  | 120 GB | 1       | 766   | 7     | 0.26   |
| Toshiba   | MQ01ABF050M        | 500 GB | 10      | 95    | 0     | 0.26   |
| Samsung   | SP0401N            | 40 GB  | 1       | 95    | 0     | 0.26   |
| Samsung   | SP1614C            | 160 GB | 8       | 464   | 15    | 0.26   |
| WDC       | WD5000BEVT-22ZAT0  | 500 GB | 13      | 511   | 67    | 0.26   |
| Toshiba   | MK7559GSXP         | 752 GB | 24      | 428   | 479   | 0.26   |
| Toshiba   | MQ04ABF100         | 1 TB   | 211     | 104   | 32    | 0.26   |
| WDC       | WD2500AAJS-60M0A0  | 250 GB | 4       | 805   | 284   | 0.26   |
| WDC       | WD3200BEVT-00A23T0 | 320 GB | 3       | 146   | 9     | 0.26   |
| WDC       | WD40PURX-64NZ6Y0   | 4 TB   | 1       | 92    | 0     | 0.25   |
| Seagate   | ST9160412ASG       | 160 GB | 1       | 92    | 0     | 0.25   |
| WDC       | WD2500JS-19NCB1    | 250 GB | 1       | 92    | 0     | 0.25   |
| Fujitsu   | MJA2500BH G2       | 500 GB | 10      | 281   | 117   | 0.25   |
| WDC       | WD1600BPVT-22JJ5T0 | 160 GB | 1       | 91    | 0     | 0.25   |
| WDC       | WD10EZRZ-22HTKB0   | 1 TB   | 12      | 91    | 0     | 0.25   |
| WDC       | WD7500AAVS-00D7B1  | 752 GB | 1       | 2278  | 24    | 0.25   |
| WDC       | WD1600AAJS-61M0A0  | 160 GB | 1       | 90    | 0     | 0.25   |
| WDC       | WD40EFAX-68JH4N0   | 4 TB   | 8       | 90    | 0     | 0.25   |
| Fujitsu   | MHV2100BH PL       | 100 GB | 7       | 169   | 2     | 0.25   |
| Toshiba   | HDWL120            | 2 TB   | 9       | 89    | 0     | 0.25   |
| Seagate   | ST1000LM010-9YH146 | 1 TB   | 13      | 178   | 755   | 0.25   |
| WDC       | WD5000AZLX-22JKKA0 | 500 GB | 15      | 113   | 1     | 0.25   |
| Seagate   | ST31000340SV       | 1 TB   | 1       | 1616  | 17    | 0.25   |
| WDC       | WD3200BEVT-22A0RT0 | 320 GB | 5       | 218   | 4     | 0.25   |
| Hitachi   | HTS541616J9AT00    | 160 GB | 2       | 356   | 7     | 0.25   |
| Samsung   | HS082HB            | 80 GB  | 1       | 89    | 0     | 0.25   |
| Seagate   | ST320LT022-1AE142  | 320 GB | 2       | 170   | 2     | 0.25   |
| Toshiba   | HDWR180            | 8 TB   | 2       | 89    | 0     | 0.24   |
| Toshiba   | MK2046GSX          | 200 GB | 12      | 375   | 41    | 0.24   |
| WDC       | WD5000LPCX-60VHAT0 | 500 GB | 42      | 102   | 1     | 0.24   |
| Hitachi   | HTS543232L9SA02    | 320 GB | 2       | 903   | 43    | 0.24   |
| Fujitsu   | MHW2040AT          | 40 GB  | 1       | 88    | 0     | 0.24   |
| WDC       | WD3200AAKX-753CA1  | 320 GB | 2       | 221   | 4     | 0.24   |
| WDC       | WD20NPVZ-00WFZT0   | 2 TB   | 4       | 88    | 0     | 0.24   |
| Seagate   | ST8000VN004-2M2101 | 8 TB   | 14      | 88    | 0     | 0.24   |
| Seagate   | ST160LM000 HM161GI | 160 GB | 2       | 88    | 0     | 0.24   |
| IBM/Hi... | IC35L040AVER07-0   | 41 GB  | 3       | 700   | 8     | 0.24   |
| Hitachi   | HTS725032A7E630    | 320 GB | 2       | 625   | 514   | 0.24   |
| Toshiba   | MK1252GSX          | 120 GB | 9       | 490   | 101   | 0.24   |
| WDC       | WD1600JS-61MHB1    | 160 GB | 1       | 959   | 10    | 0.24   |
| Toshiba   | MK1246GSX          | 120 GB | 16      | 405   | 84    | 0.24   |
| WDC       | WD2000JB-22GVA0    | 200 GB | 1       | 694   | 7     | 0.24   |
| Seagate   | ST500LM001-1EL162  | 500 GB | 1       | 86    | 0     | 0.24   |
| WDC       | WD1200BEVS-22LAT0  | 120 GB | 1       | 86    | 0     | 0.24   |
| WDC       | WD1600BEVT-00A1TT0 | 160 GB | 2       | 273   | 3     | 0.24   |
| WDC       | WD5000AAKS-07A7B2  | 500 GB | 1       | 1709  | 19    | 0.23   |
| WDC       | WD20SPZX-22UA7T0   | 2 TB   | 10      | 85    | 0     | 0.23   |
| Samsung   | HD300LD            | 304 GB | 4       | 554   | 15    | 0.23   |
| WDC       | WD2500AAJS-75B4A0  | 250 GB | 3       | 351   | 7     | 0.23   |
| WDC       | WD60PURX-64T0ZY0   | 6 TB   | 2       | 83    | 0     | 0.23   |
| Toshiba   | MK5076GSX          | 500 GB | 45      | 167   | 175   | 0.23   |
| Toshiba   | MK8032GAX          | 80 GB  | 2       | 117   | 252   | 0.23   |
| HGST      | HUS726T4TALN6L4    | 4 TB   | 1       | 83    | 0     | 0.23   |
| Seagate   | ST3400620NS        | 400 GB | 2       | 1825  | 21    | 0.23   |
| Hitachi   | HTS542512K9A300    | 120 GB | 7       | 403   | 151   | 0.23   |
| Seagate   | ST9120821AS        | 120 GB | 8       | 323   | 1209  | 0.23   |
| Toshiba   | MK3021GAS          | 32 GB  | 1       | 495   | 5     | 0.23   |
| WDC       | WD5000AACS-00G8B0  | 500 GB | 6       | 788   | 10    | 0.23   |
| WDC       | WD10SPZX-24Z10     | 1 TB   | 86      | 84    | 1     | 0.23   |
| WDC       | WD2500AAKX-193CA0  | 250 GB | 1       | 82    | 0     | 0.23   |
| Seagate   | ST3320613AS        | 320 GB | 105     | 875   | 273   | 0.22   |
| Seagate   | ST9250410ASG       | 250 GB | 1       | 409   | 4     | 0.22   |
| WDC       | WD1600JD-41HBC0    | 160 GB | 1       | 1884  | 22    | 0.22   |
| WDC       | WD5000BPVT-08HXZT1 | 500 GB | 2       | 81    | 0     | 0.22   |
| IBM/Hi... | IC35L060AVV207-0   | 40 GB  | 1       | 326   | 3     | 0.22   |
| Toshiba   | HDWK105            | 500 GB | 10      | 81    | 0     | 0.22   |
| WDC       | WD5000AAKS-00H2B0  | 499 GB | 1       | 731   | 8     | 0.22   |
| WDC       | WD20SDRW-11VUUS0   | 2 TB   | 6       | 81    | 0     | 0.22   |
| WDC       | WD3000HLFS-01MZUV0 | 304 GB | 2       | 977   | 535   | 0.22   |
| Fujitsu   | MHT2080BH          | 80 GB  | 2       | 543   | 10    | 0.22   |
| WDC       | WD6400AAKS-75A7B0  | 640 GB | 2       | 208   | 2     | 0.22   |
| Seagate   | ST3250820AV        | 250 GB | 1       | 80    | 0     | 0.22   |
| WDC       | WD10J31X-00U3VT0   | 1 TB   | 1       | 80    | 0     | 0.22   |
| Hitachi   | HTS722020K9SA00    | 200 GB | 5       | 615   | 7     | 0.22   |
| WDC       | WD40NDZW-11MR8S1   | 4 TB   | 6       | 80    | 0     | 0.22   |
| WDC       | WD5000BMVW-11AJGS4 | 500 GB | 6       | 82    | 94    | 0.22   |
| Magnet... | MD03200-AJDW-RO    | 320 GB | 1       | 79    | 0     | 0.22   |
| Toshiba   | MK5065GSX          | 500 GB | 26      | 325   | 375   | 0.22   |
| Seagate   | ST500DM002-9YN14C  | 500 GB | 5       | 595   | 247   | 0.22   |
| WDC       | WD600BEVS-07LAT0   | 64 GB  | 1       | 635   | 7     | 0.22   |
| WDC       | WD400BB-75JHC0     | 40 GB  | 1       | 476   | 5     | 0.22   |
| Hitachi   | HTS542525K9A300    | 250 GB | 6       | 666   | 545   | 0.22   |
| WDC       | WD5000BEVT-60ZAT1  | 500 GB | 8       | 613   | 442   | 0.21   |
| Seagate   | ST3160812AS 41N... | 160 GB | 4       | 822   | 132   | 0.21   |
| WDC       | WD5000AZRX-00A3KB0 | 500 GB | 3       | 114   | 3     | 0.21   |
| Seagate   | ST1000LM049-2GH172 | 1 TB   | 109     | 101   | 37    | 0.21   |
| WDC       | WD7500BPVT-60HXZT1 | 752 GB | 4       | 557   | 44    | 0.21   |
| WDC       | WD10EAVS-14M4B0    | 1 TB   | 1       | 77    | 0     | 0.21   |
| Hitachi   | HTS543280L9A300    | 80 GB  | 3       | 93    | 1     | 0.21   |
| WDC       | WD7500LPCX-60KHST0 | 752 GB | 3       | 77    | 0     | 0.21   |
| WDC       | WD10EZEX-75WN4A1   | 1 TB   | 13      | 79    | 1     | 0.21   |
| Seagate   | ST9120823ASG       | 120 GB | 1       | 76    | 0     | 0.21   |
| Samsung   | SP1604N            | 160 GB | 4       | 413   | 94    | 0.21   |
| WDC       | WD141KRYZ-01C66B0  | 14 TB  | 3       | 76    | 0     | 0.21   |
| Fujitsu   | MHV2060AT PL       | 64 GB  | 3       | 851   | 16    | 0.21   |
| WDC       | WD5000KMVV-11BG7S0 | 500 GB | 1       | 152   | 1     | 0.21   |
| WDC       | WD3200BEKT-75F3T0  | 320 GB | 1       | 683   | 8     | 0.21   |
| WDC       | WD2502ABYS-50B7A1  | 250 GB | 1       | 1290  | 16    | 0.21   |
| Toshiba   | MK1646GSX          | 160 GB | 11      | 572   | 152   | 0.21   |
| Fujitsu   | MJA2250BH G2       | 250 GB | 8       | 471   | 133   | 0.21   |
| Toshiba   | MK6476GSXN         | 640 GB | 3       | 122   | 601   | 0.21   |
| Seagate   | ST3320813AS        | 320 GB | 5       | 820   | 70    | 0.20   |
| WDC       | WD400VE-07HDT0     | 40 GB  | 1       | 74    | 0     | 0.20   |
| WDC       | WD15NMVW-11AV3S3   | 1.5 TB | 1       | 743   | 9     | 0.20   |
| Seagate   | ST6000NE000-2KR101 | 6 TB   | 1       | 74    | 0     | 0.20   |
| Samsung   | HN-M750MBB         | 752 GB | 5       | 299   | 11    | 0.20   |
| WDC       | WD800VE-75HDT1     | 80 GB  | 1       | 369   | 4     | 0.20   |
| Seagate   | ST16000NM001G-2... | 16 TB  | 7       | 73    | 0     | 0.20   |
| WDC       | WD2500BPVT-22JJ5T0 | 250 GB | 10      | 253   | 212   | 0.20   |
| Hitachi   | HDE721050SLA330    | 500 GB | 1       | 2416  | 32    | 0.20   |
| WDC       | WD1500BLHX-01V7BV0 | 150 GB | 1       | 72    | 0     | 0.20   |
| WDC       | WD1600SD-01KCC0    | 160 GB | 1       | 2914  | 39    | 0.20   |
| WDC       | WD1004FBYZ-01YCBB1 | 1 TB   | 2       | 72    | 0     | 0.20   |
| WDC       | WD10JMVW-11S5XS1   | 1 TB   | 1       | 72    | 0     | 0.20   |
| WDC       | WD50NDZW-11A8JS1   | 5 TB   | 4       | 72    | 0     | 0.20   |
| WDC       | WD30NMZW-11LG6S1   | 3 TB   | 2       | 72    | 0     | 0.20   |
| Hitachi   | HTS722016K9A300    | 160 GB | 4       | 242   | 259   | 0.20   |
| WDC       | WD10EZEX-60WN4A1   | 1 TB   | 17      | 85    | 1     | 0.20   |
| Toshiba   | MK1237GSX          | 120 GB | 20      | 424   | 141   | 0.20   |
| Seagate   | ST9120411ASG       | 120 GB | 1       | 361   | 4     | 0.20   |
| WDC       | WD20NMVW-11AV3S4   | 2 TB   | 2       | 751   | 512   | 0.20   |
| WDC       | WD10SPZX-17Z10T1   | 1 TB   | 5       | 71    | 0     | 0.20   |
| Hitachi   | HTS725050A9A360    | 500 GB | 2       | 116   | 505   | 0.20   |
| WDC       | WD20EARS-22MVWB0   | 2 TB   | 3       | 2096  | 347   | 0.20   |
| Toshiba   | MQ01ABD032V -63    | 320 GB | 1       | 714   | 9     | 0.20   |
| HP        | MB1000EAMZE        | 1 TB   | 1       | 1919  | 26    | 0.19   |
| WDC       | WD10SPZX-00Z10T0   | 1 TB   | 21      | 70    | 0     | 0.19   |
| Seagate   | ST31000322CS       | 1 TB   | 3       | 935   | 34    | 0.19   |
| WDC       | WD20SPZX-21UA7T0   | 2 TB   | 1       | 70    | 0     | 0.19   |
| IBM       | DTLA-307015        | 16 GB  | 1       | 423   | 5     | 0.19   |
| HGST      | HTS545050B7E660    | 500 GB | 20      | 70    | 0     | 0.19   |
| Seagate   | ST9160310AS        | 160 GB | 41      | 278   | 212   | 0.19   |
| WDC       | WD5000AZLX-60K2TA1 | 500 GB | 4       | 68    | 0     | 0.19   |
| WDC       | WD3200AAJS-60M0A1  | 320 GB | 5       | 837   | 965   | 0.19   |
| Toshiba   | MG06ACA800E        | 8 TB   | 2       | 68    | 0     | 0.19   |
| HGST      | HTS545032A7E380    | 320 GB | 50      | 163   | 571   | 0.19   |
| WDC       | WD2500AAJS-22L7A0  | 250 GB | 3       | 625   | 9     | 0.19   |
| Seagate   | ST91608220AS       | 160 GB | 1       | 135   | 1     | 0.19   |
| Hitachi   | HDT721050SLA360    | 500 GB | 3       | 1119  | 64    | 0.19   |
| WDC       | WD800BB-55JKC0     | 80 GB  | 8       | 588   | 119   | 0.18   |
| WDC       | WD200BB-60CJA0     | 20 GB  | 1       | 1417  | 20    | 0.18   |
| Toshiba   | MK5065GSXN         | 500 GB | 12      | 401   | 612   | 0.18   |
| Seagate   | ST3402111A         | 40 GB  | 2       | 117   | 36    | 0.18   |
| Samsung   | HN-M101XBB         | 1 TB   | 2       | 66    | 0     | 0.18   |
| WDC       | WD20EZAZ-00GGJB0   | 2 TB   | 28      | 66    | 0     | 0.18   |
| Maxtor    | STM3160811AS       | 160 GB | 6       | 687   | 266   | 0.18   |
| HGST      | HCC545050A7E630    | 500 GB | 2       | 66    | 0     | 0.18   |
| Hitachi   | HTS543232L9SA00    | 320 GB | 10      | 423   | 295   | 0.18   |
| WDC       | WD120EDAZ-11F3RA0  | 12 TB  | 5       | 65    | 0     | 0.18   |
| WDC       | WD1600AAJS         | 160 GB | 1       | 65    | 0     | 0.18   |
| WDC       | WD2500AAJS-60VWA1  | 250 GB | 1       | 65    | 0     | 0.18   |
| Hitachi   | HTS421280H9AT00    | 80 GB  | 7       | 600   | 14    | 0.18   |
| Samsung   | HD252KJ            | 250 GB | 11      | 721   | 471   | 0.18   |
| WDC       | WD10SPZX-75Z10T3   | 1 TB   | 14      | 64    | 0     | 0.18   |
| Samsung   | SP1203N            | 120 GB | 10      | 554   | 33    | 0.18   |
| Toshiba   | MK3263GSXN         | 320 GB | 9       | 543   | 22    | 0.18   |
| WDC       | WD3200BUCT-62TWBY0 | 320 GB | 1       | 64    | 0     | 0.18   |
| WDC       | WD3200BUCT-63TWBY0 | 320 GB | 3       | 183   | 4     | 0.18   |
| WDC       | WD20SMZW-11YFCS0   | 2 TB   | 3       | 64    | 0     | 0.18   |
| Seagate   | ST31500341AS       | 1.5 TB | 78      | 809   | 289   | 0.18   |
| Seagate   | ST3750330AS        | 752 GB | 14      | 1124  | 333   | 0.17   |
| WDC       | WD10EZRX-00RKKA0   | 1 TB   | 1       | 1714  | 26    | 0.17   |
| WDC       | WD3200AAJS-08B4A0  | 320 GB | 1       | 695   | 10    | 0.17   |
| Seagate   | ST320VM001-1AD142  | 320 GB | 3       | 63    | 0     | 0.17   |
| WDC       | WD5000LPVX-16V0TT3 | 500 GB | 2       | 62    | 0     | 0.17   |
| WDC       | WD5000BPKT-80PK4T0 | 500 GB | 1       | 563   | 8     | 0.17   |
| WDC       | WD3200AVJS-63TBA0  | 320 GB | 1       | 311   | 4     | 0.17   |
| WDC       | WD10EZRX-22L4HB0   | 1 TB   | 1       | 62    | 0     | 0.17   |
| WDC       | WD5000LPCX-08VHA   | 500 GB | 5       | 61    | 0     | 0.17   |
| WDC       | WD25EZRS-00J99B0   | 2.5 TB | 1       | 2353  | 37    | 0.17   |
| WDC       | WD7500BPVT-35HXZT3 | 752 GB | 1       | 309   | 4     | 0.17   |
| Maxtor    | 4K060H3            | 64 GB  | 1       | 927   | 14    | 0.17   |
| Fujitsu   | MHV2080BH PL       | 80 GB  | 19      | 114   | 3     | 0.17   |
| Seagate   | ST3160215SCE       | 160 GB | 2       | 100   | 2     | 0.17   |
| WDC       | WD120EMFZ-11A6JA0  | 12 TB  | 3       | 60    | 0     | 0.17   |
| HGST      | HTS545025A7E330    | 250 GB | 1       | 60    | 0     | 0.17   |
| Fujitsu   | MHV2100AH PL       | 100 GB | 1       | 423   | 6     | 0.17   |
| Seagate   | ST31000524NS 44... | 1 TB   | 1       | 1693  | 27    | 0.17   |
| Toshiba   | MK6465GSX          | 640 GB | 29      | 646   | 652   | 0.17   |
| Hitachi   | DK23FB-60          | 64 GB  | 1       | 960   | 15    | 0.16   |
| Toshiba   | MK3275GSX          | 320 GB | 19      | 325   | 288   | 0.16   |
| WDC       | WD2500AAJS-98B4A0  | 250 GB | 1       | 540   | 8     | 0.16   |
| IBM/Hi... | IC25N080ATMR04-0   | 80 GB  | 3       | 195   | 19    | 0.16   |
| WDC       | WD10SPZX-60Z10T0   | 1 TB   | 45      | 63    | 1     | 0.16   |
| WDC       | WD1600BB-22GUC0    | 160 GB | 1       | 898   | 14    | 0.16   |
| MediaMax  | WL750GSA6472       | 752 GB | 1       | 59    | 0     | 0.16   |
| Samsung   | HM120JI            | 120 GB | 4       | 327   | 5     | 0.16   |
| Seagate   | ST380021A          | 80 GB  | 11      | 826   | 47    | 0.16   |
| Seagate   | ST9320325ASG       | 320 GB | 1       | 357   | 5     | 0.16   |
| WDC       | WD1600BEVE-00A0HT0 | 160 GB | 1       | 58    | 0     | 0.16   |
| WDC       | WD2000JB-00EVA0    | 200 GB | 1       | 5656  | 96    | 0.16   |
| WDC       | WD3200LPVT-22G33T0 | 320 GB | 1       | 58    | 0     | 0.16   |
| Seagate   | ST980811A          | 80 GB  | 1       | 58    | 0     | 0.16   |
| MediaMax  | WL250GPA872B       | 250 GB | 1       | 58    | 0     | 0.16   |
| Samsung   | HM502JX            | 500 GB | 2       | 57    | 0     | 0.16   |
| Seagate   | ST3640323AS        | 640 GB | 9       | 1059  | 431   | 0.16   |
| Samsung   | SP2014N            | 200 GB | 6       | 359   | 188   | 0.16   |
| WDC       | WD3200BEVT-60A23T0 | 320 GB | 24      | 344   | 364   | 0.16   |
| WDC       | WD20EZRZ-60Z5HB0   | 2 TB   | 2       | 56    | 0     | 0.15   |
| Hitachi   | HTS548040M9AT00    | 40 GB  | 2       | 365   | 10    | 0.15   |
| Hitachi   | HCC543225A7A380    | 250 GB | 1       | 56    | 0     | 0.15   |
| Seagate   | ST3200826A         | 200 GB | 2       | 561   | 8     | 0.15   |
| WDC       | WD1500HLHX-01JJPV0 | 150 GB | 1       | 498   | 8     | 0.15   |
| WDC       | WD3200BPVT-00HXZT1 | 320 GB | 8       | 387   | 272   | 0.15   |
| WDC       | WD5000LPVX-55V0TT3 | 500 GB | 1       | 55    | 0     | 0.15   |
| WDC       | WD10SPZX-80Z10T2   | 1 TB   | 7       | 55    | 0     | 0.15   |
| WDC       | WD10EALX-229BA1    | 1 TB   | 1       | 493   | 8     | 0.15   |
| Samsung   | HM060HC            | 52 GB  | 1       | 272   | 4     | 0.15   |
| Hitachi   | HTS541060G9SA00    | 64 GB  | 3       | 331   | 119   | 0.15   |
| Toshiba   | MK1633GSG          | 160 GB | 5       | 192   | 206   | 0.15   |
| WDC       | WD20SPZX-08UA7     | 2 TB   | 5       | 54    | 0     | 0.15   |
| Hitachi   | HDT725032VLAT80    | 320 GB | 4       | 1102  | 67    | 0.15   |
| WDC       | WD5000AVVS-63H0B1  | 500 GB | 3       | 320   | 6     | 0.15   |
| Samsung   | HM501IX            | 500 GB | 1       | 54    | 0     | 0.15   |
| WDC       | WD10EZEX-35M2NA0   | 1 TB   | 1       | 54    | 0     | 0.15   |
| Toshiba   | DT01ACA050 LENOVO  | 500 GB | 2       | 53    | 0     | 0.15   |
| WDC       | WD1600YS-23SHB0    | 160 GB | 1       | 53    | 0     | 0.15   |
| WDC       | WD10SPSX-00A6WT0   | 1 TB   | 1       | 53    | 0     | 0.15   |
| Toshiba   | MK6008GAH          | 64 GB  | 3       | 480   | 8     | 0.15   |
| Toshiba   | MK1665GSX          | 160 GB | 18      | 214   | 309   | 0.15   |
| Hitachi   | HTS543225L9SA00    | 250 GB | 9       | 425   | 35    | 0.15   |
| Maxtor    | 6L080J4            | 80 GB  | 1       | 319   | 5     | 0.15   |
| HGST      | HUS728T8TALE6L4    | 8 TB   | 2       | 53    | 0     | 0.15   |
| WDC       | WD1600BEVS-00RST0  | 160 GB | 1       | 52    | 0     | 0.15   |
| WDC       | WD2500BEVT-22ZAT0  | 250 GB | 1       | 316   | 5     | 0.14   |
| WDC       | WD2005FBYZ-01YCBB3 | 2 TB   | 2       | 52    | 0     | 0.14   |
| Hitachi   | HTS541040G9SA00    | 40 GB  | 2       | 400   | 9     | 0.14   |
| Hitachi   | HTS424040M9AT00    | 40 GB  | 6       | 456   | 186   | 0.14   |
| WDC       | WD20EURX-25T0FY0   | 2 TB   | 3       | 51    | 0     | 0.14   |
| WDC       | WD10SMZW-59Y0TS0   | 1 TB   | 1       | 51    | 0     | 0.14   |
| WDC       | WD50NMZW-59A8NS1   | 5 TB   | 2       | 51    | 0     | 0.14   |
| Seagate   | ST1000LM022-9XV155 | 1 TB   | 2       | 1349  | 2021  | 0.14   |
| WDC       | WD7500AARS-003BB1  | 752 GB | 2       | 753   | 121   | 0.14   |
| WDC       | WD2500AAJS-00YZCA0 | 250 GB | 4       | 442   | 61    | 0.14   |
| Samsung   | SP1213N            | 120 GB | 4       | 832   | 261   | 0.14   |
| HGST      | HTS541075A7E630    | 752 GB | 9       | 71    | 113   | 0.14   |
| WDC       | WD1600AAJB-56R1A0  | 160 GB | 2       | 152   | 4     | 0.14   |
| Seagate   | ST960812A          | 64 GB  | 1       | 151   | 2     | 0.14   |
| Hitachi   | HTS722080K9A300    | 80 GB  | 4       | 279   | 3     | 0.14   |
| WDC       | WD6400BPVT-75HXZT3 | 640 GB | 1       | 50    | 0     | 0.14   |
| WDC       | WD5000AAKS-60WWPA0 | 500 GB | 9       | 736   | 538   | 0.14   |
| WDC       | WD360GD-00FLA2     | 37 GB  | 4       | 1259  | 29    | 0.14   |
| Seagate   | ST500LM034-2GH17A  | 500 GB | 18      | 49    | 0     | 0.14   |
| Seagate   | ST95000NSSUN500... | 500 GB | 1       | 2980  | 59    | 0.14   |
| Toshiba   | MQ02ABF050H        | 500 GB | 5       | 166   | 405   | 0.14   |
| WDC       | WD6400BPVT-24HXZT1 | 640 GB | 2       | 575   | 509   | 0.14   |
| WDC       | WD400EB-00CPF0     | 40 GB  | 5       | 676   | 61    | 0.14   |
| WDC       | WD3200BEKT-60F3T1  | 320 GB | 10      | 506   | 548   | 0.13   |
| WDC       | WD5003AZEX-00K3CA0 | 500 GB | 2       | 138   | 4     | 0.13   |
| Seagate   | ST3000VX009-2AY10G | 3 TB   | 2       | 49    | 0     | 0.13   |
| Samsung   | HM160HC            | 160 GB | 7       | 216   | 20    | 0.13   |
| Toshiba   | MK1652GSX          | 160 GB | 25      | 442   | 50    | 0.13   |
| Seagate   | ST8000VX004-2M1101 | 8 TB   | 1       | 48    | 0     | 0.13   |
| WDC       | WD10JUCT-61CYNY0   | 1 TB   | 1       | 48    | 0     | 0.13   |
| WDC       | WD5000LPCX-80VHAT0 | 500 GB | 2       | 48    | 0     | 0.13   |
| WDC       | WD600UE-22KVT0     | 64 GB  | 1       | 243   | 4     | 0.13   |
| ExcelStor | J8160              | 34 GB  | 1       | 48    | 0     | 0.13   |
| WDC       | WD2500BPVT-26JJ5T0 | 250 GB | 1       | 48    | 0     | 0.13   |
| Fujitsu   | MHZ2160BJ FFS G2   | 160 GB | 1       | 436   | 8     | 0.13   |
| WDC       | WD5000LPLX-66ZNTT1 | 500 GB | 3       | 53    | 1     | 0.13   |
| Seagate   | ST9808210A         | 80 GB  | 2       | 259   | 19    | 0.13   |
| WDC       | WD7500BMVW-11S5XS0 | 752 GB | 1       | 434   | 8     | 0.13   |
| WDC       | WD400BB-00CAA1     | 40 GB  | 1       | 289   | 5     | 0.13   |
| WDC       | WD15NMVW-11EDZS2   | 1.5 TB | 1       | 48    | 0     | 0.13   |
| WDC       | WD6001FSYZ-01SS7B1 | 6 TB   | 1       | 47    | 0     | 0.13   |
| WDC       | WD10TMVV-11BG7S0   | 1 TB   | 3       | 595   | 10    | 0.13   |
| Hitachi   | HTS421210H9AT00    | 100 GB | 1       | 568   | 11    | 0.13   |
| WDC       | WD10SDRW-11A0XS1   | 1 TB   | 3       | 47    | 0     | 0.13   |
| WDC       | WD3200BEKT-22KA9T0 | 320 GB | 1       | 46    | 0     | 0.13   |
| Hitachi   | HTS541660J9AT00    | 64 GB  | 1       | 184   | 3     | 0.13   |
| WDC       | WD20SPZX-75UA7T1   | 2 TB   | 3       | 45    | 0     | 0.13   |
| WDC       | WD101KFBX-68R56N0  | 10 TB  | 1       | 45    | 0     | 0.13   |
| WDC       | WD2500AAKX-07U6AA1 | 250 GB | 1       | 45    | 0     | 0.13   |
| IBM/Hi... | IC25N060ATMR04-0   | 64 GB  | 8       | 316   | 15    | 0.13   |
| WDC       | WD7500AYPS-01ZKB0  | 752 GB | 1       | 228   | 4     | 0.12   |
| WDC       | WD5000LMVW-11VEDS3 | 500 GB | 4       | 150   | 275   | 0.12   |
| Samsung   | SV4012H            | 40 GB  | 2       | 1504  | 236   | 0.12   |
| WDC       | WD3200AAJS-00V4A0  | 320 GB | 3       | 396   | 9     | 0.12   |
| WDC       | WD1600AAJS-19WAA0  | 160 GB | 1       | 44    | 0     | 0.12   |
| WDC       | WD800BEVS-60RST0   | 80 GB  | 2       | 643   | 291   | 0.12   |
| IBM       | DTLA-307020        | 20 GB  | 1       | 754   | 16    | 0.12   |
| WDC       | WD101EMAZ-11G7DA0  | 10 TB  | 5       | 44    | 0     | 0.12   |
| Hitachi   | HTS541212H9SA00    | 120 GB | 1       | 221   | 4     | 0.12   |
| MARSHAL   | MAL2500SA-T54      | 500 GB | 3       | 247   | 18    | 0.12   |
| Seagate   | ST9250320AS        | 250 GB | 22      | 469   | 265   | 0.12   |
| WDC       | WD5000AAKX-004EA0  | 500 GB | 1       | 392   | 8     | 0.12   |
| Hitachi   | HDP725025GLAT80    | 250 GB | 1       | 216   | 4     | 0.12   |
| WDC       | WD3200BMVS-11F9S0  | 320 GB | 1       | 43    | 0     | 0.12   |
| WDC       | WD50EZRZ-00GZ5B1   | 5 TB   | 1       | 42    | 0     | 0.12   |
| Seagate   | ST2000VX000-9YW164 | 2 TB   | 7       | 700   | 892   | 0.12   |
| Maxtor    | 6B300R0            | 304 GB | 1       | 42    | 0     | 0.12   |
| WDC       | WD1600BMVS-11F9S0  | 160 GB | 1       | 339   | 7     | 0.12   |
| WDC       | WD1503FYYS-02W0B0  | 1.5 TB | 1       | 382   | 8     | 0.12   |
| Maxtor    | 6B160P0            | 163 GB | 1       | 42    | 0     | 0.12   |
| WDC       | WD1600BEVT-26ZCT0  | 160 GB | 2       | 186   | 22    | 0.12   |
| Seagate   | ST500LM030-1RK17D  | 500 GB | 19      | 42    | 0     | 0.12   |
| WDC       | WD10EADS-67M2B0    | 1 TB   | 1       | 1217  | 28    | 0.11   |
| IBM/Hi... | IC25N030ATCS04-0   | 32 GB  | 2       | 134   | 3     | 0.11   |
| WDC       | WD15NMVW-11EDZS6   | 1.5 TB | 1       | 41    | 0     | 0.11   |
| WDC       | WD5000AURX-63UY4Y0 | 500 GB | 1       | 370   | 8     | 0.11   |
| Toshiba   | MK4055GSX          | 400 GB | 3       | 338   | 7     | 0.11   |
| Maxtor    | 7L250R0            | 256 GB | 1       | 40    | 0     | 0.11   |
| Fujitsu   | MHV2200BT PL       | 200 GB | 1       | 325   | 7     | 0.11   |
| WDC       | WD1600BEVE-00UYT0  | 160 GB | 1       | 40    | 0     | 0.11   |
| WDC       | WD3200LPVT-00G33T0 | 320 GB | 2       | 40    | 0     | 0.11   |
| Toshiba   | MK1255GSX H        | 120 GB | 3       | 237   | 282   | 0.11   |
| WDC       | WD6400AAKS-55A7B2  | 640 GB | 1       | 361   | 8     | 0.11   |
| WDC       | WD40EZRX-19SPEB0   | 4 TB   | 1       | 320   | 7     | 0.11   |
| MediaMax  | WL1000GSA3254G     | 1 TB   | 1       | 476   | 11    | 0.11   |
| WDC       | WD40EMRX-82UZ0N0   | 4 TB   | 4       | 60    | 1     | 0.11   |
| Hitachi   | HTS545012B9SA00    | 120 GB | 1       | 197   | 4     | 0.11   |
| Samsung   | HM251JI            | 250 GB | 9       | 296   | 466   | 0.11   |
| WDC       | WD5000LPCX-75VHAT1 | 500 GB | 3       | 39    | 0     | 0.11   |
| WDC       | WD5000AVCS-612DY1  | 500 GB | 1       | 582   | 14    | 0.11   |
| WDC       | WD40EMAZ-11LW3B0   | 4 TB   | 1       | 38    | 0     | 0.11   |
| Samsung   | HM100JC            | 100 GB | 1       | 383   | 9     | 0.10   |
| WDC       | WD1500ADFD-00NLR5  | 150 GB | 1       | 344   | 8     | 0.10   |
| Hitachi   | HTS541020G9SA00    | 20 GB  | 1       | 38    | 0     | 0.10   |
| WDC       | WD153AA-53BAA0     | 16 GB  | 1       | 491   | 12    | 0.10   |
| Hitachi   | HDT721050SLA380    | 500 GB | 1       | 224   | 5     | 0.10   |
| Toshiba   | HDWD240            | 4 TB   | 6       | 37    | 0     | 0.10   |
| WDC       | WD1600BEKT-60V5T1  | 160 GB | 3       | 150   | 4     | 0.10   |
| WDC       | WD10EADS-11M2B1    | 1 TB   | 3       | 867   | 26    | 0.10   |
| WDC       | WD3200BEVS-16VAT0  | 320 GB | 1       | 37    | 0     | 0.10   |
| Toshiba   | HDWJ105            | 500 GB | 11      | 36    | 0     | 0.10   |
| WDC       | WD30NMZW-11A8NS1   | 3 TB   | 1       | 36    | 0     | 0.10   |
| WDC       | WD20EVDS-63T3B0    | 2 TB   | 2       | 330   | 8     | 0.10   |
| WDC       | WD5000BEVT-80A0RT1 | 500 GB | 2       | 284   | 7     | 0.10   |
| Seagate   | ST12000VN0008-2... | 12 TB  | 2       | 36    | 0     | 0.10   |
| WDC       | WD800AAJS-60M0A0   | 80 GB  | 1       | 2215  | 60    | 0.10   |
| Hitachi   | HTS543212L9A300    | 120 GB | 2       | 232   | 72    | 0.10   |
| WDC       | WD10TPVT-00U4RT1   | 1 TB   | 3       | 319   | 155   | 0.10   |
| HGST      | HUS726060ALE611    | 6 TB   | 2       | 36    | 0     | 0.10   |
| WDC       | WD800AAJS-60B4A0   | 80 GB  | 2       | 1529  | 24    | 0.10   |
| Seagate   | ST4000NE001-2MA101 | 4 TB   | 4       | 35    | 0     | 0.10   |
| Maxtor    | 6L120P0            | 122 GB | 2       | 35    | 0     | 0.10   |
| WDC       | WD82PURZ-85TEUY0   | 8 TB   | 3       | 35    | 0     | 0.10   |
| Seagate   | ST3500320AS        | 500 GB | 92      | 817   | 467   | 0.10   |
| WDC       | WD5000LPLX-21ZNTT0 | 500 GB | 3       | 78    | 366   | 0.10   |
| Hitachi   | HTS725025A9A361... | 250 GB | 1       | 34    | 0     | 0.09   |
| WDC       | WD40PURZ-85AKKY0   | 4 TB   | 3       | 42    | 1     | 0.09   |
| WDC       | WD5000BEKT-22KA9T0 | 500 GB | 1       | 302   | 8     | 0.09   |
| Hitachi   | HDS722580VLAT20    | 82 GB  | 3       | 418   | 180   | 0.09   |
| HGST      | HTS725050B7E630    | 500 GB | 2       | 33    | 0     | 0.09   |
| Maxtor    | 2F030L0            | 32 GB  | 1       | 33    | 0     | 0.09   |
| Toshiba   | MK1235GSL          | 120 GB | 1       | 32    | 0     | 0.09   |
| WDC       | WD6400BEVT-24A0RT0 | 640 GB | 1       | 329   | 9     | 0.09   |
| WDC       | WD40EZAZ-00ZGHB0   | 4 TB   | 1       | 32    | 0     | 0.09   |
| Toshiba   | HDWM105            | 500 GB | 1       | 32    | 0     | 0.09   |
| Hitachi   | DK23EA-40          | 40 GB  | 2       | 241   | 236   | 0.09   |
| WDC       | WD5000LMVW-11VEDS6 | 500 GB | 3       | 188   | 24    | 0.09   |
| MaxDig... | MD1TBLSSHD         | 1 TB   | 1       | 288   | 8     | 0.09   |
| WDC       | WD10E              | 1 TB   | 1       | 31    | 0     | 0.09   |
| Toshiba   | MK6476GSX          | 640 GB | 22      | 36    | 323   | 0.09   |
| Maxtor    | STM3500320AS       | 500 GB | 19      | 704   | 312   | 0.09   |
| WDC       | WD10SPSX-08A6W     | 1 TB   | 1       | 31    | 0     | 0.09   |
| WDC       | WD5000LPCX-60VHAT1 | 500 GB | 13      | 39    | 1     | 0.09   |
| Maxtor    | STM3320613AS       | 320 GB | 15      | 1094  | 432   | 0.09   |
| WDC       | WD1600BEVS-00VAT0  | 160 GB | 1       | 31    | 0     | 0.09   |
| WDC       | WD800JB-00FSA0     | 80 GB  | 1       | 1366  | 43    | 0.09   |
| WDC       | WD2500JD-00HBC0    | 250 GB | 1       | 620   | 19    | 0.09   |
| Maxtor    | 2F030J1            | 32 GB  | 1       | 185   | 5     | 0.08   |
| Seagate   | ST14000NE0008-2... | 14 TB  | 6       | 30    | 0     | 0.08   |
| Toshiba   | MK5056GSY          | 500 GB | 3       | 138   | 2     | 0.08   |
| Seagate   | ST9402115AS        | 40 GB  | 2       | 160   | 1042  | 0.08   |
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
| WDC       | WD5000BPVX-00JC3T0 | 500 GB | 2       | 29    | 0     | 0.08   |
| Seagate   | ST9250311CS        | 250 GB | 2       | 1305  | 467   | 0.08   |
| CLOVER    | CN-M500MBB         | 500 GB | 2       | 29    | 0     | 0.08   |
| Seagate   | ST330621A          | 32 GB  | 1       | 319   | 10    | 0.08   |
| Toshiba   | MK5061GSYN         | 500 GB | 20      | 85    | 381   | 0.08   |
| WDC       | WD3200LPVX-00V0TT0 | 320 GB | 1       | 28    | 0     | 0.08   |
| WDC       | WD1200BEVS-07LAT0  | 120 GB | 5       | 382   | 339   | 0.08   |
| MediaMax  | WL120GBSATA        | 120 GB | 1       | 139   | 4     | 0.08   |
| Seagate   | ST33000650NS       | 3 TB   | 3       | 109   | 35    | 0.07   |
| WDC       | WD2000JD-55HBC0    | 200 GB | 1       | 26    | 0     | 0.07   |
| WDC       | WD3200AAJS-00VWA1  | 320 GB | 1       | 708   | 26    | 0.07   |
| Hitachi   | HTS421260H9AT00    | 64 GB  | 4       | 462   | 19    | 0.07   |
| WDC       | WD2500JB-55EVA0    | 250 GB | 1       | 77    | 2     | 0.07   |
| Samsung   | HM322IX            | 320 GB | 1       | 25    | 0     | 0.07   |
| WDC       | WD1200JB-00CRA1    | 120 GB | 1       | 871   | 34    | 0.07   |
| WDC       | WD6003FRYZ-01F0DB0 | 6 TB   | 4       | 24    | 0     | 0.07   |
| WDC       | WD2500AAJS-52B4A0  | 250 GB | 2       | 942   | 45    | 0.07   |
| Toshiba   | MK3261GSYN         | 320 GB | 14      | 45    | 106   | 0.07   |
| Seagate   | ST3500620AS        | 500 GB | 7       | 737   | 782   | 0.07   |
| WDC       | WD400VE-75HDT1     | 40 GB  | 1       | 23    | 0     | 0.06   |
| WDC       | WUH721414ALE6L4    | 14 TB  | 2       | 23    | 0     | 0.06   |
| Toshiba   | MK6032GAX          | 64 GB  | 1       | 23    | 0     | 0.06   |
| Toshiba   | MK3265GSX H        | 320 GB | 2       | 44    | 15    | 0.06   |
| Seagate   | ST4000VX000-2AG166 | 4 TB   | 1       | 23    | 0     | 0.06   |
| Toshiba   | MK6465GSXW         | 640 GB | 1       | 552   | 23    | 0.06   |
| Toshiba   | MK2529GSG          | 250 GB | 2       | 313   | 1127  | 0.06   |
| Magnet... | MD02500-BQDW-RO    | 250 GB | 1       | 22    | 0     | 0.06   |
| Hitachi   | HTS543216L9SA02    | 160 GB | 3       | 134   | 11    | 0.06   |
| HGST      | HUS726T4TALE6L4    | 4 TB   | 4       | 27    | 381   | 0.06   |
| WDC       | WD2000JS-60NCB1    | 200 GB | 2       | 192   | 6     | 0.06   |
| WDC       | WD5000LPSX-08A6W   | 500 GB | 2       | 22    | 0     | 0.06   |
| CLOVER    | CN-M750MBB         | 752 GB | 1       | 22    | 0     | 0.06   |
| Samsung   | HM641JX            | 640 GB | 1       | 22    | 0     | 0.06   |
| Toshiba   | MK1032GAX          | 100 GB | 2       | 108   | 4     | 0.06   |
| WDC       | WD3200AVVS-63L2B0  | 320 GB | 5       | 325   | 69    | 0.06   |
| WDC       | WD10TPVT-00HT5T1   | 1 TB   | 1       | 219   | 9     | 0.06   |
| WDC       | WD3200BEKX-22B7WT0 | 320 GB | 1       | 21    | 0     | 0.06   |
| WDC       | WD1600BEKT-00PVMT0 | 160 GB | 1       | 21    | 0     | 0.06   |
| Seagate   | ST3300831A         | 304 GB | 1       | 347   | 15    | 0.06   |
| Seagate   | ST3000VM002-1ET166 | 3 TB   | 2       | 599   | 1011  | 0.06   |
| Seagate   | ST3250824SCE       | 250 GB | 1       | 21    | 0     | 0.06   |
| WDC       | WD2500BEVT-60A23T0 | 250 GB | 4       | 245   | 23    | 0.06   |
| Seagate   | ST10000NE0008-2... | 10 TB  | 3       | 21    | 0     | 0.06   |
| Maxtor    | STM3160613AS       | 160 GB | 1       | 41    | 1     | 0.06   |
| Fujitsu   | MHT2040AT          | 40 GB  | 1       | 166   | 7     | 0.06   |
| WDC       | WD20SDRW-34VUUS1   | 2 TB   | 1       | 20    | 0     | 0.06   |
| Maxtor    | 6Y120M0            | 122 GB | 2       | 25    | 4     | 0.06   |
| WDC       | WD400BB-22DEA0     | 40 GB  | 1       | 831   | 39    | 0.06   |
| Toshiba   | MQ02ABF050H-SSH... | 500 GB | 2       | 20    | 0     | 0.06   |
| Seagate   | ST9500424AS        | 500 GB | 2       | 120   | 505   | 0.06   |
| WDC       | WD2000BB-00GUC0    | 200 GB | 1       | 637   | 30    | 0.06   |
| Maxtor    | 6B200M0            | 200 GB | 3       | 26    | 13    | 0.06   |
| WDC       | WD40EMAZ-11ZRJB0   | 4 TB   | 2       | 20    | 0     | 0.06   |
| Toshiba   | MK3276GSX          | 320 GB | 29      | 26    | 298   | 0.06   |
| WDC       | WD10SMZW-34Y0TS0   | 1 TB   | 1       | 20    | 0     | 0.06   |
| WDC       | WD5000BPVT-75A1YT0 | 500 GB | 1       | 20    | 0     | 0.06   |
| WDC       | WD2500BPVT-00ZEST0 | 250 GB | 3       | 136   | 74    | 0.06   |
| WDC       | WD140EFFX-68VBXN0  | 14 TB  | 11      | 20    | 0     | 0.06   |
| Fujitsu   | MHV2060AH          | 64 GB  | 1       | 968   | 47    | 0.06   |
| MediaMax  | WL640GSA6472B      | 647 GB | 1       | 20    | 0     | 0.05   |
| WDC       | WD2500LPCX-24VHAT0 | 250 GB | 2       | 55    | 5     | 0.05   |
| IBM       | DARA-206000        | 6 GB   | 1       | 118   | 5     | 0.05   |
| Samsung   | HM160HI            | 160 GB | 76      | 344   | 342   | 0.05   |
| Seagate   | ST9100822A         | 100 GB | 2       | 627   | 31    | 0.05   |
| IBM/Hi... | IC25N040ATMR04-0   | 40 GB  | 2       | 628   | 181   | 0.05   |
| Maxtor    | 6L080M0            | 80 GB  | 6       | 26    | 170   | 0.05   |
| Maxtor    | 6L200P0            | 208 GB | 4       | 22    | 7     | 0.05   |
| Samsung   | HS12UHE            | 120 GB | 1       | 136   | 6     | 0.05   |
| Maxtor    | STM3300622A        | 304 GB | 1       | 173   | 8     | 0.05   |
| Maxtor    | 6B200P0            | 208 GB | 4       | 35    | 4     | 0.05   |
| WDC       | WD200EB-75CPF0     | 20 GB  | 2       | 402   | 20    | 0.05   |
| Maxtor    | 2F040J0            | 40 GB  | 1       | 19    | 0     | 0.05   |
| WDC       | WD1600JD-00GBB0    | 160 GB | 1       | 727   | 37    | 0.05   |
| WDC       | WD15EADS-22P8B0    | 1.5 TB | 2       | 388   | 511   | 0.05   |
| Seagate   | ST8000VN0002-1Z... | 8 TB   | 1       | 1048  | 54    | 0.05   |
| Seagate   | ST31000340AS       | 1 TB   | 6       | 1025  | 364   | 0.05   |
| Seagate   | ST9250421ASG       | 250 GB | 1       | 453   | 23    | 0.05   |
| WDC       | WD1001FAES-75W7A0  | 1 TB   | 3       | 1442  | 442   | 0.05   |
| Hitachi   | HTS541640J9SA00    | 40 GB  | 2       | 309   | 387   | 0.05   |
| Toshiba   | MK8052GSX          | 80 GB  | 5       | 151   | 37    | 0.05   |
| Samsung   | HM320JI            | 320 GB | 10      | 328   | 470   | 0.05   |
| WDC       | WD5000LUCT-62RC2Y0 | 500 GB | 1       | 18    | 0     | 0.05   |
| Hitachi   | HCP725050GLAT80    | 500 GB | 1       | 240   | 12    | 0.05   |
| WDC       | WD7500BPVT-75HXZT1 | 752 GB | 1       | 547   | 29    | 0.05   |
| Toshiba   | MQ01ABU050W        | 500 GB | 1       | 54    | 2     | 0.05   |
| WDC       | WD6003FFBX-68MU3N0 | 6 TB   | 1       | 18    | 0     | 0.05   |
| WDC       | WD10SDRW-11A0XS0   | 1 TB   | 5       | 40    | 406   | 0.05   |
| WDC       | WD800JD-75LSA0     | 80 GB  | 1       | 616   | 33    | 0.05   |
| WDC       | WD1600BB-55GUA0    | 160 GB | 2       | 661   | 134   | 0.05   |
| WDC       | WD20SMRW-59YNDS0   | 2 TB   | 2       | 17    | 0     | 0.05   |
| Apple     | HDD HTS547550A9... | 500 GB | 5       | 174   | 19    | 0.05   |
| Toshiba   | MK2576GSX          | 250 GB | 4       | 121   | 2     | 0.05   |
| WDC       | WD5000LPVX-16V0TT0 | 500 GB | 1       | 71    | 3     | 0.05   |
| Maxtor    | 6L200M0            | 208 GB | 5       | 28    | 14    | 0.05   |
| Quantum   | FIREBALLlct15 10   | 10 GB  | 1       | 105   | 5     | 0.05   |
| Hitachi   | HUA723030ALA641    | 3 TB   | 1       | 17    | 0     | 0.05   |
| WDC       | WD1600JS-55MHB0    | 160 GB | 1       | 761   | 43    | 0.05   |
| Seagate   | ST31000333AS       | 1 TB   | 27      | 738   | 411   | 0.05   |
| WDC       | WD40NDZW-11A8JS0   | 4 TB   | 2       | 17    | 0     | 0.05   |
| Maxtor    | 6L160P0            | 163 GB | 5       | 32    | 5     | 0.05   |
| Hitachi   | HDP725032GLAT80    | 320 GB | 1       | 943   | 55    | 0.05   |
| WDC       | WD40NDZW-11A8JS1   | 4 TB   | 2       | 16    | 0     | 0.05   |
| Seagate   | ST3320310CS        | 320 GB | 4       | 863   | 50    | 0.05   |
| Samsung   | HN-M250MBB         | 250 GB | 1       | 292   | 17    | 0.04   |
| Samsung   | HM060HI            | 64 GB  | 3       | 542   | 697   | 0.04   |
| Seagate   | ST10000VN0008-2... | 10 TB  | 2       | 16    | 0     | 0.04   |
| Samsung   | HM080HI            | 80 GB  | 3       | 525   | 289   | 0.04   |
| WDC       | WD3200BEKT-75PVMT0 | 320 GB | 2       | 217   | 18    | 0.04   |
| Seagate   | ST500LX025-1U71... | 500 GB | 1       | 15    | 0     | 0.04   |
| WDC       | WD800BB-88JHC0     | 80 GB  | 1       | 1625  | 101   | 0.04   |
| IBM/Hi... | IC35L060AVVA07-0   | 64 GB  | 1       | 678   | 42    | 0.04   |
| WDC       | WD140EDFZ-11A0VA0  | 14 TB  | 14      | 15    | 0     | 0.04   |
| HGST      | HUS726020ALA610    | 2 TB   | 2       | 15    | 0     | 0.04   |
| Toshiba   | MK5055GSXF         | 500 GB | 2       | 231   | 87    | 0.04   |
| HGST      | HUS722T1TALA604    | 1 TB   | 3       | 15    | 0     | 0.04   |
| WDC       | WD4000ABYS-01TNA0  | 400 GB | 1       | 688   | 44    | 0.04   |
| WDC       | WD40NMZW-59GX6S1   | 4 TB   | 1       | 15    | 0     | 0.04   |
| Toshiba   | MK5059GSX          | 500 GB | 2       | 693   | 61    | 0.04   |
| Hitachi   | HUS724040ALE641    | 4 TB   | 1       | 15    | 0     | 0.04   |
| Maxtor    | 6L250S0            | 250 GB | 3       | 28    | 8     | 0.04   |
| Samsung   | SP1253N            | 120 GB | 1       | 286   | 18    | 0.04   |
| MediaMax  | WL250GSA872        | 250 GB | 1       | 15    | 0     | 0.04   |
| Hitachi   | HDS7250SASUN500G   | 500 GB | 1       | 14    | 0     | 0.04   |
| Hitachi   | HTS723225L9A360    | 250 GB | 3       | 322   | 1301  | 0.04   |
| WDC       | WD5000AVDS-73U7B1  | 500 GB | 3       | 126   | 5     | 0.04   |
| Samsung   | HD160HJ            | 160 GB | 22      | 746   | 775   | 0.04   |
| Seagate   | OOS500G            | 500 GB | 1       | 14    | 0     | 0.04   |
| Seagate   | ST9120310AS        | 120 GB | 1       | 14    | 0     | 0.04   |
| Seagate   | ST31000533CS       | 1 TB   | 1       | 1038  | 72    | 0.04   |
| Hitachi   | HTS725025A9A364    | 250 GB | 19      | 424   | 1093  | 0.04   |
| WDC       | WD205BA            | 20 GB  | 1       | 296   | 20    | 0.04   |
| Toshiba   | MK1656GSYF         | 160 GB | 1       | 96    | 6     | 0.04   |
| Seagate   | STM980215AS        | 80 GB  | 1       | 13    | 0     | 0.04   |
| Seagate   | ST310212A          | 10 GB  | 1       | 380   | 27    | 0.04   |
| WDC       | WD10SMRW-11Y43S0   | 1 TB   | 4       | 13    | 0     | 0.04   |
| WDC       | WD5000AADS-98S9B1  | 500 GB | 1       | 120   | 8     | 0.04   |
| Maxtor    | 6L100M0            | 100 GB | 1       | 13    | 0     | 0.04   |
| Seagate   | ST320LT012-9WS14C  | 320 GB | 56      | 278   | 1053  | 0.04   |
| Toshiba   | MK3265GSXV         | 320 GB | 2       | 166   | 136   | 0.04   |
| WDC       | WD30EZRZ-60Z5HB0   | 3 TB   | 1       | 13    | 0     | 0.04   |
| Seagate   | ST500LT012-9WS142  | 500 GB | 226     | 344   | 1055  | 0.04   |
| Maxtor    | STM3160813AS       | 160 GB | 5       | 780   | 476   | 0.04   |
| WDC       | WD10TMVV-11TK7S1   | 1 TB   | 3       | 212   | 30    | 0.04   |
| WDC       | WD20SDZW-11JJ8S1   | 2 TB   | 1       | 12    | 0     | 0.04   |
| Maxtor    | 6L160M0            | 160 GB | 8       | 23    | 270   | 0.04   |
| WDC       | WD800BB-00CAA1     | 80 GB  | 1       | 800   | 61    | 0.04   |
| WDC       | WD10EACS-22D6B1    | 1 TB   | 1       | 12    | 0     | 0.04   |
| Toshiba   | MK2565GSXV         | 250 GB | 3       | 197   | 24    | 0.03   |
| WDC       | WD3200AAJS-00RYA0  | 320 GB | 2       | 1320  | 143   | 0.03   |
| Fujitsu   | MPG3204AT E        | 20 GB  | 1       | 138   | 10    | 0.03   |
| Seagate   | ST3250412CS        | 250 GB | 1       | 12    | 0     | 0.03   |
| Maxtor    | 2F040L0            | 40 GB  | 4       | 23    | 5     | 0.03   |
| WDC       | WD1602ABKS-18N8A0  | 160 GB | 1       | 111   | 8     | 0.03   |
| WDC       | WD121KFBX-68EF5N0  | 12 TB  | 1       | 12    | 0     | 0.03   |
| WDC       | WD5000LPCX-80VHAT1 | 500 GB | 3       | 31    | 650   | 0.03   |
| WDC       | WD2500BPVT-80ZEST0 | 250 GB | 1       | 106   | 8     | 0.03   |
| Maxtor    | 6L080L0            | 82 GB  | 6       | 21    | 13    | 0.03   |
| WDC       | WD7500LPCX-22HWST0 | 752 GB | 1       | 129   | 10    | 0.03   |
| MaxDig... | MD3000GSA3257DVR 0 | 3 TB   | 1       | 11    | 0     | 0.03   |
| WDC       | WD800BB-00CAA0     | 80 GB  | 1       | 414   | 35    | 0.03   |
| Samsung   | HS030GB            | 32 GB  | 1       | 11    | 0     | 0.03   |
| WDC       | WD80EDAZ-11TA3A0   | 8 TB   | 3       | 11    | 0     | 0.03   |
| Seagate   | ST9320421AS        | 320 GB | 5       | 456   | 51    | 0.03   |
| Toshiba   | MQ01ABD100V        | 1 TB   | 2       | 255   | 21    | 0.03   |
| Hitachi   | HDS722525VLAT80    | 250 GB | 1       | 11    | 0     | 0.03   |
| WDC       | WSH722020ALE6L0    | 20 TB  | 12      | 11    | 0     | 0.03   |
| Maxtor    | STM3320820A        | 320 GB | 1       | 11    | 0     | 0.03   |
| MediaMax  | WL2000GSA6454G     | 2 TB   | 1       | 33    | 2     | 0.03   |
| Hitachi   | HDS721025CLA382... | 160 GB | 1       | 2614  | 237   | 0.03   |
| WDC       | WD5000AAKS-19V0A0  | 500 GB | 1       | 1131  | 103   | 0.03   |
| Seagate   | ST1750LM000 HN-... | 1.7 TB | 1       | 10    | 0     | 0.03   |
| Toshiba   | MG08ACA16TE        | 16 TB  | 2       | 10    | 0     | 0.03   |
| WDC       | WD20SPZX-60UA7T0   | 2 TB   | 3       | 10    | 0     | 0.03   |
| Hitachi   | DK23CA-20          | 20 GB  | 1       | 93    | 8     | 0.03   |
| WDC       | WD400ABJS-23TEA0   | 40 GB  | 1       | 10    | 0     | 0.03   |
| WDC       | WD5000BEVT-55A0RT0 | 500 GB | 1       | 110   | 10    | 0.03   |
| Seagate   | ST1000DL004 HD1... | 1 TB   | 1       | 9     | 0     | 0.03   |
| WDC       | WD180PURZ-85AFFY0  | 18 TB  | 2       | 9     | 0     | 0.03   |
| Toshiba   | MK2016GAP          | 20 GB  | 1       | 349   | 36    | 0.03   |
| Maxtor    | 6L120M0            | 122 GB | 3       | 28    | 15    | 0.03   |
| Samsung   | HD322IJ            | 320 GB | 1       | 469   | 51    | 0.02   |
| WDC       | WD800JD-75JNC0     | 80 GB  | 2       | 858   | 355   | 0.02   |
| Maxtor    | 4K040H2            | 34 GB  | 1       | 298   | 33    | 0.02   |
| Toshiba   | MK1214GAH          | 120 GB | 3       | 60    | 142   | 0.02   |
| WDC       | WD10EZRX-00A3KB0   | 1 TB   | 1       | 8     | 0     | 0.02   |
| WDC       | WD10SDZM-59ZKVS0   | 1 TB   | 1       | 8     | 0     | 0.02   |
| WDC       | WD3200BEVT-80A0RT1 | 320 GB | 2       | 1035  | 140   | 0.02   |
| Maxtor    | 6E040L0            | 40 GB  | 13      | 30    | 29    | 0.02   |
| Hitachi   | HTS548080M9AT00    | 80 GB  | 1       | 136   | 16    | 0.02   |
| ExcelStor | J9250              | 250 GB | 1       | 1349  | 167   | 0.02   |
| MediaMax  | WL250GLSA6410000   | 250 GB | 2       | 36    | 4     | 0.02   |
| LENOVO    | WD1004FBYZ-23YC... | 1 TB   | 2       | 7     | 0     | 0.02   |
| WDC       | WD5000AZLX-00ZR6A0 | 500 GB | 1       | 7     | 0     | 0.02   |
| Maxtor    | 2F030J0            | 32 GB  | 3       | 32    | 96    | 0.02   |
| Hitachi   | HCC543232A7A380    | 320 GB | 1       | 30    | 3     | 0.02   |
| Maxtor    | 6Y120L0            | 122 GB | 7       | 28    | 15    | 0.02   |
| Maxtor    | 6Y060L2            | 64 GB  | 1       | 542   | 71    | 0.02   |
| Maxtor    | 6K040L0            | 41 GB  | 1       | 29    | 3     | 0.02   |
| Maxtor    | 7B300S0            | 304 GB | 1       | 244   | 32    | 0.02   |
| Hitachi   | DK23EA-20B         | 17 GB  | 1       | 183   | 24    | 0.02   |
| WDC       | WD2000JS-00NCB1    | 200 GB | 1       | 537   | 73    | 0.02   |
| Hitachi   | HTS722016K9SA00    | 160 GB | 1       | 591   | 81    | 0.02   |
| WDC       | WD20EFAX-68B2RN1   | 2 TB   | 1       | 7     | 0     | 0.02   |
| Seagate   | ST730212DE         | 32 GB  | 1       | 7     | 0     | 0.02   |
| Toshiba   | HDWD260            | 6 TB   | 1       | 7     | 0     | 0.02   |
| Samsung   | HD254GJ            | 250 GB | 1       | 710   | 100   | 0.02   |
| Seagate   | ST4000NM0115-1Y... | 4 TB   | 3       | 7     | 0     | 0.02   |
| Fujitsu   | MHV2120BH PL       | 120 GB | 11      | 20    | 3     | 0.02   |
| Maxtor    | 6E030L0            | 32 GB  | 5       | 15    | 19    | 0.02   |
| WDC       | WD2500AAJS-41RYA0  | 250 GB | 1       | 76    | 10    | 0.02   |
| Seagate   | ST8000VX0022-2E... | 8 TB   | 1       | 893   | 130   | 0.02   |
| Maxtor    | 6L300S0            | 304 GB | 7       | 18    | 263   | 0.02   |
| WDC       | WD40EZAZ-00SF3B0   | 4 TB   | 5       | 6     | 0     | 0.02   |
| Maxtor    | 6L200S0            | 208 GB | 2       | 20    | 21    | 0.02   |
| Samsung   | SP1614N            | 160 GB | 1       | 690   | 106   | 0.02   |
| WDC       | WD360ADFD-00NLR4   | 37 GB  | 1       | 499   | 77    | 0.02   |
| HPE       | MB004000GWWQH      | 4 TB   | 1       | 6     | 0     | 0.02   |
| HGST      | HTS725050A7E635... | 500 GB | 1       | 451   | 72    | 0.02   |
| HGST      | QC-FT-D H20GB-5... | 20 GB  | 1       | 6     | 0     | 0.02   |
| Samsung   | HM100JI            | 100 GB | 1       | 827   | 140   | 0.02   |
| Hitachi   | HTS541612J9AT00    | 120 GB | 1       | 116   | 19    | 0.02   |
| Seagate   | ST3500320SV        | 500 GB | 1       | 45    | 7     | 0.02   |
| MediaMax  | WL1500GSA3272      | 1.5 TB | 1       | 2210  | 391   | 0.02   |
| Toshiba   | MK1656GSY          | 160 GB | 4       | 96    | 7     | 0.02   |
| WDC       | WD10SPCX-24HWST0   | 1 TB   | 1       | 2080  | 373   | 0.02   |
| Toshiba   | MK1655GSXF         | 160 GB | 1       | 855   | 157   | 0.01   |
| Maxtor    | 85400D5            | 5 GB   | 1       | 5613  | 1044  | 0.01   |
| Seagate   | ST2000NE001-2M5101 | 2 TB   | 1       | 5     | 0     | 0.01   |
| WDC       | WD15SMZW-11JW8S0   | 1.5 TB | 1       | 5     | 0     | 0.01   |
| Seagate   | ST1000LM002-9VQ14L | 1 TB   | 1       | 25    | 4     | 0.01   |
| Samsung   | HM121HI            | 120 GB | 10      | 430   | 1611  | 0.01   |
| WDC       | WD1200AAJS-00VTA0  | 120 GB | 1       | 995   | 203   | 0.01   |
| Hitachi   | HTS723232L9A360    | 320 GB | 5       | 1148  | 974   | 0.01   |
| WDC       | WD5000LPVX-28V0TT1 | 500 GB | 1       | 134   | 27    | 0.01   |
| Seagate   | ST3500820AS        | 500 GB | 6       | 298   | 58    | 0.01   |
| Hitachi   | HTE721060G9AT00    | 64 GB  | 1       | 4     | 0     | 0.01   |
| Maxtor    | 6L300R0            | 304 GB | 2       | 8     | 10    | 0.01   |
| Fujitsu   | MHT2080AH          | 80 GB  | 1       | 292   | 64    | 0.01   |
| WDC       | WD40EFAX-68JH4N1   | 4 TB   | 5       | 4     | 0     | 0.01   |
| Toshiba   | MK8050GAC          | 80 GB  | 1       | 878   | 197   | 0.01   |
| Maxtor    | 6L080P0            | 82 GB  | 3       | 11    | 10    | 0.01   |
| Maxtor    | 4R060J0            | 64 GB  | 1       | 25    | 5     | 0.01   |
| WDC       | WD20EZAZ-00L9GB0   | 2 TB   | 3       | 4     | 0     | 0.01   |
| Fujitsu   | MHZ2160BJ G1       | 160 GB | 1       | 4     | 0     | 0.01   |
| Seagate   | ST9250421AS        | 250 GB | 1       | 539   | 136   | 0.01   |
| WDC       | WD2500BEKT-66F3T2  | 250 GB | 1       | 193   | 50    | 0.01   |
| WDC       | WD6003FZBX-00GXAB0 | 6 TB   | 1       | 3     | 0     | 0.01   |
| Seagate   | ST1000NX0313       | 1 TB   | 1       | 1357  | 370   | 0.01   |
| Toshiba   | MK6028GAL          | 64 GB  | 1       | 3     | 0     | 0.01   |
| Seagate   | ST3750630AS        | 752 GB | 4       | 697   | 791   | 0.01   |
| Seagate   | ST3250310SV        | 250 GB | 1       | 287   | 79    | 0.01   |
| WDC       | WD5000AVJS-63TRA0  | 500 GB | 1       | 2013  | 578   | 0.01   |
| Fujitsu   | MJA2320BH G1       | 320 GB | 1       | 800   | 230   | 0.01   |
| Maxtor    | 6Y160P0            | 163 GB | 6       | 21    | 121   | 0.01   |
| Hitachi   | HTS541640J9AT00    | 40 GB  | 1       | 283   | 82    | 0.01   |
| HGST      | HTS725050A7E635    | 500 GB | 2       | 490   | 557   | 0.01   |
| Maxtor    | 6B250S0            | 250 GB | 2       | 20    | 471   | 0.01   |
| WDC       | WD10EADS-00R6B0    | 1 TB   | 1       | 1856  | 560   | 0.01   |
| Fujitsu   | MPE3136AT          | 16 GB  | 1       | 794   | 240   | 0.01   |
| Apple     | HDD HTS547575A9... | 752 GB | 1       | 506   | 153   | 0.01   |
| IBM/Hi... | IC35L060AVER07-0   | 64 GB  | 1       | 997   | 304   | 0.01   |
| Maxtor    | 6Y080P0            | 82 GB  | 7       | 16    | 7     | 0.01   |
| Maxtor    | 6E020L0            | 21 GB  | 1       | 22    | 6     | 0.01   |
| Seagate   | ST6000NE0021-2E... | 6 TB   | 1       | 3     | 0     | 0.01   |
| WDC       | WD2004FBYZ-01YCBB0 | 2 TB   | 1       | 12    | 3     | 0.01   |
| Maxtor    | 6Y080M0            | 80 GB  | 11      | 30    | 92    | 0.01   |
| WDC       | TP00250GB          | 250 GB | 1       | 1073  | 351   | 0.01   |
| Seagate   | ST3320820A         | 320 GB | 1       | 641   | 210   | 0.01   |
| Maxtor    | 6B160M0            | 163 GB | 1       | 3     | 0     | 0.01   |
| Seagate   | ST8000NM0105       | 8 TB   | 2       | 2     | 0     | 0.01   |
| WDC       | WD800UE-22HCT0     | 80 GB  | 2       | 568   | 272   | 0.01   |
| Toshiba   | MAL2040SA-T54L     | 40 GB  | 1       | 2     | 0     | 0.01   |
| WDC       | WD10SPSX-75A6WT0   | 1 TB   | 1       | 2     | 0     | 0.01   |
| Maxtor    | 6Y120P0            | 122 GB | 3       | 21    | 28    | 0.01   |
| Seagate   | ST3160316CS        | 160 GB | 2       | 107   | 20    | 0.01   |
| WDC       | WD1200BEVS-75LAT0  | 118 GB | 1       | 1008  | 378   | 0.01   |
| Seagate   | ST500LM020-1G1162  | 500 GB | 3       | 2     | 0     | 0.01   |
| Maxtor    | 7L250S0            | 250 GB | 1       | 7     | 2     | 0.01   |
| Samsung   | SV0802N            | 80 GB  | 1       | 554   | 215   | 0.01   |
| Seagate   | ST3160310CS        | 160 GB | 3       | 225   | 273   | 0.01   |
| WDC       | WD10SPSX-22A6WT0   | 1 TB   | 2       | 2     | 0     | 0.01   |
| Seagate   | ST3160212SCE       | 160 GB | 1       | 2510  | 1028  | 0.01   |
| WDC       | WD3200AADS-00S9B0  | 320 GB | 1       | 26    | 10    | 0.01   |
| WDC       | WD10SPSX-60A6WT0   | 1 TB   | 2       | 2     | 0     | 0.01   |
| Maxtor    | 6Y200P0            | 208 GB | 2       | 20    | 9     | 0.01   |
| Seagate   | ST3160812AS Q      | 160 GB | 1       | 1049  | 480   | 0.01   |
| Maxtor    | 6Y080L0            | 80 GB  | 40      | 21    | 276   | 0.01   |
| Seagate   | OOS1000G128M       | 1 TB   | 1       | 39    | 18    | 0.01   |
| MARSHAL   | MAL2020SA 80       | 20 GB  | 1       | 4     | 1     | 0.01   |
| Hitachi   | HDS722516VLAT20    | 164 GB | 1       | 2242  | 1102  | 0.01   |
| WDC       | WD10SDRW-34A0XS0   | 1 TB   | 1       | 1     | 0     | 0.01   |
| WDC       | WD6400AAKS-00E4A0  | 640 GB | 1       | 1016  | 521   | 0.01   |
| WDC       | WD10EURX-63UHWY0   | 1 TB   | 1       | 644   | 338   | 0.01   |
| WDC       | WD4000AAKS-22TMA0  | 400 GB | 1       | 820   | 431   | 0.01   |
| Seagate   | ST9320423ASG       | 320 GB | 1       | 270   | 145   | 0.01   |
| Samsung   | HM160JI            | 160 GB | 6       | 304   | 1043  | 0.01   |
| WDC       | WD20EARS-19MVWB0   | 2 TB   | 1       | 713   | 392   | 0.00   |
| Toshiba   | MK2533GSG          | 250 GB | 1       | 1671  | 948   | 0.00   |
| Hitachi   | HUA5C3020ALA640    | 2 TB   | 1       | 1045  | 595   | 0.00   |
| WDC       | WD1600BEKT-75PVMT0 | 160 GB | 1       | 1003  | 580   | 0.00   |
| Seagate   | ST5000AS0011-1L... | 5 TB   | 1       | 1743  | 1015  | 0.00   |
| CLOVER    | CD155UI            | 1.5 TB | 1       | 1     | 0     | 0.00   |
| IBM/Hi... | IC35L120AVVA07-0   | 128 GB | 1       | 918   | 552   | 0.00   |
| WDC       | WD140PURZ-85GG1Y0  | 14 TB  | 4       | 1     | 0     | 0.00   |
| Maxtor    | 2F020J0            | 21 GB  | 2       | 21    | 45    | 0.00   |
| WDC       | WD7501AAES-60Z2A0  | 752 GB | 1       | 1058  | 666   | 0.00   |
| Toshiba   | MK5061GSY          | 500 GB | 3       | 4     | 35    | 0.00   |
| Samsung   | HD251KJ            | 250 GB | 1       | 1539  | 1019  | 0.00   |
| Maxtor    | 2B020H1            | 20 GB  | 11      | 23    | 156   | 0.00   |
| Seagate   | ST3120023AS        | 120 GB | 1       | 152   | 101   | 0.00   |
| WDC       | WD3200AAKX-00U6AA0 | 320 GB | 1       | 83    | 56    | 0.00   |
| WDC       | WD5000LPZX-60Z10T0 | 500 GB | 1       | 1     | 0     | 0.00   |
| Hitachi   | HUA722010CLA330... | 1 TB   | 1       | 161   | 112   | 0.00   |
| WDC       | WD2500JD-98GBB0    | 250 GB | 1       | 875   | 628   | 0.00   |
| Maxtor    | 4R160L0            | 163 GB | 1       | 5     | 3     | 0.00   |
| Seagate   | ST8000NC0002-1X... | 8 TB   | 1       | 107   | 82    | 0.00   |
| WDC       | WD15EADS-11P8B1    | 1.5 TB | 2       | 908   | 934   | 0.00   |
| Seagate   | ST3400820AS        | 400 GB | 1       | 1276  | 1004  | 0.00   |
| WDC       | WD3200LPCX-60VHAT0 | 320 GB | 1       | 1     | 0     | 0.00   |
| WDC       | WD1200             | 120 GB | 1       | 11    | 8     | 0.00   |
| Toshiba   | MK4026GAX          | 40 GB  | 1       | 191   | 157   | 0.00   |
| Hitachi   | HCS5C1050DLE630    | 500 GB | 1       | 885   | 737   | 0.00   |
| Toshiba   | MK7559GSM          | 752 GB | 1       | 1015  | 847   | 0.00   |
| WDC       | WD400BB-00CAA0     | 40 GB  | 1       | 194   | 163   | 0.00   |
| WDC       | WD10JUCX-63WPNY0   | 1 TB   | 1       | 87    | 73    | 0.00   |
| Hitachi   | HTS723225A7A364    | 250 GB | 1       | 1210  | 1023  | 0.00   |
| Hitachi   | HTS723216L9A360    | 160 GB | 6       | 516   | 1478  | 0.00   |
| WDC       | WD7500AACS-00ZJB0  | 752 GB | 1       | 1106  | 1007  | 0.00   |
| Maxtor    | 4D040H2            | 41 GB  | 4       | 16    | 188   | 0.00   |
| WDC       | WD60EZAZ-00SF3B0   | 6 TB   | 1       | 1     | 0     | 0.00   |
| Seagate   | ST9320327AS        | 320 GB | 1       | 725   | 705   | 0.00   |
| WDC       | WD3200JS-63PDB1    | 320 GB | 1       | 343   | 342   | 0.00   |
| WDC       | WD2003FYPS-27W9B0  | 2 TB   | 1       | 523   | 529   | 0.00   |
| Maxtor    | 6Y060L0            | 64 GB  | 4       | 24    | 63    | 0.00   |
| WDC       | WD1005FBYZ-01YCBB3 | 1 TB   | 2       | 0     | 0     | 0.00   |
| Fujitsu   | MHV2160BT          | 160 GB | 1       | 483   | 535   | 0.00   |
| Seagate   | ST250LT021-1AF14C  | 250 GB | 1       | 1021  | 1169  | 0.00   |
| Hitachi   | HTS725032A9A365    | 320 GB | 2       | 859   | 1023  | 0.00   |
| WDC       | RAT015VQHB-DSG2D7  | 1.5 TB | 1       | 0     | 0     | 0.00   |
| WDC       | RFT030VQHR-GTK4D   | 3 TB   | 1       | 0     | 0     | 0.00   |
| Maxtor    | 4R120L0            | 122 GB | 3       | 30    | 39    | 0.00   |
| HGST      | TPH00100500GB 0... | 500 GB | 1       | 8     | 10    | 0.00   |
| HP        | GB1000EAFJL        | 1 TB   | 1       | 2402  | 3024  | 0.00   |
| WDC       | WD800BEVT-26ZCT0   | 80 GB  | 1       | 0     | 0     | 0.00   |
| Maxtor    | 4G120J6            | 122 GB | 2       | 20    | 218   | 0.00   |
| Toshiba   | MK3256GSY          | 320 GB | 4       | 5     | 282   | 0.00   |
| Maxtor    | STM3750330AS       | 752 GB | 1       | 995   | 1293  | 0.00   |
| MediaMax  | WL400GSA6454G      | 400 GB | 1       | 0     | 0     | 0.00   |
| WDC       | WD3200LPCX-22VHAT0 | 320 GB | 1       | 0     | 0     | 0.00   |
| Seagate   | ST500LX012-1LM1... | 500 GB | 1       | 358   | 480   | 0.00   |
| Fujitsu   | MHV2200BT          | 200 GB | 1       | 382   | 518   | 0.00   |
| Apple     | HDD HUA722010CL... | 1 TB   | 1       | 83    | 113   | 0.00   |
| Maxtor    | 7Y250M0            | 250 GB | 2       | 25    | 38    | 0.00   |
| Seagate   | ST3320620SV        | 320 GB | 1       | 564   | 835   | 0.00   |
| Seagate   | ST500LT015-9WU142  | 500 GB | 2       | 708   | 1108  | 0.00   |
| Seagate   | ST3320410SV        | 320 GB | 1       | 685   | 1110  | 0.00   |
| Seagate   | ST500DM009-1BD142  | 500 GB | 1       | 0     | 0     | 0.00   |
| Maxtor    | 4D060H3            | 64 GB  | 1       | 18    | 31    | 0.00   |
| Maxtor    | 6Y160M0            | 160 GB | 6       | 20    | 195   | 0.00   |
| Hitachi   | HUA722010CLA630    | 1 TB   | 1       | 0     | 0     | 0.00   |
| WDC       | WD15EARS-19MVWB0   | 1.5 TB | 1       | 696   | 1306  | 0.00   |
| Hitachi   | HTS723212L9A360    | 120 GB | 1       | 535   | 1012  | 0.00   |
| Hitachi   | HTS723232A7A365    | 320 GB | 1       | 1130  | 2203  | 0.00   |
| Seagate   | ST10000NM001G-2... | 10 TB  | 4       | 0     | 0     | 0.00   |
| MediaMax  | WL6000GSA6457      | 6 TB   | 1       | 637   | 1372  | 0.00   |
| WDC       | WD15EURS-63S48Y0   | 1.5 TB | 1       | 11    | 26    | 0.00   |
| WDC       | WD2500BB-22RDA0    | 250 GB | 1       | 655   | 1524  | 0.00   |
| Seagate   | ST3802110ACE       | 80 GB  | 1       | 1203  | 3052  | 0.00   |
| Hitachi   | HDP725040GLA380    | 400 GB | 1       | 215   | 554   | 0.00   |
| Samsung   | HM500LX            | 500 GB | 2       | 133   | 293   | 0.00   |
| Seagate   | ST2000NP0011       | 2 TB   | 1       | 1143  | 3103  | 0.00   |
| Seagate   | ST3250311SV        | 250 GB | 1       | 363   | 1010  | 0.00   |
| Seagate   | ST3750640A         | 752 GB | 1       | 732   | 2049  | 0.00   |
| Seagate   | ST3500321CS        | 500 GB | 1       | 48    | 137   | 0.00   |
| MARSHAL   | MAL2500SA-T54L     | 500 GB | 1       | 90    | 262   | 0.00   |
| WDC       | WD3200L22X-00JVPT0 | 320 GB | 1       | 0     | 0     | 0.00   |
| Maxtor    | 7L300S0            | 304 GB | 3       | 13    | 40    | 0.00   |
| WDC       | WD2500BEKT-60F3T1  | 250 GB | 1       | 533   | 1607  | 0.00   |
| WDC       | WD5000BEVT-60ZAT0  | 500 GB | 1       | 381   | 1160  | 0.00   |
| Seagate   | ST250LT012-9WS141  | 250 GB | 4       | 337   | 1077  | 0.00   |
| Fujitsu   | MHZ2120BH G2       | 120 GB | 3       | 322   | 1027  | 0.00   |
| Samsung   | HD402LJ            | 400 GB | 1       | 315   | 1018  | 0.00   |
| Seagate   | ST980817AS         | 80 GB  | 1       | 310   | 1009  | 0.00   |
| WDC       | WD2500AAKS-60L9A0  | 250 GB | 1       | 282   | 937   | 0.00   |
| WDC       | WD1600AAJS-56WAA0  | 160 GB | 1       | 299   | 1021  | 0.00   |
| WDC       | WD20EZRX-00SPEB0   | 2 TB   | 1       | 574   | 2072  | 0.00   |
| Seagate   | ST320LT000-9VL142  | 320 GB | 1       | 278   | 1009  | 0.00   |
| Hitachi   | HTS542580K9A300    | 80 GB  | 2       | 267   | 1012  | 0.00   |
| Seagate   | ST9320312AS        | 320 GB | 2       | 264   | 1108  | 0.00   |
| Samsung   | SV2011H            | 20 GB  | 1       | 0     | 3     | 0.00   |
| WDC       | WD2500AAJS-55B4A0  | 250 GB | 1       | 476   | 2020  | 0.00   |
| Toshiba   | MK2555GSX H        | 250 GB | 1       | 428   | 1908  | 0.00   |
| WDC       | WD800 AAJS-00PSA0  | 80 GB  | 1       | 97    | 459   | 0.00   |
| Fujitsu   | MHT2060BH          | 64 GB  | 1       | 407   | 2048  | 0.00   |
| China     | Generic S050 Ha... | 500 GB | 1       | 245   | 1377  | 0.00   |
| Maxtor    | 6B120P0            | 122 GB | 1       | 0     | 0     | 0.00   |
| Seagate   | ST4000NC000-1FR168 | 4 TB   | 1       | 0     | 0     | 0.00   |
| WDC       | WD2005FBYZ-01YCBB1 | 2 TB   | 1       | 0     | 0     | 0.00   |
| Samsung   | HM320JX            | 320 GB | 1       | 37    | 331   | 0.00   |
| Seagate   | ST980829A          | 80 GB  | 1       | 222   | 2022  | 0.00   |
| Seagate   | MB0500EAMZD        | 500 GB | 1       | 94    | 857   | 0.00   |
| Maxtor    | 7L300R0            | 304 GB | 1       | 11    | 116   | 0.00   |
| Toshiba   | MK8025GAL          | 80 GB  | 1       | 78    | 1017  | 0.00   |
| Seagate   | ST3500630NS Q      | 500 GB | 1       | 201   | 3060  | 0.00   |
| Samsung   | HS122JC            | 120 GB | 1       | 188   | 3047  | 0.00   |
| Maxtor    | 6L250R0            | 250 GB | 1       | 2     | 45    | 0.00   |
| Maxtor    | 53073H6            | 32 GB  | 1       | 121   | 2068  | 0.00   |
| WDC       | WD20EADS-22R6B0    | 2 TB   | 1       | 105   | 1848  | 0.00   |
| Hitachi   | HTS548060M9AT00    | 64 GB  | 1       | 35    | 655   | 0.00   |
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

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG       | Family                 | Models | Samples | Days  | Err   | MTBF   |
|-----------|------------------------|--------|---------|-------|-------|--------|
| Samsung   | SpinPoint V20400       | 1      | 1       | 5713  | 0     | 15.65  |
| HP        | Seagate Barracuda 7... | 1      | 2       | 3447  | 0     | 9.44   |
| Hitachi   | Sun Original           | 2      | 11      | 2609  | 0     | 7.15   |
| Seagate   | Barracuda ES+          | 2      | 2       | 2199  | 0     | 6.03   |
| Toshiba   | 3.5" HDD MK.002TSKB    | 2      | 2       | 1775  | 0     | 4.87   |
| Seagate   | Momentus Xt            | 1      | 1       | 1697  | 0     | 4.65   |
| Samsung   | SpinPoint PL40         | 1      | 2       | 3755  | 9     | 4.62   |
| Seagate   | SpinPoint F4 EG (AF)   | 1      | 3       | 1617  | 0     | 4.43   |
| Hitachi   | CinemaStar C5K500      | 1      | 1       | 1573  | 0     | 4.31   |
| Seagate   | Constellation.2 (SATA) | 2      | 25      | 1693  | 1     | 4.30   |
| HPE       | WDC Enterprise         | 1      | 1       | 1526  | 0     | 4.18   |
| Quantum   | Unknown                | 1      | 1       | 1486  | 0     | 4.07   |
| WDC       | Caviar WDxxxAA         | 2      | 2       | 1697  | 6     | 4.03   |
| Seagate   | Exos 7E2               | 5      | 26      | 1452  | 15    | 3.84   |
| Seagate   | Laptop Thin            | 1      | 1       | 1394  | 0     | 3.82   |
| Hitachi   | Deskstar 7K4000        | 1      | 4       | 1544  | 341   | 3.74   |
| Maxtor    | DiamondMax 8s          | 1      | 1       | 2684  | 1     | 3.68   |
| WDC       | RE2                    | 7      | 17      | 1547  | 36    | 3.52   |
| HGST      | Ultrastar 7K4000       | 6      | 88      | 1265  | 24    | 3.40   |
| Hitachi   | Deskstar 7K2000        | 2      | 34      | 1722  | 104   | 3.39   |
| Hitachi   | Ultrastar A7K2000      | 9      | 53      | 1583  | 25    | 3.34   |
| WDC       | RE4-GP                 | 5      | 16      | 1642  | 60    | 3.27   |
| Seagate   | Archive HDD            | 3      | 97      | 1381  | 63    | 3.25   |
| Hitachi   | Ultrastar A7K1000      | 4      | 10      | 1889  | 198   | 3.23   |
| WDC       | Raptor X               | 1      | 1       | 1164  | 0     | 3.19   |
| Toshiba   | 1.8" HDD MK..17GSG     | 1      | 1       | 1162  | 0     | 3.18   |
| WDC       | WDC Enterprise         | 1      | 1       | 1134  | 0     | 3.11   |
| WDC       | RE3                    | 19     | 82      | 1447  | 4     | 3.02   |
| Seagate   | U5                     | 4      | 5       | 1159  | 2     | 3.02   |
| Hitachi   | Deskstar 7K3000        | 6      | 83      | 1243  | 52    | 2.93   |
| Apple     | Travelstar 7K750       | 1      | 3       | 1036  | 0     | 2.84   |
| Hitachi   | Ultrastar 7K3000       | 4      | 72      | 1131  | 34    | 2.83   |
| HP        | Unknown                | 2      | 2       | 1030  | 0     | 2.82   |
| Hitachi   | CinemaStar P7K500      | 4      | 6       | 1282  | 3     | 2.81   |
| WDC       | Purple NV              | 1      | 1       | 1023  | 0     | 2.80   |
| Hitachi   | CinemaStar 5K320       | 2      | 4       | 1079  | 1     | 2.77   |
| Toshiba   | 3.5" HDD               | 1      | 1       | 1008  | 0     | 2.76   |
| WDC       | Se                     | 6      | 15      | 1166  | 1     | 2.74   |
| HGST      | MegaScale 4000         | 2      | 15      | 979   | 0     | 2.68   |
| Seagate   | Constellation.2        | 3      | 3       | 958   | 0     | 2.63   |
| Samsung   | SpinPoint F4 EG (AF)   | 2      | 55      | 1201  | 125   | 2.62   |
| Toshiba   | 2.5" HDD MQ01UBB       | 1      | 4       | 952   | 0     | 2.61   |
| HGST      | Deskstar NAS           | 8      | 55      | 977   | 18    | 2.61   |
| Hitachi   | Unknown                | 2      | 3       | 962   | 2     | 2.46   |
| Seagate   | Enterprise NAS HDD     | 2      | 4       | 896   | 0     | 2.46   |
| WDC       | Caviar SE16            | 5      | 41      | 1141  | 16    | 2.44   |
| Seagate   | Desktop HDD.15         | 4      | 134     | 1002  | 67    | 2.42   |
| Hitachi   | Deskstar 5K4000        | 1      | 2       | 879   | 0     | 2.41   |
| Toshiba   | 2.5" HDD MQ01ABF..H    | 1      | 2       | 873   | 0     | 2.39   |
| Hitachi   | Deskstar 5K3000        | 5      | 34      | 1103  | 20    | 2.37   |
| HP        | Proliant HardDrive     | 10     | 17      | 1266  | 22    | 2.32   |
| Quantum   | Fireball Plus AS       | 2      | 2       | 845   | 0     | 2.32   |
| Hitachi   | CinemaStar C5K750      | 1      | 1       | 844   | 0     | 2.31   |
| HP        | RE3                    | 1      | 2       | 814   | 0     | 2.23   |
| WDC       | VelociRaptor           | 29     | 79      | 968   | 17    | 2.22   |
| HGST      | CinemaStar Z7K500      | 1      | 1       | 810   | 0     | 2.22   |
| HP        | 250GB SATA disk VB0... | 1      | 15      | 1182  | 4     | 2.21   |
| Seagate   | Desktop HDD            | 1      | 2       | 801   | 0     | 2.20   |
| WDC       | Caviar Black           | 46     | 490     | 1080  | 40    | 2.19   |
| Seagate   | Barracuda XT           | 3      | 23      | 1081  | 168   | 2.19   |
| Hitachi   | Deskstar 7K500         | 2      | 9       | 1578  | 9     | 2.18   |
| Toshiba   | 3.5" DT01ABA Deskto... | 3      | 18      | 798   | 2     | 2.08   |
| Hitachi   | Deskstar T7K500        | 8      | 69      | 1220  | 61    | 2.08   |
| Seagate   | NAS HDD                | 8      | 46      | 842   | 47    | 2.07   |
| Seagate   | Barracuda 7200.7       | 1      | 3       | 1192  | 70    | 2.05   |
| Samsung   | SpinPoint F3 RE        | 1      | 3       | 2260  | 41    | 2.00   |
| Maxtor    | DiamondMax Plus D740X  | 3      | 5       | 1106  | 3     | 1.93   |
| WDC       | RE                     | 27     | 72      | 1049  | 31    | 1.90   |
| Hitachi   | Ultrastar 7K4000       | 4      | 19      | 716   | 66    | 1.90   |
| Hitachi   | Deskstar 5K1000        | 3      | 27      | 885   | 60    | 1.90   |
| Samsung   | SpinPoint F1 RE        | 2      | 3       | 824   | 34    | 1.90   |
| Seagate   | Barracuda 7200.8       | 9      | 48      | 1294  | 83    | 1.90   |
| HP        | Constellation ES.3     | 1      | 2       | 691   | 0     | 1.89   |
| WDC       | Raptor                 | 14     | 21      | 1235  | 11    | 1.88   |
| WDC       | RE4                    | 22     | 137     | 973   | 32    | 1.86   |
| Toshiba   | 2.5" HDD MQ01ABB       | 1      | 12      | 782   | 70    | 1.85   |
| Seagate   | Barracuda ES           | 8      | 44      | 1283  | 468   | 1.83   |
| Toshiba   | 3.5" MD04ACA Enterp... | 2      | 15      | 803   | 269   | 1.79   |
| WDC       | Caviar SE              | 156    | 552     | 941   | 30    | 1.78   |
| Samsung   | SpinPoint T133         | 5      | 25      | 985   | 142   | 1.77   |
| WDC       | Red                    | 29     | 717     | 776   | 9     | 1.76   |
| Samsung   | SpinPoint F3           | 5      | 290     | 872   | 38    | 1.75   |
| WDC       | Caviar Green           | 156    | 1805    | 972   | 75    | 1.74   |
| Hitachi   | Deskstar 7K1000        | 3      | 17      | 1168  | 19    | 1.74   |
| Toshiba   | 3.5" HDD DT01ABA..V    | 4      | 4       | 633   | 0     | 1.74   |
| Maxtor    | MaXLine III (SATA/300) | 2      | 4       | 1049  | 238   | 1.73   |
| Hitachi   | Deskstar 7K80          | 6      | 81      | 867   | 31    | 1.71   |
| Seagate   | Constellation ES (S... | 4      | 34      | 1198  | 165   | 1.71   |
| HGST      | Deskstar 7K4000        | 2      | 8       | 1035  | 253   | 1.68   |
| Seagate   | Barracuda Green (AF)   | 4      | 193     | 955   | 215   | 1.67   |
| Toshiba   | 3.5" MG03ACAxxx(Y) ... | 4      | 21      | 774   | 3     | 1.67   |
| Hitachi   | Deskstar 7K1000.B      | 11     | 124     | 1051  | 57    | 1.66   |
| Seagate   | Constellation ES.2 ... | 4      | 17      | 1129  | 92    | 1.65   |
| Seagate   | Constellation ES.3     | 6      | 62      | 684   | 94    | 1.64   |
| Seagate   | U9                     | 2      | 6       | 595   | 0     | 1.63   |
| WDC       | Black                  | 24     | 252     | 663   | 15    | 1.62   |
| Apple     | SpinPoint              | 1      | 1       | 589   | 0     | 1.61   |
| Toshiba   | 2.5" HDD MQ01ABC       | 1      | 1       | 574   | 0     | 1.57   |
| Hitachi   | CinemaStar 7K500       | 1      | 1       | 573   | 0     | 1.57   |
| Seagate   | DB35.3                 | 6      | 15      | 659   | 155   | 1.55   |
| Hitachi   | CinemaStar 5K1000      | 4      | 7       | 638   | 1     | 1.54   |
| Seagate   | Momentus 5400.7        | 2      | 12      | 807   | 327   | 1.53   |
| Hitachi   | Deskstar E7K500        | 2      | 2       | 559   | 0     | 1.53   |
| Fujitsu   | MPA..MPG               | 5      | 6       | 711   | 42    | 1.53   |
| Maxtor    | MaXLine Pro 500        | 1      | 4       | 646   | 1     | 1.53   |
| Samsung   | SpinPoint F2 EG        | 3      | 168     | 961   | 247   | 1.51   |
| Seagate   | Barracuda 7200.10      | 35     | 1372    | 922   | 268   | 1.51   |
| Hitachi   | Deskstar 7K1000.C      | 16     | 554     | 823   | 70    | 1.51   |
| Seagate   | Video 3.5 HDD          | 10     | 45      | 646   | 191   | 1.48   |
| Samsung   | SpinPoint              | 7      | 10      | 670   | 60    | 1.47   |
| WDC       | Green                  | 7      | 133     | 584   | 1     | 1.44   |
| Hitachi   | Deskstar T7K250        | 5      | 40      | 1033  | 77    | 1.43   |
| Hitachi   | Deskstar 7K250         | 7      | 15      | 965   | 247   | 1.42   |
| Seagate   | Exos 7E8               | 4      | 9       | 595   | 1     | 1.42   |
| Maxtor    | DiamondMax 10 (SATA... | 6      | 36      | 770   | 31    | 1.40   |
| Samsung   | SpinPoint F1 DT        | 12     | 357     | 1016  | 201   | 1.38   |
| Samsung   | SpinPoint F3 EG        | 4      | 43      | 687   | 98    | 1.38   |
| Toshiba   | 2.5" HDD MK..32GSX     | 1      | 6       | 521   | 1     | 1.37   |
| WDC       | Red Pro                | 11     | 21      | 500   | 0     | 1.37   |
| Seagate   | Barracuda 7200.7 an... | 19     | 618     | 864   | 87    | 1.36   |
| Seagate   | Pipeline HD 5900.2     | 9      | 103     | 756   | 135   | 1.35   |
| Seagate   | Constellation ES (S... | 3      | 40      | 1302  | 42    | 1.34   |
| Seagate   | Enterprise Capacity... | 12     | 64      | 486   | 0     | 1.33   |
| Apple     | Travelstar 5K1000      | 4      | 30      | 603   | 160   | 1.33   |
| Apple     | Barracuda              | 1      | 16      | 484   | 0     | 1.33   |
| WDC       | RE2-GP                 | 3      | 3       | 544   | 2     | 1.33   |
| WDC       | Scorpio Blue EIDE      | 7      | 11      | 483   | 0     | 1.33   |
| Seagate   | Barracuda 5400.1       | 1      | 5       | 835   | 33    | 1.32   |
| HGST      | Travelstar 5K1500      | 2      | 5       | 810   | 212   | 1.30   |
| Hitachi   | Deskstar P7K500        | 10     | 184     | 962   | 77    | 1.28   |
| Seagate   | Constellation ES.2     | 1      | 1       | 467   | 0     | 1.28   |
| Samsung   | SpinPoint VL40         | 1      | 1       | 2328  | 4     | 1.28   |
| Seagate   | Barracuda Pro          | 3      | 9       | 465   | 0     | 1.28   |
| Hitachi   | Deskstar 7K160         | 7      | 174     | 924   | 107   | 1.27   |
| WDC       | AV                     | 28     | 58      | 733   | 63    | 1.26   |
| Seagate   | SpinPoint F4           | 2      | 7       | 704   | 63    | 1.26   |
| WDC       | Caviar                 | 66     | 176     | 759   | 40    | 1.25   |
| WDC       | AV-GP                  | 42     | 136     | 700   | 46    | 1.24   |
| WDC       | Caviar Blue            | 326    | 3957    | 666   | 44    | 1.23   |
| WDC       | Black SSHD             | 1      | 9       | 448   | 0     | 1.23   |
| Seagate   | Desktop SSHD           | 9      | 113     | 622   | 83    | 1.22   |
| Apple     | Momentus               | 1      | 3       | 887   | 2     | 1.21   |
| Seagate   | Barracuda 7200.9       | 35     | 524     | 808   | 400   | 1.21   |
| Seagate   | Barracuda 7200.14 (AF) | 27     | 2540    | 606   | 119   | 1.20   |
| Seagate   | SpinPoint M9T          | 3      | 60      | 498   | 4     | 1.19   |
| Toshiba   | 2.5" HDD MQ01UBD       | 3      | 38      | 531   | 155   | 1.18   |
| Seagate   | Barracuda 7200.12      | 16     | 1541    | 768   | 176   | 1.17   |
| Seagate   | Barracuda SpinPoint F3 | 2      | 58      | 543   | 7     | 1.17   |
| Seagate   | UX                     | 1      | 8       | 856   | 11    | 1.16   |
| Seagate   | Surveillance           | 6      | 17      | 424   | 0     | 1.16   |
| HGST      | Unknown                | 3      | 3       | 424   | 4     | 1.16   |
| Fujitsu   | MHZ BJ                 | 3      | 3       | 549   | 3     | 1.15   |
| WDC       | Green Mobile           | 3      | 7       | 470   | 6     | 1.15   |
| Toshiba   | MG07ACA Enterprise ... | 1      | 2       | 414   | 0     | 1.14   |
| HGST      | Ultrastar 7K2          | 3      | 9       | 414   | 0     | 1.14   |
| HGST      | CinemaStar Z5K500      | 3      | 6       | 473   | 1     | 1.13   |
| Seagate   | SV35                   | 12     | 97      | 503   | 130   | 1.10   |
| HGST      | Ultrastar He10         | 4      | 16      | 424   | 1     | 1.10   |
| Quantum   | Fireball lct20         | 1      | 1       | 400   | 0     | 1.10   |
| Samsung   | SpinPoint F4           | 2      | 44      | 636   | 103   | 1.07   |
| Seagate   | Barracuda ES.2         | 4      | 46      | 1044  | 355   | 1.07   |
| Toshiba   | 3.5" HDD DT01ACA       | 4      | 1025    | 445   | 31    | 1.06   |
| Toshiba   | 2.5" HDD MK..59GSXP... | 1      | 4       | 450   | 7     | 1.05   |
| HGST      | Ultrastar He8          | 3      | 14      | 376   | 0     | 1.03   |
| Seagate   | SpinPoint M7E          | 3      | 17      | 384   | 1     | 1.02   |
| Apple     | HGST Travelstar Z5K500 | 1      | 27      | 396   | 9     | 1.02   |
| Fujitsu   | MHW BH                 | 9      | 63      | 541   | 80    | 1.02   |
| Seagate   | Momentus               | 4      | 10      | 611   | 152   | 1.01   |
| Seagate   | Momentus XT (AF)       | 1      | 17      | 429   | 109   | 1.01   |
| WDC       | Caviar Blue EIDE       | 18     | 106     | 630   | 60    | 1.00   |
| WDC       | Elements / My Passport | 57     | 324     | 462   | 29    | 1.00   |
| Toshiba   | Toshiba Enterprise     | 3      | 13      | 364   | 0     | 1.00   |
| Toshiba   | 3.5" HDD N300          | 1      | 14      | 388   | 1     | 0.99   |
| Toshiba   | S300                   | 2      | 2       | 354   | 0     | 0.97   |
| Toshiba   | 2.5" HDD MK..61GSY     | 1      | 1       | 354   | 0     | 0.97   |
| Seagate   | IronWolf               | 15     | 181     | 399   | 9     | 0.97   |
| Maxtor    | DiamondMax 21          | 16     | 233     | 727   | 382   | 0.97   |
| HGST      | Ultrastar 7K6000       | 11     | 29      | 361   | 20    | 0.96   |
| Seagate   | BarraCuda              | 1      | 1       | 346   | 0     | 0.95   |
| Seagate   | Video 2.5              | 5      | 24      | 337   | 0     | 0.92   |
| ExcelStor | Jupiter                | 8      | 19      | 771   | 13    | 0.92   |
| Seagate   | Constellation CS       | 3      | 12      | 594   | 333   | 0.92   |
| Seagate   | Unknown                | 4      | 4       | 897   | 1     | 0.91   |
| Seagate   | Barracuda              | 2      | 8       | 325   | 0     | 0.89   |
| Toshiba   | 3.5" MG04ACA Enterp... | 3      | 11      | 323   | 1     | 0.88   |
| Seagate   | Laptop HDD             | 3      | 5       | 602   | 443   | 0.87   |
| Seagate   | Constellation ES       | 4      | 5       | 1716  | 829   | 0.87   |
| Hitachi   | Travelstar 7K320       | 13     | 32      | 696   | 584   | 0.85   |
| WDC       | Blue UltraSlim         | 2      | 2       | 309   | 0     | 0.85   |
| MediaMax  | WL5000                 | 1      | 1       | 308   | 0     | 0.85   |
| Samsung   | SpinPoint P80 SD       | 7      | 234     | 803   | 394   | 0.84   |
| Seagate   | Maxtor DiamondMax 23   | 4      | 68      | 718   | 262   | 0.84   |
| Seagate   | BarraCuda Pro          | 4      | 8       | 305   | 1     | 0.83   |
| HGST      | Travelstar 7K1000      | 4      | 363     | 364   | 142   | 0.82   |
| Samsung   | SpinPoint M7E (AF)     | 4      | 157     | 466   | 77    | 0.82   |
| Seagate   | Barracuda LP           | 4      | 87      | 820   | 354   | 0.82   |
| Seagate   | SpinPoint D8X          | 1      | 3       | 424   | 269   | 0.82   |
| Toshiba   | Toshiba Surveillance   | 2      | 2       | 744   | 3     | 0.82   |
| Seagate   | Barracuda ATA V        | 3      | 4       | 1510  | 35    | 0.82   |
| Toshiba   | Unknown                | 3      | 3       | 305   | 1     | 0.80   |
| Toshiba   | X300                   | 5      | 62      | 327   | 45    | 0.80   |
| WDC       | Scorpio Blue           | 230    | 2267    | 433   | 65    | 0.80   |
| Samsung   | SpinPoint T166         | 8      | 207     | 925   | 446   | 0.80   |
| HGST      | Ultrastar DC HC520 ... | 3      | 10      | 288   | 0     | 0.79   |
| Hitachi   | Travelstar 5K500.B     | 16     | 483     | 519   | 159   | 0.78   |
| Seagate   | SV35.5                 | 2      | 4       | 668   | 267   | 0.78   |
| WDC       | Scorpio Black          | 53     | 243     | 476   | 96    | 0.78   |
| Fujitsu   | MHY BH                 | 5      | 78      | 517   | 174   | 0.78   |
| Seagate   | Barracuda 3.5          | 9      | 785     | 308   | 24    | 0.78   |
| Seagate   | Momentus 7200.2        | 7      | 22      | 555   | 200   | 0.78   |
| Seagate   | IronWolf Pro           | 11     | 33      | 381   | 4     | 0.78   |
| Apple     | MK..65GSXF             | 1      | 3       | 430   | 134   | 0.77   |
| Fujitsu   | MHZ BH                 | 10     | 106     | 506   | 299   | 0.77   |
| Seagate   | FireCuda 3.5           | 2      | 59      | 306   | 22    | 0.76   |
| Seagate   | Ultra Mobile SSHD      | 2      | 5       | 374   | 97    | 0.75   |
| Samsung   | SpinPoint M7           | 3      | 151     | 401   | 36    | 0.75   |
| Seagate   | Momentus 7200.3        | 8      | 24      | 596   | 67    | 0.75   |
| WDC       | HGST Ultrastar He10    | 5      | 90      | 272   | 0     | 0.75   |
| WDC       | Gold                   | 16     | 47      | 286   | 1     | 0.75   |
| Apple     | Seagate Samsung Spi... | 1      | 1       | 271   | 0     | 0.74   |
| Seagate   | Pipeline HD Mini       | 4      | 16      | 688   | 172   | 0.74   |
| Seagate   | SpinPoint M8 (AF)      | 6      | 1103    | 376   | 43    | 0.72   |
| MediaMax  | WL1000                 | 5      | 5       | 593   | 4     | 0.72   |
| Seagate   | Barracuda V            | 1      | 1       | 259   | 0     | 0.71   |
| Samsung   | SpinPoint S166         | 3      | 77      | 807   | 464   | 0.71   |
| Toshiba   | 2.5" HDD MQ03ABB       | 2      | 3       | 258   | 0     | 0.71   |
| Hitachi   | Travelstar 5K750       | 3      | 358     | 495   | 394   | 0.70   |
| Maxtor    | DiamondMax 20          | 6      | 22      | 619   | 372   | 0.70   |
| WDC       | Blue                   | 52     | 592     | 280   | 14    | 0.70   |
| Samsung   | SpinPoint S250         | 2      | 62      | 821   | 614   | 0.70   |
| HP        | 500GB SATA disk MM0... | 1      | 13      | 1725  | 49    | 0.70   |
| Hitachi   | Deskstar E7K1000       | 2      | 5       | 1462  | 40    | 0.69   |
| Toshiba   | 2.5" HDD MQ03UBB       | 2      | 16      | 270   | 3     | 0.69   |
| Hitachi   | Deskstar 7K1000.D      | 2      | 92      | 665   | 543   | 0.68   |
| Toshiba   | 2.5" HDD MQ04UBF       | 1      | 23      | 258   | 1     | 0.68   |
| Maxtor    | DiamondMax 17          | 2      | 11      | 379   | 114   | 0.67   |
| Seagate   | Momentus 7200.5        | 4      | 113     | 511   | 106   | 0.66   |
| Toshiba   | 2.5" HDD               | 18     | 65      | 469   | 68    | 0.66   |
| Fujitsu   | MHW BJ                 | 3      | 4       | 325   | 33    | 0.66   |
| Seagate   | Skyhawk                | 9      | 32      | 269   | 5     | 0.66   |
| Hitachi   | Travelstar 7K100       | 5      | 16      | 514   | 25    | 0.66   |
| Apple     | Barracuda 7200.12      | 1      | 1       | 236   | 0     | 0.65   |
| Seagate   | LD25.2                 | 2      | 2       | 383   | 1     | 0.65   |
| Seagate   | Barracuda ATA IV       | 4      | 57      | 668   | 30    | 0.64   |
| IBM/Hi... | Deskstar GXP-180       | 4      | 6       | 620   | 5     | 0.64   |
| Seagate   | Momentus XT            | 1      | 20      | 721   | 116   | 0.64   |
| Seagate   | Momentus 7200.4        | 9      | 250     | 545   | 369   | 0.63   |
| Fujitsu   | MJA BH                 | 8      | 42      | 504   | 187   | 0.63   |
| WDC       | Blue SSHD              | 2      | 2       | 230   | 0     | 0.63   |
| Fujitsu   | MHV                    | 26     | 102     | 380   | 37    | 0.63   |
| Toshiba   | 2.5" HDD MK..58GSX     | 1      | 4       | 418   | 3     | 0.63   |
| Hitachi   | Travelstar Z7K500      | 2      | 14      | 425   | 676   | 0.62   |
| HGST      | Travelstar Z7K500      | 8      | 204     | 389   | 237   | 0.62   |
| Seagate   | Momentus 5400.2        | 13     | 55      | 432   | 373   | 0.62   |
| HGST      | Travelstar 5K1000      | 5      | 288     | 387   | 391   | 0.61   |
| Toshiba   | 2.5" HDD MQ01ABD       | 8      | 808     | 342   | 136   | 0.61   |
| WDC       | Purple                 | 19     | 95      | 293   | 24    | 0.61   |
| Hitachi   | Travelstar 4K120       | 4      | 14      | 785   | 31    | 0.61   |
| Toshiba   | 2.5" HDD MQ02ABD..H    | 1      | 22      | 341   | 97    | 0.61   |
| Seagate   | Constellation (SATA)   | 1      | 3       | 1402  | 99    | 0.60   |
| Seagate   | Exos X14               | 3      | 4       | 220   | 0     | 0.60   |
| Hitachi   | Travelstar 7K750       | 2      | 40      | 548   | 374   | 0.60   |
| Hitachi   | Travelstar 7K200       | 8      | 27      | 585   | 129   | 0.60   |
| Hitachi   | CinemaStar 7K1000.B    | 2      | 4       | 218   | 0     | 0.60   |
| Seagate   | Laptop SSHD            | 8      | 237     | 350   | 105   | 0.60   |
| Seagate   | SpinPoint M9TU (USB)   | 1      | 5       | 217   | 0     | 0.60   |
| Seagate   | U6                     | 3      | 20      | 566   | 34    | 0.59   |
| Samsung   | SpinPoint M8 (AF)      | 5      | 77      | 398   | 84    | 0.59   |
| Seagate   | Laptop Thin SSHD       | 1      | 3       | 212   | 0     | 0.58   |
| Seagate   | Momentus 5400.7 (AF)   | 2      | 17      | 547   | 372   | 0.58   |
| WDC       | Blue Mobile            | 123    | 2022    | 249   | 18    | 0.58   |
| HGST      | Edurastar              | 1      | 1       | 211   | 0     | 0.58   |
| Toshiba   | 2.5" HDD MQ04UBD       | 1      | 13      | 229   | 2     | 0.58   |
| Seagate   | Laptop Ultrathin       | 1      | 4       | 207   | 0     | 0.57   |
| Toshiba   | 3.5" HDD E300          | 2      | 7       | 207   | 0     | 0.57   |
| Toshiba   | 2.5" HDD MK..75GSX     | 1      | 2       | 272   | 538   | 0.56   |
| Toshiba   | 2.5" HDD MQ01ACF       | 2      | 66      | 309   | 65    | 0.56   |
| HGST      | Ultrastar DC HC310     | 2      | 7       | 205   | 0     | 0.56   |
| Toshiba   | 2.5" HDD MK..53GSX     | 1      | 1       | 201   | 0     | 0.55   |
| Toshiba   | 2.5" HDD MK..75GSX     | 4      | 108     | 480   | 395   | 0.55   |
| Samsung   | SpinPoint F1 EG        | 1      | 3       | 671   | 1018  | 0.55   |
| WDC       | Black Mobile           | 28     | 240     | 228   | 10    | 0.55   |
| WDC       | Scorpio                | 2      | 2       | 199   | 0     | 0.55   |
| Fujitsu   | MHX BT                 | 2      | 8       | 515   | 21    | 0.55   |
| Toshiba   | 2.5" HDD MK..76GSX     | 6      | 16      | 268   | 121   | 0.54   |
| Toshiba   | P300                   | 4      | 408     | 211   | 13    | 0.54   |
| Maxtor    | DiamondMax D540X-4K    | 3      | 3       | 582   | 16    | 0.54   |
| Seagate   | Momentus 5400 PSD      | 2      | 3       | 352   | 338   | 0.53   |
| Seagate   | Barracuda ATA III      | 1      | 1       | 194   | 0     | 0.53   |
| Toshiba   | 2.5" HDD MQ01ABF       | 2      | 39      | 247   | 41    | 0.53   |
| Toshiba   | 1.8" HDD MK..29GSG     | 3      | 7       | 390   | 337   | 0.53   |
| Samsung   | SpinPoint MP5          | 3      | 10      | 343   | 182   | 0.53   |
| Samsung   | SpinPoint MT2          | 1      | 5       | 191   | 0     | 0.53   |
| Hitachi   | Travelstar Z7K320      | 4      | 58      | 475   | 490   | 0.52   |
| Samsung   | SpinPoint P80          | 18     | 127     | 587   | 158   | 0.52   |
| Toshiba   | 2.5" HDD MQ01ABD       | 3      | 11      | 247   | 1     | 0.52   |
| Toshiba   | 2.5" HDD MK..59GSM     | 2      | 33      | 609   | 804   | 0.51   |
| Seagate   | Video 3.5              | 1      | 3       | 186   | 0     | 0.51   |
| Seagate   | Momentus 5400.4        | 3      | 88      | 518   | 393   | 0.51   |
| Apple     | Seagate Barracuda 7... | 1      | 1       | 185   | 0     | 0.51   |
| IBM/Hi... | Deskstar 120GXP        | 4      | 8       | 655   | 117   | 0.50   |
| Hitachi   | Travelstar 5K1000      | 3      | 26      | 491   | 718   | 0.50   |
| HGST      | Travelstar Z5K1000     | 3      | 86      | 206   | 49    | 0.50   |
| Seagate   | Barracuda Compute      | 4      | 94      | 198   | 19    | 0.50   |
| Fujitsu   | MHZ BT                 | 1      | 2       | 1426  | 6     | 0.50   |
| Hitachi   | Travelstar Z5K500      | 3      | 169     | 373   | 200   | 0.50   |
| Seagate   | DB35.4                 | 1      | 2       | 701   | 21    | 0.49   |
| MediaMax  | WL3000                 | 1      | 1       | 178   | 0     | 0.49   |
| Hitachi   | Travelstar Z5K320      | 3      | 243     | 333   | 301   | 0.48   |
| Seagate   | Barracuda 2.5 5400     | 6      | 258     | 203   | 52    | 0.48   |
| Seagate   | Momentus 5400.3        | 8      | 163     | 445   | 450   | 0.48   |
| Toshiba   | 2.5" HDD MK..59GSM     | 1      | 20      | 496   | 413   | 0.47   |
| Hitachi   | Travelstar 5K250       | 10     | 202     | 537   | 148   | 0.47   |
| Toshiba   | N300                   | 3      | 17      | 251   | 11    | 0.47   |
| Seagate   | FireCuda 2.5           | 6      | 127     | 218   | 59    | 0.47   |
| Toshiba   | 2.5" HDD MK..55GSX     | 8      | 85      | 425   | 77    | 0.46   |
| Lenovo    | Seagate Enterprise     | 1      | 1       | 165   | 0     | 0.45   |
| Fujitsu   | MHW AT                 | 2      | 2       | 165   | 0     | 0.45   |
| Toshiba   | 2.5" HDD MK..34GSX     | 2      | 13      | 383   | 166   | 0.45   |
| WDC       | Shrek LT 2.5           | 6      | 6       | 274   | 2     | 0.45   |
| Toshiba   | 2.5" HDD MK..63GSX     | 2      | 18      | 643   | 18    | 0.45   |
| Toshiba   | 2.5" HDD MK..37GSX     | 1      | 19      | 448   | 139   | 0.44   |
| Hitachi   | Travelstar 5K320       | 12     | 163     | 508   | 227   | 0.44   |
| Fujitsu   | MHZ BS                 | 1      | 1       | 159   | 0     | 0.44   |
| WDC       | Ultrastar DC HC530     | 2      | 4       | 158   | 0     | 0.43   |
| WDC       | Black UltraSlim        | 1      | 2       | 596   | 10    | 0.43   |
| Seagate   | MobileMax-2            | 1      | 1       | 155   | 0     | 0.43   |
| Samsung   | SpinPoint V80          | 3      | 4       | 597   | 63    | 0.42   |
| Seagate   | Momentus 7200.1        | 2      | 9       | 541   | 366   | 0.42   |
| Samsung   | SpinPoint V60          | 1      | 6       | 1055  | 104   | 0.42   |
| WDC       | Black P10              | 2      | 4       | 150   | 0     | 0.41   |
| Toshiba   | 2.5" HDD MQ01ABF       | 1      | 412     | 194   | 71    | 0.41   |
| Samsung   | SpinPoint P120         | 5      | 101     | 886   | 613   | 0.40   |
| Toshiba   | 2.5" HDD MK..59GSXP    | 7      | 144     | 399   | 320   | 0.40   |
| MediaMax  | WL320                  | 1      | 1       | 146   | 0     | 0.40   |
| Hitachi   | Travelstar 5K500       | 1      | 6       | 520   | 5     | 0.40   |
| WDC       | Protege                | 6      | 12      | 681   | 34    | 0.40   |
| Toshiba   | 2.5" HDD MQ04UBB       | 1      | 6       | 144   | 0     | 0.40   |
| Seagate   | Mobile HDD             | 3      | 572     | 178   | 116   | 0.39   |
| Toshiba   | 1.8" HDD               | 5      | 12      | 401   | 12    | 0.39   |
| HP        | Ultrastar 7K4000       | 1      | 2       | 1500  | 505   | 0.39   |
| Toshiba   | 2.5" HDD MQ04ABD       | 1      | 2       | 142   | 0     | 0.39   |
| Hitachi   | Travelstar 7K500       | 10     | 97      | 460   | 730   | 0.39   |
| Seagate   | Momentus 5400.6        | 11     | 995     | 470   | 470   | 0.39   |
| Toshiba   | L200                   | 5      | 39      | 145   | 29    | 0.38   |
| HP        | Barracuda ES.2         | 1      | 1       | 138   | 0     | 0.38   |
| Hitachi   | Travelstar 5K160       | 11     | 184     | 518   | 74    | 0.38   |
| IBM/Hi... | Travelstar 60GH and... | 3      | 4       | 190   | 2     | 0.37   |
| HGST      | Deskstar 5K4000        | 1      | 2       | 133   | 0     | 0.37   |
| Quantum   | Fireball lct15         | 3      | 3       | 226   | 2     | 0.36   |
| HGST      | Travelstar Z5K500      | 6      | 574     | 290   | 352   | 0.36   |
| Toshiba   | 2.5" HDD MQ02ABF       | 1      | 7       | 147   | 1     | 0.36   |
| Seagate   | Momentus Thin          | 9      | 211     | 397   | 588   | 0.35   |
| Toshiba   | 1.8" HDD               | 5      | 13      | 701   | 179   | 0.35   |
| HPE       | Proliant HardDrive     | 1      | 2       | 127   | 0     | 0.35   |
| Hitachi   | Travelstar 5K100       | 9      | 54      | 438   | 64    | 0.35   |
| Toshiba   | 1.8" HDD MK..16GSG     | 1      | 3       | 272   | 4     | 0.34   |
| Seagate   | SpinPoint M8U (USB)    | 2      | 36      | 145   | 1     | 0.34   |
| Magnet... | Unknown                | 4      | 5       | 123   | 0     | 0.34   |
| Toshiba   | 2.5" HDD MK..59GSX     | 1      | 4       | 178   | 319   | 0.33   |
| Seagate   | FreePlay               | 4      | 17      | 343   | 816   | 0.33   |
| Toshiba   | 2.5" HDD MK..65GSX     | 13     | 232     | 464   | 292   | 0.33   |
| Seagate   | BarraCuda 3.5          | 2      | 7       | 173   | 2     | 0.33   |
| Seagate   | BarraCuda 3.5 (SMR)    | 1      | 173     | 128   | 17    | 0.33   |
| Hitachi   | Travelstar 5K120       | 2      | 4       | 384   | 5     | 0.32   |
| Fujitsu   | MHT                    | 6      | 8       | 496   | 269   | 0.32   |
| Seagate   | Laptop Thin HDD        | 7      | 915     | 278   | 404   | 0.31   |
| Seagate   | SV35.2                 | 3      | 8       | 609   | 881   | 0.31   |
| Seagate   | Exos 5E8               | 1      | 5       | 110   | 0     | 0.30   |
| Toshiba   | 3.5" HDD DT01ACA       | 3      | 7       | 109   | 0     | 0.30   |
| Seagate   | Ultra Mobile HDD       | 2      | 3       | 107   | 0     | 0.30   |
| Samsung   | HM100UX (S2 Portable)  | 1      | 2       | 186   | 4     | 0.29   |
| IBM       | Travelstar 25GS, 18... | 2      | 2       | 156   | 3     | 0.29   |
| Toshiba   | 2.5" HDD MK..51GSY     | 1      | 1       | 939   | 8     | 0.29   |
| Toshiba   | 2.5" HDD H200          | 2      | 4       | 103   | 0     | 0.28   |
| Toshiba   | 2.5" HDD MK..46GSX     | 4      | 45      | 491   | 123   | 0.28   |
| Toshiba   | 2.5" HDD MK..65GSX     | 4      | 7       | 301   | 53    | 0.28   |
| WDC       | Ultrastar He10/12      | 1      | 3       | 100   | 0     | 0.28   |
| IBM       | Deskstar 40GV & 75G... | 3      | 4       | 1041  | 24    | 0.27   |
| Toshiba   | V300                   | 1      | 1       | 97    | 0     | 0.27   |
| Toshiba   | MG06ACA Enterprise ... | 3      | 7       | 95    | 0     | 0.26   |
| Toshiba   | 2.5" HDD MQ04ABF       | 1      | 211     | 104   | 32    | 0.26   |
| Toshiba   | 2.5" HDD MK..37GSX     | 2      | 54      | 505   | 93    | 0.25   |
| Toshiba   | 2.5" HDD MK..55GSX     | 3      | 6       | 320   | 461   | 0.25   |
| Toshiba   | 2.5" HDD MK..46GSX     | 1      | 12      | 375   | 41    | 0.24   |
| Samsung   | SpinPoint M            | 2      | 11      | 289   | 16    | 0.24   |
| Hitachi   | CinemaStar 5K1000.B    | 2      | 2       | 527   | 369   | 0.23   |
| Toshiba   | 2.5" HDD MK..52GSX     | 5      | 83      | 565   | 134   | 0.23   |
| Seagate   | Barracuda 7200.11      | 12     | 394     | 837   | 332   | 0.23   |
| Toshiba   | 2.5" HDD L200 Slim     | 1      | 10      | 81    | 0     | 0.22   |
| Seagate   | Momentus 4200.2        | 5      | 7       | 466   | 304   | 0.22   |
| China     | Unknown                | 3      | 3       | 159   | 459   | 0.21   |
| WDC       | White Label            | 5      | 35      | 84    | 1     | 0.21   |
| Toshiba   | 2.5" HDD MK..61GSY[N]  | 6      | 47      | 109   | 213   | 0.20   |
| Seagate   | LD25 Series            | 2      | 3       | 161   | 695   | 0.20   |
| Seagate   | Momentus 5400.5        | 5      | 92      | 444   | 208   | 0.20   |
| Seagate   | Barracuda Pro Compute  | 2      | 127     | 94    | 32    | 0.20   |
| Seagate   | Terascale              | 2      | 2       | 71    | 0     | 0.20   |
| HGST      | Travelstar Z5K500.B    | 1      | 20      | 70    | 0     | 0.19   |
| Toshiba   | 2.5" HDD MK..56GSY     | 6      | 18      | 145   | 186   | 0.19   |
| Samsung   | SpinPoint M8U (USB)    | 1      | 2       | 66    | 0     | 0.18   |
| IBM/Hi... | Deskstar 60GXP         | 2      | 4       | 774   | 82    | 0.18   |
| MediaMax  | WL250                  | 4      | 5       | 450   | 4     | 0.18   |
| WDC       | Internal Use HDD       | 9      | 23      | 64    | 0     | 0.18   |
| WDC       | Scorpio EIDE           | 7      | 8       | 356   | 71    | 0.17   |
| MediaMax  | WL750                  | 1      | 1       | 59    | 0     | 0.16   |
| Samsung   | SpinPoint M40/60/80    | 9      | 22      | 437   | 432   | 0.16   |
| IBM/Hi... | Hitachi Travelstar ... | 4      | 14      | 351   | 39    | 0.15   |
| Hitachi   | Travelstar 4K40        | 1      | 6       | 456   | 186   | 0.14   |
| Toshiba   | 2.5" HDD MK..76GSX     | 5      | 101     | 95    | 243   | 0.14   |
| Seagate   | Constellation          | 1      | 1       | 2980  | 59    | 0.14   |
| Seagate   | SV35.3                 | 2      | 2       | 831   | 12    | 0.13   |
| Seagate   | Exos X16               | 2      | 11      | 47    | 0     | 0.13   |
| Samsung   | SpinPoint M7U (USB)    | 2      | 3       | 46    | 0     | 0.13   |
| MARSHAL   | Unknown                | 4      | 6       | 163   | 53    | 0.13   |
| Toshiba   | 1.8" HDD MK..33GSG     | 2      | 6       | 438   | 330   | 0.13   |
| Samsung   | SpinPoint N2           | 2      | 2       | 46    | 1044  | 0.12   |
| WDC       | IU HA500               | 1      | 5       | 44    | 0     | 0.12   |
| Toshiba   | 2.5" HDD MQ02ABF..H    | 2      | 7       | 124   | 289   | 0.11   |
| Samsung   | SpinPoint M6           | 3      | 21      | 304   | 424   | 0.10   |
| HGST      | Travelstar Z7K500.B    | 1      | 2       | 33    | 0     | 0.09   |
| Toshiba   | 3.5" HDD P300          | 2      | 7       | 32    | 0     | 0.09   |
| HGST      | Ultrastar HC310/320    | 2      | 6       | 36    | 254   | 0.09   |
| Samsung   | SpinPoint M5           | 5      | 104     | 345   | 422   | 0.09   |
| Hitachi   | CinemaStar Z5K320      | 2      | 2       | 43    | 2     | 0.09   |
| Hitachi   | Travelstar 5K80        | 3      | 4       | 225   | 173   | 0.08   |
| Samsung   | SpinPoint V40+         | 2      | 3       | 1003  | 159   | 0.08   |
| Seagate   | U8                     | 1      | 1       | 754   | 24    | 0.08   |
| Seagate   | Mobile USB Momentus    | 1      | 3       | 29    | 0     | 0.08   |
| Hitachi   | Travelstar DK23XX/D... | 4      | 5       | 344   | 104   | 0.08   |
| Maxtor    | DiamondMax 22          | 4      | 40      | 867   | 402   | 0.08   |
| MediaMax  | WL120                  | 1      | 1       | 139   | 4     | 0.08   |
| Samsung   | USB Hard Disk          | 2      | 2       | 45    | 166   | 0.07   |
| WDC       | IU CB500               | 3      | 9       | 38    | 226   | 0.07   |
| CLOVER    | Unknown                | 1      | 1       | 22    | 0     | 0.06   |
| MediaMax  | WL1500                 | 2      | 3       | 800   | 133   | 0.06   |
| MaxDig... | Unknown                | 2      | 2       | 150   | 4     | 0.06   |
| MediaMax  | WL640                  | 1      | 1       | 20    | 0     | 0.05   |
| CLOVER    | Hightech Utania        | 2      | 3       | 19    | 0     | 0.05   |
| WDC       | Unknown                | 8      | 19      | 139   | 20    | 0.05   |
| Apple     | HGST Travelstar 5K750  | 2      | 6       | 230   | 42    | 0.04   |
| Maxtor    | DiamondMax 10 (ATA/... | 22     | 71      | 24    | 91    | 0.04   |
| Seagate   | Pipeline HD Pro        | 1      | 1       | 1038  | 72    | 0.04   |
| WDC       | Caviar WDxxxBA         | 1      | 1       | 296   | 20    | 0.04   |
| Seagate   | MobileMax 80215        | 1      | 1       | 13    | 0     | 0.04   |
| Seagate   | U10                    | 1      | 1       | 380   | 27    | 0.04   |
| Maxtor    | Fireball 3             | 6      | 12      | 39    | 34    | 0.04   |
| Seagate   | DB35.2                 | 2      | 2       | 1265  | 514   | 0.03   |
| Samsung   | SpinPoint N3A          | 1      | 1       | 11    | 0     | 0.03   |
| MediaMax  | WL2000                 | 1      | 1       | 33    | 2     | 0.03   |
| WDC       | eServer                | 1      | 1       | 10    | 0     | 0.03   |
| Toshiba   | 2.5" HDD               | 3      | 3       | 301   | 66    | 0.03   |
| Seagate   | SpinPoint F3           | 1      | 1       | 9     | 0     | 0.03   |
| Seagate   | Pipeline HD 5900.1     | 3      | 8       | 521   | 145   | 0.03   |
| Samsung   | SpinPoint T            | 1      | 1       | 469   | 51    | 0.02   |
| LENOVO    | RE                     | 1      | 2       | 7     | 0     | 0.02   |
| Maxtor    | DiamondMax Plus 8      | 4      | 20      | 26    | 24    | 0.02   |
| Maxtor    | MaXLine III (ATA/13... | 4      | 6       | 16    | 40    | 0.02   |
| Maxtor    | MaXLine III            | 1      | 1       | 244   | 32    | 0.02   |
| Seagate   | Lyrion                 | 1      | 1       | 7     | 0     | 0.02   |
| HPE       | Unknown                | 1      | 1       | 6     | 0     | 0.02   |
| Maxtor    | DiamondMax 1750        | 1      | 1       | 5613  | 1044  | 0.01   |
| Hitachi   | Travelstar E7K100      | 1      | 1       | 4     | 0     | 0.01   |
| Maxtor    | DiamondMax Plus 9      | 11     | 89      | 28    | 164   | 0.01   |
| Seagate   | FireCuda               | 1      | 1       | 39    | 18    | 0.01   |
| Hitachi   | Ultrastar 5K3000       | 1      | 1       | 1045  | 595   | 0.00   |
| Maxtor    | DiamondMax 16          | 3      | 5       | 24    | 25    | 0.00   |
| Maxtor    | Fireball 541DX         | 1      | 11      | 23    | 156   | 0.00   |
| Seagate   | Enterprise NAS         | 1      | 1       | 107   | 82    | 0.00   |
| Seagate   | Momentus 5400 FDE.4    | 1      | 1       | 725   | 705   | 0.00   |
| Maxtor    | DiamondMax D540X-4D    | 2      | 5       | 17    | 157   | 0.00   |
| HP        | 1TB SATA disk GB100... | 1      | 1       | 2402  | 3024  | 0.00   |
| Maxtor    | DiamondMax D540X-4G    | 1      | 2       | 20    | 218   | 0.00   |
| MediaMax  | WL400                  | 1      | 1       | 0     | 0     | 0.00   |
| Apple     | Ultrastar A7K2000      | 1      | 1       | 83    | 113   | 0.00   |
| Maxtor    | MaXLine Plus II        | 1      | 2       | 25    | 38    | 0.00   |
| Seagate   | SV35.4                 | 1      | 1       | 685   | 1110  | 0.00   |
| MediaMax  | WL6000                 | 1      | 1       | 637   | 1372  | 0.00   |
| Samsung   | SpinPoint N1           | 1      | 1       | 188   | 3047  | 0.00   |
| Maxtor    | DiamondMax Plus 40 ... | 1      | 1       | 121   | 2068  | 0.00   |

HDD by Vendor
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF   |
|-------------|--------|---------|-------|-------|--------|
| HP          | 20     | 57      | 1389  | 90    | 2.03   |
| Quantum     | 7      | 7       | 608   | 1     | 1.56   |
| HPE         | 3      | 4       | 446   | 0     | 1.22   |
| WDC         | 1704   | 14976   | 616   | 42    | 1.20   |
| Apple       | 16     | 93      | 498   | 63    | 1.15   |
| Hitachi     | 274    | 3953    | 704   | 187   | 1.10   |
| Samsung     | 142    | 2398    | 773   | 243   | 1.04   |
| Seagate     | 604    | 15764   | 585   | 192   | 0.96   |
| ExcelStor   | 8      | 19      | 771   | 13    | 0.92   |
| HGST        | 85     | 1812    | 407   | 236   | 0.80   |
| Fujitsu     | 81     | 425     | 486   | 152   | 0.76   |
| Toshiba     | 230    | 4599    | 351   | 107   | 0.64   |
| Maxtor      | 102    | 585     | 475   | 248   | 0.57   |
| Lenovo      | 1      | 1       | 165   | 0     | 0.45   |
| IBM/Hitachi | 17     | 36      | 493   | 51    | 0.34   |
| Magnetic... | 4      | 5       | 123   | 0     | 0.34   |
| MediaMax    | 20     | 22      | 415   | 83    | 0.30   |
| IBM         | 5      | 6       | 746   | 17    | 0.28   |
| China       | 3      | 3       | 159   | 459   | 0.21   |
| MARSHAL     | 4      | 6       | 163   | 53    | 0.13   |
| MaxDigital  | 2      | 2       | 150   | 4     | 0.06   |
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

See complete list of tested SSD samples in the Appendix 2 ([All_SSD.md](/All_SSD.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF   |
|-----------|--------------------|--------|---------|-------|-------|--------|
| OCZ       | VERTEX v1.10       | 64 GB  | 1       | 4164  | 0     | 11.41  |
| Intel     | SSDSA2SH064G1GC    | 64 GB  | 2       | 2956  | 0     | 8.10   |
| Intel     | SSDSA2MH080G1GC    | 80 GB  | 1       | 2796  | 0     | 7.66   |
| OCZ       | AGILITY2           | 50 GB  | 1       | 2769  | 0     | 7.59   |
| Intenso   | SSD                | 64 GB  | 1       | 2587  | 0     | 7.09   |
| Samsung   | MCCOE64G5MPP-0VA   | 64 GB  | 1       | 2540  | 0     | 6.96   |
| Corsair   | Force GT           | 50 GB  | 1       | 2387  | 0     | 6.54   |
| Samsung   | MZ7PC256HAFU-000L7 | 256 GB | 1       | 2371  | 0     | 6.50   |
| HPE       | MK0100GCTYU        | 100 GB | 1       | 2360  | 0     | 6.47   |
| Toshiba   | THNSNH060GCST      | 64 GB  | 1       | 2246  | 0     | 6.16   |
| Corsair   | CSSD-F40GB2-A      | 40 GB  | 1       | 2230  | 0     | 6.11   |
| Micron    | C400-MTFDDAC128MAM | 128 GB | 1       | 2224  | 0     | 6.09   |
| SandForce | FM-25S2S-120GBP2   | 120 GB | 1       | 2101  | 0     | 5.76   |
| Intel     | SSDSC2BB160G4      | 160 GB | 1       | 2027  | 0     | 5.55   |
| Intel     | SSDSC2BB480G4      | 480 GB | 2       | 1984  | 0     | 5.44   |
| Intel     | SSDSC2BA200G3C     | 200 GB | 1       | 1963  | 0     | 5.38   |
| OCZ       | VERTEX2 3.5        | 240 GB | 1       | 1798  | 0     | 4.93   |
| Kingston  | SVP100S2512G       | 512 GB | 1       | 1795  | 0     | 4.92   |
| Intel     | SSDSC2BB800G4      | 800 GB | 2       | 1780  | 0     | 4.88   |
| Samsung   | MZHPV256HDGL-000H1 | 256 GB | 1       | 1721  | 0     | 4.72   |
| Intel     | SSDSC2BB120G6      | 120 GB | 1       | 1702  | 0     | 4.66   |
| OCZ       | VERTEX3            | 96 GB  | 1       | 1686  | 0     | 4.62   |
| Samsung   | MZ7PD128HCFV-000H7 | 128 GB | 1       | 1667  | 0     | 4.57   |
| SanDisk   | SDSA6DM-016G-1006  | 16 GB  | 1       | 1639  | 0     | 4.49   |
| Kingston  | SVP100S296G        | 96 GB  | 2       | 1638  | 0     | 4.49   |
| ADATA     | SP310              | 32 GB  | 1       | 1628  | 0     | 4.46   |
| Samsung   | SSD PB22-JS3 FD... | 128 GB | 1       | 1626  | 0     | 4.46   |
| OCZ       | VECTOR             | 512 GB | 1       | 1610  | 0     | 4.41   |
| Intel     | SSDSC2BA100G3      | 100 GB | 22      | 1675  | 1     | 4.38   |
| Crucial   | CT500MX200SSD3     | 500 GB | 1       | 1556  | 0     | 4.26   |
| OCZ       | VERTEX2            | 40 GB  | 2       | 1543  | 0     | 4.23   |
| Intel     | SSDSA2SH032G1GN    | 32 GB  | 2       | 1518  | 0     | 4.16   |
| Mushkin   | MKNSSDCR240GB      | 240 GB | 1       | 1513  | 0     | 4.15   |
| Intel     | SSDSC2BX400G4      | 400 GB | 1       | 1508  | 0     | 4.13   |
| OCZ       | VERTEX2 3.5        | 90 GB  | 1       | 1507  | 0     | 4.13   |
| SanDisk   | SD7SN6S512G1122    | 512 GB | 1       | 1488  | 0     | 4.08   |
| Kingston  | SSDNOW             | 32 GB  | 2       | 1465  | 0     | 4.02   |
| Corsair   | Force 3 SSD        | 180 GB | 5       | 1764  | 1     | 3.97   |
| Toshiba   | THNS128GG4BAAA-... | 128 GB | 2       | 1443  | 0     | 3.96   |
| Samsung   | SSD 830 Series     | 512 GB | 10      | 1437  | 0     | 3.94   |
| Samsung   | MZ7LM240HCGR-00003 | 240 GB | 2       | 1433  | 0     | 3.93   |
| Intel     | SSDMCEAC120B3A     | 120 GB | 2       | 1373  | 0     | 3.76   |
| Samsung   | MZ7LN512HCHP-00000 | 512 GB | 2       | 1362  | 0     | 3.73   |
| Samsung   | MO0100EBTJT        | 100 GB | 1       | 1361  | 0     | 3.73   |
| Corsair   | Force GT           | 240 GB | 2       | 1634  | 1     | 3.73   |
| Corsair   | Force 3 SSD        | 240 GB | 9       | 1407  | 1     | 3.71   |
| WDC       | WD1001X06X-00SJVT0 | 1.1 TB | 2       | 1341  | 0     | 3.68   |
| OCZ       | SOLID3             | 64 GB  | 5       | 1604  | 223   | 3.66   |
| Intel     | SSDSC2BA200G3      | 200 GB | 1       | 1330  | 0     | 3.64   |
| Intel     | SSDSC2BB080G4      | 80 GB  | 3       | 1302  | 0     | 3.57   |
| SanDisk   | SD5SE2128G1002E    | 128 GB | 4       | 1285  | 0     | 3.52   |
| Samsung   | MZ7LN256HMJP-00000 | 256 GB | 2       | 1259  | 0     | 3.45   |
| Toshiba   | THNSNJ120PCSZ      | 120 GB | 2       | 1255  | 0     | 3.44   |
| Intel     | SSDSA2CW080G3      | 80 GB  | 12      | 1309  | 1     | 3.42   |
| Samsung   | SSD 840 EVO        | 1 TB   | 24      | 1244  | 0     | 3.41   |
| Kingston  | SKC300S37A480G     | 480 GB | 1       | 1231  | 0     | 3.37   |
| Crucial   | C300-CTFDDAC256MAG | 256 GB | 3       | 1525  | 336   | 3.36   |
| Kingston  | SH100S3120G        | 120 GB | 4       | 1207  | 0     | 3.31   |
| Corsair   | Force GT           | 180 GB | 3       | 1205  | 0     | 3.30   |
| Samsung   | SSD PM830 2.5" 7mm | 256 GB | 12      | 1202  | 0     | 3.29   |
| Intel     | SSDSC2BB240G4      | 240 GB | 3       | 1196  | 0     | 3.28   |
| Toshiba   | THNSFC256GAMJ      | 256 GB | 2       | 1189  | 0     | 3.26   |
| Seagate   | ST480HM000-1G5162  | 480 GB | 2       | 1282  | 1     | 3.20   |
| Micron    | MTFDDAK064MAR-1... | 64 GB  | 1       | 1164  | 0     | 3.19   |
| OCZ       | VERTEX2            | 64 GB  | 13      | 1163  | 0     | 3.19   |
| MyDigi... | SB M2 SSD          | 240 GB | 1       | 1161  | 0     | 3.18   |
| Samsung   | MZMPC064HBDR-000L1 | 64 GB  | 1       | 1157  | 0     | 3.17   |
| Toshiba   | THNS064GG2BNAA     | 64 GB  | 5       | 1157  | 0     | 3.17   |
| Crucial   | M4-CT256M4SSD1     | 256 GB | 3       | 1157  | 0     | 3.17   |
| Samsung   | MZ7WD240HCFV-00003 | 240 GB | 1       | 1154  | 0     | 3.16   |
| Toshiba   | THNSNC128GMMJ      | 128 GB | 5       | 1148  | 0     | 3.15   |
| SanDisk   | SDSA6MM-016G-1006  | 16 GB  | 3       | 1121  | 0     | 3.07   |
| SanDisk   | SD5SG2128G1052E    | 128 GB | 1       | 1121  | 0     | 3.07   |
| Intel     | SSDSC2BP480G4      | 480 GB | 5       | 1117  | 0     | 3.06   |
| Kingston  | RBU-SC400S37256G   | 256 GB | 2       | 1095  | 0     | 3.00   |
| Samsung   | MZ7PD480HAGM-000DA | 480 GB | 1       | 1092  | 0     | 2.99   |
| Samsung   | SSD 840 EVO 120... | 120 GB | 4       | 1090  | 0     | 2.99   |
| Corsair   | Force GS           | 180 GB | 3       | 1087  | 0     | 2.98   |
| Micron    | M500_MTFDDAK480MAV | 480 GB | 1       | 1083  | 0     | 2.97   |
| Samsung   | SSD PM800 2.5"     | 128 GB | 2       | 1081  | 0     | 2.96   |
| Samsung   | SSD 850 EVO        | 2 TB   | 11      | 1077  | 0     | 2.95   |
| Intel     | SSDSA2MH080G1HP    | 80 GB  | 1       | 1075  | 0     | 2.95   |
| OCZ       | REVODRIVE350       | 120 GB | 4       | 1073  | 0     | 2.94   |
| Samsung   | MZ7PC128HAFU-000L1 | 128 GB | 4       | 1069  | 0     | 2.93   |
| Samsung   | MZHPV512HDGL-00000 | 512 GB | 2       | 1064  | 0     | 2.92   |
| Crucial   | M4-CT512M4SSD2     | 512 GB | 5       | 1600  | 202   | 2.88   |
| OCZ       | AGILITY4           | 128 GB | 6       | 1045  | 0     | 2.86   |
| Intel     | SSDSC2CW240A3      | 240 GB | 28      | 1035  | 0     | 2.84   |
| Apple     | SSD SM1024G        | 1 TB   | 2       | 1029  | 0     | 2.82   |
| Samsung   | MZ7PC128HAFU-000L5 | 128 GB | 2       | 1028  | 0     | 2.82   |
| Micron    | C400-MTFDDAK128MAM | 128 GB | 2       | 1024  | 0     | 2.81   |
| SK hynix  | SC300B SATA        | 512 GB | 1       | 1018  | 0     | 2.79   |
| SanDisk   | SSD U110           | 32 GB  | 1       | 1009  | 0     | 2.76   |
| Crucial   | M4-CT128M4SSD2     | 128 GB | 43      | 1040  | 95    | 2.76   |
| ADATA     | SP800              | 32 GB  | 2       | 1001  | 0     | 2.74   |
| Samsung   | SSD 850 PRO        | 1 TB   | 26      | 1000  | 0     | 2.74   |
| Transcend | TS256GMTS600       | 256 GB | 1       | 998   | 0     | 2.73   |
| Apple     | SSD SM1024F        | 1 TB   | 4       | 997   | 0     | 2.73   |
| Hyundai   | 120GB SSD          | 120 GB | 1       | 997   | 0     | 2.73   |
| OCZ       | VERTEX2            | 120 GB | 9       | 986   | 0     | 2.70   |
| Corsair   | Force LE SSD       | 240 GB | 1       | 983   | 0     | 2.69   |
| Apple     | SSD SM768E         | 752 GB | 1       | 982   | 0     | 2.69   |
| Intel     | SSDSC2BX200G4      | 200 GB | 2       | 969   | 0     | 2.66   |
| Patriot   | Ignite             | 480 GB | 1       | 967   | 0     | 2.65   |
| MyDigi... | BP5                | 240 GB | 2       | 967   | 0     | 2.65   |
| Kingston  | SVP200S360G        | 64 GB  | 6       | 966   | 0     | 2.65   |
| SanDisk   | SSD U110           | 128 GB | 3       | 958   | 0     | 2.63   |
| Samsung   | MZ7TY256HDHP-000L1 | 256 GB | 1       | 950   | 0     | 2.60   |
| OCZ       | VECTOR             | 256 GB | 3       | 943   | 0     | 2.58   |
| Intel     | SSDSA2BW120G3A     | 120 GB | 1       | 939   | 0     | 2.58   |
| Intel     | SSDSC2BB480G7      | 480 GB | 2       | 935   | 0     | 2.56   |
| Kingston  | SE50S3480G         | 480 GB | 10      | 1104  | 1     | 2.54   |
| SK hynix  | SC300 2.5 7MM      | 256 GB | 1       | 923   | 0     | 2.53   |
| SanDisk   | SDLF1CRR-019T-1HA2 | 1.9 TB | 1       | 916   | 0     | 2.51   |
| KingSpec  | ACSC2M064S25       | 64 GB  | 2       | 910   | 0     | 2.49   |
| OWC       | Mercury EXTREME... | 480 GB | 5       | 907   | 0     | 2.49   |
| Intel     | SSDMCEAW120A4      | 120 GB | 2       | 902   | 0     | 2.47   |
| Samsung   | SSD 830 Series     | 128 GB | 36      | 900   | 0     | 2.47   |
| Kingston  | SKC310S37A960G     | 960 GB | 1       | 885   | 0     | 2.43   |
| Samsung   | SSD SM871 2.5 7mm  | 256 GB | 3       | 882   | 0     | 2.42   |
| Corsair   | Neutron SSD        | 256 GB | 1       | 879   | 0     | 2.41   |
| Toshiba   | THNSNH256GMCT      | 256 GB | 3       | 875   | 0     | 2.40   |
| Samsung   | SSD PM800 2.5"     | 256 GB | 1       | 871   | 0     | 2.39   |
| Axiom     | Signature III SSD  | 240 GB | 1       | 866   | 0     | 2.37   |
| Samsung   | MZ7LF128HCHP-00000 | 128 GB | 1       | 865   | 0     | 2.37   |
| Intel     | SSDSC2CW180A3      | 180 GB | 11      | 863   | 0     | 2.37   |
| Phison    | SATA SSD           | 16 GB  | 2       | 862   | 0     | 2.36   |
| Apple     | SSD TS256A         | 256 GB | 1       | 858   | 0     | 2.35   |
| Crucial   | CT120M500SSD3      | 120 GB | 4       | 947   | 8     | 2.30   |
| PNY       | CS1311 480GB SSD   | 480 GB | 3       | 837   | 0     | 2.29   |
| Kingston  | RBU-SC100S37256GD  | 256 GB | 1       | 833   | 0     | 2.28   |
| Patriot   | Blaze SSD ATA D... | 240 GB | 1       | 833   | 0     | 2.28   |
| Phison    | UGBA1TPH32H0S2-... | 32 GB  | 1       | 833   | 0     | 2.28   |
| Samsung   | SSD PM800 Serie... | 256 GB | 2       | 825   | 0     | 2.26   |
| Samsung   | SSD 830 Series     | 64 GB  | 17      | 824   | 0     | 2.26   |
| Patriot   | Blast              | 480 GB | 1       | 823   | 0     | 2.26   |
| Samsung   | MZ7GE240HMGR-00003 | 240 GB | 1       | 822   | 0     | 2.25   |
| Kingston  | SNVP325S2512GB     | 512 GB | 1       | 822   | 0     | 2.25   |
| Innodisk  | DES25-64GM41BC1... | 64 GB  | 1       | 821   | 0     | 2.25   |
| Crucial   | M4-CT128M4SSD1     | 128 GB | 6       | 819   | 0     | 2.24   |
| Samsung   | MZHPV128HDGM-00000 | 128 GB | 2       | 818   | 0     | 2.24   |
| Apple     | SSD TS256C         | 256 GB | 6       | 809   | 0     | 2.22   |
| SanDisk   | SD6SF1M064G1022    | 64 GB  | 2       | 803   | 0     | 2.20   |
| OCZ       | VERTEX PLUS R2     | 64 GB  | 2       | 802   | 0     | 2.20   |
| Intel     | SSDSC2BB120G4      | 120 GB | 2       | 801   | 0     | 2.20   |
| OCZ       | DENRSTE251M45-0... | 100 GB | 1       | 801   | 0     | 2.20   |
| ADATA     | SSD S599           | 55 GB  | 1       | 801   | 0     | 2.20   |
| SanDisk   | SD6SP1M128G1102    | 128 GB | 2       | 797   | 0     | 2.18   |
| SanDisk   | SSD U110           | 64 GB  | 3       | 797   | 0     | 2.18   |
| OCZ       | VERTEX PLUS R2     | 247 GB | 1       | 797   | 0     | 2.18   |
| Samsung   | MZ7KM480HMHQ-00005 | 480 GB | 2       | 794   | 0     | 2.18   |
| Micron    | MTFDDAK256MBF-1... | 256 GB | 2       | 790   | 0     | 2.17   |
| Crucial   | CT1024MX200SSD1    | 1 TB   | 5       | 862   | 1     | 2.16   |
| Toshiba   | THNSNH060GMCT      | 64 GB  | 1       | 787   | 0     | 2.16   |
| Samsung   | SSD CM871 M.2 2280 | 128 GB | 1       | 785   | 0     | 2.15   |
| OWC       | Mercury Electra... | 500 GB | 3       | 783   | 0     | 2.15   |
| PNY       | CS1311 960GB SSD   | 960 GB | 2       | 781   | 0     | 2.14   |
| Micron    | C400-MTFDDAC256MAM | 256 GB | 1       | 780   | 0     | 2.14   |
| Toshiba   | THNSNJ512GDNU      | 512 GB | 1       | 779   | 0     | 2.14   |
| Corsair   | Force 3 SSD        | 64 GB  | 16      | 815   | 1     | 2.13   |
| Corsair   | Force GS           | 90 GB  | 1       | 776   | 0     | 2.13   |
| Samsung   | MZNLF192HCGS-000L1 | 192 GB | 1       | 776   | 0     | 2.13   |
| SanDisk   | SD8SB8U1T001122    | 1 TB   | 1       | 776   | 0     | 2.13   |
| SanDisk   | SD9SB8W256G1014    | 256 GB | 1       | 772   | 0     | 2.12   |
| Samsung   | MZMPC032HBCD-000D1 | 32 GB  | 5       | 769   | 0     | 2.11   |
| Lite-On   | ECE-240NAS         | 240 GB | 1       | 766   | 0     | 2.10   |
| Samsung   | MZ7KM480HAHP-00005 | 480 GB | 1       | 765   | 0     | 2.10   |
| Kingston  | SVP200S37A480G     | 480 GB | 1       | 765   | 0     | 2.10   |
| Intel     | SSDSC2CT060A3      | 64 GB  | 9       | 763   | 0     | 2.09   |
| Samsung   | SSD 840 PRO Series | 128 GB | 41      | 910   | 7     | 2.09   |
| Innodisk  | 2.5" SATA SSD 3ME3 | 64 GB  | 1       | 760   | 0     | 2.08   |
| SanDisk   | SD6SB1M-256G-1006  | 256 GB | 1       | 757   | 0     | 2.08   |
| Patriot   | Flare              | 120 GB | 1       | 753   | 0     | 2.06   |
| Toshiba   | THNSNJ128GMCU      | 128 GB | 2       | 751   | 0     | 2.06   |
| SK hynix  | SC300B SATA        | 256 GB | 2       | 751   | 0     | 2.06   |
| Toshiba   | THNSNJ256G8NU      | 256 GB | 3       | 751   | 0     | 2.06   |
| Crucial   | M4-CT064M4SSD2     | 64 GB  | 20      | 909   | 156   | 2.05   |
| Samsung   | SSD 840 Series     | 500 GB | 7       | 853   | 1     | 2.04   |
| Samsung   | SSD PM851a 2.5 7mm | 1 TB   | 1       | 740   | 0     | 2.03   |
| Toshiba   | THNSNF128GMCS      | 128 GB | 4       | 738   | 0     | 2.02   |
| Intel     | SSDSA2CT040G3      | 40 GB  | 5       | 734   | 0     | 2.01   |
| SanDisk   | SDSSDRC032G        | 32 GB  | 3       | 731   | 0     | 2.00   |
| ADATA     | SSD S510           | 120 GB | 8       | 745   | 1     | 2.00   |
| Mushkin   | MKNSSDAT60GB-DX    | 64 GB  | 1       | 728   | 0     | 2.00   |
| Samsung   | SSD 830 Series     | 256 GB | 24      | 745   | 43    | 1.98   |
| Samsung   | MZ7PA256HMDR-010H1 | 256 GB | 2       | 842   | 520   | 1.98   |
| Micro ... | G2 series          | 64 GB  | 1       | 722   | 0     | 1.98   |
| Samsung   | MZ7TD512HAGM-000L1 | 512 GB | 2       | 715   | 0     | 1.96   |
| Samsung   | SSD 840 Series     | 250 GB | 28      | 740   | 2     | 1.95   |
| Samsung   | MZ7PD256HAFV-000H7 | 256 GB | 7       | 708   | 0     | 1.94   |
| OCZ       | NOCTI              | 64 GB  | 1       | 704   | 0     | 1.93   |
| Plextor   | PX-128M2S          | 128 GB | 3       | 827   | 1     | 1.92   |
| Samsung   | MZHPV256HDGL-00000 | 256 GB | 4       | 700   | 0     | 1.92   |
| Intel     | SSDSC2BA200G4      | 200 GB | 8       | 770   | 1     | 1.92   |
| Kingston  | SV200S364G         | 64 GB  | 4       | 698   | 0     | 1.91   |
| Kingston  | SVP100S2128G       | 128 GB | 1       | 698   | 0     | 1.91   |
| Samsung   | SSD 850 PRO        | 128 GB | 38      | 697   | 0     | 1.91   |
| Intel     | SSDSC2BW240A3L     | 240 GB | 6       | 697   | 0     | 1.91   |
| Intel     | SSDSC2BP240G4      | 240 GB | 4       | 691   | 0     | 1.89   |
| Samsung   | MZ7LN256HCHP-00000 | 256 GB | 1       | 687   | 0     | 1.88   |
| Kingston  | SVP200S390G        | 90 GB  | 1       | 686   | 0     | 1.88   |
| SK hynix  | HFS512G32MND-3312A | 512 GB | 1       | 686   | 0     | 1.88   |
| Samsung   | MZMPC256HBGJ-000H1 | 256 GB | 2       | 685   | 0     | 1.88   |
| Samsung   | SSD 840 EVO        | 500 GB | 43      | 712   | 1     | 1.87   |
| Samsung   | MZ7LN256HCHP-00007 | 256 GB | 1       | 681   | 0     | 1.87   |
| Samsung   | MZ7LN512HMJP-00000 | 512 GB | 2       | 679   | 0     | 1.86   |
| Samsung   | SSD 840 PRO Series | 512 GB | 16      | 1004  | 12    | 1.86   |
| Seagate   | 2E256-TU2-510B00   | 170 GB | 3       | 2072  | 1366  | 1.85   |
| Crucial   | M4-CT256M4SSD2     | 256 GB | 25      | 859   | 204   | 1.85   |
| Kingston  | SNVP325S2128GB     | 128 GB | 1       | 674   | 0     | 1.85   |
| Samsung   | MZ7TE512HMHP-000L2 | 512 GB | 4       | 672   | 0     | 1.84   |
| KingDian  | N400               | 240 GB | 1       | 670   | 0     | 1.84   |
| Mushkin   | MKNSSDCR120GB      | 120 GB | 2       | 1370  | 4     | 1.84   |
| Kingston  | RBU-SNS8152S3128GF | 128 GB | 1       | 665   | 0     | 1.82   |
| OCZ       | AGILITY3           | 64 GB  | 50      | 861   | 4     | 1.82   |
| ADATA     | SP600              | 256 GB | 9       | 663   | 0     | 1.82   |
| Samsung   | SSD PM810 2.5" 7mm | 128 GB | 5       | 720   | 19    | 1.81   |
| Samsung   | MZ7TE256HMHP-00000 | 256 GB | 2       | 659   | 0     | 1.81   |
| Samsung   | SSD 850 PRO        | 512 GB | 60      | 670   | 18    | 1.80   |
| SanDisk   | SD7SB6S128G1122    | 128 GB | 3       | 656   | 0     | 1.80   |
| Apple     | SSD SM0512F        | 500 GB | 3       | 656   | 0     | 1.80   |
| OCZ       | VERTEX3 MI         | 240 GB | 2       | 1285  | 2     | 1.78   |
| Apple     | SSD SM0256F        | 256 GB | 8       | 648   | 0     | 1.78   |
| ADATA     | SP600              | 128 GB | 10      | 648   | 0     | 1.78   |
| Intel     | SSDSCMMW180A3L     | 180 GB | 2       | 646   | 0     | 1.77   |
| Samsung   | SSD 850 PRO        | 2 TB   | 3       | 644   | 0     | 1.76   |
| Kingston  | SMS100S264G        | 64 GB  | 3       | 643   | 0     | 1.76   |
| OCZ       | VECTOR180          | 240 GB | 2       | 641   | 0     | 1.76   |
| Samsung   | MZ7PD128HAFV-000H7 | 128 GB | 5       | 640   | 0     | 1.75   |
| Samsung   | SSD 840 PRO Series | 256 GB | 67      | 673   | 3     | 1.75   |
| Apple     | SSD SD512E         | 500 GB | 1       | 636   | 0     | 1.74   |
| Kingston  | SH103S390G         | 90 GB  | 1       | 636   | 0     | 1.74   |
| Transcend | TS64GSSD320        | 64 GB  | 2       | 633   | 0     | 1.74   |
| OCZ       | VERTEX4            | 256 GB | 30      | 929   | 2     | 1.74   |
| Samsung   | SSD 840 EVO        | 120 GB | 116     | 633   | 1     | 1.73   |
| Samsung   | MZ7TD256HAFV-000L7 | 256 GB | 8       | 631   | 0     | 1.73   |
| Toshiba   | THNSNF512GCSS      | 512 GB | 1       | 631   | 0     | 1.73   |
| Samsung   | SSD 840 EVO        | 250 GB | 141     | 649   | 16    | 1.73   |
| ADATA     | XM11 256GB-V2      | 256 GB | 3       | 625   | 0     | 1.71   |
| Plextor   | PX-512M5Pro        | 512 GB | 2       | 624   | 0     | 1.71   |
| Kingston  | SVP200S37A240G     | 240 GB | 1       | 623   | 0     | 1.71   |
| Intel     | SSDMCEAC120B3      | 120 GB | 1       | 1247  | 1     | 1.71   |
| BlueRay   | SDM9SI128A         | 128 GB | 1       | 619   | 0     | 1.70   |
| Samsung   | MZMPA128HMFU-00000 | 128 GB | 1       | 616   | 0     | 1.69   |
| OCZ       | AGILITY3           | 120 GB | 47      | 816   | 65    | 1.69   |
| Corsair   | Force GT           | 120 GB | 14      | 692   | 1     | 1.69   |
| Intel     | SSDSA2BW120G3H     | 120 GB | 4       | 651   | 1     | 1.68   |
| Samsung   | MZ7TD256HAFV-000L9 | 256 GB | 5       | 612   | 0     | 1.68   |
| Samsung   | MZ7PD128HCFV-000H1 | 128 GB | 4       | 608   | 0     | 1.67   |
| Samsung   | MZ7LN256HCHP-000H1 | 256 GB | 2       | 607   | 0     | 1.66   |
| Kingston  | SKC400S37512G      | 512 GB | 6       | 602   | 0     | 1.65   |
| SanDisk   | SDSSDHII480G       | 480 GB | 11      | 601   | 0     | 1.65   |
| Corsair   | Force 3 SSD        | 480 GB | 1       | 598   | 0     | 1.64   |
| Samsung   | SSD 850 EVO        | 4 TB   | 2       | 597   | 0     | 1.64   |
| Corsair   | CSSD-V64GB2        | 64 GB  | 2       | 597   | 0     | 1.64   |
| SanDisk   | SD7SN6S512G1001    | 512 GB | 1       | 593   | 0     | 1.63   |
| Samsung   | SSD 850 EVO M.2    | 120 GB | 7       | 592   | 0     | 1.62   |
| Micron    | MTFDDAK128MAM-1J1  | 128 GB | 8       | 591   | 0     | 1.62   |
| Micron    | M600_MTFDDAT128MBF | 128 GB | 2       | 589   | 0     | 1.61   |
| Corsair   | Force 3 SSD        | 120 GB | 24      | 670   | 89    | 1.60   |
| OCZ       | DENCSTE351M16-0... | 240 GB | 1       | 585   | 0     | 1.60   |
| SanDisk   | SD7SB3Q-128G-1006  | 128 GB | 2       | 584   | 0     | 1.60   |
| OCZ       | D2RSTK251E19-0200  | 200 GB | 1       | 584   | 0     | 1.60   |
| SanDisk   | SD6SN1M128G        | 128 GB | 1       | 584   | 0     | 1.60   |
| OCZ       | VERTEX2 3.5        | 115 GB | 2       | 583   | 0     | 1.60   |
| Samsung   | SSD PM830 2.5" 7mm | 128 GB | 10      | 772   | 101   | 1.60   |
| Kingston  | SVP200S3120G       | 120 GB | 8       | 709   | 250   | 1.59   |
| Samsung   | MZ7LN512HMJP-000L7 | 512 GB | 5       | 581   | 0     | 1.59   |
| Intel     | SSDSC2BA400G3      | 400 GB | 1       | 580   | 0     | 1.59   |
| Crucial   | C300-CTFDDAC128MAG | 128 GB | 6       | 576   | 0     | 1.58   |
| Micron    | 5200_MTFDDAK1T9TDC | 1.9 TB | 11      | 612   | 1     | 1.58   |
| Toshiba   | THNSNC128GCSJ      | 128 GB | 2       | 574   | 0     | 1.57   |
| SATADOM   | SL 3ME3 V2         | 128 GB | 1       | 574   | 0     | 1.57   |
| SanDisk   | SD8SB8U256G1122    | 256 GB | 5       | 572   | 0     | 1.57   |
| ADATA     | SSD S510           | 64 GB  | 3       | 572   | 0     | 1.57   |
| Samsung   | MZ7LN256HMJP-000L7 | 256 GB | 1       | 571   | 0     | 1.57   |
| ADATA     | SP580              | 240 GB | 1       | 571   | 0     | 1.56   |
| Intel     | SSDSC2CT080A4      | 80 GB  | 4       | 568   | 0     | 1.56   |
| OCZ       | AGILITY4           | 64 GB  | 1       | 567   | 0     | 1.56   |
| Intel     | SSDSCIHF120A4H     | 120 GB | 1       | 566   | 0     | 1.55   |
| Samsung   | MZ7KM480HMHQ0D3    | 480 GB | 6       | 565   | 0     | 1.55   |
| OCZ       | REVODRIVE3         | 64 GB  | 4       | 564   | 0     | 1.55   |
| PNY       | SSD2SC480G1CS27... | 480 GB | 4       | 564   | 0     | 1.55   |
| SanDisk   | SD8SN8U256G1122    | 256 GB | 3       | 562   | 0     | 1.54   |
| Samsung   | MZ7PC128HAFU-000H1 | 128 GB | 5       | 559   | 0     | 1.53   |
| Samsung   | MZMPC128HBFU-000L1 | 128 GB | 1       | 559   | 0     | 1.53   |
| Patriot   | Torch LE           | 240 GB | 1       | 558   | 0     | 1.53   |
| Transcend | TS128GSSD340       | 128 GB | 8       | 605   | 126   | 1.53   |
| OCZ       | VERTEX2 3.5        | 120 GB | 3       | 734   | 1     | 1.52   |
| Samsung   | MZ7PD256HCGM-000H7 | 256 GB | 13      | 569   | 188   | 1.52   |
| Samsung   | MZNLF128HCHP-00000 | 128 GB | 8       | 554   | 0     | 1.52   |
| Samsung   | SG9MSM6D024GPM00   | 22 GB  | 5       | 551   | 0     | 1.51   |
| ADATA     | SSD SP900 256GB... | 256 GB | 1       | 550   | 0     | 1.51   |
| Intel     | SSDSC2CT180A3      | 180 GB | 7       | 548   | 0     | 1.50   |
| SK hynix  | HFS512G32MND-3210A | 512 GB | 1       | 547   | 0     | 1.50   |
| SanDisk   | SD8SB8U-256G-1006  | 256 GB | 2       | 546   | 0     | 1.50   |
| Toshiba   | THNSFJ256GDNU A    | 256 GB | 4       | 545   | 0     | 1.50   |
| Plextor   | PX-512M7VC         | 512 GB | 2       | 544   | 0     | 1.49   |
| OCZ       | VERTEX2            | 240 GB | 1       | 544   | 0     | 1.49   |
| Samsung   | MMCRE64G8MPP-0VA   | 64 GB  | 1       | 544   | 0     | 1.49   |
| Samsung   | MZNTD256HAGL-000L9 | 256 GB | 2       | 541   | 0     | 1.48   |
| Toshiba   | VT180              | 480 GB | 3       | 747   | 1     | 1.47   |
| Toshiba   | Q300 Pro           | 128 GB | 2       | 537   | 0     | 1.47   |
| Samsung   | SSD 850 PRO        | 256 GB | 118     | 548   | 1     | 1.47   |
| Phison    | SM280128GPTC15T... | 128 GB | 1       | 535   | 0     | 1.47   |
| Samsung   | SSD 840 EVO 250... | 250 GB | 7       | 530   | 0     | 1.45   |
| Lite-On   | LCH-256V2S-HP      | 256 GB | 1       | 530   | 0     | 1.45   |
| Smartbuy  | SSD                | 90 GB  | 1       | 530   | 0     | 1.45   |
| Samsung   | MZ7LN256HMJP-000H1 | 256 GB | 5       | 530   | 0     | 1.45   |
| Samsung   | MZMTD256HAGM-00004 | 256 GB | 1       | 529   | 0     | 1.45   |
| HP        | VK000240GWJPD      | 240 GB | 1       | 529   | 0     | 1.45   |
| SanDisk   | SD6SB2M128G1022I   | 128 GB | 2       | 528   | 0     | 1.45   |
| Samsung   | MZNLN512HCJH-000H1 | 512 GB | 4       | 526   | 0     | 1.44   |
| Intel     | SSDSA2CW120G3      | 120 GB | 10      | 526   | 0     | 1.44   |
| SanDisk   | SD6SP1M128G1002    | 128 GB | 3       | 524   | 0     | 1.44   |
| Goodram   | C100               | 120 GB | 2       | 523   | 0     | 1.44   |
| OCZ       | TRION150           | 480 GB | 4       | 521   | 0     | 1.43   |
| Samsung   | MZ7PC128HAFU-000   | 128 GB | 3       | 521   | 0     | 1.43   |
| Samsung   | MZRPA256HMDR-000SO | 128 GB | 2       | 520   | 0     | 1.43   |
| Intel     | SSDSC2CT240A4      | 240 GB | 9       | 555   | 1     | 1.42   |
| OCZ       | VERTEX3            | 64 GB  | 30      | 576   | 1     | 1.42   |
| AFOX      | SSD                | 120 GB | 1       | 518   | 0     | 1.42   |
| Intel     | SSDSC2BB240G7      | 240 GB | 4       | 516   | 0     | 1.42   |
| SanDisk   | SD8SB8U512G1122    | 512 GB | 7       | 516   | 0     | 1.42   |
| Kingston  | RBUSNS8280S3128GH2 | 128 GB | 3       | 515   | 0     | 1.41   |
| Radeon    | R7                 | 120 GB | 3       | 514   | 0     | 1.41   |
| SanDisk   | SD7UB2Q512G1122    | 512 GB | 2       | 514   | 0     | 1.41   |
| Kingston  | SEDC400S37960G     | 960 GB | 1       | 513   | 0     | 1.41   |
| Samsung   | SSD 850 EVO        | 120 GB | 90      | 512   | 0     | 1.41   |
| SK hynix  | SC308 SATA         | 512 GB | 3       | 689   | 36    | 1.40   |
| ADATA     | SSD S599           | 115 GB | 1       | 511   | 0     | 1.40   |
| SanDisk   | SD8SBBU480G1122    | 480 GB | 2       | 511   | 0     | 1.40   |
| Toshiba   | TL100              | 120 GB | 1       | 509   | 0     | 1.40   |
| Samsung   | MZ7TE512HMHP-000L1 | 512 GB | 1       | 509   | 0     | 1.39   |
| OCZ       | VERTEX4            | 128 GB | 73      | 574   | 1     | 1.39   |
| Samsung   | MZ7PA128HMCD-010L1 | 128 GB | 1       | 504   | 0     | 1.38   |
| Verbatim  | SATA-III SSD       | 256 GB | 1       | 503   | 0     | 1.38   |
| OCZ       | D2RSTK251E14-0400  | 400 GB | 1       | 502   | 0     | 1.38   |
| Corsair   | Force GT           | 90 GB  | 4       | 610   | 1     | 1.36   |
| Toshiba   | THNSFJ256GCSU      | 256 GB | 11      | 505   | 1     | 1.36   |
| Samsung   | SSD PM830 mSATA    | 32 GB  | 10      | 495   | 0     | 1.36   |
| Samsung   | SSD 750 EVO        | 500 GB | 20      | 495   | 0     | 1.36   |
| OCZ       | VERTEX460A         | 240 GB | 3       | 494   | 0     | 1.35   |
| Transcend | TS128GSSD320       | 128 GB | 1       | 493   | 0     | 1.35   |
| Samsung   | SSD 850 EVO        | 500 GB | 352     | 493   | 1     | 1.35   |
| Crucial   | CT256MX100SSD1     | 256 GB | 38      | 522   | 13    | 1.35   |
| Toshiba   | FujiFilm           | 128 GB | 1       | 491   | 0     | 1.35   |
| SanDisk   | SDSSDHII960G       | 960 GB | 2       | 491   | 0     | 1.35   |
| SanDisk   | SDSSDHP256G        | 256 GB | 20      | 487   | 0     | 1.33   |
| OCZ       | VERTEX3            | 120 GB | 56      | 710   | 44    | 1.33   |
| Samsung   | MZMPC032HBCD-000L1 | 32 GB  | 3       | 485   | 0     | 1.33   |
| Samsung   | SSD 850 EVO mSATA  | 120 GB | 5       | 485   | 0     | 1.33   |
| Kingston  | SH103S3120G        | 120 GB | 67      | 526   | 1     | 1.33   |
| SPCC      | SSD110             | 64 GB  | 4       | 482   | 0     | 1.32   |
| Goodram   | SSD                | 64 GB  | 1       | 480   | 0     | 1.32   |
| Samsung   | MZ7TE128HMGR-000L1 | 128 GB | 6       | 480   | 0     | 1.32   |
| Samsung   | MZ7LN512HAJQ-00000 | 512 GB | 7       | 480   | 0     | 1.32   |
| Intel     | SSDSC2CT120A3      | 120 GB | 21      | 835   | 2     | 1.32   |
| Samsung   | MZMPC032HBCD-00000 | 32 GB  | 7       | 479   | 0     | 1.31   |
| Samsung   | MZNLN256HMHQ-00000 | 256 GB | 6       | 479   | 0     | 1.31   |
| Toshiba   | Q300 Pro           | 256 GB | 2       | 478   | 0     | 1.31   |
| PNY       | CS1311 240GB SSD   | 240 GB | 11      | 478   | 0     | 1.31   |
| OCZ       | AGILITY3           | 240 GB | 12      | 667   | 32    | 1.31   |
| Samsung   | MZNLF128HCHP-00004 | 128 GB | 13      | 476   | 0     | 1.31   |
| Kingston  | SVP200S37A60G      | 64 GB  | 12      | 475   | 0     | 1.30   |
| Intel     | SSDSC2MH120A2      | 120 GB | 4       | 474   | 0     | 1.30   |
| SanDisk   | SD8SBBU240G1122    | 240 GB | 2       | 474   | 0     | 1.30   |
| Kingston  | RBU-SNS8100S3256GD | 256 GB | 3       | 473   | 0     | 1.30   |
| Samsung   | MZMTD512HAGL-000MV | 512 GB | 1       | 473   | 0     | 1.30   |
| SanDisk   | SDSSDH240GG25      | 240 GB | 1       | 473   | 0     | 1.30   |
| OCZ       | AGILITY2           | 64 GB  | 3       | 472   | 0     | 1.29   |
| Toshiba   | THNSNJ128G8NU      | 128 GB | 6       | 471   | 0     | 1.29   |
| Goodram   | C40                | 120 GB | 4       | 471   | 0     | 1.29   |
| KingSpec  | SPK-SF12-M120      | 120 GB | 1       | 468   | 0     | 1.28   |
| Samsung   | SSD PM800 TM       | 128 GB | 1       | 468   | 0     | 1.28   |
| Toshiba   | THNSNH060GCST      | 64 GB  | 1       | 467   | 0     | 1.28   |
| Plextor   | PX-64M2S           | 64 GB  | 2       | 467   | 0     | 1.28   |
| Kingston  | SV200S3128G        | 128 GB | 9       | 617   | 1     | 1.28   |
| OCZ       | VERTEX3            | 240 GB | 12      | 811   | 107   | 1.28   |
| Micron    | 5100_MTFDDAK1T9TBY | 1.9 TB | 3       | 1010  | 110   | 1.28   |
| Indilinx  | IND-S3MP-128G      | 128 GB | 1       | 465   | 0     | 1.27   |
| Toshiba   | THNSNB128GMCJ      | 128 GB | 1       | 464   | 0     | 1.27   |
| Mushkin   | MKNSSDTR128GB-3DL  | 128 GB | 1       | 464   | 0     | 1.27   |
| Samsung   | SSD PM830 mSATA    | 128 GB | 3       | 462   | 0     | 1.27   |
| Transcend | TS32GSSD370        | 32 GB  | 2       | 461   | 0     | 1.26   |
| Kingston  | SMSM150S324G2      | 24 GB  | 3       | 461   | 0     | 1.26   |
| Samsung   | SSD 750 EVO        | 250 GB | 52      | 459   | 0     | 1.26   |
| Toshiba   | THNSNH128GCST      | 128 GB | 3       | 459   | 0     | 1.26   |
| WDC       | WDBNCE2500PNC-WRSN | 250 GB | 1       | 457   | 0     | 1.25   |
| Samsung   | MZ7LF128HCHP-00004 | 128 GB | 2       | 457   | 0     | 1.25   |
| Intel     | SSDSC2BW180A3L     | 180 GB | 10      | 468   | 1     | 1.25   |
| XSTAR     | SSD                | 120 GB | 1       | 455   | 0     | 1.25   |
| WDC       | WDS500G1B0B-00AS40 | 500 GB | 8       | 453   | 0     | 1.24   |
| Plextor   | PX-256M3P          | 256 GB | 1       | 1360  | 2     | 1.24   |
| Intel     | SSDSA2M080G2GC     | 80 GB  | 19      | 1005  | 6     | 1.24   |
| Samsung   | MZ7PC256HAFU-000H1 | 256 GB | 1       | 452   | 0     | 1.24   |
| Crucial   | CT240M500SSD3      | 240 GB | 5       | 514   | 7     | 1.24   |
| Samsung   | MZ7TE128HMGR-00004 | 128 GB | 4       | 450   | 0     | 1.24   |
| Samsung   | SSD 850 EVO        | 250 GB | 432     | 455   | 3     | 1.23   |
| SK hynix  | SC300 M.2 2280     | 256 GB | 5       | 449   | 0     | 1.23   |
| ADATA     | SP900              | 64 GB  | 23      | 492   | 2     | 1.23   |
| Toshiba   | THNSNJ128GCSU      | 128 GB | 10      | 448   | 0     | 1.23   |
| Samsung   | SSD 850 EVO M.2    | 500 GB | 29      | 447   | 0     | 1.23   |
| Kingston  | SH100S3240G        | 240 GB | 3       | 1083  | 2     | 1.23   |
| Crucial   | CT512MX100SSD1     | 512 GB | 19      | 503   | 1     | 1.22   |
| Innodisk  | Corp. DRPS-02GJ... | 2 GB   | 1       | 444   | 0     | 1.22   |
| Foxline   | FLDMMS128G         | 128 GB | 1       | 443   | 0     | 1.22   |
| Kingston  | SH103S3240G        | 240 GB | 21      | 577   | 104   | 1.21   |
| SanDisk   | SDSSDP064G         | 64 GB  | 22      | 465   | 47    | 1.21   |
| ADATA     | SSD                | 32 GB  | 1       | 442   | 0     | 1.21   |
| OCZ       | VERTEX2            | 80 GB  | 1       | 442   | 0     | 1.21   |
| Corsair   | Force GT           | 64 GB  | 5       | 690   | 7     | 1.21   |
| SanDisk   | SD6SB1M128G        | 128 GB | 2       | 442   | 0     | 1.21   |
| SanDisk   | SD7SB3Q-256G-1006  | 256 GB | 4       | 440   | 0     | 1.21   |
| Samsung   | SSD 850 EVO        | 1 TB   | 89      | 510   | 7     | 1.21   |
| Intel     | SSDSA2M040G2GC     | 40 GB  | 6       | 781   | 3     | 1.20   |
| Samsung   | MZYTN512HDJH-000L2 | 512 GB | 2       | 437   | 0     | 1.20   |
| Crucial   | CT500MX200SSD1     | 500 GB | 18      | 437   | 0     | 1.20   |
| OCZ       | REVODRIVE X2       | 25 GB  | 4       | 435   | 0     | 1.19   |
| Kingston  | RBU-SC152S37256GG2 | 256 GB | 1       | 435   | 0     | 1.19   |
| Phison    | SSDS30256XQC800... | 240 GB | 1       | 433   | 0     | 1.19   |
| Patriot   | Blaze              | 240 GB | 3       | 432   | 0     | 1.18   |
| Apple     | SSD TS128A         | 121 GB | 1       | 431   | 0     | 1.18   |
| ADATA     | SSD S511           | 120 GB | 1       | 430   | 0     | 1.18   |
| Samsung   | MMCQE28G8MUP-0VA   | 128 GB | 3       | 658   | 1     | 1.18   |
| China     | 256GB SATA SSD     | 256 GB | 1       | 429   | 0     | 1.18   |
| Samsung   | SMART SSD Xceed... | 32 GB  | 3       | 429   | 0     | 1.18   |
| Samsung   | MZRPC128HACD-000SO | 64 GB  | 2       | 429   | 0     | 1.18   |
| Samsung   | MZ7LM480HCHP-00... | 480 GB | 2       | 427   | 0     | 1.17   |
| ADATA     | SSD S396           | 32 GB  | 2       | 427   | 0     | 1.17   |
| Toshiba   | THNS128GG4BBAA     | 128 GB | 1       | 427   | 0     | 1.17   |
| Toshiba   | THNSNF128GCSS      | 128 GB | 3       | 427   | 0     | 1.17   |
| ADATA     | AXM13S2-24GM-B     | 24 GB  | 2       | 740   | 510   | 1.17   |
| PNY       | CS1311 120GB SSD   | 120 GB | 4       | 425   | 0     | 1.17   |
| Samsung   | MZ7LN256HCHP-000F0 | 256 GB | 1       | 425   | 0     | 1.16   |
| SanDisk   | Ultra II           | 960 GB | 15      | 462   | 1     | 1.16   |
| Transcend | TS480GJDM725       | 480 GB | 1       | 424   | 0     | 1.16   |
| Toshiba   | THNSNJ256GVNU      | 256 GB | 2       | 423   | 0     | 1.16   |
| Kingston  | SS200S330G         | 32 GB  | 3       | 423   | 0     | 1.16   |
| SanDisk   | SD6SB2M-512G-1006  | 512 GB | 3       | 423   | 0     | 1.16   |
| Axiom     | Signature III S... | 64 GB  | 1       | 422   | 0     | 1.16   |
| Samsung   | MZMPC128HBFU-00000 | 128 GB | 3       | 422   | 0     | 1.16   |
| Toshiba   | THNSNJ256GCST      | 256 GB | 1       | 421   | 0     | 1.15   |
| Samsung   | MZ7LM480HCHP-00... | 480 GB | 2       | 421   | 0     | 1.15   |
| Toshiba   | THNSNX032GMCT      | 32 GB  | 2       | 421   | 0     | 1.15   |
| SanDisk   | SDSSDXPS240G       | 240 GB | 10      | 423   | 104   | 1.15   |
| Kingston  | SKC380S360G        | 64 GB  | 1       | 420   | 0     | 1.15   |
| SanDisk   | SDSSDH2256G        | 256 GB | 2       | 417   | 0     | 1.14   |
| Toshiba   | THNSNC128GMLJ      | 128 GB | 1       | 416   | 0     | 1.14   |
| PNY       | SSD2SC480G1CS27... | 480 GB | 1       | 415   | 0     | 1.14   |
| Kingston  | SUV400S37960G      | 960 GB | 1       | 415   | 0     | 1.14   |
| Samsung   | MZYTY256HDHP-000L2 | 256 GB | 5       | 414   | 0     | 1.14   |
| SPCC      | SSD110             | 120 GB | 7       | 645   | 291   | 1.13   |
| Toshiba   | THNSNJ256GCSU      | 256 GB | 7       | 414   | 0     | 1.13   |
| Intel     | SSDMAEMC040G2      | 40 GB  | 1       | 414   | 0     | 1.13   |
| SanDisk   | SD6SF1M256G1022    | 256 GB | 2       | 413   | 0     | 1.13   |
| Toshiba   | THNSNJ256GMCU      | 256 GB | 2       | 413   | 0     | 1.13   |
| Hoodisk   | SSD                | 16 GB  | 2       | 412   | 0     | 1.13   |
| Samsung   | MZ7TD128HAFV-000L1 | 128 GB | 11      | 412   | 0     | 1.13   |
| Toshiba   | Q300 Pro           | 512 GB | 1       | 411   | 0     | 1.13   |
| SK hynix  | SC300 SATA         | 512 GB | 2       | 411   | 0     | 1.13   |
| SanDisk   | PLUS               | 480 GB | 4       | 410   | 0     | 1.13   |
| Kingston  | SM2280S3240G       | 240 GB | 2       | 410   | 0     | 1.13   |
| Samsung   | MMCRE28G5MXP-0VBH1 | 128 GB | 1       | 410   | 0     | 1.12   |
| Kingston  | SM2280S3G2120G     | 120 GB | 11      | 409   | 0     | 1.12   |
| SanDisk   | SD7TB3Q-256G-1006  | 256 GB | 6       | 408   | 0     | 1.12   |
| Micron    | 1100_MTFDDAK512TBN | 512 GB | 14      | 616   | 80    | 1.12   |
| WDC       | WDS200T2B0B-00YS70 | 2 TB   | 3       | 406   | 0     | 1.11   |
| Transcend | TS64GMTS400S       | 64 GB  | 2       | 405   | 0     | 1.11   |
| SanDisk   | SD7SN6S-512G-1006  | 512 GB | 4       | 405   | 0     | 1.11   |
| Intel     | SSDSC2BW180A3H     | 180 GB | 10      | 429   | 1     | 1.11   |
| Kingston  | SVP200S37A120G     | 120 GB | 10      | 695   | 173   | 1.11   |
| Kingston  | SVP200S3240G       | 240 GB | 3       | 404   | 0     | 1.11   |
| Samsung   | SSD 850 EVO mSATA  | 500 GB | 15      | 404   | 0     | 1.11   |
| SanDisk   | SDSSDHP128G        | 128 GB | 33      | 410   | 1     | 1.11   |
| OCZ       | VERTEX3            | 128 GB | 2       | 402   | 0     | 1.10   |
| SanDisk   | SDSSDXP240G        | 240 GB | 6       | 402   | 0     | 1.10   |
| KingSpec  | MT-512             | 512 GB | 1       | 401   | 0     | 1.10   |
| Micron    | C400-MTFDDAT128MAM | 128 GB | 2       | 439   | 1034  | 1.10   |
| Toshiba   | THNSNH060GBST      | 64 GB  | 2       | 400   | 0     | 1.10   |
| Smartbuy  | SSD                | 64 GB  | 7       | 399   | 0     | 1.09   |
| Mushkin   | MKNSSDTR480GB-3DL  | 480 GB | 1       | 398   | 0     | 1.09   |
| OCZ       | SOLID3             | 120 GB | 2       | 397   | 0     | 1.09   |
| Kingston  | SV300S37A60G       | 64 GB  | 133     | 405   | 1     | 1.09   |
| WDC       | WDS250G1B0B-00AS40 | 250 GB | 6       | 395   | 0     | 1.08   |
| Plextor   | PH6-CE480-L2       | 480 GB | 2       | 395   | 0     | 1.08   |
| Palit     | PSP120 SSD         | 120 GB | 2       | 394   | 0     | 1.08   |
| Goodram   | SSD                | 240 GB | 11      | 393   | 0     | 1.08   |
| Patriot   | Blast              | 240 GB | 7       | 392   | 0     | 1.08   |
| Micron    | MTFDDAT128MAM-1J2  | 128 GB | 2       | 450   | 548   | 1.07   |
| Samsung   | MZNLN512HMJP-00000 | 512 GB | 1       | 391   | 0     | 1.07   |
| Kingston  | SV100S232G         | 32 GB  | 4       | 390   | 0     | 1.07   |
| Kingston  | SUV300S37A480G     | 480 GB | 2       | 389   | 0     | 1.07   |
| Micron    | MTFDDAK512MBF-1... | 512 GB | 4       | 483   | 4     | 1.07   |
| OCZ       | AGILITY3           | 128 GB | 3       | 749   | 1     | 1.07   |
| Crucial   | CT1050MX300SSD1    | 1 TB   | 20      | 513   | 9     | 1.07   |
| Toshiba   | TR150              | 240 GB | 18      | 388   | 0     | 1.06   |
| Samsung   | MZ7LN128HCHP-000L1 | 128 GB | 5       | 387   | 0     | 1.06   |
| SanDisk   | SD6SB1M256G1002    | 256 GB | 3       | 386   | 0     | 1.06   |
| OCZ       | ARC100             | 240 GB | 12      | 419   | 1     | 1.06   |
| SanDisk   | SDSSDX120GG25      | 120 GB | 8       | 385   | 0     | 1.06   |
| SanDisk   | Ultra II           | 480 GB | 15      | 385   | 0     | 1.06   |
| Samsung   | SSD 850 EVO mSATA  | 250 GB | 12      | 384   | 0     | 1.05   |
| Lite-On   | LAT-128M2S         | 128 GB | 1       | 384   | 0     | 1.05   |
| OCZ       | VERTEX4            | 64 GB  | 9       | 433   | 1     | 1.05   |
| Samsung   | SSD 840 Series     | 120 GB | 37      | 435   | 1     | 1.05   |
| Samsung   | MMCRE28GFMXP-MVB   | 128 GB | 2       | 383   | 0     | 1.05   |
| Toshiba   | THNSNH128GBST      | 128 GB | 4       | 756   | 162   | 1.05   |
| Kingston  | SKC400S37256G      | 256 GB | 3       | 382   | 0     | 1.05   |
| Vaseky    | V800-60G           | 64 GB  | 1       | 381   | 0     | 1.05   |
| Samsung   | SSD PM800 TM       | 64 GB  | 3       | 381   | 0     | 1.05   |
| HP        | SSD S700           | 120 GB | 3       | 545   | 1     | 1.04   |
| Intel     | SSDSC2BB480G6      | 480 GB | 1       | 381   | 0     | 1.04   |
| Kingston  | SM2280S3G2240G     | 240 GB | 2       | 380   | 0     | 1.04   |
| Samsung   | SATA SSD           | 256 GB | 1       | 379   | 0     | 1.04   |
| OCZ       | VERTEX3            | 90 GB  | 12      | 669   | 7     | 1.04   |
| Seagate   | STT_FTM64GX25H     | 64 GB  | 1       | 378   | 0     | 1.04   |
| Corsair   | Force 3 SSD        | 90 GB  | 5       | 378   | 0     | 1.04   |
| Samsung   | MZ7TY256HDHP-000L7 | 256 GB | 6       | 377   | 0     | 1.03   |
| Samsung   | MZNTY128HDHP-000H1 | 128 GB | 9       | 377   | 0     | 1.03   |
| OCZ       | TRION100           | 480 GB | 1       | 375   | 0     | 1.03   |
| SanDisk   | SD7SB6S-128G-1006  | 128 GB | 3       | 573   | 2     | 1.03   |
| Toshiba   | THNSNF256GRHS      | 128 GB | 2       | 375   | 0     | 1.03   |
| Samsung   | SSD 850 EVO mSATA  | 1 TB   | 4       | 374   | 0     | 1.03   |
| Crucial   | CT960M500SSD1      | 960 GB | 11      | 695   | 193   | 1.02   |
| OCZ       | REVODRIVE3         | 120 GB | 2       | 373   | 0     | 1.02   |
| SanDisk   | SD8SN8U512G1122    | 512 GB | 4       | 372   | 0     | 1.02   |
| OCZ       | TRION100           | 240 GB | 10      | 404   | 1     | 1.02   |
| OCZ       | VERTEX2            | 115 GB | 2       | 370   | 0     | 1.02   |
| Samsung   | SSD SM871 2.5 7mm  | 512 GB | 3       | 920   | 104   | 1.01   |
| Intel     | SSDSC2BW240A3H     | 240 GB | 1       | 369   | 0     | 1.01   |
| Toshiba   | THNS064GE4BBDC     | 64 GB  | 2       | 369   | 0     | 1.01   |
| OCZ       | VERTEX3 MI         | 120 GB | 16      | 526   | 126   | 1.01   |
| SanDisk   | SD6SB1M128G1022I   | 128 GB | 6       | 368   | 0     | 1.01   |
| Toshiba   | THNSNH512GCST      | 512 GB | 2       | 367   | 0     | 1.01   |
| Apple     | SSD SM0512G        | 500 GB | 7       | 367   | 0     | 1.01   |
| SanDisk   | SD7SN3Q256G1002    | 256 GB | 3       | 417   | 344   | 1.00   |
| Crucial   | CT512M550SSD1      | 512 GB | 6       | 660   | 183   | 1.00   |
| Kingston  | SNV425S2128GB      | 128 GB | 2       | 1079  | 4     | 1.00   |
| Corsair   | Force GS           | 128 GB | 18      | 365   | 0     | 1.00   |
| Plextor   | PX-64M3            | 64 GB  | 3       | 668   | 346   | 1.00   |
| Crucial   | CT128M550SSD3      | 128 GB | 4       | 469   | 8     | 1.00   |
| SanDisk   | SSD PLUS 480 GB    | 480 GB | 9       | 406   | 7     | 0.99   |
| Micron    | 5200_MTFDDAK240TDN | 240 GB | 10      | 362   | 0     | 0.99   |
| Goodram   | IRP-SSDPR-S25B-240 | 240 GB | 1       | 359   | 0     | 0.99   |
| KingShare | 230120SSD          | 128 GB | 1       | 358   | 0     | 0.98   |
| Intel     | SSDSC2CW480A3      | 480 GB | 4       | 357   | 0     | 0.98   |
| ADATA     | SP310              | 128 GB | 2       | 355   | 0     | 0.97   |
| Samsung   | MZ7LN512HCHP-000L1 | 512 GB | 8       | 355   | 0     | 0.97   |
| Samsung   | MZMPC128HBFU-000H1 | 128 GB | 2       | 354   | 0     | 0.97   |
| CFD       | CSSD-MG4VT         | 1 TB   | 1       | 354   | 0     | 0.97   |
| KingSpec  | KSD-SA25.5-016MJ   | 16 GB  | 1       | 353   | 0     | 0.97   |
| Samsung   | SSD 650            | 120 GB | 5       | 353   | 0     | 0.97   |
| SanDisk   | Ultra II           | 240 GB | 19      | 382   | 1     | 0.97   |
| Micron    | 1100_MTFDDAK256TBN | 256 GB | 15      | 407   | 75    | 0.97   |
| Samsung   | MZNLN128HCGR-000L2 | 128 GB | 3       | 352   | 0     | 0.96   |
| SK hynix  | SC300 SATA         | 256 GB | 1       | 351   | 0     | 0.96   |
| Kingston  | RBU-SC100S37128GD  | 128 GB | 2       | 351   | 0     | 0.96   |
| KingDian  | N480-240GB         | 240 GB | 1       | 351   | 0     | 0.96   |
| Intel     | SSDSC2BW240A4      | 240 GB | 26      | 588   | 2     | 0.96   |
| Crucial   | CT128M550SSD4      | 128 GB | 1       | 349   | 0     | 0.96   |
| Intel     | SSDSA2M160G2GC     | 160 GB | 3       | 656   | 4     | 0.96   |
| SanDisk   | SDSSDH31000G       | 1 TB   | 10      | 349   | 0     | 0.96   |
| Kingston  | SHSS37A240G        | 240 GB | 32      | 361   | 1     | 0.95   |
| Intel     | SSDSC2CT240A3      | 240 GB | 3       | 622   | 1     | 0.95   |
| Plextor   | PX-128M3           | 128 GB | 4       | 393   | 454   | 0.95   |
| Toshiba   | THNSNX024GMNT      | 24 GB  | 2       | 346   | 0     | 0.95   |
| Samsung   | SSD 840 EVO        | 752 GB | 3       | 345   | 0     | 0.95   |
| Corsair   | Force LE200 SSD    | 240 GB | 5       | 345   | 0     | 0.95   |
| Advantech | SQF-S25M4-32G-S9E  | 32 GB  | 1       | 345   | 0     | 0.95   |
| Vaseky    | v800-128G          | 128 GB | 1       | 344   | 0     | 0.94   |
| Samsung   | SSD 850 EVO M.2    | 250 GB | 25      | 344   | 0     | 0.94   |
| Plextor   | PH6-CE120-G        | 120 GB | 3       | 344   | 0     | 0.94   |
| Intel     | SSDSC2BA400G4      | 400 GB | 3       | 344   | 0     | 0.94   |
| SanDisk   | SD6SF1M128G1022I   | 128 GB | 2       | 446   | 1     | 0.94   |
| Crucial   | CT275MX300SSD1     | 275 GB | 46      | 372   | 35    | 0.94   |
| Micron    | C400-MTFDDAK256MAM | 256 GB | 3       | 417   | 674   | 0.94   |
| Kingston  | SV100S264G         | 64 GB  | 11      | 538   | 5     | 0.94   |
| SanDisk   | SDSSDHII120G       | 120 GB | 29      | 341   | 0     | 0.94   |
| Samsung   | MZNLN256HCHP-000L7 | 256 GB | 9       | 340   | 0     | 0.93   |
| Intel     | SSDSCKJW120H6      | 120 GB | 1       | 339   | 0     | 0.93   |
| Samsung   | MZNTY256HDHP-000H1 | 256 GB | 5       | 366   | 1     | 0.93   |
| SanDisk   | SDSSDP128G         | 128 GB | 45      | 376   | 7     | 0.93   |
| SanDisk   | X400 2.5 7MM       | 256 GB | 2       | 339   | 0     | 0.93   |
| Samsung   | MZNTE256HMHP-000H1 | 256 GB | 2       | 338   | 0     | 0.93   |
| Samsung   | MZMTE512HMHP-000L1 | 512 GB | 1       | 338   | 0     | 0.93   |
| Transcend | TSA                | 480 GB | 1       | 337   | 0     | 0.93   |
| SPCC      | SSD                | 480 GB | 2       | 337   | 0     | 0.92   |
| SanDisk   | SD8TB8U256G1001    | 256 GB | 6       | 337   | 0     | 0.92   |
| SanDisk   | SSD i100           | 32 GB  | 5       | 336   | 0     | 0.92   |
| Corsair   | Neutron XT SSD     | 480 GB | 3       | 561   | 2     | 0.92   |
| Plextor   | PX-512M6S+         | 512 GB | 1       | 336   | 0     | 0.92   |
| SanDisk   | X400 M.2 2280      | 512 GB | 2       | 335   | 0     | 0.92   |
| SanDisk   | SDSSDX240GG25      | 240 GB | 4       | 1027  | 8     | 0.91   |
| Intel     | SSDSC2BW080A4      | 80 GB  | 4       | 333   | 0     | 0.91   |
| Samsung   | MZMTE512HMHP-000MV | 512 GB | 1       | 333   | 0     | 0.91   |
| SK hynix  | SC300 M.2 2280     | 512 GB | 1       | 333   | 0     | 0.91   |
| Micron    | M600_MTFDDAV256MBF | 256 GB | 7       | 332   | 0     | 0.91   |
| OCZ       | VECTOR150          | 240 GB | 7       | 363   | 1     | 0.91   |
| Team      | TEAML5Lite3D120G   | 120 GB | 5       | 332   | 0     | 0.91   |
| KingFast  | SSD                | 32 GB  | 1       | 332   | 0     | 0.91   |
| Team      | L3 SSD             | 120 GB | 3       | 331   | 0     | 0.91   |
| OCZ       | VERTEX PLUS R2     | 128 GB | 2       | 331   | 0     | 0.91   |
| Apple     | SSD SM0256G        | 256 GB | 12      | 331   | 0     | 0.91   |
| Kingston  | RBUSNS4180S364GJ   | 64 GB  | 1       | 330   | 0     | 0.90   |
| Crucial   | CT240M500SSD1      | 240 GB | 31      | 569   | 76    | 0.90   |
| OCZ       | AGILITY3           | 90 GB  | 4       | 471   | 1     | 0.90   |
| China     | SH00R480GB         | 480 GB | 4       | 328   | 0     | 0.90   |
| ZOTAC     | ZTSSD-S11-240G-P   | 240 GB | 1       | 328   | 0     | 0.90   |
| Samsung   | MZMTE256HMHP-00000 | 256 GB | 2       | 328   | 0     | 0.90   |
| Mushkin   | MKNSSDCR240GB-7    | 240 GB | 1       | 326   | 0     | 0.89   |
| Seagate   | SSD                | 1 TB   | 3       | 325   | 0     | 0.89   |
| Toshiba   | Q300               | 480 GB | 5       | 325   | 0     | 0.89   |
| Kingston  | SV300S37A120G      | 120 GB | 462     | 399   | 18    | 0.89   |
| OCZ       | VERTEX             | 64 GB  | 2       | 324   | 0     | 0.89   |
| KingFast  | SSD                | 64 GB  | 4       | 324   | 1     | 0.89   |
| Patriot   | Blaze              | 64 GB  | 6       | 324   | 0     | 0.89   |
| Corsair   | Force GS           | 240 GB | 5       | 1343  | 25    | 0.89   |
| Micron    | M600_MTFDDAY512MBF | 512 GB | 1       | 323   | 0     | 0.89   |
| SanDisk   | SD6SF1M128G1022    | 128 GB | 1       | 323   | 0     | 0.89   |
| Kingston  | RBU-SNS8152S325... | 256 GB | 1       | 323   | 0     | 0.89   |
| Corsair   | Force LE SSD       | 120 GB | 3       | 321   | 0     | 0.88   |
| Samsung   | MZMPC128HBFU-000MV | 128 GB | 3       | 321   | 0     | 0.88   |
| OCZ       | VERTEX3 LP         | 64 GB  | 1       | 320   | 0     | 0.88   |
| Team      | TIM3F49256GMBA04MA | 256 GB | 1       | 320   | 0     | 0.88   |
| Samsung   | MZNTY256HDHP-000   | 256 GB | 1       | 319   | 0     | 0.87   |
| SanDisk   | SDSSDHP064G        | 64 GB  | 8       | 318   | 0     | 0.87   |
| Intel     | SSDSC2BB012T7O     | 1.2 TB | 1       | 317   | 0     | 0.87   |
| Team      | TEAML5Lite3D1T     | 1 TB   | 3       | 317   | 0     | 0.87   |
| SanDisk   | SSD i110           | 64 GB  | 1       | 317   | 0     | 0.87   |
| Zheino    | CHN 25SATAA3 360   | 360 GB | 1       | 316   | 0     | 0.87   |
| ADATA     | SP900              | 128 GB | 39      | 386   | 10    | 0.87   |
| SanDisk   | SDSSDA960G         | 960 GB | 4       | 316   | 0     | 0.87   |
| Samsung   | MMCRE28G8MXP-0VBL1 | 128 GB | 3       | 315   | 0     | 0.87   |
| Samsung   | SSD PM810 FDE 2.5" | 256 GB | 2       | 403   | 129   | 0.87   |
| Toshiba   | THNSNJ512G8NY      | 512 GB | 1       | 315   | 0     | 0.86   |
| Kingston  | SMS200S3120G       | 120 GB | 18      | 333   | 43    | 0.86   |
| Crucial   | CT1050MX300SSD4    | 1 TB   | 7       | 328   | 11    | 0.86   |
| Netac     | SSD                | 120 GB | 1       | 314   | 0     | 0.86   |
| SanDisk   | X400 M.2 2280      | 256 GB | 14      | 314   | 0     | 0.86   |
| Intenso   | SATA III SSD       | 120 GB | 14      | 312   | 0     | 0.86   |
| Samsung   | SSD PM810 2.5"     | 128 GB | 1       | 1560  | 4     | 0.86   |
| SanDisk   | SSD U100           | 128 GB | 1       | 312   | 0     | 0.86   |
| Micron    | MTFDDAV512TBN-1... | 512 GB | 1       | 620   | 1     | 0.85   |
| Intel     | SSDSCKGF180A4H     | 180 GB | 1       | 309   | 0     | 0.85   |
| ADATA     | SP900              | 256 GB | 14      | 383   | 1     | 0.85   |
| SanDisk   | SD7SB7S512G1001    | 512 GB | 2       | 308   | 0     | 0.84   |
| Samsung   | MZHPV256HDGL-000L1 | 256 GB | 2       | 308   | 0     | 0.84   |
| Kingston  | SM2280S3120G       | 120 GB | 4       | 307   | 0     | 0.84   |
| Crucial   | C300-CTFDDAC064MAG | 64 GB  | 1       | 307   | 0     | 0.84   |
| Samsung   | MZMPC032HBCD-000H1 | 32 GB  | 10      | 307   | 0     | 0.84   |
| SanDisk   | SDSSDHII240G       | 240 GB | 24      | 326   | 2     | 0.84   |
| Samsung   | MZ7TE128HMGR-00000 | 128 GB | 3       | 305   | 0     | 0.84   |
| Kingston  | SV300S37A240G      | 240 GB | 132     | 339   | 8     | 0.84   |
| AMD       | R5SL480G           | 480 GB | 1       | 305   | 0     | 0.84   |
| ADATA     | SP600              | 512 GB | 1       | 305   | 0     | 0.84   |
| Samsung   | MZ7TE256HMHP-000H1 | 256 GB | 2       | 305   | 0     | 0.84   |
| Samsung   | SSD 750 EVO        | 120 GB | 43      | 304   | 0     | 0.83   |
| Lite-On   | L8H-128V2G-HP      | 128 GB | 1       | 303   | 0     | 0.83   |
| Kingston  | SUV400S37480G      | 480 GB | 15      | 335   | 91    | 0.83   |
| Toshiba   | THNSNC128GBSJ      | 128 GB | 1       | 303   | 0     | 0.83   |
| Samsung   | MZ7TD128HAFV-00000 | 128 GB | 3       | 303   | 0     | 0.83   |
| SanDisk   | SD8TB8U512G1001    | 512 GB | 2       | 302   | 0     | 0.83   |
| Samsung   | MZ7LN256HCHP-000L7 | 256 GB | 12      | 301   | 0     | 0.83   |
| Mushkin   | MKNSSDAT240GB-DX   | 240 GB | 1       | 299   | 0     | 0.82   |
| Samsung   | MZNLN128HAHQ-00000 | 128 GB | 2       | 299   | 0     | 0.82   |
| ADATA     | SP600              | 32 GB  | 7       | 298   | 0     | 0.82   |
| Samsung   | MZ7LM480HMHQ-000MV | 480 GB | 2       | 298   | 0     | 0.82   |
| Plextor   | PX-256S3G          | 256 GB | 2       | 298   | 0     | 0.82   |
| Crucial   | CT120M500SSD1      | 120 GB | 26      | 712   | 98    | 0.81   |
| SanDisk   | X300 2.5 7MM       | 256 GB | 1       | 297   | 0     | 0.81   |
| Plextor   | PX-128M7VG         | 128 GB | 3       | 297   | 0     | 0.81   |
| Samsung   | MZNLN512HMJP-000L7 | 512 GB | 8       | 297   | 0     | 0.81   |
| SanDisk   | SDSSDP256G         | 256 GB | 10      | 341   | 3     | 0.81   |
| Transcend | TS512GSSD370       | 512 GB | 3       | 296   | 0     | 0.81   |
| ADATA     | SSD S599           | 64 GB  | 2       | 296   | 0     | 0.81   |
| Intenso   | SSD Sata III       | 250 GB | 1       | 295   | 0     | 0.81   |
| Ramaxel   | RDM-II XM020C024G  | 24 GB  | 2       | 295   | 0     | 0.81   |
| Kingston  | SUV400S37240G      | 240 GB | 103     | 328   | 40    | 0.81   |
| Samsung   | MZAPF032HCFV-000H1 | 32 GB  | 1       | 294   | 0     | 0.81   |
| SanDisk   | SSD i100           | 16 GB  | 7       | 312   | 1     | 0.81   |
| Netac     | SSD                | 240 GB | 1       | 294   | 0     | 0.81   |
| Kingston  | SNVP325S2256GB     | 256 GB | 1       | 293   | 0     | 0.80   |
| Samsung   | SSD RBX Series ... | 64 GB  | 1       | 292   | 0     | 0.80   |
| Samsung   | MZNLN128HCGR-00000 | 128 GB | 2       | 292   | 0     | 0.80   |
| Samsung   | MZ7LF120HCHP-000L1 | 120 GB | 4       | 292   | 0     | 0.80   |
| Phison    | 128GB PS3110-S10C  | 128 GB | 1       | 291   | 0     | 0.80   |
| WDC       | WDS100T1B0B-00AS40 | 1 TB   | 3       | 291   | 0     | 0.80   |
| Intel     | SSDSC2BW480A4      | 480 GB | 5       | 577   | 11    | 0.80   |
| Samsung   | MZMPA064HMDR-00000 | 64 GB  | 1       | 290   | 0     | 0.79   |
| Innodisk  | 2.5" SATA SSD 3ME4 | 128 GB | 2       | 289   | 0     | 0.79   |
| Kingston  | RBU-SNS8152S312... | 128 GB | 3       | 288   | 0     | 0.79   |
| Plextor   | PX-256M7VC         | 256 GB | 4       | 288   | 0     | 0.79   |
| Crucial   | CT275MX300SSD4     | 275 GB | 10      | 329   | 1     | 0.79   |
| Micron    | MTFDDAK256MAM-1K1  | 256 GB | 3       | 288   | 0     | 0.79   |
| Samsung   | SSD PM830 2.5" 7mm | 512 GB | 2       | 594   | 505   | 0.79   |
| Kingston  | RBU-SNS8152S325... | 256 GB | 2       | 287   | 0     | 0.79   |
| Intel     | SSDSC2KF256G8      | 256 GB | 1       | 287   | 0     | 0.79   |
| Crucial   | CT750MX300SSD1     | 752 GB | 13      | 287   | 0     | 0.79   |
| OCZ       | CACHE-SYNAPSE      | 32 GB  | 1       | 286   | 0     | 0.79   |
| Samsung   | MZNTY256HDHP-000L7 | 256 GB | 12      | 286   | 0     | 0.78   |
| SanDisk   | SD8SN8U512G1002    | 512 GB | 11      | 285   | 0     | 0.78   |
| OCZ       | VTX3-25SAT3-120G   | 120 GB | 1       | 285   | 0     | 0.78   |
| Toshiba   | TR150              | 120 GB | 5       | 285   | 0     | 0.78   |
| Corsair   | CSSD-V60GB2        | 64 GB  | 2       | 433   | 4     | 0.78   |
| Intel     | SSDMCEAC240B3      | 240 GB | 1       | 284   | 0     | 0.78   |
| Crucial   | CT250MX200SSD1     | 250 GB | 20      | 283   | 0     | 0.78   |
| Apple     | SSD TS128C         | 121 GB | 3       | 283   | 0     | 0.78   |
| Corsair   | CMFSSD-32D1        | 32 GB  | 1       | 566   | 1     | 0.78   |
| SanDisk   | SD6SB1M128G1001    | 128 GB | 3       | 283   | 0     | 0.78   |
| SanDisk   | SDSSDA480G         | 480 GB | 10      | 286   | 1     | 0.78   |
| OCZ       | ARC100             | 120 GB | 12      | 282   | 0     | 0.77   |
| SanDisk   | SD8SBBU120G1122    | 120 GB | 4       | 282   | 0     | 0.77   |
| Samsung   | MZ7TE128HMGR-000H1 | 128 GB | 3       | 281   | 0     | 0.77   |
| Samsung   | MZYLF128HCHP-000L2 | 128 GB | 8       | 280   | 0     | 0.77   |
| Hoodisk   | SSD                | 128 GB | 4       | 279   | 0     | 0.77   |
| Kingston  | SMS100S232G        | 32 GB  | 1       | 279   | 0     | 0.76   |
| Kingston  | SUV300S37A120G     | 120 GB | 36      | 284   | 1     | 0.76   |
| Apacer    | AS330              | 120 GB | 3       | 277   | 0     | 0.76   |
| Plextor   | PX-256M5Pro        | 256 GB | 12      | 277   | 0     | 0.76   |
| Samsung   | SSD PM871a M.2 ... | 512 GB | 1       | 277   | 0     | 0.76   |
| PNY       | CS2211 480GB SSD   | 480 GB | 1       | 277   | 0     | 0.76   |
| Samsung   | MZ7WD960HMHP-00003 | 960 GB | 5       | 610   | 4     | 0.75   |
| ADATA     | SP600NS34          | 256 GB | 1       | 274   | 0     | 0.75   |
| WDC       | WDS100T1B0A-00H9H0 | 1 TB   | 11      | 273   | 0     | 0.75   |
| SanDisk   | SD8SB8U128G1002    | 128 GB | 1       | 273   | 0     | 0.75   |
| WDC       | WDS500G1B0A-00H9H0 | 500 GB | 15      | 293   | 1     | 0.75   |
| Samsung   | MZYTY128HDHP-000L2 | 128 GB | 5       | 273   | 0     | 0.75   |
| MyDigi... | SC2 M2 SSD         | 120 GB | 1       | 271   | 0     | 0.74   |
| SanDisk   | SD7SB2Q-512G-1006  | 512 GB | 4       | 269   | 0     | 0.74   |
| Toshiba   | THNSNH060GMCT      | 64 GB  | 1       | 269   | 0     | 0.74   |
| Samsung   | MZ7LF192HCGS-000L1 | 192 GB | 5       | 268   | 0     | 0.74   |
| Samsung   | SSD 840 EVO 500... | 500 GB | 3       | 268   | 0     | 0.74   |
| Kingston  | SMS200S3240G       | 240 GB | 3       | 591   | 340   | 0.74   |
| SK hynix  | HFS512G39TND-N210A | 512 GB | 4       | 404   | 517   | 0.73   |
| SanDisk   | SDSSDXPS960G       | 960 GB | 5       | 423   | 67    | 0.73   |
| Apple     | SSD TS064C         | 64 GB  | 4       | 265   | 0     | 0.73   |
| China     | SATA SSD           | 1 TB   | 1       | 265   | 0     | 0.73   |
| Samsung   | MZNLN512HMJP-000H1 | 512 GB | 1       | 265   | 0     | 0.73   |
| PNY       | CS900 480GB SSD    | 480 GB | 9       | 265   | 0     | 0.73   |
| Intel     | SSDPAMM0008G1      | 8 GB   | 1       | 265   | 0     | 0.73   |
| SK hynix  | HFS120G32TND-N1A2A | 120 GB | 1       | 264   | 0     | 0.73   |
| imation   | M.2 SATA3 256GB... | 256 GB | 1       | 264   | 0     | 0.73   |
| China     | SATA SSD           | 20 GB  | 13      | 289   | 1     | 0.73   |
| ADATA     | SX900              | 128 GB | 12      | 711   | 514   | 0.72   |
| Kingston  | SKC400S37128G      | 128 GB | 2       | 264   | 0     | 0.72   |
| Kingston  | RBUSNS8180S3128GI  | 128 GB | 3       | 264   | 0     | 0.72   |
| Plextor   | PX-512M8VC         | 512 GB | 1       | 264   | 0     | 0.72   |
| Integral  | V Series SATA SSD  | 120 GB | 1       | 263   | 0     | 0.72   |
| Crucial   | CT525MX300SSD1     | 528 GB | 67      | 339   | 122   | 0.72   |
| OCZ       | VERTEX             | 32 GB  | 2       | 616   | 2     | 0.72   |
| Team      | L5 LITE SSD        | 120 GB | 3       | 263   | 0     | 0.72   |
| SPCC      | SSD                | 2 TB   | 1       | 263   | 0     | 0.72   |
| SanDisk   | SD6SB2M512G1001    | 512 GB | 1       | 262   | 0     | 0.72   |
| Apacer    | A7202              | 64 GB  | 1       | 262   | 0     | 0.72   |
| Samsung   | SSD 860 EVO        | 4 TB   | 18      | 262   | 0     | 0.72   |
| Samsung   | MZNTY256HDHP-00000 | 256 GB | 5       | 261   | 0     | 0.72   |
| OCZ       | ARC100             | 480 GB | 4       | 263   | 1     | 0.72   |
| Pioneer   | APS-SL3N-512       | 512 GB | 3       | 261   | 0     | 0.72   |
| SK hynix  | SC313 HFS256G39... | 256 GB | 1       | 261   | 0     | 0.72   |
| Lite-On   | LCS-256L9S-11 2... | 256 GB | 5       | 260   | 0     | 0.71   |
| Samsung   | MZ7TE256HMHP-000L2 | 256 GB | 1       | 260   | 0     | 0.71   |
| Micron    | C400-MTFDDAC064MAM | 64 GB  | 2       | 259   | 0     | 0.71   |
| WDC       | WDS250G1B0A-00H9H0 | 250 GB | 18      | 309   | 57    | 0.71   |
| SanDisk   | SD5SG2256G1052E    | 256 GB | 5       | 392   | 1     | 0.71   |
| ADATA     | IM2S3138E-128GM-B  | 128 GB | 2       | 257   | 0     | 0.70   |
| Samsung   | SSD PM810 TM       | 64 GB  | 1       | 257   | 0     | 0.70   |
| Team      | T253X1960G         | 960 GB | 1       | 256   | 0     | 0.70   |
| Crucial   | CT500MX200SSD4     | 500 GB | 2       | 255   | 0     | 0.70   |
| Samsung   | MZNTY128HDHP-000L1 | 128 GB | 4       | 255   | 0     | 0.70   |
| Toshiba   | A100               | 240 GB | 9       | 255   | 0     | 0.70   |
| Goodram   | SSDPR-CX400-01T    | 1 TB   | 3       | 254   | 0     | 0.70   |
| SanDisk   | SSD U100           | 128 GB | 7       | 336   | 31    | 0.70   |
| Kingston  | SKC300S37A60G      | 64 GB  | 15      | 349   | 5     | 0.69   |
| Apple     | SSD SD128E         | 121 GB | 3       | 252   | 0     | 0.69   |
| Toshiba   | TL100              | 240 GB | 5       | 252   | 0     | 0.69   |
| OCZ       | VECTOR150          | 120 GB | 10      | 251   | 0     | 0.69   |
| Goodram   | C50                | 120 GB | 3       | 251   | 0     | 0.69   |
| Intel     | SSDSC2BW180A4      | 180 GB | 9       | 486   | 3     | 0.69   |
| Samsung   | SSD PM800 TH       | 64 GB  | 1       | 251   | 0     | 0.69   |
| SanDisk   | SD7SB6S256G1122    | 256 GB | 2       | 251   | 0     | 0.69   |
| TCSUNBOW  | X3                 | 1 TB   | 1       | 250   | 0     | 0.69   |
| Kingston  | SMS200S360G        | 64 GB  | 12      | 460   | 9     | 0.69   |
| Kingston  | RBUSC180DS37128GH  | 128 GB | 1       | 250   | 0     | 0.69   |
| Goodram   | SSD                | 120 GB | 33      | 249   | 0     | 0.68   |
| Intel     | SSDSCKHF240A4L     | 240 GB | 2       | 306   | 554   | 0.68   |
| Samsung   | MZNLN256HCHP-00000 | 256 GB | 7       | 249   | 0     | 0.68   |
| Kingston  | SHPM2280P2H-480G   | 480 GB | 3       | 288   | 1     | 0.68   |
| Samsung   | MZMTD256HAGM-000L1 | 256 GB | 4       | 248   | 0     | 0.68   |
| Samsung   | SSD PM871b 2.5 7mm | 512 GB | 1       | 248   | 0     | 0.68   |
| WDC       | WDS120G1G0B-00RC30 | 120 GB | 13      | 248   | 0     | 0.68   |
| SanDisk   | SD8SN8U256G1002    | 256 GB | 3       | 248   | 0     | 0.68   |
| Samsung   | MZMPA024HMCD-000L1 | 24 GB  | 3       | 284   | 7     | 0.68   |
| Crucial   | CT250MX200SSD3     | 250 GB | 4       | 248   | 0     | 0.68   |
| Apacer    | AST680S            | 128 GB | 2       | 248   | 0     | 0.68   |
| ADATA     | SX930              | 120 GB | 3       | 247   | 0     | 0.68   |
| SanDisk   | Ultra II           | 250 GB | 2       | 247   | 0     | 0.68   |
| Toshiba   | THNSNJ256G8NY      | 256 GB | 7       | 283   | 1     | 0.68   |
| SanDisk   | SD8SN8U-512G-1006  | 512 GB | 2       | 297   | 2     | 0.68   |
| Toshiba   | TR150              | 960 GB | 1       | 246   | 0     | 0.68   |
| SanDisk   | SD7SN6S-256G-1006  | 256 GB | 5       | 246   | 0     | 0.67   |
| Samsung   | MZ7TE256HMHP-000L7 | 256 GB | 5       | 246   | 0     | 0.67   |
| Plextor   | PX-128M7VC         | 128 GB | 5       | 245   | 0     | 0.67   |
| Intel     | SSDSA1MH080G1GN    | 80 GB  | 1       | 244   | 0     | 0.67   |
| SK hynix  | HFS256G39TNH-73A0A | 256 GB | 3       | 245   | 594   | 0.67   |
| Intel     | SSDSC2CW120A3      | 120 GB | 36      | 570   | 424   | 0.67   |
| Kingston  | SUV400S37120G      | 120 GB | 121     | 264   | 58    | 0.67   |
| OCZ       | VECTOR             | 128 GB | 4       | 245   | 4     | 0.67   |
| Kingston  | SA400S37 120G      | 120 GB | 1       | 242   | 0     | 0.66   |
| Samsung   | MZMTD128HAFV-000L1 | 128 GB | 10      | 259   | 15    | 0.66   |
| Phison    | SATA SSD           | 64 GB  | 4       | 241   | 0     | 0.66   |
| Kingston  | RBUSNS8180S3128GI1 | 128 GB | 3       | 241   | 0     | 0.66   |
| SanDisk   | Ultra II           | 500 GB | 2       | 241   | 0     | 0.66   |
| Patriot   | Spark              | 128 GB | 8       | 240   | 0     | 0.66   |
| SanDisk   | SD9SB8W128G1001    | 128 GB | 3       | 240   | 0     | 0.66   |
| WDC       | WDS240G1G0A-00SS50 | 240 GB | 19      | 239   | 0     | 0.66   |
| Samsung   | MZMTE128HMGR-000MV | 128 GB | 3       | 239   | 0     | 0.66   |
| SK hynix  | SC311 SATA         | 512 GB | 14      | 254   | 75    | 0.65   |
| KingFast  | SSD                | 240 GB | 3       | 239   | 0     | 0.65   |
| HP        | VK0240GDJXU        | 240 GB | 1       | 238   | 0     | 0.65   |
| Plextor   | PX-512M5P          | 512 GB | 1       | 238   | 0     | 0.65   |
| Kingston  | SUV300S37A240G     | 240 GB | 13      | 238   | 0     | 0.65   |
| Crucial   | M4-CT128M4SSD3     | 128 GB | 1       | 238   | 0     | 0.65   |
| Kingston  | SHSS37A480G        | 480 GB | 9       | 238   | 0     | 0.65   |
| Samsung   | SSD 860 EVO mSATA  | 1 TB   | 3       | 238   | 0     | 0.65   |
| Intel     | SSDSC2BW240H6      | 240 GB | 12      | 285   | 1     | 0.65   |
| Samsung   | MZMTE256HMHP-000MV | 256 GB | 4       | 237   | 0     | 0.65   |
| Toshiba   | THNSNJ512GDNU A    | 512 GB | 2       | 237   | 0     | 0.65   |
| Kingston  | RBU-SNS8152S312... | 128 GB | 3       | 237   | 0     | 0.65   |
| ADATA     | SX900              | 256 GB | 6       | 451   | 541   | 0.65   |
| HP        | SSD S700 Pro       | 512 GB | 1       | 236   | 0     | 0.65   |
| Samsung   | MZ7LN256HAJQ-000H1 | 256 GB | 1       | 235   | 0     | 0.65   |
| Intel     | SSDSC2BW120A4      | 120 GB | 32      | 279   | 1     | 0.65   |
| OCZ       | VERTEX460A         | 120 GB | 7       | 264   | 1     | 0.64   |
| Verbatim  | SATA-III SSD       | 128 GB | 2       | 279   | 508   | 0.64   |
| Kingston  | SHSS37A120G        | 120 GB | 8       | 234   | 0     | 0.64   |
| China     | SSD                | 64 GB  | 9       | 268   | 1     | 0.64   |
| SK hynix  | SC311 SATA         | 256 GB | 38      | 240   | 1     | 0.64   |
| OCZ       | TRION150           | 240 GB | 5       | 233   | 0     | 0.64   |
| Toshiba   | TR150              | 480 GB | 5       | 354   | 2     | 0.64   |
| WDC       | WDS250G2B0B-00YS70 | 250 GB | 14      | 232   | 0     | 0.64   |
| Intel     | SSDSA2M120G2GC     | 120 GB | 2       | 1424  | 6     | 0.64   |
| Crucial   | CT960BX200SSD1     | 960 GB | 3       | 231   | 0     | 0.63   |
| SanDisk   | Z400s M.2 2280     | 256 GB | 1       | 229   | 0     | 0.63   |
| Toshiba   | THNSNF256GMCS      | 256 GB | 2       | 229   | 0     | 0.63   |
| SK hynix  | SC210 mSATA        | 128 GB | 3       | 307   | 21    | 0.63   |
| SanDisk   | SDSSDXPS480G       | 480 GB | 8       | 618   | 69    | 0.63   |
| Transcend | TS128GMSA340       | 128 GB | 1       | 227   | 0     | 0.62   |
| OCZ       | VERTEX450          | 128 GB | 6       | 519   | 347   | 0.62   |
| Kingston  | USNS8180S3512GJ    | 512 GB | 1       | 227   | 0     | 0.62   |
| Intel     | SSDSC2MH250A2      | 250 GB | 1       | 227   | 0     | 0.62   |
| SanDisk   | X300 MSATA         | 128 GB | 2       | 227   | 0     | 0.62   |
| SanDisk   | SD8TN8U256G1001    | 256 GB | 5       | 226   | 0     | 0.62   |
| Samsung   | MZNLN512HCJH-000L1 | 512 GB | 2       | 226   | 0     | 0.62   |
| Team      | T253X2512G         | 512 GB | 3       | 226   | 0     | 0.62   |
| China     | 240GB SSD          | 240 GB | 4       | 226   | 0     | 0.62   |
| Corsair   | Performance Pro    | 128 GB | 2       | 227   | 1     | 0.62   |
| Samsung   | MMCRE28G5MXP-MVB   | 128 GB | 1       | 225   | 0     | 0.62   |
| Samsung   | MZNTN512HDJH-00007 | 512 GB | 1       | 225   | 0     | 0.62   |
| Patriot   | Flare              | 64 GB  | 4       | 225   | 0     | 0.62   |
| Samsung   | MZNTE128HMGR-000L1 | 128 GB | 1       | 224   | 0     | 0.62   |
| OCZ       | OCTANE S2          | 64 GB  | 1       | 224   | 0     | 0.61   |
| Kingston  | SHFS37A240G        | 240 GB | 29      | 263   | 246   | 0.61   |
| Intel     | SSDSC2BB600G4      | 600 GB | 1       | 223   | 0     | 0.61   |
| Kingston  | SVP200S37A90G      | 90 GB  | 2       | 223   | 0     | 0.61   |
| Team      | L3 EVO SSD         | 120 GB | 4       | 222   | 0     | 0.61   |
| SK hynix  | HFS512G39MND-3510A | 512 GB | 1       | 222   | 0     | 0.61   |
| ADATA     | SSD DP900 128GB... | 128 GB | 3       | 467   | 680   | 0.61   |
| Micron    | 1100_MTFDDAK2T0TBN | 2 TB   | 3       | 221   | 0     | 0.61   |
| SanDisk   | SD7SB6S-256G-1006  | 256 GB | 2       | 220   | 0     | 0.60   |
| Phison    | SATA SSD           | 240 GB | 13      | 220   | 0     | 0.60   |
| Samsung   | MZNLN256HMHQ-000H1 | 256 GB | 13      | 220   | 0     | 0.60   |
| Corsair   | Force LE SSD       | 480 GB | 1       | 220   | 0     | 0.60   |
| SanDisk   | SD6SB1M-128G-1006  | 128 GB | 6       | 237   | 2     | 0.60   |
| Transcend | TS32GSSD340        | 32 GB  | 1       | 219   | 0     | 0.60   |
| OCZ       | AGILITY4           | 256 GB | 8       | 364   | 43    | 0.60   |
| SanDisk   | SD8SN8U128G1001    | 128 GB | 2       | 218   | 0     | 0.60   |
| Samsung   | MZNTE128HMGR-000SO | 128 GB | 2       | 379   | 773   | 0.60   |
| Lite-On   | PH4-CE240          | 240 GB | 2       | 218   | 0     | 0.60   |
| Samsung   | MMDPE56GFDXP-MVB   | 256 GB | 1       | 218   | 0     | 0.60   |
| Kingston  | RBU-SMSM151S324GD  | 24 GB  | 1       | 217   | 0     | 0.60   |
| Plextor   | PX-128S2G          | 128 GB | 2       | 217   | 0     | 0.60   |
| Samsung   | MMCQE28GFMUP-MVA   | 128 GB | 3       | 243   | 9     | 0.59   |
| ADATA     | XM13               | 32 GB  | 2       | 216   | 0     | 0.59   |
| WDC       | WDS200T2B0B        | 2 TB   | 2       | 216   | 0     | 0.59   |
| Samsung   | MZHPU256HCGL-00005 | 256 GB | 1       | 216   | 0     | 0.59   |
| Micron    | 5100_MTFDDAK960TBY | 960 GB | 1       | 216   | 0     | 0.59   |
| Crucial   | CT250MX200SSD4     | 250 GB | 1       | 215   | 0     | 0.59   |
| Intel     | SSDSC2CT180A4      | 180 GB | 7       | 215   | 0     | 0.59   |
| Smartbuy  | SSD                | 64 GB  | 24      | 214   | 0     | 0.59   |
| Samsung   | MZMTD128HAFV-00007 | 128 GB | 1       | 214   | 0     | 0.59   |
| Hoodisk   | SSD                | 64 GB  | 1       | 214   | 0     | 0.59   |
| OCZ       | VERTEX             | 96 GB  | 1       | 214   | 0     | 0.59   |
| Kingston  | SNV425S264GB       | 64 GB  | 5       | 878   | 5     | 0.59   |
| SanDisk   | SDSSDH2128G        | 128 GB | 2       | 213   | 0     | 0.58   |
| SanDisk   | SDSSDH31024G       | 1 TB   | 12      | 213   | 0     | 0.58   |
| SanDisk   | SD8SN8U-256G-1006  | 256 GB | 30      | 251   | 137   | 0.58   |
| Intel     | SSDSC2KG960G8      | 960 GB | 1       | 212   | 0     | 0.58   |
| DOGFISH   | SSD 256G           | 256 GB | 1       | 212   | 0     | 0.58   |
| Micron    | 5210_MTFDDAK7T6QDE | 7.6 TB | 2       | 211   | 0     | 0.58   |
| Corsair   | Neutron SSD        | 64 GB  | 4       | 261   | 3     | 0.58   |
| Toshiba   | THNSNJ128GVNU      | 128 GB | 1       | 211   | 0     | 0.58   |
| Micron    | 5100_MTFDDAV960TBY | 960 GB | 2       | 210   | 0     | 0.58   |
| Samsung   | MZ7LN128HAHQ-000H1 | 128 GB | 1       | 210   | 0     | 0.58   |
| SanDisk   | SSD U100           | 32 GB  | 6       | 212   | 168   | 0.57   |
| Kingston  | SHFS37A120G        | 120 GB | 105     | 298   | 263   | 0.57   |
| Apple     | SSD SM0128G        | 121 GB | 13      | 209   | 0     | 0.57   |
| Team      | T253TD480G         | 480 GB | 1       | 209   | 0     | 0.57   |
| Intel     | SSDSC2BW120H6      | 120 GB | 17      | 234   | 5     | 0.57   |
| SK hynix  | HFS256G39MND-2300A | 256 GB | 3       | 552   | 162   | 0.57   |
| Toshiba   | THNSNJ128GCST      | 128 GB | 3       | 208   | 0     | 0.57   |
| OCZ       | VERTEX2            | 50 GB  | 2       | 309   | 320   | 0.57   |
| SK hynix  | SC311 SATA         | 128 GB | 23      | 207   | 0     | 0.57   |
| Team      | L5 SSD             | 120 GB | 1       | 207   | 0     | 0.57   |
| Palit     | PH120 SSD          | 120 GB | 1       | 207   | 0     | 0.57   |
| Kingston  | SKC300S37A120G     | 120 GB | 20      | 209   | 1     | 0.57   |
| SanDisk   | iSSD P4            | 8 GB   | 4       | 276   | 1     | 0.57   |
| Intel     | SSDSA2BW160G3L     | 160 GB | 9       | 206   | 0     | 0.57   |
| Micron    | MTFDDAK256MAM-1K12 | 256 GB | 13      | 234   | 466   | 0.57   |
| Smartbuy  | m.2 S10-2280T      | 128 GB | 1       | 206   | 0     | 0.57   |
| Corsair   | CSSD-F60GB2        | 64 GB  | 5       | 799   | 199   | 0.56   |
| Toshiba   | THNSNJ512GCSU      | 512 GB | 1       | 205   | 0     | 0.56   |
| Zheino    | CHN-25SATAS3-256   | 256 GB | 1       | 205   | 0     | 0.56   |
| ADATA     | SU810NS38 SATA ... | 128 GB | 3       | 205   | 0     | 0.56   |
| Kingston  | SS050S216G         | 16 GB  | 1       | 205   | 0     | 0.56   |
| China     | SATA SSD           | 256 GB | 2       | 205   | 0     | 0.56   |
| SPCC      | SSD B29            | 32 GB  | 1       | 204   | 0     | 0.56   |
| Mushkin   | MKNSSDRE1TB        | 1 TB   | 6       | 204   | 0     | 0.56   |
| Micron    | M550_MTFDDAV128MAY | 128 GB | 1       | 204   | 0     | 0.56   |
| Goodram   | SSDPR-CX300-240    | 240 GB | 6       | 203   | 0     | 0.56   |
| Transcend | TS64GSSD370        | 64 GB  | 3       | 203   | 0     | 0.56   |
| SanDisk   | SD6SF1M128GG56     | 128 GB | 1       | 203   | 0     | 0.56   |
| Smartbuy  | m.2 S11-2280S      | 128 GB | 1       | 202   | 0     | 0.56   |
| Samsung   | MZRPA128HMCD-000SO | 64 GB  | 10      | 202   | 0     | 0.56   |
| OCZ       | TRION100           | 120 GB | 7       | 217   | 2     | 0.55   |
| Samsung   | MZNTY128HDHP-00000 | 128 GB | 7       | 201   | 0     | 0.55   |
| Micron    | 1100 SATA          | 512 GB | 10      | 253   | 249   | 0.55   |
| Samsung   | MZNTE256HMHP-000L7 | 256 GB | 1       | 201   | 0     | 0.55   |
| SanDisk   | SDSSDA-2T00        | 2 TB   | 1       | 200   | 0     | 0.55   |
| Samsung   | SSD PM871b M.2 ... | 128 GB | 1       | 200   | 0     | 0.55   |
| V-GeN     | SSD                | 240 GB | 1       | 200   | 0     | 0.55   |
| Patriot   | Blaze              | 120 GB | 6       | 200   | 0     | 0.55   |
| SanDisk   | SD5SF2128G1014E    | 128 GB | 2       | 200   | 0     | 0.55   |
| SPCC      | SSD                | 64 GB  | 77      | 211   | 40    | 0.55   |
| ADATA     | SU900              | 1 TB   | 4       | 199   | 1     | 0.54   |
| OCZ       | VERTEX PLUS        | 64 GB  | 1       | 396   | 1     | 0.54   |
| HP        | SSD M700           | 120 GB | 4       | 196   | 0     | 0.54   |
| Samsung   | MZ7TY256HDHP-00000 | 256 GB | 4       | 196   | 0     | 0.54   |
| Samsung   | MZNTD256HAGL-00000 | 256 GB | 1       | 196   | 0     | 0.54   |
| Smartbuy  | SSD                | 480 GB | 2       | 195   | 0     | 0.54   |
| Toshiba   | Q300               | 240 GB | 4       | 326   | 3     | 0.54   |
| Plextor   | PX-128S3G          | 128 GB | 1       | 194   | 0     | 0.53   |
| SanDisk   | X400 M.2 2280      | 128 GB | 7       | 194   | 0     | 0.53   |
| Kingston  | RBU-SC100S37240GE  | 240 GB | 1       | 194   | 0     | 0.53   |
| Smartbuy  | SSD                | 120 GB | 71      | 203   | 1     | 0.53   |
| Crucial   | CT120BX300SSD1     | 120 GB | 8       | 193   | 0     | 0.53   |
| Micron    | MTFDBAK128MAG-1G1  | 128 GB | 2       | 192   | 0     | 0.53   |
| OCZ       | VERTEX4            | 512 GB | 1       | 573   | 2     | 0.52   |
| ADATA     | SU760              | 512 GB | 1       | 190   | 0     | 0.52   |
| Neo Forza | NFS011SA328-600... | 128 GB | 1       | 190   | 0     | 0.52   |
| Kingston  | SS100S216G         | 16 GB  | 1       | 190   | 0     | 0.52   |
| Golden... | SSD 128            | 128 GB | 1       | 190   | 0     | 0.52   |
| Intenso   | SSD                | 256 GB | 9       | 190   | 0     | 0.52   |
| SanDisk   | SDSSDH3 512G       | 512 GB | 3       | 189   | 0     | 0.52   |
| Micron    | 5300_MTFDDAK3T8TDT | 3.8 TB | 6       | 189   | 0     | 0.52   |
| Kingston  | SUV500MS480G       | 480 GB | 4       | 189   | 0     | 0.52   |
| Samsung   | SSD 860 EVO mSATA  | 500 GB | 8       | 189   | 0     | 0.52   |
| SanDisk   | SDSSDH32000G       | 2 TB   | 2       | 189   | 0     | 0.52   |
| Intel     | SSDSC2BW360H6      | 360 GB | 1       | 566   | 2     | 0.52   |
| HP        | SSD S700           | 500 GB | 8       | 188   | 0     | 0.52   |
| Intel     | SSDSC2KB038T8R     | 3.8 TB | 1       | 188   | 0     | 0.52   |
| Crucial   | CT128MX100SSD1     | 128 GB | 6       | 377   | 8     | 0.51   |
| Samsung   | MZMTD512HAGL-000L1 | 512 GB | 3       | 223   | 33    | 0.51   |
| Transcend | TS128GSSD720       | 128 GB | 2       | 187   | 0     | 0.51   |
| Intel     | SSDSC2BF180A4L     | 180 GB | 4       | 186   | 0     | 0.51   |
| Smartbuy  | mSata              | 64 GB  | 1       | 186   | 0     | 0.51   |
| SanDisk   | SD5SE2256G1002E    | 256 GB | 4       | 183   | 0     | 0.50   |
| SK hynix  | HFS256G32TND-N210A | 256 GB | 3       | 183   | 0     | 0.50   |
| Kingston  | SV200S3256G        | 256 GB | 4       | 528   | 2     | 0.50   |
| e2e4      | SSD                | 240 GB | 2       | 183   | 0     | 0.50   |
| Samsung   | MZNLN256HCHP-000H1 | 256 GB | 2       | 182   | 0     | 0.50   |
| SanDisk   | SDSSDA240G         | 240 GB | 106     | 188   | 5     | 0.50   |
| Kston     | SSD                | 128 GB | 3       | 181   | 0     | 0.50   |
| SK hynix  | HFS128G32TNF-N3A0A | 128 GB | 4       | 180   | 0     | 0.50   |
| SanDisk   | SD9SN8W512G1002    | 512 GB | 2       | 180   | 0     | 0.50   |
| Transcend | TS128GMSA740       | 128 GB | 1       | 180   | 0     | 0.50   |
| Kingston  | SV300S37A480G      | 480 GB | 19      | 184   | 54    | 0.49   |
| INNOVA... | SSD                | 1 TB   | 1       | 180   | 0     | 0.49   |
| SanDisk   | SD6SN1M-256G-1006  | 256 GB | 4       | 243   | 1     | 0.49   |
| ZTC       | SM201-256G         | 256 GB | 2       | 179   | 0     | 0.49   |
| ADATA     | SP550              | 480 GB | 2       | 179   | 0     | 0.49   |
| SK hynix  | HFS128G3BMND-3210A | 128 GB | 2       | 178   | 0     | 0.49   |
| Seagate   | SSD                | 500 GB | 2       | 178   | 0     | 0.49   |
| SanDisk   | SSD U100           | 16 GB  | 10      | 178   | 0     | 0.49   |
| Phison    | SATA SSD           | 128 GB | 6       | 177   | 0     | 0.49   |
| KingDian  | S400 XT            | 240 GB | 1       | 177   | 0     | 0.49   |
| SPCC      | SSD A20            | 64 GB  | 2       | 177   | 0     | 0.49   |
| Toshiba   | Q300               | 120 GB | 3       | 176   | 0     | 0.48   |
| Vaseky    | V800-64G           | 64 GB  | 1       | 175   | 0     | 0.48   |
| Intenso   | SSD                | 128 GB | 21      | 191   | 1     | 0.48   |
| BIOSTAR   | S100-240GB PLUS    | 240 GB | 1       | 175   | 0     | 0.48   |
| SanDisk   | SD7TB3Q-128G-1006  | 128 GB | 2       | 220   | 15    | 0.48   |
| SanDisk   | SD7TB6S256G1001    | 256 GB | 3       | 174   | 0     | 0.48   |
| Micron    | MTFDDAK512MBF-1... | 512 GB | 1       | 173   | 0     | 0.48   |
| SanDisk   | SD9SN8W256G1102    | 256 GB | 13      | 173   | 0     | 0.47   |
| Faspeed   | F510-120G          | 120 GB | 1       | 173   | 0     | 0.47   |
| PNY       | SSD2SC240G1CS17... | 240 GB | 3       | 172   | 0     | 0.47   |
| SK hynix  | HFS256G39MND-3310A | 256 GB | 1       | 172   | 0     | 0.47   |
| Kingston  | SV100S2128G        | 128 GB | 3       | 286   | 2     | 0.47   |
| Kingston  | RBU-SNS8152S351... | 512 GB | 1       | 171   | 0     | 0.47   |
| Samsung   | MZNTY128HDHP-000L2 | 128 GB | 1       | 171   | 0     | 0.47   |
| Toshiba   | THNSNH128GMCT      | 128 GB | 3       | 170   | 0     | 0.47   |
| SanDisk   | SSD i100           | 24 GB  | 21      | 207   | 50    | 0.47   |
| SanDisk   | X300 MSATA         | 256 GB | 3       | 170   | 0     | 0.47   |
| SanDisk   | SD6SB1M256G1022I   | 256 GB | 2       | 370   | 237   | 0.47   |
| SPCC      | SSD                | 120 GB | 132     | 224   | 109   | 0.47   |
| Samsung   | SSD 860 EVO M.2    | 250 GB | 35      | 169   | 0     | 0.47   |
| SanDisk   | SD9TN8W512G1001    | 512 GB | 1       | 169   | 0     | 0.47   |
| Samsung   | SSD 860 EVO        | 1 TB   | 262     | 169   | 0     | 0.46   |
| Mushkin   | MKNSSDEC60GB       | 64 GB  | 1       | 169   | 0     | 0.46   |
| KingFast  | SSD                | 128 GB | 13      | 180   | 1     | 0.46   |
| SK hynix  | HFS512G39TNF-N3A0A | 512 GB | 2       | 168   | 0     | 0.46   |
| Samsung   | MZ7TY128HDHP-00000 | 128 GB | 2       | 168   | 0     | 0.46   |
| Crucial   | CT480M500SSD1      | 480 GB | 9       | 1172  | 349   | 0.46   |
| Intel     | SSDSC2BF180A4H     | 180 GB | 11      | 269   | 1     | 0.46   |
| Samsung   | SSD 850 EVO M.2    | 1 TB   | 4       | 167   | 0     | 0.46   |
| Intel     | SSDSA2CW300G3      | 304 GB | 4       | 167   | 0     | 0.46   |
| Plextor   | PX-256M5M          | 256 GB | 3       | 167   | 0     | 0.46   |
| Intenso   | SSD Sata III       | 240 GB | 3       | 166   | 0     | 0.46   |
| SK hynix  | SC308 SATA         | 256 GB | 7       | 193   | 13    | 0.46   |
| Phison    | SATA SSD           | 480 GB | 6       | 166   | 0     | 0.46   |
| Samsung   | SSD 860 EVO        | 250 GB | 238     | 167   | 1     | 0.46   |
| Samsung   | SSD 860 QVO        | 2 TB   | 32      | 166   | 0     | 0.46   |
| Patriot   | Blast              | 120 GB | 7       | 166   | 0     | 0.46   |
| SanDisk   | SDSSDH3512G        | 512 GB | 18      | 165   | 0     | 0.45   |
| LDLC      | SSD                | 120 GB | 8       | 195   | 1     | 0.45   |
| Plextor   | PX-AG256M6e        | 256 GB | 2       | 165   | 0     | 0.45   |
| KingFast  | SSD                | 256 GB | 9       | 164   | 0     | 0.45   |
| Intel     | SSDSA2M080G2HP     | 80 GB  | 3       | 169   | 1     | 0.45   |
| WDC       | WDS250G2B0A-00SM50 | 250 GB | 40      | 164   | 0     | 0.45   |
| Samsung   | SSD 830 Series     | 56 GB  | 1       | 164   | 0     | 0.45   |
| SanDisk   | SDSSDH3250G        | 250 GB | 16      | 163   | 0     | 0.45   |
| SanDisk   | SD9SN8W256G1002    | 256 GB | 6       | 163   | 0     | 0.45   |
| Kingmax   | SSD                | 120 GB | 26      | 263   | 277   | 0.45   |
| GLOWAY    | STK720GS3-S7       | 720 GB | 1       | 163   | 0     | 0.45   |
| Seagate   | BarraCuda SSD Z... | 1 TB   | 4       | 162   | 0     | 0.45   |
| OCZ       | VERTEX460          | 120 GB | 4       | 294   | 5     | 0.45   |
| SanDisk   | SSD U100           | 256 GB | 4       | 184   | 1     | 0.45   |
| V-GeN     | V-GEN02SM19EG51... | 512 GB | 1       | 162   | 0     | 0.45   |
| Apacer    | 256GB SATA Flas... | 256 GB | 1       | 162   | 0     | 0.44   |
| Samsung   | SSD PM871b M.2 ... | 512 GB | 2       | 161   | 0     | 0.44   |
| Intel     | SSDSC2KB240G8      | 240 GB | 8       | 161   | 0     | 0.44   |
| Goodram   | CX100              | 120 GB | 8       | 266   | 2     | 0.44   |
| Crucial   | M4-CT512M4SSD1     | 512 GB | 1       | 161   | 0     | 0.44   |
| Samsung   | SSD EVO 360G       | 360 GB | 1       | 161   | 0     | 0.44   |
| Intel     | SSDSA2CW160G3      | 160 GB | 3       | 161   | 0     | 0.44   |
| Intel     | SSDSCMMW240A3L     | 240 GB | 3       | 221   | 1     | 0.44   |
| SanDisk   | X600 M.2 2280 SATA | 128 GB | 5       | 161   | 0     | 0.44   |
| Corsair   | Force LS SSD       | 240 GB | 3       | 343   | 505   | 0.44   |
| GeIL      | ZENITH R3_120GB    | 120 GB | 3       | 160   | 0     | 0.44   |
| SanDisk   | SDSSDH3500G        | 500 GB | 16      | 160   | 0     | 0.44   |
| Plextor   | PX-256M5S          | 256 GB | 12      | 160   | 0     | 0.44   |
| Micron    | MTFDDAV512MBF-1... | 512 GB | 4       | 160   | 0     | 0.44   |
| Samsung   | MZ7LN256HAJQ-00000 | 256 GB | 2       | 159   | 0     | 0.44   |
| Samsung   | MZ7TY128HDHP-000L1 | 128 GB | 4       | 159   | 0     | 0.44   |
| SanDisk   | SD9SN8W512G1102    | 512 GB | 2       | 158   | 0     | 0.43   |
| Zheino    | CHN mSATAM3 128    | 128 GB | 2       | 158   | 0     | 0.43   |
| SanDisk   | SDSSDA120G         | 120 GB | 83      | 171   | 38    | 0.43   |
| Intel     | SSDSC2BF240A4L     | 240 GB | 5       | 283   | 3     | 0.43   |
| OCZ       | VERTEX2            | 180 GB | 3       | 158   | 0     | 0.43   |
| ADATA     | AXNS381E-128GM-B2  | 128 GB | 1       | 158   | 0     | 0.43   |
| Team      | TEAML5Lite3D480G   | 480 GB | 3       | 158   | 0     | 0.43   |
| Ramsta    | SSD S600           | 480 GB | 1       | 158   | 0     | 0.43   |
| Transcend | TS480GSSD220S      | 480 GB | 7       | 157   | 0     | 0.43   |
| GeIL      | ZENITH R3_240GB    | 240 GB | 1       | 157   | 0     | 0.43   |
| Lite-On   | CV1-CC128-11 2.... | 128 GB | 1       | 157   | 0     | 0.43   |
| WDC       | WDS100T2B0A-00SM50 | 1 TB   | 62      | 161   | 1     | 0.43   |
| WDC       | WDS200T2B0A-00SM50 | 2 TB   | 4       | 156   | 0     | 0.43   |
| Toshiba   | TR200              | 960 GB | 1       | 156   | 0     | 0.43   |
| Samsung   | SSD 860 EVO        | 500 GB | 431     | 157   | 3     | 0.43   |
| Samsung   | MMCRE64GFMPP-MVA   | 64 GB  | 2       | 155   | 0     | 0.43   |
| Goodram   | SSDPR-CX300-120    | 120 GB | 8       | 155   | 0     | 0.43   |
| Crucial   | CT525MX300SSD4     | 528 GB | 12      | 207   | 92    | 0.43   |
| SK hynix  | SH920 2.5 7MM      | 256 GB | 3       | 1222  | 97    | 0.43   |
| Kingston  | SUV500120G         | 120 GB | 19      | 164   | 1     | 0.43   |
| Patriot   | Burst              | 240 GB | 43      | 154   | 0     | 0.42   |
| Lite-On   | CV3-CE128-HP       | 128 GB | 1       | 154   | 0     | 0.42   |
| Lite-On   | LCS-256M6S         | 256 GB | 5       | 181   | 211   | 0.42   |
| SanDisk   | SD9TB8W256G1001    | 256 GB | 4       | 153   | 0     | 0.42   |
| Goodram   | SSDPR-S400U-240-80 | 240 GB | 3       | 153   | 0     | 0.42   |
| Plextor   | PX-256S2C          | 256 GB | 2       | 153   | 0     | 0.42   |
| Phison    | SATA SSD           | 120 GB | 31      | 153   | 0     | 0.42   |
| Intel     | SSDSC2BW180H6      | 180 GB | 1       | 153   | 0     | 0.42   |
| China     | 120GB SSD          | 120 GB | 48      | 153   | 0     | 0.42   |
| SanDisk   | SDSSDA-1T00        | 1 TB   | 7       | 153   | 0     | 0.42   |
| SPCC      | SSD162             | 120 GB | 9       | 439   | 569   | 0.42   |
| Toshiba   | Q300               | 960 GB | 1       | 153   | 0     | 0.42   |
| WDC       | WDS500G2B0A-00SM50 | 500 GB | 105     | 152   | 0     | 0.42   |
| Lite-On   | LCH-128V2S-11 2... | 128 GB | 4       | 152   | 0     | 0.42   |
| Hajaan    | SSD 256G           | 256 GB | 2       | 151   | 0     | 0.42   |
| Samsung   | MZNLF128HCHP-000L1 | 128 GB | 1       | 151   | 0     | 0.42   |
| Samsung   | MZNLN512HAJQ-000H1 | 512 GB | 2       | 151   | 0     | 0.41   |
| Crucial   | FCCT512MX100SSD1   | 512 GB | 1       | 151   | 0     | 0.41   |
| PNY       | CS2040 128GB SSD   | 128 GB | 1       | 150   | 0     | 0.41   |
| SanDisk   | SD8SN8U1T001122    | 1 TB   | 2       | 150   | 0     | 0.41   |
| Transcend | TS120GMTS820S      | 120 GB | 2       | 150   | 0     | 0.41   |
| Crucial   | FCCT480M500SSD1    | 480 GB | 1       | 150   | 0     | 0.41   |
| Corsair   | CSSD-F180GB2       | 180 GB | 1       | 149   | 0     | 0.41   |
| ADATA     | SX900              | 64 GB  | 5       | 444   | 618   | 0.41   |
| Plextor   | PX-128M6G-2242     | 128 GB | 2       | 149   | 0     | 0.41   |
| GALAX     | TA1D0120A          | 120 GB | 3       | 149   | 0     | 0.41   |
| SanDisk   | SD8SN8U128G1002    | 128 GB | 3       | 149   | 0     | 0.41   |
| Corsair   | Force LS SSD       | 120 GB | 14      | 351   | 433   | 0.41   |
| Toshiba   | A100               | 120 GB | 5       | 148   | 0     | 0.41   |
| Intel     | SSDSC2BB300G4      | 304 GB | 2       | 147   | 0     | 0.41   |
| Transcend | TS256GMTS400       | 256 GB | 4       | 147   | 0     | 0.40   |
| Toshiba   | TR200              | 480 GB | 9       | 147   | 0     | 0.40   |
| Kingston  | MS80000058688      | 256 GB | 3       | 146   | 0     | 0.40   |
| Teclast   | 128GB S550         | 128 GB | 1       | 146   | 0     | 0.40   |
| Samsung   | Portable SSD T5    | 2 TB   | 3       | 146   | 0     | 0.40   |
| Intel     | SSDSC2KG240G7      | 240 GB | 1       | 146   | 0     | 0.40   |
| Kingston  | HyperX Fury 3D     | 480 GB | 2       | 146   | 0     | 0.40   |
| KingSpec  | ACJC2M032mSH       | 32 GB  | 2       | 145   | 0     | 0.40   |
| Netac     | SSD                | 720 GB | 4       | 145   | 0     | 0.40   |
| Samsung   | MZ-5EA2000-0D3     | 200 GB | 2       | 145   | 0     | 0.40   |
| Apple     | SSD SD0128F        | 121 GB | 7       | 145   | 0     | 0.40   |
| SK hynix  | SHGS31-500GS-2     | 500 GB | 4       | 145   | 0     | 0.40   |
| Intel     | SSDSC2KW512G8      | 512 GB | 17      | 145   | 1     | 0.40   |
| SanDisk   | SSD U110           | 16 GB  | 22      | 144   | 0     | 0.40   |
| Lite-On   | CV3-8D128-HP       | 128 GB | 1       | 144   | 0     | 0.40   |
| SanDisk   | SSD PLUS 240 GB    | 240 GB | 19      | 184   | 4     | 0.39   |
| Crucial   | CT256M550SSD3      | 256 GB | 2       | 840   | 8     | 0.39   |
| ADATA     | SP920SS            | 128 GB | 8       | 430   | 8     | 0.39   |
| Lumino... | SSD                | 256 GB | 1       | 143   | 0     | 0.39   |
| WDC       | WDS100T2B0B-00YS70 | 1 TB   | 19      | 158   | 1     | 0.39   |
| Smartbuy  | SSD                | 240 GB | 22      | 174   | 1     | 0.39   |
| QUMO      | SSD                | 64 GB  | 1       | 143   | 0     | 0.39   |
| SPCC      | SSD                | 256 GB | 41      | 147   | 3     | 0.39   |
| Seagate   | BarraCuda 120 S... | 1 TB   | 3       | 142   | 0     | 0.39   |
| Plextor   | PH6-CE120          | 120 GB | 8       | 142   | 0     | 0.39   |
| Toshiba   | THNSNW032GMCP      | 32 GB  | 1       | 142   | 0     | 0.39   |
| SanDisk   | X600 M.2 2280 SATA | 512 GB | 1       | 141   | 0     | 0.39   |
| Corsair   | Force LS SSD       | 64 GB  | 23      | 291   | 136   | 0.39   |
| KingSpec  | KSD-SA25.5-064MJ   | 64 GB  | 1       | 141   | 0     | 0.39   |
| WDC       | WDBNCE2500PNC      | 250 GB | 7       | 141   | 0     | 0.39   |
| SanDisk   | SDSSDH3 1T00       | 1 TB   | 15      | 141   | 0     | 0.39   |
| Lite-On   | L8H-256V2G-HP      | 256 GB | 7       | 140   | 0     | 0.39   |
| Mushkin   | MKNSSDCR120GB-7    | 120 GB | 2       | 702   | 514   | 0.39   |
| Innodisk  | mSATA mini 3ME ... | 32 GB  | 1       | 140   | 0     | 0.39   |
| TCSUNBOW  | X3                 | 480 GB | 2       | 139   | 0     | 0.38   |
| UNIC2     | S100-480           | 480 GB | 1       | 139   | 0     | 0.38   |
| INNOVA... | SSD                | 480 GB | 1       | 139   | 0     | 0.38   |
| MENGMI    | SSD                | 240 GB | 1       | 139   | 0     | 0.38   |
| WDC       | WDS500G2B0B-00YS70 | 500 GB | 44      | 139   | 0     | 0.38   |
| Micron    | MTFDDAK256MBF-1... | 256 GB | 3       | 139   | 0     | 0.38   |
| Toshiba   | THNSNH512GDNT      | 512 GB | 1       | 138   | 0     | 0.38   |
| ADATA     | AXNS381E-128GM-B   | 128 GB | 1       | 138   | 0     | 0.38   |
| ADATA     | SU900              | 512 GB | 3       | 138   | 0     | 0.38   |
| SK hynix  | HFS256G39TND-N210A | 256 GB | 34      | 186   | 81    | 0.38   |
| Patriot   | P200               | 512 GB | 1       | 137   | 0     | 0.38   |
| Intel     | SSDSC2KB480G8      | 480 GB | 4       | 137   | 0     | 0.38   |
| Lite-On   | IT LMT-256L9M      | 256 GB | 2       | 137   | 0     | 0.38   |
| Samsung   | MZ7LH480HAHQ0D3    | 480 GB | 2       | 137   | 0     | 0.38   |
| KingSpec  | P3-2TB             | 2 TB   | 1       | 136   | 0     | 0.37   |
| Toshiba   | THNSNH256GBST      | 256 GB | 2       | 136   | 0     | 0.37   |
| KingSpec  | NT-2TB             | 2 TB   | 1       | 136   | 0     | 0.37   |
| KingDian  | S400               | 480 GB | 3       | 136   | 0     | 0.37   |
| SanDisk   | SD9SN8W128G1102    | 128 GB | 6       | 136   | 0     | 0.37   |
| Micron    | MTFDDAK1T0MBF-1... | 1 TB   | 1       | 136   | 0     | 0.37   |
| WDC       | PC SA530 SDATB8... | 1 TB   | 1       | 136   | 0     | 0.37   |
| SPCC      | SSD                | 240 GB | 39      | 231   | 279   | 0.37   |
| SK hynix  | HFS128G32MND-3210A | 128 GB | 1       | 135   | 0     | 0.37   |
| Mushkin   | MKNSSDE3240GB      | 240 GB | 2       | 134   | 0     | 0.37   |
| Toshiba   | VX500              | 256 GB | 1       | 134   | 0     | 0.37   |
| Intel     | SSDSCKJF180A5H REF | 180 GB | 1       | 133   | 0     | 0.37   |
| Zheino    | CHN mSATA02M 256   | 256 GB | 2       | 219   | 1     | 0.37   |
| Crucial   | CT960BX500SSD1     | 960 GB | 13      | 133   | 0     | 0.37   |
| WDC       | WDS120G1G0A-00SS50 | 120 GB | 31      | 133   | 0     | 0.37   |
| MyDigi... | SB2                | 240 GB | 2       | 132   | 0     | 0.36   |
| KingDian  | S400               | 120 GB | 14      | 132   | 0     | 0.36   |
| Samsung   | MMCRE28GQDXP-MVB   | 64 GB  | 4       | 132   | 0     | 0.36   |
| Micron    | 1100 SATA          | 256 GB | 12      | 219   | 1     | 0.36   |
| Samsung   | SSD 860 EVO mSATA  | 250 GB | 15      | 131   | 0     | 0.36   |
| Plextor   | PX-128M5S          | 128 GB | 46      | 132   | 1     | 0.36   |
| HPE       | MK0800GEYKE        | 800 GB | 1       | 130   | 0     | 0.36   |
| SanDisk   | SDSSDH3 1T02       | 1 TB   | 2       | 130   | 0     | 0.36   |
| WDC       | WDBNCE5000PNC      | 500 GB | 10      | 129   | 0     | 0.36   |
| Toshiba   | THNSNF064GMCS      | 64 GB  | 2       | 129   | 0     | 0.35   |
| SPCC      | SPCCSolidStateDisk | 512 GB | 2       | 128   | 0     | 0.35   |
| KLEVV     | SSD NEO N500       | 240 GB | 1       | 127   | 0     | 0.35   |
| Toshiba   | TR200              | 240 GB | 35      | 127   | 0     | 0.35   |
| Vaseky    | V800-120G          | 120 GB | 1       | 127   | 0     | 0.35   |
| Goodram   | IRIDIUM            | 480 GB | 2       | 127   | 0     | 0.35   |
| Samsung   | MZNTY256HDHP-000L2 | 256 GB | 4       | 127   | 0     | 0.35   |
| OWC       | Mercury Electra... | 2 TB   | 3       | 371   | 2     | 0.35   |
| Samsung   | MZMTE256HMHP-000L1 | 256 GB | 2       | 126   | 0     | 0.35   |
| Lumino... | SSD                | 240 GB | 1       | 126   | 0     | 0.35   |
| Chiprex   | S10T3120GB         | 120 GB | 1       | 126   | 0     | 0.35   |
| Transcend | TS256GSSD370S      | 256 GB | 13      | 126   | 0     | 0.35   |
| Seagate   | BarraCuda SSD Z... | 2 TB   | 2       | 126   | 0     | 0.35   |
| Kingston  | SMSM150S324G       | 24 GB  | 1       | 126   | 0     | 0.35   |
| Intel     | SSDSC2CW060A3      | 64 GB  | 13      | 546   | 548   | 0.35   |
| Samsung   | MZNLN256HMHQ-000H7 | 256 GB | 2       | 126   | 0     | 0.35   |
| Samsung   | SSD 860 EVO M.2    | 500 GB | 50      | 126   | 0     | 0.35   |
| BlueRay   | SSD                | 120 GB | 1       | 125   | 0     | 0.34   |
| SanDisk   | SD5SB2-128G-1006E  | 128 GB | 1       | 125   | 0     | 0.34   |
| KingFast  | SSD                | 32 GB  | 1       | 125   | 0     | 0.34   |
| Samsung   | SSD 860 PRO        | 256 GB | 25      | 125   | 0     | 0.34   |
| BRAVEE... | SSD                | 240 GB | 1       | 125   | 0     | 0.34   |
| Lite-On   | CV5-8Q128          | 128 GB | 1       | 125   | 0     | 0.34   |
| Toshiba   | KSG60ZMV512G M.... | 512 GB | 4       | 124   | 0     | 0.34   |
| Samsung   | SSD PM871b M.2 ... | 256 GB | 3       | 124   | 0     | 0.34   |
| SanDisk   | SSD U100           | 24 GB  | 27      | 146   | 48    | 0.34   |
| Samsung   | SSD 860 QVO        | 1 TB   | 109     | 126   | 1     | 0.34   |
| Corsair   | Neutron GTX SSD    | 240 GB | 5       | 299   | 65    | 0.34   |
| Apple     | SSD SM128C         | 121 GB | 3       | 248   | 7     | 0.34   |
| Apple     | SSD SM512E         | 500 GB | 1       | 123   | 0     | 0.34   |
| Patriot   | P200               | 2 TB   | 3       | 226   | 16    | 0.34   |
| WDC       | PC SA530 SDASB8... | 1 TB   | 1       | 122   | 0     | 0.33   |
| Hypertec  | SSD2S240SF1200SA2  | 240 GB | 2       | 371   | 512   | 0.33   |
| ADATA     | SP600              | 64 GB  | 9       | 129   | 1     | 0.33   |
| PNY       | CS900 240GB SSD    | 240 GB | 40      | 121   | 0     | 0.33   |
| HP        | VK001920GWJPH      | 1.9 TB | 2       | 121   | 0     | 0.33   |
| Transcend | TS240GSSD220S      | 240 GB | 17      | 121   | 0     | 0.33   |
| Crucial   | CT250MX500SSD4     | 250 GB | 12      | 121   | 0     | 0.33   |
| ADATA     | SSD S511           | 64 GB  | 3       | 450   | 679   | 0.33   |
| Samsung   | MZNTD128HAGM-00000 | 128 GB | 3       | 120   | 0     | 0.33   |
| Samsung   | SSD 850            | 120 GB | 29      | 120   | 0     | 0.33   |
| Toshiba   | THNSNK128GVN8      | 128 GB | 6       | 120   | 0     | 0.33   |
| Kingston  | SUV500M8240G       | 240 GB | 1       | 120   | 0     | 0.33   |
| China     | 256GB SSD          | 256 GB | 1       | 119   | 0     | 0.33   |
| Fujitsu   | F500s 480G         | 480 GB | 1       | 119   | 0     | 0.33   |
| SPCC      | M.2 Disk           | 256 GB | 1       | 119   | 0     | 0.33   |
| Samsung   | MZMTD128HAFV-000   | 128 GB | 5       | 119   | 0     | 0.33   |
| Plextor   | PX-AG128M6e        | 128 GB | 4       | 229   | 2     | 0.33   |
| ADATA     | SP550              | 240 GB | 21      | 119   | 1     | 0.33   |
| Micron    | MTFDDAK256TBN-1... | 256 GB | 2       | 118   | 0     | 0.33   |
| Apacer    | AS340              | 240 GB | 13      | 126   | 1     | 0.33   |
| SanDisk   | SSD PLUS           | 120 GB | 49      | 118   | 0     | 0.33   |
| SK hynix  | HFS128G3BTND-N210A | 128 GB | 3       | 118   | 0     | 0.32   |
| China     | 128GB SSD          | 128 GB | 15      | 118   | 0     | 0.32   |
| SanDisk   | SD8SN8U-128G-1006  | 128 GB | 27      | 175   | 153   | 0.32   |
| Crucial   | CT2000BX500SSD1    | 2 TB   | 6       | 117   | 0     | 0.32   |
| LDLC      | SSD                | 480 GB | 4       | 123   | 1     | 0.32   |
| Lite-On   | CV3-8D256-11 SATA  | 256 GB | 6       | 117   | 0     | 0.32   |
| Samsung   | SSD 860 PRO        | 2 TB   | 5       | 117   | 0     | 0.32   |
| SanDisk   | SD9TN8W256G1001    | 256 GB | 3       | 117   | 0     | 0.32   |
| Kingston  | HyperX Fury 3D     | 240 GB | 3       | 117   | 0     | 0.32   |
| Hikvision | HS-SSD-E100 512G   | 512 GB | 1       | 116   | 0     | 0.32   |
| Samsung   | SSD 860 EVO M.2    | 1 TB   | 28      | 116   | 0     | 0.32   |
| Kingston  | SUV500M8480G       | 480 GB | 2       | 116   | 0     | 0.32   |
| ADATA     | SSD SX900 512GB... | 512 GB | 2       | 116   | 0     | 0.32   |
| Samsung   | MZNLN256HAJQ-000H7 | 256 GB | 3       | 115   | 0     | 0.32   |
| Kingston  | SA400S37480G       | 480 GB | 229     | 131   | 2     | 0.32   |
| Samsung   | SG9XCS2D400GESLT   | 400 GB | 1       | 115   | 0     | 0.32   |
| SanDisk   | SSD PLUS 120 GB    | 120 GB | 23      | 118   | 1     | 0.32   |
| Kingston  | SA400S37120G       | 120 GB | 456     | 125   | 1     | 0.31   |
| GLOWAY    | STK1TS3-S7         | 1 TB   | 1       | 114   | 0     | 0.31   |
| Goodram   | SSDPR-CL100-240    | 240 GB | 3       | 114   | 0     | 0.31   |
| OCZ       | D2CSTK181M11-0180  | 180 GB | 3       | 114   | 0     | 0.31   |
| Goodram   | IR-SSDPR-S25A-120  | 120 GB | 7       | 114   | 0     | 0.31   |
| SanDisk   | SD9SN8W256G        | 256 GB | 2       | 113   | 0     | 0.31   |
| Corsair   | FORCE LX SSD       | 256 GB | 1       | 113   | 0     | 0.31   |
| Crucial   | CT480BX300SSD1     | 480 GB | 12      | 113   | 0     | 0.31   |
| Intel     | SSDSA2M080G2LE     | 80 GB  | 2       | 154   | 6     | 0.31   |
| OCZ       | VERTEX2            | 90 GB  | 1       | 113   | 0     | 0.31   |
| ADATA     | SU650              | 240 GB | 45      | 134   | 1     | 0.31   |
| Micron    | MTFDDAK512MAM-1K1  | 512 GB | 1       | 113   | 0     | 0.31   |
| SanDisk   | SD9SB8W512G1101    | 512 GB | 4       | 112   | 0     | 0.31   |
| Samsung   | Portable SSD T5    | 1 TB   | 14      | 112   | 0     | 0.31   |
| Kingston  | SA400S37240G       | 240 GB | 483     | 119   | 1     | 0.31   |
| Samsung   | MZMPC128HBFU-000   | 128 GB | 2       | 112   | 0     | 0.31   |
| SanDisk   | SDSSDH3 250G       | 250 GB | 4       | 111   | 0     | 0.31   |
| Toshiba   | THNSNK256GVN8      | 256 GB | 1       | 111   | 0     | 0.31   |
| Crucial   | CT2000MX500SSD1    | 2 TB   | 38      | 111   | 0     | 0.30   |
| Samsung   | MZNTY256HDHP-00007 | 256 GB | 1       | 110   | 0     | 0.30   |
| SanDisk   | SSD PLUS           | 480 GB | 55      | 128   | 2     | 0.30   |
| SanDisk   | SD6SB1M128G1002    | 128 GB | 1       | 110   | 0     | 0.30   |
| Crucial   | CT1000MX500SSD1    | 1 TB   | 138     | 113   | 1     | 0.30   |
| KingDian  | S280               | 480 GB | 6       | 109   | 0     | 0.30   |
| Intel     | SSDSCKGF256A5 SATA | 256 GB | 5       | 109   | 0     | 0.30   |
| Samsung   | MZNLF128HCHP-000H1 | 128 GB | 1       | 109   | 0     | 0.30   |
| ADATA     | SU750              | 256 GB | 3       | 109   | 0     | 0.30   |
| Gigabyte  | GP-GSTFS31120GNTD  | 120 GB | 19      | 109   | 0     | 0.30   |
| WDC       | WDS500G1R0A-68A4W0 | 500 GB | 2       | 109   | 0     | 0.30   |
| Faspeed   | H7-240G            | 240 GB | 1       | 109   | 0     | 0.30   |
| Zheino    | CHN-25SATAC3-120   | 120 GB | 1       | 108   | 0     | 0.30   |
| SPCC      | SSD                | 1 TB   | 13      | 121   | 2     | 0.30   |
| KingDian  | S280-120GB         | 120 GB | 9       | 119   | 439   | 0.30   |
| GeIL      | R3_128GB           | 128 GB | 1       | 107   | 0     | 0.30   |
| Transcend | TS256GSSD230S      | 256 GB | 8       | 122   | 1     | 0.30   |
| Transcend | TS256GSSD370       | 256 GB | 1       | 107   | 0     | 0.30   |
| Kingston  | RBUSNS8180S3128GJ  | 128 GB | 3       | 107   | 0     | 0.29   |
| Transcend | TS120GSSD220S      | 120 GB | 15      | 107   | 0     | 0.29   |
| Intel     | SSDSC2KW256G8      | 256 GB | 26      | 106   | 0     | 0.29   |
| Crucial   | CT256M550SSD1      | 256 GB | 6       | 362   | 8     | 0.29   |
| ADATA     | IM2S3338-128GD2    | 128 GB | 7       | 106   | 0     | 0.29   |
| PNY       | SSD2SC240G5LC72... | 240 GB | 1       | 106   | 0     | 0.29   |
| Mushkin   | MKNSSDAT60GB-V     | 64 GB  | 1       | 106   | 0     | 0.29   |
| Transcend | TS1TSSD230S        | 1 TB   | 5       | 106   | 0     | 0.29   |
| Samsung   | MZYTE128HMGR-000L2 | 128 GB | 1       | 106   | 0     | 0.29   |
| Samsung   | MZNLN512HAJQ-00000 | 512 GB | 5       | 106   | 0     | 0.29   |
| SanDisk   | SD9SN8W128G1002    | 128 GB | 8       | 106   | 0     | 0.29   |
| Silicon   | SATA3 120GB SSD    | 120 GB | 1       | 106   | 0     | 0.29   |
| Crucial   | CT500BX100SSD1     | 500 GB | 13      | 106   | 1     | 0.29   |
| Plextor   | PH6-CE240-L1       | 240 GB | 1       | 106   | 0     | 0.29   |
| Lite-On   | IT L8T-128L9G      | 128 GB | 1       | 105   | 0     | 0.29   |
| Micron    | 1100_MTFDDAV512TBN | 512 GB | 26      | 108   | 1     | 0.29   |
| Toshiba   | THNSNC256GBSJ      | 256 GB | 1       | 105   | 0     | 0.29   |
| Kingston  | SHFS37A480G        | 480 GB | 1       | 104   | 0     | 0.29   |
| Samsung   | SSD 860 EVO        | 2 TB   | 34      | 104   | 0     | 0.29   |
| Transcend | TS256GSSD360S      | 256 GB | 3       | 104   | 0     | 0.29   |
| Intenso   | SSD                | 512 GB | 3       | 104   | 0     | 0.29   |
| Seagate   | XA480ME10063       | 480 GB | 4       | 104   | 0     | 0.29   |
| SanDisk   | SD8SB8U-128G-1006  | 128 GB | 1       | 104   | 0     | 0.29   |
| Transcend | TS64GSSD340        | 64 GB  | 3       | 180   | 336   | 0.28   |
| WDC       | WDS240G1G0B-00RC30 | 240 GB | 6       | 103   | 0     | 0.28   |
| Micron    | MTFDDAV256TBN-1... | 256 GB | 13      | 123   | 80    | 0.28   |
| Intel     | SSDSC2BF180A5L     | 180 GB | 8       | 193   | 16    | 0.28   |
| Intel     | SSDSA2M160G2GN     | 160 GB | 1       | 2996  | 28    | 0.28   |
| SK hynix  | SC210 2.5 7MM      | 128 GB | 2       | 478   | 2     | 0.28   |
| Fujitsu   | F300               | 480 GB | 1       | 103   | 0     | 0.28   |
| Transcend | TS120GSSD25D-M     | 128 GB | 1       | 309   | 2     | 0.28   |
| Apacer    | AS510S             | 64 GB  | 5       | 103   | 0     | 0.28   |
| Phison    | SATA SSD           | 1 TB   | 7       | 102   | 0     | 0.28   |
| Intel     | SSDSA2BW160G3H     | 160 GB | 10      | 206   | 2     | 0.28   |
| SanDisk   | SDSA6MM-032G-1006  | 32 GB  | 1       | 102   | 0     | 0.28   |
| KingDian  | S370               | 512 GB | 2       | 102   | 0     | 0.28   |
| Samsung   | MZNLN128HAHQ-000H1 | 128 GB | 33      | 105   | 40    | 0.28   |
| KingFast  | SSD                | 32 GB  | 1       | 102   | 0     | 0.28   |
| SanDisk   | SD9SN8W256G1014    | 256 GB | 2       | 101   | 0     | 0.28   |
| Crucial   | CT250MX500SSD1     | 250 GB | 69      | 103   | 31    | 0.28   |
| ADATA     | SU700              | 120 GB | 8       | 103   | 1     | 0.28   |
| Phison    | SSM28512GPTCB3B... | 512 GB | 1       | 101   | 0     | 0.28   |
| WDC       | WDS120G2G0B-00EPW0 | 120 GB | 36      | 102   | 1     | 0.28   |
| Goodram   | SSDPR-CX400-512    | 512 GB | 10      | 101   | 0     | 0.28   |
| Micron    | MTFDDAK256TBN      | 256 GB | 1       | 101   | 0     | 0.28   |
| ADATA     | SU810NS38 SATA ... | 256 GB | 11      | 101   | 0     | 0.28   |
| Corsair   | Force LE200 SSD    | 120 GB | 5       | 101   | 0     | 0.28   |
| Samsung   | MZMTD128HAFV-00000 | 128 GB | 1       | 100   | 0     | 0.28   |
| China     | SATA SSD           | 120 GB | 38      | 100   | 0     | 0.28   |
| Crucial   | CT500MX500SSD1     | 500 GB | 148     | 100   | 1     | 0.28   |
| Goodram   | SSD                | 480 GB | 1       | 99    | 0     | 0.27   |
| ORICO     | N300               | 128 GB | 1       | 99    | 0     | 0.27   |
| SK hynix  | HFS128G32TND-N210A | 128 GB | 3       | 412   | 132   | 0.27   |
| Patriot   | Burst              | 960 GB | 6       | 99    | 0     | 0.27   |
| Intel     | SSDSC2KF128G8L     | 128 GB | 6       | 99    | 0     | 0.27   |
| Hikvision | HKVSN HS-SSD-C1... | 240 GB | 1       | 99    | 0     | 0.27   |
| Intel     | SSDMCEAC180B3      | 180 GB | 3       | 98    | 0     | 0.27   |
| SK hynix  | HFS128G39TND-N210A | 128 GB | 35      | 138   | 8     | 0.27   |
| KIOXIA... | SATA SSD           | 480 GB | 1       | 98    | 0     | 0.27   |
| Micron    | 5100_MTFDDAK240TCB | 240 GB | 1       | 98    | 0     | 0.27   |
| AMD       | R3SL480G           | 480 GB | 1       | 98    | 0     | 0.27   |
| Toshiba   | THNSNH256G8NT      | 256 GB | 1       | 293   | 2     | 0.27   |
| Intel     | SSDSCKGF240A5L     | 240 GB | 1       | 97    | 0     | 0.27   |
| WDC       | WDS500G2B0A        | 500 GB | 23      | 97    | 0     | 0.27   |
| Samsung   | MZNLN256HCHP-000L2 | 256 GB | 4       | 97    | 0     | 0.27   |
| Patriot   | Burst              | 480 GB | 20      | 104   | 1     | 0.27   |
| Samsung   | MZ7KM480HMHQ-000MV | 480 GB | 1       | 97    | 0     | 0.27   |
| Anobit    | Gen2A400 118032738 | 400 GB | 1       | 96    | 0     | 0.27   |
| SanDisk   | SD7SB3Q128G1002    | 128 GB | 1       | 387   | 3     | 0.27   |
| Dogfish   | SSD                | 250 GB | 1       | 96    | 0     | 0.26   |
| Londisk   | SSD                | 120 GB | 8       | 96    | 0     | 0.26   |
| WDC       | WDS250G2B0A        | 250 GB | 7       | 96    | 0     | 0.26   |
| Samsung   | MZNLN256HAJQ-000H1 | 256 GB | 18      | 105   | 12    | 0.26   |
| Phison    | 256GB PS3110-S10C  | 256 GB | 1       | 95    | 0     | 0.26   |
| SPCC      | SSD170             | 120 GB | 3       | 245   | 341   | 0.26   |
| Plextor   | PX-128M5M          | 128 GB | 9       | 95    | 0     | 0.26   |
| Lite-On   | CV8-8E128-11 SATA  | 128 GB | 15      | 95    | 0     | 0.26   |
| BHT       | WR202I0064G E70... | 64 GB  | 1       | 95    | 0     | 0.26   |
| KingDian  | SSD-S400           | 120 GB | 1       | 285   | 2     | 0.26   |
| ADATA     | SU655              | 120 GB | 4       | 95    | 0     | 0.26   |
| Kingston  | SUV500240G         | 240 GB | 25      | 104   | 50    | 0.26   |
| GOWE      | M750 120G          | 120 GB | 1       | 284   | 2     | 0.26   |
| Kingston  | RBUSC180DS37256GJ  | 256 GB | 2       | 94    | 0     | 0.26   |
| Samsung   | SSD 860 EVO M.2    | 2 TB   | 4       | 93    | 0     | 0.26   |
| Integral  | V Series SATA SSD  | 480 GB | 1       | 93    | 0     | 0.26   |
| BIOSTAR   | S120-128GB         | 128 GB | 1       | 93    | 0     | 0.26   |
| Team      | T2535T480G         | 480 GB | 1       | 93    | 0     | 0.26   |
| Pioneer   | APS-SL3N-240       | 240 GB | 2       | 93    | 0     | 0.26   |
| SK hynix  | HFS256G3BTND-N210A | 256 GB | 7       | 93    | 0     | 0.26   |
| Crucial   | M4-CT256M4SSD3     | 256 GB | 2       | 716   | 507   | 0.26   |
| SanDisk   | ASMT109x- Volume   | 756 GB | 5       | 93    | 0     | 0.26   |
| Mushkin   | MKNSSDSR250GB      | 250 GB | 1       | 93    | 0     | 0.26   |
| ADATA     | SU800              | 128 GB | 33      | 94    | 3     | 0.26   |
| Samsung   | MZNLN128HCGR-000H1 | 128 GB | 1       | 93    | 0     | 0.25   |
| SK hynix  | HFS256G32TNF-N3A0A | 256 GB | 4       | 92    | 0     | 0.25   |
| Samsung   | MZMTD256HAGM-00000 | 256 GB | 1       | 92    | 0     | 0.25   |
| BHT       | WR202HH032G E70... | 32 GB  | 4       | 92    | 0     | 0.25   |
| Lite-On   | PH2-CJ120          | 120 GB | 1       | 92    | 0     | 0.25   |
| Intel     | SSDSC2KI128G8      | 128 GB | 2       | 92    | 0     | 0.25   |
| Verbatim  | Vi500 S3 120GB SSD | 120 GB | 3       | 92    | 0     | 0.25   |
| Apacer    | AS350              | 480 GB | 4       | 92    | 0     | 0.25   |
| Crucial   | CT240BX200SSD1     | 240 GB | 16      | 91    | 0     | 0.25   |
| Crucial   | CT120BX100SSD1     | 120 GB | 4       | 91    | 0     | 0.25   |
| Samsung   | SSD 860 PRO        | 1 TB   | 12      | 91    | 0     | 0.25   |
| SK hynix  | SC308 SATA         | 128 GB | 8       | 123   | 138   | 0.25   |
| HP        | SSD S700           | 1 TB   | 4       | 91    | 0     | 0.25   |
| Platinet  | SSD                | 120 GB | 2       | 91    | 0     | 0.25   |
| Gigabyte  | GP-GSTFS30512GTTD  | 512 GB | 3       | 91    | 0     | 0.25   |
| ADATA     | SU650              | 480 GB | 15      | 140   | 267   | 0.25   |
| Foxline   | FLSSD128X5SE       | 128 GB | 1       | 90    | 0     | 0.25   |
| Faspeed   | H5-60G PLUS        | 64 GB  | 1       | 90    | 0     | 0.25   |
| Crucial   | CT480BX500SSD1     | 480 GB | 73      | 96    | 1     | 0.25   |
| SanDisk   | SD7SB3Q256G1002    | 256 GB | 2       | 232   | 26    | 0.25   |
| Crucial   | CT3500SC           | 500 GB | 1       | 898   | 9     | 0.25   |
| ADATA     | SU800NS38          | 128 GB | 5       | 89    | 0     | 0.25   |
| Lite-On   | CV3-8D128-11 SATA  | 128 GB | 7       | 89    | 0     | 0.25   |
| Intel     | SSDSC2BF240A5L     | 240 GB | 8       | 132   | 10    | 0.25   |
| Plextor   | PX-128M5Pro        | 128 GB | 53      | 89    | 0     | 0.25   |
| Intel     | SSDSCKJF180A5L     | 180 GB | 4       | 89    | 0     | 0.24   |
| China     | SATA SSD           | 240 GB | 17      | 89    | 0     | 0.24   |
| Plextor   | PH6-CE120-L1       | 120 GB | 2       | 89    | 0     | 0.24   |
| Samsung   | MZNLN256HAJQ-000L2 | 256 GB | 6       | 88    | 0     | 0.24   |
| ORICO     | PM200-1T           | 1 TB   | 1       | 88    | 0     | 0.24   |
| Lite-On   | CV3-8D256          | 256 GB | 3       | 87    | 0     | 0.24   |
| Team      | T253LE240G         | 240 GB | 3       | 87    | 0     | 0.24   |
| Kingston  | SA400M8240G        | 240 GB | 21      | 87    | 0     | 0.24   |
| Kingston  | SKC380S3120G       | 120 GB | 1       | 86    | 0     | 0.24   |
| SPCC      | M.2 SSD            | 256 GB | 2       | 86    | 0     | 0.24   |
| Samsung   | SSD 860 PRO        | 512 GB | 27      | 86    | 0     | 0.24   |
| KingSpec  | P4-960             | 960 GB | 1       | 86    | 0     | 0.24   |
| WDC       | WDS120G2G0A-00JH30 | 120 GB | 129     | 93    | 1     | 0.24   |
| Lite-On   | CV3-CE128-11 SATA  | 128 GB | 1       | 86    | 0     | 0.24   |
| Gigabyte  | GP-GSTFS31240GNTD  | 240 GB | 20      | 86    | 0     | 0.24   |
| Mushkin   | MKNSSDEC120GB      | 120 GB | 1       | 86    | 0     | 0.24   |
| SPCC      | SSD                | 512 GB | 23      | 128   | 16    | 0.24   |
| Intel     | SSDSA2M080G2GN     | 80 GB  | 2       | 1445  | 15    | 0.24   |
| ADATA     | SU800              | 256 GB | 33      | 112   | 35    | 0.23   |
| AMD       | R5SL240G           | 240 GB | 12      | 97    | 1     | 0.23   |
| Intel     | SSDMCEAF180A4L     | 180 GB | 1       | 85    | 0     | 0.23   |
| Samsung   | MZNTE128HMGR-000H1 | 128 GB | 1       | 85    | 0     | 0.23   |
| Plextor   | PX-256M3           | 256 GB | 1       | 256   | 2     | 0.23   |
| Samsung   | MZMTD256HAGM-000   | 256 GB | 1       | 85    | 0     | 0.23   |
| Apple     | SSD SM256E         | 256 GB | 2       | 84    | 0     | 0.23   |
| SanDisk   | SD9TB8W512G1001    | 512 GB | 1       | 84    | 0     | 0.23   |
| Vaseky    | V800-350G          | 360 GB | 1       | 84    | 0     | 0.23   |
| Crucial   | CT500MX500SSD4     | 500 GB | 26      | 84    | 0     | 0.23   |
| Goodram   | SSDPR-CX400-256    | 256 GB | 13      | 84    | 0     | 0.23   |
| Colorful  | SL500              | 256 GB | 2       | 84    | 0     | 0.23   |
| Goodram   | SSDPR-CX400-128    | 128 GB | 13      | 84    | 0     | 0.23   |
| Team      | T253X1120G         | 120 GB | 3       | 84    | 0     | 0.23   |
| Transcend | TS256GMTS800       | 256 GB | 4       | 84    | 0     | 0.23   |
| Micron    | M600_MTFDDAK1T0MBF | 1 TB   | 2       | 84    | 0     | 0.23   |
| SPCC      | SSD                | 128 GB | 49      | 84    | 1     | 0.23   |
| Vaseky    | V900-128G          | 128 GB | 2       | 84    | 0     | 0.23   |
| Transcend | TS256GSSD320       | 256 GB | 2       | 84    | 0     | 0.23   |
| Micron    | MTFDDAK960TDN      | 960 GB | 2       | 83    | 0     | 0.23   |
| PNY       | CS900 120GB SSD    | 120 GB | 45      | 83    | 0     | 0.23   |
| Dogfish   | SSD                | 1 TB   | 1       | 83    | 0     | 0.23   |
| Intel     | SSDSC2KI256G8      | 256 GB | 1       | 83    | 0     | 0.23   |
| ADATA     | SP920SS            | 256 GB | 7       | 157   | 7     | 0.23   |
| China     | SATA SSD           | 64 GB  | 17      | 83    | 0     | 0.23   |
| ADATA     | SU800NS38          | 512 GB | 2       | 154   | 3     | 0.22   |
| KingSpec  | NT-128             | 128 GB | 3       | 81    | 0     | 0.22   |
| Seagate   | BarraCuda 120 S... | 500 GB | 5       | 81    | 0     | 0.22   |
| OCZ       | VECTOR180          | 120 GB | 2       | 81    | 0     | 0.22   |
| Lite-On   | LCS-128M6S         | 128 GB | 3       | 81    | 0     | 0.22   |
| Transcend | TS256GMTS400S      | 256 GB | 2       | 81    | 0     | 0.22   |
| Goodram   | IR-SSDPR-S25A-240  | 240 GB | 6       | 81    | 0     | 0.22   |
| Crucial   | CT240BX300SSD1     | 240 GB | 3       | 81    | 0     | 0.22   |
| Micron    | MTFDDAV512TBN      | 512 GB | 1       | 81    | 0     | 0.22   |
| China     | SATA SSD           | 128 GB | 10      | 80    | 0     | 0.22   |
| China     | SATA SSD           | 480 GB | 3       | 80    | 0     | 0.22   |
| ADATA     | SU800              | 1 TB   | 12      | 80    | 0     | 0.22   |
| Crucial   | CT2050MX300SSD1    | 2 TB   | 3       | 89    | 1     | 0.22   |
| ADATA     | SP580              | 120 GB | 13      | 80    | 0     | 0.22   |
| Corsair   | Force LS SSD       | 480 GB | 1       | 80    | 0     | 0.22   |
| Kingston  | RBU-SNS8152S325... | 256 GB | 1       | 80    | 0     | 0.22   |
| Team      | TEAML5Lite3D240G   | 240 GB | 2       | 80    | 0     | 0.22   |
| ADATA     | SU635              | 240 GB | 10      | 80    | 0     | 0.22   |
| Seagate   | BarraCuda SSD Z... | 250 GB | 6       | 79    | 0     | 0.22   |
| Lite-On   | LAT-256M2S         | 256 GB | 1       | 239   | 2     | 0.22   |
| Fordisk   | S860 256G 6Gbps    | 256 GB | 1       | 79    | 0     | 0.22   |
| China     | SSD 120G           | 120 GB | 3       | 79    | 0     | 0.22   |
| WDC       | WDS240G2G0A-00JH30 | 240 GB | 176     | 98    | 1     | 0.22   |
| Lite-On   | CV3-DE512          | 512 GB | 1       | 79    | 0     | 0.22   |
| e2e4      | SSD                | 480 GB | 1       | 79    | 0     | 0.22   |
| PNY       | SSD2SC120G1CS17... | 120 GB | 1       | 79    | 0     | 0.22   |
| Kingston  | SA400S37960G       | 960 GB | 26      | 79    | 0     | 0.22   |
| Seagate   | ST120HM000-1G5142  | 120 GB | 1       | 79    | 0     | 0.22   |
| Kingston  | SUV500MS120G       | 120 GB | 18      | 85    | 68    | 0.22   |
| WDC       | WDS240G2G0B-00EPW0 | 240 GB | 75      | 84    | 1     | 0.21   |
| Samsung   | MZNLN256HAJQ-00000 | 256 GB | 6       | 78    | 0     | 0.21   |
| T-FORCE   | SSD                | 500 GB | 3       | 78    | 0     | 0.21   |
| Crucial   | CT1000MX500SSD1N   | 1 TB   | 1       | 77    | 0     | 0.21   |
| Kingston  | RBU-SNS8100S312... | 128 GB | 4       | 77    | 0     | 0.21   |
| Lite-On   | CMT-64L3M          | 64 GB  | 2       | 149   | 12    | 0.21   |
| Corsair   | Neutron XTI SSD    | 240 GB | 1       | 77    | 0     | 0.21   |
| Lexar     | SSD                | 480 GB | 3       | 77    | 0     | 0.21   |
| Transcend | TS128GSSD370S      | 128 GB | 25      | 77    | 0     | 0.21   |
| KingDian  | S180               | 64 GB  | 13      | 81    | 88    | 0.21   |
| Patriot   | Burst              | 120 GB | 53      | 77    | 0     | 0.21   |
| SanDisk   | SSD PLUS           | 240 GB | 107     | 91    | 1     | 0.21   |
| Gigabyte  | GP-GSTFS30256GTTD  | 256 GB | 1       | 76    | 0     | 0.21   |
| Samsung   | Portable SSD T5    | 500 GB | 13      | 76    | 0     | 0.21   |
| Toshiba   | THNSNJ128G8NY      | 128 GB | 2       | 76    | 0     | 0.21   |
| Palit     | UVS                | 120 GB | 2       | 76    | 0     | 0.21   |
| Lite-On   | CV3-8D256-41 SA... | 256 GB | 2       | 75    | 0     | 0.21   |
| SPCC      | SSD170             | 55 GB  | 4       | 540   | 762   | 0.21   |
| Lite-On   | LCH-512V2S         | 512 GB | 1       | 75    | 0     | 0.21   |
| Kingston  | SA400S37-240G      | 240 GB | 2       | 75    | 0     | 0.21   |
| Transcend | TS64GSSD360S       | 64 GB  | 1       | 75    | 0     | 0.21   |
| Crucial   | CT1000MX500SSD4    | 1 TB   | 25      | 75    | 0     | 0.21   |
| SanDisk   | SDSSDH3 4T00       | 4 TB   | 3       | 75    | 0     | 0.21   |
| Kingston  | SMS200S330G        | 32 GB  | 2       | 246   | 10    | 0.21   |
| OCZ       | ONYX               | 32 GB  | 2       | 105   | 1     | 0.21   |
| China     | 64GB SSD           | 64 GB  | 11      | 74    | 0     | 0.20   |
| SanDisk   | SD7SN3Q128G1002    | 128 GB | 2       | 99    | 1     | 0.20   |
| Reeinno   | ST240GB S4S3       | 240 GB | 1       | 74    | 0     | 0.20   |
| Lite-On   | LCH-256V2S         | 256 GB | 2       | 73    | 0     | 0.20   |
| Vaseky    | V800-32G           | 32 GB  | 1       | 73    | 0     | 0.20   |
| Kingrich  | K9 128GB SATA3 SSD | 128 GB | 1       | 657   | 8     | 0.20   |
| Kingston  | SUV500480G         | 480 GB | 10      | 82    | 114   | 0.20   |
| Lite-On   | LCS-128M6S-HP      | 128 GB | 5       | 72    | 0     | 0.20   |
| ZTC       | SM201-512G         | 512 GB | 1       | 72    | 0     | 0.20   |
| SanDisk   | SSD PLUS           | 1 TB   | 36      | 89    | 29    | 0.20   |
| Samsung   | MZNLN256HAJQ-000L7 | 256 GB | 6       | 72    | 0     | 0.20   |
| Crucial   | CT240BX500SSD1     | 240 GB | 156     | 72    | 0     | 0.20   |
| Intel     | SSDSC2KF256G8 SATA | 256 GB | 1       | 71    | 0     | 0.20   |
| Kingston  | SUV500M8120G       | 120 GB | 7       | 71    | 0     | 0.20   |
| Leven     | JAJS300M120C       | 120 GB | 2       | 71    | 0     | 0.20   |
| Apacer    | AS340              | 120 GB | 9       | 71    | 0     | 0.20   |
| Leven     | JAJS600M256C       | 256 GB | 2       | 71    | 0     | 0.20   |
| Gigabyte  | GP-GSTFS31480GNTD  | 480 GB | 3       | 71    | 0     | 0.20   |
| Vaseky    | V800-500G          | 512 GB | 1       | 71    | 0     | 0.20   |
| Transcend | TS128GSSD370       | 128 GB | 10      | 71    | 0     | 0.20   |
| Kingston  | V300 120G          | 120 GB | 1       | 71    | 0     | 0.20   |
| Apple     | SSD SM128E         | 121 GB | 2       | 1109  | 12    | 0.20   |
| Toshiba   | THNSNH256GCST      | 256 GB | 1       | 71    | 0     | 0.20   |
| Intel     | SSDSCKKF256G8 SATA | 256 GB | 8       | 70    | 0     | 0.19   |
| Kingston  | SUV500MS240G       | 240 GB | 7       | 70    | 0     | 0.19   |
| OCZ       | SABER1000          | 480 GB | 1       | 70    | 0     | 0.19   |
| Samsung   | MZ7LN128HAHQ-000L2 | 128 GB | 12      | 70    | 0     | 0.19   |
| ADATA     | SP900NS38          | 128 GB | 4       | 120   | 254   | 0.19   |
| SanDisk   | SSD i100           | 8 GB   | 3       | 69    | 0     | 0.19   |
| Integral  | V Series SATA SSD  | 240 GB | 9       | 69    | 0     | 0.19   |
| Kingrich  | K9 120GB SATA3     | 128 GB | 1       | 69    | 0     | 0.19   |
| ADATA     | SU800              | 512 GB | 19      | 75    | 2     | 0.19   |
| Intel     | SSDSCKKW512G8      | 512 GB | 1       | 69    | 0     | 0.19   |
| Transcend | TS256GSSD340       | 256 GB | 3       | 69    | 0     | 0.19   |
| Kingston  | RBUSMS180DS3128GH  | 128 GB | 1       | 69    | 0     | 0.19   |
| Micron    | MTFDDAK3T8TCB 0... | 3.8 TB | 1       | 483   | 6     | 0.19   |
| oyunkey   | SSD                | 120 GB | 1       | 68    | 0     | 0.19   |
| ViperTeq  | VT-SSDUP500-240    | 240 GB | 1       | 68    | 0     | 0.19   |
| ADATA     | S596               | 128 GB | 1       | 68    | 0     | 0.19   |
| WDC       | WDS500G1R0B-68A4Z0 | 500 GB | 2       | 68    | 0     | 0.19   |
| ADATA     | SU630              | 240 GB | 35      | 76    | 55    | 0.19   |
| Kingston  | SA400S371920G      | 1.9 TB | 1       | 67    | 0     | 0.19   |
| Plextor   | PX-128M6M          | 128 GB | 4       | 67    | 0     | 0.19   |
| Samsung   | SSD 870 QVO        | 4 TB   | 2       | 67    | 0     | 0.18   |
| KingDian  | P10                | 120 GB | 2       | 69    | 19    | 0.18   |
| Lite-On   | LMT-256L9M-11 M... | 256 GB | 3       | 67    | 0     | 0.18   |
| Vaseky    | V800-240G          | 240 GB | 1       | 67    | 0     | 0.18   |
| Samsung   | SSD 860 QVO        | 4 TB   | 5       | 66    | 0     | 0.18   |
| ADATA     | SP900              | 512 GB | 2       | 66    | 0     | 0.18   |
| KingSpec  | Q-360              | 360 GB | 4       | 66    | 0     | 0.18   |
| GLOWAY    | YCT512GS3-S7 Pro   | 512 GB | 1       | 66    | 0     | 0.18   |
| ADATA     | SU650              | 120 GB | 50      | 75    | 2     | 0.18   |
| Intel     | SSDMCEAW180A4      | 180 GB | 2       | 65    | 0     | 0.18   |
| Corsair   | Neutron GTX SSD    | 120 GB | 3       | 1300  | 100   | 0.18   |
| Plextor   | PX-512S2G          | 512 GB | 1       | 65    | 0     | 0.18   |
| SPCC      | SSD                | 55 GB  | 9       | 361   | 452   | 0.18   |
| SanDisk   | SD9TB8W1T001001    | 1 TB   | 2       | 65    | 0     | 0.18   |
| EMTEC     | X250               | 512 GB | 1       | 65    | 0     | 0.18   |
| Team      | T253X2128G         | 128 GB | 1       | 65    | 0     | 0.18   |
| Kingston  | SQ500S37240G       | 240 GB | 3       | 64    | 0     | 0.18   |
| Plextor   | PX-128S3C          | 128 GB | 12      | 64    | 0     | 0.18   |
| Intel     | SSDSCKKW256H6      | 256 GB | 2       | 64    | 0     | 0.18   |
| SanDisk   | SSD i110           | 32 GB  | 1       | 64    | 0     | 0.18   |
| Micron    | 1100_MTFDDAV256TBN | 256 GB | 62      | 71    | 63    | 0.18   |
| SanDisk   | SD8TN8U512G1001    | 512 GB | 2       | 64    | 0     | 0.18   |
| WDC       | WDS100T2B0A        | 1 TB   | 1       | 128   | 1     | 0.18   |
| Kingston  | RBU-SNS8151S396GG  | 96 GB  | 2       | 202   | 4     | 0.18   |
| Team      | T2535T240G         | 240 GB | 1       | 63    | 0     | 0.17   |
| Pioneer   | APS-SL3N-256       | 256 GB | 1       | 63    | 0     | 0.17   |
| Lenovo    | SSD SL700 120G     | 120 GB | 4       | 63    | 0     | 0.17   |
| Patriot   | P200               | 256 GB | 5       | 63    | 0     | 0.17   |
| Kingston  | SUV400S37 120G     | 120 GB | 1       | 63    | 0     | 0.17   |
| Apacer    | AS350              | 240 GB | 15      | 63    | 0     | 0.17   |
| Plextor   | PX-128M6S          | 128 GB | 27      | 72    | 79    | 0.17   |
| Transcend | TS128GMTS400S      | 128 GB | 2       | 63    | 0     | 0.17   |
| Transcend | TS240GMTS420S      | 240 GB | 8       | 63    | 0     | 0.17   |
| Intel     | SSDSC2KW010T8      | 1 TB   | 1       | 504   | 7     | 0.17   |
| Lite-On   | LCS-128L9S-11 2... | 128 GB | 1       | 62    | 0     | 0.17   |
| SanDisk   | SDSSDH2064G        | 64 GB  | 1       | 62    | 0     | 0.17   |
| KingSpec  | P4-480             | 480 GB | 2       | 62    | 0     | 0.17   |
| China     | SATA SSD           | 512 GB | 2       | 62    | 0     | 0.17   |
| Intel     | SSDSC2BF480A5L     | 480 GB | 1       | 62    | 0     | 0.17   |
| Kingrich  | SSD 120G           | 120 GB | 1       | 62    | 0     | 0.17   |
| Lexar     | 512GB SSD          | 512 GB | 2       | 62    | 0     | 0.17   |
| Netac     | W800S 512GB SSD    | 512 GB | 1       | 62    | 0     | 0.17   |
| SMI       | SSD DISK           | 500 GB | 1       | 62    | 0     | 0.17   |
| OCZ       | VERTEX460          | 240 GB | 2       | 61    | 0     | 0.17   |
| Transcend | TS256GMTS430S      | 256 GB | 8       | 61    | 0     | 0.17   |
| Toshiba   | Q200 EX            | 240 GB | 1       | 61    | 0     | 0.17   |
| SK hynix  | HFS128G39TNF-N3A0A | 128 GB | 6       | 61    | 0     | 0.17   |
| SanDisk   | SDSSDH3256G        | 256 GB | 2       | 61    | 0     | 0.17   |
| Plextor   | PX-256M6S          | 256 GB | 10      | 69    | 214   | 0.17   |
| SPCC      | M.2 SSD            | 120 GB | 4       | 106   | 1     | 0.17   |
| Hoodisk   | SSD                | 256 GB | 3       | 61    | 0     | 0.17   |
| ADATA     | SU900              | 256 GB | 7       | 61    | 1     | 0.17   |
| Gigabyte  | GP-GSTFS31100TNTD  | 1 TB   | 1       | 61    | 0     | 0.17   |
| Transcend | TS128GMTS400       | 128 GB | 4       | 60    | 0     | 0.17   |
| Samsung   | MZNTE256HMHP-000L2 | 256 GB | 2       | 60    | 0     | 0.17   |
| Lite-On   | LCH-512V2S-11 2... | 512 GB | 1       | 60    | 0     | 0.17   |
| Phison    | 128GB PS3109-S9    | 128 GB | 1       | 121   | 1     | 0.17   |
| Samsung   | MZ7LN128HAHQ-000L1 | 128 GB | 2       | 60    | 0     | 0.17   |
| SPCC      | SSDB28             | 128 GB | 2       | 76    | 1     | 0.17   |
| Transcend | TS960GMTS820S      | 960 GB | 1       | 60    | 0     | 0.17   |
| Toshiba   | THNSN9480GESG      | 480 GB | 1       | 60    | 0     | 0.17   |
| Leven     | JAJS600M512C       | 512 GB | 4       | 60    | 0     | 0.16   |
| SUNEAST   | SSD SE800          | 1.9 TB | 1       | 60    | 0     | 0.16   |
| KingSpec  | P3-512             | 512 GB | 10      | 76    | 181   | 0.16   |
| Intel     | SSDSC2KB960G8      | 960 GB | 7       | 59    | 0     | 0.16   |
| HP        | SSD S700           | 250 GB | 15      | 59    | 0     | 0.16   |
| Patriot   | P210               | 256 GB | 1       | 59    | 0     | 0.16   |
| Lite-On   | CV3-8D512-11 SATA  | 512 GB | 1       | 59    | 0     | 0.16   |
| PNY       | SSD2SC240G1CS17... | 240 GB | 1       | 59    | 0     | 0.16   |
| Phison    | SATA SSD           | 256 GB | 4       | 59    | 0     | 0.16   |
| KingDian  | S400               | 240 GB | 1       | 59    | 0     | 0.16   |
| Kingston  | RBU-SUS151S364GD   | 64 GB  | 4       | 59    | 0     | 0.16   |
| AGI       | AGI240G18AI238     | 240 GB | 1       | 59    | 0     | 0.16   |
| Dogfish   | SSD                | 128 GB | 1       | 59    | 0     | 0.16   |
| TEKET     | SA18-032M-4F       | 32 GB  | 2       | 59    | 0     | 0.16   |
| Plextor   | PX-512M6Pro        | 512 GB | 1       | 58    | 0     | 0.16   |
| AMD       | R3SL120G           | 120 GB | 28      | 58    | 1     | 0.16   |
| BIWIN     | SSD                | 120 GB | 2       | 58    | 0     | 0.16   |
| HP        | SSD S700 Pro       | 256 GB | 2       | 58    | 0     | 0.16   |
| Kingston  | SKC380S3240G       | 240 GB | 1       | 58    | 0     | 0.16   |
| Zheino    | CHN 25SATAC3 120   | 120 GB | 1       | 58    | 0     | 0.16   |
| Lite-On   | IT LCS-128L9S-HP   | 128 GB | 3       | 58    | 0     | 0.16   |
| Kingston  | RBUSNS8180DS3256GJ | 256 GB | 5       | 74    | 1     | 0.16   |
| tigo      | SSD                | 120 GB | 1       | 57    | 0     | 0.16   |
| KingSpec  | MSH-256            | 256 GB | 3       | 57    | 0     | 0.16   |
| Intenso   | SSD Sata III       | 120 GB | 9       | 80    | 96    | 0.16   |
| China     | 512GB SSD          | 512 GB | 2       | 57    | 0     | 0.16   |
| Lite-On   | LMT-32L3M-HP       | 32 GB  | 3       | 57    | 0     | 0.16   |
| Goldkey   | GKH84-64GB         | 64 GB  | 1       | 57    | 0     | 0.16   |
| Crucial   | CT512M550SSD3      | 512 GB | 4       | 108   | 176   | 0.16   |
| DeTech    | SSD                | 120 GB | 1       | 57    | 0     | 0.16   |
| China     | SSD                | 1 TB   | 6       | 57    | 0     | 0.16   |
| TCSUNBOW  | X3                 | 64 GB  | 2       | 56    | 0     | 0.16   |
| SanDisk   | X600 M.2 2280 SATA | 256 GB | 1       | 56    | 0     | 0.16   |
| Lite-On   | IT L8T-128L9G-HP   | 128 GB | 1       | 56    | 0     | 0.16   |
| Apacer    | AS340              | 480 GB | 9       | 56    | 0     | 0.16   |
| PNY       | SSD2SC240G1SAHT... | 240 GB | 1       | 56    | 0     | 0.15   |
| Super ... | FTM50N325H         | 500 GB | 2       | 56    | 0     | 0.15   |
| Crucial   | CT1000BX500SSD1    | 1 TB   | 18      | 56    | 0     | 0.15   |
| Plextor   | PX-256M6Pro        | 256 GB | 3       | 91    | 2     | 0.15   |
| Gigabyte  | GP-GSTFS31256GTND  | 256 GB | 1       | 56    | 0     | 0.15   |
| WDC       | WDBNCE0010PNC      | 1 TB   | 3       | 55    | 0     | 0.15   |
| Plextor   | PX-128M8VC         | 128 GB | 1       | 55    | 0     | 0.15   |
| Smartbuy  | mSata              | 256 GB | 2       | 55    | 0     | 0.15   |
| Team      | T253LE120G         | 120 GB | 2       | 55    | 0     | 0.15   |
| PNY       | SSD2SC120G1SA75... | 120 GB | 1       | 55    | 0     | 0.15   |
| Patriot   | P200               | 1 TB   | 4       | 78    | 11    | 0.15   |
| Samsung   | MZYTE256HMHP-000L2 | 256 GB | 1       | 55    | 0     | 0.15   |
| Toshiba   | KSG60ZMV256G       | 256 GB | 1       | 55    | 0     | 0.15   |
| ADATA     | SU630              | 480 GB | 11      | 66    | 195   | 0.15   |
| OWC       | Neptune 6G SSD     | 480 GB | 2       | 55    | 0     | 0.15   |
| Apacer    | AST280             | 240 GB | 2       | 55    | 0     | 0.15   |
| SanDisk   | SD6PP4M-256G-1006  | 256 GB | 3       | 175   | 2     | 0.15   |
| TAMMUZ    | SSD                | 128 GB | 1       | 54    | 0     | 0.15   |
| SanDisk   | SSD i100           | 64 GB  | 1       | 54    | 0     | 0.15   |
| WDC       | WDS480G2G0B-00EPW0 | 480 GB | 10      | 54    | 0     | 0.15   |
| Goodram   | SSDPR-CL100-480-G2 | 480 GB | 4       | 54    | 0     | 0.15   |
| Aoluska   | A6-120G            | 120 GB | 1       | 54    | 0     | 0.15   |
| Samsung   | MCCOE64G8MPP-0VA   | 64 GB  | 1       | 377   | 6     | 0.15   |
| Netac     | SSD                | 1 TB   | 1       | 53    | 0     | 0.15   |
| SanDisk   | SD8SBAT-256G-1006  | 256 GB | 2       | 53    | 0     | 0.15   |
| Londisk   | SSD                | 240 GB | 2       | 53    | 0     | 0.15   |
| Transcend | TS64GMTS800S       | 64 GB  | 1       | 53    | 0     | 0.15   |
| Kingston  | SHPM2280P2-240G    | 240 GB | 1       | 1557  | 28    | 0.15   |
| ADATA     | SU635              | 480 GB | 2       | 106   | 103   | 0.15   |
| Goodram   | SSDPR-CL100-120-G2 | 120 GB | 9       | 53    | 0     | 0.15   |
| Intel     | SSDSA2M160G2LE     | 160 GB | 2       | 1075  | 16    | 0.15   |
| Samsung   | MZMTD128HAFV-000H1 | 128 GB | 1       | 53    | 0     | 0.15   |
| Zheino    | CHN-25SATAA3-480   | 480 GB | 2       | 53    | 0     | 0.15   |
| China     | SATA3 128GB SSD    | 128 GB | 3       | 53    | 0     | 0.15   |
| Crucial   | CT1024M550SSD1     | 1 TB   | 1       | 897   | 16    | 0.14   |
| Transcend | TS64GSSD370S       | 64 GB  | 3       | 52    | 0     | 0.14   |
| Lite-On   | LGT-128M6G         | 128 GB | 1       | 52    | 0     | 0.14   |
| China     | SSD                | 128 GB | 33      | 52    | 1     | 0.14   |
| Maxtor    | Z1 SSD             | 240 GB | 5       | 52    | 0     | 0.14   |
| Intel     | SSDSCKKB240G8      | 240 GB | 1       | 52    | 0     | 0.14   |
| China     | SSD                | 256 GB | 14      | 52    | 1     | 0.14   |
| Lite-On   | L8H-128V2G-11 M... | 128 GB | 3       | 52    | 0     | 0.14   |
| Phison    | SATA SSD           | 960 GB | 3       | 52    | 0     | 0.14   |
| Hikvision | HS-SSD-C100 240G   | 240 GB | 2       | 52    | 0     | 0.14   |
| Samsung   | MZ7LN256HAJQ-000L2 | 256 GB | 16      | 52    | 0     | 0.14   |
| IPLEX     | TITAN256XP         | 256 GB | 1       | 52    | 0     | 0.14   |
| Team      | T2535T120G         | 120 GB | 3       | 100   | 3     | 0.14   |
| Crucial   | CT250BX100SSD1     | 250 GB | 31      | 52    | 1     | 0.14   |
| Team      | L7 EVO SSD         | 64 GB  | 1       | 51    | 0     | 0.14   |
| Kingmax   | SSD                | 240 GB | 5       | 134   | 280   | 0.14   |
| China     | SATA SSD           | 16 GB  | 1       | 1295  | 24    | 0.14   |
| Lite-On   | LMT-19nmBGA-128G   | 128 GB | 1       | 51    | 0     | 0.14   |
| ADATA     | SP610              | 128 GB | 3       | 51    | 0     | 0.14   |
| ADATA     | SU650NS38          | 480 GB | 1       | 51    | 0     | 0.14   |
| Toshiba   | THNSFC128GBSJ      | 128 GB | 1       | 51    | 0     | 0.14   |
| SK hynix  | SHGS31-1000GS-2    | 1 TB   | 7       | 51    | 0     | 0.14   |
| Seagate   | ZA1920NM10001      | 1.9 TB | 4       | 51    | 0     | 0.14   |
| Lite-On   | IT LCS-256L9S      | 256 GB | 1       | 51    | 0     | 0.14   |
| Micron    | MTFDDAK256MAY-1... | 256 GB | 2       | 870   | 16    | 0.14   |
| Intel     | SSDSCKKF512G8 SATA | 512 GB | 2       | 50    | 0     | 0.14   |
| XrayDisk  | SSD                | 120 GB | 2       | 50    | 0     | 0.14   |
| Samsung   | SSD PB22-CS3 FD... | 256 GB | 1       | 50    | 0     | 0.14   |
| OCZ       | INTREPID 3800      | 400 GB | 1       | 50    | 0     | 0.14   |
| Crucial   | CT120BX500SSD1     | 120 GB | 102     | 52    | 1     | 0.14   |
| Corsair   | Neutron GTX SSD    | 480 GB | 1       | 49    | 0     | 0.14   |
| KingDian  | S280               | 240 GB | 12      | 49    | 0     | 0.14   |
| KingSpec  | NT-256             | 256 GB | 7       | 49    | 0     | 0.14   |
| ADATA     | SU800              | 2 TB   | 5       | 54    | 1     | 0.14   |
| Kingston  | RBUSNS8180DS3128GH | 128 GB | 7       | 49    | 0     | 0.14   |
| Micron    | MTFDDAV256MBF-1... | 256 GB | 7       | 49    | 0     | 0.14   |
| Dogfish   | SSD                | 256 GB | 4       | 49    | 0     | 0.14   |
| V-GeN     | V-GEN12AS19AR12... | 120 GB | 1       | 49    | 0     | 0.14   |
| WDC       | WDS100T1R0A-68A4W0 | 1 TB   | 2       | 49    | 0     | 0.13   |
| KingDian  | S200               | 120 GB | 2       | 49    | 0     | 0.13   |
| Transcend | TSA                | 1 TB   | 1       | 49    | 0     | 0.13   |
| SanDisk   | SDSA5DK 32G        | 32 GB  | 1       | 49    | 0     | 0.13   |
| Vaseky    | V800-128G          | 128 GB | 2       | 48    | 0     | 0.13   |
| HP        | SSD S700 Pro       | 1 TB   | 1       | 48    | 0     | 0.13   |
| LDLC      | F6+M.2 480         | 480 GB | 2       | 48    | 0     | 0.13   |
| Lexar     | SSD                | 240 GB | 3       | 48    | 0     | 0.13   |
| LDLC      | SSD F7 PLUS 3D ... | 240 GB | 1       | 48    | 0     | 0.13   |
| Apacer    | AS350              | 512 GB | 7       | 57    | 1     | 0.13   |
| Apacer    | AS350              | 120 GB | 10      | 48    | 1     | 0.13   |
| ADATA     | SU630              | 960 GB | 2       | 73    | 1     | 0.13   |
| OCZ       | VECTOR180          | 480 GB | 1       | 48    | 0     | 0.13   |
| SK hynix  | HFS128G32MND-3212A | 128 GB | 1       | 48    | 0     | 0.13   |
| GeIL      | R3 120G            | 120 GB | 1       | 47    | 0     | 0.13   |
| Lite-On   | IT LMH-256V2M      | 256 GB | 1       | 47    | 0     | 0.13   |
| China     | 80GB SSD           | 80 GB  | 2       | 47    | 0     | 0.13   |
| FORESEE   | 64GB SSD           | 64 GB  | 4       | 47    | 0     | 0.13   |
| WDC       | WDS400T2B0A-00SM50 | 4 TB   | 2       | 47    | 0     | 0.13   |
| Teclast   | 120GB S500         | 120 GB | 1       | 47    | 0     | 0.13   |
| Verbatim  | Vi550 S3 SSD       | 128 GB | 2       | 47    | 0     | 0.13   |
| GLOWAY    | FER120GS3-S7       | 120 GB | 4       | 46    | 0     | 0.13   |
| Apacer    | AS350              | 128 GB | 20      | 46    | 0     | 0.13   |
| KingSpec  | Q-180              | 180 GB | 5       | 53    | 188   | 0.13   |
| China     | SATA3 240GB SSD    | 240 GB | 4       | 69    | 2     | 0.13   |
| Samsung   | SSD 870 QVO        | 8 TB   | 2       | 46    | 0     | 0.13   |
| China     | SSD                | 240 GB | 18      | 60    | 1     | 0.13   |
| AMD       | R5SL120G           | 120 GB | 14      | 55    | 1     | 0.13   |
| AMD       | R3SL60G            | 64 GB  | 3       | 46    | 0     | 0.13   |
| Intel     | SSDSC2KG240G8      | 240 GB | 2       | 46    | 0     | 0.13   |
| Crucial   | CT128M550SSD1      | 128 GB | 5       | 193   | 25    | 0.13   |
| SK hynix  | HFS256G32TNH-73A0A | 256 GB | 4       | 45    | 0     | 0.13   |
| SanDisk   | SD5SF2032G1010E    | 32 GB  | 1       | 45    | 0     | 0.13   |
| ADATA     | SU800NS38          | 1 TB   | 3       | 45    | 0     | 0.13   |
| Kingston  | RBU-SC152S37128GG2 | 128 GB | 1       | 45    | 0     | 0.12   |
| Zheino    | CHN mSATA02M 128   | 128 GB | 1       | 45    | 0     | 0.12   |
| BHT       | WR202H0032G E70... | 32 GB  | 1       | 45    | 0     | 0.12   |
| Intel     | SSDSCKKF256H6L     | 256 GB | 2       | 51    | 29    | 0.12   |
| Transcend | TS512GSSD230S      | 512 GB | 1       | 45    | 0     | 0.12   |
| WDC       | WDS500G2B0B        | 500 GB | 6       | 45    | 0     | 0.12   |
| China     | M10C               | 128 GB | 1       | 44    | 0     | 0.12   |
| SanDisk   | Z400s 2.5 7MM      | 256 GB | 1       | 44    | 0     | 0.12   |
| Transcend | TS512GMTS800       | 512 GB | 1       | 44    | 0     | 0.12   |
| Lite-On   | CV3-CE256-11 SATA  | 256 GB | 2       | 44    | 0     | 0.12   |
| KingSpec  | P3-1TB             | 1 TB   | 2       | 44    | 0     | 0.12   |
| Hikvision | HS-SSD-E100 128G   | 128 GB | 1       | 133   | 2     | 0.12   |
| Silicon   | SATA3 128GB SSD    | 128 GB | 1       | 44    | 0     | 0.12   |
| PRETEC    | G2000 SSD          | 32 GB  | 1       | 44    | 0     | 0.12   |
| XPG       | SX950U             | 240 GB | 2       | 44    | 0     | 0.12   |
| Plextor   | PX-512M3           | 512 GB | 1       | 1402  | 31    | 0.12   |
| KingSpec  | P4-60              | 64 GB  | 1       | 43    | 0     | 0.12   |
| KingSpec  | Q-720              | 720 GB | 4       | 43    | 0     | 0.12   |
| Transcend | TS64GMSA370        | 64 GB  | 3       | 43    | 0     | 0.12   |
| Samsung   | MZ7LN256HAJQ-000L7 | 256 GB | 4       | 43    | 0     | 0.12   |
| China     | SSD                | 360 GB | 9       | 43    | 0     | 0.12   |
| Ramsta    | SSD S800           | 480 GB | 1       | 43    | 0     | 0.12   |
| BIWIN     | SSD                | 128 GB | 7       | 96    | 442   | 0.12   |
| Intel     | SSDSCKKF128G8 SATA | 128 GB | 5       | 59    | 3     | 0.12   |
| Intel     | SSDSCKKF010X6      | 1 TB   | 1       | 42    | 0     | 0.12   |
| China     | SSD                | 120 GB | 23      | 60    | 3     | 0.12   |
| PNY       | SSD2SC120G5LC70... | 120 GB | 1       | 42    | 0     | 0.12   |
| China     | SSD128G            | 128 GB | 1       | 42    | 0     | 0.12   |
| FORESEE   | 128GB SSD          | 128 GB | 11      | 42    | 0     | 0.12   |
| SanDisk   | SD8SFAT128G1122    | 128 GB | 1       | 42    | 0     | 0.12   |
| Apacer    | AS350              | 256 GB | 10      | 42    | 0     | 0.12   |
| Goodram   | SSDPR-CX400-128-G2 | 128 GB | 2       | 42    | 0     | 0.12   |
| Intel     | SSDSC2KG480G8      | 480 GB | 1       | 42    | 0     | 0.12   |
| KingSpec  | NT-64              | 64 GB  | 1       | 41    | 0     | 0.11   |
| Crucial   | CT500MX500SSD4N    | 500 GB | 1       | 41    | 0     | 0.11   |
| PNY       | SSD2SC240G5SA75... | 240 GB | 1       | 41    | 0     | 0.11   |
| KingDian  | S280               | 1 TB   | 3       | 41    | 0     | 0.11   |
| Union ... | RTOTJ128VGD2EYX    | 128 GB | 3       | 41    | 0     | 0.11   |
| RCESSD    | SSD                | 512 GB | 1       | 41    | 0     | 0.11   |
| Team      | TM8PS7256G         | 256 GB | 4       | 41    | 0     | 0.11   |
| GALAX     | TA1D0240A          | 240 GB | 1       | 41    | 0     | 0.11   |
| Intel     | SSDSC2KW128G8      | 128 GB | 7       | 40    | 0     | 0.11   |
| SanDisk   | SD8SBAT256G1122    | 256 GB | 8       | 40    | 0     | 0.11   |
| KingDian  | S280-240GB         | 240 GB | 9       | 70    | 168   | 0.11   |
| Goodram   | SSDPR-S400U-120-80 | 120 GB | 1       | 40    | 0     | 0.11   |
| Lite-On   | CV3-8D128          | 128 GB | 3       | 40    | 0     | 0.11   |
| Hikvision | HS-SSD-E100 1024G  | 1 TB   | 1       | 40    | 0     | 0.11   |
| WDC       | WDS100T2G0A-00JH30 | 1 TB   | 9       | 40    | 0     | 0.11   |
| KingDian  | P10                | 240 GB | 1       | 39    | 0     | 0.11   |
| XrayDisk  | SSD                | 512 GB | 1       | 39    | 0     | 0.11   |
| Netac     | SSD                | 256 GB | 9       | 39    | 0     | 0.11   |
| Seagate   | ST480HM000         | 480 GB | 1       | 39    | 0     | 0.11   |
| WDC       | WDS480G2G0A-00JH30 | 480 GB | 30      | 40    | 1     | 0.11   |
| Corsair   | Force LX SSD       | 256 GB | 1       | 39    | 0     | 0.11   |
| Lite-On   | LMT-128M6M-HP      | 128 GB | 1       | 39    | 0     | 0.11   |
| PNY       | CS900 250GB SSD    | 250 GB | 3       | 39    | 0     | 0.11   |
| Verbatim  | Vi500 S3 240GB SSD | 240 GB | 2       | 38    | 0     | 0.11   |
| Team      | T253X2001T         | 1 TB   | 6       | 38    | 0     | 0.11   |
| PNY       | SSD2SC240G1CS27... | 240 GB | 1       | 38    | 0     | 0.11   |
| Kingston  | SH103S3480G        | 480 GB | 1       | 38    | 0     | 0.11   |
| ADATA     | SU655              | 480 GB | 2       | 38    | 0     | 0.11   |
| KingDian  | S200               | 64 GB  | 8       | 69    | 17    | 0.11   |
| DOGFISH   | SSD                | 256 GB | 1       | 38    | 0     | 0.11   |
| Lite-On   | CV8-8E256-11 SATA  | 256 GB | 2       | 38    | 0     | 0.11   |
| Micron    | MTFDDAV256TBN      | 256 GB | 1       | 114   | 2     | 0.10   |
| Lite-On   | CV3-DE256          | 256 GB | 5       | 38    | 0     | 0.10   |
| Faspeed   | K5-120G            | 120 GB | 1       | 38    | 0     | 0.10   |
| KingSpec  | T-64               | 64 GB  | 4       | 46    | 2     | 0.10   |
| Neo Forza | NFS011SA396-600... | 960 GB | 1       | 341   | 8     | 0.10   |
| Zheino    | CHN-mSATAM3-128    | 128 GB | 1       | 37    | 0     | 0.10   |
| Drevo     | X1-60G             | 64 GB  | 1       | 37    | 0     | 0.10   |
| Apacer    | 32GB SATA Flash... | 32 GB  | 2       | 37    | 0     | 0.10   |
| BAITITON  | BT58SSD15S         | 2 TB   | 1       | 37    | 0     | 0.10   |
| Plextor   | PX-128M6Pro        | 128 GB | 10      | 39    | 1     | 0.10   |
| SanDisk   | SDSSDHP64G         | 64 GB  | 1       | 37    | 0     | 0.10   |
| ADATA     | SP550              | 120 GB | 33      | 38    | 1     | 0.10   |
| SanDisk   | SSD G5 BICS4       | 500 GB | 11      | 37    | 0     | 0.10   |
| LDLC      | SSD                | 240 GB | 1       | 36    | 0     | 0.10   |
| Micron    | MTFDDAK512MAY-1... | 512 GB | 1       | 624   | 16    | 0.10   |
| Toshiba   | KSG60ZMV256G M.... | 256 GB | 9       | 42    | 23    | 0.10   |
| Lite-On   | LSS-32L6G-HP       | 32 GB  | 4       | 148   | 254   | 0.10   |
| Transcend | TS512GMSA370       | 512 GB | 2       | 36    | 0     | 0.10   |
| Intenso   | SSD                | 120 GB | 3       | 36    | 0     | 0.10   |
| Intenso   | SSD SATAIII        | 480 GB | 8       | 36    | 0     | 0.10   |
| QUMO      | SSD                | 240 GB | 2       | 36    | 0     | 0.10   |
| SK hynix  | HFS256G39TNF-N3A0A | 256 GB | 4       | 35    | 0     | 0.10   |
| Lexar     | 256GB SSD          | 256 GB | 9       | 35    | 0     | 0.10   |
| PNY       | SSD2SC120G726A1... | 120 GB | 1       | 35    | 0     | 0.10   |
| Transcend | TS256GMSA370       | 256 GB | 1       | 35    | 0     | 0.10   |
| Seagate   | BarraCuda SSD Z... | 500 GB | 9       | 35    | 0     | 0.10   |
| KingSpec  | P3-128             | 128 GB | 12      | 77    | 13    | 0.10   |
| ADATA     | XM11               | 120 GB | 1       | 105   | 2     | 0.10   |
| Lite-On   | IT LMT-128L9M      | 128 GB | 2       | 35    | 0     | 0.10   |
| Zheino    | CHN 25SATAS3 256   | 256 GB | 2       | 34    | 0     | 0.10   |
| Plextor   | PX-256S3C          | 256 GB | 1       | 34    | 0     | 0.10   |
| Innodisk  | Corp. - mSATA 3... | 128 GB | 1       | 34    | 0     | 0.10   |
| Toshiba   | KHK61RSE1T92       | 1.9 TB | 8       | 34    | 0     | 0.10   |
| PNY       | SSD2SC240G1LC70... | 240 GB | 2       | 34    | 0     | 0.10   |
| Transcend | TS120GMTS420S      | 120 GB | 17      | 36    | 1     | 0.10   |
| Plextor   | PX-64M5M           | 64 GB  | 1       | 34    | 0     | 0.10   |
| Crucial   | FCCT256M4SSD1      | 256 GB | 1       | 34    | 0     | 0.09   |
| ZOTAC     | SATA SSD           | 120 GB | 2       | 34    | 0     | 0.09   |
| Kingston  | RBUSNS8180DS3128GJ | 128 GB | 9       | 34    | 0     | 0.09   |
| SanDisk   | SD8SN8U128G1122    | 128 GB | 1       | 34    | 0     | 0.09   |
| Samsung   | MZNLH512HALU-00000 | 512 GB | 6       | 34    | 0     | 0.09   |
| ADATA     | SX950              | 240 GB | 1       | 34    | 0     | 0.09   |
| SMI       | SSD DISK           | 256 GB | 1       | 33    | 0     | 0.09   |
| Teclast   | 256GB NA850-2280   | 256 GB | 1       | 33    | 0     | 0.09   |
| AMD       | R5S240GBSF         | 240 GB | 1       | 33    | 0     | 0.09   |
| Lite-On   | LMH-256V2M-11 M... | 256 GB | 4       | 33    | 0     | 0.09   |
| China     | SATA3 256GB SSD    | 256 GB | 2       | 33    | 0     | 0.09   |
| Intel     | SSDSA1MH080G1HP    | 80 GB  | 1       | 33    | 0     | 0.09   |
| RECADATA  | RD-S325MCN-N2563   | 240 GB | 1       | 33    | 0     | 0.09   |
| SMI       | SSD DISK           | 497 GB | 1       | 33    | 0     | 0.09   |
| SanDisk   | SD6SB1M-032G-1006  | 32 GB  | 1       | 33    | 0     | 0.09   |
| KingDian  | S280               | 120 GB | 9       | 33    | 0     | 0.09   |
| TCSUNBOW  | X3                 | 240 GB | 3       | 33    | 0     | 0.09   |
| Goodram   | IRP-SSDPR-S25C-512 | 512 GB | 3       | 33    | 0     | 0.09   |
| Corsair   | CSSD-F120GB3-BK    | 120 GB | 2       | 58    | 509   | 0.09   |
| KingFast  | SSD                | 120 GB | 6       | 41    | 512   | 0.09   |
| Smartbuy  | mSata              | 128 GB | 2       | 32    | 0     | 0.09   |
| Lite-On   | LST-32S9G-11 SATA  | 32 GB  | 2       | 32    | 0     | 0.09   |
| Samsung   | SSD PM851          | 128 GB | 1       | 32    | 0     | 0.09   |
| KingSpec  | ACSC4M512mSA       | 506 GB | 1       | 32    | 0     | 0.09   |
| OCZ       | VERTEX4            | 80 GB  | 1       | 129   | 3     | 0.09   |
| Lite-On   | L8T-128L6G-HP      | 128 GB | 2       | 32    | 640   | 0.09   |
| SanDisk   | SDSSDXP120G        | 120 GB | 1       | 32    | 0     | 0.09   |
| Goodram   | SSDPR-CL100-240-G2 | 240 GB | 3       | 32    | 0     | 0.09   |
| Toshiba   | THNSNB062GMCJ      | 64 GB  | 1       | 32    | 0     | 0.09   |
| China     | Solid              | 480 GB | 3       | 31    | 0     | 0.09   |
| Transcend | TS128GMTS800       | 128 GB | 5       | 31    | 0     | 0.09   |
| Transcend | TS1TMTS800         | 1 TB   | 1       | 31    | 0     | 0.09   |
| Transcend | TS512GMTS400       | 512 GB | 1       | 31    | 0     | 0.09   |
| Crucial   | CT1000BX100SSD1    | 1 TB   | 1       | 31    | 0     | 0.09   |
| SPCC      | 2.5�� SSD          | 1 TB   | 1       | 31    | 0     | 0.09   |
| Kingston  | RBUSNS8180DS3512GJ | 512 GB | 4       | 31    | 0     | 0.09   |
| SUNEAST   | SSD SE800          | 512 GB | 1       | 31    | 0     | 0.09   |
| China     | T480               | 480 GB | 2       | 65    | 138   | 0.09   |
| EMTEC     | X150               | 240 GB | 1       | 31    | 0     | 0.09   |
| Smartbuy  | SSD                | 512 GB | 2       | 31    | 0     | 0.09   |
| Lexar     | 128GB SSD          | 128 GB | 7       | 31    | 0     | 0.09   |
| KingSpec  | KSD-SA25.7-016MJ   | 16 GB  | 2       | 30    | 0     | 0.08   |
| Colorful  | SL500              | 480 GB | 3       | 38    | 65    | 0.08   |
| Micron    | MTFDDAK256TDL      | 256 GB | 5       | 30    | 0     | 0.08   |
| SK hynix  | SC401 SATA         | 512 GB | 5       | 135   | 547   | 0.08   |
| Intenso   | SSD Sata III       | 256 GB | 9       | 34    | 57    | 0.08   |
| SK hynix  | SC210 mSATA        | 256 GB | 3       | 340   | 21    | 0.08   |
| QUMO      | SSD                | 120 GB | 4       | 175   | 255   | 0.08   |
| China     | SH00R240GB         | 240 GB | 2       | 30    | 0     | 0.08   |
| Intenso   | SSD Sata III       | 128 GB | 10      | 42    | 206   | 0.08   |
| SanDisk   | pSSD               | 128 GB | 17      | 30    | 2     | 0.08   |
| PNY       | SSD2SC120G1CS17... | 120 GB | 2       | 30    | 0     | 0.08   |
| Lite-On   | LCH-128V2S         | 128 GB | 3       | 30    | 0     | 0.08   |
| SK hynix  | HFS128G39MNC-3510A | 128 GB | 1       | 30    | 0     | 0.08   |
| LDLC      | F7+240GB           | 240 GB | 2       | 29    | 0     | 0.08   |
| SanDisk   | SDSA5DK-016G-1006  | 16 GB  | 1       | 29    | 0     | 0.08   |
| KingPower | 1108 SSD           | 64 GB  | 1       | 29    | 0     | 0.08   |
| Lite-On   | LMT-64M6M-HP       | 64 GB  | 2       | 102   | 507   | 0.08   |
| Patriot   | SDVPSA1910128      | 128 GB | 1       | 29    | 0     | 0.08   |
| Samsung   | SSD Thin uSATA ... | 128 GB | 1       | 378   | 12    | 0.08   |
| KingSpec  | MT-128             | 128 GB | 4       | 29    | 0     | 0.08   |
| EMTEC     | X150               | 480 GB | 1       | 29    | 0     | 0.08   |
| Crucial   | CT480BX200SSD1     | 480 GB | 3       | 28    | 0     | 0.08   |
| Patriot   | Spark              | 256 GB | 2       | 28    | 0     | 0.08   |
| China     | Mit-SSD512A        | 512 GB | 1       | 28    | 0     | 0.08   |
| T-FORCE   | SSD                | 250 GB | 2       | 28    | 0     | 0.08   |
| SK hynix  | HFS256G32MND-2900A | 256 GB | 2       | 436   | 15    | 0.08   |
| Samsung   | SSD 870 QVO        | 1 TB   | 27      | 28    | 0     | 0.08   |
| Apple     | SSD TS128E         | 121 GB | 4       | 105   | 47    | 0.08   |
| INNOVA... | SSD                | 240 GB | 1       | 28    | 0     | 0.08   |
| Kingston  | SKC600512G         | 512 GB | 8       | 27    | 0     | 0.08   |
| Netac     | SSD                | 480 GB | 2       | 27    | 0     | 0.08   |
| Kingmax   | SSD                | 64 GB  | 24      | 196   | 521   | 0.08   |
| PNY       | CS900 500GB SSD    | 500 GB | 11      | 27    | 0     | 0.08   |
| TAISU     | SSD 240G           | 240 GB | 1       | 27    | 0     | 0.08   |
| SenDisk   | C3-60G             | 64 GB  | 1       | 27    | 0     | 0.08   |
| China     | 256GB PCS 2.5" SSD | 256 GB | 1       | 27    | 0     | 0.07   |
| Kingch... | SSD                | 360 GB | 1       | 27    | 0     | 0.07   |
| Intenso   | SSD Sata III       | 960 GB | 1       | 27    | 0     | 0.07   |
| Lenovo    | Thinklife SSD S... | 480 GB | 1       | 27    | 0     | 0.07   |
| KingSpec  | CHA-M2B7-M256      | 256 GB | 2       | 27    | 0     | 0.07   |
| SanDisk   | SD8SBAT128G1122    | 128 GB | 9       | 27    | 0     | 0.07   |
| BIWIN     | M6305              | 120 GB | 1       | 26    | 0     | 0.07   |
| Micron    | 5200_MTFDDAK960TDC | 960 GB | 1       | 26    | 0     | 0.07   |
| Plextor   | PX-256M8VG         | 256 GB | 2       | 26    | 0     | 0.07   |
| HECTRON   | HECX1-240G         | 240 GB | 1       | 26    | 0     | 0.07   |
| Transcend | TS64GSSD720        | 64 GB  | 1       | 26    | 0     | 0.07   |
| Hikvision | HS-SSD-E100N 512G  | 512 GB | 1       | 26    | 0     | 0.07   |
| Plextor   | PX-256M6GV-2280    | 256 GB | 1       | 26    | 0     | 0.07   |
| Lite-On   | LMH-512V2M-11 M... | 512 GB | 1       | 26    | 0     | 0.07   |
| Team      | T253X1480G         | 480 GB | 5       | 26    | 0     | 0.07   |
| Pasoul    | OASDX-120G         | 120 GB | 1       | 25    | 0     | 0.07   |
| KingSpec  | T-120              | 120 GB | 1       | 25    | 0     | 0.07   |
| Toshiba   | THNSNH128G8NT      | 128 GB | 1       | 25    | 0     | 0.07   |
| SanDisk   | Z400s M.2 2280     | 128 GB | 3       | 25    | 0     | 0.07   |
| SanDisk   | SDSSDH3 2T00       | 2 TB   | 4       | 25    | 0     | 0.07   |
| Advantech | SQF-S25M8-256G-SAC | 256 GB | 1       | 25    | 0     | 0.07   |
| Lite-On   | LMH-256V2M-41 M... | 256 GB | 1       | 25    | 0     | 0.07   |
| Lite-On   | CV5-8Q256          | 256 GB | 1       | 24    | 0     | 0.07   |
| Mushkin   | MKNSSDCR60GB-7     | 64 GB  | 2       | 81    | 2     | 0.07   |
| Team      | TM8PS7512G         | 512 GB | 2       | 24    | 0     | 0.07   |
| Apacer    | AS510S             | 256 GB | 1       | 24    | 0     | 0.07   |
| Corsair   | CSSD-V32GB2        | 32 GB  | 1       | 99    | 3     | 0.07   |
| Dogfish   | SSD                | 500 GB | 1       | 24    | 0     | 0.07   |
| LDLC      | SSD                | 128 GB | 5       | 24    | 0     | 0.07   |
| Plextor   | PX-128S2C          | 128 GB | 2       | 24    | 0     | 0.07   |
| BIOSTAR   | S100-120GB         | 120 GB | 2       | 24    | 0     | 0.07   |
| V-GeN     | V-GEN07SM20AR12... | 128 GB | 1       | 24    | 0     | 0.07   |
| Team      | L5 LITE SSD        | 64 GB  | 3       | 27    | 1     | 0.07   |
| Patriot   | P210               | 1 TB   | 1       | 72    | 2     | 0.07   |
| Kingston  | SA400M8120G        | 120 GB | 8       | 23    | 0     | 0.07   |
| Intenso   | SSD Sata III       | 1 TB   | 2       | 23    | 0     | 0.07   |
| Samsung   | MZNLN512HCJH-000L2 | 512 GB | 1       | 23    | 0     | 0.07   |
| PNY       | SSD2SC120G1SA75... | 120 GB | 1       | 23    | 0     | 0.07   |
| SNR       | ML 240             | 240 GB | 1       | 23    | 0     | 0.07   |
| Kingch... | SSD                | 1 TB   | 1       | 23    | 0     | 0.06   |
| SK hynix  | SC401 SATA         | 256 GB | 3       | 23    | 0     | 0.06   |
| OWC       | 1.0TB Mercury E... | 1 TB   | 1       | 23    | 0     | 0.06   |
| XrayDisk  | SSD                | 128 GB | 5       | 23    | 0     | 0.06   |
| addlink   | SATA SSD           | 1 TB   | 1       | 23    | 0     | 0.06   |
| Kingch... | SSD                | 32 GB  | 1       | 23    | 0     | 0.06   |
| EMTEC     | X150               | 960 GB | 1       | 23    | 0     | 0.06   |
| Seagate   | QSCD-ST52570-128GB | 128 GB | 1       | 23    | 0     | 0.06   |
| GLOWAY    | FER240GS3-S7       | 240 GB | 1       | 23    | 0     | 0.06   |
| Samsung   | SSD 870 QVO        | 2 TB   | 13      | 22    | 0     | 0.06   |
| TCSUNBOW  | N4                 | 240 GB | 1       | 22    | 0     | 0.06   |
| Intel     | SSDSA1M080G2HP     | 80 GB  | 2       | 342   | 17    | 0.06   |
| Lite-On   | CV1-8B256          | 256 GB | 5       | 22    | 0     | 0.06   |
| Plextor   | PX-128S1G          | 128 GB | 1       | 22    | 0     | 0.06   |
| Lite-On   | L8H-256V2G         | 256 GB | 2       | 22    | 0     | 0.06   |
| Toshiba   | THNSNS060GBSP      | 64 GB  | 1       | 22    | 0     | 0.06   |
| SK hynix  | HFS256G32MND-2200A | 256 GB | 3       | 298   | 173   | 0.06   |
| Kingston  | 480GBV500          | 480 GB | 1       | 22    | 0     | 0.06   |
| Plextor   | PX-128M6V          | 128 GB | 1       | 22    | 0     | 0.06   |
| Zheino    | CHN25SATAS1 256    | 256 GB | 1       | 22    | 0     | 0.06   |
| Ramaxel   | RTITF128PCA1MADL   | 128 GB | 1       | 22    | 0     | 0.06   |
| Foxline   | FLSSD480X5SE       | 480 GB | 1       | 22    | 0     | 0.06   |
| ELSKY     | SSD 64G            | 64 GB  | 1       | 21    | 0     | 0.06   |
| Transcend | TS128GMSA370       | 128 GB | 2       | 21    | 0     | 0.06   |
| Transcend | TS32GSSD370S       | 32 GB  | 10      | 21    | 0     | 0.06   |
| Plextor   | PX-256M6M          | 256 GB | 3       | 29    | 1     | 0.06   |
| Maximus   | SSD                | 128 GB | 1       | 21    | 0     | 0.06   |
| Samsung   | MZMPA128HMFU-000H1 | 128 GB | 4       | 287   | 1374  | 0.06   |
| OCZ       | INTREPID 3600      | 400 GB | 1       | 21    | 0     | 0.06   |
| BAITITON  | BT58SSD09S         | 240 GB | 1       | 21    | 0     | 0.06   |
| China     | CIE M8 M350 128... | 128 GB | 1       | 21    | 0     | 0.06   |
| OSCOO     | OSC mSATA          | 256 GB | 1       | 21    | 0     | 0.06   |
| Yeyian    | VALK 1500          | 240 GB | 1       | 21    | 0     | 0.06   |
| China     | SSD                | 480 GB | 10      | 20    | 0     | 0.06   |
| Intel     | SSDSC2KB240G8L ... | 240 GB | 2       | 20    | 0     | 0.06   |
| Intel     | SSDSCKKF180G8L     | 180 GB | 1       | 20    | 0     | 0.06   |
| Goldkey   | GKH84-256GB        | 256 GB | 1       | 20    | 0     | 0.06   |
| Transcend | TS240GMTS820S      | 240 GB | 3       | 20    | 0     | 0.06   |
| China     | SSD                | 96 GB  | 1       | 20    | 0     | 0.06   |
| Lite-On   | CV1-8B128          | 128 GB | 6       | 20    | 0     | 0.06   |
| Intel     | SSDSC2KR120H6      | 120 GB | 1       | 20    | 0     | 0.06   |
| Lenovo    | SSD SL700 480G     | 480 GB | 1       | 20    | 0     | 0.06   |
| AMD       | R3SL240G           | 240 GB | 4       | 44    | 1     | 0.06   |
| Kingston  | SHFR200240G        | 240 GB | 1       | 20    | 0     | 0.06   |
| XUNZHE    | XUNZHE800S 120G    | 120 GB | 1       | 20    | 0     | 0.05   |
| Seagate   | XA1920LE10063      | 1.9 TB | 4       | 19    | 0     | 0.05   |
| Crucial   | CT512M550SSD4      | 512 GB | 1       | 338   | 16    | 0.05   |
| China     | SSD                | 512 GB | 9       | 32    | 2     | 0.05   |
| SanDisk   | SDSA5GK-016G-1006  | 16 GB  | 2       | 157   | 53    | 0.05   |
| BlueRay   | SDM8SI240A         | 240 GB | 1       | 19    | 0     | 0.05   |
| SanDisk   | SD8SB8U128G1122    | 128 GB | 1       | 19    | 0     | 0.05   |
| Transcend | TS128GSSD230S      | 128 GB | 11      | 19    | 0     | 0.05   |
| Kingston  | RBUSNS8180S3256GJ  | 256 GB | 2       | 19    | 0     | 0.05   |
| ADATA     | SU800NS38          | 256 GB | 9       | 34    | 248   | 0.05   |
| Drevo     | X1 SSD             | 120 GB | 4       | 214   | 17    | 0.05   |
| Micron    | MTFDDAK1T0TBN-1... | 1 TB   | 1       | 19    | 0     | 0.05   |
| Plextor   | PX-256M8VC         | 256 GB | 3       | 18    | 0     | 0.05   |
| Corsair   | CSSD-F80GB2-A      | 80 GB  | 1       | 18    | 0     | 0.05   |
| Intel     | SSDSCKJF240A5L     | 240 GB | 2       | 84    | 6     | 0.05   |
| Kingston  | SA400M8480G        | 480 GB | 1       | 18    | 0     | 0.05   |
| Samsung   | SSD 870 EVO        | 2 TB   | 3       | 18    | 0     | 0.05   |
| Lite-On   | CV1-8B256-HP       | 256 GB | 1       | 18    | 0     | 0.05   |
| Corsair   | Neutron SSD        | 240 GB | 1       | 2126  | 114   | 0.05   |
| Intel     | SSDSCKKF256H6 SATA | 256 GB | 4       | 49    | 7     | 0.05   |
| WDC       | WDS100T2B0B        | 1 TB   | 3       | 18    | 0     | 0.05   |
| DGM       | SSD 120GB S3-120A  | 120 GB | 1       | 18    | 0     | 0.05   |
| SanDisk   | SDSSDH3 500G       | 500 GB | 10      | 18    | 0     | 0.05   |
| Team      | T253X1240G         | 240 GB | 5       | 18    | 0     | 0.05   |
| ADATA     | SP610              | 256 GB | 1       | 18    | 0     | 0.05   |
| Hyperdisk | SDOM               | 16 GB  | 1       | 18    | 0     | 0.05   |
| Kingston  | RBUSC180DS37128GJ  | 128 GB | 3       | 18    | 0     | 0.05   |
| Lite-On   | CV3-SD256          | 256 GB | 1       | 18    | 0     | 0.05   |
| Lite-On   | LCH-128V2S-HP      | 128 GB | 1       | 18    | 0     | 0.05   |
| LDLC      | SSD F6 PLUS M.2... | 960 GB | 2       | 17    | 0     | 0.05   |
| SanDisk   | Extreme Portabl... | 1 TB   | 1       | 17    | 0     | 0.05   |
| SanDisk   | SSD U100           | 64 GB  | 9       | 19    | 1     | 0.05   |
| Toshiba   | THNSNJ256GMCT      | 256 GB | 1       | 17    | 0     | 0.05   |
| Lite-On   | CV8-8E256          | 256 GB | 6       | 17    | 0     | 0.05   |
| Intel     | SSDSC2KB019T8      | 1.9 TB | 3       | 17    | 0     | 0.05   |
| Lite-On   | LMH-128V2M-11 M... | 128 GB | 1       | 17    | 0     | 0.05   |
| Dell      | WR202KD032G E70... | 32 GB  | 3       | 17    | 0     | 0.05   |
| Team      | TM8PS5256G         | 256 GB | 1       | 17    | 0     | 0.05   |
| China     | 60GB SSD           | 64 GB  | 1       | 17    | 0     | 0.05   |
| China     | RTMMB256VBV4KFY    | 256 GB | 1       | 17    | 0     | 0.05   |
| Lite-On   | IT L8T-256L9G-HP   | 256 GB | 1       | 17    | 0     | 0.05   |
| PNY       | SSD2SC240G1SA75... | 240 GB | 1       | 17    | 0     | 0.05   |
| Kingrich  | 64GB K9 SATA3 SSD  | 64 GB  | 2       | 17    | 0     | 0.05   |
| China     | NGFF 2280 1TB SSD  | 1 TB   | 1       | 17    | 0     | 0.05   |
| KINGBANK  | KP330              | 480 GB | 2       | 17    | 0     | 0.05   |
| AMD       | R3S60GBSM          | 64 GB  | 2       | 17    | 0     | 0.05   |
| LDNDISK   | SSD                | 240 GB | 1       | 16    | 0     | 0.05   |
| Lite-On   | L8H-256V2G-11 M... | 256 GB | 2       | 16    | 0     | 0.05   |
| Intel     | SSDSCKKF512H6 SATA | 512 GB | 1       | 249   | 14    | 0.05   |
| XrayDisk  | SSD                | 240 GB | 2       | 16    | 0     | 0.05   |
| China     | SATA3 480GB SSD    | 480 GB | 1       | 16    | 0     | 0.05   |
| Intel     | SSDSA1M160G2HP     | 160 GB | 6       | 102   | 14    | 0.05   |
| AEGO      | SSD                | 240 GB | 3       | 16    | 0     | 0.04   |
| Intel     | SSDSCKKW256G8      | 256 GB | 2       | 16    | 0     | 0.04   |
| Intel     | SSDMCEAW080A4      | 80 GB  | 1       | 16    | 0     | 0.04   |
| XUM       | HX240GSSDSATA3     | 240 GB | 1       | 16    | 0     | 0.04   |
| Kingston  | SKC300S37A180G     | 180 GB | 3       | 320   | 745   | 0.04   |
| Intel     | SSDSC2KF256H6L     | 256 GB | 5       | 82    | 8     | 0.04   |
| FASTDISK  | FASTDISK120G       | 120 GB | 1       | 15    | 0     | 0.04   |
| SanDisk   | SD8SNAT128G1122    | 128 GB | 1       | 15    | 0     | 0.04   |
| China     | MLC 256G           | 256 GB | 1       | 15    | 0     | 0.04   |
| ADATA     | SP900NS34          | 128 GB | 2       | 230   | 508   | 0.04   |
| FORESEE   | 240GB SSD          | 240 GB | 1       | 15    | 0     | 0.04   |
| Transcend | TS64GSSD25S-M      | 64 GB  | 2       | 15    | 0     | 0.04   |
| T-FORCE   | SSD                | 1 TB   | 1       | 15    | 0     | 0.04   |
| e2e4      | SSD                | 120 GB | 3       | 15    | 0     | 0.04   |
| Lite-On   | CV1-SB128          | 128 GB | 1       | 15    | 0     | 0.04   |
| Apple     | SSD TS0128F        | 121 GB | 1       | 15    | 0     | 0.04   |
| Leven     | JAJS500M120C-1     | 120 GB | 1       | 15    | 0     | 0.04   |
| KingSpec  | P4-240             | 240 GB | 10      | 17    | 1     | 0.04   |
| Micron    | 1300_MTFDDAK256TDL | 256 GB | 2       | 14    | 0     | 0.04   |
| China     | SSD                | 64 GB  | 3       | 14    | 0     | 0.04   |
| FASTDISK  | SSD 60G            | 64 GB  | 1       | 14    | 0     | 0.04   |
| PNY       | SSD2SC240G5LC70... | 240 GB | 1       | 14    | 0     | 0.04   |
| Smartbuy  | SSD                | 128 GB | 2       | 14    | 0     | 0.04   |
| Lexar     | SSD                | 120 GB | 1       | 14    | 0     | 0.04   |
| Team      | T253TD001T         | 1 TB   | 1       | 14    | 0     | 0.04   |
| Samsung   | MZNLN128HAHQ-000L1 | 128 GB | 1       | 14    | 0     | 0.04   |
| Lenovo    | SSD SL700 M.2 128G | 128 GB | 1       | 14    | 0     | 0.04   |
| Kingston  | SKC600256G         | 256 GB | 18      | 14    | 0     | 0.04   |
| Seagate   | ST480FP0021        | 480 GB | 1       | 14    | 0     | 0.04   |
| Lite-On   | LCH-256V2S-11 2... | 256 GB | 3       | 14    | 1     | 0.04   |
| Crucial   | CT2000MX500SSD1N   | 2 TB   | 1       | 14    | 0     | 0.04   |
| SK hynix  | SH920 mSATA        | 128 GB | 2       | 108   | 17    | 0.04   |
| WDC       | WDBNCE5000PNC-WRSN | 500 GB | 1       | 14    | 0     | 0.04   |
| Micron    | MTFDDAK240TCB      | 240 GB | 1       | 14    | 0     | 0.04   |
| Kingston  | RBUSNS8180DS3256GH | 256 GB | 1       | 41    | 2     | 0.04   |
| Lite-On   | LSS-24L6G          | 24 GB  | 2       | 13    | 0     | 0.04   |
| SMI       | SSD DISK           | 128 GB | 1       | 13    | 0     | 0.04   |
| Pioneer   | APS-SL3N-120       | 120 GB | 1       | 13    | 0     | 0.04   |
| Smartbuy  | m.2 S11-2280       | 256 GB | 1       | 13    | 0     | 0.04   |
| OCZ       | VECTOR180          | 960 GB | 1       | 13    | 0     | 0.04   |
| ShanDi... | SSD                | 256 GB | 1       | 13    | 0     | 0.04   |
| Lite-On   | LGT-256M6G         | 256 GB | 1       | 13    | 0     | 0.04   |
| Lite-On   | LJH-256V2G-11 M... | 256 GB | 1       | 13    | 0     | 0.04   |
| Kingston  | HyperX Fury 3D     | 120 GB | 3       | 13    | 0     | 0.04   |
| Seagate   | FireCuda 120 SS... | 500 GB | 1       | 13    | 0     | 0.04   |
| Plextor   | PX-G256M6e         | 256 GB | 2       | 13    | 0     | 0.04   |
| Plextor   | PX-128M6S+         | 128 GB | 1       | 13    | 0     | 0.04   |
| Transcend | TS128GMTS600       | 128 GB | 1       | 13    | 0     | 0.04   |
| Dogfish   | SSD                | 240 GB | 1       | 13    | 0     | 0.04   |
| Intel     | SSDSCKKW128G8      | 128 GB | 3       | 13    | 0     | 0.04   |
| TCSUNBOW  | X3                 | 120 GB | 1       | 13    | 0     | 0.04   |
| e2e4      | SSD                | 64 GB  | 1       | 13    | 0     | 0.04   |
| Phison    | S11-256G-PHISON... | 256 GB | 1       | 12    | 0     | 0.04   |
| Teclast   | 256GB NS550-2242   | 256 GB | 7       | 12    | 0     | 0.04   |
| Samsung   | MZ7LH240HAHQ-00005 | 240 GB | 2       | 12    | 0     | 0.03   |
| Varro     | BULLDOZER-120GB    | 120 GB | 1       | 12    | 0     | 0.03   |
| Zheino    | CHN 25SATA01M 030  | 32 GB  | 1       | 12    | 0     | 0.03   |
| Super ... | FTM28N325H         | 128 GB | 1       | 12    | 0     | 0.03   |
| Lite-On   | CV3-SD128          | 128 GB | 1       | 12    | 0     | 0.03   |
| Silico... | ULTIMATE CF CARD   | 16 GB  | 1       | 12    | 0     | 0.03   |
| Wicgtyp   | M900-128           | 128 GB | 1       | 12    | 0     | 0.03   |
| Transcend | TS128GSSD360S      | 128 GB | 8       | 12    | 0     | 0.03   |
| Samsung   | MZ7PA128HMCD-010H1 | 128 GB | 1       | 12    | 0     | 0.03   |
| KIOXIA... | SATA SSD           | 240 GB | 4       | 12    | 0     | 0.03   |
| KingSpec  | P3-256             | 256 GB | 7       | 12    | 0     | 0.03   |
| Kingrich  | KM9 60GB MSATA3... | 64 GB  | 1       | 12    | 0     | 0.03   |
| SanDisk   | SD9SN8W512G1122    | 512 GB | 1       | 12    | 0     | 0.03   |
| PNY       | CS900 1TB SSD      | 1 TB   | 1       | 11    | 0     | 0.03   |
| China     | SSD                | 180 GB | 1       | 11    | 0     | 0.03   |
| Goodram   | SSDPR-CX400-256-G2 | 256 GB | 4       | 11    | 0     | 0.03   |
| SK hynix  | HFS128G39MNC-2300A | 128 GB | 1       | 223   | 18    | 0.03   |
| PNY       | SSD2SC120G1SA75... | 120 GB | 1       | 11    | 0     | 0.03   |
| KingFast  | SSD                | 512 GB | 3       | 11    | 0     | 0.03   |
| FORESEE   | 256GB SSD          | 256 GB | 5       | 11    | 0     | 0.03   |
| Transcend | TS512GMTS430S      | 512 GB | 8       | 11    | 0     | 0.03   |
| Netac     | SSD 120G           | 120 GB | 2       | 11    | 0     | 0.03   |
| Transcend | TSKU60SSD420       | 64 GB  | 1       | 11    | 0     | 0.03   |
| SanDisk   | SD8SNAT-256G-1006  | 256 GB | 7       | 11    | 0     | 0.03   |
| Crucial   | V4-CT128V4SSD2     | 128 GB | 1       | 11    | 0     | 0.03   |
| Faspeed   | M3-360G            | 360 GB | 1       | 11    | 0     | 0.03   |
| Micron    | M600_MTFDDAV512MBF | 512 GB | 1       | 11    | 0     | 0.03   |
| China     | MSATA SSD          | 256 GB | 1       | 11    | 0     | 0.03   |
| SUNEAST   | SSD SE800          | 256 GB | 1       | 11    | 0     | 0.03   |
| ADATA     | SSD S511           | 240 GB | 1       | 10    | 0     | 0.03   |
| Transcend | TS32GSSD25S-M      | 32 GB  | 1       | 10    | 0     | 0.03   |
| SanDisk   | SSD i110           | 16 GB  | 3       | 10    | 0     | 0.03   |
| Intel     | SSDSCKKW240H6      | 240 GB | 3       | 18    | 1     | 0.03   |
| China     | EK V100 120G       | 120 GB | 1       | 10    | 0     | 0.03   |
| Golden... | GDSA25-120MS       | 120 GB | 1       | 10    | 0     | 0.03   |
| SanDisk   | SD8SNAT256G1122    | 256 GB | 3       | 10    | 0     | 0.03   |
| Micron    | 1300 SATA          | 256 GB | 2       | 10    | 0     | 0.03   |
| ADATA     | SX300              | 128 GB | 1       | 10    | 0     | 0.03   |
| Hikvision | HS-SSD-C100 120G   | 120 GB | 1       | 10    | 0     | 0.03   |
| Mushkin   | MKNSSDTR240GB      | 240 GB | 1       | 10    | 0     | 0.03   |
| KingSpec  | ACSC2M256S25       | 256 GB | 1       | 10    | 0     | 0.03   |
| PNY       | CS1311 32GB SSD    | 32 GB  | 1       | 10    | 0     | 0.03   |
| BIWIN     | SSD                | 512 GB | 3       | 9     | 0     | 0.03   |
| Samsung   | SSD 870 EVO        | 1 TB   | 11      | 9     | 0     | 0.03   |
| SanDisk   | SD8SNAT256G1002    | 256 GB | 4       | 9     | 0     | 0.03   |
| Transcend | TS128GMSA230S      | 128 GB | 1       | 9     | 0     | 0.03   |
| Lite-On   | CV1-8B512-HP       | 512 GB | 2       | 9     | 0     | 0.03   |
| SK hynix  | SH920 mSATA        | 256 GB | 3       | 530   | 252   | 0.03   |
| Seagate   | IronWolf ZA500N... | 500 GB | 1       | 9     | 0     | 0.03   |
| SPCC      | SSD162             | 240 GB | 1       | 203   | 20    | 0.03   |
| Ramsta    | SSD R800           | 120 GB | 1       | 9     | 0     | 0.03   |
| Kingston  | SKC6001024G        | 1 TB   | 3       | 9     | 0     | 0.03   |
| KingSpec  | NT-1TB             | 1 TB   | 2       | 9     | 0     | 0.03   |
| Lite-On   | CV3-SD512          | 512 GB | 1       | 9     | 0     | 0.03   |
| KingSpec  | P3-64              | 64 GB  | 2       | 9     | 0     | 0.03   |
| Faspeed   | H5-120G PLUS       | 120 GB | 1       | 9     | 0     | 0.03   |
| HP        | SSD S600           | 120 GB | 1       | 9     | 0     | 0.03   |
| KingSpec  | ACSC2M064mSA       | 64 GB  | 1       | 9     | 0     | 0.03   |
| Microtech | SSD480M2S80        | 480 GB | 1       | 9     | 0     | 0.03   |
| Samsung   | SSD PM810 2.5" 7mm | 256 GB | 2       | 369   | 61    | 0.03   |
| ADATA     | SU650NS38          | 120 GB | 3       | 9     | 0     | 0.03   |
| SanDisk   | SD8TN8U-256G-1006  | 256 GB | 1       | 64    | 6     | 0.03   |
| Micron    | MTFDDAK256MAY-1... | 256 GB | 3       | 248   | 130   | 0.02   |
| ADATA     | SU900              | 128 GB | 1       | 9     | 0     | 0.02   |
| Kingston  | v300 240G          | 240 GB | 1       | 9     | 0     | 0.02   |
| SanDisk   | WD easystore       | 240 GB | 1       | 9     | 0     | 0.02   |
| SanDisk   | SSD P4             | 32 GB  | 13      | 109   | 254   | 0.02   |
| Seagate   | BarraCuda 120 S... | 250 GB | 5       | 9     | 0     | 0.02   |
| SanDisk   | SD8SMAT-128G-1006  | 128 GB | 1       | 9     | 0     | 0.02   |
| Micron    | MTFDDAK128MAY-1... | 128 GB | 2       | 151   | 16    | 0.02   |
| Teclast   | 128GB MS550        | 128 GB | 1       | 8     | 0     | 0.02   |
| SanDisk   | iSSD P4            | 16 GB  | 1       | 238   | 26    | 0.02   |
| Dogfish   | SSD                | 120 GB | 1       | 8     | 0     | 0.02   |
| KingDian  | N400 60G           | 64 GB  | 1       | 8     | 0     | 0.02   |
| SanDisk   | SD7SN6S-128G-1006  | 128 GB | 1       | 8     | 0     | 0.02   |
| Getrich   | 120G SSD           | 120 GB | 1       | 8     | 0     | 0.02   |
| FORESEE   | S50AF512GB         | 512 GB | 4       | 8     | 0     | 0.02   |
| KingSpec  | ACSC4M128MSA       | 128 GB | 1       | 8     | 0     | 0.02   |
| Mushkin   | MKNSSDRE2TB        | 2 TB   | 1       | 8     | 0     | 0.02   |
| PNY       | SSD2SC240G1CS17... | 240 GB | 1       | 8     | 0     | 0.02   |
| Londisk   | SSD                | 480 GB | 1       | 8     | 0     | 0.02   |
| China     | ESA3ASA2PSTBT120GB | 120 GB | 1       | 243   | 28    | 0.02   |
| Kingspeed | SSD                | 240 GB | 1       | 8     | 0     | 0.02   |
| Drevo     | X1                 | 120 GB | 2       | 144   | 1016  | 0.02   |
| Plextor   | PX-512M6S          | 512 GB | 1       | 8     | 0     | 0.02   |
| Netac     | SATA3 120GB SSD    | 120 GB | 1       | 8     | 0     | 0.02   |
| Mushkin   | MKNSSDRW1TB        | 1 TB   | 1       | 8     | 0     | 0.02   |
| Samsung   | MZ7LH128HBHQ-000L1 | 128 GB | 2       | 7     | 0     | 0.02   |
| PNY       | SSD2SC256GM1P3D... | 256 GB | 1       | 7     | 0     | 0.02   |
| Micron    | MTFDDAK512TBN-1... | 512 GB | 1       | 7     | 0     | 0.02   |
| FASTDISK  | SSD 120G           | 120 GB | 1       | 7     | 0     | 0.02   |
| Intel     | SSDSC2BF180A5H SED | 180 GB | 3       | 290   | 47    | 0.02   |
| ADATA     | SU750              | 512 GB | 1       | 7     | 0     | 0.02   |
| China     | SSD60G             | 64 GB  | 2       | 7     | 0     | 0.02   |
| SanDisk   | SD8SBAT256G1002    | 256 GB | 1       | 7     | 0     | 0.02   |
| Zheino    | CHN 25SATA01M 060  | 64 GB  | 1       | 7     | 0     | 0.02   |
| China     | SSD128GBS800       | 128 GB | 1       | 7     | 0     | 0.02   |
| KingSpec  | ACSC2M128mSA       | 128 GB | 1       | 7     | 0     | 0.02   |
| Toshiba   | THNSNS128GMCP      | 128 GB | 1       | 7     | 0     | 0.02   |
| SanDisk   | SD9SN8W128G1122    | 128 GB | 1       | 7     | 0     | 0.02   |
| FASTDISK  | SSD 30G            | 32 GB  | 1       | 7     | 0     | 0.02   |
| Samsung   | SSD 870 EVO        | 500 GB | 13      | 7     | 0     | 0.02   |
| Dell      | WR202KD032G E70... | 32 GB  | 2       | 6     | 0     | 0.02   |
| tigo      | SSD                | 128 GB | 1       | 6     | 0     | 0.02   |
| WDC       | WDS250G2B0B        | 250 GB | 4       | 6     | 0     | 0.02   |
| Kingston  | SV300S37A 120G     | 120 GB | 1       | 6     | 0     | 0.02   |
| Intenso   | lntenso SSD Sat... | 960 GB | 1       | 171   | 24    | 0.02   |
| Phison    | SSBP064GTB3C0-S11  | 64 GB  | 1       | 6     | 0     | 0.02   |
| Mushkin   | MKNSSDE3480GB      | 480 GB | 1       | 6     | 0     | 0.02   |
| Intel     | SSDSCKJW180H6      | 180 GB | 1       | 6     | 0     | 0.02   |
| Patriot   | Ignite             | 240 GB | 1       | 6     | 0     | 0.02   |
| Kingston  | RBUSC180S37128GJ   | 128 GB | 1       | 6     | 0     | 0.02   |
| Kingston  | SA400S37 240G      | 240 GB | 1       | 6     | 0     | 0.02   |
| ADATA     | SU650NS38          | 240 GB | 3       | 6     | 0     | 0.02   |
| Samsung   | SSD PM871b 2.5 7mm | 128 GB | 1       | 6     | 0     | 0.02   |
| BHT       | WR202I0064G E70... | 64 GB  | 4       | 6     | 0     | 0.02   |
| SanDisk   | SD8SNAT128G1002    | 128 GB | 4       | 6     | 0     | 0.02   |
| Apacer    | 16GB SATA Flash... | 16 GB  | 4       | 225   | 24    | 0.02   |
| Kingston  | SM2280S3G2480G     | 480 GB | 2       | 149   | 63    | 0.02   |
| Lite-On   | CV5-8Q512-HP       | 512 GB | 1       | 6     | 0     | 0.02   |
| ADATA     | SU720              | 1 TB   | 1       | 6     | 0     | 0.02   |
| Goodram   | SSDPR_CX300_120    | 120 GB | 1       | 6     | 0     | 0.02   |
| China     | SSD 128G           | 128 GB | 2       | 6     | 0     | 0.02   |
| KingSpec  | KSQ120             | 120 GB | 1       | 6     | 0     | 0.02   |
| QNIX      | SSD                | 120 GB | 1       | 6     | 0     | 0.02   |
| GeIL      | Zenith A3-PRO      | 240 GB | 1       | 6     | 0     | 0.02   |
| GeIL      | Zenith A3          | 120 GB | 1       | 6     | 0     | 0.02   |
| SPCC      | 2.5" SSD           | 512 GB | 1       | 6     | 0     | 0.02   |
| Intel     | SSDSCKGW180A4      | 180 GB | 1       | 286   | 47    | 0.02   |
| China     | SATA SSD           | 960 GB | 1       | 5     | 0     | 0.02   |
| INDMEM    | SSD mSATA          | 128 GB | 1       | 5     | 0     | 0.02   |
| BRAVEE... | SSD                | 120 GB | 1       | 5     | 0     | 0.02   |
| V-GeN     | V-GEN10SM19AR12... | 120 GB | 1       | 5     | 0     | 0.02   |
| Dell      | WR202KD128G E70... | 128 GB | 1       | 5     | 0     | 0.02   |
| Intenso   | SSD                | 480 GB | 2       | 5     | 0     | 0.02   |
| KingSpec  | T-60               | 64 GB  | 4       | 12    | 88    | 0.02   |
| KingSpec  | NT-512             | 512 GB | 4       | 34    | 4     | 0.01   |
| Lite-On   | L8T-256L9G-11 M... | 256 GB | 1       | 5     | 0     | 0.01   |
| ADATA     | SX850              | 256 GB | 2       | 171   | 40    | 0.01   |
| Iod       | MST1001-512        | 512 GB | 1       | 5     | 0     | 0.01   |
| SanDisk   | SSD PLUS           | 2 TB   | 1       | 5     | 0     | 0.01   |
| EMTEC     | X150               | 120 GB | 1       | 5     | 0     | 0.01   |
| China     | M.2 2280-1TB SSD   | 1 TB   | 1       | 5     | 0     | 0.01   |
| MaxDig... | MD500 120G         | 120 GB | 1       | 5     | 0     | 0.01   |
| Teclast   | 512GB A850         | 512 GB | 1       | 5     | 0     | 0.01   |
| Mushkin   | MKNSSDCG480GB      | 480 GB | 2       | 116   | 508   | 0.01   |
| Intel     | SSDSA1M080G2LE     | 80 GB  | 2       | 84    | 19    | 0.01   |
| Leven     | JS500120C          | 120 GB | 1       | 4     | 0     | 0.01   |
| Smartbuy  | m.2 S11-2280       | 128 GB | 1       | 4     | 0     | 0.01   |
| TAMMUZ    | SSD                | 120 GB | 1       | 4     | 0     | 0.01   |
| KingSpec  | ACSC2M128S25       | 128 GB | 1       | 4     | 0     | 0.01   |
| Maxtor    | Z1 SSD             | 480 GB | 3       | 4     | 0     | 0.01   |
| Seagate   | BarraCuda 120 S... | 2 TB   | 1       | 4     | 0     | 0.01   |
| Micron    | MTFDDAV256TBN-1... | 256 GB | 4       | 6     | 1     | 0.01   |
| PNY       | SSD2SC480G1CS17... | 480 GB | 1       | 4     | 0     | 0.01   |
| Samsung   | MZ7LN256HAJQ-00007 | 256 GB | 1       | 4     | 0     | 0.01   |
| Intel     | SSDSCKKF180H6L     | 180 GB | 1       | 79    | 17    | 0.01   |
| SanDisk   | SD9SB8W256G1102    | 256 GB | 2       | 4     | 0     | 0.01   |
| Team      | TM4PS5128G         | 128 GB | 1       | 8     | 1     | 0.01   |
| Intel     | SSDSC2BW480H6      | 480 GB | 1       | 182   | 41    | 0.01   |
| Maximus   | SSD 256G           | 256 GB | 1       | 4     | 0     | 0.01   |
| PNY       | SSD2SC240G1SA75... | 240 GB | 2       | 7     | 44    | 0.01   |
| Kingston  | SA400S37           | 240 GB | 1       | 4     | 0     | 0.01   |
| 2-Power   | SSD2041A           | 120 GB | 1       | 4     | 0     | 0.01   |
| Samsung   | SSD PM800 mSATA    | 64 GB  | 1       | 4     | 0     | 0.01   |
| Mushkin   | MKNSSDTR240GB-LT   | 240 GB | 1       | 4     | 0     | 0.01   |
| PHINOCOM  | SSD                | 120 GB | 1       | 4     | 0     | 0.01   |
| Hikvision | HS-SSD-C100 480G   | 480 GB | 1       | 4     | 0     | 0.01   |
| INNOVA... | SSD                | 1 TB   | 2       | 4     | 0     | 0.01   |
| KODAK     | SSD X100           | 120 GB | 1       | 4     | 0     | 0.01   |
| XrayDisk  | SSD                | 256 GB | 2       | 4     | 0     | 0.01   |
| Intel     | SSDMAEMC080G2H     | 80 GB  | 1       | 4     | 0     | 0.01   |
| Corsair   | Neutron GTX SSD    | 128 GB | 1       | 1173  | 291   | 0.01   |
| BIWIN     | G2242              | 64 GB  | 2       | 4     | 0     | 0.01   |
| GeIL      | ZENITH-A3 120G     | 120 GB | 1       | 3     | 0     | 0.01   |
| Zheino    | CHN-25SATAA3-360   | 360 GB | 1       | 87    | 21    | 0.01   |
| Intel     | SSDSC2KF010T8      | 1 TB   | 1       | 3     | 0     | 0.01   |
| Leven     | JAJS300M240C       | 240 GB | 1       | 3     | 0     | 0.01   |
| Fujitsu   | F500S              | 1 TB   | 1       | 3     | 0     | 0.01   |
| SanDisk   | SATAIII            | 16 GB  | 1       | 3     | 0     | 0.01   |
| tigo      | SSD                | 64 GB  | 1       | 3     | 0     | 0.01   |
| Samsung   | SSD 870 EVO        | 250 GB | 7       | 3     | 0     | 0.01   |
| KingDian  | S200               | 240 GB | 1       | 3     | 0     | 0.01   |
| ADATA     | IM2S3334-256GD     | 256 GB | 1       | 7     | 1     | 0.01   |
| Intel     | SSDMAEXC024G3H     | 24 GB  | 1       | 112   | 30    | 0.01   |
| HPE       | MK000960GWJPP      | 960 GB | 1       | 3     | 0     | 0.01   |
| Pacifi... | PSM-128GBSATA3S... | 128 GB | 1       | 3     | 0     | 0.01   |
| OWC       | Aura SSD           | 120 GB | 1       | 3     | 0     | 0.01   |
| ShanDi... | SSD                | 128 GB | 1       | 3     | 0     | 0.01   |
| SanDisk   | SD8SNAT-128G-1006  | 128 GB | 4       | 3     | 0     | 0.01   |
| Lite-On   | IT L8H-64V2G       | 64 GB  | 1       | 3     | 0     | 0.01   |
| Colorful  | SL300              | 120 GB | 1       | 129   | 37    | 0.01   |
| Corsair   | Neutron XT SSD     | 240 GB | 1       | 823   | 244   | 0.01   |
| SanDisk   | SD7UB3Q256G1001    | 256 GB | 4       | 339   | 100   | 0.01   |
| Samsung   | MZNLN256HAJQ-00007 | 256 GB | 1       | 3     | 0     | 0.01   |
| OCZ       | REVODRIVE X2       | 64 GB  | 4       | 1204  | 516   | 0.01   |
| SPCC      | SSDB27             | 32 GB  | 1       | 23    | 6     | 0.01   |
| ShineDisk | M667 128G          | 120 GB | 1       | 3     | 0     | 0.01   |
| Timetec   | 35TTM8SSATA-512G   | 512 GB | 1       | 3     | 0     | 0.01   |
| i-Flas... | K8                 | 64 GB  | 1       | 3     | 0     | 0.01   |
| China     | SSD-512G           | 512 GB | 1       | 3     | 0     | 0.01   |
| China     | DEPOSM3DT-480      | 480 GB | 1       | 3     | 0     | 0.01   |
| Smartbuy  | SSD                | 240 GB | 2       | 3     | 0     | 0.01   |
| Intel     | SSDSC2KW480H6      | 480 GB | 1       | 6     | 1     | 0.01   |
| Netac     | M.2 2280-128GB SSD | 128 GB | 1       | 3     | 0     | 0.01   |
| Seagate   | SSD                | 250 GB | 1       | 3     | 0     | 0.01   |
| KingSpec  | MT-256             | 256 GB | 5       | 61    | 19    | 0.01   |
| Smart     | SSD                | 240 GB | 1       | 3     | 0     | 0.01   |
| Star D... | SATA SSD           | 240 GB | 1       | 3     | 0     | 0.01   |
| Pichau    | Gaming PG256X      | 256 GB | 1       | 3     | 0     | 0.01   |
| ShanDi... | SSD                | 512 GB | 3       | 3     | 0     | 0.01   |
| Lite-On   | LMS-32L6M-HP       | 32 GB  | 2       | 3     | 0     | 0.01   |
| Foxline   | FLSSD512X5         | 512 GB | 2       | 2     | 0     | 0.01   |
| Micron    | 1100_MTFDDAK1T0TBN | 1 TB   | 4       | 66    | 14    | 0.01   |
| Samsung   | SSD PM810 mSATA    | 128 GB | 1       | 137   | 46    | 0.01   |
| Goodram   | IR_SSDPR_S25A_120  | 120 GB | 1       | 2     | 0     | 0.01   |
| SanDisk   | SD8SBAT064G1122    | 64 GB  | 1       | 2     | 0     | 0.01   |
| SanDisk   | SSD i110           | 128 GB | 1       | 2     | 0     | 0.01   |
| Fordisk   | SATA SSD           | 120 GB | 1       | 2     | 0     | 0.01   |
| Kingch... | SSD                | 64 GB  | 1       | 2     | 0     | 0.01   |
| Patriot   | Wildfire           | 120 GB | 1       | 2712  | 1022  | 0.01   |
| Intel     | SSDSC2KB480G7      | 480 GB | 3       | 2     | 0     | 0.01   |
| Foxline   | FLSSD256X5         | 256 GB | 1       | 2     | 0     | 0.01   |
| Golden... | 60Gb               | 64 GB  | 1       | 2     | 0     | 0.01   |
| Gigastone | SS6200-256GB       | 256 GB | 1       | 2     | 0     | 0.01   |
| SanDisk   | SD7SB2Q512G1001    | 512 GB | 2       | 246   | 100   | 0.01   |
| SanDisk   | SD7SB3Q128G1001    | 128 GB | 2       | 240   | 100   | 0.01   |
| KingDian  | N400               | 120 GB | 1       | 2     | 0     | 0.01   |
| SOLIDATA  | SSD                | 120 GB | 1       | 2420  | 1019  | 0.01   |
| Micron    | 1300_MTFDDAK512TDL | 512 GB | 1       | 2     | 0     | 0.01   |
| SanDisk   | SD8SNAT-128G-1009  | 128 GB | 1       | 2     | 0     | 0.01   |
| China     | 256GB QLC SATA SSD | 256 GB | 1       | 2     | 0     | 0.01   |
| Innodisk  | 2.5" SATA SSD 3... | 496 GB | 1       | 2     | 0     | 0.01   |
| SanDisk   | SSD i110           | 24 GB  | 1       | 2     | 0     | 0.01   |
| Transcend | TS64GMTS800        | 64 GB  | 1       | 2     | 0     | 0.01   |
| Intel     | SSDSCKKF240H6L     | 240 GB | 1       | 47    | 20    | 0.01   |
| OCZ       | VERTEX3 LP         | 240 GB | 1       | 2268  | 1019  | 0.01   |
| Netac     | SSD                | 128 GB | 3       | 2     | 0     | 0.01   |
| ACPI      | M2SCF-6M           | 64 GB  | 1       | 2     | 0     | 0.01   |
| Netac     | SSD                | 160 GB | 1       | 2     | 0     | 0.01   |
| VSEVEN    | V7 SSD             | 512 GB | 1       | 2     | 0     | 0.01   |
| Zheino    | CHN25SATAS1 032    | 32 GB  | 2       | 2     | 0     | 0.01   |
| SK hynix  | SH920 2.5 7MM      | 128 GB | 1       | 54    | 25    | 0.01   |
| Mushkin   | MKNSSDCL120GB      | 120 GB | 1       | 2066  | 1007  | 0.01   |
| SPCC      | M.2 SSD            | 128 GB | 1       | 2     | 0     | 0.01   |
| Lite-On   | CV1-8B512          | 512 GB | 2       | 2     | 0     | 0.01   |
| SanDisk   | SDSSDH120GG25      | 120 GB | 1       | 112   | 55    | 0.01   |
| Intel     | SSDSC2BB300G4R     | 304 GB | 2       | 2029  | 1029  | 0.01   |
| Kingston  | SKC300S37A240G     | 240 GB | 2       | 1     | 0     | 0.01   |
| SK hynix  | SH920 2.5 7MM      | 512 GB | 6       | 330   | 281   | 0.01   |
| Fujitsu   | F500S 128G         | 128 GB | 1       | 1     | 0     | 0.01   |
| Hikvision | HS-SSD-C160 256G   | 256 GB | 1       | 1     | 0     | 0.01   |
| KingSpec  | P3D-240            | 240 GB | 1       | 1     | 0     | 0.01   |
| ASENNO    | AS25               | 120 GB | 2       | 1     | 0     | 0.00   |
| FASTDISK  | SSD                | 64 GB  | 1       | 1     | 0     | 0.00   |
| Kingston  | SA400S37-120G      | 128 GB | 1       | 1     | 0     | 0.00   |
| Team      | T253E2001T         | 1 TB   | 1       | 1     | 0     | 0.00   |
| Yunhai... | Y6-240G            | 240 GB | 1       | 1     | 0     | 0.00   |
| China     | S41CF256G          | 256 GB | 1       | 1     | 0     | 0.00   |
| INDMEM    | M.2 2280           | 128 GB | 1       | 1     | 0     | 0.00   |
| Drevo     | X1 pro             | 1 TB   | 1       | 33    | 18    | 0.00   |
| OCZ       | VERTEX2            | 100 GB | 1       | 1     | 0     | 0.00   |
| Intel     | SSDSCKKW010X6      | 1 TB   | 1       | 1     | 0     | 0.00   |
| KingSpec  | ACJC2M064S25       | 64 GB  | 1       | 1     | 0     | 0.00   |
| Lite-On   | L8T-64L6G          | 64 GB  | 1       | 1     | 0     | 0.00   |
| Micron    | C400-MTFDDAT064MAM | 64 GB  | 1       | 1     | 0     | 0.00   |
| Micron    | MTFDDAT256MAM-1K2  | 256 GB | 1       | 1666  | 1010  | 0.00   |
| Mcpoint   | MC240              | 240 GB | 1       | 6     | 3     | 0.00   |
| Micron    | 5300_MTFDDAK240TDS | 240 GB | 2       | 1     | 0     | 0.00   |
| TCSUNBOW  | X1                 | 16 GB  | 1       | 1     | 0     | 0.00   |
| addlink   | SATA SSD           | 256 GB | 1       | 1     | 0     | 0.00   |
| Intel     | SSDSC2BA400G3T     | 400 GB | 1       | 1671  | 1029  | 0.00   |
| SK hynix  | HFS128G38MNB-2200A | 128 GB | 3       | 228   | 133   | 0.00   |
| Intel     | SSDSC2BX400G4R     | 400 GB | 2       | 1654  | 1028  | 0.00   |
| Intel     | SSDSC2KW240H6      | 240 GB | 6       | 8     | 174   | 0.00   |
| Team      | L5 LITE SSD        | 240 GB | 1       | 472   | 296   | 0.00   |
| China     | SSD 256G           | 256 GB | 1       | 1     | 0     | 0.00   |
| SanDisk   | SD8SB8U128G1001    | 128 GB | 1       | 1     | 0     | 0.00   |
| Toshiba   | THNSNK256GCS8 SATA | 256 GB | 2       | 159   | 100   | 0.00   |
| acpi      | MSS4FV-MP mSATA... | 128 GB | 1       | 1     | 0     | 0.00   |
| Dogfish   | SSD                | 64 GB  | 2       | 1     | 0     | 0.00   |
| Goodram   | SSDPR-CL100-120    | 120 GB | 1       | 1     | 0     | 0.00   |
| Foxline   | FLSSD128X5         | 128 GB | 3       | 1     | 0     | 0.00   |
| ADATA     | SSD DP900 512GB... | 512 GB | 2       | 1465  | 1016  | 0.00   |
| Toshiba   | THNSNK256GVN8 M... | 256 GB | 4       | 145   | 100   | 0.00   |
| Teclast   | 128GB A850         | 128 GB | 1       | 1     | 0     | 0.00   |
| BHT       | WR202I0032G E70... | 32 GB  | 1       | 1     | 0     | 0.00   |
| Plextor   | PX-512M6M          | 512 GB | 1       | 1     | 0     | 0.00   |
| S3+       | S3SSDC480XEU       | 480 GB | 1       | 1     | 0     | 0.00   |
| Patriot   | Pyro m3            | 240 GB | 1       | 1378  | 1015  | 0.00   |
| ADATA     | AXM14S3-128GM-B    | 128 GB | 1       | 1363  | 1018  | 0.00   |
| ADATA     | IMSS316-256GD      | 256 GB | 1       | 1     | 0     | 0.00   |
| BR        | SSD 60G            | 64 GB  | 1       | 1     | 0     | 0.00   |
| Transcend | TS32GMSA370        | 32 GB  | 2       | 1     | 0     | 0.00   |
| Kingston  | SHPM2280P2H-240G   | 240 GB | 6       | 512   | 639   | 0.00   |
| Lite-On   | LMT-19nmBGA-128... | 128 GB | 1       | 1     | 0     | 0.00   |
| OEM       | Genuine            | 1 TB   | 1       | 1     | 0     | 0.00   |
| Patriot   | Solid              | 240 GB | 2       | 1     | 0     | 0.00   |
| Team      | TM8PS7001T         | 1 TB   | 1       | 1     | 0     | 0.00   |
| Micron    | P300-MTFDBAC050SAL | 50 GB  | 1       | 1411  | 1140  | 0.00   |
| Toshiba   | THNSNK128GVN8 M... | 128 GB | 2       | 124   | 100   | 0.00   |
| Team      | M8PS5 SSD          | 128 GB | 1       | 1     | 0     | 0.00   |
| KingSpec  | ACJC2M128S25       | 128 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | MZNLN128HAHQ-000L2 | 128 GB | 2       | 1     | 0     | 0.00   |
| Intel     | N18A               | 240 GB | 2       | 1     | 0     | 0.00   |
| Kingston  | SKC600MS512G       | 512 GB | 1       | 1     | 0     | 0.00   |
| Netac     | SSD0128S00         | 128 GB | 1       | 1     | 0     | 0.00   |
| Dogfish   | SSD                | 512 GB | 2       | 1     | 0     | 0.00   |
| Intel     | SSDSC2BA200G4R     | 200 GB | 2       | 1037  | 1028  | 0.00   |
| Goodram   | SSDPR-CX400-512-G2 | 512 GB | 2       | 1     | 0     | 0.00   |
| Lite-On   | CV1-CC256          | 256 GB | 1       | 1     | 0     | 0.00   |
| Teclast   | 240GB A800         | 240 GB | 1       | 1     | 0     | 0.00   |
| Foxline   | FLSSD60X3          | 64 GB  | 1       | 993   | 1016  | 0.00   |
| SanDisk   | SSD P4             | 64 GB  | 1       | 14    | 14    | 0.00   |
| Toshiba   | KSG60ZSE512G SATA  | 512 GB | 2       | 97    | 100   | 0.00   |
| SPCC      | SSD                | 32 GB  | 1       | 998   | 1036  | 0.00   |
| Crucial   | CT480M500SSD3      | 480 GB | 2       | 1290  | 1480  | 0.00   |
| ADATA     | SP900NS38          | 256 GB | 1       | 942   | 1023  | 0.00   |
| Kingch... | SSD                | 480 GB | 1       | 0     | 0     | 0.00   |
| Plextor   | PH6-CE240          | 240 GB | 2       | 0     | 0     | 0.00   |
| ADATA     | SU630 1.9TB        | 1.9 TB | 1       | 0     | 0     | 0.00   |
| China     | ESA3SMN2ISN1BQ4... | 480 GB | 1       | 0     | 0     | 0.00   |
| ORTIAL    | SSD                | 256 GB | 3       | 0     | 0     | 0.00   |
| ADATA     | SX900              | 112 GB | 1       | 872   | 1016  | 0.00   |
| Corsair   | CSSD-F40GB2        | 40 GB  | 2       | 500   | 588   | 0.00   |
| FORESEE   | 32GB SSD           | 32 GB  | 1       | 0     | 0     | 0.00   |
| Kross ... | KE-SSDIS12G        | 120 GB | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSC2KW180H6      | 180 GB | 3       | 5     | 74    | 0.00   |
| SK hynix  | HFS060G32MNM-1010U | 64 GB  | 1       | 822   | 1016  | 0.00   |
| Eluktro   | TRO-SSD7-500GB-PRO | 500 GB | 1       | 806   | 1016  | 0.00   |
| Patriot   | JAJM600M128C       | 128 GB | 1       | 0     | 0     | 0.00   |
| Plextor   | PX-128M6MV         | 128 GB | 1       | 0     | 0     | 0.00   |
| SandForce | FM-25S2S-60GBP2    | 64 GB  | 1       | 317   | 416   | 0.00   |
| BAITITON  | BT58SSD11S         | 480 GB | 1       | 0     | 0     | 0.00   |
| China     | REVOLUTIONS500_256 | 256 GB | 1       | 0     | 0     | 0.00   |
| KingSpec  | MT-64              | 64 GB  | 1       | 0     | 0     | 0.00   |
| SK hynix  | SC210 2.5 7MM      | 256 GB | 2       | 556   | 856   | 0.00   |
| HP Phison | PSSBN016GA27MC0    | 16 GB  | 1       | 717   | 1033  | 0.00   |
| Kingston  | RBU-SNS8350DES3... | 128 GB | 3       | 65    | 95    | 0.00   |
| Lite-On   | E200-160           | 160 GB | 1       | 12    | 18    | 0.00   |
| Micron    | 5300_MTFDDAK480TDS | 480 GB | 2       | 0     | 0     | 0.00   |
| Intel     | SSDSCMMW120A3L     | 120 GB | 1       | 649   | 1017  | 0.00   |
| Advantech | SQF-S25M4-32G-S9C  | 32 GB  | 1       | 0     | 0     | 0.00   |
| Lexar     | SSD                | 256 GB | 1       | 0     | 0     | 0.00   |
| QUMO      | SSD                | 480 GB | 1       | 625   | 1015  | 0.00   |
| Indilinx  | InM2246S3-128G     | 128 GB | 2       | 0     | 0     | 0.00   |
| Samsung   | SSD PM810 TM       | 128 GB | 2       | 688   | 1107  | 0.00   |
| Intel     | SSDSC2KW256G8L     | 256 GB | 1       | 0     | 0     | 0.00   |
| UMAX      | 2242               | 512 GB | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSC2BX200G4R     | 200 GB | 1       | 574   | 1027  | 0.00   |
| Intenso   | SSD Sata III       | 247 GB | 1       | 18    | 32    | 0.00   |
| China     | SATA3 120GB SSD    | 120 GB | 2       | 0     | 0     | 0.00   |
| Lite-On   | LAT-256M3S         | 256 GB | 1       | 1074  | 2017  | 0.00   |
| Intel     | SSDMCEAW080A4 m... | 80 GB  | 2       | 515   | 1008  | 0.00   |
| DOGFISH   | SSD                | 512 GB | 1       | 0     | 0     | 0.00   |
| BIOSTAR   | S120-256GB         | 256 GB | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSCKKF180H6H     | 180 GB | 1       | 1     | 2     | 0.00   |
| Liren     | LIREN128G          | 128 GB | 1       | 0     | 0     | 0.00   |
| ADATA     | XM12               | 32 GB  | 1       | 465   | 1015  | 0.00   |
| Apple     | SSD SM256C         | 256 GB | 3       | 335   | 788   | 0.00   |
| ADATA     | XM11 128GB-V2      | 128 GB | 1       | 449   | 1048  | 0.00   |
| Gost      | SSD120             | 120 GB | 1       | 0     | 0     | 0.00   |
| Lite-On   | LMT-19nmBGA-64G-DS | 64 GB  | 1       | 0     | 0     | 0.00   |
| SMI       | B17A               | 240 GB | 1       | 0     | 0     | 0.00   |
| Yeyian    | VALK 1000          | 120 GB | 1       | 0     | 0     | 0.00   |
| Zheino    | CHN 25SATAA3 120   | 120 GB | 2       | 0     | 0     | 0.00   |
| Indilinx  | IND-S325S120G      | 120 GB | 1       | 3     | 8     | 0.00   |
| PNY       | SSD2SC120G3LC70... | 120 GB | 1       | 393   | 1015  | 0.00   |
| China     | T60                | 64 GB  | 2       | 0     | 0     | 0.00   |
| Patriot   | P210               | 512 GB | 2       | 0     | 0     | 0.00   |
| Reeinno   | ST960GB S7S3       | 960 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | SH103S3240G-NV     | 240 GB | 1       | 377   | 1018  | 0.00   |
| PNY       | SSD2SC120GE2DA0... | 120 GB | 1       | 373   | 1018  | 0.00   |
| SPCC      | SSD170             | 64 GB  | 1       | 358   | 1016  | 0.00   |
| SK hynix  | HFS128G3AMNB-2200A | 128 GB | 2       | 350   | 1009  | 0.00   |
| Mushkin   | MKNSSDCL120GB-DX   | 120 GB | 1       | 348   | 1006  | 0.00   |
| Lite-On   | CS1-SP32-11 M.2... | 32 GB  | 1       | 1     | 4     | 0.00   |
| Mushkin   | MKNSSDCL480GB-DX   | 480 GB | 1       | 347   | 1020  | 0.00   |
| Samsung   | Portable SSD T5    | 250 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TS8GHSD630         | 8 GB   | 1       | 679   | 2050  | 0.00   |
| Intel     | SSDSCKKF256G8H     | 256 GB | 5       | 31    | 98    | 0.00   |
| Kingston  | SVP200S37A256G     | 256 GB | 1       | 311   | 1017  | 0.00   |
| China     | ESA3ASA2ISN1BQ4... | 480 GB | 1       | 0     | 0     | 0.00   |
| FASTDISK  | SSD 32G            | 32 GB  | 1       | 0     | 0     | 0.00   |
| GLOWAY    | STK120GS3-S7       | 120 GB | 1       | 0     | 0     | 0.00   |
| KingSpec  | P4-120             | 120 GB | 1       | 0     | 0     | 0.00   |
| Patriot   | Torch LE           | 120 GB | 1       | 0     | 0     | 0.00   |
| Goodram   | SSDPR-CL100-120-G3 | 120 GB | 2       | 0     | 0     | 0.00   |
| SK hynix  | HFS256G3AMNB-2200A | 256 GB | 3       | 293   | 1038  | 0.00   |
| SanDisk   | SD8SBAT-032G-1006  | 32 GB  | 4       | 0     | 0     | 0.00   |
| KingSpec  | Q-90               | 90 GB  | 1       | 134   | 520   | 0.00   |
| Lite-On   | LMT-256M6M-HP      | 256 GB | 1       | 39    | 152   | 0.00   |
| AXIOMTEK  | FSA016G300MC4T-H   | 16 GB  | 1       | 0     | 0     | 0.00   |
| DERLAR    | SSD                | 128 GB | 1       | 0     | 0     | 0.00   |
| GLOWAY    | VAL64GM3-mSATA     | 64 GB  | 1       | 0     | 0     | 0.00   |
| TEUTONS   | SSD                | 256 GB | 1       | 0     | 0     | 0.00   |
| Bamba     | SSD                | 240 GB | 1       | 60    | 249   | 0.00   |
| GeIL      | ZENITH S3-120GB    | 120 GB | 1       | 245   | 1021  | 0.00   |
| Myung     | G3 Series          | 120 GB | 1       | 228   | 1015  | 0.00   |
| Goldenfir | T650-120G          | 128 GB | 1       | 0     | 0     | 0.00   |
| Lite-On   | S960 256           | 256 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZNLH256HAJD-000L7 | 256 GB | 1       | 0     | 0     | 0.00   |
| Zheino    | CHN25SATAS1 064    | 64 GB  | 1       | 0     | 0     | 0.00   |
| SanDisk   | SDSSDX480GG25      | 480 GB | 2       | 163   | 908   | 0.00   |
| SK hynix  | HFS256G38MNB-2200A | 256 GB | 1       | 207   | 1007  | 0.00   |
| PNY       | 69D03094-T         | 40 GB  | 1       | 195   | 1016  | 0.00   |
| China     | ESA3SMD2HTGT240GB  | 240 GB | 1       | 51    | 273   | 0.00   |
| Patriot   | Pyro SE            | 240 GB | 1       | 180   | 1016  | 0.00   |
| Apacer    | 8GB SATA Flash ... | 8 GB   | 2       | 18    | 104   | 0.00   |
| China     | NGFF 2280 256GB... | 256 GB | 1       | 0     | 0     | 0.00   |
| China     | S3 SSD             | 256 GB | 1       | 0     | 0     | 0.00   |
| China     | T120               | 120 GB | 1       | 0     | 0     | 0.00   |
| Faspeed   | H5-30G             | 32 GB  | 1       | 0     | 0     | 0.00   |
| Fujitsu   | F500s 240G         | 240 GB | 1       | 0     | 0     | 0.00   |
| Kingmax   | SSD                | 480 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | CF Card            | 16 GB  | 1       | 0     | 0     | 0.00   |
| Transcend | TS64GMSA230S       | 64 GB  | 1       | 0     | 0     | 0.00   |
| Kingston  | SNS4151S332G       | 32 GB  | 1       | 170   | 1022  | 0.00   |
| Toshiba   | THNSNK128GCS8 SATA | 128 GB | 1       | 16    | 100   | 0.00   |
| Kingston  | SNS4151S316G       | 16 GB  | 2       | 156   | 1028  | 0.00   |
| China     | 240G SATA III SSD  | 240 GB | 1       | 154   | 1016  | 0.00   |
| Goldenfir | T650-120GB         | 120 GB | 1       | 4     | 28    | 0.00   |
| SK hynix  | SH910 mSATA        | 128 GB | 1       | 151   | 1026  | 0.00   |
| Intenso   | TOP M.2 SATA       | 256 GB | 1       | 125   | 961   | 0.00   |
| Lite-On   | LCT-128M3S         | 128 GB | 1       | 132   | 1047  | 0.00   |
| Foxline   | FLSSD256X5SE       | 256 GB | 1       | 0     | 0     | 0.00   |
| Netac     | GM256              | 256 GB | 1       | 0     | 0     | 0.00   |
| Vaseky    | V900-1TB           | 1 TB   | 1       | 0     | 0     | 0.00   |
| SanDisk   | SD9SN8W-256G-1006  | 256 GB | 5       | 107   | 987   | 0.00   |
| Lite-On   | LSS-16L6G-HP       | 16 GB  | 1       | 125   | 1275  | 0.00   |
| Kingston  | SMS151S324G        | 24 GB  | 1       | 95    | 1022  | 0.00   |
| AXIOMTEK  | FSA128GMC5T        | 128 GB | 1       | 0     | 0     | 0.00   |
| China     | SATA SSD           | 24 GB  | 1       | 0     | 0     | 0.00   |
| China     | SH00R120GB         | 120 GB | 1       | 0     | 0     | 0.00   |
| Colorful  | SL500              | 240 GB | 1       | 0     | 0     | 0.00   |
| DOGFISH   | SSD                | 128 GB | 1       | 0     | 0     | 0.00   |
| Dahua     | C800A SSD          | 120 GB | 1       | 0     | 0     | 0.00   |
| HP        | SSD S600           | 240 GB | 1       | 0     | 0     | 0.00   |
| HP        | SSD S750           | 512 GB | 1       | 0     | 0     | 0.00   |
| Palit     | UVSE               | 240 GB | 1       | 0     | 0     | 0.00   |
| Plextor   | PX-32G5L           | 32 GB  | 1       | 0     | 0     | 0.00   |
| Smartbuy  | 120GB STELS        | 128 GB | 1       | 0     | 0     | 0.00   |
| Team      | T253E2512G         | 512 GB | 1       | 0     | 0     | 0.00   |
| PNY       | SSD2SC240GC2DH1... | 240 GB | 1       | 85    | 1023  | 0.00   |
| Intel     | SSDSC2KF256H6 SATA | 256 GB | 1       | 9     | 112   | 0.00   |
| Intel     | SSDSC2KF512H6 SATA | 512 GB | 1       | 7     | 84    | 0.00   |
| Micron    | MTFDDAT064MAM-1J2  | 64 GB  | 1       | 85    | 1039  | 0.00   |
| ADATA     | XM11 128GB-V3      | 128 GB | 1       | 77    | 1016  | 0.00   |
| ADATA     | AXM21S3-24GM-B     | 24 GB  | 1       | 77    | 1020  | 0.00   |
| Transcend | TS64GSSD340K       | 64 GB  | 1       | 74    | 1008  | 0.00   |
| Mushkin   | MKNSSDCR120GB-DX7  | 120 GB | 1       | 73    | 1016  | 0.00   |
| SandForce | 906190             | 64 GB  | 1       | 65    | 1018  | 0.00   |
| PNY       | SSD2SC120G3LC72... | 120 GB | 1       | 65    | 1019  | 0.00   |
| ADATA     | SP900NS38          | 512 GB | 1       | 64    | 1020  | 0.00   |
| MaxDig... | MD300 128G         | 128 GB | 1       | 41    | 666   | 0.00   |
| SanDisk   | SD9SN8W-128G-1006  | 128 GB | 23      | 49    | 991   | 0.00   |
| Kingston  | SNS4151S316GD      | 16 GB  | 1       | 51    | 1022  | 0.00   |
| Lite-On   | LMT-128M3M         | 128 GB | 1       | 44    | 1009  | 0.00   |
| DOGGO     | DQ-60G             | 64 GB  | 2       | 0     | 0     | 0.00   |
| Intel     | SSDSC2BB150G7      | 150 GB | 1       | 0     | 0     | 0.00   |
| KingDian  | S180               | 120 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TS16GCFX600I       | 16 GB  | 1       | 0     | 0     | 0.00   |
| Transcend | TS64GSSD420I       | 64 GB  | 1       | 0     | 0     | 0.00   |
| ADATA     | SX300              | 64 GB  | 1       | 32    | 1020  | 0.00   |
| Intel     | SSDSCKKB240G8R     | 240 GB | 1       | 31    | 1026  | 0.00   |
| Lite-On   | CV8-8E128-HP       | 128 GB | 17      | 28    | 1007  | 0.00   |
| SanDisk   | TE22D10400GE8001   | 400 GB | 1       | 34    | 2047  | 0.00   |
| Lite-On   | CV8-8E256-HP       | 256 GB | 1       | 16    | 1007  | 0.00   |
| AMD       | R5S120GBSF         | 120 GB | 1       | 15    | 1016  | 0.00   |
| JIAWEI    | SSD                | 240 GB | 1       | 47    | 3057  | 0.00   |
| Intel     | SSDSC2KW360H6      | 360 GB | 2       | 16    | 1365  | 0.00   |
| Neo Forza | NFS011SA356-600... | 256 GB | 1       | 41    | 3130  | 0.00   |
| Intel     | SSDSC2KF240H6L     | 240 GB | 1       | 16    | 2012  | 0.00   |
| WDC       | PC SA530 SDASN8... | 256 GB | 2       | 8     | 999   | 0.00   |
| SPCC      | M.2 SSD            | 1 TB   | 1       | 10    | 2711  | 0.00   |
| Mushkin   | MKNSSDCR250GB-7... | 250 GB | 1       | 3     | 1016  | 0.00   |
| ADATA     | SX910              | 512 GB | 1       | 3     | 1018  | 0.00   |
| Micron    | MTFDDAV256TDL-1... | 256 GB | 6       | 2     | 1008  | 0.00   |
| Samsung   | MZNLH128HBHQ-000H1 | 128 GB | 1       | 0     | 100   | 0.00   |
| Intel     | SSDSC2KG400G7M ... | 400 GB | 1       | 2     | 1025  | 0.00   |
| SanDisk   | sandisk120         | 120 GB | 1       | 0     | 21    | 0.00   |
| Kingston  | EK60HYXTFY176 V100 | 64 GB  | 1       | 1     | 1130  | 0.00   |
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

| MFG       | Family                 | Models | Samples | Days  | Err   | MTBF   |
|-----------|------------------------|--------|---------|-------|-------|--------|
| Intel     | X25-E SSDs             | 2      | 4       | 2237  | 0     | 6.13   |
| Crucial   | RealSSD C300/P300      | 1      | 3       | 1525  | 336   | 3.36   |
| Micron    | MX100/MX200/M5x0/M6... | 1      | 1       | 1083  | 0     | 2.97   |
| SandForce | SandForce Driven SSDs  | 2      | 2       | 1209  | 208   | 2.88   |
| Intel     | X18-M/X25-M G1 SSDs    | 4      | 4       | 1037  | 0     | 2.84   |
| Intel     | 730 and DC S35x0/36... | 26     | 78      | 1192  | 106   | 2.78   |
| Hyundai   | Unknown                | 1      | 1       | 997   | 0     | 2.73   |
| Toshiba   | HG2 Series             | 2      | 7       | 932   | 0     | 2.55   |
| SanDisk   | SATA Cloudspeed Max... | 1      | 1       | 916   | 0     | 2.51   |
| Crucial   | RealSSD m4/C400/P400   | 6      | 98      | 993   | 146   | 2.35   |
| HPE       | Unknown                | 3      | 3       | 831   | 0     | 2.28   |
| Intel     | 730 and DC S3500/S3... | 1      | 2       | 801   | 0     | 2.20   |
| Toshiba   | HG3 Series             | 3      | 5       | 766   | 0     | 2.10   |
| Toshiba   | HG5 Series             | 1      | 4       | 738   | 0     | 2.02   |
| Micro ... | Unknown                | 1      | 1       | 722   | 0     | 1.98   |
| OCZ       | Indilinx Barefoot b... | 5      | 8       | 808   | 1     | 1.95   |
| Kingston  | JMicron/Maxiotek ba... | 1      | 1       | 674   | 0     | 1.85   |
| Crucial   | RealSSD m4/C400        | 3      | 8       | 664   | 0     | 1.82   |
| OWC       | SandForce Driven SSDs  | 3      | 11      | 727   | 1     | 1.81   |
| Axiom     | Unknown                | 2      | 2       | 644   | 0     | 1.77   |
| MyDigi... | Unknown                | 4      | 6       | 605   | 0     | 1.66   |
| OCZ       | SandForce Driven SSDs  | 41     | 323     | 769   | 42    | 1.64   |
| SATADOM   | Innodisk 3IE3/3ME3/... | 1      | 1       | 574   | 0     | 1.57   |
| Corsair   | SandForce Driven SSDs  | 24     | 166     | 694   | 92    | 1.51   |
| Intel     | 520 Series SSDs        | 7      | 108     | 707   | 207   | 1.50   |
| Intel     | 320 Series SSDs        | 9      | 58      | 573   | 1     | 1.48   |
| Crucial   | RealSSD C300/M500      | 2      | 7       | 538   | 0     | 1.47   |
| OCZ       | Indilinx Barefoot_2... | 12     | 135     | 649   | 3     | 1.45   |
| Apple     | JMicron based SSDs     | 3      | 13      | 520   | 0     | 1.43   |
| AFOX      | Unknown                | 1      | 1       | 518   | 0     | 1.42   |
| Radeon    | Indilinx Barefoot 3... | 1      | 3       | 514   | 0     | 1.41   |
| Kingston  | JMicron based SSDs     | 14     | 47      | 719   | 3     | 1.39   |
| Intel     | 330/335 Series SSDs    | 6      | 56      | 653   | 1     | 1.37   |
| ADATA     | JMicron based SSDs     | 7      | 39      | 470   | 1     | 1.28   |
| Micron    | RealSSD m4/C400/P400   | 8      | 32      | 482   | 253   | 1.27   |
| Toshiba   | HG6 Series SSD         | 16     | 57      | 458   | 1     | 1.25   |
| XSTAR     | Unknown                | 1      | 1       | 455   | 0     | 1.25   |
| Innodisk  | 3IE3/3ME3/3ME4 SSDs    | 2      | 3       | 446   | 0     | 1.22   |
| Micron    | 5100 Pro / 5200 SSDs   | 5      | 18      | 558   | 19    | 1.22   |
| Micron    | RealSSD m4/C400        | 2      | 3       | 433   | 0     | 1.19   |
| Toshiba   | HG5d Series            | 8      | 17      | 513   | 39    | 1.17   |
| Intel     | 510 Series SSDs        | 2      | 5       | 425   | 0     | 1.17   |
| Toshiba   | JMicron based SSDs     | 2      | 2       | 421   | 0     | 1.16   |
| Apple     | SD/SM/TS E/F/G SSDs    | 13     | 63      | 412   | 0     | 1.13   |
| ADATA     | SandForce Driven SSDs  | 14     | 101     | 448   | 5     | 1.09   |
| Samsung   | Samsung based SSDs     | 273    | 4087    | 403   | 7     | 1.08   |
| WDC       | Unknown                | 5      | 8       | 381   | 250   | 1.04   |
| Seagate   | Indilinx Barefoot b... | 1      | 1       | 378   | 0     | 1.04   |
| Corsair   | Indilinx Barefoot b... | 3      | 4       | 465   | 1     | 1.03   |
| Innodisk  | Unknown                | 4      | 4       | 360   | 0     | 0.99   |
| KingShare | Unknown                | 1      | 1       | 358   | 0     | 0.98   |
| CFD       | Unknown                | 1      | 1       | 354   | 0     | 0.97   |
| Toshiba   | OCZ                    | 4      | 10      | 414   | 1     | 0.96   |
| Kingston  | SandForce Driven SSDs  | 36     | 1110    | 401   | 50    | 0.93   |
| OCZ       | Indilinx Barefoot 3... | 16     | 79      | 368   | 27    | 0.90   |
| OCZ       | OCZ/Toshiba Trion SSDs | 5      | 27      | 340   | 1     | 0.89   |
| Toshiba   | OCZ/Toshiba Trion SSDs | 5      | 33      | 355   | 1     | 0.88   |
| Intel     | S3520 Series SSDs      | 1      | 1       | 317   | 0     | 0.87   |
| Mushkin   | SandForce Driven SSDs  | 13     | 16      | 519   | 255   | 0.84   |
| Transcend | SandForce Driven SSDs  | 5      | 8       | 291   | 0     | 0.80   |
| Transcend | JMicron based SSDs     | 7      | 19      | 319   | 107   | 0.79   |
| Goodram   | Phison Driven OEM SSDs | 4      | 46      | 286   | 0     | 0.78   |
| Phison    | Unknown                | 8      | 8       | 291   | 1     | 0.78   |
| Intel     | X18-M/X25-M/X25-V G... | 12     | 50      | 778   | 8     | 0.77   |
| Intel     | 53x and Pro 1500/25... | 10     | 81      | 402   | 3     | 0.75   |
| Team      | Silicon Motion base... | 4      | 12      | 274   | 0     | 0.75   |
| Kingston  | SSDNow UV400           | 3      | 239     | 296   | 53    | 0.74   |
| imation   | Unknown                | 1      | 1       | 264   | 0     | 0.73   |
| BlueRay   | Unknown                | 3      | 3       | 254   | 0     | 0.70   |
| Plextor   | M3/M5/M6/M7 Series ... | 6      | 15      | 253   | 0     | 0.69   |
| SanDisk   | SanDisk based SSDs     | 31     | 249     | 284   | 24    | 0.69   |
| ADATA     | JMicron/Maxiotek ba... | 1      | 3       | 247   | 0     | 0.68   |
| Toshiba   | Unknown                | 50     | 163     | 256   | 8     | 0.67   |
| Intel     | 525 Series SSDs        | 3      | 5       | 365   | 1     | 0.66   |
| Intel     | 530 Series SSDs        | 2      | 41      | 324   | 1     | 0.65   |
| Micron    | BX/MX1/2/3/500, M5/... | 5      | 11      | 271   | 2     | 0.65   |
| Hoodisk   | Phison Driven OEM SSDs | 3      | 9       | 236   | 0     | 0.65   |
| SanDisk   | Marvell based SanDi... | 70     | 729     | 249   | 17    | 0.63   |
| Corsair   | Phison Driven SSDs     | 2      | 10      | 223   | 0     | 0.61   |
| Intenso   | Phison Driven OEM SSDs | 3      | 44      | 229   | 1     | 0.61   |
| Plextor   | M3/M5 (Pro) Series ... | 4      | 15      | 291   | 70    | 0.60   |
| Hoodisk   | Unknown                | 1      | 1       | 214   | 0     | 0.59   |
| Patriot   | Unknown                | 19     | 34      | 340   | 90    | 0.58   |
| Micron    | 5100 Pro / 52x0 / 5... | 2      | 3       | 212   | 0     | 0.58   |
| Crucial   | MX1/2/300, M5/600, ... | 2      | 10      | 405   | 8     | 0.58   |
| Apple     | Unknown                | 4      | 8       | 380   | 298   | 0.57   |
| Corsair   | Unknown                | 19     | 35      | 490   | 67    | 0.57   |
| Crucial   | BX/MX1/2/3/500, M5/... | 39     | 804     | 272   | 34    | 0.56   |
| Ramaxel   | Unknown                | 2      | 3       | 204   | 0     | 0.56   |
| Smartbuy  | Phison Driven SSDs     | 4      | 124     | 211   | 1     | 0.55   |
| SK hynix  | SATA SSDs              | 26     | 197     | 244   | 50    | 0.55   |
| PNY       | Phison Driven SSDs     | 8      | 115     | 194   | 0     | 0.53   |
| Kingston  | Unknown                | 78     | 175     | 237   | 72    | 0.53   |
| Palit     | Unknown                | 4      | 6       | 191   | 0     | 0.52   |
| Intel     | Dell Certified Inte... | 1      | 1       | 188   | 0     | 0.52   |
| SanDisk   | SandForce Driven SSDs  | 6      | 213     | 209   | 26    | 0.51   |
| Samsung   | Unknown                | 32     | 230     | 197   | 2     | 0.50   |
| Kston     | Unknown                | 1      | 3       | 181   | 0     | 0.50   |
| Phison    | Driven OEM SSDs        | 9      | 76      | 177   | 0     | 0.49   |
| SanDisk   | Unknown                | 121    | 406     | 187   | 85    | 0.48   |
| WDC       | Blue / Red / Green ... | 9      | 34      | 169   | 0     | 0.46   |
| Seagate   | Unknown                | 17     | 50      | 255   | 82    | 0.46   |
| KingFast  | Silicon Motion base... | 1      | 9       | 164   | 0     | 0.45   |
| Intel     | Unknown                | 54     | 136     | 209   | 63    | 0.45   |
| Micron    | BX/MX1/2/3/500, M5/... | 14     | 160     | 201   | 55    | 0.45   |
| Zheino    | Silicon Motion base... | 1      | 2       | 158   | 0     | 0.43   |
| KingFast  | Unknown                | 8      | 32      | 162   | 97    | 0.43   |
| SPCC      | Unknown                | 22     | 59      | 341   | 341   | 0.43   |
| SPCC      | Phison Driven OEM SSDs | 8      | 376     | 187   | 77    | 0.42   |
| Hajaan    | Unknown                | 1      | 2       | 151   | 0     | 0.42   |
| Transcend | Unknown                | 12     | 15      | 195   | 137   | 0.41   |
| Pioneer   | Unknown                | 4      | 7       | 149   | 0     | 0.41   |
| OCZ       | Unknown                | 8      | 11      | 355   | 93    | 0.41   |
| ZTC       | Unknown                | 2      | 3       | 143   | 0     | 0.39   |
| Patriot   | Phison Driven SSDs     | 9      | 149     | 144   | 1     | 0.39   |
| Verbatim  | Unknown                | 5      | 10      | 151   | 102   | 0.39   |
| Goodram   | Unknown                | 23     | 76      | 152   | 1     | 0.39   |
| Plextor   | Unknown                | 31     | 82      | 152   | 1     | 0.39   |
| UNIC2     | Unknown                | 1      | 1       | 139   | 0     | 0.38   |
| MENGMI    | Unknown                | 1      | 1       | 139   | 0     | 0.38   |
| Mushkin   | Silicon Motion base... | 4      | 9       | 138   | 0     | 0.38   |
| HP        | Unknown                | 14     | 45      | 147   | 1     | 0.37   |
| Micron    | Unknown                | 27     | 63      | 251   | 205   | 0.37   |
| Lumino... | Unknown                | 2      | 2       | 135   | 0     | 0.37   |
| ZOTAC     | Unknown                | 2      | 3       | 132   | 0     | 0.36   |
| Kingston  | Phison Driven SSDs     | 17     | 1336    | 139   | 1     | 0.35   |
| Intel     | 53x and Pro 2500 Se... | 4      | 4       | 129   | 0     | 0.35   |
| KLEVV     | Unknown                | 1      | 1       | 127   | 0     | 0.35   |
| Chiprex   | Unknown                | 1      | 1       | 126   | 0     | 0.35   |
| WDC       | Blue and Green SSDs    | 31     | 926     | 131   | 2     | 0.34   |
| Micron    | Client SSDs            | 6      | 30      | 133   | 35    | 0.34   |
| Advantech | Unknown                | 3      | 3       | 123   | 0     | 0.34   |
| Vaseky    | Unknown                | 11     | 13      | 122   | 0     | 0.34   |
| GALAX     | Unknown                | 2      | 4       | 122   | 0     | 0.34   |
| Hypertec  | Unknown                | 1      | 2       | 371   | 512   | 0.33   |
| Plextor   | M3/M5/M6 Series SSDs   | 17     | 181     | 135   | 34    | 0.33   |
| Indilinx  | Unknown                | 3      | 4       | 117   | 2     | 0.32   |
| Samsung   | SandForce Driven SSDs  | 1      | 1       | 115   | 0     | 0.32   |
| TCSUNBOW  | Unknown                | 4      | 5       | 110   | 0     | 0.30   |
| Intenso   | Unknown                | 14     | 46      | 122   | 86    | 0.30   |
| ADATA     | Unknown                | 63     | 228     | 206   | 170   | 0.30   |
| Kingston  | SSDNow UV400/500       | 8      | 91      | 112   | 40    | 0.29   |
| Mushkin   | Unknown                | 10     | 12      | 295   | 338   | 0.29   |
| Transcend | Indilinx Barefoot b... | 1      | 1       | 309   | 2     | 0.28   |
| Crucial   | MX500 SSDs             | 6      | 418     | 103   | 6     | 0.28   |
| Phison    | Phison Driven SSDs     | 1      | 1       | 101   | 0     | 0.28   |
| Intel     | 545s Series SSDs       | 8      | 58      | 106   | 1     | 0.27   |
| AMD       | Silicon Motion base... | 1      | 1       | 98    | 0     | 0.27   |
| Anobit    | Unknown                | 1      | 1       | 96    | 0     | 0.27   |
| Golden... | Unknown                | 2      | 2       | 96    | 0     | 0.26   |
| Smartbuy  | Unknown                | 13     | 19      | 95    | 0     | 0.26   |
| GOWE      | Unknown                | 1      | 1       | 284   | 2     | 0.26   |
| Gigabyte  | Phison Driven SSDs     | 4      | 43      | 94    | 0     | 0.26   |
| ORICO     | Unknown                | 2      | 2       | 94    | 0     | 0.26   |
| KingDian  | Unknown                | 13     | 43      | 108   | 155   | 0.26   |
| Team      | Unknown                | 30     | 66      | 102   | 5     | 0.26   |
| Kingmax   | Unknown                | 4      | 56      | 218   | 377   | 0.25   |
| Goodram   | Phison Driven SSDs     | 5      | 49      | 91    | 0     | 0.25   |
| Platinet  | Unknown                | 1      | 2       | 91    | 0     | 0.25   |
| Transcend | JMicron/Maxiotek ba... | 2      | 2       | 127   | 504   | 0.25   |
| ADATA     | Silicon Motion base... | 14     | 252     | 103   | 22    | 0.25   |
| Intel     | S4510/S4610/S4500/S... | 11     | 32      | 90    | 33    | 0.25   |
| Integral  | Unknown                | 3      | 11      | 89    | 0     | 0.24   |
| V-GeN     | Unknown                | 5      | 5       | 88    | 0     | 0.24   |
| Transcend | Silicon Motion base... | 32     | 146     | 89    | 1     | 0.24   |
| LDLC      | Unknown                | 8      | 25      | 98    | 1     | 0.24   |
| China     | Unknown                | 73     | 386     | 96    | 5     | 0.24   |
| PNY       | Unknown                | 32     | 52      | 108   | 100   | 0.24   |
| Apacer    | AS340 SSDs             | 3      | 31      | 90    | 1     | 0.24   |
| SK hynix  | Unknown                | 34     | 100     | 224   | 169   | 0.23   |
| Ramsta    | Unknown                | 2      | 2       | 83    | 0     | 0.23   |
| Crucial   | Silicon Motion base... | 6      | 68      | 82    | 1     | 0.22   |
| GeIL      | Unknown                | 8      | 10      | 105   | 103   | 0.22   |
| Gigabyte  | Unknown                | 3      | 5       | 81    | 0     | 0.22   |
| Londisk   | Unknown                | 3      | 11      | 80    | 0     | 0.22   |
| Patriot   | Silicon Motion base... | 4      | 13      | 111   | 7     | 0.22   |
| Seagate   | 600 Series             | 1      | 1       | 79    | 0     | 0.22   |
| Apple     | SD/SM/TS E/F SSDs      | 2      | 4       | 597   | 6     | 0.21   |
| Toshiba   | HG6 Series             | 1      | 2       | 76    | 0     | 0.21   |
| Neo Forza | Unknown                | 3      | 3       | 191   | 1046  | 0.21   |
| Silicon   | Motion based OEM SSDs  | 2      | 2       | 75    | 0     | 0.21   |
| Lite-On   | Silicon Motion base... | 5      | 10      | 75    | 1     | 0.21   |
| KingDian  | Silicon Motion base... | 10     | 59      | 79    | 3     | 0.21   |
| Apacer    | Unknown                | 13     | 81      | 73    | 1     | 0.20   |
| Transcend | SiliconMotion based... | 10     | 81      | 72    | 0     | 0.20   |
| e2e4      | Unknown                | 4      | 7       | 72    | 0     | 0.20   |
| Crucial   | Unknown                | 8      | 8       | 172   | 2     | 0.20   |
| INNOVA... | Unknown                | 4      | 5       | 71    | 0     | 0.20   |
| Crucial   | Client SSDs            | 3      | 25      | 104   | 1     | 0.19   |
| oyunkey   | Unknown                | 1      | 1       | 68    | 0     | 0.19   |
| ViperTeq  | Unknown                | 1      | 1       | 68    | 0     | 0.19   |
| Lite-On   | Unknown                | 88     | 204     | 82    | 138   | 0.19   |
| BRAVEE... | Unknown                | 2      | 2       | 65    | 0     | 0.18   |
| BIOSTAR   | Unknown                | 4      | 5       | 63    | 0     | 0.17   |
| DOGFISH   | Unknown                | 4      | 4       | 62    | 0     | 0.17   |
| Seagate   | Nytro SATA SSD         | 2      | 8       | 62    | 0     | 0.17   |
| Faspeed   | Unknown                | 7      | 7       | 61    | 0     | 0.17   |
| Netac     | Unknown                | 14     | 29      | 60    | 0     | 0.17   |
| KingSpec  | Unknown                | 44     | 118     | 70    | 33    | 0.17   |
| Zheino    | Unknown                | 16     | 21      | 72    | 2     | 0.17   |
| AMD       | Unknown                | 8      | 38      | 69    | 28    | 0.16   |
| AGI       | Unknown                | 1      | 1       | 59    | 0     | 0.16   |
| TEKET     | Unknown                | 1      | 2       | 59    | 0     | 0.16   |
| AMD       | SiliconMotion based... | 1      | 28      | 58    | 1     | 0.16   |
| DeTech    | Unknown                | 1      | 1       | 57    | 0     | 0.16   |
| GLOWAY    | Unknown                | 7      | 10      | 55    | 0     | 0.15   |
| Aoluska   | Unknown                | 1      | 1       | 54    | 0     | 0.15   |
| Leven     | Unknown                | 5      | 10      | 53    | 0     | 0.15   |
| IPLEX     | Unknown                | 1      | 1       | 52    | 0     | 0.14   |
| Foxline   | Unknown                | 8      | 11      | 142   | 93    | 0.14   |
| Seagate   | IronWolf 110 SATA SSD  | 1      | 4       | 51    | 0     | 0.14   |
| T-FORCE   | Unknown                | 3      | 6       | 50    | 0     | 0.14   |
| BHT       | Unknown                | 5      | 11      | 48    | 0     | 0.13   |
| Fujitsu   | Unknown                | 5      | 5       | 45    | 0     | 0.13   |
| Lenovo    | Unknown                | 4      | 7       | 45    | 0     | 0.12   |
| Hikvision | Unknown                | 9      | 10      | 53    | 1     | 0.12   |
| PRETEC    | Unknown                | 1      | 1       | 44    | 0     | 0.12   |
| XPG       | Unknown                | 1      | 2       | 44    | 0     | 0.12   |
| Ramsta    | Silicon Motion base... | 1      | 1       | 43    | 0     | 0.12   |
| Intel     | SSD Pro 5400s Series   | 1      | 1       | 42    | 0     | 0.12   |
| QUMO      | Unknown                | 4      | 8       | 192   | 254   | 0.12   |
| Kingrich  | Unknown                | 5      | 6       | 139   | 2     | 0.11   |
| Super ... | Unknown                | 2      | 3       | 41    | 0     | 0.11   |
| Union ... | Unknown                | 1      | 3       | 41    | 0     | 0.11   |
| RCESSD    | Unknown                | 1      | 1       | 41    | 0     | 0.11   |
| Fordisk   | Unknown                | 2      | 2       | 41    | 0     | 0.11   |
| Lexar     | Unknown                | 7      | 26      | 40    | 0     | 0.11   |
| Goldkey   | Unknown                | 2      | 2       | 39    | 0     | 0.11   |
| KingSpec  | JMicron/Maxiotek ba... | 2      | 7       | 54    | 3     | 0.10   |
| Colorful  | Unknown                | 4      | 7       | 59    | 34    | 0.10   |
| TCSUNBOW  | Silicon Motion base... | 3      | 6       | 37    | 0     | 0.10   |
| Apacer    | SDM4 Series SSD Module | 1      | 2       | 37    | 0     | 0.10   |
| Reeinno   | Unknown                | 2      | 2       | 37    | 0     | 0.10   |
| ADATA     | SiliconMotion based... | 1      | 33      | 38    | 1     | 0.10   |
| OCZ       | Intrepid 3000 SSDs     | 2      | 2       | 35    | 0     | 0.10   |
| Dogfish   | Unknown                | 9      | 14      | 34    | 0     | 0.10   |
| Maxtor    | Unknown                | 2      | 8       | 34    | 0     | 0.09   |
| OWC       | Unknown                | 3      | 4       | 34    | 0     | 0.09   |
| SUNEAST   | Unknown                | 3      | 3       | 34    | 0     | 0.09   |
| RECADATA  | Unknown                | 1      | 1       | 33    | 0     | 0.09   |
| BIWIN     | Unknown                | 5      | 15      | 57    | 206   | 0.09   |
| Toshiba   | SG2 Series             | 1      | 1       | 32    | 0     | 0.09   |
| Intenso   | Silicon Motion base... | 1      | 9       | 34    | 57    | 0.08   |
| EMTEC     | Unknown                | 5      | 5       | 30    | 0     | 0.08   |
| TAMMUZ    | Unknown                | 2      | 2       | 29    | 0     | 0.08   |
| KingPower | Unknown                | 1      | 1       | 29    | 0     | 0.08   |
| KIOXIA... | Unknown                | 2      | 5       | 29    | 0     | 0.08   |
| FORESEE   | Unknown                | 6      | 26      | 29    | 0     | 0.08   |
| Crucial   | SiliconMotion based... | 1      | 3       | 28    | 0     | 0.08   |
| Apple     | MacBook Air SSD        | 1      | 4       | 105   | 47    | 0.08   |
| TAISU     | Unknown                | 1      | 1       | 27    | 0     | 0.08   |
| SenDisk   | Unknown                | 1      | 1       | 27    | 0     | 0.08   |
| HECTRON   | Unknown                | 1      | 1       | 26    | 0     | 0.07   |
| Pasoul    | Unknown                | 1      | 1       | 25    | 0     | 0.07   |
| XrayDisk  | Unknown                | 5      | 12      | 25    | 0     | 0.07   |
| SMI       | Unknown                | 6      | 6       | 23    | 327   | 0.07   |
| Teclast   | Unknown                | 8      | 14      | 23    | 0     | 0.07   |
| SNR       | Unknown                | 1      | 1       | 23    | 0     | 0.07   |
| tigo      | Unknown                | 3      | 3       | 22    | 0     | 0.06   |
| ELSKY     | Unknown                | 1      | 1       | 21    | 0     | 0.06   |
| OSCOO     | Unknown                | 1      | 1       | 21    | 0     | 0.06   |
| XUNZHE    | Unknown                | 1      | 1       | 20    | 0     | 0.05   |
| BAITITON  | Unknown                | 3      | 3       | 19    | 0     | 0.05   |
| Drevo     | Silicon Motion base... | 1      | 4       | 214   | 17    | 0.05   |
| DGM       | Unknown                | 1      | 1       | 18    | 0     | 0.05   |
| Hyperdisk | Unknown                | 1      | 1       | 18    | 0     | 0.05   |
| Kingston  | Silicon Motion base... | 3      | 29      | 17    | 0     | 0.05   |
| KINGBANK  | Unknown                | 1      | 2       | 17    | 0     | 0.05   |
| LDNDISK   | Unknown                | 1      | 1       | 16    | 0     | 0.05   |
| AEGO      | Unknown                | 1      | 3       | 16    | 0     | 0.04   |
| XUM       | Unknown                | 1      | 1       | 16    | 0     | 0.04   |
| Kingch... | Unknown                | 5      | 5       | 15    | 0     | 0.04   |
| Leven     | Silicon Motion base... | 1      | 1       | 15    | 0     | 0.04   |
| Seagate   | 600 Pro Series         | 1      | 1       | 14    | 0     | 0.04   |
| Drevo     | Unknown                | 3      | 4       | 89    | 513   | 0.04   |
| Maximus   | Unknown                | 2      | 2       | 13    | 0     | 0.04   |
| Varro     | Unknown                | 1      | 1       | 12    | 0     | 0.03   |
| addlink   | Unknown                | 2      | 2       | 12    | 0     | 0.03   |
| Silico... | Unknown                | 1      | 1       | 12    | 0     | 0.03   |
| Wicgtyp   | Unknown                | 1      | 1       | 12    | 0     | 0.03   |
| Dell      | Unknown                | 3      | 6       | 12    | 0     | 0.03   |
| Micron    | MX1/2/300, M5/600, ... | 1      | 1       | 11    | 0     | 0.03   |
| Yeyian    | Unknown                | 2      | 2       | 11    | 0     | 0.03   |
| Golden... | Unknown                | 1      | 1       | 10    | 0     | 0.03   |
| Microtech | Unknown                | 1      | 1       | 9     | 0     | 0.03   |
| Getrich   | Unknown                | 1      | 1       | 8     | 0     | 0.02   |
| Kingspeed | Unknown                | 1      | 1       | 8     | 0     | 0.02   |
| FASTDISK  | Unknown                | 6      | 6       | 7     | 0     | 0.02   |
| QNIX      | Unknown                | 1      | 1       | 6     | 0     | 0.02   |
| ShanDi... | Unknown                | 3      | 5       | 5     | 0     | 0.01   |
| Iod       | Unknown                | 1      | 1       | 5     | 0     | 0.01   |
| Apacer    | SDM5/5A/5A-M Series... | 2      | 6       | 156   | 51    | 0.01   |
| 2-Power   | Unknown                | 1      | 1       | 4     | 0     | 0.01   |
| PHINOCOM  | Unknown                | 1      | 1       | 4     | 0     | 0.01   |
| KODAK     | Unknown                | 1      | 1       | 4     | 0     | 0.01   |
| INDMEM    | Unknown                | 2      | 2       | 3     | 0     | 0.01   |
| Intel     | 311/313 Series SSDs    | 1      | 1       | 112   | 30    | 0.01   |
| Pacifi... | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| ShineDisk | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| Timetec   | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| i-Flas... | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| Intel     | 540 Series SSDs        | 6      | 16      | 10    | 250   | 0.01   |
| Smart     | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| Star D... | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| Pichau    | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| MaxDig... | Unknown                | 2      | 2       | 23    | 333   | 0.01   |
| Gigastone | Unknown                | 1      | 1       | 2     | 0     | 0.01   |
| SOLIDATA  | Unknown                | 1      | 1       | 2420  | 1019  | 0.01   |
| Innodisk  | 3IE2/3ME2/3MG2/3SE2... | 1      | 1       | 2     | 0     | 0.01   |
| ACPI      | Unknown                | 1      | 1       | 2     | 0     | 0.01   |
| VSEVEN    | Unknown                | 1      | 1       | 2     | 0     | 0.01   |
| ASENNO    | Unknown                | 1      | 2       | 1     | 0     | 0.00   |
| Yunhai... | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| Mcpoint   | Unknown                | 1      | 1       | 6     | 3     | 0.00   |
| acpi      | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| S3+       | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| BR        | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| OEM       | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| ORTIAL    | Unknown                | 1      | 3       | 0     | 0     | 0.00   |
| Kross ... | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Eluktro   | Unknown                | 1      | 1       | 806   | 1016  | 0.00   |
| HP Phison | Unknown                | 1      | 1       | 717   | 1033  | 0.00   |
| UMAX      | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Liren     | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Gost      | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| DERLAR    | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| TEUTONS   | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Bamba     | Unknown                | 1      | 1       | 60    | 249   | 0.00   |
| Myung     | Unknown                | 1      | 1       | 228   | 1015  | 0.00   |
| Goldenfir | Unknown                | 2      | 2       | 2     | 14    | 0.00   |
| AXIOMTEK  | Unknown                | 2      | 2       | 0     | 0     | 0.00   |
| Dahua     | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| SandForce | Unknown                | 1      | 1       | 65    | 1018  | 0.00   |
| DOGGO     | Unknown                | 1      | 2       | 0     | 0     | 0.00   |
| JIAWEI    | Unknown                | 1      | 1       | 47    | 3057  | 0.00   |

SSD by Vendor
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF   |
|-------------|--------|---------|-------|-------|--------|
| Hyundai     | 1      | 1       | 997   | 0     | 2.73   |
| HPE         | 3      | 3       | 831   | 0     | 2.28   |
| Micro Ce... | 1      | 1       | 722   | 0     | 1.98   |
| SandForce   | 3      | 3       | 828   | 478   | 1.92   |
| Axiom       | 2      | 2       | 644   | 0     | 1.77   |
| MyDigita... | 4      | 6       | 605   | 0     | 1.66   |
| SATADOM     | 1      | 1       | 574   | 0     | 1.57   |
| OCZ         | 89     | 585     | 658   | 29    | 1.44   |
| AFOX        | 1      | 1       | 518   | 0     | 1.42   |
| Radeon      | 1      | 3       | 514   | 0     | 1.41   |
| OWC         | 6      | 15      | 542   | 1     | 1.35   |
| Corsair     | 48     | 215     | 635   | 82    | 1.30   |
| XSTAR       | 1      | 1       | 455   | 0     | 1.25   |
| Intel       | 171    | 742     | 514   | 61    | 1.08   |
| Samsung     | 306    | 4318    | 392   | 6     | 1.04   |
| Apple       | 23     | 92      | 419   | 29    | 1.04   |
| KingShare   | 1      | 1       | 358   | 0     | 0.98   |
| CFD         | 1      | 1       | 354   | 0     | 0.97   |
| Innodisk    | 7      | 8       | 347   | 0     | 0.95   |
| Toshiba     | 93     | 301     | 355   | 7     | 0.93   |
| imation     | 1      | 1       | 264   | 0     | 0.73   |
| BlueRay     | 3      | 3       | 254   | 0     | 0.70   |
| Hoodisk     | 4      | 10      | 234   | 0     | 0.64   |
| Kingston    | 160    | 3028    | 260   | 28    | 0.62   |
| Crucial     | 77     | 1452    | 266   | 31    | 0.59   |
| SanDisk     | 229    | 1598    | 234   | 37    | 0.59   |
| Micron      | 71     | 322     | 259   | 97    | 0.57   |
| Ramaxel     | 2      | 3       | 204   | 0     | 0.56   |
| Mushkin     | 27     | 37      | 354   | 220   | 0.55   |
| Palit       | 4      | 6       | 191   | 0     | 0.52   |
| Phison      | 18     | 85      | 187   | 1     | 0.51   |
| Smartbuy    | 17     | 143     | 196   | 1     | 0.51   |
| Kston       | 1      | 3       | 181   | 0     | 0.50   |
| Goodram     | 32     | 171     | 170   | 1     | 0.45   |
| ADATA       | 100    | 656     | 211   | 68    | 0.45   |
| PNY         | 40     | 167     | 167   | 31    | 0.44   |
| SK hynix    | 60     | 297     | 237   | 90    | 0.44   |
| KingFast    | 9      | 41      | 163   | 76    | 0.43   |
| SPCC        | 30     | 435     | 208   | 113   | 0.42   |
| Intenso     | 18     | 99      | 162   | 45    | 0.42   |
| Hajaan      | 1      | 2       | 151   | 0     | 0.42   |
| Patriot     | 32     | 196     | 176   | 17    | 0.41   |
| Pioneer     | 4      | 7       | 149   | 0     | 0.41   |
| Seagate     | 23     | 65      | 214   | 64    | 0.40   |
| ZTC         | 2      | 3       | 143   | 0     | 0.39   |
| Verbatim    | 5      | 10      | 151   | 102   | 0.39   |
| UNIC2       | 1      | 1       | 139   | 0     | 0.38   |
| MENGMI      | 1      | 1       | 139   | 0     | 0.38   |
| Plextor     | 58     | 293     | 154   | 25    | 0.38   |
| HP          | 14     | 45      | 147   | 1     | 0.37   |
| LuminouTek  | 2      | 2       | 135   | 0     | 0.37   |
| ZOTAC       | 2      | 3       | 132   | 0     | 0.36   |
| WDC         | 45     | 968     | 135   | 4     | 0.35   |
| KLEVV       | 1      | 1       | 127   | 0     | 0.35   |
| Chiprex     | 1      | 1       | 126   | 0     | 0.35   |
| Advantech   | 3      | 3       | 123   | 0     | 0.34   |
| Vaseky      | 11     | 13      | 122   | 0     | 0.34   |
| GALAX       | 2      | 4       | 122   | 0     | 0.34   |
| Hypertec    | 1      | 2       | 371   | 512   | 0.33   |
| Team        | 34     | 78      | 129   | 4     | 0.33   |
| Indilinx    | 3      | 4       | 117   | 2     | 0.32   |
| Transcend   | 69     | 272     | 113   | 19    | 0.29   |
| Anobit      | 1      | 1       | 96    | 0     | 0.27   |
| Golden m... | 2      | 2       | 96    | 0     | 0.26   |
| GOWE        | 1      | 1       | 284   | 2     | 0.26   |
| ORICO       | 2      | 2       | 94    | 0     | 0.26   |
| Gigabyte    | 7      | 48      | 93    | 0     | 0.26   |
| Kingmax     | 4      | 56      | 218   | 377   | 0.25   |
| Platinet    | 1      | 2       | 91    | 0     | 0.25   |
| Integral    | 3      | 11      | 89    | 0     | 0.24   |
| V-GeN       | 5      | 5       | 88    | 0     | 0.24   |
| LDLC        | 8      | 25      | 98    | 1     | 0.24   |
| China       | 73     | 386     | 96    | 5     | 0.24   |
| KingDian    | 23     | 102     | 91    | 67    | 0.23   |
| GeIL        | 8      | 10      | 105   | 103   | 0.22   |
| Londisk     | 3      | 11      | 80    | 0     | 0.22   |
| Neo Forza   | 3      | 3       | 191   | 1046  | 0.21   |
| Silicon     | 2      | 2       | 75    | 0     | 0.21   |
| Apacer      | 19     | 120     | 81    | 3     | 0.20   |
| e2e4        | 4      | 7       | 72    | 0     | 0.20   |
| INNOVATI... | 4      | 5       | 71    | 0     | 0.20   |
| TCSUNBOW    | 7      | 11      | 71    | 0     | 0.19   |
| Ramsta      | 3      | 3       | 70    | 0     | 0.19   |
| Zheino      | 17     | 23      | 79    | 1     | 0.19   |
| oyunkey     | 1      | 1       | 68    | 0     | 0.19   |
| Lite-On     | 93     | 214     | 82    | 131   | 0.19   |
| ViperTeq    | 1      | 1       | 68    | 0     | 0.19   |
| BRAVEEAGLE  | 2      | 2       | 65    | 0     | 0.18   |
| BIOSTAR     | 4      | 5       | 63    | 0     | 0.17   |
| DOGFISH     | 4      | 4       | 62    | 0     | 0.17   |
| Faspeed     | 7      | 7       | 61    | 0     | 0.17   |
| Netac       | 14     | 29      | 60    | 0     | 0.17   |
| AMD         | 10     | 67      | 65    | 16    | 0.16   |
| KingSpec    | 46     | 125     | 70    | 32    | 0.16   |
| AGI         | 1      | 1       | 59    | 0     | 0.16   |
| TEKET       | 1      | 2       | 59    | 0     | 0.16   |
| DeTech      | 1      | 1       | 57    | 0     | 0.16   |
| GLOWAY      | 7      | 10      | 55    | 0     | 0.15   |
| Aoluska     | 1      | 1       | 54    | 0     | 0.15   |
| IPLEX       | 1      | 1       | 52    | 0     | 0.14   |
| Foxline     | 8      | 11      | 142   | 93    | 0.14   |
| T-FORCE     | 3      | 6       | 50    | 0     | 0.14   |
| Leven       | 6      | 11      | 50    | 0     | 0.14   |
| BHT         | 5      | 11      | 48    | 0     | 0.13   |
| Fujitsu     | 5      | 5       | 45    | 0     | 0.13   |
| Lenovo      | 4      | 7       | 45    | 0     | 0.12   |
| Hikvision   | 9      | 10      | 53    | 1     | 0.12   |
| PRETEC      | 1      | 1       | 44    | 0     | 0.12   |
| XPG         | 1      | 2       | 44    | 0     | 0.12   |
| QUMO        | 4      | 8       | 192   | 254   | 0.12   |
| Kingrich    | 5      | 6       | 139   | 2     | 0.11   |
| Super Ta... | 2      | 3       | 41    | 0     | 0.11   |
| Union Me... | 1      | 3       | 41    | 0     | 0.11   |
| RCESSD      | 1      | 1       | 41    | 0     | 0.11   |
| Fordisk     | 2      | 2       | 41    | 0     | 0.11   |
| Lexar       | 7      | 26      | 40    | 0     | 0.11   |
| Goldkey     | 2      | 2       | 39    | 0     | 0.11   |
| Colorful    | 4      | 7       | 59    | 34    | 0.10   |
| Reeinno     | 2      | 2       | 37    | 0     | 0.10   |
| Dogfish     | 9      | 14      | 34    | 0     | 0.10   |
| Maxtor      | 2      | 8       | 34    | 0     | 0.09   |
| SUNEAST     | 3      | 3       | 34    | 0     | 0.09   |
| RECADATA    | 1      | 1       | 33    | 0     | 0.09   |
| BIWIN       | 5      | 15      | 57    | 206   | 0.09   |
| EMTEC       | 5      | 5       | 30    | 0     | 0.08   |
| TAMMUZ      | 2      | 2       | 29    | 0     | 0.08   |
| KingPower   | 1      | 1       | 29    | 0     | 0.08   |
| KIOXIA-E... | 2      | 5       | 29    | 0     | 0.08   |
| FORESEE     | 6      | 26      | 29    | 0     | 0.08   |
| TAISU       | 1      | 1       | 27    | 0     | 0.08   |
| SenDisk     | 1      | 1       | 27    | 0     | 0.08   |
| HECTRON     | 1      | 1       | 26    | 0     | 0.07   |
| Pasoul      | 1      | 1       | 25    | 0     | 0.07   |
| XrayDisk    | 5      | 12      | 25    | 0     | 0.07   |
| SMI         | 6      | 6       | 23    | 327   | 0.07   |
| Teclast     | 8      | 14      | 23    | 0     | 0.07   |
| SNR         | 1      | 1       | 23    | 0     | 0.07   |
| tigo        | 3      | 3       | 22    | 0     | 0.06   |
| ELSKY       | 1      | 1       | 21    | 0     | 0.06   |
| OSCOO       | 1      | 1       | 21    | 0     | 0.06   |
| XUNZHE      | 1      | 1       | 20    | 0     | 0.05   |
| BAITITON    | 3      | 3       | 19    | 0     | 0.05   |
| DGM         | 1      | 1       | 18    | 0     | 0.05   |
| Hyperdisk   | 1      | 1       | 18    | 0     | 0.05   |
| KINGBANK    | 1      | 2       | 17    | 0     | 0.05   |
| LDNDISK     | 1      | 1       | 16    | 0     | 0.05   |
| Drevo       | 4      | 8       | 152   | 265   | 0.05   |
| AEGO        | 1      | 3       | 16    | 0     | 0.04   |
| XUM         | 1      | 1       | 16    | 0     | 0.04   |
| Kingchuxing | 5      | 5       | 15    | 0     | 0.04   |
| Maximus     | 2      | 2       | 13    | 0     | 0.04   |
| Varro       | 1      | 1       | 12    | 0     | 0.03   |
| addlink     | 2      | 2       | 12    | 0     | 0.03   |
| Silicon ... | 1      | 1       | 12    | 0     | 0.03   |
| Wicgtyp     | 1      | 1       | 12    | 0     | 0.03   |
| Dell        | 3      | 6       | 12    | 0     | 0.03   |
| Yeyian      | 2      | 2       | 11    | 0     | 0.03   |
| Goldendisk  | 1      | 1       | 10    | 0     | 0.03   |
| Microtech   | 1      | 1       | 9     | 0     | 0.03   |
| Getrich     | 1      | 1       | 8     | 0     | 0.02   |
| Kingspeed   | 1      | 1       | 8     | 0     | 0.02   |
| FASTDISK    | 6      | 6       | 7     | 0     | 0.02   |
| QNIX        | 1      | 1       | 6     | 0     | 0.02   |
| ShanDianZhe | 3      | 5       | 5     | 0     | 0.01   |
| Iod         | 1      | 1       | 5     | 0     | 0.01   |
| 2-Power     | 1      | 1       | 4     | 0     | 0.01   |
| PHINOCOM    | 1      | 1       | 4     | 0     | 0.01   |
| KODAK       | 1      | 1       | 4     | 0     | 0.01   |
| INDMEM      | 2      | 2       | 3     | 0     | 0.01   |
| Pacific Sun | 1      | 1       | 3     | 0     | 0.01   |
| ShineDisk   | 1      | 1       | 3     | 0     | 0.01   |
| Timetec     | 1      | 1       | 3     | 0     | 0.01   |
| i-FlashDisk | 1      | 1       | 3     | 0     | 0.01   |
| Smart       | 1      | 1       | 3     | 0     | 0.01   |
| Star Drive  | 1      | 1       | 3     | 0     | 0.01   |
| Pichau      | 1      | 1       | 3     | 0     | 0.01   |
| MaxDigital  | 2      | 2       | 23    | 333   | 0.01   |
| Gigastone   | 1      | 1       | 2     | 0     | 0.01   |
| SOLIDATA    | 1      | 1       | 2420  | 1019  | 0.01   |
| ACPI        | 1      | 1       | 2     | 0     | 0.01   |
| VSEVEN      | 1      | 1       | 2     | 0     | 0.01   |
| ASENNO      | 1      | 2       | 1     | 0     | 0.00   |
| Yunhaitian  | 1      | 1       | 1     | 0     | 0.00   |
| Mcpoint     | 1      | 1       | 6     | 3     | 0.00   |
| acpi        | 1      | 1       | 1     | 0     | 0.00   |
| S3+         | 1      | 1       | 1     | 0     | 0.00   |
| BR          | 1      | 1       | 1     | 0     | 0.00   |
| OEM         | 1      | 1       | 1     | 0     | 0.00   |
| ORTIAL      | 1      | 3       | 0     | 0     | 0.00   |
| Kross El... | 1      | 1       | 0     | 0     | 0.00   |
| Eluktro     | 1      | 1       | 806   | 1016  | 0.00   |
| HP Phison   | 1      | 1       | 717   | 1033  | 0.00   |
| UMAX        | 1      | 1       | 0     | 0     | 0.00   |
| Liren       | 1      | 1       | 0     | 0     | 0.00   |
| Gost        | 1      | 1       | 0     | 0     | 0.00   |
| DERLAR      | 1      | 1       | 0     | 0     | 0.00   |
| TEUTONS     | 1      | 1       | 0     | 0     | 0.00   |
| Bamba       | 1      | 1       | 60    | 249   | 0.00   |
| Myung       | 1      | 1       | 228   | 1015  | 0.00   |
| Goldenfir   | 2      | 2       | 2     | 14    | 0.00   |
| AXIOMTEK    | 2      | 2       | 0     | 0     | 0.00   |
| Dahua       | 1      | 1       | 0     | 0     | 0.00   |
| DOGGO       | 1      | 2       | 0     | 0     | 0.00   |
| JIAWEI      | 1      | 1       | 47    | 3057  | 0.00   |

NVME by Model
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

See complete list of tested NVMe samples in the Appendix 5 ([All_NVMe.md](/All_NVMe.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF   |
|-----------|--------------------|--------|---------|-------|-------|--------|
| Intel     | MEMPEK1J016GAD     | 16 GB  | 2       | 5999  | 0     | 16.44  |
| Intel     | SSDPEDMW800G4      | 800 GB | 1       | 1422  | 0     | 3.90   |
| Intel     | H10 HBRPEKNX020... | 32 GB  | 6       | 1148  | 0     | 3.15   |
| ZOTAC     | ZTSSDPG3-480G-GE   | 480 GB | 1       | 899   | 0     | 2.47   |
| Corsair   | Force MP500        | 480 GB | 1       | 869   | 0     | 2.38   |
| Samsung   | MZVPV512HDGL-00000 | 512 GB | 2       | 862   | 0     | 2.36   |
| Intel     | SSDPEDMW012T4      | 1.2 TB | 1       | 823   | 0     | 2.26   |
| Transcend | TS128GMTE850       | 128 GB | 1       | 745   | 0     | 2.04   |
| Samsung   | SSD 950 PRO        | 512 GB | 21      | 709   | 0     | 1.94   |
| Samsung   | SSD 950 PRO        | 256 GB | 7       | 701   | 0     | 1.92   |
| Toshiba   | THNSN5256GPU7      | 256 GB | 7       | 698   | 0     | 1.91   |
| Intel     | MEMPEK1W032GA      | 32 GB  | 3       | 674   | 0     | 1.85   |
| Intel     | SSDPEKKF256G7H     | 256 GB | 6       | 643   | 0     | 1.76   |
| Intel     | SSDPEKKW256G7      | 256 GB | 29      | 685   | 1     | 1.71   |
| Intel     | SSDPED1K375GA      | 375 GB | 1       | 603   | 0     | 1.65   |
| Intel     | SSDPEDMD400G4      | 400 GB | 1       | 595   | 0     | 1.63   |
| WDC       | WDS512G1X0C-00ENX0 | 512 GB | 7       | 574   | 0     | 1.57   |
| Intel     | SSDPEKKW512G7      | 512 GB | 13      | 663   | 78    | 1.56   |
| Toshiba   | THNSN5512GPUK      | 512 GB | 1       | 563   | 0     | 1.54   |
| Toshiba   | KXG50PNV2T04 1.6TB | 1.6 TB | 1       | 553   | 0     | 1.52   |
| Toshiba   | THNSN51T02DUK NVMe | 1 TB   | 6       | 551   | 0     | 1.51   |
| Intel     | SSDPEKKF360G7H     | 360 GB | 6       | 526   | 0     | 1.44   |
| Corsair   | Force MP500        | 120 GB | 5       | 525   | 0     | 1.44   |
| Intel     | SSDPE21D480GA      | 480 GB | 2       | 515   | 0     | 1.41   |
| Samsung   | MZVPV512HDGL-000H1 | 512 GB | 3       | 510   | 0     | 1.40   |
| Samsung   | MZVPV256HDGL-000H1 | 256 GB | 3       | 497   | 0     | 1.36   |
| ADATA     | SX7000NP           | 128 GB | 1       | 483   | 0     | 1.33   |
| Samsung   | MZVKW512HMJP-00000 | 512 GB | 3       | 483   | 0     | 1.33   |
| Samsung   | MZVPV256HDGL-00000 | 256 GB | 8       | 474   | 0     | 1.30   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 1       | 448   | 0     | 1.23   |
| Intel     | SSDPEKKW010T7      | 1 TB   | 2       | 445   | 0     | 1.22   |
| Micron    | MTFDHAL3T2MCE-1... | 3.2 TB | 1       | 424   | 0     | 1.16   |
| Samsung   | MS1PC2DD3ORA3.2T   | 3.2 TB | 1       | 416   | 0     | 1.14   |
| Samsung   | PM951 NVMe         | 512 GB | 4       | 401   | 0     | 1.10   |
| Toshiba   | THNSF5256GPUK      | 256 GB | 2       | 401   | 0     | 1.10   |
| Intel     | SSDPEKKF128G7      | 128 GB | 1       | 778   | 1     | 1.07   |
| SanDisk   | A400 NVMe          | 512 GB | 2       | 382   | 0     | 1.05   |
| Toshiba   | THNSN5512GPUK NVMe | 512 GB | 18      | 380   | 0     | 1.04   |
| Samsung   | MZVPV128HDGM-00000 | 128 GB | 6       | 379   | 0     | 1.04   |
| Toshiba   | KXG50ZNV1T02 NVMe  | 1 TB   | 10      | 377   | 0     | 1.04   |
| Plextor   | PX-512M8PeGN       | 512 GB | 1       | 362   | 0     | 0.99   |
| Samsung   | MZVLV512HCJH-000L2 | 512 GB | 1       | 361   | 0     | 0.99   |
| Samsung   | MZSLW1T0HMLH-000L1 | 1 TB   | 2       | 359   | 0     | 0.98   |
| Intel     | SSDPE2MX012T7      | 1.2 TB | 4       | 358   | 0     | 0.98   |
| HP        | SSD EX920          | 512 GB | 9       | 354   | 0     | 0.97   |
| Phison    | Asura NVME         | 2 TB   | 1       | 353   | 0     | 0.97   |
| WDC       | WDS256G1X0C-00ENX0 | 256 GB | 7       | 334   | 0     | 0.92   |
| Toshiba   | THNSN51T02DU7 NVMe | 1 TB   | 1       | 321   | 0     | 0.88   |
| Intel     | SSDPED1D280GA      | 280 GB | 3       | 311   | 0     | 0.85   |
| Samsung   | MZVPV128HDGM-000H1 | 128 GB | 1       | 304   | 0     | 0.83   |
| Intel     | SSDPEBKF128G7      | 128 GB | 1       | 291   | 0     | 0.80   |
| Toshiba   | THNSN5256GPUK NVMe | 256 GB | 5       | 286   | 0     | 0.78   |
| ADATA     | SX6000NP           | 128 GB | 4       | 342   | 41    | 0.78   |
| Intel     | SSDPEKKW128G7      | 128 GB | 3       | 402   | 1     | 0.77   |
| Toshiba   | KXG50ZNV512G NVMe  | 512 GB | 26      | 272   | 0     | 0.75   |
| Samsung   | MZVLV512HCJH-000H1 | 512 GB | 1       | 269   | 0     | 0.74   |
| ADATA     | SX8200NP           | 480 GB | 3       | 269   | 0     | 0.74   |
| Silico... | Asgard AN3 2TNV... | 2 TB   | 1       | 269   | 0     | 0.74   |
| XPG       | GAMMIX S11         | 480 GB | 6       | 264   | 0     | 0.73   |
| Samsung   | MZVLV256HCHP-000L2 | 256 GB | 5       | 263   | 0     | 0.72   |
| Kingston  | SKC2000M8500G      | 500 GB | 2       | 262   | 0     | 0.72   |
| Intel     | SSDPEKNW020T9      | 2 TB   | 1       | 260   | 0     | 0.71   |
| Samsung   | MZVLW512HMJP-000L2 | 512 GB | 9       | 253   | 0     | 0.70   |
| Intel     | SSDPEKKF256G7L     | 256 GB | 8       | 279   | 17    | 0.69   |
| Toshiba   | THNSF5256GPUK      | 256 GB | 1       | 249   | 0     | 0.68   |
| Toshiba   | KXG50PNV1T02 NVMe  | 1 TB   | 1       | 249   | 0     | 0.68   |
| Corsair   | Force MP500        | 240 GB | 6       | 417   | 2     | 0.68   |
| Toshiba   | THNSN51T02DUK      | 1 TB   | 2       | 246   | 0     | 0.68   |
| WDC       | WDS100T2X0C-00L350 | 1 TB   | 8       | 245   | 0     | 0.67   |
| Lite-On   | CL1-4D128          | 128 GB | 1       | 244   | 0     | 0.67   |
| Samsung   | MZVKV512HAJH-000L1 | 512 GB | 4       | 243   | 0     | 0.67   |
| Samsung   | PM951 NVMe         | 256 GB | 4       | 241   | 0     | 0.66   |
| ADATA     | SX8200NP           | 960 GB | 3       | 239   | 0     | 0.66   |
| Toshiba   | KXG50ZNV256G NVMe  | 256 GB | 22      | 239   | 0     | 0.66   |
| Toshiba   | KBG40ZPZ512G NVMe  | 512 GB | 2       | 236   | 0     | 0.65   |
| Intel     | SSDPEKKF512G8 NVMe | 512 GB | 4       | 228   | 0     | 0.63   |
| Lite-On   | T10 240            | 240 GB | 1       | 227   | 0     | 0.62   |
| Intel     | SSDPEKKF512G7H     | 512 GB | 2       | 224   | 0     | 0.62   |
| SK hynix  | PC300 NVMe         | 512 GB | 3       | 224   | 0     | 0.61   |
| SanDisk   | Extreme Pro        | 1 TB   | 2       | 222   | 0     | 0.61   |
| Intel     | SSDPED1D480GA      | 480 GB | 2       | 222   | 0     | 0.61   |
| Plextor   | PX-256M9PeG        | 256 GB | 3       | 221   | 0     | 0.61   |
| Team      | TM8FP2240G         | 240 GB | 1       | 219   | 0     | 0.60   |
| Toshiba   | THNSN5128GPU7      | 128 GB | 6       | 218   | 0     | 0.60   |
| Toshiba   | THNSF5512GPUK      | 512 GB | 4       | 214   | 0     | 0.59   |
| WDC       | WDS200T3XHC-00SJG0 | 2 TB   | 2       | 213   | 0     | 0.59   |
| Intel     | SSDPE2KX020T8      | 2 TB   | 3       | 212   | 0     | 0.58   |
| Samsung   | MZVLV256HCHP-00000 | 256 GB | 3       | 210   | 0     | 0.58   |
| Toshiba   | KXG5AZNV256G       | 256 GB | 6       | 209   | 0     | 0.57   |
| Intel     | H10 HBRPEKNX010... | 256 GB | 1       | 208   | 0     | 0.57   |
| Toshiba   | KXG5AZNV512G NV... | 512 GB | 1       | 207   | 0     | 0.57   |
| WDC       | WDS500G2X0C-00L350 | 500 GB | 16      | 204   | 0     | 0.56   |
| Intel     | SSDPE2MX450G7      | 450 GB | 2       | 204   | 0     | 0.56   |
| Transcend | TS128GMTE110S      | 128 GB | 4       | 200   | 0     | 0.55   |
| Corsair   | Force MP510        | 960 GB | 17      | 199   | 0     | 0.55   |
| Toshiba   | KXG50ZNV512G       | 512 GB | 18      | 199   | 0     | 0.55   |
| Samsung   | MZVLW128HEGR-000L1 | 128 GB | 4       | 198   | 0     | 0.54   |
| Toshiba   | KXG5AZNV512G       | 512 GB | 5       | 198   | 0     | 0.54   |
| Samsung   | MZVLW128HEGR-00000 | 128 GB | 2       | 198   | 0     | 0.54   |
| Toshiba   | RD400              | 512 GB | 1       | 193   | 0     | 0.53   |
| Phison    | BPX                | 480 GB | 2       | 193   | 0     | 0.53   |
| Intel     | SSDPEKKF010T8      | 1 TB   | 5       | 191   | 0     | 0.53   |
| Mushkin   | MKNSSDHL500GB-D8   | 500 GB | 1       | 189   | 0     | 0.52   |
| Toshiba   | KXG50ZNV1T02       | 1 TB   | 3       | 188   | 0     | 0.52   |
| Intel     | MEMPEK1J016GAL     | 16 GB  | 5       | 183   | 0     | 0.50   |
| Samsung   | MZVLW1T0HMLH-00000 | 1 TB   | 5       | 183   | 0     | 0.50   |
| Transcend | TS1TMTE220S        | 1 TB   | 6       | 181   | 0     | 0.50   |
| Toshiba   | THNSN5256GPUK      | 256 GB | 3       | 179   | 0     | 0.49   |
| Samsung   | MZFLV512HCJH-000MV | 512 GB | 2       | 178   | 0     | 0.49   |
| Transcend | TS256GMTE220S      | 256 GB | 4       | 177   | 0     | 0.49   |
| Gigabyte  | GP-ASM2NE6100TTTD  | 1 TB   | 4       | 175   | 0     | 0.48   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 1       | 175   | 0     | 0.48   |
| Team      | M8FP2              | 480 GB | 1       | 172   | 0     | 0.47   |
| Intel     | SSDPEKKW256G8      | 256 GB | 25      | 172   | 0     | 0.47   |
| Samsung   | SSD 960 PRO        | 1 TB   | 10      | 183   | 1     | 0.47   |
| Intel     | SSDPEKNW020T8      | 2 TB   | 36      | 171   | 0     | 0.47   |
| WDC       | WDS100T3XHC-00SJG0 | 1 TB   | 5       | 167   | 0     | 0.46   |
| Toshiba   | KXG50PNV2T04       | 2 TB   | 2       | 167   | 0     | 0.46   |
| addlink   | M.2 PCIE G3x4 NVMe | 2 TB   | 3       | 167   | 0     | 0.46   |
| Apacer    | AS2280P4           | 240 GB | 1       | 165   | 0     | 0.45   |
| Gigabyte  | GP-ASM2NE2256GTTDR | 256 GB | 1       | 165   | 0     | 0.45   |
| Apacer    | AS2280P4           | 480 GB | 1       | 163   | 0     | 0.45   |
| Mushkin   | MKNSSDPL500GB-D8   | 500 GB | 2       | 163   | 0     | 0.45   |
| Plextor   | PX-512M9PeG        | 512 GB | 1       | 159   | 0     | 0.44   |
| Phison    | E12-512G-PHISON... | 512 GB | 1       | 159   | 0     | 0.44   |
| Samsung   | SSD 960 PRO        | 2 TB   | 8       | 168   | 6     | 0.43   |
| Toshiba   | THNSN5256GPUK      | 256 GB | 2       | 157   | 0     | 0.43   |
| Lite-On   | CX2-8B512-Q11 NVMe | 512 GB | 2       | 156   | 0     | 0.43   |
| Samsung   | MZVLV256HCHP-000H1 | 256 GB | 7       | 156   | 0     | 0.43   |
| ADATA     | SX8200NP           | 240 GB | 5       | 184   | 24    | 0.43   |
| Toshiba   | THNSN5512GPUK      | 512 GB | 5       | 155   | 0     | 0.43   |
| Seagate   | BarraCuda 510 S... | 1 TB   | 2       | 154   | 0     | 0.42   |
| Lite-On   | CL1-3D128-Q11 NVMe | 128 GB | 2       | 154   | 0     | 0.42   |
| WDC       | WDS250G2X0C-00L350 | 250 GB | 7       | 152   | 0     | 0.42   |
| Intel     | MEMPEK1J016GA      | 16 GB  | 3       | 152   | 0     | 0.42   |
| Phison    | PP3-8D256          | 256 GB | 1       | 150   | 0     | 0.41   |
| Samsung   | SM951 NVMe         | 256 GB | 1       | 150   | 0     | 0.41   |
| Toshiba   | THNSN0256GTYA      | 256 GB | 1       | 149   | 0     | 0.41   |
| Kingston  | SKC1000240G        | 240 GB | 1       | 148   | 0     | 0.41   |
| Toshiba   | RC100              | 240 GB | 6       | 148   | 0     | 0.41   |
| Toshiba   | KXG60ZNV512G NVMe  | 512 GB | 29      | 147   | 0     | 0.40   |
| Samsung   | MZVLW1T0HMLH-000L2 | 1 TB   | 3       | 147   | 0     | 0.40   |
| Samsung   | MZVPW256HEGL-00000 | 256 GB | 10      | 146   | 0     | 0.40   |
| Intel     | SSDPEL1D380GA      | 384 GB | 1       | 146   | 0     | 0.40   |
| Lenovo    | LENSE20256GMSP3... | 256 GB | 9       | 142   | 0     | 0.39   |
| SanDisk   | Extreme Pro        | 500 GB | 5       | 142   | 0     | 0.39   |
| Patriot   | Scorch M2          | 128 GB | 3       | 141   | 0     | 0.39   |
| Corsair   | Force MP510 1.9TB  | 1.9 TB | 2       | 139   | 0     | 0.38   |
| SK hynix  | PC601 NVMe         | 1 TB   | 8       | 138   | 0     | 0.38   |
| Phison    | M.2 PCIE G3x4 NVMe | 1 TB   | 2       | 137   | 0     | 0.38   |
| Samsung   | SSD 960 PRO        | 512 GB | 40      | 155   | 4     | 0.38   |
| Samsung   | PM981 NVMe         | 1 TB   | 4       | 136   | 0     | 0.38   |
| Gigabyte  | GP-GSM2NE3128GNTD  | 128 GB | 1       | 136   | 0     | 0.37   |
| Toshiba   | KXG60ZNV1T02 NVMe  | 1 TB   | 6       | 135   | 0     | 0.37   |
| Lite-On   | CA3-8D512          | 512 GB | 6       | 135   | 0     | 0.37   |
| Kingston  | SKC2000M8250G      | 250 GB | 2       | 135   | 0     | 0.37   |
| Toshiba   | THNSN5256GPU7 NVMe | 256 GB | 3       | 133   | 0     | 0.37   |
| WDC       | WDS250G1B0C-00S6U0 | 250 GB | 7       | 133   | 0     | 0.37   |
| Kingston  | SKC1000480G        | 480 GB | 2       | 131   | 0     | 0.36   |
| Intel     | SSDPEKKF512G7      | 512 GB | 1       | 130   | 0     | 0.36   |
| Plextor   | PX-1TM8PeY         | 1 TB   | 2       | 129   | 0     | 0.35   |
| Lenovo    | LENSE20512GMSP3... | 512 GB | 7       | 129   | 0     | 0.35   |
| Samsung   | SSD 960 EVO        | 1 TB   | 34      | 129   | 1     | 0.35   |
| SK hynix  | PC401 NVMe         | 256 GB | 7       | 128   | 0     | 0.35   |
| Samsung   | PM951 NVMe         | 1 TB   | 1       | 128   | 0     | 0.35   |
| Toshiba   | KXG60ZNV256G NVMe  | 256 GB | 17      | 125   | 0     | 0.34   |
| Phison    | APS-SE20G-2T       | 2 TB   | 1       | 122   | 0     | 0.34   |
| Crucial   | CT500P1SSD8        | 500 GB | 52      | 136   | 12    | 0.34   |
| Phison    | BPXP               | 960 GB | 2       | 122   | 0     | 0.33   |
| Mushkin   | MKNSSDPL1TB-D8     | 1 TB   | 1       | 121   | 0     | 0.33   |
| Intel     | SSDPEKKW128G8      | 128 GB | 12      | 121   | 0     | 0.33   |
| WDC       | WDBGMP0020BNC-WRSN | 2 TB   | 1       | 121   | 0     | 0.33   |
| HP        | SSD EX900          | 250 GB | 6       | 120   | 0     | 0.33   |
| PNY       | CS3030 1000GB SSD  | 1 TB   | 1       | 120   | 0     | 0.33   |
| Intel     | SSDPEKKF010T8 NVMe | 1 TB   | 5       | 119   | 0     | 0.33   |
| Samsung   | SSD 960 EVO        | 500 GB | 68      | 132   | 18    | 0.33   |
| Toshiba   | RC500              | 500 GB | 3       | 119   | 0     | 0.33   |
| Samsung   | KUS040202M-B000    | 512 GB | 1       | 118   | 0     | 0.32   |
| Corsair   | Force MP600        | 1 TB   | 28      | 117   | 0     | 0.32   |
| Lexar     | 1TB SSD            | 1 TB   | 1       | 117   | 0     | 0.32   |
| Crucial   | CT1000P1SSD8       | 1 TB   | 83      | 133   | 12    | 0.32   |
| Corsair   | Force MP510        | 240 GB | 16      | 117   | 0     | 0.32   |
| Intel     | HBRPEKNX0203AHO    | 32 GB  | 7       | 117   | 0     | 0.32   |
| Kingston  | SA1000M8480G       | 480 GB | 7       | 117   | 0     | 0.32   |
| Phison    | Sabrent            | 1 TB   | 53      | 117   | 0     | 0.32   |
| Plextor   | PX-512M8PeG        | 512 GB | 4       | 145   | 138   | 0.32   |
| WDC       | WDBRPG5000ANC-WRSN | 500 GB | 2       | 116   | 0     | 0.32   |
| Hikvision | HS-SSD-C2000       | 1 TB   | 1       | 116   | 0     | 0.32   |
| Samsung   | MZVLW256HEHP-000L2 | 256 GB | 21      | 115   | 0     | 0.32   |
| Silico... | M Series NVMe S... | 256 GB | 3       | 115   | 0     | 0.32   |
| Toshiba   | THNSN5128GPUK      | 128 GB | 1       | 114   | 0     | 0.31   |
| SK hynix  | SKHynix_HFS001T... | 1 TB   | 2       | 113   | 0     | 0.31   |
| Samsung   | SM961 NVMe         | 512 GB | 1       | 112   | 0     | 0.31   |
| Intel     | SSDPEKNW512G8      | 512 GB | 106     | 111   | 0     | 0.31   |
| SK hynix  | PC601A NVMe        | 1 TB   | 1       | 111   | 0     | 0.30   |
| Huawei    | HWE52P432T0L005N   | 2 TB   | 6       | 110   | 0     | 0.30   |
| Phison    | PCIe SSD           | 1 TB   | 30      | 109   | 0     | 0.30   |
| Seagate   | FireCuda 520 SS... | 1 TB   | 8       | 109   | 0     | 0.30   |
| Phison    | Viper M.2 VPN100   | 1 TB   | 8       | 109   | 0     | 0.30   |
| HP        | SSD EX920          | 256 GB | 1       | 325   | 2     | 0.30   |
| SK hynix  | HFS256GD9MNE-6200A | 256 GB | 1       | 107   | 0     | 0.29   |
| Seagate   | BarraCuda 510 S... | 500 GB | 1       | 106   | 0     | 0.29   |
| Plextor   | PX-256M9PeY        | 256 GB | 1       | 106   | 0     | 0.29   |
| Plextor   | PX-128M8PeGN       | 128 GB | 1       | 106   | 0     | 0.29   |
| Samsung   | MZVKW512HMJP-000H1 | 512 GB | 4       | 105   | 0     | 0.29   |
| PNY       | CS3030 2TB SSD     | 2 TB   | 2       | 103   | 0     | 0.28   |
| Samsung   | KUS030202M-B000    | 256 GB | 4       | 101   | 0     | 0.28   |
| Intel     | SSDPEKNW010T8      | 1 TB   | 100     | 101   | 0     | 0.28   |
| Toshiba   | RD400              | 1 TB   | 1       | 101   | 0     | 0.28   |
| Corsair   | Force MP600        | 2 TB   | 4       | 100   | 0     | 0.28   |
| Toshiba   | KBG40ZNS512G NVMe  | 512 GB | 7       | 100   | 0     | 0.27   |
| Apacer    | Z280 120G          | 120 GB | 2       | 99    | 0     | 0.27   |
| Toshiba   | THNSN5512GPU7 NVMe | 512 GB | 2       | 99    | 0     | 0.27   |
| Samsung   | SSD 970 PRO        | 512 GB | 97      | 99    | 1     | 0.27   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 13      | 98    | 0     | 0.27   |
| WDC       | WDS500G1B0C-00S6U0 | 500 GB | 5       | 98    | 0     | 0.27   |
| Intel     | SSDPEKKF256G8 NVMe | 256 GB | 5       | 98    | 0     | 0.27   |
| Zheino    | CHN-NGFFNV2280-1TB | 1 TB   | 2       | 98    | 0     | 0.27   |
| Samsung   | MZVLW512HMJP-00000 | 512 GB | 10      | 101   | 1     | 0.27   |
| Goodram   | SSDPR-PX400-256-80 | 256 GB | 1       | 97    | 0     | 0.27   |
| Plextor   | PX-1TM8SeG         | 1 TB   | 2       | 380   | 54    | 0.27   |
| Samsung   | MZVLW512HMJP-000H7 | 512 GB | 1       | 97    | 0     | 0.27   |
| Toshiba   | KXG60PNV2T04 NV... | 2 TB   | 5       | 97    | 0     | 0.27   |
| Samsung   | MZVLB2T0HMLB-000L2 | 2 TB   | 1       | 96    | 0     | 0.27   |
| Samsung   | SSD 970 EVO        | 250 GB | 75      | 101   | 3     | 0.26   |
| Toshiba   | KXG50ZNV256G       | 256 GB | 10      | 96    | 0     | 0.26   |
| Patriot   | Hellfire M2        | 480 GB | 1       | 96    | 0     | 0.26   |
| Smartbuy  | m.2 PS5012-2280    | 256 GB | 1       | 95    | 0     | 0.26   |
| Intel     | MEMPEK1W016GA      | 16 GB  | 4       | 95    | 0     | 0.26   |
| SK hynix  | PC601 NVMe         | 512 GB | 29      | 95    | 0     | 0.26   |
| SK hynix  | BC501 HFM128GDJ... | 128 GB | 3       | 95    | 0     | 0.26   |
| Silico... | NE-512             | 512 GB | 6       | 95    | 0     | 0.26   |
| Samsung   | PM961 NVMe         | 512 GB | 7       | 98    | 1     | 0.26   |
| Intel     | HBRPEKNX0203AH     | 1 TB   | 7       | 94    | 0     | 0.26   |
| Intel     | SSDPEKNW010T8H     | 1 TB   | 7       | 93    | 0     | 0.26   |
| Phison    | APS-SE20G-512      | 512 GB | 1       | 93    | 0     | 0.26   |
| Intel     | SSDPEK1W060GA      | 64 GB  | 1       | 93    | 0     | 0.26   |
| Phison    | SBXe               | 960 GB | 2       | 92    | 0     | 0.25   |
| Micron    | 2200 NVMe          | 512 GB | 2       | 91    | 0     | 0.25   |
| Intel     | SSDPEKKW010T8L     | 1 TB   | 1       | 91    | 0     | 0.25   |
| Samsung   | SSD 960 EVO        | 250 GB | 113     | 98    | 20    | 0.25   |
| Corsair   | Force MP300        | 120 GB | 2       | 90    | 0     | 0.25   |
| Union ... | UMIS RPJTJ256ME... | 256 GB | 3       | 90    | 0     | 0.25   |
| Silico... | R5MP480G8          | 480 GB | 2       | 90    | 0     | 0.25   |
| XPG       | GAMMIX S11 Pro     | 1 TB   | 36      | 89    | 0     | 0.25   |
| ADATA     | SX8200PNP          | 1 TB   | 44      | 88    | 0     | 0.24   |
| Toshiba   | THNSF5256GPU7      | 256 GB | 1       | 88    | 0     | 0.24   |
| Intel     | H10 HBRPEKNX020... | 512 GB | 11      | 86    | 0     | 0.24   |
| Intel     | SSDPEDMW400G4      | 400 GB | 1       | 86    | 0     | 0.24   |
| ADATA     | SX8200PNP          | 512 GB | 39      | 85    | 0     | 0.24   |
| Toshiba   | THNSN5256GPU7      | 256 GB | 1       | 85    | 0     | 0.23   |
| Toshiba   | KBG40ZNS256G NVMe  | 256 GB | 9       | 85    | 0     | 0.23   |
| Team      | TM8FP4256G         | 256 GB | 2       | 84    | 0     | 0.23   |
| Toshiba   | KBG30ZMV256G       | 256 GB | 19      | 84    | 0     | 0.23   |
| Silico... | S2000              | 1 TB   | 2       | 84    | 0     | 0.23   |
| Samsung   | MZVLB1T0HALR-000L7 | 1 TB   | 25      | 84    | 0     | 0.23   |
| Silico... | R5MP120G8          | 120 GB | 3       | 83    | 0     | 0.23   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 1       | 83    | 0     | 0.23   |
| Samsung   | MZFLV128HCGR-000MV | 128 GB | 4       | 81    | 0     | 0.22   |
| Silico... | NVME SSD           | 1 TB   | 2       | 81    | 0     | 0.22   |
| Samsung   | MZVLV128HCGR-00000 | 128 GB | 1       | 81    | 0     | 0.22   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 1       | 81    | 0     | 0.22   |
| Silico... | 1TB PCS PCIe M.... | 1 TB   | 1       | 81    | 0     | 0.22   |
| Intel     | HBRPEKNX0202AHO    | 32 GB  | 13      | 80    | 0     | 0.22   |
| Samsung   | MZVPV256HDGL-000L2 | 256 GB | 1       | 80    | 0     | 0.22   |
| WDC       | PC SN520 SDAPMU... | 256 GB | 2       | 80    | 0     | 0.22   |
| SPCC      | M.2 PCIE SSD       | 256 GB | 3       | 79    | 0     | 0.22   |
| Toshiba   | KBG30ZMT128G       | 128 GB | 13      | 78    | 0     | 0.22   |
| Intel     | SSDPEKKW512G8      | 512 GB | 11      | 78    | 0     | 0.21   |
| ADATA     | SX8200PNP          | 256 GB | 22      | 85    | 46    | 0.21   |
| Union ... | UMIS RPJTJ128ME... | 128 GB | 2       | 76    | 0     | 0.21   |
| Corsair   | Force MP300        | 960 GB | 1       | 76    | 0     | 0.21   |
| Lite-On   | CB1-SD512          | 512 GB | 1       | 75    | 0     | 0.21   |
| SPCC      | M.2 PCIe SSD       | 512 GB | 9       | 75    | 0     | 0.21   |
| HP        | SSD EX900          | 500 GB | 6       | 139   | 14    | 0.20   |
| Toshiba   | KXG60ZNV256G NV... | 256 GB | 1       | 74    | 0     | 0.20   |
| Corsair   | Force MP510        | 480 GB | 16      | 74    | 0     | 0.20   |
| Plextor   | PX-256M8PeY        | 256 GB | 2       | 73    | 0     | 0.20   |
| KIOXIA    | KBG40ZPZ512G NVMe  | 512 GB | 7       | 73    | 0     | 0.20   |
| Silico... | AITC M.2 FZ300     | 128 GB | 1       | 73    | 0     | 0.20   |
| Toshiba   | KXG50PNV2T04 NVMe  | 2 TB   | 1       | 72    | 0     | 0.20   |
| WDC       | WDS250G3X0C-00SJG0 | 250 GB | 10      | 72    | 0     | 0.20   |
| Phison    | Sabrent Rocket 4.0 | 1 TB   | 39      | 71    | 0     | 0.20   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 2       | 71    | 0     | 0.20   |
| Samsung   | MZVLW128HEGR-000L2 | 128 GB | 10      | 87    | 1     | 0.20   |
| Transcend | TS512GMTE220S      | 512 GB | 1       | 70    | 0     | 0.19   |
| HP        | SSD EX900          | 1 TB   | 3       | 70    | 0     | 0.19   |
| SPCC      | M.2 PCIe SSD       | 1 TB   | 9       | 70    | 0     | 0.19   |
| Team      | TM8FP4001T         | 1 TB   | 3       | 70    | 0     | 0.19   |
| Micron    | MTFDHBA512TCK      | 512 GB | 2       | 69    | 0     | 0.19   |
| Hikvision | HS-SSD-E2000       | 256 GB | 1       | 69    | 0     | 0.19   |
| Samsung   | MZVLW256HEHP-00000 | 256 GB | 31      | 69    | 0     | 0.19   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 1       | 69    | 0     | 0.19   |
| Seagate   | FireCuda 520 SS... | 500 GB | 5       | 68    | 0     | 0.19   |
| Intel     | HBRPEKNX0202AH     | 512 GB | 15      | 68    | 0     | 0.19   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 2       | 68    | 0     | 0.19   |
| Plextor   | PX-512M9PeY        | 512 GB | 4       | 68    | 0     | 0.19   |
| Phison    | Sabrent Rocket 4.0 | 500 GB | 3       | 68    | 0     | 0.19   |
| Samsung   | MZVKW1T0HMLH-000L7 | 1 TB   | 1       | 67    | 0     | 0.19   |
| Toshiba   | KBG30ZMS256G NVMe  | 256 GB | 17      | 67    | 0     | 0.19   |
| Samsung   | PM961 NVMe         | 1 TB   | 1       | 67    | 0     | 0.18   |
| Samsung   | MZVKW512HMJP-000L7 | 512 GB | 5       | 67    | 0     | 0.18   |
| WDC       | PC SN520 NVMe      | 128 GB | 7       | 67    | 0     | 0.18   |
| Samsung   | MZVLW1T0HMLH-000L7 | 1 TB   | 5       | 78    | 4     | 0.18   |
| SK hynix  | PC401 HFS256GD9... | 256 GB | 8       | 66    | 0     | 0.18   |
| FORESEE   | P900F128GBH        | 128 GB | 1       | 66    | 0     | 0.18   |
| Intel     | SSDPEKNU512G8L     | 512 GB | 2       | 66    | 0     | 0.18   |
| Toshiba   | KXG6AZNV256G       | 256 GB | 7       | 66    | 0     | 0.18   |
| Plextor   | PX-256M9PeGN       | 256 GB | 3       | 65    | 0     | 0.18   |
| PNY       | CS3030 250GB SSD   | 250 GB | 5       | 65    | 0     | 0.18   |
| Samsung   | PM961 NVMe SED     | 512 GB | 1       | 64    | 0     | 0.18   |
| Samsung   | KUS020203M-B000    | 128 GB | 1       | 64    | 0     | 0.18   |
| Toshiba   | KBG30ZMS128G NVMe  | 128 GB | 4       | 64    | 0     | 0.18   |
| Toshiba   | KXG60ZNV1T02 NV... | 1 TB   | 15      | 63    | 0     | 0.17   |
| Samsung   | MZVLW128HEGR-000H1 | 128 GB | 8       | 63    | 0     | 0.17   |
| Patriot   | Scorch M2          | 256 GB | 4       | 63    | 0     | 0.17   |
| Intel     | HBRPEKNX0101AHO    | 16 GB  | 5       | 63    | 0     | 0.17   |
| WDC       | WDS500G3X0C-00SJG0 | 500 GB | 50      | 67    | 21    | 0.17   |
| Kingston  | SA2000M81000G      | 1 TB   | 42      | 64    | 25    | 0.17   |
| Kingston  | RBUSNS8154P3512GJ1 | 512 GB | 3       | 61    | 0     | 0.17   |
| Phison    | Sabrent Rocket 4.0 | 2 TB   | 4       | 60    | 0     | 0.17   |
| Intel     | HBRPEKNX0101AO     | 16 GB  | 1       | 60    | 0     | 0.17   |
| SK hynix  | PC601 NVMe         | 256 GB | 4       | 60    | 0     | 0.17   |
| WDC       | WDS500G3XHC-00SJG0 | 500 GB | 3       | 60    | 0     | 0.17   |
| Phison    | Sabrent Rocket Q   | 1 TB   | 20      | 60    | 0     | 0.16   |
| Kingch... | 256GB              | 256 GB | 1       | 60    | 0     | 0.16   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 22      | 59    | 0     | 0.16   |
| Samsung   | PM981 NVMe         | 512 GB | 22      | 64    | 1     | 0.16   |
| ADATA     | SX8200PNP          | 2 TB   | 16      | 59    | 0     | 0.16   |
| ADATA     | SX8100NP           | 1 TB   | 1       | 59    | 0     | 0.16   |
| Intel     | SSDPEKKW256G8L     | 256 GB | 2       | 58    | 0     | 0.16   |
| Toshiba   | KXG60ZNV1T02       | 1 TB   | 2       | 58    | 0     | 0.16   |
| KIOXIA... | PLUS SSD           | 1 TB   | 3       | 58    | 0     | 0.16   |
| Crucial   | CT250P2SSD8        | 250 GB | 1       | 58    | 0     | 0.16   |
| Hikvision | HS-SSD-C2000Pro    | 1 TB   | 1       | 58    | 0     | 0.16   |
| HP        | SSD EX950          | 2 TB   | 4       | 58    | 0     | 0.16   |
| Phison    | SBX                | 256 GB | 1       | 58    | 0     | 0.16   |
| Lite-On   | CL1-4D256          | 256 GB | 4       | 58    | 0     | 0.16   |
| Samsung   | MZFLV256HCHP-000MV | 256 GB | 2       | 58    | 0     | 0.16   |
| PNY       | CS3030 500GB SSD   | 500 GB | 9       | 57    | 0     | 0.16   |
| Kingston  | RBUSNS8154P3256GJ  | 256 GB | 7       | 57    | 0     | 0.16   |
| Gigabyte  | GP-GSM2NE8256GNTD  | 256 GB | 1       | 57    | 0     | 0.16   |
| WDC       | PC SN520 NVMe      | 256 GB | 10      | 57    | 0     | 0.16   |
| Toshiba   | KXG60ZNV512G       | 512 GB | 11      | 57    | 0     | 0.16   |
| Samsung   | MZVLW512HMJP-000L7 | 512 GB | 6       | 58    | 1     | 0.16   |
| ADATA     | SX8100NP           | 256 GB | 2       | 56    | 0     | 0.16   |
| Apple     | SSD AP8192N        | 8 TB   | 1       | 56    | 0     | 0.15   |
| Samsung   | SSD 970 EVO        | 500 GB | 169     | 58    | 13    | 0.15   |
| WDC       | PC SN520 SDAPMU... | 512 GB | 23      | 56    | 0     | 0.15   |
| Toshiba   | KBG40ZPZ256G ME... | 256 GB | 1       | 55    | 0     | 0.15   |
| Seagate   | BarraCuda 510 S... | 256 GB | 1       | 55    | 0     | 0.15   |
| WDC       | PC SN720 SED SD... | 1 TB   | 2       | 55    | 0     | 0.15   |
| SK hynix  | HFM128GDHTNG-8310A | 128 GB | 6       | 55    | 0     | 0.15   |
| XPG       | GAMMIX S50         | 1 TB   | 2       | 55    | 0     | 0.15   |
| Intel     | HBRPEKNX0202ALO    | 32 GB  | 3       | 55    | 0     | 0.15   |
| Intel     | HBRPEKNX0101AH     | 256 GB | 5       | 55    | 0     | 0.15   |
| Intel     | HBRPEKNX0101A      | 256 GB | 1       | 55    | 0     | 0.15   |
| Silico... | NE-256             | 256 GB | 11      | 55    | 0     | 0.15   |
| Samsung   | MZVLW512HMJP-000H1 | 512 GB | 13      | 54    | 0     | 0.15   |
| Samsung   | MZVLW256HEHP-000L7 | 256 GB | 32      | 55    | 1     | 0.15   |
| Intel     | SSDPE2KX040T8      | 4 TB   | 4       | 53    | 0     | 0.15   |
| Kingston  | RBUSNS8154P3102... | 1 TB   | 1       | 53    | 0     | 0.15   |
| Gigabyte  | GP-GSM2NE3256GNTD  | 256 GB | 5       | 53    | 0     | 0.15   |
| Toshiba   | KXG6AZNV512G       | 512 GB | 12      | 52    | 0     | 0.15   |
| Seagate   | FireCuda 510 SS... | 1 TB   | 7       | 52    | 0     | 0.14   |
| WDC       | PC SN720 SDAQNT... | 512 GB | 27      | 52    | 0     | 0.14   |
| ADATA     | SX8100NP           | 512 GB | 4       | 52    | 0     | 0.14   |
| Intel     | SSDPEKKF256G8L     | 256 GB | 31      | 52    | 0     | 0.14   |
| WDC       | PC SN720 SDAQNT... | 256 GB | 7       | 52    | 0     | 0.14   |
| Apple     | SSD SM2048L        | 2 TB   | 1       | 52    | 0     | 0.14   |
| KIOXIA    | KBG40ZNS256G NVMe  | 256 GB | 20      | 51    | 0     | 0.14   |
| Plextor   | PX-256M8PeG        | 256 GB | 1       | 51    | 0     | 0.14   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 8       | 51    | 0     | 0.14   |
| SK hynix  | PC300 NVMe         | 1 TB   | 3       | 50    | 0     | 0.14   |
| Lenovo    | LENSE30512GMSP3... | 512 GB | 7       | 50    | 0     | 0.14   |
| SK hynix  | PC401 NVMe         | 512 GB | 29      | 54    | 1     | 0.14   |
| HP        | SSD EX920          | 1 TB   | 5       | 50    | 0     | 0.14   |
| Kingston  | OM8PDP3256B-A01    | 256 GB | 1       | 49    | 0     | 0.14   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 5       | 49    | 0     | 0.14   |
| Samsung   | MZVLB512HAJQ-000L7 | 512 GB | 62      | 48    | 1     | 0.13   |
| Corsair   | Force MP300        | 240 GB | 1       | 48    | 0     | 0.13   |
| Samsung   | MZVLB1T0HALR-00000 | 1 TB   | 20      | 48    | 1     | 0.13   |
| Samsung   | SSD 970 EVO        | 1 TB   | 156     | 48    | 1     | 0.13   |
| Lenovo    | LENSN20256GMSP3... | 256 GB | 1       | 47    | 0     | 0.13   |
| Solid ... | CL1-3D512-Q11 N... | 512 GB | 2       | 47    | 0     | 0.13   |
| ADATA     | SX6000PNP          | 512 GB | 3       | 47    | 0     | 0.13   |
| Intel     | HBRPEKNX0202AL     | 512 GB | 4       | 47    | 0     | 0.13   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 6       | 47    | 0     | 0.13   |
| SPCC      | M.2 PCIE SSD       | 1 TB   | 3       | 47    | 0     | 0.13   |
| Intel     | HBRPEKNX0202AO     | 32 GB  | 5       | 47    | 0     | 0.13   |
| Intel     | SSDPE2KE020T7      | 2 TB   | 4       | 46    | 0     | 0.13   |
| Samsung   | PM981 NVMe         | 2 TB   | 1       | 46    | 0     | 0.13   |
| Samsung   | MZVLB512HAJQ-000L2 | 512 GB | 15      | 47    | 1     | 0.13   |
| Intel     | HBRPEKNX0202A      | 512 GB | 5       | 45    | 0     | 0.13   |
| Hikvision | HS-SSD-E2000       | 512 GB | 1       | 45    | 0     | 0.12   |
| Micron    | 2200S NVMe         | 512 GB | 19      | 45    | 0     | 0.12   |
| Silico... | FPI1TBMWR7         | 1 TB   | 1       | 45    | 0     | 0.12   |
| WDC       | WDS100T3X0C-00SJG0 | 1 TB   | 37      | 45    | 0     | 0.12   |
| Samsung   | MZVLW256HEHP-000H1 | 256 GB | 26      | 57    | 1     | 0.12   |
| Samsung   | MZFLW256HEHP-000MV | 256 GB | 1       | 44    | 0     | 0.12   |
| Silico... | Asgard AN2 250N... | 250 GB | 1       | 44    | 0     | 0.12   |
| SPCC      | M.2 PCIe SSD       | 256 GB | 13      | 43    | 0     | 0.12   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 1       | 43    | 0     | 0.12   |
| Apacer    | AS2280P4           | 512 GB | 1       | 43    | 0     | 0.12   |
| Kingston  | SA2000M8250G       | 250 GB | 39      | 43    | 0     | 0.12   |
| Samsung   | PM961 NVMe         | 256 GB | 8       | 43    | 0     | 0.12   |
| Intel     | SSDPEKKF512G8L     | 512 GB | 24      | 42    | 0     | 0.12   |
| Samsung   | MZVLB512HAJQ-00000 | 512 GB | 49      | 43    | 1     | 0.12   |
| Intel     | SSDPEKKW010T8      | 1 TB   | 4       | 42    | 0     | 0.12   |
| Patriot   | Scorch M2          | 512 GB | 2       | 42    | 0     | 0.12   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 13      | 42    | 0     | 0.12   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 10      | 42    | 0     | 0.12   |
| Intel     | SSDPEKNW512G8H     | 512 GB | 80      | 42    | 1     | 0.12   |
| Samsung   | MZVLB2T0HALB-000L7 | 2 TB   | 8       | 42    | 0     | 0.12   |
| Lite-On   | CA3-8D256          | 256 GB | 3       | 42    | 0     | 0.12   |
| Intel     | SSDPEMKF512G8 NVMe | 512 GB | 12      | 42    | 0     | 0.12   |
| Apple     | SSD AP0032H        | 24 GB  | 1       | 42    | 0     | 0.12   |
| Corsair   | Force MP600        | 500 GB | 4       | 41    | 0     | 0.11   |
| ADATA     | SX8200PNP-512GT-S  | 512 GB | 1       | 41    | 0     | 0.11   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 5       | 40    | 0     | 0.11   |
| Kingston  | RBUSNS8154P3128GJ  | 128 GB | 11      | 40    | 0     | 0.11   |
| WDC       | WDS250G2B0C-00PXH0 | 250 GB | 13      | 40    | 0     | 0.11   |
| Toshiba   | KXG60ZNV512G KI... | 512 GB | 11      | 40    | 0     | 0.11   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 22      | 40    | 0     | 0.11   |
| Samsung   | SSD 970 PRO        | 1 TB   | 43      | 49    | 1     | 0.11   |
| Kingston  | SA2000M8500G       | 500 GB | 41      | 40    | 0     | 0.11   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 7       | 39    | 0     | 0.11   |
| SK hynix  | PC611 NVMe         | 256 GB | 2       | 39    | 0     | 0.11   |
| WDC       | WDS100T2B0C-00PXH0 | 1 TB   | 55      | 39    | 0     | 0.11   |
| Kingston  | SA1000M8240G       | 240 GB | 15      | 39    | 0     | 0.11   |
| Samsung   | PM981a NVMe        | 1 TB   | 13      | 39    | 0     | 0.11   |
| Gigabyte  | GP-AG42TB          | 2 TB   | 3       | 38    | 0     | 0.11   |
| Samsung   | MZFLW1T0HMLH-000MU | 1 TB   | 1       | 38    | 0     | 0.11   |
| Samsung   | PM981 NVMe         | 256 GB | 13      | 38    | 0     | 0.11   |
| Micron    | 2200S NVMe         | 256 GB | 5       | 38    | 0     | 0.10   |
| Samsung   | MZVLB256HAHQ-00000 | 256 GB | 27      | 38    | 0     | 0.10   |
| SPCC      | M.2 PCIE SSD       | 2 TB   | 1       | 38    | 0     | 0.10   |
| WDC       | WDS500G2B0C-00PXH0 | 500 GB | 41      | 37    | 0     | 0.10   |
| Gigabyte  | GP-ASM2NE6500GTTD  | 500 GB | 3       | 37    | 0     | 0.10   |
| Samsung   | MZVLB1T0HALR-000L2 | 1 TB   | 10      | 37    | 0     | 0.10   |
| Silico... | NVME SSD           | 256 GB | 1       | 37    | 0     | 0.10   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 9       | 36    | 0     | 0.10   |
| Toshiba   | KXG50PNV2T04 NV... | 2 TB   | 2       | 36    | 0     | 0.10   |
| Samsung   | MZVLB512HAJQ-000H1 | 512 GB | 47      | 36    | 0     | 0.10   |
| SK hynix  | HFB1M8MO331C0MR    | 256 GB | 1       | 35    | 0     | 0.10   |
| WDC       | PC SN520 SDAPMU... | 512 GB | 2       | 35    | 0     | 0.10   |
| Silico... | NE-128             | 128 GB | 6       | 35    | 0     | 0.10   |
| Toshiba   | KBG30ZMV512G       | 512 GB | 9       | 34    | 0     | 0.10   |
| Silico... | KLLISRE            | 128 GB | 1       | 34    | 0     | 0.10   |
| Kingston  | RBUSNS8154P3256GJ3 | 256 GB | 9       | 34    | 0     | 0.10   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 3       | 34    | 0     | 0.10   |
| Samsung   | MZVLB256HAHQ-000L7 | 256 GB | 27      | 34    | 0     | 0.10   |
| SanDisk   | Ultra 3D NVMe      | 1 TB   | 6       | 34    | 0     | 0.10   |
| Samsung   | MZVPW256HEGL-000H1 | 256 GB | 2       | 34    | 0     | 0.09   |
| Silico... | NVME SSD           | 512 GB | 1       | 34    | 0     | 0.09   |
| PNY       | CS3030 1TB SSD     | 1 TB   | 7       | 33    | 0     | 0.09   |
| Phison    | Sabrent ROCKET-PRO | 512 GB | 1       | 33    | 0     | 0.09   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 33      | 33    | 32    | 0.09   |
| Samsung   | SSD 970 EVO Plus   | 500 GB | 227     | 33    | 0     | 0.09   |
| SK hynix  | HFS256GD9TNG-62A0A | 256 GB | 10      | 33    | 0     | 0.09   |
| Intel     | SSDPEMKF010T8 NVMe | 1 TB   | 11      | 37    | 92    | 0.09   |
| KIOXIA    | KBG40ZNS512G NVMe  | 512 GB | 27      | 32    | 0     | 0.09   |
| WDC       | PC SN720 SDAQNT... | 512 GB | 2       | 32    | 0     | 0.09   |
| Apple     | SSD AP2048M        | 2 TB   | 2       | 32    | 0     | 0.09   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 5       | 32    | 0     | 0.09   |
| Gigabyte  | GP-GSM2NE3100TNTD  | 1 TB   | 7       | 31    | 0     | 0.09   |
| SK hynix  | PC401 NVMe         | 1 TB   | 5       | 31    | 0     | 0.09   |
| SK hynix  | SHGP31-500GM-2     | 500 GB | 1       | 31    | 0     | 0.09   |
| Toshiba   | KBG30ZMT256G       | 256 GB | 5       | 31    | 0     | 0.09   |
| Huawei    | HWE52P433T2M005N   | 3.2 TB | 4       | 31    | 0     | 0.09   |
| Intel     | SSDPEKNW512G8L     | 512 GB | 14      | 31    | 0     | 0.09   |
| ADATA     | SX6000NP           | 256 GB | 1       | 31    | 0     | 0.09   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 1       | 30    | 0     | 0.08   |
| WDC       | CL SN520 SDAPMU... | 512 GB | 1       | 30    | 0     | 0.08   |
| Samsung   | MZVLB1T0HBLR-00000 | 1 TB   | 10      | 30    | 0     | 0.08   |
| Samsung   | MZQLB1T9HAJR-00007 | 1.9 TB | 6       | 30    | 0     | 0.08   |
| Kingston  | OM8PDP3512B-A01    | 512 GB | 1       | 30    | 0     | 0.08   |
| Apple     | SSD SM0128L        | 121 GB | 1       | 30    | 0     | 0.08   |
| Samsung   | MZVLB256HAHQ-000H1 | 256 GB | 40      | 29    | 0     | 0.08   |
| XPG       | GAMMIX S5          | 1 TB   | 8       | 29    | 0     | 0.08   |
| WDC       | PC SN720 SDAQNT... | 1 TB   | 2       | 29    | 0     | 0.08   |
| Intel     | MEMPEK1J016GAH     | 16 GB  | 1       | 29    | 0     | 0.08   |
| Silico... | JAMESDONKEY JD512  | 512 GB | 1       | 28    | 0     | 0.08   |
| Lite-On   | CA1-8D128-HP       | 128 GB | 5       | 28    | 0     | 0.08   |
| Toshiba   | KXG60ZNV512G NV... | 512 GB | 18      | 28    | 0     | 0.08   |
| Seagate   | FireCuda 510 SS... | 2 TB   | 2       | 28    | 0     | 0.08   |
| Samsung   | MZVLQ1T0HALB-000H1 | 1 TB   | 5       | 28    | 0     | 0.08   |
| KIOXIA    | KBG40ZPZ1T02 NVMe  | 1 TB   | 5       | 27    | 0     | 0.08   |
| Gigabyte  | GP-GSM2NE3512GNTD  | 512 GB | 5       | 27    | 0     | 0.08   |
| SPCC      | M.2 PCIe SSD       | 2 TB   | 1       | 27    | 0     | 0.08   |
| Samsung   | MZVLW1T0HMLH-000H1 | 1 TB   | 2       | 27    | 0     | 0.08   |
| SK hynix  | PC611 NVMe         | 512 GB | 11      | 27    | 0     | 0.08   |
| Silico... | NVME SSD           | 128 GB | 6       | 27    | 0     | 0.08   |
| Lexar     | SSD                | 128 GB | 5       | 27    | 0     | 0.08   |
| Samsung   | MZVKW1T0HMLH-000H1 | 1 TB   | 1       | 27    | 0     | 0.07   |
| Samsung   | MZVLB1T0HALR-000H1 | 1 TB   | 10      | 27    | 0     | 0.07   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 13      | 27    | 0     | 0.07   |
| Toshiba   | KBG30ZPZ128G       | 128 GB | 2       | 27    | 0     | 0.07   |
| Corsair   | MP400              | 1 TB   | 1       | 26    | 0     | 0.07   |
| Samsung   | PM981a NVMe        | 256 GB | 2       | 26    | 0     | 0.07   |
| Toshiba   | KBG30ZMV128G       | 128 GB | 2       | 26    | 0     | 0.07   |
| Toshiba   | KXG60ZNV256G KI... | 256 GB | 8       | 26    | 0     | 0.07   |
| Phison    | Sabrent Rocket ... | 1 TB   | 1       | 26    | 0     | 0.07   |
| Samsung   | MZVKW1T0HMLH-00000 | 1 TB   | 1       | 26    | 0     | 0.07   |
| Samsung   | MZVLB256HAHQ-000L2 | 256 GB | 17      | 26    | 0     | 0.07   |
| Samsung   | MZVPW256HEGL-000L7 | 256 GB | 1       | 25    | 0     | 0.07   |
| Samsung   | SSD 970 EVO Plus   | 1 TB   | 215     | 25    | 0     | 0.07   |
| Phison    | E12-512G-PHISON... | 512 GB | 2       | 25    | 0     | 0.07   |
| Lenovo    | LENSE30256GMSP3... | 256 GB | 4       | 25    | 0     | 0.07   |
| Plextor   | PX-256M8PeGN       | 256 GB | 2       | 25    | 0     | 0.07   |
| Kingston  | RBUSNS8154P3512GJ  | 512 GB | 9       | 25    | 0     | 0.07   |
| Kingch... | 512GB              | 512 GB | 1       | 25    | 0     | 0.07   |
| Toshiba   | KBG30ZMV256G KI... | 256 GB | 17      | 25    | 0     | 0.07   |
| Toshiba   | KBG30ZMT512G       | 512 GB | 2       | 24    | 0     | 0.07   |
| Toshiba   | RC500              | 250 GB | 1       | 24    | 0     | 0.07   |
| WDC       | WDS200T2B0C-00PXH0 | 2 TB   | 2       | 24    | 0     | 0.07   |
| Transcend | TS512GMTE110S      | 512 GB | 5       | 24    | 0     | 0.07   |
| Union ... | UMIS LENSE40512... | 512 GB | 1       | 24    | 0     | 0.07   |
| Apple     | SSD AP0512M        | 500 GB | 4       | 24    | 0     | 0.07   |
| Samsung   | SSD 970 EVO        | 2 TB   | 9       | 103   | 13    | 0.07   |
| SK hynix  | BC501 HFM256GDJ... | 256 GB | 31      | 24    | 68    | 0.07   |
| Silico... | ShiJi 512GB M.2... | 512 GB | 1       | 24    | 0     | 0.07   |
| HP        | SSD EX950          | 1 TB   | 5       | 24    | 0     | 0.07   |
| Lite-On   | CA5-8D256          | 256 GB | 1       | 23    | 0     | 0.06   |
| Crucial   | CT500P2SSD8        | 500 GB | 14      | 23    | 0     | 0.06   |
| Samsung   | MZVLB256HBHQ-00A00 | 256 GB | 1       | 23    | 0     | 0.06   |
| Samsung   | MZ1LB3T8HMLA-00007 | 3.8 TB | 2       | 23    | 0     | 0.06   |
| SK hynix  | BA HFS256GD9TNG... | 256 GB | 2       | 23    | 0     | 0.06   |
| Samsung   | MZVLB512HBJQ-00007 | 512 GB | 2       | 23    | 0     | 0.06   |
| Netac     | NVMe SSD           | 1 TB   | 1       | 23    | 0     | 0.06   |
| Micron    | 2200V_MTFDHBA51... | 512 GB | 13      | 23    | 0     | 0.06   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 26      | 23    | 0     | 0.06   |
| WDC       | PC SN720 SDAPNT... | 1 TB   | 4       | 22    | 0     | 0.06   |
| Intel     | SSDPEKKF010T8L     | 1 TB   | 16      | 29    | 12    | 0.06   |
| SK hynix  | PC611 NVMe         | 1 TB   | 14      | 22    | 0     | 0.06   |
| Toshiba   | KXG6APNV2T04       | 2 TB   | 2       | 22    | 0     | 0.06   |
| WDC       | PC SN530 SDBPNP... | 1 TB   | 10      | 22    | 0     | 0.06   |
| WDC       | PC SN520 NVMe      | 512 GB | 10      | 22    | 0     | 0.06   |
| XPG       | SPECTRIX S40G      | 1 TB   | 6       | 22    | 0     | 0.06   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 1       | 21    | 0     | 0.06   |
| Samsung   | SSD 970 EVO Plus   | 250 GB | 101     | 21    | 0     | 0.06   |
| Smartbuy  | m.2 PS5013-2280T   | 256 GB | 1       | 21    | 0     | 0.06   |
| Silico... | IM2P33F8BR1-512GB  | 512 GB | 2       | 21    | 0     | 0.06   |
| Crucial   | CT1000P2SSD8       | 1 TB   | 9       | 21    | 0     | 0.06   |
| Gigabyte  | GP-AG4500G         | 500 GB | 3       | 21    | 0     | 0.06   |
| Intel     | SSDPEBKF256G7      | 256 GB | 1       | 21    | 0     | 0.06   |
| ADATA     | SX6000LNP          | 256 GB | 4       | 21    | 0     | 0.06   |
| Silico... | R5MP240G8          | 240 GB | 2       | 21    | 0     | 0.06   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 6       | 20    | 0     | 0.06   |
| Kingston  | RBUSNS8154P3128GJ1 | 128 GB | 5       | 20    | 0     | 0.06   |
| WDC       | PC SN520 SDAPMU... | 256 GB | 19      | 20    | 0     | 0.06   |
| WDC       | WDS500G1X0E-00AFY0 | 500 GB | 3       | 20    | 0     | 0.06   |
| Kingston  | OM8PCP3512F-AB     | 512 GB | 20      | 20    | 0     | 0.06   |
| Solid ... | SSSTC CL1-8D512    | 512 GB | 1       | 20    | 0     | 0.06   |
| WDC       | PC SN530 NVMe      | 256 GB | 5       | 20    | 0     | 0.06   |
| Samsung   | MZFLW512HMJP-000MV | 512 GB | 1       | 20    | 0     | 0.06   |
| Toshiba   | KBG30ZMS512G NVMe  | 512 GB | 1       | 20    | 0     | 0.06   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 4       | 20    | 0     | 0.06   |
| SK hynix  | PC601 HFS512GD9... | 512 GB | 8       | 20    | 0     | 0.05   |
| KIOXIA    | KBG40ZPZ256G NVMe  | 256 GB | 2       | 19    | 0     | 0.05   |
| Silico... | OSC PCIE           | 512 GB | 1       | 19    | 0     | 0.05   |
| Samsung   | MZVLB256HAHQ-00007 | 256 GB | 1       | 19    | 0     | 0.05   |
| Union ... | RPFTJ128PDD2EWX    | 128 GB | 25      | 19    | 0     | 0.05   |
| Apacer    | AS2280P4           | 256 GB | 1       | 19    | 0     | 0.05   |
| SK hynix  | HFM256GDHTNG-8310A | 256 GB | 10      | 19    | 0     | 0.05   |
| SK hynix  | BC711 NVMe         | 512 GB | 1       | 19    | 0     | 0.05   |
| ADATA     | IM2P33F3 NVMe      | 512 GB | 4       | 18    | 0     | 0.05   |
| Silico... | NVMe SSD 256G      | 256 GB | 1       | 18    | 0     | 0.05   |
| Apple     | SSD SM0512L        | 500 GB | 3       | 18    | 0     | 0.05   |
| Lite-On   | CL1-3D256-Q11 NVMe | 256 GB | 4       | 18    | 0     | 0.05   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 2       | 18    | 0     | 0.05   |
| Union ... | RPFTJ256PDD2MWX    | 256 GB | 13      | 18    | 0     | 0.05   |
| Kingston  | RBUSNS8154P3512GJ2 | 512 GB | 1       | 18    | 0     | 0.05   |
| ADATA     | SX6000PNP          | 256 GB | 6       | 18    | 0     | 0.05   |
| HP        | SSD EX900          | 120 GB | 3       | 18    | 0     | 0.05   |
| Samsung   | SSD 970 EVO Plus   | 2 TB   | 53      | 18    | 0     | 0.05   |
| SanDisk   | Extreme Pro        | 2 TB   | 1       | 18    | 0     | 0.05   |
| Samsung   | MZVLB256HBHQ-00007 | 256 GB | 1       | 18    | 0     | 0.05   |
| Gigabyte  | GP-ASM2NE6200TTTD  | 2 TB   | 4       | 17    | 0     | 0.05   |
| ADATA     | IM2P33F3 NVMe      | 256 GB | 7       | 17    | 0     | 0.05   |
| Union ... | UMIS RPJTJ512ME... | 512 GB | 10      | 17    | 0     | 0.05   |
| Corsair   | MP600 CORE         | 2 TB   | 1       | 17    | 0     | 0.05   |
| Union ... | UMIS RPJTJ1TBME... | 1 TB   | 1       | 17    | 0     | 0.05   |
| Micron    | 2200S NVMe         | 1 TB   | 7       | 17    | 0     | 0.05   |
| SK hynix  | BC501 NVMe         | 128 GB | 5       | 16    | 0     | 0.05   |
| Samsung   | MZVLB256HBHQ-00000 | 256 GB | 13      | 16    | 0     | 0.05   |
| WDC       | PC SN730 NVMe      | 512 GB | 10      | 16    | 0     | 0.05   |
| Team      | TM8FP6256G         | 256 GB | 1       | 16    | 0     | 0.04   |
| Silico... | KingSSD-N201000    | 1 TB   | 1       | 16    | 0     | 0.04   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 2       | 16    | 0     | 0.04   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 4       | 16    | 0     | 0.04   |
| Colorful  | CN600S             | 480 GB | 1       | 16    | 0     | 0.04   |
| Silico... | NE-1TB             | 1 TB   | 3       | 15    | 0     | 0.04   |
| ADATA     | SX6000LNP          | 512 GB | 3       | 15    | 0     | 0.04   |
| SK hynix  | BA HFS512GD9TNG... | 512 GB | 1       | 15    | 0     | 0.04   |
| SK hynix  | PC300 NVMe         | 256 GB | 4       | 30    | 2     | 0.04   |
| Micron    | MTFDHBA1T0TCK      | 1 TB   | 4       | 15    | 0     | 0.04   |
| SK hynix  | SKHynix_HFS001T... | 1 TB   | 13      | 15    | 0     | 0.04   |
| Toshiba   | KBG40ZNT512G ME... | 512 GB | 18      | 14    | 0     | 0.04   |
| Toshiba   | KXG6AZNV1T02       | 1 TB   | 4       | 14    | 0     | 0.04   |
| WDC       | WDS200T3X0C-00SJG0 | 2 TB   | 4       | 14    | 0     | 0.04   |
| Patriot   | P300               | 1 TB   | 1       | 14    | 0     | 0.04   |
| WDC       | WDBRPG0020BNC-WRSN | 2 TB   | 1       | 14    | 0     | 0.04   |
| SK hynix  | HFS512GD9TNG-L2A0A | 512 GB | 3       | 14    | 0     | 0.04   |
| SK hynix  | BC501 NVMe         | 256 GB | 8       | 14    | 0     | 0.04   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 5       | 14    | 0     | 0.04   |
| V-GeN     | V-GEN11SM20AR51... | 512 GB | 1       | 14    | 0     | 0.04   |
| WDC       | PC SN730 SDBQNT... | 512 GB | 58      | 14    | 0     | 0.04   |
| SK hynix  | HFM256GDJTNG-8310A | 256 GB | 21      | 13    | 0     | 0.04   |
| WDC       | PC SN530 SDBPNP... | 1 TB   | 3       | 13    | 0     | 0.04   |
| Apple     | SSD SM0032L        | 32 GB  | 8       | 13    | 0     | 0.04   |
| Seagate   | BarraCuda 510 S... | 512 GB | 2       | 13    | 0     | 0.04   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 3       | 13    | 0     | 0.04   |
| Kingston  | RBUSNS8154P3512GJ3 | 512 GB | 3       | 13    | 0     | 0.04   |
| Apple     | SSD AP0512J        | 500 GB | 4       | 13    | 0     | 0.04   |
| Samsung   | MZVLB1T0HBLR-000L2 | 1 TB   | 37      | 13    | 0     | 0.04   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 2       | 13    | 0     | 0.04   |
| Toshiba   | KBG40ZNT256G ME... | 256 GB | 8       | 13    | 0     | 0.04   |
| SK hynix  | HFM512GD3JX013N    | 512 GB | 1       | 13    | 0     | 0.04   |
| Lexar     | 500GB SSD          | 500 GB | 4       | 13    | 0     | 0.04   |
| Patriot   | M.2 P300           | 512 GB | 1       | 12    | 0     | 0.04   |
| SK hynix  | HFM256GDHTNG-8510B | 256 GB | 6       | 12    | 0     | 0.04   |
| Samsung   | MZVLB256HBHQ-000L7 | 256 GB | 38      | 12    | 0     | 0.04   |
| KIOXIA    | KBG40ZNS1T02 NVMe  | 1 TB   | 1       | 12    | 0     | 0.03   |
| Samsung   | MZVLB2T0HALB-000L2 | 2 TB   | 2       | 12    | 0     | 0.03   |
| WDC       | PC SN730 SDBQNT... | 256 GB | 10      | 12    | 0     | 0.03   |
| SK hynix  | HFS512GD9TNG-62A0A | 512 GB | 5       | 12    | 0     | 0.03   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 2       | 12    | 0     | 0.03   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 7       | 12    | 0     | 0.03   |
| ADATA     | SX8200PNP-512GT    | 512 GB | 1       | 12    | 0     | 0.03   |
| Micron    | 2200_MTFDHBA512TCK | 512 GB | 2       | 11    | 0     | 0.03   |
| Samsung   | MZWLJ1T9HBJR-00007 | 1.9 TB | 1       | 11    | 0     | 0.03   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 3       | 11    | 0     | 0.03   |
| Lite-On   | CL1-8D512          | 512 GB | 6       | 11    | 0     | 0.03   |
| Samsung   | MZVLB1T0HBLR-00A00 | 1 TB   | 1       | 11    | 0     | 0.03   |
| Samsung   | MZVLB512HBJQ-000L2 | 512 GB | 54      | 11    | 0     | 0.03   |
| SK hynix  | PC711 NVMe         | 1 TB   | 3       | 11    | 0     | 0.03   |
| Patriot   | P300               | 128 GB | 1       | 11    | 0     | 0.03   |
| Silico... | Inland NVMe SSD    | 256 GB | 1       | 11    | 0     | 0.03   |
| WDC       | CL SN720 SDAQNT... | 1 TB   | 1       | 11    | 0     | 0.03   |
| Solid ... | SSSTC CL1-4D256    | 256 GB | 3       | 11    | 0     | 0.03   |
| Samsung   | PM991 NVMe         | 256 GB | 9       | 11    | 0     | 0.03   |
| Samsung   | MZVLB1T0HBLR-000L7 | 1 TB   | 54      | 11    | 0     | 0.03   |
| Solid ... | SSSTC CL1-8D256-HP | 256 GB | 2       | 11    | 0     | 0.03   |
| Samsung   | MZVLB512HBJQ-000L7 | 512 GB | 74      | 11    | 0     | 0.03   |
| ADATA     | IM2P33F3A NVMe     | 256 GB | 5       | 10    | 0     | 0.03   |
| Silico... | Qunion P20A 512... | 512 GB | 1       | 10    | 0     | 0.03   |
| ADATA     | SX6000PNP          | 1 TB   | 9       | 13    | 65    | 0.03   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 9       | 10    | 0     | 0.03   |
| Mushkin   | MKNSSDHL1TB-D8     | 1 TB   | 3       | 59    | 25    | 0.03   |
| Silico... | 256GB              | 256 GB | 6       | 10    | 0     | 0.03   |
| Kingston  | RBUSNS8154P3256GJ1 | 256 GB | 14      | 10    | 0     | 0.03   |
| Micron    | 2200V_MTFDHBA25... | 256 GB | 1       | 10    | 0     | 0.03   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 2       | 10    | 0     | 0.03   |
| Seagate   | IronWolf510 ZP9... | 960 GB | 2       | 10    | 0     | 0.03   |
| Seagate   | FireCuda 520 SS... | 2 TB   | 4       | 9     | 0     | 0.03   |
| Phison    | One-Netbook PCI... | 512 GB | 2       | 9     | 0     | 0.03   |
| Star D... | PCIe SSD           | 480 GB | 2       | 9     | 0     | 0.03   |
| Samsung   | MZVLB512HBJQ-00A00 | 512 GB | 3       | 9     | 0     | 0.03   |
| KIOXIA    | KBG40ZNV1T02       | 1 TB   | 7       | 9     | 0     | 0.03   |
| Union ... | UMIS RPITJ256PE... | 256 GB | 1       | 9     | 0     | 0.03   |
| Intel     | SSDPEKNW010T9      | 1 TB   | 11      | 9     | 0     | 0.03   |
| Apple     | SSD AP0128H        | 121 GB | 2       | 9     | 0     | 0.03   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 2       | 9     | 0     | 0.03   |
| Team      | TM8FP6001T         | 1 TB   | 3       | 9     | 0     | 0.03   |
| WDC       | PC SN730 SDBQNT... | 1 TB   | 16      | 9     | 0     | 0.03   |
| SK hynix  | HFM128GDGTNG-87A0A | 128 GB | 1       | 9     | 0     | 0.03   |
| WDC       | PC SN520 SDAPMU... | 512 GB | 4       | 14    | 1     | 0.02   |
| Micron    | 2210_MTFDHBA1T0QFD | 1 TB   | 10      | 8     | 0     | 0.02   |
| Phison    | Viper M.2 VPR100   | 512 GB | 1       | 8     | 0     | 0.02   |
| Toshiba   | KBG40ZNS128G NVMe  | 128 GB | 1       | 8     | 0     | 0.02   |
| Samsung   | MZALQ128HBHQ-000L2 | 128 GB | 9       | 8     | 0     | 0.02   |
| Phison    | Daten DS2000       | 512 GB | 1       | 8     | 0     | 0.02   |
| Intel     | SSDPEMKF256G8 NVMe | 256 GB | 1       | 8     | 0     | 0.02   |
| SPCC      | M.2 PCIE SSD       | 512 GB | 1       | 8     | 0     | 0.02   |
| WDC       | PC SN520 SDAPMU... | 128 GB | 6       | 8     | 0     | 0.02   |
| Samsung   | MZVLB512HBJQ-00000 | 512 GB | 11      | 8     | 0     | 0.02   |
| Crucial   | CT2000P2SSD8       | 2 TB   | 1       | 8     | 0     | 0.02   |
| WDC       | WDS200T1X0E-00AFY0 | 2 TB   | 1       | 8     | 0     | 0.02   |
| Kingston  | OM8PCP3512F-AI1    | 512 GB | 7       | 8     | 0     | 0.02   |
| SK hynix  | BC511 NVMe         | 256 GB | 13      | 8     | 0     | 0.02   |
| Samsung   | MZVLB256HBHQ-000L2 | 256 GB | 13      | 8     | 0     | 0.02   |
| WDC       | WDS100T1X0E-00AFY0 | 1 TB   | 3       | 8     | 0     | 0.02   |
| Samsung   | PM981a NVMe        | 512 GB | 20      | 8     | 0     | 0.02   |
| Hikvision | HS-SSD-C2000Pro... | 1 TB   | 2       | 8     | 0     | 0.02   |
| Samsung   | MZVLQ256HAJD-00007 | 256 GB | 1       | 7     | 0     | 0.02   |
| Lexar     | 250GB SSD          | 250 GB | 1       | 7     | 0     | 0.02   |
| Apple     | SSD AP0512N        | 500 GB | 4       | 7     | 0     | 0.02   |
| Samsung   | MZVLQ512HALU-00000 | 512 GB | 27      | 7     | 0     | 0.02   |
| Solid ... | CL1-3D128-Q11 N... | 128 GB | 1       | 7     | 0     | 0.02   |
| Samsung   | PM991 NVMe         | 512 GB | 9       | 7     | 0     | 0.02   |
| ADATA     | IM2P33F3 NVMe      | 128 GB | 1       | 7     | 0     | 0.02   |
| XrayDisk  | 512GB              | 512 GB | 1       | 7     | 0     | 0.02   |
| ADATA     | SX6000LNP          | 1 TB   | 4       | 60    | 252   | 0.02   |
| KINGBANK  | KP230              | 128 GB | 1       | 7     | 0     | 0.02   |
| Toshiba   | KXG5AZNV256G NV... | 256 GB | 1       | 7     | 0     | 0.02   |
| Kingston  | OM8PDP3256B-AI1    | 256 GB | 2       | 7     | 0     | 0.02   |
| Samsung   | MZVLQ256HAJD-000H1 | 256 GB | 29      | 7     | 0     | 0.02   |
| KIOXIA    | KBG40ZNV512G       | 512 GB | 18      | 7     | 0     | 0.02   |
| ADATA     | SWORDFISH          | 250 GB | 1       | 7     | 0     | 0.02   |
| Samsung   | PM981a NVMe        | 2 TB   | 11      | 7     | 0     | 0.02   |
| WDC       | PC SN730 NVMe      | 256 GB | 2       | 7     | 0     | 0.02   |
| Silico... | 512GB PCS PCIe ... | 512 GB | 1       | 6     | 0     | 0.02   |
| Toshiba   | KXG6AZNV512G KI... | 512 GB | 3       | 6     | 0     | 0.02   |
| Apple     | SSD AP0256J        | 256 GB | 3       | 6     | 0     | 0.02   |
| SK hynix  | BC501 HFM512GDJ... | 512 GB | 19      | 6     | 0     | 0.02   |
| WDC       | PC SN730 SDBPNT... | 256 GB | 6       | 6     | 0     | 0.02   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 15      | 6     | 0     | 0.02   |
| SanDisk   | WD_BLACK SN850     | 1 TB   | 1       | 6     | 0     | 0.02   |
| FORESEE   | 512GB SSD          | 512 GB | 2       | 6     | 0     | 0.02   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 22      | 6     | 0     | 0.02   |
| Lite-On   | CX2-8B256-Q11 NVMe | 256 GB | 2       | 6     | 0     | 0.02   |
| Union ... | UMIS RPJTJ256ME... | 256 GB | 12      | 6     | 0     | 0.02   |
| Samsung   | MZALQ512HALU-000L2 | 512 GB | 45      | 6     | 0     | 0.02   |
| Samsung   | MZVL2512HCJQ-00BL2 | 512 GB | 3       | 6     | 0     | 0.02   |
| SK hynix  | BC501 NVMe         | 512 GB | 5       | 6     | 0     | 0.02   |
| Phison    | Sabrent Rocket ... | 1 TB   | 3       | 6     | 0     | 0.02   |
| SK hynix  | HFM512GDHTNG-8310A | 512 GB | 5       | 6     | 0     | 0.02   |
| Phison    | Reletech P400 SSD  | 512 GB | 1       | 6     | 0     | 0.02   |
| Samsung   | MZALQ512HALU-000L1 | 512 GB | 27      | 5     | 0     | 0.02   |
| Samsung   | PM981a NVMe SED    | 512 GB | 1       | 5     | 0     | 0.02   |
| Toshiba   | KBG30ZMV512G KI... | 512 GB | 5       | 5     | 0     | 0.02   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 4       | 5     | 0     | 0.02   |
| SK hynix  | SKHynix_HFM256G... | 256 GB | 16      | 5     | 0     | 0.02   |
| Kingston  | SKC2500M8250G      | 250 GB | 2       | 5     | 0     | 0.02   |
| Intenso   | PCIe               | 240 GB | 1       | 5     | 0     | 0.02   |
| Samsung   | MZVLQ1T0HALB-00000 | 1 TB   | 4       | 5     | 0     | 0.02   |
| Samsung   | MZALQ256HAJD-000L2 | 256 GB | 25      | 5     | 0     | 0.02   |
| KIOXIA    | KBG40ZNV256G       | 256 GB | 9       | 5     | 0     | 0.01   |
| Samsung   | MZVLB2T0HMLB-000H1 | 2 TB   | 1       | 5     | 0     | 0.01   |
| Micron    | MTFDHBA256TCK-1... | 256 GB | 17      | 6     | 1     | 0.01   |
| PNY       | CS3030 2000GB SSD  | 2 TB   | 1       | 5     | 0     | 0.01   |
| Phison    | PS5012-E12S-512G   | 512 GB | 1       | 5     | 0     | 0.01   |
| SK hynix  | HFM001TD3JX013N    | 1 TB   | 5       | 5     | 0     | 0.01   |
| Samsung   | SSD 980 PRO        | 500 GB | 18      | 5     | 0     | 0.01   |
| Apple     | SSD AP1024N        | 1 TB   | 2       | 5     | 0     | 0.01   |
| Micron    | 2210_MTFDHBA512QFD | 512 GB | 2       | 5     | 0     | 0.01   |
| SK hynix  | BC501A NVMe        | 128 GB | 2       | 5     | 0     | 0.01   |
| SK hynix  | HFM512GDJTNG-8310A | 512 GB | 23      | 5     | 0     | 0.01   |
| Micron    | MTFDHBA1T0TDV-1... | 1 TB   | 1       | 5     | 0     | 0.01   |
| SK hynix  | HFM512GDHTNG-8710B | 512 GB | 12      | 5     | 0     | 0.01   |
| Toshiba   | KXG60ZNV256G       | 256 GB | 4       | 4     | 0     | 0.01   |
| Intel     | SSDPE21D280GA      | 280 GB | 1       | 4     | 0     | 0.01   |
| Toshiba   | KBG40ZMT128G ME... | 128 GB | 3       | 4     | 0     | 0.01   |
| Gigabyte  | GP-AG41TB          | 1 TB   | 3       | 4     | 0     | 0.01   |
| Kingston  | SKC2500M81000G     | 1 TB   | 3       | 4     | 0     | 0.01   |
| PNY       | CS2130 1TB SSD     | 1 TB   | 1       | 4     | 0     | 0.01   |
| Samsung   | PM981 NVMe SED     | 512 GB | 1       | 4     | 0     | 0.01   |
| Micron    | MTFDHBA512QFD      | 512 GB | 3       | 4     | 0     | 0.01   |
| Micron    | 2300 NVMe          | 1 TB   | 12      | 4     | 0     | 0.01   |
| Micron    | 2200_MTFDHBA256TCK | 256 GB | 3       | 4     | 0     | 0.01   |
| Samsung   | MZVLB1T0HBLR-000H1 | 1 TB   | 15      | 4     | 0     | 0.01   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 10      | 4     | 0     | 0.01   |
| Intel     | SSDPEKKA128G8      | 128 GB | 1       | 4     | 0     | 0.01   |
| MAXIO     | NE-256             | 256 GB | 1       | 4     | 0     | 0.01   |
| WDC       | WDBRPG0010BNC-WRSN | 1 TB   | 3       | 4     | 0     | 0.01   |
| Apple     | SSD SM0256L        | 256 GB | 3       | 4     | 0     | 0.01   |
| Solid ... | CL1-3D256-Q11 N... | 256 GB | 4       | 4     | 0     | 0.01   |
| ADATA     | SX6000NP           | 512 GB | 2       | 4     | 0     | 0.01   |
| Phison    | E12S-1TB-PHISON... | 1 TB   | 1       | 4     | 0     | 0.01   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 17      | 4     | 0     | 0.01   |
| SK hynix  | BC511 NVMe         | 512 GB | 27      | 4     | 0     | 0.01   |
| Samsung   | MZALQ128HBHQ-000L1 | 128 GB | 4       | 4     | 0     | 0.01   |
| Toshiba   | KXG60ZNV1T02 KI... | 1 TB   | 5       | 4     | 0     | 0.01   |
| Kingston  | OM8PCP3512F-AA     | 512 GB | 5       | 4     | 0     | 0.01   |
| KIOXIA... | SSD                | 500 GB | 2       | 3     | 0     | 0.01   |
| Samsung   | MZVLQ512HALU-000H1 | 512 GB | 18      | 3     | 0     | 0.01   |
| Phison    | 1TB SM2801T24GK... | 1 TB   | 5       | 3     | 0     | 0.01   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 6       | 3     | 0     | 0.01   |
| Apple     | SSD AP0256M        | 256 GB | 3       | 3     | 0     | 0.01   |
| Samsung   | SSD 980 PRO        | 1 TB   | 19      | 3     | 0     | 0.01   |
| SK hynix  | HFM128GDHTNG-8310B | 128 GB | 2       | 3     | 0     | 0.01   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 1       | 3     | 0     | 0.01   |
| WDC       | PC SN520 SDAPMU... | 128 GB | 5       | 3     | 0     | 0.01   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 2       | 28    | 5     | 0.01   |
| ADATA     | SX6000LNP          | 128 GB | 5       | 3     | 0     | 0.01   |
| Samsung   | MZVLB512HAJQ-000H7 | 512 GB | 4       | 3     | 0     | 0.01   |
| Samsung   | MZVLB512HBJQ-000H1 | 512 GB | 21      | 3     | 0     | 0.01   |
| EMTEC     | X300               | 256 GB | 1       | 3     | 0     | 0.01   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 4       | 3     | 0     | 0.01   |
| Apple     | SSD AP2048N        | 2 TB   | 2       | 3     | 0     | 0.01   |
| Corsair   | Force MP510        | 4 TB   | 1       | 3     | 0     | 0.01   |
| ADATA     | SWORDFISH          | 1 TB   | 6       | 3     | 0     | 0.01   |
| WDC       | PC SN530 SDBPMP... | 512 GB | 9       | 3     | 0     | 0.01   |
| SK hynix  | BC511 HFM512GDJ... | 512 GB | 22      | 3     | 0     | 0.01   |
| Gigabyte  | GP-GSM2NE8128GNTD  | 128 GB | 1       | 3     | 0     | 0.01   |
| WDC       | WDBA3V5000ANC-WRSN | 500 GB | 1       | 3     | 0     | 0.01   |
| Samsung   | SSD 980 PRO        | 2 TB   | 5       | 3     | 0     | 0.01   |
| Crucial   | CT250P5SSD8        | 250 GB | 1       | 2     | 0     | 0.01   |
| Samsung   | MZVLB256HBHQ-000H1 | 256 GB | 3       | 2     | 0     | 0.01   |
| WDC       | PC SN530 SDBPMP... | 256 GB | 4       | 2     | 0     | 0.01   |
| KingFast  | 1TB                | 1 TB   | 1       | 2     | 0     | 0.01   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 2       | 2     | 0     | 0.01   |
| Crucial   | CT1000P5SSD8       | 1 TB   | 4       | 2     | 0     | 0.01   |
| Samsung   | MZALQ256HAJD-000L1 | 256 GB | 11      | 2     | 0     | 0.01   |
| SK hynix  | HFM128GDJTNG-8310A | 128 GB | 2       | 2     | 0     | 0.01   |
| Silico... | NVMe               | 256 GB | 1       | 2     | 0     | 0.01   |
| WDC       | PC SN530 SDBPMP... | 256 GB | 13      | 2     | 0     | 0.01   |
| Kingston  | RBUSNS8154P3256GJ5 | 256 GB | 1       | 2     | 0     | 0.01   |
| WDC       | PC SN530 SDBPMP... | 512 GB | 9       | 2     | 0     | 0.01   |
| Lite-On   | CA5-8D512          | 512 GB | 3       | 2     | 0     | 0.01   |
| WDC       | PC SN730 NVMe      | 1 TB   | 21      | 2     | 0     | 0.01   |
| WDC       | PC SN730 SDBPNT... | 256 GB | 1       | 2     | 0     | 0.01   |
| FORESEE   | P900F256GB         | 256 GB | 1       | 2     | 0     | 0.01   |
| Samsung   | PM991a NVMe        | 512 GB | 2       | 2     | 0     | 0.01   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 3       | 2     | 0     | 0.01   |
| Phison    | Sabrent Rocket Q4  | 1 TB   | 1       | 2     | 0     | 0.01   |
| SK hynix  | HFM512GDJTNI-82A0A | 512 GB | 11      | 2     | 0     | 0.01   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 7       | 1     | 0     | 0.01   |
| Samsung   | SSD 980            | 500 GB | 4       | 1     | 0     | 0.01   |
| SK hynix  | Skhynix BC501 NVMe | 128 GB | 1       | 1     | 0     | 0.01   |
| Intel     | SSDPEKKA256G7      | 256 GB | 2       | 1     | 0     | 0.01   |
| Seagate   | BarraCuda Q5 ZP... | 500 GB | 1       | 1     | 0     | 0.01   |
| SK hynix  | SKHynix_HFM512G... | 512 GB | 21      | 1     | 0     | 0.01   |
| SK hynix  | BC511 HFM256GDJ... | 256 GB | 17      | 1     | 0     | 0.01   |
| GLOWAY    | YCT512NVMe-M.2-... | 512 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | MZVL21T0HCLR-00BL7 | 1 TB   | 3       | 1     | 0     | 0.00   |
| Toshiba   | KBG30ZMV128G KI... | 128 GB | 1       | 1     | 0     | 0.00   |
| Kingston  | OM8PCP31024F-AI1   | 1 TB   | 2       | 1     | 0     | 0.00   |
| Micron    | MTFDHBA512TDV      | 512 GB | 1       | 1     | 0     | 0.00   |
| Union ... | UMIS RPITJ512PE... | 512 GB | 2       | 1     | 0     | 0.00   |
| ADATA     | IM2P33F8BR1-128GB  | 128 GB | 1       | 1     | 0     | 0.00   |
| Corsair   | MP400              | 2 TB   | 2       | 1     | 0     | 0.00   |
| Micron    | 2300 NVMe          | 512 GB | 8       | 1     | 0     | 0.00   |
| Lite-On   | CA3-8D128-HP       | 128 GB | 2       | 1     | 0     | 0.00   |
| BIWIN     | NE-128             | 128 GB | 1       | 1     | 0     | 0.00   |
| Toshiba   | KXG60PNV1T02 NV... | 1 TB   | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN530 SDBPNP... | 1 TB   | 1       | 1     | 0     | 0.00   |
| ADATA     | IM2P33F3A NVMe     | 512 GB | 2       | 1     | 0     | 0.00   |
| Silico... | Asgard AN3 1TNV... | 1 TB   | 1       | 1     | 0     | 0.00   |
| Intel     | SSDPEDKE020T7      | 2 TB   | 2       | 1     | 0     | 0.00   |
| Samsung   | MZVLB1T0HBLR-00007 | 1 TB   | 1       | 1     | 0     | 0.00   |
| Seagate   | BarraCuda 510 S... | 250 GB | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 7       | 1     | 0     | 0.00   |
| SK hynix  | HFM256GDJTNI-82A0A | 256 GB | 4       | 1     | 0     | 0.00   |
| KIOXIA    | KBG40ZNS128G BG4A  | 128 GB | 1       | 1     | 0     | 0.00   |
| PNY       | CS1030 1TB SSD     | 1 TB   | 1       | 1     | 0     | 0.00   |
| Transcend | TS256GMTE110S      | 256 GB | 3       | 1     | 0     | 0.00   |
| Micron    | MTFDHBA256TCK      | 256 GB | 2       | 1     | 0     | 0.00   |
| SK hynix  | SHGP31-1000GM-2    | 1 TB   | 2       | 1     | 0     | 0.00   |
| Crucial   | CT500P5SSD8        | 500 GB | 7       | 1     | 0     | 0.00   |
| Phison    | E12-512G-PHISON... | 512 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | MZVPW128HEGM-00000 | 128 GB | 1       | 37    | 32    | 0.00   |
| Kingston  | SKC2000M81000G     | 1 TB   | 1       | 1     | 0     | 0.00   |
| SK hynix  | PC711 NVMe         | 256 GB | 1       | 1     | 0     | 0.00   |
| SK hynix  | PC711 NVMe         | 512 GB | 2       | 1     | 0     | 0.00   |
| Silico... | WN600              | 1 TB   | 1       | 1     | 0     | 0.00   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 1       | 1     | 0     | 0.00   |
| Silico... | 512GB              | 512 GB | 1       | 1     | 0     | 0.00   |
| Crucial   | CT2000P5SSD8       | 2 TB   | 1       | 1     | 0     | 0.00   |
| Samsung   | MZVLQ256HAJD-00000 | 256 GB | 6       | 1     | 0     | 0.00   |
| SK hynix  | SKHynix_HFM512G... | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | Skhynix BC501 NVMe | 256 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | SSD 980            | 1 TB   | 2       | 0     | 0     | 0.00   |
| Samsung   | MZVLB512HBJQ-000H7 | 512 GB | 2       | 0     | 0     | 0.00   |
| Goodram   | SSDPR-PX500-512-80 | 512 GB | 2       | 0     | 0     | 0.00   |
| XrayDisk  | 256GB              | 256 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | PM9A1 NVMe         | 1 TB   | 4       | 0     | 0     | 0.00   |
| WDC       | PC SN530 SDBPTP... | 512 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVL21T0HCLR-00BH1 | 1 TB   | 1       | 0     | 0     | 0.00   |
| Micron    | MTFDHBA256TDV      | 256 GB | 4       | 0     | 0     | 0.00   |
| Phison    | 512GB SM280512G... | 512 GB | 1       | 0     | 0     | 0.00   |
| Silico... | NE-240             | 240 GB | 1       | 0     | 0     | 0.00   |
| Toshiba   | KXG50PNV2T04 KI... | 2 TB   | 1       | 0     | 0     | 0.00   |
| WDC       | WDBA3V0010BNC-WRSN | 1 TB   | 1       | 0     | 0     | 0.00   |
| Lite-On   | CA1-8D256-HP       | 256 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVLB512HBJQ-000   | 512 GB | 3       | 0     | 0     | 0.00   |
| ADATA     | FALCON             | 512 GB | 1       | 0     | 0     | 0.00   |
| Zheino    | CHN-NGFFNV2280-256 | 256 GB | 1       | 0     | 0     | 0.00   |
| BIWIN     | NI201_256GB        | 256 GB | 1       | 0     | 0     | 0.00   |
| SMI       | 2263XT             | 120 GB | 1       | 0     | 0     | 0.00   |
| Plextor   | PX-512M9PeGN       | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | PC601 SED NVMe     | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | Skhynix BC501 NVMe | 512 GB | 1       | 0     | 0     | 0.00   |
| T-FORCE   | TM8FP7002T         | 2 TB   | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 1       | 0     | 0     | 0.00   |
| Silico... | NVMe SSD           | 240 GB | 1       | 0     | 0     | 0.00   |
| Solid ... | SSSTC CL1-4D256... | 256 GB | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN530 NVMe      | 512 GB | 4       | 0     | 0     | 0.00   |
| Mushkin   | MKNSSDPE2TB-D8     | 2 TB   | 2       | 0     | 0     | 0.00   |
| Phison    | Viper M.2 VP4100   | 500 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | SSD 980 PRO        | 250 GB | 4       | 0     | 0     | 0.00   |
| ADATA     | IM2P33F8-512GD     | 512 GB | 2       | 0     | 0     | 0.00   |
| Solid ... | SSSTC CL1-4D512    | 512 GB | 1       | 0     | 0     | 0.00   |
| Toshiba   | KBG40ZPZ128G ME... | 128 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TS512GMTE510T      | 512 GB | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN530 SDBQNP... | 512 GB | 2       | 0     | 0     | 0.00   |
| SK hynix  | HFM128GDHTNG-8510B | 128 GB | 2       | 0     | 0     | 0.00   |
| Kingston  | RBUSNS8154P3128GJ5 | 128 GB | 3       | 0     | 0     | 0.00   |
| Gigabyte  | GP-ASM2NE2512GTTDR | 512 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | OM3PDP3-AD NVMe... | 256 GB | 1       | 0     | 0     | 0.00   |
| Mushkin   | MKNSSDPE1TB-D8     | 1 TB   | 1       | 0     | 0     | 0.00   |
| Yangtz... | ZHITAI PC005 Ac... | 1 TB   | 1       | 0     | 0     | 0.00   |
| BIWIN     | NE-512             | 512 GB | 1       | 0     | 0     | 0.00   |
| Crucial   | CT2000P1SSD8       | 2 TB   | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVLB256HBHQ-000   | 256 GB | 1       | 0     | 0     | 0.00   |

NVME by Vendor
--------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF   |
|-------------|--------|---------|-------|-------|--------|
| ZOTAC       | 1      | 1       | 899   | 0     | 2.47   |
| addlink     | 1      | 3       | 167   | 0     | 0.46   |
| Intel       | 77     | 743     | 170   | 4     | 0.45   |
| Corsair     | 17     | 108     | 157   | 1     | 0.40   |
| Transcend   | 8      | 25      | 141   | 0     | 0.39   |
| Toshiba     | 82     | 502     | 139   | 0     | 0.38   |
| HP          | 9      | 42      | 141   | 2     | 0.35   |
| SanDisk     | 6      | 17      | 126   | 0     | 0.35   |
| Plextor     | 14     | 28      | 132   | 24    | 0.30   |
| Apacer      | 5      | 6       | 98    | 0     | 0.27   |
| Crucial     | 11     | 174     | 108   | 9     | 0.26   |
| Lenovo      | 5      | 28      | 96    | 0     | 0.26   |
| XPG         | 5      | 58      | 91    | 0     | 0.25   |
| Phison      | 32     | 194     | 87    | 0     | 0.24   |
| Huawei      | 2      | 10      | 78    | 0     | 0.22   |
| Team        | 6      | 11      | 74    | 0     | 0.20   |
| ADATA       | 33     | 213     | 74    | 14    | 0.19   |
| Patriot     | 7      | 13      | 69    | 0     | 0.19   |
| Mushkin     | 6      | 10      | 81    | 8     | 0.18   |
| Zheino      | 2      | 3       | 65    | 0     | 0.18   |
| Seagate     | 12     | 36      | 61    | 0     | 0.17   |
| Lite-On     | 16     | 44      | 60    | 0     | 0.17   |
| Samsung     | 157    | 2872    | 61    | 3     | 0.16   |
| Smartbuy    | 2      | 2       | 58    | 0     | 0.16   |
| SPCC        | 8      | 40      | 58    | 0     | 0.16   |
| PNY         | 8      | 27      | 52    | 0     | 0.14   |
| Hikvision   | 5      | 6       | 50    | 0     | 0.14   |
| Gigabyte    | 14     | 42      | 49    | 0     | 0.14   |
| Silicon ... | 35     | 76      | 47    | 0     | 0.13   |
| WDC         | 111    | 932     | 46    | 3     | 0.13   |
| Kingchuxing | 2      | 2       | 42    | 0     | 0.12   |
| Kingston    | 32     | 263     | 42    | 4     | 0.12   |
| KIOXIA-E... | 2      | 5       | 36    | 0     | 0.10   |
| Goodram     | 2      | 3       | 33    | 0     | 0.09   |
| KIOXIA      | 10     | 97      | 29    | 0     | 0.08   |
| Lexar       | 4      | 11      | 28    | 0     | 0.08   |
| SK hynix    | 72     | 539     | 27    | 4     | 0.07   |
| Netac       | 1      | 1       | 23    | 0     | 0.06   |
| Micron      | 21     | 119     | 22    | 1     | 0.06   |
| Union Me... | 10     | 70      | 20    | 0     | 0.06   |
| FORESEE     | 3      | 4       | 20    | 0     | 0.06   |
| Colorful    | 1      | 1       | 16    | 0     | 0.04   |
| Apple       | 16     | 44      | 15    | 0     | 0.04   |
| V-GeN       | 1      | 1       | 14    | 0     | 0.04   |
| Solid St... | 8      | 15      | 13    | 0     | 0.04   |
| Star Drive  | 1      | 2       | 9     | 0     | 0.03   |
| KINGBANK    | 1      | 1       | 7     | 0     | 0.02   |
| Intenso     | 1      | 1       | 5     | 0     | 0.02   |
| MAXIO       | 1      | 1       | 4     | 0     | 0.01   |
| XrayDisk    | 2      | 2       | 4     | 0     | 0.01   |
| EMTEC       | 1      | 1       | 3     | 0     | 0.01   |
| KingFast    | 1      | 1       | 2     | 0     | 0.01   |
| GLOWAY      | 1      | 1       | 1     | 0     | 0.00   |
| BIWIN       | 3      | 3       | 0     | 0     | 0.00   |
| SMI         | 1      | 1       | 0     | 0     | 0.00   |
| T-FORCE     | 1      | 1       | 0     | 0     | 0.00   |
| Yangtze ... | 1      | 1       | 0     | 0     | 0.00   |

