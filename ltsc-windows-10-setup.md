

# 🧱 PHASE 1 — CREATE VM (FOUNDATION YANG BENAR)

Buka **VirtualBox → New**

---

## 1️⃣ Basic Configuration

```
Name: win10-ltsc-forensic
Type: Microsoft Windows
Version: Windows 10 (64-bit)
```

Klik **Next**.

---

## 2️⃣ Hardware

Set:

```
RAM : 4096 MB
CPU : 2
```

⚠️ Jangan terlalu besar — kita ingin artefact stabil.

Klik **Next**.

---

## 3️⃣ EFI (PENTING)

Kalau ada opsi:

```
Use EFI
```

👉 **UNCHECK**

Kenapa?

* BIOS mode lebih simpel
* NTFS artefact lebih predictable
* Autopsy parsing lebih stabil.

---

## 4️⃣ Virtual Hard Disk ⭐ (INI KUNCI UTAMA)

Pilih:

```
Create a virtual hard disk now
```

---

### Hard disk settings:

```
Type: VDI
Storage: Dynamically allocated
Size: ⭐ 15 GB
```

Bukan 32GB.
Bukan 40GB.

👉 **15GB saja.**

Klik Finish.

---

# 🧱 PHASE 2 — ATTACH ISO

Settings → Storage

Di Controller SATA:

```
Empty → klik icon CD → Choose disk file
```

Pilih ISO:

```
Windows 10 Enterprise LTSC 2021.iso
```

Pastikan tampil seperti:

```
windows.vdi
Win10_LTSC.iso
```

OK.

---

# 🧱 PHASE 3 — INSTALL WINDOWS LTSC

Start VM.

---

## Language Screen

Next → Install Now.

---

## Edition Selection

Biasanya otomatis:

```
Windows 10 Enterprise LTSC
```

Next.

---

## License

Accept → Next.

---

## Installation Type

Pilih:

```
Custom: Install Windows only
```

(BUKAN Upgrade)

---

## Disk Partition

Kamu akan lihat:

```
Drive 0 Unallocated Space (~15GB)
```

Langsung:

```
Next
```

Jangan manual partition.

Windows akan auto buat layout optimal.

---

⏳ Tunggu install selesai (±10–15 menit).

---

# 🧱 PHASE 4 — OOBE SETUP (IKUTI PERSIS)

Ini penting supaya artefact bersih.

---

## Region

Indonesia / sesuai.

---

## Keyboard

US / default.

---

## Network

Kalau minta connect internet:

👉 **Skip / I don’t have internet**

(offline account lebih clean).

---

## Account Setup

Pilih:

```
Offline account
```

User:

```
student
```

Password (optional):

```
student123
```

---

## Privacy Settings ⭐

Semua:

```
OFF
OFF
OFF
OFF
OFF
OFF
```

Klik Accept.

---

## Customize Experience

Klik:

```
Skip
```

---

## Cortana

Disable / Not now.

---

Tunggu sampai desktop muncul.

---

# 🧱 PHASE 5 — POST INSTALL HARDENING (WAJIB)

Sekarang kita bikin OS ringan + forensic friendly.

---

## Disable Windows Update

WIN+R:

```
services.msc
```

Cari:

```
Windows Update
```

→ Stop
→ Startup type: Disabled.

---

## Disable SysMain

Masih di services:

```
SysMain → Disabled
```

Mengurangi noise disk.

---

## Disable Indexing

File Explorer → Right click C:

```
Properties
→ uncheck:
Allow files on this drive to have contents indexed
```

Apply → Ignore errors.

---

## Set Timezone

Settings → Time:

```
UTC+07 Jakarta
```

---

Restart sekali.

---

# 🧱 PHASE 6 — SNAPSHOT BASELINE ⭐⭐⭐

VirtualBox:

```
Machine → Take Snapshot
```

Name:

```
CLEAN_BASE
```

Ini checkpoint emas.

Kalau artefact rusak → rollback 5 detik.

---
