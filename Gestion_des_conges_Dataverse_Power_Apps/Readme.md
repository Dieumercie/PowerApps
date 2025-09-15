# 🚀 Projet RH — Gestion des congés avec Dataverse & Power Platform

## 📌 Contexte

Entreprise fictive de 200 employés qui souhaite remplacer ses fichiers Excel dispersés par une solution centralisée basée sur Microsoft Power Platform.
L’objectif :

Centraliser les informations RH (Employés, Types de congés, Demandes de congés).

Automatiser les flux de validation.

Offrir un accès transparent aux employés, managers et RH.


## 🏗️ Architecture du projet

    - Dataverse : base de données centralisée (Employés, Demandes de congés, Types de congés).

    - Applications :

       Model-Driven App : back-office RH avec vues et formulaires.

       Canvas App : application mobile pour les employés.

    - Power Automate : flux pour valider les soldes, notifier les managers et mettre à jour les compteurs.

    - Sécurité : rôles adaptés (Employé, Manager, RH) avec hiérarchie managériale activée.


### 🔹 Étape 1 — Modélisation Dataverse

#### Tables créées

** Employés

Nom, Prénom, Email (unique), Poste, Département (choix), Date d’embauche , Manager (lookup auto-référencé) , SoldeCongés (nombre entier)

** Types de congés

Nom du type (CP, RTT, Maladie, Exceptionnel)

** Demandes de congés

Employé (lookup)

Type de congé (lookup)

Date début, Date fin

NombreJours (entier calculé)

Statut (choix : En attente, Approuvé, Refusé)

Relations clés :

Employé ↔ Manager (auto-référence 1:N).

Employés 1:N Demandes de congés.

Types de congés 1:N Demandes de congés.

### 🔹 Étape 2 — Règles métier & Sécurité

#### Business Rules

** Validation des dates : Date fin >= Date début.

** Validation du solde : implémentée via Power Automate (NombreJours ≤ SoldeCongés).

#### Rôles de sécurité

** Employé : CRUD uniquement sur ses propres demandes.

** Manager : accès aux demandes de ses subordonnés via la hiérarchie managériale.

** RH : accès complet (Organisation).

#### Hiérarchie managériale

Activée dans l’admin center → Sécurité → Hiérarchie → Modèle du responsable → Profondeur = 3.

### 🔹 Étape 3 — Application Model-Driven

#### Navigation (site map)

Zone RH → Employés

Zone Congés → Demandes de congés, Types de congés

#### Vues

Employés → vue “Fiches Employés” (Nom, Email, Poste, Département, Manager, Solde).

** Demandes de congés → vues filtrées :

En attente

Approuvé

Refusé

#### Formulaires

** Employés :

Onglet Infos générales

Onglet Historique (sous-grille des demandes liées)

** Demandes de congés :

Onglet Détails (Employé, Type, Dates)

Onglet Workflow (Statut, Commentaire manager)

### 🔹 Étape 4 — Application Canvas (mobile employés)

### Fonctionnalités :

Soumettre une nouvelle demande SubmitForm().


### 🔹 Étape 5 — Automatisations Power Automate

#### Flux 1 — Validation du solde

    Déclencheur : Création d’une demande.

    Vérifie NombreJours ≤ SoldeCongés (Employé lié).

    Si Non → met Statut = Refusé + mail à l’employé.

    Si Oui → met Statut = En cours + mail au Manager.

#### Flux 2 — Validation Manager

    Déclencheur : Modification d’une demande (Statut = Approuvé).

    Récupère l’Employé lié.

    Calcule : NouveauSolde = AncienSolde – NombreJours.

    Met à jour la table Employés.

    Notifie l’employé.

#### 🔹 Étape 6 — Gouvernance & Solutions

Solution Dataverse RH-Conges-Solution.

Contient : tables, vues, formulaires, apps, flux.


### 🎯 Compétences mises en pratique

 ##### Modélisation Dataverse : tables, relations, colonnes calculées.

##### Règles métier et sécurité : rôles, hiérarchie managériale.

##### Applications : Model-Driven (back-office), Canvas (mobile).

##### Automatisations : Power Automate (conditions, expressions, connecteurs Dataverse).

