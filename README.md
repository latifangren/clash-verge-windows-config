# Clash Verge Windows - config.yaml

Konfigurasi ini digunakan untuk aplikasi Clash Verge di Windows, yang berfungsi sebagai klien proxy untuk mengelola lalu lintas internet melalui berbagai server dan aturan. Berikut penjelasan singkat mengenai bagian-bagian utama file `config.yaml` ini:

## Daftar Isi
- [Port dan Mode](#port-dan-mode)
- [TUN Mode](#tun-mode)
- [Proxy & Proxy Provider](#proxy--proxy-provider)
- [Proxy Groups](#proxy-groups)
- [DNS](#dns)
- [Rule Provider & Rules](#rule-provider--rules)
- [Fitur Lainnya](#fitur-lainnya)
- [Tips Penggunaan](#tips-penggunaan)
- [Dukungan Dual Interface: LAN & USB Tethering HP](#dukungan-dual-interface-lan--usb-tethering-hp)

---

## Port dan Mode
- **mixed-port, redir-port, tproxy-port, port, socks-port**: Pengaturan port untuk berbagai jenis proxy (HTTP, SOCKS5, Redir, TProxy, dll).
- **mode**: Mode operasi utama (`rule`), artinya lalu lintas diatur berdasarkan aturan.
- **allow-lan**: Mengizinkan akses dari jaringan lokal.
- **external-controller**: Port untuk mengontrol Clash dari aplikasi lain (misal dashboard).
- **secret**: Kata sandi untuk akses controller.

## TUN Mode
Bagian `tun` mengaktifkan mode TUN (virtual network interface) untuk menangkap semua lalu lintas jaringan.
- **auto-route**: Otomatis mengatur rute.
- **dns-hijack**: Mengalihkan permintaan DNS ke Clash.

## Proxy & Proxy Provider
- **proxies**: Daftar proxy langsung (misal: USB-DIRECT, LAN-DIRECT).
- **proxy-providers**: Mengelola daftar proxy dari file eksternal (misal: WARP-ID, WARP-SG, WARP-US).

## Proxy Groups
Mengelompokkan proxy menjadi beberapa grup untuk berbagai kebutuhan, seperti:
- **AdBlock, Speedtest, Steam, BattleNet, EA-Games, Streaming**: Grup untuk aplikasi/spesifik.
- **Auto-Proxies, Best Ping-Proxies**: Otomatis memilih proxy terbaik.
- **USB, LAN, GLOBAL**: Grup berdasarkan sumber koneksi.

## DNS
Pengaturan DNS untuk menghindari sensor dan mempercepat resolusi domain.
- **enhanced-mode: fake-ip**: Menggunakan fake IP untuk domain.
- **nameserver, fallback**: Daftar DNS resolver (AdGuard, Google, Cloudflare).
- **fake-ip-filter**: Daftar domain yang tidak akan difake-IP.

## Rule Provider & Rules
- **rule-providers**: Mengambil aturan dari file lokal/URL (Direct, Umum, Reject, Streaming, AdBlock, Speedtest, Steam, BattleNet, EA-Games).
- **rules**: Urutan aturan yang diterapkan, mulai dari direct, blokir, adblock, hingga fallback global.

## Fitur Lainnya
- **profile**: Menyimpan pilihan proxy dan fake IP.
- **sniffer**: Mengaktifkan sniffer untuk mendeteksi protokol lalu lintas.
- **experimental**: Fitur eksperimental seperti sniff-tls-sni, tcp-concurrent, dll.
- **hosts**: Mapping domain ke IP tertentu.

---

## Tips Penggunaan
1. **Edit nama interface** pada bagian `proxies` sesuai dengan nama adapter jaringan di Windows Anda (misal: "Ethernet", "Ethernet 2").
2. **Pastikan file provider** (misal: `warp-id.yaml`, `warp-sg.yaml`, dll) tersedia di folder `provide/`.
3. **Update rule-provider** secara berkala agar aturan tetap terbaru.
4. **Gunakan dashboard** Clash Verge untuk memantau dan mengubah proxy secara real-time.
5. **Restart aplikasi** setelah mengubah konfigurasi agar perubahan diterapkan.

---

## Dukungan Dual Interface: LAN & USB Tethering HP

Konfigurasi ini mendukung penggunaan dua koneksi internet secara bersamaan, yaitu melalui LAN (kabel) dan USB tethering dari HP. Fitur ini sangat berguna untuk:
- **Redundansi koneksi:** Jika salah satu koneksi terputus, koneksi lain tetap bisa digunakan.
- **Load balancing:** Lalu lintas internet dapat dibagi atau dipilih otomatis antara dua sumber internet.
- **Prioritas aplikasi:** Anda bisa mengatur aplikasi tertentu menggunakan koneksi LAN atau USB tethering sesuai kebutuhan.

### Cara Menggunakan
1. **Sambungkan kedua koneksi ke PC/laptop:**
   - LAN (Ethernet) dari router/modem.
   - USB tethering dari HP (pastikan mode tethering aktif di HP dan terdeteksi di Windows).
2. **Cek nama interface di Windows:**
   - Buka Command Prompt, jalankan `ipconfig` atau cek di "Network Connections".
   - Biasanya LAN bernama "Ethernet" dan USB tethering bernama "Ethernet 2" atau sejenisnya.
3. **Edit bagian `proxies` di config.yaml:**
   - Pastikan `interface-name` sesuai dengan nama adapter di Windows Anda.
   - Contoh:
     ```yaml
     proxies:
       - name: USB-DIRECT
         type: direct
         interface-name: "Ethernet 2"  # USB tethering HP
       - name: LAN-DIRECT
         type: direct
         interface-name: "Ethernet"    # LAN kabel
     ```
4. **Pilih proxy group di aplikasi Clash Verge:**
   - Anda bisa memilih antara "USB", "LAN", atau membiarkan sistem memilih otomatis berdasarkan kecepatan/ping.

### Catatan Penting
- Pastikan kedua koneksi aktif dan terdeteksi oleh Windows.
- Anda bisa memanfaatkan fitur load-balance atau auto-fallback agar koneksi tetap stabil.
- Jika ingin memprioritaskan salah satu koneksi, atur urutan pada proxy group sesuai kebutuhan.

---

## Catatan
- File ini sudah dioptimalkan untuk penggunaan multi-proxy, adblock, dan bypass region.
- Untuk bantuan lebih lanjut, kunjungi [GitHub Clash](https://github.com/Dreamacro/clash) atau [Clash Verge](https://github.com/zzzgydi/clash-verge).

---

**Dibuat oleh Latifan | Otomatisasi README oleh AI**