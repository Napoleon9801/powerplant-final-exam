# PowerPlant Final Exam — แนวข้อสอบ & สูตรทั้งหมด

> กระดาษจด A4 **1 แผ่น** เข้าห้องสอบได้  
> ข้อสอบ 50 คะแนน: ปรนัย 60 ข้อ (20 คะแนน) + อัตนัย 6 ข้อ × 5 คะแนน (30 คะแนน)

---

## ⏱ Strategy

- **ชั่วโมงแรก** → ทำ Choice ให้เสร็จ (60 ข้อ)
- **ชั่วโมงที่เหลือ** → ดูข้อเขียน 6 ข้อก่อน → ทำข้อที่ทำได้ก่อน
- ข้อเขียนข้อไหนยาก → ข้ามก่อน กลับมาทีหลัง

---

## 📝 ส่วนที่ 1 — ปรนัย 60 ข้อ (เน้นทฤษฎี)

| บทที่ | หัวข้อ | จำนวน | หมายเหตุ |
|-------|--------|-------|---------|
| 6 | Economic Load Dispatch | 10 ข้อ | ทฤษฎี 9 + คำนวณง่าย 1 |
| 7 | AGC | 10 ข้อ | ทฤษฎีล้วน |
| 8 | Substation | 15 ข้อ | ทฤษฎีล้วน |
| 9 | Smart Grid | 15 ข้อ | ทฤษฎีล้วน (protocol, ตัวย่อ, SBO, Gateway) |
| 10 | Protection | 10 ข้อ | ทฤษฎี 9 + คำนวณ 1 |

---

## 📐 ส่วนที่ 2 — อัตนัย 6 ข้อ × 5 คะแนน

---

### ข้อที่ 1 — Ch6: Economic Load Dispatch (Priority List)

**โจทย์:** ให้ cost function แต่ละ unit → จัดลำดับ priority โดยพิจารณา **Average Cost** หรือ **IC** ที่จุด **Min / Average / Max** (อาจารย์กำหนดให้เลือกค่าเดียว)

#### Cost Function & Incremental Cost

```
F_i(P_i) = a_i + b_i·P_i + c_i·P_i²   [฿/h]
IC_i = dF_i/dP_i = b_i + 2·c_i·P_i    [฿/MWh]
```

#### วิธีทำ Priority List (Field Cost Base List)

1. อ่านโจทย์ว่าให้ใช้ P_test = Min, Average (=(Pmin+Pmax)/2), หรือ Max
2. คำนวณ Average Cost = F_i(P_test) / P_test สำหรับแต่ละ unit
3. เรียงลำดับ: **Average Cost ต่ำสุด = Priority 1** (เปิดใช้งานก่อน)
4. เพิ่ม unit ทีละตัวจนครบ demand แต่ละ time period

#### วิธีทำ IC-based Priority

1. คำนวณ IC = b + 2c·P_test สำหรับแต่ละ unit
2. **IC ต่ำ = Priority สูง** (เปิดใช้งานก่อน)

#### Lambda Iteration (ถ้าออก)

```
เงื่อนไข: λ* = IC_1 = IC_2 = ... = IC_n
P_i = (λ* − b_i) / (2·c_i)
P_i,min ≤ P_i ≤ P_i,max (fix ถ้าเกิน limit)
ΣP_i = P_D (demand)
```

---

### ข้อที่ 2 — Ch7: AGC Multi-Area (ΔP และ ACE)

**โจทย์:** ให้ระบบ 2 หรือ 3 Area → คำนวณ ΔP_tie และ ACE → บอกว่าแต่ละ Area ควร **เพิ่มหรือลด** Generation

#### สูตร ACE

```
ACE_i = ΔP_tie,i + B_i × Δf

ΔP_tie,i = actual tie-line power − scheduled tie-line power
B_i      = Frequency Bias [MW/Hz] (มักกำหนดมาให้)
Δf       = f_actual − f_nominal [Hz]
```

