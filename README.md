# Analisis Kesesuaian Lokasi Fitness Center Berdasarkan Aksesibilitas dan Kepadatan Penduduk Usia Produktif
**Studi Kasus:** Kota Yogyakarta, Daerah Istimewa Yogyakarta  

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Clis3n/23-517152-SV-22742_Clisen-Ardy-Laksono-Wicaksono_GitHub/blob/main/23-517152-SV-22742_Clisen-Ardy-Laksono-Wicaksono_Kode.ipynb)

*(Klik tombol di atas untuk mereproduksi seluruh alur analisis secara instan di cloud)*

---

## 📌 Deskripsi Proyek
Repositori ini merupakan sistem pendukung keputusan geospasial berbasis **Multi-Criteria Decision Analysis (MCDA)** yang dirancang untuk menentukan lokasi paling optimal bagi pendirian fasilitas *fitness center* premium di kawasan perkotaan padat. Proyek ini disusun sebagai pemenuhan Tugas Akhir Praktikum Aplikasi SIG untuk Sosial, Ekonomi, dan Bisnis (SVIG223647) di Program Studi Sistem Informasi Geografis, Universitas Gadjah Mada (UGM).

Sistem ini didesain secara arsitektural untuk memenuhi prinsip **Fully Reproducible Research**. Seluruh parameter evaluasi ruang ditarik secara dinamis dari infrastruktur *Open Source*, memitigasi kebutuhan akan penyimpanan *shapefile* statis secara lokal.

## ⚙️ Metodologi Analitik
Analisis dieksekusi dengan mentransformasikan area Kota Yogyakarta menjadi matriks spasial beresolusi tinggi (Grid $100 \times 100$ meter) pada proyeksi metrik **UTM Zone 49S (EPSG:32749)**. 

Algoritma mengadopsi model **Analytic Hierarchy Process (AHP)** (Saaty, 1980) untuk mendekonstruksi prioritas kriteria melalui proses evaluasi matriks berbasis *Numpy Eigenvector*, diikuti operasi *Weighted Overlay*.

**Parameter Evaluasi Spasial:**
1. **Aksesibilitas Jaringan Jalan:** Jarak Euclidean terpendek menuju hierarki jalan arteri/kolektor. *(Data: OpenStreetMap / OSMnx)*
2. **Kawasan Pendidikan (Pasar Potensial):** Sentroid kedekatan terhadap universitas/kampus sebagai proksi penarik pasar usia produktif. *(Data: OpenStreetMap / OSMnx)*
3. **Kepadatan Demografi:** Kepadatan populasi aktual per kilometer persegi di tingkat kecamatan yang diinterpolasi ke dalam sel grid. *(Data Tabular: BPS Kota Yogyakarta, Proyeksi 2026)*
4. **Kejenuhan Kompetitor:** Jarak dari *fitness center* komersial eksisting. Semakin jauh, semakin tinggi nilai kesesuaiannya (*Cost Parameter*). *(Data Vektor: Scraping Google Maps)*

## 🚀 Fitur Utama (*Highlight*)
*   **Zero-Dependency Local Data:** Kecuali repositori kompetitor (*Google Maps*), tidak ada file vektor `.shp` yang diperlukan. Kode menarik data infrastruktur perkotaan secara *live* melalui *Overpass API*.
*   **One-Click Cloud Execution:** Kompatibel 100% dengan lingkungan isolasi Google Colab, lengkap dengan penanganan limitasi dependensi spasial (otomasi `pip install`).
*   **Publication-Ready Cartography:** Modul memproduksi *Dashboard Layout* Peta skala penuh secara terprogram (*programmatic layouting* via `matplotlib.gridspec`), mencakup algoritma *Label-Repel* (`adjustText`), Skala, Arah Utara Poligonal, Inset Peta Kontekstual, dan Distribusi *Bar Chart*, diekspor otomatis pada resolusi 300 dpi.

## 🛠️ Instalasi dan Penggunaan Lokal
Jika Anda bermaksud mengeksekusi proyek ini di lingkungan komputer lokal (VS Code / Jupyter Notebook konvensional), pastikan *virtual environment* Anda telah terinstal pustaka yang sesuai:

```bash
pip install -r requirements.txt
