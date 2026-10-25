# salesforce-realestate-crm

# 🏡 Salesforce Sales Cloud Mini-CRM — Agence Immobilière

## 📌 Présentation du Projet
Ce projet est une solution CRM complète développée sur **Salesforce Sales Cloud (Developer Edition)** pour une agence immobilière.  
L'objectif est de gérer l'intégralité du cycle de vie commercial : de la capture de prospects (*Leads*) à la conclusion de ventes d'opportunités rattachées à des biens immobiliers (*Custom Object*).

---

## 🛠️ Architecture & Modèle de Données (Data Model)

### 1. Objets Standards & Personnalisés
* **Lead / Contact / Account / Opportunity :** Utilisation du cycle de vente natif Salesforce.
* **Bien immobilier (`Bien_Immobilier__c`) [Custom Object] :**
  * `Nom du bien` (Name - Text)
  * `Type` (Picklist : Appartement, Maison, Terrain, Local commercial)
  * `Ville` (Text)
  * `Prix affiché` (Currency)
  * `Statut` (Picklist : Disponible, Sous offre, Vendu, Retiré)

### 2. Relations
* **Lookup Relationship** sur l'objet `Opportunity` vers `Bien_Immobilier__c` pour associer chaque négociation commerciale au bien concerné.

---

## 🚀 Fonctionnalités & Configuration Métier

### 1. Qualification & Conversion de Leads
* Processus complet de qualification d'un prospect avec conversion automatique en **Compte**, **Contact** et **Opportunité**.
* Association du bien immobilier dès la création de l'opportunité.

### 2. Pipeline de Vente Personnalisé (Sales Process)
* Étapes adaptées au secteur immobilier :
  `Prospecting` ➔ `Visite` (30%) ➔ `Offre` (50%) ➔ `Négociation` (80%) ➔ `Closed Won` / `Closed Lost`.

### 3. Règle de Gestion (Validation Rule)
* **`Prix_Obligatoire_Si_Offre` :** Empeche le passage d'une opportunité à l'étape "Offre" si le montant (`Amount`) n'est pas renseigné.
  ```excel
  AND(
      ISPICKVAL(StageName, "Offre"),
      ISBLANK(Amount)
  )
