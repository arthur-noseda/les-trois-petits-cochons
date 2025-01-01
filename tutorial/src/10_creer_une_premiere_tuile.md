# Créer une première tuile

Sous le nœud racine, ajouter un `Node3D`.
Mettre 0.1 pour l'ordonnée (coordonnée y).
Changer le nom du nœud pour `IShapedTile`.

Ajouter une `GridMap` à `IShapedTile`.
Configurer la `GridMap` comme précédemment (mesh library, cell, ).
Remplir les cellules comme sur la capture ci-dessous :

![](images/tile-01.png)

Nous allons maintenant programmer la réaction de la tuile aux actions du joueur.
La première étape est de mapper des actions sur des événements.

Dans la barre de menu, cliquer sur _Project_ > _Project Settings..._.

![](images/input-map-01.png)

Afficher l'onglet _Input Map_.

![](images/input-map-02.png)

Dans le champ _Add New Action_ entrer `move_left` et valider avec la touche Entrée.

![](images/input-map-03.png)

Cliquer sur le bouton _+_. 

![](images/input-map-04.png)

Appuyer sur la touche Flèche gauche du clavier (ou tout autre touche appropriée) puis cliquer sur le bouton _OK_.

![](images/input-map-05.png)

Répéter ces étapes pour mapper la touche Flèche droite sur l'action `move_right`, Flèche haut sur `move_up`, Flèche bas sur `move_down` et Clic droit sur `rotate`.
Enfin, fermer la boite de dialogue en cliquant sur le bouton _Close_.

![](images/input-map-06.png)

Avec le bouton droit de la souris, cliquer sur le nœud IShapedTile > _Attach Script..._.

![](images/first-script-01.png)

Remplacer le nom du script par `Tile.gd`.

![](images/first-script-02.png)

L'éditeur 3D est remplacé par l'éditeur de script.

![](images/first-script-03.png)

Remplacer le code proposé par celui ci-dessous.

```python
extends Node3D


# Called every frame. 'delta' is the elapsed time since the previous frame.
func _process(delta):
	if Input.is_action_just_pressed("move_left"):
		translate(Vector3.LEFT)
	if Input.is_action_just_pressed("move_right"):
		translate(Vector3.RIGHT)
	if Input.is_action_just_pressed("move_up"):
		translate(Vector3.FORWARD)
	if Input.is_action_just_pressed("move_down"):
		translate(Vector3.BACK)
	if Input.is_action_just_pressed("rotate"):
		rotate_y(deg_to_rad(90))

```

![](images/first-script-04.png)

Tester le jeu.
Pourquoi la rotation ne fonctionne-t-elle pas on le voudrait ?
Une fois le problème résolu, créer les 2 dernières tuiles (si vous êtes en panne d'inspiration, j'ai appelé les miennes `LShapedTile` et `CornerShapedTile`).
Que se passe-t-il quand le joueur agit ?