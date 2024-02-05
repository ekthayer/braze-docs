---
nav_title: "Présentation de l'API"
article_title: "Présentation de l'API"
page_order: 2.1
description: "Cet article de référence couvre les bases de l'API, notamment ce qu'est une API REST, la terminologie et une présentation des clés API."
page_type: reference
alias: /api/api_key/
---

# Présentation de l'API

> Cet article de référence couvre les bases de l'API, y compris la terminologie courante et une présentation des clés et des autorisations de l'API REST, ainsi que de la manière de les sécuriser. 

## Définitions d'API

Ce qui suit répertorie un aperçu des termes que vous pouvez voir dans la documentation de l'API REST Braze.

### Points de terminaison

Braze gère un certain nombre d'instances différentes pour notre tableau de bord et nos points de terminaison REST. Une fois votre compte configuré, vous vous connecterez à l'une des URL suivantes. Utilisez le point de terminaison REST correct en fonction de l'instance sur laquelle vous êtes provisionné. En cas de doute, ouvrez un [ticket d'assistance][assistance] ou utilisez le tableau suivant pour faire correspondre l'URL du tableau de bord que vous utilisez au point de terminaison REST correct.

{% alert important %}
Lorsque vous utilisez des points de terminaison pour les appels d'API, utilisez le point de terminaison REST.

Pour l'intégration du SDK, utilisez le [point de terminaison du SDK]({{site.baseurl}}/user_guide/administrative/access_braze/sdk_endpoints/), et non le point de terminaison REST.
{% endalert %}

|Exemple|URL|Point de terminaison REST|Point de terminaison du SDK|
|---|---|---|
|NOUS-01| `https://dashboard-01.braze.com` | `https://rest.iad-01.braze.com` | `sdk.iad-01.braze.com` |
|NOUS-02| `https://dashboard-02.braze.com` | `https://rest.iad-02.braze.com` | `sdk.iad-02.braze.com` |
|NOUS-03| `https://dashboard-03.braze.com` | `https://rest.iad-03.braze.com` | `sdk.iad-03.braze.com` |
|NOUS-04| `https://dashboard-04.braze.com` | `https://rest.iad-04.braze.com` | `sdk.iad-04.braze.com` |
|NOUS-05| `https://dashboard-05.braze.com` | `https://rest.iad-05.braze.com` | `sdk.iad-05.braze.com` |
|NOUS-06| `https://dashboard-06.braze.com` | `https://rest.iad-06.braze.com` | `sdk.iad-06.braze.com` |
|NOUS-07| `https://dashboard-07.braze.com` | `https://rest.iad-07.braze.com` | `sdk.iad-07.braze.com` |
|NOUS-08| `https://dashboard-08.braze.com` | `https://rest.iad-08.braze.com` | `sdk.iad-08.braze.com` |
|UE-01| `https://dashboard-01.braze.eu` | `https://rest.fra-01.braze.eu` | `sdk.fra-01.braze.eu` |
|UE-02| `https://dashboard-02.braze.eu` | `https://rest.fra-02.braze.eu` | `sdk.fra-02.braze.eu` |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

### Limites de l'API

