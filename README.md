# jmt-workflow — Claude Code Marketplace

Marketplace กลางของทีม มี plugin **`fulloption-pj`** : คำสั่งเดียว `/FullOption_pj` รัน workflow ครบวงจร
**ในโปรเจกต์ใดก็ได้** โดยปรับตามกฎของโปรเจกต์นั้นอัตโนมัติ

## ติดตั้ง (ทำครั้งเดียว ใช้ได้ทุกโปรเจกต์)

```
/plugin marketplace add fluke351/FullOption_pj
/plugin install fulloption-pj@jmt-workflow
```

> **หมายเหตุชื่อ:** repo ชื่อ `FullOption_pj` แต่ marketplace ภายในชื่อ `jmt-workflow` และ plugin ชื่อ `fulloption-pj`
> ดังนั้นคำสั่ง install ใช้ `fulloption-pj@jmt-workflow` (ไม่ใช่ `@FullOption_pj`)

> ติดตั้งจากในเครื่อง (ตอนพัฒนา) ก็ได้: `/plugin marketplace add <path>/jmt-workflow`

ติดตั้งแบบ user-level จะใช้ได้ทุกโปรเจกต์ที่เปิดด้วย Claude Code (ไม่ต้องติดตั้งซ้ำ)

## ใช้งาน

```
/FullOption_pj init                                # โปรเจกต์ใหม่: วางโครง Skills/Agents/Hooks + CLAUDE.md + PROJECT_RULES.md (กฎพื้นฐาน)
/FullOption_pj เพิ่ม endpoint ดึงรายการตามแผนก    # งานพัฒนาปกติ — รันครบ 4 ขั้น
/FullOption_pj status                              # ดูสถานะ branch/งานค้าง
/FullOption_pj commit                              # commit ตามมาตรฐาน (หรือ Hooks/commit.md ของโปรเจกต์)
/FullOption_pj release                             # เตรียม release (ต้องอนุมัติ)
```

### เริ่มโปรเจกต์ใหม่ด้วย `init`
รัน `/FullOption_pj init` ครั้งเดียว จะคัดลอก baseline templates มาวางที่รากโปรเจกต์
(ไม่ทับของเดิม) + เติมชื่อโปรเจกต์/stack ที่ตรวจพบให้อัตโนมัติ — เหลือแค่ผู้ใช้กรอกส่วน `TODO`
จากนั้น `/FullOption_pj <งาน>` จะอ่านกฎเหล่านี้เองทุกครั้ง

## ทำงานยังไง

`/FullOption_pj` เป็น orchestrator ที่:
1. **BEFORE** — ค้นและโหลดกฎของโปรเจกต์ที่เปิดอยู่ (`CLAUDE.md`, `PROJECT_RULES.md`, `Skills/`, `Hooks/`) + ตรวจ stack จริง + ทบทวน Memory
2. **เลือกบทบาท** — มอบหมาย subagent: `pj-pm` / `pj-sa` / `pj-dev` / `pj-qc`
3. **WORK** — ทำตามกฎที่โหลดมา (contract, parameterized query, ไม่รั่ว secret, กลมกลืนสไตล์เดิม)
4. **AFTER** — verify/test จริง → QC → อัปเดต Skill/Memory/Docs โดยไม่สร้างซ้ำ

> ถ้าโปรเจกต์ไม่มีไฟล์กฎเหล่านี้ จะ fallback เป็นแนวปฏิบัติทั่วไป + สไตล์โค้ดที่เห็นรอบ ๆ
> agent ทั้ง 4 เป็น **generic** จึงไม่ผูกกับ stack ใด — อ่านกฎของโปรเจกต์เองทุกครั้ง

## โครงสร้าง

```
jmt-workflow/
├── .claude-plugin/marketplace.json
└── fulloption-pj/
    ├── .claude-plugin/plugin.json
    ├── commands/FullOption_pj.md        ← /FullOption_pj
    ├── agents/  pj-pm · pj-sa · pj-dev · pj-qc
    ├── hooks/hooks.json
    └── templates/                       ← baseline ที่ /FullOption_pj init ก็อปไปวาง
        ├── CLAUDE.md · PROJECT_RULES.md
        ├── Skills/  (README · _template)
        ├── Hooks/   (README · before/after-task · commit · release)
        └── Agents/  (README)
```
