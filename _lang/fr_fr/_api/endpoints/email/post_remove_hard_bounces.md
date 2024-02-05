---
nav_title: "POST: Supprimer les courriels rebondis durs"
article_title: "POST: Supprimer les courriels rebondis durs"
search_tag: Endpoint
page_order: 6
layout: api_page
page_type: reference
description: "Cet article présente des détails sur le point de terminaison Braze Remove hard bounced email address."

---
{% api %}
# Supprimer les emails rebondis
{% apimethod post %}
/email/bounce/remove
{% endapimethod %}

> Utilisez ce point de terminaison pour supprimer les adresses e-mail de votre liste de rebond Braze et de la liste de rebond maintenue par votre fournisseur de messagerie.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#7b87a884-fa20-4085-b9f1-18363103575f {% endapiref %}

## Prérequis

Pour utiliser ce point de terminaison, vous aurez besoin d'une [clé API]({{site.baseurl}}/api/basics#rest-api-key/) avec l'autorisation `email.bounce.remove`.

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
| ----------|-----------| ---------|------ |
| `email` | Obligatoire | Chaîne ou tableau | Chaîne d'adresse e-mail à modifier, ou un tableau allant jusqu'à 50 adresses e-mail à modifier. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Exemple de demande
```
curl --location --request POST 'https://rest.iad-01.braze.com/email/bounce/remove' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY' \
--data-raw '{
  "email": "example@braze.com"
}'
```

{% endapi %}
