# belajarMongo

📝 Resume Hasil Belajar NodeJS (Pribadi). biar gk lupa 😎

## Sedikit Catatan

**MongoDB** adalah database yang berorientasi pada dokumen atau *document oriented database*. MongoDB disebut sebagai document oriented database karena cara kerja nya dalam menyimpan data. dalam MongoDB, data akan disimpan dalam sebuah collection, dimana setiap data tersebut disebut sebagai document.

**MongoDB** masuk dalam keluarga **noSQL**

MongoDB menyimpan data benbentuk **JSON** ke dalam storage dengan bentuk **BSON**  (Binary). jadi setiap operasi pada MongoDB, akan banyak menggunakan **JSON**

**Perhatian**

Penulisan perintah dalam repo ini menggunakan beberapa tanda yang ditampilkan hanya sebagai pendukung untuk memudahkan pembaca. tanda yang digunakan adalah > dan $. kedua tanda tersebut tidak perlu di copy

### Instalasi

Silahkan lihat tahap2 di [link](https://docs.mongodb.com/manual/installation/) ini

ketika MongoDB terinstall, akan ada beberapa program mongo yang dapat dieksekusi. namun yang umum digunakan adalah dua yaitu mongo dan mongod

**mongo** adalah database client dari MongoDB. program ini digunakan untuk melakukan operasi terhadap database, collection dll. simpelnya, disini kita melakukan querynya

**mongod** adalah program untuk menjalankan mongodb itu sendiri. program mongo tidak akan bisa dijalankan jika tidak ada service mongoDB yang berjalan.

### Menjalankan

###### mongod

terdapat beberapa cara menjalankan yaitu :

Sebagai Service

untuk menjalankan MongoDB sebagai service yang perlu dilakukan adalah cukup dengan perintah standar `systemctl` ataupun `service`

berikut perintahnya 

```
$ sudo systemctl start mongod.service
```

Manual

untuk menjalankan MongoDB secara manual, anda dapat menggunakan perintah yang sudah disediakan MongoDB yaitu mongod

1. Buat folder untuk menyimpan file database. contoh `mkdir ~/mongo-data/`  

2. Jalankan perintah mongod dan arahkan dbpath ke folder yang telah dibuat. ketik diterminal `sudo mongod --dbpath ~/mongo-data` 

kita juga bisa mengatur port jika ingin tidak ingin menggunakan port standar. cukup berikan argumen --port dengan valuenya. contoh `mongod --dbpath ~/mongo-data --port 12880`

###### mongo

untuk menjalankan MongoDB client, cukup ketik perintah 

```
$ mongo
```

pastikan mongod telah berjalan

### Perintah & Query

Untuk menjalankan perintah & query, pastikan ada sudah berada dalam program client dari MongoDB / mongo. jika belum, jalankan perintah mongod, lalu jalankan program mongo.

###### Membuat Database

untuk membuat database, gunakan perintah `use`. perintah use berisikan 1 argumen yaitu nama database

contoh perintah membuat database *book*

```
> use book
```

###### Menampilkan Databases

untuk melihat database, gunakan perintah 

```
> show dbs
```

ketika pertama kali menjalankan perintah `show dbs` akan terdapat 3 database. 3 database tersebut adalah database standard di mongodb 

###### **Menghapus Database**

untuk menghapus **Database**, gunakan perintah 

```
> db.dropDatabse()
```

pastikan anda telah memilih database sebelum menghapus database.

untuk mengecek database yang terpilih, cukup ketikan perintah `db`

##### Mengubah Database

sampai saat ini belum ada cara mengubah nama database secara official dari mongodbnya. untuk mengubah nama, diperlukan cara2 tricky

##### Membuat Collection

untuk membuat collection gunakan perintah

```
> db.createCollection('namacollection')
```

atau bisa juga dengan langsung menuliskan query untuk menginput document. mongo akan otomatis membuat collection tersebut

```
> db.namacollection.insertOne({judul: "judul"})
```

##### Menampilkan Collection

untuk melihat database, gunakan perintah

```
> show collections
```

##### Mengubah Collection

untuk mengubah nama collection, gunakan perintah

```
> db.namaCollection.renameCollection(namaBaruCollection)
```

##### Menghapus Collection

untuk mengubah nama collection, gunakan perintah

```
> db.namaCollection.drop()
```

##### Membuat Dokumen

untuk membuat / menambahkan dokumen bisa menggunakan 3 cara yaitu

**insertOne**

insertOne digunakan untuk menambahkan satu dokumen kedalam collection.

insertOne menerima data dokumen berbentuk objek atau json

```
> db.namaCollection.insertOne({contohKey: "contohValue""})
```

perintah diatas akan mengembalikan respon kurang lebih seperti dibawah 

```
{ "_id" : ObjectId("5d59dfa3f0650355d96637bc"), "contohKey" : "contohValue" }
```

valu dari _id adalah value yang digenerate otomatis oleh mongoDB. _id adalah pembeda dari masing2 dokumen, layaknya primary key dalam SQL

**insertMany**

insertMany digunakan untuk menambahkan dokumen dengan jumlah lebih dari 1

insertMany menerima data dokumen berupa list atau array dari beberapa/banyak dokumen

```
> db.namaCollection.insertMany([{contohKey: "contohValue"}, {contohKey2: "contohValue2"}])
```

perintah diatas akan menghasilkan respon kurang lebih seperti dibawah

```
{
    "acknowledged" : true,
    "insertedIds" : [
        ObjectId("5d59e39df0650355d96637c0"),
        ObjectId("5d59e39df0650355d96637c1")
    ]
}
```

**insert**

insert adalah kombinasi dari insertOne dan insertMany, insert menerima data dokumen berupa object ataupun list/array

```
db.namaCollection.insertMany([{contohKey: "contohValue"}, {contohKey2: "contohValue2"}])
```

respon yang dihasilkan oleh perintah insert berbeda dengan insertOne dan insertMany. insert akan mengembalikan response berupa writeResult dan bulkWriteResult. respon dari insert kurang lebih seperti dibawah

```
BulkWriteResult({
    "writeErrors" : [ ],
    "writeConcernErrors" : [ ],
    "nInserted" : 2,
    "nUpserted" : 0,
    "nMatched" : 0,
    "nModified" : 0,
    "nRemoved" : 0,
    "upserted" : [ ]
})
```

##### Membaca Dokumen

untuk membaca dokumen, kita bisa menggunakan 2 cara yaitu

**find**

find adalah perintah standar untuk menampilkan dokumen. find akan mengembalikan response dalam bentuk list/array

- Menampilkan Semua Data
  
  ```
  > db.namaCollection.find() 
  atau 
  > db.namaCollection.find({})
  ```

- Menampilkan Data dengan Query
  ```
  > db.namaCollection.find({nama: "budi"})
  ```
  perintah diatas digunakan untuk menampilkan semua dokumen yang memiliki attibut nama dengan value budi


**findOne**

find digunakan untuk menampilkan 1 dokumen. apabila terdapat lebih dari satu dokumen yang sama, maka findOne akan mengembalikan hasil pertama

 ```
  > db.namaCollection.findOne() 
  atau
  > db.namaCollection.findOne({nama: "budi"}) // dengan query
  ```
  
##### Mengubah Dokumen
untuk mengubah dokumen, kita bisa menggunakan 3 cara yaitu updateOne, updateMany dan update.
semua perintah tersebut membutuhkan minimal 2 argument/parameter yaitu :
- query untuk menentukan yang akan diubah
- data baru untuk menggantikan data lama

**updateOne**

updateOne digunakan untuk mengupdate 1 dokumen. 
```
> db.namaCollection.updateOne({query}, {$set: dataBaru})
contoh
> db.namaCollection.updateOne({nama: "budi"}, {$set: {nama: "andi"}})
```
contoh perintah diatas jika eksekusi maka akan mengubah 1 data pertama yang memiliki `nama` budi, dan mengubah `nama` menjadi andi

**updateMany**

updateMany digunakan untuk mengupdate semua dokumen yang sesuai dengan query. 
```
> db.namaCollection.updateMany({nama: "budi"}, {$set: {nama: "andi"}})
```
contoh perintah diatas jika eksekusi maka akan mengubah semua data yang memiliki `nama` budi, dan mengubah `nama` menjadi andi

**update**

update digunakan untuk mengupdate dokumen yang sesuai dengan query. perintah update dapat mengupdate satu maupun banyak dokumen. update juga dapat digunakan untuk melakukan operasi replace. untuk melakukan operasi update, diperlukan 3 parameter/argumen yaitu
- `query` untuk mengfilter dokumen mana yang perlu diubah
- `databaru` sebagai data untuk mengganti data lama
- `options` untuk menentukan operasi mana yang ingin dilakukan terhadap dokumen
```
> db.namaCollection.update() !! COMING SOON
```

##### Menghapus Dokumen
untuk menghapus dokumen, kita bisa menggunakan 2 cara yaitu deleteOne, deleteMany.

**deleteOne**
deleteOne digunakan untuk menghapus 1 dokumen. 
```
> db.namaCollection.deleteOne({query})
contoh
> db.namaCollection.deleteOne({nama: "budi"})
```
perintah diatas akan menghapus 1 dokumen yang memiliki attribut `nama` dengan `value` budi.

**deleteMany**
deleteMany digunakan untuk menghapus beberapa/banyak dokumen. 
```
> db.namaCollection.deleteMany({query})
contoh
> db.namaCollection.deleteMany({nama: "budi"})
```
perintah diatas akan menghapus semua dokumen yang memiliki attribut `nama` dengan `value` budi.

**Tambahan**

untuk menghapus berdasarkan _id dokumen, diperlukan sedikit tambahan yaitu seperti berikut

```
>  db.namaCollection.deleteMany({ _id: ObjectId(_idDariDokumen)})
```
seperti pada contoh diatas, diperlukan bagi pengguna untuk menambahkan ObjectId pada _id dari dokumen

##### Kursor / Cursor
Coming Soon

##### - / Embedded Document
Coming Soon

##### Operator
Coming Soon

##### Skema / Schema
Coming Soon
