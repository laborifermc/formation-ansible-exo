# Execercie de Configuration de base

- Éditez /etc/hosts de manière à ce que les Target Hosts soient joignables par leur nom d’hôte simple.
```
vim /etc/hosts
192.168.56.20 target01
192.168.56.30 target02
192.168.56.40 target03
```
- Configurez l’authentification par clé SSH avec les trois Target Hosts.
```
Collecte des clés ssh : 
ssh-keyscan -t rsa target01 target02 target03 >> .ssh/known_hosts
ssh-keygen
ssh-copy-id vagrant@target01
ssh-copy-id vagrant@target02
ssh-copy-id vagrant@target03
```
- Installez Ansible.
```
cat /etc/os-release => on voit que c'est ubuntu
sudo apt install ansible
```
- Envoyez un premier ping Ansible sans configuration.
```
ansible all -i target01,target02,target03 -u vagrant -m ping
target01 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
target03 | SUCCESS => {
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
- Créez un répertoire de projet ~/monprojet.
`mkdir ~/monprojet`
- Créez un fichier vide ansible.cfg dans ce répertoire.
`touch ~/monprojet/ansible.cfg`
- Vérifiez si ce fichier est bien pris en compte par Ansible.
```
cd ~/monprojet
ansible --version | head -n 2
ansible 2.10.8
  config file = /home/vagrant/monprojet/ansible.cfg
```
- Spécifiez un inventaire nommé hosts.
```
vim ansible.cfg : 
[defaults]
inventory = ./hosts
```
- Activez la journalisation dans ~/journal/ansible.log.
```
 mkdir -v ~/journal
vim ansible.cfg : dans [defaults]
log_path = ~/journal/ansible.log

```
- Testez la journalisation.
```
vagrant@control:~/monprojet$ ansible all -i target01,target02,target03 -m ping
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
}
target03 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
vagrant@control:~/monprojet$ cat ~/journal/ansible.log 
2025-03-25 09:45:50,616 p=2869 u=vagrant n=ansible | target01 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
2025-03-25 09:45:50,618 p=2869 u=vagrant n=ansible | target02 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
2025-03-25 09:45:50,632 p=2869 u=vagrant n=ansible | target03 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```
- Créez un groupe [testlab] avec vos trois Target Hosts.
```
vim hosts : 
[testlab]
target01
target02
target03
```
- Définissez explicitement l’utilisateur vagrant pour la connexion à vos cibles.
```
vim hosts : 
[testlab:vars]
ansible_user=vagrant

```
- Envoyez un ping Ansible vers le groupe de machines [all].
```
ansible all -m ping
target02 | SUCCESS => {
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
target03 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```
- Définissez l’élévation des droits pour l’utilisateur vagrant sur les Target Hosts.
```
Dans hosts, [testlab:vars] 
ansible_become=yes
```
- Affichez la première ligne du fichier /etc/shadow sur tous les Target Hosts.
```
ansible all -a "head -n 1 /etc/shadow"
target01 | CHANGED | rc=0 >>
root:*:19977:0:99999:7:::
target02 | CHANGED | rc=0 >>
root:*:19977:0:99999:7:::
target03 | CHANGED | rc=0 >>
root:*:19977:0:99999:7:::
```
- Quittez le Control Host et supprimez toutes les VM de l’atelier.
```
exit
vagrant destroy -f
```
