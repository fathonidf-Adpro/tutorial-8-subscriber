# TUTORIAL 8 ADPRO  (Event Driver Architecture)
#### Daffa Mohamad Fathoni (2206824161)
#### Advanced Programming B / GEN

<hr>

## REFLECTION

>a. what is amqp?
AMQP merupakan singkatan dari Advanced Message Queuing Protocol. 

Ini adalah protokol komunikasi yang digunakan untuk pertukaran pesan antara aplikasi dan layanan dalam arsitektur sistem terdistribusi. AMQP dirancang untuk mendukung berbagai kasus penggunaan, termasuk antara lain antrian pesan, publikasi-langganan, dan pertukaran pesan.

>b. what it means? guest:guest@localhost:5672 , what is the first quest, and what is
the second guest, and what is localhost:5672 is for?

- `guest:guest`: Ini adalah cara untuk menyediakan kredensial login ke server AMQP. Biasanya, guest digunakan sebagai nama pengguna dan kata sandi default. Ini mungkin berbeda di lingkungan produksi yang sebenarnya.
- `localhost:5672`: Ini adalah alamat host dan port yang digunakan untuk terhubung ke server AMQP.
localhost berarti koneksi akan dilakukan ke mesin yang sama di mana program ini dijalankan.
- `5672` adalah nomor port standar untuk server AMQP.

Jadi, `guest:guest@localhost:5672` berarti program akan mencoba terhubung ke server AMQP menggunakan kredensial default (`guest:guest`) pada host yang sama (`localhost`) dan port yang spesifik (`5672`).

## Simulation slow subscriber

![image](https://github.com/fathonidf-Adpro/tutorial-8-publisher/assets/105644250/055f1690-7e81-4de3-97cc-f528f62616cc)

Pada message broker saya terdapat 15 message dalam queue, hal ini karena saya menjalani `cargo run` sebanyak 4 kali secara cepat ditambah dengan adanya `thread::sleep(ten_millis);` pada publisher yang menjadi buffer untuk menunggu setiap thread untuk menerima message, dalam hal ini maka program saya maksimal terdapat 15 message yang mengantri dalam queue tersebut.

## Reflection and Running at least three subscribers

![image](https://github.com/fathonidf-Adpro/tutorial-8-subscriber/assets/105644250/03f54f85-22d9-415d-b7bd-db8c33a2caea)

Dengan menjalankan 3 subscriber yang berbeda dengan terminal berbeda melakukan `cargo run`, dilanjutkan dengan 4 kali `cargo run` pada publisher maka pada grafik queued messages terlihat puncak grafik menurun yang darinya 15 menjadi 7,5. 

#### Kesimpulan:

Dalam konteks event-driven architecture, menjalankan tiga subscriber dapat menghasilkan penanganan pesan yang lebih cepat dibandingkan hanya satu subscriber karena potensi paralelisme yang lebih besar, distribusi yang lebih merata dari beban kerja, dan kemungkinan pengurangan latensi karena setiap subscriber dapat menangani pesan secara independen tanpa harus menunggu pesan sebelumnya selesai ditangani.

1. **Penerbitan Event**: Menggunakan `CrosstownBus::new_queue_publisher` untuk menerbitkan pesan ke antrian dengan topik tertentu ("user_created").
  
2. **Langganan Event**: Menggunakan `CrosstownBus::new_queue_listener` untuk mendengarkan pesan yang diterbitkan ke topik yang sama ("user_created").

3. **Pola Pub/Sub**: Implementasi penerbit (publisher) dan pelanggan (subscriber) mematuhi pola publish/subscribe, di mana pesan diterbitkan ke suatu topik dan pelanggan tertentu yang tertarik dengan topik tersebut akan menerima dan menangani pesan tersebut.

4. **MessageHandler**: Penggunaan `MessageHandler` untuk menangani pesan yang diterima, yang memungkinkan penanganan pesan secara asinkron oleh subscriber yang sesuai dengan topik atau jenis pesan yang diterima.
