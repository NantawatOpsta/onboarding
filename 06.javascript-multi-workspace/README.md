# JavaScript Multi-Workspace

เรียนรู้วิธีการจัดการโปรเจกต์ JavaScript ที่มีหลาย workspace โดยใช้เครื่องมือ Yarn Workspaces เพื่อเพิ่มประสิทธิภาพในการพัฒนาและการจัดการ dependencies

อ่านวิธีการตั้งค่าและใช้งานได้ที่: https://classic.yarnpkg.com/en/docs/workspaces/

## ติดตั้ง Node.js และ Yarn

ติดตั้ง nvm (Node Version Manager) เพื่อจัดการเวอร์ชันของ Node.js ได้ง่ายขึ้น:
https://github.com/nvm-sh/nvm

ติดตั้ง Node.js เวอร์ชันล่าสุดผ่าน nvm:

```bash
nvm install node
nvm use node
```

## เริ่มทดการลองโปรเจกต์

การสร้าง Yarn Workspaces โดยมี 2 packages: ui (Vite+Storybook) และ web (Next.js)

my-monorepo/
├── package.json (Root)
├── packages/
│ ├── ui/ (Vite + Storybook -> @workspace/ui)
│ └── web/ (Next.js App -> ใช้งาน @workspace/ui)

#### ขั้นตอนที่ 1: สร้าง Root Workspace

เริ่มจากการสร้างโฟลเดอร์หลักและตั้งค่า Yarn Workspaces

1.1 สร้างโฟลเดอร์และ initialize:

```bash
mkdir my-monorepo
cd my-monorepo
yarn init -y
```

1.2 แก้ไขไฟล์ package.json ที่ root: เปิดไฟล์ package.json แล้วเพิ่มบรรทัด "workspaces" และ "private": true เข้าไปครับ

```json
{
    "name": "my-monorepo",
    "private": true,
    "workspaces": ["packages/*"]
}
```

#### ขั้นตอนที่ 2: สร้าง Workspace 1 (UI Library)

เราจะใช้ Vite ในการ setup environment และลง Storybook

2.1 สร้างโฟลเดอร์สำหรับ workspace ui:

```bash
mkdir packages
cd packages
yarn create vite ui --template react-ts
```

2.2 ตั้งชื่อ Package: เปิดไฟล์ packages/ui/package.json และเปลี่ยน name ให้เป็นชื่อที่มี Scope (เพื่อให้ import ง่ายและไม่ซ้ำใคร) เช่น @workspace/ui

```json
{
  "name": "@workspace/ui",
  "version": "1.0.0",
  "main": "./src/main.tsx",
  ...
}
```

2.3 ติดตั้ง Storybook: เข้าไปในโฟลเดอร์ ui แล้วรันคำสั่ง (เลือก yes หากมีคำถาม):

```bash
cd ui
npx storybook@latest init
```

2.4 สร้างไฟล์สำหรับ Export Component: เพื่อให้ Next.js เรียกใช้ได้ง่าย เราควรสร้างไฟล์ index.ts เพื่อรวม export

packages/ui/src/index.ts

```typescript
// ตัวอย่างการ export component ปุ่มที่ Storybook สร้างมาให้
export { Button } from "./stories/Button";
export type { ButtonProps } from "./stories/Button";
```

สำคัญ: อัปเดต packages/ui/package.json ให้ชี้ main และ types มาที่ไฟล์นี้ (เพื่อให้ Next.js หาเจอโดยไม่ต้อง Build)

```json
{
  "name": "@workspace/ui",
  "version": "0.0.0",
  "type": "module",
  "main": "./src/index.ts",
  "types": "./src/index.ts",
  ...
}
```

#### ขั้นตอนที่ 3: สร้าง Workspace 2 (Next.js App)

กลับไปที่โฟลเดอร์ packages แล้วสร้าง Next.js

3.1 สร้าง Next.js app:

```bash
# ถอยกลับไปที่ packages/
cd ..
npx create-next-app@latest web --typescript --eslint
# กด Enter เลือก default settings ได้เลย
```

3.2 เปลี่ยนชื่อ Package (Optional): เข้าไปที่ packages/web/package.json เปลี่ยนชื่อเป็น @workspace/web เพื่อความเป็นระเบียบ

#### ขั้นตอนที่ 4: การสร้าง Dependency (เชื่อม Workspace)

4.1 สั่ง Install ข้าม Workspace: รันคำสั่งนี้ที่ Root ของ Monorepo (หรือเข้าไปใน packages/web ก็ได้):

```bash
yarn workspace @workspace/web add @workspace/ui
```

(คำสั่งนี้จะไปแก้ package.json ของ web และทำการ link folder ui เข้ามาให้เหมือนเป็น node_module ตัวหนึ่ง)

ตรวจสอบไฟล์ packages/web/package.json จะเห็น:

```json
"dependencies": {
  "@workspace/ui": "*",
  ...
}
```

4.2 ตั้งค่า Next.js ให้รองรับ Monorepo (Transpile): เนื่องจากเรา import โค้ด TypeScript ดิบๆ จาก ui (ไม่ได้ build เป็น js ก่อน) เราต้องบอก Next.js ให้ช่วย Compile โค้ดจาก package นี้ด้วย

เปิดไฟล์ packages/web/next.config.ts (หรือ .js):

```typescript
import type { NextConfig } from "next";

const nextConfig: NextConfig = {
    // เพิ่มบรรทัดนี้สำคัญมาก!
    transpilePackages: ["@workspace/ui"],
};

export default nextConfig;
```

#### ขั้นตอนที่ 5: ทดสอบใช้งาน (Integration)

ตอนนี้เราพร้อมเรียกใช้ Component แล้ว

5.1 แก้ไขไฟล์หน้าแรกของ Next.js: เปิด packages/web/src/app/page.tsx

```typescript
import { Button } from "@workspace/ui"; // Import ได้เลยเหมือน lib ทั่วไป

export default function Home() {
  return (
    <main style={{ padding: 50 }}>
      <h1>Hello Monorepo</h1>
      <Button primary label="Button from UI Workspace" />
    </main>
  );
}
```

#### ขั้นตอนที่ 6: การรันโปรเจกต์

รัน Storybook (UI):

```bash
yarn workspace @workspace/ui storybook
```

รัน Next.js (Web):

```bash
yarn workspace @workspace/web dev
```
