# Secure Coding Practices

Platform-specific secure coding guidelines for iOS (Swift) and Android (Kotlin) mobile application development.

---

## Secure Data Storage

### iOS Keychain

Use the iOS Keychain for storing credentials, tokens, and sensitive configuration:

```swift
import Security

func saveToKeychain(key: String, data: Data) -> Bool {
    let query: [String: Any] = [
        kSecClass as String: kSecClassGenericPassword,
        kSecAttrAccount as String: key,
        kSecValueData as String: data,
        kSecAttrAccessible as String: kSecAttrAccessibleWhenUnlockedThisDeviceOnly
    ]
    SecItemDelete(query as CFDictionary)  // Remove existing
    let status = SecItemAdd(query as CFDictionary, nil)
    return status == errSecSuccess
}
```

Key accessibility levels:
- `kSecAttrAccessibleWhenUnlockedThisDeviceOnly`: Most secure — available only when device is unlocked, not included in backups
- `kSecAttrAccessibleAfterFirstUnlockThisDeviceOnly`: Available after first unlock — suitable for background operations
- Never use `kSecAttrAccessibleAlways` — data accessible even when device is locked

### Android EncryptedSharedPreferences

```kotlin
import androidx.security.crypto.EncryptedSharedPreferences
import androidx.security.crypto.MasterKey

val masterKey = MasterKey.Builder(context)
    .setKeyScheme(MasterKey.KeyScheme.AES256_GCM)
    .build()

val prefs = EncryptedSharedPreferences.create(
    context, "secure_prefs", masterKey,
    EncryptedSharedPreferences.PrefKeyEncryptionScheme.AES256_SIV,
    EncryptedSharedPreferences.PrefValueEncryptionScheme.AES256_GCM
)

prefs.edit().putString("auth_token", token).apply()
```

## Network Security

### Certificate Pinning — iOS

```swift
class PinningDelegate: NSObject, URLSessionDelegate {
    let pinnedCertHash = "sha256/AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA="

    func urlSession(_ session: URLSession, didReceive challenge: URLAuthenticationChallenge,
                    completionHandler: @escaping (URLSession.AuthChallengeDisposition, URLCredential?) -> Void) {
        guard let serverTrust = challenge.protectionSpace.serverTrust,
              let certificate = SecTrustGetCertificateAtIndex(serverTrust, 0) else {
            completionHandler(.cancelAuthenticationChallenge, nil)
            return
        }
        let serverCertData = SecCertificateCopyData(certificate) as Data
        let serverHash = sha256Hash(serverCertData)
        if serverHash == pinnedCertHash {
            completionHandler(.useCredential, URLCredential(trust: serverTrust))
        } else {
            completionHandler(.cancelAuthenticationChallenge, nil)
        }
    }
}
```

### Android Network Security Config

```xml
<!-- res/xml/network_security_config.xml -->
<network-security-config>
    <domain-config cleartextTrafficPermitted="false">
        <domain includeSubdomains="true">api.example.com</domain>
        <pin-set expiration="2025-01-01">
            <pin digest="SHA-256">base64EncodedPin=</pin>
            <pin digest="SHA-256">backupBase64Pin=</pin>
        </pin-set>
    </domain-config>
</network-security-config>
```

## Input Validation

### Parameterized Queries

```kotlin
// CORRECT - Parameterized
val cursor = db.rawQuery(
    "SELECT * FROM users WHERE email = ? AND status = ?",
    arrayOf(userEmail, "active")
)

// WRONG - String concatenation (SQL injection risk)
// val cursor = db.rawQuery("SELECT * FROM users WHERE email = '$userEmail'", null)
```

### WebView Security

```swift
// iOS - Disable JavaScript if not needed
let config = WKWebViewConfiguration()
config.preferences.javaScriptEnabled = false

// If JavaScript is required, sanitize any data injected into the WebView
let sanitized = userInput.replacingOccurrences(of: "<", with: "&lt;")
```

## Authentication Best Practices

- Use OAuth 2.0 with PKCE flow for mobile (never implicit grant)
- Store tokens in secure storage (Keychain / EncryptedSharedPreferences)
- Implement token refresh with short-lived access tokens (15 min) and longer refresh tokens (7-30 days)
- Require biometric confirmation for sensitive operations (payment, password change)
- Clear all tokens and cached data on logout

## Logging and Debugging

| Practice | Development | Production |
|----------|------------|-----------|
| Verbose logging | Enabled | Disabled |
| Network request logging | Enabled | Disabled |
| Sensitive data in logs | Never | Never |
| Debug flags | Enabled | Stripped |
| Crash reports | Full stack trace | Symbolicated, no PII |

Never log tokens, passwords, PII, or API keys in any environment. Use log redaction for fields that might accidentally contain sensitive data.
