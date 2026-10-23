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

## טבלת שיאים (Firebase Realtime Database)
הטבלה כבויה עד שממלאים את `LB_URL` ב-`index.html`. הגדרה חד-פעמית:
1. https://console.firebase.google.com > פרויקט > Build > Realtime Database > Create database.
2. בלשונית Rules מדביקים את התוכן של `database.rules.json` ולוחצים Publish.
3. בלשונית Data מעתיקים את הכתובת שמופיעה למעלה (`https://...firebasedatabase.app`) לתוך `LB_URL`.

ההגנה היא החוקים: אפשר רק להוסיף שחקן או להעלות לו ניקוד, לא למחוק ולא להוריד.
מי שמבין בקוד יכול לשלוח ניקוד מזויף. לטבלה בין חברים זה מספיק.

## העלאה לגוגל פליי
ה-APK של debug טוב להתקנה ישירה, לא לחנות. בשביל החנות:
Android Studio > Build > Generate Signed App Bundle > `.aab`.
צור keystore ושמור אותו וגם את הסיסמה במקום בטוח. אם תאבד אותו לא תוכל לעדכן את האפליקציה.

- חשבון מפתח בגוגל פליי עולה 25$ חד-פעמי, ודורש גיל 18+ (חשבון של הורה).
- חשבון אישי חדש חייב Closed testing עם 12 בודקים ל-14 ימים רצופים לפני שאפשר לפרסם.
- השם "פאקמן" והדמויות הם סימן מסחרי של Bandai Namco. לשיתוף בין חברים זה בסדר, אבל לפני גוגל פליי חייבים לשנות שם, אחרת האפליקציה תיחסם.
