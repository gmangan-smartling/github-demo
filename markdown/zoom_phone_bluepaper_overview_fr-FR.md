Présentation
============

Zoom Phone est le service de téléphonie basé sur le cloud de Zoom, conçu pour répondre aux besoins de téléphonie des entreprises de toute taille. Doté d'un menu d'administration intuitif basé sur le web pour les paramètres et les politiques, et d'une architecture de service basée sur le cloud qui remplace l'ancien équipement sur site, Zoom Phone simplifie la téléphonie.

Cette section fournit une vue d'ensemble des services, de l'architecture, de la conception, des exigences du réseau, des normes de sécurité, des appareils pris en charge, des fonctionnalités, des licences, etc. de Zoom Phone. Après avoir lu cette section, vous pouvez vous attendre à acquérir une compréhension de haut niveau des éléments de conception et des fonctionnalités fondamentales de Zoom Phone.

#### <mark style="color:blue;">Zoom Phone propose trois offres de services principales : Native, BYOC Cloud Peering et BYOC Premises Peering.</mark>

Zoom Phone propose aux entreprises trois offres de services principales pour répondre aux divers besoins à travers le monde : **Zoom Phone Native** , **Zoom Phone Bring Your Own Carrier with Cloud Peering (BYOC-C)** , et **Zoom Phone Bring Your Own Carrier with Premises Peering (BYOC-P)** . Chacun de ces services est brièvement décrit dans les sections suivantes, un résumé du réseau étant disponible à la fin de la description de chaque service.

{% content-ref url="zoom-phone-native.md" %}
[zoom-phone-native.md](zoom-phone-native.md)
{% endcontent-ref %}

{% content-ref url="bring-your-own-carrier-cloud-peering-byoc-c.md" %}
[bring-your-own-carrier-cloud-peering-byoc-c.md](bring-your-own-carrier-cloud-peering-byoc-c.md)
{% endcontent-ref %}

{% content-ref url="bring-your-own-carrier-premises-peering-byoc-p.md" %}
[bring-your-own-carrier-premises-peering-byoc-p.md](bring-your-own-carrier-premises-peering-byoc-p.md)
{% endcontent-ref %}

#### <mark style="color:blue;">Zoom Phone est conçu avec une architecture active-active pour la fiabilité et la résilience.</mark>

Zoom Phone utilise une architecture active-active de premier ordre pour fournir un service téléphonique fiable et de qualité professionnelle. Les détails de cette conception sont développés dans les sections suivantes, en mettant l'accent sur les zones SIP spécifiques aux centres de données et sur les centres de données de Zoom dans leur ensemble.

### Zoom Phone Data Center Zones SIP

Dans une architecture active-active, la résilience et la redondance sont essentielles. Chaque centre de données Zoom Phone dispose de deux zones SIP identiques, interconnectées et équipées de matériel et de services dédiés pour une résilience et une durabilité indépendantes.

Pendant les opérations normales, un équilibreur de charge distribue uniformément les appels entre les deux zones SIP au sein d'un centre de données. Au sein de chaque zone SIP, les appels sont répartis équitablement entre une grappe de commutateurs d'appels, qui sont responsables de diverses fonctions telles que l'acheminement des appels, l'établissement et le démontage. À partir des commutateurs d'appel, les appels se connectent à un contrôleur frontal de session (SBC) dans chaque zone, qui se connecte au réseau sous-jacent de fournisseurs de Zoom pour le routage RTPC jusqu'à ce que l'appel atteigne sa destination finale.

Dans ce cadre, chaque élément intégral de l'architecture - c'est-à-dire les SBC, les équilibreurs de charge et les commutateurs d'appel - est complété par du matériel redondant en attente pour assurer la résilience. Dans le cas où une zone SIP connaîtrait un événement ayant un impact sur le service, les médias actifs, la signalisation et l'enregistrement d'un appel basculeraient vers l'autre zone pour un service ininterrompu.

