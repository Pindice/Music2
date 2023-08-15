# Détail du contenu du groupe "analysis" des fichers h5

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

- `segments_loudness_max` : Vecteur contenant la "max dB value" pour chaque segments
- `segments_loudness_max_time` : Vecteur contenant le temps ou la "max dB value" est atteinte pour chaque segments

<u>Analyse mélodique et harmonique</u>

- `segments_pitches` : Matrice (k \* 12) => k: nombre de segments ; 12: hauteurs de notes possibles dans la musique occidentale ; valeurs (0 à 1) => % ? correspond à la présence / intensité de la hauteurs de notes dans le segments
