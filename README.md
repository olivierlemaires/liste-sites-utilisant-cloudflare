# Liste des sites sur Cloudflare DNS (archivé)

Ceci est une liste (archivée) des sites sur le DNS Cloudflare au moment de l'annonce de la fuite de trafic CloudBleed HTTPS. Fil de vuln original par Google Project Zero.

Cloudflare a posté une réponse très détaillée, expliquant exactement quelles sont les implications de cette fuite. Il explique en détail leur langage dans les déclarations précédentes, et je recommande fortement de le lire avant de parcourir cette liste pour les domaines : https://blog.cloudflare.com/quantifying-the-impact-of-cloudbleed/

## DISCLAIMER:
Cette liste est archivée et n'est plus gérée activement. Il peut contenir des données périmées ou inexactes qui ne seront pas corrigées. Ne créez pas de lien vers ce site à partir de communiqués de presse, il n'est pas destiné aux utilisateurs finaux. Si les gens veulent le trouver, ils peuvent le chercher sur Google.

Cette liste contient tous les domaines qui utilisent le DNS Cloudflare, pas seulement le proxy Cloudflare (le service affecté qui a perdu des données). Il s'agit d'une vaste liste qui comprend tout. Ce n'est pas parce qu'un domaine figure sur la liste que le site est compromis, et les sites qui ne figurent pas sur cette liste peuvent être compromis.

Cloudflare n'a pas fourni de liste officielle des domaines concernés et ne le fera probablement pas pour des raisons de confidentialité. J'ai compilé une liste non officielle ici pour que vous sachiez où chercher les sessions à réinitialiser et les mots de passe à modifier.

Voir les numéros 127 et 87 pour de plus amples renseignements sur les sites susceptibles d'être touchés.

## Impact

Between 2016-09-22 - 2017-02-18 session tokens, passwords, private messages, API keys, and other sensitive data were leaked by Cloudflare to random requesters. Data was cached by search engines, and may have been collected by random adversaries over the past few months.

Requests to sites with the HTML rewrite features enabled triggered a pointer math bug. Once the bug was triggered the response would include data from ANY other Cloudflare proxy customer that happened to be in memory at the time. Meaning a request for a page with one of those features could include data from Uber or one of the many other customers that didn't use those features. So the potential impact is every single one of the sites using Cloudflare's proxy services (including HTTP & HTTPS proxy).

"The greatest period of impact was from February 13 and February 18 with around 1 in every 3,300,000 HTTP requests through Cloudflare potentially resulting in memory leakage (that’s about 0.00003% of requests), potential of 100k-200k paged with private data leaked every day" -- source

## Que dois-je faire ?

La chose la plus importante que vous puissiez faire est de demander à vos fournisseurs et sites de réinitialiser tous leurs jetons de session, car plus de données de réponse ont été divulguées que de données de demande, et les réponses contiennent généralement des jetons de session plutôt que des mots de passe. Si les sites Web que vous utilisez disposent d'un bouton pour "déconnecter toutes les sessions actives", utilisez-le. Comme les sites peuvent être compromis cette semaine en raison de données découvertes dans les caches, il est préférable de le refaire dans une semaine ou deux, une fois que tout sera réglé. Si les sites Web que vous utilisez n'ont pas la possibilité de se déconnecter de toutes les sessions actives, contactez-les et poussez-les à faire pivoter tous leurs jetons de session.

Pour plus de sécurité, vous voudrez peut-être vérifier vos gestionnaires de mots de passe et modifier les mots de passe essentiels, en particulier ceux de ces sites concernés. Faites pivoter les clés et secrets de l'API et confirmez que vous avez configuré la fonction 2-FA pour les comptes importants. Cela peut sembler un peu alarmiste, mais l'ampleur de cette fuite est vraiment énorme, et du fait que tous les clients proxy de Cloudflare étaient vulnérables aux fuites de données, beaucoup de personnes très prudentes préfèrent être en sécurité que d'être désolées.

Théoriquement, les sites qui ne figurent pas dans cette liste peuvent également être affectés (parce qu'un site affecté aurait pu faire une requête API à un site non affecté).

## Methodology

Cette liste a été compilée à partir de 3 grandes décharges de tous les clients Cloudflare fournies par crimeflare.com/cfs.html, et plusieurs listes copiées-collées manuellement à partir de stackshare.io et wappalyzer.com. Crimeflare a collecté leurs listes en effectuant des recherches DNS NS sur un grand nombre de domaines et en vérifiant la propriété des certificats SSL.

J'ai gratté le top 10 000 Alexa en utilisant une simple boucle sur la liste :


for domain in (cat ~/Desktop/alexa_10000.csv)
    if dig $domain NS | grep cloudflare
        echo $domain >> affected.txt
    end
end

La raclée Alexa et les décharges de Crimeflare ont ensuite été regroupées dans un seul fichier texte, et sont passées par sort | uniq. Depuis, j'ai accepté plusieurs RP et problèmes pour retirer de la liste les sites qui n'ont pas été touchés.

## Data sources:

https://stackshare.io/cloudflare
https://wappalyzer.com/applications/cloudflare
DNS scraper I'm running on Alexa top 10,000 sites (grepping for cloudflare in results)
https://www.cloudflare.com/ips/ (going to find sites that resolve to these IPs next)
http://www.crimeflare.com/cfs.html (scrape of all Cloudflare customers)
http://www.doesitusecloudflare.com/



Je préfère être en sécurité plutôt que désolé donc j'ai inclus ici tout domaine qui touche à distance Cloudflare. Ne dirigez pas les utilisateurs finaux vers cette liste s'il vous plaît, elle a trop de faux positifs pour être utile à des fins non-analytiques. Je n'accepte plus les RP pour retirer des sites de la liste, notre processus précédent de retrait de sites était sujet à des erreurs et demandait beaucoup de travail. La liste est maintenant en mode archive, considérez-la défunte. Si vous pensez que pour une raison ou une autre, cela aura un impact important sur vous ou vos utilisateurs, DM me sur Twitter.


## Outils de recherche

Il existe plusieurs outils pour faire des recherches dans la liste, je n'en approuverai aucun ici parce qu'ils ont des degrés d'exactitude très variables.  Veuillez ne pas utiliser d'outils de recherche ou de références croisées avec l'historique du navigateur, car cette liste contient trop de faux positifs pour être utilisée à cette fin.  Vous ferez perdre la confiance des utilisateurs dans de nombreux sites, bien qu'il y ait moins d'une chance sur un million qu'ils aient des fuites de données. 

## Notable Sites

authy.com (no leaked data found in several search engine caches)
coinbase.com
bitcoin.de
betterment.com
prosper.com
patreon.com
bitpay.com
news.ycombinator.com
producthunt.com
medium.com
4chan.org
yelp.com
okcupid.com
zendesk.com (Zendesk post and updates | no leaked data found)
uber.com
poloniex.com
localbitcoins.com
kraken.com
23andme.com
curse.com (and some other Curse sites like minecraftforum.net)
counsyl.com
tfl.gov.uk
brand-for-influencer.com
myaccount.nytimes.com
technicpack.net
cloudflare.com
blockchain.info
discordapp.com (affected)
digitalocean.com (no leaked data found in several search engine caches)
namecheap.com (no leaked data found in several search engine caches)
glassdoor.com (no leaked data found in several search engine caches)
transferwise.com (no leaked data found in several search engine caches
vultr.com (no leaked data found in several search engine caches)
fastmail.com (not affected, #2)
1password.com (not affected)
