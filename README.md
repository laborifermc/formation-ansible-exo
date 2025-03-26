# Formation Ansible

Ce dépôt contient des ressources et des scripts pour la configuration et l'automatisation de divers services avec Ansible en lien avec cette formation..

## Répertoires

Voici la structure des répertoires de ce projet :

- [01-installation](./01-installation/)  
  Contient des scripts et des instructions pour l'installation des services et des applications nécessaires.

- [02-authentification](./02-authentification/)  
  Comprend des ressources et des scripts pour la mise en place de mécanismes d'authentification.

- [03-configuration-de-base](./03-configuration-de-base/)  
  Contient des fichiers de configuration de base pour divers services et applications.

- [04-idempotence](./04-idempotence/)  
  Ce répertoire traite des concepts d'idempotence dans les scripts et les playbooks, garantissant que les opérations peuvent être répétées sans effets indésirables.

- [05-apache](./05-apache/)  
  Contient des configurations et des scripts relatifs à l'installation et à la gestion du serveur Apache.

- [06-handler](./06-handler/)  
  Comprend des handlers utilisés pour gérer les notifications et les redémarrages de services dans les playbooks.

- [07-variables](./07-variables/)  
  Comprend des fichiers de variables utilisés pour personnaliser les configurations dans les playbooks.

- [08-variable-enregistrees](./08-variable-enregistrees/)  
  Ce répertoire contient des variables enregistrées utilisées dans les playbooks Ansible pour la configuration dynamique.

- [09-facts-et-variables-implicites](./09-facts-et-variables-implicites/)  
  Ce répertoire contient des informations sur les faits et les variables implicites utilisés dans les playbooks Ansible.

- [10-cibles-heterogenes](./10-cibles-heterogenes/)  
  Contient des ressources et des scripts pour gérer des cibles hétérogènes dans des environnements d'automatisation.

- [11-jinja-templates](./11-jinja-templates/)  
  Contient des modèles Jinja utilisés pour générer des fichiers de configuration dynamiques.


## Installation

Pour cloner ce dépôt, utilisez la commande suivante :

```bash
git clone https://github.com/vlaborifermc/formation-ansible-exo.git
