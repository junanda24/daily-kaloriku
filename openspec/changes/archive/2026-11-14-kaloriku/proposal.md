# Proposal — KALORIKU! Hitung Kalori Makanan Indonesia

**Tanggal:** 2026-11-14 · **Slug:** `kaloriku` · **Jenis:** web app (frontend-only, tanpa backend) · **Repo:** `junanda24/daily-kaloriku`

## Apa ini

KALORIKU! adalah pelacak kalori yang ngerti makanan Indonesia. Bukan aplikasi kalori Barat yang isinya salad dan sandwich — di sini ada nasi padang, bakso, mie ayam, gorengan, es teh manis, sampai klepon. Pengguna cari makanan, atur porsi (setengah / satu / satu setengah / dua), masukkan ke "Piring Hari Ini", dan langsung lihat total kalori hari ini lawan target harian (AKG 2019). Ada cincin progres animasi, terjemahan kalori ke aktivitas ("segini = 45 menit jalan kaki"), riwayat 7 hari, dan mode kuis **Tebak Kalori** — tebak berapa kalori sepiring nasi padang, skor tersimpan.

## Kenapa ide ini mengejutkan

- **Sudut pandang yang tidak kepikiran orang:** semua aplikasi kalori besar (MyFitnessPal, FatSecret) datanya Barat dan porsinya gram. Orang Indonesia makan pakai "piring", "mangkok", "potong", "buah" — KALORIKU! memakai satuan itu. Satu piring nasi padang = 700 kkal, satu bakwan = 137 kkal. Datanya nyata, bukan karangan.
- **Efek "wah" bawaan:** hampir semua orang salah tebak kalori makanan sehari-hari (soto ayam 480 kkal terasa "ringan", padahal setara 2 piring nasi). Kuis Tebak Kalori mengubah rasa kaget itu jadi permainan.
- **Berguna tiap hari, bukan sekali pakai:** orang makan 3x sehari; ini alat yang dipakai berulang, dengan riwayat yang bertahan di localStorage.

## Kenapa bentuk ini (web app frontend-only)

- Tidak ada data yang butuh server: 51 makanan + target AKG adalah data statis hasil riset. Semua state (piring, riwayat, profil, skor kuis) hidup di localStorage.
- Harus bisa dibuka di HP dalam 2 detik tanpa install/login — artifact web statis adalah bentuk paling tepat.
- Backend akan jadi beban tanpa manfaat (dilarang pakai backend cuma biar kelihatan canggih).

## Uji bar "receh"

Bukan utilitas satu fungsi. Ini produk dengan 4 fitur yang saling nyambung (katalog + piring harian + riwayat + kuis), state bertahan antar hari, dan alur end-to-end (cari → tambah → capai target → lihat riwayat). Selevel patokan (KOSTKU!/TITIP!), bukan kata-angka/Berani Resign.

## Data — kejujuran angka

Semua angka kalori adalah **perkiraan per porsi umum**, diriset pagi ini dari sumber yang bisa dicek:

- TKPI Kemenkes 2020 — nasi putih 180 kkal/100 g (1 piring 150 g = 270 kkal), nasi merah 149 kkal/100 g
- Nibbs (diperbarui 16 Okt 2026) — nasi goreng 550, nasi padang 700, bakso 450, soto ayam 480, mie ayam 460, ayam geprek + nasi 700, bubur ayam 420, es teh manis 100, martabak manis 270, pisang goreng 130
- FatSecret via SehatAqua/Halodoc/Beautynesia — bakwan 137, tahu isi 134, tempe goreng 34, tahu goreng 35, pisang goreng 68–140 (dipakai 130 dari Nibbs)
- Halodoc — bakso 350–550 (dipakai 450), mie ayam 400–500 (dipakai 460)
- Finansialku — rendang 193/100 g, gulai ayam 250/potong, nasi 200 g = 263 kkal
- Geraksob tabel kalori — indomie goreng 390, kwetiau 520, boba 400, kopi susu gula aren 180, es cendol 270, thai tea 220, sate ayam 400, ayam goreng 260, ayam bakar 200
- Dietpartner/Kemenkes AKG 2019 — target harian pria 19–29 th 2650 kkal, wanita 19–29 th 2250 kkal; gado-gado 295, siomay 361/100 g
- USDA standar — telur rebus 1 butir ±80 kkal, apel 95 kkal, pisang 105 kkal

Aplikasi menampilkan disclaimer jujur di dalam app: "Angka perkiraan per porsi umum — resep & ukuran asli bisa beda 20–30%." Tidak ada angka yang dikarang tanpa sumber; item yang tidak bisa diverifikasi (mis. ketoprak, ikan goreng) sengaja TIDAK dimasukkan.

## Fitur

1. **Katalog 51 makanan** — 7 kategori, pencarian teks, filter kategori, tiap kartu menampilkan kalori/porsi + satuan porsi asli Indonesia.
2. **Piring Hari Ini** — tambah makanan dengan pengali porsi (0,5× / 1× / 1,5× / 2×), hapus item, total kalori berjalan, cincin progres animasi lawan target harian.
3. **Target harian** — preset AKG 2019 (Umum 2000, Wanita 2250, Pria 2650) + slider kustom 1200–3500 kkal, tersimpan.
4. **Setara Dengan** — total kalori diterjemahkan ke menit jalan kaki (≈4 kkal/mnt), menit lari (≈10 kkal/mnt), piring nasi (270 kkal), gelas es teh manis (100 kkal).
5. **Riwayat 7 hari** — total per hari tersimpan otomatis (localStorage), grafik batang CSS, hari ini ter-highlight.
6. **Tebak Kalori (kuis)** — 5 ronde, 3 pilihan jawaban per ronde, skor + skor terbaik tersimpan, streak, confetti saat skor sempurna.
7. **Momen delight** — cincin animasi + count-up, toast saat makanan masuk piring, confetti saat target tercapai / kuis sempurna, kartu makanan beranimasi stagger saat muncul.

## Yang sengaja TIDAK dibuat

- Tanpa makro (protein/karbo/lemak): tidak ada sumber makro terverifikasi untuk ke-51 item; menampilkan makro karangan = fabrikasi.
- Tanpa foto makanan: semua visual digambar via CSS/SVG (tile monogram + ikon SVG), nol aset pihak ketiga, nol risiko IP.
- Tanpa login/sinkronisasi cloud: localStorage cukup; privasi pengguna terjaga.
- Tanpa mode gelap: satu dunia visual terang yang konsisten (keputusan desain, bukan kekurangan).
