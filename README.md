# Project Scheduling & Critical Path Analyzer

**By Prof. Abdulrahman Al-Ahmari, ECI Lab**

An interactive, bilingual (English / Arabic) web tool for learning and applying the **Critical Path Method (CPM)**. Enter activities, durations and predecessors; the tool calculates the full schedule, finds every critical path and explains the result.

**Live demo:** https://ecilab.github.io/cpm-analyzer/

![Header and KPI cards](assets/screenshots/overview.png)

![Gantt chart with critical-path trace](assets/screenshots/gantt.png)

![Activity-on-node network diagram](assets/screenshots/network.png)

[العربية ↓](#محلل-جدولة-المشاريع-والمسار-الحرج)

## Features

- **CPM calculation:** forward and backward passes in topological order, ES, EF, LS, LF, total float and free float.
- **All critical paths:** every zero-float path from start to finish is found and listed, not just one.
- **Input validation:** duplicate numbers, missing names, negative durations, unknown predecessors, self-dependencies and circular dependencies (reported as the exact cycle, e.g. 3 → 5 → 7 → 3).
- **Animated Gantt chart:** dependency arrows, float tails, a step-by-step critical-path trace, schedule playback at ×1/×2/×4, zoom and PNG export.
- **Network diagram:** activity-on-node layout with an animated run along the critical path.
- **Schedule analysis:** statements and risk indicators generated only from the calculated values.
- **Five example projects:** 10, 11, 20 and 40 activities, plus a validation demo containing a cycle.
- **Import / export:** CSV and JSON, a printable report, and a light/dark theme.
- **Arabic interface** with right-to-left layout.

## Quick start

Open `index.html` in any modern browser. Nothing needs to be installed and no internet connection is required, except to load the web fonts.

1. Click one of the example cards above the activity table, or type your own activities.
2. Separate multiple predecessors with commas (`4,5`). Leave the field empty or type `-` for a starting activity.
3. The schedule recalculates as you type.

See [`docs/user-guide.md`](docs/user-guide.md) for a full walkthrough and [`docs/cpm-method.md`](docs/cpm-method.md) for the method.

## For instructors

- [`docs/exercises.md`](docs/exercises.md) contains student exercises based on the built-in examples.
- [`docs/exercises-answers.md`](docs/exercises-answers.md) contains the answers, all produced by the tool's own engine. Remove this file from a public copy if you want to use the exercises for assessment.
- [`examples/`](examples) holds every example as JSON, plus `template.csv` for students to fill in and import.

## Repository contents

| Path | Contents |
|---|---|
| `index.html` | The complete application (HTML, CSS and JavaScript in one file) |
| `examples/` | Example projects (JSON) and a CSV template |
| `docs/` | User guide, CPM method, exercises and answers |
| `LICENSE` | MIT License (code) |
| `NOTICE.md` | Logo exclusion, documentation license, fonts and privacy |
| `CITATION.cff` | Citation information |

## Privacy

Everything runs in the browser. No project data is sent anywhere; projects are saved only in the visitor's own browser storage.

## License

- **Code:** [MIT License](LICENSE).
- **Documentation and examples:** [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
- **Name and logo:** the ECI Lab name and logo are **not** covered by these licenses. See [NOTICE.md](NOTICE.md).

## How to cite

> Al-Ahmari, A. (2026). *Project Scheduling & Critical Path Analyzer* (Version 1.0.0) [Computer software]. ECI Lab. https://github.com/ecilab/cpm-analyzer

GitHub also shows a **Cite this repository** button generated from [`CITATION.cff`](CITATION.cff).

---

<div dir="rtl">

# محلل جدولة المشاريع والمسار الحرج

**إعداد: أ.د. عبدالرحمن الأحمري، مختبر ECI**

أداة ويب تفاعلية ثنائية اللغة (العربية والإنجليزية) لتعلّم **طريقة المسار الحرج (CPM)** وتطبيقها. أدخل الأنشطة ومددها والأنشطة السابقة لها، فتحسب الأداة الجدول الزمني كاملًا، وتحدّد جميع المسارات الحرجة، وتشرح النتائج.

**العرض المباشر:** https://ecilab.github.io/cpm-analyzer/

## المزايا

- **حساب CPM:** الحساب الأمامي والخلفي وفق الترتيب الطوبولوجي، وقيم ES و EF و LS و LF، والفائض الكلي والفائض الحر.
- **جميع المسارات الحرجة:** تُحصر كل المسارات ذات الفائض الصفري من البداية إلى النهاية، لا مسار واحد فقط.
- **التحقق من المدخلات:** الأرقام المكررة، والأسماء المفقودة، والمدد السالبة، والأنشطة السابقة غير الموجودة، والاعتماد على النفس، والاعتماد الدائري مع عرض الحلقة نفسها.
- **مخطط جانت متحرك:** أسهم الاعتماد، وذيول الفائض، وتتبّع المسار الحرج خطوة بخطوة، وتشغيل الجدول بسرعات ×1 و×2 و×4، والتكبير، والتصدير بصيغة PNG.
- **مخطط الشبكة:** عرض الأنشطة على العُقد مع حركة على المسار الحرج.
- **تحليل الجدول:** عبارات ومؤشرات مخاطر مستخرجة من القيم المحسوبة فقط.
- **خمسة أمثلة جاهزة:** بأحجام 10 و11 و20 و40 نشاطًا، إضافة إلى مثال للتحقق يحتوي على حلقة دائرية.
- **الاستيراد والتصدير:** بصيغتي CSV و JSON، وتقرير قابل للطباعة، ووضعان فاتح وداكن.

## البدء السريع

افتح الملف `index.html` في أي متصفح حديث، ولا حاجة إلى أي تثبيت.

1. انقر على أحد الأمثلة فوق جدول الأنشطة، أو أدخل أنشطتك.
2. افصل بين الأنشطة السابقة المتعددة بفاصلة (مثل `4,5`)، واترك الحقل فارغًا أو اكتب `-` للنشاط الابتدائي.
3. يُعاد حساب الجدول تلقائيًا أثناء الكتابة.

## لأعضاء هيئة التدريس

- يحتوي الملف `docs/exercises.md` على تمارين للطلاب مبنية على الأمثلة الجاهزة.
- يحتوي الملف `docs/exercises-answers.md` على الإجابات. احذفه من النسخة العامة إن أردت استخدام التمارين في التقييم.

## الترخيص

- **الشيفرة البرمجية:** رخصة MIT.
- **الوثائق والأمثلة:** رخصة CC BY 4.0.
- **الاسم والشعار:** اسم مختبر ECI وشعاره غير مشمولين بهذه التراخيص، انظر `NOTICE.md`.

</div>
