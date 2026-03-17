---
marp: true
theme: default
paginate: true
backgroundColor: #ffffff
color: #1a1a2e
style: |
  section {
    font-family: 'Segoe UI', Arial, sans-serif;
    padding: 48px 58px;
  }
  h1 {
    color: #16213e;
    font-size: 1.75em;
    border-bottom: 3px solid #0f3460;
    padding-bottom: 12px;
  }
  h2 {
    color: #0f3460;
    font-size: 1.28em;
  }
  strong { color: #e94560; }
  table {
    font-size: 0.76em;
    width: 100%;
  }
  th { background: #0f3460; color: white; padding: 6px 10px; }
  td { padding: 5px 10px; border-bottom: 1px solid #ddd; }
  ul { line-height: 1.7; }
  section.compact {
    font-size: 0.9em;
    line-height: 1.25;
    padding: 42px 52px;
  }
  section.compact table { font-size: 0.7em; }
  section.compact ul { line-height: 1.45; }
  .tag {
    background: #0f3460;
    color: white;
    padding: 3px 10px;
    border-radius: 12px;
    font-size: 0.7em;
  }
---

<!-- _backgroundColor: #16213e -->
<!-- _color: #ffffff -->

# [Biology-driven insights into the power of single-cell foundation models](https://doi.org/10.1186/s13059-025-03781-6)

<br>

**Genome Biology** · October 2025  
🔗 Paper: https://doi.org/10.1186/s13059-025-03781-6

> *Les scFMs apprennent-ils vraiment de la biologie — ou juste de la statistique ?*

<br>

🧬 Benchmarking · Foundation Models · Single-Cell · Computational Biology

---

# Contexte : Le scepticisme autour des scFMs

Les modèles fondationnels single-cell (**scGPT, Geneformer, UCE, scCello**…) promettaient tout.

Mais les études précédentes concluaient :

> *"Les baselines simples (HVG, scVI) font aussi bien — à quoi ça sert ?"*

<br>

### Le vrai problème

Les benchmarks standard (scIB) ne capturent **pas la structure biologique** des embeddings.

Ils mesurent la performance brute — pas si le modèle *comprend* la biologie cellulaire.

**→ Ce papier propose de changer les règles du jeu.**

---
<!-- _class: compact -->

# Nouvelles métriques bio-informées

Deux métriques originales basées sur l'**ontologie cellulaire** (Cell Ontology graph) :

| Métrique | Ce qu'elle mesure |
|----------|-------------------|
| **scGraph-OntoRWR** | Cohérence des relations entre types cellulaires dans l'espace latent vs. l'ontologie |
| **LCAD** *(Lowest Common Ancestor Distance)* | Gravité des erreurs d'annotation — confondre deux types proches ≠ confondre deux types distants |

<br>

### Tâches évaluées (6 scFMs × 5 datasets)

- 🧬 Gene embeddings (Gene Ontology)
- 🔬 Batch integration & cell type annotation
- 🎯 **Cancer cell ID + Drug sensitivity prediction** (clinique)

---
<!-- _class: compact -->

# Résultats : Les scFMs valent bien plus que prévu

Sur les métriques classiques → scFMs ≈ scVI (sans surprise)

Sur les métriques bio-informées → **scFMs dominent largement** :

| Modèle | Bio-conservation | Ontologie (OntoRWR) | Tâches cliniques |
|--------|-----------------|---------------------|-----------------|
| **UCE** | ✅ | ✅ meilleur global | ✅ |
| **scCello** | ✅ meilleur | ✅ +38.8% vs scVI | ✅ |
| scGPT | batch correction | — | ✅ |
| Geneformer | ❌ | ❌ | — |

<br>

**Insight clé :** Un espace latent plus *lisse* (smooth landscape) = meilleures performances downstream → argument fort pour les architectures type scPRINT.

---
<!-- _class: compact -->

# Conclusion & Ce que ça change

### Pour la recherche

- ✅ Les scFMs **apprennent vraiment de la biologie**, pas juste des corrélations
- ✅ Les benchmarks passés **sous-estimaient** leur valeur — il faut des métriques bio-aware
- ✅ Plug-and-play : les embeddings zero-shot boostent n'importe quel modèle aval

### Recommandations pratiques

> Utiliser **UCE** ou **scCello** comme feature extractor → gains immédiats sans réentraînement

### Lien avec scPRINT-2

Ce travail valide directement l'approche de scPRINT : concevoir des modèles dont les représentations capturent la **structure hiérarchique de la biologie cellulaire**, mesurée par des métriques adaptées.

<br>

📄 *Genome Biology 26:334 · DOI: 10.1186/s13059-025-03781-6*  
🔗 https://doi.org/10.1186/s13059-025-03781-6
