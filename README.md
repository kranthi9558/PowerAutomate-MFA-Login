# 🔐 Automated MFA Login using Power Automate Desktop and Python

This guide shows how to fully automate login to a portal protected by MFA (6-digit Time-based One-Time Password) using **Power Automate Desktop (PAD)** and **Python**.

Many automation tools struggle with MFA, but with this method, you can bypass manual steps using a secure, real-time TOTP generator.

---

## 🚀 What This Automation Does

* Opens the login portal in Microsoft Edge
* Enters username and password
* Runs a Python script to generate a 6-digit MFA code
* Inputs the MFA code automatically
* Logs in — no human in the loop!

---

## 📦 Prerequisites

* [Power Automate Desktop](https://flow.microsoft.com/en-us/desktop/)
* [Python 3.x](https://www.python.org/downloads/)
* Python library: `pyotp`

  ```bash
  pip install pyotp
  ```
* Your **MFA shared secret key** (base32 format)


## 🐍 Python Script — `GenerateMFA.py`

```python
import pyotp

# Replace with your base32 secret key
secret_key = "JBSWY3DPEHPK3PXP"

# Generate the 6-digit TOTP code
totp = pyotp.TOTP(secret_key)
code = totp.now()

# Output the code for PAD to capture
print(code)
```

✅ Save this as `GenerateMFA.py` in a known location, e.g., `C:\Automation\MFA\GenerateMFA.py`

---

## 🧰 Power Automate Desktop Flow Overview

### 🔹 Actions Summary:

1. **Set Variables**

   * `totpScriptPath = "C:\\Automation\\MFA\\GenerateMFA.py"`
2. **Launch Edge** and open login URL
3. **Populate Username and Password** fields
4. **Click Next**
5. **Run DOS Command**

   ```plaintext
   python %totpScriptPath%
   ```

   * Output to: `MfaCode`
6. **(Optional)** Display message box with `%MfaCode%` for debug
7. **Populate MFA field** with `%MfaCode%`
8. **Click Final Login button**

---

## 🖼️ Screenshots

### 🔸 Flow Overview

![Flow Overview](images/flow-overview.png)

### 🔸 Run DOS Command Step

![Run DOS Command](images/pad-dos-command.png)

---

## ✅ End Result

With this setup:

* You no longer need to manually enter MFA codes
* Everything from login to secure OTP handling is fully automated
* Great for internal tools, RPA flows, and headless bots

---

## 🗨️ Questions or Feedback?

Feel free to raise an issue or connect with me on [LinkedIn]([https://www.linkedin.com/in/YOUR_PROFILE_LINK](https://www.linkedin.com/in/devarapallykranthikumar/)).
