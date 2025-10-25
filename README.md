# Frontend Odoo Developer Interview Questions (Junior Level)

> 📘 هذا الملف مخصص لتحضير مقابلات **Frontend Odoo Developer** — يحتوي على أهم الأسئلة والأجوبة المختصرة + أكواد عملية.

---

## 🟢 القسم الأول: HTML / CSS / JavaScript

### HTML

* **ما الفرق بين `<div>` و `<span>`؟**
  `div` عنصر block، بينما `span` عنصر inline.

* **ما هو الـ Semantic HTML؟**
  استخدام عناصر HTML بمعناها الصحيح مثل `<header>`, `<nav>`, `<footer>` لتحسين SEO والوصولية.

* **ما الفرق بين id و class؟**
  `id` فريد، بينما `class` يمكن استخدامه لأكثر من عنصر.

---

### CSS

* **الفرق بين position: relative / absolute / fixed / sticky:**

  * `relative`: بالنسبة لمكان العنصر الأصلي.
  * `absolute`: بالنسبة لأقرب عنصر أب عنده position.
  * `fixed`: ثابت في الشاشة حتى مع الـ scroll.
  * `sticky`: يتحول إلى ثابت بعد scroll معين.

* **الفرق بين em / rem / px:**

  * `px`: وحدة ثابتة.
  * `em`: نسبة إلى حجم خط العنصر الأب.
  * `rem`: نسبة إلى حجم خط العنصر الجذر.

* **الفرق بين flex و grid؟**

  * `flex`: لتصميم الاتجاه الواحد.
  * `grid`: لتصميم اتجاهين (صفوف وأعمدة).

---

### JavaScript

* **الفرق بين var / let / const:**
  `var` قديمة (function scope)، `let` و `const` (block scope).
  `const` لا يمكن إعادة تعيينها.

* **الفرق بين == و ===:**
  `==` يقارن بعد التحويل، `===` يقارن النوع والقيمة.

* **ما هو Event Bubbling؟**
  انتقال الحدث من العنصر الداخلي إلى الخارجي.

* **الفرق بين function و arrow function؟**
  Arrow functions لا تملك `this` خاص بها.

---

## 🟣 القسم الثاني: OWL.js Framework

* **ما هو OWL؟**
  إطار Frontend حديث من Odoo مبني على مبدأ الـ Components.

* **ما الفرق بين Component و Template؟**
  Template = HTML، Component = المنطق (logic + state).

* **مثال على Component بسيط:**

  ```js
  /** @odoo-module **/
  import { Component } from "@odoo/owl";

  export class HelloWorld extends Component {
      static template = "my_module.HelloWorldTemplate";
  }
  ```

  ```xml
  <templates>
      <t t-name="my_module.HelloWorldTemplate">
          <div>Hello <t t-esc="props.name"/></div>
      </t>
  </templates>
  ```

* **ما هو useState؟**
  يستخدم لإدارة الحالة الداخلية للـ component.

* **ما هو onMounted()؟**
  Hook يتم تنفيذه بعد عرض العنصر على DOM.

---

## 🟠 القسم الثالث: QWeb Templates

* **ما هو QWeb؟**
  محرك قوالب Odoo يُستخدم في الويب والتقارير.

* **ما الفرق بين t-esc و t-raw؟**
  `t-esc` يعرض نص آمن (يمنع HTML injection)، `t-raw` يعرض HTML كما هو.

* **مثال على تكرار:**

  ```xml
  <t t-foreach="records" t-as="rec">
      <div><t t-esc="rec.name"/></div>
  </t>
  ```

* **ما هو t-att-class؟**
  لإضافة class ديناميكي.

---

## 🔵 القسم الرابع: Web Assets & JS Widgets

* **إضافة JS/CSS:**

  ```xml
  <template id="assets_frontend" inherit_id="web.assets_frontend">
      <xpath expr="." position="inside">
          <script src="/my_module/static/src/js/main.js"></script>
          <link rel="stylesheet" href="/my_module/static/src/css/style.css"/>
      </xpath>
  </template>
  ```

* **الفرق بين web.assets_backend و web.assets_frontend؟**

  * backend: للـ UI الداخلي.
  * frontend: لموقع الويب.

* **ما هو AbstractAction؟**
  كلاس أساسي لأي شاشة مخصصة في الـ backend.

* **الفرق بين rpc.query و ajax.jsonRpc؟**

  * rpc.query: للتواصل الداخلي.
  * jsonRpc: للتعامل مع Controllers عبر HTTP.

---

## 🟣 القسم الخامس: Website / Portal Customization

* **إنشاء Controller:**

  ```python
  from odoo import http

  class MyWebsite(http.Controller):
      @http.route('/my_page', auth='public', website=True)
      def my_page(self, **kw):
          return http.request.render('my_module.my_template')
  ```

* **تمرير بيانات للـ Template:**

  ```python
  return http.request.render('my_module.my_template', {'name': 'Sameh'})
  ```

  ```xml
  <t t-esc="name"/>
  ```

* **ما فائدة t-call="website.layout"؟**
  لإعادة استخدام هيكل الصفحة الرئيسي (Header/Footer).

---

## 🔴 القسم السادس: أسئلة عملية

1. اعمل modal بسيط يظهر عند الضغط على زر.
2. أضف animation باستخدام @keyframes.
3. اعمل custom snippet يعرض صور متحركة.
4. اعمل component OWL يجلب بيانات من controller.

---

## 🟢 القسم السابع: HR / تجربة العمل

* احكي عن مشروع Odoo Frontend اشتغلت عليه.
* إزاي بتتعامل مع backend team؟
* إزاي بتبدأ تعديل تصميم في Odoo website؟
* ما هي أصعب مشكلة واجهتك في OWL أو QWeb؟
* كيف تختبر التصميم قبل تسليمه؟

---

> ✅ **نصيحة:** راجع جيدًا ملفات `web.assets_frontend` و `web.assets_backend`، وتمرّن على إنشاء Component OWL مع Controller بسيط — دي أكتر نقطة بيسألو فيها في المقابلات.