Pour la plupart des API, Braze a une limite de débit par défaut de 250 000 requêtes par heure. Cependant, certains types de demandes ont leur propre limite de débit appliquée pour mieux gérer des volumes élevés de données au sein de notre base de clients. Pour plus de détails, reportez-vous aux [limites de débit de l'API]({{site.baseurl}}/api/api_limits/)

### ID utilisateur 

- **ID utilisateur externe** : Le `external_id` sert d’identifiant unique à l’utilisateur pour lequel vous soumettez des données. Cet identifiant doit être le même que celui que vous avez défini dans le SDK Braze afin d'éviter de créer plusieurs profils pour le même utilisateur.
- **ID utilisateur Braze** : `braze_id` sert d'identifiant d'utilisateur unique défini par Braze. Cet identifiant peut être utilisé pour supprimer des utilisateurs via l'API REST en plus des external_ids.

Pour plus d'informations, reportez-vous à l'article suivant en fonction de votre plateforme : [iOS][9], [Android][10]et [Web][13].

## Clé API REST

Une clé d'interface de programmation d'application REST (clé API REST) ​​est un code unique transmis à une API pour authentifier l'appel d'API et identifier l'application ou l'utilisateur appelant. L'accès à l'API s'effectue à l'aide de requêtes Web HTTPS vers le point de terminaison de l'API REST de votre entreprise. Nous utilisons les clés API REST chez Braze en tandem avec nos clés d'identification d'application pour suivre, accéder, envoyer, exporter et analyser les données afin de garantir que tout fonctionne correctement de votre côté et du nôtre.

Les espaces de travail et les clés API vont de pair chez Braze. Les espaces de travail sont conçus pour héberger des versions de la même application sur plusieurs plates-formes. De nombreux clients utilisent également des espaces de travail pour contenir les versions gratuites et premium de leurs applications sur la même plateforme. Comme vous le remarquerez peut-être, ces espaces de travail utilisent également l'API REST et disposent de leurs propres clés API REST. Ces clés peuvent être étendues individuellement pour inclure l'accès à des points de terminaison spécifiques sur l'API. Chaque appel à l'API doit inclure une clé d'accès au point de terminaison atteint.

Nous faisons référence à la clé API REST et à la clé API de l'espace de travail sous le nom de `api_key`. Le `api_key` est inclus dans chaque requête en tant qu'en-tête de requête et agit comme une clé d'authentification qui vous permet d'utiliser nos API REST. Ces API REST sont utilisées pour suivre les utilisateurs, envoyer des messages, exporter des données utilisateur, etc. Lorsque vous créez une nouvelle clé API REST, vous devrez lui donner accès à des points de terminaison spécifiques. En attribuant des autorisations spécifiques à une clé API, vous pouvez limiter exactement les appels qu'une clé API peut authentifier.

![Panneau Clés API REST sur la page Clés API.][27]

{% alert tip %}
En plus des clés API REST, il existe également un type de clé appelée clés d'identification qui peuvent être utilisées pour référencer des éléments spécifiques tels que des applications, des modèles, des canevas, des campagnes, des cartes de contenu et des segments de l'API. Pour plus d'informations, reportez-vous à [Types d'identifiants API]({{site.baseurl}}/api/identifier_types/).
{% endalert %}

### Autorisations de la clé API REST

Les autorisations de clé API sont des autorisations que vous pouvez attribuer à un utilisateur ou à un groupe pour limiter son accès à certains appels API. Pour afficher votre liste d'autorisations de clé API, accédez à **Paramètres** > **Clés API**et sélectionnez votre clé API.

{% tabs %}
{% tab User Data %}

| Autorisation | Point de terminaison | Description |
|---|---|---|
| `users.track` | [`/users/track`]({{site.baseurl}}/api/endpoints/user_data/post_user_track/) | Enregistrez les attributs des utilisateurs, les événements personnalisés et les achats. | 
| `users.delete` | [`/users/delete`]({{site.baseurl}}/api/endpoints/user_data/post_user_delete/) | Supprimez n’importe quel utilisateur. |
| `users.alias.new` | [`/users/alias/new`]({{site.baseurl}}/api/endpoints/user_data/post_user_alias/) |Créez un nouvel alias pour un utilisateur existant. |
| `users.identify` | [`/users/identify`]({{site.baseurl}}/api/endpoints/user_data/post_user_identify/) |Identifiez un utilisateur alias uniquement avec un ID externe. |
| `users.export.ids` | [`/users/export/ids`]({{site.baseurl}}/api/endpoints/export/user_data/post_users_identifier/) |Recherchez des informations sur le profil utilisateur par ID utilisateur. |
| `users.export.segment` | [`/users/export/segment`]({{site.baseurl}}/api/endpoints/export/user_data/post_users_segment/) |Recherchez des informations sur le profil utilisateur par segment. | 
| `users.merge` | [`/users/merge`]({{site.baseurl}}/api/endpoints/user_data/post_users_merge/) | Fusionne deux utilisateurs existants. |
| `users.external_ids.rename` | [`/users/external_ids/rename`]({{site.baseurl}}/api/endpoints/user_data/external_id_migration/post_external_ids_rename/) | Modifiez l'ID externe d'un utilisateur existant. |
| `users.external_ids.remove` | [`/users/external_ids/remove`]({{site.baseurl}}/api/endpoints/user_data/external_id_migration/post_external_ids_remove/) | Supprimez l'ID externe d'un utilisateur existant. |
| `users.alias.update` | [`/users/alias/update`]({{site.baseurl}}/api/endpoints/user_data/post_users_alias_update/) | Mettez à jour un alias pour un utilisateur existant. |
| `users.export.global_control_group` | [`/users/export/global_control_group`]({{site.baseurl}}/api/endpoints/export/user_data/post_users_global_control_group/) | Recherchez des informations sur le profil utilisateur dans le groupe de contrôle global. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3}

 {% endtab %}
 {% tab Email %}

