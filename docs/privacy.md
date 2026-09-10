# Privacy · 隐私

Career stress tests ingest sensitive personal data: age, income, savings,
education, health/physical constraints, family situation, immigration plans.

## Rules · 规则

1. **Privacy by default.** Ask only for profile fields the stated goal
   actually needs. Never demand a complete profile.
2. **No persistence.** Do not write user personal data to files, memory
   systems, logs, or caches. The analysis lives in the conversation only,
   unless the user explicitly asks to save an output document.
3. **No exfiltration.** Never send personal data to third-party services,
   APIs, or web searches. When retrieving data, query only occupation/country
   level information (e.g. "BLS median wage electricians"), never personal
   attributes.
4. **Local reasoning.** Personal fit computation happens inside the agent's
   reasoning; profile data is never embedded in URLs, search queries, or
   filenames.
5. **User-owned exports.** If the user asks to save the report, save it
   locally where they specify; do not upload.
6. **Health data minimality.** Physical constraints are used only as
   hard-filter criteria (e.g. "cannot lift >10kg"), not stored or elaborated.

## For contributors

This repository must never contain real user profiles. All examples use
fictional personas.
