# Installation

## Exercice 1 
- Démarrez la VM ubuntu depuis le répertoire atelier-01
```
vagrant up ubuntu
```
- Connectez-vous à cette VM 
```
vagrant ssh ubuntu
```
- Rafraîchissez les informations sur les paquets
`sudo apt update`
- Recherchez le paquet ansible avec les options qui vont bien.
`apt-cache search -names-only ansible`
- Installez le paquet officiel fourni par la distribution.
`sudo apt install -y ansible`
- Vérifiez si l’installation s’est bien déroulée.
`ansible --v`
- Notez la version d’Ansible.
`ansible 2.10.8`
- Déconnectez-vous et supprimez la VM.
```
exit
vagrant destroy -f ubuntu
```
## Exercice 2
`sudo apt-add repository ppa:ansible/ansible`
`ansible [core 2.17.9]`

## Exercice 3
- Lancez une VM Rocky Linux et installez Ansible en utilisant PIP et Virtualenv.
```
vagrant up rocky
vagrant ssh rocky
sudo dnf install python3
python3 -m venv ~/.venv/ansible
source ~/.venv/ansible/bin/activate
pip install --upgrade pip
pip install ansible
ansible --version => ansible [core 2.15.13]
deactivate
exit
vagrant destroy -f debian
```
