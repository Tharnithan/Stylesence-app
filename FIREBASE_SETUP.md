# 🔥 Firebase Setup Guide for StyleSense

## Issue: Account Creation Not Working

### **Problem Identified:**
Your `firebase_options.dart` contains placeholder values instead of real Firebase project credentials.

### **Quick Fix: Manual Firebase Setup**

#### **Step 1: Create Firebase Project**
1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Create a project" or "Add project"
3. Enter project name: `stylesense-app` (or your preferred name)
4. Disable Google Analytics for now (can enable later)
5. Click "Create project"

#### **Step 2: Enable Authentication**
1. In Firebase Console, go to **Authentication**
2. Click **"Get started"**
3. Go to **"Sign-in method"** tab
4. Enable **Email/Password**:
   - Click on "Email/Password"
   - Toggle "Enable" to ON
   - Click "Save"

#### **Step 3: Set up Firestore Database**
1. Go to **Firestore Database**
2. Click **"Create database"**
3. Choose **"Start in production mode"**
4. Select location (choose closest to your users)
5. Click "Done"

#### **Step 4: Add Web App to Firebase**
1. In Firebase Console, click the **Web icon** (</>) on the project overview
2. Register app with nickname: `StyleSense Web`
3. **DO NOT** check "Firebase Hosting"
4. Click "Register app"
5. **COPY** the configuration object that appears

#### **Step 5: Update firebase_options.dart**
Replace the content in `lib/firebase_options.dart` with:

```dart
import 'package:firebase_core/firebase_core.dart';

class DefaultFirebaseOptions {
  static FirebaseOptions get currentPlatform {
    return const FirebaseOptions(
      apiKey: 'YOUR_API_KEY_HERE',           // From Firebase config
      appId: 'YOUR_APP_ID_HERE',             // From Firebase config  
      messagingSenderId: 'YOUR_SENDER_ID',   // From Firebase config
      projectId: 'YOUR_PROJECT_ID',          // From Firebase config
      storageBucket: 'YOUR_PROJECT_ID.appspot.com',
      authDomain: 'YOUR_PROJECT_ID.firebaseapp.com',
    );
  }
}
```

**Replace ALL the placeholder values with the actual values from step 4.**

### **Step 6: Test Account Creation**

After updating `firebase_options.dart`:

1. Save the file
2. Run: `flutter run -d chrome`
3. Try creating an account with:
   - Valid email (e.g., `test@example.com`)
   - Password (6+ characters)
   - Full name

### **Common Issues & Solutions:**

#### **Issue: "Firebase project not found"**
- Double-check the `projectId` in `firebase_options.dart`
- Ensure the Firebase project exists

#### **Issue: "Authentication disabled"**
- Go to Firebase Console → Authentication → Sign-in method
- Enable Email/Password authentication

#### **Issue: "CORS errors"**
- Add your domain to Firebase Auth settings
- Go to Authentication → Settings → Authorized domains

#### **Issue: "Network errors"**
- Check internet connection
- Verify Firebase project is active

### **Alternative: Quick Test Setup**

If you want to test immediately, I can create a temporary Firebase configuration:

```dart
// Temporary test configuration (replace with your own)
return const FirebaseOptions(
  apiKey: 'AIzaSyC_test_key_example',
  appId: '1:123456789:web:abcdef123456',
  messagingSenderId: '123456789',
  projectId: 'stylesense-test',
  storageBucket: 'stylesense-test.appspot.com',
  authDomain: 'stylesense-test.firebaseapp.com',
);
```

**⚠️ This is for testing only. Create your own Firebase project for production.**

### **Next Steps After Firebase Setup:**
1. Deploy Firestore security rules
2. Deploy Storage security rules  
3. Configure authentication providers
4. Set up analytics (optional)

Let me know if you need help with any of these steps!
