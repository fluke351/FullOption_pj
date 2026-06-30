# Hook: Commit — ก่อน commit

ทำเฉพาะเมื่อ user สั่งให้ commit/push

## Checklist
1. **Branch** — ห้าม commit ตรงเข้า `main`/branch หลัก หากอยู่บนนั้นให้แตก branch ก่อน
2. **ตรวจ diff** — `git diff` ดูว่าเปลี่ยนเฉพาะที่ตั้งใจ ไม่มีไฟล์หลุด (เช่น `.env`, ข้อมูลทดสอบ)
3. **ไม่มี secret** — ไม่มี key/credential/token ใน diff
4. **Message format** — Conventional Commits:
   ```
   feat(<scope>): ...    fix(<scope>): ...    chore: ...    docs: ...
   ```
   ลงท้ายด้วย:
   ```
   Co-Authored-By: Claude <noreply@anthropic.com>
   ```
5. **ไม่ใช้ `--no-verify`** หรือข้าม hook เว้นแต่ user สั่งชัดเจน — ถ้า hook fail ให้แก้ต้นเหตุ

## เกณฑ์ผ่าน
- diff สะอาด, message สื่อความหมาย, อยู่บน branch ที่ถูกต้อง
