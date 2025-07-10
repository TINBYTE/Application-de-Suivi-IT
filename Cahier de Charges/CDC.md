# Cahier des Charges Fonctionnel et Technique
## Application de Suivi des Projets et Tickets RSI

**Version** : 1.0  
**Date** : Juillet 2025  
**Destinataire** : RSI - Entreprise de Préfabrication  
**Technologie** : Django (Python)

---

## 1. Contexte et Objectifs

### 1.1 Contexte

L'entreprise de préfabrication collabore avec plusieurs sous-traitants informatiques pour la maintenance et le développement de ses systèmes d'information. Le RSI fait face à des difficultés de suivi dans la gestion des communications par email, des tickets ouverts et de la résolution des problèmes informatiques.

### 1.2 Problématiques identifiées

- Perte de suivi des emails échangés avec les sous-traitants
- Absence de centralisation des tickets et de leur statut
- Difficulté à suivre l'avancement des projets informatiques
- Manque de traçabilité des actions et décisions prises
- Absence d'indicateurs de performance et de délais

### 1.3 Objectifs

**Objectif principal** : Développer une application web personnelle permettant un suivi efficace et centralisé des projets, problèmes informatiques et communications avec les sous-traitants.

**Objectifs spécifiques** :
- Centraliser la gestion des projets informatiques
- Assurer la traçabilité complète des problèmes et incidents
- Faciliter le suivi des communications avec les sous-traitants
- Fournir des indicateurs de performance et des rappels automatiques
- Simplifier la génération de rapports et exports

---

## 2. Périmètre Fonctionnel

### 2.1 Périmètre inclus

- Gestion des projets informatiques
- Déclaration et suivi des problèmes/incidents
- Gestion des tickets et de leur cycle de vie
- Suivi des communications email avec les sous-traitants
- Système de notifications et rappels
- Tableau de bord et indicateurs
- Export de données et génération de rapports
- Historique complet des actions

### 2.2 Périmètre exclu

- Gestion multi-utilisateurs
- Intégration avec des systèmes tiers (ERP, CRM)
- Système de facturation
- Gestion documentaire avancée
- API publique

---

## 3. Description Détaillée des Fonctionnalités

### 3.1 Gestion des Projets

**F01 - Création de projet**
- Nom du projet (obligatoire, unique)
- Description détaillée
- Date de début et fin prévisionnelle
- Statut (Planifié, En cours, En attente, Terminé, Annulé)
- Sous-traitant principal assigné
- Budget prévisionnel (optionnel)
- Priorité (Faible, Normale, Haute, Critique)
- Pièces jointes (cahier des charges, devis, etc.)

**F02 - Suivi de projet**
- Modification des informations projet
- Ajout de commentaires et notes
- Association de tickets au projet
- Historique des modifications
- Calcul automatique du pourcentage d'avancement

### 3.2 Gestion des Problèmes/Incidents

**F03 - Déclaration de problème**
- Titre du problème (obligatoire)
- Description détaillée du problème
- Type de problème (Hardware, Software, Réseau, Sécurité, Autre)
- Niveau d'urgence (Faible, Modéré, Élevé, Critique)
- Service concerné (Production, Administration, Commercial, etc.)
- Collaborateur impacté
- Date et heure de détection
- Impact estimé sur l'activité
- Première analyse/diagnostic

**F04 - Classification du traitement**
- Option "Traiter en interne" ou "Envoyer à un sous-traitant"
- Si interne : assignation à soi-même avec checklist d'actions
- Si sous-traitant : sélection du prestataire et création automatique de ticket

### 3.3 Gestion des Tickets

**F05 - Cycle de vie des tickets**
- Statuts : Nouveau, Assigné, En cours, En attente client, En attente sous-traitant, Résolu, Fermé
- Assignation à un sous-traitant
- Date d'ouverture automatique
- Date de première réponse
- Date de résolution
- Date de fermeture
- SLA (Service Level Agreement) configurable par sous-traitant

**F06 - Informations détaillées du ticket**
- Numéro unique auto-généré
- Référence externe (numéro du sous-traitant)
- Catégorie (Incident, Demande, Changement, Problème)
- Temps estimé et temps passé
- Coût estimé et coût réel
- Solution appliquée
- Satisfaction (notation 1-5)

### 3.4 Gestion des Communications Email

**F07 - Intégration email**
- Copie manuelle des emails envoyés aux sous-traitants
- Stockage du contenu, destinataires, date d'envoi
- Association automatique ou manuelle avec un ticket
- Suivi des réponses reçues
- Indicateur "En attente de réponse"

**F08 - Templates d'emails**
- Modèles prédéfinis pour les types de demandes courants
- Variables dynamiques (nom projet, détails problème, etc.)
- Historique des emails envoyés par template

### 3.5 Système de Notifications et Rappels

