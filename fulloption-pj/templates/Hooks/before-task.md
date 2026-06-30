# Hook: Before Task — ก่อนเริ่มงาน

ทำตามขั้นตอนนี้ **ทุกครั้งก่อนลงมือ** เพื่อโหลด context ที่จำเป็น

## Checklist
1. **อ่านกฎ** — [CLAUDE.md](../CLAUDE.md) + CLAUDE.md ของ sub-project ที่จะแตะ + [PROJECT_RULES.md](../PROJECT_RULES.md)
2. **โหลด Skill ที่เกี่ยวข้อง** — สแกน [/Skills](../Skills/README.md) เลือกตาม `domain` ของงาน อ่านก่อนเขียนโค้ด
3. **เลือก Agent/บทบาท** — ดู [/Agents](../Agents/README.md) ว่างานนี้ควรใช้บทบาทไหน (`pj-pm`/`pj-sa`/`pj-dev`/`pj-qc`)
4. **ทบทวน Memory** — ความรู้เกี่ยวกับ user/โปรเจกต์ที่ถูก recall มา ตรวจว่ายังตรงกับโค้ดจริงหรือไม่
5. **ยืนยันสภาพแวดล้อม** — config/port/branch ปัจจุบัน และระวัง `.env` อาจไม่ใช่ของ production

## เกณฑ์ผ่าน
- เข้าใจ contract / convention ของโปรเจกต์
- รู้ว่ามี Skill/Gotcha ใดเกี่ยวข้องบ้าง
- มีแผนชัดเจนว่าจะแตะไฟล์ไหน ชั้นใด
