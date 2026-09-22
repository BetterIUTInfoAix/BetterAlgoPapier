# Publier une nouvelle version de Better Algo Papier

Ce document explique comment publier l'extension sur les trois canaux de
distribution. Il s'adresse aux membres de l'organisation
[BetterIUTInfoAix](https://github.com/BetterIUTInfoAix).

## Les règles d'or

1. **On ne partage JAMAIS un token** (ni dans un message, ni dans un commit,
   ni dans une variable d'env commitée). Chacun crée le sien (voir plus bas).
   Un token leaké = quelqu'un peut publier n'importe quoi à notre nom.
2. **Une version = un seul éditeur.** Annoncez-vous avant de publier pour
   ne pas publier deux fois la même version en parallèle.
3. **La version est la même partout** : tag git = Release GitHub = Marketplace
   VS Code = Open VSX.

## Être ajouté comme éditeur (une seule fois, par un owner)

### Marketplace VS Code (Microsoft)

Un propriétaire du publisher fait :

1. Aller sur <https://marketplace.visualstudio.com/manage/publishers/betteriutinfoaix>
2. **Members** → **Add** → inviter le compte Microsoft/GitHub du nouveau membre
   (avec le rôle qui va bien)

### Open VSX (VSCodium)

Un propriétaire du namespace fait :

1. Aller sur <https://open-vsx.org/namespace/betteriutinfoaix> (connecté)
2. **Add member** → inviter le compte GitHub du nouveau membre

Une fois membre des deux côtés, vous pouvez publier avec **votre propre
token**, obtenu comme suit.

## Créer ses tokens (une seule fois par personne)

### Token Azure DevOps (pour le Marketplace VS Code)

1. Aller sur <https://aex.dev.azure.com> (connexion avec le même compte que
   celui invité ci-dessus), entrer/créer une organisation
2. Dans l'organisation : icône ⚙️ *User settings* (en haut à droite) →
   **Personal access tokens** → **+ New Token** :
   - **Name** : `vsce`
   - **Organization** : **All accessible organizations** (important !)
   - **Expiration** : 30 à 90 jours
   - **Scopes** : *Custom defined* → lien **"Show all scopes"** en bas →
     section **Marketplace** → cocher **Manage**
3. **Create** → copier le token immédiatement (il n'est plus jamais affiché)

### Token Open VSX (pour VSCodium)

1. Aller sur <https://open-vsx.org> → **Login with GitHub**
2. Signer le *Publisher Agreement* depuis la page profil (crée un compte
   Eclipse avec le **même e-mail** que votre GitHub si demandé)
3. **Account Settings → Access Tokens → Generate** → copier le token

## Publier une version (exemple : 1.0.2)

### 0. Prérequis (une seule fois)

```bash
npm install -g @vscode/vsce
```

(Si erreur `EACCES` : `mkdir ~/.npm-global && npm config set prefix ~/.npm-global`
puis ajouter `export PATH="$HOME/.npm-global/bin:$PATH"` au `~/.bashrc`.)

Connexion au Marketplace (mémorise le token) :

```bash
vsce login betteriutinfoaix
```

### 1. Version + commit + tag

```bash
# modifier "version": "1.0.2" dans package.json (+ vos changements)
git add -A
git commit -m "1.0.2 : ce qui change"
git tag v1.0.2
git push origin main v1.0.2
```

Le tag déclenche le workflow GitHub qui construit le `.vsix` et crée la
Release automatiquement.

> Dépendances CI : les actions sont épinglées au SHA (`uses: ...@<SHA> # vX`)
> et `vsce` à une version exacte. Ne jamais repasser un tag mutable :
> accepter la PR Dependabot hebdo, ou résoudre le nouveau SHA via
> `gh api repos/<owner>/<repo>/git/ref/tags/<tag> --jq .object.sha`
> (si type `tag`, peler avec `gh api repos/<owner>/<repo>/git/tags/<sha> --jq .object.sha`).

### 2. Marketplace VS Code

```bash
vsce publish
```

### 3. Open VSX (VSCodium)

```bash
npx ovsx publish -p VOTRE_TOKEN_OPEN_VSX
```

(Le `create-namespace` n'est à faire qu'une seule fois dans la vie du
projet, par le premier éditeur.)

### 4. Vérifier

- <https://marketplace.visualstudio.com/items?itemName=betteriutinfoaix.better-algo-papier>
- <https://open-vsx.org/extension/betteriutinfoaix/better-algo-papier>
- <https://github.com/BetterIUTInfoAix/BetterAlgoPapier/releases>

## En cas de problème

| Symptôme | Cause probable |
| --- | --- |
| `Access Denied ... View user permissions` | Publisher inexistant, ou vous n'êtes pas membre, ou mauvais compte |
| `You must use a PAT from an organization...` | Le PAT a été créé sur une seule organisation (mettre *All accessible organizations*) |
| `Access tokens cannot be created ... Publisher Agreement` | Signer l'accord Eclipse d'abord (voir plus haut) |
| `version already exists` | La version est déjà publiée → bumper la version |
