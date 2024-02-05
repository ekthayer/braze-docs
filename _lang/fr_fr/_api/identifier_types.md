---
nav_title: "Types d'identificateurs API"
article_title: "Types d'identificateurs API"
page_order: 2.2
description: "Cet article de référence traite des différents types d'identifiants API qui existent dans le tableau de bord Braze, de l'endroit où tu peux les trouver et de leur utilité." 
page_type: reference

---

# Types d'identifiants API

> Ce guide de référence aborde les différents types d'identifiants d'API que l'on peut trouver dans le tableau de bord de Braze, leur but, l'endroit où tu peux les trouver et la façon dont ils sont généralement utilisés. Pour plus d'informations sur les clés de l'API REST ou les clés de l'API de l'espace de travail, reporte-toi à la [vue d'ensemble de l'API]({{site.baseurl}}/api/api_key/).

Les identifiants suivants peuvent être utilisés pour accéder à ton modèle, Canvas, campagne, segment, envoi ou carte à partir de l'API externe de Braze. Tous les messages doivent respecter le codage [UTF-8][1].

{% tabs %}
{% tab App IDs %}

## L'identifiant de l'application

L'identifiant de l'appli ou `app_id` est un paramètre qui associe l'activité à une appli spécifique dans ton espace de travail. Il désigne l'application avec laquelle tu interagis au sein de l'espace de travail. Par exemple, tu constateras que tu auras un `app_id` pour ton application iOS, un `app_id` pour ton application Android, et un `app_id` pour ton intégration web. Chez Braze, il se peut que tu aies plusieurs apps pour la même plateforme à travers les différents types de plateformes que Braze prend en charge.

#### Où puis-je le trouver ?

Il y a deux façons de localiser ton `app_id`:

1. Va dans **Paramètres** > **Clés API**. Sous **Identification**, tu peux voir chaque `app_id` qui existe pour tes apps.
2. Va dans **Réglages** > **Réglages de l'application**. Ta clé API est indiquée à côté du champ **Clé API** dans la section des paramètres.

{% alert note %}
Si tu utilises l'[ancienne navigation]({{site.baseurl}}/navigation), ces pages se trouvent à un nouvel emplacement :<br> \- Les **clés API** se trouvent dans la **console du développeur** > **Paramètres API**.<br> - **Paramètres de l'application** situés dans **Gérer les paramètres** > **Paramètres**
{% endalert %}

#### À quoi peut-il servir ?

Les identifiants d'appli à Braze sont utilisés lors de l'intégration du SDK et sont également utilisés pour référencer une appli spécifique dans les appels d'API REST. Avec le site `app_id`, tu peux faire beaucoup de choses, comme extraire des données pour un événement personnalisé qui s'est produit pour une application particulière, récupérer les statistiques de désinstallation, les statistiques sur les nouveaux utilisateurs, les statistiques DAU et les statistiques sur le démarrage de la session pour une application particulière.

{% alert note %}
Il peut arriver que l'on te demande un `app_id` mais que tu ne travailles pas avec une application, car il s'agit d'un champ hérité propre à une plateforme spécifique, tu peux omettre ce champ en incluant n'importe quelle chaîne de caractères en guise d'espace réservé pour ce paramètre obligatoire.
{% endalert %}

#### Identifiants d'applications multiples

Lors de la configuration du SDK, le cas d'utilisation le plus courant pour les identifiants d'applications multiples est la séparation de ces identifiants pour les variantes de construction de débogage et de version.

Pour passer facilement d'un identifiant d'appli à l'autre dans tes builds, nous te recommandons de créer un fichier `braze.xml` distinct pour chaque [variante de build](https://developer.android.com/studio/build/build-variants.html) concernée. Une variante de construction est une combinaison de type de construction et de saveur de produit. Note que par défaut, un nouveau projet Android est configuré avec les types de construction `debug` et `release` et aucune saveur de produit.

