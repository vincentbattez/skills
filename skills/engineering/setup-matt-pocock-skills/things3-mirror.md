# Mirror new work to Things 3

Append this section to `docs/agents/issue-tracker.md`, below the tracker's own conventions.
Replace `<THINGS PROJECT>` with the confirmed project title (emoji included — it is part of the
title) and `<ISSUE-ID>` with whatever identifier the tracker uses (`VIN-42`, `#128`, `03-slug`).

---

## Mirror new work to Things 3

New work created for this repo is also mirrored as a task in the user's Things 3 to-do list,
using the `things3` skill (`things` CLI). Do it in the same run, right after the issue is
created.

The point is that nothing gets forgotten: everything the user has to do surfaces in Things 3.
Only the parent surfaces there — never the details.

**Mirror the root of a work item, never its children.** A feature broken into 10
implementation tickets stays a single Things task, the one named after the feature.

- A spec, feature, or parent issue is published (`/to-spec`) → create the task.
- A standalone issue with no parent — feature, bug, chore, whatever it is → create the task.
- Children — `/to-tickets` slices, sub-issues, any ticket under a spec → create nothing. The
  parent already has its task.

Fields:

- **Project**: `<THINGS PROJECT>` — pass the emoji, it is part of the title.
- **Title**: `[<ISSUE-ID>] <feature in French>` — short and direct (~35 characters total). The
  Things title column is narrow: no trailing punctuation.
- **Notes**: `<ISSUE-ID> — <one-line French summary>` on the first line, the spec URL (or file
  path, for a local-markdown tracker) on the second.
- **Tags**: `--tags="🤖 IA: Ready to auto-implement"`
- **Checklist**: the manual acceptance checks the user will run themselves once the issue is
  done. One `--checklist-item` per check, 3–6 items. See below.

```bash
things add "[<ISSUE-ID>] Système de notifications" --list "<THINGS PROJECT>" \
  --tags="🤖 IA: Ready to auto-implement" \
  --notes "<ISSUE-ID> — Notifications in-app et système, avec réglages par projet
<spec URL>" \
  --checklist-item "Recevoir une notif système avec l'app en arrière-plan" \
  --checklist-item "Couper les notifs d'un projet → plus rien pour ce projet" \
  --checklist-item "Cliquer la notif → ouvre la bonne session"
```

### Checklist: what the user verifies by hand

The task carries a short list of things **the user** checks personally once the issue is closed
— the app-level verification an agent can't do (visual, feel, real data, real device).

- Derive it from the issue's acceptance criteria, one item per observable behaviour.
- Phrase each item as an action with its expected result: "Ouvrir X → Y s'affiche".
- 3–6 items max. Skip anything already covered by an automated test — the point is what only a
  human eye catches.
- Same rule as the task itself: only the root work item gets a checklist, never the children.

Check for an existing task first to avoid duplicates. `--project` requires a `--query`;
`title:/./` is the catch-all:

```bash
things search --query=title:/./ --project="<THINGS PROJECT>" --select="uuid,title,notes" --json
```

The first result is the project row itself (its title, empty notes), not a duplicate.
