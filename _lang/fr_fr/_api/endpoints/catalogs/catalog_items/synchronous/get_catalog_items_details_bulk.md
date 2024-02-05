---
nav_title: "GET : Liste des détails des articles de catalogues multiples"
article_title: "GET : Liste des détails des articles de catalogues multiples"
search_tag: Endpoint
page_order: 3

layout: api_page
page_type: reference
description: "Cet article présente les détails du point de terminaison Braze List multiple catalog item details."

---
{% api %}
# Liste les détails de plusieurs articles du catalogue
{% apimethod get %}
/catalogs/{catalog_name}/items
{% endapimethod %}

> Utilise ce point de terminaison pour renvoyer plusieurs éléments de catalogue et leur contenu.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#63a19dd5-10e0-4649-bdf0-097216748bbb {% endapiref %}

## Conditions préalables

Pour utiliser ce point de terminaison, tu auras besoin d'une [clé API]({{site.baseurl}}/api/basics#rest-api-key/) avec l'autorisation `catalogs.get_items`.

## Limite du taux

{% multi_lang_include rate_limits.md endpoint='synchronous catalog item' %}

## Paramètres du chemin

| Paramètre | Exigée | Type de données | Description |
|---|---|---|---|
| `catalog_name` | Exigée | Chaîne | Nom du catalogue. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Paramètres de la requête

Note que chaque appel à ce point d'extrémité renverra 50 éléments. Pour un catalogue de plus de 50 articles, utilise l'en-tête `Link` pour récupérer les données sur la page suivante, comme le montre l'exemple de réponse suivant.

| Paramètre | Exigée | Type de données | Description |
|---|---|---|---|
| `cursor` | En option | Chaîne | Détermine la pagination des articles du catalogue. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Paramètres de la demande

Il n'y a pas de corps de requête pour ce point de terminaison.

## Exemples de demandes

### Sans curseur

```
curl --location --request GET 'https://rest.iad-03.braze.com/catalogs/restaurants/items' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'
```

### Avec le curseur

```
curl --location --request GET 'https://rest.iad-03.braze.com/catalogs/restaurants/items?cursor=c2tpcDow' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'
```

## Réponse

Il y a trois codes de statut pour ce point d'accès : `200`, `400`, et `404`.

### Exemple de réponse positive

Le code de statut `200` pourrait renvoyer l'en-tête et le corps de réponse suivants.

{% alert note %}
L'en-tête `Link` n'existera pas si le catalogue a moins ou égal à 50 articles. Pour les appels sans curseur, `prev` ne s'affiche pas. Lorsque tu regardes la dernière page d'articles, `next` ne s'affiche pas.
{% endalert %}

```
Link: </catalogs/all_restaurants/items?cursor=c2tpcDow>; rel="prev",</catalogs/all_restaurants/items?cursor=c2tpcDoxMDA=>; rel="next"
```

```json
{
  "items": [
    {
      "id": "restaurant1",
      "Name": "Restaurant1",
      "City": "New York",
      "Cuisine": "American",
      "Rating": 5,
      "Loyalty_Program": true,
      "Open_Time": "2022-11-02T09:03:19.967Z"
    },
    {
      "id": "restaurant2",
      "Name": "Restaurant2",
      "City": "New York",
      "Cuisine": "American",
      "Rating": 10,
      "Loyalty_Program": true,
      "Open_Time": "2022-11-02T09:03:19.967Z"
    },
    {
      "id": "restaurant3",
      "Name": "Restaurant3",
      "City": "New York",
      "Cuisine": "American",
      "Rating": 5,
      "Loyalty_Program": false,
      "Open_Time": "2022-11-02T09:03:19.967Z"
    }
  ],
  "message": "success"
}
```

### Exemple de réponse à une erreur

Le code de statut `400` pourrait renvoyer le corps de réponse suivant. Reporte-toi à la rubrique [Dépannage](#troubleshooting) pour plus d'informations sur les erreurs que tu peux rencontrer.

```json
{
  "errors": [
    {
      "id": "invalid-cursor",
      "message": "'cursor' is not valid",
      "parameters": [
        "cursor"
      ],
      "parameter_values": [
        "bad-cursor"
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
| `invalid-cursor` | Vérifie que ton site `cursor` est valide. |
{: .reset-td-br-1 .reset-td-br-2}

{% endapi %}