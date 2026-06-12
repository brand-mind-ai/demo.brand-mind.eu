## Videos

- https://www.youtube.com/watch?v=U6gg_bi1I70 | Tutorial
- https://www.youtube.com/watch?v=_xTvejNLhyk | Deep Dive

---

# Issues & Updates

> This file is the single source of truth for the demo library.  
> Edit it in GitHub and the site updates automatically on next page load.

---

## v1.1.0 — June 2026

### Added

- **Multi-language inbound support** — AI now handles queries in Polish, German, and English within the same conversation thread
- **Live inventory sync** — KWHotel integration now pulls real-time room availability with sub-second latency
- **Confidence scoring** — every AI response now carries an internal confidence score; low-confidence answers auto-escalate to human

### Fixed

- Resolved a race condition in the handover protocol that occasionally caused duplicate escalation emails
- Fixed context loss when a conversation exceeded 4,000 tokens in the customer care sequence
- Corrected timezone handling for booking confirmations in UTC+2 regions

---

## v1.0.2 — May 2026

### Fixed

- Response latency under high concurrent load reduced from ~3.2s to ~0.8s avg
- Session memory now persists correctly across page refreshes in the web widget

### Known Issues

- **iOS Safari scroll bug** — the chat widget scroll position resets on keyboard dismiss. Workaround: user can tap outside the input to dismiss keyboard before scrolling.
- **Outlook compatibility** — automated email summaries render incorrectly in Outlook 2019 and earlier. Modern Outlook (365) and Gmail are unaffected.
- Integration with **XYZ CRM** pending audit from their API team — ETA unknown.

---

## Roadmap

| Feature | Status | Target |
|---|---|---|
| Voice input for inbound queries | In progress | Q3 2026 |
| WhatsApp Business channel | Planned | Q3 2026 |
| Analytics dashboard | Planned | Q4 2026 |
| Self-serve onboarding flow | Under review | TBD |

---

## Architecture Notes

The system runs on a **three-layer stack**:

```
[Inbound Channel]  →  [Routing Layer]  →  [Agent Core]
  Web / Social          Intent + Lang       LLM + Tools
  Email / Phone         Confidence Score    CRM / Booking
                        Escalation Rules    Knowledge Base
```

Each agent is stateless per session but uses a **persistent context window** managed by the routing layer. This means:

- No data is stored inside the model
- All memory is external and auditable
- GDPR deletion requests can be executed in under 60 seconds

```javascript
// Example: triggering a human handover
if (response.confidence < 0.72 || intent === 'complaint') {
  await escalate({
    to: 'human',
    context: session.history,
    reason: response.escalationReason
  });
}
```

---

## Contact

For technical issues: **ops@brand-mind.eu**  
For billing or account changes: use the client portal or contact your account manager directly.
