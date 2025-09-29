# sheLLM
An operating shell for LLMs. A protocol that transforms conversational interaction into a stateful, programmable command-line session for advanced persona management.

<p align="center">
  <img src="./assets/sheLLM.png" alt="sheLLM Logo" width="700"/>
</p>

<p align="center">
  <a href="https://github.com/VOTRE-NOM/sheLLM/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/License-MIT-white.svg" alt="License: MIT">
  </a>
  <img src="https://img.shields.io/badge/Contributions-Welcome-brightgreen.svg" alt="Contributions Welcome">
  <img src="https://img.shields.io/github/stars/Noenr/sheLLM?style=social" alt="GitHub stars">
</p>

<h1 align="center">sheLLM</h1>
<p align="center"><i>Un shell d'exploitation pour l'ère de l'intelligence artificielle.</i></p>

---

**sheLLM** est un protocole qui transforme l'interaction conversationnelle avec les Large Language Models (LLMs) en une session de commande stateful et programmable. Il dote les LLMs d'un shell conversationnel pour la gestion avancée de personas, le contrôle de l'output et la persistance de la mémoire.

## ✨ Fonctionnalités Principales

-   **🤖 Gestion de Personas Persistants :** Créez (`/uCR`), chargez (`/uX`) et supprimez (`/uDEL`) des profils utilisateurs avec leur propre configuration mémorisée.
-   **⌨️ Interface de Commande Intuitive :** Pilotez le style (`/Sp`), le format (`/Fo`) et la structure (`/Me`) des réponses du LLM avec une syntaxe simple et puissante.
-   **🧠 Interaction Stateful par Session :** Initialisez un persona en début de chat et interagissez avec lui de manière contextuelle. Le LLM se souvient de l'état de l'agent pour toute la durée du chat.
-   **🔒 Protocole Strict et Validable :** Une syntaxe claire et une politique de tolérance zéro pour les erreurs, garantissant des interactions fiables et prévisibles.

## 🚀 Comment ça Marche ?

`sheLLM` fonctionne comme une couche d'interprétation de commandes qui s'exécute avant que le LLM ne traite le prompt.

1.  **Création :** Un utilisateur est créé via `/uCR` avec un fichier de configuration définissant son `USER_ID` et ses règles.
2.  **Initialisation :** L'utilisateur est chargé en mémoire pour la session de chat via `/u0`, `/u1`, etc.
3.  **Exécution :** Les commandes suivantes (`/SpC`, `/MeLi`...) sont interceptées pour modifier le comportement de l'IA sans avoir à les ré-expliquer.

### Exemple d'utilisation

```bash
# 1. Créer un nouvel utilisateur "u1" à partir d'un fichier de conf
/uCR "u1" + [Contenu du fichier de configuration avec USER_ID = "u1"]

# 2. Initialiser une session avec ce nouvel utilisateur
/u1 /SpC /Fo -m /MeLi Bonjour, présente-toi.

# 3. La configuration est maintenant active. Les commandes suivantes sont plus courtes.
# Le LLM se souvient d'utiliser un langage courant, du Markdown et des listes.
Fais-moi une liste des planètes du système solaire.
