# Contribuer

Merci de l'intérêt porté à ce skill. Quelques règles simples :

## Avant de proposer un changement

- Gardez `SKILL.md` sous ~500 lignes. Si une section grossit trop, déplacez le détail dans un fichier de `references/` et pointez-y depuis `SKILL.md`.
- N'ajoutez pas d'abstraction ou de section qui ne sert pas directement le workflow en deux passes (constat → confirmation → correction). C'est le principe même du skill — il s'applique aussi à lui-même.
- Si vous ajoutez une vérification (ex. un nouveau type de faille à détecter), donnez un exemple concret de `file:line` attendu dans le tableau de sortie.

## Tester un changement

1. Modifiez `SKILL.md`.
2. Lancez `python3 -m scripts.quick_validate <chemin-du-skill>` (script fourni par [skill-creator](https://github.com/anthropics/skills)) pour vérifier que le frontmatter reste valide.
3. Si possible, testez sur un vrai petit dépôt (avec et sans tests existants) et vérifiez que Claude respecte bien les deux passes.

## Soumettre

Ouvrez une Pull Request avec :
- Ce qui a changé et pourquoi
- Un exemple de prompt avant/après si le comportement du skill change
