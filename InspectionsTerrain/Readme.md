# Mini Projet Power Apps : Inspection Terrain

## 📌 Présentation

L’application Inspection Terrain est une application Power Apps Canvas permettant de collecter des données sur le terrain et de les stocker dans Dataverse.
Elle a été conçue pour aider les équipes d’inspection à :

Suivre l’état des sites,

Capturer des photos sur place,

Enregistrer automatiquement la localisation GPS,

Synchroniser les données avec une base centralisée.

## 🚀 Fonctionnalités principales

### 📝 1. Formulaire d’inspection

Saisie des informations principales :

Code du site

Nom du site

Type d’équipement

État

Inspecteur

Remarques

Sélection de la date et l’heure d’inspection.

### 📸 2. Upload d’images

La colonne Photo permet d’ajouter une photo directement dans le formulaire.

L’image est enregistrée automatiquement dans Dataverse

### 🌍 3. Géolocalisation automatique

Récupération des coordonnées GPS :

Latitude = Location.Latitude

Longitude = Location.Longitude

Stockage automatique dans Dataverse.

### 🔍 4. Filtrage et recherche

Barre de recherche intégrée pour filtrer les inspections selon :

Le code du site

Le nom du site

### 🗑️ 5. Suppression et édition

Possibilité de modifier une inspection existante.

Suppression directe depuis la galerie des inspections.

## 🛠️ Architecture technique

Composant	            Rôle	                     Détails

Power Apps Canvas    Interface utilisateur	     Formulaire d’inspection, galerie, filtres
Dataverse	           Base de données	           Stockage structuré des inspections et des photos
Contrôles Power Fx	 Automatisation	             Formules pour géolocalisation, filtrage, enregistrement
Images	             Captures terrain	           Stockées directement dans Dataverse

## 📷 Captures d’écran

Formulaire d'ajout d'inspection

<img width="1197" height="677" alt="image" src="https://github.com/user-attachments/assets/7a017950-46b9-4ab4-bbce-2d59f078a7cd" />







