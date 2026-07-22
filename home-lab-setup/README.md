# Home Lab Setup

Dokumentasi environment lab pribadi untuk persiapan karier IT Security/Networking — dipakai sebagai basis praktik dari Fase 0 hingga fase-fase berikutnya.

## Topologi

![Network Topology](topology-diagram.png)

Tiga node (Host, VM Kali, VM Ubuntu) terhubung dalam satu jaringan host-only, dan masing-masing VM juga punya akses internet terpisah lewat NAT.

## Komponen

| Node | Peran | IP (Host-only) |
|---|---|---|
| Host (Windows) | Laptop fisik, menjalankan hypervisor | 192.168.56.1 |
| VM Kali Linux 2026.2 | Attacker/security tools (Wireshark, Snort, dll) | 192.168.56.103 |
| VM Ubuntu Desktop | Target/general purpose Linux | 192.168.56.104 |

## Konfigurasi Network

Setiap VM (Kali & Ubuntu) menggunakan **2 network adapter**:

- **Adapter 1 — NAT**: memberikan akses internet ke masing-masing VM secara independen (untuk update package, download tools, dll)
- **Adapter 2 — Host-only Adapter**: menghubungkan Host dan kedua VM dalam satu jaringan lokal `192.168.56.0/24`, dengan DHCP Server aktif dari VirtualBox

Setup dilakukan lewat: VirtualBox → **Tools → Host Network Manager → Create** (host-only network dibuat sekali, lalu di-attach ke Adapter 2 tiap VM lewat Settings → Network).

## Tools yang Digunakan

- **Hypervisor**: Oracle VirtualBox
- **Kali Linux 2026.2** (VM pre-built, format `.vbox` + `.vdi`)
- **Ubuntu Desktop** (install manual dari ISO)
- **Cisco Packet Tracer** untuk visualisasi topologi

## Verifikasi Konektivitas

Semua node berhasil saling ping tanpa packet loss:

| Dari | Ke | Hasil |
|---|---|---|
| Host | VM Ubuntu (192.168.56.104) | 0% loss, avg 2ms |
| Host | VM Kali (192.168.56.103) | 0% loss, avg 0ms |
| VM Kali | VM Ubuntu | Reply lancar, tidak ada timeout |
| VM Ubuntu | VM Kali | Reply lancar, tidak ada timeout |

## Catatan

Repo ini adalah bagian dari roadmap pembelajaran IT Security/Networking 6 bulan, mencakup fondasi networking, security fundamentals, CompTIA Security+, praktik SOC, dan cloud security.
