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
- **Concevoir**, **développer** et **tester** une application complète.
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

<div class="columns">

<div>

- Séparation entre logique et interface utilisateur
- Facilite la collaboration entre développeurs et designers
- Lisibilité améliorée du code
- Réutilisation et modularité

</div>

<div>

```xml
<?xml version="1.0" encoding="UTF-8"?>

<?import javafx.geometry.Insets?>
<?import javafx.scene.control.Label?>
<?import javafx.scene.layout.VBox?>

<?import javafx.scene.control.Button?>

<VBox alignment="CENTER" spacing="20.0" xmlns:fx="http://javafx.com/fxml">
    <padding>
        <Insets bottom="20.0" left="20.0" right="20.0" top="20.0"/>
    </padding>

    <Label text="Bonjour, FXML!" />
    <Button text="Cliquez-moi" onAction="#onHelloButtonClick"/>

</VBox>
```

<figcaption align="center">
<b>Code</b>: FXML Hello World.
</figcaption>

</div>

</div>

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

# Transformation d'une balise VBox

- On peut enrichir cette balise avec des attributs pour mieux contrôler l'affichage :
    - `alignment="CENTER"` : Centre les éléments à l'intérieur de la VBox.
    - `spacing="20.0"` : Définit un espacement de 20 pixels entre les éléments.


<div class="columns">

<div>

### FXML

```xml
<VBox alignment="CENTER" 
      spacing="20.0" 
      xmlns:fx="http://javafx.com/fxml">
```

</div>
<div>

### Equivalent Java

```java
VBox vbox = new VBox();
vbox.setAlignment(Pos.CENTER);
vbox.setSpacing(20.0);
```
</div>
</div>

---

# Import et première balise en FXML

- Un fichier FXML commence toujours par une balise de conteneur racine : la **root** .
- La root est de type `VBox` dans l'exemple.
- L'attribut `xmlns` est obligatoire et définit l'espace de noms XML utilisé.
- L'attribut `xmlns:fx` est utilisé pour les fonctionnalités spécifiques à JavaFX.

Exemple :
```xml
<VBox xmlns="http://javafx.com/javafx" 
      xmlns:fx="http://javafx.com/fxml">
```

- On doit importer des classes Java directement dans FXML :
```xml
<?import javafx.scene.control.Label?>
<?import javafx.scene.layout.VBox?>
<?import javafx.scene.control.Button?>
```
---

# Déclaration XML en FXML

- Chaque fichier FXML commence par une déclaration XML standard.
- Cette déclaration spécifie la version XML et l'encodage utilisé.
- Obligatoire pour assurer la compatibilité avec les analyseurs XML.

Exemple :
```xml
<?xml version="1.0" encoding="UTF-8"?>
```
- `version="1.0"` : Définit la version XML utilisée.
- `encoding="UTF-8"` : Spécifie l'encodage des caractères, essentiel pour la prise en charge des accents et caractères spéciaux.

---

# Dépendances Maven pour JavaFX et FXML

Dans le fichier `pom.xml`, ajoutez les dépendances suivantes :
```xml
<dependency>
    <groupId>org.openjfx</groupId>
    <artifactId>javafx-controls</artifactId>
    <version>17</version>
</dependency>
<dependency>
    <groupId>org.openjfx</groupId>
    <artifactId>javafx-fxml</artifactId>
    <version>17</version>
</dependency>
```

- `javafx-controls` : Contient les composants UI JavaFX
- `javafx-fxml` : Permet d'utiliser FXML dans l'application

---

# SceneBuilder : Interface graphique pour créer du FXML

<div class="columns-center">
<div>

<center>

![](./img/scenebuilder.png)

<figcaption align="center">
<b>Figure</b>: Scene Builder.
</figcaption>
</center>

</div>
<div>

- Permet de générer du FXML visuellement
- Facile d'utilisation pour les non-développeurs
- Génère automatiquement les IDs et méthodes associées

</div>
</div>

---

# Structure d'un projet Maven avec FXML - Version 1

```
my-javafx-app/
│-- src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/example/app/
│   │   │       ├── Main.java
│   │   ├── resources/
│   │   │   └── com/example/app/
│   │   │       ├── view.fxml
│-- pom.xml
```
- `Main.java` : Classe principale pour lancer l'application JavaFX.
- `view.fxml` : Définit l'interface graphique.

---

# Charger un fichier

```java
public class Main extends Application {
    @Override
    public void start(Stage stage) throws IOException {
        URL resource = Main.class.getResource("hello-view.fxml");
        FXMLLoader loader = new FXMLLoader(resource);
        Parent root = loader.load();
        Scene scene = new Scene(root, 640, 800);
        stage.setTitle("Hello!");
        stage.setScene(scene);
        stage.show();
    }

    public static void main(String[] args) {
        launch();
    }
}
```

---

# Une nouvelle classe : le Contrôleur FXML

- Lien entre FXML et logique Java
- Utilisation de `FXMLLoader` pour charger le fichier FXML
- Annotation `@FXML` pour lier les composants
- `@FXML` est utilisé pour injecter l'élément défini dans le fichier FXML.
- Gestion des événements avec `EventHandler`

---

# Structure d'un projet Maven avec FXML - Version 2

