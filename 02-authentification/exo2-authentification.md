# Authentification sur les Target Hosts

## Exercie
- Placez-vous dans le répertoire du troisième atelier pratique
`cd ~/formation-ansible/atelier-03`
- Création des machines virtuelles Ubuntu 22.04 de cet atelier
`vagrant up
- Connectez-vous au Control Host
`vagrant ssh control`
- Faire le nécessaire pour réussir un ping Ansible 
```
Dans /etc/hosts : 
192.168.56.10 control
192.168.56.20 target01
192.168..56.30 target02
192.168..56.40 target03

Collecte des clés SSH publiques : 
ssh-keyscan -t rsa target01 target02 target03 >> .ssh/known_hosts

Création d'une clé sur control : 
ssh-keygen
Distribution de la clé publique :
ssh-copy-id vagrant@target01 (mdp : vagrant)
ssh-copy-id vagrant@target02 (mdp : vagrant)
ssh-copy-id vagrant@target03 (mdp : vagrant)
```
- Résultat
```
ansible all -i target01,target02,target03 -m ping
target03 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
target01 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
target02 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
```
