# Application de Suivi RSI – Gestion des Projets et Tickets IT

Bienvenue dans cette application développée pour répondre aux besoins spécifiques d’un **Responsable des Systèmes Informatiques (RSI)** .

Elle a pour but de centraliser la **gestion des problèmes informatiques**, le **suivi des demandes internes**, et la **communication avec les sous-traitants IT**, tout en facilitant la **traçabilité** des actions.

---

## Pourquoi cette application ?

Dans un environnement où les sollicitations informatiques sont nombreuses, et où plusieurs sous-traitants peuvent être impliqués, il devient difficile de :

* Suivre les tickets envoyés par email
* Savoir si un problème a été résolu ou non
* Ne pas perdre le fil des demandes internes
* Organiser les projets informatiques

Cette application vous permettra de ne plus rien oublier et d’avoir une **vue d’ensemble claire et simple** sur vos activités IT.

---

## Fonctionnalités principales

### 1. Suivi des projets

* Créez des projets et associez-y des demandes ou des incidents.
* Suivez leur avancement au fil du temps.

### 2. Déclaration de problèmes

* Centralisez toutes les réclamations : collaborateurs, erreurs systèmes, incidents matériels, etc.
* Chaque problème peut être documenté, priorisé et tracé.

### 3. Affectation des tickets

* Décidez si vous traitez un problème en interne ou si vous devez le transmettre à un sous-traitant.
* Chaque ticket transmis peut être suivi de bout en bout.

### 4. Suivi des sous-traitants

* Historique des emails envoyés pour chaque problème.
* Suivi de l’état des tickets (en attente, en cours, résolu).
* Archivage automatique des tickets fermés.

### 5. Tableau de bord

* Visualisez en un coup d’œil l’état de vos projets et incidents.
* Filtrez par projet, priorité, date, ou sous-traitant.

---

## Technologies utilisées

* Django 5 (framework web backend)
* PostgreSQL (base de données relationnelle)
* HTML / CSS / Bootstrap (interface simple et responsive)
* SMTP / IMAP (gestion des emails automatisée – à configurer)

---

## Lancer le projet en local

1. Clonez ce dépôt :

```bash
git clone https://votre-url-depot.git
cd nom-du-projet
```

2. Créez un environnement virtuel :

```bash
python -m venv env
source env/bin/activate
```

3. Installez les dépendances :

```bash
pip install -r requirements.txt
```

4. Lancez les migrations :

```bash
python manage.py migrate
```

5. Démarrez le serveur :

```bash
python manage.py runserver
```

6. Accédez à l’application via :

```
http://127.0.0.1:8000/
```

---

## À venir (fonctionnalités futures)

* Connexion automatique à une boîte email (IMAP) pour lire les réponses aux tickets
* Génération automatique de rapports PDF
* Application mobile complémentaire
* Interface pour les sous-traitants

---

## Contact

Développé par un RSI, pour les RSI.
Pour toute remarque, suggestion ou contribution, n’hésitez pas à me contacter.


