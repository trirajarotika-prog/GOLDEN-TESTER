# Golden Food Production v4.0 — Premium Edition

Aplikasi pelaporan produksi internal **CV Golden Food Lestari** — manufaktur tepung roti.

## 🎯 Apa yang Baru di v4

### 1. Wizard Input 6-Step
Form input laporan dipecah jadi 6 step interaktif yang lebih ringan:
- **Step 1** — Info Dasar (tanggal, shift, toggle Mixing/Drying)
- **Step 2** — Mixing + Bahan Baku (digabung agar leader bisa kontrol total tepung langsung)
- **Step 3** — Drying + Metering Gas
- **Step 4** — Tenaga Kerja
- **Step 5** — Downtime + Catatan Umum
- **Step 6** — Review (print preview style A4 → siap submit)

Navigasi: **Sebelumnya** + **Selanjutnya** + **Lewati** (link kecil) + **Simpan Draft**.

### 2. Multi-Draft per Leader
- Auto-save setiap pindah step
- Leader bisa punya beberapa draft tersimpan (mis: shift 1 + shift 2 belum selesai)
- Modal pilihan saat buka "Input Laporan" — pilih lanjutkan, hapus, atau buat baru

### 3. UI Premium ala Mobile Banking
- Header gelap cokelat dengan gradient + radial gold mesh accent
- Kartu putih bersih, border-radius besar, shadow halus
- Tombol pill-shaped dengan gradient gold
- Tetap mempertahankan brand cokelat-emas Golden Food

### 4. Export Multi-Format
- **Excel (multi-sheet)** — 4 sheet: Ringkasan, Rincian Mixing, Rincian Drying, Total per Leader
- **PDF** — via Print-to-PDF dengan layout A4 portrait + kop perusahaan
- **JPEG WhatsApp** — format vertikal 1080×1920 dengan QR code

### 5. Submit Success Modal
Setelah submit laporan, langsung muncul 4 opsi: Download PDF / JPEG / Lihat Detail / Buat Baru.

## 🚀 Cara Buka

1. **Double-click** `Golden_Food_Production.html` — akan membuka di browser default
2. Atau drag & drop ke browser (Chrome/Edge/Firefox direkomendasikan)
3. **Mode online** — butuh koneksi internet untuk load library (React, SheetJS, html2canvas)

## 🔑 Akun Login Demo

| Role          | Email                              | Password    |
|---------------|------------------------------------|-------------|
| Admin         | tri.rajaroti.ka@gmail.com          | admin123    |
| Supervisor    | produksi.gflklodran@gmail.com      | super123    |
| Team Leader 1 | goldenfood.leader01@gmail.com      | leader123   |
| Team Leader 2 | goldenfood.leader02@gmail.com      | leader123   |
| Viewer        | viewer@gflklodran.com              | viewer123   |

## 📋 Fitur per Role

**Admin** — Akses semua menu, kelola Master Data, hapus laporan (password + soft delete)

**Supervisor & Team Leader** — Dashboard, Monitoring, Input Laporan, Mutasi, Edit profil sendiri

**Viewer** — Read-only access ke Dashboard, Monitoring, Mutasi

## 🧮 Aturan Bisnis

- **Shift 1**: 23:30 – 07:30 · **Shift 2**: 07:30 – 15:30 · **Shift 3**: 15:30 – 23:30
- **Auto-Calc Tepung**: Mixer Kecil 1.4 sak/batch · Mixer Besar 6 sak/batch · Tolerance ±1 sak
- **Formula Gas (PT Hartono Energi)**:
  `Sm³ = (UV1-UV2) × ((P.O+1.01325)/1.01325) × (300/(T+273)) × 1.002`
  Default: P.O=1.8 Bar · T=30°C · Harga Rp 9.000/Sm³
- **Auto-fill Meter Awal Gas** dari laporan terakhir
- **Soft Delete** laporan yang dihapus masuk arsip

## 💾 Penyimpanan Data

- Data tersimpan di **localStorage browser** (key: `gfl_app_data_v4`)
- Tetap tersimpan saat browser ditutup
- **Tidak sinkron antar perangkat** — tiap device punya data sendiri
- Untuk reset: hapus localStorage via browser DevTools

## ⚠️ Catatan Teknis

File ini **prototype/demo** untuk validasi alur sebelum migrasi ke Next.js + Supabase (sesuai PRD). Single HTML file, jalan di browser tanpa install. Multi-user di prototype ini hanya simulasi — semua akun share localStorage device yang sama.

## 🛠️ Bug yang Sudah Diperbaiki dari v3

- ✅ Input angka tidak kehilangan fokus saat mengetik
- ✅ Edit user data (profil sendiri + admin kelola user lain)
- ✅ Master data toggle aktif/non-aktif
- ✅ Dashboard cards bisa diklik ke Mutasi
- ✅ Hapus laporan dengan konfirmasi password + soft delete + activity log

---
**v4.0** · Premium Edition · CV Golden Food Lestari
