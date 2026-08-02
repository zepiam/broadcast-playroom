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
- **Viewer Overlay** — แสดงยอดคนดูบนจอ (overlay อิสระ — ไม่ต้องเปิด Game Overlay)
  - โหมดรวม: `👥 1,234` (ยอดรวมทุก platform)
  - โหมดแยก: `[Twitch icon] 500 [YT icon] 300` (ใช้ platform icon จริง)
  - ปรับขนาด icon + font + stroke + shadow + color
  - เลือกจัดวาง: ชิดซ้าย/กลาง/ชิดขวา + ตำแหน่ง 4 มุม
- **Overlay+** — custom URL overlay สูงสุด 3 อัน (Streamlabs/StreamElements/alert)
  - ปรับความโปร่งใสแยกแต่ละอัน
- **ปุ่ม Overlay รวม** — กดปุ่ม 🔲 เดียว → เปิด/ปิดทั้ง Game + Viewer Overlay
  - ▼ Dropdown: ซ่อนกรอบ / Game Overlay Setting / Viewer Overlay Setting
  - Hotkey ซ่อนกรอบร่วม (Ctrl+Shift+H)
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
- **Splash screen** — แยกภาพ LITE/FULL + Pixel Block loading bar + พื้นหลังโปร่งใส
- **prefix อัตโนมัติ** — `!` สำหรับโค้ดลับ, `#` สำหรับ Playroom
- **Log rotation** — เก็บ 10 ครั้งล่าสุด + crash.log
- **Plugin System** — command plugin (config-only YAML)
- **Viewer Commands** — ผู้ชมคุม TTS ผ่านแชท (`[x2]` `[p1]` `[v50]`)

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

### v1.8.19
- **👥 Viewer Overlay** — overlay อิสระแสดงยอดคนดู (แยก server ของตัวเอง)
  - โหมดรวม / แยก platform (ใช้ platform icon จริง)
  - ปรับขนาด icon + font + stroke + shadow + color
  - จัดวาง: ชิดซ้าย/กลาง/ชิดขวา + 4 มุม + จดจำตำแหน่ง
- **🎨 Splash ใหม่** — แยกภาพ LITE/FULL + Pixel Block loading bar + โปร่งใส
- **🔲 ปุ่ม Overlay รวม** — กดปุ่มเดียวเปิด/ปิดทั้ง Game + Viewer + dropdown menu
- **⌨️ Hotkey ร่วม** — Ctrl+Shift+H ซ่อนกรอบทั้งคู่
- **🔧 Job Object** — subprocess ตายอัตโนมัติเมื่อ parent ปิด/crash

### v1.8.17
- **🎮 Viewer Commands** — ผู้ชมคุม TTS ผ่านแชท (`[x2]` `[p1]` `[v50]`)
- **Voice Downloader** — 85 curated models + popup picker + status indicator

### v1.8.9
- **Setting เปิดเร็วขึ้น** — lazy build + preload
- **Theme ใหม่ 30+ แบบ** — Pip-Boy + สไตล์ผู้หญิง + กรอบลูกเล่น
- **Game Overlay toggle ใน Setting**

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
├── game_overlay.py         # Game Overlay + Overlay+ + Viewer Overlay manager
├── game_overlay_qt.py      # Qt transparent window subprocess (game/overlay+/viewer)
├── game_overlay.html       # Game overlay web page
├── viewer_overlay.html     # Viewer overlay web page (ยอดคนดู)
├── viewer_overlay_server.py # Viewer overlay HTTP server (port 8790-8800)
├── splash.py               # Splash screen (Pixel Block loading bar)
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
# ⚠️ สำคัญมาก: ทำตามลำดับนี้เท่านั้น — ผิดลำดับ = updater พัง

# 1. แก้ไขโค้ด + syntax check
python -m py_compile *.py

# 2. Bump version.json ก่อน (version + changelog + lite/full blocks)
#    ⚠️ version.json ต้องมี lite/full blocks ครบ (ไม่ใช่แค่ version+changelog)
#    build_patch.py version จะสร้างให้อัตโนมัติจาก patch sizes

# 3. Build exe (PyInstaller) — ต้องปิดโปรแกรมก่อน!
python -m PyInstaller tts_lite.spec --noconfirm
python -m PyInstaller tts_full.spec --noconfirm

# 4. สร้าง patch + version files
#    ⚠️ ต้องรันหลัง build exe เสมอ (build_patch.py sync version.json → dist/_internal/)
python build_patch.py patch lite
python build_patch.py patch full
python build_patch.py version    # สร้าง remote_version.json + version.json (เหมือนกัน)

# 5. ตรวจสอบ patch zip มี version ที่ถูกต้อง
python -c "
import zipfile, json
for f in ['release/patch_lite.zip', 'release/patch_full.zip']:
    z = zipfile.ZipFile(f)
    data = json.loads(z.read('_internal/version.json'))
    print(f'{f}: version={data.get(\"version\")}, has blocks={\"lite\" in data}')
"
# ต้องเห็น version ใหม่ + has blocks=True ทั้งคู่

# 6. อัพโหลดขึ้น GitHub
gh release upload latest release/patch_lite.zip release/patch_full.zip \
  release/remote_version.json version.json --clobber
gh release edit latest --title "Broadcast Playroom vX.Y.Z"

# 7. ⚠️ ตรวจสอบ version.json บน GitHub มี lite/full blocks จริง
gh release download latest --pattern "version.json" --dir /tmp/check --clobber
python -c "import json; d=json.load(open('/tmp/check/version.json')); print('lite:', d.get('lite',{}).get('type')); print('full:', d.get('full',{}).get('type'))"
# ต้องเห็น lite: patch / full: patch (ไม่ใช่ major)
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