Le diagramme suivant illustre la conception de l'architecture active-active d'une zone SIP à un niveau élevé :
<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXcaXOw7Bu4ZXR75kgEYWSh6IBU4P_G6DOUGuE8OQ1zvgGln0to_91pq8BY9N-2cmzn24uMorcOayjSp2Y_g9_zpCjHBKHWbja2Qh988ncL6TUs8zHh1ZkANbXk3Mr5wB8uZr1zDkhIucgemMtCxngk?key=gORaE6vjeZ6i7Y4PGyLKfw" alt="" width="563"><figcaption><p>Diagramme de l'architecture active-active d'une zone SIP.</p></figcaption></figure> 

### Zoom Phone Data Centers At Large

D'un point de vue physique, les centres de données de Zoom sont situés dans des installations de colocation hautement sécurisées, avec une sécurité physique, des systèmes d'alimentation et de refroidissement redondants, et un accès aux principaux fournisseurs de services Internet neutres et aux partenaires d'échange de trafic (peering).

D'un point de vue technologique, les centres de données de Zoom sont construits avec une architecture tolérante aux pannes, comprenant une redondance complète et des capacités de basculement rapide d'un centre de données principal vers un centre de données secondaire, afin d'améliorer la fiabilité et de minimiser les temps d'arrêt.

Dans le cas improbable d'une panne complète du centre de données ou d'un événement affectant le service, les médias, la signalisation et les informations d'enregistrement de Zoom Phone peuvent être temporairement perdus, ce qui nécessite une convergence sur le centre de données secondaire de secours.

Le diagramme suivant illustre la conception de la redondance du centre de données de Zoom à un niveau élevé :
<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXfRZ-QerC-_7-wr6qOfb5lHUQ9x9bFHPozJutStPSc9ykAroO56EAaipWz2KpDSEHXR9TIinValkP20Rz07ffEUYZTLUF6v09x48u7Jo8DD8xgrIvS_1S1_oimOP_EiSkl7mL7cLxjDCqaPoo-2LQ?key=gORaE6vjeZ6i7Y4PGyLKfw" alt="" width="563"><figcaption><p>Diagramme de la redondance du centre de données de Zoom.</p></figcaption></figure> 

### Emplacement des services de la zone SIP

Zoom Phone offre une connectivité RTC où Zoom fournit des services de téléphonie natifs. De plus, les clients hébergés sur le cluster de Zoom basé aux États-Unis (US01) peuvent bénéficier de la connectivité SIP Zone à travers l'infrastructure média mondiale de Zoom, qui comprend les centres de données suivants afin d'optimiser la qualité des appels et le routage en fonction de l'emplacement de l'utilisateur :

{% columns %}
{% column %}
**Amérique du Nord :** 

* Ouest des États-Unis, Californie
* Centre des États-Unis, Colorado
* États-Unis d'Amérique, New York
* Est des États-Unis, Virginie

**Amérique latine :** 

* Brésil, São Paulo
* Mexique, Querétaro {% endcolumn %}

{% column %}
**EMEA :** 

* Pays-Bas, Amsterdam
* Allemagne, Francfort
* Arabie saoudite, Riyad
* Arabie Saoudite, Jeddah

**APAC :** 

* Australie, Sydney
* Australie, Melbourne
* Chine, Hong Kong
* Japon, Tokyo
* Japon, Osaka
* Singapour, Singapour {% endcolumn %} {% endcolumns %}

#### <mark style="color:blue;">Connectivité régionale</mark>

Pour les clients qui ont besoin de la localisation des données pour des raisons de conformité et qui sont situés dans les régions supportées, Zoom Phone supporte également la connectivité RTC localisée pour les comptes spécifiques à la région. Les clients disposant d'un compte spécifique à une région sont obligés d'initialiser tous les appels à partir du centre de données associé à leur région et ne peuvent pas utiliser les zones SIP en dehors de la région de leur compte.

La liste suivante détaille les régions prises en charge et les emplacements des centres de données spécifiques aux régions disponibles avec Zoom Phone :

{% columns %}
{% column %}
**Australie** 

* Sydney
* Melbourne

**Canada** 

