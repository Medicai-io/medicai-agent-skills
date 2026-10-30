# Changelog

## 0.1.0 (2026-10-29)

First packaged version of `medicai-integration`, private preview.

- Router SKILL.md with the two API layers, onboarding (15-day trial), no-account demo viewer, quickstart, eight rules, pitfalls table
- References: concepts, authentication (incl. workspace ids), viewer embed (demo viewer, embed + postMessage, gallery, public-study links), uploads (DICOM, files, cloud documents), cases and sharing (incl. trash/delete), webhooks, plans and limits, migrating from flat routes (existing integrations only)
- Synced to the October 2026 Medicai API: workspace-scoped routes everywhere, `X-Medicai-Client` mandatory, `searchInTrash` required, `withResources` on trash/delete, cloud documents from Markdown
- Four eval cases in the `claude plugin eval` layout, one of which never mentions Medicai
