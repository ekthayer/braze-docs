---
nav_title: Limites de débit
article_title: Limites de débit de l’API
page_order: 4.5
description: "Cet article de référence couvre les limites de débit de l’API pour l’infrastructure de l’API Braze."
page_type: reference

---

# Limites de débit

> L’infrastructure API de Braze est conçue pour gérer de gros volumes de données dans l’ensemble de notre clientèle. À cette fin, nous appliquons des limites de débit d’API par espace de travail. 

Une limite de débit est le nombre de requêtes que l’API peut recevoir au cours d’une période donnée. De nombreux incidents de déni de service basés sur la charge dans les grands systèmes sont involontaires, c’est-à-dire causés par des erreurs logicielles ou de configuration, et non par des attaques malveillantes. Les limites de débit vérifient que de telles erreurs ne privent pas nos clients des ressources de l’API Braze. Si un trop grand nombre de demandes sont envoyées au cours d’une période donnée, vous pouvez voir des réponses d’erreur avec un code d’état de , ce qui indique que la limite de `429`, débit a été atteinte.

{% alert warning %}
Les limites de débit de l’API sont susceptibles d’être modifiées en fonction de l’utilisation appropriée de notre système. Nous encourageons les limites raisonnables lors de l’appel d’API afin d’éviter les dommages ou les abus.
{% endalert %}

## Limites de débit par type de demande

Le tableau suivant répertorie les limites de débit d’API par défaut pour différents types de requêtes. Ces limites par défaut peuvent être augmentées sur demande. Contactez votre responsable de la réussite client pour plus d’informations.

{% alert note %}
Les demandes qui ne sont pas répertoriées dans ce tableau partagent une limite de taux de défaut total de 250 000 demandes par heure.
{% endalert %}