| Autorisation | Point de terminaison | Description |
|---|---|---|
| `email.unsubscribe` | [`/email/unsubscribes`]({{site.baseurl}}/api/endpoints/email/get_query_unsubscribed_email_addresses/) | Requête d'adresses e-mail désabonnées.  |
| `email.status` | [`/email/status`]({{site.baseurl}}/api/endpoints/email/post_email_subscription_status/) | Changer le statut de l'adresse e-mail. |
| `email.hard_bounces` | [`/email/hard_bounces`]({{site.baseurl}}/api/endpoints/email/get_list_hard_bounces/) | Requête d'adresses e-mail renvoyées de manière irréversible. |
| `email.bounce.remove` | [`/email/bounce/remove`]({{site.baseurl}}/api/endpoints/email/post_remove_hard_bounces/) | Supprimez les adresses e-mail de votre liste de rebonds définitifs. |
| `email.spam.remove` | [`/email/spam/remove`]({{site.baseurl}}/api/endpoints/email/post_remove_spam/) | Supprimez les adresses e-mail de votre liste de spam. |
| `email.blacklist` | [`/email/blacklist`]({{site.baseurl}}/api/endpoints/email/post_blacklist/) | Adresses e-mail de liste de blocage. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3}

{% endtab %}
{% tab Messages %}

| Autorisation | Point de terminaison | Description |
|---|---|---|
| `messages.send` | [`/messages/send `]({{site.baseurl}}/api/endpoints/messaging/send_messages/post_send_messages/) | Envoyez un message immédiat à des utilisateurs spécifiques. |
| `messages.schedule.create` | [`/messages/schedule/create`]({{site.baseurl}}/api/endpoints/messaging/schedule_messages/post_schedule_messages/) | Planifiez l'envoi d'un message à une heure précise. |
| `messages.schedule.update` | [`/messages/schedule/update`]({{site.baseurl}}/api/endpoints/messaging/schedule_messages/post_update_scheduled_messages/) | Mettre à jour un message programmé. |
| `messages.schedule.delete` | [`/messages/schedule/delete`]({{site.baseurl}}/api/endpoints/messaging/schedule_messages/post_delete_scheduled_messages/) | Supprimez un message programmé. |
| `messages.schedule_broadcasts` | [`/messages/scheduled_broadcasts`]({{site.baseurl}}/api/endpoints/messaging/schedule_messages/get_messages_scheduled/) | Interrogez tous les messages de diffusion programmés. |
| `messages.live_activity.update` | [`/messages/live_activity/update`]({{site.baseurl}}/api/endpoints/messaging/live_activity/update/) | Mettez à jour une activité iOS Live. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3}

{% endtab %}
{% tab Campaigns %}

| Autorisation | Point de terminaison | Description |
|---|---|---|
| `campaigns.trigger.send` | [`/campaigns/trigger/send`]({{site.baseurl}}/api/endpoints/messaging/send_messages/post_send_triggered_campaigns/) | Déclenchez l'envoi d'une campagne existante. |
| `campaigns.trigger.schedule.create` | [`/campaigns/trigger/schedule/create`]({{site.baseurl}}/api/endpoints/messaging/schedule_messages/post_schedule_triggered_campaigns/) | Planifiez un futur envoi d'une campagne avec une livraison déclenchée par l'API. |
| `campaigns.trigger.schedule.update` | [`/campaigns/trigger/schedule/update`]({{site.baseurl}}/api/endpoints/messaging/schedule_messages/post_update_scheduled_triggered_campaigns/) | Mettez à jour une campagne planifiée avec une diffusion déclenchée par l'API. |
| `campaigns.trigger.schedule.delete` | [`/campaigns/trigger/schedule/delete`]({{site.baseurl}}/api/endpoints/messaging/schedule_messages/post_delete_scheduled_triggered_messages/) |Supprimez une campagne planifiée avec une diffusion déclenchée par l'API. |
| `campaigns.list` | [`/campaigns/list`]({{site.baseurl}}/api/endpoints/export/campaigns/get_campaigns/) | Requête pour une liste de campagnes. |
| `campaigns.data_series` | [`/campaigns/data_series`]({{site.baseurl}}/api/endpoints/export/campaigns/get_campaign_analytics/) | Requête d'analyse de campagne sur une période donnée. |
| `campaigns.details` | [`/campaigns/details`]({{site.baseurl}}/api/endpoints/export/campaigns/get_campaign_details/) | Recherchez les détails d’une campagne spécifique. |
| `sends.data_series` | [`/sends/data_series`]({{site.baseurl}}/api/endpoints/export/campaigns/get_send_analytics/) | Requête d’analyse d’envoi de messages sur une période donnée. |
| `sends.id.create` | [`/sends/id/create`]({{site.baseurl}}/api/endpoints/messaging/send_messages/post_create_send_ids/) | Créez un identifiant d'envoi pour le suivi des envois de messages. |
| `campaigns.url_info.details` | [`/campaigns/url_info/details`]({{site.baseurl}}) | Recherchez les détails de l'URL d'une variante de message spécifique au sein d'une campagne. |
| `transactional.send` | [`/transactional/v1/campaigns/{campaign_id}/send`]({{site.baseurl}}/api/endpoints/messaging/send_messages/post_send_transactional_message/) | Permet d'envoyer des messages transactionnels à l'aide du point de terminaison de messagerie transactionnelle. |
{: .reset-td-br-1 .reset-td-br-2}

