Buildout Odoo
=============

Buildout basé sur celui de Deltablue-cloud (<https://github.com/deltablue-cloud/odoo-buildout-sample>)

Installation
------------

    pip3 install zc.buildout
    buildout

Démarrer l'instance
-------------------

    bin/start_odoo

Changer la version de Odoo
--------------------------

Editer la variable `odoo_branch` de la parts `[odoo_vars]`

Upgrade Odoo
------------

Pour upragder de la v11 à la v12:

Serveur1 en v11
Serveur2 en v12

Sur Serveur1:
Appeler http://<Serveur1>:8069/web/database/manager et dupliquer la base db vers db_v12
Stopper le service Odoo
git clone --branch 12.0 --depth 1 https://github.com/OCA/OpenUpgrade.git
cd OpenUpgrade
pip3 install -r requirements.txt
./odoo-bin --database db_v12 --db_user odoo --update all --stop-after-init --logfile /tmp/migration.log
Démarrer le service Odoo
Appeler http://<Serveur1>:8069/web/database/manager and sauvegarder la base db_v12 dans le fichier db_v12.zip

Sur Serveur2:
Appeler http://<Serveur2>:8069/web/database/manager et restaurer la base db_v12
Stopper le service Odoo
bin/start_odoo -u all -d db_v12 --stop-after-init
Démarrer le service Odoo
