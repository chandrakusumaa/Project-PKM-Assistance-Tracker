# PRODUCT REQUIREMENTS DOCUMENT (PRD)
## WakeMeThere: Aplikasi Alarm Perjalanan Berbasis Lokasi (Geofencing)

| | |
|---|---|
| **Dokumen** | Product Requirements Document — Versi 2.2 (Detailed Development Cost & Lean Operations) |
| **Nama Proyek** | WakeMeThere |
| **Platform** | Android (Fokus MVP awal) via Flutter |
| **Tahap** | Perancangan, Pengembangan MVP, dan Rilis Publik |
| **Target Utama** | Mencegah pengguna kendaraan umum terlewat tujuan melalui pelacakan lokasi dan notifikasi jarak. |

---

## 1. Executive Summary

WakeMeThere adalah aplikasi asisten perjalanan cerdas berbasis *Geofencing* yang dirancang khusus untuk komuter dan pelancong. Berbeda dengan alarm konvensional yang mengandalkan waktu, WakeMeThere menggunakan lokasi pengguna secara *real-time* untuk memicu peringatan (alarm dan getaran) ketika pengguna memasuki radius jarak tertentu dari titik tujuan.

Produk ini dirancang dengan arsitektur *mobile-first* menggunakan framework Flutter untuk efisiensi maksimal. Rilis MVP difokuskan pada platform Android (Google Play Store) agar sesuai dengan batas anggaran ketat di bawah Rp 7.500.000, dengan porsi terbesar dialokasikan secara transparan dan detail pada pos biaya pengembangan perangkat lunak.

---

## 2. Latar Belakang dan Problem Statement

Penggunaan transportasi umum sering kali menjadi waktu bagi komuter untuk beristirahat, membaca, atau menggunakan gawai. Sayangnya, tidak ada jaminan waktu tempuh yang pasti akibat kemacetan atau gangguan teknis operasional transit.

**Problem yang ingin diselesaikan:**
- Pengguna sering tertidur dan melewati stasiun/halte tujuan mereka, menyebabkan kerugian waktu dan biaya.
- Alarm berbasis jam (waktu) tidak efektif karena waktu tempuh transportasi umum sering berubah-ubah.
- Notifikasi aplikasi navigasi biasa (seperti Google Maps) terlalu pelan dan tidak dirancang untuk membangunkan orang tidur.
- Kebutuhan akan *tracker* yang tetap berjalan di latar belakang (background) ketika layar ponsel dimatikan.

---

## 3. Product Vision

Menjadi asisten perjalanan berbasis lokasi paling andal yang memastikan setiap komuter tiba di tujuannya tanpa rasa cemas akan terlewat, memberikan ketenangan pikiran selama perjalanan.

---

## 4. Product Objectives

| ID | Objective |
|---|---|
| OBJ-01 | Mengembangkan sistem *geofencing* presisi yang mampu mendeteksi radius jarak pengguna terhadap tujuan akhir. |
| OBJ-02 | Membangun *background service* yang tangguh agar pelacakan tetap berjalan meski layar terkunci. |
| OBJ-03 | Menyediakan sistem alarm persisten (intrusive) yang memotong mode hening (jika diizinkan) dan memaksimalkan getaran untuk membangunkan pengguna. |
| OBJ-04 | Menyediakan antarmuka peta interaktif yang responsif dan mudah digunakan oleh pengguna awam. |
| OBJ-05 | Meluncurkan MVP fungsional di platform Android dalam batasan anggaran ketat (< Rp 7.500.000) dengan rincian biaya dev yang transparan. |

---

## 5. Target User dan Persona

