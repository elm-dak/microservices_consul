# TP 2 : Migration de Eureka à Consul

## Description du Projet
Ce projet présente les étapes nécessaires pour migrer un ensemble de microservices utilisant Eureka vers Consul. Cette migration vise à moderniser l'architecture de découverte de services, en adoptant Consul, un outil open-source de HashiCorp qui offre des fonctionnalités avancées de découverte de services, de gestion de configuration, et de segmentation réseau.

## Objectifs
- **Modernisation de l'infrastructure** : Améliorer l'architecture de découverte de services en remplaçant Eureka par Consul.
- **Gestion de la configuration** : Faciliter la gestion de la configuration des microservices à travers une solution centralisée.
- **Scalabilité et Résilience** : Augmenter la résilience et la scalabilité de l'infrastructure grâce aux fonctionnalités avancées de Consul.

## Prérequis
Avant de commencer, assurez-vous de disposer des éléments suivants :
- [Git](https://git-scm.com/downloads) pour cloner le projet
- [Java](https://www.oracle.com/java/technologies/javase-downloads.html) et [Maven](https://maven.apache.org/download.cgi) pour compiler et exécuter les microservices
- [Consul](https://www.consul.io/downloads) pour le déploiement du service de découverte

## Étapes de la Migration

### 1. Préparation et Vérification des Microservices
1. Clonez le dépôt du projet initial :
    ```bash
    git clone https://github.com/elm-dak/App_microservices.git
    ```
2. Lancez chaque microservice localement pour valider leur bon fonctionnement sous Eureka :
    ```bash
    mvn spring-boot:run
    ```
3. Vérifiez que chaque service est bien enregistré dans Eureka et qu'il fonctionne comme prévu.

### 2. Installation de Consul
1. Téléchargez la dernière version de Consul depuis le [site officiel de HashiCorp](https://www.consul.io/downloads).
2. Extrayez le fichier téléchargé dans un répertoire dédié (par exemple, `C:\consul` sur Windows ou `/usr/local/bin/consul` sur Linux).
3. Ajoutez le répertoire de Consul à la variable d'environnement **PATH** :
   - **Sous Windows** : Ajoutez `C:\consul` dans les variables d'environnement.
   - **Sous Linux/Mac** : Ajoutez la ligne suivante dans le fichier `~/.bashrc` ou `~/.zshrc` :
     ```bash
     export PATH=$PATH:/usr/local/bin/consul
     ```
4. Démarrez Consul en mode développement pour tester la configuration :
    ```bash
    consul agent -dev
    ```

### 3. Configuration des Microservices pour Utiliser Consul
1. **Modification de la configuration** : Dans chaque microservice, configurez Consul comme service de découverte. Mettez à jour les fichiers `application.yml` ou `application.properties` comme suit :
    ```yaml
    spring:
      cloud:
        consul:
          host: localhost
          port: 8500
          discovery:
            enabled: true
            service-name: nom-du-service
    ```
2. **Désactiver Eureka** : Retirez les dépendances et configurations liées à Eureka dans chaque microservice.
3. **Redéploiement des microservices** : Redémarrez chaque microservice pour qu'il s'enregistre désormais dans Consul.

### 4. Vérification et Tests
- Accédez à l'interface web de Consul pour vérifier l'enregistrement des services : [http://localhost:8500/ui](http://localhost:8500/ui).
- Assurez-vous que tous les microservices sont listés et peuvent être découverts via Consul.

## Documentation Supplémentaire
Pour des informations plus détaillées sur la configuration de Consul et ses fonctionnalités, veuillez consulter la [documentation officielle de Consul](https://www.consul.io/docs).

## Auteur
Ce projet a été réalisé dans le cadre du TP 2 de la formation en architecture des microservices.

---

