---
nav_title: "POST: Supprimer les adresses e-mail de la liste de spam"
article_title: "POST: Supprimer les adresses e-mail de la liste de spam"
search_tag: Endpoint
page_order: 7
layout: api_page
page_type: reference
description: "Cet article décrit des détails sur le point de terminaison Supprimer les adresses e-mail de la liste de spam Braze."

---
{% api %}
# Supprimer les adresses e-mail de la liste de spam
{% apimethod post %}
/email/spam/remove
{% endapimethod %}

> Utilisez ce point de terminaison pour supprimer les adresses e-mail de votre liste de spam Braze et de la liste de spam maintenue par votre fournisseur de messagerie.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#1614a82f-510a-4c37-95a6-8207a125e487 {% endapiref %}

## Prérequis

Pour utiliser ce point de terminaison, vous aurez besoin d'une [clé API]({{site.baseurl}}/api/basics#rest-api-key/) avec l'autorisation `email.spam.remove`.

## Limite tarifaire

{% multi_lang_include rate_limits.md endpoint='default' %}

## Organisme demandeur
```
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
```

```json
{
  "email": "example@braze.com"
}
```

## Paramètres de requête

| Paramètre | Obligatoire | Type de données | Description |
| ----------|-----------| --------|------- |
| `email` | Obligatoire | Chaîne ou tableau | Chaîne d'adresse e-mail à modifier, ou un tableau allant jusqu'à 50 adresses e-mail à modifier. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Exemple de demande
```
curl --location --request POST 'https://rest.iad-01.braze.com/email/spam/remove' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY' \
--data-raw '{
  "email": "example@braze.com"
}'
```
{% endapi %}
