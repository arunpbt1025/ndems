# NDEMS — National Digital Evidence Management System

Live App: https://ndems.onrender.com  
Problem Statement: PS-019 (Personal-Data Discovery and Privacy Evidence Inventory)  
Track: Cyber Security | AIORI-3  
Team: Numera 2.0 (Code: A3-PS019-TC072)  
Team Lead: Arun Bharti  

---

## What is NDEMS?

NDEMS is an automated evidence ingestion and integrity-verification system built for cyber forensic workflows. It solves two critical legal problems during evidence intake:

1. **Tamper Detection (Section 63 BSA, 2023):** Computes cryptographic bitstream hashes (SHA-256) upon file intake and records them onto an immutable smart contract ledger. Any minor byte alternation immediately triggers a mismatch flag.
2. **Privacy Protection (DPDP Act, 2023):** Sanitizes and masks personally identifiable information (PII) such as phone numbers, emails, and government identity patterns before evidence records are moved to downstream analysis.

---

## Core Architecture & Workflow

```text
[ Incoming File / Evidence ]
           │
           ├──> Regex Parser & PII Masking Engine ──> Redacted Evidence Copy
           │
           ├──> SHA-256 Bitstream Hash Engine
                     │
                     ├──> Hardhat / Ethereum Local Ledger (Smart Contract Custody)
                     │
                     └──> Ingestion Store (JSON Records + State Map)
                               │
                               v
               [ Forensic Comparator Engine ]
                 ├── Hash Match    --> Verified -> Sec 63 BSA Certificate
                 └── Hash Mismatch --> Live Tamper Alert (Court Inadmissible)