# 📘 Authentification JWT avec Spring Boot 

## 👤 **Auteur**

Ayoub Ouhensous
TP : Mise en place d’un système d’authentification sécurisé avec JWT
Technologies : Spring Boot · Spring Security · JWT

---

# 🚀 **1. Introduction**

Ce projet démontre comment mettre en place une **authentification sécurisée utilisant les JWT (JSON Web Tokens)** avec **Spring Boot** et **Spring Security**.

L'application permet :

* L’authentification d’un utilisateur (login)
* La génération d’un JWT signé
* La validation du JWT dans chaque requête
* La protection des endpoints de l’API

---

# 🏗️ **2. Architecture du projet**

Le système d’authentification repose sur les éléments suivants :

* **JwtService** → Génère et valide les tokens
* **JwtAuthFilter** → Intercepte les requêtes et vérifie le JWT
* **SecurityConfig** → Configure Spring Security
* **MyUserDetailsService** → Définit les utilisateurs en mémoire
* **AuthController** → Gère le login et les endpoints sécurisés

```
Client → /api/auth/login → AuthController  
AuthController → AuthenticationManager → UserDetailsService  
UserDetailsService → Retourne User  
JwtService → Génère un Token signé  
Client → Envoie Authorization: Bearer TOKEN  
Filter → Valide Token → Accès accordé
```

---

# 📦 **3. Installation**

## 🔧 Prérequis

* Java 17+
* Maven 3+
* Spring Boot 3+
* IDE (IntelliJ, Eclipse, VS Code…)

## 📥 Cloner le projet

```bash
git clone https://github.com/<your-repo>/jwt-auth-demo.git
cd jwt-auth-demo
```

## ▶️ Lancer l’application

```bash
mvn spring-boot:run
```

Application disponible sur :

```
http://localhost:8080
```

---

# 🔐 **4. Configuration JWT**

Dans `application.properties` :

```properties
app.jwt.secret=ChangeThisSecretToAStrongOne_32chars_min
app.jwt.expiration-ms=3600000
server.port=8080
```

* `secret` doit faire **32 caractères minimum**
* `expiration-ms` = validité du token (1 heure)

---

# 🧪 **5. Tester l’API (Postman)**

## 📌 1. **Login – Obtenir un JWT**

```
POST /api/auth/login
```

### Body (JSON)

```json
{
  "username": "user",
  "password": "password"
}
```

### Réponse

```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6..."
}
```

---

## 📌 2. **Accéder à un endpoint sécurisé**

```
GET /api/hello
```

### Ajouter dans les headers :

```
Authorization: Bearer <token>
```

### Réponse :

```json
{
  "message": "Bonjour, endpoint protégé OK"
}
```

---

# 📂 **6. Structure du projet**

```
src/main/java
├── controller
│   └── AuthController.java
├── security
│   ├── JwtAuthFilter.java
│   ├── JwtService.java
│   ├── MyUserDetailsService.java
│   └── SecurityConfig.java
├── dto
│   ├── AuthRequest.java
│   └── AuthResponse.java
└── DemoApplication.java
```

---

# 🧠 **7. Explication rapide – Comment ça marche ?**

1. L’utilisateur envoie ses identifiants → `/api/auth/login`
2. Spring Security vérifie les credentials
3. Si OK → création d’un JWT signé
4. Le client envoie ce token dans chaque requête
5. Le `JwtAuthFilter` valide le token
6. Si valide → l’utilisateur est authentifié

---

# 📚 **8. Technologies utilisées**

* Spring Boot 3
* Spring Security
* JWT (jjwt)
* Java 17
* Maven

---

# 📝 **9. Améliorations futures**

* Utilisateurs stockés dans une base de données (MySQL)
* Refresh Token
* Gestion des rôles (Admin / User)
* Intégration avec un front-end Angular

---

# 🎯 **10. Conclusion**

Ce projet met en œuvre une authentification robuste basée sur JWT, conforme aux standards modernes.
Il constitue une base solide pour un système de sécurité dans une application Spring Boot.


