# 🎙️ Broadcast Playroom

โปรแกรม TTS สำหรับอ่านแชทสดจาก Twitch / YouTube / MyLive / TikTok / KICK ด้วย edge-tts และ RVC voice conversion

> **สำหรับผู้ใช้ทั่วไป** — ดาวน์โหลดเวอร์ชันล่าสุดได้ที่ https://men9ch.com/broadcast-playroom/

---

## 📦 เวอร์ชัน

| เวอร์ชัน | ขนาด | ความสามารถ |
|----------|------|-----------|
| **Lite** | ~900 MB | edge-tts + ทุกฟีเจอร์ยกเว้น RVC |
| **Full** | ~5.7 GB | Lite + RVC voice conversion (PyTorch+CUDA) |

---

## ✨ ฟีเจอร์หลัก

### TTS & เสียง
- **edge-tts (Premwadee)** — เสียงหญิงไทย ฟรี ไม่ต้อง GPU
- **RVC voice conversion** — แปลงเสียงเป็น VTuber/อนิเมะ/ผู้ประกาศ (Full only)
- **Mixed Voice** — อ่านหลายภาษาในประโยคเดียว (ไทย+ญี่ปุ่น+ไทย)
- **อ่านชื่อ + ข้อความ** — ปรับ volume/rate ได้
- **ข้ามข้อความยาว** — ตั้ง threshold + เสียงเตือน

### การแปลภาษา
- **Google** (ฟรี) / **DeepL** / **DeepSeek v4-flash** (LLM)
- แปลเป็นไทย → TTS อ่านไทย
- แสดงคำแปลใน Live Chat + Overlay + Game Overlay (realtime)
- บังคับแปลรายบุคคล (Force translate)
- ภาษาที่ไม่รู้จัก (ฮินดี/อาหรับ) → เงียบ ไม่ error

### แพลตฟอร์ม
- **5 แพลตฟอร์ม**: Twitch / YouTube / MyLive / TikTok / KICK
- Default 3 (Twitch/YouTube/MyLive) — เปิดเพิ่มได้ใน Platform Modal (เฟือง sidebar)
- ผู้ชมนับ live / auto-reconnect

### Overlays
- **Chat Overlay (OBS)** — แสดงแชทใน OBS/Streamlabs (Browser Source)
  - 3 โหมด: Default / Theme / Special (Balloon)
- **Game Overlay** — แชทลอยเหนือเกม (transparent + click-through, Qt)
  - เปิด/ปิดได้จากใน Setting เลย (ไม่ต้องกลับหน้าหลัก)
- **Overlay+** — custom URL overlay สูงสุด 3 อัน (Streamlabs/StreamElements/alert)
  - ปรับความโปร่งใสแยกแต่ละอัน
