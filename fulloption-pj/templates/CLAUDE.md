# CLAUDE.md

ไฟล์นี้ให้คำแนะนำกับ Claude Code (claude.ai/code) เมื่อทำงานในโปรเจกต์นี้
> สร้างจาก baseline ของ plugin `fulloption-pj` — โปรดแก้ส่วน `TODO` ให้ตรงกับโปรเจกต์จริง

## ภาพรวมโปรเจกต์ (Project Overview)
- **ชื่อ:** {{PROJECT_NAME}}
- **Stack:** {{STACK}}
- **TODO:** อธิบายสั้น ๆ ว่าโปรเจกต์ทำอะไร, ใครใช้, มี service/โมดูลอะไรบ้าง, รันยังไง

## AI Working Rules (สำคัญ — ปฏิบัติทุกครั้ง)

โปรเจกต์นี้แยกองค์ความรู้และ Workflow ออกเป็น 3 โฟลเดอร์ + ไฟล์มาตรฐาน:

| โฟลเดอร์/ไฟล์ | หน้าที่ |
|---------------|---------|
| [`/Skills`](Skills/README.md) | how-to / gotcha ที่ใช้ซ้ำได้ เรียนรู้จากงานจริง |
| [`/Agents`](Agents/README.md) | บทบาท/หน้าที่ของ AI (runtime ใช้ subagent จาก plugin: `pj-pm`/`pj-sa`/`pj-dev`/`pj-qc`) |
| [`/Hooks`](Hooks/README.md) | Workflow ก่อน–หลังงาน (before/after task, commit, release) |
| [`PROJECT_RULES.md`](PROJECT_RULES.md) | มาตรฐานของโปรเจกต์ (contract, role, security, git ฯลฯ) |

**ลำดับการทำงานบังคับ:**
1. **ก่อนเริ่มงาน** — รัน [Hooks/before-task.md](Hooks/before-task.md): โหลด `PROJECT_RULES.md`, CLAUDE.md ที่เกี่ยวข้อง, Skill ที่เกี่ยวข้อง, ทบทวน Memory แล้วเลือกบทบาท
2. **ระหว่างทำงาน** — เคารพ `PROJECT_RULES.md` ทุกข้อ
3. **หลังทำงานเสร็จ** — รัน [Hooks/after-task.md](Hooks/after-task.md): ทดสอบ, QC, แล้ว **อัปเดต Skill / Memory / Documentation อัตโนมัติ** เมื่อมีความรู้หรือการเปลี่ยนแปลงใหม่

**กฎเหล็ก:** อัปเดตความรู้แบบ **ไม่สร้างข้อมูลซ้ำ** — ถ้ามีหัวข้อใกล้เคียงอยู่แล้วให้แก้ไฟล์เดิมและปรับ `updated:` ไม่สร้างไฟล์ใหม่ซ้อน

## เรียกใช้ด้วยคำสั่งเดียว
ติดตั้ง plugin [`fulloption-pj`](https://github.com/fluke351/FullOption_pj) แล้ว:
- พิมพ์ **`/Rules`** เพื่อดูคำสั่งและกฎทั้งหมด
- เริ่มงานด้วย **`/FullOption_pj <งาน>`**
