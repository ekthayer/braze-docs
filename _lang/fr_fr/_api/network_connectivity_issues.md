---
nav_title: Problèmes de connectivité réseau de l’API
article_title: Problèmes de connectivité réseau de l’API
page_order: 4
description: "Cet article de référence aborde les problèmes de connectivité des API et la façon de les résoudre." 
page_type: reference

---

# Problèmes de connectivité réseau de l’API

> Cet article de référence aborde les problèmes de connectivité des API et la façon de les résoudre. 

Les points de terminaison de l’API Braze utilisent un CDN qui achemine le trafic vers le POP le plus proche en fonction des informations DNS.  Si vous rencontrez des problèmes de connexion ou si vous remarquez que vous vous connectez à un POP qui n’est pas efficace, assurez-vous d’utiliser les serveurs DNS de votre fournisseur ou les serveurs DNS qui sont configurés dans le même centre de données que votre serveur et qui sont associés à des métadonnées de localisation IP appropriées.

Nous avons remarqué qu’une poignée de pare-feu tentent de modifier ou de sécuriser HTTPS/TLS traffic which interferes with connections to Braze API endpoints. If your servers are behind any sort of physical firewall, disable any HTTPS/TLS acceleration or modifications that the firewall or router is performing. Additionally, you can allowlist outbound traffic to our CDN providers (Fastly.com) to see if that resolves the issue.

De temps en temps, iptables qui filtrent sur SYN/ACK/RST packets can also cause issues, so if you are using iptables on your host you could also allowlist outbound traffic to our CDN providers (Fastly.com) to see if that resolves the issue.

Si vous rencontrez toujours des problèmes de réseau lors de la connexion aux points de terminaison de l’API Braze, fournissez un test][1] MTR et les résultats de Fastly Debug lorsque vous rencontrez un [problème et soumettez-le avec votre demande d’assistance [.][2]  Notez que les résultats des tests doivent être obtenus à partir d’un serveur qui rencontre des problèmes de connexion aux points de terminaison de l’API Braze, et non à partir d’une machine de développement. Une capture réseau (fichier tcpdump ou .pcap) sera également utile si elle peut être obtenue.

Pour plus d’informations sur MTR, consultez ces ressources en fonction de votre système d’exploitation :

- [GNU/Linux][4]
- [macOS][5]

## Liste d’autorisation des plages d’adresses IP des points de terminaison de l’API Braze

Pour ajouter des points de terminaison d’API Braze à la liste d’autorisation via votre pare-feu, notre CDN permet d’accéder à la liste des plages d’adresses IP attribuées via un vidage JSON. Pour obtenir la liste des plages d’adresses IP Fastly.com, reportez-vous à leur [liste][3]d’adresses IP publiques.

[1]: https://www.privateinternetaccess.com/helpdesk/kb/articles/what-is-an-mtr-test-and-how-do-i-run-one-2
[2]: http://www.fastly-debug.com/
[3]: https://api.fastly.com/public-ip-list
[4]: https://www.digitalocean.com/community/tutorials/how-to-use-traceroute-and-mtr-to-diagnose-network-issues
[5]: https://formulae.brew.sh/formula/mtr
