# Hook: Release — ก่อน release / deploy

ทำเฉพาะเมื่อ user สั่งให้เตรียม release/deploy

## Checklist
1. **Changelog** — สรุปการเปลี่ยนแปลงรอบนี้
2. **Smoke test** — build/start ทุก service ที่เกี่ยวข้องให้ผ่าน และเปิดใช้งานหลักได้
3. **ตรวจ environment** — `.env`/config ของสภาพแวดล้อมเป้าหมายถูกต้อง (API base, DB host, port)
4. **Migration** — ถ้ามี `*.sql`/migration ต้องระบุลำดับรันให้ชัด และมี backup
5. **ยืนยันกับ user** — release เป็น action ที่ย้อนยาก ต้องได้รับอนุมัติก่อนเสมอ
6. **อัปเดตเอกสาร** — version/changelog ถูก commit แล้ว

## เกณฑ์ผ่าน
- ทุก service build/start ผ่าน
- changelog + migration พร้อม และ user อนุมัติ