**F09 - Alertes automatiques**
- Tickets sans réponse depuis X jours (configurable)
- Projets en retard sur les échéances
- SLA dépassés
- Tickets en attente de fermeture
- Notifications par email (optionnel)

**F10 - Dashboard des rappels**
- Liste prioritaire des actions à effectuer
- Compteurs d'alertes par catégorie
- Calendrier des échéances importantes

### 3.6 Recherche et Filtres

**F11 - Système de filtres avancés**
- Filtres par projet, statut, sous-traitant, date
- Recherche textuelle dans titre et description
- Filtres combinés (ET/OU)
- Sauvegarde de filtres fréquents
- Export des résultats filtrés

### 3.7 Tableau de Bord et Indicateurs

**F12 - Vue d'ensemble**
- Nombre de tickets ouverts/fermés par période
- Temps moyen de résolution par sous-traitant
- Répartition des tickets par statut
- Projets en cours et leur avancement
- Alertes et actions urgentes

**F13 - Graphiques et métriques**
- Évolution mensuelle du nombre de tickets
- Performance des sous-traitants (délais, satisfaction)
- Répartition par type de problème
- Charge de travail par période

### 3.8 Export et Rapports

**F14 - Exports de données**
- Export Excel : listes de tickets, projets, statistiques
- Export PDF : rapports formatés, fiches détaillées
- Période personnalisable
- Sélection des champs à exporter

**F15 - Rapports automatisés**
- Rapport mensuel d'activité
- Bilan par sous-traitant
- Rapport de performance SLA
- Synthèse des coûts

### 3.9 Historique et Traçabilité

**F16 - Audit trail complet**
- Toutes les actions utilisateur horodatées
- Modifications des champs avec valeurs avant/après
- Actions automatiques du système
- Conservation illimitée de l'historique

---

## 4. Interfaces Utilisateur

### 4.1 Principes de Design

- Interface simple et épurée
- Navigation intuitive avec menu principal
- Responsive design (utilisable sur tablette)
- Couleurs cohérentes avec charte graphique entreprise
- Icônes claires pour les actions principales

### 4.2 Pages Principales

**Page d'accueil - Dashboard**
- Vue synthétique des indicateurs clés
- Alertes et notifications importantes
- Accès rapide aux fonctions principales
- Graphiques de performance

**Page Projets**
- Liste des projets avec statuts visuels
- Bouton "Nouveau projet"
- Filtres et recherche
- Vue détaillée en modal ou page dédiée

**Page Problèmes/Tickets**
- Liste des tickets avec codes couleur par urgence
- Création rapide de problème
- Filtres avancés
- Actions groupées (fermeture, assignation)

**Page Communications**
- Historique des emails par ticket
- Indicateurs de réponse
- Accès aux templates
- Composition d'email avec pré-remplissage

**Page Sous-traitants**
- Liste des prestataires et leurs performances
- Configuration des SLA
- Historique des collaborations
- Évaluation et notes

**Page Rapports**
- Générateur de rapports personnalisés
- Téléchargements disponibles
- Historique des exports

### 4.3 Composants d'Interface

- **Sidebar de navigation** : accès aux modules principaux
- **Breadcrumb** : navigation dans les niveaux
- **Notifications toast** : confirmations d'actions
- **Modals** : création/édition rapide
- **Tooltips** : aide contextuelle
- **Badges de statut** : codes couleur pour les états

---

## 5. Architecture Technique

### 5.1 Stack Technologique

**Backend**
- **Django 4.2+ LTS** : framework principal
- **Python 3.11+** : langage de développement
- **PostgreSQL 14+** : base de données principale
- **Redis** : cache et sessions (optionnel)

**Frontend**
- **Django Templates** : rendu HTML côté serveur
- **Bootstrap 5.3** : framework CSS responsive
- **jQuery 3.6** : interactions JavaScript
- **Chart.js 4.0** : graphiques et visualisations
- **DataTables** : tableaux interactifs avec tri/filtres

**Bibliothèques Python**
- **Django-extensions** : outils de développement
- **Django-crispy-forms** : amélioration des formulaires
- **Pillow** : gestion des images
- **openpyxl** : export Excel
- **reportlab** : génération PDF
- **django-environ** : gestion configuration
- **django-crontab** : tâches automatisées

### 5.2 Structure de Base de Données

**Tables principales**

