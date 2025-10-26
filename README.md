# 🏦 API REST JAX-RS - Gestion de Comptes Bancaires

[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5.7-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![Java](https://img.shields.io/badge/Java-17+-orange.svg)](https://www.oracle.com/java/)
[![JAX-RS](https://img.shields.io/badge/JAX--RS-Jersey-blue.svg)](https://eclipse-ee4j.github.io/jersey/)
[![H2 Database](https://img.shields.io/badge/H2-Database-lightblue.svg)](https://www.h2database.com/)

## 📋 Description

Application Spring Boot qui expose une API RESTful utilisant **JAX-RS (Jersey)** pour la gestion de comptes bancaires. L'API supporte les formats **JSON** et **XML** pour une interopérabilité maximale.

![Démonstration](jaxrs/assets/demo.gif)

## 🎯 Objectifs du Projet

- Implémenter une API REST avec JAX-RS et Jersey
- Gérer les opérations CRUD (Create, Read, Update, Delete)
- Supporter les formats JSON et XML
- Utiliser Spring Data JPA avec une base de données H2
- Appliquer les bonnes pratiques REST

## 🏗️ Architecture

```
jaxrs/
├── src/
│   ├── main/
│   │   ├── java/TP7/jaxrs/
│   │   │   ├── JaxrsApplication.java          # Point d'entrée de l'application
│   │   │   ├── config/
│   │   │   │   └── MyConfig.java              # Configuration Jersey
│   │   │   ├── entities/
│   │   │   │   ├── Compte.java                # Entité JPA
│   │   │   │   └── TypeCompte.java            # Énumération
│   │   │   ├── repositories/
│   │   │   │   └── CompteRepository.java      # Repository Spring Data JPA
│   │   │   └── restapi/
│   │   │       └── CompteRestJaxRSAPI.java    # Contrôleur REST JAX-RS
│   │   └── resources/
│   │       └── application.properties         # Configuration de l'application
│   └── test/
└── pom.xml                                     # Dépendances Maven
```

## 🛠️ Technologies Utilisées

| Technologie | Version | Description |
|------------|---------|-------------|
| **Spring Boot** | 3.5.7 | Framework principal |
| **JAX-RS (Jersey)** | 3.1.11 | API REST |
| **Spring Data JPA** | 3.5.5 | Accès aux données |
| **H2 Database** | 2.3.232 | Base de données en mémoire |
| **Lombok** | 1.18.42 | Réduction du code boilerplate |
| **JAXB** | 4.0.6 | Support XML |
| **Hibernate** | 6.6.33 | ORM |
| **Maven** | - | Gestion des dépendances |

## 📦 Prérequis

- **Java 17** ou supérieur
- **Maven 3.6+**
- **Postman** ou **cURL** (pour tester l'API)
- Un IDE (IntelliJ IDEA, Eclipse, VS Code)

## 🚀 Installation et Démarrage

### 1. Cloner le projet
```bash
git clone <url-du-repository>
cd jaxrs
```

### 2. Compiler le projet
```bash
mvnw clean install
```

### 3. Lancer l'application
```bash
mvnw spring-boot:run
```

### 4. Vérifier le démarrage
L'application démarre sur **http://localhost:8080**

Console H2 accessible à : **http://localhost:8080/h2-console**
- **JDBC URL**: `jdbc:h2:mem:banque`
- **Username**: `sa`
- **Password**: _(vide)_

## 📡 Endpoints de l'API

### Base URL
```
http://localhost:8080/banque
```

### Liste des endpoints

| Méthode | Endpoint | Description | Content-Type | Accept |
|---------|----------|-------------|--------------|--------|
| `GET` | `/banque/comptes` | Récupérer tous les comptes | - | `application/json` ou `application/xml` |
| `GET` | `/banque/comptes/{id}` | Récupérer un compte par ID | - | `application/json` ou `application/xml` |
| `POST` | `/banque/comptes` | Créer un nouveau compte | `application/json` ou `application/xml` | `application/json` ou `application/xml` |
| `PUT` | `/banque/comptes/{id}` | Mettre à jour un compte | `application/json` ou `application/xml` | `application/json` ou `application/xml` |
| `DELETE` | `/banque/comptes/{id}` | Supprimer un compte | - | - |

## 📊 Modèle de Données

### Entité Compte

```java
{
    "id": 1,
    "solde": 5000.0,
    "dateCreation": "2025-10-26",
    "type": "COURANT"  // COURANT ou EPARGNE
}
```

### Types de Compte
- `COURANT` : Compte courant
- `EPARGNE` : Compte épargne

## 🧪 Tests avec Postman

### Configuration des Headers

#### Pour JSON
```
Accept: application/json
Content-Type: application/json
```

#### Pour XML
```
Accept: application/xml
Content-Type: application/xml
```

### Exemples de Requêtes

#### 1. GET - Récupérer tous les comptes (JSON)
```http
GET http://localhost:8080/banque/comptes
Accept: application/json
```

**Réponse :**
```json
[
    {
        "id": 1,
        "solde": 2038.025422337777,
        "dateCreation": "2025-10-26",
        "type": "EPARGNE"
    },
    {
        "id": 2,
        "solde": 4532.3112822542125,
        "dateCreation": "2025-10-26",
        "type": "COURANT"
    }
]
```

#### 2. GET - Récupérer tous les comptes (XML)
```http
GET http://localhost:8080/banque/comptes
Accept: application/xml
```

**Réponse :**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<comptes>
    <compte>
        <id>1</id>
        <solde>2038.025422337777</solde>
        <dateCreation>2025-10-26</dateCreation>
        <type>EPARGNE</type>
    </compte>
    <compte>
        <id>2</id>
        <solde>4532.3112822542125</solde>
        <dateCreation>2025-10-26</dateCreation>
        <type>COURANT</type>
    </compte>
</comptes>
```

#### 3. GET - Récupérer un compte par ID
```http
GET http://localhost:8080/banque/comptes/1
Accept: application/json
```

#### 4. POST - Créer un nouveau compte (JSON)
```http
POST http://localhost:8080/banque/comptes
Content-Type: application/json
Accept: application/json

{
    "solde": 7500.0,
    "dateCreation": "2025-10-26",
    "type": "COURANT"
}
```

#### 5. POST - Créer un nouveau compte (XML)
```http
POST http://localhost:8080/banque/comptes
Content-Type: application/xml
Accept: application/xml

<?xml version="1.0" encoding="UTF-8"?>
<compte>
    <solde>7500.0</solde>
    <dateCreation>2025-10-26</dateCreation>
    <type>COURANT</type>
</compte>
```

#### 6. PUT - Mettre à jour un compte
```http
PUT http://localhost:8080/banque/comptes/1
Content-Type: application/json
Accept: application/json

{
    "solde": 10000.0,
    "dateCreation": "2025-10-26",
    "type": "EPARGNE"
}
```

#### 7. DELETE - Supprimer un compte
```http
DELETE http://localhost:8080/banque/comptes/1
```

## 🔧 Configuration

### application.properties
```properties
# Application
spring.application.name=jaxrs
server.port=8080

# H2 Database
spring.datasource.url=jdbc:h2:mem:banque
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

# H2 Console
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console

# JPA/Hibernate
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect

# Jersey
spring.jersey.application-path=/
```


## 👨‍💻 Auteur

**ACHRAF**


