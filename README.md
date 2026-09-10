# 📦 Warehouse Management System (WMS) - Real-time Multi-device Sync

ระบบบริหารจัดการคลังสินค้าแบบเรียลไทม์ที่สามารถซิงค์ข้อมูลระหว่างเครื่องต่าง ๆ ได้

---

## ✨ **Features**

✅ **Real-time Sync** - ข้อมูลอัพเดตทันที (Firestore)
✅ **Multi-device Support** - ใช้งานร่วมกันได้บนหลายเครื่อง
✅ **Role-based Access** - Admin, Manager, Warehouse Staff
✅ **Goods Receipt (GR)** - รับสินค้าเข้า
✅ **Goods Issue (GI)** - เบิกจ่ายสินค้า
✅ **Inventory Management** - จัดการคลังสินค้า
✅ **Master Data** - ข้อมูลหลักสินค้า
✅ **Transaction History** - บันทึกประวัติ
✅ **Thai Language Support** - รองรับภาษาไทย
✅ **Export CSV** - ส่งออกรายงาน

---

## 🚀 **Quick Start**

### 1. **Clone Repository**
```bash
git clone https://github.com/pong2555k-spec/WMS-Warehouse-Management-System.git
cd WMS-Warehouse-Management-System
```

### 2. **ตั้งค่า Firebase**
- ไปที่ https://console.firebase.google.com/
- สร้าง Project ชื่อ "WMS-Warehouse-System"
- สร้าง Firestore Database (Region: asia-southeast1)
- เปิด Anonymous Authentication
- Copy Firebase Config

### 3. **แก้ไข index.html**
- เปิด `index.html`
- ค้นหา `FIREBASE_CONFIG` (บรรทัด ~330)
- วาง Firebase Config ที่ได้

### 4. **เปิดเบราว์เซอร์**
- เปิด `index.html` ในเบราว์เซอร์
- ลอกอิน (admin / admin123)
- ทดสอบบนเครื่องอื่น

---

## 📋 **Firebase Setup (Detailed)**

ดู `FIREBASE-SETUP-TH.md` สำหรับคำแนะนำภาษาไทยอย่างละเอียด

---

## 🔐 **Login Credentials (Demo)**

| Username | Password | Role |
|----------|----------|------|
| admin | admin123 | Admin (ผู้ดูแลระบบ) |
| anyawee.t | 1234 | Assistant Manager |
| staff01 | 1234 | Warehouse Staff |

---

## 📁 **Files Structure**

```
WMS-Warehouse-Management-System/
├── index.html                      # Main application (ไฟล์หลัก)
├── firestore-rules.txt             # Firebase Firestore Rules
├── FIREBASE-SETUP-TH.md            # Firebase Setup Guide (Thai)
├── README.md                       # Documentation
├── .github/
│   └── workflows/                  # CI/CD (Optional)
└── docs/
    ├── TROUBLESHOOTING-TH.md       # Troubleshooting (Thai)
    └── SECURITY.md                 # Security Guide
```

---

## 🎯 **Main Features**

### 📥 **Inbound (GR - Goods Receipt)**
- รับสินค้าเข้าคลัง
- สแกนรหัส → เลือกตำแหน่ง → บันทึก
- จำนวนอัพเดต real-time

### 📤 **Outbound (GI - Goods Issue)**
- เบิกจ่ายสินค้า
- ตรวจสอบ Stock อัตโนมัติ
- ป้องกันเบิกเกิน

### 📊 **Dashboard**
- KPI Summary
- Current Stock Status
- Live Activity Stream
- Sync Status Indicator

### 🗂️ **Inventory Management**
- ดูจำนวนสินค้า
- ตรวจสอบตำแหน่ง
- Alert Low Stock
- Search & Filter

### 📋 **Master Data**
- จัดการรหัสสินค้า
- ประเภท/Description
- ผู้จำหน่าย

### ⚙️ **Settings**
- เปลี่ยนชื่อระบบ
- เพิ่ม/ลบ ตำแหน่ง
- ตั้ง Min Threshold

### 👥 **User Management (Admin)**
- เพิ่มผู้ใช้
- ลบผู้ใช้
- User List

---

## 🔄 **Real-time Sync Flow**

```
Machine A (Add GR) → Firestore Cloud → Machine B, C, D (Auto Update)
```

---

## 🧪 **Testing**

### Local Test (1 machine, 2 tabs)
```
1. Tab 1: Open index.html
2. Tab 2: Open index.html
3. Tab 1: Add stock
4. Tab 2: Updates instantly ✅
```

### Network Test (Multiple machines)
```
1. Machine A: Open index.html
2. Machine B: Open index.html (different computer)
3. Same Firebase Config
4. Machine A: Add item
5. Machine B: Updates instantly ✅
```

---

## 🛡️ **Security**

✅ Authentication (Username/Password)
✅ Role-based Access Control
✅ Firestore Rules
✅ Input Validation
✅ Session Management

---

## ⚡ **Performance**

- Real-time sync (no manual refresh)
- Offline support (localStorage)
- Optimized queries
- Debounced renders

---

## 🐛 **Troubleshooting**

ดู `TROUBLESHOOTING-TH.md` สำหรับแนวทางแก้ปัญหา

---

## 📞 **Support**

1. ตรวจสอบ `FIREBASE-SETUP-TH.md`
2. ดู `TROUBLESHOOTING-TH.md`
3. Check browser console (F12)
4. Reset demo data (Settings)

---

**Made with ❤️ for Warehouse Management**

🚀 Happy Warehouse Managing!