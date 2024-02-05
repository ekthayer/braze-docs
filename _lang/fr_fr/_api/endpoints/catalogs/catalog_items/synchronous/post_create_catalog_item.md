---
nav_title: "POST : Créer un article de catalogue"
article_title: "POST : Créer un article de catalogue"
search_tag: Endpoint
page_order: 5

layout: api_page
page_type: reference
description: "Cet article présente les détails du point de terminaison Créer un élément de catalogue Braze."

---
{% api %}
# Créer un article de catalogue
{% apimethod post %}
/catalogs/{catalog_name}/items/{item_id}
{% endapimethod %}

> Utilise ce point de terminaison pour créer un article dans ton catalogue.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#820c305b-ea6a-4b71-811a-55003a212a40 {% endapiref %}

## Conditions préalables

Pour utiliser ce point de terminaison, tu auras besoin d'une [clé API]({{site.baseurl}}/api/basics#rest-api-key/) avec l'autorisation `catalogs.create_item`.

## Limite du taux

{% multi_lang_include rate_limits.md endpoint='synchronous catalog item' %}

## Paramètres du chemin

| Paramètre | Exigée | Type de données | Description |
|---|---|---|---|
| `catalog_name` | Exigée | Chaîne | Nom du catalogue. |
| `item_id` | Exigée | Chaîne | L'identifiant de l'article du catalogue. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Paramètres de la demande

| Paramètre | Exigée | Type de données | Description |
|---|---|---|---|
| `items` | Exigée | Array | Un tableau qui contient des objets d'articles. Les objets de l'article doivent contenir tous les champs du catalogue à l'exception du champ `id`. Un seul objet d'article est autorisé par demande. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Exemple de demande

```
curl --location --request POST 'https://rest.iad-03.braze.com/catalogs/restaurants/items/restaurant1' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY' \
--data-raw '{
  "items": [
    {
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
    }
  ]
}'
```

## Réponse

Il y a trois codes de statut pour ce point d'accès : `201`, `400`, et `404`.

### Exemple de réponse positive

Le code de statut `201` pourrait renvoyer le corps de réponse suivant.

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
| `arbitrary-error` | Une erreur arbitraire s'est produite. Essaie à nouveau ou contacte l'[assistance]({{site.baseurl}}/support_contact/). |
| `catalog-not-found` | Vérifie que le nom du catalogue est valide. |
| `filtered-set-field-too-long` | La valeur du champ est utilisée dans un ensemble filtré qui dépasse la limite de caractères pour un article. |
| `id-in-body` | Supprime tous les identifiants d'articles dans le corps de la demande. |
| `ids-too-large` | La limite de caractères pour chaque identifiant d'article est de 250 caractères. |
| `invalid-ids` | Les caractères pris en charge pour les noms d'identification des articles sont les lettres, les chiffres, les traits d'union et les traits de soulignement. |
| `invalid-fields` | Confirme que tous les champs que tu envoies dans la requête API existent déjà dans le catalogue. Cela n'a rien à voir avec le champ d'identification mentionné dans l'erreur. |
| `invalid-keys-in-value-object` | Les clés d'objet de l'article ne peuvent pas inclure `.` ou `$`. |
| `item-already-exists` | L'article existe déjà dans le catalogue. |
| `item-array-invalid` | `items` doit être un tableau d'objets. | 
| `items-too-large` | La limite de caractères pour chaque article est de 5 000 caractères. |
| `request-includes-too-many-items` | Tu ne peux créer qu'un seul article de catalogue par demande. |
| `too-deep-nesting-in-value-object` | Les objets ne peuvent pas avoir plus de 50 niveaux d'imbrication. |
| `unable-to-coerce-value` | Les types d'articles ne peuvent pas être convertis. |
{: .reset-td-br-1 .reset-td-br-2}

{% endapi %}