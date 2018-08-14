Menjalankan Java Di Termux
==========================
[English]()

# Daftar Kontent
- [Apa itu dalvikvm ?](#apa-itu-dalvikvm)
- [Kompilasi java Di Termux](#kompilasi-java-di-termux)
- [Membuat File Dex](#membuat-file-dex)
- [Menjalakan](#menjalankan)
- [Penutup](#penutup)

## Apa itu dalvikvm
Dalvikvm adalah Virual Mesin yang menjalankan program java di platform android, melalui kompilasi ulang dari file _*.class_ yg di targetkan untuk Jvm[TM] .

Cara kerjanya adalah:
> Ibaratkan kita mempunyai file _Main.java_

1. Kompil _Main.java_ source code dengan tools _javac_,_ecj_ atau yang lainnya,

2. Cara pertama menghasilkan file _*.class_

3. Cara pertama Sudah bisa dijalankan oleh Jvm[TM] jika tidak terdapat error pada file _Main.java_ .

4. Agar program dapat berjalan di android yang menggunakan Dalvikvm[TM], kita harus mengkompile _Main.class_ ke dalvik executable (dex) file menggunakan _dx_ tools.

5. Jika tidak terdapat error program sudah dapat berjalan di dakvikvm.

Gambaran:
```
Main.java
    |----------------------- javac / ecj --(compile)
Main.class ---- Untuk JVM
    |----------------------- dx --(compile)
Main.dex ------ Untuk Dalvikvm 
```

## Kompilasi Java Di Termux

> Bagian ini terhubung dengan bagian selanjutnya
> agar mudah di pahami tolong perhatikan dengan seksama.


Tools yang di perlukan untuk kompilasi java di termux.
- ecj
- dx

Install dengan mengetik:


```bash
apt install -y ecj dx
```

Praktek:
1. Buat directory untuk kita bekerja.
```bash
mkdir -p $HOME/workspace/java/mytools
```

2. Pindah Ke directory yang baru saja di buat.
```bash
cd !$
```

3. Pastikan kita berada di directory _/data/data/com.termux/files/home/workspace/java/mytools_, cek dengan perintah
```bash
pwd
```

4. Buat lagi directory khusus untuk file java.
```bash
mkdir -p src/main/java/my/tools
```
> perhatikan directory diatas.
>
> src/main/java/my/tools
>
> agar selanjutnya mudah di pahami kita bagi menjadi 2 bagian
> _src/main/java/_ dan _my/tools/_.
>
> _src/main/java_ adalah standard sourcepath. 
>
> _my/tools_ adalah directory untuk packet/package java kita.

5. Buat file _src/main/java/my/tools/Main.java_ menggunakan nano, vim atau yg lainnya.
> Karna kita bekerja di directory internal milik termux,
> kita tidak bisa menggunakan aplikasi external seperti
> Quoda, Anacode, AIDE, Droidedit atau yang lainnya.

Pengguna vim ketik: 
```bash
vim src/main/java/my/tools/Main.java
```
Pengguna nano ketik:
```bash
nano src/main/java/my/tools/Main.java
```
> Pengguna editor lainnya silahkan menyesuaikan
> dan targetkan file yang akan di edit ke
> _src/main/java/my/tools/Main.java_.

6. Isi file _src/main/java/my/tools/Main.java_ dengan kode di bawah.


```java
// ini komentar

/** file location:  /data/data/com.termux/files/home/workspace/java/mytools/src/main/java/my/tools/Main.java */

package my.tools; // my/tools (lihat section ke 4 di atas)

/**
 * Ini juga komentar.
 * Text di dalam block komentar akan di buang saat kompilasi .
 */

public class Main {

	public static void main(String... args) {
		System.out.println("Ini program pertama saya");
	}
}
```

Lalu save.

7. Kompilasi java ke java byte code (.class).
Untuk mengkompilasi java ke java bytecode kita membutuhkan packet _ecj_ yang sebelumnya sudah kita install di atas.
Ketik:
```bash
ecj -d ./classes -verbose -classpath $PREFIX/share/java/android.jar -sourcepath ./src/main/java/ $(find ./src/main/java -type f -name \*.java)
```
Keterangan:
> option **-d** directory untuk hasil kompilasi, kita targetkan ke _./classes_.
>
> option **-verbose** menampilkan proses kompilasi.
>
> option **-classpath** menambahkan library yang di butuhkan (di C programming di sebut include dir).
>
> option **-sourcepath** memberi tahu kompiler bahwa semua file java ada di _./src/main/java_ directory.

Pada bagian
```bash
$(find ./src/main/java -type f -name \*.java)
``` 
adalah mencari dan menapilkan semua file yang ber-extension .java di directory _./src/main/java_ yg akan di kompil.

Jika tidak ada error dari kompilasi di atas seharusnya menghasilkan file _Main.class_ di dalam directory _./classes_.
untuk meng-check kita bisa jalankan perintah berikut.

```bash
ls ./classes
```

Chapter ini baru membuat java berjalan di JVM[TM] belum bisa berjalan di Dalvikvm (android).

Agar bisa berjalan di dalvikvm kita harus translate java bytecode (class) ke dalvik executable (dex) dengan cara di bawah.


## Membuat File Dex
Cara ini berhubungan dengan step-step di atas.
Ingat. kita sudah meng-install _dx_ di atas.
Dan sudah meng-kompilasi java menjadi java bytecode dengan _ecj_.
Jika lupa mohon baca kembali.
Kali ini kita akan membuat file dex atau men-translate java bytecode ke dalvik bytecode agar di mengerti oleh Dalvikvm.
Ibarat men-translate bahasa Jawa ke bahasa Sunda agar orang sunda mengerti.
Sebelumnya kita buat dulu folder _./bin_:
```bash
mkdir ./bin
```

Setelah itu jalankan perintah:
```bash
dx --dex --verbose --output ./bin/Main.dex 
```
Jika berhasil seharusnya menghasilkan file _Main.dex_ di directory _./bin_.
Check:
```bash
ls ./bin
```
Jika ada artinya translate berhasil.


## Menjalankan.
Ingat file dex berada di _./bin/Main.dex_.
Ingat java code pada bagian 
```java
package my.tools;

public class Main ....
```
di atas.

Ini akan berkaitan.
Untuk menjalankan progran yang telah kita buat ketik command:
```bash
dalvikvm -cp ./bin/Main.dex my.tools.Main
```
Jika mengikuti panduan dengan benar seharusnya menampilkan output.
```
Ini program pertama saya
```


## Penutup
Terlihat sulit?
> Tidak ada yang sulit jika kita mau belajar.

Terlalu bertele tele untuk membuat program yang sederhana?
> Ya.. java memang di design untuk programmer yg bekerja Tim lebih dari 1 orang.
>
> Karna java adalah OOP (object oriented programming).

Apa ke unggulannya?
> Java di design extensible kita bisa meng-upgrade aplikasi tanpa merubah kode sebelumnya .
>
> Dengan java kita bisa membuat web app, desktop app, command line app, Android app, dan masih banyak lagi.
>
> java memikiki library yang banyak builtin atau pun library yang bertebarab di internet.
>
> Java meng-klaim sama cepat dengan C.
>
> Java meng-klaim lebih secure dari C.



