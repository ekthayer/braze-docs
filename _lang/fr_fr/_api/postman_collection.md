---
nav_title: "Demandes de facteur et d'échantillon"
article_title: "Demandes de facteur et d'échantillon"
page_order: 3
description: "Cet article de référence couvre la collection Braze Postman, ce qu'elle est, comment configurer et utiliser la collection, ainsi que comment modifier et envoyer des demandes."
page_type: reference

---

# Facteur et échantillons de demandes

> Braze vous permet de générer des exemples de demandes d'API pour tous nos terminaux via notre collection de facteurs. Cet article de référence couvre la collection Braze Postman, ce qu'elle est, comment configurer et utiliser la collection, ainsi que comment modifier et envoyer des demandes.

## Qu'est-ce que Postman?

Postman est un outil d'édition visuelle gratuit pour construire et tester des requêtes API. Contrairement à d'autres méthodes pour interagir avec les API (par exemple, en utilisant cURL), Postman vous permet de modifier facilement les requêtes d'API, afficher les informations d'en-tête, et bien plus encore. Postman a la possibilité pour vous de sauvegarder des Collections ou des bibliothèques d'exemples de demandes d'API pré-faites. Pour permettre à nos clients d'être facilement opérationnels avec notre API REST, nous avons créé une Collection avec des exemples pré-établis pour tous nos terminaux API.

Consultez ou téléchargez notre collection de facteurs en cliquant sur **Run in Postman** dans nos [docs Postman](https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#intro) pour commencer.

## Utiliser la collection Braze Postman

Si vous avez un compte Postman (vous pouvez télécharger les versions macOS, Windows et Linux sur le [site Postman][1]), vous pouvez ouvrir notre documentation Postman dans votre propre application Postman en cliquant sur le bouton orange **Exécuter dans Postman**. Vous pouvez alors [créer un environnement](#setting-up-your-postman-environment), ou utiliser notre environnement Braze REST API comme modèle, et modifier les demandes de `POST` et de `GET` disponibles en fonction de vos propres besoins.

### Configuration de votre environnement Postman

{% raw %}
La collection Braze Postman utilise une variable de modélisation, `{{instance_url}}`, pour substituer l'URL REST API de votre instance Braze dans les requêtes précompilées, et la variable `{{api_key}}` pour votre clé API. Plutôt que d'avoir à modifier manuellement toutes les requêtes de la Collection, vous pouvez configurer cette variable dans votre environnement Postman. Vous pouvez soit sélectionner notre environnement template (Braze REST API Environment Template) dans la liste déroulante et remplacer les valeurs des variables par les vôtres, soit configurer votre propre environnement.
{% endraw %}

Pour configurer votre propre environnement, effectuez les étapes suivantes :

1. Dans l’onglet **Espaces de travail**, sélectionnez **Environnements**.
2. Cliquez sur le bouton **+** plus pour créer un nouvel environnement.
3. Donnez un nom à cet environnement (par exemple, « Demandes d'API Braze ») et ajoutez des clés pour les `instance_url` et `api_key` avec des valeurs correspondant à votre [instance Braze][7] et [clé d'API BRaze REST][8].
4. Cliquez sur **Enregistrer**.

{% alert note %}
Dans les organismes de demande de `POST`, les `api_key` doivent être encapsulés entre guillemets: `"MY-API-KEY-EXAMPLE"`. Dans les URL `GET`, il ne devrait pas l'être. Nous avons déjà fourni cette mise en forme pour vous dans les corps de demande de `POST` de cette documentation, les URL de `GET` et le modèle d'environnement pour les `YOUR-API-KEY-HERE`.
{% endalert %}

![Ajout de variables pour la clé d'API et l'URL d'instance à l'environnement d'API Braze REST dans Postman.][3]

### Utiliser les requêtes pré-construites de la collection

Une fois que vous avez configuré votre environnement. Vous pouvez utiliser n'importe laquelle des requêtes précompilées dans la collection comme modèle pour construire de nouvelles requêtes d'API. Pour commencer à utiliser une des requêtes pré-compilées, cliquez dessus dans le menu **Collections** de Postman. Cela ouvrira la demande comme un nouvel onglet dans la fenêtre principale de l'application Postman.

En général, il existe deux types de requêtes que les terminaux Braze API acceptent - `GET` et `POST`. Selon la méthode de `HTTP` utilisée par le terminal, vous devrez modifier la requête précompilée différemment.

#### Modifier une demande POST

Lorsque vous modifiez une demande de `POST`, ouvrez la demande et accédez à la section **Corps** dans l'éditeur de demande. Pour plus de lisibilité, sélectionnez le bouton radio **brut** pour formater le corps de la demande de `JSON`.

![Onglet Corps lors de l'édition d'une requête POST User Track dans Postman][4]

#### Modifier une requête GET

Lors de l'édition d'une requête `GET`, modifiez les paramètres passés dans l'URL de la requête. Pour ce faire, sélectionnez l'onglet **Paramètres** et modifiez les paires clé-valeur dans les champs qui apparaissent.

![Onglet Paramètres lors de l'édition d'une requête GET Liste des adresses e-mail non abonnées dans Postman.][5]

### Envoyez votre demande

Une fois votre demande d'API prête, cliquez **sur Envoyer**. La requête envoie et les données de réponse se remplissent dans une section sous l'éditeur de requête. À partir de là, vous pouvez afficher les données brutes renvoyées depuis l'API Braze, voir le code de réponse HTTP, voir le temps de traitement de la requête et afficher les informations d'en-tête.

![Exemple de données de réponse du corps d'une requête POST avec un statut de 201 Créé et un temps de réponse de 269 millisecondes.][6]

[1]: https://www.getpostman.com
[3]: {% image_buster /assets/img_archive/postman_variable.png %}
[4]: {% image_buster /assets/img_archive/postman_post.png %}
[5]: {% image_buster /assets/img_archive/postman_get.png %}
[6]: {% image_buster /assets/img_archive/postman_response.png %}
[7]: {{site.baseurl}}/developer_guide/rest_api/basics/#endpoints
[8]: {{site.baseurl}}/api/api_key/
