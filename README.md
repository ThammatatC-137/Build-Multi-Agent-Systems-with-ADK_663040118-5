# 🏛️ Historical Court Agent (ADK Project)

โปรเจกต์นี้เป็นตัวอย่างการสร้าง Multi-Agent System โดยใช้ **Google ADK (Agent Development Kit)** ร่วมกับเครื่องมือจาก LangChain และ Wikipedia API เพื่อจำลอง “ศาลประวัติศาสตร์” (Historical Court) ที่ให้ Agent หลายตัวช่วยกันค้นหาข้อมูลด้านบวกและด้านลบของบุคคลหรือเหตุการณ์ทางประวัติศาสตร์ แล้วสรุปออกมาเป็นรายงานแบบเป็นกลาง

---

## 📌 แนวคิดของระบบ (Concept)

ระบบถูกออกแบบให้เหมือนกระบวนการพิจารณาคดีในศาล โดยแบ่งบทบาท Agent ดังนี้

* 👤 **Admirer Agent**
  ค้นหาข้อมูลด้านบวก ความสำเร็จ หรือผลงานสำคัญ

* ⚖️ **Critic Agent**
  ค้นหาข้อมูลด้านลบ ข้อโต้แย้ง หรือความขัดแย้ง

* 🧑‍⚖️ **Judge Agent**
  ตรวจสอบความสมดุลของข้อมูล และตัดสินใจว่าจะวนลูปค้นหาต่อหรือไม่

* 📝 **Verdict Writer Agent**
  สรุปรายงานแบบเป็นกลาง และบันทึกไฟล์ .txt

ระบบใช้รูปแบบการทำงานแบบ:

* `ParallelAgent` → ให้ Admirer กับ Critic ทำงานพร้อมกัน
* `LoopAgent` → ให้ Judge ตรวจสอบแล้วสั่งวนซ้ำได้
* `SequentialAgent` → เรียงขั้นตอนตั้งแต่ค้นหา → สรุปผล

---

## 🧩 โครงสร้างการทำงาน (Workflow)

```
User Input
   ↓
Root Agent (รับชื่อบุคคล)
   ↓
Trial Process (Loop)
   ├── Admirer Agent (Positive Research)
   ├── Critic Agent (Negative Research)
   └── Judge Agent (Decision)
   ↓
Verdict Writer
   ↓
Output file (.txt)
```

---

## ⚙️ เทคโนโลยีที่ใช้

* Python
* Google ADK (Agent Framework)
* LangChain Tools
* Wikipedia API
* Google Cloud Logging
* dotenv

---

## 📦 การติดตั้ง (Installation)

1️⃣ Clone repository

```
git clone https://github.com/your-username/historical-court-agent.git
cd historical-court-agent
```

2️⃣ ติดตั้ง dependencies

```
pip install -r requirements.txt
```

3️⃣ สร้างไฟล์ `.env`

```
MODEL=your_model_name
```

---

## ▶️ วิธีใช้งาน (Usage)

รันโปรแกรมหลัก:

```
python main.py
```

จากนั้นระบบจะ:

1. ทักทายผู้ใช้
2. ขอชื่อบุคคลหรือเหตุการณ์
3. ให้ Agent ค้นหาข้อมูลทั้งสองด้าน
4. สรุปผลเป็นรายงาน

ไฟล์ผลลัพธ์จะถูกบันทึกไว้ที่:

```
court_records/
```

---

## 🧠 ตัวอย่าง Input

```
Napoleon Bonaparte
Albert Einstein
World War II
```

---

## 📁 โครงสร้างไฟล์

```
project/
│
├── main.py
├── .env
├── court_records/
└── README.md
```

---

## 🎯 วัตถุประสงค์ของโปรเจกต์

* ศึกษาแนวคิด Multi-Agent System
* ทดลองใช้ Parallel และ Loop Agent
* ฝึกการออกแบบ Workflow ของ AI Agents
* เข้าใจการจัดการ state ระหว่าง agent

---


