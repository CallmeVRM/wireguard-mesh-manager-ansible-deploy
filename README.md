# wireguard-mesh-manager-ansible-deploy
Déployez les fichiers de configurer générés avec Wireguard Mesh Manager

## 🧱 Structure du projet
```bash


.
├── inventory.ini
├── playbook_install_wireguard.yml     
├── playbook_wireguard.yml             
└── roles/
    ├── wireguard_install/
    │   └── tasks/main.yml
    └── wireguard_config/
        ├── tasks/
        │   ├── main.yml
        │   ├── verify.yml
        │   └── rollback.yml
        └── handlers/main.yml
        └── files/
            ├── node01.conf
            ├── node02.conf
            └── node03.conf
```

## Clonez la répository :

git clone && cd 

## 🗂️ inventory.ini
Chaque serveur est associé à son fichier de configuration :
PS : `wg_conf_file=node-prod-services-ipv4.conf  (selon la convention, node-<nom_que_vous_avez_choisis>.conf)`
```bash
[wireguard_nodes]
prod-services-ipv4 ansible_host=20.51.131.162 wg_conf_file=node-prod-services-ipv4.conf
prod-databases-ipv4 ansible_host=172.190.75.205 wg_conf_file=node-prod-databases-ipv4.conf
prod-monitoring-ipv4 ansible_host=14.236.132.228 wg_conf_file=node-prod-monitoring-ipv4.conf
```

## Organisation des playbooks WireGuard

Le déploiement de WireGuard repose sur deux playbooks distincts :
    Installation : playbook_install_wireguard.yml utilise le rôle wireguard_install.
    Configuration : playbook_config_wireguard.yml s'appuie sur le rôle wireguard_config.

## Fonctionnement du rôle de configuration
Ce rôle permet de paramétrer WireGuard selon les besoins définis dans votre inventaire et vos variables. Il gère la création des clés, la configuration des interfaces, et l’ajout des pairs.
Exécution des playbooks
Avant de lancer les commandes, assurez-vous que :
    Vous disposez d’un accès SSH par clé.
    Un agent SSH est actif pour gérer l’authentification.
    
### Installation :  
ansible-playbook -i inventory.ini playbook_install_wireguard.yml

### Configuration :  
ansible-playbook -i inventory.ini playbook_config_wireguard.yml
