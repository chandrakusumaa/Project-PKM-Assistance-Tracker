# Product Requirements Document (PRD)
**Nama Proyek:** WakeMeThere (Nama Sementara - Aplikasi Alarm Berbasis Lokasi)
**Platform:** iOS & Android (Cross-platform)
**Versi Dokumen:** 1.0
**Tanggal:** September 2026

---

## 1. Ringkasan Eksekutif (Executive Summary)
Aplikasi ini adalah asisten perjalanan berbasis *Geofencing* yang dirancang untuk mencegah pengguna terlewat dari tempat tujuan saat menggunakan kendaraan umum (KRL, MRT, TransJakarta, Angkot, Bus Antar Kota). Aplikasi akan melacak lokasi pengguna secara *real-time* (termasuk di latar belakang) dan akan memicu alarm bersuara keras serta getaran saat pengguna memasuki radius jarak tertentu dari titik tujuan.

## 2. Tujuan & Sasaran (Goals & Objectives)
*   **Masalah:** Pengguna kendaraan umum sering tertidur, asyik bermain *gadget*, atau membaca buku, sehingga terlewat stasiun/halte tujuan.
*   **Solusi:** Menyediakan alarm yang tidak bergantung pada waktu (jam), melainkan pada jarak fisik pengguna dengan titik tujuan.
*   **Tujuan Bisnis:** Merilis MVP (Minimum Viable Product) yang fungsional dan stabil di App Store dan Google Play Store.

## 3. Target Pengguna (Target Audience)
*   Komuter harian (Pekerja & Mahasiswa/Pelajar).
*   Pelancong/Turis yang menggunakan transportasi umum di kota baru.
*   Pengguna bus malam / kereta jarak jauh.

## 4. Spesifikasi Teknis (Tech Stack)
*   **Framework Aplikasi:** Flutter (Dart) untuk iOS dan Android.
*   **State Management:** Riverpod atau Provider.
*   **Layanan Peta (Map Service):** Google Maps Platform (`google_maps_flutter`).
*   **Pelacakan Lokasi (Location Engine):** `geolocator` dan integrasi *Background Service* (`flutter_background_service`).
*   **Sistem Alarm:** `alarm` package atau `flutter_ringtone_player` (untuk bypass mode *silent* jika diizinkan OS, dan getaran maksimal).
*   **Database Lokal:** Hive atau Isar (untuk menyimpan riwayat rute).

## 5. Fitur Utama (MVP Features)
1.  **Peta & Pencarian Lokasi (Map & Search):**
    *   Tampilan peta interaktif dengan titik lokasi pengguna saat ini (My Location).
    *   Kolom pencarian untuk mencari stasiun, halte, atau alamat tujuan.
2.  **Penentuan Radius (Dynamic Geofence):**
    *   Sistem *Quick Select* untuk radius: 500m, 1km, 2km.
    *   Opsi *Custom Input* (Slider atau ketik manual) untuk menentukan jarak spesifik.
3.  **Pelacakan Latar Belakang (Background Tracking):**
    *   Aplikasi tetap melacak pergerakan GPS secara efisien meskipun layar mati.
4.  **Sistem Peringatan (Intrusive Alarm):**
    *   Membunyikan nada dering yang persisten dan getaran (Vibration) yang baru akan mati jika pengguna menekan tombol "Matikan Alarm".
5.  **Rute Tersimpan (Saved Routes - Optional tapi direkomendasikan):**
    *   Menyimpan titik tujuan yang sering digunakan (Misal: "Kampus", "Kantor", "Rumah") agar tidak perlu mencari dari awal setiap hari.

## 6. Alur Pengguna (User Flow)
1.  **Onboarding:** Buka aplikasi -> Izinkan akses lokasi "Allow All The Time" & Notifikasi -> Tampil layar utama (Peta).
2.  **Set Tujuan:** Pengguna mengetik nama tujuan di *Search Bar* -> Pin peta jatuh di lokasi tujuan.
3.  **Set Radius:** Pengguna memilih radius peringatan (misal: 1 km sebelum sampai).
4.  **Mulai Perjalanan:** Pengguna menekan tombol "Mulai Perjalanan". Status aplikasi berubah menjadi "Melacak...". Pengguna bisa mematikan layar HP dan memasukkannya ke saku.
5.  **Trigger Geofence:** Saat jarak GPS HP < 1 km dari Pin Tujuan, aplikasi mengirimkan sinyal trigger.
6.  **Alarm Berbunyi:** Layar HP menyala menampilkan tombol raksasa, alarm berbunyi keras, HP bergetar.
7.  **Selesai:** Pengguna bangun -> Tekan "Matikan" -> Perjalanan selesai.