Pour chaque variante de construction pertinente, crée un nouveau site `braze.xml` dans `src/<build variant name>/res/values/`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
<string name="com_braze_api_key">{YOUR_BUILD_VARIANT_API_KEY}</string>
</resources>
```
Lorsque la variante de construction sera compilée, elle utilisera le nouvel identifiant.

{% endtab %}
{% tab Template IDs %}

## Identificateur de modèle

Un identifiant de [modèle]({{site.baseurl}}/api/endpoints/templates/) ou ID de modèle est une clé aléatoire générée par Braze pour un modèle donné dans le tableau de bord. Les identifiants de modèle sont uniques pour chaque modèle et peuvent être utilisés pour référencer les modèles par le biais de l'API. 

Les modèles sont parfaits si ton entreprise sous-traite tes conceptions HTML pour des campagnes. Une fois les modèles construits, tu as maintenant un modèle qui n'est pas spécifique à une campagne mais qui peut être appliqué à une série de campagnes comme une newsletter.

#### Où puis-je le trouver ?
Tu peux trouver l'identifiant de ton modèle de deux façons :

1. Va dans **Modèles**, sélectionne une page modèle, puis sélectionne un modèle préexistant. Si le modèle que tu souhaites n'existe pas encore, crée-en un et enregistre-le. En bas de la page du modèle individuel, tu pourras trouver l'identifiant de ton modèle.<br><br>
2. Va dans **Paramètres** > **Clés API**. Ici, Braze propose une recherche d'**identifiants d'API supplémentaires** où tu peux rechercher des identifiants spécifiques.

{% alert note %}
Si tu utilises l'[ancienne navigation]({{site.baseurl}}/navigation), tu peux trouver les identifiants d'API à partir de **Developer Console** > **API Settings**.{% endalert %}

#### À quoi peut-il servir ?

- Mettre à jour les modèles par le biais de l'API
- Obtenir des informations sur un modèle spécifique

<br>
{% endtab %}
{% tab Canvas IDs %}

## Identificateur de toile

Un identifiant de [Canvas]({{site.baseurl}}/user_guide/engagement_tools/canvas/) ou Canvas ID est une clé aléatoire générée par Braze pour un Canvas donné au sein du tableau de bord. Les identifiants des toiles sont uniques à chaque toile et peuvent être utilisés pour référencer les toiles par le biais de l'API. 

Note que si tu as un Canvas qui a des variantes, il existe un ID de Canvas global ainsi que des ID de Canvas de variantes individuelles imbriqués sous le Canvas principal. 

#### Où puis-je le trouver ?
Tu trouveras ton identifiant Canvas dans le tableau de bord. Va dans **Messagerie** > **Canevas** et sélectionne un canevas préexistant. Si le Canvas que tu souhaites n'existe pas encore, crée-en un et enregistre-le. En bas d'une page individuelle de Canvas, clique sur **Analyser les variantes**. Une fenêtre apparaît avec l'identifiant de l'API Canvas situé en bas.

{% alert note %}
Si tu utilises l'[ancienne navigation]({{site.baseurl}}/navigation), **Canvas** se trouve sous **Engagement**.
{% endalert %}

#### À quoi peut-il servir ?
- Suivre les analyses d'un message spécifique
- Obtenir des statistiques globales de haut niveau sur les performances de Canvas.
- Obtenir des détails sur une toile spécifique
- Avec Currents pour apporter des données au niveau de l'utilisateur pour une approche "plus globale" des toiles.
- Avec livraison de déclencheurs API afin de collecter des statistiques pour les messages transactionnels.

<br>
{% endtab %}
{% tab Campaign IDs %}

## Identificateur de campagne

Un identifiant de [campagne]({{site.baseurl}}/user_guide/engagement_tools/campaigns/) ou ID de campagne est une clé aléatoire générée par Braze pour une campagne donnée dans le tableau de bord. Les identifiants de campagne sont uniques à chaque campagne et peuvent être utilisés pour référencer les campagnes par le biais de l'API. 

Note que si tu as une campagne qui a des variantes, il y a à la fois un identifiant de campagne globale et des identifiants de campagne de variantes individuelles imbriqués sous la campagne principale. 

#### Où puis-je le trouver ?
Tu peux trouver l'identifiant de ta campagne de deux façons :

1. Va dans **Messagerie** > **Campagnes** et sélectionne une campagne préexistante. Si la campagne que tu souhaites n'existe pas encore, crée-en une et enregistre-la. En bas de la page de la campagne individuelle, tu pourras trouver ton **identifiant API de campagne**.<br><br>
2. Va dans **Paramètres** > **Clés API**. Ici, Braze propose une recherche d'**identifiants d'API supplémentaires** où tu peux rechercher des identifiants spécifiques.

{% alert note %}
Si tu utilises l'[ancienne navigation]({{site.baseurl}}/navigation), ces pages se trouvent à un autre endroit :<br> - **Campagnes** est sous **Engagement**<br> \- Les **clés API** se trouvent dans la **console du développeur** > **Paramètres API**.
{% endalert %}

#### À quoi peut-il servir ?
- Suivre les analyses d'un message spécifique
- Obtenir des statistiques globales de haut niveau sur les performances de la campagne.
- Obtenir des détails sur une campagne spécifique
- Avec Currents pour apporter des données au niveau de l'utilisateur pour une approche "plus globale" des campagnes.
- Avec une livraison déclenchée par l'API afin de collecter des statistiques pour les messages transactionnels.
- Pour [rechercher une campagne spécifique]({{site.baseurl}}/user_guide/engagement_tools/campaigns/managing_campaigns/search_campaigns/#search-syntax) sur la page **Campagnes** à l'aide du filtre `api_id:YOUR_API_ID`

<br>
{% endtab %}
{% tab Segment IDs %}

## Identificateur de segment

Un identifiant de [segment]({{site.baseurl}}/user_guide/engagement_tools/segments/) ou ID de segment est une clé aléatoire générée par Braze pour un segment donné dans le tableau de bord. Les identifiants de segment sont uniques à chaque segment et peuvent être utilisés pour référencer les segments par le biais de l'API. 

#### Où puis-je le trouver ?
Tu peux trouver ton identifiant de segment de deux façons :

1. Va dans **Audience** > **Segments** et sélectionne un segment préexistant. Si le segment que tu souhaites n'existe pas encore, crée-en un et enregistre-le. En bas de la page du segment individuel, tu pourras trouver ton identifiant de segment. <br><br>
2. Va dans **Paramètres** > **Clés API**. Ici, Braze propose une recherche d'**identifiants d'API supplémentaires** où tu peux rechercher des identifiants spécifiques.

{% alert note %}
Si tu utilises l'[ancienne navigation]({{site.baseurl}}/navigation), ces pages se trouvent à un autre endroit :<br> - **Segments** est sous **Engagement**<br> \- Les **clés API** se trouvent dans la **console du développeur** > **Paramètres API**.
{% endalert %}

#### À quoi peut-il servir ?
- Obtenir des détails sur un segment spécifique
- Récupérer les analyses d'un segment spécifique
- Tire combien de fois un événement personnalisé a été enregistré pour un segment particulier.
- Spécifier et envoyer une campagne aux membres d'un segment à partir de l'API

{% endtab %}
{% tab Card IDs %}

## Identifiant de la carte

Un identifiant de carte ou ID de carte est une clé aléatoire générée par Braze pour une carte de fil d'actualité donnée dans le tableau de bord. Les identifiants de carte sont uniques à chaque carte de [fil d'actualité]({{site.baseurl}}/user_guide/engagement_tools/news_feed/) et peuvent être utilisés pour référencer les cartes par le biais de l'API. 

{% alert note %}
Le fil d'actualité est en train d'être supprimé. Braze recommande aux clients qui utilisent notre outil de fil d'actualité de passer à notre canal de messagerie Content Cards : il est plus flexible, personnalisable et fiable. Consulte le [guide de migration]({{site.baseurl}}/user_guide/message_building_by_channel/content_cards/migrating_from_news_feed/) pour en savoir plus.
{% endalert %}

#### Où puis-je le trouver ?
Tu peux trouver l'identifiant de ta carte de deux façons :

1. Va dans **Messagerie** > **Fil d'actualité** et sélectionne un fil d'actualité préexistant. Si le fil d'actualité que tu souhaites n'existe pas encore, crée-en un et enregistre-le. En bas de la page individuelle du fil d'actualité, tu pourras trouver l'identifiant unique de ta carte. <br><br>
2. Va dans **Paramètres** > **Clés API**. Ici, Braze propose une recherche d'**identifiants d'API supplémentaires** où tu peux rechercher des identifiants spécifiques.

{% alert note %}
Si tu utilises l'[ancienne navigation]({{site.baseurl}}/navigation), ces pages se trouvent à un nouvel emplacement :<br> \- Le **fil d'actualité** est sous **Engagement**<br> \- Les **clés API** se trouvent dans la **console du développeur** > **Paramètres API**.
{% endalert %}

#### À quoi peut-il servir ?
- Récupère les informations pertinentes sur une carte
- Suivre les événements liés aux cartes de contenu et à l'engagement.

<br>
{% endtab %}
{% tab Send IDs %}

## Envoyer l'identifiant

Un identifiant d'envoi, ou ID d'envoi, est une clé soit générée par Braze, soit créée par toi pour un envoi de message donné, sous laquelle les analyses doivent être suivies. L'identifiant d'envoi te permet de récupérer les analyses d'une instance spécifique d'une campagne envoyée via le [point de terminaison`/sends/data_series` ]({{site.baseurl}}/api/endpoints/export/campaigns/get_send_analytics/).

#### Où puis-je le trouver ?
Les campagnes API et déclenchées par l'API qui sont envoyées en tant que diffusion génèrent automatiquement un identifiant d'envoi si celui-ci n'est pas fourni. Si tu veux spécifier ton propre identifiant d'envoi, tu devras d'abord en créer un via le [point de terminaison`/sends/id/create` ]({{site.baseurl}}/api/endpoints/messaging/send_messages/post_create_send_ids/). L'identifiant doit être composé de tous les caractères ASCII et comporter au maximum 64 caractères. Tu peux réutiliser un identifiant d'envoi sur plusieurs envois de la même campagne si tu veux regrouper les analyses de ces envois.

#### À quoi peut-il servir ?
Envoyer et suivre les performances des messages de façon programmatique, sans création de campagne pour chaque envoi.

<br>
{% endtab %}
{% endtabs %}

[1]: https://en.wikipedia.org/wiki/UTF-8
[3]: https://developer.android.com/studio/build/build-variants.html
