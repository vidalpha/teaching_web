## Prérequis

- Algorithmique
- Bases en Java 
- Bases en Programmation Orientée Objet (POO)

## Planning des séances

Ces TPs se dérouleront en trois séances comme suit:

<table>
  
  <caption>Objectif: Tu seras capable d'évaluer une application en environnement multithreadé</caption>

    <tr> 
        <th>Séances</th> 
        <th>Avant TP</th> 
        <th>Contenu</th>
        <th>Ressources</th> 
    </tr>

    <tr> 
        <td>1</td> 
        <td>QCM sur les threads ❌</td> 
        <td>
        Identifier les problèmes classiques liés à l'utilisation des threads <br/>
        - Questions ouvertes
        </td>
        
        <td>
            3.12 Philosophes ❌ <br/>
            Lecteurs/Rédacteurs ❌ <br/>
            Producteurs/Consommateurs ❌ <br/>
        </td> 
    </tr>

    <tr> 
        <td>2</td> 
        <td>
            Rendre en ligne les exercices: <br/>
                - Salle d'attente ❌<br/>
                3.14 Le verrou Mutex ❌
        </td> 
        <td> 
            1. Comprendre les mécanismes de synchronisation (mutex et les sémaphores) <br/>
            2. Résoudre un problème complexe de synchronisation. <br/><br/>
            - Correction des exercices rendus ❌ <br/>
            - Résolution d'un étude de cas complexe portant sur l'une des fiches <br/>
            - Apprendre à debugger une application multithreadée avec Eclipse/IntelliJ ❌ <br/>
            - Questions ouvertes
        </td>
        <td>
            3.15 Tower Bridge <b>ou</b> ❌ <br/>
            3.11 Petri Net <b>ou</b> ❌ <br/>
            3.10 Workflow ❌ <br/>
        </td> 
    </tr>

    <tr> 
        <td>3</td> 
        <td></td> 
        <td>
        Objectifs spécifiques: <br/>
        1. Proposer une solution à une mise en situation <br/>
        2. Evaluer la production d'un pair <br/>
            - Mini-Exam (1H) <br/>
            - Correction <br/>
            - Evaluation par les pairs <br/>
            - Questions ouvertes
        </td>
        <td> 
        3.13 Le problème métaphysique des “philosophes et des boulets à la liégeoise congelés” ❌ <b>ou</b><br/>
        3.16 Power Bridge ❌ <b>ou</b><br/>
        3.18 Pipe-Line ❌
        </td>  
    </tr>

</table>


## Quelques rappels

### Implémentation en Java

#### Avec l'interface

```java linenums="1" hl_lines="1 16 18 20"
class ToDo implements Runnable {
    private String image;
    public ToDo(String im){ 
        image=im; 
    }
    public void DisplayImage(String im){ … }

    public void run(){
        DisplayImage(image);
    }
}


class Main(){
    public static void main(String...){
        ToDo job1 = new ToDo("http://www.ici.com/lion.jpg");
        ToDo job2 = new ToDo("http://www.la-bas.com/tigre.jpg");
        Thread t1 = new Thread(job1);
        Thread t2 = new Thread(job2);
        t1.start();
        t2.start();
        // Autre chose;
    }

}
```

#### Avec l'héritage

```java linenums="1" hl_lines="1 12 14"
public class ToDoFast extends Thread {
    private String image;
    public ToDoFast(String im){
        image= im;
    }

    public void run(){
        displayImage(image);
    }
}

ToDoFast t1 = new ToDoFast(« http://www.ici.com/lion.jpg »);
ToDoFast t2 = new ToDoFast(« http://www.labas.com/tigre.jpg »);
t1.start();
t2.start();
```

### Bon à savoir

- La méthode <span class="span-hightlight">run()</span> d’un thread ne doit pas être invoquée ;
- Le bloc synchronisé ne doit pas prendre en paramètre un thread ;
- <span class="span-hightlight">Wait()</span>, <span class="span-hightlight">notity</span>, <span class="span-hightlight">notifyAll()</span> doivent être utilisé dans le bloc synchronized ;
- Si une variable est partagée en dehors d’un bloc synchronisé, le modificateur volatile est peut être pertinent à utiliser pour s’assurer de la cohérence de la même visibilité de la variable par les différents threads.