#### 2-Area System

```
ACE_1 = ΔP_tie,12 + B_1·Δf
ACE_2 = ΔP_tie,21 + B_2·Δf
ΔP_tie,21 = −ΔP_tie,12  (สมดุล tie-line)
```

#### 3-Area System

```
ACE_i = ΔP_tie,net,i + B_i·Δf
ΔP_tie,net,i = ผลรวม power flow ออกจาก Area i (+ = ส่งออก)
```

#### การแปลผล

| ACE | ความหมาย | ต้องทำ |
|-----|----------|--------|
| **ACE > 0** | ผลิตมากเกินหรือส่งออกเกิน scheduled | **ลด Generation ↓** |
| **ACE < 0** | ผลิตน้อยเกินหรือรับเข้าเกิน scheduled | **เพิ่ม Generation ↑** |
| ACE = 0 | สมดุล | คง Generation |

#### Power Balance ใน Area

```
ΔP_G,i − ΔP_D,i = ΔP_tie,net,i
ถ้า demand เพิ่ม (ΔP_D > 0) → ΔP_tie_net < 0 → ACE < 0 → เพิ่ม Gen
```

---

### ข้อที่ 3 — Ch8: Bus Arrangement (วาดรูป)

**โจทย์:** ให้ Single Line Diagram → กำหนด Bus Type ให้วาด

#### 6 ประเภท Bus Arrangement

| # | ชื่อ | CB/Feeder | Reliability | หลักการ |
|---|------|-----------|-------------|---------|
| 1 | Single Bus | 1 | ต่ำ | Bus เดียว, CB 1 ตัว/feeder |
| 2 | Main & Transfer | 1+bus coupler | ปานกลาง | Bus หลัก + Bus สำรอง, ซ่อมได้ไม่ตัดไฟ |
| 3 | Double Bus Single Breaker | 1 | ปานกลาง | 2 Bus + selector switch, Bus coupler CB |
| 4 | Double Bus Double Breaker | 2 | สูง | 2 Bus, 2 CB/feeder, CB 1 ตัวเสียยังทำงาน |
| 5 | Ring Bus | 1 | สูง | CBs เชื่อมเป็นวงแหวน, n feeder = n CB |
| 6 | Breaker and a Half | 1.5 | สูงมาก | 3 CB / 2 feeder, CB กลางใช้ร่วม |

#### Topology Diagrams (จำไปวาด)

**① Single Bus**
```
───[CB]───[CB]───[CB]───
═══════════BUS═══════════
    F1        F2      F3
```

**② Main & Transfer Bus**
```
═══════BUS-MAIN══════
─[CB]─────┼─────[CB]─
   (bypass SW)
═══════BUS-TRANSFER══
         [BCB]
```

**③ Double Bus Single Breaker**
```
════════BUS-1═══════
   SW-1    SW-2
───[CB]────────[CB]──
   SW-2    SW-1
════════BUS-2═══════
[BUS COUPLER CB ตรงกลาง]
```

**④ Double Bus Double Breaker**
```
════════BUS-1═══════
[CB1]         [CB1]
 F1─●          ●─F2
[CB2]         [CB2]
════════BUS-2═══════
```

**⑤ Ring Bus**
```
[CB1]────[CB2]
  │              │
F1─●          ●─F2
  │              │
[CB4]────[CB3]
           │
          ●─F3 (ตรงกลาง CB3-CB4)
```

**⑥ Breaker and a Half**
```
══════════BUS-1══════════
[CB-1A]        [CB-1B]
F1─●──[CB-TIE]──●─F2
[CB-2A]        [CB-2B]
══════════BUS-2══════════
(3 CB กลางแนว: CB-1A, CB-TIE, CB-2A ต่อกัน)
```

---

### ข้อที่ 4 — Ch8: Touch & Step Voltage

