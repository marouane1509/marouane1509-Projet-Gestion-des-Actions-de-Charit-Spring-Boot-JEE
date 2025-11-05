# CharityApp (Spring Boot) – README (FR)

Une application web de gestion caritative construite avec Spring Boot, Spring Security, Spring Data JPA et Thymeleaf. Elle permet de gérer les actions de charité, les dons, les partenaires, les organisations et les utilisateurs via une interface web sécurisée.

## Fonctionnalités
- Gestion des utilisateurs (authentification, rôles)
- Tableau de bord administrateur
- Gestion des actions de charité
- Gestion des dons
- Gestion des partenaires et organisations
- Pages publiques (accueil, mission, contact, etc.)

## Stack technique
- Java 17
- Spring Boot 3.4.4 (Web, Security, Data JPA, Thymeleaf)
- MySQL (prod/dev) + H2 (runtime/test)
- Maven

## Prérequis
- Java 17 installé
- Maven installé (ou utiliser les wrappers `mvnw`/`mvnw.cmd` inclus)
- MySQL en local

## Installation
1. Cloner le dépôt
   ```bash
   git clone <URL_DU_DEPOT>
   cd charityapp
   ```
2. Configurer la base de données MySQL (voir section Configuration)
3. Lancer l’application
   - Avec le wrapper Maven (Windows):
     ```bash
     .\mvnw.cmd spring-boot:run
     ```
   - Avec le wrapper Maven (Linux/Mac):
     ```bash
     ./mvnw spring-boot:run
     ```
   - Ou avec Maven installé:
     ```bash
     mvn spring-boot:run
     ```

L’application démarrera sur `http://localhost:8080`.

## Configuration
Les propriétés principales se trouvent dans `src/main/resources/application.properties`.

Exemple de configuration MySQL locale:
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/charitydb?createDatabaseIfNotExist=true&useSSL=false&serverTimezone=UTC
spring.datasource.username=root
spring.jpa.hibernate.ddl-auto=update
spring.thymeleaf.prefix=classpath:/templates/
spring.thymeleaf.suffix=.html
spring.thymeleaf.check-template-location=true
```

Adapter `spring.datasource.username` (et ajouter `spring.datasource.password` si nécessaire) selon votre environnement MySQL.

## Sécurité et rôles
La sécurité est configurée via Spring Security. Les routes publiques incluent `/`, `/login`, `/register`, `/mission`, `/contact` ainsi que les ressources statiques. Les routes sous `/admin/**` sont restreintes au rôle `ADMIN`.

À la première exécution, un compte administrateur est créé automatiquement si absent:
- Email: `admin@example.com`
- Mot de passe: `admin123`
- Rôle: `ADMIN`

Après connexion, les utilisateurs sont redirigés vers la page d’accueil.

## Pages/Endpoints principaux
- Public: `/`, `/mission`, `/contact`, `/login`, `/register`
- Admin: `/admin/**` (ex. gestion des utilisateurs, dons, partenaires, actions)

## Structure du projet (extrait)
```text
charityapp/
  pom.xml
  src/
    main/
      java/org/example/charityapp/
        CharityAppApplication.java
        controllers/ (ActionChariteController, AdminController, ...)
        dto/ (ActionChariteDTO, DonDTO, ...)
        entities/ (User, Don, Organization, ...)
        mappers/ (...)
        repositories/ (...)
        security/ (SecurityConfig.java)
        services/ (DataInitializer.java, ...)
      resources/
        application.properties
        templates/ (index.html, login.html, admin-*.html, ...)
    test/
      java/org/example/charityapp/
        CharityAppApplicationTests.java
```

## Commandes utiles
- Lancer en développement:
  ```bash
  mvn spring-boot:run
  ```
- Construire un JAR exécutable:
  ```bash
  mvn clean package
  ```
- Exécuter le JAR:
  ```bash
  java -jar target/CharityApp-0.0.1-SNAPSHOT.jar
  ```
- Lancer les tests:
  ```bash
  mvn test
  ```

## Dépannage
- Vérifier que MySQL tourne et que l’utilisateur/MDP ont les droits sur la base `charitydb`.
- Adapter `spring.jpa.hibernate.ddl-auto` (`update`, `create`, etc.) suivant vos besoins.
- En cas d’erreur de mot de passe admin, supprimer l’utilisateur correspondant dans la base puis relancer pour recréer l’admin par défaut.

## Licence
Spécifiez la licence souhaitée (par ex. MIT) dans ce fichier ou ajoutez un fichier `LICENSE`.


