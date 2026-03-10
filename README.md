# UniStudent Manager
 est une application de bureau développée en **Python** permettant de gérer les étudiants, les évaluations et les notes au sein d'un établissement universitaire. Elle offre une interface graphique simple et intuitive, sans aucune dépendance externe.

---

## Fonctionnalités

### 👨‍🎓 Gestion des étudiants
- Ajouter un étudiant avec les champs suivants : **CNE**, **Nom**, **Prénom**, **Groupe**, **Filière** et **Email**
- Modifier les informations d'un étudiant en le sélectionnant dans le tableau
- Supprimer un étudiant (ses notes sont automatiquement supprimées)
- Rechercher un étudiant par CNE, nom ou groupe

### 📝 Gestion des évaluations
- Créer une évaluation de type **Examen** ou **Projet**
- Définir un **titre**, une **date**, un **coefficient** et une **note maximale** personnalisée
- Supprimer une évaluation (les notes associées sont automatiquement supprimées)

### 🏆 Saisie des notes
- Sélectionner un étudiant et une évaluation via des listes déroulantes
- Saisir une note entre **0 et 20**
- Si une note existe déjà pour cet étudiant et cette évaluation, elle est automatiquement **mise à jour**
- Supprimer une note existante

### 📊 Tableau de bord statistique
- Nombre total d'étudiants inscrits
- **Moyenne générale de la classe** (pondérée par les coefficients)
- **Taux de réussite** (étudiants avec une moyenne ≥ 10/20)
- **Top 5** des meilleurs étudiants avec mention (Très bien, Excellent)
- Liste des **étudiants à risque** (moyenne < 10/20)

### 💾 Import / Export JSON
- Exporter l'intégralité des données (étudiants, évaluations, notes) dans un fichier `.json`
- Importer un fichier `.json` pour restaurer ou transférer les données

---

## 🗂️ Structure du projet

```
UniStudentManager/
├── App.py        # Interface graphique (Tkinter)
├── models.py     # Modèles de données et logique SQLite (Student, Evaluation, Grade, Database)
├── university.db # Base de données SQLite générée automatiquement au premier lancement
└── README.md
```

---

## 🗃️ Base de données

La base de données SQLite est créée automatiquement à la première exécution. Elle contient trois tables :

| Table         | Description                                              |
|---------------|----------------------------------------------------------|
| `students`    | Informations des étudiants (CNE, nom, prénom, groupe…)   |
| `evaluations` | Évaluations avec leur type, coefficient et note maximale |
| `grades`      | Notes par étudiant et par évaluation                     |

> La contrainte `UNIQUE(student_id, evaluation_id)` dans la table `grades` garantit qu'un étudiant ne peut avoir qu'une seule note par évaluation.

---

## ⚙️ Calcul de la moyenne

La moyenne d'un étudiant est calculée de la façon suivante :

```
Moyenne = Σ (note_sur_20 × coefficient) / Σ coefficients
```

Si la note maximale d'une évaluation est différente de 20, la note est d'abord ramenée sur 20 avant le calcul.

---

## 🚀 Lancement

### Prérequis

- Python 3.x (Tkinter est inclus par défaut)

### Exécution

```bash
python App.py
```

> Aucune installation de bibliothèque externe n'est requise.

---

## 🛠️ Technologies utilisées

| Technologie  | Rôle                                              |
|--------------|---------------------------------------------------|
| **Python 3** | Langage principal                                 |
| **Tkinter**  | Interface graphique native (incluse avec Python)  |
| **SQLite3**  | Base de données locale embarquée                  |
| **JSON**     | Format d'import/export des données                |
