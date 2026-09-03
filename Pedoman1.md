# PRODUCT REQUIREMENTS DOCUMENT (PRD)
## WakeMeThere: Aplikasi Alarm Perjalanan Berbasis Lokasi (Geofencing)

| | |
|---|---|
| **Dokumen** | Product Requirements Document — Versi 2.0 (Comprehensive) |
| **Nama Proyek** | WakeMeThere |
| **Platform** | iOS & Android (Cross-platform) |
| **Tahap** | Perancangan, Pengembangan MVP, dan Rilis Publik |
| **Target Utama** | Mencegah pengguna kendaraan umum terlewat tujuan melalui pelacakan lokasi dan notifikasi jarak. |

---

## 1. Executive Summary

WakeMeThere adalah aplikasi asisten perjalanan cerdas berbasis *Geofencing* yang dirancang khusus untuk komuter dan pelancong. Berbeda dengan alarm konvensional yang mengandalkan waktu, WakeMeThere menggunakan lokasi pengguna secara *real-time* untuk memicu peringatan (alarm dan getaran) ketika pengguna memasuki radius jarak tertentu dari titik tujuan.

Produk ini dirancang dengan arsitektur *mobile-first* yang efisien di mana sistem pelacakan (GPS) beroperasi secara presisi di latar belakang tanpa menguras baterai secara ekstrem. Fokus utama tahap pengembangan MVP ini adalah pembuktian keandalan *background location tracking* dan sistem alarm yang intrusif agar pengguna yang tertidur di kendaraan umum (KRL, MRT, Bus) dapat terbangun tepat waktu.

---

## 2. Latar Belakang dan Problem Statement

Penggunaan transportasi umum sering kali menjadi waktu bagi komuter untuk beristirahat, membaca, atau menggunakan gawai. Sayangnya, tidak ada jaminan waktu tempuh yang pasti akibat kemacetan atau gangguan teknis operasional transit.

**Problem yang ingin diselesaikan:**
- Pengguna sering tertidur dan melewati stasiun/halte tujuan mereka, menyebabkan kerugian waktu dan biaya.
- Alarm berbasis jam (waktu) tidak efektif karena waktu tempuh transportasi umum sering berubah-ubah.
- Notifikasi aplikasi navigasi biasa (seperti Google Maps) terlalu pelan dan tidak dirancang untuk membangunkan orang tidur.
- Kebutuhan akan *tracker* yang tetap berjalan di latar belakang (background) ketika layar ponsel dimatikan atau ponsel dimasukkan ke dalam saku.

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
| OBJ-05 | Meluncurkan MVP yang stabil dan efisien baterai di App Store dan Google Play Store. |

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
| **Alarm System** | Nada dering persisten, getaran maksimal, bypass DND (Do Not Disturb) jika OS mengizinkan. | Integrasi dengan Smartwatch/Wearable device secara native. |
| **Mapping** | Integrasi Google Maps, Search Place API, My Location. | Navigasi turn-by-turn dan integrasi jadwal/tiket transportasi resmi. |
| **Data Storage** | Local database (Hive/Isar) untuk menyimpan rute/tempat favorit. | Cloud Sync (akun online), Leaderboard. |

---

## 7. Feature Prioritization — MoSCoW

| Priority | Feature | Alasan |
|---|---|---|
| **Must Have** | Interactive Map & Place Search | Pengguna butuh presisi dalam memilih titik tujuan. |
| **Must Have** | Dynamic Geofence Setup | Kustomisasi radius (500m, 1km, dst) krusial sesuai moda transportasi. |
| **Must Have** | Background Location Service | Aplikasi tidak berguna jika mati saat layar dikunci. |
| **Must Have** | Intrusive Alarm Trigger | Inti produk; alarm harus keras dan butuh interaksi fisik untuk mati. |
| **Should Have** | Saved Routes / Favorite Places | Mengurangi friksi penggunaan harian untuk komuter. |
| **Should Have** | Battery Optimization Warning | Panduan *in-app* agar user menonaktifkan *battery saver* untuk app ini. |
| **Could Have** | Custom Alarm Tones | Menambah personalisasi pengalaman pengguna. |
| **Won't Have** | Transit Schedules / Live Traffic | Kompleksitas tinggi dan di luar fokus utama MVP. |

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
| **UC-07** | Mengatasi kehilangan sinyal (Dead Zone). | Sistem | Mengabaikan loncatan GPS palsu; menunggu *fix* akurat, memberi notif jika GPS hilang total > 5 menit. |

---

## 10. Functional Requirements — Application

