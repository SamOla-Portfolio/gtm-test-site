# Debug Diary (Felsökningslogg)
## Den här loggen dokumenterar min testprocess, validering av taggar i GTM och datakvalitetskontroller för Case Study.

| Datum | Vad jag testade (Test Case) | Förväntat Resultat | Resultat i DebugView | Status | Noteringar |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 2026-02-11 | **GTM Connection** | Tag Assistant visar "Connected" | Connected ✅ | ✅ OK | Container ID: GTM-XXXX |
| 2026-02-11 | **CTA Button Click** | Eventet `begin_checkout` ska fyras | Event fired korrekt | ✅ OK | Parameter `value` saknades först (fixat) |
| 2026-02-12 | **Consent Mode (Denied)** | Inga cookies, bara "pings" | *Väntar på test* | 🟡 Todo | Måste kolla "Application"-fliken i Chrome |

## 🛠 Felsökningslogg (Debug Log) - 2026-02-11

### 1. Installation av GTM Container
- **Problem:** GTM Tag Assistant kunde inte hitta containern på den vanliga URL:en.
- **Analys:** GitHub Pages tog tid att bygga (Deployment lag), och webbläsaren visade en cachad version av sidan utan scriptet.
- **Åtgärd (Action):** Använde en URL-parameter (`?v=new`) för att tvinga webbläsaren att hämta den senaste versionen. Verifierade källkoden (Source Code) att GTM-ID fanns på plats.
- **Resultat:** ✅ Connected.

# Debug Log - GTM Implementation

## [2026-02-13] Session 1: GA4 Connection & Event Tracking Setup

### 🎯 Objectives
1. Connect Google Tag Manager (GTM) to Google Analytics 4 (GA4).
2. Track user interactions: Purchase clicks, Outbound links, and Broken links.
3. Validate data flow using GA4 DebugView.

### 🛠️ Implementation Details

#### 1. GA4 Configuration
- **Status:** Connected ✅
- **Measurement ID:** `G-1NB1FYD904`
- **Method:** Created a GA4 Configuration Tag (via Google Tag).

#### 2. Event: Purchase Button (`click_purchase_test`)
- **Trigger:** Click - All Elements
- **Condition:** `Click Text` contains "Köp Nu".
- **Result:** Tag fires correctly on button click. Data visible in GA4.

#### 3. Event: Outbound Link (`click_outbound`)
- **Trigger:** Click - Just Links
- **Condition:** `Click URL` contains "google".
- **Parameter Added:** `destination: google`.
- **Result:** Tag captures exit clicks successfully.

#### 4. Event: Broken Link (`click_broken_link`)
- **Trigger:** Click - Just Links
- **Condition:** `Click Text` contains "404".
- **Result:** Successfully tracking clicks to the 404 error page.
---
### 🐛 Bugs & Challenges Encountered

#### Issue: Race Condition on 404 Link
- **Problem:** When clicking the "Testa 404-fel" link, the browser navigated to the error page too quickly. The GTM tag fired but was cancelled before sending data to GA4.
- **Diagnosis:** The browser unloaded the current page (where GTM lives) before the network request completed.
- **Solution:** 1. Modified the Trigger settings.
  2. Enabled **"Wait for Tags"** (set to 2000 milliseconds).
  3. Applied this wait only on pages where `Page URL` contains "gtm-test-site".
- **Verification:** Tested using `Ctrl + Click` (Open in new tab) to keep the GTM session alive. The tag `GA4 Event - Broken Link` appeared successfully in DebugView.

### ✅ Final Status
All tags are configured, fired, and verified in GA4. Ready for next phase.
