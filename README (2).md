# Golden Food Production — v5.0

Aplikasi web pelaporan produksi untuk **CV Golden Food Lestari** (manufaktur tepung roti).

## 🚀 Cara Pakai

### Buka Lokal
Double-click `Golden_Food_Production.html` (browser modern: Chrome/Edge/Safari/Firefox).

### Deploy ke Netlify
1. Drag & drop file `index.html` ke [Netlify Drop](https://app.netlify.com/drop), atau
2. Push ke GitHub `trirajarotika-prog/GOLDEN-TESTER` — Netlify auto-deploy.

> File `index.html` adalah duplikat dari `Golden_Food_Production.html` agar Netlify mengenalinya sebagai entry-point.

## 🔐 Akun Login

| Email | Password | Role |
|---|---|---|
| tri.rajaroti.ka@gmail.com | admin123 | Admin |
| produksi.gflklodran@gmail.com | super123 | Supervisor |
| goldenfood.leader01@gmail.com | leader123 | Team Leader |
| goldenfood.leader02@gmail.com | leader123 | Team Leader |
| viewer@gflklodran.com | viewer123 | Viewer |

---

## ✨ Yang Baru di v5.0

### 🐛 Bug Fix
- **Refresh tidak logout lagi** — session disimpan di localStorage
- **Setting Meter Gas Awal** sekarang bisa diubah di Master Data → Gas
- **Nama user tidak revert** lagi saat re-login (currentUser di-derive fresh dari data)
- **Halaman login bersih** — info demo dihapus
- **JPEG WhatsApp** — kop ganda diperbaiki, hanya 1 header, proporsi rapi

### 🆕 Fitur Baru

#### 1. Edit Laporan dengan Approval Flow
- **< 1 jam dari submit**: Leader bisa edit langsung (tidak perlu approval)
- **> 1 jam dari submit**: Leader klik "Ajukan Edit" → isi alasan → kirim ke Supervisor
- **Admin**: selalu bisa edit langsung kapan saja
- Badge status: "Bisa edit (sisa Xm)" / "Perlu pengajuan"
- Halaman **Approval** baru untuk Supervisor/Admin (muncul di bottom nav saat ada pengajuan)
- Diff view: tampilkan total Sebelum vs Sesudah

#### 2. Struktur Mixing & Drying Multi-Produk
Sekarang **1 mesin bisa menampung banyak produk**, dan tiap produk bisa multi-planning:
```
Mixer Kecil
  ├─ Produk: ECO CRUMB MIX
  │    ├─ Planning P.04158 — 70 batch
  │    └─ Planning P.04162 — 30 batch
  └─ Produk: ROYAL MIX
       └─ Planning P.04200 — 20 batch
```
Tombol "+ Tambah Planning" dan "+ Tambah Produk" diletakkan dekat input agar tidak perlu scroll panjang.

#### 3. Master Data Operator (CRUD)
- Tab baru di **Master Data** → **Operator**
- Akses: Admin & Supervisor
- 31 operator pre-loaded dari list aktual GFL
- Daftar ini muncul di Step 4 (Tenaga Kerja) saat input laporan

#### 4. Excel Export — 5 Sheet
1. **Ringkasan** — total batch, sak, gas, biaya, downtime, tepung, ragi
2. **Rincian Mixing** — per mesin/produk/planning/batch
3. **Rincian Drying** — per mesin/produk/planning/sak
4. **Rincian Downtime** ⭐ BARU — per mesin/jam/durasi/kategori/detail
5. **Total per Leader** — agregasi per Team Leader

#### 5. Stat Cards Dashboard → Auto-Filter Mutasi
Klik kartu di "Ringkasan Produksi" → langsung tampilkan rincian lengkap di Mutasi:

| Kartu | Tab Mutasi |
|---|---|
| Total Batch | Mixing (rincian semua planning) |
| Total Sak | Drying (rincian semua planning) |
| Konsumsi Gas | Gas (meter awal/akhir/Sm³/biaya) |
| Biaya Gas | Gas |
| Total Tepung | Tepung (per merk + ragi) |
| Downtime | Downtime (per kategori + detail) |

Halaman Mutasi sekarang punya **6 tab**: Semua, Mixing, Drying, Gas, Tepung, Downtime.

---

## 📋 Fitur Inti

### Wizard Input Laporan (6 Langkah)
1. **Info Dasar** — tanggal, shift (1/2/3), bagian aktif
2. **Mixing & Bahan Baku** — multi-mesin/produk/planning, 4 merk tepung, ragi, validasi tepung otomatis ±1 sak
3. **Drying & Gas** — multi-mesin/produk/planning, perhitungan gas otomatis (Sm³ + biaya)
4. **Tenaga Kerja** — operator per section (Mixing/Baking/Drying/Indexing)
5. **Downtime & Catatan** — multi-entry dengan kategori
6. **Review & Submit** — preview siap-print

### Auto-Save Draft
- Setiap berpindah step, draft otomatis tersimpan
- Bisa lanjut nanti dari Beranda (notif Draft Tersimpan)

### Auto-Calculate
- **Tepung**: Mixer Kecil 1.4 sak/batch, Mixer Besar 6 sak/batch
- **Gas**: `Sm³ = (UV1-UV2) × ((P.O+1.01325)/1.01325) × (300/(T+273)) × 1.002`
- **Biaya gas**: `Sm³ × Rp 9.000` (default)
- **Meter awal**: auto-fill dari shift sebelumnya, atau dari setup awal

### Roles & Permissions
| Aksi | Admin | Supervisor | Team Leader | Viewer |
|---|---|---|---|---|
| Buat laporan | ✅ | ✅ | ✅ | ❌ |
| Edit laporan (<1jam) | ✅ | ✅ | ✅ (own) | ❌ |
| Edit laporan (>1jam) | ✅ langsung | Approve | Ajukan | ❌ |
| Approve edit | ✅ | ✅ | ❌ | ❌ |
| Hapus laporan | ✅ | ❌ | ❌ | ❌ |
| Master Data | ✅ semua | ✅ kecuali user/gas/log | ❌ | ❌ |

### Export & Print
- **PDF** — print-optimized (A4 portrait), kop perusahaan + tanda tangan leader & supervisor
- **JPEG** — square-ish format, optimal untuk WhatsApp
- **Excel** — 5 sheet dengan filter periode

---

## 💾 Penyimpanan Data

Semua data disimpan di **localStorage browser** (per device):
- `gfl_app_data_v5` — data utama (users, reports, master data)
- `gfl_session_v5` — session login

**Migration otomatis**: data dari v4 (1 mesin → 1 produk) akan otomatis dikonversi ke v5 (1 mesin → produk[]) saat pertama kali dibuka.

> ⚠️ Data localStorage bersifat **lokal** — backup berkala via Excel export untuk arsip.

---

## 📞 Kontak

- **Perusahaan**: CV Golden Food Lestari
- **Alamat**: Jl. Sawahan, Plalangan, Klodran, Colomadu, Karanganyar 57172
- **Email**: produksi.gflklodran@gmail.com
- **Admin**: Tri Purwadi
