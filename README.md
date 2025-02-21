### TP Ansible

## Exercice 1 

# Démarrez la VM ubuntu depuis le répertoire atelier-01.
``` 
[ema@2a02-8440-c115-db0c-b6ac-ae24-d16a-c530:~] $ cd formation-ansible/
[ema@2a02-8440-c115-db0c-b6ac-ae24-d16a-c530:formation-ansible] $ cd atelier-01/
[ema@2a02-8440-c115-db0c-b6ac-ae24-d16a-c530:atelier-01] $ ls
setup-rocky.sh  Vagrantfile
[ema@2a02-8440-c115-db0c-b6ac-ae24-d16a-c530:atelier-01] $ vagrant up ubuntu
```

# Connectez-vous à cette VM.
```
[ema@2a02-8440-c115-db0c-b6ac-ae24-d16a-c530:atelier-01] $ vagrant ssh ubuntu
Welcome to Ubuntu 22.04.4 LTS (GNU/Linux 5.15.0-116-generic x86_64)
```

# Rafraîchissez les informations sur les paquets.
```
vagrant@ubuntu:~$ sudo apt install
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
```

# Recherchez le paquet ansible avec les options qui vont bien.
```
vagrant@ubuntu:~$ apt-cache search --names-only ansible
ansible - Configuration management, deployment, and task execution system
ansible-core - Configuration management, deployment, and task execution system
ansible-lint - lint tool for Ansible playbooks
ansible-mitogen - Fast connection strategy for Ansible
python-ansible-runner-doc - library that interfaces with Ansible (docs)
python-networking-ansible-doc - OpenStack virtual network service - Ansible plugin (docs)
python3-ansible-runner - library that interfaces with Ansible (Python 3.x)
python3-networking-ansible - OpenStack virtual network service - Ansible plugin (Python 3.x)
```

# Installez le paquet officiel fourni par la distribution.
```
vagrant@ubuntu:~$ sudo apt install -y ansible
```

# Vérifiez si l’installation s’est bien déroulée et notez la version d’Ansible.
```
vagrant@ubuntu:~$ ansible --version
ansible 2.10.8
  config file = None
  configured module search path = ['/home/vagrant/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  executable location = /usr/bin/ansible
  python version = 3.10.12 (main, Mar 22 2024, 16:50:05) [GCC 11.4.0]
```

#Déconnectez-vous et supprimez la VM.
```
vagrant@ubuntu:~$ exit
logout
Connection to 127.0.0.1 closed.

[ema@2a02-8440-c115-db0c-b6ac-ae24-d16a-c530:atelier-01] $ vagrant destroy -f ubuntu
==> ubuntu: Forcing shutdown of VM...
==> ubuntu: Destroying VM and associated drives...
```


## Exercice 2
# Répétez l’exercice précédent en configurant un dépôt PPA (Personal Package Archive) pour Ansible :
```
$ sudo apt-add-repository ppa:ansible/ansible
```
# Notez la version fournie par ce dépôt tiers et comparez avec la version officielle de l’exercice précédent.


Reprise de l'exercice 1 jusqu'a la connection à la VM : 
```
vagrant@ubuntu:~$  sudo apt-add-repository ppa:ansible/ansible
vagrant@ubuntu:~$ sudo apt update
vagrant@ubuntu:~$ sudo apt install ansible
vagrant@ubuntu:~$ ansible --version
ansible [core 2.17.8]
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/home/vagrant/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  ansible collection location = /home/vagrant/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/bin/ansible
  python version = 3.10.12 (main, Mar 22 2024, 16:50:05) [GCC 11.4.0] (/usr/bin/python3)
  jinja version = 3.0.3
  libyaml = True
```
La version est plus récente

```
vagrant@ubuntu:~$ exit
logout
Connection to 127.0.0.1 closed.
[ema@2a02-8440-c115-db0c-b6ac-ae24-d16a-c530:atelier-01] $ vagrant destroy -f ubuntu
```


## Exercice 3
Connection à la Vm Rocky, puis rafraîchissement des paquetes et installation de pip : 
```
[vagrant@rocky ~]$ sudo dnf check-update
[vagrant@rocky ~]$ sudo dnf install python3-pip

Installed:
  python3-pip-21.3.1-1.el9.noarch                      python3-setuptools-53.0.0-13.el9.noarch                     

Complete!
```
Initialisation et lancement de Virtualenv : 
```
[vagrant@rocky ~]$ python3 -m venv ~/.venv/ansible
[vagrant@rocky ~]$ source ~/.venv/ansible/bin/activate
```

