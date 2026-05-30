# 🧠 Kenapa kita masih perlu optimasi?

Walaupun LTSC kecil, Windows tetap menyimpan:

* free space random pattern
* temporary write blocks
* installer residue

Kalau langsung di-image → size tetap maksimal.

Kita perlu membuat **free space compressible** dulu.

---

# 🧱 STEP 1 — Boot VM Sekali Lagi

Start VM LTSC kamu.

Masuk desktop.

---

# 🧱 STEP 2 — Download SDelete (Tool Resmi Microsoft)

Di Edge buka:

```
https://learn.microsoft.com/sysinternals/downloads/sdelete
```

Download ZIP.

Extract ke:

```
Desktop\sdelete
```

---

# 🧱 STEP 3 — Zero Free Space ⭐ (INI MAGIC STEP)

Buka **Command Prompt as Administrator**.

Masuk folder:

```cmd
cd Desktop\sdelete
```

Jalankan:

```cmd
sdelete64.exe -z C:
```

---

## Apa yang terjadi?

Tool ini:

```
free space → diisi byte 0
```

Bukan hapus data.

Artefact tetap aman.

Ini membuat disk bisa di-compact maksimal.

⏳ Tunggu sampai selesai (5–10 menit).

---

# 🧱 STEP 4 — Shutdown (PENTING)

```
Start → Power → Shut down
```

Bukan restart.

---

# 🧱 STEP 5 — Compact VDI (HOST)

Di host PowerShell:

```powershell
cd "C:\Program Files\Oracle\VirtualBox"
```

Lalu:

```powershell
.\VBoxManage.exe modifymedium disk "C:\Users\ACER\VirtualBox VMs\win10-ltsc-forensic\win10-ltsc-forensic.vdi" --compact
```

(Proses cepat.)

Ini benar-benar mengecilkan file VDI.

---

# 🧱 STEP 6 — CEK SIZE VDI (harus kecil)

Sekarang lihat ukuran `.vdi`.

Biasanya jadi:

```
9–11 GB
```

---

# 🧱 STEP 7 — Create FINAL RAW IMG

Sekarang imaging:

```powershell
.\VBoxManage.exe clonemedium disk "C:\Users\ACER\VirtualBox VMs\win10-ltsc-forensic\win10-ltsc-forensic.vdi" "C:\Users\ACER\Downloads\Evidence.img" --format RAW
```

---

# 🎉 EXPECTED RESULT

Sekarang:

```
Evidence.img ≈ 15 GB
```

---