# IoT Dashboard — Monitoring Sensor & Kontrol Aktuator

Dashboard pemantauan sensor suhu dan kelembaban berbasis web yang terintegrasi dengan **Node-RED** menggunakan REST API, autentikasi `X-API-Key`, visualisasi grafik real-time **Chart.js**, serta sistem peringatan multi-kanal.

---

## Identitas Mahasiswa

| Keterangan | Detail |
| :--- | :--- |
| **Nama** | Salfani Khairussalim |
| **NPM** | 2410010363 |
| **Kelas** | 5N (Semester 5) |
| **GitHub** | [@Salfanikh](https://github.com/Salfanikh) |

---

## Fitur Utama Dashboard

- **Real-Time Telemetry Cards:** Menampilkan nilai suhu (`°C`), kelembaban (`%`), status koneksi perangkat (`ONLINE` / `OFFLINE`), dan status ambang batas (`NORMAL` / `WARNING`).
- **Grafik Monitoring Real-Time (Chart.js):** Visualisasi tren 20 pembacaan sensor terakhir dengan kurva interaktif dan gradasi warna untuk suhu serta kelembaban.
- **Sistem Peringatan & Notifikasi Multi-Kanal:**
  - *In-App Floating Toast Notification* untuk status threshold, kontrol perangkat, dan gangguan koneksi.
  - *Browser Desktop Notification API* saat tab browser berjalan di latar belakang.
  - *Audio Alarm (Web Audio API)* otomatis ketika nilai sensor melewati ambang batas.
  - *Alert Banner* dinamis pada panel dashboard.
- **Kontrol Aktuator Jarak Jauh:** Tombol interaktif untuk menyalakan (`ON`) dan mematikan (`OFF`) lampu melalui Node-RED.
- **Riwayat 10 Data Sensor Terakhir:** Tabel riwayat lengkap dengan penanda warna otomatis untuk nilai yang melampaui threshold.
- **Console Log Aktivitas:** Catatan diagnostik *real-time* untuk memantau respons API dan perubahan status sistem.

---

## Implementasi Tugas Pengembangan (Nilai Tambah)

Proyek ini mencakup pengembangan fitur lanjutan berikut:

- [x] **Endpoint `PUT /api/threshold` & Notifikasi Otomatis:** Mendukung pembaruan batas suhu dan kelembaban ke backend Node-RED serta memicu notifikasi otomatis (Toast, Desktop Notification, dan Audio Alarm) saat batas terlampaui.
- [x] **Grafik Real-Time dengan Chart.js:** Menggunakan pustaka `Chart.js` untuk merender grafik garis dua variabel (Suhu & Kelembaban) secara langsung tanpa *reload* halaman.
- [x] **Autentikasi API Key (`X-API-Key`):** Setiap permintaan HTTP dari dashboard menyertakan header `X-API-Key` untuk validasi akses pada flow Node-RED.
- [x] **Komunikasi Real-Time WebSocket Node-RED:** Mendukung jalur WebSocket (`ws://127.0.0.1:1880/ws/sensor`) untuk menerima *push data* sensor secara instan tanpa *polling* berulang.
- [x] **Penyimpanan Riwayat ke Database (SQLite / InfluxDB):** Data telemetri sensor disimpan secara persisten ke database sehingga riwayat 10 data terakhir tetap tersedia meskipun Node-RED di-*restart*.

---

## Dokumentasi API & WebSocket

### Autentikasi
Semua endpoint REST API mewajibkan header berikut:

```http
Content-Type: application/json
x-api-key: KULIAH-API-2026
