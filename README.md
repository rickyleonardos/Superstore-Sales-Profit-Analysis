# Superstore Sales & Profit Analysis

*Laporan analisis dashboard Excel · Data transaksi Januari 2014 sampai Desember 2017 · Nilai dalam USD*

**Ringkasan.** Selama 2014 sampai 2017, Superstore mencatat penjualan 2.297.201 dan profit 286.397 (margin 12,5%). Bisnis tumbuh, tetapi profit bocor lewat diskon besar: transaksi berdiskon di atas 20% merugi secara neto sebesar 135.376. Selain itu, kategori Furniture bermargin sangat tipis (2,5%) dan Region Central paling lemah (7,9%). Dokumen ini merangkum masalah, analisis, insight, rekomendasi, dan tools yang dipakai.

## 1. Masalah

### Latar belakang

Superstore menjual produk Furniture, Office Supplies, dan Technology kepada tiga segmen pelanggan (Consumer, Corporate, Home Office) di empat region (Central, East, South, West). Dataset berisi 9.994 baris transaksi, 5.009 order unik, dan 793 customer, tanpa data kosong dan tanpa duplikat.

Penjualan yang besar belum tentu berarti untung. Manajemen perlu tahu di mana bisnis menghasilkan profit, di mana bisnis merugi, dan apa penyebabnya.

### Pertanyaan bisnis

1. Seberapa besar penjualan dan profit, dan bagaimana polanya per bulan dan per kuartal?
2. Bagaimana diskon memengaruhi profit?
3. Produk dan customer mana yang paling berkontribusi?
4. Kategori, sub-kategori, region, dan segmen mana yang margin-nya lemah?

### Tujuan

Membangun dashboard Excel interaktif yang menjawab pertanyaan di atas, lalu menurunkan insight dan rekomendasi yang bisa ditindaklanjuti.

## 2. Analisis

### Metode

1. **Pembersihan data (Power Query):** import CSV dengan encoding Windows-1252, ubah tipe data (tanggal dengan locale English US), rapikan teks, lalu tambah kolom Year, Year Month, Year Quarter, Discount Band, dan Band Order.
2. **Pemodelan (Data Model dan DAX):** empat measure, yaitu Total Sales, Total Profit, Profit Margin %, dan Avg Discount.
3. **Eksplorasi (PivotTable):** delapan pivot untuk KPI, tren bulanan, tren kuartalan, diskon, top produk, top customer, kategori, dan sub-kategori.
4. **Visualisasi:** dashboard dengan 4 KPI card, 6 chart, dan 4 slicer (Year, Region, Category, Segment).

Bagian 2.1 sampai 2.8 mengikuti urutan panel dashboard, dari kiri atas ke kanan bawah. Semua nilai dan persentase dihitung langsung dari dataset (9.994 baris) dan sama dengan yang tampil di dashboard saat tidak ada slicer yang aktif.

### 2.1 KPI (empat kartu di bagian atas)

Dashboard membuka dengan penjualan 2.297.201 dan profit 286.397, sehingga margin keseluruhan 12,5% dengan rata-rata diskon 15,6%.

| KPI | Nilai | Cara dihitung |
| --- | --- | --- |
| Total Sales | 2.297.201 | Jumlah kolom Sales |
| Total Profit | 286.397 | Jumlah kolom Profit |
| Margin | 12,5% | Total Profit dibagi Total Sales |
| Avg Discount | 15,6% | Rata-rata kolom Discount di seluruh baris |

Angka ini berasal dari 5.009 order unik dan 793 customer.

### 2.2 Penjualan & profit per bulan

Garis penjualan naik turun tajam dan cenderung naik menuju akhir tahun, sedangkan garis profit tipis dan relatif datar. Rata-rata per bulan (48 bulan), penjualan 47.858 dan profit 5.967.

| Ukuran | Bulan | Penjualan | Profit |
| --- | --- | --- | --- |
| Penjualan tertinggi | November 2017 | 118.448 | 9.690 (margin 8,2%) |
| Penjualan terendah | Februari 2014 | 4.520 | 862 |
| Profit tertinggi | Desember 2016 | 96.999 | 17.885 |
| Profit negatif | Juli 2014 | 33.946 | -841 |
| Profit negatif | Januari 2015 | 18.174 | -3.281 |

Puncak penjualan tiap tahun selalu jatuh pada September sampai Desember: September 2014 (81.777), November 2015 (75.973), Desember 2016 (96.999), dan November 2017 (118.448). Jika semua tahun digabung per nama bulan, November (352.461), Desember (325.294), dan September (307.650) tertinggi, sedangkan Februari terendah (59.751).

### 2.3 Diskon di atas 20% membuat rugi

Profit turun seiring naiknya diskon dan berubah rugi di atas 20%, seperti yang terlihat pada chart.

