# Requirements Document

## 1. Application Overview

### 1.1 Application Name
LoanFlow AI (Intelligent Loan Origination, Affordability & Decision Management System)

### 1.2 Application Description
LoanFlow AI is a comprehensive loan origination and decision management web application. It manages the complete end-to-end loan lifecycle, including applicant profile management, employment and income verification, credit facility tracking, loan application processing, deterministic affordability calculations, automated rule-based decisioning, document verification, repayment schedule generation, exception and issue management, immutable audit logging, and portfolio analytics.

---

## 2. Users and Core Scenarios

### 2.1 Target Users
- **Loan Officers / Underwriters**: Initiate loan applications, review applicant documents, assess affordability metrics, and resolve manual review decisions.
- **Credit Risk & Compliance Officers**: Configure loan product parameters, review decision logic outcomes, audit exceptions, and inspect compliance audit logs.
- **Portfolio & Operations Managers**: Monitor pipeline KPIs, analyze approval/rejection trends, generate portfolio reports, and export analytical data.

### 2.2 Core Scenarios
- Registering applicant personal, employment, and income details along with existing credit facilities.
- Submitting a new loan application against a configured loan product with automated eligibility and affordability checks.
- Evaluating deterministic rule-based decisions (Approved, Rejected, Manual Review) with transparent reason codes.
- Verifying submitted applicant documents and flagging missing or invalid records.
- Generating and inspecting reducing-balance monthly repayment schedules for approved applications.
- Investigating and resolving data or policy exceptions within the exception tracking queue.
- Reviewing portfolio metrics, charts, audit trails, and exporting analytical reports.

---

## 3. Page Structure and Functional Specifications

### 3.1 Information Architecture

```
LoanFlow AI
├── Top Navigation Bar
│   ├── Global Search Bar (with AI Search integration)
│   ├── Quick Action Menu
│   ├── Date Display & User Profile
│   └── System Notifications
├── Collapsible Sidebar Navigation
│   ├── 1. Dashboard Overview
│   ├── 2. Applicants Management
│   ├── 3. Loan Applications
│   ├── 4. Loan Products
│   ├── 5. Affordability Analysis
│   ├── 6. Loan Decisions
│   ├── 7. Document Verification
│   ├── 8. Repayment Schedules
│   ├── 9. Exception Management
│   ├── 10. Audit Logs
│   ├── 11. Reports & Analytics
│   └── 12. Settings & System Seed
```

### 3.2 Page Functional Specifications

#### 3.2.1 Top Navigation Bar
- **Global Search**: Supports multi-entity search across applicants, applications, products, and exceptions with AI-powered search capability via ai-search.
- **Quick Action**: Direct triggers to register a new applicant, create a new loan application, or launch product configuration.
- **System Status Bar**: Displays current system timestamp and user session profile.

#### 3.2.2 Dashboard Overview
- **KPI Metric Cards**: Real-time calculated indicators:
  - Total Applicants Count
  - Total Loan Applications Count
  - Approved Applications Count
  - Rejected Applications Count
  - Manual Review Queue Count
  - Total Loan Amount Requested
  - Total Approved Loan Amount
  - Average Debt-to-Income (DTI) Ratio
- **Portfolio Charts**:
  - Application Status Distribution
  - Product Volume Distribution
  - Monthly Application Trends
  - Approval vs. Rejection Rates
  - Applicant Income Distribution
  - Risk Rating Distribution
- **Operational Feeds**:
  - Recent Applications Table (with direct status navigation)
  - Latest Decision Outcomes
  - Pending Document Verification Queue
  - High-Risk Application Alerts
  - Latest System Audit Events

#### 3.2.3 Applicants Management
- **Applicant List**: Paginated, filterable by name, national ID, employment status, risk band, and registration date.
- **Applicant Registration & Editing**: Form capturing personal details, contact information, national ID, and residence data.
- **Applicant Detail Profile**:
  - Overview of demographic details
  - Employment History table (employer, tenure, status, job title)
  - Income Records table (source, monthly amount, frequency, verification state)
  - Active Credit Facilities table (lender, facility type, credit limit, outstanding balance, monthly commitment)
  - Historic Loan Applications & Decisions timeline

#### 3.2.4 Loan Applications Management
- **Application Pipeline**: Tabular and status-filtered views across lifecycle states (DRAFT, SUBMITTED, UNDER_REVIEW, APPROVED, REJECTED, MANUAL_REVIEW, DISBURSED, CLOSED).
- **Application Creation Wizard**:
  - Step 1: Select or search applicant
  - Step 2: Select active loan product
  - Step 3: Input requested principal and tenure
  - Step 4: Upload/link required documents
  - Step 5: System eligibility pre-check and affordability preview
  - Step 6: Submission and initial state transition
- **Application Detail View**:
  - Summary of requested terms and applicant profile
  - Current lifecycle stage tracker with state transition actions
  - Embedded affordability summary, decision panel, and attached document statuses

