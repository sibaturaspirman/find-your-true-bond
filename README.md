# Find Your True Bond

Kuis kepribadian berpasangan (Player 1 & Player 2) untuk booth/kiosk.
Semua sudah ada di **index.html**: font, gambar, logo, dan library QR tertanam di dalamnya,
jadi web ini jalan 100% offline tanpa file tambahan.

## Cara pakai
- **Langsung:** buka `index.html` di browser (Chrome disarankan).
- **Di TV / tablet kiosk:** buka `index.html` lewat browser lalu set ke mode layar penuh (kiosk mode).
- **Hosting online:** upload `index.html` ke hosting statis mana pun (Netlify, Vercel, GitHub Pages, server sendiri).

## Pengaturan (di bagian atas `<script>` dalam index.html)
| Setting | Default | Fungsi |
|---|---|---|
| `UPLOAD_ENDPOINT` | `https://photo-ai-iims.zirolu.id/v1/iqos` | API tempat gambar hasil diunggah |
| `UPLOAD_AUTH` | `client_id:secret` | Header `Authorization` untuk upload |
| `RESULT_BASE_URL` | link artifact claude.ai | Tidak dipakai QR. Halaman `#r-...` tetap bisa menggambar story kalau link lama dibuka |
| `QUESTION_SECONDS` | 10 | Waktu tiap pemain menjawab |
| `WARN_AT` | 3 | Detik terakhir timer berubah warna + bunyi tik |
| `HOME_SECONDS` | 15 | Halaman QR kembali ke Home otomatis |
| `RESULT_FLIP_MS` | 3600 | Jeda kartu hasil bergantian depan-belakang |
| `PROCESS_MS` | 3400 | Lama animasi loading sebelum hasil |
| `IDLE_MS` | 90000 | Layar kembali ke Home kalau tidak disentuh |
| `SOUND_ON` / `SOUND_VOLUME` | true / 0.7 | Efek suara |
| `KEYBOARD_MODE` | "auto" | Input nama: `auto` = keyboard di layar untuk PC/TV touchscreen, keyboard bawaan untuk HP/tablet. Bisa dipaksa `always` / `never` |
| `NAME_MAX` | 12 | Panjang maksimal nama pemain (kedua nama wajib diisi sebelum NEXT) |
| `BOND_DESC` | teks | Kalimat di kartu Bond Meter |

## Bond Meter (persentase kecocokan)
Setiap pertanyaan yang jawaban Player 1 dan Player 2 sama (huruf A/B/C yang sama) = 25%.
Yang ditampilkan di kartu Bond Meter hanya persentasenya (tanpa label).

## QR hasil digital (Instagram Story)
Satu QR untuk berdua. Di halaman download, kiosk menggambar hasil 1080×1920 (ukuran Story IG),
mengunggah JPEG itu ke API (`name`, `phone`, `file`), lalu QR meng-encode URL publik di field `file`.
Scan membuka gambar itu langsung. Kalau upload gagal atau offline, QR tidak muncul dan bisa dicoba lagi.
URL upload yang sukses disimpan di `sessionStorage` supaya tap download yang sama tidak mengunggah dua kali.
Halaman `#r-...` (kode hasil + nama) tetap ada untuk link lama: HP menggambar story sendiri dan bisa disimpan.

## Perhitungan hasil (sesuai Find_Your_True_Bond_Matrix.xlsx)
Tipe tiap jawaban (S = The Spark, M = The Magnet, K = The Seeker):
Q1 A=S B=K C=M · Q2 A=S B=K C=M · Q3 A=M B=S C=K · Q4 A=K B=M C=S.
Tipe terbanyak dari 4 jawaban jadi hasil; kalau seri, dipakai tipe jawaban Q4.
Hasil tiap pemain dihitung dari jawabannya sendiri (sheet "Bond Match": Personality A / B).
Sudah dicek cocok dengan 81 baris sheet Matrix dan 6.561 baris sheet Bond Match.

## Folder assets
Salinan aset untuk diedit atau dipakai ulang (tidak dibutuhkan untuk menjalankan web):
- `assets/background.jpg` – background
- `assets/svg/` – logo dan judul bridging dalam bentuk vektor
- `assets/fonts/` – font IQOS dan Migra Italic Extrabold (subset) yang dipakai di web
