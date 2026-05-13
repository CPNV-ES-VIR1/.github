# VIR1 - LABO PAYROLL

Voici la ROADMAP du laboratoire.

---

## STEP 00 - Mise en place de l'environnement

- [ ] Valider l'invitation à votre dépôt (voir dans gh->organisation)
- [ ] Clone votre dépôt
- [ ] Initialiser Git-flow
- [ ] Ajouter l'upstream vers le dépôt ["start-point"](https://github.com/CPNV-ES-VIR1/payroll-start-point)
- [ ] Publier votre branche develop sur votre dépôt
- [ ] Déployer la solution en lisant attentivement le README
- [ ] Tester un maximum de commande décrites dans le README pour prendre en main le projet

---

## STEP 01 - Ajout du service "Customers"

- [ ] Intégrer la branche ["/feature/customers"](https://github.com/CPNV-ES-VIR1/payroll-start-point/tree/feature/customers) à votre dépôt
- [ ] [Télécharger l'archive contenant le nouveau service](https://etml-es-devops.s3.eu-west-1.amazonaws.com/customers.zip)
- [ ] Etudier le schéma livré dans le README.
- [ ] Réaliser les modifications par couche (docker-compose, api-gateway, ajout du service) afin d'intégrer le service
- [ ] Tester le nouveau service

```bash
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

---

## STEP 02 - Ajout du service "Departments"

- [ ] Intégrer la branche ["/feature/departments"](https://github.com/CPNV-ES-VIR1/payroll-start-point/tree/feature/departments) à votre dépôt
- [ ] [Télécharger l'archive contenant le nouveau service](https://etml-es-devops.s3.eu-west-1.amazonaws.com/ms-departments.zip)
- [ ] Etudier le schéma livré dans le README.
- [ ] Réaliser les modifications par couche (docker-compose, api-gateway, ajout du service) afin d'intégrer le service
- [ ] Tester le nouveau service (vous obtenez d'abord cette erreur)

```bash
curl -X GET localhost/api/v1/departments | jq
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   107    0   107    0     0   3870      0 --:--:-- --:--:-- --:--:--  3962
{
  "timestamp": "2026-05-05T13:36:32.475+00:00",
  "status": 404,
  "error": "Not Found",
  "path": "/api/v1/departments"
}
```

- [ ] Des erreurs sont présentes dans le conteneurs "departments"... à vous de jouer ! (aidez-vous du microservice "employees")

```bash
curl -X GET localhost/api/v1/departments | jq

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100     2    0     2    0     0     13      0 --:--:-- --:--:-- --:--:--    13
[]
```

- [ ] [Solution proposée](https://github.com/CPNV-ES-VIR1/payroll-start-point/tree/feature/departments-solution)

---

## STEP 03 - Ajout du service "Employees POST"

- [ ] Intégrer la branche ["/feature/employees-post"](https://github.com/CPNV-ES-VIR1/payroll-start-point/tree/feature/employees-post) à votre dépôt
- [ ] [Télécharger l'archive contenant le nouveau service](https://etml-es-devops.s3.eu-west-1.amazonaws.com/ms-post.zip)
- [ ] Etudier le schéma livré dans le README.
- [ ] Réaliser les modifications par couche (docker-compose, api-gateway, ajout du service) afin d'intégrer le service

Aide :

Nginx permet d'utiliser des "upstreams" pour gérer le routage à l'aide du verbe HTTP.

```bash
//nginx.conf
//ajout d un upstream
  upstream microservice_get {
      server ms-payroll-employees-get:8080;
  }

//utilisation d une map pour éviter les if/else imbriqués
  map $request_method $upstream_service {
      GET     microservice_get;
      default "";
  }

//utilisation des upstreams pour rerouter les appels entrants
location /api/v1/employees {
    if ($upstream_service = "") {
        return 405;
    }

    proxy_pass http://$upstream_service;
}
```

- [ ] Tester la création d'un employé

```
    /* curl sample :
    curl -i -X POST localhost/api/v1/employees \
        -H 'Content-type:application/json' \
        -d '{\"name\": \"Russel George\", \"role\": \"gardener\"}'
    */
```
- [ ] Valider la création en appelant le ms-employees-get

- [ ] Prouver techniquement comment valider que notre infrastructure fonctionne bien comme attendue, sans provoquer d'interruption de service
