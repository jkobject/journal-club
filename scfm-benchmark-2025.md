# Biology-driven insights into the power of single-cell foundation models

**Source:** Genome Biology, 3 octobre 2025  
**DOI:** 10.1186/s13059-025-03781-6  
**Lien:** https://pmc.ncbi.nlm.nih.gov/articles/PMC12492631/

---

## En une phrase

Ce papier propose un benchmark biologically-informed de 6 modèles fondationnels single-cell (scFMs), révélant qu'ils capturent des structures biologiques sous-estimées par les métriques classiques — et ouvre la voie à leur usage comme modules plug-and-play pour des tâches cliniquement pertinentes.

---

## Contexte & Motivation

Les scFMs (scGPT, Geneformer, UCE, scCello, LangCell, scFoundation) ont suscité beaucoup d'espoir mais aussi de scepticisme : plusieurs études précédentes montraient que des baselines simples (HVG, scVI) les égalaient sur les benchmarks standards. Le problème ? Ces benchmarks ne captent pas les **structures biologiques relationnelles** entre types cellulaires — ils évaluent la performance brute, pas la qualité des représentations.

---

## Ce qu'ils font

**Tâches évaluées :**
- 🧬 **Gene-level** : qualité des embeddings de gènes (comparaison avec FRoGS sur Gene Ontology)
- 🔬 **Cell-level** : intégration de batches, annotation de types cellulaires
- 🎯 **Tâches cliniques** : identification de cellules cancéreuses, prédiction de sensibilité aux drogues

**Nouvelles métriques proposées :**
- `scGraph-OntoRWR` : mesure si les relations entre types cellulaires dans l'espace latent sont cohérentes avec l'ontologie cellulaire (Cell Ontology graph)
- `LCAD` (Lowest Common Ancestor Distance) : mesure la gravité des erreurs d'annotation — confondre deux types proches dans l'ontologie est moins grave que confondre des types distants

---

## Résultats clés

| Modèle | Batch integration (scIB) | Bio-conservation (scIB) | Ontologie (scGraph-OntoRWR) |
|--------|--------------------------|-------------------------|-----------------------------|
| scGPT | ✅ meilleur | — | — |
| scCello | — | ✅ meilleur | ✅ meilleur |
| UCE | — | — | ✅ meilleur global |
| Geneformer | — | ❌ mauvais | ❌ mauvais |

**Insight principal :** Les scFMs *ne* surpassent pas scVI sur les métriques classiques — mais ils **surpassent largement scVI sur les métriques bio-informées** (+38.8% pour scCello en PPC). Les benchmarks passés sous-estimaient donc systématiquement leur valeur.

**Tâches cliniques :** Les scFMs montrent des avantages nets sur les baselines pour l'identification de cellules tumorales et la prédiction de drug sensitivity (transfert bulk → single-cell).

---

## Conclusion & Implications

1. **Les scFMs apprennent vraiment de la biologie** — pas juste des patterns statistiques
2. **Les métriques classiques sont insuffisantes** — il faut des métriques biologically-aware
3. **Usage plug-and-play** : les embeddings zero-shot des scFMs peuvent booster n'importe quel modèle aval, sans réentraînement
4. **Recommandation pratique** : utiliser UCE ou scCello comme feature extractor, pas comme modèle seul

---

## Pertinence pour scPRINT

Ce travail valide l'importance des benchmarks biologiquement informés — exactement ce que scPRINT-2 cherche à adresser avec ses propres métriques. La notion de "smoother latent landscape" (paysage latent plus lisse → meilleure performance downstream) est un argument direct pour justifier l'architecture scPRINT.
