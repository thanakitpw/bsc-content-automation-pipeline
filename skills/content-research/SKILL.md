---
name: content-research
description: หา topic ideas สำหรับบทความ — strategy ตาม business_type (web + social listening + misconception). ส่ง 5-10 topic ให้เลือก. Trigger "หาเรื่องเขียน", "หา topic", "research content".
---

# Content Research

## Purpose

ค้นหาและเสนอ topic ideas สำหรับธุรกิจที่ระบุ — research strategy + angle ที่เสนอ ปรับตาม `business_type` ของเพจ

## Preflight: หา Active Business + Type

ก่อนเริ่ม research:

1. ตรวจ working memory ว่ามี active business หรือไม่
2. ถ้าไม่มี — อ่าน `business-profiles/INDEX.md`
   - ไม่มีไฟล์/profile — บอกผู้ใช้ "ยังไม่มี business profile กรุณารัน business-profile-manager ก่อน" หยุด
   - มี profile 1 ตัว — ใช้ตัวนั้น confirm กับผู้ใช้
   - มีหลายตัว — AskUserQuestion เลือก
3. โหลด `business-profiles/<slug>/profile.yaml`
4. ★ **อ่าน `business_type`** — strategy ตอนถัดไปขึ้นอยู่กับค่านี้

ถ้าไม่มี `business_type` (profile เก่าจาก v0.1) — ถามผู้ใช้แล้วอัปเดต profile ก่อน research

## Research Strategy by Type

ดู `references/research-by-type.md` สำหรับรายละเอียด — ตรงนี้คือสรุป

### `product` — Pain-driven research

โหลดจาก profile: `products[].target_pain`, `target_audience.pain_points`

**Track 1 — Web Trend**: `<industry> trend 2026`, `<product> pantip`, `<product> ปัญหา`
**Track 2 — Social Listening**: หา pain quote ใน Pantip/Reddit/FB groups — ใช้ phrase ตรงจากคนจริง
**Track 3 — Competitor**: ดูเพจคู่แข่งโพสต์อะไร angle ไหน — หา gap

**Topic angle**: pain question → solution → soft mention product
**CTA fit**: purchase / dm

### `creator` — Question + Misconception research ★

โหลดจาก profile: `niche`, `topics_covered`, `target_audience.questions_they_ask`, `unique_perspective`

**Track 1 — Curiosity Gap**:
- ค้น `"<niche> คืออะไร"`, `"<niche> ทำงานยังไง"`, `"<niche> beginner"`
- ดู Google PAA (People Also Ask) — ★ source ที่ดีสุดสำหรับ creator
- หา Wikipedia/blog ที่อธิบาย <niche> — เห็นว่าคนค้นเรื่องไหนใต้หัวข้อใหญ่

**Track 2 — Misconception Hunt** ★ exclusive to creator:
- ค้น `"misconception about <niche>"`, `"<niche> มีคนเข้าใจผิด"`, `"common mistakes <niche>"`
- ดู Reddit/Pantip thread ที่คน "แก้" ความเข้าใจผิดของคนอื่น
- เก็บ misconception เป็น hook material — creator content ที่ "เริ่มจากแก้ความเข้าใจผิด" engagement สูง

**Track 3 — Niche Trend**:
- ดู newsletter/blog/podcast ใน niche นั้น 2-3 แห่ง
- หาเรื่องที่เพิ่งมีคนพูดถึง (ใหม่พอที่จะเป็น "first explainer ในไทย")
- ดูเพจ creator คู่แข่งใน niche เดียวกัน — gap analysis

**Topic angle**: misconception → reveal → explanation → 1 takeaway
**CTA fit**: save / follow / share / comment

### `personal_brand` — Case + Insight research

โหลดจาก profile: `professional_role`, `unique_perspective`, `target_audience.audience_outcome`

**Track 1 — Industry Commentary**:
- ค้น `"<industry> news 2026"`, `"<industry> เปลี่ยนแปลง"`, recent industry reports
- หา event/news ที่ผู้เชี่ยวชาญ comment ได้

**Track 2 — Client Situation Patterns**:
- ค้น pain ของ client ใน niche
- ดู case study ใน LinkedIn/blog — หา pattern ที่ผู้เชี่ยวชาญเจอบ่อย แล้วทำ post

