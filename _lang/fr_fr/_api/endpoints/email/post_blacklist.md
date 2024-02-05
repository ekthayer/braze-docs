---
nav_title: "POST : Liste noire de courriels"
article_title: "POST : Liste noire de courriels"
search_tag: Endpoint
page_order: 10
layout: api_page
page_type: reference
alias: /blacklist/
description: "Cet article présente les détails du point de terminaison Braze de la liste noire des courriels."

---
{% api %}
# Liste noire de courriels
{% apimethod post core_endpoint|https://www.braze.com/docs/core_endpoints %}
/email/blacklist
{% endapimethod %}

{% alert important %}
Braze a lancé le [point d'accès`/email/blocklist` ]({{site.baseurl}}/api/endpoints/email/post_blocklist/) qui offre les mêmes fonctionnalités que le point d'accès `/email/blacklist`. Nous te recommandons d'utiliser plutôt le point de terminaison `/email/blocklist`.
{% endalert %}

> Utilise ce point de terminaison pour désabonner un utilisateur d'un courriel et le marquer comme ayant subi un rebond.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#d51155a1-a6e8-4dcc-9f2b-88c54ab9e8c6 {% endapiref %}

## Conditions préalables

Pour utiliser ce point de terminaison, tu auras besoin d'une [clé API]({{site.baseurl}}/api/basics#rest-api-key/) avec l'autorisation `email.blacklist`.

## Limite du taux

{% multi_lang_include rate_limits.md endpoint='default' %}

## Corps de la demande

```
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
```

```json
{
  "email": ["blacklist_email1","blacklist_email2"]
}
```

## Paramètres de la demande

| Paramètre | Exigée | Type de données | Description |
| -----------|----------| --------|------- |
| `email` | Exigée | Chaîne ou tableau | Chaîne de l'adresse électronique à mettre sur liste noire, ou tableau de 50 adresses électroniques maximum à mettre sur liste noire. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Exemple de demande
```
curl --location --request POST 'https://rest.iad-01.braze.com/email/blacklist' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-API-KEY-HERE' \
--data-raw '{
  "email": ["blacklist_email1","blacklist_email2"]
}'
```

{% endapi %}


