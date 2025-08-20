# RAG Procurement Sourcing Tool

## Project Goal

This project demonstrates a Supplier & Procurement Intelligence Sourcing Tool, based on RAG system built with OpenAI embeddings, FAISS for semantic search, and synthetic procurement data.

The workflow begins with the generation of realistic supplier documents such as capability decks (PDFs summarizing a supplier’s products, certifications, and lead times), contracts with key clauses (liability caps, Incoterms), audit reports (ISO/ROHS compliance), PO/ASN histories (used to calculate On-Time Delivery performance), meeting notes, and pricing tables.

These files are chunked into meaningful units — contract clauses, capability sections, and table rows — then embedded using OpenAI’s text-embedding-3-small model. The embeddings are stored in a FAISS index, alongside supplier metadata like region, category, certifications, and ESG flags. A lightweight natural language filter extractor enriches search by applying constraints (e.g., “ISO 13485 suppliers in ASEAN with < 4-week lead time”), and retrieved results are fed into an OpenAI LLM (gpt-4o-mini) to generate concise, context-grounded answers.

### Products & Parts in Scope

The synthetic dataset covers typical industrial components often sourced globally:


*   Impellers (316L stainless steel, sizes 50mm & 75mm)
*   Bearings (type 6205)
*   Pumps
*   Valves

These represent common mechanical parts with varied suppliers, lead times, and quality compliance requirements.

### Procurement KPIs

The project uses common procurement performance metrics:
*   Lead Time: The time between placing an order and receiving the goods.
*   On-Time Delivery (OTD): Percentage of deliveries arriving as promised (e.g., OTD = 95% means 95 out of 100 orders were delivered on time).
*   Audit Score: Result of quality or compliance audits (e.g., ISO certifications, ROHS compliance).
*   Supplier Rating: Overall performance score (synthetic, 1-5 scale).
*   Pricing & Cost: Unit prices in USD for each SKU.

### Synthetic Data Structure

The synthetic dataset is generated in multiple files/folders:


*   Supplier Master (suppliers.csv)
	- supplier_id, name, region, categories, certifications, esg_flags, rating
*   Capability Decks (PDFs)
	- Supplier profile (region, certifications, ESG flags)
	- Claimed lead times (standard/custom parts)
	- Historical OTD by quarter
*   Contracts (PDFs)
	- Contract ID, supplier details
	- Clauses: Scope, Pricing, Payment Terms, Liability Cap, Incoterms, Quality, Lead Time
*   Audit Reports (audit_reports.csv)
	- supplier_id, iso13485, iso9001, rohs, last_audit, score
*   PO/ASN Histories (po_asn.csv)
	- po_id, supplier_id, sku, category, qty, order_date, promised_date, shipped_date, asn_id, region
	- Used to calculate OTD by quarter
*   Notes (text files)
	- Informal meeting notes, supplier risks, improvement actions
*   Pricing Table (pricing.csv)
	- supplier_id, sku, part, price_usd, lead_time_weeks, region

### How This Helps Procurement

Procurement professionals often spend hours digging through contracts, supplier brochures, audit reports, and spreadsheets. This tool centralizes all that information into a semantic search engine in order to:

*   Quickly find alternative suppliers by part, region, or certification.
*   Check contract clauses like liability caps or Incoterms without reading entire PDFs.
*   Monitor supplier OTD trends and audit scores to evaluate reliability.
*   Compare prices and lead times across suppliers to optimize sourcing.
*   Apply ESG filters (e.g., conflict-free, low emissions) to align with sustainability goals.

By automating retrieval and summarization, procurement teams save time, reduce risk, and make better, data-backed sourcing decisions. Instead of manually opening dozens of PDFs, spreadsheets, and audit logs, category managers or supplier quality specialists can ask natural-language questions and instantly surface compliant alternative suppliers, lead-time risks, or contract terms. It reduces time-to-source, highlights suppliers with strong past OTD performance, and flags contract risks without requiring hours of document review. By filtering across ESG compliance and certifications, it also enables faster alignment with sustainability and regulatory requirements. Ultimately, this system empowers procurement professionals to make faster, evidence-backed sourcing decisions, improves supplier risk management, and frees teams from repetitive data lookup tasks so they can focus on strategic supplier relationships.
