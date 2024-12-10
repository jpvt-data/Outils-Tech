## **Python - Regex (partie 1) Expressions Régulières**

### Introduction aux Expressions Régulières

Une **expression régulière** (regex) est un motif utilisé pour rechercher, identifier ou manipuler des chaînes de caractères. Elle est particulièrement utile pour extraire des informations précises ou valider des formats dans des données textuelles. Bien que le terme français correct soit **expression rationnelle**, l'usage courant conserve "expression régulière".

#### Pourquoi utiliser les regex ?
Prenons l'exemple d'un projet où il faut extraire tous les millésimes d’une liste de noms de vins, comme dans :  
`Domaine Marcel Deiss 2016 Pinot Gris (Alsace)`.  
Les regex permettent de faire cela efficacement, même avec des milliers d'entrées. 

Exemple simple :  

```python
import re

vin = "Domaine Marcel Deiss 2016 Pinot Gris (Alsace)"
millésime = re.findall(r'\d{4}', vin)  # Recherche une suite de 4 chiffres
print(millésime)  # ['2016']
```

---

### Le Module `re` en Python

Python fournit le module intégré **`re`** pour travailler avec les expressions régulières. Il contient plusieurs fonctions utiles pour effectuer des recherches, des substitutions ou des validations dans des chaînes de caractères.

#### Fonctions principales :

1. **`re.search(motif, texte)`**  
   Vérifie si un motif apparaît au moins une fois dans le texte. Renvoie un objet `Match` ou `None`.

   ```python
   fournitures = "cahier stylo crayon"
   resultat = re.search("stylo", fournitures)
   if resultat:
       print("Mot trouvé :", resultat.group())  # Mot trouvé : stylo
   ```

2. **`re.findall(motif, texte)`**  
   Renvoie une liste de toutes les occurrences correspondant au motif.

   ```python
   fournitures = "stylo cahier crayon stylo"
   mots = re.findall("stylo", fournitures)
   print(mots)  # ['stylo', 'stylo']
   ```

3. **`re.split(motif, texte)`**  
   Sépare le texte en segments selon le motif fourni.

   ```python
   fournitures = "stylo, cahier, crayon"
   segments = re.split(", ", fournitures)
   print(segments)  # ['stylo', 'cahier', 'crayon']
   ```

4. **`re.sub(motif, remplacement, texte)`**  
   Remplace les occurrences du motif par une chaîne donnée.

   ```python
   fournitures = "stylo cahier crayon"
   nouveau_texte = re.sub("stylo", "plume", fournitures)
   print(nouveau_texte)  # plume cahier crayon
   ```

---

### Syntaxe des Regex : Métacaractères et Séquences

Les **métacaractères** permettent de définir des motifs complexes. Voici les principaux :

| **Caractère** | **Description** | **Exemple** |
|---------------|----------------|-------------|
| `.`           | N'importe quel caractère sauf une nouvelle ligne | `c.t` trouve `cat`, `cut` |
| `\d`          | Un chiffre (0-9) | `\d+` trouve `123` |
| `\w`          | Une lettre, un chiffre ou `_` | `\w+` trouve `hello123` |
| `\s`          | Un espace blanc (tab, espace, etc.) | `\s+` trouve les espaces |
| `^`           | Début du texte | `^The` trouve `The` au début |
| `$`           | Fin du texte | `Moon.$` trouve `Moon` à la fin |
| `*`           | 0 ou plusieurs occurrences | `ca*` trouve `c`, `ca`, `caa` |
| `+`           | 1 ou plusieurs occurrences | `ca+` trouve `ca`, `caa` |
| `{n}`         | Exactement n occurrences | `a{2}` trouve `aa` |
| `[abc]`       | Un des caractères listés | `[aeiou]` trouve une voyelle |
| `|`           | OU logique | `red|blue` trouve `red` ou `blue` |
| `\`           | Échappe un métacaractère | `\.` trouve `.` littéral |

---

### Combinaisons Avancées

1. **Groupes de motifs avec `()`**  
   Permet de capturer des sous-motifs.

   ```python
   texte = "Le coût est de 150 euros."
   resultat = re.search(r"(\d+) euros", texte)
   print(resultat.group(1))  # 150
   ```

2. **Quantificateurs avancés `{n,m}`**  
   Spécifie un nombre minimum et maximum d'occurrences.

   ```python
   texte = "aa ab aabb aaa"
   matches = re.findall(r"a{2,3}", texte)
   print(matches)  # ['aa', 'aaa']
   ```

---

### Ressources Utiles

- [Regex101](https://regex101.com/) : Test interactif des regex.
- [Regex Crossword](https://regexcrossword.com/) : Apprendre les regex en jouant.
- [Python Documentation](https://docs.python.org/3/library/re.html) : Module `re`.

---

### Conclusion

Les expressions régulières sont un outil puissant pour manipuler des données textuelles. Leur apprentissage demande de la pratique, mais elles offrent un gain de temps immense pour extraire, valider ou transformer des informations.