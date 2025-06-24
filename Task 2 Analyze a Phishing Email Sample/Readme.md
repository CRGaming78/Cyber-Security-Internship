<H2>Analyze a Phishing Email</H2>

Below are some of email samples I have used to analyze phishing emails which are also saved in ` email-samples ` folder :

---

<H3>Sample 1</H3>

1.  **Sender Email Address Mismatch & Spoofing:**
    *   **Displayed From:** `Microsoft account team ,_<no-reply@access-accsecurity.com>`
        *   The `,_<` part is highly unprofessional and a red flag.
        *   The domain `access-accsecurity.com` is **not** a legitimate Microsoft domain. Microsoft uses domains like `microsoft.com`, `outlook.com`, `live.com`, etc. This is a clear attempt to look similar but is fraudulent.
    *   **Actual Sending Infrastructure (from Headers):**
        *   `smtp.mailfrom=thcultarfdes.co.uk`
        *   `Return-Path: bounce@thcultarfdes.co.uk`
        *   The IP address `89.144.44.2` is associated with `thcultarfdes.co.uk`.
        *   This domain `thcultarfdes.co.uk` is completely unrelated to Microsoft and is highly suspicious. The `.co.uk` TLD for a global Microsoft alert is also a mismatch.

2.  **Email Header Analysis (Authentication Failures):**
    *   `Authentication-Results: spf=none (sender IP is 89.144.44.2) smtp.mailfrom=thcultarfdes.co.uk; dkim=none (message not signed) header.d=none;dmarc=permerror action=none header.from=access-accsecurity.com;`
        *   **SPF=none:** The sending domain `thcultarfdes.co.uk` does not have an SPF record, or the check couldn't be performed definitively. More importantly, even if it had one, it wouldn't authorize sending for `access-accsecurity.com` (the `header.from` domain).
        *   **DKIM=none:** The message is not digitally signed. Legitimate Microsoft emails are DKIM signed.
        *   **DMARC=permerror action=none header.from=access-accsecurity.com:** There's a permanent error in the DMARC lookup for `access-accsecurity.com`, likely because the domain is fake or poorly configured for this purpose. Even if it were valid, the `none` action means the email isn't strictly rejected based on DMARC, but the SPF/DKIM failures are key.
    *   `Received-SPF: None (protection.outlook.com: thcultarfdes.co.uk does not designate permitted sender hosts)`: This explicitly states the SPF failure.
    *   `X-MS-Exchange-Organization-AuthAs: Anonymous`: The email entered the Microsoft Exchange system from an unauthenticated (anonymous) source.

<img src="/Task 2 Analyze a Phishing Email Sample/Images/Image1.png">

3.  **Suspicious Links (All `mailto:` Links to a Gmail Address):**
    *   The primary call to action, "Report The User," is a `mailto:` link:
        `href="mailto:sotrecognizd@gmail.com?&cc=sotrecognizd@gmail.com&subject=unusual signin activity&body=Report The User"`
    *   The link in the line "We detected something unusual..." also points to the same `mailto:`:
        `href="mailto:sotrecognizd@gmail.com?&cc=sotrecognizd@gmail.com&Subject=Report+The+User"`
    *   The "To opt out or change where you receive security notifications, click here" link is also a `mailto:`:
        `href="mailto:sotrecognizd@gmail.com?&cc=sotrecognizd@gmail.com&Subject=Unsubscribe+me"`
    *   **CRITICAL FLAW:** Legitimate Microsoft security actions (reporting unusual activity, managing notification preferences) would **NEVER** be handled by sending an email to a generic `@gmail.com` address (`sotrecognizd@gmail.com`). This is a dead giveaway. They would link to secure Microsoft web pages. The attacker is likely trying to get recipients to send them an email, perhaps to engage further or confirm the email address is active.

4.  **Reply-To Mismatch:**
    *   `Reply-To: sotrecognizd@gmail.com`
    *   This is the same suspicious Gmail address used in the links. If a user replies to the email, it goes to the attacker, not Microsoft or the spoofed `access-accsecurity.com` domain.

5.  **Language and Tone (Social Engineering):**
    *   **Urgency/Fear:** "Unusual sign.in activity," "We detected something unusual," "If this wasn't you, please report the user." This creates a sense of alarm to prompt immediate action.
    *   **False Authority:** Uses "Microsoft account team" and mimics the style of a legitimate Microsoft alert.
    *   **Specific but False Details:** Provides alleged sign-in details (Country/region: Russia/Moscow, IP address: 103.225.77.255, Date, Platform, Browser) to make the threat seem more credible. The IP address `103.225.77.255` is indeed often associated with Russia, which is a common tactic to evoke fear.