| User Persona | Karakteristik / Kebutuhan | Pain Point | Solusi Produk |
|---|---|---|---|
| **Pekerja Komuter** | Setiap hari menggunakan KRL/MRT. Lelah setelah bekerja dan butuh tidur di kereta. | Sering kelewatan stasiun transit. Alarm jam tidak cocok karena kereta kadang delay. | Alarm berbasis sisa jarak (misal 1 km sebelum stasiun transit). |
| **Turis / Pelancong** | Menggunakan rute bus malam atau bus antar-kota di daerah yang belum dikenal. | Tidak tahu bentang alam sekitar dan takut terlewat di malam hari. | Peta interaktif dan alarm yang berbunyi jauh sebelum sampai. |
| **Mahasiswa** | Mobilitas tinggi dengan angkot atau TransJakarta sambil mengerjakan tugas di HP. | Terlalu asyik *screen-time* sehingga tidak memperhatikan pengumuman halte. | Peringatan *pop-up* layar penuh dan getaran kuat. |

---

## 6. Product Scope

| Area | Termasuk dalam Prototype / MVP | Batasan (Out of Scope) |
|---|---|---|
| **Location Tracking** | Akses GPS/GNSS presisi tinggi, background tracking, perbandingan radius. | Pelacakan rute orang lain / Live tracking sharing (fitur sosial). |
| **Alarm System** | Nada dering persisten, getaran maksimal. | Integrasi dengan Smartwatch/Wearable device secara native. |
| **Mapping** | Integrasi Google Maps, Search Place API, My Location. | Navigasi turn-by-turn dan integrasi jadwal/tiket transportasi resmi. |
| **Data Storage** | Local database (Hive/Isar) untuk menyimpan rute favorit. | Cloud Sync (akun online), Leaderboard. |

---

## 7. Feature Prioritization — MoSCoW

| Priority | Feature | Alasan |
|---|---|---|
| **Must Have** | Interactive Map & Place Search | Pengguna butuh presisi dalam memilih titik tujuan. |
| **Must Have** | Dynamic Geofence Setup | Kustomisasi radius (500m, 1km, dst) krusial sesuai moda transportasi. |
| **Must Have** | Background Location Service | Aplikasi tidak berguna jika mati saat layar dikunci. |
| **Must Have** | Intrusive Alarm Trigger | Inti produk; alarm harus keras dan butuh interaksi fisik untuk mati. |
| **Should Have** | Saved Routes / Favorite Places | Mengurangi friksi penggunaan harian untuk komuter. |
| **Should Have** | Battery Optimization Warning | Panduan *in-app* agar user menonaktifkan *battery saver*. |
| **Could Have** | Custom Alarm Tones | Menambah personalisasi pengalaman pengguna. |
| **Won't Have** | Rilis iOS (Apple App Store) | Ditunda dari MVP untuk menghemat biaya lisensi (Apple Developer Program $99). |

---

## 8. User Journey

| Tahap | Aktivitas Pengguna | Respons Sistem |
|---|---|---|
| **1. Onboarding** | Install dan buka aplikasi pertama kali. | Sistem meminta izin lokasi (Allow All The Time) dan Notifikasi/Alarm. |
| **2. Search Destination** | Mengetik stasiun atau alamat. | Auto-complete API memunculkan saran, pengguna memilih, peta fokus ke pin tujuan. |
| **3. Set Parameters** | Menggeser *slider* radius alarm (misal: 2km). | Sistem menyimpan parameter radius secara lokal. |
| **4. Start Journey** | Menekan tombol "Mulai Perjalanan". | *Foreground Service* aktif, memunculkan notifikasi persisten bahwa pelacakan sedang berjalan. |
| **5. En Route** | Mengunci HP dan memasukkan ke saku/tas. | Sistem di latar belakang secara periodik mengecek koordinat dan menghitung jarak. |
| **6. Geofence Trigger** | Memasuki radius 2km dari tujuan. | Sistem mendeteksi kondisi *True*, menginisiasi *Alarm Engine*. |
| **7. Alarm State** | Pengguna tertidur. | Layar menyala (wake screen), suara dering berbunyi keras, HP bergetar terus-menerus. |
| **8. Resolution** | Pengguna bangun, menekan tombol "Matikan". | Alarm berhenti, *background service* dimatikan, perjalanan selesai. |

