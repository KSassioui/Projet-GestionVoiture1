# Autoroad — Gestion de location de voitures

Application web de **gestion et de réservation de voitures de location**, développée avec **ASP.NET Core MVC (.NET 8)** et **MySQL**. Elle propose un site public pour les clients (catalogue, disponibilité, réservation en ligne) et un espace d'administration pour gérer le parc, les clients et les réservations. Les prix sont exprimés en **MAD**.

## Fonctionnalités

### Espace client
- Page d'accueil, catalogue des voitures avec **filtres** (marque, catégorie, ville, transmission) et fiche détaillée.
- **Vérification de disponibilité en direct** : détection des chevauchements de dates, prise en compte des voitures en maintenance, calcul automatique du nombre de jours et du montant total.
- Inscription, connexion, profil et page **« Mes réservations »**.
- Réservation confirmée automatiquement lorsque la voiture est libre sur la période choisie.
- Page de contact.

### Espace administrateur
- **Tableau de bord** : nombre de réservations, revenus, voitures disponibles, nombre de clients, réservations récentes, voitures les plus louées, graphique des revenus réels et potentiels sur 7 jours.
- **Gestion des voitures** : ajout, modification, suppression, recherche et envoi de photo.
- **Gestion des clients** et **des réservations**.
- **Exports CSV** : rapport des réservations et liste des clients.

## Technologies

| Couche | Technologie |
|---|---|
| Framework | ASP.NET Core MVC, .NET 8, C# |
| Base de données | MySQL, Entity Framework Core 8, Pomelo.EntityFrameworkCore.MySql |
| Authentification | ASP.NET Core Identity (rôles `Admin` et `Client`, cookies de session) |
| Vues | Razor (`.cshtml`) avec plusieurs layouts (public, client, admin, connexion) |
| Front-end | Bootstrap, jQuery, Owl Carousel, AOS, Magnific Popup |

## Modèle de données

- **Voiture** : nom, marque, modèle, catégorie, ville, prix par jour, état (`Disponible`, `Reservee`, `EnLocation`, `EnMaintenance`), couleur, année, plaque, carburant, transmission, portes, sièges, climatisation, kilométrage, photo.
- **Reservation** : client, voiture, dates de début et de fin, statut (`En attente`, `Confirmée`, `Annulée`), montant total.
- **Paiement** : réservation, montant, date, méthode.
- **Client** et **Administrateur** : comptes Identity avec nom, prénom et téléphone.

## Prérequis

- [.NET SDK 8](https://dotnet.microsoft.com/download) (ou plus récent)
- MySQL 8 démarré en local
- Outil EF Core : `dotnet tool install --global dotnet-ef`

## Installation et lancement

1. **Configurer la connexion MySQL** dans `appsettings.json` :

   ```json
   "ConnectionStrings": {
     "DefaultConnection": "Server=localhost;Port=3306;Database=location_voiture_db;Uid=root;Pwd=;"
   }
   ```

2. **Créer la base et les tables** :

   ```bash
   dotnet ef database update
   ```

3. **Lancer l'application** :

   ```bash
   dotnet run
   ```

   Puis ouvrez http://localhost:5063 (ou l'adresse affichée dans le terminal).

## Compte administrateur

Au premier démarrage, les rôles `Admin` et `Client` ainsi qu'un compte administrateur sont créés automatiquement (voir `Data/SeedData.cs`). **Changez ce mot de passe avant tout usage réel.**

| Rôle | Email | Mot de passe |
|---|---|---|
| Administrateur | `admin@autoroad.com` | `Admin@123` |

## Structure du projet

```
Projet-GestionVoiture1/
├── Controllers/     Account, ClientInterface, Voitures, Reservations, Clients, Dashboard
├── Models/          Voiture, Reservation, Paiement, Client, Administrateur
├── ViewModels/      LoginViewModel, RegisterViewModel
├── Data/            ApplicationDbContext, SeedData
├── Migrations/      Migrations Entity Framework Core
├── Views/           Vues Razor (Account, ClientInterface, Voitures, Reservations, Clients, Dashboard, Shared)
├── wwwroot/         CSS, JavaScript, images, polices
├── Program.cs       Configuration de l'application (Identity, MySQL, routes)
└── appsettings.json Configuration et chaîne de connexion
```

## Auteur

Projet réalisé par [KSassioui](https://github.com/KSassioui).
