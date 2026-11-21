# Jeu de la vie

Simulation du jeu de la vie de Conway en Python 3, réalisée par le groupe 6.

## Installation

Python 3.10 ou plus récent (`lib.py` utilise la syntaxe `str | Path`) et Git suffisent pour lancer le programme : aucune bibliothèque Python externe n'est nécessaire. Les vidéos demandent en plus `ffmpeg` et Gource.

### Ubuntu ou Debian

```bash
sudo apt update
sudo apt install python3 git gource ffmpeg
```

### macOS

```bash
brew install python git gource ffmpeg
```

### Windows

Installer WSL depuis un terminal PowerShell ouvert en administrateur, redémarrer, ouvrir Ubuntu, puis taper les commandes Ubuntu ci-dessus :

```powershell
wsl --install
```

### Récupérer et vérifier le programme

```bash
git clone https://github.com/aliyanisse123-ux/git-evaluation-jeu-de-la-vie-groupe-6.git
cd git-evaluation-jeu-de-la-vie-groupe-6
python3 main.py --help
sh check_script_options.sh
sh check_tests.sh
```

## Exécution

Le programme se lance depuis la racine du dépôt. Sans grille sur l'entrée standard, il crée une grille aléatoire ; avec un pipe ou une redirection, il lit la grille reçue.

### Images avec les valeurs par défaut

```bash
$ python3 main.py
Generation of 21 images in directory outputs
$ echo $?
0
$ ls -p1 outputs | wc -l
21
```

Le dossier `outputs` contient alors `grid_0000.png` à `grid_0020.png`.

### Grille aléatoire de 50 cellules, 200 itérations, graine 4200

```bash
$ python3 main.py -n 50 -m 200 -s 4200
Generation of 201 images in directory outputs
```

### Grille lue sur l'entrée standard, sortie texte

```bash
$ cat tests/matrix3/input.txt | python3 main.py -m 1 -t text
iteration: 1
0 1 0
0 0 1
0 1 0
```

### Même grille avec les limites périodiques

```bash
$ cat tests/matrix3/input.txt | python3 main.py -m 1 -p -t text
iteration: 1
0 0 0
0 0 0
0 0 0
```

### Grille aléatoire en texte

```bash
$ python3 main.py -n 4 -s 7 -m 0 -t text
iteration: 0
1 0 1 0
0 0 1 0
0 0 0 1
1 0 0 0
```

### Erreurs

Une option invalide ou une grille mal formée affiche un message sur la sortie d'erreur et termine le programme avec un code différent de 0.

```bash
$ python3 main.py -n 0
usage: main.py [-h] [-n NB_CELLS] [-m MAX_ITERATIONS] [-s SEED]
               [-o OUTPUT_DIRECTORY] [-t {image,text}] [-p]
main.py: error: argument -n/--nb_cells: doit être strictement positif : 0
$ echo $?
2
$ printf '2\n1 2\n0 1\n' | python3 main.py -t text
Erreur : grille invalide : ligne 1 : valeur '2' différente de 0 et 1
$ echo $?
1
```

## Arguments

| Option courte | Option longue | Description | Valeur par défaut |
|---|---|---|---|
| `-n N` | `--nb_cells N` | nombre de cellules par côté d'une grille aléatoire, entier strictement positif | `10` |
| `-m N` | `--max_iterations N` | numéro de la dernière itération calculée, entier positif ou nul | `20` |
| `-s N` | `--seed N` | graine du générateur aléatoire, entier quelconque | `42` |
| `-o DOSSIER` | `--output_directory DOSSIER` | dossier où écrire les images ; il doit exister | `outputs` |
| `-t TYPE` | `--output_type TYPE` | `image` : une image PNG par génération ; `text` : la dernière génération sur la sortie standard | `image` |
| `-p` | `--periodic` | conditions aux limites périodiques (la grille se referme comme un tore) | désactivée |
| `-h` | `--help` | affiche l'aide | |

La génération initiale porte le numéro 0 : `-m 20` produit 21 générations. Quand une grille arrive sur l'entrée standard, `-n` et `-s` n'ont pas d'effet.

## Vidéos

## Auteurs

- Virapin Dhiessene 45006136
- Maillot Maenice 46008293

## Liens utiles