```sql
-- Sous-traitants
contractors (
    id, name, email, phone, contact_person,
    sla_response_time, sla_resolution_time,
    is_active, created_at, updated_at
)

-- Projets
projects (
    id, name, description, start_date, end_date,
    status, contractor_id, budget, priority,
    completion_percentage, created_at, updated_at
)

-- Problèmes/Incidents
problems (
    id, title, description, problem_type, urgency,
    affected_service, affected_user, detected_at,
    impact_level, initial_analysis, treatment_decision,
    project_id, created_at, updated_at
)

-- Tickets
tickets (
    id, number, external_reference, category,
    problem_id, contractor_id, status, priority,
    estimated_time, actual_time, estimated_cost,
    actual_cost, solution, satisfaction_rating,
    opened_at, first_response_at, resolved_at,
    closed_at, created_at, updated_at
)

-- Communications Email
email_communications (
    id, ticket_id, subject, content, recipients,
    sent_at, response_received_at, is_outgoing,
    template_used, created_at, updated_at
)

-- Pièces jointes
attachments (
    id, name, file_path, file_size, content_type,
    linked_to_type, linked_to_id, uploaded_at
)

-- Historique/Audit
audit_logs (
    id, table_name, record_id, action_type,
    field_changes, user_action, timestamp
)

-- Templates Email
email_templates (
    id, name, subject_template, content_template,
    variables, is_active, created_at, updated_at
)

-- Notifications/Rappels
notifications (
    id, type, title, message, related_to_type,
    related_to_id, is_read, priority, created_at
)
```

### 5.3 Architecture Applicative

**Structure Django**
```
project_rsi/
├── manage.py
├── requirements.txt
├── config/
│   ├── settings/
│   │   ├── base.py
│   │   ├── development.py
│   │   └── production.py
│   ├── urls.py
│   └── wsgi.py
├── apps/
│   ├── core/           # Modèles communs, utilitaires
│   ├── projects/       # Gestion projets
│   ├── problems/       # Problèmes et incidents
│   ├── tickets/        # Gestion tickets
│   ├── contractors/    # Sous-traitants
│   ├── communications/ # Emails et messages
│   ├── notifications/  # Alertes et rappels
│   └── reports/        # Exports et rapports
├── templates/
│   ├── base.html
│   ├── dashboard/
│   ├── projects/
│   ├── tickets/
│   └── reports/
├── static/
│   ├── css/
│   ├── js/
│   └── img/
└── media/              # Fichiers uploadés
```

### 5.4 Modèles Django Principaux

**Exemple de modèle Ticket**
```python
class Ticket(models.Model):
    STATUS_CHOICES = [
        ('new', 'Nouveau'),
        ('assigned', 'Assigné'),
        ('in_progress', 'En cours'),
        ('waiting_client', 'En attente client'),
        ('waiting_contractor', 'En attente sous-traitant'),
        ('resolved', 'Résolu'),
        ('closed', 'Fermé'),
    ]
    
    number = models.CharField(max_length=20, unique=True)
    problem = models.ForeignKey('problems.Problem', on_delete=models.CASCADE)
    contractor = models.ForeignKey('contractors.Contractor', on_delete=models.CASCADE)
    status = models.CharField(max_length=20, choices=STATUS_CHOICES, default='new')
    # ... autres champs
    
    class Meta:
        ordering = ['-created_at']
        verbose_name = 'Ticket'
        verbose_name_plural = 'Tickets'
```

---

## 6. Contraintes Techniques

### 6.1 Contraintes de Performance

- Temps de réponse page < 2 secondes
- Support jusqu'à 10 000 tickets simultanés
- Optimisation des requêtes SQL (select_related, prefetch_related)
- Pagination des listes longues (50 éléments/page)

### 6.2 Contraintes de Sécurité

- Authentification simple par session Django
- Protection CSRF activée
- Validation côté serveur de tous les formulaires
- Uploads de fichiers sécurisés (types autorisés, taille limitée)
- Sauvegarde automatique de la base de données

### 6.3 Contraintes d'Environnement

- Déploiement sur serveur Linux (Ubuntu/CentOS)
- Compatible avec Python 3.11+
- Base de données PostgreSQL recommandée
- Serveur web Apache/Nginx + uWSGI
- SSL/TLS obligatoire en production

### 6.4 Contraintes de Maintenance

- Code documenté et commenté
- Tests unitaires pour les fonctions critiques
- Logs détaillés des actions utilisateur
- Migration de données simplifiée
- Interface d'administration Django accessible

---

## 7. Suggestions d'Évolutions Futures

### 7.1 Évolutions à Court Terme (6 mois)

**Intégrations email automatiques**
- Connexion IMAP pour récupération automatique des réponses
- Parsing intelligent des emails pour mise à jour des tickets
- Envoi automatique d'emails depuis l'application

**Améliorations UX**
- Interface mobile native (PWA)
- Notifications push navigateur
- Raccourcis clavier pour actions fréquentes
- Mode sombre/clair

### 7.2 Évolutions à Moyen Terme (1 an)

**Analytics avancées**
- Machine learning pour prédiction des délais
- Détection automatique de patterns dans les problèmes
- Recommandations d'optimisation
- Comparaison avec benchmarks sectoriels

