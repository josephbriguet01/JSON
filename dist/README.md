Copyright (C) BRIGUET Systems, Inc - All Rights Reserved
# JSON

### Introduction
JSON est une librairie qui se sert de Gson pour pouvoir transformer un objet en chaîne de caractère JSON et inversement. 
La librairie `*.jar` de Gson est téléchargeable à l'adresse suivante [https://jar-download.com/artifacts/com.google.code.gson/gson/2.8.2/source-code](https://jar-download.com/artifacts/com.google.code.gson/gson/2.8.2/source-code)

### Serialisation d'un objet en Json & Deserialisation d'une chaîne JSON en objet
```java
//Partons du principe que nous avons un tableau de 3 objets Voiture.
Voiture[] voitures = ... //initialisation d'un tableau de voitures



//Serialise la dernière voiture du tableau
String json = JSON.serialize(voitures[2]);

//Affiche la chaîne de caractères au format json de la voiture
System.out.println(json);



//Déserialise une chaîne json en objet Voiture
JSON<Voiture> voitureJSON = JSON.deserialize(Voiture.class, json);

//Récupère la voiture déserialisée -> On vient de récupérer un objet à partir d'un texte json
Voiture voiture = voitureJSON.getObj();



//Serialise le tableau complet de voitures
json = JSON.serialize(voitures);

//Affiche la chaîne de caractères au format json du tableau de voitures
System.out.println(json);



//Déserialise une chaîne json en liste de Voitures
voitureJSON = JSON.deserialize(Voiture.class, json);

//Récupère la liste de voitures déserialisée -> on vient de récupérer une liste à partir d'un texte json
List<Voiture> listVoitures = voitureJSON.getList();
```

### Attention
On peut constater que la déserialisation se fait de manière identique pour un objet ou une liste. Cela est dû au fait, que la méthode `JSON.deserialize()` s'occupe automatiquement de distinguer les listes ou les objets bruts. Donc dans les deux cas, la méthode renvoie un objet `JSON<ObjetADeserialiser>`.

"Alors comment savoir si l'objet contient une liste et non un objet brut et vice-versa ?"

-> C'est grâce à ses méthodes

Voici un exemple. Partons du principe que nous avons désérialisé une liste appelée `JSON<Voiture> list` et un objet appelé `JSON<Voiture> obj`
```java
//Commençons le test avec l'objet
boolean obj_isObject = obj.isObject();
boolean obj_isList = obj.isList();
System.out.println(obj_isObject + " - " + obj_isList); // Résultat: "true - false"

//Faisons maintenant le test avec la liste
boolean list_isObject = list.isObject();
boolean list_isList = list.isList();
System.out.println(list_isObject + " - " + list_isList); // Résultat: "false - true"

//Lorsque l'on utilise le switch case, il est possible d'utiliser cette structure (exemple sur l'objet. Cela fonctionne de la même manière pour la liste)
switch(obj.getType()){
    case "OBJECT":
        Voiture voiture = obj.getObj();
        break;
    case "LIST":
        List<Voiture> voitures = obj.getList();
        break;
}
```

##### Remarque
 * Un tableau d'objet serialisé puis redéserialisé ne redonne pas un tableau, mais une liste.
 * Une liste d'objet serialisé puis redéserialisé ne donne pas un tableau, mais une liste.
 
## Accès au projet GitHub => [ici](https://github.com/josephbriguet01/JSON "Accès au projet Git JSON")