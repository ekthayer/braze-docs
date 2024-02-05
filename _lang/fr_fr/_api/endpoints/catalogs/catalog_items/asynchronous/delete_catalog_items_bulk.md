---
nav_title: "SUPPRIMER: Supprimer plusieurs éléments de catalogue"
article_title: "SUPPRIMER: Supprimer plusieurs éléments de catalogue"
search_tag: Endpoint
page_order: 1

layout: api_page
page_type: reference
description: "Cet article décrit les détails du point de terminaison Braze Supprimer plusieurs éléments de catalogue."

---
{% api %}
# Supprimer plusieurs éléments de catalogue
{% apimethod delete %}
/catalogs/{catalog_name}/items
{% endapimethod %}

> Utilisez ce point de terminaison pour supprimer plusieurs éléments de votre catalogue. 

Chaque demande peut prendre en charge jusqu’à 50 éléments. Ce point de terminaison est asynchrone.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#647c82e8-8b38-4df2-bde2-b1d8e19fd332 {% endapiref %}

## Conditions préalables

Pour utiliser ce point de terminaison, vous aurez besoin d’une [clé]({{site.baseurl}}/api/basics#rest-api-key/) API avec l’autorisation `catalogs.delete_items` .

## Limite de débit

{% multi_lang_include rate_limits.md endpoint='asynchronous catalog item' %}

## Paramètres de chemin

| Paramètre | Obligatoire | Type de données | Description |
|---|---|---|---|
| `catalog_name` | Obligatoire | Corde | Nom du catalogue. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Paramètres de la requête

| Paramètre | Obligatoire | Type de données | Description |
|---|---|---|---|
| `items` | Obligatoire | Tableau | Tableau contenant des objets item. Les objets item doivent contenir une `id` référence aux éléments que Braze doit supprimer. Jusqu’à 50 objets d’article sont autorisés par demande. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Exemple de demande

```
curl --location --request DELETE 'https://rest.iad-03.braze.com/catalogs/restaurants/items' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY' \
--data-raw '{
  "items": [
    {"id": "restaurant1"},
    {"id": "restaurant2"},
    {"id": "restaurant3"}
  ]
}'
```

## Réponse

Il existe trois réponses de code d’état pour ce point de terminaison : `202`, `400`, et `404`.

### Exemple de réponse de réussite

Le code `202` d’état peut renvoyer le corps de la réponse suivant.

```json
{
  "message": "success"
}
```

### Exemple de réponse d’erreur

Le code `400` d’état peut renvoyer le corps de la réponse suivant. Reportez-vous à [la section Dépannage](#troubleshooting) pour plus d’informations sur les erreurs que vous pouvez rencontrer.

```json
{
  "errors": [
    {
      "id": "items-missing-ids",
      "message": "There are 1 item(s) that do not have ids",
      "parameters": [],
      "parameter_values": []
    }
  ],
  "message": "Invalid Request",
}
```

## Dépannage

Le tableau suivant répertorie les erreurs renvoyées possibles et les étapes de dépannage associées.

| Erreur | Dépannage |
| --- | --- |
| `catalog-not-found` | Vérifiez que le nom du catalogue est valide. |
| `ids-too-large` | Les ID d’élément ne peuvent pas comporter plus de 250 caractères. |
| `ids-not-unique` | Vérifiez que les ID d’élément sont uniques dans la demande. |
| `ids-not-strings` | Les ID d’élément doivent être de type chaîne. |
| `items-missing-ids` | Certains éléments n’ont pas d’ID d’élément. Vérifiez que chaque élément dispose d’un ID d’article. |
| `invalid-ids` | Les ID d’élément ne peuvent inclure que des lettres, des chiffres, des traits d’union et des traits de soulignement. |
| `request-includes-too-many-items` | Votre demande comporte trop d’éléments. La limite d’éléments par demande est de 50. |
{: .reset-td-br-1 .reset-td-br-2}

{% endapi %}