```
my-javafx-app/
│-- src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/example/app/
│   │   │       ├── Main.java
│   │   │       ├── FxmlController.java
│   │   ├── resources/
│   │   │   └── com/example/app/
│   │   │       ├── view.fxml
│-- pom.xml
```
- `Main.java` : Classe principale pour lancer l'application JavaFX.
- `Controller.java` : Gère la logique associée aux événements FXML.
- `view.fxml` : Définit l'interface graphique.

---

# Utilisation de `fx:id`

- `fx:id` permet d'identifier un élément du fichier FXML pour y accéder dans le contrôleur.

### Exemple :
```xml
<VBox xmlns:fx="http://javafx.com/fxml">
    <Button fx:id="myButton" text="Cliquez-moi"/>
</VBox>
```

### Accès en Java :
```java
public class Controller {
    @FXML
    private Button myButton;
}
```


---

# Utilisation de `fx:controller`

`fx:controller` spécifie la classe Java qui gère la logique de l'interface.

### Exemple :
```xml
<VBox xmlns:fx="http://javafx.com/fxml" fx:controller="com.example.FxmlController">
    <Button fx:id="myButton" text="Cliquez-moi"/>
</VBox>
```

### Accès en Java :
```java
public class FxmlController {
    @FXML
    private Button myButton;
}
```
---

# La méthode `initialize()` du contrôleur

- La méthode `initialize()` est automatiquement appelée **après l'instanciation** du contrôleur.
- Elle permet d'initialiser des composants.

### Exemple :
```java
public class FxmlController {
    @FXML private Label label;

    public void initialize() {
        label.setText("Bienvenue dans l'application!");
    }
}
```

---
# Notions avancées : `TableView` et `ObservableList`

- Une `ObservableList` est une liste dynamique qui permet de notifier les changements à l'interface utilisateur.
- Utile pour gérer des données affichées dans des composants comme `TableView`.
- `TableView` est un composant permettant d'afficher des données tabulaires.

---

# Déclaration d'un `TableView` en FXML

```xml
<TableView fx:id="personTable" xmlns:fx="http://javafx.com/fxml">
    <columns>
        <TableColumn text="Nom" fx:id="nameColumn" />
        <TableColumn text="Âge" fx:id="ageColumn" />
    </columns>
</TableView>
```

---

# Contrôleur associé à une `TableView` en FXML

```java
public class FxmlController {
    @FXML private TableView<Person> personTable;
    @FXML private TableColumn<Person, String> nameColumn;
    @FXML private TableColumn<Person, Integer> ageColumn;

    public void initialize() {
        ObservableList<String> items = 
            FXCollections.observableArrayList(person1, person2);
        nameColumn.setCellValueFactory(
            new PropertyValueFactory<>("name"));
        ageColumn.setCellValueFactory(
            new PropertyValueFactory<>("age"));
        personTable.setItems(items);
    }
}
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
- Patterns recommandés : **MVC** ou ses variants

Exemple de changement de scène :
```java
Parent newView = FXMLLoader.load(getClass().getResource("view.fxml"));
stage.setScene(new Scene(newView));
```

---

# FXML et CSS dans `src/main/java/resources`

<div class="columns" align="center">
<div>         

## styles.css

```css
.root {
    -fx-background-color: lightgray;
}

.button {
    -fx-background-color: blue;
    -fx-text-fill: white;
}
```
   
</div>
<div>

## hello-world.fxml

```xml
<VBox xmlns="http://javafx.com/javafx"
      xmlns:fx="http://javafx.com/fxml"
      stylesheets="@styles.css">
    <Button text="Bouton Stylisé" 
            styleClass="button"/>
</VBox>
```

</div>
</div>

- `stylesheets="@styles.css"` : Charge le fichier CSS.
- `styleClass="button"` : Applique la classe CSS définie.
--- 

# Structure d'un projet Maven avec FXML - Version 3

```
my-javafx-app/
│-- src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/example/app/
│   │   │       ├── Main.java
│   │   │       ├── FxmlController.java
│   │   ├── resources/
│   │   │   └── com/example/app/
│   │   │       ├── view.fxml
│   │   │       ├── styles.css
│   │   │       ├── images/
│-- pom.xml
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

# Introduction

<div class="columns">
<div>

<center>

![h:450](./img/thread-intro.jpg)

</center>

</div>
<div>


### Définition
- Un **thread** est une unité d'exécution au sein d'un processus.
- Permet l'exécution parallèle de tâches.

### Avantages du multithreading en Java
- **Meilleure utilisation des ressources**.
- **Réduction du temps d'attente** pour certaines tâches.
- **Amélioration de la réactivité** des applications.

</div>
</div>

---

# Le cycle de vie d'un thread

<div class="center">         
 
![h:450px](./img/thread-lifecycle.png)
   
</div> 

---

# Création d'un Thread

<!-- _class: cool-list -->

1. *Héritage de la classe Thread*
2. *Implémentation de l'interface Runnable*
3. *Composition via un attribut Thread*

---

# Création d'un Thread

<div class="columns">
<div>

<center>

![h:400](./img/thread-sequence-heritage.png)

</center>

</div>
<div>

## Héritage de la classe Thread

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread en cours d'exécution");
    }
}

