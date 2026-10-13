# Tugas Praktikum 5 — Sistem Operasi
## Topik: Job Control

**Nama:** Fiky Hasan  
**Username Linux:** `fiky-hasanmudin`

Repository ini berisi jawaban dan file script untuk bagian **VI. Tugas** pada Modul Praktikum Sistem Operasi Pertemuan 5. Perintah interaktif (`su`, `history`, `fc`, `fg`, `bg`, `jobs`, `pushd`, dan `popd`) dijalankan langsung di terminal Bash.

> Catatan: Sesuaikan nama jika diperlukan sebelum dikumpulkan. Jangan menyimpan password ke repository. Perubahan `/etc/profile` hanya dilakukan jika memiliki izin administrator.

---

## 1. Profile

### a. `/etc/profile`
Tambahkan baris berikut di akhir `/etc/profile` jika praktikum meminta perubahan profile sistem:

```bash
echo "Profile dari /etc/profile"
```

Perintah edit:
```bash
sudo nano /etc/profile
```

### b. Profile pengguna
Tambahkan pesan yang sesuai ke file profile pengguna. Contoh:

`~/.bash_profile`
```bash
echo "Profile dari .bash_profile"
```

`~/.bash_login`
```bash
echo "Profile dari .bash_login"
```

`~/.profile`
```bash
echo "Profile dari .profile"
```

`~/.bashrc`
```bash
echo "Profile dari .bashrc"
```

Edit file menggunakan `nano ~/.NAMA_FILE`. Bash login biasanya membaca hanya file pertama yang tersedia dari `.bash_profile`, `.bash_login`, atau `.profile`; `.bashrc` umumnya dibaca oleh shell interaktif non-login.

### c. Perbedaan `su` dan `su -`
```bash
su NAMA_USER
exit
su - NAMA_USER
exit
```
Ganti `NAMA_USER` dengan akun Linux yang benar-benar ada. Akun `mahasiswa` mungkin tidak tersedia; periksa dengan `getent passwd mahasiswa`. `su -` memulai lingkungan login pengguna tujuan, sedangkan `su` berpindah pengguna tanpa memuat lingkungan login sepenuhnya.

---

## 2. Prompt String (PS)

Tambahkan ke `~/.bashrc` atau file profile yang sesuai:

```bash
PS1='> '
export PS1
```

Coba format prompt berikut satu per satu di terminal:

```bash
PS1='\! > '
PS1='\d > '
PS1='\t > '
PS1='Saya=\u > '
PS1='\w > '
PS1='\h > '
```

Keterangan: `\!` nomor history, `\d` tanggal, `\t` waktu, `\u` username, `\w` direktori kerja, dan `\h` hostname.

---

## 3. Logout

Tambahkan ke `~/.bash_logout`:

```bash
echo "Terima kasih atas sesi yang diberikan"
sleep 5
clear
```

File `.bash_logout` dijalankan pada akhir sesi login Bash yang mendukungnya; efeknya dapat berbeda pada terminal desktop.

---

## 4. Bash Script

File yang disertakan:
- `p1.sh`: menampilkan informasi file (`ls -l`).
- `p2.sh`: menampilkan pengguna yang login (`who`).
- `p3.sh`: menampilkan proses (`ps x`).

Jalankan:

```bash
chmod +x p1.sh p2.sh p3.sh
./p1.sh ; ./p3.sh ; ./p2.sh
./p1.sh &
./p1.sh
./p2.sh &
./p3.sh &
( ./p1.sh ; ./p3.sh ) &
```

---

## 5. Jobs

File `pwaktu.sh` mencatat tanggal dan waktu ke file `hasil` setiap 10 detik.

```bash
chmod +x pwaktu.sh
./pwaktu.sh &
jobs
find / -print > files 2>/dev/null &
jobs
```

Pindahkan job pertama ke foreground, tekan `Ctrl+Z`, lalu kembalikan ke background:

```bash
fg %1
# Tekan Ctrl+Z
bg
jobs
```

Lihat PID dan hentikan proses yang sesuai:

```bash
jobs -l
ps x
kill NOMOR_PID
```

Ganti `NOMOR_PID` dengan PID sebenarnya. Jangan menyalin teks `NOMOR_PID` secara harfiah.

---

## 6. History

Jalankan di terminal Bash interaktif:

```bash
HISTSIZE=20
history
fc -l
!-5
!!
!150
!ls
```

Perintah yang diawali `!` menjalankan ulang perintah dari history. Pastikan perintah yang akan diulang aman. `!150` hanya berhasil jika nomor 150 ada dalam history.

---

## Menjalankan script

```bash
chmod +x p1.sh p2.sh p3.sh pwaktu.sh
./p1.sh
./p2.sh
./p3.sh
```

Untuk menguji `pwaktu.sh`, jalankan `./pwaktu.sh &`, tunggu beberapa detik, lalu periksa dengan `cat hasil`. Hentikan proses setelah selesai.


