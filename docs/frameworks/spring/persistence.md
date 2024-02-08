# Persistence layer

## JPA or Hibernate

J'importe les annotations d'Hibernate ou de JPA 😵‍💫? 

### Pour faire court... 🚀

Faites un tour [ici](https://www.youtube.com/watch?v=hM9wkQBFdDw){:target="_blank"} 🙃 pour vite discerner.


### Pour faire long 🚲
Hibernate est l'une des implémentation populaire de JPA. Lorsque vous importez les annotations JPA dans votre projet, Spring Boot les convertit automatiquement en annotations Hibernate. Cela permet à Spring Boot de profiter des fonctionnalités avancées d'Hibernate, tout en conservant la simplicité des annotations JPA.

Par exemple, l'annotation <span class="span-hightlight">@Entity</span> est convertie en annotation @Entity d'Hibernate. L'annotation <span class="span-hightlight">@Table</span> est convertie en annotation @Table d'Hibernate. Et ainsi de suite.

Voici un exemple de code qui montre comment Spring Boot convertit les annotations JPA en annotations Hibernate :

``` java
import javax.persistence.*;

@Entity
@Table(name = "users")
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "username")
    private String username;

    @Column(name = "password")
    private String password;

    // ...
}

```

Lorsque vous exécutez ce code dans un projet Spring Boot, Spring Boot convertit les annotations JPA en annotations Hibernate comme suit :

``` java
import org.hibernate.annotations.*;

@Entity
@Table(name = "users")
public class User {

    @Id
    @Generated(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "username")
    private String username;

    @Column(name = "password")
    private String password;

    // ...
}
```
Les annotations Hibernate sont ensuite utilisées par Hibernate pour gérer les données en base de données.

#### Pourquoi utiliser les annotations JPA dans le code ?
Dans un projet Spring Boot avec Hibernate et JPA, il est recommandé d'importer les annotations depuis JPA et non Hibernate. Cela est dû aux raisons suivantes :

- JPA est le standard, tandis qu'Hibernate est une implémentation de JPA. Cela signifie que les annotations JPA sont disponibles dans toutes les implémentations de JPA, y compris Hibernate.
- Les annotations JPA sont plus simples et plus portables que les annotations Hibernate. Les annotations JPA utilisent une syntaxe plus simple et sont plus faciles à comprendre pour les développeurs qui ne sont pas familiers avec Hibernate.
- Les annotations JPA sont plus évolutives que les annotations Hibernate. Les annotations JPA sont conçues pour évoluer avec le standard JPA, tandis que les annotations Hibernate peuvent devenir obsolètes ou indisponibles dans les futures versions d'Hibernate.

En conséquence, il est recommandé d'utiliser les annotations JPA dans tous les projets Spring Boot, quel que soit l'implémentation de JPA utilisée. Et si un jour vous pensez à changer d'implémentation... 😜 quoi de plus facile.

#### Autres implémentations JPA

| Implémentation             | Caractéristiques                          |
| ------------------ | ------------------------------------ |
| `EclipseLink`      | Implémentation de référence, complète et robuste  |
| `OpenJPA`          | Implémentation mature et stable, compatible avec une large gamme de SGBDR |
| `DataNucleus`      | Implémentation flexible et extensible, offre une large gamme de fonctionnalités |
| `Hibernate`      | Implémentation populaire, offre une large gamme de fonctionnalités|

En fin de compte, le choix de l'implémentation de JPA dépend des besoins spécifiques de l'application. Si vous recherchez une solution flexible et performante, Hibernate est un bon choix. Cependant, si vous recherchez une solution simple et abordable, une autre implémentation de JPA peut être une meilleure option.

## Annotations et attributs (*focus*)

Nous ne parcourrons pas dans cette section, tous les annotations et attributs mais juste certains à garder sous le coude 🧷.

### GenerationType

### CascadeType

### FetchType strategies
<span class="span-hightlight">FetchType</span> est une annotation utilisée en JPA et Hibernate pour spécifier comment une association entre deux entités doit être chargée. Dans une relation one-to-one, il existe trois valeurs possibles pour:

- LAZY = l'association est chargée avec l'entité principale. Cela signifie que lorsque nous chargeons l'entité principale, l'entité associée est également chargée.
- EAGER = l'association est chargée uniquement lorsque nous y accédons. Cela signifie que lorsque nous chargeons l'entité principale, l'entité associée n'est pas chargée.

Exemple:
``` java linenums="1" hl_lines="7-8"
@Entity
public class User {

    @Id
    private Long id;

    @OneToOne(fetch = FetchType.LAZY)
    private Address address;

}

@Entity
public class Address {

    @Id
    private Long id;

    private String street;
    private String city;
    private String state;
    private String zipCode;

}

```

Dans cet exemple, lorsque nous chargeons un utilisateur, l'adresse associée n'est pas chargée. Pour accéder à l'adresse, nous devons appeler la méthode <span class="span-hightlight">getAddress()</span> sur l'utilisateur.

#### Impact sur la performance

Le choix de FetchType peut avoir un impact sur les performances de l'application. <span class="span-hightlight">FetchType.EAGER</span> peut améliorer les performances si nous accédons souvent à l'association. Cependant, il peut également entraîner une augmentation de la taille de la requête et de la consommation de mémoire. <span class="span-hightlight">FetchType.LAZY</span> peut améliorer les performances si nous n'accédons pas souvent à l'association. Cependant, il peut entraîner une augmentation du temps de réponse de la requête.

[Aller plus loin ...](https://stackoverflow.com/questions/2990799/difference-between-fetchtype-lazy-and-eager-in-java-persistence-api){:target="_blank"}

## OneToOne relationship
:fontawesome-brands-youtube:{ .youtube } [Ressource vidéo](https://www.youtube.com/watch?v=GRV69QNSdVg){:target="_blank"}

Les annotations <span class="span-hightlight">@JoinColumn</span> et <span class="span-hightlight">@MapsId</span> sont utilisées pour définir la relation entre deux entités en Java Spring Boot. Elles sont toutes deux utilisées dans les relations un-à-un, mais elles ont des différences importantes.

### @JoinColumn

L'annotation <span class="span-hightlight">@JoinColumn</span> est utilisée pour définir une colonne de jointure entre les deux entités. La colonne de jointure est une colonne qui est présente dans les deux entités et qui est utilisée pour stocker la clé étrangère de l'autre entité.

Par exemple, si nous avons deux entités, User et Address, et que nous voulons que chaque utilisateur ait une adresse, nous pouvons utiliser l'annotation <span class="span-hightlight">@JoinColumn</span> comme suit :
``` java linenums="1" hl_lines="7-8"
@Entity
public class User {

    @Id
    private Long id;

    @OneToOne
    @JoinColumn(name = "address_id")
    private Address address;

}

@Entity
public class Address {

    @Id
    private Long id;

    private String street;
    private String city;
    private String state;
    private String zipCode;

}
```
Dans cet exemple, la colonne de jointure est <span class="span-hightlight">address_id</span>. Cette colonne est présente dans les deux entités, <span class="span-hightlight">User</span> et <span class="span-hightlight">Address</span>. La valeur de la colonne <span class="span-hightlight">address_id</span> dans l'entité User est la clé étrangère de l'entité Address.

### @MapsId
L'annotation <span class="span-hightlight">@MapsId</span> est utilisée pour mapper la clé primaire de l'une des entités sur la clé primaire de l'autre entité. Cela permet d'éviter d'avoir à définir une colonne de jointure distincte.

Par exemple, nous pouvons utiliser l'annotation <span class="span-hightlight">@MapsId</span> pour redéfinir la relation entre les entités User et Address comme suit :
``` java linenums="1" hl_lines="7-8"
@Entity
public class User {

    @Id
    private Long id;

    @OneToOne
    @MapsId
    private Address address;

}

@Entity
public class Address {

    @Id
    private Long id;

    private String street;
    private String city;
    private String state;
    private String zipCode;

}
```
Dans cet exemple, la clé primaire de l'entité User est mappée sur la clé primaire de l'entité Address. Cela signifie que la valeur de la clé primaire de l'entité User est également la clé étrangère de l'entité Address.

**Différences**

Les principales différences entre <span class="span-hightlight">@JoinColumn</span> et <span class="span-hightlight">@MapsId</span> sont les suivantes :

- <span class="span-hightlight">@JoinColumn</span> nécessite une colonne de jointure distincte, tandis que <span class="span-hightlight">@MapsId</span> n'en nécessite pas.
- <span class="span-hightlight">@JoinColumn</span> est plus flexible, car il permet de spécifier le nom et le type de la colonne de jointure.
- <span class="span-hightlight">@MapsId</span> est plus simple à utiliser, car il n'est pas nécessaire de définir une colonne de jointure distincte. Avec cette stratégie, vous n'avez plus besoin de vous souciez de la relation inverse (bidirectionnelle) 😎 car les deux entités *parent* Address (*parent*) et User (*enfant*) partagent la même clé primaire. Du parent, on peut récupérer l'enfant en spécifiant la clé primaire du parent.

### Performance
####  Default FetchType

FetchType.EAGER est la valeur par défaut pour les relations one-to-one.


#### LazyToOneOption.NO_PROXY|PROXY|FALSE
*06:14 :fontawesome-brands-youtube:{ .youtube } [(Source)](https://www.youtube.com/watch?v=GRV69QNSdVg&t=6m14s){:target="_blank"}==> L'annotation @LazyToOne(LazyToOneOption.NO_PROXY) est obsolète depuis la version 5.5 de Hibernate. La référence pour la fonctionnalité de chargement paresseux sans proxy est la suivante : <span class="span-hightlight">@OneToOne(fetch = FetchType.LAZY)</span>*

1. **FALSE**: The *@LazyToOne(LazyToOneOption.FALSE)* Hibernate annotation operates as if you set the fetch strategy to *FetchType.EAGER*. 

2. **PROXY**: The *@LazyToOne(LazyToOneOption.PROXY)* Hibernate annotation is redundant if the association uses the *FetchType.LAZY* strategy. 

3. **NO_PROXY *(Before)***: In *@OneToOne* bidirectional association side with following configuration activated:

``` xml linenums="1" hl_lines="8"
<plugin>
    <groupId>org.hibernate.orm.tooling</groupId>
    <artifactId>hibernate-enhance-maven-plugin</artifactId>
    <version>${hibernate.version}</version>
    <executions>
        <execution>
            <configuration>
                <enableLazyInitialization>true</enableLazyInitialization>
            </configuration>
            <goals>
                <goal>enhance</goal>
            </goals>
        </execution>
    </executions>
</plugin>

```

L'utiliation de *@LazyToOne(LazyToOneOption.PROXY)* est obselète à partir de la version 5.5 de Hibernate. Plus besoin dans faire mention explicite. *@OneToOne(fetch = FetchType.LAZY)* suffit.

[Aller plus loin...](https://vladmihalcea.com/hibernate-lazytoone-annotation/){:target="_blank"}


## ManyToOne relationship

La nom par défaut de la colonne de jointure est sous ce format: *entityParentNameLowercase*_*id*

Exemple:

``` java linenums="1" hl_lines="9"
@Entity
@Table(name = "orders")
public class Order {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @ManyToOne
    @JoinColumn(name = "customer_id")
    private Customer customer;

    // ...
}
```

Relation inverse:

```java linenums="1" hl_lines="12"
@Entity
@Table(name = "customers")
public class Customer {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "name")
    private String name;

    @OneToMany(mappedBy = "customer")
    private List<Order> orders;

    // ...
}
```

Pour utiliser la relation inverse en JPA, nous pouvons utiliser les méthodes *get()* et *set()* de la propriété de la classe *Customer* qui référence la collection d'instances de la classe *Order*.

Voici un exemple de code qui montre comment utiliser la relation inverse en JPA :

``` java
Customer customer = new Customer();
customer.setName("John Doe");

// Créer un nouvel ordre
Order order = new Order();
order.setCustomer(customer);

// Ajouter l'ordre à la liste des commandes du client
customer.getOrders().add(order);

// Obtenir la liste des commandes du client
List<Order> orders = customer.getOrders();
System.out.println(orders.size()); // 1
```

**Aller plus loin:**

- :fontawesome-brands-youtube:{ .youtube } [@vladmihalcea](https://www.youtube.com/watch?v=fuLaCgzzMBA){:target="_blank"}
- :fontawesome-brands-youtube:{ .youtube } [koor.fr](https://www.youtube.com/watch?v=GLiXZWZ3hCc){:target="_blank"}
- 📄 [baeldung.com](https://www.baeldung.com/hibernate-one-to-many){:target="_blank"}


## ManyToMany relationship

``` java linenums="1" hl_lines="12-17"
@Entity
@Table(name = "products")
public class Product {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "name")
    private String name;

    @ManyToMany(cascade={CascadeType.PERSIST, CascadeType.MERGE})
    @JoinTable(
        name = "products_categories",
        joinColumns = @JoinColumn(name = "product_id"),
        inverseJoinColumns = @JoinColumn(name = "category_id")
    )
    private Set<Category> categories;

    // ...
}
```

Dans cet exemple, les propriétés categories de la classe Product et products de la classe *Category* sont définies comme des relations *ManyToMany*. L'annotation <span class="span-hightlight">@JoinTable</span> spécifie la table de jointure qui est utilisée pour stocker les données de la relation.

Pour utiliser une relation *ManyToMany* en JPA, nous pouvons utiliser les méthodes *add()* et *remove()* de la propriété qui référence la collection d'instances de l'autre entité.

Voici un exemple de code qui montre comment utiliser une relation ManyToMany en JPA :

``` java
Product product = new Product();
product.setName("T-shirt");

// Ajouter la catégorie "Vêtements" au produit
Category category = new Category();
category.setName("Vêtements");
product.getCategories().add(category);

// Ajouter la catégorie "Homme" au produit
Category category = new Category();
category.setName("Homme");
product.getCategories().add(category);

// Obtenir la liste des catégories du produit
Set<Category> categories = product.getCategories();
System.out.println(categories.size()); // 2
```

Dans cet exemple, nous créons un nouveau produit nommé "T-shirt". Nous ajoutons ensuite les catégories "Vêtements" et "Homme" au produit. Enfin, nous obtenons la liste des catégories du produit et imprimons sa taille.

Dans ce cas, un produit peut appartenir à plusieurs catégories, et une catégorie peut contenir plusieurs produits.

**Relation inverse**

``` java linenums="1" hl_lines="12"
@Entity
@Table(name = "categories")
public class Category {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "name")
    private String name;

    @ManyToMany(mappedBy = "categories")
    private Set<Product> products;

    // ...
}
```

**List or Set mapping**

Dans le cas d'une relation *ManyToMany*, il est recommandé d'utiliser la structure de données Set au lieu de List pour le mapping. Cela est dû à deux raisons principales :

- Les clés étrangères doivent être uniques. Dans une relation *ManyToMany*, chaque instance de l'entité principale peut être associée à plusieurs instances de l'entité secondaire. Pour s'assurer que les clés étrangères sont uniques, il est nécessaire d'utiliser une structure de données qui ne permet pas les doublons. La structure de données Set est une bonne solution car elle ne permet pas les doublons.
- Les performances sont meilleures. Les structures de données Set sont généralement plus efficaces que les structures de données List. Cela est dû au fait que les structures de données Set ne nécessitent pas de maintenir l'ordre des éléments.

Dans l'exemple que j'ai donné, la relation *ManyToMany* entre les classes *Product* et *Category* est bidirectionnelle. Cela signifie que chaque produit peut être associé à plusieurs catégories, et que chaque catégorie peut contenir plusieurs produits. Dans ce cas, il est important de s'assurer que les clés étrangères sont uniques. L'utilisation d'une structure de données Set permet de garantir l'unicité des clés étrangères, et améliore les performances de la relation.

Bien sûr, il existe des cas où l'utilisation d'une structure de données List peut être préférable. Par exemple, si la relation *ManyToMany* est unidirectionnelle, ou si l'ordre des éléments est important.

### Custom mapping table

- :fontawesome-brands-youtube:{ .youtube } [@vladmihalcea](https://www.youtube.com/watch?v=bVLsHPfYerk&t=6m41s){:target="_blank"}

- 📄 [baeldung.com](https://www.baeldung.com/jpa-many-to-many){:target="_blank"}

**Aller plus loin:**

- :fontawesome-brands-youtube:{ .youtube } [@vladmihalcea](https://www.youtube.com/watch?v=bVLsHPfYerk){:target="_blank"}
- :fontawesome-brands-youtube:{ .youtube } [koor.fr](https://www.youtube.com/watch?v=nL50qlzgZAI){:target="_blank"}


## Héritage

JPA offre trois types d'héritage :

### JOINED 
la stratégie *JOINED* est la plus courante et la plus flexible. Elle consiste à créer une table par classe héritée. Chaque classe héritée aura donc sa propre table, et les tables seront jointes entre elles par une clé étrangère.

**Avantages :**

La stratégie *JOINED* est la plus flexible, car elle permet de représenter tout type d'héritage.
Elle est également la plus efficace, car elle permet de réduire le nombre de tables et de colonnes nécessaires.

**Inconvénients :**

La stratégie *JOINED* peut être moins performante que les autres stratégies, car elle nécessite de faire des jointures lors de l'accès aux données.

### TABLE_PER_CLASS 

La stratégie *TABLE_PER_CLASS* consiste à créer une table par classe, y compris la classe de base. Cela signifie que chaque attribut de la classe de base sera répété dans chaque table des classes héritées.

**Avantages :**

La stratégie *TABLE_PER_CLASS* est la plus simple à mettre en œuvre, car elle ne nécessite pas de jointures.
Elle est également la plus performante, car elle évite les jointures lors de l'accès aux données.

**Inconvénients :**

La stratégie *TABLE_PER_CLASS* peut être moins flexible que les autres stratégies, car elle ne permet pas de représenter facilement des relations entre classes héritées.

Elle peut également être moins efficace en termes de stockage, car elle nécessite de répéter les attributs de la classe de base dans chaque table des classes héritées.

### SINGLE_TABLE

La stratégie *SINGLE_TABLE* consiste à créer une seule table pour toutes les classes héritées. Cela signifie que tous les attributs de toutes les classes héritées seront stockés dans la même table.

**Avantages :**

La stratégie *SINGLE_TABLE* est la plus simple à mettre en œuvre, car elle ne nécessite pas de jointures.
Inconvénients :

La stratégie *SINGLE_TABLE* est la moins flexible, car elle ne permet pas de représenter facilement des relations entre classes héritées.
Elle peut également être moins efficace en termes de stockage, car elle nécessite de stocker des données redondantes dans la même table.

Le choix de la stratégie d'héritage à utiliser dépend des besoins spécifiques de l'application. La stratégie *JOINED* est la plus courante et la plus flexible, mais elle peut être moins performante que les autres stratégies. La stratégie *TABLE_PER_CLASS* est la plus simple à mettre en œuvre et la plus performante, mais elle peut être moins flexible. La stratégie *SINGLE_TABLE* est la plus simple à mettre en œuvre, mais elle est la moins flexible et la moins efficace en termes de stockage.

**Aller plus loin...**

- 📄 [Héritage avec JPA](https://gayerie.dev/epsi-b3-orm/javaee_orm/jpa_inheritance.html#l-annotation-inheritance){:target="_blank"}

## Autres ressources

- 📄 [Moocs Java EE Spring](https://gdufrene.github.io/mooc_jee_spring/jpa.html){:target="_blank"}

- 📄 [gayerie.dev](https://gayerie.dev/epsi-b3-orm/javaee_orm/jpa_relations.html){:target="_blank"}
- 📄 [thorben-janssen.com (Best pratices)](https://thorben-janssen.com/best-practices-many-one-one-many-associations-mappings/){:target="_blank"}
- 📄 [cours CNAM](http://orm.bdpedia.fr/introjpa.html){:target="_blank"}

- :fontawesome-brands-youtube:{ .youtube } [High-Performance Java Persistence](https://www.youtube.com/watch?v=FjmuClV40A4&list=PLwZWXcnAr8uecV7Oi3arDBRmQarKg7d65){:target="_blank"}

- :fontawesome-brands-youtube:{ .youtube } [High-Performance Java Persistence](https://www.youtube.com/watch?v=FjmuClV40A4&list=PLwZWXcnAr8uecV7Oi3arDBRmQarKg7d65){:target="_blank"}

- :fontawesome-brands-youtube:{ .youtube } [Tutorials about Hibernate and JPA](https://www.youtube.com/@ThoughtsOnJava){:target="_blank"}


