## Videos

-  | Isolated issue
-  | Deep Dive

---

# Issues & Updates

> This file is the single source of truth for the guestsage.com Booking Engine imprementation for zaciszeturawa.pl — Work in Progress 

---

## v0.0.1 — 12 June 2026

### #1 Top priority fix requests:

- **Database SLOW AF** — affecting both BE and PMS - currently exploring 3rd party VPS options.

- **Make stay packages NOT visible if not available for the selected dates** — this is confusing be cause we have a lot of them, it makes the whoe BE slow, there's no logic to only show them if someone is off by 1 day for example. Meanwhile, "Show unavailable offers” MUST be enabled, otherwise the calendar looks like the hotel is closed during PEAK season. 

- **PMS sync including all GSBE price plans and all their settings** — instructions still unclear.

- **ONBOARDING CHECKLIST** — requested on 27 May, probably doesn't exist

## Known Issues

### #2 Sign-up, Sign-in, Sign-out, Cookies

1. **By default the GSBE is requesting access to other apps and services in a modal** - NOT A DESIRED FUNCTIONALITY
2. **What determines whether Gmail social login loads by default on mobile and on desktop?** Unclear, seem random
3. **I still see the login banner after I’ve just logged in (on mobile).** *Fix timeline estimate?*
4. **I only see a login login link on desktop when there’s an active discount for that.** - maybe that's actually good. Can we disable logging in completely? Unclear
5. **I don’t see any indication AT ALL indicating if I’m currently logged in or not. Impossible to log out.** This is a  USER PRIVACY VIOLATION! *Fix timeline estimate?*

---

### #3 API SYNC

1. **API DOCS NOT AVAILABLE** — I know which data has a 2 way sync, which only one way, and which way is it?? Send specific documentation PLEASE


### #4 CSS docs

1. **Supported and unsupported CSS rules?** - unknown
2. **Content mapping docs?** - non-existent


### #5 Rich HTML emails
- **NOT SUPPORTED** — emails look basic AF. *Fix timeline estimate?*

### #6 Additional options config

1. **UNCLEAR** - units: pieces / per person / per night / per night per person, etc VS how it's shown in the checkout - I don't get it. Docs?


### #7 TBC



## Fixed

1. Crucial paynow WEBHOOK (adres powiadomień)  **https://cloud.kwhotel.com/paynow/response**



# Contact

**marcin@zaciszeturawa.pl**
**szydlowski001@gmail.com**  



---

## Roadmap

| Feature | Status | Target |
|---|---|---|
| Unclear | In progress | Q3 2026 |
| Unclear | Planned | Q3 2026 |
| Unclear | Planned | Q4 2026 |
| Unknown | Under review | TBD |

---

## Architecture Notes

WIP

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



