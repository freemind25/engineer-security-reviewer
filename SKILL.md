# 1. Authentifiez-vous (une seule fois)
gh auth login

# 2. Clonez votre repo
git clone https://github.com/freemind25/engineer-security-reviewer.git
cd engineer-security-reviewer

# 3. Créez une branche
git checkout -b enhance/security-reviewer-v2

# 4. Créez/modifiez le fichier SKILL.md
# Collez le contenu que j'ai fourni

# 5. Committez
git add SKILL.md
git commit -m "enhance: security reviewer v2 with supply chain, context modes, triage summary"

# 6. Poussez (l'auth est déjà gérée par gh)
git push origin enhance/security-reviewer-v2

# 7. Créez une PR sur GitHub.com
