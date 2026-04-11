# 🛠️ مخطط كامل لإنشاء تطبيق "عيادة الأثير للبصريات" - جاهز للـ AI

**انسخ هذا المخطط بالكامل وأعطه لأي AI لإنشاء نفس التطبيق 100%**

## 🎯 المواصفات العامة
```
الاسم: عيادة الأثير للبصريات (The Ethereal Clinic)
اللغة: عربي RTL فقط
التصميم: Glassmorphism حديث + Tailwind CSS
الموبايل: Responsive 100% (mobile-first)
التخزين: LocalStorage فقط
الخطوط: Tajawal + Manrope
الأيقونات: Material Symbols
الألوان: 
  - Primary: #00BCD4 (Cyan)
  - Secondary: Purple (#8B5CF6)
  - Red: Expenses (#EF4444)
  - Green: Profit
```

## 📁 هيكل الملفات (8 ملفات HTML فقط)
```
home.html          - الرئيسية (داشبورد)
add-patient.html   - إضافة مريض + وصفة
archive.html       - أرشيف المرضى
expenses.html      - المصروفات
inventory.html     - الجرد
add-material.html  - إضافة مواد
reports.html       - التقارير والإحصائيات
settings.html      - الإعدادات + Backup
```

## 🧬 CSS مشترك لكل ملف (انسخه في `<style>`)

```html
<style>
/* أساسيات */
body { 
  font-family: &#39;Tajawal&#39;, sans-serif; 
  direction: rtl; 
  min-height: 100dvh;
}
.mesh-gradient { 
  background: linear-gradient(135deg, #0c1324 0%, #1e1b4b 50%, #312e81 100%);
}
.dark .mesh-gradient { /* dark mode */ }

/* Glass Cards */
.glass-card { 
  backdrop-filter: blur(20px); 
  border: 1px solid rgba(255,255,255,0.1); 
}

/* Header */
header { 
  backdrop-blur-xl; 
  position: fixed; 
  top: 0; 
  z-50; 
  h-20; 
}

/* Bottom Nav */
nav.bottom { 
  fixed bottom-0; 
  h-20; 
  rounded-t-[2rem]; 
  flex justify-around;
}

/* Sidebar */
.sidebar { 
  fixed inset-y-0 right-0; 
  w-80; 
  translate-x-full; 
  transition-transform; 
  rounded-l-3xl;
}
</style>
```

## 📋 تفاصيل كل صفحة (Copy-Paste ready)

### 1️⃣ **home.html** - داشبورد
```
Header + Stats Cards (4 كروت):
- زبائن اليوم | فحوصات | إيرادات | مصروفات
Recent Transactions List (آخر 5 مرضى)
Bottom Nav: home(active) | add | archive | settings
```

### 2️⃣ **add-patient.html** - إضافة مريض
```
شخصي: اسم | عمر | عنوان | هاتف
عين يمنى: SPH/CYL/AXIS/ADD/VA (steppers ±0.25)
عين يسرى: نفس الخطوات (بنفسجي)
PD: stepper 55-75mm
زر: حفظ | طباعة A5
```

### 3️⃣ **archive.html** - الأرشيف
```
Search Bar + Date Filter (اليوم/أسبوع/شهر)
قائمة مرضى: avatar + name + phone + date
Modal: تفاصيل كاملة + طباعة + حذف
```

### 4️⃣ **expenses.html** - مصروفات
```
فلتر: اليوم/أسبوع/شهر
نموذج: نوع(إيجار/راتب/...) | مبلغ | تاريخ | ملاحظات
قائمة مصروفات + إجمالي
```

### 5️⃣ **inventory.html** - الجرد
```
قائمة: اسم | فئة | كمية | سعر | (تنبيه أحمر إذا < الحد الأدنى)
Search + إضافة جديدة
```

### 6️⃣ **add-material.html** - إضافة مواد
```
نموذج: اسم | فئة(عدسات/إطارات) | وحدة | كمية | حد أدنى | سعر
```

### 7️⃣ **reports.html** - تقارير
```
إحصائيات: مرضى | إيرادات | مصروفات | ربح
رسم بياني إيرادات (7 أيام)
إحصائيات عيون: قصر/طول/لابؤرية (bars)
تصدير JSON
```

### 8️⃣ **settings.html** - إعدادات
```
عيادة: اسم | عنوان | هاتف | سوشيال
قوالب فاتورة: Modern/Classic
Dark Mode Toggle
Backup: Export JSON | Import | Clear All
```

## ⚙️ LocalStorage Schema
```javascript
patients: [{id, fullName, age, address, phone, rightEye{sph,cyl,axis,add,va}, leftEye{}, pd, createdAt}]
expenses: [{id, type, amount, date, notes}]
materials: [{id, name, category, unit, quantity, minQuantity, price}]
clinicSettings: {clinicName, address, phone, social}
```

## 🎨 الـ JavaScript المطلوب
```javascript
// 1. Theme Toggle (localStorage.theme)
document.getElementById(&#39;theme-toggle&#39;).onclick = () => {
  document.documentElement.classList.toggle(&#39;dark&#39;);
}

// 2. Sidebar Toggle
menuBtn.onclick = () => sidebar.classList.toggle(&#39;translate-x-full&#39;);

// 3. Search/Filter Functions
function filterPatients() { /* فلترة حسب تاريخ/اسم */ }

// 4. Save to LocalStorage
function savePatient(data) {
  let patients = JSON.parse(localStorage.getItem(&#39;patients&#39;) || &#39;[]&#39;);
  patients.push(data);
  localStorage.setItem(&#39;patients&#39;, JSON.stringify(patients));
}

// 5. Toast Notification
function showToast(msg) {
  // أنشئ div ثابت أسفل الشاشة 2 ثانية
}

// 6. Print Prescription (A5)
window.print(); // مع template جاهز
```

## 📱 Bottom Nav (في كل صفحة)
```html
<nav class="fixed bottom-0 w-full flex justify-around h-20">
  <a href="home.html"><span>home</span></a>
  <a href="add-patient.html"><span>person_add</span></a>
  <a href="archive.html"><span>inventory</span></a>
  <a href="settings.html"><span>settings</span></a>
</nav>
```

## 🚀 خطوات التنفيذ للـ AI
```
1. أنشئ ملف HTML واحد بـ CSS/JS كامل
2. انسخ CSS المشترك في <style>
3. طبق المحتوى حسب الصفحة
4. أضف LocalStorage functions
5. اختبر على Mobile Chrome
6. تأكد RTL + Dark Mode يعملان
```

**هذا المخطط = 100% نفس التطبيق الأصلي!** 🔥

انسخه وأعطه لأي AI Developer → **سيُنشئ نفس الـ App بالضبط**

