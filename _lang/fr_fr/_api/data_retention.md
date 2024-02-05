---
nav_title: Conservation des données
article_title: Conservation des données
alias: /data_retention/
description: "Cet article de référence couvre les informations générales sur la conservation des données de Braze."
page_type: reference
page_order: 2.5

---

<!--
Warning! Don't make any changes to this document without approval from the legal department.
-->

# Informations sur la conservation des données de Braze

*Dernière révision le 20 janvier 2023*

> Cet article couvre les informations générales sur la conservation des données de Braze.<br><br>Les données stockées dans Braze sont conservées et utilisables à des fins de segmentation, de personnalisation et de ciblage pendant toute la durée de vie du compte du client. Cela signifie que les données telles que les attributs du profil de l'utilisateur, les attributs personnalisés, les événements personnalisés et les achats sont stockés indéfiniment pour les utilisateurs actifs, à moins qu'ils ne soient supprimés par le client, pendant la durée du contrat.<br><br>Braze a mis en place des fonctionnalités, des processus et des API pour mettre en œuvre automatiquement les bonnes pratiques d'hygiène des données afin de se conformer au GDPR et à d'autres bonnes pratiques. Ils sont décrits ci-dessous.

## Rétention des données gérée par les clients via le tableau de bord ou l'API de Braze.

Braze permet à ses clients de supprimer eux-mêmes des profils d'utilisateurs entiers et des données d'attributs depuis leur espace de travail.

Cela signifie que tu peux : 
- Supprimer des profils d'utilisateurs à l'aide du [point de terminaison]({{site.baseurl}}/api/endpoints/user_data/post_user_delete/) Braze [Delete user API]({{site.baseurl}}/api/endpoints/user_data/post_user_delete/). 
- Supprimer (null) ou modifier des attributs sur des profils d'utilisateurs en utilisant le [point de terminaison de l'API]({{site.baseurl}}/api/endpoints/user_data/post_user_track/) Braze [Track user]({{site.baseurl}}/api/endpoints/user_data/post_user_track/).

Les événements comportementaux ne peuvent pas être supprimés d'un profil d'utilisateur (événements personnalisés, sessions, campagnes, achats). Pour supprimer ces événements, tu dois supprimer l'ensemble du profil d'utilisateur.

Pour le respect de la vie privée, il se peut que tu doives supprimer toutes les données personnelles relatives à un utilisateur à la demande de ce dernier. Tu trouveras des instructions sur notre page d'[assistance technique sur la protection des données]({{site.baseurl}}/help/dp-technical-assistance/#the-right-to-erasure).

{% alert note %}
Un utilisateur peut avoir plusieurs profils, et il se peut que tu doives supprimer plusieurs profils pour supprimer toutes les données relatives à un seul utilisateur. Suis les instructions de la page d'assistance technique sur la protection des données pour savoir comment supprimer complètement toutes les données concernant un utilisateur.
{% endalert %}

## Conservation des données gérée par Braze pour des fonctionnalités spécifiques des services de Braze.

#### Base de données Braze : Archivage/suppression automatique des utilisateurs désabonnés

Chaque semaine, Braze exécute un processus visant à supprimer les utilisateurs inactifs et dormants des services Braze. En général, il s'agit d'utilisateurs qui ne sont pas joignables (par exemple, qui n'ont pas d'adresse e-mail, pas de numéro de téléphone, pas de jeton push, qui n'utilisent pas tes applis ou ne visitent pas tes sites Web), qui n'ont eu aucune activité enregistrée sur leur profil d'utilisateur et qui n'ont pas reçu de message ou n'ont pas été engagés avec Braze. Ceci est fait pour respecter les principes du GDPR et les meilleures pratiques. Tu peux en savoir plus sur ce processus sur notre page de [définitions des archives d'utilisateurs]({{site.baseurl}}/user_guide/data_and_analytics/user_data_collection/user_archival/).

{% alert note %}
Les clients ont un contrôle total sur le fait qu'un utilisateur soit inactif ou dormant et peuvent empêcher l'archivage des profils d'utilisateurs en enregistrant un point de données à intervalles réguliers. Braze Canvas offre la possibilité de le faire automatiquement, ce qui te permet de désactiver efficacement cette fonctionnalité pour une partie ou la totalité de tes utilisateurs inactifs ou dormants.
{% endalert %}

#### Données sur les campagnes et les interactions avec le canevas 

{% tabs %}
{% tab Campaign Interactions Data %}
**Qu'est-ce que c'est ?** Les interactions de la campagne sont des données liées aux interactions des utilisateurs finaux avec une campagne. Ils sont utilisés pour les filtres de reciblage et pour déterminer la rééligibilité des campagnes.