6.  **Tracking Pixel:**
    *   `<img alt="" src="http://thebandalisty.com/track/o43062rdzGz18708448Gdrw1821750fYo33632dSjh176" width="1px" height="1px" style="visibility:hidden">`
    *   This is a 1x1 pixel image hosted on `thebandalisty.com` (another non-Microsoft, suspicious domain). Its purpose is to track if and when the email is opened, and potentially the IP address of the recipient who opened it.

7.  **Unprofessional `From` Address Structure:**
    *   `From: Microsoft account team ,_<no-reply@access-accsecurity.com>`
    *   The inclusion of `,_<` before the email address is very unusual and not typical of professional communications.

8.  **Excessive and Irrelevant CSS Style Block:**
    *   The `<style type="text/css">...</style>` block at the end contains a massive list of random CSS class names and keywords (e.g., `tweeting pbt85voo_pm`, `d21c`, `criptomonedas`, `pokemon sendungen f5a8`). This is a common tactic called "keyword stuffing" or "word salad." Its purpose is often to try and confuse spam filters by including many seemingly legitimate (but out-of-context) terms.
---

<H3>Sample 2</H3>

1.  **Sender Email Address Mismatch & Spoofing:**
    *   **Displayed From:** `Anti-Virus Protection <pusxa@proteschip.com>`
        *   "Anti-Virus Protection" is generic.
        *   The domain `proteschip.com` is **not** a legitimate McAfee domain (McAfee uses `mcafee.com`). This is a key indicator of spoofing.
    *   **Actual Sending Infrastructure (from Headers):**
        *   `smtp.mailfrom=xunri.com`
        *   `Return-Path: pukio@xunri.com`
        *   The IP address `103.167.154.167` is associated with `mollitialdwjq.co.uk`.
        *   The `mailfrom` domain `xunri.com` and the originating server domain `mollitialdwjq.co.uk` are completely unrelated to McAfee or the displayed `proteschip.com`, and are highly suspicious.

2.  **Email Header Analysis (Authentication Failures):**
    *   `Authentication-Results: spf=none (sender IP is 103.167.154.167) smtp.mailfrom=xunri.com; dkim=none (message not signed) header.d=none;dmarc=none action=none header.from=proteschip.com;compauth=fail reason=001`
        *   **SPF=none:** The sending domain `xunri.com` either has no SPF record or the check was inconclusive. Regardless, it wouldn't authorize sending for the `header.from` domain `proteschip.com`.
        *   **DKIM=none:** The message is not digitally signed. Legitimate McAfee emails would likely be DKIM signed.
        *   **DMARC=none action=none header.from=proteschip.com:** No DMARC record was found for `proteschip.com` or the policy is `p=none`.
        *   **compauth=fail reason=001:** This is a Microsoft-specific header indicating a composite authentication failure (likely due to the SPF/DKIM issues and mismatch between `header.from` and the actual sending domain).
    *   `Received-SPF: None (protection.outlook.com: xunri.com does not designate permitted sender hosts)`: Explicitly states the SPF failure for `xunri.com`.
    *   `X-MS-Exchange-Organization-AuthAs: Anonymous`: Email entered the Microsoft Exchange system from an unauthenticated source.

<img src="/Task 2 Analyze a Phishing Email Sample/Images/Image2.png">

3.  **Suspicious Links (Using URL Shortener `rb.gy`):**
    *   All clickable elements (the main heading and both images) link to URLs using the `rb.gy` shortener:
        *   `https://rb.gy/4ydc8v`
        *   `https://rb.gy/cbzums`
    *   **CRITICAL FLAW:** Legitimate companies like McAfee would link directly to their own domains for subscription renewals or offers, not through generic URL shorteners. URL shorteners are used to obfuscate the true destination, which is a classic phishing tactic. The actual destination behind these links is likely a fake McAfee login page or a page designed to trick users into entering payment information.

4.  **Reply-To Mismatch (Different from From Address, but same suspicious domain):**
    *   `Reply-To: newsletter@proteschip.com`
    *   While the domain is the same as the displayed `From:` domain (`proteschip.com`), it's still a suspicious, non-McAfee domain. If a user replies, it goes to an address controlled by the attackers.

