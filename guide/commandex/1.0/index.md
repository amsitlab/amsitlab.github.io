Commandex Guide
===============


# List

* [Pembuka](#pembuka)
* [Instalasi](#instalasi)
* [Penggunaan](#penggunaan)
* [Tutorial](#tutorial)


# Pembuka
**commandex** adalah tools untuk membuat aplikasi commandline dengan java code.
Untuk saat ini **commandex** hanya dapat berjalan di [Termux](https://termux.net) environment.
Commandex hadir untuk memudahkan membuat commandline dengan java code di termux, tanpa harus repot memanggil command **ecj** dan **dx** setting classpath, membuat bashshortcuts commandex melakukan itu semua untuk anda.
Commandex memberikan pilihan untuk anda yaitu
1. Pure tanpa plugin commandline parsing.
2. Menggunakan [Picocli](https://picocli.info) sebagai plugin commandline parsing.
Saya rekomendasikan menggunakan pilihan ke 2, karna ini mudahkan developer membuat aplikasi tanpa perlu pusing dengan command line parsing.


# Instalasi

Jika anda sudah menambakan [amsitlab repo](https://amsitlab.github.io/amsitlab-repo) anda bisa meng-install dengan mengetik:

```bash
apt install commandex
```

Namun, jika belum meng-aktifkan repo [amsitlab repo](https://amsitlab.github.io/amsitlab-repo) anda bisa meng-install commandex dengan command di bawah:

```bash
curl -LO "https://amsitlab.github.io/dists/termux/amsitlab/binary-all/commandex_1.0_all.deb" && \
apt install -y ./commandex_1.0_all.deb
```

# Penggunaan
**commandex** terbagi menjadi 4 command.
setiap command memiliki fungsi masing-masing.
1. **commandex new**
> Command ini berfungsi membuat project baru.
>
> Membuatkan anda directory untuk bekerja.
> Defaultnya commandex membuatkan workspace directory
> didalam folder **~/workspace/java/**, namun anda bisa
> merubahnya dengan men-set variable **$CMDX****_****WORKSPACE**.

2. **commandex compile**
> Command ini berfungsi untuk meng-compile file java menjadi javabytecode.
> 
> Command ini memnghasilkan kumpulan file _.class_ di
> dalam direcrory _~/workspace/java/nama-projek/classes_ .

3. **commandex jar**
> Command ini berfungsi untuk men-traslate java bytecode
> ke dalvik executable agar bisa berjalan di [dalvikvm](https://id.m.wikipedia.org/wiki/Dalvik_(perangkat_lunak))
> lalu mem-pack menjadi sebuah file .jar.
> command ini juga membuatkan anda _bash_ _shortcuts_ agar
> aplikasi dapat di panggil dengan command yang simple.

4. **commandex config**
> Command ini berfungsi untuk meng-edit default project config
> yang di definisikan di file _.config.proj_ .
> command ini menggunakan [vim](https://www.vim.org) sebagai default editor, namun anda bisa merubahnya dengan
> merubah value dari variable **$EDITOR**


# Tutorial
Untuk tutorial saya buat artikel terpisah di halaman [ini](https://amsitlab.github.io/guide/commandex/1.0/tutorial.md) .
