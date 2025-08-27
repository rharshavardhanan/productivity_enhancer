# Login System Integration

This document explains how to set up the login system for your application.

## Overview

The login system uses Firebase Authentication to handle user authentication. It includes:

- Email/password authentication
- Google Sign-In
- Protected routes that redirect to the login page when not authenticated
- Logout functionality

## Setup Instructions

### 1. Install Firebase

```bash
npm install firebase
```

### 2. Create a Firebase project

1. Go to the [Firebase Console](https://console.firebase.google.com/)
2. Click "Add project" and follow the setup steps
3. Once your project is created, click on "Web" to add a web app to your project
4. Register your app with a nickname (e.g., "prodpanda-web")
5. Copy the Firebase configuration object

### 3. Update Firebase Configuration

Open `src/contexts/AuthContext.jsx` and replace the placeholder Firebase configuration with your own:

```javascript
// Firebase configuration
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_AUTH_DOMAIN",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_STORAGE_BUCKET",
  messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
  appId: "YOUR_APP_ID",
};
```

### 4. Enable Authentication Methods in Firebase

1. In the Firebase Console, go to your project
2. Click on "Authentication" in the left sidebar
3. Click on "Sign-in method" tab
4. Enable the following providers:
   - Email/Password
   - Google

For Google authentication, you may need to configure the OAuth consent screen in the Google Cloud Console.

## How It Works

### Authentication Flow

1. When a user visits any protected route, the `PrivateRoute` component checks if they are authenticated
2. If not authenticated, they are redirected to the `/login` page
3. After successful login, users are redirected to the route they were trying to access

### Login Methods

- **Email/Password**: Users can create an account or sign in with their email and password
- **Google Sign-In**: Users can sign in with their Google account

### Logout

- Users can log out by clicking the logout button in the sidebar
- After logout, they will be redirected to the login page

## Customization

### UI Customization

The login page uses the existing styles from your login-page folder. To customize the appearance:

- Update the CSS in `src/login-page/login-page.css`
- Modify the Login component in `src/components/Login.jsx`

### Firebase Rules

For production use, make sure to set up proper security rules in Firebase:

1. Go to Firebase Console > Authentication > Users
2. Set up Email Templates for verification emails, password reset, etc.
3. Configure Firebase Security Rules for any Firebase services you use

## Troubleshooting

- **Firebase initialization error**: Make sure your Firebase configuration is correct
- **Google Sign-In issues**: Verify that you've properly set up OAuth consent screen and enabled the Google provider
- **"auth/configuration-not-found" error**: Your Firebase project might not be properly configured for the authentication methods you're trying to use 