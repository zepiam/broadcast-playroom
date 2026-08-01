# 📋 Broadcast Playroom — Changelog

ประวัติการเปลี่ยนแปลงทั้งหมดของ Broadcast Playroom

---

## v1.8.18 (2026-08-02)

### 🔧 แก้ไข

**Live Chat**
- แก้ scrollbar ไม่ทำงาน — บังคับ CTkScrollableFrame update scrollregion หลังเพิ่มข้อความใหม่ (debounced)
- แก้ auto-scroll ดึงกลับบนสุดตลอด — ตอนนี้ถ้า user เลื่อนไปดูข้อความเก่า จะไม่ดึงกลับ

**Game Overlay**
- แก้ข้อความถูกบีบจนมองไม่เห็นตอนแชทเยอะ — `.msg` มี `flex-shrink: 0` (คงความสูง ไม่บีบ)

**Mute (ปิดการอ่าน)**
- กดปิดแล้วหยุดทันที — `clear_queues()` ล้างคิวทั้งหมด + `player.stop()` หยุดเสียงทันที (ไม่อ่านต่อจนหมดคิว)

**Memory / Performance**
- แก้ thread storm — `message_history`, `event_log`, `donate_tracker` เปลี่ยนจาก spawn-thread-per-record เป็น debounced single-writer
- แก้ `_paused_msgs` (popout) ไม่จำกัด — cap ที่ `_MAX_CHAT_ROWS` (60)
- เพิ่ม `flush()` ตอนปิดโปรแกรม (กันเสียข้อมูลจาก debounce)

**RVC**
- เลิกโหลด RVC ตอน auto-connect (เคยทำให้ RAM พุ่งตอนเปิดโปรแกรม)
- RVC โหลดเฉพาะตอน user เลือกเสียงเท่านั้น

---

## v1.8.17 (2026-07-31)

### 🎮 ใหม่ — Viewer Interaction Commands

ให้ผู้ชมควบคุม TTS ผ่านคำสั่งข้างหน้าข้อความ (ปิดไว้เป็น default — เปิดเองได้ใน Setting → TTS)

- `[x2]` ความเร็ว — `x1` ปกติ, `x2` เร็ว 2 เท่า, `x0.5` ช้าลงครึ่ง
- `[p1]` เสียงสูง/ต่ำ — 1 unit = 5Hz (`p1` = +5Hz, `p-2` = -10Hz)
- `[v50]` ความดัง — `v100` ปกติ, `v50` เบาครึ่ง, `v150` ดัง 1.5x
- รวมคำสั่งได้ เช่น `[x2][p1]สวัสดี` = เร็ว 2x + เสียงสูง 5Hz
- คำสั่งถูกตัดออกจากข้อความ (ผู้ชม/สตรีมเมอร์ไม่เห็น prefix ในแชท/overlay)
- มี cooldown ต่อ user (ปรับได้ 0-60 วินาที, default 5) ป้องกันการ spam
- ถ้าผู้ชมใช้คำสั่งซ้ำในช่วง cooldown → อ่านข้อความปกติ (ไม่ block แชท)

อ้างอิงรูปแบบคำสั่งจาก BouyomiChan command system

---

## v1.8.7 (2026-07-29)

### 🔧 แก้ไข
- Theme selector หายตอน switch mode → `pack(before=card_parent)`
- Balloon มีเงาตัวอักษรจาก Default → เพิ่ม `!important`

### 🧩 ใหม่ (Developer)
- Plugin System foundation: `plugin_loader.py` + `plugin_api.py`
- Command plugin (config-only): `plugins/commands/*.yml`
- Abstract classes: TTSEngine, PlatformClient, CommandHandler
- Developer docs: PLUGIN_DEV.md, ARCHITECTURE.md, CONTRIBUTING.md

---

## v1.8.5 (2026-07-29)

### 🔧 แก้ไข
- User Manager rename เพิ่ม checkbox "🔊 ให้ TTS อ่านชื่อนี้" + ปุ่ม "↩️ ลบการเปลี่ยนชื่อ"
- เปลี่ยน "จีนไต้หวัน" → "ไต้หวัน"

---

## v1.8.3 (2026-07-29)

