---
nav_title: "SUPPRIMER : Supprimer un article du catalogue"
article_title: "SUPPRIMER : Supprimer un article du catalogue"
search_tag: Endpoint
page_order: 1

layout: api_page
page_type: reference
description: "Cet article présente des détails sur le point de terminaison Supprimer un élément de catalogue Braze."

---
{% api %}
# Supprimer un article du catalogue
{% apimethod delete %}
/catalogs/{catalog_name}/items/{item_id}
{% endapimethod %}

> Utilise ce point de terminaison pour supprimer un élément de ton catalogue. 

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#0dcce797-1346-472f-9384-082f14541689 {% endapiref %}

## Conditions préalables

Pour utiliser ce point de terminaison, tu auras besoin d'une [clé API]({{site.baseurl}}/api/basics#rest-api-key/) avec l'autorisation `catalogs.delete_item`.

## Limite du taux

{% multi_lang_include rate_limits.md endpoint='synchronous catalog item' %}

## Paramètres du chemin

| Paramètre | Exigée | Type de données | Description |
|---|---|---|---|
| `catalog_name` | Exigée | Chaîne | Nom du catalogue. |
| `item_id` | Exigée | Chaîne | L'identifiant de l'article du catalogue. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Paramètres de la demande

Il n'y a pas de corps de requête pour ce point de terminaison.

## Exemple de demande

```
curl --location --request DELETE 'https://rest.iad-03.braze.com/catalogs/restaurants/items/restaurant1' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'
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

Le tableau suivant répertorie les erreurs renvoyées possibles et les étapes de dépannage associées.

| Erreur | Dépannage |
| --- | --- |
| `arbitrary-error` | Une erreur arbitraire s'est produite. Essaie à nouveau ou contacte l'[assistance]({{site.baseurl}}/support_contact/). |
| `catalog-not-found` | Vérifie que le nom du catalogue est valide. |
| `item-not-found` | Vérifie que l'élément à supprimer existe bien dans ton catalogue. |
{: .reset-td-br-1 .reset-td-br-2}

{% endapi %}