| Band diskon | Jumlah baris | Penjualan | Profit | Margin |
| --- | --- | --- | --- | --- |
| 0% | 4.798 | 1.087.908 | 320.988 | 29,5% |
| 1-20% | 3.803 | 846.522 | 100.785 | 11,9% |
| 21-40% | 460 | 234.138 | -35.817 | -15,3% |
| >40% | 933 | 128.632 | -99.559 | -77,4% |

Band diskon di atas 20% hanya mencakup sekitar 14% baris transaksi, tetapi seluruh baris pada band >40% merugi (933 dari 933) dan 90% baris pada band 21-40% merugi (415 dari 460). Secara keseluruhan ada 1.871 baris transaksi merugi (18,7%) dengan total kerugian 156.131.

### 2.4 Penjualan & profit per kuartal

Penjualan memuncak di kuartal 4 setiap tahun, dan Q4 menyumbang sekitar 38% dari total penjualan. Sebaliknya Q1 paling rendah, hanya 15,7% dari total.

| Tahun | Penjualan Q4 | Profit Q4 | Margin Q4 |
| --- | --- | --- | --- |
| 2014 | 179.628 | 21.724 | 12,1% |
| 2015 | 182.297 | 23.309 | 12,8% |
| 2016 | 236.099 | 38.140 | 16,2% |
| 2017 | 280.054 | 27.449 | 9,8% |

Kuartal dengan penjualan terendah adalah Q1 2015 (68.852) dan tertinggi Q4 2017 (280.054). Margin kuartalan berkisar dari 5,1% (Q1 2014) sampai 19,1% (Q1 2017), dan Q4 2017 hanya 9,8% meski penjualannya tertinggi.

### 2.5 Profit per kategori

Technology dan Office Supplies menghasilkan sekitar 94% profit, sedangkan Furniture hanya 6% meski porsi penjualannya 32%.

| Kategori | Penjualan | Profit | Margin | Porsi penjualan | Porsi profit |
| --- | --- | --- | --- | --- | --- |
| Technology | 836.154 | 145.455 | 17,4% | 36,4% | 50,8% |
| Office Supplies | 719.047 | 122.491 | 17,0% | 31,3% | 42,8% |
| Furniture | 741.999 | 18.451 | 2,5% | 32,3% | 6,4% |

Di balik margin Furniture, sub-kategori Tables (-17.725; margin -8,6%) dan Bookcases (-3.473; margin -3,0%) merugi, begitu pula Supplies (-1.189). Machines nyaris impas dengan margin 1,8%. Sub-kategori tidak tampil di dashboard dan dihitung dari dataset (pivot P7).

### 2.6 Top 10 produk berdasarkan profit

Sepuluh produk teratas menyumbang 66.479 atau 23,2% dari total profit, padahal jumlahnya kurang dari 1% dari 1.850 produk.

| # | Produk | Profit | Margin |
| --- | --- | --- | --- |
| 1 | Canon imageCLASS 2200 Advanced Copier | 25.200 | 40,9% |
| 2 | Fellowes PB500 Electric Punch Plastic Comb Binding Machine | 7.753 | 28,2% |
| 3 | Hewlett Packard LaserJet 3310 Copier | 6.984 | 37,1% |
| 4 | Canon PC1060 Personal Laser Copier | 4.571 | 39,3% |
| 5 | HP Designjet T520 Inkjet Large Format Printer | 4.095 | 22,3% |
| 6 | Ativa V4110MDD Micro-Cut Shredder | 3.773 | 49,0% |
| 7 | 3D Systems Cube Printer, 2nd Generation, Magenta | 3.718 | 26,0% |
| 8 | Plantronics Savi W720 Multi-Device Wireless Headset System | 3.696 | 39,5% |
| 9 | Ibico EPK-21 Electric Binding System | 3.345 | 21,1% |
| 10 | Zebra ZM400 Thermal Label Printer | 3.344 | 48,0% |

Canon imageCLASS 2200 sendirian menyumbang 8,8% dari seluruh profit, jauh di atas peringkat kedua. Semua produk di daftar ini berupa mesin atau perangkat kantor dengan margin 21% sampai 49%. Produk paling merugi, yang tidak tampil di dashboard, adalah Cubify CubeX 3D Printer Double Head Print (-8.880) dan Lexmark MX611dhe Monochrome Laser Printer (-4.590).

### 2.7 Top 10 customer berdasarkan penjualan

Sepuluh customer teratas hanya menyumbang 6,7% dari penjualan, dan satu di antaranya, Sean Miller, justru merugi.

