# Content Spec: Git Series (10 บทความ)

**Created by**: @PM
**Date**: 2026-02-01
**Status**: Ready for Development

---

## Overview

ชุดบทความ Git สำหรับนักพัฒนาไทย ครอบคลุมตั้งแต่พื้นฐานจนถึงขั้นสูง เสริมจากบทความ Conventional Commits ที่มีอยู่แล้ว

---

## บทความที่ 1: Git Rebase vs Merge - เมื่อไหร่ใช้อะไร

### Meta
- **Slug**: `git-rebase-vs-merge`
- **Category**: Development
- **Tags**: Git, Rebase, Merge, Version Control
- **Level**: Intermediate
- **Priority**: High

### Outline
1. ความแตกต่างพื้นฐานระหว่าง Merge และ Rebase
2. Merge: รักษาประวัติแบบ Non-destructive
3. Rebase: สร้าง Linear History ที่สะอาด
4. Golden Rule: อย่า Rebase บน Public Branch
5. Interactive Rebase (git rebase -i) สำหรับจัดระเบียบ commits
6. Hybrid Approach: ใช้ทั้งสองแบบให้เหมาะสม
7. Best Practices สำหรับทีม

### Acceptance Criteria
- [ ] อธิบายความแตกต่างชัดเจนพร้อม diagram
- [ ] มีตัวอย่าง commands สำหรับทั้งสอง approach
- [ ] มี use cases ว่าเมื่อไหร่ใช้อะไร
- [ ] มี code examples ที่รันได้จริง

---

## บทความที่ 2: การกู้คืนจากความผิดพลาดใน Git

### Meta
- **Slug**: `git-undo-mistakes`
- **Category**: Development
- **Tags**: Git, Reset, Revert, Reflog, Recovery
- **Level**: Beginner-Intermediate
- **Priority**: High

### Outline
1. ความแตกต่างระหว่าง reset, revert, และ checkout
2. Git Reset: --soft, --mixed, --hard (เมื่อไหร่ใช้แบบไหน)
3. Git Revert: ยกเลิก commit อย่างปลอดภัย
4. Git Reflog: กู้คืน commits ที่หายไป
5. Cherry-pick: เลือก commit ที่ต้องการ
6. การกู้คืนไฟล์ที่ลบไปแล้ว
7. Stash: บันทึกงานชั่วคราวก่อนทำอะไรเสี่ยง

### Acceptance Criteria
- [ ] มีตารางเปรียบเทียบ reset/revert/checkout
- [ ] มีตัวอย่าง real-world scenarios
- [ ] มี step-by-step สำหรับกู้คืนข้อมูล
- [ ] อธิบาย reflog ให้เข้าใจง่าย

---

## บทความที่ 3: Git Hooks และ Pre-commit - Automation สำหรับ Code Quality

### Meta
- **Slug**: `git-hooks-precommit`
- **Category**: Development
- **Tags**: Git, Git Hooks, Pre-commit, Automation, CI/CD
- **Level**: Intermediate-Advanced
- **Priority**: High (เสริม Conventional Commits)

### Outline
1. Git Hooks คืออะไร (client-side vs server-side)
2. Pre-commit Framework: ติดตั้งและใช้งาน
3. การตั้งค่า .pre-commit-config.yaml
4. Hooks ที่ควรมี: linting, formatting, commit message validation
5. การบังคับใช้ Conventional Commits ด้วย commitlint
6. การ integrate กับ CI/CD Pipeline
7. Best Practices: Pre-commit vs CI/CD checks

### Acceptance Criteria
- [ ] มี setup guide แบบ step-by-step
- [ ] มีตัวอย่าง config files
- [ ] เชื่อมโยงกับบทความ Conventional Commits
- [ ] มี troubleshooting section

---

## บทความที่ 4: Gitflow vs Trunk-Based Development

### Meta
- **Slug**: `git-workflow-comparison`
- **Category**: Development
- **Tags**: Git, Gitflow, Trunk-Based, Workflow, Team
- **Level**: Intermediate
- **Priority**: Medium

