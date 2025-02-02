---
title       : Gestion de projet 1
author      : Jonathan Lechien
description : Supports de l'unité 4PRJ1D.
keywords    : Marp, Slides, Informatique, Projet, Java.
marp        : true
paginate    : true
theme       : godel
mermaid     : true
footer      : "JLC - 4PRJ1D"

--- 

<!-- _class: titlepage -->

# 4PRJ1D - Théorie
## Gestion de projet 1
### Jonathan Lechien
#### Bruxelles, février 2025
##### Haute École Bruxelles-Brabant : Département des Sciences Informatiques 

---        
     
# Objectifs pédagogiques

- **Analyser** les exigences et **planifier** le développement du projet.
- **Concevoir**, **développer** et développer** une application complète.
- **Justifier** ses choix techniques et proposer des améliorations.
- **Critiquer** de manière réfléchie son analyse à la fin du développement,

---        
     
# Matières

<div class="columns">
<div>
      
<!-- _class: cool-list -->

### Développement Java

1. *FXML et Scene Builder*
2. *Multi Threading*
3. *JDBC et JPA*
4. *Librairie OCR*
   
</div>  
<div>    

### Conception et gestion de projet

5. *Repository pattern* 
6. *Architectural pattern* 
7. *Tester une application*
8. *Présenter une analyse* 
 
</div>    
</div> 

---

# Organisation de l'unité

- 2H par semaine de théorie
- 4H par semaine de laboratoire
- Planning détaillé disponible sur PoEsi  

--- 
 
<!-- _class: cite -->        

L'**évaluation** repose sur un contrôle **continu** structuré autour de la réalisation d’un **projet en binôme**. Une **défense individuelle** sera organisée afin d’évaluer les aspects techniques du projet, au cours de laquelle chaque étudiant devra également répondre à une **question théorique** sur les concepts abordés en cours. 

---
<!-- _class: transition2 -->  

Interface utilisateur avec Scene Builder<br>
Utilisation de fichiers FXML

--- 

# Une approche déclarative pour JavaFX

- Séparation entre logique et interface utilisateur
- Facilite la collaboration entre développeurs et designers
- Lisibilité améliorée du code
- Réutilisation et modularité

---

# Qu'est-ce que le FXML ?

- Un langage basé sur XML permettant de définir des interfaces JavaFX
- Chargé et interprété à l'exécution par JavaFX
- Permet de créer des interfaces graphiques dynamiques

Exemple :
```xml
<VBox xmlns="http://javafx.com/javafx" 
      xmlns:fx="http://javafx.com/fxml">
    <Label text="Bonjour, FXML!" />
    <Button text="Cliquez-moi" />
</VBox>
```
> **Note** : Un espace de noms XML (`xmlns`) est une recommandation du W3C qui permet d'employer des éléments et des attributs nommés dans une instance XML. 
---

# Balises et équivalence avec JavaFX

- `<VBox>` équivaut à `new VBox()` en Java
- `<Label text="Texte"/>` équivaut à `new Label("Texte")`
- `<Button>` équivaut à `new Button()`

Exemple JavaFX classique :
```java
VBox vbox = new VBox();
Label label = new Label("Bonjour, JavaFX!");
Button button = new Button("Cliquez-moi");
vbox.getChildren().addAll(label, button);
```

---

# SceneBuilder : Interface graphique pour créer du FXML

- Permet de générer du FXML visuellement
- Facile d'utilisation pour les non-développeurs
- Génère automatiquement les IDs et méthodes associées

---

# Charger un fichier

```java
public void start(Stage stage) throws IOException {
    URL resource = Main.class.getResource("hello-view.fxml");
    FXMLLoader fxmlLoader = new FXMLLoader(resource);
    Scene scene = new Scene(fxmlLoader.load(), 640, 800);
    stage.setTitle("Hello!");
    stage.setScene(scene);
    stage.show();
}
```

---

# Contrôleur et gestion des événements