**โจทย์:** ให้ค่า soil resistivity (ρ), fault clearing time (t_s) → คำนวณ E_touch และ E_step ที่ยอมรับได้ → เปรียบกับค่าวัดจริง

#### สูตร (IEEE 80)

```
E_touch_allowable = (1000 + 1.5·Cs·ρs) × K / √t_s   [V]
E_step_allowable  = (1000 + 6·Cs·ρs)   × K / √t_s   [V]
```

#### ค่าคงที่ K

| Body Weight | K |
|-------------|---|
| 50 kg | **0.116** |
| 70 kg | **0.157** |

#### ตัวแปร

- `Cs` = derating factor ผิวชั้นบน (ถ้าไม่มี gravel = **1.0**)
- `ρs` = resistivity ผิวชั้นบน (Ω·m) — ถ้าไม่มีชั้นบน ใช้ ρs = ρ ดิน
- `t_s` = fault clearing time (s)

#### การสรุปผล

```
E_measured ≤ E_allowable  →  ✓ SAFE
E_measured > E_allowable  →  ✗ UNSAFE (ต้องปรับปรุง ground grid)
```

#### ตัวอย่าง

```
ρ = 100 Ω·m, Cs = 1.0, ρs = 100 Ω·m, t_s = 0.5 s, คน 50 kg

E_touch = (1000 + 1.5×1.0×100) × 0.116/√0.5
        = (1000 + 150) × 0.116/0.707
        = 1150 × 0.164
        = 188.6 V

E_step = (1000 + 6×1.0×100) × 0.116/√0.5
       = 1600 × 0.164
       = 262.4 V
```

---

### ข้อที่ 5 — Ch8: Ground Grid Resistance (R_G)

**โจทย์:** ให้รูปตารางกราวด์กริด → คำนวณ R_G

#### Sverak Formula (IEEE 80)

```
R_G = ρ × [ 1/L_T  +  1/√(20·A) × (1 + 1/(1 + h·√(20/A))) ]   [Ω]
```

#### ตัวแปร

| Symbol | ความหมาย | หน่วย |
|--------|----------|-------|
| ρ | Soil Resistivity | Ω·m |
| L_T | ความยาวรวมสายกราวด์ทั้งหมด | m |
| A | พื้นที่กริด (กว้าง × ยาว) | m² |
| h | ความลึกของการฝัง (burial depth) | **m** ← ⚠ |

> **⚠ อาจารย์เน้น:** ระวังหน่วยของ h — ถ้าโจทย์ให้เป็น cm หรือ ft ต้องแปลงเป็น m ก่อน

#### วิธีอ่านรูปกริด

1. ดูขนาดกริด: กว้าง (W) × ยาว (L) → **A = W × L**
2. นับเส้น:
   - แนวนอน n_h เส้น ยาว L แต่ละเส้น → ความยาว = n_h × L
   - แนวตั้ง n_v เส้น ยาว W แต่ละเส้น → ความยาว = n_v × W
   - **L_T = n_h × L + n_v × W** + Ground rods (ถ้ามี)
3. อ่าน h และ ρ จากโจทย์
4. แทนสมการ

---

### ข้อที่ 6 — Ch10: Relay Setting (เลือกค่าเองทั้งหมด)

**โจทย์:** ให้ระบบ (I_load, I_fault) → ออกแบบ relay setting ทั้งหมด → คำนวณ trip time T

#### Step 1: เลือก CT Ratio

```
CTR = I_load_primary / 5 A  (ปัดขึ้นเป็น Standard Ratio)
Standard: 50/5, 75/5, 100/5, 150/5, 200/5, 300/5, 400/5, 500/5, 600/5, 800/5
```

> เลือก CTR ให้ I_load_secondary = I_load/CTR ≈ 5A (หรือน้อยกว่า)

#### Step 2: เลือก Pick-up Current (I_p)

