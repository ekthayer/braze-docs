---
nav_title: "SUPPRIMER : Supprimer l'état d'abonnement par adresse e-mail ou numéro de téléphone"
article_title: "SUPPRIMER : Supprimer l'état d'abonnement par adresse e-mail ou numéro de téléphone"
search_tag: Endpoint
page_order: 0
hidden: true
layout: api_page
page_type: reference
description: "Cet article décrit les détails de l'état Supprimer l'abonnement par adresse e-mail ou numéro de téléphone Braze endpoint."

---

{% api %}
# Supprimer l'état d'abonnement par adresse e-mail ou numéro de téléphone
{% apimethod delete %}
/users/subscription
{% endapimethod %}

> Utilisez ce point de terminaison pour supprimer la valeur de l'état d'abonnement en fonction d'une adresse e-mail ou d'un numéro de téléphone.

## Paramètres de requête

| Paramètre | Obligatoire | Type de données | Description |
| --- | --- | --- | --- |
| `email` | Oui | String | L'adresse e-mail de l'utilisateur (doit inclure au moins une adresse et au plus 50 adresses). |
| `phone` | Oui | String | Le numéro de téléphone de l'utilisateur (doit inclure au moins un numéro de téléphone et au plus 50 numéros de téléphone). Nous vous recommandons de le fournir au format E.164. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Exemple de demande

```json
Content-Type: application/json
Authorization: Bearer YOUR_REST_API_KEY
{
  {phone: "+12125551212"},
  {email: "dont.spam@me.com"},
  {phone: "+17185551212"}
}
```

## Réponse

```json
{
  "status": "The emails and/or phone numbers have been queued for deletion",
  "message": "success"
}
```

{% endapi %}