Ceci est une liste (archivée) des sites sur le DNS Cloudflare au moment de l'annonce de la fuite de trafic CloudBleed HTTPS. Fil de vuln original par Google Project Zero.

Cloudflare a posté une réponse très détaillée, expliquant exactement quelles sont les implications de cette fuite. Il explique en détail leur langage dans les déclarations précédentes, et je recommande fortement de le lire avant de parcourir cette liste pour les domaines : https://blog.cloudflare.com/quantifying-the-impact-of-cloudbleed/

DISCLAIMER:
Cette liste est archivée et n'est plus gérée activement. Il peut contenir des données périmées ou inexactes qui ne seront pas corrigées. Ne créez pas de lien vers ce site à partir de communiqués de presse, il n'est pas destiné aux utilisateurs finaux. Si les gens veulent le trouver, ils peuvent le chercher sur Google.

Cette liste contient tous les domaines qui utilisent le DNS Cloudflare, pas seulement le proxy Cloudflare (le service affecté qui a perdu des données). Il s'agit d'une vaste liste qui comprend tout. Ce n'est pas parce qu'un domaine figure sur la liste que le site est compromis, et les sites qui ne figurent pas sur cette liste peuvent être compromis.

Cloudflare n'a pas fourni de liste officielle des domaines concernés et ne le fera probablement pas pour des raisons de confidentialité. J'ai compilé une liste non officielle ici pour que vous sachiez où chercher les sessions à réinitialiser et les mots de passe à modifier.

Voir les numéros 127 et 87 pour de plus amples renseignements sur les sites susceptibles d'être touchés.

Impact

Between 2016-09-22 - 2017-02-18 session tokens, passwords, private messages, API keys, and other sensitive data were leaked by Cloudflare to random requesters. Data was cached by search engines, and may have been collected by random adversaries over the past few months.

Requests to sites with the HTML rewrite features enabled triggered a pointer math bug. Once the bug was triggered the response would include data from ANY other Cloudflare proxy customer that happened to be in memory at the time. Meaning a request for a page with one of those features could include data from Uber or one of the many other customers that didn't use those features. So the potential impact is every single one of the sites using Cloudflare's proxy services (including HTTP & HTTPS proxy).

"The greatest period of impact was from February 13 and February 18 with around 1 in every 3,300,000 HTTP requests through Cloudflare potentially resulting in memory leakage (that’s about 0.00003% of requests), potential of 100k-200k paged with private data leaked every day" -- source

##Que dois-je faire ?
