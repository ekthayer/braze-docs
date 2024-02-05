---
nav_title: "GET: Liste État d'abonnement avec adresse e-mail ou numéro de téléphone"
article_title: "GET: Liste État d'abonnement avec adresse e-mail ou numéro de téléphone"
search_tag: Endpoint
page_order: 2
hidden: true
layout: api_page
page_type: reference
description: "Cet article décrit les détails de l'état d'abonnement Liste avec une adresse e-mail ou un numéro de téléphone Braze endpoint."

---
{% api %}
# Lister l'état d'abonnement avec une adresse e-mail ou un numéro de téléphone
{% apimethod get %}
/users/subscription
{% endapimethod %}

> Utilisez ce point de terminaison pour retourner la valeur de l'état d'abonnement en fonction d'une adresse e-mail ou d'un numéro de téléphone.

## Paramètres de requête

| Paramètre | Obligatoire | Type de données | Description |
| --- | --- | --- | --- |
| `email` | Oui | String | L'adresse e-mail de l'utilisateur (doit inclure au moins une adresse et au plus 50 adresses). |
| `phone` | Oui | String | Le numéro de téléphone de l'utilisateur (doit inclure au moins un numéro de téléphone et au plus 50 numéros de téléphone). Nous vous recommandons de le fournir au format E.164. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Exemple de demande
```
curl --location --request GET 'https://rest.iad-01.braze.com/users/subscriptions?phone=+12123355555&email=example%40braze.com' \
--header 'Authorization: Bearer YOUR_REST_API_KEY'
```

## Réponse

Les entrées sont classées par ordre décroissant.

```json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
  "emails": [
    {
      "email": "example@braze.com",
      "email_subscribe": {
        "email_subscription_event_date": "2019-11-20T19:58:04.825Z",
        "email_subscription_state": "Subscribed"
      },
      "subscription_group": [
        {
          "subscription_group_id": "5f5536d2a76e0f4e323a1234",
          "subscription_group_event_date": "2021-03-11T21:29:22.347Z",
          "subscription_group_state": "Unsubscribed"
        }
      ],
      "hard_bounced_at": null,
      "spam_at": null
    }
  ],
	"phone": [{
		"phone": "+12123355555",
		"subscription_group": [{
			"subscription_group_id": "3f5536d2a76e0f4e323a5555",
			"subscription_group_state": "Subsscribed",
			"subscription_group_event_date": "2021-03-11T21:29:22.347Z"
		}]
	}],
	"message": "success"
}
```

{% endapi %}