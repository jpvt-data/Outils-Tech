[⬅ Retour à Python](../README.md)


# **Regex - Expressions Régulières**

## Introduction aux Expressions Régulières

Une **expression régulière** (regex) est un modèle utilisé pour rechercher, extraire ou manipuler des chaînes de caractères. Elle est particulièrement efficace pour traiter des données textuelles complexes et automatiser certaines tâches. Bien que le terme français exact soit **expression rationnelle**, "expression régulière" reste couramment utilisé.

## Pourquoi utiliser les regex ?  
Imaginons que tu doives extraire toutes les dates d'un journal de bord comme :  
`Visite de contrôle : 12-04-2023, prochaine visite : 18-05-2023.`  
Avec les regex, cela devient facile et rapide, même si tu as des milliers d'enregistrements.  

Exemple simple :  

```python
import re

journal = "Visite de contrôle : 12-04-2023, prochaine visite : 18-05-2023."
dates = re.findall(r'\d{2}-\d{2}-\d{4}', journal)  # Recherche des dates au format DD-MM-YYYY
print(dates)  # ['12-04-2023', '18-05-2023']
```

---

## Le Module `re` en Python

Le module **`re`** de Python est dédié aux regex. Il permet de chercher, diviser ou modifier des chaînes de caractères avec précision.

### Fonctions principales :

1. **`re.search(motif, texte)`**  
   Vérifie la présence d'un motif dans le texte et renvoie un objet `Match` ou `None`.

   ```python
   liste_courses = "pommes poires bananes"
   resultat = re.search("poires", liste_courses)
   if resultat:
       print("Mot trouvé :", resultat.group())  # Mot trouvé : poires
   ```

2. **`re.findall(motif, texte)`**  
   Retourne toutes les correspondances du motif sous forme de liste.

   ```python
   liste_courses = "pommes oranges pommes bananes"
   fruits = re.findall("pommes", liste_courses)
   print(fruits)  # ['pommes', 'pommes']
   ```

3. **`re.split(motif, texte)`**  
   Coupe la chaîne selon le motif et renvoie une liste.

   ```python
   liste_courses = "pommes;oranges;bananes"
   segments = re.split(";", liste_courses)
   print(segments)  # ['pommes', 'oranges', 'bananes']
   ```

4. **`re.sub(motif, remplacement, texte)`**  
   Remplace toutes les occurrences du motif par une chaîne donnée.

   ```python
   liste_courses = "pommes poires bananes"
   nouveau_texte = re.sub("poires", "raisins", liste_courses)
   print(nouveau_texte)  # pommes raisins bananes
   ```

---

## Syntaxe des Regex : Métacaractères et Séquences

Les **métacaractères** et **séquences** permettent de construire des motifs complexes pour la recherche et la manipulation de chaînes de caractères. Voici une liste enrichie :

