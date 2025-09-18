# 🟠 Mini Projet d’entreprise — Gestion des formations internes

## 🎯 Contexte

Une entreprise de 300 salariés souhaite mettre en place un portail centralisé pour gérer la formation de ses collaborateurs :

Consultation du catalogue de formations.

Inscription et suivi par les employés.

Historique personnel des formations suivies et feedbacks.

### 👉 Objectif : automatiser le processus de bout en bout

### 🗄️ Partie 1 — Dataverse (base de données centralisée)

#### Tables principales

    * Employés

    Nom, Prénom, Email, Service, Manager, Solde formation annuel.

    * Formations

    Titre, Thème, Durée, Formateur, Nombre de places, Mode (Présentiel/Distanciel).

    * Inscriptions

    Employé lié, Formation liée, Statut (En attente, Confirmé, Annulé), Date d’inscription.

    * Feedbacks

    Employé lié, Formation liée, Note (1–5), Commentaire.

    * Relations

    1 Employé → plusieurs Inscriptions.

    1 Formation → plusieurs Inscriptions.

    1 Employé → plusieurs Feedbacks.

### 📱 Partie 2 — Power Apps (application front office)
 
 #### Application Employés

    Catalogue des formations disponibles

    Affiché dans une Table.

    Filtrage par thème via un ComboBox (Items = Formations).

    Recherche par mot-clé via un champ texte (Search()).

    Affichage par défaut de toutes les données.

    * Exemple de formule Items :

    Filter(
    Search(Formations; txtSearch.Text; Titre; Thème);
    IsEmpty(ComboBoxThemes.SelectedItems) 
        || Thème in ComboBoxThemes.SelectedItems.Thème
    )

#### Formulaire d’inscription

    Champ Employé prérempli automatiquement avec l’utilisateur connecté :
    
    DefaultSelectedItems = LookUp(Employés, Email = User().Email)

    Enregistrement de l’inscription dans Dataverse.
    
#### Historique personnel

    Liste des formations suivies par l’utilisateur connecté :
    
    Filter(
    Inscriptions,
    Employé.Email = User().Email
    )

    Affiche : titre de la formation, durée, statut (Confirmé, Annulé, En attente).

    Page séparée pour les feedbacks donnés.

### 🔐 Sécurité et rôles

#### Rôles créés :

Employé → accès uniquement à ses propres inscriptions et feedbacks.

Manager → accès aux inscriptions de son équipe.

Sécurité hiérarchique mise en place dans Dataverse :

Permet aux managers de voir les données de leurs subordonnés.

Les employés n’ont accès qu’à leurs propres données.

#### 📌 Les captures d’écran associées montrent :

##### Le catalogue filtrable et recherchable.

<img width="846" height="411" alt="image" src="https://github.com/user-attachments/assets/e99df8d9-5223-41af-a336-9b57b3b87175" />
<img width="1820" height="647" alt="image" src="https://github.com/user-attachments/assets/9f7cc52a-c762-4ee3-a658-1100412eabed" />
<img width="1823" height="540" alt="image" src="https://github.com/user-attachments/assets/18068d74-f36b-4390-8e08-8fbd5513ad8d" />

##### Le formulaire d’inscription prérempli avec le compte connecté.

<img width="1572" height="760" alt="image" src="https://github.com/user-attachments/assets/be6aabe7-3c09-4de4-b9f4-9de6a192244b" />
<img width="1852" height="812" alt="image" src="https://github.com/user-attachments/assets/70845fa1-f1a8-4453-a467-df2d45cae9e9" />


##### L’historique personnel des formations suivies.
<img width="973" height="547" alt="image" src="https://github.com/user-attachments/assets/a3fd2ce5-027c-4283-8707-e563efe7d514" />

##### Mes FeedBacks
<img width="883" height="493" alt="image" src="https://github.com/user-attachments/assets/fe7fe098-f71f-4562-9b87-9b70354da9fb" />

