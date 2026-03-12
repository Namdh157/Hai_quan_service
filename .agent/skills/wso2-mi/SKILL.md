---
name: wso2-mi
description: WSO2 Micro Integrator (MI) development, API design, mediation sequences, and data services. Expert in Synapse XML and enterprise integration patterns.
allowed-tools: Read, Write, Edit, Glob, Grep, RunCommand
---

# WSO2 Micro Integrator Specialist Skill

> Enterprise Integration with WSO2 MI 4.x.
> **Focus on Synapse XML, Mediators, and Integration Patterns.**

## 🎯 Selective Reading Rule

**Read ONLY files relevant to the request!** Check the content map, find what you need.

---

## 📑 Content Map

| File | Description | When to Read |
|------|-------------|--------------|
| `mediators.md` | Core mediators (Log, Property, PayloadFactory, Call) | Designing mediation logic |
| `sequences.md` | Sequence design, named/inline, reusable patterns | Building integration flows |
| `apis.md` | Synapse REST API design, resources, URI templates | Designing REST interfaces |
| `endpoints.md` | HTTP, Address, LoadBalance, Failover endpoints | Connecting to backend services |
| `error-handling.md` | Fault sequences, Error codes, Retry patterns | Building robust integrations |
| `connectors.md` | WSO2 Connectors (HTTP, Kafka, File) | Integrating with external systems |
| `data-services.md` | Data Service (.dbs), RDBMS/CSV sources | Exposing data as services |
| `references/` | 📁 User-defined Use Case (UC) documentation | Understanding project business logic |

---

## ✅ Decision Checklist

Before implementing a flow:

- [ ] **Mediator selection:** Is this the most efficient mediator (e.g., PayloadFactory vs Enrich)?
- [ ] **Endpoint configuration:** Correct timeout and retry policies applied?
- [ ] **Error Handling:** Is there a proper fault sequence for this flow?
- [ ] **Context path:** Unique and following naming conventions?
- [ ] **Reuse:** Can any logic be extracted into a reusable Sequence or Local Entry?
- [ ] **Code Convention:** For REST APIs and Use Cases (UC), does it strictly follow the **"Standard Resource Template (UC Pattern)"** defined in `apis.md`? (Explicit property extraction, validation filter, logging, and backend mapping).

---

## ❌ Anti-Patterns

**DON'T:**
- Use Script Mediator for simple logic (use Property/Enrich instead)
- Use `SELECT *` in Data Services
- Hardcode values in XML (use Properties or Registry)
- Overuse Class Mediators (try to stick to standard mediators for maintainability)
- Ignore `ERROR_CODE` in fault sequences

---

## Script

| Script | Purpose | Command |
|--------|---------|---------|
| `scripts/validate_xml.py` | Basic Synapse XML validation | `python scripts/validate_xml.py <file_path>` |