### Outline
1. ทำไมต้องมี Git Workflow?
2. Gitflow: โครงสร้างและข้อดี-ข้อเสีย
3. Trunk-Based Development: แนวทางสมัยใหม่
4. Feature Branch Workflow
5. GitHub Flow: ทางเลือกที่เรียบง่าย
6. การเลือก Workflow ตามขนาดทีมและ project
7. Tips สำหรับทีมไทย

### Acceptance Criteria
- [ ] มี diagram สำหรับแต่ละ workflow
- [ ] มีตารางเปรียบเทียบข้อดี-ข้อเสีย
- [ ] มี recommendations ตามขนาดทีม
- [ ] มีตัวอย่าง companies ที่ใช้แต่ละ approach

---

## บทความที่ 5: Merge Conflicts - เข้าใจและแก้ไขอย่างมืออาชีพ

### Meta
- **Slug**: `git-merge-conflicts`
- **Category**: Development
- **Tags**: Git, Merge, Conflicts, Collaboration
- **Level**: Beginner-Intermediate
- **Priority**: High

### Outline
1. ทำไม Merge Conflict ถึงเกิดขึ้น
2. การอ่านและเข้าใจ Conflict Markers
3. วิธีแก้ไข Conflicts ด้วย CLI
4. การใช้ VS Code และ GUI Tools
5. ป้องกัน Conflicts: การ pull บ่อยๆ และ communication
6. Git Rerere: จำการแก้ไข Conflicts
7. Best Practices สำหรับทีม

### Acceptance Criteria
- [ ] มีภาพอธิบาย conflict markers
- [ ] มี video/GIF แสดงการแก้ไข
- [ ] มี tips ป้องกัน conflicts
- [ ] มีตัวอย่าง real-world scenarios

---

## บทความที่ 6: Git สำหรับมือใหม่ - พื้นฐานที่ต้องรู้

### Meta
- **Slug**: `git-beginners-guide`
- **Category**: Development
- **Tags**: Git, Beginners, Tutorial, Version Control
- **Level**: Beginner
- **Priority**: Medium

### Outline
1. Version Control คืออะไร ทำไมต้องใช้
2. Git vs GitHub vs GitLab: ความแตกต่าง
3. การติดตั้งและตั้งค่า Git
4. Commands พื้นฐาน: init, add, commit, push, pull
5. การทำงานกับ Branches
6. การเชื่อมต่อกับ Remote Repository
7. แหล่งเรียนรู้เพิ่มเติมและ Resources

### Acceptance Criteria
- [ ] มี installation guide ทั้ง Windows/Mac/Linux
- [ ] มี cheatsheet commands พื้นฐาน
- [ ] มีภาพประกอบทุกขั้นตอน
- [ ] เขียนเข้าใจง่ายสำหรับมือใหม่

---

## บทความที่ 7: Advanced Git Tips - เทคนิคที่จะทำให้คุณทำงานเร็วขึ้น

### Meta
- **Slug**: `git-advanced-tips`
- **Category**: Development
- **Tags**: Git, Tips, Productivity, Advanced
- **Level**: Intermediate-Advanced
- **Priority**: Medium

### Outline
1. Git Aliases: สร้าง shortcuts สำหรับ commands ที่ใช้บ่อย
2. Interactive Staging (git add -p): commit เฉพาะส่วนที่ต้องการ
3. Git Bisect: หา commit ที่ทำให้เกิด bug
4. Git Stash: เทคนิคขั้นสูง (stash pop, apply, drop, list)
5. Git Worktrees: ทำงานหลาย branches พร้อมกัน
6. Git Diff ขั้นสูง: เปรียบเทียบ branches และ commits
7. .gitconfig tips และ global configurations

### Acceptance Criteria
- [ ] มี alias recommendations พร้อมใช้
- [ ] มีตัวอย่าง .gitconfig
- [ ] มี use cases สำหรับแต่ละ tip
- [ ] มี benchmark/comparison ก่อน-หลังใช้ tips

---

## บทความที่ 8: Git Tools และ Extensions สำหรับ VS Code

### Meta
- **Slug**: `git-vscode-tools`
- **Category**: Development
- **Tags**: Git, VS Code, Tools, Extensions, GitLens
- **Level**: Beginner-Intermediate
- **Priority**: Medium