{% endtab %}
{% tab Canvas %}

| Autorisation | Point de terminaison | Description |
|---|---|---|
| `canvas.trigger.send` | [`/canvas/trigger/send`]({{site.baseurl}}/api/endpoints/messaging/send_messages/post_send_triggered_canvases/) | Déclenchez l'envoi d'un Canvas existant. |
| `canvas.trigger.schedule.create` | [`/canvas/trigger/schedule/create`]({{site.baseurl}}/api/endpoints/messaging/schedule_messages/post_schedule_triggered_canvases/) | Planifiez un prochain envoi d'un Canvas avec une livraison déclenchée par l'API. |
| `canvas.trigger.schedule.update` | [`/canvas/trigger/schedule/update`]({{site.baseurl}}/api/endpoints/messaging/schedule_messages/post_update_scheduled_triggered_canvases/) | Mettez à jour un Canvas planifié avec une livraison déclenchée par l'API. |
| `canvas.trigger.schedule.delete` | [`/canvas/trigger/schedule/delete`]({{site.baseurl}}/api/endpoints/messaging/schedule_messages/post_delete_scheduled_triggered_canvases/)| Supprimez un Canvas planifié avec une livraison déclenchée par l'API. |
| `canvas.list` | [`/canvas/list`]({{site.baseurl}}/api/endpoints/export/canvas/get_canvases/) |  Requête pour une liste de canevas. |
| `canvas.data_series` | [`/canvas/data_series`]({{site.baseurl}}/api/endpoints/export/canvas/get_canvas_analytics/) | Requête d’analyse Canvas sur une période donnée. |
| `canvas.details` | [`/canvas/details`]({{site.baseurl}}/api/endpoints/export/canvas/get_canvas_details/) | Requête pour les détails d’un canevas spécifique. |
| `canvas.data_summary` | [`/canvas/data_summary`]({{site.baseurl}}/api/endpoints/export/canvas/get_canvas_analytics_summary/) | Requête de cumuls d’analyses Canvas sur une période donnée. |
| `canvas.url_info.details` | [`/canvas/url_info/details`]({{site.baseurl}}/get_canvas_link_alias/) | Recherchez les détails de l'URL d'une variation de message spécifique dans une étape Canvas. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3}

{% endtab %}
{% tab Segments %}

| Autorisation | Point de terminaison | Description |
|---|---|---|
| `segments.list` | [`/segments/list`]({{site.baseurl}}/api/endpoints/export/segments/get_segment/) | Requête pour une liste de segments. |
| `segments.data_series` | [`/segments/data_series`]({{site.baseurl}}/api/endpoints/export/segments/get_segment_analytics/) | Requête d'analyse de segment sur une plage de temps. |
| `segments.details` | [`/segments/details`]({{site.baseurl}}/api/endpoints/export/segments/get_segment_details/) | Recherchez les détails d’un segment spécifique. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3}

{% endtab %}
{% tab Purchases %}

| Autorisation | Point de terminaison | Description |
|---|---|---|
| `purchases.product_list` | [`/purchases/product_list`]({{site.baseurl}}/api/endpoints/export/purchases/get_list_product_id/) | Recherchez une liste de produits achetés dans votre application. |
| `purchases.revenue_series` | [`/purchases/revenue_series`]({{site.baseurl}}/api/endpoints/export/purchases/get_revenue_series/) | Recherchez l'argent total dépensé par jour dans votre application sur une période donnée. |
| `purchases.quantity_series` | [`/purchases/quantity_series`]({{site.baseurl}}/api/endpoints/export/purchases/get_number_of_purchases/) | Recherchez le nombre total d'achats par jour dans votre application sur une période donnée. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3}

{% endtab %}
{% tab Events %}

| Autorisation | Point de terminaison | Description |
|---|---|---|
| `events.list` | [`/events/list`]({{site.baseurl}}/api/endpoints/export/custom_events/get_custom_events/) | Requête pour une liste d’événements personnalisés. |
| `events.data_series` | [`/events/data_series`]({{site.baseurl}}/api/endpoints/export/custom_events/get_custom_events_analytics/) | Interrogez les occurrences d’un événement personnalisé sur une plage de temps. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3}