**Intégrations externes**
- API REST pour connexion avec ERP
- Synchronisation avec calendriers (Outlook, Google)
- Connexion avec outils de monitoring (Nagios, Zabbix)
- Intégration messagerie instantanée (Slack, Teams)

### 7.3 Évolutions à Long Terme (2+ ans)

**Multi-utilisateurs limité**
- Accès en lecture pour direction
- Collaboration avec sous-traitants via portail dédié
- Gestion des rôles et permissions

**Intelligence artificielle**
- Chatbot pour création rapide de tickets
- Classification automatique des problèmes
- Suggestion de solutions basée sur l'historique
- Génération automatique de rapports intelligents

---

## 8. Annexes

### 8.1 Wireframes Conceptuels

**Dashboard Principal**
```
┌─────────────────────────────────────────────────────────┐
│ [Logo] RSI Tracker                    [Profile] [Logout]│
├─────────────────────────────────────────────────────────┤
│ Dashboard │ Projets │ Tickets │ Comms │ Rapports        │
├─────────────────────────────────────────────────────────┤
│                                                         │
│ ┌─── Alertes ───┐ ┌─── Statistiques ───┐ ┌─── Activité ─┐│
│ │ 🔴 3 Urgents  │ │ 📊 15 Tickets     │ │ ⏰ Dernières ││
│ │ ⚠️  7 En retard│ │    ouverts        │ │    actions   ││
│ │ ✅ 2 À fermer │ │ 📈 85% SLA resp.  │ │              ││
│ └───────────────┘ └───────────────────┘ └──────────────┘│
│                                                         │
│ ┌─── Projets en cours ─────────────────────────────────┐│
│ │ Projet A ████████░░ 80% │ Migration serveurs        ││
│ │ Projet B ████░░░░░░ 40% │ Mise à jour ERP          ││
│ └───────────────────────────────────────────────────────┘│
└─────────────────────────────────────────────────────────┘
```

**Liste des Tickets**
```
┌─────────────────────────────────────────────────────────┐
│ Tickets                               [+ Nouveau Ticket]│
├─────────────────────────────────────────────────────────┤
│ Filtres: [Statut ▼][Sous-traitant ▼][Urgence ▼] [🔍]   │
├─────────────────────────────────────────────────────────┤
│ # │ Titre                │ Statut    │ Sous-traitant │ Maj│
│ 001│🔴 Panne serveur prod │ En cours  │ TechCorp      │1j │
│ 002│⚠️  Bug logiciel      │ Assigné   │ DevSoft       │3j │
│ 003│✅ Installation PC    │ Résolu    │ Hardware+     │1h │
└─────────────────────────────────────────────────────────┘
```

### 8.2 Dictionnaire de Données

**Niveaux d'urgence**
- **Critique** : Arrêt de production, sécurité compromise
- **Élevé** : Impact significatif sur l'activité
- **Modéré** : Gêne dans le travail quotidien
- **Faible** : Amélioration ou demande non urgente

**Types de problèmes**
- **Hardware** : Serveurs, postes de travail, équipements réseau
- **Software** : Applications métier, OS, logiciels bureautiques
- **Réseau** : Connectivité, débit, Wi-Fi
- **Sécurité** : Intrusions, mises à jour sécurité, antivirus
- **Autre** : Formation, conseil, audit

### 8.3 Matrice de Décision SLA

| Urgence/Impact | Faible | Modéré | Élevé | Critique |
|----------------|--------|--------|-------|----------|
| **Critique**   | 4h     | 2h     | 1h    | 30min    |
| **Élevé**      | 8h     | 4h     | 2h    | 1h       |
| **Modéré**     | 1j     | 8h     | 4h    | 2h       |
| **Faible**     | 3j     | 1j     | 8h    | 4h       |

### 8.4 Planning de Développement Suggéré

**Phase 1 - Core (4 semaines)**
- Modèles de données et migrations
- Authentification basique
- CRUD projets et problèmes
- Interface de base

**Phase 2 - Tickets (3 semaines)**
- Gestion complète des tickets
- Workflow de statuts
- Association problèmes/tickets
- Historique des modifications

**Phase 3 - Communications (2 semaines)**
- Gestion des emails
- Templates et variables
- Association avec tickets

**Phase 4 - Dashboard & Rapports (2 semaines)**
- Tableaux de bord
- Graphiques et métriques
- Exports Excel/PDF

**Phase 5 - Notifications (1 semaine)**
- Système d'alertes
- Rappels automatiques
- Configuration des seuils

**Phase 6 - Tests & Déploiement (1 semaine)**
- Tests de validation
- Documentation utilisateur
- Mise en production

---

**Total estimé : 13 semaines de développement**

Ce cahier des charges constitue un guide complet pour le développement de votre application de suivi RSI. Il peut être adapté selon vos priorités et contraintes spécifiques.