#### 3.2.5 Loan Products Management
- **Product List**: View all loan products (e.g., Personal Loan, Auto Loan, Mortgage, SME Microloan).
- **Product Configuration**:
  - Product Name and Code
  - Minimum and Maximum Principal Amount
  - Minimum and Maximum Tenure (in months)
  - Annual Percentage Interest Rate (APR)
  - Minimum Monthly Income Requirement
  - Maximum Allowed DTI Ratio
  - Required Employment Status (e.g., Permanent, Self-Employed)
  - Required Document Checklist
  - Active/Inactive Status Toggle

#### 3.2.6 Affordability Analysis
- **Calculation Engine Interface**:
  - Inputs: Net monthly verified income, total existing monthly debt obligations, requested loan amount, product interest rate, requested tenure.
  - Outputs:
    - Equal Monthly Installment (EMI) using deterministic reducing-balance formula
    - Total Monthly Debt Commitments (Existing Obligations + Proposed EMI)
    - Debt-to-Income (DTI) Ratio (%)
    - Net Monthly Disposable Income
    - Maximum Affordable Loan Amount under product DTI ceiling
- **Affordability Records Log**: Historical record of every affordability calculation performed for auditability.

#### 3.2.7 Loan Decisions Management
- **Decision Queue**: Overview of automated and manual decisions with rule results.
- **Decision Detail View**:
  - Final Outcome: APPROVED, REJECTED, or MANUAL_REVIEW
  - Rule Evaluation Breakdown: Detailed table of each business rule checked (e.g., Min Income Check, Max DTI Check, Product Limit Check, Employment Stability Check, Document Completeness Check)
  - Primary Rule Reason Codes and Explanations
  - Stored Snapshot of Input Data and Rule Engine Version
  - Manual Review Override Form (for Underwriters) with mandatory rationale notes

#### 3.2.8 Document Verification
- **Verification Queue**: Filterable by document type (Identity Proof, Address Proof, Income Proof, Employment Proof, Bank Statement) and status (PENDING, VERIFIED, REJECTED, MISSING).
- **Document Review Workspace**:
  - Document metadata and view pane
  - Verification action buttons (Verify, Reject, Request Re-upload)
  - Verification notes and reviewer attribution
  - Missing document checklist generator for linked loan applications

#### 3.2.9 Repayment Schedules
- **Schedule Generator**: Computes amortization schedules for approved loans.
- **Amortization Breakdown Table**:
  - Period Number / Installment Due Date
  - Beginning Balance
  - Monthly Installment Amount (EMI)
  - Principal Portion
  - Interest Portion
  - Ending Outstanding Balance
- **Schedule Totals Validation**: Total principal paid, total interest paid, aggregate repayment sum, reconciliation verification status.

#### 3.2.10 Exception Management
- **Issue Tracking Dashboard**: Centralized register of policy exceptions and data inconsistencies:
  - Missing Income Proof / Verification discrepancies
  - Duplicate Application submissions
  - Severe debt burden or negative disposable income
  - Term or amount outside loan product constraints
  - Amortization reconciliation discrepancies
  - Decision triggered prior to document completion
- **Issue Resolution Modal**: Severity assignment (Low, Medium, High, Critical), assignee routing, resolution status (OPEN, IN_PROGRESS, RESOLVED, WAIVED), and audit remarks.

#### 3.2.11 Audit Logs
- **Audit Trail Explorer**: Read-only log of every system transaction:
  - Timestamp
  - Acting User / System Actor
  - Entity Type (Applicant, Application, Decision, Document, Schedule, Product)
  - Entity ID
  - Action Performed (CREATE, UPDATE, STATE_CHANGE, VERIFY, OVERRIDE)
  - Before and After State payload
  - IP and session metadata
- **Filter & Search**: Query by date range, actor, entity type, and action type.

#### 3.2.12 Reports & Analytics
- **Portfolio Reports**:
  - Monthly Origination Volume & Value Report
  - Approval, Rejection, and Manual Review Breakdown
  - Product Performance and Distribution Analysis
  - Risk Band & DTI Concentration Analysis
- **Data Export**: Export filtered dataset in CSV and JSON formats.

#### 3.2.13 Settings & Data Generator
- **Synthetic Data Generator Control**:
  - Configurable deterministic random seed
  - Execution trigger to generate sample dataset (10,000 applicants, 6,000 applications, 4 default loan products, and associated records including deliberate edge cases)
  - Database reset and re-seed mechanism
- **System Parameters**: Display of active rule engine versions and calculation constants.

---

## 4. Business Rules and Core Logic

### 4.1 Loan Application Lifecycle State Machine
- Valid states: `DRAFT` -> `SUBMITTED` -> `UNDER_REVIEW` -> `APPROVED` | `REJECTED` | `MANUAL_REVIEW` -> `DISBURSED` -> `CLOSED`.
- State transitions must strictly follow permitted paths; an application cannot move to `APPROVED` if required mandatory documents are in `MISSING` or `REJECTED` state, unless formally overridden.