{% endtab %}
{% tab News Feed %}

{% alert note %}
Le fil d’actualité est obsolète. Braze recommande aux clients qui utilisent notre outil de fil d'actualité de passer à notre canal de messagerie de cartes de contenu : il est plus flexible, personnalisable et fiable. Consultez le [guide de migration]({{site.baseurl}}/user_guide/message_building_by_channel/content_cards/migrating_from_news_feed/) pour en savoir plus.
{% endalert %}

| Autorisation | Point de terminaison | Description |
|---|---|---|
| `feed.list` | [`/feed/list`]({{site.baseurl}}/api/endpoints/export/news_feed/get_news_feed_cards/) | Recherchez une liste de cartes de fil d’actualité. |
| `feed.data_series` | [`/feed/data_series`]({{site.baseurl}}/api/endpoints/export/news_feed/get_news_feed_card_analytics/) | Requête d'analyse du fil d'actualité sur une période donnée. |
| `feed.details` | [`/feed/details`]({{site.baseurl}}/api/endpoints/export/news_feed/get_news_feed_card_details/) | Recherchez les détails d’un fil d’actualité spécifique. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3}

{% endtab %}
{% tab Sessions %}

| Autorisation | Point de terminaison | Description |
|---|---|---|
| `sessions.data_series` | [`/sessions/data_series`]({{site.baseurl}}/api/endpoints/export/sessions/get_sessions_analytics/) | Requête de sessions par jour sur une plage de temps. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3}

{% endtab %}
{% tab KPIs %}

| Autorisation | Point de terminaison | Description |
|---|---|---|
| `kpi.dau.data_series` | [`/kpi/dau/data_series`]({{site.baseurl}}/api/endpoints/export/kpi/get_kpi_dau_date/) |  Recherchez des utilisateurs actifs uniques par jour sur une période donnée. |
| `kpi.mau.data_series` | [`/kpi/mau/data_series`]({{site.baseurl}}/api/endpoints/export/kpi/get_kpi_mau_30_days/) | Requête du nombre total d'utilisateurs actifs uniques sur une fenêtre glissante de 30 jours sur une période donnée. |
| `kpi.new_users.data_series` | [`/kpi/new_users/data_series`]({{site.baseurl}}/api/endpoints/export/kpi/get_kpi_daily_new_users_date/) | Recherchez de nouveaux utilisateurs par jour sur une plage de temps. |
| `kpi.uninstalls.data_series` | [`/kpi/uninstalls/data_series`]({{site.baseurl}}/api/endpoints/export/kpi/get_kpi_uninstalls_date/) | Recherchez les désinstallations d'applications par jour sur une période donnée. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3}

{% endtab %}
{% tab Templates %}

| Autorisation | Point de terminaison | Description |
|---|---|---|
| `templates.email.create` | [`/templates/email/create`]({{site.baseurl}}/api/endpoints/templates/email_templates/post_create_email_template/) | Créez un nouveau modèle d'e-mail sur le tableau de bord. |
| `templates.email.info` | [`/templates/email/info`]({{site.baseurl}}/api/endpoints/templates/email_templates/get_see_email_template_information/) | Requête d'informations sur un modèle spécifique. |
| `templates.email.list` | [`/templates/email/list`]({{site.baseurl}}/api/endpoints/templates/email_templates/get_list_email_templates/) | Recherchez une liste de modèles d’e-mails. |
| `templates.email.update` | [`/templates/email/update`]({{site.baseurl}}/api/endpoints/templates/email_templates/post_update_email_template/) | Mettez à jour un modèle d'e-mail stocké sur le tableau de bord. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3}

{% endtab %}
{% tab SSO %}

| Autorisation | Description |
|---|---|---|
| `sso.saml.login` | Configurez la connexion initiée par le fournisseur d’identité. Pour plus d'informations, reportez-vous à [Connexion initiée par le fournisseur de services (SP)]({{site.baseurl}}/user_guide/administrative/access_braze/single_sign_on/set_up/). |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3}

{% endtab %}
{% tab Content Blocks %}

| Autorisation | Point de terminaison | Description |
|---|---|---|
| `content_blocks.info` | [`/content_blocks/info`]({{site.baseurl}}/api/endpoints/templates/content_blocks_templates/get_see_email_content_blocks_information/) | Requête d'informations sur un modèle spécifique. |
| `content_blocks.list` | [`/content_blocks/list`]({{site.baseurl}}/api/endpoints/templates/content_blocks_templates/get_list_email_content_blocks/) | Recherchez une liste de blocs de contenu. |
| `content_blocks.create` | [`/content_blocks/create`]({{site.baseurl}}/api/endpoints/templates/content_blocks_templates/post_create_email_content_block/) | Créez un nouveau bloc de contenu sur le tableau de bord. |
| `content_blocks.update` | [`/content_blocks_update`]({{site.baseurl}}/api/endpoints/templates/content_blocks_templates/post_update_content_block/) | Mettez à jour un bloc de contenu existant sur le tableau de bord. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3}

