# Ansible
Collection de playbook ansible pour la configuration des EC2 pour le projet Mondecole.


| Playbook             | Utilité          | 
| :--------------------| :--------------- | 
| ``install_ssh_keys`` | Installe les clés SSH de l'équipe IT sur le host |
| `rename_user`        | Renomme l'utilisateur admin par défaut (**example**) en **admin** | 
| `ddns`               | Implémente le service DDNS pour le host _(map ip publique aws a hostname.dev)_ | 
| `docker_install`     | Installe les repos et le runtime **Docker** |



<br>


### Install SSH keys

Installe les clés SSH de l'équipe `devops/prod` ainsi que la clé de `jenkins`. Si vous souhaitez **ajouter votre clé SSH**, vous devez modifier le fichier [authorized_keys](https://github.com/mondecole/Ansible/blob/main/files/authorized_keys) et l'ajouter.

```bash
ansible-playbook -i inventory.ini -l [TARGET_NAME] install_ssh_keys.yml.yml
```


### Rename user

```bash
ansible-playbook -i inventory.ini -l [TARGET_NAME] rename_user.yml
```

Par défaut le user source est `example`, et le user destination `admin`. Vous pouvez changer ce comportement en 
utilisant l'option `-e` et en écrasant les variables suivantes:

- **old_user** `(default: example)`
- **new_user** `(default: admin)`
- **ansible_user** `(default: admin, user utilisé pour la connexion SSH)`


### DDNS

Les IP publiques attribuée par AWS aux EC2 sont dynamiques _(elles changent à chaque démarrage)_, donc on ne peut pas faire du DNS classique
 
```bash
ansible-playbook -i inventory.ini -l [TARGET_NAME] ddns.yml
```

Ce playbook installe un [service systemd](https://github.com/mondecole/Ansible/blob/main/files/update-dns.service) qui lance un [script bash](https://github.com/mondecole/Ansible/blob/main/templates/update-dns.sh.j2) qui utilise le protocole **DDNS** pour update le **A RECORD** `[hostname].mondecole.com` avec l'IP publique attribuée dynamiquement par AWS.


### Docker install

Installe les repo de docker, update la repo list, et installe Docker et le Docker-engine ainsi que le plugin Docker-Compose. Ajoute également l'user admin au groupe Docker.

```bash
ansible-playbook -i inventory.ini -l [TARGET_NAME] docker_install.yml
```



