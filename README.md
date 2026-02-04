# gtm-test-site
Testmiljö för implementering av GTM och spårning. Del av kursen i Webbanalys./ Test site for GTM and GA4 implementation exercises.

# 🏷️ My GTM Project

Here is how my tracking works (Legal & GDPR Safe):

```mermaid
graph TD
    User(Visit Site) --> Consent{Accept Cookies?}
    Consent -- YES --> GTM[🚀 GTM Fires Tags]
    Consent -- NO --> Block[🛑 No Data Sent]
    GTM --> GA4(Google Analytics)