- Lien entre FXML et logique Java
- Utilisation de `FXMLLoader` pour charger le fichier FXML
- Annotation `@FXML` pour lier les composants
- Gestion des événements avec `EventHandler`

Exemple :
```java
@FXML
private Button myButton;

@FXML
private void handleButtonClick() {
    System.out.println("Bouton cliqué !");
}
```

---

# Observable List

- Liste dynamique qui notifie les changements
- Utilisée dans JavaFX pour des éléments dynamiques

Exemple :
```java
ObservableList<String> items = FXCollections.observableArrayList("Item 1", "Item 2");
listView.setItems(items);
```

---

# TableView en JavaFX

- Tableaux dynamiques avec colonnes et données
- Utilisation d'`ObservableList` pour mise à jour automatique

Exemple :
```java
TableView<Person> table = new TableView<>();
TableColumn<Person, String> nameCol = new TableColumn<>("Nom");
table.getColumns().add(nameCol);
```

---

# Import de composants de `org.controlsfx`

- Bibliothèque JavaFX avancée
- `SearchableComboBox` pour une liste déroulante avec recherche intégrée

Exemple :
```java
SearchableComboBox<String> comboBox = new SearchableComboBox<>();
comboBox.getItems().addAll("Option 1", "Option 2");
```

---

# Navigation entre vues et patterns

- Utilisation de `FXMLLoader` pour charger dynamiquement les vues
- Patterns recommandés : **MVC** ou **Singleton Controller**

Exemple de changement de scène :
```java
Parent newView = FXMLLoader.load(getClass().getResource("view.fxml"));
stage.setScene(new Scene(newView));
```

---

# FXML et CSS

- Personnalisation avec des styles CSS
- Ajout via `setStylesheet` ou fichier `.css`

Exemple :
```css
.button {
    -fx-background-color: #2a5298;
    -fx-text-fill: white;
}
```

--- 

<!-- _class: biblio -->

# References 
<div class="columns">
<div>

OpenJFX. **OpenJFX**. Consulté le 1er février 2025. [https://openjfx.io/](https://openjfx.io/).

OpenJFX. **JavaDoc 23**. Consulté le 1er février 2025. [https://openjfx.io/javadoc/23/](https://openjfx.io/javadoc/23/).

GluonHQ. **Scene Builder**. Consulté le 1er février 2025. [https://gluonhq.com/products/scene-builder/](https://gluonhq.com/products/scene-builder/).

</div>

<div>

ControlsFX. **ControlsFX**. Consulté le 1er février 2025. [https://controlsfx.github.io/](https://controlsfx.github.io/).

OpenJFX. **Référence CSS JavaFX**. Consulté le 1er février 2025. [https://openjfx.io/javadoc/23/javafx.graphics/javafx/scene/doc-files/cssref.html](https://openjfx.io/javadoc/23/javafx.graphics/javafx/scene/doc-files/cssref.html).


</div>
</div>

---
<!-- _class: transition2 -->  

Programmation concurrente<br>
Les threads en java

--- 

<div>         
 
![h:450px](./img/work-in-progress.jpeg)
   
</div> 

---
<!-- _class: transition2 -->  

Design Pattern Repository<br>
JDBC et JPA

--- 

<div>         
 
![h:450px](./img/work-in-progress.jpeg)
   
</div> 


---
<!-- _class: transition2 -->  

Tester une application<br>
Des tests unitaires aux tests utilisateurs

--- 

<div>         
 
![h:450px](./img/work-in-progress.jpeg)
   
</div> 

---
<!-- _class: transition2 -->  

Architecture et gestion de projet<br>
MVC et ses variantes

--- 

<div>         
 
![h:450px](./img/work-in-progress.jpeg)
   
</div> 

---
<!-- _class: transition2 -->  

Présenter une analyse<br>

--- 

<div>         
 
![h:450px](./img/work-in-progress.jpeg)
   
</div> 