MyThread t = new MyThread();
t.start();
```

</div>
</div>

> [Lien vers les codes exemples utilisés lors de la présentation](https://git.esi-bru.be/4prj1d-ressources/demo-thread)
---


# Création d'un Thread

<div class="columns">
<div>

<center>

![h:400](./img/thread-sequence-runnable.png)

</center>

</div>
<div>

## Implémentation de l'interface Runnable

```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Thread en cours d'exécution");
    }
}

Thread t = new Thread(new MyRunnable());
t.start();
```

</div>
</div>

---


# Création d'un Thread

<div class="columns">
<div>

<center>

![h:400](./img/thread-sequence-composition.png)

</center>

</div>
<div>

## Composition via un attribut

```java
public class MyThreadComposition {

    private Thread thread;

    public MyThreadComposition() {
        thread = new Thread(new MyRunnable());
    }

    public void start() {
        thread.start();
    }

}
```

</div>
</div>

---

# Différences entre la méthode start et run

- `start()` : démarre l'exécution du thread, elle appelle **automatiquement** la méthode `run()` dans un **nouveau thread** d'exécution.

- `run()` : méthode qui contient le code à exécuter dans le thread. Si vous définissez une classe qui **implémente Runnable** ou **étend Thread**, vous redéfinissez cette méthode pour spécifier ce que doit faire le thread. Si vous appelez directement `run()`, le code sera exécuté dans le thread principal, pas dans un nouveau thread.

---

# Threads Démon

Un **thread démon** s'exécute en arrière-plan et ne bloque pas la fermeture de l'application.

```java
Thread daemonThread = new Thread(() -> {
    while (true) {
        System.out.println("Daemon thread en cours");
    }
});

daemonThread.setDaemon(true);
daemonThread.start();
```

---

# Attendre la fin d'un Thread avec la méthode `join()`

<div class="columns">
<div>


```java
public class MonThread extends Thread {

    @Override
    public void run() {

        try {

            System.out.println("Le thread commence");

            // Simuler un travail en suspendant 
            // le thread  pendant 2 secondes
            Thread.sleep(2000);

            System.out.println("Le thread se " +
              " termine après 2 secondes.");

        } catch (InterruptedException e) {
            e.printStackTrace();
        }

    }
}