| ID | Requirement Detail | Priority |
|---|---|---|
| **APP-01** | **Permission Request Flow:** Aplikasi harus memvalidasi dan memandu pengguna memberikan izin Lokasi (Always), Notifikasi, dan *Draw Over Other Apps* (Android). | Must |
| **APP-02** | **Map Interface:** Render Google Maps SDK, menampikan *user dot* (lokasi saat ini) dan *destination pin*. | Must |
| **APP-03** | **Geofence Configuration:** UI Slider dan Text Input untuk rentang jarak 100m hingga 50km. Tampilan visual lingkaran radius pada peta. | Must |
| **APP-04** | **Background Engine:** Integrasi `flutter_background_service` untuk mempertahankan *polling* GPS setiap X detik/meter. | Must |
| **APP-05** | **Distance Calculation:** Modul internal untuk kalkulasi jarak presisi tinggi (memperhitungkan kelengkungan bumi). | Must |
| **APP-06** | **Alarm Manager:** Mengeksekusi pemutaran media dengan *volume channel* ALARM, bukan MEDIA (agar tetap bunyi walau HP di-silent, dengan asumsi izin OS). | Must |
| **APP-07** | **Wake Screen Notification:** Memaksa layar menyala (Full-screen intent di Android) saat alarm terpicu. | Must |
| **APP-08** | **Local Storage:** CRUD rute menggunakan Hive/Isar DB. | Should |

---

## 11. Detailed Feature Descriptions

**11.1 Dynamic Geofencing & Visualizer**
Tidak hanya menentukan jarak dalam bentuk angka, peta harus menampilkan lingkaran bayangan transparan (overlay) di sekitar titik tujuan yang ukurannya membesar/mengecil sesuai input pengguna. Ini memberikan konteks visual seberapa jauh alarm akan berbunyi sebelum stasiun.

**11.2 Background Location Engine (Core Engine)**
Tantangan terbesar aplikasi *tracker* adalah manajemen OS (Android Doze / iOS Background Fetch) yang suka mematikan aplikasi. Aplikasi harus menginisialisasi *Foreground Service* dengan notifikasi permanen di *status bar*. Polling rate harus adaptif:
- Jarak > 10 km: Polling setiap 1 menit (hemat baterai).
- Jarak < 3 km: Polling setiap 10 detik (akurasi tinggi).

**11.3 Intrusive Alarm State**
Ketika geofence terpicu, aplikasi tidak hanya mengirim notifikasi *push* (yang mudah terabaikan). Ia harus mengikat ke *Audio Service* sistem, menaikkan volume alarm secara bertahap (fade-in) ke maksimum, dan menjalankan pola getaran ekstrem (`Vibrate - Pause - Vibrate`).

**11.4 Signal Loss & Dead Reckoning Handling**
KRL dan MRT sering melewati area *blank spot* atau masuk ke bawah tanah. Jika akurasi GPS memburuk (margin error > 100 meter) atau sinyal hilang, algoritma tidak boleh langsung memicu alarm palsu. Ia harus mencatat lokasi valid terakhir dan menampilkan status *warning* di antarmuka.

---

## 12. Software & System Architecture

| Layer | Komponen | Tanggung Jawab |
|---|---|---|
| **Presentation (UI)** | Flutter Widgets, Riverpod (State) | Menangani interaksi pengguna, merender peta, dan indikator status. |
| **Domain (Logic)** | Geofence Controller, Distance Math | Mengkalkulasi *Haversine*, memvalidasi aturan radius, mengatur status perjalanan. |
| **Data (Services)** | `geolocator`, `google_maps_flutter` | Mendapatkan koordinat GPS mentah dan merender data spasial API. |
| **OS Interop** | Background Service, Alarm Plugin | Komunikasi *native* dengan Android/iOS untuk bypass limitasi *background*. |
| **Persistence** | Hive / Isar NoSQL | Penyimpanan data titik koordinat favorit dan history konfigurasi. |

---

## 13. Data Flow Skenario Perjalanan

1. **User Setup:** User memilih koordinat `(Lat_A, Long_A)` sebagai tujuan dan radius `R`.
2. **Init Service:** UI memanggil Controller untuk memulai *Background Service*.
3. **Polling Loop:** OS memberikan koordinat user terkini `(Lat_U, Long_U)`.
4. **Distance Check:** Controller menghitung jarak `D` antara `(Lat_U, Long_U)` dan `(Lat_A, Long_A)`.
5. **Evaluation:**
   - Jika `D > R`, simpan koordinat ke *cache*, update UI (jika terbuka), ulangi loop.
   - Jika `D <= R`, hentikan *Polling Loop*, kirim *Event* ke Alarm Manager.
6. **Trigger:** Alarm Manager memanggil *native bridge* untuk membunyikan sirine dan membangunkan layar.
7. **Resolution:** User mematikan alarm, State kembali ke *IDLE*.

---

## 14. Geofencing Logic & State Machine

