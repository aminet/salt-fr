﻿Compte rendu Salt Meetup Paris - avril 2015
===========================================


:date: 2015-04-16
:tags: cr, tinyclues, logilab, enterprise, ui, ansible, REx 
:category: Compte Rendus
:author: Aurélien Minet
:email: amlabs@free.fr


Une petite trentaine de membre de communauté Salt parisienne a été accueilli dans les nouveaux locaux de `Tinyclues <http://www.tinyclues.com/>` pour ce meetup, l'on remercie. Merci également à `Logilab <http://www.logilab.fr/>` qui a offert pour le dîner des bagels.

Voici un compte rendu rapide des trois présentations de cette soirée.

Interface Web SaltStack Enterprise
----------------------------------
Rob Hilberding de `SaltStack Inc. <http://www.saltstack.com/>` qui était à Paris pour plusieurs jours est venu présenter une "pure preview" ce que sera potentiellement l'interface web de la version Enterprise de Saltstack.
Il a présenté l'interface qu'il développe, cette dernière s'appuie sur l'API SaltStack et MariaDB ou MySQL. A noter que cette interface n'est qu'une extention, à savoir que la version Salstack Enterprise (master et minion) est basée sur le même code que la version communautaire.
L'interface supporte le multi-master, elle liste les minions et pour chaque minion : elle permet d'avoir l'ensemble de ces grains, le statut de ça connexion, des informations sur dernier job.
La liste des minions pouvant être longue il y a la possibilité de filtre soit par une correspondance sur une partie de l'ID des minions soit sur la valeur d'un ou plusieurs grains.
Un filtre peut permettre la création de groupe de minions, c'est également possible via un wizard dédié. Les groupes créés peuvent être partagé (publics) ou privés.
Pour les minions sélectionnés il est possible dans lancer un job (depuis une liste).
Ainsi cet interface permet à des utilisateurs ne connaissant pas de manière poussé SaltStack de lancer des actions (job) sur des machines (minions) pour lesquelles ils ont les droits.



Paul Tonelli de `Heuritech <http://www.heuritech.com/>` a présenté les différences entre Ansible et SaltStack qu'il a appréhender après une semaine d'utilisation d'Ansible.
* Ansible utilise SSH pour les communication et donc c'est le serveur qui ce connecte aux clients ce qui peut impliquer de paramétrer ssh avec des proxy, le cas typique est l'accès au serveurs qui ont derrière un HAProxy en mode transparent.
* Ansible n'a pas de serveur (daemon) qui tourne en continu comme SaltStack, mis à part Tower qui est payant.
* Tower est une interface Web, qui au delà du fait d'être une GUI, peut offrir des fonctionnalités proches du reactor de Salt
* L'approche d'Ansible est d'avoir un playbook par projet alors que SaltStack à une arborescence pour l'ensemble.
* Ansible peut cibler un peut comme Salt mais sur des nom de machines et faire des groupes de machines en les déclarant dans un fichier, les wilcards peuvent être utilisés.
* La gestion des dépendances est simple il faut que cela soit déclaré avant/au dessus.
La conclusion est que Ansible a une approche plus minimaliste et la configuration est plus statique.



Samuel Phan de `DDN <http://www.ddn.com/>` à présenté l'utilisation de SaltStack dans le cadre du déploiement et maintient des produits de DDN de stockage type big data et S3.
Les clients de DDN déploient quelques RPM et produisent une configuration qui va pousser sur l'ensemble des nœuds (via SSH) les masters et les minions pour déployer toute la stack: (Zookeeper, HBase, Hadoop, memecache Jetty ....) puis pour la surveiller et l'orchestrer.
A noter que l’environnement déployé est multi-master, 2 ou 3 pas plus afin de minimiser certaines latence 
Un ensemble outils (\*ctl), qui forment une couche d'abstraction à Saltstack comme un wrapper, afin de gérer le stockage offert par les solutions de stockage. SaltStack est manqué pour le client qui n'a pas besoin de le maîtriser.
SaltStack a été choisi pour sa rapidité, la parallélisation, la consistance dans ce qui est déployé, le multi-master (actif-actif).