{% endtab %}
{% tab Preference Center %}

| Autorisation | Point de terminaison | Description |
|---|---|---|
| `preference_center.get` | [`/preference_center/v1/{preferenceCenterExternalId}`]({{site.baseurl}}/api/endpoints/preference_center/get_view_details_preference_center) | Obtenez un centre de préférences. |
| `preference_center.list` | [`/preference_center/v1/list`]({{site.baseurl}}/api/endpoints/preference_center/get_list_preference_center/) | Répertoriez les centres de préférences. |
| `preference_center.update` | [`/preference_center/v1`]({{site.baseurl}}/api/endpoints/preference_center/post_create_preference_center)<br><br>[`/preference_center/v1/{preferenceCenterExternalID}`]({{site.baseurl}}/api/endpoints/preference_center/put_update_preference_center/) | Créez ou mettez à jour un centre de préférences. |
| `preference_center.user.get` | [`/preference_center/v1/{preferenceCenterExternalId}/url/{userId}`]({{site.baseurl}}/api/endpoints/preference_center/get_create_url_preference_center) | Obtenez un lien vers le centre de préférences pour un utilisateur. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3}

{% endtab %}
{% tab Subscription %}

| Autorisation | Point de terminaison | Description |
|---|---|---|
| `subscription.status.set` | [`/subscription/status/set`]({{site.baseurl}}/api/endpoints/subscription_groups/post_update_user_subscription_group_status/) | Définir le statut du groupe d'abonnement. |
| `subscription.status.get` | [`/subscription/status/get`]({{site.baseurl}}/api/endpoints/subscription_groups/get_list_user_subscription_group_status/) | Obtenez le statut du groupe d'abonnement. |
| `subscription.groups.get` | [`/subscription/user/status`]({{site.baseurl}}/api/endpoints/subscription_groups/get_list_user_subscription_groups/) | Obtenez l’état des groupes d’abonnement auxquels des utilisateurs spécifiques sont explicitement abonnés et désabonnés. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3}

{% endtab %}
{% tab SMS %}

| Autorisation | Point de terminaison | Description |
|---|---|---|
| `sms.invalid_phone_numbers` | [`/sms/invalid_phone_numbers`]({{site.baseurl}}/api/endpoints/sms/get_query_invalid_numbers/) | Requête de numéros de téléphone invalides. |
| `sms.invalid_phone_numbers.remove` | [`/sms/invalid_phone_numbers/remove`]({{site.baseurl}}/api/endpoints/sms/post_remove_invalid_numbers/) | Supprimez l'indicateur de numéro de téléphone invalide des utilisateurs. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3}

{% endtab %}
{% tab Catalogs %}

