# Spec — KALORIKU! (kaloriku)

## Capability: katalog makanan Indonesia

- **SHALL-01** Aplikasi menampilkan katalog minimal 50 makanan Indonesia dengan nama, kategori, satuan porsi (piring/mangkok/potong/buah/gelas/porsi), dan kalori per porsi.
  - WHEN aplikasi dibuka THEN katalog menampilkan semua item, dikelompokkan dalam 7 kategori: Nasi, Mie & Bakso, Lauk, Gorengan, Jajanan, Minuman, Buah.
- **SHALL-02** Pengguna dapat mencari makanan berdasarkan nama.
  - WHEN pengguna mengetik di kolom pencarian THEN daftar langsung menyaring item yang namanya mengandung kata kunci (case-insensitive), tanpa perlu menekan tombol.
- **SHALL-03** Pengguna dapat memfilter katalog per kategori.
  - WHEN pengguna memilih satu kategori THEN hanya item kategori itu yang tampil; WHEN memilih "Semua" THEN semua item tampil.
- **SHALL-04** Setiap nilai kalori disertai konteks kejujuran data.
  - WHEN pengguna melihat katalog atau footer aplikasi THEN ada teks yang menyatakan angka adalah perkiraan per porsi umum dan bisa berbeda tergantung resep/ukuran.

## Capability: piring hari ini

- **SHALL-05** Pengguna dapat menambahkan makanan ke Piring Hari Ini dengan pengali porsi 0,5× / 1× / 1,5× / 2×.
  - WHEN pengguna mengetuk tombol tambah pada kartu makanan THEN muncul pilihan porsi; WHEN porsi dipilih THEN item masuk ke piring dengan kalori = kalori dasar × pengali (dibulatkan ke bilangan bulat).
- **SHALL-06** Piring Hari Ini menampilkan daftar item hari ini beserta total kalori berjalan.
  - WHEN item ditambah/dihapus THEN total kalori diperbarui seketika dan ditampilkan dengan animasi count-up.
- **SHALL-07** Pengguna dapat menghapus satu item dari piring atau mengosongkan seluruh piring.
  - WHEN pengguna mengetuk hapus pada item THEN item itu hilang dan total berkurang; WHEN pengguna mengetuk "Kosongkan" THEN semua item hilang setelah konfirmasi.
- **SHALL-08** Isi piring bertahan antar sesi dan berganti hari otomatis.
  - WHEN aplikasi ditutup lalu dibuka lagi di hari yang sama THEN isi piring tetap ada; WHEN dibuka di hari berbeda THEN piring hari kemarin dipindahkan ke riwayat dan piring hari ini mulai kosong.
- **SHALL-09** Cincin progres menampilkan persentase target harian yang tercapai.
  - WHEN total berubah THEN cincin terisi sesuai total/target dengan animasi; WHEN total ≥ target THEN cincin penuh, tampil pesan target tercapai, dan confetti muncul sekali untuk hari itu.

## Capability: target harian

- **SHALL-10** Pengguna dapat memilih target harian dari preset AKG 2019 (Umum 2000, Wanita 2250, Pria 2650 kkal) atau mengatur sendiri via slider 1200–3500 kkal.
  - WHEN preset/slider diubah THEN target baru langsung dipakai cincin dan tersimpan.
- **SHALL-11** Target tersimpan antar sesi.
  - WHEN aplikasi dibuka kembali THEN target terakhir yang dipilih tetap dipakai.

## Capability: setara dengan (penerjemah kalori)

- **SHALL-12** Total kalori hari ini diterjemahkan ke aktivitas dan porsi pembanding.
  - WHEN total > 0 THEN tampil: menit jalan kaki (≈4 kkal/menit), menit lari (≈10 kkal/menit), jumlah piring nasi (270 kkal), jumlah gelas es teh manis (100 kkal); WHEN total = 0 THEN bagian ini menampilkan ajakan untuk mulai menambah makanan.

## Capability: riwayat 7 hari

- **SHALL-13** Total kalori tiap hari tersimpan dan ditampilkan sebagai grafik batang 7 hari terakhir.
  - WHEN hari berganti THEN total hari kemarin tersimpan; WHEN pengguna membuka riwayat THEN 7 batang tampil dengan label hari (Sen/Sel/...) dan nilai kkal, hari ini ter-highlight.

## Capability: kuis Tebak Kalori

- **SHALL-14** Kuis terdiri dari 5 ronde; tiap ronde menampilkan satu makanan dan 3 pilihan kalori.
  - WHEN kuis dimulai THEN 5 makanan dipilih acak tanpa pengulangan; WHEN pengguna menjawab THEN jawaban benar/salah langsung ditandai dan jawaban benar ditampilkan.
- **SHALL-15** Skor dihitung dan skor terbaik tersimpan.
  - WHEN kuis selesai THEN tampil skor (x/5) + pesan sesuai skor; WHEN skor melebihi skor terbaik THEN skor terbaik diperbarui dan tersimpan di localStorage.
- **SHALL-16** Kuis dapat dimainkan ulang dan dibatalkan.
  - WHEN pengguna mengetuk "Main Lagi" THEN kuis baru dimulai dengan 5 makanan acak baru; WHEN pengguna keluar di tengah kuis THEN kembali ke layar awal kuis tanpa menyimpan skor.
- **SHALL-17** Skor sempurna memicu confetti.
  - WHEN skor 5/5 THEN confetti tampil dan pesan khusus muncul.

## Capability: kualitas umum

- **SHALL-18** Aplikasi mobile-first, lebar maksimal 480px, tanpa scroll horizontal di lebar 360px.
  - WHEN dibuka di HP (360–480px) THEN semua konten terbaca, tombol sentuh minimal 44×44px, dan navigasi bawah dapat dipakai satu tangan.
- **SHALL-19** Semua kontrol berfungsi; tidak ada tombol mati, teks placeholder, atau lorem ipsum.
  - WHEN setiap tombol/interaksi diuji THEN ada respons yang terlihat (state berubah / toast / navigasi).
- **SHALL-20** Copy Bahasa Indonesia natural, tanpa emoji pada label UI.
  - WHEN seluruh layar dibaca THEN tidak ada emoji yang dipakai sebagai ikon/label; ikon berupa SVG atau tile monogram huruf.
- **SHALL-21** Aksesibilitas dasar terpenuhi.
  - WHEN diperiksa THEN kontras teks ≥4,5:1, tombol punya label yang bisa dibaca screen reader, fokus keyboard terlihat, dan `prefers-reduced-motion` menonaktifkan animasi non-esensial.
- **SHALL-22** Tidak ada error console saat alur utama dijalankan (buka → cari → tambah → hapus → kuis → restart).
