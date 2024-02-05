---
nav_title: "AVOIR: Répertorier les détails de l’élément du catalogue"
article_title: "AVOIR: Répertorier les détails de l’élément du catalogue"
search_tag: Endpoint
page_order: 2

layout: api_page
page_type: reference
description: "Cet article décrit les détails de l’extrémité Braze des détails de l’élément de catalogue Lister."

---
{% api %}
# Répertorier les détails des éléments du catalogue
{% apimethod get %}
/catalogs/{catalog_name}/items/{item_id}
{% endapimethod %}

> Utilisez ce point de terminaison pour renvoyer un élément de catalogue et son contenu.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#52c6631c-7366-48e5-9e0e-16de7b6285cc {% endapiref %}

## Conditions préalables

Pour utiliser ce point de terminaison, vous aurez besoin d’une [clé]({{site.baseurl}}/api/basics#rest-api-key/) API avec l’autorisation `catalogs.get_item` .

## Limite de débit

{% multi_lang_include rate_limits.md endpoint='synchronous catalog item' %}

## Paramètres de chemin

| Paramètre | Obligatoire | Type de données | Description |
|---|---|---|---|
| `catalog_name` | Obligatoire | Corde | Nom du catalogue. |
| `item_id` | Obligatoire | Corde | ID de l’élément de catalogue. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Paramètres de la requête

Il n’y a pas de corps de requête pour ce point de terminaison.

## Exemple de demande

```
curl --location --request GET 'https://rest.iad-03.braze.com/catalogs/restaurants/items/restaurant1' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'
```

## Réponse

Il existe deux réponses de code d’état pour ce point de terminaison : `200` et `404`.

### Exemple de réponse de réussite

Le code `200` d’état peut renvoyer le corps de la réponse suivant.

```json
{
  "items": [
    {
      "id": "restaurant3",
      "Name": "Restaurant1",
      "City": "New York",
      "Cuisine": "American",
      "Rating": 5,
      "Loyalty_Program": true,
      "Open_Time": "2022-11-01T09:03:19.967Z"
    }
  ],
  "message": "success"
}
```

### Exemple de réponse d’erreur

Le code `404` d’état peut renvoyer la réponse suivante. Reportez-vous à [la section Dépannage](#troubleshooting) pour plus d’informations sur les erreurs que vous pouvez rencontrer.

```json
{
  "errors": [
    {
      "id": "item-not-found",
      "message": "Could not find item",
      "parameters": [
        "item_id"
      ],
      "parameter_values": [
        "restaurant34"
      ]
    }
  ],
  "message": "Invalid Request"
}
```

## Dépannage

Le tableau suivant répertorie les erreurs renvoyées possibles et les étapes de dépannage associées, le cas échéant.

| Erreur | Dépannage |
| --- | --- |
| `catalog-not-found` | Vérifiez que le nom du catalogue est valide. |
| `item-not-found` | Vérifiez que l’article figure dans le catalogue. |
{: .reset-td-br-1 .reset-td-br-2}

{% endapi %}