---
nav_title: "POST : Créer plusieurs articles de catalogue"
article_title: "POST : Créer plusieurs articles de catalogue"
search_tag: Endpoint
page_order: 3

layout: api_page
page_type: reference
description: "Cet article présente les détails du point de terminaison Créer plusieurs éléments de catalogue Braze."

---
{% api %}
# Créer plusieurs articles de catalogue
{% apimethod post %}
/catalogs/{catalog_name}/items
{% endapimethod %}

> Utilise ce point de terminaison pour créer plusieurs articles dans ton catalogue. 

Chaque demande peut prendre en charge jusqu'à 50 articles. Ce point d'arrivée est asynchrone.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#cea18bb3-b83a-4160-81fe-8cd42aa6e7cc {% endapiref %}

## Conditions préalables

Pour utiliser ce point de terminaison, tu auras besoin d'une [clé API]({{site.baseurl}}/api/basics#rest-api-key/) avec l'autorisation `catalogs.add_items`.

## Limite du taux

{% multi_lang_include rate_limits.md endpoint='asynchronous catalog item' %}

## Paramètres du chemin

| Paramètre | Exigée | Type de données | Description |
|---|---|---|---|
| `catalog_name` | Exigée | Chaîne | Nom du catalogue. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Paramètres de la demande

| Paramètre | Exigée | Type de données | Description |
|---|---|---|---|
| `items` | Exigée | Array | Un tableau qui contient des objets d'articles. Les objets de l'article doivent contenir tous les champs du catalogue. Jusqu'à 50 objets d'articles sont autorisés par demande. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Exemple de demande

```
curl --location --request POST 'https://rest.iad-03.braze.com/catalogs/restaurants/items' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY' \
--data-raw '{
  "items": [
    {
      "id": "restaurant1",
      "Name": "Restaurant1",
      "City": "New York",
      "Cuisine": "American",
      "Rating": 5,
      "Loyalty_Program": true,
      "Location": {
        "Latitude": 33.6112,
        "Longitude": -117.8711
      },
      "Created_At": "2022-11-01T09:03:19.967+00:00"
    },
    {
      "id": "restaurant2",
      "Name": "Restaurant2",
      "City": "New York",
      "Cuisine": "American",
      "Rating": 10,
      "Loyalty_Program": true,
      "Location": {
        "Latitude": 40.7413,
        "Longitude": -73.9764
      },
      "Created_At": "2022-11-02T09:03:19.967+00:00"
    },
    {
      "id": "restaurant3",
      "Name": "Restaurant3",
      "City": "New York",
      "Cuisine": "American",
      "Rating": 3,
      "Loyalty_Program": false,
      "Location": {
        "Latitude": 40.7489,
        "Longitude": -73.9972
      },
      "Created_At": "2022-11-03T09:03:19.967+00:00"
    }
  ]
}'
```

## Réponse

Il y a trois codes de statut pour ce point d'accès : `202`, `400`, et `404`.

### Exemple de réponse positive

Le code de statut `202` pourrait renvoyer le corps de réponse suivant.

```json
{
  "message": "success"
}
```

### Exemple de réponse à une erreur

Le code de statut `400` pourrait renvoyer le corps de réponse suivant. Reporte-toi à la rubrique [Dépannage](#troubleshooting) pour plus d'informations sur les erreurs que tu peux rencontrer.

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

Le tableau suivant répertorie les erreurs renvoyées possibles et les étapes de dépannage associées.

| Erreur | Dépannage |
| --- | --- |
| `catalog-not-found` | Vérifie que le nom du catalogue est valide. |
| `ids-not-strings` | Les identifiants des articles doivent être de type chaîne de caractères. |
| `ids-not-unique` | Les identifiants des articles doivent être uniques dans la demande. |
| `ids-too-large` | Les identifiants des articles ne peuvent pas dépasser 250 caractères. |
| `invalid-ids` | Les identifiants des articles ne peuvent comporter que des lettres, des chiffres, des traits d'union et des traits de soulignement. |
| `invalid-fields` | Confirme que tous les champs que tu envoies dans la requête API existent déjà dans le catalogue. Cela n'a rien à voir avec le champ d'identification mentionné dans l'erreur. |
| `invalid-keys-in-value-object` | Les clés d'objet de l'article ne peuvent pas inclure `.` ou `$`. |
| `item-array-invalid` | `items` doit être un tableau d'objets. |
| `items-missing-ids` | Il y a des articles qui n'ont pas d'identifiant. Vérifie que chaque article possède un identifiant. |
| `items-too-large` | Les valeurs des articles ne peuvent pas dépasser 5 000 caractères. |
| `request-includes-too-many-items` | Ta demande comporte trop d'éléments. La limite d'articles par demande est de 50. |
| `too-deep-nesting-in-value-object` | Les objets ne peuvent pas avoir plus de 50 niveaux d'imbrication. |
| `unable-to-coerce-value` | Les types d'articles ne peuvent pas être convertis. |
{: .reset-td-br-1 .reset-td-br-2}

{% endapi %}
