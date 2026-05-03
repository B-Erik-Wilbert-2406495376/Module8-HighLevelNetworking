# REFLECTION

1. Dalam gRPC, metode unary melibatkan satu permintaan dan satu respons sehingga sesuai untuk operasi sederhana seperti pengambilan atau pengiriman data tunggal. Server streaming memungkinkan satu permintaan menghasilkan aliran respons secara bertahap, yang cocok untuk pengiriman data dalam jumlah besar atau berkelanjutan. Sementara itu, bidirectional streaming memungkinkan klien dan server saling bertukar pesan secara simultan, sehingga lebih tepat digunakan pada skenario komunikasi real-time seperti aplikasi percakapan.

2. Implementasi layanan gRPC di Rust perlu memperhatikan aspek keamanan seperti autentikasi untuk memastikan identitas pengguna, otorisasi untuk membatasi hak akses, serta enkripsi data menggunakan TLS. Tanpa mekanisme tersebut, sistem berisiko terhadap serangan seperti pencurian data atau akses tidak sah.

3. Penanganan bidirectional streaming dalam Rust gRPC memiliki beberapa tantangan, seperti pengelolaan proses asynchronous yang kompleks, potensi terjadinya deadlock, serta kebutuhan sinkronisasi data antar klien. Pada aplikasi seperti chat, kestabilan koneksi dan kemampuan menangani banyak pesan secara bersamaan menjadi faktor yang perlu diperhatikan.

4. Penggunaan `tokio_stream::wrappers::ReceiverStream` memberikan kemudahan dalam mengubah channel asynchronous menjadi stream yang dapat digunakan dalam gRPC, sehingga implementasi menjadi lebih sederhana. Namun, pendekatan ini memiliki keterbatasan dalam hal kontrol terhadap performa dan pengelolaan buffer, terutama jika digunakan dalam sistem dengan beban tinggi.

5. Struktur kode gRPC di Rust dapat dibuat lebih modular dengan memisahkan definisi layanan, logika bisnis, dan akses data ke dalam komponen yang berbeda. Penggunaan trait dan pemisahan file `.proto` dari implementasi juga membantu meningkatkan keterbacaan, kemudahan pengujian, serta mempermudah pengembangan lebih lanjut.

6. Pada implementasi `MyPaymentService`, diperlukan langkah tambahan seperti validasi data permintaan, integrasi dengan sistem penyimpanan, serta penanganan kesalahan yang lebih lainnya. Selain itu, mekanisme logging dan pengelolaan transaksi juga penting untuk menjaga konsistensi proses pembayaran.

7. Penggunaan gRPC dalam sistem terdistribusi mendorong pendekatan berbasis kontrak melalui definisi skema yang jelas, sehingga komunikasi antar layanan menjadi lebih terstruktur dan efisien. Namun, pendekatan ini dapat mengurangi fleksibilitas dan memerlukan penyesuaian tambahan.

8. HTTP/2 sebagai protokol dasar gRPC menawarkan keunggulan seperti multiplexing dan efisiensi penggunaan koneksi dibandingkan HTTP/1.1. Meskipun demikian, kompleksitas implementasi dan keterbatasan dukungan di beberapa lingkungan dapat menjadi kendala, sehingga dalam beberapa kasus pendekatan berbasis HTTP/1.1 atau WebSocket masih digunakan.

9. Model request-response pada REST bersifat sederhana dan stateless, sehingga cocok untuk komunikasi yang tidak memerlukan interaksi berkelanjutan. Sebaliknya, gRPC mendukung streaming dua arah yang memungkinkan komunikasi real-time, sehingga lebih responsif untuk aplikasi yang membutuhkan pertukaran data secara terus-menerus.

10. Pendekatan berbasis skema pada gRPC dengan Protocol Buffers memberikan keuntungan berupa ukuran data yang lebih kecil, performa yang lebih tinggi, serta validasi struktur data yang lebih ketat. Namun, pendekatan ini kurang fleksibel dibandingkan JSON pada REST, yang lebih mudah dimodifikasi tanpa perlu regenerasi kode.