- **Theme 54 แบบ** — Neon/Glass/Cyberpunk ฯลฯ + Pip-Boy (Fallout) + สไตล์ผู้หญิง (Sakura/Princess/Galaxy Girl ฯลฯ)
- **Playroom** — มินิเกมวิดีโอ (trigger ด้วย #)

### Event System
- รองรับ: sub/bits/raid/superchat/gift/follow/share/like/join/redeem
- เสียงแจ้งเตือน + TTS announcement (toggle ได้)
- Event List (ใหม่→เก่า)

### การจัดการ
- **NG-Replace** — คำต้องห้าม + คำแทนที่ (2 คอลัมน์ + Edit + TTS preview)
- **User Manager** — เปลี่ยนชื่อ / Block / Force translate / TTS rename + Refresh
- **Channel Points** (Twitch text-prompt rewards)
- **NG words** — 2 โหมด: hide / show_no_tts

### อำนวยความสะดวก
- **Auto-update** — ตรวจ + ดาวน์โหลด + ติดตั้งอัตโนมัติ (4 layer fallback)
- **Settings auto-save** — เปลี่ยนค่าแล้วเซฟทันที (debounce 500ms)
- **Splash screen** — ขั้นต่ำ 2.5 วิ (กันกะพริบ)
- **prefix อัตโนมัติ** — `!` สำหรับโค้ดลับ, `#` สำหรับ Playroom
- **Log rotation** — เก็บ 10 ครั้งล่าสุด + crash.log
- **Plugin System** — command plugin (config-only YAML)

---

## 🔄 Auto-Update

โปรแกรมจะตรวจอัพเดทอัตโนมัติเมื่อเปิดใช้งาน (5 วินาทีหลังเปิด)

- **Patch update** — ดาวน์โหลดและติดตั้งอัตโนมัติ (~9-33 MB)
- **Major update** — แจ้งให้ดาวน์โหลดเวอร์ชันใหม่ทั้งหมด

### ⚠️ Windows Defender / Antivirus
PyInstaller exe อาจถูก AV แจ้งเตือน (false positive) — เพิ่ม Exception:
1. Windows Security → Virus & threat protection → Manage settings
2. Add or remove exclusions → Add an exclusion → Folder
3. เลือกโฟลเดอร์ Broadcast Playroom

ดูเพิ่มเติม: [FAQ.md](FAQ.md)

---

## 📋 Release Assets

ไฟล์ที่อัพโหลดไว้ใน [Releases](https://github.com/zepiam/broadcast-playroom/releases) tag `latest`:

| ไฟล์ | หน้าที่ |
|------|---------|
| `version.json` | ⚠️ **ต้องมี lite/full block** (ไม่ใช่แค่ version+changelog) — updater อ่านไฟล์นี้ |
| `remote_version.json` | เหมือน version.json (สำรอง) |
| `patch_lite.zip` | Patch สำหรับ Lite (delta update) |
| `patch_full.zip` | Patch สำหรับ Full (delta update) |

> ⚠️ **สำคัญ**: `version.json` บน GitHub ต้องมีโครงสร้าง `{version, changelog, lite: {type, url, size}, full: {type, url, size}}` — ถ้าขาด lite/full block updater จะ fallback เป็น major (ดาวน์โหลดใหม่ทั้งโปรแกรม) ทั้งที่ควรเป็น patch

---

## 📝 Changelog ล่าสุด

### v1.8.9
- **Setting เปิดเร็วขึ้น** — lazy build + preload (แท็บ TTS/Overlay ไปเลย ไม่ค้าง)
- **Theme ใหม่ 30+ แบบ**
  - ☢️ Pip-Boy (จอเขียว Fallout)
  - 🌸 สไตล์ผู้หญิง 8 แบบ: Sakura, Princess, Macaron, Galaxy Girl, Cotton Candy, Kawaii, Mermaid, Rose Gold
  - กรอบลูกเล่น: Hologram, Graffiti, Ribbon, Cloud, Tag, Receipt, TV, Circuit ฯลฯ
- **Game Overlay toggle ใน Setting** — เปิด/ปิดได้จากใน Setting เลย
- **Loop Demo ขยาย** — 50 → 107 ข้อความ (หลากหลาย ไม่ซ้ำ)
- **Opacity แยก Default/Balloon** — set ใคร set มัน (ไม่ sync กัน)
- **กรอบ edit frame ชัด 100% เสมอ** — จัดวางได้แม่น
- **Migration reset opacity** — อัพเดทแล้วทุกค่า reset เป็น 100% อัตโนมัติ
- **ลบเบลอพื้นหลัง** — ใช้ไม่ได้จริงใน overlay

---

## 🛠️ สำหรับนักพัฒนา (Development)

### โครงสร้างโปรเจค

```
tts-for-livestream/
├── main.py                 # Entry point + splash + log rotation
├── app_gui.py              # GUI (~11000+ lines) — Main app + SettingsDialog
├── chat_queue.py           # TTS pipeline + Mixed Voice + translation
├── settings.py             # AppSettings dataclass + load/save
├── updater.py              # Auto-update (4 layer fallback)
├── build_patch.py          # สร้าง patch/full zip สำหรับ release
├── tts_lite.spec           # PyInstaller spec (Lite)
├── tts_full.spec           # PyInstaller spec (Full)
├── plugin_loader.py        # Plugin loader (command config-only)
├── plugin_api.py           # Abstract classes (TTSEngine, PlatformClient, CommandHandler)
├── rvc_engine.py           # RVC voice conversion + HuBERT cache
├── chat_twitch.py          # Twitch IRC client
├── chat_youtube.py         # YouTube chat client
├── chat_mylive.py          # MyLive Playwright client
├── chat_tiktok.py          # TikTok client
├── chat_kick.py            # KICK client
├── overlay_server.py       # OBS overlay HTTP server
├── overlay.html            # OBS overlay web page
├── game_overlay.py         # Game Overlay + Overlay+ manager (MoreOverlay)
├── game_overlay_qt.py      # Qt transparent window subprocess
├── game_overlay.html       # Game overlay web page
├── assets/                 # icon + fonts + logo
├── plugins/                # Plugin directory (commands/*.yml)
├── version.json            # เลขเวอร์ชัน local
├── web/                    # Documentation website (Node.js + Express)
└── release/                # output ของ build_patch.py (ไม่ commit)
```

### เอกสารสำหรับนักพัฒนา

| ไฟล์ | เนื้อหา |
|------|--------|
| [PLATFORM_DEV.md](PLATFORM_DEV.md) | **คู่มือเพิ่มแพลตฟอร์มใหม่** (chat/emote/event) |
| [AUDIO_DEV.md](AUDIO_DEV.md) | **คู่มือปรับแต่งเสียง** (TTS/RVC/Mixed Voice/Translation) |
| [PROJECT_NOTES.md](PROJECT_NOTES.md) | 56 บัค + วิธีแก้ + สถาปัตยกรรมลึก |
| [CONTRIBUTING.md](CONTRIBUTING.md) | Setup + code style + build + debug + gotchas |
| [PLUGIN_DEV.md](PLUGIN_DEV.md) | API reference สำหรับ plugin (Command/TTSEngine/Platform) |
| [ARCHITECTURE.md](ARCHITECTURE.md) | ภาพรวมระบบ + flow + โครงสร้างไฟล์ |
| [CHANGELOG.md](CHANGELOG.md) | ประวัติเวอร์ชั่นทั้งหมด |
| [FAQ.md](FAQ.md) | ปัญหาที่พบ + วิธีแก้ (ผู้ใช้) |

---

## 🗺️ Roadmap — สิ่งที่วางไว้ (ทำเมื่อสั่ง)

> 💡 เก็บไว้เป็นแผน ไม่ได้ทำทันที — เมื่อถึงเวลาที่มี requirement ใหม่ค่อยทำ

### 🔌 Plugin System (เชื่อม ABC ที่ยังเป็น stub)

| ลำดับ | ฟีเจอร์ | สถานะปัจจุบัน | สิ่งที่ต้องทำ |
|---|---|---|---|
| 1 | **Command Plugin (Python)** | `plugin_loader.py` สร้างแล้ว แต่ไม่ได้ import ใน `app_gui.py`/`chat_queue.py` | เชื่อม `get_plugin_loader().check_command(msg)` เข้า on_message pipeline |
| 2 | **TTSEngine Plugin** | ABC มีใน `plugin_api.py` แต่ `tts_engine.py` ไม่ได้ subclass | ทำให้ edge-tts เป็น subclass + รองรับ TTS อื่น (Google Cloud, Azure, Coqui) |
| 3 | **PlatformClient Plugin** | ABC มี แต่ client จริงไม่ได้ subclass (duck-typed) | ทำให้ client จริง inherit + รองรับ plugin loading |
| 4 | **Event Hooks** | ไม่มี | เพิ่มระบบให้ plugin รับ event (sub/bits/raid) ผ่าน callback |

### 🎨 ฟีเจอร์ที่ขยายได้ (คนอื่นต่อยอด)

| ฟีเจอร์ | วิธีเพิ่ม | อ้างอิง |
|---|---|---|
| **Command Plugin (YAML)** | สร้าง `.yml` ใน `plugins/commands/` | [PLUGIN_DEV.md](PLUGIN_DEV.md) |
| **RVC Voice Model** | วาง `.pth` ใน `rvc_models/` | [AUDIO_DEV.md](AUDIO_DEV.md) |
| **แพลตฟอร์มใหม่** | สร้าง `chat_xxx.py` + register | [PLATFORM_DEV.md](PLATFORM_DEV.md) |
| **Translation Provider** | เพิ่มใน `translator.py` | [AUDIO_DEV.md](AUDIO_DEV.md) |
| **Overlay Theme** | แก้ CSS ใน `overlay.html` | — |
| **ภาษาใหม่ (Mixed Voice)** | เพิ่มใน `VOICE_BY_LANG` | [AUDIO_DEV.md](AUDIO_DEV.md) |

### 📝 TODO อื่นๆ

- [ ] Settings > Plugins tab (ดู + เปิด/ปิด plugin)
- [ ] PyYAML ใน PyInstaller spec (สำหรับ command plugin)
- [ ] Web Wiki: User Guide (สำหรับผู้ใช้ทั่วไป ไม่ใช่ dev)
- [ ] Web Wiki: Settings Reference (อธิบายทุก setting)
- [ ] Web Wiki: Overlay/RVC/Translation Setup Guide

---

### Build

```bash
# สำคัญ: ปิดโปรแกรมก่อน build เสมอ (กัน file lock)
# สำคัญ: numpy < 2 (เพื่อ torch 2.2.2 compatibility)
pip install "numpy<2"

python -m PyInstaller tts_lite.spec --noconfirm   # Lite
python -m PyInstaller tts_full.spec --noconfirm   # Full
```

### สร้างไฟล์ Release + อัพโหลด

```bash
# 1. อัพเดท version.json (local — version + changelog อย่างเดียว)
#    ไฟล์นี้ bundle ใน exe สำหรับ get_current_version()

# 2. สร้าง patch + remote_version.json (มี lite/full block ครบ)
python build_patch.py patch lite
python build_patch.py patch full
python build_patch.py version

# 3. ⚠️ สำคัญ: สร้าง version.json แบบเต็ม (มี lite/full block) สำหรับ GitHub
#    (เหมือน remote_version.json แต่ชื่อ version.json เพราะ updater อ่านชื่อนี้)
cp release/remote_version.json release/version.json

# 4. อัพโหลดขึ้น GitHub (ต้องมี version.json + remote_version.json + patch zips)
gh release edit latest --repo zepiam/broadcast-playroom --title "vX.Y.Z" --notes "..."
gh release upload latest release/version.json release/remote_version.json \
  release/patch_lite.zip release/patch_full.zip \
  --repo zepiam/broadcast-playroom --clobber

# 5. ⚠️ ตรวจสอบว่า version.json บน GitHub มี lite/full block จริง
gh release download latest --repo zepiam/broadcast-playroom --pattern "version.json" --dir /tmp/check --clobber
cat /tmp/check/version.json  # ต้องเห็น "lite": {...} และ "full": {...}
```

### Dependencies สำคัญ
- `numpy < 2` (torch 2.2.2 compatibility)
- `collect_submodules('requests')` + `('urllib3')` ใน spec (ต้องมี! — updater ใช้)
- `certifi` (SSL certificates สำหรับ HTTPS)

### Documentation Website
```bash
cd web
npm install
node server.js  # http://localhost:3000
```
หลังบ้าน: `/admin/login` (เปลี่ยน password ใน server.js)

---

## 📝 License

Private project — สงวนลิขสิทธิ์
