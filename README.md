# Tracable

> Compliance Automation, Straight from your Infrastructure.

Tracable automates compliance. It pulls real-time configuration data from your cloud environments and maps it to controls from frameworks like SOC2 & ISO27001. No more screenshots, spreadsheets, or stale policies - just evidence you can trust.

---

## 🔥 Why Tracable?

- ✅ Designed for DevOps, not compliance managers
- 🛠 Framework-as-code - define what you need, verify in CI
- ☁️ Supports AWS (GCP, Azure coming soon)
- 📦 Exports to JSON, PDF, Markdown - ready for auditors or GRC tools

---

## ⚙️ Install

```bash
curl -sSL https://tracable.github.io/install.sh | bash
```
---

## 🚀 Quickstart

```bash
tracable init --framework soc2 --cloud aws
tracable check
tracable report --summary
tracable export --format pdf
```
Or define everything in `tracable.yaml`:

```yaml
framework: soc2
cloud: aws
account: prod
controls:
  - AC-2
  - AC-6
  - CM-2
```

---

### 📋 Supported Frameworks (WIP)

  - [ ] SOC2

  - [ ] ISO 27001

  - [ ] HIPAA

  - [ ] NIST 800-53

---

---

### 📤 Outputs

  - `tracable-report.md` - human-readable control report

  - `evidence.json` - structured data for export or ingestion

  - `screenshots/` - auto-generated console screenshots (optional)

  - `audit-ready.zip` - shareable bundle for auditors

---