---

## 9. Use Cases

| ID | Use Case | Aktor | Hasil / Output |
|---|---|---|---|
| **UC-01** | Mencari lokasi tujuan via Teks. | Pengguna | Drop pin akurat di peta berdasarkan Google Places API. |
| **UC-02** | Mengatur radius geofencing secara kustom. | Pengguna | Threshold jarak tersimpan dalam memori (mis: 1500 meter). |
| **UC-03** | Mengelola (Tambah/Hapus) Lokasi Favorit. | Pengguna | Daftar riwayat/favorit diperbarui di Local DB. |
| **UC-04** | Memulai sesi Background Tracking. | Sistem / OS | Notifikasi *sticky* muncul, CPU melakukan *wake lock* / *foreground polling*. |
| **UC-05** | Menghitung sisa jarak (Haversine Formula). | Sistem | Jarak antara koordinat terkini dan tujuan diperbarui secara berkala. |
| **UC-06** | Memicu Alarm (Geofence terlampaui). | Sistem | Modul audio dan haptic feedback aktif tanpa henti hingga diintervensi. |
| **UC-07** | Mengatasi kehilangan sinyal (Dead Zone). | Sistem | Mengabaikan loncatan GPS palsu; menunggu *fix* akurat, memberi notif jika GPS hilang. |

---

## 10. Functional Requirements — Application

| ID | Requirement Detail | Priority |
|---|---|---|
| **APP-01** | **Permission Request Flow:** Aplikasi harus memvalidasi dan memandu pengguna memberikan izin Lokasi, Notifikasi, dan *Draw Over Other Apps*. | Must |
| **APP-02** | **Map Interface:** Render Google Maps SDK, menampikan *user dot* dan *destination pin*. | Must |
| **APP-03** | **Geofence Configuration:** UI Slider dan Text Input (100m hingga 50km). Tampilan visual lingkaran radius pada peta. | Must |
| **APP-04** | **Background Engine:** Integrasi `flutter_background_service` untuk mempertahankan *polling* GPS setiap X detik/meter. | Must |
| **APP-05** | **Distance Calculation:** Modul internal untuk kalkulasi jarak presisi tinggi (Haversine). | Must |
| **APP-06** | **Alarm Manager:** Mengeksekusi pemutaran media dengan *volume channel* ALARM. | Must |
| **APP-07** | **Wake Screen Notification:** Memaksa layar menyala saat alarm terpicu. | Must |
| **APP-08** | **Local Storage:** CRUD rute menggunakan Hive/Isar DB. | Should |

---

## 11. Detailed Feature Descriptions

**11.1 Dynamic Geofencing & Visualizer**
Tidak hanya menentukan jarak dalam bentuk angka, peta harus menampilkan lingkaran bayangan transparan (overlay) di sekitar titik tujuan yang ukurannya membesar/mengecil sesuai input pengguna.

**11.2 Background Location Engine (Core Engine)**
Tantangan terbesar aplikasi *tracker* adalah manajemen OS (Android Doze) yang suka mematikan aplikasi. Aplikasi harus menginisialisasi *Foreground Service* dengan notifikasi permanen di *status bar*. Polling rate harus adaptif:
- Jarak > 10 km: Polling setiap 1 menit (hemat baterai).
- Jarak < 3 km: Polling setiap 10 detik (akurasi tinggi).

**11.3 Intrusive Alarm State**
Ketika geofence terpicu, aplikasi harus mengikat ke *Audio Service* sistem, menaikkan volume alarm secara bertahap ke maksimum, dan menjalankan pola getaran ekstrem (`Vibrate - Pause - Vibrate`).

