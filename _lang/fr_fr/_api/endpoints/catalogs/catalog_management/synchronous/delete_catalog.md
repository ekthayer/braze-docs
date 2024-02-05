---
nav_title: "SUPPRIMER : Supprimer le catalogue"
article_title: "SUPPRIMER : Supprimer le catalogue"
search_tag: Endpoint
page_order: 1

layout: api_page
page_type: reference
description: "Cet article présente des détails sur le point de terminaison Supprimer le catalogue Braze."

---
{% api %}
# Supprimer le catalogue
{% apimethod delete %}
/catalogs/{catalog_name}
{% endapimethod %}

> Utilise ce point de terminaison pour supprimer un catalogue.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#c0915a86-797a-4486-8217-24cd1c689d0f {% endapiref %}

## Conditions préalables

Pour utiliser ce point de terminaison, tu auras besoin d'une [clé API]({{site.baseurl}}/api/basics#rest-api-key/) avec l'autorisation `catalogs.delete`.

## Limite du taux

{% multi_lang_include rate_limits.md endpoint='synchronous catalog' %}

## Paramètres du chemin

| Paramètre | Exigée | Type de données | Description |
|---|---|---|---|
| `catalog_name` | Exigée | Chaîne | Nom du catalogue. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Exemple de demande

```
curl --location --request DELETE 'https://rest.iad-03.braze.com/catalogs/restaurants' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY' \
```

## Réponse

Il existe deux codes de statut pour ce point d'accès : `200` et `404`.

### Exemple de réponse positive

Le code de statut `200` pourrait renvoyer le corps de réponse suivant :

```json
{
  "message": "success"
}
```

### Exemple de réponse à une erreur

Le code de statut `404` pourrait renvoyer le corps de réponse suivant. Reporte-toi à la rubrique [Dépannage](#troubleshooting) pour plus d'informations sur les erreurs que tu peux rencontrer.

```json
{
  "errors": [
    {
      "id": "catalog-not-found",
      "message": "Could not find catalog",
      "parameters": [
        "catalog_name"
      ],
      "parameter_values": [
        "restaurants"
      ]
    }
  ],
  "message": "Invalid Request"
}
```

## Dépannage 

Le tableau suivant répertorie les erreurs renvoyées possibles et les étapes de dépannage associées.

| Erreur | Dépannage |
| --- | --- |
| `catalog-not-found` | Vérifie que le nom du catalogue est valide. |
{: .reset-td-br-1 .reset-td-br-2}

{% endapi %}