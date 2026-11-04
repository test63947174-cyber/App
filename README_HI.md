# RND Staking Android App — Fresh Build

यह प्रोजेक्ट Android WebView ऐप है। ऐप खुलने पर `https://staking.randigital.in/login.html` लोड करता है। वेबसाइट के मौजूदा लॉगिन, Firebase Auth और Realtime Database सिस्टम को ही इस्तेमाल किया जाता है। वेबसाइट के HTML/CSS/JS में बदलाव वेबसाइट पर प्रकाशित होने के बाद ऐप में अगली बार पेज reload/open होने पर दिखाई देंगे। Native Android कोड बदलने पर नया APK बनाना होगा।

## Firebase

दिए गए वेबसाइट ZIP के `firebase.js` में Firebase project ID `rnd2-70080` है। इस Android wrapper में अलग Firebase configuration या दूसरा login/database नहीं बनाया गया है। वेबसाइट का मौजूदा Firebase code ही चलता है।

## इस बार पिछले build errors से बचाव

- `rnd_navy` रंग केवल `app/src/main/res/values/colors.xml` में एक बार घोषित है।
- `styles.xml` में `rnd_navy` दोबारा define नहीं किया गया है; वह केवल `@color/rnd_navy` को reference करता है।
- `values-v31` directory और `postSplashScreenTheme` attribute शामिल नहीं हैं। इससे पिछले `android:attr/postSplashScreenTheme not found` error का स्रोत हटता है।
- कोई AndroidX/AppCompat या Kotlin plugin dependency नहीं है; ऐप Java में Android framework `Activity` और WebView का उपयोग करता है।

## GitHub पर नया repository बनाना

1. GitHub में नया खाली repository बनाएँ। उदाहरण नाम: `RND-Staking-Android`।
2. इस ZIP की अंदर की सभी फाइलें और folders repository की root में upload करें। ध्यान रहे कि `.github/workflows/build-apk.yml` भी upload हो।
3. सभी फाइलें `main` branch में commit करें।
4. GitHub repository में **Actions** खोलें। Workflow `Build RND Staking Android APK` दिखाई देगा।
5. जरूरत हो तो workflow खोलकर **Run workflow** दबाएँ। Push करने पर भी build अपने-आप शुरू होगा।
6. सफल run खोलें और नीचे **Artifacts** में `RND-Staking-Android-APK` डाउनलोड करें। ZIP extract करने पर `app-debug.apk` मिलेगा।

## जरूरी जाँच

पहला APK केवल DEBUG/testing build है, Play Store/public release के लिए signed release APK/AAB नहीं है। APK को पहले फोन में install करके login, registration, dashboard, package, deposit, withdrawal, referral, transfer, support और download flows जाँचें।

Google OAuth/Google Sign-In कुछ स्थितियों में embedded WebView को रोक सकता है। Email/password login पहले test करें। यदि Google Sign-In जरूरी है, तो native Google sign-in integration अलग से जोड़नी होगी।

## सुरक्षा/सीमा

- Firebase Realtime Database rules और Auth सुरक्षा Firebase Console में लागू रहती हैं; Android app में admin credentials hardcode न करें।
- यह ऐप remote live website खोलता है; ZIP में `website-source/` केवल दिए गए source का reference/copy है। यह वेबसाइट को अपने-आप deploy या modify नहीं करता।
- Android Studio आपके कंप्यूटर पर आवश्यक नहीं है; GitHub Actions cloud runner build करता है।

## ZIP source audit में मिला अतिरिक्त Firebase mismatch

मूल ZIP के `support.html` में Firebase project `mywebsite-600d3` था, जबकि बाकी मुख्य पेज `rnd2-70080` इस्तेमाल कर रहे हैं। इस fresh project की `website-source/support.html` कॉपी में इसे `rnd2-70080` से align किया गया है। ध्यान दें: यह केवल repository में रखी source-copy का सुधार है; live website पर इसे लागू करने के लिए corrected `support.html` को वेबसाइट hosting पर भी publish करना होगा।

## ZIP source audit में मिला अतिरिक्त Firebase mismatch

मूल ZIP के `support.html` में Firebase project `mywebsite-600d3` था, जबकि बाकी मुख्य पेज `rnd2-70080` इस्तेमाल कर रहे हैं। इस fresh project की `website-source/support.html` कॉपी में इसे `rnd2-70080` से align किया गया है। ध्यान दें: यह केवल repository में रखी source-copy का सुधार है; live website पर इसे लागू करने के लिए corrected `support.html` को वेबसाइट hosting पर भी publish करना होगा।
