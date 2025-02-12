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