**11.4 Signal Loss & Dead Reckoning Handling**
KRL dan MRT sering melewati area *blank spot* atau masuk ke bawah tanah. Jika akurasi GPS memburuk (margin error > 100 meter) atau sinyal hilang, algoritma tidak boleh langsung memicu alarm palsu. Ia harus mencatat lokasi valid terakhir dan menampilkan status *warning*.

---

## 12. Software & System Architecture

| Layer | Komponen | Tanggung Jawab |
|---|---|---|
| **Presentation (UI)** | Flutter Widgets, Riverpod (State) | Menangani interaksi pengguna, merender peta, dan indikator status. |
| **Domain (Logic)** | Geofence Controller, Distance Math | Mengkalkulasi *Haversine*, memvalidasi aturan radius. |
| **Data (Services)** | `geolocator`, `google_maps_flutter` | Mendapatkan koordinat GPS mentah dan merender data spasial API. |
| **OS Interop** | Background Service, Alarm Plugin | Komunikasi *native* dengan Android untuk bypass limitasi *background*. |
| **Persistence** | Hive / Isar NoSQL | Penyimpanan data titik koordinat favorit dan history. |

---

## 13. Data Flow Skenario Perjalanan

1. **User Setup:** User memilih koordinat `(Lat_A, Long_A)` sebagai tujuan dan radius `R`.
2. **Init Service:** UI memanggil Controller untuk memulai *Background Service*.
3. **Polling Loop:** OS memberikan koordinat user terkini `(Lat_U, Long_U)`.
4. **Distance Check:** Controller menghitung jarak `D` antara `(Lat_U, Long_U)` dan `(Lat_A, Long_A)`.
5. **Evaluation:**
   - Jika `D > R`, simpan koordinat ke *cache*, update UI, ulangi loop.
   - Jika `D <= R`, hentikan *Polling Loop*, kirim *Event* ke Alarm Manager.
6. **Trigger:** Alarm Manager membunyikan sirine dan membangunkan layar.
7. **Resolution:** User mematikan alarm, State kembali ke *IDLE*.

---

## 14. Geofencing Logic & State Machine

Aplikasi berjalan pada model *State Machine* berikut:
- `STATE_IDLE`: Aplikasi diam, tidak ada pelacakan.
- `STATE_CONFIGURING`: Pengguna sedang mencari lokasi atau menggeser radius.
- `STATE_TRACKING`: GPS aktif, *foreground service* berjalan. (State terlama).
- `STATE_TRIGGERED`: Masuk geofence, membunyikan alarm. Menunggu input *Stop*.
- `STATE_GPS_LOST`: Sub-state saat pelacakan gagal mendapat *fix* sinyal; menunggu sinyal pulih.

---

## 15. Non-Functional Requirements (NFR)

| Kategori | Requirement |
|---|---|
| **Performance** | Konsumsi memori tidak boleh melebihi 150MB agar tidak di-*kill* OS (OOM). |
| **Battery Efficiency** | *Drain* baterai maksimal 5-7% per jam saat mode pelacakan aktif. |
| **Reliability** | Harus berbunyi 100% jika GPS memberikan *fix* yang valid di dalam radius. |
| **Usability** | Tombol "Matikan Alarm" harus besar agar mudah ditekan saat bangun tidur. |
| **Privacy** | Data lokasi sepenuhnya diolah di perangkat (*on-device*). |

---

## 16. Error & Exception Handling

| Kondisi / Masalah | Respons Sistem |
|---|---|
| Izin lokasi ditolak | Aplikasi memblokir mulai perjalanan dan memandu user ke Settings OS. |
| Akurasi GPS buruk (>100m error) | Mengabaikan data *spike* untuk mencegah alarm palsu. |
| Baterai HP hampir habis (<15%) | Peringatan bahwa OS mungkin akan membunuh aplikasi secara paksa. |
| Akses internet mati di perjalanan | *Background service* dan alarm GPS lokal tetap berjalan. |

---

## 17. Prototype Testing Plan

