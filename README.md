# Objectifs

- [ ] surveiller les paramètres environnementaux des équipements réseaux
- [ ] Collecter la version du système d’exploitation des équipements réseau
- [ ] Afficher l’état des interfaces des équipements réseaux
- [ ] réaliser une sauvegarde ou une restauration des fichiers de configuration des équipements réseau sur un serveur tftp local.
- [ ] Mettre en place la synchronisation NTP pour l’ensemble des équipements réseaux.

# Commandes
- Tester les pings
```
ansible all -i inventory.ini -m ping
```