Installation Ansible : 
```
(ansible) [vagrant@rocky ~]$ pip install ansible
(ansible) [vagrant@rocky ~]$ ansible --version
ansible [core 2.15.13]
  config file = None
  configured module search path = ['/home/vagrant/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /home/vagrant/.venv/ansible/lib64/python3.9/site-packages/ansible
  ansible collection location = /home/vagrant/.ansible/collections:/usr/share/ansible/collections
  executable location = /home/vagrant/.venv/ansible/bin/ansible
  python version = 3.9.18 (main, Sep  7 2023, 00:00:00) [GCC 11.4.1 20230605 (Red Hat 11.4.1-2)] (/home/vagrant/.venv/ansible/bin/python3)
  jinja version = 3.1.5
  libyaml = True
```

Sortie et destruction de la VM 
```
(ansible) [vagrant@rocky ~]$ deactivate
[vagrant@rocky ~]$ exit
logout
Connection to 127.0.0.1 closed.
[ema@2a02-8440-c115-db0c-b6ac-ae24-d16a-c530:atelier-01] $ vagrant destroy -f rocky
```


## Atelier 3 - Exercice 
```
[ema@2a02-8440-c115-db0c-b6ac-ae24-d16a-c530:formation-ansible] $ cd atelier-03
[ema@2a02-8440-c115-db0c-b6ac-ae24-d16a-c530:atelier-03] $ vagrant up

[ema@2a02-8440-c115-db0c-b6ac-ae24-d16a-c530:atelier-03] $ vagrant ssh control
Welcome to Ubuntu 22.04.4 LTS (GNU/Linux 5.15.0-116-generic x86_64)

vagrant@control:~$ type ansible
vagrant@control:~$ sudo nano /etc/hosts
```

Edition du fichier comme ceci (pour appeler les machines plus simplement ^^): 

```
  GNU nano 6.2                                         /etc/hosts                                                   
127.0.0.1 localhost
127.0.1.1 vagrant

127.0.0.1 localhost.localdomain localhost
192.168.56.10 control.sandbox.lan control
192.168.56.20 target01.sandbox.lan target01
192.168.56.30 target02.sandbox.lan target02
192.168.56.40 target03.sandbox.lan target03

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```
Récupération des clés publiques RSA des hôtes et écriture de ceux-ci dans le .ssh/known_host (suppression message erreur). 
```
vagrant@control:~$ ssh-keyscan -t rsa target01 target02 target03 >> .ssh/known_hosts
vagrant@control:~$ ssh-keygen
```
En retour, création des clés ssh vagrant et envoie de la publique sur les hôtes
```
vagrant@control:~$ ssh-copy-id vagrant@target01 #(mdp : vagrant)
vagrant@control:~$ ssh-copy-id vagrant@target02 #(mdp : vagrant)
vagrant@control:~$ ssh-copy-id vagrant@target03 #(mdp : vagrant)
```

TESTTTTTTT : 
```
vagrant@control:~$ ansible all -i target01,target02,target03 -m ping
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
}
target01 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```
Validé ! 


## Atelier 6 - Exercice
Dans le dossier atelier 06 : 
```
vagrant up
vagrant ssh control
```
Comme pour l'exercice précédent, on modifie "/etc/hosts" pour pouvoir appeler les machines par leurs noms :
```
sudo nano /etc/hosts
```
contenu : 
```
127.0.0.1 localhost
127.0.1.1 vagrant

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
127.0.2.1 control control

192.168.56.20 target01
192.168.56.30 target02
192.168.56.40 target03
```

Même méthode qu'a l'exercice précédent pour joindre les VMs via ssh : 
```
vagrant@control:~$ ssh-keyscan -t rsa target01 target02 target03 >> .ssh/known_hosts
vagrant@control:~$ ssh-keygen
vagrant@control:~$ ssh-copy-id vagrant@target01
vagrant@control:~$ ssh-copy-id vagrant@target02
vagrant@control:~$ ssh-copy-id vagrant@target03
```
Installation Ansible et test ping sans configuration.
```
vagrant@control:~$ sudo apt update
vagrant@control:~$ sudo apt install ansible
vagrant@control:~$ ansible all -i target01,target02,target03 -m ping
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
}
target01 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

création et test du dossier monprojet avec le fichier ansible.cfg
```
vagrant@control:~$ mkdir monprojet
vagrant@control:~$ cd monprojet/
vagrant@control:~/monprojet$ touch ansible.cfg
vagrant@control:~/monprojet$ ansible --version
ansible 2.10.8
  config file = /home/vagrant/monprojet/ansible.cfg
  configured module search path = ['/home/vagrant/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  executable location = /usr/bin/ansible
  python version = 3.10.12 (main, Mar 22 2024, 16:50:05) [GCC 11.4.0]
```
Le fichier est bien prit en compte ! 

Création de l'inventaire et de la journalisation, dans le fichier ansible.cfg : 
```
[defaults]
inventory = ./hosts
log_path =  ./logs/ansible.log
```
Création du fichier hosts (avec le groupe testlab et l'utilisateur vagrant pour la connection) : 
```
vagrant@control:~/monprojet$ touch hosts
```
```
[testlab]
target01
target02
target03

[testlab:vars]
ansible_user=vagrant
```

Création et test du fichier de journalisation : 
```
vagrant@control:~/monprojet$ mkdir logs
vagrant@control:~/monprojet$ ansible all -m ping
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
target01 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```
```
vagrant@control:~/monprojet$ cat logs/ansible.log

2025-02-12 15:36:13,571 p=4420 u=vagrant n=ansible | target02 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
2025-02-12 15:36:13,574 p=4420 u=vagrant n=ansible | target03 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
2025-02-12 15:36:13,575 p=4420 u=vagrant n=ansible | target01 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}

