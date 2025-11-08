# ROG LED Control Dashboard

Web dashboard untuk mengontrol LED melalui MQTT broker HiveMQ dengan tema ROG (Republic of Gamers).

## Fitur

- **Real-time LED Control**: Kontrol 4 LED secara individual atau bersamaan
- **MQTT Integration**: Terhubung ke broker.hivemq.com dengan WebSocket secure
- **ROG Theme**: Desain dark dengan aksen merah khas gaming
- **Status Monitoring**: Monitor koneksi MQTT dan status LED real-time
- **Message Log**: Tampilkan log pesan MQTT yang terkirim
- **Responsive Design**: Tampilan optimal di desktop dan mobile

## Cara Penggunaan

### 1. Koneksi ke MQTT Broker
- Klik tombol "Connect" untuk terhubung ke broker.hivemq.com
- Status koneksi akan ditampilkan di bagian atas dashboard
- Client ID akan dibuat otomatis dengan format `rog-led-control-xxxxxxxx`

### 2. Kontrol LED
- **Individual Control**: Gunakan toggle switch atau tombol pada setiap kartu LED
- **Master Control**: Gunakan panel kontrol untuk mengontrol semua LED:
  - "Toggle All LEDs": Toggle semua LED
  - "All On": Nyalakan semua LED
  - "All Off": Matikan semua LED

### 3. Monitoring
- **Status Bar**: Menampilkan informasi broker, port, dan client ID
- **LED Status**: Indikator visual untuk setiap LED dengan efek glow saat aktif
- **Message Log**: Log pesan MQTT yang terkirim dengan timestamp

## MQTT Topics

Dashboard menggunakan topik MQTT berikut:
- **Control**: `rog/led/{ledId}` (led1, led2, led3, led4)
- **Status**: `rog/led/{ledId}/status`
- **Message**: `ON` atau `OFF`

## Teknologi

- **Frontend**: Next.js 15, TypeScript, Tailwind CSS, shadcn/ui
- **Backend**: Next.js API Routes, MQTT.js
- **Broker**: HiveMQ Public Broker (broker.hivemq.com:8884)
- **Protocol**: MQTT over WebSocket (WSS)

## Struktur Project

```
src/
├── app/
│   ├── page.tsx                 # Dashboard UI
│   └── api/mqtt/
│       ├── connect/route.ts     # MQTT connection API
│       ├── disconnect/route.ts  # MQTT disconnect API
│       └── publish/route.ts     # MQTT publish API
├── lib/
│   └── mqtt.ts                  # MQTT client wrapper
└── components/ui/               # shadcn/ui components
```

## Konfigurasi MQTT

- **Broker**: broker.hivemq.com
- **Port**: 8884 (WebSocket Secure)
- **Client ID**: Auto-generated
- **QoS**: 1 (at least once delivery)
- **Retain**: True untuk status messages

## Cara Kerja

1. Dashboard terhubung ke MQTT broker melalui WebSocket secure
2. Setiap aksi kontrol LED mengirim pesan ON/OFF ke topik yang sesuai
3. Status LED diperbarui secara real-time di UI
4. Message log menampilkan semua pesan yang terkirim
5. Koneksi otomatis direconnect jika terputus

## Notes

- Pastikan koneksi internet stabil untuk koneksi MQTT
- LED fisik perlu dikonfigurasi untuk subscribe ke topik yang sama
- Dashboard siap digunakan untuk kontrol LED yang compatible dengan MQTT