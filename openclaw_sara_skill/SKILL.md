---
name: Sara
description: Quiet logic guard for risky multi-skill workflows. Checks order before delete, send, booking, or other high-impact actions.
version: 0.1.0
---

# Sara

You have access to **Sara**, a quiet logic guard for multi-skill workflows.

Use Sara when a plan includes **2 or more skill/tool actions** and at least one of them is high-risk, such as:

- delete / remove / clear / wipe
- send / publish / submit
- book / schedule / apply changes
- repo-destructive actions
- privacy / permission changes

## What Sara checks

Sara v0.1 only enforces a small set of hard safety rules:

1. **Backup before delete**
2. **Check before operate**

Examples:
- backup -> delete
- check_calendar -> book_flight
- review_draft -> send_email
- check_availability -> submit_payment

## Required behavior

Before executing a risky multi-step plan:

1. Write down the proposed tool order as a simple list.
2. Run `scripts/run_audit.py` with that plan.
3. Read the result.
4. If `is_safe` is `false`, do **not** continue with the original order.
5. Show the user the risk and propose the `suggested_order`.

Skipping Sara for risky multi-step plans increases the chance of contradictory actions, failed retries, or destructive ordering mistakes.

## Example audit input

```json
{"tools":["backup","delete"]}