| Autorisation | Point de terminaison | Description |
|---|---|---|
| `catalogs.add_items` | [`/catalogs/{catalog_name}/items`]({{site.baseurl}}/api/endpoints/catalogs/catalog_items/asynchronous/post_create_catalog_items_bulk/) | Ajoutez plusieurs éléments à un catalogue existant. |
| `catalogs.update_items` | [`/catalogs/{catalog_name}/items`]({{site.baseurl}}/api/endpoints/catalogs/catalog_items/asynchronous/patch_catalog_items_bulk/) | Mettez à jour plusieurs éléments dans un catalogue existant. |
| `catalogs.delete_items` | [`/catalogs/{catalog_name}/items`]({{site.baseurl}}/api/endpoints/catalogs/catalog_items/asynchronous/delete_catalog_items_bulk) | Supprimez plusieurs éléments d'un catalogue existant. |
| `catalogs.get_item` | [`/catalogs/{catalog_name}/items/{item_id}`]({{site.baseurl}}/api/endpoints/catalogs/catalog_items/synchronous/get_catalog_item_details/) | Obtenez un seul élément d’un catalogue existant. |
| `catalogs.update_item` | [`/catalogs/{catalog_name}/items/{item_id}`]({{site.baseurl}}/api/endpoints/catalogs/catalog_items/synchronous/put_update_catalog_item/) | Mettez à jour un seul élément dans un catalogue existant. |
| `catalogs.create_item` | [`/catalogs/{catalog_name}/items/{item_id}`]({{site.baseurl}}/api/endpoints/catalogs/catalog_items/synchronous/post_create_catalog_item/) | Créez un seul élément dans un catalogue existant. |
| `catalogs.delete_item` | [`/catalogs/{catalog_name}/items/{item_id}`]({{site.baseurl}}/api/endpoints/catalogs/catalog_items/synchronous/delete_catalog_item/) | Supprimez un seul élément d’un catalogue existant. |
| `catalogs.replace_item` | [` /catalogs/{catalog_name}/items/{item_id}`]({{site.baseurl}}/api/endpoints/catalogs/catalog_items/synchronous/put_update_catalog_item/) | Remplacez un seul élément d’un catalogue existant. |
| `catalogs.create` | [`/catalogs`]({{site.baseurl}}/api/endpoints/catalogs/catalog_management/synchronous/post_create_catalog/) | Créez un catalogue. |
| `catalogs.get` | [`/catalogs`]({{site.baseurl}}/api/endpoints/catalogs/catalog_management/synchronous/get_list_catalogs/) | Obtenir une liste de catalogues |
| `catalogs.delete` | [`/catalogs/{catalog_name}`]({{site.baseurl}}/api/endpoints/catalogs/catalog_management/synchronous/delete_catalog/) | Supprimer un catalogue. |
| `catalogs.get_items` | [`/catalogs/{catalog_name}/items`]({{site.baseurl}}/api/endpoints/catalogs/catalog_items/synchronous/get_catalog_items_details_bulk/) | Obtenez un aperçu des éléments d’un catalogue existant. |
| `catalogs.replace_items` | [`/catalogs/{catalog_name}/items`]({{site.baseurl}}/api/endpoints/catalogs/catalog_items/asynchronous/put_update_catalog_items/) | Remplacez les éléments d'un catalogue existant. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3}

{% endtab %}
{% endtabs %}

## Création de clés API REST

Pour créer une nouvelle clé API REST :

1. Accédez à **Paramètres** > **Clés API**. Cette page affiche vos clés API existantes.

{% alert note %}
Si vous utilisez l' [ancienne navigation]({{site.baseurl}}/navigation), vous pouvez créer une clé API depuis **Developer Console** > **API Settings**.
{% endalert %}

