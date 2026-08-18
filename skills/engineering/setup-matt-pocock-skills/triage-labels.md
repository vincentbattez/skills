# Triage Labels

The skills speak in terms of five canonical triage roles. This file maps those roles to the actual label strings used in this repo's issue tracker.

| Label in mattpocock/skills | Label in our tracker | Tracker label ID | Meaning                                  |
| -------------------------- | -------------------- | ---------------- | ---------------------------------------- |
| `needs-triage`             | `needs-triage`       | `<ID>`           | Maintainer needs to evaluate this issue  |
| `needs-info`               | `needs-info`         | `<ID>`           | Waiting on reporter for more information |
| `ready-for-agent`          | `ready-for-agent`    | `<ID>`           | Fully specified, ready for an AFK agent  |
| `ready-for-human`          | `ready-for-human`    | `<ID>`           | Requires human implementation            |
| `wontfix`                  | `wontfix`            | `<ID>`           | Will not be actioned                     |

When a skill mentions a role (e.g. "apply the AFK-ready triage label"), use the corresponding label string from this table.

The **Tracker label ID** column holds the tracker's own identifier for the label — a UUID in
Linear (`list_issue_labels`), a numeric id in GitLab (`glab api`). Fill it in when the tracker's
API addresses labels by ID; drop the column entirely for trackers that only use names (GitHub,
local markdown).

Record any pre-existing type labels the tracker already carries (`Bug`, `Feature`, …) in a second
table with their IDs — they are orthogonal to triage state and can be combined with the above.

Edit the label column to match whatever vocabulary you actually use.
