# NAT Configuration

## Skenario

Mengkonfigurasi **NAT Overload (PAT)** pada router agar seluruh PC di jaringan internal dapat mengakses internet menggunakan satu alamat IP publik pada interface router yang menghadap ISP/WAN.

## Topologi

Jaringan terdiri dari beberapa PC yang terhubung ke dua switch (Switch0 dan Switch1), yang kemudian terhubung ke router (R1). R1 terhubung ke router kedua (R2) mewakili sisi ISP/internet lewat koneksi serial.

*(Tambahkan screenshot topologi di sini: `topology-screenshot.png`)*

## Konfigurasi Kunci

**Interface internal (menghadap LAN):**
```
interface FastEthernet0/0
 ip address <IP_LAN> <subnet_mask>
 ip nat inside
```

**Interface eksternal (menghadap WAN/Serial):**
```
interface Serial0/0/1
 ip address <IP_WAN> <subnet_mask>
 ip nat outside
```

**Access-list untuk menentukan trafik yang di-NAT:**
```
access-list 1 permit <network_LAN> <wildcard_mask>
```

**NAT overload:**
```
ip nat inside source list 1 interface Serial0/0/1 overload
```

*(Ganti placeholder di atas dengan konfigurasi asli yang kamu pakai di lab ini)*

## Hasil Test

- Verifikasi tabel NAT translation:
```
show ip nat translations
```
- Test ping dari PC internal ke luar jaringan berhasil
- *(Tambahkan screenshot hasil `show ip nat translations` dan hasil ping di sini)*

## Tantangan/Troubleshooting

*(Isi dengan kendala yang kamu temui selama membuat lab ini, misalnya error konfigurasi ACL atau routing, dan bagaimana cara menyelesaikannya — ini menunjukkan proses belajar, bukan cuma hasil akhir)*
