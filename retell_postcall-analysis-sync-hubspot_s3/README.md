# Post‑Call Analysis Sync (Retell.ai → S3 → HubSpot)
n8n workflows to capture **post‑call summaries** (via Retell.ai), store them in **S3**, convert **JSON → CSV**, and sync structured insights back to **HubSpot** (for social content & follow‑ups).

## Flow (Mermaid)
```mermaid
flowchart LR
    A[Call ends] --> B[Retell ai Post-call summary]
    B --> C[S3 Store raw JSON]
    C --> D[Convert JSON to CSV batch]
    D --> E[HubSpot Upsert notes and properties]
    E --> F[Optional Slack or Notion for review]
```

## Highlights
- **Event‑driven**: post‑call summaries land in S3 immediately
- **Transform**: JSON → CSV for analytics / bulk ops
- **CRM sync**: HubSpot notes + properties for searchability
- **Sanitized**: keys, tokens, buckets, URLs → placeholders

## Under the hood
- API orchestration between Retell.ai, AWS S3, and HubSpot  
- JSON → CSV data transformation for analytics  
- Dynamic S3 file handling and secure credential setup  
- Error handling, retries, and idempotent task design  
- Modular, stateful workflow structure for scalability

## 🔐 Security & Reliability
- Credentials stored as environment variables, never in nodes  
- All tokens, URLs, and bucket names sanitized before export  
- Workflow designed for safe retries without data duplication  
- Auditable logs for every upload and sync operation  

## Placeholders
- `{{hubspotToken}}`, `{{awsAccessKeyId}}`, `{{awsSecretAccessKey}}`, `{{awsRegion}}`
- `{{s3Bucket}}`, `{{s3Key}}`, `{{externalUrl}}`
- `{{redactedEmail}}`, `{{redactedPhone}}`

📜 License: CC BY‑NC 4.0 — Portfolio/demo only.
