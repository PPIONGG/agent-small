# Content Spec: Conventional Commits Article Enhancement

**Task**: ปรับปรุงบทความ Conventional Commits ให้มีเนื้อหามากขึ้น
**Owner**: @Developer
**Priority**: 🟡 Medium
**Created by**: @PM
**Date**: 2026-02-01

---

## Current Content Analysis

### สิ่งที่มีอยู่แล้ว
- รูปแบบ Commit Message (basic)
- Types 7 ประเภท (สั้นเกินไป)
- ตัวอย่าง 3 ตัวอย่าง (น้อยเกินไป)
- Breaking Changes (brief)
- ประโยชน์ 4 ข้อ

### สิ่งที่ต้องเพิ่ม
1. อธิบาย Types ละเอียดขึ้น พร้อมตัวอย่าง
2. Scope - วิธีใช้และตัวอย่าง
3. Body - วิธีเขียนและตัวอย่าง
4. Footer - วิธีใช้ต่างๆ
5. Real-world scenarios
6. Tools ที่ใช้ร่วมกัน
7. วิธี Setup ในโปรเจค
8. ข้อผิดพลาดที่พบบ่อย

---

## New Content Structure

### 1. บทนำ (เพิ่มเติม)
- Conventional Commits คืออะไร
- ทำไมถึงสำคัญ
- ใครควรใช้

### 2. รูปแบบ Commit Message (ละเอียดขึ้น)

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

**อธิบายแต่ละส่วน:**
- **type** (บังคับ): ประเภทของการเปลี่ยนแปลง
- **scope** (ไม่บังคับ): ขอบเขตที่ได้รับผลกระทบ
- **description** (บังคับ): คำอธิบายสั้นๆ
- **body** (ไม่บังคับ): รายละเอียดเพิ่มเติม
- **footer** (ไม่บังคับ): metadata เพิ่มเติม

### 3. Types ที่ใช้บ่อย (ละเอียด + ตัวอย่าง)

| Type | ความหมาย | Semantic Version | ตัวอย่าง |
|------|----------|------------------|---------|
| feat | เพิ่ม feature ใหม่ | MINOR (0.x.0) | feat: add dark mode toggle |
| fix | แก้ bug | PATCH (0.0.x) | fix: resolve login timeout |
| docs | แก้ไขเอกสาร | - | docs: update API documentation |
| style | แก้ไข formatting | - | style: format code with prettier |
| refactor | ปรับโครงสร้างโค้ด | - | refactor: extract validation logic |
| perf | ปรับปรุง performance | PATCH | perf: optimize image loading |
| test | เพิ่ม/แก้ไข tests | - | test: add unit tests for auth |
| build | แก้ไข build system | - | build: update webpack config |
| ci | แก้ไข CI/CD | - | ci: add GitHub Actions workflow |
| chore | งาน maintenance | - | chore: update dependencies |
| revert | ย้อนกลับ commit | - | revert: revert "feat: add login" |

### 4. Scope - ขอบเขตการเปลี่ยนแปลง

**ตัวอย่าง Scopes:**
- `feat(auth): add OAuth login`
- `fix(api): handle null response`
- `docs(readme): update installation steps`
- `style(button): adjust padding`
- `refactor(utils): simplify date formatting`

**Best Practices:**
- ใช้ lowercase
- ใช้คำสั้นๆ ที่สื่อความหมาย
- สอดคล้องกับโครงสร้างโปรเจค (เช่น component name, module name)

### 5. Description - คำอธิบายสั้น

**กฎการเขียน:**
- ขึ้นต้นด้วยตัวพิมพ์เล็ก
- ไม่ใส่จุด (.) ตอนจบ
- ใช้ imperative mood (add, fix, update, remove)
- ไม่เกิน 72 ตัวอักษร

**ตัวอย่างที่ดี:**
```
feat: add user profile page
fix: resolve memory leak in dashboard
docs: update API endpoints documentation
```

**ตัวอย่างที่ไม่ดี:**
```
feat: Added user profile page.     ❌ ใช้ past tense + มีจุด
fix: Fixing bug                    ❌ ใช้ gerund
docs: Updated the docs             ❌ ใช้ past tense
```

### 6. Body - รายละเอียดเพิ่มเติม

**เมื่อไหร่ควรใช้ Body:**
- เมื่อต้องอธิบายว่า "ทำไม" ถึงเปลี่ยน
- เมื่อมีหลายสิ่งที่เปลี่ยน
- เมื่อมีข้อมูลที่เป็นประโยชน์

**ตัวอย่าง:**
```
fix(auth): resolve session timeout issue

The session was expiring after 5 minutes due to
incorrect token refresh logic. This commit fixes
the refresh mechanism to properly extend the session.

Fixes #123
```

### 7. Footer - Metadata เพิ่มเติม

**การใช้งาน Footer:**

1. **Issue References:**
```
feat(api): add pagination support

Closes #456
Fixes #789
Refs #101
```

2. **Breaking Changes:**
```
feat!: remove deprecated API endpoints

BREAKING CHANGE: The following endpoints have been removed:
- GET /api/v1/users
- POST /api/v1/auth

Use /api/v2/* instead.
```

3. **Co-authors:**
```
feat: implement new design system

Co-authored-by: John Doe <john@example.com>
Co-authored-by: Jane Smith <jane@example.com>
```

4. **Reviewed-by:**
```
fix: critical security patch

Reviewed-by: Security Team <security@example.com>
```

### 8. Breaking Changes (ละเอียด)

**วิธีระบุ Breaking Change:**

1. **ใส่ ! หลัง type:**
```
feat!: drop support for Node 14
refactor!: change API response format
```

