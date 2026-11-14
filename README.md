# Pre-Payment Scam Firewall

**VH-S02: Detecting digital payment scams before money is sent.**

Built at VECTOR HACKS '26 (Software Track, VH-S02).

A browser-based tool that checks suspicious calls, messages and payment requests *before* you pay. It scores the risk, explains why in plain language, and if the risk is critical it pushes the user toward the India Cyber Crime Helpline (**1930**) and helps them file a complaint.

> Most scam tools react after money is lost. This one tries to interrupt the scam in the moment, when the victim is under pressure.

## What it does

- **Log what is happening:** paste a WhatsApp/SMS message, record an incoming call, and add a payment or QR request (UPI link or recipient, amount).
- **Risk score from 0 to 100** with four levels: no warning signs, medium, high, critical.
- **Explains the "why":** lists each warning sign found, such as urgency pressure, authority impersonation, threats, secrecy, KYC/account-block claims, OTP/PIN requests, and refund or investment bait.
- **Contradiction detection:** flags claims that don't add up, for example "a refund" that requires you to scan a QR code, or "police" asking for a payment.
- **Scam chain view:** shows which stage of a typical scam you are at (contact, pressure, request, payment) and the stop point where you can still back out.
- **Scam pattern matching:** recognises patterns like digital arrest, QR receive-money, investment, task/job and KYC scams.
- **Critical mode:** at a high score a full-screen warning appears with a countdown and a one-tap call to **1930**. Cancel stays locked while the suspicious caller is still calling.
- **Complaint helper:** a form that generates a downloadable cyber crime complaint letter (DD/MM/YYYY dates, points to cybercrime.gov.in and 1930), with a reminder never to include OTPs, PINs or passwords. The complainant's own name and number are left for the user to fill in.
- **Five languages:** English, Hindi, Tamil, Telugu, Malayalam.
- **Demo scenarios** to try the flow without real data.

## How it works

A single-file web app (HTML, CSS, vanilla JavaScript) with no backend and no external API calls. Everything runs in the browser.

1. Each message, call and payment becomes an *evidence* item.
2. Messages are matched against a lexicon of scam signals (regex patterns with weights). Repeated calls, unknown contacts and large or QR-based payments add weight. Saved contacts add nothing.
3. Signals are combined as independent probabilities: `risk = 1 − Π(1 − wᵢ)`. Certain combinations (secrecy plus a payment request, or credential requests) set a higher minimum score.
4. The score decides the level, the explanation, the contradiction checks and whether critical mode opens.

## Run it locally

No build step. Download `index.html` and open it in a browser.

## Limitations (honest)

- Detection is **rule-based**, not machine learning. It can miss new scam wording or flag harmless messages.
- It gives a **risk assessment, not a legal finding**, and says so in the app.
- Currently tuned for scam patterns common in **India** (UPI, KYC, digital arrest, 1930 helpline).
- Message text is typed or pasted by the user. It doesn't read live calls or SMS.

## Roadmap

- Add an ML or LLM classifier alongside the rules and compare accuracy.
- Test against a labelled set of real scam messages and report precision/recall.
- Browser extension or mobile app that checks UPI links before payment.
- Split the single file into modules and add tests.

## Team
Anns Meljin ( Leader) 
Anusha
Aaditeya

## Disclaimer

Educational hackathon project. It is not a substitute for official advice. If you are being scammed, call **1930** or visit the National Cyber Crime Reporting Portal.
