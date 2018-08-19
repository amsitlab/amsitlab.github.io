Integrasi Dengan Picocli
========================



# Pembuka
--------------------------------------------------------
Panduan ini menujukan bagaimana membuat java commandline app dengan commandex yang ter-integrasi dengan library [picocli], untuk dokumetasi lebih lanjut tentang picocli silahkan menuju official website di atas.



# Index
--------------------------------------------------------
> Kita akan membuat aplikasi bernama **mytools**.
>
> Saya menggunakan [vim] sebagai editor, anda bisa mesusaikan 
> dengan editor favorit anda.
>
> `com.mytools` adalah nama package kita.

Langkah pertama pastikan **commandex** telah ter-install di perangkat anda, untuk tahap instalasi sudah saya jelaskan di halaman [Commandex Guide] .

Jika **commandex** sudah ter-install, anda bisa buka [termux] dan ketik perintah

```bash
commandex new mytools
```

Commandex akan memunculkan input-prompt `Enter project package` isi dengan `com.mytools` lalu tekan enter.
Setelah itu **commandex** akan memunculkan input-prompt lagi seperti:

```bash
Available template:
0) Basic
1) Picocli
Choose one of template number:
```

isi dengan angka `1`, tekan enter lalu commandex akan membuatkan direktori untuk kita bekerja, membuatkan kita file **./src/main/java/com/mytools/App.java** seperti pada gambar berikut:

<p align="center">
	<img src="/images/1.png">
</p>

Tahap selanjutnya mari kita edit file **./src/main/java/com/mytools/App.java** dengan editor favorit masing-masing, saya menggunakan vim, tolong sesuaikan dengan editor anda.

```bash
vim ./src/main/java/com/mytools/App.java
```

Akan mucul default code yang telah di buatkan oleh **commandex** yang hanya perlu kita edit sesuai kebutuhan.
default code dari file _./src/main/java/com/mytools/App.java_ seperti di bawah:

```java
/** This file created by commadex */

package com.mytools;

import picocli.CommandLine;
import picocli.CommandLine.Command;
import picocli.CommandLine.Option;
import picocli.CommandLine.Parameters;

@Command(name = "mytools",
	mixinStandardHelpOptions = true,
	version = "mytools 1.1"
	)
public class App implements Runnable
{

	/**
	 * Application name
	 */
	public static String APP_NAME = "mytools";


	public void run()
	{
		System.out.println("Created by commandex");

	}


	/**
	 * main program
	 */
	 public static void main(String ...args)
	 {
	 	CommandLine.run(new App(), System.out, args);
	 }


}
```

Default code bisa kita edit sesuai kebutuhan.
Namun di panduan kali ini saya hanya menjelaskan integrasi antara **commandex** dan **picocli** .
Kita lompatke step compilasi dengan mengetik command di bawah:

```bash
commandex jar
```

Maka **commandex** akan men-compilasi code, membuat file .jar, membuat bash shortcuts untuk anda, seperti gambar di bawah.

<p align="center">
	<img src="/images/2.png">
</p>

Sekarang kita bisa menjalankan aplikasi dengan perintah:

```bash
./mytools
```

Atau menampilkan `help` untuk aplikasi anda dengan command:

```bash
./mytools -h
# atau
./mytools --help
```

<p align="center">
	<img src="/images/3.png">
</p>



# Catatan
--------------------------------------------------------
> Sekali lagi saya himbau.
>
> Default code bisa kita edit sesuai kebutuhan.
> Namun di panduan kali ini saya hanya menjelaskan integrasi antara **commandex** dan **picocli** .




[Commandex Guide]: https://amsitlab.github.io/guide/commandex/1.0/
[termux]: https://termux.net
[tmux]: https://id.m.wikipedia.org/wiki/Tmux
[vim]: https://www.vim.org
[picocli]: https://picocli.info
