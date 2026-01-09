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

Total drives: 285751.

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
| Hitachi   | HUA7275SASUN750G   | 752 GB | 2       | 5915  | 0     | 16.21  |
| HP        | GB0160EAFJE        | 160 GB | 2       | 3447  | 0     | 9.44   |
| WDC       | WD6400AAVS-00G9B0  | 640 GB | 2       | 3191  | 0     | 8.74   |
| WDC       | WD5000AAKS-60A7B0  | 500 GB | 2       | 3047  | 0     | 8.35   |
| WDC       | WD20EZRX-19D8PB0   | 2 TB   | 3       | 3026  | 0     | 8.29   |
| HGST      | HUP722020APA330    | 2 TB   | 2       | 2688  | 0     | 7.36   |
| HPE       | MB0500EBNCR        | 500 GB | 5       | 2835  | 183   | 7.34   |
| Hitachi   | HUA7210SASUN1.0T   | 1 TB   | 12      | 2672  | 0     | 7.32   |
| Hitachi   | HUA721075KLA330    | 752 GB | 4       | 3103  | 2     | 7.30   |
| Toshiba   | MB3000GDUPA        | 3 TB   | 4       | 2657  | 0     | 7.28   |
| WDC       | WD4000FYYZ-50UL1B0 | 4 TB   | 7       | 2818  | 1     | 7.17   |
| WDC       | WD7500AAVS-00D7B0  | 752 GB | 3       | 3077  | 1     | 7.12   |
| WDC       | WD1000FYPS-01ZKB0  | 1 TB   | 3       | 2471  | 0     | 6.77   |
| Hitachi   | HDS7216SBSUN160G   | 160 GB | 2       | 4110  | 2     | 6.76   |
| Hitachi   | HUA722020ALA330... | 2 TB   | 2       | 2417  | 0     | 6.62   |
| HP        | GB0500EAFYL        | 500 GB | 3       | 2738  | 1     | 6.58   |
| WDC       | WD1002FBYS-50A6B0  | 1 TB   | 2       | 2401  | 0     | 6.58   |
| Seagate   | ST3000VM002-1F316N | 3 TB   | 2       | 2381  | 0     | 6.53   |
| Toshiba   | MK2002TSKB         | 2 TB   | 11      | 2367  | 2     | 6.49   |
| WDC       | WD800JD-75MSA1     | 80 GB  | 2       | 2361  | 0     | 6.47   |
| WDC       | WD2500AAJS-07VWA0  | 250 GB | 2       | 2354  | 0     | 6.45   |
| WDC       | WD5001AALS-00J7B0  | 500 GB | 2       | 2335  | 0     | 6.40   |
| Seagate   | ST4000DX000-1CL160 | 4 TB   | 2       | 2334  | 0     | 6.40   |
| Seagate   | ST6000DM001-1XY17Z | 6 TB   | 10      | 2322  | 0     | 6.36   |
| WDC       | WD2502ABYS-18B7A0  | 250 GB | 13      | 2969  | 2     | 6.32   |
| WDC       | WD5000AAKS-75YGA0  | 500 GB | 3       | 2294  | 0     | 6.29   |
| Hitachi   | HDS724040ALE640    | 4 TB   | 20      | 2357  | 69    | 6.26   |
| Seagate   | ST4000DM000-1CD168 | 4 TB   | 2       | 2274  | 0     | 6.23   |
| Hitachi   | HUA721050KLA330    | 500 GB | 7       | 2259  | 0     | 6.19   |
| HGST      | MB6000GEBTP        | 6 TB   | 3       | 2206  | 0     | 6.04   |
| WDC       | WD1001FALS-00K1B0  | 1 TB   | 2       | 2199  | 0     | 6.02   |
| HP        | MB2000EAZNL        | 2 TB   | 3       | 2181  | 0     | 5.98   |
| Hitachi   | HUA722020ALA330    | 2 TB   | 41      | 2786  | 57    | 5.96   |
| WDC       | WD1002FBYS-01A6B0  | 1 TB   | 14      | 3114  | 146   | 5.94   |
| WDC       | WD10EVDS-63N5B1    | 1 TB   | 6       | 2535  | 2     | 5.93   |
| WDC       | WD2502ABYS-02B7A0  | 256 GB | 19      | 2726  | 5     | 5.81   |
| WDC       | WD20EADS-32S2B0    | 2 TB   | 3       | 2484  | 4     | 5.81   |
| WDC       | WD1003FBYX-01Y7B2  | 1 TB   | 3       | 2660  | 1     | 5.81   |
| WDC       | WD5000ABYS-01TNA0  | 500 GB | 2       | 2117  | 0     | 5.80   |
| WDC       | WD1002FBYS-05A6B0  | 1 TB   | 11      | 2985  | 28    | 5.80   |
| WDC       | WD3200AVJB-63J5A0  | 320 GB | 2       | 2113  | 0     | 5.79   |
| Hitachi   | HDS5C3030ALA630    | 3 TB   | 19      | 2358  | 2     | 5.79   |
| WDC       | WD3200KS-00PFB0    | 320 GB | 7       | 2297  | 14    | 5.77   |
| Seagate   | ST6000NM0125-1Y... | 6 TB   | 3       | 2104  | 0     | 5.76   |
| WDC       | WD3200AACS-00M6B0  | 320 GB | 2       | 2575  | 5     | 5.73   |
| Hitachi   | HUA722020ALA330... | 2 TB   | 2       | 2087  | 0     | 5.72   |
| WDC       | WD6400AAKS-40H2B0  | 640 GB | 11      | 2473  | 77    | 5.71   |
| WDC       | WD3000HLFS-01G6U1  | 304 GB | 2       | 2066  | 0     | 5.66   |
| Samsung   | HE160HJ            | 160 GB | 3       | 3337  | 339   | 5.66   |
| Hitachi   | HUA723030ALA640... | 3 TB   | 2       | 2062  | 0     | 5.65   |
| IBM/Hi... | IC35L120AVV207-0   | 128 GB | 2       | 2350  | 1     | 5.59   |
| WDC       | WD3000BLFS-01YBU0  | 304 GB | 6       | 2016  | 0     | 5.52   |
| Seagate   | ST1000NM0053-1C... | 1 TB   | 3       | 2006  | 0     | 5.50   |
| Hitachi   | HUA721010KLA330    | 1 TB   | 41      | 2504  | 53    | 5.49   |
| Seagate   | ST5000NM0084-1H... | 5 TB   | 2       | 1991  | 0     | 5.46   |
| Seagate   | ST31000340NS EIT   | 1 TB   | 2       | 1989  | 0     | 5.45   |
| WDC       | WD5000AUDX-73H9TY0 | 500 GB | 2       | 1985  | 0     | 5.44   |
| WDC       | WD6401AALS-00E8B0  | 640 GB | 7       | 1975  | 0     | 5.41   |
| WDC       | WD5000BHTZ-04JCPV0 | 500 GB | 2       | 1970  | 0     | 5.40   |
| WDC       | WD2500KS-22MJB0    | 250 GB | 2       | 1943  | 0     | 5.32   |
| HPE       | MB8000GEQUU        | 8 TB   | 3       | 1926  | 0     | 5.28   |
| WDC       | WD400BD-55MTA1     | 40 GB  | 2       | 1922  | 0     | 5.27   |
| WDC       | WD3000GLFS-01F8U0  | 304 GB | 10      | 2335  | 116   | 5.25   |
| WDC       | WD5000BUCT-63PUZY0 | 500 GB | 4       | 2078  | 1     | 5.24   |
| WDC       | WD5000AAKX-753CA0  | 500 GB | 4       | 1912  | 0     | 5.24   |
| WDC       | WD4000AAJS-22YFA0  | 400 GB | 2       | 1904  | 0     | 5.22   |
| HGST      | HUS726060ALA640    | 6 TB   | 7       | 2215  | 1     | 5.20   |
| WDC       | WD5000AVVS-63ZWB0  | 500 GB | 8       | 2405  | 6     | 5.19   |
| Hitachi   | HDS722020ALA330... | 2 TB   | 4       | 2606  | 73    | 5.18   |
| HGST      | HDN728080ALE604    | 8 TB   | 16      | 1882  | 0     | 5.16   |
| WDC       | WD15EARS-32MVWB0   | 1.5 TB | 5       | 1875  | 0     | 5.14   |
| Seagate   | ST3160828AS        | 160 GB | 2       | 1874  | 0     | 5.14   |
| WDC       | WD5000BHTZ-04JCPV1 | 500 GB | 5       | 2448  | 168   | 5.11   |
| WDC       | WD1003FBYX-50Y7B1  | 1 TB   | 5       | 1862  | 0     | 5.10   |
| Seagate   | ST2000NX0423       | 2 TB   | 5       | 1853  | 0     | 5.08   |
| WDC       | WD10EACS-00C7B0    | 1 TB   | 9       | 1844  | 0     | 5.05   |
| HP        | GB0500C4413        | 500 GB | 3       | 1829  | 0     | 5.01   |
| WDC       | WD5000KMVV-11TK7S1 | 500 GB | 2       | 1815  | 0     | 4.98   |
| Hitachi   | HUS724020ALA640    | 2 TB   | 4       | 1797  | 0     | 4.92   |
| Seagate   | ST5000AS0011-1L... | 5 TB   | 8       | 2013  | 127   | 4.92   |
| HGST      | HUH728080ALE604    | 8 TB   | 33      | 2111  | 5     | 4.92   |
| HGST      | HUS726060ALE610    | 6 TB   | 39      | 1916  | 5     | 4.91   |
| WDC       | WD80PUZX-64NEAY0   | 8 TB   | 4       | 1788  | 0     | 4.90   |
| WDC       | WD2500BMVV-11DCLS0 | 250 GB | 3       | 1781  | 0     | 4.88   |
| WDC       | WD2502ABYS-23B7... | 250 GB | 10      | 2101  | 3     | 4.87   |
| WDC       | WD20NPVX-00EA4T0   | 2 TB   | 36      | 1941  | 2     | 4.84   |
| HPE       | MM2000GEFRA        | 2 TB   | 4       | 1765  | 0     | 4.84   |
| HGST      | HDN724030ALE640    | 3 TB   | 33      | 1843  | 4     | 4.81   |
| HP        | GB0250EAFYK        | 250 GB | 8       | 2521  | 284   | 4.81   |
| Samsung   | HM161HI            | 160 GB | 2       | 1753  | 0     | 4.80   |
| Hitachi   | HDS723030ALA640    | 3 TB   | 45      | 2059  | 36    | 4.78   |
| WDC       | WD30EURX-63T0FY0   | 3 TB   | 4       | 1953  | 3     | 4.77   |
| Seagate   | ST6000NM0024       | 6 TB   | 6       | 1735  | 0     | 4.76   |
| WDC       | WD8002FRYZ-01FF2B0 | 8 TB   | 2       | 1735  | 0     | 4.75   |
| WDC       | WD3000HLFS-01G6U4  | 304 GB | 6       | 1723  | 0     | 4.72   |
| WDC       | WD5000AAKS-75A7B2  | 500 GB | 9       | 1983  | 2     | 4.71   |
| WDC       | WD1001FALS-41K1B0  | 1 TB   | 3       | 1715  | 0     | 4.70   |
| WDC       | WD400JB-00ENA0     | 40 GB  | 3       | 2383  | 6     | 4.69   |
| Seagate   | ST3250620NS        | 250 GB | 29      | 2221  | 263   | 4.68   |
| Hitachi   | HUA723020ALA640    | 2 TB   | 61      | 1894  | 1     | 4.64   |
| Samsung   | SP0411N            | 40 GB  | 2       | 3755  | 9     | 4.62   |
| Seagate   | ST9500320AS        | 500 GB | 2       | 1684  | 0     | 4.62   |
| Toshiba   | HDWT31A            | 10 TB  | 2       | 1677  | 0     | 4.59   |
| Hitachi   | HCC545025B9A300    | 250 GB | 4       | 1673  | 0     | 4.59   |
| Hitachi   | HUA721010KLA330... | 1 TB   | 2       | 1934  | 3     | 4.56   |
| WDC       | WD30EFRX-68AX9N0   | 3 TB   | 103     | 2149  | 32    | 4.54   |
| WDC       | WD10EACS-32ZJB0    | 1 TB   | 5       | 2407  | 5     | 4.52   |
| WDC       | WD2500YS-01SHB0    | 256 GB | 5       | 1693  | 6     | 4.50   |
| Toshiba   | MG04ACA400EY       | 4 TB   | 2       | 1642  | 0     | 4.50   |
| HGST      | HUH728060ALE600    | 6 TB   | 4       | 1641  | 0     | 4.50   |
| WDC       | WD1001FALS-00Y6A0  | 1 TB   | 15      | 1703  | 32    | 4.49   |
| WDC       | WD25EZRS-00J99B0   | 2.5 TB | 3       | 2847  | 13    | 4.48   |
| WDC       | WD5000AAVS-00G9B0  | 500 GB | 10      | 1761  | 1     | 4.47   |
| HGST      | HUS728T8TALE600    | 8 TB   | 18      | 1629  | 0     | 4.46   |
| Samsung   | HE103UJ            | 1 TB   | 4       | 2284  | 1     | 4.46   |
| WDC       | WD2500AAJS-62B4A0  | 250 GB | 2       | 1624  | 0     | 4.45   |
| WDC       | WD5000AAKS-07A7B2  | 500 GB | 3       | 2164  | 7     | 4.45   |
| Seagate   | ST2000NC000-1CX164 | 2 TB   | 3       | 2487  | 125   | 4.42   |
| Seagate   | ST8000NC0002-1X... | 8 TB   | 3       | 1641  | 28    | 4.40   |
| WDC       | WD15EARS-19MVWB0   | 1.5 TB | 4       | 1777  | 327   | 4.39   |
| Samsung   | SP1624N            | 160 GB | 3       | 1601  | 0     | 4.39   |
| WDC       | WD3000F9YZ-09N20L1 | 3 TB   | 7       | 1830  | 1     | 4.38   |
| WDC       | WD5000AUDX-57WNHY0 | 500 GB | 2       | 1594  | 0     | 4.37   |
| WDC       | WD40EZRX-00MVLB1   | 4 TB   | 2       | 1590  | 0     | 4.36   |
| WDC       | WD10EACS-00ZJB0    | 1 TB   | 21      | 1807  | 33    | 4.35   |
| WDC       | WD1001FALS-41Y6A1  | 1 TB   | 11      | 1756  | 4     | 4.35   |
| WDC       | WD6400AAKS-41H2B0  | 640 GB | 4       | 1581  | 0     | 4.33   |
| WDC       | WD101KRYZ-01JPDB1  | 10 TB  | 9       | 1577  | 0     | 4.32   |
| Seagate   | ST4000VN000-1H4168 | 4 TB   | 48      | 1727  | 132   | 4.28   |
| HGST      | HUS724020ALE640    | 2 TB   | 15      | 1561  | 0     | 4.28   |
| WDC       | WD8001FFWX-68J1UN0 | 8 TB   | 14      | 1559  | 0     | 4.27   |
| WDC       | WD1003FBYX-88 LEN  | 1 TB   | 4       | 1743  | 1     | 4.27   |
| Seagate   | ST3400820AS        | 400 GB | 4       | 1957  | 252   | 4.27   |
| WDC       | WD5002ABYS-02B1B0  | 500 GB | 36      | 2202  | 7     | 4.26   |
| Seagate   | ST8000NM0045-1R... | 8 TB   | 8       | 1802  | 31    | 4.26   |
| HGST      | HUS724020ALA640    | 2 TB   | 77      | 1603  | 6     | 4.25   |
| WDC       | WD5000AAKS-40YGA1  | 500 GB | 3       | 1549  | 0     | 4.25   |
| Toshiba   | MC04ACA200E        | 2 TB   | 2       | 1548  | 0     | 4.24   |
| WDC       | WD5000LUCT-63Y8HY0 | 500 GB | 3       | 1547  | 0     | 4.24   |
| WDC       | WD20EADS-42R6B0    | 2 TB   | 2       | 1547  | 0     | 4.24   |
| HGST      | HDN724040ALE640    | 4 TB   | 70      | 1576  | 29    | 4.23   |
| WDC       | WD1002FBYS-02A6B0  | 1 TB   | 35      | 2103  | 75    | 4.23   |
| Hitachi   | HDT721075SLA360    | 752 GB | 3       | 1538  | 0     | 4.22   |
| WDC       | WD2502ABYS-01B7A0  | 256 GB | 7       | 2013  | 1     | 4.21   |
| Seagate   | ST3750641NS EIT    | 752 GB | 2       | 2427  | 2     | 4.21   |
| Seagate   | ST1000NC000-1CX162 | 1 TB   | 4       | 2282  | 223   | 4.18   |
| WDC       | WD2502ABYS-23B7... | 250 GB | 2       | 1522  | 0     | 4.17   |
| Samsung   | HE253GJ            | 250 GB | 3       | 2214  | 1     | 4.17   |
| WDC       | WD10EAVS-32D7B1    | 1 TB   | 9       | 1939  | 44    | 4.16   |
| WDC       | WD2500YD-01NVB1    | 256 GB | 4       | 1798  | 2     | 4.15   |
| Seagate   | ST4000NM0024-1H... | 4 TB   | 9       | 1508  | 0     | 4.13   |
| WDC       | WD80EFAX-68LHPN0   | 8 TB   | 51      | 1508  | 0     | 4.13   |
| WDC       | WD10EZEX-19M2NA0   | 1 TB   | 4       | 1507  | 0     | 4.13   |
| HGST      | HDN726060ALE610    | 6 TB   | 29      | 1812  | 30    | 4.12   |
| HGST      | HUS724030ALA640    | 3 TB   | 40      | 1631  | 2     | 4.11   |
| WDC       | WD2500AAJS-22VWA0  | 250 GB | 3       | 1496  | 0     | 4.10   |
| WDC       | WD10EACS-00D6B0    | 1 TB   | 30      | 1922  | 74    | 4.08   |
| WDC       | WD2003FYYS-18W0B0  | 2 TB   | 13      | 2173  | 131   | 4.08   |
| WDC       | WD3200AAJS-22RYA0  | 320 GB | 7       | 1516  | 1     | 4.07   |
| WDC       | WD5003ABYX-18WERA0 | 500 GB | 37      | 2018  | 31    | 4.07   |
| WDC       | WD101KFBX-68R56N0  | 10 TB  | 15      | 1483  | 0     | 4.06   |
| WDC       | WD15NPVT-00Z2TT0   | 1.5 TB | 4       | 2133  | 19    | 4.06   |
| WDC       | WD1600AVJS-63WNA0  | 160 GB | 3       | 1481  | 0     | 4.06   |
| WDC       | WD2500SD-01KCB0    | 250 GB | 3       | 1973  | 49    | 4.05   |
| HP        | FB080C4080         | 80 GB  | 2       | 1472  | 0     | 4.04   |
| WDC       | WD2000F9YZ-09N20L0 | 2 TB   | 19      | 1799  | 308   | 4.03   |
| WDC       | WD1200JB-00REA0    | 120 GB | 2       | 1515  | 1     | 4.03   |
| WDC       | WD1001FALS-00J7B0  | 1 TB   | 59      | 2056  | 3     | 4.01   |
| Seagate   | ST3000DM003-2AE16L | 3 TB   | 2       | 1463  | 0     | 4.01   |
| WDC       | WD20EARS-42S0XB0   | 2 TB   | 5       | 1462  | 0     | 4.01   |
| Seagate   | ST3400620NS        | 400 GB | 7       | 1959  | 6     | 4.00   |
| Hitachi   | HDS723020BLA642    | 2 TB   | 116     | 1703  | 58    | 3.97   |
| Hitachi   | HUA723030ALA640    | 3 TB   | 67      | 1628  | 35    | 3.95   |
| WDC       | WD1200JS-00SGB0    | 120 GB | 3       | 1437  | 0     | 3.94   |
| HGST      | HUS724040ALA640    | 4 TB   | 62      | 1555  | 66    | 3.93   |
| Seagate   | ST340212AS         | 40 GB  | 6       | 1654  | 35    | 3.92   |
| Seagate   | ST2000NX0253       | 2 TB   | 28      | 1431  | 0     | 3.92   |
| WDC       | WD3200AAJB-00WGA0  | 320 GB | 6       | 1422  | 0     | 3.90   |
| WDC       | WD7500BMVW-11AJGS2 | 752 GB | 3       | 1521  | 1     | 3.88   |
| Seagate   | ST320LT014-9YK142  | 320 GB | 3       | 1414  | 0     | 3.88   |
| WDC       | WD1600JS-75NCB3    | 160 GB | 7       | 1834  | 2     | 3.86   |
| WDC       | WD1500HLFS-01G6U3  | 150 GB | 2       | 1407  | 0     | 3.86   |
| WDC       | WD30EURS-63SPKY0   | 3 TB   | 9       | 1406  | 0     | 3.85   |
| WDC       | WD20EARX-008FB0    | 2 TB   | 31      | 1624  | 5     | 3.85   |
| WDC       | WD40EZRX-22SPEB0   | 4 TB   | 9       | 1910  | 4     | 3.83   |
| WDC       | WD1600YS-01SHB1    | 164 GB | 9       | 1396  | 0     | 3.83   |
| WDC       | WD1600HLHX-60JJPV1 | 160 GB | 2       | 1643  | 2     | 3.83   |
| WDC       | WD10EVDS-63U8B1    | 1 TB   | 3       | 1386  | 0     | 3.80   |
| WDC       | WD740ADFD-00NLR1   | 74 GB  | 2       | 1386  | 0     | 3.80   |
| WDC       | WD2500AAJS-00VWA0  | 250 GB | 3       | 1379  | 0     | 3.78   |
| WDC       | WD1002F9YZ-09H1JL0 | 1 TB   | 2       | 1374  | 0     | 3.76   |
| Toshiba   | MG03ACA400         | 4 TB   | 21      | 1465  | 1     | 3.76   |
| Seagate   | MB3000EBKAB        | 3 TB   | 3       | 1366  | 0     | 3.74   |
| Seagate   | ST3320820AS_P      | 320 GB | 3       | 1366  | 0     | 3.74   |
| WDC       | WD1500HLFS-50G6U1  | 150 GB | 2       | 1364  | 0     | 3.74   |
| WDC       | WD5000AZLX-00K4KA0 | 500 GB | 2       | 1364  | 0     | 3.74   |
| WDC       | WD1002FBYS-18A6B0  | 1 TB   | 8       | 1886  | 8     | 3.74   |
| HPE       | MB4000GCWDC        | 4 TB   | 6       | 1477  | 1     | 3.73   |
| WDC       | WD15EADS-00R6B0    | 1.5 TB | 4       | 1362  | 0     | 3.73   |
| Seagate   | ST32000646NS       | 2 TB   | 4       | 1677  | 1     | 3.73   |
| WDC       | WD1600JS-98MHB0    | 160 GB | 2       | 1358  | 0     | 3.72   |
| Seagate   | ST32000645NS       | 2 TB   | 26      | 1623  | 5     | 3.72   |
| Hitachi   | HMRSK0002TBAT07K   | 2 TB   | 2       | 1355  | 0     | 3.71   |
| WDC       | WD800HLFS-75G6U1   | 80 GB  | 3       | 1354  | 0     | 3.71   |
| HP        | MB2000GCWDA        | 2 TB   | 9       | 1590  | 1     | 3.70   |
| WDC       | WD30EURS-63R8UY0   | 3 TB   | 7       | 1957  | 2     | 3.70   |
| WDC       | WD6401AALS-00J7B0  | 640 GB | 4       | 1845  | 157   | 3.69   |
| Toshiba   | MG03ACA200         | 2 TB   | 11      | 1784  | 101   | 3.69   |
| HGST      | HUS726020ALE614    | 2 TB   | 6       | 1346  | 0     | 3.69   |
| WDC       | WD1003FBYX-12      | 1 TB   | 4       | 1893  | 2     | 3.69   |
| HGST      | HUS726020ALE610    | 2 TB   | 2       | 1345  | 0     | 3.69   |
| WDC       | WD1600AVBS-63SVA0  | 160 GB | 2       | 1344  | 0     | 3.68   |
| Hitachi   | HDS721025CLA682    | 250 GB | 7       | 1342  | 0     | 3.68   |
| WDC       | WD3200JS-55PDB0    | 320 GB | 2       | 1342  | 0     | 3.68   |
| WDC       | WD100PURZ-85W86Y0  | 10 TB  | 8       | 1618  | 1     | 3.67   |
| WDC       | WD10EADS-67M2B0    | 1 TB   | 3       | 1747  | 9     | 3.67   |
| WDC       | WD5000AAKS-60A7B2  | 500 GB | 3       | 1335  | 0     | 3.66   |
| WDC       | WD5001ABYS-01YNA0  | 500 GB | 4       | 1332  | 0     | 3.65   |
| WDC       | WD6002FRYZ-01WD5B0 | 6 TB   | 7       | 1913  | 151   | 3.65   |
| Seagate   | ST6000NM0024-1H... | 6 TB   | 22      | 1763  | 10    | 3.64   |
| WDC       | WD10TMVV-11A27S2   | 1 TB   | 2       | 1342  | 7     | 3.63   |
| WDC       | WD1600YS-18SHB2    | 160 GB | 2       | 2714  | 5     | 3.63   |
| WDC       | WD7501AALS-00E8B0  | 752 GB | 5       | 1832  | 4     | 3.63   |
| WDC       | WD5000AAJS-00TKA0  | 500 GB | 7       | 1324  | 0     | 3.63   |
| HP        | MB1000GCEEK        | 1 TB   | 4       | 1553  | 1     | 3.63   |
| Toshiba   | MG03ACA300         | 3 TB   | 11      | 1859  | 5     | 3.63   |
| HGST      | HUS726020ALA610    | 2 TB   | 21      | 1496  | 7     | 3.62   |
| Seagate   | ST3000NM0053       | 3 TB   | 2       | 1892  | 1     | 3.61   |
| WDC       | WD360GD-00FNA0     | 37 GB  | 5       | 2117  | 1     | 3.60   |
| Fujitsu   | MPE3064AT          | 6 GB   | 2       | 1315  | 0     | 3.60   |
| WDC       | WD1600JD-00HBC0    | 160 GB | 3       | 1534  | 2     | 3.60   |
| Seagate   | ST4000VN0001-1S... | 4 TB   | 6       | 1562  | 75    | 3.60   |
| WDC       | WD10EADS-65M2B0    | 1 TB   | 23      | 1695  | 95    | 3.60   |
| WDC       | WD6002FFWX-68TZ4N0 | 6 TB   | 8       | 1312  | 0     | 3.60   |
| WDC       | WD30EURS-73TLHY0   | 3 TB   | 3       | 1311  | 0     | 3.59   |
| WDC       | WD7500AYYS-01RCA0  | 752 GB | 7       | 1364  | 1     | 3.59   |
| WDC       | WD5000LPVT-60G33T0 | 500 GB | 3       | 1310  | 0     | 3.59   |
| WDC       | WD1500HLFS-01G6U0  | 150 GB | 9       | 1768  | 69    | 3.59   |
| Seagate   | ST4000VM000-1F3168 | 4 TB   | 7       | 1304  | 0     | 3.57   |
| Seagate   | ST2000VM002-9UY166 | 2 TB   | 4       | 2223  | 94    | 3.57   |
| WDC       | WD40NMZW-34GX6S1   | 4 TB   | 2       | 1301  | 0     | 3.57   |
| Seagate   | ST3320620NS        | 320 GB | 8       | 2318  | 128   | 3.56   |
| WDC       | WD10EZEX-75ZF5A0   | 1 TB   | 43      | 1358  | 56    | 3.56   |
| WDC       | WD2003FYYS-02W0B1  | 2 TB   | 42      | 1666  | 6     | 3.56   |
| HGST      | HUH721212ALE601    | 12 TB  | 40      | 1380  | 1     | 3.55   |
| WDC       | WD3200BEKX-66B7WT0 | 320 GB | 2       | 1294  | 0     | 3.55   |
| HP        | MB1000EAMZE        | 1 TB   | 4       | 2174  | 519   | 3.55   |
| Seagate   | ST16000NE000-2W... | 16 TB  | 2       | 1291  | 0     | 3.54   |
| Hitachi   | HDS722020ALA330    | 2 TB   | 86      | 1998  | 115   | 3.54   |
| WDC       | WD5000AAJS-08A8B0  | 500 GB | 3       | 1513  | 1     | 3.53   |
| Seagate   | ST500VT001-1K61... | 500 GB | 2       | 1288  | 0     | 3.53   |
| WDC       | WD3000HLFS-75G6U1  | 304 GB | 9       | 1374  | 1     | 3.53   |
| WDC       | WD15EARS-22Z5B1    | 1.5 TB | 6       | 1287  | 0     | 3.53   |
| WDC       | WD2001FFSX-68JNUN0 | 2 TB   | 2       | 1287  | 0     | 3.53   |
| Seagate   | ST4000NM0085-1Y... | 4 TB   | 3       | 1284  | 0     | 3.52   |
| Seagate   | ST2000DL004 HD2... | 2 TB   | 10      | 1324  | 1     | 3.50   |
| WDC       | WD1601ABYS-18C0A0  | 160 GB | 4       | 1882  | 5     | 3.50   |
| WDC       | WD1001FALS-00U9B0  | 1 TB   | 4       | 2201  | 124   | 3.50   |
| WDC       | WD5000BTKT-40MD3T0 | 500 GB | 3       | 2051  | 1     | 3.49   |
| Hitachi   | HDS723020ALA640    | 2 TB   | 4       | 1268  | 0     | 3.48   |
| WDC       | WD7501AALS-00J7B1  | 752 GB | 12      | 1411  | 1     | 3.46   |
| WDC       | WD10EALX-759BA1    | 1 TB   | 21      | 1613  | 146   | 3.46   |
| Hitachi   | HUA722010ALA330    | 1 TB   | 9       | 1658  | 20    | 3.46   |
| WDC       | WD5000AAKS-40V2B0  | 500 GB | 5       | 1280  | 2     | 3.46   |
| Samsung   | HD204UI            | 2 TB   | 137     | 1488  | 61    | 3.45   |
| HGST      | HUS726060ALE614    | 6 TB   | 19      | 1271  | 30    | 3.45   |
| WDC       | WD20EARS-00J2GB0   | 2 TB   | 32      | 1912  | 100   | 3.44   |
| WDC       | WD1500HLFS-01G6U1  | 150 GB | 7       | 1253  | 0     | 3.43   |
| Hitachi   | HTS421212H9AT00    | 120 GB | 2       | 2184  | 120   | 3.43   |
| WDC       | WD10EACS-00D6B1    | 1 TB   | 16      | 2142  | 124   | 3.42   |
| HPE       | MB4000GEFNA        | 4 TB   | 2       | 2358  | 8     | 3.42   |
| WDC       | WD2003FYYS-02W0B0  | 2 TB   | 27      | 1926  | 129   | 3.42   |
| Hitachi   | HDS5C3015ALA632    | 1.5 TB | 4       | 1382  | 80    | 3.42   |
| WDC       | WD3200AAKS-22SBA0  | 320 GB | 4       | 1244  | 0     | 3.41   |
| Toshiba   | HDWA130            | 3 TB   | 9       | 1243  | 0     | 3.41   |
| WDC       | WD4000F9YZ-09N20L1 | 4 TB   | 19      | 1401  | 1     | 3.40   |
| Seagate   | ST8000AS0002-1N... | 8 TB   | 141     | 1433  | 52    | 3.40   |
| HGST      | HUH728080ALE600    | 8 TB   | 14      | 1384  | 4     | 3.38   |
| Hitachi   | HDS5C3020ALA632    | 2 TB   | 44      | 1582  | 15    | 3.37   |
| WDC       | WD1002FBYS-18W8B0  | 1 TB   | 8       | 1808  | 27    | 3.36   |
| Seagate   | ST14000NM0138-2... | 14 TB  | 17      | 1550  | 4     | 3.36   |
| WDC       | WD3000FYYZ-01UL1B0 | 3 TB   | 5       | 1793  | 2     | 3.35   |
| Seagate   | ST8000VN0022-2E... | 8 TB   | 117     | 1338  | 4     | 3.35   |
| WDC       | WD3000BLFS-60YBU2  | 304 GB | 7       | 2494  | 3     | 3.34   |
| HGST      | HUH728080ALN600    | 8 TB   | 7       | 1218  | 0     | 3.34   |
| Seagate   | ST310211A          | 10 GB  | 2       | 1214  | 0     | 3.33   |
| WDC       | WD1001FALS-00J7B1  | 1 TB   | 56      | 1784  | 23    | 3.33   |
| WDC       | WD5001AALS-00E3A0  | 500 GB | 22      | 1669  | 57    | 3.32   |
| WDC       | WD2001FASS-00W2B0  | 2 TB   | 10      | 1687  | 6     | 3.32   |
| Seagate   | ST3500630NS        | 500 GB | 27      | 1729  | 317   | 3.31   |
| WDC       | WD1005FBYZ-01YCBB1 | 1 TB   | 10      | 1300  | 1     | 3.31   |
| WDC       | WD10JPVT-16A1YT0   | 1 TB   | 4       | 1206  | 0     | 3.31   |
| Toshiba   | DT01ABA100         | 1 TB   | 2       | 1201  | 0     | 3.29   |
| Seagate   | ST4000VX000-1F4168 | 4 TB   | 8       | 1516  | 19    | 3.29   |
| Samsung   | HD502HM            | 500 GB | 2       | 2022  | 1     | 3.28   |
| HGST      | HDN726050ALE610    | 5 TB   | 4       | 1557  | 2     | 3.28   |
| WDC       | WD1600AAJS-61WAA0  | 160 GB | 5       | 1198  | 0     | 3.28   |
| Hitachi   | HDS723020BLE640    | 2 TB   | 15      | 1205  | 1     | 3.27   |
| WDC       | WD2500AAJS-61B4A0  | 250 GB | 2       | 1191  | 0     | 3.27   |
| Seagate   | ST8000VN0002-1Z... | 8 TB   | 7       | 1713  | 67    | 3.26   |
| WDC       | WD1001FALS-41Y6A0  | 1 TB   | 6       | 1282  | 1     | 3.26   |
| Hitachi   | HDS5C3020BLE630    | 2 TB   | 20      | 1429  | 69    | 3.26   |
| WDC       | WD10EADS-00L5B1    | 1 TB   | 146     | 1798  | 31    | 3.25   |
| WDC       | WD7500AADS-00L5B1  | 752 GB | 3       | 1184  | 1     | 3.24   |
| Seagate   | ST3000LM024-2AN17R | 3 TB   | 6       | 1292  | 11    | 3.23   |
| Fujitsu   | MHZ2080BH G2       | 80 GB  | 2       | 1178  | 0     | 3.23   |
| WDC       | WD80EFZX-68UW8N0   | 8 TB   | 44      | 1211  | 2     | 3.23   |
| Hitachi   | HUS724030ALA640    | 3 TB   | 5       | 1449  | 1     | 3.23   |
| WDC       | WD1600AABS-56PRA0  | 160 GB | 3       | 1178  | 0     | 3.23   |
| Hitachi   | HDS728040PLA320    | 40 GB  | 4       | 1548  | 4     | 3.22   |
| WDC       | WD2500JD-40HBC0    | 250 GB | 2       | 1945  | 3     | 3.22   |
| Seagate   | ST2000VN000-1HJ164 | 2 TB   | 19      | 1275  | 160   | 3.22   |
| WDC       | WD2500AAKS-61L9A0  | 250 GB | 5       | 1362  | 2     | 3.22   |
| WDC       | WD1001FALS-40U9B0  | 1 TB   | 7       | 1563  | 1     | 3.22   |
| WDC       | WD30EZRX-00AZ6B0   | 3 TB   | 12      | 1983  | 25    | 3.22   |
| WDC       | WD3200AAJB-56WGA0  | 320 GB | 3       | 1172  | 0     | 3.21   |
| Maxtor    | 7H500F0            | 500 GB | 9       | 1212  | 1     | 3.21   |
| WDC       | WD800BB-60JKC0     | 80 GB  | 2       | 1292  | 2     | 3.21   |
| Maxtor    | 6N040T0            | 40 GB  | 2       | 1842  | 1     | 3.21   |
| Seagate   | ST4000VN000-2AH166 | 4 TB   | 4       | 1166  | 0     | 3.19   |
| WDC       | WD1600JS-75NCB2    | 160 GB | 2       | 1161  | 0     | 3.18   |
| Seagate   | ST9250610NS        | 250 GB | 7       | 1160  | 0     | 3.18   |
| Seagate   | ST1000DX001-1CM... | 1 TB   | 4       | 1283  | 1     | 3.18   |
| WDC       | WD6000HLHX-75JJPV0 | 600 GB | 4       | 1936  | 3     | 3.18   |
| WDC       | WD1001FALS-55J7B0  | 1 TB   | 3       | 1155  | 0     | 3.17   |
| WDC       | WD10EALX-759BA0    | 1 TB   | 5       | 1498  | 2     | 3.16   |
| WDC       | WD2002FAEX-007BA0  | 2 TB   | 107     | 1626  | 18    | 3.16   |
| Hitachi   | HDT721010SLA360    | 1 TB   | 100     | 1828  | 43    | 3.16   |
| Seagate   | ST3000NM0033-9Z... | 3 TB   | 18      | 1285  | 58    | 3.16   |
| Seagate   | ST3000VX006-1HH166 | 3 TB   | 3       | 1169  | 380   | 3.15   |
| HGST      | HDS5C4040ALE630    | 4 TB   | 9       | 1145  | 0     | 3.14   |
| WDC       | WD80PURZ-85YNPY0   | 8 TB   | 2       | 1145  | 0     | 3.14   |
| WDC       | WD1002FAEX-00Y9A0  | 1 TB   | 114     | 1403  | 9     | 3.14   |
| WDC       | WD1003FBYX-18Y7B0  | 1 TB   | 10      | 1727  | 5     | 3.13   |
| HGST      | HDN726040ALE614    | 4 TB   | 28      | 1251  | 12    | 3.13   |
| HGST      | HDS724040ALE640    | 4 TB   | 25      | 1585  | 125   | 3.13   |
| Seagate   | ST4000DM006-2G5107 | 4 TB   | 11      | 1141  | 0     | 3.13   |
| WDC       | WD10EAVS-22D7B0    | 1 TB   | 4       | 1775  | 4     | 3.13   |
| HGST      | HUS724030ALA640... | 3 TB   | 2       | 1138  | 0     | 3.12   |
| WDC       | WD2500JS-00MHB0    | 250 GB | 6       | 1191  | 1     | 3.12   |
| WDC       | WD7500AACS-00D6B0  | 752 GB | 3       | 1244  | 3     | 3.12   |
| Seagate   | ST1000NM0008-2F... | 1 TB   | 33      | 1135  | 0     | 3.11   |
| WDC       | WD5003AZEX-00RKKA0 | 500 GB | 2       | 1135  | 0     | 3.11   |
| WDC       | WD5000AAVS-00ZTB0  | 500 GB | 38      | 1391  | 56    | 3.11   |
| Seagate   | ST6000NM0115-1Y... | 6 TB   | 120     | 1262  | 18    | 3.11   |
| WDC       | WD1600JS-88MHB0    | 160 GB | 2       | 1132  | 0     | 3.10   |
| WDC       | WD2500JS-41SGB0    | 250 GB | 2       | 1132  | 0     | 3.10   |
| WDC       | WD6002FZWX-00GBGB0 | 6 TB   | 8       | 1592  | 39    | 3.10   |
| WDC       | WD5000AAVS-00G9B1  | 500 GB | 6       | 1530  | 187   | 3.10   |
| Hitachi   | HUA723030ALA641    | 3 TB   | 21      | 1197  | 2     | 3.09   |
| WDC       | WD10EZEX-07ZF5A0   | 1 TB   | 5       | 1371  | 3     | 3.09   |
| Seagate   | ST3000DM001-1E6166 | 3 TB   | 13      | 1355  | 414   | 3.09   |
| WDC       | WD4002FYYZ-01B7CB1 | 4 TB   | 16      | 1124  | 1     | 3.08   |
| Hitachi   | HDT725040VLA360    | 400 GB | 8       | 1526  | 42    | 3.08   |
| WDC       | WD3000F9YZ-09N20L0 | 3 TB   | 9       | 1754  | 2     | 3.07   |
| WDC       | WD3200AAKS-00G3A0  | 320 GB | 7       | 1120  | 0     | 3.07   |
| Hitachi   | HDS725050KLA360    | 500 GB | 19      | 2223  | 28    | 3.07   |
| WDC       | WD2500BMVU-11A04S0 | 250 GB | 3       | 1119  | 0     | 3.07   |
| WDC       | WUH721414ALE604    | 14 TB  | 29      | 1118  | 1     | 3.06   |
| Seagate   | ST6000AS0002-1N... | 6 TB   | 14      | 1523  | 57    | 3.06   |
| Hitachi   | HDS721010CLA630    | 1 TB   | 27      | 1429  | 114   | 3.06   |
| WDC       | WD2500JS-40MVB1    | 250 GB | 2       | 1115  | 0     | 3.06   |
| WDC       | WD1600AAJS-08WAA0  | 160 GB | 4       | 1256  | 1     | 3.05   |
| WDC       | WD3000HLFS-01G6U3  | 304 GB | 2       | 1113  | 0     | 3.05   |
| WDC       | WD1002FBYS-18W8B1  | 1 TB   | 3       | 1540  | 2     | 3.05   |
| Hitachi   | HCC547550A9E380    | 500 GB | 3       | 1309  | 8     | 3.05   |
| Hitachi   | HDS722516VLSA80    | 164 GB | 5       | 1524  | 2     | 3.04   |
| WDC       | WD5001FZWX-00ZHUA0 | 5 TB   | 7       | 1587  | 18    | 3.04   |
| WDC       | WD800JD-55MSA1     | 80 GB  | 5       | 1109  | 0     | 3.04   |
| Seagate   | ST500DM002-1ER14C  | 500 GB | 7       | 1106  | 0     | 3.03   |
| WDC       | WD20EARX-22PASB0   | 2 TB   | 15      | 1467  | 2     | 3.03   |
| WDC       | WD15EARX-00ZUDB0   | 1.5 TB | 8       | 1311  | 2     | 3.03   |
| Seagate   | ST3000NC002-1DY166 | 3 TB   | 6       | 1353  | 498   | 3.02   |
| Hitachi   | HDS721010KLA330    | 1 TB   | 32      | 1483  | 8     | 3.02   |
| WDC       | WD5000KS-00MNB0    | 500 GB | 4       | 1103  | 0     | 3.02   |
| WDC       | WD7500AALX-009BA0  | 752 GB | 11      | 1098  | 0     | 3.01   |
| Seagate   | ST2000NC001-1DY164 | 2 TB   | 17      | 1398  | 29    | 3.01   |
| WDC       | WD3200KS-75PFB0    | 320 GB | 2       | 1365  | 39    | 3.00   |
| HPE       | MM1000GBKAL        | 1 TB   | 14      | 2050  | 6     | 2.99   |
| WDC       | WD4NPURX-64TPFY0   | 4 TB   | 2       | 1090  | 0     | 2.99   |
| WDC       | WD10EZRX-00DC0B0   | 1 TB   | 11      | 1127  | 1     | 2.98   |
| WDC       | WD1200JD-00HBB0    | 120 GB | 11      | 1699  | 122   | 2.97   |
| Hitachi   | HDT722520DLAT80    | 200 GB | 4       | 1084  | 0     | 2.97   |
| Seagate   | ST3000VN007-2E4166 | 3 TB   | 31      | 1133  | 1     | 2.96   |
| Toshiba   | MD03ACA300V        | 3 TB   | 2       | 1080  | 0     | 2.96   |
| Toshiba   | MQ03ABB200         | 2 TB   | 2       | 1079  | 0     | 2.96   |
| WDC       | WD7502ABYS-02A6B0  | 752 GB | 2       | 2894  | 4     | 2.95   |
| WDC       | WD2000FYYZ-01UL1B2 | 2 TB   | 12      | 1242  | 1     | 2.95   |
| WDC       | WD1004FBYZ-23YC    | 1 TB   | 4       | 1074  | 0     | 2.94   |
| Seagate   | ST1000NX0423 00... | 1 TB   | 5       | 1073  | 0     | 2.94   |
| WDC       | WD5000AAKS-00V2B0  | 500 GB | 4       | 1202  | 1     | 2.94   |
| WDC       | WD360ADFD-00NLR1   | 37 GB  | 2       | 1073  | 0     | 2.94   |
| WDC       | WD15EVDS-63V9B1    | 1.5 TB | 3       | 1581  | 4     | 2.94   |
| Maxtor    | 6L020J1            | 20 GB  | 3       | 1213  | 2     | 2.93   |
| WDC       | WD1002FAEX-007BA0  | 1 TB   | 7       | 1099  | 1     | 2.93   |
| Hitachi   | HCS5C2020ALA632    | 2 TB   | 4       | 1941  | 3     | 2.93   |
| WDC       | WD20EADS-14R6B0    | 2 TB   | 2       | 2064  | 4     | 2.92   |
| WDC       | WD2003FYYS-01T8B0  | 2 TB   | 2       | 3318  | 5     | 2.92   |
| WDC       | WD3200AAKS-75SBA0  | 320 GB | 6       | 1066  | 0     | 2.92   |
| Seagate   | ST32000641AS       | 2 TB   | 47      | 1592  | 142   | 2.92   |
| WDC       | WD20EURX-57T0FY1   | 2 TB   | 2       | 1064  | 0     | 2.92   |
| WDC       | WD30EFRX-68EUZN0   | 3 TB   | 397     | 1382  | 19    | 2.91   |
| Seagate   | ST10000DM0004      | 10 TB  | 3       | 1063  | 0     | 2.91   |
| HGST      | HUH721010ALE601    | 10 TB  | 12      | 1062  | 0     | 2.91   |
| WDC       | WD5000AAKS-00TMA0  | 500 GB | 20      | 1172  | 3     | 2.91   |
| HP        | FB160C4081         | 160 GB | 2       | 1164  | 44    | 2.91   |
| Seagate   | ST3300822AS        | 304 GB | 4       | 1214  | 602   | 2.91   |
| WDC       | WD10EZEX-00ER1A0   | 1 TB   | 13      | 1206  | 1     | 2.91   |
| WDC       | WD1001FALS-00E3A0  | 1 TB   | 9       | 1498  | 184   | 2.90   |
| HGST      | HMS5C4040ALE640    | 4 TB   | 12      | 1058  | 0     | 2.90   |
| WDC       | WD7500BPVT-35HXZT3 | 752 GB | 5       | 1107  | 1     | 2.90   |
| WDC       | WD10EAVS-00D7B0    | 1 TB   | 28      | 1595  | 5     | 2.90   |
| WDC       | WD2500AAJS-75VWA0  | 250 GB | 3       | 1056  | 0     | 2.89   |
| Toshiba   | MG04ACA600EY       | 6 TB   | 3       | 1055  | 0     | 2.89   |
| Maxtor    | STM3320620AS       | 320 GB | 3       | 1055  | 0     | 2.89   |
| WDC       | WD1003FZEX-00RLFA0 | 1 TB   | 4       | 1055  | 0     | 2.89   |
| WDC       | WD1600JS-60MHB1    | 160 GB | 8       | 1181  | 3     | 2.89   |
| Hitachi   | HUA722020ALA331    | 2 TB   | 50      | 1898  | 67    | 2.89   |
| WDC       | WD40EURX-64WRWY0   | 4 TB   | 6       | 1320  | 1     | 2.89   |
| WDC       | WD20EARX-00PASB0   | 2 TB   | 381     | 1412  | 98    | 2.89   |
| WDC       | WD30EZRS-42KEZB0   | 3 TB   | 4       | 1052  | 0     | 2.88   |
| WDC       | WD2500JS-00MHB1    | 250 GB | 2       | 1052  | 0     | 2.88   |
| Seagate   | ST1000NM0033-9Z... | 1 TB   | 93      | 1282  | 89    | 2.88   |
| Seagate   | ST2000NM0033-9Z... | 2 TB   | 40      | 1235  | 149   | 2.87   |
| WDC       | WD3000BLFS-08YBU0  | 304 GB | 2       | 1048  | 0     | 2.87   |
| WDC       | WD6400AAKS-75A7B0  | 640 GB | 8       | 1238  | 1     | 2.87   |
| Seagate   | ST3000VN000-1HJ166 | 3 TB   | 25      | 1192  | 165   | 2.86   |
| Seagate   | ST3300622AS        | 304 GB | 5       | 1371  | 1     | 2.86   |
| WDC       | WD2003FZEX-00Z4SA0 | 2 TB   | 109     | 1305  | 14    | 2.85   |
| Hitachi   | HDS721075KLA330    | 752 GB | 13      | 1193  | 8     | 2.85   |
| Samsung   | HD160JJ-P          | 160 GB | 20      | 1409  | 306   | 2.85   |
| WDC       | WD10EZEX-00KUWA0   | 1 TB   | 71      | 1151  | 2     | 2.85   |
| Maxtor    | 6H500F0            | 500 GB | 2       | 1037  | 0     | 2.84   |
| WDC       | WD4002FYYZ-01B7CB0 | 4 TB   | 2       | 1036  | 0     | 2.84   |
| HGST      | HMS5C4040BLE640    | 4 TB   | 23      | 1035  | 0     | 2.84   |
| WDC       | WD800BB-75FRA0     | 80 GB  | 2       | 1034  | 0     | 2.83   |
| WDC       | WD5000AVVS-00ZWB0  | 500 GB | 2       | 1033  | 0     | 2.83   |
| Seagate   | ST31000521AS       | 1 TB   | 3       | 1032  | 0     | 2.83   |
| WDC       | WD4004FZWX-00GBGB0 | 4 TB   | 20      | 1277  | 120   | 2.83   |
| WDC       | WD2500JS-75NCB3    | 250 GB | 11      | 1280  | 12    | 2.82   |
| WDC       | WD30EZRX-00DC0B0   | 3 TB   | 108     | 1304  | 29    | 2.82   |
| Hitachi   | HDS722525VLSA80    | 250 GB | 7       | 1148  | 6     | 2.82   |
| WDC       | WD5000AAKS-22YGA0  | 500 GB | 9       | 1195  | 51    | 2.82   |
| WDC       | WD10EURS-730AB1    | 1 TB   | 2       | 1772  | 5     | 2.82   |
| Seagate   | ST1000DL004 HD1... | 1 TB   | 3       | 1297  | 3     | 2.82   |
| Seagate   | ST4000NM0245-1Z... | 4 TB   | 11      | 1206  | 1     | 2.82   |
| WDC       | WD20EURS-73TLHY0   | 2 TB   | 5       | 1665  | 48    | 2.82   |
| Toshiba   | MG04ACA100N        | 1 TB   | 9       | 1233  | 1     | 2.81   |
| HP        | MB2000GCVBR        | 2 TB   | 2       | 1026  | 0     | 2.81   |
| WDC       | WD1002FAEX-00Z3A0  | 1 TB   | 217     | 1341  | 55    | 2.81   |
| WDC       | WD10TMVW-11ZSMS5   | 1 TB   | 34      | 1202  | 117   | 2.81   |
| WDC       | WD2500JS-60NCB1    | 250 GB | 12      | 1143  | 8     | 2.80   |
| Seagate   | ST320413A          | 20 GB  | 2       | 1076  | 2     | 2.80   |
| WDC       | WD800JD-60LUA0     | 80 GB  | 3       | 1020  | 0     | 2.80   |
| WDC       | WD30EZRS-00J99B0   | 3 TB   | 20      | 1521  | 411   | 2.80   |
| WDC       | WD6000HLHX-01JJPV0 | 600 GB | 18      | 1568  | 10    | 2.79   |
| WDC       | WD80EZZX-11CSGA0   | 8 TB   | 21      | 1376  | 60    | 2.79   |
| WDC       | WD400LB-00DNA0     | 40 GB  | 2       | 1103  | 2     | 2.78   |
| WDC       | WD20NMVW-59EDZS3   | 2 TB   | 2       | 1016  | 0     | 2.78   |
| WDC       | WD3000HLFS-01G6U0  | 304 GB | 8       | 1184  | 34    | 2.78   |
| WDC       | WD5000AAKS-402AA0  | 500 GB | 15      | 1373  | 10    | 2.78   |
| WDC       | WD20EZRX-00DC0B0   | 2 TB   | 117     | 1234  | 19    | 2.78   |
| WDC       | WD4000AAKS-00YGA0  | 400 GB | 8       | 1165  | 1     | 2.78   |
| WDC       | WD5000AACS-61M6B2  | 500 GB | 3       | 2013  | 4     | 2.78   |
| WDC       | WD6001F4PZ-49CWHM0 | 6 TB   | 3       | 1755  | 2     | 2.78   |
| WDC       | WD2000JS-22MHB0    | 200 GB | 7       | 1742  | 14    | 2.77   |
| WDC       | WD4000F9YZ-09N20L0 | 4 TB   | 11      | 1735  | 184   | 2.77   |
| WDC       | WD5003ABYX-01WERA2 | 500 GB | 4       | 1011  | 1     | 2.77   |
| Western   | WUH721816ALE6L4    | 16 TB  | 5       | 1007  | 0     | 2.76   |
| WDC       | WD6401AALS-00L3B2  | 640 GB | 44      | 1342  | 26    | 2.76   |
| WDC       | WD1600ADFS-75SLR2  | 160 GB | 2       | 2094  | 102   | 2.75   |
| WDC       | WD25EZRX-00MMMB0   | 2.5 TB | 6       | 1880  | 6     | 2.74   |
| WDC       | WD2000JD-22HBC0    | 200 GB | 4       | 1499  | 3     | 2.74   |
| WDC       | WD800JD-00JNA0     | 80 GB  | 4       | 1336  | 3     | 2.74   |
| Toshiba   | DT01ACA300         | 3 TB   | 311     | 1156  | 53    | 2.74   |
| WDC       | WD8000AARS-00Y5B1  | 800 GB | 5       | 2108  | 10    | 2.74   |
| WDC       | WD6400AAKS-00A7B0  | 640 GB | 23      | 1194  | 3     | 2.74   |
| Hitachi   | HCS5C1010CLA382    | 1 TB   | 9       | 998   | 0     | 2.73   |
| Seagate   | ST1500LM003-9YH148 | 1.5 TB | 2       | 996   | 0     | 2.73   |
| Seagate   | ST3400833AS        | 400 GB | 2       | 996   | 0     | 2.73   |
| WDC       | WD2000FYYZ-05UL1B0 | 2 TB   | 2       | 996   | 0     | 2.73   |
| HGST      | HUH721010ALN600    | 10 TB  | 5       | 995   | 0     | 2.73   |
| WDC       | WD1002F9YZ-09H1JL1 | 1 TB   | 12      | 1244  | 1     | 2.73   |
| WDC       | WD80EMAZ-00WJTA0   | 8 TB   | 106     | 1028  | 3     | 2.72   |
| Hitachi   | HDS723030BLE640    | 3 TB   | 4       | 1045  | 505   | 2.72   |
| Seagate   | ST3500630AS        | 500 GB | 108     | 1517  | 218   | 2.72   |
| WDC       | WD3200JS-63PDB1    | 320 GB | 3       | 1327  | 217   | 2.71   |
| Seagate   | ST3750640A         | 752 GB | 2       | 1355  | 1025  | 2.71   |
| WDC       | WD3200YS-01PGB0    | 320 GB | 5       | 1016  | 1     | 2.71   |
| HGST      | HUS724040ALE640    | 4 TB   | 22      | 988   | 0     | 2.71   |
| Toshiba   | MD04ACA400         | 4 TB   | 43      | 1175  | 177   | 2.70   |
| WDC       | WD6400AAKS-65A7B2  | 640 GB | 48      | 1389  | 13    | 2.70   |
| Toshiba   | MG04ACA400E        | 4 TB   | 23      | 985   | 0     | 2.70   |
| Seagate   | ST3000VX000-1ES166 | 3 TB   | 10      | 984   | 0     | 2.70   |
| WDC       | WD2000JS-22NCB1    | 200 GB | 3       | 1611  | 16    | 2.70   |
| Seagate   | ST1000NX0443       | 1 TB   | 4       | 981   | 0     | 2.69   |
| WDC       | WD20EURX-57T0FY0   | 2 TB   | 2       | 981   | 0     | 2.69   |
| WDC       | WD20EARS-07MVWB0   | 2 TB   | 7       | 1810  | 107   | 2.69   |
| WDC       | WD1600AAJS-22PSA0  | 160 GB | 21      | 1108  | 24    | 2.69   |
| WDC       | WD800JD-08LSA0     | 80 GB  | 15      | 1126  | 2     | 2.68   |

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
| HPE         | 12     | 55      | 1383  | 37    | 2.87   |
| Western     | 1      | 5       | 1007  | 0     | 2.76   |
| HP          | 27     | 131     | 1468  | 99    | 2.56   |
| MaxDigital  | 3      | 10      | 914   | 29    | 1.81   |
| WDC         | 1818   | 40090   | 776   | 39    | 1.58   |
| Apple       | 18     | 566     | 744   | 102   | 1.53   |
| Hitachi     | 255    | 8108    | 870   | 199   | 1.42   |
| HGST        | 92     | 5005    | 671   | 247   | 1.34   |
| Quantum     | 1      | 2       | 483   | 0     | 1.33   |
| Samsung     | 132    | 4473    | 885   | 232   | 1.27   |
| China       | 2      | 5       | 556   | 193   | 1.24   |
| Seagate     | 736    | 40766   | 676   | 165   | 1.22   |
| Magnetic... | 3      | 6       | 540   | 1     | 1.19   |
| MediaMax    | 13     | 36      | 561   | 69    | 1.17   |
| ExcelStor   | 5      | 39      | 888   | 172   | 1.08   |
| Toshiba     | 279    | 13960   | 508   | 97    | 1.04   |
| Colorful    | 1      | 2       | 319   | 0     | 0.88   |
| Lenovo      | 2      | 10      | 303   | 0     | 0.83   |
| DELL        | 1      | 2       | 265   | 0     | 0.73   |
| Fujitsu     | 80     | 1059    | 415   | 126   | 0.67   |
| Maxtor      | 88     | 957     | 536   | 265   | 0.66   |
| IBM/Hitachi | 15     | 56      | 727   | 54    | 0.66   |
| MARSHAL     | 3      | 9       | 339   | 431   | 0.43   |
| IBM         | 1      | 2       | 1494  | 37    | 0.39   |
| Synology    | 2      | 9       | 55    | 0     | 0.15   |
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
| Patriot   | Pyro SE            | 64 GB  | 2       | 3262  | 0     | 8.94   |
| Transcend | 3E128-TS2-550B01   | 100 GB | 16      | 3197  | 1     | 7.88   |
| Samsung   | MO0200EBTJU        | 200 GB | 2       | 2807  | 0     | 7.69   |
| Samsung   | MZ7KM120HAFD-00005 | 120 GB | 2       | 2779  | 0     | 7.61   |
| HP        | VK0480GEYJR        | 480 GB | 2       | 2710  | 0     | 7.43   |
| Samsung   | MZ7WD240HAFV-00003 | 240 GB | 2       | 2706  | 0     | 7.41   |
| Intel     | SSDSC2BB300G4      | 304 GB | 9       | 2534  | 0     | 6.94   |
| Kingston  | SVP100S2512G       | 512 GB | 2       | 2532  | 0     | 6.94   |
| Intel     | SSDSC2BA200G3      | 200 GB | 4       | 2440  | 0     | 6.69   |
| Samsung   | 470 Series SSD     | 256 GB | 3       | 2390  | 0     | 6.55   |
| Samsung   | MZ7KM1T9HAJM-00005 | 1.9 TB | 6       | 2322  | 0     | 6.36   |
| Intel     | SSDSC2BB240G4C     | 240 GB | 2       | 2185  | 0     | 5.99   |
| Corsair   | Force GT           | 50 GB  | 2       | 2183  | 0     | 5.98   |
| Intel     | VK1600GEYJU        | 1.6 TB | 4       | 2171  | 0     | 5.95   |
| Samsung   | MZ7KH3T8HALS-00005 | 3.8 TB | 4       | 2116  | 0     | 5.80   |
| Samsung   | MZ7PD480HAGM-000DA | 480 GB | 2       | 2086  | 0     | 5.72   |
| Kingston  | KC-S44240-6F       | 240 GB | 3       | 2024  | 0     | 5.55   |
| Goodram   | SSD                | 960 GB | 2       | 2023  | 0     | 5.54   |
| Kingston  | SSDNOW             | 32 GB  | 13      | 2060  | 1     | 5.48   |
| Intel     | SSDSC2BB600G4      | 600 GB | 6       | 1992  | 0     | 5.46   |
| Intel     | SSDSC2BB120G4      | 120 GB | 9       | 1980  | 0     | 5.43   |
| Patriot   | Pyro               | 64 GB  | 2       | 1972  | 0     | 5.41   |
| Intel     | SSDSA2SH064G1GC    | 64 GB  | 4       | 1964  | 0     | 5.38   |
| Kingston  | SEDC400S371600G    | 1.6 TB | 2       | 1962  | 0     | 5.38   |
| Samsung   | MZ7KM960HAHP-00005 | 960 GB | 13      | 2028  | 1     | 5.36   |
| Intel     | SSDSC2BB240G4      | 240 GB | 11      | 1951  | 0     | 5.35   |
| Intel     | SSDSA2BW120G3      | 120 GB | 2       | 1950  | 0     | 5.34   |
| Samsung   | MZ7KM240HAGR-0E005 | 240 GB | 4       | 1946  | 0     | 5.33   |
| Intel     | SSDSA2BW600G3D     | 600 GB | 2       | 1942  | 0     | 5.32   |
| Samsung   | MZ7WD240HCFV-00003 | 240 GB | 2       | 1938  | 0     | 5.31   |
| SanDisk   | SD6SB2M256G1022I   | 256 GB | 2       | 1921  | 0     | 5.27   |
| OCZ       | REVODRIVE3         | 120 GB | 8       | 1915  | 0     | 5.25   |
| HP        | VK001920GWSRU      | 1.9 TB | 4       | 1905  | 0     | 5.22   |
| Intel     | SSDSC2BA400G3      | 400 GB | 6       | 1902  | 0     | 5.21   |
| Samsung   | MZ7KM960HMJP0D3    | 960 GB | 2       | 1900  | 0     | 5.21   |
| Samsung   | MZ7KM480HAHP-00005 | 480 GB | 4       | 1887  | 0     | 5.17   |
| Toshiba   | THNSNA240GESK      | 240 GB | 2       | 1882  | 0     | 5.16   |
| Intel     | SSDSC2BB160G4      | 160 GB | 9       | 1875  | 0     | 5.14   |
| Toshiba   | THNSNH060GCST      | 64 GB  | 2       | 1857  | 0     | 5.09   |
| Intel     | SSDSA2MH080G1GC    | 80 GB  | 2       | 1846  | 0     | 5.06   |
| Intel     | SSDSC2BB240G6      | 240 GB | 6       | 1826  | 0     | 5.00   |
| Micron    | M510DC_MTFDDAK2... | 240 GB | 3       | 1807  | 0     | 4.95   |
| Samsung   | MZ7WD480HCGM-00003 | 480 GB | 2       | 2415  | 1     | 4.94   |
| Apacer    | AS681              | 240 GB | 2       | 1797  | 0     | 4.93   |
| Corsair   | Performance Pro    | 256 GB | 2       | 1790  | 0     | 4.90   |
| Corsair   | Force 3 SSD        | 180 GB | 10      | 1943  | 1     | 4.89   |
| Intel     | SSDSC1BG800G4      | 800 GB | 2       | 1777  | 0     | 4.87   |
| Kingston  | SVP100S2128G       | 128 GB | 6       | 1776  | 0     | 4.87   |
| Samsung   | SSD 845DC PRO      | 800 GB | 2       | 2842  | 2     | 4.85   |
| Intel     | SSDSC2KB480G7      | 480 GB | 42      | 1897  | 1     | 4.83   |
| Kingston  | SKC400S371T        | 1 TB   | 6       | 1975  | 9     | 4.66   |
| Samsung   | MZ7KH1T9HAJR-00005 | 1.9 TB | 2       | 1700  | 0     | 4.66   |
| Intel     | SSDSC2KB960G7R     | 960 GB | 12      | 2015  | 1     | 4.63   |
| Intel     | SSDSC2KG240G7R     | 240 GB | 3       | 1684  | 0     | 4.61   |
| Samsung   | MZ7LM960HCHP-0Z003 | 960 GB | 3       | 1683  | 0     | 4.61   |
| Samsung   | MO0100EBTJT        | 100 GB | 2       | 1671  | 0     | 4.58   |
| Intel     | SSDSC2BB016T4      | 1.6 TB | 4       | 1923  | 1     | 4.49   |
| Samsung   | MZNLN512HCJH-00000 | 512 GB | 2       | 1637  | 0     | 4.49   |
| Intel     | SSDSC2BB080G4      | 80 GB  | 16      | 1625  | 0     | 4.45   |
| Micron    | MTFDDAK960TDD      | 960 GB | 2       | 1623  | 0     | 4.45   |
| Intel     | SSDSC2BX400G4      | 400 GB | 3       | 1622  | 0     | 4.45   |
| Intel     | SSDSC2BB800G4      | 800 GB | 5       | 1587  | 0     | 4.35   |
| OCZ       | AGILITY2           | 64 GB  | 6       | 1582  | 0     | 4.34   |
| Samsung   | MZ7LM1T9HMJP-00005 | 1.9 TB | 2       | 1575  | 0     | 4.32   |
| Intel     | SSDMCEAC120B3      | 120 GB | 5       | 1834  | 1     | 4.27   |
| Samsung   | SSD PM851a 2.5 7mm | 1 TB   | 3       | 1544  | 0     | 4.23   |
| OCZ       | VERTEX2            | 40 GB  | 2       | 1543  | 0     | 4.23   |
| Intel     | SSDSC2BX480G4K     | 480 GB | 4       | 1541  | 0     | 4.22   |
| Intel     | SSDSC2BB120G6      | 120 GB | 5       | 1539  | 0     | 4.22   |
| Seagate   | ST240HM000-1G5152  | 240 GB | 3       | 2387  | 1     | 4.21   |
| SanDisk   | SDSA6DM-016G-1006  | 16 GB  | 5       | 1522  | 0     | 4.17   |
| Samsung   | MZ7KM960HMJP-00005 | 960 GB | 13      | 1512  | 0     | 4.14   |
| Micron    | M500_MTFDDAK960MAV | 960 GB | 5       | 2308  | 2     | 4.14   |
| Intel     | SSDSC2BA100G3      | 100 GB | 27      | 1573  | 1     | 4.14   |
| Phison    | SSBP064GTMC0-S91   | 64 GB  | 2       | 1507  | 0     | 4.13   |
| Intel     | SSDSC2BB480G7      | 480 GB | 26      | 1932  | 2     | 4.09   |
| Intel     | SSDSC2BP480G4      | 480 GB | 14      | 1501  | 1     | 4.09   |
| Intel     | SSDSC2BB800G6      | 800 GB | 22      | 1564  | 1     | 4.07   |
| Samsung   | MZ7LM240HCGR-00003 | 240 GB | 3       | 1479  | 0     | 4.05   |
| OCZ       | VERTEX v1.10       | 64 GB  | 3       | 1655  | 1     | 4.05   |
| Samsung   | MZ7LM960HCHP-00003 | 960 GB | 6       | 1469  | 0     | 4.03   |
| Samsung   | MZ7PD128HCFV-000H7 | 128 GB | 4       | 1466  | 0     | 4.02   |
| Kingston  | SVP100S296G        | 96 GB  | 6       | 1442  | 0     | 3.95   |
| Samsung   | SSD 850 PRO        | 1 TB   | 107     | 1527  | 12    | 3.91   |
| Toshiba   | THNSF8120CCSE      | 120 GB | 2       | 1423  | 0     | 3.90   |
| Intel     | SSDSA2CW600G3      | 600 GB | 3       | 1409  | 0     | 3.86   |
| Intel     | SSDSC2BB480G7K     | 480 GB | 2       | 1403  | 0     | 3.85   |
| Samsung   | SSD 840 EVO        | 752 GB | 12      | 1420  | 2     | 3.79   |
| ADATA     | SSD DM900 256GB... | 256 GB | 2       | 1380  | 0     | 3.78   |
| Samsung   | MZ7LN512HMJP-000L1 | 512 GB | 2       | 1380  | 0     | 3.78   |
| Samsung   | MZ7WD960HMHP-00003 | 880 GB | 2       | 2062  | 1     | 3.77   |
| Kingston  | SVP100S264G        | 64 GB  | 5       | 1369  | 0     | 3.75   |
| FASTDISK  | SSD 32G            | 32 GB  | 2       | 1365  | 0     | 3.74   |
| Toshiba   | THNSNJ256GCST      | 256 GB | 7       | 1360  | 0     | 3.73   |
| SanDisk   | SD8SB8U128G1122    | 128 GB | 2       | 1359  | 0     | 3.72   |
| Corsair   | Force 3 SSD        | 240 GB | 16      | 1454  | 66    | 3.72   |
| Intel     | SSDSA2BZ300G3S     | 304 GB | 3       | 1349  | 0     | 3.70   |
| Toshiba   | THNSNH256GCST      | 256 GB | 6       | 1345  | 0     | 3.69   |
| Corsair   | Neutron GTX SSD    | 480 GB | 2       | 1345  | 0     | 3.69   |
| SuperM... | SSD                | 128 GB | 2       | 1778  | 1     | 3.66   |
| Intel     | SSDSC2BB800G7      | 800 GB | 37      | 1620  | 1     | 3.63   |
| Micron    | 1100 SATA          | 1 TB   | 2       | 1313  | 0     | 3.60   |
| SanDisk   | SD8SB8U512G1001    | 512 GB | 2       | 1312  | 0     | 3.60   |
| Mushkin   | MKNSSDEC120GB      | 120 GB | 4       | 1312  | 0     | 3.60   |
| Samsung   | SSD 850 EVO        | 2 TB   | 38      | 1312  | 0     | 3.60   |
| Samsung   | SSD 840 EVO        | 1 TB   | 96      | 1413  | 14    | 3.59   |
| Samsung   | MZ7GE960HMHP-00003 | 960 GB | 2       | 2613  | 508   | 3.59   |
| Intel     | SSDSC2BB480G4      | 480 GB | 12      | 1311  | 0     | 3.59   |
| SanDisk   | SD8SB8U1T00        | 1 TB   | 2       | 1308  | 0     | 3.59   |
| SanDisk   | SDSSDXP480G        | 480 GB | 3       | 1306  | 0     | 3.58   |
| Mushkin   | MKNSSDCR240GB-7    | 240 GB | 2       | 1302  | 0     | 3.57   |
| Intel     | SSDSC2BB240G7      | 240 GB | 10      | 1301  | 0     | 3.57   |
| Samsung   | MZ7PC256HAFU-000L7 | 256 GB | 5       | 1296  | 0     | 3.55   |
| Kingston  | SNVP325S2128GB     | 128 GB | 4       | 1294  | 0     | 3.55   |
| Intel     | SSDSA2SH032G1GN    | 32 GB  | 4       | 1293  | 0     | 3.54   |
| Mushkin   | MKNSSDCR60GB       | 64 GB  | 2       | 1435  | 3     | 3.53   |
| SanDisk   | SD5SE2128G1002E    | 128 GB | 4       | 1285  | 0     | 3.52   |
| Intel     | SSDSC2BB480G6      | 480 GB | 3       | 1280  | 0     | 3.51   |
| Intel     | SSDSC2KB240G7      | 240 GB | 5       | 1518  | 1     | 3.48   |
| Samsung   | MZ7KH480HAHQ0D3    | 480 GB | 3       | 1261  | 0     | 3.46   |
| Toshiba   | THNSNJ120PCSZ      | 120 GB | 2       | 1255  | 0     | 3.44   |
| Samsung   | MZ7KM480HMHQ-00005 | 480 GB | 5       | 1243  | 0     | 3.41   |
| OCZ       | VERTEX PLUS R2     | 64 GB  | 4       | 1242  | 0     | 3.40   |
| Seagate   | XF1230-1A0960      | 960 GB | 2       | 1236  | 0     | 3.39   |
| OCZ       | VERTEX2            | 64 GB  | 26      | 1269  | 12    | 3.39   |
| Intel     | SSDSC2CW240A3      | 240 GB | 55      | 1257  | 1     | 3.36   |
| Gigabyte  | GP-GSTFS30512GTTD  | 512 GB | 2       | 1226  | 0     | 3.36   |
| Samsung   | SSD 830 Series     | 512 GB | 15      | 1288  | 135   | 3.35   |
| Intel     | SSDSC2CW180A3      | 180 GB | 25      | 1220  | 0     | 3.34   |
| Samsung   | MZ7LN256HMJP-00000 | 256 GB | 13      | 1218  | 0     | 3.34   |
| SK hynix  | SC300B SATA        | 256 GB | 3       | 1214  | 0     | 3.33   |
| OCZ       | VERTEX2            | 120 GB | 20      | 1205  | 0     | 3.30   |
| OCZ       | AGILITY4           | 128 GB | 10      | 1201  | 0     | 3.29   |
| HP        | VK0480GEQNB        | 480 GB | 5       | 1672  | 2     | 3.29   |
| Innodisk  | Corp. - mSATA 3ME3 | 32 GB  | 2       | 1195  | 0     | 3.28   |
| Corsair   | Force GT           | 180 GB | 4       | 1193  | 0     | 3.27   |
| Patriot   | Ignite             | 480 GB | 4       | 1192  | 0     | 3.27   |
| HP        | VK000240GWSRQ      | 240 GB | 6       | 1189  | 0     | 3.26   |
| Corsair   | Neutron XTI SSD    | 480 GB | 3       | 1188  | 0     | 3.26   |
| HPE       | MK001920GWXFK      | 1.9 TB | 3       | 1185  | 0     | 3.25   |
| Micron    | M600_MTFDDAK1T0MBF | 1 TB   | 14      | 1206  | 7     | 3.24   |
| SanDisk   | SD7SB6S128G1001    | 128 GB | 4       | 1179  | 0     | 3.23   |
| OCZ       | TRION150           | 960 GB | 2       | 1176  | 0     | 3.22   |
| KingDian  | N400               | 240 GB | 2       | 1174  | 0     | 3.22   |
| Samsung   | MZHPV256HDGL-000H1 | 256 GB | 2       | 1172  | 0     | 3.21   |
| Seagate   | ST480HM000-1G5162  | 480 GB | 2       | 1282  | 1     | 3.20   |
| Micron    | M500_MTFDDAK480MAV | 480 GB | 7       | 1584  | 4     | 3.20   |
| Samsung   | MZMTE512HMHP-000L1 | 512 GB | 3       | 1165  | 0     | 3.19   |
| Micron    | 5200_MTFDDAK960TDN | 960 GB | 5       | 1158  | 0     | 3.17   |
| Toshiba   | THNSNC064GMMJ      | 64 GB  | 6       | 1151  | 0     | 3.15   |
| Micron    | C400-MTFDDAC128MAM | 128 GB | 5       | 1150  | 0     | 3.15   |
| Samsung   | SSD PM871a 2.5 7mm | 256 GB | 4       | 1140  | 0     | 3.13   |
| Micron    | 5300_MTFDDAK480TDT | 480 GB | 2       | 1131  | 0     | 3.10   |
| PNY       | CS1311 960GB SSD   | 960 GB | 4       | 1129  | 0     | 3.09   |
| Intel     | SSDSC2BB150G7      | 150 GB | 36      | 1252  | 1     | 3.08   |
| Toshiba   | THNS128GG4BAAA-... | 128 GB | 6       | 1119  | 0     | 3.07   |
| Micron    | 5200_MTFDDAK7T6TDC | 7.6 TB | 15      | 1360  | 1     | 3.06   |
| Toshiba   | TL100              | 120 GB | 5       | 1115  | 0     | 3.06   |
| Intel     | SSDSA2CW080G3      | 80 GB  | 27      | 1286  | 1     | 3.06   |
| PNY       | CS2211 240GB SSD   | 240 GB | 3       | 1112  | 0     | 3.05   |
| Seagate   | IronWolf ZA250N... | 250 GB | 2       | 1111  | 0     | 3.04   |
| Intel     | LK0200GEYMR        | 200 GB | 5       | 1109  | 0     | 3.04   |
| Patriot   | Blast              | 480 GB | 3       | 1106  | 0     | 3.03   |
| Corsair   | Force GS           | 480 GB | 3       | 1884  | 15    | 3.02   |
| Hyundai   | 120GB SSD          | 120 GB | 4       | 1101  | 0     | 3.02   |
| Kingston  | RBU-SC400S37256G   | 256 GB | 2       | 1095  | 0     | 3.00   |
| Samsung   | SSD 840 EVO        | 500 GB | 169     | 1164  | 25    | 2.99   |
| Mushkin   | MKNSSDCR120GB      | 120 GB | 9       | 1306  | 4     | 2.98   |
| Samsung   | SSD 830 Series     | 128 GB | 118     | 1140  | 35    | 2.98   |
| Corsair   | Force GS           | 180 GB | 3       | 1087  | 0     | 2.98   |
| Apple     | SSD SM1024F        | 1 TB   | 25      | 1159  | 1     | 2.97   |
| Samsung   | MZ7LN512HCHP-00000 | 512 GB | 3       | 1076  | 0     | 2.95   |
| OCZ       | REVODRIVE350       | 120 GB | 4       | 1073  | 0     | 2.94   |
| Toshiba   | THNSNC128GMMJ      | 128 GB | 7       | 1071  | 0     | 2.94   |
| Samsung   | SSD PB22-JS3 FD... | 256 GB | 5       | 1071  | 0     | 2.93   |
| Intel     | SSDSC2BB016T7      | 1.6 TB | 4       | 1721  | 2     | 2.93   |
| KingSpec  | SPK-SF12-M120      | 120 GB | 2       | 1069  | 0     | 2.93   |
| Kingston  | SVP200S37A240G     | 240 GB | 2       | 1068  | 0     | 2.93   |
| Intel     | SSDSA2CT040G3      | 40 GB  | 15      | 1065  | 0     | 2.92   |
| SATADOM   | SL 3ME3 V2         | 128 GB | 2       | 1064  | 0     | 2.92   |
| Intel     | SSDSC2KG019T8R     | 1.9 TB | 4       | 1051  | 0     | 2.88   |
| Crucial   | M4-CT064M4SSD2     | 64 GB  | 50      | 1174  | 148   | 2.87   |
| Corsair   | Force GT           | 120 GB | 31      | 1207  | 35    | 2.86   |
| Micron    | M600_MTFDDAK512MBF | 512 GB | 6       | 1038  | 0     | 2.84   |
| OCZ       | AGILITY3           | 90 GB  | 7       | 1500  | 1     | 2.83   |
| SanDisk   | SD7SB7S512G1122    | 512 GB | 5       | 1032  | 0     | 2.83   |
| Corsair   | Neutron SSD        | 256 GB | 2       | 1031  | 0     | 2.83   |
| Intel     | SSDSC2BA800G4      | 800 GB | 5       | 1031  | 0     | 2.83   |
| Intel     | SSDSA2CW120G3      | 120 GB | 32      | 1202  | 32    | 2.82   |
| Samsung   | MZ7PC128HAFU-000L5 | 128 GB | 2       | 1028  | 0     | 2.82   |
| Samsung   | MZHPU512HCGL-000H1 | 512 GB | 2       | 1028  | 0     | 2.82   |
| Micron    | MTFDDAK960TDC-1... | 960 GB | 2       | 1022  | 0     | 2.80   |
| OCZ       | SOLID3             | 64 GB  | 10      | 1157  | 112   | 2.80   |
| Toshiba   | THNSNJ512GDNU      | 512 GB | 2       | 1021  | 0     | 2.80   |
| Samsung   | MZ7LM480HMHQ-00005 | 480 GB | 4       | 1018  | 0     | 2.79   |
| Samsung   | SSD 850 PRO        | 512 GB | 214     | 1100  | 21    | 2.79   |
| Samsung   | MZ7LN512HMJP-000H1 | 512 GB | 2       | 1012  | 0     | 2.77   |
| OCZ       | VERTEX2 3.5        | 240 GB | 2       | 1011  | 0     | 2.77   |
| SanDisk   | X300 2.5 7MM       | 128 GB | 3       | 1011  | 0     | 2.77   |
| Hajaan    | SSD 256G           | 256 GB | 2       | 1004  | 0     | 2.75   |
| Samsung   | MZ7LN128HCHP-00000 | 128 GB | 11      | 1001  | 0     | 2.74   |
| Apple     | SSD SM768E         | 752 GB | 5       | 1001  | 0     | 2.74   |
| ADATA     | SP800              | 32 GB  | 2       | 1001  | 0     | 2.74   |
| Kingston  | SH103S390G         | 90 GB  | 5       | 1368  | 1     | 2.73   |
| Corsair   | Force 3 SSD        | 120 GB | 56      | 1118  | 84    | 2.71   |
| Kingston  | SH100S3120G        | 120 GB | 10      | 987   | 0     | 2.70   |
| Samsung   | MZ7LM960HCHP-00005 | 960 GB | 2       | 985   | 0     | 2.70   |
| ADATA     | XM11               | 120 GB | 3       | 1005  | 2     | 2.69   |
| Toshiba   | TR150              | 960 GB | 6       | 980   | 0     | 2.69   |
| Crucial   | CT250MX200SSD4     | 250 GB | 6       | 994   | 168   | 2.68   |
| Micron    | MTFDDAK1T0MBF-1... | 1 TB   | 4       | 1588  | 1     | 2.68   |
| OCZ       | NOCTI              | 64 GB  | 2       | 974   | 0     | 2.67   |
| Samsung   | MZHPV512HDGL-00000 | 512 GB | 7       | 986   | 25    | 2.67   |
| WDC       | WD1001X06X-00SJVT0 | 1.1 TB | 3       | 974   | 0     | 2.67   |
| Intel     | SSDSC2BX200G4      | 200 GB | 2       | 969   | 0     | 2.66   |
| Samsung   | SSD 830 Series     | 256 GB | 91      | 991   | 34    | 2.65   |
| Toshiba   | THNSFC256GAMJ      | 256 GB | 3       | 968   | 0     | 2.65   |
| Samsung   | SSD 850 PRO        | 128 GB | 86      | 1008  | 12    | 2.65   |
| SanDisk   | SD6SF1M064G1022    | 64 GB  | 2       | 963   | 0     | 2.64   |
| Crucial   | M4-CT128M4SSD2     | 128 GB | 114     | 1056  | 101   | 2.64   |
| China     | L06B B0KB          | 960 GB | 2       | 960   | 0     | 2.63   |
| HP        | VK000240GWCFD      | 240 GB | 2       | 960   | 0     | 2.63   |
| Intel     | SSDMCEAW240A4      | 240 GB | 2       | 1130  | 765   | 2.63   |
| Samsung   | SSD 840 EVO        | 250 GB | 445     | 1038  | 14    | 2.62   |
| Crucial   | C300-CTFDDAC256MAG | 256 GB | 6       | 1548  | 571   | 2.62   |
| Samsung   | MZRPA128HMCD-000SO | 64 GB  | 16      | 976   | 1     | 2.61   |
| Apple     | SSD TS256C         | 256 GB | 22      | 1050  | 1     | 2.60   |
| Samsung   | SSD 840 PRO Series | 512 GB | 59      | 1179  | 73    | 2.60   |
| HP        | VK0300GDUQV        | 304 GB | 3       | 945   | 0     | 2.59   |
| SK hynix  | SC300 SATA         | 512 GB | 4       | 942   | 0     | 2.58   |
| ADATA     | SSD SP900          | 256 GB | 2       | 2284  | 508   | 2.58   |
| MyDigi... | BP5                | 240 GB | 6       | 939   | 0     | 2.58   |
| SK hynix  | SC311 SATA         | 1 TB   | 3       | 935   | 0     | 2.56   |
| OCZ       | VERTEX4            | 256 GB | 56      | 1261  | 2     | 2.56   |
| Samsung   | MZ7LN256HCHP-000H1 | 256 GB | 17      | 933   | 0     | 2.56   |
| Micron    | MTFDDAK256MBF-1... | 256 GB | 14      | 1048  | 1     | 2.56   |
| WDC       | WDS400T1R0A-68A4W0 | 4 TB   | 3       | 931   | 0     | 2.55   |
| Samsung   | SSD PM800 2.5"     | 256 GB | 5       | 931   | 0     | 2.55   |
| Samsung   | SSD 850 EVO M.2    | 1 TB   | 12      | 928   | 0     | 2.54   |
| SK hynix  | HFS120G32TND-N1A2A | 120 GB | 2       | 928   | 0     | 2.54   |
| Samsung   | MZ7PC128HAFU-000H1 | 128 GB | 13      | 927   | 0     | 2.54   |
| Samsung   | SSD 840 Series     | 250 GB | 111     | 992   | 1     | 2.54   |
| SanDisk   | SSD U110           | 32 GB  | 3       | 927   | 0     | 2.54   |
| Crucial   | C300-CTFDDAC128MAG | 128 GB | 13      | 1187  | 157   | 2.54   |
| Kingston  | SE50S3480G         | 480 GB | 10      | 1104  | 1     | 2.54   |
| Samsung   | MZ7LN256HAJQ-000H1 | 256 GB | 16      | 923   | 0     | 2.53   |
| Crucial   | M4-CT512M4SSD2     | 512 GB | 19      | 1527  | 596   | 2.53   |
| Samsung   | MZ7PC128HAFU-000L1 | 128 GB | 5       | 922   | 0     | 2.53   |
| Crucial   | M4-CT256M4SSD1     | 256 GB | 5       | 992   | 203   | 2.52   |
| Kingston  | SM2280S3G2120G     | 120 GB | 22      | 918   | 0     | 2.52   |
| Intel     | SSDSC2CW480A3      | 480 GB | 10      | 915   | 0     | 2.51   |
| Samsung   | SSD 850 EVO        | 1 TB   | 325     | 1089  | 6     | 2.50   |
| Kingston  | SH103S3120G        | 120 GB | 144     | 993   | 14    | 2.50   |
| SanDisk   | SDSSDRC032G        | 32 GB  | 12      | 909   | 0     | 2.49   |
| Apacer    | AS330              | 240 GB | 3       | 908   | 0     | 2.49   |
| Samsung   | SSD 840 PRO Series | 256 GB | 205     | 1103  | 10    | 2.48   |
| Intel     | SSDSC2KG480G8      | 480 GB | 17      | 1105  | 1     | 2.48   |
| Intel     | SSDSA2BW600G3      | 600 GB | 3       | 905   | 0     | 2.48   |
| Corsair   | Force GT           | 240 GB | 7       | 1348  | 237   | 2.48   |
| SK hynix  | SC300B SATA        | 512 GB | 6       | 901   | 0     | 2.47   |
| Intel     | SSDSA2BW160G3      | 160 GB | 6       | 1102  | 201   | 2.47   |
| Samsung   | SSD 850 PRO        | 256 GB | 355     | 939   | 6     | 2.46   |
| Corsair   | Force 3 SSD        | 64 GB  | 23      | 922   | 1     | 2.46   |
| Samsung   | MZ7TE512HMHP-000L1 | 512 GB | 9       | 896   | 0     | 2.46   |
| SanDisk   | SDSSDXP120G        | 120 GB | 4       | 895   | 0     | 2.45   |
| Micron    | 5300_MTFDDAK1T9TDT | 1.9 TB | 20      | 1045  | 1     | 2.45   |
| Intel     | SSDSC2BP240G4      | 240 GB | 13      | 1002  | 1     | 2.45   |
| ADATA     | SP600              | 256 GB | 16      | 892   | 0     | 2.45   |
| Fury      | HyperX 3D          | 240 GB | 8       | 887   | 0     | 2.43   |
| SanDisk   | SD7SB3Q064G        | 56 GB  | 2       | 885   | 0     | 2.43   |
| Samsung   | SSD 840 Series     | 500 GB | 32      | 1049  | 15    | 2.42   |
| Samsung   | SSD 840 PRO Series | 128 GB | 133     | 1019  | 14    | 2.42   |
| Samsung   | MZ7LH960HAJR-00005 | 960 GB | 24      | 881   | 0     | 2.42   |
| Samsung   | SSD 830 Series     | 64 GB  | 37      | 985   | 28    | 2.41   |
| Intel     | SSDSC2BB800G7R     | 800 GB | 2       | 1166  | 1     | 2.40   |
| Intel     | SSDSC2BA200G4      | 200 GB | 11      | 926   | 1     | 2.40   |
| Teclast   | 256GB A750         | 256 GB | 2       | 870   | 0     | 2.38   |
| Mushkin   | MKNSSDSR1TB        | 1 TB   | 4       | 870   | 0     | 2.38   |
| Samsung   | MZ7LN128HCHP-000H1 | 128 GB | 21      | 870   | 0     | 2.38   |
| ADATA     | SX930              | 480 GB | 2       | 869   | 0     | 2.38   |
| Samsung   | SSD 840 EVO        | 120 GB | 338     | 939   | 15    | 2.38   |
| Samsung   | SSD 840 EVO 250... | 250 GB | 17      | 879   | 9     | 2.38   |
| Crucial   | C300-CTFDDAC064MAG | 64 GB  | 13      | 1007  | 156   | 2.38   |
| Transcend | TS128GSSD340K      | 128 GB | 4       | 868   | 0     | 2.38   |
| Samsung   | MZ7LN256HMJP-000H7 | 256 GB | 2       | 867   | 0     | 2.38   |
| PNY       | CS1311 240GB SSD   | 240 GB | 39      | 898   | 1     | 2.37   |
| Samsung   | SSD SM871 2.5 7mm  | 256 GB | 16      | 908   | 29    | 2.37   |
| Micron    | MTFDDAK512MBF-1... | 512 GB | 12      | 896   | 2     | 2.37   |
| Intel     | SSDSC2MH250A2      | 250 GB | 2       | 864   | 0     | 2.37   |
| Phison    | SATA SSD           | 16 GB  | 2       | 862   | 0     | 2.36   |
| Corsair   | Force GS           | 128 GB | 31      | 883   | 2     | 2.36   |
| Micron    | M600_MTFDDAK256MBF | 256 GB | 7       | 861   | 0     | 2.36   |
| Micron    | MTFDDAK480TDN      | 480 GB | 3       | 858   | 0     | 2.35   |
| Goodram   | SSD                | 480 GB | 6       | 857   | 0     | 2.35   |
| Toshiba   | KHK61RSE480G       | 480 GB | 4       | 856   | 0     | 2.35   |
| Samsung   | MZ7TY256HDHP-000L1 | 256 GB | 6       | 1173  | 4     | 2.34   |
| SanDisk   | SDSA6MM-016G-1006  | 16 GB  | 17      | 919   | 92    | 2.33   |
| ADATA     | SSD S599           | 55 GB  | 2       | 849   | 0     | 2.33   |
| WDC       | PC SA530 SDASN8... | 256 GB | 2       | 849   | 0     | 2.33   |
| Samsung   | SSD 850 EVO        | 500 GB | 1265    | 855   | 1     | 2.32   |
| SK        | SKhynix SC300 H... | 512 GB | 2       | 843   | 0     | 2.31   |
| Toshiba   | THNSNJ256GCSY      | 256 GB | 5       | 843   | 0     | 2.31   |
| Samsung   | MZ7LN512HMJP-00000 | 512 GB | 7       | 841   | 0     | 2.31   |
| SanDisk   | SD7SB6S-128G-1006  | 128 GB | 8       | 914   | 1     | 2.30   |
| Samsung   | SSD 840 Series     | 120 GB | 148     | 924   | 8     | 2.30   |
| OCZ       | VERTEX             | 32 GB  | 6       | 953   | 1     | 2.29   |
| Seagate   | XA1920ME10063      | 1.9 TB | 3       | 835   | 0     | 2.29   |
| SanDisk   | SD7SB6S128G1122    | 128 GB | 11      | 835   | 0     | 2.29   |
| Kingston  | SMSR150S3256G      | 128 GB | 2       | 833   | 0     | 2.28   |
| Kingston  | RBU-SNS8152S3256GF | 256 GB | 2       | 832   | 0     | 2.28   |
| Kingston  | SH100S3240G        | 240 GB | 7       | 1234  | 2     | 2.28   |
| Intel     | SSDMCEAC120B3A     | 120 GB | 5       | 845   | 1     | 2.27   |
| Samsung   | MZ7LH480HBHQ0D3    | 480 GB | 2       | 823   | 0     | 2.25   |
| WDC       | WDBNCE0010PNC-WRSN | 1 TB   | 2       | 821   | 0     | 2.25   |
| OCZ       | AGILITY3           | 128 GB | 5       | 1521  | 1     | 2.25   |
| SanDisk   | SSD U110           | 128 GB | 5       | 820   | 0     | 2.25   |
| Intel     | SSDSC2KB019T7      | 1.9 TB | 2       | 1492  | 2     | 2.24   |
| Kingston  | SVP200S360G        | 64 GB  | 17      | 859   | 1     | 2.24   |
| DeTech    | Development Tec... | 120 GB | 3       | 916   | 1     | 2.24   |
| Samsung   | MZHPV512HDGL-000L1 | 512 GB | 3       | 816   | 0     | 2.24   |
| Toshiba   | THNSFC064GBSJ      | 64 GB  | 2       | 814   | 0     | 2.23   |
| Micron    | 5100_MTFDDAK960TCB | 960 GB | 4       | 1023  | 15    | 2.23   |
| Samsung   | MZ7PD256HAFV-000H7 | 256 GB | 16      | 809   | 0     | 2.22   |
| Crucial   | CT512MX100SSD1     | 512 GB | 83      | 882   | 1     | 2.21   |
| Transcend | TS32GSSD340K       | 32 GB  | 3       | 806   | 0     | 2.21   |
| Samsung   | MZ7LH1T9HMLT-00005 | 1.9 TB | 4       | 805   | 0     | 2.21   |
| Maxsun    | 120GB X5           | 120 GB | 2       | 804   | 0     | 2.20   |
| Samsung   | MZ7TE256HMHP-00000 | 256 GB | 4       | 803   | 0     | 2.20   |
| China     | OSSD512GBTSS2      | 512 GB | 2       | 802   | 0     | 2.20   |
| Toshiba   | THNSFC128GBSJ      | 128 GB | 5       | 801   | 0     | 2.20   |
| SanDisk   | SD8SN8U128G1122    | 128 GB | 3       | 801   | 0     | 2.20   |
| SanDisk   | SD7TB3Q-128G-1006  | 128 GB | 7       | 813   | 5     | 2.19   |
| Toshiba   | THNSNH512GCST      | 512 GB | 3       | 800   | 0     | 2.19   |
| Corsair   | Force GS           | 240 GB | 10      | 1342  | 16    | 2.19   |
| Toshiba   | THNS064GG2BNAA     | 64 GB  | 9       | 799   | 0     | 2.19   |
| OCZ       | VECTOR180          | 480 GB | 2       | 798   | 0     | 2.19   |
| Samsung   | SSD PM800 Serie... | 256 GB | 4       | 988   | 2     | 2.19   |
| SanDisk   | SD8SB8U-128G-1006  | 128 GB | 8       | 797   | 0     | 2.18   |
| Seagate   | SSD                | 500 GB | 4       | 796   | 0     | 2.18   |
| Kingston  | SEDC500M1920G      | 1.9 TB | 4       | 1049  | 1     | 2.18   |
| Intel     | SSDSC2KB019T8      | 1.9 TB | 30      | 923   | 1     | 2.18   |
| Samsung   | SSD 883 DCT 3.84TB | 3.8 TB | 2       | 794   | 0     | 2.18   |
| Samsung   | SSD PM830 2.5" 7mm | 256 GB | 32      | 963   | 127   | 2.18   |
| Samsung   | SSD PM830 2.5" 7mm | 512 GB | 5       | 917   | 202   | 2.18   |
| Samsung   | MZ7TD512HAGM-000L1 | 512 GB | 5       | 794   | 0     | 2.18   |
| Hoodisk   | SSD                | 32 GB  | 5       | 791   | 0     | 2.17   |
| Toshiba   | Q300 Pro           | 256 GB | 2       | 789   | 0     | 2.16   |
| Samsung   | SSD 850 EVO M.2    | 500 GB | 70      | 789   | 0     | 2.16   |
| Mushkin   | MKNSSDSR500GB      | 500 GB | 8       | 785   | 0     | 2.15   |
| SanDisk   | SD8SB8U-256G-1006  | 256 GB | 22      | 866   | 1     | 2.15   |
| WDC       | WDS200T2B0B        | 2 TB   | 10      | 848   | 1     | 2.15   |
| SanDisk   | Ultra II           | 480 GB | 76      | 801   | 1     | 2.15   |
| SanDisk   | SD7SN6S512G1122    | 512 GB | 2       | 779   | 0     | 2.14   |
| Samsung   | MZ7KM240HMHQ-00005 | 240 GB | 6       | 778   | 0     | 2.13   |
| Samsung   | SSD 850 EVO M.2    | 250 GB | 75      | 778   | 0     | 2.13   |
| Kingston  | RBU-SNS8152S325... | 256 GB | 5       | 777   | 0     | 2.13   |
| Micron    | MTFDDAV240TDU      | 240 GB | 6       | 777   | 0     | 2.13   |
| Intel     | SSDSC2BB480G7R     | 480 GB | 3       | 1110  | 1     | 2.13   |
| Toshiba   | THNSNJ256G8NU      | 256 GB | 8       | 776   | 0     | 2.13   |
| WDC       | WDBNCE2500PNC-WRSN | 250 GB | 4       | 775   | 0     | 2.12   |
| Crucial   | CT500MX200SSD3     | 500 GB | 9       | 1125  | 18    | 2.12   |
| SK hynix  | HFS250G32TND-N1A0A | 250 GB | 2       | 772   | 0     | 2.12   |
| Intel     | SSDSA2CW160G3      | 160 GB | 17      | 812   | 1     | 2.11   |
| SanDisk   | X400 2.5 7MM       | 256 GB | 16      | 771   | 0     | 2.11   |
| SanDisk   | SSD U110           | 64 GB  | 6       | 771   | 0     | 2.11   |
| SanDisk   | SD8SB8U1T001122    | 1 TB   | 16      | 769   | 0     | 2.11   |
| SanDisk   | SD9SB8W256G1014    | 256 GB | 3       | 768   | 0     | 2.11   |
| Kingston  | SVP200S390G        | 90 GB  | 2       | 767   | 0     | 2.10   |
| OCZ       | VERTEX2 3.5        | 115 GB | 3       | 765   | 0     | 2.10   |
| Samsung   | MZ7LN128HAHQ-000H1 | 128 GB | 8       | 763   | 0     | 2.09   |
| Samsung   | MZHPV256HDGL-00000 | 256 GB | 18      | 788   | 1     | 2.09   |
| SanDisk   | SDSSDH120GG25      | 120 GB | 4       | 889   | 14    | 2.09   |
| AEGO      | SSD                | 480 GB | 4       | 760   | 0     | 2.08   |
| SanDisk   | SD8SBBU480G1122    | 480 GB | 6       | 759   | 0     | 2.08   |
| SK hynix  | SC300 2.5 7MM      | 128 GB | 2       | 759   | 0     | 2.08   |
| Kingston  | RBU-SNS6100S3128GD | 128 GB | 2       | 759   | 0     | 2.08   |
| Samsung   | MZ7TD256HAFV-000L9 | 256 GB | 19      | 759   | 0     | 2.08   |
| Toshiba   | Q200 EX            | 240 GB | 2       | 758   | 0     | 2.08   |
| SanDisk   | SDSSDHP256G        | 256 GB | 56      | 793   | 1     | 2.08   |
| Apple     | SSD SM1024G        | 1 TB   | 19      | 757   | 0     | 2.08   |
| SSSTC     | ER2-CD960A         | 960 GB | 2       | 757   | 0     | 2.07   |
| Maxsun    | 120GB A6           | 120 GB | 2       | 756   | 0     | 2.07   |
| Plextor   | PX-512M8VC +       | 512 GB | 2       | 756   | 0     | 2.07   |
| Samsung   | MZNLF128HCHP-00004 | 128 GB | 18      | 755   | 0     | 2.07   |
| OCZ       | VERTEX3 MI         | 120 GB | 30      | 974   | 102   | 2.07   |
| Kingston  | SUV500M8960G       | 960 GB | 2       | 802   | 722   | 2.07   |
| Mushkin   | MKNSSDTR1TB-3D     | 1 TB   | 3       | 1404  | 26    | 2.06   |
| Corsair   | CSSD-V128GB2       | 128 GB | 2       | 752   | 0     | 2.06   |
| OCZ       | AGILITY3           | 64 GB  | 88      | 990   | 16    | 2.06   |
| Samsung   | SSD 850 EVO        | 4 TB   | 7       | 749   | 0     | 2.05   |
| Samsung   | MZ7TY256HDHP-00007 | 256 GB | 3       | 749   | 0     | 2.05   |
| Crucial   | M4-CT256M4SSD2     | 256 GB | 66      | 947   | 156   | 2.05   |
| Samsung   | MZHPU256HCGL-000H1 | 256 GB | 3       | 746   | 0     | 2.05   |
| WDC       | WDS200T2B0A        | 2 TB   | 7       | 745   | 0     | 2.04   |
| SanDisk   | PLUS               | 480 GB | 15      | 745   | 0     | 2.04   |
| Kingston  | SVP200S37A120G     | 120 GB | 27      | 869   | 65    | 2.04   |
| Intel     | SSDSC2BB120G7R     | 120 GB | 7       | 743   | 0     | 2.04   |
| Toshiba   | KHK61RSE960G       | 960 GB | 2       | 743   | 0     | 2.04   |
| Transcend | TS16GMTS400        | 16 GB  | 2       | 742   | 0     | 2.04   |
| Samsung   | SSD 750 EVO        | 500 GB | 62      | 781   | 4     | 2.03   |
| Apple     | SSD SM128E         | 121 GB | 14      | 888   | 2     | 2.03   |
| Samsung   | SSD PM830 2.5" 7mm | 128 GB | 45      | 895   | 139   | 2.02   |
| Corsair   | Force GT           | 90 GB  | 6       | 813   | 1     | 2.02   |
| SanDisk   | SD8SB8U512G1122    | 512 GB | 13      | 735   | 0     | 2.02   |
| OCZ       | VERTEX3            | 120 GB | 109     | 999   | 44    | 2.01   |
| Kingston  | RBU-SNS8151S396GG  | 96 GB  | 4       | 803   | 2     | 2.01   |
| OWC       | Mercury EXTREME... | 480 GB | 9       | 886   | 9     | 2.00   |
| Intel     | SSDSC2MH120A2      | 120 GB | 8       | 729   | 0     | 2.00   |
| Intel     | SSDSC2CT060A3      | 64 GB  | 16      | 872   | 1     | 1.99   |
| SanDisk   | Ultra II           | 960 GB | 58      | 785   | 18    | 1.98   |
| Samsung   | MZ7PA256HMDR-010H1 | 256 GB | 2       | 842   | 520   | 1.98   |
| OCZ       | VERTEX3            | 64 GB  | 44      | 762   | 1     | 1.98   |
| Samsung   | SSD 850 EVO        | 250 GB | 1549    | 738   | 2     | 1.98   |
| Intel     | SSDSC2KB960G8      | 960 GB | 54      | 782   | 1     | 1.97   |
| SanDisk   | SD7SB6S-256G-1006  | 256 GB | 18      | 719   | 0     | 1.97   |
| Samsung   | MZMPC256HBGJ-000H1 | 256 GB | 4       | 719   | 0     | 1.97   |
| Crucial   | M4-CT064M4SSD3     | 64 GB  | 2       | 963   | 548   | 1.97   |
| Samsung   | MZ7PA128HMCD-010L1 | 128 GB | 12      | 799   | 247   | 1.97   |
| SanDisk   | SDSSDA960G         | 960 GB | 12      | 718   | 0     | 1.97   |
| OCZ       | TRION150           | 480 GB | 13      | 718   | 0     | 1.97   |
| Crucial   | CT3500SC           | 500 GB | 4       | 928   | 6     | 1.97   |
| Samsung   | SSD PM800 2.5"     | 128 GB | 6       | 717   | 0     | 1.97   |
| Toshiba   | THNSNH128GBST      | 128 GB | 9       | 885   | 72    | 1.97   |
| OCZ       | TRION100           | 960 GB | 3       | 716   | 0     | 1.96   |
| PNY       | CS900 M.2 1TB SSD  | 1 TB   | 2       | 715   | 0     | 1.96   |
| Kingston  | SEDC400S37960G     | 960 GB | 2       | 714   | 0     | 1.96   |
| Micron    | M500DC_MTFDDAK8... | 800 GB | 2       | 710   | 0     | 1.95   |
| Crucial   | CT1024MX200SSD1    | 1 TB   | 22      | 909   | 9     | 1.95   |
| KUIJIA    | DK500-64G          | 64 GB  | 5       | 709   | 0     | 1.94   |
| SanDisk   | SDSSDHII480G       | 480 GB | 31      | 717   | 1     | 1.94   |
| Corsair   | Force LE SSD       | 480 GB | 11      | 765   | 1     | 1.94   |
| SanDisk   | SDSSDH31024G       | 1 TB   | 31      | 707   | 0     | 1.94   |
| Samsung   | SSD 840 EVO 120... | 120 GB | 12      | 711   | 1     | 1.93   |
| Seagate   | ST120HM000-1G5142  | 120 GB | 3       | 705   | 0     | 1.93   |
| Plextor   | PX-128M2S          | 128 GB | 3       | 833   | 1     | 1.93   |
| Samsung   | MZ7LH256HAJD-000L7 | 256 GB | 2       | 704   | 0     | 1.93   |
| Samsung   | SSD PM830 mSATA    | 256 GB | 7       | 703   | 0     | 1.93   |
| OCZ       | VECTOR             | 128 GB | 9       | 704   | 2     | 1.93   |
| Samsung   | MZNLF192HCGS-000L1 | 192 GB | 5       | 702   | 0     | 1.93   |
| Apple     | SSD SM0512F        | 500 GB | 87      | 716   | 1     | 1.92   |
| Toshiba   | VT180              | 480 GB | 3       | 1072  | 1     | 1.92   |
| SanDisk   | SDSSDP064G         | 64 GB  | 70      | 715   | 15    | 1.92   |
| Samsung   | MZ7LN256HAJQ-00000 | 256 GB | 8       | 700   | 0     | 1.92   |
| SanDisk   | SDSSDA480G         | 480 GB | 51      | 711   | 1     | 1.92   |
| SanDisk   | SDSSDHII960G       | 960 GB | 23      | 749   | 1     | 1.92   |
| Samsung   | MZ7LN128HCHP-000L1 | 128 GB | 23      | 699   | 0     | 1.92   |
| Samsung   | SSD 850 EVO        | 120 GB | 237     | 698   | 0     | 1.91   |
| Kingston  | SVP200S3120G       | 120 GB | 18      | 763   | 169   | 1.91   |
| SanDisk   | SD8SN8U256G1122    | 256 GB | 5       | 696   | 0     | 1.91   |
| Team      | T253TD480G         | 480 GB | 5       | 694   | 0     | 1.90   |
| SK hynix  | HFS128G39MNC-3310A | 128 GB | 2       | 693   | 0     | 1.90   |
| Kingston  | SHSS37A120G        | 120 GB | 18      | 693   | 0     | 1.90   |
| Intel     | SSDSC2KG240G8      | 240 GB | 20      | 693   | 0     | 1.90   |
| Kingston  | SMSM151S3128GD     | 128 GB | 2       | 692   | 0     | 1.90   |
| Goodram   | SSDPR_CX300_120    | 120 GB | 5       | 692   | 0     | 1.90   |
| Intel     | SSDSC2BW240A3L     | 240 GB | 15      | 691   | 0     | 1.89   |
| WDC       | WDS100T1B0A-00H9H0 | 1 TB   | 25      | 735   | 41    | 1.89   |
| ADATA     | SX950              | 240 GB | 3       | 689   | 0     | 1.89   |
| Micron    | 1100_MTFDDAK2T0TBN | 2 TB   | 12      | 1178  | 3     | 1.89   |
| OCZ       | VECTOR             | 256 GB | 7       | 704   | 1     | 1.89   |
| Samsung   | MMCRE28G5MXP-0VBH1 | 128 GB | 3       | 688   | 0     | 1.89   |
| Samsung   | MZHPV128HDGM-00000 | 128 GB | 5       | 683   | 0     | 1.87   |
| Intel     | SSDSC2KG480G7      | 480 GB | 6       | 741   | 3     | 1.87   |
| Crucial   | M4-CT128M4SSD1     | 128 GB | 14      | 797   | 145   | 1.87   |
| Samsung   | MZMPC032HBCD-000D1 | 32 GB  | 10      | 681   | 0     | 1.87   |
| Crucial   | CT500MX200SSD4     | 500 GB | 13      | 757   | 1     | 1.86   |
| PNY       | CS1311 480GB SSD   | 480 GB | 18      | 680   | 0     | 1.86   |
| Intel     | SSDSA2BW120G3H     | 120 GB | 7       | 702   | 1     | 1.86   |
| OCZ       | VERTEX4            | 64 GB  | 14      | 711   | 1     | 1.86   |
| Samsung   | MZ7PD128HAFV-000H7 | 128 GB | 13      | 719   | 4     | 1.86   |
| Samsung   | SSD SM871 2.5 7mm  | 512 GB | 4       | 1091  | 78    | 1.86   |
| Micron    | C400-MTFDDAK128MAM | 128 GB | 9       | 678   | 0     | 1.86   |
| China     | SSD                | 720 GB | 4       | 745   | 1     | 1.86   |
| Corsair   | Force LE SSD       | 240 GB | 10      | 677   | 0     | 1.86   |
| Samsung   | MZNLN256HCHP-00000 | 256 GB | 22      | 677   | 0     | 1.86   |
| Ramaxel   | RTFMB016JGV2BWX    | 16 GB  | 2       | 677   | 0     | 1.86   |
| Apple     | SSD SM0256F        | 256 GB | 79      | 681   | 1     | 1.85   |
| Apple     | SSD SM0128F        | 121 GB | 5       | 675   | 0     | 1.85   |
| Toshiba   | THNSNJ128GCST      | 128 GB | 6       | 674   | 0     | 1.85   |
| SK        | SKhynix SC300 H... | 256 GB | 2       | 672   | 0     | 1.84   |
| SK hynix  | SC300 M.2 2280     | 128 GB | 8       | 672   | 0     | 1.84   |
| Samsung   | MZ7TE128HMGR-000L1 | 128 GB | 47      | 671   | 0     | 1.84   |
| PNY       | CS1311 120GB SSD   | 120 GB | 18      | 681   | 1     | 1.84   |
| Apacer    | AST220             | 240 GB | 3       | 669   | 0     | 1.83   |
| Transcend | TS128GSSD320       | 128 GB | 5       | 669   | 0     | 1.83   |
| OCZ       | REVODRIVE3         | 240 GB | 2       | 1000  | 1     | 1.83   |
| Samsung   | SSD PM871b 2.5 7mm | 128 GB | 5       | 667   | 0     | 1.83   |
| Samsung   | MZ7TE128HMGR-00004 | 128 GB | 11      | 666   | 0     | 1.83   |
| Kingston  | SH103S3240G        | 240 GB | 56      | 908   | 126   | 1.83   |
| Toshiba   | THNSNF128GCSS      | 128 GB | 28      | 704   | 1     | 1.83   |
| Micron    | 5200_MTFDDAK1T9TDD | 1.9 TB | 2       | 666   | 0     | 1.83   |
| SanDisk   | SD6SA1M064G1011    | 64 GB  | 4       | 666   | 0     | 1.82   |
| Samsung   | SSD 850 EVO mSATA  | 500 GB | 37      | 665   | 0     | 1.82   |
| Samsung   | SSD PB22-JS3 2.5"  | 128 GB | 3       | 665   | 0     | 1.82   |
| Samsung   | MZ7PD128HCFV-000H1 | 128 GB | 14      | 665   | 0     | 1.82   |
| SK hynix  | SC300 SATA         | 256 GB | 4       | 665   | 0     | 1.82   |
| OCZ       | AGILITY3           | 120 GB | 103     | 821   | 57    | 1.82   |
| Innodisk  | Corp. DRPS-02GJ... | 2 GB   | 3       | 664   | 0     | 1.82   |
| Apacer    | AS450              | 120 GB | 2       | 662   | 0     | 1.82   |
| Samsung   | MZNLN512HCJH-000H1 | 512 GB | 8       | 659   | 0     | 1.81   |

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
| FASTDISK    | 1      | 2       | 1365  | 0     | 3.74   |
| SATADOM     | 1      | 2       | 1064  | 0     | 2.92   |
| Hajaan      | 1      | 2       | 1004  | 0     | 2.75   |
| Fury        | 2      | 10      | 784   | 0     | 2.15   |
| Maxsun      | 2      | 4       | 780   | 0     | 2.14   |
| SK          | 2      | 4       | 758   | 0     | 2.08   |
| HPE         | 6      | 19      | 772   | 1     | 1.95   |
| KUIJIA      | 1      | 5       | 709   | 0     | 1.94   |
| Corsair     | 46     | 442     | 913   | 89    | 1.93   |
| OCZ         | 79     | 1100    | 837   | 25    | 1.84   |
| Intel       | 221    | 2513    | 739   | 57    | 1.61   |
| MyDigita... | 3      | 16      | 571   | 0     | 1.56   |
| Radeon      | 1      | 6       | 564   | 0     | 1.55   |
| SuperMicro  | 3      | 12      | 633   | 1     | 1.53   |
| Samsung     | 388    | 19250   | 586   | 13    | 1.53   |
| Turbox      | 1      | 2       | 556   | 0     | 1.53   |
| VENO SCORP  | 1      | 2       | 545   | 0     | 1.49   |
| SMI         | 1      | 2       | 534   | 0     | 1.47   |
| minisforum  | 2      | 8       | 505   | 0     | 1.38   |
| Apple       | 26     | 980     | 488   | 13    | 1.28   |
| Toshiba     | 95     | 1053    | 491   | 14    | 1.27   |
| DeTech      | 2      | 7       | 504   | 1     | 1.27   |
| T-CREATE    | 1      | 2       | 442   | 0     | 1.21   |
| OWC         | 6      | 53      | 473   | 2     | 1.19   |
| Axiom       | 1      | 2       | 591   | 524   | 1.19   |
| AEGO        | 2      | 8       | 420   | 0     | 1.15   |
| Mushkin     | 31     | 137     | 480   | 50    | 1.08   |
| FCS         | 1      | 2       | 379   | 0     | 1.04   |
| Hoodisk     | 5      | 44      | 371   | 0     | 1.02   |
| Seagate     | 35     | 230     | 433   | 54    | 0.97   |
| HAJAAN      | 1      | 3       | 351   | 0     | 0.96   |
| GALAX       | 3      | 15      | 343   | 0     | 0.94   |
| Kston       | 1      | 8       | 333   | 0     | 0.91   |
| Mach Xtreme | 1      | 2       | 332   | 0     | 0.91   |
| Hyundai     | 5      | 15      | 328   | 0     | 0.90   |
| Kingston    | 203    | 10843   | 372   | 20    | 0.90   |
| SanDisk     | 285    | 6462    | 359   | 24    | 0.89   |
| Silicon     | 7      | 24      | 337   | 1     | 0.89   |
| Micron      | 121    | 1415    | 403   | 100   | 0.88   |
| HP          | 27     | 298     | 349   | 13    | 0.87   |
| Biwintech   | 1      | 2       | 310   | 0     | 0.85   |
| Gigabyte    | 8      | 268     | 306   | 0     | 0.84   |
| WDC         | 69     | 4511    | 318   | 6     | 0.82   |
| Palit       | 5      | 14      | 301   | 1     | 0.80   |
| Faspeed     | 4      | 8       | 313   | 1     | 0.79   |
| SK hynix    | 80     | 1270    | 410   | 112   | 0.79   |
| Smartbuy    | 14     | 266     | 313   | 4     | 0.79   |
| Crucial     | 81     | 8300    | 325   | 22    | 0.77   |
| JASTER      | 1      | 3       | 278   | 0     | 0.76   |
| RZX         | 1      | 3       | 653   | 1     | 0.76   |
| VisionTek   | 2      | 4       | 271   | 0     | 0.74   |
| PNY         | 49     | 1195    | 273   | 3     | 0.74   |
| VICK        | 1      | 2       | 268   | 0     | 0.74   |
| addlink     | 4      | 21      | 266   | 1     | 0.73   |
| AFOX        | 1      | 4       | 382   | 76    | 0.73   |
| SandForce   | 1      | 2       | 422   | 208   | 0.72   |
| BIOSTAR     | 4      | 19      | 263   | 0     | 0.72   |
| DERLER      | 1      | 2       | 261   | 0     | 0.72   |
| Pioneer     | 7      | 35      | 273   | 1     | 0.71   |
| ADROITLARK  | 1      | 2       | 256   | 0     | 0.70   |
| XPG         | 1      | 4       | 249   | 0     | 0.68   |
| Maxtor      | 3      | 30      | 248   | 0     | 0.68   |
| Goodram     | 38     | 871     | 250   | 1     | 0.68   |
| tigo        | 3      | 8       | 244   | 0     | 0.67   |
| Ramaxel     | 7      | 20      | 273   | 103   | 0.66   |
| UNIC2       | 2      | 8       | 239   | 0     | 0.66   |
| ASMedia     | 2      | 10      | 237   | 0     | 0.65   |
| DIERYA      | 1      | 2       | 237   | 0     | 0.65   |
| Patriot     | 41     | 969     | 241   | 9     | 0.63   |
| Aoluska     | 1      | 2       | 225   | 0     | 0.62   |
| GAMER       | 2      | 5       | 224   | 0     | 0.62   |
| Plextor     | 59     | 490     | 235   | 32    | 0.60   |
| SPCC        | 30     | 1607    | 251   | 44    | 0.60   |
| VISIPRO     | 3      | 11      | 216   | 2     | 0.59   |
| ADATA       | 108    | 2697    | 261   | 59    | 0.58   |
| ZHITAI      | 3      | 22      | 211   | 0     | 0.58   |
| Transcend   | 80     | 903     | 230   | 13    | 0.58   |
| e2e4        | 3      | 10      | 207   | 0     | 0.57   |
| JAMESDONKEY | 2      | 5       | 248   | 2     | 0.57   |
| Phison      | 24     | 168     | 206   | 1     | 0.56   |
| KINGBANK    | 2      | 13      | 204   | 0     | 0.56   |
| Team        | 53     | 589     | 209   | 2     | 0.55   |
| KIOXIA-E... | 3      | 156     | 198   | 0     | 0.54   |
| KingFast    | 8      | 200     | 218   | 17    | 0.54   |
| Innodisk    | 17     | 55      | 237   | 149   | 0.53   |
| Union Me... | 2      | 22      | 214   | 46    | 0.52   |
| UMAX        | 1      | 4       | 188   | 0     | 0.52   |
| ZOTAC       | 2      | 4       | 184   | 0     | 0.51   |
| HYDRA       | 1      | 3       | 229   | 1     | 0.50   |
| LDLC        | 12     | 87      | 235   | 39    | 0.50   |
| CFD         | 2      | 4       | 181   | 0     | 0.50   |
| Ramsta      | 6      | 18      | 271   | 90    | 0.50   |
| Leven       | 9      | 88      | 187   | 2     | 0.49   |
| KingDian    | 17     | 185     | 192   | 55    | 0.49   |
| Drevo       | 5      | 41      | 317   | 190   | 0.48   |
| GSemi       | 2      | 6       | 183   | 4     | 0.48   |
| TCSUNBOW    | 7      | 35      | 173   | 0     | 0.48   |
| JD          | 1      | 2       | 168   | 0     | 0.46   |
| Apacer      | 29     | 784     | 187   | 13    | 0.46   |
| RX7         | 3      | 6       | 164   | 0     | 0.45   |
| aigo        | 1      | 2       | 163   | 0     | 0.45   |
| China       | 154    | 2696    | 177   | 21    | 0.45   |
| T-FORCE     | 11     | 188     | 163   | 1     | 0.44   |
| TEXTORM     | 4      | 16      | 157   | 3     | 0.43   |
| Kingmax     | 5      | 92      | 279   | 241   | 0.43   |
| ORIGIN I... | 1      | 2       | 155   | 0     | 0.43   |
| Qumo        | 2      | 7       | 238   | 146   | 0.43   |
| ADTEC       | 1      | 2       | 152   | 0     | 0.42   |
| Londisk     | 3      | 24      | 152   | 0     | 0.42   |
| Lenovo      | 7      | 20      | 167   | 1     | 0.41   |
| Win Memory  | 3      | 9       | 150   | 0     | 0.41   |
| Lexar       | 23     | 417     | 152   | 4     | 0.41   |
| Inland      | 4      | 21      | 145   | 0     | 0.40   |
| SuperSSpeed | 1      | 6       | 235   | 177   | 0.40   |
| LuminouTek  | 3      | 9       | 141   | 0     | 0.39   |
| MSI         | 4      | 32      | 136   | 0     | 0.37   |
| Vaseky      | 10     | 32      | 140   | 4     | 0.37   |
| Timetec     | 11     | 33      | 137   | 2     | 0.37   |
| WHALEKOM    | 1      | 2       | 162   | 5     | 0.37   |
| DST         | 2      | 4       | 135   | 0     | 0.37   |
| Fujitsu     | 2      | 4       | 407   | 6     | 0.36   |
| Advantech   | 3      | 9       | 132   | 0     | 0.36   |
| MidasForce  | 5      | 26      | 130   | 0     | 0.36   |
| Gigabyte... | 6      | 88      | 130   | 0     | 0.36   |
| Intenso     | 43     | 985     | 135   | 29    | 0.34   |
| Dogfish     | 9      | 112     | 141   | 10    | 0.34   |
| J.ZAO       | 1      | 2       | 123   | 0     | 0.34   |
| Kingchuxing | 8      | 58      | 129   | 28    | 0.34   |
| Hypertec    | 1      | 2       | 371   | 512   | 0.33   |
| BIWIN       | 10     | 61      | 128   | 68    | 0.33   |
| HGST        | 2      | 10      | 202   | 203   | 0.33   |
| TAMMUZ      | 6      | 15      | 118   | 0     | 0.33   |
| Super Ta... | 7      | 21      | 235   | 49    | 0.33   |
| Verbatim    | 8      | 237     | 123   | 6     | 0.33   |
| AirDisk     | 2      | 25      | 118   | 0     | 0.33   |
| GOFATOO     | 2      | 6       | 118   | 0     | 0.33   |
| Hikvision   | 24     | 240     | 121   | 9     | 0.32   |
| SUNEAST     | 5      | 12      | 156   | 15    | 0.32   |
| ZTC         | 2      | 6       | 116   | 0     | 0.32   |
| GeIL        | 3      | 9       | 116   | 0     | 0.32   |
| Reeinno     | 3      | 6       | 141   | 1     | 0.32   |
| EMTEC       | 9      | 142     | 117   | 43    | 0.32   |
| Colorful    | 10     | 64      | 123   | 20    | 0.32   |
| Zheino      | 16     | 44      | 130   | 4     | 0.31   |
| HEORIADY    | 3      | 7       | 114   | 0     | 0.31   |
| LVCARDS     | 1      | 2       | 113   | 0     | 0.31   |
| Integral    | 5      | 48      | 113   | 1     | 0.30   |
| KingSpec    | 46     | 631     | 126   | 32    | 0.30   |
| Lite-On     | 122    | 891     | 137   | 110   | 0.30   |
| AMD         | 17     | 279     | 135   | 22    | 0.30   |
| Pichau      | 1      | 2       | 108   | 0     | 0.30   |
| GLOWAY      | 8      | 27      | 116   | 38    | 0.30   |
| XSTAR       | 3      | 9       | 118   | 6     | 0.30   |
| TRIVENTA    | 1      | 2       | 105   | 0     | 0.29   |
| INNOVATI... | 16     | 61      | 140   | 3     | 0.29   |
| QUMO        | 10     | 37      | 119   | 2     | 0.29   |
| XUM         | 4      | 17      | 110   | 1     | 0.29   |
| Acer        | 8      | 37      | 103   | 1     | 0.28   |
| KLLISRE     | 1      | 2       | 102   | 0     | 0.28   |
| FORESEE     | 6      | 116     | 101   | 0     | 0.28   |
| BlueRay     | 1      | 2       | 166   | 1     | 0.27   |
| HUGWORLD    | 2      | 5       | 98    | 0     | 0.27   |
| Ant Esports | 2      | 4       | 97    | 1     | 0.26   |
| VSEVEN      | 1      | 3       | 95    | 0     | 0.26   |
| KLEVV       | 5      | 16      | 96    | 192   | 0.26   |
| EYOTA       | 3      | 9       | 96    | 119   | 0.26   |
| SATAFIRM    | 1      | 5       | 189   | 55    | 0.26   |
| XrayDisk    | 14     | 167     | 106   | 21    | 0.26   |
| Origin I... | 1      | 2       | 172   | 6     | 0.25   |
| Foxline     | 8      | 39      | 92    | 0     | 0.25   |
| Wibtek      | 6      | 43      | 92    | 11    | 0.25   |
| AGI         | 10     | 53      | 104   | 10    | 0.25   |
| TwinMOS     | 1      | 3       | 109   | 1     | 0.25   |
| Simmtronics | 1      | 2       | 91    | 0     | 0.25   |
| Silicon ... | 1      | 2       | 91    | 0     | 0.25   |
| V-GeN       | 7      | 14      | 91    | 0     | 0.25   |
| GS Nanotech | 1      | 3       | 90    | 0     | 0.25   |
| Star Drive  | 1      | 8       | 89    | 0     | 0.25   |
| Netac       | 22     | 565     | 101   | 12    | 0.24   |
| Solid       | 2      | 9       | 159   | 1     | 0.24   |
| ASENNO      | 3      | 8       | 156   | 3     | 0.24   |
| EXRAM       | 2      | 6       | 129   | 50    | 0.24   |
| NTC         | 1      | 2       | 87    | 0     | 0.24   |
| Dahua       | 8      | 21      | 87    | 0     | 0.24   |
| WALRAM      | 11     | 74      | 89    | 31    | 0.23   |
| RESCUE      | 2      | 4       | 84    | 0     | 0.23   |
| BHT         | 8      | 50      | 84    | 0     | 0.23   |
| EDILOCA     | 10     | 28      | 104   | 5     | 0.23   |
| Teclast     | 11     | 70      | 88    | 14    | 0.22   |
| G.Skill     | 1      | 3       | 695   | 704   | 0.22   |
| Fanxiang    | 23     | 205     | 86    | 1     | 0.22   |
| EDGE        | 1      | 3       | 79    | 0     | 0.22   |
| Valuetech   | 4      | 16      | 83    | 1     | 0.22   |
| 2-Power     | 3      | 10      | 78    | 1     | 0.21   |
| CYX         | 1      | 8       | 78    | 0     | 0.21   |
| MicroFrom   | 2      | 10      | 77    | 0     | 0.21   |
| EVM         | 4      | 16      | 74    | 0     | 0.21   |
| KOWIN       | 3      | 8       | 74    | 0     | 0.20   |
| Kross El... | 1      | 2       | 86    | 1     | 0.20   |
| BAITITON    | 11     | 44      | 105   | 6     | 0.20   |
| ShanDianZhe | 3      | 11      | 72    | 0     | 0.20   |

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
| Intel     | H10 HBRPEKNX020... | 32 GB  | 3       | 3588  | 0     | 9.83   |
| Intel     | H10 HBRPEKNX010... | 16 GB  | 3       | 3193  | 0     | 8.75   |
| Intel     | H10 HBRPEKNX020... | 32 GB  | 15      | 3084  | 0     | 8.45   |
| Intel     | 7335943            |        |         | 0     | 0     | 5.69   |
| Dell      | Express Flash N... | 1 TB   | 2       | 2033  | 0     | 5.57   |
| Samsung   | MS1PC5ED3ORA3.2T   | 3.2 TB | 8       | 2009  | 0     | 5.50   |
| Intel     | SSDPEDMW800G4      | 800 GB | 2       | 1879  | 0     | 5.15   |
| Dell      | Express Flash N... | 1.6 TB | 4       | 1735  | 0     | 4.76   |
| Intel     | SSDPE2MX450G7      | 450 GB | 13      | 1707  | 0     | 4.68   |
| Samsung   | SSD 983 DCT 1.92TB | 1.9 TB | 2       | 1679  | 0     | 4.60   |
| Intel     | SSDPEDMW400G4      | 400 GB | 11      | 1611  | 0     | 4.41   |
| Corsair   | Force MP500        | 480 GB | 2       | 1519  | 0     | 4.16   |
| Intel     | SSDPEDMD400G4      | 400 GB | 4       | 1389  | 0     | 3.81   |
| Intel     | SSDPEDMW012T4      | 1.2 TB | 5       | 1371  | 0     | 3.76   |
| Intel     | SSDPEKKR128G7      | 128 GB | 2       | 1272  | 0     | 3.49   |
| Mushkin   | MKNSSDPL1TB-D8     | 1 TB   | 3       | 1228  | 0     | 3.36   |
| Samsung   | SSD 950 PRO        | 256 GB | 36      | 1191  | 0     | 3.26   |
| Toshiba   | KXD51RUE1T92       | 1.9 TB | 2       | 1166  | 0     | 3.20   |
| Patriot   | Hellfire M2        | 480 GB | 2       | 1152  | 0     | 3.16   |
| Toshiba   | RD400              | 256 GB | 10      | 1115  | 0     | 3.06   |
| Mushkin   | MKNSSDPL250GB-D8   | 250 GB | 2       | 1101  | 0     | 3.02   |
| Toshiba   | RD400              | 128 GB | 2       | 1083  | 0     | 2.97   |
| Samsung   | MZVPV256HDGL-000L7 | 256 GB | 3       | 1026  | 0     | 2.81   |
| WDC       | WDS512G1X0C-00ENX0 | 512 GB | 21      | 1004  | 0     | 2.75   |
| Intel     | SSDPEKKF010T7      | 1 TB   | 3       | 1349  | 25    | 2.72   |
| Toshiba   | THNSN51T02DU7      | 1 TB   | 2       | 978   | 0     | 2.68   |
| Samsung   | MZVLB256HAHQ-000H7 | 256 GB | 2       | 977   | 0     | 2.68   |
| Samsung   | SSD 950 PRO        | 512 GB | 71      | 971   | 6     | 2.65   |
| ADATA     | SX8000NP           | 512 GB | 4       | 943   | 0     | 2.59   |
| Intel     | SSDPED1D480GA      | 480 GB | 6       | 938   | 0     | 2.57   |
| Kingston  | SKC1000240G        | 240 GB | 5       | 937   | 0     | 2.57   |
| WDC       | CL SN720 SDAQNT... | 512 GB | 12      | 936   | 0     | 2.57   |
| Toshiba   | RD400              | 512 GB | 5       | 926   | 0     | 2.54   |
| ZOTAC     | ZTSSDPG3-480G-GE   | 480 GB | 2       | 919   | 0     | 2.52   |
| Intel     | SSDPE21D480GA      | 480 GB | 6       | 908   | 0     | 2.49   |
| Samsung   | MZQLB960HAJR-00007 | 960 GB | 19      | 906   | 0     | 2.48   |
| Samsung   | MZVPV512HDGL-00000 | 512 GB | 24      | 917   | 1     | 2.43   |
| Intel     | SSDPEKKF256G7H     | 256 GB | 49      | 912   | 39    | 2.42   |
| Toshiba   | THNSN5512GPU7 NVMe | 512 GB | 10      | 874   | 0     | 2.40   |
| Toshiba   | RD400              | 1 TB   | 3       | 855   | 0     | 2.34   |
| Samsung   | MZPLL1T6HAJQ-00005 | 1.6 TB | 2       | 841   | 0     | 2.30   |
| Toshiba   | KXG6AZNV1T02 NV... | 1 TB   | 2       | 833   | 0     | 2.28   |
| Dell      | Express Flash N... | 6.4 TB | 2       | 829   | 0     | 2.27   |
| Samsung   | SM951 NVMe         | 256 GB | 3       | 825   | 0     | 2.26   |
| China     | 128GB              | 128 GB | 2       | 812   | 0     | 2.23   |
| Hikvision | HS-SSD-E2000 1024G | 1 TB   | 2       | 803   | 0     | 2.20   |
| Corsair   | Force MP500        | 120 GB | 18      | 800   | 0     | 2.19   |
| Samsung   | MZVKW1T0HMLH-000L7 | 1 TB   | 4       | 796   | 0     | 2.18   |
| Samsung   | MZVLV256HCHP-000L1 | 256 GB | 2       | 793   | 0     | 2.17   |
| Toshiba   | KXG50PNV1T02 NVMe  | 1 TB   | 8       | 782   | 0     | 2.14   |
| SPCC      | M.2 PCIE SSD       | 2 TB   | 3       | 781   | 0     | 2.14   |
| ASint     | AS806              | 256 GB | 2       | 777   | 0     | 2.13   |
| Toshiba   | KBG40ZPZ1T02 ME... | 1 TB   | 3       | 770   | 0     | 2.11   |
| Plextor   | PX-512M9PeG        | 512 GB | 5       | 766   | 0     | 2.10   |
| Samsung   | MZQLB3T8HALS-00007 | 3.8 TB | 28      | 755   | 0     | 2.07   |
| Samsung   | PM951 NVMe         | 1 TB   | 8       | 749   | 0     | 2.05   |
| Intel     | MEMPEK1W032GA      | 32 GB  | 7       | 743   | 0     | 2.04   |
| Viper     | M.2 VPN100         | 1 TB   | 7       | 731   | 0     | 2.00   |
| Intel     | SSDPEKKW128G7      | 128 GB | 21      | 1119  | 1     | 2.00   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 3       | 727   | 0     | 1.99   |
| Intenso   | JAJPR600M2TB       | 2 TB   | 2       | 723   | 0     | 1.98   |
| Corsair   | Force MP500        | 240 GB | 21      | 769   | 1     | 1.97   |
| Intel     | SSDPED1D280GA      | 280 GB | 9       | 719   | 0     | 1.97   |
| Silico... | Asgard AN3 2TNV... | 2 TB   | 14      | 718   | 0     | 1.97   |
| Samsung   | MZ1LB960HAJQ-000MV | 960 GB | 2       | 717   | 0     | 1.97   |
| PNY       | CS3030 250GB SSD   | 250 GB | 38      | 702   | 0     | 1.93   |
| Intel     | SSDPEKKW512G7      | 512 GB | 43      | 903   | 93    | 1.91   |
| KLEVV     | CRAS C720 M.2 N... | 512 GB | 2       | 696   | 0     | 1.91   |
| J.ZAO     | 5 SERIES 512GB SSD | 512 GB | 3       | 696   | 0     | 1.91   |
| SPCC      | M.2 PCIe SSD       | 500 GB | 3       | 693   | 0     | 1.90   |
| Micron    | 7300_MTFDHBE960TDF | 960 GB | 6       | 692   | 0     | 1.90   |
| WDC       | WUS4BB076D7P3E3    | 7.6 TB | 6       | 687   | 0     | 1.88   |
| Samsung   | MZVPV128HDGM-00000 | 128 GB | 16      | 686   | 0     | 1.88   |
| Intel     | SSDPEDKE020T7      | 2 TB   | 3       | 684   | 0     | 1.88   |
| Samsung   | MZVLB256HAHQ-000H2 | 256 GB | 6       | 683   | 0     | 1.87   |
| ADATA     | SX8000NP           | 128 GB | 2       | 680   | 0     | 1.86   |
| Samsung   | MZWLL1T6HAJQ-00005 | 1.6 TB | 4       | 673   | 0     | 1.85   |
| KIOXIA    | KXG50PNV2T04       | 2 TB   | 3       | 667   | 0     | 1.83   |
| Kingston  | RBUSNS8154P3102... | 1 TB   | 2       | 667   | 0     | 1.83   |
| SanDisk   | A400 NVMe          | 256 GB | 3       | 665   | 0     | 1.82   |
| Toshiba   | KXG50PNV2T04 1.6TB | 1.6 TB | 2       | 664   | 0     | 1.82   |
| Toshiba   | THNSN5512GPUK NVMe | 512 GB | 64      | 671   | 2     | 1.81   |
| Asgard    | AN3 2TNVMe-M.2-80  | 2 TB   | 2       | 654   | 0     | 1.79   |
| Lite-On   | CL1-4D128          | 128 GB | 3       | 649   | 0     | 1.78   |
| Intel     | SSDPELKX010T8      | 1 TB   | 5       | 643   | 0     | 1.76   |
| WDC       | WDS200T1XHE-00AFY0 | 2 TB   | 7       | 641   | 0     | 1.76   |
| KIOXIA    | KXG6APNV2T04       | 2 TB   | 2       | 639   | 0     | 1.75   |
| Intel     | SSDPEKKF512G7H     | 512 GB | 12      | 702   | 21    | 1.75   |
| WDC       | WDS256G1X0C-00ENX0 | 256 GB | 36      | 637   | 0     | 1.75   |
| Toshiba   | THNSN5256GPU7 NVMe | 256 GB | 12      | 637   | 0     | 1.75   |
| Intel     | SSDPEKKF360G7H     | 360 GB | 11      | 698   | 17    | 1.74   |
| Kingston  | SKC1000480G        | 480 GB | 5       | 628   | 0     | 1.72   |
| Intel     | SSDPEKKW256G7      | 256 GB | 103     | 796   | 51    | 1.72   |
| Intel     | SSDPED1D960GAY     | 960 GB | 5       | 730   | 203   | 1.71   |
| Samsung   | MZVPV256HDGL-00000 | 256 GB | 19      | 651   | 14    | 1.71   |
| Toshiba   | THNSN51T02DUK NVMe | 1 TB   | 18      | 689   | 57    | 1.70   |
| Toshiba   | KXG50PNV2T04 NVMe  | 2 TB   | 5       | 618   | 0     | 1.69   |
| Phison    | ESO256GMFCH-E3C-2  | 256 GB | 4       | 614   | 0     | 1.68   |
| Samsung   | MZVKW1T0HMLH-00000 | 1 TB   | 6       | 608   | 0     | 1.67   |
| Samsung   | SM951 NVMe         | 512 GB | 3       | 607   | 0     | 1.66   |
| Samsung   | MZVLB1T0HALR-000H2 | 1 TB   | 4       | 605   | 0     | 1.66   |
| Corsair   | Force MP600        | 2 TB   | 40      | 603   | 0     | 1.65   |
| Intel     | SSDPEKKW020T8      | 2 TB   | 5       | 603   | 0     | 1.65   |
| Samsung   | MZVPV512HDGL-000H1 | 512 GB | 8       | 602   | 0     | 1.65   |
| HP        | SSD EX900 Pro      | 1 TB   | 2       | 601   | 0     | 1.65   |
| Plextor   | PX-1TM9PG +        | 1 TB   | 2       | 599   | 0     | 1.64   |
| Samsung   | MZQLB960HAJR-00003 | 960 GB | 4       | 588   | 0     | 1.61   |
| Seagate   | FireCuda 510 SS... | 500 GB | 4       | 583   | 0     | 1.60   |
| Samsung   | MZVPV256HDGL-000H1 | 256 GB | 11      | 732   | 25    | 1.59   |
| Toshiba   | KXG50ZNV1T02 NVMe  | 1 TB   | 45      | 575   | 0     | 1.58   |
| Toshiba   | THNSF5256GPUK      | 256 GB | 21      | 574   | 0     | 1.57   |
| Team      | TM8FP4512G         | 512 GB | 5       | 573   | 0     | 1.57   |
| Hikvision | HS-SSD-C2000       | 1 TB   | 3       | 572   | 0     | 1.57   |
| Toshiba   | KXG50ZNV256G NVMe  | 256 GB | 80      | 569   | 0     | 1.56   |
| Samsung   | PM951 NVMe         | 512 GB | 24      | 564   | 0     | 1.55   |
| HP        | SSD EX900 Pro      | 256 GB | 2       | 561   | 0     | 1.54   |
| Samsung   | MZVLV128HCGR-00000 | 128 GB | 5       | 557   | 0     | 1.53   |
| Gigabyte  | GP-ASM2NE6100TTTD  | 1 TB   | 21      | 551   | 0     | 1.51   |
| Phison    | APS-SE20G-2T       | 2 TB   | 4       | 548   | 0     | 1.50   |
| WDC       | WDS200T3XHC-00SJG0 | 2 TB   | 6       | 548   | 0     | 1.50   |
| Toshiba   | KXG50ZNV512G NVMe  | 512 GB | 104     | 547   | 0     | 1.50   |
| KIOXIA    | KXG60PNV1T02 NVMe  | 1 TB   | 6       | 542   | 0     | 1.49   |
| Mushkin   | MKNSSDHL500GB-D8   | 500 GB | 3       | 663   | 336   | 1.47   |
| Goodram   | SSDPR-PX500-01T-80 | 1 TB   | 10      | 533   | 0     | 1.46   |
| Toshiba   | THNSN5256GPUK NVMe | 256 GB | 40      | 533   | 0     | 1.46   |
| Toshiba   | THNSF5512GPUK      | 512 GB | 30      | 527   | 0     | 1.45   |
| PNY       | CS3030 1000GB SSD  | 1 TB   | 11      | 526   | 0     | 1.44   |
| Goodram   | IR-SSDPR-P34B-0... | 2 TB   | 6       | 525   | 0     | 1.44   |
| Phison    | Sabrent Rocket Q   | 1 TB   | 187     | 532   | 6     | 1.43   |
| Intel     | SSDPED1K375GA      | 375 GB | 4       | 522   | 0     | 1.43   |
| Intel     | HBRPEKNL0202AHO    | 32 GB  | 2       | 522   | 0     | 1.43   |
| Toshiba   | KXG5AZNV1T02       | 1 TB   | 10      | 521   | 0     | 1.43   |
| Intel     | SSDPEKKW010T7      | 1 TB   | 6       | 1048  | 173   | 1.42   |
| Intel     | HBRPEKNL0202AH     | 512 GB | 2       | 519   | 0     | 1.42   |
| Samsung   | MZVLV512HCJH-000L2 | 512 GB | 4       | 518   | 0     | 1.42   |
| Samsung   | MZPLJ1T6HBJR-00007 | 736 GB | 2       | 515   | 0     | 1.41   |
| Toshiba   | KXG5AZNV512G NV... | 512 GB | 3       | 513   | 0     | 1.41   |
| Samsung   | MZVKV512HAJH-000L1 | 512 GB | 20      | 513   | 0     | 1.41   |
| Kingston  | SNVS2000GB         | 2 TB   | 7       | 513   | 0     | 1.41   |
| Gigaby... | GP-AG4500G         | 500 GB | 6       | 512   | 0     | 1.41   |
| Samsung   | SM961 NVMe         | 1 TB   | 7       | 539   | 3     | 1.40   |
| Intel     | SSDPEKKF256G7L     | 256 GB | 85      | 579   | 55    | 1.39   |
| Phison    | MANIX2000GB-G4SS   | 2 TB   | 2       | 502   | 0     | 1.38   |
| ADATA     | SX8200NP           | 240 GB | 8       | 520   | 15    | 1.37   |
| Crucial   | CT2000P1SSD8       | 2 TB   | 10      | 501   | 0     | 1.37   |
| Intel     | SSDPEKNW020T9      | 2 TB   | 5       | 501   | 0     | 1.37   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 3       | 500   | 0     | 1.37   |
| HP        | SSD EX950          | 1 TB   | 35      | 500   | 0     | 1.37   |
| Corsair   | Force MP510 1.9TB  | 1.9 TB | 24      | 497   | 0     | 1.36   |
| Smartbuy  | m.2 PS5013-2280T   | 512 GB | 2       | 496   | 0     | 1.36   |
| ADATA     | SX8200NP           | 480 GB | 17      | 494   | 0     | 1.36   |
| Corsair   | Force MP600        | 500 GB | 35      | 492   | 0     | 1.35   |
| Kingston  | SA1000M8960G       | 960 GB | 4       | 491   | 0     | 1.35   |
| KIOXIA    | KBG30ZMV128G       | 128 GB | 5       | 490   | 0     | 1.34   |
| Intel     | SSDPE2KX010T8      | 1 TB   | 5       | 489   | 0     | 1.34   |
| Gigabyte  | GP-ASM2NE2512GTTDR | 512 GB | 2       | 489   | 0     | 1.34   |
| Phison    | 512GB NVMe SSD     | 512 GB | 4       | 489   | 0     | 1.34   |
| PNY       | CS3030 2TB SSD     | 2 TB   | 33      | 488   | 0     | 1.34   |
| Lexar     | SSD                | 256 GB | 14      | 486   | 0     | 1.33   |
| Corsair   | Force MP510        | 960 GB | 63      | 486   | 0     | 1.33   |
| Intel     | SSDPEK1W060GA      | 64 GB  | 4       | 482   | 0     | 1.32   |
| Samsung   | Portable SSD T7... | 1 TB   | 6       | 480   | 0     | 1.32   |
| Intel     | SSDPE2KX020T8      | 2 TB   | 15      | 479   | 0     | 1.31   |
| Toshiba   | THNSN5128GPU7      | 128 GB | 16      | 478   | 0     | 1.31   |
| Phison    | Sabrent SB-RKT4... | 8 TB   | 2       | 478   | 0     | 1.31   |
| Reletech  | P400 M.2 Pro Q2... | 2 TB   | 2       | 477   | 0     | 1.31   |
| Kingston  | SKC2000M8250G      | 250 GB | 8       | 476   | 0     | 1.31   |
| Hikvision | HS-SSD-E2000 512G  | 512 GB | 3       | 475   | 0     | 1.30   |
| Asgard    | AN3 1TNVMe-M.2-80  | 1 TB   | 2       | 472   | 0     | 1.30   |
| Phison    | PM8256GPTCB4B8T... | 256 GB | 2       | 468   | 0     | 1.28   |
| Asgard    | AN2 250NVMe-M.2-80 | 250 GB | 4       | 466   | 0     | 1.28   |
| Samsung   | PM951 NVMe         | 256 GB | 31      | 464   | 0     | 1.27   |
| Intel     | SSDPEKNW020T8      | 2 TB   | 114     | 468   | 1     | 1.26   |
| Goodram   | IR-SSDPR-P34B-0... | 1 TB   | 3       | 460   | 0     | 1.26   |
| Toshiba   | KXG60ZNV1T02 NVMe  | 1 TB   | 29      | 459   | 0     | 1.26   |
| EMTEC     | X410               | 4 TB   | 2       | 459   | 0     | 1.26   |
| Toshiba   | KXG60ZNV512G NVMe  | 512 GB | 70      | 458   | 0     | 1.26   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 3       | 456   | 0     | 1.25   |
| SSSTC     | CL1-3D256          | 256 GB | 4       | 456   | 0     | 1.25   |
| Toshiba   | THNSN5256GPU7      | 256 GB | 29      | 455   | 0     | 1.25   |
| Toshiba   | KXG50ZNV1T02       | 1 TB   | 11      | 455   | 0     | 1.25   |
| T-FORCE   | TM8FP5512G         | 512 GB | 2       | 455   | 0     | 1.25   |
| WDC       | WDS100T3XHC-00SJG0 | 1 TB   | 30      | 455   | 0     | 1.25   |
| Corsair   | Force MP600        | 1 TB   | 139     | 454   | 0     | 1.25   |
| T-FORCE   | TM8FPZ004T         | 4 TB   | 2       | 452   | 0     | 1.24   |
| Toshiba   | RC500              | 250 GB | 3       | 449   | 0     | 1.23   |
| KIOXIA... | SSD                | 250 GB | 4       | 448   | 0     | 1.23   |
| Samsung   | MZ1LB3T8HMLA-00007 | 3.8 TB | 4       | 447   | 0     | 1.23   |
| Phison    | APS-SE20Q-1T       | 1 TB   | 3       | 446   | 0     | 1.22   |
| Toshiba   | THNSN51T02DUK      | 1 TB   | 3       | 446   | 0     | 1.22   |
| Phison    | APS-SE20G-256      | 256 GB | 5       | 445   | 0     | 1.22   |
| SK hynix  | PC601A NVMe        | 1 TB   | 10      | 445   | 0     | 1.22   |
| Samsung   | MZQLB1T9HAJR-00007 | 1.9 TB | 20      | 490   | 1     | 1.21   |
| Silico... | GSDFN512TS3F1OGCX  | 512 GB | 2       | 443   | 0     | 1.21   |
| KIOXIA    | KCD6XVUL6T40       | 6.4 TB | 2       | 443   | 0     | 1.21   |
| Phison    | Neutron NX500      | 800 GB | 2       | 442   | 0     | 1.21   |
| Samsung   | MZVLV256HCHP-00000 | 256 GB | 19      | 442   | 0     | 1.21   |
| KIOXIA    | KCD61VUL6T40       | 6.4 TB | 2       | 441   | 0     | 1.21   |
| Gigabyte  | GP-AG70S2TB        | 2 TB   | 5       | 438   | 0     | 1.20   |
| Hikvision | HS-SSD-E2000 2048G | 2 TB   | 2       | 437   | 0     | 1.20   |
| KIOXIA    | KXG6AZNV256G       | 256 GB | 2       | 435   | 0     | 1.19   |
| WDC       | WDS500G2X0C-00L350 | 500 GB | 40      | 434   | 0     | 1.19   |
| Toshiba   | KXG50ZNV512G       | 512 GB | 80      | 434   | 0     | 1.19   |
| KIOXIA    | KBG4AZNS512G       | 512 GB | 3       | 433   | 0     | 1.19   |
| Samsung   | MZVPV128HDGM-000H1 | 128 GB | 2       | 428   | 0     | 1.18   |
| Phison    | ESR512GMFCM-E8G... | 512 GB | 2       | 427   | 0     | 1.17   |
| Toshiba   | KBG20ZMS256G NVMe  | 256 GB | 3       | 426   | 0     | 1.17   |
| Seagate   | FireCuda 510 SS... | 1 TB   | 11      | 425   | 0     | 1.17   |
| Intel     | MEMPEK1J016GAH     | 16 GB  | 7       | 425   | 0     | 1.17   |
| Intel     | SSDPEKKW512G8      | 512 GB | 30      | 424   | 0     | 1.16   |
| Intel     | SSDPF2KX038T9N     | 3.8 TB | 3       | 423   | 0     | 1.16   |
| SK hynix  | PC601 HFS256GD9... | 256 GB | 15      | 422   | 0     | 1.16   |
| Gigabyte  | GP-ASM2NE6200TTTD  | 2 TB   | 17      | 421   | 0     | 1.16   |
| Seagate   | FireCuda 510 SS... | 1 TB   | 16      | 421   | 0     | 1.16   |
| HP        | SSD EX920          | 512 GB | 20      | 420   | 0     | 1.15   |
| Intel     | MEMPEK1W016GA      | 16 GB  | 20      | 450   | 4     | 1.15   |
| Intel     | SSDPF2KX076T1      | 3.8 TB | 8       | 418   | 0     | 1.15   |
| Aura      | Pro X2             | 960 GB | 17      | 418   | 0     | 1.15   |
| Samsung   | MZVKW512HMJP-000H1 | 512 GB | 28      | 422   | 1     | 1.15   |
| Toshiba   | KBG40ZPZ256G ME... | 256 GB | 9       | 416   | 0     | 1.14   |
| Samsung   | PM981 NVMe         | 2 TB   | 3       | 415   | 0     | 1.14   |
| Corsair   | Force MP300        | 240 GB | 9       | 413   | 0     | 1.13   |
| SK hynix  | PC601 NVMe         | 256 GB | 22      | 413   | 0     | 1.13   |
| Intel     | SSDPEKKW256G8      | 256 GB | 77      | 426   | 14    | 1.13   |
| Toshiba   | KXG5AZNV256G NV... | 256 GB | 2       | 412   | 0     | 1.13   |
| Phison    | ESR512GTLCG-EAC-4  | 512 GB | 10      | 410   | 0     | 1.13   |
| Toshiba   | KXD51LN11T92 1.9TB | 1.9 TB | 3       | 409   | 0     | 1.12   |
| Intel     | HBRPEKNX0202ACO    | 32 GB  | 6       | 409   | 0     | 1.12   |
| FIKWOT    | FN501 Pro          | 2 TB   | 2       | 405   | 0     | 1.11   |
| Samsung   | PM981a NVMe SED    | 512 GB | 3       | 403   | 0     | 1.10   |
| Corsair   | MP400              | 1 TB   | 18      | 402   | 0     | 1.10   |
| WDC       | WDS250G2X0C-00L350 | 250 GB | 31      | 401   | 0     | 1.10   |
| WDC       | WDS500G1B0C-00S6U0 | 500 GB | 30      | 414   | 1     | 1.10   |
| Mushkin   | MKNSSDHL250GB-D8   | 250 GB | 6       | 417   | 168   | 1.10   |
| Patriot   | Hellfire M2        | 240 GB | 3       | 400   | 0     | 1.10   |
| MSI       | M370               | 1 TB   | 3       | 400   | 0     | 1.10   |
| Gigabyte  | GP-GSM2NE3100TNTD  | 1 TB   | 20      | 399   | 0     | 1.09   |
| LDLC      | F8+M.2 120         | 120 GB | 2       | 399   | 0     | 1.09   |
| Patriot   | P300               | 512 GB | 4       | 398   | 0     | 1.09   |
| Toshiba   | KXG60PNV512G NVMe  | 512 GB | 2       | 396   | 0     | 1.09   |
| WDC       | WDS100T2X0C-00L350 | 1 TB   | 18      | 394   | 0     | 1.08   |
| Toshiba   | THNSN0256GTYA      | 256 GB | 7       | 391   | 0     | 1.07   |
| Phison    | Sabrent            | 1 TB   | 296     | 391   | 0     | 1.07   |
| Phison    | Sabrent Rocket 4.0 | 2 TB   | 28      | 390   | 0     | 1.07   |
| Plextor   | PX-256M9PeY        | 256 GB | 5       | 386   | 0     | 1.06   |
| Intel     | SSDPEKKF010T8      | 1 TB   | 6       | 382   | 0     | 1.05   |
| Intel     | SSDPF2NV307TZ      | 30.... | 2       | 381   | 0     | 1.05   |
| Toshiba   | THNSN5512GPU7      | 512 GB | 20      | 380   | 0     | 1.04   |
| SK hynix  | PC300 NVMe         | 512 GB | 15      | 379   | 0     | 1.04   |
| Hikvision | HS-SSD-E2000 256G  | 256 GB | 4       | 378   | 0     | 1.04   |
| Gigabyte  | GP-ASM2NE6500GTTD  | 500 GB | 8       | 378   | 0     | 1.04   |
| SSSTC     | CL1-4D256-D22      | 256 GB | 6       | 376   | 0     | 1.03   |
| Goodram   | IR-SSDPR-P34B-2... | 256 GB | 5       | 375   | 0     | 1.03   |
| HP        | SSD EX920          | 256 GB | 3       | 447   | 1     | 1.03   |
| Toshiba   | THNSN5128GPUK      | 128 GB | 2       | 374   | 0     | 1.03   |
| addlink   | M.2 PCIE G3x4 NVMe | 1 TB   | 39      | 374   | 0     | 1.03   |
| Phison    | M.2 PCIE G3x4 NVMe | 1 TB   | 4       | 373   | 0     | 1.02   |
| Corsair   | Force MP510        | 480 GB | 64      | 373   | 0     | 1.02   |
| Toshiba   | THNSN5512GPUK      | 512 GB | 20      | 372   | 0     | 1.02   |
| Gigabyte  | GP-ASM2NE2256GTTDR | 256 GB | 5       | 372   | 0     | 1.02   |
| Gigabyte  | GP-AG4500G         | 500 GB | 13      | 371   | 0     | 1.02   |
| Intel     | SSDPEKNW010T8      | 1 TB   | 392     | 375   | 3     | 1.02   |
| SK hynix  | HFM128GDHTNG-8310B | 128 GB | 15      | 370   | 0     | 1.02   |
| Intel     | SSDPEKKF512G7L     | 512 GB | 12      | 528   | 222   | 1.02   |
| SanDisk   | A400 NVMe          | 512 GB | 3       | 370   | 0     | 1.01   |
| HP        | SSD EX920          | 1 TB   | 20      | 369   | 0     | 1.01   |
| Seagate   | BarraCuda Q5 ZP... | 2 TB   | 10      | 369   | 0     | 1.01   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 23      | 368   | 0     | 1.01   |
| Phison    | Metabox Perform... | 2 TB   | 6       | 367   | 0     | 1.01   |
| Intel     | HBRPEKNX0202AC     | 512 GB | 6       | 367   | 0     | 1.01   |
| Phison    | Sabrent Rocket 4.0 | 1 TB   | 140     | 366   | 0     | 1.00   |
| tigo      | SSD                | 256 GB | 2       | 366   | 0     | 1.00   |
| aigo      | NVMe SSD P2000     | 256 GB | 2       | 366   | 0     | 1.00   |
| Toshiba   | KXG60ZNV1T02       | 1 TB   | 33      | 365   | 0     | 1.00   |
| PNY       | CS3030 1TB SSD     | 1 TB   | 36      | 378   | 8     | 1.00   |
| LDLC      | F8+M.2 480         | 480 GB | 10      | 364   | 0     | 1.00   |
| SK hynix  | PC611 NVMe         | 256 GB | 7       | 364   | 0     | 1.00   |
| Patriot   | Scorch M2          | 512 GB | 6       | 364   | 0     | 1.00   |
| ADATA     | LEGEND 850 LITE    | 2 TB   | 4       | 363   | 0     | 1.00   |
| WDC       | PC SN720 SDAPNT... | 512 GB | 5       | 363   | 0     | 1.00   |
| EMTEC     | X300               | 256 GB | 4       | 362   | 0     | 0.99   |
| Corsair   | Force MP510        | 4 TB   | 6       | 362   | 0     | 0.99   |
| Crucial   | CT1000P1SSD8       | 1 TB   | 374     | 380   | 23    | 0.99   |
| WDC       | WDBRPG5000ANC-WRSN | 500 GB | 35      | 361   | 0     | 0.99   |
| Toshiba   | THNSN51T02DU7 NVMe | 1 TB   | 8       | 360   | 0     | 0.99   |
| Intel     | HBRPEKNX0203AHO    | 32 GB  | 25      | 360   | 0     | 0.99   |
| Intel     | HBRPEKNX0202AHO    | 32 GB  | 86      | 368   | 5     | 0.98   |
| Intel     | SSDPE2MX012T7      | 1.2 TB | 4       | 358   | 0     | 0.98   |
| Lite-On   | CL1-3D128-Q11 NVMe | 128 GB | 5       | 358   | 0     | 0.98   |
| ADATA     | AGAMMIXS70B-2T-CS  | 2 TB   | 2       | 358   | 0     | 0.98   |
| ADATA     | SX8200PNP          | 1 TB   | 242     | 381   | 33    | 0.98   |
| Samsung   | PM981 NVMe         | 1 TB   | 24      | 356   | 0     | 0.98   |
| MSI       | M480               | 1 TB   | 4       | 356   | 0     | 0.98   |
| Samsung   | MZQL23T8HCLS-00... | 3.8 TB | 46      | 355   | 0     | 0.97   |
| SanDisk   | WD_BLACK SN850     | 2 TB   | 3       | 354   | 0     | 0.97   |
| WDC       | WDS250G1B0C-00S6U0 | 250 GB | 20      | 353   | 0     | 0.97   |
| KIOXIA    | KCD61LUL960G       | 960 GB | 2       | 352   | 0     | 0.97   |
| Samsung   | MZVLV256HCHP-000L2 | 256 GB | 19      | 351   | 0     | 0.96   |
| T-FORCE   | TM8FPQ004T         | 4 TB   | 3       | 351   | 0     | 0.96   |
| Intel     | H10 HBRPEKNX010... | 256 GB | 5       | 350   | 0     | 0.96   |
| KingSpec  | NE-256             | 256 GB | 8       | 390   | 3     | 0.96   |
| Samsung   | MZ1LB960HAJQ-00007 | 960 GB | 7       | 349   | 0     | 0.96   |
| ADATA     | SX8200PNP          | 512 GB | 215     | 352   | 1     | 0.96   |
| Mushkin   | MKNSSDPL500GB-D8   | 500 GB | 3       | 348   | 0     | 0.96   |
| SK hynix  | SHGP31-1000GM-2    | 1 TB   | 46      | 347   | 0     | 0.95   |
| Phison    | E12-512G-PHISON... | 512 GB | 10      | 347   | 0     | 0.95   |
| Plextor   | PX-256M9PeG        | 256 GB | 8       | 346   | 0     | 0.95   |
| Intel     | MEMPEK1J016GA      | 16 GB  | 21      | 372   | 50    | 0.95   |
| Toshiba   | KXG50ZNV256G       | 256 GB | 78      | 345   | 0     | 0.95   |
| Kingston  | SKC2000M8500G      | 500 GB | 7       | 430   | 144   | 0.95   |
| Seagate   | BarraCuda 510 S... | 500 GB | 7       | 344   | 0     | 0.94   |
| Dell      | Express Flash N... | 3.2 TB | 4       | 344   | 0     | 0.94   |
| Silico... | NVME SSD           | 1 TB   | 3       | 343   | 0     | 0.94   |
| Intel     | HBRPEKNX0203A      | 1 TB   | 5       | 343   | 0     | 0.94   |
| Gigaby... | GP-ASM2NE6100TTTD  | 1 TB   | 11      | 342   | 0     | 0.94   |
| Intel     | SSDPEK1W120GA      | 118 GB | 2       | 341   | 0     | 0.94   |
| Corsair   | MP600 CORE         | 1 TB   | 13      | 340   | 0     | 0.93   |
| WDC       | WDBA3V5000ANC-WRSN | 500 GB | 6       | 339   | 0     | 0.93   |
| Corsair   | MP600 PRO          | 2 TB   | 11      | 339   | 0     | 0.93   |
| Phison    | PP3480-R           | 1 TB   | 2       | 339   | 0     | 0.93   |
| Asgard    | AN4+2TNVMe-M.2-80  | 2 TB   | 2       | 338   | 0     | 0.93   |
| Toshiba   | THNSN5256GPUK      | 256 GB | 15      | 411   | 9     | 0.93   |
| Intel     | HBRPEKNX0203AH     | 1 TB   | 26      | 337   | 0     | 0.93   |
| SSSTC     | CL1-8D128          | 128 GB | 3       | 337   | 0     | 0.92   |
| KIOXIA    | KCD6XLUL15T3       | 15.... | 4       | 337   | 0     | 0.92   |
| Toshiba   | KBG30ZMV128G       | 128 GB | 12      | 358   | 85    | 0.92   |
| AMD       | R5MP120G8          | 120 GB | 10      | 336   | 0     | 0.92   |
| Plextor   | PX-512M9PGN +      | 512 GB | 3       | 336   | 0     | 0.92   |
| Plextor   | PX-256M8PeGN       | 256 GB | 4       | 336   | 0     | 0.92   |
| Samsung   | MZVLW128HEGR-000L1 | 128 GB | 18      | 335   | 0     | 0.92   |
| Intel     | SSDPEKNW010T9      | 1 TB   | 63      | 334   | 0     | 0.92   |
| Micron    | 9300_MTFDHAL15T... | 15.... | 3       | 333   | 0     | 0.91   |
| WDC       | WDS500G3XHC-00SJG0 | 500 GB | 39      | 332   | 0     | 0.91   |
| Toshiba   | KXG5AZNV256G       | 256 GB | 34      | 330   | 0     | 0.91   |
| Corsair   | Force MP300        | 120 GB | 6       | 330   | 0     | 0.90   |
| Intel     | SSDPEKNW256G8      | 256 GB | 2       | 329   | 0     | 0.90   |
| XPG       | GAMMIX S11         | 480 GB | 10      | 398   | 101   | 0.90   |
| KIOXIA... | SSD                | 1 TB   | 14      | 328   | 0     | 0.90   |
| MSI       | M480 PRO           | 1 TB   | 3       | 327   | 0     | 0.90   |
| Silico... | Longline SSD       | 512 GB | 2       | 327   | 0     | 0.90   |
| SanDisk   | WD_BLACK SN750     | 2 TB   | 23      | 326   | 0     | 0.89   |
| Intel     | HBRPEKNX0203AO     | 32 GB  | 6       | 325   | 0     | 0.89   |
| KIOXIA    | KXG60PNV2T04 NVMe  | 2 TB   | 20      | 325   | 0     | 0.89   |
| Toshiba   | THNSF5256GCJ7      | 256 GB | 2       | 325   | 0     | 0.89   |
| Samsung   | Portable SSD T7... | 2 TB   | 7       | 324   | 0     | 0.89   |
| WDC       | WDS200T3X0C-00SJG0 | 2 TB   | 17      | 324   | 0     | 0.89   |
| Samsung   | MZVL2256HCHQ-00BL7 | 256 GB | 3       | 845   | 349   | 0.89   |
| T-FORCE   | TM8FPV002T         | 2 TB   | 2       | 323   | 0     | 0.89   |
| WDC       | WDS400T3X0C-00SJG0 | 4 TB   | 4       | 322   | 0     | 0.88   |
| Kingston  | SA2000M8500G       | 500 GB | 230     | 322   | 0     | 0.88   |
| Intel     | HBRPEKNX0202AH     | 512 GB | 95      | 322   | 0     | 0.88   |
| WDC       | WDS500G3X0C-00SJG0 | 500 GB | 281     | 322   | 4     | 0.88   |
| SanDisk   | WD_BLACK SN850 ... | 1 TB   | 2       | 321   | 0     | 0.88   |
| Phison    | E12-256G-PHISON... | 256 GB | 4       | 321   | 0     | 0.88   |
| China     | M2 Series NVMe ... | 1 TB   | 3       | 400   | 1     | 0.88   |
| SK hynix  | PC601 NVMe         | 512 GB | 75      | 319   | 0     | 0.88   |
| Mushkin   | MKNSSDPE500GB-D8   | 500 GB | 2       | 319   | 0     | 0.88   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 8       | 319   | 0     | 0.88   |
| SanDisk   | A400 SD9PN9U-25... | 256 GB | 4       | 318   | 0     | 0.87   |
| Transcend | TS1TMTE220S        | 1 TB   | 22      | 337   | 93    | 0.87   |
| Samsung   | MZ1LB1T9HALS-00007 | 1.9 TB | 4       | 317   | 0     | 0.87   |
| SK hynix  | PC601 NVMe         | 1 TB   | 13      | 410   | 1     | 0.87   |
| SPCC      | M.2 PCIE SSD       | 1 TB   | 8       | 316   | 0     | 0.87   |
| SanDisk   | Extreme Pro        | 500 GB | 24      | 315   | 0     | 0.87   |
| BIWIN     | NI201_256GB        | 256 GB | 2       | 315   | 0     | 0.86   |
| KIOXIA    | KXG60PNV2T04       | 2 TB   | 13      | 315   | 0     | 0.86   |
| KIOXIA    | KXG60ZNV1T02 NVMe  | 1 TB   | 81      | 314   | 0     | 0.86   |
| Intel     | SSDPEKNW512G8      | 512 GB | 569     | 316   | 1     | 0.86   |
| ADATA     | SX6000NP           | 256 GB | 5       | 339   | 3     | 0.86   |
| SK hynix  | PC601 HFS512GD9... | 512 GB | 31      | 311   | 0     | 0.85   |
| Seagate   | FireCuda 520 SS... | 500 GB | 32      | 311   | 0     | 0.85   |
| KIOXIA    | KXG60ZNV512G NVMe  | 512 GB | 71      | 311   | 0     | 0.85   |
| Kingston  | SA2000M8250G       | 250 GB | 173     | 311   | 0     | 0.85   |
| Phison    | Viper M.2 VPN100   | 1 TB   | 37      | 309   | 0     | 0.85   |
| Crucial   | CT500P1SSD8        | 500 GB | 170     | 334   | 16    | 0.85   |
| Verbatim  | Vi3000 Internal... | 2 TB   | 2       | 308   | 0     | 0.84   |
| WDC       | WDBA3V0010BNC-WRSN | 1 TB   | 17      | 306   | 0     | 0.84   |
| Phison    | Sabrent Rocket Q4  | 2 TB   | 29      | 306   | 0     | 0.84   |
| Lite-On   | CX2-8B256-Q11 NVMe | 256 GB | 12      | 381   | 41    | 0.84   |
| Corsair   | MP600 PRO XT       | 2 TB   | 12      | 305   | 0     | 0.84   |
| XrayDisk  | 256GB              | 256 GB | 8       | 305   | 0     | 0.84   |
| China     | NVME SSD           | 1 TB   | 12      | 308   | 1     | 0.83   |
| XPG       | GAMMIX S11 Pro     | 1 TB   | 201     | 305   | 1     | 0.83   |
| Samsung   | MZ1LW960HMJP-00003 | 960 GB | 2       | 303   | 0     | 0.83   |
| PNY       | CS2130 2TB SSD     | 2 TB   | 8       | 303   | 0     | 0.83   |
| Micron    | 2200 NVMe          | 512 GB | 5       | 302   | 0     | 0.83   |
| Toshiba   | KXG5AZNV512G       | 512 GB | 27      | 302   | 0     | 0.83   |
| Goodram   | IRP-SSDPR-P44A-... | 2 TB   | 3       | 302   | 0     | 0.83   |
| Seagate   | FireCuda 520 SS... | 2 TB   | 22      | 301   | 0     | 0.83   |
| Toshiba   | RC500              | 500 GB | 10      | 676   | 203   | 0.83   |
| WDC       | WDS100T2B0C-00PXH0 | 1 TB   | 431     | 303   | 5     | 0.82   |
| PNY       | CS3140 4TB SSD     | 4 TB   | 3       | 300   | 0     | 0.82   |
| Transcend | TS256GMTE220S      | 256 GB | 17      | 300   | 0     | 0.82   |
| Predator  | SSD GM3500         | 2 TB   | 2       | 299   | 0     | 0.82   |
| Mushkin   | MKNSSDTS512GB-D8   | 512 GB | 3       | 298   | 0     | 0.82   |
| Intel     | SSDPE21D015TA      | 1.5 TB | 4       | 297   | 0     | 0.81   |
| Toshiba   | KXG60ZNV256G NVMe  | 256 GB | 40      | 297   | 0     | 0.81   |
| Intel     | SSDPEK1W120GAH     | 118 GB | 2       | 296   | 0     | 0.81   |
| Smartbuy  | m.2 PS5013-2280T   | 128 GB | 3       | 296   | 0     | 0.81   |
| ADATA     | SX8200PNP          | 256 GB | 77      | 316   | 42    | 0.81   |
| Nextorage | SSD NE1N1TB        | 1 TB   | 2       | 296   | 0     | 0.81   |
| ADATA     | SX6000NP           | 128 GB | 10      | 437   | 209   | 0.81   |
| KIOXIA    | KBG40ZNS128G BG4A  | 128 GB | 8       | 295   | 0     | 0.81   |
| Corsair   | Force MP510        | 240 GB | 68      | 295   | 0     | 0.81   |
| KIOXIA    | KXG6AZNV512G       | 512 GB | 10      | 294   | 0     | 0.81   |
| Samsung   | Portable SSD T7    | 500 GB | 24      | 293   | 0     | 0.81   |
| China     | NVME SSD           | 2 TB   | 3       | 293   | 0     | 0.80   |
| Micron    | 7300_MTFDHBE6T4TDG | 6.4 TB | 2       | 293   | 0     | 0.80   |
| WDC       | WDS100T3X0C-00SJG0 | 1 TB   | 262     | 293   | 3     | 0.80   |
| ZHITAI    | PC005 Active       | 1 TB   | 7       | 292   | 0     | 0.80   |
| SanDisk   | WD_BLACK SN850     | 500 GB | 8       | 292   | 0     | 0.80   |
| PNY       | CS1031 2TB SSD     | 2 TB   | 7       | 292   | 0     | 0.80   |
| Kingston  | SA2000M81000G      | 1 TB   | 292     | 293   | 11    | 0.80   |
| Corsair   | MP400              | 4 TB   | 8       | 291   | 0     | 0.80   |
| WDC       | WDS250G3X0C-00SJG0 | 250 GB | 43      | 291   | 0     | 0.80   |
| SPCC      | M.2 PCIE SSD       | 512 GB | 6       | 302   | 169   | 0.80   |
| Toshiba   | KBG30ZMV256G       | 256 GB | 111     | 290   | 0     | 0.80   |
| PNY       | CS3140 2TB SSD     | 2 TB   | 3       | 290   | 0     | 0.80   |
| Plextor   | PX-512M9PeGN       | 512 GB | 2       | 290   | 0     | 0.80   |
| EDILOCA   | EN600 Pro          | 1 TB   | 4       | 288   | 0     | 0.79   |
| Seagate   | BarraCuda Q5 ZP... | 1 TB   | 18      | 288   | 0     | 0.79   |
| Intel     | SSDPEMKF256G8 NVMe | 256 GB | 12      | 347   | 84    | 0.79   |
| XPG       | GAMMIX S50         | 1 TB   | 11      | 287   | 0     | 0.79   |
| SanDisk   | WD Red SN700       | 2 TB   | 4       | 286   | 0     | 0.79   |
| Toshiba   | KBG40ZNS256G ME... | 256 GB | 5       | 285   | 0     | 0.78   |
| SSSTC     | CL1-3D256-Q11 NVMe | 256 GB | 39      | 285   | 0     | 0.78   |
| HP        | SSD EX900          | 250 GB | 35      | 323   | 90    | 0.78   |
| Intel     | SSDPEKKF512G8 NVMe | 512 GB | 18      | 341   | 2     | 0.78   |
| Toshiba   | KBG40ZNS512G NVMe  | 512 GB | 20      | 285   | 0     | 0.78   |
| Transcend | TS512GMTE110S      | 512 GB | 16      | 284   | 0     | 0.78   |
| Transcend | TS128GMTE110S      | 128 GB | 30      | 282   | 0     | 0.77   |
| Seagate   | FireCuda 530 ZP... | 4 TB   | 6       | 282   | 0     | 0.77   |
| Micron    | 7300_MTFDHBG3T8TDF | 3.8 TB | 3       | 281   | 0     | 0.77   |
| Apacer    | AS2280P4           | 480 GB | 5       | 280   | 0     | 0.77   |
| UMIS      | RPIRJ512VME2OWD    | 512 GB | 2       | 280   | 0     | 0.77   |
| Lenovo    | LENSE20256GMSP3... | 256 GB | 53      | 296   | 25    | 0.77   |
| SanDisk   | WD_BLACK SN850 ... | 2 TB   | 5       | 280   | 0     | 0.77   |
| PNY       | CS3040 1TB SSD     | 1 TB   | 3       | 280   | 0     | 0.77   |
| Intel     | MEMPEK1W016GAL     | 16 GB  | 2       | 279   | 0     | 0.77   |
| Intel     | HBRPEKNX0101AHO    | 16 GB  | 40      | 291   | 5     | 0.77   |
| GLOWAY    | YCT512NVMe-M.2-... | 512 GB | 2       | 278   | 0     | 0.76   |
| Intel     | SSDPEKKW010T8      | 1 TB   | 15      | 277   | 0     | 0.76   |
| Silico... | M Series NVMe S... | 256 GB | 4       | 277   | 0     | 0.76   |
| Intel     | H10 HBRPEKNX020... | 512 GB | 48      | 277   | 0     | 0.76   |
| Apacer    | AS2280P4           | 240 GB | 4       | 276   | 0     | 0.76   |
| Intel     | H10 HBRPEKNX020... | 1 TB   | 5       | 334   | 1     | 0.76   |
| Phison    | Sabrent Rocket 4.0 | 500 GB | 38      | 275   | 0     | 0.76   |
| Colorful  | CN700 4TB PRO      | 4 TB   | 2       | 275   | 0     | 0.75   |
| PNY       | CS2140 2TB SSD     | 2 TB   | 2       | 274   | 0     | 0.75   |
| Nextorage | SSD NEM-PA1TB      | 1 TB   | 4       | 273   | 0     | 0.75   |
| SanDisk   | WD Red SN700       | 4 TB   | 18      | 273   | 0     | 0.75   |
| Samsung   | SSD 960 EVO        | 1 TB   | 87      | 294   | 14    | 0.75   |
| Phison    | Sabrent Rocket ... | 1 TB   | 48      | 273   | 0     | 0.75   |
| SK hynix  | PC611 NVMe         | 512 GB | 70      | 274   | 15    | 0.75   |
| MSI       | M390               | 250 GB | 5       | 271   | 0     | 0.75   |
| ADATA     | SX8200PNP          | 2 TB   | 94      | 285   | 33    | 0.74   |
| Micron    | 2400_MTFDKBA2T0QFM | 2 TB   | 2       | 271   | 0     | 0.74   |
| VICKTER   | NVME SSD           | 512 GB | 5       | 271   | 0     | 0.74   |
| Intel     | HBRPEKNX0101AH     | 256 GB | 41      | 271   | 0     | 0.74   |
| PNY       | CS2130 500GB SSD   | 500 GB | 7       | 271   | 0     | 0.74   |
| Phison    | E18-1TB-PHISON-... | 1 TB   | 3       | 271   | 0     | 0.74   |
| Seagate   | ZP2000GM30004      | 2 TB   | 17      | 270   | 0     | 0.74   |
| KIOXIA    | KXG7AZNV512G LA    | 512 GB | 9       | 270   | 0     | 0.74   |
| Reletech  | P400 SSD           | 512 GB | 5       | 270   | 0     | 0.74   |
| Intel     | SSDPEKKW256G8L     | 256 GB | 10      | 269   | 0     | 0.74   |
| Samsung   | MZFLV512HCJH-000MV | 512 GB | 11      | 269   | 0     | 0.74   |
| Samsung   | MZVPW256HEGL-000H1 | 256 GB | 21      | 269   | 0     | 0.74   |
| Samsung   | MZVKW512HMJP-00000 | 512 GB | 16      | 319   | 9     | 0.73   |
| Intel     | SSDPEKKW128G8      | 128 GB | 23      | 268   | 0     | 0.73   |
| Seagate   | FireCuda 530 ZP... | 2 TB   | 34      | 267   | 0     | 0.73   |
| EDILOCA   | EN705              | 2 TB   | 2       | 266   | 0     | 0.73   |
| Samsung   | SSD 960 EVO        | 500 GB | 224     | 280   | 28    | 0.73   |
| Corsair   | MP600 PRO          | 1 TB   | 11      | 266   | 0     | 0.73   |
| WDC       | WDS200T1X0E-00AFY0 | 2 TB   | 71      | 266   | 0     | 0.73   |
| Corsair   | Force MP300        | 480 GB | 4       | 265   | 0     | 0.73   |
| SK hynix  | PC400 NVMe         | 512 GB | 4       | 265   | 0     | 0.73   |
| PNY       | CS1031 500GB SSD   | 500 GB | 2       | 265   | 0     | 0.73   |
| Corsair   | MP600 PRO XT       | 1 TB   | 6       | 264   | 0     | 0.72   |
| T-FORCE   | TM8FP7002T         | 2 TB   | 9       | 263   | 0     | 0.72   |
| WDC       | WDBRPG0010BNC-WRSN | 1 TB   | 42      | 262   | 0     | 0.72   |
| SK hynix  | PC711 NVMe         | 1 TB   | 106     | 262   | 0     | 0.72   |
| Gigabyte  | GP-AG42TB          | 2 TB   | 7       | 261   | 0     | 0.72   |
| KIOXIA    | KXG6AZNV1T02 NV... | 1 TB   | 2       | 261   | 0     | 0.72   |
| Seagate   | FireCuda 520 SS... | 1 TB   | 35      | 261   | 0     | 0.72   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 15      | 261   | 0     | 0.72   |
| Toshiba   | KXG6AZNV1T02       | 1 TB   | 47      | 260   | 0     | 0.71   |
| Intel     | SSDPEKKF256G8L     | 256 GB | 178     | 263   | 6     | 0.71   |
| Transcend | TS1TMTE110S        | 1 TB   | 4       | 259   | 0     | 0.71   |
| Toshiba   | RC100              | 240 GB | 15      | 260   | 18    | 0.71   |
| Samsung   | MZFLV256HCHP-000MV | 256 GB | 23      | 259   | 0     | 0.71   |
| WDC       | WDS500G2B0C-00PXH0 | 500 GB | 291     | 258   | 0     | 0.71   |
| Phytium   | S1200CYX1-T0M22... | 256 GB | 2       | 258   | 0     | 0.71   |
| Toshiba   | KBG40ZPZ512G NVMe  | 512 GB | 5       | 257   | 0     | 0.71   |
| ADATA     | SX6000NP           | 512 GB | 7       | 326   | 17    | 0.71   |
| Crucial   | CT1000P2SSD8       | 1 TB   | 266     | 259   | 1     | 0.71   |
| SK hynix  | PC611 NVMe         | 1 TB   | 71      | 257   | 0     | 0.70   |
| UMIS      | RPITJ512PED2OWX    | 512 GB | 5       | 516   | 202   | 0.70   |
| SK hynix  | PC711 NVMe         | 256 GB | 10      | 256   | 0     | 0.70   |
| KIOXIA    | KXG60ZNV256G       | 256 GB | 51      | 254   | 0     | 0.70   |
| Samsung   | Portable SSD T7    | 1 TB   | 76      | 254   | 0     | 0.70   |

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
| Aura        | 2      | 19      | 374   | 0     | 1.03   |
| Dell        | 13     | 48      | 372   | 0     | 1.02   |
| LDLC        | 2      | 12      | 370   | 0     | 1.02   |
| tigo        | 1      | 2       | 366   | 0     | 1.00   |
| Corsair     | 51     | 760     | 362   | 1     | 0.99   |
| Toshiba     | 99     | 2175    | 330   | 4     | 0.90   |
| Intel       | 132    | 4533    | 330   | 8     | 0.86   |
| PNY         | 30     | 318     | 310   | 1     | 0.84   |
| addlink     | 2      | 52      | 306   | 0     | 0.84   |
| Asgard      | 8      | 20      | 298   | 0     | 0.82   |
| Plextor     | 17     | 67      | 312   | 44    | 0.78   |
| GLOWAY      | 1      | 2       | 278   | 0     | 0.76   |
| Mushkin     | 16     | 77      | 296   | 28    | 0.75   |
| VICKTER     | 1      | 5       | 271   | 0     | 0.74   |
| J.ZAO       | 2      | 8       | 316   | 85    | 0.74   |
| HP          | 22     | 256     | 286   | 15    | 0.74   |
| ASint       | 3      | 11      | 263   | 0     | 0.72   |
| Phytium     | 1      | 2       | 258   | 0     | 0.71   |
| Phison      | 130    | 1931    | 253   | 4     | 0.69   |
| Gigabyte    | 26     | 310     | 251   | 14    | 0.69   |
| Reletech    | 5      | 15      | 248   | 0     | 0.68   |
| Seagate     | 35     | 368     | 245   | 0     | 0.67   |
| EMTEC       | 4      | 11      | 220   | 0     | 0.61   |
| Transcend   | 19     | 179     | 224   | 12    | 0.60   |
| Kingmax     | 1      | 3       | 216   | 0     | 0.59   |
| OSCOO       | 1      | 3       | 206   | 0     | 0.57   |
| AMD         | 6      | 31      | 200   | 0     | 0.55   |
| SPCC        | 12     | 620     | 207   | 24    | 0.54   |
| Smartbuy    | 6      | 19      | 196   | 0     | 0.54   |
| Viper       | 7      | 37      | 193   | 0     | 0.53   |
| BAITITON    | 1      | 2       | 193   | 0     | 0.53   |
| SNR         | 1      | 3       | 193   | 0     | 0.53   |
| XPG         | 16     | 506     | 210   | 29    | 0.53   |
| TOPMORE     | 2      | 4       | 186   | 0     | 0.51   |
| Gigabyte... | 12     | 81      | 184   | 0     | 0.50   |
| T-FORCE     | 21     | 96      | 192   | 11    | 0.50   |
| Lenovo      | 5      | 147     | 184   | 16    | 0.48   |
| XrayDisk    | 6      | 51      | 172   | 0     | 0.47   |
| Goodram     | 22     | 154     | 172   | 1     | 0.47   |
| KINGBANK    | 2      | 19      | 169   | 0     | 0.47   |
| Hikvision   | 23     | 106     | 177   | 1     | 0.46   |
| ADATA       | 104    | 1880    | 179   | 23    | 0.46   |
| KIOXIA      | 96     | 2644    | 165   | 1     | 0.45   |
| GOFATOO     | 2      | 16      | 161   | 0     | 0.44   |
| WDC         | 176    | 7243    | 159   | 2     | 0.44   |
| SSSTC       | 37     | 455     | 157   | 7     | 0.42   |
| MasonSemi   | 1      | 2       | 151   | 0     | 0.42   |
| Kingston    | 105    | 5258    | 151   | 3     | 0.41   |
| Crucial     | 50     | 4080    | 150   | 4     | 0.40   |
| KIOXIA-E... | 9      | 220     | 146   | 1     | 0.40   |
| MSI         | 21     | 140     | 142   | 0     | 0.39   |
| Lite-On     | 27     | 188     | 160   | 28    | 0.38   |
| SMI         | 1      | 4       | 138   | 0     | 0.38   |
| Nextorage   | 7      | 26      | 136   | 0     | 0.37   |
| S3+         | 1      | 2       | 135   | 0     | 0.37   |
| Team        | 22     | 353     | 139   | 22    | 0.37   |
| EAGET       | 2      | 7       | 129   | 0     | 0.35   |
| Silicon ... | 69     | 510     | 130   | 6     | 0.35   |
| SK hynix    | 179    | 5655    | 130   | 1     | 0.35   |
| VISIPRO     | 1      | 2       | 128   | 0     | 0.35   |
| GeIL        | 1      | 2       | 127   | 0     | 0.35   |
| GenMachine  | 1      | 2       | 125   | 0     | 0.34   |
| ACCLAMATOR  | 1      | 3       | 124   | 0     | 0.34   |
| Ramsta      | 1      | 3       | 124   | 0     | 0.34   |
| UMIS        | 37     | 565     | 124   | 3     | 0.33   |
| KingFast    | 2      | 13      | 120   | 0     | 0.33   |
| Patriot     | 23     | 251     | 125   | 2     | 0.33   |
| Zheino      | 2      | 4       | 119   | 0     | 0.33   |
| aigo        | 3      | 7       | 116   | 0     | 0.32   |
| China       | 28     | 272     | 119   | 7     | 0.32   |
| Timetec     | 2      | 13      | 115   | 0     | 0.32   |
| EDILOCA     | 11     | 29      | 115   | 0     | 0.32   |
| Intenso     | 5      | 23      | 114   | 1     | 0.31   |
| ZHITAI      | 12     | 94      | 114   | 1     | 0.31   |
| ORTIAL      | 2      | 18      | 111   | 0     | 0.31   |
| Kimtigo     | 2      | 26      | 116   | 40    | 0.31   |
| Western ... | 3      | 11      | 110   | 1     | 0.30   |
| Swissbit    | 2      | 5       | 109   | 0     | 0.30   |
| WALRAM      | 5      | 25      | 108   | 0     | 0.30   |
| JAMESDONKEY | 1      | 2       | 107   | 0     | 0.29   |
| Netac       | 10     | 216     | 114   | 12    | 0.29   |
| KLEVV       | 7      | 23      | 123   | 6     | 0.29   |
| Samsung     | 372    | 24915   | 108   | 5     | 0.28   |
| KLLISRE     | 2      | 9       | 100   | 0     | 0.28   |
| LuminouTek  | 2      | 5       | 100   | 0     | 0.27   |
| Star Drive  | 1      | 22      | 98    | 0     | 0.27   |
| Kingchuxing | 3      | 7       | 91    | 0     | 0.25   |
| PCSPECIA... | 2      | 7       | 91    | 0     | 0.25   |
| Inland      | 3      | 19      | 91    | 4     | 0.25   |
| Lexar       | 39     | 631     | 91    | 1     | 0.25   |
| SOLIDIGM    | 13     | 254     | 91    | 1     | 0.25   |
| KingSpec    | 27     | 214     | 104   | 12    | 0.24   |
| HUAWEI      | 2      | 10      | 88    | 0     | 0.24   |
| Apacer      | 13     | 185     | 89    | 6     | 0.23   |
| Fanxiang    | 26     | 145     | 84    | 2     | 0.23   |
| FIKWOT      | 11     | 35      | 80    | 0     | 0.22   |
| Verbatim    | 7      | 21      | 80    | 0     | 0.22   |
| Micron      | 124    | 3697    | 79    | 2     | 0.22   |
| ShiJi       | 3      | 10      | 81    | 160   | 0.21   |
| YMTC        | 18     | 207     | 74    | 1     | 0.20   |
| Colorful    | 5      | 15      | 74    | 0     | 0.20   |
| OWC         | 2      | 6       | 73    | 0     | 0.20   |
| QUANXING    | 1      | 2       | 73    | 0     | 0.20   |
| SanDisk     | 172    | 5043    | 72    | 1     | 0.20   |
| DAPUSTOR    | 2      | 5       | 66    | 0     | 0.18   |
| PC Pet      | 1      | 2       | 64    | 0     | 0.18   |
| Predator    | 12     | 71      | 64    | 1     | 0.17   |
| MOVESPEED   | 4      | 8       | 63    | 0     | 0.17   |
| Integral    | 1      | 2       | 59    | 0     | 0.16   |
| Kllisre     | 1      | 2       | 59    | 0     | 0.16   |
| TwinMOS     | 1      | 8       | 53    | 0     | 0.15   |
| ARDOR GA... | 5      | 48      | 55    | 5     | 0.13   |
| AirDisk     | 3      | 83      | 49    | 1     | 0.13   |
| PUSKILL     | 2      | 7       | 46    | 0     | 0.13   |
| HJDK        | 2      | 8       | 46    | 0     | 0.13   |
| Teclast     | 2      | 5       | 46    | 0     | 0.13   |
| Acer        | 6      | 32      | 49    | 3     | 0.12   |
| FORESEE     | 18     | 244     | 47    | 1     | 0.12   |
| HUADISK     | 3      | 60      | 44    | 1     | 0.12   |
| INDMEM      | 1      | 2       | 174   | 3     | 0.12   |
| imation     | 2      | 4       | 43    | 0     | 0.12   |
| T-CREATE    | 4      | 8       | 43    | 0     | 0.12   |
| KUU         | 1      | 2       | 42    | 0     | 0.12   |
| Digma       | 6      | 14      | 39    | 2     | 0.11   |
| Monster ... | 1      | 2       | 39    | 0     | 0.11   |
| Dahua       | 3      | 10      | 37    | 0     | 0.10   |
| Qumox       | 1      | 2       | 36    | 0     | 0.10   |
| Apple       | 36     | 725     | 36    | 3     | 0.10   |
| UDSS        | 2      | 6       | 36    | 0     | 0.10   |
| AGI         | 5      | 25      | 34    | 0     | 0.10   |
| BIWIN       | 20     | 173     | 34    | 1     | 0.10   |
| Wodposit    | 4      | 55      | 33    | 0     | 0.09   |
| INNOVATI... | 1      | 3       | 32    | 0     | 0.09   |
| ORICO       | 8      | 41      | 35    | 2     | 0.09   |
| Bestoss     | 1      | 2       | 31    | 0     | 0.09   |
| KOOTION     | 1      | 2       | 29    | 0     | 0.08   |
| CUSU        | 2      | 5       | 71    | 6     | 0.08   |
| MiWhole     | 1      | 3       | 26    | 0     | 0.07   |
| EVM         | 2      | 5       | 24    | 0     | 0.07   |
| HighRel     | 1      | 12      | 23    | 0     | 0.06   |
| SUNEAST     | 1      | 2       | 22    | 0     | 0.06   |
| Union Me... | 7      | 67      | 21    | 0     | 0.06   |
| ExeGate     | 2      | 4       | 20    | 0     | 0.06   |
| Foxline     | 2      | 32      | 20    | 0     | 0.06   |
| Ramaxel     | 1      | 5       | 19    | 0     | 0.05   |
| SCY         | 5      | 28      | 18    | 0     | 0.05   |
| Innodisk    | 1      | 6       | 23    | 3     | 0.05   |
| BESHTAU     | 1      | 2       | 18    | 0     | 0.05   |
| CYX         | 1      | 3       | 17    | 0     | 0.05   |
| Rayson      | 4      | 26      | 15    | 0     | 0.04   |
| Solid St... | 4      | 11      | 15    | 0     | 0.04   |
| PHIXERO     | 2      | 4       | 13    | 0     | 0.04   |
| BR          | 3      | 9       | 13    | 0     | 0.04   |
| Neo Forza   | 2      | 7       | 12    | 0     | 0.03   |
| OEM         | 1      | 4       | 12    | 0     | 0.03   |
| MMY         | 2      | 10      | 9     | 0     | 0.03   |
| Electron... | 1      | 2       | 8     | 0     | 0.02   |
| Digma Top   | 1      | 2       | 7     | 0     | 0.02   |
| TWSC        | 3      | 8       | 5     | 0     | 0.02   |
| Daten       | 1      | 3       | 4     | 0     | 0.01   |
| Valuetech   | 1      | 2       | 3     | 0     | 0.01   |
| TIMETEC     | 1      | 2       | 3     | 0     | 0.01   |
| WOOKING     | 1      | 3       | 2     | 0     | 0.01   |
| HomeNet     | 2      | 7       | 2     | 0     | 0.01   |
| Gudga       | 1      | 2       | 2     | 0     | 0.01   |
| ESSENCORE   | 1      | 5       | 1     | 0     | 0.01   |
| Firebat     | 1      | 2       | 1     | 0     | 0.00   |
| ZTC         | 1      | 2       | 0     | 0     | 0.00   |
| WalkDisk    | 1      | 2       | 0     | 0     | 0.00   |
| kllisre     | 1      | 2       | 0     | 0     | 0.00   |
| ZETTASTONE  | 1      | 2       | 0     | 0     | 0.00   |
| DELL        | 1      | 2       | 0     | 0     | 0.00   |

