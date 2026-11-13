# Design — KALORIKU!

## Mode & dunia visual

- **Mode (impeccable): Operate** — pengunjung menyelesaikan tugas (mencatat makanan). Scanability dan kecepatan lebih penting dari ekspresi; brand hidup di detail presisi.
- **Dunia visual:** "warteg modern, flat & hangat". Sistem desain dari ui-ux-pro-max (query: *food calorie tracker mobile app warm playful*, dials variance 6 / motion 6 / density 5):
  - Style: Flat Design — 2D, warna berani, tanpa bayangan kompleks, tipografi sebagai bintang.
  - Warna: primer hijau sehat `#059669`, sekunder `#10B981`, aksen/CTA oranye `#EA580C`, latar `#ECFDF5` (mint muda — dihangatkan ke krem-mint `#F3FBF5` pada permukaan halaman), kartu putih `#FFFFFF`, teks `#0F172A`, teks sekunder `#475569`, border `#E1F2ED`, destruktif `#DC2626`.
  - Tipografi: Fredoka (display/angka besar, playful) + Nunito (body). Google Fonts.
  - Motion: stagger list 300–450ms `back.out(1.4)` saat kartu muncul; transisi 150–200ms ease; hormati `prefers-reduced-motion`.
- **Anti-AI-slop (craft-floor):** tanpa gradient text, tanpa kicker/eyebrow di atas heading, tanpa emoji sebagai ikon (pakai SVG inline + tile monogram 2 huruf), tanpa bayangan blok keras, tanpa kartu seragam "ikon + judul + teks" sebagai struktur halaman. Seleksi teks, focus ring, dan scrollbar diwarnai dari palet. Angka memakai tabular-nums.

## Struktur (artifact web statis — pola ARCHITECTURE.md §1)

```
index.html   # struktur + mounting point
styles.css   # token :root → komponen → responsif
app.js       # STATE → DATA → RENDER → EVENTS → INIT (IIFE, satu objek state)
```

Tidak ada backend, tidak ada framework build — satu artifact statis. State ditulis ke keranjang:

| State | Keranjang |
|---|---|
| Query pencarian, filter kategori aktif, tab aktif, pilihan porsi di sheet | Lokal (in-memory) |
| Piring hari ini, riwayat 7 hari, target harian, skor terbaik kuis | localStorage via satu modul `store` |
| Skor/ronde kuis berjalan | Lokal (in-memory) |

## Layout (mobile-first, max-width 480px)

1. **Header:** judul "KALORIKU!" (Fredoka 700) + subjudul satu baris: "Berapa kalori makananmu hari ini?" + tanggal hari ini (Bahasa Indonesia).
2. **Hero cincin:** SVG progress ring (total vs target), angka total besar di tengah (count-up), label "dari target X kkal", sisa/lebih target. Di bawahnya: 4 chip "Setara dengan" (jalan kaki / lari / piring nasi / es teh manis).
3. **Piring Hari Ini:** daftar item (nama, porsi ×, kkal, tombol hapus SVG), total bar, tombol "Kosongkan".
4. **Katalog:** kolom pencarian sticky + chip kategori (Semua, Nasi, Mie & Bakso, Lauk, Gorengan, Jajanan, Minuman, Buah). Kartu makanan: tile monogram warna kategori + nama + satuan porsi + kalori besar + tombol "+ Tambah". Tap tambah → sheet pilihan porsi (0,5×/1×/1,5×/2×) lalu toast "Nasi padang masuk piring!".
5. **Riwayat 7 hari:** grafik batang CSS (7 batang, nilai di atas batang, hari ini hijau penuh).
6. **Tebak Kalori:** kartu kuis — makanan besar, 3 tombol jawaban, feedback benar/salah + penjelasan ("Nasi padang 700 kkal — sepiring ini = 175 menit jalan kaki"), progres ronde 1/5, layar hasil + skor terbaik + "Main Lagi".
7. **Navigasi bawah (sticky):** 3 tab — Piring, Katalog, Tebak. Riwayat tinggal di dalam tab Piring.
8. **Footer disclaimer:** "Angka perkiraan per porsi umum (TKPI Kemenkes, FatSecret, Nibbs, Halodoc). Resep & ukuran asli bisa beda 20–30%."

## Data

51 item, 7 kategori, di `FOODS` (id, nama, kategori, kkal, satuan, porsiLabel). Nilai per proposal.md (sumber tercantum di README). Pengali porsi: 0,5 / 1 / 1,5 / 2.

## Delight (satu momen utama + pendukung)

- **Utama:** cincin progres yang "hidup" — stroke animasi + count-up setiap kali makanan masuk, dan confetti (partikel CSS/JS buatan sendiri, tanpa library) saat target tercapai atau kuis 5/5.
- **Pendukung:** kartu katalog stagger saat filter berubah; toast dengan animasi naik; jawaban kuis benar → kartu hijau berdenyut lembut; jawaban salah → goyang halus + jawaban benar ditandai.

## Kualitas

- Kontras ≥4,5:1; tombol ≥44px; fokus keyboard terlihat; `prefers-reduced-motion` mematikan stagger/confetti.
- Tanpa lorem ipsum; tanpa placeholder palsu; tanpa fungsi mati.
- Verifikasi: jalankan alur SHALL-01 s.d. SHALL-22 secara manual di artifact; cek console bersih; cek 360px tanpa overflow.
