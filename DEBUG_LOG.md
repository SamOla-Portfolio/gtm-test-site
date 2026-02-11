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

