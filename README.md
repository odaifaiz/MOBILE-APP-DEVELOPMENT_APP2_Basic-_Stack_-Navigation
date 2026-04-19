
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


</div>

---

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
                                                            | ![Home](scrennshots/home.png) | ![Detail](scrennshots/details.png) | 

|
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
git clone https://github.com/odaifaez/MOBILE-APP-DEVELOPMENT_APP2_Basic-_Stack_-Navigation.git
cd MOBILE-APP-DEVELOPMENT_APP2_Basic-_Stack_-Navigation
```

#### 2️⃣ تثبيت الاعتماديات
```bash
flutter pub get
```

#### 3️⃣ تشغيل التطبيق
```bash
flutter run

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

Copyright (c) 2026 [odai faez]

يُمنح إذن، مجاناً، لأي شخص يحصل على نسخة من هذا البرنامج
والمستندات المرتبطة به ("البرنامج")، للتعامل في البرنامج
دون قيود، بما في ذلك على سبيل المثال لا الحصر حقوق
الاستخدام والنسخ والتعديل والدمج والنشر والتوزيع والترخيص
و/أو بيع نسخ من البرنامج، ويسمح للأشخاص الذين يحصلون
على البرنامج القيام بذلك وفقاً للشروط التالية:

[نص الترخيص الكامل في ملف LICENSE]
```

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