Aplikasi berjalan pada model *State Machine* berikut:
- `STATE_IDLE`: Aplikasi diam, tidak ada pelacakan.
- `STATE_CONFIGURING`: Pengguna sedang mencari lokasi atau menggeser radius.
- `STATE_TRACKING`: GPS aktif, *foreground service* berjalan. (State terlama).
- `STATE_TRIGGERED`: Masuk geofence, membunyikan alarm. Menunggu input *Stop*.
- `STATE_GPS_LOST`: Sub-state saat pelacakan gagal mendapat *fix* sinyal; alarm tidak ditekan, menunggu sinyal pulih.

---

## 15. Non-Functional Requirements (NFR)

| Kategori | Requirement |
|---|---|
| **Performance** | Konsumsi memori tidak boleh melebihi 150MB agar tidak di-*kill* OS (OOM). |
| **Battery Efficiency** | *Drain* baterai maksimal 5-7% per jam saat mode pelacakan aktif. |
| **Reliability** | Harus berbunyi 100% jika GPS memberikan *fix* yang valid di dalam radius. |
| **Usability** | Tombol "Matikan Alarm" harus cukup besar agar mudah ditekan orang yang baru bangun tidur, tapi tidak mudah tidak sengaja tertekan. |
| **Privacy** | Data lokasi sepenuhnya diolah di perangkat (*on-device*). Tidak ada data GPS yang dikirim ke server pihak ketiga (kecuali agregat *crash reporting* anonim). |

---

## 16. Error & Exception Handling

| Kondisi / Masalah | Respons Sistem |
|---|---|
| Izin lokasi "Only While Using" | Aplikasi memblokir mulai perjalanan dan memandu user mengganti ke "Allow All The Time" di Settings OS. |
| Akurasi GPS buruk (>100m error) | Mengabaikan data *spike* untuk mencegah alarm palsu. Menampilkan *banner* kuning "Akurasi GPS Rendah". |
| Baterai HP hampir habis (<15%) | Menampilkan peringatan kepada pengguna bahwa OS mungkin akan membunuh aplikasi secara paksa. |
| Akses internet mati di perjalanan | *Background service* dan kalkulasi GPS tetap berjalan (titik peta mungkin tidak *load*, tapi alarm tetap valid karena pakai GPS lokal). |

---

## 17. Prototype Testing Plan

| Fase Tes | Skenario | Hasil yang Diharapkan |
|---|---|---|
| **Lab/Stationary** | Mode *Mock Location* developer diaktifkan, lompat ke dalam radius tujuan. | Alarm berbunyi kurang dari 3 detik setelah koordinat diletakkan. |
| **Field Test (Surface)** | Tim naik KRL rute Depok - Manggarai. Set radius 1 km sebelum St. UI. Layar dimatikan, HP masuk saku. | Alarm berbunyi tepat saat KRL mendekati pondok cina/UI. Notifikasi tembus kondisi *lock screen*. |
| **Field Test (Underground)**| Tim naik MRT rute Blok M - Bundaran HI. Set radius 500m dari HI. | (Risiko) GPS berpotensi hilang. Verifikasi apakah *last known location* atau jaringan *cellular tower* cukup untuk memicu alarm. |

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
| **OS Aggressive Task Killer** (Pabrikan HP China, iOS strict limit). | Sangat Tinggi | 1. Implementasi *Foreground Service* dengan notifikasi persisten.<br>2. Sediakan halaman *Troubleshooting* di aplikasi untuk menuntun pengguna men-disable *Battery Optimization* per-device. |
| **Sinyal GPS Hilang** (Underground MRT / Terowongan). | Sedang | Memberikan edukasi/disclaimer kepada pengguna. Gunakan kombinasi `Network Provider Location` selain `GPS Provider`. |
| **False Positive Alarm** (Loncatan sinyal GPS / *Rubber-banding*). | Sedang | Algoritma *smoothing*: Harus membaca 3 koordinat valid berturut-turut di dalam radius sebelum memicu sirine. |

---

## 20. Rencana Anggaran Biaya (RAB) - Pengembangan MVP

RAB ini ditujukan untuk pendanaan tahap pertama (pengerjaan 1,5 – 2 bulan oleh tim skala kecil/Freelance/In-House Startup).

### A. Biaya Pengembangan Tim (Development Cost)
| Posisi / Peran | Tanggung Jawab & Deskripsi | Durasi Kerja | Estimasi Biaya (IDR) |
| :--- | :--- | :--- | :--- |
| **UI/UX Designer** | Riset kompetitor, Wireframing, Hi-Fi Prototype Figma, Asset creation | 1 Bulan | Rp 6.500.000 |
| **Flutter Developer** | Koding lintas platform, integrasi Map API, Native Bridge, State Management | 1,5 Bulan | Rp 22.000.000 |
| **QA / Field Tester** | Uji coba multi-device (Android & iOS), Field Test rute KRL/MRT | 2 Minggu | Rp 3.500.000 |
| **Project Manager** | Scrum master, mengelola backlog, menjamin requirement tercapai | 1,5 Bulan | Rp 5.000.000 |
| **Sub-Total A** | | | **Rp 37.000.000** |