### 4.2 Deterministic EMI Calculation Rule
- Reducing balance formula: `EMI = P * r * (1 + r)^n / ((1 + r)^n - 1)` where `P` = Principal, `r` = Monthly interest rate (Annual APR / 12 / 100), `n` = Tenure in months.
- Special boundary handling:
  - If `r == 0`, `EMI = P / n`.
  - Zero or negative principal inputs must be rejected with validation errors.
  - All installment calculations must be rounded to two decimal places, with final period rounding adjustment ensuring ending balance equals exactly 0.00.

### 4.3 Affordability Metrics
- `Total Monthly Debt = Sum(Applicant Existing Monthly Commitments) + Proposed Loan EMI`.
- `Debt-to-Income (DTI) Ratio = (Total Monthly Debt / Total Verified Monthly Income) * 100`.
- `Net Disposable Income = Total Verified Monthly Income - Total Monthly Debt - Stated Living Expenses`.
- If `Total Verified Monthly Income <= 0`, DTI must be flagged as non-computable (Infinite) and triggered for automatic rejection or manual review.

### 4.4 Deterministic Decision Engine Rules
- **REJECTED** if:
  - Requested principal is below product minimum or above product maximum.
  - Requested tenure is outside product minimum/maximum tenure.
  - Calculated DTI exceeds the maximum allowable threshold for the product.
  - Verified monthly income is below product minimum income requirement.
  - Identity document is verified as fraudulent or unresolvable.
- **MANUAL_REVIEW** if:
  - DTI is within borderline buffer (e.g., within 5% of product max DTI).
  - Employment tenure is under 6 months.
  - Multiple applications detected for the same applicant within 30 days.
  - Discrepancy detected between declared income and bank statement verified income.
- **APPROVED** if:
  - All eligibility, DTI, income, employment, and document verification criteria are strictly satisfied without triggers for review or rejection.

### 4.5 Repayment Schedule Integrity Rule
- Repayment schedules can only be generated for applications in `APPROVED` or `DISBURSED` states.
- The sum of all schedule principal portions must equal the disbursed principal amount exactly.

---

## 5. Exceptions and Edge Cases

| Case ID | Scenario Description | Expected System Behavior |
| :--- | :--- | :--- |
| EX-01 | Applicant has zero declared or verified income | Reject affordability check; prevent automated approval; flag issue in Exception Management. |
| EX-02 | Duplicate loan application submitted while an active application is pending | Block submission or mark status as `MANUAL_REVIEW` and log duplicate submission exception. |
| EX-03 | Stated income conflicts with verified document record | Route application to `MANUAL_REVIEW` with issue code `INCOME_MISMATCH`. |
| EX-04 | Requested tenure or principal outside product boundaries | Reject application instantly with specific constraint violation reason code. |
| EX-05 | Decision requested when required documents are missing | Block automated decision or flag `PENDING_DOCUMENTS` exception; route to underwriter review. |
| EX-06 | Amortization schedule rounding discrepancy | Apply penny-adjustment on the final installment to ensure exact zero closing balance. |
| EX-07 | Underwriter manual override of rejection | Require mandatory text justification; record immutable before/after snapshot in Audit Logs. |

---

## 6. Acceptance Criteria

1. The user can create, view, edit, and search applicant profiles containing employment, income, and credit facility records.
2. The system allows configuring loan products with principal limits, tenure ranges, interest rates, and eligibility thresholds.
3. The user can submit a loan application through the multi-step workflow and track its lifecycle states with enforced validation.
4. The affordability engine accurately computes reducing-balance EMI, DTI ratio, and disposable income based on verified financial data.
5. The decision engine deterministically outputs Approved, Rejected, or Manual Review statuses along with clear rule reason codes and input snapshots.
6. Underwriters can review, verify, or reject uploaded applicant documents and trigger missing document alerts.
7. The system generates complete, balanced amortization repayment schedules for approved applications with zero ending balance reconciliation.
8. The exception management module records, classifies, and tracks resolution for data inconsistencies, policy breaches, and review queues.
9. All entity modifications, status changes, manual overrides, and decision events produce immutable audit logs queryable by date, actor, and entity.
10. The dashboard and analytics module correctly display aggregated metrics, distribution charts, and enable CSV/JSON report exports.

---

## 7. Out of Scope (Current MVP)

- Integration with live external banking payment rails or real-time fund disbursement gateways.
- Live credit bureau API integrations (credit facilities and scores are simulated via system database).
- Automated OCR/AI document parsing (document verification is managed via internal review workflows).
- Customer-facing self-service loan portal (current scope focuses on internal underwriting and management platform).
- SMS and external email dispatch gateways.
