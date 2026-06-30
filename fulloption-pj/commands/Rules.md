---
description: แสดงและอธิบายระบบกฎ/ความรู้ของโปรเจกต์ (CLAUDE.md/PROJECT_RULES.md/Skills/Agents/Hooks) + รายการคำสั่งทั้งหมดที่ใช้ได้
---

# /Rules — สรุประบบกฎ & ความรู้ของโปรเจกต์

ทำหน้าที่เป็น "สารบัญ" ให้ผู้ใช้เข้าใจว่ามีอะไรบ้าง แต่ละอย่างทำอะไรได้ และกฎจริงของโปรเจกต์นี้คืออะไร — โดยไม่ต้องจำเอง

ทำตามขั้นตอนนี้แล้วแสดงผลให้ผู้ใช้:

1. **สแกนโปรเจกต์** — เช็กว่ามีอะไรอยู่จริง: `CLAUDE.md`, `PROJECT_RULES.md`, `Skills/`, `Hooks/`, `Agents/`
2. **แสดงตาราง "องค์ประกอบของระบบ"** ด้านล่าง — ทำเครื่องหมาย ✅/➖ ว่ามี/ไม่มีในโปรเจกต์นี้
3. ถ้ามี `PROJECT_RULES.md` → **สรุปกฎสำคัญสั้น ๆ** จากไฟล์จริง (อย่าแต่งเอง อ่านจากไฟล์)
4. ถ้ามี `Skills/` → ลิสต์ Skill ที่มีจากดัชนีใน `Skills/README.md`
5. **แสดงตาราง "คำสั่งที่ใช้ได้"** ด้านล่าง
6. ถ้ายังไม่มีโครง (ไม่มี `CLAUDE.md`/`PROJECT_RULES.md`) → แนะนำให้รัน `/FullOption_pj init` ก่อน

---

## องค์ประกอบของระบบ (แต่ละอันทำอะไรได้)

| องค์ประกอบ | ทำอะไรได้ |
|-----------|-----------|
| **CLAUDE.md** | กฎการทำงานของ AI + ภาพรวมโปรเจกต์ — บอกลำดับงาน (before → ทำ → after) และชี้ไปองค์ประกอบอื่น เป็นไฟล์แรกที่ AI อ่านก่อนเริ่ม |
| **PROJECT_RULES.md** | มาตรฐานโปรเจกต์ที่ต้องยึด — API contract, backend/frontend convention, role/permission, security, git, testing, การจัดการความรู้ |
| **/Skills** | how-to / gotcha ที่ใช้ซ้ำได้ (เรียนรู้จากงานจริง) — 1 ไฟล์ = 1 เรื่อง มี frontmatter `domain`/`updated`; AI สแกนก่อนเริ่มงานตาม domain |
| **/Agents** | บทบาท/หน้าที่ของ AI — runtime ใช้ subagent จาก plugin (`pj-pm`/`pj-sa`/`pj-dev`/`pj-qc`); โฟลเดอร์นี้บันทึกข้อกำหนดบทบาทเฉพาะโปรเจกต์ |
| **/Hooks** | Workflow ก่อน–หลังงาน — `before-task` (โหลด context), `after-task` (test+QC+อัปเดตความรู้), `commit`, `release` |
| **Memory** | ความรู้เรื่อง user/โปรเจกต์ที่ไม่ derive จากโค้ดได้ (เก็บข้าม session) |

> **กฎเหล็ก:** อัปเดตความรู้เมื่อมีของใหม่ และ **ห้ามสร้างข้อมูลซ้ำ** — มีหัวข้อใกล้เคียงให้แก้ไฟล์เดิม

## บทบาท (subagent) ที่เรียกได้

| บทบาท | subagent | หน้าที่ |
|-------|----------|---------|
| PM | `pj-pm` | รับโจทย์, วางแผน/แตกงาน, ประสานทีม, ปิดงาน |
| SA | `pj-sa` | วิเคราะห์ requirement, ออกแบบ contract/flow, เขียน spec |
| DEV | `pj-dev` | ลงมือเขียน/แก้โค้ด backend/frontend/db |
| QC | `pj-qc` | ทดสอบ, review diff, ตรวจ security/role ก่อนปิดงาน |

## คำสั่งที่ใช้ได้

| คำสั่ง | ทำอะไร |
|--------|--------|
| `/FullOption_pj <งาน>` | รัน workflow ครบวงจร: before → เลือกบทบาท → ทำงานตามกฎ → verify + อัปเดตความรู้ |
| `/FullOption_pj init` | โปรเจกต์ใหม่: วางโครง Skills/Agents/Hooks + CLAUDE.md + PROJECT_RULES.md (กฎพื้นฐาน) |
| `/FullOption_pj status` | ดูสถานะ branch / งานค้าง |
| `/FullOption_pj commit` | commit ตามมาตรฐาน (หรือ `Hooks/commit.md` ของโปรเจกต์) |
| `/FullOption_pj release` | เตรียม release/deploy (ต้องขออนุมัติ) |
| `/Rules` | แสดงหน้านี้ — สารบัญกฎ & คำสั่งทั้งหมด |