| Type de demande | Limite de débit d’API par défaut |
| --- | --- |
| [`/users/track`][10] | **Requêtes:** 50 000 requêtes par minute.<br><br>**Dosage:** 75 événements, 75 achats et 75 attributs par requête d’API. Pour plus d’informations, reportez-vous à la section [Traitement par lot des demandes de suivi des utilisateurs](#batch-user-track) . |
| [`/users/export/ids`][11] | 2 500 requêtes par minute. |
| [`/users/delete`][12]<br>[`/users/alias/new`][13]<br>[`/users/alias/update`][45]<br>[`/users/identify`][14]<br>[`/users/merge`][44] | 20 000 requêtes par minute, partagées entre les terminaux. |
| [`/users/external_id/rename`][20] | 1 000 requêtes par minute. |
| [`/users/external_id/remove`][21] | 1 000 requêtes par minute. |
| [`/events/list`][15] | 1 000 requêtes par heure, partagées avec le point de `/purchases/product_list` terminaison. |
| [`/purchases/product_list`][16] | 1 000 requêtes par heure, partagées avec le point de `/events/list` terminaison. |
| [`/campaigns/data_series`][17.3] | 50 000 requêtes par minute. |
| [`/messages/send`][17] | 250 requêtes par minute pour les appels de diffusion (lorsque vous ne spécifiez qu’un segment ou une audience connectée). Sinon, 250 000 requêtes par heure. |
| [`/campaigns/trigger/send`][17.1] | 250 requêtes par minute pour les appels de diffusion (lorsque vous ne spécifiez qu’un segment ou une audience connectée). Sinon, 250 000 requêtes par heure. |
| [`/canvas/trigger/send`][17.2] | 250 requêtes par minute pour les appels de diffusion (lorsque vous ne spécifiez qu’un segment ou une audience connectée). Sinon, 250 000 requêtes par heure. |
| [`/sends/id/create`][18] | 100 demandes par jour. |
| [`/subscription/status/set`][19] | 5 000 requêtes par minute. |
| [`/preference_center/v1/{preferenceCenterExternalId}/url/{userId}`][26]<br>[`/preference_center/v1/list`][27]<br>[`/preference_center/v1/{preferenceCenterExternalId}`][28] | 1 000 requêtes par minute, par espace de travail. |
| [`/preference_center/v1`][29]<br>[`/preference_center/v1/{preferenceCenterExternalId}`][30] | 10 requêtes par minute, par espace de travail. |
| [`/catalogs/{catalog_name}`][31]<br>[`/catalogs`][32]<br>[`/catalogs`][33] | 50 requêtes par minute partagées entre les points de terminaison. |
| [`/catalogs/{catalog_name}/items`][34]<br>[`/catalogs/{catalog_name}/items`][35]<br>[`/catalogs/{catalog_name}/items`][36] | 16 000 requêtes par minute partagées entre les terminaux. |
| [`/catalogs/{catalog_name}/items/{item_id}`][37]<br>[`/catalogs/{catalog_name}/items/{item_id}`][38]<br>[`/catalogs/{catalog_name}/items`][39]<br>[`/catalogs/{catalog_name}/items/{item_id}`][40]<br>[`/catalogs/{catalog_name}/items/{item_id}`][41] | 50 requêtes par minute partagées entre les points de terminaison. |
| [`/scim/v2/Users/{id}`][22]<br>[`/scim/v2/Users?filter={userName@example.com}`][43]<br>[`/scim/v2/Users/{id}`][25]<br>[`/scim/v2/Users/{id}}`][24]<br>[`/scim/v2/Users/`][23] | 5 000 requêtes par jour, par entreprise, partagées entre les terminaux. |
{: .reset-td-br-1 .reset-td-br-2}

<!-- Add during CDI endpoints GA
| [`/cdi/integrations`][46] | 50 requests per minute. |
| [`/cdi/integrations/{integration_id}/sync`][47] | 20 requests per minute. |
| [`/cdi/integrations/{integration_id}/job_sync_status`][48] | 100 requests per minute. |
-->

## Traitement par lots des demandes d’API

Les API Braze sont conçues pour prendre en charge le traitement par lots. Avec le traitement par lots, Braze peut prendre autant de données que possible en un seul appel d’API afin que vous n’ayez pas besoin d’effectuer beaucoup d’appels d’API. Il est plus efficace pour Braze de traiter les données par lots que de traiter les données un appel à la fois. Par exemple, la gestion de 1 000 appels d’API par lots nécessite moins de ressources que la gestion de 75 000 appels individuels. Le traitement par lots est extrêmement important pour toute application qui peut nécessiter plus de 75 000 appels par heure.

{% alert note %}
Les augmentations de la limite de débit de l’API REST sont envisagées en fonction des besoins des clients qui utilisent les fonctionnalités de traitement par lot de l’API.
{% endalert %}

### Traitement par lot des demandes de suivi des utilisateurs {#batch-user-track}

Chaque `/users/track` requête peut contenir jusqu’à 75 objets d’événement, 75 objets d’attribut et 75 objets d’achat. Chaque objet (tableau d’événement, d’attribut et d’achat) peut mettre à jour un utilisateur chacun. Au total, cela signifie qu’un maximum de 225 utilisateurs peuvent être mis à jour en un seul appel. De plus, un seul profil utilisateur peut être mis à jour par plusieurs objets.

Les demandes adressées à ce point de terminaison commencent généralement à être traitées dans l’ordre suivant : 

1. Attributs
2. Épreuves
3. Achats

### Traitement par lot des demandes de point de terminaison de messagerie

Une seule demande adressée aux [points de][1] terminaison de messagerie peut atteindre l’un des éléments suivants :

- Jusqu’à 50 spécifiques `external_ids`, chacun avec des paramètres de message individuels
- Segment de n’importe quelle taille créé dans le tableau de bord Braze, spécifié par son `segment_id`
- Utilisateurs qui correspondent à des filtres d’audience supplémentaires de n’importe quelle taille, définis dans la requête en tant qu’objet d’audience [][2] connectée

## Surveillance de vos limites de débit

Chaque requête d’API envoyée à Braze renvoie les informations suivantes dans les en-têtes de réponse :

Nom de l’en-tête             | Description
----------------------- | -----------------------
`X-RateLimit-Limit`     | Nombre maximal de demandes que vous pouvez effectuer au cours d’un intervalle spécifié (votre limite de débit).
`X-RateLimit-Remaining` | Nombre de demandes restantes dans la fenêtre de limite de débit actuelle.
`X-RateLimit-Reset`     | Heure à laquelle la fenêtre de limite de débit actuelle se réinitialise en secondes d’époque UTC.
{: .reset-td-br-1 .reset-td-br-2}

Ces informations sont intentionnellement incluses dans l’en-tête de la réponse à la demande d’API plutôt que dans le tableau de bord Braze. Cela permet à votre système de mieux réagir en temps réel lorsque vous interagissez avec notre API. Par exemple, si la `X-RateLimit-Remaining` valeur tombe en dessous d’un certain seuil, vous pouvez ralentir l’envoi pour vous assurer que tous les e-mails transactionnels sont envoyés. Ou, s’il atteint zéro, vous pouvez suspendre tous les envois jusqu’à ce que le temps spécifié dans `X-RateLimit-Reset` s’écoule.

Si vous avez des questions sur les limites de l’API, contactez votre responsable de la réussite client ou ouvrez un ticket][support]d’assistance [.

### Délai optimal entre les points de terminaison

{% alert note %}
Nous vous recommandons de prévoir un délai de 5 minutes entre les appels de point de terminaison consécutifs afin de minimiser les erreurs.
{% endalert %}

Il est essentiel de comprendre le délai optimal entre les points de terminaison lorsque vous effectuez des appels consécutifs à l’API Braze. Les problèmes surviennent lorsque les points de terminaison dépendent du traitement réussi d’autres points de terminaison et, s’ils sont appelés trop tôt, peuvent générer des erreurs. Par exemple, si vous attribuez un alias à des utilisateurs via notre point de terminaison, puis que vous appuyez sur cet alias pour envoyer un événement personnalisé via notre `/user/alias/new`  `/users/track` point de terminaison, combien de temps devez-vous attendre ?

Dans des conditions normales, le temps nécessaire à la cohérence de nos données est de 10 à 100 ms (1/10 de seconde). Cependant, il peut y avoir des cas où il faut plus de temps pour que cette cohérence se produise, nous vous recommandons donc de prévoir un délai de 5 minutes entre les appels suivants afin de minimiser la probabilité d’erreur.

[1]: {{site.baseurl}}/api/endpoints/messaging/
[2]: {{site.baseurl}}/api/objects_filters/connected_audience/
[support]: {{site.baseurl}}/braze_support/
[10]: {{site.baseurl}}/api/endpoints/user_data/post_user_track/
[11]: {{site.baseurl}}/api/endpoints/export/user_data/post_users_identifier/
[12]: {{site.baseurl}}/api/endpoints/user_data/post_user_delete/
[13]: {{site.baseurl}}/api/endpoints/user_data/post_user_alias/
[14]: {{site.baseurl}}/api/endpoints/user_data/post_user_identify/
[15]: {{site.baseurl}}/api/endpoints/export/custom_events/get_custom_events/
[16]: {{site.baseurl}}/api/endpoints/export/purchases/get_list_product_id/
[17]: {{site.baseurl}}/api/endpoints/messaging/send_messages/post_send_messages/
[17.1]: {{site.baseurl}}/api/endpoints/messaging/send_messages/post_send_triggered_campaigns/
[17.2]: {{site.baseurl}}/api/endpoints/messaging/send_messages/post_send_triggered_canvases/
[17.3]: {{site.baseurl}}/api/endpoints/export/campaigns/get_campaign_analytics/
[18]: {{site.baseurl}}/api/endpoints/messaging/send_messages/post_create_send_ids/
[19]: {{site.baseurl}}/api/endpoints/subscription_groups/post_update_user_subscription_group_status/
[20]: {{site.baseurl}}/api/endpoints/user_data/external_id_migration/post_external_ids_rename/
[21]: {{site.baseurl}}/api/endpoints/user_data/external_id_migration/post_external_ids_remove/
[22]: {{site.baseurl}}/get_see_user_account_information/
[23]: {{site.baseurl}}/post_create_user_account/
[24]: {{site.baseurl}}/delete_existing_dashboard_user/
[25]: {{site.baseurl}}/post_update_existing_user_account/
[26]: {{site.baseurl}}/api/endpoints/preference_center/get_create_url_preference_center/
[27]: {{site.baseurl}}/api/endpoints/preference_center/get_list_preference_center/
[28]: {{site.baseurl}}/api/endpoints/preference_center/get_view_details_preference_center/
[29]: {{site.baseurl}}/api/endpoints/preference_center/post_create_preference_center/
[30]: {{site.baseurl}}/api/endpoints/preference_center/put_update_preference_center/
[31]: {{site.baseurl}}/api/endpoints/catalogs/catalog_management/synchronous/delete_catalog/
[32]: {{site.baseurl}}/api/endpoints/catalogs/catalog_management/synchronous/get_list_catalogs/
[33]: {{site.baseurl}}/api/endpoints/catalogs/catalog_management/synchronous/post_create_catalog/
[34]: {{site.baseurl}}/api/endpoints/catalogs/catalog_items/asynchronous/delete_catalog_items_bulk/
[35]: {{site.baseurl}}/api/endpoints/catalogs/catalog_items/asynchronous/patch_catalog_items_bulk/
[36]: {{site.baseurl}}/api/endpoints/catalogs/catalog_items/asynchronous/post_create_catalog_items_bulk/
[37]: {{site.baseurl}}/api/endpoints/catalogs/catalog_items/synchronous/delete_catalog_item/
[38]: {{site.baseurl}}/api/endpoints/catalogs/catalog_items/synchronous/get_catalog_item_details/
[39]: {{site.baseurl}}/api/endpoints/catalogs/catalog_items/synchronous/get_catalog_items_details_bulk/
[40]: {{site.baseurl}}/api/endpoints/catalogs/catalog_items/synchronous/patch_catalog_item/
[41]: {{site.baseurl}}/api/endpoints/catalogs/catalog_items/synchronous/post_create_catalog_item/
[43]: {{site.baseurl}}/get_search_existing_dashboard_user_email/
[44]: {{site.baseurl}}/api/endpoints/user_data/post_users_merge/
[45]: {{site.baseurl}}/api/endpoints/user_data/post_users_alias_update/
[46]: {{site.baseurl}}/api/endpoints/cdi/get_integration_list/
[47]: {{site.baseurl}}/api/endpoints/cdi/job_sync/
[48]: {{site.baseurl}}/api/endpoints/cdi/job_sync_status/