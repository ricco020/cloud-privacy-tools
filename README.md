# cloud-privacy-tools

> Python utilities to assess and verify privacy properties of cloud storage providers: encryption claims, jurisdiction exposure, share-link safety, breach-history surfacing.

Companion editorial site: **[Priviy](https://www.priviy.com/)** — independent cloud privacy reviews.

## Tools

| Tool | Purpose |
|------|---------|
| `tools/encryption_audit.py` | Reads a provider whitepaper URL or local PDF, extracts key claims (algorithms, KDF parameters, zero-knowledge architecture), surfaces gaps. |
| `tools/jurisdiction_check.py` | Given a provider, looks up its corporate domicile, server locations, and applicable surveillance frameworks (Five/Nine/Fourteen Eyes, CLOUD Act, GDPR). |
| `tools/sharelink_audit.py` | Inspects a public share link without downloading: does the provider expose metadata? Filename? Size? Preview? |
| `tools/breach_history.py` | Aggregates publicly-documented breach events for a provider (sources: HIBP API, official disclosures). |
| `tools/e2e_probe.py` | Practical probes to validate whether a provider's E2E claims hold (without attacking the service). |

## Quickstart

```bash
git clone https://github.com/ricco020/cloud-privacy-tools
cd cloud-privacy-tools
pip install -r requirements.txt

python tools/encryption_audit.py --provider proton-drive
python tools/jurisdiction_check.py --provider tresorit
python tools/sharelink_audit.py "https://share.example.com/abc123"
python tools/breach_history.py --provider lastpass
python tools/e2e_probe.py --provider mega
```

## Scope

These tools are **assessment** utilities — they do not exploit, decrypt, or attack any service. They surface what is publicly observable and compare it to the provider's marketing claims.

## Editorial references

The methodology behind these checks and detailed provider scorecards are published at the companion site:
- [E2E vs zero-knowledge cloud storage (FR)](https://www.priviy.com/fr/blog/e2e-vs-zero-knowledge-cloud-storage-2026)
- [E2E vs zero-knowledge cloud storage (EN)](https://www.priviy.com/en/blog/e2e-vs-zero-knowledge-cloud-storage-2026)
- [pCloud review 2026 (FR)](https://www.priviy.com/fr/avis-pcloud)
- [Methodology](https://www.priviy.com/en/methodology)

## Privacy notes

This toolkit makes outbound network calls to:
- The provider's documentation URL (HTTPS GET)
- HIBP API for breach lookups (k-anonymity, no plaintext sent)
- Public Wikidata for jurisdiction metadata

It does not log queries beyond local STDOUT and does not require API keys other than HIBP (free tier).

## Dependencies

```
pip install requests beautifulsoup4 PyPDF2 pycryptodome
```

Python 3.10+.

## License

CC0 — see [LICENSE](LICENSE). Use freely.

## Contributing

Adding provider profiles, new probes, and translating documentation are welcome. Open an issue first for substantial changes.
