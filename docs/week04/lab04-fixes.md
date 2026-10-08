# Lab 04 Fix Log

| Widget | Error / symptom | Rule broken | Fix |
|---|---|---|---|
| StoreHeader | overflow di kanan pada 320 dp | Row memberi Column lebar tak terbatas, tidak ada yang mengalah | Expanded + maxLines + ellipsis, rating dipindah ke dalam Column |
| CategoryBar | 6 chip lebih lebar dari layar, overflow di kanan | Sizes go up: total lebar anak melebihi constraint parent | SingleChildScrollView horizontal |
| PromoStrip / PromoCard | dua kartu 200 dp + padding melebihi 320 dp, tinggi 150 dp tetap | Ukuran dipaksa, bukan mengikuti constraint | Strip scroll horizontal, tinggi mengikuti isi (IntrinsicHeight), maxLines pada teks |
| PromoStrip | RangeError saat zero items (promos[0], promos[1]) | Kode mengira data selalu ada | take(2) dan SizedBox.shrink() jika kosong |
| MenuTile | nama panjang mendorong harga keluar layar | Row dengan Column tanpa Expanded | Expanded + maxLines: 2 + ellipsis |
| MenuTile | teks harga dan 'Promo' tanpa batas (font test lebar) | Teks tanpa strategi overflow | maxLines: 1 + ellipsis + softWrap: false |
| MenuScreen | overflow bawah saat landscape dan keyboard terbuka | Column berisi anak tinggi tetap + Expanded, konten lebih tinggi dari sisa ruang | Satu CustomScrollView dengan sliver |
| MenuScreen | 500 item dibangun sekaligus | List yang panjangnya tak terkontrol harus lazy | SliverList.builder dan SliverGrid.builder |
| MenuScreen | 4 kolom tetap membuat kartu sempit di 600 dp | Jumlah kolom dipatok, bukan mengikuti lebar | SliverGridDelegateWithMaxCrossAxisExtent |
| MenuScreen | breakpoint memakai MediaQuery dan `> 600` | Layout harus mengikuti constraint dari parent | LayoutBuilder dan `constraints.maxWidth >= 600` |
| MenuCard | gambar 110 dp tetap, isi kartu overflow di bawah | Sizes go up: isi lebih tinggi dari kartu | Expanded pada area gambar |
| MenuScreen | zero items menampilkan area kosong | Tidak ada empty state | EmptyState ber-Key('empty-state'): ikon, pesan, aksi |
| CartBar | tinggi 72 dan tombol 160 tetap, teks overflow | Constraint kaku | minHeight, Expanded + maxLines pada teks, tombol selebar kontennya |
| CartBar | tombol tertutup gesture bar | Parent sets position: konten tidak dijauhkan dari area sistem | Material di luar, SafeArea (top: false) di dalam |