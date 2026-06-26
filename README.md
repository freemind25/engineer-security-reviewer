# engineer-security-reviewer

**Skill Claude (Agent Skill)** — audit de code en deux passes : sécurité, dépendances, duplication, puis correctifs uniquement sur ce qui est confirmé.

> Conçu pour fonctionner avec [Claude.ai](https://claude.ai), [Claude Code](https://claude.com/claude-code) et l'[API Claude](https://platform.claude.com), et compatible avec la spécification ouverte [Agent Skills](https://agentskills.io).

## Pourquoi ce skill

Demander à une IA d'« auditer mon code » donne souvent l'un des deux résultats suivants : soit elle réécrit tout sans demander, soit elle déclare des changements « sûrs » sans aucune preuve à l'appui. Ce skill impose une discipline simple :

1. **Passe 1 — Constat.** Sécurité, dépendances, duplication. Aucune modification de code. Restitution sous forme de tableaux.
2. **Passe 2 — Correction.** Uniquement ce que vous avez explicitement validé. Les changements de comportement sont annoncés, pas découverts après coup.

Le skill refuse explicitement de qualifier un changement de « sûr » s'il n'y a aucun test pour le prouver — il vous le dit, et propose plutôt d'écrire un test avant de toucher au code à risque.

## Quand Claude l'utilise

Déclenché par des demandes comme :
- « Audite mon code »
- « Fais une revue de sécurité de ce dépôt »
- « Vérifie les vulnérabilités / dépendances obsolètes »
- « Trouve les secrets en dur dans le code »
- « Trouve le code dupliqué et nettoie-le »

Et plus généralement toute demande combinant sécurité + dépendances + nettoyage, ou n'en couvrant qu'une partie (ex. juste « lance `npm audit` et dis-moi ce qui est risqué »).

## Installation

Les skills personnalisés **ne se synchronisent pas automatiquement entre surfaces** (claude.ai, Claude Code, API) — installez-le séparément selon où vous l'utilisez.

### Claude.ai
1. `git clone` ce dépôt, puis compressez le dossier `engineer-security-reviewer/` en `.zip` (le ZIP doit contenir le dossier du skill à sa racine, pas un sous-dossier).
2. Allez dans **Réglages → Fonctionnalités (Features) → Skills**.
3. Importez le fichier `.zip`.

*(Disponible sur les plans Pro, Max, Team et Enterprise, avec l'exécution de code activée.)*

### Claude Code
```bash
# Personnel (tous vos projets)
git clone https://github.com/<votre-compte>/engineer-security-reviewer ~/.claude/skills/engineer-security-reviewer

# Ou par projet (ce dépôt uniquement)
git clone https://github.com/<votre-compte>/engineer-security-reviewer .claude/skills/engineer-security-reviewer
```

### API Claude
Uploadez le dossier (ou son ZIP) via l'endpoint de création de Skill — voir la [documentation Agent Skills de l'API](https://platform.claude.com/docs/en/build-with-claude/skills-guide). Disponible workspace-wide une fois uploadé.

## Structure du dépôt

```
engineer-security-reviewer/
├── SKILL.md                          # Le skill lui-même (frontmatter + instructions)
├── README.md                         # Ce fichier
├── LICENSE
├── CONTRIBUTING.md
├── .github/workflows/validate-skill.yml  # Valide le frontmatter à chaque push/PR
├── scripts/validate_skill.py         # Script de validation autonome (zéro dépendance interne)
└── evals/
    └── evals.json                    # Prompts de test (non inclus dans le .skill packagé)
```

Le frontmatter (`name`, `description`) est validé automatiquement par CI à chaque push/PR sur `main` : kebab-case, ≤ 64 caractères pour le nom, ≤ 1024 caractères et aucun chevron pour la description.

## Exemple d'utilisation

```
Vous : "Audite mon code, sécurité d'abord, puis dépendances et duplication."

Claude :
  0. Détecte le stack (langage, framework, gestionnaire de paquets) et dit
     clairement si des tests existent ou non.
  1. Tableau Sécurité (sévérité, fichier:ligne, pourquoi, correctif suggéré)
  2. Tableau Dépendances (paquet, version actuelle → dernière, type, audit)
  3. Tableau Duplication (motif, emplacements, pourquoi, correctif suggéré)
  → s'arrête et attend votre confirmation avant de modifier quoi que ce soit

Vous : "Corrige la sécurité et les dépendances mineures, pas la duplication."

Claude :
  - Applique les correctifs de sécurité (annonce chaque changement de comportement)
  - Met à jour les dépendances patch/minor, liste les majeures séparément
  - Construit/teste après modification
  - Résumé final : ce qui a été corrigé, ce qui reste à votre décision
```

## Sécurité — lisez ceci avant d'activer un skill téléchargé

Conformément aux recommandations officielles d'Anthropic sur les skills personnalisés :
- **Relisez le contenu de tout skill avant de l'activer**, y compris celui-ci — c'est un fichier texte, vous pouvez (et devriez) le lire entièrement avant de l'importer.
- Ce skill ne contient **aucun secret, clé d'API, ni identifiant en dur**, et n'en demande jamais.
- Ce skill n'installe ni n'exécute aucun package au moment de son utilisation au-delà des outils déjà disponibles dans votre environnement Claude (terminal/exécution de code selon la surface).

## Limites connues

- C'est un ensemble d'instructions pour Claude, pas un scanner statique déterministe : la qualité du résultat dépend de l'accès de Claude au code (dépôt cloné, fichiers ouverts, etc.) et des outils d'audit réellement disponibles dans l'environnement d'exécution (ex. `npm audit` doit être installable/exécutable).
- En l'absence de tests dans le projet audité, le skill est conçu pour le signaler plutôt que de improviser une garantie — mais cela dépend de Claude qui suit correctement l'instruction à chaque session.

## Contribuer

Voir [`CONTRIBUTING.md`](./CONTRIBUTING.md).

## Licence

[MIT](./LICENSE) — utilisation, modification et redistribution libres, y compris commerciales, sans garantie.