**Track 3 — Peer Watch**:
- ดูคนสายเดียวกันใน LinkedIn/Twitter โพสต์อะไร
- หา angle ที่ unique_perspective ของผู้ใช้ไปต่างจากคนอื่นได้

**Topic angle**: observation/case → analysis (ใช้ expertise) → recommendation
**CTA fit**: dm / website / register

### `hybrid`

ดู `primary_component` ใน profile — ใช้ strategy ของ component นั้นเป็นหลัก
+ research strategy ของ component รองสำหรับ slot ที่ pillar = Promo

## Topic Idea Output Format

แต่ละ topic ต้องมี 5 ฟิลด์:

1. **title** — Question/Hook (ตรงกับวิธีคนเสิร์ช)
2. **angle** — มุมมอง:
   - product: "personal story" / "step-by-step" / "myth-busting"
   - creator: "misconception reveal" / "deep-dive explainer" / "framework intro" / "trend explainer"
   - personal_brand: "case observation" / "industry commentary" / "framework from experience"
3. **why_fit** — 1 ประโยคบอกว่าเหมาะกับเพจนี้เพราะอะไร (อ้างอิง profile fields):
   - product → audience.pain_points / products.target_pain
   - creator → questions_they_ask / unique_perspective
   - personal_brand → professional_role / unique_perspective
4. **search_intent** — information / decision / entertainment / inspiration
5. **source_signal** — Track ไหน + signal (เช่น "Reddit thread 500 upvotes", "competitor ยังไม่ครอบคลุม", "Google PAA แสดงเป็นคำถามแรก")

แสดง topic list เป็น numbered list ใน Markdown ก่อนใช้ AskUserQuestion

## Selection — AskUserQuestion

หลังแสดง list ใช้ AskUserQuestion (multiSelect: false):
- options: 4 ตัวจาก list (top 4 score สูงสุด)
- ถ้า list มีมากกว่า 4 — บอก "ตัวอื่นดูได้ในตารางด้านบน หรือพิมพ์เลข"

## Save Research Output

หลังผู้ใช้เลือก:

Save ที่ `research/<slug>/<YYYY-MM-DD>-<topic-slug>.md` รูปแบบ:

```markdown
# Research: <topic title>

**Business**: <slug> (<business_type>)
**Date**: YYYY-MM-DD
**Selected**: yes
**Search Intent**: <intent>
**Suggested Angle**: <angle>

## Why This Topic

<why_fit + source_signal>

## Source Material

### Track 1
- ...

### Track 2
- Pantip: <link> — "<excerpt>"
- ...

### Track 3
- <competitor>: angle <X> — gap คือ <Y>

## Reference Quotes (ใช้เป็น hook)

> "<quote จากคนจริง>"
> — <source>, <date>

## Type-specific notes

(เก็บข้อมูลเฉพาะ type — เช่น ถ้า creator: list ของ misconceptions ที่อาจ apply กับบทความนี้)

## Other Considered Topics (not selected)

1. <title> — <reason>
```

แสดงสรุป:
- "เลือก: <title>"
- "Saved at: research/<slug>/<file>.md"
- "Next: รัน content-writer เพื่อแปลง research → draft"

## Skip Research (Bring Your Own Topic)

ถ้าผู้ใช้บอก "ฉันมี topic ในใจแล้ว เรื่อง X" หรือ "research เพิ่มเรื่อง X":

- ข้าม Track 3 ถ้าเร็ว
- Track 1+2 ทำเหมือนเดิมแต่ scope ตาม topic — หา supporting material, quote, related angle
- ไม่ AskUserQuestion เลือก — save ตรงๆ ที่ `research/<slug>/<date>-<user-topic>.md`

## Quality Bar

ห้าม output:
- topic ที่กว้างเกินกว่า profile.niche
- topic ที่ AI generate ลอยๆ ไม่มี source ใน Track 1-3
- หัวข้อที่อ้างอิง stats/event แต่ไม่ระบุแหล่ง
- (creator) topic ที่ไม่ตรง topics_covered — ถ้าเจอ ถามผู้ใช้ว่า expand topics_covered หรือเปลี่ยน topic

ถ้าหา signal ไม่เจอ — ลด scope แล้ว retry ห้ามแต่งเรื่อง

## See Also

- `references/research-by-type.md` ★ — รายละเอียด strategy แต่ละ type
- `references/search-queries.md` — query templates ตาม industry/niche
- `references/topic-quality.md` — เกณฑ์ scoring topic
