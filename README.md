# Davomat jurnali — Android ilova (tekin)

Papkadagi 7 ta fayl tayyor. Ular **hech narsa sozlamasdan ham** ishlaydi (ma'lumot faqat shu telefonda saqlanadi).
Bir nechta odamga ko'rsatish uchun Firebase'ni ulang (2-qadam).

## 1-qadam. Saytga joylash (GitHub Pages, tekin)
1. github.com da hisob oching, "New repository" bosing (nomi: davomat, Public).
2. "uploading an existing file" orqali shu papkadagi hamma fayllarni yuklang.
3. Settings -> Pages -> Branch: main -> Save.
4. 1-2 daqiqada havola chiqadi: `https://SIZNING_NOM.github.io/davomat/`

## 2-qadam. Firebase (hamma ko'rishi uchun, tekin Spark tarifi)
1. console.firebase.google.com -> "Add project" (Analytics shart emas).
2. "Build -> Firestore Database" -> Create database (production mode, yaqin joylashuv).
3. "Build -> Authentication" -> Get started -> Email/Password ni yoqing -> "Users" bo'limida o'zingizga foydalanuvchi qo'shing (email + parol). Bu o'qituvchi hisobi.
4. Firestore -> Rules ga quyidagini qo'ying (SIZNING_EMAIL o'rniga o'z emailingiz):
```
rules_version = '2';
service cloud.firestore {
  match /databases/{db}/documents {
    match /contacts/{d} {
      allow read, write: if request.auth != null && request.auth.token.email == "SIZNING_EMAIL";
    }
    match /{coll}/{d} {
      allow read: if coll != "contacts";
      allow write: if request.auth != null && request.auth.token.email == "SIZNING_EMAIL";
    }
  }
}
```
5. Project settings -> "Your apps" -> Web (</>) -> ilova qo'shing. Chiqqan `apiKey`, `authDomain`, `projectId`, `appId` qiymatlarini `firebase-config.js` ichiga yozing va GitHub'da faylni yangilang.
6. Authentication -> Settings -> Authorized domains ga `SIZNING_NOM.github.io` ni qo'shing.

Natija: havolani ochgan hamma davomatni ko'radi, faqat siz "O'qituvchi kirishi" orqali belgilay olasiz. Ota-ona telefon raqamlari esa faqat siz kirganingizda ko'rinadi (qoida shuni ta'minlaydi).

## 3-qadam. Android'ga o'rnatish
- **Eng oson:** Chrome'da havolani oching -> ⋮ menyu -> "Ilovani o'rnatish" (Install app). Bosh ekranda ikonka paydo bo'ladi.
- **APK kerak bo'lsa:** pwabuilder.com ga havolani kiriting -> Package for stores -> Android -> APK yuklab oling (tekin). Play Market'ga qo'yish esa $25.

## 4-qadam. Ota-ona raqamlarini kiritish (bir marta)
Raqamlar xavfsizlik uchun fayllar ichida emas (GitHub sayti ochiq, uni hamma ko'ra oladi).
Firebase ulangach: ilovada "O'qituvchi kirishi" -> "O'quvchilar" bo'limi -> pastdagi "Raqamlarni ro'yxatdan import qilish" ni oching, "Familiya Ism — 90 123 45 67" ko'rinishidagi ro'yxatni joylab "Import qilish" ni bosing. Ismlar avtomatik moslashadi.

## Eslatma
- Eski ma'lumotlar (Claude ichidagi) bu ilovaga o'tmaydi, davomatni qaytadan boshlaysiz. Ro'yxatdagi ismlar tayyor.
