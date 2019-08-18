# belajarMongo
Resume Hasil Belajar NodeJS (Pribadi). biar gk lupa 😎

## Sedikit Catatan

**MongoDB** adalah database yang berorientasi pada dokumen atau *document oriented database*. MongoDB disebut sebagai document oriented database karena cara kerja nya dalam menyimpan data. dalam MongoDB, data akan disimpan dalam sebuah collection, dimana setiap data tersebut disebut sebagai document.

**MongoDB** masuk dalam keluarga **noSQL**

MongoDB menyimpan data benbentuk **JSON** ke dalam storage dengan bentuk **BSON**  (Binary). jadi setiap operasi pada MongoDB, akan banyak menggunakan **JSON**

## Instalasi

Silahkan lihat tahap2 di [link](https://docs.mongodb.com/manual/installation/) ini

ketika MongoDB terinstall, akan ada beberapa program mongo yang dapat dieksekusi. namun yang umum digunakan adalah dua yaitu mongo dan mongod

**mongo** adalah database client dari MongoDB. program ini digunakan untuk melakukan operasi terhadap database, collection dll. simpelnya, disini kita melakukan querynya

**mongod** adalah program untuk menjalankan mongodb itu sendiri. program mongo tidak akan bisa dijalankan jika tidak ada service mongoDB yang berjalan.

## Menjalankan

### mongod

terdapat beberapa cara menjalankan yaitu :

#### Sebagai Service

untuk menjalankan MongoDB sebagai service yang perlu dilakukan adalah cukup dengan perintah standar `systemctl` ataupun `service`

berikut perintahnya 

`sudo systemctl start mongod.service`

#### Manual

untuk menjalankan MongoDB secara manual, anda dapat menggunakan perintah yang sudah disediakan MongoDB yaitu mongod

1. Buat folder untuk menyimpan file database. contoh `mkdir ~/mongo-data/`  

2. Jalankan perintah mongod dan arahkan dbpath ke folder yang telah dibuat. ketik diterminal `sudo mongod --dbpath ~/mongo-data` 

kita juga bisa mengatur port jika ingin tidak ingin menggunakan port standar. cukup berikan argumen --port dengan valuenya. contoh `mongod --dbpath ~/mongo-data --port 12880`

### mongo

untuk menjalankan MongoDB client, cukup ketik perintah `mongo`. pastikan mongod telah berjalan

## Perintah & Query

Untuk menjalankan perintah & query, pastikan ada sudah berada dalam program client dari MongoDB / mongo. jika belum, jalankan perintah mongod, lalu jalankan program mongo.

#### Membuat Database

untuk membuat database, gunakan perintah `use`. perintah use berisikan 1 argumen yaitu nama database

contoh perintah membuat database *book*

`use book` 

#### Melihat Databases

untuk melihat database, gunakan perintah `show dbs`

ketika pertama kali menjalankan perintah `show dbs` akan terdapat 3 database. 3 database tersebut adalah database standard di mongodb 

**Menghapus Database**

untuk menghapus **Database**, gunakan perintah `db.dropDatabse()`. pastikan anda telah memilih database sebelum menghapus database.

untuk mengecek database yang terpilih, cukup ketikan perintah `db`

