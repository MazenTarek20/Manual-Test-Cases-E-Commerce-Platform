# 🧪 Manual Test Cases — E-Commerce Platform

A structured manual test case suite. Covers three user stories from an e-commerce platform:
**Credit Card Account Opening**,
**Contact Us Form**,
and **WhatsApp Business Plugin** — with full functional, boundary, negative, and business logic test coverage.

---

## 📁 Repository Structure

```
Test-Cases/
│
├── Open a credit card account – Test Cases.pdf   # Discount logic & account creation tests
├── Contact us – Test Cases.pdf                   # Form validation & email format tests
└── WhatsApp Plugin – Test Cases.pdf              # Plugin installation & messaging tests
```

---

## 📋 User Stories & Test Coverage

### 1. 💳 Open a Credit Card Account

**User Story:** As a customer, I want to open a credit card account.

**Acceptance Criteria:**
- New customers receive a **15% discount** on all purchases today
- Existing customers with a **loyalty card** receive a **10% discount**
- A **coupon** gives **20% off** (cannot be combined with the new customer discount)
- Applicable discounts are **added together**

**Test Scenarios Covered:**

| Category | Example Scenarios |
|---|---|
| ✅ Functional | New customer opens account and receives 15% discount |
| ✅ Functional | Existing customer with loyalty card receives 10% discount |
| ✅ Functional | Existing customer with loyalty card + coupon receives 30% (10% + 20%) |
| ❌ Negative | New customer attempts to combine 15% with coupon — should be rejected |
| 🔲 Boundary | Customer with both new-customer status and coupon — only coupon applies |
| 🔲 Boundary | No discount conditions met — 0% applied |
| 🔲 Business Logic | Verify discount stacking is additive, not multiplicative |

---

### 2. 📧 Contact Us Form

**User Story:** As a customer, I want to contact the website about a problem with my product.

**Acceptance Criteria:**
- Email must follow the format `name@domain.xyz` and is **mandatory**
- Contact name is **mandatory**
- Message is **mandatory** and must not exceed **500 characters**

**Test Scenarios Covered:**

| Category | Example Scenarios |
|---|---|
| ✅ Functional | Valid form submission with all correct fields |
| ❌ Negative | Submit with empty email field |
| ❌ Negative | Submit with invalid email (missing `@`, missing domain, etc.) |
| ❌ Negative | Submit with empty name field |
| ❌ Negative | Submit with empty message field |
| 🔲 Boundary | Message at exactly 500 characters — should be accepted |
| 🔲 Boundary | Message at 501 characters — should be rejected |
| 🔲 Boundary | Message at 0 characters — should be rejected |
| 🔲 Edge Case | Email with special characters, subdomains, uppercase |

---

### 3. 💬 WhatsApp Business Plugin

**User Story:** As a business, I want to use a WhatsApp plugin in my dashboard to communicate with customers.

**Acceptance Criteria:**
- Plugin is installed via **phone number + OTP**
- User can **chat** with customers
- User can **share products** saved in the dashboard
- User can **send images** to customers

**Test Scenarios Covered:**

| Category | Example Scenarios |
|---|---|
| ✅ Functional | Successful plugin installation with valid phone + correct OTP |
| ✅ Functional | Send a text message to a customer |
| ✅ Functional | Share a saved product card to a customer |
| ✅ Functional | Send an image to a customer |
| ❌ Negative | Install with invalid phone number format |
| ❌ Negative | Install with incorrect/expired OTP |
| ❌ Negative | Share a product that is no longer available in the dashboard |
| ❌ Negative | Send an unsupported image format |
| 🔲 Edge Case | OTP expires before entry — user must request new OTP |
| 🔲 Edge Case | Send very large image file |

---

## 🗂️ Test Case Format

Each PDF follows a standard test case template:

| Field | Description |
|---|---|
| **Test Case ID** | Unique identifier (e.g., `TC-CC-001`) |
| **Test Title** | Short description of the scenario |
| **Preconditions** | System state before test execution |
| **Test Steps** | Numbered, reproducible steps |
| **Expected Result** | Clear, observable outcome |
| **Test Type** | Functional / Negative / Boundary / Business Logic |
| **Priority** | High / Medium / Low |

---

## 🧠 Testing Techniques Applied

- **Equivalence Partitioning** — grouping valid/invalid email formats, discount conditions
- **Boundary Value Analysis** — 499 / 500 / 501 character message tests
- **Decision Table Testing** — all discount combination logic mapped and tested
- **Negative Testing** — empty fields, invalid formats, rule violations
- **Business Logic Testing** — coupon exclusions, discount stacking rules

---

## 📌 Key Design Decisions

**Discount Logic (Credit Card):** The acceptance criteria contains an important constraint — the coupon discount (20%) **cannot** be used together with the new customer discount (15%). However, it **can** be combined with the loyalty card discount (10%). All valid combinations are covered as separate test cases to prevent ambiguity.

**Email Validation (Contact Us):** The format `name@domain.xyz` implies a mandatory TLD. Test cases cover structural variants including missing `@`, missing TLD, spaces in email, and numbers-only local parts to ensure the validation regex is comprehensive.

**OTP Expiry (WhatsApp Plugin):** Acceptance criteria does not specify OTP expiry behavior, so edge cases around expiry are included and marked for clarification with the development team.