2. **ใส่ใน footer:**
```
feat: update authentication flow

BREAKING CHANGE: JWT tokens now expire after 1 hour instead of 24 hours.
Update your token refresh logic accordingly.
```

**ตัวอย่าง Real-world:**
```
feat(api)!: change user endpoint response structure

BREAKING CHANGE: The user endpoint now returns:
{
  "data": { "user": {...} },
  "meta": { "timestamp": "..." }
}

Instead of:
{
  "user": {...}
}

Migration: Update all API calls to access user data via response.data.user
```

### 9. Real-world Scenarios

**Scenario 1: เพิ่ม Feature ใหม่**
```
feat(cart): add quantity selector for products

- Add increment/decrement buttons
- Add direct input for quantity
- Validate against stock availability
- Update cart total on change

Closes #234
```

**Scenario 2: แก้ Bug**
```
fix(checkout): prevent duplicate order submission

Users were able to submit orders multiple times by
clicking the submit button rapidly. Added debounce
and disabled state to prevent this.

Fixes #567
```

**Scenario 3: Refactor**
```
refactor(auth): extract token management to separate service

- Move token logic from AuthContext to TokenService
- Add token refresh queue to prevent race conditions
- Improve error handling for expired tokens

No functional changes. Improves maintainability.
```

**Scenario 4: Performance**
```
perf(images): implement lazy loading for product gallery

- Add Intersection Observer for viewport detection
- Use placeholder images until visible
- Reduce initial page load by 40%

Tested on Chrome, Firefox, Safari
```

### 10. Tools ที่ใช้ร่วมกับ Conventional Commits

**1. commitlint - ตรวจสอบ commit message**
```bash
npm install -D @commitlint/cli @commitlint/config-conventional
```

```js
// commitlint.config.js
module.exports = {
  extends: ['@commitlint/config-conventional']
};
```

**2. husky - Git hooks**
```bash
npm install -D husky
npx husky init
echo "npx commitlint --edit \$1" > .husky/commit-msg
```

**3. commitizen - Interactive commit**
```bash
npm install -D commitizen cz-conventional-changelog
npx commitizen init cz-conventional-changelog --save-dev --save-exact
```

```json
// package.json
{
  "scripts": {
    "commit": "cz"
  }
}
```

**4. semantic-release - Auto versioning**
```bash
npm install -D semantic-release
```

**5. standard-version - CHANGELOG generation**
```bash
npm install -D standard-version
```

```json
// package.json
{
  "scripts": {
    "release": "standard-version"
  }
}
```

### 11. Quick Setup Guide

**Step 1: ติดตั้ง Dependencies**
```bash
npm install -D @commitlint/cli @commitlint/config-conventional husky
```

**Step 2: Setup Husky**
```bash
npx husky init
echo "npx commitlint --edit \$1" > .husky/commit-msg
```

**Step 3: สร้าง commitlint config**
```bash
echo "module.exports = { extends: ['@commitlint/config-conventional'] };" > commitlint.config.js
```

**Step 4: ทดสอบ**
```bash
git commit -m "test"  # ❌ จะถูก reject
git commit -m "feat: add new feature"  # ✅ ผ่าน
```

### 12. ข้อผิดพลาดที่พบบ่อย

| ผิด | ถูก | เหตุผล |
|-----|-----|--------|
| `Fix: login bug` | `fix: resolve login issue` | ใช้ lowercase, imperative |
| `feat: Added feature.` | `feat: add new feature` | ไม่ใช้ past tense, ไม่ใส่จุด |
| `update code` | `refactor: improve code structure` | ต้องระบุ type |
| `fix: fix bug` | `fix: resolve null pointer exception` | อธิบายให้ชัดเจน |
| `feat(UI): Add Button` | `feat(ui): add button component` | ใช้ lowercase ทั้งหมด |

### 13. Commit Message Examples (เพิ่มเติม)

**Features:**
```bash
feat: add user authentication
feat(auth): implement JWT refresh token
feat(ui): add dark mode toggle
feat(api): add pagination to user list
feat!: redesign authentication flow
```

**Bug Fixes:**
```bash
fix: resolve memory leak in dashboard
fix(form): validate email format correctly
fix(api): handle empty response gracefully
fix(ui): correct button alignment on mobile
```

**Documentation:**
```bash
docs: update README with installation steps
docs(api): add endpoint documentation
docs(contributing): add commit guidelines
```

**Refactoring:**
```bash
refactor: extract validation to separate module
refactor(auth): simplify token management
refactor(utils): use lodash for deep merge
```

**Performance:**
```bash
perf: lazy load images
perf(api): add response caching
perf(bundle): reduce initial load size
```

**Tests:**
```bash
test: add unit tests for auth service
test(api): add integration tests for user endpoint
test(e2e): add login flow tests
```

**Build & CI:**
```bash
build: update to webpack 5
build(deps): upgrade React to v18
ci: add GitHub Actions workflow
ci(deploy): add automatic staging deployment
```

**Chores:**
```bash
chore: update dependencies
chore(release): bump version to 1.2.0
chore(deps): remove unused packages
```

---

## Acceptance Criteria

- [ ] เนื้อหาครอบคลุมทุกหัวข้อที่ระบุ
- [ ] ตัวอย่าง code ทุกตัวถูกต้องและ copy ไปใช้ได้
- [ ] อธิบายเข้าใจง่าย เหมาะสำหรับมือใหม่
- [ ] มีตัวอย่าง Real-world scenarios
- [ ] มี Tools และ Setup guide
- [ ] Build ผ่านไม่มี errors

---

*Created by @PM | 2026-02-01*
