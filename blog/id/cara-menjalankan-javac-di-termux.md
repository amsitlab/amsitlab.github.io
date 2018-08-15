Cara Menjalankan Javac Di Termux
=================================

# Daftar Isi
1. [Pendahuluan](#pendahuluan) .
2. [Peralatan](#peralatan) .
3. [Memulai](#memulai) .
4. [Testing](#testing) .
5. [Membuat Shortcuts](#membuat-shortcuts) .


# Pedahulauan
Apa itu javac?
> **javac** adalah tools compiler untuk meng-kompile code java ke java bytecode agar dapat berjalan di JVM[TM].

Bagaimana supaya **javac** bisa berjalan di Termux?
> Karna termux berjalan di android,
> dan android menggunakan dalvikvm maka kita harus men-translate
> javabytecode dari tools **javac** ke dex executable agar bisa
> berjalan di termux yang menggunakan dalvikvm.

Caranya?
> Simak panduan di bawah


# Peralatan
Pastikan kita memiliki per-alatan yang di butuhkan untuk bekerja.
* **javac-1.0.jar**
> Akan di download di bawah.

* **dx**
> untuk men-translate javabytecode ke dalvik executable
>
> jika belum ter-install silahkan install dengan cara.
>
```bash
apt install -y dx
```
>

* **ecj** 
> membutuhkan file android.jar untuk bootclasspath yang ada di pacakge ecj.
>
> jika belum ter-install, silahkan install dengan cara.
>
```bash
apt install -y ecj
```
>


# Memulai
Setelah peralatan sudah tersedia, mari kita explore.
* Pertama-tama kita buat directory untuk bekerja.
>
```bash
mkdir -p $HOME/workspace/java/porting-javac
```
>

* Lalu kita pindah ke directory yang baru kita buat.
>
```bash
cd !$
```
>

* Pastikan kita di directory yg benar.
> Ketik:
>
```bash 
pwd
```
>

* Jika hasilnya **/data/data/com.termux/files/home/workspace/java/porting-javac** mari ketahap selanjutnya.

* Download **javac-1.0.jar.zip**
>
```bash
wget -O "javac-1.0.jar.zip" "http://www.java2s.com/Code/JarDownload/javac/javac-1.0.jar.zip"
```
>

* Meng-extract file **javac-1.0-jar.zip** yang baru di download.
>
```bash
unzip javac-1.0.jar.zip -d .
```
>

* lalu check
>
```bash
ls
```
>

* Jika terdapat file **javac-1.0.jar** mari lanjutkan.


* Translate ke dex.
> Mari translate java bytecode ke dex, dengan cara 
>
```bash
dx --dex \
   --verbose \
   --keep-classes \
   --output javac-1.0-dex.jar \
   javac-1.0.jar
```
>

* Tunggu sekitar 1-2 menit, setelah selesai mari cek
>
```bash
ls
```
>

* jika terdapat file baru bernama **javac-1.0-dex.jar** mari kita test.


# Testing
* Buat file java bernama **Test.java**.
> isi text di bawah.
>

```java
import static java.lang.System.out;

/**
 * Just Test class
 *
 * @author Kang Sate
 * @since Negara Api Menyerang
 * @version always alpha
 */
public class Test {

	public static void main(String[] args) {
		out.println("Work perfectly");
	}

}
```

* Lalu compile file **Test.java** dengan progran **javac** yg baru saja kita translate.
>
```bash
dalvikvm -cp ./javac-1.0-dex.jar \
	 com.sun.tools.javac.Main \
	 	-bootclasspath $PREFIX/share/java/android.jar \
		Test.java
```
>

* Jika menghasilkan file **Test.claas** maka kita berhasil.

> Commandnya terlalu panjang? mari kita buat shortcuts.


# Membuat Shortcuts
> Saya pengguna [vim](http://vim.org) dan akan menggunakan vim
> sebagi text editor di panduan ini. tolong sesuaikan dengan
> text editor favorit kalian.

* Buat Directory baru di **$HOME** bernama **share/dex**
>
```bash
mkdir -p $HOME/share/dex
```
>

* Pindahkan file **./javac-1.0-dex.jar** ke **$HOME/share/dex**.
>
```bash
mv ./javac-1.0-dex.jar $HOME/share/dex
```
>

* Buat directory baru di **$HOME** bernama **bin**.
>
```bash
mkdir -p $HOME/bin
```
>

* Buat file baru di **$HOME/bin** bernama **javac**
>
```bash
vim $HOME/bin/javac
```
>

* Isi dengan kode berikut.
>
```bash
#!/data/data/com.termux/files/usr/bin/bash

dalvikvm -cp $HOME/share/dex/javac-1.0-dex.jar \
	com.sun.tools.javac.Main \
		-bootclasspath $PREFIX/share/java/android.jar
		$@
```
>

* Lalu save.

> Sekarang kita bisa menjalankan **javac** dengan perintah 
>
```bash
bash $HOME/bin/javac
```
>
> Masih terlalu panjang? belum puas? dasar manusia.
> Ok lah..
>

* ketik perintah ini:
>
```bash
echo "export PATH=$PATH:$HOME/bin" > $HOME/.bashrc
```
>

* Sekarang manusia bisa memanggil program **javac** dengan command
>
```bash
javac
```
>
> Seneng? Ah sudahlah..





