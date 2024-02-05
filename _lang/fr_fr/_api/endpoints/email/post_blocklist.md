---
nav_title: "POST: Blocklist Emails"
article_title: "POST: Blocklist Emails"
search_tag: Endpoint
page_order: 8
layout: api_page
page_type: reference
description: "Cet article décrit les détails du point de terminaison Braze de Blocklist emails."

---
{% api %}
# Blocklist emails
{% apimethod post core_endpoint|https://www.braze.com/docs/core_endpoints %}
/email/blocklist
{% endapimethod %}

> Utilisez ce point de terminaison pour désinscrire un utilisateur du courrier électronique et le marquer comme rebondi.
 
{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#d51155a1-a6e8-4dcc-9f2b-88c54ab9e8c6 {% endapiref %}

## Prérequis

Pour utiliser ce point de terminaison, vous aurez besoin d'une [clé API]({{site.baseurl}}/api/basics#rest-api-key/) avec l'autorisation `email.blacklist`.

## Limite tarifaire

{% multi_lang_include rate_limits.md endpoint='default' %}

## Organisme demandeur

```
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
```

```json
{
  "email": ["blocklist_email1","blocklist_email2"]
}
```

## Paramètres de requête

| Paramètre | Obligatoire | Type de données | Description |
| -----------|----------| --------|------- |
| `email` | Obligatoire | Chaîne ou tableau | Chaîne d'adresse e-mail à la liste de blocage, ou un tableau d'un maximum de 50 adresses e-mail à la liste de blocage. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Exemple de demande
```
curl --location --request POST 'https://rest.iad-01.braze.com/email/blocklist' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-API-KEY-HERE' \
--data-raw '{
  "email": ["blocklist_email1","blocklist_email2"]
}'
```

{% endapi %}
