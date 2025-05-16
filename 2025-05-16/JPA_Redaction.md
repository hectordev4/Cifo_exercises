# Redacció de JPA

## Què és la persistència en JPA i per què és clau en aplicacions Spring Boot?

La persistència és el procés de **guardar**, **recuperar**, **actualitzar** i **eliminar** dades *(CRUD operations)* d'una base de dades relacional a través d'entitats Java. JPA actua com una capa d'abstracció que *facilita* i *simplifica* aquesta comunicació, de manera que els developers poden treballar amb objectes Java *(Object-Relational Mapping aka **ORM**)* sense preocupar-se dels detalls SQL subjacents.

### Quines són les seves característiques principals?

1. **ORM (Object-Relational Mapping)**:
Mapeja els objectes Java a les taules de la base de dades i gestiona operacions CRUD sense necessitat d'SQL directe.

2. **Entity Manager**:
Gestiona el cicle de vida de les entitats, incloent la creació, recuperació, actualització i eliminació.

3. **Persistència Transparent**:
Sincronitza automàticament els objectes Java amb la base de dades sense gestionar manualment sessions.

4. **JPQL (Java Persistence Query Language)**:
Permet realitzar consultes utilitzant una sintaxi orientada a objectes en lloc de taules de la base de dades.

5. **Suport per Transaccions**:
Garanteix la consistència de les dades mitjançant la gestió automàtica de transaccions i rollback en cas d'error.

6. **Callbacks del Cicle de Vida**:
Ofereix mecanismes per interceptar esdeveniments en el cicle de vida de les entitats, com creació, actualització o eliminació.

7. **Herència i Relacions**:
Suporta l'herència entre entitats i diferents tipus de relacions (OneToOne, OneToMany, ManyToOne, ManyToMany).

8. **Repositoris de Spring Data**:
Simplifica les operacions CRUD amb interfícies de repositori integrades i consultes basades en el nom dels mètodes.

### Com s'aplica en la gestió d'entitats? I què significa mapejar una entitat?

JPA gestiona les entitats a través de l'Entity Manager, que permet crear, recuperar, actualitzar i eliminar registres de la base de dades.

Mapejar una entitat és **vincular** una classe Java amb una *taula de la base de dades*, on els atributs de la classe representen les columnes de la taula.
Amb anotacions com **@OneToOne**, **@OneToMany**, **@ManyToOne** i **@ManyToMany**.

#### Exemple pràctic de configuració

```
@Entity
public class Student {
    @OneToMany(mappedBy = "student")
    private List<Enrollment> enrollments;
}
```
```
@Entity
public class Course {
    @OneToMany(mappedBy = "course")
    private List<Enrollment> enrollments;
}
```
```
@Entity
public class Enrollment {
    @ManyToOne
    private Student student;

    @ManyToOne
    private Course course;

    private LocalDate enrollmentDate;
    private String grade;
}
```