## ⚠️ Limites observées dans Dataverse

#### Colonne primaire figée :

    Les relations (lookups) affichent toujours la colonne primaire de la table liée.
    
    👉 Dans mon projet, cela signifie que la table Demandes de congés affiche un identifiant (User-000X) au lieu du prénom/nom.

    👉 Pourquoi ?
    Parce que la colonne primaire (ID User) de la table Employés est définie comme un identifiant technique.

    👉 Conséquences
    Dans les captures d’écran, on peut voir ces IDs. Ce n’est pas une mauvaise conception.

    👉 Bonne pratique
    Définir dès le départ une colonne primaire (Nom complet) pour éviter ce type de rendu.

 #### Modèle de données (tables + relations).

<img width="1590" height="240" alt="image" src="https://github.com/user-attachments/assets/f88e3c86-fd24-4664-861f-2f21fb0b0772" />

<img width="472" height="436" alt="image" src="https://github.com/user-attachments/assets/05a2f0ba-16e6-458e-8a88-1b8b0458d8d7" />

<img width="1157" height="307" alt="image" src="https://github.com/user-attachments/assets/7e182508-aba2-4160-9f5b-8bc160c45985" />

#### Relations

<img width="613" height="566" alt="image" src="https://github.com/user-attachments/assets/53304c9e-2844-4e21-80bf-61bb4a52bd29" />

<img width="635" height="441" alt="image" src="https://github.com/user-attachments/assets/0a547ebf-ef2a-4b16-8ce1-f75140494b33" />

<img width="635" height="467" alt="image" src="https://github.com/user-attachments/assets/5c049647-2f62-4c46-ad0d-e557a9e6a4fd" />


#### Forulaires

##### Demande

<img width="555" height="556" alt="image" src="https://github.com/user-attachments/assets/88bd506d-ea01-4815-8c93-28d2e05252f5" />

##### Modification de statut

<img width="530" height="632" alt="image" src="https://github.com/user-attachments/assets/1bd13ed0-afbc-4e3b-a3c7-94e363f442bf" />

#### Model Driven App

<img width="1506" height="477" alt="image" src="https://github.com/user-attachments/assets/81e8763d-a41d-40fc-b259-9f3beeeada44" />


#### Rôles de sécurité

##### Employé 
<img width="1555" height="200" alt="image" src="https://github.com/user-attachments/assets/dcea0eeb-1aa1-458d-9641-db83e74ab5d2" />

<img width="1573" height="172" alt="image" src="https://github.com/user-attachments/assets/d9f6392e-530d-4748-beee-1a004c064283" />

##### Manager
<img width="1561" height="250" alt="image" src="https://github.com/user-attachments/assets/918b2c1e-17d3-4043-ad83-ffd2d62678d4" />
<img width="1560" height="183" alt="image" src="https://github.com/user-attachments/assets/d7ab8a60-7600-4c76-accb-eb4a08b038e9" />

##### RH
<img width="1552" height="258" alt="image" src="https://github.com/user-attachments/assets/4c8713d0-4397-4732-8696-c8a8e22c7fb8" />
<img width="1480" height="167" alt="image" src="https://github.com/user-attachments/assets/1a6580ff-d674-495c-ab20-86491bc12121" />

#### Sécurité de la hierarchie
<img width="967" height="316" alt="image" src="https://github.com/user-attachments/assets/af2bb7ed-e62c-407a-8439-58c3d32eb724" />


#### Flux Power Automate

##### Validation Solde

<img width="1307" height="847" alt="image" src="https://github.com/user-attachments/assets/dd94b588-84e0-4a21-8144-82791252c16e" />

<img width="1442" height="818" alt="image" src="https://github.com/user-attachments/assets/94ef9e79-0503-4ee4-a2de-d308273e34bc" />

##### Validation Manager et Mise à jour Solde

<img width="1337" height="748" alt="image" src="https://github.com/user-attachments/assets/7e56bead-195e-4159-9e78-5416ca42aabe" />

<img width="1196" height="866" alt="image" src="https://github.com/user-attachments/assets/5edd8571-9c23-4576-a6d3-240af6c63056" />

