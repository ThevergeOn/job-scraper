<div dir="rtl">

# 🤖 ربات تلگرامی جستجوی شغل سئو

یه ربات رایگان که هر روز صبح از سایت‌های لینکدین، Indeed، Glassdoor و غیره آگهی‌های شغلی سئو رو جمع‌آوری میکنه و مستقیم برات توی تلگرام میفرسته.

**نیازی به سرور یا هزینه‌ای نیست** — همه چیز روی GitHub Actions رایگان اجرا میشه.

---

## ✨ امکانات

- 🔍 جستجوی روزانه خودکار در تمام سایت‌های شغلی
- 📱 ارسال مستقیم به تلگرام
- ⛔ فیلتر هوشمند آگهی‌های نامناسب (Senior، US only و غیره)
- 💰 نمایش حقوق (اگر در آگهی ذکر شده باشد)
- 🔁 جلوگیری از ارسال تکراری آگهی‌های قبلی
- 📊 آرشیو اختیاری در Google Sheets

---

## 📋 پیش‌نیازها

فقط به این ۳ چیز نیاز داری:

| چی نیاز داری | رایگانه؟ | لینک |
|---|---|---|
| اکانت GitHub | ✅ بله | [github.com](https://github.com) |
| اکانت RapidAPI (برای JSearch) | ✅ بله | [rapidapi.com](https://rapidapi.com/letscrape-6bRBa3QguO5/api/jsearch) |
| یه ربات تلگرام | ✅ بله | [@BotFather](https://t.me/BotFather) |

---

## 🚀 راه‌اندازی گام به گام

### گام ۱ — Fork کردن این پروژه

> **Fork یعنی چی؟** یعنی یه کپی از این پروژه توی اکانت خودت میسازی.

1. بالای همین صفحه دکمه **Fork** رو بزن

   ![Fork button](https://docs.github.com/assets/cb-40142/mw-1440/images/help/repository/fork-button.webp)

2. در صفحه بعد روی **Create fork** کلیک کن

3. الان یه نسخه از این پروژه توی اکانت خودت هست ✅

---

### گام ۲ — گرفتن API Key از RapidAPI (JSearch)

> این کلید به ربات اجازه میده آگهی‌های شغلی رو جستجو کنه.

1. برو به [این لینک](https://rapidapi.com/letscrape-6bRBa3QguO5/api/jsearch) و با ایمیل ثبت‌نام کن

2. بعد از ورود، همان صفحه JSearch باز هست. روی تب **Pricing** کلیک کن

3. پلن **BASIC** رو انتخاب کن (رایگان — ۲۰۰ ریکوئست در ماه)

   > 💡 با ۵ کوئری روزانه = ~۱۵۰ ریکوئست در ماه. کاملاً در محدوده رایگان.

4. بعد از subscribe، از منوی بالای سایت روی **My Apps** کلیک کن

5. یه App انتخاب کن (یا بساز)، بعد تب **Authorization** رو بزن

6. **API Key** رو پیدا کن — یه رشته طولانی از حروف و عدده. این رو کپی و یه جای امن ذخیره کن.

   شکل API Key: `36e8988a43mshXXXXXXXXXXXXXXXXXXXXX`

---

### گام ۳ — ساخت ربات تلگرام

1. توی تلگرام، به [@BotFather](https://t.me/BotFather) پیام بده

2. دستور `/newbot` رو بفرست

3. یه اسم برای ربات بده (مثلاً: `Job Alert Bot`)

4. یه username بده که باید به `bot` ختم بشه (مثلاً: `my_seo_job_bot`)

5. BotFather یه **توکن** بهت میده — شبیه این:
   ```
   8911114373:AAGn_K6PQm3yLpo7fbc8PinmuRb6fEp6TrU
   ```
   این رو کپی کن ✅

6. حالا باید **آیدی عددی تلگرام** خودت رو پیدا کنی:
   - به [@userinfobot](https://t.me/userinfobot) پیام بده
   - یه عدد بهت میده — این **Chat ID** توئه (مثلاً `359353459`)

7. **مهم:** به ربات خودت پیام بده (یه /start بفرست) تا فعال بشه

---

### گام ۴ — ذخیره کردن کلیدها در GitHub Secrets

> **Secrets چیه؟** جایی که GitHub کلیدهای محرمانه‌ات رو مثل پسورد نگه میداره — هیچ‌کس توی کد نمیتونه ببینه.

1. برو به ریپوی Fork شده‌ات در GitHub

2. روی **Settings** کلیک کن (تب بالا)

3. از منوی سمت چپ برو به:  
   `Secrets and variables` → `Actions`

4. دکمه **New repository secret** رو بزن

5. این ۳ تا Secret رو یکی یکی اضافه کن:

   ---
   
   **Secret اول:**
   - Name: `RAPIDAPI_KEY`
   - Secret: کلید API که از RapidAPI کپی کردی
   - دکمه **Add secret** رو بزن

   ---

   **Secret دوم:**
   - Name: `TELEGRAM_BOT_TOKEN`
   - Secret: توکنی که BotFather داد (مثلاً `8911114373:AAGn_...`)
   - دکمه **Add secret** رو بزن

   ---

   **Secret سوم:**
   - Name: `TELEGRAM_CHAT_ID`
   - Secret: آیدی عددی تلگرامت (مثلاً `359353459`)
   - دکمه **Add secret** رو بزن

   ---

   بعد از اتمام، باید ۳ تا Secret داشته باشی:
   
   ```
   ✅ RAPIDAPI_KEY
   ✅ TELEGRAM_BOT_TOKEN  
   ✅ TELEGRAM_CHAT_ID
   ```

---

### گام ۵ — تست اولیه (اجرای دستی)

1. در ریپوی خودت روی تب **Actions** کلیک کن

2. اگه پیام زرد رنگ دیدی که گفت "Workflows aren't being run on this forked repository" روی دکمه **I understand my workflows, enable them** کلیک کن

3. از سمت چپ **Job Search Bot 🤖** رو انتخاب کن

4. دکمه **Run workflow** رو بزن → **Run workflow** رو تأیید کن

5. صبر کن چند ثانیه، بعد صفحه رو Refresh کن

6. باید یه Run با دایره سبز ✅ ببینی

7. **توی تلگرام چک کن** — ربات باید پیام فرستاده باشه!

---

## ⚙️ شخصی‌سازی — تغییر کلمات جستجو

فایل `bot.py` رو در GitHub باز کن و این بخش رو پیدا کن:

```python
SEARCH_QUERIES = [
    "Junior SEO remote",
    "Technical SEO remote",
    "SEO Content Editor remote",
    "SEO Python remote",
    "WordPress SEO Specialist remote",
]
```

**چطور ویرایش کنی؟**

1. روی فایل `bot.py` کلیک کن
2. دکمه ✏️ (Edit) رو بزن
3. کلمات جستجو رو تغییر بده
4. پایین صفحه **Commit changes** رو بزن

**نمونه کوئری‌های مختلف:**

```python
# برای دیجیتال مارکتینگ
"digital marketing specialist remote"
"social media manager remote"
"content marketing remote"

# برای طراحی
"UI UX designer remote"
"graphic designer remote"

# برای توسعه
"python developer remote"
"react developer remote"
"frontend developer remote"

# برای داده
"data analyst remote"
"data scientist remote"

# با فیلتر پلتفرم خاص
"SEO specialist remote via linkedin"
"marketing manager remote via indeed"
```

> 💡 **نکته:** هر کوئری = ۱ ریکوئست در ماه. با ۵ کوئری و اجرای روزانه = حدود ۱۵۰ ریکوئست در ماه که در محدوده پلن رایگان (۲۰۰ تا) هست.

---

## ⛔ شخصی‌سازی فیلتر Blacklist

این بخش رو در `bot.py` پیدا کن:

```python
BLACKLIST_KEYWORDS = [
    "us residents only",
    "must reside in us",
    "senior",
    "director",
    "agency",
    "full stack",
]
```

هر کلمه‌ای که اضافه کنی، آگهی‌هایی که اون کلمه رو در توضیحاتشون دارن فیلتر میشن.

---

## ⏰ تغییر زمان اجرا

ربات الان هر روز **ساعت ۷ صبح به وقت ایران** اجرا میشه.

برای تغییر، فایل `.github/workflows/run.yml` رو باز کن و این خط رو پیدا کن:

```yaml
- cron: "30 3 * * *"
```

| میخوای ساعت چند باشه؟ | مقدار cron |
|---|---|
| ۶ صبح ایران | `"30 2 * * *"` |
| ۷ صبح ایران | `"30 3 * * *"` |
| ۸ صبح ایران | `"30 4 * * *"` |
| ۲ بار در روز (۷ص و ۵ع) | `"30 3 * * *\n    - cron: \"30 13 * * *\""` |

> زمان UTC است. ایران = UTC+3:30

---

## 📊 اضافه کردن Google Sheets (اختیاری)

اگه میخوای آگهی‌ها علاوه بر تلگرام توی یه فایل اکسل آنلاین هم ذخیره بشن، فایل `SETUP_GSHEET.md` رو بخون.

---

## ❓ سوالات رایج

**ربات پیامی نفرستاد — چیکار کنم؟**
1. برو به تب **Actions** در GitHub
2. روی آخرین Run کلیک کن
3. روی **run-bot** کلیک کن
4. لاگ‌ها رو بخون — معمولاً خطا واضحه

**خطای `RAPIDAPI_KEY` داد:**
Secret رو درست وارد کردی؟ هیچ فاصله اضافه‌ای نباشه.

**ربات تلگرام جواب نمیده:**
مطمئن شو که به ربات `/start` فرستادی.

**آگهی‌های تکراری میاد:**
فایل `seen_jobs.txt` هنوز ساخته نشده. بعد از دومین اجرا حل میشه.

---

## 🙏 Credits

- جستجوی شغل: [JSearch API](https://rapidapi.com/letscrape-6bRBa3QguO5/api/jsearch) by OpenWeb Ninja
- اجرای خودکار: [GitHub Actions](https://github.com/features/actions) (رایگان)
- ارسال پیام: [Telegram Bot API](https://core.telegram.org/bots/api) (رایگان)

</div>
