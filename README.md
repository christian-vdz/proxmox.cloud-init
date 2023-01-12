# Proxmox Cloud-Init

Exemples de fichiers de configuration Cloud-Init.  
*Supposant que Cloud-Init est installé sur votre machine virtuelle et que son VM ID est l'ID 101.*

- `cloud-init_ssh.yml`  
Ce fichier de configuration modifie le nom d'hôte de la VM, met à jour les paquets installés, met à jour le fuseau horaire et la configuration de langue. Il exécute également des commandes `sed` visant à modifier la configuration du daemon SSHD afin d'interdire la connexion par mot de passe puis relance le service.

- `cloud-init_docker.yml`
Ce fichier de configuration modifie le nom d'hôte de la VM, met à jour les dépôts locaux, installe divers paquets puis execute les lignes de commandes qui permettent d'installer Docker sur la machine virtuelle.

Comment utiliser ces fichiers de configuration ?

1. Créer un dossier cloud-init dans le volume par défaut de Proxmox `mkdir /var/lib/vz/cloud-init/`
2. Télécharger le fichier Cloud-Init d'exemple qui vous intéresse :
    - cloud-init_ssh.yml : `wget -O /var/lib/vz/cloud-init/101-config.yml wget https://raw.githubusercontent.com/fyc-proxmox/proxmox.cloud-init/main/cloud-init_ssh.yml`
    - cloud-init_docker.yml : `wget -O /var/lib/vz/cloud-init/101-config.yml wget https://raw.githubusercontent.com/fyc-proxmox/proxmox.cloud-init/main/cloud-init_docker.yml`
3. Ajouter le fichier de configuration à la marchine virtuelle `qm set 101 --cicustom "user=local:snippets/101-config.yml"`
4. Démarrer la machine virtuelle

*Ces fichiers de configuration ont été crées pour l'image Cloud Ubuntu Server 22.04.*
