# Détail du contenu du groupe "analysis" des fichers h5

TODO: La même transformation doit être effectués sur les audio de prédiciton, pour tester la feature extraction

- reprendre l'audio d'une musique présent dans le dataset
- effectuer la feature extraction
- comparer les résultats obtenus avec les datas présentes dans le dataset

=> "The main audio features are 'segments_pitches' and 'segments_timbre'." !!!

<u>Confidence values</u>

TODO: Faire des boîtes à moustache pour visualiser la précision / pertinence de la feature correspondante. Pour le total (toutes les musiques). Et unique !

<u>Analyse rythmique</u>

- `bars_start` : Début d'une mesure. Vecteur contenant le temps (sec) où chaque nouvelle mesure commence.
- `beats_start` : Vecteur contenant le temps (sec) de chaque battement.
- `sections_start` : Vecteur contenant le temps (sec) du debut de chaque nouvelle sections(couplet, refrains, pont,...).
- `tatums_start` : Vecteur contenant le temps (sec) du debut de chaque 'tatums', subdivision rythmique plus fine que le battement.
- `segments_start` : Vecteur contenant le temps (sec) du debut de segments ?

<u>Autre</u>

- `segments_loudness_max` : Vecteur contenant la "max dB value" pour chaque segments ATTENTION loudness (perception) != volume
- `segments_loudness_max_time` : Vecteur contenant le temps ou la "max dB value" est atteinte pour chaque segments
- `segments_loudness_start` : Pas présent pour toutes les musiques !!! valeur en décibels au début du segment

<u>Analyse mélodique et harmonique</u>

- `segments_pitches` : Matrice (k \* 12) => k: nombre de segments ; 12: hauteurs de notes possibles dans la musique occidentale ; valeurs (0 à 1) => % ? correspond à la présence / intensité de la hauteurs de notes dans le segments
- `segments_timbre` : Matrice (k \* 12 ) => k: nombre de segments ; 12: coefficients timbraux extraits de chaque segment (ici il y en 12) ; la valeur correspond au resultat de la transformation (MFCC+PCA-like)

## Conclusion

Pour avoir une bonne prédiction (avec un modèle ou une combinaison de pls modèles) il faudrait pouvoir entrainer sur les diff caractéristiques qui compose une musique via:

- une analyse structurelle
  - sections
- une analyse rythmique
  - bars
  - beats
  - tatums
  - segments
  - tempo (songs)
  - dynamique (variation de volumes) récup depuis `segments_loudness` ?!
- une analyse mélodique et harmonique

  - texture => `segments_timbre`
  - `segments_pitches`

- loudness(songs) ?
- end_of_fade_in(songs) ?
- start_of_fade_out(songs) ? => plutot utiliser duration - start_of_fade_out = fade_out_to_end ?!

Pour n'utiliser qu'un seul modèle: (forcement mauvaise idée ??!?)
=> ne pas utiliser un vecteur ni une MATRICE mais un TENSOR avec n dimensions (n = nombre de features)
TODO: Vérif si POSSIBLE avec pls dimensions de diff shape
=> pas vraiment en l'état toute les shapes doivent êtres les mêmes !!

Diff shapes à exploiter:

scalaire => ex: `tempo`
vecteur => ex: `segments_loudness_max`
matrix => ex: `segments_pitches`

Tout transformer en matrice ?? Pertinence ?

Grouper les informations par format ? Matrice ensemble, vecteur ensemble ? Interêt ? Impact ?
