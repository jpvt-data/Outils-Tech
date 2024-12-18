# Utilisation de Pydantic pour l'analyse de données

Pydantic est une bibliothèque Python puissante pour la validation des données, offrant une syntaxe simple et des mécanismes de validation des modèles. Elle est particulièrement utile pour un data analyst lorsqu'il doit gérer des données non structurées, des valeurs manquantes ou des erreurs dans les données. Cette fiche technique présente les concepts clés de l’utilisation de Pydantic, avec des exemples pratiques pour faciliter l’intégration dans un workflow d’analyse de données.

---

## 1. Introduction à Pydantic

Pydantic permet de définir des modèles de données avec des contraintes de validation sur les types de données. Elle est utilisée pour garantir que les données manipulées respectent une structure et des types définis, évitant ainsi les erreurs de type courantes.

```python
from pydantic import BaseModel

class Utilisateur(BaseModel):
    id: int
    nom: str
    age: int
```

Dans cet exemple, `Utilisateur` est un modèle qui garantit que les données fournies respectent les types `int` pour `id` et `age`, et `str` pour `nom`.

## 2. Validation et Gestion des Erreurs

Pydantic valide automatiquement les données lors de la création des instances de modèle. Si les données sont incorrectes, une exception `ValidationError` est levée.

```python
from pydantic import ValidationError

try:
    utilisateur = Utilisateur(id='abc', nom="Jean", age=25)
except ValidationError as e:
    print(e)
```

Dans cet exemple, une erreur est générée car `id` n'est pas un entier, ce qui entraîne une exception.

## 3. Valeurs par défaut et gestion des données manquantes

Il est fréquent que certaines données soient manquantes. Pydantic permet de gérer ces cas avec des valeurs par défaut et des champs optionnels.

```python
from pydantic import BaseModel, Field
from typing import Optional

class DonneesSondage(BaseModel):
    id: int
    question: str
    reponse: Optional[str] = None
    score: float = Field(default=0.0, ge=0.0, le=10.0)
    commentaire: str = ""

# Exemple d'utilisation
sondage_complet = DonneesSondage(id=1, question="Êtes-vous satisfait ?", reponse="Oui", score=8.5)
sondage_partiel = DonneesSondage(id=2, question="Recommanderiez-vous notre service ?")

print(sondage_complet)
print(sondage_partiel)
```

**Explications :**
- **`Optional[str]`** : La réponse peut être une chaîne ou `None`.
- **`Field(default=0.0, ge=0.0, le=10.0)`** : Valeur par défaut avec contraintes sur la plage de valeurs.
- **`commentaire: str = ""`** : Valeur par défaut vide.

## 4. Modèles imbriqués et listes

Pydantic supporte les modèles imbriqués et les listes, ce qui est très utile pour structurer des données complexes.

```python
from pydantic import BaseModel
from typing import List, Dict

class Adresse(BaseModel):
    rue: str
    ville: str
    code_postal: str

class HistoriqueAchat(BaseModel):
    date: str
    montant: float
    produits: List[str]

class ClientComplet(BaseModel):
    id: int
    nom: str
    adresses: List[Adresse]
    historique_achats: List[HistoriqueAchat]
    preferences: Dict[str, float]

# Exemple d'utilisation
client_data = {
    "id": 3,
    "nom": "Charlie Brown",
    "adresses": [{"rue": "123 Rue Principale", "ville": "Paris", "code_postal": "75001"}],
    "historique_achats": [{"date": "2023-03-15", "montant": 150.75, "produits": ["Livre", "DVD"]}],
    "preferences": {"Électronique": 0.8, "Livres": 0.6, "Vêtements": 0.4}
}

client_complet = ClientComplet(**client_data)
print(client_complet)
```

**Explications :**
- **Modèles imbriqués** : `Adresse` et `HistoriqueAchat` sont des sous-modèles utilisés dans `ClientComplet`.
- **`List[Adresse]` et `List[HistoriqueAchat]`** : Listes d'objets respectivement des modèles `Adresse` et `HistoriqueAchat`.
- **`Dict[str, float]`** : Un dictionnaire représentant les préférences avec des clés de type `str` et des valeurs de type `float`.

