# VPN Site-to-Site

## Skenario

Mengkonfigurasi **VPN Site-to-Site berbasis IPsec** untuk menghubungkan dua jaringan lokal yang terpisah secara geografis (misal Kantor A dan Kantor B) melalui tunnel terenkripsi lewat internet, sehingga trafik antar-site aman dari sadap-menyadap.

## Topologi

Dua jaringan lokal, masing-masing dengan PC dan router gateway (R1 dan R2), terhubung lewat router perantara (R3) yang mewakili internet/ISP. Tunnel VPN dibangun antara R1 dan R2 melalui interface serial mereka.

*(Tambahkan screenshot topologi di sini: `topology-screenshot.png`)*

## Konfigurasi Kunci

**ISAKMP Phase 1 (mengamankan negosiasi tunnel):**
```
crypto isakmp policy 10
 encryption aes 256
 hash sha256
 authentication pre-share
 group 14
crypto isakmp key <shared_key> address <peer_IP>
```

**IPsec Phase 2 (mengamankan trafik data):**
```
crypto ipsec transform-set MY-SET esp-aes esp-sha-hmac

access-list 100 permit ip <local_network> <wildcard> <remote_network> <wildcard>

crypto map MY-MAP 10 ipsec-isakmp
 set peer <peer_IP>
 set transform-set MY-SET
 match address 100
```

**Terapkan crypto map ke interface WAN:**
```
interface Serial0/3/0
 crypto map MY-MAP
```

*(Ganti placeholder di atas dengan konfigurasi asli yang kamu pakai di lab ini)*

## Hasil Test

- Verifikasi status tunnel:
```
show crypto isakmp sa
show crypto ipsec sa
```
- Test ping dari PC di Site A ke PC di Site B berhasil melalui tunnel
- *(Tambahkan screenshot hasil `show crypto session` dan hasil ping antar-site di sini)*

## Tantangan/Troubleshooting

*(Isi dengan kendala yang kamu temui, misalnya mismatch pre-shared key, ACL yang salah arah, atau tunnel tidak establish — jelaskan cara kamu mendiagnosis dan menyelesaikannya)*
