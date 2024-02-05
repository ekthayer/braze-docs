---
nav_title: "POST: Trigger Sync"
article_title: "POST: Trigger Sync"
search_tag: Endpoint
page_order: 2
alias: /api/cdi/post_trigger_sync/
layout: api_page
page_type: reference
description: "Cet article décrit les détails du point de terminaison Trigger sync Braze."

---
{% api %}
# Déclencher une synchronisation
{% apimethod post %}
/cdi/integrations/{integration_id}/sync
{% endapimethod %}

> Utilisez ce point de terminaison pour déclencher une synchronisation pour une intégration donnée.

{% alert note %}
Pour utiliser ce point de terminaison, vous devrez générer une clé API avec l'autorisation `cdi.integration_sync`.
{% endalert %}

## Limite tarifaire

{% multi_lang_include rate_limits.md endpoint='cdi job sync' %}

## Paramètres du chemin

| Paramètre | Obligatoire | Type de données | Description |
|---|---|---|---|
| `integration_id` | Obligatoire | String | Integration ID. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Exemple de demande

```
curl --location --request POST 'https://rest.iad-03.braze.com/cdi/integrations/00000000-0000-0000-0000-000000000000/sync' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'
```

## Réponse

### Exemple de réponse au succès

Le `202` de code d'état pourrait renvoyer le corps de réponse suivant:

```json
{
  "message": "success"
}
```

## Dépannage

Le tableau suivant répertorie les erreurs retournées possibles et les étapes de dépannage associées.

| Erreur | Dépannage |
| --- | --- |
| `400 Invalid integration ID` | Vérifiez que votre `integration_id` est valide. |
| `404 Integration not found` | Aucune intégration n'existe pour l'ID d'intégration donné. Assurez-vous que votre ID d'intégration est valide. |
| `429 Another job is in progress` | Une synchronisation fonctionne actuellement pour cette intégration. Réessayez une fois la synchronisation terminée. |
{: .reset-td-br-1 .reset-td-br-2}

Pour les codes d'état supplémentaires et les messages d'erreur associés, veuillez consulter [Erreurs et réponses]({{site.baseurl}}/api/errors/#fatal-errors) fatales.

{% endapi %}
