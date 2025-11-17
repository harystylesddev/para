Good question. Can you clarify which “Capsule” you’re talking about:

1. **CapsuleCRM** — the customer-relationship management tool (capsulecrm.com)
2. **Capsule SDK / Wallet / MPC** — the embedded wallet / smart-account system provided by usecapsule.com

Because “no-reply@usecapsule” makes me think you mean **Capsule SDK / Wallet**, not CapsuleCRM. If that’s correct, here’s how it works (and what docs are available):

---

## 🔍 Capsule (SDK / Wallet) — How Email Verification Works

* Capsule is primarily a *wallet / signer* SDK: it uses **email (or social login)** as a way for users to authenticate and create a secure embedded MPC wallet. ([docs.zerodev.app][1])
* The official Web SDK is **@usecapsule/web-sdk**, and its full API-level documentation is available. ([capsule-org.github.io][2])
* For mobile (React Native), there’s a separate SDK: `@usecapsule/react-native-sdk`. ([capsule-org.github.io][3])
* When a user signs up or logs in via email, Capsule sends them a verification / OTP to the email address. That’s how it “verifies” them. ([Dart packages][4])
* In Flutter (using Para / Capsule integration), for example, after you call the “initiateAuthFlow” with email, you move to a “verify” stage where a code is sent to their email. ([Dart packages][4])

---

## 📚 Documentation / Developer Resources

* **Capsule Web SDK docs**: function-level docs are auto-generated via TypeDoc. ([capsule-org.github.io][2])
* **Biconomy + Capsule tutorial**: shows how to use Capsule signer with Biconomy’s account abstraction setup. ([docs-devx.biconomy.io][5])
* **Least Authority audit report**: contains some architectural overview of Capsule’s signing / MPC system. ([Least Authority][6])
* **Para + Capsule (Flutter)**: the Para SDK guide shows email auth + verification flow. ([Dart packages][4])

---

## ⚠️ Important Notes

* There is **no “send arbitrary transactional emails”** API in Capsule SDK itself. Capsule is not an email-sending service or transactional email provider. Its “email” functionality is limited to **authentication / login verification** (OTP) via email.
* If you want to send verification or welcome emails (beyond login OTPs), you’ll need to integrate with a proper transactional email service (like SendGrid, Mailgun, SES etc).
* “[no-reply@usecapsule.com](mailto:no-reply@usecapsule.com)” sounds like a system email address used by Capsule to send their auth / verification emails — you as an app developer don’t “send from” that address via an API. That’s controlled by Capsule.

---

If instead you *are* talking about **CapsuleCRM**, then what you’re asking (“use no-reply@usecapsule to send email for verification, etc”) doesn’t align with how CapsuleCRM works — their API is CRM-focused, not for user-auth flows. Their developer API is more about interacting with CRM data. ([developer.capsulecrm.com][7])

---

If you like, I can dig into the **latest (2025) Capsule SDK docs** (web + mobile) and share exactly how to implement email-based login + verification in your app — do you want me to do that?

[1]: https://docs.zerodev.app/sdk/v5_3_x/signers/capsule?utm_source=chatgpt.com "Use Capsule with ZeroDev"
[2]: https://capsule-org.github.io/web-sdk/?utm_source=chatgpt.com "@usecapsule/web-sdk - GitHub Pages"
[3]: https://capsule-org.github.io/react-native-sdk/?utm_source=chatgpt.com "@usecapsule/react-native-wallet - GitHub Pages"
[4]: https://pub.dev/packages/para/versions/2.1.2-alpha.1?utm_source=chatgpt.com "para 2.1.2-alpha.1 | Flutter package"
[5]: https://docs-devx.biconomy.io/tutorials/signers/capsule?utm_source=chatgpt.com "How to use a Capsule signer with Biconomy"
[6]: https://leastauthority.com/wp-content/uploads/2024/02/Capsule_Signing_and_Permissioning_Toolkit_Updated_2.pdf?utm_source=chatgpt.com "Capsule"
[7]: https://developer.capsulecrm.com/?utm_source=chatgpt.com "Capsule API - Capsule API"






---
---

Good question. **Yes**, Capsule and Para are very closely related — in fact, Capsule *became* Para. Here’s how they map to each other:

---

## 🔍 How Capsule and Para Relate

1. **Rebranding / Migration**

   * According to Para’s docs: *“Capsule is now Para!”*. ([docs.getpara.com][1])
   * There’s a full migration guide from Capsule → Para. ([docs.getpara.com][2])
   * The package namespaces changed: e.g., `@usecapsule/react-sdk` → `@getpara/react-sdk`. ([docs.getpara.com][2])
   * On mobile, e.g. Flutter: the `capsule` package was replaced by `para` on pub.dev. ([docs.getpara.com][2])

2. **Same Core Functionality / Architecture**

   * Para’s wallet architecture uses **multi-party computation (MPC)** and passkeys, which aligns with Capsule’s design. ([Para Blog][3])
   * Para supports *universal embedded wallets*: users can log in once (e.g. via email) and use the same wallet across multiple apps. ([docs.getpara.com][4])
   * Para’s security design ensures the full private key is never reconstructed in one place. ([Para Blog][3])

3. **APIs / SDK Changes**

   * Method signatures are updated in the Para SDK: for example, where Capsule used positional arguments, Para now uses objects. ([docs.getpara.com][2])
   * New React hooks in Para: e.g. `useCreateUser`, `useInitiateLogin`, etc. ([docs.getpara.com][2])
   * Session management, signing, transaction flows, etc., are handled similarly but with updated APIs. ([docs.getpara.com][5])

---

### ✅ So, to answer your question directly:

**Yes**, “this” (Capsule) is basically the same as Para — Para is the evolution / rebranded version of Capsule. If you’re building now, you should use the **Para SDK and docs**.

---

If you like, I can send **working code examples** (web + mobile) for how to do email login + verification + wallet creation using Para — do you want me to share that?

[1]: https://docs.getpara.com/v1/introduction/welcome?utm_source=chatgpt.com "Welcome - Para Docs"
[2]: https://docs.getpara.com/v2/general/migration-from-capsule?utm_source=chatgpt.com "Migrating from Capsule to Para - Para Docs"
[3]: https://blog.getpara.com/non-custodial-embedded-wallets/?utm_source=chatgpt.com "How Para Works: Non-Custodial, Secure Wallet SDK"
[4]: https://docs.getpara.com/concepts/portability?utm_source=chatgpt.com "Universal Embedded Wallets - Para Docs"
[5]: https://docs.getpara.com/v2/concepts/technical-faq?utm_source=chatgpt.com "Technical FAQ - Para Docs"
