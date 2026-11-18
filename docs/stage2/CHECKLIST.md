# Stage 2 — GuardianBot Checklist

รอบ Build เน้นการออกแบบระบบและแผนงานที่ทำตามได้ ส่วนการประกอบและทดสอบระบบรวมเป็นงานรอบ Launch ตาม [กติกา Stage 2](https://github.com/D-Robotics/Robotics-Dream-Keeper-Challenge-Winter/blob/main/stages/stage2-build.md) และ [กติกา Stage 3](https://github.com/D-Robotics/Robotics-Dream-Keeper-Challenge-Winter/blob/main/stages/stage3-launch.md)

กำหนด Stage 2 ตามไทม์ไลน์คือ 11–26 พฤศจิกายน 2026 โดยหน้าแรกของผู้จัดระบุว่าส่งแต่ละรอบได้ยืดหยุ่นตลอดโครงการ และวันปิดส่งรวมคือ 15 ธันวาคม 2026 [ไทม์ไลน์](https://github.com/D-Robotics/Robotics-Dream-Keeper-Challenge-Winter/blob/main/TIMELINE.md) · [ประกาศโครงการ](https://github.com/D-Robotics/Robotics-Dream-Keeper-Challenge-Winter)

## 1. Proposal

- [x] มีสถานการณ์ใช้งาน ข้อจำกัด ผู้ใช้ วิธีโต้ตอบ และแนวคิดการรับรู้ ตัดสินใจ และสั่งงาน
- [x] มีจุดต่างจากเดโมและเป้าหมายวัดผลใน [Project Proposal](PROJECT_PROPOSAL.md)
- [x] ระบุ waypoint patrol เป็นงานเสริมใน Proposal, Architecture และ Roadmap
- [ ] ยืนยันวิธีนับ DOF ของแขนจากรุ่นจริง
- [x] ตรวจรูปแบบตัวเลขและหน่วยของ KPI ให้แสดงได้ชัดเจนบน GitHub

## 2. AI System Architecture

[ร่าง Architecture](ARCHITECTURE.md)

- [x] มีแผนภาพการทำงานเบื้องต้นใน [เอกสารโครงการ](../../GUARDIANBOT_PROJECT.md)
- [x] ร่างแผนภาพข้อมูลจากเซนเซอร์ผ่าน AI และการตัดสินใจไปถึงมอเตอร์หรือเซอร์โว พร้อมทางเดินข้อมูลสำหรับการบันทึกเหตุการณ์
- [x] ร่างตารางโมดูล ระบุหน้าที่ อินพุต เอาต์พุต และลักษณะเมื่อทำงานผิดพลาด
- [x] แบ่งงานระหว่าง BPU และ CPU ให้ชัด และให้เหตุผลหากมีบริการนอกบอร์ด
- [x] ร่าง ROS 2 node graph พร้อม topics, services หรือ actions, ชนิดข้อความ และอัตราที่คาดไว้

## 3. Engineering Plan และ Roadmap

[ร่าง Engineering Plan](ENGINEERING_PLAN.md) · [Roadmap](../../ROADMAP.md)

- [x] มีร่างรายการอุปกรณ์และความเสี่ยงใน [เอกสารโครงการ](../../GUARDIANBOT_PROJECT.md)
- [x] ร่าง BOM ระบุจำนวนและผู้ผลิตของรายการที่ทราบ
- [ ] ยืนยันฉลากรุ่น ผู้ขายหรือ SKU และแรงดันหรืออินเทอร์เฟซของรายการที่ยังไม่ทราบ
- [x] ระบุทางเลือกการเชื่อม RDK X5 กับ MasterPi และทำเครื่องหมายส่วนที่ยังต้องตรวจบนฮาร์ดแวร์จริง
- [x] ร่าง `ROADMAP.md` จนถึงเดโมสุดท้าย
- [x] ระบุ 5 ความเสี่ยงหลัก พร้อมวิธีลดความเสี่ยง เงื่อนไขที่ต้องลงมือ และแผนสำรอง
- [x] มีผัง GitHub ที่วางไว้ในหัวข้อถัดไป

## 4. เผยแพร่และส่ง

- [x] เผยแพร่ Proposal, Architecture, Engineering Plan และ Roadmap ใน [GitHub สาธารณะของโปรเจกต์](https://github.com/Sorawit-2005/Robotics-Dream-Keeper-Challenge-Winter) แล้ว
- [ ] โพสต์สรุป Stage 2 พร้อมลิงก์งานใน Discord thread ส่วนตัวและบันทึก permalink
- [ ] อัปเดตไฟล์ Showcase เดิมของโปรเจกต์ผ่าน PR ไปยัง repo ของผู้จัด
- [ ] ตรวจลิงก์และเก็บให้เปิดได้ตลอดช่วงตัดสิน 16–31 ธันวาคม

## ผัง GitHub ที่แนะนำ

```text
Repo สาธารณะของ GuardianBot
├── README.md
├── GUARDIANBOT_PROJECT.md
├── ROADMAP.md                       # แผนจนถึงเดโมสุดท้าย
├── stages/state 1/
│   ├── STAGE1_IGNITE.md
│   └── โฟลเดอร์ภาพหลักฐานทั้งสาม Challenge
├── docs/stage2/
│   ├── CHECKLIST.md
│   ├── PROJECT_PROPOSAL.md
│   ├── ARCHITECTURE.md              # ร่างแบบระบบ
│   └── ENGINEERING_PLAN.md          # ร่าง BOM และแผนวิศวกรรม
├── src/                            # โค้ดเมื่อเริ่มพัฒนา
├── launch/                         # ไฟล์เปิดระบบ ROS 2
├── models/                         # โมเดลหรือวิธีดาวน์โหลดพร้อมไลเซนส์
├── config/                         # ค่าตั้งระบบ
└── tests/                          # การทดสอบ
```

ใน fork ของ repo ผู้จัด ให้ใช้ `projects/Sorawit-Project-GuardianBot.md` เป็นชื่อที่เสนอสำหรับหน้า Showcase และอัปเดตไฟล์เดียวกันตลอดทั้งสามรอบ ตาม [คู่มือส่ง Showcase PR](https://github.com/D-Robotics/Robotics-Dream-Keeper-Challenge-Winter/blob/main/docs/github-pr-guide.md)
