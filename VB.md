# Surcouche perso (branche `vb`)

Ce clone remplace l'installation skills.sh (`~/.agents/skills/`) pour les skills de Matt.
Mes modifs vivent en commits sur `vb` au-dessus de `main` — un update upstream produit un
conflit git explicite au lieu d'un écrasement silencieux.

## Câblage

`~/.claude/skills/<nom>` → symlink vers `skills/<catégorie>/<nom>` de ce repo (23 skills).
Backup des anciennes cibles : `~/.claude/skills/.relink-backup.json`.

Rester sur `vb` : un `git checkout main` fait disparaître la surcouche des skills actives.

## Update depuis upstream

```sh
git fetch origin
git rebase origin/main        # depuis vb
```

En cas de conflit : résoudre, `git add`, `git rebase --continue`. Si un de mes commits est
devenu inutile (Matt a intégré la même idée), `git rebase --skip`.

Vérifier ce qui a bougé chez Matt avant de rebaser :

```sh
git log --oneline HEAD..origin/main -- skills/
```

## Mes commits

- `chore(vb)` — retire `disable-model-invocation` sur `implement`, `to-spec`, `to-tickets`,
  et préfixe leur description par `Matt skill - `.
- `feat(vb)` — Section D « Things 3 mirroring » dans `setup-matt-pocock-skills` + `things3-mirror.md`.
- `feat(vb)` — colonne `Tracker label ID` dans `triage-labels.md`.

## Non migré

`ubiquitous-language` et `writing-great-skills` n'existent plus upstream ; leurs symlinks
pointent encore vers `~/.agents/skills/`.
