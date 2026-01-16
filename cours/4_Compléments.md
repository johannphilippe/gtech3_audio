# Compléments techniques optionnels 

## Quelques moteurs audio génériques 

1. RtAudio - API C++ - encapsulation des API des systèmes principaux 
   -  [Un exemple](https://github.com/johannphilippe/combinator3000/blob/fa45273cb1d7d953cf40ebe288ff656085a9027d/src/combinator3000.cpp#L743)
   -  [Git](https://github.com/thestk/rtaudio)
2. MiniAudio - Pareil que RTAudio, mais header only library, et avec des fonctionnalités supplémentaires (effets etc)
   - [Un exemple](https://github.com/johannphilippe/combinator3000/blob/fa45273cb1d7d953cf40ebe288ff656085a9027d/src/combinator3000.cpp#L837)
   - [Site](https://miniaud.io/)
   - [Git](https://github.com/mackron/miniaudio)
3. PortAudio - Similaire à RtAudio 
   - [Doc](https://www.portaudio.com/docs.html)
 
## Framework audio  

1. JUCE - Framework de développement Audio : standalone, plugins (etc). C'est le framework le plus utilisé dans le monde du developpement audio. Il offre la possibilité de faire des plugins, mais aussi des "hosts" audio. 
   - [JUCE website](https://juce.com/)
2. WWise - Environnement de design audio pour le jeu vidéo : on peut créer des plugins 
   - [WWise website](https://www.audiokinetic.com/fr/wwise/overview/)
   - [Create plugins](https://www.audiokinetic.com/en/public-library/2025.1.4_9062/?source=SDK&id=soundengine_plugins.html)

## Standalone environnements de programmation audio 

1. Max MSP : Environnement propriétaire de programmation graphique de graphs audio 
2. PureData : Open-source, équivalent Max MSP développé lorsque Max est passé propriétaire. 
3. Csound : langage & moteur audio doté d'une librairie exceptionnelle. API C/C++ pour embarquer Csound dans d'autres projets. 
4. Supercollider : similaire. Plus basé sur une communication réseau entre contrôle & moteur audio. 
5. ... 

## Librairies & autres 

1. Q DSP (digital signal processing) library - une librairie très bien conçue, architecture exquise, de Joel de Guzman - standardisée C++20 full STL - adaptée pour de l'embarqué
   - [Git](https://github.com/cycfi/q)
2. Libsndfile - la librairie standard pour parser / sérialiser les fichiers WAVE, AIFF, FLAC (et bien d'autres) 
   - [Site](https://libsndfile.github.io/libsndfile/)
3. Lame - Encodage décodage MP3 
   - [Site](https://lame.sourceforge.io/)
4. STK - synthesis toolkit 
   - [Git](https://github.com/thestk/stk)

## Les formats de plugins standards 

Ces formats sont admis dans la plupart des logiciels audio et DAW (Digital Audio Workstation)

- VST : multiplateforme, propriétaire Steinberg
- LADSPA & LV2 : Linux 
- AU : Apple 
- AAX : AVID
- CLAP : Multiplateforme, le potentiel successeur à tous ces formats 