| **Caractère / Séquence** | **Description** | **Exemple** |
|--------------------------|-----------------|-------------|
| `.`                      | N'importe quel caractère sauf une nouvelle ligne | `c.t` trouve `cat`, `cut` |
| `\d`                     | Un chiffre (0-9) | `\d+` trouve `123` |
| `\D`                     | Tout sauf un chiffre | `\D+` trouve `abc` dans `abc123` |
| `\w`                     | Une lettre, un chiffre ou `_` | `\w+` trouve `hello123` |
| `\W`                     | Tout sauf une lettre, un chiffre ou `_` | `\W+` trouve `@!$` |
| `\s`                     | Un espace blanc (tab, espace, etc.) | `\s+` trouve les espaces |
| `\S`                     | Tout sauf un espace blanc | `\S+` trouve `word` dans `word  ` |
| `^`                      | Début du texte ou d'une ligne (mode multilignes) | `^The` trouve `The` au début |
| `$`                      | Fin du texte ou d'une ligne (mode multilignes) | `end$` trouve `end` à la fin |
| `*`                      | 0 ou plusieurs occurrences | `ca*` trouve `c`, `ca`, `caa` |
| `+`                      | 1 ou plusieurs occurrences | `ca+` trouve `ca`, `caa` |
| `?`                      | 0 ou 1 occurrence | `ca?` trouve `c`, `ca` |
| `{n}`                    | Exactement n occurrences | `a{2}` trouve `aa` |
| `{n,}`                   | Au moins n occurrences | `a{2,}` trouve `aa`, `aaa` |
| `{n,m}`                  | Entre n et m occurrences | `a{2,3}` trouve `aa`, `aaa` |
| `[abc]`                  | Un des caractères listés | `[aeiou]` trouve une voyelle |
| `[^abc]`                 | Aucun des caractères listés | `[^aeiou]` trouve une consonne |
| `[a-z]`                  | Une plage de caractères | `[a-z]` trouve toutes les lettres minuscules |
| `[0-9]`                  | Une plage de chiffres | `[0-9]` trouve `5` dans `a5b` |
| `\b`                     | Limite de mot (début ou fin d'un mot) | `\bcat\b` trouve `cat` uniquement |
| `\B`                     | Non-limite de mot | `\Bcat` trouve `category` mais pas `cat` |
| `|`                      | OU logique | `red|blue` trouve `red` ou `blue` |
| `()`                     | Groupe capturant | `(abc)` capture `abc` |
| `(?:)`                   | Groupe non capturant | `(?:abc)` trouve `abc` sans capturer |
| `(?=...)`                | Anticipation positive (lookahead) | `\d(?= dollars)` trouve `5` dans `5 dollars` |
| `(?!...)`                | Anticipation négative (negative lookahead) | `\d(?! euros)` trouve `5` dans `5 dollars`, mais pas dans `5 euros` |
| `(?<=...)`               | Retard positif (lookbehind) | `(?<=\$)\d+` trouve `100` dans `$100` |
| `(?<!...)`               | Retard négatif (negative lookbehind) | `(?<!\$)\d+` trouve `100` sauf s'il est précédé par `$` |
| `\`                      | Échappe un métacaractère | `\.` trouve `.` littéral |
| `[[:alpha:]]`            | Lettres (a-z, A-Z) | `[[:alpha:]]+` trouve `abc`, `XYZ` |
| `[[:digit:]]`            | Chiffres (0-9) | `[[:digit:]]+` trouve `123` |
| `[[:space:]]`            | Espaces blancs (espace, tabulation) | `[[:space:]]` trouve ` ` ou `\t` |
| `[[:punct:]]`            | Caractères de ponctuation | `[[:punct:]]` trouve `!`, `.`, `,` |
| `[[:alnum:]]`            | Alphanumérique (lettres et chiffres) | `[[:alnum:]]+` trouve `abc123` |
| `[[:xdigit:]]`           | Hexadécimal (0-9, a-f, A-F) | `[[:xdigit:]]+` trouve `3F` |

### Notes :
- Les **lookaheads** et **lookbehinds** sont particulièrement utiles pour effectuer des validations complexes sans capturer les motifs eux-mêmes.
- Les **classes POSIX** (par ex. `[[:alpha:]]`) sont compatibles dans certains outils et langages (comme `grep` ou Perl), mais nécessitent parfois une configuration spécifique dans Python.

---

## Combinaisons Avancées

1. **Groupes capturants avec `()`**  
   Utilisés pour capturer une sous-partie du motif.

   ```python
   texte = "Prix total : 120 euros."
   resultat = re.search(r"(\d+) euros", texte)
   print(resultat.group(1))  # 120
   ```

2. **Quantificateurs avancés `{n,m}`**  
   Indique un minimum et un maximum d'occurrences.

   ```python
   texte = "aaa ab aabb aaa"
   matches = re.findall(r"a{2,3}", texte)
   print(matches)  # ['aaa', 'aa', 'aaa']
   ```

---

## Ressources Utiles

- [Regex101](https://regex101.com/) : Test interactif des regex.  
- [RegexOne](https://regexone.com/) : Tutoriels pas à pas.  
- [Documentation Python](https://docs.python.org/3/library/re.html) : Tout sur le module `re`.  

---

## Conclusion

Les expressions régulières sont des outils redoutables pour la manipulation de texte. Bien qu'elles nécessitent un peu de pratique, elles permettent de gagner un temps précieux dans le traitement des données.


[⬅ Retour à Python](../README.md)