5.  **Subject Line & Content (Social Engineering):**
    *   **Subject:** `Re: "Your McAfee Subscription may have ENDED. 60% OFF NOW!"`
        *   The "Re:" prefix is often used to make it seem like part of an ongoing conversation, increasing the chance of it being opened.
        *   **Urgency/Fear of Loss:** "may have ENDED" creates anxiety about losing protection.
        *   **Lure/Incentive:** "60% OFF NOW!" is designed to entice users to click quickly to get a supposed deal.
    *   **Email Body:**
        *   `Mcafee Subscription may have TERMINATED. Activate with 60% OFF NOW` (Slight variation from subject, "TERMINATED" is stronger).
        *   Images used are likely mimicking legitimate McAfee branding to appear genuine.

6.  **In-Reply-To Header:**
    *   `In-Reply-To: <DM4PR19MB6317A7801126BBD236418D0EB3389@electropro.com>`
    *   This header suggests the email is a reply to a message from `electropro.com`, which is another unrelated and suspicious domain. This is likely an attempt to bypass spam filters that might be more lenient with replies.

7.  **Excessive and Irrelevant CSS Style Block (Again):**
    *   Similar to the previous sample, there's a large `<style type="text/css">...</style>` block filled with random CSS class names and keywords (e.g., `harmonia samman`, `destruction`, `cyberattacks`, `pokemon`). This is the same "keyword stuffing" / "word salad" technique to attempt to confuse spam filters.

---

<H3>Sample 3</H3>

1.  **Sender Email Address Discrepancy (Even Though Technically "Authenticated"):**
    *   **Displayed From:** `"MR. JEFFREY BEZOS" <edmondasiimwe0@gmail.com>`
    *   **CRITICAL FLAW:** Jeff Bezos, or any representative of his, would **NEVER** use a generic Gmail address like `edmondasiimwe0@gmail.com` for official communication, especially regarding a massive supposed donation. The name "Edmond Asiimwe" is completely unrelated to Jeff Bezos.
    *   **Technical Authentication (SPF/DKIM/DMARC Pass for `gmail.com`):**
        *   `Authentication-Results: spf=pass ... smtp.mailfrom=gmail.com; dkim=pass ... header.d=gmail.com;dmarc=pass ... header.from=gmail.com;compauth=pass ...`
        *   This email **passes SPF, DKIM, and DMARC checks because it was legitimately sent from a Gmail account through Google's servers.** This is a crucial point: just because an email is technically authenticated for its *sending domain* (in this case, `gmail.com`) does NOT mean the *content* or the *claimed sender identity* is legitimate. Scammers can easily create free Gmail accounts.

<img src="/Task 2 Analyze a Phishing Email Sample/Images/Image3.png">

2.  **Reply-To Address:**
    *   `Reply-To: mrjeffreyprestonbezos07@gmail.com`
    *   Another generic Gmail address. The scammer wants replies to go here to continue the fraud. The "07" in the address is also a common tactic for creating multiple similar email accounts.

3.  **Content and Subject Line (Classic Scam Tropes):**
    *   **Subject:** `YOUR $2.500,000.00`
        *   Unsolicited large sum of money – a primary red flag for advance fee fraud.
        *   The use of a comma as a thousands separator and a period for decimals (`$2.500,000.00`) is inconsistent with standard US currency notation for this amount (which would be `$2,500,000.00`).
    *   **Email Body:**
        *   "Dear E-mail Owner," – Impersonal and generic greeting.
        *   "My name is Jeff Bezos, an American, investor, and charity donor. I'm the founder, CEO and president of Amazon.com" – While true facts about Jeff Bezos, the context is absurd.
        *   "And Your email address has won you( $2.500,000.00 )" – Emails don't "win" money this way. The formatting of the amount is again slightly off.
        *   "Kindly get back to me,so I know your email address is valid.( mrjeffreyprestonbezos07@gmail.com)" – The primary goal is to get a reply to confirm the email is active and to engage the victim in the next stage of the scam. The word "Kindly" is very common in these types of scam emails.

4.  **"To: undisclosed-recipients:;"**
    *   This indicates the email was likely sent to a large list of people (BCC'd), with the actual recipients hidden. This is typical for mass-mailed spam and scams.

5.  **Lack of Professionalism:**
    *   Grammar and punctuation are slightly off (e.g., "And Your email...", inconsistent spacing around parentheses).
    *   The overall premise is inherently unbelievable for anyone familiar with how legitimate philanthropy or prize winnings work.

---