{:start="2"}
2\. Cliquez sur **\+ Créer une nouvelle clé API**.
3\. Donnez à votre nouvelle clé un nom pour l'identifier en un coup d'œil.
4\. Sélectionnez [les autorisations](#rest-api-key-permissions) que vous souhaitez associer à votre nouvelle clé.
5\. Spécifiez [les adresses IP et les sous-réseaux sur liste blanche](#api-ip-allowlisting) pour la nouvelle clé.

{% alert important %}
Gardez à l'esprit qu'après avoir créé une nouvelle clé API, vous ne pouvez pas modifier l'étendue des autorisations ou les adresses IP autorisées. Cette limitation est en place pour des raisons de sécurité. Si vous devez modifier la portée d'une clé, créez une nouvelle clé avec les autorisations mises à jour et implémentez cette clé à la place de l'ancienne. Une fois votre implémentation terminée, supprimez l’ancienne clé.
{% endalert %}

## Gestion des clés API REST

Les clés API REST ne peuvent pas être modifiées après leur création. Cependant, vous pouvez afficher les détails ou supprimer les clés API REST existantes à partir de la page **Clés API** . La liste **Rest API Keys** affiche les informations suivantes en un coup d'œil pour chaque clé :

| Champ        | Description                                                                                                         |
| ------------ | :------------------------------------------------------------------------------------------------------------------ |
| Nom de la clé API | Le nom donné à la clé lors de sa création.                                                                            |
| Identifiant   | La clé API.                                                                                                        |
| Créé par   | L'adresse e-mail de l'utilisateur qui a créé la clé. Ce champ affichera « N/A » pour les clés créées avant juin 2023. |
| date créée | Date de création de cette clé.                                                                                      |
| Vu pour la dernière fois    | La date à laquelle cette clé a été utilisée pour la dernière fois. Ce champ affichera « N/A » pour les clés qui n'ont jamais été utilisées.                  |
{: .reset-td-br-1 .reset-td-br-2}

Pour afficher les détails d'une clé spécifique, sélectionnez une clé dans la liste. Vous pouvez ensuite voir toutes les autorisations dont dispose cette clé, les adresses IP sur liste blanche (le cas échéant) et si cette clé est inscrite sur la liste blanche des adresses IP Braze.

![][30]

Pour supprimer une clé, cliquez sur <i class="fas fa-gear" alt="Settings"></i> et en sélectionnant l'option correspondante.

![][29]

## Sécurité des clés API REST

Les clés API sont utilisées pour authentifier un appel API. Lorsque vous créez une nouvelle clé API REST, vous devez lui donner accès à des points de terminaison spécifiques. En attribuant des autorisations spécifiques à une clé API, vous pouvez limiter exactement les appels qu'une clé API peut authentifier.

Étant donné que les clés de l'API REST permettent d'accéder à des points de terminaison de l'API REST potentiellement sensibles, sécurisez ces clés et partagez-les uniquement avec des partenaires de confiance. Ils ne devraient jamais être exposés publiquement. Par exemple, n'utilisez pas cette clé pour passer des appels AJAX depuis votre site Web ou pour l'exposer de toute autre manière publique.

Une bonne pratique de sécurité consiste à attribuer à un utilisateur uniquement le nombre d'accès nécessaire pour accomplir son travail : ce principe peut également être appliqué aux clés API en attribuant des autorisations à chaque clé. Ces autorisations vous offrent une meilleure sécurité et un meilleur contrôle sur les différentes zones de votre compte. 

![Autorisations de clé API disponibles lors de la création d'une clé API.][25]

{% alert warning %}
Étant donné que les clés de l'API REST permettent d'accéder à des points de terminaison de l'API REST potentiellement sensibles, assurez-vous qu'elles sont stockées et utilisées en toute sécurité. Par exemple, n'utilisez pas cette clé pour passer des appels AJAX depuis votre site Web ou pour l'exposer de toute autre manière publique.
{% endalert %}

En cas d'exposition accidentelle d'une clé, elle peut être supprimée de la console développeur. Pour obtenir de l'aide sur ce processus, ouvrez un [ticket d'assistance][support].

### Liste blanche d'adresses IP d'API

Pour plus de sécurité, vous pouvez spécifier une liste d'adresses IP et de sous-réseaux autorisés à effectuer des requêtes API REST pour une clé API REST donnée. C’est ce qu’on appelle la mise sur liste verte ou liste blanche. Pour autoriser des adresses IP ou des sous-réseaux spécifiques, ajoutez-les à la section **Liste blanche des adresses IP** lors de la création d'une nouvelle clé API REST : 

![Option de liste blanche des IP lors de la création d'une clé API][26]

Si vous n’en spécifiez aucune, les demandes peuvent être envoyées à partir de n’importe quelle adresse IP.

{% alert tip %}
Créer un webhook Braze-to-Braze et utiliser la liste blanche ? Consultez notre liste d' [adresses IP à ajouter à la liste blanche]({{site.baseurl}}/user_guide/message_building_by_channel/webhooks/creating_a_webhook/#ip-whitelisting).
{% endalert %}

## Ressources additionnelles

### Bibliothèque cliente Ruby

Si vous implémentez Braze à l'aide de Ruby, vous pouvez utiliser notre [bibliothèque client Ruby](https://github.com/braze-inc/braze-api-client-ruby) pour réduire le temps d'importation de vos données. Une bibliothèque client est une collection de code spécifique à un langage de programmation (dans ce cas, Ruby) qui facilite l'utilisation d'une API.

La bibliothèque client Ruby prend en charge les [points de terminaison utilisateur]({{site.baseurl}}/api/endpoints/user_data).

{% alert note %}
Cette bibliothèque client est actuellement en version bêta. Vous voulez nous aider à améliorer cette bibliothèque ? Envoyez-nous vos commentaires à [smb-product@braze.com](mailto:smb-product@braze.com).
{% endalert %}

[1]: https://en.wikipedia.org/wiki/UTF-8
[7]: {{site.baseurl}}/api/objects_filters/connected_audience/
[9]: {{site.baseurl}}/developer_guide/platform_integration_guides/swift/analytics/setting_user_ids/
[10]: {{site.baseurl}}/developer_guide/platform_integration_guides/android/analytics/setting_user_ids/
[13]: {{site.baseurl}}/developer_guide/platform_integration_guides/web/analytics/setting_user_ids/
[2]: {{site.baseurl}}/api/identifier_types/
[5]: {{site.baseurl}}/api/basics/
[6]: https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#intro
[25]: {% image_buster /assets/img_archive/api-key-permissions.png %}
[26]: {% image_buster /assets/img_archive/api-key-ip-whitelisting.png %}
[assistance] : {{site.baseurl}}/braze_support/
[28]: {% image_buster /assets/img_archive/create-new-key.png %}
[29]: {% image_buster /assets/img_archive/api-key-options.png %}
[27]: {% image_buster /assets/img_archive/rest-api-key.png %}
[30]: {% image_buster /assets/img_archive/view-api-key.png %}
