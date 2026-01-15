##Table of Contents
* [Core Concepts](#core-concepts)
* [Regulatory Standards](#regulatory-standards)
* [Technology Stack](#technology-stack)


# Fintech Technical Glossary
Welcome to my technical glossary.  This project is a living document where I translate complex financial concepts into chear, developer-friendly documentation.

## Core Concepts

### API (Application Programming Interface)
An **API** acts as a bridge between two software programs.  In Fintech, APIs allow your bank to talk to apps like *Venmo* or *Stripe* securely.

### KYC (Know Your Customer)
**KYC** is a mandatory process where businesses verify the identity of their clients.
* **Purpose:** To prevent money laundering and fraud.
* **Key Step:** Validating government-issed IDs.

### PCI DSS (Payment Card Industry Data Security Standard)
A set of security standards designed to ensure that **all** companies that accept, process, store, or transmit credit card information maintain a secure environment.

### Blockchain
A distributed, decentralized ledger technology.   In Fintech, it is used to record transactions across many computers so that the record cannot be altered retroactively.

### SaaS (Software as a Service)
A software licensing and delivery model in which software is licensed on a subscription basis and is centrally hosted.  Most modern Fintech tools (like *QuickBooks Online*) are SaaS.

## Regulatory Standards

### AML (Anti-Money Laundering)
A set of laws, regulations, and procedures intended to prevent criminals from disguising illegally obtained funds as legitimate income.  In Fintech, documentation must clearly outline how software flags suspicious activity.

### GDPR (General Data Protection Regulation)
A legal framework that sets guidelines for the collection and processing of personal information from individuals who live in the European Union (EU).
* **Note:** Even if a company is based in the US, if they have one customer in the SU, they must be GDPR compliant.

## Technology Stack

### Cloud Computing (AWS/Azure)
Most Fintechs host their data on remote servers (the "Cloud") rather than physical hardware in an office. This allows for global scaling and high-level security.

#Encryption at Rest vs. In Transit
* **At Rest:** Data is protected while it is stored on a disk.
* **In Transit:** Data is protected while it is moving between a user's phone and the bank's server. 

## System Visualizations

```mermaid
graph LR
    A[Customer App] -->|1. Request Payment| B(Payment Gateway)
    B -->|2. Validate Credentials| C{Security Shield}
    C -->|3. Approved| D[(Bank Database)]
    C -->|3. Denied| E[Error Message]
    D -->|4. Success Token| B
    B -->|5. Confirmation| A

```mermaid
graph TD
    User((User)) -->|Plaintext Data| SSL[SSL/TLS Encryption]
    SSL -->|Encrypted Tunnel| Server[Fintech Server]
    Server -->|Hashed Password| DB[(Secure Storage)]
    
    subgraph Internal Network
    Server
    DB
    end
