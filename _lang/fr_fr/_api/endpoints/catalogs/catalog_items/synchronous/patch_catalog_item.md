---
nav_title: "PATCH: Modifier l'article du catalogue"
article_title: "PATCH: Modifier l'article du catalogue"
search_tag: Endpoint
page_order: 4

layout: api_page
page_type: reference
description: "Cet article présente des détails sur l'élément de catalogue Modifier le paramètre Braze."

---
{% api %}
# Modifier le catalogue
{% apimethod patch %}
/catalogs/{catalog_name}/items/{item_id}
{% endapimethod %}

> Utilisez ce paramètre pour modifier un élément existant dans votre catalogue.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#e35976ae-ff77-42b7-b691-a883c980d8c0 {% endapiref %}

## Prérequis

Pour utiliser ce point de terminaison, vous aurez besoin d'une [clé API]({{site.baseurl}}/api/basics#rest-api-key/) avec l'autorisation `catalogs.update_item`.

## Limite tarifaire

{% multi_lang_include rate_limits.md endpoint='synchronous catalog item' %}

## Paramètres du chemin

| Paramètre | Obligatoire | Type de données | Description |
|---|---|---|---|
| `catalog_name` | Obligatoire | String | Nom du catalogue. |
| `item_id` | Obligatoire | String | L'ID de l'article du catalogue. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Paramètres de requête

| Paramètre | Obligatoire | Type de données | Description |
|---|---|---|---|
| `items` | Obligatoire | Array | Un tableau qui contient des objets d'élément. Les objets d'élément doivent contenir des champs qui existent dans le catalogue à l'exception du champ `id`. Un seul objet item est autorisé par requête. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Exemple de demande

```
curl --location --request PATCH 'https://rest.iad-03.braze.com/catalogs/restaurants/items/restaurant1' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY' \
--data-raw '{
  "items": [
    {
      "Name": "Restaurant",
      "Loyalty_Program": false,
      "Location": {
        "Latitude": 33.6112,
        "Longitude": -117.8711
      },
      "Open_Time": "2021-09-03T09:03:19.967+00:00"
    }
  ]
}'
```

## Réponse

Il existe trois réponses de code d'état pour ce paramètre : `200`, `400` et `404`.

### Exemple de réponse au succès

Le `200` de code d'état pourrait renvoyer le corps de réponse suivant.

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
| `arbitrary-error` | Une erreur arbitraire s'est produite. Veuillez réessayer ou contacter [le support]({{site.baseurl}}/support_contact/) technique. |
| `catalog-not-found` | Vérifiez que le nom du catalogue est valide. |
| `filtered-set-field-too-long` | La valeur du champ est utilisée dans un ensemble filtré qui dépasse la limite de caractères pour un élément. |
| `id-in-body` | Un ID d'article existe déjà dans le catalogue. |
| `ids-too-large` | La limite de caractères pour chaque ID d'objet est de 250 caractères. |
| `invalid-ids` | Les caractères pris en charge pour les noms d'ID d'élément sont des lettres, des chiffres, des traits d'union et des soulignements. |
| `invalid-fields` | Confirmez que les champs de la requête existent dans le catalogue. |
| `invalid-keys-in-value-object` | Les touches d'objet d'élément ne peuvent pas inclure de `.` ou de `$`. |
| `item-not-found` | Vérifiez que l'article est dans le catalogue. |
| `item-array-invalid` | `items` doit être un tableau d'objets. |
| `items-too-large` | La limite de caractères pour chaque objet est de 5 000 caractères. |
| `request-includes-too-many-items` | Vous ne pouvez modifier qu'un seul article de catalogue par demande. |
| `too-deep-nesting-in-value-object` | Les objets ne peuvent pas avoir plus de 50 niveaux d'imbrication. |
| `unable-to-coerce-value` | Les types d'articles ne peuvent pas être convertis. |
{: .reset-td-br-1 .reset-td-br-2}

{% endapi %}