```

</div>
<div>


```java
public static void main(String[] args) {

    MonThread monThread = new MonThread();
    monThread.start();

    try {

        System.out.println(
          "Main attend la fin du thread");

        monThread.join();

        System.out.println(
          "Main reprend après la fin du thread");

    } catch (InterruptedException e) {
        e.printStackTrace();
    }

    System.out.println(
      "Le programme principal se termine.");
}
```

</div>
</div>

---


# Quelle est la valeur affichée ?

<div class="columns">
<div>


```java
public class MonCompteur
    implements Runnable {

    // Variable partagée entre les threads
    private static int compteur = 0;

    private void incrementer() {
        compteur++;
    }

    @Override
    public void run() {
        for (int i = 0; i < 1000; i++) {
            incrementer();
        }
    }
}
```

</div>
<div>


```java
public static void main(String[] args) 
    throws InterruptedException {

    MonCompteur monCompteur = new MonCompteur();
    Thread t1 = new Thread(monCompteur);
    Thread t2 = new Thread(monCompteur);

    // Démarrer les threads
    t1.start();
    t2.start();

    // Attendre la fin des deux threads
    t1.join();
    t2.join();

    // Afficher la valeur finale du compteur
    System.out.println(
        "Valeur du compteur : " + compteur);
}
```

</div>
</div>


---

# Synchronisation et gestion de la concurrence

#### Méthode synchronisée

L'accès à cette méthode est limité à un seul thread à la fois.

```java
private synchronized void incrementer() {
    compteur++;
}
```

--- 

# Synchronisation et gestion de la concurrence

#### Bloc synchronisé

```java
public void incrementer() {
    // Code non synchronisé
    //avant le bloc
    
    // Bloc synchronisé
    synchronized(this) {
        compteur++;
    }
}
```

--- 

# Synchronisation et gestion de la concurrence

#### Synchronisation sur des objets spécifiques

```java
public class MonCompteur
    implements Runnable {

    private static int compteur = 0;

    private final Object verrou = new Object();  // Un objet pour le verrouillage

    public void incrementer() {
        synchronized(verrou) {
            compteur++;
        }
    }
}
```

---


# L'étreinte mortelle - Deadlock

<!-- <div class="columns">
<div> -->

<center>

![h:400](./img/thread-deadlock.png)

<figcaption align="center">
Vision séquentielle des accès aux ressources, en réalité les actions sont concourantes.
</figcaption>

</center>

<!-- </div>
<div>

1. **Thread1** acquiert **Ressource1** et dort pendant 100 ms.
2. **Thread2** acquiert **Ressource2** et dort pendant 100 ms.
3. **Thread1** essaie de récupérer **Ressource2**, mais elle est déjà occupée par **Thread2**. **Thread1** se bloque en attendant.
4. **Thread2** essaie de récupérer **Ressource1**, mais elle est déjà occupée par **Thread1**. **Thread2** se bloque également en attendant.
5. Résultat : les deux threads sont **bloqués indéfiniment**, créant une **impasse** ou **deadlock**.

</div>
</div> -->


---


# Structures **thread-safe**



Structures de données conçues pour être utilisées en toute sécurité dans des environnements multithreads sans nécessiter de synchronisation externe.


<!-- _class: cool-list -->

Exemples : 

1. *SynchronizedList, SynchronizedSet, SynchronizedMap*
1. *ConcurrentSkipListMap, ConcurrentSkipListSet*
1. *CopyOnWriteArrayList, CopyOnWriteArraySet*
1. *Vector*



---

# Lister les Threads

`Thread.getAllStackTraces()` retourne les threads en cours d'exécution.

| **Nom du Thread**      | **Rôle** |
|------------------------|----------|
| `main`                | Le thread principal qui exécute la méthode `main()` |
| `Reference Handler`   | Gère les références|
| `Finalizer`           | Appelle la méthode `finalize()` |
| `Signal Dispatcher`   | Gère les signaux du système d'exploitation |

> Remarque : Le nombre exact peut varier selon la version de la JVM et l'environnement d'exécution.

---

# Threads et JavaFX

- **Main Thread** démarre l'application.
- **JavaFX Application Thread** gère l'UI.
- Une exception est lancée si une mise à jour est effectuée hors du **JavaFX Application Thread**,

```java
Exception in thread "Thread-XX" java.lang.IllegalStateException:
Not on FX application thread; currentThread = Thread-XX
```

---

# Threads et JavaFX

### Solution avec `Platform.runLater()`

<div class="columns">
<div>

```java
button.setOnAction(event -> {
    new Thread(() -> {
        try {
            Thread.sleep(2000);

            label.setText("Traitement "
                + " terminé !");  

        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }).start();
});

```

</div>
<div>


```java
button.setOnAction(event -> {
    new Thread(() -> {
        try {
            Thread.sleep(2000);

            Platform.runLater(()-> 
              label.setText("Traitement "
              + " terminé !"));

        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }).start();
});
```

</div>
</div>


---

# Threads et JavaFX

### Solution avec un Task<Void>
```java
Task<Void> task = new Task<>() {
        @Override
        protected Void call() throws Exception {
            label.setText("Mise à jour UI")
            return null;
        }
    };

// Liaison des propriétés du Task avec l'UI
label.textProperty().bind(task.messageProperty());
```

---

# Design Pattern Thread pool

## Principe

- Un nombre fixe ou dynamique de threads est maintenu dans un **pool**.
- Des tâches sont placées dans une file d'attente.
- Les threads du pool prennent et exécutent les tâches disponibles.
- Une fois une tâche terminée, le thread devient à nouveau disponible pour une nouvelle tâche

---


# Design Pattern Thread pool

<div class="columns">
<div>

<center>

![h:400](./img/threadpool-sequence.png)

</center>

</div>
<div>

```java
public static void main(String[] args) {
    // Création d'un pool de 3 threads
    ExecutorService executor = 
        Executors.newFixedThreadPool(3);

    // Soumission de 5 tâches au pool
    for (int i = 1; i <= 5; i++) {
        final int taskId = i;
        executor.submit(() -> {
            System.out.println("Tâche " + taskId + 
                " exécutée par " + 
                Thread.currentThread().getName());
            try {
                Thread.sleep(2000);
            } catch (InterruptedException ignored) {}
        });
    }

    executor.shutdown();
}
```

</div>
</div>


---

# JDK 21+ introduction des Virtual Threads

**Plus légers** et **scalables**.

```java
public static void main(String[] args) {
    Thread.startVirtualThread(() -> {
        System.out.println("Virtual Thread exécuté par : " + Thread.currentThread());
        try {
            Thread.sleep(1000); // Simulation d'un traitement
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
        System.out.println("Fin du Virtual Thread : " + Thread.currentThread());
    });

    System.out.println("Thread principal terminé : " + Thread.currentThread());
}
```

---

<!-- _class: biblio -->

# References 

Thread. **JavaDoc 23**. Consulté le 8 février 2025. [https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/lang/Thread.html](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/lang/Thread.html).

ExecutorService. **JavaDoc 23**. Consulté le 8 février 2025. [https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/concurrent/ExecutorService.html](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/concurrent/ExecutorService.html).

Asynchronous Programming in Java using Virtual Threads. **Venkat Subramaniam**. Consulté le 8 février 2025. [https://www.youtube.com/watch?v=uoTyIFvckXA](https://www.youtube.com/watch?v=uoTyIFvckXA).



---
<!-- _class: transition2 -->  

Principes SOLID</br>
&</br>
Design patterns

--- 

<!-- _class: cite -->        

**SOLID** est un ensemble de principes pour améliorer la conception logicielle en **Programmation Orientée Objet**.

---

# Principe SOLID

5 principes introduits par Robert C. Martin

- **S**ingle responsibility principle - Responsabilité unique 
- **O**pen–closed principle - Ouvert/fermé
- **L**iskov substitution principle - Substitution de Liskov 
- **I**nterface segregation principle - Ségrégation des interfaces 
- **D**ependency inversion principle - Inversion des dépendances

---

# **S**ingle Responsibility Principle - SRP

Une **classe**, une **fonction** ou une **méthode** doit avoir une et une seule **unique** raison d'être modifiée. 

Cela favorise la modularité et facilite la maintenance en évitant les classes surchargées de responsabilités.

---
# **S**RP - Exemple sur une classe

<div class="columns">
<div>         


```java
class Report {

    private String content;

    public void generate() {
        content = "Rapport de ventes\n
           ================\nTotal: 5000€\n";
    }

    public void saveToFile(String filename) {
        try (FileWriter writer 
                 = new FileWriter(filename)) {
            writer.write(content);
            System.out.println("Report saved to " 
                + filename);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

</div> 
<div>

### La classe a deux responsabilités :

1. Générer le rapport (logique métier)
2. Sauvegarder le fichier (interaction avec le système de fichiers)

</div>
</div>

---
# **S**RP - Exemple sur une classe

<div class="columns">
<div>         


```java
public class FileSaver {
    public void saveToFile(String data,
                          String filename) {
        try (FileWriter writer 
               = new FileWriter(filename)) {
            writer.write(data);
            System.out.println(
                "Report saved to " 
                + filename);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

</div> 
<div>

```java
public class Report {
    private String content;

    public void generate() {
        content = "Rapport de ventes\n
            ================\nTotal: 5000€\n";
    }

    public String getContent() {
        return content;
    }
}
```
</div>
</div>

- `Report` génère le rapport (logique métier)
- `FileSaver` sauvegarde le fichier (interaction avec le système de fichiers)

---

# **S**RP en lien avec le pattern Facade


<div class="columns">
<div>         

```java
public class ReportFacade {
    private Report report;
    private FileSaver saver;

    public ReportFacade() {
        this.report = new Report();
        this.saver = new FileSaver();
    }

    public void generateAndSaveReport(
            String filename) {

        report.generate();
        saver.saveToFile(
            report.getContent(),
                        filename); 
    }
}
```

</div> 
<div>

Le design pattern Facade fournit une interface simplifiée et unifiée pour **cacher la complexité** d'un sous-système, en **déléguant** les appels aux classes internes sans les exposer directement.

`ReportFacade` **coordonne** les deux services.

</div>
</div>

---

# **S**RP - Exemple sur une méthode

<div class="columns">
<div>         

### Deux responsabilités par méthode

```java
void displayWinner(List<Player> players, 
         Player currentPlayer) {

    Player winner = currentPlayer;

    for (Player player : players) {
        if(player.getScore()> 100){
            winner = player;
        }
    }

    System.out.println("Vainqueur : " 
        + winner.getName());
}
```

</div> 
<div>

### Une responsabilité par méthode

```java
Player getWinner(List<Player> players, 
         Player currentPlayer) {
    Player winner = currentPlayer;
    for (Player player : players) {
        if (player.getScore() > 100) {
            winner = player;
        }
    }
    return winner;
}

void displayWinner(Player player){
    System.out.println("Vainqueur : " 
        + winner.getName());
}
```

</div>
</div>

---

# **O**pen/Closed Principle

Une classe (ou une fonction, un module ...) doit être **fermée** à la **modification** directe mais **ouverte** à l'**extension**. 

L'objectif est de permettre l'ajout de nouvelles fonctionnalités **sans altérer le code existant**.

---

# **O**pen/Closed Principle - Exemple

<div class="columns">
<div>         


```java
public class PaymentProcessor {

    public void processPayment(String type) {

        if (type.equals("credit_card")) {

            System.out.println(
               "Processing card payment...");

        } else if (type.equals("payconiq")) {

            System.out.println(
               "Processing Payconiq payment...");
               
        }
    }
} 
```

</div> 
<div>

Pour ajouter le Bitcoin comme moyen de paiement, il faut modifier `PaymentProcessor`.

Si une classe a été **testée** et **validé**, on ne la **modifie pas**.
</div>
</div>

---

# **O**pen/Closed Principle en lien avec le pattern Strategy

<div class="columns">
<div>         

```java
interface PaymentStrategy {
    void pay();
}

class CreditCardPayment implements PaymentStrategy {
    public void pay() {

        System.out.println(
            "Processing credit card payment...");

    }
}

class PayconiqPayment implements PaymentStrategy {
    public void pay() {

        System.out.println(
            "Processing Payconiq payment...");

    }
}
```

</div> 
<div>

Pour ajouter un nouveau moyen de paiement il faut créer une nouvelle implémentation de `PaymentStrategy`.

Le design pattern Strategy permet de définir une **famille d'algorithmes**, de les **encapsuler** et de les **interchanger dynamiquement** sans modifier le code du client, favorisant ainsi l'extensibilité.
</div>
</div>

---

# **O**pen/Closed Principle en lien avec le pattern Strategy

<div class="columns">
<div>         

```java
public class PaymentProcessor {
    private PaymentStrategy strategy;

    public PaymentProcessor(
             PaymentStrategy strategy) {

        this.strategy = strategy;
    }

    public void processPayment() {
        strategy.pay();
    }

    public void setStrategy(
            PaymentStrategy strategy) {
        this.strategy = strategy;
    }
}
```

</div> 
<div>

```java
public static void main(String[] args) {

    CreditCardPayment cardStrategy
            = new CreditCardPayment();

    PaymentProcessor processor
            = new PaymentProcessor(
                cardStrategy);

    processor.processPayment();

    PayconiqPayment payconiqStrategy
            = new PayconiqPayment();

    processor.setStrategy(payconiqStrategy);

    processor.processPayment();
}
```
</div>
</div>


---

# Liskov Substitution Principle 

Une instance de type T doit pouvoir être remplacée par une instance de type G, tel que G sous-type de T, sans que cela ne modifie la cohérence du programme. 
Cela garantit que les sous-classes peuvent être utilisées de manière interchangeable avec leurs classes de base.

L'extension d'une classe **ne doit pas modifier le comportement attendu des méthodes remplacées**.

---

# Liskov Substitution Principle  - Exemple

<div class="columns">
<div>         

```java
class Rectangle {
    protected int width, height;

    public Rectangle(int width, 
                int height) {
        this.width = width;
        this.height = height;
    }

    public void setWidth(int width) { 
        this.width = width; 
    }
    public void setHeight(int height) { 
        this.height = height; 
    }
    public int getArea() { 
        return width * height; 
    }
}
```

</div> 
<div>

```java
class Square extends Rectangle {
    public Square(int side) {
        this.width = side;
        this.height = side;
    }

    @Override
    public void setWidth(int width) {
        this.width = width;
        this.height = width;
    }

    @Override
    public void setHeight(int height) {
        this.width = height;
        this.height = height;
    }
}
```

</div>
</div>

---
# Liskov Substitution Principle  - Exemple

```java
public static void main(String[] args) {
    Rectangle rect = new Rectangle();
    rect.setWidth(4);
    rect.setHeight(5);
    System.out.println("Rectangle area: " + rect.getArea());  // 4 * 5 = 20

    Rectangle square = new Square();
    square.setWidth(4);
    square.setHeight(5);

    System.out.println("Square area: " + square.getArea());  // 5 * 5 = 25 au lieu de 4 * 5
}
```
---

# Liskov Substitution Principle  - Exemple

<div class="columns">
<div>         

```java
interface Shape {
    int getArea();
}

class Rectangle implements Shape {
    protected int width, height;

    public Rectangle(int width, 
               int height) {

        this.width = width;
        this.height = height;

    }
...
}
```

</div> 
<div>

```java

class Square implements Shape {
    private int side;

    public Square(int side) { 
        this.side = side; 
    }
    
    ...
```

</div>
</div>

---

# Liskov Substitution en lien avec le pattern factory

<div class="columns">
<div>         

```java
class ShapeFactory {

    public static Shape createRectangle(
              int width, int height) {
        return new Rectangle(width, height);
    }

    public static Shape createSquare(
               int side) {
        return new Square(side);
    }

}
```

</div> 
<div>

La fabrique (**factory**) est un patron de conception créationnel utilisé en programmation orientée objet. 

Elle permet d'instancier des objets dont le type est dérivé d'un type abstrait. 

La **classe exacte** de l'objet n'est donc **pas connue par l'appelant**. 

</div>
</div>


---
# Interface Segregation Principle

Préférer **plusieurs interfaces spécifiques** pour chaque client plutôt qu'une seule interface générale. 

Cela évite aux classes de dépendre de méthodes dont elles n'ont pas besoin, réduisant ainsi les couplages inutiles.

---

# Interface Segregation Principle  - Exemple

```java
interface Worker {
    void work();
    void eat();
}

class Developer implements Worker {

    public void work() {
        System.out.println("Writing code...");
    }

    public void eat() {
        throw new UnsupportedOperationException("Developers don’t eat at work!");
    }
}
```


La classe `Developer` ne devrait pas être obligée d’implémenter `eat()`.


---

# Interface Segregation Principle  - Exemple

<div class="columns">
<div>         

```java
interface Workable {
    void work();
}

interface Eatable {
    void eat();
}

class Developer 
         implements Workable {
    public void work() {
        System.out.println(
            "Writing code...");
    }
}
```

</div> 
<div>

```java
class HumanWorker 
        implements Workable,
                      Eatable {

    public void work() {
        System.out.println(
            "Working...");
    }

    public void eat() {
        System.out.println(
            "Eating...");
    }
}
```

</div>
</div>

---

# Dependency Inversion Principle

Il faut **dépendre** des **abstractions**, pas des implémentations. 

Cela favorise la modularité, la flexibilité et la réutilisabilité en réduisant les dépendances directes entre les modules.

---

# Dependency Inversion Principle  - Exemple

<div class="columns">
<div>         

```java
class Keyboard {
    public String getInput() {
        return "User input";
    }
}

class Computer {
    private Keyboard keyboard = new Keyboard();

    public void useKeyboard() {
        System.out.println("Using: " 
            + keyboard.getInput());
    }
}
```

</div> 
<div>

```java
interface InputDevice {
    String getInput();
}

class Keyboard implements InputDevice {
    public String getInput() {
        return "User input from Keyboard";
    }
}

class Computer {
    private InputDevice inputDevice;

    public Computer(InputDevice inputDevice) {
        this.inputDevice = inputDevice;
    }

    public void useInputDevice() {
        System.out.println("Using: " 
            + inputDevice.getInput());
    }
}
```

</div>
</div>

---

# Pourquoi appliquer SOLID ?

- **Facilite la maintenance et l’évolutivité**
- **Réduit le couplage et améliore la réutilisabilité**
- **Facilite les tests unitaires**
- **Favorise un code plus clair et modulaire**
- **Conserver la conformité aux spécifications inchangées**

---

# Principle of Least Knowledge - Loi de Demeter

La Loi de Déméter stipule qu'un module ou une classe ne doit interagir qu'avec **ses dépendances directes** et **éviter les chaînes d’appels** profondes.

Une méthode d'un objet ne doit appeler que :

- Ses propres méthodes
- Les méthodes de ses attributs directs
- Les méthodes des paramètres qu’elle reçoit
- Les méthodes de ses propres objets créés

---
# Loi de Demeter - Exemple

```java
class Address {
    private String city;

    public Address(String city) {
        this.city = city;
    }

    public String getCity() {
        return city;
    }
}
```

---
# Loi de Demeter - Exemple

`Order` dépend de `Person` **et** de `Address`, le **couplage** est fort.

<div class="columns">
<div>         

```java
class Person {
    private Address address;

    public Person(Address address) {
        this.address = address;
    }

    public Address getAddress() {
        return address;
    }
}
```

</div> 
<div>

```java
class Order {
    private Person customer;

    public Order(Person customer) {
        this.customer = customer;
    }

    public void printCustomerCity() {
        System.out.println(
             customer
                  .getAddress()
                         .getCity()); 
    }
}
```

</div>
</div>

---

# Loi de Demeter - Exemple

`Order` ne dépend que de `Person`, ce qui réduit le **couplage**.

<div class="columns">
<div>         

```java
class Person {
    private Address address;

    public Person(Address address) {
        this.address = address;
    }

    public String getCity() { 
        return address.getCity();
    }
}
```

</div> 
<div>

```java
class Order {
    private Person customer;

    public Order(Person customer) {
        this.customer = customer;
    }

    public void printCustomerCity() {
        System.out.println(
            customer.getCity());
    }
}
```

</div>
</div>

---

# Limites des principes SOLID

## Complexité accrue
- **Problème :** Appliquer strictement SOLID peut fragmenter le code en trop de petites classes et interfaces, rendant le projet difficile à suivre.  
- **Solution :** Appliquer SOLID avec bon sens, en évitant une abstraction excessive si elle n’apporte pas de valeur.  

**Exemple :**  
- Avoir une **interface par type de paiement** (`CreditCardPayment`, `PaypalPayment`, etc.) est utile.  
- Mais créer une **interface pour chaque méthode** (`ProcessPayment`, `VerifyPayment`, `RefundPayment`) peut être exagéré.

---

# Limites des principes SOLID

## Risque de surconception (Overengineering)
- **Problème :** Trop appliquer **OCP (Ouvert/Fermé)** et **DIP (Dépendance Inversion)** peut mener à des couches d’abstraction inutiles.  
- **Solution :** Appliquer **KISS** (*Keep It Simple, Stupid*) et introduire des abstractions seulement si nécessaire.

**Exemple :**  
- Si une **classe concrète suffit** (`FileLogger`), inutile de créer une **interface** (`ILogger`) et plusieurs implémentations si le besoin ne se présente pas encore.

---

# Limites des principes SOLID

## Difficulté d’application dans les petits projets
- **Problème :** Dans un **projet simple**, appliquer SOLID peut être inutilement contraignant et ralentir le développement.  
- **Solution :** SOLID est plus adapté aux **projets évolutifs**. Dans un petit projet, mieux vaut **prioriser la lisibilité et la simplicité**.

**Exemple :**  
- Une simple **classe utilitaire** (`MathUtils`) n’a pas besoin d’être fragmentée en plusieurs **interfaces et classes**.

---
# Limites des principes SOLID

## Conclusion : SOLID ≠ dogme absolu
SOLID **améliore la maintenabilité et la modularité** d’un projet.  
Mais **trop l’appliquer peut compliquer inutilement le code**.  

### Meilleure approche :
- **Trouver un équilibre** entre SOLID, lisibilité et simplicité.  
- Toujours se demander : **"Est-ce que cette abstraction ajoute vraiment de la valeur ?"**  

**SOLID est un outil, pas une règle absolue !**



---

<!-- _class: transition2 -->  

JDBC<br>
Design Pattern Repository

--- 

<!-- _class: cite -->  

**Java Data Base Connectivity** est une API qui permet d’exploiter des bases de données au travers de requêtes SQL. 
Cette API permet d’écrire un code **indépendant du SGBD** utilisé.

---

# Classes essentielles de l'API

- **DriverManager** : Gère les pilotes JDBC et établit des connexions à une base de données.
- **Connection** : Représente une connexion active à une base de données, permettant d'exécuter des requêtes SQL.
- **Statement** : Utilisé pour exécuter des requêtes SQL statiques (SELECT, INSERT, UPDATE, DELETE).
- **ResultSet**: Contient les résultats d'une requête SQL SELECT et permet d'itérer sur les données retournées.
- **SqlException** : Exception levée en cas d'erreur liée à l'exécution d'une requête SQL.

---
# Commencer par ajouter le Driver



<div class="columns">
<div>         

### Driver pour SQLite

```xml
<dependency>
    <groupId>org.xerial</groupId>
    <artifactId>sqlite−jdbc</artifactId>
    <version>3.49.0.0</version>
</dependency>
```

</div> 
<div>

### Driver pour MySQL


```xml
<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
    <version>9.2.0</version>
</dependency>
```

</div>
</div>

---

# Écrire une requête de selection

```java
try {
    Connection connexion = DriverManager.getConnection("jdbc:sqlite:data/sqlite/demo.db";
    Statement stmt = connexion.createStatement();

    String query = "SELECT id,firstname,lastname FROM STUDENTS";

    ResultSet result = stmt.executeQuery(query);

    while (result.next()) {
        int id = result.getInt("id");
        String firstname = result.getString("firstname");
        String lastname = result.getString("lastname");
        System.out.println("\t record : " + id + " " + firstname + " " + lastname);
    }
} catch (SQLException ex) {
    System.out.println("DEMO_SELECT_ALL | Erreur " + ex.getMessage() + " SQLState " + ex.getSQLState());
}
```

---
# Écrire une requête de mise à jour

```java
try {
    Connection connexion = DriverManager.getConnection("jdbc:sqlite:data/sqlite/demo.db";
    Statement stmt = connexion.createStatement();

    String query = "UPDATE STUDENTS SET firstname='Patrick',lastName='Star' where id=1 ";

    int count = stmt.executeUpdate(query);
    System.out.println("\t Nombre de record modifié : " + count);
    
} catch (SQLException ex) {
    System.out.println("DEMO_UPDATE | Erreur " + ex.getMessage() + " SQLState " + ex.getSQLState());
}
```

---

# Code vulnérable ?

```java
public void execute(String query) {
    try {
        Connection connexion = DriverManager.getConnection("jdbc:sqlite:data/sqlite/demo.db";
        Statement stmt = connexion.createStatement();

        int count = stmt.executeUpdate(query);
        System.out.println("\t Nombre de record modifié : " + count);

    } catch (SQLException ex) {
        System.out.println("DEMO_UPDATE | Erreur " + ex.getMessage() + " SQLState " + ex.getSQLState());
    }
}
```

---
# Injection SQL

- La méthode `execute` accepte une requête SQL en paramètre (`query`) qui est ensuite exécutée directement avec `Statement`.
- `Statement` ne protège pas contre les entrées malveillantes.
- Un attaquant peut injecter du SQL arbitraire en passant une requête malveillante.

```java
execute("DELETE FROM users WHERE 1=1; --");
```

 Suppression de toutes les lignes de la table users !

---
# PrepareStatement

```java
public void executeSafe(String query, String name, int id) {
    try (Connection connexion = DriverManager.getConnection("jdbc:sqlite:data/sqlite/demo.db")) {
        String sql = "UPDATE users SET name = ? WHERE id = ?";
        try (PreparedStatement pstmt = connexion.prepareStatement(sql)) {
            pstmt.setString(1, name);
            pstmt.setInt(2, id);
            int count = pstmt.executeUpdate();
            System.out.println("\t Nombre de records modifiés : " + count);
        }
    } catch (SQLException ex) {
        System.out.println("DEMO_UPDATE | Erreur " + ex.getMessage() + " SQLState " + ex.getSQLState());
    }
}
```

---
# PreparedStatement

- Évite l'**injection** SQL : Les valeurs sont séparées de la requête SQL.
- Meilleure performance : La requête est **précompilée** par la base de données.
- Les mutateurs permettent de lier des valeurs dynamiques aux requêtes SQL : 
    - `setString(1, "Alice")`
    - `setInt(2, 30)`
    - `setDouble(3, 1500.75)`
    - `setNull(13, Types.INTEGER)`
    - `setBoolean(5, true)`

---

<!-- _class: cite -->  

Le design pattern **Repository** est un modèle d’architecture utilisé pour **séparer** la **logique d'accès aux données** de la **logique métier** d’une application. 

---

# L'interface Repository

<div class="columns">
<div>         

```java
public interface Repository<T, K> {
    void save(T entity);
    void deleteById(K id);
    T findById(K id);
    List<T> findAll();
}
```

</div> 
<div>

Décomposition des génériques <T, K>

- T : le type d'entité (ex: User, Product, etc.).
- K : le type de l'identifiant (ex: Integer, Long, etc.).

</div>
</div>

---

# Implémentation intuitive avec JDBC

```java
public class UserSqliteRepository implements Repository<User, Integer> {
    private static final String URL = "jdbc:sqlite:users.db";
    private Connection connection;

    public UserSqliteRepository() {
        this.connection = DriverManager.getConnection(URL);
    }

    @Override
    public void save(User user)  {
        String sql = "INSERT INTO users (name, email) VALUES (?, ?)";
        PreparedStatement pstmt = connection.prepareStatement(sql));
        pstmt.setString(1, user.getName());
        pstmt.setString(2, user.getEmail());
        pstmt.executeUpdate();
    }
```

---

# Implémentations multiples possibles

```java
public class UserSqlLiteRepository implements Repository<User, Integer> {
...
}

public class UserMySqlRepository implements Repository<User, Integer> {
...
}

public class UserFileRepository implements Repository<User, Integer> {
...
}

public class UserFirebaseRepository implements Repository<User, Integer> {
...
}

```

---

# Data Access Object et Data Transfert Object

Le pattern Repository peut être complété par deux autres concepts clés :

- DAO (Data Access Object) : Gère l'accès aux données dans la base de données.
- DTO (Data Transfer Object) : Transporte des données entre couches de l’application.


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