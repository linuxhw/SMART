HDD/SSD Desktop-Class Reliability Test
======================================

This is a project to estimate reliability of desktop-class HDD/SSD drives by
the analysis of SMART data collected by Linux users at https://linux-hardware.org. The
primary aim of the project is to find drives with longest power-on hours (POH) and
minimal number of errors, i.e. maximal MTBF (mean time between failures).

Everyone can contribute to this report by uploading probes of their computers by
the [hw-probe](https://github.com/linuxhw/hw-probe) tool:

    sudo -E hw-probe -all -upload

This is a report for consumer drives. Report for enterprise drives: [EnterpriseDrive](https://github.com/linuxhw/EnterpriseDrive)

Total drives: 145442.

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

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| Samsung   | HM020GI            | 20 GB  | 2       | 6601  | 0     | 18.09  |
| Samsung   | SV1021H            | 10 GB  | 1       | 5713  | 0     | 15.65  |
| Toshiba   | MQ01AAD020C        | 200 GB | 1       | 4449  | 0     | 12.19  |
| WDC       | WD7500AAVS-00D7B0  | 752 GB | 1       | 4362  | 0     | 11.95  |
| WDC       | WD3200AACS-00M6B0  | 320 GB | 1       | 4087  | 0     | 11.20  |
| Hitachi   | HCP725025GLAT80    | 250 GB | 1       | 4058  | 0     | 11.12  |
| Samsung   | HD754JJ            | 752 GB | 1       | 3908  | 0     | 10.71  |
| WDC       | WD3000HLHX-60JJPV0 | 304 GB | 1       | 3761  | 0     | 10.31  |
| WDC       | WD10EAVS-55D7B1    | 1 TB   | 1       | 3680  | 0     | 10.08  |
| Hitachi   | HUA721075KLA330    | 752 GB | 1       | 3668  | 0     | 10.05  |
| Hitachi   | HUA722020ALA330... | 2 TB   | 1       | 3566  | 0     | 9.77   |
| Hitachi   | HDS728040PLA320... | 40 GB  | 1       | 3563  | 0     | 9.76   |
| WDC       | WD2002FYPS-12      | 2 TB   | 1       | 3557  | 0     | 9.75   |
| Hitachi   | HUA7210SASUN1.0... | 1 TB   | 1       | 3495  | 0     | 9.58   |
| HP        | GB0160EAFJE        | 160 GB | 2       | 3447  | 0     | 9.44   |
| Samsung   | HM161HI            | 160 GB | 1       | 3308  | 0     | 9.06   |
| Hitachi   | HTS541680J9AT00    | 80 GB  | 1       | 3303  | 0     | 9.05   |
| WDC       | WD6400AAVS-00G9B0  | 640 GB | 2       | 3191  | 0     | 8.74   |
| Samsung   | HE160HJ            | 160 GB | 2       | 3097  | 0     | 8.49   |
| Seagate   | ST33000650NS 81... | 3 TB   | 1       | 2940  | 0     | 8.06   |
| WDC       | WD84AA             | 8 GB   | 1       | 2903  | 0     | 7.95   |
| WDC       | WD800AAJB-00J3A0   | 80 GB  | 1       | 2880  | 0     | 7.89   |
| WDC       | WD5000AAKS-60A7B0  | 500 GB | 2       | 2876  | 0     | 7.88   |
| WDC       | WD2500AAJS-62B4A0  | 250 GB | 1       | 2854  | 0     | 7.82   |
| Seagate   | ST4000DM000-1CD168 | 4 TB   | 1       | 2813  | 0     | 7.71   |
| WDC       | WD2500AVJB-63J5A0  | 250 GB | 1       | 2804  | 0     | 7.68   |
| WDC       | WD2500AAJS-00RYA0  | 250 GB | 1       | 2800  | 0     | 7.67   |
| WDC       | WD10EACS-14ZJB0    | 1 TB   | 1       | 2742  | 0     | 7.51   |
| WDC       | WD4000AAKS-00C8A0  | 400 GB | 1       | 2706  | 0     | 7.42   |
| WDC       | WD10EAVS-22D7B1    | 1 TB   | 1       | 2691  | 0     | 7.37   |
| HGST      | HUP722020APA330    | 2 TB   | 2       | 2688  | 0     | 7.36   |
| WDC       | WD20EZRX-19D8PB0   | 2 TB   | 1       | 2679  | 0     | 7.34   |
| Hitachi   | HUA7210SASUN1.0T   | 1 TB   | 12      | 2672  | 0     | 7.32   |
| WDC       | WD30EURS-73TLHY0   | 3 TB   | 1       | 2606  | 0     | 7.14   |
| WDC       | WD5000BUCT-63PUZY0 | 500 GB | 2       | 2600  | 0     | 7.13   |
| WDC       | WD10EVDS-63N5B1    | 1 TB   | 4       | 2541  | 0     | 6.96   |
| HP        | GB0500EAFYL        | 500 GB | 2       | 2969  | 1     | 6.86   |
| Seagate   | ST3750641NS EIT    | 752 GB | 1       | 2476  | 0     | 6.79   |
| WDC       | WD1002F9YZ-09H1JL0 | 1 TB   | 1       | 2469  | 0     | 6.76   |
| Hitachi   | HDS7216SBSUN160G   | 160 GB | 2       | 4110  | 2     | 6.76   |
| WDC       | WD7502ABYS-18A6B0  | 752 GB | 1       | 2416  | 0     | 6.62   |
| WDC       | WD1002FBYS-50A6B0  | 1 TB   | 2       | 2401  | 0     | 6.58   |
| WDC       | WD60EFRX-68MYMN0   | 6 TB   | 1       | 2399  | 0     | 6.58   |
| WDC       | WD40EZRX-00MVLB1   | 4 TB   | 1       | 2385  | 0     | 6.54   |
| Seagate   | ST4000VX000-1F4168 | 4 TB   | 1       | 2378  | 0     | 6.52   |
| WDC       | WD5000AVVS-63ZWB0  | 500 GB | 4       | 3388  | 12    | 6.49   |
| WDC       | WD2500AAJS-07VWA0  | 250 GB | 2       | 2354  | 0     | 6.45   |
| WDC       | WD1600YS-18SHB2    | 160 GB | 1       | 2341  | 0     | 6.41   |
| WDC       | WD1002FBYS-01A6B0  | 1 TB   | 13      | 3294  | 2     | 6.39   |
| WDC       | WD5001AALS-00J7B0  | 500 GB | 1       | 2295  | 0     | 6.29   |
| Toshiba   | MK2002TSKB         | 2 TB   | 9       | 2285  | 3     | 6.26   |
| WDC       | WD6400AAKS-40H2B0  | 640 GB | 10      | 2625  | 84    | 6.26   |
| WDC       | WD1600JS-75NCB1    | 160 GB | 1       | 2267  | 0     | 6.21   |
| WDC       | WD5000AAKS-40YGA1  | 500 GB | 2       | 2259  | 0     | 6.19   |
| Advantech | SQF-P10S2-8G       | 8 GB   | 1       | 2258  | 0     | 6.19   |
| Hitachi   | HDS724040ALE640    | 4 TB   | 8       | 2332  | 171   | 6.14   |
| WDC       | WD2500SD-01KCB0    | 250 GB | 2       | 2568  | 1     | 6.06   |
| Hitachi   | HDS722516VLAT80    | 164 GB | 1       | 2212  | 0     | 6.06   |
| Fujitsu   | MHT2040BH          | 40 GB  | 1       | 4417  | 1     | 6.05   |
| WDC       | WD1001FALS-00K1B0  | 1 TB   | 2       | 2199  | 0     | 6.02   |
| Hitachi   | HDS722020ALA330... | 2 TB   | 2       | 2191  | 0     | 6.00   |
| Seagate   | ST3750641NS        | 752 GB | 1       | 2169  | 0     | 5.94   |
| Fujitsu   | MHZ2080BK G2       | 80 GB  | 1       | 2160  | 0     | 5.92   |
| WDC       | WD5000AAKS-65TMA0  | 500 GB | 1       | 2137  | 0     | 5.86   |
| WDC       | WD600BB-00DKA0     | 64 GB  | 1       | 4248  | 1     | 5.82   |
| Hitachi   | HUA722020ALA330    | 2 TB   | 24      | 2617  | 9     | 5.81   |
| WDC       | WD5000ABYS-01TNA0  | 500 GB | 2       | 2117  | 0     | 5.80   |
| Samsung   | HE103UJ            | 1 TB   | 3       | 2992  | 1     | 5.79   |
| WDC       | WD3200AVJB-63J5A0  | 320 GB | 2       | 2113  | 0     | 5.79   |
| WDC       | WD5000AADS-57S9B1  | 500 GB | 1       | 2086  | 0     | 5.72   |
| Hitachi   | HDS721025CLA682    | 250 GB | 3       | 2082  | 0     | 5.71   |
| WDC       | WD10EACS-00C7B0    | 1 TB   | 5       | 2079  | 0     | 5.70   |
| WDC       | WD3000HLFS-01G6U1  | 304 GB | 2       | 2066  | 0     | 5.66   |
| HP        | MB2000EAZNL        | 2 TB   | 1       | 2065  | 0     | 5.66   |
| Hitachi   | HUA723030ALA640... | 3 TB   | 2       | 2062  | 0     | 5.65   |
| WDC       | WD800JD-75MSA1     | 80 GB  | 2       | 2057  | 0     | 5.64   |
| WDC       | WD10EAVS-32D7B1    | 1 TB   | 4       | 2050  | 0     | 5.62   |
| Seagate   | ST6000VN0021-1Z... | 6 TB   | 1       | 2047  | 0     | 5.61   |
| WDC       | WD6001FFWX-68Z39N0 | 6 TB   | 1       | 2045  | 0     | 5.60   |
| Seagate   | ST4000DX000-1CL160 | 4 TB   | 1       | 2041  | 0     | 5.59   |
| IBM/Hi... | IC35L120AVV207-0   | 128 GB | 2       | 2350  | 1     | 5.59   |
| WDC       | WD20EARS-00S0XB0   | 2 TB   | 1       | 2031  | 0     | 5.57   |
| WDC       | WD3000BLFS-01YBU0  | 304 GB | 6       | 2016  | 0     | 5.52   |
| WDC       | WD5000AAKS-60A7B2  | 500 GB | 1       | 2011  | 0     | 5.51   |
| WDC       | WD10EACS-32ZJB0    | 1 TB   | 4       | 2011  | 0     | 5.51   |
| HP        | GB0500C4413        | 500 GB | 2       | 2009  | 0     | 5.51   |
| WDC       | WD1002FBYS-18W8B1  | 1 TB   | 1       | 1999  | 0     | 5.48   |
| WDC       | WD1600ADFS-75SLR2  | 160 GB | 1       | 1997  | 0     | 5.47   |
| Seagate   | ST5000NM0084-1H... | 5 TB   | 2       | 1991  | 0     | 5.46   |
| WDC       | WD20EADS-32S2B0    | 2 TB   | 3       | 2352  | 4     | 5.45   |
| Seagate   | ST31000340NS EIT   | 1 TB   | 2       | 1989  | 0     | 5.45   |
| WDC       | WD1601ABYS-01C0A0  | 164 GB | 1       | 1982  | 0     | 5.43   |
| WDC       | WD7500KMVV-11A27S0 | 752 GB | 1       | 1976  | 0     | 5.42   |
| WDC       | WD6401AALS-00E8B0  | 640 GB | 7       | 1975  | 0     | 5.41   |
| WDC       | WD1002FBYS-05A6B0  | 1 TB   | 5       | 2597  | 1     | 5.41   |
| Hitachi   | HUA721050KLA330    | 500 GB | 6       | 1973  | 0     | 5.41   |
| WDC       | WD1600AAJS-00RYA0  | 160 GB | 1       | 1970  | 0     | 5.40   |
| WDC       | WD2500KS-22MJB0    | 250 GB | 2       | 1943  | 0     | 5.32   |
| WDC       | WD400BD-55MTA1     | 40 GB  | 2       | 1922  | 0     | 5.27   |
| Toshiba   | Freecom            | 5 TB   | 1       | 1916  | 0     | 5.25   |
| WDC       | WD5000AAKX-753CA0  | 500 GB | 4       | 1912  | 0     | 5.24   |
| WDC       | WD5000AUDX-61WNHY0 | 500 GB | 1       | 1901  | 0     | 5.21   |
| WDC       | WD10EURS-730AB1    | 1 TB   | 1       | 1894  | 0     | 5.19   |
| WDC       | WD3200JS-55PDB0    | 320 GB | 1       | 1881  | 0     | 5.15   |
| Seagate   | ST3160828AS        | 160 GB | 2       | 1874  | 0     | 5.14   |
| Toshiba   | MD04ACA50D         | 5 TB   | 1       | 1874  | 0     | 5.13   |
| WDC       | WD7500AAKS-22RBA0  | 752 GB | 1       | 1816  | 0     | 4.98   |
| WDC       | WD20NPVX-00EA4T0   | 2 TB   | 30      | 2001  | 2     | 4.97   |
| Hitachi   | HDS723030ALA640    | 3 TB   | 32      | 2117  | 51    | 4.92   |
| Hitachi   | HCS5C3020BLE630    | 2 TB   | 1       | 1789  | 0     | 4.90   |
| WDC       | WD2500YS-70SHB1    | 250 GB | 1       | 1789  | 0     | 4.90   |
| WDC       | WD80PUZX-64NEAY0   | 8 TB   | 4       | 1788  | 0     | 4.90   |
| Seagate   | ST6000DM001-1XY17Z | 6 TB   | 3       | 1778  | 0     | 4.87   |
| WDC       | WD1500HLFS-01G6U0  | 150 GB | 4       | 1805  | 1     | 4.87   |
| HP        | GB0250EAFYK        | 250 GB | 3       | 2106  | 45    | 4.85   |
| WDC       | WD1003FBYX-12      | 1 TB   | 2       | 1766  | 0     | 4.84   |
| WDC       | WD400BD-60LTA0     | 40 GB  | 1       | 1764  | 0     | 4.83   |
| WDC       | WD400JD-19JNA0     | 40 GB  | 1       | 1756  | 0     | 4.81   |
| WDC       | WD2500SB-01KBC0    | 250 GB | 1       | 1755  | 0     | 4.81   |
| Hitachi   | HDS7225SBSUN250G   | 250 GB | 1       | 5248  | 2     | 4.79   |
| WDC       | WD30EURX-63T0FY0   | 3 TB   | 4       | 1953  | 3     | 4.77   |
| Seagate   | ST32000646NS       | 2 TB   | 2       | 1727  | 0     | 4.73   |
| WDC       | WD4000AAJS-22YFA0  | 400 GB | 1       | 1725  | 0     | 4.73   |
| WDC       | WD2502ABYS-01B7A0  | 256 GB | 6       | 2126  | 1     | 4.71   |
| WDC       | WD1001FALS-41K1B0  | 1 TB   | 3       | 1715  | 0     | 4.70   |
| WDC       | WD5001AALS-00F41A0 | 500 GB | 1       | 1714  | 0     | 4.70   |
| WDC       | WD400JB-00ENA0     | 40 GB  | 3       | 2383  | 6     | 4.69   |
| Hitachi   | HUA722010ALA330    | 1 TB   | 6       | 1982  | 1     | 4.68   |
| HGST      | HTE541515A9E630    | 1.5 TB | 1       | 1702  | 0     | 4.66   |
| WDC       | WD3200AAJS-22RYA0  | 320 GB | 5       | 1701  | 0     | 4.66   |
| Seagate   | ST3300822AS        | 304 GB | 2       | 1700  | 0     | 4.66   |
| WDC       | WD2500AAKS-402AA0  | 250 GB | 1       | 1700  | 0     | 4.66   |
| WDC       | WD7502ABYS-02A6B0  | 752 GB | 1       | 1700  | 0     | 4.66   |
| WDC       | WD3200KS-00PFB0    | 320 GB | 6       | 1917  | 16    | 4.64   |
| WDC       | WD5000LPCX-16VHAT0 | 500 GB | 1       | 1686  | 0     | 4.62   |
| Samsung   | SP0411N            | 40 GB  | 2       | 3755  | 9     | 4.62   |
| Seagate   | ST9500320AS        | 500 GB | 2       | 1684  | 0     | 4.62   |
| WDC       | WD30EURS-63SPKY0   | 3 TB   | 5       | 1681  | 0     | 4.61   |
| WDC       | WD1601ABYS-18C0A0  | 160 GB | 3       | 2303  | 4     | 4.60   |
| HGST      | HUS724020ALE640    | 2 TB   | 12      | 1668  | 0     | 4.57   |
| WDC       | WD1600JS-88MHB0    | 160 GB | 1       | 1667  | 0     | 4.57   |
| Seagate   | ST2000NX0253       | 2 TB   | 16      | 1662  | 0     | 4.55   |
| WDC       | WD6400AAKS-00H2B1  | 640 GB | 1       | 1653  | 0     | 4.53   |
| WDC       | WD3200LPVX-16V0TT3 | 320 GB | 1       | 1644  | 0     | 4.50   |
| HP        | MB2000EBUCF        | 2 TB   | 2       | 2923  | 6     | 4.48   |
| Seagate   | ST3200021A         | 200 GB | 1       | 1632  | 0     | 4.47   |
| Seagate   | ST4000NM0024-1H... | 4 TB   | 7       | 1632  | 0     | 4.47   |
| WDC       | WD3000GLFS-01F8U0  | 304 GB | 7       | 2232  | 165   | 4.47   |
| WDC       | WD2500AAKS-22VSA0  | 250 GB | 1       | 1628  | 0     | 4.46   |
| WDC       | WD5000AAKS-07A7B2  | 500 GB | 3       | 2164  | 7     | 4.45   |
| Seagate   | ST91000640NS       | 1 TB   | 22      | 1778  | 2     | 4.45   |
| Hitachi   | HUA721010KLA330... | 1 TB   | 2       | 1886  | 3     | 4.43   |
| WDC       | WD3200YS-01PGB0    | 320 GB | 3       | 1617  | 0     | 4.43   |
| WDC       | WD360GD-00FNA0     | 37 GB  | 3       | 2943  | 2     | 4.41   |
| WDC       | WD10EURX-61C57Y0   | 1 TB   | 1       | 1606  | 0     | 4.40   |
| WDC       | WD7500AYYS-01RCA0  | 752 GB | 5       | 1678  | 1     | 4.39   |
| WDC       | WD1600JB-22GVA0    | 160 GB | 1       | 1600  | 0     | 4.39   |
| WDC       | WD5000AUDX-57WNHY0 | 500 GB | 2       | 1594  | 0     | 4.37   |
| WDC       | WD2000JB-16FUA0    | 200 GB | 1       | 1584  | 0     | 4.34   |
| Seagate   | ST4000VN000-1H4168 | 4 TB   | 33      | 1618  | 62    | 4.32   |
| WDC       | WD3000HLFS-01G6U4  | 304 GB | 5       | 1570  | 0     | 4.30   |
| WDC       | WD2500YS-18SHB2    | 250 GB | 1       | 1566  | 0     | 4.29   |
| WDC       | WD2003FYPS-27Y2B0  | 2 TB   | 8       | 1874  | 14    | 4.29   |
| WDC       | WD2502ABYS-23B7... | 250 GB | 7       | 1984  | 2     | 4.28   |
| WDC       | WD1003FBYX-88 LEN  | 1 TB   | 4       | 1743  | 1     | 4.27   |
| Toshiba   | MC04ACA200E        | 2 TB   | 2       | 1548  | 0     | 4.24   |
| WDC       | WD5000LUCT-63Y8HY0 | 500 GB | 3       | 1547  | 0     | 4.24   |
| WDC       | WD40EZRX-75SPEB0   | 4 TB   | 1       | 1542  | 0     | 4.23   |
| WDC       | WD1001FALS-00Y6A0  | 1 TB   | 13      | 1619  | 37    | 4.23   |
| Hitachi   | HDT721075SLA360    | 752 GB | 3       | 1538  | 0     | 4.22   |
| WDC       | WD4000AAJS-65TKA0  | 400 GB | 1       | 1532  | 0     | 4.20   |
| Seagate   | ST31000424CS       | 1 TB   | 1       | 1527  | 0     | 4.19   |
| Seagate   | ST1000NC000-1CX162 | 1 TB   | 4       | 2282  | 223   | 4.18   |
| HPE       | MB0500EBNCR        | 500 GB | 1       | 1526  | 0     | 4.18   |
| WDC       | WD2500YS-01SHB0    | 256 GB | 4       | 1588  | 7     | 4.18   |
| Seagate   | ST2000DL004 HD2... | 2 TB   | 7       | 1523  | 0     | 4.17   |
| WDC       | WD7500BMVW-11AJGS2 | 752 GB | 1       | 1523  | 0     | 4.17   |
| WDC       | WD2502ABYS-23B7... | 250 GB | 2       | 1522  | 0     | 4.17   |
| HGST      | HDN724030ALE640    | 3 TB   | 22      | 1518  | 0     | 4.16   |
| Hitachi   | HUA721010KLA330    | 1 TB   | 18      | 2162  | 111   | 4.12   |
| Seagate   | ST980412ASG        | 80 GB  | 1       | 1501  | 0     | 4.11   |
| WDC       | WD10EACS-00D6B1    | 1 TB   | 9       | 2669  | 219   | 4.11   |
| HGST      | HUS724020ALA640    | 2 TB   | 55      | 1497  | 0     | 4.10   |
| WDC       | WD2500AAJS-22VWA0  | 250 GB | 3       | 1496  | 0     | 4.10   |
| WDC       | WD2003FYYS-02W0B0  | 2 TB   | 15      | 1926  | 1     | 4.09   |
| Quantum   | FIREBALLlct10 05   | 5 GB   | 1       | 1486  | 0     | 4.07   |
| Seagate   | ST3000NM0053       | 3 TB   | 1       | 1484  | 0     | 4.07   |
| MaxDig... | MD4000GBDS         | 4 TB   | 2       | 1483  | 0     | 4.07   |
| WDC       | WD15NPVT-00Z2TT0   | 1.5 TB | 4       | 2133  | 19    | 4.06   |
| WDC       | WD2000JD-00GBB0    | 200 GB | 1       | 1482  | 0     | 4.06   |
| WDC       | WD30EFRX-68AX9N0   | 3 TB   | 60      | 1774  | 2     | 4.04   |
| HP        | FB080C4080         | 80 GB  | 2       | 1472  | 0     | 4.04   |
| WDC       | WD1200JB-00REA0    | 120 GB | 2       | 1515  | 1     | 4.03   |
| WDC       | WD3200AAKX-753CA0  | 320 GB | 1       | 1471  | 0     | 4.03   |
| Seagate   | ST4000NM0085-1Y... | 4 TB   | 2       | 1468  | 0     | 4.02   |
| HGST      | HUS724030ALE640    | 3 TB   | 1       | 1465  | 0     | 4.01   |
| WDC       | WD3200BUDT-73DPZY0 | 320 GB | 1       | 1463  | 0     | 4.01   |
| WDC       | WD8002FRYZ-01FF2B0 | 8 TB   | 2       | 1452  | 0     | 3.98   |
| Seagate   | ST32000644NS 59... | 2 TB   | 1       | 2894  | 1     | 3.96   |
| WDC       | WD1002FBYS-02A6B0  | 1 TB   | 21      | 1820  | 28    | 3.95   |
| WDC       | WD2500AAKS-61L9A0  | 250 GB | 4       | 1439  | 0     | 3.94   |
| Seagate   | ST6000NM0024       | 6 TB   | 5       | 1433  | 0     | 3.93   |
| Seagate   | ST340212AS         | 40 GB  | 6       | 1654  | 35    | 3.92   |
| Hitachi   | HUA723020ALA640    | 2 TB   | 31      | 1470  | 1     | 3.90   |
| WDC       | WD40EZRX-22SPEB0   | 4 TB   | 4       | 1967  | 2     | 3.90   |
| WDC       | WD20EADS-55R6B0    | 2 TB   | 1       | 1422  | 0     | 3.90   |
| WDC       | WD15EARS-32MVWB0   | 1.5 TB | 3       | 1419  | 0     | 3.89   |
| WDC       | WD2002FYPS-01U1B1  | 2 TB   | 1       | 4245  | 2     | 3.88   |
| Seagate   | ST3320820AS_P      | 320 GB | 2       | 1408  | 0     | 3.86   |
| WDC       | WD1500HLFS-01G6U3  | 150 GB | 2       | 1407  | 0     | 3.86   |
| Samsung   | SP1624N            | 160 GB | 3       | 1402  | 0     | 3.84   |
| WDC       | WD3200AAKS-75SBA0  | 320 GB | 4       | 1401  | 0     | 3.84   |
| Toshiba   | MG04ACA600EY       | 6 TB   | 2       | 1401  | 0     | 3.84   |
| WDC       | WD2500JB-22REA0    | 250 GB | 1       | 1398  | 0     | 3.83   |
| WDC       | WD2502ABYS-18B7A0  | 250 GB | 6       | 1674  | 2     | 3.83   |
| Seagate   | ST2000VM002-9UY166 | 2 TB   | 2       | 2460  | 186   | 3.83   |
| WDC       | WD2003FYYS-18W0B0  | 2 TB   | 11      | 2206  | 155   | 3.82   |
| WDC       | WD1001FALS-00J7B0  | 1 TB   | 41      | 1978  | 3     | 3.82   |
| WDC       | WD3200JS-57PDB0    | 320 GB | 1       | 1391  | 0     | 3.81   |
| WDC       | WD3200AAJB-00WGA0  | 320 GB | 4       | 1389  | 0     | 3.81   |
| WDC       | WD10EVDS-63U8B1    | 1 TB   | 3       | 1386  | 0     | 3.80   |
| WDC       | WD740ADFD-00NLR1   | 74 GB  | 2       | 1386  | 0     | 3.80   |
| WDC       | WD20EARS-07MVWB0   | 2 TB   | 4       | 1896  | 1     | 3.79   |
| WDC       | WD2500AAJS-00VWA0  | 250 GB | 2       | 1384  | 0     | 3.79   |
| WDC       | WD40EURX-64WRWY0   | 4 TB   | 3       | 1382  | 0     | 3.79   |
| Seagate   | MB3000EBKAB        | 3 TB   | 3       | 1366  | 0     | 3.74   |
| WDC       | WD1500HLFS-50G6U1  | 150 GB | 2       | 1364  | 0     | 3.74   |
| WDC       | WD800HLFS-75G6U1   | 80 GB  | 2       | 1360  | 0     | 3.73   |
| Hitachi   | HCC545025B9A300    | 250 GB | 3       | 1359  | 0     | 3.72   |
| WDC       | WD1600JS-98MHB0    | 160 GB | 2       | 1358  | 0     | 3.72   |
| WDC       | WD1600AAJS-61WAA0  | 160 GB | 4       | 1357  | 0     | 3.72   |
| Hitachi   | HCC545050B9A300    | 500 GB | 1       | 1349  | 0     | 3.70   |
| WDC       | WD6401AALS-00J7B0  | 640 GB | 4       | 1845  | 157   | 3.69   |
| WDC       | WD10EACS-00D6B0    | 1 TB   | 21      | 1879  | 104   | 3.67   |
| Hitachi   | HUA723020ALA640... | 2 TB   | 1       | 1337  | 0     | 3.66   |
| WDC       | WD2500AAKX-19U6AA0 | 250 GB | 1       | 1334  | 0     | 3.66   |
| WDC       | WD5001ABYS-01YNA0  | 500 GB | 4       | 1332  | 0     | 3.65   |
| Seagate   | ST8000VN0002-1Z... | 8 TB   | 5       | 1736  | 21    | 3.65   |
| WDC       | WD20EARS-42S0XB0   | 2 TB   | 3       | 1330  | 0     | 3.64   |
| Seagate   | ST2000NM0033       | 2 TB   | 1       | 1328  | 0     | 3.64   |
| WDC       | WD5000BTKT-40MD3T0 | 500 GB | 2       | 1326  | 0     | 3.63   |
| WDC       | WD7501AALS-00E8B0  | 752 GB | 5       | 1832  | 4     | 3.63   |
| WDC       | WD5000BPKT-08PK4T0 | 500 GB | 2       | 1320  | 0     | 3.62   |
| WDC       | WD2001FASS-00W2B0  | 2 TB   | 6       | 1930  | 2     | 3.61   |
| WDC       | WD10EADS-67M2B0    | 1 TB   | 3       | 1726  | 9     | 3.61   |
| Fujitsu   | MPE3064AT          | 6 GB   | 2       | 1315  | 0     | 3.60   |
| WDC       | WD1600JD-00HBC0    | 160 GB | 3       | 1534  | 2     | 3.60   |
| Hitachi   | HDS722516VLSA80    | 164 GB | 4       | 1529  | 2     | 3.60   |
| WDC       | WD2500AAKX-08ERMA0 | 250 GB | 2       | 1311  | 0     | 3.59   |
| WDC       | WD5000AAKS-60YGA1  | 500 GB | 1       | 1311  | 0     | 3.59   |
| WDC       | WD400BD-22JMC0     | 40 GB  | 1       | 1310  | 0     | 3.59   |
| WDC       | WD1600JS-00MHB5    | 160 GB | 1       | 1303  | 0     | 3.57   |
| Hitachi   | HDS725050KLAT80    | 500 GB | 1       | 1303  | 0     | 3.57   |
| Maxtor    | 6H500F0            | 500 GB | 1       | 1294  | 0     | 3.55   |
| WDC       | WD2500LPLX-75ZNTT0 | 250 GB | 1       | 1292  | 0     | 3.54   |
| WDC       | WD5002ABYS-02B1B0  | 500 GB | 15      | 1535  | 2     | 3.53   |
| HGST      | HUS724030ALA640    | 3 TB   | 25      | 1390  | 3     | 3.53   |
| Toshiba   | MQ01UBD075         | 752 GB | 1       | 1287  | 0     | 3.53   |
| WDC       | WD740GD-00FLA1     | 74 GB  | 2       | 2935  | 20    | 3.52   |
| WDC       | WD1200BB-00GUA0    | 120 GB | 1       | 1284  | 0     | 3.52   |
| WDC       | WD20EACS-11BHUB0   | 2 TB   | 3       | 1344  | 533   | 3.52   |
| WDC       | WD2000BB-22GUC0    | 200 GB | 1       | 1282  | 0     | 3.51   |
| Seagate   | ST320LT014-9YK142  | 320 GB | 2       | 1282  | 0     | 3.51   |
| WDC       | WD4000AAKS-00A7B0  | 400 GB | 1       | 1280  | 0     | 3.51   |
| WDC       | WD20EARX-008FB0    | 2 TB   | 24      | 1533  | 6     | 3.51   |
| WDC       | WD5000AAKS-00TMA0  | 500 GB | 16      | 1350  | 3     | 3.50   |
| WDC       | WD3000FYYZ-50UL1B0 | 3 TB   | 1       | 1278  | 0     | 3.50   |
| WDC       | WD6400AAKS-41H2B0  | 640 GB | 3       | 1277  | 0     | 3.50   |
| WDC       | WD1001FALS-00U9B0  | 1 TB   | 4       | 2201  | 124   | 3.50   |
| WDC       | WD15EVDS-68V9B0    | 1.5 TB | 1       | 1276  | 0     | 3.50   |
| HP        | J7989G             | 80 GB  | 1       | 1274  | 0     | 3.49   |
| HP        | MB1000GCEEK        | 1 TB   | 1       | 1272  | 0     | 3.49   |
| WDC       | WD1000DHTZ-04N21V1 | 1 TB   | 2       | 1270  | 0     | 3.48   |
| Seagate   | ST3000DM001-1E6166 | 3 TB   | 8       | 1457  | 500   | 3.48   |
| WDC       | WD15EVDS-73V9B0    | 1.5 TB | 1       | 3810  | 2     | 3.48   |
| Seagate   | ST4000NM0033       | 4 TB   | 1       | 1267  | 0     | 3.47   |
| WDC       | WD81PURZ-85LWMY0   | 8 TB   | 1       | 1265  | 0     | 3.47   |
| WDC       | WD1200JS-00SGB0    | 120 GB | 3       | 1264  | 0     | 3.46   |
| Seagate   | ST3160022ACE       | 160 GB | 1       | 1263  | 0     | 3.46   |
| HGST      | HUS726060ALE610    | 6 TB   | 11      | 1260  | 0     | 3.45   |
| WDC       | WD800BD-00JMA0     | 80 GB  | 1       | 1260  | 0     | 3.45   |
| HGST      | HUP723020APA640    | 2 TB   | 1       | 1257  | 0     | 3.45   |
| WDC       | WD30EZRX-00AZ6B0   | 3 TB   | 7       | 1608  | 40    | 3.44   |
| HP        | MB2000GCWDA        | 2 TB   | 5       | 1687  | 2     | 3.44   |
| Toshiba   | MG03ACA200         | 2 TB   | 9       | 1540  | 48    | 3.44   |
| Hitachi   | HDT725040VLA360    | 400 GB | 5       | 1539  | 5     | 3.43   |
| Hitachi   | HTS421212H9AT00    | 120 GB | 2       | 2184  | 120   | 3.43   |
| Hitachi   | HDS723020BLA642    | 2 TB   | 74      | 1467  | 83    | 3.42   |
| Hitachi   | HDS5C3015ALA632    | 1.5 TB | 4       | 1382  | 80    | 3.42   |
| WDC       | WD5003ABYX-18WERA0 | 500 GB | 17      | 1700  | 64    | 3.40   |
| Hitachi   | HDT722520DLAT80    | 200 GB | 3       | 1238  | 0     | 3.39   |
| Samsung   | SP0451N            | 40 GB  | 1       | 1237  | 0     | 3.39   |
| WDC       | WD1003FBYX-18Y7B0  | 1 TB   | 5       | 1803  | 5     | 3.37   |
| WDC       | WD2500HHTZ-04N21V1 | 250 GB | 2       | 1226  | 0     | 3.36   |
| WDC       | WD800JD-55MSA1     | 80 GB  | 4       | 1226  | 0     | 3.36   |
| WDC       | WD4000AAJS-32TKA0  | 400 GB | 1       | 1226  | 0     | 3.36   |
| WDC       | WD10EAVS-00D7B0    | 1 TB   | 18      | 1691  | 7     | 3.36   |
| WDC       | WD2000FYYZ-01UL1B2 | 2 TB   | 6       | 1328  | 1     | 3.35   |
| WDC       | WD5000AAVS-00G9B0  | 500 GB | 7       | 1406  | 2     | 3.34   |
| HGST      | HUH728080ALN600    | 8 TB   | 7       | 1218  | 0     | 3.34   |
| Seagate   | ST3808110AS 41N... | 80 GB  | 2       | 1356  | 1     | 3.34   |
| Toshiba   | HDWU110            | 1 TB   | 1       | 1217  | 0     | 3.34   |
| Seagate   | ST8000AS0002-1N... | 8 TB   | 114     | 1377  | 57    | 3.33   |
| Seagate   | ST310211A          | 10 GB  | 2       | 1214  | 0     | 3.33   |
| WDC       | WD2002FAEX-007BA0  | 2 TB   | 64      | 1521  | 11    | 3.32   |
| WDC       | WD7501AALS-00J7B1  | 752 GB | 12      | 1353  | 1     | 3.31   |
| WDC       | WD10EACS-00ZJB0    | 1 TB   | 12      | 1585  | 57    | 3.31   |
| WDC       | WD10JPVT-16A1YT0   | 1 TB   | 4       | 1206  | 0     | 3.31   |
| WDC       | WD10EARS-67Y5B1    | 1 TB   | 1       | 1206  | 0     | 3.30   |
| Hitachi   | HDT721075SLA380    | 752 GB | 1       | 1205  | 0     | 3.30   |
| Fujitsu   | MHV2160BT PL       | 160 GB | 1       | 1202  | 0     | 3.30   |
| WDC       | WD1500HLFS-01G6U1  | 150 GB | 6       | 1200  | 0     | 3.29   |
| Apple     | HDD ST2000LM003    | 2 TB   | 1       | 1200  | 0     | 3.29   |
| WDC       | WD10EALX-759BA0    | 1 TB   | 4       | 1628  | 3     | 3.29   |
| Hitachi   | HDS723020BLE640    | 2 TB   | 12      | 1196  | 0     | 3.28   |
| Hitachi   | HCS5C1010CLA382    | 1 TB   | 6       | 1195  | 0     | 3.28   |
| HGST      | HDS724040ALE640    | 4 TB   | 15      | 1470  | 139   | 3.27   |
| Hitachi   | HDS722020ALA330    | 2 TB   | 56      | 1901  | 109   | 3.27   |
| WDC       | WD2500AAJS-61B4A0  | 250 GB | 2       | 1191  | 0     | 3.27   |
| Samsung   | HD502HM            | 500 GB | 2       | 1993  | 1     | 3.26   |
| WDC       | WD5000AAJS-32YFA0  | 500 GB | 1       | 1187  | 0     | 3.25   |
| Seagate   | ST3300631A         | 304 GB | 1       | 1185  | 0     | 3.25   |
| Seagate   | ST9808211A         | 80 GB  | 1       | 1185  | 0     | 3.25   |
| HGST      | HUS724040ALA640    | 4 TB   | 32      | 1295  | 65    | 3.24   |
| Hitachi   | HDS721075KLA330    | 752 GB | 10      | 1380  | 10    | 3.24   |
| WDC       | WD1600AABS-56PRA0  | 160 GB | 3       | 1178  | 0     | 3.23   |
| WDC       | WD10EZEX-75ZF5A0   | 1 TB   | 21      | 1225  | 97    | 3.23   |
| HGST      | HDN728080ALE604    | 8 TB   | 5       | 1176  | 0     | 3.22   |
| Hitachi   | HDS728040PLA320    | 40 GB  | 4       | 1548  | 4     | 3.22   |
| Hitachi   | HCS5C2020ALA632    | 2 TB   | 3       | 1986  | 4     | 3.22   |
| WDC       | WD3200AAJB-56WGA0  | 320 GB | 3       | 1172  | 0     | 3.21   |
| WDC       | WD800BB-60JKC0     | 80 GB  | 2       | 1292  | 2     | 3.21   |
| Maxtor    | 6N040T0            | 40 GB  | 2       | 1842  | 1     | 3.21   |
| WDC       | WD1600AAJS-60WAA0  | 160 GB | 9       | 1200  | 113   | 3.20   |
| WDC       | WD3200AAJS-07RYA0  | 320 GB | 1       | 1168  | 0     | 3.20   |
| WDC       | WD15EARS-22Z5B1    | 1.5 TB | 4       | 1168  | 0     | 3.20   |
| WDC       | WD1600JS-75NCB2    | 160 GB | 1       | 1168  | 0     | 3.20   |
| WDC       | WD1500AHFD-00RAR5  | 150 GB | 1       | 1164  | 0     | 3.19   |
| WDC       | WD7500BPVX-55JC3T3 | 752 GB | 1       | 1163  | 0     | 3.19   |
| WDC       | WD5000AVJB-63YUA0  | 500 GB | 1       | 1163  | 0     | 3.19   |
| HGST      | HDN724040ALE640    | 4 TB   | 35      | 1229  | 58    | 3.19   |
| Toshiba   | MK8017GSG          | 80 GB  | 1       | 1162  | 0     | 3.18   |
| Seagate   | ST9250610NS        | 250 GB | 7       | 1159  | 0     | 3.18   |
| WDC       | WD6000HLHX-75JJPV0 | 600 GB | 4       | 1936  | 3     | 3.18   |
| WDC       | WD20EARX-32PASB0   | 2 TB   | 10      | 1173  | 1     | 3.17   |
| Hitachi   | HDS722525VLSA80    | 250 GB | 6       | 1232  | 6     | 3.17   |
| WDC       | WD2500JB-00GVA0    | 250 GB | 1       | 1155  | 0     | 3.16   |
| WDC       | WD2503ABYX-01WERA0 | 256 GB | 1       | 1155  | 0     | 3.16   |
| Toshiba   | MG04ACA100N        | 1 TB   | 4       | 1154  | 0     | 3.16   |
| WDC       | WD10EADS-00L5B1    | 1 TB   | 107     | 1640  | 9     | 3.16   |
| Seagate   | ST32000645NS       | 2 TB   | 10      | 1521  | 9     | 3.14   |
| WDC       | WD3200LPLX-60ZNTT1 | 320 GB | 1       | 1145  | 0     | 3.14   |
| WDC       | WD80PURZ-85YNPY0   | 8 TB   | 2       | 1145  | 0     | 3.14   |
| WDC       | WD3200AAKS-22SBA0  | 320 GB | 3       | 1144  | 0     | 3.14   |
| WDC       | WD10EAVS-22D7B0    | 1 TB   | 4       | 1775  | 4     | 3.13   |
| HGST      | HDN726060ALE610    | 6 TB   | 18      | 1193  | 38    | 3.12   |
| WDC       | WD7500AACS-00D6B0  | 752 GB | 3       | 1244  | 3     | 3.12   |
| WDC       | WD5003AZEX-00RKKA0 | 500 GB | 2       | 1135  | 0     | 3.11   |
| WDC       | MB0500EBNCR        | 500 GB | 1       | 1134  | 0     | 3.11   |
| WDC       | WD2500JS-41SGB0    | 250 GB | 2       | 1132  | 0     | 3.10   |
| Hitachi   | HUA722020ALA330... | 2 TB   | 1       | 1132  | 0     | 3.10   |
| WDC       | WD10EZEX-07ZF5A0   | 1 TB   | 5       | 1371  | 3     | 3.09   |
| Seagate   | ST4000VN0001-1S... | 4 TB   | 3       | 1128  | 0     | 3.09   |
| Seagate   | ST250DM001 HD256GJ | 250 GB | 1       | 1123  | 0     | 3.08   |
| WDC       | WD4000F9YZ-09N20L1 | 4 TB   | 3       | 1122  | 0     | 3.08   |
| WDC       | WD3200AAKS-00G3A0  | 320 GB | 7       | 1120  | 0     | 3.07   |
| WDC       | WD3200AAJS-40VWA0  | 320 GB | 1       | 1118  | 0     | 3.06   |
| WDC       | WD2000F9YZ-09N20L0 | 2 TB   | 9       | 1221  | 12    | 3.06   |
| WDC       | WD2500JS-40MVB1    | 250 GB | 2       | 1115  | 0     | 3.06   |
| Seagate   | ST4000DM006-2G5107 | 4 TB   | 4       | 1115  | 0     | 3.05   |
| WDC       | WD3000HLFS-01G6U3  | 304 GB | 2       | 1113  | 0     | 3.05   |
| WDC       | WD1001FALS-00J7B1  | 1 TB   | 37      | 1581  | 3     | 3.04   |
| Hitachi   | HCP725025GLA380    | 250 GB | 1       | 1111  | 0     | 3.04   |
| Toshiba   | MG03ACA300         | 3 TB   | 9       | 1429  | 6     | 3.04   |
| WDC       | WD5001FZWX-00ZHUA0 | 5 TB   | 7       | 1587  | 18    | 3.04   |
| WDC       | WD1002FAEX-00Y9A0  | 1 TB   | 83      | 1303  | 11    | 3.04   |
| WDC       | WD2500AACS-00M6B0  | 250 GB | 1       | 1107  | 0     | 3.03   |
| WDC       | WD1200BEVE-00WZT0  | 120 GB | 1       | 1103  | 0     | 3.02   |
| Hitachi   | HDS7250SASUN500... | 500 GB | 1       | 1103  | 0     | 3.02   |
| WDC       | WD1600AAJS-08WAA0  | 160 GB | 3       | 1291  | 1     | 3.02   |
| MARSHAL   | MAL2120SA-T54      | 120 GB | 1       | 1099  | 0     | 3.01   |
| Hitachi   | HUA721075KLA330... | 752 GB | 1       | 1098  | 0     | 3.01   |
| WDC       | WD20EURX-64HYZY0   | 2 TB   | 1       | 1098  | 0     | 3.01   |
| Seagate   | ST6000AS0002-1N... | 6 TB   | 11      | 1573  | 73    | 3.00   |
| Hitachi   | HDS721010CLA630    | 1 TB   | 20      | 1268  | 53    | 3.00   |
| Hitachi   | HUA723030ALA640    | 3 TB   | 41      | 1394  | 56    | 3.00   |
| WDC       | WD3200KS-75PFB0    | 320 GB | 2       | 1365  | 39    | 3.00   |
| WDC       | WD30EZRX-22D8PB0   | 3 TB   | 8       | 1183  | 1     | 3.00   |
| Hitachi   | HDS5C3030ALA630    | 3 TB   | 11      | 1518  | 3     | 3.00   |
| WDC       | WD80EFAX-68LHPN0   | 8 TB   | 27      | 1092  | 0     | 2.99   |
| WDC       | WD2500JS-00MHB0    | 250 GB | 5       | 1155  | 1     | 2.99   |
| Samsung   | HE253GJ            | 250 GB | 2       | 2131  | 1     | 2.99   |
| Hitachi   | HDT725032VLA380    | 320 GB | 17      | 1539  | 80    | 2.99   |
| WDC       | WD1001FALS-41Y6A0  | 1 TB   | 5       | 1202  | 1     | 2.99   |
| WDC       | WD10SPCX-00KHST0   | 1 TB   | 2       | 1089  | 0     | 2.99   |
| WDC       | WD1600YS-01SHB1    | 164 GB | 7       | 1088  | 0     | 2.98   |
| WDC       | WD1200JD-00HBB0    | 120 GB | 11      | 1699  | 122   | 2.97   |
| Seagate   | ST32000641AS       | 2 TB   | 29      | 1581  | 156   | 2.97   |
| WDC       | WD1001FALS-40U9B0  | 1 TB   | 5       | 1220  | 1     | 2.97   |
| Seagate   | ST3300620A         | 304 GB | 1       | 1083  | 0     | 2.97   |
| Seagate   | ST9500620NS 81Y... | 500 GB | 1       | 1083  | 0     | 2.97   |
| Toshiba   | MQ03ABB200         | 2 TB   | 2       | 1079  | 0     | 2.96   |
| WDC       | WD2500JS-60NCB1    | 250 GB | 11      | 1142  | 1     | 2.96   |
| Seagate   | MM0500EBKAE        | 500 GB | 1       | 3231  | 2     | 2.95   |
| WDC       | WD30EURX-64HYZY0   | 3 TB   | 1       | 1077  | 0     | 2.95   |
| Maxtor    | 7V250F0            | 256 GB | 2       | 1075  | 0     | 2.95   |
| WDC       | WD6400BPVT-16HXZT1 | 640 GB | 3       | 1465  | 3     | 2.95   |
| WDC       | WD1004FBYZ-23YC    | 1 TB   | 4       | 1074  | 0     | 2.94   |
| Seagate   | ST1000NX0423 00... | 1 TB   | 5       | 1073  | 0     | 2.94   |
| WDC       | WD360ADFD-00NLR1   | 37 GB  | 2       | 1073  | 0     | 2.94   |
| WDC       | WD3200AZKX-00D6NA0 | 320 GB | 1       | 1073  | 0     | 2.94   |
| WDC       | WD15EVDS-63V9B1    | 1.5 TB | 3       | 1581  | 4     | 2.94   |
| Maxtor    | 6V300F0            | 304 GB | 4       | 1071  | 0     | 2.94   |
| Maxtor    | 6L020J1            | 20 GB  | 3       | 1213  | 2     | 2.93   |
| WDC       | WD3200AAKS-00WWPA0 | 320 GB | 1       | 1069  | 0     | 2.93   |
| Toshiba   | HDWA130            | 3 TB   | 5       | 1069  | 0     | 2.93   |
| HGST      | HTS721050A9E630    | 500 GB | 1       | 1069  | 0     | 2.93   |
| WDC       | WD5000BHTZ-04JCPV0 | 500 GB | 1       | 1069  | 0     | 2.93   |
| Seagate   | ST2000NC001-1DY164 | 2 TB   | 8       | 1068  | 0     | 2.93   |
| Seagate   | ST3300622AS        | 304 GB | 4       | 1477  | 1     | 2.92   |
| WDC       | WD20EURX-57T0FY1   | 2 TB   | 2       | 1064  | 0     | 2.92   |
| HGST      | HUS726020ALA610    | 2 TB   | 10      | 1062  | 0     | 2.91   |
| Hitachi   | HUA722020ALA331    | 2 TB   | 26      | 1747  | 6     | 2.91   |
| Hitachi   | HDS721075CLA332    | 752 GB | 7       | 1275  | 290   | 2.91   |
| WDC       | WD4000AAKS-00YGA0  | 400 GB | 7       | 1233  | 1     | 2.91   |
| Seagate   | ST500DM002-1ER14C  | 500 GB | 4       | 1057  | 0     | 2.90   |
| Fujitsu   | MHV2040BH          | 40 GB  | 3       | 1057  | 0     | 2.90   |
| WDC       | WD2500AAJS-75VWA0  | 250 GB | 3       | 1056  | 0     | 2.89   |
| Maxtor    | STM3320620AS       | 320 GB | 3       | 1055  | 0     | 2.89   |
| Seagate   | ST3000VX000-1ES166 | 3 TB   | 6       | 1055  | 0     | 2.89   |
| WDC       | WD6002FZWX-00GBGB0 | 6 TB   | 2       | 1675  | 2     | 2.88   |
| WDC       | WD2500JS-00MHB1    | 250 GB | 2       | 1052  | 0     | 2.88   |
| WDC       | WD2500YD-01NVB1    | 256 GB | 3       | 1428  | 2     | 2.88   |
| Seagate   | ST3500414CS        | 500 GB | 30      | 1295  | 121   | 2.88   |
| WDC       | WD10EALX-759BA1    | 1 TB   | 14      | 1491  | 178   | 2.88   |
| Hitachi   | HDS725050KLA360    | 500 GB | 16      | 1985  | 29    | 2.88   |
| WDC       | WD5000AAKS-402AA0  | 500 GB | 7       | 1561  | 10    | 2.87   |
| WDC       | WD3000BLFS-08YBU0  | 304 GB | 2       | 1048  | 0     | 2.87   |
| HGST      | MB6000GEBTP        | 6 TB   | 1       | 1046  | 0     | 2.87   |
| WDC       | WD3200BEKT-22F3T0  | 320 GB | 1       | 2090  | 1     | 2.86   |
| WDC       | WD10EAVS-00M4B0    | 1 TB   | 2       | 1038  | 0     | 2.84   |
| WDC       | WD10EADS-00P8B0    | 1 TB   | 11      | 1320  | 28    | 2.84   |
| Apple     | HDD ST3000DM001    | 3 TB   | 2       | 1034  | 0     | 2.84   |
| WDC       | WD800BB-75FRA0     | 80 GB  | 2       | 1034  | 0     | 2.83   |
| Seagate   | ST340823A          | 40 GB  | 1       | 1034  | 0     | 2.83   |
| Seagate   | ST10000VX0004-1... | 10 TB  | 1       | 1033  | 0     | 2.83   |
| Seagate   | ST3500630AS        | 500 GB | 75      | 1523  | 214   | 2.83   |
| WDC       | WD40NMZW-34GX6S1   | 4 TB   | 1       | 1031  | 0     | 2.83   |
| WDC       | WD5000AAKS-40V2B0  | 500 GB | 2       | 1031  | 0     | 2.83   |
| WDC       | WD2502ABYS-02B7A0  | 256 GB | 8       | 1316  | 11    | 2.82   |
| Hitachi   | HDS722580VLAT20    | 82 GB  | 5       | 1261  | 108   | 2.82   |
| WDC       | WD1600AVJS-63WNA0  | 160 GB | 1       | 1027  | 0     | 2.82   |
| WDC       | WD5000AAKS-22YGA0  | 500 GB | 9       | 1192  | 51    | 2.82   |
| Samsung   | HD204UI            | 2 TB   | 84      | 1203  | 61    | 2.81   |
| WDC       | WD2000FYYZ-01UL1B0 | 2 TB   | 5       | 1244  | 1     | 2.81   |
| Hitachi   | HUA722010CLA331    | 1 TB   | 3       | 1365  | 222   | 2.81   |
| HGST      | HUS726020ALE614    | 2 TB   | 5       | 1024  | 0     | 2.81   |
| WDC       | WD4NPURX-64TPFY0   | 4 TB   | 1       | 1023  | 0     | 2.80   |
| WDC       | WD3000F9YZ-09N20L0 | 3 TB   | 6       | 1435  | 1     | 2.80   |
| WDC       | WD2500JB-57REA0    | 250 GB | 1       | 1021  | 0     | 2.80   |
| Seagate   | ST320413A          | 20 GB  | 2       | 1076  | 2     | 2.80   |
| WDC       | WD800JD-60LUA0     | 80 GB  | 3       | 1020  | 0     | 2.80   |
| WDC       | WD800JD-08LSA0     | 80 GB  | 13      | 1129  | 2     | 2.79   |
| WDC       | WD400LB-00DNA0     | 40 GB  | 2       | 1103  | 2     | 2.78   |
| WDC       | WD200BB-00DEA0     | 20 GB  | 1       | 1015  | 0     | 2.78   |
| WDC       | WD1600AAJS-22PSA0  | 160 GB | 19      | 1157  | 26    | 2.78   |
| WDC       | WD5000AACS-61M6B2  | 500 GB | 3       | 2013  | 4     | 2.78   |
| WDC       | WD25EZRX-00MMMB0   | 2.5 TB | 4       | 1720  | 7     | 2.78   |
| Seagate   | ST6000NM0115-1Y... | 6 TB   | 85      | 1013  | 0     | 2.78   |
| WDC       | WD1600JB-00EVA0    | 160 GB | 1       | 1012  | 0     | 2.77   |
| WDC       | WD1002F9YZ-09H1JL1 | 1 TB   | 8       | 1009  | 0     | 2.77   |
| WDC       | WD3200AAKS-75B3A0  | 320 GB | 3       | 1584  | 1     | 2.76   |
| WDC       | WD2002FYPS-01U1B0  | 2 TB   | 5       | 2628  | 105   | 2.75   |
| WDC       | WD1600AABS-61PRA0  | 160 GB | 3       | 1341  | 1     | 2.75   |
| WDC       | WD2500JS-75NCB3    | 250 GB | 9       | 1309  | 15    | 2.75   |
| WDC       | WD20EARX-00ZUDB0   | 2 TB   | 4       | 1492  | 5     | 2.75   |
| WDC       | WD1002FAEX-00Z3A0  | 1 TB   | 153     | 1259  | 58    | 2.75   |
| HGST      | HMS5C4040BLE640    | 4 TB   | 15      | 1001  | 0     | 2.74   |
| Toshiba   | MD04ACA400         | 4 TB   | 30      | 1227  | 251   | 2.74   |
| WDC       | WD6001FZWX-00A2VA0 | 6 TB   | 12      | 1073  | 1     | 2.74   |
| Seagate   | ST3160215ACE       | 160 GB | 7       | 1232  | 187   | 2.74   |
| Seagate   | ST3500641AS        | 500 GB | 9       | 1599  | 26    | 2.74   |
| Toshiba   | MK3255GSXF         | 320 GB | 2       | 1185  | 1     | 2.74   |
| Hitachi   | HDE721010SLA330    | 1 TB   | 13      | 1855  | 15    | 2.74   |
| Seagate   | ST1500LM003-9YH148 | 1.5 TB | 2       | 996   | 0     | 2.73   |
| Seagate   | ST3400833AS        | 400 GB | 2       | 996   | 0     | 2.73   |
| WDC       | WD5000AAKS-65A7B2  | 500 GB | 3       | 996   | 0     | 2.73   |
| WDC       | WD2000FYYZ-05UL1B0 | 2 TB   | 2       | 996   | 0     | 2.73   |
| HGST      | HUH721010ALN600    | 10 TB  | 5       | 995   | 0     | 2.73   |
| WDC       | WD20EFRX-68AX9N0   | 2 TB   | 38      | 1340  | 2     | 2.72   |
| WDC       | WD6401AALS-22A7B2  | 640 GB | 1       | 993   | 0     | 2.72   |
| WDC       | WD2500LPVX-00V0TT0 | 250 GB | 1       | 992   | 0     | 2.72   |
| WDC       | WD5000KS-00MNB0    | 500 GB | 1       | 992   | 0     | 2.72   |
| WDC       | WD3200JS-63PDB1    | 320 GB | 3       | 1327  | 217   | 2.71   |
| WDC       | WD6400AAKS-65A7B2  | 640 GB | 27      | 1417  | 19    | 2.71   |
| WDC       | WD1000FYPS-01ZKB0  | 1 TB   | 1       | 989   | 0     | 2.71   |
| WDC       | WD1001FALS-00E3A0  | 1 TB   | 8       | 1483  | 207   | 2.71   |
| Hitachi   | HDT725025VLA380    | 250 GB | 28      | 1274  | 19    | 2.70   |
| WDC       | WD7500BPVT-35HXZT3 | 752 GB | 3       | 1069  | 2     | 2.70   |
| Seagate   | ST3120023A         | 120 GB | 1       | 985   | 0     | 2.70   |
| Hitachi   | HDS5C3020ALA632    | 2 TB   | 28      | 1308  | 22    | 2.70   |
| WDC       | WD6400AACS-00G8B0  | 640 GB | 9       | 1126  | 72    | 2.69   |
| Seagate   | ST4000NM0033-9Z... | 4 TB   | 37      | 1503  | 313   | 2.69   |
| WDC       | WD3200AAKX-221CA0  | 320 GB | 1       | 981   | 0     | 2.69   |
| WDC       | WD1002FBYS-18A6B0  | 1 TB   | 3       | 2376  | 19    | 2.69   |
| WDC       | WD400JB-00JJC0     | 40 GB  | 1       | 980   | 0     | 2.69   |
| WDC       | WD2003FZEX-00Z4SA0 | 2 TB   | 69      | 1179  | 20    | 2.69   |
| WDC       | WD3200BMVW-11AMCS4 | 320 GB | 1       | 979   | 0     | 2.68   |
| Toshiba   | MG03ACA400         | 4 TB   | 8       | 979   | 0     | 2.68   |
| Quantum   | FIREBALLP KX13.6   | 16 GB  | 1       | 975   | 0     | 2.67   |
| Seagate   | ST3320413CS        | 320 GB | 15      | 1096  | 76    | 2.67   |
| WDC       | WD1600AAJB-56R1A0  | 160 GB | 3       | 1041  | 3     | 2.67   |
| WDC       | WD10EFRX-68JCSN0   | 1 TB   | 36      | 1199  | 107   | 2.66   |
| WDC       | WD20EARX-00PASB0   | 2 TB   | 240     | 1222  | 77    | 2.66   |
| WDC       | WD5000AAVS-00ZTB0  | 500 GB | 20      | 1269  | 74    | 2.66   |
| HGST      | HUS726040ALE614    | 4 TB   | 8       | 970   | 0     | 2.66   |
| WDC       | WD5000AVVS-00ZWB0  | 500 GB | 1       | 970   | 0     | 2.66   |
| Toshiba   | DT01ABA050V        | 500 GB | 2       | 969   | 0     | 2.66   |
| WDC       | WD4002FYYZ-01B7CB1 | 4 TB   | 5       | 968   | 0     | 2.65   |
| WDC       | WD10EALX-079BA1    | 1 TB   | 1       | 968   | 0     | 2.65   |
| Hitachi   | HDS721016CLA382    | 160 GB | 13      | 1269  | 79    | 2.65   |
| WDC       | WD1002FBYS-18W8B0  | 1 TB   | 4       | 1397  | 1     | 2.65   |
| Toshiba   | MK1229GSGF         | 80 GB  | 1       | 6753  | 6     | 2.64   |
| WDC       | WD1600HLFS-75G6U1  | 160 GB | 3       | 964   | 0     | 2.64   |
| WDC       | WD7500KMVV-11TK7S1 | 752 GB | 2       | 964   | 0     | 2.64   |
| Seagate   | ST3000VN000-1HJ166 | 3 TB   | 16      | 963   | 0     | 2.64   |
| WDC       | WD5000AAKS-00YGA0  | 500 GB | 27      | 1173  | 3     | 2.64   |
| Toshiba   | MG04ACA400E        | 4 TB   | 13      | 961   | 0     | 2.63   |
| Toshiba   | MK4032GAX          | 40 GB  | 1       | 960   | 0     | 2.63   |
| WDC       | WD200EB-00CPF0     | 20 GB  | 1       | 960   | 0     | 2.63   |
| Apple     | HDD HTS727575A9... | 752 GB | 4       | 960   | 0     | 2.63   |
| Seagate   | ST1000NM0095-2D... | 1 TB   | 4       | 1306  | 509   | 2.63   |
| WDC       | WD10EARS-003BB1    | 1 TB   | 19      | 1063  | 91    | 2.63   |
| WDC       | WD2000JS-00MVB1    | 200 GB | 1       | 957   | 0     | 2.62   |
| WDC       | WD1600AAJS-08B4A0  | 160 GB | 2       | 957   | 0     | 2.62   |
| WDC       | WD7502AAEX-00Z3A0  | 752 GB | 1       | 956   | 0     | 2.62   |
| WDC       | WD30EZRX-00MMMB0   | 3 TB   | 57      | 1227  | 36    | 2.62   |
| WDC       | WD2500BMVS-11F9S0  | 250 GB | 1       | 954   | 0     | 2.62   |
| WDC       | WD20NMVW-11W68S0   | 2 TB   | 9       | 1152  | 10    | 2.62   |
| Hitachi   | HDT722520DLA380    | 200 GB | 5       | 1127  | 2     | 2.62   |
| WDC       | WD3000HLFS-01G6U0  | 304 GB | 2       | 953   | 0     | 2.61   |
| WDC       | WD7500AALX-009BA0  | 752 GB | 8       | 950   | 0     | 2.60   |
| Toshiba   | DT01ABA200V        | 2 TB   | 4       | 1013  | 42    | 2.60   |
| WDC       | WD1600BB-22RDA0    | 160 GB | 2       | 947   | 0     | 2.60   |
| WDC       | WD2500AAKX-22ERMA0 | 250 GB | 2       | 946   | 0     | 2.59   |
| Quantum   | FIREBALLP AS20.5   | 20 GB  | 1       | 946   | 0     | 2.59   |
| WDC       | WD2500JD-00GBB0    | 250 GB | 1       | 944   | 0     | 2.59   |
| HGST      | HTE725032A7E630    | 320 GB | 1       | 943   | 0     | 2.58   |
| Seagate   | ST500LX003-1AC15G  | 500 GB | 4       | 1051  | 8     | 2.58   |
| WDC       | WD20EURS-63S48Y0   | 2 TB   | 14      | 1244  | 147   | 2.58   |
| WDC       | WD1001FALS-41Y6A1  | 1 TB   | 1       | 938   | 0     | 2.57   |
| WDC       | WD800JD-60LSA5     | 80 GB  | 27      | 984   | 1     | 2.57   |
| Toshiba   | MD04ABA400V        | 4 TB   | 3       | 936   | 0     | 2.57   |
| Seagate   | ST3320620NS        | 320 GB | 5       | 1540  | 2     | 2.56   |
| WDC       | WD10EZEX-00KUWA0   | 1 TB   | 46      | 1065  | 1     | 2.56   |
| WDC       | WD5000AAKB-00YSA0  | 500 GB | 2       | 935   | 0     | 2.56   |
| Hitachi   | HDS723015BLA642    | 1.5 TB | 10      | 1088  | 20    | 2.56   |
| WDC       | WD30EZRX-00DC0B0   | 3 TB   | 74      | 1120  | 26    | 2.56   |
| Seagate   | ST500LM024-1RS152  | 500 GB | 2       | 932   | 0     | 2.56   |
| WDC       | WD2500AAJS-75M0A0  | 250 GB | 25      | 1097  | 82    | 2.55   |
| WDC       | WD80EFZX-68UW8N0   | 8 TB   | 21      | 968   | 1     | 2.55   |
| Hitachi   | HDS721010CLA632    | 1 TB   | 17      | 1356  | 8     | 2.55   |
| WDC       | WD10EADS-65M2B0    | 1 TB   | 14      | 1223  | 83    | 2.54   |
| Samsung   | HD400LD            | 400 GB | 5       | 1135  | 150   | 2.54   |
| Seagate   | OOS1000G           | 1 TB   | 1       | 925   | 0     | 2.54   |
| Seagate   | ST1000NM0011 43... | 1 TB   | 1       | 925   | 0     | 2.53   |
| Seagate   | ST3000VX000-1CU166 | 3 TB   | 9       | 925   | 7     | 2.53   |
| WDC       | WD1600JS-55MHB1    | 160 GB | 3       | 924   | 0     | 2.53   |
| WDC       | WD800JB-00DUA3     | 80 GB  | 1       | 923   | 0     | 2.53   |
| WDC       | WD30EFRX-68EUZN0   | 3 TB   | 233     | 1113  | 5     | 2.53   |
| WDC       | WD5003ABYX-50WERA1 | 500 GB | 1       | 922   | 0     | 2.53   |
| WDC       | WD10TMVW-11ZSMS5   | 1 TB   | 18      | 1142  | 218   | 2.52   |
| WDC       | WD1600JB-00REA0    | 160 GB | 9       | 1095  | 133   | 2.52   |
| Seagate   | ST4000DM000-1F2168 | 4 TB   | 165     | 1108  | 126   | 2.52   |
| WDC       | WD6401AALS-00L3B2  | 640 GB | 30      | 1182  | 4     | 2.52   |
| WDC       | WD3202ABYS-02B7A0  | 320 GB | 8       | 1039  | 11    | 2.51   |
| Seagate   | ST4000VM000-1F3168 | 4 TB   | 6       | 917   | 0     | 2.51   |
| WDC       | WD3200AAKX-603CA0  | 320 GB | 1       | 914   | 0     | 2.51   |
| HGST      | HMS5C4040ALE640    | 4 TB   | 7       | 913   | 0     | 2.50   |
| Toshiba   | MK2561GSY          | 250 GB | 2       | 913   | 0     | 2.50   |
| Seagate   | ST3300622A         | 304 GB | 1       | 912   | 0     | 2.50   |
| WDC       | WD6400AAKS-75A7B2  | 640 GB | 9       | 1024  | 3     | 2.50   |
| WDC       | WD3200AAVS-00ZTB0  | 320 GB | 2       | 1145  | 1     | 2.49   |
| WDC       | WD800JB-00FMA0     | 80 GB  | 2       | 1099  | 343   | 2.49   |
| Seagate   | ST91000640NS 81... | 1 TB   | 1       | 909   | 0     | 2.49   |
| WDC       | WD20EARX-00MMMB0   | 2 TB   | 4       | 1284  | 4     | 2.49   |
| WDC       | WD15EARS-00J2GB0   | 1.5 TB | 1       | 908   | 0     | 2.49   |
| Seagate   | ST3250820AS P      | 250 GB | 1       | 907   | 0     | 2.49   |
| Seagate   | ST4000NM0124-1R... | 4 TB   | 1       | 906   | 0     | 2.48   |
| WDC       | WD5002ABYS-01B1B0  | 500 GB | 17      | 1389  | 3     | 2.48   |
| Seagate   | ST9160314ASG       | 160 GB | 1       | 903   | 0     | 2.47   |
| WDC       | WD2500JS-60NCB2    | 250 GB | 3       | 903   | 0     | 2.47   |
| Seagate   | ST3000DM003-1F216N | 3 TB   | 6       | 1255  | 27    | 2.47   |
| Seagate   | ST3500418ASQ       | 500 GB | 4       | 1387  | 259   | 2.47   |
| WDC       | WD3003FZEX-00Z4SA0 | 3 TB   | 9       | 1087  | 113   | 2.47   |
| WDC       | WD1600BB-00RDA0    | 160 GB | 4       | 1124  | 20    | 2.47   |
| WDC       | WD800BEVS-08RST3   | 80 GB  | 1       | 900   | 0     | 2.47   |
| WDC       | WD400BB-71DGA0     | 40 GB  | 1       | 900   | 0     | 2.47   |
| WDC       | WD3200LPVX-00V0TT0 | 320 GB | 3       | 900   | 0     | 2.47   |
| WDC       | WD10EZEX-08RKKA0   | 1 TB   | 10      | 900   | 0     | 2.47   |
| WDC       | WD6400AAKS-00A7B0  | 640 GB | 18      | 1040  | 3     | 2.46   |
| Hitachi   | HUS724040ALE640    | 4 TB   | 6       | 930   | 64    | 2.45   |
| WDC       | WD1600AABS-00PRA0  | 160 GB | 5       | 894   | 0     | 2.45   |
| Fujitsu   | MHW2160BHPL        | 160 GB | 1       | 894   | 0     | 2.45   |
| WDC       | WD7500BPKX-75HPJT0 | 752 GB | 9       | 894   | 0     | 2.45   |
| Seagate   | ST3500630NS        | 500 GB | 12      | 1138  | 392   | 2.45   |
| WDC       | WD20EARX-22PASB0   | 2 TB   | 7       | 1221  | 2     | 2.44   |
| Seagate   | ST3000NC002-1DY166 | 3 TB   | 5       | 1190  | 598   | 2.44   |
| Hitachi   | HUA722050CLA330    | 500 GB | 4       | 891   | 0     | 2.44   |
| WDC       | WD20EARS-00J2GB0   | 2 TB   | 14      | 1595  | 107   | 2.44   |
| Hitachi   | HDS5C3030BLE630    | 3 TB   | 4       | 890   | 0     | 2.44   |
| HGST      | HDN721010ALE604    | 10 TB  | 1       | 889   | 0     | 2.44   |
| WDC       | WD10EARX-22N0YB0   | 1 TB   | 3       | 1079  | 697   | 2.44   |
| Seagate   | ST4000NM0245-1Z... | 4 TB   | 8       | 975   | 1     | 2.43   |
| WDC       | WD800BB-22HEA1     | 80 GB  | 1       | 888   | 0     | 2.43   |
| WDC       | WD30EZRX-00SPEB0   | 3 TB   | 33      | 1051  | 9     | 2.43   |
| HGST      | HTE541010A9E680    | 1 TB   | 2       | 913   | 509   | 2.43   |
| WDC       | WD2500AAJS-55RYA0  | 250 GB | 2       | 887   | 0     | 2.43   |
| WDC       | WD1003FZEX-00RLFA0 | 1 TB   | 3       | 886   | 0     | 2.43   |
| WDC       | WD3200AAJB-00TYA0  | 320 GB | 4       | 885   | 0     | 2.43   |
| WDC       | WD20EZRX-00DC0B0   | 2 TB   | 75      | 1076  | 23    | 2.42   |
| WDC       | WD30EZRX-00D8PB0   | 3 TB   | 79      | 948   | 6     | 2.42   |
| WDC       | WD5000AAKS-65V0A0  | 500 GB | 7       | 1369  | 150   | 2.42   |
| Seagate   | ST91000640NS 81... | 1 TB   | 1       | 883   | 0     | 2.42   |
| WDC       | WD1005FBYZ-01YCBB1 | 1 TB   | 6       | 883   | 0     | 2.42   |
| Hitachi   | HDS5C1010CLA382    | 1 TB   | 14      | 1080  | 36    | 2.41   |
| WDC       | WD800AAJS-19M0A0   | 80 GB  | 1       | 880   | 0     | 2.41   |
| WDC       | WD5000KMVV-11TK7S1 | 500 GB | 1       | 880   | 0     | 2.41   |
| WDC       | WD3200JD-00KLB0    | 320 GB | 2       | 879   | 0     | 2.41   |
| Hitachi   | HDE721064SLA360    | 640 GB | 4       | 1234  | 4     | 2.41   |
| WDC       | WD5001AALS-00E3A0  | 500 GB | 18      | 1401  | 69    | 2.40   |
| Samsung   | HD083GJ            | 80 GB  | 6       | 876   | 0     | 2.40   |
| WDC       | WD40EFRX-68WT0N0   | 4 TB   | 161     | 1165  | 6     | 2.40   |
| Seagate   | ST2000VN000-1HJ164 | 2 TB   | 9       | 874   | 0     | 2.40   |
| WDC       | WD30EZRS-42KEZB0   | 3 TB   | 1       | 874   | 0     | 2.40   |
| WDC       | WD1003FBYX-01Y7B0  | 1 TB   | 23      | 1494  | 95    | 2.40   |
| WDC       | WD1600BB-56RDA0    | 160 GB | 3       | 874   | 0     | 2.40   |
| Hitachi   | HTS545050B9SA02    | 500 GB | 2       | 1756  | 3     | 2.40   |
| HGST      | HUS722T2TALA604    | 2 TB   | 8       | 873   | 0     | 2.39   |
| WDC       | WD1002FAEX-007BA0  | 1 TB   | 6       | 907   | 1     | 2.39   |
| Seagate   | ST8000VN0022-2E... | 8 TB   | 70      | 978   | 5     | 2.39   |
| WDC       | WD2500YS-01SHB1    | 250 GB | 13      | 1172  | 10    | 2.39   |
| WDC       | WD6400AACS-00G8B1  | 640 GB | 15      | 1181  | 18    | 2.38   |
| WDC       | WD1200JS-55NCB1    | 120 GB | 2       | 869   | 0     | 2.38   |
| WDC       | WD5000AACS-00ZUB0  | 500 GB | 20      | 1025  | 6     | 2.38   |
| WDC       | WD2500BMVU-11A04S0 | 250 GB | 1       | 866   | 0     | 2.37   |
| Magnet... | MD05000-BQDW-RO    | 500 GB | 2       | 865   | 0     | 2.37   |
| WDC       | WD800BB-75JHA0     | 80 GB  | 1       | 865   | 0     | 2.37   |
| WDC       | WD5000AZDX-00SC2B0 | 500 GB | 7       | 1062  | 8     | 2.37   |
| WDC       | WD6400AAVS-00G9B1  | 640 GB | 3       | 1491  | 95    | 2.37   |
| HP        | MB1000EBZQB        | 1 TB   | 1       | 863   | 0     | 2.37   |
| Seagate   | ST1000NM0065-1V... | 1 TB   | 1       | 861   | 0     | 2.36   |
| Seagate   | ST3320413AS        | 320 GB | 30      | 1127  | 29    | 2.36   |
| HP        | VB0250EAVER        | 250 GB | 20      | 1200  | 3     | 2.36   |
| WDC       | WD800JD-75MSA3     | 80 GB  | 47      | 1122  | 27    | 2.35   |
| WDC       | WD1600AAJS-75WAA0  | 160 GB | 3       | 857   | 0     | 2.35   |
| Seagate   | ST1000LX001-1EM164 | 1 TB   | 1       | 857   | 0     | 2.35   |
| WDC       | WD6400AAKS-22A7B0  | 640 GB | 25      | 1260  | 44    | 2.34   |
| WDC       | WD800AAJS-22PSA0   | 80 GB  | 4       | 852   | 0     | 2.33   |
| WDC       | WD1600AAJS-60PSA0  | 160 GB | 5       | 989   | 206   | 2.33   |
| Samsung   | HD203WI            | 2 TB   | 9       | 900   | 2     | 2.33   |
| WDC       | WD2500JS-55NCB1    | 250 GB | 9       | 1083  | 11    | 2.33   |
| WDC       | WD3200AAKS-75VYA0  | 320 GB | 4       | 846   | 0     | 2.32   |
| WDC       | WD1001FALS-00E8B0  | 1 TB   | 18      | 1293  | 125   | 2.32   |
| HGST      | HUS726060ALE614    | 6 TB   | 10      | 868   | 57    | 2.31   |
| WDC       | WD3200AAKS-00YGA0  | 320 GB | 5       | 933   | 1     | 2.31   |
| Samsung   | HE103SJ            | 1 TB   | 6       | 2421  | 24    | 2.31   |
| WDC       | WD10JMVW-59AJGS3   | 1 TB   | 2       | 840   | 0     | 2.30   |
| WDC       | WD5000AAKS-07YGA0  | 500 GB | 5       | 896   | 1     | 2.30   |
| WDC       | WD20EADS-00W4B0    | 2 TB   | 2       | 837   | 0     | 2.29   |
| WDC       | WD7501AALS-00J7B0  | 752 GB | 26      | 1246  | 126   | 2.29   |
| WDC       | WD10EALX-089BA0    | 1 TB   | 2       | 836   | 0     | 2.29   |
| Seagate   | ST1000VM002-1ET162 | 1 TB   | 10      | 896   | 12    | 2.29   |
| WDC       | WD7500BPVT-08A1YT2 | 752 GB | 1       | 835   | 0     | 2.29   |
| WDC       | WD20EZRX-00D8PB0   | 2 TB   | 167     | 921   | 37    | 2.29   |
| Hitachi   | HCS5C3232SLA380    | 320 GB | 4       | 903   | 1     | 2.29   |
| Hitachi   | HTS722020K9SA00... | 200 GB | 1       | 835   | 0     | 2.29   |
| WDC       | WD40EZRX-00SPEB0   | 4 TB   | 71      | 961   | 28    | 2.29   |
| WDC       | WD10EAVS-00D7B1    | 1 TB   | 43      | 1318  | 61    | 2.28   |
| WDC       | WD1600JS-60MHB1    | 160 GB | 7       | 975   | 4     | 2.28   |
| Seagate   | ST4000DX001-1CE168 | 4 TB   | 26      | 997   | 33    | 2.28   |
| Samsung   | HD300LJ            | 304 GB | 14      | 1247  | 245   | 2.28   |
| Seagate   | ST3000DM001-1ER166 | 3 TB   | 121     | 1031  | 171   | 2.27   |
| Hitachi   | HUA723020ALA641    | 2 TB   | 60      | 1045  | 41    | 2.27   |
| Seagate   | ST3500630A         | 500 GB | 10      | 1351  | 427   | 2.27   |
| WDC       | WD1600AAJS-00PSA0  | 160 GB | 40      | 1007  | 36    | 2.27   |
| WDC       | WD800AAJS-60WAA0   | 80 GB  | 2       | 828   | 0     | 2.27   |
| WDC       | WD5000HHTZ-04N21V0 | 500 GB | 10      | 1004  | 1     | 2.27   |
| WDC       | WD20EFRX-68EUZN0   | 2 TB   | 203     | 1013  | 9     | 2.26   |
| WDC       | WD800JD-08MSA1     | 80 GB  | 4       | 826   | 0     | 2.26   |
| WDC       | WD400BD-75LRA0     | 40 GB  | 2       | 825   | 0     | 2.26   |
| Hitachi   | HUS724030ALE641    | 3 TB   | 38      | 922   | 87    | 2.26   |
| Toshiba   | DT01ABA200         | 2 TB   | 20      | 848   | 1     | 2.26   |
| WDC       | WD800BD-88JMC0     | 80 GB  | 2       | 824   | 0     | 2.26   |
| WDC       | WD20EADS-11R6B1    | 2 TB   | 2       | 1529  | 8     | 2.26   |
| Seagate   | ST33000651NS       | 3 TB   | 10      | 1676  | 141   | 2.26   |
| Seagate   | ST2000VN0001-1S... | 2 TB   | 2       | 823   | 0     | 2.25   |
| Hitachi   | HDS728040PLAT20    | 41 GB  | 5       | 979   | 1     | 2.25   |
| Hitachi   | HDS722580VLSA80    | 82 GB  | 5       | 1092  | 403   | 2.25   |
| WDC       | WD20EURS-73TLHY0   | 2 TB   | 2       | 1360  | 2     | 2.25   |
| WDC       | WD101KRYZ-01JPDB1  | 10 TB  | 5       | 821   | 0     | 2.25   |
| WDC       | WD10JPVT-80A1YT0   | 1 TB   | 2       | 820   | 0     | 2.25   |
| HP        | MB2000EBZQC        | 2 TB   | 4       | 880   | 39    | 2.25   |
| Seagate   | ST3250620NS        | 250 GB | 19      | 1377  | 400   | 2.25   |
| WDC       | WD5000AAKS-00A7B0  | 500 GB | 58      | 1337  | 21    | 2.24   |
| Seagate   | ST12000NM0007-2... | 12 TB  | 20      | 919   | 9     | 2.24   |
| Seagate   | ST3000NM0033-9Z... | 3 TB   | 8       | 927   | 3     | 2.24   |
| WDC       | WD2500BEVE-00WZT0  | 250 GB | 2       | 817   | 0     | 2.24   |
| WDC       | WD400BB-00LNA0     | 40 GB  | 1       | 817   | 0     | 2.24   |
| WDC       | WD2500AAJS-08L7A0  | 250 GB | 5       | 816   | 0     | 2.24   |
| WDC       | WD10EADS-00M2B0    | 1 TB   | 68      | 1287  | 60    | 2.23   |
| Seagate   | ST3250823AS        | 250 GB | 26      | 1406  | 37    | 2.23   |
| HP        | GB1000EAMYC        | 1 TB   | 2       | 814   | 0     | 2.23   |
| WDC       | WD2500JB-00GVC0    | 250 GB | 2       | 811   | 0     | 2.22   |
| Seagate   | ST10000NM0016-1... | 10 TB  | 19      | 811   | 0     | 2.22   |
| HGST      | HCC725050A7E630    | 500 GB | 1       | 810   | 0     | 2.22   |
| Toshiba   | MK1002TSKB         | 1 TB   | 2       | 1657  | 5     | 2.21   |
| Toshiba   | MG04ACA400N        | 4 TB   | 1       | 808   | 0     | 2.21   |
| WDC       | WD1600JS-55NCB1    | 160 GB | 9       | 808   | 0     | 2.21   |
| WDC       | WD2500HHTZ-04N21V0 | 250 GB | 10      | 856   | 1     | 2.21   |
| HGST      | HDN726050ALE610    | 5 TB   | 2       | 1524  | 4     | 2.21   |
| WDC       | WD2000JS-22MHB0    | 200 GB | 5       | 1828  | 19    | 2.21   |
| Toshiba   | DT01ABA300         | 3 TB   | 15      | 820   | 1     | 2.21   |
| Seagate   | ST3120213AS        | 120 GB | 1       | 806   | 0     | 2.21   |
| Hitachi   | HCC543225A7A380    | 250 GB | 4       | 1159  | 1     | 2.21   |
| WDC       | WD5000AADS-00L4B1  | 500 GB | 12      | 1104  | 55    | 2.21   |
| WDC       | WD800AAJS-00PSA0   | 80 GB  | 30      | 894   | 25    | 2.20   |
| Hitachi   | HTS723232L9SA62    | 320 GB | 1       | 804   | 0     | 2.20   |
| Hitachi   | HDS7250SASUN500G   | 500 GB | 2       | 802   | 0     | 2.20   |
| Seagate   | ST4000DX002-1H2178 | 4 TB   | 2       | 801   | 0     | 2.20   |
| HGST      | HUS726040ALA610    | 4 TB   | 6       | 801   | 0     | 2.20   |
| Seagate   | ST3400620AS        | 400 GB | 38      | 1293  | 71    | 2.20   |
| WDC       | WD5000BMVV-11GNWS0 | 500 GB | 6       | 1014  | 15    | 2.19   |
| WDC       | WD15EARS-00S8B1    | 1.5 TB | 9       | 1710  | 4     | 2.19   |
| WDC       | WD800AAJS-60PSA0   | 80 GB  | 3       | 1007  | 336   | 2.19   |
| WDC       | WD30NMVW-11C3NS4   | 3 TB   | 1       | 799   | 0     | 2.19   |
| WDC       | WD7500AAKS-00RBA0  | 752 GB | 16      | 1192  | 34    | 2.19   |
| Fujitsu   | MHV2060AH PL       | 64 GB  | 2       | 796   | 0     | 2.18   |
| Seagate   | ST3320633AS        | 320 GB | 1       | 795   | 0     | 2.18   |
| Samsung   | HD103SJ            | 1 TB   | 223     | 1049  | 29    | 2.18   |
| HGST      | HUH728080ALE601    | 8 TB   | 24      | 1276  | 3     | 2.18   |
| WDC       | WD50EZRZ-32RWYB1   | 5 TB   | 3       | 1131  | 3     | 2.18   |
| Apple     | HDD HTS541075A9... | 752 GB | 1       | 792   | 0     | 2.17   |
| WDC       | WD20EADS-00S2B0    | 2 TB   | 9       | 1232  | 116   | 2.17   |
| WDC       | WD1600ADFD-60NLR5  | 160 GB | 4       | 790   | 0     | 2.17   |
| Toshiba   | DT01ACA300         | 3 TB   | 196     | 896   | 40    | 2.17   |
| Toshiba   | MQ01ABD032V        | 320 GB | 2       | 790   | 303   | 2.16   |
| Seagate   | ST380012A          | 80 GB  | 2       | 787   | 0     | 2.16   |
| Seagate   | ST2000DL001-9VT156 | 2 TB   | 31      | 1180  | 268   | 2.16   |
| HP        | MB1000ECWCQ        | 1 TB   | 1       | 787   | 0     | 2.16   |
| WDC       | WD80EZZX-11CSGA0   | 8 TB   | 8       | 787   | 0     | 2.16   |
| Seagate   | ST3000VN007-2E4166 | 3 TB   | 11      | 786   | 0     | 2.16   |
| WDC       | WD10EZEX-75M2NA0   | 1 TB   | 44      | 885   | 2     | 2.15   |
| WDC       | WD1600JB-00GVA0    | 160 GB | 2       | 784   | 0     | 2.15   |
| WDC       | WD20EARS-00MVWB0   | 2 TB   | 161     | 1302  | 121   | 2.15   |
| WDC       | WD1600AAJS-07WAA0  | 160 GB | 5       | 1143  | 170   | 2.15   |
| Seagate   | ST32000644NS       | 2 TB   | 19      | 1251  | 184   | 2.15   |
| WDC       | WD40EZRX-19SPEB0   | 4 TB   | 2       | 921   | 4     | 2.14   |
| Hitachi   | HCS5C3225SLA380    | 250 GB | 3       | 1073  | 3     | 2.14   |
| Seagate   | ST91603110CS       | 160 GB | 1       | 781   | 0     | 2.14   |
| WDC       | WD3000HLFS-01MZUV0 | 304 GB | 4       | 1279  | 268   | 2.14   |
| WDC       | WD1001FALS-403AA0  | 1 TB   | 11      | 954   | 3     | 2.13   |
| WDC       | WD5000AAKS-07TMA0  | 500 GB | 2       | 778   | 0     | 2.13   |
| WDC       | WD7500BPKX-80HPJT0 | 752 GB | 7       | 778   | 0     | 2.13   |
| WDC       | WD400BD-75MRA1     | 40 GB  | 3       | 778   | 0     | 2.13   |
| WDC       | WD1200JB-00DUA3    | 120 GB | 2       | 1239  | 2     | 2.13   |
| WDC       | WD10EURX-63C57Y0   | 1 TB   | 12      | 994   | 1     | 2.12   |
| WDC       | WD2500BB-00GUA0    | 250 GB | 1       | 773   | 0     | 2.12   |
| WDC       | WD2000BB-00RDA0    | 200 GB | 1       | 1546  | 1     | 2.12   |
| WDC       | WD10EZEX-22RKKA0   | 1 TB   | 16      | 1068  | 3     | 2.12   |
| WDC       | WD2005FBYZ-01YCBB2 | 2 TB   | 25      | 803   | 1     | 2.11   |
| WDC       | WD10EACS-65D6B0    | 1 TB   | 5       | 987   | 32    | 2.11   |
| Seagate   | ST12000NE0007-2... | 12 TB  | 4       | 771   | 0     | 2.11   |
| WDC       | WD5000BMVW-11AMCS4 | 500 GB | 8       | 893   | 1     | 2.11   |
| Hitachi   | HTS723225L9A362    | 250 GB | 1       | 770   | 0     | 2.11   |
| WDC       | WD10JPVT-55A1YT0   | 1 TB   | 4       | 968   | 1     | 2.11   |
| Seagate   | ST10000VN0004-1... | 10 TB  | 39      | 958   | 8     | 2.11   |
| Seagate   | ST3000LM016-1N217V | 3 TB   | 3       | 768   | 0     | 2.11   |
| WDC       | WD60EZRX-00MVLB1   | 6 TB   | 19      | 905   | 2     | 2.11   |
| WDC       | WD7500BPVT-35HXZT1 | 752 GB | 1       | 766   | 0     | 2.10   |
| Hitachi   | HTS545032B9SA02    | 320 GB | 8       | 969   | 12    | 2.09   |
| HGST      | HUS724040ALE640    | 4 TB   | 10      | 762   | 0     | 2.09   |
| Seagate   | ST3400620A         | 400 GB | 5       | 1706  | 115   | 2.09   |
| WDC       | WD8001FFWX-68J1UN0 | 8 TB   | 4       | 760   | 0     | 2.08   |
| Seagate   | ST8000NM0055-1R... | 8 TB   | 45      | 859   | 7     | 2.08   |
| WDC       | WD10EFRX-68PJCN0   | 1 TB   | 45      | 876   | 1     | 2.08   |
| WDC       | WD5002AALX-00J37A0 | 500 GB | 28      | 984   | 39    | 2.07   |
| WDC       | WD2500JD-55HBB0    | 250 GB | 2       | 1468  | 16    | 2.07   |
| WDC       | WD800JD-75JNA0     | 80 GB  | 6       | 1214  | 20    | 2.07   |
| Seagate   | ST3320620AS        | 320 GB | 186     | 1220  | 224   | 2.07   |
| WDC       | WD1003FBYZ-010FB0  | 1 TB   | 25      | 844   | 2     | 2.07   |
| WDC       | WD2500JS-22NCB1    | 250 GB | 14      | 1430  | 71    | 2.07   |
| Hitachi   | HDS721050CLA662    | 500 GB | 29      | 838   | 38    | 2.07   |
| Seagate   | ST4000DM005-2DP166 | 4 TB   | 59      | 767   | 29    | 2.06   |
| Hitachi   | HUS724030ALA640    | 3 TB   | 3       | 1205  | 1     | 2.06   |
| WDC       | WD1001FALS-75J7B0  | 1 TB   | 4       | 1195  | 4     | 2.06   |
| WDC       | WD3200AAKX-221CA1  | 320 GB | 5       | 751   | 0     | 2.06   |
| WDC       | WD3000JS-19PDB0    | 304 GB | 1       | 751   | 0     | 2.06   |
| Toshiba   | MQ01ABB200         | 2 TB   | 27      | 866   | 171   | 2.05   |
| Seagate   | ST3200826AS        | 200 GB | 19      | 1137  | 51    | 2.05   |
| Hitachi   | HDS5C3020BLE630    | 2 TB   | 11      | 1185  | 125   | 2.05   |
| Seagate   | ST2000NM0033-9Z... | 2 TB   | 17      | 885   | 92    | 2.05   |
| WDC       | WD3200AAKX-083CA1  | 320 GB | 4       | 746   | 0     | 2.05   |
| Seagate   | ST3500312CS        | 500 GB | 125     | 982   | 119   | 2.04   |
| WDC       | WD5000AAKS-00C8A0  | 500 GB | 4       | 1134  | 324   | 2.04   |
| Quantum   | FIREBALLP AS40.0   | 40 GB  | 1       | 744   | 0     | 2.04   |
| Seagate   | ST3300831AS        | 304 GB | 6       | 1545  | 346   | 2.04   |
| Seagate   | ST3750640A         | 752 GB | 2       | 1111  | 1025  | 2.04   |
| WDC       | WD6001F4PZ-49CWHM0 | 6 TB   | 1       | 743   | 0     | 2.04   |
| WDC       | WD2500KS-00MJB0    | 250 GB | 39      | 1018  | 13    | 2.04   |
| HGST      | HDN726060ALE614    | 6 TB   | 11      | 844   | 1     | 2.03   |
| WDC       | WD5003AZEX-00MK2A0 | 500 GB | 19      | 772   | 1     | 2.03   |
| WDC       | WD30EZRS-00J99B0   | 3 TB   | 12      | 1239  | 489   | 2.03   |
| WDC       | WD20EZRX-07D8PB0   | 2 TB   | 2       | 739   | 0     | 2.03   |
| WDC       | WD10EALS-00Z8A0    | 1 TB   | 37      | 1065  | 41    | 2.02   |
| WDC       | WD5000AAJS-00TKA0  | 500 GB | 3       | 737   | 0     | 2.02   |
| WDC       | WD5000AAKS-00D2B0  | 500 GB | 21      | 1218  | 28    | 2.02   |
| WDC       | WD2500AAJS-00VTA0  | 250 GB | 29      | 907   | 58    | 2.02   |
| WDC       | WD1600JS-75NCB3    | 160 GB | 6       | 1233  | 2     | 2.02   |
| WDC       | WD6000HLHX-01JJPV0 | 600 GB | 13      | 1217  | 11    | 2.01   |
| WDC       | WD2000F9YZ-09N20L1 | 2 TB   | 1       | 733   | 0     | 2.01   |
| Hitachi   | HDS723030BLE640    | 3 TB   | 2       | 841   | 1010  | 2.01   |
| WDC       | WD5003ABYX-01WERA2 | 500 GB | 2       | 733   | 0     | 2.01   |
| WDC       | WD7500BPVT-80HXZT1 | 752 GB | 2       | 1049  | 3     | 2.01   |
| WDC       | WD5001AALS-00L3B2  | 500 GB | 49      | 1076  | 38    | 2.01   |
| HGST      | HDN724020ALE640    | 2 TB   | 1       | 732   | 0     | 2.01   |
| WDC       | WD1200JB-00EVA0    | 120 GB | 4       | 731   | 0     | 2.00   |
| Hitachi   | HUA722010CLA630    | 1 TB   | 6       | 1349  | 13    | 2.00   |
| WDC       | WD80EMAZ-00WJTA0   | 8 TB   | 64      | 730   | 0     | 2.00   |
| WDC       | WD2003FYYS-02W0B1  | 2 TB   | 19      | 1058  | 12    | 2.00   |
| WDC       | WD5003ABYZ-011FA0  | 500 GB | 23      | 842   | 3     | 2.00   |
| WDC       | WD10EARX-00N0YB0   | 1 TB   | 98      | 948   | 28    | 1.99   |
| Seagate   | ST1000VX001-1Z4102 | 1 TB   | 4       | 726   | 0     | 1.99   |
| HGST      | HDN726040ALE614    | 4 TB   | 15      | 833   | 19    | 1.99   |
| Seagate   | ST3250820AS Q      | 250 GB | 4       | 724   | 0     | 1.99   |
| WDC       | WD800JD-60LSA0     | 80 GB  | 15      | 1281  | 73    | 1.99   |
| Maxtor    | STM380215A         | 80 GB  | 9       | 960   | 209   | 1.98   |
| WDC       | WD400BD-60LRA0     | 40 GB  | 1       | 723   | 0     | 1.98   |
| Hitachi   | HDT721010SLA360    | 1 TB   | 64      | 1373  | 25    | 1.98   |
| WDC       | WD7501AALS-75J7B0  | 752 GB | 1       | 723   | 0     | 1.98   |
| Seagate   | ST500UM001-1EK162  | 500 GB | 1       | 723   | 0     | 1.98   |
| WDC       | WD2500AAKX-083CA1  | 250 GB | 21      | 1011  | 3     | 1.98   |
| WDC       | WD5000AAKS-65YGA0  | 500 GB | 11      | 970   | 9     | 1.98   |
| WDC       | WD15EARS-60MVWB0   | 1.5 TB | 9       | 1228  | 32    | 1.97   |
| Fujitsu   | MHV2100AH          | 100 GB | 2       | 719   | 0     | 1.97   |
| Seagate   | ST6000NM0024-1H... | 6 TB   | 6       | 1049  | 12    | 1.97   |
| WDC       | WD10EZEX-00ZF5A0   | 1 TB   | 34      | 833   | 68    | 1.97   |
| WDC       | WD40EZRZ-00WN9B0   | 4 TB   | 39      | 761   | 1     | 1.97   |
| HGST      | HCC545032A7E380    | 320 GB | 1       | 719   | 0     | 1.97   |
| WDC       | WD15EADS-00P8B0    | 1.5 TB | 24      | 1387  | 51    | 1.97   |
| WDC       | WD4000FYYZ-01UL1B2 | 4 TB   | 7       | 1125  | 456   | 1.97   |
| WDC       | WD800JD-22MSA1     | 80 GB  | 14      | 908   | 12    | 1.97   |
| Seagate   | ST3250824AS        | 250 GB | 37      | 1074  | 562   | 1.97   |
| WDC       | WD7500AADS-00M2B0  | 752 GB | 25      | 1251  | 27    | 1.97   |
| MediaMax  | WL1000GSA6454G     | 1 TB   | 2       | 717   | 0     | 1.97   |
| WDC       | WD20EARS-55MVWB0   | 2 TB   | 3       | 717   | 0     | 1.97   |
| Seagate   | ST2000DL003-9VT166 | 2 TB   | 157     | 1006  | 200   | 1.97   |
| Hitachi   | HDS721010CLA332    | 1 TB   | 207     | 1129  | 132   | 1.97   |
| Seagate   | ST3500630AS P      | 500 GB | 1       | 717   | 0     | 1.96   |
| WDC       | WD2500AAKS-00L9A0  | 250 GB | 12      | 1050  | 4     | 1.96   |
| Seagate   | ST3400832AS        | 400 GB | 4       | 2013  | 67    | 1.96   |
| WDC       | WD3000HLFS-75G6U1  | 304 GB | 4       | 907   | 1     | 1.96   |
| Hitachi   | HDS5C1032CLA382    | 320 GB | 8       | 849   | 2     | 1.96   |
| Seagate   | ST500NM0011        | 500 GB | 21      | 1428  | 48    | 1.95   |
| WDC       | WD5000BEVT-16A0RT0 | 500 GB | 1       | 713   | 0     | 1.95   |
| Seagate   | ST3250620AS        | 250 GB | 69      | 1060  | 294   | 1.95   |
| WDC       | WD800BB-00DKA0     | 80 GB  | 4       | 987   | 1     | 1.95   |
| WDC       | WD1600JS-58NCB1    | 160 GB | 1       | 712   | 0     | 1.95   |
| Maxtor    | STM3160215A        | 160 GB | 16      | 805   | 193   | 1.95   |
| WDC       | WD5000AAJS-00YFA0  | 500 GB | 10      | 879   | 26    | 1.94   |
| WDC       | WD200BB-32CFC0     | 20 GB  | 1       | 709   | 0     | 1.94   |
| WDC       | WD3200AAKS-00UU3A0 | 320 GB | 25      | 1082  | 46    | 1.94   |
| Seagate   | ST6000VX0023-2E... | 6 TB   | 5       | 721   | 4     | 1.94   |
| WDC       | WD2003FZEX-00SRLA0 | 2 TB   | 71      | 726   | 1     | 1.94   |
| WDC       | WD10EALX-229BA0    | 1 TB   | 6       | 1193  | 9     | 1.94   |
| WDC       | WD1200PD-00FZB0    | 120 GB | 1       | 706   | 0     | 1.94   |
| Toshiba   | MQ01ABD100R        | 1 TB   | 1       | 706   | 0     | 1.94   |
| WDC       | WD1003FZEX-00MK2A0 | 1 TB   | 122     | 833   | 10    | 1.94   |
| WDC       | WD4003FZEX-00Z4SA0 | 4 TB   | 32      | 1027  | 26    | 1.93   |
| WDC       | WD30EFAX-68JH4N0   | 3 TB   | 1       | 705   | 0     | 1.93   |
| Hitachi   | HDT721016SLA380    | 160 GB | 28      | 1094  | 41    | 1.93   |
| WDC       | WD800AAJS-00WAA0   | 80 GB  | 8       | 701   | 2     | 1.92   |
| WDC       | WD2500BEVS-22VAT0  | 250 GB | 1       | 700   | 0     | 1.92   |
| Seagate   | ST3160215SCE       | 160 GB | 3       | 725   | 2     | 1.92   |
| WDC       | WD5003AZEX-00S3DA0 | 500 GB | 1       | 698   | 0     | 1.91   |
| Seagate   | ST6000VN0041-2E... | 6 TB   | 8       | 917   | 28    | 1.91   |
| WDC       | WD7500AACS-00D6B1  | 752 GB | 6       | 935   | 2     | 1.91   |
| WDC       | WD3200BEKT-00PVMT0 | 320 GB | 5       | 697   | 0     | 1.91   |
| Seagate   | ST3160212A         | 160 GB | 16      | 931   | 56    | 1.91   |
| WDC       | WD2500LPVT-00G33T0 | 250 GB | 1       | 696   | 0     | 1.91   |
| WDC       | WD800JD-00LSA0     | 80 GB  | 26      | 983   | 9     | 1.90   |
| WDC       | WD4001FAEX-00MJRA0 | 4 TB   | 4       | 1126  | 507   | 1.90   |
| WDC       | WD1502FAEX-007BA0  | 1.5 TB | 11      | 804   | 17    | 1.90   |
| WDC       | WD2500BMVV-11DCLS0 | 250 GB | 1       | 694   | 0     | 1.90   |
| WDC       | WD10EURX-63FH1Y0   | 1 TB   | 13      | 894   | 1     | 1.90   |
| WDC       | WD800JD-22JNA0     | 80 GB  | 2       | 692   | 0     | 1.90   |
| WDC       | WD3200AAJS-00VWA0  | 320 GB | 14      | 746   | 33    | 1.90   |
| WDC       | WD5000BMVW-11AJGS0 | 500 GB | 1       | 692   | 0     | 1.90   |
| WDC       | WD3200BEVE-00A0HT0 | 320 GB | 3       | 691   | 0     | 1.90   |
| WDC       | WD15EZRX-00DC0B0   | 1.5 TB | 2       | 691   | 0     | 1.89   |
| WDC       | WD7500AACS-65D6B0  | 752 GB | 3       | 830   | 5     | 1.89   |
| Seagate   | ST4000VN000-2AH166 | 4 TB   | 3       | 690   | 0     | 1.89   |
| WDC       | WD5000AZLX-00K4KA0 | 500 GB | 1       | 690   | 0     | 1.89   |
| WDC       | WD2003FYYS-20W0B0  | 2 TB   | 2       | 690   | 0     | 1.89   |
| WDC       | WD10EZEX-00ER1A0   | 1 TB   | 8       | 891   | 1     | 1.89   |
| WDC       | WD10EUCX-63YZ1Y0   | 1 TB   | 2       | 688   | 0     | 1.89   |
| WDC       | WD6002FFWX-68TZ4N0 | 6 TB   | 4       | 688   | 0     | 1.89   |
| WDC       | WD3200AAJS-40VWA1  | 320 GB | 4       | 1016  | 14    | 1.89   |
| Hitachi   | HDS721612PLA380    | 120 GB | 10      | 1092  | 158   | 1.89   |
| Seagate   | ST2000DM001-1ER164 | 2 TB   | 339     | 821   | 114   | 1.88   |
| WDC       | WD4000YS-01MPB1    | 400 GB | 2       | 686   | 0     | 1.88   |
| Seagate   | ST340215AS         | 40 GB  | 1       | 686   | 0     | 1.88   |
| WDC       | WD2500JS-40TGB0    | 250 GB | 2       | 1092  | 1     | 1.88   |
| Seagate   | ST960813AS         | 64 GB  | 3       | 873   | 4     | 1.88   |
| Seagate   | ST2000DX001-1NS164 | 2 TB   | 30      | 826   | 71    | 1.88   |
| Toshiba   | HDWE150            | 5 TB   | 27      | 712   | 1     | 1.88   |
| Hitachi   | HDT725050VLA380    | 500 GB | 7       | 1581  | 8     | 1.88   |
| Hitachi   | HDS721064CLA332    | 640 GB | 4       | 742   | 1     | 1.88   |
| Fujitsu   | MHZ2080BH G2       | 80 GB  | 1       | 684   | 0     | 1.88   |
| Maxtor    | 7H500F0            | 500 GB | 6       | 743   | 1     | 1.87   |
| WDC       | WD10EARS-00MVWB0   | 1 TB   | 65      | 1385  | 77    | 1.87   |
| WDC       | WD2500AAJS-22RYA0  | 250 GB | 2       | 771   | 213   | 1.87   |
| WDC       | WD5000BEKT-22KA9T0 | 500 GB | 4       | 806   | 3     | 1.87   |
| WDC       | WD5000AAJS-22TKA0  | 500 GB | 5       | 681   | 0     | 1.87   |
| WDC       | WD6003FZBX-00GXAB0 | 6 TB   | 1       | 681   | 0     | 1.87   |
| Seagate   | ST500LM000-1EJ1... | 500 GB | 3       | 1046  | 8     | 1.87   |
| WDC       | WD1500BLHX-01V7BV0 | 150 GB | 1       | 680   | 0     | 1.86   |
| Hitachi   | HDP725025GLA380    | 250 GB | 56      | 1209  | 98    | 1.86   |
| Seagate   | ST9320325ASG       | 320 GB | 3       | 779   | 2     | 1.86   |
| WDC       | WD40EMAZ-51TKPB0   | 4 TB   | 1       | 679   | 0     | 1.86   |
| Hitachi   | HUA721010KLA330... | 1 TB   | 1       | 2715  | 3     | 1.86   |
| WDC       | WD10EZRX-00L4HB0   | 1 TB   | 92      | 741   | 3     | 1.86   |
| WDC       | WD6002FRYZ-01WD5B1 | 6 TB   | 4       | 678   | 0     | 1.86   |
| Seagate   | ST5000DM000-1FK178 | 5 TB   | 24      | 839   | 99    | 1.85   |
| WDC       | WD10SPZX-11Z10T0   | 1 TB   | 2       | 676   | 0     | 1.85   |
| WDC       | WD800BB-63JKC0     | 80 GB  | 1       | 676   | 0     | 1.85   |
| Samsung   | HD162GJ            | 160 GB | 3       | 675   | 0     | 1.85   |
| Seagate   | ST3160318AS        | 160 GB | 110     | 913   | 109   | 1.85   |
| Seagate   | ST31000521AS       | 1 TB   | 1       | 675   | 0     | 1.85   |
| WDC       | WD2002FAEX-00MJRA0 | 2 TB   | 4       | 998   | 38    | 1.85   |
| Toshiba   | MG04ACA600E        | 6 TB   | 3       | 675   | 0     | 1.85   |
| WDC       | WD800BB-75DKA0     | 80 GB  | 1       | 672   | 0     | 1.84   |
| Seagate   | ST12000VN0007-2... | 12 TB  | 14      | 819   | 153   | 1.84   |
| WDC       | WD1200JS-55MHB0    | 120 GB | 2       | 671   | 0     | 1.84   |
| Seagate   | ST3250820SCE       | 250 GB | 6       | 841   | 169   | 1.84   |
| WDC       | WD5000AAKS-40V6A0  | 500 GB | 4       | 980   | 2     | 1.84   |
| WDC       | WD5000LPVT-60G33T0 | 500 GB | 1       | 670   | 0     | 1.84   |
| WDC       | WD4000KS-00MNB0    | 400 GB | 4       | 670   | 0     | 1.84   |
| WDC       | WD5000HHTZ-75N21V0 | 500 GB | 1       | 670   | 0     | 1.84   |
| WDC       | WD3200AAKS-22B3A0  | 320 GB | 3       | 1113  | 3     | 1.83   |
| WDC       | WD2000JD-00HBB0    | 200 GB | 9       | 1583  | 3     | 1.83   |
| Seagate   | ST2000DM001-1CH164 | 2 TB   | 332     | 889   | 145   | 1.82   |
| WDC       | WD6400BPVT-35HXZT1 | 640 GB | 3       | 666   | 0     | 1.82   |
| Samsung   | HD103SI            | 1 TB   | 101     | 1170  | 275   | 1.82   |
| WDC       | WD10EZEX-22BN5A0   | 1 TB   | 49      | 736   | 1     | 1.82   |
| WDC       | WD5000BPKX-80HPJT0 | 500 GB | 1       | 665   | 0     | 1.82   |
| WDC       | WD2000JD-22HBC0    | 200 GB | 3       | 1330  | 4     | 1.82   |
| Seagate   | ST340014AS         | 40 GB  | 10      | 1183  | 366   | 1.82   |
| Seagate   | ST1000NX0423       | 1 TB   | 5       | 665   | 0     | 1.82   |
| WDC       | WD10EZRX-00A8LB0   | 1 TB   | 90      | 864   | 20    | 1.82   |
| WDC       | WD20EARS-14MVWB0   | 2 TB   | 3       | 664   | 0     | 1.82   |
| WDC       | WD5000LPVX-16V0TT0 | 500 GB | 2       | 691   | 2     | 1.82   |
| WDC       | WD30EURS-63R8UY0   | 3 TB   | 2       | 664   | 0     | 1.82   |
| HGST      | HTS541515A9E630    | 1.5 TB | 8       | 874   | 133   | 1.82   |
| Maxtor    | 2R010H1            | 10 GB  | 1       | 1326  | 1     | 1.82   |
| WDC       | WD15EARX-00PASB0   | 1.5 TB | 16      | 845   | 2     | 1.82   |
| WDC       | WD2000JB-00REA0    | 200 GB | 4       | 885   | 1     | 1.82   |
| Seagate   | ST6000DM004-2EH11C | 6 TB   | 3       | 662   | 0     | 1.82   |
| Seagate   | ST3802110AS        | 80 GB  | 6       | 839   | 528   | 1.81   |
| Seagate   | ST4000NM0053       | 4 TB   | 4       | 983   | 6     | 1.81   |
| WDC       | WD1200JD-00FYB0    | 120 GB | 1       | 661   | 0     | 1.81   |
| Seagate   | ST380815AS         | 80 GB  | 220     | 931   | 243   | 1.81   |
| WDC       | WD1600AAJS-22WAA0  | 160 GB | 9       | 915   | 2     | 1.81   |
| WDC       | WD2500AAKX-60U6AA0 | 250 GB | 12      | 923   | 60    | 1.81   |
| WDC       | WD1600AAJS-07M0A0  | 160 GB | 11      | 1054  | 2     | 1.81   |
| Seagate   | ST3400620NS        | 400 GB | 5       | 1356  | 9     | 1.81   |
| Seagate   | ST3250824SCE       | 250 GB | 2       | 658   | 0     | 1.81   |
| WDC       | WD1600AVBS-63SVA0  | 160 GB | 1       | 658   | 0     | 1.80   |
| HGST      | HUH721212ALN600    | 12 TB  | 4       | 658   | 0     | 1.80   |
| WDC       | WD2500JS-00NCB1    | 250 GB | 13      | 956   | 26    | 1.80   |
| WDC       | WD1600BEKT-66F3T2  | 160 GB | 2       | 656   | 0     | 1.80   |
| Maxtor    | STM3250820A        | 250 GB | 9       | 779   | 145   | 1.80   |
| WDC       | WD1600JS-98NCB1    | 160 GB | 1       | 655   | 0     | 1.80   |
| WDC       | WD10EZEX-00UD2A0   | 1 TB   | 16      | 712   | 55    | 1.79   |
| WDC       | WD5000AAKS-07V0A0  | 500 GB | 1       | 654   | 0     | 1.79   |
| WDC       | WD10EADS-11M2B2    | 1 TB   | 14      | 1064  | 76    | 1.79   |
| Seagate   | ST3160812AS        | 160 GB | 70      | 1014  | 354   | 1.79   |
| WDC       | WD5000AAKS-00Z7B0  | 500 GB | 1       | 652   | 0     | 1.79   |
| WDC       | WD40PURX-64NZ6Y0   | 4 TB   | 5       | 651   | 0     | 1.79   |
| WDC       | WD5000BPKT-22PK4T0 | 500 GB | 4       | 651   | 0     | 1.78   |
| WDC       | WD400BD-60JPA0     | 40 GB  | 1       | 651   | 0     | 1.78   |
| WDC       | WD2500AAKX-753CA1  | 250 GB | 35      | 920   | 32    | 1.78   |
| Seagate   | ST1000NM0033-9Z... | 1 TB   | 49      | 890   | 125   | 1.78   |
| Seagate   | ST640LM000 HM641JI | 640 GB | 8       | 650   | 0     | 1.78   |
| Toshiba   | MK1265GSX H        | 120 GB | 1       | 649   | 0     | 1.78   |
| WDC       | WD10JPVT-24A1YT0   | 1 TB   | 7       | 833   | 1     | 1.78   |
| WDC       | WD1200BEVT-75ZCT2  | 120 GB | 1       | 649   | 0     | 1.78   |
| Hitachi   | HDT721032SLA360    | 320 GB | 33      | 1134  | 12    | 1.78   |
| Seagate   | ST1000VX008-2MX10C | 1 TB   | 1       | 647   | 0     | 1.77   |
| WDC       | WD3200AAJS-65RYA0  | 320 GB | 3       | 647   | 0     | 1.77   |
| Seagate   | ST980812AS         | 80 GB  | 1       | 647   | 0     | 1.77   |
| WDC       | WD5000AAJS-00A8B0  | 500 GB | 5       | 816   | 2     | 1.77   |
| WDC       | WD10EZRX-00DC0B0   | 1 TB   | 8       | 698   | 2     | 1.77   |
| Hitachi   | HDS5C4040ALE630    | 4 TB   | 6       | 646   | 0     | 1.77   |
| Toshiba   | DT01ACA200         | 2 TB   | 316     | 696   | 38    | 1.77   |
| WDC       | WD3200BEVS-08VAT2  | 320 GB | 7       | 757   | 160   | 1.77   |
| Seagate   | ST1000DM003-1ER162 | 1 TB   | 465     | 703   | 65    | 1.77   |
| WDC       | WD6400BPVT-55HXZT3 | 640 GB | 3       | 820   | 3     | 1.76   |
| WDC       | WD6400AAKS-65A7B0  | 640 GB | 18      | 1364  | 77    | 1.76   |
| Seagate   | ST1000NM0011       | 1 TB   | 27      | 1431  | 23    | 1.76   |
| Seagate   | ST10000DM0004      | 10 TB  | 2       | 641   | 0     | 1.76   |
| WDC       | WD1001FALS-19J7B0  | 1 TB   | 1       | 641   | 0     | 1.76   |
| Samsung   | HD502IJ            | 500 GB | 76      | 1110  | 168   | 1.76   |
| WDC       | WD7500AZEX-00RKKA0 | 752 GB | 8       | 640   | 0     | 1.76   |
| WDC       | WD10EZEX-08M2NA0   | 1 TB   | 159     | 746   | 9     | 1.76   |
| WDC       | WD7502AAEX-00Y9A0  | 752 GB | 6       | 640   | 0     | 1.75   |
| WDC       | WD3200BPVT-75JJ5T0 | 320 GB | 8       | 666   | 1     | 1.75   |
| WDC       | WD1004FBYZ-01YCBB1 | 1 TB   | 5       | 637   | 0     | 1.75   |
| WDC       | WD3200AAKS-00VYA0  | 320 GB | 12      | 683   | 30    | 1.75   |
| WDC       | WD10EADX-22TDHB0   | 1 TB   | 22      | 1032  | 54    | 1.74   |
| Seagate   | ST3160815AS        | 160 GB | 271     | 911   | 315   | 1.74   |
| WDC       | WD5000AAKX-603CA0  | 500 GB | 32      | 926   | 240   | 1.74   |
| Samsung   | HD103UJ            | 1 TB   | 131     | 1315  | 257   | 1.74   |
| Seagate   | ST12000NM0008-2... | 12 TB  | 12      | 699   | 2     | 1.74   |
| Fujitsu   | MHZ2250BJ FFS G2   | 250 GB | 4       | 781   | 24    | 1.74   |
| WDC       | WD800BD-22LRA0     | 80 GB  | 2       | 634   | 0     | 1.74   |
| WDC       | WD1002FBYS-43P1B0  | 1 TB   | 2       | 1021  | 39    | 1.74   |
| WDC       | WD1200JS-00MHB0    | 120 GB | 17      | 664   | 1     | 1.74   |
| Hitachi   | HDS721025CLA382    | 250 GB | 40      | 850   | 181   | 1.74   |
| WDC       | WD5003ABYX-01WERA0 | 500 GB | 14      | 1049  | 4     | 1.74   |
| WDC       | WD5003AZEX-00K1GA0 | 500 GB | 35      | 662   | 31    | 1.74   |
| WDC       | WD5000AAKS-75A7B2  | 500 GB | 5       | 1090  | 5     | 1.74   |
| WDC       | WD1600BEVT-11ZCT0  | 160 GB | 1       | 633   | 0     | 1.74   |
| Toshiba   | HDWA120            | 2 TB   | 9       | 780   | 3     | 1.74   |
| WDC       | WD10EADS-11M2B3    | 1 TB   | 4       | 633   | 0     | 1.73   |
| WDC       | WD5000AAKX-07U6AA0 | 500 GB | 14      | 764   | 2     | 1.73   |
| Seagate   | ST1000DL002-9TT153 | 1 TB   | 66      | 1080  | 276   | 1.73   |
| Hitachi   | HTS723220L9A360    | 200 GB | 1       | 630   | 0     | 1.73   |
| Toshiba   | MK5055GSXN         | 500 GB | 3       | 748   | 3     | 1.73   |
| WDC       | WD1600AAJS-07PSA0  | 160 GB | 5       | 1139  | 5     | 1.72   |
| WDC       | WD3001FFSX-68JNUN0 | 3 TB   | 2       | 628   | 0     | 1.72   |
| WDC       | WD50EZRX-00MVLB1   | 5 TB   | 7       | 809   | 2     | 1.72   |
| Seagate   | ST5000NM0024-1H... | 5 TB   | 5       | 1990  | 149   | 1.72   |
| WDC       | WD3200AAJS-00G0A0  | 320 GB | 1       | 628   | 0     | 1.72   |
| WDC       | WD7500BPKX-60HPJT0 | 752 GB | 1       | 627   | 0     | 1.72   |
| WDC       | WD4000BEVT-11ZAT0  | 400 GB | 1       | 626   | 0     | 1.72   |
| WDC       | WD20EURS-73S48Y0   | 2 TB   | 1       | 626   | 0     | 1.72   |
| HGST      | HDS724020ALE640    | 2 TB   | 2       | 626   | 0     | 1.72   |
| Hitachi   | HDS5C1050CLA382    | 500 GB | 21      | 951   | 162   | 1.71   |
| WDC       | WD15EADS-00R6B0    | 1.5 TB | 1       | 625   | 0     | 1.71   |
| Hitachi   | HDP725032GLA360    | 320 GB | 27      | 949   | 60    | 1.71   |
| WDC       | WD3200AUDX-56WNHY0 | 320 GB | 5       | 624   | 0     | 1.71   |
| WDC       | WD360GD-00FLC0     | 37 GB  | 1       | 622   | 0     | 1.70   |
| WDC       | WD400BD-23JMC0     | 40 GB  | 1       | 1866  | 2     | 1.70   |
| WDC       | WD3200BEKX-66B7WT0 | 320 GB | 1       | 622   | 0     | 1.70   |
| Hitachi   | HDS721010KLA330    | 1 TB   | 17      | 987   | 12    | 1.70   |
| Hitachi   | HDP725050GLA360    | 500 GB | 137     | 1226  | 75    | 1.70   |
| Apple     | HDD HTS541010A9... | 1 TB   | 54      | 877   | 101   | 1.70   |
| WDC       | WD1600AAJS-55PSA0  | 160 GB | 1       | 620   | 0     | 1.70   |
| WDC       | WD10EZEX-00BN5A0   | 1 TB   | 293     | 714   | 18    | 1.70   |
| Toshiba   | MK1229GSG          | 120 GB | 1       | 619   | 0     | 1.70   |
| WDC       | WD10EFRX-68FYTN0   | 1 TB   | 63      | 688   | 1     | 1.70   |
| WDC       | WD6400AAKS-00A7B2  | 640 GB | 11      | 722   | 2     | 1.69   |
| WDC       | WD2500BEVS-26VAT0  | 250 GB | 3       | 617   | 0     | 1.69   |
| WDC       | WD1500HLFS-01MZUV0 | 150 GB | 3       | 894   | 1     | 1.69   |
| WDC       | WD4000FYYZ-01UL1B3 | 4 TB   | 2       | 1532  | 3     | 1.69   |
| WDC       | WD20NMVW-11EDZS6   | 2 TB   | 30      | 647   | 1     | 1.69   |
| WDC       | WD1600AAJB-00WRA0  | 160 GB | 4       | 778   | 272   | 1.69   |
| WDC       | WD5000AACS-00G8B1  | 500 GB | 19      | 1007  | 56    | 1.69   |
| Seagate   | ST9500620NS        | 500 GB | 4       | 1211  | 7     | 1.69   |
| Seagate   | ST2000VX000-1CU164 | 2 TB   | 23      | 1034  | 195   | 1.69   |
| WDC       | WD4000F9YZ-09N20L0 | 4 TB   | 2       | 616   | 0     | 1.69   |
| WDC       | WD3200BEKX-60B7WT0 | 320 GB | 3       | 614   | 0     | 1.68   |
| Seagate   | ST3000VN000-1H4167 | 3 TB   | 5       | 614   | 0     | 1.68   |
| Hitachi   | HCS5C1032CLA382    | 320 GB | 2       | 883   | 2     | 1.68   |
| Seagate   | ST3200820AS        | 200 GB | 31      | 976   | 480   | 1.68   |
| WDC       | WD1600AAJS-00Z4A0  | 160 GB | 3       | 1076  | 1     | 1.68   |
| WDC       | WD10EALX-009BA0    | 1 TB   | 108     | 951   | 26    | 1.68   |
| Samsung   | HD154UI            | 1.5 TB | 80      | 1050  | 275   | 1.67   |
| WDC       | WD20NMVW-11AV3S0   | 2 TB   | 9       | 829   | 17    | 1.67   |
| HGST      | HUS724030ALA640... | 3 TB   | 2       | 610   | 0     | 1.67   |
| WDC       | WD10JPVX-08JC3T5   | 1 TB   | 20      | 717   | 4     | 1.67   |
| WDC       | WD6400BPVT-24HXZT1 | 640 GB | 3       | 961   | 340   | 1.67   |
| WDC       | WD800JD-00LUA0     | 80 GB  | 1       | 610   | 0     | 1.67   |
| WDC       | WD10EURX-73C57Y0   | 1 TB   | 6       | 609   | 0     | 1.67   |
| HP        | MB1000GDUNU        | 1 TB   | 1       | 609   | 0     | 1.67   |
| WDC       | WD10EARS-22Y5B1    | 1 TB   | 41      | 1098  | 58    | 1.67   |
| Seagate   | ST31000526SV       | 1 TB   | 3       | 769   | 343   | 1.67   |
| WDC       | WD2500AAKS-00VSA0  | 250 GB | 30      | 825   | 14    | 1.67   |
| WDC       | WD3200AAKS-00B3A0  | 320 GB | 46      | 868   | 25    | 1.66   |
| Seagate   | ST340014A          | 40 GB  | 102     | 834   | 30    | 1.66   |
| Samsung   | HD502HJ            | 500 GB | 192     | 844   | 51    | 1.66   |
| Seagate   | ST3250312AS        | 250 GB | 62      | 777   | 68    | 1.66   |
| Seagate   | ST4000LM016-1N2170 | 4 TB   | 15      | 604   | 0     | 1.66   |
| WDC       | WD20EZRX-60D8PB0   | 2 TB   | 2       | 604   | 0     | 1.66   |
| WDC       | WD60EFRX-68L0BN1   | 6 TB   | 38      | 875   | 111   | 1.66   |
| WDC       | WD3200BEVT-00ZCT0  | 320 GB | 9       | 848   | 56    | 1.65   |
| WDC       | WD3000JS-60PDB0    | 304 GB | 2       | 603   | 0     | 1.65   |
| WDC       | WD2500AAJS-60B4A0  | 250 GB | 2       | 603   | 0     | 1.65   |
| WDC       | WD2500BEVS-26UST0  | 250 GB | 6       | 603   | 0     | 1.65   |
| WDC       | WD2500LPLX-00ZNTT0 | 250 GB | 1       | 603   | 0     | 1.65   |
| WDC       | WD10JFCX-68N6GN0   | 1 TB   | 31      | 650   | 1     | 1.65   |
| WDC       | WD1001FAES-22W7A0  | 1 TB   | 2       | 603   | 0     | 1.65   |
| WDC       | WD60EFRX-68MYMN1   | 6 TB   | 19      | 959   | 37    | 1.65   |
| Seagate   | ST3000DM008-2DM166 | 3 TB   | 86      | 684   | 62    | 1.65   |
| WDC       | WD7500BFCX-68N6GN0 | 752 GB | 2       | 905   | 8     | 1.65   |
| WDC       | WD1600BEVS-26VAT0  | 160 GB | 4       | 601   | 0     | 1.65   |
| WDC       | WD5000AZRX-00A8LB0 | 500 GB | 111     | 659   | 11    | 1.65   |
| Seagate   | ST3808110AS        | 80 GB  | 53      | 1034  | 330   | 1.65   |
| Hitachi   | HDS723020ALA640    | 2 TB   | 2       | 600   | 0     | 1.65   |
| WDC       | WD10EADS-65P6B0    | 1 TB   | 3       | 2363  | 5     | 1.64   |
| WDC       | WD2500AAKS-00L6A0  | 250 GB | 4       | 911   | 3     | 1.64   |
| WDC       | WD1600AAJS-62WAA0  | 160 GB | 1       | 597   | 0     | 1.64   |
| Toshiba   | DT01ABA100V        | 1 TB   | 14      | 870   | 135   | 1.64   |
| Hitachi   | HDS721616PLAT80    | 160 GB | 7       | 1042  | 18    | 1.64   |
| WDC       | WD10EZEX-00RKKA0   | 1 TB   | 138     | 833   | 78    | 1.64   |
| Seagate   | ST2000DM001-1E6164 | 2 TB   | 14      | 808   | 82    | 1.64   |
| WDC       | WD10EADS-65L5B1    | 1 TB   | 24      | 1118  | 16    | 1.63   |
| WDC       | WD10EURX-56FH1Y0   | 1 TB   | 2       | 596   | 0     | 1.63   |
| WDC       | WD5000LMVW-11CKRS0 | 500 GB | 4       | 595   | 0     | 1.63   |
| Seagate   | ST9640423AS        | 640 GB | 7       | 1037  | 218   | 1.63   |
| WDC       | WD6402AAEX-00Z3A0  | 640 GB | 6       | 594   | 0     | 1.63   |
| Seagate   | ST3000VX010-2E3166 | 3 TB   | 7       | 612   | 1     | 1.63   |
| Seagate   | ST2000DX001-1CM164 | 2 TB   | 40      | 779   | 94    | 1.63   |
| Apple     | HDD WDC WD10EAL... | 1 TB   | 1       | 594   | 0     | 1.63   |
| WDC       | WD5000AAKX-753CA1  | 500 GB | 23      | 1145  | 19    | 1.63   |
| WDC       | WD100EMAZ-00WJTA0  | 10 TB  | 50      | 593   | 0     | 1.63   |
| WDC       | WD6402AAEX-00Y9A0  | 640 GB | 8       | 799   | 6     | 1.63   |
| HP        | GB0250C8045        | 250 GB | 3       | 1283  | 67    | 1.63   |
| WDC       | WD5000AAKS-75V0A0  | 500 GB | 18      | 1186  | 4     | 1.63   |
| Hitachi   | HCC545016B9A300    | 160 GB | 1       | 593   | 0     | 1.63   |
| WDC       | WD2000JS-22NCB1    | 200 GB | 2       | 1533  | 24    | 1.62   |
| WDC       | WD800JD-00MSA1     | 80 GB  | 16      | 808   | 16    | 1.62   |
| Seagate   | ST1000DM005 HD1... | 1 TB   | 21      | 669   | 1     | 1.62   |
| WDC       | WD1600AAJS-60M0A0  | 160 GB | 5       | 647   | 19    | 1.62   |
| WDC       | WD1600BEKT-75A25T0 | 160 GB | 2       | 590   | 0     | 1.62   |
| WDC       | WD15EARS-19MVWB0   | 1.5 TB | 2       | 938   | 653   | 1.62   |
| Seagate   | ST4000NE0025-2E... | 4 TB   | 5       | 590   | 0     | 1.62   |
| WDC       | WD1600AAJB-56WRA0  | 160 GB | 2       | 590   | 0     | 1.62   |
| WDC       | WD5000BPVT-75HXZT1 | 500 GB | 2       | 589   | 0     | 1.62   |
| WDC       | WD2500BEAS-00URT0  | 250 GB | 1       | 1768  | 2     | 1.61   |
| Hitachi   | HDS721050CLA362    | 500 GB | 215     | 836   | 63    | 1.61   |
| WDC       | WD2000JS-00MHB0    | 200 GB | 9       | 782   | 54    | 1.61   |
| WDC       | WD2002FYPS-02W3B0  | 2 TB   | 10      | 1183  | 4     | 1.61   |
| Samsung   | HD153WI            | 1.5 TB | 2       | 588   | 0     | 1.61   |
| WDC       | WD800JD-19LSA0     | 80 GB  | 1       | 588   | 0     | 1.61   |
| WDC       | WD3200AAJS-07M0A0  | 320 GB | 6       | 747   | 11    | 1.61   |
| WDC       | WD400BD-75MRA3     | 40 GB  | 2       | 587   | 0     | 1.61   |
| WDC       | WD20EARS-00S8B1    | 2 TB   | 16      | 1066  | 34    | 1.61   |
| WDC       | WD800BEVS-08RST2   | 80 GB  | 5       | 585   | 0     | 1.60   |
| WDC       | WD3200BUDT-63DPZY0 | 320 GB | 4       | 960   | 6     | 1.60   |
| Seagate   | ST3120026AS        | 120 GB | 36      | 1203  | 60    | 1.60   |
| WDC       | WD2500AAJS-60M0A1  | 250 GB | 3       | 585   | 0     | 1.60   |
| WDC       | WD5003ABYX-01WERA1 | 500 GB | 14      | 1094  | 6     | 1.60   |
| WDC       | WD400BB-60JKA0     | 40 GB  | 4       | 785   | 21    | 1.60   |
| WDC       | WD5000LPVT-75G33T0 | 500 GB | 9       | 686   | 18    | 1.60   |
| WDC       | WD10S21X-24R1BT... | 1 TB   | 11      | 583   | 0     | 1.60   |
| Seagate   | ST3500514NS        | 500 GB | 13      | 1355  | 73    | 1.60   |
| Toshiba   | MQ01ABF050H        | 500 GB | 3       | 730   | 42    | 1.60   |
| WDC       | WD5000AZRX-00L4HB0 | 500 GB | 41      | 610   | 1     | 1.60   |
| WDC       | WD800JD-75MSA2     | 80 GB  | 3       | 582   | 0     | 1.60   |
| WDC       | WD1602ABJS-43P5A0  | 160 GB | 1       | 582   | 0     | 1.60   |
| WDC       | WD5001AALS-00J7B1  | 500 GB | 3       | 964   | 4     | 1.60   |
| WDC       | WD3200AAJS-40RYA0  | 320 GB | 3       | 933   | 260   | 1.59   |
| Seagate   | ST2000VX000-1ES164 | 2 TB   | 12      | 622   | 1     | 1.59   |
| Seagate   | ST1000DM003-1SB10C | 1 TB   | 126     | 618   | 29    | 1.59   |
| Seagate   | ST33000650NS       | 3 TB   | 6       | 621   | 18    | 1.59   |
| WDC       | WD10EZEX-21M2NA0   | 1 TB   | 69      | 653   | 22    | 1.59   |
| WDC       | WD800LB-07DNA2     | 80 GB  | 1       | 579   | 0     | 1.59   |
| Seagate   | ST3360320AS        | 360 GB | 18      | 1092  | 79    | 1.59   |
| WDC       | WD2000FYYZ-01UL1B1 | 2 TB   | 15      | 1188  | 129   | 1.59   |
| WDC       | WD10EZRX-00D8PB0   | 1 TB   | 34      | 620   | 20    | 1.59   |
| WDC       | WD2500AAJS-07M0A0  | 250 GB | 6       | 942   | 5     | 1.59   |
| WDC       | WD1600BB-55RDA0    | 160 GB | 3       | 682   | 2     | 1.58   |
| Samsung   | HD105SI            | 1 TB   | 22      | 802   | 180   | 1.58   |
| Seagate   | ST3000DM001-1CH166 | 3 TB   | 96      | 797   | 303   | 1.58   |
| WDC       | WD6400AAKS-65Z7B0  | 640 GB | 11      | 1052  | 5     | 1.58   |
| Seagate   | ST1000DM003-1CH162 | 1 TB   | 577     | 732   | 86    | 1.58   |
| WDC       | WD10EZEX-19M2NA0   | 1 TB   | 1       | 576   | 0     | 1.58   |
| Seagate   | ST3320311CS        | 320 GB | 15      | 733   | 75    | 1.58   |
| Hitachi   | HDS728080PLA380    | 80 GB  | 63      | 870   | 40    | 1.58   |
| Seagate   | ST6000NE0023-2E... | 6 TB   | 2       | 574   | 0     | 1.57   |
| Seagate   | ST3000VX000-9YW166 | 3 TB   | 5       | 730   | 5     | 1.57   |
| WDC       | WD10TPVT-00HT5T0   | 1 TB   | 2       | 573   | 0     | 1.57   |
| Seagate   | ST2000NM0011       | 2 TB   | 6       | 1296  | 11    | 1.57   |
| Hitachi   | HCS725032VLA380    | 320 GB | 1       | 573   | 0     | 1.57   |
| WDC       | WD4000FYYZ-01UL1B1 | 4 TB   | 12      | 1219  | 9     | 1.57   |
| WDC       | WD3200AAKS-00L9A0  | 320 GB | 71      | 996   | 22    | 1.57   |
| Seagate   | ST32000541AS       | 2 TB   | 1       | 572   | 0     | 1.57   |
| Maxtor    | 6V160E0            | 160 GB | 18      | 670   | 2     | 1.57   |
| WDC       | WD30NMRW-11YL9S4   | 3 TB   | 3       | 571   | 0     | 1.57   |
| WDC       | WD10EURX-63UY4Y0   | 1 TB   | 12      | 705   | 2     | 1.56   |
| Toshiba   | MG06ACA10TEY       | 10 TB  | 4       | 570   | 0     | 1.56   |
| Seagate   | ST3160316AS        | 160 GB | 14      | 675   | 6     | 1.56   |
| WDC       | WD2500JS-00SGB0    | 250 GB | 6       | 691   | 1     | 1.56   |
| Hitachi   | HDS721032CLA362    | 320 GB | 71      | 876   | 32    | 1.56   |
| WDC       | WD30EZRZ-00WN9B0   | 3 TB   | 13      | 612   | 1     | 1.56   |
| Seagate   | ST3320418AS        | 320 GB | 132     | 963   | 148   | 1.55   |
| WDC       | WD1600BEVS-08VAT2  | 160 GB | 12      | 707   | 1     | 1.55   |
| Seagate   | ST3160212SCE       | 160 GB | 3       | 1562  | 793   | 1.55   |
| Samsung   | HD503HI            | 500 GB | 31      | 818   | 9     | 1.55   |
| Seagate   | ST1000NX0443       | 1 TB   | 2       | 566   | 0     | 1.55   |
| Hitachi   | HDS721050CLA660    | 500 GB | 45      | 800   | 117   | 1.55   |
| WDC       | WD400EB-75CPF0     | 40 GB  | 1       | 564   | 0     | 1.55   |
| Seagate   | ST3320820AS_Q      | 320 GB | 2       | 1793  | 1068  | 1.54   |
| WDC       | WD1600AABS-52PRA0  | 160 GB | 1       | 562   | 0     | 1.54   |
| Seagate   | ST380011A          | 80 GB  | 202     | 847   | 68    | 1.54   |
| Seagate   | ST16000NM003G-2... | 16 TB  | 1       | 560   | 0     | 1.54   |
| WDC       | WD5000AAKS-22A7B0  | 500 GB | 23      | 1142  | 53    | 1.54   |
| WDC       | WD2500AAKX-75U6AA0 | 250 GB | 22      | 766   | 3     | 1.53   |
| Seagate   | ST3500413AS        | 500 GB | 260     | 799   | 97    | 1.53   |
| WDC       | WD30PURX-64P6ZY0   | 3 TB   | 15      | 1071  | 68    | 1.53   |
| Seagate   | ST1000VX000-1CU162 | 1 TB   | 32      | 570   | 32    | 1.53   |
| Hitachi   | HDT725050VLA360    | 500 GB | 11      | 873   | 20    | 1.53   |
| WDC       | WD2500JS-58NCB1    | 250 GB | 3       | 858   | 205   | 1.53   |
| WDC       | WD2500JB-98GVA0    | 250 GB | 1       | 3354  | 5     | 1.53   |
| WDC       | WD2500AAJB-00WGA0  | 250 GB | 5       | 1069  | 115   | 1.53   |
| Seagate   | ST3250823A         | 250 GB | 6       | 977   | 440   | 1.53   |
| WDC       | WD6400AAKS-75A7B0  | 640 GB | 4       | 940   | 2     | 1.53   |
| WDC       | WD4004FZWX-00GBGB0 | 4 TB   | 9       | 721   | 265   | 1.53   |
| Samsung   | HD160JJ-P          | 160 GB | 15      | 1050  | 408   | 1.53   |
| Samsung   | HD040GJ            | 40 GB  | 7       | 896   | 163   | 1.53   |
| WDC       | WD3200AAJS-65VWA0  | 320 GB | 4       | 673   | 1     | 1.53   |
| WDC       | WD7500BPVT-24HXZT1 | 752 GB | 14      | 803   | 75    | 1.53   |
| WDC       | WD3200BEVT-75ZCT1  | 320 GB | 1       | 2230  | 3     | 1.53   |
| HGST      | HUH721010ALE600    | 10 TB  | 20      | 575   | 1     | 1.53   |
| WDC       | WD1600BEVS-75RST0  | 160 GB | 4       | 557   | 0     | 1.53   |
| WDC       | WD20NMVW-11AV3S2   | 2 TB   | 57      | 731   | 17    | 1.53   |
| WDC       | WD5000AUDX-63WNHY0 | 500 GB | 6       | 555   | 0     | 1.52   |
| WDC       | WD30EFRX-68N32N0   | 3 TB   | 15      | 572   | 1     | 1.52   |
| Toshiba   | MK6032GSX          | 64 GB  | 1       | 555   | 0     | 1.52   |
| WDC       | WD3000JS-00PDB0    | 304 GB | 1       | 554   | 0     | 1.52   |
| WDC       | WD800AAJS-75M0A0   | 80 GB  | 7       | 1095  | 6     | 1.52   |
| WDC       | WD10EADS-11M2B1    | 1 TB   | 7       | 911   | 13    | 1.52   |
| Hitachi   | HUA722010CLA330    | 1 TB   | 30      | 1000  | 165   | 1.52   |
| WDC       | WD800JD-55JRC0     | 80 GB  | 2       | 672   | 31    | 1.51   |
| WDC       | WD1600AAJS-75M0A0  | 160 GB | 23      | 1002  | 50    | 1.51   |
| WDC       | WD1600JS-23MHB0    | 160 GB | 2       | 552   | 0     | 1.51   |
| Seagate   | ST3000VX010-2H916L | 3 TB   | 4       | 552   | 0     | 1.51   |
| WDC       | WD400BB-00JHA0     | 40 GB  | 4       | 1037  | 3     | 1.51   |
| Seagate   | ST980813AS         | 80 GB  | 5       | 656   | 1     | 1.51   |
| Seagate   | ST3300620AS        | 304 GB | 2       | 550   | 0     | 1.51   |
| Seagate   | ST2000NM0008-2F... | 2 TB   | 4       | 550   | 0     | 1.51   |
| Hitachi   | HTS723216L9SA60    | 160 GB | 12      | 759   | 6     | 1.51   |
| Seagate   | ST3250820AS        | 250 GB | 81      | 898   | 280   | 1.51   |
| WDC       | WD3200BPVT-00HXZT0 | 320 GB | 1       | 549   | 0     | 1.51   |
| WDC       | WD7500AARX-00N0YB0 | 752 GB | 2       | 1312  | 42    | 1.51   |
| WDC       | WD5000AAKS-00V0A0  | 500 GB | 6       | 674   | 340   | 1.50   |
| WDC       | WD1600JS-00SGB0    | 160 GB | 1       | 549   | 0     | 1.50   |
| WDC       | WD2500AAKS-00YGA0  | 250 GB | 2       | 548   | 0     | 1.50   |
| Seagate   | ST360015A          | 64 GB  | 2       | 1494  | 5     | 1.50   |
| WDC       | WD2500AAKX-073CA1  | 250 GB | 1       | 547   | 0     | 1.50   |
| Maxtor    | STM380215AS        | 80 GB  | 14      | 727   | 419   | 1.50   |
| Apple     | HDD ST1000DM003    | 1 TB   | 32      | 545   | 0     | 1.50   |
| WDC       | WD2500AAJS-75B4A0  | 250 GB | 5       | 716   | 4     | 1.50   |
| WDC       | WD100EFAX-68LHPN0  | 10 TB  | 19      | 545   | 0     | 1.49   |
| Hitachi   | HDS721010CLA330    | 1 TB   | 53      | 861   | 42    | 1.49   |
| Seagate   | ST3200827A         | 200 GB | 1       | 544   | 0     | 1.49   |
| WDC       | WD20NMVW-11EDZS2   | 2 TB   | 15      | 544   | 0     | 1.49   |
| Hitachi   | HDS721616PLA320    | 160 GB | 6       | 961   | 4     | 1.49   |
| MediaMax  | WL1000GSA6472C     | 1 TB   | 1       | 543   | 0     | 1.49   |
| WDC       | WD6400AARS-00Y5B1  | 640 GB | 18      | 901   | 10    | 1.49   |
| Hitachi   | HDT725025VLAT80    | 250 GB | 2       | 1843  | 2     | 1.49   |
| WDC       | WD1005FBYZ-01YCBB2 | 1 TB   | 8       | 542   | 0     | 1.49   |
| WDC       | WD40PURX-64GVNY0   | 4 TB   | 7       | 906   | 3     | 1.49   |
| Fujitsu   | MHV2080BH          | 80 GB  | 7       | 590   | 1     | 1.48   |
| WDC       | WD1200JS-00MHB1    | 120 GB | 3       | 685   | 8     | 1.48   |
| WDC       | WD5000AVJS-63TRA0  | 500 GB | 2       | 1544  | 289   | 1.48   |
| WDC       | WD2500AAKX-603CA0  | 250 GB | 19      | 843   | 118   | 1.48   |
| Seagate   | ST3000NM0005-1V... | 3 TB   | 4       | 1190  | 15    | 1.48   |
| Seagate   | ST1000VT000 HN-... | 1 TB   | 1       | 539   | 0     | 1.48   |
| Seagate   | OOS14000G          | 14 TB  | 2       | 538   | 0     | 1.48   |
| Magnet... | MD03200-NVDW-RO    | 320 GB | 1       | 538   | 0     | 1.47   |
| WDC       | WD3200BPVT-26JJ5T0 | 320 GB | 1       | 538   | 0     | 1.47   |
| WDC       | WD1000DHTZ-04N21V0 | 1 TB   | 7       | 945   | 14    | 1.47   |
| WDC       | WD1600AAJS-61M0A0  | 160 GB | 2       | 535   | 0     | 1.47   |
| WDC       | WD6400AACS-00M3B0  | 640 GB | 2       | 535   | 0     | 1.47   |
| WDC       | WD6400AAKS-07A7B0  | 640 GB | 5       | 957   | 25    | 1.47   |
| Seagate   | ST1000DX001-1NS... | 1 TB   | 5       | 535   | 0     | 1.47   |
| WDC       | WD10JUCT-63CYNY0   | 1 TB   | 14      | 654   | 1     | 1.46   |
| WDC       | WD800AAJS-22L7A0   | 80 GB  | 1       | 534   | 0     | 1.46   |
| WDC       | WD7500BPVX-75JC3T0 | 752 GB | 6       | 742   | 2     | 1.46   |
| WDC       | WD3200AAKX-083CA0  | 320 GB | 1       | 533   | 0     | 1.46   |
| WDC       | WD1001FAES-55W7A0  | 1 TB   | 4       | 533   | 0     | 1.46   |
| Toshiba   | MK3259GSX          | 320 GB | 2       | 628   | 41    | 1.46   |
| WDC       | WD10TMVW-11ZSMS0   | 1 TB   | 1       | 533   | 0     | 1.46   |
| WDC       | WD3200AAJS-56B4A0  | 320 GB | 11      | 1066  | 6     | 1.46   |
| WDC       | WD20NMVW-11EDZS7   | 2 TB   | 21      | 609   | 59    | 1.46   |
| Maxtor    | 6V200E0            | 208 GB | 11      | 970   | 96    | 1.46   |
| WDC       | WD800JB-00ETA0     | 80 GB  | 6       | 1299  | 337   | 1.46   |
| WDC       | WD15EARS-00MVWB0   | 1.5 TB | 61      | 1015  | 220   | 1.46   |
| WDC       | WD10EZEX-60M2NA0   | 1 TB   | 47      | 696   | 101   | 1.46   |
| WDC       | WD20EARS-22MVWB0   | 2 TB   | 6       | 1870  | 175   | 1.46   |
| WDC       | WD1600AAJS-08PSA0  | 160 GB | 18      | 723   | 8     | 1.45   |
| WDC       | WD20EZRX-22D8PB0   | 2 TB   | 13      | 626   | 78    | 1.45   |
| Seagate   | ST360021A          | 64 GB  | 5       | 598   | 10    | 1.45   |
| Seagate   | ST2000DM002-1BJ164 | 2 TB   | 1       | 529   | 0     | 1.45   |
| WDC       | WD15EADS-00S2B0    | 1.5 TB | 6       | 1306  | 8     | 1.45   |
| Hitachi   | HTS722012K9A300    | 120 GB | 4       | 839   | 68    | 1.45   |
| Seagate   | ST3200827AS        | 200 GB | 32      | 909   | 285   | 1.45   |
| Seagate   | ST2000VX003-1HH164 | 2 TB   | 6       | 529   | 0     | 1.45   |
| Seagate   | ST10000NE0004-1... | 10 TB  | 11      | 1003  | 11    | 1.45   |
| Samsung   | HD252HJ            | 250 GB | 50      | 936   | 132   | 1.45   |
| WDC       | WD40EFRX-68N32N0   | 4 TB   | 203     | 591   | 1     | 1.45   |
| Samsung   | HD642JJ            | 640 GB | 48      | 1340  | 353   | 1.44   |
| WDC       | WD5000BEVT-80A0RT0 | 500 GB | 4       | 961   | 5     | 1.44   |
| WDC       | WD10EARX-32N0YB0   | 1 TB   | 8       | 682   | 61    | 1.44   |
| Seagate   | ST14000VN0008-2... | 14 TB  | 2       | 525   | 0     | 1.44   |
| WDC       | WD5000BPKX-75HPJT0 | 500 GB | 4       | 537   | 2     | 1.44   |
| WDC       | WD10EURS-630AB1    | 1 TB   | 2       | 2135  | 4     | 1.44   |
| WDC       | WD7500BPVT-00HXZT1 | 752 GB | 1       | 525   | 0     | 1.44   |
| Seagate   | ST1000LM044 HN-... | 1 TB   | 4       | 619   | 202   | 1.44   |
| WDC       | WD20SPZX-11UA7T0   | 2 TB   | 2       | 525   | 0     | 1.44   |
| WDC       | WD5000LUCT-63C26Y0 | 500 GB | 4       | 748   | 1     | 1.44   |
| WDC       | WD800BB-22JHA0     | 80 GB  | 4       | 1152  | 197   | 1.44   |
| WDC       | WD5000BPVT-24HXZT1 | 500 GB | 2       | 1262  | 4     | 1.44   |
| Seagate   | ST250LT021-1AF14C  | 250 GB | 2       | 1034  | 585   | 1.44   |
| WDC       | WD800BB-55HEA0     | 80 GB  | 1       | 523   | 0     | 1.44   |
| WDC       | WD15EARS-00S0XB0   | 1.5 TB | 5       | 1302  | 4     | 1.43   |
| HGST      | HUS726040ALE610    | 4 TB   | 4       | 694   | 1     | 1.43   |
| Maxtor    | 2F030J1            | 32 GB  | 2       | 600   | 3     | 1.43   |
| Apple     | HDD ST750LM022     | 752 GB | 3       | 523   | 0     | 1.43   |
| WDC       | WD1001FAES-60Z2A0  | 1 TB   | 3       | 522   | 0     | 1.43   |
| Seagate   | ST160LM003 HN-M... | 160 GB | 3       | 522   | 0     | 1.43   |
| WDC       | WD1501FASS-00W2B0  | 1.5 TB | 2       | 522   | 0     | 1.43   |
| Maxtor    | 4K020H1            | 20 GB  | 1       | 522   | 0     | 1.43   |
| ExcelStor | J9250S             | 250 GB | 6       | 667   | 205   | 1.43   |
| WDC       | WD5000AAKX-07U6AA1 | 500 GB | 2       | 521   | 0     | 1.43   |
| WDC       | WD800BB-00JKC0     | 80 GB  | 2       | 520   | 0     | 1.43   |
| WDC       | WD6400AARS-003BB1  | 640 GB | 1       | 520   | 0     | 1.43   |
| WDC       | WD10SPCX-75KHST0   | 1 TB   | 8       | 520   | 0     | 1.43   |
| HGST      | HTE721010A9E630    | 1 TB   | 9       | 729   | 2     | 1.42   |
| Seagate   | ST330621A          | 32 GB  | 2       | 664   | 5     | 1.42   |
| WDC       | WD5000AAKS-00A7B2  | 500 GB | 44      | 865   | 20    | 1.42   |
| WDC       | WD3200LPLX-75ZNTT0 | 320 GB | 2       | 519   | 0     | 1.42   |
| WDC       | WD20NMVW-59EDZS7   | 2 TB   | 4       | 668   | 3     | 1.42   |
| Seagate   | ST5000LM000-2AN170 | 5 TB   | 53      | 556   | 18    | 1.42   |
| WDC       | WD5000LPVT-16G33T0 | 500 GB | 5       | 518   | 0     | 1.42   |
| Seagate   | ST3250310AS        | 250 GB | 215     | 1018  | 233   | 1.42   |
| WDC       | WD800AAJS-00L7A0   | 80 GB  | 3       | 517   | 0     | 1.42   |
| Toshiba   | MD04ACA500         | 5 TB   | 10      | 581   | 2     | 1.42   |
| WDC       | WD20NMVW-59AV3S3   | 2 TB   | 2       | 626   | 4     | 1.41   |
| WDC       | WD10JPVT-00A1YT0   | 1 TB   | 6       | 737   | 150   | 1.41   |
| Toshiba   | HDWT360            | 6 TB   | 1       | 516   | 0     | 1.41   |
| Seagate   | ST3120026A         | 120 GB | 27      | 962   | 137   | 1.41   |
| WDC       | WD7500BPVX-08JC3T5 | 752 GB | 1       | 515   | 0     | 1.41   |
| WDC       | WD3200BEKT-75PVMT1 | 320 GB | 28      | 662   | 25    | 1.41   |
| Apple     | HDD ST500LM012     | 500 GB | 5       | 515   | 0     | 1.41   |
| Hitachi   | HTS722012K9SA00    | 120 GB | 5       | 576   | 407   | 1.41   |
| Seagate   | ST250LT007-9ZV14C  | 250 GB | 6       | 792   | 200   | 1.41   |
| WDC       | WD1003FBYX-05Y7B0  | 1 TB   | 2       | 555   | 883   | 1.41   |
| Seagate   | ST2000LM003 HN-... | 2 TB   | 112     | 578   | 4     | 1.41   |
| WDC       | WD5000AAKS-22TMA0  | 500 GB | 2       | 514   | 0     | 1.41   |
| Toshiba   | MQ03UBB200         | 2 TB   | 23      | 579   | 102   | 1.41   |
| WDC       | WD3200BUCT-63TWBY0 | 320 GB | 9       | 553   | 2     | 1.41   |
| WDC       | WD3200BEKX-75B7WT0 | 320 GB | 6       | 568   | 1     | 1.41   |
| WDC       | WD400BB-00DEA0     | 40 GB  | 2       | 1013  | 3     | 1.41   |
| WDC       | WD740ADFD-00NLR5   | 74 GB  | 3       | 512   | 0     | 1.40   |
| WDC       | WD2500AAKX-221CA1  | 250 GB | 3       | 1011  | 6     | 1.40   |
| WDC       | WD30EZRZ-00Z5HB0   | 3 TB   | 56      | 622   | 31    | 1.40   |
| Hitachi   | HDT721064SLA360    | 640 GB | 12      | 949   | 39    | 1.40   |
| WDC       | WD2500AVCS-632DY1  | 250 GB | 1       | 510   | 0     | 1.40   |
| WDC       | WD3200AAJS-55B4A0  | 320 GB | 2       | 749   | 4     | 1.40   |
| Hitachi   | HDT721032SLA380    | 320 GB | 15      | 755   | 159   | 1.40   |
| Seagate   | ST3750640AS        | 752 GB | 20      | 961   | 177   | 1.40   |
| Seagate   | ST2000DM006-2DM164 | 2 TB   | 307     | 582   | 76    | 1.39   |
| Seagate   | ST1000NM000A       | 1 TB   | 7       | 508   | 0     | 1.39   |
| WDC       | WD6400AAKS-55A7B0  | 640 GB | 1       | 507   | 0     | 1.39   |
| Hitachi   | HDS728080PLAT20    | 82 GB  | 29      | 701   | 6     | 1.39   |
| Seagate   | ST320LT023-1AF142  | 320 GB | 2       | 676   | 28    | 1.39   |
| WDC       | WD1600JS-56MHB1    | 160 GB | 7       | 922   | 5     | 1.39   |
| Samsung   | HD321HJ            | 320 GB | 16      | 832   | 148   | 1.39   |
| WDC       | WD3200AAKS-75L9A0  | 320 GB | 35      | 978   | 27    | 1.39   |
| WDC       | WD1600AAJS-00M0A0  | 160 GB | 7       | 691   | 59    | 1.38   |
| WDC       | WD2500AAKX-001CA0  | 250 GB | 42      | 656   | 74    | 1.38   |
| Toshiba   | MK2556GSYF         | 250 GB | 1       | 503   | 0     | 1.38   |
| Seagate   | ST31500541AS       | 1.5 TB | 17      | 775   | 27    | 1.38   |
| WDC       | WD20EZRZ-22Z5HB0   | 2 TB   | 15      | 503   | 0     | 1.38   |
| Samsung   | HD403LJ            | 400 GB | 25      | 1187  | 411   | 1.38   |
| WDC       | WD2500JD-75HBB0    | 250 GB | 1       | 501   | 0     | 1.37   |
| Seagate   | ST12000NM0117-2... | 12 TB  | 2       | 501   | 0     | 1.37   |
| WDC       | WD800JD-22JNC0     | 80 GB  | 3       | 580   | 2     | 1.37   |
| Toshiba   | MD03ACA400V        | 4 TB   | 2       | 945   | 3     | 1.37   |
| Seagate   | ST2000DM001-9YN164 | 2 TB   | 105     | 924   | 302   | 1.37   |
| WDC       | WD10EALX-559BA0    | 1 TB   | 7       | 816   | 6     | 1.37   |
| Hitachi   | HTS545050B9A302    | 500 GB | 5       | 588   | 1     | 1.37   |
| Seagate   | ST3320620A         | 320 GB | 31      | 828   | 139   | 1.37   |
| Seagate   | ST380012ACE        | 80 GB  | 4       | 498   | 0     | 1.37   |
| Apple     | HDD HTS545050A7... | 500 GB | 55      | 542   | 26    | 1.37   |
| Seagate   | ST380817AS         | 80 GB  | 57      | 776   | 8     | 1.37   |
| WDC       | WD7500AZEX-00ZF5A0 | 752 GB | 6       | 497   | 0     | 1.36   |
| WDC       | WD800JD-00HKA0     | 80 GB  | 5       | 1137  | 25    | 1.36   |
| WDC       | WD200EB-00BHF0     | 20 GB  | 1       | 992   | 1     | 1.36   |
| WDC       | WD800BB-55JKA0     | 80 GB  | 5       | 740   | 1     | 1.36   |
| WDC       | WD3200BEVT-11ZCT0  | 320 GB | 8       | 660   | 379   | 1.36   |
| Seagate   | ST1000VM002-1SD102 | 1 TB   | 10      | 496   | 0     | 1.36   |
| WDC       | WD6400AAKS-22A7B2  | 640 GB | 40      | 843   | 12    | 1.36   |
| WDC       | WD4001FFSX-68JNUN0 | 4 TB   | 4       | 901   | 4     | 1.36   |
| WDC       | WD1200JD-00GBB0    | 120 GB | 3       | 754   | 4     | 1.36   |
| WDC       | WD800BEVT-00ZCT0   | 80 GB  | 2       | 494   | 0     | 1.36   |
| Fujitsu   | MPE3136AH          | 16 GB  | 1       | 494   | 0     | 1.35   |
| Samsung   | HD753LJ            | 752 GB | 69      | 1203  | 191   | 1.35   |
| WDC       | WD3200AAKS-00SBA0  | 320 GB | 15      | 825   | 19    | 1.35   |
| WDC       | WD10JPVX-08JC3T2   | 1 TB   | 8       | 689   | 2     | 1.35   |
| Seagate   | ST31000524NS       | 1 TB   | 16      | 916   | 98    | 1.35   |
| WDC       | WD4000FYYZ-05UL1B0 | 4 TB   | 1       | 493   | 0     | 1.35   |
| WDC       | WD2500JS-75NCB1    | 250 GB | 3       | 1381  | 51    | 1.35   |
| HGST      | HUH728080ALE600    | 8 TB   | 9       | 726   | 6     | 1.35   |
| Seagate   | ST9320421ASG       | 320 GB | 3       | 787   | 6     | 1.35   |
| WDC       | WD3000FYYZ-01UL1B3 | 3 TB   | 1       | 492   | 0     | 1.35   |
| WDC       | WD2500AAJB-00J3A0  | 250 GB | 18      | 769   | 5     | 1.35   |
| WDC       | WD6002FRYZ-01WD5B0 | 6 TB   | 2       | 817   | 1     | 1.35   |
| WDC       | WD5000AAKS-00V2B0  | 500 GB | 3       | 663   | 1     | 1.35   |
| Seagate   | ST1000VX000-9YW162 | 1 TB   | 5       | 491   | 0     | 1.35   |
| Seagate   | ST2000NM0055-1V... | 2 TB   | 4       | 491   | 0     | 1.35   |
| WDC       | WD10EADX-00TDHB0   | 1 TB   | 6       | 763   | 11    | 1.35   |
| WDC       | WD10JMVW-11S5XS0   | 1 TB   | 12      | 715   | 3     | 1.35   |
| WDC       | WD6400BPVT-75HXZT1 | 640 GB | 7       | 562   | 1     | 1.34   |
| WDC       | WD1003FBYX-01Y7B1  | 1 TB   | 51      | 775   | 3     | 1.34   |
| WDC       | WD2500AAKS-00F0A0  | 250 GB | 11      | 872   | 217   | 1.34   |
| WDC       | WD10EZEX-08Y20A0   | 1 TB   | 14      | 564   | 2     | 1.34   |
| WDC       | WD3200AAJS-65M0A0  | 320 GB | 9       | 895   | 229   | 1.34   |
| WDC       | WD800BB-00JHA0     | 80 GB  | 8       | 827   | 4     | 1.34   |
| WDC       | WD400JD-55MSA1     | 40 GB  | 1       | 488   | 0     | 1.34   |
| Hitachi   | HDT722516DLA380    | 164 GB | 20      | 932   | 37    | 1.34   |
| WDC       | WD6400BPVT-55HXZT2 | 640 GB | 2       | 488   | 0     | 1.34   |
| Samsung   | HD040GJ-P          | 40 GB  | 2       | 737   | 507   | 1.34   |
| Maxtor    | 6V080E0            | 80 GB  | 13      | 741   | 4     | 1.34   |
| HGST      | HUS726040ALA614    | 4 TB   | 8       | 619   | 2     | 1.33   |
| WDC       | WD5000AACS-32G8B1  | 500 GB | 1       | 487   | 0     | 1.33   |
| WDC       | WD3200AZRX-00A8LB0 | 320 GB | 5       | 487   | 0     | 1.33   |
| WDC       | WD20EADS-00R6B0    | 2 TB   | 10      | 801   | 331   | 1.33   |
| WDC       | WD102KRYZ-01A5AB0  | 10 TB  | 7       | 486   | 0     | 1.33   |
| WDC       | WD1600BJKT-00F4T0  | 160 GB | 1       | 486   | 0     | 1.33   |
| Seagate   | ST3402111AS        | 40 GB  | 2       | 1607  | 524   | 1.33   |
| Seagate   | ST500DM009-2DM14C  | 500 GB | 6       | 500   | 5     | 1.33   |
| Toshiba   | MQ01UBB200         | 2 TB   | 14      | 826   | 243   | 1.33   |
| WDC       | WD1600AAJS-65WAA0  | 160 GB | 3       | 1039  | 671   | 1.33   |
| Seagate   | ST1000DX001-1CM... | 1 TB   | 2       | 733   | 1     | 1.33   |
| Seagate   | ST320410A          | 20 GB  | 8       | 830   | 10    | 1.33   |
| Seagate   | ST3750640NS        | 752 GB | 22      | 1427  | 415   | 1.33   |
| Seagate   | ST3160023A         | 160 GB | 19      | 862   | 271   | 1.33   |
| Fujitsu   | MJA2250BH FFS G1   | 250 GB | 5       | 644   | 2     | 1.33   |
| Seagate   | ST3160212AS        | 160 GB | 4       | 497   | 2     | 1.33   |
| Seagate   | ST33000651AS       | 3 TB   | 12      | 706   | 169   | 1.33   |
| WDC       | WD10JMVW-11AJGS2   | 1 TB   | 40      | 644   | 5     | 1.33   |
| WDC       | WD3200BEVT-75ZCT2  | 320 GB | 19      | 582   | 41    | 1.32   |
| WDC       | WD10EUCX-73YZ1Y0   | 1 TB   | 3       | 707   | 72    | 1.32   |
| Seagate   | ST10000VN0004-2... | 10 TB  | 1       | 483   | 0     | 1.32   |
| HP        | GB0250EAFJF        | 250 GB | 3       | 1117  | 3     | 1.32   |
| WDC       | WD3200BPVT-16JJ5T0 | 320 GB | 9       | 640   | 1     | 1.32   |
| Hitachi   | HCS5C1050CLA382    | 500 GB | 2       | 482   | 0     | 1.32   |
| Seagate   | ST340015A          | 40 GB  | 5       | 835   | 33    | 1.32   |
| WDC       | WD5000AVDS-63U7B1  | 500 GB | 31      | 838   | 30    | 1.32   |
| WDC       | WD4003FRYZ-01F0DB0 | 4 TB   | 10      | 481   | 0     | 1.32   |
| WDC       | WD10EZEX-60ZF5A0   | 1 TB   | 85      | 838   | 135   | 1.32   |
| WDC       | WD5000AAKS-08WWPA0 | 500 GB | 4       | 1261  | 41    | 1.32   |
| WDC       | WD10EZEX-07M2NA0   | 1 TB   | 6       | 793   | 4     | 1.32   |
| WDC       | WD2002FFSX-68PF8N0 | 2 TB   | 7       | 480   | 0     | 1.32   |
| WDC       | WD1600AAJS-00L7A0  | 160 GB | 52      | 888   | 7     | 1.31   |
| WDC       | WD5000AAKX-08U6AA0 | 500 GB | 105     | 595   | 5     | 1.31   |
| WDC       | WD3200AAKS-00V6A0  | 320 GB | 4       | 544   | 1     | 1.31   |
| Seagate   | ST8000DM0004-1Z... | 8 TB   | 5       | 478   | 0     | 1.31   |
| Samsung   | HD501LJ            | 500 GB | 115     | 1143  | 422   | 1.31   |
| WDC       | WD3200BMVU-11A04S0 | 320 GB | 3       | 480   | 77    | 1.31   |
| Seagate   | ST250DM000-1BC141  | 250 GB | 17      | 518   | 6     | 1.31   |
| Fujitsu   | MHW2120BH          | 120 GB | 32      | 541   | 48    | 1.31   |
| WDC       | WD5000AAKX-08ERMA0 | 500 GB | 47      | 753   | 117   | 1.30   |
| Seagate   | ST9120821A         | 120 GB | 4       | 719   | 19    | 1.30   |
| Seagate   | ST1000NC001-1DY162 | 1 TB   | 8       | 892   | 127   | 1.30   |
| WDC       | WD10EARS-00Z5B1    | 1 TB   | 14      | 1000  | 85    | 1.30   |
| WDC       | WD800JD-00LSA5     | 80 GB  | 3       | 475   | 0     | 1.30   |
| WDC       | WD120EMAZ-11BLFA0  | 12 TB  | 13      | 475   | 0     | 1.30   |
| WDC       | WD10JMVW-11AJGS0   | 1 TB   | 9       | 740   | 9     | 1.30   |
| Fujitsu   | MHV2120AH          | 120 GB | 3       | 587   | 2     | 1.30   |
| Toshiba   | MK1032GSX          | 100 GB | 10      | 485   | 1     | 1.30   |
| WDC       | WD10EACS-11BHUB0   | 1 TB   | 1       | 473   | 0     | 1.30   |
| Toshiba   | MK1016GAP          | 10 GB  | 1       | 472   | 0     | 1.29   |
| Seagate   | ST2000VN000-1H3164 | 2 TB   | 6       | 743   | 9     | 1.29   |
| Seagate   | ST3160815A         | 160 GB | 42      | 744   | 213   | 1.29   |
| WDC       | WD3200AAJS-00B4A0  | 320 GB | 30      | 927   | 76    | 1.29   |
| Seagate   | ST1000VM002-1CT162 | 1 TB   | 22      | 898   | 265   | 1.29   |
| WDC       | WD20EARX-55PASB0   | 2 TB   | 4       | 471   | 0     | 1.29   |
| Toshiba   | MG04ACA100NY       | 1 TB   | 11      | 470   | 0     | 1.29   |
| Hitachi   | HUA723030ALA641    | 3 TB   | 11      | 479   | 2     | 1.29   |
| WDC       | WD40PURX-78AKYY0   | 4 TB   | 2       | 470   | 0     | 1.29   |
| WDC       | WD3001FAEX-00MJRA0 | 3 TB   | 5       | 1269  | 3     | 1.29   |
| WDC       | WD5000AAKX-75U6AA0 | 500 GB | 63      | 694   | 60    | 1.29   |
| ExcelStor | J880               | 82 GB  | 1       | 469   | 0     | 1.29   |
| Seagate   | ST5000VX0011-1T... | 5 TB   | 1       | 468   | 0     | 1.28   |
| WDC       | WD60EZRZ-11RWYB1   | 6 TB   | 1       | 468   | 0     | 1.28   |
| Seagate   | ST320014A          | 20 GB  | 9       | 852   | 10    | 1.28   |
| WDC       | WD1600BEVS-22RST0  | 160 GB | 54      | 563   | 69    | 1.28   |
| Seagate   | ST14000DM001-2J... | 14 TB  | 3       | 467   | 0     | 1.28   |
| Hitachi   | HDS721616PLA380    | 160 GB | 118     | 921   | 97    | 1.28   |
| Seagate   | ST8000VX0022-2E... | 8 TB   | 5       | 697   | 26    | 1.28   |
| WDC       | WD10EURX-62C57Y0   | 1 TB   | 1       | 466   | 0     | 1.28   |
| Samsung   | SV0221N            | 20 GB  | 1       | 2328  | 4     | 1.28   |
| IBM/Hi... | IC35L060AVV207-0   | 40 GB  | 3       | 1555  | 40    | 1.28   |
| Seagate   | STM3250318AS       | 250 GB | 37      | 742   | 165   | 1.27   |
| WDC       | WD15EARX-22PASB0   | 1.5 TB | 3       | 464   | 0     | 1.27   |
| WDC       | WD5003AZEX-00K3CA0 | 500 GB | 6       | 494   | 2     | 1.27   |
| WDC       | WD10EZEX-00M2NA0   | 1 TB   | 4       | 509   | 10    | 1.27   |
| Hitachi   | HDT721064SLA380    | 640 GB | 1       | 464   | 0     | 1.27   |
| WDC       | WD800AAJS-00B4A0   | 80 GB  | 5       | 543   | 3     | 1.27   |
| Seagate   | ST500DM002-1SB10A  | 500 GB | 69      | 508   | 48    | 1.27   |
| WDC       | WD400BB-00JHC0     | 40 GB  | 5       | 842   | 20    | 1.27   |
| WDC       | WD6400BPVT-80HXZT3 | 640 GB | 8       | 702   | 9     | 1.27   |
| Seagate   | ST3500830AS        | 500 GB | 21      | 944   | 381   | 1.27   |
| WDC       | WD5000BPKX-00HPJT0 | 500 GB | 6       | 462   | 0     | 1.27   |
| WDC       | WD10EZRZ-00Z5HB0   | 1 TB   | 11      | 491   | 1     | 1.26   |
| WDC       | WD7500BPKT-75PK4T0 | 752 GB | 31      | 689   | 3     | 1.26   |
| WDC       | WD20PURX-64P6ZY0   | 2 TB   | 24      | 569   | 7     | 1.26   |
| Seagate   | ST3250620A         | 250 GB | 15      | 692   | 42    | 1.26   |
| Hitachi   | HTS727550A9E364    | 500 GB | 39      | 801   | 429   | 1.26   |
| HGST      | HUH721008ALE600    | 8 TB   | 5       | 828   | 2     | 1.26   |
| WDC       | WD1600JS-00NCB1    | 160 GB | 20      | 756   | 29    | 1.26   |
| WDC       | WD1600BEVS-08RST2  | 160 GB | 3       | 459   | 0     | 1.26   |
| WDC       | WD5000AADS-00S9B0  | 500 GB | 170     | 855   | 41    | 1.26   |
| WDC       | WD800JD-22LSA0     | 80 GB  | 10      | 929   | 83    | 1.26   |
| Seagate   | ST2000NP0011       | 2 TB   | 3       | 941   | 2068  | 1.26   |
| Seagate   | ST3500411SV        | 500 GB | 3       | 646   | 25    | 1.26   |
| Seagate   | ST980411ASG        | 80 GB  | 4       | 748   | 6     | 1.26   |
| WDC       | WD2500JS-22MHB0    | 250 GB | 4       | 580   | 70    | 1.26   |
| WDC       | WD15EARX-00ZUDB0   | 1.5 TB | 5       | 790   | 3     | 1.26   |
| WDC       | WD2500AAJS-22VTA0  | 250 GB | 9       | 564   | 1     | 1.26   |
| Seagate   | ST3250820A         | 250 GB | 12      | 906   | 446   | 1.26   |
| WDC       | WD1600BEVS-22UST0  | 160 GB | 4       | 684   | 49    | 1.25   |
| Toshiba   | MQ01ABD100H        | 1 TB   | 1       | 456   | 0     | 1.25   |
| Seagate   | ST250DM000-1BD141  | 250 GB | 171     | 716   | 105   | 1.25   |
| WDC       | WD7500BPKX-22HPJT0 | 752 GB | 18      | 468   | 1     | 1.25   |
| WDC       | WD3200AAJS-60M0A0  | 320 GB | 4       | 839   | 2     | 1.25   |
| WDC       | WD1600AAJS-00B4A0  | 160 GB | 24      | 686   | 59    | 1.25   |
| WDC       | WD5000AAKX-001CA0  | 500 GB | 284     | 785   | 39    | 1.25   |
| Samsung   | HD253GJ            | 250 GB | 16      | 778   | 10    | 1.25   |
| Seagate   | ST1500DM003-1CH16G | 1.5 TB | 9       | 481   | 2     | 1.25   |
| WDC       | WD2500AABS-00SDA0  | 250 GB | 1       | 455   | 0     | 1.25   |
| Seagate   | ST500VT000-1BS142  | 500 GB | 3       | 454   | 0     | 1.25   |
| WDC       | WD3200AAJS-60Z0A0  | 320 GB | 16      | 1124  | 85    | 1.24   |
| Hitachi   | HTS723232L9A362    | 320 GB | 2       | 959   | 4     | 1.24   |
| WDC       | WD5000AAKS-007AA0  | 500 GB | 16      | 767   | 8     | 1.24   |
| Seagate   | ST500VM000-1SD101  | 500 GB | 6       | 453   | 0     | 1.24   |
| Hitachi   | HTS541610J9SA00    | 100 GB | 2       | 453   | 0     | 1.24   |
| WDC       | WD1001FALS-55J7B0  | 1 TB   | 2       | 453   | 0     | 1.24   |
| WDC       | WD1600BEVS-00VAT0  | 160 GB | 3       | 453   | 0     | 1.24   |
| Seagate   | ST5000DM002-1XY17X | 5 TB   | 1       | 452   | 0     | 1.24   |
| Seagate   | ST10000NM0568-2... | 10 TB  | 4       | 452   | 0     | 1.24   |
| WDC       | WD10EZEX-00WN4A0   | 1 TB   | 166     | 509   | 12    | 1.24   |
| Maxtor    | STM3320820AS       | 320 GB | 27      | 800   | 191   | 1.24   |
| WDC       | WD3200AAKS-61L9A0  | 320 GB | 13      | 688   | 8     | 1.24   |
| WDC       | WD5000AADS-56S9B0  | 500 GB | 3       | 451   | 1     | 1.24   |
| Hitachi   | HTS545016B9SA02    | 160 GB | 4       | 552   | 34    | 1.24   |
| WDC       | WD5000AAKX-00ERMA0 | 500 GB | 185     | 679   | 8     | 1.24   |
| Seagate   | ST2000DM009-2G4100 | 2 TB   | 10      | 451   | 0     | 1.24   |
| WDC       | WD800JD-55MUA1     | 80 GB  | 11      | 600   | 6     | 1.23   |
| Toshiba   | MD03ACA300V        | 3 TB   | 1       | 450   | 0     | 1.23   |
| WDC       | WD2500BEVT-22ZCT0  | 250 GB | 64      | 559   | 47    | 1.23   |
| WDC       | WD60PURX-64T0ZY0   | 6 TB   | 6       | 449   | 0     | 1.23   |
| WDC       | WD1600AAJS-00WAA0  | 160 GB | 13      | 553   | 4     | 1.23   |
| WDC       | WD3200AAJS-08L7A0  | 320 GB | 31      | 980   | 74    | 1.23   |
| WDC       | WD2004FBYZ-01YCBB1 | 2 TB   | 5       | 449   | 0     | 1.23   |
| Hitachi   | HDS728080PLA380... | 80 GB  | 1       | 449   | 0     | 1.23   |
| WDC       | WD5000BEKT-00KA9T0 | 500 GB | 2       | 1084  | 7     | 1.23   |
| WDC       | WD2500AAJS-00V4A0  | 250 GB | 6       | 742   | 1     | 1.23   |
| ExcelStor | J360               | 64 GB  | 1       | 897   | 1     | 1.23   |
| Hitachi   | HDT722525DLA380    | 250 GB | 21      | 1141  | 208   | 1.23   |
| WDC       | WD80EZAZ-11TDBA0   | 8 TB   | 48      | 448   | 3     | 1.23   |
| Seagate   | ST3500418AS        | 500 GB | 632     | 837   | 153   | 1.23   |
| Samsung   | HD502HI            | 500 GB | 73      | 909   | 279   | 1.23   |
| Hitachi   | HTS541064A9E680    | 640 GB | 3       | 447   | 0     | 1.23   |
| Seagate   | ST3120022A         | 120 GB | 47      | 711   | 132   | 1.23   |
| Hitachi   | HCP725032GLA380    | 320 GB | 7       | 655   | 2     | 1.23   |
| WDC       | WD10EADS-19M2B0    | 1 TB   | 1       | 446   | 0     | 1.22   |
| Toshiba   | MK8032GSX          | 80 GB  | 12      | 564   | 131   | 1.22   |
| Seagate   | ST3200820A         | 200 GB | 5       | 491   | 61    | 1.22   |
| Seagate   | ST3250624AS        | 250 GB | 14      | 942   | 101   | 1.22   |
| Seagate   | ST500DM002-1BC142  | 500 GB | 82      | 705   | 138   | 1.22   |
| Seagate   | ST1000DX001-1NS162 | 1 TB   | 28      | 764   | 77    | 1.22   |
| Seagate   | ST1500DL003-9VT16L | 1.5 TB | 51      | 881   | 245   | 1.22   |
| WDC       | WD740GD-00FLA2     | 74 GB  | 1       | 1330  | 2     | 1.22   |
| WDC       | WD1003FZEX-00K3CA0 | 1 TB   | 82      | 467   | 26    | 1.21   |
| WDC       | WD5000AAKS-75A7B0  | 500 GB | 7       | 1129  | 4     | 1.21   |
| Seagate   | ST1000DM003-9YN162 | 1 TB   | 243     | 766   | 232   | 1.21   |
| Hitachi   | HTS723216L9A362    | 160 GB | 1       | 439   | 0     | 1.20   |
| WDC       | WD7500BPVX-60JC3T0 | 752 GB | 13      | 552   | 27    | 1.20   |
| WDC       | WD50EZRZ-00RWYB1   | 5 TB   | 2       | 438   | 0     | 1.20   |
| WDC       | WD7500BPVT-16HXZT3 | 752 GB | 3       | 655   | 1     | 1.20   |
| WDC       | WD5000AAKS-00E4A0  | 500 GB | 12      | 1141  | 38    | 1.20   |
| WDC       | WD3200AAJS-00YZCA0 | 320 GB | 17      | 626   | 7     | 1.20   |
| Seagate   | ST380215AS         | 80 GB  | 35      | 764   | 432   | 1.20   |
| WDC       | WD10JPVT-75A1YT0   | 1 TB   | 23      | 575   | 67    | 1.20   |
| WDC       | WD1600JS-22MHB0    | 160 GB | 4       | 755   | 8     | 1.20   |
| WDC       | WD6003FZBX-00K5WB0 | 6 TB   | 31      | 437   | 0     | 1.20   |
| WDC       | WD5000BPKT-00PK4T0 | 500 GB | 10      | 445   | 1     | 1.20   |
| WDC       | WD5000BEVT-75A0RT0 | 500 GB | 14      | 665   | 32    | 1.20   |
| Seagate   | ST1000NM0008-2F... | 1 TB   | 10      | 436   | 0     | 1.20   |
| WDC       | WD15EADS-11P8B2    | 1.5 TB | 3       | 471   | 1     | 1.20   |
| WDC       | WD10EARS-00Y5B1    | 1 TB   | 192     | 959   | 134   | 1.19   |
| Hitachi   | HCC547550A9E380    | 500 GB | 2       | 729   | 12    | 1.19   |
| WDC       | WD2500JS-57MHB1    | 250 GB | 1       | 434   | 0     | 1.19   |
| IBM/Hi... | IC25N020ATCS04-0   | 20 GB  | 1       | 434   | 0     | 1.19   |
| WDC       | WD10EALS-002BA0    | 1 TB   | 7       | 927   | 154   | 1.19   |
| WDC       | WD3200AAJS-22L7A0  | 320 GB | 15      | 752   | 17    | 1.19   |
| WDC       | WD20EZRZ-00Z5HB0   | 2 TB   | 255     | 508   | 37    | 1.19   |
| Seagate   | ST3000DM007-1WY10G | 3 TB   | 35      | 457   | 1     | 1.19   |
| WDC       | WD40EZRZ-00GXCB0   | 4 TB   | 164     | 439   | 16    | 1.19   |
| WDC       | WD1200BEVS-22RST0  | 120 GB | 3       | 458   | 1     | 1.18   |
| Samsung   | HD322HJ            | 320 GB | 113     | 883   | 142   | 1.18   |
| WDC       | WD1600AABS-62PRA0  | 160 GB | 2       | 431   | 0     | 1.18   |
| Samsung   | HM161GI            | 160 GB | 1       | 431   | 0     | 1.18   |
| Samsung   | SP1644N            | 160 GB | 4       | 636   | 649   | 1.18   |
| Seagate   | ST10000NM0156-2... | 10 TB  | 22      | 578   | 43    | 1.18   |
| WDC       | WD10EZEX-75WN4A0   | 1 TB   | 69      | 464   | 24    | 1.18   |
| WDC       | WD2500BEVS-22UST0  | 250 GB | 79      | 508   | 27    | 1.18   |
| Hitachi   | HTE545025B9A300    | 250 GB | 1       | 430   | 0     | 1.18   |
| Toshiba   | DT01ACA100         | 1 TB   | 691     | 507   | 47    | 1.18   |
| WDC       | WD6400AACS-00D6B1  | 640 GB | 3       | 922   | 125   | 1.18   |
| WDC       | WD2500BUCT-63TWBY0 | 250 GB | 3       | 767   | 347   | 1.17   |
| WDC       | WD5001AALS-00LWTA0 | 500 GB | 7       | 1053  | 43    | 1.17   |
| Hitachi   | HDS721050CLA360    | 500 GB | 90      | 588   | 28    | 1.17   |
| Seagate   | ST4000DM000-2AE166 | 4 TB   | 14      | 522   | 1     | 1.17   |
| WDC       | WD3200LPLX-66ZNTT0 | 320 GB | 1       | 427   | 0     | 1.17   |
| WDC       | WD5000AAKX-083CA1  | 500 GB | 25      | 859   | 34    | 1.17   |
| WDC       | WD50NDZM-59PW8S1   | 5 TB   | 1       | 426   | 0     | 1.17   |
| WDC       | WD4000AAKS-00TMA0  | 400 GB | 5       | 513   | 1     | 1.17   |
| WDC       | WD1200LB-55EDA0    | 120 GB | 1       | 425   | 0     | 1.17   |
| Seagate   | ST1000NM0053-1C... | 1 TB   | 2       | 424   | 0     | 1.16   |
| WDC       | WD1001FALS-42K1B0  | 1 TB   | 1       | 423   | 0     | 1.16   |
| WDC       | WD2500AAJS-40RYA0  | 250 GB | 1       | 422   | 0     | 1.16   |
| Seagate   | ST16000VN001-2R... | 16 TB  | 3       | 574   | 2     | 1.15   |
| Seagate   | ST3120827AS        | 120 GB | 54      | 794   | 13    | 1.15   |
| WDC       | WD5000BPKT-60PK4T0 | 500 GB | 11      | 593   | 118   | 1.15   |
| WDC       | WD5000AAJS-22YFA0  | 500 GB | 6       | 781   | 352   | 1.15   |
| Seagate   | ST380013AS         | 80 GB  | 46      | 1275  | 63    | 1.15   |
| WDC       | WD10SDZW-11UMGS0   | 1 TB   | 17      | 420   | 0     | 1.15   |
| Seagate   | ST3160812A         | 160 GB | 32      | 768   | 340   | 1.15   |
| Seagate   | ST6000NM021A-2R... | 6 TB   | 7       | 419   | 0     | 1.15   |
| WDC       | WD7500BPVT-75A1YT0 | 752 GB | 1       | 419   | 0     | 1.15   |
| WDC       | WD3000FYYZ-05UL1B0 | 3 TB   | 1       | 418   | 0     | 1.15   |
| Toshiba   | HDWE160            | 6 TB   | 31      | 506   | 4     | 1.14   |
| Seagate   | ST31000520AS       | 1 TB   | 29      | 955   | 428   | 1.14   |
| WDC       | WD60EFAX-68SHWN0   | 6 TB   | 10      | 531   | 1     | 1.14   |
| WDC       | WD1600BEVT-35ZCT0  | 160 GB | 3       | 416   | 0     | 1.14   |
| WDC       | WD40PURZ-85TTDY0   | 4 TB   | 39      | 514   | 1     | 1.14   |
| WDC       | WD2500BEVS-00UST0  | 250 GB | 3       | 587   | 2     | 1.14   |
| WDC       | WD7500AARS-00Y5B1  | 752 GB | 15      | 557   | 4     | 1.14   |
| WDC       | WD1600JS-08MHB0    | 160 GB | 1       | 414   | 0     | 1.14   |
| WDC       | WD5000AAKX-22ERMA0 | 500 GB | 88      | 618   | 15    | 1.13   |
| WDC       | WD5000BMVW-11AJGS1 | 500 GB | 1       | 412   | 0     | 1.13   |
| Seagate   | ST3160215AS        | 160 GB | 28      | 783   | 442   | 1.13   |
| Seagate   | ST750LX003-1AC154  | 752 GB | 25      | 632   | 158   | 1.13   |
| WDC       | WD3200AAKX-00ERMA0 | 320 GB | 16      | 671   | 3     | 1.13   |
| WDC       | WD2500AAKX-07U6AA0 | 250 GB | 5       | 411   | 0     | 1.13   |
| WDC       | WD5000AAKX-00U6AA0 | 500 GB | 36      | 545   | 3     | 1.13   |
| Seagate   | ST3500841A         | 500 GB | 1       | 3287  | 7     | 1.13   |
| Seagate   | ST9200420AS        | 200 GB | 3       | 571   | 6     | 1.13   |
| Seagate   | ST3500320NS        | 500 GB | 20      | 819   | 301   | 1.12   |
| WDC       | WD5000AAKX-329BA0  | 500 GB | 1       | 410   | 0     | 1.12   |
| WDC       | WD1600JS-08NCB1    | 160 GB | 6       | 562   | 22    | 1.12   |
| Seagate   | ST2000VM003-1ET164 | 2 TB   | 17      | 491   | 2     | 1.12   |
| Seagate   | ST3250318AS        | 250 GB | 194     | 770   | 119   | 1.12   |
| Seagate   | ST500DM002-1BD142  | 500 GB | 1141    | 704   | 116   | 1.12   |
| WDC       | WD3000FYYZ-01UL1B1 | 3 TB   | 2       | 1047  | 6     | 1.12   |
| WDC       | WD1600AAJS-75PSA0  | 160 GB | 8       | 500   | 2     | 1.12   |
| WDC       | WD1600BEVS-08VAT1  | 160 GB | 1       | 409   | 0     | 1.12   |
| Seagate   | ST1000DX001-1CM162 | 1 TB   | 68      | 627   | 57    | 1.12   |
| Seagate   | ST380811AS         | 80 GB  | 78      | 692   | 429   | 1.12   |
| Seagate   | ST31000523AS       | 1 TB   | 3       | 1683  | 7     | 1.12   |
| WDC       | WD10JPVT-08A1YT1   | 1 TB   | 2       | 408   | 0     | 1.12   |
| WDC       | WD120EMFZ-11A6JA0  | 12 TB  | 35      | 423   | 1     | 1.12   |
| WDC       | WD3200BEVT-22ZCT0  | 320 GB | 151     | 515   | 70    | 1.12   |
| Samsung   | HM502JX            | 500 GB | 5       | 407   | 0     | 1.12   |
| Fujitsu   | MHY2250BH          | 250 GB | 11      | 644   | 128   | 1.12   |
| Toshiba   | DT01ACA050         | 500 GB | 593     | 499   | 42    | 1.12   |
| WDC       | WD800EB-11DJF0     | 80 GB  | 1       | 407   | 0     | 1.12   |
| WDC       | WD2000JB-00KFA0    | 200 GB | 1       | 1220  | 2     | 1.11   |
| WDC       | WD2500JD-00HBB0    | 250 GB | 1       | 406   | 0     | 1.11   |
| WDC       | WD2500AAKS-00UU3A0 | 250 GB | 7       | 523   | 2     | 1.11   |
| WDC       | WD2500BEKT-75PVMT0 | 250 GB | 16      | 554   | 9     | 1.11   |
| WDC       | WD1600AAJS-00V4A0  | 160 GB | 7       | 409   | 11    | 1.11   |
| Samsung   | HD321KJ            | 320 GB | 98      | 942   | 341   | 1.11   |
| HPE       | MB4000GCWDC        | 4 TB   | 4       | 578   | 1     | 1.11   |
| Seagate   | ST1000DM003-1SB102 | 1 TB   | 229     | 458   | 38    | 1.11   |
| WDC       | WD2500AAKS-00V6A0  | 250 GB | 1       | 404   | 0     | 1.11   |
| WDC       | WD10EZEX-60WN4A0   | 1 TB   | 144     | 459   | 20    | 1.11   |
| Samsung   | HE161HJ            | 160 GB | 1       | 1213  | 2     | 1.11   |
| Hitachi   | HDP725040GLA360    | 400 GB | 7       | 835   | 187   | 1.11   |
| Seagate   | ST3400633AS        | 400 GB | 1       | 2017  | 4     | 1.11   |
| WDC       | WD10JMVW-11AJGS3   | 1 TB   | 40      | 520   | 3     | 1.10   |
| Toshiba   | MK1234GSX          | 120 GB | 18      | 757   | 15    | 1.10   |
| Seagate   | ST5000DX000-1H2170 | 5 TB   | 1       | 402   | 0     | 1.10   |
| Seagate   | ST3250624A         | 250 GB | 1       | 1205  | 2     | 1.10   |
| HGST      | HUS726040ALE611    | 4 TB   | 1       | 401   | 0     | 1.10   |
| WDC       | WD5000AVKX-635FY0  | 500 GB | 1       | 401   | 0     | 1.10   |
| Fujitsu   | MHZ2160BH G1       | 160 GB | 15      | 529   | 4     | 1.10   |
| Toshiba   | HDWD130            | 3 TB   | 154     | 424   | 7     | 1.10   |
| WDC       | WD5000AAKS-00UU3A0 | 500 GB | 82      | 790   | 63    | 1.10   |
| WDC       | WD40NMZW-11GX6S1   | 4 TB   | 69      | 438   | 9     | 1.10   |
| WDC       | WD5000BMVW-11S5XS0 | 500 GB | 15      | 695   | 2     | 1.10   |
| WDC       | WD1001FALS-40K1B0  | 1 TB   | 4       | 933   | 4     | 1.10   |
| WDC       | WD5000HHTZ-60N21V0 | 500 GB | 1       | 401   | 0     | 1.10   |
| WDC       | WD5003ABYX-23 8... | 500 GB | 2       | 668   | 2     | 1.10   |
| Quantum   | FIREBALLlct20 40   | 40 GB  | 1       | 400   | 0     | 1.10   |
| Toshiba   | MQ01ACF032         | 320 GB | 30      | 448   | 1     | 1.10   |
| Seagate   | ST2000VM003-1CT164 | 2 TB   | 21      | 505   | 206   | 1.10   |
| WDC       | WD2500AAKS-00VYA0  | 250 GB | 4       | 468   | 1     | 1.10   |
| HGST      | HTS725025A7E630    | 250 GB | 5       | 603   | 331   | 1.10   |
| Toshiba   | MQ01UBD100         | 1 TB   | 73      | 608   | 138   | 1.10   |
| Seagate   | ST8000NE0021-2E... | 8 TB   | 1       | 399   | 0     | 1.10   |
| WDC       | WD10EADS-11P8B2    | 1 TB   | 1       | 799   | 1     | 1.10   |
| WDC       | WD1200JB-00GVA0    | 120 GB | 5       | 684   | 2     | 1.10   |
| Seagate   | ST8000VX0002-1Z... | 8 TB   | 1       | 399   | 0     | 1.10   |
| WDC       | WD5000BEKT-75KA9T0 | 500 GB | 8       | 663   | 4     | 1.09   |
| Seagate   | ST31000524AS       | 1 TB   | 321     | 750   | 224   | 1.09   |
| WDC       | WD2003FYYS-05T9B0  | 2 TB   | 3       | 1194  | 38    | 1.09   |
| WDC       | WD10EZEX-19ZF5A0   | 1 TB   | 1       | 399   | 0     | 1.09   |
| Samsung   | HD400LJ            | 400 GB | 4       | 623   | 5     | 1.09   |
| Hitachi   | HTS543280L9SA00    | 80 GB  | 1       | 398   | 0     | 1.09   |
| WDC       | WD3200AAJB-56R1A0  | 320 GB | 3       | 429   | 4     | 1.09   |
| WDC       | WD5000AAKX-60U6AA0 | 500 GB | 150     | 579   | 98    | 1.09   |
| WDC       | WD10JMVW-11AJGS1   | 1 TB   | 20      | 520   | 85    | 1.09   |
| WDC       | WD3200AVVS-73M8B0  | 320 GB | 1       | 398   | 0     | 1.09   |
| Seagate   | ST1000DX001-SSH... | 1 TB   | 6       | 669   | 26    | 1.09   |
| WDC       | WD5000AAKS-65A7B0  | 500 GB | 12      | 710   | 37    | 1.09   |
| Seagate   | ST6000DM003-2CY186 | 6 TB   | 60      | 414   | 33    | 1.09   |
| Seagate   | ST3802110A         | 80 GB  | 45      | 656   | 413   | 1.09   |
| Seagate   | ST3160023AS        | 160 GB | 25      | 1110  | 23    | 1.09   |
| WDC       | WD2500AAKS-60VYA0  | 250 GB | 2       | 395   | 0     | 1.08   |
| Seagate   | ST3160827AS        | 160 GB | 31      | 939   | 169   | 1.08   |
| HPE       | MB8000GFECR        | 8 TB   | 1       | 395   | 0     | 1.08   |
| WDC       | WD1200BEVS-22UST0  | 120 GB | 38      | 486   | 61    | 1.08   |
| WDC       | WD7500BPKT-22PK4T0 | 752 GB | 20      | 515   | 4     | 1.08   |
| WDC       | WD5000AZLX-00CL5A0 | 500 GB | 9       | 425   | 1     | 1.08   |
| Seagate   | ST6000VN0033-2E... | 6 TB   | 19      | 419   | 1     | 1.08   |
| WDC       | WD10JPVX-08JC3T6   | 1 TB   | 8       | 436   | 1     | 1.08   |
| WDC       | WD7500BPVT-26HXZT3 | 752 GB | 1       | 1575  | 3     | 1.08   |
| Toshiba   | MQ04ABB400         | 4 TB   | 5       | 393   | 0     | 1.08   |
| Seagate   | ST3000VX009-2AY10G | 3 TB   | 5       | 392   | 0     | 1.08   |
| WDC       | WD5000LPVT-22G33T0 | 500 GB | 36      | 532   | 43    | 1.07   |
| Samsung   | HD161HJ            | 160 GB | 80      | 968   | 447   | 1.07   |
| Seagate   | ST320DM000-1BC14C  | 320 GB | 16      | 505   | 15    | 1.07   |
| WDC       | WD10EACS-22D6B0    | 1 TB   | 5       | 1670  | 8     | 1.07   |
| WDC       | WD5000AAKS-22A7B2  | 500 GB | 10      | 1360  | 77    | 1.07   |
| WDC       | WD4002FFWX-68TZ4N0 | 4 TB   | 2       | 389   | 0     | 1.07   |
| WDC       | WD15NMVW-11W68S0   | 1.5 TB | 2       | 389   | 0     | 1.07   |
| WDC       | WD1600AAJS-60B4A0  | 160 GB | 10      | 919   | 128   | 1.07   |
| WDC       | WD5000AACS-22ZUB0  | 500 GB | 1       | 388   | 0     | 1.07   |
| Maxtor    | 6G160P0            | 160 GB | 4       | 510   | 253   | 1.06   |
| WDC       | WD2500AVJS-63WDA0  | 250 GB | 3       | 388   | 0     | 1.06   |
| Seagate   | ST4000VM000-2AF166 | 4 TB   | 4       | 388   | 0     | 1.06   |
| Maxtor    | STM3320620A        | 320 GB | 3       | 592   | 43    | 1.06   |
| WDC       | WD10SPCX-08S8TT0   | 1 TB   | 8       | 388   | 0     | 1.06   |
| WDC       | WD160EMFZ-11AFXA0  | 16 TB  | 1       | 387   | 0     | 1.06   |
| Apple     | HDD HTS541010A9... | 1 TB   | 27      | 474   | 10    | 1.06   |
| HGST      | HTS721010A9E630    | 1 TB   | 660     | 486   | 163   | 1.06   |
| WDC       | WD5000LPCX-35VHAT0 | 500 GB | 3       | 386   | 0     | 1.06   |
| Maxtor    | 7V300F0            | 304 GB | 3       | 1070  | 317   | 1.06   |
| WDC       | WD5000AADS-00M2B0  | 500 GB | 36      | 952   | 150   | 1.06   |
| Samsung   | HD322GJ            | 320 GB | 58      | 704   | 131   | 1.06   |
| Seagate   | ST2000VN004-2E4164 | 2 TB   | 33      | 467   | 7     | 1.06   |
| WDC       | WD40EZRZ-75GXCB0   | 4 TB   | 22      | 384   | 0     | 1.05   |
| WDC       | WD10PURX-64E5EY0   | 1 TB   | 24      | 564   | 2     | 1.05   |
| WDC       | WD5000BEVT-00A03T0 | 500 GB | 3       | 384   | 0     | 1.05   |
| WDC       | WD1600BEVS-07RST0  | 160 GB | 13      | 418   | 1     | 1.05   |
| WDC       | WD5000BEVT-35A0RT0 | 500 GB | 19      | 528   | 36    | 1.05   |
| Hitachi   | HDT721025SLA380    | 250 GB | 15      | 870   | 205   | 1.05   |
| Apple     | HDD ST2000DM001    | 2 TB   | 8       | 546   | 302   | 1.05   |
| Samsung   | HD163GJ            | 160 GB | 2       | 382   | 0     | 1.05   |
| Seagate   | ST500DM005 HD502HJ | 500 GB | 55      | 562   | 9     | 1.05   |
| Fujitsu   | MHV2100AT PL       | 100 GB | 4       | 381   | 0     | 1.05   |
| Seagate   | ST3200822AS        | 200 GB | 28      | 979   | 203   | 1.05   |
| WDC       | WD3200AAJB-00J3A0  | 320 GB | 25      | 726   | 21    | 1.04   |
| WDC       | WD2500JS-60MHB5    | 250 GB | 4       | 848   | 10    | 1.04   |
| WDC       | WD3200AAJS-22B4A0  | 320 GB | 12      | 1238  | 78    | 1.04   |
| WDC       | WD40E31X-00HY4A0   | 4 TB   | 1       | 380   | 0     | 1.04   |
| WDC       | WD6003FRYZ-01F0DB0 | 6 TB   | 18      | 379   | 0     | 1.04   |
| WDC       | WD5000AVCS-982DY1  | 500 GB | 1       | 379   | 0     | 1.04   |
| Seagate   | ST1000DM010-2DM162 | 1 TB   | 14      | 379   | 0     | 1.04   |
| Samsung   | HD161GJ            | 160 GB | 46      | 730   | 164   | 1.04   |
| Fujitsu   | MHV2040AH          | 40 GB  | 5       | 666   | 4     | 1.04   |
| WDC       | WD5000AAKS-00WWPA0 | 500 GB | 10      | 596   | 9     | 1.04   |
| Seagate   | ST31000340NS       | 1 TB   | 25      | 1433  | 321   | 1.04   |
| Toshiba   | HDWG180            | 8 TB   | 9       | 378   | 0     | 1.04   |
| Fujitsu   | MHW2160BH          | 160 GB | 7       | 501   | 13    | 1.04   |
| WDC       | WD2000JS-00SGB0    | 200 GB | 1       | 377   | 0     | 1.03   |
| Toshiba   | MN07ACA12T         | 12 TB  | 1       | 376   | 0     | 1.03   |
| WDC       | WD800AAJS-22WAA0   | 80 GB  | 2       | 376   | 0     | 1.03   |
| WDC       | WD1600BEVS-22VAT0  | 160 GB | 3       | 430   | 1     | 1.03   |
| Seagate   | ST3250410AS        | 250 GB | 221     | 888   | 279   | 1.03   |
| WDC       | WD10JPVT-22A1YT0   | 1 TB   | 13      | 512   | 2     | 1.03   |
| Toshiba   | HDWN180            | 8 TB   | 14      | 375   | 0     | 1.03   |
| WDC       | WD30EZRZ-00GXCB0   | 3 TB   | 34      | 429   | 1     | 1.03   |
| WDC       | WD800BB-00JKA0     | 80 GB  | 1       | 374   | 0     | 1.03   |
| WDC       | WD7500BPKT-80PK4T0 | 752 GB | 5       | 781   | 5     | 1.03   |
| WDC       | WD5000AAKS-00V1A0  | 500 GB | 80      | 881   | 280   | 1.02   |
| WDC       | WD1600AAJS-98PSA0  | 160 GB | 4       | 440   | 1     | 1.02   |
| Seagate   | ST16000NE000-2R... | 16 TB  | 4       | 372   | 0     | 1.02   |
| WDC       | WD2500BEVT-75ZCT2  | 250 GB | 11      | 484   | 1     | 1.02   |
| Seagate   | ST9402112A         | 40 GB  | 1       | 1117  | 2     | 1.02   |
| WDC       | WD1600JS-22NCB1    | 160 GB | 4       | 712   | 6     | 1.02   |
| Seagate   | ST8000DM005-2EH112 | 8 TB   | 3       | 726   | 22    | 1.02   |
| WDC       | WD2500BEVT-35ZCT0  | 250 GB | 2       | 845   | 225   | 1.02   |
| WDC       | WD10JPVT-60A1YT0   | 1 TB   | 6       | 742   | 337   | 1.02   |
| Hitachi   | HTS545032B9SA00    | 320 GB | 11      | 497   | 376   | 1.02   |
| Hitachi   | HTS541660J9AT00    | 64 GB  | 2       | 788   | 2     | 1.02   |
| Seagate   | ST980310AS         | 80 GB  | 2       | 449   | 1     | 1.02   |
| Seagate   | ST12000NM0538-2... | 12 TB  | 3       | 371   | 0     | 1.02   |
| WDC       | WD10JPLX-00MBPT0   | 1 TB   | 56      | 395   | 4     | 1.02   |
| WDC       | WD2500AVVS-62L2B0  | 250 GB | 3       | 373   | 3     | 1.02   |
| WDC       | WD2500AAKX-00U6AA0 | 250 GB | 3       | 373   | 3     | 1.01   |
| WDC       | WD1600BEVT-75ZCT2  | 160 GB | 21      | 460   | 99    | 1.01   |
| WDC       | WD7500BPVT-00HXZT3 | 752 GB | 12      | 637   | 8     | 1.01   |
| WDC       | WD10JPVX-35JC3T0   | 1 TB   | 7       | 512   | 1     | 1.01   |
| WDC       | WD3200BEKT-00KA9T0 | 320 GB | 1       | 369   | 0     | 1.01   |
| WDC       | WD5000BPVT-08HXZT3 | 500 GB | 11      | 456   | 2     | 1.01   |
| Seagate   | ST3750525AS        | 752 GB | 22      | 714   | 196   | 1.01   |
| WDC       | WD5000BPKT-75PK4T0 | 500 GB | 18      | 533   | 3     | 1.01   |
| WDC       | WD20PURZ-85GU6Y0   | 2 TB   | 34      | 440   | 59    | 1.01   |
| WDC       | WD2500AAKX-08U6AA0 | 250 GB | 12      | 439   | 2     | 1.01   |
| Seagate   | ST4000NM0035-1V... | 4 TB   | 14      | 511   | 124   | 1.01   |
| Toshiba   | MQ01ABD100V -63    | 1 TB   | 2       | 367   | 0     | 1.01   |
| WDC       | WD3200AVVS-56L2B0  | 320 GB | 10      | 534   | 57    | 1.01   |
| WDC       | WD800JB-00JJC0     | 80 GB  | 26      | 647   | 23    | 1.01   |
| Hitachi   | HDS721680PLAT80    | 80 GB  | 6       | 1080  | 5     | 1.01   |
| WDC       | WD60EZRX-11MVLB1   | 6 TB   | 1       | 366   | 0     | 1.01   |
| WDC       | WD80EFAX-68KNBN0   | 8 TB   | 39      | 366   | 0     | 1.01   |
| HGST      | HUH721010ALE604    | 10 TB  | 13      | 366   | 0     | 1.00   |
| Seagate   | ST31000528AS       | 1 TB   | 364     | 841   | 272   | 1.00   |
| Seagate   | ST2000DX002-2DV164 | 2 TB   | 72      | 491   | 35    | 1.00   |
| WDC       | WD10SPZX-17Z10T1   | 1 TB   | 14      | 366   | 0     | 1.00   |
| HP        | MM0500EANCR        | 500 GB | 15      | 1721  | 83    | 1.00   |
| Toshiba   | HDWD120            | 2 TB   | 162     | 375   | 7     | 1.00   |
| WDC       | WD40EZRZ-19GXCB0   | 4 TB   | 9       | 365   | 0     | 1.00   |
| WDC       | WD2500JB-00REA0    | 250 GB | 12      | 725   | 22    | 1.00   |
| Fujitsu   | MHW2060BH          | 64 GB  | 4       | 787   | 4     | 1.00   |
| WDC       | WD10JPVX-22JC3T0   | 1 TB   | 332     | 453   | 33    | 1.00   |
| Fujitsu   | MHW2040BH          | 40 GB  | 4       | 390   | 1     | 1.00   |
| WDC       | WD5000AAKS-41YGA1  | 500 GB | 1       | 728   | 1     | 1.00   |
| WDC       | WD1600JS-00MHB0    | 160 GB | 8       | 709   | 146   | 1.00   |
| WDC       | WD5000BPVT-80HXZT3 | 500 GB | 31      | 457   | 36    | 1.00   |
| Toshiba   | MK5075GSX          | 500 GB | 47      | 539   | 277   | 1.00   |
| Toshiba   | MG07ACA14TE        | 14 TB  | 7       | 363   | 0     | 1.00   |
| Seagate   | ST1000VT001-1RE172 | 1 TB   | 2       | 363   | 0     | 1.00   |
| Seagate   | ST320LM000 HM321HI | 320 GB | 15      | 376   | 1     | 0.99   |
| Samsung   | SP1654N            | 160 GB | 8       | 849   | 412   | 0.99   |
| Seagate   | ST32000542AS       | 2 TB   | 41      | 913   | 391   | 0.99   |
| WDC       | WD3200AAJS-56M0A0  | 320 GB | 41      | 533   | 31    | 0.99   |
| WDC       | WD800BB-00JHC0     | 80 GB  | 28      | 627   | 67    | 0.99   |
| WDC       | WD2500BEKT-66PVMT0 | 250 GB | 1       | 362   | 0     | 0.99   |
| WDC       | WD2500AAJS-55M0A0  | 250 GB | 4       | 421   | 2     | 0.99   |
| WDC       | WD5000AAJS-22A8B0  | 500 GB | 2       | 2243  | 4     | 0.99   |
| WDC       | WD2500BEVS-08VAT2  | 250 GB | 5       | 361   | 0     | 0.99   |
| Toshiba   | MG04ACA400EY       | 4 TB   | 2       | 360   | 0     | 0.99   |
| HP        | Secure Hard Disk   | 500 GB | 2       | 360   | 0     | 0.99   |
| Seagate   | ST8000DM004-2CX188 | 8 TB   | 189     | 429   | 34    | 0.99   |
| WDC       | WD7500BPVT-75HXZT3 | 752 GB | 8       | 441   | 1     | 0.99   |
| WDC       | WD7500BPVT-55HXZT3 | 752 GB | 4       | 465   | 2     | 0.99   |
| Maxtor    | STM3160212A        | 160 GB | 2       | 817   | 1     | 0.99   |
| WDC       | WD1200BEVS-75UST0  | 120 GB | 17      | 427   | 1     | 0.99   |
| WDC       | WD800BB-22JHC0     | 80 GB  | 12      | 506   | 32    | 0.99   |
| WDC       | WD7500BPVT-22A1YT0 | 752 GB | 5       | 911   | 3     | 0.99   |
| Toshiba   | HDWQ140            | 4 TB   | 35      | 417   | 1     | 0.99   |
| Hitachi   | HDP725032GLA380    | 320 GB | 9       | 886   | 25    | 0.98   |
| WDC       | WD2500BPVT-00JJ5T0 | 250 GB | 3       | 358   | 0     | 0.98   |
| Seagate   | ST4000VN008-2DR166 | 4 TB   | 176     | 379   | 7     | 0.98   |
| Hitachi   | HDT725032VLA360    | 320 GB | 29      | 1035  | 85    | 0.98   |
| WDC       | WD6400AADS-00M2B0  | 640 GB | 14      | 951   | 17    | 0.98   |
| WDC       | WD3200LPLX-00ZNTT0 | 320 GB | 3       | 357   | 0     | 0.98   |
| WDC       | WD2500AAKX-08ANVA0 | 250 GB | 1       | 357   | 0     | 0.98   |
| Seagate   | ST8000NM000A-2K... | 8 TB   | 27      | 356   | 0     | 0.98   |
| WDC       | WD3200AAKX-001CA0  | 320 GB | 42      | 752   | 60    | 0.98   |
| Maxtor    | STM3160215AS       | 160 GB | 45      | 897   | 663   | 0.98   |
| Seagate   | ST3250310NS        | 250 GB | 3       | 737   | 755   | 0.98   |
| Hitachi   | HTS545050B9SA08    | 499 GB | 1       | 713   | 1     | 0.98   |
| WDC       | WD20SPZX-22CRAT0   | 2 TB   | 2       | 356   | 0     | 0.98   |
| WDC       | WD800BD-22MRA1     | 80 GB  | 10      | 880   | 38    | 0.98   |
| WDC       | WD10JPVX-80JC3T0   | 1 TB   | 13      | 355   | 0     | 0.97   |
| Hitachi   | HTS725032A9A362    | 320 GB | 1       | 355   | 0     | 0.97   |
| Hitachi   | HTS725032A9A360    | 320 GB | 6       | 655   | 235   | 0.97   |
| Fujitsu   | MJA2160BH FFS G1   | 160 GB | 4       | 355   | 0     | 0.97   |
| Seagate   | ST500VT000-1DK142  | 500 GB | 34      | 406   | 11    | 0.97   |
| Seagate   | ST98823A           | 80 GB  | 6       | 453   | 216   | 0.97   |
| WDC       | WD5000AAJS-08A8B0  | 500 GB | 2       | 691   | 2     | 0.97   |
| Seagate   | ST3320820AS        | 320 GB | 34      | 552   | 324   | 0.97   |
| WDC       | WD3200AAJS-00M0A0  | 320 GB | 2       | 574   | 1     | 0.97   |
| Toshiba   | MK3261GSYG         | 320 GB | 1       | 354   | 0     | 0.97   |
| HGST      | HUS726060ALA640    | 6 TB   | 1       | 353   | 0     | 0.97   |
| Hitachi   | HTS545032B9A301    | 320 GB | 1       | 353   | 0     | 0.97   |
| WDC       | WD5000LPVX-08V0TT5 | 500 GB | 25      | 398   | 1     | 0.97   |
| Maxtor    | STM380211AS        | 80 GB  | 7       | 630   | 933   | 0.97   |
| WDC       | WD7500BPVT-22HXZT3 | 752 GB | 36      | 427   | 18    | 0.97   |
| Fujitsu   | MJA2160BH G2       | 160 GB | 13      | 485   | 255   | 0.96   |
| WDC       | WD10EALX-008EA0    | 1 TB   | 7       | 358   | 1     | 0.96   |
| WDC       | WD2500JD-22HBC0    | 250 GB | 2       | 1266  | 78    | 0.96   |
| WDC       | WD5000LMZW-11Y0TS0 | 500 GB | 2       | 350   | 0     | 0.96   |
| Seagate   | ST1500LM006 HN-... | 1.5 TB | 9       | 373   | 1     | 0.96   |
| WDC       | WD4005FZBX-00K5WB0 | 4 TB   | 45      | 349   | 1     | 0.96   |
| WDC       | WD50PURX-64T0ZY0   | 5 TB   | 1       | 349   | 0     | 0.96   |
| Hitachi   | HTS545050B9A300    | 500 GB | 185     | 648   | 223   | 0.96   |
| WDC       | WD5000LUCT-63RC2Y0 | 500 GB | 4       | 349   | 0     | 0.96   |
| Samsung   | HM500JI            | 500 GB | 68      | 507   | 15    | 0.96   |
| WDC       | WD1600AAJS-75B4A0  | 160 GB | 3       | 1057  | 3     | 0.96   |
| Seagate   | ST320LM001 HN-M... | 320 GB | 78      | 405   | 2     | 0.96   |
| Maxtor    | STM3160815AS       | 160 GB | 38      | 736   | 395   | 0.96   |
| WDC       | WD10EZEX-08WN4A0   | 1 TB   | 617     | 371   | 9     | 0.96   |
| WDC       | WD5000AAKX-221CA1  | 500 GB | 24      | 617   | 20    | 0.95   |
| ExcelStor | J880S              | 82 GB  | 3       | 733   | 8     | 0.95   |
| WDC       | WD1200JS-00NCB1    | 120 GB | 3       | 558   | 18    | 0.95   |
| Fujitsu   | MHT2080AH          | 80 GB  | 3       | 443   | 22    | 0.95   |
| WDC       | WD5000BMVV-11A1CS0 | 500 GB | 3       | 701   | 63    | 0.95   |
| WDC       | WD3200AVJS-63B6A0  | 320 GB | 12      | 1133  | 11    | 0.95   |
| Seagate   | ST6000DM0003       | 6 TB   | 1       | 346   | 0     | 0.95   |
| WDC       | WD3200JS-22PDB0    | 320 GB | 3       | 837   | 8     | 0.95   |
| Samsung   | SP0802N            | 80 GB  | 29      | 806   | 43    | 0.95   |
| Toshiba   | MQ02ABD100H        | 1 TB   | 37      | 450   | 60    | 0.95   |
| Hitachi   | HDS721680PLA380    | 80 GB  | 61      | 948   | 227   | 0.95   |
| Seagate   | ST980813ASG        | 80 GB  | 6       | 424   | 2     | 0.95   |
| WDC       | WD5000BUCT-63LS5Y1 | 500 GB | 1       | 345   | 0     | 0.95   |
| WDC       | WD1600JD-22HBB0    | 160 GB | 1       | 2072  | 5     | 0.95   |
| WDC       | WD1600BEVT-75ZCT0  | 160 GB | 2       | 695   | 48    | 0.95   |
| Seagate   | ST2000VX002-1AH166 | 2 TB   | 2       | 345   | 0     | 0.95   |
| Seagate   | ST3120814A         | 120 GB | 22      | 739   | 267   | 0.94   |
| WDC       | WD3200BPVT-00HXZT3 | 320 GB | 5       | 476   | 6     | 0.94   |
| WDC       | WD20NMVW-11AV3S3   | 2 TB   | 8       | 447   | 3     | 0.94   |
| Seagate   | ST320DM000-1BD14C  | 320 GB | 38      | 491   | 94    | 0.94   |
| WDC       | WD10JPVX-75JC3T0   | 1 TB   | 97      | 415   | 26    | 0.94   |
| Seagate   | ST3160811AS        | 160 GB | 93      | 817   | 412   | 0.94   |
| WDC       | WD101EFAX-68LDBN0  | 10 TB  | 7       | 344   | 0     | 0.94   |
| WDC       | WD7500BPVX-22JC3T0 | 752 GB | 31      | 447   | 2     | 0.94   |
| Hitachi   | HTS725050A9A362    | 500 GB | 7       | 411   | 45    | 0.94   |
| Seagate   | ST5000DM003-2FH18L | 5 TB   | 1       | 343   | 0     | 0.94   |
| WDC       | WD5000ABPS-01ZZB0  | 500 GB | 2       | 1419  | 4     | 0.94   |
| Seagate   | ST31000528ASQ      | 1 TB   | 3       | 428   | 44    | 0.94   |
| WDC       | WD6401AALS-00E3A0  | 640 GB | 6       | 726   | 5     | 0.94   |
| Samsung   | SP0812N            | 80 GB  | 7       | 597   | 4     | 0.94   |
| Hitachi   | HCS5C1025CLA382    | 250 GB | 1       | 341   | 0     | 0.94   |
| Seagate   | ST320LM010-1KJ15C  | 320 GB | 10      | 586   | 103   | 0.94   |
| HGST      | HTS545025A7E380    | 250 GB | 4       | 341   | 0     | 0.94   |
| WDC       | WD60EZRZ-00GZ5B1   | 6 TB   | 19      | 446   | 2     | 0.94   |
| WDC       | WD10EZEX-21WN4A0   | 1 TB   | 64      | 377   | 1     | 0.93   |
| Fujitsu   | MHT2040AH          | 40 GB  | 3       | 348   | 3     | 0.93   |
| Toshiba   | MQ01ABD075         | 752 GB | 190     | 475   | 115   | 0.93   |
| WDC       | WD800JD-32LSA0     | 80 GB  | 2       | 1577  | 53    | 0.93   |
| WDC       | WD2003FYYS-01T8B0  | 2 TB   | 1       | 3050  | 8     | 0.93   |
| WDC       | WD800BB-75JHC0     | 80 GB  | 3       | 535   | 1     | 0.93   |
| WDC       | WD2500BEVT-35A23T0 | 250 GB | 27      | 502   | 48    | 0.93   |
| WDC       | WD10EZEX-35WN4A0   | 1 TB   | 9       | 338   | 0     | 0.93   |
| Hitachi   | HDT721050SLA380    | 500 GB | 2       | 431   | 3     | 0.93   |
| Samsung   | HD401LJ            | 400 GB | 5       | 678   | 12    | 0.93   |
| WDC       | WD1600BEVT-26A23T0 | 160 GB | 1       | 338   | 0     | 0.93   |
| WDC       | WD3200BEVS-26VAT0  | 320 GB | 6       | 511   | 246   | 0.93   |
| Seagate   | ST1000LM014-1EJ... | 1 TB   | 18      | 501   | 16    | 0.92   |
| HGST      | HTS721075A9E630    | 752 GB | 14      | 429   | 160   | 0.92   |
| ExcelStor | J680               | 82 GB  | 1       | 1687  | 4     | 0.92   |
| IBM/Hi... | IC35L090AVV207-0   | 80 GB  | 2       | 735   | 2     | 0.92   |
| WDC       | WD2500BEVT-08A23T1 | 250 GB | 20      | 411   | 86    | 0.92   |
| WDC       | WD80EMAZ-00M9AA0   | 8 TB   | 1       | 336   | 0     | 0.92   |
| Toshiba   | MQ01UBD050         | 500 GB | 18      | 392   | 337   | 0.92   |
| Seagate   | ST4000NM016A-2H... | 4 TB   | 1       | 336   | 0     | 0.92   |
| WDC       | WD5000BPVT-22HXZT3 | 500 GB | 67      | 481   | 44    | 0.92   |
| WDC       | WD20SPZX-00CRAT0   | 2 TB   | 5       | 594   | 10    | 0.92   |
| WDC       | WD5000LPVT-24G33T1 | 500 GB | 28      | 425   | 48    | 0.92   |
| WDC       | WD10SMZW-11Y0TS0   | 1 TB   | 40      | 335   | 1     | 0.92   |
| WDC       | WD10JMVW-11S5XS1   | 1 TB   | 8       | 520   | 1     | 0.92   |
| HGST      | HUS728T8TALE600    | 8 TB   | 6       | 334   | 0     | 0.92   |
| Fujitsu   | MHZ2250BH G1       | 250 GB | 12      | 516   | 55    | 0.92   |
| WDC       | WD1502FYPS-01U1B1  | 1.5 TB | 2       | 349   | 13    | 0.92   |
| Toshiba   | MK2575GSX          | 250 GB | 2       | 399   | 538   | 0.91   |
| WDC       | WD2500BEVS-75UST0  | 250 GB | 12      | 450   | 2     | 0.91   |
| WDC       | WD3200LPVX-16V0TT0 | 320 GB | 1       | 333   | 0     | 0.91   |
| WDC       | WD5000BMVW-11AMCS2 | 500 GB | 5       | 341   | 2     | 0.91   |
| Seagate   | ST3160215A         | 160 GB | 28      | 724   | 433   | 0.91   |
| Seagate   | STM3500418AS       | 500 GB | 33      | 859   | 369   | 0.91   |
| WDC       | WD5000LPVT-08G33T1 | 500 GB | 18      | 391   | 1     | 0.91   |
| Fujitsu   | MHW2080BH          | 80 GB  | 9       | 411   | 2     | 0.91   |
| WDC       | WD40EMAZ-11LW3B0   | 4 TB   | 4       | 332   | 0     | 0.91   |
| WDC       | WD10EZRZ-00HTKB0   | 1 TB   | 89      | 357   | 19    | 0.91   |
| WDC       | WD5000LPVX-60V0TT0 | 500 GB | 33      | 415   | 67    | 0.91   |
| WDC       | WD7500BPVT-24HXZT3 | 752 GB | 16      | 440   | 34    | 0.91   |
| WDC       | WD800BB-60JKA0     | 80 GB  | 1       | 331   | 0     | 0.91   |
| Hitachi   | HTE725032A9A364    | 320 GB | 1       | 1985  | 5     | 0.91   |
| Seagate   | ST250DM001 HD253GJ | 250 GB | 7       | 330   | 0     | 0.91   |
| Samsung   | HD322GM            | 320 GB | 1       | 1320  | 3     | 0.90   |
| Seagate   | ST4000DM004-2CV104 | 4 TB   | 402     | 357   | 25    | 0.90   |
| WDC       | WD5000BMVW-11AJGS2 | 500 GB | 4       | 329   | 0     | 0.90   |
| WDC       | WD2500BEKT-60PVMT0 | 250 GB | 17      | 461   | 78    | 0.90   |
| WDC       | WD3200LPVX-80V0TT0 | 320 GB | 2       | 328   | 0     | 0.90   |
| WDC       | WD1600BEVT-22ZCT0  | 160 GB | 147     | 447   | 65    | 0.90   |
| WDC       | WD7500BPKT-60PK4T0 | 752 GB | 6       | 384   | 2     | 0.90   |
| WDC       | WD3200BEKT-08PVMT1 | 320 GB | 8       | 399   | 1     | 0.90   |
| WDC       | WD3200BPVT-35ZEST0 | 320 GB | 24      | 451   | 2     | 0.90   |
| Seagate   | ST250LT020-1AE14C  | 250 GB | 3       | 409   | 314   | 0.90   |
| WDC       | WD800BB-08JHC0     | 80 GB  | 1       | 327   | 0     | 0.90   |
| WDC       | WD800BEVT-75ZCT2   | 80 GB  | 4       | 327   | 0     | 0.90   |
| WDC       | WD2500AAJS-00Z0A0  | 250 GB | 3       | 819   | 4     | 0.90   |
| WDC       | WD20SDZW-11Z3CS0   | 2 TB   | 7       | 342   | 1     | 0.90   |
| WDC       | WD7500BMVW-11S5XS0 | 752 GB | 3       | 455   | 3     | 0.90   |
| WDC       | WD5000AAJS-19A8B0  | 500 GB | 1       | 326   | 0     | 0.90   |
| WDC       | WD2500AAKX-00ERMA0 | 250 GB | 39      | 453   | 36    | 0.89   |
| WDC       | WD10JMVW-11AJGS4   | 1 TB   | 65      | 345   | 27    | 0.89   |
| Fujitsu   | MHV2080AT PL       | 80 GB  | 4       | 515   | 569   | 0.89   |
| Toshiba   | MK1255GSX          | 120 GB | 1       | 326   | 0     | 0.89   |
| WDC       | WD10EZEX-22MFCA0   | 1 TB   | 147     | 365   | 13    | 0.89   |
| WDC       | WD2503ABYZ-011FA0  | 256 GB | 1       | 325   | 0     | 0.89   |
| WDC       | WD6400BPVT-22HXZT1 | 640 GB | 9       | 621   | 3     | 0.89   |
| Toshiba   | MK1234GAX          | 120 GB | 4       | 325   | 0     | 0.89   |
| WDC       | WD60EZAZ-00ZGHB0   | 6 TB   | 18      | 325   | 0     | 0.89   |
| Toshiba   | MK3276GSX H        | 320 GB | 3       | 325   | 0     | 0.89   |
| WDC       | WD5000BPVT-24HXZT3 | 500 GB | 29      | 528   | 2     | 0.89   |
| Seagate   | ST9750420AS        | 752 GB | 102     | 641   | 141   | 0.89   |
| ExcelStor | J8160S             | 160 GB | 9       | 701   | 3     | 0.89   |
| WDC       | WD5000BPVT-16HXZT3 | 500 GB | 1       | 324   | 0     | 0.89   |
| WDC       | WD3200JS-00PDB0    | 320 GB | 1       | 324   | 0     | 0.89   |
| Samsung   | HD160JJ            | 160 GB | 98      | 831   | 383   | 0.89   |
| WDC       | WD7500BPKT-00PK4T0 | 752 GB | 10      | 448   | 30    | 0.89   |
| WDC       | WD400BB-23DEA0     | 40 GB  | 3       | 1947  | 4     | 0.89   |
| Apple     | HDD HTS541075A9... | 752 GB | 2       | 323   | 0     | 0.89   |
| WDC       | WD5000BEVT-55A0RT0 | 500 GB | 2       | 373   | 5     | 0.89   |
| Seagate   | ST3160813AS        | 160 GB | 51      | 853   | 118   | 0.89   |
| WDC       | WD20SMZW-34JW8S0   | 2 TB   | 1       | 323   | 0     | 0.89   |
| WDC       | WD8003FRYZ-01JPDB1 | 8 TB   | 2       | 322   | 0     | 0.88   |
| Toshiba   | MK2553GSX          | 250 GB | 1       | 322   | 0     | 0.88   |
| Seagate   | ST1000NX0313       | 1 TB   | 5       | 592   | 74    | 0.88   |
| WDC       | WD3200BVVT-63A26Y0 | 320 GB | 5       | 359   | 132   | 0.88   |
| Seagate   | ST3160211AS        | 160 GB | 13      | 597   | 676   | 0.88   |
| WDC       | WD2500AAJS-08B4A0  | 250 GB | 2       | 931   | 1211  | 0.88   |
| Hitachi   | HTS725016A9A364    | 160 GB | 17      | 602   | 442   | 0.88   |
| Toshiba   | MK3261GSY          | 320 GB | 2       | 320   | 0     | 0.88   |
| WDC       | WD5000AAKS-55V0A0  | 500 GB | 8       | 645   | 6     | 0.88   |
| Seagate   | ST9750422AS        | 752 GB | 5       | 588   | 125   | 0.87   |
| WDC       | WD1600YD-01NVB1    | 164 GB | 2       | 377   | 1     | 0.87   |
| WDC       | WD5000AVDS-73U7B1  | 500 GB | 6       | 376   | 47    | 0.87   |
| WDC       | WD10SPZX-75Z10T0   | 1 TB   | 6       | 318   | 0     | 0.87   |
| Samsung   | SP1203N            | 120 GB | 14      | 703   | 88    | 0.87   |
| Toshiba   | MK5065GSXF         | 500 GB | 34      | 496   | 89    | 0.87   |
| Seagate   | ST500LX012-SSHD... | 500 GB | 5       | 401   | 1     | 0.87   |
| Toshiba   | MK2559GSXP         | 250 GB | 5       | 439   | 15    | 0.87   |
| WDC       | WD5000LPVX-55V0TT0 | 500 GB | 17      | 377   | 1     | 0.87   |
| HGST      | HUH728080ALE604    | 8 TB   | 8       | 316   | 0     | 0.87   |
| WDC       | WD5000BPVT-80HXZT1 | 500 GB | 11      | 639   | 34    | 0.87   |
| Samsung   | HD752LJ            | 752 GB | 2       | 1517  | 4     | 0.87   |
| Seagate   | ST12000NM001G-2... | 12 TB  | 5       | 316   | 0     | 0.87   |
| Fujitsu   | MHV2100AT          | 100 GB | 1       | 316   | 0     | 0.87   |
| WDC       | WD1600AAJS-60M0A1  | 160 GB | 4       | 800   | 257   | 0.87   |
| WDC       | WD3200AVJS-63N9A0  | 320 GB | 6       | 315   | 0     | 0.87   |
| Maxtor    | STM3200820A        | 200 GB | 1       | 315   | 0     | 0.86   |
| WDC       | WD800BEVS-00UST0   | 80 GB  | 1       | 315   | 0     | 0.86   |
| Samsung   | HM641JI            | 640 GB | 47      | 513   | 47    | 0.86   |
| Seagate   | ST9160411AS        | 160 GB | 9       | 583   | 130   | 0.86   |
| Toshiba   | MG08ADA400NY       | 4 TB   | 1       | 314   | 0     | 0.86   |
| WDC       | WD3200AAKB-00WHA0  | 320 GB | 2       | 314   | 0     | 0.86   |
| Seagate   | ST2000VX008-2E3164 | 2 TB   | 14      | 314   | 0     | 0.86   |
| WDC       | WD7500BPVX-55JC3T0 | 752 GB | 1       | 314   | 0     | 0.86   |
| WDC       | WD10JPVX-00JC3T0   | 1 TB   | 64      | 323   | 1     | 0.86   |
| WDC       | WD2000JS-55MHB0    | 200 GB | 1       | 313   | 0     | 0.86   |
| WDC       | WD40NMZM-59Y94S1   | 4 TB   | 1       | 313   | 0     | 0.86   |
| WDC       | WD3200AAKS-00L6A0  | 320 GB | 4       | 577   | 5     | 0.86   |
| WDC       | WD2000JB-00GVA0    | 200 GB | 3       | 590   | 101   | 0.86   |
| Maxtor    | STM380815AS        | 80 GB  | 23      | 730   | 578   | 0.86   |
| WDC       | WD5000AACS-00G8B0  | 500 GB | 7       | 918   | 9     | 0.86   |
| Fujitsu   | MHV2060BH          | 64 GB  | 12      | 469   | 6     | 0.86   |
| Samsung   | HM501II            | 500 GB | 7       | 958   | 64    | 0.86   |
| Samsung   | HD080HJ            | 80 GB  | 117     | 764   | 383   | 0.86   |
| WDC       | WD5000BEVT-24A0RT0 | 500 GB | 29      | 486   | 16    | 0.85   |
| WDC       | WD3200BPVT-24JJ5T0 | 320 GB | 81      | 382   | 46    | 0.85   |
| Maxtor    | STM3250310AS       | 250 GB | 92      | 793   | 405   | 0.85   |
| WDC       | WD2500LPVX-22V0TT0 | 250 GB | 5       | 325   | 1     | 0.85   |
| WDC       | WD800JD-23LSA0     | 80 GB  | 2       | 631   | 2     | 0.85   |
| Fujitsu   | MHZ2160BH G2       | 160 GB | 42      | 560   | 330   | 0.85   |
| Fujitsu   | MHY2200BH          | 200 GB | 24      | 516   | 73    | 0.85   |
| WDC       | WD20NMVW-59AV3S2   | 2 TB   | 2       | 310   | 0     | 0.85   |
| Toshiba   | HDWE140            | 4 TB   | 62      | 348   | 24    | 0.85   |
| WDC       | WD400BB-60DGA0     | 40 GB  | 4       | 403   | 1     | 0.85   |
| Seagate   | ST9320423ASG       | 320 GB | 2       | 443   | 73    | 0.85   |
| Toshiba   | MG03ACA100         | 1 TB   | 16      | 376   | 2     | 0.85   |
| Maxtor    | STM3250820AS       | 250 GB | 19      | 814   | 166   | 0.85   |
| WDC       | WD5000BPVT-00HXZT3 | 500 GB | 18      | 374   | 32    | 0.85   |
| WDC       | WD1600JS-40TGB0    | 160 GB | 1       | 308   | 0     | 0.85   |
| WDC       | WD5000BMVW-11AJGS3 | 500 GB | 2       | 308   | 0     | 0.85   |
| MediaMax  | WL5000GSA12872B    | 5 TB   | 1       | 308   | 0     | 0.85   |
| Toshiba   | MQ02ABF100         | 1 TB   | 14      | 316   | 1     | 0.85   |
| WDC       | WD5000AZLX-75K2TA0 | 500 GB | 19      | 308   | 0     | 0.85   |
| WDC       | WD3200BEKT-60PVMT0 | 320 GB | 20      | 537   | 203   | 0.84   |
| Toshiba   | HDWF180            | 8 TB   | 15      | 315   | 108   | 0.84   |
| WDC       | WD1600AAJS-00YZCA0 | 160 GB | 15      | 496   | 25    | 0.84   |
| WDC       | WD800JB-00JJA0     | 80 GB  | 4       | 1406  | 9     | 0.84   |
| WDC       | WD2500JD-40HBC0    | 250 GB | 1       | 1847  | 5     | 0.84   |
| Hitachi   | HTS723280L9A362    | 80 GB  | 2       | 307   | 0     | 0.84   |
| Seagate   | ST3000VX006-1HH166 | 3 TB   | 2       | 334   | 570   | 0.84   |
| WDC       | WD2500BEKT-60V5T1  | 250 GB | 2       | 399   | 3     | 0.84   |
| WDC       | WD100EDAZ-11F3RA0  | 10 TB  | 1       | 307   | 0     | 0.84   |
| WDC       | WD2500BEKT-00PVMT0 | 250 GB | 3       | 307   | 0     | 0.84   |
| Fujitsu   | MJA2320BH G2       | 320 GB | 14      | 670   | 296   | 0.84   |
| WDC       | WD3200BEVT-00SCST0 | 320 GB | 1       | 306   | 0     | 0.84   |
| WDC       | WD5000LUCT-62C26Y0 | 500 GB | 3       | 452   | 20    | 0.84   |
| WDC       | WD1500ADFD-00NLR1  | 150 GB | 2       | 454   | 4     | 0.84   |
| WDC       | WD800BEVS-22VAT0   | 80 GB  | 2       | 305   | 0     | 0.84   |
| Seagate   | ST3750840AS        | 752 GB | 3       | 944   | 927   | 0.84   |
| Hitachi   | HTS545032B9A300    | 320 GB | 161     | 528   | 156   | 0.84   |
| WDC       | WD1600BEKT-60A25T1 | 160 GB | 5       | 372   | 6     | 0.83   |
| WDC       | WD2500BEKT-75PVMT1 | 250 GB | 4       | 1180  | 6     | 0.83   |
| Fujitsu   | MHZ2120BH G2       | 120 GB | 6       | 485   | 686   | 0.83   |
| Fujitsu   | MHY2160BH          | 160 GB | 30      | 398   | 218   | 0.83   |
| WDC       | WD10EZEX-07WN4A0   | 1 TB   | 12      | 353   | 1     | 0.83   |
| Seagate   | ST1750LM000 HN-... | 1.7 TB | 2       | 303   | 0     | 0.83   |
| Toshiba   | HDWL120            | 2 TB   | 33      | 315   | 1     | 0.83   |
| WDC       | WD15EARS-00Z5B1    | 1.5 TB | 40      | 1344  | 400   | 0.83   |
| Seagate   | ST500NM0011 81Y... | 500 GB | 2       | 2410  | 506   | 0.83   |
| Seagate   | ST250LT003-9YG14C  | 250 GB | 4       | 302   | 0     | 0.83   |
| WDC       | WD3200BPVT-00JJ5T0 | 320 GB | 21      | 536   | 166   | 0.83   |
| Samsung   | HD251HJ            | 250 GB | 12      | 708   | 122   | 0.83   |
| WDC       | WD5000BEVT-22A0RT0 | 500 GB | 68      | 668   | 101   | 0.83   |
| Seagate   | ST3250824A         | 250 GB | 5       | 646   | 203   | 0.83   |
| WDC       | WD800BB-00CAA1     | 80 GB  | 3       | 1103  | 132   | 0.82   |
| HGST      | HTS725032A7E630    | 320 GB | 49      | 519   | 244   | 0.82   |
| WDC       | WD2000JD-22HBB0    | 200 GB | 4       | 834   | 7     | 0.82   |
| WDC       | WD5000LPVX-22V0TT0 | 500 GB | 300     | 368   | 9     | 0.82   |
| WDC       | WD1600JS-60MHB5    | 160 GB | 5       | 752   | 18    | 0.82   |
| WDC       | WD5000AVCS-632DY1  | 500 GB | 22      | 401   | 5     | 0.82   |
| WDC       | WD600BEAS-22KZT0   | 64 GB  | 1       | 300   | 0     | 0.82   |
| WDC       | WD5000AAKX-00KJ3A0 | 500 GB | 2       | 416   | 4     | 0.82   |
| Toshiba   | MG05ACA800E        | 8 TB   | 2       | 300   | 0     | 0.82   |
| Toshiba   | HDWR180            | 8 TB   | 9       | 299   | 0     | 0.82   |
| WDC       | WD1600BPVT-00ZEST0 | 160 GB | 1       | 299   | 0     | 0.82   |
| Maxtor    | 7L320S0            | 323 GB | 1       | 299   | 0     | 0.82   |
| WDC       | WD62PURZ-74B3AY0   | 6 TB   | 1       | 299   | 0     | 0.82   |
| WDC       | WD3200AAJS-00L7A0  | 320 GB | 109     | 778   | 50    | 0.82   |
| WDC       | WD1600BPVT-22ZEST0 | 160 GB | 1       | 299   | 0     | 0.82   |
| Seagate   | ST1000DX002-2DV162 | 1 TB   | 38      | 306   | 3     | 0.82   |
| HP        | GB0160CAABV        | 160 GB | 1       | 299   | 0     | 0.82   |
| WDC       | WD60EZRZ-00RWYB1   | 6 TB   | 14      | 496   | 161   | 0.82   |
| Hitachi   | HTS721080G9AT00    | 80 GB  | 2       | 298   | 0     | 0.82   |
| Hitachi   | HDP725016GLA380    | 160 GB | 16      | 951   | 163   | 0.82   |
| Seagate   | ST9250410AS        | 250 GB | 80      | 534   | 226   | 0.82   |
| WDC       | WD10JPVX-60JC3T0   | 1 TB   | 93      | 411   | 124   | 0.82   |
| WDC       | WD10JPVX-11JC3T0   | 1 TB   | 3       | 297   | 0     | 0.82   |
| Seagate   | ST10000DM0004-1... | 10 TB  | 9       | 339   | 1     | 0.82   |
| Seagate   | ST1000LM024 HN-... | 1 TB   | 1085    | 439   | 48    | 0.81   |
| Hitachi   | HTS542580K9SA00    | 80 GB  | 22      | 444   | 3     | 0.81   |
| Seagate   | ST16000NM001G-2... | 16 TB  | 62      | 297   | 2     | 0.81   |
| Seagate   | ST750LM022 HN-M... | 752 GB | 149     | 423   | 35    | 0.81   |
| WDC       | WD2500AAJS-00L7A0  | 250 GB | 31      | 607   | 13    | 0.81   |
| WDC       | WD10JPVX-16JC3T3   | 1 TB   | 5       | 296   | 0     | 0.81   |
| WDC       | WD5000AVCS-732DY1  | 500 GB | 2       | 658   | 9     | 0.81   |
| Seagate   | ST500LM012 HN-M... | 500 GB | 382     | 430   | 37    | 0.81   |
| Maxtor    | STM3250620A        | 250 GB | 1       | 295   | 0     | 0.81   |
| Hitachi   | HDS723020BLA642... | 2 TB   | 1       | 295   | 0     | 0.81   |
| Toshiba   | HDWM110            | 1 TB   | 5       | 295   | 0     | 0.81   |
| WDC       | WD100PURZ-85W86Y0  | 10 TB  | 1       | 295   | 0     | 0.81   |
| Seagate   | ST380819AS         | 80 GB  | 6       | 658   | 685   | 0.81   |
| WDC       | WD1500HLFS-01G6U4  | 150 GB | 2       | 295   | 0     | 0.81   |
| Toshiba   | MQ03UBB300         | 3 TB   | 11      | 323   | 4     | 0.81   |
| WDC       | WD2500AAJS-00B4A0  | 250 GB | 23      | 794   | 45    | 0.81   |
| Seagate   | ST4000LM024-2AN17V | 4 TB   | 33      | 390   | 37    | 0.81   |
| WDC       | WD6400BPVT-00HXZT1 | 640 GB | 5       | 294   | 0     | 0.81   |
| WDC       | WD10JPCX-24UE4T0   | 1 TB   | 124     | 399   | 25    | 0.80   |
| WDC       | WD7501AALS-00E3A0  | 752 GB | 10      | 745   | 83    | 0.80   |
| HGST      | HTS541010A7E630    | 1 TB   | 60      | 402   | 188   | 0.80   |
| Seagate   | ST1000VX001-1HH162 | 1 TB   | 7       | 293   | 0     | 0.80   |
| Samsung   | SV1203N            | 120 GB | 2       | 441   | 3     | 0.80   |
| WDC       | WD800BB-00FJA0     | 80 GB  | 8       | 477   | 31    | 0.80   |
| WDC       | WD3200BEVT-75A23T0 | 320 GB | 7       | 632   | 42    | 0.80   |
| Maxtor    | 6V320F0            | 320 GB | 3       | 649   | 2     | 0.80   |
| Fujitsu   | MHW2080BH PL       | 80 GB  | 11      | 452   | 95    | 0.80   |
| WDC       | WD5000BMVW-11AMCS0 | 500 GB | 4       | 390   | 3     | 0.80   |
| WDC       | WD6400BPVT-60HXZT1 | 640 GB | 7       | 748   | 597   | 0.80   |
| WDC       | WD10TPVT-00U4RT1   | 1 TB   | 7       | 413   | 67    | 0.80   |
| WDC       | WD60EZRZ-22GZ5B1   | 6 TB   | 2       | 291   | 0     | 0.80   |
| Seagate   | ST9408114A         | 40 GB  | 1       | 291   | 0     | 0.80   |
| WDC       | WD1600AAJS-08L7A0  | 160 GB | 17      | 844   | 78    | 0.80   |
| Magnet... | MD02500-BJDW-RO    | 250 GB | 1       | 291   | 0     | 0.80   |
| WDC       | WD6400BPVT-80HXZT1 | 640 GB | 11      | 526   | 99    | 0.80   |
| WDC       | WD800BEVS-07RST0   | 80 GB  | 8       | 309   | 1     | 0.80   |
| Hitachi   | HDP725050GLAT80    | 500 GB | 3       | 825   | 2     | 0.79   |
| WDC       | WD1600BB-00GUC0    | 160 GB | 4       | 832   | 61    | 0.79   |
| Seagate   | ST2000LV000-2G2174 | 2 TB   | 1       | 289   | 0     | 0.79   |
| Seagate   | OOS2000G           | 2 TB   | 1       | 289   | 0     | 0.79   |
| WDC       | WD5000BPKX-60HPJT0 | 500 GB | 6       | 521   | 39    | 0.79   |
| Seagate   | ST380215A          | 80 GB  | 35      | 482   | 177   | 0.79   |
| Fujitsu   | MHZ2320BH G1       | 320 GB | 14      | 675   | 21    | 0.79   |
| Seagate   | ST31000525SV       | 1 TB   | 4       | 952   | 49    | 0.79   |
| Seagate   | ST3250820ACE       | 250 GB | 4       | 595   | 781   | 0.79   |
| WDC       | WD10EURX-83UY4Y0   | 1 TB   | 3       | 759   | 110   | 0.79   |
| WDC       | WD10EZRX-22A3KB0   | 1 TB   | 2       | 288   | 0     | 0.79   |
| Fujitsu   | MHV2100BH          | 100 GB | 6       | 611   | 19    | 0.79   |
| WDC       | WD40NMZW-59GX6S1   | 4 TB   | 4       | 288   | 0     | 0.79   |
| Hitachi   | HTS547550A9E384    | 500 GB | 211     | 513   | 319   | 0.79   |
| Toshiba   | MK3029GAC          | 32 GB  | 1       | 287   | 0     | 0.79   |
| WDC       | WD5000BMVV-11SXZS1 | 500 GB | 3       | 1103  | 4     | 0.79   |
| Samsung   | HM120JC            | 120 GB | 3       | 1075  | 38    | 0.79   |
| WDC       | WD7500BPVT-80HXZT3 | 752 GB | 22      | 409   | 16    | 0.79   |
| WDC       | WD40EZRZ-22GXCB0   | 4 TB   | 43      | 286   | 0     | 0.79   |
| WDC       | WD1200BEVT-22ZCT0  | 120 GB | 1       | 286   | 0     | 0.79   |
| WDC       | WD2000JS-60NCB1    | 200 GB | 3       | 399   | 4     | 0.79   |
| Hitachi   | HUS724040ALE641    | 4 TB   | 21      | 286   | 1     | 0.78   |
| WDC       | WD7500AYPS-01ZKB0  | 752 GB | 1       | 286   | 0     | 0.78   |
| WDC       | WD1200BEVS-75RST0  | 120 GB | 3       | 286   | 0     | 0.78   |
| WDC       | WD100EZAZ-11TDBA0  | 10 TB  | 20      | 286   | 0     | 0.78   |
| WDC       | WD5000AAKX-083CA0  | 500 GB | 2       | 285   | 0     | 0.78   |
| Seagate   | ST96812AS          | 64 GB  | 17      | 429   | 171   | 0.78   |
| WDC       | WD10EZEX-00MFCA0   | 1 TB   | 34      | 338   | 3     | 0.78   |
| WDC       | WD5000AAKS-22V1A0  | 500 GB | 21      | 1063  | 146   | 0.78   |
| Hitachi   | HTS545025B9A300    | 250 GB | 173     | 499   | 91    | 0.78   |
| WDC       | WD10PURX-64D85Y0   | 1 TB   | 6       | 616   | 3     | 0.78   |
| WDC       | WD5000AAVS-22G9B1  | 500 GB | 3       | 1103  | 8     | 0.78   |
| Seagate   | ST1000UM000-1EK164 | 1 TB   | 3       | 284   | 0     | 0.78   |
| Seagate   | ST1000LM014-1EJ164 | 1 TB   | 119     | 498   | 87    | 0.78   |
| WDC       | WD5000LPCX-24C6HT0 | 500 GB | 90      | 354   | 25    | 0.78   |
| WDC       | WD1600AAJB-00PVA0  | 160 GB | 12      | 631   | 156   | 0.78   |
| Toshiba   | MK2546GSX_200      | 200 GB | 3       | 464   | 388   | 0.78   |
| Hitachi   | HDS721032CLA662    | 320 GB | 1       | 283   | 0     | 0.78   |
| Toshiba   | DT01ACA050 LENOVO  | 500 GB | 4       | 282   | 0     | 0.78   |
| Seagate   | ST2000LX001-1RG174 | 2 TB   | 83      | 349   | 65    | 0.77   |
| WDC       | WD3009FYPX-09AAMB0 | 3 TB   | 1       | 2256  | 7     | 0.77   |
| WDC       | WD5000MPCK-22AWHT0 | 500 GB | 2       | 281   | 0     | 0.77   |
| WDC       | WD5000BPVT-55HXZT3 | 500 GB | 9       | 329   | 3     | 0.77   |
| HGST      | HTS545032A7E680    | 320 GB | 19      | 347   | 72    | 0.77   |
| WDC       | WD3200LPVT-08G33T1 | 320 GB | 6       | 327   | 2     | 0.77   |
| WDC       | WD5000AAKS-07A7B0  | 500 GB | 3       | 782   | 6     | 0.77   |
| WDC       | WD3200BPVT-22JJ5T0 | 320 GB | 175     | 348   | 51    | 0.77   |
| Seagate   | ST12000VN0008-2... | 12 TB  | 3       | 280   | 0     | 0.77   |
| WDC       | WD5000BPVT-35HXZT1 | 500 GB | 6       | 280   | 0     | 0.77   |
| WDC       | WD10SPCX-22HWST0   | 1 TB   | 3       | 280   | 0     | 0.77   |
| WDC       | WD800BEVS-22RST0   | 80 GB  | 31      | 405   | 49    | 0.77   |
| WDC       | WD20SDZW-11JJ8S0   | 2 TB   | 9       | 279   | 0     | 0.77   |
| WDC       | WD10PURZ-85U8XY0   | 1 TB   | 27      | 318   | 1     | 0.77   |
| Fujitsu   | MHW2100BH          | 100 GB | 1       | 279   | 0     | 0.76   |
| WDC       | WD1600BEVT-75ZCT1  | 160 GB | 1       | 279   | 0     | 0.76   |
| WDC       | WD6400BPVT-22HXZT3 | 640 GB | 13      | 586   | 121   | 0.76   |
| Hitachi   | HCC543216A7A380    | 160 GB | 2       | 278   | 0     | 0.76   |
| Seagate   | ST1000VX005-2EZ102 | 1 TB   | 16      | 278   | 0     | 0.76   |
| WDC       | WD1600AABS-00H4A0  | 160 GB | 4       | 721   | 6     | 0.76   |
| WDC       | WD100EB-00BHF0     | 10 GB  | 1       | 557   | 1     | 0.76   |
| Hitachi   | HTS547575A9E384    | 640 GB | 206     | 601   | 473   | 0.76   |
| WDC       | WD10J31X-00U3VT0   | 1 TB   | 2       | 278   | 0     | 0.76   |
| Seagate   | ST9500423AS        | 500 GB | 63      | 560   | 96    | 0.76   |
| Seagate   | ST3160021A         | 160 GB | 19      | 654   | 338   | 0.76   |
| WDC       | WD40EZRX-11SPEB0   | 4 TB   | 1       | 277   | 0     | 0.76   |
| WDC       | WD10EADS-22M2B0    | 1 TB   | 22      | 729   | 52    | 0.76   |
| WDC       | WD3200BPVT-55JJ5T0 | 320 GB | 7       | 424   | 140   | 0.76   |
| WDC       | WD3200BPVT-22ZEST0 | 320 GB | 73      | 417   | 58    | 0.76   |
| WDC       | WD5000LPVX-75V0TT0 | 500 GB | 58      | 347   | 2     | 0.75   |
| Seagate   | STM3320418AS       | 320 GB | 10      | 666   | 140   | 0.75   |
| Seagate   | ST94813AS          | 40 GB  | 3       | 347   | 68    | 0.75   |
| WDC       | WD3200LPVX-22V0TT0 | 320 GB | 25      | 309   | 1     | 0.75   |
| Toshiba   | MG06ACA800E        | 8 TB   | 11      | 274   | 0     | 0.75   |
| WDC       | WD3200AAKS-00V1A0  | 320 GB | 11      | 891   | 150   | 0.75   |
| WDC       | WD1600BEVT-60ZCT1  | 160 GB | 15      | 371   | 151   | 0.75   |
| Seagate   | ST3120213A         | 120 GB | 13      | 706   | 593   | 0.75   |
| Samsung   | HM320II            | 320 GB | 34      | 394   | 150   | 0.75   |
| WDC       | WD5000LPVT-00FMCT0 | 500 GB | 8       | 279   | 1     | 0.75   |
| Apple     | HDD ST1000LM024    | 1 TB   | 8       | 860   | 5     | 0.75   |
| Seagate   | ST9320310AS        | 320 GB | 13      | 529   | 478   | 0.75   |
| WDC       | WD5000BEVT-26A0RT0 | 500 GB | 7       | 674   | 107   | 0.75   |
| Hitachi   | HTS543216A7A384    | 160 GB | 7       | 548   | 23    | 0.75   |
| Seagate   | ST500DM009-2F110A  | 500 GB | 48      | 283   | 24    | 0.75   |
| WDC       | WD6400BEVT-80A0RT0 | 640 GB | 3       | 314   | 2     | 0.75   |
| Hitachi   | HTS541640J9SA00    | 40 GB  | 3       | 466   | 258   | 0.75   |
| Toshiba   | MG08ACA16TEY       | 16 TB  | 14      | 272   | 0     | 0.75   |
| Seagate   | ST8000NE001-2M7101 | 8 TB   | 7       | 363   | 12    | 0.75   |
| Toshiba   | MQ01ABD100         | 1 TB   | 800     | 384   | 114   | 0.74   |
| Seagate   | ST1000VX000-1ES162 | 1 TB   | 21      | 271   | 0     | 0.74   |
| Seagate   | ST320DM001 HD322GJ | 320 GB | 8       | 653   | 77    | 0.74   |
| WDC       | WD5000LPVX-80V0TT0 | 500 GB | 66      | 338   | 68    | 0.74   |
| Seagate   | ST3000VN007-2AH16M | 3 TB   | 6       | 270   | 0     | 0.74   |
| WDC       | WD3200AAJS-00RYA0  | 320 GB | 7       | 1086  | 95    | 0.74   |
| WDC       | WD3200JB-00KFA0    | 320 GB | 3       | 1330  | 8     | 0.74   |
| Seagate   | ST1000DM010-2EP102 | 1 TB   | 837     | 300   | 27    | 0.74   |
| Seagate   | ST1000NM0055-1V... | 1 TB   | 2       | 703   | 3     | 0.74   |
| Fujitsu   | MHZ2200BH G2       | 200 GB | 1       | 269   | 0     | 0.74   |
| Samsung   | HM321HI            | 320 GB | 140     | 445   | 89    | 0.74   |
| WDC       | WD5000LPLX-66ZNTT0 | 500 GB | 2       | 269   | 0     | 0.74   |
| Hitachi   | HCS5C1010DLE630    | 1 TB   | 2       | 269   | 0     | 0.74   |
| HGST      | HUS726T4TALA6L1    | 4 TB   | 11      | 269   | 0     | 0.74   |
| WDC       | WD1600BEVT-00A23T0 | 160 GB | 8       | 450   | 66    | 0.74   |
| WDC       | WD10EADS-65M2BX    | 1 TB   | 2       | 807   | 46    | 0.74   |
| WDC       | WD1200BEVS-07RST0  | 120 GB | 2       | 268   | 0     | 0.74   |
| WDC       | WD3200AAKX-073CA0  | 320 GB | 2       | 847   | 5     | 0.74   |
| Seagate   | ST2000DX001-SSH... | 2 TB   | 1       | 805   | 2     | 0.74   |
| Fujitsu   | MHV2080AH          | 80 GB  | 9       | 492   | 9     | 0.73   |
| HGST      | HTS725032A7E635... | 320 GB | 2       | 268   | 0     | 0.73   |
| Hitachi   | HDS721010DLE630    | 1 TB   | 61      | 820   | 725   | 0.73   |
| WDC       | WD2500AAJB-57R1A0  | 250 GB | 1       | 268   | 0     | 0.73   |
| Seagate   | ST3000DM001-9YN166 | 3 TB   | 42      | 922   | 904   | 0.73   |
| WDC       | WD30NMZW-11GX6S1   | 3 TB   | 9       | 279   | 1     | 0.73   |
| WDC       | WD5000AZLX-22JKKA0 | 500 GB | 23      | 319   | 1     | 0.73   |
| WDC       | WD1200JD-22HBB0    | 120 GB | 2       | 1602  | 5     | 0.73   |
| Hitachi   | HTS541075A9E680    | 752 GB | 9       | 417   | 454   | 0.73   |
| WDC       | WD121KRYZ-01W0RB0  | 12 TB  | 12      | 266   | 0     | 0.73   |
| Seagate   | ST500LM036-2LU17A  | 500 GB | 1       | 266   | 0     | 0.73   |
| Seagate   | ST9250414ASG       | 250 GB | 2       | 284   | 535   | 0.73   |
| MediaMax  | WL1000GSA3272C     | 1 TB   | 1       | 265   | 0     | 0.73   |
| WDC       | WD2500BEKT-00A25T0 | 250 GB | 1       | 264   | 0     | 0.73   |
| Hitachi   | HTS727575A9E364    | 752 GB | 36      | 798   | 274   | 0.73   |
| WDC       | WD2500AAKX-321CA0  | 250 GB | 1       | 264   | 0     | 0.72   |
| Seagate   | ST640LM001 HN-M... | 640 GB | 7       | 417   | 9     | 0.72   |
| WDC       | WD1600AAJS-22L7A0  | 160 GB | 21      | 659   | 14    | 0.72   |
| WDC       | WD5000BPVT-00HXZT1 | 500 GB | 21      | 432   | 85    | 0.72   |
| WDC       | WD2500BEKX-00B7WT0 | 250 GB | 2       | 263   | 0     | 0.72   |
| WDC       | WD10EZRX-00A3KB0   | 1 TB   | 4       | 387   | 15    | 0.72   |
| WDC       | WD5000LPVX-08V0TT6 | 500 GB | 2       | 263   | 0     | 0.72   |
| Fujitsu   | MHZ2320BH G2       | 320 GB | 25      | 492   | 317   | 0.72   |
| HGST      | HUS722T1TALA604    | 1 TB   | 24      | 262   | 0     | 0.72   |
| WDC       | WD5000AAKB-00H8A0  | 500 GB | 21      | 715   | 8     | 0.72   |
| WDC       | WD5000AZLX-00K2TA0 | 500 GB | 16      | 261   | 0     | 0.72   |
| Seagate   | ST9500420ASG       | 500 GB | 9       | 841   | 368   | 0.72   |
| Hitachi   | HTS723225A7A365... | 250 GB | 1       | 261   | 0     | 0.72   |
| Seagate   | ST320011A          | 20 GB  | 7       | 489   | 5     | 0.71   |
| WDC       | WD5000AZLX-08K2TA0 | 500 GB | 40      | 266   | 1     | 0.71   |
| WDC       | WD5000LPCX-22VHAT1 | 500 GB | 20      | 260   | 0     | 0.71   |
| Seagate   | ST9500325ASG       | 500 GB | 15      | 422   | 150   | 0.71   |
| WDC       | WD3200BPVT-24ZEST0 | 320 GB | 29      | 408   | 76    | 0.71   |
| IBM/Hi... | IC35L040AVVA07-0   | 41 GB  | 4       | 623   | 83    | 0.71   |
| Seagate   | ST1500LM012-1R817G | 1.5 TB | 5       | 259   | 0     | 0.71   |
| Samsung   | HN-M500MBB         | 500 GB | 58      | 416   | 33    | 0.71   |
| WDC       | WD5000BPVT-22HXZT1 | 500 GB | 38      | 563   | 92    | 0.71   |
| WDC       | WD3200BEVT-80A0RT0 | 320 GB | 48      | 451   | 55    | 0.71   |
| Seagate   | ST330013A          | 32 GB  | 1       | 259   | 0     | 0.71   |
| WDC       | WD3200BPVT-80JJ5T0 | 320 GB | 72      | 328   | 44    | 0.71   |
| WDC       | WD2500BEVS-60UST0  | 250 GB | 14      | 569   | 252   | 0.71   |
| Toshiba   | MK6459GSXP         | 640 GB | 16      | 638   | 544   | 0.71   |
| WDC       | WD1200BEVS-00UST0  | 120 GB | 5       | 270   | 1     | 0.71   |
| WDC       | WD7500BPVT-22HXZT1 | 752 GB | 9       | 874   | 242   | 0.71   |
| Seagate   | ST91208220AS       | 120 GB | 2       | 461   | 507   | 0.71   |
| WDC       | WD20EZAZ-00GGJB0   | 2 TB   | 69      | 258   | 0     | 0.71   |
| Maxtor    | 6V250F0            | 250 GB | 4       | 481   | 1     | 0.71   |
| Toshiba   | MQ01ABD100M        | 1 TB   | 18      | 294   | 13    | 0.71   |
| WDC       | WD5000BEVT-75ZAT0  | 500 GB | 3       | 322   | 4     | 0.70   |
| Seagate   | ST3160212ACE       | 160 GB | 4       | 539   | 27    | 0.70   |
| WDC       | WD2500AVJS-63B6A0  | 250 GB | 4       | 666   | 7     | 0.70   |
| WDC       | WD3200BEVT-08A23T1 | 320 GB | 14      | 511   | 109   | 0.70   |
| WDC       | WD40EFAX-68JH4N0   | 4 TB   | 25      | 280   | 1     | 0.70   |
| WDC       | WD5000LPVX-08V0TT2 | 500 GB | 4       | 314   | 2     | 0.70   |
| Fujitsu   | MHT2060BH          | 64 GB  | 3       | 411   | 683   | 0.70   |
| WDC       | WD2503ABYX-01WERA1 | 256 GB | 8       | 440   | 2     | 0.70   |
| Seagate   | ST2000LM015-2E8174 | 2 TB   | 157     | 302   | 53    | 0.69   |
| WDC       | WD3200BEKT-00F3T0  | 320 GB | 2       | 253   | 0     | 0.69   |
| HGST      | HTS541010A9E680    | 1 TB   | 376     | 472   | 425   | 0.69   |
| Hitachi   | HTS545016B9A300    | 160 GB | 69      | 412   | 89    | 0.69   |
| WDC       | WD5000AZLX-60K2TA0 | 500 GB | 27      | 293   | 77    | 0.69   |
| WDC       | WD7500AZEX-00BN5A0 | 752 GB | 1       | 252   | 0     | 0.69   |
| Toshiba   | HDWD110            | 1 TB   | 427     | 273   | 3     | 0.69   |
| WDC       | WD10SPZX-75Z10T1   | 1 TB   | 28      | 260   | 2     | 0.69   |
| Toshiba   | HDWR11A            | 10 TB  | 2       | 251   | 0     | 0.69   |
| WDC       | WD5000AAKX-003CA0  | 500 GB | 53      | 784   | 37    | 0.69   |
| Toshiba   | MQ01ACF050         | 500 GB | 97      | 349   | 61    | 0.69   |
| WDC       | WD10JPVX-55JC3T3   | 1 TB   | 3       | 602   | 343   | 0.69   |
| WDC       | WD5000LPLX-75ZNTT0 | 500 GB | 27      | 269   | 88    | 0.68   |
| WDC       | WD2500BJKT-75F4T0  | 250 GB | 2       | 428   | 4     | 0.68   |
| WDC       | WD50NMZW-59LG6S1   | 5 TB   | 2       | 249   | 0     | 0.68   |
| WDC       | WD3200BEKT-75PVMT0 | 320 GB | 6       | 669   | 8     | 0.68   |
| Seagate   | ST14000NM0018-2... | 14 TB  | 2       | 265   | 24    | 0.68   |
| Seagate   | ST380211AS         | 80 GB  | 12      | 610   | 549   | 0.68   |
| WDC       | WD8001FZBX-00ASYA0 | 8 TB   | 2       | 248   | 0     | 0.68   |
| Seagate   | ST9320328CS        | 320 GB | 15      | 658   | 140   | 0.68   |
| Toshiba   | MQ04UBB400         | 4 TB   | 43      | 258   | 7     | 0.68   |
| WDC       | WD3200BEVT-60ZCT0  | 320 GB | 7       | 536   | 41    | 0.68   |
| Toshiba   | MQ01ABD050V        | 500 GB | 18      | 354   | 304   | 0.68   |
| Seagate   | ST1000VN002-2EY102 | 1 TB   | 14      | 264   | 70    | 0.68   |
| WDC       | WD2000JS-00MHB1    | 200 GB | 1       | 246   | 0     | 0.68   |
| WDC       | WD5000BEVT-22ZAT0  | 500 GB | 33      | 559   | 155   | 0.68   |
| Hitachi   | HCT721016SLA380    | 160 GB | 3       | 246   | 0     | 0.67   |
| Fujitsu   | MJA2500BH FFS G1   | 500 GB | 1       | 246   | 0     | 0.67   |
| WDC       | WD2500BEKT-75A25T0 | 250 GB | 11      | 551   | 36    | 0.67   |
| Quantum   | FIREBALLlct20 30   | 32 GB  | 1       | 1477  | 5     | 0.67   |
| Seagate   | ST4000NM0165       | 4 TB   | 3       | 246   | 0     | 0.67   |
| Seagate   | ST500LM000-1EJ162  | 500 GB | 133     | 386   | 62    | 0.67   |
| WDC       | WD3000HLHX-01JJPV0 | 304 GB | 4       | 671   | 3     | 0.67   |
| WDC       | WD5000LPLX-21ZNTT0 | 500 GB | 4       | 278   | 274   | 0.67   |
| Toshiba   | MK1656GSY          | 160 GB | 7       | 305   | 4     | 0.67   |
| Hitachi   | HTS721010G9SA00    | 100 GB | 7       | 1056  | 176   | 0.67   |
| Samsung   | HD250HJ            | 250 GB | 58      | 869   | 653   | 0.67   |
| WDC       | WD5000BPVT-75HXZT3 | 500 GB | 21      | 446   | 3     | 0.67   |
| WDC       | WD5000BEVT-00ZAT0  | 500 GB | 8       | 442   | 149   | 0.67   |
| WDC       | WD400UE-22HCT0     | 40 GB  | 1       | 732   | 2     | 0.67   |
| WDC       | WD5000BEVT-11A0RT0 | 500 GB | 1       | 243   | 0     | 0.67   |
| Fujitsu   | MHV2120BH          | 120 GB | 3       | 371   | 3     | 0.67   |
| Hitachi   | HTS722020K9A300    | 200 GB | 2       | 434   | 11    | 0.67   |
| Hitachi   | HTS545032A7E380    | 320 GB | 38      | 426   | 207   | 0.67   |
| Toshiba   | MQ01ABF032         | 320 GB | 51      | 339   | 77    | 0.67   |
| WDC       | WD10JPVT-08A1YT2   | 1 TB   | 13      | 516   | 34    | 0.67   |
| WDC       | WD10SPCX-24HWST1   | 1 TB   | 48      | 304   | 39    | 0.66   |
| Samsung   | HM251HI            | 250 GB | 10      | 309   | 2     | 0.66   |
| WDC       | WD3000JD-55KLB0    | 304 GB | 1       | 969   | 3     | 0.66   |
| Toshiba   | MK6475GSX          | 640 GB | 47      | 431   | 253   | 0.66   |
| WDC       | WD2500BEVT-24A23T0 | 250 GB | 28      | 479   | 79    | 0.66   |
| Apple     | HDD HTS547550A9... | 500 GB | 12      | 376   | 18    | 0.66   |
| WDC       | WD5000LMVW-11VEDS2 | 500 GB | 1       | 1208  | 4     | 0.66   |
| Fujitsu   | MHW2080AT          | 80 GB  | 1       | 241   | 0     | 0.66   |
| Seagate   | ST10000VN0008-2... | 10 TB  | 3       | 241   | 0     | 0.66   |
| WDC       | WD4000LPCX-24C6HT0 | 400 GB | 1       | 241   | 0     | 0.66   |
| WDC       | WD140EDFZ-11A0VA0  | 14 TB  | 44      | 251   | 1     | 0.66   |
| Samsung   | HM250HI            | 250 GB | 103     | 360   | 35    | 0.66   |
| WDC       | WD40NDZW-11MR8S1   | 4 TB   | 27      | 247   | 27    | 0.66   |
| WDC       | WD7500BPVT-08HXZT3 | 752 GB | 6       | 516   | 13    | 0.66   |
| WDC       | WD50EFRX-68MYMN1   | 5 TB   | 7       | 1655  | 172   | 0.66   |
| Seagate   | ST9160823AS        | 160 GB | 10      | 718   | 436   | 0.66   |
| China     | OOS250G            | 250 GB | 1       | 239   | 0     | 0.66   |
| WDC       | WD1600BEVT-00ZCT0  | 160 GB | 8       | 262   | 1     | 0.66   |
| Seagate   | ST9160411ASG       | 160 GB | 5       | 536   | 2     | 0.66   |
| Fujitsu   | MHW2160BH PL       | 160 GB | 16      | 583   | 210   | 0.65   |
| WDC       | WD2500AAKX-07U6AA1 | 250 GB | 2       | 239   | 0     | 0.65   |
| Seagate   | ST4000VX000-2AG166 | 4 TB   | 4       | 629   | 4     | 0.65   |
| Toshiba   | MG04ACA200N        | 2 TB   | 2       | 237   | 0     | 0.65   |
| Hitachi   | HTS545025B9SA00    | 250 GB | 4       | 237   | 0     | 0.65   |
| WDC       | WD1600AAJS-62B4A0  | 160 GB | 1       | 237   | 0     | 0.65   |
| Seagate   | ST1000VM002-9ZL162 | 1 TB   | 3       | 516   | 733   | 0.65   |
| WDC       | WD1000CHTZ-04JCPV0 | 1 TB   | 2       | 236   | 0     | 0.65   |
| Seagate   | ST3120813AS        | 120 GB | 29      | 871   | 551   | 0.65   |
| Toshiba   | MQ01ABD032         | 320 GB | 115     | 375   | 173   | 0.65   |
| WDC       | WD3200AVVS-63L2B0  | 320 GB | 13      | 539   | 78    | 0.65   |
| Toshiba   | MK1665GSX H        | 160 GB | 4       | 388   | 3     | 0.65   |
| WDC       | WD101EFBX-68B0AN0  | 10 TB  | 16      | 235   | 0     | 0.65   |
| WDC       | WD40NDZW-11MR8S0   | 4 TB   | 3       | 235   | 0     | 0.64   |
| Seagate   | ST500LM011 HM501II | 500 GB | 2       | 277   | 1     | 0.64   |
| Toshiba   | MK6465GSXN         | 640 GB | 9       | 456   | 180   | 0.64   |
| WDC       | WD3200BEKT-75KA9T0 | 320 GB | 1       | 234   | 0     | 0.64   |
| MediaMax  | WL250GSA1672       | 250 GB | 1       | 2109  | 8     | 0.64   |
| Seagate   | ST500LM000-1EJ1... | 500 GB | 23      | 275   | 17    | 0.64   |
| WDC       | WD5003ABYX-23 0... | 500 GB | 1       | 234   | 0     | 0.64   |
| HGST      | HCC545050A7E380    | 500 GB | 8       | 563   | 44    | 0.64   |
| WDC       | WD3200BPVT-55ZEST0 | 320 GB | 5       | 355   | 28    | 0.64   |
| WDC       | WD3200BEVT-00A0RT0 | 320 GB | 30      | 323   | 10    | 0.64   |
| WDC       | WD5000AADS-67S9B0  | 500 GB | 1       | 2104  | 8     | 0.64   |
| Toshiba   | MK7559GSXF         | 752 GB | 11      | 415   | 218   | 0.64   |
| WDC       | WD6400BPVT-26HXZT1 | 640 GB | 1       | 232   | 0     | 0.64   |
| WDC       | WD5000LPVT-00G33T0 | 500 GB | 7       | 556   | 3     | 0.64   |
| Toshiba   | MK3276GSX -63      | 320 GB | 9       | 426   | 62    | 0.63   |
| WDC       | WD1200BEVS-08UST0  | 120 GB | 1       | 230   | 0     | 0.63   |
| WDC       | WD3200AAJS-65B4A0  | 320 GB | 4       | 1069  | 39    | 0.63   |
| WDC       | WD161KRYZ-01AGBB0  | 16 TB  | 2       | 230   | 0     | 0.63   |
| Seagate   | ST360014A          | 64 GB  | 4       | 584   | 12    | 0.63   |
| Maxtor    | STM3802110A        | 80 GB  | 2       | 404   | 512   | 0.63   |
| HGST      | HUH721212ALE604    | 12 TB  | 10      | 230   | 0     | 0.63   |
| Toshiba   | Generic L200 Ha... | 2 TB   | 2       | 229   | 0     | 0.63   |
| Hitachi   | HTS543225A7A384    | 250 GB | 47      | 363   | 312   | 0.63   |
| WDC       | WD15NMVW-11AV3S2   | 1.5 TB | 7       | 468   | 5     | 0.63   |
| WDC       | WD800BB-98JHC0     | 80 GB  | 1       | 1829  | 7     | 0.63   |
| Seagate   | ST340016A          | 40 GB  | 40      | 695   | 30    | 0.63   |
| HGST      | HTS725050A7E630    | 500 GB | 292     | 484   | 303   | 0.62   |
| WDC       | WD5000LPCX-00VHAT0 | 500 GB | 49      | 260   | 1     | 0.62   |
| WDC       | WD4000FYYZ-01UL1B0 | 4 TB   | 3       | 1746  | 9     | 0.62   |
| WDC       | WD10SPZX-17Z10T0   | 1 TB   | 9       | 258   | 49    | 0.62   |
| WDC       | WD20SDZW-11Z3CS1   | 2 TB   | 1       | 226   | 0     | 0.62   |
| WDC       | WD5000BEKT-80KA9T1 | 500 GB | 4       | 280   | 1     | 0.62   |
| WDC       | WD7500BPKX-00HPJT0 | 752 GB | 18      | 330   | 50    | 0.62   |
| Fujitsu   | MHW2120BJ G2       | 120 GB | 2       | 319   | 1     | 0.62   |
| WDC       | WD5000LPCX-22VHAT0 | 500 GB | 39      | 233   | 1     | 0.62   |
| WDC       | WD30NDZW-11A8JS0   | 3 TB   | 1       | 225   | 0     | 0.62   |
| Samsung   | HD200HJ            | 200 GB | 20      | 898   | 621   | 0.62   |
| Toshiba   | MK5076GSXN         | 500 GB | 1       | 224   | 0     | 0.62   |
| WDC       | WD1600BEKT-00A25T0 | 160 GB | 1       | 224   | 0     | 0.61   |
| Toshiba   | MK8034GSX          | 80 GB  | 15      | 479   | 23    | 0.61   |
| Seagate   | ST3120211AS        | 120 GB | 5       | 517   | 12    | 0.61   |
| WDC       | WD15EARS-22MVWB0   | 1.5 TB | 7       | 626   | 221   | 0.61   |
| WDC       | WD2500AAJS-65M0A0  | 250 GB | 3       | 665   | 13    | 0.61   |
| WDC       | WD40EZAZ-19SF3B0   | 4 TB   | 2       | 223   | 0     | 0.61   |
| WDC       | WD1600JS-60NCB1    | 160 GB | 6       | 530   | 54    | 0.61   |
| Seagate   | ST10000NM0086-2... | 10 TB  | 12      | 436   | 16    | 0.61   |
| WDC       | WD5000BPVT-22A1YT0 | 500 GB | 13      | 223   | 0     | 0.61   |
| WDC       | WD800BB-56JKC0     | 80 GB  | 8       | 730   | 8     | 0.61   |
| WDC       | WD20EARS-60MVWB0   | 2 TB   | 6       | 993   | 785   | 0.61   |
| Seagate   | ST9640320AS        | 640 GB | 24      | 584   | 309   | 0.61   |
| Toshiba   | MK3261GSYD         | 320 GB | 2       | 222   | 0     | 0.61   |
| Hitachi   | HTS543216L9SA00    | 160 GB | 32      | 485   | 47    | 0.61   |
| WDC       | WD50NDZW-11MR8S1   | 5 TB   | 23      | 256   | 1     | 0.61   |
| Toshiba   | MQ04UBD200         | 2 TB   | 68      | 224   | 2     | 0.61   |
| WDC       | WD5000AZLX-00JKKA0 | 500 GB | 15      | 264   | 38    | 0.61   |
| Seagate   | ST9750423AS        | 752 GB | 21      | 546   | 218   | 0.61   |
| Fujitsu   | MHW2120BJ FFS G2   | 120 GB | 1       | 221   | 0     | 0.61   |
| WDC       | WD1600BEKT-60F3T1  | 160 GB | 1       | 221   | 0     | 0.61   |
| WDC       | WD5000BPVT-55A1YT0 | 500 GB | 2       | 221   | 0     | 0.61   |
| Seagate   | ST8000AS0003-2H... | 8 TB   | 5       | 272   | 2     | 0.61   |
| WDC       | WD10SPZX-22Z10T0   | 1 TB   | 30      | 234   | 2     | 0.61   |
| WDC       | WD5000AZRZ-00HTKB0 | 500 GB | 24      | 288   | 47    | 0.60   |
| Seagate   | ST9500530NS        | 500 GB | 3       | 1402  | 99    | 0.60   |
| Toshiba   | DT01ABA300V        | 3 TB   | 1       | 220   | 0     | 0.60   |
| WDC       | WD800BB-00FRA0     | 80 GB  | 5       | 670   | 10    | 0.60   |
| WDC       | WD5000AAKS-00V6A0  | 500 GB | 8       | 811   | 9     | 0.60   |
| WDC       | WD2500BPVT-24JJ5T0 | 250 GB | 6       | 219   | 0     | 0.60   |
| Seagate   | ST1000LM014-SSH... | 1 TB   | 48      | 409   | 202   | 0.60   |
| Seagate   | ST9160412AS        | 160 GB | 29      | 500   | 395   | 0.60   |
| WDC       | WD3200AAKX-073CA1  | 320 GB | 3       | 358   | 3     | 0.60   |
| HGST      | HTS541010B7E610    | 1 TB   | 80      | 232   | 2     | 0.60   |
| Seagate   | ST8000VN004-2M2101 | 8 TB   | 36      | 234   | 1     | 0.60   |
| Samsung   | SP2014N            | 200 GB | 9       | 1023  | 201   | 0.60   |
| WDC       | WD20EURX-63T0FY0   | 2 TB   | 15      | 417   | 138   | 0.60   |
| Toshiba   | HDWT140            | 4 TB   | 3       | 218   | 0     | 0.60   |
| WDC       | WD5000LPCX-16VHAT1 | 500 GB | 2       | 218   | 0     | 0.60   |
| Fujitsu   | MHY2120BH          | 120 GB | 47      | 475   | 158   | 0.60   |
| WDC       | WD3200LPVX-75V0TT0 | 320 GB | 8       | 253   | 1     | 0.60   |
| Toshiba   | MQ01ABD100V        | 1 TB   | 11      | 330   | 5     | 0.60   |
| WDC       | WD20NPVT-00Z2TT0   | 2 TB   | 3       | 336   | 12    | 0.60   |
| WDC       | WD7500BPVT-60HXZT3 | 752 GB | 15      | 515   | 163   | 0.60   |
| WDC       | WD5000BEVT-60A0RT0 | 500 GB | 6       | 565   | 306   | 0.60   |
| WDC       | WD1600JB-00GVC0    | 160 GB | 2       | 777   | 3     | 0.59   |
| Hitachi   | HTS543216L9A300    | 160 GB | 70      | 512   | 174   | 0.59   |
| WDC       | WD5002AALX-32Z3A0  | 500 GB | 2       | 647   | 1     | 0.59   |
| WDC       | WD6400AAKS-00H2B0  | 640 GB | 2       | 955   | 1011  | 0.59   |
| WDC       | WD800BB-55JKC0     | 80 GB  | 10      | 635   | 98    | 0.59   |
| Hitachi   | HTS542516K9A300    | 160 GB | 9       | 723   | 154   | 0.59   |
| WDC       | WD20EADS-42R6B0    | 2 TB   | 1       | 215   | 0     | 0.59   |
| WDC       | WD3200AZDX-00SC2B0 | 320 GB | 2       | 379   | 440   | 0.59   |
| Hitachi   | HTS721080G9SA00    | 80 GB  | 9       | 437   | 30    | 0.59   |
| WDC       | WD20SPZX-21UA7T0   | 2 TB   | 3       | 214   | 0     | 0.59   |
| WDC       | WD3200AAJS-61B4A0  | 320 GB | 3       | 307   | 6     | 0.59   |
| WDC       | WD5000BPVT-55HXZT4 | 500 GB | 1       | 214   | 0     | 0.59   |
| WDC       | WD5000AZLX-21K2TA0 | 500 GB | 15      | 213   | 0     | 0.59   |
| Hitachi   | HDS721050DLE630    | 500 GB | 64      | 538   | 443   | 0.59   |
| WDC       | WD20SPZX-75UA7T0   | 2 TB   | 5       | 213   | 0     | 0.58   |
| WDC       | WD5000LPLX-60ZNTT0 | 500 GB | 2       | 213   | 0     | 0.58   |
| Fujitsu   | MPE3084AE          | 8 GB   | 1       | 213   | 0     | 0.58   |
| Seagate   | ST2000LM007-1R8174 | 2 TB   | 203     | 263   | 100   | 0.58   |
| WDC       | WD10SPCX-60KHST0   | 1 TB   | 5       | 433   | 10    | 0.58   |
| WDC       | WD5000BMVW-11AJGS4 | 500 GB | 11      | 213   | 52    | 0.58   |
| Seagate   | ST95005620AS       | 500 GB | 26      | 685   | 127   | 0.58   |
| Toshiba   | MQ01ABF050         | 500 GB | 668     | 285   | 97    | 0.58   |
| WDC       | WD1600AAJB-22WRA0  | 160 GB | 3       | 531   | 2     | 0.58   |
| WDC       | WD5000LPCX-21VHAT0 | 500 GB | 101     | 224   | 1     | 0.58   |
| HGST      | HEJ423232H9E300    | 320 GB | 1       | 211   | 0     | 0.58   |
| WDC       | WD3200BEKX-00B7WT0 | 320 GB | 8       | 213   | 2     | 0.58   |
| Toshiba   | MK2561GSYN         | 250 GB | 14      | 212   | 99    | 0.58   |
| Seagate   | ST3750528AS        | 752 GB | 54      | 864   | 403   | 0.58   |
| WDC       | WD120EDAZ-11F3RA0  | 12 TB  | 19      | 210   | 0     | 0.58   |
| Toshiba   | MK1059GSMP         | 1 TB   | 24      | 512   | 445   | 0.58   |
| WDC       | WD2005FBYZ-01YCBB3 | 2 TB   | 6       | 210   | 0     | 0.58   |
| Hitachi   | HTS542516K9SA00    | 160 GB | 85      | 655   | 195   | 0.58   |
| Toshiba   | DT01ABA100         | 1 TB   | 1       | 209   | 0     | 0.57   |
| Seagate   | ST9160412ASG       | 160 GB | 4       | 389   | 3     | 0.57   |
| Fujitsu   | MHX2300BT          | 304 GB | 5       | 742   | 154   | 0.57   |
| Seagate   | ST4000VX007-2DT166 | 4 TB   | 23      | 271   | 60    | 0.57   |
| WDC       | WD2500BEVT-00ZCT0  | 250 GB | 14      | 257   | 19    | 0.57   |
| WDC       | WD5000BEKT-80KA9T0 | 500 GB | 3       | 317   | 1     | 0.57   |
| Maxtor    | STM3500630AS       | 500 GB | 2       | 243   | 73    | 0.57   |
| WDC       | WD800BEVS-00RST0   | 80 GB  | 3       | 277   | 1     | 0.57   |
| WDC       | WD10EADS-65M2B1    | 1 TB   | 9       | 1076  | 114   | 0.57   |
| IBM/Hi... | IC35L040AVVN07-0   | 41 GB  | 2       | 576   | 3     | 0.57   |
| WDC       | WD400BB-00FJA0     | 40 GB  | 2       | 699   | 222   | 0.57   |
| Seagate   | ST32500NSSUN250G   | 250 GB | 1       | 1455  | 6     | 0.57   |
| Fujitsu   | MHV2040AT          | 40 GB  | 3       | 207   | 0     | 0.57   |
| HGST      | HTE725050A7E630    | 500 GB | 3       | 207   | 0     | 0.57   |
| Hitachi   | HTS541660J9SA00    | 64 GB  | 7       | 427   | 4     | 0.57   |
| Fujitsu   | MHT2080AT PL       | 80 GB  | 1       | 207   | 0     | 0.57   |
| Hitachi   | HTS722010K9SA00    | 100 GB | 8       | 713   | 9     | 0.57   |
| WDC       | WD140EDGZ-11B2DA2  | 14 TB  | 4       | 206   | 0     | 0.57   |
| WDC       | WD2500BEVT-22A23T0 | 250 GB | 82      | 406   | 50    | 0.57   |
| WDC       | WD5000AAKX-08ANVA0 | 500 GB | 4       | 241   | 2     | 0.56   |
| Toshiba   | MK2555GSXF         | 250 GB | 12      | 205   | 0     | 0.56   |
| Samsung   | HD120IJ            | 120 GB | 28      | 793   | 359   | 0.56   |
| WDC       | WD1200JB-00GVC0    | 120 GB | 3       | 539   | 4     | 0.56   |
| Toshiba   | MK2552GSX          | 250 GB | 30      | 782   | 227   | 0.56   |
| Seagate   | ST12000VN0008-2... | 12 TB  | 6       | 204   | 0     | 0.56   |
| WDC       | WD5000AVDS-61U7B1  | 500 GB | 2       | 1303  | 6     | 0.56   |
| WDC       | WD20SMZW-11YFCS0   | 2 TB   | 8       | 204   | 0     | 0.56   |
| WDC       | WD800AAJS-60M0A0   | 80 GB  | 2       | 1294  | 30    | 0.56   |
| Hitachi   | HTS547564A9E384    | 640 GB | 74      | 512   | 455   | 0.56   |
| Samsung   | HD082GJ            | 80 GB  | 25      | 488   | 382   | 0.56   |
| Samsung   | HD320KJ            | 320 GB | 9       | 988   | 268   | 0.56   |
| Hitachi   | HTS545016B9SA00    | 160 GB | 5       | 221   | 1     | 0.56   |
| WDC       | WD6400BEVT-22A0RT0 | 640 GB | 22      | 461   | 32    | 0.56   |
| WDC       | RFT030VQHF-KRM5P7  | 3 TB   | 2       | 203   | 0     | 0.56   |
| WDC       | WD1600AVVS-63L2B0  | 160 GB | 11      | 596   | 4     | 0.56   |
| Maxtor    | 6L040J2            | 40 GB  | 2       | 1365  | 6     | 0.56   |
| WDC       | WD20PURX-64PFUY0   | 2 TB   | 3       | 203   | 0     | 0.56   |
| Toshiba   | MK6006GAH          | 64 GB  | 2       | 203   | 0     | 0.56   |
| WDC       | WD3200BEVT-22A23T0 | 320 GB | 59      | 476   | 89    | 0.56   |
| WDC       | WD181KRYZ-01AGBB0  | 18 TB  | 4       | 203   | 0     | 0.56   |
| WDC       | WD10JPVX-60JC3T1   | 1 TB   | 58      | 264   | 39    | 0.56   |
| Seagate   | ST1000LX015-1U7172 | 1 TB   | 143     | 264   | 65    | 0.56   |
| WDC       | WD1003FBYX-50Y7B0  | 1 TB   | 1       | 202   | 0     | 0.56   |
| Seagate   | ST9120822AS        | 120 GB | 65      | 453   | 483   | 0.56   |
| WDC       | WD5000LPLX-00ZNTT0 | 500 GB | 72      | 248   | 15    | 0.55   |
| Seagate   | ST2000DM008-2FR102 | 2 TB   | 620     | 226   | 44    | 0.55   |
| Seagate   | ST9250827AS        | 250 GB | 65      | 540   | 430   | 0.55   |
| WDC       | WD2500AAJS-60Z0A0  | 250 GB | 6       | 690   | 171   | 0.55   |
| Toshiba   | HDWR160            | 6 TB   | 7       | 201   | 0     | 0.55   |
| WDC       | WD800JD-00JNC0     | 80 GB  | 4       | 451   | 16    | 0.55   |
| Toshiba   | HDWD105            | 500 GB | 118     | 235   | 20    | 0.55   |
| WDC       | WD2500BPVT-26JJ5T0 | 250 GB | 2       | 201   | 0     | 0.55   |
| Seagate   | ST9160827AS        | 160 GB | 43      | 505   | 358   | 0.55   |
| WDC       | WD10SPCX-21KHST0   | 1 TB   | 6       | 200   | 0     | 0.55   |
| WDC       | WD10SPZX-00Z10T0   | 1 TB   | 49      | 200   | 0     | 0.55   |
| Seagate   | ST500LT015-1DJ142  | 500 GB | 2       | 200   | 0     | 0.55   |
| WDC       | WD3200LPCX-24C6HT0 | 320 GB | 29      | 239   | 1     | 0.55   |
| Seagate   | ST6000VN0001-1S... | 6 TB   | 1       | 200   | 0     | 0.55   |
| WDC       | WD740GD-00FLC0     | 74 GB  | 1       | 1202  | 5     | 0.55   |
| HGST      | HUS726T4TALA6L4    | 4 TB   | 10      | 200   | 0     | 0.55   |
| WDC       | WD1600BEVS-60RST0  | 160 GB | 12      | 487   | 231   | 0.55   |
| Toshiba   | MK6034GAX          | 64 GB  | 4       | 663   | 352   | 0.55   |
| WDC       | WD3200BEKT-60KA9T0 | 320 GB | 3       | 456   | 690   | 0.55   |
| Seagate   | ST14000NM001G-2... | 14 TB  | 21      | 198   | 0     | 0.54   |
| WDC       | WD15NMVW-11EDZS6   | 1.5 TB | 2       | 198   | 0     | 0.54   |
| Seagate   | ST1000LM048-2E7172 | 1 TB   | 269     | 240   | 83    | 0.54   |
| WDC       | WD7500BPVX-16JC3T0 | 752 GB | 1       | 197   | 0     | 0.54   |
| WDC       | WD20SMZW-59YFCS1   | 2 TB   | 2       | 197   | 0     | 0.54   |
| WDC       | WD5000AARS-003BB1  | 500 GB | 5       | 568   | 7     | 0.54   |
| WDC       | WD1600BEVT-08A23T1 | 160 GB | 3       | 197   | 0     | 0.54   |
| WDC       | WD82PURZ-85TEUY0   | 8 TB   | 10      | 197   | 0     | 0.54   |
| HGST      | HUS722T1TALA600    | 1 TB   | 4       | 197   | 0     | 0.54   |
| WDC       | WD20SMZW-11JW8S0   | 2 TB   | 13      | 196   | 0     | 0.54   |
| WDC       | WD5000AAKX-221CA0  | 500 GB | 3       | 778   | 6     | 0.54   |
| Hitachi   | HTS722080K9A300    | 80 GB  | 5       | 426   | 3     | 0.54   |
| Samsung   | SP2504C            | 250 GB | 68      | 1101  | 740   | 0.54   |
| Quantum   | FIREBALLlct15 30   | 32 GB  | 1       | 391   | 1     | 0.54   |
| Hitachi   | HDS721612PLAT80    | 128 GB | 1       | 1366  | 6     | 0.53   |
| Hitachi   | HTS723216A7A364    | 160 GB | 2       | 359   | 512   | 0.53   |
| Toshiba   | MK6034GSX          | 64 GB  | 4       | 423   | 18    | 0.53   |
| Seagate   | ST94011A           | 40 GB  | 1       | 194   | 0     | 0.53   |
| WDC       | WD3200BEKT-60V5T1  | 320 GB | 41      | 481   | 325   | 0.53   |
| Toshiba   | MK7575GSX          | 752 GB | 40      | 700   | 674   | 0.53   |
| Fujitsu   | MHW2080BJ G2       | 80 GB  | 2       | 362   | 66    | 0.53   |
| Seagate   | ST320414A          | 20 GB  | 1       | 194   | 0     | 0.53   |
| WDC       | WD50NMZW-59A8NS1   | 5 TB   | 7       | 194   | 0     | 0.53   |
| Hitachi   | HTS725050A7E630    | 500 GB | 23      | 426   | 551   | 0.53   |
| Seagate   | ST9120823AS        | 120 GB | 3       | 546   | 345   | 0.53   |
| Toshiba   | MQ01ABC150         | 1.5 TB | 4       | 263   | 272   | 0.53   |
| Seagate   | ST940210AS         | 40 GB  | 4       | 268   | 1     | 0.53   |
| IBM       | DARA-212000        | 12 GB  | 1       | 193   | 0     | 0.53   |
| HGST      | HTS545050A7E380    | 500 GB | 264     | 430   | 314   | 0.53   |
| Seagate   | ST9160823ASG       | 160 GB | 6       | 299   | 170   | 0.53   |
| WDC       | WD5000LMVW-11VEDS0 | 500 GB | 3       | 193   | 0     | 0.53   |
| WDC       | WD3200LPVX-08V0TT5 | 320 GB | 4       | 204   | 1     | 0.53   |
| WDC       | WD400BB-00DKA0     | 40 GB  | 1       | 193   | 0     | 0.53   |
| WDC       | WD800BEVS-75RST0   | 80 GB  | 4       | 381   | 252   | 0.53   |
| WDC       | WD1600AAJS-60Z0A0  | 160 GB | 6       | 306   | 175   | 0.53   |
| Hitachi   | HTS542525K9SA00    | 250 GB | 59      | 604   | 114   | 0.53   |
| Toshiba   | MQ04UBF100         | 1 TB   | 86      | 217   | 2     | 0.53   |
| Hitachi   | HTS543212L9SA02    | 120 GB | 2       | 192   | 0     | 0.53   |
| Samsung   | HM100UI            | 1 TB   | 5       | 191   | 0     | 0.53   |
| WDC       | WD60EFZX-68B3FN0   | 6 TB   | 17      | 199   | 1     | 0.52   |
| Toshiba   | HDWN160            | 6 TB   | 11      | 317   | 16    | 0.52   |
| Toshiba   | MK3263GSX          | 320 GB | 16      | 661   | 98    | 0.52   |
| WDC       | WD6400BPVT-75HXZT3 | 640 GB | 3       | 347   | 3     | 0.52   |
| WDC       | WD1600BJKT-75F4T0  | 160 GB | 10      | 586   | 10    | 0.52   |
| Toshiba   | DT01ACA100 LENOVO  | 1 TB   | 10      | 190   | 0     | 0.52   |
| WDC       | WD740GD-00FLA0     | 74 GB  | 2       | 2375  | 56    | 0.52   |
| Samsung   | HD161HJ 41R0186LEN | 160 GB | 2       | 551   | 507   | 0.52   |
| WDC       | WD5000BPVT-26HXZT3 | 500 GB | 1       | 190   | 0     | 0.52   |
| Seagate   | ST250LM004 HN-M... | 250 GB | 10      | 279   | 5     | 0.52   |
| WDC       | WD7500BPVX-16JC3T3 | 752 GB | 1       | 379   | 1     | 0.52   |
| WDC       | WD5000AAKS-08V0A0  | 500 GB | 12      | 621   | 25    | 0.52   |
| WDC       | WD5000KMVW-11ZSMS5 | 500 GB | 1       | 189   | 0     | 0.52   |
| WDC       | WD1001FALS-40Y6A0  | 1 TB   | 1       | 1698  | 8     | 0.52   |
| WDC       | WD3200BPVT-00ZEST0 | 320 GB | 5       | 265   | 2     | 0.52   |
| Seagate   | ST9500420AS        | 500 GB | 157     | 645   | 572   | 0.51   |
| Samsung   | SP1213C            | 120 GB | 11      | 749   | 24    | 0.51   |
| WDC       | WD2500BJKT-00F4T0  | 250 GB | 2       | 187   | 0     | 0.51   |
| WDC       | WD40NPZZ-00PDPT0   | 4 TB   | 4       | 187   | 0     | 0.51   |
| WDC       | WD30NMVW-11C3NS2   | 3 TB   | 5       | 749   | 274   | 0.51   |
| WDC       | WD5000LPCX-08VHA   | 500 GB | 6       | 187   | 0     | 0.51   |
| Seagate   | ST1000LM035-1RK172 | 1 TB   | 1004    | 241   | 138   | 0.51   |
| Toshiba   | MG08ACA14TE        | 14 TB  | 4       | 186   | 0     | 0.51   |
| WDC       | WD40PURX-64N96Y0   | 4 TB   | 3       | 285   | 1     | 0.51   |
| WDC       | WD30EZRX-19DC0B0   | 3 TB   | 1       | 186   | 0     | 0.51   |
| WDC       | WD2500BEVT-00A23T0 | 250 GB | 14      | 430   | 8     | 0.51   |
| Toshiba   | MK8037GSX          | 80 GB  | 23      | 458   | 115   | 0.51   |
| Hitachi   | HTS543232A7A384    | 320 GB | 271     | 363   | 311   | 0.51   |
| WDC       | WD20EFAX-68FB5N0   | 2 TB   | 19      | 186   | 0     | 0.51   |
| MediaMax  | WL3000GSA6454      | 3.7 TB | 1       | 186   | 0     | 0.51   |
| Toshiba   | HDWL110            | 1 TB   | 33      | 204   | 12    | 0.51   |
| Maxtor    | STM380811AS        | 80 GB  | 7       | 435   | 349   | 0.51   |
| WDC       | WD5000LPLX-60ZNTT1 | 500 GB | 31      | 259   | 57    | 0.51   |
| Toshiba   | MD05ACA800         | 8 TB   | 2       | 185   | 0     | 0.51   |
| Seagate   | ST10000VN0008-2... | 10 TB  | 6       | 185   | 0     | 0.51   |
| WDC       | WD800BEVT-22ZCT0   | 80 GB  | 3       | 240   | 1     | 0.51   |
| Toshiba   | MQ01ABD050         | 500 GB | 241     | 388   | 232   | 0.51   |
| WDC       | WD5000LPCX-75VHAT0 | 500 GB | 24      | 184   | 0     | 0.51   |
| Seagate   | ST2000LM005 HN-... | 2 TB   | 17      | 184   | 0     | 0.51   |
| Fujitsu   | MHZ2080BH G1       | 80 GB  | 6       | 184   | 0     | 0.51   |
| Hitachi   | HTS723232L9SA60    | 320 GB | 5       | 404   | 20    | 0.50   |
| HGST      | HUS728T8TALE6L4    | 8 TB   | 24      | 186   | 2     | 0.50   |
| WDC       | WD1200BB-00GUC0    | 120 GB | 3       | 939   | 9     | 0.50   |
| Quantum   | FIREBALLlct15 15   | 16 GB  | 1       | 183   | 0     | 0.50   |
| Seagate   | ST500LT012-1DG142  | 500 GB | 744     | 306   | 109   | 0.50   |
| WDC       | WD5000LPSX-60A6WT0 | 500 GB | 1       | 182   | 0     | 0.50   |
| WDC       | WD4003FFBX-68MU3N0 | 4 TB   | 10      | 182   | 0     | 0.50   |
| WDC       | WD50NDZW-11A8JS1   | 5 TB   | 28      | 182   | 0     | 0.50   |
| WDC       | WD1600BEVT-22A23T0 | 160 GB | 38      | 317   | 4     | 0.50   |
| WDC       | WD800JD-60MSA1     | 80 GB  | 2       | 405   | 2     | 0.50   |
| WDC       | WD1000CHTZ-04JCPV1 | 1 TB   | 1       | 181   | 0     | 0.50   |
| WDC       | WD10SPZX-75Z10T2   | 1 TB   | 52      | 183   | 1     | 0.50   |
| Seagate   | ST9200420ASG       | 200 GB | 5       | 371   | 54    | 0.50   |
| WDC       | WD2500JD-00HBC0    | 250 GB | 2       | 1972  | 14    | 0.50   |
| Fujitsu   | MHZ2500BT G1       | 500 GB | 2       | 1426  | 6     | 0.50   |
| IBM/Hi... | IC25N030ATMR04-0   | 32 GB  | 1       | 544   | 2     | 0.50   |
| WDC       | WD140EMFZ-11A0WA0  | 14 TB  | 15      | 208   | 1     | 0.50   |
| Seagate   | ST9320423AS        | 320 GB | 96      | 453   | 354   | 0.50   |
| WDC       | WD6000BLHX-01V7BV0 | 600 GB | 2       | 181   | 0     | 0.50   |
| WDC       | WD10EADS-114BB1    | 1 TB   | 3       | 1281  | 669   | 0.50   |
| Seagate   | ST160NM0011 39M... | 160 GB | 1       | 361   | 1     | 0.50   |
| Seagate   | ST160NM0011 39M... | 160 GB | 1       | 361   | 1     | 0.50   |
| WDC       | WD5000AUDX-73H9TY0 | 500 GB | 1       | 180   | 0     | 0.50   |
| WDC       | WD30EZRZ-22Z5HB0   | 3 TB   | 5       | 180   | 0     | 0.50   |
| Toshiba   | MK2035GSS          | 200 GB | 24      | 517   | 32    | 0.49   |
| WDC       | WD1200JB-00FUA0    | 120 GB | 1       | 180   | 0     | 0.49   |
| WDC       | WD5000BPKX-22HPJT0 | 500 GB | 19      | 270   | 24    | 0.49   |
| WDC       | WD10EURX-73FH1Y0   | 1 TB   | 8       | 466   | 2     | 0.49   |
| Samsung   | SP1613N            | 160 GB | 2       | 858   | 508   | 0.49   |
| Toshiba   | HDWD260            | 6 TB   | 9       | 189   | 1     | 0.49   |
| Seagate   | ST500LX012-1LM1... | 500 GB | 3       | 495   | 161   | 0.49   |
| Seagate   | ST2000DM005-2CW102 | 2 TB   | 27      | 179   | 0     | 0.49   |
| Hitachi   | HTS543232L9SA02    | 320 GB | 5       | 1029  | 19    | 0.49   |
| Samsung   | HE753LJ            | 752 GB | 2       | 374   | 51    | 0.49   |
| Hitachi   | HTS421240H9AT00    | 40 GB  | 2       | 179   | 0     | 0.49   |
| WDC       | WD5000AAKS-60Z1A0  | 500 GB | 8       | 1180  | 116   | 0.49   |
| Seagate   | ST500LM021-1KJ152  | 500 GB | 174     | 400   | 381   | 0.49   |
| WDC       | WD3200BPVT-80ZEST0 | 320 GB | 43      | 350   | 73    | 0.49   |
| Seagate   | ST10000DM0004-2... | 10 TB  | 6       | 177   | 0     | 0.49   |
| Toshiba   | MG08ADA600E        | 6 TB   | 3       | 177   | 0     | 0.49   |
| WDC       | WD1600BEVT-24A23T0 | 160 GB | 14      | 230   | 2     | 0.49   |
| Samsung   | SP0812C            | 80 GB  | 25      | 597   | 197   | 0.49   |
| WDC       | WD3201ABYS-01B9A0  | 320 GB | 3       | 1408  | 188   | 0.49   |
| WDC       | WD5000AAKS-60WWPA0 | 500 GB | 10      | 795   | 484   | 0.49   |
| WDC       | WD3200BEVT-75ZCT0  | 320 GB | 3       | 671   | 57    | 0.49   |
| WDC       | WD1600JD-00HBB0    | 160 GB | 8       | 513   | 13    | 0.49   |
| WDC       | WD10SPCX-08HWST0   | 1 TB   | 1       | 177   | 0     | 0.49   |
| Seagate   | ST3402111A         | 40 GB  | 4       | 359   | 809   | 0.49   |
| WDC       | WD40EMRX-82UZ0N0   | 4 TB   | 7       | 187   | 1     | 0.48   |
| WDC       | WD20NMVW-11AV3S4   | 2 TB   | 5       | 738   | 206   | 0.48   |
| WDC       | WD3200AAJS-60M0A1  | 320 GB | 6       | 816   | 804   | 0.48   |
| Toshiba   | MK8009GAH          | 80 GB  | 5       | 520   | 21    | 0.48   |
| WDC       | WD10SPCX-11HWST0   | 1 TB   | 1       | 351   | 1     | 0.48   |
| WDC       | WD5000BEVT-00A0RT0 | 500 GB | 17      | 433   | 137   | 0.48   |
| Toshiba   | MK2576GSX          | 250 GB | 8       | 272   | 2     | 0.48   |
| Samsung   | HM080HC            | 72 GB  | 1       | 526   | 2     | 0.48   |
| Seagate   | ST980210AS         | 80 GB  | 1       | 175   | 0     | 0.48   |
| WDC       | WD3200LPVX-60V0TT0 | 320 GB | 2       | 175   | 0     | 0.48   |
| Hitachi   | HTS723232A7A364    | 320 GB | 88      | 529   | 536   | 0.48   |
| Apple     | HDD TOSHIBA MK5... | 500 GB | 6       | 256   | 69    | 0.48   |
| WDC       | WD600UE-22KVT0     | 64 GB  | 2       | 271   | 2     | 0.48   |
| WDC       | WD40NDZW-11A8JS1   | 4 TB   | 20      | 174   | 0     | 0.48   |
| WDC       | WD10SPCX-16HWST0   | 1 TB   | 1       | 173   | 0     | 0.48   |
| Toshiba   | MK3259GSXP         | 320 GB | 69      | 431   | 250   | 0.48   |
| Seagate   | ST1500DM003-9YN16G | 1.5 TB | 21      | 559   | 382   | 0.48   |
| WDC       | WD2001FASS-00U0B0  | 2 TB   | 3       | 1465  | 419   | 0.47   |
| Hitachi   | HDS722512VLAT20    | 128 GB | 1       | 863   | 4     | 0.47   |
| Toshiba   | MK1629GSG          | 160 GB | 4       | 372   | 26    | 0.47   |
| ASMedia   | ASMT106x_ V0Safe   | 320 GB | 1       | 172   | 0     | 0.47   |
| WDC       | WD10TMVW-11ZSMS1   | 1 TB   | 3       | 374   | 2     | 0.47   |
| Hitachi   | HTS541080G9SA00    | 80 GB  | 10      | 410   | 66    | 0.47   |
| WDC       | WD1600BEVT-88ZCT0  | 160 GB | 2       | 171   | 0     | 0.47   |
| Toshiba   | MK3275GSX          | 320 GB | 36      | 495   | 297   | 0.47   |
| WDC       | WD3200BEVT-24A23T0 | 320 GB | 15      | 506   | 70    | 0.47   |
| Samsung   | HD252KJ            | 250 GB | 12      | 774   | 432   | 0.47   |
| WDC       | WD60EFAX-68JH4N1   | 6 TB   | 10      | 193   | 1     | 0.47   |
| Toshiba   | MK1646GSX          | 160 GB | 16      | 701   | 267   | 0.47   |
| WDC       | WD10SDZM-59ZKVS0   | 1 TB   | 2       | 170   | 0     | 0.47   |
| Toshiba   | MK1633GSG          | 160 GB | 9       | 277   | 128   | 0.47   |
| Toshiba   | HDWJ110            | 1 TB   | 15      | 281   | 149   | 0.47   |
| WDC       | WD5000BEKT-60KA9T0 | 500 GB | 9       | 384   | 35    | 0.47   |
| Hitachi   | HDS722525VLAT80    | 250 GB | 2       | 2632  | 8     | 0.47   |
| Seagate   | ST320LT009-9WC142  | 320 GB | 5       | 224   | 1     | 0.46   |
| Seagate   | ST3250312CS        | 250 GB | 15      | 393   | 170   | 0.46   |
| Toshiba   | MK1059GSM          | 1 TB   | 42      | 614   | 812   | 0.46   |
| Seagate   | ST1000DM000-9TS15E | 1 TB   | 3       | 587   | 336   | 0.46   |
| WDC       | WD2500BEVT-75A23T0 | 250 GB | 17      | 413   | 54    | 0.46   |
| Toshiba   | MK6459GSX          | 640 GB | 7       | 460   | 495   | 0.46   |
| Toshiba   | MK6461GSY          | 640 GB | 5       | 205   | 245   | 0.46   |
| Seagate   | ST3400832A         | 400 GB | 1       | 2186  | 12    | 0.46   |
| Seagate   | ST12000DM0007-2... | 12 TB  | 4       | 175   | 1     | 0.46   |
| WDC       | WD10SPZX-24Z10T0   | 1 TB   | 62      | 230   | 22    | 0.46   |
| Toshiba   | MQ04ABF100V -63    | 1 TB   | 1       | 167   | 0     | 0.46   |
| WDC       | WD2500LPCX-24C6HT0 | 250 GB | 47      | 216   | 69    | 0.46   |
| Seagate   | ST940815A          | 40 GB  | 1       | 167   | 0     | 0.46   |
| WDC       | WD2500AAKS-00B3A0  | 250 GB | 9       | 850   | 227   | 0.46   |
| Hitachi   | HTS541612J9SA00 3H | 120 GB | 2       | 558   | 93    | 0.46   |
| WDC       | WD5000MPCK-60AWHT0 | 500 GB | 1       | 166   | 0     | 0.46   |
| Seagate   | ST3250820NS        | 250 GB | 2       | 695   | 1050  | 0.46   |
| Samsung   | HN-M101MBB         | 1 TB   | 31      | 379   | 181   | 0.46   |
| WDC       | WD3200LPVT-00FMCT0 | 320 GB | 3       | 476   | 3     | 0.46   |
| WDC       | WD3200BPVT-60JJ5T0 | 320 GB | 12      | 345   | 99    | 0.46   |
| WDC       | WD20EARS-00J99B0   | 2 TB   | 4       | 503   | 732   | 0.45   |
| WDC       | WD2005FBYZ-01YCBB1 | 2 TB   | 2       | 165   | 0     | 0.45   |
| Seagate   | ST9100824A         | 100 GB | 1       | 165   | 0     | 0.45   |
| WDC       | WD800BEVE-00A0HT0  | 80 GB  | 1       | 165   | 0     | 0.45   |
| WDC       | WD2500BPVT-22ZEST0 | 250 GB | 21      | 201   | 3     | 0.45   |
| Fujitsu   | MJA2500BH G1       | 500 GB | 2       | 390   | 4     | 0.45   |
| Seagate   | ST3160812AS 41N... | 160 GB | 5       | 760   | 106   | 0.45   |
| WDC       | WD20SPZX-08UA7     | 2 TB   | 9       | 165   | 0     | 0.45   |
| WDC       | WD10EARX-00PASB0   | 1 TB   | 6       | 566   | 13    | 0.45   |
| WDC       | WD20EURX-57T0FY0   | 2 TB   | 1       | 164   | 0     | 0.45   |
| Hitachi   | HTS541616J9SA00    | 160 GB | 50      | 530   | 60    | 0.45   |
| Toshiba   | MG04ACA200E        | 2 TB   | 5       | 169   | 2     | 0.45   |
| WDC       | WD2500BEVT-60ZCT1  | 250 GB | 17      | 448   | 222   | 0.45   |
| WDC       | WD5000BPVT-60HXZT3 | 500 GB | 14      | 452   | 112   | 0.45   |
| Samsung   | HD155UI            | 1.5 TB | 3       | 1164  | 599   | 0.45   |
| WDC       | WD10SPZX-21Z10T0   | 1 TB   | 194     | 176   | 8     | 0.45   |
| IBM/Hi... | IC35L120AVV207-1   | 128 GB | 2       | 496   | 9     | 0.45   |
| WDC       | WD5000AAKS-00H2B0  | 500 GB | 2       | 1469  | 8     | 0.45   |
| Seagate   | ST5000AS0011-1L... | 5 TB   | 2       | 1033  | 508   | 0.45   |
| Seagate   | ST980811AS         | 80 GB  | 55      | 369   | 329   | 0.45   |
| WDC       | WD6400BEVT-60A0RT0 | 640 GB | 6       | 342   | 38    | 0.45   |
| Seagate   | ST3400820AS        | 400 GB | 2       | 961   | 503   | 0.44   |
| Seagate   | ST920217AS         | 20 GB  | 1       | 162   | 0     | 0.44   |
| Fujitsu   | MJA2500BH G2       | 500 GB | 13      | 370   | 92    | 0.44   |
| Hitachi   | HTS543225L9A300    | 250 GB | 55      | 544   | 285   | 0.44   |
| Toshiba   | MK8007GAH          | 80 GB  | 2       | 210   | 7     | 0.44   |
| HGST      | HTS541075A9E680    | 752 GB | 83      | 440   | 605   | 0.44   |
| Toshiba   | MK1655GSX          | 160 GB | 21      | 368   | 60    | 0.44   |
| WDC       | WD3200JD-60KLB0    | 320 GB | 1       | 965   | 5     | 0.44   |
| Seagate   | ST500LX025-1U717D  | 500 GB | 11      | 167   | 36    | 0.44   |
| WDC       | WD10SPCX-80HWST0   | 1 TB   | 1       | 160   | 0     | 0.44   |
| Hitachi   | HTS725016A9A362    | 160 GB | 2       | 290   | 1     | 0.44   |
| Toshiba   | MK1246GSX          | 120 GB | 21      | 463   | 67    | 0.44   |
| WDC       | WD1005FBYZ-01YCBB3 | 1 TB   | 3       | 160   | 0     | 0.44   |
| WDC       | WD1600AAJB-00J3A0  | 160 GB | 18      | 558   | 119   | 0.44   |
| Fujitsu   | MHZ2250BS G2       | 250 GB | 1       | 159   | 0     | 0.44   |
| WDC       | WD10EZEX-60WN4A1   | 1 TB   | 42      | 174   | 7     | 0.44   |
| WDC       | WD6400BEVT-80A0RT1 | 640 GB | 2       | 479   | 13    | 0.44   |
| WDC       | WD400BB-23FJA0     | 40 GB  | 1       | 796   | 4     | 0.44   |
| Toshiba   | MG06ACA10TE        | 10 TB  | 4       | 159   | 0     | 0.44   |
| WDC       | WD140EDGZ-11B1PA0  | 14 TB  | 19      | 159   | 0     | 0.44   |
| WDC       | WD20EZWX-60F5KA0   | 2 TB   | 1       | 159   | 0     | 0.44   |
| Fujitsu   | MHZ2120BH G1       | 120 GB | 1       | 794   | 4     | 0.44   |
| WDC       | WD1600BEVT-80A23T0 | 160 GB | 29      | 223   | 88    | 0.43   |
| HGST      | HUS728T8TALE6L0    | 8 TB   | 9       | 158   | 0     | 0.43   |
| Samsung   | HN-M750MBB         | 752 GB | 10      | 375   | 6     | 0.43   |
| Toshiba   | MK5059GUXP         | 500 GB | 1       | 157   | 0     | 0.43   |
| WDC       | WD10PURX-78E5EY0   | 1 TB   | 1       | 157   | 0     | 0.43   |
| Seagate   | ST1000LM049-2GH172 | 1 TB   | 246     | 188   | 64    | 0.43   |
| HGST      | HTS545050A7E660    | 500 GB | 21      | 302   | 68    | 0.43   |
| Seagate   | ST98823AS          | 80 GB  | 17      | 400   | 504   | 0.43   |
| WDC       | WD3200BEVT-26A23T0 | 320 GB | 3       | 274   | 73    | 0.43   |
| WDC       | WD-WD3200BVVT-6... | 320 GB | 1       | 157   | 0     | 0.43   |
| Seagate   | ST9320325AS        | 320 GB | 364     | 481   | 422   | 0.43   |
| Seagate   | ST910021AS         | 100 GB | 7       | 582   | 469   | 0.43   |
| WDC       | WD5000M22K-24Z1... | 500 GB | 2       | 596   | 10    | 0.43   |
| Toshiba   | MK3276GSXN         | 320 GB | 1       | 156   | 0     | 0.43   |
| Hitachi   | HTS545025B9SA02    | 250 GB | 28      | 268   | 151   | 0.43   |
| WDC       | WD80EDAZ-11TA3A0   | 8 TB   | 13      | 156   | 0     | 0.43   |
| Toshiba   | MK3265GSX          | 320 GB | 85      | 587   | 229   | 0.43   |
| WDC       | WD10SPZX-35Z10T0   | 1 TB   | 11      | 155   | 0     | 0.43   |
| Fujitsu   | MHZ2250BH G2       | 250 GB | 21      | 537   | 662   | 0.43   |
| Seagate   | ST5000LM000-2U8170 | 5 TB   | 4       | 155   | 0     | 0.43   |
| WDC       | WD20SPZX-22UA7T0   | 2 TB   | 36      | 155   | 0     | 0.43   |
| WDC       | WD2500AAKS-60B3A0  | 250 GB | 1       | 155   | 0     | 0.43   |
| WDC       | WD5000LPVX-00V0TT0 | 500 GB | 36      | 209   | 72    | 0.42   |
| WDC       | WD20SDRW-11VUUS0   | 2 TB   | 51      | 161   | 21    | 0.42   |
| Toshiba   | MK1252GSX          | 120 GB | 17      | 401   | 111   | 0.42   |
| WDC       | WD1200JD-55HBB0    | 120 GB | 1       | 923   | 5     | 0.42   |
| Samsung   | SV0412H            | 40 GB  | 6       | 1055  | 104   | 0.42   |
| WDC       | WD60EZAZ-00SF3B0   | 6 TB   | 15      | 153   | 0     | 0.42   |
| Hitachi   | HTS541010A9E680    | 1 TB   | 26      | 552   | 721   | 0.42   |
| WDC       | WD5000LPCX-24VHAT0 | 500 GB | 131     | 164   | 34    | 0.42   |
| Hitachi   | HTS545032B9A302    | 320 GB | 12      | 315   | 227   | 0.42   |
| Toshiba   | MQ03ABB300         | 3 TB   | 2       | 152   | 0     | 0.42   |
| WDC       | WD8004FRYZ-01VAEB0 | 8 TB   | 10      | 152   | 0     | 0.42   |
| Hitachi   | HTS545050A7E380    | 500 GB | 189     | 393   | 306   | 0.42   |
| WDC       | WD10SPZX-80Z10T1   | 1 TB   | 2       | 152   | 0     | 0.42   |
| WDC       | WD10EARX-00NYB0    | 1 TB   | 1       | 151   | 0     | 0.42   |
| MediaMax  | WL2000GSA1672 0    | 2 TB   | 1       | 151   | 0     | 0.42   |
| Samsung   | HD080HJ-P          | 80 GB  | 16      | 880   | 380   | 0.42   |
| Samsung   | HM500JJ            | 500 GB | 6       | 369   | 161   | 0.42   |
| Toshiba   | MK4058GSX          | 400 GB | 8       | 930   | 10    | 0.41   |
| Samsung   | HN-M320MBB         | 320 GB | 5       | 347   | 7     | 0.41   |
| HGST      | HTS541050A9E680    | 500 GB | 6       | 151   | 0     | 0.41   |
| WDC       | WD2500BEKT-60A25T1 | 250 GB | 15      | 601   | 234   | 0.41   |
| Samsung   | SP2004C            | 200 GB | 37      | 793   | 588   | 0.41   |
| WDC       | WD3200AAKS-22L6A0  | 320 GB | 5       | 534   | 5     | 0.41   |
| WDC       | WD10SPCX-60HWST0   | 1 TB   | 2       | 558   | 2     | 0.41   |
| Toshiba   | MQ01ABF050M        | 500 GB | 15      | 206   | 68    | 0.41   |
| Toshiba   | HDWR480            | 8 TB   | 2       | 150   | 0     | 0.41   |
| Seagate   | ST9160821A         | 160 GB | 5       | 414   | 15    | 0.41   |
| Samsung   | HM250JI            | 250 GB | 12      | 446   | 132   | 0.41   |
| Hitachi   | HDS721010KLA33R... | 1 TB   | 1       | 3734  | 24    | 0.41   |
| Seagate   | ST500LT032-1E9142  | 500 GB | 9       | 200   | 4     | 0.41   |
| Samsung   | SP1634N            | 160 GB | 1       | 298   | 1     | 0.41   |
| Hitachi   | HTS723225L9SA62    | 250 GB | 1       | 595   | 3     | 0.41   |
| Toshiba   | MK4009GAL          | 40 GB  | 2       | 151   | 5     | 0.41   |
| WDC       | WD10TMVW-11ZSMS4   | 1 TB   | 8       | 500   | 5     | 0.41   |
| WDC       | WD20SDRW-34VUUS0   | 2 TB   | 4       | 148   | 0     | 0.41   |
| Samsung   | SP1614C            | 160 GB | 12      | 591   | 13    | 0.41   |
| Fujitsu   | MHV2060AT          | 64 GB  | 2       | 528   | 4     | 0.41   |
| Toshiba   | MQ04ABF100         | 1 TB   | 530     | 168   | 54    | 0.41   |
| Toshiba   | MK3265GSXN         | 320 GB | 27      | 470   | 355   | 0.41   |
| WDC       | WD2500JS-60MHB1    | 250 GB | 2       | 350   | 8     | 0.41   |
| WDC       | WD1200JS-22NCB1    | 120 GB | 1       | 1184  | 7     | 0.41   |
| WDC       | WD5000AVVS-63H0B1  | 500 GB | 7       | 914   | 6     | 0.41   |
| Hitachi   | HTS542512K9SA00    | 120 GB | 89      | 448   | 109   | 0.40   |
| MediaMax  | WL1000GSA6472B     | 1 TB   | 2       | 770   | 4     | 0.40   |
| WDC       | WD10EZEX-07M2NA1   | 1 TB   | 2       | 476   | 164   | 0.40   |
| Seagate   | ST3320820SCE       | 320 GB | 2       | 233   | 560   | 0.40   |
| WDC       | WD1200BEVS-60UST0  | 120 GB | 17      | 472   | 343   | 0.40   |
| Seagate   | ST750LM030-1KKG62  | 752 GB | 2       | 146   | 0     | 0.40   |
| WDC       | WD2500BEVT-00A0RT1 | 245 GB | 1       | 146   | 0     | 0.40   |
| WDC       | WD2500BPVT-75JJ5T0 | 250 GB | 7       | 348   | 3     | 0.40   |
| Seagate   | ST94811A           | 40 GB  | 6       | 188   | 1     | 0.40   |
| WDC       | WD5000LPLX-08ZNTT0 | 500 GB | 72      | 166   | 1     | 0.40   |
| Fujitsu   | MHZ2160BH FFS G1   | 160 GB | 208     | 166   | 1     | 0.40   |
| MediaMax  | WL320GLSA854G      | 320 GB | 1       | 146   | 0     | 0.40   |
| Hitachi   | HTS545050KTA300    | 500 GB | 6       | 520   | 5     | 0.40   |
| WDC       | WD5000AAVS-00N7B0  | 500 GB | 2       | 405   | 1     | 0.40   |
| WDC       | WD101FZBX-00ATAA0  | 10 TB  | 2       | 145   | 0     | 0.40   |
| MediaMax  | WL3000GSA6472E 1   | 3 TB   | 1       | 144   | 0     | 0.40   |
| Fujitsu   | MHV2060BHPL        | 64 GB  | 1       | 144   | 0     | 0.40   |
| WDC       | WD10SPCX-00HWST0   | 1 TB   | 2       | 144   | 0     | 0.40   |
| Toshiba   | MK5076GSX -63      | 500 GB | 2       | 144   | 0     | 0.40   |
| WDC       | WD2500BEVT-80A23T0 | 250 GB | 29      | 315   | 43    | 0.39   |
| MARSHAL   | MAL2500HSA-T54L    | 500 GB | 1       | 143   | 0     | 0.39   |
| Seagate   | ST3200822A         | 200 GB | 9       | 1218  | 9     | 0.39   |
| WDC       | WD3200AAJS-55VWA0  | 320 GB | 1       | 1006  | 6     | 0.39   |
| Seagate   | ST96023AS          | 64 GB  | 2       | 395   | 5     | 0.39   |
| WDC       | WD30EZRS-11J99B1   | 3 TB   | 3       | 832   | 230   | 0.39   |
| Hitachi   | HTS541680J9SA00    | 80 GB  | 81      | 503   | 68    | 0.39   |
| HP        | MB2000GCWLT        | 2 TB   | 2       | 1504  | 505   | 0.39   |
| WDC       | WD3200AAKX-32ERMA0 | 320 GB | 1       | 142   | 0     | 0.39   |
| Hitachi   | HTS725032A9A364    | 320 GB | 47      | 541   | 690   | 0.39   |
| Hitachi   | HTS542560K9SA00    | 64 GB  | 4       | 409   | 9     | 0.39   |
| WDC       | WD6400BEVT-00A0RT0 | 640 GB | 5       | 534   | 98    | 0.39   |
| Seagate   | ST3320820A         | 320 GB | 2       | 461   | 105   | 0.39   |
| Seagate   | ST3500412AS        | 500 GB | 29      | 800   | 454   | 0.39   |
| Hitachi   | HTS541212H9AT00    | 120 GB | 3       | 438   | 5     | 0.39   |
| Hitachi   | HTS543232L9A300    | 320 GB | 44      | 605   | 397   | 0.39   |
| IBM       | DTLA-305020        | 20 GB  | 2       | 1494  | 37    | 0.39   |
| Seagate   | ST96812A           | 64 GB  | 4       | 302   | 1123  | 0.39   |
| WDC       | WD7500BPVT-00HXZT0 | 752 GB | 1       | 141   | 0     | 0.39   |
| WDC       | WD800AAJS-00M0A0   | 80 GB  | 1       | 141   | 0     | 0.39   |
| Seagate   | ST500LM030-2E717D  | 500 GB | 71      | 159   | 65    | 0.39   |
| Samsung   | SP2514N            | 250 GB | 13      | 819   | 494   | 0.39   |
| WDC       | WD2500AAJB-57WGA0  | 250 GB | 1       | 140   | 0     | 0.38   |
| Toshiba   | MK5059GSXP         | 500 GB | 53      | 415   | 376   | 0.38   |
| WDC       | WD10JMVW-59AJGS2   | 1 TB   | 1       | 140   | 0     | 0.38   |
| WDC       | WD800BB-00HEA0     | 80 GB  | 1       | 840   | 5     | 0.38   |
| Toshiba   | MK2565GSX          | 250 GB | 36      | 442   | 140   | 0.38   |
| WDC       | WD2500AAJS-07B4A0  | 250 GB | 2       | 1695  | 198   | 0.38   |
| WDC       | WD5000LMVW-11VEDS3 | 500 GB | 6       | 209   | 183   | 0.38   |
| WDC       | WD400EB-11CPF0     | 40 GB  | 2       | 1019  | 31    | 0.38   |
| Seagate   | OOS4000G           | 4 TB   | 1       | 139   | 0     | 0.38   |
| Seagate   | ST4000DX005-3GH101 | 4 TB   | 1       | 139   | 0     | 0.38   |
| WDC       | WUH721414ALE604    | 14 TB  | 6       | 141   | 3     | 0.38   |
| WDC       | WD3200BEVT-00ZAT0  | 320 GB | 4       | 203   | 7     | 0.38   |
| Hitachi   | HUA722010CLA330... | 1 TB   | 1       | 2081  | 14    | 0.38   |
| HP        | GB0750C8047        | 752 GB | 1       | 138   | 0     | 0.38   |
| WDC       | WD60PURZ-85ZUFY1   | 6 TB   | 7       | 138   | 0     | 0.38   |
| Samsung   | SP0822N            | 80 GB  | 10      | 138   | 1     | 0.38   |
| WDC       | WD84PURZ-85B2YY0   | 8 TB   | 2       | 137   | 0     | 0.38   |
| Seagate   | ST3160815SV        | 160 GB | 6       | 704   | 1035  | 0.38   |
| Toshiba   | MK3255GSX          | 320 GB | 2       | 282   | 4     | 0.38   |
| WDC       | WD50EZRZ-00GZ5B1   | 5 TB   | 5       | 137   | 0     | 0.38   |
| WDC       | WD5000BPVT-08HXZT1 | 500 GB | 3       | 549   | 2     | 0.38   |
| Seagate   | ST320LT007-9ZV142  | 320 GB | 82      | 497   | 635   | 0.38   |
| WDC       | WD120EFAX-68UNTN0  | 12 TB  | 3       | 136   | 0     | 0.37   |
| Hitachi   | HCT721050SLA380    | 500 GB | 1       | 136   | 0     | 0.37   |
| Seagate   | ST3160812AS Q      | 160 GB | 2       | 659   | 240   | 0.37   |
| Samsung   | HM100UX            | 1 TB   | 2       | 214   | 4     | 0.37   |
| WDC       | WD15EADS-11R6B1    | 1.5 TB | 1       | 1626  | 11    | 0.37   |
| WDC       | WD3200BPVT-75ZEST0 | 320 GB | 11      | 466   | 12    | 0.37   |
| WDC       | WD800JD-00JNA0     | 80 GB  | 2       | 809   | 5     | 0.37   |
| Hitachi   | HTS541060G9AT00    | 64 GB  | 9       | 439   | 13    | 0.37   |
| Hitachi   | HTS725032A7E630    | 320 GB | 6       | 783   | 685   | 0.37   |
| Toshiba   | MK5055GSX          | 500 GB | 29      | 503   | 162   | 0.37   |
| WDC       | WD10JUCT-63J6SY0   | 1 TB   | 6       | 342   | 183   | 0.37   |
| Seagate   | ST9120823ASG       | 120 GB | 2       | 229   | 1     | 0.37   |
| WDC       | WD1600BUCT-63TWBY0 | 160 GB | 2       | 134   | 0     | 0.37   |
| WDC       | WD3200BEVT-60ZCT1  | 320 GB | 16      | 424   | 191   | 0.37   |
| WDC       | WD5000LPLX-66ZNTT1 | 500 GB | 5       | 137   | 1     | 0.37   |
| WDC       | WD2500BPVT-22JJ5T0 | 250 GB | 11      | 298   | 193   | 0.37   |
| WDC       | WD7500AACS-00ZJB0  | 752 GB | 2       | 1621  | 507   | 0.37   |
| WDC       | WD10SPZX-22Z10T1   | 1 TB   | 50      | 133   | 0     | 0.37   |
| Samsung   | SP0842N            | 80 GB  | 14      | 601   | 564   | 0.37   |
| Seagate   | ST9160821AS        | 160 GB | 88      | 455   | 522   | 0.37   |
| HGST      | HDS5C4040ALE630    | 4 TB   | 2       | 133   | 0     | 0.37   |
| WDC       | WD5000LPCX-60VHAT0 | 500 GB | 69      | 171   | 5     | 0.36   |
| WDC       | WD2500BEVE-00A0HT0 | 250 GB | 3       | 132   | 0     | 0.36   |
| Fujitsu   | MHY2080BH          | 80 GB  | 17      | 265   | 140   | 0.36   |
| Seagate   | ST9500325AS        | 500 GB | 631     | 514   | 531   | 0.36   |
| Fujitsu   | MHV2100BH PL       | 100 GB | 9       | 209   | 2     | 0.36   |
| Toshiba   | MQ01ABD050V -63    | 500 GB | 6       | 132   | 0     | 0.36   |
| Hitachi   | HTS541040G9AT00    | 40 GB  | 9       | 415   | 10    | 0.36   |
| HP        | MB1000CBZQE        | 1 TB   | 1       | 1450  | 10    | 0.36   |
| WDC       | WD3200BEVT-26ZCT0  | 320 GB | 6       | 250   | 17    | 0.36   |
| Maxtor    | STM3160211AS       | 160 GB | 7       | 890   | 1179  | 0.36   |
| Seagate   | ST320LT012-1DG14C  | 320 GB | 40      | 273   | 134   | 0.36   |
| WDC       | WD10SPZX-60Z10T0   | 1 TB   | 105     | 138   | 1     | 0.36   |
| WDC       | WD101EDBZ-11B1DA0  | 10 TB  | 4       | 130   | 0     | 0.36   |
| WDC       | WD20SPZX-00UA7T0   | 2 TB   | 6       | 130   | 0     | 0.36   |
| WDC       | WD10EZEX-75WN4A1   | 1 TB   | 52      | 140   | 1     | 0.36   |
| WDC       | WD1600BEVT-35ZCT1  | 160 GB | 1       | 130   | 0     | 0.36   |
| Seagate   | ST340810A          | 40 GB  | 14      | 545   | 31    | 0.36   |
| WDC       | WD5000AZLX-35K2TA0 | 500 GB | 2       | 130   | 0     | 0.36   |
| WDC       | WD15EADS-22P8B0    | 1.5 TB | 3       | 376   | 341   | 0.36   |
| WDC       | WD10SPCX-24HWST0   | 1 TB   | 2       | 1167  | 187   | 0.36   |
| Toshiba   | HDWU130            | 3 TB   | 1       | 129   | 0     | 0.36   |
| Seagate   | ST9120822A         | 120 GB | 2       | 273   | 53    | 0.36   |
| WDC       | WD10SPZX-08Z10     | 1 TB   | 65      | 137   | 2     | 0.35   |
| Maxtor    | 6G160E0            | 160 GB | 9       | 363   | 147   | 0.35   |
| Toshiba   | MQ02ABF050H        | 500 GB | 8       | 241   | 257   | 0.35   |
| WDC       | WD20EZAZ-00L9GB0   | 2 TB   | 35      | 128   | 0     | 0.35   |
| Seagate   | ST10000DM005-3A... | 10 TB  | 1       | 128   | 0     | 0.35   |
| WDC       | WD800JD-22LSA1     | 80 GB  | 4       | 485   | 174   | 0.35   |
| WDC       | WD10SPZX-80Z10T2   | 1 TB   | 22      | 127   | 0     | 0.35   |
| IBM/Hi... | IC25N020ATMR04-0   | 20 GB  | 2       | 515   | 8     | 0.35   |
| Seagate   | ST500LM000-SSHD... | 500 GB | 65      | 315   | 379   | 0.35   |
| Fujitsu   | MHT2040AH PL       | 40 GB  | 2       | 766   | 5     | 0.35   |
| Seagate   | ST9250315ASG       | 250 GB | 3       | 166   | 6     | 0.35   |
| HPE       | MM1000EBKAF        | 1 TB   | 2       | 127   | 0     | 0.35   |
| WDC       | WD10SPZX-80Z10T0   | 1 TB   | 3       | 127   | 0     | 0.35   |
| WDC       | WD1600AAJS-56M0A0  | 160 GB | 2       | 469   | 4     | 0.35   |
| WDC       | WD102KFBX-68M95N0  | 10 TB  | 3       | 126   | 0     | 0.35   |
| WDC       | WD5000BEVT-80A0RT1 | 500 GB | 4       | 348   | 5     | 0.35   |
| MaxDig... | MD1TBLSSHD         | 1 TB   | 2       | 255   | 4     | 0.35   |
| Seagate   | ST500LM030-1RK17D  | 500 GB | 30      | 132   | 1     | 0.35   |
| Seagate   | ST3500830SCE       | 500 GB | 1       | 126   | 0     | 0.35   |
| WDC       | WD800JD-75HKA1     | 80 GB  | 1       | 379   | 2     | 0.35   |
| ExcelStor | J8080S             | 82 GB  | 1       | 2405  | 18    | 0.35   |
| Toshiba   | MK2546GSX          | 250 GB | 16      | 497   | 33    | 0.35   |
| Toshiba   | MQ04ABD200         | 2 TB   | 12      | 126   | 0     | 0.35   |
| WDC       | WD10SPZX-24Z10     | 1 TB   | 164     | 138   | 32    | 0.34   |
| WDC       | WD5000LUCT-61C26Y0 | 500 GB | 1       | 1005  | 7     | 0.34   |
| WDC       | WD60EMAZ-11LW3B0   | 6 TB   | 4       | 125   | 0     | 0.34   |
| Toshiba   | MK1216GSG          | 120 GB | 3       | 272   | 4     | 0.34   |
| Hitachi   | HTS541612J9SA00    | 120 GB | 85      | 593   | 89    | 0.34   |
| Toshiba   | MK4025GAS          | 40 GB  | 3       | 309   | 12    | 0.34   |
| Toshiba   | MQ01ABD064         | 640 GB | 1       | 124   | 0     | 0.34   |
| Seagate   | ST3160316CS        | 160 GB | 3       | 194   | 14    | 0.34   |
| HGST      | HTS545050A7E680    | 500 GB | 440     | 329   | 447   | 0.34   |
| WDC       | WD3200AAKS-00C9A0  | 320 GB | 3       | 1080  | 8     | 0.34   |
| WDC       | WD30PURZ-85GU6Y0   | 3 TB   | 4       | 124   | 0     | 0.34   |
| Toshiba   | DT01ACA200V        | 2 TB   | 1       | 124   | 0     | 0.34   |
| Toshiba   | MK1031GAS          | 100 GB | 7       | 301   | 11    | 0.34   |
| WDC       | WD20EZRZ-60Z5HB0   | 2 TB   | 3       | 123   | 0     | 0.34   |
| WDC       | WD1600HLHX-60JJPV1 | 160 GB | 1       | 617   | 4     | 0.34   |
| Toshiba   | MK6461GSYG         | 640 GB | 1       | 1971  | 15    | 0.34   |
| Fujitsu   | MHZ2160BH          | 160 GB | 2       | 123   | 0     | 0.34   |
| Seagate   | ST9250315AS        | 250 GB | 264     | 489   | 449   | 0.34   |
| WDC       | WD1600BEVT-75A23T0 | 160 GB | 11      | 301   | 56    | 0.34   |
| Seagate   | STM3160318AS       | 160 GB | 1       | 245   | 1     | 0.34   |
| Seagate   | ST9320320AS        | 320 GB | 35      | 721   | 174   | 0.34   |
| Toshiba   | MK7559GSXP         | 752 GB | 33      | 488   | 599   | 0.34   |
| Hitachi   | TPH01204000GB 0    | 4 TB   | 1       | 122   | 0     | 0.33   |
| Hitachi   | HTS541010G9SA00    | 100 GB | 19      | 402   | 80    | 0.33   |
| MaxDig... | MD4000GSA6472DVR 1 | 4 TB   | 1       | 121   | 0     | 0.33   |
| WDC       | WD2500JS-63MHB5    | 250 GB | 3       | 1066  | 96    | 0.33   |
| Samsung   | HM320HJ            | 320 GB | 9       | 315   | 427   | 0.33   |
| Hitachi   | HTS543216L9SA02    | 160 GB | 11      | 198   | 8     | 0.33   |
| Toshiba   | MK2555GSX          | 250 GB | 55      | 492   | 87    | 0.33   |
| Hitachi   | HDT722525DLAT80    | 250 GB | 4       | 819   | 11    | 0.33   |
| WDC       | WD2500AAJS-00YZCA0 | 250 GB | 9       | 935   | 32    | 0.33   |
| Seagate   | ST750LM000-1EJ16G  | 752 GB | 1       | 362   | 2     | 0.33   |
| Samsung   | HA200JC            | 200 GB | 1       | 120   | 0     | 0.33   |
| WDC       | WD40NPZZ-00A9JT0   | 4 TB   | 2       | 120   | 0     | 0.33   |
| WDC       | WD1600BEKT-00PVMT0 | 160 GB | 2       | 120   | 0     | 0.33   |
| Hitachi   | HTS541010G9AT00    | 100 GB | 2       | 238   | 1     | 0.33   |
| Toshiba   | MK3265GSXF         | 320 GB | 6       | 344   | 18    | 0.33   |
| Lenovo    | ST1000NM0055 91... | 1 TB   | 2       | 120   | 0     | 0.33   |
| MediaMax  | WL6000GSA6457      | 6 TB   | 2       | 438   | 686   | 0.33   |
| Samsung   | HM121HI            | 120 GB | 14      | 508   | 1409  | 0.33   |
| Toshiba   | MG06ACA600E        | 6 TB   | 2       | 119   | 0     | 0.33   |
| Seagate   | ST1000LM025 HN-... | 1 TB   | 59      | 135   | 18    | 0.33   |
| Seagate   | ST9100827AS        | 100 GB | 1       | 838   | 6     | 0.33   |
| WDC       | WD1600BEVS-26RST0  | 160 GB | 1       | 239   | 1     | 0.33   |
| Seagate   | ST960821A          | 64 GB  | 1       | 358   | 2     | 0.33   |
| WDC       | WD10EVDS-63U8B0    | 1 TB   | 1       | 1074  | 8     | 0.33   |
| HP        | MB1000GCWCV        | 1 TB   | 2       | 133   | 40    | 0.33   |
| Toshiba   | DT02ABA400         | 4 TB   | 3       | 118   | 0     | 0.33   |
| Seagate   | ST2000NE001-2M5101 | 2 TB   | 5       | 118   | 0     | 0.33   |
| WDC       | WD30PURZ-85AKKY0   | 3 TB   | 1       | 594   | 4     | 0.33   |
| Seagate   | ST3500410AS        | 500 GB | 34      | 1023  | 388   | 0.32   |
| Fujitsu   | MHY2060BH          | 64 GB  | 1       | 355   | 2     | 0.32   |
| Hitachi   | HTS545025A7E380    | 250 GB | 4       | 118   | 0     | 0.32   |
| Samsung   | HD103UI            | 1 TB   | 8       | 774   | 443   | 0.32   |
| WDC       | WD2500AVVS-61L2B0  | 250 GB | 2       | 1141  | 6     | 0.32   |
| WDC       | WD20EZBX-00AYRA0   | 2 TB   | 47      | 117   | 0     | 0.32   |
| WDC       | WD5000LPLX-60ZNTT2 | 500 GB | 9       | 126   | 1     | 0.32   |
| Seagate   | ST18000NE000-2Y... | 18 TB  | 7       | 117   | 0     | 0.32   |
| MediaMax  | WL1500GSA6472B     | 1.5 TB | 2       | 117   | 0     | 0.32   |
| HGST      | HUS726T6TALE6L4    | 6 TB   | 11      | 117   | 0     | 0.32   |
| WDC       | WD101EMAZ-11G7DA0  | 10 TB  | 7       | 117   | 0     | 0.32   |
| Fujitsu   | MHX2250BT          | 250 GB | 5       | 320   | 6     | 0.32   |
| Toshiba   | MK2565GSXN         | 250 GB | 8       | 353   | 130   | 0.32   |
| WDC       | WD100EJRX-89SYHY0  | 10 TB  | 1       | 116   | 0     | 0.32   |
| MaxDig... | MDT MD5000AAKS-... | 500 GB | 1       | 116   | 0     | 0.32   |
| Toshiba   | MK8046GSX          | 80 GB  | 7       | 464   | 291   | 0.32   |
| WDC       | 500GB              | 500 GB | 1       | 1047  | 8     | 0.32   |
| Hitachi   | TPH00500500GB 8    | 500 GB | 1       | 115   | 0     | 0.32   |
| WDC       | WD40NMZW-59LG6S1   | 4 TB   | 1       | 115   | 0     | 0.32   |
| Seagate   | ST500LM034-2GH17A  | 500 GB | 31      | 114   | 0     | 0.31   |
| WDC       | WD3200BEVT-00A23T0 | 320 GB | 5       | 175   | 9     | 0.31   |
| WDC       | WD8000AARS-00Y5B1  | 800 GB | 4       | 1501  | 12    | 0.31   |
| Toshiba   | MK6037GSX          | 64 GB  | 3       | 235   | 123   | 0.31   |
| WDC       | WD180EDFZ-11AFWA0  | 18 TB  | 3       | 113   | 0     | 0.31   |
| Hitachi   | HTS725050A9A364    | 500 GB | 46      | 551   | 792   | 0.31   |
| Seagate   | ST320LT020-9YG142  | 320 GB | 182     | 384   | 564   | 0.31   |
| Seagate   | ST960822A          | 64 GB  | 2       | 235   | 200   | 0.31   |
| WDC       | WD5000LPZX-08Z10   | 500 GB | 3       | 112   | 0     | 0.31   |
| Seagate   | ST9100823A         | 96 GB  | 1       | 1007  | 8     | 0.31   |
| Hitachi   | HTS721060G9SA00    | 64 GB  | 6       | 494   | 37    | 0.31   |
| WDC       | WD1600BEVS-60VAT0  | 160 GB | 2       | 415   | 7     | 0.31   |
| Seagate   | ST1000LV000-2G3172 | 1 TB   | 1       | 111   | 0     | 0.31   |
| WDC       | WD5000LPLX-22ZNTT0 | 500 GB | 12      | 145   | 5     | 0.31   |
| WDC       | WD400JB-00FMA0     | 40 GB  | 2       | 675   | 8     | 0.31   |
| Toshiba   | MG08ACA16TE        | 16 TB  | 11      | 111   | 0     | 0.31   |
| WDC       | WD6003FFBX-68MU3N0 | 6 TB   | 5       | 118   | 8     | 0.30   |
| WDC       | WD20SMZW-11JW8S1   | 2 TB   | 1       | 111   | 0     | 0.30   |
| Magnet... | MD03200-AVDW-RO    | 320 GB | 2       | 110   | 0     | 0.30   |
| WDC       | WD400BD-75JMA0     | 40 GB  | 1       | 663   | 5     | 0.30   |
| Seagate   | ST4000VN006-3CW104 | 4 TB   | 4       | 110   | 0     | 0.30   |
| Seagate   | ST3120811AS        | 120 GB | 20      | 488   | 475   | 0.30   |
| Samsung   | HM080GI            | 80 GB  | 1       | 220   | 1     | 0.30   |
| Fujitsu   | MHW2020BH          | 20 GB  | 2       | 109   | 0     | 0.30   |
| WDC       | WD8001PURP-74B6RY0 | 8 TB   | 1       | 109   | 0     | 0.30   |
| Seagate   | ST9100824AS        | 100 GB | 7       | 410   | 461   | 0.30   |
| WDC       | WD3000FYYZ-01UL1B0 | 3 TB   | 2       | 109   | 0     | 0.30   |
| WDC       | WD3200BEKT-00V5T0  | 320 GB | 1       | 109   | 0     | 0.30   |
| Seagate   | ST5000VN0001-1S... | 5 TB   | 1       | 217   | 1     | 0.30   |
| WDC       | WD80EFBX-68AZZN0   | 8 TB   | 18      | 108   | 0     | 0.30   |
| Toshiba   | HDWD240            | 4 TB   | 63      | 108   | 0     | 0.30   |
| WDC       | WD30EFZX-68AWUN0   | 3 TB   | 3       | 108   | 0     | 0.30   |
| WDC       | WD5000LPVX-28V0TT0 | 500 GB | 4       | 462   | 4     | 0.30   |
| Toshiba   | MK3252GSX          | 320 GB | 36      | 576   | 237   | 0.29   |
| Fujitsu   | MHV2040BH PL       | 40 GB  | 1       | 107   | 0     | 0.29   |
| WDC       | WD3200BEVT-88ZCT0  | 320 GB | 1       | 106   | 0     | 0.29   |
| WDC       | WD10EZRZ-22HTKB0   | 1 TB   | 18      | 116   | 1     | 0.29   |
| WDC       | WD80EDBZ-11B0ZA0   | 8 TB   | 4       | 106   | 0     | 0.29   |
| Toshiba   | MK1034GSX          | 100 GB | 5       | 375   | 373   | 0.29   |
| WDC       | WD5000BEVT-00SCST0 | 500 GB | 2       | 246   | 5     | 0.29   |
| WDC       | WD20EFZX-68AWUN0   | 2 TB   | 5       | 106   | 0     | 0.29   |
| China     | TP00250GB          | 250 GB | 1       | 106   | 0     | 0.29   |
| WDC       | WD3200BPVT-11HXZT3 | 320 GB | 1       | 106   | 0     | 0.29   |
| HPE       | MB8000GEQUU        | 8 TB   | 1       | 105   | 0     | 0.29   |
| WDC       | WD20SDRM-59A4DS1   | 2 TB   | 2       | 105   | 0     | 0.29   |
| WDC       | WD10SDRW-11A0XS0   | 1 TB   | 23      | 109   | 89    | 0.29   |
| Seagate   | ST500LM014 HN-M... | 500 GB | 15      | 157   | 5     | 0.29   |
| Toshiba   | MK1251GSY          | 120 GB | 1       | 939   | 8     | 0.29   |
| WDC       | WD3200BPVT-35JJ5T0 | 320 GB | 1       | 104   | 0     | 0.29   |
| WDC       | WD3200BJKT-00F4T0  | 320 GB | 2       | 104   | 0     | 0.29   |
| Seagate   | ST380023A          | 80 GB  | 1       | 2913  | 27    | 0.29   |
| WDC       | WD15EADS-65R2B0    | 1.5 TB | 1       | 934   | 8     | 0.28   |
| WDC       | WD5000AAKX-19U6AA0 | 500 GB | 1       | 103   | 0     | 0.28   |
| WDC       | WD161KFGX-68AFPN0  | 16 TB  | 1       | 103   | 0     | 0.28   |
| WDC       | WD1600YS-01SHB0    | 164 GB | 1       | 726   | 6     | 0.28   |
| WDC       | WD15NMVW-11EDZS7   | 1.5 TB | 1       | 103   | 0     | 0.28   |
| WDC       | WD40EJRX-89T1XY0   | 4 TB   | 1       | 103   | 0     | 0.28   |
| HGST      | HUS726T4TALE6L4    | 4 TB   | 9       | 105   | 169   | 0.28   |
| Fujitsu   | MHZ2080BJ FFS G2   | 80 GB  | 2       | 339   | 3     | 0.28   |
| WDC       | WD7500AARS-003BB1  | 752 GB | 4       | 588   | 63    | 0.28   |
| WDC       | WD1600BEVT-60ZCT0  | 160 GB | 9       | 352   | 345   | 0.28   |
| Hitachi   | HTS541080G9AT00    | 80 GB  | 16      | 562   | 98    | 0.28   |
| WDC       | WD5000AAKS-00M9A0  | 500 GB | 7       | 907   | 376   | 0.28   |
| Toshiba   | MK1637GSX          | 160 GB | 43      | 547   | 79    | 0.28   |
| WDC       | WD40NDZW-11BCSS0   | 4 TB   | 5       | 101   | 0     | 0.28   |
| Seagate   | ST6000NE000-2KR101 | 6 TB   | 7       | 101   | 0     | 0.28   |
| WDC       | WD10JPVT-00MS8T0   | 1 TB   | 1       | 607   | 5     | 0.28   |
| WDC       | WD3202ABYS-01B7A0  | 320 GB | 3       | 581   | 5     | 0.28   |
| Seagate   | ST9160301AS        | 160 GB | 13      | 133   | 155   | 0.28   |
| Fujitsu   | MHV2060BH PL       | 64 GB  | 9       | 100   | 3     | 0.28   |
| WDC       | WD10JPLX-00MBPT1   | 1 TB   | 3       | 376   | 80    | 0.28   |
| Seagate   | OOS3000G           | 3 TB   | 1       | 100   | 0     | 0.28   |
| Seagate   | STM31000528AS      | 1 TB   | 6       | 590   | 231   | 0.28   |
| Toshiba   | MK8025GAS          | 80 GB  | 4       | 122   | 22    | 0.28   |
| WDC       | WD5000HHTZ-04N21V1 | 500 GB | 1       | 100   | 0     | 0.27   |
| Toshiba   | HDWJ105            | 500 GB | 16      | 146   | 1     | 0.27   |
| WDC       | WD10SPCX-75HWST0   | 1 TB   | 1       | 100   | 0     | 0.27   |
| WDC       | WD42PURZ-85B4YY0   | 4 TB   | 5       | 100   | 0     | 0.27   |
| WDC       | WD10EADS-98M2B0    | 1 TB   | 2       | 807   | 8     | 0.27   |
| WDC       | WD20NPVZ-00WFZT0   | 2 TB   | 5       | 99    | 0     | 0.27   |
| WDC       | WD1600JD-55HBB0    | 160 GB | 1       | 695   | 6     | 0.27   |
| WDC       | WD1600BEAS-00RRT0  | 160 GB | 1       | 99    | 0     | 0.27   |
| Seagate   | ST10000NM0478-2... | 10 TB  | 8       | 99    | 0     | 0.27   |
| Seagate   | OOS6000G           | 6 TB   | 1       | 99    | 0     | 0.27   |
| Toshiba   | MK5065GSX          | 500 GB | 38      | 431   | 326   | 0.27   |
| WDC       | WUH721414ALE6L4    | 14 TB  | 11      | 98    | 0     | 0.27   |
| Seagate   | ST9160314AS        | 160 GB | 55      | 299   | 245   | 0.27   |
| WDC       | WD5000AADS-56S9B1  | 500 GB | 8       | 550   | 6     | 0.27   |
| Seagate   | ST3750330NS        | 752 GB | 7       | 560   | 201   | 0.27   |
| WDC       | WD600VE-00HDT0     | 64 GB  | 1       | 97    | 0     | 0.27   |
| Hitachi   | HTS542520K9SA00    | 200 GB | 5       | 614   | 10    | 0.27   |
| Seagate   | ST1000VN000-1HJ162 | 1 TB   | 1       | 97    | 0     | 0.27   |
| Toshiba   | MK1011GAH          | 100 GB | 7       | 299   | 125   | 0.27   |
| WDC       | WD2500BPVT-80ZEST0 | 250 GB | 2       | 144   | 4     | 0.27   |
| Fujitsu   | MJA2250BH G2       | 250 GB | 11      | 385   | 97    | 0.27   |
| Seagate   | ST500VT001-1K6142  | 500 GB | 1       | 96    | 0     | 0.26   |
| WDC       | WD2500AAJS-60M0A0  | 250 GB | 5       | 707   | 227   | 0.26   |
| WDC       | RFT030VQHR-GTK4D7  | 3 TB   | 1       | 96    | 0     | 0.26   |
| Seagate   | ST10000NE000-3A... | 10 TB  | 1       | 96    | 0     | 0.26   |
| WDC       | WD1200BEVS-60RST0  | 120 GB | 1       | 768   | 7     | 0.26   |
| WDC       | WD800JD-60JRA0     | 80 GB  | 1       | 672   | 6     | 0.26   |
| WDC       | WD800AAJS-60B4A0   | 80 GB  | 3       | 1091  | 16    | 0.26   |
| WDC       | WD7500BPVX-00JC3T0 | 752 GB | 3       | 95    | 0     | 0.26   |
| Samsung   | SP0401N            | 40 GB  | 1       | 95    | 0     | 0.26   |
| WDC       | WD20SDRW-11VUUS1   | 2 TB   | 8       | 95    | 0     | 0.26   |
| WDC       | WD102PURZ-85BXPY0  | 10 TB  | 3       | 95    | 0     | 0.26   |
| WDC       | WUH721818ALE6L4    | 18 TB  | 18      | 95    | 0     | 0.26   |
| Samsung   | HM250HJ            | 250 GB | 4       | 533   | 263   | 0.26   |
| Toshiba   | MK1653GSX          | 160 GB | 45      | 111   | 3     | 0.26   |
| WDC       | WD7500BPVT-55HXZT4 | 752 GB | 5       | 227   | 18    | 0.26   |
| Fujitsu   | MHW2080BHPL        | 80 GB  | 2       | 185   | 10    | 0.26   |
| WDC       | WD5000L12X-21UJGT0 | 516 GB | 1       | 93    | 0     | 0.26   |
| WDC       | WD10SPZX-75Z10T3   | 1 TB   | 31      | 96    | 4     | 0.26   |
| HGST      | HUH721212ALE600    | 12 TB  | 17      | 95    | 1     | 0.26   |
| Seagate   | ST9120817AS        | 120 GB | 11      | 385   | 507   | 0.26   |
| WDC       | WD40NMZW-59A8NS1   | 4 TB   | 6       | 124   | 2     | 0.26   |
| Seagate   | STM9120817AS       | 120 GB | 2       | 169   | 3     | 0.26   |
| Toshiba   | MG07ACA12TE        | 12 TB  | 20      | 92    | 0     | 0.25   |
| WDC       | WD2500JS-19NCB1    | 250 GB | 1       | 92    | 0     | 0.25   |
| Seagate   | ST18000NM000J-2... | 18 TB  | 33      | 92    | 0     | 0.25   |
| Samsung   | HM321HX            | 320 GB | 4       | 132   | 2     | 0.25   |
| Seagate   | ST3250310CS        | 250 GB | 4       | 948   | 186   | 0.25   |
| WDC       | WD5000BPVT-60HXZT1 | 500 GB | 5       | 604   | 985   | 0.25   |
| WDC       | WD1600BPVT-22JJ5T0 | 160 GB | 1       | 91    | 0     | 0.25   |
| Samsung   | HN-M101XBB         | 1 TB   | 2       | 91    | 0     | 0.25   |
| Samsung   | MP0402H            | 40 GB  | 11      | 245   | 15    | 0.25   |
| Maxtor    | STM3250824AS       | 250 GB | 2       | 1544  | 50    | 0.25   |
| WDC       | WD50NMZW-59BCBS1   | 5 TB   | 1       | 90    | 0     | 0.25   |
| Seagate   | ST6000VN001-2BB186 | 6 TB   | 1       | 90    | 0     | 0.25   |
| WDC       | WD40EZAZ-22SF3B0   | 4 TB   | 3       | 90    | 0     | 0.25   |
| Seagate   | ST31000340SV       | 1 TB   | 1       | 1616  | 17    | 0.25   |
| WDC       | WD3200BEVT-22A0RT0 | 320 GB | 5       | 218   | 4     | 0.25   |
| WDC       | WD10SPSX-08A6W     | 1 TB   | 7       | 89    | 0     | 0.25   |
| Samsung   | HS082HB            | 80 GB  | 1       | 89    | 0     | 0.25   |
| WDC       | WD10SPSX-00A6WT0   | 1 TB   | 8       | 89    | 0     | 0.24   |
| WDC       | WD800BD-08MRA1     | 80 GB  | 1       | 1427  | 15    | 0.24   |
| Toshiba   | MG09ACA18TE        | 18 TB  | 4       | 88    | 0     | 0.24   |
| Toshiba   | HDWT860            | 6 TB   | 1       | 88    | 0     | 0.24   |
| Seagate   | ST160LM000 HM161GI | 160 GB | 2       | 88    | 0     | 0.24   |
| WDC       | WD7500KMVW-11ZSMS4 | 752 GB | 2       | 373   | 6     | 0.24   |
| WDC       | WD3200SD-01KNB0    | 320 GB | 1       | 703   | 7     | 0.24   |
| IBM/Hi... | IC35L040AVER07-0   | 41 GB  | 3       | 700   | 8     | 0.24   |
| HGST      | HUS726030ALA610    | 3 TB   | 1       | 437   | 4     | 0.24   |
| WDC       | WD1600JS-61MHB1    | 160 GB | 1       | 959   | 10    | 0.24   |
| Hitachi   | HTS726060M9AT00    | 64 GB  | 2       | 289   | 34    | 0.24   |
| Seagate   | ST16000NM000J-2... | 16 TB  | 37      | 87    | 0     | 0.24   |
| Seagate   | ST3320613AS        | 320 GB | 125     | 874   | 277   | 0.24   |
| Toshiba   | MK5076GSX          | 500 GB | 56      | 155   | 180   | 0.24   |
| WDC       | WD2000JB-22GVA0    | 200 GB | 1       | 694   | 7     | 0.24   |
| WDC       | WD20SPZX-75UA7T1   | 2 TB   | 5       | 86    | 0     | 0.24   |
| WDC       | WD5000AZLX-60K2TA1 | 500 GB | 7       | 96    | 1     | 0.24   |
| Seagate   | ST500LM001-1EL162  | 500 GB | 1       | 86    | 0     | 0.24   |
| WDC       | WD1600BEVT-00A1TT0 | 160 GB | 2       | 273   | 3     | 0.24   |
| HGST      | HTS545050B7E660    | 500 GB | 26      | 90    | 1     | 0.23   |
| Samsung   | HD256GJ            | 250 GB | 4       | 404   | 260   | 0.23   |
| WDC       | WD20EFAX-68B2RN1   | 2 TB   | 2       | 84    | 0     | 0.23   |
| Seagate   | ST4000NE001-2MA101 | 4 TB   | 16      | 84    | 0     | 0.23   |
| Seagate   | ST2000LM010-1RA174 | 2 TB   | 1       | 84    | 0     | 0.23   |
| Toshiba   | HDWR440            | 4 TB   | 1       | 84    | 0     | 0.23   |
| Samsung   | HD300LD            | 304 GB | 4       | 554   | 15    | 0.23   |
| WDC       | WD5000LPZX-80Z10T0 | 500 GB | 1       | 83    | 0     | 0.23   |
| Seagate   | ST1000LX015-1U7... | 1 TB   | 5       | 216   | 686   | 0.23   |
| Toshiba   | MK8032GAX          | 80 GB  | 2       | 117   | 252   | 0.23   |
| HGST      | HUS726T4TALN6L4    | 4 TB   | 1       | 83    | 0     | 0.23   |
| Seagate   | ST10000NE0008-2... | 10 TB  | 6       | 82    | 0     | 0.23   |
| Seagate   | ST2000DM006-2EP102 | 2 TB   | 1       | 82    | 0     | 0.23   |
| WDC       | WD1001FAES-75W7A0  | 1 TB   | 6       | 1469  | 281   | 0.23   |
| Toshiba   | MK3021GAS          | 32 GB  | 1       | 495   | 5     | 0.23   |
| Toshiba   | MQ01UBF050         | 500 GB | 1       | 82    | 0     | 0.23   |
| WDC       | WD2500AAKX-193CA0  | 250 GB | 1       | 82    | 0     | 0.23   |
| WDC       | WD1200JB-00CRA1    | 120 GB | 2       | 793   | 12    | 0.23   |
| WDC       | WD1600JD-41HBC0    | 160 GB | 1       | 1884  | 22    | 0.22   |
| Toshiba   | MK2046GSX          | 200 GB | 14      | 359   | 46    | 0.22   |
| Toshiba   | MK1655GSXF         | 160 GB | 48      | 117   | 23    | 0.22   |
| WDC       | WD1200BEVS-60LAT0  | 120 GB | 1       | 81    | 0     | 0.22   |
| Fujitsu   | MHW2040AT          | 40 GB  | 2       | 621   | 8     | 0.22   |
| WDC       | WD8003FFBX-68B9AN0 | 8 TB   | 5       | 81    | 0     | 0.22   |
| Fujitsu   | MHT2080BH          | 80 GB  | 2       | 543   | 10    | 0.22   |
| Toshiba   | MK1652GSX          | 160 GB | 34      | 442   | 51    | 0.22   |
| Seagate   | ST3250820AV        | 250 GB | 1       | 80    | 0     | 0.22   |
| WDC       | WD40EDAZ-11SLVB0   | 4 TB   | 14      | 80    | 0     | 0.22   |
| Hitachi   | HTS722020K9SA00    | 200 GB | 5       | 615   | 7     | 0.22   |
| Seagate   | ST3000LM024-2AN17R | 3 TB   | 1       | 80    | 0     | 0.22   |
| Toshiba   | MK6025GAS          | 64 GB  | 3       | 181   | 62    | 0.22   |
| Magnet... | MD03200-AJDW-RO    | 320 GB | 1       | 79    | 0     | 0.22   |
| WDC       | WD2003FYYS-05T8B0  | 2 TB   | 1       | 79    | 0     | 0.22   |
| WDC       | WD600BEVS-07LAT0   | 64 GB  | 1       | 635   | 7     | 0.22   |
| WDC       | WD400BB-75JHC0     | 40 GB  | 1       | 476   | 5     | 0.22   |
| Seagate   | ST1000LM010-9YH146 | 1 TB   | 20      | 206   | 661   | 0.22   |
| Seagate   | ST31000322CS       | 1 TB   | 5       | 1341  | 113   | 0.22   |
| WDC       | WD3200BPVT-00HXZT1 | 320 GB | 10      | 350   | 218   | 0.22   |
| WDC       | WD40EFAX-68JH4N1   | 4 TB   | 23      | 79    | 1     | 0.22   |
| Toshiba   | MK6465GSX          | 640 GB | 38      | 721   | 581   | 0.21   |
| HGST      | HTS545032A7E380    | 320 GB | 67      | 178   | 573   | 0.21   |
| Seagate   | ST6000VX0003-1Z... | 6 TB   | 1       | 622   | 7     | 0.21   |
| WDC       | WD5000AZLX-75K2TA1 | 500 GB | 1       | 77    | 0     | 0.21   |
| WDC       | WD10EAVS-14M4B0    | 1 TB   | 1       | 77    | 0     | 0.21   |
| MediaMax  | WL2000GSA6454G     | 2 TB   | 2       | 735   | 6     | 0.21   |
| Hitachi   | HTS543280L9A300    | 80 GB  | 3       | 93    | 1     | 0.21   |
| WDC       | WD7500LPCX-60KHST0 | 752 GB | 3       | 77    | 0     | 0.21   |
| Seagate   | ST4000DM004-2U9104 | 4 TB   | 9       | 76    | 0     | 0.21   |
| Seagate   | ST9160310AS        | 160 GB | 61      | 279   | 169   | 0.21   |
| Lenovo    | WD1004FBYZ-23YC... | 1 TB   | 4       | 76    | 0     | 0.21   |
| WDC       | WD141KRYZ-01C66B0  | 14 TB  | 3       | 76    | 0     | 0.21   |
| Fujitsu   | MHV2060AT PL       | 64 GB  | 3       | 851   | 16    | 0.21   |
| WDC       | WD5000KMVV-11BG7S0 | 500 GB | 1       | 152   | 1     | 0.21   |
| Hitachi   | HDT721050SLA360    | 500 GB | 6       | 785   | 372   | 0.21   |
| WDC       | WD3200BEKT-75F3T0  | 320 GB | 1       | 683   | 8     | 0.21   |
| WDC       | WD2502ABYS-50B7A1  | 250 GB | 1       | 1290  | 16    | 0.21   |
| Seagate   | ST4000VX016-3CV104 | 4 TB   | 2       | 75    | 0     | 0.21   |
| WDC       | WD10SPSX-21A6WT0   | 1 TB   | 1       | 75    | 0     | 0.21   |
| WDC       | WD20EZBX-60AYRA0   | 2 TB   | 2       | 75    | 0     | 0.21   |
| WDC       | WD60PURX-64WY0Y1   | 6 TB   | 1       | 74    | 0     | 0.21   |
| Seagate   | ST9200827AS        | 200 GB | 1       | 1340  | 17    | 0.20   |
| WDC       | WD400VE-07HDT0     | 40 GB  | 1       | 74    | 0     | 0.20   |
| WDC       | WD15NMVW-11AV3S3   | 1.5 TB | 1       | 743   | 9     | 0.20   |
| Seagate   | ST12000VN0008-2... | 12 TB  | 3       | 74    | 0     | 0.20   |
| Samsung   | HM500LI            | 500 GB | 3       | 151   | 955   | 0.20   |
| Samsung   | SP1604N            | 160 GB | 8       | 458   | 60    | 0.20   |
| WDC       | WD5000MPCK-24AWHT0 | 500 GB | 1       | 74    | 0     | 0.20   |
| WDC       | WD800VE-75HDT1     | 80 GB  | 1       | 369   | 4     | 0.20   |
| Seagate   | ST4000NC001-1FS168 | 4 TB   | 2       | 73    | 0     | 0.20   |
| Hitachi   | HDE721050SLA330    | 500 GB | 1       | 2416  | 32    | 0.20   |
| Toshiba   | HDWK105            | 500 GB | 14      | 88    | 1     | 0.20   |
| WDC       | WD1600SD-01KCC0    | 160 GB | 1       | 2914  | 39    | 0.20   |
| WDC       | WD30NMZW-11LG6S1   | 3 TB   | 2       | 72    | 0     | 0.20   |
| Hitachi   | HTS722016K9A300    | 160 GB | 4       | 242   | 259   | 0.20   |
| Seagate   | ST9120411ASG       | 120 GB | 1       | 361   | 4     | 0.20   |
| MediaMax  | WL4000GSA6472E 1   | 4 TB   | 1       | 71    | 0     | 0.20   |
| Hitachi   | HTS548040M9AT00    | 40 GB  | 4       | 293   | 9     | 0.20   |
| Seagate   | ST31500341AS       | 1.5 TB | 107     | 921   | 321   | 0.20   |
| HP        | VB0160EAVEQ        | 160 GB | 2       | 216   | 513   | 0.20   |
| Seagate   | ST1000LM026 HN-... | 1 TB   | 1       | 214   | 2     | 0.20   |
| Toshiba   | MQ01ABD032V -63    | 320 GB | 1       | 714   | 9     | 0.20   |
| Hitachi   | HTS543232L9SA00    | 320 GB | 14      | 507   | 300   | 0.20   |
| WDC       | WD1600BEVS-00UST0  | 160 GB | 1       | 427   | 5     | 0.20   |
| Hitachi   | HCT721010SLA360    | 1 TB   | 1       | 925   | 12    | 0.20   |
| Samsung   | HD250KJ            | 250 GB | 1       | 711   | 9     | 0.19   |
| WDC       | WD40EFZX-68AWUN0   | 4 TB   | 36      | 73    | 1     | 0.19   |
| WDC       | WD40EZAZ-00SF3B0   | 4 TB   | 42      | 71    | 0     | 0.19   |
| IBM       | DTLA-307015        | 16 GB  | 1       | 423   | 5     | 0.19   |
| Seagate   | ST2000DM005-2U9102 | 2 TB   | 1       | 70    | 0     | 0.19   |
| WDC       | WD40NDZW-11A8JS0   | 4 TB   | 13      | 70    | 0     | 0.19   |
| Seagate   | STM980215AS        | 80 GB  | 2       | 195   | 1     | 0.19   |
| Toshiba   | MK6476GSXN         | 640 GB | 5       | 126   | 770   | 0.19   |
| Hitachi   | HTS545050B9SA00    | 500 GB | 13      | 932   | 887   | 0.19   |
| WDC       | WD20SMRW-59YNDS0   | 2 TB   | 7       | 69    | 0     | 0.19   |
| HGST      | HTS545025A7E330    | 250 GB | 2       | 69    | 0     | 0.19   |
| Toshiba   | MK1237GSX          | 120 GB | 23      | 435   | 168   | 0.19   |
| Seagate   | ST8000NM012A-2K... | 8 TB   | 1       | 69    | 0     | 0.19   |
| Toshiba   | MK3263GSXN         | 320 GB | 10      | 564   | 21    | 0.19   |
| Seagate   | ST380021A          | 80 GB  | 11      | 899   | 47    | 0.19   |
| Seagate   | ST3500320SV        | 500 GB | 2       | 940   | 10    | 0.19   |
| AMP       | uST340015A-1       | 40 GB  | 1       | 68    | 0     | 0.19   |
| WDC       | WD5000AVVS-63M8B0  | 500 GB | 3       | 1006  | 42    | 0.19   |
| Seagate   | ST91608220AS       | 160 GB | 1       | 135   | 1     | 0.19   |
| WDC       | WD200BB-60CJA0     | 20 GB  | 1       | 1417  | 20    | 0.18   |
| Seagate   | ST3300631AS        | 304 GB | 1       | 875   | 12    | 0.18   |
| Maxtor    | STM3160613AS       | 160 GB | 4       | 266   | 14    | 0.18   |
| Toshiba   | HDWT740            | 4 TB   | 3       | 67    | 0     | 0.18   |
| Hitachi   | HTS542512K9A300    | 120 GB | 9       | 425   | 236   | 0.18   |
| WDC       | WD10SPSX-60A6WT0   | 1 TB   | 11      | 66    | 0     | 0.18   |
| Seagate   | ST9120821AS        | 120 GB | 10      | 304   | 1207  | 0.18   |
| Seagate   | ST500DM002-9YN14C  | 500 GB | 6       | 530   | 465   | 0.18   |
| Toshiba   | MD06ACA10T         | 10 TB  | 1       | 66    | 0     | 0.18   |
| WDC       | WD1600AAJS         | 160 GB | 1       | 65    | 0     | 0.18   |
| WDC       | WD2500AAJS-60VWA1  | 250 GB | 1       | 65    | 0     | 0.18   |
| WDC       | WD60EDAZ-11U78B0   | 6 TB   | 8       | 65    | 0     | 0.18   |
| Hitachi   | HTS421280H9AT00    | 80 GB  | 7       | 600   | 14    | 0.18   |
| WDC       | WD3200BUCT-62TWBY0 | 320 GB | 3       | 65    | 0     | 0.18   |
| Fujitsu   | MHV2080BH PL       | 80 GB  | 24      | 107   | 3     | 0.18   |
| Seagate   | ST92011A           | 20 GB  | 1       | 1303  | 19    | 0.18   |
| Seagate   | ST320VM001-1AD142  | 320 GB | 3       | 64    | 0     | 0.18   |
| Seagate   | ST3160310CS        | 160 GB | 6       | 296   | 137   | 0.18   |
| Seagate   | ST2000NE0025-2F... | 2 TB   | 4       | 64    | 0     | 0.18   |
| WDC       | WD10SPSX-75A6WT0   | 1 TB   | 3       | 64    | 0     | 0.18   |
| WDC       | WD5000BEVT-60ZAT1  | 500 GB | 10      | 765   | 457   | 0.18   |
| WDC       | WD5000BEVT-11ZAT0  | 500 GB | 2       | 564   | 25    | 0.18   |
| WDC       | WD20PURZ-85AKKY0   | 2 TB   | 5       | 67    | 1     | 0.17   |
| WDC       | WD10EZRX-00RKKA0   | 1 TB   | 1       | 1714  | 26    | 0.17   |
| Fujitsu   | MHZ2160BJ FFS G2   | 160 GB | 1       | 569   | 8     | 0.17   |
| WDC       | WD3200AAJS-08B4A0  | 320 GB | 1       | 695   | 10    | 0.17   |
| WDC       | WD3200AAKX-753CA1  | 320 GB | 3       | 278   | 14    | 0.17   |
| Seagate   | ST6000NM019B-2T... | 6 TB   | 10      | 66    | 1     | 0.17   |
| WDC       | WD1200BEVE-00A0HT0 | 120 GB | 1       | 62    | 0     | 0.17   |
| WDC       | WD5000LPVX-16V0TT3 | 500 GB | 2       | 62    | 0     | 0.17   |
| Hitachi   | HDP725016GLAT80    | 160 GB | 1       | 62    | 0     | 0.17   |
| WDC       | WD5000AZRX-00A3KB0 | 500 GB | 4       | 160   | 6     | 0.17   |
| WDC       | WD6401AALS-00J7B1  | 640 GB | 1       | 564   | 8     | 0.17   |
| WDC       | WD3200AVJS-63TBA0  | 320 GB | 1       | 311   | 4     | 0.17   |
| WDC       | WD5000BMVU-11A08S0 | 500 GB | 1       | 745   | 11    | 0.17   |
| WDC       | WD10EZRX-22L4HB0   | 1 TB   | 1       | 62    | 0     | 0.17   |
| WDC       | WD25EZRS-00J99B0   | 2.5 TB | 1       | 2353  | 37    | 0.17   |
| WDC       | WD120EDBZ-11B1HA0  | 12 TB  | 10      | 61    | 0     | 0.17   |
| Maxtor    | 4K060H3            | 64 GB  | 1       | 927   | 14    | 0.17   |
| Toshiba   | MK6008GAH          | 64 GB  | 4       | 467   | 7     | 0.17   |
| Samsung   | SP1603C            | 160 GB | 1       | 367   | 5     | 0.17   |
| WDC       | WD5000BPVT-16HXZT1 | 500 GB | 1       | 549   | 8     | 0.17   |
| WDC       | WD160EDFZ-11AFWA0  | 16 TB  | 8       | 60    | 0     | 0.17   |
| WDC       | WD5000LPSX-08A6W   | 500 GB | 4       | 60    | 0     | 0.17   |
| Fujitsu   | MHV2100AH PL       | 100 GB | 1       | 423   | 6     | 0.17   |
| Seagate   | ST31000524NS 44... | 1 TB   | 1       | 1693  | 27    | 0.17   |
| Toshiba   | MK2556GSY          | 250 GB | 10      | 122   | 330   | 0.17   |
| Seagate   | ST320LT022-1AE142  | 320 GB | 3       | 329   | 118   | 0.17   |
| Hitachi   | DK23FB-60          | 64 GB  | 1       | 960   | 15    | 0.16   |
| MediaMax  | WL160GSA872B       | 160 GB | 1       | 540   | 8     | 0.16   |
| WDC       | WD2500AAJS-98B4A0  | 250 GB | 1       | 540   | 8     | 0.16   |
| WDC       | WD3200AAJS-00V4A0  | 320 GB | 3       | 531   | 9     | 0.16   |
| WDC       | WD1600BB-22GUC0    | 160 GB | 1       | 898   | 14    | 0.16   |
| WDC       | WD1600BEKT-00F3T0  | 160 GB | 2       | 59    | 0     | 0.16   |
| MediaMax  | WL750GSA6472       | 752 GB | 1       | 59    | 0     | 0.16   |
| Seagate   | ST3640323AS        | 640 GB | 11      | 1045  | 355   | 0.16   |
| WDC       | WD40NDZM-59PW8S1   | 4 TB   | 1       | 59    | 0     | 0.16   |
| WDC       | WUH721816ALE6L4    | 16 TB  | 4       | 59    | 0     | 0.16   |
| WDC       | WD50NDZW-11BCSS0   | 5 TB   | 5       | 59    | 0     | 0.16   |
| Maxtor    | STM3160811AS       | 160 GB | 7       | 648   | 232   | 0.16   |
| Seagate   | ST9250311CS        | 250 GB | 4       | 791   | 489   | 0.16   |
| Samsung   | HM641JX            | 640 GB | 3       | 87    | 5     | 0.16   |
| WDC       | WD30PURX-64PFUY0   | 3 TB   | 1       | 59    | 0     | 0.16   |
| Hitachi   | HTS541040G9SA00    | 40 GB  | 2       | 431   | 9     | 0.16   |
| WDC       | WD50NPZZ-00A9JT0   | 5 TB   | 2       | 58    | 0     | 0.16   |
| WDC       | WD1600BEVE-00A0HT0 | 160 GB | 1       | 58    | 0     | 0.16   |
| WDC       | WD2000JB-00EVA0    | 200 GB | 1       | 5666  | 96    | 0.16   |
| WDC       | WD1600HLFS-60G6U2  | 160 GB | 1       | 58    | 0     | 0.16   |
| Seagate   | ST980811A          | 80 GB  | 1       | 58    | 0     | 0.16   |
| MediaMax  | WL250GPA872B       | 250 GB | 1       | 58    | 0     | 0.16   |
| WDC       | WD10EZEX-35M2NA0   | 1 TB   | 2       | 305   | 4     | 0.16   |
| WDC       | WD5000BMVV-11SXZS2 | 500 GB | 1       | 57    | 0     | 0.16   |
| IBM/Hi... | IC25N080ATMR04-0   | 80 GB  | 6       | 310   | 29    | 0.16   |
| Seagate   | ST3750330AS        | 752 GB | 19      | 1076  | 308   | 0.16   |
| WDC       | WD20SDZM-59TM5S1   | 2 TB   | 1       | 56    | 0     | 0.16   |
| Seagate   | ST32000644NS 45... | 2 TB   | 1       | 1247  | 21    | 0.16   |
| Seagate   | ST31000340NS 44... | 1 TB   | 1       | 56    | 0     | 0.15   |
| Seagate   | ST4000VX013-2XG104 | 4 TB   | 3       | 55    | 0     | 0.15   |
| Seagate   | ST3200826A         | 200 GB | 2       | 561   | 8     | 0.15   |
| Hitachi   | HTS723232L9A360    | 320 GB | 7       | 932   | 844   | 0.15   |
| Samsung   | SP1213N            | 120 GB | 5       | 741   | 210   | 0.15   |
| WDC       | WD1500HLHX-01JJPV0 | 150 GB | 1       | 498   | 8     | 0.15   |
| WDC       | WD4500HLHX-01JJPV0 | 450 GB | 1       | 1108  | 19    | 0.15   |
| WDC       | WD5000LPVX-55V0TT3 | 500 GB | 1       | 55    | 0     | 0.15   |
| Seagate   | ST1000DL004 HD1... | 1 TB   | 2       | 458   | 4     | 0.15   |
| Hitachi   | HTS541616J9AT00    | 160 GB | 4       | 298   | 7     | 0.15   |
| WDC       | WD7500BPVT-60HXZT1 | 752 GB | 6       | 735   | 213   | 0.15   |
| WDC       | WD10EALX-229BA1    | 1 TB   | 1       | 493   | 8     | 0.15   |
| Samsung   | HM120JI            | 120 GB | 5       | 325   | 5     | 0.15   |
| Toshiba   | HDWD220            | 2 TB   | 13      | 54    | 0     | 0.15   |
| Seagate   | ST8000DM004-2U9188 | 8 TB   | 11      | 54    | 0     | 0.15   |
| Samsung   | HM060HC            | 52 GB  | 1       | 272   | 4     | 0.15   |
| Toshiba   | MK1255GSX H        | 120 GB | 8       | 285   | 110   | 0.15   |
| Hitachi   | HDT725032VLAT80    | 320 GB | 4       | 1102  | 67    | 0.15   |
| Samsung   | HM501IX            | 500 GB | 1       | 54    | 0     | 0.15   |
| HGST      | HTS725050A7E635... | 500 GB | 4       | 759   | 28    | 0.15   |
| Seagate   | ST3320813AS        | 320 GB | 8       | 896   | 126   | 0.15   |
| WDC       | WD5000LQVX-22K6RT0 | 500 GB | 1       | 53    | 0     | 0.15   |
| Seagate   | ST4000NM002A-2H... | 4 TB   | 3       | 53    | 0     | 0.15   |
| WDC       | WD5003ABYZ-011FAO  | 500 GB | 1       | 53    | 0     | 0.15   |
| Toshiba   | MK5055GSXF         | 500 GB | 3       | 498   | 61    | 0.15   |
| WDC       | WD5000BPKT-80PK4T0 | 500 GB | 2       | 347   | 5     | 0.15   |
| WDC       | WD3200BEVT-63ZCT0  | 320 GB | 1       | 53    | 0     | 0.15   |
| Maxtor    | 6L080J4            | 80 GB  | 1       | 319   | 5     | 0.15   |
| WDC       | WD1600BEVS-00RST0  | 160 GB | 1       | 52    | 0     | 0.15   |
| WDC       | WD2500AAJS-22L7A0  | 250 GB | 4       | 950   | 74    | 0.14   |
| WDC       | WD2500BEVT-22ZAT0  | 250 GB | 1       | 316   | 5     | 0.14   |
| WDC       | WD40PURZ-85AKKY0   | 4 TB   | 28      | 81    | 1     | 0.14   |
| WDC       | WD5000LPCX-80VHAT1 | 500 GB | 5       | 92    | 766   | 0.14   |
| WDC       | WUH721816ALE6L0    | 16 TB  | 1       | 52    | 0     | 0.14   |
| Toshiba   | MK5065GSXN         | 500 GB | 18      | 460   | 527   | 0.14   |
| Maxtor    | 7B300S0            | 304 GB | 1       | 2421  | 46    | 0.14   |
| WDC       | WD20EURX-25T0FY0   | 2 TB   | 3       | 51    | 0     | 0.14   |
| WDC       | WD10SMZW-59Y0TS0   | 1 TB   | 1       | 51    | 0     | 0.14   |
| Seagate   | ST1000LM022-9XV155 | 1 TB   | 2       | 1349  | 2021  | 0.14   |
| Seagate   | ST500LM016 HN-M... | 500 GB | 3       | 51    | 0     | 0.14   |
| HGST      | HCC545050A7E630    | 500 GB | 3       | 51    | 0     | 0.14   |
| WDC       | WD3200BEVT-60A23T0 | 320 GB | 31      | 400   | 416   | 0.14   |
| Seagate   | ST3500511CS        | 500 GB | 1       | 50    | 0     | 0.14   |
| Seagate   | ST960812A          | 64 GB  | 1       | 151   | 2     | 0.14   |
| Seagate   | ST9250320AS        | 250 GB | 27      | 500   | 293   | 0.14   |
| ExcelStor | J8160              | 34 GB  | 1       | 50    | 0     | 0.14   |
| WDC       | WD10JUCX-63WPNY0   | 1 TB   | 2       | 97    | 22    | 0.14   |
| Toshiba   | HDWG11A            | 10 TB  | 1       | 50    | 0     | 0.14   |
| Seagate   | ST2000VX007-2AY102 | 2 TB   | 1       | 50    | 0     | 0.14   |
| Hitachi   | HTS725050A9A360    | 500 GB | 3       | 189   | 354   | 0.14   |
| WDC       | WD360GD-00FLA2     | 37 GB  | 4       | 1259  | 29    | 0.14   |
| Seagate   | ST95000NSSUN500G   | 500 GB | 1       | 2980  | 59    | 0.14   |
| Seagate   | ST95000NSSUN500... | 500 GB | 1       | 2980  | 59    | 0.14   |
| Seagate   | ST6000VX001-2BD186 | 6 TB   | 1       | 49    | 0     | 0.14   |
| WDC       | WD5000MPCK-21AWHT0 | 500 GB | 1       | 49    | 0     | 0.14   |
| Seagate   | OOS12000G          | 12 TB  | 7       | 49    | 0     | 0.13   |
| Seagate   | ST2000VX000-9YW164 | 2 TB   | 8       | 717   | 782   | 0.13   |
| Seagate   | ST8000VX004-2M1101 | 8 TB   | 1       | 48    | 0     | 0.13   |
| WDC       | WD10JUCT-61CYNY0   | 1 TB   | 1       | 48    | 0     | 0.13   |
| WDC       | WD5000LPCX-80VHAT0 | 500 GB | 2       | 48    | 0     | 0.13   |
| Hitachi   | HTS424040M9AT00    | 40 GB  | 7       | 441   | 161   | 0.13   |
| Seagate   | ST9808210A         | 80 GB  | 2       | 259   | 19    | 0.13   |
| Maxtor    | STM3160813AS       | 160 GB | 8       | 905   | 431   | 0.13   |
| WDC       | WD400BB-00CAA1     | 40 GB  | 1       | 289   | 5     | 0.13   |
| Seagate   | ST9402115AS        | 40 GB  | 4       | 113   | 521   | 0.13   |
| WDC       | WD15NMVW-11EDZS2   | 1.5 TB | 1       | 48    | 0     | 0.13   |
| WDC       | WD5000AURX-63UY4Y0 | 500 GB | 3       | 817   | 17    | 0.13   |
| WDC       | WD6001FSYZ-01SS7B1 | 6 TB   | 1       | 47    | 0     | 0.13   |
| WDC       | WD6400BEVT-16A0RT0 | 640 GB | 1       | 430   | 8     | 0.13   |
| Seagate   | ST4000NC000-1FR168 | 4 TB   | 4       | 47    | 0     | 0.13   |
| MARSHAL   | MAL2500SA-T54      | 500 GB | 3       | 282   | 18    | 0.13   |
| Hitachi   | HTS421210H9AT00    | 100 GB | 1       | 568   | 11    | 0.13   |
| WDC       | WD360GD-00FLA1     | 37 GB  | 1       | 1789  | 37    | 0.13   |
| HGST      | HTS541075A7E630    | 752 GB | 10      | 100   | 203   | 0.13   |
| WDC       | WD1600AAJS-22B4A0  | 160 GB | 1       | 46    | 0     | 0.13   |
| WDC       | WD3200BEKT-22KA9T0 | 320 GB | 1       | 46    | 0     | 0.13   |
| Seagate   | ST31000340AS       | 1 TB   | 13      | 810   | 451   | 0.13   |
| WDC       | WD5000LPZX-60Z10T0 | 500 GB | 5       | 59    | 425   | 0.13   |
| WDC       | WD101EDAZ-11Y7KA0  | 10 TB  | 1       | 46    | 0     | 0.13   |
| WDC       | WD7500AAVS-00D7B1  | 752 GB | 2       | 1348  | 344   | 0.13   |
| Hitachi   | HTS543225L9SA00    | 250 GB | 13      | 483   | 106   | 0.12   |
| WDC       | WD1200BEVS-22LAT0  | 120 GB | 2       | 406   | 81    | 0.12   |
| Hitachi   | HTS541060G9SA00    | 64 GB  | 5       | 265   | 74    | 0.12   |
| WDC       | WD30EZRX-00D8PB... | 3 TB   | 1       | 45    | 0     | 0.12   |
| Samsung   | SV4012H            | 40 GB  | 2       | 1504  | 236   | 0.12   |
| WDC       | WD1600AAJS-19WAA0  | 160 GB | 1       | 44    | 0     | 0.12   |
| WDC       | WD800BEVS-60RST0   | 80 GB  | 2       | 643   | 291   | 0.12   |
| IBM       | DTLA-307020        | 20 GB  | 1       | 754   | 16    | 0.12   |
| Hitachi   | HTS541212H9SA00    | 120 GB | 1       | 221   | 4     | 0.12   |
| MARSHAL   | MAL2750SA-T54      | 752 GB | 3       | 231   | 849   | 0.12   |
| Toshiba   | HDWG480            | 8 TB   | 4       | 43    | 0     | 0.12   |
| WDC       | WD5000AAKX-004EA0  | 500 GB | 1       | 392   | 8     | 0.12   |
| Toshiba   | MK1665GSX          | 160 GB | 24      | 192   | 325   | 0.12   |
| Seagate   | ST3500410SV        | 500 GB | 4       | 1006  | 282   | 0.12   |
| WDC       | WD5000LPCX-60VHAT1 | 500 GB | 19      | 84    | 10    | 0.12   |
| Hitachi   | HDP725025GLAT80    | 250 GB | 1       | 216   | 4     | 0.12   |
| Hitachi   | HDS722540VLAT20    | 40 GB  | 1       | 215   | 4     | 0.12   |
| WDC       | WD10JUCX-56WPNY0   | 1 TB   | 1       | 43    | 0     | 0.12   |
| Hitachi   | HTS722016K9SA00    | 160 GB | 2       | 335   | 41    | 0.12   |
| Fujitsu   | MHV2060AH          | 64 GB  | 2       | 1144  | 33    | 0.12   |
| WDC       | WD10SDRW-11A0XS1   | 1 TB   | 6       | 42    | 0     | 0.12   |
| WDC       | WD20EZBX-08AYR     | 2 TB   | 3       | 42    | 0     | 0.12   |
| WDC       | WD80EMZZ-11B4FB0   | 8 TB   | 2       | 42    | 0     | 0.12   |
| WDC       | WD10TPVT-00HT5T1   | 1 TB   | 2       | 396   | 9     | 0.12   |
| Samsung   | HM100JC            | 100 GB | 2       | 546   | 12    | 0.12   |
| Toshiba   | MK5056GSY          | 500 GB | 7       | 261   | 151   | 0.12   |
| HGST      | HTS725050B7E630    | 500 GB | 3       | 42    | 0     | 0.12   |
| Maxtor    | 6B300R0            | 304 GB | 1       | 42    | 0     | 0.12   |
| Hitachi   | HCP725050GLA380    | 500 GB | 2       | 1373  | 1059  | 0.12   |
| WDC       | WD1600BMVS-11F9S0  | 160 GB | 1       | 339   | 7     | 0.12   |
| WDC       | WD400EB-00CPF0     | 40 GB  | 6       | 618   | 58    | 0.12   |
| WDC       | WD1503FYYS-02W0B0  | 1.5 TB | 1       | 382   | 8     | 0.12   |
| Maxtor    | 6B160P0            | 163 GB | 1       | 42    | 0     | 0.12   |
| Hitachi   | HTS725025A9A364    | 250 GB | 27      | 460   | 1039  | 0.12   |
| WDC       | WD120EFBX-68B0EN0  | 12 TB  | 4       | 42    | 0     | 0.12   |
| WDC       | WD1600BEVT-26ZCT0  | 160 GB | 2       | 186   | 22    | 0.12   |
| WDC       | WD400BD-08JMC0     | 40 GB  | 1       | 801   | 18    | 0.12   |
| Quantum   | FIREBALLlct20 10   | 10 GB  | 1       | 42    | 0     | 0.12   |
| WDC       | WD5000LPZX-22Z10T0 | 500 GB | 4       | 41    | 0     | 0.11   |
| Seagate   | ST2000DM008-2UB102 | 2 TB   | 39      | 41    | 10    | 0.11   |
| WDC       | WD10SPZX-60Z10T1   | 1 TB   | 9       | 41    | 0     | 0.11   |
| Hitachi   | HTS723225A7A364    | 250 GB | 3       | 636   | 679   | 0.11   |
| IBM/Hi... | IC25N030ATCS04-0   | 32 GB  | 3       | 198   | 5     | 0.11   |
| Seagate   | ST31000533CS       | 1 TB   | 2       | 828   | 40    | 0.11   |
| Seagate   | ST9250410ASG       | 250 GB | 2       | 543   | 513   | 0.11   |
| WDC       | WD10TPVT-65HT5T0   | 1 TB   | 1       | 411   | 9     | 0.11   |
| WDC       | WD1200BEVS-00RST0  | 120 GB | 1       | 41    | 0     | 0.11   |
| WDC       | WD15SMZW-11JW8S0   | 1.5 TB | 2       | 41    | 0     | 0.11   |
| Maxtor    | 7L250R0            | 256 GB | 1       | 40    | 0     | 0.11   |
| WDC       | WD30EZAZ-00SF3B0   | 3 TB   | 1       | 40    | 0     | 0.11   |
| Fujitsu   | MHV2200BT PL       | 200 GB | 1       | 325   | 7     | 0.11   |
| WDC       | WD1600BEVE-00UYT0  | 160 GB | 1       | 40    | 0     | 0.11   |
| WDC       | WD3200LPVT-00G33T0 | 320 GB | 2       | 40    | 0     | 0.11   |
| WDC       | WD6400AAKS-55A7B2  | 640 GB | 1       | 361   | 8     | 0.11   |
| Seagate   | ST9500424AS        | 500 GB | 5       | 168   | 504   | 0.11   |
| MediaMax  | WL1000GSA3254G     | 1 TB   | 1       | 476   | 11    | 0.11   |
| Toshiba   | MK1214GAH          | 120 GB | 5       | 95    | 87    | 0.11   |
| Hitachi   | HTS545012B9SA00    | 120 GB | 1       | 197   | 4     | 0.11   |
| WDC       | WD5000LPCX-75VHAT1 | 500 GB | 3       | 39    | 0     | 0.11   |
| WDC       | WD3200LPVT-22G33T0 | 320 GB | 2       | 39    | 0     | 0.11   |
| WDC       | WD10EZEX-00BBHA0   | 1 TB   | 52      | 42    | 1     | 0.11   |
| Synology  | HAT5300-16T        | 16 TB  | 7       | 39    | 0     | 0.11   |
| WDC       | WD3200BEKT-60F3T1  | 320 GB | 13      | 496   | 443   | 0.11   |
| WDC       | WD5000AVCS-612DY1  | 500 GB | 1       | 582   | 14    | 0.11   |
| WDC       | WD15SMRW-11YNDS0   | 1.5 TB | 1       | 38    | 0     | 0.11   |
| IBM/Hi... | IC25N060ATMR04-0   | 64 GB  | 10      | 342   | 23    | 0.11   |
| WDC       | WD10EVVS-63M5B0    | 1 TB   | 1       | 38    | 0     | 0.11   |
| WDC       | WD1500ADFD-00NLR5  | 150 GB | 1       | 344   | 8     | 0.10   |
| WDC       | WD1600BEKT-66PVMT0 | 160 GB | 1       | 761   | 19    | 0.10   |
| Hitachi   | HTS541020G9SA00    | 20 GB  | 1       | 38    | 0     | 0.10   |
| WDC       | WD153AA-53BAA0     | 16 GB  | 1       | 491   | 12    | 0.10   |
| WDC       | WD50NDZW-11BCSS1   | 5 TB   | 6       | 37    | 0     | 0.10   |
| Toshiba   | MK2529GSG          | 250 GB | 4       | 209   | 859   | 0.10   |
| WDC       | WD20SPZX-60UA7T0   | 2 TB   | 5       | 45    | 1     | 0.10   |
| WDC       | WD1600BEKT-60V5T1  | 160 GB | 3       | 150   | 4     | 0.10   |
| WDC       | WD1200UE-22KVT0    | 120 GB | 2       | 376   | 46    | 0.10   |
| Toshiba   | MK2555GSX H        | 250 GB | 2       | 472   | 957   | 0.10   |
| WDC       | WD3200BEVS-16VAT0  | 320 GB | 1       | 37    | 0     | 0.10   |
| WDC       | WD30NMZW-11A8NS1   | 3 TB   | 1       | 36    | 0     | 0.10   |
| WDC       | WD20EVDS-63T3B0    | 2 TB   | 2       | 330   | 8     | 0.10   |
| Seagate   | ST8000VN004-3CP101 | 8 TB   | 1       | 36    | 0     | 0.10   |
| Toshiba   | MK4055GSX          | 400 GB | 4       | 288   | 7     | 0.10   |
| Toshiba   | MG07ACA12TEY       | 12 TB  | 3       | 36    | 0     | 0.10   |
| WDC       | WD1600BUDT-63DPZY0 | 160 GB | 16      | 45    | 2     | 0.10   |
| HGST      | HUS726060ALE611    | 6 TB   | 2       | 36    | 0     | 0.10   |
| Hitachi   | HTS542525K9A300    | 250 GB | 14      | 565   | 765   | 0.10   |
| HP        | MB1000EAMZE        | 1 TB   | 2       | 1797  | 1037  | 0.10   |
| IBM/Hi... | IC25N040ATMR04-0   | 40 GB  | 3       | 442   | 121   | 0.10   |
| WDC       | WD10TMVV-11BG7S0   | 1 TB   | 4       | 610   | 232   | 0.10   |
| WDC       | WD5000BPVX-00JC3T0 | 500 GB | 4       | 35    | 0     | 0.10   |
| Maxtor    | 6L120P0            | 122 GB | 2       | 35    | 0     | 0.10   |
| Toshiba   | MK6476GSX          | 640 GB | 30      | 74    | 365   | 0.10   |
| Seagate   | ST1000NM0011 99... | 1 TB   | 1       | 1126  | 31    | 0.10   |
| Seagate   | ST250VT000-1DK141  | 250 GB | 1       | 35    | 0     | 0.10   |
| Apple     | HDD HTS547575A9... | 752 GB | 2       | 453   | 79    | 0.10   |
| Seagate   | ST3500320AS        | 500 GB | 109     | 830   | 415   | 0.10   |
| Fujitsu   | MHJ2181AT          | 18 GB  | 1       | 1462  | 41    | 0.10   |
| WDC       | WD1600BPVT-00JJ5T0 | 160 GB | 1       | 34    | 0     | 0.10   |
| WDC       | WD140EFFX-68VBXN0  | 14 TB  | 16      | 34    | 0     | 0.10   |
| Toshiba   | MK6028GAL          | 64 GB  | 2       | 34    | 0     | 0.10   |
| Hitachi   | HTS725025A9A361... | 250 GB | 1       | 34    | 0     | 0.09   |
| WDC       | WD1500ADFS-00SLR5  | 150 GB | 1       | 103   | 2     | 0.09   |
| Samsung   | HM160HC            | 160 GB | 13      | 198   | 17    | 0.09   |
| WDC       | WD6400BEVT-24A0RT0 | 640 GB | 1       | 442   | 12    | 0.09   |
| Seagate   | ST14000NE0008-2... | 14 TB  | 8       | 33    | 0     | 0.09   |
| WDC       | WD20EARX-00AZ6B0   | 2 TB   | 1       | 505   | 14    | 0.09   |
| Maxtor    | 2F030L0            | 32 GB  | 1       | 33    | 0     | 0.09   |
| Toshiba   | MK3261GSYN         | 320 GB | 28      | 69    | 260   | 0.09   |
| WDC       | WD3200BMVS-11F9S0  | 320 GB | 3       | 37    | 1     | 0.09   |
| Toshiba   | MK1235GSL          | 120 GB | 1       | 33    | 0     | 0.09   |
| Toshiba   | HDWM105            | 500 GB | 1       | 32    | 0     | 0.09   |
| Hitachi   | DK23EA-40          | 40 GB  | 2       | 241   | 236   | 0.09   |
| Seagate   | ST2000NM000A-2J... | 2 TB   | 3       | 32    | 0     | 0.09   |
| WDC       | WD5000LMVW-11VEDS6 | 500 GB | 3       | 188   | 24    | 0.09   |
| Maxtor    | STM3500320AS       | 500 GB | 28      | 576   | 279   | 0.09   |
| Seagate   | ST31000333AS       | 1 TB   | 42      | 788   | 323   | 0.09   |
| WDC       | WD20SDRW-34VUUS1   | 2 TB   | 2       | 32    | 0     | 0.09   |
| WDC       | WD10E              | 1 TB   | 1       | 31    | 0     | 0.09   |
| WDC       | WD7500KMVV-11A27S2 | 752 GB | 1       | 31    | 0     | 0.09   |
| WDC       | WD800JB-00FSA0     | 80 GB  | 1       | 1366  | 43    | 0.09   |
| MediaMax  | WL1500GSA6454G     | 1.5 TB | 2       | 100   | 4     | 0.08   |
| WDC       | WD121KFBX-68EF5N0  | 12 TB  | 7       | 30    | 0     | 0.08   |
| WDC       | WD367GD-00FLA1     | 37 GB  | 1       | 1757  | 57    | 0.08   |
| Samsung   | HM121HC            | 120 GB | 3       | 230   | 19    | 0.08   |
| Seagate   | ST38410A           | 9 GB   | 1       | 754   | 24    | 0.08   |
| WDC       | WD600VE-75HDT0     | 64 GB  | 1       | 268   | 8     | 0.08   |
| IBM/Hi... | IC25N040ATCS04-0   | 40 GB  | 1       | 59    | 1     | 0.08   |
| Samsung   | SV0401N            | 40 GB  | 1       | 952   | 31    | 0.08   |
| Toshiba   | HDWR440UZSVB       | 4 TB   | 1       | 29    | 0     | 0.08   |
| Samsung   | MP0804H            | 80 GB  | 3       | 243   | 8     | 0.08   |
| WDC       | WD1600JS-00MHB1    | 160 GB | 1       | 1060  | 35    | 0.08   |
| WDC       | WD6004FZWX-00BKVA0 | 6 TB   | 3       | 29    | 0     | 0.08   |
| Samsung   | HS12UHE            | 120 GB | 2       | 146   | 5     | 0.08   |
| CLOVER    | CN-M500MBB         | 500 GB | 2       | 29    | 0     | 0.08   |
| Fujitsu   | MHT2030AT          | 32 GB  | 2       | 367   | 13    | 0.08   |
| Maxtor    | STM3320613AS       | 320 GB | 18      | 984   | 364   | 0.08   |
| Maxtor    | 6L100M0            | 100 GB | 2       | 28    | 0     | 0.08   |
| WDC       | WD101KFBX-68R56N0  | 10 TB  | 2       | 28    | 0     | 0.08   |
| Seagate   | ST94813A           | 40 GB  | 1       | 28    | 0     | 0.08   |
| WDC       | WD2003FYPS-27W9B0  | 2 TB   | 3       | 1397  | 248   | 0.08   |
| Seagate   | ST2000DM008-2CW102 | 2 TB   | 1       | 28    | 0     | 0.08   |
| MediaMax  | WL120GBSATA        | 120 GB | 1       | 139   | 4     | 0.08   |
| HPE       | MM1000GBKAL        | 1 TB   | 1       | 1005  | 35    | 0.08   |
| Fujitsu   | MHV2080BHPL        | 80 GB  | 1       | 83    | 2     | 0.08   |
| Toshiba   | MK5061GSYN         | 500 GB | 32      | 66    | 269   | 0.08   |
| Magnet... | MD01600-BJDW-RO    | 160 GB | 1       | 27    | 0     | 0.08   |
| Samsung   | HM251JI            | 250 GB | 13      | 228   | 504   | 0.08   |
| WDC       | WD40NDZM-59A8KS1   | 4 TB   | 1       | 274   | 9     | 0.08   |
| Seagate   | ST4000NM000A 00... | 4 TB   | 5       | 27    | 0     | 0.08   |
| Seagate   | ST4000LM024-2U817V | 4 TB   | 2       | 27    | 0     | 0.07   |
| WDC       | WD1600YS-23SHB0    | 160 GB | 2       | 398   | 926   | 0.07   |
| Hitachi   | HCS721010CLA332    | 1 TB   | 1       | 2081  | 76    | 0.07   |
| WDC       | WD140EFGX-68B0GN0  | 14 TB  | 3       | 26    | 0     | 0.07   |
| WDC       | WD2000JD-55HBC0    | 200 GB | 1       | 26    | 0     | 0.07   |
| WDC       | WD20SPZX-60UA7T1   | 2 TB   | 1       | 26    | 0     | 0.07   |
| Toshiba   | HDWG440            | 4 TB   | 2       | 26    | 0     | 0.07   |
| WDC       | WD5000LPSX-00A6WT0 | 500 GB | 3       | 26    | 0     | 0.07   |
| Toshiba   | MQ01ABD075H        | 752 GB | 1       | 236   | 8     | 0.07   |
| WDC       | WD3200AAJS-00VWA1  | 320 GB | 1       | 708   | 26    | 0.07   |
| WDC       | WD160EDGZ-11B2DA0  | 16 TB  | 2       | 26    | 0     | 0.07   |
| Samsung   | HM251JJ            | 250 GB | 1       | 156   | 5     | 0.07   |
| WDC       | WD2500JB-55EVA0    | 250 GB | 1       | 77    | 2     | 0.07   |
| Toshiba   | MK2565GSXV         | 250 GB | 4       | 292   | 20    | 0.07   |
| Maxtor    | 6B250S0            | 250 GB | 3       | 36    | 314   | 0.07   |
| Samsung   | HM322IX            | 320 GB | 1       | 25    | 0     | 0.07   |
| WDC       | WD6400BPVT-60HXZT3 | 640 GB | 1       | 1069  | 41    | 0.07   |
| Seagate   | ST14000NM0007-2... | 14 TB  | 4       | 25    | 0     | 0.07   |
| WDC       | WD80EAZZ-00BKLB0   | 8 TB   | 1       | 25    | 0     | 0.07   |
| WDC       | WD40EZAZ-00ZGHB0   | 4 TB   | 2       | 24    | 0     | 0.07   |
| WDC       | WD50NDZM-59A8KS1   | 5 TB   | 2       | 24    | 0     | 0.07   |
| WDC       | WD3200JD-22KLB0    | 320 GB | 1       | 1261  | 50    | 0.07   |
| WDC       | WD3200AAJS-57VWA2  | 320 GB | 1       | 24    | 0     | 0.07   |
| WDC       | WD2500AAJS-52B4A0  | 250 GB | 2       | 942   | 45    | 0.07   |
| Seagate   | ST3750840ACE       | 752 GB | 1       | 483   | 19    | 0.07   |
| WDC       | WD400VE-75HDT1     | 40 GB  | 1       | 23    | 0     | 0.06   |
| Hitachi   | HTS421260H9AT00    | 64 GB  | 5       | 380   | 16    | 0.06   |
| IBM       | DJSA-220           | 12 GB  | 1       | 140   | 5     | 0.06   |
| Toshiba   | MK6032GAX          | 64 GB  | 1       | 23    | 0     | 0.06   |
| Toshiba   | MK8052GSX          | 80 GB  | 7       | 196   | 29    | 0.06   |
| Toshiba   | MK3265GSX H        | 320 GB | 2       | 44    | 15    | 0.06   |
| Toshiba   | MK6465GSXW         | 640 GB | 1       | 552   | 23    | 0.06   |
| Magnet... | MD02500-BQDW-RO    | 250 GB | 1       | 22    | 0     | 0.06   |
| WDC       | WD40EMAZ-11ZRJB0   | 4 TB   | 3       | 22    | 0     | 0.06   |
| WDC       | WD5000LPZX-35Z10T0 | 500 GB | 2       | 22    | 0     | 0.06   |
| WDC       | WD3200AVBS-63TAA0  | 320 GB | 1       | 741   | 32    | 0.06   |
| WDC       | WD5000AAKX-00PWEA0 | 500 GB | 1       | 918   | 40    | 0.06   |
| CLOVER    | CN-M750MBB         | 752 GB | 1       | 22    | 0     | 0.06   |
| Toshiba   | MK1032GAX          | 100 GB | 2       | 108   | 4     | 0.06   |
| WDC       | WD3200BEKX-22B7WT0 | 320 GB | 1       | 21    | 0     | 0.06   |
| Maxtor    | 6B200M0            | 200 GB | 7       | 29    | 19    | 0.06   |
| Seagate   | ST14000VE0008-2... | 14 TB  | 5       | 21    | 0     | 0.06   |
| WDC       | WD4000FYYZ-36UL1B0 | 4 TB   | 1       | 21    | 0     | 0.06   |
| Seagate   | ST3300831A         | 304 GB | 1       | 347   | 15    | 0.06   |
| Magnet... | MD01600-AVDW-RO    | 160 GB | 1       | 194   | 8     | 0.06   |
| Samsung   | HS06THB            | 64 GB  | 2       | 22    | 1044  | 0.06   |
| Maxtor    | 4K040H2            | 40 GB  | 2       | 249   | 19    | 0.06   |
| WDC       | WD5000AAKX-009FA0  | 500 GB | 1       | 230   | 10    | 0.06   |
| WDC       | WD400BB-22DEA0     | 40 GB  | 1       | 831   | 39    | 0.06   |
| Maxtor    | 6L200P0            | 208 GB | 5       | 22    | 5     | 0.06   |
| Toshiba   | MQ02ABF050H-SSH... | 500 GB | 2       | 20    | 0     | 0.06   |
| WDC       | WD2000BB-00GUC0    | 200 GB | 1       | 637   | 30    | 0.06   |
| WDC       | WD10SMZW-34Y0TS0   | 1 TB   | 1       | 20    | 0     | 0.06   |
| WDC       | WD5000BPVT-75A1YT0 | 500 GB | 1       | 20    | 0     | 0.06   |
| WDC       | WD20SPZX-11CRAT0   | 2 TB   | 1       | 20    | 0     | 0.06   |
| WDC       | WD2500BPVT-00ZEST0 | 250 GB | 3       | 136   | 74    | 0.06   |
| WDC       | WD1200BEVS-07LAT0  | 120 GB | 8       | 476   | 262   | 0.06   |
| MediaMax  | WL640GSA6472B      | 647 GB | 1       | 20    | 0     | 0.05   |
| WDC       | WD2500LPCX-24VHAT0 | 250 GB | 2       | 55    | 5     | 0.05   |
| IBM       | DARA-206000        | 6 GB   | 1       | 118   | 5     | 0.05   |
| Seagate   | ST9100822A         | 100 GB | 2       | 627   | 31    | 0.05   |
| Maxtor    | STM3300622A        | 304 GB | 1       | 173   | 8     | 0.05   |
| Maxtor    | 6L200M0            | 208 GB | 8       | 27    | 11    | 0.05   |
| Samsung   | HD160HJ            | 160 GB | 24      | 731   | 772   | 0.05   |
| Toshiba   | MK3276GSX          | 320 GB | 42      | 37    | 253   | 0.05   |
| WDC       | WD200EB-75CPF0     | 20 GB  | 2       | 402   | 20    | 0.05   |
| WDC       | WD5000LPVX-28V0TT1 | 500 GB | 1       | 172   | 8     | 0.05   |
| WDC       | WD1600JD-00GBB0    | 160 GB | 1       | 727   | 37    | 0.05   |
| Toshiba   | MQ01ABU050W        | 500 GB | 1       | 56    | 2     | 0.05   |
| WDC       | WD10EACS-22D6B1    | 1 TB   | 1       | 18    | 0     | 0.05   |
| WDC       | WD180EDGZ-11B2DA0  | 18 TB  | 2       | 18    | 0     | 0.05   |
| WDC       | WD5000LUCT-62RC2Y0 | 500 GB | 1       | 18    | 0     | 0.05   |
| Hitachi   | HCP725050GLAT80    | 500 GB | 1       | 240   | 12    | 0.05   |
| WDC       | WD7500BPVT-75HXZT1 | 752 GB | 1       | 547   | 29    | 0.05   |
| WDC       | WD800JD-75LSA0     | 80 GB  | 1       | 616   | 33    | 0.05   |
| WDC       | WD1600BB-55GUA0    | 160 GB | 2       | 661   | 134   | 0.05   |
| Samsung   | HM160HI            | 160 GB | 100     | 350   | 409   | 0.05   |
| Seagate   | ST91000430AS       | 1 TB   | 1       | 124   | 6     | 0.05   |
| WDC       | WD2500BEVT-60A23T0 | 250 GB | 7       | 341   | 308   | 0.05   |
| WDC       | WD5000AZLX-07K2TA0 | 500 GB | 9       | 17    | 0     | 0.05   |
| Seagate   | ST3500620AS        | 500 GB | 12      | 843   | 647   | 0.05   |
| Quantum   | FIREBALLlct15 10   | 10 GB  | 1       | 105   | 5     | 0.05   |
| WDC       | WD1600JS-55MHB0    | 160 GB | 1       | 761   | 43    | 0.05   |
| Seagate   | ST8000VE001-3AU101 | 8 TB   | 1       | 17    | 0     | 0.05   |
| WDC       | WD10JPVX-08JC3T1   | 1 TB   | 1       | 17    | 0     | 0.05   |
| Toshiba   | HDWG21C            | 12 TB  | 1       | 17    | 0     | 0.05   |
| Maxtor    | 6L080M0            | 80 GB  | 7       | 23    | 146   | 0.05   |
| Samsung   | SV1204H            | 120 GB | 1       | 474   | 27    | 0.05   |
| Hitachi   | HDP725032GLAT80    | 320 GB | 1       | 943   | 55    | 0.05   |
| Hitachi   | HTS543212L9A300    | 120 GB | 5       | 623   | 617   | 0.05   |
| Maxtor    | 6B300S0            | 304 GB | 2       | 17    | 1     | 0.05   |
| Seagate   | ST2000NM012A-2M... | 2 TB   | 4       | 16    | 0     | 0.05   |
| WDC       | WD10SMRW-11Y43S0   | 1 TB   | 6       | 16    | 0     | 0.05   |
| Seagate   | ST9500530NS 42D... | 500 GB | 1       | 1139  | 68    | 0.05   |
| Maxtor    | 6L080L0            | 82 GB  | 7       | 24    | 11    | 0.04   |
| Samsung   | HN-M250MBB         | 250 GB | 1       | 292   | 17    | 0.04   |
| Samsung   | HM060HI            | 64 GB  | 3       | 543   | 697   | 0.04   |
| Toshiba   | HDWT840            | 4 TB   | 1       | 16    | 0     | 0.04   |
| WDC       | WD60EDAZ-11BMZB0   | 6 TB   | 1       | 16    | 0     | 0.04   |
| Seagate   | ST3320310CS        | 320 GB | 9       | 720   | 71    | 0.04   |
| Seagate   | ST500LX025-1U71... | 500 GB | 1       | 15    | 0     | 0.04   |
| WDC       | WD800BB-88JHC0     | 80 GB  | 1       | 1625  | 101   | 0.04   |
| Maxtor    | 6B200P0            | 208 GB | 5       | 31    | 723   | 0.04   |
| IBM/Hi... | IC35L060AVVA07-0   | 64 GB  | 1       | 678   | 42    | 0.04   |
| HGST      | TPH00901000GB 0    | 1 TB   | 1       | 613   | 38    | 0.04   |
| IBM       | DTLA-307045        | 48 GB  | 1       | 346   | 21    | 0.04   |
| WDC       | WD121PURZ-85GUCY0  | 12 TB  | 5       | 15    | 0     | 0.04   |
| Samsung   | HM320JI            | 320 GB | 18      | 303   | 327   | 0.04   |
| Maxtor    | 6L300R0            | 304 GB | 6       | 20    | 4     | 0.04   |
| WDC       | WD5000BEVT-35ZAT0  | 500 GB | 2       | 586   | 533   | 0.04   |
| WDC       | WD4000ABYS-01TNA0  | 400 GB | 1       | 688   | 44    | 0.04   |
| Toshiba   | MK5059GSX          | 500 GB | 2       | 693   | 61    | 0.04   |
| Samsung   | SP1253N            | 120 GB | 1       | 286   | 18    | 0.04   |
| MediaMax  | WL250GSA872        | 250 GB | 1       | 15    | 0     | 0.04   |
| Seagate   | ST750LM028-1KK162  | 752 GB | 2       | 53    | 521   | 0.04   |
| Seagate   | ST9320421AS        | 320 GB | 8       | 433   | 43    | 0.04   |
| Seagate   | ST3000VM002-1ET166 | 3 TB   | 3       | 497   | 849   | 0.04   |
| Seagate   | OOS500G            | 500 GB | 1       | 14    | 0     | 0.04   |
| WDC       | WD3200AAKS-00M9A0  | 320 GB | 1       | 751   | 51    | 0.04   |
| Seagate   | ST9120310AS        | 120 GB | 1       | 14    | 0     | 0.04   |
| Maxtor    | 6L300S0            | 304 GB | 9       | 27    | 212   | 0.04   |
| WDC       | WD205BA            | 20 GB  | 1       | 296   | 20    | 0.04   |
| WDC       | WD10SPSX-22A6WT0   | 1 TB   | 4       | 13    | 0     | 0.04   |
| WDC       | WD1200VE-00KWT0    | 120 GB | 1       | 263   | 18    | 0.04   |
| Seagate   | ST1000NM004A-2M... | 1 TB   | 4       | 13    | 0     | 0.04   |
| WDC       | WD60EFAX-68JH4N0   | 6 TB   | 1       | 13    | 0     | 0.04   |
| Toshiba   | MK1656GSYF         | 160 GB | 1       | 96    | 6     | 0.04   |
| Seagate   | ST9250421ASG       | 250 GB | 2       | 355   | 26    | 0.04   |
| Seagate   | ST500LT012-9WS142  | 500 GB | 328     | 419   | 1085  | 0.04   |
| WDC       | WD5000AADS-98S9B1  | 500 GB | 1       | 120   | 8     | 0.04   |
| Toshiba   | MK3265GSXV         | 320 GB | 2       | 166   | 136   | 0.04   |
| WDC       | WD30EZRZ-60Z5HB0   | 3 TB   | 1       | 13    | 0     | 0.04   |
| WDC       | WD10PURZ-85BDSY0   | 1 TB   | 1       | 13    | 0     | 0.04   |
| WDC       | WD10TMVV-11TK7S1   | 1 TB   | 3       | 212   | 30    | 0.04   |
| WDC       | WD20SDZW-11JJ8S1   | 2 TB   | 1       | 12    | 0     | 0.04   |
| Maxtor    | 6L160M0            | 160 GB | 13      | 22    | 167   | 0.03   |
| Fujitsu   | MPG3204AT E        | 20 GB  | 1       | 138   | 10    | 0.03   |
| Maxtor    | 6L250S0            | 250 GB | 4       | 31    | 8     | 0.03   |
| Seagate   | ST3250412CS        | 250 GB | 1       | 12    | 0     | 0.03   |
| WDC       | WD1602ABKS-18N8A0  | 160 GB | 1       | 111   | 8     | 0.03   |
| WDC       | WD3200LPCX-00VHAT0 | 320 GB | 2       | 12    | 0     | 0.03   |
| Toshiba   | HDWV110            | 1 TB   | 1       | 12    | 0     | 0.03   |
| Maxtor    | 6L160P0            | 160 GB | 8       | 21    | 4     | 0.03   |
| WDC       | WD7500LPCX-22HWST0 | 752 GB | 1       | 129   | 10    | 0.03   |
| Maxtor    | 2F040L0            | 40 GB  | 5       | 22    | 5     | 0.03   |
| WDC       | WD20PURX-64P6ZYO   | 2 TB   | 1       | 139   | 11    | 0.03   |
| MaxDig... | MD3000GSA3257DVR 0 | 3 TB   | 1       | 11    | 0     | 0.03   |
| WDC       | WD800BB-00CAA0     | 80 GB  | 1       | 414   | 35    | 0.03   |
| Samsung   | HS030GB            | 32 GB  | 1       | 11    | 0     | 0.03   |
| Seagate   | ST320LT012-9WS14C  | 320 GB | 66      | 295   | 1075  | 0.03   |
| IBM       | ST3500641NS 39M... | 500 GB | 1       | 1423  | 124   | 0.03   |
| WDC       | WSH722020ALE6L0    | 20 TB  | 12      | 11    | 0     | 0.03   |
| Fujitsu   | MHT2040AT          | 40 GB  | 2       | 102   | 18    | 0.03   |
| Maxtor    | STM3320820A        | 320 GB | 1       | 11    | 0     | 0.03   |
| Hitachi   | HDS721025CLA382... | 160 GB | 1       | 2614  | 237   | 0.03   |
| Magnet... | MD07500-ALDW-RO    | 752 GB | 1       | 359   | 32    | 0.03   |
| WDC       | WD5000AAKS-19V0A0  | 500 GB | 1       | 1131  | 103   | 0.03   |
| Maxtor    | 7L250S0            | 250 GB | 2       | 13    | 1     | 0.03   |
| Hitachi   | DK23CA-20          | 20 GB  | 1       | 93    | 8     | 0.03   |
| WDC       | WD400ABJS-23TEA0   | 40 GB  | 1       | 10    | 0     | 0.03   |
| Maxtor    | STM3500323AS       | 500 GB | 1       | 40    | 3     | 0.03   |
| WDC       | WD20EZAZ-22L9GB0   | 2 TB   | 3       | 10    | 0     | 0.03   |
| Seagate   | ST500LM021-1KJ1... | 500 GB | 1       | 10    | 0     | 0.03   |
| Maxtor    | 2F040J0            | 40 GB  | 2       | 27    | 28    | 0.03   |
| Maxtor    | 6L120M0            | 122 GB | 3       | 29    | 15    | 0.03   |
| Samsung   | HM080HI            | 80 GB  | 5       | 338   | 461   | 0.03   |
| HGST      | HTE545032A7E380    | 320 GB | 1       | 9     | 0     | 0.03   |
| Maxtor    | 6Y120M0            | 122 GB | 6       | 32    | 36    | 0.03   |
| Samsung   | HM161JJ            | 160 GB | 1       | 96    | 9     | 0.03   |
| Seagate   | ST10000NM001G-2... | 10 TB  | 8       | 9     | 0     | 0.03   |
| WDC       | WD180PURZ-85AFFY0  | 18 TB  | 2       | 9     | 0     | 0.03   |
| Toshiba   | MK2016GAP          | 20 GB  | 1       | 349   | 36    | 0.03   |
| Seagate   | ST9100828AS        | 100 GB | 1       | 9     | 0     | 0.03   |
| WDC       | WD800BD-00MRA1     | 80 GB  | 1       | 1944  | 210   | 0.03   |
| Samsung   | HD322IJ            | 320 GB | 1       | 469   | 51    | 0.02   |
| Seagate   | ST92505610AS       | 250 GB | 1       | 775   | 85    | 0.02   |
| WDC       | WD800JD-75JNC0     | 80 GB  | 2       | 858   | 355   | 0.02   |
| WDC       | WD10EZEX-60WN4A2   | 1 TB   | 2       | 8     | 0     | 0.02   |
| Seagate   | OOS1000G128M       | 1 TB   | 1       | 143   | 16    | 0.02   |
| WDC       | WD3200BEVT-80A0RT1 | 320 GB | 2       | 1035  | 140   | 0.02   |
| WDC       | WD10SDSW-11AGTS0   | 1 TB   | 1       | 8     | 0     | 0.02   |
| Samsung   | HS12RJF            | 120 GB | 1       | 96    | 11    | 0.02   |
| Hitachi   | HTS548080M9AT00    | 80 GB  | 1       | 136   | 16    | 0.02   |
| ExcelStor | J9250              | 250 GB | 1       | 1349  | 167   | 0.02   |
| MediaMax  | WL250GLSA6410000   | 250 GB | 2       | 36    | 4     | 0.02   |
| Seagate   | ST6000DX000-1H217Z | 6 TB   | 2       | 7     | 0     | 0.02   |
| HGST      | QC-FT-D H20GB-5... | 20 GB  | 1       | 7     | 0     | 0.02   |
| WDC       | WD5000AZLX-00ZR6A0 | 500 GB | 1       | 7     | 0     | 0.02   |
| Maxtor    | 6E040L0            | 40 GB  | 15      | 30    | 26    | 0.02   |
| Maxtor    | 2F030J0            | 32 GB  | 3       | 32    | 84    | 0.02   |
| MaxDig... | MDT MD2000KS-00... | 200 GB | 1       | 579   | 75    | 0.02   |
| Seagate   | ST310212A          | 10 GB  | 2       | 236   | 42    | 0.02   |
| Maxtor    | 6Y060L2            | 64 GB  | 1       | 542   | 71    | 0.02   |
| Maxtor    | 6K040L0            | 41 GB  | 1       | 29    | 3     | 0.02   |
| Seagate   | ST9250421AS        | 250 GB | 2       | 296   | 70    | 0.02   |
| Hitachi   | DK23EA-20B         | 17 GB  | 1       | 183   | 24    | 0.02   |
| WDC       | WD2000JS-00NCB1    | 200 GB | 1       | 537   | 73    | 0.02   |
| WDC       | WD400BB-75CAA0     | 40 GB  | 1       | 564   | 77    | 0.02   |
| Seagate   | ST730212DE         | 32 GB  | 1       | 7     | 0     | 0.02   |
| Samsung   | HD254GJ            | 250 GB | 1       | 710   | 100   | 0.02   |
| Seagate   | ST4000NM0115-1Y... | 4 TB   | 3       | 7     | 0     | 0.02   |
| WDC       | WD2500AAJS-41RYA0  | 250 GB | 1       | 76    | 10    | 0.02   |
| Samsung   | SP1614N            | 160 GB | 2       | 837   | 120   | 0.02   |
| Hitachi   | HTS723225L9A360    | 250 GB | 7       | 553   | 1012  | 0.02   |
| Hitachi   | HTS721010G9AT00    | 100 GB | 1       | 6     | 0     | 0.02   |
| WDC       | WD10SPZX-16Z10T1   | 1 TB   | 1       | 6     | 0     | 0.02   |
| Maxtor    | 6L200S0            | 208 GB | 2       | 20    | 21    | 0.02   |
| WDC       | WD800BD-00LRA1     | 80 GB  | 1       | 382   | 57    | 0.02   |
| Hitachi   | HCC543232A7A380    | 320 GB | 2       | 323   | 92    | 0.02   |
| Maxtor    | 6Y120L0            | 122 GB | 9       | 27    | 26    | 0.02   |
| Toshiba   | MK6465GSXNW        | 640 GB | 1       | 284   | 43    | 0.02   |
| WDC       | WD360ADFD-00NLR4   | 37 GB  | 1       | 499   | 77    | 0.02   |
| HPE       | MB004000GWWQH      | 4 TB   | 1       | 6     | 0     | 0.02   |
| Seagate   | ST94019A           | 40 GB  | 1       | 225   | 35    | 0.02   |
| Fujitsu   | MHV2120BH PL       | 120 GB | 13      | 17    | 2     | 0.02   |
| WDC       | WD2500BEVT-00SCST0 | 250 GB | 1       | 5     | 0     | 0.02   |
| Maxtor    | 6E030L0            | 32 GB  | 6       | 15    | 20    | 0.02   |
| Samsung   | HM100JI            | 100 GB | 1       | 827   | 140   | 0.02   |
| Toshiba   | MK5061GSY          | 500 GB | 15      | 9     | 14    | 0.02   |
| Hitachi   | HTS541612J9AT00    | 120 GB | 1       | 116   | 19    | 0.02   |
| MediaMax  | WL1500GSA3272      | 1.5 TB | 1       | 2210  | 391   | 0.02   |
| Seagate   | ST3500820AS        | 500 GB | 11      | 614   | 224   | 0.02   |
| Maxtor    | 85400D5            | 5 GB   | 1       | 5613  | 1044  | 0.01   |
| WDC       | WD7500BMVW-11AJGS4 | 752 GB | 1       | 5     | 0     | 0.01   |
| Maxtor    | 6Y080M0            | 80 GB  | 17      | 27    | 129   | 0.01   |
| Seagate   | ST1000LM002-9VQ14L | 1 TB   | 1       | 25    | 4     | 0.01   |
| Seagate   | ST4000VX005-2LY104 | 4 TB   | 3       | 5     | 0     | 0.01   |
| WDC       | WD1200AAJS-00VTA0  | 120 GB | 1       | 995   | 203   | 0.01   |
| Hitachi   | HTE721060G9AT00    | 64 GB  | 1       | 4     | 0     | 0.01   |
| Seagate   | ST980829A          | 80 GB  | 2       | 116   | 1011  | 0.01   |
| Toshiba   | MK1676GSX          | 160 GB | 2       | 16    | 447   | 0.01   |
| Maxtor    | 6Y080P0            | 82 GB  | 8       | 17    | 6     | 0.01   |
| Toshiba   | MK8050GAC          | 80 GB  | 1       | 878   | 197   | 0.01   |
| Maxtor    | 6L080P0            | 82 GB  | 3       | 11    | 10    | 0.01   |
| Maxtor    | 4R060J0            | 64 GB  | 1       | 25    | 5     | 0.01   |
| Fujitsu   | MHZ2160BJ G1       | 160 GB | 1       | 4     | 0     | 0.01   |
| WDC       | WD2500BEKT-66F3T2  | 250 GB | 1       | 193   | 50    | 0.01   |
| Hitachi   | HCS721050CLA362    | 500 GB | 1       | 3     | 0     | 0.01   |
| Seagate   | ST3750630AS        | 752 GB | 4       | 697   | 791   | 0.01   |
| Seagate   | ST3250310SV        | 250 GB | 1       | 287   | 79    | 0.01   |
| Maxtor    | 6Y160P0            | 163 GB | 8       | 22    | 109   | 0.01   |
| Samsung   | HD256GM            | 250 GB | 1       | 3558  | 1009  | 0.01   |
| WDC       | WD1600BB-55GUC0    | 160 GB | 1       | 332   | 94    | 0.01   |
| Hitachi   | HTS541640J9AT00    | 40 GB  | 1       | 283   | 82    | 0.01   |
| HGST      | HTS725050A7E635    | 500 GB | 2       | 490   | 557   | 0.01   |
| Fujitsu   | MJA2320BH G1       | 320 GB | 2       | 577   | 168   | 0.01   |
| WDC       | WD10EADS-00R6B0    | 1 TB   | 1       | 1856  | 560   | 0.01   |
| Fujitsu   | MPE3136AT          | 16 GB  | 1       | 794   | 240   | 0.01   |
| Maxtor    | 6E020L0            | 21 GB  | 1       | 22    | 6     | 0.01   |
| IBM/Hi... | IC35L060AVER07-0   | 64 GB  | 2       | 546   | 167   | 0.01   |
| Seagate   | ST6000NE0021-2E... | 6 TB   | 1       | 3     | 0     | 0.01   |
| Seagate   | ST64022CF          |        | 1       | 3     | 0     | 0.01   |
| WDC       | WD2004FBYZ-01YCBB0 | 2 TB   | 1       | 12    | 3     | 0.01   |
| WDC       | TP00250GB          | 250 GB | 1       | 1073  | 351   | 0.01   |
| Maxtor    | 6B160M0            | 163 GB | 1       | 3     | 0     | 0.01   |
| Seagate   | ST8000NM0105       | 8 TB   | 2       | 2     | 0     | 0.01   |
| WDC       | WD40NDZW-11BHVS1   | 4 TB   | 1       | 2     | 0     | 0.01   |
| WDC       | WD800UE-22HCT0     | 80 GB  | 2       | 568   | 272   | 0.01   |
| HGST      | HTS545025A7E680    | 250 GB | 1       | 25    | 8     | 0.01   |
| MARSHAL   | MAL2040SA-T54L     | 40 GB  | 1       | 2     | 0     | 0.01   |
| Toshiba   | MAL2040SA-T54L     | 40 GB  | 1       | 2     | 0     | 0.01   |
| Toshiba   | MG08ADA800E        | 8 TB   | 1       | 2     | 0     | 0.01   |
| WDC       | WD1600BEKT-75PVMT0 | 160 GB | 2       | 909   | 396   | 0.01   |
| Maxtor    | 6Y120P0            | 122 GB | 3       | 21    | 28    | 0.01   |
| WDC       | WD1200BEVS-75LAT0  | 118 GB | 1       | 1008  | 378   | 0.01   |
| Maxtor    | 6Y080L0            | 80 GB  | 45      | 20    | 289   | 0.01   |
| Seagate   | ST500LM020-1G1162  | 500 GB | 3       | 2     | 0     | 0.01   |
| Toshiba   | MQ01ACF050R        | 500 GB | 1       | 2     | 0     | 0.01   |
| WDC       | WD10JPVX-28JC3T1   | 1 TB   | 1       | 2     | 0     | 0.01   |
| WDC       | WD15SMZW-11YFCS0   | 1.5 TB | 1       | 2     | 0     | 0.01   |
| Samsung   | SV0802N            | 80 GB  | 1       | 554   | 215   | 0.01   |
| WDC       | RFT030VQFF-KRM5P7  | 3 TB   | 1       | 129   | 50    | 0.01   |
| Seagate   | ST500NM0011 39M... | 500 GB | 1       | 2520  | 1007  | 0.01   |
| WDC       | WD1600BUDT-73DPZY0 | 160 GB | 1       | 22    | 8     | 0.01   |
| WDC       | WD181KFGX-68AFPN0  | 18 TB  | 6       | 2     | 0     | 0.01   |
| WDC       | WD3200AADS-00S9B0  | 320 GB | 1       | 26    | 10    | 0.01   |
| Maxtor    | 6Y200P0            | 208 GB | 2       | 20    | 9     | 0.01   |
| Seagate   | ST8000DX001-3GK101 | 8 TB   | 1       | 2     | 0     | 0.01   |
| Seagate   | ST10000VN000-3A... | 10 TB  | 1       | 2     | 0     | 0.01   |
| MARSHAL   | MAL2020SA 80       | 20 GB  | 1       | 4     | 1     | 0.01   |
| WDC       | INO-IHDD0250S2-... | 250 GB | 1       | 18    | 8     | 0.01   |
| Hitachi   | HDS722516VLAT20    | 164 GB | 1       | 2242  | 1102  | 0.01   |
| WDC       | WD10SDRW-34A0XS0   | 1 TB   | 1       | 1     | 0     | 0.01   |
| WDC       | WD6400AAKS-00E4A0  | 640 GB | 1       | 1016  | 521   | 0.01   |
| WDC       | WD10EURX-63UHWY0   | 1 TB   | 1       | 644   | 338   | 0.01   |
| WDC       | WD4000AAKS-22TMA0  | 400 GB | 1       | 820   | 431   | 0.01   |
| HGST      | MB3000EBUCH        | 3 TB   | 1       | 765   | 406   | 0.01   |
| Samsung   | HM160JI            | 160 GB | 6       | 304   | 1043  | 0.01   |
| WDC       | WD20EARS-19MVWB0   | 2 TB   | 1       | 713   | 392   | 0.00   |
| Fujitsu   | MHY2080BS          | 80 GB  | 1       | 2382  | 1317  | 0.00   |
| WDC       | WD400ZB-00JYA0     | 40 GB  | 1       | 927   | 520   | 0.00   |
| Toshiba   | MK2533GSG          | 250 GB | 1       | 1671  | 948   | 0.00   |
| Hitachi   | HUA5C3020ALA640    | 2 TB   | 1       | 1045  | 595   | 0.00   |
| CLOVER    | CD155UI            | 1.5 TB | 1       | 1     | 0     | 0.00   |
| IBM/Hi... | IC35L120AVVA07-0   | 128 GB | 1       | 918   | 552   | 0.00   |
| WDC       | WD800JB-00CRA1     | 80 GB  | 1       | 538   | 323   | 0.00   |
| Maxtor    | 2F020J0            | 21 GB  | 2       | 22    | 67    | 0.00   |
| WDC       | WD140PURZ-85GG1Y0  | 14 TB  | 4       | 1     | 0     | 0.00   |
| Apple     | HDD HUA722010CL... | 1 TB   | 2       | 176   | 110   | 0.00   |
| WDC       | WD7501AAES-60Z2A0  | 752 GB | 1       | 1058  | 666   | 0.00   |
| Samsung   | HD251KJ            | 250 GB | 1       | 1539  | 1019  | 0.00   |
| Seagate   | ST3120023AS        | 120 GB | 1       | 152   | 101   | 0.00   |
| WDC       | WD3200AAKX-00U6AA0 | 320 GB | 1       | 83    | 56    | 0.00   |
| Samsung   | HN-M500XBB         | 500 GB | 1       | 1     | 0     | 0.00   |
| Maxtor    | 2B020H1            | 20 GB  | 12      | 23    | 165   | 0.00   |
| Hitachi   | HUA722010CLA330... | 1 TB   | 1       | 161   | 112   | 0.00   |
| WDC       | WD2500JD-98GBB0    | 250 GB | 1       | 875   | 628   | 0.00   |
| Maxtor    | 4R160L0            | 163 GB | 1       | 5     | 3     | 0.00   |
| WDC       | WD2500AAJS-40VWA1  | 250 GB | 1       | 999   | 759   | 0.00   |
| Seagate   | ST8000NC0002-1X... | 8 TB   | 1       | 107   | 82    | 0.00   |
| WDC       | WD15EADS-11P8B1    | 1.5 TB | 2       | 908   | 934   | 0.00   |
| WDC       | WD3200LPCX-60VHAT0 | 320 GB | 1       | 1     | 0     | 0.00   |
| WDC       | WUS721010ALE6L4    | 10 TB  | 1       | 1     | 0     | 0.00   |
| Fujitsu   | MHT2060AT          | 64 GB  | 1       | 302   | 241   | 0.00   |
| WDC       | WD1200             | 120 GB | 1       | 11    | 8     | 0.00   |
| Maxtor    | 4D040H2            | 41 GB  | 4       | 24    | 191   | 0.00   |
| Toshiba   | MK4026GAX          | 40 GB  | 1       | 191   | 157   | 0.00   |
| Hitachi   | HCS5C1050DLE630    | 500 GB | 1       | 885   | 737   | 0.00   |
| Toshiba   | MK7559GSM          | 752 GB | 1       | 1015  | 847   | 0.00   |
| WDC       | WD400BB-00CAA0     | 40 GB  | 1       | 194   | 163   | 0.00   |
| Seagate   | ST9888430AS        | 888 GB | 2       | 678   | 1426  | 0.00   |
| Seagate   | ST9320327AS        | 320 GB | 1       | 725   | 705   | 0.00   |
| WDC       | WD7500KMVV-11BG7S0 | 752 GB | 1       | 679   | 698   | 0.00   |
| Fujitsu   | MHV2160BT          | 160 GB | 1       | 483   | 535   | 0.00   |
| Seagate   | ST9160418ASG       | 160 GB | 1       | 555   | 625   | 0.00   |
| Toshiba   | HDWD320            | 2 TB   | 1       | 0     | 0     | 0.00   |
| Hitachi   | HTS723216L9A360    | 160 GB | 8       | 423   | 1365  | 0.00   |
| WDC       | WD600UE-22HCT0     | 64 GB  | 1       | 204   | 237   | 0.00   |
| Hitachi   | HTS725032A9A365    | 320 GB | 2       | 859   | 1023  | 0.00   |
| WDC       | RAT015VQHB-DSG2D7  | 1.5 TB | 1       | 0     | 0     | 0.00   |
| WDC       | RFT030VQHR-GTK4D   | 3 TB   | 1       | 0     | 0     | 0.00   |
| Toshiba   | MK3256GSY          | 320 GB | 10      | 5     | 360   | 0.00   |
| Maxtor    | 4R120L0            | 122 GB | 3       | 30    | 39    | 0.00   |
| HGST      | TPH00100500GB 0... | 500 GB | 1       | 8     | 10    | 0.00   |
| HP        | GB1000EAFJL        | 1 TB   | 1       | 2402  | 3024  | 0.00   |
| WDC       | WD800BEVT-26ZCT0   | 80 GB  | 1       | 0     | 0     | 0.00   |
| Maxtor    | 4G120J6            | 122 GB | 2       | 20    | 218   | 0.00   |
| WDC       | WD3200LPCX-22VHAT0 | 320 GB | 2       | 373   | 459   | 0.00   |
| Maxtor    | 6Y060L0            | 64 GB  | 5       | 23    | 84    | 0.00   |
| Maxtor    | STM3750330AS       | 752 GB | 1       | 995   | 1293  | 0.00   |
| MediaMax  | WL400GSA6454G      | 400 GB | 1       | 0     | 0     | 0.00   |
| Maxtor    | 7Y250M0            | 250 GB | 2       | 27    | 37    | 0.00   |
| Fujitsu   | MHV2200BT          | 200 GB | 1       | 382   | 518   | 0.00   |
| Seagate   | ST360012A          | 64 GB  | 1       | 194   | 274   | 0.00   |
| Seagate   | ST3320620SV        | 320 GB | 1       | 564   | 835   | 0.00   |
| Seagate   | ST500LT015-9WU142  | 500 GB | 2       | 708   | 1108  | 0.00   |
| Seagate   | ST4000NM0265-2D... | 4 TB   | 1       | 0     | 0     | 0.00   |
| Seagate   | ST3320410SV        | 320 GB | 1       | 685   | 1110  | 0.00   |
| Seagate   | ST500DM009-1BD142  | 500 GB | 1       | 0     | 0     | 0.00   |
| Maxtor    | 4D060H3            | 64 GB  | 1       | 18    | 31    | 0.00   |
| Hitachi   | DK23CA-30          | 32 GB  | 1       | 532   | 919   | 0.00   |
| Seagate   | ST2000LX001-1RG... | 2 TB   | 1       | 283   | 507   | 0.00   |
| Maxtor    | 6Y160M0            | 160 GB | 8       | 18    | 166   | 0.00   |
| Hitachi   | HTS723212L9A360    | 120 GB | 1       | 535   | 1012  | 0.00   |
| Hitachi   | HTS723232A7A365    | 320 GB | 1       | 1130  | 2203  | 0.00   |
| WDC       | WD22EJRX-89BEMY0   | 2 TB   | 1       | 0     | 0     | 0.00   |
| Seagate   | ST250LT012-1DG141  | 250 GB | 1       | 500   | 1007  | 0.00   |
| Fujitsu   | MHK2120AT          | 12 GB  | 1       | 77    | 155   | 0.00   |
| Seagate   | ST3250311SV        | 250 GB | 2       | 486   | 1035  | 0.00   |
| WDC       | WD10EZEX-08WN4A1   | 1 TB   | 2       | 0     | 0     | 0.00   |
| WDC       | WD15EURS-63S48Y0   | 1.5 TB | 1       | 11    | 26    | 0.00   |
| WDC       | WD2500BB-22RDA0    | 250 GB | 1       | 655   | 1524  | 0.00   |
| Seagate   | ST320LT000-9VL142  | 320 GB | 2       | 402   | 1009  | 0.00   |
| Seagate   | ST3802110ACE       | 80 GB  | 1       | 1203  | 3052  | 0.00   |
| Seagate   | ST9100821AS        | 100 GB | 1       | 392   | 1009  | 0.00   |
| Hitachi   | HDP725040GLA380    | 400 GB | 1       | 215   | 554   | 0.00   |
| Samsung   | HM500LX            | 500 GB | 2       | 133   | 293   | 0.00   |
| Hitachi   | HTS725050A7E635    | 500 GB | 2       | 429   | 1165  | 0.00   |
| WDC       | WD8088AADS-00M2B0  | 808 GB | 1       | 676   | 1936  | 0.00   |
| Seagate   | ST3500321CS        | 500 GB | 1       | 48    | 137   | 0.00   |
| MARSHAL   | MAL2500SA-T54L     | 500 GB | 1       | 90    | 262   | 0.00   |
| Hitachi   | HTS722080K9SA00    | 80 GB  | 2       | 339   | 1017  | 0.00   |
| WDC       | WD3200L22X-00JVPT0 | 320 GB | 1       | 0     | 0     | 0.00   |
| Maxtor    | 7L300S0            | 304 GB | 3       | 13    | 40    | 0.00   |
| WDC       | WD2500BEKT-60F3T1  | 250 GB | 1       | 533   | 1607  | 0.00   |
| WDC       | WD5000BEVT-60ZAT0  | 500 GB | 1       | 381   | 1160  | 0.00   |
| Samsung   | HD402LJ            | 400 GB | 1       | 316   | 1018  | 0.00   |
| Seagate   | ST980817AS         | 80 GB  | 1       | 310   | 1009  | 0.00   |
| WDC       | WD2500AAKS-60L9A0  | 250 GB | 1       | 282   | 937   | 0.00   |
| Seagate   | ST250LT012-9WS141  | 250 GB | 5       | 363   | 1224  | 0.00   |
| WDC       | WD1600AAJS-56WAA0  | 160 GB | 1       | 299   | 1021  | 0.00   |
| Toshiba   | HDWR460            | 6 TB   | 1       | 0     | 0     | 0.00   |
| WDC       | WD5000L            | 500 GB | 1       | 88    | 302   | 0.00   |
| WDC       | WD20EZRX-00SPEB0   | 2 TB   | 1       | 574   | 2072  | 0.00   |
| Seagate   | ST3640623AS        | 640 GB | 1       | 55    | 209   | 0.00   |
| Hitachi   | HTS542580K9A300    | 80 GB  | 2       | 267   | 1012  | 0.00   |
| Seagate   | ST9320312AS        | 320 GB | 2       | 264   | 1108  | 0.00   |
| WDC       | WD5000AAVS-00G9B1  | 500 GB | 1       | 257   | 1020  | 0.00   |
| Samsung   | HM252HX            | 250 GB | 1       | 0     | 3     | 0.00   |
| Samsung   | SV2011H            | 20 GB  | 1       | 0     | 3     | 0.00   |
| WDC       | WD2500AAJS-55B4A0  | 250 GB | 1       | 476   | 2020  | 0.00   |
| WDC       | WD800 AAJS-00PSA0  | 80 GB  | 1       | 97    | 459   | 0.00   |
| Maxtor    | 6B120P0            | 122 GB | 1       | 0     | 0     | 0.00   |
| Seagate   | ST1000LM014-1EJ... | 1 TB   | 1       | 202   | 1009  | 0.00   |
| China     | Generic S050 Ha... | 500 GB | 1       | 245   | 1377  | 0.00   |
| Toshiba   | MK6461GSYN         | 640 GB | 1       | 0     | 0     | 0.00   |
| WDC       | WD450VF4YZ-49SJYM0 | 4.5 TB | 1       | 0     | 0     | 0.00   |
| WDC       | WD50NDZW-11A8JS0   | 5 TB   | 1       | 0     | 0     | 0.00   |
| Samsung   | HM320JX            | 320 GB | 1       | 37    | 331   | 0.00   |
| HPE       | MB0500EAMZD        | 500 GB | 1       | 94    | 857   | 0.00   |
| Seagate   | MB0500EAMZD        | 500 GB | 1       | 94    | 857   | 0.00   |
| Maxtor    | 7L300R0            | 304 GB | 1       | 11    | 116   | 0.00   |
| Hitachi   | DK23AA-60          | 6 GB   | 1       | 3     | 38    | 0.00   |
| China     | TPH00800640GB 0    | 640 GB | 1       | 82    | 1007  | 0.00   |
| Toshiba   | MK8025GAL          | 80 GB  | 1       | 79    | 1017  | 0.00   |
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
| WDC       | WD7500AADS-00L5B1  | 752 GB | 1       | 0     | 1     | 0.00   |
| Hitachi   | HTS721060G9AT00    | 64 GB  | 1       | 0     | 37    | 0.00   |
| Fujitsu   | MHZ2250BJ G2       | 250 GB | 1       | 12    | 1044  | 0.00   |
| Seagate   | ST380020A          | 80 GB  | 1       | 2     | 225   | 0.00   |
| Fujitsu   | MHZ2160BJ G2       | 160 GB | 1       | 6     | 1025  | 0.00   |
| ExcelStor | G140               | 40 GB  | 1       | 0     | 1010  | 0.00   |
| Maxtor    | 90680D4            | 7 GB   | 1       | 0     | 1152  | 0.00   |

HDD by Family
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

| MFG       | Family                 | Models | Samples | Days  | Err   | MTBF |
|-----------|------------------------|--------|---------|-------|-------|------|
| Samsung   | SpinPoint M40S         | 1      | 2       | 6601  | 0     | 18.09  |
| Samsung   | SpinPoint V20400       | 1      | 1       | 5713  | 0     | 15.65  |
| HP        | Seagate Barracuda 7... | 1      | 2       | 3447  | 0     | 9.44   |
| Hitachi   | Sun Original           | 2      | 13      | 2736  | 0     | 7.50   |
| Seagate   | Barracuda ES+          | 2      | 2       | 2323  | 0     | 6.37   |
| Advantech | Unknown                | 1      | 1       | 2258  | 0     | 6.19   |
| Hitachi   | Deskstar 7K4000        | 1      | 8       | 2332  | 171   | 6.14   |
| Fujitsu   | MHZ BK                 | 1      | 1       | 2160  | 0     | 5.92   |
| Toshiba   | 3.5" HDD MK.002TSKB    | 2      | 11      | 2171  | 3     | 5.53   |
| Toshiba   | Toshiba Client HDD     | 1      | 1       | 1874  | 0     | 5.13   |
| WDC       | RE EIDE                | 1      | 1       | 1755  | 0     | 4.81   |
| Hitachi   | Deskstar 7K250 (SUN... | 1      | 1       | 5248  | 2     | 4.79   |
| Seagate   | Constellation ES.2     | 1      | 2       | 1727  | 0     | 4.73   |
| Samsung   | SpinPoint PL40         | 1      | 2       | 3755  | 9     | 4.62   |
| WDC       | Green Mobile           | 3      | 37      | 1880  | 5     | 4.52   |
| Hitachi   | Ultrastar A7K1000      | 6      | 29      | 2138  | 69    | 4.49   |
| Toshiba   | 3.5" HDD               | 1      | 2       | 1548  | 0     | 4.24   |
| HPE       | WDC Enterprise         | 1      | 1       | 1526  | 0     | 4.18   |
| Seagate   | SpinPoint F4 EG (AF)   | 1      | 7       | 1523  | 0     | 4.17   |
| Quantum   | Unknown                | 1      | 1       | 1486  | 0     | 4.07   |
| WDC       | Caviar WDxxxAA         | 2      | 2       | 1697  | 6     | 4.03   |
| Seagate   | Seagate Enterprise     | 1      | 5       | 1433  | 0     | 3.93   |
| Seagate   | Barracuda 7200.7       | 1      | 6       | 1654  | 35    | 3.92   |
| Seagate   | Constellation.2 (SATA) | 3      | 33      | 1578  | 2     | 3.84   |
| WDC       | RE3                    | 21     | 127     | 1800  | 9     | 3.74   |
| Samsung   | SpinPoint F1 RE        | 2      | 5       | 1945  | 21    | 3.67   |
| HGST      | Ultrastar 7K4000       | 7      | 137     | 1379  | 16    | 3.66   |
| Hitachi   | Deskstar 7K3000        | 8      | 134     | 1538  | 75    | 3.64   |
| Maxtor    | DiamondMax 11          | 1      | 1       | 1294  | 0     | 3.55   |
| HP        | Seagate Constellati... | 1      | 1       | 1272  | 0     | 3.49   |
| WDC       | RE2                    | 8      | 21      | 1577  | 30    | 3.46   |
| HP        | Constellation ES.3     | 1      | 5       | 1687  | 2     | 3.44   |
| Hitachi   | Deskstar 7K2000        | 2      | 58      | 1911  | 106   | 3.36   |
| Apple     | Unknown                | 1      | 1       | 1200  | 0     | 3.29   |
| Seagate   | Archive HDD            | 3      | 127     | 1389  | 66    | 3.26   |
| Seagate   | NAS HDD                | 8      | 78      | 1244  | 28    | 3.23   |
| Hitachi   | Ultrastar A7K2000      | 11     | 103     | 1678  | 60    | 3.22   |
| Hitachi   | CinemaStar 5K2000      | 1      | 3       | 1986  | 4     | 3.22   |
| Maxtor    | DiamondMax 8s          | 1      | 2       | 1842  | 1     | 3.21   |
| Hitachi   | CinemaStar C5K500      | 2      | 4       | 1167  | 0     | 3.20   |
| WDC       | Raptor X               | 1      | 1       | 1164  | 0     | 3.19   |
| Toshiba   | 1.8" HDD MK..17GSG     | 1      | 1       | 1162  | 0     | 3.18   |
| Seagate   | Exos 7E2               | 5      | 33      | 1193  | 12    | 3.16   |
| HGST      | Deskstar 7K4000        | 2      | 17      | 1371  | 123   | 3.09   |
| HGST      | Deskstar NAS           | 9      | 110     | 1184  | 28    | 3.06   |
| HP        | Proliant HardDrive     | 13     | 28      | 1548  | 129   | 3.01   |
| Samsung   | SpinPoint F3R          | 1      | 2       | 2131  | 1     | 2.99   |
| WDC       | Se                     | 7      | 30      | 1182  | 4     | 2.93   |
| Hitachi   | Deskstar 7K500         | 2      | 17      | 1945  | 27    | 2.92   |
| Hitachi   | Unknown                | 10     | 16      | 1574  | 135   | 2.84   |
| Apple     | Seagate Barracuda 7... | 1      | 2       | 1034  | 0     | 2.84   |
| WDC       | Purple NV              | 1      | 1       | 1023  | 0     | 2.80   |
| Hitachi   | Ultrastar 7K3000       | 4      | 143     | 1194  | 33    | 2.76   |
| Samsung   | SpinPoint F4 EG (AF)   | 2      | 87      | 1202  | 80    | 2.73   |
| WDC       | VelociRaptor           | 38     | 125     | 1200  | 21    | 2.72   |
| HGST      | MegaScale 4000         | 2      | 22      | 973   | 0     | 2.67   |
| Hitachi   | Deskstar 5K3000        | 5      | 58      | 1301  | 40    | 2.66   |
| WDC       | Caviar Black           | 58     | 791     | 1260  | 38    | 2.64   |
| Apple     | Travelstar 7K750       | 1      | 4       | 960   | 0     | 2.63   |
| Seagate   | Constellation.2        | 3      | 3       | 958   | 0     | 2.63   |
| WDC       | RE4-GP                 | 8      | 31      | 1771  | 47    | 2.60   |
| Seagate   | Momentus Xt            | 1      | 4       | 1051  | 8     | 2.58   |
| Seagate   | Constellation ES.2 ... | 4      | 29      | 1372  | 55    | 2.58   |
| Toshiba   | Low spin               | 1      | 3       | 936   | 0     | 2.57   |
| Seagate   | U5                     | 4      | 7       | 992   | 2     | 2.56   |
| Hitachi   | Deskstar E7K1000       | 2      | 14      | 1895  | 16    | 2.56   |
| Seagate   | Laptop Thin            | 1      | 2       | 932   | 0     | 2.56   |
| Hitachi   | Deskstar 7K250         | 9      | 26      | 1387  | 143   | 2.55   |
| Seagate   | Barracuda XT           | 5      | 44      | 1309  | 149   | 2.53   |
| Seagate   | Constellation CS       | 4      | 25      | 1230  | 196   | 2.51   |
| WDC       | Caviar SE16            | 6      | 54      | 1139  | 13    | 2.48   |
| Hitachi   | Deskstar E7K500        | 2      | 3       | 902   | 0     | 2.47   |
| Hitachi   | CinemaStar 5K1000      | 4      | 11      | 931   | 1     | 2.42   |
| Toshiba   | 3.5" MD04ACA Enterp... | 2      | 40      | 1065  | 189   | 2.41   |
| Seagate   | Desktop HDD.15         | 6      | 208     | 1052  | 111   | 2.40   |
| HP        | 250GB SATA disk VB0... | 1      | 20      | 1200  | 3     | 2.36   |
| HGST      | Ultrastar 7K6000       | 13     | 68      | 892   | 9     | 2.35   |
| Samsung   | Unknown                | 4      | 4       | 2013  | 262   | 2.33   |
| Quantum   | Fireball Plus AS       | 2      | 2       | 845   | 0     | 2.32   |
| Samsung   | SpinPoint F3 RE        | 1      | 6       | 2421  | 24    | 2.31   |
| Hitachi   | CinemaStar P7K500      | 4      | 10      | 999   | 2     | 2.28   |
| Seagate   | Exos X12               | 1      | 20      | 919   | 9     | 2.24   |
| HP        | RE3                    | 1      | 2       | 814   | 0     | 2.23   |
| Hitachi   | CinemaStar 5K320       | 2      | 7       | 976   | 2     | 2.23   |
| Toshiba   | 3.5" MG03ACAxxx(Y) ... | 4      | 42      | 966   | 12    | 2.22   |
| HGST      | CinemaStar Z7K500      | 1      | 1       | 810   | 0     | 2.22   |
| Hitachi   | Deskstar 7K1000        | 3      | 28      | 1225  | 12    | 2.20   |
| Toshiba   | 3.5" DT01ABA Deskto... | 3      | 36      | 819   | 1     | 2.19   |
| WDC       | RE                     | 34     | 119     | 1132  | 62    | 2.18   |
| Toshiba   | 3.5" HDD E300          | 2      | 14      | 883   | 2     | 2.16   |
| Seagate   | Constellation ES.3     | 8      | 119     | 1086  | 162   | 2.16   |
| WDC       | RE4                    | 28     | 251     | 1135  | 30    | 2.16   |
| HGST      | Travelstar 5K1500      | 2      | 9       | 966   | 118   | 2.13   |
| Seagate   | Enterprise Capacity... | 20     | 256     | 875   | 16    | 2.13   |
| Seagate   | Enterprise NAS HDD     | 4      | 7       | 778   | 1     | 2.09   |
| Toshiba   | 3.5" MG04ACA Enterp... | 5      | 25      | 755   | 1     | 2.07   |
| WDC       | Caviar Green           | 179    | 2989    | 1103  | 70    | 2.06   |
| Toshiba   | 2.5" HDD MQ01ABB       | 1      | 27      | 866   | 171   | 2.05   |
| Hitachi   | Deskstar T7K500        | 8      | 103     | 1246  | 48    | 2.00   |
| Seagate   | Pipeline HD 5900.2     | 9      | 210     | 970   | 114   | 1.99   |
| Hitachi   | Deskstar 5K1000        | 3      | 43      | 974   | 91    | 1.99   |
| HGST      | Unknown                | 6      | 12      | 772   | 4     | 1.98   |
| WDC       | Red                    | 37     | 1459    | 875   | 10    | 1.98   |
| HGST      | Ultrastar He8          | 4      | 48      | 1005  | 3     | 1.97   |
| IBM/Hi... | Deskstar GXP-180       | 4      | 9       | 1314  | 16    | 1.97   |
| Seagate   | Barracuda 7200.8       | 10     | 67      | 1299  | 104   | 1.95   |
| Seagate   | BarraCuda 3.5 (CMR)    | 3      | 8       | 840   | 8     | 1.94   |
| Samsung   | SpinPoint F3           | 6      | 435     | 951   | 38    | 1.93   |
| Seagate   | U9                     | 3      | 7       | 690   | 0     | 1.89   |
| Maxtor    | MaXLine Pro 500        | 1      | 6       | 743   | 1     | 1.87   |
| Toshiba   | 3.5" HDD DT01ABA..V    | 4      | 21      | 875   | 98    | 1.87   |
| Seagate   | Barracuda ES           | 8      | 67      | 1325  | 398   | 1.86   |
| WDC       | Raptor                 | 17     | 32      | 1340  | 13    | 1.85   |
| Maxtor    | DiamondMax VL15        | 1      | 1       | 1326  | 1     | 1.82   |
| Seagate   | Barracuda Pro          | 1      | 3       | 662   | 0     | 1.82   |
| Maxtor    | MaXLine III (SATA/300) | 2      | 5       | 1072  | 190   | 1.81   |
| Seagate   | Constellation ES (S... | 3      | 54      | 1415  | 32    | 1.81   |
| Seagate   | Barracuda Green (AF)   | 4      | 305     | 1019  | 231   | 1.81   |
| WDC       | Caviar SE              | 171    | 693     | 978   | 31    | 1.80   |
| Hitachi   | Ultrastar 7K4000       | 5      | 69      | 730   | 54    | 1.79   |
| WDC       | Ultrastar He10/12      | 4      | 128     | 647   | 0     | 1.77   |
| Hitachi   | Deskstar 5K4000        | 1      | 6       | 646   | 0     | 1.77   |
| Hitachi   | Deskstar 7K1000.C      | 16     | 816     | 924   | 81    | 1.75   |
| Seagate   | Surveillance           | 13     | 81      | 792   | 71    | 1.75   |
| Hitachi   | Deskstar 7K1000.B      | 11     | 180     | 1131  | 63    | 1.74   |
| WDC       | WDC Enterprise         | 3      | 3       | 625   | 0     | 1.71   |
| Samsung   | SpinPoint T133         | 5      | 32      | 976   | 135   | 1.70   |
| Seagate   | Constellation ES (S... | 4      | 49      | 1146  | 141   | 1.70   |
| Hitachi   | Deskstar 7K80          | 6      | 103     | 876   | 26    | 1.70   |
| WDC       | AV-GP                  | 62     | 277     | 874   | 38    | 1.69   |
| Toshiba   | 2.5" HDD MQ03ABB       | 2      | 4       | 616   | 0     | 1.69   |
| WDC       | Black                  | 29     | 563     | 716   | 20    | 1.68   |
| Seagate   | DB35.3                 | 7      | 24      | 804   | 274   | 1.68   |
| Maxtor    | DiamondMax Plus D740X  | 3      | 6       | 1114  | 4     | 1.68   |
| WDC       | Green                  | 7      | 187     | 689   | 8     | 1.68   |
| Samsung   | SpinPoint F3 EG        | 4      | 64      | 817   | 66    | 1.67   |
| Seagate   | DB35.2                 | 2      | 5       | 1201  | 476   | 1.65   |
| Samsung   | SpinPoint              | 7      | 16      | 796   | 39    | 1.64   |
| Apple     | Western Digital Blue   | 1      | 1       | 594   | 0     | 1.63   |
| Seagate   | Barracuda 7200.10      | 36     | 1768    | 973   | 267   | 1.61   |
| Hitachi   | Deskstar P7K500        | 11     | 259     | 1136  | 86    | 1.61   |
| Samsung   | SpinPoint F2 EG        | 3      | 254     | 1057  | 276   | 1.61   |
| WDC       | Black SSHD             | 1      | 11      | 583   | 0     | 1.60   |
| Toshiba   | 2.5" HDD MQ01ABF..H    | 1      | 3       | 730   | 42    | 1.60   |
| Quantum   | Fireball               | 2      | 2       | 579   | 0     | 1.59   |
| Hitachi   | CinemaStar 7K500       | 1      | 1       | 573   | 0     | 1.57   |
| Fujitsu   | MPA..MPG               | 5      | 6       | 711   | 42    | 1.53   |
| Seagate   | Desktop SSHD           | 9      | 206     | 752   | 63    | 1.50   |
| Apple     | Barracuda              | 1      | 32      | 545   | 0     | 1.50   |
| Maxtor    | DiamondMax 10 (SATA... | 6      | 53      | 764   | 22    | 1.48   |
| Apple     | Travelstar 5K1000      | 4      | 84      | 733   | 68    | 1.48   |
| HGST      | Ultrastar He10         | 4      | 43      | 590   | 1     | 1.48   |
| HP        | Unknown                | 5      | 6       | 755   | 2     | 1.47   |
| Hitachi   | Deskstar T7K250        | 5      | 53      | 1042  | 97    | 1.46   |
| Samsung   | SpinPoint F1 DT        | 12     | 572     | 1077  | 193   | 1.45   |
| Seagate   | Barracuda 7200.14 (AF) | 27     | 4281    | 733   | 126   | 1.45   |
| Seagate   | SpinPoint D8X          | 1      | 4       | 619   | 202   | 1.44   |
| Apple     | SpinPoint              | 1      | 3       | 523   | 0     | 1.43   |
| Apple     | Seagate Samsung Spi... | 1      | 5       | 515   | 0     | 1.41   |
| WDC       | Caviar Blue            | 361    | 6406    | 735   | 40    | 1.40   |
| Seagate   | BarraCuda Pro          | 3      | 10      | 507   | 0     | 1.39   |
| Seagate   | Video 3.5 HDD          | 10     | 98      | 690   | 157   | 1.39   |
| Seagate   | Barracuda 7200.7 an... | 19     | 725     | 900   | 88    | 1.38   |
| WDC       | Gold                   | 20     | 136     | 514   | 1     | 1.38   |
| Toshiba   | 3.5" HDD DT01ACA       | 4      | 1796    | 580   | 43    | 1.37   |
| Seagate   | SpinPoint M9T          | 3      | 123     | 558   | 4     | 1.37   |
| Apple     | HGST Travelstar Z5K500 | 1      | 55      | 542   | 26    | 1.37   |
| Seagate   | Laptop HDD             | 6      | 24      | 571   | 135   | 1.35   |
| WDC       | RE2-GP                 | 3      | 4       | 1028  | 2     | 1.34   |
| Toshiba   | 2.5" HDD MQ01UBB       | 1      | 14      | 826   | 243   | 1.33   |
| Toshiba   | Toshiba Surveillance   | 2      | 3       | 780   | 2     | 1.33   |
| Seagate   | Barracuda 5400.1       | 1      | 5       | 835   | 33    | 1.32   |
| Toshiba   | 2.5" HDD MK..32GSX     | 2      | 11      | 492   | 1     | 1.32   |
| Seagate   | IronWolf               | 21     | 455     | 538   | 12    | 1.31   |
| Hitachi   | CinemaStar Z5K320      | 3      | 8       | 730   | 24    | 1.30   |
| Seagate   | UX                     | 1      | 9       | 852   | 10    | 1.28   |
| Toshiba   | Unknown                | 21     | 33      | 484   | 36    | 1.28   |
| Samsung   | SpinPoint VL40         | 1      | 1       | 2328  | 4     | 1.28   |
| Seagate   | Barracuda 7200.9       | 38     | 643     | 849   | 378   | 1.27   |
| WDC       | Caviar                 | 84     | 221     | 813   | 43    | 1.27   |
| Seagate   | Momentus 5400.7        | 2      | 15      | 683   | 415   | 1.26   |
| Seagate   | Barracuda 7200.12      | 16     | 2239    | 831   | 176   | 1.25   |
| Seagate   | Video 3.5              | 1      | 6       | 453   | 0     | 1.24   |
| Hitachi   | Deskstar 7K160         | 7      | 209     | 949   | 129   | 1.22   |
| Toshiba   | 2.5" HDD MQ03UBB       | 2      | 34      | 496   | 71    | 1.21   |
| Seagate   | Barracuda SpinPoint F3 | 2      | 76      | 592   | 7     | 1.21   |
| Seagate   | Barracuda ATA V        | 4      | 5       | 1408  | 28    | 1.20   |
| WDC       | AV                     | 36     | 126     | 633   | 31    | 1.19   |
| MaxDig... | Unknown                | 6      | 8       | 538   | 11    | 1.19   |
| Hitachi   | CinemaStar C5K750      | 1      | 2       | 729   | 12    | 1.19   |
| WDC       | Caviar Blue EIDE       | 18     | 131     | 731   | 50    | 1.19   |
| Seagate   | SpinPoint M7E          | 3      | 25      | 440   | 1     | 1.19   |
| Toshiba   | MG04ACA Enterprise HDD | 2      | 3       | 428   | 0     | 1.17   |
| Toshiba   | Toshiba Enterprise     | 2      | 13      | 427   | 0     | 1.17   |
| WDC       | Scorpio Blue EIDE      | 8      | 13      | 426   | 0     | 1.17   |
| Seagate   | Momentus XT (AF)       | 1      | 25      | 632   | 158   | 1.13   |
| Seagate   | Exos X14               | 5      | 29      | 435   | 3     | 1.12   |
| HPE       | Seagate Constellati... | 1      | 4       | 578   | 1     | 1.11   |
| Seagate   | Desktop HDD            | 2      | 4       | 404   | 0     | 1.11   |
| Seagate   | SV35                   | 8      | 75      | 498   | 113   | 1.11   |
| Seagate   | Barracuda ES.2         | 6      | 58      | 1075  | 305   | 1.11   |
| WDC       | HGST Ultrastar He10    | 2      | 68      | 400   | 2     | 1.10   |
| Toshiba   | 2.5" HDD MQ01UBD       | 3      | 92      | 573   | 176   | 1.09   |
| HPE       | Seagate Enterprise     | 1      | 1       | 395   | 0     | 1.08   |
| WDC       | Elements / My Passport | 85     | 774     | 488   | 24    | 1.08   |
| Toshiba   | 2.5" HDD MQ04ABB       | 1      | 5       | 393   | 0     | 1.08   |
| Maxtor    | DiamondMax 21          | 17     | 307     | 785   | 378   | 1.07   |
| Toshiba   | X300                   | 7      | 153     | 430   | 21    | 1.07   |
| Samsung   | SpinPoint T166         | 8      | 285     | 1021  | 422   | 1.07   |
| HGST      | Ultrastar 7K2          | 3      | 36      | 390   | 0     | 1.07   |
| HGST      | Travelstar 7K1000      | 4      | 684     | 489   | 160   | 1.07   |
| Apple     | Barracuda 7200.12      | 1      | 8       | 546   | 302   | 1.05   |
| Seagate   | Constellation ES       | 9      | 14      | 1342  | 593   | 1.03   |
| MediaMax  | WL1000                 | 5      | 7       | 608   | 3     | 1.01   |
| Hitachi   | Travelstar 7K750       | 2      | 75      | 799   | 355   | 1.00   |
| Samsung   | SpinPoint F4           | 2      | 62      | 684   | 139   | 1.00   |
| Seagate   | SpinPoint F4           | 2      | 9       | 705   | 69    | 1.00   |
| HP        | 500GB SATA disk MM0... | 1      | 15      | 1721  | 83    | 1.00   |
| Fujitsu   | MHW BH                 | 11     | 89      | 509   | 68    | 1.00   |
| Seagate   | Maxtor DiamondMax 23   | 5      | 87      | 762   | 242   | 1.00   |
| Seagate   | Video 2.5              | 5      | 41      | 403   | 10    | 0.99   |
| Seagate   | Barracuda Compute      | 1      | 189     | 429   | 34    | 0.99   |
| Seagate   | Barracuda 3.5          | 9      | 1760    | 397   | 37    | 0.98   |
| Seagate   | BarraCuda 3.5          | 7      | 124     | 374   | 17    | 0.98   |
| ExcelStor | Jupiter                | 9      | 24      | 807   | 61    | 0.97   |
| HGST      | Ultrastar He6          | 1      | 1       | 353   | 0     | 0.97   |
| Seagate   | Momentus               | 7      | 21      | 582   | 74    | 0.97   |
| Seagate   | BarraCuda              | 1      | 1       | 346   | 0     | 0.95   |
| Toshiba   | 2.5" HDD MQ02ABD..H    | 1      | 37      | 450   | 60    | 0.95   |
| Seagate   | Skyhawk                | 10     | 81      | 379   | 19    | 0.95   |
| Samsung   | SpinPoint S166         | 3      | 107     | 848   | 433   | 0.94   |
| Seagate   | FireCuda 3.5           | 2      | 110     | 427   | 24    | 0.94   |
| WDC       | Blue                   | 64     | 1319    | 375   | 17    | 0.94   |
| Seagate   | Barracuda LP           | 4      | 116     | 875   | 363   | 0.94   |
| Toshiba   | N300/MN NAS HDD        | 4      | 54      | 378   | 1     | 0.93   |
| WDC       | Purple                 | 35     | 280     | 440   | 12    | 0.93   |
| WDC       | Scorpio Black          | 59     | 393     | 547   | 92    | 0.92   |
| Toshiba   | 2.5" HDD MK..75GSX     | 1      | 2       | 399   | 538   | 0.91   |
| Samsung   | SpinPoint F1           | 1      | 1       | 1320  | 3     | 0.90   |
| WDC       | Scorpio                | 3      | 3       | 722   | 1     | 0.90   |
| Seagate   | Barracuda              | 2      | 8       | 325   | 0     | 0.89   |
| Toshiba   | 2.5" HDD MK..59GSXP... | 1      | 5       | 439   | 15    | 0.87   |
| Samsung   | SpinPoint P80 SD       | 7      | 283     | 815   | 377   | 0.87   |
| WDC       | Blue SSHD              | 2      | 3       | 312   | 0     | 0.86   |
| MediaMax  | WL5000                 | 1      | 1       | 308   | 0     | 0.85   |
| Toshiba   | 2.5" HDD MQ02ABF       | 1      | 14      | 316   | 1     | 0.85   |
| Seagate   | Exos 7E8               | 13     | 69      | 323   | 30    | 0.83   |
| Hitachi   | Travelstar 5K500.B     | 16     | 678     | 538   | 164   | 0.83   |
| Toshiba   | MG05ACA Enterprise ... | 1      | 2       | 300   | 0     | 0.82   |
| WDC       | Scorpio Blue           | 254    | 3107    | 463   | 70    | 0.82   |
| Seagate   | Momentus 7200.5        | 4      | 175     | 597   | 135   | 0.82   |
| Seagate   | SpinPoint M8 (AF)      | 6      | 1711    | 433   | 42    | 0.82   |
| WDC       | Red Pro                | 15     | 63      | 324   | 1     | 0.82   |
| Samsung   | SpinPoint M7U (USB)    | 3      | 7       | 295   | 1     | 0.81   |
| Toshiba   | MG06ACA Enterprise ... | 4      | 21      | 294   | 0     | 0.81   |
| Toshiba   | S300                   | 2      | 4       | 292   | 0     | 0.80   |
| Fujitsu   | MHT                    | 10     | 20      | 604   | 123   | 0.79   |
| Seagate   | Laptop Thin SSHD       | 1      | 3       | 284   | 0     | 0.78   |
| Toshiba   | 2.5" HDD MQ01ACF       | 3      | 128     | 370   | 46    | 0.78   |
| Samsung   | SpinPoint M7           | 3      | 205     | 415   | 47    | 0.77   |
| Fujitsu   | MHZ BJ                 | 6      | 10      | 439   | 218   | 0.77   |
| Samsung   | SpinPoint M7E (AF)     | 5      | 205     | 471   | 74    | 0.77   |
| Seagate   | Momentus 7200.2        | 9      | 41      | 508   | 189   | 0.76   |
| Toshiba   | P300                   | 7      | 946     | 295   | 7     | 0.76   |
| WDC       | Black Mobile           | 34     | 414     | 314   | 21    | 0.76   |
| Hitachi   | Travelstar 7K320       | 14     | 54      | 632   | 465   | 0.75   |
| Apple     | Momentus               | 1      | 8       | 860   | 5     | 0.75   |
| Hitachi   | Travelstar 5K750       | 3      | 491     | 550   | 404   | 0.74   |
| Magnet... | Unknown                | 9      | 11      | 315   | 4     | 0.73   |
| Seagate   | Exos X16               | 6      | 98      | 266   | 1     | 0.73   |
| Seagate   | Ultra Mobile SSHD      | 2      | 8       | 437   | 61    | 0.73   |
| Toshiba   | 2.5" HDD MQ01ABD       | 8      | 1378    | 396   | 141   | 0.72   |
| Seagate   | Barracuda V            | 1      | 1       | 259   | 0     | 0.71   |
| Fujitsu   | MHY BH                 | 6      | 130     | 451   | 150   | 0.71   |
| Toshiba   | 2.5" HDD               | 18     | 93      | 492   | 56    | 0.70   |
| Samsung   | SpinPoint P80          | 18     | 156     | 653   | 150   | 0.70   |
| Fujitsu   | MJA BH                 | 9      | 65      | 485   | 155   | 0.69   |
| Toshiba   | N300 NAS HDD           | 4      | 22      | 316   | 8     | 0.69   |
| Toshiba   | 2.5" HDD H200          | 2      | 6       | 251   | 0     | 0.69   |
| Toshiba   | 2.5" HDD MK..75GSX     | 4      | 170     | 538   | 368   | 0.68   |
| Hitachi   | Travelstar 7K200       | 10     | 38      | 557   | 148   | 0.68   |
| Seagate   | U6                     | 3      | 23      | 620   | 32    | 0.68   |
| Toshiba   | 2.5" HDD MQ01ABD       | 5      | 28      | 294   | 9     | 0.68   |
| Toshiba   | 2.5" HDD MQ04UBB       | 1      | 43      | 258   | 7     | 0.68   |
| WDC       | Blue Mobile            | 151    | 3432    | 295   | 22    | 0.68   |
| Seagate   | IronWolf Pro           | 15     | 88      | 308   | 3     | 0.66   |
| Toshiba   | 2.5" HDD MQ01ABD..H    | 2      | 2       | 346   | 4     | 0.66   |
| Hitachi   | Deskstar 7K1000.D      | 2      | 125     | 675   | 580   | 0.66   |
| Samsung   | SpinPoint S250         | 2      | 78      | 876   | 645   | 0.66   |
| Seagate   | Laptop SSHD            | 10     | 414     | 410   | 132   | 0.66   |
| Toshiba   | 2.5" HDD MK..61GSY     | 2      | 2       | 1162  | 8     | 0.65   |
| HGST      | Travelstar Z7K500      | 8      | 358     | 491   | 288   | 0.65   |
| HGST      | Travelstar 5K1000      | 5      | 469     | 463   | 450   | 0.65   |
| HGST      | Travelstar Z5K1000     | 3      | 150     | 291   | 90    | 0.65   |
| HGST      | Ultrastar DC HC310     | 2      | 21      | 236   | 0     | 0.65   |
| Fujitsu   | MHV                    | 29     | 134     | 369   | 29    | 0.65   |
| Seagate   | Unknown                | 36     | 57      | 318   | 51    | 0.65   |
| Seagate   | Barracuda 2.5 5400     | 9      | 620     | 275   | 60    | 0.64   |
| Toshiba   | 2.5" HDD MK..59GSX     | 1      | 11      | 415   | 218   | 0.64   |
| Quantum   | Fireball lct20         | 3      | 3       | 640   | 2     | 0.63   |
| HGST      | CinemaStar Z5K500      | 3      | 12      | 448   | 30    | 0.63   |
| Seagate   | Barracuda ATA IV       | 4      | 63      | 700   | 29    | 0.62   |
| Seagate   | FireCuda 2.5           | 7      | 245     | 289   | 77    | 0.62   |
| Seagate   | Momentus 7200.3        | 8      | 34      | 541   | 52    | 0.61   |
| Toshiba   | 2.5" HDD MQ01ABF       | 2      | 66      | 309   | 75    | 0.61   |
| Toshiba   | 2.5" HDD MQ04UBD       | 1      | 68      | 224   | 2     | 0.61   |
| Seagate   | Exos 5E8               | 1      | 5       | 272   | 2     | 0.61   |
| Seagate   | Constellation (SATA)   | 1      | 3       | 1402  | 99    | 0.60   |
| Hitachi   | CinemaStar 7K1000.B    | 2      | 4       | 218   | 0     | 0.60   |
| WDC       | Protege                | 8      | 15      | 669   | 30    | 0.60   |
| Seagate   | Momentus 7200.4        | 9      | 380     | 565   | 415   | 0.59   |
| Samsung   | SpinPoint M8 (AF)      | 5      | 105     | 397   | 73    | 0.59   |
| WDC       | Shrek LT 2.5           | 6      | 14      | 381   | 3     | 0.59   |
| Seagate   | Pipeline HD Mini       | 4      | 23      | 609   | 176   | 0.59   |
| Seagate   | Momentus 5400.2        | 17     | 78      | 417   | 439   | 0.58   |
| Fujitsu   | MHW BJ                 | 3      | 5       | 317   | 27    | 0.58   |
| Apple     | HGST Travelstar 5K750  | 2      | 14      | 387   | 26    | 0.58   |
| Toshiba   | 2.5" HDD MQ01ABF       | 1      | 668     | 285   | 97    | 0.58   |
| HGST      | Edurastar              | 1      | 1       | 211   | 0     | 0.58   |
| Toshiba   | 3.5" HDD DT01ACA       | 3      | 15      | 210   | 0     | 0.58   |
| Toshiba   | 2.5" HDD MK..59GSM     | 1      | 24      | 512   | 445   | 0.58   |
| HGST      | Ultrastar DC HC520 ... | 3      | 31      | 211   | 1     | 0.58   |
| Maxtor    | DiamondMax 17          | 2      | 13      | 408   | 180   | 0.57   |
| Hitachi   | Travelstar 4K120       | 5      | 17      | 670   | 25    | 0.56   |
| Seagate   | Momentus XT            | 2      | 27      | 689   | 126   | 0.56   |
| Hitachi   | Travelstar 5K1000      | 3      | 38      | 512   | 601   | 0.56   |
| Fujitsu   | MHZ BH                 | 13     | 354     | 314   | 116   | 0.55   |
| Seagate   | Momentus 5400.7 (AF)   | 2      | 23      | 522   | 295   | 0.55   |
| Toshiba   | MG08ACA Enterprise ... | 2      | 25      | 201   | 0     | 0.55   |
| WDC       | Black P10              | 3      | 10      | 195   | 0     | 0.53   |
| Seagate   | Momentus 5400 PSD      | 2      | 3       | 352   | 338   | 0.53   |
| Toshiba   | 2.5" HDD MK..34GSX     | 2      | 20      | 453   | 110   | 0.53   |
| Seagate   | Barracuda ATA III      | 1      | 1       | 194   | 0     | 0.53   |
| Hitachi   | Travelstar Z5K320      | 3      | 325     | 367   | 305   | 0.53   |
| Toshiba   | 2.5" HDD MQ01ABC       | 1      | 4       | 263   | 272   | 0.53   |
| Toshiba   | 2.5" HDD MK..76GSX     | 6      | 21      | 291   | 210   | 0.53   |
| Seagate   | BarraCuda 3.5 (SMR)    | 6      | 708     | 215   | 39    | 0.53   |
| Toshiba   | L200                   | 6      | 113     | 224   | 24    | 0.53   |
| Toshiba   | 2.5" HDD MQ04UBF       | 1      | 86      | 217   | 2     | 0.53   |
| Samsung   | SpinPoint MT2          | 1      | 5       | 191   | 0     | 0.53   |
| Seagate   | Mobile HDD             | 4      | 1213    | 245   | 131   | 0.52   |
| Maxtor    | DiamondMax 20          | 7      | 33      | 631   | 602   | 0.52   |
| Seagate   | Momentus 5400.4        | 4      | 120     | 520   | 408   | 0.52   |
| Seagate   | LD25.2                 | 2      | 5       | 249   | 1     | 0.52   |
| Hitachi   | Travelstar 7K100       | 6      | 26      | 573   | 68    | 0.52   |
| Toshiba   | 2.5" HDD MK..55GSX     | 3      | 13      | 421   | 215   | 0.51   |
| Seagate   | SpinPoint M9TU (USB)   | 1      | 17      | 184   | 0     | 0.51   |
| IBM/Hi... | Deskstar 120GXP        | 4      | 8       | 655   | 117   | 0.50   |
| Fujitsu   | MHZ BT                 | 1      | 2       | 1426  | 6     | 0.50   |
| Hitachi   | CinemaStar 5K1000.B    | 2      | 3       | 474   | 246   | 0.49   |
| Toshiba   | 2.5" HDD MK..37GSX     | 2      | 26      | 432   | 116   | 0.49   |
| Samsung   | SpinPoint P120         | 6      | 130     | 971   | 626   | 0.49   |
| Hitachi   | Travelstar 5K250       | 10     | 298     | 552   | 166   | 0.49   |
| Seagate   | Momentus 7200 FDE.2    | 2      | 3       | 374   | 565   | 0.49   |
| Apple     | MK..65GSXF             | 1      | 6       | 256   | 69    | 0.48   |
| WDC       | White Label            | 13     | 130     | 179   | 1     | 0.47   |
| ASMedia   | Unknown                | 1      | 1       | 172   | 0     | 0.47   |
| WDC       | Blue UltraSlim         | 4      | 5       | 170   | 0     | 0.47   |
| Seagate   | Momentus 5400.3        | 10     | 222     | 432   | 431   | 0.47   |
| Hitachi   | Travelstar Z7K500      | 3      | 31      | 495   | 616   | 0.47   |
| Hitachi   | Travelstar Z7K320      | 4      | 94      | 535   | 558   | 0.46   |
| Hitachi   | Travelstar Z5K500      | 3      | 231     | 394   | 284   | 0.46   |
| Hitachi   | Travelstar 5K320       | 12     | 255     | 521   | 218   | 0.45   |
| MediaMax  | WL3000                 | 2      | 2       | 165   | 0     | 0.45   |
| Toshiba   | 2.5" HDD MK..59GSM     | 2      | 43      | 623   | 812   | 0.45   |
| Toshiba   | 2.5" HDD MK..59GSXP    | 7      | 182     | 461   | 381   | 0.45   |
| Fujitsu   | MHX BT                 | 2      | 10      | 531   | 80    | 0.45   |
| Toshiba   | 1.8" HDD MK..29GSG     | 3      | 9       | 327   | 393   | 0.44   |
| Hitachi   | Travelstar 5K160       | 12     | 239     | 546   | 72    | 0.44   |
| Fujitsu   | MHZ BS                 | 1      | 1       | 159   | 0     | 0.44   |
| HGST      | Ultrastar DC HC320     | 1      | 9       | 158   | 0     | 0.43   |
| WDC       | Black UltraSlim        | 1      | 2       | 596   | 10    | 0.43   |
| Maxtor    | DiamondMax D540X-4K    | 3      | 4       | 487   | 13    | 0.43   |
| Samsung   | SpinPoint V80          | 3      | 4       | 597   | 63    | 0.42   |
| Seagate   | Momentus 7200.1        | 2      | 9       | 541   | 366   | 0.42   |
| Samsung   | SpinPoint V60          | 1      | 6       | 1055  | 104   | 0.42   |
| Toshiba   | 1.8" HDD MK..33GSG     | 2      | 10      | 417   | 210   | 0.42   |
| Seagate   | Barracuda Pro Compute  | 2      | 277     | 180   | 57    | 0.42   |
| MARSHAL   | Unknown                | 6      | 10      | 288   | 287   | 0.42   |
| Hitachi   | Travelstar 7K500       | 12     | 160     | 534   | 683   | 0.42   |
| Toshiba   | 2.5" HDD MK..58GSX     | 1      | 8       | 930   | 10    | 0.41   |
| HGST      | Ultrastar HC310/320    | 3      | 44      | 152   | 36    | 0.41   |
| Toshiba   | MG07ACA Enterprise ... | 3      | 30      | 150   | 0     | 0.41   |
| Toshiba   | MG08                   | 2      | 5       | 150   | 0     | 0.41   |
| Seagate   | Laptop Ultrathin       | 1      | 9       | 200   | 4     | 0.41   |
| Toshiba   | 2.5" HDD MK..46GSX     | 4      | 60      | 536   | 137   | 0.41   |
| HGST      | Travelstar Z5K500      | 8      | 817     | 348   | 393   | 0.41   |
| Toshiba   | 2.5" HDD MQ04ABF       | 2      | 531     | 168   | 54    | 0.41   |
| MediaMax  | WL320                  | 1      | 1       | 146   | 0     | 0.40   |
| WDC       | Internal Use HDD       | 15     | 89      | 152   | 13    | 0.40   |
| Hitachi   | Travelstar 5K500       | 1      | 6       | 520   | 5     | 0.40   |
| Seagate   | Momentus Thin          | 9      | 287     | 434   | 555   | 0.40   |
| Toshiba   | 2.5" HDD MK..63GSX     | 2      | 26      | 624   | 69    | 0.39   |
| Toshiba   | 1.8" HDD               | 5      | 15      | 373   | 11    | 0.39   |
| HP        | Ultrastar 7K4000       | 1      | 2       | 1504  | 505   | 0.39   |
| Seagate   | FreePlay               | 5      | 26      | 344   | 664   | 0.39   |
| Toshiba   | 2.5" HDD MK..65GSX     | 13     | 329     | 494   | 279   | 0.39   |
| Seagate   | Momentus 5400.6        | 12     | 1379    | 488   | 459   | 0.39   |
| HP        | Barracuda ES.2         | 1      | 1       | 138   | 0     | 0.38   |
| Samsung   | HM100UX (S2 Portable)  | 1      | 2       | 214   | 4     | 0.37   |
| WDC       | Unknown                | 37     | 67      | 226   | 37    | 0.37   |
| Fujitsu   | MHW AT                 | 2      | 3       | 494   | 5     | 0.37   |
| HGST      | Deskstar 5K4000        | 1      | 2       | 133   | 0     | 0.37   |
| Seagate   | SV35.5                 | 3      | 10      | 880   | 339   | 0.36   |
| Seagate   | Laptop Thin HDD        | 7      | 1367    | 346   | 429   | 0.36   |
| Toshiba   | 2.5" HDD MK..55GSX     | 10     | 177     | 358   | 68    | 0.36   |
| Toshiba   | V300                   | 1      | 1       | 129   | 0     | 0.36   |
| HPE       | Proliant HardDrive     | 1      | 2       | 127   | 0     | 0.35   |
| Toshiba   | 2.5" HDD MQ04ABD       | 1      | 12      | 126   | 0     | 0.35   |
| Samsung   | SpinPoint MP5          | 3      | 19      | 378   | 308   | 0.34   |
| Toshiba   | 2.5" HDD MK..52GSX     | 5      | 124     | 543   | 154   | 0.34   |
| Toshiba   | 1.8" HDD MK..16GSG     | 1      | 3       | 272   | 4     | 0.34   |
| Maxtor    | Unknown                | 3      | 4       | 857   | 26    | 0.34   |
| WDC       | Red Plus               | 8      | 108     | 122   | 1     | 0.33   |
| Samsung   | SpinPoint V120CE       | 1      | 1       | 120   | 0     | 0.33   |
| Lenovo    | Seagate Enterprise     | 1      | 2       | 120   | 0     | 0.33   |
| MediaMax  | WL6000                 | 1      | 2       | 438   | 686   | 0.33   |
| Toshiba   | 1.8" HDD               | 5      | 16      | 592   | 146   | 0.33   |
| HP        | Seagate Constellati... | 1      | 2       | 133   | 40    | 0.33   |
| Hitachi   | Travelstar 5K100       | 9      | 73      | 426   | 60    | 0.33   |
| Toshiba   | DT02 Series            | 1      | 3       | 118   | 0     | 0.33   |
| Samsung   | SpinPoint F1 EG        | 1      | 8       | 774   | 443   | 0.32   |
| IBM/Hi... | Travelstar 60GH and... | 3      | 5       | 217   | 3     | 0.32   |
| Hitachi   | Travelstar 5K120       | 2      | 4       | 384   | 5     | 0.32   |
| WDC       | IU HA500               | 1      | 7       | 117   | 0     | 0.32   |
| Seagate   | SpinPoint M8U (USB)    | 2      | 74      | 140   | 16    | 0.32   |
| Seagate   | SV35.2                 | 3      | 8       | 609   | 881   | 0.31   |
| WDC       | Ultrastar DC HC530     | 2      | 17      | 113   | 1     | 0.31   |
| Toshiba   | 2.5" HDD MQ02ABF..H    | 2      | 10      | 197   | 205   | 0.29   |
| IBM       | Travelstar 25GS, 18... | 2      | 2       | 156   | 3     | 0.29   |
| Quantum   | Fireball lct15         | 2      | 2       | 248   | 3     | 0.29   |
| Seagate   | SkyHawk                | 5      | 17      | 105   | 0     | 0.29   |
| Toshiba   | 2.5" HDD MK..51GSY     | 1      | 1       | 939   | 8     | 0.29   |
| MediaMax  | WL2000                 | 2      | 3       | 541   | 4     | 0.28   |
| Toshiba   | 2.5" HDD MK..53GSX     | 2      | 46      | 116   | 3     | 0.27   |
| IBM       | Deskstar 40GV & 75G... | 3      | 4       | 1041  | 24    | 0.27   |
| Seagate   | MobileMax-2            | 1      | 2       | 169   | 3     | 0.26   |
| Seagate   | DB35.4                 | 1      | 4       | 948   | 186   | 0.25   |
| Toshiba   | 2.5" HDD MK..37GSX     | 2      | 66      | 508   | 110   | 0.25   |
| Toshiba   | 2.5" HDD MK..65GSX     | 5      | 9       | 332   | 47    | 0.25   |
| Seagate   | Exos X18               | 2      | 70      | 89    | 0     | 0.25   |
| WDC       | IU CB500               | 3      | 30      | 92    | 68    | 0.24   |
| Toshiba   | MG09ACA Enterprise ... | 1      | 4       | 88    | 0     | 0.24   |
| Seagate   | Momentus 5400.5        | 5      | 126     | 450   | 193   | 0.24   |
| Toshiba   | 2.5" HDD MK..56GSY     | 6      | 36      | 162   | 222   | 0.24   |
| Hitachi   | Travelstar 7K60        | 1      | 2       | 289   | 34    | 0.24   |
| WDC       | Ultrastar DC HC550     | 3      | 23      | 87    | 0     | 0.24   |
| China     | Unknown                | 4      | 4       | 168   | 596   | 0.24   |
| HGST      | Travelstar Z5K500.B    | 1      | 26      | 90    | 1     | 0.23   |
| Seagate   | Barracuda 7200.11      | 13     | 513     | 866   | 320   | 0.23   |
| Toshiba   | 2.5" HDD MK..61GSY[N]  | 8      | 99      | 108   | 189   | 0.23   |
| Toshiba   | 2.5" HDD MQ01UBF       | 1      | 1       | 82    | 0     | 0.23   |
| Toshiba   | 2.5" HDD MK..46GSX     | 1      | 14      | 359   | 46    | 0.22   |
| Seagate   | Ultra Mobile HDD       | 2      | 4       | 100   | 261   | 0.22   |
| Maxtor    | Fireball 3             | 6      | 15      | 102   | 31    | 0.22   |
| Samsung   | SpinPoint M            | 2      | 14      | 244   | 13    | 0.21   |
| Lenovo    | RE                     | 1      | 4       | 76    | 0     | 0.21   |
| Seagate   | SV35.3                 | 2      | 3       | 1165  | 13    | 0.21   |
| MediaMax  | WL4000                 | 1      | 1       | 71    | 0     | 0.20   |
| Seagate   | Momentus 4200.2        | 5      | 8       | 409   | 266   | 0.19   |
| Seagate   | LD25 Series            | 2      | 5       | 123   | 417   | 0.19   |
| WDC       | Scorpio EIDE           | 11     | 14      | 319   | 65    | 0.19   |
| Seagate   | MobileMax 80215        | 1      | 2       | 195   | 1     | 0.19   |
| AMP       | Unknown                | 1      | 1       | 68    | 0     | 0.19   |
| MediaMax  | WL250                  | 4      | 5       | 450   | 4     | 0.18   |
| Samsung   | SpinPoint M8U (USB)    | 2      | 3       | 61    | 0     | 0.17   |
| MediaMax  | WL1500                 | 3      | 5       | 529   | 80    | 0.17   |
| MediaMax  | WL160                  | 1      | 1       | 540   | 8     | 0.16   |
| MediaMax  | WL750                  | 1      | 1       | 59    | 0     | 0.16   |
| Toshiba   | 2.5" HDD MK..76GSX     | 5      | 138     | 106   | 236   | 0.16   |
| Samsung   | SpinPoint M40/60/80    | 9      | 27      | 471   | 406   | 0.16   |
| IBM/Hi... | Hitachi Travelstar ... | 5      | 22      | 372   | 36    | 0.16   |
| Seagate   | Terascale              | 2      | 6       | 56    | 0     | 0.15   |
| HPE       | Unknown                | 2      | 2       | 56    | 0     | 0.15   |
| Seagate   | SpinPoint F3           | 1      | 2       | 458   | 4     | 0.15   |
| IBM/Hi... | Deskstar 60GXP         | 2      | 5       | 638   | 72    | 0.15   |
| Maxtor    | MaXLine III            | 1      | 1       | 2421  | 46    | 0.14   |
| Seagate   | Mobile USB Momentus    | 1      | 3       | 51    | 0     | 0.14   |
| Hitachi   | Travelstar 5K80        | 3      | 6       | 224   | 118   | 0.13   |
| Hitachi   | Travelstar 4K40        | 1      | 7       | 441   | 161   | 0.13   |
| Samsung   | SpinPoint N2           | 2      | 3       | 45    | 696   | 0.12   |
| HGST      | Travelstar Z7K500.B    | 1      | 3       | 42    | 0     | 0.12   |
| Seagate   | Pipeline HD Pro        | 1      | 2       | 828   | 40    | 0.11   |
| Samsung   | SpinPoint M5           | 6      | 143     | 356   | 437   | 0.11   |
| Synology  | Synology Enterprise    | 1      | 7       | 39    | 0     | 0.11   |
| Seagate   | Constellation          | 3      | 3       | 2366  | 62    | 0.11   |
| Fujitsu   | MHJ                    | 1      | 1       | 1462  | 41    | 0.10   |
| Seagate   | Pipeline HD 5900.1     | 3      | 16      | 519   | 100   | 0.09   |
| Maxtor    | DiamondMax 22          | 4      | 55      | 765   | 347   | 0.09   |
| Samsung   | SpinPoint V40+         | 2      | 3       | 1003  | 159   | 0.08   |
| Seagate   | U8                     | 1      | 1       | 754   | 24    | 0.08   |
| MediaMax  | WL120                  | 1      | 1       | 139   | 4     | 0.08   |
| HPE       | Seagate Constellati... | 1      | 1       | 1005  | 35    | 0.08   |
| Samsung   | USB Hard Disk          | 2      | 2       | 45    | 166   | 0.07   |
| Samsung   | SpinPoint M6           | 3      | 34      | 261   | 450   | 0.07   |
| IBM       | Travelstar 32GH, 30... | 1      | 1       | 140   | 5     | 0.06   |
| CLOVER    | Unknown                | 1      | 1       | 22    | 0     | 0.06   |
| Hitachi   | Travelstar DK23XX/D... | 6      | 7       | 322   | 211   | 0.06   |
| MediaMax  | WL640                  | 1      | 1       | 20    | 0     | 0.05   |
| CLOVER    | Hightech Utania        | 2      | 3       | 19    | 0     | 0.05   |
| Samsung   | SpinPoint MP2          | 2      | 2       | 126   | 7     | 0.05   |
| Maxtor    | DiamondMax 10 (ATA/... | 23     | 101     | 25    | 101   | 0.04   |
| IBM       | Deskstar 40GV & 75G... | 1      | 1       | 346   | 21    | 0.04   |
| Hitachi   | CinemaStar 7K1000.C    | 2      | 2       | 1042  | 38    | 0.04   |
| WDC       | Caviar WDxxxBA         | 1      | 1       | 296   | 20    | 0.04   |
| Samsung   | SpinPoint N3A          | 1      | 1       | 11    | 0     | 0.03   |
| IBM       | Unknown                | 1      | 1       | 1423  | 124   | 0.03   |
| WDC       | eServer                | 1      | 1       | 10    | 0     | 0.03   |
| Toshiba   | 2.5" HDD               | 3      | 3       | 301   | 66    | 0.03   |
| Samsung   | SpinPoint T            | 1      | 1       | 469   | 51    | 0.02   |
| Maxtor    | MaXLine III (ATA/13... | 4      | 7       | 17    | 34    | 0.02   |
| Seagate   | FireCuda               | 1      | 1       | 143   | 16    | 0.02   |
| Samsung   | SpinPoint N3C          | 1      | 1       | 96    | 11    | 0.02   |
| Seagate   | U10                    | 1      | 2       | 236   | 42    | 0.02   |
| Seagate   | Lyrion                 | 1      | 1       | 7     | 0     | 0.02   |
| Maxtor    | DiamondMax Plus 8      | 4      | 23      | 25    | 23    | 0.02   |
| Seagate   | Momentus 42            | 1      | 1       | 225   | 35    | 0.02   |
| Maxtor    | DiamondMax 1750        | 1      | 1       | 5613  | 1044  | 0.01   |
| Hitachi   | Travelstar E7K100      | 1      | 1       | 4     | 0     | 0.01   |
| Maxtor    | DiamondMax Plus 9      | 11     | 112     | 27    | 165   | 0.01   |
| Seagate   | ST1.2 CompactFlash     | 1      | 1       | 3     | 0     | 0.01   |
| MARSHAL   | 2.5" HDD               | 1      | 1       | 2     | 0     | 0.01   |
| HGST      | Proliant HardDrive     | 1      | 1       | 765   | 406   | 0.01   |
| Fujitsu   | MHY BS                 | 1      | 1       | 2382  | 1317  | 0.00   |
| Hitachi   | Ultrastar 5K3000       | 1      | 1       | 1045  | 595   | 0.00   |
| Apple     | Ultrastar A7K2000      | 1      | 2       | 176   | 110   | 0.00   |
| Maxtor    | DiamondMax 16          | 3      | 5       | 24    | 25    | 0.00   |
| Maxtor    | Fireball 541DX         | 1      | 12      | 23    | 165   | 0.00   |
| Seagate   | Enterprise NAS         | 1      | 1       | 107   | 82    | 0.00   |
| WDC       | Ultrastar DC HC330     | 1      | 1       | 1     | 0     | 0.00   |
| Maxtor    | DiamondMax D540X-4D    | 2      | 5       | 23    | 159   | 0.00   |
| Seagate   | Momentus 5400 FDE.4    | 1      | 1       | 725   | 705   | 0.00   |
| Toshiba   | 3.5" HDD P300          | 1      | 1       | 0     | 0     | 0.00   |
| HP        | 1TB SATA disk GB100... | 1      | 1       | 2402  | 3024  | 0.00   |
| Maxtor    | DiamondMax D540X-4G    | 1      | 2       | 20    | 218   | 0.00   |
| MediaMax  | WL400                  | 1      | 1       | 0     | 0     | 0.00   |
| Maxtor    | MaXLine Plus II        | 1      | 2       | 27    | 37    | 0.00   |
| Seagate   | U7                     | 1      | 1       | 194   | 274   | 0.00   |
| Seagate   | SV35.4                 | 1      | 1       | 685   | 1110  | 0.00   |
| Fujitsu   | MHK                    | 1      | 1       | 77    | 155   | 0.00   |
| HPE       | Seagate Constellati... | 1      | 1       | 94    | 857   | 0.00   |
| Samsung   | SpinPoint N1           | 1      | 1       | 188   | 3047  | 0.00   |
| Maxtor    | DiamondMax Plus 40 ... | 1      | 1       | 121   | 2068  | 0.00   |
| Seagate   | Barracuda ATA II       | 1      | 1       | 103   | 2102  | 0.00   |
| Maxtor    | DiamondMax 40 VL Ul... | 1      | 1       | 8     | 396   | 0.00   |
| ExcelStor | Unknown                | 1      | 1       | 0     | 1010  | 0.00   |
| Maxtor    | DiamondMax 3400 Ult... | 1      | 1       | 0     | 1152  | 0.00   |

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
| Advantech   | 1      | 1       | 2258  | 0     | 6.19   |
| HP          | 28     | 85      | 1432  | 107   | 2.37   |
| Quantum     | 10     | 10      | 675   | 2     | 1.44   |
| WDC         | 2078   | 25360   | 682   | 39    | 1.36   |
| Apple       | 18     | 225     | 619   | 47    | 1.36   |
| Hitachi     | 310    | 5829    | 789   | 194   | 1.25   |
| MaxDigital  | 6      | 8       | 538   | 11    | 1.19   |
| Samsung     | 159    | 3387    | 840   | 233   | 1.18   |
| Seagate     | 751    | 26091   | 619   | 175   | 1.06   |
| HGST        | 99     | 3132    | 516   | 246   | 1.00   |
| ExcelStor   | 10     | 25      | 775   | 99    | 0.94   |
| HPE         | 8      | 12      | 475   | 75    | 0.90   |
| Toshiba     | 288    | 8516    | 414   | 99    | 0.82   |
| Magnetic... | 9      | 11      | 315   | 4     | 0.73   |
| Fujitsu     | 102    | 833     | 401   | 106   | 0.67   |
| Maxtor      | 112    | 779     | 506   | 254   | 0.63   |
| IBM/Hitachi | 18     | 49      | 602   | 46    | 0.56   |
| ASMedia     | 1      | 1       | 172   | 0     | 0.47   |
| MediaMax    | 25     | 32      | 415   | 58    | 0.41   |
| MARSHAL     | 7      | 11      | 262   | 261   | 0.38   |
| Lenovo      | 2      | 6       | 91    | 0     | 0.25   |
| China       | 4      | 4       | 168   | 596   | 0.24   |
| IBM         | 8      | 9       | 709   | 28    | 0.20   |
| AMP         | 1      | 1       | 68    | 0     | 0.19   |
| Synology    | 1      | 7       | 39    | 0     | 0.11   |
| CLOVER      | 3      | 4       | 20    | 0     | 0.06   |

SSD by Model
------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

See full list of tested SSD samples in the Appendix 2 ([All_SSD.md](/All_SSD.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| Patriot   | Pyro SE            | 64 GB  | 1       | 3150  | 0     | 8.63   |
| Corsair   | Performance Pro    | 256 GB | 1       | 3050  | 0     | 8.36   |
| Patriot   | Inferno 60GB SSD   | 64 GB  | 1       | 2979  | 0     | 8.16   |
| Intel     | SSDSA2SH064G1GC    | 64 GB  | 2       | 2956  | 0     | 8.10   |
| OCZ       | DENRSTE251M45-0100 | 100 GB | 1       | 2904  | 0     | 7.96   |
| Transcend | 3E128-TS2-550B01   | 100 GB | 16      | 3197  | 1     | 7.88   |
| Samsung   | MO0200EBTJU        | 200 GB | 2       | 2807  | 0     | 7.69   |
| Intel     | SSDSA2MH080G1GC    | 80 GB  | 1       | 2796  | 0     | 7.66   |
| OCZ       | AGILITY2           | 50 GB  | 1       | 2769  | 0     | 7.59   |
| Intenso   | SSD                | 64 GB  | 1       | 2588  | 0     | 7.09   |
| Samsung   | SSD 840 Series     | 225 GB | 1       | 2573  | 0     | 7.05   |
| Toshiba   | THNSNC512GBSJ      | 512 GB | 1       | 2557  | 0     | 7.01   |
| Samsung   | MCCOE64G5MPP-0VA   | 64 GB  | 1       | 2540  | 0     | 6.96   |
| HPE       | MK0800GCTZB        | 800 GB | 1       | 2515  | 0     | 6.89   |
| SanDisk   | SDSA5GK-032G-1006  | 32 GB  | 1       | 2382  | 0     | 6.53   |
| HPE       | MK0100GCTYU        | 100 GB | 1       | 2360  | 0     | 6.47   |
| Transcend | TS256GSSD340K      | 256 GB | 1       | 2255  | 0     | 6.18   |
| Toshiba   | THNSNH060GCST      | 64 GB  | 1       | 2246  | 0     | 6.16   |
| Corsair   | CSSD-F40GB2-A      | 40 GB  | 1       | 2230  | 0     | 6.11   |
| Micron    | C400-MTFDDAC128MAM | 128 GB | 1       | 2224  | 0     | 6.09   |
| Corsair   | Force GT           | 50 GB  | 2       | 2183  | 0     | 5.98   |
| Intel     | SSDSC2BB240G6      | 240 GB | 1       | 2183  | 0     | 5.98   |
| SandForce | FM-25S2S-120GBP2   | 120 GB | 1       | 2101  | 0     | 5.76   |
| Samsung   | MZ7PD480HAGM-000DA | 480 GB | 2       | 2086  | 0     | 5.72   |
| Espada    | C3000.6-M064       | 64 GB  | 1       | 2060  | 0     | 5.65   |
| Intel     | SSDSC2BA012T4      | 1.2 TB | 1       | 2002  | 0     | 5.49   |
| Intel     | SSDSC2BA200G3C     | 200 GB | 1       | 1963  | 0     | 5.38   |
| Toshiba   | THNSNJ256GCSY      | 256 GB | 1       | 1948  | 0     | 5.34   |
| Samsung   | MZ7WD240HCFV-00003 | 240 GB | 2       | 1938  | 0     | 5.31   |
| SanDisk   | SD6SA1M064G1011    | 64 GB  | 1       | 1929  | 0     | 5.29   |
| Intel     | SSDMCEAW240A4      | 240 GB | 1       | 1918  | 0     | 5.26   |
| Samsung   | MZ7LM960HCHP00D6   | 960 GB | 1       | 1889  | 0     | 5.18   |
| Intel     | SSDSC2BB240G4      | 240 GB | 5       | 1885  | 0     | 5.17   |
| SanDisk   | SD7UN3Q128G1022    | 128 GB | 1       | 1881  | 0     | 5.15   |
| Plextor   | PX-G512M6e         | 512 GB | 1       | 1878  | 0     | 5.15   |
| Seagate   | ST240HM000-1G5152  | 240 GB | 1       | 1871  | 0     | 5.13   |
| Intel     | SSDSC2BB240G4C     | 240 GB | 1       | 1870  | 0     | 5.12   |
| Intel     | SSDSC2BB600G4      | 600 GB | 4       | 1855  | 0     | 5.08   |
| Crucial   | M4-CT064M4SSD1     | 64 GB  | 1       | 1845  | 0     | 5.06   |
| EXBOM     | SSD-25SA240G       | 240 GB | 1       | 1829  | 0     | 5.01   |
| OCZ       | VERTEX2 3.5        | 240 GB | 1       | 1798  | 0     | 4.93   |
| Kingston  | SVP100S2512G       | 512 GB | 1       | 1795  | 0     | 4.92   |
| Intel     | SSDSC2BB800G4      | 800 GB | 2       | 1780  | 0     | 4.88   |
| Kingston  | SNVP325S2128GB     | 128 GB | 2       | 1729  | 0     | 4.74   |
| Samsung   | MZHPV256HDGL-000H1 | 256 GB | 1       | 1721  | 0     | 4.72   |
| China     | mSATAS3-0060-XQ... | 64 GB  | 1       | 1717  | 0     | 4.71   |
| Corsair   | Neutron XTI SSD    | 480 GB | 1       | 1717  | 0     | 4.70   |
| Intel     | SSDSC2BB800G6      | 800 GB | 1       | 1709  | 0     | 4.68   |
| Corsair   | CMFSSD-256GBG2D    | 256 GB | 1       | 1693  | 0     | 4.64   |
| OCZ       | D2RSTK251E19-0100  | 100 GB | 1       | 1689  | 0     | 4.63   |
| OCZ       | VERTEX3            | 96 GB  | 1       | 1686  | 0     | 4.62   |
| Samsung   | MZ7PD128HCFV-000H7 | 128 GB | 1       | 1668  | 0     | 4.57   |
| ADATA     | SP310              | 32 GB  | 1       | 1658  | 0     | 4.54   |
| HPE       | MK0200GEYKC        | 200 GB | 1       | 1653  | 0     | 4.53   |
| Intel     | SSDSC2BA200G3      | 200 GB | 2       | 1653  | 0     | 4.53   |
| Kingston  | SVP100S296G        | 96 GB  | 2       | 1638  | 0     | 4.49   |
| Samsung   | SSD PB22-JS3 FD... | 128 GB | 1       | 1626  | 0     | 4.46   |
| China     | EDGSD25240GBOOS... | 240 GB | 1       | 1625  | 0     | 4.45   |
| OCZ       | VECTOR             | 512 GB | 1       | 1610  | 0     | 4.41   |
| Samsung   | MZHPU256HCGL-000L1 | 256 GB | 1       | 1608  | 0     | 4.41   |
| Intel     | SSDSC2BF240A4H     | 240 GB | 1       | 1607  | 0     | 4.41   |
| SanDisk   | SD6SB2M256G1022I   | 256 GB | 1       | 1592  | 0     | 4.36   |
| OCZ       | REVODRIVE3         | 120 GB | 4       | 1590  | 0     | 4.36   |
| Corsair   | Force GT           | 240 GB | 4       | 1689  | 1     | 4.25   |
| Samsung   | SSD PM851a 2.5 7mm | 1 TB   | 3       | 1544  | 0     | 4.23   |
| OCZ       | VERTEX2            | 40 GB  | 2       | 1543  | 0     | 4.23   |
| HPE       | MK0400GEYKD        | 400 GB | 1       | 1533  | 0     | 4.20   |
| Toshiba   | THNSFC064GBSJ      | 64 GB  | 1       | 1526  | 0     | 4.18   |
| Samsung   | SATA SSD           | 256 GB | 1       | 1519  | 0     | 4.16   |
| Intel     | SSDSA2SH032G1GN    | 32 GB  | 2       | 1518  | 0     | 4.16   |
| OCZ       | AGILITY2           | 40 GB  | 1       | 1516  | 0     | 4.15   |
| Corsair   | Force 3 SSD        | 180 GB | 5       | 1832  | 1     | 4.15   |
| Samsung   | SATA SSD           | 128 GB | 1       | 1509  | 0     | 4.14   |
| Intel     | SSDSC2BX400G4      | 400 GB | 1       | 1508  | 0     | 4.13   |
| OCZ       | VERTEX2 3.5        | 90 GB  | 1       | 1507  | 0     | 4.13   |
| Intel     | SSDSC2BA100G3      | 100 GB | 24      | 1576  | 1     | 4.13   |
| Intel     | SSDSC2BB160G4      | 160 GB | 3       | 1488  | 0     | 4.08   |
| SanDisk   | SD7SN6S512G1122    | 512 GB | 1       | 1488  | 0     | 4.08   |
| Advantech | SQF-S25M8-64G-SAC  | 64 GB  | 1       | 1483  | 0     | 4.06   |
| OCZ       | VERTEX v1.10       | 64 GB  | 3       | 1655  | 1     | 4.05   |
| Samsung   | MZNLN512HCJH-00000 | 512 GB | 2       | 1476  | 0     | 4.04   |
| ADATA     | XM11               | 120 GB | 2       | 1508  | 1     | 4.03   |
| Kingston  | SVP100S264G        | 64 GB  | 3       | 1469  | 0     | 4.03   |
| Samsung   | MZ7PC256HAFU-000L7 | 256 GB | 4       | 1464  | 0     | 4.01   |
| Intel     | SSDSA2BW600G3D     | 600 GB | 1       | 1462  | 0     | 4.01   |
| Intel     | SSDSC1BG200G4      | 200 GB | 1       | 1438  | 0     | 3.94   |
| Crucial   | M4-CT064M4SSD3     | 64 GB  | 1       | 1438  | 0     | 3.94   |
| Toshiba   | THNSN8240PCSE      | 240 GB | 1       | 1434  | 0     | 3.93   |
| Toshiba   | THNSN8480PCSE      | 480 GB | 1       | 1433  | 0     | 3.93   |
| Samsung   | MZ7LM240HCGR-00003 | 240 GB | 2       | 1433  | 0     | 3.93   |
| SanDisk   | SDSA6DM-016G-1006  | 16 GB  | 4       | 1413  | 0     | 3.87   |
| SuperM... | SSD                | 16 GB  | 1       | 1404  | 0     | 3.85   |
| Intel     | SSDSC2BP480G4      | 480 GB | 9       | 1416  | 1     | 3.84   |
| WDC       | WD1001X06X-00SJVT0 | 1.1 TB | 2       | 1381  | 0     | 3.79   |
| SMART     | SSD XceedValue2... | 32 GB  | 1       | 1374  | 0     | 3.77   |
| Intel     | SSDMCEAC120B3A     | 120 GB | 2       | 1373  | 0     | 3.76   |
| Samsung   | MZ7LN512HCHP-00000 | 512 GB | 2       | 1362  | 0     | 3.73   |
| Samsung   | MO0100EBTJT        | 100 GB | 1       | 1361  | 0     | 3.73   |
| Samsung   | MZ7LN256HMJP-00000 | 256 GB | 7       | 1348  | 0     | 3.69   |
| Samsung   | MZHPU512HCGL-00004 | 512 GB | 1       | 1347  | 0     | 3.69   |
| Kingston  | SKC310S37A960G     | 960 GB | 1       | 1340  | 0     | 3.67   |
| Micron    | M510DC_MTFDDAK2... | 240 GB | 2       | 1322  | 0     | 3.62   |
| Samsung   | MZ7GE960HMHP-00003 | 960 GB | 2       | 2613  | 508   | 3.59   |
| Intel     | SSDSC2BB480G4      | 480 GB | 5       | 1302  | 0     | 3.57   |
| SK hynix  | HFS250G32TND-N1A0A | 250 GB | 1       | 1302  | 0     | 3.57   |
| Apacer    | AST680S            | 480 GB | 1       | 1293  | 0     | 3.54   |
| Corsair   | Force GS           | 360 GB | 1       | 1291  | 0     | 3.54   |
| Intel     | SSDSC2BB120G7R     | 120 GB | 4       | 1287  | 0     | 3.53   |
| SanDisk   | SD5SE2128G1002E    | 128 GB | 4       | 1285  | 0     | 3.52   |
| Toshiba   | THNS128GG4BAAA-... | 128 GB | 4       | 1284  | 0     | 3.52   |
| Samsung   | SSD PM871a 2.5 7mm | 256 GB | 1       | 1282  | 0     | 3.51   |
| Intel     | SSDSC2BB080G4      | 80 GB  | 10      | 1281  | 0     | 3.51   |
| Corsair   | Force SSD          | 120 GB | 1       | 1271  | 0     | 3.48   |
| Samsung   | MZ7KM960HAHP-00005 | 960 GB | 2       | 1259  | 0     | 3.45   |
| Toshiba   | THNSNJ120PCSZ      | 120 GB | 2       | 1255  | 0     | 3.44   |
| OCZ       | VERTEX2            | 64 GB  | 21      | 1289  | 13    | 3.44   |
| Intel     | SSDSA2CW080G3      | 80 GB  | 19      | 1289  | 1     | 3.43   |
| OCZ       | VERTEX PLUS R2     | 64 GB  | 3       | 1248  | 0     | 3.42   |
| TANCA     | SSD                | 120 GB | 1       | 1246  | 0     | 3.42   |
| Samsung   | MZ7KM480HMHQ-00005 | 480 GB | 5       | 1243  | 0     | 3.41   |
| Kingston  | SSDNOW             | 32 GB  | 4       | 1242  | 0     | 3.40   |
| Seagate   | XF1230-1A0960      | 960 GB | 2       | 1236  | 0     | 3.39   |
| Samsung   | MZ7LM960HMJP-00005 | 960 GB | 2       | 1234  | 0     | 3.38   |
| Intel     | SSDSC2BB120G4      | 120 GB | 3       | 1218  | 0     | 3.34   |
| Intel     | SSDSA2BW160G3      | 160 GB | 3       | 1222  | 402   | 3.34   |
| Apple     | SSD SM1024F        | 1 TB   | 10      | 1217  | 0     | 3.34   |
| Samsung   | SSD 830 Series     | 512 GB | 15      | 1280  | 135   | 3.32   |
| Corsair   | Force 3 SSD        | 240 GB | 12      | 1344  | 88    | 3.32   |
| ADATA     | SP920SS            | 1 TB   | 1       | 1211  | 0     | 3.32   |
| Samsung   | TK0120GECQL        | 120 GB | 1       | 1208  | 0     | 3.31   |
| Kingston  | SVP200S360G        | 64 GB  | 9       | 1205  | 0     | 3.30   |
| Corsair   | Force GT           | 180 GB | 3       | 1205  | 0     | 3.30   |
| Samsung   | MZHPV512HDGL-00000 | 512 GB | 5       | 1204  | 0     | 3.30   |
| Samsung   | SSD 840 EVO 1TB... | 1 TB   | 1       | 1204  | 0     | 3.30   |
| Samsung   | SSD 840 EVO        | 1 TB   | 48      | 1232  | 3     | 3.29   |
| Intel     | SSDSC2BA800G4      | 800 GB | 4       | 1199  | 0     | 3.29   |
| Samsung   | SSD RBX Series ... | 128 GB | 1       | 1196  | 0     | 3.28   |
| Samsung   | MZ7TN512HDHP-00007 | 512 GB | 1       | 1194  | 0     | 3.27   |
| Toshiba   | THNSFC256GAMJ      | 256 GB | 2       | 1189  | 0     | 3.26   |
| OCZ       | TRION150           | 960 GB | 2       | 1176  | 0     | 3.22   |
| Seagate   | ST480HM000-1G5162  | 480 GB | 2       | 1282  | 1     | 3.20   |
| Samsung   | SSD 850 PRO        | 1 TB   | 56      | 1192  | 1     | 3.20   |
| Samsung   | MZ7LM960HCHP-00003 | 960 GB | 4       | 1165  | 0     | 3.19   |
| Micron    | MTFDDAK064MAR-1... | 64 GB  | 1       | 1164  | 0     | 3.19   |
| Intel     | SSDSC2CW240A3      | 240 GB | 40      | 1164  | 0     | 3.19   |
| Apple     | SSD SM128E         | 121 GB | 5       | 1577  | 5     | 3.18   |
| MyDigi... | SB M2 SSD          | 240 GB | 1       | 1161  | 0     | 3.18   |
| Samsung   | MZMPC064HBDR-000L1 | 64 GB  | 1       | 1157  | 0     | 3.17   |
| Toshiba   | THNSNC128GMMJ      | 128 GB | 5       | 1148  | 0     | 3.15   |
| HP        | VK0300GDUQV        | 304 GB | 1       | 1137  | 0     | 3.12   |
| Intel     | SSDSC2BB120G6      | 120 GB | 3       | 1133  | 0     | 3.11   |
| Corsair   | Force LS SSD       | 960 GB | 1       | 1129  | 0     | 3.09   |
| Samsung   | MZ7KM240HMHQ-00005 | 240 GB | 2       | 1125  | 0     | 3.08   |
| Kingston  | SH103S390G         | 90 GB  | 4       | 1123  | 0     | 3.08   |
| Micron    | MTFDDAK128MBF-1... | 128 GB | 1       | 1117  | 0     | 3.06   |
| Samsung   | MZ7LM3T8HCJM-00003 | 3.8 TB | 1       | 1115  | 0     | 3.06   |
| OCZ       | SOLID3             | 64 GB  | 6       | 1338  | 186   | 3.05   |
| OYUNKEY   | SSD                | 360 GB | 1       | 1107  | 0     | 3.04   |
| PNY       | CS2211 240GB SSD   | 240 GB | 1       | 1102  | 0     | 3.02   |
| Corsair   | Force GS           | 480 GB | 3       | 1884  | 15    | 3.02   |
| OCZ       | AGILITY4           | 128 GB | 6       | 1095  | 0     | 3.00   |
| Kingston  | RBU-SC400S37256G   | 256 GB | 2       | 1095  | 0     | 3.00   |
| OCZ       | VERTEX2            | 120 GB | 13      | 1094  | 0     | 3.00   |
| Intel     | SSDSA2CT040G3      | 40 GB  | 9       | 1093  | 0     | 2.99   |
| Toshiba   | TL100              | 120 GB | 5       | 1089  | 0     | 2.99   |
| Corsair   | Force GS           | 180 GB | 3       | 1087  | 0     | 2.98   |
| Micron    | M500_MTFDDAK480MAV | 480 GB | 1       | 1083  | 0     | 2.97   |
| Intel     | SSDSA2MH080G1HP    | 80 GB  | 1       | 1075  | 0     | 2.95   |
| PNY       | CS1311 960GB SSD   | 960 GB | 4       | 1074  | 0     | 2.94   |
| OCZ       | REVODRIVE350       | 120 GB | 4       | 1073  | 0     | 2.94   |
| Samsung   | MZ7PC128HAFU-000L1 | 128 GB | 4       | 1069  | 0     | 2.93   |
| KingSpec  | SPK-SF12-M120      | 120 GB | 2       | 1069  | 0     | 2.93   |
| Crucial   | CT500MX200SSD3     | 500 GB | 5       | 1066  | 0     | 2.92   |
| Crucial   | M4-CT512M4SSD2     | 512 GB | 12      | 1454  | 519   | 2.91   |
| Micron    | MTFDDAK512TBN-1... | 512 GB | 1       | 1062  | 0     | 2.91   |
| Samsung   | MZNTE256HMHP-000L1 | 256 GB | 1       | 1061  | 0     | 2.91   |
| Mushkin   | MKNSSDCR120GB      | 120 GB | 8       | 1306  | 4     | 2.91   |
| SanDisk   | SDSSDXP480G        | 480 GB | 1       | 1058  | 0     | 2.90   |
| SK        | SKhynix SC300 H... | 256 GB | 1       | 1054  | 0     | 2.89   |
| Patriot   | Blast              | 480 GB | 2       | 1050  | 0     | 2.88   |
| Micron    | 5100_MTFDDAK960TCB | 960 GB | 3       | 1048  | 0     | 2.87   |
| SanDisk   | SD8SB8U1T00        | 1 TB   | 1       | 1045  | 0     | 2.86   |
| Intel     | SSDMCEAC120B3      | 120 GB | 3       | 1502  | 2     | 2.86   |
| Intel     | SSDSC2BX016T4      | 1.6 TB | 1       | 1040  | 0     | 2.85   |
| Micron    | C400-MTFDDAK128MAM | 128 GB | 4       | 1032  | 0     | 2.83   |
| Samsung   | MZ7PC128HAFU-000L5 | 128 GB | 2       | 1028  | 0     | 2.82   |
| China     | R580               | 120 GB | 1       | 1024  | 0     | 2.81   |
| Intel     | SSDSC2CW180A3      | 180 GB | 17      | 1022  | 0     | 2.80   |
| Toshiba   | THNSNJ512GDNU      | 512 GB | 2       | 1021  | 0     | 2.80   |
| SanDisk   | SDSSDRC032G        | 32 GB  | 9       | 1017  | 0     | 2.79   |
| ADATA     | SP310              | 64 GB  | 1       | 1015  | 0     | 2.78   |
| Samsung   | SSD PM830 2.5" 7mm | 256 GB | 18      | 1064  | 57    | 2.77   |
| Innodisk  | Corp. - mSATA 3ME3 | 16 GB  | 1       | 1009  | 0     | 2.76   |
| Crucial   | C300-CTFDDAC064MAG | 64 GB  | 10      | 1187  | 202   | 2.76   |
| ADATA     | SP800              | 32 GB  | 2       | 1001  | 0     | 2.74   |
| Hyundai   | 120GB SSD          | 120 GB | 1       | 997   | 0     | 2.73   |
| Kingston  | SQ500S37960G       | 960 GB | 1       | 995   | 0     | 2.73   |
| Samsung   | SSD 830 Series     | 128 GB | 66      | 999   | 16    | 2.72   |
| Toshiba   | THNSNH256GMCT      | 256 GB | 4       | 991   | 0     | 2.72   |
| SanDisk   | SD7SB7S512G1122    | 512 GB | 4       | 987   | 0     | 2.71   |
| Kingston  | SH100S3120G        | 120 GB | 10      | 987   | 0     | 2.70   |
| Samsung   | SSD 850 EVO        | 2 TB   | 25      | 984   | 0     | 2.70   |
| Lite-On   | PH5-CE120          | 120 GB | 1       | 980   | 0     | 2.69   |
| SanDisk   | SD7SB6S128G1122    | 128 GB | 8       | 975   | 0     | 2.67   |
| Kingston  | SEDC400S37960G     | 960 GB | 1       | 974   | 0     | 2.67   |
| Intel     | SSDSC2BX200G4      | 200 GB | 2       | 969   | 0     | 2.66   |
| Crucial   | M4-CT128M4SSD2     | 128 GB | 74      | 1029  | 111   | 2.65   |
| SanDisk   | SD6SF1M064G1022    | 64 GB  | 2       | 963   | 0     | 2.64   |
| Samsung   | MZRPA128HMCD-000SO | 64 GB  | 14      | 958   | 0     | 2.63   |
| Samsung   | SSD 840 EVO        | 500 GB | 91      | 1015  | 21    | 2.62   |
| Corsair   | CMFSSD-128GBG2D    | 128 GB | 1       | 954   | 0     | 2.62   |
| Crucial   | M4-CT064M4SSD2     | 64 GB  | 29      | 1072  | 180   | 2.61   |
| China     | SSD512GB           | 512 GB | 1       | 951   | 0     | 2.61   |
| OCZ       | VECTOR             | 256 GB | 4       | 939   | 0     | 2.57   |
| Intel     | SSDSC2BB480G7      | 480 GB | 3       | 937   | 0     | 2.57   |
| Micron    | M600_MTFDDAK1T0MBF | 1 TB   | 8       | 929   | 0     | 2.55   |
| Kingston  | SE50S3480G         | 480 GB | 10      | 1104  | 1     | 2.54   |
| Crucial   | C300-CTFDDAC256MAG | 256 GB | 4       | 1552  | 605   | 2.52   |
| Samsung   | MZMLN256HCHP-000   | 256 GB | 1       | 919   | 0     | 2.52   |
| ExeGate   | EX280461RUS        | 128 GB | 1       | 917   | 0     | 2.51   |
| Samsung   | MZ7KM480HAHP-00005 | 480 GB | 1       | 916   | 0     | 2.51   |
| SanDisk   | SDLF1CRR-019T-1HA2 | 1.9 TB | 1       | 916   | 0     | 2.51   |
| Intel     | SSDSA2BW080G3H     | 80 GB  | 1       | 914   | 0     | 2.50   |
| Corsair   | Force GT           | 120 GB | 21      | 1118  | 2     | 2.50   |
| Samsung   | MZ7LN128HCHP-000H1 | 128 GB | 3       | 903   | 0     | 2.48   |
| Intel     | SSDMCEAW120A4      | 120 GB | 2       | 902   | 0     | 2.47   |
| Patriot   | Ignite             | 960 GB | 1       | 901   | 0     | 2.47   |
| Samsung   | Sasmung SSD 883... | 480 GB | 1       | 900   | 0     | 2.47   |
| Micron    | 5200_MTFDDAK1T9TDD | 1.9 TB | 1       | 893   | 0     | 2.45   |
| Samsung   | Portable SSD T3    | 250 GB | 1       | 892   | 0     | 2.45   |
| Intel     | SSDSA2CW120G3      | 120 GB | 23      | 1132  | 44    | 2.45   |
| Micron    | MTFDDAK256MBF-1... | 256 GB | 4       | 892   | 0     | 2.44   |
| Samsung   | MZMTE128HMGR-00000 | 128 GB | 1       | 887   | 0     | 2.43   |
| Samsung   | MZ7WD480HAGM-000D2 | 480 GB | 1       | 886   | 0     | 2.43   |
| Samsung   | MZ7TE512HMHP-000L1 | 512 GB | 6       | 885   | 0     | 2.43   |
| SanDisk   | SD7SB3Q064G        | 56 GB  | 2       | 885   | 0     | 2.43   |
| SK hynix  | SC300B SATA        | 512 GB | 3       | 882   | 0     | 2.42   |
| Samsung   | SSD PM800 2.5"     | 256 GB | 2       | 878   | 0     | 2.41   |
| Intel     | SSDSC2BB800G7R     | 800 GB | 2       | 1166  | 1     | 2.40   |
| Toshiba   | THNS064GG2BNAA     | 64 GB  | 7       | 872   | 0     | 2.39   |
| KingDian  | N400               | 240 GB | 1       | 871   | 0     | 2.39   |
| Samsung   | SSD 840 PRO Series | 128 GB | 78      | 978   | 4     | 2.39   |
| Micron    | C400-MTFDDAK512MAM | 512 GB | 1       | 870   | 0     | 2.39   |
| ADATA     | SX930              | 480 GB | 2       | 869   | 0     | 2.38   |
| Intel     | SSDSC2CT060A3      | 64 GB  | 11      | 1080  | 1     | 2.38   |
| SanDisk   | SD8SB8U-128G-1016  | 128 GB | 1       | 868   | 0     | 2.38   |
| Crucial   | M4-CT256M4SSD1     | 256 GB | 4       | 957   | 253   | 2.38   |
| Axiom     | Signature III SSD  | 240 GB | 1       | 866   | 0     | 2.37   |
| Samsung   | MZ7LF128HCHP-00000 | 128 GB | 1       | 865   | 0     | 2.37   |
| Phison    | SATA SSD           | 16 GB  | 2       | 862   | 0     | 2.36   |
| Samsung   | MZ7TE256HMHP-00000 | 256 GB | 3       | 861   | 0     | 2.36   |
| Micron    | MTFDDAK256MAM-1K1  | 256 GB | 6       | 859   | 0     | 2.35   |
| Apple     | SSD TS256A         | 256 GB | 1       | 858   | 0     | 2.35   |
| Samsung   | SSD 830 Series     | 256 GB | 49      | 867   | 21    | 2.35   |
| Micron    | M600_MTFDDAK512MBF | 512 GB | 2       | 855   | 0     | 2.34   |
| Corsair   | Force 3 SSD        | 120 GB | 43      | 961   | 61    | 2.34   |
| WDC       | WDBNCE2500PNC-WRSN | 250 GB | 3       | 849   | 0     | 2.33   |
| KingSpec  | P4-960             | 960 GB | 1       | 846   | 0     | 2.32   |
| MyDigi... | BP5                | 240 GB | 4       | 845   | 0     | 2.32   |
| Samsung   | SSD 830 Series     | 64 GB  | 25      | 839   | 0     | 2.30   |
| Samsung   | MZ7TY256HDHP-00007 | 256 GB | 2       | 834   | 0     | 2.29   |
| Apple     | SSD SM0128F        | 121 GB | 1       | 833   | 0     | 2.28   |
| Kingston  | RBU-SC150S3732G    | 32 GB  | 1       | 833   | 0     | 2.28   |
| Kingston  | SMSR150S3256G      | 128 GB | 2       | 833   | 0     | 2.28   |
| Patriot   | Blaze SSD ATA D... | 240 GB | 1       | 833   | 0     | 2.28   |
| Phison    | BP4 mSATA SSD      | 240 GB | 1       | 833   | 0     | 2.28   |
| Phison    | UGBA1TPH32H0S2-... | 32 GB  | 1       | 833   | 0     | 2.28   |
| Team      | L5 LITE SSD        | 240 GB | 2       | 1068  | 148   | 2.28   |
| Corsair   | Force 3 SSD        | 64 GB  | 20      | 863   | 1     | 2.28   |
| ADATA     | SSD S510           | 120 GB | 11      | 844   | 1     | 2.28   |
| Mushkin   | MKNSSDCR60GB-7     | 64 GB  | 3       | 865   | 2     | 2.27   |
| ADATA     | SP600              | 128 GB | 13      | 826   | 0     | 2.26   |
| Samsung   | SSD 840 Series     | 500 GB | 15      | 962   | 4     | 2.26   |
| Crucial   | CT120M500SSD3      | 120 GB | 5       | 911   | 7     | 2.26   |
| SK hynix  | HFS128G39MNC-3310A | 128 GB | 1       | 824   | 0     | 2.26   |
| Intel     | SSDSC2BB960G7      | 960 GB | 1       | 1648  | 1     | 2.26   |
| Kingston  | SNVP325S2512GB     | 512 GB | 1       | 822   | 0     | 2.25   |
| WDC       | WDBNCE0010PNC-WRSN | 1 TB   | 2       | 821   | 0     | 2.25   |
| Innodisk  | DES25-64GM41BC1... | 64 GB  | 1       | 821   | 0     | 2.25   |
| Samsung   | SSD 840 PRO Series | 256 GB | 122     | 904   | 11    | 2.25   |
| Samsung   | SSD 840 Series     | 250 GB | 64      | 894   | 1     | 2.24   |
| ADATA     | SSD S599           | 55 GB  | 1       | 815   | 0     | 2.23   |
| SK hynix  | HFS256G39MND-3510A | 256 GB | 3       | 814   | 0     | 2.23   |
| Intel     | SSDSC2BB016T7      | 1.6 TB | 1       | 1625  | 1     | 2.23   |
| SanDisk   | SDSA6MM-016G-1006  | 16 GB  | 13      | 902   | 121   | 2.22   |
| SanDisk   | SD6SP1M128G1102    | 128 GB | 2       | 809   | 0     | 2.22   |
| Samsung   | SSD 850 PRO        | 512 GB | 109     | 824   | 10    | 2.22   |
| Intel     | SSDSCKGF180A4L     | 180 GB | 1       | 809   | 0     | 2.22   |
| SanDisk   | SSD U110           | 128 GB | 5       | 805   | 0     | 2.21   |
| Crucial   | M4-CT128M4SSD3     | 128 GB | 3       | 801   | 0     | 2.20   |
| Corsair   | Neutron SSD        | 256 GB | 2       | 801   | 0     | 2.20   |
| OCZ       | DENRSTE251M45-0... | 100 GB | 1       | 801   | 0     | 2.20   |
| Toshiba   | THNSNH512GCST      | 512 GB | 3       | 800   | 0     | 2.19   |
| OCZ       | VECTOR180          | 480 GB | 2       | 798   | 0     | 2.19   |
| Samsung   | SSD PM800 Serie... | 256 GB | 4       | 988   | 2     | 2.19   |
| SanDisk   | SSD U110           | 64 GB  | 3       | 797   | 0     | 2.18   |
| OCZ       | VERTEX PLUS R2     | 247 GB | 1       | 797   | 0     | 2.18   |
| Samsung   | MZMTE512HMHP-000MV | 512 GB | 4       | 797   | 0     | 2.18   |
| Corsair   | Force GT           | 64 GB  | 8       | 948   | 4     | 2.17   |
| Samsung   | SSD PM830 mSATA    | 256 GB | 2       | 787   | 0     | 2.16   |
| Toshiba   | THNSNH060GMCT      | 64 GB  | 1       | 787   | 0     | 2.16   |
| ADATA     | SP600              | 256 GB | 14      | 783   | 0     | 2.15   |
| SanDisk   | SDSSDHII960G       | 960 GB | 11      | 830   | 1     | 2.14   |
| Kingston  | SVP200S37A120G     | 120 GB | 20      | 948   | 87    | 2.14   |
| Corsair   | CSSD-F115GB2-A     | 115 GB | 1       | 781   | 0     | 2.14   |
| Radeon    | R7                 | 120 GB | 4       | 778   | 0     | 2.13   |
| SanDisk   | SD7SB6S128G1001    | 128 GB | 1       | 778   | 0     | 2.13   |
| Corsair   | Force GS           | 90 GB  | 1       | 776   | 0     | 2.13   |
| SPCC      | SSD                | 480 GB | 7       | 775   | 0     | 2.12   |
| SanDisk   | SD9SB8W256G1014    | 256 GB | 1       | 772   | 0     | 2.12   |
| Samsung   | SSD 850 PRO        | 128 GB | 55      | 835   | 19    | 2.11   |
| TCSUNB0W  | X3                 | 64 GB  | 1       | 767   | 0     | 2.10   |
| Crucial   | M4-CT128M4SSD1     | 128 GB | 11      | 786   | 92    | 2.10   |
| Lite-On   | ECE-240NAS         | 240 GB | 1       | 766   | 0     | 2.10   |
| Samsung   | MZ7LN256HAJQ-000H1 | 256 GB | 4       | 765   | 0     | 2.10   |
| Kingston  | SVP200S37A480G     | 480 GB | 1       | 765   | 0     | 2.10   |
| OCZ       | VERTEX2 3.5        | 115 GB | 3       | 765   | 0     | 2.10   |
| Samsung   | SSD PM830 2.5" 7mm | 128 GB | 23      | 876   | 88    | 2.09   |
| SanDisk   | SD8SN8U1T001122    | 1 TB   | 5       | 761   | 0     | 2.09   |
| OWC       | Mercury EXTREME... | 480 GB | 6       | 857   | 13    | 2.08   |
| OCZ       | VERTEX4            | 256 GB | 36      | 1050  | 1     | 2.08   |
| OCZ       | AGILITY3           | 64 GB  | 66      | 933   | 4     | 2.08   |
| Kingston  | SVP200S3120G       | 120 GB | 14      | 830   | 143   | 2.08   |
| Samsung   | MZNLF192HCGS-000L1 | 192 GB | 3       | 757   | 0     | 2.08   |
| Patriot   | Flare              | 120 GB | 1       | 753   | 0     | 2.06   |
| Samsung   | MZMPC032HBCD-000D1 | 32 GB  | 8       | 753   | 0     | 2.06   |
| Kingston  | SEDC400S37480G     | 480 GB | 2       | 752   | 0     | 2.06   |
| Samsung   | MZ7PC128HAFU-000H1 | 128 GB | 7       | 751   | 0     | 2.06   |
| SK hynix  | SC300B SATA        | 256 GB | 2       | 751   | 0     | 2.06   |
| Pioneer   | APS-SL3N-128       | 128 GB | 1       | 750   | 0     | 2.06   |
| Intel     | SSDSC2BB300G4      | 304 GB | 3       | 750   | 0     | 2.06   |
| Kingston  | SH103S3120G        | 120 GB | 98      | 819   | 11    | 2.05   |
| PNY       | CS1311 240GB SSD   | 240 GB | 26      | 748   | 0     | 2.05   |
| PNY       | EU SSD CS1311      | 240 GB | 1       | 746   | 0     | 2.05   |
| Samsung   | SSD 840 EVO        | 250 GB | 264     | 791   | 13    | 2.04   |
| Toshiba   | KHK61RSE960G       | 960 GB | 2       | 743   | 0     | 2.04   |
| Transcend | TS128GSSD320       | 128 GB | 3       | 743   | 0     | 2.04   |
| Super ... | FTM25N325H         | 250 GB | 1       | 742   | 0     | 2.03   |
| Samsung   | SSD 750 EVO        | 500 GB | 39      | 742   | 0     | 2.03   |
| CFD       | CSSD-S6B240CG3VX   | 240 GB | 1       | 742   | 0     | 2.03   |
| ADATA     | SP600FA3-256GM     | 256 GB | 1       | 735   | 0     | 2.02   |
| Samsung   | MZ7PD128HCFV-000H1 | 128 GB | 8       | 735   | 0     | 2.02   |
| China     | MTG-480GB          | 480 GB | 1       | 732   | 0     | 2.01   |
| Crucial   | FCCT128M4SSD1      | 128 GB | 1       | 732   | 0     | 2.01   |
| Toshiba   | THNSNJ256G8NU      | 256 GB | 7       | 731   | 0     | 2.01   |
| Mushkin   | MKNSSDAT60GB-DX    | 64 GB  | 1       | 728   | 0     | 2.00   |
| Crucial   | CT512MX100SSD1     | 512 GB | 44      | 775   | 1     | 1.99   |
| Samsung   | SSD PM800 2.5"     | 128 GB | 5       | 724   | 0     | 1.99   |
| Samsung   | MZ7PA256HMDR-010H1 | 256 GB | 2       | 842   | 520   | 1.98   |
| Micro ... | G2 series          | 64 GB  | 1       | 722   | 0     | 1.98   |
| Intel     | SSDSC2BW240A3L     | 240 GB | 8       | 721   | 0     | 1.98   |
| Crucial   | M4-CT256M4SSD2     | 256 GB | 47      | 891   | 195   | 1.97   |
| Kingston  | SMSM151S3128GD     | 128 GB | 1       | 718   | 0     | 1.97   |
| Corsair   | CSSD-F60GB2        | 64 GB  | 7       | 1343  | 286   | 1.96   |
| Samsung   | MZ7TD512HAGM-000L1 | 512 GB | 3       | 715   | 0     | 1.96   |
| Samsung   | SSD 840 PRO Series | 512 GB | 35      | 1038  | 94    | 1.96   |
| SanDisk   | SD8SB8U512G1001    | 512 GB | 1       | 713   | 0     | 1.95   |
| SanDisk   | SDSA6MM-032G-1006  | 32 GB  | 2       | 712   | 0     | 1.95   |
| Samsung   | SSD 840 EVO        | 120 GB | 207     | 777   | 18    | 1.95   |
| Samsung   | MZ7PD256HAFV-000H7 | 256 GB | 10      | 711   | 0     | 1.95   |
| Samsung   | MZ7LM3T8HMLP-00005 | 3.8 TB | 1       | 711   | 0     | 1.95   |
| Samsung   | SSD 840 Series     | 120 GB | 84      | 785   | 1     | 1.94   |
| Corsair   | Force LE SSD       | 240 GB | 4       | 709   | 0     | 1.94   |
| SanDisk   | SD5SB2-128G-1006E  | 128 GB | 6       | 708   | 0     | 1.94   |
| SanDisk   | X300 2.5 7MM       | 256 GB | 2       | 707   | 0     | 1.94   |
| Samsung   | SSD 850 PRO        | 256 GB | 209     | 735   | 1     | 1.94   |
| Apple     | SSD TS256C         | 256 GB | 9       | 706   | 0     | 1.94   |
| Samsung   | SSD 840 EVO 120... | 120 GB | 10      | 713   | 1     | 1.93   |
| OCZ       | NOCTI              | 64 GB  | 1       | 704   | 0     | 1.93   |
| Plextor   | PX-128M2S          | 128 GB | 3       | 833   | 1     | 1.93   |
| Samsung   | MZHPU256HCGL-000H1 | 256 GB | 3       | 704   | 0     | 1.93   |
| Samsung   | SSD 850 EVO M.2    | 1 TB   | 8       | 704   | 0     | 1.93   |
| Kston     | SSD                | 64 GB  | 1       | 699   | 0     | 1.92   |
| Kingston  | SVP100S2128G       | 128 GB | 1       | 698   | 0     | 1.91   |
| Toshiba   | THNS128GG4BBAA     | 128 GB | 3       | 698   | 0     | 1.91   |
| Crucial   | C300-CTFDDAC128MAG | 128 GB | 11      | 1003  | 185   | 1.91   |
| Samsung   | MZ7PD256HCGM-000H7 | 256 GB | 24      | 703   | 102   | 1.91   |
| Samsung   | SSD 840 EVO 250... | 250 GB | 12      | 690   | 0     | 1.89   |
| Samsung   | MZMPC256HBGJ-000H1 | 256 GB | 2       | 690   | 0     | 1.89   |
| Kingston  | SVP200S390G        | 90 GB  | 1       | 686   | 0     | 1.88   |
| Intel     | SSDSC2BB240G7      | 240 GB | 5       | 686   | 0     | 1.88   |
| SK hynix  | HFS512G32MND-3312A | 512 GB | 1       | 686   | 0     | 1.88   |
| Smart     | SSD XceedValue2... | 32 GB  | 1       | 681   | 0     | 1.87   |
| Samsung   | MZ7LN256HCHP-00007 | 256 GB | 1       | 681   | 0     | 1.87   |
| SanDisk   | X400 2.5 7MM       | 256 GB | 9       | 678   | 0     | 1.86   |
| OCZ       | INTREPID 3700 1... | 1.8 TB | 1       | 677   | 0     | 1.86   |
| Kingston  | SHFS37A480G        | 480 GB | 3       | 675   | 0     | 1.85   |
| Seagate   | 2E256-TU2-510B00   | 170 GB | 3       | 2072  | 1366  | 1.85   |
| Patriot   | Ignite             | 480 GB | 3       | 674   | 0     | 1.85   |
| Intel     | SSDSC2BA200G4      | 200 GB | 10      | 730   | 1     | 1.85   |
| Samsung   | SSD 850 EVO        | 1 TB   | 164     | 765   | 5     | 1.84   |
| Samsung   | MZHPV128HDGM-00000 | 128 GB | 4       | 671   | 0     | 1.84   |
| OCZ       | TRION150           | 480 GB | 11      | 668   | 0     | 1.83   |
| Mushkin   | MKNSSDCR240GB-7    | 240 GB | 1       | 666   | 0     | 1.83   |
| Apple     | SSD SD256E         | 256 GB | 1       | 666   | 0     | 1.83   |
| Samsung   | SSD 850 EVO M.2    | 500 GB | 46      | 666   | 0     | 1.83   |
| SanDisk   | SD6SB2M-512G-1006  | 512 GB | 5       | 665   | 0     | 1.82   |
| Samsung   | MZNLF128HCHP-00000 | 128 GB | 15      | 665   | 0     | 1.82   |
| Innodisk  | Corp. DRPS-02GJ... | 2 GB   | 3       | 664   | 0     | 1.82   |
| Transcend | TS128GMSA720       | 128 GB | 1       | 663   | 0     | 1.82   |
| Intel     | SSDSC2BP240G4      | 240 GB | 9       | 662   | 0     | 1.81   |
| ADATA     | SX930              | 240 GB | 1       | 661   | 0     | 1.81   |
| Smartbuy  | SSD                | 90 GB  | 2       | 661   | 0     | 1.81   |
| Intel     | SSDSA2CW160G3      | 160 GB | 10      | 661   | 0     | 1.81   |
| Samsung   | SSD 850 EVO        | 500 GB | 706     | 667   | 1     | 1.81   |
| SanDisk   | SD7SB3Q-128G-1006  | 128 GB | 5       | 655   | 0     | 1.80   |
| SanDisk   | SD7TB3Q-256G-1006  | 256 GB | 13      | 652   | 0     | 1.79   |
| Samsung   | SSD RBX Series ... | 64 GB  | 2       | 651   | 0     | 1.79   |
| Apple     | SSD SM1024G        | 1 TB   | 7       | 651   | 0     | 1.78   |
| ADATA     | SSD SX900 256GB... | 256 GB | 1       | 651   | 0     | 1.78   |
| Toshiba   | THNSNH256GCST      | 256 GB | 2       | 651   | 0     | 1.78   |
| Apple     | SSD SM0512F        | 500 GB | 22      | 650   | 0     | 1.78   |
| Toshiba   | THNSNJ128GMCU      | 128 GB | 9       | 649   | 0     | 1.78   |
| Kingston  | RBUSNS8280S3128GH2 | 128 GB | 5       | 649   | 0     | 1.78   |
| Samsung   | MZNLN512HCJH-000H1 | 512 GB | 6       | 649   | 0     | 1.78   |
| OCZ       | AGILITY3           | 120 GB | 73      | 840   | 77    | 1.78   |
| Kingston  | SKC400S37512G      | 512 GB | 9       | 648   | 0     | 1.78   |
| Samsung   | MZ7TY128HDHP-000L1 | 128 GB | 14      | 643   | 0     | 1.76   |
| Kingston  | SKC300S37A480G     | 480 GB | 2       | 643   | 0     | 1.76   |
| Toshiba   | Q300 Pro           | 128 GB | 3       | 641   | 0     | 1.76   |
| Intel     | SSDSC2CW480A3      | 480 GB | 6       | 640   | 0     | 1.76   |
| Corsair   | Force GS           | 128 GB | 24      | 640   | 0     | 1.75   |
| Samsung   | SSD PB22-JS3 FD... | 256 GB | 1       | 637   | 0     | 1.75   |
| Kingston  | SV100S232G         | 32 GB  | 5       | 635   | 0     | 1.74   |
| Intel     | SSDSC2CT180A3      | 180 GB | 16      | 730   | 1     | 1.74   |
| Samsung   | MZ7PD128HAFV-000H7 | 128 GB | 9       | 633   | 0     | 1.74   |
| Micron    | 1100 SATA          | 1 TB   | 1       | 632   | 0     | 1.73   |
| Toshiba   | THNSNF512GCSS      | 512 GB | 1       | 631   | 0     | 1.73   |
| Apacer    | AS330              | 240 GB | 1       | 629   | 0     | 1.73   |
| Samsung   | MZHPV256HDGL-00000 | 256 GB | 9       | 677   | 1     | 1.72   |
| SK hynix  | HFS120G32TND-N1A2A | 120 GB | 2       | 626   | 0     | 1.72   |
| OCZ       | VERTEX3            | 120 GB | 83      | 863   | 31    | 1.71   |
| Crucial   | CT1024MX200SSD1    | 1 TB   | 9       | 767   | 12    | 1.71   |
| Kingston  | SVP200S37A240G     | 240 GB | 1       | 623   | 0     | 1.71   |
| Samsung   | SSD 850 EVO        | 4 TB   | 5       | 622   | 0     | 1.71   |
| Samsung   | MZ7LN512HCHP-000H1 | 512 GB | 3       | 622   | 0     | 1.71   |
| SanDisk   | Ultra II           | 480 GB | 46      | 645   | 1     | 1.70   |
| SanDisk   | SD8SBBU240G1122    | 240 GB | 5       | 621   | 0     | 1.70   |
| Samsung   | SSD CM871 M.2 2280 | 128 GB | 4       | 621   | 0     | 1.70   |
| SanDisk   | SDSSDHP256G        | 256 GB | 36      | 636   | 1     | 1.70   |
| Toshiba   | TR150              | 960 GB | 3       | 620   | 0     | 1.70   |
| BlueRay   | SDM9SI128A         | 128 GB | 1       | 619   | 0     | 1.70   |
| SanDisk   | SDSSDP064G         | 64 GB  | 40      | 638   | 26    | 1.69   |
| Samsung   | MZMPA128HMFU-00000 | 128 GB | 1       | 616   | 0     | 1.69   |
| ZOTAC     | ZTSSD-A4P-120G     | 120 GB | 1       | 615   | 0     | 1.69   |
| Apple     | SSD SM256E         | 256 GB | 12      | 614   | 0     | 1.68   |
| Samsung   | SSD 850 EVO        | 120 GB | 153     | 614   | 0     | 1.68   |
| Hyundai   | SSD 240G           | 240 GB | 1       | 613   | 0     | 1.68   |
| OCZ       | VECTOR150          | 480 GB | 1       | 611   | 0     | 1.67   |
| SanDisk   | SDSSDHII480G       | 480 GB | 18      | 622   | 1     | 1.67   |
| SanDisk   | SD8SN8U256G1122    | 256 GB | 4       | 608   | 0     | 1.67   |
| Crucial   | CT240M500SSD4      | 240 GB | 1       | 608   | 0     | 1.67   |
| KingSpec  | ACSC2M064S25       | 64 GB  | 3       | 607   | 0     | 1.67   |
| Transcend | TS32GMTS400        | 32 GB  | 1       | 607   | 0     | 1.66   |
| Intel     | SSDSC2BW180A3L     | 180 GB | 19      | 613   | 1     | 1.66   |
| Micron    | M600_MTFDDAT128MBF | 128 GB | 2       | 604   | 0     | 1.66   |
| Samsung   | MZNTY128HDHP-000L2 | 128 GB | 2       | 604   | 0     | 1.66   |
| Samsung   | SSD SM871 2.5 7mm  | 256 GB | 8       | 631   | 1     | 1.65   |
| Samsung   | MZMTE256HMHP-00000 | 256 GB | 4       | 603   | 0     | 1.65   |
| Toshiba   | THNSNJ256GCST      | 256 GB | 4       | 603   | 0     | 1.65   |
| Transcend | TS64S37CA00IM3     | 64 GB  | 1       | 602   | 0     | 1.65   |
| Samsung   | MZ7TE256HMHP-000L7 | 256 GB | 26      | 642   | 15    | 1.65   |
| Kingston  | SHSS37A120G        | 120 GB | 15      | 601   | 0     | 1.65   |
| Apple     | SSD SM0256F        | 256 GB | 28      | 600   | 0     | 1.65   |
| Micron    | MTFDDAK1T0MBF-1... | 1 TB   | 2       | 600   | 0     | 1.64   |
| Patriot   | Blast              | 240 GB | 11      | 600   | 0     | 1.64   |
| Phison    | 64GB PS3109-S9     | 64 GB  | 1       | 599   | 0     | 1.64   |
| SK hynix  | HFS512G39MND-3510A | 512 GB | 5       | 598   | 0     | 1.64   |
| Corsair   | Force 3 SSD        | 480 GB | 1       | 598   | 0     | 1.64   |
| Samsung   | MZNTE256HMHP-000   | 256 GB | 1       | 598   | 0     | 1.64   |
| Samsung   | MZ7LN256HMJP-000H1 | 256 GB | 12      | 673   | 1     | 1.64   |
| ADATA     | XM11               | 256 GB | 1       | 598   | 0     | 1.64   |
| Corsair   | CSSD-V64GB2        | 64 GB  | 2       | 597   | 0     | 1.64   |
| Micron    | 5200_MTFDDAK1T9TDC | 1.9 TB | 13      | 636   | 1     | 1.64   |
| Palit     | PSP240 SSD         | 240 GB | 1       | 597   | 0     | 1.64   |
| Toshiba   | THNSFJ256GCSU      | 256 GB | 21      | 603   | 1     | 1.64   |
| Toshiba   | THNSFJ256GDNU A    | 256 GB | 8       | 596   | 0     | 1.64   |
| Apacer    | AS220              | 64 GB  | 1       | 596   | 0     | 1.63   |
| OCZ       | VERTEX2            | 115 GB | 5       | 595   | 0     | 1.63   |
| SanDisk   | PLUS               | 480 GB | 9       | 595   | 0     | 1.63   |
| Plextor   | PX-64M5S           | 64 GB  | 1       | 595   | 0     | 1.63   |
| Micron    | MTFDDAK512MBF-1... | 512 GB | 7       | 648   | 3     | 1.63   |
| Crucial   | CT500MX200SSD6     | 500 GB | 2       | 593   | 0     | 1.63   |
| Intel     | SSDSC2KB480G8R     | 480 GB | 1       | 593   | 0     | 1.62   |
| Patriot   | Blaze              | 240 GB | 5       | 592   | 0     | 1.62   |
| Intel     | SSDSCMMW180A3L     | 180 GB | 5       | 592   | 0     | 1.62   |
| Samsung   | MZ7TE512HMHP-000L2 | 512 GB | 5       | 591   | 0     | 1.62   |
| Samsung   | MZ7LN512HMJP-000L7 | 512 GB | 14      | 591   | 0     | 1.62   |
| SPCC      | SSD110             | 120 GB | 7       | 653   | 146   | 1.62   |
| OCZ       | VERTEX4            | 128 GB | 99      | 648   | 1     | 1.62   |
| Micron    | 5300_MTFDDAK1T9TDS | 1.9 TB | 1       | 589   | 0     | 1.61   |
| Samsung   | MZ7TD128HAFV-000L1 | 128 GB | 18      | 588   | 0     | 1.61   |
| PNY       | CS1311 480GB SSD   | 480 GB | 9       | 588   | 0     | 1.61   |
| Kingston  | RBU-SNS8100S3256GD | 256 GB | 6       | 587   | 0     | 1.61   |
| Samsung   | SSD 850 EVO        | 250 GB | 858     | 601   | 3     | 1.61   |
| Samsung   | MZ7TY256HDHP-000L1 | 256 GB | 2       | 585   | 0     | 1.60   |
| OCZ       | DENCSTE351M16-0... | 240 GB | 1       | 585   | 0     | 1.60   |
| Micron    | 5200_MTFDDAK480TDC | 480 GB | 6       | 584   | 0     | 1.60   |
| OCZ       | D2RSTK251E19-0200  | 200 GB | 1       | 584   | 0     | 1.60   |
| SanDisk   | SD6SN1M128G        | 128 GB | 1       | 584   | 0     | 1.60   |
| Intel     | SSDSC2BA400G4      | 400 GB | 4       | 584   | 0     | 1.60   |
| Micron    | MTFDDAV512TBN-1... | 512 GB | 2       | 739   | 1     | 1.60   |
| Samsung   | SSD PM871b 2.5 7mm | 256 GB | 9       | 583   | 0     | 1.60   |
| SanDisk   | Ultra II           | 960 GB | 35      | 618   | 1     | 1.60   |
| Samsung   | MZ7TD256HAFV-000L9 | 256 GB | 12      | 582   | 0     | 1.59   |
| Crucial   | CT250MX200SSD3     | 250 GB | 5       | 580   | 0     | 1.59   |
| Intel     | SSDSC2BA400G3      | 400 GB | 1       | 580   | 0     | 1.59   |
| ADATA     | SU650              | 960 GB | 4       | 579   | 0     | 1.59   |
| Kingston  | SKC400S37256G      | 256 GB | 10      | 578   | 0     | 1.58   |
| Galaxy    | GX0240ML103        | 240 GB | 1       | 578   | 0     | 1.58   |
| Samsung   | MZNTD256HAGL-000L9 | 256 GB | 3       | 577   | 0     | 1.58   |
| Toshiba   | Q300               | 480 GB | 12      | 576   | 0     | 1.58   |
| Samsung   | MZ7LN256HCHP-000H1 | 256 GB | 3       | 576   | 0     | 1.58   |
| SanDisk   | SSD U100           | 8 GB   | 2       | 575   | 0     | 1.58   |
| Samsung   | MZ7LM1T9HCJM-0E003 | 1.9 TB | 1       | 574   | 0     | 1.58   |
| Samsung   | SSD 850 EVO M.2    | 120 GB | 12      | 574   | 0     | 1.57   |
| SATADOM   | SL 3ME3 V2         | 128 GB | 1       | 574   | 0     | 1.57   |
| SanDisk   | SD9SB8W128G1001    | 128 GB | 5       | 572   | 0     | 1.57   |
| ADATA     | SSD S510           | 64 GB  | 3       | 572   | 0     | 1.57   |
| Samsung   | MZYLN256HCHP-000L2 | 256 GB | 1       | 571   | 0     | 1.57   |
| Intenso   | SATA3 512GB SSD    | 512 GB | 1       | 570   | 0     | 1.56   |
| Kingston  | SKC400S37128G      | 128 GB | 3       | 570   | 0     | 1.56   |
| OCZ       | VERTEX PLUS R2     | 128 GB | 4       | 569   | 0     | 1.56   |
| Intel     | SSDSC2CT080A4      | 80 GB  | 4       | 568   | 0     | 1.56   |
| Toshiba   | THNSNJ512GCSU      | 512 GB | 6       | 568   | 0     | 1.56   |
| OCZ       | AGILITY4           | 64 GB  | 1       | 567   | 0     | 1.56   |
| Kingston  | SMSM150S324G2      | 24 GB  | 5       | 567   | 0     | 1.55   |
| OCZ       | VECTOR             | 128 GB | 7       | 568   | 3     | 1.55   |
| OCZ       | VERTEX3            | 64 GB  | 37      | 613   | 1     | 1.55   |
| Apple     | SSD SM768E         | 752 GB | 3       | 566   | 0     | 1.55   |
| PNY       | SSD2SC480G1CS27... | 480 GB | 4       | 566   | 0     | 1.55   |
| Samsung   | MZ7KM480HMHQ0D3    | 480 GB | 6       | 565   | 0     | 1.55   |
| OCZ       | REVODRIVE3         | 64 GB  | 4       | 564   | 0     | 1.55   |
| Samsung   | SSD 750 EVO        | 250 GB | 100     | 565   | 1     | 1.54   |
| SanDisk   | SSD G5 BICS3       | 250 GB | 1       | 559   | 0     | 1.53   |
| Lite-On   | CV6-8Q128          | 128 GB | 3       | 559   | 0     | 1.53   |
| Kingston  | SMS200S360G        | 64 GB  | 19      | 793   | 54    | 1.53   |
| Toshiba   | TR150              | 120 GB | 11      | 558   | 0     | 1.53   |
| Patriot   | Torch LE           | 240 GB | 1       | 558   | 0     | 1.53   |
| Toshiba   | THNSNC128GAMJ      | 128 GB | 1       | 557   | 0     | 1.53   |
| Samsung   | MZMPC128HBFU-000H1 | 128 GB | 6       | 557   | 0     | 1.53   |
| OCZ       | VERTEX2 3.5        | 120 GB | 3       | 734   | 1     | 1.52   |
| Micron    | M600_MTFDDAY512MBF | 512 GB | 2       | 555   | 0     | 1.52   |
| Samsung   | SSD 850 PRO        | 2 TB   | 7       | 671   | 7     | 1.52   |
| SK hynix  | SC300 2.5 7MM      | 256 GB | 5       | 553   | 0     | 1.52   |
| WDC       | WDS500G1B0B-00AS40 | 500 GB | 9       | 553   | 0     | 1.52   |
| China     | ZSS11DA02C         | 512 GB | 2       | 551   | 0     | 1.51   |
| Intel     | SSDSC2BF180A5      | 180 GB | 3       | 1641  | 3     | 1.51   |
| SanDisk   | SDSSDP256G         | 256 GB | 15      | 579   | 2     | 1.51   |
| Toshiba   | THNSNC064GMMJ      | 64 GB  | 2       | 547   | 0     | 1.50   |
| SK hynix  | HFS512G32MND-3210A | 512 GB | 1       | 547   | 0     | 1.50   |
| Samsung   | MZ7PA128HMCD-010L1 | 128 GB | 5       | 633   | 189   | 1.50   |
| SanDisk   | SD8SB8U1T001122    | 1 TB   | 5       | 546   | 0     | 1.50   |
| Goodram   | SSD                | 240 GB | 23      | 546   | 0     | 1.50   |
| Biostar   | S100-240GB PLUS    | 240 GB | 1       | 545   | 0     | 1.50   |
| Kingston  | SH100S3240G        | 240 GB | 3       | 1181  | 2     | 1.49   |
| Plextor   | PX-512M7VC         | 512 GB | 2       | 544   | 0     | 1.49   |
| Micron    | M550_MTFDDAV128MAY | 128 GB | 1       | 543   | 0     | 1.49   |
| Hoodisk   | SSD                | 64 GB  | 4       | 543   | 0     | 1.49   |
| Hoodisk   | SSD                | 32 GB  | 1       | 542   | 0     | 1.49   |
| Lite-On   | PH4-8E256          | 256 GB | 1       | 542   | 0     | 1.49   |
| Kingston  | SH103S3240G        | 240 GB | 37      | 788   | 88    | 1.48   |
| OCZ       | AGILITY3           | 240 GB | 18      | 703   | 12    | 1.48   |
| OWC       | Mercury Electra... | 500 GB | 9       | 540   | 0     | 1.48   |
| SanDisk   | SD9SB8W128G1122    | 128 GB | 1       | 539   | 0     | 1.48   |
| Samsung   | SSD 850 EVO mSATA  | 1 TB   | 8       | 539   | 0     | 1.48   |
| Toshiba   | THNSNJ128G8NU      | 128 GB | 9       | 538   | 0     | 1.47   |
| Toshiba   | VT180              | 480 GB | 3       | 747   | 1     | 1.47   |
| Plextor   | PX-128M3           | 128 GB | 7       | 601   | 260   | 1.47   |
| Kingston  | SV300S37A60G       | 64 GB  | 185     | 577   | 1     | 1.47   |
| SanDisk   | SDSSDA480G         | 480 GB | 26      | 538   | 1     | 1.47   |
| Samsung   | SSD PM810 TH       | 64 GB  | 1       | 536   | 0     | 1.47   |
| Phison    | SM280128GPTC15T... | 128 GB | 1       | 535   | 0     | 1.47   |
| Samsung   | MZ7TD256HAFV-000L7 | 256 GB | 12      | 534   | 0     | 1.47   |
| SanDisk   | SDSSDXPS240G       | 240 GB | 23      | 701   | 55    | 1.46   |
| Micron    | M600_MTFDDAK256MBF | 256 GB | 2       | 533   | 0     | 1.46   |
| Toshiba   | THNSNC128GCSJ      | 128 GB | 3       | 532   | 0     | 1.46   |
| Intel     | SSDSC2KG240G8      | 240 GB | 16      | 532   | 0     | 1.46   |
| Crucial   | CT128M550SSD4      | 128 GB | 1       | 532   | 0     | 1.46   |
| Samsung   | MZMTD256HAGM-00004 | 256 GB | 1       | 529   | 0     | 1.45   |
| HP        | VK000240GWJPD      | 240 GB | 1       | 529   | 0     | 1.45   |
| Kingston  | SHSS37A240G        | 240 GB | 56      | 537   | 1     | 1.45   |
| Apple     | SSD SM512E         | 500 GB | 8       | 543   | 1     | 1.45   |
| Samsung   | MZ7LF128HCHP-000L1 | 128 GB | 2       | 528   | 0     | 1.45   |
| Samsung   | SSD 650            | 120 GB | 10      | 528   | 0     | 1.45   |
| SanDisk   | SD6SB2M128G1022I   | 128 GB | 2       | 528   | 0     | 1.45   |
| Samsung   | SSD 850 EVO M.2    | 250 GB | 42      | 525   | 0     | 1.44   |
| Intel     | SSDSC2KB960G8      | 960 GB | 35      | 549   | 1     | 1.44   |
| GALAX     | GXTA1B0120A        | 120 GB | 2       | 525   | 0     | 1.44   |
| SanDisk   | SD6SP1M128G1002    | 128 GB | 3       | 524   | 0     | 1.44   |
| SK hynix  | HFS512G39MND-3310A | 512 GB | 2       | 524   | 0     | 1.44   |
| Kingston  | SV200S364G         | 64 GB  | 8       | 552   | 1     | 1.43   |
| Samsung   | MZ7LF128HCHP-00004 | 128 GB | 3       | 522   | 0     | 1.43   |
| Samsung   | MZ7PC128HAFU-000   | 128 GB | 3       | 521   | 0     | 1.43   |
| Neo Forza | NFS011SA328-600... | 128 GB | 1       | 521   | 0     | 1.43   |
| Samsung   | MZRPA256HMDR-000SO | 128 GB | 2       | 520   | 0     | 1.43   |
| SanDisk   | SD9TB8W512G1001    | 512 GB | 5       | 520   | 0     | 1.43   |
| Micron    | MTFDDAV512TBN-1... | 512 GB | 1       | 519   | 0     | 1.42   |
| Goodram   | SSDPR-CX300-480    | 480 GB | 1       | 518   | 0     | 1.42   |
| Intenso   | SSD Sata III       | 480 GB | 2       | 518   | 0     | 1.42   |
| Apple     | SSD SD512E         | 500 GB | 4       | 517   | 0     | 1.42   |
| Toshiba   | THNSNJ128GCSU      | 128 GB | 19      | 517   | 0     | 1.42   |
| Toshiba   | THNSNJ256GMCY      | 256 GB | 1       | 515   | 0     | 1.41   |
| Micron    | M500DC_MTFDDAK2... | 240 GB | 1       | 515   | 0     | 1.41   |
| Crucial   | CT256MX100SSD1     | 256 GB | 76      | 560   | 7     | 1.41   |
| Team      | L3 EVO SSD         | 120 GB | 7       | 514   | 0     | 1.41   |
| SanDisk   | SD8SB8U512G1122    | 512 GB | 10      | 514   | 0     | 1.41   |
| Intel     | SSDSA2BW120G3H     | 120 GB | 5       | 544   | 1     | 1.41   |
| KingFast  | SSD                | 32 GB  | 1       | 513   | 0     | 1.41   |
| ADATA     | SSD S599           | 115 GB | 1       | 512   | 0     | 1.41   |
| Transcend | TS256GMTS600       | 256 GB | 2       | 512   | 0     | 1.40   |
| Samsung   | SSD PM830 mSATA    | 32 GB  | 20      | 511   | 0     | 1.40   |
| Samsung   | MZMTE128HMGR-00007 | 128 GB | 1       | 511   | 0     | 1.40   |
| Goodram   | SSDPR-CX300-960    | 960 GB | 1       | 509   | 0     | 1.40   |
| WDC       | WDS250G1B0B-00AS40 | 250 GB | 10      | 508   | 0     | 1.39   |
| WDC       | WDS200T2B0A        | 2 TB   | 3       | 507   | 0     | 1.39   |
| Intel     | SSDSC2BX480G4      | 480 GB | 1       | 506   | 0     | 1.39   |
| SanDisk   | SSD U110           | 32 GB  | 2       | 505   | 0     | 1.39   |
| SanDisk   | SDSSDH2128G        | 128 GB | 4       | 505   | 0     | 1.38   |
| Corsair   | Force GS           | 240 GB | 7       | 1232  | 18    | 1.38   |
| Intel     | SSDSC2CT240A4      | 240 GB | 16      | 785   | 2     | 1.38   |
| Palit     | UVS                | 240 GB | 2       | 503   | 0     | 1.38   |
| Verbatim  | SATA-III SSD       | 256 GB | 1       | 503   | 0     | 1.38   |
| OCZ       | VERTEX3 MI         | 120 GB | 23      | 782   | 132   | 1.38   |
| Samsung   | MZ7WD960HMHP-00003 | 960 GB | 6       | 846   | 3     | 1.38   |
| OCZ       | D2RSTK251E14-0400  | 400 GB | 1       | 502   | 0     | 1.38   |
| Micron    | MTFDDAK128MAM-1J1  | 128 GB | 26      | 500   | 0     | 1.37   |
| Kingston  | RBU-SNS8152S3128GF | 128 GB | 2       | 498   | 0     | 1.37   |
| Corsair   | Force GT           | 90 GB  | 4       | 610   | 1     | 1.36   |
| Crucial   | CT240M500SSD3      | 240 GB | 7       | 541   | 5     | 1.36   |
| Toshiba   | Q300               | 240 GB | 15      | 635   | 2     | 1.36   |
| Samsung   | MZ7TE128HMGR-000L1 | 128 GB | 13      | 495   | 0     | 1.36   |
| OCZ       | VERTEX460A         | 240 GB | 3       | 494   | 0     | 1.35   |
| Patriot   | Flare              | 64 GB  | 6       | 493   | 0     | 1.35   |
| ADROIT... | SSD                | 48 GB  | 1       | 493   | 0     | 1.35   |
| SanDisk   | SD7SB6S-256G-1006  | 256 GB | 8       | 492   | 0     | 1.35   |
| Samsung   | MZ7TE128HMGR-00004 | 128 GB | 7       | 492   | 0     | 1.35   |
| Toshiba   | FujiFilm           | 128 GB | 1       | 492   | 0     | 1.35   |
| SanDisk   | SD6SB1M128G1022I   | 128 GB | 7       | 491   | 0     | 1.35   |
| KingFast  | SSD                | 32 GB  | 1       | 490   | 0     | 1.34   |
| Mushkin   | MKNSSDCR240GB      | 240 GB | 4       | 1034  | 522   | 1.34   |
| Transcend | TS64GSSD320        | 64 GB  | 3       | 487   | 0     | 1.34   |
| Toshiba   | THNSFC128GBSJ      | 128 GB | 2       | 486   | 0     | 1.33   |
| OCZ       | ARC100             | 240 GB | 20      | 508   | 1     | 1.33   |
| Samsung   | SSD PM810 2.5" 7mm | 128 GB | 9       | 644   | 126   | 1.33   |
| Kingston  | SKC400S371T        | 1 TB   | 2       | 1172  | 25    | 1.33   |
| Samsung   | SSD CM871 2.5 7mm  | 128 GB | 4       | 484   | 0     | 1.33   |
| Kingston  | SVP200S37A60G      | 64 GB  | 15      | 558   | 3     | 1.33   |
| Lite-On   | LCM-256M3S         | 256 GB | 1       | 484   | 0     | 1.33   |
| Samsung   | SSD 850 EVO mSATA  | 500 GB | 27      | 484   | 0     | 1.33   |
| China     | ESA3SMH2MSM1BT1... | 120 GB | 1       | 483   | 0     | 1.32   |
| Intel     | SSDSA2BW120G3A     | 120 GB | 2       | 482   | 0     | 1.32   |
| Goodram   | SSD                | 64 GB  | 1       | 480   | 0     | 1.32   |
| TAISU     | SSD                | 120 GB | 1       | 480   | 0     | 1.32   |
| OCZ       | VERTEX3            | 240 GB | 16      | 860   | 85    | 1.32   |
| Samsung   | MZNLF128HCHP-00004 | 128 GB | 13      | 479   | 0     | 1.31   |
| Toshiba   | TR150              | 480 GB | 10      | 540   | 1     | 1.31   |
| Toshiba   | Q300 Pro           | 256 GB | 2       | 478   | 0     | 1.31   |
| GLOWAY    | FER240GS3-S7       | 240 GB | 2       | 510   | 506   | 1.31   |
| Goodram   | SSDPR_CX300_120    | 120 GB | 4       | 476   | 0     | 1.30   |
| Kingston  | SHSS37A480G        | 480 GB | 14      | 475   | 0     | 1.30   |
| Samsung   | SG9MSM6D024GPM00   | 22 GB  | 6       | 598   | 2     | 1.30   |
| Apple     | SSD SM0512G        | 500 GB | 23      | 474   | 0     | 1.30   |
| SanDisk   | SD8SBBU480G1122    | 480 GB | 3       | 473   | 0     | 1.30   |
| Corsair   | Force 3 SSD        | 90 GB  | 7       | 473   | 0     | 1.30   |
| Toshiba   | THNSNH128GCST      | 128 GB | 10      | 491   | 1     | 1.30   |
| SanDisk   | SDSSDH240GG25      | 240 GB | 1       | 473   | 0     | 1.30   |
| Micron    | 5200_MTFDDAK240TDN | 240 GB | 10      | 472   | 0     | 1.30   |
| OCZ       | AGILITY2           | 64 GB  | 3       | 472   | 0     | 1.29   |
| Yunhai... | Y6-120G            | 120 GB | 1       | 472   | 0     | 1.29   |
| addlink   | SATA SSD           | 256 GB | 3       | 471   | 0     | 1.29   |
| SanDisk   | SD8SB8U-256G-1006  | 256 GB | 9       | 469   | 0     | 1.29   |
| ADATA     | XM11 256GB-V2      | 256 GB | 4       | 1108  | 254   | 1.29   |
| Samsung   | MZNLF128HCHP-000H1 | 128 GB | 8       | 468   | 0     | 1.28   |
| Samsung   | MZMPC032HBCD-00000 | 32 GB  | 16      | 489   | 64    | 1.28   |
| Toshiba   | THNSNH060GCST      | 64 GB  | 1       | 467   | 0     | 1.28   |
| Lite-On   | PH4-CE120          | 120 GB | 2       | 467   | 0     | 1.28   |
| Plextor   | PX-64M2S           | 64 GB  | 2       | 467   | 0     | 1.28   |
| Kingston  | SM2280S3G2240G     | 240 GB | 7       | 467   | 0     | 1.28   |
| Lite-On   | LCH-256V2S-HP      | 256 GB | 2       | 465   | 0     | 1.28   |
| ADATA     | SP900              | 64 GB  | 26      | 522   | 4     | 1.28   |
| Patriot   | Spark              | 256 GB | 3       | 465   | 0     | 1.28   |
| Indilinx  | IND-S3MP-128G      | 128 GB | 1       | 465   | 0     | 1.27   |
| HP        | SSD M700           | 240 GB | 2       | 465   | 0     | 1.27   |
| Mushkin   | MKNSSDTR128GB-3DL  | 128 GB | 1       | 464   | 0     | 1.27   |
| Intel     | SSDSC2CT120A3      | 120 GB | 27      | 768   | 1     | 1.27   |
| FORESEE   | 60GB SSD           | 64 GB  | 1       | 463   | 0     | 1.27   |
| Plextor   | PX-256M7VC         | 256 GB | 5       | 462   | 0     | 1.27   |
| Samsung   | Portable SSD T3    | 2 TB   | 1       | 462   | 0     | 1.27   |
| Samsung   | MZ7TE256HMHP-000L2 | 256 GB | 4       | 462   | 0     | 1.27   |
| Kingston  | SM2280S3240G       | 240 GB | 2       | 462   | 0     | 1.27   |
| OCZ       | TRION150           | 240 GB | 9       | 462   | 0     | 1.27   |
| Samsung   | MZ7TD256HAFV-00000 | 256 GB | 1       | 458   | 0     | 1.26   |
| ADATA     | SX950              | 240 GB | 3       | 458   | 0     | 1.26   |
| Kingston  | SM2280S3G2120G     | 120 GB | 13      | 458   | 0     | 1.26   |
| Samsung   | MZ7LN512HCHP-000L1 | 512 GB | 14      | 458   | 0     | 1.26   |
| Samsung   | MZ7LN256HCHP-00000 | 256 GB | 6       | 458   | 0     | 1.26   |
| Plextor   | PX-512M5Pro        | 512 GB | 3       | 457   | 0     | 1.25   |
| OWC       | Mercury Electra... | 480 GB | 9       | 538   | 1     | 1.25   |
| Mushkin   | MKNSSDEC240GB      | 240 GB | 3       | 456   | 0     | 1.25   |
| SanDisk   | SD9SN8W1T001122    | 1 TB   | 1       | 456   | 0     | 1.25   |
| SK hynix  | SC300 M.2 2280     | 256 GB | 7       | 456   | 0     | 1.25   |
| Plextor   | PX-256S3C          | 256 GB | 3       | 456   | 0     | 1.25   |
| Intel     | SSDMCEAC240B3      | 240 GB | 3       | 456   | 0     | 1.25   |
| XSTAR     | SSD                | 120 GB | 1       | 455   | 0     | 1.25   |
| Intel     | SSDSC2KB480G8      | 480 GB | 9       | 455   | 0     | 1.25   |
| SanDisk   | Ultra II           | 240 GB | 39      | 469   | 1     | 1.25   |
| Plextor   | PX-256M3P          | 256 GB | 1       | 1360  | 2     | 1.24   |
| Transcend | TS128GSSD340       | 128 GB | 10      | 452   | 0     | 1.24   |
| Toshiba   | TL100              | 240 GB | 13      | 452   | 0     | 1.24   |
| Samsung   | MZ7PC256HAFU-000H1 | 256 GB | 1       | 452   | 0     | 1.24   |
| Kingston  | RBU-SC100S37256GD  | 256 GB | 2       | 450   | 0     | 1.24   |
| Micron    | C400-MTFDDAC256MAM | 256 GB | 2       | 450   | 0     | 1.23   |
| MyDigi... | SC2 M2 SSD         | 120 GB | 2       | 449   | 0     | 1.23   |
| Samsung   | SSD 850 EVO mSATA  | 120 GB | 6       | 448   | 0     | 1.23   |
| Kingston  | SMS100S264G        | 64 GB  | 5       | 463   | 2     | 1.23   |
| Samsung   | MZ7LM480HCHP-00... | 480 GB | 2       | 447   | 0     | 1.23   |
| WDC       | WDS250G1B0A-00H9H0 | 250 GB | 30      | 477   | 34    | 1.23   |
| Crucial   | CT960M500SSD1      | 960 GB | 14      | 762   | 80    | 1.22   |
| Micron    | M600_MTFDDAK128... | 128 GB | 1       | 445   | 0     | 1.22   |
| Foxline   | FLDMMS128G         | 128 GB | 1       | 443   | 0     | 1.22   |
| Toshiba   | THNSNJ128G8NY      | 128 GB | 7       | 443   | 0     | 1.21   |
| Intel     | SSDSC2BW180A3D     | 180 GB | 1       | 443   | 0     | 1.21   |
| WDC       | WDS100T1B0A-00H9H0 | 1 TB   | 18      | 442   | 0     | 1.21   |
| SanDisk   | SD9TB8W1T001001    | 1 TB   | 4       | 442   | 0     | 1.21   |
| Transcend | TS128GSSD720       | 128 GB | 4       | 442   | 0     | 1.21   |
| Samsung   | MZNTN512HDJH-00007 | 512 GB | 1       | 442   | 0     | 1.21   |
| SanDisk   | SSD PLUS 480G      | 480 GB | 1       | 440   | 0     | 1.21   |
| KingFast  | SSD                | 32 GB  | 2       | 440   | 0     | 1.21   |
| Samsung   | MZ7LN512HMJP-00000 | 512 GB | 5       | 439   | 0     | 1.21   |
| Samsung   | MZHPV512HDGL-000H1 | 512 GB | 1       | 439   | 0     | 1.20   |
| SanDisk   | SD8TB8U256G1001    | 256 GB | 20      | 439   | 0     | 1.20   |
| SanDisk   | SDSSDHII120G       | 120 GB | 43      | 439   | 0     | 1.20   |
| OCZ       | VECTOR180          | 240 GB | 3       | 438   | 0     | 1.20   |
| OCZ       | VERTEX3 MI         | 240 GB | 3       | 1419  | 44    | 1.20   |
| OCZ       | TRION100           | 240 GB | 22      | 452   | 1     | 1.20   |
| Samsung   | SSD 750 EVO        | 120 GB | 55      | 437   | 0     | 1.20   |
| OCZ       | VECTOR150          | 120 GB | 12      | 482   | 3     | 1.20   |
| Pioneer   | APS-SL3N-1T        | 1 TB   | 2       | 436   | 0     | 1.20   |
| Drevo     | X1 pro             | 1 TB   | 2       | 451   | 9     | 1.19   |
| OCZ       | REVODRIVE X2       | 25 GB  | 4       | 435   | 0     | 1.19   |
| Crucial   | CT240M500SSD1      | 240 GB | 63      | 700   | 89    | 1.19   |
| SanDisk   | SDSSDHP128G        | 128 GB | 45      | 458   | 23    | 1.19   |
| SanDisk   | SD6SB1M-256G-1006  | 256 GB | 3       | 433   | 0     | 1.19   |
| SanDisk   | SDSSDA960G         | 960 GB | 8       | 433   | 0     | 1.19   |
| Phison    | SSDS30256XQC800... | 240 GB | 1       | 433   | 0     | 1.19   |
| Intel     | SSDSC2BB012T7O     | 1.2 TB | 1       | 432   | 0     | 1.19   |
| Patriot   | Blast              | 120 GB | 13      | 432   | 0     | 1.19   |
| SanDisk   | SD6SB1M-128G-1006  | 128 GB | 9       | 444   | 1     | 1.19   |
| Samsung   | MZNLN256HCHP-00000 | 256 GB | 11      | 432   | 0     | 1.18   |
| PNY       | SSD2SC240G3SA75... | 240 GB | 1       | 432   | 0     | 1.18   |
| Apple     | SSD TS128A         | 121 GB | 1       | 431   | 0     | 1.18   |
| Samsung   | MZ7TD128HAFV-00000 | 128 GB | 6       | 431   | 0     | 1.18   |
| OCZ       | VERTEX4            | 64 GB  | 10      | 475   | 1     | 1.18   |
| Intel     | SSDSA2M080G2GC     | 80 GB  | 26      | 1086  | 5     | 1.18   |
| ADATA     | SSD S511           | 120 GB | 1       | 430   | 0     | 1.18   |
| Kingston  | SMS200S330G        | 32 GB  | 3       | 544   | 7     | 1.18   |
| Crucial   | CT120BX300SSD1     | 120 GB | 19      | 430   | 0     | 1.18   |
| Toshiba   | THNSNF256GMCS      | 256 GB | 6       | 430   | 0     | 1.18   |
| Micron    | MTFDDAK2T0TBN-1... | 2 TB   | 1       | 430   | 0     | 1.18   |
| Samsung   | MZ7LN512HAJQ-00000 | 512 GB | 8       | 429   | 0     | 1.18   |
| Samsung   | MZMPC032HBCD-000H1 | 32 GB  | 15      | 429   | 0     | 1.18   |
| Seagate   | ST120HM000-1G5142  | 120 GB | 2       | 429   | 0     | 1.18   |
| Samsung   | SMART SSD Xceed... | 32 GB  | 3       | 429   | 0     | 1.18   |
| Toshiba   | Q300 Pro           | 512 GB | 2       | 429   | 0     | 1.18   |
| Apple     | SSD TS128C         | 121 GB | 7       | 506   | 1     | 1.17   |
| SanDisk   | SD7TB6S256G1001    | 256 GB | 7       | 428   | 0     | 1.17   |
| Toshiba   | VX500              | 256 GB | 1       | 428   | 0     | 1.17   |
| ADATA     | SSD S396           | 32 GB  | 2       | 427   | 0     | 1.17   |
| SanDisk   | SD6SF1M064G        | 64 GB  | 4       | 427   | 0     | 1.17   |
| Samsung   | MZ7TY256HDHP-00000 | 256 GB | 7       | 426   | 0     | 1.17   |
| ADATA     | AXM13S2-24GM-B     | 24 GB  | 2       | 740   | 510   | 1.17   |
| Toshiba   | THNSNX032GMCT      | 32 GB  | 2       | 425   | 0     | 1.17   |
| SanDisk   | SD8SN8U-512G-1006  | 512 GB | 8       | 557   | 1     | 1.16   |
| Samsung   | MZ7PA128HMCD-010H1 | 128 GB | 3       | 706   | 339   | 1.16   |
| Transcend | TS64GSSD340        | 64 GB  | 5       | 470   | 202   | 1.16   |
| Transcend | TS480GJDM725       | 480 GB | 1       | 424   | 0     | 1.16   |
| SanDisk   | SDSSDP128G         | 128 GB | 75      | 450   | 4     | 1.16   |
| Toshiba   | THNSNJ256GVNU      | 256 GB | 2       | 423   | 0     | 1.16   |
| OCZ       | ONYX               | 32 GB  | 3       | 443   | 1     | 1.16   |
| Axiom     | Signature III S... | 64 GB  | 1       | 422   | 0     | 1.16   |
| Goodram   | C100               | 120 GB | 6       | 422   | 0     | 1.16   |
| Crucial   | CT750MX300SSD1     | 752 GB | 21      | 428   | 1     | 1.16   |
| Samsung   | MZ7LN256HCHP-000L7 | 256 GB | 34      | 422   | 0     | 1.16   |
| Samsung   | MZ7LM480HCHP-00... | 480 GB | 2       | 421   | 0     | 1.15   |
| SanDisk   | SD6SB1M256G1022I   | 256 GB | 5       | 501   | 95    | 1.15   |
| SK hynix  | SC308 SATA         | 512 GB | 7       | 535   | 122   | 1.15   |
| Kingston  | RBU-SNS8100S3128GD | 128 GB | 2       | 613   | 23    | 1.15   |
| SK hynix  | SC300 mSATA        | 512 GB | 2       | 420   | 0     | 1.15   |
| Hajaan    | SSD 256G           | 256 GB | 2       | 420   | 0     | 1.15   |
| Kingston  | SKC380S360G        | 64 GB  | 1       | 420   | 0     | 1.15   |
| Samsung   | SSD 850 EVO mSATA  | 250 GB | 21      | 419   | 0     | 1.15   |
| Toshiba   | THNSNF128GCSS      | 128 GB | 11      | 505   | 1     | 1.15   |
| Samsung   | SSD 860 EVO        | 4 TB   | 39      | 417   | 0     | 1.15   |
| SanDisk   | SDSSDXPS480G       | 480 GB | 14      | 640   | 40    | 1.14   |
| Samsung   | MZ7LF192HCGS-000L1 | 192 GB | 17      | 417   | 0     | 1.14   |
| OCZ       | VERTEX2            | 80 GB  | 3       | 417   | 0     | 1.14   |
| SanDisk   | SDSSDH2256G        | 256 GB | 2       | 417   | 0     | 1.14   |
| PNY       | SSD2SC480G1CS27... | 480 GB | 1       | 415   | 0     | 1.14   |
| Kingston  | SUV400S37960G      | 960 GB | 1       | 415   | 0     | 1.14   |
| Intel     | SSDSC2MH120A2      | 120 GB | 5       | 415   | 0     | 1.14   |
| Kingston  | SM2280S3G2480G     | 480 GB | 5       | 472   | 26    | 1.14   |
| Plextor   | PH6-CE480-L2       | 480 GB | 2       | 414   | 0     | 1.14   |
| Micron    | 5100_MTFDDAK1T9TBY | 1.9 TB | 4       | 907   | 84    | 1.14   |
| Toshiba   | THNSNF128GMCS      | 128 GB | 9       | 414   | 0     | 1.13   |
| SanDisk   | SD6SF1M256G1022    | 256 GB | 2       | 413   | 0     | 1.13   |
| Team      | L3 SSD             | 120 GB | 4       | 413   | 0     | 1.13   |
| Hoodisk   | SSD                | 16 GB  | 2       | 412   | 0     | 1.13   |
| SK hynix  | SC300 SATA         | 512 GB | 2       | 411   | 0     | 1.13   |
| SanDisk   | SD8SN8U512G1122    | 512 GB | 5       | 411   | 0     | 1.13   |
| SanDisk   | SDSSDH31000G       | 1 TB   | 23      | 410   | 0     | 1.13   |
| SanDisk   | Ultra II           | 250 GB | 4       | 410   | 0     | 1.12   |
| Kingston  | SM2280S3120G       | 120 GB | 7       | 410   | 0     | 1.12   |
| Kingston  | RBUSMS180DS3128GH  | 128 GB | 2       | 410   | 0     | 1.12   |
| Samsung   | MZ7TE256HMHP-000H1 | 256 GB | 7       | 409   | 0     | 1.12   |
| Toshiba   | THNSNJ256GCSU      | 256 GB | 11      | 409   | 0     | 1.12   |
| Toshiba   | THNSNJ128GCST      | 128 GB | 4       | 409   | 0     | 1.12   |
| Samsung   | MZMPC256HBGJ-000   | 256 GB | 1       | 409   | 0     | 1.12   |
| Kingston  | SV300S37A120G      | 120 GB | 731     | 520   | 19    | 1.12   |
| Goodram   | SSD                | 480 GB | 2       | 408   | 0     | 1.12   |
| HP        | SSD M700           | 120 GB | 4       | 408   | 0     | 1.12   |
| Samsung   | MZMTE512HMHP-000L1 | 512 GB | 2       | 408   | 0     | 1.12   |
| Samsung   | MZNLN256HMHQ-00000 | 256 GB | 11      | 407   | 0     | 1.12   |
| Phison    | S10C-512G-PHISO... | 512 GB | 1       | 406   | 0     | 1.11   |
| BIOSTAR   | S100-240GB         | 240 GB | 2       | 406   | 0     | 1.11   |
| China     | SH00R480GB         | 480 GB | 6       | 406   | 0     | 1.11   |
| Samsung   | MZHPV256HDGL-000L1 | 256 GB | 3       | 406   | 0     | 1.11   |
| Samsung   | MZNLN256HCHP-000L7 | 256 GB | 22      | 405   | 0     | 1.11   |
| Samsung   | MZNTY256HDHP-000H1 | 256 GB | 9       | 420   | 1     | 1.11   |
| Apple     | SSD SM0256G        | 256 GB | 43      | 405   | 0     | 1.11   |
| Kingston  | SVP200S3240G       | 240 GB | 3       | 404   | 0     | 1.11   |
| Kingston  | SMS200S3120G       | 120 GB | 31      | 436   | 26    | 1.11   |
| Samsung   | MZNLN512HMJP-000H1 | 512 GB | 7       | 403   | 0     | 1.11   |
| KingFast  | SSD                | 64 GB  | 6       | 403   | 1     | 1.11   |
| Intenso   | SSD Sata III       | 960 GB | 2       | 402   | 0     | 1.10   |
| Samsung   | MZMPC032HBCD-000L1 | 32 GB  | 6       | 402   | 0     | 1.10   |
| SanDisk   | SD7SB3Q-256G-1006  | 256 GB | 6       | 402   | 0     | 1.10   |
| SPCC      | 2.5" SSD           | 1 TB   | 1       | 402   | 0     | 1.10   |
| Samsung   | MZ7GE240HMGR-00003 | 240 GB | 3       | 401   | 0     | 1.10   |
| Micron    | C400-MTFDDAT128MAM | 128 GB | 2       | 439   | 1034  | 1.10   |
| Intel     | SSDSC2CW120A3      | 120 GB | 58      | 726   | 368   | 1.10   |
| ADATA     | SU635              | 960 GB | 1       | 400   | 0     | 1.10   |
| Crucial   | CT500MX200SSD1     | 500 GB | 33      | 418   | 1     | 1.10   |
| Crucial   | CT120M500SSD1      | 120 GB | 46      | 737   | 58    | 1.10   |
| Toshiba   | THNSNH060GBST      | 64 GB  | 2       | 400   | 0     | 1.10   |
| Crucial   | CT1050MX300SSD4    | 1 TB   | 11      | 490   | 7     | 1.09   |
| ADATA     | SP920SS            | 256 GB | 11      | 543   | 5     | 1.09   |
| OCZ       | VERTEX3            | 90 GB  | 12      | 690   | 7     | 1.09   |
| Samsung   | SSD PB22-JS3 2.5"  | 128 GB | 1       | 399   | 0     | 1.09   |
| Toshiba   | THNSNB128GMCJ      | 128 GB | 3       | 399   | 0     | 1.09   |
| Samsung   | MZMTE256HMHP-000MV | 256 GB | 13      | 398   | 0     | 1.09   |
| Mushkin   | MKNSSDTR480GB-3DL  | 480 GB | 1       | 398   | 0     | 1.09   |
| WDC       | WDBNCE5000PNC-WRSN | 500 GB | 2       | 398   | 0     | 1.09   |
| Samsung   | MZ7LN128HCHP-000L1 | 128 GB | 7       | 398   | 0     | 1.09   |
| PNY       | CS1311 120GB SSD   | 120 GB | 7       | 398   | 0     | 1.09   |
| Kingston  | RBU-SMS151S3128GG  | 128 GB | 1       | 398   | 0     | 1.09   |
| Micron    | 1100_MTFDDAK2T0TBN | 2 TB   | 6       | 397   | 0     | 1.09   |
| Samsung   | MZ7TY256HDHP-000L7 | 256 GB | 20      | 397   | 0     | 1.09   |
| Samsung   | MZMPC128HBFU-00000 | 128 GB | 6       | 397   | 0     | 1.09   |
| OCZ       | SOLID3             | 120 GB | 2       | 397   | 0     | 1.09   |
| Toshiba   | TR150              | 240 GB | 31      | 395   | 0     | 1.08   |
| SPCC      | SSD110             | 64 GB  | 5       | 595   | 4     | 1.08   |
| Samsung   | MZ7LN256HAJQ-00000 | 256 GB | 2       | 395   | 0     | 1.08   |
| OCZ       | VERTEX2            | 180 GB | 5       | 395   | 0     | 1.08   |
| Kingston  | SV200S3128G        | 128 GB | 12      | 600   | 2     | 1.08   |
| Intel     | SSDSC2BW180A4      | 180 GB | 13      | 628   | 4     | 1.08   |
| Samsung   | SSD PM830 2.5" 7mm | 512 GB | 3       | 597   | 337   | 1.08   |
| Intel     | SSDSC2CT180A4      | 180 GB | 11      | 618   | 1     | 1.08   |
| Samsung   | MZ7TE256HMHP-00004 | 256 GB | 2       | 392   | 0     | 1.07   |
| SanDisk   | SD5SG2128G1052E    | 128 GB | 5       | 391   | 0     | 1.07   |
| SanDisk   | SD7TB3Q-128G-1006  | 128 GB | 4       | 414   | 8     | 1.07   |
| Hikvision | HKVSN HS-SSD-C1... | 240 GB | 1       | 391   | 0     | 1.07   |
| Samsung   | MZNLN512HMJP-00000 | 512 GB | 1       | 391   | 0     | 1.07   |
| SanDisk   | SDSSDHII240G       | 240 GB | 45      | 401   | 1     | 1.07   |
| SanDisk   | SD7SB6S-128G-1006  | 128 GB | 4       | 538   | 1     | 1.07   |
| ZOTAC     | ZTSSD-S11-240G-P   | 240 GB | 1       | 389   | 0     | 1.07   |
| KingShare | M300128G           | 128 GB | 1       | 389   | 0     | 1.07   |
| OCZ       | AGILITY3           | 128 GB | 3       | 749   | 1     | 1.07   |
| Micron    | M600_MTFDDAV128MBF | 128 GB | 4       | 388   | 0     | 1.07   |
| Toshiba   | VX500              | 128 GB | 1       | 387   | 0     | 1.06   |
| Samsung   | MZYTY256HDHP-000L2 | 256 GB | 10      | 387   | 0     | 1.06   |
| ADATA     | SSD SP900 256GB... | 256 GB | 2       | 387   | 0     | 1.06   |
| SanDisk   | SDSSDXP240G        | 240 GB | 11      | 498   | 2     | 1.06   |
| Samsung   | SSD PM830 mSATA    | 128 GB | 4       | 387   | 0     | 1.06   |
| Kingston  | SNV425S2128GB      | 128 GB | 3       | 863   | 3     | 1.06   |
| Patriot   | Pyro SSD           | 120 GB | 2       | 386   | 0     | 1.06   |
| DIERYA    | SSD                | 120 GB | 1       | 385   | 0     | 1.06   |
| SanDisk   | SD8SB8U256G1122    | 256 GB | 9       | 384   | 0     | 1.05   |
| ADATA     | SP900              | 128 GB | 53      | 451   | 8     | 1.05   |
| Samsung   | MMCRE28GFMXP-MVB   | 128 GB | 2       | 383   | 0     | 1.05   |
| Samsung   | MZ7LH960HAJR-00005 | 960 GB | 3       | 383   | 0     | 1.05   |
| Apacer    | AST680S            | 128 GB | 3       | 383   | 0     | 1.05   |
| Smartbuy  | SSD                | 64 GB  | 8       | 382   | 0     | 1.05   |
| SanDisk   | SDSSDH31024G       | 1 TB   | 18      | 382   | 0     | 1.05   |
| Intel     | SSDSC2BW180A3      | 180 GB | 1       | 382   | 0     | 1.05   |
| FCS       | SSD                | 240 GB | 1       | 381   | 0     | 1.05   |
| Samsung   | SSD PM800 TM       | 64 GB  | 3       | 381   | 0     | 1.05   |
| Palit     | PSP120 SSD         | 120 GB | 3       | 381   | 0     | 1.05   |
| Samsung   | SSD 860 EVO mSATA  | 500 GB | 20      | 381   | 0     | 1.05   |
| Samsung   | MZNLN512HCJH-000L1 | 512 GB | 11      | 381   | 0     | 1.04   |
| Intel     | SSDSC2BB480G6      | 480 GB | 1       | 381   | 0     | 1.04   |
| Intel     | SSDSCIHF120A4H     | 120 GB | 2       | 381   | 0     | 1.04   |
| Toshiba   | THNSNJ256G8NY      | 256 GB | 12      | 401   | 1     | 1.04   |
| SanDisk   | Ultra II           | 500 GB | 3       | 380   | 0     | 1.04   |
| SanDisk   | SDSSDH120GG25      | 120 GB | 2       | 435   | 28    | 1.04   |
| Crucial   | CT128M550SSD3      | 128 GB | 6       | 474   | 8     | 1.04   |
| Kingston  | RBU-SC152S37256GG2 | 256 GB | 2       | 379   | 0     | 1.04   |
| Seagate   | STT_FTM64GX25H     | 64 GB  | 1       | 378   | 0     | 1.04   |
| SanDisk   | SDSSDHP064G        | 64 GB  | 9       | 378   | 0     | 1.04   |
| Plextor   | PX-256M6S+         | 256 GB | 1       | 377   | 0     | 1.04   |
| Crucial   | CT1050MX300SSD1    | 1 TB   | 35      | 545   | 46    | 1.03   |
| SK hynix  | HFS128G32MNB-2200A | 128 GB | 1       | 375   | 0     | 1.03   |
| Kingston  | SUV400S37480G      | 480 GB | 38      | 421   | 78    | 1.03   |
| SanDisk   | SD6SB1M128G        | 128 GB | 3       | 375   | 0     | 1.03   |
| Toshiba   | THNSNF256GRHS      | 128 GB | 2       | 375   | 0     | 1.03   |
| Team      | T253X5480G         | 480 GB | 2       | 374   | 0     | 1.03   |
| Apacer    | AS450              | 240 GB | 1       | 374   | 0     | 1.03   |
| Plextor   | PX-128M7VC         | 128 GB | 6       | 374   | 0     | 1.03   |
| Samsung   | SSD PM871b M.2 ... | 512 GB | 4       | 374   | 0     | 1.03   |
| Samsung   | MZYLF128HCHP-000L2 | 128 GB | 11      | 373   | 0     | 1.02   |
| Intel     | SSDSC2BW180A3H     | 180 GB | 18      | 386   | 1     | 1.02   |
| Samsung   | MZNTY128HDHP-000H1 | 128 GB | 11      | 373   | 0     | 1.02   |
| SanDisk   | SD7SN3Q256G1002    | 256 GB | 6       | 472   | 173   | 1.02   |
| WDC       | WDS250G2B0B-00YS70 | 250 GB | 41      | 371   | 0     | 1.02   |
| Colorful  | SL500              | 512 GB | 1       | 371   | 0     | 1.02   |
| WDC       | WDS240G1G0A-00SS50 | 240 GB | 37      | 371   | 0     | 1.02   |
| SanDisk   | SD7SN6S512G1001    | 512 GB | 2       | 371   | 0     | 1.02   |
| Samsung   | Portable SSD T5    | 250 GB | 11      | 371   | 0     | 1.02   |
| Kingston  | RBUSC180DS37128GH  | 128 GB | 4       | 406   | 1     | 1.02   |
| Team      | TIM3F49256GMBA04MA | 256 GB | 1       | 370   | 0     | 1.02   |
| SanDisk   | SD9SB8W256G1122    | 256 GB | 1       | 370   | 0     | 1.02   |
| China     | 512GB PCS 2.5" SSD | 512 GB | 1       | 370   | 0     | 1.01   |
| SanDisk   | X300 M.2 2280      | 128 GB | 1       | 369   | 0     | 1.01   |
| Samsung   | SSD SM871 2.5 7mm  | 512 GB | 3       | 920   | 104   | 1.01   |
| Samsung   | MMCQE28G8MUP-0VA   | 128 GB | 4       | 634   | 1     | 1.01   |
| Intel     | SSDSC2BW240A3H     | 240 GB | 1       | 369   | 0     | 1.01   |
| Toshiba   | THNS064GE4BBDC     | 64 GB  | 2       | 369   | 0     | 1.01   |
| Team      | TEAML5Lite3D1T     | 1 TB   | 3       | 368   | 0     | 1.01   |
| Samsung   | MZRPC128HACD-000SO | 64 GB  | 4       | 367   | 0     | 1.01   |
| OCZ       | VERTEX             | 32 GB  | 3       | 602   | 1     | 1.01   |
| ADATA     | SSD DP900 512GB... | 512 GB | 4       | 1103  | 509   | 1.01   |
| Samsung   | SSD PM871b 2.5 7mm | 512 GB | 6       | 366   | 0     | 1.01   |
| Plextor   | PX-512M6S+         | 512 GB | 1       | 366   | 0     | 1.00   |
| Team      | L5 LITE SSD        | 120 GB | 3       | 366   | 0     | 1.00   |
| China     | SATA SSD           | 16 GB  | 5       | 406   | 11    | 1.00   |
| Kingston  | SV100S264G         | 64 GB  | 14      | 520   | 4     | 1.00   |
| Toshiba   | THNSNJ512GDNU A    | 512 GB | 4       | 365   | 0     | 1.00   |
| SanDisk   | SD8SN8U512G1002    | 512 GB | 25      | 365   | 0     | 1.00   |
| Plextor   | PX-64M3            | 64 GB  | 3       | 668   | 346   | 1.00   |
| Seagate   | SSD                | 500 GB | 2       | 364   | 0     | 1.00   |
| OCZ       | VERTEX460A         | 120 GB | 10      | 384   | 1     | 1.00   |
| Hyundai   | 480GB SSD          | 480 GB | 1       | 363   | 0     | 1.00   |
| Crucial   | CT512M550SSD1      | 512 GB | 10      | 839   | 180   | 1.00   |
| Samsung   | MZMTD512HAGL-000MV | 512 GB | 2       | 363   | 0     | 1.00   |
| Redapple  | SSD                | 32 GB  | 1       | 363   | 0     | 1.00   |
| Intel     | SSDSC2BW240A4      | 240 GB | 39      | 621   | 3     | 0.99   |
| Kingston  | SKC300S37A60G      | 64 GB  | 17      | 447   | 5     | 0.99   |
| Samsung   | MZMTE256HMHP-000   | 256 GB | 1       | 362   | 0     | 0.99   |
| Corsair   | Force LE200 SSD    | 240 GB | 10      | 435   | 6     | 0.99   |
| Kingston  | SS200S330G         | 32 GB  | 4       | 361   | 0     | 0.99   |
| Micron    | 5210_MTFDDAK7T6QDE | 7.6 TB | 5       | 361   | 0     | 0.99   |
| WDC       | WDS500G1B0A-00H9H0 | 500 GB | 25      | 373   | 1     | 0.99   |
| Kingston  | SV300S37A240G      | 240 GB | 228     | 408   | 16    | 0.99   |
| Samsung   | MZNLN512HMJP-000L7 | 512 GB | 14      | 359   | 0     | 0.99   |
| ADATA     | SX900              | 64 GB  | 8       | 543   | 386   | 0.99   |
| Intel     | SSDSC2KB038T8      | 3.8 TB | 7       | 359   | 0     | 0.98   |
| KingShare | 230120SSD          | 128 GB | 1       | 358   | 0     | 0.98   |
| SanDisk   | X400 M.2 2280      | 256 GB | 32      | 358   | 0     | 0.98   |
| Goodram   | C40                | 120 GB | 8       | 384   | 2     | 0.98   |
| Micron    | MTFDDAK256MBF-1... | 256 GB | 6       | 357   | 0     | 0.98   |
| Samsung   | MZMPA064HMDR-00000 | 64 GB  | 3       | 357   | 0     | 0.98   |
| Intel     | SSDSC2BW120A4      | 120 GB | 48      | 453   | 1     | 0.98   |
| SanDisk   | SD9SN8W512G1002    | 512 GB | 5       | 356   | 0     | 0.98   |
| Kingston  | SUV400S37240G      | 240 GB | 177     | 442   | 84    | 0.98   |
| China     | 240GB SSD          | 240 GB | 8       | 356   | 0     | 0.98   |
| Kingston  | SUV300S37A240G     | 240 GB | 19      | 387   | 1     | 0.98   |
| Kingston  | SHPM2280P2H-480G   | 480 GB | 4       | 487   | 2     | 0.98   |
| ADATA     | SP310              | 128 GB | 2       | 355   | 0     | 0.97   |
| CFD       | CSSD-MG4VT         | 1 TB   | 1       | 354   | 0     | 0.97   |
| ExeGate   | EX276536RUS        | 120 GB | 1       | 353   | 0     | 0.97   |
| ADATA     | SU700              | 240 GB | 1       | 353   | 0     | 0.97   |
| KingSpec  | KSD-SA25.5-016MJ   | 16 GB  | 1       | 353   | 0     | 0.97   |
| Transcend | TS32GSSD370        | 32 GB  | 3       | 353   | 0     | 0.97   |
| Goodram   | SSDPR-CL100-480-G2 | 480 GB | 10      | 353   | 0     | 0.97   |
| Intel     | SSDSC2CT240A3      | 240 GB | 6       | 714   | 1     | 0.96   |
| Intel     | SSDSC2BF256A5 SATA | 256 GB | 2       | 352   | 0     | 0.96   |
| Samsung   | MZNLN128HCGR-000L2 | 128 GB | 3       | 352   | 0     | 0.96   |
| SK hynix  | SC300 SATA         | 256 GB | 1       | 351   | 0     | 0.96   |
| SanDisk   | SD8SB8U128G1001    | 128 GB | 4       | 351   | 0     | 0.96   |
| Micron    | 1100_MTFDDAK512TBN | 512 GB | 23      | 684   | 65    | 0.96   |
| KingDian  | N480-240GB         | 240 GB | 1       | 351   | 0     | 0.96   |
| Kingston  | SUV400S37120G      | 120 GB | 206     | 373   | 50    | 0.96   |
| Corsair   | Force LS SSD       | 480 GB | 2       | 970   | 1     | 0.96   |
| Toshiba   | THNSNH128GBST      | 128 GB | 6       | 601   | 108   | 0.96   |
| Kingmax   | SSD                | 512 GB | 1       | 349   | 0     | 0.96   |
| Samsung   | MZYTY128HDHP-000L2 | 128 GB | 9       | 348   | 0     | 0.95   |
| Samsung   | MZ7LN128HAHQ-000L1 | 128 GB | 4       | 347   | 0     | 0.95   |
| SanDisk   | SD7SN6S-512G-1006  | 512 GB | 5       | 347   | 0     | 0.95   |
| SanDisk   | SD7SB7S512G1001    | 512 GB | 3       | 346   | 0     | 0.95   |
| Kingston  | SA400S371920G      | 1.9 TB | 5       | 346   | 0     | 0.95   |
| Toshiba   | THNSNX024GMNT      | 24 GB  | 2       | 346   | 0     | 0.95   |
| SanDisk   | SD6SF1M128G1022I   | 128 GB | 2       | 451   | 1     | 0.95   |
| SanDisk   | SSD U100           | 32 GB  | 11      | 347   | 92    | 0.95   |
| SanDisk   | SDSSDX240GG25      | 240 GB | 16      | 988   | 68    | 0.95   |
| SanDisk   | SD7UB2Q512G1122    | 512 GB | 3       | 345   | 0     | 0.95   |
| Samsung   | MZ7LN256HMJP-000L7 | 256 GB | 4       | 345   | 0     | 0.95   |
| Advantech | SQF-S25M4-32G-S9E  | 32 GB  | 1       | 345   | 0     | 0.95   |
| Vaseky    | v800-128G          | 128 GB | 1       | 344   | 0     | 0.94   |
| OCZ       | VERTEX450          | 128 GB | 9       | 608   | 232   | 0.94   |
| Kingston  | SUV300S37A120G     | 120 GB | 48      | 349   | 1     | 0.94   |
| Crucial   | CT275MX300SSD1     | 275 GB | 90      | 425   | 79    | 0.94   |
| Toshiba   | THNSNJ1T02CSX      | 1 TB   | 1       | 344   | 0     | 0.94   |
| Kingston  | SHFS37A240G        | 240 GB | 45      | 370   | 159   | 0.94   |
| Intel     | SSDSC2BW240H6      | 240 GB | 15      | 414   | 6     | 0.94   |
| Kingston  | SMS200S3240G       | 240 GB | 7       | 676   | 436   | 0.94   |
| Foxline   | FLSSD480X3         | 480 GB | 1       | 343   | 0     | 0.94   |
| Colorful  | SL500              | 256 GB | 3       | 343   | 0     | 0.94   |
| AMD       | R5M256G8           | 256 GB | 1       | 342   | 0     | 0.94   |
| SanDisk   | X400 M.2 2280      | 512 GB | 6       | 341   | 0     | 0.94   |
| Samsung   | MZMPC128HBFU-000L1 | 128 GB | 6       | 341   | 0     | 0.94   |
| Kingston  | RBU-SNS8151S396GG  | 96 GB  | 3       | 435   | 3     | 0.94   |
| BAITITON  | BT58SSD07M         | 120 GB | 1       | 341   | 0     | 0.93   |
| Intenso   | SSD M.2 HIGH       | 120 GB | 1       | 341   | 0     | 0.93   |
| Kingston  | RBU-SNS8152S351... | 512 GB | 2       | 340   | 0     | 0.93   |
| Goodram   | IRP-SSDPR-S25B-240 | 240 GB | 2       | 340   | 0     | 0.93   |
| Goodram   | SSD                | 120 GB | 55      | 341   | 1     | 0.93   |
| Intel     | SSDMAEMC040G2      | 40 GB  | 2       | 1135  | 3     | 0.93   |
| Intel     | SSDSCKJW120H6      | 120 GB | 1       | 339   | 0     | 0.93   |
| Corsair   | Force LE SSD       | 480 GB | 5       | 339   | 0     | 0.93   |
| THU       | SSD 120G           | 120 GB | 1       | 339   | 0     | 0.93   |
| Micron    | 5300_MTFDDAK960TDT | 960 GB | 6       | 339   | 0     | 0.93   |
| Seagate   | IronWolf ZA2000... | 2 TB   | 1       | 338   | 0     | 0.93   |
| OCZ       | ARC100             | 120 GB | 17      | 338   | 0     | 0.93   |
| OCZ       | VERTEX3            | 128 GB | 3       | 478   | 1     | 0.93   |
| Plextor   | PX-128S2G          | 128 GB | 3       | 338   | 0     | 0.93   |
| SanDisk   | SD7SB2Q-512G-1006  | 512 GB | 7       | 380   | 3     | 0.93   |
| Transcend | TSA                | 480 GB | 1       | 337   | 0     | 0.93   |
| OCZ       | AGILITY3           | 90 GB  | 5       | 450   | 1     | 0.92   |
| Kingston  | RBUSNS8180S3128GI1 | 128 GB | 6       | 337   | 0     | 0.92   |
| Mushkin   | MKNSSDCR120GB-7    | 120 GB | 3       | 711   | 343   | 0.92   |
| Micron    | M600_MTFDDAV256MBF | 256 GB | 11      | 336   | 0     | 0.92   |
| Corsair   | Neutron XT SSD     | 480 GB | 3       | 561   | 2     | 0.92   |
| ADATA     | SU760              | 512 GB | 5       | 336   | 0     | 0.92   |
| Crucial   | CT525MX300SSD1     | 528 GB | 119     | 464   | 120   | 0.92   |
| WDC       | WDS200T2B0B        | 2 TB   | 4       | 335   | 0     | 0.92   |
| Samsung   | MZ7LH240HAHQ-00005 | 240 GB | 15      | 335   | 0     | 0.92   |
| Gigabyte  | GP-UDPRO256G       | 256 GB | 1       | 334   | 0     | 0.92   |
| Micron    | MTFDDAK960TDT-1... | 960 GB | 1       | 334   | 0     | 0.92   |
| GeIL      | ZENITH 120G R3     | 120 GB | 1       | 334   | 0     | 0.92   |
| Toshiba   | THNSNH128G8NT      | 128 GB | 3       | 334   | 0     | 0.92   |
| Intel     | SSDSC2KG480G7      | 480 GB | 3       | 342   | 3     | 0.92   |
| Kingston  | SQ500S371920G      | 1.9 TB | 1       | 334   | 0     | 0.92   |
| SK hynix  | SC300 M.2 2280     | 512 GB | 1       | 334   | 0     | 0.92   |
| Plextor   | PX-512M8VC         | 512 GB | 5       | 333   | 0     | 0.91   |
| AFOX      | SSD                | 120 GB | 3       | 333   | 0     | 0.91   |
| SanDisk   | X300 MSATA         | 256 GB | 4       | 331   | 0     | 0.91   |
| ADATA     | SP600              | 64 GB  | 13      | 402   | 2     | 0.91   |
| OCZ       | VECTOR150          | 240 GB | 9       | 790   | 9     | 0.91   |
| Kingston  | SV300S37A-60G      | 64 GB  | 4       | 330   | 0     | 0.91   |
| China     | SATA SSD           | 480 GB | 28      | 330   | 0     | 0.91   |
| SanDisk   | SDSSDX120GG25      | 120 GB | 10      | 464   | 3     | 0.90   |
| Kingston  | RBUSNS4180S364GJ   | 64 GB  | 1       | 330   | 0     | 0.90   |
| Crucial   | CT275MX300SSD4     | 275 GB | 26      | 429   | 3     | 0.90   |
| SanDisk   | SD6SB1M256G1002    | 256 GB | 4       | 329   | 0     | 0.90   |
| Samsung   | MZNTY256HDHP-000L2 | 256 GB | 8       | 329   | 0     | 0.90   |
| SK hynix  | SC311 SATA         | 256 GB | 76      | 333   | 1     | 0.90   |
| SPCC      | SSD                | 240 GB | 68      | 403   | 160   | 0.90   |
| ADATA     | SX900              | 128 GB | 16      | 667   | 449   | 0.90   |
| Timetec   | 35TTM8SSATA-1TB    | 1 TB   | 1       | 328   | 0     | 0.90   |
| SanDisk   | X400 M.2 2280      | 128 GB | 16      | 327   | 0     | 0.90   |
| Intel     | SSDSA2BW300G3H     | 304 GB | 2       | 327   | 0     | 0.90   |
| VENO S... | SSD                | 240 GB | 1       | 326   | 0     | 0.89   |
| Intel     | SSDSA2BW160G3L     | 160 GB | 19      | 326   | 0     | 0.89   |
| Mushkin   | MKNSSDSR250GB      | 250 GB | 3       | 325   | 0     | 0.89   |
| Samsung   | MZ7TE128HMGR-00000 | 128 GB | 4       | 325   | 0     | 0.89   |
| ADATA     | SX930              | 120 GB | 5       | 324   | 0     | 0.89   |
| SanDisk   | SD8SBBU120G1122    | 120 GB | 8       | 324   | 0     | 0.89   |
| SanDisk   | SDSSDH3250G        | 250 GB | 24      | 332   | 4     | 0.89   |
| Samsung   | MZ7LN256HCHP-000F0 | 256 GB | 3       | 324   | 0     | 0.89   |
| Toshiba   | SSD0256XQC82X20... | 256 GB | 1       | 323   | 0     | 0.89   |
| SanDisk   | SD6SF1M128G1022    | 128 GB | 1       | 323   | 0     | 0.89   |
| Kingston  | RBU-SNS8152S325... | 256 GB | 1       | 323   | 0     | 0.89   |
| Samsung   | MZNLN256HMHQ-000H1 | 256 GB | 25      | 322   | 0     | 0.88   |
| Fujitsu   | F500S-480GB        | 480 GB | 1       | 321   | 0     | 0.88   |
| OCZ       | TRION100           | 120 GB | 10      | 364   | 2     | 0.88   |
| OCZ       | VERTEX3 LP         | 64 GB  | 1       | 320   | 0     | 0.88   |
| Samsung   | SSD 840 EVO 500... | 500 GB | 6       | 320   | 0     | 0.88   |
| Kingston  | SVP180S264G        | 64 GB  | 1       | 320   | 0     | 0.88   |
| Inland    | SSD                | 1 TB   | 1       | 319   | 0     | 0.88   |
| SanDisk   | SDSSDXP120G        | 120 GB | 2       | 319   | 0     | 0.88   |
| Samsung   | MZNTY256HDHP-000   | 256 GB | 1       | 319   | 0     | 0.87   |
| SanDisk   | SD9SN8W128G        | 128 GB | 1       | 318   | 0     | 0.87   |
| Intel     | SSDSCMMW240A3L     | 240 GB | 5       | 354   | 1     | 0.87   |
| KingDian  | S280               | 1 TB   | 7       | 317   | 0     | 0.87   |
| Toshiba   | THNSNC128GBSJ      | 128 GB | 2       | 316   | 0     | 0.87   |
| SanDisk   | SSD U100           | 128 GB | 1       | 316   | 0     | 0.87   |
| Goodram   | SSDPR-CL100-120    | 120 GB | 2       | 316   | 0     | 0.87   |
| BRAVEE... | SSD                | 240 GB | 1       | 316   | 0     | 0.87   |
| Samsung   | MZYTN512HDJH-000L2 | 512 GB | 3       | 316   | 0     | 0.87   |
| Samsung   | MMCRE28G8MXP-0VBL1 | 128 GB | 3       | 315   | 0     | 0.87   |
| Samsung   | 470 Series SSD     | 64 GB  | 2       | 315   | 0     | 0.86   |
| Transcend | TS64GMTS400S       | 64 GB  | 5       | 315   | 0     | 0.86   |
| Samsung   | MZNLN128HAHQ-00000 | 128 GB | 4       | 315   | 0     | 0.86   |
| Kingston  | RBU-SC100S37128GD  | 128 GB | 3       | 315   | 0     | 0.86   |
| Toshiba   | THNSNJ512G8NY      | 512 GB | 1       | 315   | 0     | 0.86   |
| Phison    | 128GB PS3110-S10C  | 128 GB | 2       | 315   | 0     | 0.86   |
| Samsung   | MZNTY256HDHP-000L7 | 256 GB | 19      | 315   | 0     | 0.86   |
| Samsung   | MZMTE128HMGR-000MV | 128 GB | 7       | 314   | 0     | 0.86   |
| Intel     | SSDSA2BW160G3H     | 160 GB | 16      | 379   | 1     | 0.86   |
| Micron    | 1100_MTFDDAK256TBN | 256 GB | 33      | 375   | 131   | 0.86   |
| GLOWAY    | STK240GS3-S7       | 240 GB | 1       | 313   | 0     | 0.86   |
| WDC       | WDBNCE2500PNC      | 250 GB | 16      | 313   | 0     | 0.86   |
| Intel     | SSDSA2M040G2GC     | 40 GB  | 10      | 763   | 4     | 0.86   |
| Smartbuy  | mSata              | 128 GB | 3       | 312   | 0     | 0.86   |
| Samsung   | MZ7LH128HBHQ-000L1 | 128 GB | 3       | 312   | 0     | 0.86   |
| Crucial   | CT250MX200SSD1     | 250 GB | 38      | 312   | 0     | 0.86   |
| Samsung   | SSD PM810 2.5"     | 128 GB | 1       | 1560  | 4     | 0.86   |
| Samsung   | MZNLN256HCHP-000H1 | 256 GB | 5       | 311   | 0     | 0.85   |
| OCZ       | VERTEX2            | 240 GB | 2       | 311   | 0     | 0.85   |
| China     | T240               | 240 GB | 1       | 311   | 0     | 0.85   |
| Samsung   | SSD 860 EVO        | 500 GB | 997     | 312   | 2     | 0.85   |
| WDC       | WDBNCE0020PNC      | 2 TB   | 1       | 310   | 0     | 0.85   |
| Seagate   | SSD                | 250 GB | 5       | 310   | 0     | 0.85   |
| Aura      | Pro S MB258        | 1 TB   | 1       | 310   | 0     | 0.85   |
| SanDisk   | SD9SN8W256G1027    | 256 GB | 2       | 310   | 0     | 0.85   |
| KingSpec  | P3-2TB             | 2 TB   | 2       | 309   | 0     | 0.85   |
| Kingston  | SHFS37A120G        | 120 GB | 139     | 416   | 177   | 0.85   |
| Samsung   | SSD PM871b M.2 ... | 256 GB | 17      | 308   | 0     | 0.84   |
| China     | SSD                | 64 GB  | 11      | 355   | 1     | 0.84   |
| Team      | TEAML5Lite3D120G   | 120 GB | 8       | 307   | 0     | 0.84   |
| ADATA     | SSD S599           | 64 GB  | 4       | 307   | 0     | 0.84   |
| SanDisk   | SD8SN8U256G1027    | 256 GB | 3       | 306   | 0     | 0.84   |
| Imation   | M.2 SATA3 256GB... | 256 GB | 1       | 306   | 0     | 0.84   |
| Micron    | MTFDDAK256MAM-1K12 | 256 GB | 29      | 358   | 386   | 0.84   |
| Toshiba   | THNSNJ128GMCT      | 128 GB | 1       | 306   | 0     | 0.84   |
| Samsung   | MZNTY256HDHP-00000 | 256 GB | 7       | 305   | 0     | 0.84   |
| Kingston  | USNS8180S3512GJ    | 512 GB | 3       | 305   | 0     | 0.84   |
| SK hynix  | HFS256G32TND-N210A | 256 GB | 5       | 358   | 51    | 0.84   |
| ADATA     | SP600              | 512 GB | 1       | 305   | 0     | 0.84   |
| Samsung   | MMCRE64G8MPP-0VA   | 64 GB  | 2       | 337   | 1     | 0.84   |
| Samsung   | SSD 860 PRO        | 1 TB   | 39      | 304   | 0     | 0.83   |
| SanDisk   | SDSA6PM-064G-1006  | 64 GB  | 2       | 304   | 0     | 0.83   |
| Samsung   | MZMTE256HMHP-00005 | 256 GB | 1       | 304   | 0     | 0.83   |
| Intel     | SSDSC2BW120H6      | 120 GB | 21      | 330   | 4     | 0.83   |
| SanDisk   | SD6SB1M128G1001    | 128 GB | 6       | 303   | 0     | 0.83   |
| Intenso   | SATA III SSD       | 120 GB | 29      | 308   | 1     | 0.83   |
| PNY       | CS900 240 SSD      | 240 GB | 1       | 303   | 0     | 0.83   |
| KingSpec  | Q-360              | 360 GB | 7       | 302   | 0     | 0.83   |
| Samsung   | MZ7KH240HAHQ-00005 | 240 GB | 4       | 302   | 0     | 0.83   |
| SMI       | L06B B0KB          | 240 GB | 1       | 302   | 0     | 0.83   |
| SanDisk   | SD7TN3Q-256G-1006  | 256 GB | 6       | 347   | 1     | 0.83   |
| SK hynix  | SC300 M.2 2280     | 128 GB | 2       | 301   | 0     | 0.83   |
| WDC       | WDS120G1G0B-00RC30 | 120 GB | 24      | 300   | 0     | 0.82   |
| SanDisk   | SD9TB8W256G1001    | 256 GB | 10      | 300   | 0     | 0.82   |
| Intenso   | SSD                | 512 GB | 18      | 300   | 0     | 0.82   |
| Samsung   | SSD 860 PRO        | 256 GB | 61      | 300   | 0     | 0.82   |
| SanDisk   | SSD PLUS 480 GB    | 480 GB | 18      | 396   | 6     | 0.82   |
| Samsung   | SSD 860 EVO        | 1 TB   | 633     | 300   | 1     | 0.82   |
| Mushkin   | MKNSSDAT240GB-DX   | 240 GB | 1       | 299   | 0     | 0.82   |
| Ramaxel   | RDM-II XM020C      | 24 GB  | 1       | 299   | 0     | 0.82   |
| Kingston  | SV200S3256G        | 256 GB | 6       | 529   | 2     | 0.82   |
| Ramsta    | SSD S800           | 120 GB | 1       | 299   | 0     | 0.82   |
| SK hynix  | HFS256G39MND-3310A | 256 GB | 3       | 299   | 0     | 0.82   |
| Samsung   | MZ7LM480HMHQ-000MV | 480 GB | 2       | 298   | 0     | 0.82   |
| Samsung   | SSD 840 EVO        | 752 GB | 5       | 298   | 0     | 0.82   |
| Plextor   | PX-256S3G          | 256 GB | 2       | 298   | 0     | 0.82   |
| SanDisk   | SSD i100           | 32 GB  | 6       | 298   | 0     | 0.82   |
| PNY       | SSD2SC120G1SA75... | 120 GB | 3       | 298   | 0     | 0.82   |
| Team      | T253E2001T         | 1 TB   | 7       | 297   | 0     | 0.82   |
| ADATA     | SP900              | 256 GB | 19      | 455   | 2     | 0.81   |
| Plextor   | PX-128M7VG         | 128 GB | 3       | 297   | 0     | 0.81   |
| Apacer    | 256GB SATA Flas... | 256 GB | 2       | 296   | 0     | 0.81   |
| SanDisk   | SD8TB8U512G1001    | 512 GB | 5       | 296   | 0     | 0.81   |
| Intenso   | SSD Sata III       | 250 GB | 1       | 295   | 0     | 0.81   |
| Kingston  | SUV500M8240G       | 240 GB | 6       | 295   | 0     | 0.81   |
| Ramaxel   | RDM-II XM020C024G  | 24 GB  | 2       | 295   | 0     | 0.81   |
| Samsung   | MZ7KM960HMJP-00005 | 960 GB | 2       | 294   | 0     | 0.81   |
| Samsung   | MZAPF032HCFV-000H1 | 32 GB  | 1       | 294   | 0     | 0.81   |
| OCZ       | VERTEX-TURBO       | 128 GB | 1       | 293   | 0     | 0.80   |
| Palit     | UVSE               | 120 GB | 1       | 293   | 0     | 0.80   |
| Kingston  | SNVP325S2256GB     | 256 GB | 1       | 293   | 0     | 0.80   |
| ADATA     | SP550              | 480 GB | 3       | 292   | 0     | 0.80   |
| Toshiba   | THNSNH060GMCT      | 64 GB  | 1       | 292   | 0     | 0.80   |
| Transcend | TS256GSSD340       | 256 GB | 5       | 292   | 0     | 0.80   |
| Plextor   | PX-1TM8VC          | 1 TB   | 1       | 292   | 0     | 0.80   |
| SK hynix  | SC311 SATA         | 128 GB | 52      | 292   | 0     | 0.80   |
| Toshiba   | Q300               | 120 GB | 9       | 292   | 0     | 0.80   |
| Samsung   | SSD 860 QVO        | 2 TB   | 58      | 308   | 15    | 0.80   |
| Seagate   | BarraCuda SSD Z... | 250 GB | 11      | 291   | 0     | 0.80   |
| V-GeN     | V-GEN11SM20AR10... | 1 TB   | 1       | 291   | 0     | 0.80   |
| Patriot   | Blaze              | 64 GB  | 7       | 291   | 0     | 0.80   |
| Crucial   | CT500MX200SSD4     | 500 GB | 6       | 457   | 1     | 0.80   |
| Innodisk  | 2.5" SATA SSD 3ME3 | 128 GB | 3       | 290   | 0     | 0.80   |
| Samsung   | MZNTE256HMHP-000L7 | 256 GB | 3       | 290   | 0     | 0.80   |
| SK hynix  | SC311 SATA         | 512 GB | 23      | 299   | 46    | 0.80   |
| OCZ       | ARC100             | 480 GB | 8       | 291   | 1     | 0.80   |
| Transcend | TS32GSSD340        | 32 GB  | 2       | 289   | 0     | 0.79   |
| Samsung   | SSD 860 EVO        | 250 GB | 596     | 290   | 1     | 0.79   |
| Palit     | UVSE               | 240 GB | 2       | 288   | 0     | 0.79   |
| Corsair   | Neutron SSD        | 64 GB  | 5       | 540   | 3     | 0.79   |
| ADATA     | SP600              | 32 GB  | 12      | 288   | 0     | 0.79   |
| Samsung   | SSD PM871a M.2 ... | 512 GB | 1       | 287   | 0     | 0.79   |
| Intel     | SSDSC2KF256G8      | 256 GB | 1       | 287   | 0     | 0.79   |
| Plextor   | PH6-CE120-G        | 120 GB | 4       | 287   | 0     | 0.79   |
| Samsung   | MZMPC128HBFU-000MV | 128 GB | 4       | 287   | 0     | 0.79   |
| Samsung   | MZMTD512HAGL-000L1 | 512 GB | 4       | 313   | 25    | 0.79   |
| Samsung   | MZNTY128HDHP-00000 | 128 GB | 15      | 286   | 0     | 0.79   |
| Kingston  | RBU-SNS8152S312... | 128 GB | 4       | 285   | 0     | 0.78   |
| Samsung   | MZHPV512HDGL-000L1 | 512 GB | 1       | 285   | 0     | 0.78   |
| Kingston  | SUV300S37A480G     | 480 GB | 3       | 285   | 0     | 0.78   |
| Micron    | MTFDDAK960TCB-1... | 960 GB | 1       | 856   | 2     | 0.78   |
| OCZ       | VTX3-25SAT3-120G   | 120 GB | 1       | 285   | 0     | 0.78   |
| Lenovo    | Thinklife ST600... | 256 GB | 1       | 285   | 0     | 0.78   |
| OCZ       | VERTEX             | 64 GB  | 3       | 353   | 1     | 0.78   |
| Samsung   | MMCRE28G5MXP-0VBH1 | 128 GB | 2       | 284   | 0     | 0.78   |
| Smartbuy  | SSD                | 240 GB | 36      | 328   | 1     | 0.78   |
| Toshiba   | THNSNC128GMLJ      | 128 GB | 2       | 284   | 0     | 0.78   |
| SanDisk   | SD7SN6S-256G-1006  | 256 GB | 9       | 284   | 0     | 0.78   |
| Zheino    | CHN-25SATAS3-256   | 256 GB | 2       | 284   | 0     | 0.78   |
| Phison    | 256GB PS3110-S10C  | 256 GB | 3       | 283   | 0     | 0.78   |
| Corsair   | CMFSSD-32D1        | 32 GB  | 1       | 566   | 1     | 0.78   |
| OCZ       | OCTANE S2          | 64 GB  | 2       | 283   | 0     | 0.78   |
| Intel     | SSDSCKHW240A4      | 240 GB | 1       | 282   | 0     | 0.77   |
| SanDisk   | SDSSDH3 512G       | 512 GB | 15      | 282   | 0     | 0.77   |
| Mushkin   | MKNSSDS2120GB      | 120 GB | 1       | 282   | 0     | 0.77   |
| China     | SATA SSD           | 20 GB  | 17      | 300   | 1     | 0.77   |
| Micron    | C400-MTFDDAC064MAM | 64 GB  | 4       | 281   | 0     | 0.77   |
| Apple     | SSD TS064C         | 64 GB  | 5       | 280   | 0     | 0.77   |
| SanDisk   | SD8SN8U-256G-1006  | 256 GB | 60      | 301   | 69    | 0.77   |
| Samsung   | MZ7TE128HMGR-000H1 | 128 GB | 6       | 338   | 3     | 0.77   |
| Samsung   | SSD 860 EVO mSATA  | 1 TB   | 8       | 279   | 0     | 0.77   |
| WDC       | WDS100T1B0B-00AS40 | 1 TB   | 4       | 279   | 0     | 0.77   |
| Kingston  | MS80000058588      | 128 GB | 1       | 279   | 0     | 0.76   |
| Kingston  | SMS100S232G        | 32 GB  | 1       | 279   | 0     | 0.76   |
| Transcend | TS256GSSD320       | 256 GB | 3       | 278   | 0     | 0.76   |
| China     | SSD                | 960 GB | 2       | 278   | 0     | 0.76   |
| Apacer    | AS330              | 120 GB | 3       | 277   | 0     | 0.76   |
| PNY       | CS2211 480GB SSD   | 480 GB | 1       | 277   | 0     | 0.76   |
| SPCC      | SSD                | 64 GB  | 96      | 286   | 32    | 0.76   |
| Crucial   | CT128MX100SSD1     | 128 GB | 17      | 1073  | 72    | 0.76   |
| Micron    | 1100 SATA          | 512 GB | 27      | 339   | 205   | 0.75   |
| Reeinno   | ST240GB S4S3       | 240 GB | 2       | 275   | 0     | 0.75   |
| Toshiba   | THNSFJ256GMCT      | 256 GB | 1       | 275   | 0     | 0.75   |
| ADATA     | SP600NS34          | 256 GB | 1       | 274   | 0     | 0.75   |
| Team      | T253X2512G         | 512 GB | 15      | 274   | 0     | 0.75   |
| Kingston  | RBUSNS8180S3128GI  | 128 GB | 5       | 274   | 0     | 0.75   |
| SuperM... | SSD                | 32 GB  | 2       | 273   | 0     | 0.75   |
| Gigaby... | GP-GSTFS30512GTTD  | 512 GB | 4       | 273   | 0     | 0.75   |
| Samsung   | SSD PM800 TM       | 128 GB | 3       | 273   | 0     | 0.75   |
| SanDisk   | SD9SN8W256G        | 256 GB | 4       | 273   | 0     | 0.75   |
| Samsung   | MZNLN128HCGR-00000 | 128 GB | 3       | 273   | 0     | 0.75   |
| Samsung   | MZNTE256HMHP-000H1 | 256 GB | 4       | 273   | 0     | 0.75   |
| BAITITON  | BT58SSD07S         | 120 GB | 1       | 273   | 0     | 0.75   |
| Samsung   | SSD PM871b M.2 ... | 128 GB | 9       | 272   | 0     | 0.75   |
| SanDisk   | SD8SN8U128G1002    | 128 GB | 11      | 272   | 0     | 0.75   |
| WDC       | WDS500G2B0A        | 500 GB | 48      | 271   | 0     | 0.74   |
| Lite-On   | J8-L1032-11 M.2... | 32 GB  | 1       | 270   | 0     | 0.74   |
| WDC       | WDS240G1G0B-00RC30 | 240 GB | 8       | 270   | 0     | 0.74   |
| Plextor   | PX-256M5Pro        | 256 GB | 15      | 270   | 0     | 0.74   |
| BlueRay   | SDM8SI960A         | 960 GB | 1       | 268   | 0     | 0.73   |
| Crucial   | M500IT_MTFDDAK1... | 128 GB | 1       | 267   | 0     | 0.73   |
| SanDisk   | SDSSDXPS960G       | 960 GB | 5       | 423   | 67    | 0.73   |
| Micron    | 1300 SATA          | 1 TB   | 3       | 267   | 0     | 0.73   |
| Lite-On   | IT LCS-256L9S      | 256 GB | 4       | 267   | 0     | 0.73   |
| Mushkin   | MKNSSDSR500GB      | 500 GB | 2       | 266   | 0     | 0.73   |
| Apple     | SSD SM0128G        | 121 GB | 126     | 266   | 0     | 0.73   |
| BIWIN     | SSD                | 120 GB | 6       | 265   | 0     | 0.73   |
| Toshiba   | A100               | 240 GB | 11      | 265   | 0     | 0.73   |
| SanDisk   | SDSSDA240G         | 240 GB | 188     | 275   | 4     | 0.73   |
| TwinMOS   | SSD SATA2.5"-120GB | 120 GB | 1       | 265   | 0     | 0.73   |
| SanDisk   | SD9SN8W128G1102    | 128 GB | 12      | 265   | 0     | 0.73   |
| Intel     | SSDSC2KG240G7      | 240 GB | 1       | 265   | 0     | 0.73   |
| Intel     | SSDPAMM0008G1      | 8 GB   | 1       | 265   | 0     | 0.73   |
| Exascend  | EXSC3A002TB        | 2 TB   | 1       | 264   | 0     | 0.73   |
| Verbatim  | Vi500 S3 120GB SSD | 120 GB | 6       | 264   | 0     | 0.73   |
| Micron    | MTFDDAK480TDT      | 480 GB | 3       | 264   | 0     | 0.72   |
| SanDisk   | SDSSDA-1T00        | 1 TB   | 21      | 264   | 0     | 0.72   |
| Hikvision | HKVSN HS-SSD-E1... | 128 GB | 1       | 263   | 0     | 0.72   |
| Plextor   | PX-AG256M6e        | 256 GB | 2       | 263   | 0     | 0.72   |
| SPCC      | SSD                | 2 TB   | 1       | 263   | 0     | 0.72   |
| Goodram   | SSDPR-CX400-01T    | 1 TB   | 8       | 262   | 0     | 0.72   |
| Kingston  | SEDC500R7680G      | 7.6 TB | 1       | 525   | 1     | 0.72   |
| SanDisk   | SD6SB2M512G1001    | 512 GB | 1       | 262   | 0     | 0.72   |
| Samsung   | SSD 850            | 120 GB | 43      | 262   | 0     | 0.72   |
| Apacer    | A7202              | 64 GB  | 1       | 262   | 0     | 0.72   |
| Toshiba   | TR200              | 480 GB | 22      | 262   | 0     | 0.72   |
| Samsung   | SSD 883 DCT        | 480 GB | 5       | 262   | 0     | 0.72   |
| Transcend | TS1TSSD220Q        | 1 TB   | 1       | 261   | 0     | 0.72   |
| Seagate   | ZA480NM10001       | 480 GB | 1       | 261   | 0     | 0.72   |
| Micron    | MTFDDAT128MAM-1J2  | 128 GB | 3       | 312   | 718   | 0.72   |
| Micron    | 1100_MTFDDAK1T0TBN | 1 TB   | 16      | 748   | 26    | 0.72   |
| Intel     | SSDSC2BW080A4      | 80 GB  | 9       | 263   | 1     | 0.72   |
| Samsung   | MZMTD128HAFV-000L1 | 128 GB | 15      | 272   | 10    | 0.72   |
| SK hynix  | SC313 HFS256G39... | 256 GB | 1       | 261   | 0     | 0.72   |
| Kingston  | RBU-SMSM151S324GD  | 24 GB  | 1       | 261   | 0     | 0.72   |
| SanDisk   | SDSSDH32000G       | 2 TB   | 8       | 260   | 0     | 0.71   |
| Kingmax   | SSD                | 480 GB | 3       | 260   | 0     | 0.71   |
| TrekStor  | TREKSTORSSD256GB   | 250 GB | 1       | 260   | 0     | 0.71   |
| Samsung   | MZNTY128HDHP-000L1 | 128 GB | 16      | 260   | 0     | 0.71   |
| EAGET     | S500 SSD           | 128 GB | 1       | 259   | 0     | 0.71   |
| SanDisk   | SD5SG2256G1052E    | 256 GB | 5       | 392   | 1     | 0.71   |
| SanDisk   | SD9TN8W512G1001    | 512 GB | 1       | 258   | 0     | 0.71   |
| SanDisk   | SDSSDH3 1T02       | 1 TB   | 12      | 258   | 0     | 0.71   |
| ADATA     | SP580              | 240 GB | 6       | 258   | 0     | 0.71   |
| Samsung   | MZ7TY128HDHP-00000 | 128 GB | 4       | 257   | 0     | 0.71   |
| SK hynix  | HFS256G39TNF-N3A0A | 256 GB | 11      | 257   | 0     | 0.71   |
| Samsung   | SSD PM810 TM       | 64 GB  | 1       | 257   | 0     | 0.70   |
| Micron    | C400-MTFDDAK256MAM | 256 GB | 4       | 334   | 758   | 0.70   |
| Toshiba   | THNSNJ256GMCU      | 256 GB | 8       | 256   | 0     | 0.70   |
| Drevo     | X1 Pro             | 512 GB | 1       | 255   | 0     | 0.70   |
| WDC       | WDS200T2B0B-00YS70 | 2 TB   | 25      | 255   | 0     | 0.70   |
| OCZ       | VERTEX2            | 100 GB | 3       | 255   | 0     | 0.70   |
| SanDisk   | SD9SB8W256G1002    | 256 GB | 1       | 254   | 0     | 0.70   |
| Samsung   | SSD 860 EVO        | 2 TB   | 83      | 254   | 0     | 0.70   |
| SK hynix  | SC401 SATA         | 256 GB | 8       | 254   | 0     | 0.70   |
| Patriot   | Burst              | 480 GB | 44      | 265   | 1     | 0.70   |
| HP        | SSD S700 Pro       | 512 GB | 3       | 254   | 0     | 0.70   |
| Intenso   | SATA3 240GB SSD    | 240 GB | 2       | 253   | 0     | 0.69   |
| Corsair   | Force LE SSD       | 120 GB | 4       | 253   | 0     | 0.69   |
| China     | LS 256G M300       | 256 GB | 1       | 252   | 0     | 0.69   |
| Samsung   | SSD 860 QVO        | 1 TB   | 240     | 253   | 1     | 0.69   |
| Apple     | SSD SD128E         | 121 GB | 3       | 252   | 0     | 0.69   |
| China     | 256GB SATA SSD     | 256 GB | 2       | 252   | 0     | 0.69   |
| Team      | T2535T240G         | 240 GB | 3       | 251   | 0     | 0.69   |
| Intel     | SSDSC2MH250A2      | 250 GB | 1       | 251   | 0     | 0.69   |
| Lite-On   | IT LCS-128L9S-HP   | 128 GB | 12      | 251   | 0     | 0.69   |
| Lite-On   | IT L8T-256L9G      | 256 GB | 1       | 251   | 0     | 0.69   |
| Intel     | SSDSCKJW180H6      | 180 GB | 3       | 250   | 0     | 0.69   |
| Team      | T253TD001T         | 1 TB   | 3       | 250   | 0     | 0.69   |
| WDC       | WDS100T2B0A        | 1 TB   | 9       | 257   | 1     | 0.69   |
| Gigabyte  | GP-GSTFS31120GNTD  | 120 GB | 35      | 249   | 0     | 0.68   |
| WDC       | WDS120G1G0A-00SS50 | 120 GB | 47      | 249   | 0     | 0.68   |
| Samsung   | MZNTE128HMGR-000L1 | 128 GB | 1       | 248   | 0     | 0.68   |
| Samsung   | MZMTD256HAGM-000L1 | 256 GB | 4       | 248   | 0     | 0.68   |
| Samsung   | SSD 860 QVO        | 4 TB   | 10      | 248   | 0     | 0.68   |
| SanDisk   | SD9SN8W256G1009    | 256 GB | 1       | 496   | 1     | 0.68   |
| Samsung   | SSD 860 PRO        | 4 TB   | 5       | 247   | 0     | 0.68   |
| Seagate   | SSD                | 1 TB   | 4       | 247   | 0     | 0.68   |
| Samsung   | MZMTE256HMHP-000L1 | 256 GB | 5       | 247   | 0     | 0.68   |
| SPCC      | M.2 SSD            | 256 GB | 6       | 246   | 0     | 0.68   |
| HP        | SSD S700           | 120 GB | 8       | 334   | 6     | 0.68   |
| OCZ       | CACHE-SYNAPSE      | 32 GB  | 2       | 246   | 0     | 0.68   |
| Micron    | MTFDDAK256TBN-1... | 256 GB | 10      | 293   | 2     | 0.67   |
| Pioneer   | APS-SL3N-512       | 512 GB | 5       | 246   | 0     | 0.67   |
| SanDisk   | SD6SN1M-256G-1006  | 256 GB | 7       | 346   | 1     | 0.67   |
| Goodram   | C50                | 120 GB | 4       | 245   | 0     | 0.67   |
| SK hynix  | HFS256G39TNH-73A0A | 256 GB | 5       | 245   | 357   | 0.67   |
| Team      | L3 SSD             | 240 GB | 1       | 244   | 0     | 0.67   |
| SanDisk   | SD8SN8U128G1001    | 128 GB | 12      | 244   | 0     | 0.67   |
| Intel     | SSDSA1MH080G1GN    | 80 GB  | 1       | 244   | 0     | 0.67   |
| Corsair   | Neutron XTI SSD    | 240 GB | 2       | 244   | 0     | 0.67   |
| Lite-On   | LCS-256L9S-11 2... | 256 GB | 11      | 243   | 0     | 0.67   |
| Kingston  | RBU-SNS8152S312... | 128 GB | 4       | 243   | 0     | 0.67   |
| Transcend | TS240GSSD220S      | 240 GB | 32      | 263   | 1     | 0.67   |
| Team      | TM8PS7128G         | 128 GB | 1       | 242   | 0     | 0.67   |
| Kingston  | SA400S37 120G      | 120 GB | 1       | 242   | 0     | 0.66   |
| Crucial   | CT960BX500SSD1     | 960 GB | 31      | 242   | 0     | 0.66   |
| SanDisk   | SSD U100           | 128 GB | 15      | 313   | 20    | 0.66   |
| Samsung   | Portable SSD T5    | 2 TB   | 8       | 242   | 0     | 0.66   |
| minisf... | SSD                | 256 GB | 2       | 241   | 0     | 0.66   |
| Phison    | SATA SSD           | 64 GB  | 4       | 241   | 0     | 0.66   |
| QUMO      | SATA SSD           | 256 GB | 1       | 241   | 0     | 0.66   |
| G.Skill   | FM-25S3-120GBP3    | 120 GB | 1       | 241   | 0     | 0.66   |
| WDC       | WDS200T2G0A-00JH30 | 2 TB   | 3       | 359   | 1     | 0.66   |
| Zheino    | CHN25SATAS1 128    | 128 GB | 1       | 722   | 2     | 0.66   |
| Innodisk  | 2.5" SATA SSD 3ME4 | 128 GB | 3       | 240   | 0     | 0.66   |
| PNY       | SSD2SC240G1SA75... | 240 GB | 4       | 240   | 0     | 0.66   |
| ADATA     | IM2S3138E-128GM-B  | 128 GB | 7       | 320   | 13    | 0.66   |
| Patriot   | Burst              | 960 GB | 12      | 239   | 0     | 0.66   |
| ADATA     | XM21E              | 32 GB  | 1       | 239   | 0     | 0.66   |
| HP        | VK0240GDJXU        | 240 GB | 1       | 238   | 0     | 0.65   |
| Plextor   | PX-512M5P          | 512 GB | 1       | 238   | 0     | 0.65   |
| Zheino    | CHN-25SATAA3-480   | 480 GB | 2       | 238   | 0     | 0.65   |
| Seagate   | BarraCuda 120 S... | 500 GB | 17      | 238   | 0     | 0.65   |
| Smartbuy  | SSD                | 64 GB  | 27      | 238   | 0     | 0.65   |
| Phison    | SATA SSD           | 128 GB | 8       | 237   | 0     | 0.65   |
| Gigaby... | GP-GSTFS30256GTTD  | 256 GB | 2       | 237   | 0     | 0.65   |
| AMD       | R3SL240G           | 240 GB | 11      | 316   | 24    | 0.65   |
| Super ... | FTM1TN325H         | 1 TB   | 1       | 236   | 0     | 0.65   |
| SanDisk   | X600 M.2 2280 SATA | 128 GB | 19      | 236   | 0     | 0.65   |
| Kingston  | SUV500120G         | 120 GB | 32      | 249   | 4     | 0.65   |
| Plextor   | PH6-CE240-L1       | 240 GB | 2       | 236   | 0     | 0.65   |
| China     | SATA SSD           | 1 TB   | 15      | 236   | 0     | 0.65   |
| Apacer    | AS350              | 480 GB | 5       | 235   | 0     | 0.64   |
| Verbatim  | SATA-III SSD       | 128 GB | 2       | 279   | 508   | 0.64   |
| Lite-On   | PH4-CE240          | 240 GB | 2       | 235   | 0     | 0.64   |
| Samsung   | Portable SSD T5    | 500 GB | 51      | 234   | 0     | 0.64   |
| Intel     | SSDSCKHF240A4L     | 240 GB | 3       | 272   | 370   | 0.64   |
| Crucial   | CT525MX300SSD4     | 528 GB | 24      | 300   | 77    | 0.64   |
| Patriot   | Spark              | 128 GB | 9       | 234   | 0     | 0.64   |
| Corsair   | Force LS SSD       | 64 GB  | 31      | 378   | 134   | 0.64   |
| SanDisk   | SDSSDH3512G        | 512 GB | 39      | 233   | 0     | 0.64   |
| Crucial   | CT240BX300SSD1     | 240 GB | 10      | 233   | 0     | 0.64   |
| Samsung   | MZMPC256HBGJ-00000 | 256 GB | 2       | 233   | 0     | 0.64   |
| Micron    | MTFDDAK480TDS      | 480 GB | 2       | 232   | 0     | 0.64   |
| Intel     | SSDSA2M120G2GC     | 120 GB | 2       | 1424  | 6     | 0.64   |
| Mushkin   | MKNSSDSR250GB-D8   | 250 GB | 1       | 232   | 0     | 0.64   |
| ADATA     | SU655              | 120 GB | 12      | 232   | 0     | 0.64   |
| SanDisk   | SSD i100           | 24 GB  | 32      | 257   | 33    | 0.64   |
| SPCC      | SSD                | 120 GB | 176     | 285   | 89    | 0.64   |
| Crucial   | CT960BX200SSD1     | 960 GB | 3       | 231   | 0     | 0.63   |
| ADATA     | SU800NS38          | 128 GB | 12      | 231   | 0     | 0.63   |
| ADATA     | SSD                | 32 GB  | 2       | 388   | 8     | 0.63   |
| Kingston  | SKC300S37A120G     | 120 GB | 24      | 232   | 1     | 0.63   |
| PNY       | CS900 960GB SSD    | 960 GB | 17      | 230   | 0     | 0.63   |
| GAMER     | L TA1D0120A        | 120 GB | 1       | 230   | 0     | 0.63   |
| LVCARDS   | SSD128G            | 128 GB | 1       | 229   | 0     | 0.63   |
| China     | 120GB SSD          | 120 GB | 61      | 228   | 0     | 0.63   |
| TCSUNBOW  | X3                 | 1 TB   | 5       | 228   | 0     | 0.63   |
| SK hynix  | HFS128G3BMND-3210A | 128 GB | 4       | 228   | 0     | 0.63   |
| PNY       | CS900 480GB SSD    | 480 GB | 35      | 228   | 0     | 0.63   |
| SanDisk   | SSD i110           | 64 GB  | 2       | 228   | 0     | 0.62   |
| ADATA     | AXNS381E-256GM-B   | 256 GB | 6       | 272   | 73    | 0.62   |
| Crucial   | CT250MX500SSD4N    | 250 GB | 3       | 227   | 0     | 0.62   |
| Transcend | TS128GMSA340       | 128 GB | 1       | 227   | 0     | 0.62   |
| Kingston  | RBU-SNS8152S325... | 256 GB | 7       | 293   | 2     | 0.62   |
| Intel     | SSDSC2KG480G8      | 480 GB | 3       | 227   | 0     | 0.62   |
| Intel     | SSDSCKKF128G8L     | 128 GB | 1       | 227   | 0     | 0.62   |
| SanDisk   | X300 MSATA         | 128 GB | 2       | 227   | 0     | 0.62   |
| Samsung   | MMCRE28G5MXP-MVB   | 128 GB | 1       | 226   | 0     | 0.62   |
| KingSpec  | NT-480             | 480 GB | 1       | 226   | 0     | 0.62   |
| Phison    | SATA SSD           | 240 GB | 18      | 226   | 0     | 0.62   |
| SanDisk   | SD6SF1M128GG56     | 128 GB | 1       | 226   | 0     | 0.62   |
| Samsung   | MZNTE512HMJH-000L1 | 512 GB | 1       | 225   | 0     | 0.62   |
| Toshiba   | THNSNH128GMCT      | 128 GB | 6       | 225   | 0     | 0.62   |
| BlitzWolf | BW-D1              | 120 GB | 1       | 225   | 0     | 0.62   |
| Goodram   | IRP-SSDPR-S25C-256 | 256 GB | 4       | 225   | 0     | 0.62   |
| ADATA     | SU810NS38 SATA ... | 128 GB | 5       | 225   | 0     | 0.62   |
| BHT       | WR202HH032G E70... | 32 GB  | 6       | 224   | 0     | 0.61   |
| Seagate   | BarraCuda 120 S... | 1 TB   | 13      | 224   | 0     | 0.61   |
| Plextor   | PX-G512M6eA        | 512 GB | 1       | 224   | 0     | 0.61   |
| Samsung   | MMCQE28GFMUP-MVA   | 128 GB | 3       | 250   | 9     | 0.61   |
| Crucial   | FCCT256M4SSD1      | 256 GB | 2       | 223   | 0     | 0.61   |
| Intel     | SSDSC2BF240A4L     | 240 GB | 8       | 340   | 5     | 0.61   |
| Apacer    | AST280             | 480 GB | 1       | 223   | 0     | 0.61   |
| Kingston  | SVP200S37A90G      | 90 GB  | 2       | 223   | 0     | 0.61   |
| SanDisk   | SDSSDH3 4T00       | 4 TB   | 10      | 222   | 0     | 0.61   |
| Foxline   | FLSSD128X5SE       | 128 GB | 3       | 222   | 0     | 0.61   |
| Crucial   | CT480M500SSD1      | 480 GB | 17      | 1100  | 250   | 0.61   |
| Crucial   | CT500MX500SSD1N    | 500 GB | 1       | 222   | 0     | 0.61   |
| Crucial   | CT250MX500SSD1N    | 250 GB | 2       | 222   | 0     | 0.61   |
| Micron    | MTFDDAK1T0TBN-1... | 1 TB   | 2       | 222   | 0     | 0.61   |
| Phison    | S11-64G-PHISON-... | 64 GB  | 1       | 221   | 0     | 0.61   |
| HP        | SSD S700           | 500 GB | 36      | 233   | 1     | 0.61   |
| ASUS      | S-128G1BYB00LP     | 128 GB | 1       | 221   | 0     | 0.61   |
| SanDisk   | SDSSDA120G         | 120 GB | 169     | 229   | 20    | 0.61   |
| Mushkin   | MKNSSDS2960GB      | 960 GB | 1       | 220   | 0     | 0.60   |
| SanDisk   | SSD i100           | 16 GB  | 11      | 239   | 2     | 0.60   |
| Intel     | SSDSC2KB240G8      | 240 GB | 15      | 220   | 0     | 0.60   |
| WDC       | WDS100T2B0B        | 1 TB   | 8       | 220   | 0     | 0.60   |
| Samsung   | MZMTD128HAFV-000   | 128 GB | 8       | 220   | 0     | 0.60   |
| Micron    | 5100_MTFDDAV960TBY | 960 GB | 2       | 219   | 0     | 0.60   |
| OCZ       | AGILITY4           | 256 GB | 10      | 415   | 36    | 0.60   |
| Toshiba   | A100               | 120 GB | 8       | 219   | 0     | 0.60   |
| Toshiba   | THNSNJ128GVNU      | 128 GB | 3       | 219   | 0     | 0.60   |
| Toshiba   | TR200              | 240 GB | 66      | 218   | 0     | 0.60   |
| Pioneer   | APS-SL3N-256       | 256 GB | 3       | 218   | 0     | 0.60   |
| Team      | L7 EVO SSD         | 120 GB | 2       | 218   | 0     | 0.60   |
| Intel     | SSDSC2BW180H6      | 180 GB | 4       | 235   | 1     | 0.60   |
| WDC       | WDS250G2B0A-00SM50 | 250 GB | 102     | 218   | 0     | 0.60   |
| Samsung   | MZNTE128HMGR-000SO | 128 GB | 2       | 379   | 773   | 0.60   |
| Samsung   | MMDPE56GFDXP-MVB   | 256 GB | 1       | 218   | 0     | 0.60   |
| WDC       | WDS500G2B0B        | 500 GB | 12      | 218   | 0     | 0.60   |
| OCZ       | VERTEX             | 96 GB  | 1       | 217   | 0     | 0.60   |
| SanDisk   | SD8SN8U256G1002    | 256 GB | 10      | 217   | 0     | 0.60   |
| Micron    | 5100_MTFDDAK960TBY | 960 GB | 1       | 217   | 0     | 0.59   |
| ADATA     | XM13               | 32 GB  | 2       | 216   | 0     | 0.59   |
| Samsung   | MZHPU256HCGL-00005 | 256 GB | 1       | 216   | 0     | 0.59   |
| Transcend | TS128GSSD340K      | 128 GB | 1       | 216   | 0     | 0.59   |
| TCSUNBOW  | N4                 | 120 GB | 1       | 216   | 0     | 0.59   |
| WDC       | WDS200T2B0A-00SM50 | 2 TB   | 26      | 243   | 39    | 0.59   |
| SK hynix  | HFS128G39MNC-3510A | 128 GB | 3       | 216   | 0     | 0.59   |
| SanDisk   | SSD PLUS 120 GB    | 120 GB | 47      | 296   | 2     | 0.59   |
| Samsung   | Portable SSD T5    | 1 TB   | 39      | 215   | 0     | 0.59   |
| Crucial   | CT250MX200SSD4     | 250 GB | 1       | 215   | 0     | 0.59   |
| ADATA     | SU900              | 512 GB | 7       | 215   | 0     | 0.59   |
| SanDisk   | SDSA6GM-032G-1006  | 32 GB  | 1       | 215   | 0     | 0.59   |
| SK hynix  | SC308 SATA         | 256 GB | 16      | 261   | 7     | 0.59   |
| Intel     | SSDSC2CW060A3      | 64 GB  | 18      | 575   | 565   | 0.59   |
| Samsung   | MZMTD128HAFV-00007 | 128 GB | 1       | 214   | 0     | 0.59   |
| SanDisk   | SD7SB6S256G1122    | 256 GB | 3       | 214   | 0     | 0.59   |
| Kingston  | SUV500M8120G       | 120 GB | 10      | 214   | 0     | 0.59   |
| Transcend | TSA                | 1 TB   | 2       | 214   | 0     | 0.59   |
| SanDisk   | SD8SB8U128G1002    | 128 GB | 2       | 214   | 0     | 0.59   |
| Lite-On   | LAT-128M2S         | 128 GB | 2       | 369   | 4     | 0.59   |
| Samsung   | MZNLN256HAJQ-00000 | 256 GB | 16      | 214   | 0     | 0.59   |
| SanDisk   | SD8TN8U256G1001    | 256 GB | 16      | 213   | 0     | 0.59   |
| Plextor   | PX-128S3G          | 128 GB | 5       | 213   | 0     | 0.58   |
| Hoodisk   | SSD                | 128 GB | 12      | 213   | 0     | 0.58   |
| China     | M.2 2280 SATA SSD  | 256 GB | 4       | 213   | 0     | 0.58   |
| Wibtek    | W800S 512GB SSD    | 512 GB | 1       | 213   | 0     | 0.58   |
| Goodram   | SSDPR-CX300-240    | 240 GB | 9       | 213   | 0     | 0.58   |
| Kingston  | SV300S37A480G      | 480 GB | 34      | 308   | 50    | 0.58   |
| Dogfish   | SSD 256G           | 256 GB | 1       | 212   | 0     | 0.58   |
| Samsung   | MZ7LF120HCHP-000L1 | 120 GB | 6       | 211   | 0     | 0.58   |
| Drevo     | X1                 | 120 GB | 3       | 302   | 677   | 0.58   |
| Crucial   | CT500MX500SSD4     | 500 GB | 58      | 211   | 0     | 0.58   |
| SMI       | SSD                | 256 GB | 1       | 211   | 0     | 0.58   |
| Samsung   | SSD PM810 FDE 2.5" | 256 GB | 3       | 481   | 317   | 0.58   |
| Intel     | SSDSC2KF256G8 SATA | 256 GB | 2       | 210   | 0     | 0.58   |
| SanDisk   | SD7SN6S-128G-1006  | 128 GB | 4       | 210   | 0     | 0.58   |
| ADATA     | SSD DP900 128GB... | 128 GB | 5       | 746   | 613   | 0.58   |
| MyDigi... | SB2                | 240 GB | 6       | 209   | 0     | 0.57   |
| PNY       | SSD2SC240G5SA75... | 240 GB | 2       | 209   | 0     | 0.57   |
| Kingston  | SKC380S3480G       | 480 GB | 1       | 208   | 0     | 0.57   |
| Samsung   | MMCRE28GQDXP-MVB   | 64 GB  | 6       | 208   | 0     | 0.57   |
| Samsung   | SSD 860 EVO M.2    | 250 GB | 84      | 208   | 0     | 0.57   |
| OCZ       | VERTEX2            | 50 GB  | 2       | 309   | 320   | 0.57   |
| Mushkin   | MKNSSDSR1TB        | 1 TB   | 2       | 208   | 0     | 0.57   |
| Patriot   | Blaze              | 120 GB | 8       | 208   | 0     | 0.57   |
| WDC       | WDS500G2B0A-00SM50 | 500 GB | 317     | 208   | 1     | 0.57   |
| SanDisk   | SD8TN8U512G1001    | 512 GB | 4       | 207   | 0     | 0.57   |
| Team      | L5 SSD             | 120 GB | 1       | 207   | 0     | 0.57   |
| Intel     | SSDMCEAC180B3      | 180 GB | 3       | 207   | 0     | 0.57   |
| Kingston  | SUV400S37-120G     | 120 GB | 1       | 207   | 0     | 0.57   |
| Lite-On   | LMT-128L9M-11 M... | 128 GB | 1       | 207   | 0     | 0.57   |
| Palit     | PH120 SSD          | 120 GB | 1       | 207   | 0     | 0.57   |
| SanDisk   | SSD G5 BICS4       | 500 GB | 36      | 207   | 0     | 0.57   |
| GALAX     | TA1D0120A          | 120 GB | 6       | 206   | 0     | 0.57   |
| Samsung   | SSD 860 EVO M.2    | 500 GB | 105     | 212   | 1     | 0.57   |
| SanDisk   | SSD U100           | 16 GB  | 23      | 206   | 0     | 0.57   |
| Samsung   | MZMPA024HMCD-000L1 | 24 GB  | 4       | 233   | 5     | 0.57   |
| Smartbuy  | m.2 S10-2280T      | 128 GB | 1       | 206   | 0     | 0.57   |
| JAMESD... | JD240LE            | 240 GB | 1       | 206   | 0     | 0.56   |
| Seagate   | ST240HM000         | 240 GB | 1       | 206   | 0     | 0.56   |
| Kingston  | SS050S216G         | 16 GB  | 1       | 205   | 0     | 0.56   |
| Mushkin   | MKNSSDRE1TB        | 1 TB   | 6       | 204   | 0     | 0.56   |
| Kingston  | RBUSNS4180S3256GJ  | 256 GB | 1       | 204   | 0     | 0.56   |
| Silicon   | SATA3 256GB SSD    | 256 GB | 1       | 204   | 0     | 0.56   |
| Samsung   | MZNTE512HMJH-00000 | 512 GB | 1       | 204   | 0     | 0.56   |
| SPCC      | SSD B29            | 32 GB  | 1       | 204   | 0     | 0.56   |
| PNY       | CS900 240GB SSD    | 240 GB | 114     | 204   | 0     | 0.56   |
| Micron    | MTFDBAK128MAG-1G1  | 128 GB | 3       | 204   | 0     | 0.56   |
| WDC       | PC SA530 SDASB8... | 512 GB | 1       | 203   | 0     | 0.56   |
| KingSpec  | MT-512             | 512 GB | 2       | 203   | 0     | 0.56   |
| Samsung   | MZMTE128HMGR-000   | 128 GB | 2       | 203   | 0     | 0.56   |
| SanDisk   | SD9SN8W256G1102    | 256 GB | 25      | 203   | 0     | 0.56   |
| Smartbuy  | m.2 S11-2280S      | 128 GB | 1       | 202   | 0     | 0.56   |
| China     | L06B B0KB          | 960 GB | 1       | 202   | 0     | 0.55   |
| Lexar     | 480GB SSD          | 480 GB | 2       | 201   | 0     | 0.55   |
| Quaroni   | QSSDS25240G        | 240 GB | 1       | 201   | 0     | 0.55   |
| Intel     | SSDSC2BB480G7K     | 480 GB | 1       | 201   | 0     | 0.55   |
| SanDisk   | SD8SN8U-128G-1006  | 128 GB | 50      | 232   | 83    | 0.55   |
| WDC       | WDS100T2B0B-00YS70 | 1 TB   | 66      | 209   | 1     | 0.55   |
| Plextor   | PH6-CE120          | 120 GB | 12      | 201   | 0     | 0.55   |
| Kingston  | SVP180S2256G       | 256 GB | 1       | 200   | 0     | 0.55   |
| V-GeN     | SSD                | 240 GB | 1       | 200   | 0     | 0.55   |
| SanDisk   | SD5SF2128G1014E    | 128 GB | 2       | 200   | 0     | 0.55   |
| Crucial   | CT256M225          | 256 GB | 1       | 200   | 0     | 0.55   |
| China     | PSX-NGFF256G       | 256 GB | 1       | 199   | 0     | 0.55   |
| Kingston  | SUV500240G         | 240 GB | 52      | 204   | 24    | 0.55   |
| WDC       | WDS500G2B0B-00YS70 | 500 GB | 126     | 207   | 9     | 0.55   |
| Samsung   | MZ7LN128HAHQ-000H1 | 128 GB | 2       | 199   | 0     | 0.55   |
| SanDisk   | SD9SN8W512G1102    | 512 GB | 3       | 199   | 0     | 0.55   |
| Kingston  | RBUSNS8180S3512GJ  | 512 GB | 3       | 199   | 0     | 0.55   |
| ADATA     | SP920SS            | 128 GB | 10      | 442   | 8     | 0.54   |
| WDC       | WDS100T2B0A-00SM50 | 1 TB   | 201     | 202   | 1     | 0.54   |
| ADATA     | SU900              | 1 TB   | 4       | 199   | 1     | 0.54   |
| Patriot   | Burst              | 240 GB | 99      | 198   | 0     | 0.54   |
| China     | 256GB PCS 2.5" SSD | 256 GB | 3       | 197   | 0     | 0.54   |
| China     | SATA SSD           | 128 GB | 25      | 196   | 0     | 0.54   |
| Crucial   | M4-CT512M4SSD1     | 512 GB | 4       | 516   | 77    | 0.54   |
| Team      | T253X6001T         | 1 TB   | 3       | 196   | 0     | 0.54   |
| JIESHUO   | SSD                | 256 GB | 1       | 196   | 0     | 0.54   |
| Micron    | 5200_MTFDDAK960TDN | 960 GB | 1       | 195   | 0     | 0.54   |
| Smartbuy  | SSD                | 480 GB | 2       | 195   | 0     | 0.54   |
| tigo      | SSD E300           | 64 GB  | 1       | 195   | 0     | 0.54   |
| SanDisk   | SD9SB8W512G1101    | 512 GB | 5       | 195   | 0     | 0.54   |
| China     | SATA SSD           | 120 GB | 101     | 197   | 1     | 0.54   |
| Samsung   | MZ7LN256HAJQ-000L7 | 256 GB | 10      | 195   | 0     | 0.54   |
| SanDisk   | SD9SN8W256G1014    | 256 GB | 9       | 195   | 0     | 0.53   |
| Kingston  | SUV500M8480G       | 480 GB | 5       | 194   | 0     | 0.53   |
| Kingston  | RBU-SC100S37240GE  | 240 GB | 1       | 194   | 0     | 0.53   |
| SanDisk   | SDSSDA-2T00        | 2 TB   | 5       | 211   | 1     | 0.53   |
| Corsair   | CSSD-V60GB2        | 64 GB  | 3       | 323   | 6     | 0.53   |
| WDC       | WDS100T1R0A-68A4W0 | 1 TB   | 8       | 193   | 0     | 0.53   |
| Seagate   | BarraCuda SSD Z... | 1 TB   | 7       | 193   | 0     | 0.53   |
| SK hynix  | SHGS31-500GS-2     | 500 GB | 19      | 193   | 0     | 0.53   |
| SuperM... | SSD                | 64 GB  | 2       | 193   | 0     | 0.53   |
| SanDisk   | SSD U110           | 16 GB  | 38      | 195   | 3     | 0.53   |
| Vaseky    | V800-60G           | 64 GB  | 2       | 247   | 14    | 0.53   |
| Londisk   | SSD                | 960 GB | 1       | 192   | 0     | 0.53   |
| OCZ       | VERTEX460          | 240 GB | 6       | 350   | 5     | 0.53   |
| China     | mSATA              | 128 GB | 1       | 192   | 0     | 0.53   |
| Apacer    | AS510S             | 256 GB | 3       | 194   | 1     | 0.53   |
| Intenso   | SSD                | 256 GB | 26      | 192   | 0     | 0.53   |
| Seagate   | BarraCuda SSD Z... | 2 TB   | 3       | 192   | 0     | 0.53   |
| China     | SATA SSD           | 240 GB | 73      | 198   | 1     | 0.53   |
| China     | SATA3 512GB SSD    | 512 GB | 2       | 191   | 0     | 0.53   |
| Lite-On   | CV1-CC128-11 2.... | 128 GB | 1       | 191   | 0     | 0.53   |
| Samsung   | MZNTD128HAGM-00000 | 128 GB | 4       | 191   | 0     | 0.52   |
| Smartbuy  | SSD                | 120 GB | 92      | 198   | 1     | 0.52   |
| OCZ       | VERTEX4            | 512 GB | 1       | 573   | 2     | 0.52   |
| Lite-On   | L8H-256V2G-HP      | 256 GB | 14      | 191   | 0     | 0.52   |
| Samsung   | MZNTE256HMHP-000L2 | 256 GB | 6       | 190   | 0     | 0.52   |
| Kingston  | SS100S216G         | 16 GB  | 1       | 190   | 0     | 0.52   |
| Golden... | SSD 128            | 128 GB | 1       | 190   | 0     | 0.52   |
| WDC       | PC SA530 SDASB8... | 1 TB   | 3       | 190   | 0     | 0.52   |
| SK hynix  | SC210 mSATA        | 128 GB | 4       | 458   | 19    | 0.52   |
| Samsung   | MZNLN256HAJQ-000H1 | 256 GB | 32      | 195   | 7     | 0.52   |
| Crucial   | CT1000MX500SSD4    | 1 TB   | 51      | 189   | 0     | 0.52   |
| Micron    | 5300_MTFDDAK3T8TDT | 3.8 TB | 6       | 189   | 0     | 0.52   |
| Goodram   | SSDPR-CL100-960-G3 | 960 GB | 4       | 189   | 0     | 0.52   |
| Micron    | MTFDDAV512MBF-1... | 512 GB | 5       | 189   | 0     | 0.52   |
| ADATA     | SX900              | 256 GB | 11      | 670   | 483   | 0.52   |
| Integral  | V Series SATA SSD  | 120 GB | 3       | 189   | 0     | 0.52   |
| China     | 1TB QLC SATA SSD   | 1 TB   | 2       | 189   | 0     | 0.52   |
| China     | SH00R1TB           | 1 TB   | 1       | 189   | 0     | 0.52   |
| Intel     | SSDSC2BW360H6      | 360 GB | 1       | 566   | 2     | 0.52   |
| OCZ       | VERTEX460A         | 480 GB | 1       | 188   | 0     | 0.52   |
| Intenso   | SSD Sata III       | 240 GB | 8       | 188   | 0     | 0.52   |
| DERLER    | SSD                | 120 GB | 1       | 188   | 0     | 0.52   |
| LDLC      | F7+120GB           | 120 GB | 2       | 188   | 0     | 0.52   |
| Transcend | TS64GSSD370        | 64 GB  | 4       | 188   | 0     | 0.52   |
| Intel     | SSDSC2KW128G8      | 128 GB | 14      | 188   | 0     | 0.52   |
| Goodram   | SSDPR-CX300-120    | 120 GB | 13      | 188   | 0     | 0.52   |
| S3+       | S3SSDC480XEU       | 480 GB | 2       | 188   | 0     | 0.52   |
| Intel     | SSDSC2KB038T8R     | 3.8 TB | 1       | 188   | 0     | 0.52   |
| Kingston  | SNV425S264GB       | 64 GB  | 6       | 817   | 6     | 0.51   |
| KingFast  | SSD                | 240 GB | 8       | 187   | 0     | 0.51   |
| TCSUNBOW  | X5                 | 120 GB | 1       | 187   | 0     | 0.51   |
| Samsung   | SSD 860 EVO M.2    | 1 TB   | 65      | 188   | 1     | 0.51   |
| Samsung   | MZNLN512HAJQ-00007 | 512 GB | 2       | 186   | 0     | 0.51   |
| Kingston  | SA400S37480G       | 480 GB | 661     | 207   | 1     | 0.51   |
| Smartbuy  | mSata              | 64 GB  | 1       | 186   | 0     | 0.51   |
| Micron    | MTFDDAV480TCB-1... | 480 GB | 1       | 184   | 0     | 0.51   |
| SanDisk   | SDSSDH3500G        | 500 GB | 28      | 184   | 0     | 0.51   |
| Samsung   | SSD 860 EVO mSATA  | 250 GB | 27      | 184   | 0     | 0.51   |
| Samsung   | MZMTE512HMHP-00000 | 512 GB | 1       | 184   | 0     | 0.51   |
| Goodram   | SSDPR-CX400-512    | 512 GB | 21      | 184   | 0     | 0.51   |
| SanDisk   | SD5SE2256G1002E    | 256 GB | 4       | 183   | 0     | 0.50   |
| Plextor   | PX-256M5P          | 256 GB | 1       | 183   | 0     | 0.50   |
| LDLC      | SSD F7 PLUS 3D ... | 240 GB | 3       | 183   | 0     | 0.50   |
| Intel     | SSDSC2BF180A4L     | 180 GB | 15      | 227   | 4     | 0.50   |
| e2e4      | SSD                | 240 GB | 2       | 183   | 0     | 0.50   |
| Lexar     | SSD                | 120 GB | 2       | 182   | 0     | 0.50   |
| Kingston  | SA400S37960G       | 960 GB | 100     | 186   | 1     | 0.50   |
| Patriot   | Burst              | 120 GB | 107     | 182   | 0     | 0.50   |
| Dogfish   | SSD                | 2 TB   | 1       | 182   | 0     | 0.50   |
| Phison    | SSM28128GPTCB3B... | 128 GB | 1       | 182   | 0     | 0.50   |
| Intel     | SSDSCKGF180A4H     | 180 GB | 2       | 181   | 0     | 0.50   |
| Team      | T253X6256G         | 256 GB | 1       | 181   | 0     | 0.50   |
| SanDisk   | SD9SB8W512G        | 512 GB | 1       | 181   | 0     | 0.50   |
| Goodram   | IRIDIUM            | 480 GB | 3       | 181   | 0     | 0.50   |
| SanDisk   | SD9SN8W256G1002    | 256 GB | 14      | 181   | 0     | 0.50   |
| Vaseky    | V800-64G           | 64 GB  | 1       | 181   | 0     | 0.50   |
| Transcend | TS512GSSD370       | 512 GB | 5       | 181   | 0     | 0.50   |
| Lexar     | 120GB SSD          | 120 GB | 2       | 181   | 0     | 0.50   |
| Plextor   | PX-256M5S          | 256 GB | 17      | 267   | 113   | 0.50   |
| LDLC      | SSD                | 480 GB | 5       | 185   | 1     | 0.50   |
| Transcend | TS128GMSA740       | 128 GB | 1       | 180   | 0     | 0.50   |
| Kingch... | SSD                | 64 GB  | 2       | 180   | 0     | 0.49   |
| Goodram   | SSDPR-CX400-128    | 128 GB | 31      | 180   | 0     | 0.49   |
| Samsung   | MZNLN512HAJQ-00000 | 512 GB | 8       | 180   | 0     | 0.49   |
| Phison    | SATA SSD           | 480 GB | 11      | 179   | 0     | 0.49   |
| Seagate   | BarraCuda SSD Z... | 500 GB | 12      | 179   | 0     | 0.49   |
| China     | SATA SSD           | 64 GB  | 26      | 179   | 0     | 0.49   |
| DeTech    | SSD                | 120 GB | 3       | 179   | 0     | 0.49   |
| ADATA     | SU800              | 1 TB   | 34      | 201   | 19    | 0.49   |
| SanDisk   | SSD i110           | 32 GB  | 3       | 179   | 0     | 0.49   |
| ADATA     | SU635              | 240 GB | 28      | 185   | 38    | 0.49   |
| Toshiba   | KSG60ZSE256G SATA  | 256 GB | 3       | 435   | 67    | 0.49   |
| KingDian  | S370               | 128 GB | 1       | 178   | 0     | 0.49   |
| Apacer    | 8GB SATA Flash ... | 8 GB   | 4       | 186   | 52    | 0.49   |
| Maxtor    | Z1 SSD             | 480 GB | 5       | 177   | 0     | 0.49   |
| SK hynix  | HFS256G39TND-N210A | 256 GB | 69      | 288   | 133   | 0.49   |
| Transcend | TS256GSSD370       | 256 GB | 4       | 177   | 0     | 0.49   |
| Kingston  | SUV500MS240G       | 240 GB | 19      | 177   | 0     | 0.49   |
| SK hynix  | HFS128G32TND-N210A | 128 GB | 7       | 418   | 94    | 0.49   |
| KingDian  | S400 XT            | 240 GB | 1       | 177   | 0     | 0.49   |
| SPCC      | SSD A20            | 64 GB  | 2       | 177   | 0     | 0.49   |
| KingSpec  | P3-1TB             | 1 TB   | 7       | 177   | 0     | 0.49   |
| Crucial   | CT250MX500SSD1     | 250 GB | 213     | 177   | 10    | 0.48   |
| Kingston  | SUV500480G         | 480 GB | 19      | 200   | 157   | 0.48   |
| SK hynix  | HFS128G32TNF-N3A0A | 128 GB | 15      | 176   | 0     | 0.48   |
| SanDisk   | SDEZS25-240G-Z01   | 240 GB | 4       | 176   | 0     | 0.48   |
| ADATA     | AXNS381E-128GM-B   | 128 GB | 2       | 175   | 0     | 0.48   |
| OCZ       | VERTEX460          | 120 GB | 4       | 306   | 5     | 0.48   |
| Goodram   | SSDPR-CL100-240    | 240 GB | 4       | 174   | 0     | 0.48   |
| AGI       | AGI960G17AI178     | 960 GB | 2       | 174   | 0     | 0.48   |
| Kingston  | SA400S37120G       | 120 GB | 874     | 188   | 1     | 0.48   |
| Zheino    | CHN 25SATAA3 360   | 360 GB | 3       | 173   | 0     | 0.48   |
| Faspeed   | F510-120G          | 120 GB | 1       | 173   | 0     | 0.47   |
| Mushkin   | MKNSSDTR500GB      | 500 GB | 1       | 173   | 0     | 0.47   |
| KingFast  | SSD                | 512 GB | 13      | 173   | 0     | 0.47   |
| Vaseky    | V800-120GB         | 120 GB | 1       | 173   | 0     | 0.47   |
| Crucial   | CT500MX500SSD4N    | 500 GB | 3       | 172   | 0     | 0.47   |
| Kingston  | RBU-SNS4151S316GD1 | 16 GB  | 1       | 172   | 0     | 0.47   |
| INNOVA... | SSD                | 1 TB   | 3       | 171   | 0     | 0.47   |
| SanDisk   | SD9SN8W128G1014    | 128 GB | 2       | 171   | 0     | 0.47   |
| Seagate   | BarraCuda Q1 SS... | 480 GB | 3       | 171   | 0     | 0.47   |
| Lite-On   | CV3-8D256-41 SA... | 256 GB | 4       | 171   | 0     | 0.47   |
| Toshiba   | THNSNK128GVN8      | 128 GB | 11      | 171   | 0     | 0.47   |
| Crucial   | CT2000BX500SSD1    | 2 TB   | 27      | 170   | 0     | 0.47   |
| Lexar     | SSD                | 128 GB | 11      | 170   | 0     | 0.47   |
| Team      | TEAML5Lite3D240G   | 240 GB | 5       | 170   | 0     | 0.47   |
| KingDian  | S400               | 120 GB | 18      | 169   | 0     | 0.47   |
| China     | SV9SAT6B480GLM21DR | 480 GB | 1       | 169   | 0     | 0.47   |
| WDC       | WDS250G2B0A        | 250 GB | 14      | 169   | 0     | 0.46   |
| KingDian  | S280-240GB         | 240 GB | 16      | 194   | 232   | 0.46   |
| Vaseky    | V800-240G          | 240 GB | 4       | 169   | 0     | 0.46   |
| LDLC      | SSD                | 120 GB | 15      | 310   | 36    | 0.46   |
| Mushkin   | MKNSSDEC60GB       | 64 GB  | 1       | 169   | 0     | 0.46   |
| Plextor   | PX-128M5S          | 128 GB | 57      | 176   | 1     | 0.46   |
| SK hynix  | HFS512G39TNF-N3A0A | 512 GB | 2       | 168   | 0     | 0.46   |
| Intel     | SSDSA2CW300G3      | 304 GB | 5       | 168   | 0     | 0.46   |
| Goodram   | CX100              | 120 GB | 9       | 260   | 2     | 0.46   |
| Samsung   | MZNLN256HCHP-000L2 | 256 GB | 6       | 167   | 0     | 0.46   |
| SPCC      | SSD162             | 120 GB | 9       | 454   | 569   | 0.46   |
| Samsung   | SSD 860 PRO        | 512 GB | 61      | 167   | 0     | 0.46   |
| Gigabyte  | GP-GSTFS30256GTTD  | 256 GB | 3       | 167   | 0     | 0.46   |
| SanDisk   | SDLF1CRR-019T-1HA1 | 1.9 TB | 1       | 167   | 0     | 0.46   |
| Samsung   | MZNLN128HCGR-000H1 | 128 GB | 4       | 167   | 0     | 0.46   |
| Samsung   | MZNLN128HAHQ-000H1 | 128 GB | 65      | 169   | 21    | 0.46   |
| Smartbuy  | m.2 S11-2280       | 128 GB | 3       | 167   | 0     | 0.46   |
| Best M... | BT-480-535         | 480 GB | 1       | 167   | 0     | 0.46   |
| Smartbuy  | SSD                | 120 GB | 7       | 167   | 0     | 0.46   |
| Kingston  | SUV500MS480G       | 480 GB | 15      | 166   | 0     | 0.46   |
| Mushkin   | MKNSSDEC120GB      | 120 GB | 1       | 166   | 0     | 0.46   |
| ADATA     | SU800NS38          | 512 GB | 10      | 219   | 78    | 0.46   |
| Vaseky    | V800-120G          | 120 GB | 4       | 165   | 0     | 0.45   |
| Corsair   | Force LS SSD       | 240 GB | 3       | 348   | 505   | 0.45   |
| SK hynix  | HFS128G39TND-N210A | 128 GB | 73      | 224   | 88    | 0.45   |
| SanDisk   | SD6PP4M-256G-1006  | 256 GB | 10      | 281   | 11    | 0.45   |
| Micron    | MTFDDAK512MAM-1K1  | 512 GB | 4       | 418   | 717   | 0.45   |
| Intel     | SSDMAEMC080G2L     | 80 GB  | 2       | 569   | 7     | 0.45   |
| Phison    | SATA SSD           | 32 GB  | 1       | 165   | 0     | 0.45   |
| Dogfish   | SSD                | 64 GB  | 4       | 165   | 0     | 0.45   |
| ADATA     | SU900              | 256 GB | 10      | 214   | 24    | 0.45   |
| WDC       | WDS240G2G0B-00EPW0 | 240 GB | 188     | 183   | 1     | 0.45   |
| Ramaxel   | RTNTE256PCA8EADL   | 256 GB | 2       | 165   | 0     | 0.45   |
| Samsung   | MZNTE128HMGR-000H1 | 128 GB | 2       | 164   | 0     | 0.45   |
| Transcend | TS480GSSD220S      | 480 GB | 13      | 206   | 236   | 0.45   |
| China     | SATA SSD           | 32 GB  | 5       | 164   | 0     | 0.45   |
| Intel     | SSDSA2M080G2HP     | 80 GB  | 3       | 169   | 1     | 0.45   |
| PNY       | SSD2SC240G1CS17... | 240 GB | 5       | 164   | 0     | 0.45   |
| Corsair   | Force LE200 SSD    | 120 GB | 8       | 164   | 0     | 0.45   |
| SanDisk   | SSD PLUS 240 GB    | 240 GB | 37      | 232   | 6     | 0.45   |
| Samsung   | SSD 830 Series     | 56 GB  | 1       | 164   | 0     | 0.45   |
| Intel     | SSDSC2KI128G8      | 128 GB | 2       | 163   | 0     | 0.45   |
| GLOWAY    | STK720GS3-S7       | 720 GB | 1       | 163   | 0     | 0.45   |
| Intel     | SSDSC2BW480A4      | 480 GB | 10      | 634   | 19    | 0.45   |
| Gigabyte  | GP-GSTFS31240GNTD  | 240 GB | 20      | 163   | 0     | 0.45   |
| WDC       | WDS500G1R0A-68A4W0 | 500 GB | 10      | 163   | 0     | 0.45   |
| Toshiba   | KSG60ZMV512G M.... | 512 GB | 9       | 162   | 0     | 0.45   |
| V-GeN     | V-GEN02SM19EG51... | 512 GB | 1       | 162   | 0     | 0.45   |
| Transcend | TS120GSSD220S      | 120 GB | 29      | 167   | 1     | 0.44   |
| Kingston  | SV100S2128G        | 128 GB | 4       | 512   | 3     | 0.44   |
| Kingston  | SA400S37240G       | 240 GB | 1269    | 172   | 1     | 0.44   |
| GeIL      | ZENITH 240G R3     | 240 GB | 1       | 161   | 0     | 0.44   |
| China     | 128GB SSD          | 128 GB | 22      | 161   | 0     | 0.44   |
| Toshiba   | VT180              | 240 GB | 1       | 161   | 0     | 0.44   |
| Intel     | SSDMAEXC024G3H     | 24 GB  | 3       | 197   | 10    | 0.44   |
| Samsung   | SSD EVO 360G       | 360 GB | 1       | 161   | 0     | 0.44   |
| Lite-On   | CV3-CE256-11 SATA  | 256 GB | 5       | 161   | 0     | 0.44   |
| GeIL      | ZENITH R3_120GB    | 120 GB | 3       | 160   | 0     | 0.44   |
| KingDian  | S280               | 480 GB | 9       | 160   | 0     | 0.44   |
| UNIC2     | S100-480           | 480 GB | 5       | 160   | 0     | 0.44   |
| INNOVA... | SSD_M.2_512GB_I... | 512 GB | 1       | 159   | 0     | 0.44   |
| Kingston  | OM8P0S3512F-00     | 512 GB | 3       | 159   | 0     | 0.44   |
| BAITITON  | BT58SSD09S         | 240 GB | 5       | 252   | 1     | 0.44   |
| Mushkin   | MKNSSDSR1TB-D8     | 1 TB   | 1       | 159   | 0     | 0.44   |
| Crucial   | CT500MX500SSD1     | 500 GB | 518     | 161   | 1     | 0.44   |
| Crucial   | CT1000MX500SSD1    | 1 TB   | 501     | 161   | 3     | 0.44   |
| WDC       | WDS500G1R0B-68A4Z0 | 500 GB | 6       | 159   | 0     | 0.44   |
| Samsung   | MZNLN256HMHQ-000H7 | 256 GB | 4       | 159   | 0     | 0.44   |
| Transcend | TS120GMTS820S      | 120 GB | 6       | 159   | 0     | 0.44   |
| SK hynix  | HFS128G3BTND-N210A | 128 GB | 4       | 229   | 2     | 0.44   |
| WDC       | WDBNCE5000PNC      | 500 GB | 51      | 159   | 0     | 0.44   |
| Plextor   | PX-256M5M          | 256 GB | 4       | 158   | 0     | 0.44   |
| Corsair   | Force LS SSD       | 120 GB | 18      | 419   | 428   | 0.43   |
| Crucial   | CT3500SC 8         | 500 GB | 2       | 279   | 7     | 0.43   |
| Goodram   | SSDPR-CL100-240-G2 | 240 GB | 10      | 158   | 0     | 0.43   |
| ADATA     | AXNS381E-128GM-B2  | 128 GB | 1       | 158   | 0     | 0.43   |
| Team      | TEAML5Lite3D480G   | 480 GB | 3       | 158   | 0     | 0.43   |
| Ramsta    | SSD S600           | 480 GB | 1       | 158   | 0     | 0.43   |
| PNY       | SSD2SC240G1CS11... | 240 GB | 1       | 158   | 0     | 0.43   |
| TAMMUZ    | SSD                | 512 GB | 1       | 157   | 0     | 0.43   |
| Phison    | SATA SSD           | 120 GB | 43      | 157   | 0     | 0.43   |
| Kingston  | RBUSC180S37256GJ   | 256 GB | 5       | 157   | 0     | 0.43   |
| GeIL      | ZENITH R3_240GB    | 240 GB | 1       | 157   | 0     | 0.43   |
| Silicon   | SATA3 120GB SSD    | 120 GB | 2       | 157   | 0     | 0.43   |
| SPCC      | SSD                | 512 GB | 82      | 187   | 44    | 0.43   |
| Samgporse | SP-8 PRO           | 1 TB   | 1       | 156   | 0     | 0.43   |
| Kingmax   | SSD                | 120 GB | 33      | 297   | 249   | 0.43   |
| China     | SATA3 2TB SSD      | 2 TB   | 4       | 156   | 0     | 0.43   |
| Londisk   | SSD                | 120 GB | 10      | 156   | 0     | 0.43   |
| tigo      | SSD                | 120 GB | 2       | 155   | 0     | 0.43   |
| Vaseky    | V900-128G          | 128 GB | 2       | 155   | 0     | 0.43   |
| Intel     | SSDSCKJF180A5H REF | 180 GB | 3       | 155   | 0     | 0.43   |
| SanDisk   | SDSSDH3 1T00       | 1 TB   | 53      | 156   | 1     | 0.43   |
| Team      | T253LE240G         | 240 GB | 4       | 155   | 0     | 0.43   |
| SPCC      | SSD                | 55 GB  | 12      | 391   | 424   | 0.42   |
| ADATA     | SP550              | 960 GB | 1       | 154   | 0     | 0.42   |
| Samsung   | MZ7LM480HMHQ-00005 | 480 GB | 1       | 154   | 0     | 0.42   |
| SanDisk   | SD7SB7S010T1122    | 1 TB   | 1       | 154   | 0     | 0.42   |
| SPCC      | SSD                | 1 TB   | 49      | 160   | 1     | 0.42   |
| Lite-On   | CV3-CE128-HP       | 128 GB | 1       | 154   | 0     | 0.42   |
| KingDian  | S400               | 240 GB | 1       | 154   | 0     | 0.42   |
| Kingston  | SA400M8240G        | 240 GB | 77      | 154   | 0     | 0.42   |
| SanDisk   | SSD PLUS           | 120 GB | 101     | 160   | 5     | 0.42   |
| Goodram   | SSDPR-S400U-240-80 | 240 GB | 3       | 153   | 0     | 0.42   |
| Plextor   | PX-256S2C          | 256 GB | 2       | 153   | 0     | 0.42   |
| Hikvision | HS-SSD-E100N 256G  | 256 GB | 3       | 153   | 0     | 0.42   |
| Kingston  | AS400S37-120GB     | 120 GB | 1       | 153   | 0     | 0.42   |
| Toshiba   | Q300               | 960 GB | 1       | 153   | 0     | 0.42   |
| ADTEC     | ADC-S25D1S-2TB     | 1.9 TB | 2       | 152   | 0     | 0.42   |
| INNOVA... | SSD                | 240 GB | 3       | 152   | 0     | 0.42   |
| SanDisk   | X400 2.5 7MM       | 128 GB | 2       | 152   | 0     | 0.42   |
| Palit     | UVS                | 120 GB | 3       | 152   | 0     | 0.42   |
| Teclast   | 256GB NA850-2280   | 256 GB | 2       | 152   | 0     | 0.42   |
| LDLC      | F7+480GB           | 480 GB | 5       | 152   | 0     | 0.42   |
| Zheino    | CHN 25SATAS3 128   | 128 GB | 1       | 151   | 0     | 0.42   |
| Team      | T253X2001T         | 1 TB   | 10      | 151   | 0     | 0.42   |
| T-FORCE   | SSD                | 250 GB | 3       | 151   | 0     | 0.42   |
| Apple     | SSD SM128C         | 121 GB | 5       | 269   | 12    | 0.41   |
| Samsung   | MZNLN128HAHQ-000L1 | 128 GB | 3       | 151   | 0     | 0.41   |
| SanDisk   | SD7SB3Q256G1002    | 256 GB | 5       | 303   | 12    | 0.41   |
| Crucial   | FCCT512MX100SSD1   | 512 GB | 1       | 151   | 0     | 0.41   |
| Samsung   | SSD PM800 TH       | 64 GB  | 2       | 151   | 0     | 0.41   |
| Silico... | AAR256GS122221030  | 256 GB | 1       | 151   | 0     | 0.41   |
| Corsair   | Performance Pro    | 128 GB | 3       | 492   | 408   | 0.41   |
| Mushkin   | MKNSSDEC512GB      | 512 GB | 4       | 150   | 0     | 0.41   |
| ADATA     | SU800              | 128 GB | 52      | 185   | 3     | 0.41   |
| PNY       | EU SSD CS1311      | 120 GB | 1       | 150   | 0     | 0.41   |
| Samsung   | MZNLN256HAJQ-000L2 | 256 GB | 9       | 150   | 0     | 0.41   |
| AMD       | R5S120GBSF         | 120 GB | 2       | 158   | 508   | 0.41   |
| Plextor   | PX-256M3           | 256 GB | 2       | 236   | 1     | 0.41   |
| PNY       | CS2040 128GB SSD   | 128 GB | 1       | 150   | 0     | 0.41   |
| Innodisk  | Corp. - mSATA 3ME  | 64 GB  | 1       | 150   | 0     | 0.41   |
| Crucial   | FCCT480M500SSD1    | 480 GB | 1       | 150   | 0     | 0.41   |
| Corsair   | CSSD-F180GB2       | 180 GB | 1       | 149   | 0     | 0.41   |
| Micron    | 1300_MTFDDAK1T0TDL | 1 TB   | 2       | 149   | 0     | 0.41   |
| WDC       | WDS120G2G0A-00JH30 | 120 GB | 248     | 167   | 5     | 0.41   |
| Plextor   | PX-128M6G-2242     | 128 GB | 2       | 149   | 0     | 0.41   |
| KingSpec  | T-64               | 64 GB  | 7       | 154   | 1     | 0.41   |
| KingSpec  | P4-480             | 480 GB | 7       | 149   | 0     | 0.41   |
| SanDisk   | SSD U100           | 256 GB | 6       | 202   | 1     | 0.41   |
| Advantech | SQF-SLMV2-128G-SBE | 128 GB | 1       | 148   | 0     | 0.41   |
| China     | SATA SSD           | 960 GB | 5       | 148   | 0     | 0.41   |
| Kingston  | SE100S3100G        | 100 GB | 1       | 1932  | 12    | 0.41   |
| SanDisk   | iSSD P4            | 8 GB   | 9       | 323   | 17    | 0.41   |
| OCZ       | TRION100           | 480 GB | 4       | 247   | 2     | 0.41   |
| Toshiba   | THNSNJ512GACU      | 512 GB | 1       | 148   | 0     | 0.41   |
| Intel     | SSDSC2BF180A5H SED | 180 GB | 4       | 368   | 35    | 0.41   |
| Intel     | SSDSC2KB019T8      | 1.9 TB | 6       | 148   | 0     | 0.41   |
| Intel     | SSDSC2KG960G8      | 960 GB | 5       | 148   | 0     | 0.41   |
| Micron    | MTFDDAK512MBF-1... | 512 GB | 2       | 148   | 0     | 0.41   |
| HP        | SSD S600           | 120 GB | 6       | 175   | 1     | 0.41   |
| Silico... | GSDSL256TY2AAQGCX  | 256 GB | 1       | 147   | 0     | 0.41   |
| Samsung   | MZNLN512HAJQ-000H1 | 512 GB | 3       | 147   | 0     | 0.40   |
| JASTER    | SSD                | 128 GB | 3       | 147   | 0     | 0.40   |
| Kingston  | RBUSNS8180S3128GJ  | 128 GB | 6       | 147   | 0     | 0.40   |
| Team      | T253X1120G         | 120 GB | 8       | 148   | 4     | 0.40   |
| Apple     | SSD SD0256F        | 256 GB | 5       | 146   | 0     | 0.40   |
| Kingston  | MS80000058688      | 256 GB | 3       | 146   | 0     | 0.40   |
| Team      | T253TD480G         | 480 GB | 3       | 146   | 0     | 0.40   |
| Intel     | SSDSA2M160G2GC     | 160 GB | 8       | 720   | 71    | 0.40   |
| WDC       | WDS120G2G0B-00EPW0 | 120 GB | 83      | 158   | 1     | 0.40   |
| Teclast   | 128GB S550         | 128 GB | 1       | 146   | 0     | 0.40   |
| ADATA     | SU650              | 240 GB | 116     | 169   | 32    | 0.40   |
| Kingston  | HyperX Fury 3D     | 480 GB | 2       | 146   | 0     | 0.40   |
| Transcend | TS1TSSD230S        | 1 TB   | 7       | 145   | 0     | 0.40   |
| Transcend | TS256GSSD230S      | 256 GB | 17      | 164   | 62    | 0.40   |
| ADATA     | SU650              | 480 GB | 37      | 170   | 169   | 0.40   |
| KingSpec  | ACJC2M032mSH       | 32 GB  | 2       | 145   | 0     | 0.40   |
| Samsung   | MZ-5EA2000-0D3     | 200 GB | 2       | 145   | 0     | 0.40   |
| China     | ESA3SMH2MSPB120GB  | 120 GB | 2       | 145   | 0     | 0.40   |
| Kingston  | SA400M8120G        | 120 GB | 28      | 145   | 0     | 0.40   |
| Intel     | SSDSC2KW512G8      | 512 GB | 30      | 179   | 1     | 0.40   |
| WDC       | WDBNCE0010PNC      | 1 TB   | 26      | 144   | 0     | 0.40   |
| Union ... | RTOTJ128VGD2EYX    | 128 GB | 12      | 144   | 0     | 0.40   |
| Super ... | FTM56N325H         | 256 GB | 4       | 227   | 1     | 0.39   |
| Lumino... | SSD                | 256 GB | 1       | 143   | 0     | 0.39   |
| Kston     | SSD                | 128 GB | 5       | 143   | 0     | 0.39   |
| Qumo      | SSD                | 64 GB  | 1       | 143   | 0     | 0.39   |
| SK hynix  | HFS256G32TNF-N3A0A | 256 GB | 5       | 143   | 0     | 0.39   |
| HP        | SSD S750           | 256 GB | 3       | 143   | 0     | 0.39   |
| VENO S... | SSD                | 256 GB | 1       | 142   | 0     | 0.39   |
| Samsung   | MZ7LN512HMJP-000H7 | 512 GB | 1       | 142   | 0     | 0.39   |
| KingFast  | SSD                | 128 GB | 20      | 150   | 1     | 0.39   |
| Lenovo    | SSD SL700 480G     | 480 GB | 2       | 142   | 0     | 0.39   |
| Toshiba   | THNSNW032GMCP      | 32 GB  | 1       | 142   | 0     | 0.39   |
| SPCC      | SSD                | 256 GB | 113     | 145   | 1     | 0.39   |
| SanDisk   | X600 M.2 2280 SATA | 512 GB | 1       | 141   | 0     | 0.39   |
| SK hynix  | HFS128G39MND-3310A | 128 GB | 2       | 141   | 0     | 0.39   |
| Team      | T253X1960G         | 960 GB | 3       | 141   | 0     | 0.39   |
| Crucial   | CT120BX500SSD1     | 120 GB | 217     | 144   | 1     | 0.39   |
| Crucial   | CT2000MX500SSD1    | 2 TB   | 126     | 141   | 8     | 0.39   |
| KingSpec  | KSD-SA25.5-064MJ   | 64 GB  | 1       | 141   | 0     | 0.39   |
| Transcend | TS512GSSD370S      | 512 GB | 6       | 165   | 2     | 0.39   |
| Samsung   | SSD 870 QVO        | 8 TB   | 9       | 140   | 0     | 0.39   |
| Transcend | TS128GSSD360S      | 128 GB | 10      | 140   | 0     | 0.39   |
| Plextor   | PX-128M6V          | 128 GB | 2       | 140   | 0     | 0.39   |
| Kingston  | SUV500MS120G       | 120 GB | 27      | 158   | 84    | 0.39   |
| e2e4      | SSD                | 64 GB  | 1       | 140   | 0     | 0.39   |
| Samsung   | MZ7LH480HAHQ0D3    | 480 GB | 2       | 140   | 0     | 0.39   |
| Innodisk  | mSATA mini 3ME ... | 32 GB  | 1       | 140   | 0     | 0.39   |
| Varro     | bulldozer-240GB    | 240 GB | 1       | 140   | 0     | 0.38   |
| Mushkin   | MKNSSDRW500GB      | 480 GB | 1       | 140   | 0     | 0.38   |
| Corsair   | Performance3 SSD   | 256 GB | 1       | 140   | 0     | 0.38   |
| WDC       | WDS480G2G0B-00EPW0 | 480 GB | 29      | 148   | 1     | 0.38   |
| ASENNO    | AS25               | 240 GB | 2       | 139   | 0     | 0.38   |
| Mushkin   | MKNSSDE3240GB      | 240 GB | 2       | 139   | 0     | 0.38   |
| MENGMI    | SSD                | 240 GB | 1       | 139   | 0     | 0.38   |
| Transcend | TS128GMSA230S      | 128 GB | 3       | 139   | 0     | 0.38   |
| Lite-On   | CV3-CE256          | 256 GB | 2       | 273   | 2     | 0.38   |
| Plextor   | PX-512M6Pro        | 512 GB | 3       | 198   | 1     | 0.38   |
| Plextor   | PX-G128M6e         | 128 GB | 1       | 138   | 0     | 0.38   |
| Intenso   | SSD                | 128 GB | 51      | 145   | 1     | 0.38   |
| Toshiba   | THNSNH512GDNT      | 512 GB | 1       | 138   | 0     | 0.38   |
| Seagate   | BarraCuda 120 S... | 2 TB   | 2       | 138   | 0     | 0.38   |
| WDC       | WDS400T2B0A-00SM50 | 4 TB   | 6       | 138   | 0     | 0.38   |
| Vaseky    | V800-1TB           | 1 TB   | 1       | 138   | 0     | 0.38   |
| Intel     | SSDSC2BF240A5L     | 240 GB | 17      | 197   | 9     | 0.38   |
| WINTEN    | WT200-SSD-256GB    | 256 GB | 1       | 138   | 0     | 0.38   |
| ADATA     | SU630              | 960 GB | 10      | 143   | 1     | 0.38   |
| ShanDi... | SSD                | 512 GB | 4       | 137   | 0     | 0.38   |
| Samsung   | SSD 860 EVO M.2    | 2 TB   | 11      | 137   | 0     | 0.38   |
| ADATA     | SU650NS38          | 480 GB | 6       | 137   | 0     | 0.38   |
| Goodram   | IR-SSDPR-S25A-120  | 120 GB | 8       | 137   | 0     | 0.38   |
| Lite-On   | IT LMT-256L9M      | 256 GB | 2       | 137   | 0     | 0.38   |
| Micron    | 1100 SATA          | 256 GB | 39      | 170   | 29    | 0.38   |
| Goodram   | IR-SSDPR-S25A-240  | 240 GB | 12      | 137   | 0     | 0.38   |
| Kingston  | RBUSC180DS37256GJ  | 256 GB | 5       | 137   | 0     | 0.38   |
| ZTC       | SM201-256G         | 256 GB | 3       | 137   | 0     | 0.38   |
| KingDian  | S280               | 240 GB | 19      | 136   | 0     | 0.38   |
| ADATA     | SU800              | 256 GB | 85      | 163   | 38    | 0.37   |
| AGI       | AGI240G18AI238     | 240 GB | 2       | 136   | 0     | 0.37   |
| PNY       | CS900 120GB SSD    | 120 GB | 126     | 136   | 0     | 0.37   |
| KingSpec  | NT-2TB             | 2 TB   | 1       | 136   | 0     | 0.37   |
| KingDian  | S400               | 480 GB | 3       | 136   | 0     | 0.37   |
| WDC       | PC SA530 SDATB8... | 1 TB   | 1       | 136   | 0     | 0.37   |
| Gost      | SSD240             | 240 GB | 1       | 135   | 0     | 0.37   |
| Kingston  | SHFR200480G        | 480 GB | 2       | 261   | 590   | 0.37   |
| Lumino... | SSD                | 128 GB | 1       | 135   | 0     | 0.37   |
| SK hynix  | HFS128G32MND-3210A | 128 GB | 1       | 135   | 0     | 0.37   |
| Micron    | MTFDDAK960TDT      | 960 GB | 3       | 135   | 0     | 0.37   |
| RZX       | 19SSD6G-480GB      | 480 GB | 2       | 134   | 0     | 0.37   |
| MACROVIP  | SSD                | 240 GB | 1       | 134   | 0     | 0.37   |
| Fujitsu   | F300               | 480 GB | 1       | 134   | 0     | 0.37   |
| Kingston  | SA400M8480G        | 480 GB | 10      | 134   | 0     | 0.37   |
| Crucial   | CT240BX200SSD1     | 240 GB | 39      | 134   | 1     | 0.37   |
| Kingston  | SA400S37           | 120 GB | 1       | 938   | 6     | 0.37   |
| Zheino    | CHN mSATA02M 256   | 256 GB | 2       | 219   | 1     | 0.37   |
| Toshiba   | THNSFJ256GDNU      | 256 GB | 1       | 133   | 0     | 0.37   |
| Yeyian    | VALK 2000          | 512 GB | 1       | 133   | 0     | 0.37   |
| Intel     | SSDSC2BF180A4H     | 180 GB | 24      | 260   | 5     | 0.37   |
| OWC       | Mercury Extreme... | 240 GB | 3       | 133   | 0     | 0.37   |
| ADATA     | IM2S3338-128GD2    | 128 GB | 12      | 133   | 0     | 0.37   |
| WDC       | WDS240G2G0A-00JH30 | 240 GB | 413     | 158   | 2     | 0.36   |
| Star D... | SATA SSD           | 960 GB | 1       | 132   | 0     | 0.36   |
| Crucial   | M4-CT256M4SSD3     | 256 GB | 4       | 477   | 559   | 0.36   |
| HP        | SSD S700           | 250 GB | 36      | 137   | 20    | 0.36   |
| Intel     | SSDSC2KW256G8      | 256 GB | 47      | 132   | 1     | 0.36   |
| SanDisk   | Z400s M.2 2280     | 256 GB | 3       | 131   | 0     | 0.36   |
| Toshiba   | TR200              | 960 GB | 4       | 131   | 0     | 0.36   |
| Kingston  | RBUSNS8180DS3512GJ | 512 GB | 8       | 131   | 0     | 0.36   |
| China     | mSATA SSD          | 128 GB | 1       | 131   | 0     | 0.36   |
| Gigabyte  | GP-GSTFS31256GTND  | 256 GB | 3       | 131   | 0     | 0.36   |
| Axiom     | C560 Series SSD    | 512 GB | 1       | 131   | 0     | 0.36   |
| BRAVEE... | SSD                | 1 TB   | 1       | 131   | 0     | 0.36   |
| Plextor   | PX-256M7VG         | 256 GB | 1       | 130   | 0     | 0.36   |
| Kingston  | SQ500S37120G       | 120 GB | 2       | 130   | 0     | 0.36   |
| Crucial   | CT480BX300SSD1     | 480 GB | 16      | 130   | 0     | 0.36   |
| Hikvision | HS-SSD-C100 960G   | 960 GB | 2       | 130   | 0     | 0.36   |
| KingSpec  | MT-128             | 128 GB | 8       | 130   | 0     | 0.36   |
| Hikvision | HS-SSD-C100        | 480 GB | 2       | 130   | 0     | 0.36   |
| ADATA     | SU635              | 480 GB | 7       | 145   | 30    | 0.36   |
| KingDian  | S180               | 64 GB  | 18      | 133   | 63    | 0.36   |
| HPE       | MK0800GEYKE        | 800 GB | 1       | 130   | 0     | 0.36   |
| Kingston  | RBUSNS8180DS3128GJ | 128 GB | 16      | 137   | 1     | 0.36   |
| China     | GM128              | 128 GB | 1       | 129   | 0     | 0.36   |
| Crucial   | CT250MX500SSD4     | 250 GB | 25      | 129   | 0     | 0.36   |
| Transcend | TS256GMTS400       | 256 GB | 9       | 129   | 0     | 0.36   |
| Toshiba   | THNSNF064GMCS      | 64 GB  | 2       | 129   | 0     | 0.35   |
| SanDisk   | SSD U100           | 24 GB  | 47      | 161   | 31    | 0.35   |
| Toshiba   | THNSNK256GVN8      | 256 GB | 3       | 129   | 0     | 0.35   |
| GLOWAY    | STK1TS3-S7         | 1 TB   | 2       | 129   | 0     | 0.35   |
| XrayDisk  | SSD                | 512 GB | 2       | 128   | 0     | 0.35   |
| SK hynix  | SC308 SATA         | 128 GB | 13      | 240   | 122   | 0.35   |
| SPCC      | SPCCSolidStateDisk | 512 GB | 2       | 128   | 0     | 0.35   |
| Micron    | 1100_MTFDDAV512TBN | 512 GB | 42      | 135   | 71    | 0.35   |
| Apacer    | AS340              | 120 GB | 24      | 128   | 0     | 0.35   |
| Samsung   | SSD 860 PRO        | 2 TB   | 14      | 128   | 0     | 0.35   |
| KLEVV     | SSD NEO N500       | 240 GB | 1       | 127   | 0     | 0.35   |
| Plextor   | PX-512S2G          | 512 GB | 3       | 127   | 0     | 0.35   |
| Goodram   | SSDPR-CL100-120-G2 | 120 GB | 13      | 127   | 0     | 0.35   |
| PNY       | SSD2SC120G3LC72... | 120 GB | 1       | 127   | 0     | 0.35   |
| Lite-On   | LMT-256M3M         | 256 GB | 1       | 253   | 1     | 0.35   |
| Lumino... | SSD                | 240 GB | 1       | 126   | 0     | 0.35   |
| AMD       | R5M120G8           | 120 GB | 4       | 126   | 0     | 0.35   |
| Chiprex   | S10T3120GB         | 120 GB | 1       | 126   | 0     | 0.35   |
| PNY       | CS900 1TB SSD      | 1 TB   | 15      | 126   | 0     | 0.35   |
| Kingston  | SMSM150S324G       | 24 GB  | 1       | 126   | 0     | 0.35   |
| LDLC      | F6+M.2 480         | 480 GB | 5       | 126   | 0     | 0.35   |
| OCZ       | D2CSTK181M11-0180  | 180 GB | 3       | 126   | 0     | 0.35   |
| BlueRay   | SSD                | 120 GB | 1       | 125   | 0     | 0.34   |
| Lite-On   | CV3-8D256-11 SATA  | 256 GB | 12      | 125   | 0     | 0.34   |
| Samsung   | MZ7KH1T9HAJR0D3    | 1.9 TB | 4       | 125   | 0     | 0.34   |
| Lite-On   | CV5-8Q128          | 128 GB | 1       | 125   | 0     | 0.34   |
| Crucial   | CT240BX500SSD1     | 240 GB | 450     | 126   | 1     | 0.34   |
| Kingston  | SA400S37           | 480 GB | 1       | 124   | 0     | 0.34   |
| China     | ASS-120            | 120 GB | 1       | 124   | 0     | 0.34   |
| Patriot   | P200               | 2 TB   | 3       | 322   | 16    | 0.34   |
| SanDisk   | SDSSDH3 250G       | 250 GB | 11      | 124   | 0     | 0.34   |
| PNY       | CS1211 240GB SS... | 240 GB | 1       | 124   | 0     | 0.34   |
| KingFast  | SSD                | 256 GB | 20      | 124   | 0     | 0.34   |
| SanDisk   | SDLF1DAR-960G-1HA1 | 960 GB | 2       | 124   | 0     | 0.34   |
| Micron    | M510DC_MTFDDAK9... | 960 GB | 1       | 1355  | 10    | 0.34   |
| Netac     | SSD                | 120 GB | 17      | 138   | 180   | 0.34   |
| Apple     | SSD SD0128F        | 121 GB | 28      | 132   | 2     | 0.34   |
| ADATA     | SP580              | 120 GB | 19      | 122   | 0     | 0.34   |
| Apacer    | AS350              | 240 GB | 20      | 127   | 1     | 0.33   |
| Crucial   | CT480BX500SSD1     | 480 GB | 323     | 124   | 1     | 0.33   |
| Hypertec  | SSD2S240SF1200SA2  | 240 GB | 2       | 371   | 512   | 0.33   |
| Kingston  | SA400S371TB        | 1 TB   | 1       | 121   | 0     | 0.33   |
| Plextor   | PH6-CE240-L2       | 240 GB | 1       | 121   | 0     | 0.33   |
| T-FORCE   | SSD                | 500 GB | 4       | 121   | 0     | 0.33   |
| Lite-On   | CV3-CE128-11 SATA  | 128 GB | 5       | 121   | 0     | 0.33   |
| HP        | VK001920GWJPH      | 1.9 TB | 2       | 121   | 0     | 0.33   |
| SK hynix  | SHGS31-1000GS-2    | 1 TB   | 23      | 145   | 1     | 0.33   |
| Innodisk  | DEM24-16GM41BC1... | 16 GB  | 2       | 121   | 0     | 0.33   |
| Smartbuy  | SSD                | 240 GB | 11      | 121   | 0     | 0.33   |
| Micron    | 5300_MTFDDAK960TDS | 960 GB | 2       | 181   | 1     | 0.33   |
| Patriot   | Burst Elite        | 960 GB | 2       | 120   | 0     | 0.33   |
| ADATA     | SU655              | 240 GB | 6       | 171   | 7     | 0.33   |
| ADATA     | SSD S511           | 64 GB  | 3       | 450   | 679   | 0.33   |
| Goodram   | SSDPR-CX400-01T-G2 | 1 TB   | 4       | 120   | 0     | 0.33   |
| ADATA     | SP550              | 240 GB | 42      | 130   | 79    | 0.33   |
| Samsung   | MZNLF128HCHP-000L1 | 128 GB | 2       | 120   | 0     | 0.33   |
| Fujitsu   | F500s 480G         | 480 GB | 1       | 119   | 0     | 0.33   |
| SPCC      | M.2 Disk           | 256 GB | 1       | 119   | 0     | 0.33   |
| Lite-On   | CV3-8D128-HP       | 128 GB | 4       | 119   | 0     | 0.33   |
| EZCOOL    | S400               | 120 GB | 1       | 119   | 0     | 0.33   |
| Plextor   | PX-AG128M6e        | 128 GB | 4       | 229   | 2     | 0.33   |
| Samsung   | SSD 870 QVO        | 2 TB   | 102     | 119   | 0     | 0.33   |
| Intel     | SSDSC2KI512G8      | 512 GB | 1       | 119   | 0     | 0.33   |
| SanDisk   | SSD PLUS           | 240 GB | 246     | 142   | 1     | 0.33   |
| SPCC      | SSD                | 128 GB | 121     | 120   | 1     | 0.32   |
| Patriot   | P210               | 1 TB   | 5       | 129   | 1     | 0.32   |
| ADATA     | SU650              | 120 GB | 155     | 134   | 57    | 0.32   |
| Samsung   | MZNTE128HMGR-00000 | 128 GB | 1       | 118   | 0     | 0.32   |
| Fanxiang  | S101-1TB           | 1 TB   | 1       | 117   | 0     | 0.32   |
| China     | SSD-128GB          | 128 GB | 1       | 117   | 0     | 0.32   |
| ADATA     | SU810NS38 SATA ... | 256 GB | 12      | 117   | 0     | 0.32   |
| Toshiba   | KSG60ZMV256G M.... | 256 GB | 37      | 163   | 28    | 0.32   |
| China     | SATA3 256GB SSD    | 256 GB | 8       | 117   | 0     | 0.32   |
| Palit     | PSP720 SSD         | 720 GB | 1       | 117   | 0     | 0.32   |
| SanDisk   | SD9SN8W128G1002    | 128 GB | 10      | 117   | 0     | 0.32   |
| Maxtor    | Z1 SSD             | 240 GB | 14      | 117   | 0     | 0.32   |
| SanDisk   | SD9TN8W256G1001    | 256 GB | 3       | 117   | 0     | 0.32   |
| Transcend | TS128GMTS430S      | 128 GB | 7       | 116   | 0     | 0.32   |
| XSTAR     | SSD                | 256 GB | 1       | 116   | 0     | 0.32   |
| SanDisk   | SDSSDH3 500G       | 500 GB | 50      | 116   | 1     | 0.32   |
| Lite-On   | CV8-8E128          | 128 GB | 1       | 116   | 0     | 0.32   |
| Samsung   | SSD 870 QVO        | 4 TB   | 31      | 116   | 0     | 0.32   |
| China     | HS1TBQE            | 1 TB   | 1       | 116   | 0     | 0.32   |
| Indilinx  | IND-S325S-512G     | 512 GB | 1       | 116   | 0     | 0.32   |
| Samsung   | MMCRE64GFMPP-MVA   | 64 GB  | 3       | 116   | 0     | 0.32   |
| Silicon   | SATA3 1TB SSD      | 1 TB   | 1       | 116   | 0     | 0.32   |
| ADATA     | SSD SX900 512GB... | 512 GB | 2       | 116   | 0     | 0.32   |
| Intel     | SSDSA2M080G2LE     | 80 GB  | 2       | 171   | 6     | 0.32   |
| Seagate   | IronWolf ZA500N... | 500 GB | 2       | 116   | 0     | 0.32   |
| ZTC       | SM201-512G         | 512 GB | 2       | 115   | 0     | 0.32   |
| WDC       | WDS480G2G0A-00JH30 | 480 GB | 81      | 149   | 5     | 0.32   |
| ADATA     | SU700              | 120 GB | 12      | 169   | 2     | 0.32   |
| Apacer    | AS450              | 120 GB | 1       | 115   | 0     | 0.32   |
| Samsung   | SG9XCS2D400GESLT   | 400 GB | 1       | 115   | 0     | 0.32   |
| SK hynix  | HFS512G39TND-N210A | 512 GB | 11      | 355   | 525   | 0.32   |
| HXY       | SSD 120G           | 120 GB | 1       | 115   | 0     | 0.32   |
| Maxtor    | Z1 SSD             | 960 GB | 1       | 114   | 0     | 0.31   |
| TCSUNBOW  | X3                 | 480 GB | 6       | 114   | 0     | 0.31   |
| SK hynix  | HFS256G32MND-2900A | 256 GB | 3       | 386   | 10    | 0.31   |
| China     | SSD 120G           | 120 GB | 3       | 114   | 0     | 0.31   |
| Intel     | SSDSC2BF180A5L     | 180 GB | 13      | 190   | 20    | 0.31   |
| Hikvision | HS-SSD-E100 512G   | 512 GB | 3       | 114   | 0     | 0.31   |
| KingSpec  | NT-128             | 128 GB | 9       | 128   | 112   | 0.31   |
| Wdstars   | ssd w31-128G       | 128 GB | 1       | 114   | 0     | 0.31   |
| SanDisk   | SSD PLUS           | 1 TB   | 123     | 156   | 76    | 0.31   |
| Intel     | SSDSCKGF240A5L     | 240 GB | 2       | 114   | 0     | 0.31   |
| Corsair   | FORCE LX SSD       | 256 GB | 1       | 113   | 0     | 0.31   |
| HEORIADY  | HX-001 E           | 1 TB   | 1       | 113   | 0     | 0.31   |
| China     | SSD512M2S80        | 512 GB | 1       | 113   | 0     | 0.31   |
| XUM       | HX256GSSDSATA3     | 240 GB | 2       | 113   | 0     | 0.31   |
| Gigaby... | GP-GSTFS31120GNTD  | 120 GB | 37      | 113   | 0     | 0.31   |
| OCZ       | VERTEX2            | 90 GB  | 1       | 113   | 0     | 0.31   |
| Inland    | SATA SSD           | 128 GB | 2       | 112   | 0     | 0.31   |
| China     | SATA SSD           | 512 GB | 9       | 112   | 0     | 0.31   |
| SanDisk   | SSD PLUS           | 480 GB | 147     | 139   | 2     | 0.31   |
| China     | SIC-1TB            | 1 TB   | 1       | 112   | 0     | 0.31   |
| China     | SSD                | 480 GB | 18      | 112   | 0     | 0.31   |
| Samsung   | MZMPC128HBFU-000   | 128 GB | 2       | 112   | 0     | 0.31   |
| Kingston  | RBU-SNS8100S312... | 128 GB | 5       | 111   | 0     | 0.31   |
| GS Nan... | 256-16 GSPTA256... | 256 GB | 2       | 111   | 0     | 0.31   |
| Samsung   | MZ7LN128HCHP-00000 | 128 GB | 1       | 111   | 0     | 0.31   |
| Seagate   | BarraCuda 120 S... | 250 GB | 14      | 111   | 0     | 0.31   |
| GLOWAY    | YCT512GS3-S7 Pro   | 512 GB | 2       | 111   | 0     | 0.31   |
| SFAS      | SSD                | 480 GB | 1       | 111   | 0     | 0.31   |
| China     | SATA3 240GB SSD    | 240 GB | 8       | 129   | 1     | 0.31   |
| SPCC      | Solid State DisK   | 2 TB   | 1       | 111   | 0     | 0.30   |
| Team      | TM4PS7256G         | 256 GB | 1       | 111   | 0     | 0.30   |
| EMTEC     | X150               | 480 GB | 7       | 110   | 0     | 0.30   |
| Samsung   | MZNTY256HDHP-00007 | 256 GB | 1       | 110   | 0     | 0.30   |
| SanDisk   | SD6SB1M128G1002    | 128 GB | 1       | 110   | 0     | 0.30   |
| Intel     | SSDSC2KG019T8      | 1.9 TB | 4       | 110   | 0     | 0.30   |
| ORICO     | N300               | 128 GB | 1       | 110   | 0     | 0.30   |
| SuperS... | S540               | 240 GB | 1       | 110   | 0     | 0.30   |
| Crucial   | CT4000MX500SSD1    | 4 TB   | 3       | 110   | 0     | 0.30   |
| Intel     | SSDSC2KB038TZ      | 3.8 TB | 1       | 110   | 0     | 0.30   |
| TEXTORM   | BM5                | 480 GB | 1       | 109   | 0     | 0.30   |
| Lite-On   | CV3-8D128-11 SATA  | 128 GB | 17      | 109   | 0     | 0.30   |
| Team      | L7 EVO SSD         | 64 GB  | 2       | 109   | 0     | 0.30   |
| China     | SSD                | 1 TB   | 29      | 109   | 0     | 0.30   |
| Kingston  | OMSP0S364B-00      | 64 GB  | 1       | 109   | 0     | 0.30   |
| Faspeed   | H7-240G            | 240 GB | 1       | 109   | 0     | 0.30   |
| Lite-On   | LCS-256M6S         | 256 GB | 9       | 124   | 117   | 0.30   |
| KingFast  | SSD                | 1 TB   | 3       | 109   | 0     | 0.30   |
| AirDisk   | 128GB SSD          | 128 GB | 3       | 108   | 0     | 0.30   |
| WDC       | WDS250G2B0B        | 250 GB | 9       | 108   | 0     | 0.30   |
| Intenso   | 1TB SATA SSD       | 1 TB   | 1       | 108   | 0     | 0.30   |
| Intel     | SSDSC2BW480H6      | 480 GB | 7       | 307   | 85    | 0.30   |
| SK hynix  | HFS256G39MND-2300A | 256 GB | 6       | 421   | 123   | 0.30   |
| China     | NGFF 2242 240GB... | 240 GB | 1       | 107   | 0     | 0.30   |
| Micron    | 5100_MTFDDAK240TCC | 240 GB | 2       | 676   | 5     | 0.30   |
| KingSpec  | Q-180              | 180 GB | 6       | 113   | 157   | 0.29   |
| FORESEE   | 128GB SSD          | 128 GB | 26      | 107   | 0     | 0.29   |
| Kingston  | RBUSNS8180DS3128GH | 128 GB | 11      | 107   | 0     | 0.29   |
| AMD       | R3SL120G           | 120 GB | 35      | 107   | 1     | 0.29   |
| Goodram   | SSDPR-CX400-256    | 256 GB | 22      | 107   | 0     | 0.29   |
| AMD       | R5SL240G           | 240 GB | 26      | 119   | 1     | 0.29   |
| KingDian  | S200               | 64 GB  | 11      | 129   | 12    | 0.29   |
| Apacer    | AS350              | 256 GB | 55      | 106   | 0     | 0.29   |
| Kingston  | HyperX Fury 3D     | 240 GB | 7       | 106   | 0     | 0.29   |
| Zheino    | CHN mSATAM3 128    | 128 GB | 3       | 106   | 0     | 0.29   |
| PNY       | SSD2SC240G5LC72... | 240 GB | 1       | 106   | 0     | 0.29   |
| Mushkin   | MKNSSDAT60GB-V     | 64 GB  | 1       | 106   | 0     | 0.29   |
| Teutons   | SSD                | 256 GB | 1       | 106   | 0     | 0.29   |
| Samsung   | MZYTE128HMGR-000L2 | 128 GB | 1       | 106   | 0     | 0.29   |
| Toshiba   | KSG60ZMV256G       | 256 GB | 4       | 106   | 0     | 0.29   |
| Samsung   | MZMPC256HAFU-000L9 | 256 GB | 1       | 106   | 0     | 0.29   |
| Intenso   | SSD                | 480 GB | 5       | 106   | 0     | 0.29   |
| Team      | TM8PS7256G         | 256 GB | 13      | 105   | 0     | 0.29   |
| HP        | SSD S700 Pro       | 1 TB   | 5       | 105   | 0     | 0.29   |
| TREKSTOR  | TREKSTORSSD128GB   | 128 GB | 1       | 105   | 0     | 0.29   |
| ADATA     | SU800              | 2 TB   | 8       | 124   | 1     | 0.29   |
| Samsung   | MZNLN256HAJQ-000H7 | 256 GB | 4       | 105   | 0     | 0.29   |
| Toshiba   | THNSNC256GBSJ      | 256 GB | 1       | 105   | 0     | 0.29   |
| AMD       | R5SL480G           | 480 GB | 5       | 181   | 29    | 0.29   |
| MARVELL   | SATAIII            | 16 GB  | 1       | 105   | 0     | 0.29   |
| Corsair   | Neutron GTX SSD    | 240 GB | 6       | 797   | 93    | 0.29   |
| KingDian  | S280-120GB         | 120 GB | 10      | 117   | 396   | 0.29   |
| Crucial   | CT480BX200SSD1     | 480 GB | 8       | 104   | 0     | 0.29   |
| SanDisk   | SDSSDH3 2T00       | 2 TB   | 17      | 104   | 0     | 0.29   |
| Transcend | TS256GSSD360S      | 256 GB | 3       | 104   | 0     | 0.29   |
| Gigaby... | GP-GSTFS31480GNTD  | 480 GB | 4       | 104   | 0     | 0.29   |
| SPCC      | SPCCSolidStateDisk | 256 GB | 3       | 104   | 0     | 0.29   |
| China     | SSD                | 120 GB | 66      | 128   | 19    | 0.29   |
| SUNEAST   | SSD SE800          | 1 TB   | 2       | 341   | 87    | 0.29   |
| China     | SATA3 1TB SSD      | 1 TB   | 10      | 104   | 0     | 0.29   |
| Seagate   | XA480ME10063       | 480 GB | 4       | 104   | 0     | 0.29   |
| Transcend | TS256GSSD370S      | 256 GB | 22      | 104   | 0     | 0.29   |
| Micron    | 1100_MTFDDAV256TBN | 256 GB | 113     | 112   | 105   | 0.29   |
| Apacer    | 16GB SATA Flash... | 16 GB  | 13      | 339   | 19    | 0.29   |
| Samsung   | MZ7LN128HAHQ-000L2 | 128 GB | 24      | 103   | 0     | 0.28   |
| Gigaby... | GP-GSTFS31240GNTD  | 240 GB | 37      | 103   | 0     | 0.28   |
| Crucial   | CT1000BX500SSD1    | 1 TB   | 116     | 103   | 1     | 0.28   |
| China     | NGFF 2280 1TB SSD  | 1 TB   | 1       | 103   | 0     | 0.28   |
| GeIL      | R3_128GB           | 128 GB | 3       | 103   | 0     | 0.28   |
| Plextor   | PX-128M5Pro        | 128 GB | 57      | 103   | 0     | 0.28   |
| Intel     | SSDSA2M160G2GN     | 160 GB | 1       | 2996  | 28    | 0.28   |
| Transcend | TS128GSSD370S      | 128 GB | 32      | 103   | 0     | 0.28   |
| Lite-On   | LCH-256V2S         | 256 GB | 10      | 106   | 1     | 0.28   |
| Samsung   | MZMTD256HAGM-000   | 256 GB | 1       | 103   | 0     | 0.28   |
| Transcend | TS120GSSD25D-M     | 128 GB | 1       | 309   | 2     | 0.28   |
| Phison    | SATA SSD           | 1 TB   | 7       | 102   | 0     | 0.28   |
| PNY       | CS900 500GB SSD    | 500 GB | 47      | 102   | 0     | 0.28   |
| KingDian  | S370               | 512 GB | 2       | 102   | 0     | 0.28   |
| TAMMUZ    | SSD                | 128 GB | 1       | 102   | 0     | 0.28   |
| XrayDisk  | SSD                | 120 GB | 5       | 102   | 0     | 0.28   |
| Micron    | MTFDDAV256TBN-1... | 256 GB | 29      | 116   | 41    | 0.28   |
| Intel     | SSDSCKKF256G8 SATA | 256 GB | 16      | 107   | 1     | 0.28   |
| Samsung   | MZNLH512HALU-00000 | 512 GB | 18      | 102   | 0     | 0.28   |
| Lite-On   | CV8-CE128-11 SATA  | 128 GB | 1       | 102   | 0     | 0.28   |
| Apacer    | AS340              | 240 GB | 33      | 128   | 65    | 0.28   |
| Phison    | SSM28512GPTCB3B... | 512 GB | 1       | 101   | 0     | 0.28   |
| SanDisk   | SSD PLUS           | 2 TB   | 7       | 101   | 0     | 0.28   |
| WDC       | WDS100T2G0A-00JH30 | 1 TB   | 41      | 107   | 27    | 0.28   |
| Samsung   | MZNLN128HCGR-000HW | 128 GB | 1       | 101   | 0     | 0.28   |
| Team      | T253X1480G         | 480 GB | 12      | 101   | 0     | 0.28   |
| Samsung   | MZNTD256HAGL-00000 | 256 GB | 2       | 101   | 0     | 0.28   |
| INNOVA... | SSD                | 256 GB | 4       | 100   | 0     | 0.28   |
| e2e4      | SSD                | 480 GB | 2       | 100   | 0     | 0.28   |
| Samsung   | MZMTD128HAFV-00000 | 128 GB | 1       | 100   | 0     | 0.28   |
| HPE       | MK001920GWXFK      | 1.9 TB | 1       | 100   | 0     | 0.28   |
| Lexar     | SSD                | 480 GB | 3       | 100   | 0     | 0.28   |
| T-FORCE   | SSD                | 512 GB | 7       | 104   | 3     | 0.28   |
| Micron    | MTFDDAK256TDL      | 256 GB | 9       | 100   | 0     | 0.27   |
| Phison    | 128GB PS3109-S9    | 128 GB | 4       | 115   | 1     | 0.27   |
| Samsung   | MZ7KM480HMHQ-000MV | 480 GB | 1       | 100   | 0     | 0.27   |
| OCZ       | VERTEX PLUS        | 64 GB  | 2       | 199   | 1     | 0.27   |
| Apacer    | AS350              | 120 GB | 25      | 99    | 1     | 0.27   |
| ASENNO    | AS25               | 1 TB   | 2       | 279   | 11    | 0.27   |
| SK hynix  | HFS256G3BTND-N210A | 256 GB | 10      | 127   | 1     | 0.27   |
| Intenso   | lntenso SSD Sat... | 960 GB | 4       | 140   | 6     | 0.27   |
| Intenso   | SSD SATA III       | 240 GB | 1       | 99    | 0     | 0.27   |
| PUSKILL   | SSD                | 128 GB | 1       | 99    | 0     | 0.27   |
| Intenso   | SSD Sata III       | 1 TB   | 4       | 99    | 0     | 0.27   |
| BHT       | WR202I0064G E70... | 64 GB  | 3       | 99    | 0     | 0.27   |
| Lite-On   | LCH-128V2S-11 2... | 128 GB | 10      | 98    | 0     | 0.27   |
| KingFast  | SSD                | 480 GB | 1       | 98    | 0     | 0.27   |
| Intel     | SSDSC2KF128G8L     | 128 GB | 12      | 105   | 1     | 0.27   |
| Micron    | 5100_MTFDDAK240TCB | 240 GB | 1       | 98    | 0     | 0.27   |
| Netac     | SSD                | 720 GB | 6       | 173   | 23    | 0.27   |
| ADATA     | SU630              | 240 GB | 102     | 104   | 47    | 0.27   |
| AMD       | R3SL480G           | 480 GB | 1       | 98    | 0     | 0.27   |
| SanDisk   | SD7UB3Q128G1122    | 128 GB | 1       | 98    | 0     | 0.27   |
| Apacer    | AS340              | 480 GB | 15      | 98    | 1     | 0.27   |
| Toshiba   | THNSNH256G8NT      | 256 GB | 1       | 293   | 2     | 0.27   |
| GS Nan... | GS SSD 256-16 STR  | 256 GB | 1       | 97    | 0     | 0.27   |
| Team      | TM8PS7001T         | 1 TB   | 6       | 97    | 0     | 0.27   |
| Patriot   | P200               | 512 GB | 5       | 125   | 86    | 0.27   |
| KLEVV     | NEO N400 SSD       | 240 GB | 1       | 97    | 0     | 0.27   |
| Crucial   | CT256M550SSD3      | 256 GB | 3       | 573   | 11    | 0.27   |
| Blackpcs  | AS201 SSD          | 128 GB | 1       | 96    | 0     | 0.26   |
| JD        | SSD                | 120 GB | 1       | 96    | 0     | 0.26   |
| Plextor   | PX-256M8VG         | 256 GB | 4       | 96    | 0     | 0.26   |
| KingDian  | SSD-S400           | 120 GB | 1       | 287   | 2     | 0.26   |
| Team      | T253A3512G         | 512 GB | 3       | 95    | 0     | 0.26   |
| KingSpec  | Q-90               | 90 GB  | 3       | 385   | 175   | 0.26   |
| SPCC      | SSD170             | 120 GB | 3       | 245   | 341   | 0.26   |
| ADATA     | SU650              | 512 GB | 3       | 95    | 0     | 0.26   |
| Lexar     | 1TB SSD            | 1 TB   | 11      | 98    | 1     | 0.26   |
| Crucial   | CT256M550SSD1      | 256 GB | 12      | 1064  | 100   | 0.26   |
| GOWE      | M750 120G          | 120 GB | 1       | 284   | 2     | 0.26   |
| Toshiba   | THNSNH256GBST      | 256 GB | 3       | 94    | 0     | 0.26   |
| Verbatim  | Vi550 S3 SSD       | 128 GB | 18      | 94    | 0     | 0.26   |
| Apacer    | 32GB SATA Flash... | 32 GB  | 7       | 126   | 5     | 0.26   |
| Lexar     | 256GB SSD          | 256 GB | 32      | 94    | 0     | 0.26   |
| Lite-On   | LCS-128M6S         | 128 GB | 11      | 98    | 6     | 0.26   |
| China     | ESA3ASA2HTH2BT1... | 120 GB | 1       | 94    | 0     | 0.26   |
| Silicon   | SATA3 240GB SSD    | 240 GB | 2       | 93    | 0     | 0.26   |
| Kingston  | SHSS37A960G        | 960 GB | 1       | 93    | 0     | 0.26   |
| Integral  | V Series SATA SSD  | 480 GB | 1       | 93    | 0     | 0.26   |
| Team      | T253E2002T         | 2 TB   | 1       | 93    | 0     | 0.26   |
| Apacer    | AS510S             | 64 GB  | 6       | 93    | 0     | 0.26   |
| Biostar   | S120-128GB         | 128 GB | 1       | 93    | 0     | 0.26   |
| Apacer    | AS350              | 1 TB   | 4       | 93    | 0     | 0.26   |
| Pioneer   | APS-SL3N-240       | 240 GB | 2       | 93    | 0     | 0.26   |
| SanDisk   | ASMT109x- Volume   | 756 GB | 5       | 93    | 0     | 0.26   |
| TwinMOS   | SSD                | 256 GB | 2       | 93    | 0     | 0.26   |
| Samsung   | MZYTE256HMHP-000L2 | 256 GB | 2       | 93    | 0     | 0.26   |
| GeIL      | Z3_256GB           | 256 GB | 1       | 93    | 0     | 0.26   |
| Leven     | JAJS600M256C       | 256 GB | 9       | 94    | 1     | 0.25   |
| Team      | TM8PS7512G         | 512 GB | 14      | 92    | 0     | 0.25   |
| Crucial   | CT500BX100SSD1     | 500 GB | 20      | 92    | 1     | 0.25   |
| Lite-On   | CV3-DE128          | 128 GB | 4       | 92    | 0     | 0.25   |
| Samsung   | MZMTD256HAGM-00000 | 256 GB | 1       | 92    | 0     | 0.25   |
| Goodram   | SSDPR-CL100-240-G3 | 240 GB | 17      | 92    | 0     | 0.25   |
| Intenso   | SDVPSA1910256      | 256 GB | 1       | 92    | 0     | 0.25   |
| Lite-On   | PH2-CJ120          | 120 GB | 1       | 92    | 0     | 0.25   |
| QUMO      | SSD                | 120 GB | 2       | 92    | 0     | 0.25   |
| INNOVA... | SSD                | 480 GB | 2       | 92    | 0     | 0.25   |
| Plextor   | PX-G256M6e         | 256 GB | 3       | 91    | 0     | 0.25   |
| Apacer    | AS350              | 128 GB | 76      | 93    | 2     | 0.25   |
| China     | ESA3SMH2ISN3BT0... | 64 GB  | 1       | 91    | 0     | 0.25   |
| T-FORCE   | SSD                | 1 TB   | 16      | 91    | 0     | 0.25   |
| Toshiba   | THNSNS256GMCP      | 256 GB | 1       | 91    | 0     | 0.25   |
| Dogfish   | SSD                | 512 GB | 11      | 91    | 0     | 0.25   |
| Samsung   | SSD 870 QVO        | 1 TB   | 200     | 90    | 0     | 0.25   |
| Lite-On   | L8H-128V2G-HP      | 128 GB | 4       | 90    | 0     | 0.25   |
| Intel     | SSDSCKGF256A5 SATA | 256 GB | 7       | 94    | 174   | 0.25   |
| HP        | SSD S700 Pro       | 128 GB | 3       | 90    | 0     | 0.25   |
| China     | SSD128GBS800       | 128 GB | 3       | 90    | 0     | 0.25   |
| KingDian  | S280               | 120 GB | 17      | 90    | 0     | 0.25   |
| Faspeed   | H5-60G PLUS        | 64 GB  | 1       | 90    | 0     | 0.25   |
| PNY       | SSD2SC480G1CS17... | 480 GB | 2       | 90    | 0     | 0.25   |
| Phison    | SATA SSD           | 256 GB | 8       | 90    | 0     | 0.25   |
| KingSpec  | NT-256             | 256 GB | 21      | 115   | 49    | 0.25   |
| OSCOO     | OSC M.2            | 120 GB | 1       | 89    | 0     | 0.25   |
| China     | SATA SSD           | 256 GB | 21      | 89    | 1     | 0.24   |
| Plextor   | PH6-CE120-L1       | 120 GB | 2       | 89    | 0     | 0.24   |
| Samsung   | MZAPF016HCDD-000H1 | 16 GB  | 1       | 89    | 0     | 0.24   |
| VisionTek | SSD                | 120 GB | 2       | 88    | 0     | 0.24   |
| KingSpec  | P3-512             | 512 GB | 22      | 96    | 82    | 0.24   |
| Kingch... | SSD                | 128 GB | 6       | 88    | 0     | 0.24   |
| Samsung   | MZ7LN256HAJQ-000L2 | 256 GB | 28      | 88    | 0     | 0.24   |
| Plextor   | PX-128M8VC         | 128 GB | 4       | 88    | 0     | 0.24   |
| Kingston  | SV300S37A-240G     | 240 GB | 2       | 88    | 0     | 0.24   |
| ORICO     | PM200-1T           | 1 TB   | 1       | 88    | 0     | 0.24   |
| China     | SATA3 128GB SSD    | 128 GB | 7       | 88    | 0     | 0.24   |
| Seagate   | ZA240NM10001       | 240 GB | 1       | 88    | 0     | 0.24   |
| Lite-On   | CV3-8D512-11 SATA  | 512 GB | 3       | 182   | 2     | 0.24   |
| Lite-On   | CV6-CQ128          | 128 GB | 1       | 88    | 0     | 0.24   |
| Lite-On   | S920 256           | 256 GB | 1       | 88    | 0     | 0.24   |
| WDC       | WDBNCE0040PNC      | 4 TB   | 1       | 88    | 0     | 0.24   |
| QUMO      | SATA SSD           | 120 GB | 1       | 88    | 0     | 0.24   |
| Intel     | SSDSCKKW256G8      | 256 GB | 5       | 129   | 10    | 0.24   |
| AXIOM     | SSD                | 120 GB | 1       | 87    | 0     | 0.24   |
| Lite-On   | CV8-8E128-11 SATA  | 128 GB | 28      | 87    | 0     | 0.24   |
| ORICO     | N300               | 256 GB | 1       | 262   | 2     | 0.24   |
| China     | SSD                | 512 GB | 29      | 99    | 130   | 0.24   |
| Kingston  | SKC380S3120G       | 120 GB | 1       | 86    | 0     | 0.24   |
| Drevo     | X1 SSD             | 120 GB | 12      | 281   | 29    | 0.24   |
| Kingston  | SV300S37A-120G     | 120 GB | 2       | 86    | 0     | 0.24   |
| Micron    | MTFDDAV256MBF-1... | 256 GB | 13      | 86    | 0     | 0.24   |
| Lenovo    | SSD SL700 120G     | 120 GB | 5       | 153   | 1     | 0.24   |
| SanDisk   | SD8TN8U-256G-1016  | 256 GB | 1       | 86    | 0     | 0.24   |
| Intel     | SSDSA2M080G2GN     | 80 GB  | 2       | 1445  | 15    | 0.24   |
| Plextor   | PX-256M6V          | 256 GB | 2       | 85    | 0     | 0.23   |
| Intel     | SSDMCEAF180A4L     | 180 GB | 1       | 85    | 0     | 0.23   |
| Team      | TEAMT2535T120G     | 120 GB | 1       | 85    | 0     | 0.23   |
| Intel     | SSDSCKJF180A5L     | 180 GB | 6       | 111   | 1     | 0.23   |
| Intenso   | SSD Sata III       | 120 GB | 30      | 114   | 83    | 0.23   |
| Colorful  | SL500              | 240 GB | 5       | 84    | 0     | 0.23   |
| Plextor   | PX-128M5M          | 128 GB | 12      | 84    | 0     | 0.23   |
| Apacer    | AS350              | 512 GB | 40      | 88    | 77    | 0.23   |
| Micron    | MTFDDAK960TDN      | 960 GB | 2       | 84    | 0     | 0.23   |
| ADATA     | SU750              | 512 GB | 11      | 84    | 0     | 0.23   |
| Londisk   | SSD                | 480 GB | 4       | 84    | 0     | 0.23   |
| Vaseky    | V800-350G          | 360 GB | 1       | 84    | 0     | 0.23   |
| Transcend | TS256GMTS800       | 256 GB | 4       | 84    | 0     | 0.23   |
| Kingston  | RBUSNS8180DS3256GJ | 256 GB | 10      | 92    | 1     | 0.23   |
| China     | 64GB SSD           | 64 GB  | 12      | 83    | 0     | 0.23   |
| Micron    | MTFDDAV256TBN-1... | 256 GB | 14      | 84    | 1     | 0.23   |
| Lite-On   | CV3-8D256          | 256 GB | 10      | 83    | 0     | 0.23   |
| Blackpcs  | AS201 SSD          | 120 GB | 1       | 83    | 0     | 0.23   |
| SanDisk   | SD9SB8W256G        | 256 GB | 1       | 83    | 0     | 0.23   |
| Lite-On   | LCH-512V2S         | 512 GB | 5       | 84    | 1     | 0.23   |
| China     | MS06               | 512 GB | 1       | 83    | 0     | 0.23   |
| Lite-On   | CV5-8Q256-HP       | 256 GB | 1       | 83    | 0     | 0.23   |
| ACPI      | SSD                | 120 GB | 1       | 83    | 0     | 0.23   |
| Lite-On   | CV4-8Q128-HP       | 128 GB | 1       | 82    | 0     | 0.23   |
| Lexar     | 128GB SSD          | 128 GB | 30      | 82    | 0     | 0.23   |
| SanDisk   | SD9SN8W-128G-1006  | 128 GB | 40      | 153   | 761   | 0.23   |
| Plextor   | PX-128S3C          | 128 GB | 14      | 82    | 0     | 0.23   |
| Lenovo    | Thinklife SSD S... | 128 GB | 1       | 82    | 0     | 0.23   |
| HP        | SSD S700           | 1 TB   | 7       | 82    | 0     | 0.23   |
| Team      | T2535T120G         | 120 GB | 5       | 111   | 2     | 0.23   |
| Team      | T253X2128G         | 128 GB | 5       | 82    | 0     | 0.23   |
| Nfortec   | ALCYON             | 512 GB | 1       | 82    | 0     | 0.22   |
| China     | MSATA 480GB SSD    | 480 GB | 2       | 81    | 0     | 0.22   |
| OCZ       | VECTOR180          | 120 GB | 2       | 81    | 0     | 0.22   |
| Intel     | SSDSCKKB240G8      | 240 GB | 2       | 81    | 0     | 0.22   |
| KingSpec  | KSQ120             | 120 GB | 1       | 81    | 0     | 0.22   |
| SanDisk   | SD7SN3Q128G1002    | 128 GB | 3       | 97    | 1     | 0.22   |
| Micron    | MTFDDAV512TBN      | 512 GB | 1       | 81    | 0     | 0.22   |
| SPCC      | 2.5¡± SSD        | 512 GB | 1       | 80    | 0     | 0.22   |
| Patriot   | P210               | 512 GB | 10      | 80    | 0     | 0.22   |
| HP        | SSD S700 Pro       | 256 GB | 3       | 80    | 0     | 0.22   |
| China     | SH00R240GB         | 240 GB | 6       | 80    | 0     | 0.22   |
| Kingston  | RBU-SNS8152S325... | 256 GB | 1       | 80    | 0     | 0.22   |
| Transcend | TS128GSSD370       | 128 GB | 15      | 80    | 0     | 0.22   |
| KingFast  | SSD                | 120 GB | 10      | 91    | 308   | 0.22   |
| China     | 256GB QLC SATA SSD | 256 GB | 2       | 80    | 0     | 0.22   |
| Intel     | SSDSC2KF180H6L     | 180 GB | 1       | 80    | 0     | 0.22   |
| Lite-On   | LAT-256M2S         | 256 GB | 1       | 239   | 2     | 0.22   |
| Fordisk   | S860 256G 6Gbps    | 256 GB | 1       | 79    | 0     | 0.22   |
| KingSpec  | NT-1TB             | 1 TB   | 4       | 79    | 0     | 0.22   |
| Transcend | TS128GMTS400S      | 128 GB | 3       | 79    | 0     | 0.22   |
| Apple     | SSD TS512C         | 500 GB | 1       | 79    | 0     | 0.22   |
| Colorful  | SL300              | 160 GB | 1       | 79    | 0     | 0.22   |
| Toshiba   | THNSFK512GVN8      | 512 GB | 1       | 79    | 0     | 0.22   |
| Lite-On   | CV3-DE512          | 512 GB | 1       | 79    | 0     | 0.22   |
| Intenso   | SSD Sata III       | 500 GB | 1       | 79    | 0     | 0.22   |
| PNY       | SSD2SC120G1CS17... | 120 GB | 1       | 79    | 0     | 0.22   |
| Seagate   | XA1920ME10063      | 1.9 TB | 2       | 79    | 0     | 0.22   |
| SanDisk   | SD8SB8U-128G-1006  | 128 GB | 2       | 78    | 0     | 0.22   |
| Dogfish   | SSD                | 500 GB | 3       | 78    | 0     | 0.22   |
| VISIPRO   | SDVPSA1910256      | 256 GB | 3       | 78    | 0     | 0.22   |
| Lexar     | 240GB SSD          | 240 GB | 8       | 78    | 0     | 0.21   |
| ADATA     | SU800              | 512 GB | 94      | 87    | 14    | 0.21   |
| KingSpec  | MT-64              | 64 GB  | 3       | 175   | 1     | 0.21   |
| Lite-On   | CV3-CE128          | 128 GB | 2       | 78    | 0     | 0.21   |
| Crucial   | CT1000MX500SSD1N   | 1 TB   | 1       | 77    | 0     | 0.21   |
| Transcend | TS240GMTS820S      | 240 GB | 9       | 77    | 0     | 0.21   |
| Transcend | TS256GMTS830S      | 256 GB | 4       | 77    | 0     | 0.21   |
| Intenso   | SSD                | 120 GB | 26      | 95    | 80    | 0.21   |
| Faspeed   | K5-120G            | 120 GB | 2       | 77    | 0     | 0.21   |
| Indilinx  | IND-S325S-120G     | 120 GB | 1       | 77    | 0     | 0.21   |
| China     | SSDG2-240G         | 240 GB | 1       | 76    | 0     | 0.21   |
| Micron    | C400-MTFDDAT064MAM | 64 GB  | 2       | 76    | 0     | 0.21   |
| INNOVA... | SSD                | 120 GB | 1       | 76    | 0     | 0.21   |
| Leven     | JAJS300M120C       | 120 GB | 6       | 76    | 0     | 0.21   |
| Dogfish   | SSD                | 240 GB | 2       | 76    | 0     | 0.21   |
| BHT       | WR202I0032G E70... | 32 GB  | 4       | 76    | 0     | 0.21   |
| SPCC      | SSD170             | 55 GB  | 4       | 540   | 762   | 0.21   |
| Solid     | SSD0240S00         | 240 GB | 3       | 75    | 0     | 0.21   |
| KingDian  | P10                | 250 GB | 1       | 75    | 0     | 0.21   |
| Transcend | TS64GSSD360S       | 64 GB  | 1       | 75    | 0     | 0.21   |
| SPEED UP  | B-128GB            | 128 GB | 1       | 75    | 0     | 0.21   |
| Fanxiang  | S101               | 512 GB | 1       | 75    | 0     | 0.21   |
| HP        | SSD S650           | 120 GB | 2       | 75    | 0     | 0.21   |
| China     | SSD                | 128 GB | 89      | 76    | 2     | 0.20   |
| PNY       | CS900 250GB SSD    | 250 GB | 13      | 74    | 0     | 0.20   |
| Lite-On   | LMH-256V2M-11 M... | 256 GB | 10      | 74    | 1     | 0.20   |
| China     | NGFF 2280          | 512 GB | 1       | 73    | 0     | 0.20   |
| Micron    | MTFDDAK256TBN      | 256 GB | 2       | 73    | 0     | 0.20   |
| Lite-On   | L8H-256V2G-11 M... | 256 GB | 9       | 73    | 0     | 0.20   |
| China     | SATA3 480GB SSD    | 480 GB | 7       | 99    | 41    | 0.20   |
| Toshiba   | KHK61VSE960G       | 960 GB | 1       | 73    | 0     | 0.20   |
| V-GeN     | V-GEN01SM22AR10... | 1 TB   | 1       | 73    | 0     | 0.20   |
| Vaseky    | V800-32G           | 32 GB  | 1       | 73    | 0     | 0.20   |
| Kingrich  | K9 128GB SATA3 SSD | 128 GB | 1       | 658   | 8     | 0.20   |
| Patriot   | P200               | 256 GB | 8       | 197   | 26    | 0.20   |
| WALRAM    | SSD 240G           | 240 GB | 3       | 72    | 0     | 0.20   |
| BAITITON  | BT58SSD12S         | 512 GB | 1       | 71    | 0     | 0.20   |
| Plextor   | PX-256M8VC         | 256 GB | 9       | 71    | 0     | 0.20   |
| Crucial   | CT120BX100SSD1     | 120 GB | 12      | 71    | 0     | 0.20   |
| KLLISRE   | SSD                | 256 GB | 1       | 71    | 0     | 0.20   |
| Vaseky    | V800-500G          | 512 GB | 1       | 71    | 0     | 0.20   |
| Kingston  | V300 120G          | 120 GB | 1       | 71    | 0     | 0.20   |
| SUNEAST   | SSD SE800          | 256 GB | 2       | 71    | 0     | 0.19   |
| EZCOOL    | S280               | 240 GB | 1       | 71    | 0     | 0.19   |
| Micron    | 1300_MTFDDAK256TDL | 256 GB | 4       | 71    | 0     | 0.19   |
| SK hynix  | SHGS31-250GS-2     | 250 GB | 1       | 70    | 0     | 0.19   |
| Samsung   | MZ7L3480HBLTAD3    | 480 GB | 2       | 70    | 0     | 0.19   |
| Samsung   | MZ7LH1T9HALT0D3    | 1.9 TB | 5       | 70    | 0     | 0.19   |
| Kingston  | SA400S37-240G      | 240 GB | 3       | 70    | 0     | 0.19   |
| Dogfish   | SSD                | 250 GB | 3       | 131   | 2     | 0.19   |
| Kingston  | SKC600MS256G       | 256 GB | 6       | 70    | 0     | 0.19   |
| Lite-On   | CV1-8B256          | 256 GB | 14      | 70    | 0     | 0.19   |
| ShanDi... | SSD                | 256 GB | 3       | 70    | 0     | 0.19   |
| TCSUNBOW  | X3                 | 240 GB | 4       | 70    | 0     | 0.19   |
| Leven     | JAJS600M512C       | 512 GB | 9       | 70    | 0     | 0.19   |
| OCZ       | SABER1000          | 480 GB | 1       | 70    | 0     | 0.19   |
| ADATA     | SP900NS38          | 128 GB | 4       | 120   | 254   | 0.19   |
| Netac     | SSD                | 240 GB | 33      | 72    | 1     | 0.19   |
| China     | SSD                | 256 GB | 61      | 77    | 1     | 0.19   |
| Kingrich  | K9 120GB SATA3     | 128 GB | 1       | 69    | 0     | 0.19   |
| Intel     | SSDSCKKW512G8      | 512 GB | 1       | 69    | 0     | 0.19   |
| Team      | T253X2256G         | 256 GB | 7       | 69    | 0     | 0.19   |
| Micron    | MTFDDAK3T8TCB 0... | 3.8 TB | 1       | 483   | 6     | 0.19   |
| Lite-On   | IT LMT-128L9M      | 128 GB | 3       | 68    | 0     | 0.19   |
| Plextor   | PX-128M6S          | 128 GB | 36      | 85    | 136   | 0.19   |
| SanDisk   | SDSSDH3256G        | 256 GB | 4       | 68    | 0     | 0.19   |
| Pioneer   | APS-SL3N-120       | 120 GB | 6       | 68    | 0     | 0.19   |
| Zheino    | CHN-25SATAC3-120   | 120 GB | 2       | 68    | 0     | 0.19   |
| Leven     | JAJS300M240C       | 240 GB | 9       | 104   | 8     | 0.19   |
| SanDisk   | SSD P4             | 32 GB  | 16      | 170   | 209   | 0.19   |
| SK hynix  | SC210 2.5 7MM      | 128 GB | 4       | 567   | 16    | 0.19   |
| Lite-On   | CV3-DE256          | 256 GB | 8       | 68    | 0     | 0.19   |
| ViperTeq  | VT-SSDUP500-240    | 240 GB | 1       | 68    | 0     | 0.19   |
| Micron    | MTFDDAV512TBN-1... | 512 GB | 5       | 78    | 1     | 0.19   |
| Samsung   | MZNLN256HAJQ-00007 | 256 GB | 2       | 68    | 0     | 0.19   |
| ADATA     | S596               | 128 GB | 1       | 68    | 0     | 0.19   |
| Plextor   | PX-256M6M          | 256 GB | 4       | 73    | 1     | 0.19   |
| SanDisk   | SD7SB3Q128G1002    | 128 GB | 3       | 647   | 107   | 0.19   |
| Kross ... | KE-SSDIS12G        | 120 GB | 2       | 67    | 0     | 0.19   |
| Intel     | SSDSC2KI256G8      | 256 GB | 2       | 67    | 0     | 0.18   |
| KingDian  | P10                | 120 GB | 2       | 69    | 19    | 0.18   |
| China     | SATA3 120GB SSD    | 120 GB | 10      | 67    | 0     | 0.18   |
| Lite-On   | LMT-256L9M-11 M... | 256 GB | 3       | 67    | 0     | 0.18   |
| SemsoTai  | L150 SSD           | 240 GB | 1       | 67    | 0     | 0.18   |
| Plextor   | PX-128M6Pro        | 128 GB | 13      | 74    | 1     | 0.18   |
| BlueRay   | SDM8SI480A         | 480 GB | 1       | 200   | 2     | 0.18   |
| ADATA     | SP900              | 512 GB | 2       | 66    | 0     | 0.18   |
| Intenso   | Memory Ghost SSD   | 512 GB | 1       | 66    | 0     | 0.18   |
| Transcend | TS512GMTS430S      | 512 GB | 20      | 66    | 0     | 0.18   |
| Kingston  | RBUSC180S3764GJ    | 64 GB  | 2       | 66    | 0     | 0.18   |
| AMD       | R5SL120G           | 120 GB | 36      | 74    | 1     | 0.18   |
| Kingmax   | SSD                | 240 GB | 7       | 130   | 55    | 0.18   |
| KLONER    | SSD                | 128 GB | 1       | 66    | 0     | 0.18   |
| Transcend | TS256GMTS400S      | 256 GB | 3       | 66    | 0     | 0.18   |
| Transcend | TS480GMTS420S      | 480 GB | 3       | 66    | 0     | 0.18   |
| Plextor   | PX-256M6S          | 256 GB | 12      | 77    | 179   | 0.18   |
| Intenso   | SATA3 1TB SSD      | 1 TB   | 2       | 219   | 12    | 0.18   |
| Intel     | SSDMCEAW180A4      | 180 GB | 2       | 65    | 0     | 0.18   |
| QUMO      | SATA SSD           | 240 GB | 1       | 65    | 0     | 0.18   |
| HGST      | HUSKY SSD          | 128 GB | 2       | 65    | 0     | 0.18   |
| FORESEE   | 64GB SSD           | 64 GB  | 7       | 65    | 0     | 0.18   |
| Netac     | SSD                | 480 GB | 5       | 65    | 0     | 0.18   |
| RX7       | MSATA              | 512 GB | 1       | 65    | 0     | 0.18   |
| Crucial   | CT250BX100SSD1     | 250 GB | 60      | 65    | 1     | 0.18   |
| Integral  | V Series SATA SSD  | 240 GB | 12      | 65    | 0     | 0.18   |
| Intel     | SSDSCKKW128G8      | 128 GB | 5       | 64    | 0     | 0.18   |
| Acer      | SSD SA100          | 120 GB | 5       | 64    | 0     | 0.18   |
| Hikvision | HS-SSD-C100 240G   | 240 GB | 13      | 64    | 0     | 0.18   |
| Avant     | 240GB Client SSD   | 240 GB | 1       | 64    | 0     | 0.18   |
| Intenso   | Morebeck-V602      | 120 GB | 1       | 64    | 0     | 0.18   |
| SanDisk   | SD5SF2032G1010E    | 32 GB  | 2       | 64    | 0     | 0.18   |
| Transcend | TS128GMSA370       | 128 GB | 7       | 64    | 0     | 0.18   |
| Hikvision | HS-SSD-C100 480G   | 480 GB | 3       | 63    | 0     | 0.17   |
| Micron    | 5300_MTFDDAK480TDS | 480 GB | 4       | 63    | 0     | 0.17   |
| Lite-On   | IT LST-32S9G-HP    | 32 GB  | 2       | 63    | 0     | 0.17   |
| Intel     | SSDSCKKF128G8 SATA | 128 GB | 9       | 74    | 2     | 0.17   |
| TrekStor  | TREKSTORSSD128GB   | 128 GB | 2       | 122   | 78    | 0.17   |
| Micron    | MTFDDAV512TDL-1... | 512 GB | 1       | 63    | 0     | 0.17   |
| Kingston  | SUV400S37 120G     | 120 GB | 1       | 63    | 0     | 0.17   |
| LDLC      | F7+240GB           | 240 GB | 5       | 63    | 0     | 0.17   |
| Seagate   | BarraCuda Q1 SS... | 240 GB | 4       | 63    | 0     | 0.17   |
| Intel     | SSDSC2KW010T8      | 1 TB   | 1       | 504   | 7     | 0.17   |
| Netac     | SSD                | 512 GB | 22      | 62    | 0     | 0.17   |
| Hikvision | HS-SSD-C100 120G   | 120 GB | 17      | 62    | 0     | 0.17   |
| Intenso   | SSD SATAIII        | 240 GB | 60      | 66    | 1     | 0.17   |
| SanDisk   | SDSSDH2064G        | 64 GB  | 1       | 62    | 0     | 0.17   |
| Neo Forza | NFS011SA351-600... | 512 GB | 2       | 62    | 0     | 0.17   |
| Ramaxel   | RTIRB128RFM2KWDL   | 128 GB | 1       | 375   | 5     | 0.17   |
| China     | ESA3SMH2ISN2BT1... | 120 GB | 1       | 62    | 0     | 0.17   |
| KINGBANK  | KP330              | 120 GB | 5       | 62    | 0     | 0.17   |
| Zheino    | CHN 25SATAC3 128   | 128 GB | 1       | 62    | 0     | 0.17   |
| Intel     | SSDSC2BF480A5L     | 480 GB | 1       | 62    | 0     | 0.17   |
| Kingrich  | SSD 120G           | 120 GB | 1       | 62    | 0     | 0.17   |
| Transcend | TS256GMTS430S      | 256 GB | 18      | 62    | 0     | 0.17   |
| KingSpec  | P3-256             | 256 GB | 15      | 114   | 6     | 0.17   |
| China     | SCCTS-603-128G SSD | 128 GB | 1       | 62    | 0     | 0.17   |
| China     | SH00N256GB         | 256 GB | 2       | 62    | 0     | 0.17   |
| Netac     | W800S 512GB SSD    | 512 GB | 1       | 62    | 0     | 0.17   |
| Lite-On   | CV8-8E256-11 SATA  | 256 GB | 8       | 62    | 0     | 0.17   |
| SanDisk   | SD9SB8W256G1102    | 256 GB | 4       | 62    | 0     | 0.17   |
| SMI       | SSD DISK           | 500 GB | 1       | 62    | 0     | 0.17   |
| Patriot   | P200               | 1 TB   | 5       | 80    | 9     | 0.17   |
| OCZ       | D2CSTK251M3T-0480  | 480 GB | 1       | 62    | 0     | 0.17   |
| Londisk   | SSD                | 240 GB | 4       | 62    | 0     | 0.17   |
| SanDisk   | SDSA5DK-016G-1006  | 16 GB  | 2       | 62    | 0     | 0.17   |
| Netac     | SSD                | 1 TB   | 18      | 79    | 1     | 0.17   |
| Patriot   | P210               | 128 GB | 14      | 62    | 0     | 0.17   |
| SK hynix  | SH920 2.5 7MM      | 256 GB | 9       | 688   | 117   | 0.17   |
| Advantech | SQF-S25M8-128G-AAG | 128 GB | 1       | 61    | 0     | 0.17   |
| China     | SSD                | 240 GB | 40      | 94    | 54    | 0.17   |
| Seagate   | FireCuda 120 SS... | 500 GB | 2       | 61    | 0     | 0.17   |
| SK hynix  | HFS128G38MNB-2200A | 128 GB | 5       | 1096  | 86    | 0.17   |
| SK hynix  | HFS128G39TNF-N3A0A | 128 GB | 6       | 61    | 0     | 0.17   |
| HP        | SSD S650           | 240 GB | 2       | 61    | 0     | 0.17   |
| Toshiba   | Q200 EX            | 240 GB | 1       | 61    | 0     | 0.17   |
| Crucial   | CT1000BX100SSD1    | 1 TB   | 2       | 61    | 0     | 0.17   |
| Plextor   | PX-256S1G          | 256 GB | 1       | 61    | 0     | 0.17   |
| SPCC      | M.2 SSD            | 120 GB | 4       | 106   | 1     | 0.17   |
| Lite-On   | IT L8T-128L9G      | 128 GB | 2       | 61    | 0     | 0.17   |
| TCSUNBOW  | X3                 | 64 GB  | 3       | 61    | 0     | 0.17   |
| Gigaby... | GP-GSTFS31100TNTD  | 1 TB   | 1       | 61    | 0     | 0.17   |
| China     | NGFF 2242 512GB... | 512 GB | 3       | 60    | 0     | 0.17   |
| KingSpec  | P3-128             | 128 GB | 30      | 116   | 6     | 0.17   |
| Platinet  | SSD                | 120 GB | 3       | 61    | 30    | 0.17   |
| Goodram   | IRIDIUM PRO        | 240 GB | 1       | 60    | 0     | 0.17   |
| SPCC      | SSDB28             | 128 GB | 2       | 76    | 1     | 0.17   |
| GS Nan... | GS SSD 256-16      | 240 GB | 1       | 60    | 0     | 0.17   |
| ANACOMDA  | A1                 | 120 GB | 1       | 60    | 0     | 0.17   |
| Qumo      | SSD                | 256 GB | 1       | 60    | 0     | 0.17   |
| Transcend | TS960GMTS820S      | 960 GB | 1       | 60    | 0     | 0.17   |
| Toshiba   | THNSN9480GESG      | 480 GB | 1       | 60    | 0     | 0.17   |
| INNOVA... | SSD_2.5"_TLC_24... | 240 GB | 3       | 60    | 0     | 0.16   |
| SUNEAST   | SSD SE800          | 1.9 TB | 1       | 60    | 0     | 0.16   |
| V-GeN     | V-GEN10SM21SCY5... | 512 GB | 1       | 60    | 0     | 0.16   |
| Intenso   | JAJM600M1024C      | 1 TB   | 1       | 59    | 0     | 0.16   |
| Gigabyte  | GP-GSTFS31480GNTD  | 480 GB | 8       | 59    | 0     | 0.16   |
| China     | 256GB SSD          | 256 GB | 11      | 59    | 0     | 0.16   |
| PNY       | SSD2SC240G1CS17... | 240 GB | 1       | 59    | 0     | 0.16   |
| Intenso   | C500               | 256 GB | 2       | 59    | 0     | 0.16   |
| China     | 512GB SSD          | 512 GB | 5       | 59    | 0     | 0.16   |
| Lite-On   | CV3-SD256          | 256 GB | 2       | 59    | 0     | 0.16   |
| Kingston  | RBU-SUS151S364GD   | 64 GB  | 4       | 59    | 0     | 0.16   |
| ORTIAL    | SSD                | 128 GB | 3       | 59    | 0     | 0.16   |
| TEKET     | SA18-032M-4F       | 32 GB  | 2       | 59    | 0     | 0.16   |
| Samsung   | MZNLN256HAJQ-000L7 | 256 GB | 8       | 59    | 0     | 0.16   |
| ADATA     | SU760              | 256 GB | 4       | 92    | 61    | 0.16   |
| Samsung   | SSD 870 EVO        | 1 TB   | 194     | 104   | 56    | 0.16   |
| EYOTA     | SSD                | 256 GB | 1       | 58    | 0     | 0.16   |
| Patriot   | P210               | 256 GB | 20      | 76    | 1     | 0.16   |
| Kingston  | SA400S37-240GB     | 240 GB | 1       | 58    | 0     | 0.16   |
| Kingston  | SKC380S3240G       | 240 GB | 1       | 58    | 0     | 0.16   |
| Team      | T253LE120G         | 120 GB | 8       | 58    | 0     | 0.16   |
| Win Me... | SWR256G-201II      | 256 GB | 2       | 58    | 0     | 0.16   |
| Vaseky    | V800-128G          | 128 GB | 3       | 58    | 0     | 0.16   |
| Lite-On   | CV3-8D128          | 128 GB | 10      | 58    | 0     | 0.16   |
| Zheino    | CHN 25SATAC3 120   | 120 GB | 1       | 58    | 0     | 0.16   |
| Vaseky    | V800-256G          | 256 GB | 3       | 57    | 0     | 0.16   |
| OCZ       | OCZSSD2-2VTX50G    | 50 GB  | 1       | 57    | 0     | 0.16   |
| Lite-On   | IT LCS-128L9S      | 128 GB | 2       | 57    | 0     | 0.16   |
| Goldkey   | GKH84-64GB         | 64 GB  | 1       | 57    | 0     | 0.16   |
| Goodram   | SSDPR-CX400-512-G2 | 512 GB | 22      | 67    | 1     | 0.16   |
| OWC       | Neptune 6G SSD     | 480 GB | 2       | 57    | 0     | 0.16   |
| Micron    | 1300 SATA          | 256 GB | 4       | 56    | 0     | 0.16   |
| SanDisk   | X600 M.2 2280 SATA | 256 GB | 1       | 56    | 0     | 0.16   |
| PNY       | SSD2SC120G1LC76... | 120 GB | 1       | 56    | 0     | 0.16   |
| Lite-On   | IT L8T-128L9G-HP   | 128 GB | 1       | 56    | 0     | 0.16   |
| ADATA     | SU630              | 480 GB | 34      | 75    | 174   | 0.16   |
| Lexar     | 512GB SSD          | 512 GB | 10      | 56    | 0     | 0.15   |
| Super ... | FTM50N325H         | 500 GB | 2       | 56    | 0     | 0.15   |
| Kingston  | RBUSC180DS37128GJ  | 128 GB | 7       | 56    | 0     | 0.15   |
| Golden... | SSD                | 240 GB | 1       | 56    | 0     | 0.15   |
| Plextor   | PX-256M6Pro        | 256 GB | 3       | 91    | 2     | 0.15   |
| Samsung   | SSD 870 EVO        | 250 GB | 87      | 59    | 1     | 0.15   |
| INNOVA... | SSD_M.2_512GB_I... | 512 GB | 1       | 56    | 0     | 0.15   |
| INNOVA... | SSD                | 512 GB | 6       | 75    | 5     | 0.15   |
| SanDisk   | SSD U100           | 64 GB  | 25      | 96    | 1     | 0.15   |
| ASMedia   | ASMT109x- Fast     | 2 TB   | 4       | 55    | 0     | 0.15   |
| Phison    | SSE064GPTC0-S81    | 64 GB  | 1       | 55    | 0     | 0.15   |
| China     | JOYSSD512          | 512 GB | 1       | 55    | 0     | 0.15   |
| Qumo      | SSD                | 240 GB | 3       | 55    | 0     | 0.15   |
| e2e4      | SSD                | 120 GB | 4       | 55    | 0     | 0.15   |
| Smartbuy  | SSD                | 512 GB | 2       | 55    | 0     | 0.15   |
| Corsair   | CSSD-F120GB2       | 120 GB | 3       | 748   | 485   | 0.15   |
| SanDisk   | SD8SBAT256G1122    | 256 GB | 15      | 57    | 3     | 0.15   |
| China     | GM1TB              | 1 TB   | 1       | 55    | 0     | 0.15   |
| Goodram   | SSDPR-CX400-128-G2 | 128 GB | 32      | 55    | 0     | 0.15   |
| Mushkin   | MKNSSDCR480GB      | 480 GB | 1       | 55    | 0     | 0.15   |
| Apacer    | AST280             | 240 GB | 2       | 55    | 0     | 0.15   |
| China     | SSD                | 64 GB  | 9       | 60    | 4     | 0.15   |
| BIWIN     | M6305              | 120 GB | 1       | 54    | 0     | 0.15   |
| Kingston  | SQ500S37240G       | 240 GB | 7       | 54    | 0     | 0.15   |
| Avant     | 60GB Client SSD    | 64 GB  | 2       | 823   | 508   | 0.15   |
| V-GeN     | V-GEN05SM21AR12... | 128 GB | 2       | 54    | 0     | 0.15   |
| AGI       | AGI240G06AI138     | 240 GB | 1       | 54    | 0     | 0.15   |
| SanDisk   | SSD i100           | 64 GB  | 1       | 54    | 0     | 0.15   |
| SanDisk   | pSSD               | 128 GB | 56      | 62    | 8     | 0.15   |
| Lite-On   | LCS-128L9S-11 2... | 128 GB | 2       | 54    | 0     | 0.15   |
| ADATA     | SP580              | 960 GB | 2       | 54    | 0     | 0.15   |
| Aoluska   | A6-120G            | 120 GB | 1       | 54    | 0     | 0.15   |
| KingSpec  | P4-240             | 240 GB | 24      | 82    | 58    | 0.15   |
| Samsung   | MCCOE64G8MPP-0VA   | 64 GB  | 1       | 377   | 6     | 0.15   |
| SanDisk   | SD8SBAT-256G-1006  | 256 GB | 2       | 53    | 0     | 0.15   |
| Transcend | TS64GMTS800S       | 64 GB  | 1       | 53    | 0     | 0.15   |
| Kingston  | SHPM2280P2-240G    | 240 GB | 1       | 1557  | 28    | 0.15   |
| China     | ESA3SMN2ISN1BQ4... | 480 GB | 1       | 53    | 0     | 0.15   |
| Fanxiang  | S101               | 256 GB | 2       | 53    | 0     | 0.15   |
| Lite-On   | LCS-128M6S-HP      | 128 GB | 7       | 66    | 145   | 0.15   |
| SanDisk   | SSD i100           | 8 GB   | 4       | 53    | 0     | 0.15   |
| INNOVA... | SSD_2.5"_TLC_51... | 512 GB | 3       | 53    | 0     | 0.15   |
| Samsung   | MZMTD128HAFV-000H1 | 128 GB | 1       | 53    | 0     | 0.15   |
| Samsung   | SSD 870 EVO        | 2 TB   | 31      | 108   | 69    | 0.15   |
| Intel     | SSDSCKKF180G8L     | 180 GB | 2       | 53    | 0     | 0.15   |
| Apple     | SSD TS064E         | 64 GB  | 2       | 98    | 4     | 0.15   |
| Netac     | N600               | 128 GB | 1       | 52    | 0     | 0.14   |
| Transcend | TS240GMTS420S      | 240 GB | 19      | 65    | 80    | 0.14   |
| Crucial   | CT1024M550SSD1     | 1 TB   | 1       | 897   | 16    | 0.14   |
| Lite-On   | L8H-256V2G         | 256 GB | 10      | 58    | 1     | 0.14   |
| XrayDisk  | SSD                | 240 GB | 13      | 65    | 1     | 0.14   |
| China     | SSV5               | 480 GB | 5       | 52    | 0     | 0.14   |
| Lite-On   | LGT-128M6G         | 128 GB | 1       | 52    | 0     | 0.14   |
| Kingston  | RBUSNS8180S3256GJ  | 256 GB | 6       | 52    | 0     | 0.14   |
| Hyundai   | C2S3T-120G         | 120 GB | 1       | 52    | 0     | 0.14   |
| Phison    | SATA SSD           | 960 GB | 3       | 52    | 0     | 0.14   |
| SanDisk   | SD8TN8U-256G-1006  | 256 GB | 4       | 274   | 513   | 0.14   |
| IPLEX     | TITAN256XP         | 256 GB | 1       | 52    | 0     | 0.14   |
| JUHOR     | Z500               | 240 GB | 1       | 52    | 0     | 0.14   |
| HP        | VK000240GWCFD      | 240 GB | 1       | 52    | 0     | 0.14   |
| SK hynix  | HFS256G32TNH-73A0A | 256 GB | 5       | 81    | 2     | 0.14   |
| ADATA     | SP610              | 128 GB | 3       | 51    | 0     | 0.14   |
| Intenso   | SSD256M2S80        | 256 GB | 1       | 51    | 0     | 0.14   |
| Lite-On   | IT LDS-128L9S      | 128 GB | 1       | 51    | 0     | 0.14   |
| Smartbuy  | mSata              | 256 GB | 3       | 51    | 0     | 0.14   |
| Apacer    | AS340              | 960 GB | 1       | 51    | 0     | 0.14   |
| Lite-On   | LMT-19nmBGA-128G   | 128 GB | 1       | 51    | 0     | 0.14   |
| Seagate   | ZA1920NM10001      | 1.9 TB | 4       | 51    | 0     | 0.14   |
| ADATA     | SU720              | 1 TB   | 4       | 50    | 0     | 0.14   |
| Intel     | SSDSCKKF512G8 SATA | 512 GB | 2       | 50    | 0     | 0.14   |
| ZHITAI    | SC001 Active 1T... | 1 TB   | 2       | 50    | 0     | 0.14   |
| i-Flas... | K6                 | 64 GB  | 1       | 50    | 0     | 0.14   |
| Plextor   | PX-128M6M          | 128 GB | 7       | 70    | 513   | 0.14   |
| Samsung   | SSD PB22-CS3 FD... | 256 GB | 1       | 50    | 0     | 0.14   |
| Transcend | TS128GSSD230S      | 128 GB | 19      | 50    | 0     | 0.14   |
| China     | SSD 240G           | 240 GB | 1       | 50    | 0     | 0.14   |
| OCZ       | INTREPID 3800      | 400 GB | 1       | 50    | 0     | 0.14   |
| Intel     | SSDSC2KF256H6 SATA | 256 GB | 4       | 54    | 31    | 0.14   |
| EMTEC     | X250               | 512 GB | 2       | 49    | 0     | 0.14   |
| ADATA     | SP610              | 512 GB | 2       | 49    | 0     | 0.14   |
| China     | WPC-240GB          | 240 GB | 1       | 49    | 0     | 0.14   |
| Corsair   | Neutron GTX SSD    | 480 GB | 1       | 49    | 0     | 0.14   |
| KingSpec  | MSH-256            | 256 GB | 4       | 49    | 0     | 0.14   |
| Lite-On   | CX1-JB256-HP       | 256 GB | 1       | 49    | 0     | 0.14   |
| Kingston  | SKC6001024G        | 1 TB   | 12      | 49    | 0     | 0.14   |
| Eluktro   | TRO-SSD7-128GB-PRO | 128 GB | 1       | 49    | 0     | 0.14   |
| Crucial   | CT2050MX300SSD1    | 2 TB   | 6       | 56    | 5     | 0.14   |
| Gateway   | W800SH 256GB SSD   | 256 GB | 1       | 49    | 0     | 0.14   |
| JAMESD... | JD480              | 480 GB | 1       | 49    | 0     | 0.14   |
| V-GeN     | V-GEN12AS19AR12... | 120 GB | 1       | 49    | 0     | 0.14   |
| KingSpec  | NT-512             | 512 GB | 18      | 55    | 1     | 0.14   |
| Inland    | SATA SSD           | 1 TB   | 1       | 49    | 0     | 0.13   |
| KingDian  | S200               | 120 GB | 2       | 49    | 0     | 0.13   |
| Greenl... | 32GB ArmourDrive   | 32 GB  | 1       | 49    | 0     | 0.13   |
| SanDisk   | SDSA5DK 32G        | 32 GB  | 1       | 49    | 0     | 0.13   |
| Transcend | TS512GMTS800       | 512 GB | 5       | 84    | 204   | 0.13   |
| Zheino    | CHN 25SATAA3 120   | 120 GB | 3       | 48    | 0     | 0.13   |
| Anobit    | Gen2A400 118032738 | 400 GB | 2       | 48    | 1     | 0.13   |
| Netac     | SSD                | 2 TB   | 1       | 48    | 0     | 0.13   |
| Rogueware | 2.5" SATA NX100S   | 1 TB   | 1       | 48    | 0     | 0.13   |
| SK hynix  | SH920 mSATA        | 256 GB | 5       | 564   | 155   | 0.13   |
| TCSUNBOW  | X3                 | 120 GB | 4       | 48    | 0     | 0.13   |
| SK hynix  | HFS128G32MND-3212A | 128 GB | 1       | 48    | 0     | 0.13   |
| Kingston  | KF-S42240-4R       | 240 GB | 1       | 47    | 0     | 0.13   |
| KingSpec  | MT-256             | 256 GB | 12      | 72    | 8     | 0.13   |
| GeIL      | R3 120G            | 120 GB | 1       | 47    | 0     | 0.13   |
| Lite-On   | IT LMH-256V2M      | 256 GB | 1       | 47    | 0     | 0.13   |
| China     | 80GB SSD           | 80 GB  | 2       | 47    | 0     | 0.13   |
| EMTEC     | X150               | 240 GB | 15      | 47    | 0     | 0.13   |
| Transcend | TS32GMSA370        | 32 GB  | 5       | 47    | 0     | 0.13   |
| Teclast   | 120GB S500         | 120 GB | 1       | 47    | 0     | 0.13   |
| Win Me... | SWR256G-301II      | 256 GB | 2       | 47    | 0     | 0.13   |
| GALAX     | TA1D0240A          | 240 GB | 2       | 47    | 0     | 0.13   |
| Kingston  | SKC600256G         | 256 GB | 46      | 46    | 0     | 0.13   |
| XPG       | SX950U             | 240 GB | 3       | 46    | 0     | 0.13   |
| Crucial   | CT128M550SSD1      | 128 GB | 8       | 346   | 59    | 0.13   |
| ADATA     | SU750              | 256 GB | 36      | 50    | 25    | 0.13   |
| RCESSD    | SSD                | 512 GB | 2       | 46    | 0     | 0.13   |
| Patriot   | Burst Elite        | 120 GB | 20      | 47    | 51    | 0.13   |
| Lite-On   | CV8-8E256          | 256 GB | 12      | 46    | 0     | 0.13   |
| Crucial   | CT3500SC           | 500 GB | 2       | 467   | 11    | 0.13   |
| Hikvision | HS-SSD-E100 256G   | 256 GB | 4       | 46    | 0     | 0.13   |
| XrayDisk  | SSD                | 256 GB | 14      | 48    | 6     | 0.13   |
| LENSEN    | LS600 120G         | 120 GB | 1       | 46    | 0     | 0.13   |
| INNOVA... | SSD_M.2_1TB_Inn... | 1 TB   | 1       | 45    | 0     | 0.13   |
| Mushkin   | MKNSSDRE2TB        | 2 TB   | 2       | 45    | 0     | 0.13   |
| Transcend | TS120GMTS420S      | 120 GB | 27      | 46    | 1     | 0.13   |
| ADATA     | SP550              | 120 GB | 44      | 46    | 1     | 0.13   |
| Intel     | SSDSCKKF256H6L     | 256 GB | 2       | 52    | 29    | 0.13   |
| Intenso   | JAJMS600M1TB       | 1 TB   | 1       | 45    | 0     | 0.12   |
| Supers... | SUPERSONIC128GB    | 128 GB | 1       | 45    | 0     | 0.12   |
| Kingston  | RBU-SC152S37128GG2 | 128 GB | 1       | 45    | 0     | 0.12   |
| Zheino    | CHN mSATA02M 128   | 128 GB | 1       | 45    | 0     | 0.12   |
| Zheino    | CHN-mSATAQ3-120    | 120 GB | 1       | 45    | 0     | 0.12   |
| BHT       | WR202H0032G E70... | 32 GB  | 1       | 45    | 0     | 0.12   |
| Lite-On   | L8H-128V2G-11 M... | 128 GB | 4       | 45    | 0     | 0.12   |
| Team      | T2535T480G         | 480 GB | 4       | 808   | 104   | 0.12   |
| Verbatim  | Vi500 S3 240GB SSD | 240 GB | 2       | 45    | 0     | 0.12   |
| China     | W552-256G          | 256 GB | 1       | 45    | 0     | 0.12   |
| China     | M10C               | 128 GB | 1       | 44    | 0     | 0.12   |
| MARSHAL   | MAL2128SA-LS3DL... | 128 GB | 1       | 44    | 0     | 0.12   |
| Intenso   | A200-240GB         | 240 GB | 1       | 44    | 0     | 0.12   |
| SanDisk   | Z400s 2.5 7MM      | 256 GB | 1       | 44    | 0     | 0.12   |
| Lite-On   | LGT-256M6G         | 256 GB | 6       | 44    | 0     | 0.12   |
| Transcend | TS128GMTS800       | 128 GB | 12      | 44    | 0     | 0.12   |
| LDLC      | SSD                | 128 GB | 5       | 44    | 0     | 0.12   |
| KIOXIA... | SATA SSD           | 960 GB | 3       | 44    | 0     | 0.12   |
| Intenso   | SSD Sata III       | 256 GB | 31      | 47    | 19    | 0.12   |
| Transcend | TS128GMTS400       | 128 GB | 7       | 44    | 0     | 0.12   |
| Silicon   | SATA3 128GB SSD    | 128 GB | 1       | 44    | 0     | 0.12   |
| PNY       | 480GB SATA SSD     | 480 GB | 1       | 44    | 0     | 0.12   |
| FATTYDOVE | SSD                | 48 GB  | 1       | 44    | 0     | 0.12   |
| PRETEC    | G2000 SSD          | 32 GB  | 1       | 44    | 0     | 0.12   |
| Intenso   | SSD Sata III       | 512 GB | 3       | 44    | 0     | 0.12   |
| JAMESD... | JD120              | 120 GB | 1       | 44    | 0     | 0.12   |
| Faspeed   | K7N8-256GF         | 256 GB | 1       | 44    | 0     | 0.12   |
| Crucial   | CT512M550SSD3      | 512 GB | 6       | 172   | 123   | 0.12   |
| Plextor   | PX-512M3           | 512 GB | 1       | 1402  | 31    | 0.12   |
| KingSpec  | P4-60              | 64 GB  | 1       | 43    | 0     | 0.12   |
| Lite-On   | LMT-19nmBGA-256G   | 256 GB | 1       | 43    | 0     | 0.12   |
| PNY       | SSD2SC240G1CS27... | 240 GB | 1       | 43    | 0     | 0.12   |
| Intel     | SSDSCKJW240H6      | 240 GB | 1       | 43    | 0     | 0.12   |
| Samsung   | SSD 870 EVO        | 500 GB | 170     | 71    | 19    | 0.12   |
| MidasF... | SSD                | 128 GB | 4       | 43    | 0     | 0.12   |
| KingSpec  | Q-720              | 720 GB | 4       | 43    | 0     | 0.12   |
| Transcend | TS64GMSA370        | 64 GB  | 3       | 43    | 0     | 0.12   |
| Apacer    | AST280             | 120 GB | 4       | 43    | 0     | 0.12   |
| Intel     | SSDSC2KW256G8L     | 256 GB | 4       | 43    | 0     | 0.12   |
| BIWIN     | SSD                | 128 GB | 13      | 72    | 238   | 0.12   |
| Samsung   | SSD 870 EVO        | 4 TB   | 13      | 59    | 64    | 0.12   |
| Ramsta    | SSD S800           | 480 GB | 1       | 43    | 0     | 0.12   |
| ORIGIN... | TLC830 Pro Series  | 1 TB   | 1       | 43    | 0     | 0.12   |
| Silico... | SP SolidState Disk | 64 GB  | 1       | 43    | 0     | 0.12   |
| Lite-On   | LMT-32L3M-HP       | 32 GB  | 4       | 128   | 533   | 0.12   |
| Zheino    | CHN 25SATA01M 060  | 64 GB  | 2       | 43    | 0     | 0.12   |
| Transcend | TS256GMSA230S      | 256 GB | 3       | 43    | 0     | 0.12   |
| Phison    | S11-512G-PHISON... | 512 GB | 6       | 42    | 0     | 0.12   |
| Gigabyte  | GP-GSTFS31960GN... | 960 GB | 2       | 42    | 0     | 0.12   |
| Samsung   | 860-500GB          | 512 GB | 1       | 42    | 0     | 0.12   |
| Intel     | SSDSCKKW256H6      | 256 GB | 3       | 59    | 194   | 0.12   |
| Intenso   | SSD                | 240 GB | 11      | 44    | 1     | 0.12   |
| SUNEAST   | SSD SE800 mSATA    | 480 GB | 1       | 42    | 0     | 0.12   |
| Foxline   | FLSSD256X5SE       | 256 GB | 4       | 42    | 0     | 0.12   |
| Intel     | SSDSCKKF010X6      | 1 TB   | 1       | 42    | 0     | 0.12   |
| Intenso   | N900-512           | 512 GB | 1       | 128   | 2     | 0.12   |
| PNY       | SSD2SC120G5LC70... | 120 GB | 1       | 42    | 0     | 0.12   |
| Teclast   | 480GB A900         | 480 GB | 1       | 42    | 0     | 0.12   |
| China     | SSD128G            | 128 GB | 1       | 42    | 0     | 0.12   |
| XrayDisk  | SSD                | 128 GB | 10      | 59    | 1     | 0.12   |
| Transcend | TS2TSSD220Q        | 2 TB   | 3       | 42    | 0     | 0.12   |
| GLOWAY    | WAR PRO T300 240G  | 240 GB | 1       | 42    | 0     | 0.12   |
| SanDisk   | SD8SFAT128G1122    | 128 GB | 1       | 42    | 0     | 0.12   |
| Apple     | SSD TS128E         | 121 GB | 8       | 84    | 24    | 0.12   |
| BAITITON  | BT58SSD11S         | 480 GB | 2       | 42    | 0     | 0.12   |
| Kingston  | SKC6002048G        | 2 TB   | 6       | 52    | 11    | 0.12   |
| VISIPRO   | SDVPSS21R0128      | 128 GB | 1       | 42    | 0     | 0.12   |
| Zheino    | CHN-25SATAS3-128   | 128 GB | 1       | 42    | 0     | 0.12   |
| SanDisk   | SD8SBAT128G1002    | 128 GB | 4       | 42    | 0     | 0.12   |
| Micron    | MTFDDAT256MAM-1K2  | 256 GB | 3       | 597   | 337   | 0.12   |
| KingSpec  | NT-64              | 64 GB  | 1       | 41    | 0     | 0.11   |
| AMD       | R3SL60G            | 64 GB  | 5       | 156   | 87    | 0.11   |
| PNY       | SSD2SC240G1SA75... | 240 GB | 4       | 43    | 22    | 0.11   |
| Dogfish   | SSD                | 128 GB | 12      | 41    | 0     | 0.11   |
| Transcend | TS256GMTS950T      | 256 GB | 1       | 41    | 0     | 0.11   |
| V-GeN     | V-GEN08SM20AR12... | 128 GB | 1       | 41    | 0     | 0.11   |
| GSemi     | GSDSM256TY2F1QGCX  | 256 GB | 2       | 41    | 0     | 0.11   |
| Varro     | BULLDOZER-240GB    | 240 GB | 1       | 41    | 0     | 0.11   |
| Phison    | SSEP128GTMC0-S10C  | 128 GB | 1       | 41    | 0     | 0.11   |
| Dogfish   | SSD                | 120 GB | 2       | 41    | 0     | 0.11   |
| Intel     | SSDSC2KF480H6L     | 480 GB | 1       | 82    | 1     | 0.11   |
| Goodram   | SSDPR-CL100-120-G3 | 120 GB | 15      | 41    | 0     | 0.11   |
| Team      | T253X1240G         | 240 GB | 11      | 41    | 0     | 0.11   |
| Lite-On   | LMT-128M6M         | 128 GB | 3       | 40    | 0     | 0.11   |
| China     | SSD 128G           | 128 GB | 8       | 40    | 0     | 0.11   |
| Kingston  | SKC600512G         | 512 GB | 21      | 40    | 0     | 0.11   |
| KIOXIA... | SATA SSD           | 240 GB | 18      | 40    | 0     | 0.11   |
| Phison    | S11-256G-PHISON... | 256 GB | 3       | 40    | 0     | 0.11   |
| ADATA     | SU650NS38          | 240 GB | 11      | 40    | 0     | 0.11   |
| Goodram   | SSDPR-S400U-120-80 | 120 GB | 1       | 40    | 0     | 0.11   |
| Kingston  | SH103S3480G        | 480 GB | 1       | 40    | 0     | 0.11   |
| Dogeish   | SSD                | 128 GB | 1       | 40    | 0     | 0.11   |
| Valuetech | 256GB SSD          | 256 GB | 1       | 40    | 0     | 0.11   |
| Smart     | SSD                | 256 GB | 1       | 40    | 0     | 0.11   |
| Lexar     | SSD                | 240 GB | 4       | 39    | 0     | 0.11   |
| LDLC      | SSD                | 240 GB | 3       | 39    | 0     | 0.11   |
| KingDian  | P10                | 240 GB | 1       | 39    | 0     | 0.11   |
| Seagate   | ST480HM000         | 480 GB | 1       | 39    | 0     | 0.11   |
| Hoodisk   | SSD                | 256 GB | 7       | 39    | 0     | 0.11   |
| ADATA     | SU800NS38          | 1 TB   | 6       | 39    | 0     | 0.11   |
| MediaR... | MR1002             | 240 GB | 1       | 39    | 0     | 0.11   |
| Lite-On   | LMT-128M6M-HP      | 128 GB | 1       | 39    | 0     | 0.11   |
| Lite-On   | CMT-64L3M          | 64 GB  | 4       | 138   | 528   | 0.11   |
| Transcend | TS512GSSD230S      | 512 GB | 7       | 39    | 0     | 0.11   |
| Transcend | TS64GSSD720        | 64 GB  | 1       | 194   | 4     | 0.11   |
| PNY       | SSD2SC120G3LC70... | 120 GB | 2       | 390   | 510   | 0.11   |
| PNY       | CS1211 480GB SS... | 480 GB | 1       | 38    | 0     | 0.11   |
| ADATA     | SU655              | 480 GB | 2       | 38    | 0     | 0.11   |
| China     | 1TB PCS 2.5" SSD   | 1 TB   | 2       | 38    | 0     | 0.11   |
| China     | 1TB SSD            | 1 TB   | 2       | 38    | 0     | 0.11   |
| Transcend | TS64GSSD370S       | 64 GB  | 5       | 38    | 0     | 0.11   |
| RX7       | SSD                | 256 GB | 1       | 38    | 0     | 0.11   |
| Intenso   | JAJM600M128C       | 128 GB | 2       | 38    | 0     | 0.10   |
| Toshiba   | THNSNK512GVN8      | 512 GB | 1       | 38    | 0     | 0.10   |
| Intenso   | SSD Sata III       | 128 GB | 23      | 43    | 178   | 0.10   |
| Intenso   | SATA3 256GB SSD    | 256 GB | 3       | 38    | 0     | 0.10   |
| Lexar     | 960GB SSD          | 960 GB | 1       | 38    | 0     | 0.10   |
| Verbatim  | Vi560 SATA III ... | 256 GB | 1       | 38    | 0     | 0.10   |
| KingSpec  | P4-120             | 120 GB | 7       | 38    | 0     | 0.10   |
| Neo Forza | NFS011SA396-600... | 960 GB | 1       | 341   | 8     | 0.10   |
| Zheino    | CHN-mSATAM3-128    | 128 GB | 1       | 37    | 0     | 0.10   |
| Dogfish   | SSD                | 256 GB | 11      | 39    | 1     | 0.10   |
| Drevo     | X1-60G             | 64 GB  | 1       | 37    | 0     | 0.10   |
| BAITITON  | BT58SSD15S         | 2 TB   | 1       | 37    | 0     | 0.10   |
| Zheino    | CHN-mSATAQ3-480    | 480 GB | 1       | 37    | 0     | 0.10   |
| minisf... | SSD                | 128 GB | 1       | 37    | 0     | 0.10   |
| BAITITON  | BT58SSD10N         | 256 GB | 1       | 37    | 0     | 0.10   |
| SanDisk   | SDSSDHP64G         | 64 GB  | 1       | 37    | 0     | 0.10   |
| Intel     | SSDSA1M160G2LE     | 160 GB | 1       | 482   | 12    | 0.10   |
| Innodisk  | Corp. - mSATA 3ME4 | 64 GB  | 2       | 615   | 49    | 0.10   |
| Hikvision | HS-SSD-E100 1024G  | 1 TB   | 4       | 36    | 0     | 0.10   |
| SCY       | N10C               | 256 GB | 1       | 36    | 0     | 0.10   |
| Silico... | AAR512GS021022030  | 512 GB | 1       | 36    | 0     | 0.10   |
| Transcend | TS512GMSA370       | 512 GB | 2       | 36    | 0     | 0.10   |
| Samsung   | MZNLH256HAJD-000L7 | 256 GB | 2       | 36    | 0     | 0.10   |
| Corsair   | Neutron GTX SSD    | 120 GB | 6       | 1038  | 114   | 0.10   |
| TOPMORE   | TU200 240GB SSD    | 240 GB | 1       | 36    | 0     | 0.10   |
| SanDisk   | WD Green 2.5       | 1 TB   | 3       | 104   | 3     | 0.10   |
| BR        | SSD                | 240 GB | 1       | 36    | 0     | 0.10   |
| Vaseky    | V900-256G          | 256 GB | 1       | 36    | 0     | 0.10   |
| China     | 2.5'' SSD          | 120 GB | 1       | 36    | 0     | 0.10   |
| GLOWAY    | FER120GS3-S7       | 120 GB | 6       | 48    | 1     | 0.10   |
| Lite-On   | LCH-256V2S-11 2... | 256 GB | 6       | 49    | 1     | 0.10   |
| BIWIN     | SSD                | 256 GB | 4       | 35    | 0     | 0.10   |
| SK hynix  | SC401 SATA         | 512 GB | 8       | 204   | 362   | 0.10   |
| OYUNKEY   | SSD                | 120 GB | 2       | 215   | 66    | 0.10   |
| NTC       | SSD                | 240 GB | 1       | 35    | 0     | 0.10   |
| PNY       | SSD2SC120G726A1... | 120 GB | 1       | 35    | 0     | 0.10   |
| SK hynix  | HFS1T9G32FEH-7A10A | 1.9 TB | 3       | 35    | 0     | 0.10   |
| Lite-On   | LSS-32L6G-HP       | 32 GB  | 5       | 128   | 204   | 0.10   |
| SanDisk   | X600 2.5 7MM SATA  | 256 GB | 1       | 35    | 0     | 0.10   |
| Transcend | TS256GMSA370       | 256 GB | 1       | 35    | 0     | 0.10   |
| Biostar   | S100-120GB         | 120 GB | 3       | 35    | 0     | 0.10   |
| China     | SSD                | 360 GB | 18      | 44    | 4     | 0.10   |
| Transcend | TS32GSSD370S       | 32 GB  | 16      | 35    | 0     | 0.10   |
| Hanye     | W400-256GMP01      | 256 GB | 1       | 35    | 0     | 0.10   |
| Zheino    | CHN 25SATAS3 256   | 256 GB | 2       | 34    | 0     | 0.10   |
| TakeMS    | SSD UTX-2200       | 240 GB | 1       | 34    | 0     | 0.10   |
| Innodisk  | Corp. - mSATA 3... | 128 GB | 1       | 34    | 0     | 0.10   |
| RESCUE    | RESCUE08SM22AR1... | 120 GB | 1       | 34    | 0     | 0.10   |
| Toshiba   | KHK61RSE1T92       | 1.9 TB | 8       | 34    | 0     | 0.10   |
| Faspeed   | K7-512G-CD         | 512 GB | 1       | 34    | 0     | 0.10   |
| PNY       | SSD2SC240G1LC70... | 240 GB | 2       | 34    | 0     | 0.10   |
| Plextor   | PX-64M5M           | 64 GB  | 1       | 34    | 0     | 0.10   |
| Netac     | SSD0128S00         | 128 GB | 1       | 34    | 0     | 0.09   |
| HP        | SSD S600           | 240 GB | 7       | 38    | 1     | 0.09   |
| ZOTAC     | SATA SSD           | 120 GB | 2       | 34    | 0     | 0.09   |
| SanDisk   | SD8SN8U128G1122    | 128 GB | 1       | 34    | 0     | 0.09   |
| BHT       | WR202H0032G E70... | 32 GB  | 2       | 34    | 0     | 0.09   |
| Samsung   | MZ7L3960HBLT-00A07 | 960 GB | 1       | 34    | 0     | 0.09   |
| Leven     | JAJS600M128C       | 128 GB | 7       | 34    | 0     | 0.09   |
| SMI       | SSD DISK           | 256 GB | 1       | 34    | 0     | 0.09   |
| SK hynix  | HFS250G32TND-N1A2A | 250 GB | 2       | 65    | 1029  | 0.09   |
| AMD       | R5S240GBSF         | 240 GB | 1       | 33    | 0     | 0.09   |
| Intel     | SSDSC2KW120H6      | 120 GB | 8       | 66    | 36    | 0.09   |
| Intel     | SSDSA1MH080G1HP    | 80 GB  | 1       | 33    | 0     | 0.09   |
| RECADATA  | RD-S325MCN-N2563   | 240 GB | 1       | 33    | 0     | 0.09   |
| AEGO      | SSD                | 240 GB | 3       | 33    | 0     | 0.09   |
| PUSKILL   | SSD                | 512 GB | 1       | 33    | 0     | 0.09   |
| SMI       | SSD DISK           | 497 GB | 1       | 33    | 0     | 0.09   |
| QUMO      | Q3DT-128GMCY       | 128 GB | 1       | 33    | 0     | 0.09   |
| Dogfish   | SSD                | 1 TB   | 6       | 33    | 0     | 0.09   |
| XrayDisk  | 512GB SSD          | 512 GB | 4       | 42    | 253   | 0.09   |
| KingSpec  | ACSC2M064mSA       | 64 GB  | 2       | 33    | 0     | 0.09   |
| MidasF... | SSD                | 240 GB | 1       | 33    | 0     | 0.09   |
| SK hynix  | HFS960G32FEH-7A10A | 960 GB | 2       | 33    | 0     | 0.09   |
| GeIL      | Z3_128GB           | 128 GB | 1       | 33    | 0     | 0.09   |
| Super ... | FNX256MORM         | 256 GB | 2       | 32    | 0     | 0.09   |
| KeepData  | GIM128             | 128 GB | 3       | 32    | 0     | 0.09   |
| Corsair   | CSSD-F120GB3-BK    | 120 GB | 2       | 58    | 509   | 0.09   |
| Samsung   | SSD PM851          | 128 GB | 1       | 32    | 0     | 0.09   |
| KingSpec  | ACSC4M512mSA       | 506 GB | 1       | 32    | 0     | 0.09   |
| Lite-On   | L8T-256L9G-11 M... | 256 GB | 2       | 32    | 0     | 0.09   |
| OCZ       | VERTEX4            | 80 GB  | 1       | 129   | 3     | 0.09   |
| Intenso   | JAJM600M1TB        | 1 TB   | 4       | 32    | 0     | 0.09   |
| Lite-On   | L8T-128L6G-HP      | 128 GB | 2       | 32    | 640   | 0.09   |
| Phison    | SSEP064GTMC0-S91   | 64 GB  | 1       | 32    | 0     | 0.09   |
| KIOXIA... | SATA SSD           | 480 GB | 21      | 32    | 0     | 0.09   |
| Teclast   | 256GB NS550-2242   | 256 GB | 13      | 32    | 0     | 0.09   |
| HEORIADY  | HX-001 F 512G      | 512 GB | 2       | 32    | 0     | 0.09   |
| OSCOO     | OSC SSD            | 512 GB | 1       | 32    | 0     | 0.09   |
| Toshiba   | THNSNB062GMCJ      | 64 GB  | 1       | 32    | 0     | 0.09   |
| Goodram   | SSDPR-CX400-256-G2 | 256 GB | 25      | 31    | 0     | 0.09   |
| Mushkin   | MKNSSDS21TB        | 1 TB   | 12      | 35    | 26    | 0.09   |
| Lite-On   | LCH-128V2S         | 128 GB | 4       | 31    | 0     | 0.09   |
| Hyundai   | C2S3T-240G         | 240 GB | 4       | 31    | 0     | 0.09   |
| SK hynix  | SC313 SATA         | 256 GB | 1       | 31    | 0     | 0.09   |
| Transcend | TS1TMTS800         | 1 TB   | 1       | 31    | 0     | 0.09   |
| Transcend | TS512GMTS400       | 512 GB | 1       | 31    | 0     | 0.09   |
| SUNEAST   | SSD SE800          | 512 GB | 1       | 31    | 0     | 0.09   |
| Varro     | BULLDOZER-120GB    | 120 GB | 1       | 31    | 0     | 0.09   |
| China     | NGFF 2280 128GB... | 128 GB | 5       | 31    | 0     | 0.09   |
| China     | SH00R120GB         | 120 GB | 4       | 31    | 0     | 0.09   |
| SPCC      | 2.5Ў± SSD        | 1 TB   | 1       | 31    | 0     | 0.09   |
| Drevo     | X1 pro 256G        | 256 GB | 1       | 31    | 0     | 0.09   |
| China     | T480               | 480 GB | 2       | 65    | 138   | 0.09   |
| Mushkin   | MKNSSDRE512GB      | 512 GB | 1       | 31    | 0     | 0.09   |
| Lite-On   | CV1-CC256          | 256 GB | 3       | 31    | 0     | 0.09   |
| KingSpec  | KSD-SA25.7-016MJ   | 16 GB  | 2       | 30    | 0     | 0.08   |
| Leven     | JAJS300M480C       | 480 GB | 3       | 44    | 1     | 0.08   |
| Colorful  | SL500              | 480 GB | 3       | 38    | 65    | 0.08   |
| Micron    | MTFDDAK256MAY-1... | 256 GB | 5       | 717   | 81    | 0.08   |
| Qumo      | SSD                | 120 GB | 4       | 175   | 255   | 0.08   |
| CFD       | CSSD-S6B480CG3VX   | 480 GB | 1       | 30    | 0     | 0.08   |
| Lite-On   | LCH-512V2S-11 2... | 512 GB | 2       | 30    | 0     | 0.08   |
| Lite-On   | CV3-SD512          | 512 GB | 2       | 30    | 0     | 0.08   |
| Hikvision | HKVSN HS-SSD-C1... | 120 GB | 1       | 30    | 0     | 0.08   |
| SK hynix  | HFS480G32FEH-BA10A | 480 GB | 1       | 30    | 0     | 0.08   |
| Imation   | 2.5" SATA3 240G... | 240 GB | 1       | 30    | 0     | 0.08   |
| KINGBANK  | KP320              | 128 GB | 2       | 30    | 0     | 0.08   |
| Kingston  | OM8P0S3512B-A0     | 512 GB | 1       | 29    | 0     | 0.08   |
| Lite-On   | LST-32S9G-11 SATA  | 32 GB  | 3       | 29    | 0     | 0.08   |
| Intel     | SSDSA2M160G2LE     | 160 GB | 5       | 517   | 16    | 0.08   |
| KingPower | 1108 SSD           | 64 GB  | 1       | 29    | 0     | 0.08   |
| Lite-On   | LMT-64M6M-HP       | 64 GB  | 2       | 102   | 507   | 0.08   |
| Netac     | SSD 128G           | 128 GB | 1       | 29    | 0     | 0.08   |
| Lite-On   | LMH-128V2M-11 M... | 128 GB | 3       | 29    | 0     | 0.08   |
| Lite-On   | LMT-512L9M-11 M... | 512 GB | 1       | 29    | 0     | 0.08   |
| Innodisk  | 2.5" SATA SSD 3... | 64 GB  | 3       | 29    | 0     | 0.08   |
| Win Me... | SWR128G-001HL      | 128 GB | 1       | 29    | 0     | 0.08   |
| Intenso   | SSD256GBS420       | 256 GB | 4       | 29    | 0     | 0.08   |
| ADATA     | SU800NS38          | 256 GB | 29      | 45    | 116   | 0.08   |
| China     | R580               | 64 GB  | 1       | 146   | 4     | 0.08   |
| KingFast  | SSD                | 2 TB   | 1       | 29    | 0     | 0.08   |
| Patriot   | SDVPSA1910128      | 128 GB | 1       | 29    | 0     | 0.08   |
| Kingston  | RBUSC180DS37256GH  | 256 GB | 1       | 29    | 0     | 0.08   |
| Kingston  | SKC600MS1024G      | 1 TB   | 2       | 29    | 0     | 0.08   |
| Samsung   | SSD Thin uSATA ... | 128 GB | 1       | 378   | 12    | 0.08   |
| Toshiba   | THNSNS128GMCP      | 128 GB | 2       | 29    | 0     | 0.08   |
| Micron    | M600 M.2 2280      | 512 GB | 1       | 29    | 0     | 0.08   |
| BHT       | WR202I0064G E70... | 64 GB  | 9       | 28    | 0     | 0.08   |
| China     | Solid              | 480 GB | 5       | 33    | 24    | 0.08   |
| PUSKILL   | SSD                | 256 GB | 1       | 28    | 0     | 0.08   |
| Lite-On   | LMS-32L6M          | 32 GB  | 1       | 28    | 0     | 0.08   |
| Transcend | TS128GSSD25S-M     | 128 GB | 1       | 28    | 0     | 0.08   |
| China     | SSD120G            | 120 GB | 1       | 28    | 0     | 0.08   |
| China     | Mit-SSD512A        | 512 GB | 1       | 28    | 0     | 0.08   |
| Gateway   | W800SH 512GB SSD   | 512 GB | 3       | 28    | 0     | 0.08   |
| Wdstars   | ssd nowm720A-512GB | 512 GB | 1       | 28    | 0     | 0.08   |
| KingSpec  | MSH-128            | 128 GB | 2       | 28    | 0     | 0.08   |
| Hyundai   | C2S3T-120          | 120 GB | 1       | 27    | 0     | 0.08   |
| Indilinx  | IND-S325S-256G     | 256 GB | 1       | 27    | 0     | 0.08   |
| China     | S500               | 512 GB | 3       | 27    | 0     | 0.08   |
| Kingmax   | SSD                | 64 GB  | 24      | 196   | 521   | 0.08   |
| SanDisk   | SDSSDX480GG25      | 480 GB | 5       | 999   | 405   | 0.08   |
| Foxline   | FLSSD512X5         | 512 GB | 3       | 27    | 0     | 0.08   |
| TAISU     | SSD 240G           | 240 GB | 1       | 27    | 0     | 0.08   |
| Intenso   | AFK-120GB          | 120 GB | 1       | 27    | 0     | 0.08   |
| V-GeN     | V-GEN07SM20AR12... | 128 GB | 1       | 27    | 0     | 0.08   |
| Tammuz    | RX440              | 120 GB | 1       | 27    | 0     | 0.08   |
| V-GeN     | V-GEN03SM22AR10... | 1 TB   | 1       | 27    | 0     | 0.08   |
| SPCC      | M.2 SSD            | 1 TB   | 3       | 30    | 904   | 0.08   |
| SenDisk   | C3-60G             | 64 GB  | 1       | 27    | 0     | 0.08   |
| Lite-On   | CV1-8B256-HP       | 256 GB | 4       | 27    | 0     | 0.08   |
| Patriot   | P210               | 1 TB   | 2       | 27    | 0     | 0.07   |
| TEXTORM   | BM5                | 240 GB | 3       | 27    | 0     | 0.07   |
| Lenovo    | Thinklife SSD S... | 480 GB | 1       | 27    | 0     | 0.07   |
| Team      | T253X6002T         | 2 TB   | 1       | 27    | 0     | 0.07   |
| KingSpec  | CHA-M2B7-M256      | 256 GB | 2       | 27    | 0     | 0.07   |
| Zheino    | CHN 25SATA01M 120  | 120 GB | 1       | 26    | 0     | 0.07   |
| SK hynix  | HFS256G32MND-2200A | 256 GB | 7       | 338   | 88    | 0.07   |
| Micron    | 5200_MTFDDAK960TDC | 960 GB | 1       | 26    | 0     | 0.07   |
| Pioneer   | APS-SL3N 120       | 120 GB | 1       | 26    | 0     | 0.07   |
| China     | CIE M8 M350 128... | 128 GB | 1       | 26    | 0     | 0.07   |
| HECTRON   | HECX1-240G         | 240 GB | 1       | 26    | 0     | 0.07   |
| Micron    | MTFDDAK128MAY-1... | 128 GB | 5       | 451   | 16    | 0.07   |
| SK hynix  | HFS1T9G3H2X069N    | 1.9 TB | 2       | 26    | 0     | 0.07   |
| BHT       | WR202HH032G E70... | 32 GB  | 2       | 26    | 0     | 0.07   |
| Netac     | SSD                | 64 GB  | 2       | 26    | 0     | 0.07   |
| QUMO      | Q3DT-256GSCY       | 256 GB | 2       | 26    | 0     | 0.07   |
| Kingspeed | SATA3-256GB        | 256 GB | 1       | 26    | 0     | 0.07   |
| Hikvision | HS-SSD-E100N 512G  | 512 GB | 1       | 26    | 0     | 0.07   |
| Plextor   | PX-256M6GV-2280    | 256 GB | 1       | 26    | 0     | 0.07   |
| Toshiba   | THNSNS128GCSP      | 128 GB | 1       | 26    | 0     | 0.07   |
| Netac     | SSD                | 256 GB | 64      | 29    | 3     | 0.07   |
| ExeGate   | EX276687RUS        | 120 GB | 1       | 26    | 0     | 0.07   |
| Lite-On   | LMH-512V2M-11 M... | 512 GB | 1       | 26    | 0     | 0.07   |
| Lenovo    | SSD SL700          | 1 TB   | 2       | 26    | 0     | 0.07   |
| Phison    | S11-128G-PHISON... | 128 GB | 6       | 26    | 0     | 0.07   |
| SK hynix  | HFS256G32MND-3310A | 256 GB | 1       | 25    | 0     | 0.07   |
| ADATA     | SU750              | 1 TB   | 3       | 79    | 674   | 0.07   |
| Pasoul    | OASDX-120G         | 120 GB | 1       | 25    | 0     | 0.07   |
| TwinMOS   | SSD                | 128 GB | 1       | 77    | 2     | 0.07   |
| KingSpec  | T-120              | 120 GB | 1       | 25    | 0     | 0.07   |
| Wdxsky    | M720k-128G         | 128 GB | 1       | 25    | 0     | 0.07   |
| SanDisk   | SD6SB1M-032G-1006  | 32 GB  | 2       | 25    | 0     | 0.07   |
| Advantech | SQF-S25M8-256G-SAC | 256 GB | 1       | 25    | 0     | 0.07   |
| China     | 2000GB SSD         | 2 TB   | 1       | 25    | 0     | 0.07   |
| Lite-On   | LMH-256V2M-41 M... | 256 GB | 1       | 25    | 0     | 0.07   |
| Samsung   | MZ7L3480HCHQ-00A07 | 480 GB | 1       | 25    | 0     | 0.07   |
| Goodram   | IRP-SSDPR-S25C-512 | 512 GB | 4       | 24    | 0     | 0.07   |
| Lite-On   | CV3-CE256-HP       | 256 GB | 1       | 24    | 0     | 0.07   |
| Lite-On   | CV5-8Q256          | 256 GB | 1       | 24    | 0     | 0.07   |
| Dell      | WR202KD032G E70... | 32 GB  | 6       | 24    | 0     | 0.07   |
| Corsair   | CSSD-V32GB2        | 32 GB  | 1       | 99    | 3     | 0.07   |
| Intel     | SSDSC2KF256H6L     | 256 GB | 12      | 75    | 32    | 0.07   |
| Colorful  | SL300              | 64 GB  | 1       | 24    | 0     | 0.07   |
| RAMOS     | SSD                | 256 GB | 1       | 24    | 0     | 0.07   |
| V-GeN     | V-GEN01SM21AR10... | 1 TB   | 1       | 24    | 0     | 0.07   |
| Kingston  | SKC600MS512G       | 512 GB | 4       | 24    | 0     | 0.07   |
| Plextor   | PX-128S2C          | 128 GB | 2       | 24    | 0     | 0.07   |
| Kingch... | SSD                | 1 TB   | 1       | 24    | 0     | 0.07   |
| HP        | SSD S750           | 512 GB | 2       | 24    | 0     | 0.07   |
| SanDisk   | WD easystore       | 240 GB | 9       | 24    | 0     | 0.07   |
| Team      | L5 LITE SSD        | 64 GB  | 3       | 27    | 1     | 0.07   |
| PNY       | SSD2SC120G1CS17... | 120 GB | 3       | 24    | 0     | 0.07   |
| Patriot   | Memory 32GB PAT... | 32 GB  | 1       | 24    | 0     | 0.07   |
| KingDian  | N400               | 32 GB  | 2       | 24    | 0     | 0.07   |
| Kingston  | OM8P0S3256B-A0     | 256 GB | 7       | 24    | 0     | 0.07   |
| Patriot   | P210               | 2 TB   | 1       | 23    | 0     | 0.07   |
| Samsung   | MZNLN512HCJH-000L2 | 512 GB | 1       | 23    | 0     | 0.07   |
| SanDisk   | SSD i110           | 128 GB | 3       | 23    | 0     | 0.07   |
| Star D... | SATA SSD           | 240 GB | 4       | 23    | 0     | 0.07   |
| SNR       | ML 240             | 240 GB | 1       | 23    | 0     | 0.07   |
| FORESEE   | 512GB SSD          | 512 GB | 5       | 23    | 0     | 0.07   |
| Colorful  | SL300              | 120 GB | 3       | 65    | 13    | 0.07   |
| PNY       | SSD2SC120G1SA75... | 120 GB | 1       | 23    | 0     | 0.07   |
| Plextor   | PX-128S1G          | 128 GB | 2       | 23    | 0     | 0.07   |
| BR        | SSD                | 256 GB | 1       | 23    | 0     | 0.06   |
| Transcend | TS32GMSA310        | 32 GB  | 1       | 47    | 1     | 0.06   |
| Samsung   | MZ7WD480HMHP-00003 | 480 GB | 1       | 941   | 39    | 0.06   |
| Teclast   | 360GB A850         | 360 GB | 1       | 257   | 10    | 0.06   |
| Plextor   | PX-512M6S          | 512 GB | 2       | 23    | 0     | 0.06   |
| addlink   | SATA SSD           | 1 TB   | 1       | 23    | 0     | 0.06   |
| PNY       | SSD2SC256GM1P3D... | 256 GB | 2       | 23    | 0     | 0.06   |
| EMTEC     | X150               | 120 GB | 4       | 23    | 0     | 0.06   |
| EAGET     | SSD 120G           | 128 GB | 1       | 23    | 0     | 0.06   |
| Kingch... | SSD                | 32 GB  | 1       | 23    | 0     | 0.06   |
| Lite-On   | CS1-SP16           | 16 GB  | 1       | 23    | 0     | 0.06   |
| Seagate   | QSCD-ST52570-128GB | 128 GB | 1       | 23    | 0     | 0.06   |
| Micron    | MTFDDAK512TBN-1... | 512 GB | 3       | 322   | 8     | 0.06   |
| TCSUNBOW  | N4                 | 240 GB | 1       | 22    | 0     | 0.06   |
| Intel     | SSDSA1M080G2HP     | 80 GB  | 2       | 342   | 17    | 0.06   |
| Foxline   | FLSSD512X5SE       | 512 GB | 2       | 22    | 0     | 0.06   |
| China     | SATA3 64GB SSD     | 64 GB  | 1       | 22    | 0     | 0.06   |
| FORESEE   | 256GB SSD          | 256 GB | 15      | 22    | 0     | 0.06   |
| Lite-On   | IT LCS-256L9S-HP   | 256 GB | 1       | 113   | 4     | 0.06   |
| Lite-On   | CV1-8B512-HP       | 512 GB | 3       | 22    | 0     | 0.06   |
| Toshiba   | THNSNS060GBSP      | 64 GB  | 1       | 22    | 0     | 0.06   |
| China     | NGFF 2280 256GB... | 256 GB | 15      | 33    | 4     | 0.06   |
| China     | ESA3SMH2ISTBT120GB | 120 GB | 1       | 1645  | 72    | 0.06   |
| Kingston  | 480GBV500          | 480 GB | 1       | 22    | 0     | 0.06   |
| SPCC      | SPCCSolidStateDisk | 128 GB | 1       | 292   | 12    | 0.06   |
| PNY       | SSD2SC240G1SAHT... | 240 GB | 3       | 22    | 0     | 0.06   |
| China     | SSD-1TB            | 1 TB   | 1       | 22    | 0     | 0.06   |
| Transcend | TS128GMSM360       | 128 GB | 1       | 22    | 0     | 0.06   |
| Zheino    | CHN25SATAS1 256    | 256 GB | 1       | 22    | 0     | 0.06   |
| Apacer    | 64GB SATA Flash... | 64 GB  | 1       | 22    | 0     | 0.06   |
| Apacer    | 512GB SATA SSD     | 512 GB | 1       | 22    | 0     | 0.06   |
| LDLC      | F6+M.2 240         | 240 GB | 1       | 22    | 0     | 0.06   |
| China     | QSSEA227512GDS     | 512 GB | 1       | 22    | 0     | 0.06   |
| TMI       | 256GB M2 CRMP.4... | 256 GB | 1       | 22    | 0     | 0.06   |
| Gigastone | Prime Series       | 256 GB | 1       | 22    | 0     | 0.06   |
| Lite-On   | LCH-128V2S-HP      | 128 GB | 3       | 163   | 16    | 0.06   |
| ELSKY     | SSD 64G            | 64 GB  | 1       | 21    | 0     | 0.06   |
| Samsung   | MZNLN512HAJQ-000   | 512 GB | 1       | 21    | 0     | 0.06   |
| SK hynix  | HFS1T9G32FEH-BA10A | 1.9 TB | 2       | 21    | 0     | 0.06   |
| Kingston  | OM8P0S3128B-A0     | 128 GB | 1       | 21    | 0     | 0.06   |
| Silicon   | T60                | 64 GB  | 1       | 21    | 0     | 0.06   |
| Samsung   | MZMPA128HMFU-000H1 | 128 GB | 4       | 287   | 1374  | 0.06   |
| OCZ       | INTREPID 3600      | 400 GB | 1       | 21    | 0     | 0.06   |
| GLOWAY    | STK4TS3-S7         | 4 TB   | 1       | 21    | 0     | 0.06   |
| OSCOO     | OSC mSATA          | 256 GB | 1       | 21    | 0     | 0.06   |
| Kingston  | HyperX Fury 3D     | 120 GB | 5       | 21    | 0     | 0.06   |
| Lite-On   | LMT-256L9M-41 M... | 256 GB | 1       | 21    | 0     | 0.06   |
| AFOX      | SSD SD250-1000GB   | 1 TB   | 1       | 21    | 0     | 0.06   |
| Samsung   | MZ7L33T8HBLT-00... | 3.8 TB | 2       | 21    | 0     | 0.06   |
| Seagate   | STT256I1-2ZAA6G2   | 240 GB | 1       | 21    | 0     | 0.06   |
| Intel     | SSDSCKKF256H6 SATA | 256 GB | 9       | 73    | 20    | 0.06   |
| Drevo     | X1 Pro SSD         | 128 GB | 1       | 234   | 10    | 0.06   |
| ORTIAL    | SSD                | 256 GB | 7       | 21    | 0     | 0.06   |
| Samsung   | SSD PM810 2.5" 7mm | 256 GB | 4       | 339   | 528   | 0.06   |
| Kingston  | SA400S37           | 240 GB | 1       | 21    | 0     | 0.06   |
| Team      | T253X5960G         | 960 GB | 1       | 21    | 0     | 0.06   |
| China     | C500               | 128 GB | 3       | 21    | 0     | 0.06   |
| China     | AC211-480GB        | 480 GB | 1       | 20    | 0     | 0.06   |
| Intel     | SSDSC2KB240G8L ... | 240 GB | 2       | 20    | 0     | 0.06   |
| Lumino... | SSD                | 512 GB | 1       | 20    | 0     | 0.06   |
| Transcend | TS64GMSA230S       | 64 GB  | 2       | 20    | 0     | 0.06   |
| GHIA      | GM2256G            | 256 GB | 1       | 20    | 0     | 0.06   |
| Goldkey   | GKH84-256GB        | 256 GB | 1       | 20    | 0     | 0.06   |
| China     | SK                 | 256 GB | 2       | 20    | 0     | 0.06   |
| Toshiba   | THNSNS064GMCP      | 64 GB  | 1       | 20    | 0     | 0.06   |
| INNOVA... | SSD_2.5"_TLC_25... | 256 GB | 3       | 20    | 0     | 0.06   |
| China     | SSD                | 96 GB  | 1       | 20    | 0     | 0.06   |
| PNY       | CS1311 32GB SSD    | 32 GB  | 2       | 20    | 0     | 0.06   |
| Intel     | SSDSC2KR120H6      | 120 GB | 1       | 20    | 0     | 0.06   |
| RZX       | 19SSD6G-120GB      | 120 GB | 1       | 20    | 0     | 0.06   |
| Corsair   | Force LX SSD       | 256 GB | 2       | 20    | 0     | 0.06   |
| Hikvision | HS-SSD-E100 128G   | 128 GB | 5       | 37    | 1     | 0.05   |
| EMTEC     | X150               | 960 GB | 2       | 20    | 0     | 0.05   |
| Mushkin   | MKNSSDTR240GB      | 240 GB | 2       | 20    | 0     | 0.05   |
| XUNZHE    | XUNZHE800S 120G    | 120 GB | 1       | 20    | 0     | 0.05   |
| HEORIADY  | HX-001 E           | 128 GB | 1       | 20    | 0     | 0.05   |
| SanDisk   | SD7SN3Q-256G-1006  | 256 GB | 1       | 499   | 24    | 0.05   |
| Seagate   | XA1920LE10063      | 1.9 TB | 4       | 19    | 0     | 0.05   |
| Colorful  | SL300              | 128 GB | 3       | 35    | 337   | 0.05   |
| Crucial   | CT512M550SSD4      | 512 GB | 1       | 338   | 16    | 0.05   |
| AFOX      | SSD                | 500 GB | 1       | 19    | 0     | 0.05   |
| SanDisk   | SDSA5GK-016G-1006  | 16 GB  | 2       | 157   | 53    | 0.05   |
| Kingston  | SSD 128G           | 128 GB | 1       | 19    | 0     | 0.05   |
| BlueRay   | SDM8SI240A         | 240 GB | 1       | 19    | 0     | 0.05   |
| Vaseky    | V850-64G           | 64 GB  | 1       | 19    | 0     | 0.05   |
| Transcend | TS32GHSD370        | 32 GB  | 1       | 19    | 0     | 0.05   |
| Micron    | MTFDDAV256TBN      | 256 GB | 2       | 65    | 8     | 0.05   |
| SanDisk   | SD8SB8U128G1122    | 128 GB | 1       | 19    | 0     | 0.05   |
| DUEX      | DX300256A5xnEMLC   | 256 GB | 1       | 1077  | 54    | 0.05   |
| Force Le  | 200                | 240 GB | 1       | 19    | 0     | 0.05   |
| Kingston  | 120GBV500          | 120 GB | 1       | 19    | 0     | 0.05   |
| JUMPER    | SSD 256G           | 256 GB | 2       | 19    | 0     | 0.05   |
| Avant     | NCSC51AD240M4P     | 240 GB | 1       | 19    | 0     | 0.05   |
| Gigaby... | GP-GSTFS31256GTND  | 256 GB | 3       | 19    | 0     | 0.05   |
| SK hynix  | HFS128G32MND-2200A | 128 GB | 3       | 264   | 128   | 0.05   |
| AMD       | R5SL128G           | 128 GB | 7       | 19    | 0     | 0.05   |
| Corsair   | CSSD-F80GB2-A      | 80 GB  | 1       | 18    | 0     | 0.05   |
| Dell      | WR202KD128G E70... | 128 GB | 1       | 18    | 0     | 0.05   |
| Transcend | TS32GMTS800        | 32 GB  | 1       | 18    | 0     | 0.05   |
| Intel     | SSDSCKJF240A5L     | 240 GB | 2       | 84    | 6     | 0.05   |
| Intenso   | SSD                | 1 TB   | 3       | 18    | 0     | 0.05   |
| Kimtigo   | SSD                | 128 GB | 4       | 18    | 0     | 0.05   |
| Micron    | MTFDDAK512MAY-1... | 512 GB | 2       | 476   | 528   | 0.05   |
| KODAK     | SSD X120 120G      | 120 GB | 1       | 18    | 0     | 0.05   |
| Corsair   | Neutron SSD        | 240 GB | 1       | 2126  | 114   | 0.05   |
| Team      | T253512GB          | 512 GB | 2       | 18    | 0     | 0.05   |
| Netac     | S535N8-256GYN      | 256 GB | 13      | 18    | 0     | 0.05   |
| ADATA     | SP610              | 256 GB | 1       | 18    | 0     | 0.05   |
| Hyperdisk | SDOM               | 16 GB  | 1       | 18    | 0     | 0.05   |
| UMIS      | RTITJ256VGD2MWDL   | 256 GB | 1       | 18    | 0     | 0.05   |
| Micron    | C300-MTFDDAC064MAG | 64 GB  | 1       | 54    | 2     | 0.05   |
| XrayDisk  | 2TB SSD            | 2 TB   | 1       | 18    | 0     | 0.05   |
| SK hynix  | SC210 mSATA        | 256 GB | 6       | 364   | 57    | 0.05   |
| LDLC      | F6+M.2 120         | 120 GB | 2       | 18    | 0     | 0.05   |
| LDLC      | SSD F6 PLUS M.2... | 960 GB | 2       | 17    | 0     | 0.05   |
| SanDisk   | Extreme Portabl... | 1 TB   | 1       | 17    | 0     | 0.05   |
| Yeyian    | VALK 1500          | 240 GB | 2       | 17    | 0     | 0.05   |
| Samsung   | PM881 SATA         | 512 GB | 1       | 17    | 0     | 0.05   |
| Toshiba   | THNSNJ256GMCT      | 256 GB | 1       | 17    | 0     | 0.05   |
| Yeestor   | SSD                | 512 GB | 1       | 17    | 0     | 0.05   |
| Intel     | SSDSCKJF180A5H ... | 180 GB | 1       | 88    | 4     | 0.05   |
| Leven     | JAJS600M1024C      | 1 TB   | 1       | 17    | 0     | 0.05   |
| QUMO      | SSD                | 240 GB | 3       | 95    | 2     | 0.05   |
| Azerty    | SSD                | 256 GB | 2       | 17    | 0     | 0.05   |
| China     | C-Series 128G S... | 128 GB | 1       | 176   | 9     | 0.05   |
| China     | M.2 SSD            | 256 GB | 5       | 17    | 0     | 0.05   |
| Team      | TM8PS5256G         | 256 GB | 1       | 17    | 0     | 0.05   |
| China     | 60GB SSD           | 64 GB  | 1       | 17    | 0     | 0.05   |
| Mushkin   | MKNSSDE3480GB      | 480 GB | 4       | 17    | 0     | 0.05   |
| Zheino    | CHN 25SATA01M 030  | 32 GB  | 3       | 17    | 0     | 0.05   |
| China     | RTMMB256VBV4KFY    | 256 GB | 1       | 17    | 0     | 0.05   |
| ADATA     | ISSS316-002TCTB4   | 2 TB   | 1       | 17    | 0     | 0.05   |
| ADATA     | SP580M             | 256 GB | 3       | 17    | 0     | 0.05   |
| Kingston  | SA400S37 960G      | 960 GB | 1       | 17    | 0     | 0.05   |
| Kingrich  | 64GB K9 SATA3 SSD  | 64 GB  | 2       | 17    | 0     | 0.05   |
| AMD       | R3S60GBSM          | 64 GB  | 2       | 17    | 0     | 0.05   |
| Fanxiang  | S101               | 2 TB   | 1       | 16    | 0     | 0.05   |
| KingFast  | SSD                | 16 GB  | 1       | 16    | 0     | 0.05   |
| LDNDISK   | SSD                | 240 GB | 1       | 16    | 0     | 0.05   |
| SanDisk   | Z400s M.2 2280     | 128 GB | 5       | 16    | 0     | 0.05   |
| SCY       | SNM4BBG12800D      | 128 GB | 2       | 16    | 0     | 0.05   |
| Intel     | SSDSCKKF512H6 SATA | 512 GB | 1       | 249   | 14    | 0.05   |
| TEXTORM   | B5                 | 480 GB | 2       | 16    | 0     | 0.05   |
| Goodram   | SSDPR-CL100-480-G3 | 480 GB | 5       | 20    | 11    | 0.04   |
| Intel     | SSDMCEAW080A4      | 80 GB  | 1       | 16    | 0     | 0.04   |
| XUM       | HX240GSSDSATA3     | 240 GB | 1       | 16    | 0     | 0.04   |
| OCZ       | VERTEX3            | 256 GB | 1       | 533   | 32    | 0.04   |
| Kingrich  | SSD                | 128 GB | 1       | 16    | 0     | 0.04   |
| Kingston  | SKC300S37A180G     | 180 GB | 3       | 320   | 745   | 0.04   |
| Biostar   | S100-256GB         | 256 GB | 1       | 16    | 0     | 0.04   |
| Golden... | GDSA25-120MS       | 120 GB | 1       | 16    | 0     | 0.04   |
| PNY       | SSD2SC240G0LC72... | 240 GB | 1       | 15    | 0     | 0.04   |
| WALRAM    | SSD 128G           | 128 GB | 6       | 15    | 0     | 0.04   |
| HP        | SSD S650           | 960 GB | 1       | 15    | 0     | 0.04   |
| FASTDISK  | FASTDISK120G       | 120 GB | 1       | 15    | 0     | 0.04   |
| Kingch... | SSD                | 360 GB | 2       | 15    | 0     | 0.04   |
| Micron    | MTFDDAK256MAY-1... | 256 GB | 8       | 303   | 59    | 0.04   |
| SanDisk   | SD9SN8W-256G-1006  | 256 GB | 10      | 182   | 882   | 0.04   |
| SK hynix  | HFS128G39MNC-2300A | 128 GB | 3       | 513   | 240   | 0.04   |
| SanDisk   | SD8SNAT128G1122    | 128 GB | 1       | 15    | 0     | 0.04   |
| SanDisk   | SSD i110           | 16 GB  | 5       | 15    | 0     | 0.04   |
| Lite-On   | IT L8T-256L9G-HP   | 256 GB | 3       | 15    | 0     | 0.04   |
| MOVESPEED | YSSDMDS-256GSQ-MG  | 256 GB | 1       | 15    | 0     | 0.04   |
| China     | MLC 256G           | 256 GB | 1       | 15    | 0     | 0.04   |
| Intel     | SSDSC2KB019T8R     | 1.9 TB | 1       | 15    | 0     | 0.04   |
| Plextor   | PH6-CE240          | 240 GB | 4       | 15    | 0     | 0.04   |
| China     | MS07               | 1 TB   | 1       | 15    | 0     | 0.04   |
| ADATA     | SP900NS34          | 128 GB | 2       | 230   | 508   | 0.04   |
| China     | IM256-WG30         | 256 GB | 1       | 15    | 0     | 0.04   |
| China     | Mit-SSD128A        | 128 GB | 1       | 15    | 0     | 0.04   |
| FORESEE   | 240GB SSD          | 240 GB | 1       | 15    | 0     | 0.04   |
| Transcend | TS64GSSD25S-M      | 64 GB  | 2       | 15    | 0     | 0.04   |
| Goldenfir | T650-256GB         | 256 GB | 1       | 91    | 5     | 0.04   |
| XrayDisk  | SSD                | 1 TB   | 2       | 15    | 0     | 0.04   |
| Netac     | SSD                | 128 GB | 33      | 16    | 1     | 0.04   |
| Lite-On   | CV1-SB128          | 128 GB | 1       | 15    | 0     | 0.04   |
| Leven     | JAJS500M120C-1     | 120 GB | 1       | 15    | 0     | 0.04   |
| V-GeN     | V-GEN10SM21AR256HY | 256 GB | 2       | 15    | 0     | 0.04   |
| Samsung   | MZNLN128HAHQ-000L2 | 128 GB | 3       | 14    | 0     | 0.04   |
| Intenso   | SSD                | 2 TB   | 1       | 14    | 0     | 0.04   |
| Kingston  | KingstonSA400S37   | 1 TB   | 1       | 14    | 0     | 0.04   |
| FASTDISK  | SSD 60G            | 64 GB  | 1       | 14    | 0     | 0.04   |
| PNY       | SSD2SC240G5LC70... | 240 GB | 1       | 14    | 0     | 0.04   |
| PNY       | 500GB SATA SSD     | 500 GB | 2       | 14    | 0     | 0.04   |
| Lenovo    | SSD SL700 M.2 128G | 128 GB | 1       | 14    | 0     | 0.04   |
| RevuAhn   | 900G Gaming        | 256 GB | 1       | 14    | 0     | 0.04   |
| Samsung   | MZ7LN1T0HAJQ-00000 | 1 TB   | 2       | 14    | 0     | 0.04   |
| Intenso   | SSD128GBCSU2-E7    | 128 GB | 1       | 14    | 0     | 0.04   |
| Seagate   | ST480FP0021        | 480 GB | 1       | 14    | 0     | 0.04   |
| Crucial   | CT2000MX500SSD1N   | 2 TB   | 1       | 14    | 0     | 0.04   |
| AMD       | R5SL256G           | 256 GB | 5       | 18    | 5     | 0.04   |
| Timetec   | MS05               | 256 GB | 2       | 14    | 0     | 0.04   |
| Micron    | 1300 SATA          | 512 GB | 1       | 14    | 0     | 0.04   |
| Microtech | SSD 60G            | 64 GB  | 1       | 14    | 0     | 0.04   |
| NFORCE    | 25625G2 TAS-SSQE3  | 256 GB | 1       | 14    | 0     | 0.04   |
| Lite-On   | CV3-8D512-41 SA... | 512 GB | 1       | 272   | 18    | 0.04   |
| Faspeed   | K7N-256G           | 256 GB | 1       | 14    | 0     | 0.04   |
| AMD       | R5SL960G           | 960 GB | 1       | 71    | 4     | 0.04   |
| Micron    | MTFDDAK240TCB      | 240 GB | 1       | 14    | 0     | 0.04   |
| Fujitsu   | F500S              | 1 TB   | 1       | 13    | 0     | 0.04   |
| Kingston  | RBUSNS8180DS3256GH | 256 GB | 1       | 41    | 2     | 0.04   |
| China     | SSD                | 2 TB   | 7       | 13    | 0     | 0.04   |
| SMI       | SSD DISK           | 128 GB | 1       | 13    | 0     | 0.04   |
| ADLINK    | SSO256GTLC9-SB3-4L | 256 GB | 1       | 13    | 0     | 0.04   |
| China     | SHMST6D128GHM11... | 128 GB | 1       | 13    | 0     | 0.04   |
| Ramaxel   | RTITF128PCA1MADL   | 128 GB | 2       | 13    | 0     | 0.04   |
| Smartbuy  | m.2 S11-2280       | 256 GB | 1       | 13    | 0     | 0.04   |
| Patriot   | Burst Elite 192... | 2 TB   | 1       | 13    | 0     | 0.04   |
| Digma     | 512GB RUN S9       | 512 GB | 2       | 13    | 0     | 0.04   |
| OCZ       | VECTOR180          | 960 GB | 1       | 13    | 0     | 0.04   |
| Verbatim  | Vi550 S3           | 1 TB   | 7       | 13    | 0     | 0.04   |
| China     | NGFF 2280 512GB... | 512 GB | 4       | 14    | 253   | 0.04   |
| Lite-On   | LJH-256V2G-11 M... | 256 GB | 1       | 13    | 0     | 0.04   |
| Patriot   | Burst Elite        | 480 GB | 5       | 13    | 1     | 0.04   |
| SanDisk   | SD8SNAT-128G-1006  | 128 GB | 11      | 13    | 0     | 0.04   |
| Kingston  | SHFR200240G        | 240 GB | 2       | 13    | 0     | 0.04   |
| Intel     | SSDSA1M160G2HP     | 160 GB | 8       | 110   | 20    | 0.04   |
| Plextor   | PX-128M6S+         | 128 GB | 1       | 13    | 0     | 0.04   |
| Origin... | TLC830 Pro Series  | 256 GB | 1       | 171   | 12    | 0.04   |
| WALRAM    | SSD                | 256 GB | 3       | 14    | 6     | 0.04   |
| China     | GSDSL128TY2AAQGCX  | 128 GB | 2       | 13    | 0     | 0.04   |
| Transcend | TS128GMTS600       | 128 GB | 1       | 13    | 0     | 0.04   |
| Transcend | TS64GMTS800        | 64 GB  | 2       | 13    | 0     | 0.04   |
| Lite-On   | CV1-8B128          | 128 GB | 18      | 13    | 0     | 0.04   |
| Lenovo    | SSD SL700          | 4 TB   | 1       | 12    | 0     | 0.04   |
| SanDisk   | SD6SB1M128G1022    | 128 GB | 1       | 219   | 16    | 0.04   |
| SomnAm... | SSD                | 120 GB | 1       | 25    | 1     | 0.04   |
| Getrich   | 120G SSD           | 120 GB | 1       | 12    | 0     | 0.04   |
| ShanDi... | SSD                | 128 GB | 2       | 12    | 0     | 0.04   |
| RECADATA  | RD-S350MCN-N0642   | 64 GB  | 1       | 12    | 0     | 0.03   |
| KUIJIA    | DK500-64G          | 64 GB  | 1       | 12    | 0     | 0.03   |
| Intel     | SSDSCKKW010X6      | 1 TB   | 3       | 27    | 194   | 0.03   |
| Lite-On   | LMH-128V2M         | 128 GB | 1       | 37    | 2     | 0.03   |
| EVM       | 512GB SSD          | 512 GB | 2       | 12    | 0     | 0.03   |
| Phison    | SSO256GTLC9-SBC-2  | 256 GB | 1       | 12    | 0     | 0.03   |
| Silico... | ULTIMATE CF CARD   | 16 GB  | 1       | 12    | 0     | 0.03   |
| Super ... | FTM28N325H         | 128 GB | 1       | 12    | 0     | 0.03   |
| Kingston  | OCP0S364B-A0       | 64 GB  | 1       | 12    | 0     | 0.03   |
| Lite-On   | CV3-SD128          | 128 GB | 1       | 12    | 0     | 0.03   |
| China     | SSDG2-256G         | 256 GB | 2       | 82    | 5     | 0.03   |
| AXIOMTEK  | FSA128GMC2T        | 128 GB | 26      | 12    | 0     | 0.03   |
| Kingston  | RBUSMS180S364GJ    | 64 GB  | 1       | 12    | 0     | 0.03   |
| Wicgtyp   | M900-128           | 128 GB | 1       | 12    | 0     | 0.03   |
| Kston     | SSD                | 256 GB | 1       | 12    | 0     | 0.03   |
| SanDisk   | SD6SF1M256G1022I   | 256 GB | 1       | 12    | 0     | 0.03   |
| V-GeN     | V-GEN01SM21AR25... | 256 GB | 1       | 12    | 0     | 0.03   |
| Leven     | JAJS500M120C       | 120 GB | 1       | 85    | 6     | 0.03   |
| OWC       | 1.0TB Mercury E... | 1 TB   | 2       | 12    | 0     | 0.03   |
| KingDian  | S280               | 32 GB  | 1       | 12    | 0     | 0.03   |
| INDMEM    | M.2 2280           | 64 GB  | 2       | 12    | 0     | 0.03   |
| Kingrich  | KM9 60GB MSATA3... | 64 GB  | 1       | 12    | 0     | 0.03   |
| SanDisk   | SD9SN8W512G1122    | 512 GB | 1       | 12    | 0     | 0.03   |
| China     | 512GB QLC SATA SSD | 512 GB | 2       | 12    | 0     | 0.03   |
| Advantech | SQF-SHMM2-8G-S9C   | 8 GB   | 2       | 11    | 0     | 0.03   |
| HP        | SSD S650           | 480 GB | 1       | 11    | 0     | 0.03   |
| XrayDisk  | SSD                | 480 GB | 2       | 11    | 0     | 0.03   |
| Samsung   | MZ7LN128HAHQ-00000 | 128 GB | 1       | 11    | 0     | 0.03   |
| PNY       | SSD2SC120G1SA75... | 120 GB | 1       | 11    | 0     | 0.03   |
| Intel     | SSDSCKKW240H6      | 240 GB | 7       | 36    | 398   | 0.03   |
| China     | SSD                | 500 GB | 5       | 11    | 0     | 0.03   |
| Kingston  | SA400S37480GB      | 480 GB | 1       | 11    | 0     | 0.03   |
| FORESEE   | S50AF512GB         | 512 GB | 6       | 11    | 0     | 0.03   |
| Netac     | SSD 120G           | 120 GB | 2       | 11    | 0     | 0.03   |
| Transcend | TSKU60SSD420       | 64 GB  | 1       | 11    | 0     | 0.03   |
| Crucial   | V4-CT128V4SSD2     | 128 GB | 1       | 11    | 0     | 0.03   |
| Intenso   | TBYTE-SSD          | 128 GB | 1       | 11    | 0     | 0.03   |
| Faspeed   | M3-360G            | 360 GB | 1       | 11    | 0     | 0.03   |
| SanDisk   | SD8SNAT-256G-1006  | 256 GB | 11      | 11    | 0     | 0.03   |
| Vaseky    | V900-128GB         | 120 GB | 1       | 11    | 0     | 0.03   |
| INDMEM    | SSD mSATA          | 512 GB | 1       | 11    | 0     | 0.03   |
| Micron    | M600_MTFDDAV512MBF | 512 GB | 1       | 11    | 0     | 0.03   |
| Transcend | TS128GMTS800I      | 128 GB | 1       | 11    | 0     | 0.03   |
| Foxline   | FLSSD480X5SE       | 480 GB | 2       | 11    | 0     | 0.03   |
| SanDisk   | Z400s 2.5 7MM      | 128 GB | 3       | 11    | 0     | 0.03   |
| China     | 1TBE               | 1 TB   | 1       | 11    | 0     | 0.03   |
| ADATA     | SSD S511           | 240 GB | 1       | 10    | 0     | 0.03   |
| Maximus   | SSD                | 128 GB | 4       | 10    | 0     | 0.03   |
| Transcend | TS32GSSD25S-M      | 32 GB  | 1       | 10    | 0     | 0.03   |
| 2-Power   | SSD2042B           | 256 GB | 2       | 10    | 3     | 0.03   |
| DGM       | SSD 120GB S3-120A  | 120 GB | 2       | 79    | 21    | 0.03   |
| SanDisk   | SD8SNAT128G1002    | 128 GB | 11      | 10    | 0     | 0.03   |
| China     | EK V100 120G       | 120 GB | 1       | 10    | 0     | 0.03   |
| SanDisk   | SD8SNAT256G1122    | 256 GB | 3       | 10    | 0     | 0.03   |
| Lumino... | SSD                | 64 GB  | 1       | 10    | 0     | 0.03   |
| ADATA     | SX300              | 128 GB | 1       | 10    | 0     | 0.03   |
| Teclast   | 256GB A850         | 256 GB | 1       | 10    | 0     | 0.03   |
| Kingston  | OCP0S3256B-AB      | 256 GB | 1       | 10    | 0     | 0.03   |
| Kingston  | SQ500S37480G       | 480 GB | 2       | 10    | 0     | 0.03   |
| SanDisk   | SD8SNAT256G1002    | 256 GB | 8       | 11    | 1     | 0.03   |
| KingSpec  | ACSC2M256S25       | 256 GB | 1       | 10    | 0     | 0.03   |
| UNIC2     | S5170-256-80       | 256 GB | 1       | 10    | 0     | 0.03   |
| Intenso   | SSD_2.5''_TLC_5... | 512 GB | 1       | 10    | 0     | 0.03   |
| ACOS      | AS-512             | 512 GB | 2       | 48    | 508   | 0.03   |
| KUU       | SSD                | 256 GB | 1       | 10    | 0     | 0.03   |
| Zheino    | CHN25SATAS1 032    | 32 GB  | 4       | 10    | 0     | 0.03   |
| SanDisk   | SD8SBAT-032G-1006  | 32 GB  | 5       | 10    | 1     | 0.03   |
| OCZ       | REVODRIVE          | 25 GB  | 2       | 1968  | 208   | 0.03   |
| Integral  | V Series SATA S... | 1 TB   | 1       | 9     | 0     | 0.03   |
| KingSpec  | MT-1TB             | 1 TB   | 3       | 13    | 32    | 0.03   |
| ZTC       | SM201-128G         | 128 GB | 1       | 9     | 0     | 0.03   |
| WALRAM    | SSD 120G           | 120 GB | 4       | 17    | 18    | 0.03   |
| China     | KZ128              | 128 GB | 1       | 9     | 0     | 0.03   |
| Seagate   | BarraCuda Q1 SS... | 960 GB | 2       | 9     | 0     | 0.03   |
| Crucial   | CT480M500SSD3      | 480 GB | 3       | 1180  | 993   | 0.03   |
| Hikvision | HS-SSD-Minder(S... | 240 GB | 1       | 9     | 0     | 0.03   |
| SPCC      | SSD162             | 240 GB | 1       | 203   | 20    | 0.03   |
| Zozt      | G3000 240          | 240 GB | 2       | 9     | 0     | 0.03   |
| SanDisk   | SD8SBAT128G1122    | 128 GB | 31      | 9     | 0     | 0.03   |
| Advantech | SATA CVB-CD128     | 128 GB | 1       | 9     | 0     | 0.03   |
| Ramsta    | SSD R800           | 120 GB | 1       | 9     | 0     | 0.03   |
| Yeyian    | VALK 1000          | 120 GB | 2       | 9     | 0     | 0.03   |
| Zozt      | G3000 480          | 480 GB | 1       | 9     | 0     | 0.03   |
| China     | MSATA SSD          | 256 GB | 2       | 9     | 0     | 0.03   |
| Faspeed   | H5-120G PLUS       | 120 GB | 1       | 9     | 0     | 0.03   |
| Transcend | TS512GSSD720       | 512 GB | 1       | 1668  | 176   | 0.03   |
| EMTEC     | X250               | 256 GB | 1       | 9     | 0     | 0.03   |
| Mushkin   | MKNSSDRW1TB        | 1 TB   | 1       | 9     | 0     | 0.03   |
| S3+       | S3SSDA512-ECS-1    | 512 GB | 1       | 9     | 0     | 0.03   |
| Microtech | SSD480M2S80        | 480 GB | 1       | 9     | 0     | 0.03   |
| Apple     | SSD TS0128F        | 121 GB | 3       | 160   | 128   | 0.03   |
| Kingston  | SA400S37-120G      | 120 GB | 3       | 9     | 0     | 0.03   |
| MidasF... | SSD                | 256 GB | 2       | 9     | 0     | 0.03   |
| ADATA     | SU900              | 128 GB | 1       | 9     | 0     | 0.02   |
| Kingston  | v300 240G          | 240 GB | 1       | 9     | 0     | 0.02   |
| SanDisk   | iSSD P4            | 16 GB  | 2       | 222   | 24    | 0.02   |
| Teclast   | 128GB MS550        | 128 GB | 1       | 8     | 0     | 0.02   |
| S3+       | S3SSDC240XEU       | 240 GB | 1       | 415   | 46    | 0.02   |
| China     | SSD                | 180 GB | 3       | 36    | 4     | 0.02   |
| VERICO    | SSD                | 120 GB | 2       | 8     | 0     | 0.02   |
| Intenso   | SSD                | 250 GB | 2       | 8     | 0     | 0.02   |
| Phison    | 128GB SSD          | 128 GB | 1       | 8     | 0     | 0.02   |
| Intenso   | MMY HC256GS6HA7T   | 256 GB | 2       | 8     | 0     | 0.02   |
| KingDian  | N400 60G           | 64 GB  | 1       | 8     | 0     | 0.02   |
| Biostar   | S160-256GB         | 256 GB | 1       | 8     | 0     | 0.02   |
| Intenso   | JAJM600M256C       | 256 GB | 1       | 8     | 0     | 0.02   |
| KingSpec  | ACSC4M128MSA       | 128 GB | 1       | 8     | 0     | 0.02   |
| SanDisk   | SD8SN8U1T002000    | 1 TB   | 1       | 8     | 0     | 0.02   |
| China     | FPT310M8SSD256G    | 256 GB | 1       | 8     | 0     | 0.02   |
| FORESEE   | S326M256G          | 256 GB | 1       | 8     | 0     | 0.02   |
| PNY       | SSD2SC240G1CS17... | 240 GB | 1       | 8     | 0     | 0.02   |
| Intel     | SSDSCKKW120H6      | 120 GB | 1       | 76    | 8     | 0.02   |
| China     | ESA3ASA2PSTBT120GB | 120 GB | 1       | 243   | 28    | 0.02   |
| Lite-On   | LSS-24L6G          | 24 GB  | 4       | 9     | 254   | 0.02   |
| Kingspeed | SSD                | 240 GB | 1       | 8     | 0     | 0.02   |
| Kingston  | A400 960G          | 960 GB | 1       | 8     | 0     | 0.02   |
| BaseTech  | A400 m.2 256Gb     | 256 GB | 1       | 8     | 0     | 0.02   |
| Teclast   | 480GB A800         | 480 GB | 1       | 174   | 20    | 0.02   |
| Super ... | FTM51N325H         | 512 GB | 2       | 8     | 0     | 0.02   |
| China     | SSD60G             | 64 GB  | 2       | 8     | 0     | 0.02   |
| SK hynix  | SH920 mSATA        | 128 GB | 6       | 312   | 169   | 0.02   |
| MIXZA     | SSD                | 120 GB | 2       | 8     | 0     | 0.02   |
| ADATA     | SX300              | 64 GB  | 3       | 60    | 344   | 0.02   |
| Netac     | SATA3 120GB SSD    | 120 GB | 1       | 8     | 0     | 0.02   |
| ANACOMDA  | TT 256GB SSD       | 256 GB | 1       | 8     | 0     | 0.02   |
| ATP       | I-Temp. SATA II... | 240 GB | 1       | 8     | 0     | 0.02   |
| Apacer    | 64GAS510           | 64 GB  | 1       | 8     | 0     | 0.02   |
| Innodisk  | M.2 (S80) 3TE7     | 960 GB | 1       | 8     | 0     | 0.02   |
| Kingston  | SV300S37A 60G      | 64 GB  | 1       | 8     | 0     | 0.02   |
| Crucial   | CT2320SX           | 320 GB | 1       | 7     | 0     | 0.02   |
| SPCC      | M.2 SSD            | 128 GB | 2       | 21    | 1     | 0.02   |
| Team      | T2531TB            | 1 TB   | 3       | 7     | 0     | 0.02   |
| PNY       | 120GB SATA SSD     | 120 GB | 2       | 7     | 0     | 0.02   |
| SanDisk   | SD8SMAT-128G-1006  | 128 GB | 2       | 7     | 0     | 0.02   |
| FASTDISK  | SSD 120G           | 120 GB | 1       | 7     | 0     | 0.02   |
| Mach X... | MXSSD3MDSFG-120G   | 120 GB | 1       | 7     | 0     | 0.02   |
| ADATA     | IM2S3138E-256GM-B  | 256 GB | 1       | 513   | 65    | 0.02   |
| ALLIED    | SSD                | 128 GB | 1       | 7     | 0     | 0.02   |
| BIWIN     | C6370_128GB        | 128 GB | 2       | 7     | 0     | 0.02   |
| China     | M.2 SSD            | 128 GB | 3       | 46    | 3     | 0.02   |
| Phison    | M.2 128GB SSO12... | 128 GB | 1       | 7     | 0     | 0.02   |
| SanDisk   | SD8SBAT256G1002    | 256 GB | 1       | 7     | 0     | 0.02   |
| ShiJi     | SSD                | 1 TB   | 2       | 7     | 0     | 0.02   |
| China     | SSD 256G           | 256 GB | 3       | 7     | 0     | 0.02   |
| KingSpec  | ACSC2M128mSA       | 128 GB | 1       | 7     | 0     | 0.02   |
| Transcend | TS64GMTS400        | 64 GB  | 1       | 7     | 0     | 0.02   |
| AGI       | AGI480G18AI238     | 480 GB | 1       | 7     | 0     | 0.02   |
| SanDisk   | SD9SN8W128G1122    | 128 GB | 1       | 7     | 0     | 0.02   |
| FASTDISK  | SSD 30G            | 32 GB  | 1       | 7     | 0     | 0.02   |
| SPCC      | M.2 SSD            | 512 GB | 4       | 7     | 0     | 0.02   |
| Digma     | RUN Y2             | 128 GB | 1       | 7     | 0     | 0.02   |
| Dell      | WR202KD032G E70... | 32 GB  | 2       | 6     | 0     | 0.02   |
| Goodram   | SSDPR-S400U-120-42 | 120 GB | 3       | 6     | 0     | 0.02   |
| XrayDisk  | 256GB SSD          | 256 GB | 3       | 6     | 0     | 0.02   |
| tigo      | SSD                | 128 GB | 1       | 6     | 0     | 0.02   |
| POLION    | SSD                | 256 GB | 1       | 6     | 0     | 0.02   |
| Kingston  | SV300S37A 120G     | 120 GB | 1       | 6     | 0     | 0.02   |
| ORICO     | M200               | 256 GB | 1       | 6     | 0     | 0.02   |
| Phison    | SSBP064GTB3C0-S11  | 64 GB  | 1       | 6     | 0     | 0.02   |
| Samsung   | MZ7LH1T9HMLT-00005 | 1.9 TB | 1       | 6     | 0     | 0.02   |
| Solid     | SSD0256S00         | 256 GB | 2       | 13    | 2     | 0.02   |
| Kingston  | RBUSC180S37128GJ   | 128 GB | 1       | 6     | 0     | 0.02   |
| Patriot   | Ignite             | 240 GB | 1       | 6     | 0     | 0.02   |
| Kingston  | SA400S37 240G      | 240 GB | 1       | 6     | 0     | 0.02   |
| Samsung   | SSD PM871b 2.5 7mm | 128 GB | 1       | 6     | 0     | 0.02   |
| Seapiy    | E535N M.2 2280     | 256 GB | 1       | 6     | 0     | 0.02   |
| SanDisk   | WD Blue SA510 2.5  | 250 GB | 1       | 6     | 0     | 0.02   |
| Teclast   | BD256GB SHCA-2280  | 256 GB | 2       | 6     | 0     | 0.02   |
| Lite-On   | CV5-8Q512-HP       | 512 GB | 1       | 6     | 0     | 0.02   |
| China     | BF9SSD 256S        | 256 GB | 1       | 6     | 0     | 0.02   |
| Kross ... | KE-SSDIS96G        | 960 GB | 1       | 6     | 0     | 0.02   |
| Intel     | SSDSC2KF512G8 SATA | 512 GB | 1       | 6     | 0     | 0.02   |
| Patriot   | Burst Elite        | 240 GB | 10      | 10    | 1     | 0.02   |
| KingSpec  | P3-64              | 64 GB  | 3       | 7     | 28    | 0.02   |
| GS Nan... | GSPMA512M16STF     | 512 GB | 1       | 6     | 0     | 0.02   |
| QUMO      | Q3DT-120GSCY       | 120 GB | 1       | 6     | 0     | 0.02   |
| geonix    | SSD                | 240 GB | 1       | 6     | 0     | 0.02   |
| ADATA     | SU650NS38          | 120 GB | 5       | 6     | 0     | 0.02   |
| QNIX      | SSD                | 120 GB | 1       | 6     | 0     | 0.02   |
| S3+       | S3SSDC120          | 120 GB | 1       | 6     | 0     | 0.02   |
| GeIL      | Zenith A3-PRO      | 240 GB | 1       | 6     | 0     | 0.02   |
| Intenso   | M.2 2242-128GB SSD | 128 GB | 1       | 6     | 0     | 0.02   |
| QUMO      | Q3DT-240GSCY       | 240 GB | 3       | 9     | 9     | 0.02   |
| GeIL      | Zenith A3          | 120 GB | 1       | 6     | 0     | 0.02   |
| Intel     | SSDSCKGW180A4      | 180 GB | 1       | 286   | 47    | 0.02   |
| Faspeed   | K7N8-256GH         | 256 GB | 1       | 5     | 0     | 0.02   |
| J.ZAO     | 3 SERIES 2.5 IN... | 240 GB | 1       | 5     | 0     | 0.02   |
| Plextor   | PX-128M6MV         | 128 GB | 2       | 5     | 0     | 0.02   |
| S3+       | S3SSDC240          | 240 GB | 2       | 5     | 0     | 0.02   |
| Teclast   | BD256GB SLCB-2280  | 256 GB | 2       | 5     | 0     | 0.02   |
| ShiJi     | SSD                | 256 GB | 2       | 5     | 0     | 0.02   |
| TEXTORM   | B5                 | 120 GB | 2       | 8     | 17    | 0.02   |
| INDMEM    | SSD mSATA          | 128 GB | 1       | 5     | 0     | 0.02   |
| kingch... | SSD                | 120 GB | 1       | 5     | 0     | 0.02   |
| BRAVEE... | SSD                | 120 GB | 1       | 5     | 0     | 0.02   |
| Kingch... | SSD                | 120 GB | 1       | 5     | 0     | 0.02   |
| T-FORCE   | SSD                | 2 TB   | 1       | 5     | 0     | 0.02   |
| Micron    | 5100_MTFDDAV960TCB | 960 GB | 1       | 188   | 32    | 0.02   |
| BUFFALO   | SSD                | 256 GB | 1       | 5     | 0     | 0.02   |
| V-GeN     | V-GEN10SM19AR12... | 120 GB | 1       | 5     | 0     | 0.02   |
| QIANGHE   | SSD                | 240 GB | 1       | 73    | 12    | 0.02   |
| Pear      | SSD                | 2 TB   | 1       | 5     | 0     | 0.02   |
| BR        | SSD                | 64 GB  | 1       | 5     | 0     | 0.02   |
| Intenso   | SSD0128S00         | 128 GB | 1       | 5     | 0     | 0.02   |
| UMAX      | 2242               | 512 GB | 3       | 5     | 0     | 0.02   |
| KingSpec  | T-60               | 64 GB  | 4       | 12    | 88    | 0.02   |
| Hikvision | HS-SSD-G100N 256G  | 256 GB | 1       | 5     | 0     | 0.02   |
| SSSTC     | CV8-8E128-11 SATA  | 128 GB | 1       | 5     | 0     | 0.02   |
| ShiJi     | SSD                | 128 GB | 1       | 5     | 0     | 0.02   |
| Intel     | SSDSA1M080G2LE     | 80 GB  | 3       | 63    | 14    | 0.02   |
| Samsung   | MZ7LN256HAJQ-00007 | 256 GB | 1       | 5     | 0     | 0.02   |
| China     | CYX-SSD-S1000      | 512 GB | 3       | 5     | 0     | 0.02   |
| Fanxiang  | S201               | 512 GB | 1       | 5     | 0     | 0.01   |
| Kingston  | SA400S37-256G      | 256 GB | 1       | 535   | 98    | 0.01   |
| Kingston  | KC600              | 128 GB | 1       | 5     | 0     | 0.01   |
| Digma     | 1TB RUN S9         | 1 TB   | 1       | 5     | 0     | 0.01   |
| Micron    | MTFDDAV240TDU      | 240 GB | 2       | 5     | 0     | 0.01   |
| ADATA     | SX850              | 256 GB | 2       | 171   | 40    | 0.01   |
| Micron    | 5300_MTFDDAK7T6TDS | 7.6 TB | 1       | 5     | 0     | 0.01   |
| TrekStor  | TREKSTORSSD512GB   | 500 GB | 1       | 5     | 0     | 0.01   |
| PNY       | 1TB SATA SSD       | 1 TB   | 4       | 5     | 0     | 0.01   |
| Advantech | SQF-S25M8-128G-SAE | 128 GB | 1       | 5     | 0     | 0.01   |
| Faspeed   | H5-500G            | 500 GB | 1       | 40    | 7     | 0.01   |
| OCZ       | AGITLITY3          | 480 GB | 1       | 5234  | 1028  | 0.01   |
| Hikvision | HS-SSD-J100N       | 256 GB | 2       | 5     | 0     | 0.01   |
| China     | M.2 2280-1TB SSD   | 1 TB   | 1       | 5     | 0     | 0.01   |
| MaxDig... | MD500 120G         | 120 GB | 1       | 5     | 0     | 0.01   |
| Teclast   | 512GB A850         | 512 GB | 1       | 5     | 0     | 0.01   |
| Zheino    | CHN25SATAS1 064    | 64 GB  | 2       | 4     | 0     | 0.01   |
| Mushkin   | MKNSSDCG480GB      | 480 GB | 2       | 116   | 508   | 0.01   |
| China     | NS128GSSD340       | 128 GB | 1       | 4     | 0     | 0.01   |
| Kingch... | SSD                | 256 GB | 1       | 4     | 0     | 0.01   |
| Leven     | JS500120C          | 120 GB | 1       | 4     | 0     | 0.01   |
| SUNEAST   | SSD SE800 mSATA    | 512 GB | 1       | 4     | 0     | 0.01   |
| Protectli | 64GB mSATA         | 64 GB  | 2       | 4     | 0     | 0.01   |
| ORTIAL    | SSD                | 1 TB   | 1       | 4     | 0     | 0.01   |
| BHT       | WR202HH032G E70... | 32 GB  | 1       | 4     | 0     | 0.01   |
| Intenso   | 512GB QLC SATA SSD | 512 GB | 2       | 4     | 0     | 0.01   |
| TAMMUZ    | SSD                | 120 GB | 1       | 4     | 0     | 0.01   |
| GLOWAY    | VAL32GS3-mSATA     | 32 GB  | 1       | 4     | 0     | 0.01   |
| KingSpec  | ACSC2M128S25       | 128 GB | 1       | 4     | 0     | 0.01   |
| PNY       | CS900 SSD          | 120 GB | 1       | 4     | 0     | 0.01   |
| China     | X160EB             | 500 GB | 2       | 4     | 0     | 0.01   |
| SPCC      | 2.5" SSD           | 512 GB | 2       | 78    | 24    | 0.01   |
| Corsair   | Neutron XT SSD     | 240 GB | 2       | 1342  | 286   | 0.01   |
| Teclast   | BD256GB SHCB-2280  | 256 GB | 8       | 4     | 0     | 0.01   |
| Goodram   | 1TB PCS 2.5" SSD   | 1 TB   | 1       | 4     | 0     | 0.01   |
| Star D... | SATA SSD           | 480 GB | 1       | 4     | 0     | 0.01   |
| Lite-On   | LCT-128M3S         | 128 GB | 3       | 100   | 687   | 0.01   |
| Intel     | SSDSCKKF180H6L     | 180 GB | 1       | 79    | 17    | 0.01   |
| Team      | TM4PS5128G         | 128 GB | 1       | 8     | 1     | 0.01   |
| Veno      | SSD                | 256 GB | 2       | 4     | 0     | 0.01   |
| Inland    | SATA SSD           | 256 GB | 1       | 4     | 0     | 0.01   |
| S3+       | S3SSDC128          | 128 GB | 1       | 4     | 0     | 0.01   |
| AGI       | AGI500GIMAI238     | 500 GB | 1       | 4     | 0     | 0.01   |
| Maximus   | SSD 256G           | 256 GB | 1       | 4     | 0     | 0.01   |
| Reletech  | P400-sata2.5 512G  | 512 GB | 1       | 4     | 0     | 0.01   |
| ASint     | AS606              | 64 GB  | 1       | 4     | 0     | 0.01   |
| Intenso   | AEROFARA M.2       | 256 GB | 1       | 4     | 0     | 0.01   |
| MicroD... | 512G SSD           | 512 GB | 2       | 4     | 0     | 0.01   |
| 2-Power   | SSD2041A           | 120 GB | 1       | 4     | 0     | 0.01   |
| KODAK     | SSD X100           | 120 GB | 1       | 4     | 0     | 0.01   |
| Samsung   | SSD PM800 mSATA    | 64 GB  | 1       | 4     | 0     | 0.01   |
| SanDisk   | SD7UB3Q256G1001    | 256 GB | 5       | 419   | 100   | 0.01   |
| Lite-On   | IT SCS-256L9S      | 256 GB | 1       | 24    | 5     | 0.01   |
| Crucial   | CT256M550SSD4      | 256 GB | 1       | 342   | 82    | 0.01   |
| Mushkin   | MKNSSDTR240GB-LT   | 240 GB | 1       | 4     | 0     | 0.01   |
| PHINOCOM  | SSD                | 120 GB | 1       | 4     | 0     | 0.01   |
| INNOVA... | SSD                | 1 TB   | 2       | 4     | 0     | 0.01   |
| Teclast   | 256GB SSD          | 256 GB | 2       | 4     | 5     | 0.01   |
| Intel     | SSDMAEMC080G2H     | 80 GB  | 1       | 4     | 0     | 0.01   |
| Samsung   | PM881 SATA         | 256 GB | 2       | 4     | 0     | 0.01   |
| Corsair   | Neutron GTX SSD    | 128 GB | 1       | 1173  | 291   | 0.01   |
| Hikvision | M.2 C100           | 128 GB | 1       | 244   | 60    | 0.01   |
| BIWIN     | G2242              | 64 GB  | 2       | 4     | 0     | 0.01   |
| Kingston  | OCP0S3128Q-A0      | 128 GB | 1       | 4     | 0     | 0.01   |
| GeIL      | ZENITH-A3 120G     | 120 GB | 1       | 3     | 0     | 0.01   |
| Mushkin   | MKNSSDTR512GB-3DL  | 512 GB | 1       | 3     | 0     | 0.01   |
| Patriot   | Morebeck-N100      | 256 GB | 2       | 3     | 0     | 0.01   |
| Zheino    | CHN-25SATAA3-360   | 360 GB | 1       | 87    | 21    | 0.01   |
| Intel     | SSDSC2KF010T8      | 1 TB   | 1       | 3     | 0     | 0.01   |
| ROKOT     | SSD 512 Gb         | 512 GB | 1       | 3     | 0     | 0.01   |
| Transcend | TS64GHSD370KI      | 64 GB  | 1       | 3     | 0     | 0.01   |
| ZHITAI    | SC001 Active 25... | 256 GB | 2       | 3     | 0     | 0.01   |
| BR        | SSD                | 128 GB | 1       | 3     | 0     | 0.01   |
| Faspeed   | M3-90G             | 90 GB  | 1       | 3     | 0     | 0.01   |
| Digma     | 256GB RUN S9       | 256 GB | 2       | 4     | 4     | 0.01   |
| Lite-On   | LSS-16L6G          | 16 GB  | 1       | 3     | 0     | 0.01   |
| Patriot   | NORCO GDSA25-64MS  | 64 GB  | 1       | 3     | 0     | 0.01   |
| Micron    | MTFDDAK960TDS-1... | 960 GB | 6       | 3     | 0     | 0.01   |
| Hikvision | HS-SSD-E100N 128G  | 128 GB | 1       | 3     | 0     | 0.01   |
| SanDisk   | SATAIII            | 16 GB  | 1       | 3     | 0     | 0.01   |
| tigo      | SSD                | 64 GB  | 1       | 3     | 0     | 0.01   |
| WDC       | WDS100T1R0B-68A4Z0 | 1 TB   | 2       | 3     | 0     | 0.01   |
| ADATA     | SU650              | 256 GB | 2       | 3     | 0     | 0.01   |
| China     | TR960GB            | 960 GB | 1       | 268   | 71    | 0.01   |
| Intenso   | LS 256GB M300      | 256 GB | 1       | 3     | 0     | 0.01   |
| KingDian  | S200               | 240 GB | 1       | 3     | 0     | 0.01   |
| ADATA     | IM2S3334-256GD     | 256 GB | 1       | 7     | 1     | 0.01   |
| Lite-On   | LGH-512V2G-11 M... | 512 GB | 1       | 11    | 2     | 0.01   |
| Lite-On   | LSS-16L6G-HP       | 16 GB  | 2       | 66    | 638   | 0.01   |
| HPE       | MK000960GWJPP      | 960 GB | 1       | 3     | 0     | 0.01   |
| Intenso   | SSD Sata III       | 2 TB   | 1       | 3     | 0     | 0.01   |
| China     | FPT310M4SSD256G    | 256 GB | 1       | 3     | 0     | 0.01   |
| Pacifi... | PSM-128GBSATA3S... | 128 GB | 1       | 3     | 0     | 0.01   |
| OWC       | Aura SSD           | 120 GB | 1       | 3     | 0     | 0.01   |
| Rogueware | 2.5'' SATA NX100S  | 512 GB | 1       | 3     | 0     | 0.01   |
| Transcend | TS240GJDM520       | 240 GB | 1       | 3     | 0     | 0.01   |
| SK hynix  | SC210 2.5 7MM      | 256 GB | 3       | 429   | 577   | 0.01   |
| SanDisk   | SD7SB2Q512G1001    | 512 GB | 3       | 356   | 100   | 0.01   |
| Acer      | SSD SA100          | 480 GB | 2       | 3     | 0     | 0.01   |
| Lite-On   | IT L8H-64V2G       | 64 GB  | 1       | 3     | 0     | 0.01   |
| Team      | T253240GB          | 240 GB | 1       | 3     | 0     | 0.01   |
| Aarvex    | 256GB SSD          | 256 GB | 1       | 3     | 0     | 0.01   |
| Foxline   | FLSSD256X5         | 256 GB | 5       | 3     | 0     | 0.01   |
| QUMO      | Q3DT-256GMSY-M2    | 256 GB | 2       | 3     | 0     | 0.01   |
| Team      | T253256GB          | 256 GB | 2       | 3     | 0     | 0.01   |
| OCZ       | REVODRIVE X2       | 64 GB  | 4       | 1204  | 516   | 0.01   |
| SPCC      | SSDB27             | 32 GB  | 1       | 23    | 6     | 0.01   |
| ShineDisk | M667 128G          | 120 GB | 1       | 3     | 0     | 0.01   |
| Timetec   | 35TTM8SSATA-512G   | 512 GB | 1       | 3     | 0     | 0.01   |
| i-Flas... | K8                 | 64 GB  | 1       | 3     | 0     | 0.01   |
| IOD       | MST1001-512        | 512 GB | 2       | 3     | 0     | 0.01   |
| China     | SSD-512G           | 512 GB | 1       | 3     | 0     | 0.01   |
| TurXun    | S500               | 256 GB | 1       | 3     | 0     | 0.01   |
| China     | DEPOSM3DT-480      | 480 GB | 1       | 3     | 0     | 0.01   |
| Corsair   | CSSD-V128GB2       | 128 GB | 1       | 3     | 0     | 0.01   |
| Indilinx  | IND-S3N80S-128G    | 128 GB | 1       | 3     | 0     | 0.01   |
| Netac     | M.2 2280-128GB SSD | 128 GB | 1       | 3     | 0     | 0.01   |
| QUMO      | Q3DT-480GSCY       | 480 GB | 1       | 3     | 0     | 0.01   |
| Wibtek    | W800S              | 512 GB | 8       | 3     | 14    | 0.01   |
| Smart     | SSD                | 240 GB | 1       | 3     | 0     | 0.01   |
| GOKE      | GG2ZT256S3C27      | 256 GB | 1       | 3     | 0     | 0.01   |
| Pichau    | Gaming PG256X      | 256 GB | 1       | 3     | 0     | 0.01   |
| Lite-On   | LMS-32L6M-HP       | 32 GB  | 2       | 3     | 0     | 0.01   |
| China     | SSV4               | 240 GB | 1       | 3     | 0     | 0.01   |
| S3+       | S3SSDC480          | 480 GB | 1       | 2     | 0     | 0.01   |
| OCZ       | AGILITY3           | 480 GB | 1       | 842   | 286   | 0.01   |
| Samsung   | SSD PM810 mSATA    | 128 GB | 1       | 137   | 46    | 0.01   |
| Goodram   | IR_SSDPR_S25A_120  | 120 GB | 1       | 2     | 0     | 0.01   |
| China     | BiCS               | 120 GB | 1       | 31    | 10    | 0.01   |
| Faspeed   | K5M-16G            | 16 GB  | 1       | 2     | 0     | 0.01   |
| SanDisk   | SD8SBAT064G1122    | 64 GB  | 1       | 2     | 0     | 0.01   |
| Colorful  | SL500              | 320 GB | 1       | 525   | 186   | 0.01   |
| Crucial   | CT250MX200SSD6     | 250 GB | 1       | 2     | 0     | 0.01   |
| SK hynix  | HFS480G3H2X069N    | 480 GB | 2       | 2     | 0     | 0.01   |
| Vaseky    | V820-512G          | 512 GB | 1       | 2     | 0     | 0.01   |
| Samsung   | MZ7LH3T8HMLT-00005 | 3.8 TB | 3       | 2     | 0     | 0.01   |
| SK hynix  | SH920 2.5 7MM      | 512 GB | 7       | 458   | 262   | 0.01   |
| Intel     | SSDSA2M160G2HP     | 160 GB | 2       | 251   | 65    | 0.01   |
| Fordisk   | SATA SSD           | 120 GB | 1       | 2     | 0     | 0.01   |
| LDLC      | SSD                | 64 GB  | 1       | 2     | 0     | 0.01   |
| Lite-On   | IT LST-16S9G       | 16 GB  | 1       | 2     | 0     | 0.01   |
| Transcend | TS64GMSA452T2      | 64 GB  | 1       | 2     | 0     | 0.01   |
| Patriot   | Wildfire           | 120 GB | 1       | 2712  | 1022  | 0.01   |
| Crucial   | CT500BX500SSD1     | 500 GB | 5       | 2     | 0     | 0.01   |
| ADATA     | SSD SP900          | 256 GB | 1       | 2673  | 1016  | 0.01   |
| Foxline   | FLSSD128X5         | 128 GB | 3       | 2     | 0     | 0.01   |
| Hikvision | HS-SSD-C260 512G   | 512 GB | 1       | 2     | 0     | 0.01   |
| KODAK     | X150               | 480 GB | 1       | 2     | 0     | 0.01   |
| SK hynix  | HFS128G3AMNB-2200A | 128 GB | 6       | 490   | 587   | 0.01   |
| Timetec   | 30TT253X2-256GB    | 256 GB | 1       | 2     | 0     | 0.01   |
| Intel     | SSDSC2KB480G7      | 480 GB | 3       | 2     | 0     | 0.01   |
| KOOTION   | X12 SSD            | 480 GB | 1       | 2     | 0     | 0.01   |
| Neo Forza | NFS011SA324-600... | 240 GB | 1       | 2     | 0     | 0.01   |
| Cactus    | CactusFlashCard    | 64 GB  | 2       | 2     | 0     | 0.01   |
| Golden... | 60Gb               | 64 GB  | 1       | 2     | 0     | 0.01   |
| KODAK     | SSD X100           | 120 GB | 1       | 2     | 0     | 0.01   |
| Gigastone | SS6200-256GB       | 256 GB | 1       | 2     | 0     | 0.01   |
| PNY       | 240GB SATA SSD     | 240 GB | 2       | 2     | 0     | 0.01   |
| China     | N900-128           | 128 GB | 1       | 2     | 0     | 0.01   |
| KingDian  | N400               | 120 GB | 1       | 2     | 0     | 0.01   |
| Team      | T253480GB          | 480 GB | 1       | 2     | 0     | 0.01   |
| SOLIDATA  | SSD                | 120 GB | 1       | 2420  | 1019  | 0.01   |
| China     | N86-256GB          | 256 GB | 1       | 2     | 0     | 0.01   |
| Foxline   | FLSSD120SM5        | 120 GB | 1       | 2     | 0     | 0.01   |
| Micron    | 1300_MTFDDAK512TDL | 512 GB | 1       | 2     | 0     | 0.01   |
| SanDisk   | SD8SNAT-128G-1009  | 128 GB | 1       | 2     | 0     | 0.01   |
| KingSpec  | KSM-SMP.5-032MJ    | 32 GB  | 1       | 2     | 0     | 0.01   |
| SanDisk   | SSD i110           | 24 GB  | 1       | 2     | 0     | 0.01   |
| JD        | SSD                | 240 GB | 1       | 242   | 105   | 0.01   |
| Valuetech | Basics             | 256 GB | 1       | 2     | 0     | 0.01   |
| Intel     | SSDSCKKF180H6H     | 180 GB | 5       | 58    | 242   | 0.01   |
| OCZ       | VERTEX3 LP         | 240 GB | 1       | 2268  | 1019  | 0.01   |
| Toshiba   | THNSNK256GCS8 SATA | 256 GB | 6       | 223   | 100   | 0.01   |
| Fanxiang  | I200               | 128 GB | 1       | 2     | 0     | 0.01   |
| Netac     | N600               | 512 GB | 1       | 2     | 0     | 0.01   |
| Timetec   | 30TT253X2-1TB      | 1 TB   | 1       | 2     | 0     | 0.01   |
| ACPI      | M2SCF-6M           | 64 GB  | 1       | 2     | 0     | 0.01   |
| BIOSTAR   | S120-256GB         | 256 GB | 1       | 2     | 0     | 0.01   |
| Netac     | SSD                | 160 GB | 1       | 2     | 0     | 0.01   |
| VSEVEN    | V7 SSD             | 512 GB | 1       | 2     | 0     | 0.01   |
| SK hynix  | SH920 2.5 7MM      | 128 GB | 1       | 54    | 25    | 0.01   |
| Intel     | SSDSC2BA400G3R     | 400 GB | 1       | 2162  | 1028  | 0.01   |
| China     | MSATA SSD          | 128 GB | 1       | 2     | 0     | 0.01   |
| China     | SSD                | 250 GB | 1       | 2     | 0     | 0.01   |
| PNY       | SSD2SC120GB1DA1... | 120 GB | 1       | 2248  | 1081  | 0.01   |
| Mushkin   | MKNSSDCL120GB      | 120 GB | 1       | 2067  | 1007  | 0.01   |
| SanDisk   | SSD P4             | 64 GB  | 3       | 47    | 300   | 0.01   |
| Team      | T253A3001T         | 1 TB   | 2       | 2     | 0     | 0.01   |
| Lite-On   | CV1-8B512          | 512 GB | 2       | 2     | 0     | 0.01   |
| Intel     | SSDSC2BB300G4R     | 304 GB | 2       | 2029  | 1029  | 0.01   |
| Netac     | SSD                | 320 GB | 1       | 96    | 48    | 0.01   |
| Netac     | W800S 256GB SSD    | 256 GB | 1       | 1     | 0     | 0.01   |
| Kingston  | RBU-SNS8350DES3... | 128 GB | 14      | 170   | 94    | 0.01   |
| SanDisk   | SD7SB3Q128G1001    | 128 GB | 4       | 195   | 100   | 0.01   |
| Toshiba   | THNSNK256GVN8 M... | 256 GB | 11      | 203   | 102   | 0.01   |
| Azerty    | M500               | 512 GB | 1       | 1     | 0     | 0.01   |
| SanDisk   | SD8SBAT128G        | 128 GB | 1       | 1     | 0     | 0.01   |
| SanDisk   | WD Blue SA510 2.5  | 1 TB   | 3       | 1     | 0     | 0.01   |
| Kingston  | SKC300S37A240G     | 240 GB | 2       | 1     | 0     | 0.01   |
| Toshiba   | THNSNK512GCS8 SATA | 512 GB | 1       | 190   | 100   | 0.01   |
| Kingston  | SHPM2280P2H-240G   | 240 GB | 7       | 469   | 553   | 0.01   |
| TMI       | 256GB SATA CRMP... | 240 GB | 1       | 1     | 0     | 0.01   |
| 2-Power   | SSD2042A           | 240 GB | 1       | 1     | 0     | 0.01   |
| Fujitsu   | F500S 128G         | 128 GB | 1       | 1     | 0     | 0.01   |
| Hikvision | HS-SSD-C160 256G   | 256 GB | 1       | 1     | 0     | 0.01   |
| KingSpec  | P3D-240            | 240 GB | 1       | 1     | 0     | 0.01   |
| Philips   | SSD                | 120 GB | 1       | 1     | 0     | 0.01   |
| DEPO      | SM3DT-120          | 120 GB | 2       | 1     | 108   | 0.00   |
| ASENNO    | AS25               | 120 GB | 2       | 1     | 0     | 0.00   |
| Acer      | SSD SA100          | 240 GB | 1       | 1     | 0     | 0.00   |
| FASTDISK  | SSD                | 64 GB  | 1       | 1     | 0     | 0.00   |
| Foxline   | FLSSD120X5SE       | 120 GB | 1       | 1     | 0     | 0.00   |
| Netac     | GN256 2280         | 256 GB | 1       | 1     | 0     | 0.00   |
| WALRAM    | SSD                | 1 TB   | 1       | 1     | 0     | 0.00   |
| Yunhai... | Y6-240G            | 240 GB | 1       | 1     | 0     | 0.00   |
| PNY       | SSD9SC240GCDA      | 240 GB | 1       | 1804  | 1015  | 0.00   |
| China     | S41CF256G          | 256 GB | 1       | 1     | 0     | 0.00   |
| INDMEM    | M.2 2280           | 128 GB | 1       | 1     | 0     | 0.00   |
| KLLISRE   | SSD                | 512 GB | 1       | 1     | 0     | 0.00   |
| SXMicro   | NF830              | 256 GB | 1       | 1     | 0     | 0.00   |
| Lite-On   | LJH-128V2G-11 M... | 128 GB | 1       | 41    | 24    | 0.00   |
| ADATA     | SU650 1.9TB        | 1.9 TB | 1       | 1     | 0     | 0.00   |
| KingSpec  | ACJC2M064S25       | 64 GB  | 1       | 1     | 0     | 0.00   |
| Lite-On   | L8T-64L6G          | 64 GB  | 1       | 1     | 0     | 0.00   |
| Mcpoint   | MC240              | 240 GB | 1       | 6     | 3     | 0.00   |
| Micron    | 5300_MTFDDAK240TDS | 240 GB | 2       | 1     | 0     | 0.00   |
| Netac     | SSD                | 360 GB | 1       | 1     | 0     | 0.00   |
| TCSUNBOW  | X1                 | 16 GB  | 1       | 1     | 0     | 0.00   |
| Intel     | SSDSC2BA400G3T     | 400 GB | 1       | 1671  | 1029  | 0.00   |
| Neo Forza | NFS121SA312-600... | 120 GB | 4       | 57    | 515   | 0.00   |
| China     | SSDS2TA120G-BULK   | 120 GB | 1       | 1     | 0     | 0.00   |
| KLEVV     | NEO N610 SSD       | 512 GB | 2       | 1     | 0     | 0.00   |
| MaxDig... | MD-2.5-512G-NC     | 512 GB | 1       | 1     | 0     | 0.00   |
| Team      | L3 EVO SSD         | 240 GB | 1       | 1     | 0     | 0.00   |
| China     | FPT310M8SSD128G    | 128 GB | 4       | 1     | 0     | 0.00   |
| Toshiba   | THNSNK128GVN8 M... | 128 GB | 4       | 157   | 100   | 0.00   |
| ACPI      | MSS4FV-MP mSATA... | 128 GB | 1       | 1     | 0     | 0.00   |
| China     | SATA3 60GB SSD     | 64 GB  | 1       | 1     | 0     | 0.00   |
| Mushkin   | MKNSSDS2512GB      | 512 GB | 1       | 1     | 0     | 0.00   |
| ORICO     | M200               | 1 TB   | 1       | 1     | 0     | 0.00   |
| MidasF... | SSD                | 120 GB | 2       | 1     | 0     | 0.00   |
| AGI       | AGI1T0G17AI178     | 1 TB   | 1       | 53    | 34    | 0.00   |
| Intel     | SSDSC2BW120A3F     | 120 GB | 1       | 1540  | 1020  | 0.00   |
| Transcend | TS1TSSD370         | 1 TB   | 1       | 1     | 0     | 0.00   |
| China     | 2.5 SSD            | 240 GB | 1       | 1     | 0     | 0.00   |
| China     | G521N256GB         | 256 GB | 1       | 1     | 0     | 0.00   |
| Innodisk  | DES25-64GM41BW1... | 64 GB  | 1       | 7     | 4     | 0.00   |
| ADATA     | AXM14S3-128GM-B    | 128 GB | 1       | 1449  | 1017  | 0.00   |
| SK hynix  | HFS064G3AMNB-2200A | 64 GB  | 2       | 406   | 585   | 0.00   |
| Intel     | SSDSC2KW480H6      | 480 GB | 3       | 28    | 56    | 0.00   |
| Foxline   | FLSSD240X5SE       | 240 GB | 2       | 1     | 0     | 0.00   |
| Teclast   | 128GB A850         | 128 GB | 1       | 1     | 0     | 0.00   |
| Xinhaike  | SSD                | 120 GB | 2       | 1     | 0     | 0.00   |
| BHT       | WR202I0032G E70... | 32 GB  | 1       | 1     | 0     | 0.00   |
| BIWIN     | C6308              | 64 GB  | 1       | 1     | 0     | 0.00   |
| Plextor   | PX-512M6M          | 512 GB | 1       | 1     | 0     | 0.00   |
| VICKTER   | SSD                | 128 GB | 3       | 1     | 0     | 0.00   |
| Patriot   | Pyro m3            | 240 GB | 1       | 1378  | 1015  | 0.00   |
| Transcend | TS128XBTMT3D58G    | 128 GB | 1       | 138   | 101   | 0.00   |
| INNOVA... | SSD_2.5"_1TB_In... | 1 TB   | 2       | 1     | 0     | 0.00   |
| Micron    | 1300_MTFDDAV256TDL | 256 GB | 1       | 1     | 0     | 0.00   |
| SK hynix  | HFS960G3H2X069N    | 960 GB | 2       | 1     | 0     | 0.00   |
| Apple     | SSD SM256C         | 256 GB | 5       | 332   | 576   | 0.00   |
| SK hynix  | HFS032G34MNC-2200A | 32 GB  | 1       | 441   | 337   | 0.00   |
| BR        | SSD 60G            | 64 GB  | 1       | 1     | 0     | 0.00   |
| Indilinx  | IND-S3N80S-256G    | 256 GB | 2       | 1     | 0     | 0.00   |
| Kingston  | SA400S37-480G      | 480 GB | 1       | 1     | 0     | 0.00   |
| SOYO      | SSD WA120G         | 120 GB | 1       | 1     | 0     | 0.00   |
| China     | SSD 512G           | 512 GB | 1       | 1     | 0     | 0.00   |
| Lite-On   | LMT-19nmBGA-128... | 128 GB | 1       | 1     | 0     | 0.00   |
| Patriot   | Solid              | 240 GB | 2       | 1     | 0     | 0.00   |
| Micron    | P300-MTFDBAC050SAL | 50 GB  | 1       | 1411  | 1140  | 0.00   |
| Intel     | SSDSC2KW240H6      | 240 GB | 9       | 8     | 318   | 0.00   |
| AMD       | R5SL512G           | 512 GB | 1       | 1     | 0     | 0.00   |
| Team      | M8PS5 SSD          | 128 GB | 1       | 1     | 0     | 0.00   |
| SATAFIRM  | S11                | 240 GB | 3       | 126   | 88    | 0.00   |
| WDC       | WD A3              | 128 GB | 2       | 1     | 0     | 0.00   |
| Intel     | SSDSC2BX200G4R     | 200 GB | 3       | 1172  | 1027  | 0.00   |
| KingSpec  | ACJC2M128S25       | 128 GB | 1       | 1     | 0     | 0.00   |
| Ramsta    | SSD S800           | 128 GB | 1       | 1     | 0     | 0.00   |
| China     | W800SH 512GB SSD   | 512 GB | 1       | 1     | 0     | 0.00   |
| Lite-On   | CV1-DB256          | 256 GB | 1       | 1     | 0     | 0.00   |
| RAMOS     | 2.5 inch SATA 2... | 256 GB | 1       | 1     | 0     | 0.00   |
| ShiJi     | SSD                | 2 TB   | 1       | 1     | 0     | 0.00   |
| Supers... | SUPERSONIC256      | 256 GB | 1       | 1     | 0     | 0.00   |
| Intel     | SSDSC2BX400G4R     | 400 GB | 3       | 1103  | 1027  | 0.00   |
| Indilinx  | IND-S325S120G      | 120 GB | 1       | 18    | 16    | 0.00   |
| Lite-On   | LAT-256M3S         | 256 GB | 3       | 1435  | 1682  | 0.00   |
| FORESEE   | 32GB SSD           | 32 GB  | 1       | 1     | 0     | 0.00   |
| FORESEE   | G500F256GB         | 256 GB | 2       | 1     | 0     | 0.00   |
| Intel     | N18A               | 240 GB | 2       | 1     | 0     | 0.00   |
| iODD      | MST1000-256        | 256 GB | 1       | 1     | 0     | 0.00   |
| Intel     | SSDSC2BA200G4R     | 200 GB | 2       | 1037  | 1028  | 0.00   |
| Intel     | SSDSC2KG960G7R     | 960 GB | 2       | 1035  | 1028  | 0.00   |
| LEQIXIANG | SSD                | 256 GB | 3       | 1     | 2     | 0.00   |
| China     | G521N              | 256 GB | 1       | 1     | 0     | 0.00   |
| Teclast   | 240GB A800         | 240 GB | 1       | 1     | 0     | 0.00   |
| SK hynix  | HFS250G32TND-3110A | 250 GB | 1       | 335   | 340   | 0.00   |
| Foxline   | FLSSD60X3          | 64 GB  | 1       | 993   | 1016  | 0.00   |
| Intel     | SSDSCKKF240H6L     | 240 GB | 3       | 52    | 376   | 0.00   |
| Toshiba   | KSG60ZSE512G SATA  | 512 GB | 2       | 97    | 100   | 0.00   |
| SPCC      | SSD                | 32 GB  | 1       | 998   | 1036  | 0.00   |
| China     | G535NW-512G        | 512 GB | 2       | 0     | 0     | 0.00   |
| SanDisk   | SD9TN8W-256G-1006  | 256 GB | 1       | 907   | 984   | 0.00   |
| China     | KCG SSD            | 256 GB | 1       | 0     | 0     | 0.00   |
| Kingch... | SSD                | 480 GB | 1       | 0     | 0     | 0.00   |
| Netac     | NS512GSSD340       | 512 GB | 1       | 0     | 0     | 0.00   |
| Emphase   | G5RM3G064-M        | 64 GB  | 1       | 907   | 1017  | 0.00   |
| ADATA     | ISSS332-256GT      | 256 GB | 1       | 0     | 0     | 0.00   |
| ADATA     | SU630 1.9TB        | 1.9 TB | 1       | 0     | 0     | 0.00   |
| GLOWAY    | VAL128GS3-M.2-80   | 128 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | SD8SMAT-032G-1006  | 32 GB  | 1       | 0     | 0     | 0.00   |
| Innodisk  | mSATA 3MG2-P       | 992 GB | 2       | 0     | 0     | 0.00   |
| ADATA     | SX900              | 112 GB | 1       | 872   | 1016  | 0.00   |
| Intel     | SSDSC2BA800G4R     | 800 GB | 1       | 877   | 1027  | 0.00   |
| Corsair   | CSSD-F40GB2        | 40 GB  | 2       | 500   | 588   | 0.00   |
| China     | FPT310M4SSD128G    | 128 GB | 2       | 0     | 0     | 0.00   |
| KLEVV     | NEO N400 SSD       | 120 GB | 1       | 0     | 0     | 0.00   |
| Leqixiang | SSD                | 1 TB   | 1       | 0     | 0     | 0.00   |
| Lite-On   | CV1-8B128-HP       | 128 GB | 1       | 0     | 0     | 0.00   |
| Maxmemory | X100               | 240 GB | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSC2KW180H6      | 180 GB | 3       | 5     | 74    | 0.00   |
| SPCC      | SSD162             | 55 GB  | 1       | 855   | 1036  | 0.00   |
| SK hynix  | HFS060G32MNM-1010U | 64 GB  | 1       | 822   | 1016  | 0.00   |
| Eluktro   | TRO-SSD7-500GB-PRO | 500 GB | 1       | 806   | 1016  | 0.00   |
| Patriot   | JAJM600M128C       | 128 GB | 1       | 0     | 0     | 0.00   |
| Phison    | S11-256G-PHISON... | 256 GB | 1       | 0     | 0     | 0.00   |
| Teclast   | 128GB NS550-2242   | 128 GB | 1       | 0     | 0     | 0.00   |
| LDLC      | SSD                | 256 GB | 1       | 6     | 7     | 0.00   |
| SandForce | FM-25S2S-60GBP2    | 64 GB  | 1       | 317   | 416   | 0.00   |
| SemsoTai  | S200 2280          | 256 GB | 1       | 8     | 10    | 0.00   |
| ADATA     | IMSS316-256GD      | 256 GB | 2       | 0     | 0     | 0.00   |
| Blackpcs  | SSDPro             | 240 GB | 1       | 0     | 0     | 0.00   |
| China     | M900-1T            | 1 TB   | 1       | 0     | 0     | 0.00   |
| China     | REVOLUTIONS500_256 | 256 GB | 1       | 0     | 0     | 0.00   |
| Innodisk  | mSATA 3TG6-P       | 240 GB | 2       | 0     | 0     | 0.00   |
| TAMMUZ    | SSD                | 240 GB | 1       | 0     | 0     | 0.00   |
| Lite-On   | E200-160           | 160 GB | 1       | 12    | 18    | 0.00   |
| KeepData  | GIM512             | 512 GB | 1       | 0     | 0     | 0.00   |
| Mushkin   | MKNSSDRW240GB      | 240 GB | 1       | 0     | 0     | 0.00   |
| iODD      | MST1001-512        | 512 GB | 2       | 0     | 0     | 0.00   |
| Lite-On   | E200-080           | 80 GB  | 1       | 706   | 1065  | 0.00   |
| Corsair   | Accelerator SSD    | 64 GB  | 1       | 654   | 1017  | 0.00   |
| Intel     | SSDSCMMW120A3L     | 120 GB | 1       | 649   | 1017  | 0.00   |
| BAITITON  | BT58SSD08M         | 128 GB | 1       | 23    | 36    | 0.00   |
| Samsung   | MZNLH128HBHQ-000H1 | 128 GB | 10      | 63    | 100   | 0.00   |
| Advantech | SQF-S25M4-32G-S9C  | 32 GB  | 1       | 0     | 0     | 0.00   |
| INDMEM    | M.2 2280           | 256 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | A400-120G          | 128 GB | 1       | 0     | 0     | 0.00   |
| Reeioon   | FR120GB R2S3       | 120 GB | 1       | 232   | 377   | 0.00   |
| Qumo      | SSD                | 480 GB | 1       | 625   | 1015  | 0.00   |
| HP Phison | PSSBN016GA27MC0    | 16 GB  | 2       | 628   | 1032  | 0.00   |
| Indilinx  | InM2246S3-128G     | 128 GB | 2       | 0     | 0     | 0.00   |
| Netac     | S535N8-128GYN      | 128 GB | 2       | 0     | 0     | 0.00   |
| Samsung   | SSD PM810 TM       | 128 GB | 2       | 688   | 1107  | 0.00   |
| Gritronix | M.2 2280           | 256 GB | 1       | 22    | 37    | 0.00   |
| China     | K1                 | 256 GB | 1       | 0     | 0     | 0.00   |
| China     | YS SSD             | 128 GB | 1       | 11    | 19    | 0.00   |
| Micron    | 5300_MTFDDAV480TDS | 480 GB | 2       | 0     | 0     | 0.00   |
| Transcend | TS256ASTMM1600X    | 256 GB | 1       | 0     | 0     | 0.00   |
| ExeGate   | EX276690RUS(960GB) | 960 GB | 3       | 0     | 0     | 0.00   |
| Samsung   | MZNLH256HAJD-000H1 | 256 GB | 2       | 57    | 100   | 0.00   |
| OCZ       | INTREPID 3700      | 240 GB | 1       | 578   | 1020  | 0.00   |
| Intenso   | SSD Sata III       | 247 GB | 1       | 18    | 32    | 0.00   |
| SK hynix  | HFS256G3AMNB-2200A | 256 GB | 9       | 322   | 887   | 0.00   |
| Netac     | MST1002-1T         | 1 TB   | 1       | 0     | 0     | 0.00   |
| Netac     | S535M3-128GYN      | 128 GB | 1       | 0     | 0     | 0.00   |
| Wibtek    | W800S              | 512 GB | 1       | 0     | 0     | 0.00   |
| RX7       | 2.5                | 240 GB | 1       | 6     | 12    | 0.00   |
| Intel     | SSDMCEAW080A4 m... | 80 GB  | 2       | 515   | 1008  | 0.00   |
| China     | FPT310M8SSD512G    | 512 GB | 1       | 0     | 0     | 0.00   |
| Intenso   | SATA3 128GB SSD    | 128 GB | 1       | 0     | 0     | 0.00   |
| PNY       | CS900 M.2 250GB... | 250 GB | 1       | 0     | 0     | 0.00   |
| POWER X   | SS1000-256GB       | 256 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | SD8TN8U256G2000    | 256 GB | 1       | 0     | 0     | 0.00   |
| Toshiba   | THNSNK128GCS8 SATA | 128 GB | 3       | 281   | 438   | 0.00   |
| Intel     | SSDSCKKF256G8H     | 256 GB | 10      | 61    | 188   | 0.00   |
| Biostar   | S120-256GB         | 256 GB | 1       | 0     | 0     | 0.00   |
| China     | SH00R128GB         | 128 GB | 1       | 0     | 0     | 0.00   |
| China     | SSD-HYX-1HAH8N-... | 256 GB | 1       | 0     | 0     | 0.00   |
| Liren     | LIREN128G          | 128 GB | 1       | 0     | 0     | 0.00   |
| Netac     | S539N8-256GSN      | 256 GB | 1       | 0     | 0     | 0.00   |
| OSCOO     | OSC SSD            | 128 GB | 1       | 0     | 0     | 0.00   |
| Seapiy    | E535N M.2 2280     | 128 GB | 1       | 0     | 0     | 0.00   |
| Team      | T253X6512G         | 512 GB | 1       | 0     | 0     | 0.00   |
| VNYEZ     | SSD M.2 2242       | 256 GB | 1       | 0     | 0     | 0.00   |
| Vaseky    | V820-256G          | 256 GB | 1       | 0     | 0     | 0.00   |
| iODD      | MST1000 - 256      | 256 GB | 1       | 0     | 0     | 0.00   |
| ADATA     | XM12               | 32 GB  | 1       | 465   | 1015  | 0.00   |
| Intel     | SSDSCKKF256H6H     | 256 GB | 2       | 34    | 245   | 0.00   |
| VISIPRO   | SSD                | 256 GB | 1       | 6     | 14    | 0.00   |
| ADATA     | XM11 128GB-V2      | 128 GB | 1       | 449   | 1048  | 0.00   |
| China     | FPT310MSSSD128G    | 128 GB | 1       | 0     | 0     | 0.00   |
| Gost      | SSD120             | 120 GB | 1       | 0     | 0     | 0.00   |
| Hyundai   | 240GB SSD          | 240 GB | 1       | 0     | 0     | 0.00   |
| Intenso   | SSDAS256           | 256 GB | 2       | 0     | 0     | 0.00   |
| Lite-On   | LMT-19nmBGA-64G-DS | 64 GB  | 1       | 0     | 0     | 0.00   |
| SMI       | B17A               | 240 GB | 1       | 0     | 0     | 0.00   |
| T-CREATE  | T253TA001T         | 1 TB   | 1       | 0     | 0     | 0.00   |
| Vaseky    | V900-1TB           | 1 TB   | 1       | 0     | 0     | 0.00   |
| PNY       | 69D03094-T         | 40 GB  | 1       | 403   | 1016  | 0.00   |
| China     | T120               | 120 GB | 2       | 0     | 0     | 0.00   |
| SanDisk   | SD9SB8W-256G-1006  | 256 GB | 1       | 390   | 989   | 0.00   |
| tecmiyo   | SATA SSD           | 128 GB | 1       | 15    | 39    | 0.00   |
| China     | T60                | 64 GB  | 2       | 0     | 0     | 0.00   |
| China     | MS201-512G         | 512 GB | 1       | 0     | 0     | 0.00   |
| Intenso   | JAJMS600M128G      | 128 GB | 1       | 0     | 0     | 0.00   |
| Leven     | JAJS600M128G-BI... | 128 GB | 1       | 0     | 0     | 0.00   |
| Reeinno   | ST960GB S7S3       | 960 GB | 1       | 0     | 0     | 0.00   |
| X-ENERGY  | X-ENERGY120GB      | 120 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | SH103S3240G-NV     | 240 GB | 1       | 377   | 1018  | 0.00   |
| PNY       | SSD2SC120GE2DA0... | 120 GB | 1       | 373   | 1018  | 0.00   |
| Kingston  | SVP200S37A256G     | 256 GB | 2       | 370   | 1016  | 0.00   |
| HP Phison | PSSBN032GA27MC1    | 32 GB  | 1       | 373   | 1032  | 0.00   |
| Bliksem   | SSD                | 256 GB | 1       | 10    | 28    | 0.00   |
| WDC       | PC SA530 SDATN8... | 256 GB | 1       | 344   | 971   | 0.00   |
| SPCC      | SSD170             | 64 GB  | 1       | 358   | 1016  | 0.00   |
| GLOWAY    | VAL120GS3-S7       | 120 GB | 1       | 135   | 389   | 0.00   |
| Mushkin   | MKNSSDCL120GB-DX   | 120 GB | 1       | 348   | 1006  | 0.00   |
| Mushkin   | MKNSSDCL480GB-DX   | 480 GB | 1       | 347   | 1020  | 0.00   |
| Transcend | TS8GHSD630         | 8 GB   | 1       | 682   | 2044  | 0.00   |
| Dahua     | C800A SSD          | 240 GB | 1       | 0     | 0     | 0.00   |
| Micron    | MTFDDAK512TDL-1... | 512 GB | 1       | 0     | 0     | 0.00   |
| SandForce | TX21B10400GB1IB... | 400 GB | 1       | 0     | 0     | 0.00   |
| ShiJi     | SSD                | 512 GB | 1       | 0     | 0     | 0.00   |
| UMAX      | 2280 64G           | 64 GB  | 1       | 0     | 0     | 0.00   |
| ADATA     | SP900NS38          | 256 GB | 3       | 327   | 1019  | 0.00   |
| Samsung   | MMCRE28G8MXP-0VBH1 | 128 GB | 1       | 311   | 1006  | 0.00   |
| BAITITON  | BT58SSD10M         | 256 GB | 1       | 0     | 0     | 0.00   |
| China     | ESA3ASA2ISN1BQ4... | 480 GB | 1       | 0     | 0     | 0.00   |
| China     | M.2 SSD            | 1 TB   | 1       | 0     | 0     | 0.00   |
| FASTDISK  | SSD 32G            | 32 GB  | 1       | 0     | 0     | 0.00   |
| GLOWAY    | STK120GS3-S7       | 120 GB | 1       | 0     | 0     | 0.00   |
| Intenso   | VERICO SSD         | 240 GB | 1       | 0     | 0     | 0.00   |
| Mushkin   | MKNSSDS2256GB-LT   | 256 GB | 1       | 0     | 0     | 0.00   |
| Patriot   | Torch LE           | 120 GB | 1       | 0     | 0     | 0.00   |
| SUNTRSI   | SSD S660ST         | 240 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZ7KM1T9HAJM-00005 | 1.9 TB | 1       | 0     | 0     | 0.00   |
| China     | NS128GSSD330       | 128 GB | 1       | 5     | 18    | 0.00   |
| ADATA     | SX900              | 512 GB | 1       | 259   | 1018  | 0.00   |
| AXIOMTEK  | FSA016G300MC4T-H   | 16 GB  | 1       | 0     | 0     | 0.00   |
| Advantech | SQF-S25V1-128GDSDM | 128 GB | 1       | 0     | 0     | 0.00   |
| BAITITON  | BT58SSD10S         | 256 GB | 1       | 0     | 0     | 0.00   |
| China     | NGFF 2242 128GB... | 128 GB | 1       | 0     | 0     | 0.00   |
| China     | SW-120GB           | 120 GB | 1       | 0     | 0     | 0.00   |
| DERLAR    | SSD                | 128 GB | 1       | 0     | 0     | 0.00   |
| Dahua     | C800 2.5 inch S... | 120 GB | 1       | 0     | 0     | 0.00   |
| GLOWAY    | VAL64GM3-mSATA     | 64 GB  | 1       | 0     | 0     | 0.00   |
| Golden... | SSD                | 32 GB  | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSC2KB960G7      | 960 GB | 4       | 0     | 0     | 0.00   |
| MAX SPEED | SSD                | 256 GB | 1       | 0     | 0     | 0.00   |
| Micron    | MTFDDAK2T0TDL      | 2 TB   | 1       | 0     | 0     | 0.00   |
| Toshiba   | THNSF81Q92CSE      | 1.9 TB | 1       | 0     | 0     | 0.00   |
| Transcend | TS128GSSD420K      | 128 GB | 1       | 0     | 0     | 0.00   |
| Tronos    | TN240G-SSD         | 240 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | CF Card            | 16 GB  | 3       | 0     | 0     | 0.00   |
| Kingston  | SNS4151S316GD      | 16 GB  | 7       | 253   | 1023  | 0.00   |
| SanDisk   | WD Blue SA510 2.5  | 1 TB   | 2       | 2     | 5     | 0.00   |
| Bamba     | SSD                | 240 GB | 1       | 60    | 249   | 0.00   |
| GeIL      | ZENITH S3-120GB    | 120 GB | 1       | 245   | 1021  | 0.00   |
| Myung     | G3 Series          | 120 GB | 1       | 228   | 1015  | 0.00   |
| ExeGate   | EX280463RUS(512GB) | 512 GB | 1       | 0     | 0     | 0.00   |
| Goldenfir | T650-120G          | 128 GB | 1       | 0     | 0     | 0.00   |
| Hitachi   | HDSSD240GJP3       | 240 GB | 1       | 0     | 0     | 0.00   |
| Lite-On   | S960 256           | 256 GB | 1       | 0     | 0     | 0.00   |
| MaiChai   | SSD 512G           | 512 GB | 1       | 0     | 0     | 0.00   |
| QUMO      | SSD                | 256 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | WD Green 2.5       | 480 GB | 1       | 0     | 2     | 0.00   |
| SanDisk   | WD Green M.2 2280  | 240 GB | 2       | 2     | 11    | 0.00   |
| SK hynix  | HFS256G38MNB-2200A | 256 GB | 1       | 207   | 1007  | 0.00   |
| Drevo     | X1 pro 480G        | 480 GB | 1       | 559   | 2830  | 0.00   |
| China     | MKSCE1BD060M4      | 64 GB  | 4       | 199   | 1016  | 0.00   |
| SanDisk   | WD Blue SA510 2.5  | 500 GB | 6       | 0     | 10    | 0.00   |
| ADATA     | SU740              | 500 GB | 1       | 417   | 2141  | 0.00   |
| Lite-On   | CS1-SP32-11 M.2... | 32 GB  | 2       | 0     | 2     | 0.00   |
| China     | ESA3SMD2HTGT240GB  | 240 GB | 1       | 51    | 273   | 0.00   |
| Wellco... | 128GB SSD          | 128 GB | 1       | 13    | 71    | 0.00   |
| Lite-On   | LMT-256M6M-HP      | 256 GB | 2       | 79    | 649   | 0.00   |
| Patriot   | Pyro SE            | 240 GB | 1       | 180   | 1016  | 0.00   |
| SanDisk   | SD9TB8W-256G-1006  | 256 GB | 1       | 171   | 984   | 0.00   |
| BIOSTAR   | S100-480GB         | 480 GB | 1       | 0     | 0     | 0.00   |
| China     | LS 512GB M300      | 512 GB | 1       | 0     | 0     | 0.00   |
| China     | S3 SSD             | 256 GB | 1       | 0     | 0     | 0.00   |
| Faspeed   | H5-30G             | 32 GB  | 1       | 0     | 0     | 0.00   |
| Fujitsu   | F500s 240G         | 240 GB | 1       | 0     | 0     | 0.00   |
| Teutons   | Platinum SSD       | 256 GB | 1       | 0     | 0     | 0.00   |
| Xinsujie  | XSJ-X100-128GB     | 128 GB | 1       | 0     | 0     | 0.00   |
| China     | 240G SATA III SSD  | 240 GB | 1       | 154   | 1016  | 0.00   |
| Goldenfir | T650-120GB         | 120 GB | 1       | 4     | 28    | 0.00   |
| SK hynix  | SH910 mSATA        | 128 GB | 1       | 151   | 1026  | 0.00   |
| Kingston  | SNS4151S316G       | 16 GB  | 5       | 151   | 1025  | 0.00   |
| PNY       | SSD2SC240G3LC70... | 240 GB | 1       | 141   | 1017  | 0.00   |
| Lite-On   | CV8-CE256-HP       | 256 GB | 1       | 135   | 1007  | 0.00   |
| China     | s60 60gb           | 55 GB  | 1       | 135   | 1016  | 0.00   |
| Intenso   | TOP M.2 SATA       | 256 GB | 1       | 125   | 961   | 0.00   |
| China     | JDa He SATA DISK   | 64 GB  | 1       | 135   | 1045  | 0.00   |
| China     | NT-1TB 2280        | 1 TB   | 1       | 0     | 0     | 0.00   |
| China     | SH00M256GB         | 256 GB | 1       | 0     | 0     | 0.00   |
| ExeGate   | EX276536RUS(120GB) | 120 GB | 1       | 0     | 0     | 0.00   |
| Netac     | GM256              | 256 GB | 1       | 0     | 0     | 0.00   |
| ZHITAI    | SC001 Active 51... | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | HFS500G32TND-3110A | 500 GB | 1       | 142   | 1209  | 0.00   |
| Kingston  | SNS4151S332G       | 32 GB  | 3       | 118   | 1022  | 0.00   |
| SanDisk   | WD Blue SA510 M... | 1 TB   | 1       | 2     | 18    | 0.00   |
| SK hynix  | HFS128G3AMNM-1010A | 128 GB | 1       | 109   | 1027  | 0.00   |
| OSCOO     | OSC SSD            | 120 GB | 1       | 9     | 89    | 0.00   |
| SanDisk   | SD9SB8W-128G-1006  | 128 GB | 1       | 83    | 992   | 0.00   |
| AXIOMTEK  | FSA128GMC5T        | 128 GB | 1       | 0     | 0     | 0.00   |
| China     | GCM2IN2280256C     | 256 GB | 1       | 0     | 0     | 0.00   |
| China     | SATA SSD           | 24 GB  | 1       | 0     | 0     | 0.00   |
| Dahua     | C800A SSD          | 120 GB | 1       | 0     | 0     | 0.00   |
| Faspeed   | K7N-128GH          | 128 GB | 1       | 0     | 0     | 0.00   |
| KINGPAN   | SSD                | 256 GB | 1       | 0     | 0     | 0.00   |
| Plextor   | PX-32G5L           | 32 GB  | 1       | 0     | 0     | 0.00   |
| SanDisk   | WD Green M.2 2280  | 480 GB | 1       | 0     | 0     | 0.00   |
| Smartbuy  | 120GB STELS        | 128 GB | 1       | 0     | 0     | 0.00   |
| TMI       | 512GB M2 CRMP.4... | 512 GB | 1       | 0     | 0     | 0.00   |
| Team      | T253E2512G         | 512 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TS16GMTS400        | 16 GB  | 1       | 0     | 0     | 0.00   |
| Transcend | TS64GMSA370I       | 64 GB  | 1       | 0     | 0     | 0.00   |
| Wintec    | S6 30G M.2 SSD     | 32 GB  | 1       | 0     | 0     | 0.00   |
| PNY       | SSD2SC240GC2DH1... | 240 GB | 1       | 85    | 1023  | 0.00   |
| ADATA     | AXM21S3-24GM-B     | 24 GB  | 1       | 83    | 1020  | 0.00   |
| Micron    | MTFDDAT064MAM-1J2  | 64 GB  | 2       | 120   | 1538  | 0.00   |
| HP Phison | PSSBN032GA27MC0    | 32 GB  | 1       | 81    | 1039  | 0.00   |
| ADATA     | XM11 128GB-V3      | 128 GB | 1       | 77    | 1016  | 0.00   |
| Transcend | TS64GSSD340K       | 64 GB  | 1       | 74    | 1008  | 0.00   |
| Mushkin   | MKNSSDCR120GB-DX7  | 120 GB | 1       | 73    | 1016  | 0.00   |
| Kingston  | SUV500M8960G       | 960 GB | 1       | 96    | 1444  | 0.00   |
| SandForce | 906190             | 64 GB  | 1       | 65    | 1018  | 0.00   |
| ADATA     | SP900NS38          | 512 GB | 1       | 64    | 1020  | 0.00   |
| MaxDig... | MD300 128G         | 128 GB | 1       | 41    | 666   | 0.00   |
| Kingston  | SMS151S324G        | 24 GB  | 2       | 61    | 1022  | 0.00   |
| Kingston  | A400               | 120 GB | 1       | 0     | 9     | 0.00   |
| Lite-On   | CV8-8E128-HP       | 128 GB | 31      | 54    | 1007  | 0.00   |
| Kingston  | SHPM2280P2-480G    | 480 GB | 1       | 54    | 1009  | 0.00   |
| WDC       | PC SA530 SDASN8... | 256 GB | 4       | 51    | 992   | 0.00   |
| Intenso   | SSD Sata III       | 506 GB | 1       | 64    | 1289  | 0.00   |
| Innodisk  | 2.5" SATA SSD 3... | 3.8 TB | 3       | 50    | 1010  | 0.00   |
| Kingston  | SSDNOW 240         | 240 GB | 1       | 45    | 1018  | 0.00   |
| Lite-On   | LMT-128M3M         | 128 GB | 1       | 44    | 1009  | 0.00   |
| Ramsta    | SSD S800           | 240 GB | 1       | 43    | 1012  | 0.00   |
| KingSpec  | ACJC2M060S25       | 64 GB  | 1       | 29    | 705   | 0.00   |
| Intel     | SSDSC2KF512H6 SATA | 512 GB | 3       | 16    | 707   | 0.00   |
| DOGGO     | DQ-60G             | 64 GB  | 2       | 0     | 0     | 0.00   |
| Hikvision | HS-SSD-E100N 1024G | 1 TB   | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSC2BB150G7      | 150 GB | 1       | 0     | 0     | 0.00   |
| KDATA     | SSD                | 128 GB | 1       | 0     | 0     | 0.00   |
| KLLISRE   | SSD                | 240 GB | 1       | 0     | 0     | 0.00   |
| KingDian  | M200               | 64 GB  | 1       | 0     | 0     | 0.00   |
| KingDian  | S180               | 120 GB | 1       | 0     | 0     | 0.00   |
| Netac     | Secureye SSD       | 128 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | WD Green 2.5       | 240 GB | 1       | 0     | 0     | 0.00   |
| Solid     | SSD0256S02         | 256 GB | 1       | 0     | 0     | 0.00   |
| TXRUI     | M750               | 512 GB | 1       | 0     | 0     | 0.00   |
| Transcend | TS16GCFX600I       | 16 GB  | 1       | 0     | 0     | 0.00   |
| Transcend | TS64GSSD420I       | 64 GB  | 1       | 0     | 0     | 0.00   |
| SSSTC     | CVB-8D128-HP       | 128 GB | 8       | 40    | 1008  | 0.00   |
| Lite-On   | CV8-8E256-HP       | 256 GB | 2       | 40    | 1007  | 0.00   |
| China     | IM3D L06B B0KB     | 120 GB | 1       | 2     | 66    | 0.00   |
| EGON      | S10                | 120 GB | 1       | 0     | 11    | 0.00   |
| Intel     | SSDSCKKB240G8R     | 240 GB | 1       | 31    | 1026  | 0.00   |
| Lite-On   | IT SCS-128L9S      | 128 GB | 1       | 35    | 1203  | 0.00   |
| China     | SSD-128G           | 128 GB | 1       | 0     | 9     | 0.00   |
| PNY       | SSD2SC240GE2DH1... | 240 GB | 1       | 29    | 1016  | 0.00   |
| tecmiyo   | SATA SSD           | 256 GB | 1       | 0     | 14    | 0.00   |
| Corsair   | CSSD-F240GB2       | 240 GB | 1       | 27    | 1009  | 0.00   |
| Micron    | MTFDDAV256TDL-1... | 256 GB | 14      | 26    | 1008  | 0.00   |
| Vaseky    | V820-1TB           | 1 TB   | 1       | 1     | 85    | 0.00   |
| SanDisk   | TE22D10400GE8001   | 400 GB | 1       | 34    | 2047  | 0.00   |
| JIAWEI    | SSD                | 240 GB | 1       | 47    | 3057  | 0.00   |
| Intel     | SSDSC2KW010X6      | 1 TB   | 4       | 3     | 369   | 0.00   |
| Kingston  | SNS4151S332GD      | 32 GB  | 3       | 14    | 1024  | 0.00   |
| Intel     | SSDSC2KW360H6      | 360 GB | 2       | 16    | 1365  | 0.00   |
| Neo Forza | NFS011SA356-600... | 256 GB | 1       | 41    | 3130  | 0.00   |
| Zebronics | ZEB-SD24           | 240 GB | 1       | 13    | 1012  | 0.00   |
| Intel     | SSDSC2KF240H6L     | 240 GB | 1       | 16    | 2012  | 0.00   |
| Lite-On   | IT LST-16S9G-HP    | 16 GB  | 1       | 6     | 1021  | 0.00   |
| KingSpec  | ACSC2M256mSA       | 256 GB | 1       | 5     | 1014  | 0.00   |
| Mushkin   | MKNSSDCR250GB-7... | 250 GB | 1       | 3     | 1016  | 0.00   |
| ADATA     | SX910              | 512 GB | 1       | 3     | 1018  | 0.00   |
| XrayDisk  | 240GB SSD          | 240 GB | 2       | 1     | 519   | 0.00   |
| Intel     | SSDSC2KG400G7M ... | 400 GB | 1       | 2     | 1025  | 0.00   |
| SanDisk   | sandisk120         | 120 GB | 1       | 0     | 21    | 0.00   |
| Kingston  | EK60HYXTFY176 V100 | 64 GB  | 1       | 1     | 1130  | 0.00   |
| SSSTC     | CVZ-83128-HP       | 128 GB | 1       | 1     | 1008  | 0.00   |
| Teclast   | 240GB SSD          | 240 GB | 1       | 1     | 1012  | 0.00   |
| DUEX      | DX240H             | 240 GB | 1       | 0     | 1007  | 0.00   |
| SMI       | SSD DISK           | 506 GB | 1       | 0     | 1957  | 0.00   |
| Mushkin   | MKNSSDCR480GB-7-A  | 480 GB | 1       | 0     | 1016  | 0.00   |

SSD by Family
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

| MFG       | Family                 | Models | Samples | Days  | Err   | MTBF |
|-----------|------------------------|--------|---------|-------|-------|------|
| Intel     | X25-E SSDs             | 2      | 4       | 2237  | 0     | 6.13   |
| Espada    | Unknown                | 1      | 1       | 2060  | 0     | 5.65   |
| EXBOM     | Unknown                | 1      | 1       | 1829  | 0     | 5.01   |
| Toshiba   | HK4R Series SSD        | 2      | 2       | 1433  | 0     | 3.93   |
| Kingston  | JMicron/Maxiotek ba... | 3      | 9       | 1426  | 0     | 3.91   |
| SMART     | Unknown                | 1      | 1       | 1374  | 0     | 3.77   |
| TANCA     | Unknown                | 1      | 1       | 1246  | 0     | 3.42   |
| Seagate   | Nytro XF1230 SATA SSD  | 1      | 2       | 1236  | 0     | 3.39   |
| HPE       | Unknown                | 7      | 7       | 1185  | 0     | 3.25   |
| Intel     | Dell Certified Inte... | 2      | 6       | 1247  | 1     | 3.15   |
| Intel     | 730 and DC S35x0/36... | 35     | 132     | 1239  | 102   | 2.98   |
| Micron    | MX100/MX200/M5x0/M6... | 1      | 1       | 1083  | 0     | 2.97   |
| SK        | hynix SATA SSDs        | 1      | 1       | 1054  | 0     | 2.89   |
| Intel     | X18-M/X25-M G1 SSDs    | 4      | 4       | 1037  | 0     | 2.84   |
| Crucial   | RealSSD m4/C400/P400   | 9      | 175     | 1007  | 179   | 2.39   |
| Crucial   | RealSSD C300/P300      | 3      | 25      | 1164  | 259   | 2.35   |
| Crucial   | RealSSD m4/C400        | 2      | 15      | 832   | 135   | 2.17   |
| Transcend | Unknown                | 29     | 66      | 882   | 33    | 2.17   |
| Radeon    | Indilinx Barefoot 3... | 1      | 4       | 778   | 0     | 2.13   |
| TCSUNB0W  | Unknown                | 1      | 1       | 767   | 0     | 2.10   |
| Toshiba   | HG2 Series             | 2      | 9       | 760   | 0     | 2.08   |
| Micro ... | Unknown                | 1      | 1       | 722   | 0     | 1.98   |
| Intel     | 320 Series SSDs        | 13     | 115     | 787   | 20    | 1.98   |
| Corsair   | SandForce Driven SSDs  | 31     | 241     | 877   | 95    | 1.94   |
| SandForce | SandForce Driven SSDs  | 3      | 3       | 806   | 139   | 1.92   |
| Toshiba   | JMicron/Maxiotek ba... | 1      | 3       | 698   | 0     | 1.91   |
| OCZ       | SandForce Driven SSDs  | 48     | 453     | 860   | 40    | 1.85   |
| Intel     | 520 Series SSDs        | 9      | 168     | 831   | 194   | 1.84   |
| Toshiba   | HG3 Series             | 3      | 7       | 658   | 0     | 1.80   |
| SuperM... | Silicon Motion base... | 2      | 3       | 650   | 0     | 1.78   |
| OCZ       | Indilinx Barefoot_2... | 12     | 174     | 724   | 3     | 1.68   |
| OCZ       | Indilinx Barefoot b... | 6      | 14      | 691   | 1     | 1.60   |
| Toshiba   | OCZ                    | 6      | 24      | 606   | 1     | 1.59   |
| Galaxy    | Unknown                | 1      | 1       | 578   | 0     | 1.58   |
| SATADOM   | Innodisk 3IE3/3ME3/... | 1      | 1       | 574   | 0     | 1.57   |
| ADATA     | JMicron/Maxiotek ba... | 5      | 28      | 589   | 4     | 1.56   |
| Intel     | 525 Series SSDs        | 3      | 9       | 722   | 1     | 1.56   |
| Intel     | S3520 Series SSDs      | 4      | 4       | 977   | 1     | 1.56   |
| OWC       | SandForce Driven SSDs  | 3      | 24      | 619   | 4     | 1.55   |
| Intel     | 330/335 Series SSDs    | 6      | 87      | 781   | 1     | 1.47   |
| ADATA     | JMicron based SSDs     | 7      | 44      | 542   | 1     | 1.43   |
| Mushkin   | SandForce Driven SSDs  | 16     | 35      | 693   | 177   | 1.42   |
| MyDigi... | Unknown                | 4      | 13      | 515   | 0     | 1.41   |
| Toshiba   | HG6 Series SSD         | 20     | 122     | 516   | 1     | 1.41   |
| Apple     | JMicron based SSDs     | 3      | 21      | 538   | 1     | 1.40   |
| Samsung   | Unknown                | 40     | 100     | 557   | 14    | 1.39   |
| Micron    | RealSSD m4/C400/P400   | 8      | 72      | 536   | 196   | 1.37   |
| Micron    | 5100 Pro / 5200 / 5... | 4      | 14      | 493   | 0     | 1.35   |
| ADROIT... | Unknown                | 1      | 1       | 493   | 0     | 1.35   |
| Axiom     | Unknown                | 3      | 3       | 473   | 0     | 1.30   |
| OCZ       | OCZ/Toshiba Trion SSDs | 6      | 58      | 490   | 1     | 1.29   |
| Samsung   | Samsung based SSDs     | 351    | 9574    | 476   | 8     | 1.26   |
| ADATA     | SandForce Driven SSDs  | 15     | 131     | 514   | 4     | 1.24   |
| Micron    | 5100 Pro / 5200 SSDs   | 6      | 22      | 562   | 16    | 1.23   |
| Toshiba   | OCZ/Toshiba Trion SSDs | 7      | 81      | 477   | 1     | 1.22   |
| Transcend | JMicron based SSDs     | 7      | 22      | 453   | 46    | 1.21   |
| Toshiba   | HG6 Series             | 1      | 7       | 443   | 0     | 1.21   |
| Kingston  | SandForce Driven SSDs  | 42     | 1717    | 530   | 41    | 1.20   |
| Kingston  | JMicron based SSDs     | 13     | 60      | 645   | 3     | 1.18   |
| Seagate   | 600 Series             | 1      | 2       | 429   | 0     | 1.18   |
| Transcend | SandForce Driven SSDs  | 6      | 15      | 544   | 12    | 1.16   |
| Hajaan    | Unknown                | 1      | 2       | 420   | 0     | 1.15   |
| OCZ       | Indilinx Barefoot 3... | 18     | 118     | 495   | 20    | 1.14   |
| Toshiba   | HG5 Series             | 1      | 9       | 414   | 0     | 1.13   |
| Apple     | SD/SM/TS E/F/G SSDs    | 18     | 332     | 422   | 2     | 1.13   |
| Toshiba   | HG5d Series            | 8      | 32      | 458   | 21    | 1.11   |
| Goodram   | Phison Driven OEM SSDs | 4      | 81      | 402   | 1     | 1.10   |
| OYUNKEY   | Unknown                | 2      | 3       | 512   | 44    | 1.08   |
| Intel     | 510 Series SSDs        | 2      | 6       | 388   | 0     | 1.06   |
| DIERYA    | Unknown                | 1      | 1       | 385   | 0     | 1.06   |
| FCS       | Unknown                | 1      | 1       | 381   | 0     | 1.05   |
| Seagate   | Indilinx Barefoot b... | 1      | 1       | 378   | 0     | 1.04   |
| CFD       | Unknown                | 3      | 3       | 375   | 0     | 1.03   |
| Kingston  | SSDNow UV400           | 1      | 38      | 421   | 78    | 1.03   |
| KingShare | Unknown                | 2      | 2       | 373   | 0     | 1.02   |
| Redapple  | Unknown                | 1      | 1       | 363   | 0     | 1.00   |
| addlink   | Unknown                | 2      | 4       | 359   | 0     | 0.98   |
| Intel     | S4510/S4610/S4500/S... | 16     | 116     | 379   | 27    | 0.97   |
| Crucial   | BX/MX1/2/3/500, M5/... | 22     | 486     | 470   | 67    | 0.96   |
| THU       | Unknown                | 1      | 1       | 339   | 0     | 0.93   |
| SanDisk   | SATA Cloudspeed Max... | 3      | 4       | 333   | 0     | 0.91   |
| Corsair   | Unknown                | 25     | 60      | 669   | 92    | 0.91   |
| Phison    | Phison Driven SSDs     | 4      | 6       | 328   | 0     | 0.90   |
| Intel     | 53x and Pro 1500/25... | 18     | 204     | 476   | 7     | 0.87   |
| WDC       | Blue and Green SSDs    | 6      | 93      | 321   | 1     | 0.86   |
| Palit     | Unknown                | 8      | 14      | 314   | 0     | 0.86   |
| Aura      | Unknown                | 1      | 1       | 310   | 0     | 0.85   |
| Micron    | RealSSD m4/C400        | 3      | 10      | 336   | 304   | 0.84   |
| Corsair   | Indilinx Barefoot b... | 4      | 5       | 372   | 1     | 0.83   |
| Kingston  | SSDNow UV400/500       | 13     | 570     | 339   | 58    | 0.83   |
| SanDisk   | SanDisk based SSDs     | 35     | 480     | 336   | 19    | 0.82   |
| Innodisk  | 3IE3/3ME3/3ME4 SSDs    | 4      | 9       | 425   | 11    | 0.81   |
| Apacer    | SSDs                   | 1      | 2       | 296   | 0     | 0.81   |
| Toshiba   | Unknown                | 66     | 325     | 324   | 16    | 0.81   |
| XSTAR     | Unknown                | 2      | 2       | 286   | 0     | 0.78   |
| Toshiba   | JMicron based SSDs     | 1      | 2       | 284   | 0     | 0.78   |
| Corsair   | Phison Driven SSDs     | 2      | 18      | 315   | 4     | 0.75   |
| SanDisk   | Marvell based SanDi... | 82     | 1673    | 299   | 37    | 0.74   |
| ZOTAC     | Unknown                | 3      | 4       | 268   | 0     | 0.74   |
| SanDisk   | SandForce Driven SSDs  | 6      | 414     | 313   | 18    | 0.73   |
| Intel     | Dell Certified Inte... | 3      | 3       | 265   | 0     | 0.73   |
| Exascend  | Unknown                | 1      | 1       | 264   | 0     | 0.73   |
| SanDisk   | Unknown                | 164    | 878     | 268   | 16    | 0.71   |
| Micron    | 5100 Pro / 52x0 / 5... | 9      | 18      | 337   | 3     | 0.71   |
| TAISU     | Unknown                | 2      | 2       | 254   | 0     | 0.70   |
| PNY       | Phison Driven SSDs     | 10     | 340     | 251   | 0     | 0.69   |
| Patriot   | Phison Driven SSDs     | 11     | 314     | 247   | 1     | 0.67   |
| Hoodisk   | Phison Driven OEM SSDs | 5      | 26      | 245   | 0     | 0.67   |
| Team      | Silicon Motion base... | 5      | 22      | 242   | 0     | 0.66   |
| Smart     | Unknown                | 3      | 3       | 241   | 0     | 0.66   |
| G.Skill   | Unknown                | 1      | 1       | 241   | 0     | 0.66   |
| Seagate   | Unknown                | 24     | 114     | 278   | 36    | 0.66   |
| GALAX     | Unknown                | 3      | 10      | 238   | 0     | 0.65   |
| Yunhai... | Unknown                | 2      | 2       | 236   | 0     | 0.65   |
| VENO S... | Unknown                | 2      | 2       | 234   | 0     | 0.64   |
| Innodisk  | Unknown                | 9      | 14      | 232   | 1     | 0.64   |
| Intel     | X18-M/X25-M/X25-V G... | 14     | 75      | 754   | 17    | 0.63   |
| GAMER     | Unknown                | 1      | 1       | 230   | 0     | 0.63   |
| LVCARDS   | Unknown                | 1      | 1       | 229   | 0     | 0.63   |
| Plextor   | M3/M5/M6/M7 Series ... | 13     | 49      | 231   | 74    | 0.63   |
| SK hynix  | SATA SSDs              | 46     | 515     | 309   | 85    | 0.62   |
| BlitzWolf | Unknown                | 1      | 1       | 225   | 0     | 0.62   |
| WDC       | Unknown                | 8      | 20      | 252   | 247   | 0.62   |
| Micron    | Client SSDs            | 36     | 252     | 282   | 85    | 0.61   |
| ASUS      | Unknown                | 1      | 1       | 221   | 0     | 0.61   |
| Smartbuy  | Phison Driven SSDs     | 6      | 181     | 232   | 1     | 0.60   |
| BlueRay   | Unknown                | 5      | 5       | 246   | 1     | 0.60   |
| Hyundai   | Unknown                | 7      | 10      | 218   | 0     | 0.60   |
| Kingston  | Unknown                | 121    | 367     | 258   | 80    | 0.59   |
| Intenso   | Phison Driven OEM SSDs | 4      | 124     | 215   | 1     | 0.58   |
| KingFast  | Unknown                | 9      | 36      | 216   | 1     | 0.58   |
| Crucial   | MX500 SSDs             | 1      | 58      | 211   | 0     | 0.58   |
| Transcend | JMicron/Maxiotek ba... | 5      | 9       | 218   | 112   | 0.57   |
| AFOX      | Unknown                | 3      | 5       | 208   | 0     | 0.57   |
| Micron    | BX/MX1/2/3/500, M5/... | 11     | 227     | 254   | 97    | 0.57   |
| Pioneer   | Unknown                | 7      | 20      | 206   | 0     | 0.57   |
| SPCC      | Phison Driven OEM SSDs | 8      | 712     | 231   | 47    | 0.56   |
| Kston     | Unknown                | 3      | 7       | 204   | 0     | 0.56   |
| BIOSTAR   | Unknown                | 3      | 4       | 203   | 0     | 0.56   |
| Drevo     | Unknown                | 6      | 9       | 321   | 544   | 0.55   |
| Quaroni   | Unknown                | 1      | 1       | 201   | 0     | 0.55   |
| Smartbuy  | Unknown                | 11     | 20      | 201   | 0     | 0.55   |
| Crucial   | Indilinx Barefoot b... | 1      | 1       | 200   | 0     | 0.55   |
| China     | Phison Driven OEM SSDs | 11     | 313     | 202   | 1     | 0.55   |
| Gigabyte  | Phison Driven SSDs     | 3      | 63      | 198   | 0     | 0.54   |
| JIESHUO   | Unknown                | 1      | 1       | 196   | 0     | 0.54   |
| SuperM... | SATA DOM (SuperDOM)    | 1      | 2       | 193   | 0     | 0.53   |
| Advantech | Unknown                | 10     | 11      | 191   | 0     | 0.52   |
| WDC       | Blue / Red / Green ... | 40     | 2344    | 202   | 3     | 0.52   |
| DERLER    | Unknown                | 1      | 1       | 188   | 0     | 0.52   |
| Kingston  | Phison Driven SSDs     | 27     | 3215    | 201   | 1     | 0.52   |
| OCZ       | Intrepid 3000 SSDs     | 4      | 4       | 331   | 255   | 0.51   |
| Plextor   | Unknown                | 35     | 113     | 196   | 1     | 0.51   |
| Reeinno   | Unknown                | 2      | 3       | 183   | 0     | 0.50   |
| Phison    | Driven OEM SSDs        | 10     | 105     | 182   | 0     | 0.50   |
| Intel     | Unknown                | 67     | 229     | 237   | 76    | 0.50   |
| Crucial   | Client SSDs            | 31     | 2920    | 203   | 7     | 0.49   |
| DeTech    | Unknown                | 1      | 3       | 179   | 0     | 0.49   |
| Intel     | 53x and Pro 2500 Se... | 2      | 2       | 177   | 0     | 0.49   |
| SPCC      | Unknown                | 28     | 80      | 330   | 231   | 0.48   |
| minisf... | Unknown                | 2      | 3       | 173   | 0     | 0.48   |
| HP        | Unknown                | 23     | 137     | 184   | 6     | 0.48   |
| Apple     | Unknown                | 4      | 12      | 358   | 245   | 0.47   |
| Gigaby... | Unknown                | 4      | 10      | 168   | 0     | 0.46   |
| Micron    | Unknown                | 34     | 95      | 309   | 121   | 0.46   |
| Imation   | Unknown                | 2      | 2       | 168   | 0     | 0.46   |
| Best M... | Unknown                | 1      | 1       | 167   | 0     | 0.46   |
| Ramaxel   | Unknown                | 5      | 8       | 202   | 1     | 0.45   |
| ExeGate   | Unknown                | 6      | 8       | 162   | 0     | 0.45   |
| Patriot   | Unknown                | 32     | 126     | 199   | 33    | 0.44   |
| Intel     | 311/313 Series SSDs    | 1      | 3       | 197   | 10    | 0.44   |
| Samgporse | Unknown                | 1      | 1       | 156   | 0     | 0.43   |
| Team      | Unknown                | 50     | 196     | 173   | 4     | 0.42   |
| Goodram   | Phison Driven SSDs     | 6      | 95      | 154   | 0     | 0.42   |
| ADTEC     | Unknown                | 1      | 2       | 152   | 0     | 0.42   |
| OCZ       | Unknown                | 10     | 15      | 652   | 137   | 0.42   |
| BRAVEE... | Unknown                | 3      | 3       | 151   | 0     | 0.41   |
| TCSUNBOW  | Unknown                | 6      | 15      | 150   | 0     | 0.41   |
| Innodisk  | 1ME3/3ME/3SE SSDs      | 1      | 1       | 150   | 0     | 0.41   |
| Plextor   | M3/M5/M6 Series SSDs   | 18     | 219     | 173   | 50    | 0.41   |
| JASTER    | Unknown                | 1      | 3       | 147   | 0     | 0.40   |
| Apacer    | SDM5/5A/5A-M Series... | 2      | 5       | 153   | 42    | 0.40   |
| Gigabyte  | Unknown                | 4      | 9       | 146   | 0     | 0.40   |
| Union ... | Unknown                | 1      | 12      | 144   | 0     | 0.40   |
| KingDian  | Silicon Motion base... | 10     | 88      | 147   | 2     | 0.40   |
| Goodram   | Unknown                | 32     | 248     | 148   | 1     | 0.39   |
| Plextor   | M3/M5 (Pro) Series ... | 3      | 17      | 205   | 62    | 0.39   |
| EAGET     | Unknown                | 2      | 2       | 141   | 0     | 0.39   |
| Crucial   | Unknown                | 16     | 30      | 176   | 2     | 0.38   |
| MENGMI    | Unknown                | 1      | 1       | 139   | 0     | 0.38   |
| WINTEN    | Unknown                | 1      | 1       | 138   | 0     | 0.38   |
| KingFast  | Silicon Motion base... | 4      | 51      | 140   | 61    | 0.38   |
| AMD       | Silicon Motion base... | 3      | 47      | 156   | 6     | 0.38   |
| ADATA     | Unknown                | 78     | 515     | 214   | 123   | 0.38   |
| Phison    | Unknown                | 19     | 35      | 137   | 1     | 0.37   |
| Super ... | Unknown                | 7      | 13      | 161   | 1     | 0.37   |
| UNIC2     | Unknown                | 2      | 6       | 135   | 0     | 0.37   |
| MACROVIP  | Unknown                | 1      | 1       | 134   | 0     | 0.37   |
| KingDian  | Unknown                | 18     | 62      | 146   | 143   | 0.37   |
| Maxtor    | Unknown                | 3      | 20      | 132   | 0     | 0.36   |
| SK hynix  | Unknown                | 39     | 130     | 294   | 135   | 0.36   |
| ADATA     | Silicon Motion base... | 23     | 741     | 144   | 38    | 0.35   |
| Chiprex   | Unknown                | 1      | 1       | 126   | 0     | 0.35   |
| Intel     | 545s Series SSDs       | 10     | 135     | 140   | 1     | 0.35   |
| Silicon   | Motion based OEM SSDs  | 5      | 7       | 123   | 0     | 0.34   |
| Londisk   | Unknown                | 4      | 19      | 123   | 0     | 0.34   |
| Hypertec  | Unknown                | 1      | 2       | 371   | 512   | 0.33   |
| Verbatim  | Unknown                | 7      | 37      | 123   | 28    | 0.33   |
| Mushkin   | Silicon Motion base... | 6      | 13      | 120   | 0     | 0.33   |
| Inland    | Unknown                | 4      | 5       | 119   | 0     | 0.33   |
| TwinMOS   | Unknown                | 3      | 4       | 132   | 1     | 0.33   |
| LDLC      | Unknown                | 14     | 55      | 157   | 10    | 0.32   |
| Apacer    | Unknown                | 22     | 255     | 117   | 13    | 0.32   |
| Samsung   | SandForce Driven SSDs  | 1      | 1       | 115   | 0     | 0.32   |
| HXY       | Unknown                | 1      | 1       | 115   | 0     | 0.32   |
| Ramsta    | Silicon Motion base... | 3      | 3       | 128   | 338   | 0.31   |
| Silico... | Unknown                | 3      | 3       | 111   | 0     | 0.31   |
| SFAS      | Unknown                | 1      | 1       | 111   | 0     | 0.31   |
| SuperS... | Unknown                | 1      | 1       | 110   | 0     | 0.30   |
| Vaseky    | Unknown                | 20     | 32      | 113   | 4     | 0.30   |
| PNY       | Unknown                | 52     | 155     | 147   | 54    | 0.30   |
| BAITITON  | Unknown                | 10     | 15      | 142   | 3     | 0.30   |
| Mushkin   | Unknown                | 22     | 42      | 164   | 104   | 0.30   |
| Kingmax   | Unknown                | 5      | 68      | 243   | 310   | 0.30   |
| Apacer    | AS340 SSDs             | 4      | 73      | 121   | 30    | 0.30   |
| AirDisk   | Unknown                | 1      | 3       | 108   | 0     | 0.30   |
| ZTC       | Unknown                | 3      | 6       | 108   | 0     | 0.30   |
| Gigaby... | Phison Driven SSDs     | 3      | 78      | 108   | 0     | 0.30   |
| Transcend | Silicon Motion base... | 50     | 425     | 111   | 16    | 0.29   |
| Zheino    | Silicon Motion base... | 1      | 3       | 106   | 0     | 0.29   |
| TREKSTOR  | Unknown                | 1      | 1       | 105   | 0     | 0.29   |
| MARVELL   | based SanDisk SSDs     | 1      | 1       | 105   | 0     | 0.29   |
| GLOWAY    | Unknown                | 13     | 21      | 117   | 67    | 0.29   |
| China     | Unknown                | 184    | 836     | 115   | 21    | 0.29   |
| KingSpec  | Unknown                | 49     | 219     | 126   | 34    | 0.28   |
| tigo      | Unknown                | 4      | 5       | 103   | 0     | 0.28   |
| e2e4      | Unknown                | 4      | 9       | 103   | 0     | 0.28   |
| Transcend | Indilinx Barefoot b... | 1      | 1       | 309   | 2     | 0.28   |
| Colorful  | Unknown                | 9      | 21      | 136   | 68    | 0.28   |
| GeIL      | Unknown                | 12     | 16      | 117   | 64    | 0.28   |
| Lexar     | Unknown                | 11     | 86      | 102   | 1     | 0.28   |
| Apacer    | SDM4 Series SSD Module | 2      | 20      | 265   | 14    | 0.28   |
| T-FORCE   | Unknown                | 5      | 31      | 101   | 1     | 0.28   |
| JAMESD... | Unknown                | 3      | 3       | 99    | 0     | 0.27   |
| Fujitsu   | Unknown                | 6      | 6       | 98    | 0     | 0.27   |
| TrekStor  | Unknown                | 3      | 4       | 127   | 39    | 0.27   |
| RZX       | Unknown                | 2      | 3       | 96    | 0     | 0.26   |
| Biostar   | Unknown                | 6      | 8       | 96    | 0     | 0.26   |
| EZCOOL    | Unknown                | 2      | 2       | 95    | 0     | 0.26   |
| Crucial   | MX1/2/300, M5/600, ... | 1      | 12      | 1064  | 100   | 0.26   |
| GOWE      | Unknown                | 1      | 1       | 284   | 2     | 0.26   |
| Crucial   | Silicon Motion base... | 7      | 144     | 94    | 1     | 0.26   |
| Seagate   | IronWolf 110 SATA SSD  | 3      | 6       | 92    | 0     | 0.25   |
| Lite-On   | Silicon Motion base... | 5      | 22      | 95    | 1     | 0.25   |
| VisionTek | Unknown                | 1      | 2       | 88    | 0     | 0.24   |
| Dogfish   | Unknown                | 8      | 22      | 96    | 1     | 0.24   |
| AXIOM     | Unknown                | 1      | 1       | 87    | 0     | 0.24   |
| Lumino... | Unknown                | 5      | 5       | 87    | 0     | 0.24   |
| ShanDi... | Unknown                | 3      | 9       | 87    | 0     | 0.24   |
| Lite-On   | Unknown                | 131    | 481     | 110   | 123   | 0.24   |
| AGI       | Unknown                | 6      | 8       | 92    | 5     | 0.24   |
| Integral  | Unknown                | 4      | 17      | 85    | 0     | 0.23   |
| Lenovo    | Unknown                | 8      | 14      | 108   | 1     | 0.23   |
| Patriot   | Silicon Motion base... | 4      | 21      | 170   | 35    | 0.23   |
| Lexar     | 128GB SSD              | 1      | 30      | 82    | 0     | 0.23   |
| Drevo     | Silicon Motion base... | 2      | 13      | 262   | 27    | 0.23   |
| SMI       | Unknown                | 8      | 8       | 82    | 245   | 0.23   |
| BIWIN     | Unknown                | 7      | 29      | 94    | 107   | 0.23   |
| BHT       | Unknown                | 9      | 29      | 82    | 0     | 0.23   |
| Nfortec   | Unknown                | 1      | 1       | 82    | 0     | 0.22   |
| Intenso   | Silicon Motion base... | 8      | 113     | 94    | 46    | 0.22   |
| XUM       | Unknown                | 2      | 3       | 81    | 0     | 0.22   |
| Zheino    | Unknown                | 23     | 39      | 99    | 1     | 0.22   |
| ASENNO    | Unknown                | 3      | 6       | 140   | 4     | 0.22   |
| Apple     | JMicron/Maxiotek ba... | 1      | 1       | 79    | 0     | 0.22   |
| Intenso   | Unknown                | 49     | 158     | 86    | 41    | 0.22   |
| KingSpec  | JMicron/Maxiotek ba... | 3      | 48      | 95    | 43    | 0.22   |
| GS Nan... | Unknown                | 4      | 5       | 77    | 0     | 0.21   |
| AMD       | Unknown                | 13     | 96      | 93    | 18    | 0.21   |
| INNOVA... | Unknown                | 14     | 35      | 79    | 1     | 0.21   |
| SPEED UP  | Unknown                | 1      | 1       | 75    | 0     | 0.21   |
| Wdstars   | Unknown                | 2      | 2       | 71    | 0     | 0.20   |
| Varro     | Unknown                | 3      | 3       | 71    | 0     | 0.19   |
| V-GeN     | Unknown                | 14     | 16      | 69    | 0     | 0.19   |
| Indilinx  | Unknown                | 8      | 10      | 71    | 2     | 0.19   |
| Neo Forza | Unknown                | 6      | 10      | 126   | 520   | 0.19   |
| ViperTeq  | Unknown                | 1      | 1       | 68    | 0     | 0.19   |
| Gost      | Unknown                | 2      | 2       | 68    | 0     | 0.19   |
| OWC       | Unknown                | 4      | 8       | 67    | 0     | 0.19   |
| Hikvision | Unknown                | 22     | 69      | 71    | 1     | 0.18   |
| TAMMUZ    | Unknown                | 4      | 4       | 66    | 0     | 0.18   |
| KLONER    | Unknown                | 1      | 1       | 66    | 0     | 0.18   |
| FORESEE   | Unknown                | 10     | 65      | 65    | 0     | 0.18   |
| Kingch... | Unknown                | 8      | 15      | 65    | 0     | 0.18   |
| HGST      | Unknown                | 1      | 2       | 65    | 0     | 0.18   |
| Seagate   | Nytro SATA SSD         | 3      | 10      | 65    | 0     | 0.18   |
| Foxline   | Unknown                | 13     | 29      | 96    | 36    | 0.17   |
| Golden... | Unknown                | 4      | 4       | 62    | 0     | 0.17   |
| Leven     | Unknown                | 10     | 47      | 71    | 2     | 0.17   |
| SUNEAST   | Unknown                | 6      | 8       | 120   | 22    | 0.17   |
| Platinet  | Unknown                | 1      | 3       | 61    | 30    | 0.17   |
| Timetec   | Unknown                | 5      | 6       | 60    | 0     | 0.17   |
| Blackpcs  | Unknown                | 3      | 3       | 60    | 0     | 0.17   |
| TCSUNBOW  | Silicon Motion base... | 3      | 11      | 59    | 0     | 0.16   |
| TEKET     | Unknown                | 1      | 2       | 59    | 0     | 0.16   |
| ORICO     | Unknown                | 5      | 5       | 94    | 1     | 0.16   |
| EYOTA     | Unknown                | 1      | 1       | 58    | 0     | 0.16   |
| Dogfish   | Silicon Motion base... | 3      | 34      | 57    | 1     | 0.15   |
| Ramsta    | Unknown                | 3      | 3       | 56    | 0     | 0.15   |
| ASMedia   | Unknown                | 1      | 4       | 55    | 0     | 0.15   |
| EMTEC     | Unknown                | 6      | 31      | 55    | 0     | 0.15   |
| VISIPRO   | Unknown                | 3      | 5       | 56    | 3     | 0.15   |
| Aoluska   | Unknown                | 1      | 1       | 54    | 0     | 0.15   |
| PUSKILL   | Unknown                | 3      | 3       | 53    | 0     | 0.15   |
| Teutons   | Unknown                | 2      | 2       | 53    | 0     | 0.15   |
| KINGBANK  | Unknown                | 2      | 7       | 53    | 0     | 0.15   |
| IPLEX     | Unknown                | 1      | 1       | 52    | 0     | 0.14   |
| JUHOR     | Unknown                | 1      | 1       | 52    | 0     | 0.14   |
| HEORIADY  | Unknown                | 3      | 4       | 49    | 0     | 0.14   |
| JD        | Unknown                | 2      | 2       | 169   | 53    | 0.14   |
| Qumo      | Unknown                | 5      | 10      | 169   | 204   | 0.14   |
| Greenl... | Unknown                | 1      | 1       | 49    | 0     | 0.13   |
| Anobit    | Unknown                | 1      | 2       | 48    | 1     | 0.13   |
| Avant     | Unknown                | 3      | 4       | 432   | 254   | 0.13   |
| Win Me... | Unknown                | 3      | 5       | 48    | 0     | 0.13   |
| XrayDisk  | Unknown                | 11     | 58      | 54    | 37    | 0.13   |
| Kross ... | Unknown                | 2      | 3       | 47    | 0     | 0.13   |
| XPG       | Unknown                | 1      | 3       | 46    | 0     | 0.13   |
| S3+       | Unknown                | 7      | 9       | 91    | 6     | 0.13   |
| RCESSD    | Unknown                | 1      | 2       | 46    | 0     | 0.13   |
| Fanxiang  | Unknown                | 6      | 7       | 46    | 0     | 0.13   |
| LENSEN    | Unknown                | 1      | 1       | 46    | 0     | 0.13   |
| KLEVV     | Unknown                | 4      | 5       | 45    | 0     | 0.13   |
| Kingston  | Silicon Motion base... | 4      | 85      | 46    | 1     | 0.12   |
| MARSHAL   | Unknown                | 1      | 1       | 44    | 0     | 0.12   |
| Netac     | Unknown                | 31     | 236     | 50    | 15    | 0.12   |
| Apple     | MacBook Air SSD        | 2      | 10      | 87    | 20    | 0.12   |
| FATTYDOVE | Unknown                | 1      | 1       | 44    | 0     | 0.12   |
| PRETEC    | Unknown                | 1      | 1       | 44    | 0     | 0.12   |
| ORIGIN... | Unknown                | 1      | 1       | 43    | 0     | 0.12   |
| Intel     | SSD Pro 5400s Series   | 1      | 1       | 42    | 0     | 0.12   |
| Acer      | Unknown                | 3      | 8       | 41    | 0     | 0.11   |
| GSemi     | Unknown                | 1      | 2       | 41    | 0     | 0.11   |
| Fordisk   | Unknown                | 2      | 2       | 41    | 0     | 0.11   |
| Faspeed   | Unknown                | 15     | 16      | 43    | 1     | 0.11   |
| Dogeish   | Unknown                | 1      | 1       | 40    | 0     | 0.11   |
| Solid     | Unknown                | 3      | 6       | 42    | 1     | 0.11   |
| QUMO      | Unknown                | 12     | 19      | 52    | 2     | 0.11   |
| MediaR... | Unknown                | 1      | 1       | 39    | 0     | 0.11   |
| Goldkey   | Unknown                | 2      | 2       | 39    | 0     | 0.11   |
| Star D... | Unknown                | 3      | 6       | 38    | 0     | 0.11   |
| Kingrich  | Unknown                | 6      | 7       | 121   | 2     | 0.10   |
| Yeyian    | Unknown                | 3      | 5       | 37    | 0     | 0.10   |
| KIOXIA... | Unknown                | 3      | 42      | 36    | 0     | 0.10   |
| TOPMORE   | Unknown                | 1      | 1       | 36    | 0     | 0.10   |
| NTC       | Unknown                | 1      | 1       | 35    | 0     | 0.10   |
| Hanye     | Unknown                | 1      | 1       | 35    | 0     | 0.10   |
| TakeMS    | Unknown                | 1      | 1       | 34    | 0     | 0.10   |
| RESCUE    | Unknown                | 1      | 1       | 34    | 0     | 0.10   |
| RX7       | Unknown                | 3      | 3       | 36    | 4     | 0.10   |
| ANACOMDA  | Unknown                | 2      | 2       | 34    | 0     | 0.09   |
| SemsoTai  | Unknown                | 2      | 2       | 37    | 5     | 0.09   |
| Gateway   | Unknown                | 2      | 4       | 33    | 0     | 0.09   |
| AEGO      | Unknown                | 1      | 3       | 33    | 0     | 0.09   |
| Toshiba   | SG2 Series             | 1      | 1       | 32    | 0     | 0.09   |
| ORTIAL    | Unknown                | 3      | 11      | 30    | 0     | 0.08   |
| KingPower | Unknown                | 1      | 1       | 29    | 0     | 0.08   |
| TEXTORM   | Unknown                | 4      | 8       | 30    | 5     | 0.08   |
| ACPI      | Unknown                | 3      | 3       | 29    | 0     | 0.08   |
| OSCOO     | Unknown                | 5      | 5       | 30    | 18    | 0.08   |
| Silico... | Unknown                | 2      | 2       | 27    | 0     | 0.08   |
| Tammuz    | Unknown                | 1      | 1       | 27    | 0     | 0.08   |
| SPCC      | Silicon Motion base... | 1      | 3       | 30    | 904   | 0.08   |
| SenDisk   | Unknown                | 1      | 1       | 27    | 0     | 0.08   |
| i-Flas... | Unknown                | 2      | 2       | 27    | 0     | 0.07   |
| Transcend | SiliconMotion based... | 2      | 2       | 26    | 0     | 0.07   |
| HECTRON   | Unknown                | 1      | 1       | 26    | 0     | 0.07   |
| Teclast   | Unknown                | 18     | 41      | 36    | 26    | 0.07   |
| Rogueware | Unknown                | 2      | 2       | 25    | 0     | 0.07   |
| Pasoul    | Unknown                | 1      | 1       | 25    | 0     | 0.07   |
| Wdxsky    | Unknown                | 1      | 1       | 25    | 0     | 0.07   |
| MidasF... | Unknown                | 4      | 9       | 25    | 0     | 0.07   |
| Eluktro   | Unknown                | 2      | 2       | 428   | 508   | 0.07   |
| KeepData  | Unknown                | 2      | 4       | 24    | 0     | 0.07   |
| KLLISRE   | Unknown                | 3      | 3       | 24    | 0     | 0.07   |
| Wibtek    | Unknown                | 3      | 10      | 23    | 11    | 0.07   |
| SNR       | Unknown                | 1      | 1       | 23    | 0     | 0.07   |
| SCY       | Unknown                | 2      | 3       | 23    | 0     | 0.06   |
| Supers... | Unknown                | 2      | 2       | 23    | 0     | 0.06   |
| WALRAM    | Unknown                | 5      | 17      | 25    | 6     | 0.06   |
| RECADATA  | Unknown                | 2      | 2       | 23    | 0     | 0.06   |
| ZHITAI    | Unknown                | 3      | 5       | 21    | 0     | 0.06   |
| ELSKY     | Unknown                | 1      | 1       | 21    | 0     | 0.06   |
| Silicon   | Silicon Motion base... | 1      | 1       | 21    | 0     | 0.06   |
| Valuetech | Unknown                | 2      | 2       | 21    | 0     | 0.06   |
| GHIA      | Unknown                | 1      | 1       | 20    | 0     | 0.06   |
| Dell      | Unknown                | 3      | 9       | 20    | 0     | 0.06   |
| XUNZHE    | Unknown                | 1      | 1       | 20    | 0     | 0.05   |
| Force Le  | Unknown                | 1      | 1       | 19    | 0     | 0.05   |
| JUMPER    | Unknown                | 1      | 2       | 19    | 0     | 0.05   |
| Kimtigo   | Unknown                | 1      | 4       | 18    | 0     | 0.05   |
| Hyperdisk | Unknown                | 1      | 1       | 18    | 0     | 0.05   |
| UMIS      | Unknown                | 1      | 1       | 18    | 0     | 0.05   |
| Yeestor   | Unknown                | 1      | 1       | 17    | 0     | 0.05   |
| Kingspeed | Unknown                | 2      | 2       | 17    | 0     | 0.05   |
| LDNDISK   | Unknown                | 1      | 1       | 16    | 0     | 0.05   |
| Golden... | Unknown                | 1      | 1       | 16    | 0     | 0.04   |
| MOVESPEED | Unknown                | 1      | 1       | 15    | 0     | 0.04   |
| Leven     | Silicon Motion base... | 1      | 1       | 15    | 0     | 0.04   |
| Innodisk  | 3IE2/3ME2/3MG2/3SE2... | 2      | 6       | 40    | 505   | 0.04   |
| RevuAhn   | Unknown                | 1      | 1       | 14    | 0     | 0.04   |
| Seagate   | 600 Pro Series         | 1      | 1       | 14    | 0     | 0.04   |
| NFORCE    | Unknown                | 1      | 1       | 14    | 0     | 0.04   |
| BR        | Unknown                | 5      | 5       | 14    | 0     | 0.04   |
| ADLINK    | Unknown                | 1      | 1       | 13    | 0     | 0.04   |
| Origin... | Unknown                | 1      | 1       | 171   | 12    | 0.04   |
| SomnAm... | Unknown                | 1      | 1       | 25    | 1     | 0.04   |
| Getrich   | Unknown                | 1      | 1       | 12    | 0     | 0.04   |
| RAMOS     | Unknown                | 2      | 2       | 12    | 0     | 0.04   |
| KUIJIA    | Unknown                | 1      | 1       | 12    | 0     | 0.03   |
| EVM       | Unknown                | 1      | 2       | 12    | 0     | 0.03   |
| Azerty    | Unknown                | 2      | 3       | 12    | 0     | 0.03   |
| Wicgtyp   | Unknown                | 1      | 1       | 12    | 0     | 0.03   |
| Gigastone | Unknown                | 2      | 2       | 12    | 0     | 0.03   |
| Microtech | Unknown                | 2      | 2       | 11    | 0     | 0.03   |
| AXIOMTEK  | Unknown                | 3      | 28      | 11    | 0     | 0.03   |
| Micron    | MX1/2/300, M5/600, ... | 1      | 1       | 11    | 0     | 0.03   |
| DGM       | Unknown                | 1      | 2       | 79    | 21    | 0.03   |
| Intel     | 540 Series SSDs        | 9      | 40      | 29    | 278   | 0.03   |
| ACOS      | Unknown                | 1      | 2       | 48    | 508   | 0.03   |
| KUU       | Unknown                | 1      | 1       | 10    | 0     | 0.03   |
| DUEX      | Unknown                | 2      | 2       | 538   | 531   | 0.03   |
| Zozt      | Unknown                | 2      | 3       | 9     | 0     | 0.03   |
| Maximus   | Unknown                | 2      | 5       | 9     | 0     | 0.03   |
| VERICO    | Unknown                | 1      | 2       | 8     | 0     | 0.02   |
| BaseTech  | Unknown                | 1      | 1       | 8     | 0     | 0.02   |
| MIXZA     | Unknown                | 1      | 2       | 8     | 0     | 0.02   |
| ATP       | Unknown                | 1      | 1       | 8     | 0     | 0.02   |
| TMI       | Unknown                | 3      | 3       | 8     | 0     | 0.02   |
| FASTDISK  | Unknown                | 6      | 6       | 7     | 0     | 0.02   |
| Digma     | Unknown                | 4      | 6       | 7     | 2     | 0.02   |
| Mach X... | Unknown                | 1      | 1       | 7     | 0     | 0.02   |
| ALLIED    | Unknown                | 1      | 1       | 7     | 0     | 0.02   |
| INDMEM    | Unknown                | 5      | 6       | 7     | 0     | 0.02   |
| 2-Power   | Unknown                | 3      | 4       | 6     | 2     | 0.02   |
| KODAK     | Unknown                | 4      | 4       | 6     | 0     | 0.02   |
| POLION    | Unknown                | 1      | 1       | 6     | 0     | 0.02   |
| geonix    | Unknown                | 1      | 1       | 6     | 0     | 0.02   |
| QNIX      | Unknown                | 1      | 1       | 6     | 0     | 0.02   |
| J.ZAO     | Unknown                | 1      | 1       | 5     | 0     | 0.02   |
| kingch... | Unknown                | 1      | 1       | 5     | 0     | 0.02   |
| BUFFALO   | Unknown                | 1      | 1       | 5     | 0     | 0.02   |
| QIANGHE   | Unknown                | 1      | 1       | 73    | 12    | 0.02   |
| Pear      | Unknown                | 1      | 1       | 5     | 0     | 0.02   |
| Goldenfir | Unknown                | 3      | 3       | 32    | 11    | 0.01   |
| Protectli | Unknown                | 1      | 2       | 4     | 0     | 0.01   |
| ShiJi     | Unknown                | 5      | 7       | 4     | 0     | 0.01   |
| Veno      | Unknown                | 1      | 2       | 4     | 0     | 0.01   |
| Reletech  | Unknown                | 1      | 1       | 4     | 0     | 0.01   |
| UMAX      | Unknown                | 2      | 4       | 4     | 0     | 0.01   |
| ASint     | Unknown                | 1      | 1       | 4     | 0     | 0.01   |
| MicroD... | Unknown                | 1      | 2       | 4     | 0     | 0.01   |
| PHINOCOM  | Unknown                | 1      | 1       | 4     | 0     | 0.01   |
| ROKOT     | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| Pacifi... | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| Seapiy    | Unknown                | 2      | 2       | 3     | 0     | 0.01   |
| Aarvex    | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| ShineDisk | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| IOD       | Unknown                | 1      | 2       | 3     | 0     | 0.01   |
| TurXun    | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| GOKE      | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| Pichau    | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| KOOTION   | Unknown                | 1      | 1       | 2     | 0     | 0.01   |
| Cactus    | Unknown                | 1      | 2       | 2     | 0     | 0.01   |
| SOLIDATA  | Unknown                | 1      | 1       | 2420  | 1019  | 0.01   |
| MaxDig... | Unknown                | 3      | 3       | 16    | 222   | 0.01   |
| VSEVEN    | Unknown                | 1      | 1       | 2     | 0     | 0.01   |
| Philips   | Unknown                | 1      | 1       | 1     | 0     | 0.01   |
| DEPO      | Unknown                | 1      | 2       | 1     | 108   | 0.00   |
| SXMicro   | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| Mcpoint   | Unknown                | 1      | 1       | 6     | 3     | 0.00   |
| Xinhaike  | Unknown                | 1      | 2       | 1     | 0     | 0.00   |
| VICKTER   | Unknown                | 1      | 3       | 1     | 0     | 0.00   |
| SOYO      | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| SATAFIRM  | Unknown                | 1      | 3       | 126   | 88    | 0.00   |
| LEQIXIANG | Unknown                | 1      | 3       | 1     | 2     | 0.00   |
| Emphase   | Unknown                | 1      | 1       | 907   | 1017  | 0.00   |
| Leqixiang | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Maxmemory | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| iODD      | Unknown                | 3      | 4       | 0     | 0     | 0.00   |
| Reeioon   | Unknown                | 1      | 1       | 232   | 377   | 0.00   |
| Gritronix | Unknown                | 1      | 1       | 22    | 37    | 0.00   |
| SSSTC     | Unknown                | 3      | 10      | 33    | 907   | 0.00   |
| POWER X   | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Liren     | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| VNYEZ     | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| T-CREATE  | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| HP Phison | Unknown                | 3      | 4       | 427   | 1034  | 0.00   |
| X-ENERGY  | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Bliksem   | Unknown                | 1      | 1       | 10    | 28    | 0.00   |
| SUNTRSI   | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| DERLAR    | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| MAX SPEED | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Tronos    | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Bamba     | Unknown                | 1      | 1       | 60    | 249   | 0.00   |
| Myung     | Unknown                | 1      | 1       | 228   | 1015  | 0.00   |
| Dahua     | Unknown                | 3      | 3       | 0     | 0     | 0.00   |
| Hitachi   | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| MaiChai   | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| tecmiyo   | Unknown                | 2      | 2       | 7     | 27    | 0.00   |
| Wellco... | Unknown                | 1      | 1       | 13    | 71    | 0.00   |
| Xinsujie  | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| KINGPAN   | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Wintec    | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| SandForce | Unknown                | 1      | 1       | 65    | 1018  | 0.00   |
| DOGGO     | Unknown                | 1      | 2       | 0     | 0     | 0.00   |
| KDATA     | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| TXRUI     | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| EGON      | Unknown                | 1      | 1       | 0     | 11    | 0.00   |
| JIAWEI    | Unknown                | 1      | 1       | 47    | 3057  | 0.00   |
| Zebronics | Unknown                | 1      | 1       | 13    | 1012  | 0.00   |

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
| Espada      | 1      | 1       | 2060  | 0     | 5.65   |
| EXBOM       | 1      | 1       | 1829  | 0     | 5.01   |
| SMART       | 1      | 1       | 1374  | 0     | 3.77   |
| TANCA       | 1      | 1       | 1246  | 0     | 3.42   |
| HPE         | 7      | 7       | 1185  | 0     | 3.25   |
| SK          | 1      | 1       | 1054  | 0     | 2.89   |
| Radeon      | 1      | 4       | 778   | 0     | 2.13   |
| TCSUNB0W    | 1      | 1       | 767   | 0     | 2.10   |
| Micro Ce... | 1      | 1       | 722   | 0     | 1.98   |
| Corsair     | 62     | 324     | 799   | 88    | 1.67   |
| OCZ         | 104    | 836     | 745   | 29    | 1.64   |
| Galaxy      | 1      | 1       | 578   | 0     | 1.58   |
| SATADOM     | 1      | 1       | 574   | 0     | 1.57   |
| SandForce   | 4      | 4       | 621   | 359   | 1.44   |
| MyDigita... | 4      | 13      | 515   | 0     | 1.41   |
| ADROITLARK  | 1      | 1       | 493   | 0     | 1.35   |
| Axiom       | 3      | 3       | 473   | 0     | 1.30   |
| SuperMicro  | 3      | 5       | 467   | 0     | 1.28   |
| Samsung     | 392    | 9675    | 477   | 8     | 1.26   |
| Intel       | 221    | 1343    | 572   | 62    | 1.22   |
| OWC         | 7      | 32      | 481   | 3     | 1.21   |
| Hajaan      | 1      | 2       | 420   | 0     | 1.15   |
| Apple       | 28     | 376     | 417   | 10    | 1.10   |
| Toshiba     | 119    | 624     | 417   | 10    | 1.08   |
| OYUNKEY     | 2      | 3       | 512   | 44    | 1.08   |
| DIERYA      | 1      | 1       | 385   | 0     | 1.06   |
| FCS         | 1      | 1       | 381   | 0     | 1.05   |
| CFD         | 3      | 3       | 375   | 0     | 1.03   |
| KingShare   | 2      | 2       | 373   | 0     | 1.02   |
| Redapple    | 1      | 1       | 363   | 0     | 1.00   |
| addlink     | 2      | 4       | 359   | 0     | 0.98   |
| THU         | 1      | 1       | 339   | 0     | 0.93   |
| Palit       | 8      | 14      | 314   | 0     | 0.86   |
| Aura        | 1      | 1       | 310   | 0     | 0.85   |
| XSTAR       | 2      | 2       | 286   | 0     | 0.78   |
| Kingston    | 224    | 6061    | 316   | 23    | 0.75   |
| SanDisk     | 290    | 3449    | 298   | 27    | 0.74   |
| Mushkin     | 44     | 90      | 363   | 118   | 0.74   |
| ZOTAC       | 3      | 4       | 268   | 0     | 0.74   |
| Exascend    | 1      | 1       | 264   | 0     | 0.73   |
| TAISU       | 2      | 2       | 254   | 0     | 0.70   |
| Micron      | 113    | 712     | 318   | 102   | 0.70   |
| Hoodisk     | 5      | 26      | 245   | 0     | 0.67   |
| Smart       | 3      | 3       | 241   | 0     | 0.66   |
| G.Skill     | 1      | 1       | 241   | 0     | 0.66   |
| GALAX       | 3      | 10      | 238   | 0     | 0.65   |
| Seagate     | 34     | 136     | 270   | 31    | 0.65   |
| Yunhaitian  | 2      | 2       | 236   | 0     | 0.65   |
| Crucial     | 93     | 3866    | 280   | 24    | 0.65   |
| VENO SCORP  | 2      | 2       | 234   | 0     | 0.64   |
| GAMER       | 1      | 1       | 230   | 0     | 0.63   |
| LVCARDS     | 1      | 1       | 229   | 0     | 0.63   |
| BlitzWolf   | 1      | 1       | 225   | 0     | 0.62   |
| ASUS        | 1      | 1       | 221   | 0     | 0.61   |
| BlueRay     | 5      | 5       | 246   | 1     | 0.60   |
| Hyundai     | 7      | 10      | 218   | 0     | 0.60   |
| Smartbuy    | 17     | 201     | 229   | 1     | 0.60   |
| Patriot     | 47     | 461     | 230   | 11    | 0.59   |
| Transcend   | 100    | 540     | 233   | 21    | 0.59   |
| AFOX        | 3      | 5       | 208   | 0     | 0.57   |
| SK hynix    | 85     | 645     | 306   | 95    | 0.57   |
| PNY         | 62     | 495     | 219   | 17    | 0.57   |
| Pioneer     | 7      | 20      | 206   | 0     | 0.57   |
| Innodisk    | 16     | 30      | 249   | 105   | 0.56   |
| Kston       | 3      | 7       | 204   | 0     | 0.56   |
| BIOSTAR     | 3      | 4       | 203   | 0     | 0.56   |
| Quaroni     | 1      | 1       | 201   | 0     | 0.55   |
| SPCC        | 37     | 795     | 240   | 69    | 0.55   |
| JIESHUO     | 1      | 1       | 196   | 0     | 0.54   |
| WDC         | 54     | 2457    | 206   | 5     | 0.54   |
| Goodram     | 42     | 424     | 198   | 1     | 0.53   |
| Gigabyte    | 7      | 72      | 191   | 0     | 0.53   |
| Advantech   | 10     | 11      | 191   | 0     | 0.52   |
| DERLER      | 1      | 1       | 188   | 0     | 0.52   |
| Reeinno     | 2      | 3       | 183   | 0     | 0.50   |
| ADATA       | 128    | 1459    | 222   | 63    | 0.49   |
| DeTech      | 1      | 3       | 179   | 0     | 0.49   |
| Phison      | 33     | 146     | 178   | 1     | 0.49   |
| minisforum  | 2      | 3       | 173   | 0     | 0.48   |
| HP          | 23     | 137     | 184   | 6     | 0.48   |
| Plextor     | 69     | 398     | 188   | 39    | 0.46   |
| Imation     | 2      | 2       | 168   | 0     | 0.46   |
| KingFast    | 13     | 87      | 171   | 36    | 0.46   |
| Best Memory | 1      | 1       | 167   | 0     | 0.46   |
| Team        | 55     | 218     | 180   | 4     | 0.45   |
| Ramaxel     | 5      | 8       | 202   | 1     | 0.45   |
| ExeGate     | 6      | 8       | 162   | 0     | 0.45   |
| Samgporse   | 1      | 1       | 156   | 0     | 0.43   |
| ADTEC       | 1      | 2       | 152   | 0     | 0.42   |
| BRAVEEAGLE  | 3      | 3       | 151   | 0     | 0.41   |
| JASTER      | 1      | 3       | 147   | 0     | 0.40   |
| Union Me... | 1      | 12      | 144   | 0     | 0.40   |
| EAGET       | 2      | 2       | 141   | 0     | 0.39   |
| KingDian    | 28     | 150     | 146   | 60    | 0.38   |
| MENGMI      | 1      | 1       | 139   | 0     | 0.38   |
| WINTEN      | 1      | 1       | 138   | 0     | 0.38   |
| Super Ta... | 7      | 13      | 161   | 1     | 0.37   |
| UNIC2       | 2      | 6       | 135   | 0     | 0.37   |
| MACROVIP    | 1      | 1       | 134   | 0     | 0.37   |
| Maxtor      | 3      | 20      | 132   | 0     | 0.36   |
| Drevo       | 8      | 22      | 286   | 238   | 0.36   |
| China       | 195    | 1149    | 139   | 15    | 0.36   |
| Chiprex     | 1      | 1       | 126   | 0     | 0.35   |
| Londisk     | 4      | 19      | 123   | 0     | 0.34   |
| Hypertec    | 1      | 2       | 371   | 512   | 0.33   |
| Intenso     | 61     | 395     | 129   | 30    | 0.33   |
| Verbatim    | 7      | 37      | 123   | 28    | 0.33   |
| Inland      | 4      | 5       | 119   | 0     | 0.33   |
| TwinMOS     | 3      | 4       | 132   | 1     | 0.33   |
| LDLC        | 14     | 55      | 157   | 10    | 0.32   |
| Apacer      | 31     | 355     | 128   | 17    | 0.32   |
| Gigabyte... | 7      | 88      | 115   | 0     | 0.32   |
| HXY         | 1      | 1       | 115   | 0     | 0.32   |
| TCSUNBOW    | 9      | 26      | 112   | 0     | 0.31   |
| Silicon ... | 3      | 3       | 111   | 0     | 0.31   |
| SFAS        | 1      | 1       | 111   | 0     | 0.31   |
| Silicon     | 6      | 8       | 111   | 0     | 0.30   |
| SuperSSpeed | 1      | 1       | 110   | 0     | 0.30   |
| Vaseky      | 20     | 32      | 113   | 4     | 0.30   |
| BAITITON    | 10     | 15      | 142   | 3     | 0.30   |
| Kingmax     | 5      | 68      | 243   | 310   | 0.30   |
| AirDisk     | 1      | 3       | 108   | 0     | 0.30   |
| ZTC         | 3      | 6       | 108   | 0     | 0.30   |
| TREKSTOR    | 1      | 1       | 105   | 0     | 0.29   |
| MARVELL     | 1      | 1       | 105   | 0     | 0.29   |
| GLOWAY      | 13     | 21      | 117   | 67    | 0.29   |
| tigo        | 4      | 5       | 103   | 0     | 0.28   |
| e2e4        | 4      | 9       | 103   | 0     | 0.28   |
| Colorful    | 9      | 21      | 136   | 68    | 0.28   |
| GeIL        | 12     | 16      | 117   | 64    | 0.28   |
| T-FORCE     | 5      | 31      | 101   | 1     | 0.28   |
| JAMESDONKEY | 3      | 3       | 99    | 0     | 0.27   |
| KingSpec    | 52     | 267     | 120   | 35    | 0.27   |
| Fujitsu     | 6      | 6       | 98    | 0     | 0.27   |
| TrekStor    | 3      | 4       | 127   | 39    | 0.27   |
| Lexar       | 12     | 116     | 97    | 1     | 0.27   |
| AMD         | 16     | 143     | 114   | 14    | 0.26   |
| RZX         | 2      | 3       | 96    | 0     | 0.26   |
| Biostar     | 6      | 8       | 96    | 0     | 0.26   |
| EZCOOL      | 2      | 2       | 95    | 0     | 0.26   |
| GOWE        | 1      | 1       | 284   | 2     | 0.26   |
| VisionTek   | 1      | 2       | 88    | 0     | 0.24   |
| AXIOM       | 1      | 1       | 87    | 0     | 0.24   |
| LuminouTek  | 5      | 5       | 87    | 0     | 0.24   |
| ShanDianZhe | 3      | 9       | 87    | 0     | 0.24   |
| Lite-On     | 136    | 503     | 110   | 118   | 0.24   |
| AGI         | 6      | 8       | 92    | 5     | 0.24   |
| Integral    | 4      | 17      | 85    | 0     | 0.23   |
| Ramsta      | 6      | 6       | 92    | 169   | 0.23   |
| Lenovo      | 8      | 14      | 108   | 1     | 0.23   |
| Zheino      | 24     | 42      | 100   | 1     | 0.23   |
| SMI         | 8      | 8       | 82    | 245   | 0.23   |
| BIWIN       | 7      | 29      | 94    | 107   | 0.23   |
| BHT         | 9      | 29      | 82    | 0     | 0.23   |
| Nfortec     | 1      | 1       | 82    | 0     | 0.22   |
| XUM         | 2      | 3       | 81    | 0     | 0.22   |
| ASENNO      | 3      | 6       | 140   | 4     | 0.22   |
| GS Nanotech | 4      | 5       | 77    | 0     | 0.21   |
| INNOVATI... | 14     | 35      | 79    | 1     | 0.21   |
| SPEED UP    | 1      | 1       | 75    | 0     | 0.21   |
| Wdstars     | 2      | 2       | 71    | 0     | 0.20   |
| Varro       | 3      | 3       | 71    | 0     | 0.19   |
| V-GeN       | 14     | 16      | 69    | 0     | 0.19   |
| Indilinx    | 8      | 10      | 71    | 2     | 0.19   |
| Neo Forza   | 6      | 10      | 126   | 520   | 0.19   |
| Dogfish     | 11     | 56      | 72    | 1     | 0.19   |
| ViperTeq    | 1      | 1       | 68    | 0     | 0.19   |
| Gost        | 2      | 2       | 68    | 0     | 0.19   |
| Hikvision   | 22     | 69      | 71    | 1     | 0.18   |
| TAMMUZ      | 4      | 4       | 66    | 0     | 0.18   |
| KLONER      | 1      | 1       | 66    | 0     | 0.18   |
| FORESEE     | 10     | 65      | 65    | 0     | 0.18   |
| Kingchuxing | 8      | 15      | 65    | 0     | 0.18   |
| HGST        | 1      | 2       | 65    | 0     | 0.18   |
| Foxline     | 13     | 29      | 96    | 36    | 0.17   |
| Golden m... | 4      | 4       | 62    | 0     | 0.17   |
| SUNEAST     | 6      | 8       | 120   | 22    | 0.17   |
| Leven       | 11     | 48      | 70    | 2     | 0.17   |
| Platinet    | 1      | 3       | 61    | 30    | 0.17   |
| Timetec     | 5      | 6       | 60    | 0     | 0.17   |
| Blackpcs    | 3      | 3       | 60    | 0     | 0.17   |
| TEKET       | 1      | 2       | 59    | 0     | 0.16   |
| ORICO       | 5      | 5       | 94    | 1     | 0.16   |
| EYOTA       | 1      | 1       | 58    | 0     | 0.16   |
| ASMedia     | 1      | 4       | 55    | 0     | 0.15   |
| EMTEC       | 6      | 31      | 55    | 0     | 0.15   |
| VISIPRO     | 3      | 5       | 56    | 3     | 0.15   |
| Aoluska     | 1      | 1       | 54    | 0     | 0.15   |
| PUSKILL     | 3      | 3       | 53    | 0     | 0.15   |
| Teutons     | 2      | 2       | 53    | 0     | 0.15   |
| KINGBANK    | 2      | 7       | 53    | 0     | 0.15   |
| IPLEX       | 1      | 1       | 52    | 0     | 0.14   |
| JUHOR       | 1      | 1       | 52    | 0     | 0.14   |
| HEORIADY    | 3      | 4       | 49    | 0     | 0.14   |
| JD          | 2      | 2       | 169   | 53    | 0.14   |
| Qumo        | 5      | 10      | 169   | 204   | 0.14   |
| Greenliant  | 1      | 1       | 49    | 0     | 0.13   |
| Anobit      | 1      | 2       | 48    | 1     | 0.13   |
| Avant       | 3      | 4       | 432   | 254   | 0.13   |
| Win Memory  | 3      | 5       | 48    | 0     | 0.13   |
| XrayDisk    | 11     | 58      | 54    | 37    | 0.13   |
| Kross El... | 2      | 3       | 47    | 0     | 0.13   |
| XPG         | 1      | 3       | 46    | 0     | 0.13   |
| S3+         | 7      | 9       | 91    | 6     | 0.13   |
| RCESSD      | 1      | 2       | 46    | 0     | 0.13   |
| Fanxiang    | 6      | 7       | 46    | 0     | 0.13   |
| LENSEN      | 1      | 1       | 46    | 0     | 0.13   |
| KLEVV       | 4      | 5       | 45    | 0     | 0.13   |
| MARSHAL     | 1      | 1       | 44    | 0     | 0.12   |
| Netac       | 31     | 236     | 50    | 15    | 0.12   |
| FATTYDOVE   | 1      | 1       | 44    | 0     | 0.12   |
| PRETEC      | 1      | 1       | 44    | 0     | 0.12   |
| ORIGIN I... | 1      | 1       | 43    | 0     | 0.12   |
| Acer        | 3      | 8       | 41    | 0     | 0.11   |
| GSemi       | 1      | 2       | 41    | 0     | 0.11   |
| Fordisk     | 2      | 2       | 41    | 0     | 0.11   |
| Faspeed     | 15     | 16      | 43    | 1     | 0.11   |
| Dogeish     | 1      | 1       | 40    | 0     | 0.11   |
| Solid       | 3      | 6       | 42    | 1     | 0.11   |
| QUMO        | 12     | 19      | 52    | 2     | 0.11   |
| MediaRange  | 1      | 1       | 39    | 0     | 0.11   |
| Goldkey     | 2      | 2       | 39    | 0     | 0.11   |
| Star Drive  | 3      | 6       | 38    | 0     | 0.11   |
| Kingrich    | 6      | 7       | 121   | 2     | 0.10   |
| Yeyian      | 3      | 5       | 37    | 0     | 0.10   |
| KIOXIA-E... | 3      | 42      | 36    | 0     | 0.10   |
| TOPMORE     | 1      | 1       | 36    | 0     | 0.10   |
| NTC         | 1      | 1       | 35    | 0     | 0.10   |
| Hanye       | 1      | 1       | 35    | 0     | 0.10   |
| TakeMS      | 1      | 1       | 34    | 0     | 0.10   |
| RESCUE      | 1      | 1       | 34    | 0     | 0.10   |
| RX7         | 3      | 3       | 36    | 4     | 0.10   |
| ANACOMDA    | 2      | 2       | 34    | 0     | 0.09   |
| SemsoTai    | 2      | 2       | 37    | 5     | 0.09   |
| Gateway     | 2      | 4       | 33    | 0     | 0.09   |
| AEGO        | 1      | 3       | 33    | 0     | 0.09   |
| ORTIAL      | 3      | 11      | 30    | 0     | 0.08   |
| KingPower   | 1      | 1       | 29    | 0     | 0.08   |
| TEXTORM     | 4      | 8       | 30    | 5     | 0.08   |
| ACPI        | 3      | 3       | 29    | 0     | 0.08   |
| OSCOO       | 5      | 5       | 30    | 18    | 0.08   |
| Silicon ... | 2      | 2       | 27    | 0     | 0.08   |
| Tammuz      | 1      | 1       | 27    | 0     | 0.08   |
| SenDisk     | 1      | 1       | 27    | 0     | 0.08   |
| i-FlashDisk | 2      | 2       | 27    | 0     | 0.07   |
| HECTRON     | 1      | 1       | 26    | 0     | 0.07   |
| Teclast     | 18     | 41      | 36    | 26    | 0.07   |
| Rogueware   | 2      | 2       | 25    | 0     | 0.07   |
| Pasoul      | 1      | 1       | 25    | 0     | 0.07   |
| Wdxsky      | 1      | 1       | 25    | 0     | 0.07   |
| MidasForce  | 4      | 9       | 25    | 0     | 0.07   |
| Eluktro     | 2      | 2       | 428   | 508   | 0.07   |
| KeepData    | 2      | 4       | 24    | 0     | 0.07   |
| KLLISRE     | 3      | 3       | 24    | 0     | 0.07   |
| Wibtek      | 3      | 10      | 23    | 11    | 0.07   |
| SNR         | 1      | 1       | 23    | 0     | 0.07   |
| SCY         | 2      | 3       | 23    | 0     | 0.06   |
| Supersonic  | 2      | 2       | 23    | 0     | 0.06   |
| WALRAM      | 5      | 17      | 25    | 6     | 0.06   |
| RECADATA    | 2      | 2       | 23    | 0     | 0.06   |
| ZHITAI      | 3      | 5       | 21    | 0     | 0.06   |
| ELSKY       | 1      | 1       | 21    | 0     | 0.06   |
| Valuetech   | 2      | 2       | 21    | 0     | 0.06   |
| GHIA        | 1      | 1       | 20    | 0     | 0.06   |
| Dell        | 3      | 9       | 20    | 0     | 0.06   |
| XUNZHE      | 1      | 1       | 20    | 0     | 0.05   |
| Force Le    | 1      | 1       | 19    | 0     | 0.05   |
| JUMPER      | 1      | 2       | 19    | 0     | 0.05   |
| Kimtigo     | 1      | 4       | 18    | 0     | 0.05   |
| Hyperdisk   | 1      | 1       | 18    | 0     | 0.05   |
| UMIS        | 1      | 1       | 18    | 0     | 0.05   |
| Yeestor     | 1      | 1       | 17    | 0     | 0.05   |
| Kingspeed   | 2      | 2       | 17    | 0     | 0.05   |
| LDNDISK     | 1      | 1       | 16    | 0     | 0.05   |
| Goldendisk  | 1      | 1       | 16    | 0     | 0.04   |
| MOVESPEED   | 1      | 1       | 15    | 0     | 0.04   |
| RevuAhn     | 1      | 1       | 14    | 0     | 0.04   |
| NFORCE      | 1      | 1       | 14    | 0     | 0.04   |
| BR          | 5      | 5       | 14    | 0     | 0.04   |
| ADLINK      | 1      | 1       | 13    | 0     | 0.04   |
| Origin I... | 1      | 1       | 171   | 12    | 0.04   |
| SomnAmbu... | 1      | 1       | 25    | 1     | 0.04   |
| Getrich     | 1      | 1       | 12    | 0     | 0.04   |
| RAMOS       | 2      | 2       | 12    | 0     | 0.04   |
| KUIJIA      | 1      | 1       | 12    | 0     | 0.03   |
| EVM         | 1      | 2       | 12    | 0     | 0.03   |
| Azerty      | 2      | 3       | 12    | 0     | 0.03   |
| Wicgtyp     | 1      | 1       | 12    | 0     | 0.03   |
| Gigastone   | 2      | 2       | 12    | 0     | 0.03   |
| Microtech   | 2      | 2       | 11    | 0     | 0.03   |
| AXIOMTEK    | 3      | 28      | 11    | 0     | 0.03   |
| DGM         | 1      | 2       | 79    | 21    | 0.03   |
| ACOS        | 1      | 2       | 48    | 508   | 0.03   |
| KUU         | 1      | 1       | 10    | 0     | 0.03   |
| DUEX        | 2      | 2       | 538   | 531   | 0.03   |
| Zozt        | 2      | 3       | 9     | 0     | 0.03   |
| Maximus     | 2      | 5       | 9     | 0     | 0.03   |
| VERICO      | 1      | 2       | 8     | 0     | 0.02   |
| BaseTech    | 1      | 1       | 8     | 0     | 0.02   |
| MIXZA       | 1      | 2       | 8     | 0     | 0.02   |
| ATP         | 1      | 1       | 8     | 0     | 0.02   |
| TMI         | 3      | 3       | 8     | 0     | 0.02   |
| FASTDISK    | 6      | 6       | 7     | 0     | 0.02   |
| Digma       | 4      | 6       | 7     | 2     | 0.02   |
| Mach Xtreme | 1      | 1       | 7     | 0     | 0.02   |
| ALLIED      | 1      | 1       | 7     | 0     | 0.02   |
| INDMEM      | 5      | 6       | 7     | 0     | 0.02   |
| 2-Power     | 3      | 4       | 6     | 2     | 0.02   |
| KODAK       | 4      | 4       | 6     | 0     | 0.02   |
| POLION      | 1      | 1       | 6     | 0     | 0.02   |
| geonix      | 1      | 1       | 6     | 0     | 0.02   |
| QNIX        | 1      | 1       | 6     | 0     | 0.02   |
| J.ZAO       | 1      | 1       | 5     | 0     | 0.02   |
| kingchuxing | 1      | 1       | 5     | 0     | 0.02   |
| BUFFALO     | 1      | 1       | 5     | 0     | 0.02   |
| QIANGHE     | 1      | 1       | 73    | 12    | 0.02   |
| Pear        | 1      | 1       | 5     | 0     | 0.02   |
| Goldenfir   | 3      | 3       | 32    | 11    | 0.01   |
| Protectli   | 1      | 2       | 4     | 0     | 0.01   |
| ShiJi       | 5      | 7       | 4     | 0     | 0.01   |
| Veno        | 1      | 2       | 4     | 0     | 0.01   |
| Reletech    | 1      | 1       | 4     | 0     | 0.01   |
| UMAX        | 2      | 4       | 4     | 0     | 0.01   |
| ASint       | 1      | 1       | 4     | 0     | 0.01   |
| MicroDream  | 1      | 2       | 4     | 0     | 0.01   |
| PHINOCOM    | 1      | 1       | 4     | 0     | 0.01   |
| ROKOT       | 1      | 1       | 3     | 0     | 0.01   |
| Pacific Sun | 1      | 1       | 3     | 0     | 0.01   |
| Seapiy      | 2      | 2       | 3     | 0     | 0.01   |
| Aarvex      | 1      | 1       | 3     | 0     | 0.01   |
| ShineDisk   | 1      | 1       | 3     | 0     | 0.01   |
| IOD         | 1      | 2       | 3     | 0     | 0.01   |
| TurXun      | 1      | 1       | 3     | 0     | 0.01   |
| GOKE        | 1      | 1       | 3     | 0     | 0.01   |
| Pichau      | 1      | 1       | 3     | 0     | 0.01   |
| KOOTION     | 1      | 1       | 2     | 0     | 0.01   |
| Cactus      | 1      | 2       | 2     | 0     | 0.01   |
| SOLIDATA    | 1      | 1       | 2420  | 1019  | 0.01   |
| MaxDigital  | 3      | 3       | 16    | 222   | 0.01   |
| VSEVEN      | 1      | 1       | 2     | 0     | 0.01   |
| Philips     | 1      | 1       | 1     | 0     | 0.01   |
| DEPO        | 1      | 2       | 1     | 108   | 0.00   |
| SXMicro     | 1      | 1       | 1     | 0     | 0.00   |
| Mcpoint     | 1      | 1       | 6     | 3     | 0.00   |
| Xinhaike    | 1      | 2       | 1     | 0     | 0.00   |
| VICKTER     | 1      | 3       | 1     | 0     | 0.00   |
| SOYO        | 1      | 1       | 1     | 0     | 0.00   |
| SATAFIRM    | 1      | 3       | 126   | 88    | 0.00   |
| LEQIXIANG   | 1      | 3       | 1     | 2     | 0.00   |
| Emphase     | 1      | 1       | 907   | 1017  | 0.00   |
| Leqixiang   | 1      | 1       | 0     | 0     | 0.00   |
| Maxmemory   | 1      | 1       | 0     | 0     | 0.00   |
| iODD        | 3      | 4       | 0     | 0     | 0.00   |
| Reeioon     | 1      | 1       | 232   | 377   | 0.00   |
| Gritronix   | 1      | 1       | 22    | 37    | 0.00   |
| SSSTC       | 3      | 10      | 33    | 907   | 0.00   |
| POWER X     | 1      | 1       | 0     | 0     | 0.00   |
| Liren       | 1      | 1       | 0     | 0     | 0.00   |
| VNYEZ       | 1      | 1       | 0     | 0     | 0.00   |
| T-CREATE    | 1      | 1       | 0     | 0     | 0.00   |
| HP Phison   | 3      | 4       | 427   | 1034  | 0.00   |
| X-ENERGY    | 1      | 1       | 0     | 0     | 0.00   |
| Bliksem     | 1      | 1       | 10    | 28    | 0.00   |
| SUNTRSI     | 1      | 1       | 0     | 0     | 0.00   |
| DERLAR      | 1      | 1       | 0     | 0     | 0.00   |
| MAX SPEED   | 1      | 1       | 0     | 0     | 0.00   |
| Tronos      | 1      | 1       | 0     | 0     | 0.00   |
| Bamba       | 1      | 1       | 60    | 249   | 0.00   |
| Myung       | 1      | 1       | 228   | 1015  | 0.00   |
| Dahua       | 3      | 3       | 0     | 0     | 0.00   |
| Hitachi     | 1      | 1       | 0     | 0     | 0.00   |
| MaiChai     | 1      | 1       | 0     | 0     | 0.00   |
| tecmiyo     | 2      | 2       | 7     | 27    | 0.00   |
| Wellcomm... | 1      | 1       | 13    | 71    | 0.00   |
| Xinsujie    | 1      | 1       | 0     | 0     | 0.00   |
| KINGPAN     | 1      | 1       | 0     | 0     | 0.00   |
| Wintec      | 1      | 1       | 0     | 0     | 0.00   |
| DOGGO       | 1      | 2       | 0     | 0     | 0.00   |
| KDATA       | 1      | 1       | 0     | 0     | 0.00   |
| TXRUI       | 1      | 1       | 0     | 0     | 0.00   |
| EGON        | 1      | 1       | 0     | 11    | 0.00   |
| JIAWEI      | 1      | 1       | 47    | 3057  | 0.00   |
| Zebronics   | 1      | 1       | 13    | 1012  | 0.00   |

NVME by Model
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

See full list of tested NVMe samples in the Appendix 5 ([All_NVMe.md](/All_NVMe.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| Intel     | H10 HBRPEKNX010... | 16 GB  | 1       | 7082  | 0     | 19.40  |
| Intel     | H20 HBRPEKNL020... | 32 GB  | 1       | 6705  | 0     | 18.37  |
| Intel     | MEMPEK1J016GAD     | 16 GB  | 2       | 5999  | 0     | 16.44  |
| Intel     | H10 HBRPEKNX020... | 32 GB  | 15      | 3084  | 0     | 8.45   |
| Intel     | MT1600KEXUV        | 1.6 TB | 1       | 1720  | 0     | 4.71   |
| Samsung   | MZVLV512HCJH-00000 | 512 GB | 1       | 1710  | 0     | 4.69   |
| Intel     | SSDPEDMW800G4      | 800 GB | 1       | 1691  | 0     | 4.64   |
| Intel     | H10 HBRPEKNX020... | 32 GB  | 2       | 1574  | 0     | 4.31   |
| Intel     | SSDPEDMW400G4      | 400 GB | 7       | 1467  | 0     | 4.02   |
| Samsung   | MZVLV256HCHP-000L1 | 256 GB | 1       | 1400  | 0     | 3.84   |
| Intel     | SSDPEDMD400G4      | 400 GB | 4       | 1389  | 0     | 3.81   |
| Intel     | SSDPEDMW012T4      | 1.2 TB | 4       | 1343  | 0     | 3.68   |
| Intel     | SSDPE7KX020T7      | 2 TB   | 1       | 1218  | 0     | 3.34   |
| Intel     | SSDPEKKR128G7      | 128 GB | 1       | 1175  | 0     | 3.22   |
| Samsung   | SSD 950 PRO        | 256 GB | 21      | 1083  | 0     | 2.97   |
| Intel     | SSDPEKKF256G7H     | 256 GB | 24      | 1086  | 43    | 2.93   |
| Lite-On   | CL1-8D128-HP       | 128 GB | 1       | 1063  | 0     | 2.91   |
| Toshiba   | THNSN5512GPU7 NVMe | 512 GB | 5       | 1037  | 0     | 2.84   |
| Toshiba   | KXG50PNV1T02 NVMe  | 1 TB   | 5       | 978   | 0     | 2.68   |
| ZOTAC     | ZTSSDPG3-480G-GE   | 480 GB | 2       | 919   | 0     | 2.52   |
| SanDisk   | A400 NVMe          | 256 GB | 2       | 917   | 0     | 2.51   |
| Intel     | SSDPEDME016T4      | 1.6 TB | 1       | 906   | 0     | 2.48   |
| Avant     | 500GB M.2 NVME     | 500 GB | 1       | 891   | 0     | 2.44   |
| Corsair   | Force MP500        | 480 GB | 1       | 869   | 0     | 2.38   |
| Toshiba   | RD400              | 1 TB   | 3       | 855   | 0     | 2.34   |
| Toshiba   | RD400              | 256 GB | 4       | 854   | 0     | 2.34   |
| Samsung   | SSD 983 DCT 1.92TB | 1.9 TB | 2       | 850   | 0     | 2.33   |
| ADATA     | SX8000NP           | 256 GB | 1       | 815   | 0     | 2.23   |
| Silico... | 128GB SSD          | 128 GB | 1       | 792   | 0     | 2.17   |
| Intel     | SSDPE7KX010T7      | 1 TB   | 1       | 791   | 0     | 2.17   |
| Kingston  | SKC1000240G        | 240 GB | 3       | 776   | 0     | 2.13   |
| Samsung   | SSD 950 PRO        | 512 GB | 44      | 776   | 0     | 2.13   |
| Intel     | SSDPEKKW512G7      | 512 GB | 24      | 912   | 107   | 2.08   |
| Intel     | SSDPEKKF512G7H     | 512 GB | 5       | 754   | 0     | 2.07   |
| Samsung   | MZVLB1T0HALR-000H2 | 1 TB   | 3       | 751   | 0     | 2.06   |
| Transcend | TS128GMTE850       | 128 GB | 1       | 745   | 0     | 2.04   |
| WDC       | WDS512G1X0C-00ENX0 | 512 GB | 14      | 714   | 0     | 1.96   |
| Intel     | SSDPE21K375GA      | 375 GB | 1       | 696   | 0     | 1.91   |
| ADATA     | SX8000NP           | 128 GB | 2       | 680   | 0     | 1.86   |
| Samsung   | MZWLL1T6HAJQ-00005 | 1.6 TB | 4       | 673   | 0     | 1.85   |
| SPCC      | M.2 PCIe SSD       | 500 GB | 1       | 670   | 0     | 1.84   |
| Kingston  | RBUSNS8154P3102... | 1 TB   | 2       | 667   | 0     | 1.83   |
| Samsung   | MZVPV256HDGL-00000 | 256 GB | 15      | 667   | 0     | 1.83   |
| Samsung   | MZVPV256HDGL-000H1 | 256 GB | 7       | 661   | 0     | 1.81   |
| Corsair   | Force MP500        | 120 GB | 12      | 659   | 0     | 1.81   |
| Intel     | SSDPE2MX450G7      | 450 GB | 4       | 658   | 0     | 1.80   |
| Corsair   | Force MP500        | 240 GB | 11      | 750   | 2     | 1.80   |
| Intel     | SSDPEKKW256G7      | 256 GB | 63      | 826   | 32    | 1.80   |
| Toshiba   | KXG50PNV2T04 NVMe  | 2 TB   | 4       | 653   | 0     | 1.79   |
| Hikvision | HS-SSD-E2000 2048G | 2 TB   | 1       | 652   | 0     | 1.79   |
| Silico... | Asgard AN3 2TNV... | 2 TB   | 14      | 652   | 0     | 1.79   |
| Samsung   | MZWLL3T2HMJP-00003 | 3.2 TB | 1       | 648   | 0     | 1.78   |
| Micron    | MTFDHAL3T2MCE-1... | 3.2 TB | 1       | 645   | 0     | 1.77   |
| Intel     | SSDPE21D480GA      | 480 GB | 6       | 643   | 0     | 1.76   |
| Lenovo    | X800 NVMe M.2 2... | 512 GB | 1       | 637   | 0     | 1.75   |
| Samsung   | MZVPV512HDGL-00000 | 512 GB | 10      | 631   | 0     | 1.73   |
| Samsung   | MZQLB960HAJR-00007 | 960 GB | 10      | 624   | 0     | 1.71   |
| Intel     | SSDPEKKW010T7      | 1 TB   | 5       | 1095  | 6     | 1.71   |
| Intel     | SSDPEKKF256G7L     | 256 GB | 29      | 737   | 42    | 1.70   |
| Toshiba   | KBG20ZMS256G NVMe  | 256 GB | 2       | 605   | 0     | 1.66   |
| Intel     | SSDPED1K375GA      | 375 GB | 1       | 603   | 0     | 1.65   |
| Gigabyte  | GP-ASM2NE2512GTTDR | 512 GB | 1       | 603   | 0     | 1.65   |
| WDC       | WUS3BA176C7P3E3    | 7.6 TB | 1       | 589   | 0     | 1.62   |
| Intel     | SSDPEKKW128G7      | 128 GB | 13      | 972   | 2     | 1.61   |
| Samsung   | MZQLB960HAJR-00003 | 960 GB | 4       | 588   | 0     | 1.61   |
| Toshiba   | THNSN5256GPU7      | 256 GB | 15      | 582   | 0     | 1.59   |
| Phison    | APS-SE20G-256      | 256 GB | 2       | 580   | 0     | 1.59   |
| Intel     | SSDPEKKF360G7H     | 360 GB | 7       | 572   | 0     | 1.57   |
| Phison    | APS-SE20Q-1T       | 1 TB   | 1       | 565   | 0     | 1.55   |
| Toshiba   | THNSN5512GPUK      | 512 GB | 1       | 563   | 0     | 1.54   |
| Toshiba   | KXG50PNV2T04 1.6TB | 1.6 TB | 1       | 553   | 0     | 1.52   |
| Intel     | SSDPEDMW012T4D ... | 1.2 TB | 1       | 552   | 0     | 1.51   |
| Intel     | SSDPED1D280GA      | 280 GB | 5       | 536   | 0     | 1.47   |
| Toshiba   | RD400              | 128 GB | 1       | 536   | 0     | 1.47   |
| Samsung   | MZQLB7T6HMLA-00007 | 7.6 TB | 1       | 533   | 0     | 1.46   |
| Samsung   | MZPLL1T6HAJQ-00005 | 1.6 TB | 1       | 527   | 0     | 1.45   |
| Toshiba   | KXG50ZNV1T02       | 1 TB   | 4       | 524   | 0     | 1.44   |
| Toshiba   | THNSN5512GPUK NVMe | 512 GB | 36      | 522   | 0     | 1.43   |
| Hikvision | HS-SSD-E2000 512G  | 512 GB | 2       | 522   | 0     | 1.43   |
| Toshiba   | THNSN5256GPUK NVMe | 256 GB | 19      | 521   | 0     | 1.43   |
| Gigabyte  | GP-AG42TB          | 2 TB   | 1       | 516   | 0     | 1.41   |
| Samsung   | MZVPV512HDGL-000H1 | 512 GB | 4       | 515   | 0     | 1.41   |
| Plextor   | PX-512M9PeG        | 512 GB | 4       | 512   | 0     | 1.40   |
| Intel     | SSDPEL1C100GA      | 100 GB | 1       | 498   | 0     | 1.37   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 2       | 495   | 0     | 1.36   |
| Samsung   | PM951 NVMe         | 512 GB | 11      | 488   | 0     | 1.34   |
| Toshiba   | THNSN51T02DUK NVMe | 1 TB   | 12      | 483   | 0     | 1.33   |
| WDC       | WDBGMP5000ANC-WRSN | 500 GB | 1       | 483   | 0     | 1.32   |
| Intel     | MEMPEK1W032GA      | 32 GB  | 6       | 479   | 0     | 1.31   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 1       | 473   | 0     | 1.30   |
| Samsung   | MZVLV128HCGR-00000 | 128 GB | 4       | 466   | 0     | 1.28   |
| Kingston  | SEDC1000BM8960G    | 960 GB | 2       | 466   | 0     | 1.28   |
| Toshiba   | KXG50ZNV512G NVMe  | 512 GB | 63      | 460   | 0     | 1.26   |
| Kingston  | SKC1000480G        | 480 GB | 4       | 456   | 0     | 1.25   |
| Toshiba   | KXG60PNV512G NVMe  | 512 GB | 1       | 454   | 0     | 1.25   |
| Mushkin   | MKNSSDHL250GB-D8   | 250 GB | 5       | 467   | 202   | 1.22   |
| Samsung   | MZVPV128HDGM-00000 | 128 GB | 11      | 443   | 0     | 1.22   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 3       | 443   | 0     | 1.21   |
| Phison    | Neutron NX500      | 800 GB | 2       | 442   | 0     | 1.21   |
| Corsair   | Force MP300        | 480 GB | 2       | 442   | 0     | 1.21   |
| Samsung   | PM951 NVMe         | 1 TB   | 4       | 440   | 0     | 1.21   |
| Kingston  | SKC2000M8250G      | 250 GB | 5       | 437   | 0     | 1.20   |
| ADATA     | SX8200NP           | 480 GB | 10      | 436   | 0     | 1.20   |
| Samsung   | MZVKV512HAJH-000L1 | 512 GB | 12      | 435   | 0     | 1.19   |
| Corsair   | Force MP500        | 960 GB | 1       | 424   | 0     | 1.16   |
| Team      | TM8FP2240G         | 240 GB | 1       | 424   | 0     | 1.16   |
| Toshiba   | THNSF5512GPUK N... | 512 GB | 1       | 417   | 0     | 1.14   |
| Samsung   | MS1PC2DD3ORA3.2T   | 3.2 TB | 1       | 416   | 0     | 1.14   |
| Toshiba   | THNSF5256GPUK      | 256 GB | 9       | 412   | 0     | 1.13   |
| KIOXIA    | KXG60PNV1T02 NVMe  | 1 TB   | 4       | 412   | 0     | 1.13   |
| Toshiba   | KXG5AZNV256G NV... | 256 GB | 2       | 412   | 0     | 1.13   |
| Smartbuy  | m.2 PS5013-2280T   | 512 GB | 1       | 408   | 0     | 1.12   |
| Reletech  | P400 M.2 Pro Q2... | 2 TB   | 1       | 408   | 0     | 1.12   |
| HP        | SSD EX920          | 512 GB | 16      | 408   | 0     | 1.12   |
| WDC       | CL SN720 SDAQNT... | 512 GB | 2       | 404   | 0     | 1.11   |
| Lite-On   | CAZ-82512-Q11 NVMe | 512 GB | 1       | 400   | 0     | 1.10   |
| Patriot   | Hellfire M2        | 240 GB | 3       | 400   | 0     | 1.10   |
| Intel     | HBRPEKNX0202ACO    | 32 GB  | 2       | 398   | 0     | 1.09   |
| Toshiba   | KXG50ZNV256G NVMe  | 256 GB | 40      | 397   | 0     | 1.09   |
| Toshiba   | KXG50ZNV1T02 NVMe  | 1 TB   | 25      | 396   | 0     | 1.09   |
| ADATA     | SX6000NP           | 256 GB | 3       | 394   | 0     | 1.08   |
| ADATA     | SX8000NP           | 512 GB | 1       | 392   | 0     | 1.07   |
| Intel     | SSDPEKKF128G7      | 128 GB | 1       | 778   | 1     | 1.07   |
| Samsung   | PM951 NVMe         | 256 GB | 17      | 388   | 0     | 1.07   |
| Intel     | SSDPED1D480GA      | 480 GB | 3       | 387   | 0     | 1.06   |
| Toshiba   | THNSN5512GPU7      | 512 GB | 9       | 385   | 0     | 1.06   |
| Lexar     | SSD                | 256 GB | 6       | 379   | 0     | 1.04   |
| SanDisk   | A400 NVMe          | 512 GB | 3       | 370   | 0     | 1.01   |
| Gigaby... | GP-ASACNE2100TTTDR | 1 TB   | 1       | 367   | 0     | 1.01   |
| Plextor   | PX-512M8PeGN       | 512 GB | 1       | 362   | 0     | 0.99   |
| Samsung   | MZVLV512HCJH-000L2 | 512 GB | 1       | 361   | 0     | 0.99   |
| Intel     | SSDPE2MX012T7      | 1.2 TB | 4       | 358   | 0     | 0.98   |
| Intel     | HBRPEKNX0202AC     | 512 GB | 2       | 357   | 0     | 0.98   |
| Phison    | Asura NVME         | 2 TB   | 1       | 353   | 0     | 0.97   |
| WDC       | WDS200T3XHC-00SJG0 | 2 TB   | 4       | 353   | 0     | 0.97   |
| Reletech  | P400 M.2 Pro Q1... | 1 TB   | 1       | 353   | 0     | 0.97   |
| Team      | TM8FP6002T         | 2 TB   | 3       | 353   | 0     | 0.97   |
| Intel     | MEMPEK1J016GA      | 16 GB  | 13      | 370   | 78    | 0.95   |
| SK hynix  | PC300 NVMe         | 512 GB | 8       | 348   | 0     | 0.95   |
| ADATA     | SX7000NP           | 128 GB | 3       | 554   | 39    | 0.95   |
| Intel     | SSDPEKKF010T8      | 1 TB   | 6       | 347   | 0     | 0.95   |
| Samsung   | MZ1LV960HCJH-000MU | 960 GB | 1       | 346   | 0     | 0.95   |
| Toshiba   | KXG5AZNV256G       | 256 GB | 15      | 345   | 0     | 0.95   |
| Toshiba   | RD400              | 512 GB | 4       | 344   | 0     | 0.94   |
| Silico... | NVME SSD           | 1 TB   | 3       | 343   | 0     | 0.94   |
| Intel     | SSDPEK1W120GA      | 118 GB | 2       | 341   | 0     | 0.94   |
| Toshiba   | THNSN5512GPUK      | 512 GB | 11      | 341   | 0     | 0.93   |
| addlink   | M.2 PCIE G3x4 NVMe | 1 TB   | 16      | 340   | 0     | 0.93   |
| Samsung   | MZVLV256HCHP-000L2 | 256 GB | 9       | 340   | 0     | 0.93   |
| Aura      | Pro X2             | 960 GB | 4       | 339   | 0     | 0.93   |
| Toshiba   | THNSF5512GPUK      | 512 GB | 12      | 336   | 0     | 0.92   |
| Plextor   | PX-256M8PeGN       | 256 GB | 4       | 336   | 0     | 0.92   |
| Plextor   | PX-1TM9PG +        | 1 TB   | 1       | 335   | 0     | 0.92   |
| Micron    | 9300_MTFDHAL15T... | 15.... | 3       | 333   | 0     | 0.91   |
| WDC       | WDS100T2X0C-00L350 | 1 TB   | 11      | 333   | 0     | 0.91   |
| WDC       | WDS500G2X0C-00L350 | 500 GB | 26      | 332   | 0     | 0.91   |
| WDC       | WDS256G1X0C-00ENX0 | 256 GB | 14      | 330   | 0     | 0.90   |
| Phison    | PRO-X-2000GB-G2R   | 2 TB   | 1       | 329   | 0     | 0.90   |
| Samsung   | MZVKW1T0HMLH-000H1 | 1 TB   | 6       | 329   | 0     | 0.90   |
| Intel     | SSDPE2KX020T8      | 2 TB   | 8       | 329   | 0     | 0.90   |
| SPCC      | M.2 PCIe SSD       | 128 GB | 2       | 327   | 0     | 0.90   |
| Samsung   | MZVLV256HCHP-00000 | 256 GB | 14      | 325   | 0     | 0.89   |
| Toshiba   | KXG5AZNV512G NV... | 512 GB | 2       | 324   | 0     | 0.89   |
| Lite-On   | CX2-8B256-Q11 NVMe | 256 GB | 8       | 319   | 0     | 0.88   |
| Intel     | SSDPEKKF512G7L     | 512 GB | 6       | 407   | 213   | 0.87   |
| tigo      | SSD                | 512 GB | 1       | 313   | 0     | 0.86   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 1       | 313   | 0     | 0.86   |
| KINGBANK  | KP230              | 512 GB | 2       | 312   | 0     | 0.86   |
| Toshiba   | THNSF51T02DU7      | 1 TB   | 1       | 312   | 0     | 0.86   |
| Phison    | CSSD-M2B1TPG3VNF   | 1 TB   | 1       | 311   | 0     | 0.85   |
| Patriot   | P300               | 512 GB | 1       | 311   | 0     | 0.85   |
| Toshiba   | KXG5AZNV1T02       | 1 TB   | 5       | 310   | 0     | 0.85   |
| OYUNKEY   | 256GB              | 256 GB | 1       | 310   | 0     | 0.85   |
| Transcend | TS256GMTE820       | 256 GB | 1       | 308   | 0     | 0.84   |
| WDC       | WDS500G1B0C-00S6U0 | 500 GB | 19      | 307   | 0     | 0.84   |
| Samsung   | MZVPV128HDGM-000H1 | 128 GB | 1       | 304   | 0     | 0.83   |
| WDC       | WDS250G2X0C-00L350 | 250 GB | 17      | 302   | 0     | 0.83   |
| ADATA     | SX6000NP           | 128 GB | 7       | 362   | 167   | 0.83   |
| Samsung   | MZQLB3T8HALS-00007 | 3.8 TB | 13      | 300   | 0     | 0.82   |
| Patriot   | Scorch M2          | 512 GB | 4       | 300   | 0     | 0.82   |
| WDC       | PC SN720 SDAPNT... | 1 TB   | 1       | 297   | 0     | 0.81   |
| Intel     | SSDPEK1W120GAH     | 118 GB | 2       | 296   | 0     | 0.81   |
| SanDisk   | A400 SD9PN9U-25... | 256 GB | 1       | 296   | 0     | 0.81   |
| Toshiba   | THNSN5128GPU7      | 128 GB | 10      | 296   | 0     | 0.81   |
| Corsair   | Force MP600        | 2 TB   | 18      | 295   | 0     | 0.81   |
| Phison    | Reletech M.2 SSD   | 512 GB | 1       | 293   | 0     | 0.80   |
| Micron    | 7300_MTFDHBE6T4TDG | 6.4 TB | 2       | 293   | 0     | 0.80   |
| Toshiba   | THNSN5256GPUK      | 256 GB | 8       | 430   | 17    | 0.80   |
| Plextor   | PX-256M9PeG        | 256 GB | 5       | 290   | 0     | 0.80   |
| ADATA     | SX6000NP           | 512 GB | 6       | 327   | 19    | 0.80   |
| Intel     | SSDPEKNW020T8      | 2 TB   | 71      | 290   | 0     | 0.79   |
| Corsair   | Force MP300        | 240 GB | 3       | 289   | 0     | 0.79   |
| SPCC      | M.2 PCIE SSD       | 1 TB   | 6       | 289   | 0     | 0.79   |
| Toshiba   | KBG40ZPZ256G ME... | 256 GB | 2       | 288   | 0     | 0.79   |
| PNY       | CS3030 1000GB SSD  | 1 TB   | 4       | 287   | 0     | 0.79   |
| Kingston  | SKC2000M8500G      | 500 GB | 3       | 287   | 0     | 0.79   |
| Reeinno   | MC20 120GB S6N8    | 120 GB | 1       | 284   | 0     | 0.78   |
| Dell      | Express Flash N... | 1.6 TB | 1       | 284   | 0     | 0.78   |
| Toshiba   | KXG60ZNV1T02 NVMe  | 1 TB   | 16      | 281   | 0     | 0.77   |
| Phison    | ESR512GDLCG-E3C-4  | 512 GB | 1       | 281   | 0     | 0.77   |
| Gigaby... | GP-ASM2NE6100TTTD  | 1 TB   | 11      | 280   | 0     | 0.77   |
| Samsung   | MZVKW512HMJP-000H1 | 512 GB | 14      | 287   | 1     | 0.76   |
| Silico... | M Series NVMe S... | 256 GB | 4       | 277   | 0     | 0.76   |
| SSSTC     | CL1-3D256          | 256 GB | 3       | 276   | 0     | 0.76   |
| Ramsta    | R900 M.2 NVMe SSD  | 512 GB | 1       | 276   | 0     | 0.76   |
| Samsung   | MZSLW1T0HMLH-000L1 | 1 TB   | 4       | 274   | 0     | 0.75   |
| XPG       | GAMMIX S11         | 480 GB | 9       | 352   | 112   | 0.75   |
| Samsung   | MZVKW512HMJP-00000 | 512 GB | 11      | 337   | 3     | 0.75   |
| SanDisk   | WD_BLACK SN850     | 2 TB   | 2       | 273   | 0     | 0.75   |
| Phison    | Reletech P400 M... | 2 TB   | 1       | 272   | 0     | 0.75   |
| Toshiba   | KXG50ZNV512G       | 512 GB | 46      | 271   | 0     | 0.74   |
| Goodram   | 120GB              | 120 GB | 1       | 271   | 0     | 0.74   |
| Samsung   | MZFLV512HCJH-000MV | 512 GB | 4       | 269   | 0     | 0.74   |
| Lite-On   | CA1-8D256-HP       | 256 GB | 2       | 269   | 0     | 0.74   |
| Phison    | Sabrent Rocket 4.0 | 2 TB   | 19      | 268   | 0     | 0.73   |
| Intel     | MEMPEK1W016GA      | 16 GB  | 8       | 267   | 0     | 0.73   |
| Corsair   | MP600 PRO XT       | 1 TB   | 1       | 261   | 0     | 0.72   |
| WDC       | WDS250G1B0C-00S6U0 | 250 GB | 15      | 260   | 0     | 0.71   |
| Corsair   | Force MP510        | 960 GB | 33      | 259   | 0     | 0.71   |
| Corsair   | Force MP510 1.9TB  | 1.9 TB | 11      | 258   | 0     | 0.71   |
| Toshiba   | THNSN51T02DU7 NVMe | 1 TB   | 3       | 255   | 0     | 0.70   |
| Toshiba   | KBG30ZMS128G NVMe  | 128 GB | 13      | 253   | 0     | 0.70   |
| Transcend | TS1TMTE220S        | 1 TB   | 10      | 253   | 0     | 0.69   |
| SK hynix  | PC401 HFS512GD9... | 512 GB | 1       | 253   | 0     | 0.69   |
| WDC       | WDS100T3XHC-00SJG0 | 1 TB   | 16      | 252   | 0     | 0.69   |
| Kingch... | 512GB              | 512 GB | 1       | 252   | 0     | 0.69   |
| Samsung   | MZ1LB960HAJQ-00007 | 960 GB | 4       | 252   | 0     | 0.69   |
| Intel     | MEMPEK1J016GAL     | 16 GB  | 10      | 251   | 0     | 0.69   |
| Intel     | MEMPEK1J016GAH     | 16 GB  | 6       | 251   | 0     | 0.69   |
| HP        | SSD EX900 Pro      | 256 GB | 1       | 251   | 0     | 0.69   |
| Toshiba   | THNSF5256GPUK      | 256 GB | 1       | 249   | 0     | 0.68   |
| Corsair   | Force MP600        | 500 GB | 16      | 249   | 0     | 0.68   |
| T-FORCE   | TM8FP5001T         | 1 TB   | 3       | 248   | 0     | 0.68   |
| Toshiba   | THNSN51T02DUK      | 1 TB   | 2       | 246   | 0     | 0.68   |
| Intel     | SSDPEKKF512G8 NVMe | 512 GB | 9       | 245   | 0     | 0.67   |
| Phison    | BPX                | 240 GB | 6       | 327   | 5     | 0.67   |
| Intel     | SSDPEKNW020T9      | 2 TB   | 3       | 245   | 0     | 0.67   |
| Kingston  | SKC2000M81000G     | 1 TB   | 5       | 245   | 0     | 0.67   |
| T-FORCE   | TM8FP8001T         | 1 TB   | 2       | 243   | 0     | 0.67   |
| Transcend | TS512GMTE220S      | 512 GB | 20      | 242   | 0     | 0.67   |
| Plextor   | PX-128M8PeGN       | 128 GB | 1       | 242   | 0     | 0.66   |
| Plextor   | PX-256M9PeGN       | 256 GB | 4       | 240   | 0     | 0.66   |
| Teclast   | 256GB NP900-2280   | 256 GB | 1       | 240   | 0     | 0.66   |
| Corsair   | Force MP600        | 1 TB   | 77      | 240   | 0     | 0.66   |
| ADATA     | SX8200NP           | 960 GB | 3       | 239   | 0     | 0.66   |
| Samsung   | MZVLV256HCHP-000H1 | 256 GB | 11      | 239   | 0     | 0.66   |
| Phison    | Sabrent            | 1 TB   | 155     | 238   | 0     | 0.65   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 13      | 238   | 0     | 0.65   |
| Seagate   | BarraCuda 510 S... | 500 GB | 4       | 238   | 0     | 0.65   |
| Mushkin   | MKNSSDPL2TB-D8     | 2 TB   | 1       | 238   | 0     | 0.65   |
| SK hynix  | PC601A NVMe        | 512 GB | 2       | 237   | 0     | 0.65   |
| Lite-On   | CL1-4D128          | 128 GB | 2       | 236   | 0     | 0.65   |
| Intel     | HBRPEKNX0203AHO    | 32 GB  | 16      | 236   | 0     | 0.65   |
| Phison    | ESO256GMFCH-E3C-2  | 256 GB | 1       | 235   | 0     | 0.65   |
| Toshiba   | KXG60ZNV512G NVMe  | 512 GB | 39      | 234   | 0     | 0.64   |
| PNY       | CS2030 480GB SSD   | 480 GB | 1       | 234   | 0     | 0.64   |
| Transcend | TS2TMTE220S        | 2 TB   | 2       | 233   | 0     | 0.64   |
| Toshiba   | KBG40ZNS1T02 ME... | 1 TB   | 1       | 232   | 0     | 0.64   |
| BAITITON  | BT58SSD08E         | 128 GB | 1       | 232   | 0     | 0.64   |
| Lite-On   | CL1-3D128-Q11 NVMe | 128 GB | 3       | 232   | 0     | 0.64   |
| ADATA     | SX7000NP           | 256 GB | 2       | 232   | 0     | 0.64   |
| Intel     | SSDPEKKW256G8      | 256 GB | 50      | 232   | 0     | 0.64   |
| Intel     | SSDPEKKF256G8H     | 256 GB | 1       | 232   | 0     | 0.64   |
| Toshiba   | KBG40ZPZ512G NVMe  | 512 GB | 3       | 232   | 0     | 0.64   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 4       | 231   | 0     | 0.63   |
| Toshiba   | THNSN0128GTYA      | 128 GB | 4       | 231   | 0     | 0.63   |
| T-CREATE  | TM8FPH001T         | 1 TB   | 1       | 230   | 0     | 0.63   |
| Samsung   | SSD 960 PRO        | 512 GB | 72      | 245   | 3     | 0.63   |
| Hikvision | HS-SSD-E2000       | 256 GB | 2       | 229   | 0     | 0.63   |
| KIOXIA    | KXG60PNV2T04 NVMe  | 2 TB   | 14      | 229   | 0     | 0.63   |
| Seagate   | FireCuda 510 SS... | 1 TB   | 11      | 228   | 0     | 0.63   |
| Crucial   | CT1000P1SSD8       | 1 TB   | 220     | 243   | 24    | 0.63   |
| Mushkin   | MKNSSDPL1TB-D8     | 1 TB   | 1       | 227   | 0     | 0.62   |
| ADATA     | SX8200NP           | 240 GB | 6       | 251   | 20    | 0.62   |
| Lite-On   | T10 240            | 240 GB | 1       | 227   | 0     | 0.62   |
| LDLC      | 120GB              | 120 GB | 1       | 226   | 0     | 0.62   |
| Samsung   | SSD 960 PRO        | 1 TB   | 26      | 254   | 5     | 0.62   |
| Goodram   | IR-SSDPR-P34B-0... | 2 TB   | 5       | 225   | 0     | 0.62   |
| AMD       | R5MP120G8          | 120 GB | 10      | 224   | 0     | 0.61   |
| Corsair   | Force MP300        | 120 GB | 3       | 223   | 0     | 0.61   |
| SanDisk   | Extreme Pro        | 1 TB   | 9       | 221   | 0     | 0.61   |
| ADATA     | SX8200PNP          | 1 TB   | 123     | 224   | 3     | 0.61   |
| Samsung   | Portable SSD T7    | 500 GB | 1       | 220   | 0     | 0.60   |
| Intel     | SSDPEKKW256G8L     | 256 GB | 6       | 220   | 0     | 0.60   |
| Toshiba   | KBG40ZPZ1T02 ME... | 1 TB   | 1       | 219   | 0     | 0.60   |
| T-FORCE   | TM8FP7001T         | 1 TB   | 3       | 218   | 0     | 0.60   |
| AMD       | R5MP240G8          | 240 GB | 6       | 217   | 0     | 0.60   |
| SPCC      | M.2 PCIe SSD       | 1 TB   | 47      | 217   | 22    | 0.60   |
| Toshiba   | KXG5AZNV512G       | 512 GB | 13      | 217   | 0     | 0.60   |
| Toshiba   | KBG30ZMS512G NVMe  | 512 GB | 6       | 226   | 168   | 0.59   |
| Toshiba   | RC500              | 500 GB | 5       | 216   | 0     | 0.59   |
| Intel     | SSDPEKNW256G8      | 256 GB | 1       | 215   | 0     | 0.59   |
| HP        | SSD EX950          | 1 TB   | 14      | 215   | 0     | 0.59   |
| SK hynix  | HFS256GD9MNE-6200A | 256 GB | 3       | 214   | 0     | 0.59   |
| XPG       | GAMMIX S70         | 2 TB   | 7       | 214   | 0     | 0.59   |
| LDLC      | F8+M.2 480         | 480 GB | 3       | 213   | 0     | 0.59   |
| Lenovo    | LENSE20256GMSP3... | 256 GB | 26      | 228   | 8     | 0.58   |
| Samsung   | KUS040202M-B000    | 512 GB | 2       | 211   | 0     | 0.58   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 6       | 210   | 0     | 0.58   |
| Team      | TM8FP4001T         | 1 TB   | 6       | 232   | 338   | 0.58   |
| ZHITAI    | PC005 Active       | 1 TB   | 3       | 210   | 0     | 0.58   |
| Intel     | SSDPEL1K100GA      | 100 GB | 2       | 382   | 5     | 0.58   |
| SK hynix  | PC601 NVMe         | 1 TB   | 10      | 209   | 0     | 0.58   |
| HP        | SSD EX900          | 250 GB | 17      | 236   | 60    | 0.57   |
| Transcend | TS128GMTE110S      | 128 GB | 17      | 208   | 0     | 0.57   |
| UMIS      | RPIRJ512VME2OWD    | 512 GB | 1       | 208   | 0     | 0.57   |
| Silico... | Asgard AN2 250N... | 250 GB | 3       | 207   | 0     | 0.57   |
| XPG       | GAMMIX S50         | 1 TB   | 8       | 207   | 0     | 0.57   |
| Seagate   | FireCuda 510 SS... | 2 TB   | 4       | 207   | 0     | 0.57   |
| Crucial   | CT500P1SSD8        | 500 GB | 111     | 213   | 6     | 0.57   |
| Silico... | ZEPLIN ZM-710      | 1 TB   | 1       | 207   | 0     | 0.57   |
| Gigabyte  | GP-ASM2NE6200TTTD  | 2 TB   | 3       | 206   | 0     | 0.57   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 2       | 206   | 0     | 0.57   |
| Intel     | SSDPEKKW512G8      | 512 GB | 17      | 205   | 0     | 0.56   |
| Intel     | HBRPEKNX0203AH     | 1 TB   | 16      | 205   | 0     | 0.56   |
| Toshiba   | KBG40ZNS512G NVMe  | 512 GB | 14      | 204   | 0     | 0.56   |
| Intel     | SSDPEKNW010T8      | 1 TB   | 238     | 206   | 5     | 0.56   |
| Gigabyte  | GP-AG70S2TB        | 2 TB   | 1       | 204   | 0     | 0.56   |
| Toshiba   | KXG50ZNV256G       | 256 GB | 30      | 203   | 0     | 0.56   |
| Apacer    | AS2280P4           | 240 GB | 2       | 203   | 0     | 0.56   |
| Phison    | ESR512GTLCG-EAC-4  | 512 GB | 4       | 203   | 0     | 0.56   |
| Toshiba   | KXG6APNV2T04       | 2 TB   | 4       | 203   | 0     | 0.56   |
| Kingston  | SNVS2000GB         | 2 TB   | 2       | 202   | 0     | 0.56   |
| Samsung   | MZVLW1T0HMLH-000L2 | 1 TB   | 6       | 202   | 0     | 0.55   |
| HP        | SSD EX920          | 1 TB   | 13      | 201   | 0     | 0.55   |
| Toshiba   | KBG40ZPZ1T02 NVMe  | 1 TB   | 1       | 201   | 0     | 0.55   |
| Toshiba   | RC100              | 240 GB | 10      | 200   | 0     | 0.55   |
| PNY       | CS3140 2TB SSD     | 2 TB   | 1       | 200   | 0     | 0.55   |
| XPG       | GAMMIX S11 Pro     | 1 TB   | 111     | 204   | 1     | 0.55   |
| Transcend | TS256GMTE220S      | 256 GB | 11      | 200   | 0     | 0.55   |
| Micron    | 9200_MTFDHAL1T6TCU | 1.6 TB | 1       | 200   | 0     | 0.55   |
| Intel     | HBRPEKNX0202AHO    | 32 GB  | 46      | 207   | 9     | 0.55   |
| Silico... | NVME SSD           | 512 GB | 8       | 199   | 0     | 0.55   |
| Intel     | SSDPED1D960GAY     | 960 GB | 1       | 199   | 0     | 0.55   |
| Samsung   | SSD 960 EVO        | 1 TB   | 57      | 204   | 1     | 0.55   |
| Team      | TM8FP4512G         | 512 GB | 1       | 198   | 0     | 0.54   |
| Gigabyte  | GP-GSM2NE3100TNTD  | 1 TB   | 8       | 198   | 0     | 0.54   |
| Phison    | Sabrent Rocket 4.0 | 1 TB   | 81      | 197   | 0     | 0.54   |
| Intel     | SSDPEKKW128G8      | 128 GB | 17      | 197   | 0     | 0.54   |
| V-GeN     | V-GEN10SM19EG25... | 256 GB | 1       | 197   | 0     | 0.54   |
| Silico... | Asgard AN512NVM... | 512 GB | 2       | 195   | 0     | 0.54   |
| Intel     | H10 HBRPEKNX020... | 512 GB | 33      | 195   | 0     | 0.54   |
| Foxline   | FLSSD256M80ECX5    | 256 GB | 1       | 195   | 0     | 0.54   |
| LDLC      | 240GB              | 240 GB | 1       | 194   | 0     | 0.53   |
| Gigaby... | GP-GSM2NE3128GNTD  | 128 GB | 3       | 193   | 0     | 0.53   |
| Toshiba   | KBG30ZMS512G       | 512 GB | 1       | 193   | 0     | 0.53   |
| Mushkin   | MKNSSDPE2TB-D8     | 2 TB   | 14      | 192   | 0     | 0.53   |
| Samsung   | SM961 NVMe         | 1 TB   | 2       | 298   | 8     | 0.53   |
| Gigabyte  | GP-ASM2NE6100TTTD  | 1 TB   | 6       | 191   | 0     | 0.52   |
| Samsung   | MZVLW512HMJP-000L2 | 512 GB | 20      | 191   | 0     | 0.52   |
| Intel     | SSDPEKKF256G8 NVMe | 256 GB | 12      | 190   | 0     | 0.52   |
| Toshiba   | KBG40ZNS256G NVMe  | 256 GB | 20      | 190   | 0     | 0.52   |
| Toshiba   | THNSN5256GPU7 NVMe | 256 GB | 6       | 190   | 0     | 0.52   |
| Dell      | Ent NVMe AGN MU... | 1.6 TB | 1       | 190   | 0     | 0.52   |
| Mushkin   | MKNSSDHL500GB-D8   | 500 GB | 1       | 189   | 0     | 0.52   |
| Samsung   | MZVLV512HCJH-000H1 | 512 GB | 2       | 189   | 0     | 0.52   |
| ADATA     | SX8200PNP          | 2 TB   | 46      | 188   | 0     | 0.52   |
| Intel     | H10 HBRPEKNX010... | 256 GB | 3       | 188   | 0     | 0.52   |
| Samsung   | SSD 960 EVO        | 500 GB | 133     | 203   | 19    | 0.52   |
| Samsung   | MZVPW256HEGL-00000 | 256 GB | 19      | 188   | 0     | 0.52   |
| Samsung   | MZFLV128HCGR-000MV | 128 GB | 15      | 188   | 0     | 0.52   |
| Crucial   | CT1000X8SSD8       | 1 TB   | 1       | 187   | 0     | 0.51   |
| WDC       | WDBRPG5000ANC-WRSN | 500 GB | 17      | 187   | 0     | 0.51   |
| Reletech  | M.2 SSD            | 512 GB | 2       | 187   | 0     | 0.51   |
| Toshiba   | KBG40ZNS128G NVMe  | 128 GB | 5       | 186   | 0     | 0.51   |
| Toshiba   | THNSN0256GTYA      | 256 GB | 2       | 185   | 0     | 0.51   |
| PNY       | CS3030 250GB SSD   | 250 GB | 9       | 184   | 0     | 0.51   |
| Samsung   | MS1PC5ED3ORA3.2T   | 3.2 TB | 1       | 184   | 0     | 0.50   |
| WDC       | WDS500G3XHC-00SJG0 | 500 GB | 20      | 183   | 0     | 0.50   |
| Toshiba   | KBG40ZNS256G ME... | 256 GB | 2       | 183   | 0     | 0.50   |
| Intel     | HBRPEKNX0202AH     | 512 GB | 48      | 183   | 0     | 0.50   |
| Samsung   | PM981 NVMe         | 1 TB   | 12      | 182   | 0     | 0.50   |
| Kingston  | SA1000M8960G       | 960 GB | 1       | 182   | 0     | 0.50   |
| Kingston  | OM8PCP3512F-A01    | 512 GB | 1       | 180   | 0     | 0.49   |
| Kingch... | 128GB              | 128 GB | 1       | 180   | 0     | 0.49   |
| Samsung   | MZVKW1T0HMLH-00000 | 1 TB   | 3       | 180   | 0     | 0.49   |
| SanDisk   | Extreme Pro        | 500 GB | 10      | 180   | 0     | 0.49   |
| SK hynix  | PC601 HFS001TD9... | 1 TB   | 2       | 179   | 0     | 0.49   |
| XrayDisk  | 512GB              | 512 GB | 2       | 179   | 0     | 0.49   |
| PNY       | CS3040 1TB SSD     | 1 TB   | 2       | 178   | 0     | 0.49   |
| Seagate   | FireCuda 510 SS... | 500 GB | 2       | 178   | 0     | 0.49   |
| SK hynix  | PC611 NVMe         | 256 GB | 5       | 177   | 0     | 0.49   |
| Phison    | PCIe SSD           | 1 TB   | 97      | 177   | 0     | 0.49   |
| Intel     | HBRPEKNX0101AHO    | 16 GB  | 19      | 176   | 0     | 0.48   |
| ADATA     | SX8200PNP          | 512 GB | 116     | 176   | 0     | 0.48   |
| SK hynix  | PC601 HFS512GD9... | 512 GB | 19      | 174   | 0     | 0.48   |
| Patriot   | Scorch M2          | 128 GB | 6       | 173   | 0     | 0.48   |
| Kingston  | SA2000M8500G       | 500 GB | 141     | 173   | 0     | 0.47   |
| Kingston  | SEDC1000BM8240G    | 240 GB | 3       | 173   | 0     | 0.47   |
| Lite-On   | CA3-8D512          | 512 GB | 7       | 172   | 0     | 0.47   |
| Team      | M8FP2              | 480 GB | 1       | 172   | 0     | 0.47   |
| Transcend | TS1TMTE110S        | 1 TB   | 1       | 172   | 0     | 0.47   |
| Lexar     | SSD                | 512 GB | 1       | 171   | 0     | 0.47   |
| SK hynix  | PC601 NVMe         | 512 GB | 52      | 171   | 0     | 0.47   |
| Phison    | E12-512G-PHISON... | 512 GB | 4       | 171   | 0     | 0.47   |
| Intel     | HBRPEKNX0202ALO    | 32 GB  | 9       | 171   | 0     | 0.47   |
| KIOXIA    | KXG60ZNV512G NVMe  | 512 GB | 42      | 171   | 0     | 0.47   |
| Corsair   | MP600 PRO          | 1 TB   | 4       | 171   | 0     | 0.47   |
| Corsair   | Force MP510        | 240 GB | 44      | 171   | 0     | 0.47   |
| Lite-On   | S980 256           | 256 GB | 1       | 170   | 0     | 0.47   |
| Corsair   | Force MP510        | 480 GB | 38      | 170   | 0     | 0.47   |
| Intel     | 660p SSDPEKNW51... | 512 GB | 1       | 170   | 0     | 0.47   |
| Phison    | Viper M.2 VPN100   | 1 TB   | 23      | 170   | 0     | 0.47   |
| Intel     | SSDPEKNW512G8      | 512 GB | 308     | 170   | 0     | 0.47   |
| Samsung   | MZ1LB960HAJQ-000H5 | 960 GB | 1       | 169   | 0     | 0.46   |
| Samsung   | MZVLB1T0HALR-00A00 | 1 TB   | 1       | 169   | 0     | 0.46   |
| OWC       | Aura N             | 960 GB | 2       | 168   | 0     | 0.46   |
| Kingston  | SA2000M8250G       | 250 GB | 107     | 165   | 0     | 0.45   |
| Seagate   | FireCuda 520 SS... | 2 TB   | 14      | 165   | 0     | 0.45   |
| Toshiba   | KXG60ZNV256G NVMe  | 256 GB | 23      | 165   | 0     | 0.45   |
| Lenovo    | LENSE20512GMSP3... | 512 GB | 13      | 168   | 1     | 0.45   |
| Kingston  | RBUSNS8154P3512GJ1 | 512 GB | 21      | 164   | 0     | 0.45   |
| Plextor   | PX-256M8PeY        | 256 GB | 2       | 163   | 0     | 0.45   |
| Apacer    | AS2280P4           | 480 GB | 1       | 163   | 0     | 0.45   |
| Toshiba   | RC500              | 250 GB | 2       | 163   | 0     | 0.45   |
| Mushkin   | MKNSSDPL500GB-D8   | 500 GB | 2       | 163   | 0     | 0.45   |
| KIOXIA... | SSD                | 1 TB   | 4       | 162   | 0     | 0.45   |
| Toshiba   | RC100              | 120 GB | 2       | 162   | 0     | 0.45   |
| ADATA     | SX8200PNP          | 256 GB | 47      | 185   | 47    | 0.44   |
| Intel     | HBRPEKNX0101AO     | 16 GB  | 2       | 161   | 0     | 0.44   |
| Samsung   | MZFLV256HCHP-000MV | 256 GB | 9       | 160   | 0     | 0.44   |
| Dell      | Ent NVMe v2 AGN... | 1.6 TB | 2       | 160   | 0     | 0.44   |
| PNY       | CS3030 1TB SSD     | 1 TB   | 15      | 159   | 0     | 0.44   |
| Phison    | TurtleArmor T3000  | 2 TB   | 1       | 158   | 0     | 0.43   |
| Samsung   | MZVPW256HEGL-000H1 | 256 GB | 9       | 158   | 0     | 0.43   |
| Hikvision | HS-SSD-E1000 128G  | 128 GB | 2       | 158   | 0     | 0.43   |
| Toshiba   | THNSN5256GPUK      | 256 GB | 2       | 157   | 0     | 0.43   |
| Dell      | Ent NVMe v2 AGN... | 1.9 TB | 3       | 157   | 0     | 0.43   |
| Toshiba   | KBG40ZPZ128G ME... | 128 GB | 4       | 156   | 0     | 0.43   |
| Samsung   | MZVLW512HMJP-00000 | 512 GB | 21      | 158   | 1     | 0.43   |
| Samsung   | MZVLW128HEGR-000L1 | 128 GB | 6       | 156   | 0     | 0.43   |
| Samsung   | MZVLB256HAHQ-000H2 | 256 GB | 2       | 156   | 0     | 0.43   |
| Samsung   | MZFLW1T0HMLH-000MU | 1 TB   | 3       | 156   | 0     | 0.43   |
| SK hynix  | PC401 NVMe         | 256 GB | 18      | 156   | 1     | 0.43   |
| SK hynix  | PC611 NVMe         | 512 GB | 37      | 155   | 0     | 0.43   |
| KIOXIA... | SSD                | 500 GB | 12      | 154   | 0     | 0.42   |
| KIOXIA    | KXG60PNV512G NVMe  | 512 GB | 3       | 153   | 0     | 0.42   |
| Silico... | BW-NV1             | 128 GB | 1       | 153   | 0     | 0.42   |
| Phison    | Sabrent Rocket 4.0 | 500 GB | 12      | 153   | 0     | 0.42   |
| SK hynix  | PC601A NVMe        | 1 TB   | 4       | 152   | 0     | 0.42   |
| Seagate   | FireCuda 520 SS... | 500 GB | 19      | 152   | 0     | 0.42   |
| SanDisk   | WD_BLACK SN850 ... | 2 TB   | 1       | 151   | 0     | 0.42   |
| WDC       | WDS500G3X0C-00SJG0 | 500 GB | 150     | 152   | 7     | 0.41   |
| Phison    | PP3-8D256          | 256 GB | 1       | 150   | 0     | 0.41   |
| Gigabyte  | GP-GSM2NE8256GNTD  | 256 GB | 2       | 150   | 0     | 0.41   |
| Samsung   | SM951 NVMe         | 256 GB | 1       | 150   | 0     | 0.41   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 20      | 150   | 0     | 0.41   |
| Samsung   | MZVKW512HMJP-000L7 | 512 GB | 18      | 150   | 0     | 0.41   |
| HP        | SSD EX900          | 500 GB | 15      | 202   | 6     | 0.41   |
| Plextor   | PX-256M8PeG        | 256 GB | 3       | 225   | 335   | 0.41   |
| HP        | SSD EX950          | 512 GB | 10      | 148   | 0     | 0.41   |
| Lite-On   | CX2-GB1024-Q11 ... | 1 TB   | 1       | 147   | 0     | 0.40   |
| Plextor   | PX-512M8PeG        | 512 GB | 6       | 166   | 92    | 0.40   |
| Crucial   | CT2000P1SSD8       | 2 TB   | 3       | 146   | 0     | 0.40   |
| Intel     | MEMPEI1J016GAL     | 16 GB  | 2       | 146   | 0     | 0.40   |
| Gigaby... | GP-AG4500G         | 500 GB | 6       | 146   | 0     | 0.40   |
| Phison    | Sabrent Rocket Q   | 1 TB   | 75      | 146   | 0     | 0.40   |
| Intel     | HBRPEKNX0101AH     | 256 GB | 18      | 146   | 0     | 0.40   |
| Intel     | HBRPEKNX0202AL     | 512 GB | 10      | 146   | 0     | 0.40   |
| Silico... | M.2 (P80) 3TG3-P   | 1 TB   | 1       | 146   | 0     | 0.40   |
| Intel     | SSDPEL1D380GA      | 384 GB | 1       | 146   | 0     | 0.40   |
| Intel     | HBRPEKNX0203A      | 1 TB   | 2       | 145   | 0     | 0.40   |
| Samsung   | SSD 960 PRO        | 2 TB   | 10      | 156   | 6     | 0.40   |
| Samsung   | MZVLW1T0HMLH-000L7 | 1 TB   | 13      | 150   | 2     | 0.40   |
| BIOSTAR   | M700-512GB         | 512 GB | 1       | 144   | 0     | 0.40   |
| Samsung   | SSD 970 PRO        | 512 GB | 180     | 145   | 1     | 0.40   |
| Samsung   | MZ1LB3T8HMLA-00007 | 3.8 TB | 3       | 144   | 0     | 0.40   |
| Samsung   | SSD 970 EVO        | 250 GB | 165     | 149   | 2     | 0.39   |
| KIOXIA    | KBG40ZPZ512G NVMe  | 512 GB | 15      | 143   | 0     | 0.39   |
| Plextor   | PX-512M9PeY        | 512 GB | 5       | 143   | 0     | 0.39   |
| SPCC      | M.2 PCIe SSD       | 2 TB   | 9       | 145   | 28    | 0.39   |
| Toshiba   | KBG30ZMT512G       | 512 GB | 7       | 143   | 0     | 0.39   |
| Kingston  | RBUSNS8154P3512GJ5 | 512 GB | 6       | 143   | 0     | 0.39   |
| Mushkin   | MKNSSDVT1TB-D8     | 1 TB   | 1       | 143   | 0     | 0.39   |
| KIOXIA    | KXG60ZNV1T02 NVMe  | 1 TB   | 45      | 143   | 0     | 0.39   |
| Intel     | SSDPEBKF128G7      | 128 GB | 3       | 500   | 10    | 0.39   |
| Seagate   | BarraCuda Q5 ZP... | 1 TB   | 4       | 142   | 0     | 0.39   |
| Toshiba   | KBG30ZMV512G       | 512 GB | 22      | 141   | 0     | 0.39   |
| Toshiba   | KXG50PNV2T04       | 2 TB   | 3       | 140   | 0     | 0.38   |
| Intel     | SSDPEKKF010T7      | 1 TB   | 1       | 139   | 0     | 0.38   |
| Kingston  | SA2000M81000G      | 1 TB   | 165     | 141   | 19    | 0.38   |
| Intel     | SSDPEK1W060GA      | 64 GB  | 2       | 139   | 0     | 0.38   |
| KIOXIA    | KXG6AZNV512G NV... | 512 GB | 7       | 138   | 0     | 0.38   |
| Toshiba   | KXG6AZNV512G NV... | 512 GB | 1       | 137   | 0     | 0.38   |
| Kingston  | RBUSNS8154P3256GJ5 | 256 GB | 3       | 137   | 0     | 0.38   |
| Intel     | SSDPEKNW512G8L     | 512 GB | 46      | 136   | 0     | 0.37   |
| Kingston  | SEDC1000BM8480G    | 480 GB | 1       | 136   | 0     | 0.37   |
| ORICO     | V500               | 256 GB | 1       | 136   | 0     | 0.37   |
| KIOXIA    | KXG50PNV2T04       | 2 TB   | 1       | 136   | 0     | 0.37   |
| SNR       | ML480M             | 480 GB | 1       | 135   | 0     | 0.37   |
| KIOXIA    | KXG60ZNV512G       | 512 GB | 30      | 135   | 0     | 0.37   |
| Smartbuy  | m.2 PS5008T-2280T  | 256 GB | 1       | 135   | 0     | 0.37   |
| Phison    | Reletech P400Pr... | 500 GB | 1       | 135   | 0     | 0.37   |
| Transcend | TS512GMTE110S      | 512 GB | 9       | 135   | 0     | 0.37   |
| Micron    | 9300_MTFDHAL6T4TDR | 6.4 TB | 2       | 134   | 0     | 0.37   |
| Corsair   | MP400              | 4 TB   | 2       | 134   | 0     | 0.37   |
| Samsung   | MZVLW256HEHP-00000 | 256 GB | 65      | 135   | 1     | 0.37   |
| Toshiba   | KBG30ZMV256G       | 256 GB | 49      | 134   | 0     | 0.37   |
| HP        | SSD EX950          | 2 TB   | 13      | 133   | 0     | 0.37   |
| Micron    | 2200V_MTFDHBA25... | 256 GB | 2       | 133   | 0     | 0.37   |
| Samsung   | MZVLW1T0HMLH-00000 | 1 TB   | 7       | 132   | 0     | 0.36   |
| Gigabyte  | GP-AG41TB          | 1 TB   | 12      | 131   | 0     | 0.36   |
| Kingston  | SA1000M8480G       | 480 GB | 9       | 131   | 0     | 0.36   |
| WDC       | WDS250G3X0C-00SJG0 | 250 GB | 22      | 131   | 0     | 0.36   |
| UMIS      | RPJTJ256MED1OWX    | 256 GB | 5       | 130   | 0     | 0.36   |
| Intel     | SSDPEKKF512G7      | 512 GB | 1       | 130   | 0     | 0.36   |
| Intel     | HBRPEKNX0203AO     | 32 GB  | 3       | 130   | 0     | 0.36   |
| FORESEE   | P900F256GB         | 256 GB | 2       | 130   | 0     | 0.36   |
| WDC       | WDBA3V0010BNC-WRSN | 1 TB   | 5       | 129   | 0     | 0.36   |
| Lite-On   | CX2-8B512-Q11 NVMe | 512 GB | 4       | 129   | 0     | 0.36   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 21      | 129   | 0     | 0.36   |
| Plextor   | PX-1TM8PeY         | 1 TB   | 2       | 129   | 0     | 0.35   |
| SK hynix  | PC611 NVMe         | 1 TB   | 43      | 129   | 0     | 0.35   |
| Samsung   | SM961 NVMe         | 512 GB | 3       | 129   | 0     | 0.35   |
| SK hynix  | PC601 HFS256GD9... | 256 GB | 5       | 128   | 0     | 0.35   |
| Phison    | Viper M.2 VP4100   | 1 TB   | 7       | 128   | 0     | 0.35   |
| Transcend | TS128GMTE652T      | 128 GB | 1       | 127   | 0     | 0.35   |
| Intel     | SSDPE2KE020T7      | 2 TB   | 4       | 127   | 0     | 0.35   |
| Samsung   | SSD 960 EVO        | 250 GB | 194     | 134   | 12    | 0.35   |
| Samsung   | MZVLB1T0HALR-00007 | 1 TB   | 1       | 126   | 0     | 0.35   |
| Apacer    | Z280 120G          | 120 GB | 2       | 126   | 0     | 0.35   |
| Silico... | NE-256             | 256 GB | 26      | 125   | 0     | 0.34   |
| WDC       | WDS100T2B0C-00PXH0 | 1 TB   | 209     | 125   | 0     | 0.34   |
| Samsung   | SSD 970 PRO        | 1 TB   | 94      | 131   | 1     | 0.34   |
| Seagate   | FireCuda 520 SS... | 1 TB   | 17      | 123   | 0     | 0.34   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 22      | 123   | 0     | 0.34   |
| Phison    | E12S-512G-PHISO... | 512 GB | 1       | 123   | 0     | 0.34   |
| Gigaby... | GP-AG42TB          | 2 TB   | 4       | 123   | 0     | 0.34   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 9       | 123   | 0     | 0.34   |
| Phison    | APS-SE20G-2T       | 2 TB   | 1       | 122   | 0     | 0.34   |
| Lite-On   | CA3-8D128-HP       | 128 GB | 4       | 122   | 0     | 0.34   |
| HP        | SSD EX920          | 256 GB | 2       | 230   | 1     | 0.33   |
| Phison    | BPXP               | 960 GB | 2       | 122   | 0     | 0.33   |
| KIOXIA    | KXG6AZNV512G       | 512 GB | 3       | 121   | 0     | 0.33   |
| WDC       | WDBGMP0020BNC-WRSN | 2 TB   | 1       | 121   | 0     | 0.33   |
| Seagate   | BarraCuda 510 S... | 1 TB   | 5       | 120   | 0     | 0.33   |
| Samsung   | PM981 NVMe         | 256 GB | 25      | 120   | 0     | 0.33   |
| Silico... | NE-1TB             | 1 TB   | 11      | 120   | 0     | 0.33   |
| Intel     | SSDPEKKF010T8 NVMe | 1 TB   | 5       | 119   | 0     | 0.33   |
| Toshiba   | KXG60ZNV1T02       | 1 TB   | 20      | 119   | 0     | 0.33   |
| Samsung   | MZVKW1T0HMLH-000L7 | 1 TB   | 1       | 119   | 0     | 0.33   |
| KIOXIA    | KBG30ZMV256G       | 256 GB | 27      | 120   | 38    | 0.33   |
| FORESEE   | P900F256GBH        | 256 GB | 2       | 118   | 0     | 0.33   |
| Toshiba   | KXG60ZNV256G       | 256 GB | 23      | 118   | 0     | 0.32   |
| SK hynix  | HFS256GD9TNG-L2A0A | 256 GB | 3       | 118   | 0     | 0.32   |
| Intel     | SSDPEKKW010T8      | 1 TB   | 8       | 118   | 0     | 0.32   |
| Zheino    | CHN-NGFFNV2280-256 | 256 GB | 2       | 117   | 0     | 0.32   |
| Samsung   | MZVLW256HEHP-000L2 | 256 GB | 44      | 120   | 1     | 0.32   |
| Samsung   | MZVLW128HEGR-000H1 | 128 GB | 15      | 116   | 0     | 0.32   |
| WDC       | WDS100T3X0C-00SJG0 | 1 TB   | 128     | 116   | 5     | 0.32   |
| AMD       | R5MP128G8          | 128 GB | 1       | 116   | 0     | 0.32   |
| Hikvision | HS-SSD-C2000       | 1 TB   | 1       | 116   | 0     | 0.32   |
| SPCC      | M.2 PCIe SSD       | 256 GB | 46      | 116   | 44    | 0.32   |
| ADATA     | SX8100NP           | 2 TB   | 4       | 335   | 254   | 0.32   |
| Corsair   | Force MP510        | 4 TB   | 3       | 115   | 0     | 0.32   |
| Intel     | H20 HBRPEKNL020... | 1 TB   | 1       | 115   | 0     | 0.32   |
| Gigaby... | GP-ASM2NE2256GTTDR | 256 GB | 2       | 114   | 0     | 0.31   |
| Phison    | Sabrent Rocket ... | 1 TB   | 13      | 114   | 0     | 0.31   |
| KIOXIA... | PRO SSD            | 2 TB   | 2       | 114   | 0     | 0.31   |
| Micron    | 2200S NVMe         | 512 GB | 51      | 114   | 0     | 0.31   |
| Toshiba   | THNSN5128GPUK      | 128 GB | 1       | 114   | 0     | 0.31   |
| Phison    | ESR01TBTLCG-EAC-4  | 1 TB   | 3       | 114   | 0     | 0.31   |
| Phison    | TerransForce PM... | 512 GB | 1       | 113   | 0     | 0.31   |
| Toshiba   | KBG30ZMV128G       | 128 GB | 6       | 157   | 169   | 0.31   |
| KIOXIA    | KBG40ZNS512G NVMe  | 512 GB | 141     | 112   | 0     | 0.31   |
| Toshiba   | KBG30ZMS256G NVMe  | 256 GB | 29      | 112   | 0     | 0.31   |
| Intel     | HBRPEKNX0101ALO    | 16 GB  | 1       | 112   | 0     | 0.31   |
| KIOXIA    | KXG60ZNV256G       | 256 GB | 15      | 112   | 0     | 0.31   |
| WDC       | WDS250G2B0C-00PXH0 | 250 GB | 43      | 112   | 0     | 0.31   |
| ASint     | AS806              | 128 GB | 1       | 111   | 0     | 0.31   |
| Gigaby... | GP-ASM2NE6500GTTD  | 500 GB | 5       | 111   | 0     | 0.31   |
| Intel     | HBRPEKNX0101AL     | 256 GB | 1       | 111   | 0     | 0.31   |
| SSSTC     | CL1-8D512          | 512 GB | 7       | 111   | 0     | 0.31   |
| KIOXIA    | KBG40ZNS128G NVMe  | 128 GB | 20      | 111   | 0     | 0.30   |
| Samsung   | MZVLW256HEHP-000L7 | 256 GB | 113     | 111   | 1     | 0.30   |
| Intel     | SSDPEKKF256G8L     | 256 GB | 62      | 112   | 17    | 0.30   |
| WDC       | WDS200T3X0C-00SJG0 | 2 TB   | 12      | 110   | 0     | 0.30   |
| HUAWEI    | HWE52P432T0L005N   | 2 TB   | 6       | 110   | 0     | 0.30   |
| Samsung   | MZVLW512HMJP-000L7 | 512 GB | 28      | 110   | 1     | 0.30   |
| Phison    | SBXe               | 480 GB | 3       | 110   | 0     | 0.30   |
| Silico... | NE-512             | 512 GB | 18      | 110   | 0     | 0.30   |
| ADATA     | SX8100NP           | 512 GB | 13      | 116   | 80    | 0.30   |
| SK hynix  | SKHynix_HFS001T... | 1 TB   | 3       | 109   | 0     | 0.30   |
| PNY       | CS2130 1TB SSD     | 1 TB   | 10      | 109   | 0     | 0.30   |
| Samsung   | MZVKW512HMJP-00007 | 512 GB | 1       | 109   | 0     | 0.30   |
| WDC       | WD BLACK SDBPNT... | 1 TB   | 1       | 109   | 0     | 0.30   |
| Phison    | Sabrent Rocket ... | 1 TB   | 27      | 108   | 0     | 0.30   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 6       | 108   | 0     | 0.30   |
| KIOXIA    | KBG40ZNS256G NVMe  | 256 GB | 92      | 108   | 0     | 0.30   |
| Samsung   | MZVLB1T0HALR-00000 | 1 TB   | 45      | 132   | 1     | 0.29   |
| SPCC      | M.2 PCIe SSD       | 512 GB | 41      | 110   | 26    | 0.29   |
| Kingston  | SKC2500M81000G     | 1 TB   | 19      | 107   | 0     | 0.29   |
| XPG       | GAMMIX S41         | 512 GB | 3       | 275   | 339   | 0.29   |
| PNY       | CS3030 2TB SSD     | 2 TB   | 16      | 107   | 0     | 0.29   |
| AMD       | R5MP256G8          | 256 GB | 1       | 107   | 0     | 0.29   |
| Samsung   | PM961 NVMe         | 1 TB   | 5       | 106   | 0     | 0.29   |
| Lite-On   | CA3-8D512-Q11 NVMe | 512 GB | 1       | 106   | 0     | 0.29   |
| KIOXIA    | KBG40ZPZ256G NVMe  | 256 GB | 6       | 106   | 0     | 0.29   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 15      | 106   | 0     | 0.29   |
| Silico... | ASint AS806        | 128 GB | 1       | 106   | 0     | 0.29   |
| Samsung   | PM961 NVMe         | 512 GB | 14      | 123   | 3     | 0.29   |
| KIOXIA    | KXG60PNV2T04       | 2 TB   | 6       | 106   | 0     | 0.29   |
| Micron    | 7400_MTFDKBG3T8TDZ | 3.8 TB | 4       | 106   | 0     | 0.29   |
| Intel     | HBRPEKNX0101A      | 256 GB | 3       | 105   | 0     | 0.29   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 82      | 105   | 13    | 0.29   |
| Intel     | SSDPEMKF256G8H     | 256 GB | 9       | 105   | 0     | 0.29   |
| WDC       | PC SN720 NVMe      | 1 TB   | 1       | 104   | 0     | 0.29   |
| Kingston  | OM8PCP3512F-AB     | 512 GB | 60      | 104   | 0     | 0.29   |
| KLLISRE   | 512GB              | 512 GB | 3       | 104   | 0     | 0.29   |
| Micron    | 7300_MTFDHBE3T8TDF | 3.8 TB | 5       | 104   | 0     | 0.29   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 28      | 103   | 0     | 0.28   |
| Samsung   | MZVLB1T0HALR-000L7 | 1 TB   | 46      | 103   | 0     | 0.28   |
| Gigabyte  | GP-GSM2NE3512GNTD  | 512 GB | 6       | 103   | 0     | 0.28   |
| Team      | TM8FP6256G         | 256 GB | 9       | 103   | 0     | 0.28   |
| Toshiba   | THNSF5256GPU7      | 256 GB | 2       | 103   | 0     | 0.28   |
| SanDisk   | WD_BLACK SN850     | 1 TB   | 14      | 103   | 0     | 0.28   |
| Intel     | HBRPEKNX0202AO     | 32 GB  | 36      | 102   | 0     | 0.28   |
| Kingston  | OM3PDP3128B-AH     | 128 GB | 1       | 102   | 0     | 0.28   |
| SSSTC     | CL1-3D256-Q11 NVMe | 256 GB | 16      | 102   | 0     | 0.28   |
| Seagate   | FireCuda 530 ZP... | 2 TB   | 7       | 102   | 0     | 0.28   |
| Phison    | M.2 PCIE G3x4 NVMe | 1 TB   | 3       | 102   | 0     | 0.28   |
| Acer      | SSD FA100          | 1 TB   | 2       | 102   | 0     | 0.28   |
| PNY       | CS2130 2TB SSD     | 2 TB   | 3       | 101   | 0     | 0.28   |
| SK hynix  | SHGP31-1000GM-2    | 1 TB   | 22      | 101   | 0     | 0.28   |
| Plextor   | PX-512M9PGN +      | 512 GB | 2       | 101   | 0     | 0.28   |
| Apacer    | AS2280P4           | 512 GB | 11      | 101   | 0     | 0.28   |
| SK hynix  | HFS256GD9TNG-62A0A | 256 GB | 25      | 102   | 1     | 0.28   |
| Lite-On   | CL1-4D256          | 256 GB | 5       | 101   | 0     | 0.28   |
| Samsung   | MZVLB2T0HMLB-000L2 | 2 TB   | 1       | 101   | 0     | 0.28   |
| KIOXIA    | KBG40ZPZ1T02 NVMe  | 1 TB   | 16      | 101   | 0     | 0.28   |
| Samsung   | MZVLB512HAJQ-000L2 | 512 GB | 29      | 101   | 1     | 0.28   |
| Intel     | SSDPEKNW010T8H     | 1 TB   | 20      | 100   | 0     | 0.28   |
| Phison    | PM8128GPTCB3B-E82  | 128 GB | 1       | 100   | 0     | 0.28   |
| Silico... | Reletech P400 M... | 1 TB   | 1       | 100   | 0     | 0.28   |
| BIWIN     | NI201_256GB        | 256 GB | 2       | 100   | 0     | 0.27   |
| Kingston  | RBUSNS8154P3256GJ3 | 256 GB | 28      | 99    | 0     | 0.27   |
| Phison    | E12-1TB-PHISON-... | 1 TB   | 1       | 99    | 0     | 0.27   |
| Toshiba   | KBG30ZMT128G       | 128 GB | 20      | 99    | 0     | 0.27   |
| Gigaby... | GP-AG41TB          | 1 TB   | 9       | 99    | 0     | 0.27   |
| ADATA     | SX6000PNP          | 512 GB | 16      | 99    | 9     | 0.27   |
| Samsung   | MZVLW256HEHP-000H1 | 256 GB | 62      | 104   | 1     | 0.27   |
| WDC       | PC SN720 SDAQNT... | 256 GB | 1       | 98    | 0     | 0.27   |
| WDC       | WDS500G2B0C-00PXH0 | 500 GB | 152     | 98    | 0     | 0.27   |
| Intel     | SSDPE2KX040T8      | 4 TB   | 14      | 98    | 0     | 0.27   |
| KIOXIA    | KXG7AZNV512G LA    | 512 GB | 2       | 98    | 0     | 0.27   |
| Plextor   | PX-1TM8SeG         | 1 TB   | 2       | 559   | 61    | 0.27   |
| SK hynix  | PC601 SED NVMe     | 1 TB   | 3       | 98    | 0     | 0.27   |
| Zheino    | CHN-NGFFNV2280-1TB | 1 TB   | 2       | 98    | 0     | 0.27   |
| Corsair   | MP400              | 2 TB   | 7       | 97    | 0     | 0.27   |
| Goodram   | SSDPR-PX400-256-80 | 256 GB | 1       | 97    | 0     | 0.27   |
| Toshiba   | KXG60ZNV512G       | 512 GB | 40      | 97    | 0     | 0.27   |
| Toshiba   | KXG60PNV2T04 NV... | 2 TB   | 5       | 97    | 0     | 0.27   |
| Lite-On   | CA3-8D256          | 256 GB | 11      | 97    | 0     | 0.27   |
| Gigaby... | GP-GSM2NE3100TNTD  | 1 TB   | 13      | 96    | 0     | 0.27   |
| Kingston  | OM8PCP31024F-AI1   | 1 TB   | 9       | 96    | 0     | 0.27   |
| Silico... | NVME SSD           | 256 GB | 8       | 96    | 0     | 0.27   |
| Patriot   | Hellfire M2        | 480 GB | 1       | 96    | 0     | 0.26   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 47      | 96    | 0     | 0.26   |
| Samsung   | SSD 970 EVO        | 1 TB   | 359     | 106   | 4     | 0.26   |
| Seagate   | FireCuda 530 ZP... | 4 TB   | 11      | 95    | 0     | 0.26   |
| Silico... | C2000              | 256 GB | 1       | 95    | 0     | 0.26   |
| Gigabyte  | GP-AG4500G         | 500 GB | 4       | 95    | 0     | 0.26   |
| Hyundai   | 256G SSD           | 256 GB | 1       | 95    | 0     | 0.26   |
| Intel     | SSDPEKNW010T9      | 1 TB   | 28      | 94    | 0     | 0.26   |
| Phison    | Daten DS2000       | 512 GB | 3       | 94    | 0     | 0.26   |
| KIOXIA    | KXG60ZNV1T02       | 1 TB   | 28      | 94    | 0     | 0.26   |
| Samsung   | MZVLB512HAJQ-00007 | 512 GB | 1       | 94    | 0     | 0.26   |
| Hikvision | HS-SSD-E2000L 256G | 256 GB | 1       | 94    | 0     | 0.26   |
| Lite-On   | NVMe CA5-8D512     | 512 GB | 3       | 94    | 0     | 0.26   |
| Samsung   | MZPLL3T2HAJQ-00005 | 3.2 TB | 1       | 94    | 0     | 0.26   |
| Samsung   | SSD 970 EVO        | 500 GB | 370     | 101   | 6     | 0.26   |
| UMIS      | RPJTJ512MEE1OWX    | 512 GB | 40      | 94    | 0     | 0.26   |
| Plextor   | PX-1TM8PeG         | 1 TB   | 1       | 93    | 0     | 0.26   |
| Phison    | ESO128GTLC9-E8C-2  | 128 GB | 1       | 93    | 0     | 0.26   |
| Samsung   | MZVLB2T0HMLB-000H1 | 2 TB   | 3       | 93    | 0     | 0.26   |
| Toshiba   | KBG30ZMT256G       | 256 GB | 23      | 93    | 0     | 0.26   |
| Silico... | Viper VPN100       | 1 TB   | 1       | 93    | 0     | 0.25   |
| Toshiba   | KXG6AZNV1T02       | 1 TB   | 24      | 92    | 0     | 0.25   |
| Intel     | HBRPEKNX0202A      | 512 GB | 37      | 92    | 0     | 0.25   |
| KIOXIA    | KXG7AZNV1T02 LA    | 1 TB   | 2       | 92    | 0     | 0.25   |
| Intel     | SSDPEKNW512G8H     | 512 GB | 198     | 94    | 11    | 0.25   |
| Toshiba   | KXG6AZNV512G       | 512 GB | 56      | 91    | 0     | 0.25   |
| Samsung   | MZ9LQ1T0HALB-00000 | 1 TB   | 1       | 91    | 0     | 0.25   |
| Micron    | 2200 NVMe          | 512 GB | 2       | 91    | 0     | 0.25   |
| Silico... | aigo NVMe SSD P... | 256 GB | 1       | 91    | 0     | 0.25   |
| Crucial   | CT1000P2SSD8       | 1 TB   | 113     | 91    | 0     | 0.25   |
| Smartbuy  | m.2 E13-2280       | 256 GB | 1       | 90    | 0     | 0.25   |
| Samsung   | PM981 NVMe         | 2 TB   | 2       | 90    | 0     | 0.25   |
| Union ... | UMIS RPJTJ256ME... | 256 GB | 3       | 90    | 0     | 0.25   |
| Silico... | R5MP480G8          | 480 GB | 2       | 90    | 0     | 0.25   |
| Patriot   | P300               | 128 GB | 7       | 90    | 0     | 0.25   |
| Micron    | 7300_MTFDHBG3T8TDF | 3.8 TB | 1       | 89    | 0     | 0.25   |
| Toshiba   | KBG30ZPZ512G       | 512 GB | 1       | 89    | 0     | 0.24   |
| Samsung   | PM961 NVMe         | 256 GB | 19      | 89    | 0     | 0.24   |
| ADATA     | IM2P33E8-001TD     | 1 TB   | 2       | 89    | 0     | 0.24   |
| Kingston  | RBUSNS8154P3256GJ2 | 256 GB | 1       | 89    | 0     | 0.24   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 37      | 88    | 0     | 0.24   |
| Intel     | SSDPEMKF010T8 NVMe | 1 TB   | 25      | 98    | 42    | 0.24   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 20      | 88    | 0     | 0.24   |
| Patriot   | Scorch M2          | 256 GB | 6       | 88    | 0     | 0.24   |
| Silico... | 1TB PCS PCIe M.... | 1 TB   | 4       | 88    | 0     | 0.24   |
| Toshiba   | KXG6AZNV256G       | 256 GB | 30      | 87    | 0     | 0.24   |
| Toshiba   | KBG30ZPZ128G       | 128 GB | 14      | 88    | 1     | 0.24   |
| AXIOM     | 500GB              | 500 GB | 1       | 87    | 0     | 0.24   |
| Goodram   | SSDPR-PX500-256-80 | 256 GB | 7       | 87    | 0     | 0.24   |
| Qunion    | P20A               | 1 TB   | 1       | 87    | 0     | 0.24   |
| Goodram   | SSDPR-PX500-01T-80 | 1 TB   | 3       | 87    | 0     | 0.24   |
| ADATA     | SX6000PNP          | 256 GB | 26      | 98    | 1     | 0.24   |
| Phison    | PS5012-E12S-1T     | 1 TB   | 1       | 86    | 0     | 0.24   |
| Micron    | 2200S NVMe         | 1 TB   | 16      | 87    | 1     | 0.24   |
| Kingston  | RBUSNS8154P3128GJ  | 128 GB | 24      | 86    | 0     | 0.24   |
| Gigabyte  | GP-AG70S1TB        | 1 TB   | 4       | 86    | 0     | 0.24   |
| Micron    | 7300_MTFDHBE7T6TDF | 7.6 TB | 5       | 86    | 0     | 0.24   |
| Toshiba   | THNSN5256GPU7      | 256 GB | 1       | 85    | 0     | 0.23   |
| Crucial   | CT500P2SSD8        | 500 GB | 119     | 85    | 0     | 0.23   |
| Kingston  | SA1000M8240G       | 240 GB | 33      | 85    | 0     | 0.23   |
| Samsung   | PM981 NVMe         | 512 GB | 54      | 87    | 1     | 0.23   |
| Phison    | Viper M.2 VPN110   | 512 GB | 1       | 85    | 0     | 0.23   |
| Smartbuy  | m.2 PS5013-2280T   | 256 GB | 3       | 84    | 0     | 0.23   |
| SK hynix  | PC300 NVMe         | 256 GB | 7       | 93    | 1     | 0.23   |
| UMIS      | RPEYJ512VMM2QWY    | 512 GB | 1       | 84    | 0     | 0.23   |
| SK hynix  | SHGP31-500GM-2     | 500 GB | 12      | 84    | 0     | 0.23   |
| Samsung   | PM991 NVMe         | 128 GB | 4       | 84    | 0     | 0.23   |
| WDC       | PC SN720 SDAQNT... | 512 GB | 55      | 84    | 0     | 0.23   |
| Samsung   | MZVLW128HEGR-000L2 | 128 GB | 28      | 93    | 1     | 0.23   |
| WDC       | PC SN530 SDBPNP... | 1 TB   | 34      | 83    | 0     | 0.23   |
| WDC       | PC SN520 NVMe      | 256 GB | 21      | 83    | 0     | 0.23   |
| Silico... | R5MP120G8          | 120 GB | 3       | 83    | 0     | 0.23   |
| ADATA     | LEGEND 700         | 1 TB   | 1       | 83    | 0     | 0.23   |
| T-CREATE  | TM8FPF002T         | 2 TB   | 1       | 83    | 0     | 0.23   |
| Samsung   | MZVLB256HBHQ-000   | 256 GB | 5       | 83    | 0     | 0.23   |
| Lenovo    | LENSE30512GMSP3... | 512 GB | 19      | 83    | 1     | 0.23   |
| XPG       | SPECTRIX S20G      | 500 GB | 3       | 82    | 0     | 0.22   |
| SSSTC     | CL1-3D512-Q11 NVMe | 512 GB | 13      | 82    | 0     | 0.22   |
| Samsung   | MZVLB2T0HMLB-00000 | 2 TB   | 1       | 81    | 0     | 0.22   |
| SK hynix  | SKHynix_HFS001T... | 1 TB   | 35      | 81    | 0     | 0.22   |
| Gigaby... | GP-ASM2NE6200TTTD  | 2 TB   | 6       | 81    | 0     | 0.22   |
| Silico... | SK                 | 128 GB | 1       | 81    | 0     | 0.22   |
| Phison    | Sabrent Rocket Q4  | 1 TB   | 10      | 81    | 0     | 0.22   |
| Samsung   | MZVLW512HMJP-000H1 | 512 GB | 22      | 81    | 0     | 0.22   |
| SK hynix  | PC401 NVMe         | 512 GB | 56      | 103   | 2     | 0.22   |
| WDC       | WDBA3V2500ANC-WRSN | 250 GB | 1       | 80    | 0     | 0.22   |
| Gigaby... | GP-GSM2NE8256GNTD  | 256 GB | 2       | 80    | 0     | 0.22   |
| Samsung   | MZVLB512HAJQ-000L7 | 512 GB | 134     | 81    | 1     | 0.22   |
| Samsung   | MZVPV256HDGL-000L2 | 256 GB | 1       | 80    | 0     | 0.22   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 17      | 80    | 0     | 0.22   |
| SPCC      | M.2 PCIE SSD       | 256 GB | 3       | 79    | 0     | 0.22   |
| Kingston  | RBUSNS8154P3512GJ2 | 512 GB | 4       | 79    | 0     | 0.22   |
| SanDisk   | Ultra 3D NVMe      | 1 TB   | 33      | 79    | 0     | 0.22   |
| Plextor   | PX-256M9PeY        | 256 GB | 3       | 79    | 0     | 0.22   |
| Corsair   | Force MP300        | 960 GB | 1       | 79    | 0     | 0.22   |
| Samsung   | KUS030202M-B000    | 256 GB | 11      | 79    | 0     | 0.22   |
| Samsung   | MZVLB512HAJQ-000H1 | 512 GB | 92      | 79    | 0     | 0.22   |
| UMIS      | RPITJ512VME2OWD    | 512 GB | 6       | 78    | 0     | 0.22   |
| SK hynix  | PC601 NVMe         | 256 GB | 9       | 78    | 0     | 0.22   |
| Samsung   | MZVLB512HAJQ-00000 | 512 GB | 111     | 78    | 1     | 0.21   |
| WDC       | PC SN520 NVMe      | 128 GB | 21      | 78    | 0     | 0.21   |
| WDC       | WDS100T2B0C        | 1 TB   | 17      | 77    | 0     | 0.21   |
| Phison    | Sabrent SB-RKT4... | 4 TB   | 2       | 77    | 0     | 0.21   |
| WDC       | WD BLACK SDBPNT... | 512 GB | 3       | 77    | 0     | 0.21   |
| UMIS      | RPJTJ128MED1MWX    | 128 GB | 6       | 84    | 16    | 0.21   |
| XrayDisk  | 256GB              | 256 GB | 5       | 77    | 0     | 0.21   |
| Dell      | Ent NVMe AGN MU... | 1.6 TB | 2       | 77    | 0     | 0.21   |
| SK hynix  | PC400 NVMe         | 512 GB | 1       | 77    | 0     | 0.21   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 24      | 77    | 0     | 0.21   |
| Silico... | NE-128             | 128 GB | 16      | 76    | 5     | 0.21   |
| WDC       | PC SN720 SED SD... | 1 TB   | 3       | 76    | 0     | 0.21   |
| Union ... | UMIS RPJTJ128ME... | 128 GB | 2       | 76    | 0     | 0.21   |
| Silico... | KingSSD-N201000    | 1 TB   | 1       | 76    | 0     | 0.21   |
| Samsung   | MZVLW512HMJP-000H7 | 512 GB | 3       | 76    | 0     | 0.21   |
| Silico... | 256GB PCS PCIe ... | 256 GB | 7       | 76    | 0     | 0.21   |
| Intel     | SSDPEKKW010T8L     | 1 TB   | 2       | 75    | 0     | 0.21   |
| WDC       | PC SN520 NVMe      | 512 GB | 25      | 75    | 0     | 0.21   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 8       | 75    | 0     | 0.21   |
| Lite-On   | CB1-SD512          | 512 GB | 1       | 75    | 0     | 0.21   |
| Intel     | SSDPEKKF010T8L     | 1 TB   | 30      | 79    | 7     | 0.21   |
| PNY       | CS3030 500GB SSD   | 500 GB | 20      | 111   | 2     | 0.21   |
| Micron    | 2210 NVMe          | 512 GB | 1       | 75    | 0     | 0.21   |
| Intel     | SSDPE2MD400G4      | 400 GB | 1       | 74    | 0     | 0.21   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 5       | 74    | 0     | 0.21   |
| Crucial   | CT2000P2SSD8       | 2 TB   | 25      | 74    | 0     | 0.21   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 31      | 74    | 0     | 0.20   |
| KIOXIA... | PLUS SSD           | 1 TB   | 6       | 74    | 0     | 0.20   |
| Mushkin   | MKNSSDPE1TB-D8     | 1 TB   | 5       | 74    | 0     | 0.20   |
| WDC       | PC SN520 SDAPMU... | 256 GB | 3       | 74    | 0     | 0.20   |
| HP        | SSD EX900          | 1 TB   | 9       | 186   | 5     | 0.20   |
| Intel     | SSDPEMKF256G8 NVMe | 256 GB | 5       | 74    | 0     | 0.20   |
| XPG       | GAMMIX S50 Lite    | 1 TB   | 12      | 74    | 0     | 0.20   |
| Lite-On   | CL1-8D512          | 512 GB | 9       | 74    | 0     | 0.20   |
| Toshiba   | KXG60ZNV256G NV... | 256 GB | 1       | 74    | 0     | 0.20   |
| Samsung   | PM981a NVMe        | 1 TB   | 33      | 73    | 0     | 0.20   |
| Samsung   | MZVLB512HAJQ-000H7 | 512 GB | 12      | 73    | 0     | 0.20   |
| Micron    | 2200S NVMe         | 256 GB | 13      | 73    | 0     | 0.20   |
| UMIS      | RPJTJ128MEE1MWX    | 128 GB | 7       | 73    | 0     | 0.20   |
| Samsung   | SSD 970 EVO Plus   | 500 GB | 664     | 73    | 1     | 0.20   |
| WDC       | PC SN730 NVMe      | 256 GB | 6       | 73    | 0     | 0.20   |
| SK hynix  | PC711 NVMe         | 1 TB   | 58      | 73    | 0     | 0.20   |
| KIOXIA    | KBG40ZNV128G       | 128 GB | 6       | 73    | 0     | 0.20   |
| Micron    | 2200V_MTFDHBA51... | 512 GB | 39      | 73    | 0     | 0.20   |
| Silico... | AITC M.2 FZ300     | 128 GB | 1       | 73    | 0     | 0.20   |
| Phison    | ESR01TBTLG-E6GB... | 1 TB   | 4       | 72    | 0     | 0.20   |
| Lite-On   | CA1-8D128          | 128 GB | 3       | 72    | 0     | 0.20   |
| Samsung   | Portable SSD T7    | 1 TB   | 2       | 72    | 0     | 0.20   |
| SK hynix  | PC401 NVMe         | 1 TB   | 12      | 77    | 1     | 0.20   |
| Team      | TM8FP4256G         | 256 GB | 3       | 72    | 0     | 0.20   |
| Samsung   | MZVLB256HAHQ-000L7 | 256 GB | 66      | 73    | 1     | 0.20   |
| Silico... | WT PCIE-256GB      | 256 GB | 1       | 71    | 0     | 0.20   |
| Toshiba   | KBG30ZPZ256G       | 256 GB | 2       | 71    | 0     | 0.20   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 2       | 71    | 0     | 0.20   |
| ADATA     | SX6000LNP          | 256 GB | 16      | 71    | 0     | 0.20   |
| SK hynix  | PC711 HFS001TDE... | 1 TB   | 4       | 71    | 0     | 0.19   |
| Silico... | NVME 512GB SSD     | 512 GB | 1       | 70    | 0     | 0.19   |
| Kingston  | RBUSNS8154P3128GJ5 | 128 GB | 5       | 70    | 0     | 0.19   |
| Kingston  | OM8PDP3256B-AB1    | 256 GB | 7       | 70    | 0     | 0.19   |
| Intel     | SSDPEKNU512GZL     | 512 GB | 3       | 69    | 0     | 0.19   |
| SK hynix  | HFS001TD9TNG-L2A0A | 1 TB   | 3       | 69    | 0     | 0.19   |
| WDC       | PC SN520 SDAPMU... | 256 GB | 51      | 69    | 0     | 0.19   |
| SK hynix  | BC501 NVMe         | 256 GB | 24      | 69    | 0     | 0.19   |
| Micron    | 2210_MTFDHBA512QFD | 512 GB | 86      | 69    | 0     | 0.19   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 68      | 68    | 0     | 0.19   |
| WDC       | PC SN730 SDBQNT... | 256 GB | 1       | 68    | 0     | 0.19   |
| Netac     | NVMe SSD           | 250 GB | 4       | 68    | 0     | 0.19   |
| Kingston  | SKC2500M82000G     | 2 TB   | 9       | 68    | 0     | 0.19   |
| Intel     | SSDPEKKF512G8L     | 512 GB | 41      | 74    | 4     | 0.19   |
| Samsung   | MZ9LQ256HAJD-000   | 256 GB | 1       | 68    | 0     | 0.19   |
| Mushkin   | MKNSSDHL1TB-D8     | 1 TB   | 7       | 89    | 11    | 0.19   |
| ADATA     | IM2P33F3 NVMe      | 512 GB | 9       | 73    | 1     | 0.18   |
| Intel     | SSDPEMKF512G8 NVMe | 512 GB | 19      | 67    | 0     | 0.18   |
| ADATA     | SX8100NP           | 1 TB   | 5       | 67    | 0     | 0.18   |
| Kingston  | OM8PDP3128B-AI1    | 128 GB | 2       | 67    | 0     | 0.18   |
| Toshiba   | KBG40ZNT512G ME... | 512 GB | 58      | 66    | 0     | 0.18   |
| Micron    | MTFDHBA1T0QFD-1... | 1 TB   | 3       | 66    | 0     | 0.18   |
| Phison    | Metabox Perform... | 2 TB   | 1       | 66    | 0     | 0.18   |
| SSSTC     | CL4-3D1024-Q11 ... | 1 TB   | 2       | 66    | 0     | 0.18   |
| WDC       | PC SN520 SDAPMU... | 512 GB | 51      | 66    | 0     | 0.18   |
| Kingston  | RBUSNS8154P3512GJ  | 512 GB | 21      | 69    | 49    | 0.18   |
| Intel     | SSDPEKNU512G8L     | 512 GB | 2       | 66    | 0     | 0.18   |
| Silico... | NP830              | 512 GB | 1       | 66    | 0     | 0.18   |
| Samsung   | MZQL21T9HCJR-00... | 1.9 TB | 12      | 66    | 0     | 0.18   |
| SK hynix  | PC401 HFS256GD9... | 256 GB | 16      | 66    | 0     | 0.18   |
| Seagate   | FireCuda 530 ZP... | 2 TB   | 2       | 66    | 0     | 0.18   |
| WDC       | PC SN720 SDAPNT... | 1 TB   | 15      | 65    | 0     | 0.18   |
| SSSTC     | CL1-4D256          | 256 GB | 35      | 65    | 0     | 0.18   |
| Kingston  | OM8PCP3512F-A02    | 512 GB | 7       | 65    | 0     | 0.18   |
| Toshiba   | KBG20ZMS512G NVMe  | 512 GB | 1       | 65    | 0     | 0.18   |
| SanDisk   | WD_BLACK SN750     | 2 TB   | 5       | 65    | 0     | 0.18   |
| SK hynix  | PC300 NVMe         | 1 TB   | 9       | 64    | 0     | 0.18   |
| KIOXIA    | KBG30ZMV128G       | 128 GB | 2       | 64    | 0     | 0.18   |
| Corsair   | MP600 CORE         | 1 TB   | 4       | 64    | 0     | 0.18   |
| Samsung   | PM961 NVMe SED     | 512 GB | 1       | 64    | 0     | 0.18   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 21      | 64    | 0     | 0.18   |
| XPG       | GAMMIX S7          | 512 GB | 1       | 64    | 0     | 0.18   |
| Patriot   | P300               | 256 GB | 5       | 64    | 0     | 0.18   |
| ShiJi     | 512GB              | 512 GB | 1       | 64    | 0     | 0.18   |
| Phison    | 512GB SM280512G... | 512 GB | 4       | 64    | 0     | 0.18   |
| XPG       | SX8200PNP-512GT    | 512 GB | 1       | 63    | 0     | 0.18   |
| Micron    | MTFDHBA512TCK      | 512 GB | 11      | 63    | 0     | 0.17   |
| Toshiba   | KXG60ZNV1T02 NV... | 1 TB   | 15      | 63    | 0     | 0.17   |
| SK hynix  | BC501 HFM128GDJ... | 128 GB | 5       | 63    | 0     | 0.17   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 38      | 63    | 0     | 0.17   |
| XPG       | SPECTRIX S40G      | 1 TB   | 25      | 79    | 82    | 0.17   |
| WDC       | PC SN520 SDAPMU... | 128 GB | 14      | 63    | 1     | 0.17   |
| Silico... | Asgard AN1TNVMe... | 1 TB   | 1       | 63    | 0     | 0.17   |
| WDC       | PC SN730 SDBQNT... | 1 TB   | 6       | 62    | 0     | 0.17   |
| Reletech  | P400 SSD           | 512 GB | 3       | 62    | 0     | 0.17   |
| Samsung   | MZVLB1T0HALR-000L2 | 1 TB   | 21      | 64    | 2     | 0.17   |
| SK hynix  | SHGP31-1000GM      | 1 TB   | 14      | 62    | 0     | 0.17   |
| Lite-On   | CA3-8D256-Q11 NVMe | 256 GB | 1       | 61    | 0     | 0.17   |
| WDC       | PC SN530 SDBPNP... | 1 TB   | 17      | 61    | 0     | 0.17   |
| Kingston  | RBUSNS8154P3256GJ  | 256 GB | 27      | 61    | 0     | 0.17   |
| Kingston  | SFYRS500G          | 500 GB | 4       | 61    | 0     | 0.17   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 59      | 61    | 0     | 0.17   |
| Apple     | SSD SM2048L        | 2 TB   | 2       | 61    | 0     | 0.17   |
| Samsung   | MZVLW1T0HMLH-000H1 | 1 TB   | 4       | 61    | 0     | 0.17   |
| Intel     | SSDPEKNU010TZ      | 1 TB   | 44      | 61    | 0     | 0.17   |
| Samsung   | MZVLB256HAHQ-00000 | 256 GB | 59      | 61    | 0     | 0.17   |
| Phison    | Enmotus P200-90... | 900 GB | 1       | 61    | 0     | 0.17   |
| SK hynix  | SKHynix_HFM512G... | 512 GB | 41      | 61    | 0     | 0.17   |
| SK hynix  | BC711 NVMe         | 512 GB | 58      | 61    | 0     | 0.17   |
| Kingston  | SKC2500M8500G      | 500 GB | 12      | 61    | 0     | 0.17   |
| Phison    | APS-SE20G-512      | 512 GB | 2       | 61    | 0     | 0.17   |
| WDC       | PC SN720 SDAQNT... | 256 GB | 15      | 60    | 0     | 0.17   |
| ADATA     | SWORDFISH          | 250 GB | 9       | 60    | 0     | 0.17   |
| Lenovo    | SL700 PCI-E M.2    | 1 TB   | 1       | 60    | 0     | 0.17   |
| Silico... | SSD_M.2_PCIe3_5... | 512 GB | 1       | 60    | 0     | 0.17   |
| UMIS      | RPJTJ256MEE1OWX    | 256 GB | 53      | 60    | 0     | 0.17   |
| Intel     | SSDPEKKW020T8      | 2 TB   | 2       | 60    | 0     | 0.17   |
| Intel     | H10 HBRPEKNX020... | 1 TB   | 3       | 104   | 1     | 0.17   |
| Phison    | SBX                | 256 GB | 2       | 60    | 0     | 0.17   |
| Micron    | 2450 NVMe          | 1 TB   | 2       | 60    | 0     | 0.17   |
| Corsair   | MP600 PRO          | 2 TB   | 3       | 60    | 0     | 0.17   |
| Seagate   | FireCuda 530 ZP... | 500 GB | 4       | 60    | 0     | 0.17   |
| SK hynix  | HFB1M8MO331C0MR    | 256 GB | 3       | 60    | 0     | 0.16   |
| Kingch... | 256GB              | 256 GB | 1       | 60    | 0     | 0.16   |
| ADATA     | SX6000LNP          | 512 GB | 15      | 59    | 0     | 0.16   |
| Micron    | 2450 NVMe          | 512 GB | 1       | 59    | 0     | 0.16   |
| XPG       | GAMMIX S5          | 1 TB   | 28      | 60    | 13    | 0.16   |
| WDC       | PC SN530 SDBPTP... | 1 TB   | 1       | 59    | 0     | 0.16   |
| Lite-On   | CA3-8D256-HP       | 256 GB | 2       | 59    | 0     | 0.16   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 1       | 59    | 0     | 0.16   |
| Samsung   | MZVLB1T0HALR-000H1 | 1 TB   | 18      | 58    | 0     | 0.16   |
| Netac     | NVMe SSD           | 256 GB | 4       | 58    | 0     | 0.16   |
| Kingston  | SNVS1000GB         | 1 TB   | 21      | 58    | 0     | 0.16   |
| Hikvision | HS-SSD-C2000Pro    | 1 TB   | 1       | 58    | 0     | 0.16   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 16      | 58    | 0     | 0.16   |
| Netac     | NVMe SSD           | 500 GB | 6       | 58    | 0     | 0.16   |
| Apple     | SSD AP1024M        | 1 TB   | 5       | 58    | 0     | 0.16   |
| WDC       | WD BLACK SDBPNT... | 2 TB   | 1       | 58    | 0     | 0.16   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 21      | 58    | 0     | 0.16   |
| Crucial   | CT250P2SSD8        | 250 GB | 23      | 58    | 0     | 0.16   |
| Samsung   | KUS040205M-B001    | 512 GB | 3       | 58    | 0     | 0.16   |
| WDC       | WUS3BA138C7P3E3    | 3.8 TB | 1       | 58    | 0     | 0.16   |
| Gigabyte  | GP-ASM2NE6500GTTD  | 500 GB | 3       | 57    | 0     | 0.16   |
| Netac     | NVMe SSD           | 512 GB | 4       | 57    | 0     | 0.16   |
| SK hynix  | HFM512GD3JX016N    | 512 GB | 24      | 57    | 0     | 0.16   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 55      | 57    | 0     | 0.16   |
| Samsung   | MZVLB256HAHQ-000H1 | 256 GB | 75      | 57    | 0     | 0.16   |
| SK hynix  | HFM001TD3JX013N    | 1 TB   | 87      | 57    | 0     | 0.16   |
| OSCOO     | OSC PCIe           | 256 GB | 2       | 56    | 0     | 0.16   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 24      | 56    | 0     | 0.16   |
| T-FORCE   | TM8FP8002T         | 2 TB   | 1       | 56    | 0     | 0.16   |
| Samsung   | SSD 970 EVO Plus   | 1 TB   | 739     | 56    | 1     | 0.15   |
| UMIS      | RPITJ1TBVME2HWD    | 1 TB   | 2       | 56    | 0     | 0.15   |
| Samsung   | MZQL23T8HCLS-00... | 3.8 TB | 9       | 56    | 0     | 0.15   |
| Kingston  | OM8PDP3256B-AI1    | 256 GB | 11      | 56    | 0     | 0.15   |
| Seagate   | BarraCuda 510 S... | 256 GB | 1       | 55    | 0     | 0.15   |
| ADATA     | IM2P32A8-256GITB5  | 256 GB | 1       | 55    | 0     | 0.15   |
| Kingston  | OM8PDP3512B-A01    | 512 GB | 25      | 55    | 0     | 0.15   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 13      | 55    | 0     | 0.15   |
| SK hynix  | PC801 NVMe         | 2 TB   | 7       | 55    | 0     | 0.15   |
| Mushkin   | MKNSSDPE500GB-D8   | 500 GB | 1       | 54    | 0     | 0.15   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 10      | 54    | 0     | 0.15   |
| SETHRISE  | Nvme 512G          | 512 GB | 1       | 54    | 0     | 0.15   |
| Samsung   | MZVLB1T0HBLR-00000 | 1 TB   | 54      | 54    | 0     | 0.15   |
| Gigabyte  | GP-GSM2NE3128GNTD  | 128 GB | 4       | 54    | 0     | 0.15   |
| Silico... | Asgard AN3 1TNV... | 1 TB   | 1       | 54    | 0     | 0.15   |
| KIOXIA    | KBG40ZNV256G       | 256 GB | 90      | 53    | 0     | 0.15   |
| WDC       | WD BLACK SDBPNT... | 256 GB | 1       | 53    | 0     | 0.15   |
| Phison    | SWG256G-112HI      | 256 GB | 2       | 53    | 0     | 0.15   |
| WDC       | WDS500G1X0E-00AFY0 | 500 GB | 39      | 55    | 1     | 0.15   |
| Samsung   | MZVLB256HAHQ-000L2 | 256 GB | 30      | 53    | 0     | 0.15   |
| Phison    | ESR512GTLG-E6GB... | 512 GB | 4       | 53    | 0     | 0.15   |
| Transcend | TS256GMTE110S      | 256 GB | 6       | 53    | 0     | 0.15   |
| Gigaby... | GP-GSM2NE3256GNTD  | 256 GB | 14      | 53    | 0     | 0.15   |
| Silico... | S2000              | 2 TB   | 4       | 53    | 0     | 0.15   |
| SK hynix  | SHGP31-500GM       | 500 GB | 3       | 53    | 0     | 0.15   |
| WDC       | PC SN530 SDBPNP... | 1 TB   | 6       | 52    | 0     | 0.14   |
| Team      | TM8FP6512G         | 512 GB | 11      | 52    | 0     | 0.14   |
| WDC       | WDBRPG0010BNC-WRSN | 1 TB   | 18      | 52    | 0     | 0.14   |
| Apacer    | AS2280P4           | 256 GB | 37      | 52    | 0     | 0.14   |
| SK hynix  | SKHynix_HFS001T... | 1 TB   | 36      | 52    | 0     | 0.14   |
| INDMEM    | SSD DMPG3N         | 1 TB   | 1       | 313   | 5     | 0.14   |
| Kingston  | OM8PCP3512F-AI1    | 512 GB | 68      | 52    | 0     | 0.14   |
| SK hynix  | SKHynix_HFS001T... | 1 TB   | 5       | 52    | 0     | 0.14   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 6       | 52    | 0     | 0.14   |
| SK hynix  | HFM256GDHTNG-8310A | 256 GB | 19      | 51    | 0     | 0.14   |
| Smartbuy  | m.2 PS5012-2280    | 256 GB | 2       | 51    | 0     | 0.14   |
| Apple     | SSD SM1024L        | 1 TB   | 4       | 51    | 0     | 0.14   |
| SK hynix  | SKHynix_HFM256G... | 256 GB | 27      | 51    | 0     | 0.14   |
| SK hynix  | BA HFS256GD9TNG... | 256 GB | 4       | 51    | 0     | 0.14   |
| ADATA     | IM2P33F8BR2-256GB  | 256 GB | 5       | 51    | 0     | 0.14   |
| Kingston  | OM8PCP3512F-AA     | 512 GB | 31      | 50    | 0     | 0.14   |
| ADATA     | IM2P33F3 NVMe      | 256 GB | 20      | 51    | 1     | 0.14   |
| Samsung   | SSD 970 EVO Plus   | 250 GB | 276     | 50    | 0     | 0.14   |
| Crucial   | CT500P5SSD8        | 500 GB | 46      | 50    | 0     | 0.14   |
| Kingston  | SNVS2000G          | 2 TB   | 25      | 50    | 0     | 0.14   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 6       | 50    | 0     | 0.14   |
| Phison    | E12-512G-PHISON... | 512 GB | 2       | 50    | 0     | 0.14   |
| Colorful  | CN600              | 128 GB | 2       | 50    | 0     | 0.14   |
| ZHITAI    | PC005 Active       | 512 GB | 1       | 50    | 0     | 0.14   |
| Apacer    | AS2280P4U          | 256 GB | 2       | 49    | 0     | 0.14   |
| SPCC      | M.2 PCIE SSD       | 512 GB | 3       | 72    | 337   | 0.14   |
| PNY       | CS2140 1TB SSD     | 1 TB   | 1       | 49    | 0     | 0.14   |
| KIOXIA    | KBG4AZNS1T02       | 1 TB   | 1       | 49    | 0     | 0.14   |
| Samsung   | MZFLW256HEHP-000MV | 256 GB | 6       | 49    | 0     | 0.14   |
| Samsung   | MZQLB1T9HAJR-00007 | 1.9 TB | 12      | 49    | 0     | 0.13   |
| Netac     | NVMe SSD           | 1 TB   | 13      | 48    | 0     | 0.13   |
| Silico... | EX-512 PRO         | 512 GB | 2       | 48    | 0     | 0.13   |
| Samsung   | MZVLW128HEGR-00000 | 128 GB | 24      | 48    | 0     | 0.13   |
| Lenovo    | LENSE30256GMSP3... | 256 GB | 14      | 63    | 1     | 0.13   |
| Corsair   | MP400              | 1 TB   | 6       | 48    | 0     | 0.13   |
| SanDisk   | SN730 SDBQNTY-5... | 512 GB | 2       | 48    | 0     | 0.13   |
| Kingston  | RBUSNS8154P3128GJ3 | 128 GB | 3       | 47    | 0     | 0.13   |
| Solid ... | CL1-3D512-Q11 N... | 512 GB | 2       | 47    | 0     | 0.13   |
| SK hynix  | PC711 NVMe         | 512 GB | 35      | 47    | 0     | 0.13   |
| Silico... | PCIe-8 SSD         | 1 TB   | 2       | 47    | 0     | 0.13   |
| WDC       | WDS500G2B0C        | 500 GB | 15      | 47    | 0     | 0.13   |
| PNY       | CS3040 4TB SSD     | 4 TB   | 2       | 47    | 0     | 0.13   |
| Samsung   | PM991 NVMe         | 256 GB | 25      | 47    | 0     | 0.13   |
| Hikvision | HS-SSD-E2000       | 512 GB | 1       | 47    | 0     | 0.13   |
| Phison    | 1TB SM2801T24GK... | 1 TB   | 18      | 47    | 0     | 0.13   |
| SK hynix  | BC711 NVMe         | 256 GB | 32      | 46    | 0     | 0.13   |
| Silico... | NVME SSD           | 128 GB | 10      | 46    | 0     | 0.13   |
| SanDisk   | WD Green SN350     | 1 TB   | 11      | 46    | 0     | 0.13   |
| WDC       | WDS200T1X0E-00AFY0 | 2 TB   | 24      | 46    | 0     | 0.13   |
| SanDisk   | SDBPTPZ-1T00-11... | 1 TB   | 1       | 46    | 0     | 0.13   |
| Silico... | GV1TB              | 1 TB   | 1       | 46    | 0     | 0.13   |
| SK hynix  | HFM512GD3JX013N    | 512 GB | 67      | 46    | 0     | 0.13   |
| Plextor   | PX-1TM9PeGN        | 1 TB   | 1       | 46    | 0     | 0.13   |
| Samsung   | MZVLB256HBHQ-000L2 | 256 GB | 40      | 46    | 0     | 0.13   |
| SSSTC     | CL1-4D256-D22      | 256 GB | 1       | 46    | 0     | 0.13   |
| Goodram   | IR-SSDPR-P34B-5... | 512 GB | 2       | 45    | 0     | 0.13   |
| Seagate   | BarraCuda Q5 ZP... | 500 GB | 6       | 45    | 0     | 0.13   |
| minisf... | 512GB              | 512 GB | 1       | 45    | 0     | 0.13   |
| Kingston  | OM8PDP3256B-A01    | 256 GB | 11      | 45    | 0     | 0.13   |
| SK hynix  | SKHynix_HFS256G... | 256 GB | 8       | 45    | 0     | 0.13   |
| Silico... | PCIe-8 SSD         | 256 GB | 5       | 45    | 0     | 0.12   |
| WDC       | WDS100T1X0E-00AFY0 | 1 TB   | 83      | 45    | 0     | 0.12   |
| Samsung   | MZVLB2T0HALB-000L7 | 2 TB   | 9       | 45    | 0     | 0.12   |
| Lexar     | 500GB SSD          | 500 GB | 8       | 45    | 0     | 0.12   |
| Silico... | FPI1TBMWR7         | 1 TB   | 1       | 45    | 0     | 0.12   |
| SK hynix  | BC501 HFM256GDJ... | 256 GB | 70      | 45    | 30    | 0.12   |
| SK hynix  | HFM128GDHTNG-8310A | 128 GB | 13      | 45    | 0     | 0.12   |
| ORICO     | V500               | 128 GB | 3       | 44    | 0     | 0.12   |
| WDC       | WDS480G2G0C-00AJM0 | 480 GB | 15      | 44    | 0     | 0.12   |
| J.ZAO     | 5 SERIES 512GB SSD | 512 GB | 1       | 44    | 0     | 0.12   |
| SanDisk   | Extreme Pro        | 2 TB   | 2       | 44    | 0     | 0.12   |
| SK hynix  | HFS512GD9TNG-62A0A | 512 GB | 10      | 50    | 1     | 0.12   |
| Samsung   | MZVLQ256HAJD-00000 | 256 GB | 30      | 43    | 0     | 0.12   |
| SSSTC     | CL1-4D512          | 512 GB | 6       | 43    | 0     | 0.12   |
| Samsung   | MZVLB512HBJQ-000H1 | 512 GB | 90      | 43    | 0     | 0.12   |
| Toshiba   | KBG40ZNT256G ME... | 256 GB | 38      | 43    | 0     | 0.12   |
| Samsung   | MZVLB512HBJQ-00000 | 512 GB | 49      | 43    | 0     | 0.12   |
| SanDisk   | WD_BLACK SN850     | 500 GB | 3       | 43    | 0     | 0.12   |
| WDC       | PC SN730 NVMe      | 512 GB | 36      | 42    | 0     | 0.12   |
| ADATA     | FALCON             | 1 TB   | 4       | 42    | 0     | 0.12   |
| Hikvision | HS-SSD-C2000Pro... | 1 TB   | 3       | 42    | 0     | 0.12   |
| KLLISRE   | 256GB              | 256 GB | 3       | 42    | 0     | 0.12   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 39      | 42    | 0     | 0.12   |
| SanDisk   | WD Blue SN570      | 1 TB   | 60      | 41    | 0     | 0.11   |
| ADATA     | SX8200PNP-512GT-S  | 512 GB | 1       | 41    | 0     | 0.11   |
| Samsung   | Portable SSD X5    | 500 GB | 1       | 41    | 0     | 0.11   |
| ADATA     | FALCON             | 256 GB | 2       | 41    | 0     | 0.11   |
| Intel     | 670p SSDPEKNU51... | 512 GB | 9       | 41    | 0     | 0.11   |
| KIOXIA    | KBG40ZNV1T02       | 1 TB   | 24      | 41    | 0     | 0.11   |
| Toshiba   | KBG40ZMT128G ME... | 128 GB | 13      | 41    | 0     | 0.11   |
| WDC       | PC SN530 SDBPTP... | 1 TB   | 12      | 40    | 0     | 0.11   |
| Goodram   | IR-SSDPR-P34B-2... | 256 GB | 1       | 40    | 0     | 0.11   |
| Corsair   | MP600 PRO LPX      | 1 TB   | 1       | 40    | 0     | 0.11   |
| Toshiba   | KXG60ZNV512G KI... | 512 GB | 11      | 40    | 0     | 0.11   |
| Kingston  | SNVS250G           | 250 GB | 27      | 42    | 2     | 0.11   |
| KIOXIA    | KXG70ZNV1T02 NVMe  | 1 TB   | 4       | 40    | 0     | 0.11   |
| WDC       | PC SN730 SDBQNT... | 256 GB | 56      | 40    | 0     | 0.11   |
| SK hynix  | BC711 HFM512GD3... | 512 GB | 22      | 39    | 0     | 0.11   |
| T-FORCE   | TM8FPZ001T         | 1 TB   | 3       | 39    | 0     | 0.11   |
| Silico... | MS10               | 1 TB   | 4       | 39    | 0     | 0.11   |
| Apple     | SSD AP0512M        | 500 GB | 19      | 39    | 0     | 0.11   |
| Apple     | SSD AP0512Q        | 500 GB | 2       | 39    | 0     | 0.11   |
| Samsung   | KUS020203M-B000    | 128 GB | 5       | 39    | 0     | 0.11   |
| Kingston  | SNVS1000G          | 1 TB   | 43      | 39    | 0     | 0.11   |
| Seagate   | FireCuda 510 SS... | 500 GB | 1       | 39    | 0     | 0.11   |
| KIOXIA    | KBG40ZNV512G       | 512 GB | 120     | 38    | 0     | 0.11   |
| Samsung   | PM981a NVMe        | 2 TB   | 23      | 38    | 0     | 0.11   |
| Phison    | MSI M480           | 1 TB   | 2       | 38    | 0     | 0.11   |
| ShiJi     | 1TB M.2-NVMe       | 1 TB   | 2       | 38    | 0     | 0.11   |
| ADATA     | SX8100NP           | 256 GB | 3       | 77    | 33    | 0.11   |
| Apple     | SSD AP1024J        | 1 TB   | 3       | 38    | 0     | 0.11   |
| Silico... | 1TB                | 1 TB   | 1       | 38    | 0     | 0.11   |
| Samsung   | SSD 970 EVO Plus   | 2 TB   | 285     | 39    | 1     | 0.10   |
| Samsung   | MZVLB1T0HBLR-000H1 | 1 TB   | 62      | 38    | 0     | 0.10   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 6       | 38    | 0     | 0.10   |
| SK hynix  | HFM512GDHTNG-8310A | 512 GB | 6       | 38    | 0     | 0.10   |
| SPCC      | M.2 PCIE SSD       | 2 TB   | 1       | 38    | 0     | 0.10   |
| SK hynix  | HFS512GD9TNG-L2A0A | 512 GB | 6       | 37    | 0     | 0.10   |
| Micron    | 2210_MTFDHBA1T0QFD | 1 TB   | 48      | 37    | 0     | 0.10   |
| SK hynix  | BC711 HFM256GD3... | 256 GB | 9       | 37    | 0     | 0.10   |
| Toshiba   | KBG4AZNV512G ME... | 512 GB | 3       | 37    | 0     | 0.10   |
| SSSTC     | CL1-8D256          | 256 GB | 13      | 37    | 0     | 0.10   |
| KIOXIA    | KXG70PN84T09 NVMe  | 4 TB   | 4       | 37    | 0     | 0.10   |
| Samsung   | PM991 NVMe         | 512 GB | 17      | 37    | 0     | 0.10   |
| Samsung   | MZVLQ256HAJD-000AC | 256 GB | 2       | 37    | 0     | 0.10   |
| Samsung   | PM971 NVMe         | 256 GB | 1       | 37    | 0     | 0.10   |
| Goodram   | SSDPR-PX500-512-80 | 512 GB | 10      | 40    | 1     | 0.10   |
| Team      | TM8FPD512G         | 512 GB | 4       | 36    | 0     | 0.10   |
| Fanxiang  | S500               | 1 TB   | 1       | 36    | 0     | 0.10   |
| Samsung   | MZVLQ1T0HALB-000H1 | 1 TB   | 22      | 36    | 0     | 0.10   |
| SK hynix  | SHPP41-2000GM      | 2 TB   | 13      | 36    | 0     | 0.10   |
| Toshiba   | KXG50PNV2T04 NV... | 2 TB   | 2       | 36    | 0     | 0.10   |
| SK hynix  | BC711 NVMe         | 1 TB   | 7       | 36    | 0     | 0.10   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 2       | 36    | 0     | 0.10   |
| Kingston  | SNVS500G           | 500 GB | 120     | 36    | 0     | 0.10   |
| Samsung   | MZQL2960HCJR-00A07 | 960 GB | 4       | 36    | 0     | 0.10   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 3       | 53    | 3     | 0.10   |
| WDC       | PC SN530 SDBPNP... | 1 TB   | 9       | 36    | 0     | 0.10   |
| SK hynix  | BC711 NVMe         | 128 GB | 25      | 36    | 0     | 0.10   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 9       | 36    | 0     | 0.10   |
| Samsung   | PM981a NVMe        | 256 GB | 5       | 36    | 0     | 0.10   |
| SanDisk   | WD Blue SN570 5... | 500 GB | 3       | 35    | 0     | 0.10   |
| Samsung   | MZVLB256HBHQ-00000 | 256 GB | 35      | 35    | 0     | 0.10   |
| SanDisk   | WD Blue SN570      | 500 GB | 42      | 35    | 0     | 0.10   |
| Lexar     | 250GB SSD          | 250 GB | 5       | 35    | 0     | 0.10   |
| UMIS      | RPFTJ128PDD2EWX    | 128 GB | 25      | 35    | 0     | 0.10   |
| Dell      | Ent NVMe AGN RI... | 3.8 TB | 1       | 35    | 0     | 0.10   |
| KIOXIA    | KXG70PNV2T04 NVMe  | 2 TB   | 13      | 35    | 0     | 0.10   |
| WDC       | PC SN520 SDAPMU... | 512 GB | 2       | 35    | 0     | 0.10   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 2       | 35    | 0     | 0.10   |
| Apacer    | AS2280P4U          | 1 TB   | 1       | 35    | 0     | 0.10   |
| SK hynix  | PC711 NVMe         | 256 GB | 6       | 35    | 0     | 0.10   |
| Silico... | KLLISRE            | 128 GB | 1       | 34    | 0     | 0.10   |
| Silico... | PCIe SSD           | 256 GB | 1       | 34    | 0     | 0.10   |
| Intel     | MEMPEK1W016GAL     | 16 GB  | 1       | 34    | 0     | 0.10   |
| Intel     | SSDPEKNU512GZH     | 512 GB | 28      | 34    | 0     | 0.10   |
| Seagate   | FireCuda 530 ZP... | 4 TB   | 3       | 34    | 0     | 0.09   |
| Phison    | C-E80T256G4-P3D... | 256 GB | 1       | 34    | 0     | 0.09   |
| WDC       | WDS384T1D0D-01AJB0 | 3.8 TB | 1       | 34    | 0     | 0.09   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 63      | 34    | 0     | 0.09   |
| UMIS      | RPETJ512MGE2QDQ    | 512 GB | 6       | 34    | 0     | 0.09   |
| SK hynix  | BC501 NVMe         | 128 GB | 13      | 34    | 0     | 0.09   |
| XPG       | GAMMIX S70 BLADE   | 2 TB   | 15      | 33    | 0     | 0.09   |
| Apple     | SSD SM0512L        | 500 GB | 12      | 38    | 85    | 0.09   |
| FORESEE   | P900F128GBH        | 128 GB | 2       | 33    | 0     | 0.09   |
| Phison    | Sabrent ROCKET-PRO | 512 GB | 1       | 33    | 0     | 0.09   |
| Kingston  | OM8PDP3512B-AA1    | 512 GB | 34      | 33    | 0     | 0.09   |
| Silico... | NVMe SSD           | 1 TB   | 1       | 33    | 0     | 0.09   |
| Crucial   | CT1000P5SSD8       | 1 TB   | 46      | 33    | 0     | 0.09   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 9       | 33    | 0     | 0.09   |
| SK hynix  | HFM128GDHTNG-8310B | 128 GB | 7       | 33    | 0     | 0.09   |
| Intel     | MEMPEK1J032GA      | 32 GB  | 1       | 33    | 0     | 0.09   |
| Gigaby... | GP-GSM2NE3512GNTD  | 512 GB | 6       | 33    | 0     | 0.09   |
| Kingston  | OM3PDP3-AD NVMe... | 256 GB | 16      | 33    | 0     | 0.09   |
| XPG       | SX8200PNP-512GT-S  | 512 GB | 3       | 33    | 0     | 0.09   |
| Kingston  | OM3PDP3256B-A01    | 256 GB | 2       | 33    | 0     | 0.09   |
| WDC       | PC SN730 SDBQNT... | 512 GB | 156     | 33    | 7     | 0.09   |
| Intel     | SSDPEKNU512GZ      | 512 GB | 112     | 32    | 0     | 0.09   |
| WDC       | PC SN720 SDAQNT... | 512 GB | 2       | 32    | 0     | 0.09   |
| SSSTC     | CL1-8D256-HP       | 256 GB | 17      | 32    | 0     | 0.09   |
| Smartbuy  | m.2 PS5013-2280T   | 128 GB | 2       | 32    | 0     | 0.09   |
| ADATA     | FALCON             | 2 TB   | 4       | 32    | 0     | 0.09   |
| Apple     | SSD SM0032L        | 32 GB  | 27      | 32    | 0     | 0.09   |
| Plextor   | PX-1TM10PG         | 1 TB   | 1       | 32    | 0     | 0.09   |
| Apple     | SSD AP2048M        | 2 TB   | 2       | 32    | 0     | 0.09   |
| Phison    | MSI M390           | 1 TB   | 4       | 32    | 0     | 0.09   |
| Lenovo    | LENSN20256GMSP3... | 256 GB | 2       | 32    | 0     | 0.09   |
| MSI       | M390               | 1 TB   | 1       | 32    | 0     | 0.09   |
| SK hynix  | PC711 HFS512GDE... | 512 GB | 9       | 32    | 0     | 0.09   |
| Samsung   | MZVLB512HBJQ-000L2 | 512 GB | 122     | 32    | 0     | 0.09   |
| WDC       | WDS200T2B0C-00PXH0 | 2 TB   | 18      | 32    | 0     | 0.09   |
| KIOXIA... | PLUS G2 SSD        | 500 GB | 8       | 32    | 0     | 0.09   |
| SanDisk   | WD_BLACK SN850 ... | 1 TB   | 1       | 32    | 0     | 0.09   |
| Seagate   | BarraCuda Q5 ZP... | 2 TB   | 1       | 32    | 0     | 0.09   |
| Phison    | Sabrent Rocket ... | 8 TB   | 1       | 31    | 0     | 0.09   |
| ADATA     | FALCON             | 512 GB | 5       | 31    | 0     | 0.09   |
| Intel     | HBRPEKNL0202AHO    | 32 GB  | 1       | 31    | 0     | 0.09   |
| Intel     | HBRPEKNL0202AH     | 512 GB | 1       | 31    | 0     | 0.09   |
| Intel     | SSDPEKKA128G8      | 128 GB | 2       | 31    | 0     | 0.09   |
| Team      | TM8FP6001T         | 1 TB   | 12      | 31    | 0     | 0.09   |
| SanDisk   | WD_BLACK SN750 SE  | 250 GB | 6       | 31    | 0     | 0.09   |
| Apple     | SSD AP8192N        | 8 TB   | 2       | 31    | 0     | 0.09   |
| Intel     | SSDPEKNU020TZ      | 2 TB   | 4       | 31    | 0     | 0.09   |
| Phison    | APS-SE20G-1T       | 1 TB   | 1       | 31    | 0     | 0.09   |
| Samsung   | MZVLB256HAHQ-00007 | 256 GB | 2       | 31    | 0     | 0.09   |
| UMIS      | LENSE40256GMSP3... | 256 GB | 2       | 31    | 0     | 0.09   |
| Samsung   | MZVL2512HCJQ-00B   | 512 GB | 1       | 31    | 0     | 0.09   |
| HUAWEI    | HWE52P433T2M005N   | 3.2 TB | 4       | 31    | 0     | 0.09   |
| Samsung   | KLFGGAR4AA-K0T0    | 1 TB   | 1       | 31    | 0     | 0.09   |
| WDC       | CL SN520 SDAPMU... | 512 GB | 1       | 30    | 0     | 0.08   |
| Apple     | SSD SM0256L        | 256 GB | 16      | 30    | 0     | 0.08   |
| Silico... | PCS M.2 NVME SSD   | 512 GB | 1       | 30    | 0     | 0.08   |
| Micron    | MTFDHBA256TCK-1... | 256 GB | 38      | 31    | 1     | 0.08   |
| WDC       | PC SN730 SDBPNT... | 256 GB | 12      | 30    | 0     | 0.08   |
| WDC       | PC SN720 SDAQNT... | 1 TB   | 3       | 30    | 0     | 0.08   |
| SK hynix  | BC501 NVMe         | 512 GB | 9       | 30    | 0     | 0.08   |
| WDC       | PC SN520 SDAPMU... | 512 GB | 9       | 33    | 9     | 0.08   |
| ADATA     | SX6000PNP          | 1 TB   | 15      | 33    | 42    | 0.08   |
| WDC       | PC SN530 SDBPTP... | 512 GB | 10      | 30    | 0     | 0.08   |
| UMIS      | RPETJ256MGE2MDQ    | 256 GB | 3       | 30    | 0     | 0.08   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 55      | 30    | 0     | 0.08   |
| UMIS      | RPFTJ256PDD2MWX    | 256 GB | 20      | 29    | 0     | 0.08   |
| SanDisk   | WD Blue SN570 1... | 1 TB   | 6       | 29    | 0     | 0.08   |
| SK hynix  | HFM256GDJTNG-8310A | 256 GB | 67      | 33    | 1     | 0.08   |
| Corsair   | MP600 PRO LPX      | 500 GB | 1       | 29    | 0     | 0.08   |
| WDC       | PC SN730 SDBQNT... | 1 TB   | 67      | 29    | 0     | 0.08   |
| KIOXIA    | KXG60ZNV256G NVMe  | 256 GB | 5       | 28    | 0     | 0.08   |
| Silico... | JAMESDONKEY JD512  | 512 GB | 1       | 28    | 0     | 0.08   |
| SK hynix  | HFM512GDJTNG-8310A | 512 GB | 44      | 28    | 1     | 0.08   |
| Phison    | Reletech P400 SSD  | 512 GB | 3       | 28    | 0     | 0.08   |
| YMTC      | PC005              | 512 GB | 27      | 28    | 0     | 0.08   |
| Toshiba   | KXG60ZNV512G NV... | 512 GB | 18      | 28    | 0     | 0.08   |
| Samsung   | MZVLB1T0HBLR-00007 | 1 TB   | 6       | 28    | 0     | 0.08   |
| Seagate   | FireCuda 530 ZP... | 1 TB   | 2       | 28    | 0     | 0.08   |
| WDC       | PC SN530 SDBPNP... | 1 TB   | 11      | 28    | 0     | 0.08   |
| KingFast  | 1TB                | 1 TB   | 2       | 27    | 0     | 0.08   |
| Silico... | PCIe-8 SSD         | 512 GB | 21      | 27    | 0     | 0.08   |
| SK hynix  | HFM256GD3JX016N    | 256 GB | 7       | 27    | 0     | 0.07   |
| Samsung   | MZVLB256HBHQ-00007 | 256 GB | 3       | 27    | 0     | 0.07   |
| WDC       | PC SN730 NVMe      | 1 TB   | 59      | 27    | 0     | 0.07   |
| Samsung   | SSD 980 PRO        | 500 GB | 133     | 27    | 1     | 0.07   |
| ADATA     | IM2P33F8BR2-1TB    | 1 TB   | 2       | 27    | 0     | 0.07   |
| WDC       | WDS250G2B0C        | 250 GB | 3       | 27    | 0     | 0.07   |
| Samsung   | MZVLB1T0HBLR-000L2 | 1 TB   | 125     | 27    | 0     | 0.07   |
| Apple     | SSD SM0128L        | 121 GB | 6       | 26    | 0     | 0.07   |
| Lite-On   | CA5-8D512          | 512 GB | 11      | 26    | 0     | 0.07   |
| Micron    | MTFDHBA512QFD      | 512 GB | 67      | 26    | 0     | 0.07   |
| Toshiba   | KXG60ZNV256G KI... | 256 GB | 8       | 26    | 0     | 0.07   |
| Phison    | 512GB NVMe SSD     | 512 GB | 3       | 26    | 0     | 0.07   |
| Samsung   | MZVL21T0HCLR-00BTW | 1 TB   | 2       | 26    | 0     | 0.07   |
| SK hynix  | BC511 NVMe         | 256 GB | 55      | 26    | 0     | 0.07   |
| ADATA     | SX6000LNP          | 128 GB | 22      | 25    | 0     | 0.07   |
| Samsung   | MZVPW256HEGL-000L7 | 256 GB | 1       | 25    | 0     | 0.07   |
| Phison    | E12-512G-PHISON... | 512 GB | 2       | 25    | 0     | 0.07   |
| Kingston  | SKC3000D4096G      | 4 TB   | 2       | 25    | 0     | 0.07   |
| Kingston  | OM8PDP3512B-AI1    | 512 GB | 4       | 25    | 0     | 0.07   |
| WDC       | PC SN730 SDBPNT... | 256 GB | 3       | 25    | 0     | 0.07   |
| Samsung   | SSD 980 PRO        | 250 GB | 38      | 26    | 5     | 0.07   |
| Micron    | 2450_MTFDKBA1T0TFK | 1 TB   | 38      | 25    | 0     | 0.07   |
| PNY       | CS2130 4TB SSD     | 4 TB   | 1       | 25    | 0     | 0.07   |
| Apple     | SSD AP0512H        | 500 GB | 2       | 25    | 0     | 0.07   |
| Samsung   | MZALQ256HAJD-000L1 | 256 GB | 39      | 25    | 0     | 0.07   |
| Phison    | NE-256             | 256 GB | 3       | 25    | 0     | 0.07   |
| Samsung   | MZVLB1T0HBLR-000L7 | 1 TB   | 120     | 25    | 0     | 0.07   |
| Samsung   | MZVLB256HBHQ-000H1 | 256 GB | 11      | 25    | 0     | 0.07   |
| WDC       | PC SN520 SDAPMU... | 128 GB | 12      | 25    | 0     | 0.07   |
| Toshiba   | KBG30ZMV256G KI... | 256 GB | 17      | 25    | 0     | 0.07   |
| Netac     | NVMe SSD           | 128 GB | 3       | 25    | 0     | 0.07   |
| Silico... | 512GB PCS PCIe ... | 512 GB | 3       | 25    | 0     | 0.07   |
| Samsung   | MZVLQ256HAJD-000H1 | 256 GB | 84      | 25    | 0     | 0.07   |
| Lite-On   | CL1-8D256          | 256 GB | 1       | 25    | 0     | 0.07   |
| Intel     | SSDPEKNU010TZH     | 1 TB   | 2       | 24    | 0     | 0.07   |
| Inland    | NVMe SSD           | 1 TB   | 3       | 26    | 23    | 0.07   |
| WDC       | WDS500G1XHE-00AFY0 | 500 GB | 1       | 24    | 0     | 0.07   |
| Union ... | UMIS LENSE40512... | 512 GB | 1       | 24    | 0     | 0.07   |
| Lite-On   | CA1-8D128-HP       | 128 GB | 7       | 25    | 38    | 0.07   |
| KIOXIA    | KBG40ZNS1T02 NVMe  | 1 TB   | 8       | 24    | 0     | 0.07   |
| SK hynix  | SHGP31-2000GM      | 2 TB   | 4       | 24    | 0     | 0.07   |
| Silico... | ShiJi 512GB M.2... | 512 GB | 1       | 24    | 0     | 0.07   |
| ADATA     | SX6000LNP          | 1 TB   | 10      | 45    | 101   | 0.07   |
| Samsung   | MZVLQ1T0HALB-00000 | 1 TB   | 19      | 23    | 0     | 0.07   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 24      | 23    | 0     | 0.06   |
| Samsung   | MZVLQ512HALU-00000 | 512 GB | 90      | 23    | 0     | 0.06   |
| Lite-On   | CA5-8D256          | 256 GB | 1       | 23    | 0     | 0.06   |
| Phison    | PM8512GPTCB4B8T... | 512 GB | 2       | 23    | 0     | 0.06   |
| Samsung   | MZVLB512HBJQ-00A00 | 512 GB | 7       | 23    | 0     | 0.06   |
| Kimtigo   | SSD                | 256 GB | 4       | 23    | 0     | 0.06   |
| WDC       | PC SN530 SDBPMP... | 512 GB | 103     | 23    | 0     | 0.06   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 16      | 23    | 0     | 0.06   |
| WDC       | PC SN540 SDDPNP... | 1 TB   | 4       | 22    | 0     | 0.06   |
| Samsung   | PM981a NVMe        | 512 GB | 33      | 22    | 0     | 0.06   |
| KLEVV     | CRAS C710 M.2 N... | 1 TB   | 1       | 22    | 0     | 0.06   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 75      | 22    | 0     | 0.06   |
| Micron    | 2200_MTFDHBA512TCK | 512 GB | 11      | 22    | 0     | 0.06   |
| Kingston  | RBUSNS8154P3512GJ3 | 512 GB | 3       | 22    | 0     | 0.06   |
| Samsung   | SSD 970 EVO        | 2 TB   | 14      | 143   | 42    | 0.06   |
| Gigabyte  | GP-GSM2NE3256GNTD  | 256 GB | 18      | 22    | 0     | 0.06   |
| Hikvision | HS-SSD-E3000 512G  | 512 GB | 1       | 22    | 0     | 0.06   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 60      | 22    | 0     | 0.06   |
| SSSTC     | CL1-4D128          | 128 GB | 6       | 22    | 0     | 0.06   |
| Kingston  | RBUSNS8154P3256GJ1 | 256 GB | 44      | 22    | 0     | 0.06   |
| Samsung   | MZALQ512HALU-000L2 | 512 GB | 167     | 22    | 0     | 0.06   |
| Kingston  | SKC3000S1024G      | 1 TB   | 18      | 22    | 0     | 0.06   |
| Silico... | Maxsun 256GB NM... | 256 GB | 2       | 22    | 0     | 0.06   |
| Samsung   | MZALQ256HAJD-000L2 | 256 GB | 111     | 22    | 0     | 0.06   |
| KIOXIA    | KBG30ZMV512G       | 512 GB | 5       | 22    | 0     | 0.06   |
| Samsung   | MZVLQ512HALU-000H1 | 512 GB | 123     | 22    | 0     | 0.06   |
| Samsung   | MZVL21T0HCLR-00B00 | 1 TB   | 65      | 22    | 2     | 0.06   |
| ADATA     | LEGEND 750         | 1 TB   | 1       | 21    | 0     | 0.06   |
| Silico... | IM2P33F8BR1-512GB  | 512 GB | 2       | 21    | 0     | 0.06   |
| Samsung   | MZVLB512HBJQ-000L7 | 512 GB | 304     | 21    | 0     | 0.06   |
| Micron    | 2450 NVMe          | 256 GB | 2       | 21    | 0     | 0.06   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 69      | 21    | 0     | 0.06   |
| Patriot   | M.2 P310           | 240 GB | 1       | 21    | 0     | 0.06   |
| SSSTC     | CL1-8D512-HP       | 512 GB | 2       | 21    | 0     | 0.06   |
| Samsung   | MZVLB256HBHQ-000L7 | 256 GB | 84      | 21    | 0     | 0.06   |
| SK hynix  | BC511 NVMe         | 512 GB | 70      | 21    | 0     | 0.06   |
| ADATA     | SWORDFISH          | 1 TB   | 20      | 23    | 51    | 0.06   |
| Samsung   | SSD 980 PRO        | 1 TB   | 350     | 22    | 1     | 0.06   |
| Intel     | SSDPEBKF256G7      | 256 GB | 1       | 21    | 0     | 0.06   |
| Silico... | R5MP240G8          | 240 GB | 2       | 21    | 0     | 0.06   |
| Team      | TM8FP6128G         | 128 GB | 3       | 20    | 0     | 0.06   |
| Micron    | 2300 NVMe          | 1 TB   | 61      | 20    | 0     | 0.06   |
| Samsung   | MZVLQ1T0HBLB-00B00 | 1 TB   | 29      | 20    | 0     | 0.06   |
| Star D... | PCIe SSD           | 480 GB | 13      | 20    | 0     | 0.06   |
| XPG       | GAMMIX S11L        | 1 TB   | 4       | 20    | 0     | 0.06   |
| SK hynix  | Skhynix BC501 NVMe | 512 GB | 4       | 20    | 0     | 0.06   |
| Phison    | ThinkPlus ST800... | 256 GB | 1       | 20    | 0     | 0.06   |
| SK hynix  | SKHynix_HFM512G... | 512 GB | 57      | 20    | 0     | 0.06   |
| ADATA     | SX8100NP           | 4 TB   | 1       | 102   | 4     | 0.06   |
| Seagate   | IronWolf510 ZP9... | 960 GB | 3       | 20    | 0     | 0.06   |
| Solid ... | SSSTC CL1-8D512    | 512 GB | 1       | 20    | 0     | 0.06   |
| Samsung   | MZFLW512HMJP-000MV | 512 GB | 1       | 20    | 0     | 0.06   |
| Apple     | SSD AP0512J        | 500 GB | 9       | 20    | 0     | 0.06   |
| Crucial   | CT1000P3PSSD8      | 1 TB   | 4       | 20    | 0     | 0.06   |
| WDC       | WDS100T1XHE-00AFY0 | 1 TB   | 5       | 20    | 0     | 0.05   |
| Samsung   | SSD 980            | 500 GB | 153     | 19    | 0     | 0.05   |
| SanDisk   | WD_BLACK SN850X HS | 1 TB   | 3       | 19    | 0     | 0.05   |
| OSCOO     | OSC PCIE           | 512 GB | 1       | 19    | 0     | 0.05   |
| Phison    | DTGC-CP            | 256 GB | 1       | 19    | 0     | 0.05   |
| Silico... | OSC PCIE           | 512 GB | 1       | 19    | 0     | 0.05   |
| SK hynix  | VO003840KXAVQ      | 3.8 TB | 1       | 19    | 0     | 0.05   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 44      | 19    | 0     | 0.05   |
| Timetec   | 35TTFP6PCIE-1TB    | 1 TB   | 2       | 19    | 0     | 0.05   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 31      | 19    | 0     | 0.05   |
| ADATA     | SWORDFISH          | 500 GB | 4       | 19    | 0     | 0.05   |
| HP        | SSD EX900          | 120 GB | 3       | 19    | 0     | 0.05   |
| Seagate   | XP800HE30012       | 800 GB | 1       | 19    | 0     | 0.05   |
| Apple     | SSD AP0256M        | 256 GB | 10      | 19    | 0     | 0.05   |
| Kingston  | SFYRD2000G         | 2 TB   | 6       | 19    | 0     | 0.05   |
| Union ... | RPFTJ128PDD2EWX    | 128 GB | 25      | 19    | 0     | 0.05   |
| Micron    | 3400 NVMe          | 1 TB   | 7       | 19    | 0     | 0.05   |
| Silico... | SPT256L2-2IAS7G2   | 256 GB | 4       | 19    | 0     | 0.05   |
| Samsung   | 980 PRO with He... | 2 TB   | 7       | 19    | 0     | 0.05   |
| Kingston  | SKC2500M8250G      | 250 GB | 9       | 19    | 0     | 0.05   |
| SSSTC     | CL4-3D256-Q11 NVMe | 256 GB | 1       | 19    | 0     | 0.05   |
| SK hynix  | PC601 SED NVMe     | 512 GB | 5       | 18    | 0     | 0.05   |
| Silico... | NVMe SSD 256G      | 256 GB | 1       | 18    | 0     | 0.05   |
| KIOXIA... | G2 SSD             | 1 TB   | 10      | 18    | 0     | 0.05   |
| Lite-On   | CL1-3D256-Q11 NVMe | 256 GB | 4       | 18    | 0     | 0.05   |
| Union ... | RPFTJ256PDD2MWX    | 256 GB | 13      | 18    | 0     | 0.05   |
| SSSTC     | CA5-8D512-Q79      | 512 GB | 1       | 18    | 0     | 0.05   |
| Crucial   | CT250P5SSD8        | 250 GB | 6       | 18    | 0     | 0.05   |
| Apple     | SSD AP0256N        | 256 GB | 4       | 18    | 0     | 0.05   |
| Apple     | SSD AP0032H        | 24 GB  | 3       | 18    | 0     | 0.05   |
| SK hynix  | HFM256GDHTNG-8510B | 256 GB | 13      | 18    | 0     | 0.05   |
| SK hynix  | HFM512GDJTNI-82A0A | 512 GB | 50      | 18    | 0     | 0.05   |
| SK hynix  | HFM001TD3JX016N    | 1 TB   | 1       | 18    | 0     | 0.05   |
| Phytium   | S1200CYX1-T0M22... | 256 GB | 1       | 18    | 0     | 0.05   |
| Silico... | ASint AS806        | 512 GB | 1       | 18    | 0     | 0.05   |
| WDC       | WDBRPG0020BNC-WRSN | 2 TB   | 1       | 18    | 0     | 0.05   |
| Silico... | SSD_M.2_PCI_NVM... | 1 TB   | 3       | 18    | 0     | 0.05   |
| SK hynix  | BC501 HFM512GDJ... | 512 GB | 30      | 17    | 0     | 0.05   |
| ADATA     | IM2P33F3A NVMe     | 512 GB | 28      | 17    | 4     | 0.05   |
| Apple     | SSD AP0256J        | 256 GB | 23      | 17    | 0     | 0.05   |
| SK hynix  | BC511 HFM256GDJ... | 256 GB | 67      | 17    | 0     | 0.05   |
| Kingston  | SKC3000S512G       | 512 GB | 5       | 17    | 0     | 0.05   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 70      | 17    | 0     | 0.05   |
| Corsair   | MP600 CORE         | 2 TB   | 5       | 17    | 0     | 0.05   |
| SK hynix  | SKHynix_HFS001T... | 1 TB   | 20      | 17    | 0     | 0.05   |
| Samsung   | MZVLB512HBJQ-00007 | 512 GB | 5       | 17    | 0     | 0.05   |
| SK hynix  | Skhynix BC501 NVMe | 128 GB | 2       | 17    | 0     | 0.05   |
| Transcend | TS256GMTE652T-I    | 256 GB | 1       | 17    | 0     | 0.05   |
| SanDisk   | SN520 SDAPNUW-2... | 256 GB | 2       | 17    | 0     | 0.05   |
| SK hynix  | BC501A NVMe        | 128 GB | 12      | 17    | 0     | 0.05   |
| ADATA     | IM2P32A8-128GCTB5  | 128 GB | 1       | 17    | 0     | 0.05   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 13      | 17    | 0     | 0.05   |
| Union ... | UMIS RPJTJ512ME... | 512 GB | 10      | 17    | 0     | 0.05   |
| WDC       | PC SN530 NVMe      | 256 GB | 42      | 17    | 0     | 0.05   |
| WDC       | PC SN530 NVMe      | 512 GB | 48      | 17    | 0     | 0.05   |
| Kingston  | SFYRS1000G         | 1 TB   | 17      | 17    | 0     | 0.05   |
| Micron    | MTFDHBA256TCK      | 256 GB | 8       | 19    | 28    | 0.05   |
| SMI       | 2263XT             | 120 GB | 2       | 17    | 0     | 0.05   |
| Silico... | 256GB              | 256 GB | 10      | 17    | 0     | 0.05   |
| KIOXIA    | KBG50ZNS512G NVMe  | 512 GB | 8       | 17    | 0     | 0.05   |
| Lenovo    | RPITJ256VFD2MWX    | 256 GB | 1       | 17    | 0     | 0.05   |
| Patriot   | M.2 P300           | 128 GB | 4       | 17    | 0     | 0.05   |
| Union ... | UMIS RPJTJ1TBME... | 1 TB   | 1       | 17    | 0     | 0.05   |
| Phison    | One-Netbook PCI... | 512 GB | 4       | 16    | 0     | 0.05   |
| ADATA     | IM2P33F8BR2-512GB  | 512 GB | 6       | 16    | 0     | 0.05   |
| Intel     | SSDPEKNW512GZL     | 512 GB | 22      | 16    | 0     | 0.05   |
| SK hynix  | BC511 HFM512GDJ... | 512 GB | 51      | 16    | 0     | 0.05   |
| UMIS      | RPETJ1T24MGE2QDQ   | 1 TB   | 3       | 16    | 0     | 0.05   |
| Samsung   | MZVL2512HCJQ-00BL7 | 512 GB | 19      | 16    | 0     | 0.05   |
| Crucial   | CT2000P5SSD8       | 2 TB   | 15      | 16    | 0     | 0.05   |
| SK hynix  | HFM256GDJTNI-82A0A | 256 GB | 20      | 16    | 0     | 0.05   |
| KIOXIA    | KBG50ZNT512G LS    | 512 GB | 12      | 16    | 0     | 0.05   |
| Toshiba   | KBG40ZNV256G ME... | 256 GB | 4       | 16    | 0     | 0.04   |
| Apple     | SSD AP0512N        | 500 GB | 30      | 16    | 0     | 0.04   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 2       | 16    | 0     | 0.04   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 4       | 16    | 0     | 0.04   |
| Samsung   | MZALQ512HALU-000L1 | 512 GB | 80      | 16    | 0     | 0.04   |
| Samsung   | MZALQ128HBHQ-000L2 | 128 GB | 33      | 16    | 0     | 0.04   |
| Colorful  | CN600S             | 480 GB | 1       | 16    | 0     | 0.04   |
| imation   | M.2 PCIe 1TB SS... | 1 TB   | 1       | 16    | 0     | 0.04   |
| WALRAM    | 256GB              | 256 GB | 1       | 16    | 0     | 0.04   |
| SK hynix  | HFB1M8MQ331C0MR    | 128 GB | 6       | 16    | 0     | 0.04   |
| Samsung   | PM991a NVMe        | 256 GB | 23      | 16    | 0     | 0.04   |
| SK hynix  | SKHynix_HFM128G... | 128 GB | 7       | 16    | 0     | 0.04   |
| Micron    | MTFDHBA256TDV      | 256 GB | 9       | 16    | 0     | 0.04   |
| Team      | TM8FPD002T         | 2 TB   | 1       | 16    | 0     | 0.04   |
| SanDisk   | WD_BLACK SN770     | 2 TB   | 10      | 16    | 0     | 0.04   |
| Micron    | 7300_MTFDHBA480TDF | 480 GB | 1       | 16    | 0     | 0.04   |
| WDC       | PC SN730 SDBQNT... | 512 GB | 2       | 15    | 0     | 0.04   |
| Lite-On   | CL1-8D256-HP       | 256 GB | 1       | 15    | 0     | 0.04   |
| Micron    | MTFDHBA512QFD-1... | 512 GB | 28      | 15    | 0     | 0.04   |
| Phison    | ESMP128GTB3C2-E8   | 128 GB | 1       | 15    | 0     | 0.04   |
| Samsung   | MZVL2512HCJQ-00BH1 | 512 GB | 10      | 15    | 0     | 0.04   |
| Kingston  | OM3PDP3-AD NVMe... | 512 GB | 23      | 15    | 0     | 0.04   |
| Samsung   | MZVLB1T0HBLR-00A00 | 1 TB   | 9       | 15    | 0     | 0.04   |
| Toshiba   | KBG20ZMS128G NVMe  | 128 GB | 1       | 15    | 0     | 0.04   |
| Fanxiang  | S500PRO            | 1 TB   | 3       | 15    | 0     | 0.04   |
| Apple     | SSD AP1024N        | 1 TB   | 18      | 15    | 0     | 0.04   |
| SK hynix  | HFM256GDGTNG-87A0A | 256 GB | 6       | 15    | 0     | 0.04   |
| Micron    | MTFDHBA1T0TCK      | 1 TB   | 8       | 15    | 0     | 0.04   |
| SK hynix  | BA HFS512GD9TNG... | 512 GB | 1       | 15    | 0     | 0.04   |
| Apple     | SSD AP0256H        | 256 GB | 1       | 15    | 0     | 0.04   |
| Samsung   | MZVLB512HBJQ-000   | 512 GB | 9       | 15    | 0     | 0.04   |
| Samsung   | SSD 980 PRO        | 2 TB   | 149     | 20    | 19    | 0.04   |
| SanDisk   | WD_BLACK SN770     | 1 TB   | 29      | 15    | 0     | 0.04   |
| Samsung   | MZVLB512HBJQ-000H7 | 512 GB | 9       | 15    | 0     | 0.04   |
| Samsung   | PM9A1 NVMe         | 512 GB | 60      | 15    | 0     | 0.04   |
| Micron    | 2200_MTFDHBA256TCK | 256 GB | 11      | 14    | 0     | 0.04   |
| Samsung   | MZVLQ512HBLU-00B00 | 512 GB | 45      | 14    | 0     | 0.04   |
| Samsung   | MZALQ128HBHQ-000L1 | 128 GB | 9       | 14    | 0     | 0.04   |
| Silico... | 512GB              | 512 GB | 7       | 14    | 0     | 0.04   |
| Samsung   | SSD 980            | 1 TB   | 252     | 16    | 3     | 0.04   |
| Samsung   | MZVL22T0HBLB-00BH1 | 2 TB   | 1       | 14    | 0     | 0.04   |
| SanDisk   | WD PC SN740 SDD... | 512 GB | 1       | 14    | 0     | 0.04   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 3       | 14    | 0     | 0.04   |
| Apple     | SSD AP2048R        | 2 TB   | 1       | 14    | 0     | 0.04   |
| V-GeN     | V-GEN11SM20AR51... | 512 GB | 1       | 14    | 0     | 0.04   |
| Lexar     | SSD NM620          | 512 GB | 2       | 14    | 0     | 0.04   |
| PNY       | CS1030 2TB SSD     | 2 TB   | 2       | 14    | 0     | 0.04   |
| Micron    | 2200_MTFDHBA1T0TCK | 1 TB   | 7       | 14    | 0     | 0.04   |
| T-FORCE   | TM8FPL1000G        | 1 TB   | 1       | 14    | 0     | 0.04   |
| OEM       | Genuine            | 1 TB   | 3       | 14    | 0     | 0.04   |
| Seagate   | BarraCuda 510 S... | 512 GB | 2       | 14    | 0     | 0.04   |
| WALRAM    | 256G               | 256 GB | 1       | 13    | 0     | 0.04   |
| SK hynix  | SKHynix_HFM256G... | 256 GB | 45      | 13    | 0     | 0.04   |
| Micron    | 2450_MTFDKBK512TFK | 512 GB | 1       | 13    | 0     | 0.04   |
| Phison    | 311CD0512GB        | 512 GB | 89      | 13    | 1     | 0.04   |
| Samsung   | MZVLQ512HBLU-00BTW | 512 GB | 11      | 13    | 0     | 0.04   |
| SK hynix  | HFM512GDHTNG-8710B | 512 GB | 32      | 13    | 0     | 0.04   |
| Hikvision | HS-SSD-E3000 1024G | 1 TB   | 3       | 13    | 0     | 0.04   |
| SK hynix  | HFM128GDJTNG-8310A | 128 GB | 26      | 13    | 0     | 0.04   |
| Kingston  | RBUSNS8154P3128GJ1 | 128 GB | 12      | 13    | 0     | 0.04   |
| Samsung   | MZVLB256HBHQ-00A00 | 256 GB | 2       | 13    | 0     | 0.04   |
| Crucial   | CT500P3PSSD8       | 500 GB | 3       | 13    | 0     | 0.04   |
| Samsung   | PM9A1 NVMe         | 1 TB   | 46      | 13    | 1     | 0.04   |
| Gigabyte  | AG4512G-SI B10     | 512 GB | 3       | 13    | 0     | 0.04   |
| SSSTC     | CA5-8D512          | 512 GB | 6       | 13    | 0     | 0.04   |
| Silico... | PCIe-4 SSD         | 512 GB | 3       | 13    | 0     | 0.04   |
| KIOXIA    | KBG50ZNV512G       | 512 GB | 11      | 13    | 0     | 0.04   |
| WDC       | PC SN730 SDBQNT... | 512 GB | 3       | 13    | 0     | 0.04   |
| YMTC      | PC005              | 256 GB | 5       | 13    | 0     | 0.04   |
| Silico... | Longline SSD       | 512 GB | 1       | 13    | 0     | 0.04   |
| SK hynix  | HFM128GDGTNG-87A0A | 128 GB | 7       | 13    | 0     | 0.04   |
| BIWIN     | SSD                | 512 GB | 9       | 13    | 0     | 0.04   |
| Patriot   | M.2 P300           | 256 GB | 6       | 13    | 0     | 0.04   |
| KIOXIA    | KBG50ZNS1T02 NVMe  | 1 TB   | 1       | 13    | 0     | 0.04   |
| Phison    | 511BS0256GB        | 256 GB | 3       | 13    | 0     | 0.04   |
| SK hynix  | HFB1M8MH331C0MR    | 512 GB | 1       | 12    | 0     | 0.04   |
| WDC       | WDS960G2G0C-00AJM0 | 960 GB | 3       | 12    | 0     | 0.04   |
| SK hynix  | SHPP41-1000GM      | 1 TB   | 2       | 12    | 0     | 0.03   |
| Kingston  | OM8PDP3256B-AA1    | 256 GB | 10      | 12    | 0     | 0.03   |
| Samsung   | MZVLB2T0HALB-000L2 | 2 TB   | 2       | 12    | 0     | 0.03   |
| SanDisk   | WD_BLACK SN750 SE  | 500 GB | 13      | 12    | 0     | 0.03   |
| Kingmax   | PCIe SSD           | 256 GB | 1       | 12    | 0     | 0.03   |
| WDC       | WDS240G2G0C-00AJM0 | 240 GB | 10      | 12    | 0     | 0.03   |
| WDC       | PC SN530 SDBPMP... | 256 GB | 52      | 12    | 0     | 0.03   |
| SK hynix  | HFM512GDGTNG-87A0A | 512 GB | 6       | 12    | 0     | 0.03   |
| WDC       | PC SN530 SDBPNP... | 1 TB   | 1       | 12    | 0     | 0.03   |
| WDC       | PC SN530 SDBPMP... | 512 GB | 27      | 12    | 0     | 0.03   |
| ADATA     | SX8200PNP-512GT    | 512 GB | 1       | 12    | 0     | 0.03   |
| Phison    | HYPERPC-SSD2000... | 2 TB   | 1       | 12    | 0     | 0.03   |
| Micron    | 9200_MTFDHAL1T9TCT | 1.9 TB | 1       | 305   | 24    | 0.03   |
| Samsung   | PM991a NVMe        | 512 GB | 35      | 12    | 0     | 0.03   |
| Kingston  | SNV2S500G          | 500 GB | 9       | 12    | 0     | 0.03   |
| KIOXIA    | KBG4AZNV512G       | 512 GB | 2       | 12    | 0     | 0.03   |
| Samsung   | MZWLJ1T9HBJR-00007 | 1.9 TB | 1       | 11    | 0     | 0.03   |
| PNY       | CS3040 2TB SSD     | 2 TB   | 3       | 11    | 0     | 0.03   |
| Samsung   | MZVL21T0HCLR-00BL2 | 1 TB   | 18      | 11    | 0     | 0.03   |
| PNY       | CS2140 500GB SSD   | 500 GB | 2       | 11    | 0     | 0.03   |
| WDC       | PC SN810 NVMe      | 2 TB   | 1       | 11    | 0     | 0.03   |
| Micron    | MTFDKBA256TFK      | 256 GB | 3       | 11    | 0     | 0.03   |
| SSSTC     | LJ1-2W7680         | 962 GB | 1       | 11    | 0     | 0.03   |
| Micron    | 2210S NVMe         | 512 GB | 4       | 11    | 0     | 0.03   |
| Micron    | 2450_MTFDKBK1T0TFK | 1 TB   | 3       | 11    | 0     | 0.03   |
| UMIS      | RPJTJ512MGE1QDQ    | 512 GB | 18      | 11    | 0     | 0.03   |
| Samsung   | MZAL4512HBLU-00BL2 | 512 GB | 5       | 11    | 0     | 0.03   |
| SanDisk   | WD Blue SN570      | 250 GB | 3       | 11    | 0     | 0.03   |
| Plextor   | PX-256M9PGN +      | 256 GB | 1       | 11    | 0     | 0.03   |
| WDC       | CL SN720 SDAQNT... | 1 TB   | 1       | 11    | 0     | 0.03   |
| Seagate   | FireCuda 530 ZP... | 1 TB   | 8       | 11    | 0     | 0.03   |
| KIOXIA    | KBG5AZNV1T02 LA    | 1 TB   | 3       | 11    | 0     | 0.03   |
| Solid ... | SSSTC CL1-4D256    | 256 GB | 3       | 11    | 0     | 0.03   |
| Solid ... | SSSTC CL1-8D256-HP | 256 GB | 2       | 11    | 0     | 0.03   |
| Kingston  | SKC3000D2048G      | 2 TB   | 12      | 10    | 0     | 0.03   |
| Silico... | Qunion P20A 512... | 512 GB | 1       | 10    | 0     | 0.03   |
| ADATA     | IM2P33F3 NVMe      | 128 GB | 1       | 10    | 0     | 0.03   |
| Samsung   | MZVLQ256HAJD-000   | 256 GB | 2       | 10    | 0     | 0.03   |
| Micron    | 2450_MTFDKBA512TFK | 512 GB | 39      | 10    | 0     | 0.03   |
| ADATA     | IM2P33F3A NVMe     | 256 GB | 39      | 15    | 48    | 0.03   |
| UDinfo    | M2P                | 512 GB | 1       | 10    | 0     | 0.03   |
| SSSTC     | CA6-8D2048-Q11 ... | 2 TB   | 6       | 10    | 0     | 0.03   |
| Micron    | MTFDKBA512TFK-1... | 512 GB | 3       | 10    | 0     | 0.03   |
| Apple     | SSD AP0128H        | 121 GB | 81      | 10    | 0     | 0.03   |
| Micron    | 2300 NVMe          | 512 GB | 45      | 10    | 1     | 0.03   |
| ExeGate   | EX282322RUS(512GB) | 512 GB | 1       | 10    | 0     | 0.03   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 32      | 10    | 0     | 0.03   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 2       | 10    | 0     | 0.03   |
| Samsung   | MZVLQ512HALU-000AC | 512 GB | 2       | 10    | 0     | 0.03   |
| SSSTC     | CL1-3D128-Q11 NVMe | 128 GB | 17      | 10    | 0     | 0.03   |
| SK hynix  | PC801 NVMe         | 1 TB   | 19      | 10    | 0     | 0.03   |
| Micron    | 2300_MTFDHBA256TDV | 256 GB | 2       | 9     | 0     | 0.03   |
| FORESEE   | VP1000F256G        | 256 GB | 3       | 9     | 0     | 0.03   |
| Micron    | MTFDHBA512TDV      | 512 GB | 31      | 9     | 0     | 0.03   |
| ADATA     | IM2P33F8BR1-128GB  | 128 GB | 5       | 9     | 0     | 0.03   |
| Samsung   | MZALQ512HBLU-00BL2 | 512 GB | 82      | 9     | 0     | 0.03   |
| SanDisk   | WD_BLACK SN750 SE  | 1 TB   | 19      | 9     | 0     | 0.03   |
| Samsung   | MZVL2512HCJQ-00BL2 | 512 GB | 26      | 9     | 0     | 0.03   |
| Micron    | MTFDHBA512TDV-1... | 512 GB | 11      | 9     | 0     | 0.03   |
| Union ... | UMIS RPITJ256PE... | 256 GB | 1       | 9     | 0     | 0.03   |
| Samsung   | PM9A1 NVMe         | 2 TB   | 17      | 33    | 20    | 0.03   |
| Transcend | TS1TMTE112S        | 1 TB   | 1       | 9     | 0     | 0.03   |
| Samsung   | MZAL4256HBJD-00BL2 | 256 GB | 2       | 9     | 0     | 0.03   |
| Kingston  | SNVS500GB          | 500 GB | 8       | 9     | 0     | 0.03   |
| Phison    | C-E80T512G4-P3D... | 512 GB | 3       | 9     | 0     | 0.03   |
| SK hynix  | Skhynix BC501 NVMe | 256 GB | 5       | 9     | 0     | 0.03   |
| ADATA     | IM2P33F8A-512GD    | 512 GB | 8       | 9     | 0     | 0.03   |
| Phison    | MSI M390           | 500 GB | 4       | 9     | 0     | 0.03   |
| SanDisk   | WD IX SN530 SDB... | 1 TB   | 1       | 9     | 0     | 0.03   |
| Toshiba   | KBG4AZNV256G ME... | 256 GB | 1       | 9     | 0     | 0.03   |
| SanDisk   | WD Green SN350     | 2 TB   | 2       | 9     | 0     | 0.02   |
| WDC       | PC SN730 SDBQNT... | 256 GB | 1       | 9     | 0     | 0.02   |
| Silico... | YSSDM-128GN2000    | 128 GB | 1       | 9     | 0     | 0.02   |
| Corsair   | MP600 CORE         | 4 TB   | 2       | 8     | 0     | 0.02   |
| Phison    | Viper M.2 VPR100   | 512 GB | 1       | 8     | 0     | 0.02   |
| SanDisk   | SN530 SDBPNPZ-5... | 512 GB | 6       | 8     | 0     | 0.02   |
| Netac     | NVMe SSD           | 2 TB   | 4       | 10    | 5     | 0.02   |
| Phison    | ESO512GYLCT-EP3-2L | 512 GB | 4       | 8     | 0     | 0.02   |
| Hikvision | HS-SSD-E2000L 512G | 512 GB | 2       | 8     | 0     | 0.02   |
| VICKTER   | NVME SSD           | 512 GB | 2       | 8     | 0     | 0.02   |
| Micron    | MTFDKBA1T0TFK      | 1 TB   | 1       | 8     | 0     | 0.02   |
| Phison    | PS5012-E12S-512G   | 512 GB | 1       | 8     | 0     | 0.02   |
| SK hynix  | HFM128GD3JX016N    | 128 GB | 1       | 8     | 0     | 0.02   |
| Phison    | ESR512GTLCW-E6G... | 512 GB | 2       | 8     | 0     | 0.02   |
| Micron    | 7400_MTFDKBA480TDZ | 480 GB | 1       | 8     | 0     | 0.02   |
| Crucial   | CT1000P3SSD8       | 1 TB   | 10      | 8     | 0     | 0.02   |
| Hikvision | HS-SSD-E1000       | 128 GB | 1       | 8     | 0     | 0.02   |
| SanDisk   | WD PC SN810 SDC... | 1 TB   | 2       | 8     | 0     | 0.02   |
| ADATA     | SWORDFISH          | 2 TB   | 2       | 8     | 0     | 0.02   |
| WDC       | PC SN810 NVMe      | 1 TB   | 13      | 8     | 0     | 0.02   |
| SSSTC     | CL4-3D512-Q11 NVMe | 512 GB | 4       | 8     | 0     | 0.02   |
| SanDisk   | WD_BLACK SN770     | 500 GB | 14      | 8     | 0     | 0.02   |
| Toshiba   | KXD51LN11T92 1.9TB | 1.9 TB | 3       | 8     | 0     | 0.02   |
| Samsung   | MZVLQ512HALU-00007 | 512 GB | 4       | 8     | 0     | 0.02   |
| Samsung   | MZVL22T0HBLB-00B00 | 2 TB   | 25      | 8     | 0     | 0.02   |
| KIOXIA    | KBG5AZNT512G LA    | 512 GB | 5       | 8     | 0     | 0.02   |
| KLEVV     | CRAS C710 M.2 N... | 512 GB | 1       | 8     | 0     | 0.02   |
| Samsung   | MZVL21T0HCLR-00BH1 | 1 TB   | 13      | 8     | 0     | 0.02   |
| Micron    | MTFDKCD1T0TFK      | 1 TB   | 1       | 8     | 0     | 0.02   |
| KIOXIA    | KBG5AZNT256G LA    | 256 GB | 1       | 7     | 0     | 0.02   |
| Phison    | E15-1TB-PHISON-... | 1 TB   | 1       | 7     | 0     | 0.02   |
| V-GeN     | V-GEN08SM22SCY5... | 512 GB | 1       | 7     | 0     | 0.02   |
| WDC       | PC SN810 SDCPNR... | 1 TB   | 2       | 7     | 0     | 0.02   |
| Samsung   | MZVLQ1T0HBLB-00BH1 | 1 TB   | 18      | 7     | 0     | 0.02   |
| SanDisk   | PC SN740 NVMe WD   | 512 GB | 5       | 7     | 0     | 0.02   |
| Samsung   | MZ9LQ1T0HBLB-00B   | 1 TB   | 2       | 7     | 0     | 0.02   |
| WDC       | PC SN730 SDBPNT... | 256 GB | 3       | 7     | 0     | 0.02   |
| Crucial   | CT2000P3SSD8       | 2 TB   | 2       | 7     | 0     | 0.02   |
| Solid ... | CL1-3D128-Q11 N... | 128 GB | 1       | 7     | 0     | 0.02   |
| Apacer    | 960GB PCIe Drive   | 960 GB | 1       | 7     | 0     | 0.02   |
| WDC       | PC SN730 SDBPNT... | 1 TB   | 4       | 7     | 0     | 0.02   |
| Samsung   | MZVLB2T0HALB-000H1 | 2 TB   | 2       | 7     | 0     | 0.02   |
| WDC       | PC SN530 SDBQTP... | 512 GB | 2       | 7     | 0     | 0.02   |
| Samsung   | MZVLQ1T0HBLB-00BTW | 1 TB   | 2       | 7     | 0     | 0.02   |
| Hikvision | HS-SSD-E3000 256G  | 256 GB | 4       | 7     | 0     | 0.02   |
| Patriot   | P300               | 1 TB   | 2       | 7     | 0     | 0.02   |
| Crucial   | CT500P3SSD8        | 500 GB | 7       | 7     | 0     | 0.02   |
| Kimtigo   | SSD                | 512 GB | 3       | 7     | 0     | 0.02   |
| Apple     | SSD AP0256Q        | 256 GB | 1       | 7     | 0     | 0.02   |
| Micron    | MTFDKCD512TFK      | 512 GB | 18      | 7     | 0     | 0.02   |
| Samsung   | MZVLQ256HBJD-00BH1 | 256 GB | 18      | 7     | 0     | 0.02   |
| Crucial   | CT500P5PSSD8       | 500 GB | 12      | 7     | 0     | 0.02   |
| Toshiba   | KBG40ZNV512G ME... | 512 GB | 2       | 7     | 0     | 0.02   |
| SK hynix  | PC801 NVMe         | 512 GB | 5       | 7     | 0     | 0.02   |
| SK hynix  | HFM128GDHTNG-8510B | 128 GB | 5       | 6     | 0     | 0.02   |
| Samsung   | MZVL21T0HCLR-00BL7 | 1 TB   | 56      | 6     | 0     | 0.02   |
| Toshiba   | KXG6AZNV512G KI... | 512 GB | 3       | 6     | 0     | 0.02   |
| Kingston  | OM8SBP3512K-AH     | 512 GB | 15      | 6     | 0     | 0.02   |
| Samsung   | MZVLQ256HBJD-00B   | 256 GB | 4       | 6     | 0     | 0.02   |
| Phison    | Vi3000 SSD         | 2 TB   | 1       | 6     | 0     | 0.02   |
| ADATA     | IM2P33F8A-001TD    | 1 TB   | 2       | 6     | 0     | 0.02   |
| Samsung   | MZVL4512HBLU-00BH1 | 512 GB | 1       | 6     | 0     | 0.02   |
| Silico... | Inland NVMe SSD    | 256 GB | 2       | 6     | 0     | 0.02   |
| Samsung   | MZ9LQ256HBJQ-00000 | 256 GB | 2       | 6     | 0     | 0.02   |
| Phison    | CFESR512GMTCT-E... | 512 GB | 3       | 6     | 0     | 0.02   |
| Union ... | UMIS RPJTJ256ME... | 256 GB | 12      | 6     | 0     | 0.02   |
| KIOXIA    | KBG5AZNV512G LA    | 512 GB | 2       | 6     | 0     | 0.02   |
| Samsung   | MZVLW256HEHP-000   | 256 GB | 2       | 6     | 0     | 0.02   |
| Micron    | MTFDHBA1T0TDV-1... | 1 TB   | 10      | 6     | 0     | 0.02   |
| SK hynix  | SKHynix_HFM001T... | 1 TB   | 2       | 6     | 0     | 0.02   |
| Apple     | SSD AP0128J        | 121 GB | 9       | 6     | 0     | 0.02   |
| Samsung   | MZ9LQ128HBHQ-000H1 | 128 GB | 2       | 6     | 0     | 0.02   |
| Samsung   | MZVLQ128HBHQ-00000 | 128 GB | 2       | 6     | 0     | 0.02   |
| ZHITAI    | TiPlus5000         | 1 TB   | 2       | 6     | 0     | 0.02   |
| Apple     | SSD AP2048N        | 2 TB   | 2       | 6     | 0     | 0.02   |
| Samsung   | MZ9LQ512HBLU-00B   | 512 GB | 9       | 6     | 0     | 0.02   |
| Phison    | ESMP512GKB4C3-E... | 512 GB | 4       | 6     | 0     | 0.02   |
| Samsung   | SSD 980 PRO wit... | 1 TB   | 11      | 6     | 0     | 0.02   |
| Samsung   | MZALQ512HBLU-00BL1 | 512 GB | 26      | 6     | 0     | 0.02   |
| Samsung   | MZVL22T0HBLB-00BL7 | 2 TB   | 12      | 6     | 0     | 0.02   |
| WDC       | PC SN530 SDBPMP... | 256 GB | 34      | 6     | 0     | 0.02   |
| Samsung   | MZVL2256HCHQ-00B00 | 256 GB | 6       | 6     | 0     | 0.02   |
| SanDisk   | WD PC SN735 SDB... | 512 GB | 6       | 6     | 0     | 0.02   |
| Kingston  | SNV2S1000G         | 1 TB   | 7       | 5     | 0     | 0.02   |
| Samsung   | SSD 980            | 250 GB | 22      | 5     | 0     | 0.02   |
| Samsung   | MZVLQ1T0HBLB-00B   | 1 TB   | 4       | 5     | 0     | 0.02   |
| AMD       | R5MP512G8          | 512 GB | 1       | 5     | 0     | 0.02   |
| Samsung   | PM981a NVMe SED    | 512 GB | 1       | 5     | 0     | 0.02   |
| Toshiba   | KBG30ZMV512G KI... | 512 GB | 5       | 5     | 0     | 0.02   |
| Phison    | E12-1TB-PHISON-... | 1 TB   | 1       | 5     | 0     | 0.02   |
| WDC       | PC SN730 SDBPNT... | 256 GB | 3       | 5     | 0     | 0.02   |
| Micron    | 3400_MTFDKBA512TFH | 512 GB | 20      | 5     | 0     | 0.02   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 22      | 5     | 0     | 0.02   |
| BIWIN     | SSD                | 1 TB   | 7       | 5     | 0     | 0.02   |
| Micron    | MTFDKBA512TFK      | 512 GB | 5       | 5     | 0     | 0.02   |
| WDC       | PC SN810 NVMe      | 512 GB | 9       | 5     | 0     | 0.02   |
| SSSTC     | CA5-8D256-Q79      | 256 GB | 2       | 5     | 0     | 0.02   |
| EAGET     | SSD Device         | 512 GB | 1       | 5     | 0     | 0.02   |
| PNY       | CS1030 1TB SSD     | 1 TB   | 4       | 5     | 0     | 0.02   |
| Intenso   | PCIe               | 240 GB | 1       | 5     | 0     | 0.02   |
| Phison    | E12S-512G-PHISO... | 512 GB | 4       | 5     | 0     | 0.02   |
| SanDisk   | WD PC SN810 SDC... | 1 TB   | 6       | 5     | 0     | 0.02   |
| Samsung   | MZALQ256HBJD-00BL2 | 256 GB | 29      | 5     | 0     | 0.01   |
| FORESEE   | XP2000F512G        | 512 GB | 1       | 5     | 0     | 0.01   |
| Samsung   | MZVL2512HCJQ-00B00 | 512 GB | 40      | 5     | 3     | 0.01   |
| SanDisk   | WD_BLACK SN770     | 250 GB | 5       | 5     | 0     | 0.01   |
| PNY       | CS3030 2000GB SSD  | 2 TB   | 1       | 5     | 0     | 0.01   |
| SanDisk   | WD PC SN740 SDD... | 256 GB | 1       | 5     | 0     | 0.01   |
| Gigaby... | GP-GM301TB-G       | 1 TB   | 1       | 5     | 0     | 0.01   |
| Kingston  | OM8SEP4512Q-A0     | 512 GB | 1       | 5     | 0     | 0.01   |
| Phison    | MSI M390           | 2 TB   | 1       | 5     | 0     | 0.01   |
| WDC       | CH SN530 SDBPTP... | 930 GB | 1       | 5     | 0     | 0.01   |
| Micron    | MTFDKCD256TFK      | 256 GB | 4       | 5     | 0     | 0.01   |
| Foxline   | FLSSD256M80E13TCX5 | 256 GB | 16      | 5     | 0     | 0.01   |
| FORESEE   | P78AF256GB         | 256 GB | 1       | 4     | 0     | 0.01   |
| Seagate   | FireCuda 510 SS... | 1 TB   | 2       | 4     | 0     | 0.01   |
| Micron    | 3400_MTFDKBA1T0TFH | 1 TB   | 50      | 4     | 0     | 0.01   |
| SanDisk   | WD PC SN735 SDB... | 1 TB   | 1       | 4     | 0     | 0.01   |
| Samsung   | MZ9LQ256HBJD-00B   | 256 GB | 4       | 4     | 0     | 0.01   |
| Kingston  | SNV2S2000G         | 2 TB   | 5       | 4     | 0     | 0.01   |
| Samsung   | MZVLQ512HBLU-00B   | 512 GB | 13      | 4     | 0     | 0.01   |
| T-FORCE   | TM8FP7002T         | 2 TB   | 2       | 4     | 0     | 0.01   |
| Crucial   | CT2000P5PSSD8      | 2 TB   | 6       | 4     | 0     | 0.01   |
| MAXIO     | NE-256             | 256 GB | 1       | 4     | 0     | 0.01   |
| SanDisk   | WD_BLACK SN850 ... | 1 TB   | 1       | 4     | 0     | 0.01   |
| Seagate   | FireCuda 510 SS... | 250 GB | 2       | 4     | 0     | 0.01   |
| Patriot   | M.2 P300           | 512 GB | 3       | 4     | 0     | 0.01   |
| Solid ... | CL1-3D256-Q11 N... | 256 GB | 4       | 4     | 0     | 0.01   |
| Samsung   | MZVL2512HCJQ-00B07 | 512 GB | 2       | 4     | 0     | 0.01   |
| SanDisk   | WD Blue SN570      | 2 TB   | 7       | 4     | 0     | 0.01   |
| Micron    | MTFDKBA512TFH      | 512 GB | 16      | 4     | 0     | 0.01   |
| Crucial   | CT1000P5PSSD8      | 1 TB   | 34      | 4     | 0     | 0.01   |
| Phison    | E12S-1TB-PHISON... | 1 TB   | 1       | 4     | 0     | 0.01   |
| WDC       | PC SN730 SDBQNT... | 1 TB   | 1       | 4     | 0     | 0.01   |
| Transcend | TS1TMTE110Q        | 1 TB   | 1       | 4     | 0     | 0.01   |
| Kingston  | OM3PDP3512B-A01    | 512 GB | 4       | 4     | 0     | 0.01   |
| Samsung   | MZVLQ512HBLU-00BH1 | 512 GB | 41      | 4     | 0     | 0.01   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 2       | 4     | 0     | 0.01   |
| Team      | TM8FPD001T         | 1 TB   | 3       | 4     | 0     | 0.01   |
| Micron    | MTFDHBA256TDV-1... | 256 GB | 3       | 4     | 0     | 0.01   |
| Kingston  | OM8SEP4256Q-A0     | 256 GB | 1       | 4     | 0     | 0.01   |
| Toshiba   | KXG60ZNV1T02 KI... | 1 TB   | 5       | 4     | 0     | 0.01   |
| Samsung   | PM991a NVMe        | 128 GB | 19      | 4     | 0     | 0.01   |
| PNY       | CS2130 500GB SSD   | 500 GB | 1       | 4     | 0     | 0.01   |
| Micron    | 2400_MTFDKBA512QFM | 512 GB | 4       | 4     | 0     | 0.01   |
| Seagate   | FireCuda 530 ZP... | 500 GB | 2       | 3     | 0     | 0.01   |
| Phison    | E12-512G-PHISON... | 512 GB | 1       | 3     | 0     | 0.01   |
| SK hynix  | HFM256GD3JX013N    | 256 GB | 1       | 3     | 0     | 0.01   |
| WDC       | PC SN810 SDCPNR... | 2 TB   | 4       | 3     | 0     | 0.01   |
| SanDisk   | WD PC SN810 SDC... | 512 GB | 3       | 3     | 0     | 0.01   |
| Samsung   | PM981a NVMe SED    | 256 GB | 2       | 3     | 0     | 0.01   |
| PNY       | CS3140 1TB SSD     | 1 TB   | 3       | 3     | 0     | 0.01   |
| Phison    | MSI M370           | 1 TB   | 1       | 3     | 0     | 0.01   |
| ADATA     | IM2P33F8ABR2-256GB | 256 GB | 6       | 3     | 0     | 0.01   |
| Samsung   | MZVL22T0HBLB-00BTW | 2 TB   | 2       | 3     | 0     | 0.01   |
| PNY       | CS1031 256GB SSD   | 256 GB | 1       | 3     | 0     | 0.01   |
| Kingston  | SNV2S250G          | 250 GB | 5       | 3     | 0     | 0.01   |
| Apple     | SSD AP1536M        | 1.5 TB | 1       | 3     | 0     | 0.01   |
| Samsung   | MZVLQ256HAJD-00007 | 256 GB | 6       | 3     | 0     | 0.01   |
| EMTEC     | X300               | 256 GB | 1       | 3     | 0     | 0.01   |
| UMIS      | RPJTJ256MGE1QDQ    | 256 GB | 1       | 3     | 0     | 0.01   |
| UMIS      | RPITJ512PED2OWX    | 512 GB | 1       | 3     | 0     | 0.01   |
| Intenso   | NVME               | 250 GB | 1       | 3     | 0     | 0.01   |
| Apple     | SSD AP1024Q        | 1 TB   | 1       | 3     | 0     | 0.01   |
| WDC       | PC SN520 SDAPMU... | 256 GB | 1       | 3     | 0     | 0.01   |
| Micron    | MTFDKBA512TFH-1... | 512 GB | 11      | 3     | 0     | 0.01   |
| ADATA     | IM2P33F8ABR1-256GB | 256 GB | 2       | 3     | 0     | 0.01   |
| Intel     | SSDPE21D280GA      | 280 GB | 2       | 3     | 0     | 0.01   |
| Silico... | SK                 | 2 TB   | 1       | 3     | 0     | 0.01   |
| Gigaby... | GP-GSM2NE8128GNTD  | 128 GB | 1       | 3     | 0     | 0.01   |
| Micron    | 2400_MTFDKBA1T0QFM | 1 TB   | 1       | 3     | 0     | 0.01   |
| WDC       | WDBA3V5000ANC-WRSN | 500 GB | 1       | 3     | 0     | 0.01   |
| FORESEE   | P900F128GH         | 128 GB | 3       | 2     | 0     | 0.01   |
| WDC       | PC SN730 SDBPNT... | 512 GB | 5       | 2     | 0     | 0.01   |
| J.ZAO     | QL SERIES 256GB... | 256 GB | 1       | 2     | 0     | 0.01   |
| KIOXIA    | KBG40ZPZ128G BG4A  | 128 GB | 1       | 2     | 0     | 0.01   |
| Silico... | AAR512GN122321030  | 512 GB | 1       | 2     | 0     | 0.01   |
| Micron    | 3400 NVMe          | 512 GB | 7       | 2     | 0     | 0.01   |
| Dell      | Ent NVMe CM6 MU... | 6.4 TB | 4       | 2     | 0     | 0.01   |
| Teclast   | 128GB NP900-2280   | 128 GB | 1       | 2     | 0     | 0.01   |
| Samsung   | MZVLQ128HBHQ-000H1 | 128 GB | 1       | 2     | 0     | 0.01   |
| Silico... | NVMe               | 256 GB | 1       | 2     | 0     | 0.01   |
| imation   | M.2 PCIe 2TB SS... | 2 TB   | 1       | 2     | 0     | 0.01   |
| J.ZAO     | QL SERIES 1TB SSD  | 1 TB   | 1       | 2     | 0     | 0.01   |
| Micron    | 2300 NVMe          | 256 GB | 1       | 2     | 0     | 0.01   |
| Samsung   | PM981 NVMe SED     | 256 GB | 1       | 2     | 0     | 0.01   |
| Crucial   | CT4000P3PSSD8      | 4 TB   | 1       | 2     | 0     | 0.01   |
| Hikvision | HS-SSD-E1000 256G  | 256 GB | 2       | 2     | 0     | 0.01   |
| Samsung   | 980 PRO with He... | 1 TB   | 4       | 2     | 0     | 0.01   |
| SanDisk   | WD PC SN810 SDC... | 512 GB | 8       | 2     | 0     | 0.01   |
| Samsung   | PM981 NVMe SED     | 512 GB | 2       | 2     | 0     | 0.01   |
| Fanxiang  | S500PRO            | 2 TB   | 1       | 2     | 0     | 0.01   |
| KIOXIA    | KBG4AZNV256G       | 256 GB | 1       | 2     | 0     | 0.01   |
| KIOXIA    | KBG5AZNT1T02 LA    | 1 TB   | 3       | 2     | 0     | 0.01   |
| Crucial   | CT4000P3SSD8       | 4 TB   | 3       | 2     | 0     | 0.01   |
| NTC       | 512GB NVMe         | 512 GB | 1       | 2     | 0     | 0.01   |
| Phison    | 256GB EM280256G... | 256 GB | 2       | 2     | 0     | 0.01   |
| FORESEE   | XP1000F512G        | 512 GB | 2       | 2     | 1     | 0.01   |
| Micron    | MTFDKBA1T0TFH-1... | 1 TB   | 8       | 2     | 0     | 0.01   |
| Gigabyte  | AG470S1TB-SI B10   | 1 TB   | 3       | 2     | 0     | 0.01   |
| Samsung   | MZVL21T0HCLR-00BH7 | 1 TB   | 1       | 2     | 0     | 0.01   |
| SanDisk   | WD_BLACK SN750 ... | 500 GB | 1       | 2     | 0     | 0.01   |
| Phison    | One-Netbook PCI... | 1 TB   | 4       | 2     | 0     | 0.01   |
| Micron    | MTFDKBA1T0TFH      | 1 TB   | 16      | 2     | 0     | 0.01   |
| YMTC      | PC210-512GB-B      | 512 GB | 1       | 2     | 0     | 0.01   |
| Samsung   | PM9A1 NVMe         | 256 GB | 5       | 2     | 0     | 0.01   |
| SanDisk   | SN530 SDBPNPZ-2... | 256 GB | 3       | 2     | 0     | 0.01   |
| YMTC      | PC005              | 1 TB   | 2       | 2     | 0     | 0.01   |
| Wester... | SN560E             | 500 GB | 1       | 1     | 0     | 0.01   |
| Intel     | SSDPEKKA256G7      | 256 GB | 2       | 1     | 0     | 0.01   |
| SanDisk   | WD PC SN735 SDB... | 256 GB | 2       | 1     | 0     | 0.01   |
| KIOXIA    | KBG50ZNS256G NVMe  | 256 GB | 4       | 1     | 0     | 0.01   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 4       | 1     | 0     | 0.00   |
| GLOWAY    | YCT512NVMe-M.2-... | 512 GB | 1       | 1     | 0     | 0.00   |
| SanDisk   | WD PC SN735 SDB... | 1 TB   | 8       | 1     | 0     | 0.00   |
| Samsung   | MZALQ256HBJD-00BL1 | 256 GB | 9       | 1     | 0     | 0.00   |
| Toshiba   | KBG30ZMV128G KI... | 128 GB | 1       | 1     | 0     | 0.00   |
| Micron    | MTFDHBA1T0QFD      | 1 TB   | 1       | 1     | 0     | 0.00   |
| Samsung   | MZAL41T0HBLB-00BL2 | 1 TB   | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN530 SDBPNP... | 512 GB | 5       | 1     | 0     | 0.00   |
| Micron    | 7300_MTFDHBE960TDF | 960 GB | 2       | 1     | 0     | 0.00   |
| Mushkin   | MKNSSDTS2TB-D8     | 2 TB   | 1       | 1     | 0     | 0.00   |
| Union ... | UMIS RPITJ512PE... | 512 GB | 2       | 1     | 0     | 0.00   |
| SanDisk   | WD_BLACK SN850X    | 1 TB   | 9       | 1     | 0     | 0.00   |
| WDC       | PC SN530 NVMe      | 1 TB   | 3       | 1     | 0     | 0.00   |
| Apacer    | AS2280P4           | 1 TB   | 1       | 1     | 0     | 0.00   |
| Samsung   | MZVLQ512HALU-000   | 512 GB | 4       | 1     | 0     | 0.00   |
| Samsung   | PM991a NVMe        | 1 TB   | 4       | 1     | 0     | 0.00   |
| Kllisre   | 256GB              | 256 GB | 2       | 1     | 0     | 0.00   |
| SanDisk   | WD_BLACK SN850X    | 2 TB   | 4       | 1     | 0     | 0.00   |
| KIOXIA    | KBG50ZNT1T02 LS    | 1 TB   | 2       | 1     | 0     | 0.00   |
| PNY       | CS1030 250GB SSD   | 250 GB | 2       | 1     | 0     | 0.00   |
| Phison    | 311CD0128GB        | 128 GB | 2       | 1     | 0     | 0.00   |
| BIWIN     | NE-128             | 128 GB | 1       | 1     | 0     | 0.00   |
| Hikvision | HS-SSD-E2000 256G  | 256 GB | 1       | 1     | 0     | 0.00   |
| Toshiba   | KBG40ZNT1T02 ME... | 1 TB   | 1       | 1     | 0     | 0.00   |
| Toshiba   | KXG60PNV1T02 NV... | 1 TB   | 1       | 1     | 0     | 0.00   |
| SanDisk   | WD PC SN740 SDD... | 1 TB   | 1       | 1     | 0     | 0.00   |
| Samsung   | MZVL4512HBLU-00BL7 | 512 GB | 2       | 1     | 0     | 0.00   |
| Transcend | TS512GMTE510T      | 512 GB | 3       | 1     | 0     | 0.00   |
| KIOXIA... | SSD                | 250 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | MZ9LQ512HALU-00000 | 512 GB | 3       | 1     | 0     | 0.00   |
| ADATA     | LEGEND 840         | 1 TB   | 1       | 1     | 0     | 0.00   |
| Intel     | SSDPEDKE020T7      | 2 TB   | 2       | 1     | 0     | 0.00   |
| Seagate   | BarraCuda 510 S... | 250 GB | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN530 SDBPNP... | 1 TB   | 2       | 1     | 0     | 0.00   |
| Corsair   | MP600 PRO NH       | 1 TB   | 1       | 1     | 0     | 0.00   |
| KIOXIA    | KBG40ZNS128G BG4A  | 128 GB | 1       | 1     | 0     | 0.00   |
| KIOXIA    | KXG70ZNV512G NVMe  | 512 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | MZALQ128HCHQ-00BL2 | 128 GB | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN530 SDBPTP... | 256 GB | 1       | 1     | 0     | 0.00   |
| Phison    | E12S-TB-PHISON-... | 1 TB   | 1       | 1     | 0     | 0.00   |
| Samsung   | MZVL22T0HBLB-00B07 | 2 TB   | 1       | 1     | 0     | 0.00   |
| SanDisk   | WD IX SN530 SDB... | 256 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | MZVPW128HEGM-00000 | 128 GB | 1       | 37    | 32    | 0.00   |
| FORESEE   | VP1000F512G        | 512 GB | 2       | 1     | 0     | 0.00   |
| ADATA     | IM2P33F8-256GD1    | 256 GB | 1       | 1     | 0     | 0.00   |
| Acer      | SSD FA100          | 2 TB   | 1       | 1     | 0     | 0.00   |
| Phison    | ESE2A044-512 NVMe  | 512 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | MZVL21T0HCLR-00BT7 | 1 TB   | 1       | 1     | 0     | 0.00   |
| ADATA     | LEGEND 740         | 250 GB | 1       | 1     | 0     | 0.00   |
| Micron    | 3460 NVMe          | 512 GB | 1       | 1     | 0     | 0.00   |
| Phison    | MLD M300 NVMe SSD  | 1 TB   | 1       | 1     | 0     | 0.00   |
| Samsung   | MZALQ1T0HALB-000L2 | 1 TB   | 2       | 1     | 0     | 0.00   |
| Silico... | WN600              | 1 TB   | 1       | 1     | 0     | 0.00   |
| V-GeN     | V-GEN08MA22SCY1... | 128 GB | 1       | 1     | 0     | 0.00   |
| WDC       | PC SN540 SDDPNP... | 512 GB | 2       | 1     | 0     | 0.00   |
| Samsung   | PM9A1 NVMe SED     | 1 TB   | 1       | 1     | 0     | 0.00   |
| Silico... | GSDFN512TS3F1OGCX  | 512 GB | 1       | 1     | 0     | 0.00   |
| WALRAM    | 1TB                | 1 TB   | 2       | 1     | 0     | 0.00   |
| YMTC      | YMSS1ED04B21MC     | 256 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | PM9A1 NVMe SED     | 512 GB | 3       | 0     | 0     | 0.00   |
| SanDisk   | WD PC SN810 SDC... | 1 TB   | 2       | 0     | 0     | 0.00   |
| Samsung   | MZVLQ256HBJD-00B00 | 256 GB | 2       | 0     | 0     | 0.00   |
| WDC       | PC SN520 SDAPTU... | 128 GB | 2       | 0     | 0     | 0.00   |
| SanDisk   | WD PC SN740 SDD... | 1 TB   | 2       | 0     | 0     | 0.00   |
| ShiJi     | 1TB                | 1 TB   | 1       | 3     | 3     | 0.00   |
| SSSTC     | CA6-8D512          | 512 GB | 2       | 0     | 0     | 0.00   |
| SanDisk   | PC SN740 NVMe WD   | 1 TB   | 2       | 0     | 0     | 0.00   |
| Lexar     | SSD NM760          | 1 TB   | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVL22T0HBLB-00BL2 | 2 TB   | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN530 SDBPNP... | 256 GB | 2       | 0     | 0     | 0.00   |
| HP        | SSD FX900 Pro      | 2 TB   | 1       | 0     | 0     | 0.00   |
| Corsair   | MP600 GS           | 1 TB   | 1       | 0     | 0     | 0.00   |
| Intel     | SSDPF2KX038T1      | 3.8 TB | 2       | 0     | 0     | 0.00   |
| Samsung   | SSD 990 PRO        | 1 TB   | 7       | 0     | 0     | 0.00   |
| SanDisk   | WD PC SN810 SDC... | 1 TB   | 2       | 0     | 0     | 0.00   |
| WALRAM    | 512G               | 512 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZALQ128HCHQ-00BL1 | 128 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVL4512HBLU-00BTW | 512 GB | 1       | 0     | 0     | 0.00   |
| Silico... | RD-P380TIN-C256    | 256 GB | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN810 SDCPNR... | 1 TB   | 1       | 0     | 0     | 0.00   |
| BIWIN     | CE480T5D101-256    | 256 GB | 14      | 0     | 0     | 0.00   |
| Intel     | SSDPE2KE016T8      | 1.6 TB | 2       | 0     | 0     | 0.00   |
| Micron    | MTFDHBA256TDV-1... | 256 GB | 1       | 0     | 0     | 0.00   |
| SSSTC     | CL1-8D128-HP       | 128 GB | 2       | 0     | 0     | 0.00   |
| Silico... | DC 256G            | 256 GB | 1       | 0     | 0     | 0.00   |
| Silico... | NE-240             | 240 GB | 1       | 0     | 0     | 0.00   |
| Toshiba   | KXG50PNV2T04 KI... | 2 TB   | 1       | 0     | 0     | 0.00   |
| UMIS      | RPIRJ256VME2MWD    | 256 GB | 2       | 0     | 0     | 0.00   |
| SSSTC     | CL4-8D512          | 512 GB | 3       | 0     | 0     | 0.00   |
| Samsung   | MZVLB1T0HBLR-000H7 | 1 TB   | 2       | 0     | 0     | 0.00   |
| SanDisk   | WD PC SN810 SDC... | 2 TB   | 2       | 0     | 0     | 0.00   |
| Samsung   | MZVL21T0HCLR-00A00 | 1 TB   | 1       | 0     | 0     | 0.00   |
| Colorful  | CN600              | 256 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | WD PC SN740 SDD... | 512 GB | 5       | 0     | 0     | 0.00   |
| Plextor   | PX-256M8SeY        | 256 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | SSD 980 PRO wit... | 2 TB   | 1       | 0     | 0     | 0.00   |
| Samsung   | SSD 990 PRO        | 2 TB   | 4       | 0     | 0     | 0.00   |
| ZHITAI    | TiPro7000          | 1 TB   | 2       | 0     | 0     | 0.00   |
| Intel     | MEMPEK1J064GA      | 64 GB  | 1       | 0     | 0     | 0.00   |
| KIOXIA    | KBG50ZNT256G LS    | 256 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | SEDC1000M3840G     | 3.8 TB | 1       | 0     | 0     | 0.00   |
| Lenovo    | M.2 2280 NVMe S... | 512 GB | 1       | 0     | 0     | 0.00   |
| Phison    | ESE2A047-M24 NVMe  | 1 TB   | 1       | 0     | 0     | 0.00   |
| WDC       | PC SN530 SDBQNP... | 512 GB | 3       | 0     | 0     | 0.00   |
| WDC       | WDS400T3X0C-00SJG0 | 4 TB   | 1       | 0     | 0     | 0.00   |
| ShiJi     | 512GB M.2-NVMe     | 512 GB | 2       | 21    | 508   | 0.00   |
| Silico... | Wodposit NVMe SSD  | 256 GB | 2       | 0     | 0     | 0.00   |
| KIOXIA    | KBG50ZNV256G       | 256 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | OM8PCP3512F-AB1    | 512 GB | 1       | 0     | 0     | 0.00   |
| Kingston  | OM8PGP41024Q-A0    | 1 TB   | 1       | 0     | 0     | 0.00   |
| Plextor   | PX-512M9PeGN       | 512 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | WD PC SN810 SDC... | 2 TB   | 1       | 0     | 0     | 0.00   |
| Silico... | FPE220M8SSD512G    | 512 GB | 1       | 0     | 0     | 0.00   |
| EMTEC     | X300               | 500 GB | 1       | 0     | 0     | 0.00   |
| ExeGate   | EX282318RUS(240GB) | 240 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | WD PC SN740 SDD... | 512 GB | 1       | 0     | 0     | 0.00   |
| Silico... | NVMe SSD           | 240 GB | 1       | 0     | 0     | 0.00   |
| Solid ... | SSSTC CL1-4D256... | 256 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVLQ512HBLU-00B07 | 512 GB | 2       | 0     | 0     | 0.00   |
| SanDisk   | WD PC SN810 SDC... | 256 GB | 2       | 0     | 0     | 0.00   |
| Samsung   | MZVL21T0HCLR-00B07 | 1 TB   | 4       | 0     | 0     | 0.00   |
| Lexar     | SSD NM610PRO       | 1 TB   | 1       | 0     | 0     | 0.00   |
| Phison    | MSI M390           | 250 GB | 1       | 0     | 0     | 0.00   |
| SSSTC     | CA5-8D1024         | 1 TB   | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVL2512HCJQ-00BT7 | 512 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | PM9A1 NVMe SED     | 256 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | SN530 SDBPNPZ-1... | 1 TB   | 3       | 0     | 0     | 0.00   |
| ADATA     | IM2P33F8-512GD     | 512 GB | 2       | 0     | 0     | 0.00   |
| SanDisk   | WD_BLACK SN850X    | 4 TB   | 1       | 0     | 0     | 0.00   |
| Silico... | HomeNet HN M2 SSD  | 256 GB | 1       | 0     | 0     | 0.00   |
| Solid ... | SSSTC CL1-4D512    | 512 GB | 1       | 0     | 0     | 0.00   |
| Micron    | MTFDHBA1T0TDV-1... | 1 TB   | 1       | 33    | 169   | 0.00   |
| AGI       | AGI512G16AI198     | 512 GB | 1       | 0     | 0     | 0.00   |
| Gigaby... | GP-ASM2NE2512GTTDR | 512 GB | 1       | 0     | 0     | 0.00   |
| Goodram   | SSDPR-PX500-512... | 512 GB | 1       | 0     | 0     | 0.00   |
| Phison    | PSEJN512GA87EC0    | 512 GB | 1       | 0     | 0     | 0.00   |
| Plextor   | PX-1TM10PGN        | 1 TB   | 1       | 0     | 0     | 0.00   |
| SanDisk   | PC SN740 NVMe WD   | 256 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | WD PC SN740 SDD... | 512 GB | 1       | 0     | 0     | 0.00   |
| Silico... | ZTC-PCIEG3-001T    | 1 TB   | 1       | 0     | 0     | 0.00   |
| ZHITAI    | TiPlus7100         | 2 TB   | 1       | 0     | 0     | 0.00   |
| POWER X   | NE1000-256GB       | 256 GB | 1       | 0     | 0     | 0.00   |
| SSSTC     | CA6-8D512-Q11 NVMe | 512 GB | 1       | 0     | 0     | 0.00   |
| Silico... | HX512GSSDM2PCIE    | 512 GB | 1       | 0     | 0     | 0.00   |
| Silico... | NVME SSD           | 2 TB   | 1       | 0     | 0     | 0.00   |
| Yangtz... | ZHITAI PC005 Ac... | 1 TB   | 1       | 0     | 0     | 0.00   |
| BIWIN     | NE-512             | 512 GB | 1       | 0     | 0     | 0.00   |
| Micron    | MTFDHBA512TDV-1... | 512 GB | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVL2256HCHQ-00BH1 | 256 GB | 1       | 0     | 0     | 0.00   |
| Gigabyte  | GP-GM30512G-G      | 512 GB | 1       | 47    | 1011  | 0.00   |
| ADATA     | LEGEND 840         | 512 GB | 1       | 0     | 0     | 0.00   |
| Corsair   | MP600 PRO LPX      | 4 TB   | 1       | 0     | 0     | 0.00   |
| FORESEE   | XP1000F256G        | 256 GB | 1       | 0     | 0     | 0.00   |
| Mushkin   | MKNSSDVT2TB-D8     | 2 TB   | 1       | 0     | 0     | 0.00   |
| Patriot   | M.2 P400           | 512 GB | 1       | 0     | 0     | 0.00   |
| ZHITAI    | TiPlus5000         | 512 GB | 1       | 0     | 0     | 0.00   |
| Phison    | ES                 | 512 GB | 1       | 33    | 1007  | 0.00   |
| ADATA     | IM2P33F8ABR1-1TB   | 1 TB   | 1       | 2     | 1015  | 0.00   |
| Team      | TM8FP4004T         | 4 TB   | 1       | 0     | 1010  | 0.00   |

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
| Avant       | 1      | 1       | 891   | 0     | 2.44   |
| addlink     | 1      | 16      | 340   | 0     | 0.93   |
| Aura        | 1      | 4       | 339   | 0     | 0.93   |
| tigo        | 1      | 1       | 313   | 0     | 0.86   |
| KINGBANK    | 1      | 2       | 312   | 0     | 0.86   |
| OYUNKEY     | 1      | 1       | 310   | 0     | 0.85   |
| Reeinno     | 1      | 1       | 284   | 0     | 0.78   |
| Ramsta      | 1      | 1       | 276   | 0     | 0.76   |
| Intel       | 124    | 2127    | 259   | 8     | 0.67   |
| Corsair     | 30     | 313     | 243   | 1     | 0.66   |
| BAITITON    | 1      | 1       | 232   | 0     | 0.64   |
| Toshiba     | 108    | 1205    | 221   | 2     | 0.60   |
| LDLC        | 3      | 5       | 212   | 0     | 0.58   |
| AMD         | 5      | 19      | 198   | 0     | 0.54   |
| HP          | 12     | 114     | 218   | 10    | 0.54   |
| Plextor     | 22     | 52      | 220   | 33    | 0.54   |
| Transcend   | 15     | 85      | 194   | 0     | 0.53   |
| Reletech    | 4      | 7       | 189   | 0     | 0.52   |
| Mushkin     | 12     | 40      | 180   | 27    | 0.48   |
| OWC         | 1      | 2       | 168   | 0     | 0.46   |
| Kingchuxing | 3      | 3       | 164   | 0     | 0.45   |
| T-CREATE    | 2      | 2       | 156   | 0     | 0.43   |
| SPCC        | 10     | 159     | 157   | 34    | 0.43   |
| XPG         | 14     | 230     | 154   | 20    | 0.40   |
| Phison      | 95     | 783     | 145   | 2     | 0.40   |
| BIOSTAR     | 1      | 1       | 144   | 0     | 0.40   |
| T-FORCE     | 7      | 15      | 139   | 0     | 0.38   |
| Lenovo      | 9      | 78      | 145   | 3     | 0.38   |
| SNR         | 1      | 1       | 135   | 0     | 0.37   |
| ADATA       | 61     | 720     | 137   | 17    | 0.36   |
| Lite-On     | 27     | 96      | 127   | 3     | 0.35   |
| Crucial     | 22     | 810     | 131   | 8     | 0.35   |
| Lexar       | 7      | 24      | 125   | 0     | 0.34   |
| Teclast     | 2      | 2       | 121   | 0     | 0.33   |
| Gigabyte... | 16     | 85      | 117   | 0     | 0.32   |
| Seagate     | 27     | 139     | 115   | 0     | 0.32   |
| ASint       | 1      | 1       | 111   | 0     | 0.31   |
| Patriot     | 14     | 50      | 110   | 0     | 0.30   |
| Silicon ... | 80     | 264     | 110   | 1     | 0.30   |
| Gigabyte    | 17     | 80      | 110   | 13    | 0.30   |
| Hikvision   | 16     | 28      | 108   | 0     | 0.30   |
| Zheino      | 2      | 4       | 107   | 0     | 0.30   |
| XrayDisk    | 2      | 7       | 106   | 0     | 0.29   |
| Smartbuy    | 6      | 10      | 105   | 0     | 0.29   |
| PNY         | 22     | 104     | 112   | 1     | 0.29   |
| Dell        | 7      | 14      | 104   | 0     | 0.29   |
| Hyundai     | 1      | 1       | 95    | 0     | 0.26   |
| Goodram     | 9      | 31      | 93    | 1     | 0.25   |
| Team        | 14     | 59      | 94    | 52    | 0.25   |
| Kingston    | 76     | 1417    | 91    | 3     | 0.25   |
| KIOXIA      | 51     | 861     | 91    | 2     | 0.25   |
| AXIOM       | 1      | 1       | 87    | 0     | 0.24   |
| Qunion      | 1      | 1       | 87    | 0     | 0.24   |
| KIOXIA-E... | 7      | 43      | 84    | 0     | 0.23   |
| HUAWEI      | 2      | 10      | 78    | 0     | 0.22   |
| WDC         | 171    | 3550    | 75    | 2     | 0.21   |
| Samsung     | 272    | 9623    | 77    | 2     | 0.21   |
| KLLISRE     | 2      | 6       | 73    | 0     | 0.20   |
| ZHITAI      | 6      | 10      | 69    | 0     | 0.19   |
| Apacer      | 9      | 58      | 69    | 0     | 0.19   |
| Acer        | 2      | 3       | 68    | 0     | 0.19   |
| ORICO       | 2      | 4       | 67    | 0     | 0.18   |
| SK hynix    | 114    | 2201    | 59    | 1     | 0.16   |
| UMIS        | 19     | 202     | 57    | 1     | 0.16   |
| V-GeN       | 4      | 4       | 55    | 0     | 0.15   |
| SETHRISE    | 1      | 1       | 54    | 0     | 0.15   |
| INDMEM      | 1      | 1       | 313   | 5     | 0.14   |
| SSSTC       | 25     | 168     | 51    | 0     | 0.14   |
| Netac       | 7      | 38      | 48    | 1     | 0.13   |
| minisforum  | 1      | 1       | 45    | 0     | 0.13   |
| SanDisk     | 65     | 419     | 45    | 0     | 0.12   |
| OSCOO       | 2      | 3       | 44    | 0     | 0.12   |
| Micron      | 71     | 922     | 36    | 1     | 0.10   |
| FORESEE     | 10     | 19      | 32    | 1     | 0.09   |
| MSI         | 1      | 1       | 32    | 0     | 0.09   |
| Colorful    | 3      | 4       | 29    | 0     | 0.08   |
| KingFast    | 1      | 2       | 27    | 0     | 0.08   |
| Inland      | 1      | 3       | 26    | 23    | 0.07   |
| ShiJi       | 4      | 6       | 31    | 170   | 0.07   |
| YMTC        | 5      | 36      | 23    | 0     | 0.06   |
| Apple       | 28     | 296     | 21    | 4     | 0.06   |
| Union Me... | 10     | 70      | 20    | 0     | 0.06   |
| Star Drive  | 1      | 13      | 20    | 0     | 0.06   |
| Timetec     | 1      | 2       | 19    | 0     | 0.05   |
| Phytium     | 1      | 1       | 18    | 0     | 0.05   |
| SMI         | 1      | 2       | 17    | 0     | 0.05   |
| Fanxiang    | 3      | 5       | 17    | 0     | 0.05   |
| J.ZAO       | 3      | 3       | 16    | 0     | 0.05   |
| Kimtigo     | 2      | 7       | 16    | 0     | 0.05   |
| Foxline     | 2      | 17      | 16    | 0     | 0.04   |
| KLEVV       | 2      | 2       | 15    | 0     | 0.04   |
| OEM         | 1      | 3       | 14    | 0     | 0.04   |
| Solid St... | 8      | 15      | 13    | 0     | 0.04   |
| Kingmax     | 1      | 1       | 12    | 0     | 0.03   |
| BIWIN       | 6      | 34      | 10    | 0     | 0.03   |
| UDinfo      | 1      | 1       | 10    | 0     | 0.03   |
| imation     | 2      | 2       | 9     | 0     | 0.03   |
| VICKTER     | 1      | 2       | 8     | 0     | 0.02   |
| WALRAM      | 4      | 5       | 6     | 0     | 0.02   |
| EAGET       | 1      | 1       | 5     | 0     | 0.02   |
| ExeGate     | 2      | 2       | 5     | 0     | 0.01   |
| MAXIO       | 1      | 1       | 4     | 0     | 0.01   |
| Intenso     | 2      | 2       | 4     | 0     | 0.01   |
| NTC         | 1      | 1       | 2     | 0     | 0.01   |
| Western ... | 1      | 1       | 1     | 0     | 0.01   |
| EMTEC       | 2      | 2       | 1     | 0     | 0.01   |
| GLOWAY      | 1      | 1       | 1     | 0     | 0.00   |
| Kllisre     | 1      | 2       | 1     | 0     | 0.00   |
| AGI         | 1      | 1       | 0     | 0     | 0.00   |
| POWER X     | 1      | 1       | 0     | 0     | 0.00   |
| Yangtze ... | 1      | 1       | 0     | 0     | 0.00   |

