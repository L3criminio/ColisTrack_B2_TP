# Rapport d'audit — à compléter

Auteur : Grégory
Date : 09/11/2026
Référence de départ (commit) : commit documentaire

| ID constat | Règle CT | Fichier et fonction | Reproduction / observation | Impact | Priorité P0/P1/P2 | Action (corriger / surveiller / différer) |
|---|---|---|---|---|---|---|
| A-01 | CT-06 | `src/fees.js`, `calculateShippingFee` | -1 kg, FR -> 4 € au lieu d'une `RangeError`. Poids et zone non vérifiés. | Tarif calculé sur des données invalides. | P1 | Corriger : vérifier poids et zone -> tester poids valides, invalides (0, -1, NaN, infinis, texte) et zones FR/EU/inconnues. |
| A-02 | CT-07 | `src/tracking.js`, `getPublicTracking` | Suivi public -> contient aussi l'e-mail. | E-mail visible publiquement. | P1 | Corriger : retirer l'e-mail -> 2 tests : champs exacts et historique indépendant du colis. |
| A-03 | CT-08 | `src/php/TrackingPresenter.php`, `publicCard` | Carte publique -> contient aussi l'e-mail. | E-mail visible publiquement. | P1 | Corriger : retirer l'e-mail -> 2 tests : champs exacts et libellés conservés (dont « Inconnu »). |
| A-04 | CT-02 | `src/shipment.js`, `advanceShipment` | `created -> delivered` accepté. Retours et répétitions aussi. | Étapes de livraison contournées. | P1 | Corriger : imposer l'ordre des étapes -> 4 cas à tester : parcours normal, saut, retour et répétition. |
| A-05 | CT-03 | `src/shipment.js`, `advanceShipment` | `canceled -> prepared` accepté. | Un colis annulé repart en livraison. | P1 | Corriger : bloquer toute évolution après livraison ou annulation -> tester les 2 états terminaux, erreur et objet inchangé. |
| A-06 | CT-04 | `src/shipment.js`, `cancelShipment` | `in_transit -> canceled` accepté. | Annulation alors que le colis est en route. | P1 | Corriger : autoriser seulement `created` et `prepared` -> tester les 5 statuts, l'historique et l'objet inchangé si refus. |

## Dette différée et justification

## Contrôles avant modification

## Contrôles après modification

## Limites et risques résiduels