| Fase Tes | Skenario | Hasil yang Diharapkan |
|---|---|---|
| **Lab/Stationary** | Mode *Mock Location* developer diaktifkan, lompat ke dalam radius tujuan. | Alarm berbunyi kurang dari 3 detik setelah koordinat diletakkan. |
| **Field Test (Surface)** | Naik KRL, set radius 1 km sebelum stasiun tujuan. HP di-lock. | Alarm berbunyi tepat mendekati stasiun. Notifikasi tembus *lock screen*. |
| **Field Test (Underground)**| Naik MRT. Set radius 500m dari stasiun tujuan. | Menguji ketahanan GPS lokal saat kehilangan sinyal satelit. |

---

## 18. Success Metrics

| Metric | Penjelasan / Standar |
|---|---|
| **Alarm Trigger Success Rate** | > 95% untuk perjalanan di atas tanah (KRL, TransJakarta, Bus). |
| **Crash-Free Rate** | > 99% diukur melalui Firebase Crashlytics. |
| **App Store/Play Store Rating** | Target rating > 4.2 dari pengguna aktif bulanan. |
| **User Retention** | > 30% komuter harian menggunakan aplikasi ini setidaknya 3x seminggu. |

---

## 19. Risks and Mitigation

| Risiko Teknis & Bisnis | Tingkat Dampak | Strategi Mitigasi |
|---|---|---|
| **OS Aggressive Task Killer** (Pabrikan HP China). | Sangat Tinggi | 1. Implementasi *Foreground Service* dengan notifikasi persisten.<br>2. Halaman *Troubleshooting* di aplikasi untuk panduan *Battery Optimization*. |
| **Sinyal GPS Hilang** (Underground MRT). | Sedang | Edukasi pengguna. Gunakan `Network Provider Location` tambahan. |
| **False Positive Alarm** (Loncatan sinyal GPS). | Sedang | Algoritma *smoothing*: Harus membaca 3 koordinat valid berturut-turut. |

---

## 20. Rencana Anggaran Biaya (RAB) - Fokus Detail Pengembangan & Lean Ops (< Rp 7.500.000)

RAB ini dirancang dengan menekan biaya operasional/kontingensi serendah mungkin dan **membedah secara rinci alokasi biaya pengembangan (development cost)** untuk Solo Developer yang mengerjakan aplikasi berbasis Flutter secara *end-to-end*.

### A. Penjabaran Biaya Pengembangan (Development Cost Details)
Total Alokasi: **Rp 6.800.000**
*Biaya ini dibagi berdasarkan modul fungsional utama yang dikerjakan oleh Solo Developer selama 8 minggu:*

| Modul / Komponen Pengerjaan | Rincian Tugas & Deliverables | Estimasi Biaya (IDR) |
| :--- | :--- | :--- |
| **1. UI/UX & Setup Project** | - Wireframing & layout dasar halaman peta.<br>- Konfigurasi awal project Flutter & State Management (Riverpod).<br>- Implementasi *Permission Handler* (Lokasi Always, Notifikasi, Draw over apps). | Rp 1.200.000 |
| **2. Core Mapping & Search** | - Integrasi Google Maps SDK & *Marker* posisi pengguna.<br>- Implementasi Google Places API untuk kolom pencarian tujuan.<br>- Visualisasi *Dynamic Geofence Circle* pada peta. | Rp 1.500.000 |
| **3. Background Tracking Engine** | - Konfigurasi `flutter_background_service` untuk Android.<br>- Pemrograman algoritma Haversine untuk kalkulasi jarak waktu nyata (*real-time*).<br>- Logika adaptif *polling rate* dan penanganan *signal loss* / GPS *jump*. | Rp 2.000.000 |
| **4. Alarm & Notification Manager** | - Integrasi pemutar audio dengan prioritas *Alarm Channel*.<br>- Implementasi getaran haptic berulang & *Wake-Screen Intent* (layar menyala saat terkunci).<br>- Pembuatan UI tombol stop alarm ukuran besar. | Rp 1.100.000 |
| **5. Testing & Local Storage** | - Integrasi Hive / Isar DB untuk menyimpan riwayat rute favorit.<br>- *Debugging* memori, optimasi baterai, & QA internal (Android device testing). | Rp 1.000.000 |
| **Sub-Total A** | | **Rp 6.800.000** |

