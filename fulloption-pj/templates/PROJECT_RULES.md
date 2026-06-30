# PROJECT_RULES.md — มาตรฐานของโปรเจกต์

มาตรฐานที่ทุกคน (และ AI) ต้องยึดเมื่อทำงานในโปรเจกต์นี้
> สร้างจาก baseline ของ plugin `fulloption-pj` — เป็น **โครงเริ่มต้น** โปรดเติม/แก้ `TODO` ให้ตรงกับโปรเจกต์จริง
> ดูภาพรวมที่ [CLAUDE.md](CLAUDE.md)

## 0. โปรเจกต์ (Project)
- **ชื่อ:** {{PROJECT_NAME}}
- **Stack:** {{STACK}}

## 1. API Contract
- รูปแบบ URL: `TODO` (เช่น REST `/api/v1/{resource}` หรือ RPC `/{domain}/{action}`)
- รูปแบบ response: `TODO` (กำหนด schema มาตรฐาน เช่น `{ status, message, data }`)
- ⚠️ เมื่อกำหนดรูปแบบ/การสะกดแล้ว **ห้ามเปลี่ยนเอง** — รักษาให้สอดคล้องทั้งระบบ

## 2. Backend
- สถาปัตยกรรม: `TODO` (เช่น MVC `router → controller → model → DB`)
- การเข้าถึงฐานข้อมูล: **parameterized query เสมอ** — ห้าม string-concat ค่าจาก user ลง SQL
- Auth: `TODO` (เช่น JWT middleware บน route ที่ต้องป้องกัน)
- จัดการ connection/resource ไม่ให้รั่วหรือค้าง

## 3. Frontend
- Framework/เวอร์ชัน: `TODO` (ระบุให้ชัดเพื่อกันใช้ API ผิดเวอร์ชัน)
- การเรียก API: `TODO` (ผ่าน helper/service ตัวกลาง ไม่กระจัดกระจาย)
- State / error handling / UI library: `TODO`

## 4. Role / Permission Model
- บทบาทผู้ใช้และสิทธิ์: `TODO` (เช่น role/scope, group-based หรือ department/level guard)
- จุดที่ต้องตรวจสิทธิ์: `TODO`

## 5. Security
- ห้าม commit secret/credential (`.env`, key, token) เข้า repo
- ตรวจให้ `.gitignore` ครอบ `.env`, `*.key`, credential — ถ้ายังไม่มี `.gitignore` ให้สร้าง
- ห้าม string-concat ค่าจาก user ลง query
- ตรวจ auth/permission บนทุก route/หน้าจอที่ต้องป้องกัน

## 6. Database / Data
- Host/ฐานข้อมูลจริง: `TODO` (⚠️ ระวัง config ใน `.env` อาจไม่ใช่ตัวเดียวกับที่เปิดในเครื่องมือ admin)
- Timezone / encoding ที่ต้องระวัง: `TODO`
- เปลี่ยน schema ต้องมี migration + backup plan

## 7. Git
- ห้าม commit เข้า `main`/branch หลักตรง ๆ — แตก branch ก่อน
- Conventional Commits + บรรทัด `Co-Authored-By` (ดู [Hooks/commit.md](Hooks/commit.md))
- ไม่ใช้ `--no-verify` เว้นแต่ผู้ใช้สั่งชัดเจน

## 8. การจัดการความรู้ (Knowledge)
- **Skill** (`/Skills`) — how-to/gotcha ที่ใช้ซ้ำได้
- **Agent** (`/Agents`) — บทบาท/ขอบเขตงาน (runtime จาก plugin)
- **Hook** (`/Hooks`) — Workflow ก่อน/หลังงาน
- **Memory** — ความรู้เรื่อง user/โปรเจกต์ที่ไม่ derive จากโค้ดได้
- กฎเหล็ก: **อัปเดตเมื่อมีความรู้ใหม่ และห้ามสร้างข้อมูลซ้ำ** — แก้ไฟล์เดิมถ้ามีหัวข้อใกล้เคียง

## 9. Testing
- คำสั่งทดสอบ: `TODO` (เช่น `npm test`, `npm run lint`, `pytest`)
- ถ้าไม่มี test runner → ทดสอบด้วยมือ/Postman และ **รายงานผลตามจริง**
- ห้ามรายงานว่า "เสร็จ/ผ่าน" ถ้ายังไม่ได้ verify จริง