```
Nouveau fichier hosts pour l'élévation des privilèges : 
```
[testlab]
target01
target02
target03

[testlab:vars]
ansible_user=vagrant
ansible_become=yes
```
Vérification et destruction des Vms : 

```
vagrant@control:~/monprojet$ ansible all -a "head -n 1 /etc/shadow"
target03 | CHANGED | rc=0 >>
root:*:19769:0:99999:7:::
target01 | CHANGED | rc=0 >>
root:*:19769:0:99999:7:::
target02 | CHANGED | rc=0 >>
root:*:19769:0:99999:7:::
vagrant@control:~/monprojet$ exit
logout
Connection to 127.0.0.1 closed.
[ema@localhost:atelier-06] $ vagrant destroy -f 

```

Atelier 8 - Exercice


Installez successivement les paquets tree, git et nmap sur toutes les cibles.
```
ansible all -m package -a "name=tree"
ansible all -m package -a "name=git"
ansible all -m package -a "name=nmap"
```

Désinstallez successivement ces trois paquets en utilisant le paramètre supplémentaire state=absent.
```
ansible all -m package -a "name=tree state=absent"
ansible all -m package -a "name=git state=absent"
ansible all -m package -a "name=nmap state=absent"
```


Atelier 10 - Exercice
Exercice
Placez-vous dans le répertoire du dixième atelier pratique :

```
cd ~/formation-ansible/atelier-10
```

Démarrez les VM :
Connectez-vous au Control Host :
```
vagrant up
vagrant ssh ansible
```

Rendez-vous dans le répertoire du projet :

```
cd ansible/projets/ema/
direnv: loading ~/ansible/projets/ema/.envrc
direnv: export +ANSIBLE_CONFIG
$ ls -l
total 8
-rw-r--r--. 1 vagrant vagrant  65 Sep 19 14:26 ansible.cfg
-rw-r--r--. 1 vagrant vagrant 128 Sep 19 14:26 inventory
drwxr-xr-x. 2 vagrant vagrant   6 Sep 19 14:26 playbooks

Un premier playbook apache-debian.yml qui installe Apache sur l’hôte debian avec une page personnalisée Apache web server running on Debian Linux.

[vagrant@ansible playbooks]$ cat apache-debian.yml 
---
- hosts: debian

  tasks: 

    - name: Update cache information
      apt:
        update_cache: true

    - name: install apache
      apt:
        name: apache2

    - name: start and enable apache2 service
      service:
        name: apache2
        state: started
        enabled: true

    - name: web page
      copy:
        dest: /var/www/html/index.html
        mode: 0644
        content : |
          <!doctype html>
          <html>
            <head>
              <meta charset="utf-8">
              <title>Test</title>
            </head>
            <body>
              <h1>DEBIAN WEB SERVER CONFIGURED BY ANSIBLE</h1>
            </body>
          </html>
```

```
[vagrant@ansible playbooks]$ curl debian
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Test</title>
  </head>
  <body>
      <h1>DEBIAN WEB SERVER CONFIGURED BY ANSIBLE</h1>
  </body>
</html>
```

Un deuxième playbook apache-rocky.yml qui installe Apache sur l’hôte rocky avec une page personnalisée Apache web server running on Rocky Linux.
```
[vagrant@ansible playbooks]$ cat apache-rocky.yml 
---
- hosts: rocky
  tasks: 
    - name: install httpd
      dnf:
        name: httpd
        state: latest

    - name: start and enable httpd service
      service:
        name: httpd
        state: started
        enabled: true

    - name: web page
      copy:
        dest: /var/www/html/index.html
        mode: 0644
        content : |
         <!doctype html>
         <html>
           <head>
             <meta charset="utf-8">
             <title>Test</title>
           </head>
           <body>
               <h1>ROCKY WEB SERVER CONFIGURED BY ANSIBLE</h1>
           </body>
         </html>
```

```
[vagrant@ansible playbooks]$ curl rocky
```
```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Test</title>
  </head>
  <body>
      <h1>ROCKY WEB SERVER CONFIGURED BY ANSIBLE</h1>
  </body>
</html>
```

