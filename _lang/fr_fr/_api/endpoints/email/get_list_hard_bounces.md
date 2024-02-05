---
nav_title: "GET: Query Hard Bounced Emails"
article_title: "GET: Query Hard Bounced Emails"
search_tag: Endpoint
page_order: 1
layout: api_page
page_type: reference
description: "Cet article décrit les détails sur le point de terminaison Braze Requête ou liste des adresses e-mail rebondies."

---
{% api %}
# Requête des emails hard bounced
{% apimethod get %}
/email/hard_bounces
{% endapimethod %}

> Utilisez ce point de terminaison pour tirer une liste d'adresses électroniques qui ont « rebondi » vos messages électroniques dans un certain délai.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#7c2ef84f-ddf5-451a-a72c-beeabc06ad9d {% endapiref %}

## Prérequis

Pour utiliser ce point de terminaison, vous aurez besoin d'une [clé API]({{site.baseurl}}/api/basics#rest-api-key/) avec l'autorisation `email.hard_bounces`.

## Limite tarifaire

{% multi_lang_include rate_limits.md endpoint='default' %}

## Paramètres de requête

| Paramètre | Obligatoire | Type de données | Description |
| ----------|-----------| ----------|----- |
| `start_date` | Facultatif<br>(voir note) | Chaîne au format AAAA-MM-JJ| La date de début de la plage pour récupérer les hard bounces, doit être antérieure à la `end_date`. Ceci est traité comme minuit en temps UTC par l'API. |
| `end_date` | Facultatif<br>(voir note) | Chaîne au format AAAA-MM-JJ | Date de fin de la plage pour récupérer les hard bounces. Ceci est traité comme minuit en temps UTC par l'API. |
| `limit` | Facultatif | Entier | Champ facultatif pour limiter le nombre de résultats renvoyés. Par défaut 100, maximum 500. |
| `offset` | Facultatif | Entier | Point de départ optionnel dans la liste où récupérer. |
| `email` | Facultatif<br>(voir note) | String | Si fourni, nous retournerons si l'utilisateur a durement rebondi ou non. Vérifiez que les chaînes de courriel sont correctement formatées. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

{% alert note %}
Vous devez fournir un `start_date` et un `end_date`, OU un `email`. Si vous fournissez les trois, `start_date`, `end_date` et un `email`, nous donnons la priorité aux courriels donnés et ne tenons pas compte de la plage de dates.
{% endalert %}

Si votre plage de dates a plus que le nombre `limit` de hard bounces, vous devrez faire plusieurs appels API, augmentant à chaque fois le `offset` jusqu'à ce qu'un appel retourne moins de `limit` ou zéro résultat. Inclure les paramètres `offset` et `limit` avec `email` peut retourner une réponse vide. 

## Exemple de demande
```
curl --location --request GET 'https://rest.iad-01.braze.com/email/hard_bounces?start_date=2019-01-01&end_date=2019-02-01&limit=100&offset=1&email=example@braze.com' \
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
      "email": (string) an email that has hard bounced,
      "unsubscribed_at": (string) the time the email hard bounced in ISO 8601
    },
    {
      "email": (string) an email that has hard bounced,
      "unsubscribed_at": (string) the time the email hard bounced in ISO 8601
    },
    {
      "email": (string) an email that has hard bounced,
      "unsubscribed_at": (string) the time the email hard bounced in ISO 8601
    }
  ],
  "message": "success"
}
```
{% endapi %}
