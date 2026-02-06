# 🏛️ Historical Court Agent — README

## 📌 Overview

โปรเจกต์นี้เป็นตัวอย่างการสร้าง **Multi-Agent System** โดยใช้ Google ADK (Agent Development Kit) เพื่อจำลองกระบวนการ “ศาลประวัติศาสตร์” ที่ให้ AI หลาย Agent ทำงานร่วมกันในการค้นหาข้อมูลด้านบวกและด้านลบของบุคคลหรือเหตุการณ์จาก Wikipedia แล้วสรุปออกมาเป็นรายงานแบบเป็นกลาง

แนวคิดหลักของโปรเจกต์คือการเรียนรู้การออกแบบ Agent workflow เช่น

* Sequential Agent
* Parallel Agent
* Loop Agent
* State Management

ซึ่งเหมาะสำหรับงานทดลองระดับนักศึกษาปริญญาตรีที่ต้องการเข้าใจระบบ Agent orchestration

---

## ⚙️ หลักการทำงานของระบบ (How It Works)

โค้ดนี้แบ่งขั้นตอนการทำงานออกเป็น 4 ส่วนหลัก

---

### 1️⃣ Tools Definition (เครื่องมือ)

ระบบมี Tools ที่ใช้ร่วมกันระหว่าง Agent ได้แก่

#### ✅ `append_to_state`

ใช้เก็บข้อมูลลงใน state เช่น

* pos_data → ข้อมูลด้านบวก
* neg_data → ข้อมูลด้านลบ
* judge_feedback → คำสั่งจาก Judge

หลักการคือ Agent แต่ละตัวจะไม่ส่งข้อมูลตรง ๆ แต่จะบันทึกลง state เพื่อให้ Agent ตัวอื่นนำไปใช้ต่อได้

---

#### ✅ `write_file`

ใช้บันทึกรายงานสุดท้ายเป็นไฟล์ `.txt` ลงในโฟลเดอร์

```
court_records/
```

---

#### ✅ Wikipedia Tool

ใช้ LangchainTool เพื่อเรียก Wikipedia API สำหรับค้นหาข้อมูลจริง

---

## 🤖 Agents ภายในระบบ (Historical Court)

---

### 👤 Admirer Agent

หน้าที่:

* ค้นหาข้อมูลด้านบวก
* ความสำเร็จ
* ผลงานเด่น

หลักการ:

* ใช้ wikipedia tool
* บันทึกลง pos_data

---

### ⚖️ Critic Agent

หน้าที่:

* ค้นหาข้อมูลด้านลบ
* controversy
* criticism
* failures

หลักการ:

* ทำงานคู่กับ Admirer แบบขนาน (Parallel)

---

### 🧑‍⚖️ Judge Agent

หน้าที่สำคัญที่สุดใน Loop

* ตรวจสอบว่าข้อมูลสองฝั่งสมดุลหรือยัง
* ถ้าข้อมูลยังไม่พอ → เขียน feedback ลง judge_feedback
* ถ้าพอแล้ว → ใช้ exit_loop ออกจาก Loop

นี่คือแนวคิด Decision Agent

---

### 📝 Verdict Writer Agent

หน้าที่:

* อ่าน pos_data และ neg_data
* เขียนรายงานแบบ Neutral
* เซฟไฟล์ผลลัพธ์

---

## 🔄 รูปแบบ Execution ของระบบ

ระบบใช้ Agent หลายแบบร่วมกัน

---

### ✅ ParallelAgent

```
Admirer + Critic
```

ทำงานพร้อมกันเพื่อประหยัดเวลา

---

### 🔁 LoopAgent

```
Investigation → Judge → Investigation → Judge ...
```

วนลูปได้สูงสุด 4 ครั้ง เพื่อป้องกัน infinite loop

---

### ▶️ SequentialAgent

ลำดับขั้นตอนสุดท้าย:

```
trial_process → verdict_writer
```

---

## 🧠 Root Agent (Entry Point)

`historical_court_clerk` คือ Agent หลัก

หน้าที่:

1. ทักทายผู้ใช้
2. รับชื่อบุคคลหรือเหตุการณ์
3. บันทึกลง PROMPT
4. ส่งต่อไปยัง court_system

---

## 📊 Workflow ของระบบ

```
User Input
   ↓
Root Agent
   ↓
Parallel Investigation
   ├── Admirer
   └── Critic
   ↓
Judge Review (Loop)
   ↓
Verdict Writer
   ↓
Text File Output
```

---

## 📦 Dependencies

* Python
* google-adk
* langchain
* langchain-community
* python-dotenv
* google-cloud-logging

---

---

## 🎯 จุดประสงค์ของโปรเจกต์

* ฝึกออกแบบ Multi-Agent Workflow
* เข้าใจ Parallel และ Loop Agent
* เรียนรู้การจัดการ State ใน Agent System
* ทดลอง Agent Decision Making

---