**Quand est-elle supprimée ?** Braze supprime automatiquement des espaces de travail du Client les Interactions de campagne pour les campagnes qui n'ont pas envoyé de messages depuis 25 mois calendaires et qui ne sont pas utilisées pour le reciblage dans des campagnes, des Canvas ou des cartes de contenu dans un statut actif.

**Que se passe-t-il après la suppression ?**

- Les campagnes sans interactions de campagne ne peuvent pas être utilisées dans les filtres de reciblage pour les campagnes, les canevas et les segments.
- Toute campagne active qui n'a pas envoyé de messages depuis 25 mois et qui n'est pas utilisée pour le reciblage dans des campagnes actives, des toiles ou des cartes, sera arrêtée car l'éligibilité de la campagne se réinitialise. Tu peux relancer la campagne après avoir revu les paramètres de rééligibilité.

**Comment réinitialiser l'horloge pour éviter la suppression ?** Pour conserver les Interactions de campagne pour une campagne particulière, tu peux envoyer un message utilisant cette campagne au moins une fois dans les 25 mois qui suivent le dernier message envoyé ou utiliser cette campagne dans un filtre de reciblage dans n'importe quelle campagne, Canvas ou Carte active. Tu peux demander une conservation des données plus courte que 25 mois via ton responsable de la réussite client Braze.

{% endtab %}
{% tab Canvas Interactions Data %}

**Qu'est-ce que c'est ?** Les interactions Canvas sont des données liées aux interactions des utilisateurs finaux avec un Canvas ou une étape Canvas. Ils sont utilisés pour les filtres de reciblage et pour déterminer la rééligibilité de Canvas.

**Quand est-elle supprimée ?** Braze supprime automatiquement des espaces de travail du client les interactions des Canvas qui n'ont envoyé aucun message depuis 25 mois calendaires et qui ne sont pas utilisées pour le reciblage par des campagnes ou des Canvas actifs.

**Que se passe-t-il après la suppression ?**
- Les toiles sans interactions avec les toiles ne peuvent pas être utilisées dans les filtres de reciblage pour les campagnes, les toiles et les segments.
- Tout Canvas actif qui n'a pas été utilisé pour envoyer des messages depuis 25 mois, et qui n'est pas utilisé pour le reciblage dans des campagnes, des Canvas ou des Cartes actives, sera arrêté car l'éligibilité des Canvas se réinitialise. Tu peux relancer le Canvas après avoir revu les paramètres de rééligibilité.
- Tu ne pourras pas référencer ces Interactions Canvas dans les fonctions de reciblage, telles que les filtres, et tu ne pourras pas extraire les données supprimées de l'API `/users/export`.

**Comment réinitialiser l'horloge pour éviter la suppression ?** Pour conserver les interactions de Canvas pour un Canvas particulier, tu peux envoyer un message utilisant ce Canvas au moins une fois dans les 25 mois qui suivent le dernier message envoyé ou utiliser ce Canvas dans un filtre de reciblage dans n'importe quelle campagne, Canvas ou Carte active. Tu peux demander une conservation des données plus courte que 25 mois via ton responsable de la réussite client Braze.
{% endtab %}
{% endtabs %}

## La conservation des données est assurée par Braze

Les politiques de conservation ci-dessous se rapportent à la conformité de Braze avec le GDPR et les réglementations en matière de confidentialité et concernent le stockage transitoire des données lorsqu'elles passent par nos systèmes internes. Ces politiques de conservation n'ont pas d'impact sur les services de Braze et sont informatives pour tes équipes juridiques et de protection de la vie privée.

#### Serveurs Braze : Conservation à court terme à des fins de récupération

Les données envoyées par Braze à certains sous-traitants peuvent encore exister dans les systèmes internes de Braze pendant 90 jours.

#### Braze Data Lake Conservation des données

Les données disponibles pour les clients dans le tableau de bord de Braze sont principalement agrégées. Les journaux détaillés sont conservés dans une base de données distincte créée par Braze (le " lac de données ", anciennement appelé " base de données BI "). Les données du lac de données sont utilisées pour les rapports agrégés et d'autres fonctionnalités avancées.

Si tu utilises nos API pour supprimer des profils d'utilisateurs ou pour supprimer ou modifier des attributs de profils d'utilisateurs, cela peut prendre jusqu'à deux semaines pour que ces données soient supprimées du lac de données de Braze. La suppression des données dans le lac de données n'affectera pas la segmentation ou la personnalisation, mais garantit plutôt que les données sont supprimées de tous les systèmes de Braze.

#### Serveurs de sauvegarde Braze

Lorsque les données sont supprimées de ton instance de production, elles restent dans les serveurs de sauvegarde de Braze pendant six mois et sont ensuite supprimées selon nos processus internes.