### B. Biaya Infrastruktur & Lisensi Sistem (Fixed Cost)
Total Alokasi: **Rp 400.000**
| Layanan | Deskripsi Lisensi / Kuota | Estimasi Biaya (IDR) |
| :--- | :--- | :--- |
| **Google Play Console** | Lisensi developer Android (Sekali bayar seumur hidup - $25) | Rp 400.000 |
| **Sub-Total B** | | **Rp 400.000** |

### C. Biaya Operasional / Kontingensi (Minimalis / Lean)
Total Alokasi: **Rp 200.000**
*(Biaya operasional dipangkas habis karena tidak krusial, hanya menyisakan alokasi sangat kecil untuk token/kuota tes API dan validasi darurat).*
| Pos Pengeluaran | Deskripsi | Estimasi Biaya (IDR) |
| :--- | :--- | :--- |
| **Internet & API Testing** | Alokasi kecil kuota internet/koneksi saat build & deploy Google Maps API | Rp 200.000 |
| **Sub-Total C** | | **Rp 200.000** |

**TOTAL ESTIMASI KESELURUHAN (A + B + C): Rp 7.400.000** *(Memenuhi syarat di bawah Rp 7.500.000)*

---

## 21. Roadmap & Timeline Prototipe (8 Minggu - Solo Dev Approach)

| Sprint / Minggu | Target Pencapaian (Output) |
|---|---|
| **Minggu 1-2** | Setup project Flutter, implementasi UI Peta (Map SDK), fitur pencarian lokasi & Database Lokal selesai. |
| **Minggu 3-4** | Koding *Core Logic*: Kalkulasi Haversine, Marker Peta responsif, & Setup *Foreground Service* Android. |
| **Minggu 5-6** | Menyelesaikan *Background Location Service* (Aplikasi tidak mati saat layar terkunci) & Integrasi Sistem Alarm (Getaran dan Wake-screen). |
| **Minggu 7** | *Field Test* Lapangan: Developer turun ke stasiun, mengetes KRL dan TransJakarta. |
| **Minggu 8** | *Bug fixing*, pembuatan *Store Assets* (Screenshot, icon), proses *submit review* ke Google Play Store. |

---

## 22. MVP Definition & Finalisasi

Produk Minimum Viable (MVP) untuk rilis awal dinyatakan siap apabila:
1. Pengguna dapat menginput tujuan dan mengatur radius.
2. Aplikasi sukses membunyikan peringatan yang kuat saat layar ponsel dalam keadaan terkunci di dalam saku celana.
3. Arsitektur GPS efisien sehingga konsumsi daya selama perjalanan 2 jam tidak menguras lebih dari 15% baterai normal ponsel rata-rata.
4. Tidak ada integrasi server (Backend/Cloud) eksternal selain layanan dasar pemetaan dan analytics untuk memastikan pengembangan cepat, biaya operasional awal rendah, dan menjaga privasi pengguna.

---

## 23. Kesimpulan

PRD WakeMeThere ini merinci alokasi anggaran dengan sangat transparan di mana **porsi biaya pengembangan dijabarkan per modul pekerjaan** secara detail, sementara biaya operasional ditekan seminimal mungkin (hampir ditiadakan) agar total keseluruhan tetap berada di angka **Rp 7.400.000** (di bawah batas maksimal Rp 7,5 juta). Pendekatan ini sangat efektif untuk pendanaan mandiri atau proyek MVP skala mikro.
