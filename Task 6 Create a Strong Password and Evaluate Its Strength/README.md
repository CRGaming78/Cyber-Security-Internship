# Task 6: Strong Password Creation and Evaluation
---

## 1. Objective

The objective of this task is to understand the core principles of what constitutes a strong password. This was achieved by creating a variety of passwords with different complexities, testing them using an online password strength checker, and analyzing the results. The goal is to identify and document best practices for password security.

---

## 2. Tools Used

*   **Password Strength Checker:** [passwordmeter.com](https://www.passwordmonster.com/) was used to evaluate the strength of each created password and receive feedback on its composition.

---

## 3. Password Creation and Strength Analysis

Multiple passwords were created to demonstrate a range from very weak to very strong. Each was tested, and the results are documented below.

| Password Tested                  | Complexity Analysis                                       | Strength Score/Feedback (from passwordmeter.com) | Estimated Time to Crack (General Estimate) |
| -------------------------------- | --------------------------------------------------------- | ------------------------------------------------ | ------------------------------------------ |
| `password`                       | 8 chars, all lowercase, common dictionary word.           | **Very Weak**. Deductions for being too common. | Instantly                                  |
| `Qwerty_123`                      | 9 chars, lowercase, numbers. Follows a keyboard pattern.  | **Very Weak**. Deductions for sequence & patterns. | A few seconds                              |
| `MyHomeWork123`                  | 13 chars, upper, lower, numbers. Predictable structure.   | **Weak**. Lacks symbols, still predictable. | Few Minutes (15min)                      |
| `Tr0ub4dor&3`                    | 11 chars, upper, lower, numbers, symbols. Uses leetspeak. | **Very Strong**. Good mix of all character types. | Few Years(46 years)                         |
| `Correct=Horse=Battery=Staple!`  | 32 chars, upper, lower, symbols. A long passphrase.       | **100% (Very Strong)**. Length is the key factor. | 3 billion years                         |
| `MyCatSitsOnTheMat#EveryDay24`   | 28 chars, upper, lower, numbers, symbols. Memorable.      | **100% (Very Strong)**. Excellent length and complexity. | 3 trillion years                         |

---

## 4. Key Learnings & Best Practices

Based on the evaluation, the following best practices for creating strong passwords were identified:

1.  **Length is King:** Password length is the single most important factor in its strength. A longer password exponentially increases the number of possible combinations, making brute-force attacks infeasible. Aim for **12-15 characters minimum**.
2.  **Complexity is Queen:** Use a mix of all four character types:
    *   Uppercase letters (A-Z)
    *   Lowercase letters (a-z)
    *   Numbers (0-9)
    *   Symbols (!, @, #, $, %, etc.)
3.  **Avoid Predictability:** Do not use personal information (names, birthdays), common dictionary words, or simple patterns (e.g., `qwerty`, `123456`).
4.  **Embrace Passphrases:** A passphrase (a sequence of words) is often more secure and easier to remember than a complex, short password. The `Correct-Horse-Battery-Staple` example is a classic illustration of this.
5.  **Uniqueness is Essential:** Never reuse passwords across different websites or services. If one site is breached, all your accounts using that password become vulnerable.
6.  **Use a Password Manager:** It's impossible for a human to remember dozens of unique, complex passwords. A password manager can generate, store, and auto-fill them securely.

---

## 5. Research on Common Password Attacks

Password complexity directly defends against common attack vectors:

*   **Brute-Force Attack:** This is a trial-and-error method where an attacker's software attempts every possible combination of letters, numbers, and symbols until it finds the correct password.
    *   **How Complexity Defends:** Every character added to a password *exponentially* increases the total number of combinations. A long, complex password makes a brute-force attack take an impractical amount of time (from seconds to thousands of years).

*   **Dictionary Attack:** This is a more targeted version of a brute-force attack. Instead of trying random combinations, the attacker uses a list of common words, phrases, and previously leaked passwords (a "dictionary").
    *   **How Complexity Defends:** Using non-dictionary words, misspelled words, or passphrases ensures the password won't be found in an attacker's list. Mixing in numbers and symbols also helps defeat this.

---