### ✨ ใหม่
- **Platform Modal** — ปุ่มเฟืองใน sidebar เปิด modal เลือกแพลตฟอร์ม (เล็กๆ ติ๊กแล้ว save ทันที)

### 🔧 แก้ไข
- Settings กว้างขึ้น → 865px (tab แสดงครบ)
- Settings เปิดเร็วขึ้น (deferred tab build)

---

## v1.8.0 (2026-07-28)

### ✨ ใหม่
- **Overlay+ (➕)** — custom URL overlay สูงสุด 3 อัน ลอยเหนือเกม
  - เชื่อม Streamlabs/StreamElements/alert URL
  - Topbar `[➕|▾]` สีเหลืองตอนเปิดอยู่
  - Hotkey toggle (ctrl+shift+m) + edit (ctrl+shift+n)
  - จดจำตำแหน่ง/ขนาด/URL อัตโนมัติ
  - Toggle on/off แต่ละอันใน Settings

### 🔧 แก้ไข
- Edit Mode toggle ต้องกด 2 ครั้ง → `edit_toggle` (Qt toggle เอง)
- โหมดแปล segments แสดงต้นฉบับ → แสดงคำแปล (MyLive/YouTube/TikTok/KICK)
- MyLive Chromium download progress bar

---

## v1.7.0 (2026-07-28)

### 🔧 แก้ไข
- **Settings auto-save** — เปลี่ยนค่าแล้วเซฟทันที (debounce 500ms) ไม่ปิด dialog
- Default 3 แพลตฟอร์ม (Twitch/YouTube/MyLive)
- ปุ่มเฟืองใน sidebar

---

## v1.6.9 (2026-07-28)

### 🔧 แก้ไข
- ลด AV suspicion — staging จาก %TEMP% → install_dir

---

## v1.6.5 (2026-07-28)

### 🔧 แก้ไข
- ระบบอัพเดท 4 layer fallback + retry + Windows cert store
- Bundle requests + urllib3 + certifi

---

## v1.6.0 (2026-07-27)

### ✨ ใหม่
- **ระบบภาษาใหม่**
  - โหมดแปลแสดงคำแปลใน overlay/game overlay
  - ภาษาที่ไม่รู้จัก (ฮินดี/อาหรับ/รัสเซีย) → เงียบ ไม่ error
  - ปุ่ม abc อยู่ตลอด + dynamic tooltip + สีตามโหมด
  - ซ่อน "ภาษาที่จะอ่าน" ตอนไม่ใช้ multilang

---

## v1.5.2 (2026-07-27)

### 🔧 แก้ไข
- User Manager ประวัติข้อความเรียงผิดลำดับ → แสดงใหม่สุดบนสุด

---

## v1.5.1 (2026-07-27)

### ✨ ใหม่
- **User Manager refresh** — ปุ่ม Refresh + auto-refresh ตอน focus
- **Overlay ▾ dropdown** — Open/Copy URL/Demo/Setting
- **Tooltip ทุกปุ่ม topbar**
- **ซ่อนกระดิ่ง** ถ้าไม่มีโค้ดลับ

### 🔧 แก้ไข
- prefix อัตโนมัติ (! โค้ดลับ, # Playroom)
- NG-Replace 2 คอลัมน์
- Tab Setting รวม Blocklist เข้า Spam + เพิ่ม tab TTS

---

## v1.5.0 (2026-07-26)

### ✨ ใหม่
- **Mixed Voice TTS** — หลายเสียงอ่านต่อกันในประโยคเดียว
- **Auto Translate** — Google / DeepL / DeepSeek v4-flash
- **Event system** — sub/bits/raid/superchat/gift/follow/share/like/join/redeem
- **Auto-update** — GitHub patch system
- **Splash screen**
- **Translation display** — realtime re-render + overlay

---

## v1.0.0 (2026-07-26)

### ✨ เริ่มต้น
- TTS สำหรับอ่านแชทสด
- 5 แพลตฟอร์ม: Twitch / YouTube / MyLive / TikTok / KICK
- Chat Overlay (OBS)
- Game Overlay (Qt transparent window)
- RVC voice conversion (Full version)
- NG words + Replace patterns
- User Manager
- Channel Points (Twitch text-prompt)
- Third-party emotes (FFZ/BTTV/7TV)
