# Smart Greenhouse – Blynk HTML Widget

Widget UI untuk dashboard HP Blynk, dibuat untuk alat **Smart Greenhouse v3 (versi fisik)**.
Satu file `index.html`, tanpa library, tanpa build.

## Fitur
- Sensor: suhu (V0), kelembapan (V1), cahaya (V2), dengan penanda oranye/merah saat melewati ambang
- Teks peringatan alat (V6)
- Mode Otomatis / Manual (V4)
- Kontrol manual: kipas (V5), ventilasi (V8), pompa (V10), LED cahaya (V11)
- Status nyata alat: kipas (V3), ventilasi (V7), pompa (V9), LED (V12)
- Update tombol instan (optimistic UI), konfirmasi balik dari alat ±0,15 dtk, polling 1 dtk
- Mode Demo (tanpa token) untuk uji tampilan

## Datastream (harus sama dengan template Blynk)
| Pin | Tipe | Arah | Fungsi |
|---|---|---|---|
| V0 | Double | Alat → App | Suhu (°C) |
| V1 | Double | Alat → App | Kelembapan (%RH) |
| V2 | Double | Alat → App | Cahaya (lux) |
| V3 | Integer | Alat → App | Status kipas |
| V4 | Integer | Dua arah | Mode (0 = Auto, 1 = Manual) |
| V5 | Integer | Dua arah | Kipas manual |
| V6 | String | Alat → App | Teks peringatan |
| V7 | Integer | Alat → App | Status ventilasi |
| V8 | Integer | Dua arah | Ventilasi manual |
| V9 | Integer | Alat → App | Status pompa |
| V10 | Integer | Dua arah | Pompa manual |
| V11 | Integer | Dua arah | LED cahaya manual |
| V12 | Integer | Alat → App | Status LED cahaya |

Event Blynk (8 kode, dikirim alat lewat `Blynk.logEvent()`): `suhu_tinggi`, `kelembapan_rendah`,
`kelembapan_tinggi`, `cahaya_rendah`, `cahaya_tinggi`, `sensor_dht_error`, `sensor_bh1750_error`, `pompa_batas_waktu`.

## Cara pakai

### A. Tempel ke widget HTML Blynk
1. Salin seluruh isi `index.html` ke widget HTML di dashboard.
2. Tekan ikon ⚙ di widget, isi Auth Token, simpan.

### B. Lewat GitHub Pages + widget Web Page
1. Di repo: **Settings → Pages → Deploy from a branch → `main` / root**.
2. Buka `https://USERNAME.github.io/NAMA-REPO/?token=AUTH_TOKEN_ANDA`
3. Pasang URL tersebut di widget Web Page Blynk.

## Keamanan
- **Jangan commit Auth Token** ke repo. Variabel `TOKEN` di `index.html` sengaja dikosongkan.
- Token di URL (`?token=`) tersimpan di riwayat browser; pakai hanya di perangkat pribadi.
- Repo publik + token yang bocor = orang lain bisa mengontrol alat Anda. Jika bocor, buat token baru di Blynk Console.

## Konfigurasi
Di bagian atas `<script>` pada `index.html`:
- `HOST` – ganti jika region Blynk bukan `blynk.cloud` (mis. `sgp1.blynk.cloud`)
- `POLL_MS` – interval baca (default 1000 ms)
- `T` – ambang suhu/kelembapan/cahaya (samakan dengan sheet Parameter di kode alat)
