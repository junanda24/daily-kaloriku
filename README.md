# KALORIKU! — Hitung Kalori Makanan Indonesia

> Pelacak kalori yang ngerti makanan Indonesia: nasi padang, bakso, mie ayam, gorengan, es teh manis, sampai klepon — dihitung pakai satuan porsi asli (piring, mangkok, potong, buah), bukan gram.

**Rilis:** 2026-11-14 · **Jenis:** web app (frontend-only, tanpa backend) · **Program:** 1 Hari 1 Project
**Link hasil:** artifact `kaloriku` (link kartu artifact)
**Repo:** https://github.com/junanda24/daily-kaloriku

## Kenapa ide ini dipilih

Semua aplikasi kalori besar datanya Barat dan porsinya gram. Orang Indonesia makan pakai "piring", "mangkok", "potong", "buah". KALORIKU! memakai satuan itu — dan hampir semua orang salah tebak kalori makanan sehari-harinya (soto ayam 480 kkal terasa "ringan", padahal setara hampir 2 piring nasi). Rasa kaget itu diubah jadi permainan lewat kuis Tebak Kalori. Ini alat yang dipakai 3x sehari, bukan sekali pakai.

## Fitur

- **Katalog 51 makanan Indonesia** — 7 kategori (Nasi, Mie & Bakso, Lauk, Gorengan, Jajanan, Minuman, Buah), pencarian langsung, filter kategori.
- **Piring Hari Ini** — tambah makanan dengan pengali porsi 0,5× / 1× / 1,5× / 2×, hapus item, kosongkan piring, total kalori berjalan dengan animasi count-up.
- **Cincin progres animasi** — total hari ini lawan target harian; confetti saat target tercapai.
- **Target harian** — preset AKG 2019 (Umum 2000, Wanita 2250, Pria 2650 kkal) + slider kustom 1200–3500 kkal, tersimpan.
- **Setara Dengan** — total kalori diterjemahkan ke menit jalan kaki (≈4 kkal/mnt), menit lari (≈10 kkal/mnt), piring nasi (270 kkal), gelas es teh manis (100 kkal).
- **Riwayat 7 hari** — total per hari tersimpan otomatis, grafik batang CSS, hari ini ter-highlight. Piring berganti hari otomatis (total kemarin masuk riwayat).
- **Tebak Kalori (kuis)** — 5 ronde, 3 pilihan jawaban, skor + skor terbaik tersimpan, confetti saat skor sempurna 5/5.
- **Tanpa login, tanpa backend** — semua data tersimpan di localStorage perangkat pengguna.

## Cara pakai

1. Buka link hasil di atas (HP atau desktop).
2. Tab **Katalog**: cari makanan, ketuk **+ Tambah**, pilih porsi (setengah / satu / satu setengah / dua).
3. Tab **Piring**: lihat total kalori hari ini di cincin, atur target harian, lihat "Setara dengan" dan riwayat 7 hari.
4. Tab **Tebak**: mainkan kuis Tebak Kalori, kejar skor 5/5.
5. Data tersimpan otomatis di browser — tutup dan buka lagi, piring hari ini tetap ada.

## Cara menjalankan dari source

Project ini adalah artifact web statis. Source hasil export ada di `src/` (satu file `kaloriku.html` mandiri + file-file build artifact):

```bash
# Cara paling gampang: buka langsung
open src/kaloriku.html        # macOS
xdg-open src/kaloriku.html    # Linux

# Atau sajikan lewat server statis apa pun
python3 -m http.server -d src 8080
# lalu buka http://localhost:8080/kaloriku.html
```

Tidak ada langkah build, tidak ada dependency, tidak ada environment variable.

## Tech stack

- HTML + CSS + JavaScript (client-side saja, tanpa framework build)
- Google Fonts: Fredoka (display) + Nunito (body)
- localStorage untuk piring harian, riwayat 7 hari, target, dan skor terbaik kuis
- SVG progress ring + partikel confetti buatan sendiri (tanpa library)

## Struktur folder

```
2026-11-14-kaloriku/
├── README.md
├── src/
│   └── kaloriku.html        # export artifact (self-contained)
└── openspec/
    └── changes/
        └── 2026-11-14-kaloriku/
            ├── proposal.md
            ├── design.md
            ├── tasks.md
            └── specs/kaloriku/spec.md
        └── archive/
            └── 2026-11-14-kaloriku/   # arsip change setelah selesai
```

## Data kalori — sumber & kejujuran angka

Semua angka adalah **perkiraan per porsi umum**, bukan hasil lab. Sumber yang dipakai (riset 2026-11-14):

| Sumber | Dipakai untuk |
|---|---|
| TKPI Kemenkes 2020 | Nasi putih 180 kkal/100 g (1 piring 150 g = 270 kkal), nasi merah 149 kkal/100 g |
| Nibbs (diperbarui 16 Okt 2026) | Nasi goreng 550, nasi padang 700, bakso 450, soto ayam 480, mie ayam 460, ayam geprek + nasi 700, bubur ayam 420, es teh manis 100, martabak manis 270, pisang goreng 130 |
| FatSecret via SehatAqua / Halodoc / Beautynesia | Bakwan 137, tahu isi 134, tempe goreng 34, tahu goreng 35 |
| Halodoc | Bakso 350–550 (dipakai 450), mie ayam 400–500 (dipakai 460) |
| Finansialku | Rendang 193/100 g, gulai ayam 250/potong |
| Geraksob tabel kalori | Indomie goreng 390, kwetiau 520, boba 400, kopi susu gula aren 180, es cendol 270, thai tea 220 |
| Dietpartner / Kemenkes AKG 2019 | Target harian pria 19–29 th 2650 kkal, wanita 19–29 th 2250 kkal |
| USDA (standar) | Telur rebus 1 butir ±80 kkal, apel 95 kkal, pisang 105 kkal |

Aplikasi menampilkan disclaimer yang sama di dalam app: resep dan ukuran asli bisa membuat angka berbeda 20–30%.

## Catatan / temuan saat build

- **Makro sengaja tidak ditampilkan.** Tidak ada sumber makro (protein/karbo/lemak) terverifikasi untuk ke-51 item; menampilkan makro karangan akan jadi fabrikasi.
- **Tanpa foto makanan.** Semua visual digambar via CSS/SVG (tile monogram + ikon SVG) — nol aset pihak ketiga, nol risiko IP.
- **Tanpa mode gelap.** Satu dunia visual terang yang konsisten — keputusan desain, bukan kekurangan.
- **Item yang tidak bisa diverifikasi sengaja tidak dimasukkan** (mis. ketoprak, ikan goreng) — katalog hanya berisi item dengan angka yang bisa dipertanggungjawabkan.
- **Tanpa backend** — data statis + localStorage sudah cukup; backend hanya akan jadi beban tanpa manfaat.
