# Slumbr Authentication System

This document explains how to properly set up the authentication system for the Slumbr app.

## Current Implementation

The current implementation provides a fully functional authentication system with:

- Email/password login and registration
- Google sign-in (mocked)
- Apple sign-in (mocked)
- User persistence via UserDefaults (simplified)

This implementation is for demonstration purposes. In a production environment, you would need to implement proper backend integration and secure storage methods.

## Setting Up Google Sign-In in a Real Project

1. **Register your app in Google Cloud Platform**:
   - Go to the [Google Cloud Console](https://console.cloud.google.com/)
   - Create a new project
   - Go to "APIs & Services" > "Credentials"
   - Click "Create Credentials" > "OAuth client ID"
   - Select "iOS" as the application type
   - Enter your bundle ID and app name
   - Download the `GoogleService-Info.plist` file

2. **Add the GoogleSignIn SDK**:
   - Add the following to your Podfile:
     ```ruby
     pod 'GoogleSignIn', '~> 6.2'
     ```
   - Run `pod install`

3. **Configure URL schemes**:
   - Add the reversed client ID from your `GoogleService-Info.plist` file to your Info.plist under `CFBundleURLTypes`
   - The format is: `com.googleusercontent.apps.[YOUR_CLIENT_ID]`

4. **Replace the mock implementation**:
   - Import the proper GoogleSignIn SDK
   - Initialize GIDSignIn in your AppDelegate
   - Implement sign-in methods using the official SDK
   - Handle the authentication callback

## Setting Up Apple Sign-In in a Real Project

1. **Enable Apple Sign-In in your app**:
   - In Xcode, go to your project settings
   - Select your app target
   - Go to "Signing & Capabilities"
   - Click "+" and add "Sign in with Apple"

2. **Add the capability to your app**:
   - Add the following to your Info.plist file:
     ```xml
     <key>com.apple.developer.applesignin</key>
     <array>
         <string>Default</string>
     </array>
     ```

3. **Replace the mock implementation**:
   - Import `AuthenticationServices`
   - Use `ASAuthorizationAppleIDProvider` for authentication
   - Implement the necessary delegates to handle sign-in completion
   - Store the user identifier securely

## Secure User Data Storage

In a production app, you should:

1. **Use Keychain for sensitive data** instead of UserDefaults:
   - Store authentication tokens
   - Store user credentials
   - Use a wrapper library like KeychainAccess for easier implementation

2. **Use Firebase or another backend service** for user management:
   - Store user profiles in a secure database
   - Handle authentication tokens properly
   - Implement proper session management

3. **Implement proper token handling**:
   - Store refresh tokens securely
   - Handle token expiration
   - Implement automatic token refresh

## Architecture Recommendations

For larger applications, consider:

1. **Repository pattern** for data access
2. **MVVM architecture** for clear separation of concerns
3. **Dependency injection** for better testability
4. **Combine framework** for reactive programming (already implemented)

## Security Considerations

1. **Multi-factor authentication** for additional security
2. **Rate limiting** for login attempts
3. **Biometric authentication** for easier login
4. **Password complexity requirements**
5. **Account recovery mechanisms**

## Testing Authentication

Ensure you test:

1. **Happy paths** (successful login/registration)
2. **Edge cases** (incorrect credentials, network errors)
3. **Security vulnerabilities** (SQL injection, CSRF)
4. **User experience flows** (login, logout, password reset)

This authentication system is designed to be extensible and can be easily integrated with a real backend service. 