# :blue_book: คู่มือการใช้ Conventional Commits

Git commit conventional หรือ [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) เป็นรูปแบบมาตรฐานในการเขียนข้อความ commit เพื่อให้ง่ายต่อการอ่าน, สร้าง changelog, และ automation อื่นๆ เช่น Semantic Release

## :wrench: โครงสร้างของ Commit Message

```markdown
<type>[optional scope]: <description>
```

ตัวอย่าง:
```
feat(user): add login feature
fix(api): correct 500 error when token is missing
refactor(ui): simplify modal logic
```

---

## :key: ประเภท (type) ที่พบบ่อย

| ประเภท | ใช้เมื่อ... | ตัวอย่าง |
|--------|-------------|----------|
| `feat` | เพิ่มฟีเจอร์ใหม่ | `feat(auth): add forgot password` |
| `fix` | แก้บั๊ก | `fix(cart): fix total calculation error` |
| `docs` | แก้ไขเอกสาร (README, etc.) | `docs(readme): update installation guide` |
| `style` | แก้ไขเรื่อง format, white-space, semi-colon ไม่มีผลกับ logic | `style: reformat code with prettier` |
| `refactor` | ปรับปรุงโค้ด **โดยไม่เพิ่มฟีเจอร์ใหม่ และไม่แก้บั๊ก** | `refactor(auth): extract token logic to util function` |
| `test` | เพิ่มหรือแก้เทสต์ | `test(login): add unit test for token service` |
| `chore` | งานเบ็ดเตล็ด เช่น config, CI/CD, dependencies | `chore(deps): update eslint` |

---

## :speech_balloon: Q&A

<details>
<summary><strong>แล้ว `refactor` คืออะไร?</strong></summary>

--- 

`refactor` คือการ **เปลี่ยนแปลงโครงสร้างของโค้ด** ให้ดีขึ้น เช่น:

- อ่านง่ายขึ้น
- ลดความซ้ำซ้อน
- แยก function ย่อยออกมา
- เปลี่ยนชื่อให้สื่อความหมาย
- ย้าย logic ไปไว้ในที่ที่เหมาะสมกว่า

โดยที่ **"การทำงานของโปรแกรมยังเหมือนเดิม"**

### ตัวอย่าง `refactor`

```ts
// ก่อน (ซับซ้อน)
function getUser() {
  const user = localStorage.getItem('user')
  if (user) return JSON.parse(user)
  return null
}

// หลัง (refactor)
function getUser() {
  const user = localStorage.getItem('user')
  return user ? JSON.parse(user) : null
}
```

อีกตัวอย่าง:

```ts
// ก่อน
function login(user) {
  localStorage.setItem('user', JSON.stringify(user))
  localStorage.setItem('token', user.token)
}

// หลัง (refactor)
function saveUser(user) {
  localStorage.setItem('user', JSON.stringify(user))
  localStorage.setItem('token', user.token)
}

function login(user) {
  saveUser(user)
}
```
</details>

<details>
<summary><strong>แล้วการเปลี่ยน UI หรือ CSS ใช้อะไรดี?</strong></summary>

---

คำตอบคือ **ขึ้นอยู่กับเจตนาและผลลัพธ์**

| กรณี | ใช้ `type` นี้ |
|------|----------------|
| เพิ่ม UI ใหม่, component ใหม่ ที่ user ใช้งานได้ | `feat` |
| เปลี่ยน UI ที่มองเห็นชัดเจน เช่น ปรับ layout, สี, responsive ฯลฯ | `feat` *(ถ้ามีผลต่อ UX)* |
| ปรับโค้ด UI/component ภายในโดยไม่เปลี่ยนหน้าตา | `refactor` |
| เปลี่ยนเฉพาะ style เช่น CSS, SCSS, Tailwind class | `style` *(ถ้าแค่จัด format หรือแก้ spacing)* |

### ตัวอย่าง

**`feat`**
```bash
feat(ui): add dark mode support
feat(button): redesign primary button with new styles
```

**`refactor`**
```bash
refactor(button): extract styles to separate file
refactor(form): split long component into smaller parts
```

**`style`**
```bash
style(ui): reformat scss files
style(button): fix indentation
```

> ถ้ามีผลต่อ **UX ที่ user เห็นหรือใช้งาน** → `feat`  
> ถ้าปรับปรุง **โครงสร้างของโค้ด UI/component** → `refactor`  
> ถ้าแค่ **จัดระเบียบ style หรือ format** → `style`
</details>

---

## :brain: สรุปสั้นๆ

| ถ้าคุณ... | ใช้ type นี้ |
|------------|-------------|
| เปลี่ยน logic เพื่อเพิ่มความสามารถใหม่ | `feat` |
| แก้ปัญหาการทำงานของระบบ | `fix` |
| ปรับปรุงโครงสร้าง/คุณภาพของโค้ด (โดยไม่มีผลต่อ output) | `refactor` |
| จัด format หรือความสวยงามของโค้ด | `style` |

---
