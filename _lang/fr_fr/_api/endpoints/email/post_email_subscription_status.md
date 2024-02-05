---
nav_title: "PUBLIER: Modifier l’état de l’abonnement aux e-mails"
article_title: "PUBLIER: Modifier l’état de l’abonnement aux e-mails"
search_tag: Endpoint
page_order: 5
layout: api_page
page_type: reference
description: "Cet article décrit les détails du point de terminaison Braze Modifier l’état de l’abonnement à la messagerie de l’utilisateur."

---
{% api %}
# Modifier l’état de l’abonnement aux e-mails
{% apimethod post core_endpoint|https://www.braze.com/docs/core_endpoints %}
/email/status
{% endapimethod %}

> Utilisez ce point de terminaison pour définir l’état de l’abonnement aux e-mails de vos utilisateurs. 

Les utilisateurs peuvent être `opted_in`, `unsubscribed`, ou (pas spécifiquement activés ou `subscribed` désactivés).

Vous pouvez définir l’état d’abonnement aux e-mails pour une adresse e-mail qui n’est pas encore associée à l’un de vos utilisateurs dans Braze. Lorsque cette adresse e-mail est ultérieurement associée à un utilisateur, l’état d’abonnement à l’e-mail que vous avez téléchargé est automatiquement défini.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#be852462-0cda-4a48-b68b-85bd8a9f2147 {% endapiref %}

## Conditions préalables

Pour utiliser ce point de terminaison, vous aurez besoin d’une [clé]({{site.baseurl}}/api/basics#rest-api-key/) API avec l’autorisation `email.status` .

## Limite de débit

{% multi_lang_include rate_limits.md endpoint='default' %}

## Corps de la requête

```
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
```

```json
{
  "email": "example@braze.com",
  "subscription_state": "subscribed"
}
```

## Paramètres de la requête

| Paramètre | Obligatoire | Type de données | Description |
| --------- | ---------| --------- | ----------- |
| `email` | Obligatoire | Chaîne ou tableau | Chaîne d’adresse e-mail à modifier ou tableau de 50 adresses e-mail maximum à modifier. |
| `subscription_state` | Obligatoire | Corde | Soit « abonné », « désabonné » ou « opted_in ». |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Exemple de demande
```
curl --location --request POST 'https://rest.iad-01.braze.com/email/status' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-API-KEY-HERE' \
--data-raw '{
  "email": "example@braze.com",
  "subscription_state": "subscribed"
}'
```


{% endapi %}
