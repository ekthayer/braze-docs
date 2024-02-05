---
nav_title: "GET : Demande une liste d'adresses électroniques désabonnées"
article_title: "GET : Demande une liste d'adresses électroniques désabonnées"
search_tag: Endpoint
page_order: 3
layout: api_page
page_type: reference
description: "Cet article présente les détails concernant le point de terminaison Récupérer la liste des ou interroger les désabonnements aux courriels Braze."

---
{% api %}
# Demande la liste des adresses électroniques désabonnées
{% apimethod get %}
/email/unsubscribes
{% endapimethod %}

> Utilise ce point de terminaison pour renvoyer les derniers courriels qui se sont désabonnés pendant la période allant de `start_date` à `end_date`. Pour un historique complet de l'état de l'abonnement, utilise [Currents]({{site.baseurl}}/user_guide/data_and_analytics/braze_currents) pour suivre ces données.

Tu peux utiliser ce point de terminaison pour mettre en place une synchronisation bidirectionnelle entre Braze et d'autres systèmes de messagerie ou ta propre base de données.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#d2966b81-188a-407b-ba7e-e6c252c44b4a {% endapiref %}

## Conditions préalables

Pour utiliser ce point de terminaison, tu auras besoin d'une [clé API]({{site.baseurl}}/api/basics#rest-api-key/) avec l'autorisation `email.unsubscribe`.

## Limite du taux

{% multi_lang_include rate_limits.md endpoint='default' %}

## Paramètres de la demande

| Paramètre | Exigée | Type de données | Description |
| ----------|-----------| ---------|------ |
| `start_date` | En option <br>(voir note) | Chaîne au format AAAA-MM-JJ| Date de début de l'intervalle pour récupérer les désabonnements, doit être antérieure à end_date. L'API considère qu'il s'agit de minuit en heure UTC. |
| `end_date` | En option <br>(voir note) | Chaîne au format AAAA-MM-JJ | Date de fin de l'intervalle pour récupérer les désabonnements. L'API considère qu'il s'agit de minuit en heure UTC. |
| `limit` | En option | Entier | Champ facultatif permettant de limiter le nombre de résultats renvoyés. La valeur par défaut est 100, la valeur maximale est 500. |
| `offset` | En option | Entier | Point de départ facultatif de la liste à partir duquel la recherche doit être effectuée. |
| `sort_direction` | En option | Chaîne | Passe la valeur `asc` pour trier les désabonnements du plus ancien au plus récent. Passe à `desc` pour trier du plus récent au plus ancien. Si `sort_direction` n'est pas inclus, l'ordre par défaut est du plus récent au plus ancien. |
| `email` | En option <br>(voir note) | Chaîne | Si cette information est fournie, nous indiquerons si l'utilisateur s'est désabonné ou non. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

{% alert note %}
Tu dois fournir un `end_date`, ainsi qu'un `email` ou un `start_date`.
{% endalert %}

Si ta plage de dates comporte plus de `limit` nombre de désabonnements, tu devras effectuer plusieurs appels API, en augmentant à chaque fois `offset` jusqu'à ce qu'un appel renvoie soit moins de `limit`, soit zéro résultat.

## Exemple de demande 
```
curl --location --request GET 'https://rest.iad-01.braze.com/email/unsubscribes?start_date=2020-01-01&end_date=2020-02-01&limit=1&offset=1&sort_direction=desc&email=example@braze.com' \
--header 'Authorization: Bearer YOUR-API-KEY-HERE'
```

## Réponse

Les entrées sont classées par ordre décroissant.

```json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
  "emails": [
    {
      "email": (string) an email that has been unsubscribed,
      "unsubscribed_at": (string) the time the email was unsubscribed in ISO 8601
    },
    {
      "email": (string) an email that has been unsubscribed,
      "unsubscribed_at": (string) the time the email was unsubscribed in ISO 8601
    },
    {
      "email": (string) an email that has been unsubscribed,
      "unsubscribed_at": (string) the time the email was unsubscribed in ISO 8601
    }
  ],
  "message": "success"
}
```
{% endapi %}
