---
layout: post
title: Mengatasi NTFS Error dengan LiveUSB  BlankOn
date: '2011-12-16T04:09:00.001+07:00'
author: Samsul Maarif
categories: blog
tags:
- Tutorial
- ntfsfix
- ntfs error
modified_time: '2011-12-16T04:10:53.423+07:00'
thumbnail: http://4.bp.blogspot.com/-xcpvgFMkmhk/TuizyGcFbMI/AAAAAAAADfc/8yT70-Nubyg/s72-c/Gambar-Layar.png
blogger_id: tag:blogger.com,1999:blog-1383767785423682157.post-3703262032346271437
blogger_orig_url: http://blog.samsul.web.id/2011/12/mengatasi-ntfs-error-dengan-liveusb.html
---

Satu permasalahan kali ini adalah di laptop teman Acer Aspire One 522 warna hitam. Kenapa selalu 'laptop teman'? Jawabannya karena saya sendiri tidak/belum memiliki laptop sendiri :D (berharap saja suatu saat akan punya sendiri, tapi jangan berharap akan punya masalah :P). Kondisi laptop telah terinstall windows 7 (bawaan laptop setelah diservice) dan Linux Sabily Al-Quds 10.10.Saat saya cek partisi hddnya di terminal dengan perintah berikut "sudo fdisk -l" (tanpa tanda kutip), muncul pesan error seperti berikut :..........$MFTMirr does not match $MFT (record 0).Failed to mount '/dev/sda8': Input/output errorNTFS is either inconsistent, or there is a hardware fault, or it's aSoftRAID/FakeRAID hardware. In the first case run chkdsk /f on Windowsthen reboot into Windows twice. The usage of the /f parameter is veryimportant! If the device is a SoftRAID/FakeRAID then first activateit and mount a different device under the /dev/mapper/ directory, (e.g./dev/mapper/nvidia_eahaabcc1). Please see the 'dmraid' documentationfor more details.Terdapat masalah pada partisi /dev/sda8 yang formatnya NTFS. Kemudian saya coba untuk mount partisi tersebut pada tempatnya, sayangnya pesan error yang sama muncul. Dari pesan error tersebut disarankan untuk masuk ke sistem windows lalu jalankan perintah "chkdsk /f" di command prompt kemudian restart komputer ke windows dua kali. Namun masalahnya, laptopnya sudah tidak bisa booting &nbsp;ke windows lagi.&nbsp;Yep, itu tadi penampakannya ketika saya jalankan melalui liveUSB BlankOn. Pesan errornya tak jauh berbeda dengan ketika dimount dengan CLI.&nbsp;Oh, iya kronologinya begini. Karena windowsnya sudah tidak waras (tidak mau masuk ke windows), pemilik laptop berniat akan menghapus/memformat partisi sistem windowsnya. Sebelumnya data-data penting dalam partisi tersebut dipindahkan ke partisi lain yang sama-sama formatnya ntfs. Nah, pada saat proses pemindahan data sebesar 32 Gb tersebut sistem mengalami freeze. Mungkin karena terlalu berat dengan sistem Sabily disamping clockspeed laptop hanya 1.0 Ghz. Dalam kondisi seperti itu, pemilik laptop nampaknya tidak sabar dan akhirnya mematikan laptopnya secara paksa dengan menekan tombol power beberapa menit. Akibatnya, ya itu tadi.....Saya mencoba tanya-tanya ke mbah google (link lengkap ada di bawah) dan menemukan banyak sekali cara pemecahan masalahnya. Salah satu di antaranya menyebutkan saya harus menginstall paket aplikasi 'ntfsprogs' :$ sudo apt-get install ntfsprogsEh, ternyata paket ini telah terinstall secara default di LiveUSB BlankOn Ombilin, jadi tinggal "rock 'n roll". Lalu jalankan perintah berikut untuk memerbaiki partisinya :$ sudo ntfsfix /dev/sda8Tak diduga, semuanya berjalan lancar dan semuanya kembali &nbsp;seperti sedia kala (sayangnya log/output dari perintah tersebut lupa saya simpan, yang saya ingat tiap baris eksekusi menunjukkan kata "Succesfully"). Padahal pada tutorial yang saya ikuti, mereka gagal. Pada intinya : jangan takut mencoba.Ini hanyalah pengalaman saya, saya tidak menjamin hal ini juga akan berhasil mengatasi permasalah Anda jika ternyata Anda juga memiliki permasalah yang sama (tergantung tingkat kerusakan partisi/hardware). Dan sebaiknya Anda baca ini juga.Sumber daya :Googleaskubuntu.comlinuxforum.orglinuxquestionsubuntu-indonesia.com