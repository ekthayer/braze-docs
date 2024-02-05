---
nav_title: "PUT: Mettre à jour plusieurs éléments du catalogue"
article_title: "PUT: Mettre à jour plusieurs éléments du catalogue"
search_tag: Endpoint
page_order: 4

layout: api_page
page_type: reference
description: "Cet article présente des détails sur le point de terminaison Braze de mise à jour de plusieurs éléments du catalogue."

---
{% api %}
# Mettre à jour les articles du catalogue
{% apimethod put %}
/catalogs/{catalog_name}/items
{% endapimethod %}

> Utilisez ce paramètre pour mettre à jour plusieurs éléments de votre catalogue. 

Si un article de catalogue n'existe pas, ce point de terminaison créera l'article dans votre catalogue. Chaque demande peut prendre en charge jusqu'à 50 articles de catalogue. Ce paramètre est asynchrone.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#ab30a4fc-60bc-4460-885c-1b92af8bc061 {% endapiref %}

## Prérequis

Pour utiliser ce point de terminaison, vous aurez besoin d'une [clé API]({{site.baseurl}}/api/basics#rest-api-key/) avec l'autorisation `catalogs.replace_items`.

## Limite tarifaire

{% multi_lang_include rate_limits.md endpoint='asynchronous catalog item' %}

## Paramètres du chemin

| Paramètre | Obligatoire | Type de données | Description |
|---|---|---|---|
| `catalog_name` | Obligatoire | String | Nom du catalogue. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Paramètres de requête

| Paramètre | Obligatoire | Type de données | Description |
|---|---|---|---|
| `items` | Obligatoire | Array | Un tableau qui contient des objets d'élément. Chaque objet doit avoir un ID. Les objets d'élément doivent contenir des champs qui existent dans le catalogue. Jusqu'à 50 objets sont autorisés par demande. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Exemple de demande

```
curl --location --request PUT 'https://rest.iad-03.braze.com/catalogs/restaurants/items' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY' \
--data-raw '{
  "items": [
    {
      "id": "restaurant1",
      "Name": "Restaurant",
      "Loyalty_Program": false,
      "Location": {
        "Latitude": 33.6112,
        "Longitude": -117.8711
      },
      "Open_Time": "2021-09-03T09:03:19.967+00:00"
    },
    {
      "id": "restaurant3",
      "City": "San Francisco",
      "Rating": 2
    }
  ]
}'
```

## Réponse

Il existe trois réponses de code d'état pour ce paramètre : `202`, `400` et `404`.

### Exemple de réponse au succès

Le `202` de code d'état pourrait renvoyer le corps de réponse suivant.

```json
{
  "message": "success"
}
```

### Exemple de réponse d'erreur

Le `400` de code d'état pourrait renvoyer le corps de réponse suivant. Reportez-vous à la section [Dépannage](#troubleshooting) pour plus d'informations sur les erreurs que vous pouvez rencontrer.

```json
{
  "errors": [
    {
      "id": "invalid-fields",
      "message": "Some of the fields given do not exist in the catalog",
      "parameters": [
        "id"
      ],
      "parameter_values": [
        "restaurant1"
      ]
    }
  ],
  "message": "Invalid Request"
}
```

## Dépannage

Le tableau suivant répertorie les erreurs retournées possibles et les étapes de dépannage associées.

| Erreur | Dépannage |
| --- | --- |
| `catalog-not-found` | Vérifiez que le nom du catalogue est valide. | 
| `ids-not-string` | Confirmez que chaque ID d'élément est une chaîne. |
| `ids-not-unique` | Vérifiez que chaque ID d'article est unique. |
| `ids-too-large` | La limite de caractères pour chaque ID d'objet est de 250 caractères. |
| `item-array-invalid` | `items` doit être un tableau d'objets. |
| `items-missing-ids` | Confirmez que chaque élément a un ID. |
| `items-too-large` | Les valeurs des objets ne peuvent pas dépasser 5 000 caractères. |
| `invalid-ids` | Les caractères pris en charge pour les noms d'ID d'élément sont des lettres, des chiffres, des traits d'union et des soulignements. |
| `invalid-fields` | Confirmez que tous les champs que vous envoyez dans la demande d'API existent déjà dans le catalogue. Ceci n'est pas lié au champ ID mentionné dans l'erreur. |
| `invalid-keys-in-value-object` | Les touches d'objet d'élément ne peuvent pas inclure de `.` ou de `$`. |
| `too-deep-nesting-in-value-object` | Les objets ne peuvent pas avoir plus de 50 niveaux d'imbrication. |
| `request-includes-too-many-items` | Votre demande comporte trop d'éléments. La limite d'article par demande est de 50. |
| `unable-to-coerce-value` | Les types d'articles ne peuvent pas être convertis. |
{: .reset-td-br-1 .reset-td-br-2}

{% endapi %}
