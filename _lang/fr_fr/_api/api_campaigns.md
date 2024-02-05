---
nav_title: Campagnes API
article_title: Campagnes API
page_order: 5
description: "Cet article de référence explique comment générer un identifiant de campagne à inclure dans tes appels API et comment configurer cette campagne."
page_type: reference
tool: Campaigns

---
# Campagnes API

> Cet article de référence explique comment générer une `campaign_id` à inclure dans tes appels API et comment configurer cette campagne.

Les campagnes API sont généralement utilisées pour les messages transactionnels. Lors de la création de campagnes API (et non de [campagnes déclenchées par l'API]({{site.baseurl}}/user_guide/engagement_tools/campaigns/building_campaigns/delivery_types/api_triggered_delivery/)), le tableau de bord Braze n'est utilisé que pour générer un `campaign_id`, qui te permet de suivre les analyses pour les rapports de campagne. Tu peux aussi générer un identifiant de variation de message, qui est différent pour chaque variante de ta campagne. 

Tu enverras ensuite ces informations à ton équipe de développement pour qu'elle les utilise dans la demande d'API, avec :
- Copie de la campagne
- Membres du public
- Actifs

Une fois la campagne commencée, tu peux consulter les résultats dans le tableau de bord. Les campagnes API utilisent les [API de messagerie de]({{site.baseurl}}/api/endpoints/messaging/) Braze, qui disposent des mêmes options de rapports détaillés et de reciblage que les campagnes créées entièrement via le tableau de bord.

‹#›
Comme les campagnes API sont généralement transactionnelles, tous les utilisateurs sont éligibles pour les campagnes API, même ceux qui font partie de ton groupe de contrôle global.
‹#›

## Créer une nouvelle campagne

Va dans **Messagerie** > **Campagnes** et clique sur **Créer une campagne**, puis sélectionne **Campagnes API**. Tu peux maintenant passer à la configuration de ta campagne API.

Une [campagne déclenchée par l'API]({{site.baseurl}}/user_guide/engagement_tools/campaigns/building_campaigns/delivery_types/api_triggered_delivery/) est différente d'une campagne API.

## Configure ta campagne

Pour configurer ta campagne, effectue les étapes suivantes :

1. Ajoute un titre descriptif pour que tu puisses trouver les résultats sur la page de nos campagnes après avoir envoyé tes messages.
2. Clique sur **Ajouter un message** et ajoute les types de messages qui seront inclus dans ta campagne API. Cela te permettra de générer un `campaign_id` et un identifiant de variation de message, qui diffère pour chaque canal que tu inclus. 
3. En option, tu peux ajouter un événement de conversion pour suivre les conversions des utilisateurs sur une action spécifique ou un objectif de campagne.
4. Clique sur **Sauvegarder la campagne** et tu es prêt à commencer ta campagne API !

## Appels API

Après avoir sauvegardé ta campagne API, inclus les éléments suivants dans ta demande API : 
- Les champs `campaign_id` générés avec ta demande d'API sont indiqués dans les [points de terminaison d'envoi de messages][2].
- Un [objet message]({{site.baseurl}}/api/objects_filters/#messaging-objects) pour chaque plateforme incluse dans la campagne. Dans l'objet du message, indique l'identifiant de la variation du message. Cela permettra de spécifier que les statistiques doivent être collectées et affichées sous cette variante. Les objets de message suivants sont pris en charge : Android, Content Cards, email, iOS, Kindle, SMS/MMS, web push et webhook.

[2]: {{site.baseurl}}/api/endpoints/messaging/#send-endpoints

