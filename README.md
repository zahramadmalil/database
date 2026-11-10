<div align="center">

# 🗄️ Streamlit Database CRUD Project

### 📘 مستندات جامع و آموزش مدیریت دیتابیس SQLite با رابط کاربری Streamlit

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.x-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)](https://streamlit.io/)
[![SQLite](https://img.shields.io/badge/SQLite-3-003B57?style=for-the-badge&logo=sqlite&logoColor=white)](https://www.sqlite.org/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

</div>

---

## 📖 درباره پروژه

این مخزن، یک **مجموعه آموزشی کامل و عملی** از کار با پایگاه داده **SQLite** در پایتون است که با یک **رابط کاربری وب (Web UI)** ساخته‌شده با **Streamlit** ترکیب شده است.

هدف این پروژه، آموزش نحوه ایجاد ارتباط با دیتابیس، تعریف جدول، و پیاده‌سازی عملیات **CRUD** (ایجاد، خواندن، به‌روزرسانی، حذف) از طریق یک رابط کاربری گرافیکی است. در این پروژه دو نسخه متفاوت پیاده‌سازی شده است: یکی بر اساس **شناسه (ID)** و دیگری بر اساس **عنوان (Title)** فیلم.

### 🗂️ فایل‌های پروژه

این پروژه شامل چهار فایل اصلی است:

| # | نام فایل | موضوع | سطح |
|---|---|---|---|
| ۱ | `app_db.py` | توابع دیتابیس (جستجو و حذف بر اساس ID) | 🟢 مقدماتی |
| ۲ | `app_ui.py` | رابط کاربری Streamlit (مدیریت بر اساس ID) | 🟡 متوسط |
| ۳ | `app_dbb.py` | توابع دیتابیس (جستجو و حذف بر اساس Title) | 🟡 متوسط |
| ۴ | `app_uii.py` | رابط کاربری Streamlit (مدیریت بر اساس Title) | 🔴 پیشرفته |

> ⚠️ **توجه:** پروژه شامل دو بخش جداگانه است. `app_db.py` و `app_ui.py` با دیتابیس `MoviesData.db` کار می‌کنند و `app_dbb.py` و `app_uii.py` با دیتابیس `MoviesDataa.db` کار می‌کنند. پیشنهاد می‌شود هر کدام را در پوشه‌های مجزا اجرا کنید.

---

## ✨ ویژگی‌های کلیدی

- ✅ **اتصال به SQLite:** استفاده از کتابخانه داخلی `sqlite3` بدون نیاز به نصب سرور دیتابیس.
- ✅ **عملیات CRUD کامل:** درج (Insert)، خواندن (Select)، آپدیت (Update) و حذف (Delete).
- ✅ **رابط کاربری تعاملی:** استفاده از Streamlit برای ساخت فرم‌ها، دکمه‌ها و منوهای کشویی.
- ✅ **جستجو بر اساس فیلدهای مختلف:** جستجو بر اساس شناسه (ID)، عنوان (Title) و امتیاز (IMDb Rate).
- ✅ **مدیریت خطا:** نمایش پیام‌های موفقیت یا خطا به کاربر در رابط کاربری.

---

## 🧰 پیش‌نیازها

قبل از اجرای پروژه، مطمئن شوید موارد زیر روی سیستم شما نصب شده‌اند:

- **Python** نسخه ۳.۸ یا بالاتر
- **pip** (مدیر بسته‌های پایتون)

---

## 🚀 نصب و راه‌اندازی

### ۱. کلون کردن مخزن
git clone https://github.com/your-username/streamlit-database-project.git
cd streamlit-database-project

### ۲. ساخت محیط مجازی (توصیه می‌شود)
در لینوکس / مک:
python -m venv venv
source venv/bin/activate

در ویندوز:
python -m venv venv
venv\Scripts\activate

### ۳. نصب وابستگی‌ها
pip install streamlit

---

## 🎯 نحوه استفاده

هر بخش از پروژه را می‌توانید به صورت مستقل با دستور زیر اجرا کنید:

بخش اول (مدیریت با ID):
streamlit run app_ui.py

بخش دوم (مدیریت با Title):
streamlit run app_uii.py

پس از اجرا، مرورگر شما به صورت خودکار باز می‌شود و می‌توانید با منوی سمت چپ، عملیات مختلف دیتابیس را انجام دهید.

---

## 📘 مستندات فایل ۱: `app_db.py` — توابع دیتابیس (بر اساس ID)

### 🎓 چه چیزی یاد می‌گیرید؟
این فایل لایه ارتباط با دیتابیس را پیاده‌سازی می‌کند. شامل توابعی برای ساخت جدول، درج، خواندن همه رکوردها، خواندن با ID، آپدیت و حذف است.

### 🗂️ ساختار جدول
- **جدول `movies`:** شامل ستون‌های `id`, `title`, `year`, `country`, `imdb_rate`.

### 💻 نمونه کدهای آموزش‌داده‌شده

۱. ایجاد جدول:
def create_table():
    query = 'CREATE TABLE IF NOT EXISTS movies (id INTEGER PRIMARY KEY AUTOINCREMENT, title TEXT, year TEXT, country TEXT, imdb_rate REAL)'
    cursor.execute(query)

۲. خواندن همه رکوردها:
def select_all_records():
    rows = cursor.execute('SELECT * FROM movies').fetchall()
    return rows

۳. حذف با ID:
def delete_record_by_id(id):
    cursor.execute('DELETE FROM movies WHERE id = ?', (id,))
    conn.commit()

---

## 📗 مستندات فایل ۲: `app_ui.py` — رابط کاربری (بر اساس ID)

### 🎓 چه چیزی یاد می‌گیرید؟
این فایل یاد می‌دهد چطور با Streamlit یک رابط کاربری کامل برای انجام عملیات دیتابیس بسازید. شما از `st.sidebar.selectbox` برای انتخاب عملیات و از `st.button` و `st.text_input` برای دریافت ورودی استفاده می‌کنید.

### 💻 نمونه کدهای آموزش‌داده‌شده

۱. منوی کناری:
option = st.sidebar.selectbox('Select Your Option:', ('SELECT ALL RECORDS', 'INSERT RECORD', ...))

۲. فرم درج رکورد جدید:
title = st.text_input('Movie Title:')
if st.button('ADD MOVIE'):
    app_db.insert_record(title, year, country, imdb_rate)
    st.success('Movie added successfully!')

---

## 📙 مستندات فایل ۳: `app_dbb.py` — توابع دیتابیس (بر اساس Title)

### 🎓 چه چیزی یاد می‌گیرید؟
این فایل نسخه دوم لایه دیتابیس است که به جای جستجو و حذف با ID، از **عنوان فیلم** استفاده می‌کند. همچنین تابع جدیدی برای جستجو بر اساس **امتیاز IMDb** به آن اضافه شده است.

### 💻 نمونه کدهای آموزش‌داده‌شده

۱. جستجو با عنوان:
def select_record_by_title(title):
    row = cursor.execute('SELECT * FROM movies WHERE title = ?', (title,)).fetchone()
    return row

۲. جستجو با امتیاز:
def select_record_by_imdb_rate(imdb_rate):
    row = cursor.execute('SELECT * FROM movies WHERE imdb_rate = ?', (imdb_rate,)).fetchone()
    return row

۳. حذف با عنوان:
def delete_record_by_title(title):
    cursor.execute('DELETE FROM movies WHERE title = ?', (title,))
    conn.commit()

---

## 📕 مستندات فایل ۴: `app_uii.py` — رابط کاربری (بر اساس Title)

### 🎓 چه چیزی یاد می‌گیرید؟
این فایل رابط کاربری نسخه دوم است. منوی آن شامل گزینه‌های جدیدی مثل «جستجو با عنوان» و «جستجو با امتیاز» است و فرم‌ها با توجه به نوع عملیات تغییر می‌کنند.

### 💻 نمونه کدهای آموزش‌داده‌شده

۱. منوی کناری با گزینه‌های جدید:
option = st.sidebar.selectbox('Select Your Option:', ('select_record_by_title', 'select_record_by_imdb_rate', ...))

۲. فرم آپدیت بر اساس عنوان:
update_title = st.text_input('Enter Record title to Update:')
if st.button('UPDATE RECORD'):
    app_dbb.update_record_by_title(update_title, new_year, new_country, new_imdb)
    st.success('Record updated successfully!')

---

## 🗂️ ساختار پیشنهادی پروژه

streamlit-database-project/
│
├── app_db.py              # توابع دیتابیس (بر اساس ID)
├── app_ui.py              # رابط کاربری (بر اساس ID)
├── app_dbb.py             # توابع دیتابیس (بر اساس Title)
├── app_uii.py             # رابط کاربری (بر اساس Title)
├── MoviesData.db          # دیتابیس بخش اول (پس از اجرا ساخته می‌شود)
├── MoviesDataa.db         # دیتابیس بخش دوم (پس از اجرا ساخته می‌شود)
├── requirements.txt       # لیست وابستگی‌ها
├── README.md              # همین فایل
└── .gitignore             # فایل‌های نادیده‌گرفته‌شده

---

## 🧠 مفاهیم کلیدی آموزش‌داده‌شده

<details>
<summary><b>🔹 ۱. SQLite چیست؟</b></summary>
SQLite یک پایگاه داده سبک و فایلی است که به صورت پیش‌فرض همراه پایتون نصب می‌شود. برای استفاده از آن نیازی به نصب سرور جداگانه ندارید و تمام داده‌ها در یک فایل `.db` ذخیره می‌شوند.
</details>

<details>
<summary><b>🔹 ۲. پارامتر گذاری در کوئری‌ها (?)</b></summary>
به جای چسباندن مستقیم مقادیر در رشته SQL، از علامت `?` استفاده می‌کنیم و مقادیر را به صورت یک تاپل به `cursor.execute` می‌دهیم. این کار از حمله SQL Injection جلوگیری می‌کند.
</details>

<details>
<summary><b>🔹 ۳. تفاوت SELECT و UPDATE و DELETE</b></summary>
- SELECT: برای خواندن داده‌هاست و نیازی به `commit()` ندارد.
- UPDATE و DELETE: برای تغییر داده‌هاست و حتماً باید بعد از آن `conn.commit()` را صدا بزنیم تا تغییرات ذخیره شوند.
</details>

---

## 🐛 عیب‌یابی رایج (Troubleshooting)

| مشکل | راه‌حل |
|------|--------|
| `no such table: movies` | جدول ساخته نشده است. کافی است یک بار تابع `create_table()` را اجرا کنید. |
| داده‌ها ذخیره نمی‌شوند | فراموش کرده‌اید `conn.commit()` را بعد از عملیات بنویسید. |
| Streamlit اجرا نمی‌شود | به جای `python app_ui.py` از دستور `streamlit run app_ui.py` استفاده کنید. |
| خطای `UNIQUE constraint failed` | در تلاش برای درج رکورد تکراری با همان شناسه هستید. دیتابیس را پاک کنید. |

---

## 🤝 مشارکت

از مشارکت شما در این پروژه استقبال می‌شود! برای همکاری:

1. پروژه را **Fork** کنید.
2. یک شاخه جدید بسازید: `git checkout -b feature/amazing-feature`
3. تغییرات خود را **Commit** کنید: `git commit -m "Add some amazing feature"`
4. شاخه را **Push** کنید: `git push origin feature/amazing-feature`
5. یک **Pull Request** باز کنید 🎉

---

## 📚 منابع پیشنهادی

- 📘 [مستندات رسمی SQLite](https://www.sqlite.org/docs.html)
- 📗 [مستندات رسمی Streamlit](https://docs.streamlit.io/)
- 📕 [آموزش SQL در W3Schools](https://www.w3schools.com/sql/)

---

## 📄 مجوز

این پروژه تحت مجوز **MIT** منتشر شده است. برای اطلاعات بیشتر فایل [LICENSE](LICENSE) را مطالعه کنید.

---

<div align="center">

### ⭐ اگر این پروژه برایتان مفید بود، به آن ستاره بدهید! ⭐

ساخته شده با ❤️ و Python

</div>
