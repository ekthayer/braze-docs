---
nav_title: Données utilisateur
article_title: Données utilisateur Endpoints
search_tag: Endpoint
page_order: 9

local_redirect: #event-object-specification #purchase-object-specification
  event-object-specification: '/docs/api/objects_filters/event_object/'
  purchase-object-specification: '/docs/api/objects_filters/purchase_object/'

layout: dev_guide

#Required
description: "Cette page de destination répertorie les points de terminaison des données utilisateur Braze."
page_type: landing

guide_top_header: "Données utilisateur Endpoints"
guide_top_text: "Les terminaux Braze User Data vous permettent de suivre les informations relatives à vos utilisateurs en enregistrant les données relatives à vos utilisateurs qui proviennent de l'extérieur de votre application mobile. Vous pouvez également utiliser cette API pour supprimer des utilisateurs à des fins de test ou autres. <br> <br> Tous les terminaux API ont une limite de charge utile de données de 4 MB. Les tentatives d'afficher plus de données que 4 MB échoueront avec une entité de requête HTTP 413 Too Large. <br> <br> Les exemples de cette section contiennent l'URL https://rest.iad-01.braze.com, mais vous devrez peut-être utiliser une URL de point final différente (par exemple, si vous êtes hébergé dans le centre de données Braze EU ou si vous avez une installation Braze dédiée). Votre gestionnaire de succès client Braze vous informera si vous devez utiliser une URL de point final différente."

guide_featured_title: "Données utilisateur Endpoints"
guide_featured_list:
  - name: "POST: Create a New User Alias"
    link: /docs/api/endpoints/user_data/post_user_alias/
    fa_icon: fas fa-user
  - name: "POST: Update a User Alias"
    link: /docs/api/endpoints/user_data/post_users_alias_update/
    fa_icon: fas fa-user-edit
  - name: "POST: Delete User Data"
    link: /docs/api/endpoints/user_data/post_user_delete/
    fa_icon: fas fa-user-minus
  - name: "POST: Identify a User"
    link: /docs/api/endpoints/user_data/post_user_identify/
    fa_icon: fas fa-user-circle
  - name: "POST: Track Users"
    link: /docs/api/endpoints/user_data/post_user_track/
    fa_icon: fas fa-database
  - name: "POST: Merge Users"
    link: /docs/api/endpoints/user_data/post_users_merge/
    fa_icon: fas fa-users

guide_menu_title: "External ID migration endpoints"
guide_menu_list:
  - name: "POST: Rename External IDs"
    link: /docs/api/endpoints/user_data/external_id_migration/post_external_ids_rename/
    fa_icon: fas fa-user
  - name: "POST: Remove Deprecated External IDs"
    link: /docs/api/endpoints/user_data/external_id_migration/post_external_ids_remove/
    fa_icon: fas fa-user-minus
---
