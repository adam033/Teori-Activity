# Teori-Activity
## Modul ini berisi teori Activity Android

### Teori Activity <br>
1.	Activity merupakan sebuah komponen di Android yang berfungsi untuk menampilkan user interface ke layar handset Android pengguna. Ini seperti pada saat Anda melihat daftar percakapan pada aplikasi chat atau daftar email pada aplikasi Gmail di ponsel Android Anda. <br>
2.	Umumnya dalam sebuah aplikasi terdapat lebih dari satu activity yang saling terhubung dengan tugas yang berbeda-beda. <br>
3.	Activity merupakan salah satu komponen penting Android yang memiliki daur hidup (life cycle) dalam sebuah stack pada virtual sandbox yang disiapkan oleh Dalvik Virtual Machine (DVM) atau Android Runtime (ART) yang bersifat last in first out. <br>
4.	Pada implementasinya, activity selalu memiliki satu layout user interface dalam bentuk berkas xml. <br>
5.	Suatu aplikasi Android bisa memiliki lebih dari satu activity dan harus terdaftar di berkas AndroidManifest.xml sebagai sub aplikasi. <br>
6.	Sebuah class Java dinyatakan sebuah activity jika mewarisi (extends) superclass Activity atau turunannya seperti AppCompatActivity dan FragmentActivity. <br>


### Activity LifeCycle <br>
![Alt Text](https://github.com/adam033/Teori-Activity/blob/master/Screenshot%20(252).png) <br>
Developer yang baik harus mengetahui secara detail tentang life cycle sebuah activity. Terutama untuk melakukan aksi yang tepat, saat terjadi perubahan state activity. Callback methods yang ada dapat digunakan untuk melakukan beragam proses terkait state dari activity. Misalnya melakukan semua inisialisasi komponen di onCreate(), melakukan disconnect terhadap koneksi ke server pada onStop() atau onDestroy() dan lain sebagainya. <br>
Pemahaman yang baik tentang daur hidup activity akan membuat implementasi rancangan aplikasi Anda menjadi lebih baik. Hal ini juga akan meminimalisir terjadinya error/bug/force close yang tidak diinginkan. <br>


### Last In, First Out (LIFO) <br>
![Alt Text](https://github.com/adam033/Teori-Activity/blob/master/Screenshot%20(253).png) <br>
**Gambar 1** <br>
Jika Anda memiliki sebuah aplikasi yang terdiri dari 2 activity, maka activity pertama akan dijalankan setelah pengguna meluncurkan aplikasi melalui ikon aplikasi di layar device. Activity yang ada saat ini berada pada posisi activity running setelah melalui beberapa state onCreate (created) → onStart (started) → onResume (resumed) dan masuk ke dalam sebuah stack activity. <br>
Bila pada activity pertama Anda menekan sebuah tombol untuk menjalankan activity kedua, maka posisi state dari activity pertama berada pada posisi stop. Saat itu, callback onStop() pada activity pertama akan dipanggil. <br>
Ini terjadi karena activity pertama sudah tidak berada pada layar foreground / tidak lagi ditampilkan. Semua informasi terakhir pada activity pertama akan disimpan secara otomatis. <br>
Sementara itu, activity kedua masuk ke dalam stack dan menjadi activity terakhir yang masuk.<br>
**Gambar 2** <br>
Activity kedua sudah muncul di layar sekarang. Ketika Anda menekan tombol back pada physical button menu utama atau menjalankan metode finish(), maka activity kedua Anda akan dikeluarkan dari stack. <br>
Pada kondisi di atas, state activity kedua akan berada pada destroy. Oleh karenanya, metode onDestroy() akan dipanggil. <br>
Kejadian keluar dan masuk stack pada proses di atas menandakan sebuah model Last In, First Out. Activity kedua menjadi yang terakhir masuk stack (Last In) dan yang paling pertama keluar dari stack (First Out). <br>
**Gambar 3** <br>
Activity pertama akan dimunculkan kembali di layar setelah melalui beberapa state dengan rangkaian callback method yang terpanggil, onStop → onRestart → onStart → onResume. <br>

### Saving Activity State <br>
Ketika sebuah activity mengalami pause kemudian resume, maka state dari sebuah activity tersebut dapat terjaga. Sebabnya, obyek activity masih tersimpan di memory sehingga dapat dikembalikan state-nya. <br>
Dengan menjaga state dari activity, maka ketika activity tersebut ditampilkan, kondisinya akan tetap sama dengan kondisi sebelumnya. <br>
Akan tetapi ketika sistem menghancurkan activity untuk keperluan memori misalnya karena memori habis, maka obyek activity dihancurkan. Alhasil, ketika activity ingin ditampilkan kembali diperlukan proses recreate activity yang dihancurkan tadi. <br>
Kejadian di atas adalah hal yang lumrah terjadi. Oleh karena itu, perubahan yang terjadi pada activity perlu disimpan terlebih dahulu sebelum ia dihancurkan. Di sinilah metode onSaveInstanceState() digunakan. <br>
Dalam onSaveInstanceState terdapat bundle yang dapat digunakan untuk menyimpan informasi. Informasi dapat disimpan dengan memanfaatkan fungsi seperti putString() dan putInt(). <br>
Ketika activity di-restart, bundle akan diberikan kepada metode onCreate dan onRestoreInstanceState. Bundle tersebut akan dimanfaatkan untuk mengembalikan kembali perubahan yang telah terjadi sebelumnya. <br>
![Alt Text](https://github.com/adam033/Teori-Activity/blob/master/Screenshot%20(254).png) <br>
Proses penghancuran activity dapat juga terjadi ketika terdapat perubahan konfigurasi seperti perubahan orientasi layar (portrait-landscape), keyboard availability, dan perubahan bahasa. Penghancuran ini akan menjalankan callback method onDestroy dan kemudian menjalankan onCreate. Penghancuran ini dimaksudkan agar activity dapat menyesuaikan diri dengan konfigurasi baru yang muncul pada kejadian-kejadian sebelumnya. <br>
Hal yang perlu diingat ketika menggunakan onSaveInstanceState adalah untuk tidak menyimpan data yang besar pada bundle. Contohnya, hindari penyimpanan data bitmap pada bundle. Bila data pada bundle berukuran besar, proses serialisasi dan deserialisasi akan memakan banyak memori. <br>