| # | Customer | Penjualan | Profit | Margin |
| --- | --- | --- | --- | --- |
| 1 | Sean Miller | 25.043 | -1.981 | -7,9% |
| 2 | Tamara Chand | 19.052 | 8.981 | 47,1% |
| 3 | Raymond Buch | 15.117 | 6.976 | 46,1% |
| 4 | Tom Ashbrook | 14.596 | 4.704 | 32,2% |
| 5 | Adrian Barton | 14.474 | 5.445 | 37,6% |
| 6 | Ken Lonsdale | 14.175 | 807 | 5,7% |
| 7 | Sanjit Chand | 14.142 | 5.757 | 40,7% |
| 8 | Hunter Lopez | 12.873 | 5.622 | 43,7% |
| 9 | Sanjit Engle | 12.209 | 2.651 | 21,7% |
| 10 | Christopher Conant | 12.129 | 2.177 | 17,9% |

Total penjualan sepuluh customer ini 153.811 dengan profit 41.140 (margin 26,7%). Chart diurutkan berdasarkan penjualan, sehingga customer teratas belum tentu paling menguntungkan: Sean Miller memimpin penjualan tetapi rugi, dan Tamara Chand paling menguntungkan di daftar ini.

### 2.8 Slicer: Year, Region, dan Segment

Slicer tidak punya chart sendiri, tetapi mengubah semua KPI dan chart. Nilai di bawah dihitung dari dataset, dan dapat dicek dengan memilih slicer lalu membaca KPI Total Sales dan Margin.

Slicer Year:

| Tahun | Penjualan | Profit | Margin | Pertumbuhan penjualan |
| --- | --- | --- | --- | --- |
| 2014 | 484.247 | 49.544 | 10,2% | - |
| 2015 | 470.533 | 61.619 | 13,1% | -2,8% |
| 2016 | 609.206 | 81.795 | 13,4% | +29,5% |
| 2017 | 733.215 | 93.439 | 12,7% | +20,4% |

Penjualan naik sekitar 51% dari 2014 ke 2017, sedangkan profit naik sekitar 89%. Margin membaik dari 10,2% menjadi 13,4% pada 2016, tetapi turun menjadi 12,7% pada 2017 meski penjualan tertinggi.

Slicer Region:

| Region | Penjualan | Profit | Margin |
| --- | --- | --- | --- |
| West | 725.458 | 108.418 | 14,9% |
| East | 678.781 | 91.523 | 13,5% |
| South | 391.722 | 46.749 | 11,9% |
| Central | 501.240 | 39.706 | 7,9% |

Slicer Segment:

| Segmen | Penjualan | Profit | Margin |
| --- | --- | --- | --- |
| Consumer | 1.161.401 | 134.119 | 11,5% |
| Corporate | 706.146 | 91.979 | 13,0% |
| Home Office | 429.653 | 60.299 | 14,0% |

## 3. Insight

1. **Bisnis tumbuh, dan profit tumbuh lebih cepat dari penjualan** (KPI dan slicer Year). Dari 2014 ke 2017 penjualan naik 51% dan profit naik 89%. Namun margin 2017 (12,7%) turun dibanding 2016 (13,4%).
2. **Diskon di atas 20% adalah sumber kerugian utama** (chart Diskon di atas 20% membuat rugi). Band 21-40% rugi 35.817 dan band >40% rugi 99.559, total 135.376. Semua transaksi dengan diskon di atas 40% merugi. Sebagai ilustrasi, jika transaksi tersebut hanya impas (profit nol), total profit akan menjadi sekitar 421.773, naik sekitar 47%.
3. **Penjualan sangat musiman, tetapi profit tidak mengikuti** (chart bulanan dan kuartalan). Q4 menyumbang sekitar 38% dari total penjualan. Namun bulan puncak, November 2017 (118.448), hanya menghasilkan profit 9.690 (margin 8,2%), dan margin Q4 2017 (9,8%) jauh di bawah Q4 2016 (16,2%). Ini dugaan awal adanya diskon musiman yang terlalu agresif dan perlu divalidasi lebih lanjut.
4. **Profit terkonsentrasi di Technology dan perangkat kantor** (chart Profit per kategori dan Top 10 produk). Technology menyumbang sekitar 51% profit. Satu produk saja, Canon imageCLASS 2200, menyumbang sekitar 9% dari seluruh profit.
5. **Furniture besar di penjualan tetapi tipis di profit** (chart Profit per kategori). Kategori ini menyumbang 32% penjualan tetapi hanya 6% profit (margin 2,5%), dengan Tables dan Bookcases sebagai sub-kategori yang merugi.
6. **Region Central paling lemah** (slicer Region). Margin Central hanya 7,9%, hampir setengah dari West (14,9%). Penyebabnya belum bisa dipastikan dari data ini dan perlu diselidiki, misalnya dari sisi diskon dan komposisi produk.
7. **Basis customer tersebar** (chart Top 10 customer). Sepuluh customer teratas hanya 6,7% dari penjualan, sehingga risiko ketergantungan pada satu atau dua customer rendah.
8. **Penjualan besar belum tentu untung** (chart Top 10 customer). Sean Miller, customer dengan penjualan terbesar (25.043), justru rugi 1.981, dan Ken Lonsdale hanya bermargin 5,7%. Sebaliknya Tamara Chand menghasilkan profit 8.981 dari penjualan 19.052.