## 7. Rencana Anggaran Biaya (RAB) - Estimasi Kasar
*Catatan: Anggaran ini adalah estimasi standar di Indonesia untuk pengerjaan oleh tim Freelancer profesional atau In-house skala kecil selama 1,5 - 2 bulan pengembangan.*

### A. Biaya Pengembangan (Development Cost)
| Pos Pengeluaran | Deskripsi | Estimasi Biaya (IDR) |
| :--- | :--- | :--- |
| **UI/UX Designer** | Riset, Wireframe, Prototype Figma (1 bulan) | Rp 5.000.000 - Rp 8.000.000 |
| **Flutter Developer** | Koding Aplikasi iOS & Android + Integrasi API (1,5 bulan) | Rp 15.000.000 - Rp 25.000.000 |
| **QA / Tester** | Uji coba di berbagai device & skenario lapangan (2 minggu) | Rp 2.000.000 - Rp 4.000.000 |
| **Sub-Total A** | | **Rp 22.000.000 - Rp 37.000.000** |

### B. Biaya Operasional & Infrastruktur (Tahun Pertama)
| Pos Pengeluaran | Deskripsi | Estimasi Biaya (IDR) |
| :--- | :--- | :--- |
| **Google Play Developer** | Lisensi sekali bayar (Seumur hidup) - $25 | Rp 400.000 |
| **Apple Developer Program** | Lisensi tahunan untuk rilis di App Store - $99 | Rp 1.600.000 |
| **Google Maps Platform** | Biaya API (Gratis kuota $200/bulan, sangat cukup untuk rilis awal) | Rp 0 (Free Tier) |
| **Database Server (BaaS)** | Firebase (Jika ke depannya butuh login, saat ini pakai Lokal DB) | Rp 0 (Free Tier) |
| **Sub-Total B** | | **Rp 2.000.000** |

### C. Biaya Lain-lain (Marketing & Legal - Opsional)
| Pos Pengeluaran | Deskripsi | Estimasi Biaya (IDR) |
| :--- | :--- | :--- |
| **Marketing Awal** | Iklan Social Media (TikTok/IG) saat rilis | Rp 3.000.000 |
| **Biaya Tak Terduga** | *Buffer* 10% dari total anggaran | Rp 2.500.000 |
| **Sub-Total C** | | **Rp 5.500.000** |

**TOTAL ESTIMASI KESELURUHAN (A + B + C): Rp 29.500.000 - Rp 44.500.000**

## 8. Timeline Pengembangan (Estimasi: 8 Minggu)
*   **Minggu 1-2:** Riset Pengguna, Pembuatan UI/UX Design (Figma).
*   **Minggu 3-4:** Setup Proyek Flutter, Integrasi Google Maps API, & Fitur Pencarian.
*   **Minggu 5-6:** Logic Geofencing, Background Location Service, & Sistem Alarm.
*   **Minggu 7:** Internal Testing (QA) & Field Test (Bawa HP naik KRL/TransJakarta untuk tes akurasi GPS).
*   **Minggu 8:** *Bug fixing*, Persiapan Aset (Icon, Screenshot), dan Submit ke App Store & Play Store.

## 9. Risiko dan Mitigasi
1.  **Risiko:** OS membunuh aplikasi di latar belakang (terutama pabrikan Android China seperti Xiaomi/Oppo dan iOS).
    *   *Mitigasi:* Menggunakan *foreground service* dengan notifikasi persisten agar OS menganggap aplikasi sedang aktif digunakan, serta memberi panduan ke pengguna cara mematikan "Battery Optimization" untuk aplikasi ini.
2.  **Risiko:** Akurasi GPS buruk di bawah tanah (seperti stasiun MRT *underground*).
    *   *Mitigasi:* Menambahkan *disclaimer* (peringatan) di dalam aplikasi bahwa akurasi di bawah tanah mungkin terganggu, dan menyarankan pengaturan radius yang lebih lebar.
