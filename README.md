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

## Arguments

## Vidéos

### Simulation du jeu de la vie

Vidéo : <lien YouTube public de la simulation>

Grille de 50 cellules par côté, graine 4200, limites fixes, 2001 générations assemblées à 20 images par seconde (100 secondes). Commandes exactes, depuis la racine du dépôt :

```bash
mkdir -p outputs/video-seed-4200
python3 main.py --nb_cells 50 --max_iterations 2000 --seed 4200 \
  --output_type image --output_directory outputs/video-seed-4200
ffmpeg -y -framerate 20 -start_number 0 \
  -i outputs/video-seed-4200/grid_%04d.png -frames:v 2001 \
  -c:v libx264 -pix_fmt yuv420p -movflags +faststart \
  outputs/video-seed-4200/game-of-life-g6.mp4
```

### Historique du dépôt (Gource)

Vidéo : <lien YouTube public de la vidéo Gource>

```bash
gource -s 2 -r 60 --file-font-size 8 \
  --title 'Jeu de la vie' --filename-time 2 \
  --stop-at-end --hide date,usernames -o - | \
ffmpeg -y -r 60 -f image2pipe -vcodec ppm -i - \
  -vcodec libx264 -preset medium -pix_fmt yuv420p \
  -crf 18 -threads 0 -bf 0 gource.mp4
```

## Auteurs

- Virapin Dhiessene 45006136

## Liens utiles
