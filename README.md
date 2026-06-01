# Task 2 — Phishing Email Analysis
Cybersecurity Internship | ElevateLabs

---

## What This Task Was About

For this task I had to find a real phishing email, go through it carefully, and figure out what makes it a phishing attempt. I got the sample from a public GitHub repository called phishing_pot which has a collection of real phishing emails that people have reported over the years.

The email I picked turned out to be a classic scam — someone pretending to be Warren Buffett and promising $5 million USD. Sounds obvious when you say it like that, but the email is actually quite carefully written to manipulate people emotionally, which is what made it interesting to analyze.

---

## Files in This Repo

- `README.md` — this report
- `phishing_sample.eml` — the actual phishing email I analyzed

---

## The Email — Quick Summary

The email claimed to be from Warren Buffett saying he wants to donate $5,000,000 to me as part of a charity project. His wife supposedly died of cancer and he is also sick in hospital. All I had to do was send my name, address and phone number.

Obviously fake. But let me break down exactly why.

**Basic header info:**

| Field | Value |
|---|---|
| From (display name) | Mr.Warren Buffett Billionaire investor |
| From (actual email) | test@central.mercfresh.com |
| Reply-To | mrwarrenb55@gmail.com |
| Subject | 52Greetings to You my good friend |
| Date | 2 Aug 2023 |
| Sending IP | 117.121.214.50 |

---

## What I Found — Phishing Indicators

### 1. The sender email is completely wrong

The email says it's from Warren Buffett but the actual sending address is test@central.mercfresh.com. That's a food company website. Nothing to do with Warren Buffett or Berkshire Hathaway at all.

Also the username is literally "test" which is not something a real person or organisation uses for official communication.

The Reply-To is a random Gmail account mrwarrenb55@gmail.com — so if you reply, it goes to a completely different place than where the email came from. That's intentional — the attacker separates the fake sending address from where victim replies land.

### 2. All email authentication checks failed

I looked at the authentication results in the email headers:

    spf=none
    dkim=none (message not signed)
    dmarc=none
    compauth=fail reason=001

SPF, DKIM and DMARC are basically the email equivalent of an ID check. All three said none or failed. Any real organisation sending legitimate email would pass these. This one failed all of them.

### 3. Microsoft already flagged it as spam

The headers also showed:

    X-Microsoft-Antispam: BCL:9
    X-MS-Exchange-Organization-SCL: 5

BCL 9 is the maximum bulk complaint score — meaning this sender has been reported for spam many times before. The email went straight to Junk folder automatically.

### 4. The proof link is a 10 year old news article

The email includes a link to a real LA Times article as supposed proof that Warren Buffett is genuine. But the article is from July 2013 — over 10 years before this email was sent. And it has nothing to do with any donation offer. It's just a real link used to look credible.

### 5. Emotional manipulation

This is actually the most interesting part. The email is full of techniques to make you feel emotional before you think logically:

- Dying wife with cancer — sympathy
- "I'm writing from a hospital computer" — more sympathy and urgency
- "I don't know when I will die" — makes you feel like you need to act fast
- "Millions of people want this but only you were chosen" — makes you feel special
- "Our information is 100% legitimate" — tries to answer your suspicion before you even ask
- Ends with "God bless you" — trying to seem trustworthy

Each one of these is designed to make you emotionally invested before you stop to question anything.

### 6. It is asking for personal information

Near the end it asks for:

- Full name
- Home address
- Phone number

Once you send this, the next step is they ask for a small processing fee to release your $5 million. That fee is what they are actually after. The $5 million does not exist.

### 7. Grammar and spelling mistakes

A few things I noticed:

- Amount written as $5,000,000,00 — wrong punctuation used twice
- Subject line starts with "52Greetings" — random number at the start
- Phrases like "meet you well" and "to be entangled" do not make sense in English
- Email sent to "Undisclosed recipients" — it is a mass email, not personal at all

### 8. Sent using a 20 year old mail client

    X-Mailer: Microsoft Outlook Express 6.00.2600.0000

Outlook Express 6 came out in 2001 and Microsoft stopped supporting it in 2009. No real business in 2023 is using software that old. This is common in phishing kits.

---

## Summary Table

| # | What I Found | Risk |
|---|---|---|
| 1 | Sender spoofed — not actually Warren Buffett | HIGH |
| 2 | Reply-To is a different Gmail account | HIGH |
| 3 | SPF, DKIM, DMARC all failed | HIGH |
| 4 | Spam score BCL:9 — maximum rating | HIGH |
| 5 | Promises $5 million to a stranger | HIGH |
| 6 | Asks for personal name, address, phone | HIGH |
| 7 | Emotional manipulation throughout | MEDIUM |
| 8 | Urgency and FOMO tactics | MEDIUM |
| 9 | Fake proof using old news article | MEDIUM |
| 10 | Grammar and spelling errors | LOW |
| 11 | 20 year old mail client | LOW |
| 12 | Sent to mass recipients, not personal | MEDIUM |

---

## Tools I Used

- **phishing_pot GitHub repo** — to get the phishing email sample
- **PhishTank** — to understand and verify phishing patterns
- **MXToolbox** — to check SPF/DKIM/DMARC records
- **Manual header reading** — went through the raw email headers line by line

---

## What Should You Do If You Get This Email

- Don't reply — replying tells them your email is active
- Don't click any links
- Don't send any personal information
- Mark it as spam
- Report it on PhishTank if you want to help others

---

## What I Learned

Before this task I knew phishing emails existed but I didn't really know what to look for technically. Going through the headers and finding the SPF/DKIM/DMARC failures was new for me — I didn't know emails had that kind of authentication built in. The social engineering part was also eye-opening, seeing exactly how deliberately each emotional manipulation technique is placed in the email.

---

*ElevateLabs Cybersecurity Internship | Task 2 | June 2026*
