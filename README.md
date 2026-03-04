# 🕹️ Basic Thomson → Python 3

> *"40 ans de programmation. Même passion. Moins de numéros de ligne."*


---

```
DATE: 02-03-26                               RAM: 512K
      1 BASIC 512 MICROSOFT 1.0              ████ B
      2 BASIC MICROSOFT 1.0                  ████ C
      3 Réglage et préférences
      4 Appel de programme                   ████ E
      5 Exploitation de fichiers
```

> *Tu te souviens de cet écran ? Ce repo est fait pour toi.*

---

## 🤔 C'est quoi ce projet ?

Ce dépôt contient des **ressources pédagogiques** pour apprendre (ou réapprendre) à programmer, en partant du **Basic Thomson des années 80** pour arriver à **Python 3** — le langage le plus utilisé au monde en 2026.
L'idée est simple : si tu as déjà tapé :
#
**10 PRINT "BONJOUR"** sur un Thomson MO5, MO6, T07, TO8, TO9, tu sais déjà programmer. Il te manque juste la nouvelle syntaxe.

**Spoiler :** **PRINT** devient **print()**. Tu survivras.

---

## 📂 Contenu du dépôt

```
📁 thomson-basic-python/
├── 📄 README.md                    ← tu es ici
├── 📄 Mode_Operatoire.pdf          ← émulateur dcmoto + sauvegarde disquette
├── 📄 Vers_Python3.pdf             ← guide de migration Basic → Python 3
├── 📁 programmes_basic/
│   ├── CADENAS.txt                 ← jeu du cadenas (Basic, 1986)
│   └── PROGRAM1.txt                ← programme de démonstration
└── 📁 programmes_python/
    └── cadenas.py                  ← même jeu, en Python 3 (2026)
```

---

## ⚡ Démarrage rapide

### Option A — Retour en 1986 (émulateur Thomson)

```bash
1. Télécharger dcmoto sur https://dcmoto.pages-perso.free.fr/
2. Créer le dossier de travail ► D:\TO8\ ou D:\TO8\ ou tout autre emplacement de ton choix (j'ai choisi le TO8)
3. Créer une disquette virtuelle avec DCFDUTIL ► (format DD 80 pistes .fd — standard du TO8)
4. Dans dcmoto : Supports amovibles → monter vierge.fd
5. Dans le Basic Thomson :

DSKINI0
SAVE"MONPROG"
RUN
```

### Option B — Bienvenue en 2026 (Python 3)

```bash
# Vérifier l'installation
python --version   # doit afficher Python 3.x.x

# Lancer le jeu du cadenas
python cadenas.py
```

> 💡 **Pas encore Python ?** → https://python.org ou https://thonny.org/

---

## 🔄 Correspondances Basic → Python 3

Les concepts n'ont pas changé en **40 ans**. Seule l'écriture a évolué.

