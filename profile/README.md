# VIR1 - LABO PAYROLL

Voici la ROADMAP du laboratoire.

## STEP 00 - Mise en place de l'environnement

- [ ] Valider l'invitation à votre dépôt (voir dans gh->organisation)
- [ ] Clone votre dépôt
- [ ] Initialiser Git-flow
- [ ] Ajouter l'upstream vers le dépôt ["start-point"](https://github.com/CPNV-ES-VIR1/payroll-start-point)
- [ ] Publier votre branche develop sur votre dépôt
- [ ] Déployer la solution en lisant attentivement le README
- [ ] Tester un maximum de commande décrites dans le README pour prendre en main le projet

## STEP 01 - Ajout du service "Customers"

- [ ] Intégrer la branche ["/feature/customers"](https://github.com/CPNV-ES-VIR1/payroll-start-point/tree/feature/customers) à votre dépôt
- [ ] [Télécharger l'archive contenant le nouveau service](https://etml-es-devops.s3.eu-west-1.amazonaws.com/customers.zip)
- [ ] Etudier le schéma livré dans le README.
- [ ] Réaliser les modifications par couche (docker-compose, api-gateway, ajout du service) afin d'intégrer le service
- [ ] Tester le nouveau service

```
curl -X GET localhost/api/v1/customers/1 | jq
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   185  100   185    0     0  12871      0 --:--:-- --:--:-- --:--:-- 13214
{
  "id": 1,
  "name": "Davis",
  "firstname": "Elijah",
  "phoneNumber": "+1-944-867-1271",
  "emailAddress": "elijah.davis@mail.com",
  "created_at": "2026-04-29 10:43:39",
  "updated_at": "2026-04-29 10:43:39"
}
```
- [ ] [La solution proposée](https://github.com/CPNV-ES-VIR1/payroll-start-point/tree/feature/customers-solution)
