<div align="center">

<img width="600" alt="YTSnap Logo" src="https://github.com/user-attachments/assets/9b3ffe92-cd20-48bb-8bb4-1f866325e8c9" />

<br/><br/>

# **Security Policy**

### **YTSnap is built with a privacy-first, zero-trust architecture.**  
### **No servers. No data. No risk.**

<br/>

![](https://img.shields.io/badge/CLIENT--SIDE-100%25-brightgreen?style=flat-square)
![](https://img.shields.io/badge/DATA%20STORED-none-blue?style=flat-square)
![](https://img.shields.io/badge/TRACKING-none-lightgrey?style=flat-square)
![](https://img.shields.io/badge/COOKIES-none-orange?style=flat-square)

</div>

---

<div align="center">

## **Architecture — Why It's Secure by Design**

| Property | Detail |
|:---:|:---:|
| 🖥️ **Processing** | 100% client-side JavaScript — no backend ever touches your data |
| 🗄️ **Database** | None — no links, IDs, or user data are stored anywhere |
| 📡 **Telemetry** | None — no analytics, no event tracking, no logging |
| 🍪 **Cookies** | None set on the generator page |
| 🔗 **Link Wrapping** | None — no server-side redirects, UTM/affiliate params preserved end-to-end |
| 🚫 **Ad Interstitials** | None — deep link fires directly, no intermediate pages |

**Your data never leaves your browser. There is nothing to breach.**

</div>

---

<div align="center">

## **Supported Versions**

| Version | Status |
|:---:|:---:|
| **v1** (current) | ✅ Actively supported |
| Older builds | ❌ Not supported |

**Always use the latest version at [yt-snap.netlify.app](https://yt-snap.netlify.app/)**

</div>

---

<div align="center">

## **Scope**

**In scope for vulnerability reports:**

| Area | Examples |
|:---:|:---|
| 🔴 **Client-side injection** | XSS via URL input parsing |
| 🔴 **Malicious redirects** | URI scheme manipulation leading to unintended destinations |
| 🔴 **Data leakage** | Any unintended network request carrying user-supplied data |
| 🔴 **Supply chain** | Compromised third-party scripts or CDN assets |

<br/>

**Out of scope:**

| | |
|:---:|:---|
| ⚪ | Vulnerabilities in third-party platforms (Netlify, GitHub) |
| ⚪ | Issues requiring physical device access |
| ⚪ | Self-inflicted issues from modified/forked deployments |
| ⚪ | Theoretical risks with no practical exploit path |

</div>

---

<div align="center">

## **Reporting a Vulnerability**

**Do not open a public GitHub issue for security vulnerabilities.**

<br/>

**① Identify** the vulnerability and document steps to reproduce it

**② Email** the maintainer privately via GitHub: **[sr-857](https://github.com/sr-857)**

**③ Include** — affected URL · browser/device · reproduction steps · potential impact

**④ Allow** reasonable time for review and response before any public disclosure

<br/>

> We follow **responsible disclosure**. Reports handled in good faith will receive a response.  
> Critical issues will be patched and credited (unless you prefer anonymity).

</div>

---

<div align="center">

## **What We Promise**

| ✅ Acknowledge your report promptly |
|:---:|
| ✅ Investigate and patch confirmed vulnerabilities |
| ✅ Credit researchers who report responsibly |
| ✅ Never pursue legal action against good-faith reporters |

</div>

---

<div align="center">

## **Security Notes for Fork Deployers**

If you fork and self-host YTSnap, ensure:

```
✔  No third-party analytics scripts are introduced
✔  No server-side components are added without a security review
✔  Netlify headers include Content-Security-Policy
✔  All dependencies (if any are added) are pinned and audited
```

</div>

---

<div align="center">

---

### **Built to be boring from a security perspective — and that's the point.**

**[yt-snap.netlify.app](https://yt-snap.netlify.app/)** &nbsp;·&nbsp; **[GitHub](https://github.com/sr-857/YTSNAP)**

<br/>

</div>