## 4. Rekomendasi

| Prioritas | Rekomendasi | Dasar | Dampak yang diharapkan |
| --- | --- | --- | --- |
| Tinggi | Batasi diskon maksimal 20% dan wajibkan persetujuan manajer untuk diskon di atas itu | Insight 2 | Menghentikan kerugian sekitar 135 ribu; potensi profit naik hingga sekitar 47% (ilustrasi) |
| Tinggi | Tinjau harga dan diskon Tables, Bookcases, dan Supplies; evaluasi produk rugi seperti Cubify CubeX 3D Printer dan Lexmark MX611dhe | Insight 5 | Mengurangi kerugian sub-kategori dan memperbaiki margin Furniture |
| Menengah | Rencanakan stok dan promosi Q4 dengan batas diskon yang jelas, dengan target margin Q4 mendekati level 2016 (sekitar 16%) | Insight 3 | Menjaga profit pada kuartal yang menyumbang 38% penjualan |
| Menengah | Arahkan promosi ke sub-kategori bermargin tinggi: Copiers (37,2%), Paper (43,4%), dan Accessories (25,1%) | Insight 4 | Pertumbuhan profit tanpa menambah ketergantungan pada diskon |
| Menengah | Audit Region Central: praktik diskon, komposisi produk, dan biaya terkait | Insight 6 | Mengangkat margin Central dari 7,9% menuju rata-rata perusahaan |
| Menengah | Evaluasi profitabilitas customer besar, mulai dari Sean Miller dan Ken Lonsdale, sebelum memberi diskon atau syarat khusus | Insight 8 | Memastikan customer dengan penjualan terbesar tidak menggerus profit |
| Rendah | Pertahankan customer teratas lewat program loyalitas tanpa diskon besar | Insight 7 | Retensi customer bernilai tinggi dengan margin terjaga |
| Rendah | Pantau secara rutin di dashboard: margin, rata-rata diskon, dan jumlah transaksi diskon di atas 20% | Semua | Deteksi dini kebocoran profit |

## 5. Tools

| Tool | Fungsi dalam project |
| --- | --- |
| Microsoft Excel 2019 | Platform utama untuk pivot, chart, dan dashboard |
| Power Query | Import CSV, ubah tipe data, pembersihan, dan pembuatan kolom Year, Year Month, Year Quarter, Discount Band, Band Order |
| Power Pivot (Data Model) | Menyimpan data di model sebagai dasar PivotTable dan measure |
| DAX | Menghitung measure KPI dan margin |
| PivotTable dan PivotChart | Delapan pivot (P0 sampai P7) dan enam chart di dashboard |
| Slicer | Filter interaktif Year, Region, Category, dan Segment |
| Dataset | Sample Superstore (Kaggle), 9.994 baris, 21 kolom |

### Measure DAX yang digunakan

```
Total Sales = SUM(Orders[Sales])
Total Profit = SUM(Orders[Profit])
Profit Margin % = DIVIDE([Total Profit], [Total Sales])
Avg Discount = AVERAGE(Orders[Discount])
```

### Kolom bantu di Power Query

```
Discount Band:
if [Discount] = 0 then '0%'
else if [Discount] <= 0.2 then '1-20%'
else if [Discount] <= 0.4 then '21-40%'
else '>40%'
```

### Keterampilan yang ditunjukkan

Pembersihan data, pemodelan data, DAX, analisis eksploratif, visualisasi dashboard, dan penyampaian insight bisnis.

## Catatan dan keterbatasan

- Nilai dan persentase di dokumen ini dihitung dari dataset untuk seluruh periode, region, kategori, dan segmen. Angkanya sama dengan KPI dashboard saat tidak ada slicer yang aktif; saat slicer dipakai, angka dashboard berubah sesuai filter, sedangkan isi dokumen tetap.
- Sub-kategori (Tables, Bookcases, Supplies, Machines) tidak punya chart di dashboard. Nilainya dihitung dari dataset dan dapat dicek di pivot P7.
- Dataset tidak memuat biaya operasional, ongkos kirim, atau biaya lain, sehingga profit mengikuti nilai pada data.
- Hubungan antara diskon dan kerugian bersifat korelasi. Penyebab pasti, terutama untuk penurunan margin Q4 2017 dan lemahnya Region Central, perlu diuji dengan analisis lanjutan.
- Data bersifat historis (2014 sampai 2017). Ilustrasi kenaikan profit sebesar 47% adalah skenario sederhana, bukan prediksi.