### B. Biaya Infrastruktur & Lisensi Sistem (Tahun Pertama)
| Layanan | Deskripsi Lisensi / Kuota | Estimasi Biaya (IDR) |
| :--- | :--- | :--- |
| **Google Play Console** | Lisensi developer Android (Sekali bayar seumur hidup - $25) | Rp 400.000 |
| **Apple Developer Program**| Lisensi App Store (Berlangganan Tahunan - $99) | Rp 1.600.000 |
| **Google Maps Platform** | Akses Peta & Place API (Tier gratis $200/bulan, sangat cukup untuk MVP) | Rp 0 (Free Tier) |
| **Firebase / Analytics** | Crash tracking & analytics (Free tier) | Rp 0 (Free Tier) |
| **Asset Digital** | Lisensi sound effect alarm khusus, icon pack premium | Rp 800.000 |
| **Sub-Total B** | | **Rp 2.800.000** |

### C. Biaya Operasional Tambahan (Opsional / Kontingensi)
| Pos Pengeluaran | Deskripsi | Estimasi Biaya (IDR) |
| :--- | :--- | :--- |
| **Field Test Transport** | Saldo uang elektronik (E-Money) untuk pengujian QA bolak-balik KRL/MRT/Bus | Rp 500.000 |
| **Initial Marketing** | Ads Social Media (Instagram/TikTok) fase *Early Adopters* | Rp 3.000.000 |
| **Biaya Tak Terduga (Buffer)**| Alokasi darurat (10% dari total) untuk kendala server/tambahan waktu dev | Rp 4.000.000 |
| **Sub-Total C** | | **Rp 7.500.000** |

**TOTAL ESTIMASI KESELURUHAN (A + B + C): Rp 47.300.000**

---

## 21. Roadmap & Timeline Prototipe (8 Minggu)

| Sprint / Minggu | Target Pencapaian (Output) |
|---|---|
| **Minggu 1** | Penyelarasan Requirement, Finalisasi UI/UX (Figma), Arsitektur Database Lokal. |
| **Minggu 2** | Setup project Flutter, implementasi Map SDK, fungsi pencarian lokasi & Place API selesai. |
| **Minggu 3** | Koding *Core Logic*: Kalkulasi Haversine, Slider Radius Geofence, Marker Peta responsif. |
| **Minggu 4** | Implementasi *Background Location Service* (Android Foreground Service & iOS Background Task). |
| **Minggu 5** | Implementasi *Alarm Engine* (Bypass volume, getaran haptic, wake-screen intents). |
| **Minggu 6** | QA Internal (Alpha): *Stationary test*, optimasi RAM, debugging loncatan GPS palsu. |
| **Minggu 7** | *Field Test* (Beta): Tim turun ke stasiun, mengetes KRL dan TransJakarta. Penyempurnaan UX *Troubleshooting* baterai. |
| **Minggu 8** | *Release Candidate*: Pembuatan *Store Assets* (Screenshot, deskripsi), proses review App Store dan Play Store. |

---

## 22. MVP Definition & Finalisasi

Produk Minimum Viable (MVP) untuk rilis awal dinyatakan siap apabila:
1. Pengguna dapat menginput tujuan dan mengatur radius.
2. Aplikasi sukses membunyikan peringatan yang kuat saat layar ponsel dalam keadaan terkunci di dalam saku celana.
3. Arsitektur GPS efisien sehingga konsumsi daya selama perjalanan 2 jam tidak menguras lebih dari 15% baterai normal ponsel rata-rata.
4. Tidak ada integrasi server (Backend/Cloud) eksternal selain layanan dasar pemetaan dan analytics untuk memastikan pengembangan cepat, biaya operasional awal rendah, dan menjaga privasi pengguna.

---

## 23. Kesimpulan

PRD WakeMeThere ini merinci seluruh tahapan pembangunan sistem alarm berbasis lokasi dari perspektif pengembangan produk *mobile end-to-end*. Mengadopsi pedoman sistem keselamatan dan pemantauan pergerakan, aplikasi ini mengutamakan **reliabilitas eksekusi latar belakang** dan **akurasi data spasial (sensor lokasi)**. Dengan rancangan arsitektur, pemetaan risiko, NFR, dan rincian RAB yang matang, dokumen ini menjadi landasan kokoh bagi tim *developer*, desainer, dan *stakeholder* untuk segera mengeksekusi proyek dengan anggaran efisien dan target rilis terukur.
