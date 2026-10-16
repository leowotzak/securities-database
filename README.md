# Securities Database

The purpose of this repository is to maintain a datastore of different securities and their associated price points over various time windows (ex. intraday, daily, weekly, monthly). The project will utilize PostgreSQL RDMS and serve as a demonstration of database design concepts in a field I'm personally curious of. The primary data source for this will be [Alpha Vantage](https://www.alphavantage.co/).

## Requirements Gathering

Database users will focus on three different groups of people: Stakeholders (investors/portfolio managers, product managers, business decision makers, and operations), engineers, and technical staff.

---
#### Stakeholders

*Question: What is the purpose of this database and what do you hope to achieve from it?*

- **Complete coverage:** All asset classes (equities, bonds, ETFs, options), with reliable cross-referencing of identifiers (ticker, CUSIP, ISIN, FIGI)
- **Deep, unbiased history:** Delisted securities retained, prices adjusted for splits and dividends
- **Point-in-time views:** Reproduce exactly what the database showed on any past date
- **Auditability:** Source, timestamp, and correction history on every data point
- **Flexibility:** Add new asset classes and attributes without a rebuild
- **Right-sized freshness:** Real-time, delayed, or end-of-day depending on asset class and use case

---
#### Engineers

*Question: How do you currently manage and store this data? What challenges and limitations do you face?*

- **Overwrite-in-place updates:** No history, so past states can’t be reconstructed
- **One wide table for everything:** 300+ columns, mostly NULLs, hard to extend
- **No lineage or validation:** Bad vendor data flows through unchecked
- **Nightly batch only:** Slow, fragile, no intraday support
- **Duplicated copies across teams:** No single source of truth
- **Shared logins:** No audit trail of who accessed or changed what

---
#### Technical Personnel

*Question: What primary tasks or activities do you perform that involve data storage and retrieval?*

- **Point-in-time retrieval:** “What did we know on this date?”
- **Audit trail:** Who changed what, when, and why.
- **Reconciliation:** Comparing two data sets and flagging differences.
- **Reference data accuracy:** One correct identifier and security record behind every transaction.
- **Date-driven queries:** Trade date, settlement date, record date, and valuation date all matter and are different.

## Analysis & Design