```
I_p = K × I_load_secondary   [K = 1.25 ถึง 1.5]
I_load_secondary = I_load / CTR

เลือก tap ที่มีบน relay: 50%, 75%, 100%, 125%, 150%, 175%, 200% ของ 5A
= 2.5, 3.75, 5, 6.25, 7.5, 8.75, 10 A
```

> I_p ต้องน้อยกว่า I_fault_secondary/2 เพื่อ sensitivity

#### Step 3: คำนวณ PSM

```
PSM = I_fault_secondary / I_p
    = (I_fault / CTR) / I_p
```

#### Step 4: เลือก TMS

```
TMS ช่วง: 0.025 ถึง 1.0
เลือกเพื่อให้ T ตามต้องการ หรือ coordinate กับ relay downstream
```

#### Step 5: คำนวณ Trip Time T (IDMT)

```
Standard Inverse (SI):    T = TMS × 0.14   / (PSM^0.02 − 1)
Very Inverse (VI):        T = TMS × 13.5   / (PSM − 1)
Extremely Inverse (EI):   T = TMS × 80     / (PSM² − 1)
Long Time Inverse (LTI):  T = TMS × 120    / (PSM − 1)
```

#### ตัวอย่างครบ

```
โจทย์: I_load = 200 A, I_fault = 2000 A, ต้องการ T ≈ 0.4 s, ใช้ Very Inverse

Step 1: CTR = 200/5 = 40 → เลือก 200/5 (CTR = 40)
Step 2: I_load_sec = 200/40 = 5A → I_p = 1.25 × 5 = 6.25A → เลือก tap 125% = 6.25A
Step 3: I_fault_sec = 2000/40 = 50A | PSM = 50/6.25 = 8.0
Step 4: T_desired = 0.4s → TMS = T / (13.5/(PSM−1))
        = 0.4 / (13.5/7) = 0.4 / 1.929 = 0.207 → เลือก TMS = 0.2
Step 5: T = 0.2 × 13.5 / (8−1) = 0.2 × 1.929 = 0.386 s ≈ 0.4 s ✓
```

---

## 🔑 Ch9 — Theory สำคัญสำหรับ Choice 15 ข้อ

### Protocol Summary

| | Modbus | DNP3 | IEC-104 | IEC 61850 |
|---|--------|------|---------|-----------|
| ยุค | 1979 | 1993 | 2000s | ปัจจุบัน |
| Architecture | Master-Slave | Master-Outstation | Control-RTU | Peer-to-Peer |
| Communication | Polling only | Poll + **Event** | Cyclic + Spontaneous | Peer-to-peer |
| Data Model | Register | **Object** | ASDU | **Logical Node** |
| Event Report | ❌ | ✅ | บางส่วน | ✅ |
| Timestamp | ❌ | ✅ ms | ✅ | ✅ Very High |
| Network | Serial/TCP | Serial/TCP | TCP/IP | **Ethernet** |
| Protection Msg | ❌ | ❌ | ❌ | **GOOSE <4ms** |
| Security | ❌ | DNP3-SA | บางส่วน | มี |
| ใช้ใน | Factory/PLC | PEA/MEA SCADA | Europe/Asia national | Digital Substation |

### Modbus Data Types

| Type | Address | Description |
|------|---------|-------------|
| Coil | 0xxxx | Digital Output (DO) |
| Discrete Input | 1xxxx | Digital Input (DI) |
| Input Register | 3xxxx | Analog Input (16-bit RO) |
| **Holding Register** | 4xxxx | Analog Output/Memory (16-bit R/W) |

**Function Codes:** 01=Read Coil | 02=Read DI | **03=Read HR ★** | 04=Read IR | 05=Write Coil | 06=Write Reg | 16=Write Multiple

### DNP3 Event Classes

| Class | Priority | ตัวอย่าง |
|-------|----------|---------|
| 1 | High | Breaker Trip |
| 2 | Medium | Alarm |
| 3 | Low | Status Change |
| 0 | Static | Measurement |

**Poll Order:** Class 1 → 2 → 3 → 0