* Vancouver
* Toronto {% endcolumn %}

{% column %}
**L'Europe** 

* Allemagne
* Amsterdam

**Zoom pour le gouvernement** 

* Californie
* New York {% endcolumn %} {% endcolumns %}

{% hint style="warning" %}
**Avertissement** 

Les appels téléphoniques passés à partir de comptes spécifiques à une région seront transmis à partir de centres de données situés dans la région ; toutefois, les appels RTPC peuvent traverser des réseaux internationaux au-delà de la région dans laquelle ils sont passés.
{% endhint %}

### Zoom Phone India

Outre les régions localisées, Zoom Phone prend également en charge la connectivité BYOC-P (Bring Your Own Carrier with Premises Peering) à l'intérieur de l'Inde grâce à une offre de services Zoom Phone India spécialisée. Avec Zoom Phone India, les clients ayant un compte basé sur un cluster américain reçoivent une instance unique de Zoom Phone spécifique aux zones de service autorisées - également connues sous le nom de cercles - où Zoom et le compte du client sont autorisés à opérer.

A la date de publication de ce document, Zoom est autorisé à opérer dans les zones de service sous licence suivantes :

* **Mumbai :** zone locale de Mumbai, Navi Mumbai et Kalyan.
* **Andhra Pradesh :** État de l'Andhra Pradesh et du Telangana, y compris Hyderabad
* **Maharashtra :** État de Maharashtra et Goa, y compris Pune
* **Karnataka :** État du Karnataka, y compris Bangalore
* **Tamil Nadu :** État du Tamil Nadu et territoire de l'union de Pondichéry, y compris Chennai
* **Delhi :** zone locale de Delhi, New Delhi, Ghaziabad, Faridabad, Noida et Gurgaon.

#### <mark style="color:blue;">Conditions requises pour Zoom Phone India</mark>

En raison des exigences réglementaires, une entreprise doit répondre à certains critères pour être éligible au service Zoom Phone India. Bien que la liste suivante ne soit pas exhaustive, les critères les plus importants sont décrits ci-dessous :

* L'entreprise **doit** payer avec la roupie indienne et ne peut pas utiliser une autre dénomination comme le dollar américain ou l'euro.
* L'entreprise **doit être** une entité commerciale enregistrée auprès du gouvernement indien et ne peut être une entité internationale.
* L'entreprise **doit** disposer d'un signataire autorisé et d'un numéro d'identification de la taxe sur les produits et les ventes (GSTIN) dans l'État où elle fournit ses services.
* L'entreprise **doit être** située dans l'une des zones de service autorisées actuellement soutenues par Zoom.

Si votre entreprise répond à ces critères et souhaite en savoir plus sur Zoom Phone India, contactez votre équipe pour plus d'informations.

### Normes de sécurité

Zoom Phone prend en charge les appels vocaux sécurisés sur différentes plateformes, y compris l'application Zoom Workplace pour les ordinateurs de bureau et les téléphones portables, le client web Zoom, Zoom Rooms et les appareils SIP pris en charge.

Lors de l'établissement de l'appel, le téléphone Zoom utilise SIP sur TLS 1\.2 avec un algorithme AES 256 bits pour le cryptage. En outre, les connexions à partir de l'application Zoom Workplace pour les ordinateurs de bureau et les téléphones portables, ainsi que le client Web Zoom, cryptent les médias d'appel vers Zoom Cloud en utilisant le protocole de transport sécurisé en temps réel (SRTP) avec un cryptage AES 256 bits.

Les appareils SIP compatibles configurés avec SRTP utilisent les algorithmes AES-128 ou AES-256 bits pour crypter les supports d'appel, tandis que le RTP non crypté est utilisé comme solution de repli pour les appareils qui ne prennent pas en charge SRTP.

{% hint style="info" %}
**Note** 

