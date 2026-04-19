
readme_content = """<div align="center">

# 🧭 التنقل بين الشاشات في فلاتر - Flutter Stack Navigation

[![Flutter Version](https://img.shields.io/badge/Flutter-3.0+-02569B.svg?style=for-the-badge&logo=flutter)](https://flutter.dev)
[![Dart Version](https://img.shields.io/badge/Dart-3.0+-0175C2.svg?style=for-the-badge&logo=dart)](https://dart.dev)
[![License](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Android%20%7C%20iOS%20%7C%20Web%20%7C%20Desktop-FF6F00.svg?style=for-the-badge)](https://flutter.dev)

<p align="center">
  <img src="https://img.shields.io/badge/اللغة-العربية-FF0000?style=for-the-badge" alt="Arabic" />
  <img src="https://img.shields.io/badge/RTL-مفعل-00C853?style=for-the-badge" alt="RTL" />
</p>

**مشروع تعليمي شامل يوضح مفهوم مكدس التنقل (Navigation Stack) في Flutter مع دعم كامل للغة العربية**

[📖 شرح المفهوم](#-مفهوم-مكدس-التنقل) • [🚀 التثبيت](#-التثبيت) • [💻 الكود](#-هيكل-المشروع) • [📚 الأمثلة](#-أمثلة-الاستخدام)

</div>

---

## 📋 جدول المحتويات

- [🎯 نظرة عامة](#-نظرة-عامة)
- [✨ المميزات](#-المميزات)
- [🧠 مفهوم مكدس التنقل](#-مفهوم-مكدس-التنقل)
- [📸 لقطات الشاشة](#-لقطات-الشاشة)
- [🚀 التثبيت](#-التثبيت)
- [📁 هيكل المشروع](#-هيكل-المشروع)
- [💻 الكود المصدري](#-الكود-المصدرى)
- [📚 أمثلة الاستخدام](#-أمثلة-الاستخدام)
- [⚠️ الأخطاء الشائعة](#️-الأخطاء-الشائعة)
- [🔄 مقارنة العمليات](#-مقارنة-العمليات)
- [🎯 التحسينات المقترحة](#-التحسينات-المقترحة)
- [🤝 المساهمة](#-المساهمة)
- [📝 الترخيص](#-الترخيص)

---

## 🎯 نظرة عامة

هذا المشروع عبارة عن **تطبيق تعليمي** يهدف إلى شرح مفهوم **التنقل بين الشاشات (Navigation)** في إطار عمل Flutter، مع التركيز على:

- ✅ فهم **مكدس التنقل (Navigation Stack)**
- ✅ استخدام `Navigator.push()` للانتقال للأمام
- ✅ استخدام `Navigator.pop()` للعودة للخلف
- ✅ فهم مبدأ **LIFO (Last In, First Out)**
- ✅ التعامل مع مشكلة **Overflow** في الشاشات الصغيرة
- ✅ دعم كامل للغة العربية واتجاه RTL

---

## ✨ المميزات

### 🎓 الجانب التعليمي
- 📖 **توضيح المكدس** - عرض حالة المكدس في كل شاشة
- 🎨 **ألوان تمييزية** - كل شاشة بلون مختلف (Indigo للرئيسية، Teal للتفاصيل)
- 📱 **تصميم تفاعلي** - أزرار واضحة مع أيقونات توضيحية

### 🛠️ الجانب التقني
- 🌐 **دعم اللغة العربية** - كامل مع الاتجاه RTL
- 📐 **تصميم متجاوب** - يعمل على جميع أحجام الشاشات
- ♿ **إمكانية الوصول** - دعم قارئات الشاشة
- 🎭 **رسوم متحركة** - انتقالات سلسة بين الشاشات

### 🔧 أفضل الممارسات
- 📁 **فصل الملفات** - كل شاشة في ملف منفصل
- 🎯 **StatelessWidget** - استخدام الأدوات الخفيفة حيثما أمكن
- 📝 **تعليقات توضيحية** - شرح كل خطوة بالعربية
- 🧪 **معالجة الأخطاء** - حل مشكلة Overflow

---

## 🧠 مفهوم مكدس التنقل

### ما هو المكدس (Stack)؟

المكدس هو **هيكل بيانات** يتبع مبدأ **LIFO**:

> **L**ast **I**n, **F**irst **O**ut  
> **آخر ما يدخل، أول ما يخرج**

### تمثيل مرئي للمكدس

```
┌─────────────────────────────────────┐
│           🔝 القمة (Top)             │
│                                     │
│  ┌─────────────────────────────┐   │
│  │     DetailScreen (الظاهرة)   │   │  ← يمكن التفاعل معها
│  │         اللون: Teal          │   │
│  └─────────────────────────────┘   │
│  ┌─────────────────────────────┐   │
│  │      HomeScreen (خلفية)      │   │  ← مخفية في الخلفية
│  │        اللون: Indigo        │   │
│  └─────────────────────────────┘   │
│                                     │
│           🔻 القاعدة (Bottom)        │
└─────────────────────────────────────┘
```

### حركة المكدس خطوة بخطوة

| الخطوة | العملية | الكود | حالة المكدس | الوصف |
|:------:|:-------:|:-----:|:-----------:|:------|
| 1️⃣ | بدء التطبيق | - | `[HomeScreen]` | الشاشة الأولى تُضاف تلقائياً |
| 2️⃣ | الضغط على الزر | `push()` | `[HomeScreen, DetailScreen]` | إضافة شاشة فوق المكدس |
| 3️⃣ | الضغط على رجوع | `pop()` | `[HomeScreen]` | إزالة الشاشة العلوية |

### رسم توضيحي للحركة

```
الخطوة 1: بدء التطبيق
┌─────────────────┐
│                 │
│   HomeScreen    │  ← ✅ مرئية وتفاعلية
│   🏠 اللون: Indigo│
│                 │
└─────────────────┘
المكدس: [HomeScreen]


الخطوة 2: Navigator.push()
┌─────────────────┐
│  DetailScreen   │  ← ✅ مرئية وتفاعلية (الجديدة)
│  📄 اللون: Teal  │
├─────────────────┤
│   HomeScreen    │  ← ⬜ مخفية في الخلفية
│   🏠 اللون: Indigo│
└─────────────────┘
المكدس: [HomeScreen, DetailScreen]


الخطوة 3: Navigator.pop()
┌─────────────────┐
│                 │
│   HomeScreen    │  ← ✅ عادت للواجهة
│   🏠 اللون: Indigo│
│                 │
└─────────────────┘
المكدس: [HomeScreen]
```

---

## 📸 لقطات الشاشة

<div align="center">

| الشاشة الرئيسية | شاشة التفاصيل  |
|:---:|:---:|:---:|
| ![Home](screenshots/home.png) | ![Detail](screenshots/details.png) | 
| **HomeScreen** | **DetailScreen** |
| اللون: Indigo | اللون: Teal | أيقونة: Layers |

</div>

---

## 🚀 التثبيت

### المتطلبات المسبقة

- [Flutter SDK](https://flutter.dev/docs/get-started/install) ≥ 3.0.0
- [Dart SDK](https://dart.dev/get-dart) ≥ 3.0.0
- محرر أكواد (VS Code / Android Studio / IntelliJ)

### خطوات التثبيت

#### 1️⃣ استنساخ المستودع
```bash
git clone https://github.com/username/flutter-stack-navigation.git
cd flutter-stack-navigation
```

#### 2️⃣ تثبيت الاعتماديات
```bash
flutter pub get
```

#### 3️⃣ تشغيل التطبيق
```bash
flutter run
```

### بناء الإصدار للإنتاج

```bash
# 📱 Android - APK
flutter build apk --release

# 📱 Android - AppBundle
flutter build appbundle --release

# 🍎 iOS
flutter build ios --release

# 🌐 Web
flutter build web --release

# 💻 Windows
flutter build windows --release

# 🐧 Linux
flutter build linux --release

# 🍏 macOS
flutter build macos --release
```

---

## 📁 هيكل المشروع

```
flutter_stack_navigation/
│
├── 📁 android/                    # إعدادات Android
├── 📁 ios/                        # إعدادات iOS
├── 📁 lib/                        # 📂 الكود المصدري الرئيسي
│   │
│   ├── 📄 main.dart                # 🎯 نقطة الدخول
│   │   └── MyApp                 # إعدادات التطبيق العامة
│   │       ├── ThemeData         # السمة (Indigo)
│   │       ├── Localizations     # دعم العربية
│   │       └── Directionality    # الاتجاه RTL
│   │
│   └── 📁 screens/               # 📂 شاشات التطبيق
│       │
│       ├── 📄 home_screen.dart    # 🏠 الشاشة الرئيسية
│       │   └── HomeScreen        # StatelessWidget
│       │       ├── AppBar        # شريط العنوان (Indigo)
│       │       ├── Stack Info    # بطاقة معلومات المكدس
│       │       └── ElevatedButton # زر الانتقال (push)
│       │
│       └── 📄 detail_screen.dart  # 📄 شاشة التفاصيل
│           └── DetailScreen      # StatelessWidget
│               ├── AppBar        # شريط العنوان (Teal)
│               ├── Stack Info    # بطاقة معلومات المكدس
│               ├── SingleChildScrollView # حل Overflow
│               ├── ElevatedButton # زر الرجوع (pop)
│               └── TextButton    # زر pushReplacement
│
├── 📁 test/                       # 🧪 اختبارات الوحدة
├── 📁 screenshots/                # 📸 لقطات الشاشة
├── 📄 pubspec.yaml               # ⚙️ إعدادات المشروع
├── 📄 README.md                  # 📖 هذا الملف
└── 📄 LICENSE                      # 📜 ترخيص MIT
```

---

## 💻 الكود المصدري

### 🎯 ملف `main.dart` - نقطة الدخول

```dart
import 'package:flutter/material.dart';
import 'package:flutter_localizations/flutter_localizations.dart';
import 'screens/home_screen.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'التنقل بين الشاشات',
      debugShowCheckedModeBanner: false,
      
      // 🌍 دعم اللغة العربية
      localizationsDelegates: const [
        GlobalMaterialLocalizations.delegate,
        GlobalWidgetsLocalizations.delegate,
        GlobalCupertinoLocalizations.delegate,
      ],
      supportedLocales: const [
        Locale('ar', 'SA'),
      ],
      locale: const Locale('ar', 'SA'),
      
      theme: ThemeData(
        primarySwatch: Colors.indigo,
        useMaterial3: true,
        fontFamily: 'Cairo',
      ),
      
      // 🔄 تفعيل الاتجاه RTL
      builder: (context, child) {
        return Directionality(
          textDirection: TextDirection.rtl,
          child: child!,
        );
      },
      
      // 🏠 الشاشة الأولى في المكدس
      home: const HomeScreen(),
    );
  }
}
```

### 🏠 ملف `screens/home_screen.dart` - الشاشة الرئيسية

```dart
import 'package:flutter/material.dart';
import 'detail_screen.dart';

class HomeScreen extends StatelessWidget {
  const HomeScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('الشاشة الرئيسية'),
        centerTitle: true,
        backgroundColor: Colors.indigo,
        foregroundColor: Colors.white,
      ),
      body: Container(
        decoration: BoxDecoration(
          gradient: LinearGradient(
            begin: Alignment.topCenter,
            end: Alignment.bottomCenter,
            colors: [Colors.indigo.shade50, Colors.white],
          ),
        ),
        child: Center(
          child: Padding(
            padding: const EdgeInsets.all(24.0),
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                // 🏠 أيقونة الشاشة الرئيسية
                Container(
                  padding: const EdgeInsets.all(24),
                  decoration: BoxDecoration(
                    color: Colors.indigo.shade100,
                    shape: BoxShape.circle,
                  ),
                  child: Icon(Icons.home, size: 80, color: Colors.indigo.shade700),
                ),
                const SizedBox(height: 32),
                
                // 📝 عنوان الترحيب
                Text(
                  'مرحباً بك!',
                  style: TextStyle(
                    fontSize: 32,
                    fontWeight: FontWeight.bold,
                    color: Colors.indigo.shade900,
                  ),
                ),
                const SizedBox(height: 16),
                
                Text(
                  'أنت حالياً في الشاشة الرئيسية',
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 16,
                    color: Colors.grey.shade600,
                  ),
                ),
                const SizedBox(height: 48),

                // 📊 بطاقة معلومات المكدس
                Container(
                  padding: const EdgeInsets.all(16),
                  decoration: BoxDecoration(
                    color: Colors.amber.shade50,
                    borderRadius: BorderRadius.circular(12),
                    border: Border.all(color: Colors.amber.shade200),
                  ),
                  child: Column(
                    children: [
                      Row(
                        children: [
                          Icon(Icons.info, color: Colors.amber.shade800),
                          const SizedBox(width: 8),
                          Text(
                            'حالة المكدس الحالية:',
                            style: TextStyle(
                              fontWeight: FontWeight.bold,
                              color: Colors.amber.shade900,
                            ),
                          ),
                        ],
                      ),
                      const SizedBox(height: 8),
                      Container(
                        padding: const EdgeInsets.all(12),
                        decoration: BoxDecoration(
                          color: Colors.white,
                          borderRadius: BorderRadius.circular(8),
                        ),
                        child: const Text(
                          '[HomeScreen]',
                          style: TextStyle(
                            fontFamily: 'monospace',
                            fontSize: 16,
                            fontWeight: FontWeight.bold,
                          ),
                        ),
                      ),
                    ],
                  ),
                ),
                const SizedBox(height: 48),

                // ➡️ زر الانتقال للشاشة التالية
                SizedBox(
                  width: double.infinity,
                  height: 56,
                  child: ElevatedButton.icon(
                    onPressed: () {
                      // 🚀 Navigator.push: إضافة شاشة جديدة فوق المكدس
                      Navigator.push(
                        context,
                        MaterialPageRoute(
                          builder: (context) => const DetailScreen(),
                        ),
                      );
                    },
                    icon: const Icon(Icons.arrow_forward),
                    label: const Text(
                      'الانتقال إلى شاشة التفاصيل',
                      style: TextStyle(fontSize: 18),
                    ),
                    style: ElevatedButton.styleFrom(
                      backgroundColor: Colors.indigo,
                      foregroundColor: Colors.white,
                      shape: RoundedRectangleBorder(
                        borderRadius: BorderRadius.circular(16),
                      ),
                      elevation: 4,
                    ),
                  ),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```

### 📄 ملف `screens/detail_screen.dart` - شاشة التفاصيل

```dart
import 'package:flutter/material.dart';
import 'home_screen.dart';

class DetailScreen extends StatelessWidget {
  const DetailScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('شاشة التفاصيل'),
        centerTitle: true,
        backgroundColor: Colors.teal,
        foregroundColor: Colors.white,
        leading: IconButton(
          icon: const Icon(Icons.arrow_back),
          onPressed: () {
            // 🔙 Navigator.pop: إزالة الشاشة الحالية من المكدس
            Navigator.pop(context);
          },
        ),
      ),
      body: Container(
        decoration: BoxDecoration(
          gradient: LinearGradient(
            begin: Alignment.topCenter,
            end: Alignment.bottomCenter,
            colors: [Colors.teal.shade50, Colors.white],
          ),
        ),
        // 📜 حل مشكلة Overflow: السماح بالتمرير
        child: SingleChildScrollView(
          child: Center(
            child: Padding(
              padding: const EdgeInsets.all(24.0),
              child: Column(
                children: [
                  // 📄 أيقونة الشاشة الثانية
                  Container(
                    padding: const EdgeInsets.all(24),
                    decoration: BoxDecoration(
                      color: Colors.teal.shade100,
                      shape: BoxShape.circle,
                    ),
                    child: Icon(Icons.description, size: 80, color: Colors.teal.shade700),
                  ),
                  const SizedBox(height: 32),
                  
                  // 📝 عنوان الشاشة
                  Text(
                    'شاشة التفاصيل',
                    style: TextStyle(
                      fontSize: 32,
                      fontWeight: FontWeight.bold,
                      color: Colors.teal.shade900,
                    ),
                  ),
                  const SizedBox(height: 16),
                  
                  Text(
                    'أنت حالياً في الشاشة الثانية',
                    textAlign: TextAlign.center,
                    style: TextStyle(
                      fontSize: 16,
                      color: Colors.grey.shade600,
                    ),
                  ),
                  const SizedBox(height: 48),

                  // 📊 بطاقة معلومات المكدس
                  Container(
                    padding: const EdgeInsets.all(16),
                    decoration: BoxDecoration(
                      color: Colors.orange.shade50,
                      borderRadius: BorderRadius.circular(12),
                      border: Border.all(color: Colors.orange.shade200),
                    ),
                    child: Column(
                      children: [
                        Row(
                          children: [
                            Icon(Icons.layers, color: Colors.orange.shade800),
                            const SizedBox(width: 8),
                            Text(
                              'حالة المكدس الحالية:',
                              style: TextStyle(
                                fontWeight: FontWeight.bold,
                                color: Colors.orange.shade900,
                              ),
                            ),
                          ],
                        ),
                        const SizedBox(height: 8),
                        Container(
                          padding: const EdgeInsets.all(12),
                          decoration: BoxDecoration(
                            color: Colors.white,
                            borderRadius: BorderRadius.circular(8),
                          ),
                          child: Column(
                            children: [
                              Text(
                                'HomeScreen',
                                style: TextStyle(
                                  fontFamily: 'monospace',
                                  fontSize: 14,
                                  color: Colors.grey.shade600,
                                ),
                              ),
                              const Icon(Icons.arrow_drop_up, size: 20),
                              const Text(
                                'DetailScreen',
                                style: TextStyle(
                                  fontFamily: 'monospace',
                                  fontSize: 16,
                                  fontWeight: FontWeight.bold,
                                  color: Colors.teal,
                                ),
                              ),
                            ],
                          ),
                        ),
                      ],
                    ),
                  ),
                  const SizedBox(height: 48),

                  // 🔙 زر الرجوع
                  SizedBox(
                    width: double.infinity,
                    height: 56,
                    child: ElevatedButton.icon(
                      onPressed: () {
                        Navigator.pop(context);
                      },
                      icon: const Icon(Icons.arrow_back),
                      label: const Text(
                        'العودة إلى الشاشة الرئيسية',
                        style: TextStyle(fontSize: 18),
                      ),
                      style: ElevatedButton.styleFrom(
                        backgroundColor: Colors.teal,
                        foregroundColor: Colors.white,
                        shape: RoundedRectangleBorder(
                          borderRadius: BorderRadius.circular(16),
                        ),
                        elevation: 4,
                      ),
                    ),
                  ),
                  const SizedBox(height: 16),

                  // 🔄 زر pushReplacement
                  TextButton.icon(
                    onPressed: () {
                      Navigator.pushReplacement(
                        context,
                        MaterialPageRoute(
                          builder: (context) => const HomeScreen(),
                        ),
                      );
                    },
                    icon: const Icon(Icons.swap_horiz),
                    label: const Text('استبدال الشاشة (pushReplacement)'),
                  ),
                  
                  // ⬇️ مساحة أمان في الأسفل
                  const SizedBox(height: 24),
                ],
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

---

## 📚 أمثلة الاستخدام

### 🎯 المثال 1: التنقل الأساسي

```dart
// الانتقال للأمام
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => const DetailScreen()),
);

// العودة للخلف
Navigator.pop(context);
```

### 🔄 المثال 2: استبدال الشاشة

```dart
// استبدال الشاشة الحالية (مفيد بعد تسجيل الدخول)
Navigator.pushReplacement(
  context,
  MaterialPageRoute(builder: (context) => const HomeScreen()),
);
```

### 📤 المثال 3: تمرير البيانات

```dart
// إرسال البيانات
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => DetailScreen(userName: 'أحمد'),
  ),
);

// استقبال البيانات
class DetailScreen extends StatelessWidget {
  final String userName;
  const DetailScreen({super.key, required this.userName});
  
  @override
  Widget build(BuildContext context) {
    return Text('مرحباً $userName');
  }
}
```

### 📥 المثال 4: استقبال النتيجة

```dart
// إرسال النتيجة عند العودة
Navigator.pop(context, 'تم الحفظ');

// استقبال النتيجة
final result = await Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => const DetailScreen()),
);
print(result); // 'تم الحفظ'
```

---

## ⚠️ الأخطاء الشائعة

### ❌ خطأ 1: نسيان تمرير `context`

```dart
// ❌ خطأ
Navigator.push(MaterialPageRoute(...));

// ✅ صحيح
Navigator.push(context, MaterialPageRoute(...));
```

### ❌ خطأ 2: استخدام `pop()` بدون `push()` سابق

```dart
// ❌ خطأ - المكدس فارغ
Navigator.pop(context); // سيغلق التطبيق!

// ✅ الحل: التحقق من إمكانية الرجوع
if (Navigator.canPop(context)) {
  Navigator.pop(context);
}
```

### ❌ خطأ 3: مشكلة Overflow

```dart
// ❌ خطأ - المحتوى أكبر من الشاشة
Column(
  children: [/* الكثير من العناصر */],
)

// ✅ الحل - إضافة Scroll
SingleChildScrollView(
  child: Column(
    children: [/* الكثير من العناصر */],
  ),
)
```

### ❌ خطأ 4: إنشاء Route داخل `build()`

```dart
// ❌ خطأ - إعادة إنشاء Route مع كل تحديث
Widget build(BuildContext context) {
  final route = MaterialPageRoute(...); // سيُعاد إنشاؤه!
  return ElevatedButton(
    onPressed: () => Navigator.push(context, route),
  );
}

// ✅ صحيح - إنشاء Route داخل onPressed
Widget build(BuildContext context) {
  return ElevatedButton(
    onPressed: () {
      final route = MaterialPageRoute(...); // إنشاء عند الحاجة
      Navigator.push(context, route);
    },
  );
}
```

---

## 🔄 مقارنة العمليات

| العملية | الكود | حالة المكدس بعد | الاستخدام |
|:-------:|:-----:|:---------------:|:---------:|
| **push** | `Navigator.push(context, route)` | `[A, B]` | ➡️ الانتقال للأمام |
| **pop** | `Navigator.pop(context)` | `[A]` | ⬅️ العودة للخلف |
| **pushReplacement** | `Navigator.pushReplacement(context, route)` | `[B]` | 🔄 استبدال الشاشة |
| **pushAndRemoveUntil** | `Navigator.pushAndRemoveUntil(context, route, (route) => false)` | `[B]` | 🚀 إعادة التعيين |
| **popUntil** | `Navigator.popUntil(context, ModalRoute.withName('/home'))` | `[Home]` | ⏪ الرجوع لشاشة محددة |

### 🎯 متى تستخدم كل عملية؟

```dart
// push - التنقل العادي
// مثال: القائمة → تفاصيل المنتج
Navigator.push(context, route);

// pushReplacement - استبدال الشاشة
// مثال: شاشة التحميل → الشاشة الرئيسية
Navigator.pushReplacement(context, route);

// pushAndRemoveUntil - إزالة كل الشاشات السابقة
// مثال: تسجيل الدخول → الصفحة الرئيسية (منع الرجوع)
Navigator.pushAndRemoveUntil(
  context,
  route,
  (route) => false, // إزالة الكل
);

// popUntil - الرجوع لشاشة محددة
// مثال: إنهاء الشراء والعودة للرئيسية
Navigator.popUntil(context, ModalRoute.withName('/home'));
```

---

## 🎯 التحسينات المقترحة

### 🎭 1. رسوم متحركة مخصصة

```dart
PageRouteBuilder(
  pageBuilder: (context, animation, secondaryAnimation) => DetailScreen(),
  transitionsBuilder: (context, animation, secondaryAnimation, child) {
    return SlideTransition(
      position: animation.drive(
        Tween(begin: const Offset(1.0, 0.0), end: Offset.zero)
          .chain(CurveTween(curve: Curves.easeInOut)),
      ),
      child: child,
    );
  },
)
```

### 🗺️ 2. استخدام Named Routes

```dart
// في main.dart
MaterialApp(
  routes: {
    '/': (context) => const HomeScreen(),
    '/details': (context) => const DetailScreen(),
  },
)

// للانتقال
Navigator.pushNamed(context, '/details');
```

### 📱 3. دعم زر الرجوع الفعلي (Android)

```dart
// في DetailScreen
WillPopScope(
  onWillPop: () async {
    // تنفيذ عملية قبل الرجوع
    print('العودة للشاشة السابقة');
    return true; // السماح بالرجوع
  },
  child: Scaffold(...),
)
```

---

## 🤝 المساهمة

نرحب بمساهماتكم! للمساهمة في المشروع:

1. **انشئ Fork** للمستودع
2. **أنشئ فرعاً جديداً**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **أجرِ تغييراتك**
   ```bash
   git commit -m 'Add: وصف التغيير'
   ```
4. **ادفع الفرع**
   ```bash
   git push origin feature/amazing-feature
   ```
5. **افتح Pull Request**

### 📌 قواعد المساهمة

- 📖 اتبع [دليل أسلوب Flutter](https://github.com/flutter/flutter/wiki/Style-guide-for-Flutter-repo)
- 📝 اكتب تعليقات واضحة بالعربية
- 🧪 أضف اختبارات للميزات الجديدة
- 🎯 تأكد من عدم وجود أخطاء (`flutter analyze`)
- 📱 اختبر على أحجام شاشات مختلفة

---

## 📞 التواصل

<div align="center">

[![Twitter](https://img.shields.io/badge/Twitter-@username-1DA1F2?style=for-the-badge&logo=twitter)](https://twitter.com/odaifaez)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-username-0077B5?style=for-the-badge&logo=linkedin)](https://linkedin.com/in/odaifaez)
[![Email](https://img.shields.io/badge/Email-email@example.com-D14836?style=for-the-badge&logo=gmail)](mailto:dymhsn712@gmail.com)

</div>

---

## 📝 الترخيص

هذا المشروع مرخص بموجب [MIT License](LICENSE).

```
MIT License

Copyright (c) 2024 [اسمك]

يُمنح إذن، مجاناً، لأي شخص يحصل على نسخة من هذا البرنامج
والمستندات المرتبطة به ("البرنامج")، للتعامل في البرنامج
دون قيود، بما في ذلك على سبيل المثال لا الحصر حقوق
الاستخدام والنسخ والتعديل والدمج والنشر والتوزيع والترخيص
و/أو بيع نسخ من البرنامج، ويسمح للأشخاص الذين يحصلون
على البرنامج القيام بذلك وفقاً للشروط التالية:

[نص الترخيص الكامل في ملف LICENSE]
```

---

## 🙏 الشكر والتقدير

- [Flutter Team](https://flutter.dev) - على الإطار الرائع
- [المتبرعين](https://github.com/username/flutter-stack-navigation/graphs/contributors) - على جهودهم القيمة
- [مجتمع Flutter العربي](https://flutter-arabic.com) - على الدعم المستمر

---

<div align="center">

### ⭐ لا تنسَ إعطاء النجمة إذا أعجبك المشروع! ⭐

**[⬆ العودة إلى الأعلى](#-التنقل-بين-الشاشات-في-فلاتر---flutter-stack-navigation)**

</div>

---

<p align="center">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Made%20with-Flutter-02569B?style=flat-square&logo=flutter" alt="Made with Flutter" />
  <img src="https://img.shields.io/badge/Made%20with-Love-FF6B6B?style=flat-square" alt="Made with Love" />
</p>


# حفظ الم
