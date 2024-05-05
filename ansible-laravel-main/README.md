# Projet Laravel avec Ansible

Ce projet utilise Ansible pour automatiser le déploiement et la gestion de la configuration d'une application Laravel sur des serveurs de production et de staging.

## Author 

- [El Mahdi Bouaiti] = (https://github.com/elmahdibouaiti)
- [Omar Moloudi] = (https://github.com/elmahdibouaiti)

## Prérequis

- Ansible 2.9 ou plus récent.
- Serveurs avec Ubuntu 20.04 (ou toute autre distribution compatible).
- Accès SSH configuré pour les machines cibles.
- Git, PHP, Composer, et MySQL doivent être installés sur les serveurs cibles pour le déploiement.

## Structure du projet

Le projet est structuré comme suit :

```bash
project-root/
│
├── ansible/
│ ├── inventory/
│ │ ├── production.yml
│ │ └── staging.yml
│ ├── roles/
│ │ ├── nginx/
│ │ ├── php/
│ │ ├── mysql/
│ │ └── laravel/
│ ├── playbooks/
│ │ ├── setup.yml
│ │ └── deploy.yml
│ └── ansible.cfg
│
├── laravel/
│ └── (dossiers de l'application Laravel)
│
├── .gitignore
└── README.md
```

## Configuration

1. **Ansible**: Configurer les fichiers `inventory` pour pointer vers vos serveurs de staging et de production.
2. **Variables**: Définir les variables nécessaires dans les dossiers `group_vars` ou `host_vars` selon l'environnement.

## Déploiement

Pour déployer l'application, utilisez les commandes suivantes :

- Pour le staging :
```bash
  ansible-playbook -i ansible/inventory/staging.yml ansible/playbooks/deploy.yml
```

- Pour la production :
```bash
  ansible-playbook -i ansible/inventory/production.yml ansible/playbooks/deploy.yml
```

## Setup Nginx
Pour configurer Nginx sur les serveurs cibles, exécutez la commande suivante :
```bash
ansible-playbook -i inventory/staging.yml playbooks/setup_nginx.yml
ansible-playbook -i inventory/production.yml playbooks/setup_nginx.yml
```

## Lancement de l'application
Après le déploiement, vous pouvez lancer l'application en naviguant vers l'adresse IP ou le domaine configuré de votre serveur. Assurez-vous que les services web et PHP sont en cours d'exécution.

Pour vérifier le statut de l'application et effectuer des opérations initiales, vous pouvez exécuter :

```bash
# Naviguer dans le répertoire de l'application
cd /var/www/app

# Lancer les migrations de la base de données
php artisan migrate

# Lancer les seeders de la base de données
php artisan db:seed

# Lancer le cache pour optimiser les performances de l'application
php artisan config:cache
# Lancer le serveur de développement
php artisan serve
```
