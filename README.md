# 🛡️ Bear Cyber Hunt – ACAD CSIRT Log Analysis

Proyek ini merupakan bagian dari simulasi keamanan siber dalam konteks Blue Team, dengan studi kasus berdasarkan skenario serangan yang dianalisis oleh ACAD-CSIRT. Fokus utama proyek ini adalah melakukan analisis terhadap file log dan packet capture (PCAP) untuk mendeteksi, mengidentifikasi, dan memberikan rekomendasi mitigasi terhadap berbagai jenis serangan siber.

## 📂 Isi Analisis

### 1. Analisis Insiden Umum
Analisis dilakukan terhadap log sistem dan menunjukkan beberapa jenis serangan:
- **Brute Force Attack (SSH)**
- **Port Scanning / Reconnaissance**
- **Web Exploitation (Command Injection)**
- **Malware Installation & Execution**
- **Privilege Escalation (john to root)**

**Sumber IP Penyerang:**
- `192.168.1.100` – Brute force SSH
- `203.0.113.5` – Port scanning
- `10.0.0.5` – Web exploitation dan malware execution
- `10.0.0.8` – Login root setelah login oleh user `john`

### 2. Analisis File `try.pcapng`
#### A. Protokol Dominan
- Protokol paling sering muncul adalah **ARP** (39 paket).
- Potensi indikasi **ARP Spoofing** jika terjadi dalam frekuensi tinggi.

#### B. HTTP Traffic
- Terjadi komunikasi dua arah antara `172.16.1.1` dan `172.16.1.129` via HTTP.

#### C. Aktivitas Penyerang
- `172.16.1.1` mencoba melakukan brute-force login ke endpoint `/login.php` sebanyak 3 kali.

#### D. Kredensial Terdeteksi
- Username: `Isac`
- Password: `lappe`

### 3. Analisis File `comm.pcap`
#### A. Komunikasi Terenkripsi
- Deteksi TLS (Transport Layer Security) handshake dengan lebih dari 3 paket.
- IP: `10.1.30.11` → `10.1.10.120`
- Port server: `8443` (port umum untuk HTTPS alternatif)

#### B. Alat yang Digunakan Penyerang
- Aktivitas menunjukkan pola port scanning dan SMTP abuse.
- Potensi tools: `Nmap`, `Hydra`, `Metasploit`, `Netcat`.

#### C. Identifikasi Sistem Operasi
- Penyerang menggunakan **Linux kernel 3.11+**
- IP Penyerang: `10.1.20.88`

#### D. Brute Force FTP & SSH
- FTP login sukses dengan banyak kode `230 Login successful`.
- Tidak ada file yang diupload melalui FTP.
- Setelah itu, terjadi koneksi SSH dari `10.1.40.80` ke `10.1.30.11`.

---

## 🔐 Rekomendasi Proteksi

### Tindakan Segera:
- Isolasi host yang terinfeksi
- Blokir IP penyerang di firewall
- Hapus file malware dan lakukan forensik

### Pencegahan Lanjutan:
- Gunakan **Fail2ban** dan **2FA** untuk SSH
- Tutup port yang tidak diperlukan
- Terapkan **WAF** untuk melindungi web application
- Audit sistem untuk backdoor dan persistence

---

## 📄 Lisensi
Proyek ini menggunakan lisensi MIT. Silakan gunakan, modifikasi, dan distribusikan dengan tetap menyertakan atribusi.

---

✉️ Untuk informasi lebih lanjut, hubungi tim CSIRT terkait atau admin proyek ini.
