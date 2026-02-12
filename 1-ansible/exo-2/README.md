# Exo 2 - Serveurs Web Nginx & HAProxy

## Prérequis système (Debian/Ubuntu)

```bash
# Mise à jour des paquets et installation de pipx (pour isoler ansible)
apt update
apt install pipx -y

# Installation d'Ansible via pipx
pipx install ansible-core
pipx ensurepath
source ~/.bashrc

# Vérifier l'installation
ansible --version
```

## Dépendances Ansible Galaxy

```bash
# Installer les rôles listés dans requirements.yml (geerlingguy.nginx, geerlingguy.haproxy)
ansible-galaxy install -r requirements.yml
```

## Exécution du playbook

```bash
# Lancer le playbook avec le fichier d'inventaire hosts
ansible-playbook -i ./hosts playbook_exo2.yml
```

## Accès à l'application

```bash
# Afficher l'URL du load balancer HAProxy
echo -e "\nhttp://$(ANSIBLE_PYTHON_INTERPRETER=auto_silent ansible -i hosts haproxy -m command -a 'hostname'  | tail -n 1).peperelab.com/proxy/80/ \n"
```
