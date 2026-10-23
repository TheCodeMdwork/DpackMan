# פאקמן

משחק קלאסי של אכילת נקודות. אתר (PWA) שעטוף כאפליקציית אנדרואיד עם Capacitor.
פרויקט האנדרואיד כבר נוצר בתיקייה `android/`, כולל אייקונים.

## הרצה בדפדפן
    npm run serve        # http://localhost:8080

## בניית APK

### אפשרות א': GitHub Actions (בלי להתקין כלום)
1. העלה את התיקייה ל-repo חדש ב-GitHub (branch בשם `main`).
2. הקובץ `.github/workflows/build-apk.yml` יבנה את ה-APK אוטומטית בכל push.
3. בלשונית Actions בוחרים את הריצה האחרונה, ומורידים את `chomper-apk` מתחתית העמוד.
4. מעבירים את `app-debug.apk` לטלפון ומתקינים (צריך לאשר "התקנה ממקורות לא ידועים").

### אפשרות ב': על המחשב שלך (Android Studio + JDK 21)
    npm install
    npm run android:sync
    cd android && ./gradlew assembleDebug
    # הקובץ: android/app/build/outputs/apk/debug/app-debug.apk

או `npm run android:open` ואז Run מתוך Android Studio.

## טבלת שיאים (Firebase Realtime Database + Authentication)
- כל שחקן מתחבר אוטומטית בחשבון אנונימי, ולא יכול לשחק בלי לבחור שם.
- השם ייחודי (אין שני "דניאל") וקבוע. אי אפשר לשנות אותו אחר כך.
- כל שחקן יכול רק להעלות את הניקוד של עצמו. אי אפשר לגעת בניקוד של אחרים.
- רק המנהל מוחק תוצאות: מקישים 5 פעמים על הכותרת "פאקמן" ומתחברים עם אימייל וסיסמה.

הגדרה: ב-`index.html` ממלאים את `LB.db` ואת `LB.apiKey`, וב-`database.rules.json`
מחליפים את `ADMIN_UID` ב-User UID של המנהל ומדביקים את הקובץ בלשונית Rules של Realtime Database.

## העלאה לגוגל פליי
ה-APK של debug טוב להתקנה ישירה, לא לחנות. בשביל החנות:
Android Studio > Build > Generate Signed App Bundle > `.aab`.
צור keystore ושמור אותו וגם את הסיסמה במקום בטוח. אם תאבד אותו לא תוכל לעדכן את האפליקציה.

- חשבון מפתח בגוגל פליי עולה 25$ חד-פעמי, ודורש גיל 18+ (חשבון של הורה).
- חשבון אישי חדש חייב Closed testing עם 12 בודקים ל-14 ימים רצופים לפני שאפשר לפרסם.
- השם "פאקמן" והדמויות הם סימן מסחרי של Bandai Namco. לשיתוף בין חברים זה בסדר, אבל לפני גוגל פליי חייבים לשנות שם, אחרת האפליקציה תיחסם.
