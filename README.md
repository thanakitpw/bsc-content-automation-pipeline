# bsc-content-pipeline

> Multi-business content pipeline plugin สำหรับ Claude Code — รองรับเพจ/ธุรกิจหลายตัว, หลาย business type, มี humanize-writing rules ที่ทำให้บทความ "ฟังเป็นคนไทย" ไม่ใช่ AI

[![Version](https://img.shields.io/badge/version-1.1.1-blue)](https://github.com/thanakitpw/bsc-content-automation-pipeline)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

## Install

### ใน Claude Code

```bash
# Add marketplace
/plugin marketplace add thanakitpw/bsc-content-automation-pipeline

# Install plugin
/plugin install bsc-content-pipeline@bsc-marketplace
```

### Update

```bash
# Refresh marketplace
/plugin marketplace update bsc-marketplace

# Update plugin to latest version
/plugin update bsc-content-pipeline
```

> หมายเหตุ: Claude Code ยังไม่มี auto-update — ต้อง run command ด้านบนเพื่อ check + ดึงเวอร์ชันใหม่

### ใน Cowork

Download `.plugin` file จาก [Releases](https://github.com/thanakitpw/bsc-content-automation-pipeline/releases) แล้วเปิดด้วย Cowork

---

## Business Types ที่รองรับ

| Type | สำหรับ |
|---|---|
| `product` | เพจขายสินค้า/บริการ — ครีม, อาหาร, คลินิก |
| `creator` | Content Creator / Educator — เพจสอน, ให้ความรู้ |
| `personal_brand` | Coach, consultant, expert |
| `hybrid` | ผสม (เช่น creator + course) |

แต่ละ type มี **คำถามตอนสร้าง profile**, **research strategy**, **structure ของบทความ**, และ **CTA pattern** ต่างกัน

## Skills (4 ตัว)

### 1. business-profile-manager

จัดการ profile แต่ละเพจ — voice, audience, products หรือ topics, visual style + style-notes (feedback loop ที่เรียนจากการแก้ของคุณ)

**Trigger**: "เพิ่มเพจ", "ตั้งโปรไฟล์", "เพจสอน X", "เก็บ style", "ดู profile"

### 2. content-research

หา topic ideas — research strategy ปรับตาม business_type:
- **product** → pain-driven (Pantip pain quote + competitor watch)
- **creator** → misconception hunt + Google PAA + niche trend
- **personal_brand** → industry commentary + client case patterns

**Trigger**: "หาเรื่องเขียน", "หา topic", "วันนี้ลงอะไรดี", "research content"

### 3. content-writer

เขียนบทความ/โพสต์ + humanize rules ที่บังคับใช้ทุกเพจ:

| ❌ ห้าม | ✅ ใช้ |
|---|---|
| งานวิจัยพบว่า / สถิติปี 2024 | "เคยเห็นว่า..." / "เพื่อนเล่ามา..." |
| stress level สูง | เครียดมาก |
| Day 1, Day 2 | วันที่ 1, วันที่ 2 |
| ในปี 2018 | เมื่อหลายปีก่อน |
| สัปดาห์ | อาทิตย์ |
| ฮ่าฮ่าฮ่า | 555 |
| ในยุคปัจจุบัน / ดังนั้น | scene/question / เลย |

มี **style-learning loop** — เมื่อคุณแก้ draft แล้วบอก "เก็บการแก้นี้เป็น style" ระบบ append เข้า `style-notes.md` ของเพจ ครั้งหน้าเขียนดีขึ้น

**Trigger**: "เขียนบทความ", "เขียนโพสต์", "draft content", "ปรับบทความ"

### 4. post-formatter ★ ใหม่ใน v1.1.0

แปลง draft (หลังแก้แล้ว) → ไฟล์ final ที่ **พร้อม copy ไปโพสต์ทันที** มี **auto-numbering ต่อเพจ** (1, 2, 3...) เพื่อจัดเรียงโพสต์ตามลำดับ

- ตัด frontmatter ออก, จัด hashtag, ตัด link ไปวาง first comment (FB)
- Auto alt-text ภาษาไทย
- Metadata footer (image path, link, char count) สำหรับ user — ไม่ paste ไปด้วย

**Trigger**: "เตรียม final", "format โพสต์", "พร้อมโพสต์", "ทำ final"

---

## Workflow

```
1. business-profile-manager  → สร้าง profile (type-aware)
2. content-research          → เลือก topic (5-10 ตัวเลือก)
3. content-writer            → ได้ draft ที่ผ่าน humanize check
4. แก้ draft → "เก็บ style"  → style-notes อัปเดต
5. post-formatter            → ได้ final/<slug>/N-<topic>.md พร้อม copy
6. paste ลงเพจจริง
```

## File Structure ที่ระบบสร้าง

```
<workspace>/
├── business-profiles/
│   ├── INDEX.md
│   └── <slug>/
│       ├── profile.yaml             # voice, audience, type-specific fields
│       ├── visual-style.yaml        # brand metadata
│       └── style-notes.md           ★ growth file
├── research/
│   └── <slug>/
│       └── YYYY-MM-DD-<topic>.md
├── drafts/                           ← work in progress (มี frontmatter)
│   └── <slug>/
│       └── YYYY-MM-DD-<topic>.md
└── final/                            ← ★ พร้อม copy ไปโพสต์ (folder ต่อ post)
    └── <slug>/
        ├── 1-<topic>/
        │   ├── 1-<topic>.md
        │   └── cover.png (optional)
        ├── 2-<topic>/
        │   └── 2-<topic>.md
        └── ...
```

## ตัวอย่าง use case

### เพจสอน "AI สำหรับ marketer"

```
1. profile creator: niche="AI marketer ไทย",
                   unique_perspective="อธิบายให้คนไม่ใช่สาย tech เข้าใจ"
2. research → "AI = ChatGPT คือ misconception" (จาก Reddit + PAA)
3. writer → hook misconception → insight → 1 takeaway → CTA save
4. (แก้ draft) → post-formatter → final/ai-edu/1-ai-misconception.md
5. copy ส่วนเหนือ "---" → paste ลง FB; metadata ใต้ "---" ใช้ดูตอน paste
```

### ร้านครีมสิว

```
1. profile product: products=[ครีมลดสิว Acne Clear],
                   target_pain="สิวฮอร์โมนเรื้อรัง"
2. research → pain quote จาก Pantip + competitor gap
3. writer → pain question hook → soft product mention → CTA ทักแชท
4. post-formatter → final/cream-shop/1-สิวฮอร์โมน.md
```

---

## Roadmap

ยังไม่ build:
- `content-planner` — calendar รายเดือน + content pillars
- `content-brief` — แยก brief จาก writer
- `pipeline-runner` — orchestration เช็ค state + flow

## Changelog

### v1.1.1 (current)
- ★ เปลี่ยน post-formatter เป็น **folder per post** — ใส่ post + cover image ที่เดียวกัน
- ลบ note ที่บอกให้รัน script (ไม่มี script ในระบบแล้ว)
- โครงใหม่: `final/<slug>/<N>-<topic>/<N>-<topic>.md`

### v1.1.0
- ★ เพิ่ม `post-formatter` skill — draft → final/<slug>/N-<topic>.md พร้อม auto-numbering
- เพิ่ม folder convention `final/` สำหรับโพสต์ที่พร้อม copy

### v1.0.0
- Initial public release — 3 skills (profile, research, writer)
- 4 business types + humanize rules + style-learning loop

---

## Contributing

ตอนนี้ plugin นี้ใช้ภายใน Best Solutions Corp — ถ้าคุณอยากใช้ + ปรับปรุง ส่ง PR ได้เลยที่ [GitHub repo](https://github.com/thanakitpw/bsc-content-automation-pipeline)

## License

[MIT](LICENSE) — Best Solutions Corp