### Outline
1. VS Code Built-in Git Features
2. GitLens: ฟีเจอร์ที่ต้องรู้
3. Git Graph: visualize commit history
4. GitHub Pull Requests & Issues Extension
5. Graphite: จัดการ Stacked PRs
6. การตั้งค่า Git ใน VS Code
7. Tips และ Shortcuts สำหรับการทำงานกับ Git

### Acceptance Criteria
- [ ] มี screenshots ของแต่ละ extension
- [ ] มี installation และ setup guide
- [ ] มี comparison table ของ extensions
- [ ] มี keyboard shortcuts รวม

---

## บทความที่ 9: Git Submodules และ Monorepo

### Meta
- **Slug**: `git-submodules-monorepo`
- **Category**: Development
- **Tags**: Git, Submodules, Monorepo, Multi-Project
- **Level**: Advanced
- **Priority**: Low

### Outline
1. Monorepo vs Multi-repo: ข้อดี-ข้อเสีย
2. Git Submodules: แนวคิดและการใช้งาน
3. การเพิ่มและอัพเดท Submodules
4. การ clone project ที่มี Submodules
5. Git Subtrees: ทางเลือกอื่น
6. Tools สำหรับ Monorepo (Lerna, Nx, Turborepo)
7. CI/CD สำหรับ Monorepo และ Submodules

### Acceptance Criteria
- [ ] มี diagram อธิบาย structure
- [ ] มี commands reference
- [ ] มีตัวอย่าง real-world projects
- [ ] มี troubleshooting section

---

## บทความที่ 10: Semantic Versioning และ Automated Releases

### Meta
- **Slug**: `semantic-versioning-releases`
- **Category**: Development
- **Tags**: Git, Semantic Versioning, Releases, CI/CD, CHANGELOG
- **Level**: Intermediate-Advanced
- **Priority**: High (เสริม Conventional Commits)

### Outline
1. Semantic Versioning คืออะไร (MAJOR.MINOR.PATCH)
2. ความเชื่อมโยงกับ Conventional Commits
3. Git Tags สำหรับ Version Management
4. semantic-release: Automation Tool
5. การ generate CHANGELOG อัตโนมัติ
6. การ integrate กับ CI/CD (GitHub Actions)
7. Best Practices สำหรับ Open Source และ Internal Projects

### Acceptance Criteria
- [ ] เชื่อมโยงกับ Conventional Commits ชัดเจน
- [ ] มี setup guide สำหรับ semantic-release
- [ ] มีตัวอย่าง GitHub Actions workflow
- [ ] มี CHANGELOG generation example

---

## Implementation Priority

| # | บทความ | Priority | เสริม CC? |
|---|--------|----------|-----------|
| 1 | Git Rebase vs Merge | High | Yes |
| 2 | Git Undo Mistakes | High | - |
| 3 | Git Hooks & Pre-commit | High | **Direct** |
| 4 | Git Workflow Comparison | Medium | Yes |
| 5 | Merge Conflicts | High | - |
| 6 | Git Beginners Guide | Medium | Foundation |
| 7 | Advanced Git Tips | Medium | - |
| 8 | Git VS Code Tools | Medium | - |
| 9 | Submodules & Monorepo | Low | - |
| 10 | Semantic Versioning | High | **Direct** |

**Recommended Order:**
1. Git Hooks & Pre-commit (เสริม CC โดยตรง)
2. Semantic Versioning (เสริม CC โดยตรง)
3. Git Rebase vs Merge
4. Git Undo Mistakes
5. Merge Conflicts
6. Git Beginners Guide
7. Git Workflow Comparison
8. Advanced Git Tips
9. Git VS Code Tools
10. Submodules & Monorepo

---

## Notes

- ทุกบทความควรมี code examples ที่รันได้จริง
- ใช้ภาษาไทยที่เข้าใจง่าย ไม่ศัพท์เทคนิคมากเกินไป
- เพิ่ม images/diagrams เพื่อให้เข้าใจง่ายขึ้น
- Link ไปยังบทความอื่นใน series เพื่อ cross-reference
