HDD/SSD Desktop-Class Reliability Test
======================================

This is a project to estimate reliability of desktop-class HDD/SSD drives by
the analysis of SMART data collected by Linux users at https://linux-hardware.org. The
primary aim of the project is to find drives with longest power-on hours (POH) and
minimal number of errors, i.e. maximal MTBF (mean time between failures).

Everyone can contribute to this report by uploading probes of their computers by
the [hw-probe](https://github.com/linuxhw/hw-probe) tool:

    sudo -E hw-probe -all -upload

Total drives: 42696.

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
| WDC       | WD1600JD-00HBC0    | 160 GB | 1       | 3315  | 0     | 9.08   |
| WDC       | WD10EAVS-32D7B1    | 1 TB   | 1       | 3311  | 0     | 9.07   |
| Samsung   | HE160HJ            | 160 GB | 1       | 2967  | 0     | 8.13   |
| WDC       | WD1200JB-00REA0    | 120 GB | 1       | 2899  | 0     | 7.94   |
| Seagate   | ST3500641AS        | 500 GB | 2       | 2833  | 0     | 7.76   |
| WDC       | WD10EACS-14ZJB0    | 1 TB   | 1       | 2742  | 0     | 7.51   |
| WDC       | WD1601ABYS-18C0A0  | 160 GB | 1       | 2667  | 0     | 7.31   |
| WDC       | WD3000HLFS-01G6U1  | 304 GB | 1       | 2636  | 0     | 7.22   |
| WDC       | WD2000FYYZ-01UL1B0 | 2 TB   | 1       | 2603  | 0     | 7.13   |
| WDC       | WD10EACS-00C7B0    | 1 TB   | 3       | 2600  | 0     | 7.12   |
| Hitachi   | HUA7210SASUN1.0T   | 1 TB   | 10      | 2520  | 0     | 6.91   |
| WDC       | WD740GD-00FLA1     | 74 GB  | 1       | 2489  | 0     | 6.82   |
| WDC       | WD2500YS-01SHB0    | 256 GB | 1       | 2484  | 0     | 6.81   |
| Seagate   | ST3320820AS_P      | 320 GB | 1       | 2447  | 0     | 6.70   |
| Seagate   | ST2000DL004 HD2... | 2 TB   | 1       | 2366  | 0     | 6.48   |
| WDC       | WD2502ABYS-02B7A0  | 256 GB | 3       | 2459  | 4     | 6.47   |
| Seagate   | ST3250820AS Q      | 250 GB | 1       | 2361  | 0     | 6.47   |
| WDC       | WD2500AAJS-07VWA0  | 250 GB | 2       | 2354  | 0     | 6.45   |
| Hitachi   | HUA722020ALA330    | 2 TB   | 12      | 2986  | 3     | 6.37   |
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
| WDC       | WD5000AAKS-402AA0  | 500 GB | 1       | 2097  | 0     | 5.75   |
| HP        | GB0500C4413        | 500 GB | 2       | 2009  | 0     | 5.51   |
| WDC       | WD1002FBYS-18W8B1  | 1 TB   | 1       | 1999  | 0     | 5.48   |
| WDC       | WD800AAJB-00J3A0   | 80 GB  | 1       | 1982  | 0     | 5.43   |
| WDC       | WD1601ABYS-01C0A0  | 164 GB | 1       | 1982  | 0     | 5.43   |
| WDC       | WD1600AAJS-00RYA0  | 160 GB | 1       | 1970  | 0     | 5.40   |
| Hitachi   | HDS722516VLSA80    | 164 GB | 2       | 2077  | 1     | 5.36   |
| Hitachi   | HUA722010CLA331    | 1 TB   | 1       | 1939  | 0     | 5.31   |
| WDC       | WD2003FYPS-27Y2B0  | 2 TB   | 5       | 2163  | 1     | 5.29   |
| WDC       | WD6400AAKS-07A7B0  | 640 GB | 1       | 1900  | 0     | 5.21   |
| WDC       | WD800JD-60LUA0     | 80 GB  | 1       | 1889  | 0     | 5.18   |
| Samsung   | HE103SJ            | 1 TB   | 1       | 1865  | 0     | 5.11   |
| WDC       | WD7500AAKS-22RBA0  | 752 GB | 1       | 1816  | 0     | 4.98   |
| Toshiba   | MK3255GSXF         | 320 GB | 1       | 1812  | 0     | 4.97   |
| Seagate   | ST3300622AS        | 304 GB | 1       | 1806  | 0     | 4.95   |
| WDC       | WD360GD-00FNA0     | 37 GB  | 2       | 2599  | 1     | 4.95   |
| WDC       | WD3200AAJS-65M0A0  | 320 GB | 2       | 2312  | 4     | 4.93   |
| WDC       | WD2500YS-70SHB1    | 250 GB | 1       | 1789  | 0     | 4.90   |
| Hitachi   | HUA721050KLA330    | 500 GB | 2       | 1774  | 0     | 4.86   |
| HGST      | HUS724020ALE640    | 2 TB   | 8       | 1770  | 0     | 4.85   |
| WDC       | WD2500JS-40MVB1    | 250 GB | 1       | 1763  | 0     | 4.83   |
| WDC       | WD2500KS-22MJB0    | 250 GB | 1       | 1734  | 0     | 4.75   |
| Seagate   | ST960813AS         | 64 GB  | 1       | 1729  | 0     | 4.74   |
| WDC       | WD4000AAJS-22YFA0  | 400 GB | 1       | 1725  | 0     | 4.73   |
| Samsung   | HE103UJ            | 1 TB   | 1       | 1723  | 0     | 4.72   |
| WDC       | WD2502ABYS-01B7A0  | 256 GB | 3       | 2375  | 1     | 4.69   |
| WDC       | WD400JB-00ENA0     | 40 GB  | 3       | 2383  | 6     | 4.69   |
| HGST      | HTE541515A9E630    | 1.5 TB | 1       | 1702  | 0     | 4.66   |
| WDC       | WD3200JS-55PDB0    | 320 GB | 1       | 1698  | 0     | 4.65   |
| Samsung   | SP0411N            | 40 GB  | 2       | 3755  | 9     | 4.62   |
| Hitachi   | HDS724040ALE640    | 4 TB   | 3       | 1910  | 454   | 4.58   |
| WDC       | WD1600JS-88MHB0    | 160 GB | 1       | 1667  | 0     | 4.57   |
| WDC       | WD30EFRX-68AX9N0   | 3 TB   | 24      | 1927  | 2     | 4.54   |
| WDC       | WD3000HLFS-01G6U4  | 304 GB | 2       | 1654  | 0     | 4.53   |
| WDC       | WD3200AAJS-22RYA0  | 320 GB | 3       | 1653  | 0     | 4.53   |
| WDC       | WD6400AAKS-00H2B1  | 640 GB | 1       | 1653  | 0     | 4.53   |
| Seagate   | ST500DM002-1ER14C  | 500 GB | 2       | 1632  | 0     | 4.47   |
| HP        | FB080C4080         | 80 GB  | 1       | 1630  | 0     | 4.47   |
| Seagate   | ST3200021A         | 200 GB | 1       | 1624  | 0     | 4.45   |
| Maxtor    | 6V300F0            | 304 GB | 1       | 1613  | 0     | 4.42   |
| WDC       | WD7500AYYS-01RCA0  | 752 GB | 5       | 1678  | 1     | 4.39   |
| WDC       | WD1600JB-22GVA0    | 160 GB | 1       | 1600  | 0     | 4.39   |
| WDC       | WD1002FBYS-02A6B0  | 1 TB   | 9       | 1720  | 1     | 4.37   |
| Seagate   | ST4000NM0024-1H... | 4 TB   | 2       | 1595  | 0     | 4.37   |
| WDC       | WD2000JB-16FUA0    | 200 GB | 1       | 1584  | 0     | 4.34   |
| WDC       | WD3200AAVS-00ZTB0  | 320 GB | 1       | 1583  | 0     | 4.34   |
| Apple     | HDD HTS727575A9... | 752 GB | 1       | 1579  | 0     | 4.33   |
| Toshiba   | MQ01ABD032V        | 320 GB | 1       | 1578  | 0     | 4.33   |
| Hitachi   | HDS723030ALA640    | 3 TB   | 11      | 1699  | 9     | 4.22   |
| WDC       | WD6401AALS-00E8B0  | 640 GB | 2       | 1538  | 0     | 4.21   |
| WDC       | WD4000AAJS-65TKA0  | 400 GB | 1       | 1532  | 0     | 4.20   |
| WDC       | WD2502ABYS-23B7... | 250 GB | 2       | 1522  | 0     | 4.17   |
| Hitachi   | HUA723030ALA640    | 3 TB   | 11      | 1507  | 1     | 4.09   |
| HP        | GB1000EAMYC        | 1 TB   | 1       | 1490  | 0     | 4.08   |
| Quantum   | FIREBALLlct10 05   | 5 GB   | 1       | 1486  | 0     | 4.07   |
| WDC       | WD1200JS-55NCB1    | 120 GB | 1       | 1484  | 0     | 4.07   |
| WDC       | WD2000JD-00GBB0    | 200 GB | 1       | 1482  | 0     | 4.06   |
| WDC       | WD3200AAKX-753CA0  | 320 GB | 1       | 1471  | 0     | 4.03   |
| Seagate   | MB3000EBKAB        | 3 TB   | 2       | 1447  | 0     | 3.97   |
| Toshiba   | MK1002TSKB         | 1 TB   | 1       | 1446  | 0     | 3.96   |
| WDC       | WD10EADS-65M2B0    | 1 TB   | 3       | 1834  | 5     | 3.90   |
| WDC       | WD20NMVW-11EDZS2   | 2 TB   | 1       | 1422  | 0     | 3.90   |
| Hitachi   | HDT722520DLAT80    | 200 GB | 2       | 1406  | 0     | 3.85   |
| WDC       | WD2500JB-22REA0    | 250 GB | 1       | 1398  | 0     | 3.83   |
| Seagate   | ST500LM024-1RS152  | 500 GB | 1       | 1394  | 0     | 3.82   |
| WDC       | WD2001FASS-00W2B0  | 2 TB   | 1       | 1392  | 0     | 3.82   |
| WDC       | WD1500HLFS-01G6U3  | 150 GB | 2       | 1388  | 0     | 3.80   |
| HGST      | HDN726060ALE610    | 6 TB   | 8       | 1383  | 0     | 3.79   |
| WDC       | WD20NMVW-11W68S0   | 2 TB   | 2       | 1381  | 0     | 3.79   |
| HP        | MB2000GCWDA        | 2 TB   | 1       | 1370  | 0     | 3.76   |
| WDC       | WD1500HLFS-01G6U0  | 150 GB | 3       | 1403  | 1     | 3.75   |
| WDC       | WD2500AAJS-22RYA0  | 250 GB | 1       | 1365  | 0     | 3.74   |
| WDC       | WD7500BPVT-80HXZT1 | 752 GB | 1       | 1360  | 0     | 3.73   |
| WDC       | WD3200AAJB-00WGA0  | 320 GB | 2       | 1356  | 0     | 3.72   |
| WDC       | WD20EARS-07MVWB0   | 2 TB   | 4       | 1865  | 1     | 3.71   |
| WDC       | WD3003FZEX-00Z4SA0 | 3 TB   | 2       | 1333  | 0     | 3.65   |
| WDC       | WD2500JS-00MHB0    | 250 GB | 4       | 1325  | 0     | 3.63   |
| Fujitsu   | MPE3064AT          | 6 GB   | 2       | 1315  | 0     | 3.60   |
| WDC       | WD2000FYYZ-01UL1B2 | 2 TB   | 2       | 1314  | 0     | 3.60   |
| Seagate   | ST91000640NS       | 1 TB   | 12      | 1426  | 2     | 3.60   |
| WDC       | WD2500AAKX-08ERMA0 | 250 GB | 1       | 1306  | 0     | 3.58   |
| WDC       | WD2500AAKS-22VSA0  | 250 GB | 1       | 1305  | 0     | 3.58   |
| Maxtor    | STM380215A         | 80 GB  | 3       | 1701  | 614   | 3.57   |
| Hitachi   | HDS722020ALA330    | 2 TB   | 23      | 1649  | 12    | 3.54   |
| WDC       | WD1200BB-00GUA0    | 120 GB | 1       | 1284  | 0     | 3.52   |
| WDC       | WD3000F9YZ-09N20L0 | 3 TB   | 4       | 1902  | 2     | 3.52   |
| WDC       | WD1001FALS-75J7B0  | 1 TB   | 2       | 1485  | 4     | 3.52   |
| Hitachi   | HTS721010G9SA00    | 100 GB | 1       | 1283  | 0     | 3.52   |
| WDC       | WD2000BB-22GUC0    | 200 GB | 1       | 1282  | 0     | 3.51   |
| Hitachi   | HDS5C3015ALA632    | 1.5 TB | 3       | 1462  | 107   | 3.51   |
| Hitachi   | HCS5C3232SLA380    | 320 GB | 1       | 1281  | 0     | 3.51   |
| WDC       | WD4000AAKS-00A7B0  | 400 GB | 1       | 1280  | 0     | 3.51   |
| WDC       | WD3000FYYZ-50UL1B0 | 3 TB   | 1       | 1278  | 0     | 3.50   |
| WDC       | WD15EVDS-68V9B0    | 1.5 TB | 1       | 1276  | 0     | 3.50   |
| HP        | J7989G             | 80 GB  | 1       | 1274  | 0     | 3.49   |
| WDC       | WD2003FYYS-02W0B1  | 2 TB   | 2       | 1290  | 3     | 3.49   |
| HGST      | HMS5C4040BLE640    | 4 TB   | 5       | 1272  | 0     | 3.49   |
| WDC       | WD6400AACS-00G8B0  | 640 GB | 3       | 1253  | 0     | 3.43   |
| Toshiba   | DT01ABA300         | 3 TB   | 1       | 1247  | 0     | 3.42   |
| WDC       | WD5000AAKS-00TMA0  | 500 GB | 7       | 1371  | 2     | 3.41   |
| WDC       | WD1600AABS-61PRA0  | 160 GB | 2       | 1750  | 1     | 3.41   |
| Samsung   | SP0451N            | 40 GB  | 1       | 1237  | 0     | 3.39   |
| Hitachi   | HDS721075KLA330    | 752 GB | 7       | 1493  | 14    | 3.31   |
| Hitachi   | HDT721075SLA380    | 752 GB | 1       | 1205  | 0     | 3.30   |
| WDC       | WD10EADS-00L5B1    | 1 TB   | 40      | 1582  | 4     | 3.30   |
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
| HGST      | HUS724030ALA640    | 3 TB   | 12      | 1281  | 2     | 3.19   |
| WDC       | WD1500AHFD-00RAR5  | 150 GB | 1       | 1164  | 0     | 3.19   |
| WDC       | WD5000AVJB-63YUA0  | 500 GB | 1       | 1163  | 0     | 3.19   |
| Toshiba   | MK8017GSG          | 80 GB  | 1       | 1162  | 0     | 3.18   |
| WDC       | WD4000AAKS-00YGA0  | 400 GB | 5       | 1249  | 1     | 3.18   |
| WDC       | WD1001FALS-41Y6A0  | 1 TB   | 3       | 1345  | 1     | 3.17   |
| WDC       | WD2503ABYX-01WERA0 | 256 GB | 1       | 1155  | 0     | 3.16   |
| WDC       | WD1001FALS-00J7B0  | 1 TB   | 11      | 1153  | 0     | 3.16   |
| WDC       | WD20EARX-22PASB0   | 2 TB   | 2       | 1153  | 0     | 3.16   |
| WDC       | WD1001FALS-00E3A0  | 1 TB   | 5       | 1273  | 1     | 3.14   |
| Toshiba   | DT01ABA200         | 2 TB   | 8       | 1145  | 0     | 3.14   |
| Seagate   | ST3400832AS        | 400 GB | 1       | 3418  | 2     | 3.12   |
| WDC       | WD2500AAJS-22VWA0  | 250 GB | 2       | 1138  | 0     | 3.12   |
| WDC       | WD740ADFD-00NLR1   | 74 GB  | 2       | 1137  | 0     | 3.12   |
| WDC       | WD20EARX-008FB0    | 2 TB   | 9       | 1244  | 2     | 3.11   |
| WDC       | WD5003AZEX-00RKKA0 | 500 GB | 2       | 1135  | 0     | 3.11   |
| Toshiba   | MG03ACA200         | 2 TB   | 1       | 1134  | 0     | 3.11   |
| WDC       | MB0500EBNCR        | 500 GB | 1       | 1134  | 0     | 3.11   |
| WDC       | WD50EZRZ-32RWYB1   | 5 TB   | 2       | 1128  | 0     | 3.09   |
| Seagate   | ST4000VN0001-1S... | 4 TB   | 3       | 1128  | 0     | 3.09   |
| Hitachi   | HDS723020BLA642    | 2 TB   | 39      | 1362  | 87    | 3.09   |
| Samsung   | HD400LD            | 400 GB | 4       | 1126  | 0     | 3.09   |
| Seagate   | ST3320820AS_Q      | 320 GB | 1       | 1125  | 0     | 3.08   |
| WDC       | WD3200AAJS-40VWA0  | 320 GB | 1       | 1118  | 0     | 3.06   |
| Seagate   | ST3250820SCE       | 250 GB | 3       | 1116  | 0     | 3.06   |
| WDC       | WD2002FYPS-02W3B0  | 2 TB   | 2       | 1108  | 0     | 3.04   |
| WDC       | WD7500AACS-00D6B0  | 752 GB | 1       | 1107  | 0     | 3.03   |
| Hitachi   | HDS7250SASUN500... | 500 GB | 1       | 1103  | 0     | 3.02   |
| WDC       | WD10EARS-67Y5B1    | 1 TB   | 1       | 1100  | 0     | 3.01   |
| WDC       | WD2002FAEX-00MJRA0 | 2 TB   | 1       | 1094  | 0     | 3.00   |
| WDC       | WD1200JS-00SGB0    | 120 GB | 2       | 1091  | 0     | 2.99   |
| WDC       | WD3200KS-75PFB0    | 320 GB | 2       | 1359  | 39    | 2.98   |
| Seagate   | ST3360320AS        | 360 GB | 4       | 1352  | 1     | 2.98   |
| Seagate   | ST9500620NS 81Y... | 500 GB | 1       | 1083  | 0     | 2.97   |
| Hitachi   | HDS728040PLA320    | 40 GB  | 3       | 1579  | 6     | 2.97   |
| WDC       | WD7500AARX-00N0YB0 | 752 GB | 1       | 1081  | 0     | 2.96   |
| WDC       | WD30EURX-64HYZY0   | 3 TB   | 1       | 1077  | 0     | 2.95   |
| Maxtor    | 7V250F0            | 256 GB | 2       | 1075  | 0     | 2.95   |
| HGST      | HTS721050A9E630    | 500 GB | 1       | 1069  | 0     | 2.93   |
| Hitachi   | HUA723020ALA640    | 2 TB   | 11      | 1068  | 0     | 2.93   |
| WDC       | WD1600YS-01SHB1    | 164 GB | 6       | 1060  | 0     | 2.91   |
| WDC       | WD6400AACS-00D6B1  | 640 GB | 1       | 1058  | 0     | 2.90   |
| WDC       | WD7500AAKS-00RBA0  | 752 GB | 8       | 1153  | 63    | 2.90   |
| WDC       | WD2500JS-00MHB1    | 250 GB | 2       | 1052  | 0     | 2.88   |
| HGST      | MB6000GEBTP        | 6 TB   | 1       | 1046  | 0     | 2.87   |
| WDC       | WD2500JS-22NCB1    | 250 GB | 8       | 1153  | 1     | 2.87   |
| WDC       | WD3200JD-00KLB0    | 320 GB | 1       | 1045  | 0     | 2.87   |
| Samsung   | HD204UI            | 2 TB   | 30      | 1215  | 66    | 2.84   |
| WDC       | WD800BB-75FRA0     | 80 GB  | 2       | 1034  | 0     | 2.83   |
| Seagate   | ST340823A          | 40 GB  | 1       | 1034  | 0     | 2.83   |
| WDC       | WD1600JB-00REA0    | 160 GB | 8       | 1147  | 4     | 2.83   |
| Hitachi   | HDS721016CLA382    | 160 GB | 5       | 1062  | 1     | 2.82   |
| WDC       | WD800BB-22JHA0     | 80 GB  | 2       | 1029  | 0     | 2.82   |
| WDC       | WD1001FALS-403AA0  | 1 TB   | 2       | 1025  | 0     | 2.81   |
| WDC       | WD800AAJS-75M0A0   | 80 GB  | 2       | 1114  | 4     | 2.81   |
| Hitachi   | HDT725040VLA360    | 400 GB | 2       | 1024  | 0     | 2.81   |
| Seagate   | ST32000644NS       | 2 TB   | 4       | 1258  | 34    | 2.80   |
| WDC       | WD4NPURX-64TPFY0   | 4 TB   | 1       | 1023  | 0     | 2.80   |
| WDC       | WD2500JB-57REA0    | 250 GB | 1       | 1021  | 0     | 2.80   |
| HP        | GB0250EAFYK        | 250 GB | 2       | 1519  | 67    | 2.79   |
| WDC       | WD3200AAJS-56B4A0  | 320 GB | 4       | 1441  | 2     | 2.79   |
| WDC       | WD400LB-00DNA0     | 40 GB  | 2       | 1103  | 2     | 2.78   |
| WDC       | WD200BB-00DEA0     | 20 GB  | 1       | 1015  | 0     | 2.78   |
| WDC       | WD5000AACS-61M6B2  | 500 GB | 3       | 2013  | 4     | 2.78   |
| WDC       | WD1600JB-00EVA0    | 160 GB | 1       | 1012  | 0     | 2.77   |
| WDC       | WD1200JD-00HBB0    | 120 GB | 6       | 1414  | 70    | 2.77   |
| Toshiba   | MC04ACA200E        | 2 TB   | 1       | 1008  | 0     | 2.76   |
| Seagate   | ST320LT023-1AF142  | 320 GB | 1       | 1007  | 0     | 2.76   |
| WDC       | WD3200AAKS-00G3A0  | 320 GB | 6       | 1006  | 0     | 2.76   |
| WDC       | WD20NMVW-59AV3S3   | 2 TB   | 1       | 1005  | 0     | 2.75   |
| WDC       | WD2000JS-22MHB0    | 200 GB | 4       | 1909  | 10    | 2.74   |
| Seagate   | ST3250823AS        | 250 GB | 13      | 1543  | 21    | 2.74   |
| WDC       | WD30EZRX-00DC0B0   | 3 TB   | 22      | 997   | 1     | 2.72   |
| WDC       | WD1000FYPS-01ZKB0  | 1 TB   | 1       | 989   | 0     | 2.71   |
| WDC       | WD3200BEKT-00PVMT0 | 320 GB | 2       | 985   | 0     | 2.70   |
| WDC       | WD5000AAKS-00C8A0  | 500 GB | 3       | 1253  | 62    | 2.70   |
| WDC       | WD2500JS-55NCB1    | 250 GB | 5       | 1231  | 8     | 2.70   |
| WDC       | WD3200AAKX-221CA0  | 320 GB | 1       | 981   | 0     | 2.69   |
| WDC       | WD2500BEVS-00UST0  | 250 GB | 1       | 981   | 0     | 2.69   |
| WDC       | WD400JB-00JJC0     | 40 GB  | 1       | 980   | 0     | 2.69   |
| Samsung   | HD040GJ-P          | 40 GB  | 1       | 975   | 0     | 2.67   |
| WDC       | WD800JD-60LSA5     | 80 GB  | 17      | 1020  | 2     | 2.67   |
| Seagate   | ST8000AS0002-1N... | 8 TB   | 19      | 974   | 0     | 2.67   |
| WDC       | WD5000AAKS-07YGA0  | 500 GB | 3       | 971   | 0     | 2.66   |
| WDC       | WD10EALX-079BA1    | 1 TB   | 1       | 968   | 0     | 2.65   |
| WDC       | WD5000BMVV-11GNWS0 | 500 GB | 2       | 967   | 0     | 2.65   |
| WDC       | WD10EADS-00P8B0    | 1 TB   | 5       | 1231  | 3     | 2.64   |
| Toshiba   | MK4032GAX          | 40 GB  | 1       | 960   | 0     | 2.63   |
| WDC       | WD2000JS-00MVB1    | 200 GB | 1       | 957   | 0     | 2.62   |
| WDC       | WD7502AAEX-00Z3A0  | 752 GB | 1       | 956   | 0     | 2.62   |
| WDC       | WD5000AAKS-22YGA0  | 500 GB | 4       | 1326  | 115   | 2.62   |
| Hitachi   | HDS5C1010CLA382    | 1 TB   | 7       | 954   | 0     | 2.61   |
| Toshiba   | MQ01UBB200         | 2 TB   | 4       | 952   | 0     | 2.61   |
| WDC       | WD800BEVT-00ZCT0   | 80 GB  | 1       | 951   | 0     | 2.61   |
| WDC       | WD1600BB-22RDA0    | 160 GB | 2       | 947   | 0     | 2.60   |
| Quantum   | FIREBALLP AS20.5   | 20 GB  | 1       | 946   | 0     | 2.59   |
| WDC       | WD10EADS-11M2B3    | 1 TB   | 2       | 940   | 0     | 2.58   |
| WDC       | WD50EZRX-00MVLB1   | 5 TB   | 2       | 940   | 0     | 2.58   |
| WDC       | WD1001FALS-41Y6A1  | 1 TB   | 1       | 938   | 0     | 2.57   |
| WDC       | WD5002ABYS-02B1B0  | 500 GB | 9       | 1214  | 2     | 2.57   |
| WDC       | WD1600JS-55NCB1    | 160 GB | 4       | 935   | 0     | 2.56   |
| WDC       | WD5000AAKB-00YSA0  | 500 GB | 2       | 935   | 0     | 2.56   |
| WDC       | WD5000LUCT-63C26Y0 | 500 GB | 1       | 934   | 0     | 2.56   |
| Seagate   | ST4000DM000-1F2168 | 4 TB   | 45      | 972   | 23    | 2.56   |
| HGST      | HDN724030ALE640    | 3 TB   | 5       | 929   | 0     | 2.55   |
| WDC       | WD10EADS-00M2B0    | 1 TB   | 33      | 1254  | 105   | 2.54   |
| WDC       | WD2002FAEX-007BA0  | 2 TB   | 20      | 1142  | 2     | 2.53   |
| WDC       | WD800JB-00DUA3     | 80 GB  | 1       | 923   | 0     | 2.53   |
| WDC       | WD5000AAKS-00YGA0  | 500 GB | 20      | 1116  | 3     | 2.53   |
| WDC       | WD2500BEVS-26VAT0  | 250 GB | 1       | 920   | 0     | 2.52   |
| WDC       | WD1600BB-56RDA0    | 160 GB | 2       | 916   | 0     | 2.51   |
| WDC       | WD10EACS-00ZJB0    | 1 TB   | 6       | 1607  | 54    | 2.51   |
| WDC       | WD2500AAJS-75M0A0  | 250 GB | 3       | 915   | 0     | 2.51   |
| WDC       | WD5000AAVS-00G9B0  | 500 GB | 3       | 1348  | 3     | 2.51   |
| Hitachi   | HDT725032VLA380    | 320 GB | 10      | 1322  | 117   | 2.51   |
| WDC       | WD3200AAKX-603CA0  | 320 GB | 1       | 914   | 0     | 2.51   |
| WDC       | WD1003FBYX-01Y7B0  | 1 TB   | 8       | 1302  | 2     | 2.50   |
| Seagate   | ST3300622A         | 304 GB | 1       | 912   | 0     | 2.50   |
| WDC       | WD15EARS-00J2GB0   | 1.5 TB | 1       | 908   | 0     | 2.49   |
| WDC       | WD10EUCX-73YZ1Y0   | 1 TB   | 1       | 907   | 0     | 2.49   |
| HGST      | HDN724040ALE640    | 4 TB   | 9       | 906   | 0     | 2.48   |
| Seagate   | ST3400833AS        | 400 GB | 1       | 905   | 0     | 2.48   |
| Seagate   | ST4000VN000-1H4168 | 4 TB   | 15      | 997   | 135   | 2.48   |
| WDC       | WD1600BB-00RDA0    | 160 GB | 4       | 1124  | 20    | 2.47   |
| WDC       | WD800BEVS-08RST3   | 80 GB  | 1       | 900   | 0     | 2.47   |
| WDC       | WD400BB-71DGA0     | 40 GB  | 1       | 900   | 0     | 2.47   |
| WDC       | WD5000AACS-00ZUB0  | 500 GB | 10      | 934   | 1     | 2.46   |
| Seagate   | ST32000641AS       | 2 TB   | 10      | 1052  | 161   | 2.45   |
| WDC       | WD800BB-22HEA1     | 80 GB  | 1       | 888   | 0     | 2.43   |
| HGST      | HTE541010A9E680    | 1 TB   | 2       | 913   | 509   | 2.43   |
| WDC       | WD2500AAJS-55RYA0  | 250 GB | 2       | 887   | 0     | 2.43   |
| WDC       | WD3200AAJB-00TYA0  | 320 GB | 4       | 885   | 0     | 2.43   |
| WDC       | WD5001ABYS-01YNA0  | 500 GB | 2       | 884   | 0     | 2.42   |
| WDC       | WD1001FALS-00J7B1  | 1 TB   | 17      | 1027  | 2     | 2.42   |
| WDC       | WD4000KS-00MNB0    | 400 GB | 3       | 883   | 0     | 2.42   |
| Seagate   | ST91000640NS 81... | 1 TB   | 1       | 883   | 0     | 2.42   |
| Seagate   | ST3300831AS        | 304 GB | 3       | 1808  | 4     | 2.42   |
| WDC       | WD2500AAJS-75VWA0  | 250 GB | 1       | 880   | 0     | 2.41   |
| WDC       | WD1600AAJS-75WAA0  | 160 GB | 2       | 880   | 0     | 2.41   |
| Seagate   | ST3250620NS        | 250 GB | 17      | 1382  | 289   | 2.41   |
| Hitachi   | HDT722520DLA380    | 200 GB | 4       | 1091  | 2     | 2.40   |
| WDC       | WD30EZRS-42KEZB0   | 3 TB   | 1       | 874   | 0     | 2.40   |
| Toshiba   | MQ01ABF050H        | 500 GB | 2       | 873   | 0     | 2.39   |
| Hitachi   | HDS5C3020ALA632    | 2 TB   | 14      | 992   | 2     | 2.39   |
| WDC       | WD800BB-75JHA0     | 80 GB  | 1       | 865   | 0     | 2.37   |
| WDC       | WD15EARS-00S8B1    | 1.5 TB | 3       | 1320  | 3     | 2.37   |
| HP        | MB1000EBZQB        | 1 TB   | 1       | 863   | 0     | 2.37   |
| WDC       | WD3202ABYS-02B7A0  | 320 GB | 6       | 929   | 1     | 2.36   |
| Seagate   | ST1000LX001-1EM164 | 1 TB   | 1       | 857   | 0     | 2.35   |
| WDC       | WD800JD-75MSA3     | 80 GB  | 23      | 990   | 1     | 2.35   |
| WDC       | WD800AAJS-22PSA0   | 80 GB  | 4       | 852   | 0     | 2.33   |
| Seagate   | ST3500630A         | 500 GB | 7       | 1381  | 33    | 2.33   |
| Seagate   | ST3802110AS        | 80 GB  | 3       | 851   | 0     | 2.33   |
| Hitachi   | HDS721612PLA380    | 120 GB | 8       | 1294  | 3     | 2.33   |
| Hitachi   | HCS5C1050CLA382    | 500 GB | 1       | 848   | 0     | 2.33   |
| WDC       | WD10EZEX-08RKKA0   | 1 TB   | 6       | 848   | 0     | 2.32   |
| Hitachi   | HDT725025VLA380    | 250 GB | 15      | 1035  | 34    | 2.32   |
| WDC       | WD5002ABYS-01B1B0  | 500 GB | 12      | 1238  | 3     | 2.32   |
| WDC       | WD1600AAJS-22PSA0  | 160 GB | 14      | 937   | 3     | 2.32   |
| Seagate   | ST32000645NS       | 2 TB   | 8       | 1309  | 11    | 2.30   |
| Hitachi   | HTS723216L9SA60    | 160 GB | 4       | 838   | 0     | 2.30   |
| WDC       | WD800BB-00DKA0     | 80 GB  | 3       | 977   | 1     | 2.29   |
| WDC       | WD10EALX-089BA0    | 1 TB   | 2       | 836   | 0     | 2.29   |
| WDC       | WD20NPVX-00EA4T0   | 2 TB   | 2       | 836   | 0     | 2.29   |
| WDC       | WD2502ABYS-18B7A0  | 250 GB | 4       | 1251  | 3     | 2.29   |
| WDC       | WD1600JS-60MHB1    | 160 GB | 7       | 974   | 4     | 2.28   |
| WDC       | WD30EZRX-00MMMB0   | 3 TB   | 14      | 1000  | 2     | 2.27   |
| Seagate   | ST3500630AS        | 500 GB | 33      | 1296  | 274   | 2.27   |
| WDC       | WD10EADS-11M2B2    | 1 TB   | 2       | 1619  | 4     | 2.27   |
| WDC       | WD10EAVS-00D7B0    | 1 TB   | 5       | 828   | 0     | 2.27   |
| Seagate   | ST3750840AS        | 752 GB | 1       | 828   | 0     | 2.27   |
| WDC       | WD1600BEVS-08VAT2  | 160 GB | 6       | 901   | 1     | 2.26   |
| WDC       | WD400BB-00DEA0     | 40 GB  | 1       | 825   | 0     | 2.26   |
| WDC       | WD800BD-88JMC0     | 80 GB  | 2       | 824   | 0     | 2.26   |
| WDC       | WD1003FZEX-00RLFA0 | 1 TB   | 2       | 823   | 0     | 2.26   |
| Hitachi   | HDS728040PLAT20    | 41 GB  | 5       | 979   | 1     | 2.25   |
| WDC       | WD1600JB-00GVA0    | 160 GB | 1       | 822   | 0     | 2.25   |
| WDC       | WD2500BEVE-00WZT0  | 250 GB | 2       | 817   | 0     | 2.24   |
| WDC       | WD400BB-00LNA0     | 40 GB  | 1       | 817   | 0     | 2.24   |
| Hitachi   | HDT725050VLA380    | 500 GB | 2       | 1307  | 19    | 2.24   |
| WDC       | WD5001AALS-00E3A0  | 500 GB | 12      | 1007  | 97    | 2.23   |
| WDC       | WD1500HLFS-01G6U1  | 150 GB | 3       | 813   | 0     | 2.23   |
| WDC       | WD30EFRX-68EUZN0   | 3 TB   | 60      | 983   | 2     | 2.23   |
| WDC       | WD1600AAJS-07M0A0  | 160 GB | 6       | 1280  | 3     | 2.23   |
| WDC       | WD2500JB-00GVC0    | 250 GB | 2       | 811   | 0     | 2.22   |
| HGST      | HUS726040ALA610    | 4 TB   | 2       | 810   | 0     | 2.22   |
| Seagate   | ST4000LM016-1N2170 | 4 TB   | 1       | 807   | 0     | 2.21   |
| WDC       | WD10EACS-00D6B0    | 1 TB   | 6       | 1303  | 6     | 2.21   |
| Seagate   | ST3120213AS        | 120 GB | 1       | 806   | 0     | 2.21   |
| Samsung   | HD160JJ-P          | 160 GB | 9       | 1347  | 676   | 2.21   |
| Hitachi   | HTS723232L9SA62    | 320 GB | 1       | 804   | 0     | 2.20   |
| WDC       | WD1502FAEX-007BA0  | 1.5 TB | 7       | 872   | 25    | 2.19   |
| WDC       | WD3200AAKS-75SBA0  | 320 GB | 1       | 798   | 0     | 2.19   |
| Seagate   | ST5000DM000-1FK178 | 5 TB   | 10      | 906   | 175   | 2.19   |
| WDC       | WD20EARS-00S8B1    | 2 TB   | 10      | 1124  | 2     | 2.18   |
| WDC       | WD1600JS-75NCB3    | 160 GB | 4       | 797   | 0     | 2.18   |
| WDC       | WD3200AAKS-22B3A0  | 320 GB | 2       | 797   | 0     | 2.18   |
| Seagate   | ST1500LM003-9YH148 | 1.5 TB | 1       | 796   | 0     | 2.18   |
| Fujitsu   | MHV2060AH PL       | 64 GB  | 2       | 796   | 0     | 2.18   |
| WDC       | WD6400AAKS-00A7B0  | 640 GB | 13      | 992   | 4     | 2.18   |
| WDC       | WD6400AACS-00G8B1  | 640 GB | 7       | 1069  | 4     | 2.17   |
| WDC       | WD2500YS-01SHB1    | 250 GB | 7       | 1083  | 1     | 2.17   |
| WDC       | WD2003FYYS-02W0B0  | 2 TB   | 5       | 1074  | 1     | 2.17   |
| WDC       | WD1005FBYZ-01YCBB1 | 1 TB   | 4       | 790   | 0     | 2.17   |
| WDC       | WD7500AALX-009BA0  | 752 GB | 7       | 789   | 0     | 2.16   |
| Seagate   | ST3400620A         | 400 GB | 4       | 1479  | 143   | 2.16   |
| WDC       | WD1002FAEX-00Y9A0  | 1 TB   | 39      | 919   | 20    | 2.16   |
| WDC       | WD5000AAJS-22TKA0  | 500 GB | 2       | 788   | 0     | 2.16   |
| WDC       | WD5000BPKX-75HPJT0 | 500 GB | 2       | 787   | 0     | 2.16   |
| WDC       | WD3200BEKT-75PVMT1 | 320 GB | 2       | 786   | 0     | 2.16   |
| WDC       | WD1600AAJB-00WRA0  | 160 GB | 3       | 1002  | 362   | 2.15   |
| WDC       | WD2500JS-60NCB1    | 250 GB | 7       | 886   | 1     | 2.15   |
| WDC       | WD1003FBYX-05Y7B0  | 1 TB   | 1       | 785   | 0     | 2.15   |
| WDC       | WD1600AAJS-07WAA0  | 160 GB | 5       | 1143  | 170   | 2.15   |
| WDC       | WD800JD-75MSA2     | 80 GB  | 2       | 783   | 0     | 2.15   |
| WDC       | WD1002FAEX-007BA0  | 1 TB   | 3       | 853   | 1     | 2.15   |
| Seagate   | ST6000DM001-1XY17Z | 6 TB   | 1       | 783   | 0     | 2.15   |
| Seagate   | ST6000VN0021-1Z... | 6 TB   | 1       | 783   | 0     | 2.15   |
| WDC       | WD6001FFWX-68Z39N0 | 6 TB   | 1       | 782   | 0     | 2.14   |
| WDC       | WD5000AADS-56S9B0  | 500 GB | 1       | 782   | 0     | 2.14   |
| WDC       | WD7501AALS-00J7B1  | 752 GB | 9       | 976   | 1     | 2.14   |
| Seagate   | ST91603110CS       | 160 GB | 1       | 781   | 0     | 2.14   |
| Seagate   | ST3000VN000-1HJ166 | 3 TB   | 5       | 780   | 0     | 2.14   |
| Hitachi   | HDS723020BLE640    | 2 TB   | 10      | 780   | 0     | 2.14   |
| WDC       | WD800JD-00HKA0     | 80 GB  | 3       | 849   | 2     | 2.14   |
| WDC       | WD1600AAJS-60PSA0  | 160 GB | 4       | 950   | 257   | 2.13   |
| WDC       | WD400BD-75MRA1     | 40 GB  | 3       | 777   | 0     | 2.13   |
| WDC       | WD6400AAKS-00A7B2  | 640 GB | 6       | 776   | 0     | 2.13   |
| WDC       | WD1200JB-00DUA3    | 120 GB | 2       | 1239  | 2     | 2.13   |
| WDC       | WD10EARX-32N0YB0   | 1 TB   | 3       | 799   | 5     | 2.13   |
| WDC       | WD2500BB-00GUA0    | 250 GB | 1       | 773   | 0     | 2.12   |
| WDC       | WD2500JS-60NCB2    | 250 GB | 2       | 773   | 0     | 2.12   |
| WDC       | WD2500JS-00NCB1    | 250 GB | 10      | 1117  | 34    | 2.12   |
| Hitachi   | HTS723225L9A362    | 250 GB | 1       | 770   | 0     | 2.11   |
| Samsung   | HD083GJ            | 80 GB  | 4       | 769   | 0     | 2.11   |
| WDC       | WD1600AAJS-07PSA0  | 160 GB | 3       | 1618  | 9     | 2.10   |
| WDC       | WD6401AALS-00L3B2  | 640 GB | 18      | 1093  | 6     | 2.10   |
| WDC       | WD10EALS-002BA0    | 1 TB   | 3       | 766   | 0     | 2.10   |
| Hitachi   | HTS723232L9A362    | 320 GB | 1       | 763   | 0     | 2.09   |
| WDC       | WD3200AAKX-083CA1  | 320 GB | 1       | 763   | 0     | 2.09   |
| WDC       | WD7501AALS-00E8B0  | 752 GB | 4       | 1396  | 4     | 2.09   |
| Samsung   | HD040GJ            | 40 GB  | 5       | 959   | 25    | 2.09   |
| WDC       | WD2500JD-55HBB0    | 250 GB | 2       | 1468  | 16    | 2.07   |
| WDC       | WD7501AALS-00J7B0  | 752 GB | 16      | 1063  | 56    | 2.07   |
| WDC       | WD1002FAEX-00Z3A0  | 1 TB   | 62      | 1006  | 85    | 2.07   |
| WDC       | WD8001FFWX-68J1UN0 | 8 TB   | 2       | 753   | 0     | 2.06   |
| WDC       | WD3000JS-19PDB0    | 304 GB | 1       | 751   | 0     | 2.06   |
| WDC       | WD3001FFSX-68JNUN0 | 3 TB   | 1       | 747   | 0     | 2.05   |
| WDC       | WD30EZRX-00SPEB0   | 3 TB   | 9       | 747   | 0     | 2.05   |
| Seagate   | ST340212AS         | 40 GB  | 3       | 1192  | 70    | 2.05   |
| WDC       | WD400BB-60JKA0     | 40 GB  | 2       | 746   | 0     | 2.04   |
| Quantum   | FIREBALLP AS40.0   | 40 GB  | 1       | 744   | 0     | 2.04   |
| WDC       | WD10EURX-61C57Y0   | 1 TB   | 1       | 744   | 0     | 2.04   |
| Seagate   | ST3320620AS        | 320 GB | 113     | 1155  | 238   | 2.04   |
| WDC       | WD20EARX-00PASB0   | 2 TB   | 87      | 955   | 129   | 2.04   |
| WDC       | WD10EALX-759BA1    | 1 TB   | 6       | 1218  | 4     | 2.04   |
| HGST      | HUS724020ALA640    | 2 TB   | 16      | 741   | 0     | 2.03   |
| WDC       | WD6400AAKS-22A7B0  | 640 GB | 11      | 1058  | 3     | 2.03   |
| WDC       | WD6400AAKS-65Z7B0  | 640 GB | 6       | 859   | 5     | 2.02   |
| WDC       | WD2500AAJS-00VTA0  | 250 GB | 22      | 911   | 73    | 2.02   |
| ExcelStor | J9250S             | 250 GB | 4       | 735   | 0     | 2.01   |
| Samsung   | HD300LJ            | 304 GB | 9       | 1235  | 380   | 2.01   |
| WDC       | WD1200JB-00EVA0    | 120 GB | 4       | 731   | 0     | 2.00   |
| Seagate   | ST4000DM000-2AE166 | 4 TB   | 2       | 729   | 0     | 2.00   |
| Maxtor    | 7H500F0            | 500 GB | 1       | 726   | 0     | 1.99   |
| WDC       | WD5000AVDS-63U7B1  | 500 GB | 6       | 772   | 3     | 1.99   |
| WDC       | WD2500AAKX-221CA1  | 250 GB | 2       | 1139  | 4     | 1.99   |
| WDC       | WD2500KS-00MJB0    | 250 GB | 24      | 968   | 18    | 1.98   |
| Seagate   | ST9320421ASG       | 320 GB | 2       | 887   | 1     | 1.97   |
| Fujitsu   | MHV2100AH          | 100 GB | 2       | 719   | 0     | 1.97   |
| WDC       | WD6402AAEX-00Z3A0  | 640 GB | 3       | 719   | 0     | 1.97   |
| Seagate   | ST310211A          | 10 GB  | 1       | 716   | 0     | 1.96   |
| Hitachi   | HDS5C3030ALA630    | 3 TB   | 3       | 1083  | 1     | 1.96   |
| WDC       | WD15EADS-00S2B0    | 1.5 TB | 2       | 1647  | 10    | 1.96   |
| WDC       | WD1600JS-58NCB1    | 160 GB | 1       | 712   | 0     | 1.95   |
| Hitachi   | HTS545032B9SA00    | 320 GB | 5       | 944   | 462   | 1.95   |
| WDC       | WD800JD-00LSA0     | 80 GB  | 22      | 972   | 10    | 1.95   |
| Seagate   | ST1000VM002-9ZL162 | 1 TB   | 1       | 709   | 0     | 1.95   |
| Seagate   | ST2000DM001-1E6164 | 2 TB   | 2       | 709   | 0     | 1.94   |
| WDC       | WD200BB-32CFC0     | 20 GB  | 1       | 709   | 0     | 1.94   |
| WDC       | WD2500JS-75NCB3    | 250 GB | 4       | 1000  | 25    | 1.93   |
| WDC       | WD2500AAKX-083CA1  | 250 GB | 10      | 1064  | 3     | 1.93   |
| WDC       | WD30EZRX-00D8PB0   | 3 TB   | 18      | 743   | 1     | 1.93   |
| Seagate   | ST3160812AS        | 160 GB | 37      | 1032  | 318   | 1.92   |
| WDC       | WD2500AAKX-75U6AA0 | 250 GB | 6       | 785   | 1     | 1.92   |
| WDC       | WD3200AAJS-65B4A0  | 320 GB | 1       | 699   | 0     | 1.92   |
| WDC       | WD2003FZEX-00SRLA0 | 2 TB   | 22      | 718   | 1     | 1.91   |
| WDC       | WD2003FZEX-00Z4SA0 | 2 TB   | 16      | 791   | 2     | 1.91   |
| WDC       | WD5000AAKS-00A7B0  | 500 GB | 27      | 1117  | 8     | 1.91   |
| WDC       | WD6400BPVT-35HXZT1 | 640 GB | 2       | 696   | 0     | 1.91   |
| WDC       | WD2500LPVT-00G33T0 | 250 GB | 1       | 696   | 0     | 1.91   |
| WDC       | WD10JPVX-08JC3T5   | 1 TB   | 9       | 707   | 1     | 1.90   |
| WDC       | WD5000AAJS-00YFA0  | 500 GB | 5       | 884   | 33    | 1.90   |
| WDC       | WD3200AAJS-65VWA0  | 320 GB | 3       | 692   | 0     | 1.90   |
| WDC       | WD5000HHTZ-04N21V0 | 500 GB | 5       | 692   | 0     | 1.90   |
| WDC       | WD5000BMVW-11AMCS4 | 500 GB | 3       | 692   | 0     | 1.90   |
| WDC       | WD3200BEVE-00A0HT0 | 320 GB | 3       | 691   | 0     | 1.90   |
| WDC       | WD5000BMVW-11S5XS0 | 500 GB | 5       | 786   | 1     | 1.89   |
| WDC       | WD6400AAKS-65A7B0  | 640 GB | 5       | 787   | 3     | 1.89   |
| WDC       | WD2500BEKT-75PVMT1 | 250 GB | 1       | 689   | 0     | 1.89   |
| Hitachi   | HUS724030ALE641    | 3 TB   | 7       | 747   | 179   | 1.89   |
| WDC       | WD20NMVW-11AV3S2   | 2 TB   | 14      | 826   | 2     | 1.88   |
| WDC       | WD1001FALS-00Y6A0  | 1 TB   | 4       | 936   | 28    | 1.88   |
| WDC       | WD10EADX-22TDHB0   | 1 TB   | 6       | 757   | 2     | 1.88   |
| Seagate   | ST340215AS         | 40 GB  | 1       | 686   | 0     | 1.88   |
| WDC       | WD10EARS-22Y5B1    | 1 TB   | 12      | 962   | 22    | 1.88   |
| WDC       | WD5000AAKS-65YGA0  | 500 GB | 8       | 796   | 8     | 1.88   |
| WDC       | WD10EURX-63UY4Y0   | 1 TB   | 2       | 684   | 0     | 1.88   |
| Fujitsu   | MHZ2080BH G2       | 80 GB  | 1       | 684   | 0     | 1.88   |
| WDC       | WD30PURX-64P6ZY0   | 3 TB   | 4       | 683   | 0     | 1.87   |
| WDC       | WD40EZRX-00SPEB0   | 4 TB   | 21      | 780   | 3     | 1.87   |
| WDC       | WD10EACS-00D6B1    | 1 TB   | 4       | 2065  | 478   | 1.87   |
| WDC       | WD20EADS-00S2B0    | 2 TB   | 2       | 750   | 2     | 1.87   |
| Seagate   | ST3000DM001-1ER166 | 3 TB   | 33      | 692   | 53    | 1.86   |
| Hitachi   | HUA721010KLA330... | 1 TB   | 1       | 2715  | 3     | 1.86   |
| WDC       | WD800BB-63JKC0     | 80 GB  | 1       | 676   | 0     | 1.85   |
| WDC       | WD2500AAKX-60U6AA0 | 250 GB | 4       | 675   | 0     | 1.85   |
| WDC       | WD2000F9YZ-09N20L0 | 2 TB   | 1       | 675   | 0     | 1.85   |
| WDC       | WD15EARS-22Z5B1    | 1.5 TB | 3       | 675   | 0     | 1.85   |
| Seagate   | ST4000NE0025-2E... | 4 TB   | 4       | 673   | 0     | 1.84   |
| WDC       | WD800BB-75DKA0     | 80 GB  | 1       | 672   | 0     | 1.84   |
| Seagate   | ST3320413CS        | 320 GB | 10      | 727   | 114   | 1.84   |
| WDC       | WD1200JS-55MHB0    | 120 GB | 2       | 671   | 0     | 1.84   |
| HGST      | HUS722T2TALA604    | 2 TB   | 3       | 671   | 0     | 1.84   |
| Seagate   | ST8000VN0022-2E... | 8 TB   | 23      | 749   | 3     | 1.84   |
| WDC       | WD5000LPVT-60G33T0 | 500 GB | 1       | 670   | 0     | 1.84   |
| WDC       | WD3200AAKS-75VYA0  | 320 GB | 3       | 670   | 0     | 1.84   |
| WDC       | WD3200AAJS-40RYA0  | 320 GB | 2       | 1197  | 389   | 1.83   |
| WDC       | WD1502FYPS-01U1B1  | 1.5 TB | 1       | 667   | 0     | 1.83   |
| WDC       | WD4003FZEX-00Z4SA0 | 4 TB   | 3       | 665   | 0     | 1.82   |
| WDC       | WD30EURS-63R8UY0   | 3 TB   | 2       | 664   | 0     | 1.82   |
| Seagate   | ST2000DL003-9VT166 | 2 TB   | 70      | 846   | 84    | 1.82   |
| Seagate   | ST4000VM000-1F3168 | 4 TB   | 5       | 663   | 0     | 1.82   |
| WDC       | WD1200JD-00FYB0    | 120 GB | 1       | 661   | 0     | 1.81   |
| WDC       | WD20EARS-00MVWB0   | 2 TB   | 55      | 1031  | 103   | 1.81   |
| WDC       | WD1600AVBS-63SVA0  | 160 GB | 1       | 658   | 0     | 1.80   |
| Hitachi   | HDT721032SLA380    | 320 GB | 6       | 928   | 390   | 1.80   |
| WDC       | WD5000BPVT-75HXZT1 | 500 GB | 1       | 657   | 0     | 1.80   |
| WDC       | WD5000AAJS-00TKA0  | 500 GB | 1       | 656   | 0     | 1.80   |
| WDC       | WD5001AALS-00L3B2  | 500 GB | 32      | 992   | 29    | 1.80   |
| WDC       | WD2500AAKX-22ERMA0 | 250 GB | 1       | 656   | 0     | 1.80   |
| WDC       | WD1600JS-98NCB1    | 160 GB | 1       | 655   | 0     | 1.80   |
| WDC       | WD5000AAKS-07V0A0  | 500 GB | 1       | 654   | 0     | 1.79   |
| WDC       | WD10EZEX-00ZF5A0   | 1 TB   | 16      | 743   | 129   | 1.79   |
| Seagate   | ST360021A          | 64 GB  | 4       | 738   | 12    | 1.79   |
| WDC       | WD3200AAJS-65RYA0  | 320 GB | 2       | 652   | 0     | 1.79   |
| Seagate   | ST3000DM003-1F216N | 3 TB   | 1       | 652   | 0     | 1.79   |
| WDC       | WD5000AAKS-00Z7B0  | 500 GB | 1       | 652   | 0     | 1.79   |
| Seagate   | ST3320413AS        | 320 GB | 12      | 1044  | 66    | 1.79   |
| Toshiba   | MD04ACA400         | 4 TB   | 7       | 906   | 573   | 1.79   |
| Seagate   | ST10000VN0004-1... | 10 TB  | 9       | 726   | 1     | 1.79   |
| WDC       | WD400BD-60JPA0     | 40 GB  | 1       | 651   | 0     | 1.78   |
| Hitachi   | HDS721010CLA632    | 1 TB   | 2       | 651   | 0     | 1.78   |
| WDC       | WD10EADS-65L5B1    | 1 TB   | 8       | 1190  | 4     | 1.78   |
| Hitachi   | HDS722580VLSA80    | 82 GB  | 3       | 1101  | 671   | 1.78   |
| Samsung   | HD154UI            | 1.5 TB | 34      | 1025  | 255   | 1.78   |
| Seagate   | ST980812AS         | 80 GB  | 1       | 647   | 0     | 1.77   |
| WDC       | WD800AAJS-00PSA0   | 80 GB  | 20      | 765   | 37    | 1.77   |
| WDC       | WD5000AAKS-07TMA0  | 500 GB | 1       | 646   | 0     | 1.77   |
| Hitachi   | HDT721010SLA360    | 1 TB   | 33      | 1160  | 18    | 1.77   |
| WDC       | WD2500HHTZ-04N21V0 | 250 GB | 8       | 706   | 1     | 1.77   |
| Toshiba   | DT01ABA050V        | 500 GB | 1       | 644   | 0     | 1.77   |
| Hitachi   | HTS722012K9SA00    | 120 GB | 4       | 708   | 255   | 1.77   |
| WDC       | WD15EADS-00P8B0    | 1.5 TB | 10      | 1312  | 8     | 1.76   |
| WDC       | WD2500AAJS-08L7A0  | 250 GB | 3       | 642   | 0     | 1.76   |
| WDC       | WD3200AAKS-00VYA0  | 320 GB | 6       | 734   | 59    | 1.76   |
| WDC       | WD5002AALX-00J37A0 | 500 GB | 16      | 741   | 67    | 1.76   |
| WDC       | WD1001FALS-19J7B0  | 1 TB   | 1       | 641   | 0     | 1.76   |
| WDC       | WD3200AAJS-07M0A0  | 320 GB | 3       | 795   | 3     | 1.75   |
| Seagate   | ST3200820AS        | 200 GB | 25      | 913   | 425   | 1.75   |
| Toshiba   | DT01ABA200V        | 2 TB   | 1       | 639   | 0     | 1.75   |
| WDC       | WD20EFRX-68AX9N0   | 2 TB   | 12      | 691   | 1     | 1.75   |
| WDC       | WD800JB-00ETA0     | 80 GB  | 5       | 1354  | 273   | 1.75   |
| WDC       | WD1600JS-98MHB0    | 160 GB | 1       | 638   | 0     | 1.75   |
| WDC       | WD10EALX-009BA0    | 1 TB   | 59      | 826   | 17    | 1.74   |
| WDC       | WD10JPVX-55JC3T3   | 1 TB   | 1       | 634   | 0     | 1.74   |
| Seagate   | ST1000VM002-1SD102 | 1 TB   | 2       | 634   | 0     | 1.74   |
| WDC       | WD20EARX-00ZUDB0   | 2 TB   | 2       | 1181  | 2     | 1.74   |
| Samsung   | HD103SI            | 1 TB   | 32      | 893   | 104   | 1.74   |
| WDC       | WD1002FBYS-43P1B0  | 1 TB   | 2       | 1021  | 39    | 1.74   |
| Samsung   | HD103SJ            | 1 TB   | 98      | 819   | 11    | 1.74   |
| WDC       | WD3200AAKS-22SBA0  | 320 GB | 1       | 633   | 0     | 1.73   |
| WDC       | WD7500BPVT-16HXZT3 | 752 GB | 1       | 632   | 0     | 1.73   |
| Hitachi   | HDT721016SLA380    | 160 GB | 15      | 788   | 6     | 1.73   |
| WDC       | WD3200AAKX-221CA1  | 320 GB | 3       | 631   | 0     | 1.73   |
| Hitachi   | HTS723220L9A360    | 200 GB | 1       | 630   | 0     | 1.73   |
| WDC       | WD1600AABS-00PRA0  | 160 GB | 1       | 630   | 0     | 1.73   |
| WDC       | WD1600AAJS-22WAA0  | 160 GB | 4       | 1063  | 2     | 1.73   |
| Seagate   | ST380815AS         | 80 GB  | 150     | 834   | 229   | 1.73   |
| WDC       | WD7500BPKX-60HPJT0 | 752 GB | 1       | 627   | 0     | 1.72   |
| WDC       | WD4000BEVT-11ZAT0  | 400 GB | 1       | 626   | 0     | 1.72   |
| WDC       | WD10EARX-00N0YB0   | 1 TB   | 53      | 762   | 4     | 1.72   |
| WDC       | WD800JD-22MSA1     | 80 GB  | 8       | 625   | 0     | 1.71   |
| WDC       | WD40EFRX-68WT0N0   | 4 TB   | 52      | 888   | 2     | 1.71   |
| WDC       | WD2500AAKS-00VSA0  | 250 GB | 24      | 857   | 17    | 1.71   |
| WDC       | WD15EADS-00R6B0    | 1.5 TB | 1       | 625   | 0     | 1.71   |
| Fujitsu   | MHY2250BH          | 250 GB | 7       | 841   | 47    | 1.71   |
| WDC       | WD1600AAJS-00PSA0  | 160 GB | 26      | 879   | 54    | 1.71   |
| Toshiba   | HDWE160            | 6 TB   | 4       | 623   | 0     | 1.71   |
| WDC       | WD10EZEX-75ZF5A0   | 1 TB   | 6       | 623   | 0     | 1.71   |
| WDC       | WD360GD-00FLC0     | 37 GB  | 1       | 622   | 0     | 1.70   |
| WDC       | WD800JD-00MSA1     | 80 GB  | 12      | 845   | 7     | 1.70   |
| WDC       | WD1600AAJS-55PSA0  | 160 GB | 1       | 620   | 0     | 1.70   |
| Seagate   | ST6000DM004-2EH11C | 6 TB   | 1       | 619   | 0     | 1.70   |
| Hitachi   | HCS5C1032CLA382    | 320 GB | 2       | 883   | 2     | 1.68   |
| WDC       | WD5000AAKS-00V0A0  | 500 GB | 4       | 675   | 2     | 1.68   |
| Samsung   | HD103UJ            | 1 TB   | 60      | 1155  | 188   | 1.68   |
| WDC       | WD1003FBYX-18Y7B0  | 1 TB   | 2       | 955   | 2     | 1.68   |
| Hitachi   | HDS721010CLA630    | 1 TB   | 7       | 680   | 1     | 1.67   |
| WDC       | WD800JD-00LUA0     | 80 GB  | 1       | 610   | 0     | 1.67   |
| Hitachi   | HDS721075CLA332    | 752 GB | 2       | 610   | 0     | 1.67   |
| HP        | MB1000GDUNU        | 1 TB   | 1       | 609   | 0     | 1.67   |
| WDC       | WD3200KS-00PFB0    | 320 GB | 3       | 1056  | 31    | 1.67   |
| Seagate   | ST340014A          | 40 GB  | 84      | 806   | 35    | 1.67   |
| Seagate   | ST31000526SV       | 1 TB   | 3       | 769   | 343   | 1.67   |
| WDC       | WD2500AAKX-753CA1  | 250 GB | 10      | 712   | 106   | 1.67   |
| WDC       | WD3200BEVT-75ZCT2  | 320 GB | 8       | 685   | 95    | 1.66   |
| WDC       | WD800JD-75MSA1     | 80 GB  | 1       | 607   | 0     | 1.66   |
| Fujitsu   | MHW2060BH          | 64 GB  | 2       | 1040  | 5     | 1.66   |
| WDC       | WD10JFCX-68N6GN0   | 1 TB   | 4       | 716   | 1     | 1.66   |
| WDC       | WD10EALS-00Z8A0    | 1 TB   | 23      | 895   | 64    | 1.66   |
| WDC       | WD5000AAJS-00A8B0  | 500 GB | 3       | 605   | 0     | 1.66   |
| Seagate   | ST3400620AS        | 400 GB | 25      | 961   | 10    | 1.65   |
| WDC       | WD3000JS-60PDB0    | 304 GB | 2       | 603   | 0     | 1.65   |
| Seagate   | ST980411ASG        | 80 GB  | 2       | 831   | 7     | 1.65   |
| Hitachi   | HTS545016B9SA02    | 160 GB | 1       | 602   | 0     | 1.65   |
| Seagate   | ST1000DM005 HD1... | 1 TB   | 12      | 690   | 2     | 1.65   |
| Seagate   | ST9200420AS        | 200 GB | 2       | 601   | 0     | 1.65   |
| WDC       | WD1200JS-00MHB0    | 120 GB | 15      | 635   | 1     | 1.65   |
| WDC       | WD800JD-23LSA0     | 80 GB  | 1       | 1202  | 1     | 1.65   |
| WDC       | WD1600JS-23MHB0    | 160 GB | 1       | 600   | 0     | 1.64   |
| WDC       | WD15EARX-00PASB0   | 1.5 TB | 11      | 663   | 2     | 1.64   |
| HGST      | HDS724040ALE640    | 4 TB   | 1       | 598   | 0     | 1.64   |
| WDC       | WD10EURX-56FH1Y0   | 1 TB   | 2       | 596   | 0     | 1.63   |
| Samsung   | HD642JJ            | 640 GB | 23      | 1296  | 408   | 1.63   |
| WDC       | WD800AAJS-00WAA0   | 80 GB  | 4       | 594   | 3     | 1.63   |
| WDC       | WD10EURX-63FH1Y0   | 1 TB   | 4       | 592   | 0     | 1.62   |
| WDC       | WD6400AAKS-65A7B2  | 640 GB | 12      | 1225  | 42    | 1.62   |
| WDC       | WD6001FZWX-00A2VA0 | 6 TB   | 1       | 590   | 0     | 1.62   |
| Seagate   | ST1000DX001-SSH... | 1 TB   | 1       | 590   | 0     | 1.62   |
| Apple     | HDD ST750LM022     | 752 GB | 1       | 589   | 0     | 1.61   |
| WDC       | WD1600BEVS-22UST0  | 160 GB | 3       | 782   | 63    | 1.61   |
| WDC       | WD800JD-19LSA0     | 80 GB  | 1       | 588   | 0     | 1.61   |
| WDC       | WD3200AAJS-00VWA0  | 320 GB | 11      | 656   | 42    | 1.61   |
| Seagate   | ST3160815AS        | 160 GB | 171     | 824   | 354   | 1.61   |
| Hitachi   | HDS728080PLAT20    | 82 GB  | 20      | 738   | 7     | 1.61   |
| WDC       | WD5003ABYX-01WERA1 | 500 GB | 6       | 783   | 1     | 1.61   |
| Hitachi   | HDS723015BLA642    | 1.5 TB | 7       | 807   | 28    | 1.61   |
| WDC       | WD1600AAJS-00M0A0  | 160 GB | 6       | 784   | 68    | 1.61   |
| Hitachi   | HDT725050VLA360    | 500 GB | 5       | 1151  | 37    | 1.60   |
| WDC       | WD20EARS-55MVWB0   | 2 TB   | 1       | 584   | 0     | 1.60   |
| Seagate   | ST4000NM0035-1V... | 4 TB   | 5       | 583   | 0     | 1.60   |
| WDC       | WD5000AAKS-00D2B0  | 500 GB | 12      | 1035  | 8     | 1.60   |
| Maxtor    | STM3160215A        | 160 GB | 10      | 630   | 307   | 1.60   |
| WDC       | WD2500AVJS-63WDA0  | 250 GB | 2       | 582   | 0     | 1.60   |
| WDC       | WD1600BEVS-75RST0  | 160 GB | 2       | 579   | 0     | 1.59   |
| Maxtor    | STM3320620A        | 320 GB | 2       | 579   | 0     | 1.59   |
| Seagate   | ST2000DX001-1NS164 | 2 TB   | 8       | 579   | 0     | 1.59   |
| WDC       | WD4002FFWX-68TZ4N0 | 4 TB   | 1       | 579   | 0     | 1.59   |
| WDC       | WD2500BEKT-60V5T1  | 250 GB | 1       | 578   | 0     | 1.59   |
| WDC       | WD2500AAJS-07M0A0  | 250 GB | 5       | 776   | 4     | 1.59   |
| WDC       | WD1600BB-55RDA0    | 160 GB | 3       | 682   | 2     | 1.58   |
| WDC       | WD30EZRZ-00WN9B0   | 3 TB   | 3       | 578   | 0     | 1.58   |
| WDC       | WD2500BUCT-63TWBY0 | 250 GB | 2       | 884   | 519   | 1.58   |
| Samsung   | SP1644N            | 160 GB | 3       | 683   | 527   | 1.58   |
| Seagate   | ST31000524NS       | 1 TB   | 6       | 1198  | 258   | 1.57   |
| Toshiba   | MQ01ABC150         | 1.5 TB | 1       | 574   | 0     | 1.57   |
| WDC       | WD800JD-75JNA0     | 80 GB  | 3       | 1489  | 39    | 1.57   |
| HGST      | HMS5C4040ALE640    | 4 TB   | 1       | 573   | 0     | 1.57   |
| Hitachi   | HUA722020ALA331    | 2 TB   | 4       | 639   | 1     | 1.57   |
| Seagate   | ST3160212AS        | 160 GB | 2       | 572   | 0     | 1.57   |
| Seagate   | ST10000NM0016-1... | 10 TB  | 7       | 572   | 0     | 1.57   |
| WDC       | WD15EARS-00S0XB0   | 1.5 TB | 2       | 912   | 1     | 1.57   |
| Hitachi   | HDS721010CLA332    | 1 TB   | 110     | 923   | 86    | 1.56   |
| WDC       | WD10EARS-003BB1    | 1 TB   | 10      | 750   | 172   | 1.56   |
| Seagate   | ST31500541AS       | 1.5 TB | 10      | 757   | 37    | 1.56   |
| WDC       | WD5000AAKS-22A7B0  | 500 GB | 15      | 1100  | 5     | 1.56   |
| Seagate   | ST1000NX0443       | 1 TB   | 2       | 566   | 0     | 1.55   |
| WDC       | WD40PURX-64GVNY0   | 4 TB   | 2       | 561   | 0     | 1.54   |
| Apple     | HDD TOSHIBA MK5... | 500 GB | 1       | 560   | 0     | 1.54   |
| Seagate   | ST3320418AS        | 320 GB | 81      | 833   | 141   | 1.54   |
| Samsung   | HD253GJ            | 250 GB | 7       | 768   | 17    | 1.53   |
| WDC       | WD6400AAKS-75A7B2  | 640 GB | 5       | 762   | 6     | 1.53   |
| WDC       | WD1000DHTZ-04N21V1 | 1 TB   | 1       | 559   | 0     | 1.53   |
| WDC       | WD20EZRX-00D8PB0   | 2 TB   | 43      | 619   | 12    | 1.53   |
| WDC       | WD2500JB-98GVA0    | 250 GB | 1       | 3354  | 5     | 1.53   |
| WDC       | WD2500AAJB-00WGA0  | 250 GB | 5       | 1069  | 115   | 1.53   |
| WDC       | WD3200AAKS-75L9A0  | 320 GB | 17      | 870   | 50    | 1.53   |
| Seagate   | ST3250823A         | 250 GB | 6       | 977   | 440   | 1.53   |
| Seagate   | ST3160318AS        | 160 GB | 62      | 774   | 96    | 1.53   |
| WDC       | WD800JD-22LSA0     | 80 GB  | 8       | 715   | 83    | 1.53   |
| WDC       | WD800JD-00LSA5     | 80 GB  | 2       | 557   | 0     | 1.53   |
| Seagate   | ST3250824AS        | 250 GB | 22      | 892   | 733   | 1.52   |
| WDC       | WD3000JS-00PDB0    | 304 GB | 1       | 554   | 0     | 1.52   |
| Samsung   | HD502HJ            | 500 GB | 93      | 771   | 73    | 1.52   |
| Seagate   | ST3160316AS        | 160 GB | 12      | 677   | 7     | 1.52   |
| WDC       | WD10EZRX-00A8LB0   | 1 TB   | 50      | 706   | 38    | 1.51   |
| Seagate   | ST380011A          | 80 GB  | 168     | 820   | 77    | 1.51   |
| Seagate   | ST3250620AS        | 250 GB | 54      | 921   | 329   | 1.51   |
| WDC       | WD5000AADS-00L4B1  | 500 GB | 7       | 905   | 5     | 1.51   |
| WDC       | WD3200BPVT-00HXZT0 | 320 GB | 1       | 549   | 0     | 1.51   |
| Seagate   | ST2000VX000-1ES164 | 2 TB   | 8       | 549   | 0     | 1.50   |
| WDC       | WD1600JS-00SGB0    | 160 GB | 1       | 549   | 0     | 1.50   |
| WDC       | WD400BB-00JHC0     | 40 GB  | 4       | 872   | 24    | 1.50   |
| WDC       | WD2500AAKS-00YGA0  | 250 GB | 2       | 548   | 0     | 1.50   |
| Seagate   | ST360015A          | 64 GB  | 2       | 1494  | 5     | 1.50   |
| WDC       | WD360ADFD-00NLR1   | 37 GB  | 1       | 547   | 0     | 1.50   |
| Seagate   | ST3120026A         | 120 GB | 20      | 899   | 153   | 1.49   |
| WDC       | WD3200AAKS-00L9A0  | 320 GB | 43      | 887   | 32    | 1.49   |
| Seagate   | ST3200827A         | 200 GB | 1       | 544   | 0     | 1.49   |
| Seagate   | ST3000VN007-2E4166 | 3 TB   | 2       | 544   | 0     | 1.49   |
| Seagate   | ST1000VX001-1Z4102 | 1 TB   | 2       | 544   | 0     | 1.49   |
| MediaMax  | WL1000GSA6472C     | 1 TB   | 1       | 543   | 0     | 1.49   |
| Hitachi   | HDT725025VLAT80    | 250 GB | 2       | 1843  | 2     | 1.49   |
| Seagate   | ST3320620A         | 320 GB | 24      | 859   | 5     | 1.49   |
| Seagate   | ST320410A          | 20 GB  | 5       | 1011  | 10    | 1.48   |
| WDC       | WD2500BEVS-26UST0  | 250 GB | 5       | 540   | 0     | 1.48   |
| WDC       | WD3000HLFS-01G6U0  | 304 GB | 1       | 540   | 0     | 1.48   |
| WDC       | WD2000JB-00REA0    | 200 GB | 3       | 837   | 1     | 1.48   |
| WDC       | WD10EADS-114BB1    | 1 TB   | 1       | 1079  | 1     | 1.48   |
| Seagate   | ST3250820AS        | 250 GB | 40      | 855   | 282   | 1.48   |
| Seagate   | ST1000DL002-9TT153 | 1 TB   | 33      | 1021  | 359   | 1.48   |
| Hitachi   | HDS721050CLA662    | 500 GB | 9       | 623   | 115   | 1.48   |
| WDC       | WD7500AZEX-00RKKA0 | 752 GB | 6       | 538   | 0     | 1.48   |
| Seagate   | ST3300620AS        | 304 GB | 2       | 538   | 0     | 1.47   |
| WDC       | WD7500BPKX-75HPJT0 | 752 GB | 3       | 536   | 0     | 1.47   |
| WDC       | WD3200BPVT-00JJ5T0 | 320 GB | 9       | 587   | 1     | 1.47   |
| WDC       | WD5000AAKS-75A7B0  | 500 GB | 3       | 714   | 3     | 1.47   |
| WDC       | WD1001FAES-55W7A0  | 1 TB   | 2       | 535   | 0     | 1.47   |
| HGST      | HUH721212ALN600    | 12 TB  | 1       | 534   | 0     | 1.46   |
| WDC       | WD800AAJS-22L7A0   | 80 GB  | 1       | 534   | 0     | 1.46   |
| Seagate   | ST4000NM0245-1Z... | 4 TB   | 1       | 533   | 0     | 1.46   |
| WDC       | WD10EZEX-00ER1A0   | 1 TB   | 3       | 533   | 0     | 1.46   |
| WDC       | WD1600JS-22MHB0    | 160 GB | 3       | 700   | 9     | 1.46   |
| Samsung   | HD105SI            | 1 TB   | 13      | 803   | 302   | 1.46   |
| Hitachi   | HUA722010CLA330    | 1 TB   | 13      | 789   | 81    | 1.45   |
| Hitachi   | HDS5C1032CLA382    | 320 GB | 5       | 748   | 3     | 1.45   |
| WDC       | WD30EZRZ-00GXCB0   | 3 TB   | 2       | 530   | 0     | 1.45   |
| Seagate   | ST3750640NS        | 752 GB | 7       | 1166  | 449   | 1.45   |
| WDC       | WD5000AZRX-00A8LB0 | 500 GB | 71      | 556   | 1     | 1.45   |
| Seagate   | ST3500320NS        | 500 GB | 14      | 896   | 402   | 1.45   |
| WDC       | WD5000AAKS-007AA0  | 500 GB | 9       | 913   | 13    | 1.44   |
| WDC       | WD5000AACS-00G8B1  | 500 GB | 11      | 726   | 3     | 1.44   |
| Seagate   | ST14000VN0008-2... | 14 TB  | 2       | 525   | 0     | 1.44   |
| WDC       | WD7500BPVT-00HXZT1 | 752 GB | 1       | 525   | 0     | 1.44   |
| WDC       | WD3200AAKS-61L9A0  | 320 GB | 5       | 528   | 6     | 1.44   |
| WDC       | WD10EURX-83UY4Y0   | 1 TB   | 1       | 524   | 0     | 1.44   |
| Seagate   | ST160LM003 HN-M... | 160 GB | 3       | 522   | 0     | 1.43   |
| WDC       | WD2500BPVT-00JJ5T0 | 250 GB | 1       | 522   | 0     | 1.43   |
| Maxtor    | 4K020H1            | 20 GB  | 1       | 522   | 0     | 1.43   |
| WDC       | WD1600JS-00NCB1    | 160 GB | 16      | 665   | 10    | 1.43   |
| WDC       | WD800BB-00JKC0     | 80 GB  | 2       | 520   | 0     | 1.43   |
| WDC       | WD6400AARS-003BB1  | 640 GB | 1       | 520   | 0     | 1.43   |
| WDC       | WD3200AAKS-00B3A0  | 320 GB | 34      | 722   | 33    | 1.42   |
| WDC       | WD10EZEX-00KUWA0   | 1 TB   | 17      | 627   | 2     | 1.42   |
| Fujitsu   | MHW2120BH          | 120 GB | 17      | 591   | 31    | 1.41   |
| Seagate   | ST2000DM001-1ER164 | 2 TB   | 76      | 557   | 24    | 1.41   |
| Seagate   | ST3160215ACE       | 160 GB | 3       | 809   | 72    | 1.41   |
| WDC       | WD20EZRX-00DC0B0   | 2 TB   | 27      | 629   | 2     | 1.41   |
| Seagate   | ST2000DM001-1CH164 | 2 TB   | 126     | 642   | 148   | 1.41   |
| Samsung   | HD502IJ            | 500 GB | 30      | 1029  | 307   | 1.41   |
| WDC       | WD20EFRX-68EUZN0   | 2 TB   | 57      | 589   | 1     | 1.41   |
| Hitachi   | HDS728080PLA380    | 80 GB  | 39      | 834   | 59    | 1.41   |
| WDC       | WD10EAVS-00D7B1    | 1 TB   | 8       | 913   | 22    | 1.41   |
| WDC       | WD1500HLFS-01MZUV0 | 150 GB | 2       | 511   | 0     | 1.40   |
| WDC       | WD2500BEVT-75ZCT2  | 250 GB | 4       | 819   | 1     | 1.40   |
| Seagate   | ST640LM000 HM641JI | 640 GB | 2       | 511   | 0     | 1.40   |
| Seagate   | ST10000NE0004-1... | 10 TB  | 7       | 857   | 15    | 1.40   |
| Seagate   | ST3000VX000-1CU166 | 3 TB   | 3       | 509   | 0     | 1.40   |
| WDC       | WD3200AAJS-55B4A0  | 320 GB | 2       | 749   | 4     | 1.40   |
| WDC       | WD5000LPVT-16G33T0 | 500 GB | 5       | 508   | 0     | 1.39   |
| WDC       | WD2500AAKS-00L9A0  | 250 GB | 10      | 909   | 4     | 1.39   |
| WDC       | WD6400AAKS-55A7B0  | 640 GB | 1       | 507   | 0     | 1.39   |
| WDC       | WD7500AADS-00M2B0  | 752 GB | 20      | 956   | 19    | 1.39   |
| WDC       | WD10JPVT-24A1YT0   | 1 TB   | 3       | 506   | 0     | 1.39   |
| WDC       | WD10EFRX-68PJCN0   | 1 TB   | 29      | 579   | 1     | 1.39   |
| Seagate   | ST3250312AS        | 250 GB | 27      | 660   | 39    | 1.38   |
| Toshiba   | MK2556GSYF         | 250 GB | 1       | 503   | 0     | 1.38   |
| Seagate   | ST1000VT000 HN-... | 1 TB   | 1       | 501   | 0     | 1.38   |
| WDC       | WD10EURX-73C57Y0   | 1 TB   | 3       | 501   | 0     | 1.37   |
| WDC       | WD1600AAJS-60WAA0  | 160 GB | 4       | 568   | 253   | 1.37   |
| Seagate   | ST2000VX003-1HH164 | 2 TB   | 2       | 500   | 0     | 1.37   |
| Seagate   | ST3160023A         | 160 GB | 16      | 827   | 320   | 1.37   |
| Seagate   | ST320014A          | 20 GB  | 6       | 787   | 13    | 1.37   |
| Seagate   | ST380012ACE        | 80 GB  | 4       | 498   | 0     | 1.37   |
| WDC       | WD2500AAJS-22VTA0  | 250 GB | 8       | 617   | 1     | 1.37   |
| WDC       | WD400BB-00JHA0     | 40 GB  | 3       | 1145  | 4     | 1.36   |
| WDC       | WD60EFRX-68MYMN1   | 6 TB   | 8       | 766   | 86    | 1.36   |
| WDC       | WD800JD-55MSA1     | 80 GB  | 2       | 497   | 0     | 1.36   |
| WDC       | WD200EB-00BHF0     | 20 GB  | 1       | 992   | 1     | 1.36   |
| WDC       | WD1200JD-00GBB0    | 120 GB | 3       | 754   | 4     | 1.36   |
| Seagate   | ST3500413AS        | 500 GB | 121     | 643   | 69    | 1.36   |
| Seagate   | ST3500630NS        | 500 GB | 5       | 684   | 529   | 1.36   |
| Fujitsu   | MPE3136AH          | 16 GB  | 1       | 494   | 0     | 1.35   |
| Samsung   | HD501LJ            | 500 GB | 51      | 991   | 364   | 1.35   |
| WDC       | WD6402AAEX-00Y9A0  | 640 GB | 4       | 675   | 10    | 1.35   |
| WDC       | WD5000AAKS-00V2B0  | 500 GB | 3       | 663   | 1     | 1.35   |
| Seagate   | ST1000VX000-9YW162 | 1 TB   | 5       | 491   | 0     | 1.35   |
| WDC       | WD4000AAKS-00TMA0  | 400 GB | 4       | 561   | 1     | 1.35   |
| WDC       | WD800BB-55JKA0     | 80 GB  | 4       | 665   | 1     | 1.34   |
| HGST      | HDN726060ALE614    | 6 TB   | 2       | 490   | 0     | 1.34   |
| WDC       | WD10JPVT-16A1YT0   | 1 TB   | 1       | 490   | 0     | 1.34   |
| Seagate   | ST3200826AS        | 200 GB | 13      | 822   | 74    | 1.34   |
| WDC       | WD800BB-00JHA0     | 80 GB  | 8       | 827   | 4     | 1.34   |
| WDC       | WD5001AALS-00LWTA0 | 500 GB | 6       | 751   | 42    | 1.34   |
| WDC       | WD2000JS-00MHB0    | 200 GB | 8       | 706   | 61    | 1.34   |
| WDC       | WD10JMVW-11S5XS0   | 1 TB   | 2       | 488   | 0     | 1.34   |
| WDC       | WD5000AAKX-603CA0  | 500 GB | 10      | 565   | 102   | 1.34   |
| WDC       | WD1600AAJS-08PSA0  | 160 GB | 12      | 645   | 8     | 1.33   |
| WDC       | WD5000BEVT-35A0RT0 | 500 GB | 12      | 636   | 8     | 1.33   |
| WDC       | WD740ADFD-00NLR5   | 74 GB  | 2       | 486   | 0     | 1.33   |
| HGST      | HUH728080ALN600    | 8 TB   | 1       | 485   | 0     | 1.33   |
| WDC       | WD3200AAJS-08L7A0  | 320 GB | 13      | 822   | 137   | 1.33   |
| WDC       | WD800JD-55JRC0     | 80 GB  | 2       | 604   | 31    | 1.33   |
| Maxtor    | STM3320820AS       | 320 GB | 15      | 713   | 71    | 1.33   |
| Seagate   | ST98823A           | 80 GB  | 4       | 633   | 323   | 1.33   |
| Seagate   | ST9500420ASG       | 500 GB | 2       | 572   | 1     | 1.33   |
| Hitachi   | HUA723020ALA641    | 2 TB   | 13      | 545   | 1     | 1.33   |
| Fujitsu   | MHT2040AH          | 40 GB  | 1       | 484   | 0     | 1.33   |
| Seagate   | ST1000VM002-1CT162 | 1 TB   | 3       | 484   | 0     | 1.33   |
| WDC       | WD1200JB-00GVA0    | 120 GB | 4       | 754   | 1     | 1.32   |
| Seagate   | ST2000DM001-9YN164 | 2 TB   | 45      | 916   | 330   | 1.32   |
| Seagate   | ST340015A          | 40 GB  | 5       | 835   | 33    | 1.32   |
| Hitachi   | HDS721050CLA362    | 500 GB | 122     | 675   | 31    | 1.32   |
| WDC       | WD7500AZEX-00ZF5A0 | 752 GB | 6       | 481   | 0     | 1.32   |
| WDC       | WD6400BPVT-75HXZT1 | 640 GB | 3       | 648   | 2     | 1.32   |
| Seagate   | ST3808110AS        | 80 GB  | 34      | 946   | 451   | 1.32   |
| WDC       | WD5000BPKX-80HPJT0 | 500 GB | 1       | 480   | 0     | 1.32   |
| WDC       | WD6400AAKS-22A7B2  | 640 GB | 17      | 815   | 3     | 1.32   |
| Seagate   | ST3160815A         | 160 GB | 37      | 746   | 235   | 1.32   |
| WDC       | WD10JMVW-11AJGS2   | 1 TB   | 9       | 606   | 2     | 1.31   |
| WDC       | WD10EADS-65M2B1    | 1 TB   | 3       | 931   | 2     | 1.31   |
| Maxtor    | 6V160E0            | 160 GB | 8       | 509   | 1     | 1.31   |
| WDC       | WD10EZEX-00RKKA0   | 1 TB   | 76      | 597   | 82    | 1.31   |
| WDC       | WD7502AAEX-00Y9A0  | 752 GB | 5       | 478   | 0     | 1.31   |
| Hitachi   | HDS721050CLA660    | 500 GB | 17      | 545   | 6     | 1.31   |
| Seagate   | ST2000NM0033-9Z... | 2 TB   | 7       | 478   | 0     | 1.31   |
| Seagate   | ST3160812A         | 160 GB | 27      | 737   | 385   | 1.31   |
| Hitachi   | HUA722050CLA330    | 500 GB | 2       | 476   | 0     | 1.31   |
| Apple     | HDD HTS545050A7... | 500 GB | 14      | 496   | 2     | 1.30   |
| WDC       | WD7500AACS-00D6B1  | 752 GB | 3       | 921   | 4     | 1.30   |
| Seagate   | ST9120821A         | 120 GB | 4       | 719   | 19    | 1.30   |
| WDC       | WD5000AUDX-63WNHY0 | 500 GB | 3       | 475   | 0     | 1.30   |
| WDC       | WD1600JS-56MHB1    | 160 GB | 6       | 572   | 5     | 1.30   |
| WDC       | WD1600BEVS-22RST0  | 160 GB | 41      | 582   | 90    | 1.30   |
| WDC       | WD3200AAJB-56R1A0  | 320 GB | 1       | 473   | 0     | 1.30   |
| Hitachi   | HDP725050GLA360    | 500 GB | 76      | 1025  | 36    | 1.30   |
| Toshiba   | MK1032GSX          | 100 GB | 5       | 497   | 1     | 1.29   |
| Toshiba   | MK1016GAP          | 10 GB  | 1       | 472   | 0     | 1.29   |
| Seagate   | ST1000NM0033-9Z... | 1 TB   | 26      | 556   | 40    | 1.29   |
| WDC       | WD10EACS-65D6B0    | 1 TB   | 1       | 471   | 0     | 1.29   |
| WDC       | WD5000AAKS-75A7B2  | 500 GB | 3       | 1036  | 6     | 1.29   |
| WDC       | WD5000BEKT-75KA9T0 | 500 GB | 3       | 469   | 0     | 1.29   |
| Toshiba   | MQ03ABB200         | 2 TB   | 1       | 468   | 0     | 1.28   |
| WDC       | WD4001FFSX-68JNUN0 | 4 TB   | 1       | 468   | 0     | 1.28   |
| Seagate   | ST250LT020-1AE14C  | 250 GB | 2       | 592   | 470   | 1.28   |
| WDC       | WD1600AAJS-00L7A0  | 160 GB | 27      | 738   | 4     | 1.28   |
| Seagate   | ST380215AS         | 80 GB  | 26      | 771   | 535   | 1.28   |
| WDC       | WD3200AVJS-63N9A0  | 320 GB | 3       | 467   | 0     | 1.28   |
| Seagate   | ST32000646NS       | 2 TB   | 1       | 467   | 0     | 1.28   |
| Samsung   | SV0221N            | 20 GB  | 1       | 2328  | 4     | 1.28   |
| Samsung   | HD252HJ            | 250 GB | 24      | 792   | 144   | 1.27   |
| WDC       | WD10EVDS-63U8B1    | 1 TB   | 1       | 464   | 0     | 1.27   |
| Hitachi   | HDT721064SLA380    | 640 GB | 1       | 464   | 0     | 1.27   |
| WDC       | WD800AAJS-00B4A0   | 80 GB  | 5       | 543   | 3     | 1.27   |
| WDC       | WD1001FAES-22W7A0  | 1 TB   | 1       | 460   | 0     | 1.26   |
| WDC       | WD10S21X-24R1BT... | 1 TB   | 7       | 460   | 0     | 1.26   |
| WDC       | WD40EZRZ-00WN9B0   | 4 TB   | 4       | 460   | 0     | 1.26   |
| WDC       | WD1600AAJS-00V4A0  | 160 GB | 6       | 463   | 13    | 1.26   |
| Seagate   | ST2000VM003-1CT164 | 2 TB   | 6       | 745   | 720   | 1.26   |
| Seagate   | ST3500411SV        | 500 GB | 3       | 646   | 25    | 1.26   |
| WDC       | WD1003FZEX-00MK2A0 | 1 TB   | 49      | 502   | 1     | 1.26   |
| WDC       | WD2500JS-22MHB0    | 250 GB | 4       | 580   | 70    | 1.26   |
| Seagate   | ST3250620A         | 250 GB | 15      | 687   | 42    | 1.25   |
| WDC       | WD1600AAJS-00B4A0  | 160 GB | 20      | 695   | 70    | 1.25   |
| Toshiba   | MG04ACA100NY       | 1 TB   | 10      | 456   | 0     | 1.25   |
| Seagate   | ST380012A          | 80 GB  | 1       | 456   | 0     | 1.25   |
| WDC       | WD4003FFBX-68MU3N0 | 4 TB   | 1       | 456   | 0     | 1.25   |
| WDC       | WD2500AABS-00SDA0  | 250 GB | 1       | 455   | 0     | 1.25   |
| WDC       | WD20EZRX-22D8PB0   | 2 TB   | 4       | 454   | 0     | 1.25   |
| Hitachi   | HTS541610J9SA00    | 100 GB | 2       | 453   | 0     | 1.24   |
| WDC       | WD5000AZLX-00CL5A0 | 500 GB | 5       | 508   | 2     | 1.24   |
| WDC       | WD800JD-60LSA0     | 80 GB  | 5       | 715   | 158   | 1.24   |
| WDC       | WD6400BPVT-80HXZT3 | 640 GB | 8       | 690   | 9     | 1.24   |
| Samsung   | HD153WI            | 1.5 TB | 1       | 451   | 0     | 1.24   |
| Seagate   | ST380013AS         | 80 GB  | 36      | 1225  | 79    | 1.23   |
| Hitachi   | HDS5C1050CLA382    | 500 GB | 11      | 664   | 124   | 1.23   |
| Hitachi   | HDP725032GLA360    | 320 GB | 16      | 853   | 100   | 1.23   |
| Hitachi   | HDS728080PLA380... | 80 GB  | 1       | 449   | 0     | 1.23   |
| Hitachi   | HDT722525DLA380    | 250 GB | 12      | 1116  | 58    | 1.23   |
| WDC       | WD5000BEKT-00KA9T0 | 500 GB | 2       | 1084  | 7     | 1.23   |
| WDC       | WD60EZRX-00MVLB1   | 6 TB   | 2       | 448   | 0     | 1.23   |
| WDC       | WD2500AAJS-00V4A0  | 250 GB | 6       | 742   | 1     | 1.23   |
| Maxtor    | 6V080E0            | 82 GB  | 9       | 780   | 5     | 1.23   |
| ExcelStor | J360               | 64 GB  | 1       | 897   | 1     | 1.23   |
| Toshiba   | MK1234GAX          | 120 GB | 2       | 448   | 0     | 1.23   |
| Apple     | HDD ST1000DM003    | 1 TB   | 9       | 448   | 0     | 1.23   |
| Hitachi   | HTS541064A9E680    | 640 GB | 3       | 447   | 0     | 1.23   |
| WDC       | WD1000CHTZ-04JCPV0 | 1 TB   | 1       | 447   | 0     | 1.23   |
| WDC       | WD15EARX-00ZUDB0   | 1.5 TB | 2       | 776   | 3     | 1.22   |
| WDC       | WD3200YS-01PGB0    | 320 GB | 1       | 446   | 0     | 1.22   |
| Seagate   | ST3200820A         | 200 GB | 5       | 491   | 61    | 1.22   |
| Seagate   | ST3250624AS        | 250 GB | 14      | 942   | 101   | 1.22   |
| WDC       | WD1600AAJS-00Z4A0  | 160 GB | 1       | 445   | 0     | 1.22   |
| WDC       | WD800BEVS-08RST2   | 80 GB  | 3       | 445   | 0     | 1.22   |
| WDC       | WD10EFRX-68JCSN0   | 1 TB   | 13      | 750   | 304   | 1.22   |
| Seagate   | ST1000VX000-1CU162 | 1 TB   | 25      | 458   | 41    | 1.22   |
| WDC       | WD740GD-00FLA2     | 74 GB  | 1       | 1330  | 2     | 1.22   |
| Hitachi   | HDS721616PLA380    | 160 GB | 81      | 866   | 83    | 1.21   |
| WDC       | WD1600BEKT-75A25T0 | 160 GB | 1       | 442   | 0     | 1.21   |
| Seagate   | ST1000DM003-1ER162 | 1 TB   | 179     | 455   | 34    | 1.21   |
| WDC       | WD5000AAKS-65V0A0  | 500 GB | 3       | 907   | 6     | 1.21   |
| WDC       | WD20EADS-00R6B0    | 2 TB   | 7       | 884   | 291   | 1.21   |
| Seagate   | ST750LX003-1AC154  | 752 GB | 11      | 494   | 96    | 1.20   |
| Fujitsu   | MHZ2250BH G1       | 250 GB | 5       | 475   | 7     | 1.20   |
| Seagate   | ST3500312CS        | 500 GB | 25      | 716   | 197   | 1.20   |
| Toshiba   | MG03ACA400         | 4 TB   | 2       | 438   | 0     | 1.20   |
| WDC       | WD15EZRX-00DC0B0   | 1.5 TB | 1       | 438   | 0     | 1.20   |
| Seagate   | ST3200827AS        | 200 GB | 26      | 814   | 306   | 1.20   |
| Seagate   | ST3120026AS        | 120 GB | 28      | 1031  | 9     | 1.20   |
| WDC       | WD7500AARS-00Y5B1  | 752 GB | 11      | 504   | 3     | 1.20   |
| Hitachi   | HDS721025CLA382    | 250 GB | 20      | 720   | 210   | 1.20   |
| Seagate   | ST12000NE0007-2... | 12 TB  | 2       | 436   | 0     | 1.20   |
| WDC       | WD7500BPKT-60PK4T0 | 752 GB | 3       | 544   | 3     | 1.19   |
| Fujitsu   | MHV2080AT PL       | 80 GB  | 3       | 434   | 0     | 1.19   |
| WDC       | WD5000AAVS-00ZTB0  | 500 GB | 3       | 434   | 0     | 1.19   |
| HP        | VB0250EAVER        | 250 GB | 6       | 976   | 7     | 1.19   |
| WDC       | WD1600AAJS-60M0A0  | 160 GB | 3       | 527   | 31    | 1.19   |
| Seagate   | ST380817AS         | 80 GB  | 47      | 721   | 9     | 1.19   |
| WDC       | WD7500BPKX-80HPJT0 | 752 GB | 2       | 432   | 0     | 1.19   |
| WDC       | WD6400AAKS-00H2B0  | 640 GB | 1       | 432   | 0     | 1.19   |
| WDC       | WD1200BEVS-22RST0  | 120 GB | 3       | 458   | 1     | 1.18   |
| Maxtor    | 6V200E0            | 208 GB | 7       | 817   | 148   | 1.18   |
| WDC       | WD800JD-55MUA1     | 80 GB  | 9       | 615   | 8     | 1.18   |
| WDC       | WD5000AAKS-00WWPA0 | 500 GB | 8       | 648   | 10    | 1.18   |
| WDC       | WD10EZEX-60M2NA0   | 1 TB   | 17      | 589   | 96    | 1.18   |
| WDC       | WD20NMVW-11EDZS6   | 2 TB   | 4       | 431   | 0     | 1.18   |
| WDC       | WD10EZEX-22RKKA0   | 1 TB   | 8       | 555   | 4     | 1.18   |
| Seagate   | ST3120022A         | 120 GB | 36      | 645   | 20    | 1.18   |
| WDC       | WD10EZEX-21M2NA0   | 1 TB   | 27      | 476   | 1     | 1.18   |
| Hitachi   | HTS543216A7A384    | 160 GB | 2       | 430   | 0     | 1.18   |
| Hitachi   | HTE545025B9A300    | 250 GB | 1       | 430   | 0     | 1.18   |
| WDC       | WD1200JS-00MHB1    | 120 GB | 2       | 647   | 12    | 1.18   |
| WDC       | WD10JMVW-11AJGS1   | 1 TB   | 3       | 429   | 0     | 1.18   |
| Seagate   | ST3160212A         | 160 GB | 13      | 694   | 63    | 1.17   |
| Toshiba   | MG04ACA400E        | 4 TB   | 6       | 428   | 0     | 1.17   |
| WDC       | WD5000AAKS-00A7B2  | 500 GB | 30      | 847   | 14    | 1.17   |
| WDC       | WD5000BEVT-75A0RT0 | 500 GB | 7       | 610   | 59    | 1.17   |
| Seagate   | ST2000VX000-1CU164 | 2 TB   | 12      | 501   | 337   | 1.17   |
| WDC       | WD1200LB-55EDA0    | 120 GB | 1       | 425   | 0     | 1.17   |
| WDC       | WD5003AZEX-00K1GA0 | 500 GB | 21      | 473   | 52    | 1.16   |
| WDC       | WD5000LUCT-63Y8HY0 | 500 GB | 1       | 424   | 0     | 1.16   |
| Toshiba   | DT01ACA200         | 2 TB   | 117     | 462   | 37    | 1.16   |
| Fujitsu   | MHV2100AT PL       | 100 GB | 1       | 424   | 0     | 1.16   |
| Fujitsu   | MHZ2160BH G2       | 160 GB | 25      | 585   | 304   | 1.16   |
| WDC       | WD10EZRX-00L4HB0   | 1 TB   | 43      | 449   | 4     | 1.16   |
| WDC       | WD1001FALS-00E8B0  | 1 TB   | 12      | 976   | 187   | 1.16   |
| WDC       | WD20EURS-63S48Y0   | 2 TB   | 5       | 897   | 408   | 1.16   |
| WDC       | WD2500JS-00SGB0    | 250 GB | 5       | 570   | 1     | 1.16   |
| Seagate   | ST3750640AS        | 752 GB | 9       | 1073  | 318   | 1.16   |
| Maxtor    | STM380215AS        | 80 GB  | 11      | 652   | 534   | 1.16   |
| Seagate   | ST2000DM006-2DM164 | 2 TB   | 66      | 421   | 0     | 1.15   |
| WDC       | WD5000AAJS-22YFA0  | 500 GB | 6       | 781   | 352   | 1.15   |
| Toshiba   | MK1234GSX          | 120 GB | 8       | 681   | 4     | 1.15   |
| Hitachi   | HDP725040GLA360    | 400 GB | 3       | 1089  | 5     | 1.15   |
| Hitachi   | HTS725016A9A364    | 160 GB | 9       | 483   | 340   | 1.15   |
| WDC       | WD7500BPVT-75A1YT0 | 752 GB | 1       | 419   | 0     | 1.15   |
| WDC       | WD5003ABYX-01WERA0 | 500 GB | 10      | 787   | 4     | 1.15   |
| Hitachi   | HDT721032SLA360    | 320 GB | 21      | 896   | 11    | 1.15   |
| Hitachi   | HDP725025GLA380    | 250 GB | 34      | 820   | 79    | 1.14   |
| WDC       | WD5000AAKS-65A7B0  | 500 GB | 5       | 595   | 81    | 1.14   |
| Hitachi   | HDS721010CLA330    | 1 TB   | 34      | 615   | 36    | 1.14   |
| Maxtor    | STM3500630AS       | 500 GB | 1       | 416   | 0     | 1.14   |
| WDC       | WD5000BPVT-80HXZT3 | 500 GB | 21      | 469   | 53    | 1.14   |
| Hitachi   | HDS721032CLA362    | 320 GB | 41      | 729   | 26    | 1.14   |
| WDC       | WD10EZEX-22BN5A0   | 1 TB   | 16      | 504   | 2     | 1.14   |
| Samsung   | SP1654N            | 160 GB | 7       | 841   | 321   | 1.14   |
| WDC       | WD5000AAKX-07U6AA0 | 500 GB | 5       | 482   | 2     | 1.14   |
| Seagate   | ST1000NM0011       | 1 TB   | 11      | 1090  | 38    | 1.14   |
| WDC       | WD1600JS-08MHB0    | 160 GB | 1       | 414   | 0     | 1.14   |
| Seagate   | ST3250310AS        | 250 GB | 145     | 858   | 195   | 1.13   |
| WDC       | WD6400BPVT-60HXZT1 | 640 GB | 3       | 554   | 28    | 1.13   |
| Seagate   | ST9750422AS        | 752 GB | 3       | 846   | 207   | 1.13   |
| Seagate   | ST94813AS          | 40 GB  | 2       | 412   | 0     | 1.13   |
| Toshiba   | MK2575GSX          | 250 GB | 1       | 412   | 0     | 1.13   |
| Seagate   | ST380811AS         | 80 GB  | 63      | 657   | 481   | 1.13   |
| WDC       | WD5000BMVW-11AJGS1 | 500 GB | 1       | 411   | 0     | 1.13   |
| WDC       | WD1200BEVS-22UST0  | 120 GB | 25      | 515   | 65    | 1.13   |
| WDC       | WD5000BPKX-00HPJT0 | 500 GB | 2       | 411   | 0     | 1.13   |
| WDC       | WD5000AAVS-22G9B1  | 500 GB | 2       | 1446  | 6     | 1.13   |
| Maxtor    | 6V320F0            | 320 GB | 1       | 410   | 0     | 1.13   |
| Toshiba   | MQ03UBB200         | 2 TB   | 4       | 409   | 0     | 1.12   |
| WDC       | WD7500BPVT-24HXZT1 | 752 GB | 9       | 604   | 115   | 1.12   |
| WDC       | WD1600BEVS-26VAT0  | 160 GB | 3       | 409   | 0     | 1.12   |
| WDC       | WD10JPVT-08A1YT1   | 1 TB   | 2       | 408   | 0     | 1.12   |
| HGST      | HTS721075A9E630    | 752 GB | 8       | 408   | 0     | 1.12   |
| Seagate   | ST380819AS         | 80 GB  | 3       | 781   | 682   | 1.12   |
| Maxtor    | STM3250820A        | 250 GB | 6       | 591   | 218   | 1.12   |
| WDC       | WD800EB-11DJF0     | 80 GB  | 1       | 407   | 0     | 1.12   |
| WDC       | WD2000JB-00KFA0    | 200 GB | 1       | 1220  | 2     | 1.11   |
| WDC       | WD2500JD-00HBB0    | 250 GB | 1       | 406   | 0     | 1.11   |
| WDC       | WD7500BPVT-80HXZT3 | 752 GB | 11      | 468   | 2     | 1.11   |
| WDC       | WD2500AAKX-001CA0  | 250 GB | 28      | 530   | 104   | 1.11   |
| Samsung   | HM251HI            | 250 GB | 4       | 532   | 3     | 1.11   |
| Seagate   | ST3500418AS        | 500 GB | 336     | 749   | 188   | 1.11   |
| Samsung   | HD161GJ            | 160 GB | 18      | 621   | 120   | 1.11   |
| WDC       | WD10EURX-63C57Y0   | 1 TB   | 1       | 405   | 0     | 1.11   |
| Hitachi   | HTS721080G9AT00    | 80 GB  | 1       | 405   | 0     | 1.11   |
| Seagate   | ST3000VX000-9YW166 | 3 TB   | 1       | 405   | 0     | 1.11   |
| WDC       | WD5000AZRX-00L4HB0 | 500 GB | 20      | 404   | 0     | 1.11   |
| WDC       | WD2500AAKS-00V6A0  | 250 GB | 1       | 404   | 0     | 1.11   |
| WDC       | WD10EARS-00Z5B1    | 1 TB   | 9       | 946   | 123   | 1.11   |
| HGST      | HUS724040ALE640    | 4 TB   | 7       | 404   | 0     | 1.11   |
| Fujitsu   | MHZ2320BH G1       | 320 GB | 5       | 572   | 5     | 1.11   |
| Seagate   | ST4000DM005-2DP166 | 4 TB   | 10      | 403   | 0     | 1.10   |
| Seagate   | ST3250318AS        | 250 GB | 102     | 735   | 108   | 1.10   |
| Samsung   | HD753LJ            | 752 GB | 26      | 916   | 261   | 1.10   |
| Hitachi   | HDS5C3020BLE630    | 2 TB   | 2       | 1265  | 144   | 1.10   |
| Toshiba   | DT01ACA300         | 3 TB   | 54      | 443   | 38    | 1.10   |
| Seagate   | ST3250624A         | 250 GB | 1       | 1205  | 2     | 1.10   |
| HGST      | HUS726040ALE611    | 4 TB   | 1       | 401   | 0     | 1.10   |
| WDC       | WD5003ABYX-23 8... | 500 GB | 2       | 668   | 2     | 1.10   |
| WDC       | WD1600BEVS-07RST0  | 160 GB | 9       | 450   | 1     | 1.10   |
| Fujitsu   | MHW2080BH PL       | 80 GB  | 6       | 603   | 172   | 1.10   |
| Fujitsu   | MJA2160BH FFS G1   | 160 GB | 2       | 400   | 0     | 1.10   |
| WDC       | WD10EZEX-00BN5A0   | 1 TB   | 114     | 447   | 2     | 1.10   |
| Seagate   | ST3000VX010-2E3166 | 3 TB   | 4       | 414   | 1     | 1.10   |
| WDC       | WD2500AAKS-00VYA0  | 250 GB | 4       | 468   | 1     | 1.10   |
| Seagate   | ST8000NE0021-2E... | 8 TB   | 1       | 399   | 0     | 1.10   |
| WDC       | WD10EADS-11P8B2    | 1 TB   | 1       | 799   | 1     | 1.10   |
| HGST      | HUH721010ALN600    | 10 TB  | 1       | 399   | 0     | 1.09   |
| WDC       | WD10EZEX-19ZF5A0   | 1 TB   | 1       | 399   | 0     | 1.09   |
| WDC       | WD5000BPKT-22PK4T0 | 500 GB | 2       | 398   | 0     | 1.09   |
| Seagate   | ST500DM002-1BC142  | 500 GB | 52      | 572   | 116   | 1.09   |
| Samsung   | HD320KJ            | 320 GB | 3       | 615   | 55    | 1.09   |
| WDC       | WD2500BEVS-08VAT2  | 250 GB | 2       | 398   | 0     | 1.09   |
| WDC       | WD6400BEVT-80A0RT0 | 640 GB | 2       | 398   | 0     | 1.09   |
| Toshiba   | HDWE150            | 5 TB   | 6       | 398   | 0     | 1.09   |
| WDC       | WD5000AAKX-001CA0  | 500 GB | 170     | 699   | 48    | 1.09   |
| WDC       | WD2500BEVS-22UST0  | 250 GB | 45      | 510   | 14    | 1.09   |
| WDC       | WD2500JS-57MHB1    | 250 GB | 1       | 397   | 0     | 1.09   |
| WDC       | WD7500BPVX-60JC3T0 | 752 GB | 5       | 576   | 3     | 1.09   |
| Fujitsu   | MJA2250BH FFS G1   | 250 GB | 3       | 397   | 0     | 1.09   |
| Seagate   | ST3160215A         | 160 GB | 19      | 708   | 163   | 1.09   |
| WDC       | WD3200LPVX-08V0TT5 | 320 GB | 1       | 396   | 0     | 1.09   |
| WDC       | WD3200AAKS-00L6A0  | 320 GB | 3       | 579   | 4     | 1.09   |
| WDC       | WD3200AVVS-56L2B0  | 320 GB | 9       | 572   | 62    | 1.09   |
| WDC       | WD2500BEVT-22ZCT0  | 250 GB | 32      | 500   | 92    | 1.08   |
| WDC       | WD10PURX-64E5EY0   | 1 TB   | 8       | 413   | 1     | 1.08   |
| WDC       | WD10JPVX-08JC3T2   | 1 TB   | 6       | 409   | 1     | 1.08   |
| WDC       | WD5000AAKX-753CA1  | 500 GB | 6       | 1067  | 13    | 1.08   |
| WDC       | WD7500BPKT-22PK4T0 | 752 GB | 8       | 395   | 0     | 1.08   |
| Samsung   | HD321HJ            | 320 GB | 6       | 972   | 195   | 1.08   |
| WDC       | WD2001FASS-00U0B0  | 2 TB   | 1       | 1578  | 3     | 1.08   |
| WDC       | WD1200BEVS-00UST0  | 120 GB | 2       | 394   | 0     | 1.08   |
| WDC       | WD1003FBYZ-010FB0  | 1 TB   | 10      | 518   | 3     | 1.08   |
| Seagate   | ST1000DM003-9YN162 | 1 TB   | 115     | 645   | 263   | 1.08   |
| Seagate   | ST320LM000 HM321HI | 320 GB | 12      | 409   | 2     | 1.08   |
| WDC       | WD10EARS-00MVWB0   | 1 TB   | 34      | 944   | 32    | 1.08   |
| WDC       | WD2500LPVX-22V0TT0 | 250 GB | 1       | 391   | 0     | 1.07   |
| Seagate   | ST8000NM0055-1R... | 8 TB   | 2       | 391   | 0     | 1.07   |
| WDC       | WD2500AAJB-00J3A0  | 250 GB | 10      | 741   | 8     | 1.07   |
| WDC       | WD5000AADS-00S9B0  | 500 GB | 102     | 734   | 35    | 1.07   |
| Seagate   | ST320DM000-1BC14C  | 320 GB | 15      | 511   | 15    | 1.07   |
| Fujitsu   | MHV2040AH          | 40 GB  | 4       | 749   | 5     | 1.07   |
| Hitachi   | HTS723216A7A364    | 160 GB | 1       | 389   | 0     | 1.07   |
| WDC       | WD3200AAKS-00SBA0  | 320 GB | 10      | 710   | 24    | 1.06   |
| Hitachi   | HDS721680PLAT80    | 80 GB  | 5       | 866   | 4     | 1.06   |
| Seagate   | ST3000DM001-1CH166 | 3 TB   | 36      | 466   | 232   | 1.06   |
| WDC       | WD3200AAJS-22L7A0  | 320 GB | 9       | 776   | 27    | 1.06   |
| Seagate   | ST3160827AS        | 160 GB | 23      | 1005  | 230   | 1.06   |
| WDC       | WD5000AAKX-08ANVA0 | 500 GB | 2       | 386   | 0     | 1.06   |
| Apple     | HDD HTS541010A9... | 1 TB   | 2       | 386   | 0     | 1.06   |
| WDC       | WD5000AAKS-00UU3A0 | 500 GB | 52      | 721   | 33    | 1.06   |
| WDC       | WD2500BEKT-75PVMT0 | 250 GB | 7       | 563   | 13    | 1.05   |
| Seagate   | ST3250820ACE       | 250 GB | 3       | 520   | 698   | 1.05   |
| WDC       | WD5000BEVT-00A03T0 | 500 GB | 3       | 384   | 0     | 1.05   |
| WDC       | WD1600AAJS-75M0A0  | 160 GB | 7       | 758   | 3     | 1.05   |
| WDC       | WD800JD-22JNA0     | 80 GB  | 1       | 383   | 0     | 1.05   |
| WDC       | WD1600JS-08NCB1    | 160 GB | 5       | 565   | 27    | 1.05   |
| WDC       | WD800BB-75JHC0     | 80 GB  | 2       | 382   | 0     | 1.05   |
| Toshiba   | MK2559GSXP         | 250 GB | 4       | 450   | 7     | 1.05   |
| WDC       | WD3000HLHX-01JJPV0 | 304 GB | 2       | 455   | 2     | 1.05   |
| Seagate   | ST1500DM003-1CH16G | 1.5 TB | 7       | 416   | 2     | 1.05   |
| Seagate   | ST31000525SV       | 1 TB   | 3       | 769   | 20    | 1.05   |
| WDC       | WD2000JD-22HBB0    | 200 GB | 3       | 993   | 7     | 1.04   |
| WDC       | WD5000BEVT-00ZAT0  | 500 GB | 4       | 483   | 289   | 1.04   |
| WDC       | WD4000FYYZ-01UL1B1 | 4 TB   | 3       | 381   | 0     | 1.04   |
| Seagate   | ST3500514NS        | 500 GB | 7       | 1229  | 128   | 1.04   |
| WDC       | WD20EARX-55PASB0   | 2 TB   | 3       | 380   | 0     | 1.04   |
| Samsung   | HD161HJ 41R0186LEN | 160 GB | 1       | 380   | 0     | 1.04   |
| WDC       | WD5000LPLX-60ZNTT2 | 500 GB | 1       | 380   | 0     | 1.04   |
| WDC       | WD40E31X-00HY4A0   | 4 TB   | 1       | 380   | 0     | 1.04   |
| Seagate   | ST3120827AS        | 120 GB | 44      | 726   | 11    | 1.04   |
| WDC       | WD2500BEVS-60UST0  | 250 GB | 9       | 572   | 225   | 1.04   |
| Seagate   | ST2000NC001-1DY164 | 2 TB   | 5       | 378   | 0     | 1.04   |
| Toshiba   | HDWF180            | 8 TB   | 2       | 378   | 0     | 1.04   |
| WDC       | WD10EARS-00Y5B1    | 1 TB   | 91      | 858   | 93    | 1.04   |
| Seagate   | ST3200822AS        | 200 GB | 16      | 897   | 220   | 1.04   |
| Seagate   | ST4000NM0033-9Z... | 4 TB   | 5       | 430   | 348   | 1.03   |
| WDC       | WD2000JS-00SGB0    | 200 GB | 1       | 377   | 0     | 1.03   |
| WDC       | WD800AAJS-22WAA0   | 80 GB  | 2       | 376   | 0     | 1.03   |
| WDC       | WD3200AAKS-00V1A0  | 320 GB | 7       | 825   | 229   | 1.03   |
| WDC       | WD5000LPVT-08G33T1 | 500 GB | 12      | 385   | 1     | 1.03   |
| Seagate   | ST1000DM003-1CH162 | 1 TB   | 271     | 484   | 42    | 1.03   |
| Seagate   | ST2000DL001-9VT156 | 2 TB   | 6       | 1078  | 529   | 1.03   |
| WDC       | WD800BB-00JKA0     | 80 GB  | 1       | 374   | 0     | 1.03   |
| WDC       | WD5000BPKT-60PK4T0 | 500 GB | 4       | 659   | 67    | 1.03   |
| WDC       | WD7500BPKT-80PK4T0 | 752 GB | 5       | 781   | 5     | 1.03   |
| WDC       | WD1500HLFS-01G6U4  | 150 GB | 1       | 374   | 0     | 1.02   |
| WDC       | WD1600AAJS-00WAA0  | 160 GB | 8       | 531   | 5     | 1.02   |
| WDC       | WD10EZEX-08M2NA0   | 1 TB   | 63      | 406   | 5     | 1.02   |
| Hitachi   | HDS721050CLA360    | 500 GB | 65      | 534   | 37    | 1.02   |
| WDC       | WD5000AAKX-00ERMA0 | 500 GB | 99      | 532   | 5     | 1.02   |
| Seagate   | ST9402112A         | 40 GB  | 1       | 1117  | 2     | 1.02   |
| WDC       | WD3200BEVT-22ZCT0  | 320 GB | 80      | 463   | 96    | 1.02   |
| Seagate   | ST1000LM044 HN-... | 1 TB   | 2       | 559   | 404   | 1.02   |
| WDC       | WD1600JS-22NCB1    | 160 GB | 4       | 712   | 6     | 1.02   |
| Samsung   | HD322HJ            | 320 GB | 40      | 750   | 189   | 1.02   |
| Hitachi   | HDT721064SLA360    | 640 GB | 4       | 1035  | 6     | 1.02   |
| Seagate   | ST3160215AS        | 160 GB | 15      | 631   | 573   | 1.01   |
| Maxtor    | STM3160215AS       | 160 GB | 19      | 858   | 602   | 1.01   |
| Seagate   | ST500DM005 HD502HJ | 500 GB | 36      | 457   | 10    | 1.01   |
| WDC       | WD2500AAKX-00U6AA0 | 250 GB | 3       | 373   | 3     | 1.01   |
| WDC       | WD3200AAJS-60Z0A0  | 320 GB | 6       | 722   | 42    | 1.01   |
| WDC       | WD15EARS-00MVWB0   | 1.5 TB | 34      | 841   | 384   | 1.01   |
| WDC       | WD5000BEVT-60A0RT0 | 500 GB | 1       | 737   | 1     | 1.01   |
| Seagate   | ST3802110A         | 80 GB  | 36      | 630   | 513   | 1.01   |
| WDC       | WD800BB-22JHC0     | 80 GB  | 10      | 511   | 38    | 1.01   |
| WDC       | WD3200AAKS-00UU3A0 | 320 GB | 11      | 664   | 12    | 1.00   |
| WDC       | WD800BB-00FJA0     | 80 GB  | 6       | 443   | 35    | 1.00   |
| Seagate   | ST1000NC001-1DY162 | 1 TB   | 3       | 365   | 0     | 1.00   |
| HGST      | HTS725032A7E630    | 320 GB | 15      | 400   | 274   | 1.00   |
| WDC       | WD10EZEX-75M2NA0   | 1 TB   | 10      | 364   | 0     | 1.00   |
| WDC       | WD2500BEVT-35A23T0 | 250 GB | 24      | 514   | 28    | 1.00   |
| WDC       | WD5000AAKS-75V0A0  | 500 GB | 8       | 916   | 3     | 1.00   |
| Seagate   | ST10000NM0156-2... | 10 TB  | 4       | 363   | 0     | 1.00   |
| Seagate   | ST3750525AS        | 752 GB | 15      | 703   | 285   | 0.99   |
| Maxtor    | STM3160815AS       | 160 GB | 28      | 666   | 336   | 0.99   |
| WDC       | WD80EFZX-68UW8N0   | 8 TB   | 7       | 362   | 0     | 0.99   |
| Hitachi   | HDT722516DLA380    | 164 GB | 10      | 822   | 57    | 0.99   |
| Seagate   | ST9640423AS        | 640 GB | 4       | 949   | 380   | 0.99   |
| WDC       | WD800JB-00JJC0     | 80 GB  | 21      | 618   | 26    | 0.99   |
| WDC       | WD2500AAKX-07U6AA0 | 250 GB | 2       | 360   | 0     | 0.99   |
| WDC       | WD3200AAKB-00WHA0  | 320 GB | 1       | 360   | 0     | 0.99   |
| WDC       | WD740GD-00FLA0     | 74 GB  | 1       | 2521  | 6     | 0.99   |
| Maxtor    | STM3160212A        | 160 GB | 2       | 817   | 1     | 0.99   |
| WDC       | WD3200AAJS-00B4A0  | 320 GB | 19      | 844   | 119   | 0.99   |
| Seagate   | ST3120814A         | 120 GB | 16      | 760   | 363   | 0.98   |
| Seagate   | ST2000DX001-1CM164 | 2 TB   | 16      | 438   | 226   | 0.98   |
| Seagate   | ST500VT000-1DK142  | 500 GB | 8       | 359   | 0     | 0.98   |
| Seagate   | ST3160211AS        | 160 GB | 9       | 758   | 977   | 0.98   |
| WDC       | WD5000BPVT-22HXZT3 | 500 GB | 39      | 468   | 28    | 0.98   |
| WDC       | WD5000BEVT-24A0RT0 | 500 GB | 22      | 500   | 3     | 0.98   |
| WDC       | WD3200AAKX-00ERMA0 | 320 GB | 12      | 538   | 3     | 0.98   |
| Seagate   | ST3250310NS        | 250 GB | 3       | 737   | 755   | 0.98   |
| Fujitsu   | MHW2120BJ G2       | 120 GB | 1       | 356   | 0     | 0.98   |
| Toshiba   | MK5075GSX          | 500 GB | 19      | 466   | 297   | 0.98   |
| WDC       | WD7500BPVX-22JC3T0 | 752 GB | 18      | 398   | 1     | 0.97   |
| Hitachi   | HDS721680PLA380    | 80 GB  | 45      | 788   | 185   | 0.97   |
| WDC       | WD7501AALS-00E3A0  | 752 GB | 8       | 720   | 45    | 0.97   |
| WDC       | WD15EVDS-63V9B1    | 1.5 TB | 2       | 1117  | 6     | 0.97   |
| Toshiba   | MK8032GSX          | 80 GB  | 8       | 467   | 161   | 0.97   |
| WDC       | WD800JB-00JJA0     | 80 GB  | 3       | 1595  | 11    | 0.97   |
| Seagate   | ST3320820AS        | 320 GB | 13      | 493   | 315   | 0.97   |
| WDC       | WD3200AAJS-00M0A0  | 320 GB | 2       | 574   | 1     | 0.97   |
| Toshiba   | MK3261GSYG         | 320 GB | 1       | 354   | 0     | 0.97   |
| WDC       | WD3001FAEX-00MJRA0 | 3 TB   | 4       | 1352  | 3     | 0.97   |
| WDC       | WD10EADX-00TDHB0   | 1 TB   | 4       | 762   | 17    | 0.97   |
| WDC       | WD4000F9YZ-09N20L0 | 4 TB   | 1       | 353   | 0     | 0.97   |
| Hitachi   | HCP725032GLA380    | 320 GB | 2       | 1010  | 2     | 0.97   |
| WDC       | WD6400AACS-00M3B0  | 640 GB | 1       | 352   | 0     | 0.97   |
| Seagate   | ST980813ASG        | 80 GB  | 3       | 509   | 4     | 0.96   |
| WDC       | WD10JPVT-60A1YT0   | 1 TB   | 2       | 455   | 505   | 0.96   |
| Apple     | HDD HTS541010A9... | 1 TB   | 13      | 379   | 156   | 0.96   |
| WDC       | WD1600AAJS-08L7A0  | 160 GB | 8       | 961   | 161   | 0.96   |
| WDC       | WD5000AAKS-22V1A0  | 500 GB | 10      | 647   | 155   | 0.96   |
| Hitachi   | HDT725032VLA360    | 320 GB | 16      | 843   | 123   | 0.96   |
| WDC       | WD25EZRX-00MMMB0   | 2.5 TB | 1       | 1049  | 2     | 0.96   |
| Fujitsu   | MHY2200BH          | 200 GB | 15      | 571   | 39    | 0.96   |
| WDC       | WD3000BLFS-08YBU0  | 304 GB | 1       | 349   | 0     | 0.96   |
| WDC       | WD6000BLHX-01V7BV0 | 600 GB | 1       | 349   | 0     | 0.96   |
| Seagate   | ST3160811AS        | 160 GB | 81      | 789   | 432   | 0.96   |
| WDC       | WD10EZRX-00DC0B0   | 1 TB   | 4       | 348   | 0     | 0.96   |
| WDC       | WD5000LPVX-08V0TT6 | 500 GB | 1       | 348   | 0     | 0.95   |
| Seagate   | ST31000524AS       | 1 TB   | 174     | 606   | 204   | 0.95   |
| Seagate   | ST3250410AS        | 250 GB | 163     | 826   | 266   | 0.95   |
| WDC       | WD40EZRZ-22GXCB0   | 4 TB   | 4       | 346   | 0     | 0.95   |
| Toshiba   | MK6465GSXN         | 640 GB | 6       | 529   | 197   | 0.95   |
| WDC       | WD1600BEVS-08RST2  | 160 GB | 1       | 345   | 0     | 0.95   |
| WDC       | WD6400BPVT-16HXZT1 | 640 GB | 1       | 1037  | 2     | 0.95   |
| Seagate   | ST1500DL003-9VT16L | 1.5 TB | 29      | 817   | 268   | 0.95   |
| WDC       | WD3200BPVT-35ZEST0 | 320 GB | 22      | 468   | 2     | 0.95   |
| Seagate   | ST4000DX001-1CE168 | 4 TB   | 8       | 693   | 95    | 0.95   |
| Toshiba   | MQ01ACF032         | 320 GB | 7       | 345   | 0     | 0.95   |
| WDC       | WD5000BUCT-63LS5Y1 | 500 GB | 1       | 345   | 0     | 0.95   |
| WDC       | WD6400AARS-00Y5B1  | 640 GB | 15      | 767   | 11    | 0.95   |
| WDC       | WD10EZEX-60ZF5A0   | 1 TB   | 44      | 500   | 87    | 0.95   |
| Hitachi   | HTS545050B9A302    | 500 GB | 1       | 344   | 0     | 0.94   |
| WDC       | WD7500BPKT-00PK4T0 | 752 GB | 2       | 343   | 0     | 0.94   |
| WDC       | WD3200BPVT-55JJ5T0 | 320 GB | 5       | 396   | 195   | 0.94   |
| WDC       | WD2500AVVS-62L2B0  | 250 GB | 2       | 347   | 5     | 0.94   |
| Seagate   | ST2000LM003 HN-... | 2 TB   | 31      | 403   | 6     | 0.94   |
| Seagate   | ST3160021A         | 160 GB | 13      | 687   | 470   | 0.94   |
| Samsung   | HD251HJ            | 250 GB | 7       | 753   | 62    | 0.94   |
| WDC       | WD3200BVVT-63A26Y0 | 320 GB | 3       | 348   | 1     | 0.94   |
| WDC       | WD6400BPVT-55HXZT2 | 640 GB | 1       | 340   | 0     | 0.93   |
| WDC       | WD15EARX-22PASB0   | 1.5 TB | 1       | 340   | 0     | 0.93   |
| Seagate   | ST3250820A         | 250 GB | 10      | 874   | 535   | 0.93   |
| WDC       | WD7500BPVT-24HXZT3 | 752 GB | 11      | 379   | 24    | 0.93   |
| WDC       | WD800JD-32LSA0     | 80 GB  | 2       | 1577  | 53    | 0.93   |
| WDC       | WD2003FYYS-01T8B0  | 2 TB   | 1       | 3050  | 8     | 0.93   |
| WDC       | WD80EZZX-11CSGA0   | 8 TB   | 1       | 338   | 0     | 0.93   |
| WDC       | WD1600AAJB-00PVA0  | 160 GB | 10      | 616   | 181   | 0.93   |
| Samsung   | HM120JC            | 120 GB | 2       | 638   | 51    | 0.93   |
| WDC       | WD6400BPVT-22HXZT3 | 640 GB | 7       | 388   | 1     | 0.93   |
| Seagate   | ST4000LM024-2AN17V | 4 TB   | 3       | 457   | 1     | 0.93   |
| ExcelStor | J680               | 82 GB  | 1       | 1687  | 4     | 0.92   |
| IBM/Hi... | IC35L090AVV207-0   | 80 GB  | 2       | 735   | 2     | 0.92   |
| WDC       | WD2500AAJS-55M0A0  | 250 GB | 3       | 416   | 3     | 0.92   |
| WDC       | WD3200BEKX-75B7WT0 | 320 GB | 2       | 336   | 0     | 0.92   |
| WDC       | WD6400BEVT-00A0RT0 | 640 GB | 2       | 542   | 4     | 0.92   |
| Fujitsu   | MHV2100BH          | 100 GB | 5       | 680   | 22    | 0.92   |
| WDC       | WD5000LPVT-22G33T0 | 500 GB | 21      | 441   | 65    | 0.92   |
| Seagate   | ST31000528AS       | 1 TB   | 176     | 727   | 248   | 0.92   |
| WDC       | WD5000BHTZ-04JCPV0 | 500 GB | 1       | 334   | 0     | 0.92   |
| WDC       | WD800BB-00JHC0     | 80 GB  | 22      | 573   | 81    | 0.92   |
| WDC       | WD6002FRYZ-01WD5B0 | 6 TB   | 1       | 332   | 0     | 0.91   |
| Samsung   | HD503HI            | 500 GB | 15      | 567   | 17    | 0.91   |
| Seagate   | ST3320311CS        | 320 GB | 8       | 374   | 126   | 0.91   |
| WDC       | WD5000AADS-00M2B0  | 500 GB | 25      | 962   | 133   | 0.91   |
| WDC       | WD5003AZEX-00MK2A0 | 500 GB | 10      | 390   | 2     | 0.91   |
| WDC       | WD1001FALS-00U9B0  | 1 TB   | 1       | 995   | 2     | 0.91   |
| WDC       | WD1200BEVS-75UST0  | 120 GB | 11      | 436   | 2     | 0.91   |
| WDC       | WD20EARS-00J99B0   | 2 TB   | 2       | 331   | 0     | 0.91   |
| Seagate   | ST250DM001 HD253GJ | 250 GB | 7       | 330   | 0     | 0.91   |
| Fujitsu   | MHV2120AH          | 120 GB | 3       | 418   | 2     | 0.91   |
| WDC       | WD5000BPVT-00HXZT3 | 500 GB | 9       | 421   | 55    | 0.90   |
| Seagate   | ST12000VN0007-2... | 12 TB  | 4       | 328   | 0     | 0.90   |
| Hitachi   | HDT721075SLA360    | 752 GB | 1       | 328   | 0     | 0.90   |
| WDC       | WD5000LPVT-24G33T1 | 500 GB | 20      | 396   | 31    | 0.90   |
| WDC       | WD3200LPVX-80V0TT0 | 320 GB | 2       | 328   | 0     | 0.90   |
| WDC       | WD2500AVJS-63B6A0  | 250 GB | 3       | 768   | 6     | 0.90   |
| WDC       | WD30EZRZ-00Z5HB0   | 3 TB   | 15      | 356   | 1     | 0.90   |
| WDC       | WD3200BPVT-55ZEST0 | 320 GB | 3       | 356   | 1     | 0.90   |
| WDC       | WD7500BPVT-22HXZT3 | 752 GB | 26      | 377   | 1     | 0.90   |
| Seagate   | ST96812AS          | 64 GB  | 8       | 470   | 236   | 0.90   |
| Hitachi   | HTS545016B9SA00    | 160 GB | 1       | 327   | 0     | 0.90   |
| WDC       | WD2500AAJS-00Z0A0  | 250 GB | 3       | 819   | 4     | 0.90   |
| WDC       | WD7500BPVT-75HXZT3 | 752 GB | 5       | 456   | 1     | 0.90   |
| Seagate   | ST2000VN000-1HJ164 | 2 TB   | 2       | 326   | 0     | 0.90   |
| WDC       | WD5000AAJS-19A8B0  | 500 GB | 1       | 326   | 0     | 0.90   |
| WDC       | WD6400AAKS-40H2B0  | 640 GB | 2       | 1447  | 406   | 0.90   |
| WDC       | WD5000LPLX-66ZNTT0 | 500 GB | 1       | 326   | 0     | 0.89   |
| WDC       | WD10SPCX-75KHST0   | 1 TB   | 3       | 326   | 0     | 0.89   |
| WDC       | WD2500JS-60MHB5    | 250 GB | 3       | 946   | 13    | 0.89   |
| WDC       | WD1600AAJS-22L7A0  | 160 GB | 15      | 543   | 7     | 0.89   |
| WDC       | WD800BB-60JKA0     | 80 GB  | 1       | 325   | 0     | 0.89   |
| WDC       | WD5000BPVT-16HXZT3 | 500 GB | 1       | 324   | 0     | 0.89   |
| WDC       | WD3200JS-00PDB0    | 320 GB | 1       | 324   | 0     | 0.89   |
| WDC       | WD2500JS-58NCB1    | 250 GB | 2       | 773   | 308   | 0.89   |
| Seagate   | ST3250824A         | 250 GB | 4       | 753   | 253   | 0.88   |
| WDC       | WD5000AAKS-55V0A0  | 500 GB | 7       | 568   | 6     | 0.88   |
| WDC       | WD5000LPVT-75G33T0 | 500 GB | 5       | 366   | 1     | 0.88   |
| WDC       | WD5000AAKX-22ERMA0 | 500 GB | 35      | 462   | 2     | 0.88   |
| Seagate   | ST2000VN000-1H3164 | 2 TB   | 1       | 321   | 0     | 0.88   |
| WDC       | WD800BEVT-22ZCT0   | 80 GB  | 1       | 321   | 0     | 0.88   |
| WDC       | WD2500AAJS-08B4A0  | 250 GB | 2       | 931   | 1211  | 0.88   |
| WDC       | WD1003FBYX-01Y7B1  | 1 TB   | 24      | 589   | 3     | 0.88   |
| WDC       | WD10JPVT-55A1YT0   | 1 TB   | 1       | 320   | 0     | 0.88   |
| WDC       | WD7500BPVT-26HXZT3 | 752 GB | 1       | 1277  | 3     | 0.88   |
| WDC       | WD2500AAJS-00L7A0  | 250 GB | 25      | 644   | 14    | 0.87   |
| WDC       | WD5000AAKS-00V6A0  | 500 GB | 4       | 1185  | 12    | 0.87   |
| WDC       | WD5000BPVT-08HXZT3 | 500 GB | 8       | 372   | 2     | 0.87   |
| Seagate   | ST31000520AS       | 1 TB   | 15      | 930   | 403   | 0.87   |
| Seagate   | ST250DM000-1BC141  | 250 GB | 14      | 368   | 7     | 0.87   |
| WDC       | WD3200AAJS-61B4A0  | 320 GB | 2       | 431   | 4     | 0.87   |
| Samsung   | HD080HJ            | 80 GB  | 94      | 762   | 363   | 0.87   |
| WDC       | WD5000AAKS-60Z1A0  | 500 GB | 3       | 482   | 2     | 0.87   |
| WDC       | WD1600BEVT-22ZCT0  | 160 GB | 86      | 437   | 84    | 0.87   |
| Hitachi   | HTS545050B9A300    | 500 GB | 103     | 594   | 186   | 0.87   |
| WDC       | WD800BEVS-07RST0   | 80 GB  | 4       | 355   | 1     | 0.87   |
| Samsung   | HM641JI            | 640 GB | 20      | 520   | 54    | 0.87   |
| Samsung   | HD752LJ            | 752 GB | 2       | 1517  | 4     | 0.87   |
| Fujitsu   | MHV2100AT          | 100 GB | 1       | 316   | 0     | 0.87   |
| WDC       | WD3200AAKX-001CA0  | 320 GB | 28      | 667   | 15    | 0.87   |
| WDC       | WD60EFRX-68L0BN1   | 6 TB   | 15      | 468   | 4     | 0.87   |
| Seagate   | ST1000DX001-1CM162 | 1 TB   | 30      | 413   | 46    | 0.87   |
| WDC       | WD10EALX-008EA0    | 1 TB   | 5       | 325   | 1     | 0.86   |
| WDC       | WD800BEVS-00UST0   | 80 GB  | 1       | 315   | 0     | 0.86   |
| WDC       | WD7500BPKX-00HPJT0 | 752 GB | 6       | 315   | 0     | 0.86   |
| WDC       | WD6400BEVT-60A0RT0 | 640 GB | 2       | 382   | 18    | 0.86   |
| WDC       | WD2000JS-55MHB0    | 200 GB | 1       | 313   | 0     | 0.86   |
| WDC       | WD10JPVT-08A1YT2   | 1 TB   | 9       | 429   | 2     | 0.86   |
| WDC       | WD2000JB-00GVA0    | 200 GB | 3       | 580   | 101   | 0.86   |
| WDC       | WD800AAJS-00L7A0   | 80 GB  | 1       | 313   | 0     | 0.86   |
| Seagate   | ST9250410AS        | 250 GB | 38      | 502   | 185   | 0.85   |
| Seagate   | ST2000VM003-1ET164 | 2 TB   | 2       | 311   | 0     | 0.85   |
| Toshiba   | MQ01UBD100         | 1 TB   | 16      | 429   | 270   | 0.85   |
| Toshiba   | MK3263GSX          | 320 GB | 6       | 620   | 17    | 0.85   |
| WDC       | WD3200BPVT-75JJ5T0 | 320 GB | 3       | 386   | 3     | 0.85   |
| Seagate   | ST3500414CS        | 500 GB | 1       | 933   | 2     | 0.85   |
| IBM/Hi... | IC35L120AVV207-0   | 128 GB | 1       | 933   | 2     | 0.85   |
| Seagate   | ST2000VX002-1AH166 | 2 TB   | 1       | 311   | 0     | 0.85   |
| Seagate   | ST32000542AS       | 2 TB   | 22      | 770   | 367   | 0.85   |
| WDC       | WD10EALX-559BA0    | 1 TB   | 5       | 517   | 6     | 0.85   |
| WDC       | WD1600JS-40TGB0    | 160 GB | 1       | 308   | 0     | 0.85   |
| Samsung   | SP0812N            | 80 GB  | 6       | 607   | 4     | 0.85   |
| MediaMax  | WL5000GSA12872B    | 5 TB   | 1       | 308   | 0     | 0.85   |
| WDC       | WD5000BPVT-00HXZT1 | 500 GB | 15      | 437   | 112   | 0.84   |
| WDC       | WD5000LPVX-08V0TT2 | 500 GB | 3       | 387   | 3     | 0.84   |
| Seagate   | ST380215A          | 80 GB  | 27      | 458   | 109   | 0.84   |
| HGST      | HUH728080ALE604    | 8 TB   | 8       | 307   | 0     | 0.84   |
| Toshiba   | DT01ACA100         | 1 TB   | 248     | 339   | 9     | 0.84   |
| WDC       | WD5000AAKS-08WWPA0 | 500 GB | 2       | 1656  | 77    | 0.84   |
| WDC       | WD3200BEVT-00SCST0 | 320 GB | 1       | 306   | 0     | 0.84   |
| WDC       | WD5000BPVT-24HXZT3 | 500 GB | 19      | 359   | 1     | 0.84   |
| Samsung   | HD400LJ            | 400 GB | 2       | 480   | 5     | 0.84   |
| WDC       | WD1500ADFD-00NLR1  | 150 GB | 2       | 454   | 4     | 0.84   |
| Hitachi   | HTS725050A9A362    | 500 GB | 3       | 461   | 104   | 0.84   |
| WDC       | WD3200BPVT-00HXZT3 | 320 GB | 5       | 437   | 6     | 0.84   |
| Toshiba   | MK6459GSXP         | 640 GB | 10      | 427   | 299   | 0.83   |
| WDC       | WD5000LPVX-08V0TT5 | 500 GB | 11      | 336   | 1     | 0.83   |
| Samsung   | HD322GJ            | 320 GB | 28      | 508   | 118   | 0.83   |
| Hitachi   | HTS547575A9E384    | 640 GB | 106     | 506   | 422   | 0.83   |
| WDC       | WD10SPZX-11Z10T0   | 1 TB   | 1       | 302   | 0     | 0.83   |
| Hitachi   | HTS545032B9A300    | 320 GB | 91      | 494   | 126   | 0.83   |
| Samsung   | HD103UI            | 1 TB   | 2       | 483   | 9     | 0.83   |
| WDC       | WD3200AAJS-00YZCA0 | 320 GB | 14      | 511   | 8     | 0.83   |
| Fujitsu   | MHW2080BH          | 80 GB  | 4       | 477   | 4     | 0.82   |
| WDC       | WD400BD-55MTA1     | 40 GB  | 1       | 300   | 0     | 0.82   |
| Toshiba   | MK2561GSYN         | 250 GB | 3       | 303   | 16    | 0.82   |
| Seagate   | ST320011A          | 20 GB  | 6       | 555   | 5     | 0.82   |
| WDC       | WD600BEAS-22KZT0   | 64 GB  | 1       | 300   | 0     | 0.82   |
| WDC       | WD2500AAKS-00UU3A0 | 250 GB | 2       | 299   | 0     | 0.82   |
| Fujitsu   | MHW2160BH PL       | 160 GB | 8       | 547   | 7     | 0.82   |
| WDC       | WD5000BPVT-22HXZT1 | 500 GB | 18      | 456   | 2     | 0.82   |
| Seagate   | ST320DM000-1BD14C  | 320 GB | 32      | 433   | 74    | 0.81   |
| WDC       | WD5000BPKT-00PK4T0 | 500 GB | 4       | 317   | 1     | 0.81   |
| Samsung   | HD502HI            | 500 GB | 23      | 601   | 214   | 0.81   |
| Fujitsu   | MHX2300BT          | 304 GB | 3       | 759   | 47    | 0.81   |
| Toshiba   | MK4009GAL          | 40 GB  | 1       | 296   | 0     | 0.81   |
| WDC       | WD1600JS-00MHB0    | 160 GB | 7       | 691   | 166   | 0.81   |
| Seagate   | ST940210AS         | 40 GB  | 1       | 591   | 1     | 0.81   |
| WDC       | WD5000AVCS-732DY1  | 500 GB | 2       | 658   | 9     | 0.81   |
| Maxtor    | STM3250620A        | 250 GB | 1       | 295   | 0     | 0.81   |
| WDC       | WD5000AZLX-00JKKA0 | 500 GB | 6       | 295   | 0     | 0.81   |
| Seagate   | ST3160813AS        | 160 GB | 33      | 847   | 159   | 0.81   |
| Seagate   | ST750LM022 HN-M... | 752 GB | 89      | 387   | 28    | 0.81   |
| WDC       | WD800JD-22JNC0     | 80 GB  | 2       | 412   | 3     | 0.81   |
| Seagate   | ST3320820SCE       | 320 GB | 1       | 294   | 0     | 0.81   |
| WDC       | WD5000AZRZ-00HTKB0 | 500 GB | 9       | 293   | 0     | 0.81   |
| Samsung   | SV1203N            | 120 GB | 2       | 441   | 3     | 0.80   |
| Seagate   | STM3250318AS       | 250 GB | 23      | 578   | 177   | 0.80   |
| Hitachi   | HDS721616PLA320    | 160 GB | 3       | 1128  | 7     | 0.80   |
| Samsung   | HD403LJ            | 400 GB | 17      | 1112  | 485   | 0.80   |
| Maxtor    | STM3160211AS       | 160 GB | 3       | 624   | 349   | 0.80   |
| WDC       | WD20NMVW-11EDZS7   | 2 TB   | 5       | 471   | 245   | 0.80   |
| WDC       | WD2500AAJS-60Z0A0  | 250 GB | 2       | 291   | 0     | 0.80   |
| Seagate   | ST500DM002-1BD142  | 500 GB | 495     | 483   | 103   | 0.80   |
| WDC       | WD3200AAJS-22B4A0  | 320 GB | 4       | 1078  | 7     | 0.80   |
| WDC       | WD2500BEVS-75UST0  | 250 GB | 9       | 378   | 2     | 0.80   |
| Magnet... | MD02500-BJDW-RO    | 250 GB | 1       | 291   | 0     | 0.80   |
| WDC       | WD1600AAJS-60M0A1  | 160 GB | 2       | 779   | 11    | 0.80   |
| WDC       | WD10JPVX-22JC3T0   | 1 TB   | 134     | 315   | 12    | 0.80   |
| Hitachi   | HCS5C1025CLA382    | 250 GB | 1       | 290   | 0     | 0.80   |
| WDC       | WD10TMVW-11ZSMS5   | 1 TB   | 5       | 481   | 370   | 0.80   |
| Seagate   | OOS2000G           | 2 TB   | 1       | 289   | 0     | 0.79   |
| WDC       | WD5000AAKX-00U6AA0 | 500 GB | 17      | 383   | 3     | 0.79   |
| IBM/Hi... | IC35L120AVV207-1   | 128 GB | 1       | 288   | 0     | 0.79   |
| Fujitsu   | MHV2080BH          | 80 GB  | 3       | 405   | 3     | 0.79   |
| Fujitsu   | MHY2120BH          | 120 GB | 26      | 520   | 217   | 0.79   |
| WDC       | WD2500AAKS-00B3A0  | 250 GB | 4       | 713   | 8     | 0.79   |
| WDC       | WD3000GLFS-01F8U0  | 304 GB | 1       | 287   | 0     | 0.79   |
| Maxtor    | STM380811AS        | 80 GB  | 4       | 500   | 5     | 0.79   |
| Toshiba   | MK3029GAC          | 32 GB  | 1       | 287   | 0     | 0.79   |
| WDC       | WD5000AAKX-75U6AA0 | 500 GB | 10      | 460   | 2     | 0.79   |
| WDC       | WD4004FZWX-00GBGB0 | 4 TB   | 3       | 707   | 794   | 0.79   |
| WDC       | WD3200BPVT-24JJ5T0 | 320 GB | 58      | 344   | 62    | 0.79   |
| WDC       | WD1200BEVT-22ZCT0  | 120 GB | 1       | 286   | 0     | 0.79   |
| WDC       | WD1200BEVS-75RST0  | 120 GB | 3       | 286   | 0     | 0.78   |
| Toshiba   | MK4025GAS          | 40 GB  | 1       | 571   | 1     | 0.78   |
| WDC       | WD3200BPVT-22ZEST0 | 320 GB | 54      | 432   | 66    | 0.78   |
| WDC       | WD40EFRX-68N32N0   | 4 TB   | 39      | 296   | 1     | 0.78   |
| WDC       | WD1600JD-22HBB0    | 160 GB | 1       | 1710  | 5     | 0.78   |
| Toshiba   | HDWA130            | 3 TB   | 1       | 285   | 0     | 0.78   |
| Samsung   | HD250HJ            | 250 GB | 35      | 797   | 615   | 0.78   |
| WDC       | WD3200BEVT-80A0RT0 | 320 GB | 36      | 454   | 21    | 0.78   |
| Samsung   | HM321HI            | 320 GB | 92      | 442   | 95    | 0.78   |
| HP        | MB2000GCWLT        | 2 TB   | 1       | 1419  | 4     | 0.78   |
| WDC       | WD10JMVW-11AJGS4   | 1 TB   | 15      | 283   | 0     | 0.78   |
| Toshiba   | MK4058GSX          | 400 GB | 3       | 452   | 3     | 0.78   |
| Hitachi   | HDS721032CLA662    | 320 GB | 1       | 283   | 0     | 0.78   |
| Seagate   | ST31000340NS       | 1 TB   | 16      | 1333  | 296   | 0.77   |
| Samsung   | HM500JI            | 500 GB | 28      | 448   | 3     | 0.77   |
| WDC       | WD10EZRX-00D8PB0   | 1 TB   | 13      | 354   | 2     | 0.77   |
| WDC       | WD15EARS-00Z5B1    | 1.5 TB | 26      | 1119  | 504   | 0.77   |
| Samsung   | HN-M500MBB         | 500 GB | 38      | 404   | 21    | 0.77   |
| Toshiba   | MQ01ABD075         | 752 GB | 84      | 365   | 17    | 0.77   |
| WDC       | WD2500BEKT-00PVMT0 | 250 GB | 2       | 279   | 0     | 0.77   |
| Samsung   | HD256GJ            | 250 GB | 1       | 279   | 0     | 0.77   |
| Fujitsu   | MHW2100BH          | 100 GB | 1       | 279   | 0     | 0.76   |
| WDC       | WD100EB-00BHF0     | 10 GB  | 1       | 557   | 1     | 0.76   |
| WDC       | WD10JPVX-16JC3T3   | 1 TB   | 3       | 278   | 0     | 0.76   |
| Hitachi   | HDP725050GLAT80    | 500 GB | 1       | 278   | 0     | 0.76   |
| Fujitsu   | MHY2080BH          | 80 GB  | 2       | 557   | 3     | 0.76   |
| WDC       | WD40EZRX-11SPEB0   | 4 TB   | 1       | 277   | 0     | 0.76   |
| Seagate   | ST3120813AS        | 120 GB | 21      | 888   | 567   | 0.76   |
| Samsung   | HD401LJ            | 400 GB | 4       | 702   | 14    | 0.76   |
| WDC       | WD5000AAKX-221CA0  | 500 GB | 2       | 1008  | 5     | 0.76   |
| Seagate   | ST3500830AS        | 500 GB | 7       | 683   | 443   | 0.76   |
| Seagate   | ST250LT007-9ZV14C  | 250 GB | 2       | 276   | 0     | 0.76   |
| WDC       | WD2500JB-00REA0    | 250 GB | 9       | 714   | 24    | 0.76   |
| Samsung   | HD321KJ            | 320 GB | 58      | 737   | 327   | 0.76   |
| Samsung   | HD161HJ            | 160 GB | 44      | 930   | 499   | 0.76   |
| WDC       | WD5000BPKX-60HPJT0 | 500 GB | 4       | 275   | 0     | 0.76   |
| Seagate   | ST5000LM000-2AN170 | 5 TB   | 8       | 275   | 0     | 0.76   |
| WDC       | WD1600BEVT-00ZCT0  | 160 GB | 5       | 289   | 1     | 0.75   |
| WDC       | WD1200JS-00NCB1    | 120 GB | 2       | 591   | 27    | 0.75   |
| WDC       | WD2000JD-00HBB0    | 200 GB | 4       | 718   | 4     | 0.75   |
| Seagate   | STM3320418AS       | 320 GB | 10      | 644   | 140   | 0.75   |
| WDC       | WD800BB-56JKC0     | 80 GB  | 6       | 735   | 7     | 0.75   |
| Seagate   | ST3000DM008-2DM166 | 3 TB   | 21      | 297   | 33    | 0.75   |
| WDC       | WD10JPVX-11JC3T0   | 1 TB   | 2       | 274   | 0     | 0.75   |
| Samsung   | HD082GJ            | 80 GB  | 13      | 586   | 340   | 0.75   |
| Seagate   | ST1000DX001-1NS162 | 1 TB   | 6       | 438   | 3     | 0.75   |
| WDC       | WD1600AAJS-00YZCA0 | 160 GB | 10      | 499   | 36    | 0.75   |
| Samsung   | HD160JJ            | 160 GB | 67      | 840   | 453   | 0.75   |
| WDC       | WD1600AABS-62PRA0  | 160 GB | 1       | 273   | 0     | 0.75   |
| WDC       | WD800BEVS-22RST0   | 80 GB  | 25      | 422   | 61    | 0.75   |
| WDC       | WD3200AZRX-00A8LB0 | 320 GB | 3       | 273   | 0     | 0.75   |
| Seagate   | ST320LT009-9WC142  | 320 GB | 1       | 546   | 1     | 0.75   |
| WDC       | WD2500AAKX-00ERMA0 | 250 GB | 22      | 453   | 63    | 0.75   |
| WDC       | WD5000LPVX-60V0TT0 | 500 GB | 13      | 369   | 14    | 0.74   |
| WDC       | WD3000FYYZ-01UL1B3 | 3 TB   | 1       | 271   | 0     | 0.74   |
| WDC       | WD3200AAJS-00L7A0  | 320 GB | 67      | 730   | 54    | 0.74   |
| WDC       | WD5000AAKX-221CA1  | 500 GB | 12      | 587   | 24    | 0.74   |
| WDC       | WD5000BPKT-75PK4T0 | 500 GB | 9       | 491   | 4     | 0.74   |
| Seagate   | ST1500LM012-1R817G | 1.5 TB | 2       | 269   | 0     | 0.74   |
| WDC       | WD3200BEVT-00A0RT0 | 320 GB | 18      | 319   | 12    | 0.74   |
| WDC       | WD1200BEVS-07RST0  | 120 GB | 2       | 268   | 0     | 0.74   |
| Toshiba   | MK1031GAS          | 100 GB | 3       | 433   | 3     | 0.74   |
| Fujitsu   | MJA2160BH G2       | 160 GB | 6       | 404   | 208   | 0.74   |
| Seagate   | ST1000LM014-1EJ... | 1 TB   | 10      | 371   | 16    | 0.74   |
| WDC       | WD2500AAJB-57R1A0  | 250 GB | 1       | 268   | 0     | 0.73   |
| WDC       | WD5000M22K-24Z1... | 500 GB | 1       | 267   | 0     | 0.73   |
| WDC       | WD2500BEVT-00A23T0 | 250 GB | 8       | 582   | 9     | 0.73   |
| WDC       | WD1200JD-22HBB0    | 120 GB | 2       | 1602  | 5     | 0.73   |
| Maxtor    | STM380815AS        | 80 GB  | 20      | 684   | 665   | 0.73   |
| WDC       | WD3200LPVT-00FMCT0 | 320 GB | 1       | 266   | 0     | 0.73   |
| Fujitsu   | MHW2160BH          | 160 GB | 3       | 493   | 30    | 0.73   |
| Seagate   | ST9750420AS        | 752 GB | 46      | 463   | 86    | 0.73   |
| WDC       | WD3200LPVX-60V0TT0 | 320 GB | 1       | 266   | 0     | 0.73   |
| WDC       | WD5000LMVW-11CKRS0 | 500 GB | 2       | 265   | 0     | 0.73   |
| WDC       | WD6000HLHX-01JJPV0 | 600 GB | 6       | 482   | 5     | 0.73   |
| Seagate   | ST9160411ASG       | 160 GB | 2       | 676   | 4     | 0.73   |
| WDC       | WD5000AAKS-65A7B2  | 500 GB | 1       | 265   | 0     | 0.73   |
| WDC       | WD2500AAKS-61L9A0  | 250 GB | 1       | 265   | 0     | 0.73   |
| WDC       | WD2500BEKT-00A25T0 | 250 GB | 1       | 264   | 0     | 0.73   |
| WDC       | WD2500AAKX-321CA0  | 250 GB | 1       | 264   | 0     | 0.72   |
| Maxtor    | STM3250820AS       | 250 GB | 11      | 812   | 279   | 0.72   |
| Seagate   | ST6000NM0115-1Y... | 6 TB   | 5       | 263   | 0     | 0.72   |
| WDC       | WD2500BEKX-00B7WT0 | 250 GB | 2       | 263   | 0     | 0.72   |
| WDC       | WD5000AAKX-08ERMA0 | 500 GB | 18      | 473   | 133   | 0.72   |
| Maxtor    | 6L040J2            | 40 GB  | 1       | 1576  | 5     | 0.72   |
| Seagate   | ST9640320AS        | 640 GB | 10      | 461   | 295   | 0.72   |
| Seagate   | ST500LM000-1EJ1... | 500 GB | 8       | 304   | 47    | 0.72   |
| HGST      | HCC545050A7E380    | 500 GB | 1       | 523   | 1     | 0.72   |
| Fujitsu   | MHZ2250BH G2       | 250 GB | 12      | 598   | 519   | 0.72   |
| WDC       | WD1600BEVS-60RST0  | 160 GB | 9       | 507   | 254   | 0.72   |
| Seagate   | ST3160023AS        | 160 GB | 14      | 928   | 36    | 0.72   |
| WDC       | WD6401AALS-00E3A0  | 640 GB | 4       | 602   | 5     | 0.71   |
| WDC       | WD10JPVX-60JC3T0   | 1 TB   | 27      | 315   | 72    | 0.71   |
| Toshiba   | MK5065GSXF         | 500 GB | 9       | 375   | 4     | 0.71   |
| Seagate   | ST340016A          | 40 GB  | 31      | 563   | 30    | 0.71   |
| WDC       | WD20EURX-63T0FY0   | 2 TB   | 9       | 417   | 229   | 0.71   |
| IBM/Hi... | IC35L040AVVA07-0   | 41 GB  | 4       | 623   | 83    | 0.71   |
| WDC       | WD1000DHTZ-04N21V0 | 1 TB   | 2       | 825   | 4     | 0.71   |
| WDC       | WD5000AAKS-00E4A0  | 500 GB | 8       | 834   | 26    | 0.71   |
| WDC       | WD1600BEVT-75ZCT2  | 160 GB | 13      | 405   | 159   | 0.71   |
| Hitachi   | HTS542516K9A300    | 160 GB | 6       | 790   | 220   | 0.71   |
| WDC       | WD1600JS-60MHB5    | 160 GB | 3       | 862   | 30    | 0.71   |
| WDC       | WD5000BPVT-35HXZT1 | 500 GB | 4       | 259   | 0     | 0.71   |
| Seagate   | ST330013A          | 32 GB  | 1       | 259   | 0     | 0.71   |
| WDC       | WD3200BPVT-22JJ5T0 | 320 GB | 110     | 325   | 51    | 0.71   |
| Seagate   | ST91208220AS       | 120 GB | 2       | 461   | 507   | 0.71   |
| WDC       | WD40EZRZ-00GXCB0   | 4 TB   | 24      | 258   | 0     | 0.71   |
| HGST      | HTS541075A9E680    | 752 GB | 30      | 336   | 443   | 0.71   |
| Toshiba   | DT01ACA050         | 500 GB | 284     | 295   | 25    | 0.71   |
| Seagate   | ST1500LM006 HN-... | 1.5 TB | 4       | 257   | 0     | 0.70   |
| Samsung   | HD203WI            | 2 TB   | 1       | 256   | 0     | 0.70   |
| Toshiba   | HDWL110            | 1 TB   | 5       | 256   | 0     | 0.70   |
| Seagate   | ST1000DM010-2DM162 | 1 TB   | 3       | 256   | 0     | 0.70   |
| WDC       | WD2500BEKT-60PVMT0 | 250 GB | 11      | 346   | 92    | 0.70   |
| WDC       | WD7500BPVT-55HXZT3 | 752 GB | 2       | 465   | 4     | 0.70   |
| WDC       | WD3200BEKT-60V5T1  | 320 GB | 23      | 519   | 360   | 0.70   |
| Hitachi   | HTS545025B9A300    | 250 GB | 110     | 484   | 118   | 0.70   |
| Fujitsu   | MHX2250BT          | 250 GB | 2       | 409   | 5     | 0.70   |
| Hitachi   | HTS545032B9SA02    | 320 GB | 2       | 840   | 30    | 0.70   |
| Maxtor    | STM3320620AS       | 320 GB | 2       | 254   | 0     | 0.70   |
| Hitachi   | HTS545032A7E380    | 320 GB | 21      | 359   | 102   | 0.70   |
| WDC       | WD3200BEKT-00F3T0  | 320 GB | 2       | 253   | 0     | 0.69   |
| WDC       | WD5000AAKX-08U6AA0 | 500 GB | 39      | 325   | 7     | 0.69   |
| WDC       | WD7500AZEX-00BN5A0 | 752 GB | 1       | 252   | 0     | 0.69   |
| WDC       | WD5000BPVT-75HXZT3 | 500 GB | 18      | 473   | 3     | 0.69   |
| WDC       | WD20EZRX-60D8PB0   | 2 TB   | 1       | 252   | 0     | 0.69   |
| WDC       | WD5000AAKS-07A7B0  | 500 GB | 3       | 754   | 6     | 0.69   |
| Toshiba   | MQ04UBF100         | 1 TB   | 7       | 252   | 0     | 0.69   |
| WDC       | WD10JPVT-75A1YT0   | 1 TB   | 8       | 398   | 2     | 0.69   |
| WDC       | WD7500BPVT-60HXZT3 | 752 GB | 8       | 554   | 134   | 0.69   |
| Seagate   | ST250DM000-1BD141  | 250 GB | 85      | 467   | 130   | 0.69   |
| WDC       | WD5000AAKB-00H8A0  | 500 GB | 15      | 547   | 7     | 0.69   |
| Samsung   | HD163GJ            | 160 GB | 1       | 251   | 0     | 0.69   |
| Maxtor    | 6L020J1            | 20 GB  | 2       | 463   | 3     | 0.69   |
| WDC       | WD10EZEX-00WN4A0   | 1 TB   | 36      | 291   | 1     | 0.69   |
| Seagate   | ST500DM009-2DM14C  | 500 GB | 2       | 250   | 0     | 0.69   |
| Seagate   | ST500LM012 HN-M... | 500 GB | 166     | 353   | 47    | 0.69   |
| WDC       | WD5000AAKS-00V1A0  | 500 GB | 50      | 759   | 330   | 0.68   |
| WDC       | WD2500AAJS-00B4A0  | 250 GB | 16      | 689   | 63    | 0.68   |
| WDC       | WD3200AAJS-60M0A0  | 320 GB | 1       | 749   | 2     | 0.68   |
| WDC       | WD2500BEVT-24A23T0 | 250 GB | 24      | 432   | 68    | 0.68   |
| WDC       | WD1600BEVT-88ZCT0  | 160 GB | 1       | 247   | 0     | 0.68   |
| WDC       | WD5000AAKX-083CA1  | 500 GB | 9       | 619   | 86    | 0.68   |
| WDC       | WD2500BEVT-60ZCT1  | 250 GB | 6       | 394   | 10    | 0.68   |
| Fujitsu   | MHV2060BH          | 64 GB  | 7       | 483   | 9     | 0.68   |
| WDC       | WD3200BPVT-80JJ5T0 | 320 GB | 56      | 316   | 55    | 0.68   |
| Seagate   | ST320LM001 HN-M... | 320 GB | 35      | 277   | 1     | 0.68   |
| WDC       | WD2000JS-00MHB1    | 200 GB | 1       | 246   | 0     | 0.68   |
| Fujitsu   | MHV2080AH          | 80 GB  | 6       | 503   | 3     | 0.68   |
| Hitachi   | HCT721016SLA380    | 160 GB | 3       | 246   | 0     | 0.67   |
| Fujitsu   | MJA2500BH FFS G1   | 500 GB | 1       | 246   | 0     | 0.67   |
| Samsung   | HM320HJ            | 320 GB | 3       | 419   | 422   | 0.67   |
| Seagate   | ST980813AS         | 80 GB  | 1       | 246   | 0     | 0.67   |
| WDC       | WD2503ABYX-01WERA1 | 256 GB | 4       | 619   | 3     | 0.67   |
| Samsung   | HD155UI            | 1.5 TB | 2       | 808   | 11    | 0.67   |
| WDC       | WD5000AAKS-22A7B2  | 500 GB | 6       | 1007  | 120   | 0.67   |
| WDC       | WD10EZEX-07ZF5A0   | 1 TB   | 1       | 982   | 3     | 0.67   |
| WDC       | WD3200LPVX-22V0TT0 | 320 GB | 13      | 272   | 1     | 0.67   |
| WDC       | WD7500BPVT-22A1YT0 | 752 GB | 1       | 733   | 2     | 0.67   |
| Hitachi   | HDT721025SLA380    | 250 GB | 11      | 788   | 188   | 0.67   |
| HGST      | HTS721010A9E630    | 1 TB   | 211     | 292   | 124   | 0.67   |
| WDC       | WD5000BEVT-11A0RT0 | 500 GB | 1       | 243   | 0     | 0.67   |
| WDC       | WD4000FYYZ-01UL1B0 | 4 TB   | 1       | 2193  | 8     | 0.67   |
| WDC       | WD100EZAZ-11TDBA0  | 10 TB  | 3       | 243   | 0     | 0.67   |
| WDC       | WD1600AAJB-22WRA0  | 160 GB | 2       | 722   | 3     | 0.67   |
| WDC       | WD5000LPVT-00G33T0 | 500 GB | 5       | 581   | 3     | 0.66   |
| WDC       | WD10EAVS-22D7B0    | 1 TB   | 1       | 2174  | 8     | 0.66   |
| Fujitsu   | MHW2080AT          | 80 GB  | 1       | 241   | 0     | 0.66   |
| WDC       | WD5000LPVT-00FMCT0 | 500 GB | 6       | 247   | 1     | 0.66   |
| Seagate   | ST4000VM000-2AF166 | 4 TB   | 1       | 240   | 0     | 0.66   |
| WDC       | WD7500BPKT-75PK4T0 | 752 GB | 13      | 408   | 3     | 0.66   |
| Seagate   | ST2000DX002-2DV164 | 2 TB   | 21      | 239   | 0     | 0.66   |
| Seagate   | ST3000NC002-1DY166 | 3 TB   | 2       | 987   | 1494  | 0.66   |
| Seagate   | ST8000DM004-2CX188 | 8 TB   | 14      | 276   | 108   | 0.65   |
| Toshiba   | MK6034GAX          | 64 GB  | 2       | 879   | 5     | 0.65   |
| Samsung   | HM320II            | 320 GB | 16      | 389   | 255   | 0.65   |
| WDC       | WD5000LPVX-80V0TT0 | 500 GB | 39      | 261   | 53    | 0.65   |
| Seagate   | STM3500418AS       | 500 GB | 21      | 824   | 462   | 0.65   |
| WDC       | WD5000LPVX-75V0TT0 | 500 GB | 25      | 261   | 2     | 0.65   |
| WDC       | WD10JPVX-80JC3T0   | 1 TB   | 8       | 237   | 0     | 0.65   |
| Hitachi   | HTS541010G9AT00    | 100 GB | 1       | 474   | 1     | 0.65   |
| Seagate   | ST1000LM024 HN-... | 1 TB   | 484     | 337   | 54    | 0.65   |
| Hitachi   | HTS725050A7E630    | 500 GB | 8       | 375   | 670   | 0.65   |
| Hitachi   | HTS547550A9E384    | 500 GB | 126     | 405   | 298   | 0.65   |
| Seagate   | ST320LM010-1KJ15C  | 320 GB | 5       | 476   | 4     | 0.65   |
| Seagate   | ST250LT003-9YG14C  | 250 GB | 3       | 235   | 0     | 0.65   |
| Seagate   | ST500LM014 HN-M... | 500 GB | 2       | 480   | 1     | 0.65   |
| Seagate   | ST500LM011 HM501II | 500 GB | 2       | 277   | 1     | 0.64   |
| WDC       | WD3200BEVS-26VAT0  | 320 GB | 1       | 235   | 0     | 0.64   |
| HGST      | HTS545032A7E680    | 320 GB | 16      | 299   | 19    | 0.64   |
| WDC       | WD10SPZX-75Z10T0   | 1 TB   | 3       | 234   | 0     | 0.64   |
| WDC       | WD3200BEKT-75KA9T0 | 320 GB | 1       | 234   | 0     | 0.64   |
| Maxtor    | STM3250310AS       | 250 GB | 62      | 713   | 376   | 0.64   |
| WDC       | WD1600JS-60NCB1    | 160 GB | 5       | 603   | 64    | 0.64   |
| WDC       | WD5003ABYX-23 0... | 500 GB | 1       | 234   | 0     | 0.64   |
| WDC       | WD5000AADS-67S9B0  | 500 GB | 1       | 2104  | 8     | 0.64   |
| WDC       | WD3200BEVT-08A23T1 | 320 GB | 4       | 294   | 2     | 0.64   |
| WDC       | WD2500AAKX-08U6AA0 | 250 GB | 3       | 479   | 3     | 0.64   |
| Hitachi   | HTS542516K9SA00    | 160 GB | 50      | 639   | 183   | 0.64   |
| WDC       | WD6400BPVT-26HXZT1 | 640 GB | 1       | 232   | 0     | 0.64   |
| HGST      | HTS725032A7E635... | 320 GB | 1       | 231   | 0     | 0.64   |
| WDC       | WD800BB-00FRA0     | 80 GB  | 4       | 704   | 12    | 0.63   |
| HGST      | HUS726060ALE610    | 6 TB   | 1       | 230   | 0     | 0.63   |
| Seagate   | ST360014A          | 64 GB  | 4       | 584   | 12    | 0.63   |
| Hitachi   | HTS721080G9SA00    | 80 GB  | 6       | 383   | 34    | 0.63   |
| Hitachi   | HDS721010KLA330    | 1 TB   | 7       | 546   | 19    | 0.63   |
| WDC       | WD5000BPVT-22A1YT0 | 500 GB | 7       | 229   | 0     | 0.63   |
| Toshiba   | Generic L200 Ha... | 2 TB   | 2       | 229   | 0     | 0.63   |
| Hitachi   | HDS725050KLA360    | 500 GB | 4       | 1530  | 15    | 0.63   |
| Seagate   | ST3160212ACE       | 160 GB | 4       | 512   | 27    | 0.63   |
| Seagate   | ST9120822AS        | 120 GB | 42      | 445   | 387   | 0.63   |
| WDC       | WD800BB-98JHC0     | 80 GB  | 1       | 1829  | 7     | 0.63   |
| Seagate   | ST9160821A         | 160 GB | 3       | 412   | 12    | 0.63   |
| Samsung   | HM100UI            | 1 TB   | 3       | 228   | 0     | 0.63   |
| WDC       | WD5000BEKT-60KA9T0 | 500 GB | 3       | 324   | 1     | 0.63   |
| Toshiba   | MK1059GSM          | 1 TB   | 27      | 593   | 811   | 0.63   |
| Hitachi   | HDS721010DLE630    | 1 TB   | 39      | 748   | 611   | 0.63   |
| WDC       | WD10EADS-22M2B0    | 1 TB   | 6       | 946   | 8     | 0.63   |
| ExcelStor | J8160S             | 160 GB | 6       | 445   | 3     | 0.62   |
| WDC       | WD3200AAKS-00V6A0  | 320 GB | 3       | 315   | 1     | 0.62   |
| Hitachi   | HTS547564A9E384    | 640 GB | 33      | 527   | 481   | 0.62   |
| WDC       | WD5000LPVX-22V0TT0 | 500 GB | 168     | 272   | 11    | 0.62   |
| Hitachi   | HTS545016B9A300    | 160 GB | 44      | 325   | 54    | 0.62   |
| WDC       | WD2500YD-01NVB1    | 256 GB | 1       | 1357  | 5     | 0.62   |
| WDC       | WD5000BEKT-80KA9T1 | 500 GB | 4       | 280   | 1     | 0.62   |
| Toshiba   | MQ01ABD032         | 320 GB | 80      | 345   | 116   | 0.62   |
| WDC       | WD10SPCX-08S8TT0   | 1 TB   | 2       | 225   | 0     | 0.62   |
| WDC       | WD2000FYYZ-01UL1B1 | 2 TB   | 5       | 280   | 382   | 0.62   |
| WDC       | WD2000JD-22HBC0    | 200 GB | 1       | 1350  | 5     | 0.62   |
| WDC       | WD6400BPVT-22HXZT1 | 640 GB | 3       | 338   | 3     | 0.62   |
| WDC       | WD10JMVW-11AJGS3   | 1 TB   | 4       | 251   | 3     | 0.62   |
| Seagate   | ST6000VN0041-2E... | 6 TB   | 1       | 224   | 0     | 0.62   |
| Toshiba   | MK5076GSXN         | 500 GB | 1       | 224   | 0     | 0.62   |
| Seagate   | ST9320423AS        | 320 GB | 48      | 439   | 293   | 0.62   |
| Samsung   | HM250HI            | 250 GB | 74      | 325   | 13    | 0.61   |
| WDC       | WD1600BEVT-00A23T0 | 160 GB | 3       | 277   | 3     | 0.61   |
| WDC       | WD5000AZLX-75K2TA0 | 500 GB | 5       | 223   | 0     | 0.61   |
| Seagate   | ST3120211AS        | 120 GB | 5       | 517   | 12    | 0.61   |
| Seagate   | ST9160412AS        | 160 GB | 11      | 559   | 338   | 0.61   |
| WDC       | WD2500AAJS-65M0A0  | 250 GB | 3       | 665   | 13    | 0.61   |
| WDC       | WD3200BEVT-75A23T0 | 320 GB | 3       | 283   | 47    | 0.61   |
| WDC       | WD20EZRZ-00Z5HB0   | 2 TB   | 40      | 245   | 2     | 0.61   |
| WDC       | WD3200BPVT-24ZEST0 | 320 GB | 22      | 304   | 54    | 0.61   |
| Seagate   | ST3000VX000-1ES166 | 3 TB   | 1       | 222   | 0     | 0.61   |
| Seagate   | ST9320328CS        | 320 GB | 7       | 502   | 249   | 0.61   |
| Fujitsu   | MHW2120BJ FFS G2   | 120 GB | 1       | 221   | 0     | 0.61   |
| Hitachi   | HTS541080G9SA00    | 80 GB  | 7       | 365   | 3     | 0.61   |
| WDC       | WD2500AAKS-60VYA0  | 250 GB | 1       | 221   | 0     | 0.61   |
| WDC       | WD2500BEVT-22A23T0 | 250 GB | 51      | 404   | 51    | 0.61   |
| WDC       | WD20PURX-64P6ZY0   | 2 TB   | 9       | 259   | 16    | 0.60   |
| WDC       | WD5000BEVT-22A0RT0 | 500 GB | 37      | 513   | 69    | 0.60   |
| Hitachi   | HTS727550A9E364    | 500 GB | 10      | 441   | 411   | 0.60   |
| HGST      | HTS541010A9E680    | 1 TB   | 155     | 331   | 281   | 0.60   |
| WDC       | WD5000AZLX-00K2TA0 | 500 GB | 9       | 218   | 0     | 0.60   |
| WDC       | WD40NMZW-11GX6S1   | 4 TB   | 9       | 333   | 54    | 0.60   |
| WDC       | WD3000HLFS-75G6U1  | 304 GB | 1       | 218   | 0     | 0.60   |
| Maxtor    | 6G160P0            | 160 GB | 2       | 217   | 0     | 0.60   |
| WDC       | WD20NPVT-00Z2TT0   | 2 TB   | 3       | 336   | 12    | 0.60   |
| Fujitsu   | MHY2160BH          | 160 GB | 10      | 270   | 194   | 0.60   |
| WDC       | WD20NMVW-11AV3S0   | 2 TB   | 2       | 411   | 1     | 0.60   |
| WDC       | WD1600JB-00GVC0    | 160 GB | 2       | 777   | 3     | 0.59   |
| WDC       | WD5002AALX-32Z3A0  | 500 GB | 2       | 647   | 1     | 0.59   |
| Seagate   | ST2000VX008-2E3164 | 2 TB   | 3       | 216   | 0     | 0.59   |
| WDC       | WD2500BEKT-60A25T1 | 250 GB | 9       | 440   | 115   | 0.59   |
| WDC       | WD7500BPKX-22HPJT0 | 752 GB | 11      | 235   | 1     | 0.59   |
| WDC       | WD3200AZDX-00SC2B0 | 320 GB | 2       | 379   | 440   | 0.59   |
| Seagate   | ST9160823ASG       | 160 GB | 2       | 400   | 506   | 0.59   |
| WDC       | WD3200BEKT-60PVMT0 | 320 GB | 9       | 273   | 21    | 0.59   |
| Toshiba   | MK3265GSXN         | 320 GB | 18      | 489   | 267   | 0.59   |
| Hitachi   | HTS543225L9A300    | 250 GB | 26      | 652   | 306   | 0.59   |
| Toshiba   | MK5055GSXN         | 500 GB | 2       | 392   | 4     | 0.59   |
| Toshiba   | MQ01ABF032         | 320 GB | 22      | 250   | 47    | 0.59   |
| WDC       | WD10JPVX-75JC3T0   | 1 TB   | 39      | 254   | 14    | 0.59   |
| Samsung   | SP1624N            | 160 GB | 2       | 213   | 0     | 0.59   |
| WDC       | WD5000BEVT-26A0RT0 | 500 GB | 2       | 483   | 321   | 0.58   |
| Fujitsu   | MPE3084AE          | 8 GB   | 1       | 213   | 0     | 0.58   |
| Seagate   | ST2000NM0011       | 2 TB   | 3       | 1091  | 19    | 0.58   |
| Toshiba   | HDWD130            | 3 TB   | 18      | 219   | 57    | 0.58   |
| WDC       | WD1200BB-00GUC0    | 120 GB | 2       | 1028  | 11    | 0.58   |
| HGST      | HEJ423232H9E300    | 320 GB | 1       | 211   | 0     | 0.58   |
| WDC       | WD3200BEKX-00B7WT0 | 320 GB | 8       | 213   | 2     | 0.58   |
| WDC       | WD30NMVW-11C3NS2   | 3 TB   | 2       | 606   | 1     | 0.58   |
| WDC       | WD3200BEVT-11ZCT0  | 320 GB | 3       | 215   | 1     | 0.58   |
| Toshiba   | MK6461GSY          | 640 GB | 4       | 254   | 183   | 0.58   |
| WDC       | WD7500BPVT-55HXZT4 | 752 GB | 2       | 210   | 0     | 0.58   |
| WDC       | WD10EALX-229BA0    | 1 TB   | 5       | 793   | 11    | 0.57   |
| WDC       | WD5000BEKT-80KA9T0 | 500 GB | 3       | 317   | 1     | 0.57   |
| Seagate   | ST2000DM009-2G4100 | 2 TB   | 4       | 208   | 0     | 0.57   |
| WDC       | WD800BEVS-00RST0   | 80 GB  | 3       | 277   | 1     | 0.57   |
| Fujitsu   | MHZ2160BH G1       | 160 GB | 8       | 279   | 1     | 0.57   |
| IBM/Hi... | IC35L040AVVN07-0   | 41 GB  | 2       | 576   | 3     | 0.57   |
| WDC       | WD400BB-00FJA0     | 40 GB  | 2       | 699   | 222   | 0.57   |
| WDC       | WD1600AAJS-75PSA0  | 160 GB | 5       | 353   | 3     | 0.57   |
| Toshiba   | HDWN180            | 8 TB   | 5       | 207   | 0     | 0.57   |
| Seagate   | ST1000DM003-1SB10C | 1 TB   | 54      | 227   | 28    | 0.57   |
| WDC       | WD1600BJKT-75F4T0  | 160 GB | 3       | 243   | 1     | 0.57   |
| Samsung   | HN-M320MBB         | 320 GB | 3       | 401   | 3     | 0.57   |
| WDC       | WD1600BEVT-60ZCT1  | 160 GB | 6       | 324   | 170   | 0.57   |
| WDC       | WD80EFAX-68KNBN0   | 8 TB   | 3       | 206   | 0     | 0.56   |
| WDC       | WD3200BEVS-08VAT2  | 320 GB | 2       | 598   | 560   | 0.56   |
| WDC       | WD10EZEX-00UD2A0   | 1 TB   | 7       | 335   | 125   | 0.56   |
| Seagate   | ST380211AS         | 80 GB  | 8       | 606   | 555   | 0.56   |
| WDC       | WD10EURS-630AB1    | 1 TB   | 1       | 1846  | 8     | 0.56   |
| WDC       | WD1200JB-00GVC0    | 120 GB | 3       | 539   | 4     | 0.56   |
| Seagate   | ST1000LM014-1EJ164 | 1 TB   | 50      | 360   | 109   | 0.56   |
| Toshiba   | HDWD120            | 2 TB   | 24      | 204   | 0     | 0.56   |
| Hitachi   | HTS723232L9SA60    | 320 GB | 2       | 292   | 4     | 0.56   |
| WDC       | WD3200BEKX-60B7WT0 | 320 GB | 2       | 203   | 0     | 0.56   |
| Toshiba   | MK1059GSMP         | 1 TB   | 17      | 487   | 241   | 0.56   |
| Toshiba   | MQ03UBB300         | 3 TB   | 4       | 252   | 3     | 0.56   |
| WDC       | WD5000BMVW-11AMCS2 | 500 GB | 1       | 202   | 0     | 0.56   |
| WDC       | WD5000AZDX-00SC2B0 | 500 GB | 4       | 371   | 12    | 0.55   |
| WDC       | WD800JD-00JNC0     | 80 GB  | 4       | 451   | 16    | 0.55   |
| Fujitsu   | MHZ2080BH G1       | 80 GB  | 2       | 201   | 0     | 0.55   |
| WDC       | WD1600AVVS-63L2B0  | 160 GB | 5       | 732   | 3     | 0.55   |
| WDC       | WD80EMAZ-00WJTA0   | 8 TB   | 7       | 201   | 0     | 0.55   |
| Samsung   | HD120IJ            | 120 GB | 21      | 795   | 334   | 0.55   |
| Seagate   | ST4000VN000-2AH166 | 4 TB   | 1       | 200   | 0     | 0.55   |
| WDC       | WD5000BEVT-00A0RT0 | 500 GB | 13      | 386   | 173   | 0.55   |
| WDC       | WD1600BEVT-24A23T0 | 160 GB | 11      | 227   | 2     | 0.54   |
| Toshiba   | MK2035GSS          | 200 GB | 13      | 441   | 24    | 0.54   |
| WDC       | WD6400BPVT-00HXZT1 | 640 GB | 3       | 198   | 0     | 0.54   |
| WDC       | WD5000AARS-003BB1  | 500 GB | 5       | 568   | 7     | 0.54   |
| WDC       | WD10JPVT-22A1YT0   | 1 TB   | 8       | 324   | 3     | 0.54   |
| Samsung   | SP0802N            | 80 GB  | 25      | 681   | 50    | 0.54   |
| Seagate   | ST9250827AS        | 250 GB | 32      | 534   | 304   | 0.54   |
| Hitachi   | HTS727575A9E364    | 752 GB | 16      | 503   | 217   | 0.54   |
| WDC       | WD1002F9YZ-09H1JL1 | 1 TB   | 2       | 196   | 0     | 0.54   |
| Maxtor    | 6V250F0            | 250 GB | 2       | 196   | 0     | 0.54   |
| WDC       | WD3200BEKT-08PVMT1 | 320 GB | 3       | 195   | 0     | 0.54   |
| Quantum   | FIREBALLlct15 30   | 32 GB  | 1       | 391   | 1     | 0.54   |
| Toshiba   | HDWA120            | 2 TB   | 4       | 195   | 0     | 0.54   |
| Seagate   | ST95005620AS       | 500 GB | 9       | 387   | 232   | 0.54   |
| Hitachi   | HDS721612PLAT80    | 128 GB | 1       | 1366  | 6     | 0.53   |
| Toshiba   | MK6034GSX          | 64 GB  | 4       | 423   | 18    | 0.53   |
| Seagate   | ST94011A           | 40 GB  | 1       | 194   | 0     | 0.53   |
| Seagate   | ST320414A          | 20 GB  | 1       | 194   | 0     | 0.53   |
| Seagate   | ST9500420AS        | 500 GB | 83      | 577   | 476   | 0.53   |
| Toshiba   | MQ02ABD100H        | 1 TB   | 12      | 294   | 4     | 0.53   |
| WDC       | WD400BB-00DKA0     | 40 GB  | 1       | 193   | 0     | 0.53   |
| WDC       | WD800BEVS-75RST0   | 80 GB  | 4       | 381   | 252   | 0.53   |
| Seagate   | ST3750528AS        | 752 GB | 40      | 694   | 362   | 0.53   |
| WDC       | WD10PURX-64D85Y0   | 1 TB   | 4       | 388   | 2     | 0.53   |
| WDC       | WD10SPZX-75Z10T1   | 1 TB   | 7       | 199   | 4     | 0.53   |
| WDC       | WD30NMRW-11YL9S4   | 3 TB   | 1       | 192   | 0     | 0.53   |
| WDC       | WD10EZEX-07WN4A0   | 1 TB   | 4       | 270   | 1     | 0.53   |
| Seagate   | ST9500423AS        | 500 GB | 25      | 397   | 55    | 0.53   |
| WDC       | WD5000LPCX-24C6HT0 | 500 GB | 40      | 244   | 2     | 0.52   |
| Magnet... | MD03200-AVDW-RO    | 320 GB | 1       | 191   | 0     | 0.52   |
| WDC       | WD5000LPVX-55V0TT0 | 500 GB | 13      | 254   | 1     | 0.52   |
| HGST      | HTS725050A7E630    | 500 GB | 124     | 290   | 173   | 0.52   |
| WDC       | WD4001FAEX-00MJRA0 | 4 TB   | 1       | 190   | 0     | 0.52   |
| WDC       | WD5000BPVT-26HXZT3 | 500 GB | 1       | 190   | 0     | 0.52   |
| Hitachi   | HDS721050DLE630    | 500 GB | 41      | 487   | 420   | 0.52   |
| Hitachi   | HTS542580K9SA00    | 80 GB  | 10      | 373   | 4     | 0.52   |
| Seagate   | ST500LM000-1EJ162  | 500 GB | 53      | 270   | 83    | 0.52   |
| WDC       | WD5000KMVW-11ZSMS5 | 500 GB | 1       | 189   | 0     | 0.52   |
| Seagate   | ST1000VX001-1HH162 | 1 TB   | 6       | 189   | 0     | 0.52   |
| Toshiba   | MQ01ABD100         | 1 TB   | 251     | 256   | 80    | 0.52   |
| Toshiba   | MG03ACA300         | 3 TB   | 3       | 992   | 13    | 0.52   |
| Seagate   | ST96812A           | 64 GB  | 3       | 379   | 758   | 0.52   |
| Toshiba   | MQ01UBD050         | 500 GB | 2       | 187   | 0     | 0.51   |
| Hitachi   | HDS721616PLAT80    | 160 GB | 3       | 1226  | 42    | 0.51   |
| WDC       | WD2500BJKT-00F4T0  | 250 GB | 2       | 187   | 0     | 0.51   |
| Seagate   | ST9250315ASG       | 250 GB | 2       | 187   | 0     | 0.51   |
| WDC       | WD6400AAVS-00G9B1  | 640 GB | 2       | 1128  | 143   | 0.51   |
| Samsung   | SP0842N            | 80 GB  | 10      | 577   | 473   | 0.51   |
| Seagate   | ST500VM000-1SD101  | 500 GB | 3       | 186   | 0     | 0.51   |
| WDC       | WD1600AAJS-60B4A0  | 160 GB | 3       | 678   | 348   | 0.51   |
| WDC       | WD3200BEVT-60ZCT1  | 320 GB | 6       | 488   | 244   | 0.51   |
| Maxtor    | 7V300F0            | 304 GB | 2       | 1022  | 475   | 0.51   |
| Seagate   | ST500NM0011        | 500 GB | 10      | 690   | 61    | 0.51   |
| WDC       | WD10EZEX-08Y20A0   | 1 TB   | 7       | 224   | 1     | 0.51   |
| Seagate   | ST2000NM0055-1V... | 2 TB   | 1       | 184   | 0     | 0.51   |
| Seagate   | ST98823AS          | 80 GB  | 11      | 369   | 378   | 0.51   |
| WDC       | WD5000BEVT-80A0RT0 | 500 GB | 1       | 1662  | 8     | 0.51   |
| Seagate   | ST6000DM003-2CY186 | 6 TB   | 2       | 184   | 0     | 0.51   |
| WDC       | WD3200BPVT-16JJ5T0 | 320 GB | 4       | 253   | 1     | 0.50   |
| Seagate   | ST2000LX001-1RG174 | 2 TB   | 21      | 233   | 57    | 0.50   |
| Quantum   | FIREBALLlct15 15   | 16 GB  | 1       | 183   | 0     | 0.50   |
| Hitachi   | HTS543232L9A300    | 320 GB | 16      | 605   | 481   | 0.50   |
| Seagate   | ST31000523AS       | 1 TB   | 2       | 2094  | 11    | 0.50   |
| Hitachi   | HUA721010KLA330    | 1 TB   | 3       | 821   | 651   | 0.50   |
| Hitachi   | HDT722525DLAT80    | 250 GB | 2       | 733   | 3     | 0.50   |
| Samsung   | HM321HX            | 320 GB | 2       | 263   | 4     | 0.50   |
| Seagate   | ST2000VN004-2E4164 | 2 TB   | 1       | 181   | 0     | 0.50   |
| Fujitsu   | MHZ2500BT G1       | 500 GB | 2       | 1426  | 6     | 0.50   |
| IBM/Hi... | IC25N030ATMR04-0   | 32 GB  | 1       | 544   | 2     | 0.50   |
| Hitachi   | HTS543225A7A384    | 250 GB | 28      | 348   | 439   | 0.50   |
| Seagate   | ST160NM0011 39M... | 160 GB | 1       | 361   | 1     | 0.50   |
| WDC       | WD1200JB-00FUA0    | 120 GB | 1       | 180   | 0     | 0.49   |
| Seagate   | ST3250310CS        | 250 GB | 2       | 701   | 21    | 0.49   |
| Samsung   | SP1613N            | 160 GB | 2       | 858   | 508   | 0.49   |
| HGST      | HUS724040ALA640    | 4 TB   | 1       | 180   | 0     | 0.49   |
| Seagate   | ST3000VN000-1H4167 | 3 TB   | 1       | 179   | 0     | 0.49   |
| WDC       | WD5000LPCX-00VHAT0 | 500 GB | 25      | 223   | 1     | 0.49   |
| Samsung   | SP2504C            | 250 GB | 41      | 1201  | 803   | 0.49   |
| Hitachi   | HTS545050A7E380    | 500 GB | 105     | 347   | 175   | 0.49   |
| WDC       | WD3200BEVT-22A23T0 | 320 GB | 38      | 461   | 81    | 0.49   |
| Samsung   | HE753LJ            | 752 GB | 2       | 374   | 51    | 0.49   |
| WDC       | WD2500JS-63MHB5    | 250 GB | 2       | 793   | 39    | 0.49   |
| WDC       | WD3200LPCX-24C6HT0 | 320 GB | 20      | 178   | 0     | 0.49   |
| Seagate   | ST1000DM003-1SB102 | 1 TB   | 40      | 207   | 7     | 0.49   |
| WDC       | WD800BEVT-75ZCT2   | 80 GB  | 1       | 177   | 0     | 0.49   |
| WDC       | WD5000LPCX-22VHAT0 | 500 GB | 21      | 182   | 1     | 0.49   |
| WDC       | WD1002FBYS-18A6B0  | 1 TB   | 2       | 2270  | 29    | 0.49   |
| WDC       | WD2005FBYZ-01YCBB2 | 2 TB   | 3       | 176   | 0     | 0.48   |
| Seagate   | ST1000VN002-2EY102 | 1 TB   | 2       | 176   | 0     | 0.48   |
| WDC       | WD20EADS-42R6B0    | 2 TB   | 1       | 176   | 0     | 0.48   |
| WDC       | WD2500BPVT-22ZEST0 | 250 GB | 18      | 218   | 4     | 0.48   |
| Seagate   | ST3300822AS        | 304 GB | 1       | 176   | 0     | 0.48   |
| Seagate   | ST33000651AS       | 3 TB   | 5       | 374   | 203   | 0.48   |
| WDC       | WD3200BEVT-24A23T0 | 320 GB | 10      | 529   | 103   | 0.48   |
| Samsung   | HM080HC            | 72 GB  | 1       | 526   | 2     | 0.48   |
| Seagate   | ST980210AS         | 80 GB  | 1       | 175   | 0     | 0.48   |
| WDC       | WD6400BPVT-80HXZT1 | 640 GB | 6       | 421   | 11    | 0.48   |
| HGST      | HUS726040ALA614    | 4 TB   | 6       | 177   | 3     | 0.48   |
| Toshiba   | MK2555GSXF         | 250 GB | 7       | 174   | 0     | 0.48   |
| Seagate   | ST12000DM0007-2... | 12 TB  | 2       | 189   | 1     | 0.48   |
| WDC       | WD2500JD-40HBC0    | 250 GB | 1       | 1391  | 7     | 0.48   |
| WDC       | WD1600BEVT-35ZCT0  | 160 GB | 2       | 173   | 0     | 0.48   |
| WDC       | WD1005FBYZ-01YCBB2 | 1 TB   | 3       | 173   | 0     | 0.48   |
| Hitachi   | HTS545025B9SA02    | 250 GB | 6       | 200   | 338   | 0.48   |
| WDC       | WD10JPVX-00JC3T0   | 1 TB   | 34      | 174   | 1     | 0.47   |
| WDC       | WD5000BPVT-80HXZT1 | 500 GB | 6       | 604   | 56    | 0.47   |
| WDC       | WD7500BPVT-08HXZT3 | 752 GB | 3       | 172   | 0     | 0.47   |
| Samsung   | SP0822N            | 80 GB  | 8       | 172   | 1     | 0.47   |
| Hitachi   | HTS543232A7A384    | 320 GB | 169     | 323   | 302   | 0.47   |
| Hitachi   | HTS541616J9SA00    | 160 GB | 31      | 473   | 78    | 0.47   |
| WDC       | WD10EALX-759BA0    | 1 TB   | 1       | 1887  | 10    | 0.47   |
| WDC       | WD10SPCX-24HWST1   | 1 TB   | 16      | 171   | 0     | 0.47   |
| WDC       | WD10EARX-00PASB0   | 1 TB   | 3       | 838   | 26    | 0.47   |
| WDC       | WD6400BEVT-22A0RT0 | 640 GB | 10      | 508   | 9     | 0.47   |
| Seagate   | ST9160301AS        | 160 GB | 7       | 230   | 288   | 0.47   |
| Toshiba   | MK8037GSX          | 80 GB  | 18      | 451   | 136   | 0.47   |
| WDC       | WD5000BPKX-22HPJT0 | 500 GB | 12      | 297   | 2     | 0.47   |
| Hitachi   | HCS5C1010DLE630    | 1 TB   | 1       | 169   | 0     | 0.47   |
| WDC       | WD3200AAKS-22L6A0  | 320 GB | 4       | 648   | 6     | 0.47   |
| WDC       | WD3200BJKT-00F4T0  | 320 GB | 1       | 169   | 0     | 0.46   |
| Samsung   | HM250HJ            | 250 GB | 2       | 337   | 17    | 0.46   |
| Seagate   | ST500LM021-1KJ152  | 500 GB | 61      | 221   | 94    | 0.46   |
| WDC       | WD3200LPVT-08G33T1 | 320 GB | 5       | 225   | 2     | 0.46   |
| Samsung   | HM250JI            | 250 GB | 7       | 395   | 222   | 0.46   |
| Seagate   | ST1000DM000-9TS15E | 1 TB   | 1       | 168   | 0     | 0.46   |
| Seagate   | ST3400832A         | 400 GB | 1       | 2185  | 12    | 0.46   |
| WDC       | WD2500LPCX-24C6HT0 | 250 GB | 38      | 191   | 57    | 0.46   |
| WDC       | WD1600BEVS-22VAT0  | 160 GB | 2       | 248   | 1     | 0.46   |
| Hitachi   | HTS541612J9SA00 3H | 120 GB | 2       | 558   | 93    | 0.46   |
| Hitachi   | HDE721010SLA330    | 1 TB   | 2       | 988   | 80    | 0.46   |
| WDC       | WD5000MPCK-60AWHT0 | 500 GB | 1       | 166   | 0     | 0.46   |
| Seagate   | ST3250820NS        | 250 GB | 2       | 695   | 1050  | 0.46   |
| WDC       | WD5000LPCX-22VHAT1 | 500 GB | 4       | 166   | 0     | 0.46   |
| Seagate   | ST340014AS         | 40 GB  | 4       | 736   | 508   | 0.46   |
| WDC       | WD5000AAKX-60U6AA0 | 500 GB | 43      | 265   | 129   | 0.46   |
| WDC       | WD1600BEVT-22A23T0 | 160 GB | 24      | 321   | 5     | 0.45   |
| Seagate   | ST9100824A         | 100 GB | 1       | 165   | 0     | 0.45   |
| WDC       | WD800BEVE-00A0HT0  | 80 GB  | 1       | 165   | 0     | 0.45   |
| WDC       | WD10SPCX-22HWST0   | 1 TB   | 1       | 165   | 0     | 0.45   |
| WDC       | WD5000LPLX-75ZNTT0 | 500 GB | 5       | 165   | 0     | 0.45   |
| Fujitsu   | MJA2320BH G2       | 320 GB | 7       | 630   | 445   | 0.45   |
| Hitachi   | HTS725050A9A364    | 500 GB | 19      | 465   | 731   | 0.45   |
| WDC       | WD10EZEX-60WN4A0   | 1 TB   | 42      | 186   | 25    | 0.45   |
| Maxtor    | 6G160E0            | 160 GB | 7       | 342   | 129   | 0.45   |
| WDC       | WD2500BEVT-80A23T0 | 250 GB | 19      | 320   | 43    | 0.45   |
| WDC       | WD6400AADS-00M2B0  | 640 GB | 10      | 911   | 19    | 0.45   |
| WDC       | WD10EZRZ-00HTKB0   | 1 TB   | 38      | 173   | 1     | 0.45   |
| Toshiba   | MK5059GSXP         | 500 GB | 31      | 394   | 368   | 0.45   |
| Toshiba   | HDWE140            | 4 TB   | 9       | 163   | 0     | 0.45   |
| WDC       | WD3200AAJB-00J3A0  | 320 GB | 18      | 346   | 25    | 0.45   |
| Samsung   | SP0812C            | 80 GB  | 17      | 492   | 159   | 0.44   |
| Seagate   | ST920217AS         | 20 GB  | 1       | 162   | 0     | 0.44   |
| WDC       | WD3200BPVT-80ZEST0 | 320 GB | 29      | 335   | 44    | 0.44   |
| Hitachi   | HTS543216L9A300    | 160 GB | 36      | 548   | 214   | 0.44   |
| Toshiba   | MK8007GAH          | 80 GB  | 2       | 210   | 7     | 0.44   |
| WDC       | WD100EMAZ-00WJTA0  | 10 TB  | 7       | 161   | 0     | 0.44   |
| WDC       | WD3200BEVT-00ZCT0  | 320 GB | 4       | 405   | 4     | 0.44   |
| WDC       | WD10JUCT-63J6SY0   | 1 TB   | 5       | 161   | 0     | 0.44   |
| Hitachi   | HDS722512VLAT20    | 128 GB | 1       | 805   | 4     | 0.44   |
| HGST      | HTS545050A7E380    | 500 GB | 146     | 348   | 257   | 0.44   |
| WDC       | WD10SPCX-80HWST0   | 1 TB   | 1       | 160   | 0     | 0.44   |
| Hitachi   | HTS542560K9SA00    | 64 GB  | 1       | 160   | 0     | 0.44   |
| WDC       | WD7500BPVX-75JC3T0 | 752 GB | 2       | 299   | 2     | 0.44   |
| WDC       | WD5000LPVX-28V0TT0 | 500 GB | 1       | 159   | 0     | 0.44   |
| Seagate   | ST9160827AS        | 160 GB | 34      | 435   | 283   | 0.44   |
| WDC       | WD6400BEVT-80A0RT1 | 640 GB | 2       | 479   | 13    | 0.44   |
| WDC       | WD400BB-23FJA0     | 40 GB  | 1       | 796   | 4     | 0.44   |
| WDC       | WD3200BPVT-60JJ5T0 | 320 GB | 9       | 393   | 132   | 0.43   |
| Hitachi   | HTS541075A9E680    | 752 GB | 4       | 325   | 764   | 0.43   |
| Toshiba   | HDWD110            | 1 TB   | 117     | 166   | 7     | 0.43   |
| Seagate   | ST9320325AS        | 320 GB | 216     | 460   | 454   | 0.43   |
| Toshiba   | MQ01ABD050V        | 500 GB | 1       | 157   | 0     | 0.43   |
| WDC       | WD7500BPVX-00JC3T0 | 752 GB | 1       | 157   | 0     | 0.43   |
| WDC       | WD3200BEVT-26A23T0 | 320 GB | 3       | 274   | 73    | 0.43   |
| WDC       | WD2500AAKX-603CA0  | 250 GB | 4       | 158   | 301   | 0.43   |
| Seagate   | ST4000DM004-2CV104 | 4 TB   | 56      | 168   | 5     | 0.43   |
| Toshiba   | MK3276GSXN         | 320 GB | 1       | 156   | 0     | 0.43   |
| HGST      | HTS541010A7E630    | 1 TB   | 19      | 187   | 57    | 0.43   |
| Hitachi   | HDP725032GLA380    | 320 GB | 6       | 868   | 35    | 0.43   |
| WDC       | WD10EFRX-68FYTN0   | 1 TB   | 18      | 168   | 1     | 0.43   |
| WDC       | WD3200BPVT-75ZEST0 | 320 GB | 4       | 675   | 7     | 0.43   |
| Seagate   | STM9120817AS       | 120 GB | 1       | 155   | 0     | 0.43   |
| WDC       | WD2500BEVT-08A23T1 | 250 GB | 13      | 270   | 133   | 0.42   |
| WDC       | WD10SPZX-17Z10T0   | 1 TB   | 4       | 154   | 0     | 0.42   |
| WDC       | WD10JPLX-00MBPT0   | 1 TB   | 28      | 168   | 6     | 0.42   |
| WDC       | WD5000AAKX-003CA0  | 500 GB | 19      | 602   | 53    | 0.42   |
| WDC       | WD1200JD-55HBB0    | 120 GB | 1       | 923   | 5     | 0.42   |
| Samsung   | SV0412H            | 40 GB  | 6       | 1055  | 104   | 0.42   |
| Hitachi   | HTS541060G9AT00    | 64 GB  | 6       | 564   | 17    | 0.42   |
| Hitachi   | HTS543216L9SA00    | 160 GB | 11      | 374   | 10    | 0.42   |
| WDC       | WD10EZEX-21WN4A0   | 1 TB   | 14      | 163   | 1     | 0.42   |
| WDC       | WD5000AAKS-08V0A0  | 500 GB | 7       | 506   | 39    | 0.42   |
| Seagate   | ST3500410AS        | 500 GB | 25      | 1071  | 418   | 0.42   |
| WDC       | WD5000BPVT-60HXZT1 | 500 GB | 3       | 667   | 388   | 0.42   |
| WDC       | WD10EZEX-08WN4A0   | 1 TB   | 149     | 166   | 8     | 0.42   |
| Seagate   | ST9100824AS        | 100 GB | 3       | 195   | 2     | 0.42   |
| WDC       | WD10EARX-00NYB0    | 1 TB   | 1       | 151   | 0     | 0.42   |
| WDC       | WD15NMVW-11AV3S2   | 1.5 TB | 1       | 151   | 0     | 0.42   |
| WDC       | WD80EFAX-68LHPN0   | 8 TB   | 2       | 150   | 0     | 0.41   |
| Hitachi   | HTS723232A7A364    | 320 GB | 30      | 374   | 514   | 0.41   |
| WDC       | WD10JUCT-63CYNY0   | 1 TB   | 2       | 150   | 0     | 0.41   |
| Seagate   | ST9160411AS        | 160 GB | 4       | 340   | 38    | 0.41   |
| Seagate   | ST9750423AS        | 752 GB | 12      | 579   | 342   | 0.41   |
| Hitachi   | HDS721010KLA33R... | 1 TB   | 1       | 3734  | 24    | 0.41   |
| Seagate   | ST3200822A         | 200 GB | 6       | 1408  | 10    | 0.41   |
| Samsung   | SP1634N            | 160 GB | 1       | 298   | 1     | 0.41   |
| Hitachi   | HTS542525K9SA00    | 250 GB | 33      | 535   | 101   | 0.41   |
| Seagate   | ST2000DM005-2CW102 | 2 TB   | 5       | 148   | 0     | 0.41   |
| Seagate   | ST3160815SV        | 160 GB | 5       | 681   | 1240  | 0.41   |
| Toshiba   | MD03ACA400V        | 4 TB   | 1       | 1037  | 6     | 0.41   |
| Fujitsu   | MHV2060AT          | 64 GB  | 2       | 528   | 4     | 0.41   |
| WDC       | WD1600BEVT-75A23T0 | 160 GB | 3       | 244   | 1     | 0.41   |
| WDC       | WD1200JS-22NCB1    | 120 GB | 1       | 1184  | 7     | 0.41   |
| WDC       | WD30EFRX-68N32N0   | 3 TB   | 2       | 147   | 0     | 0.41   |
| Seagate   | ST1000LM014-SSH... | 1 TB   | 16      | 329   | 300   | 0.40   |
| HGST      | HUS726040ALE614    | 4 TB   | 1       | 147   | 0     | 0.40   |
| WDC       | WD5000AVVS-63M8B0  | 500 GB | 1       | 1324  | 8     | 0.40   |
| Hitachi   | HTS542512K9SA00    | 120 GB | 53      | 514   | 103   | 0.40   |
| Hitachi   | HDS722525VLSA80    | 250 GB | 2       | 370   | 17    | 0.40   |
| Seagate   | ST750LM030-1KKG62  | 752 GB | 2       | 146   | 0     | 0.40   |
| WDC       | WD2500BEVT-00A0RT1 | 245 GB | 1       | 146   | 0     | 0.40   |
| WDC       | WD1600AAJB-00J3A0  | 160 GB | 16      | 532   | 134   | 0.40   |
| Toshiba   | MK8009GAH          | 80 GB  | 3       | 455   | 31    | 0.40   |
| MediaMax  | WL320GLSA854G      | 320 GB | 1       | 146   | 0     | 0.40   |
| Hitachi   | HTS545050KTA300    | 500 GB | 6       | 520   | 5     | 0.40   |
| WDC       | WD3000FYYZ-01UL1B0 | 3 TB   | 1       | 145   | 0     | 0.40   |
| WDC       | WD10EZEX-22MFCA0   | 1 TB   | 43      | 168   | 29    | 0.40   |
| Seagate   | ST1000DX002-2DV162 | 1 TB   | 12      | 148   | 1     | 0.40   |
| WDC       | WD5000BPVT-55HXZT3 | 500 GB | 3       | 216   | 2     | 0.40   |
| Fujitsu   | MHV2060BHPL        | 64 GB  | 1       | 144   | 0     | 0.40   |
| WDC       | WD7500KMVW-11ZSMS4 | 752 GB | 1       | 434   | 2     | 0.40   |
| Toshiba   | MK5076GSX -63      | 500 GB | 2       | 144   | 0     | 0.40   |
| Seagate   | ST3750330NS        | 752 GB | 3       | 560   | 337   | 0.39   |
| HGST      | HUH721212ALE604    | 12 TB  | 2       | 144   | 0     | 0.39   |
| WDC       | WD10EZRZ-00Z5HB0   | 1 TB   | 4       | 144   | 0     | 0.39   |
| WDC       | WD3200AAJS-55VWA0  | 320 GB | 1       | 1006  | 6     | 0.39   |
| Seagate   | ST4000NC001-1FS168 | 4 TB   | 1       | 143   | 0     | 0.39   |
| Samsung   | HM501II            | 500 GB | 4       | 461   | 4     | 0.39   |
| Seagate   | ST3000NM0033-9Z... | 3 TB   | 2       | 577   | 9     | 0.39   |
| WDC       | WD2500BPVT-24JJ5T0 | 250 GB | 4       | 142   | 0     | 0.39   |
| WDC       | WD3200AAKX-32ERMA0 | 320 GB | 1       | 142   | 0     | 0.39   |
| Hitachi   | HTS541212H9AT00    | 120 GB | 3       | 438   | 5     | 0.39   |
| WDC       | WD7500KMVV-11TK7S1 | 752 GB | 1       | 141   | 0     | 0.39   |
| WDC       | WD800BD-22MRA1     | 80 GB  | 2       | 141   | 0     | 0.39   |
| IBM       | DTLA-305020        | 20 GB  | 2       | 1494  | 37    | 0.39   |
| Toshiba   | MG03ACA100         | 1 TB   | 8       | 165   | 1     | 0.39   |
| WDC       | WD5000LPLX-22ZNTT0 | 500 GB | 7       | 140   | 0     | 0.39   |
| WDC       | WD2500AAJB-57WGA0  | 250 GB | 1       | 140   | 0     | 0.38   |
| WDC       | WD800BB-00HEA0     | 80 GB  | 1       | 840   | 5     | 0.38   |
| WDC       | WD2500AAJS-07B4A0  | 250 GB | 2       | 1695  | 198   | 0.38   |
| WDC       | WD400EB-11CPF0     | 40 GB  | 2       | 1019  | 31    | 0.38   |
| Seagate   | ST2000LM015-2E8174 | 2 TB   | 20      | 139   | 0     | 0.38   |
| WDC       | WD5000AZLX-08K2TA0 | 500 GB | 20      | 139   | 0     | 0.38   |
| WDC       | WD2500BEKT-75A25T0 | 250 GB | 3       | 443   | 5     | 0.38   |
| WDC       | WD5000AADS-56S9B1  | 500 GB | 4       | 553   | 4     | 0.38   |
| WDC       | WD2500JS-60MHB1    | 250 GB | 2       | 331   | 8     | 0.38   |
| Seagate   | ST320LT022-1AE142  | 320 GB | 1       | 138   | 0     | 0.38   |
| Seagate   | ST1000DM010-2EP102 | 1 TB   | 168     | 160   | 18    | 0.38   |
| WDC       | WD5000LPVX-00V0TT0 | 500 GB | 16      | 186   | 48    | 0.38   |
| Toshiba   | MK1655GSX          | 160 GB | 12      | 315   | 34    | 0.38   |
| Toshiba   | HDWN160            | 6 TB   | 5       | 240   | 13    | 0.38   |
| WDC       | WD20SPZX-00CRAT0   | 2 TB   | 1       | 137   | 0     | 0.38   |
| Toshiba   | MK2555GSX          | 250 GB | 28      | 411   | 81    | 0.38   |
| WDC       | WD10PURZ-85U8XY0   | 1 TB   | 1       | 137   | 0     | 0.38   |
| Seagate   | ST9320310AS        | 320 GB | 9       | 466   | 436   | 0.37   |
| Hitachi   | HCT721050SLA380    | 500 GB | 1       | 136   | 0     | 0.37   |
| Toshiba   | MQ01ABD050         | 500 GB | 112     | 303   | 312   | 0.37   |
| Hitachi   | HTS541040G9AT00    | 40 GB  | 4       | 263   | 4     | 0.37   |
| Samsung   | HD080HJ-P          | 80 GB  | 10      | 735   | 396   | 0.37   |
| WDC       | WD800JD-00JNA0     | 80 GB  | 2       | 809   | 5     | 0.37   |
| Seagate   | ST500LT012-1DG142  | 500 GB | 369     | 201   | 72    | 0.37   |
| WDC       | WD1001FALS-40K1B0  | 1 TB   | 1       | 1481  | 10    | 0.37   |
| WDC       | WD3201ABYS-01B9A0  | 320 GB | 2       | 926   | 278   | 0.37   |
| WDC       | WD3200AAKX-073CA1  | 320 GB | 2       | 342   | 4     | 0.37   |
| WDC       | WD1600JD-00HBB0    | 160 GB | 6       | 582   | 17    | 0.37   |
| Seagate   | ST320DM001 HD322GJ | 320 GB | 5       | 477   | 88    | 0.37   |
| WDC       | WD1600AAJS-98PSA0  | 160 GB | 1       | 401   | 2     | 0.37   |
| WDC       | WD1600BEVT-80A23T0 | 160 GB | 22      | 210   | 19    | 0.36   |
| Toshiba   | HDWJ110            | 1 TB   | 5       | 187   | 227   | 0.36   |
| IBM/Hi... | IC35L040AVER07-0   | 41 GB  | 2       | 1050  | 7     | 0.36   |
| Seagate   | ST500LT032-1E9142  | 500 GB | 1       | 131   | 0     | 0.36   |
| Seagate   | ST3120811AS        | 120 GB | 14      | 572   | 369   | 0.36   |
| Seagate   | ST3000DM001-9YN166 | 3 TB   | 21      | 728   | 1156  | 0.36   |
| Seagate   | ST1500DM003-9YN16G | 1.5 TB | 17      | 452   | 462   | 0.36   |
| HGST      | HUH728080ALE600    | 8 TB   | 1       | 130   | 0     | 0.36   |
| Toshiba   | MQ01ABF050         | 500 GB | 302     | 164   | 77    | 0.36   |
| WDC       | WD5000AZLX-35K2TA0 | 500 GB | 2       | 130   | 0     | 0.36   |
| WDC       | WD20EZRZ-22Z5HB0   | 2 TB   | 4       | 130   | 0     | 0.36   |
| Seagate   | ST9120822A         | 120 GB | 2       | 273   | 53    | 0.36   |
| WDC       | WD1003FZEX-00K3CA0 | 1 TB   | 17      | 148   | 1     | 0.36   |
| WDC       | WD20PURZ-85GU6Y0   | 2 TB   | 10      | 256   | 198   | 0.35   |
| Toshiba   | DT01ACA100 LENOVO  | 1 TB   | 3       | 128   | 0     | 0.35   |
| Toshiba   | MK2565GSX          | 250 GB | 23      | 312   | 197   | 0.35   |
| WDC       | WD10EADS-98M2B0    | 1 TB   | 1       | 899   | 6     | 0.35   |
| WDC       | WD800JD-22LSA1     | 80 GB  | 4       | 485   | 174   | 0.35   |
| Samsung   | HM500JJ            | 500 GB | 2       | 331   | 5     | 0.35   |
| Toshiba   | MK1034GSX          | 100 GB | 4       | 418   | 464   | 0.35   |
| Seagate   | ST1000LM048-2E7172 | 1 TB   | 45      | 140   | 7     | 0.35   |
| Toshiba   | MK8046GSX          | 80 GB  | 4       | 500   | 4     | 0.35   |
| Seagate   | ST500DM002-9YN14C  | 500 GB | 3       | 464   | 339   | 0.35   |
| WDC       | WD1600AAJS-56M0A0  | 160 GB | 2       | 469   | 4     | 0.35   |
| Seagate   | ST1000VX000-1ES162 | 1 TB   | 16      | 126   | 0     | 0.35   |
| WDC       | WD5000LPLX-08ZNTT0 | 500 GB | 11      | 206   | 1     | 0.35   |
| WDC       | WD5000BPVT-55A1YT0 | 500 GB | 1       | 126   | 0     | 0.35   |
| Seagate   | ST3500830SCE       | 500 GB | 1       | 126   | 0     | 0.35   |
| WDC       | WD5000BPVT-60HXZT3 | 500 GB | 10      | 510   | 124   | 0.35   |
| Seagate   | ST9120821AS        | 120 GB | 5       | 274   | 1101  | 0.35   |
| Toshiba   | HDWM110            | 1 TB   | 3       | 126   | 0     | 0.35   |
| WDC       | WD3200BEVT-26ZCT0  | 320 GB | 4       | 160   | 1     | 0.35   |
| WDC       | WD1600BEKT-60A25T1 | 160 GB | 2       | 145   | 1     | 0.34   |
| Seagate   | ST3250312CS        | 250 GB | 11      | 317   | 230   | 0.34   |
| WDC       | WD5000LPCX-21VHAT0 | 500 GB | 57      | 133   | 1     | 0.34   |
| Toshiba   | MK1216GSG          | 120 GB | 3       | 272   | 4     | 0.34   |
| Seagate   | ST500LT015-1DJ142  | 500 GB | 1       | 124   | 0     | 0.34   |
| Samsung   | MP0402H            | 40 GB  | 6       | 330   | 25    | 0.34   |
| WDC       | WD3200AAKS-00C9A0  | 320 GB | 3       | 1080  | 8     | 0.34   |
| Toshiba   | DT01ACA200V        | 2 TB   | 1       | 124   | 0     | 0.34   |
| Seagate   | ST9250315AS        | 250 GB | 177     | 466   | 444   | 0.34   |
| WDC       | WD8000AARS-00Y5B1  | 800 GB | 3       | 1740  | 14    | 0.34   |
| Samsung   | SP2004C            | 200 GB | 27      | 662   | 508   | 0.34   |
| Hitachi   | HTS541680J9SA00    | 80 GB  | 48      | 465   | 81    | 0.34   |
| Hitachi   | HTS541660J9SA00    | 64 GB  | 4       | 443   | 7     | 0.34   |
| WDC       | WD5000BEVT-22ZAT0  | 500 GB | 9       | 431   | 14    | 0.34   |
| Seagate   | ST9500325AS        | 500 GB | 351     | 465   | 572   | 0.34   |
| Seagate   | ST500DM009-2F110A  | 500 GB | 21      | 130   | 29    | 0.34   |
| Seagate   | ST2000LM007-1R8174 | 2 TB   | 39      | 141   | 47    | 0.33   |
| WDC       | WD2500BEVE-00A0HT0 | 250 GB | 2       | 120   | 0     | 0.33   |
| Samsung   | HD200HJ            | 200 GB | 16      | 817   | 710   | 0.33   |
| WDC       | WD10JPCX-24UE4T0   | 1 TB   | 34      | 151   | 1     | 0.33   |
| Seagate   | ST9100827AS        | 100 GB | 1       | 838   | 6     | 0.33   |
| WDC       | WD5001AALS-00J7B1  | 500 GB | 1       | 1077  | 8     | 0.33   |
| Seagate   | ST910021AS         | 100 GB | 6       | 552   | 547   | 0.33   |
| Seagate   | ST9160821AS        | 160 GB | 54      | 446   | 617   | 0.33   |
| Seagate   | ST960821A          | 64 GB  | 1       | 358   | 2     | 0.33   |
| Hitachi   | HTS541010G9SA00    | 100 GB | 13      | 383   | 88    | 0.33   |
| Toshiba   | MK6025GAS          | 64 GB  | 2       | 166   | 9     | 0.33   |
| WDC       | WD80EZAZ-11TDBA0   | 8 TB   | 11      | 119   | 0     | 0.33   |
| Toshiba   | MK6475GSX          | 640 GB | 21      | 374   | 401   | 0.33   |
| WDC       | WD2500BPVT-75JJ5T0 | 250 GB | 3       | 118   | 0     | 0.33   |
| WDC       | WD5000BEVT-60ZAT1  | 500 GB | 5       | 316   | 29    | 0.32   |
| WDC       | WD5000BPVT-08HXZT1 | 500 GB | 1       | 117   | 0     | 0.32   |
| WDC       | WD5000AAKS-00M9A0  | 500 GB | 5       | 695   | 457   | 0.32   |
| Toshiba   | MK7575GSX          | 752 GB | 20      | 566   | 620   | 0.32   |
| Toshiba   | MK1633GSG          | 160 GB | 2       | 116   | 0     | 0.32   |
| WDC       | 500GB              | 500 GB | 1       | 1047  | 8     | 0.32   |
| Seagate   | ST500DM002-1SB10A  | 500 GB | 23      | 118   | 1     | 0.32   |
| Toshiba   | MK5055GSX          | 500 GB | 13      | 490   | 136   | 0.32   |
| Hitachi   | HTS541010A9E680    | 1 TB   | 13      | 487   | 808   | 0.32   |
| Toshiba   | MK2546GSX          | 250 GB | 12      | 520   | 41    | 0.32   |
| WDC       | WD6400AAKS-75A7B0  | 640 GB | 1       | 230   | 1     | 0.32   |
| Hitachi   | HTS722016K9A300    | 160 GB | 2       | 325   | 6     | 0.31   |
| Seagate   | ST1000LM010-9YH146 | 1 TB   | 9       | 190   | 909   | 0.31   |
| Seagate   | ST3120213A         | 120 GB | 10      | 601   | 637   | 0.31   |
| HGST      | HUH721212ALE600    | 12 TB  | 2       | 113   | 0     | 0.31   |
| WDC       | WD10EZEX-07M2NA0   | 1 TB   | 2       | 773   | 9     | 0.31   |
| WDC       | WD5000LPCX-24VHAT0 | 500 GB | 58      | 118   | 20    | 0.31   |
| WDC       | WD3200AAKS-00YGA0  | 320 GB | 1       | 562   | 4     | 0.31   |
| Seagate   | ST9100823A         | 96 GB  | 1       | 1007  | 8     | 0.31   |
| Seagate   | ST340810A          | 40 GB  | 10      | 526   | 32    | 0.31   |
| WDC       | WD5000LPLX-00ZNTT0 | 500 GB | 45      | 115   | 1     | 0.30   |
| WDC       | WD10JPVX-60JC3T1   | 1 TB   | 22      | 135   | 4     | 0.30   |
| Toshiba   | MK8034GSX          | 80 GB  | 8       | 324   | 38    | 0.30   |
| WDC       | WD2500BEVT-00ZCT0  | 250 GB | 6       | 110   | 0     | 0.30   |
| WDC       | WD2500BEVT-75A23T0 | 250 GB | 5       | 581   | 13    | 0.30   |
| WDC       | WD400JB-00FMA0     | 40 GB  | 2       | 656   | 8     | 0.30   |
| WDC       | WD7500BPVT-00HXZT3 | 752 GB | 8       | 512   | 11    | 0.30   |
| Fujitsu   | MHW2020BH          | 20 GB  | 2       | 109   | 0     | 0.30   |
| WDC       | WD20SPZX-22UA7T0   | 2 TB   | 7       | 109   | 0     | 0.30   |
| Seagate   | ST250LM004 HN-M... | 250 GB | 7       | 236   | 7     | 0.30   |
| WDC       | WD10SPZX-24Z10T0   | 1 TB   | 12      | 109   | 0     | 0.30   |
| WDC       | WD3200BEKT-00V5T0  | 320 GB | 1       | 109   | 0     | 0.30   |
| WDC       | WD20EADS-32S2B0    | 2 TB   | 1       | 1198  | 10    | 0.30   |
| WDC       | WD10JPVX-35JC3T0   | 1 TB   | 2       | 108   | 0     | 0.30   |
| HGST      | HDN726040ALE614    | 4 TB   | 1       | 108   | 0     | 0.30   |
| WDC       | WD1200BEVS-60UST0  | 120 GB | 10      | 422   | 361   | 0.30   |
| Seagate   | ST320LT007-9ZV142  | 320 GB | 29      | 430   | 713   | 0.29   |
| WDC       | WD10TMVW-11ZSMS4   | 1 TB   | 1       | 107   | 0     | 0.29   |
| Fujitsu   | MHW2040BH          | 40 GB  | 1       | 214   | 1     | 0.29   |
| WDC       | WD3200BEVT-88ZCT0  | 320 GB | 1       | 106   | 0     | 0.29   |
| Toshiba   | MK7559GSXP         | 752 GB | 20      | 400   | 550   | 0.29   |
| HGST      | HTS541010B7E610    | 1 TB   | 21      | 106   | 0     | 0.29   |
| Hitachi   | HTS542520K9SA00    | 200 GB | 4       | 658   | 11    | 0.29   |
| Toshiba   | MK3259GSXP         | 320 GB | 48      | 322   | 165   | 0.29   |
| China     | TP00250GB          | 250 GB | 1       | 106   | 0     | 0.29   |
| Toshiba   | MD04ACA500         | 5 TB   | 2       | 105   | 0     | 0.29   |
| WDC       | WD3200AVJS-63B6A0  | 320 GB | 5       | 1024  | 22    | 0.29   |
| Toshiba   | HDWD105            | 500 GB | 65      | 110   | 31    | 0.29   |
| Seagate   | ST980811AS         | 80 GB  | 22      | 437   | 499   | 0.29   |
| Seagate   | ST320LT012-1DG14C  | 320 GB | 18      | 201   | 64    | 0.28   |
| Toshiba   | MK6006GAH          | 64 GB  | 1       | 103   | 0     | 0.28   |
| WDC       | WD5000AAKX-19U6AA0 | 500 GB | 1       | 103   | 0     | 0.28   |
| WDC       | WD1600BEVT-60ZCT0  | 160 GB | 5       | 203   | 403   | 0.28   |
| Hitachi   | HTS541080G9AT00    | 80 GB  | 13      | 481   | 86    | 0.28   |
| Seagate   | ST1000LM035-1RK172 | 1 TB   | 202     | 125   | 93    | 0.28   |
| WDC       | WD5000BMVW-11AJGS4 | 500 GB | 4       | 106   | 141   | 0.28   |
| Hitachi   | HTS721060G9SA00    | 64 GB  | 3       | 664   | 13    | 0.28   |
| Fujitsu   | MHT2040AH PL       | 40 GB  | 1       | 306   | 2     | 0.28   |
| WDC       | WD1600AAJS-60Z0A0  | 160 GB | 4       | 272   | 262   | 0.28   |
| Toshiba   | MK3252GSX          | 320 GB | 22      | 594   | 185   | 0.28   |
| WDC       | WD10SPZX-08Z10     | 1 TB   | 7       | 101   | 0     | 0.28   |
| WDC       | WD400BB-60DGA0     | 40 GB  | 2       | 290   | 2     | 0.28   |
| WDC       | WD20EARS-00J2GB0   | 2 TB   | 2       | 914   | 8     | 0.28   |
| WDC       | WD10EZRX-22A3KB0   | 1 TB   | 1       | 101   | 0     | 0.28   |
| Samsung   | SP1604N            | 160 GB | 3       | 394   | 62    | 0.28   |
| WDC       | WD5000AACS-00G8B0  | 500 GB | 4       | 911   | 8     | 0.28   |
| WDC       | WD3202ABYS-01B7A0  | 320 GB | 3       | 581   | 5     | 0.28   |
| WDC       | WD30PURZ-85GU6Y0   | 3 TB   | 2       | 101   | 0     | 0.28   |
| Seagate   | ST500LM000-SSHD... | 500 GB | 21      | 193   | 205   | 0.28   |
| Seagate   | ST320LT020-9YG142  | 320 GB | 130     | 341   | 606   | 0.28   |
| WDC       | WD10EADS-65P6B0    | 1 TB   | 1       | 907   | 8     | 0.28   |
| Seagate   | OOS3000G           | 3 TB   | 1       | 100   | 0     | 0.28   |
| WDC       | WD5000HHTZ-04N21V1 | 500 GB | 1       | 100   | 0     | 0.27   |
| Toshiba   | MK3265GSX          | 320 GB | 56      | 590   | 239   | 0.27   |
| WDC       | WD10SPCX-75HWST0   | 1 TB   | 1       | 100   | 0     | 0.27   |
| Seagate   | ST3160812AS 41N... | 160 GB | 2       | 1038  | 42    | 0.27   |
| WDC       | WD7500AARS-003BB1  | 752 GB | 1       | 894   | 8     | 0.27   |
| HGST      | HTE725032A7E630    | 320 GB | 1       | 99    | 0     | 0.27   |
| Seagate   | ST3400620NS        | 400 GB | 1       | 2185  | 21    | 0.27   |
| Hitachi   | HTS541612J9SA00    | 120 GB | 59      | 540   | 72    | 0.27   |
| WDC       | WD3200BEVT-75ZCT0  | 320 GB | 2       | 839   | 86    | 0.27   |
| WDC       | WD3200BEVT-22A0RT0 | 320 GB | 4       | 174   | 4     | 0.27   |
| Seagate   | ST9160314AS        | 160 GB | 32      | 307   | 240   | 0.27   |
| HGST      | HTS545050A7E660    | 500 GB | 13      | 217   | 5     | 0.27   |
| Toshiba   | MQ01ACF050         | 500 GB | 16      | 187   | 148   | 0.27   |
| Toshiba   | HDWU130            | 3 TB   | 1       | 97    | 0     | 0.27   |
| Toshiba   | MG04ACA200E        | 2 TB   | 3       | 105   | 3     | 0.27   |
| Toshiba   | MK2046GSX          | 200 GB | 11      | 401   | 42    | 0.27   |
| Toshiba   | MK1637GSX          | 160 GB | 30      | 580   | 72    | 0.27   |
| WDC       | WD1600AAJS-65WAA0  | 160 GB | 2       | 928   | 1006  | 0.27   |
| WDC       | WD10SMZW-11Y0TS0   | 1 TB   | 10      | 96    | 0     | 0.26   |
| Seagate   | ST380023A          | 80 GB  | 1       | 2897  | 29    | 0.26   |
| WDC       | WD7500BPVT-22HXZT1 | 752 GB | 4       | 834   | 260   | 0.26   |
| WDC       | WD5003ABYZ-011FA0  | 500 GB | 5       | 272   | 8     | 0.26   |
| WDC       | WD1200BEVS-60RST0  | 120 GB | 1       | 766   | 7     | 0.26   |
| Samsung   | SP0401N            | 40 GB  | 1       | 95    | 0     | 0.26   |
| WDC       | WD10SPZX-80Z10T2   | 1 TB   | 1       | 95    | 0     | 0.26   |
| WDC       | WD3200BPVT-00ZEST0 | 320 GB | 3       | 94    | 0     | 0.26   |
| Seagate   | ST1000UM000-1EK164 | 1 TB   | 1       | 94    | 0     | 0.26   |
| Toshiba   | MK1665GSX H        | 160 GB | 1       | 93    | 0     | 0.26   |
| Seagate   | ST320VM001-1AD142  | 320 GB | 2       | 93    | 0     | 0.26   |
| WDC       | WD3200BEVT-00A23T0 | 320 GB | 3       | 146   | 9     | 0.26   |
| WDC       | WD120EMAZ-11BLFA0  | 12 TB  | 1       | 93    | 0     | 0.26   |
| Hitachi   | HTS542512K9A300    | 120 GB | 5       | 299   | 4     | 0.25   |
| WDC       | WD40PURX-64NZ6Y0   | 4 TB   | 1       | 92    | 0     | 0.25   |
| Seagate   | ST9160823AS        | 160 GB | 5       | 1026  | 670   | 0.25   |
| WDC       | WD2500JS-19NCB1    | 250 GB | 1       | 92    | 0     | 0.25   |
| Samsung   | HN-M101MBB         | 1 TB   | 15      | 419   | 366   | 0.25   |
| Fujitsu   | MJA2500BH G2       | 500 GB | 10      | 281   | 117   | 0.25   |
| WDC       | WD5000AZLX-21K2TA0 | 500 GB | 3       | 91    | 0     | 0.25   |
| Seagate   | ST1000LX015-1U7172 | 1 TB   | 33      | 99    | 35    | 0.25   |
| HGST      | HTS545032A7E380    | 320 GB | 30      | 204   | 476   | 0.25   |
| WDC       | WD1600BPVT-22JJ5T0 | 160 GB | 1       | 91    | 0     | 0.25   |
| WDC       | WD7500AAVS-00D7B1  | 752 GB | 1       | 2278  | 24    | 0.25   |
| WDC       | WD3200AAJS-56M0A0  | 320 GB | 9       | 292   | 3     | 0.25   |
| WDC       | WD1600AAJS-61M0A0  | 160 GB | 1       | 90    | 0     | 0.25   |
| HP        | GB0250EAFJF        | 250 GB | 1       | 634   | 6     | 0.25   |
| Toshiba   | MK3276GSX -63      | 320 GB | 6       | 254   | 22    | 0.25   |
| Toshiba   | HDWK105            | 500 GB | 5       | 90    | 0     | 0.25   |
| Seagate   | ST3500412AS        | 500 GB | 20      | 783   | 519   | 0.25   |
| Seagate   | ST9500325ASG       | 500 GB | 4       | 369   | 429   | 0.25   |
| WDC       | WD10EZEX-75WN4A0   | 1 TB   | 16      | 189   | 103   | 0.25   |
| Seagate   | ST31000340SV       | 1 TB   | 1       | 1616  | 17    | 0.25   |
| Fujitsu   | MHV2080BH PL       | 80 GB  | 13      | 167   | 4     | 0.25   |
| WDC       | WD10EZEX-00MFCA0   | 1 TB   | 11      | 121   | 5     | 0.25   |
| Hitachi   | HTS541616J9AT00    | 160 GB | 2       | 356   | 7     | 0.25   |
| Seagate   | ST3320613AS        | 320 GB | 88      | 835   | 251   | 0.25   |
| Samsung   | HS082HB            | 80 GB  | 1       | 89    | 0     | 0.25   |
| WDC       | WD20SDRW-11VUUS0   | 2 TB   | 1       | 89    | 0     | 0.24   |
| Fujitsu   | MHW2040AT          | 40 GB  | 1       | 88    | 0     | 0.24   |
| WDC       | WD7500BPVT-60HXZT1 | 752 GB | 3       | 625   | 56    | 0.24   |
| WDC       | WD10EZEX-35WN4A0   | 1 TB   | 3       | 88    | 0     | 0.24   |
| WDC       | WD3200AAKX-753CA1  | 320 GB | 2       | 221   | 4     | 0.24   |
| Seagate   | ST500LM030-2E717D  | 500 GB | 24      | 99    | 5     | 0.24   |
| Toshiba   | MQ02ABF050H        | 500 GB | 1       | 88    | 0     | 0.24   |
| Samsung   | HN-M750MBB         | 752 GB | 4       | 229   | 7     | 0.24   |
| Hitachi   | HDP725016GLA380    | 160 GB | 7       | 596   | 224   | 0.24   |
| WDC       | WD1600JS-61MHB1    | 160 GB | 1       | 959   | 10    | 0.24   |
| WDC       | WD2000JB-22GVA0    | 200 GB | 1       | 694   | 7     | 0.24   |
| WDC       | WD50NDZW-11MR8S1   | 5 TB   | 3       | 86    | 0     | 0.24   |
| WDC       | WD1200BEVS-22LAT0  | 120 GB | 1       | 86    | 0     | 0.24   |
| HGST      | HTS545050A7E680    | 500 GB | 226     | 208   | 365   | 0.24   |
| WDC       | WD1600BEVT-00A1TT0 | 160 GB | 2       | 273   | 3     | 0.24   |
| WDC       | WD60EZAZ-00ZGHB0   | 6 TB   | 5       | 85    | 0     | 0.24   |
| WDC       | WD5000LPCX-60VHAT0 | 500 GB | 29      | 99    | 1     | 0.23   |
| Seagate   | ST9320320AS        | 320 GB | 21      | 686   | 168   | 0.23   |
| Seagate   | ST2000DM008-2FR102 | 2 TB   | 56      | 93    | 3     | 0.23   |
| Hitachi   | HTS725032A9A364    | 320 GB | 16      | 456   | 917   | 0.23   |
| WDC       | WD10SDZW-11UMGS0   | 1 TB   | 2       | 84    | 0     | 0.23   |
| Samsung   | HD300LD            | 304 GB | 4       | 554   | 15    | 0.23   |
| WDC       | WD60PURX-64T0ZY0   | 6 TB   | 2       | 83    | 0     | 0.23   |
| Toshiba   | MK8032GAX          | 80 GB  | 2       | 117   | 252   | 0.23   |
| HGST      | HUS726T4TALN6L4    | 4 TB   | 1       | 83    | 0     | 0.23   |
| WDC       | WD5000AVCS-632DY1  | 500 GB | 5       | 150   | 4     | 0.23   |
| Toshiba   | MK3021GAS          | 32 GB  | 1       | 495   | 5     | 0.23   |
| WDC       | WD2500AAKX-193CA0  | 250 GB | 1       | 82    | 0     | 0.23   |
| WDC       | WD20EARS-22MVWB0   | 2 TB   | 1       | 739   | 8     | 0.23   |
| Seagate   | ST9250410ASG       | 250 GB | 1       | 409   | 4     | 0.22   |
| WDC       | WD1600JD-41HBC0    | 160 GB | 1       | 1884  | 22    | 0.22   |
| WDC       | WD50EFRX-68MYMN1   | 5 TB   | 2       | 81    | 0     | 0.22   |
| IBM/Hi... | IC35L060AVV207-0   | 40 GB  | 1       | 326   | 3     | 0.22   |
| WDC       | WD2500BPVT-22JJ5T0 | 250 GB | 9       | 257   | 218   | 0.22   |
| Toshiba   | MK1237GSX          | 120 GB | 15      | 436   | 102   | 0.22   |
| WDC       | WD5000AAKS-00H2B0  | 499 GB | 1       | 731   | 8     | 0.22   |
| Fujitsu   | MHT2080BH          | 80 GB  | 2       | 543   | 10    | 0.22   |
| Toshiba   | MK1246GSX          | 120 GB | 15      | 420   | 90    | 0.22   |
| Seagate   | ST3250820AV        | 250 GB | 1       | 80    | 0     | 0.22   |
| WDC       | WD10J31X-00U3VT0   | 1 TB   | 1       | 80    | 0     | 0.22   |
| Seagate   | ST1000VX005-2EZ102 | 1 TB   | 3       | 80    | 0     | 0.22   |
| Fujitsu   | MHV2100BH PL       | 100 GB | 4       | 218   | 3     | 0.22   |
| Magnet... | MD03200-AJDW-RO    | 320 GB | 1       | 79    | 0     | 0.22   |
| Toshiba   | MK5065GSX          | 500 GB | 21      | 329   | 355   | 0.22   |
| WDC       | WD600BEVS-07LAT0   | 64 GB  | 1       | 635   | 7     | 0.22   |
| WDC       | WD400BB-75JHC0     | 40 GB  | 1       | 476   | 5     | 0.22   |
| WDC       | WD5000LPCX-75VHAT0 | 500 GB | 11      | 79    | 0     | 0.22   |
| Samsung   | HD252KJ            | 250 GB | 9       | 802   | 459   | 0.22   |
| WDC       | WD3200BUCT-63TWBY0 | 320 GB | 2       | 79    | 0     | 0.22   |
| WDC       | WD20NPVZ-00WFZT0   | 2 TB   | 3       | 78    | 0     | 0.22   |
| Maxtor    | STM380211AS        | 80 GB  | 4       | 271   | 874   | 0.21   |
| WDC       | WD10SPZX-22Z10T0   | 1 TB   | 8       | 78    | 0     | 0.21   |
| WDC       | WD5000AZRX-00A3KB0 | 500 GB | 3       | 114   | 3     | 0.21   |
| Toshiba   | MQ01ABF050M        | 500 GB | 8       | 77    | 0     | 0.21   |
| WDC       | WD800BB-55JKC0     | 80 GB  | 7       | 605   | 23    | 0.21   |
| WDC       | WD7500LPCX-60KHST0 | 752 GB | 3       | 77    | 0     | 0.21   |
| Seagate   | ST9120823ASG       | 120 GB | 1       | 76    | 0     | 0.21   |
| WDC       | WD10SPCX-60KHST0   | 1 TB   | 1       | 230   | 2     | 0.21   |
| Seagate   | ST9120817AS        | 120 GB | 5       | 366   | 476   | 0.21   |
| Seagate   | ST8000DM0004-1Z... | 8 TB   | 1       | 76    | 0     | 0.21   |
| Fujitsu   | MHV2060BH PL       | 64 GB  | 3       | 76    | 3     | 0.21   |
| Samsung   | SP1614C            | 160 GB | 6       | 449   | 15    | 0.21   |
| Fujitsu   | MHV2060AT PL       | 64 GB  | 3       | 851   | 16    | 0.21   |
| WDC       | WD2502ABYS-50B7A1  | 250 GB | 1       | 1290  | 16    | 0.21   |
| HGST      | HUS728T8TALE6L4    | 8 TB   | 1       | 75    | 0     | 0.21   |
| WDC       | WD400EB-00CPF0     | 40 GB  | 3       | 448   | 24    | 0.21   |
| Hitachi   | HTS543280L9A300    | 80 GB  | 2       | 99    | 1     | 0.21   |
| WDC       | WD1004FBYZ-01YCBB1 | 1 TB   | 1       | 75    | 0     | 0.21   |
| Toshiba   | MK6476GSXN         | 640 GB | 3       | 122   | 601   | 0.21   |
| Hitachi   | HTS543232L9SA00    | 320 GB | 8       | 424   | 115   | 0.21   |
| WDC       | WD400VE-07HDT0     | 40 GB  | 1       | 74    | 0     | 0.20   |
| Seagate   | ST3000DM007-1WY10G | 3 TB   | 5       | 73    | 0     | 0.20   |
| WDC       | WD800VE-75HDT1     | 80 GB  | 1       | 369   | 4     | 0.20   |
| Hitachi   | HTS722020K9SA00    | 200 GB | 4       | 609   | 8     | 0.20   |
| HGST      | HTE721010A9E630    | 1 TB   | 4       | 73    | 0     | 0.20   |
| Seagate   | ST9160310AS        | 160 GB | 36      | 274   | 182   | 0.20   |
| Hitachi   | HDE721050SLA330    | 500 GB | 1       | 2416  | 32    | 0.20   |
| WDC       | WD1500BLHX-01V7BV0 | 150 GB | 1       | 72    | 0     | 0.20   |
| WDC       | WD1600SD-01KCC0    | 160 GB | 1       | 2914  | 39    | 0.20   |
| WDC       | WD10JMVW-11S5XS1   | 1 TB   | 1       | 72    | 0     | 0.20   |
| Seagate   | ST1000LM025 HN-... | 1 TB   | 10      | 80    | 1     | 0.20   |
| Seagate   | ST9120411ASG       | 120 GB | 1       | 361   | 4     | 0.20   |
| WDC       | WD20NMVW-11AV3S4   | 2 TB   | 2       | 751   | 512   | 0.20   |
| Hitachi   | HTS542525K9A300    | 250 GB | 5       | 644   | 653   | 0.20   |
| HP        | MB1000EAMZE        | 1 TB   | 1       | 1919  | 26    | 0.19   |
| Seagate   | ST31000322CS       | 1 TB   | 3       | 935   | 34    | 0.19   |
| IBM       | DTLA-307015        | 16 GB  | 1       | 423   | 5     | 0.19   |
| Toshiba   | MK6465GSX          | 640 GB | 24      | 659   | 702   | 0.19   |
| WDC       | WD5000AAKS-60WWPA0 | 500 GB | 6       | 640   | 726   | 0.19   |
| WDC       | WD3200AAJS-60M0A1  | 320 GB | 5       | 837   | 965   | 0.19   |
| Hitachi   | HTS543225L9SA00    | 250 GB | 6       | 507   | 35    | 0.19   |
| HGST      | HTE725050A7E630    | 500 GB | 2       | 68    | 0     | 0.19   |
| WDC       | WD2500AAJS-22L7A0  | 250 GB | 3       | 625   | 9     | 0.19   |
| WDC       | WD3200BPVT-00HXZT1 | 320 GB | 6       | 408   | 174   | 0.19   |
| Toshiba   | MK1011GAH          | 100 GB | 5       | 319   | 8     | 0.19   |
| Seagate   | ST2000LM005 HN-... | 2 TB   | 1       | 67    | 0     | 0.19   |
| Seagate   | ST91608220AS       | 160 GB | 1       | 135   | 1     | 0.19   |
| Seagate   | ST3750330AS        | 752 GB | 12      | 1160  | 301   | 0.19   |
| Hitachi   | HDT721050SLA360    | 500 GB | 3       | 1119  | 64    | 0.19   |
| WDC       | WD200BB-60CJA0     | 20 GB  | 1       | 1417  | 20    | 0.18   |
| WDC       | WD3200JS-22PDB0    | 320 GB | 1       | 1538  | 22    | 0.18   |
| Seagate   | ST3402111A         | 40 GB  | 2       | 117   | 36    | 0.18   |
| Maxtor    | STM3160811AS       | 160 GB | 6       | 687   | 266   | 0.18   |
| WDC       | WD6400BPVT-55HXZT3 | 640 GB | 1       | 597   | 8     | 0.18   |
| Samsung   | SP2014N            | 200 GB | 5       | 362   | 219   | 0.18   |
| Seagate   | ST1000LM049-2GH172 | 1 TB   | 41      | 65    | 0     | 0.18   |
| HGST      | HTS545050B7E660    | 500 GB | 17      | 65    | 0     | 0.18   |
| Toshiba   | MK3263GSXN         | 320 GB | 8       | 590   | 25    | 0.18   |
| WDC       | WD30EZRX-22D8PB0   | 3 TB   | 1       | 65    | 0     | 0.18   |
| WDC       | WD1600AAJS         | 160 GB | 1       | 65    | 0     | 0.18   |
| Seagate   | ST640LM001 HN-M... | 640 GB | 2       | 467   | 27    | 0.18   |
| Hitachi   | HTS545032B9A302    | 320 GB | 2       | 228   | 13    | 0.18   |
| Seagate   | ST380021A          | 80 GB  | 10      | 764   | 38    | 0.18   |
| WDC       | WD10SPZX-21Z10T0   | 1 TB   | 35      | 64    | 0     | 0.18   |
| WDC       | WD3200BEVT-60A23T0 | 320 GB | 17      | 275   | 362   | 0.18   |
| WDC       | WD10SPZX-17Z10T1   | 1 TB   | 2       | 64    | 0     | 0.18   |
| Toshiba   | MK8025GAS          | 80 GB  | 2       | 75    | 29    | 0.18   |
| WDC       | WD10JPLX-00MBPT1   | 1 TB   | 1       | 63    | 0     | 0.17   |
| Fujitsu   | MJA2250BH G2       | 250 GB | 7       | 237   | 151   | 0.17   |
| WDC       | WD3200AAJS-08B4A0  | 320 GB | 1       | 695   | 10    | 0.17   |
| Samsung   | SP2514N            | 250 GB | 7       | 588   | 620   | 0.17   |
| Hitachi   | HTS722080K9A300    | 80 GB  | 2       | 371   | 3     | 0.17   |
| WDC       | WD10EURX-73FH1Y0   | 1 TB   | 2       | 63    | 0     | 0.17   |
| WDC       | WD5000LPVX-16V0TT3 | 500 GB | 2       | 62    | 0     | 0.17   |
| WDC       | WD60EZRZ-00GZ5B1   | 6 TB   | 2       | 62    | 0     | 0.17   |
| WDC       | WD5000BPKT-80PK4T0 | 500 GB | 1       | 563   | 8     | 0.17   |
| Seagate   | ST4000VN008-2DR166 | 4 TB   | 17      | 62    | 0     | 0.17   |
| WDC       | WD100EFAX-68LHPN0  | 10 TB  | 4       | 62    | 0     | 0.17   |
| WDC       | WD10EZRX-22L4HB0   | 1 TB   | 1       | 62    | 0     | 0.17   |
| WDC       | WD5000LPCX-08VHA   | 500 GB | 5       | 61    | 0     | 0.17   |
| WDC       | WD7500BPVT-35HXZT3 | 752 GB | 1       | 309   | 4     | 0.17   |
| WDC       | WD20SMZW-11JW8S0   | 2 TB   | 3       | 61    | 0     | 0.17   |
| Maxtor    | 4K060H3            | 64 GB  | 1       | 927   | 14    | 0.17   |
| Toshiba   | MK1665GSX          | 160 GB | 15      | 214   | 233   | 0.17   |
| WDC       | WD3200BEKT-60F3T1  | 320 GB | 8       | 547   | 496   | 0.17   |
| Hitachi   | HTS725016A9A362    | 160 GB | 1       | 61    | 0     | 0.17   |
| HGST      | HTS545025A7E330    | 250 GB | 1       | 60    | 0     | 0.17   |
| Fujitsu   | MHV2100AH PL       | 100 GB | 1       | 423   | 6     | 0.17   |
| Hitachi   | DK23FB-60          | 64 GB  | 1       | 960   | 15    | 0.16   |
| WDC       | WD2500AAJS-98B4A0  | 250 GB | 1       | 540   | 8     | 0.16   |
| IBM/Hi... | IC25N080ATMR04-0   | 80 GB  | 3       | 195   | 19    | 0.16   |
| WDC       | WD1600BB-22GUC0    | 160 GB | 1       | 898   | 14    | 0.16   |
| Samsung   | HM120JI            | 120 GB | 4       | 327   | 5     | 0.16   |
| WDC       | WD10SPZX-00Z10T0   | 1 TB   | 10      | 59    | 0     | 0.16   |
| Toshiba   | MQ04ABF100         | 1 TB   | 72      | 69    | 15    | 0.16   |
| WDC       | WD3200AAJS-40VWA1  | 320 GB | 2       | 242   | 21    | 0.16   |
| WDC       | WD1600BEVE-00A0HT0 | 160 GB | 1       | 58    | 0     | 0.16   |
| WDC       | WD20EZAZ-00GGJB0   | 2 TB   | 7       | 58    | 0     | 0.16   |
| WDC       | WD3200LPVT-22G33T0 | 320 GB | 1       | 58    | 0     | 0.16   |
| MediaMax  | WL250GPA872B       | 250 GB | 1       | 58    | 0     | 0.16   |
| WDC       | WD1600BEVT-08A23T1 | 160 GB | 1       | 57    | 0     | 0.16   |
| Seagate   | ST500LM034-2GH17A  | 500 GB | 4       | 57    | 0     | 0.16   |
| WDC       | WD10SPCX-21KHST0   | 1 TB   | 3       | 57    | 0     | 0.16   |
| Toshiba   | MQ01ABD100M        | 1 TB   | 2       | 57    | 0     | 0.16   |
| Seagate   | ST9250311CS        | 250 GB | 1       | 2074  | 35    | 0.16   |
| Seagate   | ST33000650NS       | 3 TB   | 1       | 57    | 0     | 0.16   |
| Toshiba   | MK1652GSX          | 160 GB | 15      | 421   | 61    | 0.16   |
| Toshiba   | MK1646GSX          | 160 GB | 8       | 570   | 56    | 0.16   |
| Hitachi   | HTS421280H9AT00    | 80 GB  | 6       | 661   | 16    | 0.15   |
| WDC       | WD20EZRZ-60Z5HB0   | 2 TB   | 2       | 56    | 0     | 0.15   |
| WDC       | WD1002FBYS-01A6B0  | 1 TB   | 1       | 393   | 6     | 0.15   |
| Seagate   | ST3200826A         | 200 GB | 2       | 561   | 8     | 0.15   |
| WDC       | WD1500HLHX-01JJPV0 | 150 GB | 1       | 498   | 8     | 0.15   |
| WDC       | WD10EALX-229BA1    | 1 TB   | 1       | 493   | 8     | 0.15   |
| WDC       | WD10TMVV-11BG7S0   | 1 TB   | 2       | 695   | 9     | 0.15   |
| Samsung   | HM060HC            | 52 GB  | 1       | 272   | 4     | 0.15   |
| WDC       | WD5000AZLX-60K2TA0 | 500 GB | 6       | 54    | 0     | 0.15   |
| Hitachi   | HTS541060G9SA00    | 64 GB  | 3       | 331   | 119   | 0.15   |
| WDC       | WD2004FBYZ-01YCBB1 | 2 TB   | 4       | 54    | 0     | 0.15   |
| WDC       | WD10EZEX-35M2NA0   | 1 TB   | 1       | 54    | 0     | 0.15   |
| WDC       | WD1600YS-23SHB0    | 160 GB | 1       | 53    | 0     | 0.15   |
| WDC       | WD10SPSX-00A6WT0   | 1 TB   | 1       | 53    | 0     | 0.15   |
| Hitachi   | HDT725032VLAT80    | 320 GB | 3       | 1450  | 89    | 0.15   |
| WDC       | WD1600BEVS-00RST0  | 160 GB | 1       | 52    | 0     | 0.15   |
| WDC       | WD2500BEVT-22ZAT0  | 250 GB | 1       | 316   | 5     | 0.14   |
| Toshiba   | MQ04UBD200         | 2 TB   | 2       | 169   | 12    | 0.14   |
| Seagate   | ST31500341AS       | 1.5 TB | 57      | 785   | 327   | 0.14   |
| Hitachi   | HTS541040G9SA00    | 40 GB  | 2       | 400   | 9     | 0.14   |
| Hitachi   | HTS424040M9AT00    | 40 GB  | 6       | 456   | 186   | 0.14   |
| WDC       | WD5000LPLX-60ZNTT1 | 500 GB | 8       | 118   | 40    | 0.14   |
| Toshiba   | MK1629GSG          | 160 GB | 2       | 409   | 9     | 0.14   |
| WDC       | WD10SPZX-75Z10T2   | 1 TB   | 13      | 51    | 0     | 0.14   |
| WDC       | WD10JMVW-11AJGS0   | 1 TB   | 1       | 51    | 0     | 0.14   |
| WDC       | WD10EZRZ-22HTKB0   | 1 TB   | 4       | 51    | 0     | 0.14   |
| WDC       | WD3200BEVT-60ZCT0  | 320 GB | 5       | 269   | 24    | 0.14   |
| WDC       | WD40PURZ-85TTDY0   | 4 TB   | 1       | 50    | 0     | 0.14   |
| WDC       | WD2500AAJS-00YZCA0 | 250 GB | 4       | 442   | 61    | 0.14   |
| Samsung   | SP1213N            | 120 GB | 4       | 832   | 261   | 0.14   |
| WDC       | WD10SPZX-75Z10T3   | 1 TB   | 3       | 50    | 0     | 0.14   |
| HGST      | HTS541075A7E630    | 752 GB | 9       | 71    | 113   | 0.14   |
| WDC       | WD1600AAJB-56R1A0  | 160 GB | 2       | 152   | 4     | 0.14   |
| Toshiba   | MK2552GSX          | 250 GB | 12      | 657   | 202   | 0.14   |
| Seagate   | ST960812A          | 64 GB  | 1       | 151   | 2     | 0.14   |
| Seagate   | ST96023AS          | 64 GB  | 1       | 554   | 10    | 0.14   |
| WDC       | WD360GD-00FLA2     | 37 GB  | 4       | 1259  | 29    | 0.14   |
| Samsung   | SP1213C            | 120 GB | 5       | 677   | 45    | 0.14   |
| WDC       | WD6400BPVT-24HXZT1 | 640 GB | 2       | 575   | 509   | 0.14   |
| Toshiba   | MK3265GSXF         | 320 GB | 3       | 155   | 5     | 0.14   |
| WDC       | WD5003AZEX-00K3CA0 | 500 GB | 2       | 138   | 4     | 0.13   |
| Seagate   | ST3000VX009-2AY10G | 3 TB   | 2       | 49    | 0     | 0.13   |
| WDC       | WD10SPZX-60Z10T0   | 1 TB   | 20      | 56    | 1     | 0.13   |
| Samsung   | HM160HC            | 160 GB | 7       | 216   | 20    | 0.13   |
| WDC       | WD10JUCT-61CYNY0   | 1 TB   | 1       | 48    | 0     | 0.13   |
| WDC       | WD600UE-22KVT0     | 64 GB  | 1       | 243   | 4     | 0.13   |
| WDC       | WD2500BPVT-26JJ5T0 | 250 GB | 1       | 48    | 0     | 0.13   |
| WDC       | WD5000LPLX-66ZNTT1 | 500 GB | 3       | 53    | 1     | 0.13   |
| Seagate   | ST9808210A         | 80 GB  | 2       | 259   | 19    | 0.13   |
| WDC       | WD7500BMVW-11S5XS0 | 752 GB | 1       | 434   | 8     | 0.13   |
| WDC       | WD6001FSYZ-01SS7B1 | 6 TB   | 1       | 47    | 0     | 0.13   |
| Samsung   | SP1203N            | 120 GB | 6       | 486   | 31    | 0.13   |
| Hitachi   | HTS421210H9AT00    | 100 GB | 1       | 568   | 11    | 0.13   |
| Toshiba   | MK1255GSX H        | 120 GB | 2       | 236   | 419   | 0.13   |
| Fujitsu   | MHZ2320BH G2       | 320 GB | 10      | 465   | 479   | 0.13   |
| WDC       | WD3200BEKT-22KA9T0 | 320 GB | 1       | 46    | 0     | 0.13   |
| Hitachi   | HTS541660J9AT00    | 64 GB  | 1       | 184   | 3     | 0.13   |
| WDC       | WD101KFBX-68R56N0  | 10 TB  | 1       | 45    | 0     | 0.13   |
| WDC       | WD1600BB-00GUC0    | 160 GB | 3       | 769   | 81    | 0.13   |
| WDC       | WD7500AYPS-01ZKB0  | 752 GB | 1       | 228   | 4     | 0.12   |
| Samsung   | SV4012H            | 40 GB  | 2       | 1504  | 236   | 0.12   |
| WDC       | WD3200AAJS-00V4A0  | 320 GB | 3       | 396   | 9     | 0.12   |
| Toshiba   | MK3265GSX H        | 320 GB | 1       | 45    | 0     | 0.12   |
| WDC       | WD1600AAJS-19WAA0  | 160 GB | 1       | 44    | 0     | 0.12   |
| IBM       | DTLA-307020        | 20 GB  | 1       | 754   | 16    | 0.12   |
| IBM/Hi... | IC25N060ATMR04-0   | 64 GB  | 7       | 306   | 16    | 0.12   |
| ExcelStor | J880S              | 82 GB  | 1       | 44    | 0     | 0.12   |
| Toshiba   | MK6008GAH          | 64 GB  | 2       | 399   | 8     | 0.12   |
| Hitachi   | HTS541212H9SA00    | 120 GB | 1       | 221   | 4     | 0.12   |
| WDC       | WD5000AAKX-004EA0  | 500 GB | 1       | 392   | 8     | 0.12   |
| Hitachi   | HDP725025GLAT80    | 250 GB | 1       | 216   | 4     | 0.12   |
| Toshiba   | MK3276GSX H        | 320 GB | 1       | 43    | 0     | 0.12   |
| WDC       | WD50EZRZ-00GZ5B1   | 5 TB   | 1       | 42    | 0     | 0.12   |
| Seagate   | ST2000VX000-9YW164 | 2 TB   | 7       | 700   | 892   | 0.12   |
| Maxtor    | 6B300R0            | 304 GB | 1       | 42    | 0     | 0.12   |
| WDC       | WD1600BMVS-11F9S0  | 160 GB | 1       | 339   | 7     | 0.12   |
| WDC       | WD1503FYYS-02W0B0  | 1.5 TB | 1       | 382   | 8     | 0.12   |
| WDC       | WD4003FRYZ-01F0DB0 | 4 TB   | 1       | 42    | 0     | 0.12   |
| WDC       | WD1600BEVT-26ZCT0  | 160 GB | 2       | 186   | 22    | 0.12   |
| Toshiba   | MK5056GSY          | 500 GB | 2       | 204   | 2     | 0.12   |
| IBM/Hi... | IC25N030ATCS04-0   | 32 GB  | 2       | 134   | 3     | 0.11   |
| WDC       | WD15NMVW-11EDZS6   | 1.5 TB | 1       | 41    | 0     | 0.11   |
| Hitachi   | HTS545050B9SA00    | 500 GB | 6       | 844   | 842   | 0.11   |
| WDC       | WD30NMZW-11GX6S1   | 3 TB   | 1       | 41    | 0     | 0.11   |
| Toshiba   | MK4055GSX          | 400 GB | 3       | 338   | 7     | 0.11   |
| Maxtor    | 7L250R0            | 256 GB | 1       | 40    | 0     | 0.11   |
| Fujitsu   | MHV2200BT PL       | 200 GB | 1       | 325   | 7     | 0.11   |
| WDC       | WD1600BEVE-00UYT0  | 160 GB | 1       | 40    | 0     | 0.11   |
| WDC       | WD3200LPVT-00G33T0 | 320 GB | 2       | 40    | 0     | 0.11   |
| HGST      | HUS726T6TALE6L4    | 6 TB   | 1       | 40    | 0     | 0.11   |
| WDC       | WD6400AAKS-55A7B2  | 640 GB | 1       | 361   | 8     | 0.11   |
| Toshiba   | MQ02ABF100         | 1 TB   | 2       | 39    | 0     | 0.11   |
| MediaMax  | WL1000GSA3254G     | 1 TB   | 1       | 476   | 11    | 0.11   |
| Hitachi   | HTS545012B9SA00    | 120 GB | 1       | 197   | 4     | 0.11   |
| WDC       | WD2000JS-22NCB1    | 200 GB | 1       | 1921  | 48    | 0.11   |
| Seagate   | ST1000NM0008-2F... | 1 TB   | 1       | 39    | 0     | 0.11   |
| WDC       | WD5000AVCS-612DY1  | 500 GB | 1       | 582   | 14    | 0.11   |
| WDC       | WD2500AAKS-00F0A0  | 250 GB | 5       | 474   | 58    | 0.11   |
| Samsung   | HM100JC            | 100 GB | 1       | 383   | 9     | 0.10   |
| Seagate   | ST500LM030-1RK17D  | 500 GB | 16      | 38    | 0     | 0.10   |
| WDC       | WD1500ADFD-00NLR5  | 150 GB | 1       | 344   | 8     | 0.10   |
| WDC       | WD82PURZ-85TEUY0   | 8 TB   | 2       | 38    | 0     | 0.10   |
| Hitachi   | HTS541020G9SA00    | 20 GB  | 1       | 38    | 0     | 0.10   |
| WDC       | WD15EADS-22P8B0    | 1.5 TB | 1       | 339   | 8     | 0.10   |
| Hitachi   | HTS722010K9SA00    | 100 GB | 2       | 676   | 23    | 0.10   |
| Seagate   | ST3000VN007-2AH16M | 3 TB   | 1       | 37    | 0     | 0.10   |
| Hitachi   | HDT721050SLA380    | 500 GB | 1       | 224   | 5     | 0.10   |
| WDC       | WD1600BEKT-60V5T1  | 160 GB | 3       | 150   | 4     | 0.10   |
| Hitachi   | HTS541640J9SA00    | 40 GB  | 1       | 186   | 4     | 0.10   |
| WDC       | WD3200BEVS-16VAT0  | 320 GB | 1       | 37    | 0     | 0.10   |
| HGST      | HTS541515A9E630    | 1.5 TB | 2       | 541   | 14    | 0.10   |
| WDC       | WD1002FBYS-18W8B0  | 1 TB   | 1       | 36    | 0     | 0.10   |
| Maxtor    | STM3320613AS       | 320 GB | 12      | 1007  | 434   | 0.10   |
| WDC       | WD5000BEVT-80A0RT1 | 500 GB | 2       | 284   | 7     | 0.10   |
| Seagate   | ST8000VN004-2M2101 | 8 TB   | 5       | 36    | 0     | 0.10   |
| WDC       | WD5000LPCX-60VHAT1 | 500 GB | 10      | 36    | 0     | 0.10   |
| WDC       | WD10EZEX-60WN4A1   | 1 TB   | 5       | 37    | 1     | 0.10   |
| WDC       | WD800AAJS-60M0A0   | 80 GB  | 1       | 2215  | 60    | 0.10   |
| Hitachi   | HTS543212L9A300    | 120 GB | 2       | 232   | 72    | 0.10   |
| WDC       | WD800AAJS-60B4A0   | 80 GB  | 2       | 1529  | 24    | 0.10   |
| WDC       | WD2500AAJS-75B4A0  | 250 GB | 2       | 348   | 9     | 0.10   |
| Maxtor    | 6L120P0            | 122 GB | 2       | 35    | 0     | 0.10   |
| WDC       | WD30EZRS-00J99B0   | 3 TB   | 4       | 801   | 875   | 0.10   |
| Toshiba   | HDWJ105            | 500 GB | 8       | 35    | 0     | 0.10   |
| WDC       | WD1200BEVS-07LAT0  | 120 GB | 4       | 373   | 249   | 0.10   |
| WDC       | WD5000LPLX-21ZNTT0 | 500 GB | 3       | 78    | 366   | 0.10   |
| WDC       | WD40NDZW-11MR8S1   | 4 TB   | 1       | 34    | 0     | 0.09   |
| Toshiba   | MK1252GSX          | 120 GB | 7       | 446   | 129   | 0.09   |
| Hitachi   | HTS725025A9A361... | 250 GB | 1       | 34    | 0     | 0.09   |
| Toshiba   | MK5076GSX          | 500 GB | 31      | 62    | 175   | 0.09   |
| Seagate   | ST10000DM0004-1... | 10 TB  | 2       | 223   | 4     | 0.09   |
| Toshiba   | MK5065GSXN         | 500 GB | 9       | 424   | 804   | 0.09   |
| WDC       | WD5000BEKT-22KA9T0 | 500 GB | 1       | 302   | 8     | 0.09   |
| Hitachi   | HDS722580VLAT20    | 82 GB  | 3       | 418   | 180   | 0.09   |
| HGST      | HTS541050A9E680    | 500 GB | 3       | 33    | 0     | 0.09   |
| Hitachi   | HTS543216L9SA02    | 160 GB | 2       | 182   | 5     | 0.09   |
| WDC       | WD1600BB-55GUA0    | 160 GB | 1       | 668   | 19    | 0.09   |
| HGST      | HTS725050B7E630    | 500 GB | 2       | 33    | 0     | 0.09   |
| Maxtor    | 2F030L0            | 32 GB  | 1       | 33    | 0     | 0.09   |
| WDC       | WD6400BEVT-24A0RT0 | 640 GB | 1       | 329   | 9     | 0.09   |
| Toshiba   | HDWM105            | 500 GB | 1       | 32    | 0     | 0.09   |
| Hitachi   | DK23EA-40          | 40 GB  | 2       | 241   | 236   | 0.09   |
| Hitachi   | HTS421260H9AT00    | 64 GB  | 3       | 555   | 16    | 0.09   |
| WDC       | WD10JPVX-08JC3T6   | 1 TB   | 2       | 32    | 0     | 0.09   |
| Toshiba   | MK3275GSX          | 320 GB | 15      | 223   | 209   | 0.09   |
| WDC       | WD20SPZX-75UA7T1   | 2 TB   | 1       | 32    | 0     | 0.09   |
| Maxtor    | 6L200P0            | 208 GB | 2       | 32    | 0     | 0.09   |
| Seagate   | ST1000VM002-1ET162 | 1 TB   | 1       | 32    | 0     | 0.09   |
| MicroData | MD1TBLSSHD         | 1 TB   | 1       | 288   | 8     | 0.09   |
| WDC       | WD10E              | 1 TB   | 1       | 31    | 0     | 0.09   |
| WDC       | WD5000AZLX-22JKKA0 | 500 GB | 9       | 31    | 0     | 0.09   |
| HGST      | HUS726020ALE614    | 2 TB   | 1       | 31    | 0     | 0.09   |
| WDC       | WD10JPVT-00A1YT0   | 1 TB   | 1       | 31    | 0     | 0.09   |
| WDC       | WD10SPZX-24Z10     | 1 TB   | 23      | 31    | 0     | 0.09   |
| WDC       | WD1600BEVS-00VAT0  | 160 GB | 1       | 31    | 0     | 0.09   |
| WDC       | WD5000BEVT-00SCST0 | 500 GB | 1       | 311   | 9     | 0.09   |
| WDC       | WD800JB-00FSA0     | 80 GB  | 1       | 1366  | 43    | 0.09   |
| WDC       | WD2500JD-00HBC0    | 250 GB | 1       | 620   | 19    | 0.09   |
| Maxtor    | 2F030J1            | 32 GB  | 1       | 185   | 5     | 0.08   |
| WDC       | WD10TPVT-00U4RT1   | 1 TB   | 2       | 455   | 232   | 0.08   |
| WDC       | WD20EVDS-63T3B0    | 2 TB   | 1       | 273   | 8     | 0.08   |
| Seagate   | ST9402115AS        | 40 GB  | 2       | 160   | 1042  | 0.08   |
| Samsung   | HM121HC            | 120 GB | 3       | 230   | 19    | 0.08   |
| Seagate   | ST38410A           | 9 GB   | 1       | 754   | 24    | 0.08   |
| WDC       | WD600VE-75HDT0     | 64 GB  | 1       | 268   | 8     | 0.08   |
| Toshiba   | HDWQ140            | 4 TB   | 3       | 29    | 0     | 0.08   |
| WDC       | WD5000BEVT-35ZAT0  | 500 GB | 1       | 268   | 8     | 0.08   |
| Samsung   | SV0401N            | 40 GB  | 1       | 952   | 31    | 0.08   |
| Seagate   | ST750LM028-1KK162  | 752 GB | 1       | 29    | 0     | 0.08   |
| Seagate   | ST3500320AS        | 500 GB | 72      | 810   | 524   | 0.08   |
| Samsung   | MP0804H            | 80 GB  | 3       | 243   | 8     | 0.08   |
| WDC       | WD1600JS-00MHB1    | 160 GB | 1       | 1060  | 35    | 0.08   |
| WDC       | WD5000AAKX-00KJ3A0 | 500 GB | 1       | 262   | 8     | 0.08   |
| CLOVER    | CN-M500MBB         | 500 GB | 2       | 29    | 0     | 0.08   |
| WDC       | WD3200JB-00KFA0    | 320 GB | 1       | 29    | 0     | 0.08   |
| Samsung   | HM320JI            | 320 GB | 6       | 467   | 589   | 0.08   |
| Maxtor    | 6L080M0            | 80 GB  | 3       | 28    | 0     | 0.08   |
| Hitachi   | HTS543212L9SA02    | 120 GB | 1       | 27    | 0     | 0.08   |
| Seagate   | ST9250320AS        | 250 GB | 17      | 333   | 223   | 0.07   |
| WDC       | WD2000JD-55HBC0    | 200 GB | 1       | 26    | 0     | 0.07   |
| WDC       | WD3200AAJS-00VWA1  | 320 GB | 1       | 708   | 26    | 0.07   |
| Hitachi   | HTS548040M9AT00    | 40 GB  | 1       | 470   | 17    | 0.07   |
| Toshiba   | MK3265GSXV         | 320 GB | 1       | 129   | 4     | 0.07   |
| Seagate   | ST3640323AS        | 640 GB | 8       | 1077  | 484   | 0.07   |
| Maxtor    | STM3500320AS       | 500 GB | 16      | 714   | 302   | 0.07   |
| Samsung   | HM322IX            | 320 GB | 1       | 25    | 0     | 0.07   |
| Toshiba   | MK5059GSX          | 500 GB | 1       | 932   | 36    | 0.07   |
| Seagate   | ST500LM016 HN-M... | 500 GB | 1       | 24    | 0     | 0.07   |
| WDC       | WD1200JB-00CRA1    | 120 GB | 1       | 871   | 34    | 0.07   |
| WDC       | WD40EZRZ-75GXCB0   | 4 TB   | 4       | 24    | 0     | 0.07   |
| Hitachi   | HTS725032A9A360    | 320 GB | 1       | 24    | 0     | 0.07   |
| WDC       | WD2500AAJS-52B4A0  | 250 GB | 2       | 942   | 45    | 0.07   |
| WDC       | WD20NMVW-11AV3S3   | 2 TB   | 1       | 23    | 0     | 0.07   |
| Toshiba   | MK3276GSX          | 320 GB | 25      | 29    | 284   | 0.06   |
| WDC       | WD400VE-75HDT1     | 40 GB  | 1       | 23    | 0     | 0.06   |
| WDC       | WD2500BEVT-60A23T0 | 250 GB | 3       | 258   | 27    | 0.06   |
| Toshiba   | MK6032GAX          | 64 GB  | 1       | 23    | 0     | 0.06   |
| Seagate   | ST4000VX000-2AG166 | 4 TB   | 1       | 23    | 0     | 0.06   |
| Toshiba   | MK6465GSXW         | 640 GB | 1       | 552   | 23    | 0.06   |
| Toshiba   | MK2529GSG          | 250 GB | 2       | 313   | 1127  | 0.06   |
| Magnet... | MD02500-BQDW-RO    | 250 GB | 1       | 22    | 0     | 0.06   |
| WDC       | WD3200AUDX-56WNHY0 | 320 GB | 1       | 22    | 0     | 0.06   |
| WDC       | WD2000JS-60NCB1    | 200 GB | 2       | 192   | 6     | 0.06   |
| Samsung   | HM251JI            | 250 GB | 6       | 334   | 527   | 0.06   |
| Seagate   | ST14000DM001-2J... | 14 TB  | 1       | 22    | 0     | 0.06   |
| Toshiba   | MK1032GAX          | 100 GB | 2       | 108   | 4     | 0.06   |
| WDC       | WD3200AVVS-63L2B0  | 320 GB | 5       | 325   | 69    | 0.06   |
| WDC       | WD10TPVT-00HT5T1   | 1 TB   | 1       | 219   | 9     | 0.06   |
| WDC       | WD3200BEKX-22B7WT0 | 320 GB | 1       | 21    | 0     | 0.06   |
| WDC       | WD4005FZBX-00K5WB0 | 4 TB   | 3       | 21    | 0     | 0.06   |
| Seagate   | ST3300831A         | 304 GB | 1       | 347   | 15    | 0.06   |
| Seagate   | ST3250824SCE       | 250 GB | 1       | 21    | 0     | 0.06   |
| WDC       | WD5000AVDS-73U7B1  | 500 GB | 2       | 189   | 7     | 0.06   |
| Maxtor    | STM3160613AS       | 160 GB | 1       | 41    | 1     | 0.06   |
| Fujitsu   | MHT2040AT          | 40 GB  | 1       | 166   | 7     | 0.06   |
| Maxtor    | 6Y120M0            | 122 GB | 2       | 25    | 4     | 0.06   |
| WDC       | WD400BB-22DEA0     | 40 GB  | 1       | 831   | 39    | 0.06   |
| Toshiba   | MQ02ABF050H-SSH... | 500 GB | 2       | 20    | 0     | 0.06   |
| Seagate   | ST9500424AS        | 500 GB | 2       | 120   | 505   | 0.06   |
| WDC       | WD2000BB-00GUC0    | 200 GB | 1       | 637   | 30    | 0.06   |
| Samsung   | HM160HI            | 160 GB | 61      | 340   | 388   | 0.06   |
| Maxtor    | 6B200M0            | 200 GB | 3       | 26    | 13    | 0.06   |
| WDC       | WD30EZRX-00AZ6B0   | 3 TB   | 2       | 99    | 124   | 0.06   |
| WDC       | WD10SMZW-34Y0TS0   | 1 TB   | 1       | 20    | 0     | 0.06   |
| WDC       | WD5000BPVT-75A1YT0 | 500 GB | 1       | 20    | 0     | 0.06   |
| WDC       | WD1001FAES-75W7A0  | 1 TB   | 1       | 2917  | 142   | 0.06   |
| WDC       | WD2500BPVT-00ZEST0 | 250 GB | 3       | 136   | 74    | 0.06   |
| Fujitsu   | MHV2060AH          | 64 GB  | 1       | 968   | 47    | 0.06   |
| WDC       | WD2500LPCX-24VHAT0 | 250 GB | 2       | 55    | 5     | 0.05   |
| IBM       | DARA-206000        | 6 GB   | 1       | 118   | 5     | 0.05   |
| Seagate   | ST3160215SCE       | 160 GB | 1       | 98    | 4     | 0.05   |
| Seagate   | ST9250610NS        | 250 GB | 2       | 19    | 0     | 0.05   |
| IBM/Hi... | IC25N040ATMR04-0   | 40 GB  | 2       | 628   | 181   | 0.05   |
| Seagate   | ST31000333AS       | 1 TB   | 22      | 721   | 477   | 0.05   |
| Samsung   | HD160HJ            | 160 GB | 16      | 764   | 789   | 0.05   |
| Maxtor    | STM3300622A        | 304 GB | 1       | 173   | 8     | 0.05   |
| WDC       | WD200EB-75CPF0     | 20 GB  | 2       | 402   | 20    | 0.05   |
| Maxtor    | 2F040J0            | 40 GB  | 1       | 19    | 0     | 0.05   |
| Toshiba   | MK8052GSX          | 80 GB  | 4       | 150   | 44    | 0.05   |
| WDC       | WD1600JD-00GBB0    | 160 GB | 1       | 727   | 37    | 0.05   |
| Seagate   | ST31000340AS       | 1 TB   | 6       | 1025  | 364   | 0.05   |
| Seagate   | ST9250421ASG       | 250 GB | 1       | 453   | 23    | 0.05   |
| Samsung   | HM080HI            | 80 GB  | 2       | 473   | 405   | 0.05   |
| Seagate   | ST9100822A         | 100 GB | 1       | 592   | 31    | 0.05   |
| MARSHAL   | MAL2500SA-T54      | 500 GB | 2       | 323   | 27    | 0.05   |
| WDC       | WD5000LPVX-16V0TT0 | 500 GB | 1       | 71    | 3     | 0.05   |
| Quantum   | FIREBALLlct15 10   | 10 GB  | 1       | 105   | 5     | 0.05   |
| WDC       | WD2500JS-75NCB1    | 250 GB | 1       | 2681  | 153   | 0.05   |
| WDC       | WD1600JS-55MHB0    | 160 GB | 1       | 761   | 43    | 0.05   |
| HGST      | HUS726T4TALE6L4    | 4 TB   | 1       | 17    | 0     | 0.05   |
| Maxtor    | 6L160M0            | 160 GB | 6       | 26    | 351   | 0.05   |
| Hitachi   | HDP725032GLAT80    | 320 GB | 1       | 943   | 55    | 0.05   |
| Seagate   | ST3320310CS        | 320 GB | 3       | 576   | 32    | 0.05   |
| WDC       | WD800JD-75JNC0     | 80 GB  | 1       | 936   | 56    | 0.04   |
| Samsung   | HN-M250MBB         | 250 GB | 1       | 292   | 17    | 0.04   |
| Maxtor    | 2F040L0            | 41 GB  | 3       | 25    | 2     | 0.04   |
| Samsung   | HM060HI            | 64 GB  | 3       | 542   | 697   | 0.04   |
| WDC       | WD3200BEKT-75PVMT0 | 320 GB | 2       | 217   | 18    | 0.04   |
| Seagate   | ST500LX025-1U71... | 500 GB | 1       | 15    | 0     | 0.04   |
| WDC       | WD800BB-88JHC0     | 80 GB  | 1       | 1625  | 101   | 0.04   |
| Hitachi   | HTS545025A7E380    | 250 GB | 1       | 15    | 0     | 0.04   |
| Seagate   | ST320LT012-9WS14C  | 320 GB | 47      | 260   | 1003  | 0.04   |
| Hitachi   | HTS725025A9A364    | 250 GB | 17      | 437   | 1036  | 0.04   |
| IBM/Hi... | IC35L060AVVA07-0   | 64 GB  | 1       | 678   | 42    | 0.04   |
| Hitachi   | HTS543232L9SA02    | 320 GB | 1       | 1319  | 84    | 0.04   |
| HGST      | HUS722T1TALA604    | 1 TB   | 3       | 15    | 0     | 0.04   |
| Maxtor    | STM3160813AS       | 160 GB | 4       | 793   | 543   | 0.04   |
| WDC       | WD4000ABYS-01TNA0  | 400 GB | 1       | 688   | 44    | 0.04   |
| WDC       | WD10SPZX-22Z10T1   | 1 TB   | 3       | 15    | 0     | 0.04   |
| WDC       | WD140EMFZ-11A0WA0  | 14 TB  | 2       | 15    | 0     | 0.04   |
| Samsung   | SP1253N            | 120 GB | 1       | 286   | 18    | 0.04   |
| Toshiba   | MQ01ABB200         | 2 TB   | 2       | 91    | 352   | 0.04   |
| Hitachi   | HDS7250SASUN500G   | 500 GB | 1       | 14    | 0     | 0.04   |
| Hitachi   | HTS723225L9A360    | 250 GB | 3       | 322   | 1301  | 0.04   |
| WDC       | WD20SPZX-60UA7T0   | 2 TB   | 2       | 14    | 0     | 0.04   |
| Seagate   | OOS500G            | 500 GB | 1       | 14    | 0     | 0.04   |
| Seagate   | ST9120310AS        | 120 GB | 1       | 14    | 0     | 0.04   |
| Seagate   | ST31000533CS       | 1 TB   | 1       | 1038  | 72    | 0.04   |
| WDC       | WD205BA            | 20 GB  | 1       | 296   | 20    | 0.04   |
| Apple     | HDD HTS547550A9... | 500 GB | 3       | 170   | 27    | 0.04   |
| WDC       | WD10EADS-11M2B1    | 1 TB   | 1       | 526   | 37    | 0.04   |
| Seagate   | ST310212A          | 10 GB  | 1       | 380   | 27    | 0.04   |
| Toshiba   | MK2565GSXN         | 250 GB | 1       | 502   | 36    | 0.04   |
| WDC       | WD5000AADS-98S9B1  | 500 GB | 1       | 120   | 8     | 0.04   |
| WDC       | WD20SDZW-11JJ8S1   | 2 TB   | 1       | 12    | 0     | 0.04   |
| WDC       | WD800BB-00CAA1     | 80 GB  | 1       | 800   | 61    | 0.04   |
| WDC       | WD10EACS-22D6B1    | 1 TB   | 1       | 12    | 0     | 0.04   |
| Toshiba   | MK2565GSXV         | 250 GB | 3       | 197   | 24    | 0.03   |
| WDC       | WD3200AAJS-00RYA0  | 320 GB | 2       | 1320  | 143   | 0.03   |
| Fujitsu   | MPG3204AT E        | 20 GB  | 1       | 138   | 10    | 0.03   |
| Seagate   | ST3250412CS        | 250 GB | 1       | 12    | 0     | 0.03   |
| Maxtor    | 6L160P0            | 163 GB | 4       | 32    | 6     | 0.03   |
| WDC       | WD2500BPVT-80ZEST0 | 250 GB | 1       | 106   | 8     | 0.03   |
| WDC       | WD7500LPCX-22HWST0 | 752 GB | 1       | 129   | 10    | 0.03   |
| WDC       | WD2500AAJS-60M0A0  | 250 GB | 2       | 705   | 533   | 0.03   |
| Samsung   | HM502JX            | 500 GB | 1       | 11    | 0     | 0.03   |
| WDC       | WD800BB-00CAA0     | 80 GB  | 1       | 414   | 35    | 0.03   |
| Maxtor    | 2F030J0            | 32 GB  | 2       | 33    | 2     | 0.03   |
| Toshiba   | MQ01ABD100V        | 1 TB   | 2       | 255   | 21    | 0.03   |
| Hitachi   | HDS722525VLAT80    | 250 GB | 1       | 11    | 0     | 0.03   |
| Maxtor    | STM3320820A        | 320 GB | 1       | 11    | 0     | 0.03   |
| MediaMax  | WL2000GSA6454G     | 2 TB   | 1       | 33    | 2     | 0.03   |
| WDC       | WD141KRYZ-01C66B0  | 14 TB  | 2       | 11    | 0     | 0.03   |
| Hitachi   | HDS721025CLA382... | 160 GB | 1       | 2614  | 237   | 0.03   |
| WDC       | WD5000AAKS-19V0A0  | 500 GB | 1       | 1131  | 103   | 0.03   |
| Seagate   | STM31000528AS      | 1 TB   | 2       | 10    | 0     | 0.03   |
| Seagate   | ST3320813AS        | 320 GB | 1       | 1569  | 150   | 0.03   |
| Hitachi   | DK23CA-20          | 20 GB  | 1       | 93    | 8     | 0.03   |
| Seagate   | ST10000NM0086-2... | 10 TB  | 4       | 10    | 0     | 0.03   |
| WDC       | WD5000LPCX-75VHAT1 | 500 GB | 2       | 9     | 0     | 0.03   |
| Maxtor    | 6L080L0            | 82 GB  | 4       | 18    | 7     | 0.03   |
| Toshiba   | MK2016GAP          | 20 GB  | 1       | 349   | 36    | 0.03   |
| WDC       | WD20EFAX-68FB5N0   | 2 TB   | 3       | 9     | 0     | 0.03   |
| WDC       | WD40EFAX-68JH4N0   | 4 TB   | 1       | 9     | 0     | 0.03   |
| Maxtor    | 4K040H2            | 34 GB  | 1       | 298   | 33    | 0.02   |
| Toshiba   | MK1214GAH          | 120 GB | 3       | 60    | 142   | 0.02   |
| WDC       | WD10EZRX-00A3KB0   | 1 TB   | 1       | 8     | 0     | 0.02   |
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
| Seagate   | ST9320421AS        | 320 GB | 3       | 522   | 73    | 0.02   |
| Hitachi   | DK23EA-20B         | 17 GB  | 1       | 183   | 24    | 0.02   |
| WDC       | WD2000JS-00NCB1    | 200 GB | 1       | 537   | 73    | 0.02   |
| Hitachi   | HTS722016K9SA00    | 160 GB | 1       | 591   | 81    | 0.02   |
| Seagate   | ST730212DE         | 32 GB  | 1       | 7     | 0     | 0.02   |
| HP        | GB0250C8045        | 250 GB | 1       | 1405  | 198   | 0.02   |
| Maxtor    | 6E040L0            | 40 GB  | 11      | 30    | 34    | 0.02   |
| Seagate   | ST4000NM0115-1Y... | 4 TB   | 3       | 7     | 0     | 0.02   |
| WDC       | WD40EMRX-82UZ0N0   | 4 TB   | 1       | 7     | 0     | 0.02   |
| Maxtor    | 6E030L0            | 32 GB  | 5       | 15    | 19    | 0.02   |
| WDC       | WD2500AAJS-41RYA0  | 250 GB | 1       | 76    | 10    | 0.02   |
| WDC       | WD1600AABS-00H4A0  | 160 GB | 1       | 81    | 11    | 0.02   |
| Maxtor    | 6B250S0            | 250 GB | 1       | 6     | 0     | 0.02   |
| WDC       | WD10TMVV-11TK7S1   | 1 TB   | 2       | 177   | 39    | 0.02   |
| Maxtor    | 6L250S0            | 250 GB | 2       | 25    | 12    | 0.02   |
| Seagate   | ST500LT012-9WS142  | 500 GB | 173     | 311   | 1072  | 0.02   |
| Samsung   | SP1614N            | 160 GB | 1       | 690   | 106   | 0.02   |
| WDC       | WD360ADFD-00NLR4   | 37 GB  | 1       | 499   | 77    | 0.02   |
| HPE       | MB004000GWWQH      | 4 TB   | 1       | 6     | 0     | 0.02   |
| Maxtor    | 6L120M0            | 122 GB | 1       | 43    | 6     | 0.02   |
| WDC       | WD20SDZW-11Z3CS0   | 2 TB   | 1       | 6     | 0     | 0.02   |
| Maxtor    | 6L080P0            | 82 GB  | 2       | 10    | 10    | 0.02   |
| Samsung   | HM100JI            | 100 GB | 1       | 827   | 140   | 0.02   |
| Hitachi   | HTS541612J9AT00    | 120 GB | 1       | 116   | 19    | 0.02   |
| Seagate   | ST4000NE001-2MA101 | 4 TB   | 1       | 5     | 0     | 0.02   |
| Seagate   | ST3500320SV        | 500 GB | 1       | 45    | 7     | 0.02   |
| Samsung   | HM121HI            | 120 GB | 9       | 458   | 1453  | 0.02   |
| Hitachi   | HTS723232L9A360    | 320 GB | 4       | 866   | 850   | 0.02   |
| Seagate   | ST2000NE001-2M5101 | 2 TB   | 1       | 5     | 0     | 0.01   |
| WDC       | WD15SMZW-11JW8S0   | 1.5 TB | 1       | 5     | 0     | 0.01   |
| Seagate   | ST1000LM002-9VQ14L | 1 TB   | 1       | 25    | 4     | 0.01   |
| Seagate   | ST14000NE0008-2... | 14 TB  | 4       | 5     | 0     | 0.01   |
| Maxtor    | 6Y160P0            | 163 GB | 4       | 23    | 145   | 0.01   |
| WDC       | WD15EARS-22MVWB0   | 1.5 TB | 3       | 818   | 514   | 0.01   |
| WDC       | WD1200AAJS-00VTA0  | 120 GB | 1       | 995   | 203   | 0.01   |
| WDC       | WD10EZEX-00M2NA0   | 1 TB   | 1       | 175   | 36    | 0.01   |
| Hitachi   | HTE721060G9AT00    | 64 GB  | 1       | 4     | 0     | 0.01   |
| Toshiba   | MK2576GSX          | 250 GB | 1       | 4     | 0     | 0.01   |
| Fujitsu   | MHT2080AH          | 80 GB  | 1       | 292   | 64    | 0.01   |
| Toshiba   | MK8050GAC          | 80 GB  | 1       | 878   | 197   | 0.01   |
| Seagate   | ST500LX025-1U717D  | 500 GB | 2       | 42    | 193   | 0.01   |
| Maxtor    | 4R060J0            | 64 GB  | 1       | 25    | 5     | 0.01   |
| Toshiba   | MK7559GSXF         | 752 GB | 2       | 117   | 637   | 0.01   |
| Fujitsu   | MHZ2160BJ G1       | 160 GB | 1       | 4     | 0     | 0.01   |
| Toshiba   | HDWL120            | 2 TB   | 3       | 4     | 0     | 0.01   |
| Maxtor    | 6Y120P0            | 122 GB | 2       | 23    | 8     | 0.01   |
| Samsung   | HM500LI            | 500 GB | 1       | 7     | 1     | 0.01   |
| Maxtor    | 6Y200P0            | 208 GB | 1       | 30    | 7     | 0.01   |
| Toshiba   | MK5061GSYN         | 500 GB | 13      | 89    | 453   | 0.01   |
| WDC       | WD2500BEKT-66F3T2  | 250 GB | 1       | 193   | 50    | 0.01   |
| WDC       | WD6003FZBX-00GXAB0 | 6 TB   | 1       | 3     | 0     | 0.01   |
| Seagate   | ST3500820AS        | 500 GB | 4       | 255   | 56    | 0.01   |
| Maxtor    | 6Y080M0            | 80 GB  | 9       | 28    | 92    | 0.01   |
| Seagate   | ST1000NX0313       | 1 TB   | 1       | 1357  | 370   | 0.01   |
| Hitachi   | HTS722012K9A300    | 120 GB | 1       | 781   | 214   | 0.01   |
| Toshiba   | MK6028GAL          | 64 GB  | 1       | 3     | 0     | 0.01   |
| Seagate   | ST3250310SV        | 250 GB | 1       | 287   | 79    | 0.01   |
| WDC       | WD5000AVJS-63TRA0  | 500 GB | 1       | 2013  | 578   | 0.01   |
| WDC       | WD20SPZX-08UA7     | 2 TB   | 1       | 3     | 0     | 0.01   |
| Hitachi   | HTS541640J9AT00    | 40 GB  | 1       | 283   | 82    | 0.01   |
| HGST      | HTS725050A7E635    | 500 GB | 2       | 490   | 557   | 0.01   |
| Maxtor    | 6B200P0            | 208 GB | 1       | 43    | 12    | 0.01   |
| WDC       | WD10EADS-00R6B0    | 1 TB   | 1       | 1856  | 560   | 0.01   |
| Fujitsu   | MPE3136AT          | 16 GB  | 1       | 794   | 240   | 0.01   |
| Apple     | HDD HTS547575A9... | 752 GB | 1       | 506   | 153   | 0.01   |
| IBM/Hi... | IC35L060AVER07-0   | 64 GB  | 1       | 997   | 304   | 0.01   |
| Toshiba   | MK3261GSYN         | 320 GB | 8       | 8     | 117   | 0.01   |
| Maxtor    | 6L300S0            | 304 GB | 4       | 23    | 460   | 0.01   |
| Maxtor    | 2F020J0            | 21 GB  | 1       | 41    | 12    | 0.01   |
| Maxtor    | 6Y080P0            | 82 GB  | 7       | 16    | 7     | 0.01   |
| Maxtor    | 6E020L0            | 21 GB  | 1       | 22    | 6     | 0.01   |
| Seagate   | ST3500620AS        | 500 GB | 2       | 429   | 996   | 0.01   |
| WDC       | WD2004FBYZ-01YCBB0 | 2 TB   | 1       | 12    | 3     | 0.01   |
| Seagate   | ST3320820A         | 320 GB | 1       | 641   | 210   | 0.01   |
| Maxtor    | 6B160M0            | 163 GB | 1       | 3     | 0     | 0.01   |
| WDC       | WD800UE-22HCT0     | 80 GB  | 2       | 568   | 272   | 0.01   |
| Toshiba   | MAL2040SA-T54L     | 40 GB  | 1       | 2     | 0     | 0.01   |
| Samsung   | HM160JI            | 160 GB | 4       | 455   | 727   | 0.01   |
| Seagate   | ST500LM020-1G1162  | 500 GB | 3       | 2     | 0     | 0.01   |
| Maxtor    | 7L250S0            | 250 GB | 1       | 7     | 2     | 0.01   |
| Samsung   | SV0802N            | 80 GB  | 1       | 554   | 215   | 0.01   |
| Fujitsu   | MHW2080BJ G2       | 80 GB  | 1       | 337   | 131   | 0.01   |
| WDC       | WD5000LPCX-80VHAT1 | 500 GB | 1       | 2     | 0     | 0.01   |
| Seagate   | ST3160212SCE       | 160 GB | 1       | 2510  | 1028  | 0.01   |
| WDC       | WD3200AADS-00S9B0  | 320 GB | 1       | 26    | 10    | 0.01   |
| Maxtor    | 2B020H1            | 20 GB  | 6       | 23    | 75    | 0.01   |
| Toshiba   | MK3259GSX          | 320 GB | 1       | 192   | 82    | 0.01   |
| Seagate   | ST3160812AS Q      | 160 GB | 1       | 1049  | 480   | 0.01   |
| Toshiba   | MK6459GSX          | 640 GB | 5       | 411   | 692   | 0.01   |
| WDC       | WD2500BEVT-35ZCT0  | 250 GB | 1       | 949   | 450   | 0.01   |
| WDC       | WD800BEVS-60RST0   | 80 GB  | 1       | 1199  | 581   | 0.01   |
| Hitachi   | HDS722516VLAT20    | 164 GB | 1       | 2242  | 1102  | 0.01   |
| WDC       | WD6400AAKS-00E4A0  | 640 GB | 1       | 1016  | 521   | 0.01   |
| WDC       | WD10EURX-63UHWY0   | 1 TB   | 1       | 644   | 338   | 0.01   |
| WDC       | WD4000AAKS-22TMA0  | 400 GB | 1       | 820   | 431   | 0.01   |
| Toshiba   | MK6476GSX          | 640 GB | 16      | 7     | 318   | 0.01   |
| Seagate   | ST9320423ASG       | 320 GB | 1       | 270   | 145   | 0.01   |
| WDC       | WD20EARS-19MVWB0   | 2 TB   | 1       | 713   | 392   | 0.00   |
| Toshiba   | MK2533GSG          | 250 GB | 1       | 1671  | 948   | 0.00   |
| Hitachi   | HUA5C3020ALA640    | 2 TB   | 1       | 1045  | 595   | 0.00   |
| WDC       | WD1600BEKT-75PVMT0 | 160 GB | 1       | 1003  | 580   | 0.00   |
| Seagate   | ST5000AS0011-1L... | 5 TB   | 1       | 1743  | 1015  | 0.00   |
| Maxtor    | 6Y080L0            | 80 GB  | 34      | 21    | 314   | 0.00   |
| CLOVER    | CD155UI            | 1.5 TB | 1       | 1     | 0     | 0.00   |
| IBM/Hi... | IC35L120AVVA07-0   | 128 GB | 1       | 918   | 552   | 0.00   |
| Hitachi   | HTS723216L9A360    | 160 GB | 4       | 592   | 1378  | 0.00   |
| Toshiba   | MK5061GSY          | 500 GB | 3       | 4     | 35    | 0.00   |
| Maxtor    | 6L200M0            | 208 GB | 3       | 18    | 23    | 0.00   |
| Samsung   | HD251KJ            | 250 GB | 1       | 1539  | 1019  | 0.00   |
| Seagate   | ST3120023AS        | 120 GB | 1       | 152   | 101   | 0.00   |
| WDC       | WD3200AAKX-00U6AA0 | 320 GB | 1       | 83    | 56    | 0.00   |
| Seagate   | ST500VT000-1BS142  | 500 GB | 1       | 1     | 0     | 0.00   |
| Seagate   | ST33000651NS       | 3 TB   | 1       | 1889  | 1344  | 0.00   |
| WDC       | WD2500JD-98GBB0    | 250 GB | 1       | 875   | 628   | 0.00   |
| HGST      | HUS726060ALE614    | 6 TB   | 2       | 124   | 281   | 0.00   |
| WDC       | WD10EZEX-75WN4A1   | 1 TB   | 4       | 1     | 0     | 0.00   |
| Toshiba   | MK2556GSY          | 250 GB | 4       | 5     | 544   | 0.00   |
| WDC       | WD3200LPCX-60VHAT0 | 320 GB | 1       | 1     | 0     | 0.00   |
| WDC       | WD1200             | 120 GB | 1       | 11    | 8     | 0.00   |
| Toshiba   | MK4026GAX          | 40 GB  | 1       | 191   | 157   | 0.00   |
| Toshiba   | MK7559GSM          | 752 GB | 1       | 1015  | 847   | 0.00   |
| WDC       | WD30EZRS-11J99B1   | 3 TB   | 1       | 794   | 663   | 0.00   |
| WDC       | WD400BB-00CAA0     | 40 GB  | 1       | 194   | 163   | 0.00   |
| WDC       | WD10JUCX-63WPNY0   | 1 TB   | 1       | 87    | 73    | 0.00   |
| Maxtor    | 4R120L0            | 122 GB | 2       | 43    | 39    | 0.00   |
| Maxtor    | 7Y250M0            | 250 GB | 1       | 43    | 37    | 0.00   |
| WDC       | WD7500AACS-00ZJB0  | 752 GB | 1       | 1106  | 1007  | 0.00   |
| Maxtor    | 4D040H2            | 41 GB  | 4       | 16    | 188   | 0.00   |
| Hitachi   | HTS725032A7E630    | 320 GB | 1       | 1076  | 1028  | 0.00   |
| WDC       | WD3200JS-63PDB1    | 320 GB | 1       | 343   | 342   | 0.00   |
| WDC       | WD2003FYPS-27W9B0  | 2 TB   | 1       | 523   | 529   | 0.00   |
| Maxtor    | 6Y060L0            | 64 GB  | 4       | 24    | 63    | 0.00   |
| Seagate   | ST3750630AS        | 752 GB | 2       | 683   | 936   | 0.00   |
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
| Apple     | HDD HUA722010CL... | 1 TB   | 1       | 83    | 113   | 0.00   |
| Seagate   | ST3320620SV        | 320 GB | 1       | 564   | 835   | 0.00   |
| Fujitsu   | MHZ2120BH G2       | 120 GB | 1       | 693   | 1028  | 0.00   |
| WDC       | WD20EARS-60MVWB0   | 2 TB   | 2       | 701   | 1048  | 0.00   |
| Maxtor    | 6Y160M0            | 160 GB | 5       | 15    | 155   | 0.00   |
| WDC       | WD800AAJS-60PSA0   | 80 GB  | 1       | 624   | 1007  | 0.00   |
| Seagate   | ST3320410SV        | 320 GB | 1       | 685   | 1110  | 0.00   |
| Seagate   | ST500DM009-1BD142  | 500 GB | 1       | 0     | 0     | 0.00   |
| Maxtor    | 4D060H3            | 64 GB  | 1       | 18    | 31    | 0.00   |
| Samsung   | HM500LX            | 500 GB | 1       | 233   | 423   | 0.00   |
| Hitachi   | HUA722010CLA630    | 1 TB   | 1       | 0     | 0     | 0.00   |
| WDC       | WD15EARS-19MVWB0   | 1.5 TB | 1       | 696   | 1306  | 0.00   |
| Hitachi   | HTS723212L9A360    | 120 GB | 1       | 535   | 1012  | 0.00   |
| Hitachi   | HTS723232A7A365    | 320 GB | 1       | 1130  | 2203  | 0.00   |
| MediaMax  | WL6000GSA6457      | 6 TB   | 1       | 637   | 1372  | 0.00   |
| WDC       | WD15EURS-63S48Y0   | 1.5 TB | 1       | 11    | 26    | 0.00   |
| WDC       | WD2500BB-22RDA0    | 250 GB | 1       | 655   | 1524  | 0.00   |
| Seagate   | ST3802110ACE       | 80 GB  | 1       | 1203  | 3052  | 0.00   |
| Maxtor    | 6L300R0            | 304 GB | 1       | 7     | 20    | 0.00   |
| Seagate   | ST3750640A         | 752 GB | 1       | 732   | 2049  | 0.00   |
| Seagate   | ST3500321CS        | 500 GB | 1       | 48    | 137   | 0.00   |
| WDC       | WD3200L22X-00JVPT0 | 320 GB | 1       | 0     | 0     | 0.00   |
| WDC       | WD2500BEKT-60F3T1  | 250 GB | 1       | 533   | 1607  | 0.00   |
| Seagate   | ST250LT012-9WS141  | 250 GB | 4       | 337   | 1077  | 0.00   |
| Seagate   | ST980817AS         | 80 GB  | 1       | 310   | 1009  | 0.00   |
| Maxtor    | 7L300S0            | 304 GB | 2       | 6     | 24    | 0.00   |
| WDC       | WD5000LPLX-60ZNTT0 | 500 GB | 1       | 0     | 0     | 0.00   |
| Hitachi   | HTS542580K9A300    | 80 GB  | 2       | 267   | 1012  | 0.00   |
| Seagate   | ST9320312AS        | 320 GB | 2       | 264   | 1108  | 0.00   |
| Samsung   | SV2011H            | 20 GB  | 1       | 0     | 3     | 0.00   |
| WDC       | WD2500AAJS-55B4A0  | 250 GB | 1       | 476   | 2020  | 0.00   |
| Toshiba   | MK2555GSX H        | 250 GB | 1       | 428   | 1908  | 0.00   |
| WDC       | WD800 AAJS-00PSA0  | 80 GB  | 1       | 97    | 459   | 0.00   |
| HGST      | HUS726020ALA610    | 2 TB   | 1       | 0     | 0     | 0.00   |
| Maxtor    | 6B120P0            | 122 GB | 1       | 0     | 0     | 0.00   |
| Seagate   | ST3160316CS        | 160 GB | 1       | 0     | 0     | 0.00   |
| WDC       | WD2005FBYZ-01YCBB1 | 2 TB   | 1       | 0     | 0     | 0.00   |
| WDC       | WD40NPZZ-00PDPT0   | 4 TB   | 1       | 0     | 0     | 0.00   |
| Samsung   | HM320JX            | 320 GB | 1       | 37    | 331   | 0.00   |
| Seagate   | ST980829A          | 80 GB  | 1       | 222   | 2022  | 0.00   |
| Seagate   | MB0500EAMZD        | 500 GB | 1       | 94    | 857   | 0.00   |
| Maxtor    | 7L300R0            | 304 GB | 1       | 11    | 116   | 0.00   |
| Toshiba   | MK8025GAL          | 80 GB  | 1       | 78    | 1017  | 0.00   |
| Maxtor    | 53073H6            | 32 GB  | 1       | 121   | 2068  | 0.00   |
| WDC       | WD20EADS-22R6B0    | 2 TB   | 1       | 105   | 1848  | 0.00   |
| Hitachi   | HTS548060M9AT00    | 64 GB  | 1       | 35    | 655   | 0.00   |
| Maxtor    | 6L200S0            | 208 GB | 1       | 2     | 39    | 0.00   |
| Seagate   | ST3000VX010-2H916L | 3 TB   | 2       | 0     | 0     | 0.00   |
| WDC       | WD120EMFZ-11A6JA0  | 12 TB  | 1       | 0     | 0     | 0.00   |
| WDC       | WD60PURX-64T0ZY1   | 6 TB   | 1       | 0     | 0     | 0.00   |
| WDC       | WD5000LMVW-11VEDS3 | 500 GB | 1       | 34    | 1094  | 0.00   |
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
| Hitachi   | Sun Original           | 2      | 11      | 2609  | 0     | 7.15   |
| Seagate   | SpinPoint F4 EG (AF)   | 1      | 1       | 2366  | 0     | 6.48   |
| Seagate   | Barracuda ES+          | 2      | 2       | 2199  | 0     | 6.03   |
| Samsung   | SpinPoint F3 RE        | 1      | 1       | 1865  | 0     | 5.11   |
| Hitachi   | CinemaStar 5K320       | 2      | 2       | 1702  | 0     | 4.67   |
| Samsung   | SpinPoint PL40         | 1      | 2       | 3755  | 9     | 4.62   |
| Hitachi   | Deskstar 7K4000        | 1      | 3       | 1910  | 454   | 4.58   |
| Apple     | Travelstar 7K750       | 1      | 1       | 1579  | 0     | 4.33   |
| HP        | RE3                    | 1      | 1       | 1490  | 0     | 4.08   |
| Quantum   | Unknown                | 1      | 1       | 1486  | 0     | 4.07   |
| WDC       | RE4-GP                 | 5      | 10      | 1639  | 53    | 4.03   |
| Toshiba   | 3.5" HDD MK.002TSKB    | 1      | 1       | 1446  | 0     | 3.96   |
| Seagate   | Laptop Thin            | 1      | 1       | 1394  | 0     | 3.82   |
| HP        | Constellation ES.3     | 1      | 1       | 1370  | 0     | 3.76   |
| WDC       | RE2                    | 7      | 14      | 1541  | 43    | 3.71   |
| Hitachi   | Deskstar 7K2000        | 1      | 23      | 1649  | 12    | 3.54   |
| HP        | Unknown                | 1      | 1       | 1274  | 0     | 3.49   |
| Hitachi   | Ultrastar A7K2000      | 7      | 34      | 1578  | 32    | 3.39   |
| Hitachi   | Ultrastar A7K1000      | 4      | 7       | 1770  | 280   | 3.30   |
| WDC       | Raptor X               | 1      | 1       | 1164  | 0     | 3.19   |
| Toshiba   | 1.8" HDD MK..17GSG     | 1      | 1       | 1162  | 0     | 3.18   |
| Toshiba   | 3.5" DT01ABA Deskto... | 2      | 9       | 1156  | 0     | 3.17   |
| HGST      | MegaScale 4000         | 2      | 6       | 1155  | 0     | 3.17   |
| WDC       | WDC Enterprise         | 1      | 1       | 1134  | 0     | 3.11   |
| Seagate   | Enterprise NAS HDD     | 1      | 3       | 1128  | 0     | 3.09   |
| Seagate   | Constellation.2 (SATA) | 2      | 14      | 1225  | 1     | 3.09   |
| Hitachi   | Deskstar 7K3000        | 4      | 67      | 1273  | 55    | 2.98   |
| WDC       | RE3                    | 15     | 59      | 1380  | 5     | 2.83   |
| WDC       | Purple NV              | 1      | 1       | 1023  | 0     | 2.80   |
| Toshiba   | 3.5" HDD               | 1      | 1       | 1008  | 0     | 2.76   |
| HGST      | Deskstar NAS           | 5      | 25      | 998   | 0     | 2.74   |
| Samsung   | SpinPoint F4 EG (AF)   | 2      | 32      | 1189  | 63    | 2.70   |
| Hitachi   | Ultrastar 7K3000       | 3      | 35      | 1012  | 1     | 2.70   |
| Seagate   | Constellation.2        | 2      | 2       | 983   | 0     | 2.69   |
| HGST      | Ultrastar 7K4000       | 5      | 44      | 1009  | 1     | 2.68   |
| Toshiba   | 2.5" HDD MQ01UBB       | 1      | 4       | 952   | 0     | 2.61   |
| HP        | Proliant HardDrive     | 8      | 10      | 1412  | 37    | 2.55   |
| Seagate   | Archive HDD            | 2      | 20      | 1013  | 51    | 2.54   |
| Seagate   | Desktop HDD.15         | 4      | 58      | 949   | 48    | 2.47   |
| Seagate   | U5                     | 2      | 2       | 875   | 0     | 2.40   |
| Toshiba   | 2.5" HDD MQ01ABF..H    | 1      | 2       | 873   | 0     | 2.39   |
| Hitachi   | Deskstar 5K3000        | 4      | 22      | 1094  | 29    | 2.37   |
| Quantum   | Fireball Plus AS       | 2      | 2       | 845   | 0     | 2.32   |
| Samsung   | SpinPoint              | 3      | 4       | 931   | 108   | 2.28   |
| WDC       | Se                     | 4      | 8       | 1128  | 1     | 2.25   |
| Seagate   | Constellation ES.2 ... | 4      | 12      | 1276  | 120   | 2.21   |
| Hitachi   | Ultrastar 7K4000       | 2      | 9       | 846   | 140   | 2.19   |
| WDC       | Caviar SE16            | 5      | 33      | 1015  | 18    | 2.13   |
| Seagate   | NAS HDD                | 7      | 26      | 808   | 78    | 2.07   |
| Seagate   | Barracuda 7200.7       | 1      | 3       | 1192  | 70    | 2.05   |
| WDC       | RE                     | 21     | 42      | 930   | 47    | 2.01   |
| WDC       | Caviar Black           | 45     | 373     | 954   | 40    | 2.01   |
| Maxtor    | MaXLine Pro 500        | 1      | 1       | 726   | 0     | 1.99   |
| Seagate   | Barracuda ES           | 6      | 35      | 1217  | 366   | 1.96   |
| Samsung   | SpinPoint F1 RE        | 2      | 3       | 824   | 34    | 1.90   |
| Seagate   | Barracuda 7200.8       | 9      | 41      | 1227  | 96    | 1.87   |
| Hitachi   | Deskstar 7K1000        | 3      | 15      | 1200  | 17    | 1.87   |
| WDC       | VelociRaptor           | 24     | 49      | 740   | 1     | 1.83   |
| Seagate   | Barracuda XT           | 2      | 15      | 826   | 175   | 1.79   |
| Toshiba   | 3.5" HDD DT01ABA..V    | 2      | 2       | 642   | 0     | 1.76   |
| Hitachi   | Deskstar T7K500        | 8      | 55      | 1103  | 75    | 1.76   |
| WDC       | Raptor                 | 12     | 19      | 1197  | 12    | 1.76   |
| Maxtor    | MaXLine III (SATA/300) | 2      | 4       | 1049  | 238   | 1.73   |
| WDC       | Caviar SE              | 146    | 475     | 897   | 25    | 1.72   |
| Hitachi   | Deskstar 7K80          | 6      | 69      | 883   | 36    | 1.71   |
| Hitachi   | Deskstar 5K1000        | 3      | 23      | 770   | 60    | 1.70   |
| Seagate   | Barracuda Pro          | 1      | 1       | 619   | 0     | 1.70   |
| HGST      | Deskstar 7K4000        | 1      | 1       | 598   | 0     | 1.64   |
| HGST      | Travelstar 5K1500      | 2      | 3       | 928   | 10    | 1.62   |
| Samsung   | SpinPoint F3           | 4      | 199     | 792   | 40    | 1.62   |
| Hitachi   | CinemaStar 5K1000      | 3      | 4       | 726   | 1     | 1.62   |
| Apple     | SpinPoint              | 1      | 1       | 589   | 0     | 1.61   |
| WDC       | Red                    | 23     | 358     | 712   | 14    | 1.59   |
| Toshiba   | 2.5" HDD MQ01ABC       | 1      | 1       | 574   | 0     | 1.57   |
| WDC       | Caviar Green           | 132    | 1224    | 891   | 73    | 1.57   |
| WDC       | Red Pro                | 7      | 8       | 573   | 0     | 1.57   |
| Samsung   | SpinPoint T133         | 5      | 23      | 939   | 154   | 1.57   |
| Seagate   | Constellation ES (S... | 4      | 18      | 1162  | 191   | 1.55   |
| Apple     | MK..65GSXF             | 1      | 1       | 560   | 0     | 1.54   |
| Hitachi   | Deskstar E7K500        | 2      | 2       | 559   | 0     | 1.53   |
| Fujitsu   | MPA..MPG               | 5      | 6       | 711   | 42    | 1.53   |
| Seagate   | Barracuda Green (AF)   | 4      | 138     | 892   | 208   | 1.52   |
| Samsung   | SpinPoint F2 EG        | 3      | 89      | 868   | 190   | 1.51   |
| Seagate   | DB35.3                 | 6      | 12      | 654   | 193   | 1.48   |
| Seagate   | Barracuda 7200.10      | 33     | 1150    | 875   | 260   | 1.46   |
| Seagate   | Exos 7E8               | 1      | 1       | 533   | 0     | 1.46   |
| Toshiba   | 3.5" MD04ACA Enterp... | 2      | 9       | 728   | 445   | 1.45   |
| Hitachi   | Deskstar T7K250        | 5      | 30      | 1008  | 43    | 1.43   |
| WDC       | RE2-GP                 | 2      | 2       | 608   | 2     | 1.42   |
| Hitachi   | Deskstar 7K1000.B      | 11     | 97      | 957   | 57    | 1.41   |
| Seagate   | UX                     | 1      | 6       | 787   | 13    | 1.37   |
| Seagate   | Video 3.5 HDD          | 8      | 21      | 577   | 206   | 1.36   |
| Hitachi   | Deskstar 7K250         | 7      | 13      | 962   | 284   | 1.36   |
| WDC       | Green                  | 6      | 99      | 523   | 1     | 1.35   |
| WDC       | RE4                    | 17     | 84      | 776   | 3     | 1.35   |
| Samsung   | SpinPoint F1 DT        | 11     | 240     | 963   | 214   | 1.35   |
| Seagate   | U9                     | 2      | 5       | 490   | 0     | 1.34   |
| WDC       | Black                  | 17     | 133     | 565   | 19    | 1.34   |
| Seagate   | Barracuda 7200.7 an... | 19     | 564     | 846   | 86    | 1.33   |
| Hitachi   | Deskstar 7K1000.C      | 14     | 436     | 721   | 54    | 1.33   |
| Seagate   | Barracuda 5400.1       | 1      | 5       | 835   | 33    | 1.32   |
| Apple     | HGST Travelstar Z5K500 | 1      | 14      | 496   | 2     | 1.30   |
| Maxtor    | DiamondMax 10 (SATA... | 6      | 28      | 687   | 39    | 1.30   |
| Toshiba   | 2.5" HDD MK..32GSX     | 1      | 5       | 497   | 1     | 1.29   |
| Toshiba   | 2.5" HDD MQ03ABB       | 1      | 1       | 468   | 0     | 1.28   |
| Seagate   | Constellation ES.2     | 1      | 1       | 467   | 0     | 1.28   |
| Seagate   | Laptop HDD             | 2      | 2       | 466   | 0     | 1.28   |
| Samsung   | SpinPoint VL40         | 1      | 1       | 2328  | 4     | 1.28   |
| WDC       | Black SSHD             | 1      | 7       | 460   | 0     | 1.26   |
| Toshiba   | Toshiba Enterprise     | 1      | 10      | 456   | 0     | 1.25   |
| WDC       | Caviar                 | 62     | 151     | 723   | 37    | 1.24   |
| Apple     | Barracuda              | 1      | 9       | 448   | 0     | 1.23   |
| Seagate   | Constellation ES.3     | 4      | 40      | 527   | 70    | 1.22   |
| Seagate   | Momentus XT (AF)       | 1      | 11      | 494   | 96    | 1.20   |
| HP        | 250GB SATA disk VB0... | 1      | 6       | 976   | 7     | 1.19   |
| Seagate   | Barracuda SpinPoint F3 | 2      | 48      | 515   | 8     | 1.17   |
| Hitachi   | Deskstar 7K160         | 7      | 146     | 882   | 104   | 1.17   |
| Seagate   | Barracuda 7200.9       | 33     | 464     | 788   | 420   | 1.16   |
| WDC       | Scorpio Blue EIDE      | 6      | 10      | 421   | 0     | 1.16   |
| Samsung   | SpinPoint F3 EG        | 4      | 30      | 655   | 139   | 1.15   |
| Hitachi   | Deskstar P7K500        | 9      | 145     | 921   | 61    | 1.14   |
| WDC       | Caviar Blue            | 300    | 2816    | 632   | 47    | 1.14   |
| Toshiba   | 2.5" HDD MK..75GSX     | 1      | 1       | 412   | 0     | 1.13   |
| Seagate   | Enterprise Capacity... | 10     | 34      | 410   | 0     | 1.12   |
| Seagate   | SpinPoint M7E          | 2      | 14      | 424   | 2     | 1.12   |
| WDC       | AV                     | 17     | 36      | 647   | 51    | 1.12   |
| Seagate   | Barracuda 7200.12      | 14     | 1185    | 726   | 177   | 1.12   |
| Seagate   | IronWolf               | 11     | 67      | 436   | 2     | 1.10   |
| HGST      | Ultrastar He10         | 1      | 1       | 399   | 0     | 1.09   |
| Fujitsu   | MHW BH                 | 9      | 44      | 551   | 39    | 1.08   |
| Toshiba   | 2.5" HDD MK..59GSXP... | 1      | 4       | 450   | 7     | 1.05   |
| Seagate   | SV35.5                 | 1      | 3       | 769   | 20    | 1.05   |
| Seagate   | Exos 7E2               | 2      | 3       | 829   | 124   | 1.04   |
| Seagate   | IronWolf Pro           | 7      | 20      | 499   | 6     | 1.04   |
| Seagate   | Barracuda ES.2         | 4      | 36      | 1049  | 379   | 1.02   |
| Seagate   | SpinPoint D8X          | 1      | 2       | 559   | 404   | 1.02   |
| Seagate   | Pipeline HD 5900.2     | 8      | 60      | 590   | 162   | 1.02   |
| WDC       | AV-GP                  | 32     | 84      | 572   | 66    | 1.01   |
| Seagate   | Momentus               | 4      | 10      | 611   | 152   | 1.01   |
| ExcelStor | Jupiter                | 6      | 14      | 685   | 14    | 1.01   |
| WDC       | Caviar Blue EIDE       | 17     | 96      | 620   | 65    | 1.00   |
| Seagate   | SV35                   | 12     | 85      | 447   | 147   | 0.99   |
| Seagate   | Barracuda 7200.14 (AF) | 25     | 1745    | 505   | 114   | 0.99   |
| Seagate   | Desktop SSHD           | 6      | 69      | 475   | 84    | 0.99   |
| WDC       | Elements / My Passport | 39     | 127     | 447   | 51    | 0.98   |
| Apple     | Travelstar 5K1000      | 2      | 15      | 380   | 135   | 0.98   |
| Toshiba   | 2.5" HDD MK..61GSY     | 1      | 1       | 354   | 0     | 0.97   |
| Hitachi   | CinemaStar P7K500      | 1      | 2       | 1010  | 2     | 0.97   |
| Seagate   | Constellation CS       | 3      | 10      | 496   | 299   | 0.95   |
| Maxtor    | DiamondMax 21          | 16     | 193     | 710   | 382   | 0.94   |
| HGST      | Ultrastar 7K2          | 2      | 6       | 343   | 0     | 0.94   |
| Toshiba   | X300                   | 4      | 21      | 338   | 0     | 0.93   |
| Seagate   | Video 2.5              | 3      | 10      | 337   | 0     | 0.93   |
| Seagate   | SpinPoint M9T          | 2      | 35      | 386   | 6     | 0.91   |
| Fujitsu   | MHY BH                 | 5      | 60      | 530   | 142   | 0.91   |
| Seagate   | Barracuda              | 2      | 8       | 325   | 0     | 0.89   |
| Toshiba   | 3.5" MG04ACA Enterp... | 2      | 9       | 320   | 1     | 0.87   |
| Samsung   | SpinPoint P80 SD       | 7      | 207     | 820   | 395   | 0.87   |
| Toshiba   | 3.5" HDD DT01ACA       | 4      | 703     | 350   | 22    | 0.86   |
| Samsung   | SpinPoint T166         | 7      | 155     | 871   | 411   | 0.85   |
| Hitachi   | Travelstar 7K320       | 11     | 23      | 634   | 602   | 0.85   |
| MediaMax  | WL5000                 | 1      | 1       | 308   | 0     | 0.85   |
| HGST      | Ultrastar He8          | 3      | 10      | 307   | 0     | 0.84   |
| WDC       | Gold                   | 7      | 15      | 307   | 0     | 0.84   |
| Fujitsu   | MHZ BH                 | 9      | 69      | 517   | 286   | 0.84   |
| Toshiba   | 2.5" HDD MQ03UBB       | 2      | 8       | 331   | 2     | 0.84   |
| Samsung   | SpinPoint F4           | 2      | 29      | 500   | 114   | 0.83   |
| Samsung   | SpinPoint F1 EG        | 1      | 2       | 483   | 9     | 0.83   |
| WDC       | Scorpio                | 1      | 1       | 300   | 0     | 0.82   |
| Seagate   | Barracuda ATA V        | 3      | 4       | 1510  | 35    | 0.82   |
| Toshiba   | 2.5" HDD MQ01UBD       | 2      | 18      | 402   | 240   | 0.82   |
| Seagate   | Constellation ES (S... | 3      | 24      | 924   | 45    | 0.81   |
| MediaMax  | WL1000                 | 2      | 2       | 509   | 6     | 0.80   |
| Seagate   | Surveillance           | 5      | 12      | 289   | 0     | 0.79   |
| Samsung   | SpinPoint M7E (AF)     | 4      | 120     | 459   | 82    | 0.79   |
| Seagate   | Barracuda LP           | 4      | 67      | 808   | 371   | 0.78   |
| HP        | Ultrastar 7K4000       | 1      | 1       | 1419  | 4     | 0.78   |
| Toshiba   | 2.5" HDD MK..58GSX     | 1      | 3       | 452   | 3     | 0.78   |
| Hitachi   | Travelstar 5K500.B     | 13     | 373     | 505   | 148   | 0.77   |
| Hitachi   | Travelstar 7K100       | 5      | 12      | 498   | 24    | 0.77   |
| WDC       | Scorpio Blue           | 209    | 1849    | 419   | 60    | 0.77   |
| Fujitsu   | MHX BT                 | 2      | 5       | 619   | 30    | 0.77   |
| Samsung   | SpinPoint S166         | 3      | 58      | 843   | 455   | 0.76   |
| HGST      | Ultrastar 7K6000       | 10     | 17      | 286   | 34    | 0.74   |
| IBM/Hi... | Deskstar GXP-180       | 4      | 5       | 604   | 2     | 0.74   |
| WDC       | Scorpio Black          | 44     | 171     | 438   | 101   | 0.74   |
| WDC       | Black UltraSlim        | 1      | 1       | 267   | 0     | 0.73   |
| Toshiba   | 3.5" MG03ACAxxx(Y) ... | 4      | 14      | 450   | 3     | 0.73   |
| Toshiba   | 2.5" HDD               | 18     | 55      | 451   | 46    | 0.72   |
| Hitachi   | Travelstar 5K750       | 3      | 265     | 461   | 370   | 0.72   |
| HGST      | CinemaStar Z5K500      | 1      | 1       | 523   | 1     | 0.72   |
| Seagate   | Momentus 7200.3        | 7      | 15      | 569   | 28    | 0.71   |
| Seagate   | Barracuda V            | 1      | 1       | 259   | 0     | 0.71   |
| Seagate   | Maxtor DiamondMax 23   | 4      | 56      | 661   | 271   | 0.71   |
| Seagate   | Barracuda ATA IV       | 4      | 51      | 615   | 27    | 0.71   |
| Seagate   | Momentus 5400.2        | 13     | 45      | 441   | 361   | 0.70   |
| Maxtor    | DiamondMax Plus D740X  | 2      | 3       | 834   | 4     | 0.70   |
| Toshiba   | 2.5" HDD MQ04UBF       | 1      | 7       | 252   | 0     | 0.69   |
| WDC       | Purple                 | 13     | 47      | 305   | 46    | 0.69   |
| HGST      | Travelstar 7K1000      | 4      | 224     | 296   | 117   | 0.69   |
| Seagate   | Momentus 7200.2        | 6      | 14      | 642   | 312   | 0.68   |
| Seagate   | SpinPoint M8 (AF)      | 6      | 783     | 343   | 47    | 0.67   |
| Seagate   | Momentus 7200.5        | 4      | 76      | 447   | 92    | 0.66   |
| Samsung   | SpinPoint M7           | 3      | 118     | 363   | 44    | 0.66   |
| Seagate   | U6                     | 3      | 16      | 645   | 38    | 0.66   |
| Fujitsu   | MHV                    | 23     | 77      | 416   | 13    | 0.65   |
| Seagate   | LD25.2                 | 2      | 2       | 383   | 1     | 0.65   |
| Seagate   | Pipeline HD Mini       | 4      | 11      | 596   | 162   | 0.64   |
| Samsung   | SpinPoint S250         | 2      | 51      | 804   | 645   | 0.64   |
| WDC       | Blue SSHD              | 2      | 2       | 230   | 0     | 0.63   |
| Seagate   | Momentus 7200.4        | 7      | 184     | 522   | 351   | 0.63   |
| Hitachi   | Deskstar 7K500         | 1      | 4       | 1530  | 15    | 0.63   |
| HGST      | Travelstar 5K1000      | 5      | 191     | 332   | 303   | 0.63   |
| Samsung   | SpinPoint MT2          | 1      | 3       | 228   | 0     | 0.63   |
| Toshiba   | 2.5" HDD MK..59GSM     | 2      | 28      | 608   | 813   | 0.60   |
| Hitachi   | CinemaStar 7K1000.B    | 2      | 4       | 218   | 0     | 0.60   |
| WDC       | Green Mobile           | 1      | 3       | 336   | 12    | 0.60   |
| WDC       | Blue Mobile            | 80     | 1111    | 246   | 13    | 0.59   |
| Samsung   | SpinPoint M8 (AF)      | 5      | 61      | 394   | 104   | 0.58   |
| Toshiba   | 3.5" HDD E300          | 2      | 5       | 213   | 0     | 0.58   |
| Seagate   | Barracuda 3.5          | 9      | 348     | 225   | 14    | 0.58   |
| HGST      | Edurastar              | 1      | 1       | 211   | 0     | 0.58   |
| Hitachi   | Travelstar Z7K500      | 2      | 9       | 453   | 709   | 0.58   |
| HGST      | Ultrastar DC HC520 ... | 3      | 5       | 209   | 0     | 0.57   |
| Hitachi   | Deskstar 7K1000.D      | 2      | 80      | 614   | 513   | 0.57   |
| Hitachi   | Travelstar 7K200       | 7      | 16      | 586   | 88    | 0.57   |
| Seagate   | FireCuda 3.5           | 2      | 33      | 206   | 1     | 0.56   |
| Hitachi   | Travelstar 7K750       | 2      | 26      | 479   | 292   | 0.56   |
| HGST      | Travelstar Z7K500      | 6      | 145     | 299   | 184   | 0.56   |
| Toshiba   | 2.5" HDD MK..59GSM     | 1      | 17      | 487   | 241   | 0.56   |
| Toshiba   | 2.5" HDD MQ01ABD       | 7      | 531     | 299   | 124   | 0.55   |
| Maxtor    | DiamondMax D540X-4K    | 3      | 3       | 582   | 16    | 0.54   |
| Seagate   | Momentus XT            | 1      | 9       | 387   | 232   | 0.54   |
| Seagate   | Momentus 5400 PSD      | 2      | 3       | 352   | 338   | 0.53   |
| Samsung   | SpinPoint P80          | 18     | 107     | 567   | 135   | 0.53   |
| Seagate   | Barracuda ATA III      | 1      | 1       | 194   | 0     | 0.53   |
| Toshiba   | 2.5" HDD MQ02ABD..H    | 1      | 12      | 294   | 4     | 0.53   |
| Fujitsu   | MHW BJ                 | 3      | 3       | 305   | 44    | 0.53   |
| Samsung   | SpinPoint MP5          | 3      | 7       | 371   | 187   | 0.52   |
| Hitachi   | Travelstar Z5K500      | 3      | 127     | 346   | 161   | 0.52   |
| Seagate   | Video 3.5              | 1      | 3       | 186   | 0     | 0.51   |
| Seagate   | Barracuda Compute      | 4      | 26      | 206   | 58    | 0.51   |
| Seagate   | Skyhawk                | 5      | 14      | 189   | 1     | 0.51   |
| IBM/Hi... | Deskstar 120GXP        | 4      | 8       | 655   | 117   | 0.50   |
| Seagate   | Laptop SSHD            | 7      | 161     | 297   | 121   | 0.50   |
| Fujitsu   | MHZ BT                 | 1      | 2       | 1426  | 6     | 0.50   |
| Seagate   | DB35.4                 | 1      | 2       | 701   | 21    | 0.49   |
| Toshiba   | 2.5" HDD MQ01ABF       | 2      | 30      | 204   | 35    | 0.49   |
| WDC       | Black Mobile           | 27     | 173     | 199   | 10    | 0.49   |
| Fujitsu   | MJA BH                 | 7      | 36      | 376   | 183   | 0.48   |
| Maxtor    | DiamondMax 17          | 2      | 9       | 314   | 101   | 0.48   |
| Hitachi   | Travelstar Z5K320      | 3      | 199     | 328   | 318   | 0.48   |
| Toshiba   | L200                   | 3      | 10      | 175   | 0     | 0.48   |
| Maxtor    | DiamondMax 20          | 6      | 20      | 544   | 308   | 0.48   |
| Hitachi   | Travelstar 5K1000      | 3      | 20      | 449   | 678   | 0.48   |
| Seagate   | Momentus 5400.3        | 7      | 125     | 452   | 486   | 0.48   |
| Toshiba   | 2.5" HDD MQ01ACF       | 2      | 23      | 235   | 103   | 0.47   |
| Hitachi   | Travelstar 5K250       | 10     | 169     | 553   | 146   | 0.47   |
| WDC       | Protege                | 6      | 10      | 614   | 18    | 0.47   |
| Toshiba   | N300                   | 2      | 10      | 223   | 7     | 0.47   |
| Toshiba   | 2.5" HDD MK..63GSX     | 2      | 14      | 603   | 21    | 0.47   |
| Seagate   | Momentus 5400.4        | 3      | 71      | 475   | 306   | 0.47   |
| Toshiba   | 2.5" HDD MK..37GSX     | 1      | 18      | 451   | 136   | 0.47   |
| Hitachi   | CinemaStar 5K1000.B    | 1      | 1       | 169   | 0     | 0.47   |
| WDC       | Blue UltraSlim         | 1      | 1       | 166   | 0     | 0.46   |
| Seagate   | FreePlay               | 3      | 11      | 231   | 744   | 0.46   |
| Fujitsu   | MHW AT                 | 2      | 2       | 165   | 0     | 0.45   |
| WDC       | Blue                   | 58     | 424     | 169   | 1     | 0.45   |
| WDC       | HGST Ultrastar He10    | 4      | 28      | 163   | 0     | 0.45   |
| Toshiba   | 2.5" HDD MK..75GSX     | 4      | 75      | 418   | 395   | 0.44   |
| Toshiba   | 2.5" HDD MK..55GSX     | 6      | 64      | 402   | 70    | 0.44   |
| Hitachi   | Travelstar 5K320       | 11     | 111     | 534   | 224   | 0.43   |
| Seagate   | MobileMax-2            | 1      | 1       | 155   | 0     | 0.43   |
| Samsung   | SpinPoint V80          | 3      | 4       | 597   | 63    | 0.42   |
| Samsung   | SpinPoint V60          | 1      | 6       | 1055  | 104   | 0.42   |
| Hitachi   | Travelstar Z7K320      | 3      | 32      | 398   | 551   | 0.42   |
| Toshiba   | P300                   | 4      | 224     | 158   | 17    | 0.42   |
| Toshiba   | Enterprise Surveill... | 1      | 1       | 1037  | 6     | 0.41   |
| Magnet... | Unknown                | 4      | 4       | 146   | 0     | 0.40   |
| MediaMax  | WL320                  | 1      | 1       | 146   | 0     | 0.40   |
| Hitachi   | Travelstar 5K500       | 1      | 6       | 520   | 5     | 0.40   |
| Samsung   | SpinPoint P120         | 5      | 82      | 912   | 647   | 0.39   |
| Seagate   | Terascale              | 1      | 1       | 143   | 0     | 0.39   |
| Hitachi   | Travelstar 7K500       | 8      | 67      | 439   | 740   | 0.39   |
| Toshiba   | 1.8" HDD               | 5      | 9       | 332   | 14    | 0.38   |
| Seagate   | Momentus 5400.7        | 1      | 9       | 466   | 436   | 0.37   |
| Hitachi   | Deskstar E7K1000       | 2      | 3       | 1464  | 64    | 0.37   |
| Seagate   | Momentus 5400.6        | 10     | 802     | 454   | 490   | 0.37   |
| Seagate   | FireCuda 2.5           | 5      | 58      | 157   | 47    | 0.37   |
| Seagate   | SpinPoint F4           | 1      | 5       | 477   | 88    | 0.37   |
| Toshiba   | 2.5" HDD MK..59GSXP    | 7      | 116     | 372   | 318   | 0.36   |
| Quantum   | Fireball lct15         | 3      | 3       | 226   | 2     | 0.36   |
| Seagate   | Laptop Ultrathin       | 1      | 1       | 131   | 0     | 0.36   |
| Toshiba   | 2.5" HDD MQ01ABF       | 1      | 302     | 164   | 77    | 0.36   |
| Fujitsu   | MHT                    | 5      | 6       | 389   | 16    | 0.35   |
| Hitachi   | Travelstar 5K100       | 9      | 50      | 411   | 56    | 0.35   |
| Seagate   | Momentus 5400.7 (AF)   | 2      | 14      | 534   | 451   | 0.35   |
| Toshiba   | 3.5" HDD DT01ACA       | 2      | 4       | 127   | 0     | 0.35   |
| Hitachi   | Travelstar 5K160       | 11     | 152     | 488   | 72    | 0.34   |
| Toshiba   | 1.8" HDD MK..16GSG     | 1      | 3       | 272   | 4     | 0.34   |
| Seagate   | Barracuda 2.5 5400     | 6      | 116     | 135   | 4     | 0.34   |
| HGST      | Travelstar Z5K1000     | 2      | 28      | 150   | 75    | 0.34   |
| Seagate   | SV35.2                 | 3      | 7       | 578   | 1005  | 0.32   |
| HGST      | Travelstar Z5K500      | 5      | 431     | 259   | 313   | 0.32   |
| Hitachi   | Travelstar 5K120       | 2      | 4       | 384   | 5     | 0.32   |
| Toshiba   | 2.5" HDD MK..34GSX     | 2      | 12      | 356   | 180   | 0.32   |
| Toshiba   | 2.5" HDD MK..65GSX     | 13     | 187     | 462   | 316   | 0.32   |
| Seagate   | Momentus Thin          | 6      | 166     | 359   | 599   | 0.31   |
| Seagate   | BarraCuda Pro          | 3      | 4       | 119   | 1     | 0.31   |
| Seagate   | Momentus 7200.1        | 2      | 7       | 552   | 471   | 0.30   |
| Seagate   | Ultra Mobile HDD       | 2      | 3       | 107   | 0     | 0.30   |
| Seagate   | Mobile HDD             | 3      | 243     | 129   | 85    | 0.29   |
| HGST      | Travelstar Z5K1        | 1      | 21      | 106   | 0     | 0.29   |
| China     | Unknown                | 1      | 1       | 106   | 0     | 0.29   |
| Toshiba   | 2.5" HDD MK..76GSX     | 6      | 14      | 186   | 138   | 0.29   |
| Toshiba   | 2.5" HDD MK..55GSX     | 3      | 5       | 337   | 551   | 0.29   |
| Toshiba   | 2.5" HDD H200          | 2      | 4       | 103   | 0     | 0.28   |
| Seagate   | SpinPoint M8U (USB)    | 2      | 12      | 147   | 1     | 0.27   |
| IBM       | Deskstar 40GV & 75G... | 3      | 4       | 1041  | 24    | 0.27   |
| Seagate   | Unknown                | 3      | 3       | 158   | 1     | 0.27   |
| Toshiba   | V300                   | 1      | 1       | 97    | 0     | 0.27   |
| Toshiba   | 2.5" HDD MK..46GSX     | 1      | 11      | 401   | 42    | 0.27   |
| WDC       | Shrek LT 2.5           | 2      | 2       | 96    | 0     | 0.27   |
| Seagate   | Laptop Thin HDD        | 7      | 677     | 238   | 399   | 0.26   |
| Seagate   | Laptop Thin SSHD       | 1      | 1       | 94    | 0     | 0.26   |
| WDC       | Ultrastar He10/12      | 1      | 1       | 93    | 0     | 0.26   |
| Samsung   | SpinPoint M            | 2      | 9       | 301   | 19    | 0.25   |
| Toshiba   | 2.5" HDD MK..37GSX     | 2      | 45      | 532   | 82    | 0.25   |
| Seagate   | BarraCuda 3.5          | 3      | 62      | 105   | 3     | 0.25   |
| Toshiba   | 2.5" HDD MK..46GSX     | 4      | 39      | 490   | 59    | 0.25   |
| Toshiba   | 2.5" HDD L200 Slim     | 1      | 5       | 90    | 0     | 0.25   |
| Seagate   | Momentus 4200.2        | 5      | 6       | 433   | 350   | 0.25   |
| IBM/Hi... | Deskstar 60GXP         | 2      | 3       | 1032  | 106   | 0.24   |
| Seagate   | Barracuda 7200.11      | 12     | 307     | 827   | 352   | 0.22   |
| Toshiba   | 1.8" HDD MK..33GSG     | 2      | 3       | 634   | 316   | 0.21   |
| HGST      | Ultrastar DC HC320     | 1      | 1       | 75    | 0     | 0.21   |
| Seagate   | LD25 Series            | 2      | 3       | 161   | 695   | 0.20   |
| Toshiba   | 2.5" HDD L200          | 2      | 13      | 93    | 87    | 0.20   |
| Seagate   | SpinPoint M9TU (USB)   | 1      | 1       | 67    | 0     | 0.19   |
| Samsung   | SpinPoint M40/60/80    | 9      | 19      | 473   | 320   | 0.19   |
| Toshiba   | 2.5" HDD MK..52GSX     | 5      | 60      | 517   | 142   | 0.18   |
| HGST      | Travelstar Z5K500.B    | 1      | 17      | 65    | 0     | 0.18   |
| Seagate   | Momentus 5400.5        | 4      | 75      | 399   | 185   | 0.18   |
| Seagate   | Barracuda Pro Compute  | 2      | 45      | 65    | 0     | 0.18   |
| Toshiba   | 2.5" HDD MQ04ABF       | 1      | 72      | 69    | 15    | 0.16   |
| Toshiba   | 2.5" HDD MK..61GSY[N]  | 5      | 31      | 102   | 249   | 0.16   |
| Toshiba   | 2.5" HDD MQ01ABD       | 1      | 2       | 57    | 0     | 0.16   |
| WDC       | Unknown                | 3      | 3       | 464   | 5     | 0.15   |
| IBM/Hi... | Hitachi Travelstar ... | 4      | 13      | 348   | 41    | 0.15   |
| Toshiba   | 2.5" HDD MQ04UBD       | 1      | 2       | 169   | 12    | 0.14   |
| Hitachi   | Travelstar 4K40        | 1      | 6       | 456   | 186   | 0.14   |
| Hitachi   | Travelstar 4K120       | 3      | 10      | 620   | 16    | 0.13   |
| Seagate   | SV35.3                 | 2      | 2       | 831   | 12    | 0.13   |
| Samsung   | SpinPoint N2           | 2      | 2       | 46    | 1044  | 0.12   |
| Toshiba   | 2.5" HDD MK..56GSY     | 5      | 14      | 95    | 238   | 0.12   |
| Toshiba   | 2.5" HDD MQ02ABF..H    | 2      | 3       | 43    | 0     | 0.12   |
| IBM/Hi... | Travelstar 60GH and... | 1      | 2       | 134   | 3     | 0.11   |
| Toshiba   | 2.5" HDD MQ02ABF       | 1      | 2       | 39    | 0     | 0.11   |
| WDC       | Internal Use HDD       | 3      | 4       | 38    | 0     | 0.11   |
| Toshiba   | 1.8" HDD MK..29GSG     | 2      | 4       | 361   | 568   | 0.10   |
| Toshiba   | 1.8" HDD               | 4      | 10      | 186   | 148   | 0.10   |
| WDC       | Scorpio EIDE           | 6      | 7       | 302   | 80    | 0.10   |
| Samsung   | SpinPoint M5           | 5      | 87      | 343   | 443   | 0.09   |
| HGST      | Travelstar Z7K500.B    | 1      | 2       | 33    | 0     | 0.09   |
| MicroData | Unknown                | 1      | 1       | 288   | 8     | 0.09   |
| Samsung   | SpinPoint V40+         | 2      | 3       | 1003  | 159   | 0.08   |
| Seagate   | U8                     | 1      | 1       | 754   | 24    | 0.08   |
| Toshiba   | 3.5" HDD N300          | 1      | 3       | 29    | 0     | 0.08   |
| HGST      | Ultrastar DC HC310     | 2      | 2       | 28    | 0     | 0.08   |
| Hitachi   | Travelstar DK23XX/D... | 4      | 5       | 344   | 104   | 0.08   |
| Maxtor    | DiamondMax 22          | 4      | 33      | 839   | 409   | 0.08   |
| Seagate   | Mobile USB Momentus    | 1      | 1       | 24    | 0     | 0.07   |
| MediaMax  | WL250                  | 2      | 3       | 43    | 3     | 0.07   |
| Samsung   | SpinPoint M6           | 3      | 13      | 370   | 515   | 0.07   |
| Toshiba   | 2.5" HDD MK..76GSX     | 5      | 74      | 37    | 250   | 0.06   |
| CLOVER    | Hightech Utania        | 2      | 3       | 19    | 0     | 0.05   |
| IBM       | Travelstar 25GS, 18... | 1      | 1       | 118   | 5     | 0.05   |
| Samsung   | SpinPoint M7U (USB)    | 2      | 2       | 18    | 0     | 0.05   |
| MARSHAL   | Unknown                | 1      | 2       | 323   | 27    | 0.05   |
| Maxtor    | Fireball 3             | 6      | 9       | 47    | 3     | 0.05   |
| Toshiba   | 2.5" HDD MK..65GSX     | 3      | 5       | 254   | 20    | 0.05   |
| Toshiba   | 2.5" HDD MQ01ABB       | 1      | 2       | 91    | 352   | 0.04   |
| Seagate   | Pipeline HD Pro        | 1      | 1       | 1038  | 72    | 0.04   |
| WDC       | Caviar WDxxxBA         | 1      | 1       | 296   | 20    | 0.04   |
| Seagate   | U10                    | 1      | 1       | 380   | 27    | 0.04   |
| Maxtor    | DiamondMax 10 (ATA/... | 19     | 43      | 24    | 98    | 0.04   |
| Seagate   | Pipeline HD 5900.1     | 2      | 4       | 444   | 58    | 0.03   |
| Seagate   | DB35.2                 | 2      | 2       | 1265  | 514   | 0.03   |
| Hitachi   | Travelstar 5K80        | 3      | 3       | 214   | 230   | 0.03   |
| Apple     | HGST Travelstar 5K750  | 2      | 4       | 254   | 59    | 0.03   |
| MediaMax  | WL2000                 | 1      | 1       | 33    | 2     | 0.03   |
| Toshiba   | 2.5" HDD               | 3      | 3       | 301   | 66    | 0.03   |
| Maxtor    | MaXLine III (ATA/13... | 4      | 5       | 14    | 34    | 0.02   |
| LENOVO    | RE                     | 1      | 2       | 7     | 0     | 0.02   |
| Seagate   | Lyrion                 | 1      | 1       | 7     | 0     | 0.02   |
| Maxtor    | DiamondMax Plus 8      | 4      | 18      | 25    | 27    | 0.02   |
| HPE       | Unknown                | 1      | 1       | 6     | 0     | 0.02   |
| Hitachi   | Travelstar E7K100      | 1      | 1       | 4     | 0     | 0.01   |
| Toshiba   | 2.5" HDD MK..59GSX     | 1      | 2       | 117   | 637   | 0.01   |
| Fujitsu   | MHZ BJ                 | 1      | 1       | 4     | 0     | 0.01   |
| Maxtor    | DiamondMax Plus 9      | 11     | 76      | 29    | 176   | 0.01   |
| Maxtor    | Fireball 541DX         | 1      | 6       | 23    | 75    | 0.01   |
| Maxtor    | DiamondMax 16          | 2      | 3       | 37    | 28    | 0.01   |
| Hitachi   | Ultrastar 5K3000       | 1      | 1       | 1045  | 595   | 0.00   |
| Maxtor    | MaXLine Plus II        | 1      | 1       | 43    | 37    | 0.00   |
| Maxtor    | DiamondMax D540X-4D    | 2      | 5       | 17    | 157   | 0.00   |
| HGST      | Unknown                | 1      | 1       | 8     | 10    | 0.00   |
| HP        | 1TB SATA disk GB100... | 1      | 1       | 2402  | 3024  | 0.00   |
| Maxtor    | DiamondMax D540X-4G    | 1      | 2       | 20    | 218   | 0.00   |
| MediaMax  | WL400                  | 1      | 1       | 0     | 0     | 0.00   |
| Seagate   | Ultra Mobile SSHD      | 1      | 1       | 358   | 480   | 0.00   |
| Apple     | Ultrastar A7K2000      | 1      | 1       | 83    | 113   | 0.00   |
| Seagate   | SV35.4                 | 1      | 1       | 685   | 1110  | 0.00   |
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
| HP          | 14     | 21      | 1330  | 164   | 2.13   |
| Quantum     | 6      | 6       | 642   | 1     | 1.63   |
| Apple       | 10     | 46      | 446   | 52    | 1.12   |
| WDC         | 1435   | 10174   | 584   | 43    | 1.12   |
| Hitachi     | 237    | 3029    | 664   | 176   | 1.02   |
| ExcelStor   | 6      | 14      | 685   | 14    | 1.01   |
| Samsung     | 129    | 1771    | 733   | 248   | 0.97   |
| Seagate     | 510    | 10930   | 561   | 210   | 0.88   |
| Fujitsu     | 72     | 311     | 486   | 123   | 0.79   |
| HGST        | 65     | 1183    | 325   | 210   | 0.64   |
| Maxtor      | 94     | 463     | 457   | 256   | 0.54   |
| Toshiba     | 192    | 3014    | 314   | 114   | 0.54   |
| Magnetic... | 4      | 4       | 146   | 0     | 0.40   |
| IBM/Hitachi | 15     | 31      | 521   | 58    | 0.34   |
| MediaMax    | 9      | 10      | 227   | 140   | 0.31   |
| China       | 1      | 1       | 106   | 0     | 0.29   |
| IBM         | 4      | 5       | 857   | 20    | 0.23   |
| MicroData   | 1      | 1       | 288   | 8     | 0.09   |
| CLOVER      | 2      | 3       | 19    | 0     | 0.05   |
| MARSHAL     | 1      | 2       | 323   | 27    | 0.05   |
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
| HPE       | MK0100GCTYU        | 100 GB | 1       | 2360  | 0     | 6.47   |
| Intel     | SSDSC2BB800G4      | 800 GB | 1       | 2052  | 0     | 5.62   |
| Intel     | SSDSC2BB160G4      | 160 GB | 1       | 2027  | 0     | 5.55   |
| OCZ       | VERTEX2 3.5        | 240 GB | 1       | 1798  | 0     | 4.93   |
| Kingston  | SVP100S2512G       | 512 GB | 1       | 1795  | 0     | 4.92   |
| Kingston  | SH100S3120G        | 120 GB | 2       | 1711  | 0     | 4.69   |
| OCZ       | VERTEX3            | 96 GB  | 1       | 1686  | 0     | 4.62   |
| Kingston  | SVP100S296G        | 96 GB  | 2       | 1638  | 0     | 4.49   |
| Crucial   | CT500MX200SSD3     | 500 GB | 1       | 1556  | 0     | 4.26   |
| OCZ       | VERTEX2            | 40 GB  | 2       | 1543  | 0     | 4.23   |
| Corsair   | Force 3 SSD        | 180 GB | 4       | 1926  | 1     | 4.19   |
| Intel     | SSDSC2BA100G3      | 100 GB | 20      | 1604  | 1     | 4.17   |
| Mushkin   | MKNSSDCR240GB      | 240 GB | 1       | 1513  | 0     | 4.15   |
| Samsung   | MZHPV128HDGM-00000 | 128 GB | 1       | 1509  | 0     | 4.14   |
| OCZ       | VERTEX2 3.5        | 90 GB  | 1       | 1507  | 0     | 4.13   |
| SanDisk   | SD7SB6S128G1122    | 128 GB | 1       | 1476  | 0     | 4.04   |
| Intel     | SSDSC2BX200G4      | 200 GB | 1       | 1454  | 0     | 3.98   |
| Samsung   | SSD 840 EVO 120... | 120 GB | 3       | 1450  | 0     | 3.97   |
| Samsung   | MZ7LN512HCHP-00000 | 512 GB | 2       | 1362  | 0     | 3.73   |
| PNY       | CS1311 960GB SSD   | 960 GB | 1       | 1338  | 0     | 3.67   |
| Samsung   | MZ7PD256HAFV-000H7 | 256 GB | 1       | 1261  | 0     | 3.46   |
| Samsung   | MZ7LN256HMJP-00000 | 256 GB | 2       | 1259  | 0     | 3.45   |
| Toshiba   | THNSNJ120PCSZ      | 120 GB | 2       | 1255  | 0     | 3.44   |
| Intel     | SSDSC2BP480G4      | 480 GB | 4       | 1247  | 0     | 3.42   |
| Toshiba   | THNSNJ128GMCU      | 128 GB | 1       | 1245  | 0     | 3.41   |
| Kingston  | SKC300S37A480G     | 480 GB | 1       | 1231  | 0     | 3.37   |
| Toshiba   | THNS064GG2BNAA     | 64 GB  | 2       | 1215  | 0     | 3.33   |
| Corsair   | Force GT           | 180 GB | 3       | 1205  | 0     | 3.30   |
| Intel     | SSDSC2BB240G4      | 240 GB | 3       | 1196  | 0     | 3.28   |
| Toshiba   | THNSFC256GAMJ      | 256 GB | 2       | 1189  | 0     | 3.26   |
| OCZ       | VERTEX2            | 64 GB  | 8       | 1182  | 0     | 3.24   |
| OCZ       | SOLID3             | 64 GB  | 3       | 1345  | 5     | 3.21   |
| Seagate   | ST480HM000-1G5162  | 480 GB | 2       | 1282  | 1     | 3.20   |
| Micron    | MTFDDAK064MAR-1... | 64 GB  | 1       | 1164  | 0     | 3.19   |
| Samsung   | SSD SM871 2.5 7mm  | 256 GB | 1       | 1162  | 0     | 3.18   |
| MyDigi... | SB M2 SSD          | 240 GB | 1       | 1161  | 0     | 3.18   |
| Samsung   | MZ7WD240HCFV-00003 | 240 GB | 1       | 1154  | 0     | 3.16   |
| Toshiba   | THNSNC128GMMJ      | 128 GB | 3       | 1122  | 0     | 3.07   |
| SanDisk   | SD5SG2128G1052E    | 128 GB | 1       | 1121  | 0     | 3.07   |
| Intel     | SSDSC2CW240A3      | 240 GB | 21      | 1118  | 0     | 3.06   |
| Samsung   | SSD PM800 2.5"     | 128 GB | 1       | 1115  | 0     | 3.06   |
| Samsung   | SSD 830 Series     | 512 GB | 3       | 1113  | 0     | 3.05   |
| Samsung   | MZ7PD480HAGM-000DA | 480 GB | 1       | 1092  | 0     | 2.99   |
| Samsung   | SSD 850 PRO        | 1 TB   | 12      | 1088  | 0     | 2.98   |
| Corsair   | Force GS           | 180 GB | 3       | 1087  | 0     | 2.98   |
| Micron    | M500_MTFDDAK480MAV | 480 GB | 1       | 1083  | 0     | 2.97   |
| SanDisk   | SD7SB3Q-256G-1006  | 256 GB | 1       | 1040  | 0     | 2.85   |
| OCZ       | VERTEX2 3.5        | 120 GB | 1       | 1040  | 0     | 2.85   |
| Intel     | SSDSC2BW240A3L     | 240 GB | 2       | 1038  | 0     | 2.85   |
| SanDisk   | SSD U110           | 32 GB  | 1       | 1009  | 0     | 2.76   |
| Samsung   | SSD 830 Series     | 64 GB  | 7       | 997   | 0     | 2.73   |
| OCZ       | VERTEX3 MI         | 240 GB | 1       | 985   | 0     | 2.70   |
| Crucial   | M4-CT256M4SSD1     | 256 GB | 1       | 982   | 0     | 2.69   |
| Samsung   | SMART SSD Xceed... | 32 GB  | 1       | 980   | 0     | 2.69   |
| Samsung   | MZMPC256HBGJ-000H1 | 256 GB | 1       | 980   | 0     | 2.69   |
| Samsung   | SSD 850 EVO        | 2 TB   | 6       | 970   | 0     | 2.66   |
| WDC       | WD1001X06X-00SJVT0 | 1.1 TB | 1       | 969   | 0     | 2.66   |
| OCZ       | AGILITY4           | 128 GB | 4       | 965   | 0     | 2.65   |
| Samsung   | SSD PM830 2.5" 7mm | 256 GB | 5       | 959   | 0     | 2.63   |
| SanDisk   | SD7SB3Q-128G-1006  | 128 GB | 1       | 935   | 0     | 2.56   |
| Intel     | SSDSC2BB480G7      | 480 GB | 2       | 935   | 0     | 2.56   |
| Crucial   | CT120M500SSD3      | 120 GB | 2       | 933   | 8     | 2.54   |
| Kingston  | SE50S3480G         | 480 GB | 10      | 1104  | 1     | 2.54   |
| SK hynix  | SC300 2.5 7MM      | 256 GB | 1       | 923   | 0     | 2.53   |
| Apple     | SSD SM1024F        | 1 TB   | 2       | 921   | 0     | 2.52   |
| Corsair   | Force 3 SSD        | 240 GB | 4       | 920   | 0     | 2.52   |
| Crucial   | M4-CT128M4SSD1     | 128 GB | 4       | 902   | 0     | 2.47   |
| Crucial   | M4-CT128M4SSD2     | 128 GB | 28      | 944   | 145   | 2.45   |
| Samsung   | SSD 840 EVO        | 1 TB   | 12      | 890   | 0     | 2.44   |
| Kingston  | SKC310S37A960G     | 960 GB | 1       | 885   | 0     | 2.43   |
| Intel     | SSDSC2CW180A3      | 180 GB | 10      | 884   | 0     | 2.42   |
| Corsair   | Neutron SSD        | 256 GB | 1       | 879   | 0     | 2.41   |
| Toshiba   | THNSNH256GMCT      | 256 GB | 3       | 875   | 0     | 2.40   |
| Samsung   | SSD PM800 2.5"     | 256 GB | 1       | 871   | 0     | 2.39   |
| Plextor   | PX-128M2S          | 128 GB | 2       | 863   | 0     | 2.37   |
| Samsung   | MZMPC032HBCD-000D1 | 32 GB  | 1       | 840   | 0     | 2.30   |
| Kingston  | RBU-SC100S37256GD  | 256 GB | 1       | 833   | 0     | 2.28   |
| Samsung   | SSD PM800 Serie... | 256 GB | 2       | 825   | 0     | 2.26   |
| Patriot   | Blast              | 480 GB | 1       | 823   | 0     | 2.26   |
| Samsung   | MZ7GE240HMGR-00003 | 240 GB | 1       | 822   | 0     | 2.25   |
| Kingston  | SNVP325S2512GB     | 512 GB | 1       | 822   | 0     | 2.25   |
| ADATA     | XM11 256GB-V2      | 256 GB | 2       | 819   | 0     | 2.25   |
| OCZ       | VERTEX2            | 120 GB | 6       | 810   | 0     | 2.22   |
| SanDisk   | SSD U110           | 128 GB | 1       | 807   | 0     | 2.21   |
| OCZ       | VERTEX PLUS R2     | 64 GB  | 2       | 802   | 0     | 2.20   |
| OCZ       | DENRSTE251M45-0... | 100 GB | 1       | 801   | 0     | 2.20   |
| ADATA     | SSD S599           | 55 GB  | 1       | 801   | 0     | 2.20   |
| Samsung   | SSD 830 Series     | 128 GB | 14      | 798   | 0     | 2.19   |
| OCZ       | VERTEX PLUS R2     | 247 GB | 1       | 797   | 0     | 2.18   |
| Intel     | SSDSA2SH032G1GN    | 32 GB  | 1       | 795   | 0     | 2.18   |
| Samsung   | MZ7KM480HMHQ-00005 | 480 GB | 2       | 794   | 0     | 2.18   |
| Toshiba   | THNSNH060GMCT      | 64 GB  | 1       | 787   | 0     | 2.16   |
| Samsung   | SSD CM871 M.2 2280 | 128 GB | 1       | 785   | 0     | 2.15   |
| Corsair   | Force GS           | 90 GB  | 1       | 776   | 0     | 2.13   |
| Samsung   | SSD SM871 2.5 7mm  | 512 GB | 1       | 773   | 0     | 2.12   |
| Transcend | TS128GSSD340       | 128 GB | 5       | 773   | 0     | 2.12   |
| Lite-On   | ECE-240NAS         | 240 GB | 1       | 766   | 0     | 2.10   |
| Samsung   | MZ7KM480HAHP-00005 | 480 GB | 1       | 765   | 0     | 2.10   |
| Kingston  | SVP200S37A480G     | 480 GB | 1       | 765   | 0     | 2.10   |
| ADATA     | SSD S510           | 120 GB | 6       | 762   | 0     | 2.09   |
| Innodisk  | 2.5" SATA SSD 3ME3 | 64 GB  | 1       | 760   | 0     | 2.08   |
| Samsung   | SSD 850 PRO        | 2 TB   | 1       | 759   | 0     | 2.08   |
| Patriot   | Flare              | 120 GB | 1       | 753   | 0     | 2.06   |
| Samsung   | SSD PM830 2.5" 7mm | 128 GB | 4       | 743   | 0     | 2.04   |
| PNY       | SSD2SC480G1CS27... | 480 GB | 3       | 742   | 0     | 2.03   |
| SanDisk   | SD5SE2128G1002E    | 128 GB | 2       | 729   | 0     | 2.00   |
| Mushkin   | MKNSSDAT60GB-DX    | 64 GB  | 1       | 728   | 0     | 2.00   |
| Samsung   | SSD 840 PRO Series | 512 GB | 10      | 1165  | 12    | 1.99   |
| Micro ... | G2 series          | 64 GB  | 1       | 722   | 0     | 1.98   |
| Samsung   | SSD 840 Series     | 500 GB | 4       | 792   | 1     | 1.98   |
| Crucial   | CT512M550SSD1      | 512 GB | 3       | 828   | 15    | 1.97   |
| Crucial   | M4-CT256M4SSD2     | 256 GB | 12      | 930   | 255   | 1.96   |
| SanDisk   | SD8SBBU480G1122    | 480 GB | 1       | 712   | 0     | 1.95   |
| OCZ       | NOCTI              | 64 GB  | 1       | 704   | 0     | 1.93   |
| Kingston  | SVP100S2128G       | 128 GB | 1       | 698   | 0     | 1.91   |
| Intel     | SSDSC2BP240G4      | 240 GB | 4       | 691   | 0     | 1.89   |
| Kingston  | SVP200S390G        | 90 GB  | 1       | 686   | 0     | 1.88   |
| SK hynix  | HFS512G32MND-3312A | 512 GB | 1       | 686   | 0     | 1.88   |
| Samsung   | MZ7TE512HMHP-000L2 | 512 GB | 3       | 685   | 0     | 1.88   |
| Kingston  | SUV500MS480G       | 480 GB | 1       | 683   | 0     | 1.87   |
| Samsung   | SSD 840 PRO Series | 128 GB | 26      | 776   | 8     | 1.87   |
| Intel     | SSDSC2CT060A3      | 64 GB  | 5       | 676   | 0     | 1.85   |
| Kingston  | SNVP325S2128GB     | 128 GB | 1       | 674   | 0     | 1.85   |
| Mushkin   | MKNSSDCR120GB      | 120 GB | 2       | 1370  | 4     | 1.84   |
| Kingston  | RBU-SNS8152S3128GF | 128 GB | 1       | 665   | 0     | 1.82   |
| Intel     | SSDSC2CT180A3      | 180 GB | 4       | 662   | 0     | 1.82   |
| Samsung   | MZ7TE256HMHP-00000 | 256 GB | 2       | 659   | 0     | 1.81   |
| Apple     | SSD SM0512F        | 500 GB | 3       | 656   | 0     | 1.80   |
| Intel     | SSDSCMMW180A3L     | 180 GB | 2       | 646   | 0     | 1.77   |
| Kingston  | SV200S364G         | 64 GB  | 2       | 645   | 0     | 1.77   |
| Crucial   | M4-CT512M4SSD2     | 512 GB | 4       | 1331  | 253   | 1.77   |
| Toshiba   | THNSFJ256GCSU      | 256 GB | 5       | 642   | 0     | 1.76   |
| OCZ       | VECTOR180          | 240 GB | 2       | 641   | 0     | 1.76   |
| Crucial   | M4-CT064M4SSD2     | 64 GB  | 15      | 805   | 139   | 1.76   |
| Corsair   | Force GT           | 120 GB | 11      | 734   | 1     | 1.74   |
| Apple     | SSD SD512E         | 500 GB | 1       | 636   | 0     | 1.74   |
| Samsung   | MZ7TE128HMGR-000L1 | 128 GB | 3       | 635   | 0     | 1.74   |
| Samsung   | MZ7TD256HAFV-000L7 | 256 GB | 5       | 627   | 0     | 1.72   |
| Kingston  | SVP200S37A240G     | 240 GB | 1       | 623   | 0     | 1.71   |
| Samsung   | MMCQE28G8MUP-0VA   | 128 GB | 1       | 622   | 0     | 1.71   |
| SK hynix  | HFS256G39MND-2300A | 256 GB | 1       | 621   | 0     | 1.70   |
| BLueRay   | SDM9SI128A         | 128 GB | 1       | 619   | 0     | 1.70   |
| Corsair   | Force 3 SSD        | 64 GB  | 11      | 658   | 1     | 1.69   |
| Samsung   | MZMPA128HMFU-00000 | 128 GB | 1       | 616   | 0     | 1.69   |
| SanDisk   | SDSSDHII480G       | 480 GB | 7       | 610   | 0     | 1.67   |
| Samsung   | SSD 840 EVO        | 250 GB | 80      | 615   | 13    | 1.67   |
| SanDisk   | SDSSDP064G         | 64 GB  | 11      | 628   | 93    | 1.66   |
| Samsung   | SSD 840 PRO Series | 256 GB | 38      | 603   | 0     | 1.65   |
| Apple     | SSD SM0256F        | 256 GB | 5       | 600   | 0     | 1.65   |
| Intel     | SSDSC2CT080A4      | 80 GB  | 3       | 600   | 0     | 1.64   |
| Corsair   | Force 3 SSD        | 480 GB | 1       | 598   | 0     | 1.64   |
| Samsung   | SSD 840 EVO        | 500 GB | 21      | 594   | 0     | 1.63   |
| SanDisk   | SD7SN6S512G1001    | 512 GB | 1       | 593   | 0     | 1.63   |
| OCZ       | DENCSTE351M16-0... | 240 GB | 1       | 585   | 0     | 1.60   |
| OCZ       | D2RSTK251E19-0200  | 200 GB | 1       | 584   | 0     | 1.60   |
| OCZ       | VERTEX2            | 115 GB | 1       | 581   | 0     | 1.59   |
| Intel     | SSDSC2BA400G3      | 400 GB | 1       | 580   | 0     | 1.59   |
| Phison    | SATA SSD           | 240 GB | 1       | 579   | 0     | 1.59   |
| SATADOM   | SL 3ME3 V2         | 128 GB | 1       | 574   | 0     | 1.57   |
| Kingston  | SVP200S360G        | 64 GB  | 4       | 572   | 0     | 1.57   |
| OCZ       | AGILITY4           | 64 GB  | 1       | 567   | 0     | 1.56   |
| OCZ       | AGILITY3           | 120 GB | 31      | 651   | 92    | 1.55   |
| Samsung   | MZ7KM480HMHQ0D3    | 480 GB | 6       | 565   | 0     | 1.55   |
| Micron    | MTFDDAK512MBF-1... | 512 GB | 2       | 564   | 0     | 1.55   |
| OCZ       | REVODRIVE3         | 64 GB  | 4       | 564   | 0     | 1.55   |
| Samsung   | SSD 840 EVO        | 120 GB | 66      | 562   | 0     | 1.54   |
| Samsung   | MZMPC128HBFU-000L1 | 128 GB | 1       | 559   | 0     | 1.53   |
| Patriot   | Torch LE           | 240 GB | 1       | 558   | 0     | 1.53   |
| Intel     | SSDSC2BA200G4      | 200 GB | 7       | 636   | 1     | 1.52   |
| Lite-On   | LCS-256L9S-11 2... | 256 GB | 2       | 551   | 0     | 1.51   |
| Toshiba   | THNSNH128GCST      | 128 GB | 1       | 549   | 0     | 1.51   |
| SanDisk   | SD6SB1M256G1002    | 256 GB | 1       | 548   | 0     | 1.50   |
| Kingston  | SMS100S264G        | 64 GB  | 2       | 547   | 0     | 1.50   |
| SK hynix  | HFS512G32MND-3210A | 512 GB | 1       | 547   | 0     | 1.50   |
| SK hynix  | SC300 SATA         | 512 GB | 1       | 546   | 0     | 1.50   |
| Intel     | SSDSC2MH120A2      | 120 GB | 3       | 545   | 0     | 1.49   |
| Plextor   | PX-512M7VC         | 512 GB | 2       | 544   | 0     | 1.49   |
| Corsair   | Force 3 SSD        | 120 GB | 14      | 682   | 78    | 1.49   |
| OCZ       | VERTEX2 3.5        | 115 GB | 1       | 541   | 0     | 1.48   |
| Samsung   | SSD 840 Series     | 250 GB | 17      | 554   | 2     | 1.48   |
| Samsung   | MZHPV512HDGL-00000 | 512 GB | 1       | 536   | 0     | 1.47   |
| Samsung   | SSD 850 EVO M.2    | 120 GB | 3       | 535   | 0     | 1.47   |
| Samsung   | SSD 830 Series     | 256 GB | 11      | 581   | 92    | 1.47   |
| Phison    | SM280128GPTC15T... | 128 GB | 1       | 535   | 0     | 1.47   |
| SanDisk   | SD7TB3Q-256G-1006  | 256 GB | 1       | 533   | 0     | 1.46   |
| HP        | VK000240GWJPD      | 240 GB | 1       | 529   | 0     | 1.45   |
| SK hynix  | SC300 M.2 2280     | 256 GB | 3       | 528   | 0     | 1.45   |
| OCZ       | AGILITY3           | 64 GB  | 34      | 669   | 3     | 1.44   |
| SanDisk   | SD6SP1M128G1002    | 128 GB | 3       | 524   | 0     | 1.44   |
| Samsung   | SSD 840 EVO 250... | 250 GB | 6       | 524   | 0     | 1.44   |
| OCZ       | VERTEX3            | 64 GB  | 26      | 590   | 2     | 1.43   |
| Samsung   | MZ7TE128HMGR-00004 | 128 GB | 3       | 522   | 0     | 1.43   |
| Kingston  | SH100S3240G        | 240 GB | 2       | 1170  | 2     | 1.42   |
| SanDisk   | SD8SB8U256G1122    | 256 GB | 4       | 518   | 0     | 1.42   |
| Samsung   | SSD 850 PRO        | 512 GB | 30      | 542   | 35    | 1.41   |
| SanDisk   | SD7UB2Q512G1122    | 512 GB | 2       | 514   | 0     | 1.41   |
| Micron    | C400-MTFDDAK256MAM | 256 GB | 2       | 513   | 0     | 1.41   |
| Kingston  | SEDC400S37960G     | 960 GB | 1       | 513   | 0     | 1.41   |
| OCZ       | VERTEX4            | 256 GB | 18      | 713   | 2     | 1.40   |
| Toshiba   | THNSNH128GBST      | 128 GB | 3       | 510   | 0     | 1.40   |
| Toshiba   | TL100              | 120 GB | 1       | 509   | 0     | 1.40   |
| Micron    | M600_MTFDDAV256MBF | 256 GB | 3       | 507   | 0     | 1.39   |
| Samsung   | MZ7PA128HMCD-010L1 | 128 GB | 1       | 504   | 0     | 1.38   |
| SanDisk   | SDSSDHP256G        | 256 GB | 11      | 503   | 0     | 1.38   |
| OCZ       | D2RSTK251E14-0400  | 400 GB | 1       | 502   | 0     | 1.38   |
| Crucial   | CT1050MX300SSD1    | 1 TB   | 10      | 607   | 1     | 1.37   |
| Corsair   | Force GT           | 90 GB  | 4       | 610   | 1     | 1.36   |
| OCZ       | VERTEX460A         | 240 GB | 3       | 494   | 0     | 1.35   |
| Transcend | TS128GSSD320       | 128 GB | 1       | 493   | 0     | 1.35   |
| Toshiba   | VT180              | 480 GB | 2       | 492   | 0     | 1.35   |
| Kingston  | SKC400S37512G      | 512 GB | 2       | 492   | 0     | 1.35   |
| Crucial   | CT250MX200SSD3     | 250 GB | 2       | 484   | 0     | 1.33   |
| SPCC      | SSD110             | 120 GB | 5       | 572   | 204   | 1.33   |
| Crucial   | CT512MX100SSD1     | 512 GB | 12      | 575   | 1     | 1.32   |
| SPCC      | SSD110             | 64 GB  | 4       | 482   | 0     | 1.32   |
| Intel     | SSDSC2CT120A3      | 120 GB | 14      | 828   | 1     | 1.32   |
| Intel     | SSDSA2CW080G3      | 80 GB  | 5       | 478   | 0     | 1.31   |
| Toshiba   | Q300 Pro           | 256 GB | 2       | 478   | 0     | 1.31   |
| Toshiba   | THNSFJ256GDNU A    | 256 GB | 2       | 476   | 0     | 1.30   |
| SanDisk   | SD8SBBU240G1122    | 240 GB | 2       | 474   | 0     | 1.30   |
| Samsung   | MZMTD512HAGL-000MV | 512 GB | 1       | 473   | 0     | 1.30   |
| Samsung   | SSD 850 EVO        | 4 TB   | 1       | 473   | 0     | 1.30   |
| SanDisk   | SDSSDH240GG25      | 240 GB | 1       | 473   | 0     | 1.30   |
| Toshiba   | THNSNF128GMCS      | 128 GB | 2       | 471   | 0     | 1.29   |
| Verbatim  | SATA-III SSD       | 128 GB | 1       | 470   | 0     | 1.29   |
| Kingston  | SVP200S37A60G      | 64 GB  | 9       | 470   | 0     | 1.29   |
| KingSpec  | SPK-SF12-M120      | 120 GB | 1       | 468   | 0     | 1.28   |
| Toshiba   | THNSNH060GCST      | 64 GB  | 1       | 467   | 0     | 1.28   |
| Plextor   | PX-64M2S           | 64 GB  | 2       | 467   | 0     | 1.28   |
| Mushkin   | MKNSSDTR128GB-3DL  | 128 GB | 1       | 464   | 0     | 1.27   |
| SanDisk   | SD7SN6S-256G-1006  | 256 GB | 1       | 463   | 0     | 1.27   |
| ADATA     | SSD S396           | 32 GB  | 1       | 462   | 0     | 1.27   |
| Plextor   | PX-128M3           | 128 GB | 3       | 462   | 0     | 1.27   |
| Samsung   | MZYTY256HDHP-000L2 | 256 GB | 2       | 461   | 0     | 1.26   |
| Toshiba   | THNSNH512GCST      | 512 GB | 1       | 461   | 0     | 1.26   |
| WDC       | WDBNCE2500PNC-WRSN | 250 GB | 1       | 457   | 0     | 1.25   |
| Samsung   | MZ7LF128HCHP-00004 | 128 GB | 2       | 457   | 0     | 1.25   |
| OCZ       | VERTEX4            | 128 GB | 62      | 495   | 1     | 1.25   |
| OCZ       | VERTEX3            | 120 GB | 51      | 685   | 47    | 1.25   |
| Intel     | SSDSA2M040G2GC     | 40 GB  | 3       | 758   | 3     | 1.25   |
| Intel     | SSDSC2CW480A3      | 480 GB | 3       | 455   | 0     | 1.25   |
| HP        | SSD S700           | 120 GB | 2       | 448   | 0     | 1.23   |
| Samsung   | SSD 850 EVO        | 1 TB   | 44      | 505   | 1     | 1.22   |
| Crucial   | CT240M500SSD3      | 240 GB | 4       | 522   | 8     | 1.22   |
| Foxline   | FLDMMS128G         | 128 GB | 1       | 443   | 0     | 1.22   |
| OCZ       | VERTEX2            | 80 GB  | 1       | 442   | 0     | 1.21   |
| Corsair   | Force GT           | 64 GB  | 5       | 690   | 7     | 1.21   |
| Samsung   | SSD 850 PRO        | 128 GB | 25      | 439   | 0     | 1.20   |
| Kingston  | SVP200S37A120G     | 120 GB | 7       | 502   | 154   | 1.20   |
| OCZ       | REVODRIVE X2       | 25 GB  | 4       | 435   | 0     | 1.19   |
| SanDisk   | SD8SN8U256G1122    | 256 GB | 1       | 434   | 0     | 1.19   |
| Phison    | SSDS30256XQC800... | 240 GB | 1       | 433   | 0     | 1.19   |
| Samsung   | MZ7TD128HAFV-000L1 | 128 GB | 9       | 432   | 0     | 1.19   |
| ADATA     | SSD S511           | 120 GB | 1       | 430   | 0     | 1.18   |
| WDC       | WDS200T2B0A-00SM50 | 2 TB   | 1       | 430   | 0     | 1.18   |
| Intel     | SSDSC2BW180A3L     | 180 GB | 7       | 446   | 1     | 1.18   |
| Samsung   | MZMPC032HBCD-00000 | 32 GB  | 6       | 427   | 0     | 1.17   |
| Intel     | SSDSA2CW120G3      | 120 GB | 7       | 425   | 0     | 1.17   |
| Samsung   | MZ7LN256HCHP-000F0 | 256 GB | 1       | 425   | 0     | 1.16   |
| SanDisk   | SD6SB2M-512G-1006  | 512 GB | 3       | 423   | 0     | 1.16   |
| SanDisk   | SDSSDX240GG25      | 240 GB | 3       | 927   | 4     | 1.16   |
| Kingston  | SH103S3120G        | 120 GB | 45      | 430   | 1     | 1.16   |
| Toshiba   | THNSNJ256GCST      | 256 GB | 1       | 421   | 0     | 1.15   |
| Kingston  | SKC380S360G        | 64 GB  | 1       | 420   | 0     | 1.15   |
| Kingston  | SMS200S3240G       | 240 GB | 1       | 419   | 0     | 1.15   |
| OCZ       | SOLID3             | 120 GB | 1       | 418   | 0     | 1.15   |
| PNY       | SSD2SC480G1CS27... | 480 GB | 1       | 415   | 0     | 1.14   |
| Kingston  | SUV400S37960G      | 960 GB | 1       | 415   | 0     | 1.14   |
| Intel     | SSDMAEMC040G2      | 40 GB  | 1       | 414   | 0     | 1.13   |
| Samsung   | MZ7LN128HCHP-000L1 | 128 GB | 2       | 413   | 0     | 1.13   |
| SanDisk   | SD6SB2M128G1022I   | 128 GB | 1       | 412   | 0     | 1.13   |
| Toshiba   | Q300 Pro           | 512 GB | 1       | 411   | 0     | 1.13   |
| Samsung   | MZNLN256HMHQ-00000 | 256 GB | 4       | 411   | 0     | 1.13   |
| Kingston  | SM2280S3240G       | 240 GB | 2       | 410   | 0     | 1.13   |
| Samsung   | MMCRE28G5MXP-0VBH1 | 128 GB | 1       | 410   | 0     | 1.12   |
| Samsung   | MZYTN512HDJH-000L2 | 512 GB | 1       | 410   | 0     | 1.12   |
| SanDisk   | SD8TB8U256G1001    | 256 GB | 3       | 409   | 0     | 1.12   |
| OCZ       | AGILITY3           | 240 GB | 6       | 618   | 1     | 1.12   |
| Samsung   | SSD 850 PRO        | 256 GB | 70      | 420   | 1     | 1.11   |
| SanDisk   | SDSSDH2256G        | 256 GB | 1       | 403   | 0     | 1.10   |
| OCZ       | VERTEX3            | 128 GB | 2       | 402   | 0     | 1.10   |
| SanDisk   | SDSSDA960G         | 960 GB | 3       | 402   | 0     | 1.10   |
| Toshiba   | THNSNJ256GCSU      | 256 GB | 5       | 400   | 0     | 1.10   |
| Toshiba   | THNSNH060GBST      | 64 GB  | 2       | 400   | 0     | 1.10   |
| Samsung   | SSD 840 EVO        | 752 GB | 2       | 399   | 0     | 1.09   |
| Kingston  | SH103S3240G        | 240 GB | 16      | 536   | 136   | 1.09   |
| Samsung   | MZNLN128HCGR-00000 | 128 GB | 1       | 396   | 0     | 1.09   |
| Crucial   | CT256MX100SSD1     | 256 GB | 26      | 438   | 19    | 1.08   |
| Micron    | MTFDDAT128MAM-1J2  | 128 GB | 2       | 450   | 548   | 1.07   |
| Apple     | SSD TS256C         | 256 GB | 3       | 391   | 0     | 1.07   |
| Kingston  | SV100S232G         | 32 GB  | 4       | 390   | 0     | 1.07   |
| Kingston  | SUV300S37A480G     | 480 GB | 2       | 389   | 0     | 1.07   |
| Samsung   | SSD PM830 mSATA    | 32 GB  | 7       | 389   | 0     | 1.07   |
| OCZ       | AGILITY3           | 128 GB | 3       | 749   | 1     | 1.07   |
| Smartbuy  | SSD                | 64 GB  | 6       | 386   | 0     | 1.06   |
| Samsung   | MZ7TD256HAFV-000L9 | 256 GB | 1       | 385   | 0     | 1.06   |
| ADATA     | SP600              | 256 GB | 3       | 384   | 0     | 1.05   |
| SanDisk   | SDSSDP256G         | 256 GB | 5       | 384   | 0     | 1.05   |
| Lite-On   | LAT-128M2S         | 128 GB | 1       | 384   | 0     | 1.05   |
| Samsung   | MMCRE28GFMXP-MVB   | 128 GB | 2       | 383   | 0     | 1.05   |
| Samsung   | MZ7TE128HMGR-00000 | 128 GB | 2       | 382   | 0     | 1.05   |
| Samsung   | MZ7PD128HCFV-000H1 | 128 GB | 2       | 381   | 0     | 1.04   |
| Kingston  | SM2280S3G2240G     | 240 GB | 2       | 380   | 0     | 1.04   |
| Samsung   | SATA SSD           | 256 GB | 1       | 379   | 0     | 1.04   |
| SanDisk   | SDSSDXP240G        | 240 GB | 4       | 379   | 0     | 1.04   |
| Corsair   | Force 3 SSD        | 90 GB  | 5       | 378   | 0     | 1.04   |
| Crucial   | CT500MX200SSD1     | 500 GB | 10      | 375   | 0     | 1.03   |
| Crucial   | CT120M500SSD1      | 120 GB | 12      | 527   | 6     | 1.02   |
| Samsung   | MZNTE256HMHP-000H1 | 256 GB | 1       | 373   | 0     | 1.02   |
| Intel     | SSDSA2M080G2GC     | 80 GB  | 14      | 908   | 5     | 1.02   |
| Kingston  | SV200S3128G        | 128 GB | 7       | 372   | 0     | 1.02   |
| Samsung   | SSD 850 EVO        | 120 GB | 56      | 370   | 0     | 1.02   |
| Samsung   | MZ7LN256HMJP-000H1 | 256 GB | 3       | 369   | 0     | 1.01   |
| SanDisk   | SDSSDHP128G        | 128 GB | 24      | 379   | 1     | 1.01   |
| Intel     | SSDSC2BW240A3H     | 240 GB | 1       | 369   | 0     | 1.01   |
| Toshiba   | THNS064GE4BBDC     | 64 GB  | 2       | 369   | 0     | 1.01   |
| OCZ       | VERTEX3 MI         | 120 GB | 16      | 526   | 126   | 1.01   |
| Toshiba   | THNSNC128GCSJ      | 128 GB | 1       | 367   | 0     | 1.01   |
| WDC       | WDS500G1B0B-00AS40 | 500 GB | 4       | 365   | 0     | 1.00   |
| Plextor   | PX-64M3            | 64 GB  | 3       | 668   | 346   | 1.00   |
| Crucial   | CT128M550SSD3      | 128 GB | 4       | 469   | 8     | 1.00   |
| Samsung   | SSD 850 EVO        | 500 GB | 158     | 364   | 0     | 1.00   |
| Samsung   | MZMPC128HBFU-000H1 | 128 GB | 1       | 363   | 0     | 1.00   |
| OCZ       | VERTEX3            | 90 GB  | 11      | 680   | 7     | 0.99   |
| Micron    | 5200_MTFDDAK240TDN | 240 GB | 10      | 362   | 0     | 0.99   |
| SanDisk   | Ultra II           | 960 GB | 7       | 442   | 1     | 0.99   |
| Samsung   | SSD 850 EVO        | 250 GB | 213     | 360   | 0     | 0.99   |
| KingShare | 230120SSD          | 128 GB | 1       | 358   | 0     | 0.98   |
| Plextor   | PX-256M5Pro        | 256 GB | 6       | 357   | 0     | 0.98   |
| ZTC       | SM201-256G         | 256 GB | 1       | 357   | 0     | 0.98   |
| SanDisk   | SDSSDH2128G        | 128 GB | 1       | 356   | 0     | 0.98   |
| KingSpec  | KSD-SA25.5-016MJ   | 16 GB  | 1       | 353   | 0     | 0.97   |
| Kingston  | RBU-SC100S37128GD  | 128 GB | 2       | 351   | 0     | 0.96   |
| ADATA     | SX900              | 128 GB | 9       | 759   | 454   | 0.96   |
| Goodram   | C40                | 120 GB | 3       | 351   | 0     | 0.96   |
| KingDian  | N480-240GB         | 240 GB | 1       | 351   | 0     | 0.96   |
| Samsung   | MZMTE256HMHP-00000 | 256 GB | 1       | 349   | 0     | 0.96   |
| Crucial   | CT128M550SSD4      | 128 GB | 1       | 349   | 0     | 0.96   |
| SanDisk   | SDSSDXPS480G       | 480 GB | 4       | 583   | 113   | 0.96   |
| OCZ       | VERTEX             | 32 GB  | 1       | 696   | 1     | 0.95   |
| Intel     | SSDMCEAW120A4      | 120 GB | 1       | 347   | 0     | 0.95   |
| ADATA     | SP600              | 128 GB | 5       | 347   | 0     | 0.95   |
| Intel     | SSDSC2CT240A3      | 240 GB | 3       | 622   | 1     | 0.95   |
| Toshiba   | THNSNX024GMNT      | 24 GB  | 2       | 346   | 0     | 0.95   |
| SanDisk   | SDSSDHII240G       | 240 GB | 15      | 345   | 0     | 0.95   |
| Advantech | SQF-S25M4-32G-S9E  | 32 GB  | 1       | 345   | 0     | 0.95   |
| Crucial   | CT750MX300SSD1     | 752 GB | 7       | 345   | 0     | 0.95   |
| Intel     | SSDSC2BA400G4      | 400 GB | 3       | 344   | 0     | 0.94   |
| SanDisk   | SD6SF1M128G1022I   | 128 GB | 2       | 446   | 1     | 0.94   |
| Samsung   | SSD 840 Series     | 120 GB | 20      | 351   | 1     | 0.94   |
| OCZ       | VERTEX3            | 240 GB | 8       | 564   | 160   | 0.94   |
| Crucial   | CT275MX300SSD1     | 275 GB | 27      | 359   | 4     | 0.94   |
| Crucial   | CT240M500SSD1      | 240 GB | 20      | 572   | 113   | 0.94   |
| Intel     | SSDSCKJW120H6      | 120 GB | 1       | 339   | 0     | 0.93   |
| SanDisk   | X400 2.5 7MM       | 256 GB | 2       | 339   | 0     | 0.93   |
| Samsung   | MZMTE512HMHP-000L1 | 512 GB | 1       | 338   | 0     | 0.93   |
| SanDisk   | SSD i100           | 16 GB  | 6       | 338   | 0     | 0.93   |
| Intel     | SSDSC2BW240A4      | 240 GB | 15      | 337   | 0     | 0.92   |
| Samsung   | MZ7PC128HAFU-000   | 128 GB | 2       | 337   | 0     | 0.92   |
| OCZ       | VERTEX4            | 64 GB  | 7       | 338   | 1     | 0.92   |
| Team      | TEAML5Lite3D120G   | 120 GB | 3       | 334   | 0     | 0.92   |
| SK hynix  | SC300 M.2 2280     | 512 GB | 1       | 333   | 0     | 0.91   |
| KingFast  | SSD                | 32 GB  | 1       | 332   | 0     | 0.91   |
| Team      | L3 SSD             | 120 GB | 3       | 331   | 0     | 0.91   |
| OCZ       | VERTEX PLUS R2     | 128 GB | 2       | 331   | 0     | 0.91   |
| Crucial   | C300-CTFDDAC128MAG | 128 GB | 3       | 330   | 0     | 0.91   |
| ZOTAC     | ZTSSD-S11-240G-P   | 240 GB | 1       | 328   | 0     | 0.90   |
| Kingston  | SV300S37A60G       | 64 GB  | 112     | 339   | 1     | 0.90   |
| Mushkin   | MKNSSDCR240GB-7    | 240 GB | 1       | 326   | 0     | 0.89   |
| OCZ       | VERTEX             | 64 GB  | 2       | 324   | 0     | 0.89   |
| Apple     | SSD TS128C         | 121 GB | 2       | 323   | 0     | 0.89   |
| WDC       | WDS250G1B0A-00H9H0 | 250 GB | 9       | 322   | 0     | 0.88   |
| Intel     | SSDSC2CT240A4      | 240 GB | 5       | 321   | 0     | 0.88   |
| Patriot   | Blast              | 240 GB | 5       | 321   | 0     | 0.88   |
| OCZ       | VERTEX3 LP         | 64 GB  | 1       | 320   | 0     | 0.88   |
| Crucial   | CT275MX300SSD4     | 275 GB | 3       | 319   | 0     | 0.87   |
| Samsung   | MZNLF128HCHP-00000 | 128 GB | 3       | 319   | 0     | 0.87   |
| SanDisk   | SDSSDHP064G        | 64 GB  | 8       | 318   | 0     | 0.87   |
| Samsung   | SSD 850 EVO mSATA  | 1 TB   | 2       | 317   | 0     | 0.87   |
| SanDisk   | SSD i110           | 64 GB  | 1       | 317   | 0     | 0.87   |
| PNY       | SSD2SC240G1CS17... | 240 GB | 1       | 317   | 0     | 0.87   |
| PNY       | CS1311 240GB SSD   | 240 GB | 3       | 316   | 0     | 0.87   |
| Micron    | 1100_MTFDDAK512TBN | 512 GB | 3       | 551   | 8     | 0.86   |
| Samsung   | SSD 850 EVO mSATA  | 120 GB | 3       | 311   | 0     | 0.85   |
| Toshiba   | TR150              | 120 GB | 4       | 311   | 0     | 0.85   |
| Toshiba   | THNSNX032GMCT      | 32 GB  | 1       | 311   | 0     | 0.85   |
| Samsung   | SSD 750 EVO        | 250 GB | 31      | 309   | 0     | 0.85   |
| Apple     | SSD SM0256G        | 256 GB | 5       | 309   | 0     | 0.85   |
| Samsung   | MZ7TE256HMHP-000L7 | 256 GB | 3       | 308   | 0     | 0.85   |
| Samsung   | MZNLN512HCJH-000L1 | 512 GB | 1       | 307   | 0     | 0.84   |
| Crucial   | C300-CTFDDAC064MAG | 64 GB  | 1       | 307   | 0     | 0.84   |
| Kingston  | SVP200S3240G       | 240 GB | 2       | 307   | 0     | 0.84   |
| SanDisk   | SD8SB8U512G1122    | 512 GB | 3       | 305   | 0     | 0.84   |
| Toshiba   | THNSNC128GBSJ      | 128 GB | 1       | 303   | 0     | 0.83   |
| Samsung   | SSD 850 EVO M.2    | 500 GB | 13      | 303   | 0     | 0.83   |
| OCZ       | AGILITY2           | 64 GB  | 2       | 302   | 0     | 0.83   |
| Kingston  | SNV425S264GB       | 64 GB  | 2       | 1165  | 4     | 0.83   |
| Samsung   | MZ7TD128HAFV-00000 | 128 GB | 1       | 300   | 0     | 0.82   |
| Samsung   | MZMTD128HAFV-000L1 | 128 GB | 8       | 322   | 18    | 0.82   |
| Samsung   | SSD PM810 2.5" 7mm | 128 GB | 1       | 300   | 0     | 0.82   |
| Mushkin   | MKNSSDAT240GB-DX   | 240 GB | 1       | 299   | 0     | 0.82   |
| Crucial   | CT960M500SSD1      | 960 GB | 7       | 526   | 298   | 0.82   |
| ADATA     | SP600              | 32 GB  | 7       | 298   | 0     | 0.82   |
| Samsung   | MZMPC032HBCD-000H1 | 32 GB  | 6       | 297   | 0     | 0.82   |
| Intel     | SSDSC2KB240G8      | 240 GB | 4       | 297   | 0     | 0.81   |
| OCZ       | VECTOR150          | 240 GB | 5       | 297   | 0     | 0.81   |
| SanDisk   | SSD U100           | 128 GB | 6       | 390   | 33    | 0.81   |
| SanDisk   | X300 2.5 7MM       | 256 GB | 1       | 297   | 0     | 0.81   |
| Apple     | SSD SM0512G        | 500 GB | 2       | 296   | 0     | 0.81   |
| ADATA     | SSD S599           | 64 GB  | 2       | 296   | 0     | 0.81   |
| Ramaxel   | RDM-II XM020C024G  | 24 GB  | 2       | 295   | 0     | 0.81   |
| Kingston  | SMS200S360G        | 64 GB  | 10      | 364   | 1     | 0.81   |
| SanDisk   | SDSSDX120GG25      | 120 GB | 6       | 293   | 0     | 0.80   |
| Kingston  | SNVP325S2256GB     | 256 GB | 1       | 293   | 0     | 0.80   |
| Micron    | MTFDDAK128MAM-1J1  | 128 GB | 3       | 292   | 0     | 0.80   |
| PHISON    | 128GB PS3110-S10C  | 128 GB | 1       | 291   | 0     | 0.80   |
| e2e4      | SSD                | 240 GB | 1       | 291   | 0     | 0.80   |
| Apple     | SSD SD128E         | 121 GB | 1       | 290   | 0     | 0.80   |
| Samsung   | MZMPA064HMDR-00000 | 64 GB  | 1       | 290   | 0     | 0.79   |
| ADATA     | SP900              | 256 GB | 11      | 382   | 2     | 0.79   |
| OCZ       | AGILITY3           | 90 GB  | 3       | 476   | 1     | 0.79   |
| Samsung   | MZ7LN512HAJQ-00000 | 512 GB | 2       | 287   | 0     | 0.79   |
| Samsung   | SSD PM830 2.5" 7mm | 512 GB | 2       | 594   | 505   | 0.79   |
| OCZ       | CACHE-SYNAPSE      | 32 GB  | 1       | 286   | 0     | 0.79   |
| Intel     | SSDSC2KB480G8      | 480 GB | 1       | 285   | 0     | 0.78   |
| SanDisk   | X400 M.2 2280      | 256 GB | 8       | 284   | 0     | 0.78   |
| Corsair   | CMFSSD-32D1        | 32 GB  | 1       | 566   | 1     | 0.78   |
| China     | SATA SSD           | 20 GB  | 9       | 317   | 1     | 0.77   |
| SanDisk   | SDSSDH31024G       | 1 TB   | 3       | 280   | 0     | 0.77   |
| SanDisk   | Ultra II           | 480 GB | 8       | 280   | 0     | 0.77   |
| Kingston  | SMS100S232G        | 32 GB  | 1       | 279   | 0     | 0.76   |
| SanDisk   | SD5SG2256G1052E    | 256 GB | 4       | 445   | 1     | 0.76   |
| PNY       | CS2211 480GB SSD   | 480 GB | 1       | 277   | 0     | 0.76   |
| SanDisk   | SDSSDXPS960G       | 960 GB | 2       | 282   | 20    | 0.76   |
| Toshiba   | THNSNJ128G8NU      | 128 GB | 2       | 274   | 0     | 0.75   |
| Samsung   | MZ7WD960HMHP-00003 | 960 GB | 5       | 610   | 4     | 0.75   |
| ADATA     | SP600NS34          | 256 GB | 1       | 274   | 0     | 0.75   |
| Samsung   | MZYTY128HDHP-000L2 | 128 GB | 2       | 273   | 0     | 0.75   |
| Corsair   | Force GT           | 240 GB | 1       | 819   | 2     | 0.75   |
| Samsung   | SSD 750 EVO        | 500 GB | 6       | 272   | 0     | 0.75   |
| SanDisk   | SD6SB1M128G1001    | 128 GB | 1       | 271   | 0     | 0.74   |
| MyDigi... | SC2 M2 SSD         | 120 GB | 1       | 271   | 0     | 0.74   |
| Plextor   | PX-128M6G-2242     | 128 GB | 1       | 271   | 0     | 0.74   |
| Samsung   | MZMTD256HAGM-000L1 | 256 GB | 3       | 270   | 0     | 0.74   |
| Crucial   | CT250MX200SSD1     | 250 GB | 9       | 269   | 0     | 0.74   |
| Samsung   | SSD 840 EVO 500... | 500 GB | 3       | 268   | 0     | 0.74   |
| Samsung   | MZNLN128HCGR-000L2 | 128 GB | 2       | 267   | 0     | 0.73   |
| Patriot   | Spark              | 128 GB | 7       | 267   | 0     | 0.73   |
| Samsung   | MZNTD256HAGL-000L9 | 256 GB | 1       | 266   | 0     | 0.73   |
| China     | SATA SSD           | 1 TB   | 1       | 265   | 0     | 0.73   |
| SK hynix  | HFS120G32TND-N1A2A | 120 GB | 1       | 264   | 0     | 0.73   |
| Kingston  | SKC400S37128G      | 128 GB | 2       | 264   | 0     | 0.72   |
| SanDisk   | SD7SN6S-512G-1006  | 512 GB | 1       | 263   | 0     | 0.72   |
| Team      | L5 LITE SSD        | 120 GB | 3       | 263   | 0     | 0.72   |
| OCZ       | ARC100             | 120 GB | 11      | 263   | 0     | 0.72   |
| SPCC      | SSD                | 2 TB   | 1       | 263   | 0     | 0.72   |
| Apacer    | A7202              | 64 GB  | 1       | 262   | 0     | 0.72   |
| Samsung   | SSD PM830 mSATA    | 128 GB | 1       | 261   | 0     | 0.72   |
| ADATA     | SP900              | 128 GB | 30      | 336   | 12    | 0.72   |
| Samsung   | MZ7TE256HMHP-000L2 | 256 GB | 1       | 260   | 0     | 0.71   |
| Apple     | SSD SM128C         | 121 GB | 1       | 518   | 1     | 0.71   |
| OCZ       | ARC100             | 480 GB | 3       | 260   | 1     | 0.71   |
| Intenso   | SSD                | 128 GB | 6       | 313   | 1     | 0.71   |
| Goodram   | C50                | 64 GB  | 2       | 258   | 0     | 0.71   |
| Samsung   | SSD 850 EVO mSATA  | 250 GB | 6       | 258   | 0     | 0.71   |
| Intel     | SSDSC2BW240H6      | 240 GB | 9       | 303   | 1     | 0.71   |
| Samsung   | SSD PM810 TM       | 64 GB  | 1       | 257   | 0     | 0.70   |
| Intel     | SSDSCMMW240A3L     | 240 GB | 1       | 256   | 0     | 0.70   |
| SanDisk   | SD6SB1M128G        | 128 GB | 1       | 256   | 0     | 0.70   |
| Corsair   | Force GS           | 240 GB | 3       | 1272  | 6     | 0.70   |
| Corsair   | Force GS           | 128 GB | 14      | 256   | 0     | 0.70   |
| Crucial   | CT500MX200SSD4     | 500 GB | 2       | 255   | 0     | 0.70   |
| Kingston  | SV300S37A120G      | 120 GB | 324     | 305   | 19    | 0.70   |
| Samsung   | MZNLN256HCHP-000L7 | 256 GB | 5       | 253   | 0     | 0.70   |
| MyDigi... | SB2                | 128 GB | 1       | 252   | 0     | 0.69   |
| OCZ       | VECTOR150          | 120 GB | 10      | 251   | 0     | 0.69   |
| Intel     | SSDSC2BW180A4      | 180 GB | 9       | 486   | 3     | 0.69   |
| Samsung   | SSD PM800 TH       | 64 GB  | 1       | 251   | 0     | 0.69   |
| SanDisk   | SD7SB6S256G1122    | 256 GB | 2       | 251   | 0     | 0.69   |
| Intel     | SSDSA2BW160G3L     | 160 GB | 4       | 250   | 0     | 0.69   |
| Samsung   | SSD 850 EVO mSATA  | 500 GB | 5       | 250   | 0     | 0.69   |
| Kingston  | RBUSC180DS37128GH  | 128 GB | 1       | 250   | 0     | 0.69   |
| Intel     | SSDSCKHF240A4L     | 240 GB | 2       | 306   | 554   | 0.68   |
| Kingston  | SS200S330G         | 32 GB  | 2       | 249   | 0     | 0.68   |
| Kingston  | SHPM2280P2H-480G   | 480 GB | 3       | 288   | 1     | 0.68   |
| Samsung   | MZMPA024HMCD-000L1 | 24 GB  | 3       | 284   | 7     | 0.68   |
| Apacer    | AST680S            | 128 GB | 2       | 248   | 0     | 0.68   |
| SanDisk   | SDSSDXPS240G       | 240 GB | 5       | 254   | 207   | 0.68   |
| Intel     | SSDSA2M080G2HP     | 80 GB  | 1       | 245   | 0     | 0.67   |
| Plextor   | PX-128M7VC         | 128 GB | 5       | 245   | 0     | 0.67   |
| Intel     | SSDSA1MH080G1GN    | 80 GB  | 1       | 244   | 0     | 0.67   |
| Hypertec  | SSD2S240SF1200SA2  | 240 GB | 1       | 243   | 0     | 0.67   |
| Corsair   | CSSD-V64GB2        | 64 GB  | 1       | 243   | 0     | 0.67   |
| Samsung   | MZNLN512HMJP-000L7 | 512 GB | 3       | 242   | 0     | 0.67   |
| OCZ       | VECTOR             | 128 GB | 4       | 245   | 4     | 0.67   |
| Kingston  | SA400S37 120G      | 120 GB | 1       | 242   | 0     | 0.66   |
| Plextor   | PX-256M5M          | 256 GB | 2       | 242   | 0     | 0.66   |
| Palit     | PSP120 SSD         | 120 GB | 1       | 242   | 0     | 0.66   |
| Intel     | SSDSC2CW120A3      | 120 GB | 28      | 462   | 327   | 0.66   |
| Kingston  | RBUSNS8180S3128GI  | 128 GB | 1       | 241   | 0     | 0.66   |
| Toshiba   | TR150              | 240 GB | 13      | 240   | 0     | 0.66   |
| SanDisk   | SD8SBBU120G1122    | 120 GB | 2       | 239   | 0     | 0.66   |
| HP        | VK0240GDJXU        | 240 GB | 1       | 238   | 0     | 0.65   |
| Plextor   | PX-512M5P          | 512 GB | 1       | 238   | 0     | 0.65   |
| Crucial   | M4-CT128M4SSD3     | 128 GB | 1       | 238   | 0     | 0.65   |
| Samsung   | MZ7LN256HAJQ-000H1 | 256 GB | 1       | 235   | 0     | 0.65   |
| Kingston  | SKC300S37A120G     | 120 GB | 16      | 236   | 1     | 0.64   |
| Kingston  | SHSS37A120G        | 120 GB | 8       | 234   | 0     | 0.64   |
| Intel     | SSDSA2CT040G3      | 40 GB  | 4       | 232   | 0     | 0.64   |
| SanDisk   | SDSSDP128G         | 128 GB | 27      | 247   | 11    | 0.64   |
| Samsung   | MZ7TY256HDHP-000L7 | 256 GB | 4       | 232   | 0     | 0.64   |
| Intel     | SSDSA2M120G2GC     | 120 GB | 2       | 1424  | 6     | 0.64   |
| Toshiba   | Q300               | 480 GB | 3       | 231   | 0     | 0.63   |
| Patriot   | Blaze              | 240 GB | 2       | 231   | 0     | 0.63   |
| Kingston  | SHSS37A240G        | 240 GB | 16      | 231   | 0     | 0.63   |
| Kingston  | SM2280S3120G       | 120 GB | 3       | 230   | 0     | 0.63   |
| SK hynix  | SH920 2.5 7MM      | 256 GB | 2       | 1001  | 10    | 0.63   |
| Samsung   | MZYLF128HCHP-000L2 | 128 GB | 2       | 230   | 0     | 0.63   |
| SanDisk   | Z400s M.2 2280     | 256 GB | 1       | 229   | 0     | 0.63   |
| SK hynix  | SC210 mSATA        | 128 GB | 3       | 307   | 21    | 0.63   |
| Kingston  | SV100S264G         | 64 GB  | 6       | 391   | 4     | 0.63   |
| Kingston  | SV300S37A240G      | 240 GB | 79      | 233   | 1     | 0.63   |
| SanDisk   | SD7SN3Q256G1002    | 256 GB | 1       | 229   | 0     | 0.63   |
| Samsung   | MZNTY256HDHP-000L7 | 256 GB | 7       | 229   | 0     | 0.63   |
| KingFast  | SSD                | 256 GB | 5       | 227   | 0     | 0.62   |
| Corsair   | Neutron SSD        | 64 GB  | 3       | 294   | 4     | 0.62   |
| Kingston  | SUV300S37A240G     | 240 GB | 9       | 227   | 0     | 0.62   |
| SanDisk   | SD8SN8U512G1002    | 512 GB | 7       | 227   | 0     | 0.62   |
| Crucial   | CT480M500SSD1      | 480 GB | 4       | 958   | 263   | 0.62   |
| Samsung   | MZMPC032HBCD-000L1 | 32 GB  | 2       | 226   | 0     | 0.62   |
| Corsair   | Performance Pro    | 128 GB | 2       | 227   | 1     | 0.62   |
| Samsung   | MMCRE28G5MXP-MVB   | 128 GB | 1       | 225   | 0     | 0.62   |
| Samsung   | MZNTN512HDJH-00007 | 512 GB | 1       | 225   | 0     | 0.62   |
| Samsung   | MZNTE128HMGR-000L1 | 128 GB | 1       | 224   | 0     | 0.62   |
| OCZ       | OCTANE S2          | 64 GB  | 1       | 224   | 0     | 0.61   |
| WDC       | WDS100T1B0A-00H9H0 | 1 TB   | 8       | 223   | 0     | 0.61   |
| Kingston  | SVP200S37A90G      | 90 GB  | 2       | 223   | 0     | 0.61   |
| Team      | L3 EVO SSD         | 120 GB | 4       | 222   | 0     | 0.61   |
| SanDisk   | SSD U110           | 64 GB  | 1       | 222   | 0     | 0.61   |
| Samsung   | SSD 860 EVO mSATA  | 1 TB   | 1       | 221   | 0     | 0.61   |
| PNY       | CS900 480GB SSD    | 480 GB | 3       | 221   | 0     | 0.61   |
| Corsair   | Force LE SSD       | 480 GB | 1       | 220   | 0     | 0.60   |
| Kingston  | SKC300S37A60G      | 64 GB  | 14      | 322   | 5     | 0.60   |
| Samsung   | MZNTE128HMGR-000SO | 128 GB | 2       | 379   | 773   | 0.60   |
| Samsung   | MMDPE56GFDXP-MVB   | 256 GB | 1       | 218   | 0     | 0.60   |
| Micron    | 1100_MTFDDAK2T0TBN | 2 TB   | 2       | 217   | 0     | 0.60   |
| SanDisk   | SDSSDRC032G        | 32 GB  | 1       | 217   | 0     | 0.60   |
| SanDisk   | SDSSDHII120G       | 120 GB | 20      | 217   | 0     | 0.60   |
| Kingston  | RBU-SMSM151S324GD  | 24 GB  | 1       | 217   | 0     | 0.60   |
| Kingston  | SMS200S3120G       | 120 GB | 12      | 245   | 65    | 0.60   |
| Plextor   | PX-128S2G          | 128 GB | 2       | 217   | 0     | 0.60   |
| Samsung   | MMCQE28GFMUP-MVA   | 128 GB | 3       | 243   | 9     | 0.59   |
| Micron    | 1100_MTFDDAK256TBN | 256 GB | 6       | 215   | 0     | 0.59   |
| Hoodisk   | SSD                | 64 GB  | 1       | 214   | 0     | 0.59   |
| Goodram   | C100               | 120 GB | 1       | 214   | 0     | 0.59   |
| OCZ       | VERTEX             | 96 GB  | 1       | 214   | 0     | 0.59   |
| Intenso   | SATA III SSD       | 120 GB | 5       | 214   | 0     | 0.59   |
| Kingston  | SM2280S3G2120G     | 120 GB | 5       | 212   | 0     | 0.58   |
| SanDisk   | Ultra II           | 240 GB | 8       | 212   | 0     | 0.58   |
| DOGFISH   | SSD 256G           | 256 GB | 1       | 212   | 0     | 0.58   |
| Intel     | SSDSC2BF180A4H     | 180 GB | 4       | 426   | 1     | 0.58   |
| WDC       | WDS240G1G0A-00SS50 | 240 GB | 15      | 210   | 0     | 0.58   |
| Samsung   | MZ7TE128HMGR-000H1 | 128 GB | 1       | 210   | 0     | 0.58   |
| Toshiba   | THNSNJ128GCST      | 128 GB | 3       | 208   | 0     | 0.57   |
| SanDisk   | SD8SN8U128G1002    | 128 GB | 2       | 208   | 0     | 0.57   |
| OCZ       | VERTEX2            | 50 GB  | 2       | 309   | 320   | 0.57   |
| Palit     | PH120 SSD          | 120 GB | 1       | 207   | 0     | 0.57   |
| SanDisk   | iSSD P4            | 8 GB   | 4       | 276   | 1     | 0.57   |
| SK hynix  | SC311 SATA         | 128 GB | 11      | 206   | 0     | 0.57   |
| Smartbuy  | m.2 S10-2280T      | 128 GB | 1       | 206   | 0     | 0.57   |
| Corsair   | CSSD-F60GB2        | 64 GB  | 5       | 799   | 199   | 0.56   |
| Zheino    | CHN-25SATAS3-256   | 256 GB | 1       | 205   | 0     | 0.56   |
| Kingston  | SHSS37A480G        | 480 GB | 8       | 205   | 0     | 0.56   |
| SPCC      | SSD B29            | 32 GB  | 1       | 204   | 0     | 0.56   |
| Samsung   | SSD 750 EVO        | 120 GB | 32      | 204   | 0     | 0.56   |
| Micron    | M550_MTFDDAV128MAY | 128 GB | 1       | 204   | 0     | 0.56   |
| SanDisk   | SD6SN1M-256G-1006  | 256 GB | 2       | 203   | 0     | 0.56   |
| SanDisk   | SD6SF1M128GG56     | 128 GB | 1       | 203   | 0     | 0.56   |
| Smartbuy  | m.2 S11-2280S      | 128 GB | 1       | 202   | 0     | 0.56   |
| Toshiba   | THNSNJ128GCSU      | 128 GB | 3       | 202   | 0     | 0.56   |
| Samsung   | MZ7LN256HCHP-000L7 | 256 GB | 5       | 202   | 0     | 0.56   |
| Plextor   | PX-128M7VG         | 128 GB | 2       | 202   | 0     | 0.56   |
| Samsung   | MZRPA128HMCD-000SO | 64 GB  | 10      | 202   | 0     | 0.56   |
| Samsung   | MZNTE256HMHP-000L7 | 256 GB | 1       | 201   | 0     | 0.55   |
| Crucial   | CT256M550SSD3      | 256 GB | 1       | 200   | 0     | 0.55   |
| WDC       | WDS250G2B0A-00SM50 | 250 GB | 17      | 200   | 0     | 0.55   |
| Samsung   | SSD PM871b M.2 ... | 128 GB | 1       | 200   | 0     | 0.55   |
| SanDisk   | SD5SF2128G1014E    | 128 GB | 2       | 200   | 0     | 0.55   |
| Kingston  | SKC400S37256G      | 256 GB | 2       | 199   | 0     | 0.55   |
| Samsung   | MZ7LN512HMJP-000L7 | 512 GB | 1       | 198   | 0     | 0.54   |
| ADATA     | SP900              | 64 GB  | 16      | 257   | 2     | 0.54   |
| Intel     | SSDMCEAC120B3A     | 120 GB | 1       | 198   | 0     | 0.54   |
| OCZ       | VERTEX PLUS        | 64 GB  | 1       | 396   | 1     | 0.54   |
| Goodram   | SSD                | 240 GB | 5       | 197   | 0     | 0.54   |
| Micron    | 1100 SATA          | 512 GB | 4       | 196   | 0     | 0.54   |
| Samsung   | MZNTD256HAGL-00000 | 256 GB | 1       | 196   | 0     | 0.54   |
| Smartbuy  | SSD                | 64 GB  | 22      | 195   | 0     | 0.54   |
| Samsung   | MZNTY256HDHP-000L2 | 256 GB | 1       | 195   | 0     | 0.54   |
| Samsung   | MZ7PD256HCGM-000H7 | 256 GB | 4       | 242   | 611   | 0.54   |
| Plextor   | PX-128S3G          | 128 GB | 1       | 194   | 0     | 0.53   |
| Kingston  | SUV400S37240G      | 240 GB | 56      | 218   | 30    | 0.53   |
| Micron    | MTFDBAK128MAG-1G1  | 128 GB | 2       | 192   | 0     | 0.53   |
| China     | SSD                | 64 GB  | 5       | 254   | 1     | 0.53   |
| OCZ       | VERTEX4            | 512 GB | 1       | 573   | 2     | 0.52   |
| Kingston  | RBU-SNS8152S312... | 128 GB | 2       | 190   | 0     | 0.52   |
| OCZ       | TRION100           | 240 GB | 7       | 237   | 1     | 0.52   |
| Crucial   | CT525MX300SSD4     | 528 GB | 7       | 256   | 1     | 0.52   |
| OCZ       | TRION150           | 240 GB | 4       | 190   | 0     | 0.52   |
| Kingston  | SS100S216G         | 16 GB  | 1       | 190   | 0     | 0.52   |
| Samsung   | MZNLN512HAJQ-000H1 | 512 GB | 1       | 189   | 0     | 0.52   |
| SanDisk   | SDSSDH32000G       | 2 TB   | 2       | 189   | 0     | 0.52   |
| Intel     | SSDSC2BW360H6      | 360 GB | 1       | 566   | 2     | 0.52   |
| SanDisk   | X400 M.2 2280      | 128 GB | 2       | 188   | 0     | 0.52   |
| Kingston  | SV100S2128G        | 128 GB | 2       | 359   | 2     | 0.52   |
| Samsung   | SG9MSM6D024GPM00   | 22 GB  | 1       | 188   | 0     | 0.52   |
| Samsung   | MZMTD512HAGL-000L1 | 512 GB | 3       | 223   | 33    | 0.51   |
| Crucial   | CT2000MX500SSD1    | 2 TB   | 12      | 187   | 0     | 0.51   |
| Transcend | TS128GSSD720       | 128 GB | 2       | 187   | 0     | 0.51   |
| Goodram   | SSD                | 120 GB | 22      | 187   | 0     | 0.51   |
| Toshiba   | THNSNH128GMCT      | 128 GB | 2       | 186   | 0     | 0.51   |
| SanDisk   | SDSSDH3512G        | 512 GB | 6       | 186   | 0     | 0.51   |
| ADATA     | SX900              | 64 GB  | 4       | 515   | 518   | 0.51   |
| SPCC      | SSD162             | 120 GB | 7       | 406   | 436   | 0.51   |
| Smartbuy  | mSata              | 64 GB  | 1       | 186   | 0     | 0.51   |
| SanDisk   | SD8TN8U256G1001    | 256 GB | 2       | 185   | 0     | 0.51   |
| Crucial   | CT525MX300SSD1     | 528 GB | 26      | 270   | 215   | 0.51   |
| SanDisk   | SD6SB1M-128G-1006  | 128 GB | 3       | 185   | 0     | 0.51   |
| Intel     | SSDSC2CT180A4      | 180 GB | 5       | 184   | 0     | 0.51   |
| SPCC      | SSD                | 64 GB  | 73      | 196   | 42    | 0.50   |
| BHT       | WR202HH032G E70... | 32 GB  | 2       | 183   | 0     | 0.50   |
| Kingston  | SV200S3256G        | 256 GB | 4       | 528   | 2     | 0.50   |
| Apacer    | AS350              | 256 GB | 1       | 183   | 0     | 0.50   |
| Micron    | C400-MTFDDAC064MAM | 64 GB  | 1       | 182   | 0     | 0.50   |
| SanDisk   | SSD i100           | 24 GB  | 16      | 194   | 3     | 0.50   |
| Plextor   | PX-256M7VC         | 256 GB | 3       | 181   | 0     | 0.50   |
| Transcend | TS128GMSA740       | 128 GB | 1       | 180   | 0     | 0.50   |
| Smartbuy  | SSD                | 120 GB | 60      | 191   | 1     | 0.49   |
| Kingston  | SNV425S2128GB      | 128 GB | 1       | 1606  | 8     | 0.49   |
| SK hynix  | SC311 SATA         | 256 GB | 19      | 191   | 1     | 0.49   |
| KingDian  | S400 XT            | 240 GB | 1       | 177   | 0     | 0.49   |
| SPCC      | SSD A20            | 64 GB  | 2       | 177   | 0     | 0.49   |
| Apacer    | AS340              | 120 GB | 2       | 176   | 0     | 0.48   |
| BIOSTAR   | S100-240GB PLUS    | 240 GB | 1       | 175   | 0     | 0.48   |
| SanDisk   | SD7TB3Q-128G-1006  | 128 GB | 2       | 220   | 15    | 0.48   |
| Faspeed   | F510-120G          | 120 GB | 1       | 173   | 0     | 0.47   |
| SK hynix  | HFS256G39MND-3310A | 256 GB | 1       | 172   | 0     | 0.47   |
| Goodram   | CX100              | 120 GB | 7       | 226   | 2     | 0.47   |
| Intel     | SSDSC2BW120A4      | 120 GB | 28      | 186   | 1     | 0.47   |
| Kingston  | RBU-SNS8152S351... | 512 GB | 1       | 171   | 0     | 0.47   |
| Netac     | SSD                | 720 GB | 3       | 171   | 0     | 0.47   |
| SanDisk   | SD8SN8U128G1001    | 128 GB | 1       | 170   | 0     | 0.47   |
| Mushkin   | MKNSSDEC60GB       | 64 GB  | 1       | 169   | 0     | 0.46   |
| Apple     | SSD SD0128F        | 121 GB | 2       | 168   | 0     | 0.46   |
| Intenso   | SSD Sata III       | 240 GB | 3       | 166   | 0     | 0.46   |
| WDC       | WDS250G2B0B-00YS70 | 250 GB | 5       | 166   | 0     | 0.46   |
| ADATA     | SX930              | 120 GB | 2       | 165   | 0     | 0.45   |
| Plextor   | PX-AG256M6e        | 256 GB | 2       | 165   | 0     | 0.45   |
| Samsung   | MMCRE28G8MXP-0VBL1 | 128 GB | 2       | 164   | 0     | 0.45   |
| Plextor   | PH6-CE120-G        | 120 GB | 2       | 164   | 0     | 0.45   |
| Samsung   | SSD 830 Series     | 56 GB  | 1       | 164   | 0     | 0.45   |
| Intel     | SSDSC2CW060A3      | 64 GB  | 10      | 265   | 407   | 0.45   |
| Phison    | SATA SSD           | 1 TB   | 1       | 163   | 0     | 0.45   |
| OCZ       | VERTEX460          | 120 GB | 4       | 294   | 5     | 0.45   |
| Apacer    | 256GB SATA Flas... | 256 GB | 1       | 162   | 0     | 0.44   |
| SanDisk   | SD5SE2256G1002E    | 256 GB | 3       | 162   | 0     | 0.44   |
| Samsung   | SSD PM871b M.2 ... | 512 GB | 2       | 161   | 0     | 0.44   |
| Crucial   | M4-CT512M4SSD1     | 512 GB | 1       | 161   | 0     | 0.44   |
| Samsung   | SSD EVO 360G       | 360 GB | 1       | 161   | 0     | 0.44   |
| Samsung   | MZ7LF192HCGS-000L1 | 192 GB | 1       | 161   | 0     | 0.44   |
| Plextor   | PX-256M5S          | 256 GB | 12      | 160   | 0     | 0.44   |
| Samsung   | MZNLF128HCHP-00004 | 128 GB | 3       | 160   | 0     | 0.44   |
| SanDisk   | SD9SN8W512G1102    | 512 GB | 1       | 159   | 0     | 0.44   |
| Micron    | MTFDDAK256MAM-1K1  | 256 GB | 1       | 159   | 0     | 0.44   |
| Zheino    | CHN mSATAM3 128    | 128 GB | 2       | 158   | 0     | 0.43   |
| Toshiba   | A100               | 240 GB | 5       | 158   | 0     | 0.43   |
| WDC       | WDS500G2B0A-00SM50 | 500 GB | 26      | 158   | 0     | 0.43   |
| Ramsta    | SSD S600           | 480 GB | 1       | 158   | 0     | 0.43   |
| SanDisk   | SDSSDH31000G       | 1 TB   | 5       | 158   | 0     | 0.43   |
| Patriot   | Blast              | 120 GB | 6       | 157   | 0     | 0.43   |
| SPCC      | SSD                | 120 GB | 112     | 196   | 110   | 0.43   |
| GeIL      | ZENITH R3_240GB    | 240 GB | 1       | 157   | 0     | 0.43   |
| Phison    | SATA SSD           | 128 GB | 1       | 156   | 0     | 0.43   |
| SK hynix  | SC308 SATA         | 256 GB | 4       | 156   | 0     | 0.43   |
| Samsung   | MMCRE64GFMPP-MVA   | 64 GB  | 2       | 155   | 0     | 0.43   |
| Lite-On   | CV3-CE128-HP       | 128 GB | 1       | 154   | 0     | 0.42   |
| Smartbuy  | SSD                | 240 GB | 18      | 192   | 1     | 0.42   |
| Goodram   | SSDPR-CX300-120    | 120 GB | 3       | 153   | 0     | 0.42   |
| Kingston  | SUV400S37120G      | 120 GB | 68      | 165   | 36    | 0.42   |
| Plextor   | PX-256S2C          | 256 GB | 2       | 153   | 0     | 0.42   |
| Intel     | SSDSC2BW180H6      | 180 GB | 1       | 153   | 0     | 0.42   |
| Micron    | 1100 SATA          | 256 GB | 3       | 344   | 2     | 0.42   |
| Crucial   | FCCT512MX100SSD1   | 512 GB | 1       | 151   | 0     | 0.41   |
| Samsung   | SSD 850 EVO M.2    | 250 GB | 12      | 150   | 0     | 0.41   |
| Samsung   | MZNTY128HDHP-000H1 | 128 GB | 5       | 150   | 0     | 0.41   |
| SanDisk   | X300 MSATA         | 128 GB | 1       | 149   | 0     | 0.41   |
| Plextor   | PH6-CE120          | 120 GB | 6       | 149   | 0     | 0.41   |
| Samsung   | SSD 860 EVO        | 250 GB | 88      | 148   | 0     | 0.41   |
| SK hynix  | SC311 SATA         | 512 GB | 7       | 178   | 149   | 0.41   |
| Intel     | SSDMCEAC180B3      | 180 GB | 2       | 148   | 0     | 0.41   |
| Corsair   | Neutron GTX SSD    | 240 GB | 4       | 180   | 74    | 0.41   |
| Intel     | SSDSC2BB300G4      | 304 GB | 2       | 147   | 0     | 0.41   |
| SanDisk   | SD7TB6S256G1001    | 256 GB | 2       | 146   | 0     | 0.40   |
| Intel     | SSDSC2KG240G7      | 240 GB | 1       | 146   | 0     | 0.40   |
| SK hynix  | SC308 SATA         | 128 GB | 3       | 145   | 0     | 0.40   |
| Kingston  | RBU-SNS8100S3256GD | 256 GB | 1       | 145   | 0     | 0.40   |
| Intel     | SSDSC2BB120G4      | 120 GB | 1       | 143   | 0     | 0.39   |
| QUMO      | SSD                | 64 GB  | 1       | 143   | 0     | 0.39   |
| Samsung   | MZMPC128HBFU-00000 | 128 GB | 1       | 142   | 0     | 0.39   |
| Samsung   | MZNTY128HDHP-000L1 | 128 GB | 2       | 142   | 0     | 0.39   |
| Toshiba   | THNSNW032GMCP      | 32 GB  | 1       | 142   | 0     | 0.39   |
| Samsung   | SSD 860 EVO mSATA  | 250 GB | 9       | 142   | 0     | 0.39   |
| KingSpec  | KSD-SA25.5-064MJ   | 64 GB  | 1       | 141   | 0     | 0.39   |
| Intel     | SSDSC2BF180A5L     | 180 GB | 1       | 141   | 0     | 0.39   |
| Innodisk  | mSATA mini 3ME ... | 32 GB  | 1       | 140   | 0     | 0.39   |
| ADATA     | SU800NS38          | 512 GB | 1       | 139   | 0     | 0.38   |
| WDC       | WDS120G1G0A-00SS50 | 120 GB | 25      | 139   | 0     | 0.38   |
| Toshiba   | THNSNH512GDNT      | 512 GB | 1       | 138   | 0     | 0.38   |
| Apple     | SSD SM0128G        | 121 GB | 7       | 138   | 0     | 0.38   |
| Transcend | TS256GSSD360S      | 256 GB | 2       | 138   | 0     | 0.38   |
| Kingston  | SHFS37A240G        | 240 GB | 20      | 196   | 356   | 0.38   |
| Samsung   | SSD 860 EVO M.2    | 250 GB | 13      | 137   | 0     | 0.38   |
| Lite-On   | IT LMT-256L9M      | 256 GB | 2       | 137   | 0     | 0.38   |
| SanDisk   | Ultra II           | 250 GB | 1       | 137   | 0     | 0.38   |
| Toshiba   | THNSNH256GBST      | 256 GB | 2       | 136   | 0     | 0.37   |
| PNY       | CS900 240GB SSD    | 240 GB | 11      | 136   | 0     | 0.37   |
| Intel     | SSDSC2BB080G4      | 80 GB  | 1       | 135   | 0     | 0.37   |
| Samsung   | SSD 860 EVO        | 500 GB | 131     | 135   | 0     | 0.37   |
| SK hynix  | HFS128G32MND-3210A | 128 GB | 1       | 135   | 0     | 0.37   |
| Samsung   | SSD 850 EVO M.2    | 1 TB   | 3       | 135   | 0     | 0.37   |
| Toshiba   | VX500              | 256 GB | 1       | 134   | 0     | 0.37   |
| Plextor   | PX-128M5S          | 128 GB | 43      | 135   | 1     | 0.37   |
| WDC       | WDS500G1B0A-00H9H0 | 500 GB | 8       | 133   | 0     | 0.36   |
| Transcend | TS256GMTS400       | 256 GB | 3       | 132   | 0     | 0.36   |
| Kingston  | SMS200S330G        | 32 GB  | 1       | 132   | 0     | 0.36   |
| Patriot   | Burst              | 960 GB | 2       | 131   | 0     | 0.36   |
| OCZ       | AGILITY4           | 256 GB | 4       | 142   | 61    | 0.36   |
| SanDisk   | SD9SN8W512G1002    | 512 GB | 1       | 130   | 0     | 0.36   |
| SanDisk   | SSD U110           | 16 GB  | 16      | 130   | 0     | 0.36   |
| ADATA     | SU800NS38          | 128 GB | 2       | 130   | 0     | 0.36   |
| HPE       | MK0800GEYKE        | 800 GB | 1       | 130   | 0     | 0.36   |
| SanDisk   | SDSSDA240G         | 240 GB | 67      | 135   | 3     | 0.36   |
| Toshiba   | THNSNF064GMCS      | 64 GB  | 2       | 129   | 0     | 0.35   |
| Kingston  | SUV300S37A120G     | 120 GB | 23      | 138   | 1     | 0.35   |
| KLEVV     | SSD NEO N500       | 240 GB | 1       | 127   | 0     | 0.35   |
| Intel     | SSDSC2BF240A4L     | 240 GB | 1       | 127   | 0     | 0.35   |
| GALAX     | TA1D0120A          | 120 GB | 2       | 126   | 0     | 0.35   |
| Samsung   | MZMTE256HMHP-000L1 | 256 GB | 2       | 126   | 0     | 0.35   |
| Samsung   | SSD 860 EVO        | 1 TB   | 81      | 126   | 0     | 0.35   |
| Chiprex   | S10T3120GB         | 120 GB | 1       | 126   | 0     | 0.35   |
| Intel     | SSDSC2BW480A4      | 480 GB | 4       | 485   | 13    | 0.35   |
| SanDisk   | SD5SB2-128G-1006E  | 128 GB | 1       | 125   | 0     | 0.34   |
| Toshiba   | TR150              | 480 GB | 3       | 125   | 0     | 0.34   |
| KingFast  | SSD                | 32 GB  | 1       | 125   | 0     | 0.34   |
| Lite-On   | CV5-8Q128          | 128 GB | 1       | 125   | 0     | 0.34   |
| Toshiba   | THNSNJ256G8NY      | 256 GB | 1       | 374   | 2     | 0.34   |
| Samsung   | MZMTD128HAFV-000   | 128 GB | 4       | 124   | 0     | 0.34   |
| KingDian  | S400               | 480 GB | 2       | 124   | 0     | 0.34   |
| OCZ       | ARC100             | 240 GB | 5       | 123   | 0     | 0.34   |
| Corsair   | Force LS SSD       | 64 GB  | 19      | 246   | 164   | 0.34   |
| Apple     | SSD SM512E         | 500 GB | 1       | 123   | 0     | 0.34   |
| Intel     | SSDSC2KF128G8L     | 128 GB | 2       | 122   | 0     | 0.34   |
| ADATA     | SP550              | 240 GB | 14      | 121   | 1     | 0.33   |
| ADATA     | SSD S511           | 64 GB  | 3       | 450   | 679   | 0.33   |
| ADATA     | SP310              | 128 GB | 1       | 120   | 0     | 0.33   |
| Samsung   | MZNTD128HAGM-00000 | 128 GB | 3       | 120   | 0     | 0.33   |
| Kingston  | RBU-SNS8152S312... | 128 GB | 1       | 120   | 0     | 0.33   |
| ADATA     | SSD SX900 512GB... | 512 GB | 1       | 120   | 0     | 0.33   |
| SPCC      | M.2 Disk           | 256 GB | 1       | 119   | 0     | 0.33   |
| Intenso   | SSD                | 256 GB | 2       | 119   | 0     | 0.33   |
| Plextor   | PX-AG128M6e        | 128 GB | 4       | 229   | 2     | 0.33   |
| SanDisk   | SD9SN8W256G1102    | 256 GB | 3       | 118   | 0     | 0.33   |
| Samsung   | MZ7LN512HCHP-000L1 | 512 GB | 2       | 118   | 0     | 0.32   |
| Kingston  | SHFS37A120G        | 120 GB | 72      | 202   | 369   | 0.32   |
| OCZ       | TRION100           | 120 GB | 5       | 139   | 2     | 0.32   |
| KingDian  | S280               | 480 GB | 2       | 117   | 0     | 0.32   |
| Samsung   | MZNLN512HAJQ-00000 | 512 GB | 2       | 117   | 0     | 0.32   |
| Samsung   | MZNLN256HMHQ-000H1 | 256 GB | 6       | 117   | 0     | 0.32   |
| ADATA     | XM13               | 32 GB  | 1       | 116   | 0     | 0.32   |
| Crucial   | CT1024MX200SSD1    | 1 TB   | 1       | 116   | 0     | 0.32   |
| WDC       | WDS100T2B0A-00SM50 | 1 TB   | 17      | 116   | 0     | 0.32   |
| Kingston  | SVP200S3120G       | 120 GB | 4       | 370   | 499   | 0.32   |
| Samsung   | SG9XCS2D400GESLT   | 400 GB | 1       | 115   | 0     | 0.32   |
| Corsair   | Force LE200 SSD    | 240 GB | 2       | 115   | 0     | 0.32   |
| Samsung   | MZMPC128HBFU-000   | 128 GB | 1       | 114   | 0     | 0.31   |
| Patriot   | P200               | 256 GB | 1       | 114   | 0     | 0.31   |
| ADATA     | SU800              | 256 GB | 12      | 119   | 1     | 0.31   |
| Corsair   | Force LE SSD       | 120 GB | 2       | 114   | 0     | 0.31   |
| OCZ       | D2CSTK181M11-0180  | 180 GB | 3       | 114   | 0     | 0.31   |
| SanDisk   | SD9SN8W256G        | 256 GB | 2       | 113   | 0     | 0.31   |
| Corsair   | Force LS SSD       | 120 GB | 10      | 268   | 505   | 0.31   |
| Intel     | SSDSA2M080G2LE     | 80 GB  | 2       | 154   | 6     | 0.31   |
| OCZ       | VERTEX2            | 90 GB  | 1       | 113   | 0     | 0.31   |
| Micron    | MTFDDAK512MAM-1K1  | 512 GB | 1       | 113   | 0     | 0.31   |
| Toshiba   | Q300               | 120 GB | 2       | 112   | 0     | 0.31   |
| ADATA     | SU800              | 1 TB   | 6       | 112   | 0     | 0.31   |
| Kingston  | RBUSNS8280S3128GH2 | 128 GB | 2       | 112   | 0     | 0.31   |
| Samsung   | MZNLN256HCHP-00000 | 256 GB | 3       | 112   | 0     | 0.31   |
| Seagate   | BarraCuda SSD Z... | 250 GB | 2       | 112   | 0     | 0.31   |
| Patriot   | Blaze              | 120 GB | 4       | 111   | 0     | 0.31   |
| Seagate   | SSD                | 500 GB | 1       | 111   | 0     | 0.31   |
| Kingston  | SUV400S37480G      | 480 GB | 4       | 141   | 1     | 0.30   |
| SanDisk   | SD6SB1M128G1002    | 128 GB | 1       | 110   | 0     | 0.30   |
| ADATA     | SU700              | 120 GB | 7       | 112   | 2     | 0.30   |
| Samsung   | MZNLF128HCHP-000H1 | 128 GB | 1       | 109   | 0     | 0.30   |
| Faspeed   | H7-240G            | 240 GB | 1       | 109   | 0     | 0.30   |
| SK hynix  | HFS256G32TND-N210A | 256 GB | 2       | 108   | 0     | 0.30   |
| SanDisk   | SD7SB6S-128G-1006  | 128 GB | 1       | 108   | 0     | 0.30   |
| Mushkin   | MKNSSDRE1TB        | 1 TB   | 1       | 107   | 0     | 0.30   |
| Transcend | TS256GSSD370       | 256 GB | 1       | 107   | 0     | 0.30   |
| SanDisk   | SD8SN8U-256G-1006  | 256 GB | 13      | 182   | 316   | 0.30   |
| Kingston  | MS80000058688      | 256 GB | 1       | 107   | 0     | 0.29   |
| Crucial   | CT240BX200SSD1     | 240 GB | 6       | 107   | 0     | 0.29   |
| Crucial   | C300-CTFDDAC256MAG | 256 GB | 2       | 555   | 504   | 0.29   |
| Lite-On   | CV3-8D256          | 256 GB | 2       | 106   | 0     | 0.29   |
| Crucial   | CT256M550SSD1      | 256 GB | 6       | 362   | 8     | 0.29   |
| Intenso   | SSD Sata III       | 120 GB | 2       | 106   | 0     | 0.29   |
| PNY       | SSD2SC240G5LC72... | 240 GB | 1       | 106   | 0     | 0.29   |
| Mushkin   | MKNSSDAT60GB-V     | 64 GB  | 1       | 106   | 0     | 0.29   |
| Samsung   | MZYTE128HMGR-000L2 | 128 GB | 1       | 106   | 0     | 0.29   |
| Plextor   | PH6-CE240-L1       | 240 GB | 1       | 106   | 0     | 0.29   |
| Lite-On   | IT L8T-128L9G      | 128 GB | 1       | 105   | 0     | 0.29   |
| Toshiba   | THNSNC256GBSJ      | 256 GB | 1       | 105   | 0     | 0.29   |
| Plextor   | PX-128M5M          | 128 GB | 8       | 104   | 0     | 0.29   |
| Kingston  | SHFS37A480G        | 480 GB | 1       | 104   | 0     | 0.29   |
| Transcend | TS64GSSD340        | 64 GB  | 3       | 180   | 336   | 0.28   |
| ADATA     | SP600              | 64 GB  | 7       | 113   | 2     | 0.28   |
| China     | SATA SSD           | 240 GB | 13      | 103   | 0     | 0.28   |
| Samsung   | SSD 860 EVO        | 4 TB   | 3       | 103   | 0     | 0.28   |
| Intel     | SSDSA2M160G2GN     | 160 GB | 1       | 2996  | 28    | 0.28   |
| SK hynix  | SC210 2.5 7MM      | 128 GB | 2       | 478   | 2     | 0.28   |
| Fujitsu   | F300               | 480 GB | 1       | 103   | 0     | 0.28   |
| Transcend | TS120GSSD25D-M     | 128 GB | 1       | 309   | 2     | 0.28   |
| Lite-On   | LMT-256L9M-11 M... | 256 GB | 1       | 103   | 0     | 0.28   |
| ADATA     | SU900              | 512 GB | 2       | 102   | 0     | 0.28   |
| Intel     | SSDSA2BW120G3H     | 120 GB | 1       | 102   | 0     | 0.28   |
| SanDisk   | SDSA6MM-032G-1006  | 32 GB  | 1       | 102   | 0     | 0.28   |
| Smartbuy  | mSata              | 256 GB | 1       | 102   | 0     | 0.28   |
| KingFast  | SSD                | 32 GB  | 1       | 102   | 0     | 0.28   |
| Phison    | SSM28512GPTCB3B... | 512 GB | 1       | 101   | 0     | 0.28   |
| Intel     | SSDSC2BW180A3H     | 180 GB | 2       | 101   | 0     | 0.28   |
| Micron    | MTFDDAK256TBN      | 256 GB | 1       | 101   | 0     | 0.28   |
| Samsung   | MZ7TY256HDHP-00000 | 256 GB | 2       | 101   | 0     | 0.28   |
| Samsung   | SSD 860 PRO        | 512 GB | 14      | 100   | 0     | 0.28   |
| SanDisk   | SSD PLUS 120 GB    | 120 GB | 15      | 104   | 1     | 0.28   |
| China     | SATA SSD           | 128 GB | 6       | 99    | 0     | 0.27   |
| Intel     | SSDSC2BW120H6      | 120 GB | 9       | 148   | 8     | 0.27   |
| Hikvision | HKVSN HS-SSD-C1... | 240 GB | 1       | 99    | 0     | 0.27   |
| OWC       | Mercury Electra... | 2 TB   | 2       | 99    | 0     | 0.27   |
| Samsung   | MZ7LN256HAJQ-000L7 | 256 GB | 1       | 98    | 0     | 0.27   |
| Micron    | 5100_MTFDDAK240TCB | 240 GB | 1       | 98    | 0     | 0.27   |
| Patriot   | Flare              | 64 GB  | 2       | 98    | 0     | 0.27   |
| SanDisk   | SD8SN8U512G1122    | 512 GB | 1       | 98    | 0     | 0.27   |
| SPCC      | SSD                | 240 GB | 33      | 171   | 299   | 0.27   |
| Lite-On   | L8H-256V2G-HP      | 256 GB | 5       | 97    | 0     | 0.27   |
| ADATA     | SP920SS            | 128 GB | 5       | 409   | 7     | 0.27   |
| Intenso   | SSD                | 120 GB | 1       | 97    | 0     | 0.27   |
| Micron    | MTFDDAV256TBN-1... | 256 GB | 7       | 135   | 149   | 0.27   |
| Leven     | JAJS600M512C       | 512 GB | 1       | 97    | 0     | 0.27   |
| Transcend | TS120GSSD220S      | 120 GB | 10      | 96    | 0     | 0.27   |
| Anobit    | Gen2A400 118032738 | 400 GB | 1       | 96    | 0     | 0.27   |
| SanDisk   | SD7SB3Q128G1002    | 128 GB | 1       | 387   | 3     | 0.27   |
| SanDisk   | SDSSDH3 250G       | 250 GB | 3       | 96    | 0     | 0.26   |
| SK hynix  | HFS256G39TND-N210A | 256 GB | 10      | 103   | 1     | 0.26   |
| Toshiba   | THNSNJ512GDNU A    | 512 GB | 1       | 96    | 0     | 0.26   |
| Samsung   | MZNLN256HCHP-000L2 | 256 GB | 3       | 96    | 0     | 0.26   |
| PHISON    | 256GB PS3110-S10C  | 256 GB | 1       | 95    | 0     | 0.26   |
| SanDisk   | SD9SB8W512G1101    | 512 GB | 2       | 95    | 0     | 0.26   |
| Samsung   | SSD 860 EVO M.2    | 500 GB | 12      | 95    | 0     | 0.26   |
| SPCC      | SSD170             | 120 GB | 3       | 245   | 341   | 0.26   |
| BHT       | WR202I0064G E70... | 64 GB  | 1       | 95    | 0     | 0.26   |
| ADATA     | SU655              | 120 GB | 4       | 95    | 0     | 0.26   |
| Intel     | SSDSC2KB960G8      | 960 GB | 4       | 94    | 0     | 0.26   |
| WDC       | WDS250G1B0B-00AS40 | 250 GB | 3       | 94    | 0     | 0.26   |
| SPCC      | SSD                | 512 GB | 7       | 94    | 0     | 0.26   |
| SanDisk   | SSD U100           | 256 GB | 1       | 94    | 0     | 0.26   |
| Patriot   | Blaze              | 64 GB  | 4       | 94    | 0     | 0.26   |
| OCZ       | VERTEX460A         | 120 GB | 5       | 134   | 1     | 0.26   |
| SanDisk   | SD8SN8U256G1002    | 256 GB | 1       | 93    | 0     | 0.26   |
| Team      | T2535T480G         | 480 GB | 1       | 93    | 0     | 0.26   |
| KingFast  | SSD                | 240 GB | 1       | 93    | 0     | 0.26   |
| Mushkin   | MKNSSDSR250GB      | 250 GB | 1       | 93    | 0     | 0.26   |
| Samsung   | MZNLN128HCGR-000H1 | 128 GB | 1       | 93    | 0     | 0.25   |
| WDC       | WDBNCE0010PNC      | 1 TB   | 1       | 92    | 0     | 0.25   |
| SPCC      | SSD                | 128 GB | 18      | 93    | 1     | 0.25   |
| China     | 120GB SSD          | 120 GB | 41      | 92    | 0     | 0.25   |
| Samsung   | MZMTD256HAGM-00000 | 256 GB | 1       | 92    | 0     | 0.25   |
| Lite-On   | PH2-CJ120          | 120 GB | 1       | 92    | 0     | 0.25   |
| SanDisk   | SDSSDA120G         | 120 GB | 49      | 94    | 2     | 0.25   |
| Intel     | SSDSC2BF240A5L     | 240 GB | 3       | 91    | 0     | 0.25   |
| Gigabyte  | GP-GSTFS30512GTTD  | 512 GB | 3       | 91    | 0     | 0.25   |
| Kingston  | SUV500480G         | 480 GB | 4       | 90    | 0     | 0.25   |
| SanDisk   | SD9SB8W128G1001    | 128 GB | 1       | 90    | 0     | 0.25   |
| Kingston  | SUV500120G         | 120 GB | 11      | 90    | 0     | 0.25   |
| SanDisk   | SSD U100           | 24 GB  | 20      | 120   | 65    | 0.25   |
| Faspeed   | H5-60G PLUS        | 64 GB  | 1       | 90    | 0     | 0.25   |
| Goodram   | IR-SSDPR-S25A-120  | 120 GB | 4       | 90    | 0     | 0.25   |
| SanDisk   | SD7SB3Q256G1002    | 256 GB | 2       | 232   | 26    | 0.25   |
| SanDisk   | SDSSDH3250G        | 250 GB | 9       | 89    | 0     | 0.25   |
| Kingston  | SV300S37A480G      | 480 GB | 12      | 96    | 85    | 0.25   |
| Samsung   | SSD 860 EVO mSATA  | 500 GB | 4       | 89    | 0     | 0.25   |
| Crucial   | CT500BX100SSD1     | 500 GB | 4       | 89    | 0     | 0.25   |
| Plextor   | PH6-CE120-L1       | 120 GB | 2       | 89    | 0     | 0.24   |
| WDC       | WDS120G1G0B-00RC30 | 120 GB | 4       | 89    | 0     | 0.24   |
| Toshiba   | TR200              | 480 GB | 6       | 88    | 0     | 0.24   |
| Kingston  | RBU-SNS8151S396GG  | 96 GB  | 1       | 88    | 0     | 0.24   |
| Micron    | MTFDDAK256MAY-1... | 256 GB | 1       | 1492  | 16    | 0.24   |
| KingDian  | S400               | 120 GB | 9       | 87    | 0     | 0.24   |
| SanDisk   | X600 M.2 2280 SATA | 128 GB | 2       | 87    | 0     | 0.24   |
| Kingston  | SKC380S3120G       | 120 GB | 1       | 86    | 0     | 0.24   |
| ADATA     | SP580              | 120 GB | 10      | 86    | 0     | 0.24   |
| Crucial   | CT500MX500SSD1     | 500 GB | 52      | 86    | 0     | 0.24   |
| KingSpec  | P4-960             | 960 GB | 1       | 86    | 0     | 0.24   |
| Plextor   | PX-128M5Pro        | 128 GB | 51      | 86    | 0     | 0.24   |
| Lexar     | SSD                | 240 GB | 1       | 86    | 0     | 0.24   |
| Mushkin   | MKNSSDEC120GB      | 120 GB | 1       | 86    | 0     | 0.24   |
| KingFast  | SSD                | 128 GB | 9       | 85    | 0     | 0.23   |
| Intel     | SSDSCKKF256G8 SATA | 256 GB | 4       | 85    | 0     | 0.23   |
| Samsung   | MZNTE128HMGR-000H1 | 128 GB | 1       | 85    | 0     | 0.23   |
| Seagate   | SSD                | 1 TB   | 1       | 85    | 0     | 0.23   |
| Plextor   | PX-256M3           | 256 GB | 1       | 256   | 2     | 0.23   |
| XPG       | SX950U             | 240 GB | 1       | 85    | 0     | 0.23   |
| SK hynix  | HFS256G3BTND-N210A | 256 GB | 4       | 84    | 0     | 0.23   |
| Micron    | M600_MTFDDAK1T0MBF | 1 TB   | 2       | 84    | 0     | 0.23   |
| Transcend | TS256GSSD320       | 256 GB | 2       | 84    | 0     | 0.23   |
| China     | SATA SSD           | 64 GB  | 17      | 83    | 0     | 0.23   |
| Apacer    | AS510S             | 64 GB  | 4       | 82    | 0     | 0.23   |
| Lenovo    | SSD SL700 120G     | 120 GB | 2       | 82    | 0     | 0.23   |
| Kingston  | SA400S37120G       | 120 GB | 228     | 87    | 1     | 0.23   |
| PNY       | CS900 120GB SSD    | 120 GB | 16      | 82    | 0     | 0.23   |
| Apple     | SSD TS064C         | 64 GB  | 1       | 81    | 0     | 0.22   |
| Intel     | SSDSC2KW512G8      | 512 GB | 6       | 82    | 1     | 0.22   |
| OCZ       | VECTOR180          | 120 GB | 2       | 81    | 0     | 0.22   |
| Kingmax   | SSD                | 120 GB | 21      | 205   | 342   | 0.22   |
| Kingston  | SUV500MS240G       | 240 GB | 2       | 81    | 0     | 0.22   |
| Lite-On   | LCS-128M6S         | 128 GB | 3       | 81    | 0     | 0.22   |
| Micron    | MTFDDAV512TBN      | 512 GB | 1       | 81    | 0     | 0.22   |
| Crucial   | CT960BX500SSD1     | 960 GB | 6       | 80    | 0     | 0.22   |
| Crucial   | CT2050MX300SSD1    | 2 TB   | 3       | 89    | 1     | 0.22   |
| Corsair   | Force LS SSD       | 480 GB | 1       | 80    | 0     | 0.22   |
| Kingston  | RBU-SNS8152S325... | 256 GB | 1       | 80    | 0     | 0.22   |
| Team      | TEAML5Lite3D240G   | 240 GB | 2       | 80    | 0     | 0.22   |
| ADATA     | SU650              | 480 GB | 10      | 107   | 313   | 0.22   |
| Lite-On   | LAT-256M2S         | 256 GB | 1       | 239   | 2     | 0.22   |
| Fordisk   | S860 256G 6Gbps    | 256 GB | 1       | 79    | 0     | 0.22   |
| SanDisk   | SD9TB8W256G1001    | 256 GB | 2       | 79    | 0     | 0.22   |
| SanDisk   | SSD PLUS           | 480 GB | 16      | 87    | 1     | 0.22   |
| China     | SSD 120G           | 120 GB | 3       | 79    | 0     | 0.22   |
| WDC       | WDS500G2B0B-00YS70 | 500 GB | 11      | 79    | 0     | 0.22   |
| Seagate   | ST120HM000-1G5142  | 120 GB | 1       | 79    | 0     | 0.22   |
| Toshiba   | Q300 Pro           | 128 GB | 1       | 79    | 0     | 0.22   |
| Lite-On   | IT LCS-128L9S-HP   | 128 GB | 2       | 78    | 0     | 0.21   |
| Crucial   | CT500MX500SSD4     | 500 GB | 12      | 78    | 0     | 0.21   |
| Corsair   | Neutron XTI SSD    | 240 GB | 1       | 77    | 0     | 0.21   |
| Toshiba   | THNSNK128GVN8      | 128 GB | 4       | 77    | 0     | 0.21   |
| KingDian  | S180               | 64 GB  | 12      | 81    | 95    | 0.21   |
| Transcend | TS256GSSD340       | 256 GB | 2       | 76    | 0     | 0.21   |
| Toshiba   | THNSNJ128G8NY      | 128 GB | 2       | 76    | 0     | 0.21   |
| Crucial   | CT1000MX500SSD4    | 1 TB   | 8       | 76    | 0     | 0.21   |
| Palit     | UVS                | 120 GB | 2       | 76    | 0     | 0.21   |
| Transcend | TS1TSSD230S        | 1 TB   | 3       | 76    | 0     | 0.21   |
| Lite-On   | CV3-8D256-41 SA... | 256 GB | 1       | 75    | 0     | 0.21   |
| Lite-On   | LCS-128M6S-HP      | 128 GB | 3       | 75    | 0     | 0.21   |
| Samsung   | SSD 650            | 120 GB | 3       | 75    | 0     | 0.21   |
| Transcend | TS256GSSD230S      | 256 GB | 3       | 75    | 0     | 0.21   |
| AMD       | R5SL240G           | 240 GB | 8       | 92    | 1     | 0.21   |
| Transcend | TS64GSSD360S       | 64 GB  | 1       | 75    | 0     | 0.21   |
| Samsung   | SSD 860 QVO        | 1 TB   | 35      | 75    | 0     | 0.21   |
| Patriot   | Burst              | 240 GB | 12      | 75    | 0     | 0.21   |
| ADATA     | SU810NS38 SATA ... | 128 GB | 1       | 75    | 0     | 0.21   |
| OCZ       | ONYX               | 32 GB  | 2       | 105   | 1     | 0.21   |
| China     | 64GB SSD           | 64 GB  | 11      | 74    | 0     | 0.20   |
| SanDisk   | SD7SN3Q128G1002    | 128 GB | 2       | 99    | 1     | 0.20   |
| ADATA     | SX900              | 256 GB | 5       | 332   | 649   | 0.20   |
| Kingston  | SA400S37240G       | 240 GB | 150     | 77    | 1     | 0.20   |
| Samsung   | MZNLN256HAJQ-000L2 | 256 GB | 5       | 74    | 0     | 0.20   |
| Reeinno   | ST240GB S4S3       | 240 GB | 1       | 74    | 0     | 0.20   |
| Samsung   | SSD 860 PRO        | 2 TB   | 3       | 73    | 0     | 0.20   |
| Toshiba   | TR200              | 240 GB | 18      | 73    | 0     | 0.20   |
| HP        | SSD M700           | 120 GB | 3       | 73    | 0     | 0.20   |
| China     | SATA SSD           | 480 GB | 1       | 73    | 0     | 0.20   |
| Goodram   | SSDPR-CL100-240    | 240 GB | 2       | 73    | 0     | 0.20   |
| SanDisk   | SD8SN8U-128G-1006  | 128 GB | 19      | 133   | 163   | 0.20   |
| SanDisk   | SSD PLUS 240 GB    | 240 GB | 7       | 72    | 0     | 0.20   |
| WDC       | WDS120G2G0A-00JH30 | 120 GB | 68      | 72    | 1     | 0.20   |
| Goodram   | SSDPR-CL100-480-G2 | 480 GB | 3       | 71    | 0     | 0.20   |
| Transcend | TS240GSSD220S      | 240 GB | 9       | 71    | 0     | 0.20   |
| WDC       | WDS120G2G0B-00EPW0 | 120 GB | 15      | 74    | 1     | 0.20   |
| ADATA     | SU630              | 480 GB | 3       | 71    | 0     | 0.20   |
| Samsung   | SSD 850            | 120 GB | 21      | 71    | 0     | 0.20   |
| Plextor   | PX-256M6Pro        | 256 GB | 2       | 71    | 0     | 0.20   |
| ADATA     | SU630              | 960 GB | 1       | 70    | 0     | 0.19   |
| OCZ       | SABER1000          | 480 GB | 1       | 70    | 0     | 0.19   |
| Crucial   | CT240BX300SSD1     | 240 GB | 2       | 69    | 0     | 0.19   |
| SanDisk   | SSD i100           | 8 GB   | 3       | 69    | 0     | 0.19   |
| Kingston  | RBUSNS8180S3128GJ  | 128 GB | 2       | 69    | 0     | 0.19   |
| PNY       | CS1311 120GB SSD   | 120 GB | 3       | 69    | 0     | 0.19   |
| Team      | T2535T120G         | 120 GB | 2       | 142   | 4     | 0.19   |
| China     | SATA SSD           | 120 GB | 28      | 69    | 0     | 0.19   |
| Transcend | TS256GMTS800       | 256 GB | 2       | 69    | 0     | 0.19   |
| oyunkey   | SSD                | 120 GB | 1       | 68    | 0     | 0.19   |
| KingSpec  | MSH-256            | 256 GB | 2       | 68    | 0     | 0.19   |
| SanDisk   | PLUS               | 480 GB | 2       | 68    | 0     | 0.19   |
| Samsung   | MZNLN256HAJQ-00000 | 256 GB | 5       | 68    | 0     | 0.19   |
| Samsung   | MZNTY256HDHP-000H1 | 256 GB | 1       | 204   | 2     | 0.19   |
| China     | 240GB SSD          | 240 GB | 3       | 68    | 0     | 0.19   |
| ADATA     | S596               | 128 GB | 1       | 68    | 0     | 0.19   |
| HP        | SSD S700           | 250 GB | 3       | 68    | 0     | 0.19   |
| Gigabyte  | GP-GSTFS31120GNTD  | 120 GB | 7       | 67    | 0     | 0.19   |
| SanDisk   | SDSSDA480G         | 480 GB | 5       | 67    | 0     | 0.19   |
| Londisk   | SSD                | 120 GB | 7       | 67    | 0     | 0.19   |
| Crucial   | CT1000MX500SSD1    | 1 TB   | 42      | 67    | 0     | 0.19   |
| Plextor   | PX-128M6M          | 128 GB | 4       | 67    | 0     | 0.19   |
| PNY       | SSD2SC240G1LC70... | 240 GB | 1       | 67    | 0     | 0.18   |
| WDC       | WDS240G1G0B-00RC30 | 240 GB | 5       | 67    | 0     | 0.18   |
| ADATA     | SP900              | 512 GB | 2       | 66    | 0     | 0.18   |
| SanDisk   | SD8TB8U512G1001    | 512 GB | 1       | 66    | 0     | 0.18   |
| Samsung   | MZ7LF120HCHP-000L1 | 120 GB | 2       | 66    | 0     | 0.18   |
| Goodram   | SSDPR-CX300-240    | 240 GB | 2       | 66    | 0     | 0.18   |
| Corsair   | CSSD-F120GB3-BK    | 120 GB | 1       | 65    | 0     | 0.18   |
| Plextor   | PX-128M6S          | 128 GB | 26      | 70    | 43    | 0.18   |
| Plextor   | PX-512S2G          | 512 GB | 1       | 65    | 0     | 0.18   |
| SPCC      | SSD                | 55 GB  | 9       | 361   | 452   | 0.18   |
| Lite-On   | LMT-32L3M-HP       | 32 GB  | 2       | 65    | 0     | 0.18   |
| Team      | T253X2128G         | 128 GB | 1       | 65    | 0     | 0.18   |
| Goodram   | SSDPR-CX400-256    | 256 GB | 4       | 65    | 0     | 0.18   |
| Kingston  | SA400S37480G       | 480 GB | 42      | 68    | 3     | 0.18   |
| Intel     | SSDSA2M160G2GC     | 160 GB | 1       | 578   | 8     | 0.18   |
| Transcend | TS256GSSD370S      | 256 GB | 6       | 64    | 0     | 0.18   |
| ADATA     | SU810NS38 SATA ... | 256 GB | 5       | 64    | 0     | 0.18   |
| Team      | T2535T240G         | 240 GB | 1       | 63    | 0     | 0.17   |
| Samsung   | MZNLN256HAJQ-000H1 | 256 GB | 7       | 88    | 29    | 0.17   |
| Toshiba   | Q300               | 240 GB | 2       | 325   | 6     | 0.17   |
| Intel     | SSDSC2BW080A4      | 80 GB  | 1       | 63    | 0     | 0.17   |
| Kingston  | SA400S37960G       | 960 GB | 4       | 63    | 0     | 0.17   |
| ADATA     | SU655              | 480 GB | 1       | 63    | 0     | 0.17   |
| Transcend | TS128GMTS400S      | 128 GB | 2       | 63    | 0     | 0.17   |
| WDC       | WDBNCE2500PNC      | 250 GB | 2       | 63    | 0     | 0.17   |
| SK hynix  | HFS256G32TNF-N3A0A | 256 GB | 1       | 62    | 0     | 0.17   |
| SanDisk   | SDSSDH2064G        | 64 GB  | 1       | 62    | 0     | 0.17   |
| KingSpec  | P4-480             | 480 GB | 2       | 62    | 0     | 0.17   |
| Kingrich  | SSD 120G           | 120 GB | 1       | 62    | 0     | 0.17   |
| Patriot   | Burst              | 120 GB | 20      | 61    | 0     | 0.17   |
| OCZ       | VERTEX460          | 240 GB | 2       | 61    | 0     | 0.17   |
| Plextor   | PX-128S3C          | 128 GB | 11      | 61    | 0     | 0.17   |
| Lite-On   | LST-32S9G-11 SATA  | 32 GB  | 1       | 61    | 0     | 0.17   |
| Toshiba   | Q200 EX            | 240 GB | 1       | 61    | 0     | 0.17   |
| ADATA     | SU900              | 256 GB | 6       | 61    | 1     | 0.17   |
| Plextor   | PX-256M6S          | 256 GB | 10      | 69    | 214   | 0.17   |
| Gigabyte  | GP-GSTFS31100TNTD  | 1 TB   | 1       | 61    | 0     | 0.17   |
| OCZ       | VERTEX450          | 128 GB | 2       | 69    | 1022  | 0.17   |
| Lite-On   | LCH-512V2S-11 2... | 512 GB | 1       | 60    | 0     | 0.17   |
| PHISON    | 128GB PS3109-S9    | 128 GB | 1       | 121   | 1     | 0.17   |
| Crucial   | CT250MX500SSD1     | 250 GB | 27      | 63    | 1     | 0.17   |
| Samsung   | MZ7LN128HAHQ-000L1 | 128 GB | 2       | 60    | 0     | 0.17   |
| Samsung   | SSD 860 EVO M.2    | 1 TB   | 6       | 60    | 0     | 0.17   |
| Toshiba   | THNSN9480GESG      | 480 GB | 1       | 60    | 0     | 0.17   |
| SPCC      | SSD                | 256 GB | 15      | 70    | 7     | 0.16   |
| SanDisk   | SSD PLUS           | 120 GB | 14      | 60    | 0     | 0.16   |
| BIWIN     | SSD                | 128 GB | 5       | 59    | 0     | 0.16   |
| SK hynix  | HFS128G39TND-N210A | 128 GB | 22      | 72    | 4     | 0.16   |
| KingDian  | S400               | 240 GB | 1       | 59    | 0     | 0.16   |
| Goodram   | IR-SSDPR-S25A-240  | 240 GB | 2       | 59    | 0     | 0.16   |
| Lite-On   | LMT-64M6M-HP       | 64 GB  | 1       | 59    | 0     | 0.16   |
| Team      | T253LE240G         | 240 GB | 2       | 59    | 0     | 0.16   |
| TEKET     | SA18-032M-4F       | 32 GB  | 2       | 59    | 0     | 0.16   |
| Kingston  | SUV500240G         | 240 GB | 14      | 71    | 83    | 0.16   |
| Crucial   | CT250BX100SSD1     | 250 GB | 13      | 60    | 1     | 0.16   |
| OCZ       | VERTEX2            | 180 GB | 1       | 58    | 0     | 0.16   |
| Plextor   | PX-512M6Pro        | 512 GB | 1       | 58    | 0     | 0.16   |
| BIWIN     | SSD                | 120 GB | 2       | 58    | 0     | 0.16   |
| Intel     | SSDSC2KW256G8      | 256 GB | 17      | 58    | 0     | 0.16   |
| Kingston  | SKC380S3240G       | 240 GB | 1       | 58    | 0     | 0.16   |
| Transcend | TS128GMTS400       | 128 GB | 3       | 58    | 0     | 0.16   |
| Goodram   | SSDPR-CX400-512    | 512 GB | 5       | 58    | 0     | 0.16   |
| Zheino    | CHN 25SATAC3 120   | 120 GB | 1       | 58    | 0     | 0.16   |
| tigo      | SSD                | 120 GB | 1       | 57    | 0     | 0.16   |
| Goldkey   | GKH84-64GB         | 64 GB  | 1       | 57    | 0     | 0.16   |
| Crucial   | CT512M550SSD3      | 512 GB | 4       | 108   | 176   | 0.16   |
| ADATA     | SP610              | 128 GB | 2       | 57    | 0     | 0.16   |
| SanDisk   | X600 M.2 2280 SATA | 256 GB | 1       | 56    | 0     | 0.16   |
| ADATA     | SP900NS38          | 128 GB | 3       | 124   | 339   | 0.16   |
| SanDisk   | SD7SB6S-256G-1006  | 256 GB | 1       | 56    | 0     | 0.16   |
| Samsung   | MZNTY256HDHP-00000 | 256 GB | 2       | 56    | 0     | 0.16   |
| Phison    | SATA SSD           | 120 GB | 12      | 56    | 0     | 0.15   |
| China     | 128GB SSD          | 128 GB | 10      | 56    | 0     | 0.15   |
| Lexar     | SSD                | 480 GB | 1       | 56    | 0     | 0.15   |
| Radeon    | R7                 | 120 GB | 1       | 56    | 0     | 0.15   |
| WDC       | WDS240G2G0B-00EPW0 | 240 GB | 26      | 56    | 1     | 0.15   |
| Team      | TEAML5Lite3D480G   | 480 GB | 1       | 55    | 0     | 0.15   |
| Gigabyte  | GP-GSTFS31240GNTD  | 240 GB | 8       | 55    | 0     | 0.15   |
| Corsair   | Force LE200 SSD    | 120 GB | 3       | 55    | 0     | 0.15   |
| Micron    | 1100_MTFDDAV512TBN | 512 GB | 10      | 61    | 1     | 0.15   |
| ADATA     | SU800              | 512 GB | 4       | 55    | 0     | 0.15   |
| Samsung   | MZYTE256HMHP-000L2 | 256 GB | 1       | 55    | 0     | 0.15   |
| SanDisk   | SSD PLUS           | 1 TB   | 8       | 58    | 1     | 0.15   |
| Lite-On   | CV8-8E128-11 SATA  | 128 GB | 6       | 55    | 0     | 0.15   |
| SanDisk   | SD6SB1M128G1022I   | 128 GB | 3       | 54    | 0     | 0.15   |
| Transcend | TS128GSSD370       | 128 GB | 8       | 54    | 0     | 0.15   |
| Micron    | 1100_MTFDDAV256TBN | 256 GB | 28      | 62    | 139   | 0.15   |
| Goodram   | SSDPR-CX400-128    | 128 GB | 6       | 54    | 0     | 0.15   |
| Netac     | SSD                | 1 TB   | 1       | 53    | 0     | 0.15   |
| LDLC      | SSD                | 120 GB | 3       | 53    | 0     | 0.15   |
| Intel     | SSDSA2M160G2LE     | 160 GB | 2       | 1075  | 16    | 0.15   |
| Samsung   | MZMTD128HAFV-000H1 | 128 GB | 1       | 53    | 0     | 0.15   |
| Zheino    | CHN-25SATAA3-480   | 480 GB | 2       | 53    | 0     | 0.15   |
| China     | SSD                | 120 GB | 9       | 53    | 0     | 0.15   |
| Lite-On   | CV3-8D128-11 SATA  | 128 GB | 3       | 52    | 0     | 0.14   |
| Apple     | SSD SM128E         | 121 GB | 1       | 52    | 0     | 0.14   |
| Intel     | SSDSCKKB240G8      | 240 GB | 1       | 52    | 0     | 0.14   |
| Samsung   | SSD 860 QVO        | 2 TB   | 8       | 52    | 0     | 0.14   |
| Team      | L5 LITE SSD        | 64 GB  | 1       | 52    | 0     | 0.14   |
| Team      | L7 EVO SSD         | 64 GB  | 1       | 51    | 0     | 0.14   |
| Lite-On   | CV3-8D256-11 SATA  | 256 GB | 2       | 51    | 0     | 0.14   |
| Lite-On   | LMT-19nmBGA-128G   | 128 GB | 1       | 51    | 0     | 0.14   |
| Lite-On   | CV3-8D128          | 128 GB | 2       | 50    | 0     | 0.14   |
| KingSpec  | Q-180              | 180 GB | 4       | 58    | 235   | 0.14   |
| Samsung   | SSD PM871b M.2 ... | 256 GB | 1       | 50    | 0     | 0.14   |
| Micron    | MTFDDAV256MBF-1... | 256 GB | 1       | 50    | 0     | 0.14   |
| Samsung   | SSD PB22-CS3 FD... | 256 GB | 1       | 50    | 0     | 0.14   |
| Crucial   | CT480BX500SSD1     | 480 GB | 14      | 50    | 0     | 0.14   |
| Crucial   | CT120BX300SSD1     | 120 GB | 4       | 50    | 0     | 0.14   |
| OCZ       | INTREPID 3800      | 400 GB | 1       | 50    | 0     | 0.14   |
| Corsair   | Neutron GTX SSD    | 480 GB | 1       | 49    | 0     | 0.14   |
| Seagate   | BarraCuda 120 S... | 500 GB | 1       | 49    | 0     | 0.14   |
| Micron    | MTFDDAK256TDL      | 256 GB | 1       | 49    | 0     | 0.14   |
| Intel     | SSDSCKKF128G8 SATA | 128 GB | 3       | 49    | 0     | 0.13   |
| KingDian  | S200               | 120 GB | 2       | 49    | 0     | 0.13   |
| Transcend | TSA                | 1 TB   | 1       | 49    | 0     | 0.13   |
| SanDisk   | SDSA5DK 32G        | 32 GB  | 1       | 49    | 0     | 0.13   |
| KingSpec  | P3-512             | 512 GB | 8       | 69    | 226   | 0.13   |
| Samsung   | MZNTY128HDHP-00000 | 128 GB | 2       | 48    | 0     | 0.13   |
| Vaseky    | V800-128G          | 128 GB | 2       | 48    | 0     | 0.13   |
| Crucial   | CT240BX500SSD1     | 240 GB | 43      | 48    | 0     | 0.13   |
| LDLC      | SSD F7 PLUS 3D ... | 240 GB | 1       | 48    | 0     | 0.13   |
| SanDisk   | SD9SN8W128G1002    | 128 GB | 3       | 48    | 0     | 0.13   |
| Intel     | SSDSA2BW160G3H     | 160 GB | 4       | 85    | 2     | 0.13   |
| KingSpec  | NT-256             | 256 GB | 4       | 48    | 0     | 0.13   |
| Micron    | MTFDDAK256MAM-1K12 | 256 GB | 7       | 79    | 722   | 0.13   |
| Kingston  | SUV500M8120G       | 120 GB | 5       | 48    | 0     | 0.13   |
| OCZ       | VECTOR180          | 480 GB | 1       | 48    | 0     | 0.13   |
| SK hynix  | HFS128G32MND-3212A | 128 GB | 1       | 48    | 0     | 0.13   |
| Lite-On   | CV3-DE256          | 256 GB | 3       | 47    | 0     | 0.13   |
| GeIL      | R3 120G            | 120 GB | 1       | 47    | 0     | 0.13   |
| China     | 80GB SSD           | 80 GB  | 2       | 47    | 0     | 0.13   |
| WDC       | WDS240G2G0A-00JH30 | 240 GB | 66      | 59    | 1     | 0.13   |
| AMD       | R3SL120G           | 120 GB | 25      | 46    | 1     | 0.13   |
| SPCC      | M.2 SSD            | 120 GB | 3       | 107   | 2     | 0.13   |
| Plextor   | PX-256M8VG         | 256 GB | 1       | 46    | 0     | 0.13   |
| ADATA     | SU800              | 128 GB | 25      | 48    | 4     | 0.13   |
| Kingston  | SUV500MS120G       | 120 GB | 6       | 46    | 0     | 0.13   |
| AMD       | R3SL60G            | 64 GB  | 3       | 46    | 0     | 0.13   |
| Crucial   | CT128M550SSD1      | 128 GB | 5       | 193   | 25    | 0.13   |
| ADATA     | SP920SS            | 256 GB | 6       | 132   | 8     | 0.13   |
| SanDisk   | SSD PLUS           | 240 GB | 35      | 54    | 1     | 0.13   |
| SanDisk   | SD5SF2032G1010E    | 32 GB  | 1       | 45    | 0     | 0.13   |
| Samsung   | SSD 860 EVO        | 2 TB   | 11      | 45    | 0     | 0.13   |
| Kingston  | RBU-SC152S37128GG2 | 128 GB | 1       | 45    | 0     | 0.12   |
| Samsung   | SSD 860 PRO        | 256 GB | 11      | 45    | 0     | 0.12   |
| WDC       | WDS100T2B0B-00YS70 | 1 TB   | 5       | 45    | 0     | 0.12   |
| Intel     | SSDSC2KW128G8      | 128 GB | 4       | 45    | 0     | 0.12   |
| Kingston  | SA400M8240G        | 240 GB | 7       | 45    | 0     | 0.12   |
| PRETEC    | G2000 SSD          | 32 GB  | 1       | 44    | 0     | 0.12   |
| HP        | SSD S700           | 500 GB | 3       | 43    | 0     | 0.12   |
| Plextor   | PX-512M3           | 512 GB | 1       | 1402  | 31    | 0.12   |
| Transcend | TS64GMSA370        | 64 GB  | 3       | 43    | 0     | 0.12   |
| BIOSTAR   | S100-120GB         | 120 GB | 1       | 43    | 0     | 0.12   |
| Kingston  | RBUSNS8180S3128GI1 | 128 GB | 2       | 43    | 0     | 0.12   |
| KingDian  | S280-240GB         | 240 GB | 7       | 43    | 0     | 0.12   |
| Samsung   | MZMPC128HBFU-000MV | 128 GB | 2       | 43    | 0     | 0.12   |
| China     | SH00R480GB         | 480 GB | 2       | 43    | 0     | 0.12   |
| ADATA     | SU650              | 120 GB | 25      | 45    | 1     | 0.12   |
| China     | SSD128G            | 128 GB | 1       | 42    | 0     | 0.12   |
| Team      | TM8PS7256G         | 256 GB | 3       | 42    | 0     | 0.12   |
| AMD       | R5SL120G           | 120 GB | 9       | 57    | 1     | 0.12   |
| Lite-On   | LMH-256V2M-11 M... | 256 GB | 3       | 42    | 0     | 0.12   |
| Intel     | SSDSC2KG480G8      | 480 GB | 1       | 42    | 0     | 0.12   |
| KingSpec  | NT-64              | 64 GB  | 1       | 41    | 0     | 0.11   |
| Crucial   | CT500MX500SSD4N    | 500 GB | 1       | 41    | 0     | 0.11   |
| Samsung   | MZNLN128HAHQ-000H1 | 128 GB | 14      | 49    | 94    | 0.11   |
| PNY       | SSD2SC240G5SA75... | 240 GB | 1       | 41    | 0     | 0.11   |
| KingDian  | S280               | 1 TB   | 3       | 41    | 0     | 0.11   |
| GALAX     | TA1D0240A          | 240 GB | 1       | 41    | 0     | 0.11   |
| Apacer    | AS350              | 240 GB | 9       | 40    | 0     | 0.11   |
| Apacer    | AS350              | 128 GB | 7       | 40    | 0     | 0.11   |
| Samsung   | Portable SSD T5    | 500 GB | 2       | 40    | 0     | 0.11   |
| Patriot   | Burst              | 480 GB | 11      | 54    | 1     | 0.11   |
| KingDian  | P10                | 240 GB | 1       | 39    | 0     | 0.11   |
| Seagate   | ST480HM000         | 480 GB | 1       | 39    | 0     | 0.11   |
| WDC       | WDS500G2B0A        | 500 GB | 9       | 39    | 0     | 0.11   |
| SanDisk   | SD7SB2Q-512G-1006  | 512 GB | 1       | 39    | 0     | 0.11   |
| Apacer    | AS330              | 120 GB | 2       | 39    | 0     | 0.11   |
| Samsung   | MZ7TY128HDHP-00000 | 128 GB | 1       | 39    | 0     | 0.11   |
| Kingston  | SH103S3480G        | 480 GB | 1       | 38    | 0     | 0.11   |
| DOGFISH   | SSD                | 256 GB | 1       | 38    | 0     | 0.11   |
| Micron    | MTFDDAV256TBN      | 256 GB | 1       | 114   | 2     | 0.10   |
| Samsung   | SSD 860 PRO        | 1 TB   | 4       | 38    | 0     | 0.10   |
| Faspeed   | K5-120G            | 120 GB | 1       | 38    | 0     | 0.10   |
| KingSpec  | T-64               | 64 GB  | 4       | 46    | 2     | 0.10   |
| Crucial   | CT480BX300SSD1     | 480 GB | 3       | 37    | 0     | 0.10   |
| Plextor   | PX-128M6Pro        | 128 GB | 10      | 39    | 1     | 0.10   |
| Transcend | TS64GSSD370S       | 64 GB  | 1       | 37    | 0     | 0.10   |
| Intenso   | SSD Sata III       | 256 GB | 3       | 43    | 1     | 0.10   |
| Corsair   | CSSD-V60GB2        | 64 GB  | 1       | 332   | 8     | 0.10   |
| SanDisk   | SD9SN8W256G1002    | 256 GB | 2       | 36    | 0     | 0.10   |
| SanDisk   | SD6PP4M-256G-1006  | 256 GB | 2       | 36    | 0     | 0.10   |
| Micron    | MTFDDAK512MAY-1... | 512 GB | 1       | 624   | 16    | 0.10   |
| Intel     | SSDSA1M080G2HP     | 80 GB  | 1       | 476   | 12    | 0.10   |
| KingDian  | S280               | 240 GB | 11      | 36    | 0     | 0.10   |
| KingSpec  | P3-128             | 128 GB | 8       | 98    | 20    | 0.10   |
| WDC       | WDS100T2B0B        | 1 TB   | 1       | 36    | 0     | 0.10   |
| Transcend | TS512GMSA370       | 512 GB | 2       | 36    | 0     | 0.10   |
| ADATA     | SP550              | 120 GB | 26      | 36    | 1     | 0.10   |
| PNY       | SSD2SC120G726A1... | 120 GB | 1       | 35    | 0     | 0.10   |
| WDC       | WDS500G2B0B        | 500 GB | 2       | 35    | 0     | 0.10   |
| ADATA     | SU650              | 240 GB | 15      | 45    | 1     | 0.10   |
| Lite-On   | IT LMT-128L9M      | 128 GB | 2       | 35    | 0     | 0.10   |
| Netac     | SSD                | 480 GB | 1       | 35    | 0     | 0.10   |
| Samsung   | MZNLN128HAHQ-00000 | 128 GB | 1       | 35    | 0     | 0.10   |
| Samsung   | MZ7LN128HAHQ-000L2 | 128 GB | 7       | 34    | 0     | 0.10   |
| Plextor   | PX-256S3C          | 256 GB | 1       | 34    | 0     | 0.10   |
| Kingston  | RBUSNS8180DS3128GH | 128 GB | 5       | 34    | 0     | 0.10   |
| Plextor   | PX-64M5M           | 64 GB  | 1       | 34    | 0     | 0.10   |
| Crucial   | FCCT256M4SSD1      | 256 GB | 1       | 34    | 0     | 0.09   |
| ZOTAC     | SATA SSD           | 120 GB | 2       | 34    | 0     | 0.09   |
| Transcend | TS128GSSD370S      | 128 GB | 18      | 34    | 0     | 0.09   |
| ADATA     | SX950              | 240 GB | 1       | 34    | 0     | 0.09   |
| China     | SSD                | 240 GB | 10      | 45    | 1     | 0.09   |
| China     | SSD                | 128 GB | 14      | 34    | 0     | 0.09   |
| Kingston  | SA400M8120G        | 120 GB | 5       | 33    | 0     | 0.09   |
| AMD       | R5S240GBSF         | 240 GB | 1       | 33    | 0     | 0.09   |
| Intel     | SSDSA1MH080G1HP    | 80 GB  | 1       | 33    | 0     | 0.09   |
| RECADATA  | RD-S325MCN-N2563   | 240 GB | 1       | 33    | 0     | 0.09   |
| Crucial   | CT120BX500SSD1     | 120 GB | 51      | 33    | 0     | 0.09   |
| SanDisk   | SD6SB1M-032G-1006  | 32 GB  | 1       | 33    | 0     | 0.09   |
| Transcend | TS240GMTS420S      | 240 GB | 2       | 33    | 0     | 0.09   |
| KingDian  | S280               | 120 GB | 9       | 33    | 0     | 0.09   |
| Smartbuy  | mSata              | 128 GB | 2       | 32    | 0     | 0.09   |
| Samsung   | SSD PM851          | 128 GB | 1       | 32    | 0     | 0.09   |
| SanDisk   | pSSD               | 128 GB | 3       | 32    | 3     | 0.09   |
| KingSpec  | ACSC4M512mSA       | 506 GB | 1       | 32    | 0     | 0.09   |
| OCZ       | VERTEX4            | 80 GB  | 1       | 129   | 3     | 0.09   |
| Samsung   | MZ7LN256HAJQ-000L2 | 256 GB | 6       | 32    | 0     | 0.09   |
| Lite-On   | L8T-128L6G-HP      | 128 GB | 2       | 32    | 640   | 0.09   |
| SanDisk   | SDSSDXP120G        | 120 GB | 1       | 32    | 0     | 0.09   |
| SanDisk   | SDSSDH3500G        | 500 GB | 4       | 32    | 0     | 0.09   |
| Toshiba   | THNSNB062GMCJ      | 64 GB  | 1       | 32    | 0     | 0.09   |
| Samsung   | Portable SSD T5    | 1 TB   | 2       | 31    | 0     | 0.09   |
| Kingmax   | SSD                | 64 GB  | 21      | 219   | 450   | 0.09   |
| LDLC      | SSD                | 480 GB | 2       | 43    | 1     | 0.09   |
| Transcend | TS512GMTS400       | 512 GB | 1       | 31    | 0     | 0.09   |
| SanDisk   | SDSSDH3 1T00       | 1 TB   | 3       | 31    | 0     | 0.09   |
| ADATA     | SU900              | 1 TB   | 3       | 33    | 1     | 0.09   |
| OCZ       | TRION150           | 480 GB | 1       | 31    | 0     | 0.09   |
| KingSpec  | KSD-SA25.7-016MJ   | 16 GB  | 2       | 30    | 0     | 0.08   |
| SanDisk   | SSD i100           | 32 GB  | 2       | 30    | 0     | 0.08   |
| ADATA     | SP900NS34          | 128 GB | 1       | 30    | 0     | 0.08   |
| Hajaan    | SSD 256G           | 256 GB | 1       | 30    | 0     | 0.08   |
| Samsung   | MZ7LN256HAJQ-00000 | 256 GB | 1       | 30    | 0     | 0.08   |
| PNY       | SSD2SC120G1CS17... | 120 GB | 2       | 30    | 0     | 0.08   |
| Micron    | MTFDDAV512MBF-1... | 512 GB | 2       | 30    | 0     | 0.08   |
| ADATA     | SU630              | 240 GB | 5       | 30    | 0     | 0.08   |
| Transcend | TS256GMTS430S      | 256 GB | 5       | 30    | 0     | 0.08   |
| SK hynix  | HFS128G39MNC-3510A | 128 GB | 1       | 30    | 0     | 0.08   |
| Apacer    | AS350              | 512 GB | 4       | 45    | 1     | 0.08   |
| SanDisk   | SDSA5DK-016G-1006  | 16 GB  | 1       | 29    | 0     | 0.08   |
| KingPower | 1108 SSD           | 64 GB  | 1       | 29    | 0     | 0.08   |
| Kingston  | SUV500M8480G       | 480 GB | 1       | 29    | 0     | 0.08   |
| Samsung   | SSD Thin uSATA ... | 128 GB | 1       | 378   | 12    | 0.08   |
| Super ... | FTM50N325H         | 500 GB | 1       | 29    | 0     | 0.08   |
| KingSpec  | MT-128             | 128 GB | 4       | 29    | 0     | 0.08   |
| Samsung   | MZNLN256HAJQ-000L7 | 256 GB | 4       | 29    | 0     | 0.08   |
| ADATA     | SU635              | 240 GB | 3       | 28    | 0     | 0.08   |
| Patriot   | Spark              | 256 GB | 2       | 28    | 0     | 0.08   |
| Mushkin   | MKNSSDCR60GB-7     | 64 GB  | 1       | 142   | 4     | 0.08   |
| Toshiba   | THNSNF256GMCS      | 256 GB | 1       | 28    | 0     | 0.08   |
| WDC       | WDBNCE5000PNC      | 500 GB | 3       | 27    | 0     | 0.08   |
| TAISU     | SSD 240G           | 240 GB | 1       | 27    | 0     | 0.08   |
| Phison    | SATA SSD           | 960 GB | 2       | 27    | 0     | 0.08   |
| SPCC      | SSD                | 1 TB   | 4       | 27    | 0     | 0.08   |
| Samsung   | MZ7TY128HDHP-000L1 | 128 GB | 2       | 27    | 0     | 0.08   |
| SenDisk   | C3-60G             | 64 GB  | 1       | 27    | 0     | 0.08   |
| SanDisk   | SSD U100           | 16 GB  | 5       | 27    | 0     | 0.08   |
| Lenovo    | Thinklife SSD S... | 480 GB | 1       | 27    | 0     | 0.07   |
| KingSpec  | CHA-M2B7-M256      | 256 GB | 2       | 27    | 0     | 0.07   |
| HECTRON   | HECX1-240G         | 240 GB | 1       | 26    | 0     | 0.07   |
| Transcend | TS64GSSD720        | 64 GB  | 1       | 26    | 0     | 0.07   |
| Transcend | TS64GSSD320        | 64 GB  | 1       | 26    | 0     | 0.07   |
| Kingston  | RBUSNS8180DS3512GJ | 512 GB | 3       | 26    | 0     | 0.07   |
| Lite-On   | LMH-512V2M-11 M... | 512 GB | 1       | 26    | 0     | 0.07   |
| Intel     | SSDSC2BB240G7      | 240 GB | 2       | 25    | 0     | 0.07   |
| WDC       | WDS250G2B0A        | 250 GB | 2       | 25    | 0     | 0.07   |
| Lite-On   | LCH-256V2S         | 256 GB | 1       | 25    | 0     | 0.07   |
| KingSpec  | T-120              | 120 GB | 1       | 25    | 0     | 0.07   |
| SK hynix  | HFS512G39TNF-N3A0A | 512 GB | 1       | 25    | 0     | 0.07   |
| Toshiba   | THNSNH128G8NT      | 128 GB | 1       | 25    | 0     | 0.07   |
| Plextor   | PX-512M5Pro        | 512 GB | 1       | 25    | 0     | 0.07   |
| SK hynix  | HFS256G32MND-2900A | 256 GB | 1       | 531   | 20    | 0.07   |
| China     | 512GB SSD          | 512 GB | 1       | 25    | 0     | 0.07   |
| SanDisk   | SD8SN8U-512G-1006  | 512 GB | 1       | 125   | 4     | 0.07   |
| Lite-On   | CV5-8Q256          | 256 GB | 1       | 24    | 0     | 0.07   |
| Corsair   | CSSD-V32GB2        | 32 GB  | 1       | 99    | 3     | 0.07   |
| Intel     | SSDSC2KF256H6L     | 256 GB | 3       | 123   | 11    | 0.07   |
| Plextor   | PX-128S2C          | 128 GB | 2       | 24    | 0     | 0.07   |
| Lite-On   | L8H-256V2G         | 256 GB | 1       | 24    | 0     | 0.07   |
| Seagate   | BarraCuda SSD Z... | 1 TB   | 3       | 23    | 0     | 0.07   |
| PNY       | SSD2SC120G1SA75... | 120 GB | 1       | 23    | 0     | 0.07   |
| KingSpec  | Q-360              | 360 GB | 3       | 23    | 0     | 0.07   |
| SK hynix  | HFS256G32TNH-73A0A | 256 GB | 3       | 23    | 0     | 0.06   |
| ADATA     | SU750              | 256 GB | 1       | 23    | 0     | 0.06   |
| LDLC      | SSD                | 128 GB | 4       | 23    | 0     | 0.06   |
| Verbatim  | Vi500 S3 240GB SSD | 240 GB | 1       | 23    | 0     | 0.06   |
| addlink   | SATA SSD           | 1 TB   | 1       | 23    | 0     | 0.06   |
| Transcend | TS32GSSD370S       | 32 GB  | 7       | 23    | 0     | 0.06   |
| GLOWAY    | FER240GS3-S7       | 240 GB | 1       | 23    | 0     | 0.06   |
| TCSUNBOW  | N4                 | 240 GB | 1       | 22    | 0     | 0.06   |
| Goodram   | IRP-SSDPR-S25C-512 | 512 GB | 1       | 22    | 0     | 0.06   |
| Plextor   | PX-128S1G          | 128 GB | 1       | 22    | 0     | 0.06   |
| Intel     | SSDSC2KI128G8      | 128 GB | 1       | 22    | 0     | 0.06   |
| Toshiba   | THNSNS060GBSP      | 64 GB  | 1       | 22    | 0     | 0.06   |
| Plextor   | PX-128M6V          | 128 GB | 1       | 22    | 0     | 0.06   |
| Hoodisk   | SSD                | 128 GB | 1       | 22    | 0     | 0.06   |
| Kingston  | SKC300S37A180G     | 180 GB | 2       | 166   | 1025  | 0.06   |
| Foxline   | FLSSD480X5SE       | 480 GB | 1       | 22    | 0     | 0.06   |
| Transcend | TS128GMSA370       | 128 GB | 2       | 21    | 0     | 0.06   |
| Plextor   | PX-256M6M          | 256 GB | 3       | 29    | 1     | 0.06   |
| Maximus   | SSD                | 128 GB | 1       | 21    | 0     | 0.06   |
| OCZ       | INTREPID 3600      | 400 GB | 1       | 21    | 0     | 0.06   |
| ADATA     | SU800              | 2 TB   | 1       | 21    | 0     | 0.06   |
| Crucial   | CT250MX500SSD4     | 250 GB | 1       | 21    | 0     | 0.06   |
| Intel     | SSDSCKKF256H6 SATA | 256 GB | 1       | 21    | 0     | 0.06   |
| Lite-On   | LSS-24L6G          | 24 GB  | 1       | 21    | 0     | 0.06   |
| China     | SSD                | 1 TB   | 1       | 21    | 0     | 0.06   |
| ADATA     | SU800NS38          | 256 GB | 4       | 30    | 288   | 0.06   |
| Crucial   | CT1050MX300SSD4    | 1 TB   | 3       | 52    | 25    | 0.06   |
| Goldkey   | GKH84-256GB        | 256 GB | 1       | 20    | 0     | 0.06   |
| Apacer    | AS350              | 120 GB | 8       | 20    | 1     | 0.06   |
| Lenovo    | SSD SL700 480G     | 480 GB | 1       | 20    | 0     | 0.06   |
| Plextor   | PX-256M8VC         | 256 GB | 2       | 20    | 0     | 0.06   |
| AMD       | R3SL240G           | 240 GB | 4       | 44    | 1     | 0.06   |
| XUNZHE    | XUNZHE800S 120G    | 120 GB | 1       | 20    | 0     | 0.05   |
| Netac     | SSD 120G           | 120 GB | 1       | 19    | 0     | 0.05   |
| Transcend | TS128GSSD230S      | 128 GB | 9       | 19    | 0     | 0.05   |
| Transcend | TS128GMTS800       | 128 GB | 3       | 19    | 0     | 0.05   |
| Intel     | SSDSCKGF256A5 SATA | 256 GB | 1       | 19    | 0     | 0.05   |
| Kingston  | RBU-SNS8152S325... | 256 GB | 1       | 18    | 0     | 0.05   |
| KingSpec  | P4-240             | 240 GB | 6       | 22    | 1     | 0.05   |
| Lite-On   | CV1-8B256-HP       | 256 GB | 1       | 18    | 0     | 0.05   |
| Corsair   | Neutron SSD        | 240 GB | 1       | 2126  | 114   | 0.05   |
| Lite-On   | CV1-8B128          | 128 GB | 4       | 18    | 0     | 0.05   |
| China     | SSD                | 512 GB | 2       | 18    | 0     | 0.05   |
| ADATA     | SP610              | 256 GB | 1       | 18    | 0     | 0.05   |
| Hyperdisk | SDOM               | 16 GB  | 1       | 18    | 0     | 0.05   |
| FORESEE   | 128GB SSD          | 128 GB | 8       | 17    | 0     | 0.05   |
| WDC       | WDS480G2G0A-00JH30 | 480 GB | 10      | 17    | 0     | 0.05   |
| SanDisk   | SSD U100           | 64 GB  | 6       | 19    | 1     | 0.05   |
| SanDisk   | SD8SN8U1T001122    | 1 TB   | 1       | 17    | 0     | 0.05   |
| WDC       | WDS480G2G0B-00EPW0 | 480 GB | 3       | 17    | 0     | 0.05   |
| Team      | TM8PS5256G         | 256 GB | 1       | 17    | 0     | 0.05   |
| China     | 60GB SSD           | 64 GB  | 1       | 17    | 0     | 0.05   |
| Kingston  | RBUSNS8180DS3128GJ | 128 GB | 4       | 17    | 0     | 0.05   |
| China     | RTMMB256VBV4KFY    | 256 GB | 1       | 17    | 0     | 0.05   |
| OWC       | Neptune 6G SSD     | 480 GB | 1       | 17    | 0     | 0.05   |
| Kingrich  | 64GB K9 SATA3 SSD  | 64 GB  | 2       | 17    | 0     | 0.05   |
| SanDisk   | SD8SBAT128G1122    | 128 GB | 3       | 17    | 0     | 0.05   |
| SanDisk   | Z400s M.2 2280     | 128 GB | 1       | 17    | 0     | 0.05   |
| AMD       | R3S60GBSM          | 64 GB  | 2       | 17    | 0     | 0.05   |
| LDNDISK   | SSD                | 240 GB | 1       | 16    | 0     | 0.05   |
| ADATA     | SP550              | 480 GB | 1       | 16    | 0     | 0.05   |
| Crucial   | CT128MX100SSD1     | 128 GB | 2       | 281   | 16    | 0.05   |
| Intel     | SSDSA1M160G2HP     | 160 GB | 6       | 102   | 14    | 0.05   |
| Platinet  | SSD                | 120 GB | 1       | 16    | 0     | 0.04   |
| AEGO      | SSD                | 240 GB | 3       | 16    | 0     | 0.04   |
| Intel     | SSDSA2M080G2GN     | 80 GB  | 1       | 245   | 14    | 0.04   |
| Intel     | SSDMCEAW080A4      | 80 GB  | 1       | 16    | 0     | 0.04   |
| Apple     | SSD SM256E         | 256 GB | 1       | 15    | 0     | 0.04   |
| FASTDISK  | FASTDISK120G       | 120 GB | 1       | 15    | 0     | 0.04   |
| GLOWAY    | FER120GS3-S7       | 120 GB | 2       | 15    | 0     | 0.04   |
| SanDisk   | SD8SNAT128G1122    | 128 GB | 1       | 15    | 0     | 0.04   |
| Transcend | TS120GMTS420S      | 120 GB | 6       | 20    | 1     | 0.04   |
| Lexar     | 512GB SSD          | 512 GB | 1       | 15    | 0     | 0.04   |
| Patriot   | P200               | 1 TB   | 1       | 15    | 0     | 0.04   |
| China     | SSD                | 64 GB  | 2       | 15    | 0     | 0.04   |
| FORESEE   | 240GB SSD          | 240 GB | 1       | 15    | 0     | 0.04   |
| Lite-On   | CV8-8E256          | 256 GB | 3       | 15    | 0     | 0.04   |
| Transcend | TS64GSSD25S-M      | 64 GB  | 2       | 15    | 0     | 0.04   |
| T-FORCE   | SSD                | 1 TB   | 1       | 15    | 0     | 0.04   |
| e2e4      | SSD                | 120 GB | 3       | 15    | 0     | 0.04   |
| Lite-On   | CV1-SB128          | 128 GB | 1       | 15    | 0     | 0.04   |
| SPCC      | SSD                | 480 GB | 1       | 15    | 0     | 0.04   |
| FASTDISK  | SSD 60G            | 64 GB  | 1       | 14    | 0     | 0.04   |
| Lite-On   | LSS-32L6G-HP       | 32 GB  | 2       | 14    | 0     | 0.04   |
| China     | SSD                | 480 GB | 4       | 14    | 0     | 0.04   |
| Toshiba   | KSG60ZMV256G M.... | 256 GB | 4       | 23    | 25    | 0.04   |
| Samsung   | MZNLN128HAHQ-000L1 | 128 GB | 1       | 14    | 0     | 0.04   |
| Lenovo    | SSD SL700 M.2 128G | 128 GB | 1       | 14    | 0     | 0.04   |
| Transcend | TS512GMTS430S      | 512 GB | 4       | 14    | 0     | 0.04   |
| Seagate   | ST480FP0021        | 480 GB | 1       | 14    | 0     | 0.04   |
| Crucial   | CT2000MX500SSD1N   | 2 TB   | 1       | 14    | 0     | 0.04   |
| SK hynix  | SH920 mSATA        | 128 GB | 2       | 108   | 17    | 0.04   |
| Intel     | SSDSCKKW128G8      | 128 GB | 2       | 14    | 0     | 0.04   |
| Apple     | SSD TS128E         | 121 GB | 2       | 99    | 6     | 0.04   |
| Micron    | MTFDDAK256MAY-1... | 256 GB | 1       | 238   | 16    | 0.04   |
| Micron    | MTFDDAK240TCB      | 240 GB | 1       | 14    | 0     | 0.04   |
| Kingston  | RBUSNS8180DS3256GH | 256 GB | 1       | 41    | 2     | 0.04   |
| Smartbuy  | m.2 S11-2280       | 256 GB | 1       | 13    | 0     | 0.04   |
| OCZ       | VECTOR180          | 960 GB | 1       | 13    | 0     | 0.04   |
| Drevo     | X1 SSD             | 120 GB | 3       | 274   | 23    | 0.04   |
| FORESEE   | 64GB SSD           | 64 GB  | 2       | 13    | 0     | 0.04   |
| Plextor   | PX-128M6S+         | 128 GB | 1       | 13    | 0     | 0.04   |
| KingSpec  | P3-256             | 256 GB | 2       | 13    | 0     | 0.04   |
| Team      | T253X1480G         | 480 GB | 1       | 13    | 0     | 0.04   |
| Transcend | TS128GMTS600       | 128 GB | 1       | 13    | 0     | 0.04   |
| TCSUNBOW  | X3                 | 120 GB | 1       | 13    | 0     | 0.04   |
| SK hynix  | SH920 mSATA        | 256 GB | 1       | 680   | 52    | 0.04   |
| Samsung   | MZ7LH240HAHQ-00005 | 240 GB | 2       | 12    | 0     | 0.03   |
| Zheino    | CHN 25SATA01M 030  | 32 GB  | 1       | 12    | 0     | 0.03   |
| Super ... | FTM28N325H         | 128 GB | 1       | 12    | 0     | 0.03   |
| SanDisk   | SDSSDH3 512G       | 512 GB | 1       | 12    | 0     | 0.03   |
| Seagate   | BarraCuda SSD Z... | 500 GB | 3       | 12    | 0     | 0.03   |
| Transcend | TS128GSSD360S      | 128 GB | 8       | 12    | 0     | 0.03   |
| Samsung   | MZ7PA128HMCD-010H1 | 128 GB | 1       | 12    | 0     | 0.03   |
| PNY       | CS900 500GB SSD    | 500 GB | 1       | 12    | 0     | 0.03   |
| SanDisk   | SD9SN8W512G1122    | 512 GB | 1       | 12    | 0     | 0.03   |
| Goodram   | SSDPR-CL100-120-G2 | 120 GB | 2       | 11    | 0     | 0.03   |
| KingSpec  | P3-64              | 64 GB  | 1       | 11    | 0     | 0.03   |
| SanDisk   | SD8SNAT256G1002    | 256 GB | 3       | 11    | 0     | 0.03   |
| China     | SATA SSD           | 512 GB | 1       | 11    | 0     | 0.03   |
| ADATA     | IM2S3138E-128GM-B  | 128 GB | 1       | 11    | 0     | 0.03   |
| Crucial   | V4-CT128V4SSD2     | 128 GB | 1       | 11    | 0     | 0.03   |
| Faspeed   | M3-360G            | 360 GB | 1       | 11    | 0     | 0.03   |
| Crucial   | CT480BX200SSD1     | 480 GB | 2       | 11    | 0     | 0.03   |
| Micron    | M600_MTFDDAV512MBF | 512 GB | 1       | 11    | 0     | 0.03   |
| SanDisk   | SSD PLUS 480 GB    | 480 GB | 1       | 32    | 2     | 0.03   |
| ADATA     | SSD S511           | 240 GB | 1       | 10    | 0     | 0.03   |
| Pioneer   | APS-SL3N-240       | 240 GB | 1       | 10    | 0     | 0.03   |
| Transcend | TS32GSSD25S-M      | 32 GB  | 1       | 10    | 0     | 0.03   |
| Intel     | SSDSCKKW240H6      | 240 GB | 3       | 18    | 1     | 0.03   |
| Golden... | GDSA25-120MS       | 120 GB | 1       | 10    | 0     | 0.03   |
| Kingston  | SM2280S3G2480G     | 480 GB | 1       | 10    | 0     | 0.03   |
| SanDisk   | SD8SBAT-256G-1006  | 256 GB | 1       | 10    | 0     | 0.03   |
| ADATA     | SX300              | 128 GB | 1       | 10    | 0     | 0.03   |
| Transcend | TS512GSSD370       | 512 GB | 1       | 10    | 0     | 0.03   |
| SPCC      | SPCCSolidStateDisk | 512 GB | 1       | 10    | 0     | 0.03   |
| Lite-On   | LCH-256V2S-11 2... | 256 GB | 1       | 10    | 0     | 0.03   |
| Mushkin   | MKNSSDTR240GB      | 240 GB | 1       | 10    | 0     | 0.03   |
| Intel     | SSDSA2CW160G3      | 160 GB | 1       | 10    | 0     | 0.03   |
| BIWIN     | SSD                | 512 GB | 3       | 9     | 0     | 0.03   |
| Toshiba   | TL100              | 240 GB | 2       | 9     | 0     | 0.03   |
| Lite-On   | CV1-8B512-HP       | 512 GB | 1       | 9     | 0     | 0.03   |
| SPCC      | SSD162             | 240 GB | 1       | 203   | 20    | 0.03   |
| QUMO      | SSD                | 120 GB | 3       | 202   | 339   | 0.03   |
| Ramsta    | SSD R800           | 120 GB | 1       | 9     | 0     | 0.03   |
| Corsair   | Neutron GTX SSD    | 120 GB | 2       | 1417  | 147   | 0.03   |
| KingSpec  | NT-1TB             | 1 TB   | 2       | 9     | 0     | 0.03   |
| Faspeed   | H5-120G PLUS       | 120 GB | 1       | 9     | 0     | 0.03   |
| HP        | SSD S600           | 120 GB | 1       | 9     | 0     | 0.03   |
| KingSpec  | ACSC2M064mSA       | 64 GB  | 1       | 9     | 0     | 0.03   |
| ADATA     | SU900              | 128 GB | 1       | 9     | 0     | 0.02   |
| Kingston  | v300 240G          | 240 GB | 1       | 9     | 0     | 0.02   |
| Intel     | SSDMCEAW180A4      | 180 GB | 1       | 9     | 0     | 0.02   |
| SK hynix  | HFS128G3BTND-N210A | 128 GB | 1       | 9     | 0     | 0.02   |
| SanDisk   | SSD P4             | 32 GB  | 13      | 109   | 254   | 0.02   |
| SanDisk   | SD8SMAT-128G-1006  | 128 GB | 1       | 9     | 0     | 0.02   |
| SanDisk   | SD8SNAT-256G-1006  | 256 GB | 2       | 8     | 0     | 0.02   |
| Londisk   | SSD                | 240 GB | 1       | 8     | 0     | 0.02   |
| Micron    | MTFDDAK128MAY-1... | 128 GB | 1       | 151   | 16    | 0.02   |
| Teclast   | 128GB MS550        | 128 GB | 1       | 8     | 0     | 0.02   |
| SanDisk   | iSSD P4            | 16 GB  | 1       | 238   | 26    | 0.02   |
| Integral  | V Series SATA SSD  | 240 GB | 2       | 8     | 0     | 0.02   |
| KingDian  | N400 60G           | 64 GB  | 1       | 8     | 0     | 0.02   |
| SanDisk   | SD7SN6S-128G-1006  | 128 GB | 1       | 8     | 0     | 0.02   |
| Londisk   | SSD                | 480 GB | 1       | 8     | 0     | 0.02   |
| Kingston  | RBU-SNS8100S312... | 128 GB | 2       | 8     | 0     | 0.02   |
| SanDisk   | SDSSDH3 500G       | 500 GB | 5       | 8     | 0     | 0.02   |
| Mushkin   | MKNSSDRW1TB        | 1 TB   | 1       | 8     | 0     | 0.02   |
| Intel     | SSDSCKJF240A5L     | 240 GB | 1       | 79    | 9     | 0.02   |
| PNY       | SSD2SC256GM1P3D... | 256 GB | 1       | 7     | 0     | 0.02   |
| KingDian  | S200               | 64 GB  | 4       | 7     | 0     | 0.02   |
| SanDisk   | SD8SNAT256G1122    | 256 GB | 2       | 7     | 0     | 0.02   |
| Lite-On   | CV1-8B256          | 256 GB | 3       | 7     | 0     | 0.02   |
| FASTDISK  | SSD 120G           | 120 GB | 1       | 7     | 0     | 0.02   |
| T-FORCE   | SSD                | 250 GB | 1       | 7     | 0     | 0.02   |
| Transcend | TS64GSSD370        | 64 GB  | 2       | 7     | 0     | 0.02   |
| China     | SSD60G             | 64 GB  | 2       | 7     | 0     | 0.02   |
| KingFast  | SSD                | 120 GB | 5       | 18    | 614   | 0.02   |
| Apacer    | AST280             | 240 GB | 1       | 7     | 0     | 0.02   |
| SanDisk   | SD8SNAT128G1002    | 128 GB | 3       | 7     | 0     | 0.02   |
| Zheino    | CHN 25SATA01M 060  | 64 GB  | 1       | 7     | 0     | 0.02   |
| Transcend | TS240GMTS820S      | 240 GB | 2       | 7     | 0     | 0.02   |
| KingSpec  | T-60               | 64 GB  | 3       | 7     | 0     | 0.02   |
| KingSpec  | ACSC2M128mSA       | 128 GB | 1       | 7     | 0     | 0.02   |
| Toshiba   | THNSNS128GMCP      | 128 GB | 1       | 7     | 0     | 0.02   |
| KingSpec  | Q-720              | 720 GB | 2       | 7     | 0     | 0.02   |
| FASTDISK  | SSD 30G            | 32 GB  | 1       | 7     | 0     | 0.02   |
| Kingston  | HyperX Fury 3D     | 120 GB | 2       | 7     | 0     | 0.02   |
| SK hynix  | SC401 SATA         | 256 GB | 2       | 7     | 0     | 0.02   |
| Dell      | WR202KD032G E70... | 32 GB  | 2       | 6     | 0     | 0.02   |
| BHT       | WR202I0064G E70... | 64 GB  | 2       | 6     | 0     | 0.02   |
| KingSpec  | P3-1TB             | 1 TB   | 1       | 6     | 0     | 0.02   |
| Kingston  | SV300S37A 120G     | 120 GB | 1       | 6     | 0     | 0.02   |
| Kingston  | RBUSC180DS37128GJ  | 128 GB | 2       | 6     | 0     | 0.02   |
| Intel     | SSDSCKJW180H6      | 180 GB | 1       | 6     | 0     | 0.02   |
| Toshiba   | KSG60ZMV512G M.... | 512 GB | 1       | 6     | 0     | 0.02   |
| Patriot   | Ignite             | 240 GB | 1       | 6     | 0     | 0.02   |
| SanDisk   | SD8SBAT256G1122    | 256 GB | 3       | 6     | 0     | 0.02   |
| Kingston  | SA400S37 240G      | 240 GB | 1       | 6     | 0     | 0.02   |
| Samsung   | SSD PM871b 2.5 7mm | 128 GB | 1       | 6     | 0     | 0.02   |
| ADATA     | SX850              | 256 GB | 1       | 6     | 0     | 0.02   |
| Lite-On   | CV5-8Q512-HP       | 512 GB | 1       | 6     | 0     | 0.02   |
| Toshiba   | A100               | 120 GB | 2       | 6     | 0     | 0.02   |
| SK hynix  | SC210 mSATA        | 256 GB | 2       | 195   | 28    | 0.02   |
| Goodram   | SSDPR_CX300_120    | 120 GB | 1       | 6     | 0     | 0.02   |
| SK hynix  | HFS128G32TNF-N3A0A | 128 GB | 1       | 6     | 0     | 0.02   |
| China     | SSD 128G           | 128 GB | 2       | 6     | 0     | 0.02   |
| Lite-On   | L8H-256V2G-11 M... | 256 GB | 1       | 6     | 0     | 0.02   |
| KingSpec  | KSQ120             | 120 GB | 1       | 6     | 0     | 0.02   |
| Smartbuy  | SSD                | 240 GB | 1       | 6     | 0     | 0.02   |
| Teclast   | 256GB NS550-2242   | 256 GB | 2       | 6     | 0     | 0.02   |
| KingDian  | S280-120GB         | 120 GB | 3       | 38    | 641   | 0.02   |
| GeIL      | Zenith A3-PRO      | 240 GB | 1       | 6     | 0     | 0.02   |
| GeIL      | Zenith A3          | 120 GB | 1       | 6     | 0     | 0.02   |
| Union ... | RTOTJ128VGD2EYX    | 128 GB | 1       | 6     | 0     | 0.02   |
| Intel     | SSDSCKGW180A4      | 180 GB | 1       | 286   | 47    | 0.02   |
| Plextor   | PX-G256M6e         | 256 GB | 1       | 5     | 0     | 0.02   |
| HP        | SSD S700 Pro       | 256 GB | 1       | 5     | 0     | 0.02   |
| V-GeN     | V-GEN10SM19AR12... | 120 GB | 1       | 5     | 0     | 0.02   |
| ADATA     | SU650NS38          | 240 GB | 1       | 5     | 0     | 0.02   |
| Dell      | WR202KD128G E70... | 128 GB | 1       | 5     | 0     | 0.02   |
| Kingston  | SKC600256G         | 256 GB | 1       | 5     | 0     | 0.02   |
| Kingston  | SKC600512G         | 512 GB | 1       | 5     | 0     | 0.02   |
| SK hynix  | HFS256G39TNF-N3A0A | 256 GB | 2       | 5     | 0     | 0.02   |
| BIWIN     | G2242              | 64 GB  | 1       | 5     | 0     | 0.01   |
| Netac     | SSD                | 256 GB | 3       | 5     | 0     | 0.01   |
| China     | SSD                | 360 GB | 4       | 5     | 0     | 0.01   |
| Intel     | SSDSC2BF180A5H SED | 180 GB | 1       | 204   | 39    | 0.01   |
| MicroData | MD500 120G         | 120 GB | 1       | 5     | 0     | 0.01   |
| Teclast   | 512GB A850         | 512 GB | 1       | 5     | 0     | 0.01   |
| Mushkin   | MKNSSDCG480GB      | 480 GB | 2       | 116   | 508   | 0.01   |
| Smartbuy  | m.2 S11-2280       | 128 GB | 1       | 4     | 0     | 0.01   |
| TAMMUZ    | SSD                | 120 GB | 1       | 4     | 0     | 0.01   |
| KingSpec  | ACSC2M128S25       | 128 GB | 1       | 4     | 0     | 0.01   |
| GeIL      | ZENITH R3_120GB    | 120 GB | 2       | 4     | 0     | 0.01   |
| PNY       | SSD2SC480G1CS17... | 480 GB | 1       | 4     | 0     | 0.01   |
| Maximus   | SSD 256G           | 256 GB | 1       | 4     | 0     | 0.01   |
| Lite-On   | LMS-32L6M-HP       | 32 GB  | 1       | 4     | 0     | 0.01   |
| Kingston  | SA400S37           | 240 GB | 1       | 4     | 0     | 0.01   |
| Apacer    | AS340              | 480 GB | 2       | 4     | 0     | 0.01   |
| PHINOCOM  | SSD                | 120 GB | 1       | 4     | 0     | 0.01   |
| Corsair   | Neutron GTX SSD    | 128 GB | 1       | 1173  | 291   | 0.01   |
| GeIL      | ZENITH-A3 120G     | 120 GB | 1       | 3     | 0     | 0.01   |
| Zheino    | CHN-25SATAA3-360   | 360 GB | 1       | 87    | 21    | 0.01   |
| Team      | TM8PS7512G         | 512 GB | 1       | 3     | 0     | 0.01   |
| Fujitsu   | F500S              | 1 TB   | 1       | 3     | 0     | 0.01   |
| Intel     | SSDSA1M080G2LE     | 80 GB  | 1       | 121   | 31    | 0.01   |
| SanDisk   | SATAIII            | 16 GB  | 1       | 3     | 0     | 0.01   |
| Transcend | TS256GMTS400S      | 256 GB | 1       | 3     | 0     | 0.01   |
| KingSpec  | ACJC2M032mSH       | 32 GB  | 1       | 3     | 0     | 0.01   |
| KingSpec  | MT-256             | 256 GB | 3       | 3     | 0     | 0.01   |
| KingDian  | S200               | 240 GB | 1       | 3     | 0     | 0.01   |
| Intenso   | SSD SATAIII        | 240 GB | 2       | 3     | 0     | 0.01   |
| Intel     | SSDMAEXC024G3H     | 24 GB  | 1       | 112   | 30    | 0.01   |
| HP        | SSD S700           | 1 TB   | 1       | 3     | 0     | 0.01   |
| HPE       | MK000960GWJPP      | 960 GB | 1       | 3     | 0     | 0.01   |
| Lite-On   | IT L8H-64V2G       | 64 GB  | 1       | 3     | 0     | 0.01   |
| Micron    | 1300 SATA          | 256 GB | 1       | 3     | 0     | 0.01   |
| Samsung   | MZNLN256HAJQ-00007 | 256 GB | 1       | 3     | 0     | 0.01   |
| OCZ       | REVODRIVE X2       | 64 GB  | 4       | 1204  | 516   | 0.01   |
| SPCC      | SSDB27             | 32 GB  | 1       | 23    | 6     | 0.01   |
| ShineDisk | M667 128G          | 120 GB | 1       | 3     | 0     | 0.01   |
| i-Flas... | K8                 | 64 GB  | 1       | 3     | 0     | 0.01   |
| WDC       | WDS100T2G0A-00JH30 | 1 TB   | 1       | 3     | 0     | 0.01   |
| Samsung   | SSD 860 QVO        | 4 TB   | 2       | 3     | 0     | 0.01   |
| Micron    | MTFDDAV256TBN-1... | 256 GB | 2       | 3     | 0     | 0.01   |
| SanDisk   | SD7SB3Q128G1001    | 128 GB | 1       | 302   | 100   | 0.01   |
| Team      | T253X2001T         | 1 TB   | 1       | 2     | 0     | 0.01   |
| Goodram   | IR_SSDPR_S25A_120  | 120 GB | 1       | 2     | 0     | 0.01   |
| SanDisk   | SD9SB8W256G1102    | 256 GB | 1       | 2     | 0     | 0.01   |
| Dell      | WR202KD032G E70... | 32 GB  | 2       | 2     | 0     | 0.01   |
| SanDisk   | SSD i110           | 128 GB | 1       | 2     | 0     | 0.01   |
| Samsung   | MZNLH512HALU-00000 | 512 GB | 1       | 2     | 0     | 0.01   |
| Fordisk   | SATA SSD           | 120 GB | 1       | 2     | 0     | 0.01   |
| Kingch... | SSD                | 64 GB  | 1       | 2     | 0     | 0.01   |
| KingSpec  | NT-512             | 512 GB | 1       | 24    | 8     | 0.01   |
| Patriot   | Wildfire           | 120 GB | 1       | 2712  | 1022  | 0.01   |
| SanDisk   | SD7UB3Q256G1001    | 256 GB | 2       | 265   | 100   | 0.01   |
| Samsung   | MZNLN512HCJH-000H1 | 512 GB | 1       | 2     | 0     | 0.01   |
| SanDisk   | SDSA5GK-016G-1006  | 16 GB  | 1       | 276   | 106   | 0.01   |
| Gigastone | SS6200-256GB       | 256 GB | 1       | 2     | 0     | 0.01   |
| Goodram   | SSDPR-CL100-240-G2 | 240 GB | 1       | 2     | 0     | 0.01   |
| SanDisk   | SD7SB2Q512G1001    | 512 GB | 2       | 246   | 100   | 0.01   |
| Micron    | 1100_MTFDDAK1T0TBN | 1 TB   | 3       | 2     | 0     | 0.01   |
| SOLIDATA  | SSD                | 120 GB | 1       | 2420  | 1019  | 0.01   |
| Micron    | 1300_MTFDDAK512TDL | 512 GB | 1       | 2     | 0     | 0.01   |
| Seagate   | ZA1920NM10001      | 1.9 TB | 2       | 2     | 0     | 0.01   |
| Intel     | SSDSC2KW240H6      | 240 GB | 2       | 14    | 6     | 0.01   |
| SanDisk   | SSD i110           | 16 GB  | 2       | 2     | 0     | 0.01   |
| SanDisk   | SSD i110           | 24 GB  | 1       | 2     | 0     | 0.01   |
| Transcend | TS64GMTS800        | 64 GB  | 1       | 2     | 0     | 0.01   |
| Intel     | SSDSCKKF240H6L     | 240 GB | 1       | 47    | 20    | 0.01   |
| China     | SSD                | 256 GB | 2       | 2     | 0     | 0.01   |
| OCZ       | VERTEX3 LP         | 240 GB | 1       | 2268  | 1019  | 0.01   |
| Netac     | SSD                | 128 GB | 3       | 2     | 0     | 0.01   |
| ACPI      | M2SCF-6M           | 64 GB  | 1       | 2     | 0     | 0.01   |
| Zheino    | CHN25SATAS1 032    | 32 GB  | 2       | 2     | 0     | 0.01   |
| SK hynix  | SH920 2.5 7MM      | 128 GB | 1       | 54    | 25    | 0.01   |
| Seagate   | BarraCuda SSD Z... | 2 TB   | 1       | 2     | 0     | 0.01   |
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
| Drevo     | X1 pro             | 1 TB   | 1       | 33    | 18    | 0.00   |
| OCZ       | VERTEX2            | 100 GB | 1       | 1     | 0     | 0.00   |
| SanDisk   | SDSSDH3256G        | 256 GB | 1       | 1     | 0     | 0.00   |
| Toshiba   | THNSNK256GVN8 M... | 256 GB | 3       | 169   | 100   | 0.00   |
| Intel     | SSDSCKKW010X6      | 1 TB   | 1       | 1     | 0     | 0.00   |
| KingSpec  | ACJC2M064S25       | 64 GB  | 1       | 1     | 0     | 0.00   |
| Micron    | C400-MTFDDAT064MAM | 64 GB  | 1       | 1     | 0     | 0.00   |
| Lite-On   | LCH-128V2S-11 2... | 128 GB | 2       | 1     | 0     | 0.00   |
| Micron    | 5300_MTFDDAK240TDS | 240 GB | 2       | 1     | 0     | 0.00   |
| TCSUNBOW  | X1                 | 16 GB  | 1       | 1     | 0     | 0.00   |
| addlink   | SATA SSD           | 256 GB | 1       | 1     | 0     | 0.00   |
| SK hynix  | HFS128G38MNB-2200A | 128 GB | 3       | 228   | 133   | 0.00   |
| Intel     | SSDSC2BX400G4R     | 400 GB | 2       | 1654  | 1028  | 0.00   |
| China     | SSD 256G           | 256 GB | 1       | 1     | 0     | 0.00   |
| SanDisk   | SD8SB8U128G1001    | 128 GB | 1       | 1     | 0     | 0.00   |
| SanDisk   | SD8SNAT-128G-1006  | 128 GB | 2       | 1     | 0     | 0.00   |
| acpi      | MSS4FV-MP mSATA... | 128 GB | 1       | 1     | 0     | 0.00   |
| Apacer    | 16GB SATA Flash... | 16 GB  | 3       | 22    | 20    | 0.00   |
| Goodram   | SSDPR-CL100-120    | 120 GB | 1       | 1     | 0     | 0.00   |
| SK hynix  | HFS256G32MND-2200A | 256 GB | 1       | 225   | 153   | 0.00   |
| ADATA     | SSD DP900 512GB... | 512 GB | 2       | 1465  | 1016  | 0.00   |
| BHT       | WR202I0032G E70... | 32 GB  | 1       | 1     | 0     | 0.00   |
| Plextor   | PX-512M6M          | 512 GB | 1       | 1     | 0     | 0.00   |
| Patriot   | Pyro m3            | 240 GB | 1       | 1378  | 1015  | 0.00   |
| ADATA     | AXM14S3-128GM-B    | 128 GB | 1       | 1363  | 1018  | 0.00   |
| Toshiba   | THNSNK128GVN8 M... | 128 GB | 1       | 133   | 100   | 0.00   |
| ADATA     | IMSS316-256GD      | 256 GB | 1       | 1     | 0     | 0.00   |
| ASENNO    | AS25               | 120 GB | 1       | 1     | 0     | 0.00   |
| OEM       | Genuine            | 1 TB   | 1       | 1     | 0     | 0.00   |
| Patriot   | Solid              | 240 GB | 2       | 1     | 0     | 0.00   |
| Team      | M8PS5 SSD          | 128 GB | 1       | 1     | 0     | 0.00   |
| KingSpec  | ACJC2M128S25       | 128 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | MZNLN128HAHQ-000L2 | 128 GB | 2       | 1     | 0     | 0.00   |
| Kingmax   | SSD                | 240 GB | 2       | 1     | 0     | 0.00   |
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
| Intenso   | SSD Sata III       | 128 GB | 2       | 0     | 0     | 0.00   |
| SanDisk   | SD6SB1M256G1022I   | 256 GB | 1       | 400   | 474   | 0.00   |
| Intel     | SSDSC2KW180H6      | 180 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | HFS060G32MNM-1010U | 64 GB  | 1       | 822   | 1016  | 0.00   |
| Eluktro   | TRO-SSD7-500GB-PRO | 500 GB | 1       | 806   | 1016  | 0.00   |
| Plextor   | PX-128M6MV         | 128 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | RBUSNS8180DS3256GJ | 256 GB | 2       | 0     | 0     | 0.00   |
| KingSpec  | MT-64              | 64 GB  | 1       | 0     | 0     | 0.00   |
| SanDisk   | SD8TN8U512G1001    | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | SC210 2.5 7MM      | 256 GB | 2       | 556   | 856   | 0.00   |
| Lite-On   | E200-160           | 160 GB | 1       | 12    | 18    | 0.00   |
| KingSpec  | ACSC2M064S25       | 64 GB  | 1       | 0     | 0     | 0.00   |
| Team      | T253X1240G         | 240 GB | 1       | 0     | 0     | 0.00   |
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
| DOGFISH   | SSD                | 512 GB | 1       | 0     | 0     | 0.00   |
| Corsair   | Force LS SSD       | 240 GB | 2       | 274   | 757   | 0.00   |
| ADATA     | XM11 128GB-V2      | 128 GB | 1       | 449   | 1048  | 0.00   |
| Gost      | SSD120             | 120 GB | 1       | 0     | 0     | 0.00   |
| SMI       | B17A               | 240 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | SDSSDA-1T00        | 1 TB   | 1       | 0     | 0     | 0.00   |
| Transcend | TS120GMTS820S      | 120 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | SHPM2280P2H-240G   | 240 GB | 3       | 218   | 540   | 0.00   |
| China     | T60                | 64 GB  | 2       | 0     | 0     | 0.00   |
| SK hynix  | HFS128G39TNF-N3A0A | 128 GB | 2       | 0     | 0     | 0.00   |
| Reeinno   | ST960GB S7S3       | 960 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | SH103S3240G-NV     | 240 GB | 1       | 377   | 1018  | 0.00   |
| PNY       | SSD2SC120GE2DA0... | 120 GB | 1       | 373   | 1018  | 0.00   |
| SPCC      | SSD170             | 64 GB  | 1       | 358   | 1016  | 0.00   |
| Mushkin   | MKNSSDCL120GB-DX   | 120 GB | 1       | 348   | 1006  | 0.00   |
| Lite-On   | CS1-SP32-11 M.2... | 32 GB  | 1       | 1     | 4     | 0.00   |
| Mushkin   | MKNSSDCL480GB-DX   | 480 GB | 1       | 347   | 1020  | 0.00   |
| Smartbuy  | SSD                | 512 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TS8GHSD630         | 8 GB   | 1       | 679   | 2050  | 0.00   |
| KingFast  | SSD                | 64 GB  | 1       | 0     | 1     | 0.00   |
| Kingston  | SVP200S37A256G     | 256 GB | 1       | 311   | 1017  | 0.00   |
| China     | SATA SSD           | 256 GB | 1       | 0     | 0     | 0.00   |
| FASTDISK  | SSD 32G            | 32 GB  | 1       | 0     | 0     | 0.00   |
| GLOWAY    | STK120GS3-S7       | 120 GB | 1       | 0     | 0     | 0.00   |
| Leven     | JAJS300M120C       | 120 GB | 1       | 0     | 0     | 0.00   |
| Lite-On   | CV1-8B512          | 512 GB | 1       | 0     | 0     | 0.00   |
| Patriot   | Torch LE           | 120 GB | 1       | 0     | 0     | 0.00   |
| Zheino    | CHN 25SATAA3 120   | 120 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | HFS256G3AMNB-2200A | 256 GB | 1       | 283   | 1006  | 0.00   |
| Intel     | SSDSCKKF256G8H     | 256 GB | 1       | 27    | 99    | 0.00   |
| SanDisk   | SD8SBAT-032G-1006  | 32 GB  | 4       | 0     | 0     | 0.00   |
| KingSpec  | Q-90               | 90 GB  | 1       | 134   | 520   | 0.00   |
| Lite-On   | LMT-256M6M-HP      | 256 GB | 1       | 39    | 152   | 0.00   |
| China     | T480               | 480 GB | 1       | 69    | 275   | 0.00   |
| GLOWAY    | VAL64GM3-mSATA     | 64 GB  | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSA2CW300G3      | 304 GB | 1       | 0     | 0     | 0.00   |
| TEUTONS   | SSD                | 256 GB | 1       | 0     | 0     | 0.00   |
| GeIL      | ZENITH S3-120GB    | 120 GB | 1       | 245   | 1021  | 0.00   |
| Samsung   | SSD PM810 TM       | 128 GB | 1       | 239   | 1033  | 0.00   |
| Intel     | SSDSCKKF256H6L     | 256 GB | 1       | 13    | 57    | 0.00   |
| Samsung   | MZ7PA256HMDR-010H1 | 256 GB | 1       | 236   | 1040  | 0.00   |
| Myung     | G3 Series          | 120 GB | 1       | 228   | 1015  | 0.00   |
| Goldenfir | T650-120G          | 128 GB | 1       | 0     | 0     | 0.00   |
| Lite-On   | S960 256           | 256 GB | 1       | 0     | 0     | 0.00   |
| Zheino    | CHN25SATAS1 064    | 64 GB  | 1       | 0     | 0     | 0.00   |
| SK hynix  | HFS256G38MNB-2200A | 256 GB | 1       | 207   | 1007  | 0.00   |
| SK hynix  | HFS512G39TND-N210A | 512 GB | 1       | 371   | 2017  | 0.00   |
| Patriot   | Pyro SE            | 240 GB | 1       | 180   | 1016  | 0.00   |
| China     | T120               | 120 GB | 1       | 0     | 0     | 0.00   |
| Faspeed   | H5-30G             | 32 GB  | 1       | 0     | 0     | 0.00   |
| Fujitsu   | F500s 240G         | 240 GB | 1       | 0     | 0     | 0.00   |
| Kingmax   | SSD                | 480 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | CF Card            | 16 GB  | 1       | 0     | 0     | 0.00   |
| SanDisk   | SDSSDH3 2T00       | 2 TB   | 1       | 0     | 0     | 0.00   |
| WDC       | WDS250G2B0B        | 250 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | SNS4151S332G       | 32 GB  | 1       | 170   | 1022  | 0.00   |
| Intel     | SSDMCEAW080A4 m... | 80 GB  | 1       | 162   | 1009  | 0.00   |
| Toshiba   | THNSNK128GCS8 SATA | 128 GB | 1       | 16    | 100   | 0.00   |
| Goldenfir | T650-120GB         | 120 GB | 1       | 4     | 28    | 0.00   |
| Lite-On   | LCS-256M6S         | 256 GB | 1       | 138   | 1051  | 0.00   |
| Colorful  | SL500              | 480 GB | 1       | 22    | 195   | 0.00   |
| Lite-On   | LSS-16L6G-HP       | 16 GB  | 1       | 125   | 1275  | 0.00   |
| Kingston  | SMS151S324G        | 24 GB  | 1       | 95    | 1022  | 0.00   |
| DOGFISH   | SSD                | 128 GB | 1       | 0     | 0     | 0.00   |
| Plextor   | PX-32G5L           | 32 GB  | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSC2KF512H6 SATA | 512 GB | 1       | 7     | 84    | 0.00   |
| Micron    | MTFDDAT064MAM-1J2  | 64 GB  | 1       | 85    | 1039  | 0.00   |
| PNY       | SSD2SC240G1SA75... | 240 GB | 1       | 7     | 88    | 0.00   |
| ADATA     | XM11 128GB-V3      | 128 GB | 1       | 77    | 1016  | 0.00   |
| Transcend | TS64GSSD340K       | 64 GB  | 1       | 74    | 1008  | 0.00   |
| Mushkin   | MKNSSDCR120GB-DX7  | 120 GB | 1       | 73    | 1016  | 0.00   |
| SanDisk   | SDSSDX480GG25      | 480 GB | 1       | 76    | 1090  | 0.00   |
| SandForce | 906190             | 64 GB  | 1       | 65    | 1018  | 0.00   |
| PNY       | SSD2SC120G3LC72... | 120 GB | 1       | 65    | 1019  | 0.00   |
| ADATA     | SP900NS38          | 512 GB | 1       | 64    | 1020  | 0.00   |
| MicroData | MD300 128G         | 128 GB | 1       | 41    | 666   | 0.00   |
| Kingston  | SNS4151S316GD      | 16 GB  | 1       | 51    | 1022  | 0.00   |
| Samsung   | MZMPA128HMFU-000H1 | 128 GB | 2       | 69    | 1727  | 0.00   |
| Lite-On   | LMT-128M3M         | 128 GB | 1       | 44    | 1009  | 0.00   |
| SanDisk   | SD9SN8W-128G-1006  | 128 GB | 16      | 43    | 995   | 0.00   |
| Foxline   | FLSSD128X5         | 128 GB | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSC2BB150G7      | 150 GB | 1       | 0     | 0     | 0.00   |
| KingDian  | S180               | 120 GB | 1       | 0     | 0     | 0.00   |
| Lite-On   | CV8-8E256-11 SATA  | 256 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | SNS4151S316G       | 16 GB  | 1       | 39    | 1022  | 0.00   |
| ADATA     | SX300              | 64 GB  | 1       | 32    | 1020  | 0.00   |
| SanDisk   | SD9SN8W-256G-1006  | 256 GB | 3       | 25    | 996   | 0.00   |
| SanDisk   | TE22D10400GE8001   | 400 GB | 1       | 34    | 2047  | 0.00   |
| AMD       | R5S120GBSF         | 120 GB | 1       | 15    | 1016  | 0.00   |
| Lite-On   | CV8-8E128-HP       | 128 GB | 9       | 11    | 1007  | 0.00   |
| Intel     | SSDSC2KW360H6      | 360 GB | 1       | 5     | 1534  | 0.00   |
| Intel     | SSDSC2KG400G7M ... | 400 GB | 1       | 2     | 1025  | 0.00   |
| SanDisk   | sandisk120         | 120 GB | 1       | 0     | 21    | 0.00   |
| Micron    | MTFDDAV256TDL-1... | 256 GB | 3       | 1     | 1008  | 0.00   |
| Kingston  | EK60HYXTFY176 V100 | 64 GB  | 1       | 1     | 1130  | 0.00   |
| SMI       | SSD DISK           | 506 GB | 1       | 0     | 1957  | 0.00   |
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
| Micron    | MX100/MX200/M5x0/M6... | 1      | 1       | 1083  | 0     | 2.97   |
| Intel     | X18-M/X25-M G1 SSDs    | 3      | 3       | 1024  | 0     | 2.81   |
| WDC       | Unknown                | 1      | 1       | 969   | 0     | 2.66   |
| Intel     | 730 and DC S35x0/36... | 17     | 58      | 1150  | 107   | 2.60   |
| HPE       | Unknown                | 3      | 3       | 831   | 0     | 2.28   |
| Crucial   | RealSSD m4/C400        | 5      | 46      | 905   | 155   | 2.24   |
| Intel     | X25-E SSDs             | 1      | 1       | 795   | 0     | 2.18   |
| Toshiba   | HG2 Series             | 2      | 4       | 792   | 0     | 2.17   |
| Toshiba   | HG3 Series             | 3      | 4       | 762   | 0     | 2.09   |
| Innodisk  | 3IE3/3ME3/3ME4 SSDs    | 1      | 1       | 760   | 0     | 2.08   |
| Micro ... | Unknown                | 1      | 1       | 722   | 0     | 1.98   |
| Kingston  | JMicron/Maxiotek ba... | 1      | 1       | 674   | 0     | 1.85   |
| Crucial   | RealSSD m4/C400/P400   | 3      | 20      | 919   | 155   | 1.80   |
| BLueRay   | Unknown                | 1      | 1       | 619   | 0     | 1.70   |
| Intel     | 520 Series SSDs        | 7      | 81      | 673   | 164   | 1.60   |
| SATADOM   | Innodisk 3IE3/3ME3/... | 1      | 1       | 574   | 0     | 1.57   |
| MyDigi... | Unknown                | 3      | 3       | 561   | 0     | 1.54   |
| Intel     | 510 Series SSDs        | 1      | 3       | 545   | 0     | 1.49   |
| OCZ       | SandForce Driven SSDs  | 38     | 244     | 690   | 47    | 1.48   |
| Phison    | Unknown                | 2      | 2       | 484   | 0     | 1.33   |
| Toshiba   | HG5 Series             | 1      | 2       | 471   | 0     | 1.29   |
| Corsair   | SandForce Driven SSDs  | 21     | 122     | 614   | 97    | 1.28   |
| OCZ       | Indilinx Barefoot_2... | 12     | 104     | 530   | 3     | 1.27   |
| Kingston  | JMicron based SSDs     | 13     | 31      | 648   | 2     | 1.26   |
| Intel     | 330/335 Series SSDs    | 6      | 36      | 611   | 1     | 1.24   |
| Toshiba   | HG6 Series SSD         | 9      | 23      | 422   | 0     | 1.16   |
| Apple     | SD/SM/TS E/F/G SSDs    | 9      | 27      | 406   | 0     | 1.11   |
| Transcend | JMicron based SSDs     | 4      | 11      | 404   | 92    | 1.05   |
| Crucial   | RealSSD C300/M500      | 5      | 40      | 529   | 59    | 0.99   |
| KingShare | Unknown                | 1      | 1       | 358   | 0     | 0.98   |
| ZTC       | Unknown                | 1      | 1       | 357   | 0     | 0.98   |
| Samsung   | Samsung based SSDs     | 199    | 1825    | 360   | 9     | 0.96   |
| Advantech | Unknown                | 1      | 1       | 345   | 0     | 0.95   |
| Toshiba   | HG5d Series            | 7      | 12      | 335   | 0     | 0.92   |
| Team      | SiliconMotion based... | 1      | 3       | 334   | 0     | 0.92   |
| Crucial   | MX1/2/300, M5/600, ... | 3      | 12      | 493   | 8     | 0.90   |
| Mushkin   | SandForce Driven SSDs  | 13     | 14      | 491   | 292   | 0.90   |
| Micron    | BX/MX1/2/3/500, M5/... | 5      | 9       | 318   | 0     | 0.87   |
| Apple     | JMicron based SSDs     | 3      | 6       | 317   | 0     | 0.87   |
| ADATA     | SandForce Driven SSDs  | 9      | 70      | 358   | 6     | 0.82   |
| Ramaxel   | Unknown                | 1      | 2       | 295   | 0     | 0.81   |
| Intel     | 320 Series SSDs        | 8      | 27      | 287   | 1     | 0.77   |
| Toshiba   | OCZ                    | 4      | 6       | 274   | 0     | 0.75   |
| Kingston  | SandForce Driven SSDs  | 35     | 790     | 318   | 63    | 0.75   |
| Apple     | Unknown                | 1      | 1       | 518   | 1     | 0.71   |
| ADATA     | JMicron based SSDs     | 5      | 23      | 256   | 1     | 0.69   |
| Verbatim  | Unknown                | 2      | 2       | 246   | 0     | 0.68   |
| Micron    | RealSSD m4/C400/P400   | 6      | 15      | 259   | 337   | 0.67   |
| Plextor   | M3/M5/M6/M7 Series ... | 6      | 13      | 243   | 0     | 0.67   |
| Hypertec  | Unknown                | 1      | 1       | 243   | 0     | 0.67   |
| WDC       | Blue PC SSD            | 2      | 17      | 233   | 0     | 0.64   |
| OCZ       | Indilinx Barefoot 3... | 14     | 58      | 246   | 36    | 0.64   |
| Intel     | X18-M/X25-M/X25-V G... | 12     | 35      | 730   | 9     | 0.62   |
| OCZ       | Indilinx Barefoot b... | 4      | 6       | 295   | 1     | 0.62   |
| Intel     | 53x and Pro 2500 Se... | 9      | 31      | 236   | 3     | 0.61   |
| Toshiba   | OCZ/Toshiba Trion SSDs | 4      | 22      | 245   | 1     | 0.61   |
| Intenso   | Phison Driven OEM SSDs | 3      | 13      | 245   | 1     | 0.60   |
| Intel     | 53x and Pro 1500/25... | 4      | 18      | 386   | 4     | 0.59   |
| Toshiba   | Unknown                | 33     | 80      | 228   | 11    | 0.59   |
| SanDisk   | Marvell based SanDi... | 53     | 312     | 227   | 30    | 0.57   |
| SanDisk   | SanDisk based SSDs     | 28     | 149     | 235   | 30    | 0.56   |
| Crucial   | BX/MX1/2/3/500, M5/... | 31     | 306     | 251   | 44    | 0.55   |
| Seagate   | Unknown                | 9      | 15      | 212   | 1     | 0.54   |
| Intel     | 530 Series SSDs        | 2      | 37      | 259   | 1     | 0.52   |
| Samsung   | Unknown                | 24     | 77      | 192   | 1     | 0.51   |
| PNY       | Unknown                | 15     | 18      | 209   | 118   | 0.51   |
| Corsair   | Indilinx Barefoot b... | 3      | 3       | 303   | 2     | 0.50   |
| Smartbuy  | Unknown                | 11     | 17      | 182   | 0     | 0.50   |
| Micron    | RealSSD m4/C400        | 1      | 1       | 182   | 0     | 0.50   |
| Smartbuy  | Phison Driven SSDs     | 3      | 100     | 192   | 1     | 0.49   |
| SPCC      | Unknown                | 19     | 119     | 257   | 146   | 0.49   |
| Patriot   | Unknown                | 16     | 33      | 305   | 93    | 0.48   |
| Intel     | S4510/S4610/S4500/S... | 6      | 12      | 174   | 0     | 0.48   |
| OCZ       | Trion SSDs             | 2      | 8       | 211   | 1     | 0.47   |
| Kingston  | SSDNow UV400           | 3      | 128     | 188   | 32    | 0.47   |
| Plextor   | M3/M5 (Pro) Series ... | 5      | 15      | 240   | 70    | 0.46   |
| PNY       | Phison Driven SSDs     | 7      | 38      | 164   | 0     | 0.45   |
| SK hynix  | SATA SSDs              | 21     | 97      | 199   | 53    | 0.44   |
| Zheino    | Silicon Motion base... | 1      | 2       | 158   | 0     | 0.43   |
| Transcend | SandForce Driven SSDs  | 5      | 7       | 155   | 0     | 0.43   |
| Micron    | Unknown                | 16     | 37      | 230   | 170   | 0.42   |
| Palit     | Unknown                | 3      | 4       | 150   | 0     | 0.41   |
| Intel     | Unknown                | 28     | 43      | 193   | 106   | 0.41   |
| Goodram   | Phison Driven SSDs     | 5      | 40      | 150   | 0     | 0.41   |
| OCZ       | OCZ/Toshiba Trion SSDs | 2      | 9       | 162   | 1     | 0.41   |
| PHISON    | Unknown                | 3      | 3       | 169   | 1     | 0.41   |
| Intel     | 525 Series SSDs        | 1      | 2       | 148   | 0     | 0.41   |
| Corsair   | Unknown                | 15     | 26      | 401   | 39    | 0.39   |
| Innodisk  | Unknown                | 1      | 1       | 140   | 0     | 0.39   |
| SanDisk   | Unknown                | 93     | 198     | 153   | 124   | 0.38   |
| HP        | Unknown                | 9      | 16      | 140   | 0     | 0.38   |
| Intel     | 730 and DC S3500/S3... | 2      | 2       | 139   | 0     | 0.38   |
| Kingston  | Unknown                | 52     | 101     | 155   | 78    | 0.38   |
| OCZ       | Unknown                | 7      | 10      | 361   | 102   | 0.37   |
| ZOTAC     | Unknown                | 2      | 3       | 132   | 0     | 0.36   |
| SPCC      | Phison Driven OEM SSDs | 6      | 189     | 165   | 118   | 0.35   |
| KLEVV     | Unknown                | 1      | 1       | 127   | 0     | 0.35   |
| SanDisk   | SandForce Driven SSDs  | 6      | 131     | 142   | 11    | 0.35   |
| Chiprex   | Unknown                | 1      | 1       | 126   | 0     | 0.35   |
| Plextor   | Unknown                | 25     | 63      | 131   | 1     | 0.34   |
| Hoodisk   | Unknown                | 2      | 2       | 118   | 0     | 0.32   |
| Team      | Unknown                | 19     | 31      | 122   | 1     | 0.32   |
| Goodram   | Unknown                | 16     | 38      | 127   | 1     | 0.32   |
| Crucial   | MX100/MX200/M5x0/M6... | 1      | 1       | 116   | 0     | 0.32   |
| Foxline   | Unknown                | 4      | 4       | 364   | 254   | 0.32   |
| Samsung   | SandForce Driven SSDs  | 1      | 1       | 115   | 0     | 0.32   |
| Mushkin   | Unknown                | 4      | 5       | 159   | 204   | 0.32   |
| Plextor   | M3/M5/M6 Series SSDs   | 13     | 162     | 125   | 21    | 0.31   |
| BIOSTAR   | Unknown                | 2      | 2       | 109   | 0     | 0.30   |
| KingFast  | Unknown                | 8      | 24      | 110   | 128   | 0.30   |
| Mushkin   | SiliconMotion based... | 1      | 1       | 107   | 0     | 0.30   |
| Crucial   | RealSSD C300/P300      | 1      | 2       | 555   | 504   | 0.29   |
| WDC       | Blue / Red / Green ... | 5      | 10      | 104   | 0     | 0.29   |
| Transcend | Indilinx Barefoot b... | 1      | 1       | 309   | 2     | 0.28   |
| Phison    | Phison Driven SSDs     | 1      | 1       | 101   | 0     | 0.28   |
| Micron    | BX/MX1/2/3/500, M5/... | 12     | 64      | 127   | 62    | 0.28   |
| Apple     | SD/SM/TS E/F SSDs      | 3      | 4       | 101   | 0     | 0.28   |
| OWC       | SandForce Driven SSDs  | 1      | 2       | 99    | 0     | 0.27   |
| Kingston  | Phison Driven SSDs     | 15     | 498     | 103   | 1     | 0.27   |
| GALAX     | Unknown                | 2      | 3       | 98    | 0     | 0.27   |
| WDC       | Blue and Green SSDs    | 25     | 347     | 99    | 1     | 0.27   |
| Anobit    | Unknown                | 1      | 1       | 96    | 0     | 0.27   |
| Phison    | Driven OEM SSDs        | 5      | 17      | 95    | 0     | 0.26   |
| Kingston  | SSDNow UV400/500       | 7      | 39      | 99    | 30    | 0.26   |
| Patriot   | Phison Driven SSDs     | 5      | 54      | 97    | 1     | 0.26   |
| Gigabyte  | Unknown                | 1      | 3       | 91    | 0     | 0.25   |
| Apacer    | AS340 SSDs             | 2      | 4       | 90    | 0     | 0.25   |
| ADATA     | Unknown                | 51     | 164     | 191   | 160   | 0.24   |
| Crucial   | SiliconMotion based... | 3      | 12      | 85    | 0     | 0.23   |
| XPG       | Unknown                | 1      | 1       | 85    | 0     | 0.23   |
| e2e4      | Unknown                | 2      | 4       | 84    | 0     | 0.23   |
| Ramsta    | Unknown                | 2      | 2       | 83    | 0     | 0.23   |
| Transcend | JMicron/Maxiotek ba... | 3      | 4       | 102   | 252   | 0.23   |
| Crucial   | MX500 SSDs             | 6      | 146     | 84    | 1     | 0.23   |
| BHT       | Unknown                | 4      | 6       | 79    | 0     | 0.22   |
| Seagate   | 600 Series             | 1      | 1       | 79    | 0     | 0.22   |
| China     | Unknown                | 37     | 216     | 80    | 2     | 0.21   |
| Toshiba   | HG6 Series             | 1      | 2       | 76    | 0     | 0.21   |
| SK hynix  | Unknown                | 24     | 37      | 206   | 97    | 0.20   |
| Crucial   | BX/MX1/2/3/500, M5/... | 1      | 2       | 69    | 0     | 0.19   |
| ADATA     | Silicon Motion base... | 8      | 59      | 71    | 2     | 0.19   |
| oyunkey   | Unknown                | 1      | 1       | 68    | 0     | 0.19   |
| KingDian  | Unknown                | 8      | 27      | 73    | 114   | 0.19   |
| Intenso   | Unknown                | 7      | 14      | 69    | 3     | 0.18   |
| ADATA     | SiliconMotion based... | 2      | 40      | 66    | 1     | 0.18   |
| Patriot   | Silicon Motion base... | 2      | 2       | 65    | 0     | 0.18   |
| Lite-On   | Unknown                | 56     | 99      | 80    | 161   | 0.17   |
| DOGFISH   | Unknown                | 4      | 4       | 62    | 0     | 0.17   |
| Faspeed   | Unknown                | 7      | 7       | 61    | 0     | 0.17   |
| Gigabyte  | Phison Driven SSDs     | 3      | 16      | 61    | 0     | 0.17   |
| Apacer    | Unknown                | 11     | 40      | 63    | 1     | 0.17   |
| TEKET     | Unknown                | 1      | 2       | 59    | 0     | 0.16   |
| Crucial   | Silicon Motion base... | 1      | 13      | 60    | 1     | 0.16   |
| tigo      | Unknown                | 1      | 1       | 57    | 0     | 0.16   |
| Intel     | 545s Series SSDs       | 5      | 30      | 56    | 1     | 0.15   |
| Micron    | 5100 Pro / 5200 SSDs   | 2      | 2       | 56    | 0     | 0.15   |
| Radeon    | Indilinx Barefoot 3... | 1      | 1       | 56    | 0     | 0.15   |
| Londisk   | Unknown                | 3      | 9       | 54    | 0     | 0.15   |
| Netac     | Unknown                | 6      | 12      | 53    | 0     | 0.15   |
| Transcend | SiliconMotion based... | 16     | 85      | 52    | 0     | 0.15   |
| Kingmax   | Unknown                | 4      | 45      | 198   | 370   | 0.14   |
| KingDian  | Silicon Motion base... | 10     | 44      | 52    | 0     | 0.14   |
| Crucial   | Unknown                | 5      | 5       | 50    | 0     | 0.14   |
| Hikvision | Unknown                | 2      | 2       | 50    | 0     | 0.14   |
| Vaseky    | Unknown                | 1      | 2       | 48    | 0     | 0.13   |
| Leven     | Unknown                | 2      | 2       | 48    | 0     | 0.13   |
| AMD       | SiliconMotion based... | 1      | 25      | 46    | 1     | 0.13   |
| AMD       | Unknown                | 7      | 28      | 59    | 37    | 0.12   |
| Lenovo    | Unknown                | 4      | 5       | 45    | 0     | 0.12   |
| PRETEC    | Unknown                | 1      | 1       | 44    | 0     | 0.12   |
| Fordisk   | Unknown                | 2      | 2       | 41    | 0     | 0.11   |
| BIWIN     | Unknown                | 4      | 11      | 41    | 0     | 0.11   |
| Lexar     | Unknown                | 4      | 4       | 39    | 0     | 0.11   |
| KingSpec  | Unknown                | 38     | 82      | 50    | 42    | 0.11   |
| Goldkey   | Unknown                | 2      | 2       | 39    | 0     | 0.11   |
| Lite-On   | Silicon Motion base... | 2      | 4       | 38    | 0     | 0.10   |
| Reeinno   | Unknown                | 2      | 2       | 37    | 0     | 0.10   |
| LDLC      | Unknown                | 4      | 10      | 39    | 1     | 0.10   |
| Zheino    | Unknown                | 9      | 11      | 43    | 2     | 0.10   |
| OCZ       | Intrepid 3000 SSDs     | 2      | 2       | 35    | 0     | 0.10   |
| QUMO      | Unknown                | 3      | 5       | 275   | 407   | 0.09   |
| Transcend | Silicon Motion base... | 16     | 45      | 34    | 1     | 0.09   |
| RECADATA  | Unknown                | 1      | 1       | 33    | 0     | 0.09   |
| Kingrich  | Unknown                | 2      | 3       | 32    | 0     | 0.09   |
| Toshiba   | SG2 Series             | 1      | 1       | 32    | 0     | 0.09   |
| Hajaan    | Unknown                | 1      | 1       | 30    | 0     | 0.08   |
| KingPower | Unknown                | 1      | 1       | 29    | 0     | 0.08   |
| GeIL      | Unknown                | 7      | 8       | 59    | 128   | 0.08   |
| TAISU     | Unknown                | 1      | 1       | 27    | 0     | 0.08   |
| SenDisk   | Unknown                | 1      | 1       | 27    | 0     | 0.08   |
| Fujitsu   | Unknown                | 4      | 4       | 27    | 0     | 0.07   |
| HECTRON   | Unknown                | 1      | 1       | 26    | 0     | 0.07   |
| Super ... | Unknown                | 2      | 2       | 20    | 0     | 0.06   |
| XUNZHE    | Unknown                | 1      | 1       | 20    | 0     | 0.05   |
| Hyperdisk | Unknown                | 1      | 1       | 18    | 0     | 0.05   |
| OWC       | Unknown                | 1      | 1       | 17    | 0     | 0.05   |
| FORESEE   | Unknown                | 3      | 11      | 16    | 0     | 0.05   |
| LDNDISK   | Unknown                | 1      | 1       | 16    | 0     | 0.05   |
| Platinet  | Unknown                | 1      | 1       | 16    | 0     | 0.04   |
| AEGO      | Unknown                | 1      | 3       | 16    | 0     | 0.04   |
| Seagate   | 600 Pro Series         | 1      | 1       | 14    | 0     | 0.04   |
| Apple     | MacBook Air SSD        | 1      | 2       | 99    | 6     | 0.04   |
| Drevo     | Silicon Motion base... | 1      | 3       | 274   | 23    | 0.04   |
| TCSUNBOW  | Silicon Motion base... | 1      | 1       | 13    | 0     | 0.04   |
| Maximus   | Unknown                | 2      | 2       | 13    | 0     | 0.04   |
| Transcend | Unknown                | 5      | 6       | 126   | 342   | 0.04   |
| addlink   | Unknown                | 2      | 2       | 12    | 0     | 0.03   |
| TCSUNBOW  | Unknown                | 2      | 2       | 12    | 0     | 0.03   |
| T-FORCE   | Unknown                | 2      | 2       | 11    | 0     | 0.03   |
| Micron    | MX1/2/300, M5/600, ... | 1      | 1       | 11    | 0     | 0.03   |
| GLOWAY    | Unknown                | 4      | 5       | 11    | 0     | 0.03   |
| Pioneer   | Unknown                | 1      | 1       | 10    | 0     | 0.03   |
| Golden... | Unknown                | 1      | 1       | 10    | 0     | 0.03   |
| Mushkin   | Silicon Motion base... | 1      | 1       | 10    | 0     | 0.03   |
| Integral  | Unknown                | 1      | 2       | 8     | 0     | 0.02   |
| FASTDISK  | Unknown                | 6      | 6       | 7     | 0     | 0.02   |
| Union ... | Unknown                | 1      | 1       | 6     | 0     | 0.02   |
| V-GeN     | Unknown                | 1      | 1       | 5     | 0     | 0.02   |
| Kingston  | Silicon Motion base... | 2      | 2       | 5     | 0     | 0.02   |
| Teclast   | Unknown                | 4      | 5       | 5     | 0     | 0.01   |
| Dell      | Unknown                | 3      | 5       | 5     | 0     | 0.01   |
| Intel     | 540 Series SSDs        | 5      | 8       | 11    | 194   | 0.01   |
| TAMMUZ    | Unknown                | 1      | 1       | 4     | 0     | 0.01   |
| PHINOCOM  | Unknown                | 1      | 1       | 4     | 0     | 0.01   |
| Intel     | 311/313 Series SSDs    | 1      | 1       | 112   | 30    | 0.01   |
| ShineDisk | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| i-Flas... | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| MicroData | Unknown                | 2      | 2       | 23    | 333   | 0.01   |
| Gigastone | Unknown                | 1      | 1       | 2     | 0     | 0.01   |
| SOLIDATA  | Unknown                | 1      | 1       | 2420  | 1019  | 0.01   |
| Seagate   | IronWolf 110 SATA SSD  | 1      | 2       | 2     | 0     | 0.01   |
| ACPI      | Unknown                | 1      | 1       | 2     | 0     | 0.01   |
| Kingch... | Unknown                | 2      | 2       | 1     | 0     | 0.00   |
| Yunhai... | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| Drevo     | Unknown                | 1      | 1       | 33    | 18    | 0.00   |
| acpi      | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| Apacer    | SDM5/5A/5A-M Series... | 1      | 3       | 22    | 20    | 0.00   |
| ASENNO    | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| OEM       | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| Eluktro   | Unknown                | 1      | 1       | 806   | 1016  | 0.00   |
| Indilinx  | Unknown                | 1      | 2       | 0     | 0     | 0.00   |
| Gost      | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| TEUTONS   | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Myung     | Unknown                | 1      | 1       | 228   | 1015  | 0.00   |
| SMI       | Unknown                | 2      | 2       | 0     | 979   | 0.00   |
| Goldenfir | Unknown                | 2      | 2       | 2     | 14    | 0.00   |
| Colorful  | Unknown                | 1      | 1       | 22    | 195   | 0.00   |
| SandForce | Unknown                | 1      | 1       | 65    | 1018  | 0.00   |

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
| HPE         | 3      | 3       | 831   | 0     | 2.28   |
| Micro Ce... | 1      | 1       | 722   | 0     | 1.98   |
| BLueRay     | 1      | 1       | 619   | 0     | 1.70   |
| SATADOM     | 1      | 1       | 574   | 0     | 1.57   |
| MyDigita... | 3      | 3       | 561   | 0     | 1.54   |
| OCZ         | 81     | 441     | 558   | 34    | 1.23   |
| Innodisk    | 2      | 2       | 450   | 0     | 1.23   |
| Corsair     | 39     | 151     | 571   | 85    | 1.11   |
| Intel       | 118    | 428     | 511   | 61    | 1.08   |
| KingShare   | 1      | 1       | 358   | 0     | 0.98   |
| ZTC         | 1      | 1       | 357   | 0     | 0.98   |
| Advantech   | 1      | 1       | 345   | 0     | 0.95   |
| Samsung     | 224    | 1903    | 353   | 9     | 0.94   |
| Apple       | 17     | 40      | 350   | 1     | 0.93   |
| Ramaxel     | 1      | 2       | 295   | 0     | 0.81   |
| Toshiba     | 65     | 156     | 297   | 6     | 0.79   |
| Mushkin     | 19     | 21      | 371   | 243   | 0.69   |
| Verbatim    | 2      | 2       | 246   | 0     | 0.68   |
| Hypertec    | 1      | 1       | 243   | 0     | 0.67   |
| Crucial     | 65     | 605     | 297   | 45    | 0.66   |
| Kingston    | 128    | 1590    | 231   | 40    | 0.55   |
| Smartbuy    | 14     | 117     | 191   | 1     | 0.49   |
| SanDisk     | 180    | 790     | 196   | 50    | 0.49   |
| PNY         | 22     | 56      | 178   | 38    | 0.47   |
| Seagate     | 12     | 19      | 172   | 1     | 0.44   |
| Micron      | 44     | 130     | 190   | 118   | 0.42   |
| Palit       | 3      | 4       | 150   | 0     | 0.41   |
| PHISON      | 3      | 3       | 169   | 1     | 0.41   |
| SPCC        | 25     | 308     | 200   | 129   | 0.40   |
| Intenso     | 10     | 27      | 154   | 2     | 0.38   |
| HP          | 9      | 16      | 140   | 0     | 0.38   |
| Team        | 20     | 34      | 140   | 1     | 0.37   |
| SK hynix    | 45     | 134     | 201   | 65    | 0.37   |
| Phison      | 8      | 20      | 135   | 0     | 0.37   |
| ADATA       | 75     | 356     | 194   | 76    | 0.37   |
| Goodram     | 21     | 78      | 139   | 1     | 0.37   |
| ZOTAC       | 2      | 3       | 132   | 0     | 0.36   |
| KLEVV       | 1      | 1       | 127   | 0     | 0.35   |
| Plextor     | 49     | 253     | 139   | 18    | 0.35   |
| Chiprex     | 1      | 1       | 126   | 0     | 0.35   |
| Patriot     | 23     | 89      | 174   | 35    | 0.34   |
| Hoodisk     | 2      | 2       | 118   | 0     | 0.32   |
| Foxline     | 4      | 4       | 364   | 254   | 0.32   |
| BIOSTAR     | 2      | 2       | 109   | 0     | 0.30   |
| KingFast    | 8      | 24      | 110   | 128   | 0.30   |
| WDC         | 33     | 375     | 108   | 1     | 0.29   |
| GALAX       | 2      | 3       | 98    | 0     | 0.27   |
| Anobit      | 1      | 1       | 96    | 0     | 0.27   |
| XPG         | 1      | 1       | 85    | 0     | 0.23   |
| e2e4        | 2      | 4       | 84    | 0     | 0.23   |
| Ramsta      | 2      | 2       | 83    | 0     | 0.23   |
| BHT         | 4      | 6       | 79    | 0     | 0.22   |
| China       | 37     | 216     | 80    | 2     | 0.21   |
| Transcend   | 50     | 159     | 82    | 26    | 0.20   |
| OWC         | 2      | 3       | 71    | 0     | 0.20   |
| oyunkey     | 1      | 1       | 68    | 0     | 0.19   |
| Gigabyte    | 4      | 19      | 66    | 0     | 0.18   |
| DOGFISH     | 4      | 4       | 62    | 0     | 0.17   |
| Lite-On     | 58     | 103     | 78    | 155   | 0.17   |
| Faspeed     | 7      | 7       | 61    | 0     | 0.17   |
| Apacer      | 14     | 47      | 62    | 2     | 0.16   |
| TEKET       | 1      | 2       | 59    | 0     | 0.16   |
| KingDian    | 18     | 71      | 60    | 44    | 0.16   |
| tigo        | 1      | 1       | 57    | 0     | 0.16   |
| Radeon      | 1      | 1       | 56    | 0     | 0.15   |
| Zheino      | 10     | 13      | 61    | 2     | 0.15   |
| Londisk     | 3      | 9       | 54    | 0     | 0.15   |
| Netac       | 6      | 12      | 53    | 0     | 0.15   |
| Kingmax     | 4      | 45      | 198   | 370   | 0.14   |
| Hikvision   | 2      | 2       | 50    | 0     | 0.14   |
| Vaseky      | 1      | 2       | 48    | 0     | 0.13   |
| Leven       | 2      | 2       | 48    | 0     | 0.13   |
| AMD         | 8      | 53      | 53    | 20    | 0.13   |
| Lenovo      | 4      | 5       | 45    | 0     | 0.12   |
| PRETEC      | 1      | 1       | 44    | 0     | 0.12   |
| Fordisk     | 2      | 2       | 41    | 0     | 0.11   |
| BIWIN       | 4      | 11      | 41    | 0     | 0.11   |
| Lexar       | 4      | 4       | 39    | 0     | 0.11   |
| KingSpec    | 38     | 82      | 50    | 42    | 0.11   |
| Goldkey     | 2      | 2       | 39    | 0     | 0.11   |
| Reeinno     | 2      | 2       | 37    | 0     | 0.10   |
| LDLC        | 4      | 10      | 39    | 1     | 0.10   |
| QUMO        | 3      | 5       | 275   | 407   | 0.09   |
| RECADATA    | 1      | 1       | 33    | 0     | 0.09   |
| Kingrich    | 2      | 3       | 32    | 0     | 0.09   |
| Hajaan      | 1      | 1       | 30    | 0     | 0.08   |
| KingPower   | 1      | 1       | 29    | 0     | 0.08   |
| GeIL        | 7      | 8       | 59    | 128   | 0.08   |
| TAISU       | 1      | 1       | 27    | 0     | 0.08   |
| SenDisk     | 1      | 1       | 27    | 0     | 0.08   |
| Fujitsu     | 4      | 4       | 27    | 0     | 0.07   |
| HECTRON     | 1      | 1       | 26    | 0     | 0.07   |
| Super Ta... | 2      | 2       | 20    | 0     | 0.06   |
| XUNZHE      | 1      | 1       | 20    | 0     | 0.05   |
| Hyperdisk   | 1      | 1       | 18    | 0     | 0.05   |
| FORESEE     | 3      | 11      | 16    | 0     | 0.05   |
| LDNDISK     | 1      | 1       | 16    | 0     | 0.05   |
| Platinet    | 1      | 1       | 16    | 0     | 0.04   |
| AEGO        | 1      | 3       | 16    | 0     | 0.04   |
| Maximus     | 2      | 2       | 13    | 0     | 0.04   |
| TCSUNBOW    | 3      | 3       | 12    | 0     | 0.03   |
| addlink     | 2      | 2       | 12    | 0     | 0.03   |
| T-FORCE     | 2      | 2       | 11    | 0     | 0.03   |
| GLOWAY      | 4      | 5       | 11    | 0     | 0.03   |
| Pioneer     | 1      | 1       | 10    | 0     | 0.03   |
| Goldendisk  | 1      | 1       | 10    | 0     | 0.03   |
| Drevo       | 2      | 4       | 213   | 22    | 0.03   |
| Integral    | 1      | 2       | 8     | 0     | 0.02   |
| FASTDISK    | 6      | 6       | 7     | 0     | 0.02   |
| Union Me... | 1      | 1       | 6     | 0     | 0.02   |
| V-GeN       | 1      | 1       | 5     | 0     | 0.02   |
| Teclast     | 4      | 5       | 5     | 0     | 0.01   |
| Dell        | 3      | 5       | 5     | 0     | 0.01   |
| TAMMUZ      | 1      | 1       | 4     | 0     | 0.01   |
| PHINOCOM    | 1      | 1       | 4     | 0     | 0.01   |
| ShineDisk   | 1      | 1       | 3     | 0     | 0.01   |
| i-FlashDisk | 1      | 1       | 3     | 0     | 0.01   |
| MicroData   | 2      | 2       | 23    | 333   | 0.01   |
| Gigastone   | 1      | 1       | 2     | 0     | 0.01   |
| SOLIDATA    | 1      | 1       | 2420  | 1019  | 0.01   |
| ACPI        | 1      | 1       | 2     | 0     | 0.01   |
| Kingchuxing | 2      | 2       | 1     | 0     | 0.00   |
| Yunhaitian  | 1      | 1       | 1     | 0     | 0.00   |
| acpi        | 1      | 1       | 1     | 0     | 0.00   |
| ASENNO      | 1      | 1       | 1     | 0     | 0.00   |
| OEM         | 1      | 1       | 1     | 0     | 0.00   |
| Eluktro     | 1      | 1       | 806   | 1016  | 0.00   |
| Indilinx    | 1      | 2       | 0     | 0     | 0.00   |
| Gost        | 1      | 1       | 0     | 0     | 0.00   |
| TEUTONS     | 1      | 1       | 0     | 0     | 0.00   |
| Myung       | 1      | 1       | 228   | 1015  | 0.00   |
| SMI         | 2      | 2       | 0     | 979   | 0.00   |
| Goldenfir   | 2      | 2       | 2     | 14    | 0.00   |
| Colorful    | 1      | 1       | 22    | 195   | 0.00   |
| SandForce   | 1      | 1       | 65    | 1018  | 0.00   |

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
| Toshiba   | THNSN5256GPU7      | 256 GB | 2       | 926   | 0     | 2.54   |
| Samsung   | SSD 950 PRO        | 256 GB | 2       | 834   | 0     | 2.29   |
| Intel     | SSDPEDMW012T4      | 1.2 TB | 1       | 823   | 0     | 2.26   |
| Samsung   | SSD 950 PRO        | 512 GB | 7       | 818   | 0     | 2.24   |
| Samsung   | MZVKW512HMJP-00000 | 512 GB | 2       | 698   | 0     | 1.91   |
| Intel     | MEMPEK1W032GA      | 32 GB  | 1       | 694   | 0     | 1.90   |
| Intel     | SSDPED1K375GA      | 375 GB | 1       | 603   | 0     | 1.65   |
| Intel     | SSDPED1D280GA      | 280 GB | 1       | 600   | 0     | 1.64   |
| Intel     | SSDPEDMD400G4      | 400 GB | 1       | 595   | 0     | 1.63   |
| Samsung   | MZVPV256HDGL-00000 | 256 GB | 3       | 564   | 0     | 1.55   |
| Toshiba   | THNSN5512GPUK      | 512 GB | 1       | 563   | 0     | 1.54   |
| SanDisk   | A400 NVMe          | 512 GB | 1       | 554   | 0     | 1.52   |
| Intel     | SSDPE21D480GA      | 480 GB | 2       | 515   | 0     | 1.41   |
| Intel     | SSDPEKKW256G7      | 256 GB | 6       | 596   | 5     | 1.34   |
| Intel     | SSDPEKKF256G7H     | 256 GB | 3       | 476   | 0     | 1.31   |
| Toshiba   | THNSN51T02DUK NVMe | 1 TB   | 2       | 457   | 0     | 1.25   |
| Samsung   | MZVPV128HDGM-00000 | 128 GB | 3       | 453   | 0     | 1.24   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 1       | 448   | 0     | 1.23   |
| Intel     | SSDPEKKF256G7L     | 256 GB | 4       | 420   | 0     | 1.15   |
| Toshiba   | RC100              | 240 GB | 1       | 404   | 0     | 1.11   |
| Toshiba   | THNSN5512GPUK NVMe | 512 GB | 7       | 399   | 0     | 1.10   |
| Samsung   | MZVLV256HCHP-000L2 | 256 GB | 2       | 388   | 0     | 1.07   |
| Samsung   | PM951 NVMe         | 512 GB | 2       | 388   | 0     | 1.06   |
| WDC       | WDS256G1X0C-00ENX0 | 256 GB | 2       | 359   | 0     | 0.99   |
| Samsung   | MZSLW1T0HMLH-000L1 | 1 TB   | 2       | 359   | 0     | 0.98   |
| XPG       | GAMMIX S11         | 480 GB | 4       | 358   | 0     | 0.98   |
| Corsair   | Force MP500        | 120 GB | 1       | 357   | 0     | 0.98   |
| Transcend | TS128GMTE110S      | 128 GB | 1       | 346   | 0     | 0.95   |
| SK hynix  | PC401 NVMe         | 256 GB | 1       | 329   | 0     | 0.90   |
| Toshiba   | THNSN51T02DU7 NVMe | 1 TB   | 1       | 321   | 0     | 0.88   |
| Toshiba   | KXG50ZNV1T02 NVMe  | 1 TB   | 2       | 311   | 0     | 0.85   |
| Toshiba   | THNSN5256GPUK NVMe | 256 GB | 3       | 307   | 0     | 0.84   |
| Samsung   | MZVLV256HCHP-00000 | 256 GB | 2       | 285   | 0     | 0.78   |
| Toshiba   | KXG5AZNV256G       | 256 GB | 3       | 281   | 0     | 0.77   |
| Intel     | SSDPEKKW128G7      | 128 GB | 3       | 402   | 1     | 0.77   |
| WDC       | WDS512G1X0C-00ENX0 | 512 GB | 2       | 257   | 0     | 0.70   |
| Toshiba   | THNSF5256GPUK      | 256 GB | 1       | 249   | 0     | 0.68   |
| Mushkin   | MKNSSDPL500GB-D8   | 500 GB | 1       | 248   | 0     | 0.68   |
| Toshiba   | THNSN5128GPU7      | 128 GB | 1       | 241   | 0     | 0.66   |
| Toshiba   | KXG5AZNV512G       | 512 GB | 3       | 241   | 0     | 0.66   |
| Intel     | SSDPEKKF360G7H     | 360 GB | 3       | 239   | 0     | 0.66   |
| WDC       | WDS250G2X0C-00L350 | 250 GB | 4       | 234   | 0     | 0.64   |
| Intel     | SSDPEKKF512G8 NVMe | 512 GB | 2       | 231   | 0     | 0.63   |
| Samsung   | MZVLW1T0HMLH-00000 | 1 TB   | 4       | 228   | 0     | 0.63   |
| Lite-On   | T10 240            | 240 GB | 1       | 227   | 0     | 0.62   |
| Toshiba   | KXG50ZNV512G NVMe  | 512 GB | 9       | 226   | 0     | 0.62   |
| Corsair   | Force MP510 1.9TB  | 1.9 TB | 1       | 223   | 0     | 0.61   |
| Intel     | SSDPED1D480GA      | 480 GB | 2       | 222   | 0     | 0.61   |
| Samsung   | MZVPV512HDGL-00000 | 512 GB | 1       | 216   | 0     | 0.59   |
| Intel     | SSDPEKNW020T8      | 2 TB   | 7       | 210   | 0     | 0.58   |
| Phison    | BPX                | 240 GB | 1       | 208   | 0     | 0.57   |
| WDC       | WDS250G1B0C-00S6U0 | 250 GB | 1       | 207   | 0     | 0.57   |
| Intel     | SSDPE2MX450G7      | 450 GB | 2       | 204   | 0     | 0.56   |
| Samsung   | MZVLW128HEGR-00000 | 128 GB | 2       | 198   | 0     | 0.54   |
| Samsung   | MZVLW1T0HMLH-000L2 | 1 TB   | 2       | 193   | 0     | 0.53   |
| Intel     | SSDPEKKF010T8      | 1 TB   | 5       | 191   | 0     | 0.53   |
| Samsung   | MZVLW512HMJP-000L2 | 512 GB | 5       | 190   | 0     | 0.52   |
| WDC       | WDS500G2X0C-00L350 | 500 GB | 6       | 189   | 0     | 0.52   |
| Intel     | MEMPEK1J016GAL     | 16 GB  | 5       | 183   | 0     | 0.50   |
| WDC       | WDBRPG5000ANC-WRSN | 500 GB | 1       | 183   | 0     | 0.50   |
| Corsair   | Force MP500        | 240 GB | 3       | 177   | 0     | 0.49   |
| Toshiba   | THNSN5256GPU7 NVMe | 256 GB | 2       | 176   | 0     | 0.48   |
| Team      | M8FP2              | 480 GB | 1       | 172   | 0     | 0.47   |
| Corsair   | Force MP510        | 240 GB | 1       | 170   | 0     | 0.47   |
| Toshiba   | KXG50PNV2T04       | 2 TB   | 2       | 167   | 0     | 0.46   |
| Toshiba   | KXG50ZNV256G NVMe  | 256 GB | 10      | 164   | 0     | 0.45   |
| Toshiba   | THNSN5256GPUK      | 256 GB | 2       | 157   | 0     | 0.43   |
| HP        | SSD EX950          | 2 TB   | 1       | 156   | 0     | 0.43   |
| Toshiba   | THNSN5512GPUK      | 512 GB | 1       | 152   | 0     | 0.42   |
| Intel     | SSDPEKKW256G8      | 256 GB | 13      | 151   | 0     | 0.42   |
| Samsung   | SM951 NVMe         | 256 GB | 1       | 150   | 0     | 0.41   |
| Kingston  | SKC1000240G        | 240 GB | 1       | 148   | 0     | 0.41   |
| Samsung   | SSD 960 PRO        | 2 TB   | 5       | 164   | 10    | 0.41   |
| Toshiba   | KXG50ZNV1T02       | 1 TB   | 2       | 147   | 0     | 0.40   |
| Lite-On   | CX2-8B512-Q11 NVMe | 512 GB | 1       | 145   | 0     | 0.40   |
| Samsung   | MZVLV256HCHP-000H1 | 256 GB | 4       | 141   | 0     | 0.39   |
| Kingston  | SA1000M8480G       | 480 GB | 3       | 141   | 0     | 0.39   |
| Kingston  | SKC1000480G        | 480 GB | 2       | 131   | 0     | 0.36   |
| Intel     | SSDPEKKW128G8      | 128 GB | 9       | 130   | 0     | 0.36   |
| Samsung   | SSD 960 EVO        | 500 GB | 30      | 132   | 1     | 0.36   |
| KIOXIA    | KBG40ZPZ512G NVMe  | 512 GB | 1       | 129   | 0     | 0.35   |
| Samsung   | MZVPV512HDGL-000H1 | 512 GB | 1       | 122   | 0     | 0.34   |
| Phison    | BPXP               | 960 GB | 2       | 122   | 0     | 0.33   |
| Mushkin   | MKNSSDPL1TB-D8     | 1 TB   | 1       | 121   | 0     | 0.33   |
| Intel     | MEMPEK1W016GA      | 16 GB  | 2       | 118   | 0     | 0.33   |
| Toshiba   | KXG60ZNV512G NVMe  | 512 GB | 11      | 118   | 0     | 0.32   |
| Samsung   | MZVKW512HMJP-000H1 | 512 GB | 2       | 117   | 0     | 0.32   |
| Samsung   | MZVKV512HAJH-000L1 | 512 GB | 2       | 112   | 0     | 0.31   |
| SK hynix  | HFS256GD9MNE-6200A | 256 GB | 1       | 107   | 0     | 0.29   |
| Toshiba   | KBG40ZPZ512G NVMe  | 512 GB | 1       | 107   | 0     | 0.29   |
| Plextor   | PX-128M8PeGN       | 128 GB | 1       | 106   | 0     | 0.29   |
| Samsung   | SSD 960 PRO        | 1 TB   | 3       | 103   | 0     | 0.28   |
| PNY       | CS3030 2TB SSD     | 2 TB   | 2       | 103   | 0     | 0.28   |
| Intel     | MEMPEK1J016GA      | 16 GB  | 1       | 102   | 0     | 0.28   |
| Samsung   | PM961 NVMe         | 512 GB | 4       | 108   | 1     | 0.28   |
| Intel     | H10 HBRPEKNX020... | 512 GB | 1       | 99    | 0     | 0.27   |
| Plextor   | PX-256M9PeGN       | 256 GB | 2       | 98    | 0     | 0.27   |
| Goodram   | SSDPR-PX400-256-80 | 256 GB | 1       | 97    | 0     | 0.27   |
| Samsung   | MZVLB2T0HMLB-000L2 | 2 TB   | 1       | 96    | 0     | 0.27   |
| SK hynix  | PC300 NVMe         | 512 GB | 1       | 96    | 0     | 0.26   |
| Toshiba   | KXG50ZNV512G       | 512 GB | 4       | 96    | 0     | 0.26   |
| SK hynix  | PC601 NVMe         | 1 TB   | 1       | 94    | 0     | 0.26   |
| Samsung   | MZVPW256HEGL-00000 | 256 GB | 7       | 93    | 0     | 0.26   |
| Lenovo    | LENSE20512GMSP3... | 512 GB | 3       | 91    | 0     | 0.25   |
| Intel     | SSDPEDMW400G4      | 400 GB | 1       | 86    | 0     | 0.24   |
| Toshiba   | THNSN5256GPU7      | 256 GB | 1       | 85    | 0     | 0.23   |
| Plextor   | PX-256M9PeG        | 256 GB | 1       | 85    | 0     | 0.23   |
| SK hynix  | PC401 NVMe         | 512 GB | 9       | 85    | 0     | 0.23   |
| Corsair   | Force MP510        | 960 GB | 4       | 84    | 0     | 0.23   |
| Phison    | PCIe SSD           | 1 TB   | 6       | 84    | 0     | 0.23   |
| Toshiba   | KBG30ZMT128G       | 128 GB | 5       | 83    | 0     | 0.23   |
| Intel     | SSDPEKNW010T8H     | 1 TB   | 1       | 82    | 0     | 0.23   |
| Samsung   | MZFLV128HCGR-000MV | 128 GB | 4       | 81    | 0     | 0.22   |
| Samsung   | MZVLV128HCGR-00000 | 128 GB | 1       | 81    | 0     | 0.22   |
| Silico... | 1TB PCS PCIe M.... | 1 TB   | 1       | 81    | 0     | 0.22   |
| Intel     | SSDPEKKW512G8      | 512 GB | 9       | 80    | 0     | 0.22   |
| Samsung   | MZVPV256HDGL-000L2 | 256 GB | 1       | 80    | 0     | 0.22   |
| Phison    | Sabrent Rocket 4.0 | 1 TB   | 5       | 79    | 0     | 0.22   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 1       | 78    | 0     | 0.22   |
| Intel     | SSDPEKKW512G7      | 512 GB | 2       | 78    | 0     | 0.21   |
| Crucial   | CT500P1SSD8        | 500 GB | 12      | 85    | 6     | 0.21   |
| ADATA     | SX8200PNP          | 1 TB   | 5       | 77    | 0     | 0.21   |
| ADATA     | SX6000PNP          | 256 GB | 1       | 76    | 0     | 0.21   |
| Samsung   | MZVLW128HEGR-000H1 | 128 GB | 2       | 76    | 0     | 0.21   |
| Lite-On   | CB1-SD512          | 512 GB | 1       | 75    | 0     | 0.21   |
| WDC       | WDS250G3X0C-00SJG0 | 250 GB | 2       | 74    | 0     | 0.20   |
| Plextor   | PX-256M8PeY        | 256 GB | 2       | 73    | 0     | 0.20   |
| Samsung   | SSD 960 PRO        | 512 GB | 20      | 100   | 8     | 0.20   |
| SK hynix  | PC300 NVMe         | 1 TB   | 2       | 73    | 0     | 0.20   |
| Gigabyte  | GP-ASM2NE6100TTTD  | 1 TB   | 2       | 72    | 0     | 0.20   |
| Samsung   | MZVLW256HEHP-00000 | 256 GB | 13      | 71    | 0     | 0.20   |
| Samsung   | SSD 970 PRO        | 512 GB | 31      | 73    | 1     | 0.20   |
| Transcend | TS512GMTE220S      | 512 GB | 1       | 70    | 0     | 0.19   |
| ADATA     | SX6000PNP          | 512 GB | 2       | 70    | 0     | 0.19   |
| Samsung   | SSD 970 EVO        | 250 GB | 30      | 78    | 6     | 0.19   |
| Intel     | SSDPEKNW010T8      | 1 TB   | 33      | 67    | 0     | 0.18   |
| ADATA     | SX8200NP           | 480 GB | 2       | 67    | 0     | 0.18   |
| WDC       | PC SN520 SDAPMU... | 512 GB | 1       | 66    | 0     | 0.18   |
| Lenovo    | LENSE20256GMSP3... | 256 GB | 2       | 64    | 0     | 0.18   |
| Samsung   | SSD 960 EVO        | 1 TB   | 15      | 66    | 2     | 0.18   |
| WDC       | PC SN520 NVMe      | 256 GB | 5       | 64    | 0     | 0.18   |
| Crucial   | CT1000P1SSD8       | 1 TB   | 21      | 90    | 4     | 0.18   |
| Samsung   | KUS020203M-B000    | 128 GB | 1       | 64    | 0     | 0.18   |
| Plextor   | PX-512M9PeY        | 512 GB | 2       | 62    | 0     | 0.17   |
| Corsair   | Force MP600        | 1 TB   | 1       | 61    | 0     | 0.17   |
| Toshiba   | KXG60ZNV256G NVMe  | 256 GB | 4       | 61    | 0     | 0.17   |
| KIOXIA    | KBG40ZPZ1T02 NVMe  | 1 TB   | 1       | 60    | 0     | 0.17   |
| Phison    | M.2 PCIE G3x4 NVMe | 1 TB   | 1       | 60    | 0     | 0.16   |
| Kingch... | 256GB              | 256 GB | 1       | 60    | 0     | 0.16   |
| WDC       | WDS500G1B0C-00S6U0 | 500 GB | 3       | 58    | 0     | 0.16   |
| Toshiba   | KXG60ZNV1T02       | 1 TB   | 2       | 58    | 0     | 0.16   |
| WDC       | WDS100T3XHC-00SJG0 | 1 TB   | 1       | 58    | 0     | 0.16   |
| Samsung   | MZVKW512HMJP-000L7 | 512 GB | 1       | 58    | 0     | 0.16   |
| Micron    | 2200S NVMe         | 256 GB | 1       | 58    | 0     | 0.16   |
| Hikvision | HS-SSD-C2000Pro    | 1 TB   | 1       | 58    | 0     | 0.16   |
| Phison    | SBX                | 256 GB | 1       | 58    | 0     | 0.16   |
| Silico... | NE-512             | 512 GB | 2       | 58    | 0     | 0.16   |
| Gigabyte  | GP-GSM2NE8256GNTD  | 256 GB | 1       | 57    | 0     | 0.16   |
| WDC       | WDS500G2B0C-00PXH0 | 500 GB | 3       | 57    | 0     | 0.16   |
| WDC       | WDS500G3XHC-00SJG0 | 500 GB | 1       | 57    | 0     | 0.16   |
| ADATA     | SX6000NP           | 128 GB | 2       | 170   | 81    | 0.16   |
| HP        | SSD EX900          | 250 GB | 1       | 56    | 0     | 0.16   |
| Samsung   | PM981 NVMe         | 1 TB   | 1       | 56    | 0     | 0.15   |
| Intel     | SSDPEKNW512G8      | 512 GB | 30      | 56    | 0     | 0.15   |
| Seagate   | FireCuda 510 SS... | 2 TB   | 1       | 56    | 0     | 0.15   |
| Toshiba   | KBG30ZMS256G NVMe  | 256 GB | 5       | 54    | 0     | 0.15   |
| Toshiba   | KXG60ZNV512G       | 512 GB | 2       | 54    | 0     | 0.15   |
| Intel     | SSDPE2KX040T8      | 4 TB   | 4       | 53    | 0     | 0.15   |
| Kingston  | RBUSNS8154P3102... | 1 TB   | 1       | 53    | 0     | 0.15   |
| Toshiba   | KBG40ZNS512G NVMe  | 512 GB | 2       | 52    | 0     | 0.14   |
| ADATA     | SX8200PNP          | 256 GB | 8       | 52    | 0     | 0.14   |
| HP        | SSD EX920          | 512 GB | 2       | 51    | 0     | 0.14   |
| Samsung   | SSD 970 PRO        | 1 TB   | 19      | 50    | 0     | 0.14   |
| Samsung   | SSD 970 EVO        | 1 TB   | 39      | 51    | 1     | 0.14   |
| Toshiba   | KXG50ZNV256G       | 256 GB | 3       | 50    | 0     | 0.14   |
| Kingston  | SA2000M8500G       | 500 GB | 3       | 49    | 0     | 0.14   |
| Phison    | Sabrent            | 1 TB   | 11      | 48    | 0     | 0.13   |
| Samsung   | SSD 960 EVO        | 250 GB | 42      | 49    | 3     | 0.13   |
| PNY       | CS3030 500GB SSD   | 500 GB | 2       | 46    | 0     | 0.13   |
| Intel     | SSDPE2KE020T7      | 2 TB   | 4       | 46    | 0     | 0.13   |
| Toshiba   | KBG40ZNS256G NVMe  | 256 GB | 4       | 45    | 0     | 0.12   |
| ADATA     | SX8200PNP          | 512 GB | 10      | 44    | 0     | 0.12   |
| HP        | SSD EX920          | 1 TB   | 4       | 44    | 0     | 0.12   |
| SPCC      | M.2 PCIe SSD       | 512 GB | 2       | 44    | 0     | 0.12   |
| Intel     | SSDPEKKF512G7H     | 512 GB | 1       | 44    | 0     | 0.12   |
| XPG       | GAMMIX S5          | 256 GB | 2       | 43    | 0     | 0.12   |
| Samsung   | MZVLW512HMJP-000H1 | 512 GB | 1       | 43    | 0     | 0.12   |
| Apple     | SSD AP0032H        | 24 GB  | 1       | 42    | 0     | 0.12   |
| Samsung   | SSD 970 EVO        | 500 GB | 56      | 42    | 1     | 0.11   |
| Samsung   | MZVLB1T0HALR-000L7 | 1 TB   | 7       | 40    | 0     | 0.11   |
| Samsung   | MZVLW512HMJP-00000 | 512 GB | 4       | 48    | 1     | 0.11   |
| Plextor   | PX-512M8PeG        | 512 GB | 2       | 98    | 275   | 0.11   |
| Samsung   | MZVLB512HAJQ-000L7 | 512 GB | 25      | 40    | 1     | 0.11   |
| Samsung   | MZVLB1T0HALR-000L2 | 1 TB   | 7       | 39    | 0     | 0.11   |
| Intel     | SSDPEKKW010T7      | 1 TB   | 1       | 39    | 0     | 0.11   |
| Lexar     | 500GB SSD          | 500 GB | 1       | 39    | 0     | 0.11   |
| XPG       | GAMMIX S11 Pro     | 1 TB   | 11      | 39    | 0     | 0.11   |
| Intel     | HBRPEKNX0202AHO    | 32 GB  | 4       | 38    | 0     | 0.11   |
| HP        | SSD EX900          | 500 GB | 1       | 38    | 0     | 0.10   |
| WDC       | WDS100T3X0C-00SJG0 | 1 TB   | 3       | 37    | 0     | 0.10   |
| Samsung   | MZVLW256HEHP-000H1 | 256 GB | 10      | 37    | 0     | 0.10   |
| Samsung   | MZVLB1T0HALR-00000 | 1 TB   | 7       | 38    | 1     | 0.10   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 5       | 37    | 0     | 0.10   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 2       | 36    | 0     | 0.10   |
| Toshiba   | KXG50PNV2T04 NV... | 2 TB   | 2       | 36    | 0     | 0.10   |
| SK hynix  | PC601 NVMe         | 256 GB | 2       | 36    | 0     | 0.10   |
| Samsung   | PM981 NVMe         | 512 GB | 6       | 35    | 0     | 0.10   |
| Kingston  | RBUSNS8154P3128GJ  | 128 GB | 6       | 35    | 0     | 0.10   |
| Toshiba   | KBG30ZMV256G       | 256 GB | 4       | 35    | 0     | 0.10   |
| Samsung   | MZVLB256HAHQ-000L7 | 256 GB | 10      | 35    | 0     | 0.10   |
| Samsung   | MZQLB1T9HAJR-00007 | 1.9 TB | 4       | 35    | 0     | 0.10   |
| ADATA     | SX8200NP           | 240 GB | 2       | 108   | 59    | 0.10   |
| Intel     | SSDPEKKF256G8L     | 256 GB | 16      | 33    | 0     | 0.09   |
| Intel     | HBRPEKNX0202AH     | 512 GB | 5       | 32    | 0     | 0.09   |
| Silico... | M Series NVMe S... | 256 GB | 2       | 32    | 0     | 0.09   |
| Intel     | SSDPEKKW256G8L     | 256 GB | 1       | 31    | 0     | 0.09   |
| Intel     | HBRPEKNX0202ALO    | 32 GB  | 1       | 31    | 0     | 0.09   |
| Samsung   | MZVLB256HAHQ-00000 | 256 GB | 10      | 31    | 0     | 0.09   |
| SPCC      | M.2 PCIe SSD       | 256 GB | 1       | 30    | 0     | 0.08   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 9       | 29    | 0     | 0.08   |
| Intel     | MEMPEK1J016GAH     | 16 GB  | 1       | 29    | 0     | 0.08   |
| Samsung   | PM981 NVMe         | 256 GB | 5       | 29    | 0     | 0.08   |
| Samsung   | MZVLW256HEHP-000L2 | 256 GB | 9       | 28    | 0     | 0.08   |
| Silico... | JAMESDONKEY JD512  | 512 GB | 1       | 28    | 0     | 0.08   |
| HP        | SSD EX950          | 1 TB   | 3       | 28    | 0     | 0.08   |
| Patriot   | Scorch M2          | 256 GB | 1       | 28    | 0     | 0.08   |
| Apple     | SSD AP0512M        | 500 GB | 1       | 27    | 0     | 0.08   |
| ADATA     | IM2P33F3 NVMe      | 256 GB | 2       | 27    | 0     | 0.08   |
| WDC       | PC SN520 NVMe      | 512 GB | 4       | 27    | 0     | 0.08   |
| WDC       | WDS200T3X0C-00SJG0 | 2 TB   | 1       | 27    | 0     | 0.08   |
| Samsung   | MZVKW1T0HMLH-000H1 | 1 TB   | 1       | 27    | 0     | 0.07   |
| Intel     | SSDPEKKF256G8 NVMe | 256 GB | 1       | 26    | 0     | 0.07   |
| Samsung   | MZVKW1T0HMLH-00000 | 1 TB   | 1       | 26    | 0     | 0.07   |
| WDC       | PC SN520 SDAPMU... | 512 GB | 9       | 26    | 0     | 0.07   |
| Toshiba   | KBG30ZMV512G       | 512 GB | 2       | 26    | 0     | 0.07   |
| WDC       | PC SN720 SDAQNT... | 512 GB | 6       | 25    | 0     | 0.07   |
| Intel     | SSDPEKNW512G8H     | 512 GB | 20      | 25    | 3     | 0.07   |
| Samsung   | SSD 970 EVO Plus   | 2 TB   | 4       | 25    | 0     | 0.07   |
| Toshiba   | KBG30ZMT512G       | 512 GB | 2       | 24    | 0     | 0.07   |
| Phison    | Viper M.2 VPN100   | 1 TB   | 2       | 24    | 0     | 0.07   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 4       | 24    | 0     | 0.07   |
| Samsung   | SSD 970 EVO        | 2 TB   | 3       | 185   | 14    | 0.07   |
| Samsung   | MZ1LB3T8HMLA-00007 | 3.8 TB | 2       | 23    | 0     | 0.06   |
| SK hynix  | BA HFS256GD9TNG... | 256 GB | 2       | 23    | 0     | 0.06   |
| Kingston  | OM8PCP3512F-AB     | 512 GB | 3       | 22    | 0     | 0.06   |
| SK hynix  | PC601 NVMe         | 512 GB | 10      | 22    | 0     | 0.06   |
| ADATA     | SX6000LNP          | 512 GB | 2       | 22    | 0     | 0.06   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 3       | 22    | 0     | 0.06   |
| Samsung   | MZVLW512HMJP-000L7 | 512 GB | 3       | 26    | 1     | 0.06   |
| Intel     | SSDPEMKF010T8 NVMe | 1 TB   | 3       | 22    | 0     | 0.06   |
| Apple     | SSD SM0512L        | 500 GB | 1       | 22    | 0     | 0.06   |
| Lite-On   | CL1-4D256          | 256 GB | 1       | 22    | 0     | 0.06   |
| Intel     | SSDPEKNW512G8L     | 512 GB | 5       | 21    | 0     | 0.06   |
| Toshiba   | KXG60ZNV1T02 NVMe  | 1 TB   | 1       | 21    | 0     | 0.06   |
| HP        | SSD EX900          | 120 GB | 2       | 21    | 0     | 0.06   |
| Union ... | RPFTJ128PDD2EWX    | 128 GB | 8       | 21    | 0     | 0.06   |
| ADATA     | SX6000LNP          | 256 GB | 4       | 21    | 0     | 0.06   |
| Silico... | R5MP240G8          | 240 GB | 2       | 21    | 0     | 0.06   |
| Corsair   | Force MP600        | 2 TB   | 1       | 21    | 0     | 0.06   |
| Samsung   | KUS030202M-B000    | 256 GB | 1       | 20    | 0     | 0.06   |
| Samsung   | MZVLW1T0HMLH-000L7 | 1 TB   | 2       | 48    | 8     | 0.06   |
| Intel     | SSDPEKKF010T8 NVMe | 1 TB   | 1       | 20    | 0     | 0.06   |
| SK hynix  | HFM256GDHTNG-8310A | 256 GB | 3       | 20    | 0     | 0.06   |
| SK hynix  | BC501 NVMe         | 128 GB | 3       | 20    | 0     | 0.06   |
| WDC       | PC SN720 SDAQNT... | 256 GB | 2       | 20    | 0     | 0.06   |
| Silico... | OSC PCIE           | 512 GB | 1       | 19    | 0     | 0.05   |
| Kingston  | SA1000M8240G       | 240 GB | 3       | 19    | 0     | 0.05   |
| Micron    | 2200S NVMe         | 1 TB   | 2       | 19    | 0     | 0.05   |
| SK hynix  | PC401 HFS256GD9... | 256 GB | 2       | 19    | 0     | 0.05   |
| Samsung   | MZVLB1T0HALR-000H1 | 1 TB   | 2       | 18    | 0     | 0.05   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 2       | 18    | 0     | 0.05   |
| Samsung   | SSD 970 EVO Plus   | 1 TB   | 48      | 18    | 0     | 0.05   |
| Samsung   | MZVLB512HAJQ-00000 | 512 GB | 14      | 18    | 0     | 0.05   |
| Lenovo    | LENSE30512GMSP3... | 512 GB | 1       | 18    | 0     | 0.05   |
| Samsung   | MZVLW256HEHP-000L7 | 256 GB | 6       | 24    | 6     | 0.05   |
| Intel     | SSDPEKKF512G8L     | 512 GB | 11      | 17    | 0     | 0.05   |
| Samsung   | SSD 970 EVO Plus   | 500 GB | 55      | 17    | 0     | 0.05   |
| Intel     | HBRPEKNX0202AL     | 512 GB | 2       | 17    | 0     | 0.05   |
| WDC       | WDS500G3X0C-00SJG0 | 500 GB | 6       | 17    | 0     | 0.05   |
| Transcend | TS512GMTE110S      | 512 GB | 1       | 17    | 0     | 0.05   |
| SK hynix  | PC611 NVMe         | 512 GB | 2       | 16    | 0     | 0.05   |
| Toshiba   | KXG6AZNV512G       | 512 GB | 5       | 16    | 0     | 0.05   |
| SK hynix  | HFS256GD9TNG-62A0A | 256 GB | 2       | 16    | 0     | 0.04   |
| Silico... | KingSSD-N201000    | 1 TB   | 1       | 16    | 0     | 0.04   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 2       | 16    | 0     | 0.04   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 4       | 16    | 0     | 0.04   |
| Colorful  | CN600S             | 480 GB | 1       | 16    | 0     | 0.04   |
| Intel     | SSDPEKKW010T8      | 1 TB   | 2       | 16    | 0     | 0.04   |
| SK hynix  | PC601 HFS512GD9... | 512 GB | 6       | 16    | 0     | 0.04   |
| Toshiba   | KXG60ZNV512G NV... | 512 GB | 3       | 16    | 0     | 0.04   |
| PNY       | CS3030 250GB SSD   | 250 GB | 1       | 16    | 0     | 0.04   |
| Micron    | MTFDHBA512TCK      | 512 GB | 1       | 15    | 0     | 0.04   |
| ADATA     | SX6000PNP          | 1 TB   | 4       | 15    | 0     | 0.04   |
| WDC       | PC SN520 SDAPMU... | 256 GB | 5       | 15    | 0     | 0.04   |
| SK hynix  | BA HFS512GD9TNG... | 512 GB | 1       | 15    | 0     | 0.04   |
| ADATA     | IM2P33F3 NVMe      | 512 GB | 1       | 15    | 0     | 0.04   |
| WDC       | PC SN520 NVMe      | 128 GB | 3       | 15    | 0     | 0.04   |
| FORESEE   | 256GB SSD          | 256 GB | 2       | 15    | 0     | 0.04   |
| Kingston  | RBUSNS8154P3512GJ  | 512 GB | 2       | 15    | 0     | 0.04   |
| Samsung   | MZVLW1T0HMLH-000H1 | 1 TB   | 1       | 15    | 0     | 0.04   |
| SK hynix  | PC300 NVMe         | 256 GB | 2       | 45    | 3     | 0.04   |
| ADATA     | SX8200PNP          | 2 TB   | 2       | 14    | 0     | 0.04   |
| Samsung   | MZVLB512HAJQ-000H1 | 512 GB | 23      | 14    | 0     | 0.04   |
| Corsair   | Force MP510        | 480 GB | 5       | 14    | 0     | 0.04   |
| Samsung   | MZVLW128HEGR-000L2 | 128 GB | 3       | 14    | 0     | 0.04   |
| Samsung   | PM961 NVMe         | 256 GB | 1       | 13    | 0     | 0.04   |
| Samsung   | SSD 970 EVO Plus   | 250 GB | 30      | 13    | 0     | 0.04   |
| Samsung   | MZVLB2T0HALB-000L7 | 2 TB   | 2       | 13    | 0     | 0.04   |
| Toshiba   | KBG30ZMV128G       | 128 GB | 1       | 13    | 0     | 0.04   |
| Silico... | NE-128             | 128 GB | 1       | 13    | 0     | 0.04   |
| Transcend | TS1TMTE220S        | 1 TB   | 1       | 12    | 0     | 0.03   |
| WDC       | PC SN520 SDAPMU... | 512 GB | 1       | 12    | 0     | 0.03   |
| Lite-On   | CA1-8D128-HP       | 128 GB | 1       | 12    | 0     | 0.03   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 1       | 12    | 0     | 0.03   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 14      | 12    | 75    | 0.03   |
| Patriot   | Scorch M2          | 512 GB | 1       | 12    | 0     | 0.03   |
| Toshiba   | KBG30ZMS128G NVMe  | 128 GB | 2       | 11    | 0     | 0.03   |
| Transcend | TS256GMTE220S      | 256 GB | 2       | 11    | 0     | 0.03   |
| Intel     | SSDPEMKF512G8 NVMe | 512 GB | 5       | 11    | 0     | 0.03   |
| Micron    | 2200_MTFDHBA512TCK | 512 GB | 1       | 11    | 0     | 0.03   |
| Samsung   | PM981a NVMe        | 256 GB | 1       | 11    | 0     | 0.03   |
| Kingston  | RBUSNS8154P3256GJ3 | 256 GB | 5       | 11    | 0     | 0.03   |
| WDC       | CL SN720 SDAQNT... | 1 TB   | 1       | 11    | 0     | 0.03   |
| Intel     | SSDPEKKF010T8L     | 1 TB   | 11      | 10    | 0     | 0.03   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 4       | 10    | 0     | 0.03   |
| Silico... | Qunion P20A 512... | 512 GB | 1       | 10    | 0     | 0.03   |
| Toshiba   | KBG30ZMT256G       | 256 GB | 1       | 10    | 0     | 0.03   |
| Samsung   | MZVLB1T0HBLR-000L2 | 1 TB   | 6       | 10    | 0     | 0.03   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 2       | 10    | 0     | 0.03   |
| Apple     | SSD SM0256L        | 256 GB | 1       | 10    | 0     | 0.03   |
| Seagate   | IronWolf510 ZP9... | 960 GB | 2       | 10    | 0     | 0.03   |
| Kingston  | SA2000M8250G       | 250 GB | 7       | 9     | 0     | 0.03   |
| Apple     | SSD AP0512N        | 500 GB | 1       | 9     | 0     | 0.03   |
| Kingston  | RBUSNS8154P3512GJ1 | 512 GB | 1       | 9     | 0     | 0.03   |
| SK hynix  | HFS512GD9TNG-62A0A | 512 GB | 1       | 8     | 0     | 0.02   |
| Phison    | Viper M.2 VPR100   | 512 GB | 1       | 8     | 0     | 0.02   |
| ADATA     | SX6000LNP          | 1 TB   | 2       | 8     | 0     | 0.02   |
| Samsung   | PM981a NVMe        | 512 GB | 6       | 8     | 0     | 0.02   |
| SK hynix  | BC511 NVMe         | 256 GB | 2       | 8     | 0     | 0.02   |
| Apple     | SSD SM0032L        | 32 GB  | 4       | 8     | 0     | 0.02   |
| Hikvision | HS-SSD-C2000Pro... | 1 TB   | 1       | 8     | 0     | 0.02   |
| Samsung   | MZVLB256HAHQ-000L2 | 256 GB | 8       | 8     | 0     | 0.02   |
| WDC       | PC SN720 SDAPNT... | 1 TB   | 2       | 8     | 0     | 0.02   |
| SK hynix  | BC501 HFM256GDJ... | 256 GB | 7       | 9     | 299   | 0.02   |
| Toshiba   | KBG40ZMT128G ME... | 128 GB | 1       | 8     | 0     | 0.02   |
| Toshiba   | KXG6AZNV256G       | 256 GB | 3       | 7     | 0     | 0.02   |
| Samsung   | MZVLB1T0HBLR-000L7 | 1 TB   | 23      | 7     | 0     | 0.02   |
| Intel     | HBRPEKNX0202AO     | 32 GB  | 2       | 7     | 0     | 0.02   |
| Apple     | SSD AP0256J        | 256 GB | 2       | 7     | 0     | 0.02   |
| Samsung   | MZVLB256HAHQ-000H1 | 256 GB | 20      | 7     | 0     | 0.02   |
| WDC       | PC SN520 SDAPMU... | 256 GB | 1       | 7     | 0     | 0.02   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 3       | 7     | 0     | 0.02   |
| Toshiba   | KXG60ZNV256G       | 256 GB | 1       | 7     | 0     | 0.02   |
| Samsung   | MZALQ512HALU-000L1 | 512 GB | 4       | 7     | 0     | 0.02   |
| Samsung   | MZALQ512HALU-000L2 | 512 GB | 3       | 7     | 0     | 0.02   |
| KIOXIA    | KBG40ZNS256G NVMe  | 256 GB | 3       | 7     | 0     | 0.02   |
| Intel     | HBRPEKNX0202A      | 512 GB | 2       | 7     | 0     | 0.02   |
| Phison    | Sabrent Rocket Q   | 2 TB   | 3       | 6     | 0     | 0.02   |
| Micron    | 2200_MTFDHBA256TCK | 256 GB | 2       | 6     | 0     | 0.02   |
| SPCC      | M.2 PCIE SSD       | 1 TB   | 1       | 6     | 0     | 0.02   |
| Samsung   | PM981a NVMe SED    | 512 GB | 1       | 5     | 0     | 0.02   |
| Team      | TM8FP4256G         | 256 GB | 1       | 5     | 0     | 0.02   |
| Samsung   | MZVLB512HAJQ-000L2 | 512 GB | 5       | 5     | 0     | 0.02   |
| Samsung   | MZVLB512HBJQ-000L7 | 512 GB | 15      | 5     | 0     | 0.02   |
| Toshiba   | KBG30ZMV512G KI... | 512 GB | 2       | 5     | 0     | 0.02   |
| WDC       | PC SN730 SDBQNT... | 256 GB | 2       | 5     | 0     | 0.02   |
| Toshiba   | RC500              | 500 GB | 1       | 5     | 0     | 0.01   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 5       | 5     | 0     | 0.01   |
| PNY       | CS3030 2000GB SSD  | 2 TB   | 1       | 5     | 0     | 0.01   |
| Samsung   | MZVLB512HBJQ-000L2 | 512 GB | 11      | 5     | 0     | 0.01   |
| Micron    | 2200S NVMe         | 512 GB | 3       | 5     | 0     | 0.01   |
| WDC       | PC SN730 SDBQNT... | 512 GB | 13      | 5     | 0     | 0.01   |
| Intel     | SSDPE2KX020T8      | 2 TB   | 2       | 5     | 0     | 0.01   |
| SPCC      | M.2 PCIe SSD       | 1 TB   | 1       | 5     | 0     | 0.01   |
| SK hynix  | BC501A NVMe        | 128 GB | 2       | 5     | 0     | 0.01   |
| Silico... | R5MP120G8          | 120 GB | 1       | 5     | 0     | 0.01   |
| Phison    | SBXe               | 480 GB | 1       | 4     | 0     | 0.01   |
| Samsung   | PM981 NVMe SED     | 512 GB | 1       | 4     | 0     | 0.01   |
| WDC       | PC SN520 SDAPMU... | 128 GB | 2       | 4     | 0     | 0.01   |
| Corsair   | Force MP600        | 500 GB | 2       | 4     | 0     | 0.01   |
| SK hynix  | HFM256GDHTNG-8510B | 256 GB | 1       | 4     | 0     | 0.01   |
| Toshiba   | KBG30ZMV256G KI... | 256 GB | 4       | 4     | 0     | 0.01   |
| ADATA     | SX6000NP           | 512 GB | 2       | 4     | 0     | 0.01   |
| Samsung   | PM981a NVMe        | 1 TB   | 2       | 4     | 0     | 0.01   |
| Lite-On   | CL1-3D128-Q11 NVMe | 128 GB | 1       | 4     | 0     | 0.01   |
| Intel     | HBRPEKNX0203AHO    | 32 GB  | 1       | 3     | 0     | 0.01   |
| Samsung   | MZVLB256HBHQ-000L2 | 256 GB | 6       | 3     | 0     | 0.01   |
| Lite-On   | CA3-8D256          | 256 GB | 2       | 3     | 0     | 0.01   |
| SK hynix  | PC401 NVMe         | 1 TB   | 1       | 3     | 0     | 0.01   |
| KIOXIA    | KBG40ZNS512G NVMe  | 512 GB | 3       | 3     | 0     | 0.01   |
| Samsung   | MZVLB512HAJQ-000H7 | 512 GB | 4       | 3     | 0     | 0.01   |
| Intel     | HBRPEKNX0203AH     | 1 TB   | 1       | 3     | 0     | 0.01   |
| SK hynix  | BC501 HFM512GDJ... | 512 GB | 7       | 3     | 0     | 0.01   |
| Gigabyte  | GP-ASM2NE6500GTTD  | 500 GB | 1       | 3     | 0     | 0.01   |
| Gigabyte  | GP-GSM2NE8128GNTD  | 128 GB | 1       | 3     | 0     | 0.01   |
| Kingston  | SA2000M81000G      | 1 TB   | 2       | 2     | 0     | 0.01   |
| Samsung   | MZVLB256HBHQ-000L7 | 256 GB | 9       | 2     | 0     | 0.01   |
| SanDisk   | Extreme Pro        | 500 GB | 1       | 2     | 0     | 0.01   |
| Lite-On   | CA3-8D512          | 512 GB | 1       | 2     | 0     | 0.01   |
| Toshiba   | KXG60ZNV1T02 NV... | 1 TB   | 1       | 2     | 0     | 0.01   |
| Kingston  | RBUSNS8154P3256GJ1 | 256 GB | 3       | 2     | 0     | 0.01   |
| Toshiba   | KXG60ZNV512G KI... | 512 GB | 2       | 2     | 0     | 0.01   |
| Silico... | 256GB              | 256 GB | 1       | 2     | 0     | 0.01   |
| Lite-On   | CL1-3D256-Q11 NVMe | 256 GB | 2       | 2     | 0     | 0.01   |
| Micron    | MTFDHBA256TCK      | 256 GB | 1       | 2     | 0     | 0.01   |
| FORESEE   | P900F256GB         | 256 GB | 1       | 2     | 0     | 0.01   |
| Samsung   | MZVLB512HBJQ-000H1 | 512 GB | 2       | 2     | 0     | 0.01   |
| Silico... | NE-256             | 256 GB | 4       | 2     | 0     | 0.01   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 1       | 2     | 0     | 0.01   |
| WDC       | PC SN730 NVMe      | 1 TB   | 3       | 2     | 0     | 0.01   |
| Samsung   | MZALQ256HAJD-000L2 | 256 GB | 4       | 2     | 0     | 0.01   |
| Samsung   | MZALQ256HAJD-000L1 | 256 GB | 2       | 1     | 0     | 0.01   |
| Intel     | SSDPEKKA256G7      | 256 GB | 2       | 1     | 0     | 0.01   |
| Gigabyte  | GP-ASM2NE6200TTTD  | 2 TB   | 1       | 1     | 0     | 0.01   |
| SK hynix  | HFM512GDJTNG-8310A | 512 GB | 8       | 1     | 0     | 0.01   |
| Toshiba   | KBG30ZMV128G KI... | 128 GB | 1       | 1     | 0     | 0.00   |
| SK hynix  | BC501 NVMe         | 256 GB | 2       | 1     | 0     | 0.00   |
| Toshiba   | KXG6AZNV1T02       | 1 TB   | 1       | 1     | 0     | 0.00   |
| KIOXIA    | KBG40ZNV512G       | 512 GB | 1       | 1     | 0     | 0.00   |
| Lite-On   | CA3-8D128-HP       | 128 GB | 2       | 1     | 0     | 0.00   |
| Samsung   | MZALQ128HBHQ-000L2 | 128 GB | 2       | 1     | 0     | 0.00   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 1       | 1     | 0     | 0.00   |
| WDC       | WDS100T2X0C-00L350 | 1 TB   | 2       | 1     | 0     | 0.00   |
| Gigabyte  | GP-GSM2NE3100TNTD  | 1 TB   | 2       | 1     | 0     | 0.00   |
| ADATA     | SX6000LNP          | 128 GB | 1       | 1     | 0     | 0.00   |
| XPG       | SPECTRIX S40G      | 256 GB | 1       | 1     | 0     | 0.00   |
| Intel     | SSDPEDKE020T7      | 2 TB   | 2       | 1     | 0     | 0.00   |
| Samsung   | MZVLB1T0HBLR-00007 | 1 TB   | 1       | 1     | 0     | 0.00   |
| SK hynix  | HFS512GD9TNG-L2A0A | 512 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | MZVLQ512HALU-00000 | 512 GB | 4       | 1     | 0     | 0.00   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 2       | 1     | 0     | 0.00   |
| Micron    | MTFDHBA256TCK-1... | 256 GB | 6       | 4     | 1     | 0.00   |
| Union ... | RPFTJ256PDD2MWX    | 256 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | MZVPW128HEGM-00000 | 128 GB | 1       | 37    | 32    | 0.00   |
| SK hynix  | HFM512GDHTNG-8710B | 512 GB | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN520 SDAPMU... | 128 GB | 1       | 1     | 0     | 0.00   |
| Kingston  | OM8PCP3512F-AA     | 512 GB | 1       | 0     | 0     | 0.00   |
| Micron    | 2200V_MTFDHBA51... | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | BC511 NVMe         | 512 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVLB1T0HBLR-000H1 | 1 TB   | 1       | 0     | 0     | 0.00   |
| Transcend | TS256GMTE110S      | 256 GB | 1       | 0     | 0     | 0.00   |
| WDC       | WDS100T2B0C-00PXH0 | 1 TB   | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVLQ512HALU-000H1 | 512 GB | 3       | 0     | 0     | 0.00   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 2       | 0     | 0     | 0.00   |
| SK hynix  | BC501 NVMe         | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | HFM512GDHTNG-8310A | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | SKHynix_HFM256G... | 256 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | PM991 NVMe         | 512 GB | 1       | 0     | 0     | 0.00   |
| Lite-On   | CA1-8D256-HP       | 256 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | HFM256GDJTNG-8310A | 256 GB | 2       | 0     | 0     | 0.00   |
| Samsung   | MZVLQ256HAJD-000H1 | 256 GB | 2       | 0     | 0     | 0.00   |
| Zheino    | CHN-NGFFNV2280-256 | 256 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | RBUSNS8154P3128GJ1 | 128 GB | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 1       | 0     | 0     | 0.00   |
| Lenovo    | LENSE30256GMSP3... | 256 GB | 1       | 0     | 0     | 0.00   |
| Plextor   | PX-512M9PeGN       | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | Skhynix BC501 NVMe | 512 GB | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 1       | 0     | 0     | 0.00   |
| SPCC      | M.2 PCIE SSD       | 256 GB | 1       | 0     | 0     | 0.00   |
| FORESEE   | 512GB SSD          | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | SKHynix_HFM512G... | 512 GB | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN730 SDBQNT... | 1 TB   | 1       | 0     | 0     | 0.00   |
| Apple     | SSD AP0256M        | 256 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TS512GMTE510T      | 512 GB | 1       | 0     | 0     | 0.00   |
| Gigabyte  | GP-GSM2NE3512GNTD  | 512 GB | 1       | 0     | 0     | 0.00   |
| Mushkin   | MKNSSDPE1TB-D8     | 1 TB   | 1       | 0     | 0     | 0.00   |
| SK hynix  | HFM128GDHTNG-8310A | 128 GB | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVLQ256HAJD-00000 | 256 GB | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN730 NVMe      | 256 GB | 1       | 0     | 0     | 0.00   |
| Seagate   | FireCuda 510 SS... | 1 TB   | 1       | 0     | 0     | 0.00   |
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
| SanDisk     | 2      | 2       | 278   | 0     | 0.76   |
| Toshiba     | 51     | 139     | 141   | 0     | 0.39   |
| Mushkin     | 3      | 3       | 123   | 0     | 0.34   |
| XPG         | 4      | 18      | 108   | 0     | 0.30   |
| Intel       | 55     | 262     | 110   | 1     | 0.29   |
| Goodram     | 1      | 1       | 97    | 0     | 0.27   |
| Corsair     | 9      | 19      | 93    | 0     | 0.26   |
| Team        | 2      | 2       | 89    | 0     | 0.24   |
| Crucial     | 2      | 33      | 88    | 5     | 0.19   |
| Plextor     | 7      | 11      | 78    | 50    | 0.18   |
| Phison      | 11     | 34      | 61    | 0     | 0.17   |
| Lenovo      | 4      | 7       | 60    | 0     | 0.17   |
| Kingchuxing | 1      | 1       | 60    | 0     | 0.16   |
| Transcend   | 7      | 8       | 58    | 0     | 0.16   |
| Samsung     | 102    | 831     | 61    | 1     | 0.16   |
| PNY         | 4      | 6       | 53    | 0     | 0.15   |
| HP          | 7      | 14      | 47    | 0     | 0.13   |
| WDC         | 58     | 171     | 42    | 7     | 0.12   |
| ADATA       | 17     | 52      | 47    | 6     | 0.11   |
| Lexar       | 1      | 1       | 39    | 0     | 0.11   |
| Lite-On     | 11     | 14      | 36    | 0     | 0.10   |
| Kingston    | 16     | 44      | 35    | 0     | 0.10   |
| Hikvision   | 2      | 2       | 33    | 0     | 0.09   |
| SK hynix    | 39     | 97      | 26    | 22    | 0.07   |
| KIOXIA      | 5      | 9       | 24    | 0     | 0.07   |
| Gigabyte    | 7      | 9       | 23    | 0     | 0.07   |
| Silicon ... | 12     | 18      | 22    | 0     | 0.06   |
| SPCC        | 5      | 6       | 21    | 0     | 0.06   |
| Patriot     | 2      | 2       | 20    | 0     | 0.05   |
| Union Me... | 2      | 9       | 19    | 0     | 0.05   |
| Seagate     | 3      | 4       | 19    | 0     | 0.05   |
| Colorful    | 1      | 1       | 16    | 0     | 0.04   |
| Apple       | 8      | 12      | 13    | 0     | 0.04   |
| Micron      | 9      | 18      | 10    | 1     | 0.02   |
| FORESEE     | 3      | 4       | 8     | 0     | 0.02   |
| Zheino      | 1      | 1       | 0     | 0     | 0.00   |