## 5. Intégration de Pydantic avec Pandas

Pydantic peut être utilisé pour valider les données avant de les charger dans un DataFrame Pandas. Cela permet de s'assurer que seules les données valides sont utilisées pour l'analyse.

```python
import pandas as pd
from pydantic import BaseModel, Field, ValidationError, field_validator
from typing import List
from datetime import date

class Vente(BaseModel):
    date: date
    produit_id: int
    quantite: int = Field(gt=0)
    prix_unitaire: float = Field(gt=0)
    
    @field_validator('prix_unitaire')
    @classmethod
    def arrondir_prix(cls, v: float) -> float:
        return round(v, 2)

def valider_donnees_ventes(donnees_brutes: List[dict]) -> List[Vente]:
    ventes_validees = []
    erreurs = []

    for idx, donnee in enumerate(donnees_brutes):
        try:
            vente = Vente.model_validate(donnee)
            ventes_validees.append(vente)
        except ValidationError as e:
            erreurs.append(f"Erreur à la ligne {idx+1}: {e}")

    if erreurs:
        print("Erreurs de validation détectées:")
        for erreur in erreurs:
            print(erreur)

    return ventes_validees

# Exemple de données brutes
donnees_brutes = [
    {"date": "2023-08-01", "produit_id": 1, "quantite": 5, "prix_unitaire": 10.99},
    {"date": "2023-08-02", "produit_id": 2, "quantite": -1, "prix_unitaire": 15.50},  # Erreur : quantité négative
    {"date": "2023-08-03", "produit_id": 3, "quantite": 3, "prix_unitaire": 0},  # Erreur : prix nul
    {"date": "2023-08-04", "produit_id": 4, "quantite": 2, "prix_unitaire": 20.005},
]

# Validation des données
ventes_validees = valider_donnees_ventes(donnees_brutes)

# Création du DataFrame avec les données validées
df_ventes = pd.DataFrame([v.model_dump() for v in ventes_validees])
print(df_ventes)
```

**Explications :**
- **`field_validator`** : Utilisé pour arrondir le prix à deux décimales.
- **Validation des données** : Chaque vente est validée et les erreurs sont collectées.
- **Pandas** : Les données validées sont ensuite converties en DataFrame.

## 6. Cas pratique : Analyse de données de ventes

Voici un cas complet où Pydantic est utilisé pour valider les données de ventes avant d'analyser et de visualiser les données avec Pandas et Matplotlib.

```python
from pydantic import BaseModel, field_validator, Field, model_validator
from typing import List
from datetime import date
import pandas as pd
import matplotlib.pyplot as plt

class Produit(BaseModel):
    id: str = Field(..., pattern=r'^P\d{4}$')
    nom: str
    categorie: str
    prix: float = Field(..., gt=0)

class Client(BaseModel):
    id: str = Field(..., pattern=r'^C\d{6}$')
    nom: str
    email: str
    date_inscription: date

class Vente(BaseModel):
    id: str = Field(..., pattern=r'^V\d{8}$')
    date: date
    produit: Produit
    client: Client
    quantite: int = Field(..., gt=0)
    montant_total: float

    @model_validator(mode='after')
    def verifier_montant_total(self) -> 'Vente':
        montant_calcule = round(self.produit.prix * self.quantite, 2)
        if abs(self.montant_total - montant_calcule) > 0.01:
            raise ValueError(f"Le montant total {self.montant_total} ne correspond pas au calcul {montant_calcule}")
        return self

    @field_validator('date')
    @classmethod
    def date_non_future(cls, v: date) -> date:
        if v > date.today():
            raise ValueError("La date de vente ne peut pas être dans le futur")
        return v
```
---

## Résumé

Pydantic est un excellent outil pour la validation et la structuration des données, particulièrement utile dans des projets d'analyse de données. Elle garantit la conformité des types et la gestion des erreurs, facilitant ainsi l'intégration des données provenant de diverses sources.
