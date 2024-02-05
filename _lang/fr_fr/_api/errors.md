---
nav_title: Erreurs & Réponses
article_title: "Erreurs et réponses de l'API"
description: "Cet article de référence couvre les différentes erreurs et réponses du serveur qui peuvent apparaître lors de l'utilisation de l'API Braze et comment les résoudre." 
page_type: reference
page_order: 2.3

---
# Erreurs et réponses de l'API

> Cet article de référence couvre les différentes erreurs et réponses du serveur qui peuvent apparaître lors de l'utilisation de l'API Braze et comment les résoudre. 

{% raw %}

## Réponses du serveur

Si votre charge utile POST a été acceptée par nos serveurs, alors les messages réussis seront accueillis avec la réponse suivante:

```json
{
  "message" : "success"
}
```

Notez que le succès signifie seulement que la charge utile de l'API RESTful a été correctement formée et transmise sur notre notification push ou email ou d'autres services de messagerie. Cela ne signifie pas que les messages ont été effectivement délivrés, car des facteurs supplémentaires pourraient empêcher le message d'être délivré (par exemple, un appareil pourrait être hors ligne, le jeton push pourrait être rejeté par les serveurs d'Apple, vous pourriez avoir fourni un identifiant utilisateur inconnu).

Si votre message est réussi mais comporte des erreurs non fatales, vous recevrez la réponse suivante:

```json
{
  "message" : "success", "errors" : [<minor error message>]
}
```

En cas de succès, tous les messages qui n'ont pas été affectés par une erreur dans le tableau de `errors` seront toujours livrés. Si votre message comporte une erreur fatale, vous recevrez la réponse suivante:

```json
{
  "message" : <fatal error message>, "errors" : [<minor error message>]
}
```

## Réponses pour les ID d'envoi suivis

Les analyses sont toujours disponibles pour les campagnes. En outre, des analyses sont disponibles pour une instance d'envoi de campagne spécifique lorsque la campagne est envoyée en tant que diffusion. Lorsque le suivi est disponible pour une instance d'envoi de campagne spécifique, vous recevrez la réponse suivante :

```json
{
  "message": "success", "send_id" : "example_send_id"
}
```

L'id d'envoi fourni peut être utilisé comme paramètre pour que le point de terminaison `/send/data_series` puisse retirer l'analyse d'envoi spécifique.

## Erreurs

L'élément de code d'état d'une réponse serveur est un nombre à 3 chiffres où le premier chiffre du code définit la classe de réponse.

- Le code d'état de la **classe 2XX** (non mortel) indique que **votre demande a** été reçue, comprise et acceptée avec succès.
- La **classe 4XX** du code d'état (fatal) indique une **erreur client**. Consultez le tableau des erreurs fatales pour une liste complète des codes d'erreur et des descriptions 4XX.
- La **classe 5XX** du code d'état (fatal) indique une **erreur de serveur**. Il y a plusieurs causes potentielles, par exemple, le serveur auquel vous essayez d'accéder est incapable d'exécuter la requête, le serveur subit une maintenance le rendant incapable d'exécuter la requête, ou le serveur subit des niveaux élevés de trafic. Lorsque cela se produit, nous vous recommandons de réessayer votre demande avec un backoff exponentiel. En cas d'incident ou de panne, Braze n'est pas en mesure de rejouer un appel REST API qui a échoué pendant la fenêtre d'incident. Vous devrez réessayer tous les appels qui ont échoué pendant la fenêtre d'incident.

### Erreurs fatales

Les codes d'état suivants et les messages d'erreur associés seront retournés si votre demande rencontre une erreur fatale.

{% endraw %}
{% alert warning %}
Tous les codes d'erreur suivants indiquent qu'aucun message ne sera envoyé.
{% endalert %}
{% raw %}

| Code d'erreur | Description |
|---|---|
| `5XX Internal Server Error` | **Vous devriez réessayer votre demande avec un recul exponentiel.**|
| `400 Bad Request` | Mauvaise syntaxe.|
| `400 No Recipients` | Il n'y a pas d'identifiants externes ou de segments ou pas de jetons push dans la requête.|
| `400 Invalid Campaign ID` | Aucune campagne d'API de messagerie n'a été trouvée pour l'ID de campagne que vous avez fourni.|
| `400 Message Variant Unspecified` | Vous fournissez un ID de campagne mais aucun ID de variation de message.|
| `400 Invalid Message Variant` | Vous avez fourni un ID de campagne valide, mais l'ID de variation de message ne correspond à aucun des messages de cette campagne.|
| `400 Mismatched Message Type` | Vous avez fourni une variation de message du mauvais type de message pour au moins un de vos messages.|
| `400 Invalid Extra Push Payload` | Vous fournissez la clé de `extra` pour `apple_push` ou `android_push` mais ce n'est pas un dictionnaire.|
| `400 Max Input Length Exceeded` | Provoqué par l'appel à plus de 75 ID externes lors de l'accès au point de terminaison `/users/track`.|
| `400 The max number of external_ids and aliases per request was exceeded` | Causé par l'appel de plus de 50 ID externes.|
| `400 The max number of ids per request was exceeded` | Causé par l'appel à plus de 50 identifiants externes.|
| `400 No message to send` | Aucune charge utile n'est spécifiée pour le message.|
| `400 Slideup Message Length Exceeded` | Le message Slideup contient plus de 140 caractères.|
| `400 Apple Push Length Exceeded` | La charge utile JSON est de plus de 1 912 octets.|
| `400 Android Push Length Exceeded` | La charge utile JSON est de plus de 4 000 octets.|
| `400 Bad Request` | Impossible d'analyser send_at datetime.|
| `400 Bad Request` | Dans votre demande, la `in_local_time` est vraie mais la `time` est passée dans le fuseau horaire de votre entreprise.|
| `401 Unauthorized` | Clé API invalide.|
| `403 Forbidden` | Le plan tarifaire ne prend pas en charge ou le compte est autrement inactivé.|
| `403 Access Denied` | La clé REST API que vous utilisez ne dispose pas des autorisations suffisantes, vérifiez les autorisations de clé API dans la Braze Developer Console.|
| `404 Not Found` | Clé d'API REST inconnue.|
| `429 Rate Limited` | Hors limite de taux.|
{: .reset-td-br-1 .reset-td-br-2}

{% endraw %}