Par défaut, le cryptage AES-128 bits est activé pour les supports d'appel transmis par les appareils SIP pris en charge. Les administrateurs peuvent [mettre à niveau les appareils vers le cryptage AES-256 bits](https://support.zoom.com/hc/en/article?id=zm_kb&sysparm_article=KB0069186#h_01ECXCAW1EWJ42PMJZ41G8SN9G) à l'aide du portail web. Les lignes de fax peuvent ne pas supporter un cryptage complet.
{% endhint %}

### Plates-formes, appareils et matériel pris en charge

En plus des applications Zoom Workplace de bureau et mobile et de l'application Zoom Rooms, Zoom Phone prend en charge une liste croissante de téléphones IP, de matériel de téléphonie et d'accessoires.

Les listes suivantes contiennent les **fabricants de matériel** pris en charge pour le téléphone Zoom, et non les modèles spécifiques. Comme Zoom Phone continue à supporter de nouveaux matériels au fil du temps, visitez le centre de support de Zoom pour voir la liste la plus récente des [matériels certifiés Zoom Phone](https://support.zoom.com/hc/en/article?id=zm_kb&sysparm_article=KB0060242), y compris les modèles supportés, les versions de firmware et les standards de cryptage supportés disponibles pour chacun d'entre eux.

#### <mark style="color:blue;">Plates-formes prises en charge</mark>

Zoom Phone est supporté nativement par les plateformes suivantes :

{% columns %}
{% column width="50%" %}

* Zoom Workplace Mac desktop app
* Zoom Workplace, application pour le bureau de Windows
* Application Zoom Rooms {% endcolumn %}

{% column %}

* Zoom Workplace Android mobile app
* Application mobile Zoom Workplace iOS/iPadOS {% endcolumn %} {% endcolumns %}

#### <mark style="color:blue;">Google Chrome Web App</mark>

Zoom Phone dispose d'une prise en charge limitée des fonctions dans Zoom for Chrome Zoom Web App, qui permet aux utilisateurs d'utiliser certaines des fonctions disponibles sur l'application Zoom Workplace de bureau ou mobile dans un navigateur web Google Chrome.

Consultez le centre de support de Zoom pour plus d'informations sur [Chrome Web App](https://support.zoom.com/hc/en/article?id=zm_kb&sysparm_article=KB0059744), ou adressez-vous à l'équipe de votre compte Zoom pour plus d'informations sur la parité des fonctionnalités et les capacités.

#### <mark style="color:blue;">Fabricants de téléphones IP pris en charge</mark>

Zoom Phone supporte des modèles limités de téléphones IP des fabricants suivants :

{% columns %}
{% column %}

* AudioCodes
* Avaya
* Cisco
* Grandstream {% endcolumn %}

{% column %}

* Mitel
* Polyéthylène
* Yealink {% endcolumn %} {% endcolumns %}

#### <mark style="color:blue;">Fabricants d'accessoires pour téléphones IP pris en charge</mark>

Le téléphone Zoom supporte des accessoires de téléphone IP limités des fabricants suivants :

{% columns %}
{% column %}

* Polyéthylène {% endcolumn %}

{% column %}

* Yealink {% endcolumn %} {% endcolumns %}

#### <mark style="color:blue;">Fabricants de passerelles analogiques pris en charge</mark>

Zoom Phone supporte les passerelles analogiques limitées des fabricants suivants :

{% columns %}
{% column %}

* AudioCodes
* Cisco {% endcolumn %}

{% column %}

* Grandstream
* Polyéthylène {% endcolumn %} {% endcolumns %}

#### <mark style="color:blue;">Fabricants de contrôleurs de session en périphérie (SBC) pris en charge</mark>

Zoom Phone supporte les contrôleurs de session limités des fabricants suivants :

{% columns %}
{% column %}

* AudioCodes
* Avaya
* Cisco
* Mitel {% endcolumn %}

{% column %}

* NextGen
* Oracle
* Ruban
* TE-Systems {% endcolumn %} {% endcolumns %}

#### <mark style="color:blue;">Exigences du SBC</mark>

Pour intégrer un SBC avec Zoom Phone, un SBC doit répondre aux exigences suivantes :

{% columns %}
{% column %}

* Prise en charge de TLS 1\.2 et SRTP
* Prise en charge de TLS mutuel
* Protocole d'initiation de session (SIP)
* DTMF (RFC-2833) {% endcolumn %}

{% column %}

* Dissimulation de la topologie (RFC-5853)
* Offre anticipée SIP (obligatoire)
* **Codecs :** Opus, G.711 μ-law, G.711 A-law et/ou G.729 {% endcolumn %} {% endcolumns %}

#### <mark style="color:blue;">Systèmes de téléavertisseurs et d'interphones pris en charge</mark>

Zoom Phone supporte les systèmes de téléavertisseurs et d'interphones limités des fabricants suivants :

{% columns %}
{% column %}

* 2N
* Algo {% endcolumn %}

{% column %}

* CyberDonnées
* Grandstream {% endcolumn %} {% endcolumns %}

#### <mark style="color:blue;">Codecs pris en charge</mark>

Par défaut, les applications mobiles et de bureau Zoom Workplace utiliseront le codec Opus lors de la connexion à un appel ; cependant, Zoom Phone prend également en charge les codecs suivants pour les appareils physiques :

{% columns %}
{% column %}

* Opus
* G.711 μ-law {% endcolumn %}

{% column %}

* G.711 A-law
* G.729 {% endcolumn %} {% endcolumns %}

### Caractéristiques du téléphone Zoom

Les listes suivantes décrivent les fonctions principales disponibles avec Zoom Phone. Comme l'équipe de Zoom Phone innove continuellement, des fonctions supplémentaires non listées peuvent également être disponibles. Si une fonctionnalité importante pour votre organisation n'est pas listée, veuillez contacter votre équipe pour plus d'informations. La disponibilité des fonctionnalités peut être influencée par la [licence](licenses-calling-plans-and-add-ons.md#zoom-phone-licenses) et le [plan d'appel de](licenses-calling-plans-and-add-ons.md#zoom-phone-calling-plans) l'utilisateur.
<table><thead><tr><th valign="top">Fonctionnalités de l'utilisateur du téléphone Zoom</th><th valign="top">Fonctions d'administration du téléphone Zoom</th><th valign="top">Support de la langue de l'invite audio</th></tr></thead><tbody><tr><td valign="top"><ul><li>Blocage des appels</li><li>Délégation d'appel</li><li>Renvoi d'appel</li><li>Paramètres de traitement des appels</li><li>Transfert d'appel entre appareils</li><li>Historique des appels</li><li>Mise en attente de l'appel</li><li>Call Me On</li><li>Surveillance des appels (écoute, chuchotement, intrusion, prise en charge)</li><li>Parc d'appel</li><li>État de la présence d'un appel</li><li>File d'attente Chats Channels</li><li>Entrée/sortie de la file d'attente d'appels</li><li>Enregistrement des appels</li><li>Transfert d'appel amélioré</li><li>Identification de l'appelant</li><li>Verrouillage de l'écran du téléphone de bureau</li><li>Élever l'appel à la réunion</li><li>Appel d'urgence</li><li>Appels cryptés de bout en bout</li><li>Conférence téléphonique à plusieurs</li><li>Prise en charge de plusieurs clés et positions</li><li>Heures ouvrables personnelles</li><li>Heures de congés personnels</li><li>Musique d'attente personnelle</li><li>Code PIN personnel</li><li>Pousser pour parler</li><li>Sélectionner l'identification de l'appelant sortant</li><li>SMS</li><li>Courrier vidéo</li><li>Boîte vocale</li><li>Transcription des messages vocaux</li></ul></td><td valign="top"><ul><li>Réceptionnistes automobiles</li><li>Liste des numéros bloqués</li><li>Création/gestion de sites en vrac</li><li>Heures d'ouverture</li><li>Analyse du parcours de l'appel</li><li>Journal des appels</li><li>Enregistrement des appels (ad hoc, automatique)</li><li>Files d'attente (Callbacks, Routing Overrides)</li><li>Téléphones de la zone commune</li><li>Support mobile de l'espace commun (iOS/Android)</li><li>Configuration des notifications par courrier électronique</li><li>Configuration des paramètres du téléphone IP</li><li>Tableaux muraux personnalisables (files d'attente/réceptionnistes automatiques)</li><li>Définir les heures d'appel/SMS</li><li>Définir les lieux d'appel/SMS</li><li>Gestion des appareils</li><li>Répertoire de composition par nom</li><li>Services d'urgence</li><li>Enquête de retour d'information à la fin de l'appel</li><li>Contacts externes</li><li>Approvisionnement automatique des travailleurs de première ligne</li><li>Musique d'attente</li><li>Hot Desking</li><li>Gestion globale des consentements pour les SMS</li><li>Aperçu des appels entrants</li><li>Dépistage des virus par SMS à l'arrivée</li><li>Contrôle d'accès à l'adresse IP</li><li>Transcriptions en direct</li><li>Masquer les données personnelles du tableau de bord et du journal des appels</li><li>Marques et campagnes multiples (10DLC) </li><li>Apparences de ligne multiples </li><li>Recherche de personnes</li><li>Soutien à la conformité PCI</li><li>Exigences et protections relatives au code PIN</li><li>Affectation de la plage de ports</li><li>Modèle de provisionnement</li><li>Mise à disposition des utilisateurs en attente</li><li>Pousser pour parler</li><li>Tableaux de bord de la qualité</li><li>Stockage régional des SMS/MMS</li><li>Règles de routage</li><li>Mappage des rôles SAML</li><li>Groupes de lignes partagées</li><li>Attribution d'une licence d'authentification unique</li><li>Gestion du site</li><li>SVI intelligent</li><li>Outil d'étiquette SMS</li><li>Contrôles de sécurité des SMS (désactiver les hyperliens, bloquer les pièces jointes, désactiver les MMS de groupe, limiter le nombre de caractères, contrôler les Emoji)</li><li>Liste des numéros de spam</li><li>Protection contre le spam</li><li>S'abonner à Zoom Phone Reports</li><li>Protection de la messagerie vocale contre le piratage du code PIN</li></ul></td><td valign="top"><ul><li>L'arabe</li><li>Bengali</li><li>Catalan</li><li>Chinois (cantonais)</li><li>Chinois (traditionnel)</li><li>Chinois (simplifié)</li><li>Tchèque</li><li>Danois</li><li>Néerlandais</li><li>Anglais (Amérique)</li><li>Anglais (Grande-Bretagne)</li><li>Estonien</li><li>Finlandais</li><li>Français (Canada)</li><li>Français (France)</li><li>Allemand</li><li>Grecque</li><li>Hébreu</li><li>Hindi</li><li>Hongrois</li><li>Indonésien</li><li>Italien</li><li>Japonais</li><li>Coréen</li><li>Malais</li><li>Persan</li><li>Polonais</li><li>Portugais (Brésil)</li><li>Portugais (Portugal)</li><li>Roumain</li><li>Espagnol (Amérique)</li><li>Espagnol (Espagne)</li><li>Suédois</li><li>Tagalog</li><li>Tamoul</li><li>Telugu</li><li>Thaïlande</li><li>Turc</li><li>Vietnamien</li><li>Ukrainien</li></ul></td></tr></tbody></table> 

### Support de fax

Le fax en ligne de Zoom permet aux utilisateurs licenciés de Zoom Phone d'envoyer et de recevoir des fax via l'application Zoom Workplace en utilisant des numéros fournis par Zoom ou BYOC, supportant jusqu'à 300 pages par fax avec des formats de fichiers multiples et l'intégration du stockage dans le nuage. Cette fonction comprend la gestion des dossiers, des capacités de prévisualisation/téléchargement, des actions en masse, des tentatives de transmission de fax améliorées, des rapports détaillés et des notes de suivi persistantes. 

Pour plus d'informations sur les nouvelles fonctionnalités de fax en ligne, veuillez consulter la [documentation de support de Zoom sur le fax en](https://support.zoom.com/hc/en/article?id=zm_kb&sysparm_article=KB0079042) ligne.

### Licences, plans d'appel et compléments d'appel

Zoom Phone propose une large gamme de licences, de plans d'appel et de modules complémentaires pour répondre aux besoins des clients. Fondamentalement, chaque utilisateur ou appareil utilisant Zoom Phone a besoin d'une licence Zoom Phone Basic pour accéder aux fonctions PBX de base. Pour les utilisateurs de Zoom Phone Native (c'est-à-dire non-BYOC-C/P), un plan d'appel est indispensable pour passer des appels sortants ; sinon, les comptes BYOC seront facturés par l'opérateur sous-jacent pour leur utilisation.

En plus des plans d'appel, Zoom propose également plusieurs modules complémentaires pour les clients des services natifs et des services BYOC-C/P, offrant aux utilisateurs des caractéristiques, des capacités et des fonctionnalités supplémentaires.

{% hint style="info" %}
**Note** 

Certains plans tarifaires Zoom incluent des licences groupées qui, lorsqu'elles sont appliquées à un utilisateur, peuvent automatiquement appliquer un plan d'appel Zoom Phone et des fonctions supplémentaires, simplifiant ainsi le processus de provisionnement. Pour plus d'informations sur les licences groupées, contactez votre équipe Zoom.
{% endhint %}
<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXeKoG_K5hyyziw4KG0-4uFnNxQtUTntGWVU8jFefA_iq3DPjfu6mQHXLQpFMztK-EgUWEDB_Tw312tdNjKnoveFZ4RaqKxB_U4qK0_2F80qdu_iGlEBodMBjuLOwJ5zLeTu5d-O2SNV9oPkKw7CDLk?key=gORaE6vjeZ6i7Y4PGyLKfw" alt="" width="563"><figcaption><p>Exemple de licence Zoom Phone.</p></figcaption></figure> 

{% content-ref url="licenses-calling-plans-and-add-ons.md" %}
[licenses-calling-plans-and-add-ons.md](licenses-calling-plans-and-add-ons.md)
{% endcontent-ref %}

### Intégration de Zoom Phone

Zoom Phone prend en charge diverses intégrations pour améliorer les fonctionnalités et l'efficacité du flux de travail de l'utilisateur. Bien que la liste suivante ne soit pas exhaustive, certaines des intégrations les plus populaires de Zoom Phone sont brièvement décrites dans la section suivante.

{% content-ref url="zoom-phone-integrations.md" %}
[zoom-phone-integrations.md](zoom-phone-integrations.md)
{% endcontent-ref %}

### Intégration des centres de contact

#### <mark style="color:blue;">Zoom Contact Center</mark>

Zoom Contact Center (ZCC) est une solution omnicanale d'entreprise qui intègre la plate-forme de communications unifiées de Zoom avec des fonctionnalités de centre de contact. Conçu pour améliorer l'expérience des clients, ZCC peut fournir un service rapide et personnalisé à travers une série de canaux, y compris la vidéo, la voix (téléphone), le SMS, les médias sociaux et le chat en ligne, ainsi que l'agent virtuel de Zoom, alimenté par l'IA.

Pour plus d'informations sur Zoom Contact Center, consultez le [site web de Zoom](https://explore.zoom.us/en/products/contactcenter/) ou adressez-vous à votre équipe Zoom.

#### <mark style="color:blue;">Suite de gestion de l'engagement du personnel de Zoom</mark>

La suite Workforce Engagement Management de Zoom fournit des produits et des fonctionnalités supplémentaires qui complètent et étendent la puissance de Zoom Contact Center avec Zoom Phone.

Avec **Zoom Workforce Management** , les entreprises ont accès à des outils alimentés par l'IA qui peuvent prévoir le volume futur de contacts, organiser et concevoir des horaires qui s'alignent sur le volume prévu à travers différents canaux, et prédire les charges de travail des agents.

Avec **Zoom Quality Management** , les responsables des centres de contact ont accès à divers outils et fonctionnalités qui contrôlent et analysent les interactions avec les consommateurs, évaluent les performances des agents, offrent des informations exploitables et identifient de manière proactive les domaines à améliorer.

Pour plus d'informations sur la suite Workforce Engagement Management de Zoom, consultez le [site web de Zoom](https://www.zoom.com/en/products/contact-center/features/workforce-engagement-management/) ou adressez-vous à votre équipe de compte Zoom.

#### <mark style="color:blue;">Intégrations supplémentaires au centre de contact</mark>

En plus de Zoom Contact Center, Zoom Phone supporte également les intégrations avec Five9, Twilio, Genesys, NICE inContact et Talkdesk.

### Survivance du téléphone Zoom

Pour les entreprises qui utilisent un service de téléphonie en nuage dépendant de la connectivité d'un fournisseur d'accès à Internet, le maintien des services de téléphonie en cas de défaillance du service Internet ou d'un événement ayant un impact sur le service est essentiel pour la continuité et les opérations de l'entreprise. Pour répondre à ces scénarios, Zoom propose le module Zoom Phone Local Survivability (ZPLS) en tant que charge de travail du nœud Zoom, qui fournit une résilience téléphonique en cas d'interruption de service.

Lors d'un événement de survivabilité où les terminaux Zoom ne peuvent pas atteindre le service Zoom Phone cloud, les appareils utilisateurs pris en charge s'enregistrent sur le module ZPLS, qui fournit des services de téléphonie de base, tels que les appels internes et les groupes de distribution de survivabilité, jusqu'à ce que le service complet puisse être rétabli. Les entreprises peuvent étendre cette fonctionnalité en connectant le module ZPLS à un contrôleur de session (SBC) relié à un opérateur sous-jacent (BYOC) pour acheminer les appels via le réseau téléphonique public commuté (RTPC).

Lorsqu'elles sont intégrées à un SBC, les entreprises bénéficient du meilleur des deux mondes : la simplicité et la facilité d'un système téléphonique géré dans le nuage, avec la capacité de survie et la résilience d'une infrastructure sur site en cas d'imprévu. En bref, avec ZPLS, les entreprises peuvent aisément abandonner la plupart des appareils de téléphonie traditionnels sur site et migrer en toute confiance vers un système téléphonique basé sur l'informatique dématérialisée.

Pour plus d'informations, reportez-vous à la section de ce document consacrée à la [capacité de survie locale du téléphone Zoom.](../zoom-phone-local-survivability.md)

### Logique d'acheminement des appels

Zoom Phone offre de nombreuses possibilités d'acheminement des appels, en supportant plusieurs sites, des contacts externes, des règles d'acheminement, etc. Pour aider le client à comprendre l'impact des flux d'appels, Zoom Phone traite différents scénarios d'appels à travers une logique de routage d'appels complète.
<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXe8AcIH76HJyaZbZGgLzZGSoYsioREHMSnT-fZmhYUkttArqrTTItC1QHW2UqdK9Za3Gzn3XpmDO-U3sRIBjpvEuareYjb5FM9VCDufgIFDrP5jompyaKIKkAmBXMsIOCOO7MzxMIck7e-lmzsqXyY?key=gORaE6vjeZ6i7Y4PGyLKfw" alt="" width="563"><figcaption><p>Exemple de différents flux d'appels Zoom Phone.</p></figcaption></figure> 

### Configuration du réseau

Grâce à l'architecture en nuage de Zoom Phone, la configuration de Zoom Phone pour votre réseau est nettement plus facile que celle des systèmes téléphoniques traditionnels sur site. D'un point de vue très simple, les utilisateurs ont besoin de deux facteurs clés pour commencer à téléphoner avec succès : une connexion internet opérationnelle et des ports réseau ouverts. Tant que les utilisateurs peuvent maintenir une connexion active avec les centres de données de Zoom Phone et que les ports nécessaires ne sont pas bloqués, Zoom Phone est prêt à être utilisé au sein de votre réseau.

{% content-ref url="network-configuration.md" %}
[configuration-réseau.md](network-configuration.md)
{% endcontent-ref %}

