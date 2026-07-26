# 🎙️ Broadcast Playroom

โปรแกรม TTS สำหรับอ่านแชทสดจาก Twitch / YouTube / MyLive / TikTok / KICK ด้วย edge-tts และ RVC voice conversion

> **สำหรับผู้ใช้ทั่วไป** — ดาวน์โหลดเวอร์ชันล่าสุดได้ที่ https://men9ch.com/broadcast-playroom/

## 📦 เวอร์ชัน

| เวอร์ชัน | ขนาด | ความสามารถ |
|----------|------|-----------|
| **Lite** | ~900 MB | edge-tts + ทุกฟีเจอร์ยกเว้น RVC |
| **Full** | ~5.7 GB | Lite + RVC voice conversion (PyTorch+CUDA) |

## 🔄 Auto-Update

โปรแกรมจะตรวจอัพเดทอัตโนมัติเมื่อเปิดใช้งาน

- **Patch update** — ดาวน์โหลดและติดตั้งอัตโนมัติ (~20-50 MB)
- **Major update** — แจ้งให้ดาวน์โหลดเวอร์ชันใหม่ทั้งหมด

## 📋 Release Assets

ไฟล์ที่อัพโหลดไว้ใน [Releases](https://github.com/zepiam/broadcast-playroom/releases) tag `latest`:

| ไฟล์ | หน้าที่ |
|------|---------|
| `version.json` | เก็บเลขเวอร์ชันล่าสุด + changelog + URL ดาวน์โหลด |
| `patch_lite.zip` | Patch สำหรับ Lite (delta update) |
| `patch_full.zip` | Patch สำหรับ Full (delta update) |

---

## 🛠️ สำหรับนักพัฒนา (Development)

### โครงสร้างโปรเจค

```
tts-for-livestream/
├── main.py                 # Entry point
├── app_gui.py              # GUI (customtkinter)
├── settings.py             # Settings + persistence
├── updater.py              # Auto-update logic
├── build_patch.py          # สร้าง patch/full zip สำหรับ release
├── tts_lite.spec           # PyInstaller spec (Lite)
├── tts_full.spec           # PyInstaller spec (Full)
├── assets/                 # icon + fonts + logo
├── version.json            # เลขเวอร์ชัน local
└── release/                # output ของ build_patch.py (ไม่ commit)
```

### Build

```bash
# Build exe (PyInstaller onedir mode)
python -m PyInstaller tts_lite.spec --noconfirm   # Lite
python -m PyInstaller tts_full.spec --noconfirm   # Full
```

### สร้างไฟล์ Release

```bash
# 1. สร้าง patch + version.json สำหรับฝั่ง server
python build_patch.py patch lite
python build_patch.py patch full
python build_patch.py version
cp release/remote_version.json release/version.json

# 2. อัพโหลดขึ้น GitHub (ต้องล็อกอิน gh CLI แล้ว)
gh release upload latest \
  release/patch_lite.zip \
  release/patch_full.zip \
  release/version.json \
        --repo zepiam/broadcast-playroom --clobber
```

---

## 📝 License

Private project — สงวนลิขสิทธิ์
