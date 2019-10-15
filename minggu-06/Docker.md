#Pertemuan 06 Docker

Docker adalah sebuah project open source yang ditujukan untuk developer atau sysadmin untuk membangun, mengemas dan menjalankan aplikasi dimana pun di dalam sebuah container.


##Langkah 1
##Menjalankan Docker Kontainer
Docker container berjalan berdasarkan Docker Image. Docker Image ini berisi tentang semua kebutuhan untuk menjalankan sebuah proses. Ada beberapa docker image yang sudah tersedia di Docker Registry atau jalankan perintah docker search nama-docker-image. Contoh kasus docker image redis. Perintah docker search <name> ini berfungsi untuk mencari apakah docker image yang diinginkan sudah tersedia di Docker Registry atau belum.
![00](gambar/1.PNG)

Secara default docker akan menjalankan kontainer di foreground. Untuk menjalankan container secara background gunakan opsi -d. Perintahnya seperti berikut : docker run -d redis
![01](gambar/2.PNG)
Perintah di atas akan menghasilkan output berupa container ID seperti yang ada di dalam gambar diatas. Secara default docker akan menjalankan container (docker image) versi terakhir. Jika ingin menjalankan docker image versi tertentu sertakan versi dari docker image yang ada, dengan perintah docker run -d redis:3.2. Berdasarkan perintah ini, Docker CLI akan me-download docker image redis versi 3.2 jika image yang dimaksud belum ada di local.

##Langkah 2
##Mencari kontainer yang berjalan
Kontainer yang sudah dijalankan menggunakan opsi -d akan berjalan di background, untuk memastikan kontainer yang berjalan sesuai dengan yang diinginkan gunakan perintah docker ps, perintah ini digunakan untuk menampilkan daftar semua kontainer yang berjalan di local komputer. Dari perintah ini kita bisa mendapatkan Container ID dan Nama Container yang sedang berjalan, seperti pada gambar dibawah ini.
![02](gambar/3.PNG)

##Langkah 3
##Accessing Redis
Sebuah docker container yang berjalan tidak akan bisa di akses oleh host computer jika port dari container tidak di expose. Perintah untuk me-expose port dari docker container supaya bisa di akses dari host computer adalah docker run -d --name redisHostPort -p 6379:6379 redis:lates.
![03](gambar/4.PNG)

##Langkah 4
##Accessing Redis
Permasalahan ketika menjalankan docker pada port yang fixed adalah kita tidak bisa menjalankan beberapa instance secara bersamaan. Untuk menjalankan beberapa instance secara bersamaan jalankan perintah docker run -d --name redisDynamic -p 6379 redis:latest abaikan host port, dengan cara ini docker akan me-assign host port secara otomatis, akan mencarai port yang tersedia untuk mem-binding port 6379 milik container redis dengan port yang tersedia milik host.
![04](gambar/5.PNG)

Untuk mengetahui container berjalan di port mana gunakan perintah docker port redisDynamic 6379
![05](gambar/6.PNG)

Selain menggunakan perintah di atas, docker ps juga bisa digunakan untuk melihat port mapping dari contaniner yang sedang berjalan.
![06](gambar/7.PNG)

##Langkah 5
##Persisting Data
Data yang ada di dalam container docker akan ikut hilang jika container yang ada dihapus atau container di buat baru. Untuk menghindari kehilangan data, docker CLI ada opsi untuk binding volumes yaitu mount volume local ke dalam volume container dengan menyertakan opsi -v <host-dir>:<container-dir>. Dengan opsi ini semua yang ada di mounted-volume akan sama dengan yang ada di dalam container, jika container di hapus atau di buat ulang, data akan tetap tersimpan di volume local.
![07](gambar/8.PNG)

##Langkah 6
##Running A Container In The Foreground
Pada langkah-langkah sebelumnya, perintah docker yang dijalankan menyertakan opsi -d yang mana container berjalan di background, jika ingin menjalankan container secara foreground hilangkan opsi -d, dengan begitu kita bisa berinteraksi dengan container. Contoh menggunakan perintah ps milik OS Ubuntu, untuk menampilkan proses yang berjalan di dalam container ubuntu.
![08](gambar/9.PNG)

Untuk bisa berintaksi dengan bash shell milik ubuntu sertakan opsi -it, dengan opsi ini container akan berjalan dan kita bisa meng-akses bash shell docker run -it ubuntu bash
![09](gambar/10.PNG)
