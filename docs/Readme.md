1. Text di dalam Row yang overflow: bagian mana dari aturan yang dilanggar, dan oleh widget apa?
- Aturan "constraints go down" dilanggar oleh Row, yang meneruskan constraint lebar tanpa batas ke Text, sehingga teks melaporkan ukuran lebih besar dari ruang yang tersedia dan terjadi overflow. Solusinya adalah membungkus Text dengan Expanded atau Flexible.
2. Mengapa menambahkan width: 150 pada teks adalah perbaikan yang salah, walaupun stripes-nya hilang?
- Menambahkan width: 150 hanya menutupi gejala dengan angka tebakan yang tidak mengikuti constraint parent. Layout akan tetap bermasalah di layar yang berbeda, saat font diperbesar, atau saat teks berubah panjang.
3. Landscape diperbaiki dengan SingleChildScrollView dan shrinkWrap: true pada list. Test mana yang gagal, dan mengapa ini penting saat data berasal dari API?
- Test yang gagal adalah test dengan data banyak, karena shrinkWrap: true di dalam SingleChildScrollView memaksa semua item dibangun sekaligus dan menghilangkan lazy building. Saat data berasal dari API dengan jumlah yang tidak terduga, hal ini menyebabkan jank dan pemakaian memori tinggi.
4. Mengapa layout tablet memakai LayoutBuilder, bukan MediaQuery.sizeOf(context)?
- LayoutBuilder dipakai karena memberi tahu ruang yang benar-benar tersedia bagi widget, sedangkan MediaQuery.sizeOf(context) hanya memberi ukuran seluruh layar. Dengan begitu layout tetap tepat saat widget berada di panel, dialog, atau split-screen.
5. Crash saat data kosong bukan error layout. Mengapa tetap relevan dalam layout lab?
- Crash data kosong tetap relevan karena layout yang baik harus tahan terhadap semua kondisi data, bukan hanya kondisi ideal. Menangani empty state termasuk bagian dari UI yang kokoh dan sering terlewat saat struktur widget diubah.