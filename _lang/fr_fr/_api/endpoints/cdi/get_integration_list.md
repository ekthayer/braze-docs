---
nav_title: "GET : Intégrations de listes"
article_title: "GET : Intégrations de listes"
search_tag: Endpoint
page_order: 1
alias: /api/cdi/get_integration_list/
layout: api_page
page_type: reference
description: "Cet article donne des détails sur le point de terminaison List integrations Braze."

---
{% api %}
# Intégrations de listes
{% apimethod get %}
/cdi/integrations
{% endapimethod %}

> Utilise ce point de terminaison pour renvoyer une liste des intégrations existantes.


{% alert note %}
Pour utiliser ce point de terminaison, tu dois générer une clé API avec l'autorisation `cdi.integration_list`.
{% endalert %}

## Limite du taux

{% multi_lang_include rate_limits.md endpoint='cdi list integrations' %}

## Paramètres de la requête

Chaque appel à ce point d'extrémité renverra 10 éléments. Pour une liste comportant plus de 10 intégrations, utilise l'en-tête `Link` pour récupérer les données sur la page suivante, comme le montre l'exemple de réponse.

| Paramètre | Exigée | Type de données | Description |
|---|---|---|---|
| `cursor` | En option | Chaîne | Détermine la pagination de la liste d'intégration. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Exemple de demande

### Sans curseur

```
curl --location --request GET 'https://rest.iad-03.braze.com/cdi/integrations' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'
```

### Avec le curseur

```
curl --location --request GET 'https://rest.iad-03.braze.com/cdi/integrations?cursor=c2tpcDow' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'
```

## Réponse

### Exemple de réponse positive

Le code de statut `200` pourrait renvoyer le corps de réponse suivant.

{% alert note %}
L'en-tête `Link` n'existe pas si le nombre total d'intégrations est inférieur ou égal à 10. Pour les appels sans curseur, `prev` ne s'affiche pas. Lorsque tu regardes la dernière page d'articles, `next` ne s'affiche pas.
{% endalert %}

```
Link: </cdi/integrations?cursor=c2tpcDow>; rel="prev",</cdi/integrations?cursor=c2tpcDoxMDA=>; rel="next"
```

```json
{
  "results": [
    {
      "integration_id": (string) integration ID,
      "app_group_id": (string) app group ID,
      "integration_name": (string) integration name,
      "integration_type": (string) integration type,
      "integration_status": (string) integration status,
      "contact_emails": (string) contact email(s),
      "last_updated_at": (string) last timestamp that was synced in ISO 8601,
      "warehouse_type": (string) data warehouse type,
      "last_job_start_time": (string) timestamp of the last sync run in ISO 8601,
      "last_job_status": (string) status of the last sync run,
      "next_scheduled_run": (string) timestamp of the next scheduled sync in ISO 8601,
    },
  ],
  "message": "success"
}
```

## Dépannage

Le tableau suivant répertorie les erreurs renvoyées possibles et les étapes de dépannage associées.

| Erreur | Dépannage |
| --- | --- |
| `400 Invalid cursor` | Vérifie que ton site `cursor` est valide. |
{: .reset-td-br-1 .reset-td-br-2}

Pour les codes d'état supplémentaires et les messages d'erreur associés, reporte-toi à la rubrique [Erreurs fatales et réponses]({{site.baseurl}}/api/errors/#fatal-errors).

{% endapi %}
