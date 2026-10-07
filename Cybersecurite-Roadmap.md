---
title: "Cybersécurité — Roadmap enrichie"
aliases: ["Roadmap Cyber", "Cybersecurity Roadmap", "Base de connaissances cyber"]
tags: [cybersécurité, roadmap, moc, sécurité, pentest, blue-team, réseau, cloud]
source: "https://roadmap.sh/cyber-security"
created: 2026-10-07
status: en-cours
---

# 🛡️ Cybersécurité — Roadmap enrichie

> [!NOTE]
> Base de connaissances construite à partir de la roadmap officielle [roadmap.sh/cyber-security](https://roadmap.sh/cyber-security), **enrichie** pour servir de référence de révision et de « second cerveau ».
> Chaque nœud de la roadmap est repris, défini, puis complété (fonctionnement, intérêt, défenses, commandes).

## 📑 Comment lire ce document

- **Callouts** : `> [!TIP]` (astuce), `> [!WARNING]` (piège courant), `> [!IMPORTANT]` (à retenir absolument). Ces blocs s'affichent nativement sur **GitHub** *et* **Obsidian**.
- **Tableaux** : utilisés pour les énumérations (ports, protocoles, commandes, attaques) — à parcourir en diagonale lors des révisions.
- **Légende de criticité** : 🟢 fondamental · 🟡 intermédiaire · 🔴 avancé.
- **Obsidian** : le frontmatter YAML (tags/alias) alimente le graphe et la recherche. Pour éclater ce fichier en notes atomiques reliées par `[[wikilinks]]`, voir la section [Aller plus loin](#-aller-plus-loin).

---

## Sommaire

1. [Compétences IT fondamentales](#1--compétences-it-fondamentales)
2. [Systèmes d'exploitation](#2--systèmes-dexploitation)
3. [Réseau — connaissances & protocoles](#3--réseau--connaissances--protocoles)
4. [Compétences & connaissances en sécurité](#4--compétences--connaissances-en-sécurité)
5. [Cryptographie](#5--cryptographie)
6. [Types d'attaques](#6--types-dattaques)
7. [Cloud](#7--cloud)
8. [Programmation & scripting](#8--programmation--scripting)
9. [Frameworks, normes & conformité](#9--frameworks-normes--conformité)
10. [Outils (par usage)](#10--outils-par-usage)
11. [Certifications](#11--certifications)
12. [CTF & plateformes d'entraînement](#12--ctf--plateformes-dentraînement)
13. [Aller plus loin](#-aller-plus-loin)

---

## 1. 🧱 Compétences IT fondamentales

> [!IMPORTANT]
> On ne sécurise bien que ce que l'on comprend. **Avant la sécurité vient l'informatique générale** : matériel, OS, réseau, suites bureautiques. C'est le socle de toute analyse d'incident ou de vulnérabilité.

### Matériel & connectique 🟢

- **Composants** : CPU (exécution), RAM (mémoire volatile — cible des *memory dumps* en forensic), stockage (HDD/SSD/NVMe), carte mère, GPU, alimentation, BIOS/UEFI (le firmware de démarrage, cible de rootkits bas niveau).
- **Types de connexion** : USB, HDMI/DisplayPort, Ethernet (RJ45), Thunderbolt, SATA/M.2. Chaque port physique est aussi une **surface d'attaque** (ex. *BadUSB*, *juice jacking* sur USB).

### Réseaux sans fil & proximité 🟢

| Techno | Portée | Usage | Risque sécurité typique |
|---|---|---|---|
| **WiFi** | ~dizaines de m | LAN sans fil | Evil Twin, deauth, WEP/WPA faibles |
| **Bluetooth** | ~10 m | Périphériques | BlueBorne, bluejacking/bluesnarfing |
| **NFC** | ~cm | Paiement, badges | Clonage de carte, relais |
| **Infrarouge (IR)** | ligne de vue | Télécommandes | Marginal, mais existant |

### Suites bureautiques & collaboratives 🟢

- **MS Office / Microsoft 365**, **Google Workspace**, **iCloud**.
- Enjeu cyber : **macros Office** (vecteur n°1 de phishing historique), partages mal configurés, politiques de rétention et DLP sur ces plateformes.

### Dépannage indépendant de l'OS (OS-Independent Troubleshooting) 🟢

Méthode générale : **isoler** (matériel vs logiciel vs réseau) → **reproduire** → **tester une hypothèse à la fois** → **documenter**. Transférable directement à l'investigation d'incident.

---

## 2. 💻 Systèmes d'exploitation

> [!NOTE]
> Objectif : savoir faire **la même chose** sur **Windows, Linux et macOS** — installer, configurer, gérer droits/fichiers, dépanner, en **GUI** comme en **CLI**.

### Compétences à acquérir pour *chaque* OS 🟢

- Installation & configuration, versions et différences.
- Navigation **GUI et CLI**.
- **Permissions** (voir ci-dessous).
- Installation d'applications, opérations **CRUD** sur fichiers (Create/Read/Update/Delete).
- Dépannage et commandes courantes.

### Permissions 🟢

- **Linux/Unix** : modèle `rwx` sur `user/group/other` → notation octale (`chmod 640`), `chown`, bit SUID/SGID/sticky. Les **SUID mal configurés** sont un vecteur classique d'escalade de privilèges (voir [GTFOBins](#lolbas--gtfobins--wadcoms)).
- **Windows** : ACL NTFS, groupes, UAC, comptes `SYSTEM`/`Administrator`, politiques via **GPO**.

### Commandes essentielles (antisèche) 🟢

| Intention | Linux | Windows (CMD/PowerShell) |
|---|---|---|
| Lister fichiers | `ls -la` | `dir` / `Get-ChildItem` |
| Où suis-je | `pwd` | `cd` / `Get-Location` |
| Processus | `ps aux`, `top`, `htop` | `tasklist` / `Get-Process` |
| Réseau actif | `ss -tulpn`, `netstat` | `netstat -ano` |
| Chercher | `grep`, `find` | `findstr` / `Select-String` |
| Droits | `chmod`, `chown` | `icacls` |
| Service | `systemctl` | `sc` / `Get-Service` |

> [!TIP]
> Pour l'offensif comme le défensif, **maîtriser le CLI** est non négociable : l'automatisation, l'analyse de logs et le travail sur serveurs distants passent par là.

---

## 3. 🌐 Réseau — connaissances & protocoles

> [!IMPORTANT]
> Le réseau est **le terrain de jeu** de la cyber. OSI, protocoles, ports, adressage et segmentation reviennent dans *toutes* les attaques et défenses.

### Le modèle OSI 🟢

| # | Couche | Rôle | Exemples | PDU |
|---|---|---|---|---|
| 7 | Application | Services utilisateur | HTTP, DNS, SMTP | Données |
| 6 | Présentation | Chiffrement, encodage | TLS, ASCII, JPEG | Données |
| 5 | Session | Ouverture/maintien de session | NetBIOS, RPC | Données |
| 4 | Transport | Fiabilité, ports | TCP, UDP | Segment |
| 3 | Réseau | Adressage logique, routage | IP, ICMP, IPsec | Paquet |
| 2 | Liaison | Adressage physique (MAC) | Ethernet, ARP, VLAN | Trame |
| 1 | Physique | Signal électrique/optique | câbles, RJ45 | Bits |

> [!TIP]
> Moyen mnémotechnique : *« Please Do Not Throw Sausage Pizza Away »* (1→7). Beaucoup d'attaques se **classent par couche** : ARP spoofing (L2), IP spoofing (L3), SYN flood (L4), attaques applicatives/OWASP (L7).

Le modèle **TCP/IP** (4 couches : Accès réseau, Internet, Transport, Application) est le modèle réellement implémenté ; OSI reste le référentiel pédagogique.

### Adressage IP & terminologie 🟢

- **IPv4** (32 bits, `192.168.1.10`) vs **IPv6** (128 bits).
- **Public vs privé** : plages privées RFC 1918 → `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16` (non routables sur Internet, sortent via NAT).
- **Vocabulaire clé** :
  - *localhost / loopback* : `127.0.0.1` (`::1` en IPv6) — soi-même.
  - *CIDR* : notation `/24` = masque. 
  - *subnet mask* : sépare partie réseau / partie hôte.
  - *default gateway* : porte de sortie vers les autres réseaux.

### Subnetting (sous-réseaux) 🟡

Découper un réseau en segments plus petits pour l'**isolation**, la **performance** et la **sécurité**.

| CIDR | Masque | Hôtes utilisables |
|---|---|---|
| /30 | 255.255.255.252 | 2 |
| /29 | 255.255.255.248 | 6 |
| /24 | 255.255.255.0 | 254 |
| /16 | 255.255.0.0 | 65 534 |

Formule : hôtes utilisables = `2^(32 - préfixe) - 2` (on retire adresse réseau et broadcast).

### Protocoles & ports courants 🟢

| Port | Proto | Service | Sécurisé ? |
|---|---|---|---|
| 20/21 | TCP | FTP | ❌ clair → préférer **SFTP (22)** / FTPS |
| 22 | TCP | SSH / SFTP / SCP | ✅ |
| 23 | TCP | Telnet | ❌ clair → bannir |
| 25 | TCP | SMTP | ⚠️ (STARTTLS) |
| 53 | TCP/UDP | DNS | ⚠️ → **DNSSEC**, DoH/DoT |
| 67/68 | UDP | DHCP | — |
| 80 | TCP | HTTP | ❌ clair → **HTTPS** |
| 110 | TCP | POP3 | ❌ → POP3S (995) |
| 123 | UDP | NTP | — |
| 143 | TCP | IMAP | → IMAPS (993) |
| 389 | TCP | LDAP | ❌ → **LDAPS (636)** |
| 443 | TCP | HTTPS / TLS | ✅ |
| 445 | TCP | SMB | ⚠️ cible fréquente (EternalBlue) |
| 636 | TCP | LDAPS | ✅ |
| 3389 | TCP | RDP | ⚠️ exposer = risque majeur |

> [!WARNING]
> **Ne jamais exposer RDP (3389), SMB (445) ou des bases de données directement sur Internet.** Ce sont des portes d'entrée classiques de ransomwares. Passer par VPN / bastion (*jump server*).

### Protocoles sécurisés vs non sécurisés 🟡

| Non sécurisé | Alternative sécurisée | Couche protégée |
|---|---|---|
| FTP | **SFTP / FTPS** | transfert fichiers |
| HTTP | **HTTPS (SSL/TLS)** | web |
| Telnet | **SSH** | administration |
| LDAP | **LDAPS** | annuaire |
| DNS | **DNSSEC** (intégrité) | résolution |
| SIP/RTP | **SRTP** | VoIP |
| Mail | **S/MIME**, STARTTLS | messagerie |
| IP | **IPsec** | tunnel/VPN |

### SSL / TLS 🟡

- **TLS** (successeur de SSL, obsolète) assure **confidentialité**, **intégrité** et **authentification** via certificats X.509 et [PKI](#pki--infrastructure-à-clés-publiques).
- *Handshake* TLS : négociation de version/ciphers → échange de clés (ex. ECDHE) → authentification serveur par certificat → clé de session symétrique.
- Versions saines : **TLS 1.2 / 1.3** (1.3 plus rapide et plus sûr). SSLv3, TLS 1.0/1.1 = à désactiver.

### Terminologie réseau à connaître 🟢

- **VLAN** : segmentation logique L2. **DMZ** : zone tampon exposée. **ARP** : résolution IP→MAC (cible de l'*ARP poisoning*). **VM** : machine virtuelle.
- **DHCP** (attribution d'IP), **DNS** (nom↔IP), **NAT** (translation d'adresses), **IP**.
- **Routeur** (L3, entre réseaux), **Switch** (L2, intra-réseau), **VPN** (tunnel chiffré).
- Étendue : **LAN** (local), **WLAN** (local sans fil), **MAN** (métropolitain), **WAN** (étendu, ex. Internet).

### Services d'infrastructure : DHCP / DNS / NTP / IPAM 🟡

- **DHCP** : baux d'adresses automatiques. Attaque : *DHCP starvation* / *rogue DHCP*.
- **DNS** : colonne vertébrale d'Internet ; cibles : empoisonnement de cache, tunneling DNS (exfiltration).
- **NTP** : synchronisation horaire — **critique** pour la corrélation de logs et Kerberos (tolérance de ~5 min).
- **IPAM** : gestion centralisée de l'adressage IP.

### Topologies réseau 🟡

**Star** (étoile, la plus courante), **Ring** (anneau), **Mesh** (maillée, résiliente), **Bus** (historique). Impact sécurité : la topologie conditionne les **points de défaillance** et la **propagation** d'un compromis.

### NAS vs SAN 🟡

- **NAS** : stockage **fichier** partagé sur le réseau (NFS/SMB), simple.
- **SAN** : réseau **bloc** dédié hautes performances (Fibre Channel/iSCSI), pour datacenters.

### Virtualisation 🟡

- **Hyperviseur** : type 1 (*bare-metal* : ESXi, Proxmox, Hyper-V) vs type 2 (hébergé : VirtualBox, VMware Workstation).
- **Host OS** (hôte) / **Guest OS** (invité) / **VM**.
- Enjeu cyber : **isolation** entre VM, risque de *VM escape*, snapshots pour l'analyse de malware.

### Méthodologies d'authentification 🟡

- **Kerberos** : tickets (TGT/TGS) — cœur d'Active Directory. Attaques : *Kerberoasting*, *Pass-the-Ticket*, *Golden/Silver Ticket*.
- **RADIUS** : AAA centralisé (accès réseau/VPN/WiFi 802.1X).
- **LDAP** : protocole d'annuaire.
- **SSO** : authentification unique (SAML, OAuth2/OIDC).
- **Certificats**, **authentification locale**.

---

## 4. 🔐 Compétences & connaissances en sécurité

### La triade CIA 🟢

> [!IMPORTANT]
> **Tout** en sécurité se ramène à la triade :
> - **C**onfidentialité — l'info n'est lue que par les autorisés (chiffrement, contrôle d'accès).
> - **I**ntégrité — l'info n'est pas altérée (hash, signatures).
> - **A**vailability (disponibilité) — l'info est accessible quand nécessaire (redondance, sauvegardes, anti-DDoS).
> On y ajoute souvent **authenticité** et **non-répudiation**.

### Authentification vs Autorisation 🟢

- **Authentification** : *qui es-tu ?* (prouver son identité).
- **Autorisation** : *as-tu le droit ?* (permissions une fois identifié).
- Facteurs : *connaissance* (mot de passe), *possession* (token/téléphone), *inhérence* (biométrie).
- **MFA / 2FA** : combiner ≥ 2 facteurs — mesure la plus rentable contre le vol d'identifiants.

### Défense en profondeur (Defense in Depth) 🟢

Empiler **plusieurs couches** de contrôles (périmètre, réseau, hôte, application, données, humain) pour qu'aucune défaillance unique ne soit fatale. Modèle complémentaire : **Zero Trust**.

### Zero Trust 🟡

> [!TIP]
> Principe : **« Never trust, always verify »**. Aucune confiance implicite, même à l'intérieur du réseau. Chaque accès est vérifié (identité, posture de l'appareil, contexte), avec **moindre privilège** et **micro-segmentation**.

### Périmètre vs DMZ vs Segmentation 🟡

- **Périmètre** : frontière traditionnelle (pare-feu en bordure) — modèle « château-douves », de moins en moins suffisant.
- **DMZ** : sous-réseau isolé pour les services exposés (web, mail), tampon entre Internet et le LAN.
- **Segmentation** : cloisonner le réseau interne pour **limiter les déplacements latéraux**.

### Isolation 🟡

Sandboxing, conteneurs, VM, VLAN : confiner un processus/hôte pour contenir un compromis. Base de l'analyse de malware (détonation en environnement isolé).

### Notion de risque 🟢

> [!IMPORTANT]
> **Risque = Menace × Vulnérabilité × Impact** (sur un *actif* ayant une *valeur*).
> Traitement du risque : **réduire** (contrôles), **transférer** (assurance), **accepter** (si résiduel faible), **éviter** (supprimer l'activité).

- **Menace** : ce qui peut causer un dommage (acteur + capacité + intention).
- **Vulnérabilité** : faiblesse exploitable.
- **Impact** : conséquence (financière, réputationnelle, légale, opérationnelle).

> [!NOTE]
> C'est exactement la logique des méthodes d'analyse de risque comme **EBIOS Risk Manager** (ANSSI) : identifier les biens essentiels/supports, les sources de risque, les scénarios stratégiques/opérationnels, puis traiter.

### Acteurs de la menace, motivations & classification 🟡

- **Acteurs** : *script kiddies*, cybercriminels (motivation financière), **hacktivistes**, **APT** (États-nations), *insiders* (menace interne).
- **Classification des menaces** : **Zero-Day** (faille inconnue, sans correctif), **connue vs inconnue**, **APT** (menace persistante avancée, furtive et ciblée).

### OWASP Top 10 (web) 🟡

> [!IMPORTANT]
> Référentiel **incontournable** des risques applicatifs web. Version **2021** :

| Rang | Catégorie | Idée clé |
|---|---|---|
| A01 | **Broken Access Control** | Contournement des droits (IDOR, path traversal) |
| A02 | **Cryptographic Failures** | Données sensibles mal/non chiffrées |
| A03 | **Injection** | SQLi, commande, LDAP — entrées non validées |
| A04 | **Insecure Design** | Défaut de conception (manque de *threat modeling*) |
| A05 | **Security Misconfiguration** | Config par défaut, services inutiles, verbosité |
| A06 | **Vulnerable & Outdated Components** | Dépendances non patchées |
| A07 | **Identification & Auth Failures** | Sessions, mots de passe, MFA défaillants |
| A08 | **Software & Data Integrity Failures** | Supply chain, désérialisation |
| A09 | **Security Logging & Monitoring Failures** | Pas de détection |
| A10 | **SSRF** | Le serveur est forcé de requêter une ressource interne |

### Attaques web & escalade de privilèges 🟡

- Voir détail dans [Types d'attaques](#6--types-dattaques). 
- **Privilege Escalation** :
  - *Verticale* : utilisateur standard → admin/root (SUID, noyau non patché, *Pass-the-Hash*, mauvaise GPO).
  - *Horizontale* : accéder aux ressources d'un autre utilisateur de même niveau.

### Malwares — types 🟢

| Type | Comportement |
|---|---|
| **Virus** | S'attache à un fichier, nécessite une exécution |
| **Ver (worm)** | Se propage seul sur le réseau |
| **Cheval de Troie** | Se fait passer pour légitime |
| **Ransomware** | Chiffre les données contre rançon |
| **Spyware / Keylogger** | Espionnage, capture de frappe |
| **Rootkit** | Furtivité, persistance bas niveau |
| **Bootkit** | Infecte le démarrage (UEFI/MBR) |
| **RAT** | Contrôle à distance |
| **Botnet** | Flotte de machines zombies |
| **Fileless** | Vit en mémoire / LOLBins, sans fichier sur disque |

### IDS / IPS, pare-feu & terminologie défensive 🟡

| Terme | Rôle |
|---|---|
| **IDS** (NIDS/HIDS) | **Détecte** et alerte (passif) |
| **IPS** (NIPS/HIPS) | **Bloque** en temps réel (actif, en coupure) |
| **Firewall / NGFW** | Filtrage ; le *Next-Gen* ajoute inspection applicative, IPS, filtrage d'URL |
| **Antivirus / Antimalware** | Détection par signatures/heuristique |
| **EDR** | Détection & réponse sur endpoint (comportemental) |
| **DLP** | Prévention de fuite de données |
| **ACL** | Liste de contrôle d'accès (réseau/fichier) |
| **Sandboxing** | Exécution isolée pour analyse |
| **Honeypot** | Leurre pour détecter/étudier les attaquants |

### Matrice de détection 🟢

> [!TIP]
> À connaître par cœur pour le SOC :
> - **Vrai Positif (TP)** : alerte correcte sur une vraie attaque.
> - **Faux Positif (FP)** : fausse alerte (bruit → fatigue d'alerte).
> - **Vrai Négatif (TN)** : silence justifié (rien à signaler).
> - **Faux Négatif (FN)** : **la pire** — une attaque passée sous les radars.

### Équipes Red / Blue / Purple 🟢

- **Red Team** : offensive, simule l'attaquant.
- **Blue Team** : défensive, détection & réponse.
- **Purple Team** : collaboration des deux pour améliorer la détection.

### Renforcement (Hardening) des OS & réseau 🟡

Concepts : **Group Policy**, filtrage par **MAC/NAC**, **blocage de ports**, **ACL**, **patching**, **sinkholes** (rediriger du trafic malveillant), **jump server/bastion**, **endpoint security**, désactivation des services inutiles, principe du **moindre privilège**.

### WiFi — sécurité 🟡

| Protocole | Verdict |
|---|---|
| **WEP** | ❌ Cassé (RC4, IV faibles) |
| **WPA** | ❌ Obsolète (TKIP) |
| **WPA2** | ⚠️ Correct (AES-CCMP) mais vulnérable (KRACK, PMKID) |
| **WPA3** | ✅ Recommandé (SAE, forward secrecy) |

- **WPS** : à désactiver (brute-force du PIN).
- **EAP / PEAP** : méthodes d'authentification 802.1X (entreprise, via RADIUS).

### Processus de réponse à incident (IR) 🟢

> [!IMPORTANT]
> Cycle **NIST / SANS** en 6 phases :
> 1. **Préparation** — outils, playbooks, formation.
> 2. **Identification** — détecter et qualifier l'incident.
> 3. **Confinement** — court et long terme (isoler).
> 4. **Éradication** — supprimer la cause (malware, compte compromis).
> 5. **Récupération** — restaurer, surveiller la reprise.
> 6. **Leçons apprises** — post-mortem, amélioration continue.

### Threat Hunting, Threat Intel & OSINT 🟡

- **Threat Hunting** : recherche **proactive** de menaces non détectées (hypothèses basées sur TTPs, IoC/IoA).
- **Threat Intelligence** : renseignement sur les menaces (IoC, campagnes, acteurs) — stratégique/tactique/opérationnel.
- **OSINT** : renseignement en sources ouvertes (reconnaissance passive, surface d'exposition).

### Forensics (investigation numérique) 🔴

Principes : **chaîne de custody** (intégrité de la preuve), **ordre de volatilité** (RAM avant disque), copie **bit-à-bit** (image), hachage pour prouver l'intégrité. Outils : [FTK Imager, Autopsy, WinHex, memdump](#10--outils-par-usage).

### Autres concepts clés 🟡

- **Cyber Kill Chain** (Lockheed Martin) : Recon → Weaponization → Delivery → Exploitation → Installation → C2 → Actions on objectives. → voir [Frameworks](#9--frameworks-normes--conformité).
- **Runbooks / Playbooks** : procédures standardisées (souvent automatisées via **SOAR**).
- **Backups & résilience** : règle **3-2-1** (3 copies, 2 supports, 1 hors-site) ; tester les restaurations ; copies **immuables/hors-ligne** contre les ransomwares.
- **Vulnerability Management** : scan → priorisation (**CVSS**, exploitabilité) → remédiation → re-scan. Référentiels : **CVE** (identifiant), **CVSS** (score), **CWE** (type de faiblesse).
- **Reverse Engineering** : analyse statique/dynamique de binaires (Ghidra, IDA, x64dbg).
- **Pentest — Rules of Engagement** : périmètre, fenêtre de test, autorisations écrites, contacts d'urgence, règles de non-destruction.
- **Rôles conformité & audit** : vérifier l'adéquation aux normes ; **public** : *stakeholders*, RH, juridique, direction, compliance.
- **Handshakes** : TCP 3-way (SYN, SYN-ACK, ACK), TLS handshake, WPA 4-way handshake (capturé lors d'attaques WiFi).

---

## 5. 🧮 Cryptographie

> [!IMPORTANT]
> La crypto sous-tend la **confidentialité** et l'**intégrité**. Règle d'or : **ne jamais inventer sa crypto** — utiliser des primitives éprouvées et à jour.

### Symétrique vs asymétrique 🟡

| | Symétrique | Asymétrique |
|---|---|---|
| Clés | **1 clé partagée** | **paire** publique/privée |
| Exemples | AES, ChaCha20 | RSA, ECC (ECDSA/ECDH) |
| Vitesse | Rapide | Lent |
| Usage | Chiffrer les données | Échange de clés, signatures |

> Dans la pratique (TLS, PGP), on **combine** : l'asymétrique sert à échanger une **clé de session** symétrique.

### Hachage 🟡

- Fonction **à sens unique** : empreinte de taille fixe, non réversible, effet d'avalanche.
- Usages : intégrité, stockage de mots de passe.
- **Obsolètes** : MD5, SHA-1 (collisions). **Sains** : SHA-256/SHA-3.
- **Mots de passe** : jamais SHA brut → **bcrypt, scrypt, Argon2** (lents, avec **sel**).

### Salting (salage) 🟡

Ajout d'une valeur **aléatoire unique** à chaque mot de passe avant hachage → neutralise les **rainbow tables** et empêche que deux mots de passe identiques aient le même hash.

### Échange de clés (Key Exchange) 🔴

**Diffie-Hellman** (et **ECDHE**) : établir un secret partagé sur un canal non sûr. **ECDHE** apporte la *Perfect Forward Secrecy* (la compromission d'une clé long-terme ne déchiffre pas les sessions passées).

### PKI — Infrastructure à clés publiques 🟡

- **Autorité de certification (CA)** signe des **certificats X.509** liant une identité à une clé publique.
- Chaîne de confiance : CA racine → intermédiaire → certificat final.
- Révocation : **CRL** / **OCSP**.
- Clés **publique vs privée** : la publique chiffre / vérifie, la privée déchiffre / signe (à **protéger absolument**).

### Obfuscation 🟡

Rendre du code/des données difficiles à comprendre **sans** garantie cryptographique (≠ chiffrement). Utilisée par les attaquants (packing de malware) comme en protection logicielle.

---

## 6. ⚔️ Types d'attaques

> [!NOTE]
> Pour chaque attaque : *comment ça marche* + *comment s'en défendre*. Organisé par famille.

### Ingénierie sociale 🟢

| Attaque | Vecteur |
|---|---|
| **Phishing** | Email frauduleux de masse |
| **Spear phishing** | Phishing ciblé (personne précise) |
| **Whaling** | Cible un dirigeant (« gros poisson ») |
| **Vishing** | Par téléphone (voice) |
| **Smishing** | Par SMS |
| **Impersonation** | Usurpation d'identité |
| **Watering hole** | Piéger un site fréquenté par la cible |
| **Shoulder surfing** | Observer par-dessus l'épaule |
| **Dumpster diving** | Fouiller les poubelles (infos jetées) |
| **Tailgating / Piggybacking** | Suivre quelqu'un pour franchir un accès physique |
| **Spam vs Spim** | Courrier indésirable (email) vs messagerie instantanée |

> [!TIP]
> Défense principale : **sensibilisation**, MFA, filtrage mail (SPF/DKIM/DMARC), vérification *out-of-band* des demandes sensibles (virements).

### Mot de passe & accès 🟡

- **Brute force** : essayer toutes les combinaisons. **Password spraying** : un mot de passe commun contre **beaucoup** de comptes (évite le verrouillage).
- **Pass-the-Hash** : réutiliser le hash NTLM sans connaître le mot de passe.
- **Credential stuffing** : rejouer des couples identifiant/mot de passe fuités.
- Défense : MFA, verrouillage de compte, mots de passe longs, détection d'anomalies.

### Réseau 🟡

| Attaque | Principe | Défense |
|---|---|---|
| **DoS / DDoS** | Saturer un service (distribué = botnet) | Anti-DDoS, rate-limiting, CDN |
| **MITM** | S'interposer dans une communication | TLS, HSTS, certificats |
| **Spoofing** | Usurper IP/MAC/email | Filtrage, authentification |
| **ARP poisoning** | Empoisonner le cache ARP (L2) | DAI, VLAN, segmentation |
| **DNS poisoning** | Falsifier la résolution DNS | DNSSEC, résolveurs sûrs |
| **Evil Twin** | Faux point d'accès WiFi jumeau | 802.1X, vérifier le SSID |
| **Rogue Access Point** | Borne non autorisée | WIPS, NAC |
| **Deauth** | Déconnecter des clients WiFi | WPA3 (trames protégées) |
| **VLAN hopping** | Franchir l'isolation VLAN | Désactiver DTP, gérer les trunks |
| **Replay** | Rejouer un message capturé | Nonces, timestamps, séquences |

### Applicatives & web 🟡

| Attaque | Principe | Défense |
|---|---|---|
| **SQL Injection** | Injecter du SQL via une entrée | **Requêtes paramétrées**, ORM, validation |
| **XSS** | Injecter du JS dans une page | Échappement des sorties, CSP |
| **CSRF** | Forcer une action authentifiée à l'insu de l'utilisateur | Tokens anti-CSRF, SameSite |
| **Directory / Path Traversal** | `../` pour sortir du répertoire | Normalisation, allowlist |
| **SSRF** | Faire requêter le serveur en interne | Allowlist, blocage métadonnées cloud |

### Bas niveau / mémoire 🔴

- **Buffer Overflow** : écrire au-delà d'un tampon → corruption/exécution de code. Défenses : **ASLR**, **DEP/NX**, canaris de pile, langages *memory-safe* (Rust).
- **Memory Leak** : fuite de mémoire (déni de service, parfois fuite d'info).

### Divers 🟡

- **Zero-Day** : exploitation d'une faille inconnue de l'éditeur.
- **Typosquatting** : domaines proches (`gooogle.com`) pour piéger.
- **Drive-by download** : infection par simple visite d'un site piégé.
- **Reconnaissance** : collecte d'informations (passive via OSINT, active via scan).

---

## 7. ☁️ Cloud

> [!NOTE]
> Le cloud déplace — mais n'efface pas — la sécurité : **modèle de responsabilité partagée**. Le fournisseur sécurise *le* cloud, le client sécurise *dans* le cloud (données, IAM, config).

### Modèles de service 🟢

| Modèle | Vous gérez | Exemple |
|---|---|---|
| **IaaS** | OS, apps, données | EC2, VM Azure |
| **PaaS** | Apps, données | App Engine, Heroku |
| **SaaS** | Données/usage | Microsoft 365, Salesforce |
| **Serverless (FaaS)** | Code uniquement | Lambda, Cloud Functions |

### Modèles de déploiement 🟢

**Public** (mutualisé), **Privé** (dédié), **Hybride** (mélange), *Community*.

### Fournisseurs & services courants 🟡

- **AWS**, **Azure**, **GCP**.
- **Stockage** : S3, Blob, Google Drive, OneDrive, Dropbox, Box, iCloud.
- Risque n°1 : **buckets de stockage mal configurés** (données exposées publiquement).

### Infrastructure as Code (IaC) 🟡

Décrire l'infra en code versionné (**Terraform**, CloudFormation, Ansible). Avantages sécurité : reproductibilité, revue, scan de config (`tfsec`, `checkov`). Risque : un secret en dur dans le code, une mauvaise config répliquée partout.

### Concepts de sécurité cloud 🟡

- **IAM** et moindre privilège (le contrôle le plus important).
- **CSPM** (posture), **CWPP** (charges de travail), **CASB**, chiffrement au repos/en transit, journalisation (CloudTrail).
- Différences **cloud vs on-premises** : élasticité, API-driven, périmètre flou → la sécurité devient **centrée sur l'identité et la donnée**.

---

## 8. 👨‍💻 Programmation & scripting

> [!TIP]
> Pas besoin d'être développeur, mais **savoir lire et écrire des scripts** décuple l'efficacité (automatisation, exploitation, parsing de logs).

| Langage | Pourquoi en cyber |
|---|---|
| **Python** 🟢 | Le couteau suisse : scripts, outils offensifs/défensifs, automatisation, API |
| **Bash** 🟢 | Administration Linux, chaînage d'outils, parsing (`grep/awk/sed`) |
| **PowerShell** 🟢 | Administration & post-exploitation Windows/AD |
| **JavaScript** 🟡 | Web, compréhension du XSS/DOM |
| **Go** 🟡 | Outils rapides et cross-platform (beaucoup d'outils modernes) |
| **C / C++** 🔴 | Comprendre mémoire, exploits, reverse, buffer overflow |
| **SQL** 🟡 | Comprendre et tester les injections |

> [!TIP]
> *Keep learning* : la constance (un peu chaque jour, projets réels, CTF) bat les sessions intensives ponctuelles.

---

## 9. 🗂️ Frameworks, normes & conformité

### Frameworks d'attaque/analyse 🟡

- **MITRE ATT&CK** : matrice des **tactiques & techniques** réellement observées — la référence pour mapper détections et TTPs.
- **Cyber Kill Chain** (Lockheed Martin) : les 7 étapes d'une intrusion (voir §4).
- **Diamond Model** : analyse d'intrusion selon 4 axes (adversaire, capacité, infrastructure, victime).

### Normes & référentiels 🟡

| Référentiel | Portée |
|---|---|
| **ISO/IEC 27001** | SMSI — management de la sécurité de l'information (certifiable) |
| **NIST CSF** | Cadre : *Identify, Protect, Detect, Respond, Recover* (+ *Govern*) |
| **NIST RMF** | Processus de gestion du risque (SP 800-37) |
| **CIS Controls / Benchmarks** | Contrôles et guides de durcissement concrets |
| **PCI-DSS** | Données de cartes bancaires |
| **RGPD** | Données personnelles (UE) |

> [!NOTE]
> Côté français/européen : **ANSSI** (guides d'hygiène, visa de sécurité), **EBIOS Risk Manager** (analyse de risque), **NIS2** et **DORA** (réglementations récentes). Utile à connaître pour un poste en France.

### SIEM & SOAR 🟡

- **SIEM** : collecte et **corrèle les logs** pour détecter (Splunk, Elastic/ELK, Sentinel, QRadar, Wazuh).
- **SOAR** : **orchestration & automatisation** de la réponse (playbooks).

---

## 10. 🧰 Outils (par usage)

### Reconnaissance & scan 🟡

| Outil | Usage |
|---|---|
| **nmap** | Découverte d'hôtes/ports/services, scripts NSE |
| **ping / arp / tracert / tracert** | Connectivité, chemin réseau |
| **dig / nslookup** | Interrogation DNS |
| **whois** | Infos de domaine/IP |
| **hping** | Forge de paquets, tests |
| **curl** | Requêtes HTTP en CLI |

### Analyse réseau & paquets 🟡

- **Wireshark** (analyse graphique), **tcpdump** (capture CLI), **netstat/ss**, **ipconfig/ifconfig**, **iptables**, **route**.

### SIEM / logs à connaître 🟡

**Event Logs** (Windows), **syslog** (Unix), **NetFlow** (flux réseau), **captures de paquets**, **logs de pare-feu**. Savoir **où les trouver** et **les corréler**.

### Analyse de malware / URL (sandbox en ligne) 🟡

| Outil | Usage |
|---|---|
| **VirusTotal** | Multi-moteur fichiers/URL |
| **Joe Sandbox / any.run** | Détonation comportementale |
| **urlscan.io / urlvoid** | Analyse d'URL |
| **WHOIS** | Réputation de domaine |

### Forensics & investigation 🔴

- **FTK Imager** (imagerie disque), **Autopsy** (analyse), **WinHex** (éditeur hexa), **memdump** (capture RAM), `dd` (copie brute).

### Distributions offensives 🟡

- **Kali Linux**, **Parrot OS** (préchargées d'outils de pentest).

### LOLBAS / GTFOBINS / WADCOMS 🔴

> [!TIP]
> Détourner des **binaires légitimes** pour contourner les défenses (*Living Off The Land*).
> - **GTFOBins** — binaires Unix/Linux détournables (escalade, bypass).
> - **LOLBAS** — équivalent Windows (binaires/scripts signés Microsoft).
> - **WADCOMS** — matrice d'outils/commandes pour Active Directory.
> Indispensable à connaître **côté Red Team** comme **Blue Team** (détection des abus).

### Exploit frameworks 🔴

**Metasploit** (le plus connu), **Cobalt Strike** (C2 commercial), **Sliver**, **Impacket** (outils AD/SMB en Python).

---

## 11. 🎓 Certifications

> [!NOTE]
> Les certifs **valident** et **structurent** l'apprentissage, mais ne remplacent pas la pratique. Classées par niveau.

### Débutant / fondamentaux 🟢

| Certif | Domaine |
|---|---|
| **CompTIA A+** | Support IT |
| **CompTIA Network+** | Réseau |
| **CompTIA Linux+** | Linux |
| **CompTIA Security+** | Sécurité (excellente porte d'entrée) |
| **CCNA** (Cisco) | Réseau |

### Intermédiaire / avancé 🔴

| Certif | Orientation |
|---|---|
| **CEH** | Hacking éthique (théorique) |
| **OSCP** (OffSec) | **Pentest pratique** (très reconnue, 100% hands-on) |
| **GPEN / GWAPT / GSEC** (GIAC) | Pentest / web / sécurité générale |
| **CREST** | Pentest (UK/international) |
| **CISA** | Audit SI |
| **CISM** | Management de la sécurité |
| **CISSP** (ISC²) | Management/architecture (la plus demandée côté gouvernance) |

> [!TIP]
> Pour viser des **rôles techniques** (infra sécurisée, pentest) : **Security+** → **OSCP** / certifs pratiques sont souvent plus valorisées que les certifs purement théoriques.

---

## 12. 🚩 CTF & plateformes d'entraînement

> [!IMPORTANT]
> La pratique est **non négociable**. Les **CTF** (Capture The Flag) et labs apprennent plus vite que n'importe quel cours.

| Plateforme | Pour qui |
|---|---|
| **TryHackMe** | Débutants → intermédiaires (parcours guidés) |
| **HackTheBox** | Intermédiaire → avancé (machines réalistes) |
| **picoCTF** | Débutants (pédagogique, par l'université Carnegie Mellon) |
| **VulnHub** | VM vulnérables à télécharger (offline) |
| **SANS Holiday Hack Challenge** | Événement annuel ludique |

Types d'épreuves CTF : **Web**, **Pwn/Binary exploitation**, **Reverse**, **Crypto**, **Forensics**, **OSINT**, **Stéganographie**.

---

## 🔭 Aller plus loin

> [!TIP]
> **Transformer ce fichier en vrai « second cerveau » Obsidian :**
> 1. Ce document est un **MOC** (*Map of Content*) : un point d'entrée unique.
> 2. Pour exploiter le **graphe** d'Obsidian, éclater chaque grande section (ou chaque concept) en **note atomique** reliée par des `[[wikilinks]]` — ex. `[[Triade CIA]]`, `[[OWASP Top 10]]`, `[[Kerberos]]`, `[[Nmap]]`.
> 3. Ajouter des **tags** par domaine (`#réseau`, `#pentest`, `#blue-team`) pour filtrer.
> 4. Les callouts et le frontmatter de ce fichier sont déjà compatibles Obsidian **et** GitHub.

### Idées d'extension

- Fiches **« commandes »** dédiées (nmap, tcpdump, PowerShell AD…).
- Un dossier **`/writeups`** pour tes CTF (TryHackMe/HTB).
- Une note **« Veille »** (flux RSS, comptes à suivre, CVE du jour).
- Lier ce socle à ton objectif : **infra sécurisée** & **pentest** (approfondir AD, Active Directory attack paths, réseau, exploitation).

---

> [!NOTE]
> Source originale : [roadmap.sh/cyber-security](https://roadmap.sh/cyber-security) — version interactive et à jour.
> Ce fichier enrichit la roadmap à des fins de révision ; vérifier les détails sensibles (CVE, versions) avant tout usage opérationnel.
