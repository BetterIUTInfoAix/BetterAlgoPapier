# Better Algo Papier

Extension pour Visual Studio Code et VSCodium dédiée à l'algorithmique sur papier de l'IUT d'Aix-en-Provence.

## Fonctionnalités

- **Coloration syntaxique** : mots-clés, types, opérateurs, chaînes, nombres et appels de fonction.
- **Snippets** pour toutes les structures : `algorithme`, `si` / `sinon_si` / `sinon`, boucles `pour` / `tant_que` / `boucle` / `repeter`, `choix_sur`, déclarations…
- **Auto-complétion** des mots-clés et des types (par exemple `ent` → `entier`).
- **Indentation automatique** des blocs.
- **Pliage de code** (folding) sur les blocs `debut`/`fin`, `si`/`fsi`, `boucle`/`fboucle` et `choix_sur`/`fchoix`.

## Installation

### Visual Studio Code

Depuis le [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=betteriutinfoaix.better-algo-papier) : ouvrez le panneau des extensions (`Ctrl+Maj+X`), cherchez **Better Algo Papier** puis cliquez sur **Installer**.

Ou faites `Ctrl+P`, collez la commande suivante et appuyez sur `Entrée` :

```
ext install betteriutinfoaix.better-algo-papier
```

### VSCodium

Depuis [Open VSX](https://open-vsx.org/extension/betteriutinfoaix/better-algo-papier) : ouvrez le panneau des extensions (`Ctrl+Maj+X`), cherchez **Better Algo Papier** puis cliquez sur **Installer**.

### Depuis le fichier `.vsix`

1. Téléchargez le fichier `.vsix` de la dernière version sur la page [Releases](https://github.com/BetterIUTInfoAix/BetterAlgoPapier/releases/latest).
2. Dans le panneau des extensions, cliquez sur `...` en haut, puis sur **Installer à partir d'un VSIX…** et sélectionnez le fichier.

Ou en ligne de commande :

```bash
code --install-extension better-algo-papier-X.Y.Z.vsix     # VS Code
codium --install-extension better-algo-papier-X.Y.Z.vsix   # VSCodium
```

## Utilisation

Les fonctionnalités s'activent automatiquement sur tous les fichiers avec l'extension `.algo`.

Pour un fichier avec une autre extension, cliquez sur le nom du langage en bas à droite de la fenêtre (souvent `Plain Text`), puis choisissez `algo-papier` dans la liste.

## Contribuer

1. Clonez le repository et créez une branche :

   ```bash
   git clone https://github.com/BetterIUTInfoAix/BetterAlgoPapier.git
   cd BetterAlgoPapier
   git switch -c feature/ma-fonctionnalite
   ```

2. Ouvrez le dossier dans VS Code ou VSCodium et appuyez sur `F5` pour tester l'extension dans une nouvelle fenêtre.
3. Commitez, poussez votre branche et ouvrez une [Pull Request](https://github.com/BetterIUTInfoAix/BetterAlgoPapier/pulls).

Les bugs et suggestions sont les bienvenus dans les [Issues](https://github.com/BetterIUTInfoAix/BetterAlgoPapier/issues).

## Publier une nouvelle version

Le workflow GitHub Actions construit le `.vsix` et crée la Release :

```bash
gh workflow run build-and-release.yml -f tag_name=vX.Y.Z
```

## Auteurs

Développé par [BetterIUTInfoAix](https://github.com/BetterIUTInfoAix).