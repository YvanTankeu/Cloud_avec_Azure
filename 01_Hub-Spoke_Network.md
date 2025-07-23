
# Architecture Hub-and-Spoke avec Azure Firewall comme NVA

## 🎯 Objectif

Mettre en place une architecture réseau Hub-and-Spoke dans Microsoft Azure. Le but est de permettre à deux réseaux Spoke (un pour le développement, un pour la production) de communiquer entre eux uniquement via un réseau central (Hub), qui intègre un Azure Firewall servant de NVA (Network Virtual Appliance).

---

## 🧩 Scénario en entreprise

Imaginons que vous travaillez pour une entreprise qui souhaite isoler ses environnements (développement vs production) tout en permettant des communications contrôlées et sécurisées entre eux. Pour cela, vous allez :

Créer trois réseaux virtuels :

- vnet-hub-canadacentral-001 (le Hub)

- vnet-spokedev-canadacentral-001 (Spoke Dev)

- vnet-spokeprod-canadacentral-001 (Spoke Prod)

Déployer un Azure Firewall (azfw) dans le Hub

Appliquer des tables de routage personnalisées (UDR) dans les Spokes pour forcer le trafic inter-spoke à passer par le Hub

S’assurer que les deux VMs (une dans chaque Spoke) ne peuvent communiquer que via le Firewall

---
## 📊 Schéma
<img width="1536" height="1024" alt="01_Hub-Spoke_Network md" src="https://github.com/user-attachments/assets/da1db8a8-6985-488f-900a-a83feb55026f" />


---

## 📝 Remarque

- La communication entre SpokeDev et SpokeProd **passe uniquement par le Firewall** dans le Hub.


---
## 🧱 Composants Azure utilisés

| Ressource                             | Type                   | Détails                         |
|--------------------------------------|------------------------|----------------------------------|
| `vnet-hub-canadacentral-001`         | Réseau virtuel         | Adresse : `10.0.0.0/16`          |
| `vnet-spokedev-canadacentral-001`    | Réseau virtuel         | Adresse : `192.168.0.0/29`       |
| `vnet-spokeprod-canadacentral-001`   | Réseau virtuel         | Adresse : `172.0.0.0/28`         |
| `azfw`                                | Azure Firewall         | IP privée : `10.0.1.64`          |
| `vm-test-dev-can1-01`                | Machine virtuelle      | IP : `192.168.0.4`               |
| `vm-test-prod-can1-01`               | Machine virtuelle      | IP : `172.0.0.4`                 |
| `rt-vnetdev-to-vnetprod`             | Table de routage       | UDR Dev → Hub                   |
| `rt-vnetprod-to-vnetdev`             | Table de routage       | UDR Prod → Hub                  |
<img width="1414" height="467" alt="image" src="https://github.com/user-attachments/assets/749738f1-d202-4897-9599-95942549eef0" />

---

## 🔁 Peering mis en place

| Source VNet                         | Destination VNet                  | Peering directionnel | Remarques                    |
|------------------------------------|-----------------------------------|-----------------------|------------------------------|
| `vnet-spokedev-canadacentral-001` | `vnet-hub-canadacentral-001`     | Bidirectionnel        | Dev → Hub                   |
| `vnet-spokeprod-canadacentral-001`| `vnet-hub-canadacentral-001`     | Bidirectionnel        | Prod → Hub                  |
| ❌                                | ❌                                | ❌                     | Pas de peering direct Dev ↔ Prod |
<img width="1823" height="585" alt="rules8" src="https://github.com/user-attachments/assets/2b790ede-3387-41c8-81bb-9670742d68ea" />

---

## 📡 Routage défini

### Table de routage `rt-vnetdev-to-vnetprod` (appliquée à Spoke Dev)
| Adresse destination | Next Hop      |
|---------------------|---------------|
| `172.0.0.0/28`      | `10.0.1.64` (Firewall) |
<img width="1816" height="611" alt="rules6" src="https://github.com/user-attachments/assets/eec425e5-795c-4a2e-bf9d-692f77464838" />


### Table de routage `rt-vnetprod-to-vnetdev` (appliquée à Spoke Prod)
| Adresse destination | Next Hop      |
|---------------------|---------------|
| `192.168.0.0/29`    | `10.0.1.64` (Firewall) |
<img width="1876" height="560" alt="rules7" src="https://github.com/user-attachments/assets/dc04d75c-cd11-4feb-8152-7148166c32b7" />

---

## 🔐 Règles de Firewall

Le firewall autorise explicitement la communication entre les deux VM :
- Règle de destination : autoriser le trafic entre `192.168.0.4` ↔ `172.0.0.4` (TCP, ICMP, etc.)
- <img width="1676" height="667" alt="rules3" src="https://github.com/user-attachments/assets/9819f9e5-cbb9-4e61-804f-be950b7a25d4" />

---

## 🧪 Tests effectués

- ✅ La communication entre Spoke Dev et Spoke Prod fonctionne **via le Hub**.
- 🧪 Test de connectivité (`ping(icmp)`, `nc(tcp)`) validé entre les VMs.

---




