# Task 7: Identify and Remove Suspicious Browser Extensions
---


## 1. Objective

The objective of this task was to learn how to identify, analyze, and remove potentially harmful or unnecessary browser extensions to enhance browser security and performance. This involved auditing installed extensions, reviewing their permissions, and documenting the findings.

## 2. Tools Used

-   **Web Browser:** `Brave`
-   **Method:** Manual review of the browser's extension manager.

## 3. Process: Browser Extension Audit

I followed a systematic process to audit the extensions installed on my browser.

1.  **Accessed Extension Manager:** Opened the `brave://extensions` page to list all installed extensions.
2.  **Initial Review:** Went through the list to identify extensions by name and purpose.
3.  **Detailed Inspection:** For each extension, I clicked "Details" to review its specific permissions and checked its ratings and recent reviews on the Chrome Web Store.
4.  **Identification:** I flagged extensions that were either no longer in use or had overly broad permissions for their function.
5.  **Removal:** I removed the identified extensions to reduce the browser's attack surface.
6.  **Restart:** Finally, I restarted the browser to ensure a clean state.

### Screenshot 1: Extensions List Before Cleanup
<img src="/Task 7 Identify and Remove Suspicious Browser Extensions/Images/Image1.png">

### Findings and Actions Taken

| Extension Name | Developer | Reason for Removal | Suspicious Permissions Noted (if any) |
| :------------- | :-------- | :----------------- | :------------------------------------ |
| Microsoft Power Automate | Microsoft | No use |  all your data on all websites |


### Screenshot 2: Extensions List After Cleanup
<img src="/Task 7 Identify and Remove Suspicious Browser Extensions/Images/Image2.png">

## 4. How Malicious Extensions Harm Users

Malicious browser extensions are a significant threat because they operate with high levels of privilege within the browser. They can cause harm by:
-   **Data Theft:** Stealing sensitive information like passwords, credit card details, and personal data by logging keystrokes or reading web page content.
-   **Adware:** Injecting unwanted advertisements and pop-ups onto web pages, which can degrade the user experience and lead to further malware.
-   **Session Hijacking:** Stealing session cookies to gain unauthorized access to user accounts on websites.
-   **Cryptojacking:** Secretly using the user's CPU power to mine for cryptocurrencies, causing performance degradation and higher electricity usage.
-   **Redirection:** Forcibly redirecting users to phishing sites or malicious domains to trick them into revealing information or downloading malware.

---