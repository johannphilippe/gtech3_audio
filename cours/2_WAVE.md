# Fichiers de stockage audio 

## Types de fichiers 

On distingue deux grands types de fichiers audio : avec ou sans compression. 

### Sans compression 

1. WAVE : format PCM, conteneur générique, le plus répandu. Little endianness. 
2. AIFF : Format développé par Apple, peu utilisé (sauf sur OSX), avec la feature de pouvoir insérer des points de bouclage & des notes d'échantillons (pour des raisons qui datent, l'utilisation avec des sampleurs etc...). Big endianness. 

Le PCM (Pulse code modulation) désigne une manière de stocker les échantillons audio les uns après les autres, garantissant le stockage de tous les échantillons d'un signal. 
Si cela semble évident et trivial, c'est une caractéristique des formats non-compressés. 

### Avec compression 

1. MP3 : le Mpeg - audio layer 3 : format compressé avec perte. Offre la possibilité de spécifier un bitrate constant (Constant Bit Rate), 64kb/s, 128, 256 etc, mais aussi de laisser l'algorithme déterminer un bitrate évolutif (VBR Variable Bit Rate ou ABR Average Bit Rate). Ce format est destructif. Facile à encapsuler dans du MPEGG 4. Intéressant de noter que les principes d'origine du MP3 datent du début du XXème siècle, lorsque les laboratoires BELL oeuvraient à réduire le coût de la bande passante pour les télécommunications. Il s'agit d'un gros travail de psychoacoustique : qu'est-ce qui, dans un signal vocal, est vraiment nécessaire pour qu'on puisse comprendre l'information ? 
2. FLAC : Free Lossless Audio Codec : Format compressé sans perte, taux de compression d'environs 50%. 

Il existe beaucoup d'autres formats. 

## Quelques librairies 

La grande librairie de parsing / sérialisation de fichiers audio est libsndfile (API C & C++) : 
- [Github](https://github.com/libsndfile/libsndfile)
- [Documentation](https://libsndfile.github.io/libsndfile/)
Elle supporte les formats WAV, AIFF, Raw PCM sans header, IRCAM SF, FLAC et plein d'autres formats (de niche, ou obsolètes pour la plupart). 

Pour le MP3, la compression est un peu plus complexe et spécifique, on utilise Lame : 
- [Documentation](https://lame.sourceforge.io/)

Ce sont les deux grandes références du C/C++. Il n'existe pas d'équivalent connu & à ce niveau. 

## Le format WAVE

Le WAVE (.wav) est le grand gagnant des formats audio non-compressés. 
Ses caractéristiques : 
- PCM 
- Support PCM int & float 
- Résolution binaire de 8 à 32 bits 
- Multicanal 
- 4Go max (taille des 4 bytes utilisés pour définir la taille)

Il est composé en trois parties : 
- Un header
  - 4B : 'RIFF'
  - 4B : File size
  - 4B : 'WAVE'
- Un format
  - 4B : 'fmt '
  - 4B : Format size 
  - 2B : Format tag : 0x0001 pour PCM entier, 0x0003 pour PCM flottant (les autres sont des formats compressés et/ou obsolètes de windows WAVE_FORMAT_EXTENSIBLE)
  - 2B : Number of channels
  - 4B : Sample rate
  - 4B : Data Rate (number of bytes / sec)
  - 2B : Size in bytes of one audio frame (1 sample for each channel)
  - 2B : Bits per sample
  - Optionnal (we won't use it : extension for WAVE_FORMAT_EXTENSIBLE)
- Un nombre indéfini de blocs de données 
  - Chaque bloc a la forme suivante 
    - 4B : Data name (for audio data, it will be 'data')
    - 4B : Size of data in bytes 
    - NB : Data (interleaved for audio)

[Specification WAVE](https://web.archive.org/web/20100325183246/http://www-mmsp.ece.mcgill.ca/Documents/AudioFormats/WAVE/WAVE.html)

Attention, sur cette spécification, certaines informations sont datées (concernant le WAVE_FORMAT_EXTENSIBLE). Il n'est pas nécessaire de l'utiliser pour les fichiers de plus de 2 canaux, ni pour les données de plus de 16 bits/sample. 
En fait, on ne l'utilise généralement pas, sauf dans certains cas spécifiques (communication avec des appareils de capture audio spécifiques par exemple). 

## Exercice 

1. Réaliser un parser de fichier WAVE 
   - Avec méthodes `seek(int num_frame)` et `read(char *data, int num_frames)` (les signatures sont données en exemple, vous êtes libres de ce point de vue)
   - Possibilité de convertir les données (si le fichier contient des PCM16 bits, et que le client veut du float 32 bits normalisé par exemple)

2. Réaliser un sérializer de fichier WAVE 
   - Peut écrire des fichiers audio à partir d'une spécification de paramètres (nombre de canaux, fréquence d'échantillonnage, format audio, résolution binaire etc) et de données audio fournies par l'utilisateur 
   - Méthodes `write(char* data, size_t num_frames)` (exemple)
   - Optionnel : méthode `write_meta(std::string name, size_t size_bytes, void* data)` pour ajouter des métadonnées dans un bloc de données supplémentaire 

3. Réaliser un outil en ligne de commande pour transformer des fichiers audio 
   - Couper un fichier (spécifier le début et la fin)
   - Modifier l'amplitude
   - Appliquer une évolution progressive du volume (courbe/enveloppe d'amplitude)
   - Modifier l'encodage : int <> float & modification de résolution binaire 
   - Gestionnaire de panoramique (stéréo gauche/droite)
   - Modulation d'amplitude par oscillateur à basse fréquence (LFO sinusoidal, PWM)
   - Autre, libre...


