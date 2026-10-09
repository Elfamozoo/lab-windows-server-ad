# Infrastructure Windows Server : AD, DNS, DHCP, NAT, GPO et quotas

![image-01.png](assets/image-01.png)

## Sommaire

- [Sur le serveur PDC:](#sur-le-serveur-pdc)
  - [Rôles ADDS&DNS :](#rôles-addsdns)
  - [Serveur DHCP](#serveur-dhcp)
  - [Structure et utilisateurs](#structure-et-utilisateurs)
- [Sur le serveur ADC:](#sur-le-serveur-adc)
  - [Rôles ADDS&DNS](#rôles-addsdns-1)
- [Sur le serveur RTR01:](#sur-le-serveur-rtr01)
- [Partage de ressources :](#partage-de-ressources-)
- [Stratégies de groupes](#stratégies-de-groupes)
- [Mise en place de quotas et filtres](#mise-en-place-de-quotas-et-filtres)
- [Intervention sur infrastructure existante :](#intervention-sur-infrastructure-existante-)

| Redigé par | Illyes Zerga |
|---|---|

## Sur le serveur PDC:

### Rôles ADDS&DNS :

Configuration de base du serveur, installation du rôle ADDS et création de la forêt `Formation.local`.

![image-02.png](assets/image-02.png)

![image-03.png](assets/image-03.png)

![image-04.png](assets/image-04.png)

![image-05.png](assets/image-05.png)

![image-06.png](assets/image-06.png)

### Serveur DHCP

Rôle DHCP installé et étendue configurée, avec une réservation d’adresse pour le poste client.

![image-07.png](assets/image-07.png)

![image-08.png](assets/image-08.png)

![image-09.png](assets/image-09.png)

### Structure et utilisateurs

Création des unités d’organisation, des groupes et des comptes utilisateurs dans l’annuaire.

![image-10.png](assets/image-10.png)

![image-11.png](assets/image-11.png)

![image-12.png](assets/image-12.png)

![image-13.png](assets/image-13.png)

## Sur le serveur ADC:

### Rôles ADDS&DNS

Installation du rôle ADDS et promotion du serveur en contrôleur de domaine additionnel.

![image-14.png](assets/image-14.png)

## Sur le serveur RTR01:

On installe le remote access :

![image-15.png](assets/image-15.png)

![image-16.png](assets/image-16.png)

Ensuite on configure et active un serveur de Routage en NAT :

![image-17.png](assets/image-17.png)

La on choisit l’interface NAT :

![image-18.png](assets/image-18.png)

On ping bien Google sur le RTR1 :

![image-19.png](assets/image-19.png)

Sur le PDC on a bien accès à Google aussi :

![image-20.png](assets/image-20.png)

Et voila le Tracert vers Google :

![image-21.png](assets/image-21.png)

## Partage de ressources :

Mise en place des partages réseau, des lecteurs personnels et des droits d’accès.

![image-22.png](assets/image-22.png)

![image-23.png](assets/image-23.png)

Exemple d’un ajout de repertoire perso :

![image-24.png](assets/image-24.png)

![image-25.png](assets/image-25.png)

On donne donc les autorisations au groupe GG_Directeurs

![image-26.png](assets/image-26.png)

Et on précise que on refuse l’accès à Bob T se qui aura la priorité au niveau des droits sur le groupe uniquement pour Bob :

![image-27.png](assets/image-27.png)

## Stratégies de groupes

Mise en place des stratégies de groupe (GPO) appliquées au domaine.

![image-28.png](assets/image-28.png)

![image-29.png](assets/image-29.png)

![image-30.png](assets/image-30.png)

![image-31.png](assets/image-31.png)

Pour cela nous allons telecharger les GPO de Google Chrome

Les fichiers à copier sont situés sous "**windows\admx**" dans l'archive ZIP. Il faut donc **copier les 2 fichiers ADMX**, ainsi que les deux répertoires nommés "**fr-FR**" et "**en-US**".

Ensuite dans les GPO on selectionne celle-ci :

![image-32.png](assets/image-32.png)

![image-33.png](assets/image-33.png)

Et donc sur un utilisatereurs du Domaine cela donne ca :

![image-34.png](assets/image-34.png)

![image-35.png](assets/image-35.png)

## Mise en place de quotas et filtres

On installe le role Gestionnaire de ressources du serveur de fichiers

![image-36.png](assets/image-36.png)

Ensuite on crée le modele de quota selon les exigences :

![image-37.png](assets/image-37.png)

Et on applique :

![image-38.png](assets/image-38.png)

Test :

![image-39.png](assets/image-39.png)

## Intervention sur infrastructure existante :

Interventions sur l’infrastructure en place : résolution DNS, accès distant et délégation de contrôle.

![image-40.png](assets/image-40.png)

![image-41.png](assets/image-41.png)

![image-42.png](assets/image-42.png)

![image-43.png](assets/image-43.png)

![image-44.png](assets/image-44.png)

Ensuite sur PS on active la regle pare-feu pour le bureau a distance :

Enable-NetFirewallRule -DisplayGroup "Bureau à distance"

Puis dans l’assistant Délégation de contrôle on va créer une tâche personnalisée à déléguer et suivre les étapes suivantes :

![image-45.png](assets/image-45.png)

![image-46.png](assets/image-46.png)

![image-47.png](assets/image-47.png)

![image-48.png](assets/image-48.png)

On se connecte donc sur le PDC avec Romain.b :

![image-49.png](assets/image-49.png)

Et on va réinitialiser un mot de passe d’utilisateur :

![image-50.png](assets/image-50.png)

![image-51.png](assets/image-51.png)