### IEC 61850 Services

| Service | ใช้สำหรับ | Latency |
|---------|----------|---------|
| **MMS** | SCADA monitoring/control | Normal |
| **GOOSE** | Protection signaling | **< 4 ms** |
| **SV** | Current/Voltage sampling | Very Fast |

**Logical Nodes:** XCBR=CB | PTOC=Overcurrent | MMXU=Measurement | CSWI=Switch Control

### SBO (Select Before Operate)

**ขั้นตอน:**
1. **SELECT** → เลือกอุปกรณ์ → ระบบตรวจ Interlock → "Selected OK" + เปิด Timer (10–30 s)
2. **OPERATE** → กดคำสั่ง → ระบบตรวจ Interlock อีกครั้ง → ส่งคำสั่ง → Feedback
3. **TIMEOUT** → ถ้าเกินเวลา → ต้อง Select ใหม่

**SBO ช่วยลด Human Error อย่างไร:**
- ป้องกันคลิกผิด Device (บังคับเห็นชื่อชัดเจนใน Select)
- ระบบตรวจ Interlock Logic ก่อนทุกครั้ง
- Timeout ป้องกัน Double Command
- ถ้าไม่มี SBO → DS ปิดขณะมีไฟ → Arc Flash, Blackout

**BCU = Bay Control Unit** รับคำสั่ง SBO จาก SCADA ตรวจ Interlock ที่ Bay

### Gateway หน้าที่ 5 ประการ

1. **Protocol Conversion** — IEC 61850 ↔ IEC-104/DNP3/Modbus
2. **Data Concentration** — รวมข้อมูล IED → SCADA
3. **Event & Timestamp** — SOE, Event Buffer
4. **Control Command** — ส่งคำสั่งจาก SCADA → Field
5. **Cybersecurity** — Authentication, Encryption, Firewall

### คำย่อสำคัญ Ch9

| ย่อ | ชื่อเต็ม |
|-----|---------|
| SCADA | Supervisory Control and Data Acquisition |
| EMS | Energy Management System |
| DAS | Distribution Automation System |
| HMI | Human Machine Interface |
| IED | Intelligent Electronic Device |
| RTU | Remote Terminal Unit |
| GOOSE | Generic Object-Oriented Substation Event |
| MMS | Manufacturing Message Specification |
| SV | Sampled Values |
| SBO | Select Before Operate |
| BCU | Bay Control Unit |
| PLC (comms) | Power Line Carrier (30–500 kHz) |
| OPGW | Optical Ground Wire |
| PCM | Pulse Code Modulation |

---

## 📋 สูตรสรุปทั้งหมด (Cheat Sheet)

```
--- CH6 ---
IC = b + 2c·P
P_opt = (λ − b) / (2c)
ΣP = P_D
Avg Cost = F(P_test) / P_test

--- CH7 ---
ACE_i = ΔP_tie,i + B_i·Δf
ACE > 0 → ลด Gen | ACE < 0 → เพิ่ม Gen

--- CH8 Touch/Step (50 kg, K=0.116) ---
E_touch = (1000 + 1.5·Cs·ρs) × 0.116/√t_s
E_step  = (1000 + 6·Cs·ρs)   × 0.116/√t_s
[70 kg → K=0.157]

--- CH8 Ground Grid (Sverak) ---
R_G = ρ × [1/L_T + 1/√(20A) × (1 + 1/(1+h√(20/A)))]
ระวัง h ต้องเป็นหน่วย m

--- CH10 Relay ---
PSM = (I_fault/CTR) / I_p
SI:  T = TMS × 0.14   / (PSM^0.02 − 1)
VI:  T = TMS × 13.5   / (PSM − 1)
EI:  T = TMS × 80     / (PSM² − 1)
LTI: T = TMS × 120    / (PSM − 1)
```

---

*PowerPlant Final — SUT EE | เตรียมสอบ 2026*
