# Claude Instructions

## เริ่มต้นใช้งาน (ทำทันทีเมื่อเริ่ม conversation)

**ถาม User ก่อนทำอะไรทั้งหมด:**
```
"จะทำงานกับ project ไหนครับ?"
- ระบุชื่อ project ที่มีอยู่
- หรือพิมพ์ "new" เพื่อสร้าง project ใหม่
```

**ถ้า User ตอบ "new":**
1. ถามชื่อ project ใหม่
2. สร้างโฟลเดอร์ `projects/{project-name}/`
3. สร้างไฟล์เริ่มต้น: `TODO.md`, `specs.md`, `CHANGELOG.md`
4. สร้าง `project.json` (ถาม path ไปยัง codebase จริง)

**ถ้า User ระบุชื่อ project ที่มีอยู่:**
- อ่าน `projects/{project-name}/project.json` เพื่อรู้ว่า codebase อยู่ที่ไหน
- ดำเนินการ Auto Status Check ตามปกติ

---

## Auto Status Check (หลังเลือก project)

**หลังจาก User ระบุ project แล้ว ต้องทำทันที:**

1. อ่าน `projects/{project-name}/project.json` - รู้ path ไปยัง codebase
2. อ่าน `projects/{project-name}/TODO.md` - ดูสถานะงาน
3. หา task ที่อยู่ใน **In Progress** section
4. แสดงสรุปให้ User:

```
สถานะปัจจุบัน: {project-name}
Codebase: {path จาก project.json}

งานที่กำลังทำ:
- [{Status}] {Task Name}
  - Owner: @{Role}
  - Priority: {Priority}

ควรทำงานเป็น: @{Owner Role}
เพื่อ: {อธิบายสั้นๆ ว่าต้องทำอะไร}
```

**ถ้าไม่มีงาน In Progress:** แสดงรายการ Up Next หรือบอกว่าไม่มีงานค้าง

---

## project.json - เชื่อม Agent กับ Codebase

ทุก project ต้องมี `project.json` ที่บอกว่า codebase จริงอยู่ที่ไหน:

```json
{
  "name": "devtalk-blog",
  "description": "Next.js blog for tech articles",
  "path": "c:\\Users\\tamma\\OneDrive\\Desktop\\devtalk-blog",
  "tech": "nextjs",
  "commands": {
    "dev": "npm run dev",
    "build": "npm run build",
    "test": "npm run check"
  },
  "scan": {
    "include": ["src/", "app/", "components/"],
    "exclude": ["node_modules/", ".next/", "dist/"]
  }
}
```

### ใครใช้ project.json

| Role | ใช้ field | เพื่อ |
|------|----------|------|
| Scout | `path`, `tech`, `scan` | scan codebase สร้าง PROJECT-SUMMARY.md |
| Developer | `path`, `commands` | อ่าน code จริง, รัน dev/build |
| QA | `path`, `commands.test` | รัน test, ตรวจ code |
| DevOps | `path`, `commands.build` | build และ deploy |
| Designer | (ผ่าน PROJECT-SUMMARY.md) | เห็น existing components |
| PM | (ผ่าน PROJECT-SUMMARY.md) | เห็น existing features |

---

## IMPORTANT: Agent Workflow

เมื่อผู้ใช้ระบุ role (pm, designer, developer, qa, devops) **ต้องทำตามขั้นตอนนี้ก่อนทำงานใดๆ**:

### Step 0: ระบุ Project (สำคัญมาก!)

ก่อนทำอะไร ต้องรู้ว่าทำงานกับ project ไหน

1. ดูว่า User บอก project name มาหรือไม่:
   - "ทำ devtalk-blog" → project = `devtalk-blog`
   - "project: my-app" → project = `my-app`

2. **ถ้า User ไม่ได้บอก → ถาม User ก่อน:**
   ```
   "กรุณาระบุชื่อ project ที่ต้องการทำงานด้วยครับ
   เช่น: devtalk-blog, my-app, etc."
   ```

3. Project data จะอยู่ที่: `projects/{project-name}/`
   - `projects/devtalk-blog/project.json` ← codebase config
   - `projects/devtalk-blog/TODO.md`
   - `projects/devtalk-blog/specs.md`
   - `projects/devtalk-blog/CHANGELOG.md`
   - `projects/devtalk-blog/PROJECT-SUMMARY.md` ← สร้างโดย Scout

### Step 1: อ่านไฟล์ (ห้ามข้าม)
1. อ่าน `README.md` - เข้าใจ workflow ของทีม
2. อ่าน agent file ของ role นั้น (เช่น `pm.md`)
3. อ่าน `projects/{project-name}/project.json` - รู้ path ไปยัง codebase
4. อ่าน `projects/{project-name}/TODO.md` - ดู task ปัจจุบัน
5. อ่าน `projects/{project-name}/PROJECT-SUMMARY.md` - เข้าใจโครงสร้าง project (ถ้ามี)

### Step 2: ทำตาม role เท่านั้น
- **PM**: สร้าง specs/task เท่านั้น → ห้าม code
- **Designer**: ออกแบบ UI/UX → ห้าม code
- **Developer**: code ตาม task ที่มีอยู่ (ใช้ path จาก project.json ไปอ่าน/แก้ code จริง)
- **QA**: ทดสอบ, สร้าง report
- **DevOps**: deploy, อัพเดท CHANGELOG
- **Scout**: scan codebase สร้าง/อัพเดท PROJECT-SUMMARY.md

### Step 3: อัพเดท TODO.md และส่งต่อ
- อัพเดท status ใน TODO.md
- ส่งต่องานให้ role ถัดไปตาม workflow

## Workflow
```
PM → Designer → Developer → QA → อัพเดท PROJECT-SUMMARY.md → DevOps
```

**หลัง QA ผ่าน:** ให้อัพเดท `PROJECT-SUMMARY.md` ก่อนส่งต่อ DevOps
- เพิ่ม modules, components, routes, API endpoints ที่สร้างใหม่
- อัพเดท section ที่เปลี่ยน (เช่น Tech Stack, Dependencies)
- ไม่ต้อง rewrite ทั้งไฟล์ แค่อัพเดทส่วนที่เกี่ยวข้อง

**ห้ามข้าม role หรือทำงานแทน role อื่น**

**Scout** ใช้ได้ตลอดเวลา ไม่ต้องอยู่ใน workflow:
- ก่อนเริ่มงานใหม่ → `scout` (full scan)
- ระหว่างงาน เมื่อ code เปลี่ยน → `scout update`

---

## Deep Commands

แต่ละ role มี **Deep Commands** เฉพาะทางเพื่อทำงานได้เต็มประสิทธิภาพ:

| Role | Deep Commands | ใช้ทำอะไร |
|------|---------------|----------|
| PM | `deep research` | ศึกษา market, competitors, user needs |
| Designer | `deep research` + `deep scan` | หา design patterns, ดู existing components |
| Developer | `deep scan` + `deep research` | เข้าใจ codebase, ศึกษา solutions |
| QA | `deep scan` | หา bugs, security issues, edge cases |
| DevOps | `deep scan` | วิเคราะห์ infrastructure, CI/CD |

### Auto-trigger
Agent ควรใช้ deep commands **อัตโนมัติ** เมื่อ:
- เริ่มงานใหม่ที่ไม่เคยทำมาก่อน
- เจอปัญหาที่ซับซ้อน
- ต้องการข้อมูลเพิ่มเติมก่อนตัดสินใจ

> ดูรายละเอียด Deep Commands ของแต่ละ role ในไฟล์ agent นั้นๆ
