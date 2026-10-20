# TP_RAG_working_on_Myresume
# 📚 TP4 : Système RAG (Retrieval-Augmented Generation) & Évaluation LLM-as-a-Judge

Ce projet implémente un pipeline complet de **Génération Augmentée par Récupération (RAG)** avec l'écosystème **LangChain**, une base vectorielle persistante **ChromaDB**, et un protocole automatisé d'évaluation de fidélité au contexte (**LLM-as-a-Judge**) basé sur le raisonnement pas-à-pas (*Chain-of-Thought*).

Le système a été développé et validé sur un document semi-structuré au format PDF (CV technique au format ATS).

---

## 🏛️ Architecture du Pipeline

```text
[ Document PDF ] 
       │
       ▼ (PyPDFLoader)
[ Document Splitting ] ── (RecursiveCharacterTextSplitter / tiktoken)
       │
       ▼
[ Segments / Chunks ] 
       │
       ▼ (Modèle d'Embedding : all-MiniLM-L6-v2)
[ Vecteurs denses ] ──► Stockage persistant : ChromaDB
                               │
[ Requête Utilisateur ] ───────┼──► [ Retriever : Similarity Search (k=5) ]
                               │                  │
                               ▼                  ▼
                     [ Contexte Extrait + Prompt Sécurisé ]
                               │
                               ▼ (Génération : Groq / LLM)
                     [ Réponse du Système RAG ]
                               │
                               ▼
            [ Arbitre Automatisé : LLM-as-a-Judge ]
            (Évaluation Groundedness / Faithfulness sur une échelle de 1 à 5)