| Ce que tu faisais en Basic |Ce que tu fais en Python |
|---|---|
| `10 PRINT "Bonjour"` | `print("Bonjour")` |
| `20 INPUT "Nom";A$` | `a = input("Nom : ")` |
| `30 IF A>5 THEN GOTO 100` | `if a > 5:` + indentation |
| `40 FOR I=1 TO 10` | `for i in range(1, 11):` |
| `50 NEXT I` | *(l'indentation suffit)* |
| `60 WHILE cond ... WEND` | `while cond:` |
| `70 GOSUB 500` | `def ma_fonction():` |
| `80 DIM C(4)` | `c = []` ou `c = [0, 0, 0, 0]` |
| `90 NOM$ = "Thomson"` | `nom = "Thomson"` *(plus de `$` !)* |
| `100 GOTO 20` | *(n'existe pas — c'est voulu)* |
| `SAVE"MONPROG"` | `# le fichier .py est déjà sauvegardé` |

### ⚠️ Les 3 pièges classiques

```python
# Piège 1 — Tester l'égalité
a = 5          # affectation ► (Basic : A = 5)
if a == 5:     # comparaison ► (Basic : IF A = 5)
    ...

# Piège 2 — Les listes commencent à 0, pas à 1 !
c = [5, 3, 8, 1]
print(c[0])    # affiche 5 ► (Basic : C(1) était le premier)
print(c[1])    # affiche 3 ► (Basic : C(2))

# Piège 3 — input() retourne toujours du texte
age = int(input("Votre âge : "))    # conversion obligatoire en entier
prix = float(input("Prix : "))      # conversion obligatoire en décimal
```

---

## 🎮 Exemple — Le Jeu du Cadenas

Le projet : le **Jeu du Cadenas**, créé en **Basic Thomson en 1986**, réécrit en **Python 3 en 2026**. Même logique, **40 ans** d'écart.

**Basic Thomson (1986) — 100 lignes de numéros :**
```basic
10  CLS
20  PRINT "BIENVENUE DANS LE JEU DU CADENAS !"
150 E=10
170 FOR J=1 TO 4
180 A=INT(RND(1)*10)
190 FOR K=1 TO J-1
200 IF C(K)=A THEN 180       ← GOTO caché dans un IF
...
640 INPUT "ENTRE 4 CHIFFRES : "; G$
880 PRINT "==> BIEN PLACES : ";BP
890 PRINT "==> MAL PLACES  : ";MP
930 REM *** PERDU ***
980 REM *** GAGNE ***
```

**Python 3 (2026) — fonctions lisibles en 80 lignes seulement :**
```python
import random

def generer_combinaison():
    return random.sample(range(10), 4)   # fini, les boucles FOR imbriquées

def evaluer_guess(combinaison, guess):
    bien_places = sum(g == c for g, c in zip(guess, combinaison))
    mal_places  = sum(g in combinaison for g in guess) - bien_places
    return bien_places, mal_places

def main():
    combinaison = generer_combinaison()
    essais = 10
    while essais > 0:
        guess = input("Entrez 4 chiffres différents ► ")
        # ... validation et évaluation
        essais -= 1
```

*Même logique. Aucun `GOTO`. Beaucoup plus lisible.*

---

## 🛠️ Prérequis

| Outil | Version | Usage |
|---|---|---|
| [dcmoto](https://dcmoto.pages-perso.free.fr/) | 2026.01.14 | Émulateur Thomson (TO7, TO8, MO5...) |
| [DCFDUTIL](https://dcmoto.pages-perso.free.fr/) | 2025.06.27 | Gestion des disquettes virtuelles `.fd` |
| [Python](https://python.org) | 3.8+ | Programmation moderne |
| [IDLE](https://docs.python.org/fr/3/library/idle.html) | fourni avec Python | Éditeur de départ |

> 🖥️ **OS :** Windows 11 recommandé pour dcmoto.  
> ⚠️ Si la version 64 bits de dcmoto ne fonctionne pas → basculer sur la version 32 bits.

---

## 📖 Antisèche — Commandes Basic 512 Thomson 

```basic
REM ── AFFICHAGE ───────────────────────────────
PRINT "texte"           ' afficher du texte
PRINT "valeur =";A      ' afficher une variable
CLS                     ' effacer l'écran
COLOR n,m               ' couleur texte(n) et fond(m)
LOCATE x,y              ' positionner le curseur

REM ── SAISIE ──────────────────────────────────
INPUT "message";A       ' saisie numérique
INPUT "message";A$      ' saisie texte

REM ── CONTRÔLE ─────────────────────────────────
IF cond THEN ...        ' condition
GOTO n                  ' saut (à éviter !)
GOSUB n / RETURN        ' sous-programme
FOR i=1 TO 10 / NEXT i  ' boucle comptée
WHILE cond / WEND       ' boucle conditionnelle

REM ── GRAPHISME ────────────────────────────────
LINE (x1,y1)-(x2,y2)   ' tracer une ligne
CIRCLE (x,y),r          ' tracer un cercle
PSET (x,y)              ' allumer un pixel

REM ── SON ─────────────────────────────────────
PLAY "notes"            ' jouer une mélodie
SOUND f,d               ' son de fréquence f, durée d

REM ── DISQUETTE ────────────────────────────────
DSKINI0                 ' initialiser le lecteur 0
SAVE"MONPROG"           ' sauvegarder sur disquette
LOAD"MONPROG"           ' charger depuis la disquette
DIR                     ' lister les fichiers
NEW                     ' effacer la mémoire
LIST                    ' afficher le programme
RUN                     ' exécuter
```

---

## 🚀 Session de travail type

```
# Avant (1986, Thomson TO8)              # Aujourd'hui (Python 3)
──────────────────────────────           ─────────────────────────────────
1. Allumer le Thomson                    1. Ouvrir le terminal (ou IDLE)
2. Attendre le démarrage...              2. cd mon_dossier/
3. Attendre encore...                    3. Ouvrir cadenas.py
4. Taper son programme ligne/ligne       4. Écrire le code (sans numéros !)
5. DSKINI0 (première utilisation)        5. Ctrl+S pour sauvegarder
6. SAVE                                  6. F5 pour exécuter
7. RUN ou RUN                            7. Résultat immédiat ✓
8. Disquette qui tourne... (320 Ko).

Pire pour les MO5, TO7, TO7-70,
le temps qu'il fallait pour ouvrir ou
enregistrer un programme sur cassette.
```

---

## 🎯 Ce que Python a gardé du Basic

- Les variables (`a = 5`)
- `print()` et `input()`
- Les boucles `for` et `while`
- Les conditions `if / else`
- Les tableaux (devenus des listes)
- La logique séquentielle ligne par ligne

## 🆕 Ce que Python apporte en plus

- Des **fonctions** vraiment puissantes (`def`) — exit le `GOSUB` limité
- Des **f-strings** : `f"Bonjour {nom}, tu as {age} ans"` — fini la concaténation laborieuse
- Des **modules** : `import random`, `import math`, `import datetime`...
- L'accès à tout l'écosystème Python : IA, data, web, automatisation

---

## 🧑‍🏫 Public cible

- 👴 Quinquagénaires nostalgiques ayant possédé un Thomson MO5, MO6, TO7, TO7-70, TO8, TO8D, TO9, TO9+ 
- 🎓 Élèves de lycée découvrant la programmation via l'histoire de l'informatique  
- 🤓 Curieux qui veulent comprendre pourquoi Python a banni `GOTO`
- 👨‍💻 Tout le monde — parce que la logique de la programmation n'a pas d'âge

---

> *"J'ai possédé un Thomson TO8 en 1986. Il tourne encore dans dcmoto.  
> Certaines choses ne vieillissent pas — dont la curiosité de programmer."*

---

## 📜 Licence

Ressources pédagogiques libres — utilisez, adaptez, partagez.  
#
👤 Auteur : SERRES Régis - Lycée E de Constant, La Flèche (72) - https://serres-regis-prof-estournelles.github.io/
