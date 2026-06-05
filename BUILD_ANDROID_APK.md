# ساخت فایل نصبی APK برای اندروید (چک‌لیست روزانه)

دو راه اصلی و آسان برای تبدیل این PWA به اپ واقعی اندروید:

## راه ۱: سریع‌ترین روش (توصیه می‌شود) — PWABuilder (بدون نصب هیچ چیز)
1. به سایت https://pwabuilder.com بروید.
2. لینک اپ را وارد کنید (اگر روی هاست آپلود کردید) یا فایل‌ها را زیپ کنید و آپلود کنید.
3. روی "Build" کلیک کنید.
4. در بخش Android گزینه "Generate Package" را بزنید.
5. APK آماده دانلود می‌شود (حتی نسخه signed).
6. روی گوشی نصب کنید.

این روش در کمتر از ۲ دقیقه APK می‌دهد و برای اکثر کاربران عالی است.

## راه ۲: با Capacitor (برای کنترل بیشتر + قابلیت‌های native)

ما در پوشه `native/` یک پروژه Capacitor آماده کردیم.

### مراحل ساخت APK روی کامپیوتر خودتان:

1. **نصب پیش‌نیازها** (یک بار):
   - Node.js (که دارید)
   - Android Studio (دانلود از developer.android.com)
   - در Android Studio: SDK Manager → نصب Android SDK (حداقل API 24) + Build Tools + Platform Tools

2. **کپی پروژه**:
   - پوشه `native/` را روی کامپیوتر خودتان کپی کنید.
   - یا اگر فایل‌ها را روی گیت‌هاب گذاشتید، کلون کنید.

3. **نصب وابستگی‌ها**:
   ```bash
   cd native
   npm install
   ```

4. **همگام‌سازی با اندروید** (اگر تغییر دادید):
   ```bash
   npx cap sync android
   ```

5. **باز کردن در Android Studio** (بهترین روش):
   ```bash
   npx cap open android
   ```
   - در Android Studio روی دکمه Run (▶️) کلیک کنید تا روی emulator یا گوشی واقعی بیلد و نصب شود.
   - برای APK: Build → Build Bundle(s)/APK(s) → Build APK(s)

6. **بیلد مستقیم از خط فرمان** (اگر gradle دارید):
   ```bash
   cd native/android
   ./gradlew assembleDebug
   ```
   APK در مسیر `native/android/app/build/outputs/apk/debug/app-debug.apk` ساخته می‌شود.

### نکات مهم برای APK واقعی:
- نام پکیج: `ir.arena.dailychecklist` (در capacitor.config.json می‌توانید تغییر دهید)
- برای انتشار در گوگل پلی: باید امضا کنید (signing key) و از نسخه release استفاده کنید.
- برای نوتیفیکیشن‌های بهتر در حالت بسته بودن اپ، بعداً می‌توان Firebase Cloud Messaging اضافه کرد.

### اضافه کردن قابلیت‌های native (مثال)
- نوتیفیکیشن محلی قوی‌تر
- ویجت اندروید
- دسترسی به تقویم
- ذخیره‌سازی بهتر

بعد از آماده شدن پروژه Capacitor، می‌توانید پلاگین‌های Capacitor اضافه کنید.

---

**فایل‌های آماده در این پروژه:**
- `index.html` + `manifest.json` + `sw.js` + `icons/` → وب‌اپ اصلی (PWA)
- `native/` → پروژه Capacitor آماده برای ساخت APK

اگر در ساخت APK گیر کردید، بگویید تا راهنمایی دقیق‌تری بدهم یا فایل خاصی آماده کنم.