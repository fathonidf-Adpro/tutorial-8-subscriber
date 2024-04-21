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