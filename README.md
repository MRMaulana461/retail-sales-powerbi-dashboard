# Retail Sales Dashboard (Power BI)

Dashboard interaktif 2 halaman yang memvisualisasikan data transaksi UK online retail (~540K baris, Des 2010 – Des 2011), sebagai lanjutan dari [analisis SQL](https://github.com/MRMaulana461/retail-sales-sql-analysis) sebelumnya — kali ini dengan fokus pada storytelling visual untuk stakeholder non-teknis.

## Ringkasan

Membangun dashboard Power BI 2 halaman (Overview & Customer Analysis) dari data retail yang sama dengan project SQL sebelumnya. Data dibersihkan dan ditransformasi menggunakan Power Query, metrik dihitung dengan DAX. Temuan utama: revenue sangat terkonsentrasi di satu negara (UK) dan mengikuti pola distribusi customer yang timpang (segelintir customer menyumbang porsi besar revenue) — konsisten dengan temuan Pareto di analisis SQL.

## Tools & Teknik

- **Power BI Desktop**
- **Power Query** — cleaning data (parsing tanggal dengan locale UK, filter data retur/invalid)
- **DAX** — custom measures (`SUMX`, `DISTINCTCOUNT`, `FORMAT`)
- Konsep visual: KPI card, line chart, bar chart (vertical & horizontal), Top N filtering

## Halaman 1 — Overview

![Overview](screenshots/overview.png)

**Isi:** KPI card (Total Revenue, Total Orders), tren revenue bulanan, dan top 20 produk terlaris.

**Temuan:**
- Total revenue: **£8.91M** dari **19K order unik** sepanjang periode data
- Tren revenue menunjukkan pola musiman jelas: relatif stabil di awal 2011, naik tajam mulai Agustus, memuncak di sekitar November 2011 — konsisten dengan pola belanja menjelang musim liburan
- **WORLD WAR 2 GLIDERS ASSTD DESIGNS** dan **JUMBO BAG RED RETROSPOT** konsisten menjadi produk dengan volume penjualan tertinggi, sejalan dengan temuan di analisis SQL yang juga menunjukkan produk ini sering muncul di top-seller bulanan

> **Catatan:** Penurunan tajam di titik akhir grafik (Desember 2011) bukan indikasi penurunan bisnis — dataset hanya mencakup transaksi hingga tanggal 9 Desember, sehingga bulan tersebut belum merepresentasikan satu bulan penuh.

## Halaman 2 — Customer & Geographic Analysis

![Customer Analysis](screenshots/customer-analysis.png)

**Isi:** Top 20 customer berdasarkan revenue, dan breakdown revenue per negara.

**Temuan:**
- Revenue sangat terkonsentrasi secara geografis — **United Kingdom mendominasi hampir seluruh revenue**, sementara negara lain (Netherlands, EIRE, Germany, France, dll.) hanya berkontribusi kecil. Ini mengindikasikan bisnis yang sangat bergantung pada pasar domestik UK, dengan potensi ekspansi pasar internasional yang belum tergarap.
- Distribusi revenue antar customer menunjukkan pola menurun tajam (skewed) — beberapa customer teratas (CustomerID 14646, 18102, 17450) menyumbang revenue jauh di atas rata-rata, konsisten dengan pola konsentrasi revenue yang juga ditemukan di analisis SQL.

> **Catatan data quality:** Terdapat sedikit selisih urutan dan nilai revenue top customer dibandingkan hasil query SQL sebelumnya, kemungkinan terkait format desimal pada kolom `UnitPrice` di data mentah yang belum sepenuhnya divalidasi ulang. Investigasi lebih lanjut disarankan sebelum angka ini digunakan untuk keputusan bisnis final — dicatat di sini sebagai bentuk transparansi proses analisis, bukan ditutup-tutupi.

## Insight Gabungan (SQL + Power BI)

Menggabungkan temuan dari kedua project (SQL dan Power BI) menghasilkan gambaran bisnis yang lebih utuh:
1. **Konsentrasi revenue tinggi** — baik dari sisi customer (segelintir top spender) maupun geografis (hampir seluruhnya dari UK) — menandakan risiko ketergantungan pada segmen sempit.
2. **Retention rate rendah (35%, dari analisis SQL)** dikombinasikan dengan pola musiman yang kuat menunjukkan bisnis mungkin lebih mengandalkan akuisisi customer baru tiap musim, dibanding mempertahankan customer lama.
3. **Rekomendasi:** investasi pada program retensi dan diversifikasi pasar (ekspansi di luar UK) berpotensi memberikan dampak bisnis yang signifikan.

## Cara Menggunakan

1. Download file `.pbix` di repo ini
2. Buka dengan [Power BI Desktop](https://www.microsoft.com/en-us/power-platform/products/power-bi/downloads) (gratis)
3. Data source menggunakan CSV lokal — jika ingin reproduce, download dataset dari [UCI Online Retail](https://archive.ics.uci.edu/dataset/352/online-retail) dan sesuaikan path data source di Power Query

## Project Terkait

- [Retail Sales Analysis with SQL](../retail-sql-project) — analisis mendalam menggunakan SQL (CTE, window functions) yang menjadi dasar project ini
